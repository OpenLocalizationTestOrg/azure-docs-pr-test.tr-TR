---
title: "Azure'da hiper ölçekli uygulaması oluşturma | Microsoft Docs"
description: "Farklı Azure Hizmetleri Azure ASP.NET uygulama performansını en üst düzeye çıkarmak için nasıl kullanılacağını öğrenin."
services: app-service\web
documentationcenter: dotnet
author: cephalin
manager: erikre
editor: 
ms.assetid: a4d49ac7-0f97-4997-84c5-cdb9c4465757
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 03/23/2017
ms.author: cephalin
ms.openlocfilehash: eac9c5b0d8d0f7802d88e6f4f27d9d23c406e025
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a>Azure'da hiper ölçekli web uygulaması oluşturma

Bu öğretici, kullanıcı isteklerini en üst düzeye çıkarmak için azure'da ASP.NET web uygulamasını genişletmek nasıl gösterir.

Bu öğreticiye başlamadan önce emin olun [Azure CLI yüklenmiş](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) makinenizde. Ayrıca, gereksinim duyduğunuz [Visual Studio](https://www.visualstudio.com/vs/) örnek uygulamayı çalıştırmak için yerel makinenizde.

## <a name="step-1---get-sample-application"></a>1. adım - Get örnek uygulama
Bu adımda, yerel ASP.NET projesi ayarlayın.

### <a name="clone-the-application-repository"></a>Uygulama depoyu kopyalayın

Tercih ettiğiniz komut satırı Terminalini açın ve `CD` bir çalışma dizini için. Ardından örnek uygulamayı kopyalamak için aşağıdaki komutları çalıştırın. 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-the-sample-application-in-visual-studio"></a>Visual Studio'da örnek uygulamayı çalıştırın

Çözümü Visual Studio'da açın.

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

Tür `F5` uygulamayı çalıştırın.

Bu örnek ASP.NET web uygulaması ve varsayılan şablondan gelir ve kullanıcı devam ediyorsa oturumlar ve çıktı önbelleği kullanır. Bir göz atalım `HighScaleApp\Controllers\HomeController.cs`. `Index()` Yöntemi veri parçası oturumuna ekler.

```csharp
Session.Add("visited", "true"); 
```

Ve `About()` ve `Contact()` yöntemlerini çıkışı önbelleğe.

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-to-azure"></a>Adım 2 - Azure'a dağıtma
Bu adımda, Azure web uygulaması oluşturun ve ona örnek ASP.NET uygulamanızı dağıtın.

### <a name="create-a-resource-group"></a>Kaynak grubu oluşturma   
Kullanım [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) oluşturmak için bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md) Batı Avrupa bölgede. Bir kaynak grubu, olduğu gibi web uygulamasını ve herhangi bir SQL veritabanı arka uç birlikte, yönetmek istediğiniz tüm Azure kaynakları koyduğunuz yerdir.

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

Hangi olası değerleri görmek için kullanabileceğiniz `---location`, kullanın [az appservice listesi-konumları](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) komutu.

### <a name="create-an-app-service-plan"></a>App Service planı oluşturma
Kullanım [az uygulama hizmeti planı oluşturma](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) "B1" oluşturmak için [uygulama hizmeti planı](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

Bir uygulama hizmeti planı aynı uygulama hizmeti altyapı üzerinden veya birlikte ölçeklendirmek istediğiniz uygulamaları herhangi bir sayıda içerebilen bir ölçek birimidir. Her plan da atanmış bir [fiyatlandırma katmanı](https://azure.microsoft.com/en-us/pricing/details/app-service/). Daha yüksek katmanları daha iyi donanım ve daha fazla genişleme örnekleri gibi daha fazla özellik içerir.

Bu öğretici için üç örneklerine ölçek genişletme sağlayan en az katman B1 olur. İstediğiniz zaman, uygulamanızın yukarı veya aşağı fiyatlandırma katmanı ve daha sonra çalıştırarak taşıyabilirsiniz [az uygulama hizmeti planı güncelleştirme](https://docs.microsoft.com/cli/azure/appservice/plan#update). 

### <a name="create-a-web-app"></a>Web uygulaması oluşturma
Kullanım [az appservice web oluşturmak](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) benzersiz bir ad ile bir web uygulaması oluşturmak için `$appName`.

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a>Dağıtım kimlik bilgilerini ayarlama
Kullanım [az appservice web dağıtım kullanıcısı ayarlanmadı](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) için uygulama hizmeti hesabı düzeyinde dağıtım kimlik bilgilerinizi ayarlamak için.

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a>Git dağıtımı yapılandırma
Kullanım [az appservice web kaynak denetimi config-yerel-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) yerel Git dağıtımı yapılandırmak için.

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

Bu komut, aşağıdakine benzer bir çıktı sunar:

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

Döndürülen URL'ye Git uzaktan yapılandırmak için kullanın. Aşağıdaki komutu önceki çıktı örneği kullanır.

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-the-sample-application"></a>Örnek uygulama dağıtma
Şimdi örnek uygulamanızı dağıtmak hazırsınız. `git push` öğesini çalıştırın.

```powershell
git push azure master
```

Parola istendiğinde, ne zaman çalıştırıldığı belirtilen parolayı kullanmak `az appservice web deployment user set`.

### <a name="browse-to-azure-web-app"></a>Azure web uygulaması'na göz atın
Kullanım [az appservice web Gözat](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) uygulamanızı Azure'da çalışırken görmek için bu komutu çalıştırın.

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-to-redis"></a>Adım 3 - Redis için Bağlan
Bu adımda, Azure Redis önbelleği, Azure web uygulamanızın bir dış, birlikte bulunan önbellek olarak ayarlayın. Sayfa çıktısının önbelleğe almak için Redis hızlı bir şekilde kullanabilirler. Web uygulamalarınızı daha sonra ölçeklendirdiğinizde Ayrıca, Redis kalıcı yardımcı olan birden çok kullanıcı oturumlarında örnekleri güvenilir.

### <a name="create-an-azure-redis-cache"></a>Azure Redis Cache oluşturma
Kullanım [az redis oluşturma](https://docs.microsoft.com/en-us/cli/azure/redis#create) bir Azure Redis önbelleği oluşturmak ve JSON kaydetmek için çıktı. Benzersiz bir ad kullanmak `$cacheName`.

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-the-application-to-use-redis"></a>Redis kullanmak için uygulamayı yapılandırma
Önbellek hesabınız için bağlantı dizesi biçimi.

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

İkinci satır şuna benzer bir çıktı vermeniz gerekir:

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

Visual Studio'da adlı proje kök web yapılandırma dosyası oluşturma `redis.config` ve aşağıdaki kodu yapıştırın. İçinde `value`, PowerShell çıkış bağlantı dizesinden kullanın.

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

Bakarsanız `.gitignore` dosya Git deponuzu bu dosyayı kaynak denetiminden dışlandı görürsünüz. Bu şekilde, hassas bilgilerinizi güvenli tutulur. 

Açık `Web.config`. Bildirim `<appSettings file="redis.config">` oluşturduğunuz ayarını alır öğesi `redis.config`. 

İçeren açıklamalı bölüm Bul `<sessionState>` ve `<caching>`. Bu bölümde açıklamadan çıkarın.

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

Bu kod Redis bağlantı dizesi için tanımladığınız görünür `RedisConnection`. 

Uygulamanızı şimdi Redis oturumlar ve önbelleğe alma yönetmek için kullanır. Tür `F5` uygulamayı çalıştırın. İsterseniz, şimdi önbelleğe kaydedilen verileri görselleştirmek için bir Redis yönetim istemcisi yükleyebilirsiniz.

### <a name="configure-the-connection-string-in-azure"></a>Bağlantı dizesi Azure'da yapılandırın

Uygulamanızı Azure'da çalışması, Azure web uygulamanızda aynı Redis bağlantı dizesi yapılandırmanız gerekir. Bu yana `redis.config` tutulmaz kaynak denetiminde onu dağıtılmazsa Azure'a Git dağıtımı çalıştırdığınızda.

Kullanım [az appservice web yapılandırma appsettings güncelleştirme](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) aynı ada sahip bağlantı dizesi eklemek için (`RedisConnection`).

appSettings güncelleştirme--az appservice web yapılandırma ayarları "RedisConnection $connstring ="--$appName--kaynak-grubu myResourceGroup adı

Unutmayın `$connstring` biçimlendirilmiş bağlantı dizesi içeriyor.

### <a name="redeploy-the-application-to-azure"></a>Azure için uygulamayı yeniden Dağıt
Değişikliklerinizi Azure'a göndermek için Git komutları kullanın

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

Parola istendiğinde, ne zaman çalıştırıldığı belirtilen parolayı kullanmak `az appservice web deployment user set`.

### <a name="browse-to-the-azure-web-app"></a>Azure web uygulaması'na göz atın
Kullanım [az appservice web Gözat](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) Azure'da Canlı değişiklikleri görmek için.

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-to-multiple-instances"></a>4. adım - birden çok örneği için Ölçeklendir
Uygulama hizmeti planı, Azure web uygulamaları için ölçek birimidir. Web uygulamanızı ölçeklendirmek için uygulama hizmeti planı ölçeklendirin.

Kullanım [az uygulama hizmeti planı güncelleştirme](https://docs.microsoft.com/cli/azure/appservice/plan#update) en büyük sayı olan uygulama hizmeti planı üç örneklerine ölçeklendirmek için izin verilen B1 fiyatlandırma katmanı tarafından. B1 zaman uygulama hizmeti planı daha önce oluşturduğunuz seçtiğiniz fiyatlandırma katmanı olduğunu unutmayın. 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a>Adım 5 - ölçek coğrafi olarak
Coğrafi olarak ölçekleme sırasında Azure bulut birden çok bölgede uygulamanızı çalıştırın. Bu kurulum yük bakiyelerini Coğrafya hakkında daha fazla temel uygulamanızı ve uygulamanıza yakın istemci tarayıcıları koyarak yanıt süresini azaltır.

Bu adımda, ASP.NET web uygulamanızı sahip ikinci bir bölge için ölçeklendirme [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/). Adımın sonunda, Batı Avrupa (önceden oluşturulmuş) çalıştıran bir web uygulaması ve Güneydoğu Asya (henüz oluşturulmadı) çalıştıran bir web uygulaması gerekir. Her iki uygulamalar aynı trafik Yöneticisi URL'den sunulacak.

### <a name="scale-up-the-europe-app-to-standard-tier"></a>Standart katmanı Avrupa uygulamaya ölçeklendirin
App Service içinde Azure Traffic Manager ile tümleştirme standart fiyatlandırma katmanı gerektirir. Kullanım [az uygulama hizmeti planı güncelleştirme](https://docs.microsoft.com/cli/azure/appservice/plan#update) S1 için uygulama hizmeti planınızı ölçeklendirmek için. 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a>Traffic Manager profili oluşturma 
Kullanım [az ağ trafik Yöneticisi profili oluştur](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) bir trafik Yöneticisi profili oluşturun ve kaynak grubuna eklemek için. Benzersiz bir DNS adı $dnsName kullanın.

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> `--routing-method Performance`belirleyen bu profili [kullanıcı trafiğini en yakın uç noktasına yönlendirir](../traffic-manager/traffic-manager-routing-methods.md).

### <a name="get-the-resource-id-of-the-europe-app"></a>Avrupa uygulama kaynak Kimliğini Al
Kullanım [az appservice web Göster](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) , web uygulamanızın kaynak kimliği alınamadı.

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-the-europe-app"></a>Trafik Yöneticisi uç noktası Avrupa uygulama Ekle
Kullanmak [az ağ trafik Yöneticisi uç noktası oluşturma](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) bir uç nokta Traffic Manager profilinize ekleyin ve hedefi olarak, web uygulamanızın kaynak Kimliğini kullanın.

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-the-traffic-manager-endpoint-url"></a>Trafik Yöneticisi uç nokta URL'sini alma
Traffic Manager profilinizin artık mevcut web uygulamanıza işaret eden bir uç nokta sahiptir. Kullanım [az ağ trafik Yöneticisi profili Göster](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) URL'sini almak için. 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

Çıktı tarayıcınıza kopyalayın. Web uygulamanızı yeniden görmeniz gerekir.

### <a name="create-an-azure-redis-cache-in-asia"></a>Bir Azure Redis önbelleği Asya'da oluşturma
Şimdi, Azure web uygulamanızın Güneydoğu Asya bölgeye çoğaltılır. Başlatmak için kullanmak [az redis oluşturma](https://docs.microsoft.com/en-us/cli/azure/redis#create) Güneydoğu Asya ikinci bir Azure Redis önbelleği oluşturmak için. Bu önbellek Asya'da uygulamanızla birlikte olması gerekir.

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

`--name $cacheName-asia`önbellek ile Batı Avrupa önbellek adını verir `-asia` soneki.

### <a name="create-an-app-service-plan-in-asia"></a>Asya'da bir uygulama hizmeti planı oluştur
Kullanım [az uygulama hizmeti planı oluşturma](https://docs.microsoft.com/cli/azure/appservice/plan#create) Batı Avrupa plan aynı S1 katmanı kullanarak Güneydoğu Asya bölgesinde ikinci bir uygulama hizmeti planı oluşturulamadı.

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a>Asya'da bir web uygulaması oluşturma
Kullanım [az appservice web oluşturmak](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) ikinci bir web uygulaması oluşturma.

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

`--name $appName-asia`uygulama ile Batı Avrupa uygulama adını verir `-asia` soneki.

### <a name="configure-the-connection-string-for-redis"></a>Redis için bağlantı dizesini yapılandırma
Kullanım [az appservice web yapılandırma appsettings güncelleştirme](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) web uygulaması'na Güneydoğu Asya önbelleği için bağlantı dizesi eklemek için.

appSettings güncelleştirme--az appservice web yapılandırma ayarları "RedisConnection = $($redis.hostname): $($redis.sslPort), parola = $($redis.accessKeys.primaryKey) ssl = True, abortConnect = False"--ad $appName-Asya--kaynak-grubu myResourceGroup

### <a name="configure-git-deployment-for-the-asia-app"></a>Asya uygulaması için Git dağıtımı yapılandırın.
Kullanım [az appservice web kaynak denetimi config-yerel-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) ikinci web uygulaması için yerel Git dağıtımı yapılandırmak için.

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

Bu komut, aşağıdakine benzer bir çıktı sunar:

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

Döndürülen URL için yerel deponuza uzak ikinci Git yapılandırmak için kullanın. Aşağıdaki komutu önceki çıktı örneği kullanır.

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a>Örnek uygulamanızı dağıtma
Çalıştırma `git push` ikinci Git remote örnek uygulamanızı dağıtmak için. 

```bash
git push azure-asia master
```

Parola istendiğinde, ne zaman çalıştırıldığı belirtilen parolayı kullanmak `az appservice web deployment user set`.

### <a name="browse-to-the-asia-app"></a>Asya app uygulamanıza gözatma
Kullanım [az appservice web Gözat](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) uygulamanızı azure'da çalıştığını doğrulayın.

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-the-resource-id-of-the-asia-app"></a>Asya uygulama kaynak Kimliğini Al
Kullanım [az appservice web Göster](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) Güneydoğu Asya, web uygulamanızın kaynak kimliği alınamadı.

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-the-asia-app"></a>Trafik Yöneticisi uç noktası Asya uygulama Ekle
Kullanım [az ağ trafik Yöneticisi uç noktası oluşturma](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) ikinci bir uç nokta Traffic Manager profili eklemek için.

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-to-web-apps"></a>Web uygulamaları için bölge tanımlayıcısı ekleme
Kullanım [az appservice web yapılandırma appsettings güncelleştirme](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) bölgeye özgü ortam değişkeni eklemek için.

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

Uygulama kodunuz, bu uygulama ayarı zaten kullanıyor. Bir göz atalım `HighScaleApp\Views\Home\Index.cshtml`.

### <a name="complete"></a>Tamamlandı!

Şimdi, farklı coğrafi bölgelerde tarayıcılardan Traffic Manager profilinizin URL'sini erişmeyi deneyin. Avrupa istemci tarayıcılarından "ASP.NET Batı Avrupa" göstermesi gerekir ve Asya istemci tarayıcısından "ASP.NET Güneydoğu Asya" göstermesi gerekir

## <a name="more-resources"></a>Diğer kaynaklar
