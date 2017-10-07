---
title: "aaaBuild Azure hiper ölçekli uygulamada | Microsoft Docs"
description: "Nasıl toouse farklı Azure Hizmetleri toomaximize hello Azure ASP.NET uygulama performansını öğrenin."
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
ms.openlocfilehash: 7952647b49a82c286c6a737eb41a7f23a13fd75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a>Azure'da hiper ölçekli web uygulaması oluşturma

Bu öğretici, nasıl ASP.NET web uygulamasını Azure toomaximize kullanıcı çıkışı tooscale istekleri gösterir.

Bu öğreticiye başlamadan önce emin olun [Azure CLI yüklü hello](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) makinenizde. Ayrıca, gereksinim duyduğunuz [Visual Studio](https://www.visualstudio.com/vs/) , LocalMachine toorun hello örnek uygulamanızın üzerinde.

## <a name="step-1---get-sample-application"></a>1. adım - Get örnek uygulama
Bu adımda, hello yerel ASP.NET projesi ayarlayın.

### <a name="clone-hello-application-repository"></a>Kopya hello uygulama havuzu

Tercih ettiğiniz komut satırı Terminalini açın hello ve `CD` tooa çalışma dizini. Ardından, çalışma hello aşağıdaki tooclone Merhaba örnek uygulaması komutları. 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-hello-sample-application-in-visual-studio"></a>Visual Studio'da Hello örnek uygulamayı çalıştırın

Merhaba çözümü Visual Studio'da açın.

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

Tür `F5` toorun Merhaba uygulaması.

Bu örnek ASP.NET web uygulaması hello varsayılan şablondan gelir ve kullanıcı oturumlarını ve kullandığı hello çıktı önbelleği devam ettirir. Bir göz atalım `HighScaleApp\Controllers\HomeController.cs`. Merhaba `Index()` yöntemi, bir veri toohello oturum ekler.

```csharp
Session.Add("visited", "true"); 
```

Ve hello `About()` ve `Contact()` yöntemlerini çıkışı önbelleğe.

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-tooazure"></a>2. adım - tooAzure dağıtma
Bu adımda, Azure web uygulaması oluşturun ve örnek ASP.NET uygulama tooit dağıtın.

### <a name="create-a-resource-group"></a>Kaynak grubu oluşturma   
Kullanım [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) toocreate bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md) hello Batı Avrupa bölgede. Bir kaynak grubu burada tüm yerleştirdiğiniz olduğu gibi hello web app ve herhangi bir SQL veritabanı arka uç toomanage birlikte, istediğiniz Azure kaynakları hello.

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

toosee hangi olası değerler için kullanabilmeniz için `---location`, hello kullan [az appservice listesi-konumları](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) komutu.

### <a name="create-an-app-service-plan"></a>App Service planı oluşturma
Kullanım [az uygulama hizmeti planı oluşturma](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate "B1" [uygulama hizmeti planı](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

Bir uygulama hizmeti planı herhangi bir sayıda tooscale yedeklemek istediğiniz veya birlikte üzerinden aynı hello uygulamalar dahil edebileceğiniz bir ölçek birimi olan uygulama hizmeti altyapı. Her plan da atanmış bir [fiyatlandırma katmanı](https://azure.microsoft.com/en-us/pricing/details/app-service/). Daha yüksek katmanları daha iyi donanım ve daha fazla genişleme örnekleri gibi daha fazla özellik içerir.

Bu öğretici için toothree örnekleri genişleme sağlayan hello en az katman B1 olur. Her zaman yukarı veya aşağı daha sonra çalıştırarak fiyatlandırma katmanı hello uygulamanızı taşıyabilirsiniz [az uygulama hizmeti planı güncelleştirme](https://docs.microsoft.com/cli/azure/appservice/plan#update). 

### <a name="create-a-web-app"></a>Web uygulaması oluşturma
Kullanım [az appservice web oluşturmak](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate benzersiz bir ada sahip bir web uygulaması olarak `$appName`.

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a>Dağıtım kimlik bilgilerini ayarlama
Kullanım [az appservice web dağıtım kullanıcısı ayarlanmadı](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset hesap düzeyinde dağıtımınız için uygulama hizmeti kimlik bilgileri.

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a>Git dağıtımı yapılandırma
Kullanım [az appservice web kaynak denetimi config-yerel-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure yerel Git dağıtımı.

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

Bu komut, hello şu şekilde görünen bir çıktı sunar:

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

Kullanım Merhaba, Git URL'si tooconfigure uzak döndürdü. Merhaba aşağıdaki komut çıktısı örneğinde önceki hello kullanır.

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-hello-sample-application"></a>Merhaba örnek uygulaması dağıtma
Örnek uygulamanız şimdi hazır toodeploy şunlardır. `git push` öğesini çalıştırın.

```powershell
git push azure master
```

Parola istendiğinde, ne zaman çalıştırıldığı belirtilen hello parola kullanmak `az appservice web deployment user set`.

### <a name="browse-tooazure-web-app"></a>TooAzure web uygulaması Gözat
Kullanım [az appservice web Gözat](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee uygulamanızı Azure üzerinde çalışırken bu komutu çalıştırın.

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-tooredis"></a>3. adım - tooRedis Bağlan
Bu adımda, Azure Redis önbelleği dış, birlikte bulunan önbellek tooyour Azure web uygulaması ayarlayın. Sayfa çıktısının Redis toocache hızlı bir şekilde kullanabilirler. Web uygulamalarınızı daha sonra ölçeklendirdiğinizde Ayrıca, Redis kalıcı yardımcı olan birden çok kullanıcı oturumlarında örnekleri güvenilir.

### <a name="create-an-azure-redis-cache"></a>Azure Redis Cache oluşturma
Kullanım [az redis oluşturma](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate bir Azure Redis önbelleği ve JSON hello çıkış. Benzersiz bir ad kullanmak `$cacheName`.

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-hello-application-toouse-redis"></a>Merhaba uygulama toouse Redis yapılandırın
Önbelleğinizi Hello bağlantı dizesi biçimi.

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

Merhaba ikinci satırı şuna benzer bir çıktı vermeniz gerekir:

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

Visual Studio'da adlı proje kök web yapılandırma dosyası oluşturma `redis.config` ve Yapıştır hello aşağıdaki kod içine. İçinde `value`, hello PowerShell çıkış hello bağlantı dizesini kullanın.

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

Merhaba bakarsanız `.gitignore` dosya Git deponuzu bu dosyayı kaynak denetiminden dışlandı görürsünüz. Bu şekilde, hassas bilgilerinizi güvenli tutulur. 

Açık `Web.config`. Bildirim hello `<appSettings file="redis.config">` oluşturduğunuz hello ayarını alır öğesi `redis.config`. 

Merhaba geçersiz kılınan bulma içeren bölümü `<sessionState>` ve `<caching>`. Bu bölümde açıklamadan çıkarın.

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

Bu kod hello Redis bağlantı dizesi için tanımladığınız görünür `RedisConnection`. 

Uygulamanız artık Redis toomanage oturumlar ve önbelleğe alma kullanır. Tür `F5` toorun Merhaba uygulaması. İsterseniz, şimdi toohello önbelleğe kaydedilen bir Redis yönetim istemci toovisualize hello veriler indirebilirsiniz.

### <a name="configure-hello-connection-string-in-azure"></a>Azure'da Hello bağlantı dizesini yapılandırma

Azure'da, uygulama toowork için ihtiyacınız tooconfigure aynı Redis bağlantı dizesi, Azure web uygulamanızda hello. Bu yana `redis.config` tutulmaz kaynak denetiminde değil dağıtılan tooAzure Git dağıtımı çalıştırdığınızda.

Kullanım [az appservice web yapılandırma appsettings güncelleştirme](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd hello bağlantı dizesi hello ile aynı adı (`RedisConnection`).

appSettings güncelleştirme--az appservice web yapılandırma ayarları "RedisConnection $connstring ="--$appName--kaynak-grubu myResourceGroup adı

Unutmayın `$connstring` Merhaba biçimlendirilmiş bağlantı dizesi içeriyor.

### <a name="redeploy-hello-application-tooazure"></a>Merhaba uygulama tooAzure yeniden dağıtın
Git komutları toopush değişiklikleri tooAzure kullanın

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

Parola istendiğinde, ne zaman çalıştırıldığı belirtilen hello parola kullanmak `az appservice web deployment user set`.

### <a name="browse-toohello-azure-web-app"></a>Toohello Azure web uygulaması Gözat
Kullanım [az appservice web Gözat](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee hello değişiklikleri Canlı Azure'da.

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-toomultiple-instances"></a>4. adım - ölçek toomultiple örnekleri
Hello uygulama hizmeti planı hello ölçek birimi, Azure web uygulamaları için değil. tooscale web uygulamanızı çıkışı hello uygulama hizmeti planı ölçeklendirin.

Kullanım [az uygulama hizmeti planı güncelleştirme](https://docs.microsoft.com/cli/azure/appservice/plan#update) olan tooscale hello uygulama hizmeti planı toothree örnekleri, çıkışı hello fiyatlandırma katmanı hello B1 tarafından izin verilen maksimum sayıyı. B1 fiyatlandırma katmanı hello önceki uygulama hizmeti planı oluştururken seçtiğiniz hello olduğunu unutmayın. 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a>Adım 5 - ölçek coğrafi olarak
Coğrafi olarak ölçekleme hello Azure bulut birden çok bölgede uygulamanızı çalıştırın. Bu kurulum yük bakiyelerini Coğrafya hakkında daha fazla temel uygulamanızı ve uygulama daha yakından tooclient tarayıcılar koyarak hello yanıt süresini azaltır.

Bu adımda, ASP.NET web uygulaması tooa ikinci bölgenizi ile ölçeklendirme [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/). Hello adım Hello sonunda, Batı Avrupa (önceden oluşturulmuş) çalıştıran bir web uygulaması ve Güneydoğu Asya (henüz oluşturulmadı) çalıştıran bir web uygulaması gerekir. Her iki uygulamalar aynı trafik Yöneticisi URL hello sunulacak.

### <a name="scale-up-hello-europe-app-toostandard-tier"></a>Avrupa uygulama tooStandard katmanı Hello ölçeklendirme
App Service içinde Azure Traffic Manager ile tümleştirme hello standart fiyatlandırma katmanı gerektirir. Kullanım [az uygulama hizmeti planı güncelleştirme](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale uygulama hizmeti planı tooS1 ayarlama. 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a>Traffic Manager profili oluşturma 
Kullanım [az ağ trafik Yöneticisi profili oluştur](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate trafik Yöneticisi profili ve tooyour kaynak grubunu ekleyin. Benzersiz bir DNS adı $dnsName kullanın.

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> `--routing-method Performance`belirleyen bu profili [kullanıcı trafiği toohello yakın endpoint yönlendirir](../traffic-manager/traffic-manager-routing-methods.md).

### <a name="get-hello-resource-id-of-hello-europe-app"></a>Merhaba kaynak hello Avrupa uygulama Kimliğini Al
Kullanım [az appservice web Göster](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) , web uygulamanızın tooget hello kaynak kimliği.

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-europe-app"></a>Trafik Yöneticisi uç noktası hello Avrupa uygulaması ekleyin
Kullanmak [az ağ trafik Yöneticisi uç noktası oluşturma](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd bir uç nokta tooyour trafik Yöneticisi profili ve kullanım hello kaynak kimliği web uygulamanızın hello hedef.

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-hello-traffic-manager-endpoint-url"></a>Merhaba trafik Yöneticisi uç nokta URL'sini alma
Traffic Manager profilinizin şimdi bu noktaları tooyour var olan web uygulamasının bir uç nokta vardır. Kullanım [az ağ trafik Yöneticisi profili Göster](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget URL'sini. 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

Merhaba çıkış tarayıcınıza kopyalayın. Web uygulamanızı yeniden görmeniz gerekir.

### <a name="create-an-azure-redis-cache-in-asia"></a>Bir Azure Redis önbelleği Asya'da oluşturma
Şimdi, Azure web uygulaması toohello Güneydoğu Asya bölgenizi çoğaltılır. toostart, kullanım [az redis oluşturma](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate bir ikinci Azure Redis Önbelleği'nde Güneydoğu Asya. Bu önbellek Asya'da uygulamanızla birlikte bulunan toobe gerekir.

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

`--name $cacheName-asia`verir hello hello ile Merhaba Batı Avrupa önbelleği, önbellek hello adı `-asia` soneki.

### <a name="create-an-app-service-plan-in-asia"></a>Asya'da bir uygulama hizmeti planı oluştur
Kullanım [az uygulama hizmeti planı oluşturma](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate ikinci bir uygulama hizmeti planı hello Güneydoğu Asya bölgesinde, hello kullanarak aynı S1 katmanı hello Batı Avrupa plan.

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a>Asya'da bir web uygulaması oluşturma
Kullanım [az appservice web oluşturmak](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate ikinci bir web uygulaması.

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

`--name $appName-asia`verir hello hello Batı Avrupa uygulamasının uygulama hello adı ile Merhaba `-asia` soneki.

### <a name="configure-hello-connection-string-for-redis"></a>Redis için Hello bağlantı dizesini yapılandırma
Kullanım [az appservice web yapılandırma appsettings güncelleştirme](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) hello Güneydoğu Asya önbelleği için tooadd toohello web uygulaması hello bağlantı dizesi.

appSettings güncelleştirme--az appservice web yapılandırma ayarları "RedisConnection = $($redis.hostname): $($redis.sslPort), parola = $($redis.accessKeys.primaryKey) ssl = True, abortConnect = False"--ad $appName-Asya--kaynak-grubu myResourceGroup

### <a name="configure-git-deployment-for-hello-asia-app"></a>Merhaba Asya uygulaması için Git dağıtımı yapılandırın.
Kullanım [az appservice web kaynak denetimi config-yerel-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure yerel Git dağıtımı hello ikinci web uygulaması için.

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

Bu komut, hello şu şekilde görünen bir çıktı sunar:

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

Kullanım hello ikinci Git URL'si tooconfigure yerel deponuza için Uzak döndürdü. Merhaba aşağıdaki komut çıktısı örneğinde önceki hello kullanır.

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a>Örnek uygulamanızı dağıtma
Çalıştırma `git push` toodeploy örnek uygulama toohello ikinci Git uzaktan. 

```bash
git push azure-asia master
```

Parola istendiğinde, ne zaman çalıştırıldığı belirtilen hello parola kullanmak `az appservice web deployment user set`.

### <a name="browse-toohello-asia-app"></a>Toohello Asya uygulama Gözat
Kullanım [az appservice web Gözat](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) uygulamanızı Canlı Azure'da çalışan tooverify.

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-hello-resource-id-of-hello-asia-app"></a>Merhaba kaynak hello Asya uygulama Kimliğini Al
Kullanım [az appservice web Göster](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) web uygulamanızın Güneydoğu Asya tooget hello kaynak kimliği.

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-asia-app"></a>Trafik Yöneticisi uç noktası hello Asya uygulaması ekleyin
Kullanım [az ağ trafik Yöneticisi uç noktası oluşturma](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd ikinci bir uç nokta toohello trafik Yöneticisi profili.

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-tooweb-apps"></a>Bölge tanımlayıcısı tooweb uygulamalar ekleme
Kullanım [az appservice web yapılandırma appsettings güncelleştirme](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd bölgeye özgü ortam değişkeni.

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

Uygulama kodunuz, bu uygulama ayarı zaten kullanıyor. Bir göz atalım `HighScaleApp\Views\Home\Index.cshtml`.

### <a name="complete"></a>Tamamlandı!

Şimdi, farklı coğrafi bölgelerde tarayıcılardan Traffic Manager profilinizin tooaccess hello URL'yi deneyin. Avrupa istemci tarayıcılarından "ASP.NET Batı Avrupa" göstermesi gerekir ve Asya istemci tarayıcısından "ASP.NET Güneydoğu Asya" göstermesi gerekir

## <a name="more-resources"></a>Diğer kaynaklar
