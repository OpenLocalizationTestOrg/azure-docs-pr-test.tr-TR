---
title: "aaaAdd özel etki alanı ve SSL tooan Azure web uygulaması | Microsoft Docs"
description: "Nasıl tooprepare Azure web uygulaması toogo üretim şirket markası ekleyerek öğrenin. Merhaba özel etki alanı adı (gösterim etki alanında) tooyour web uygulaması harita ve özel bir SSL sertifikası ile güvenli."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 03/29/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2679ed8b2dbbeba0b128c1a3ec01148f97c35342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-domain-and-ssl-tooan-azure-web-app"></a>Özel etki alanı ve SSL tooan Azure web uygulaması ekleyin

Bu öğretici nasıl tooquickly bir özel etki alanı adı tooyour Azure web uygulaması harita ve özel bir SSL sertifikası ile güvenli gösterir. 

## <a name="before-you-begin"></a>Başlamadan önce

Bu örneği çalıştırmadan önce hello yükleyin [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) yerel olarak.

Ayrıca yönetim erişimi toohello DNS yapılandırma sayfasında ilgili etki sağlayıcınız için gerekir. Örneğin, tooadd `www.contoso.com`, toobe mümkün tooconfigure DNS girişleri için gereksinim duyduğunuz `contoso.com`.

Son olarak, geçerli bir gerekir. PFX dosyası _ve_ tooupload istediğiniz hello SSL sertifikasının parolası ve bağlayın. Bu SSL sertifikasını istediğiniz yapılandırılmış toosecure hello özel etki alanı adı olmalıdır. Örnek yukarıda Hello SSL sertifikanızı güvenli `www.contoso.com`. 

## <a name="step-1---create-an-azure-web-app"></a>1. adım - Azure web uygulaması oluşturma

### <a name="log-in-tooazure"></a>İçinde tooAzure oturum

Bir terminal penceresi toocreate hello kaynakları giderek toouse hello Azure CLI 2.0 toohost Node.js uygulamamıza Azure gerekli artık duyuyoruz.  Tooyour hello Azure aboneliğiyle oturum [az oturum açma](/cli/azure/#login) komut ve hello ekrandaki yönergeleri izleyin. 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a>Kaynak grubu oluşturma   
Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create). Azure kaynak grubu; web uygulamaları, veritabanları ve depolama hesapları gibi Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır. 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

toosee hangi olası değerler için kullanabilmeniz için `---location`, hello kullan `az appservice list-locations` Azure CLI komutu.

## <a name="create-an-app-service-plan"></a>App Service planı oluşturma

Merhaba ile bir uygulama hizmeti planı oluştur [az uygulama hizmeti planı oluşturma](/cli/azure/appservice/plan#create) komutu. 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Merhaba aşağıdaki örnekte oluşturur adlı bir uygulama hizmeti planı `myAppServicePlan` hello kullanarak **temel** fiyatlandırma katmanı.

az uygulama hizmeti planı oluşturma--ad myAppServicePlan--kaynak-grubu myResourceGroup--sku B1

Uygulama hizmeti planı Hello oluşturduğunuzda hello Azure CLI örnek aşağıdaki bilgileri benzer toohello gösterir. 

```json 
{ 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "kind": "app", 
    "location": "West Europe", 
    "sku": { 
    "capacity": 1, 
    "family": "B", 
    "name": "B1", 
    "tier": "Basic" 
    }, 
    "status": "Ready", 
    "type": "Microsoft.Web/serverfarms" 
} 
``` 

## <a name="create-a-web-app"></a>Web uygulaması oluşturma

Bir uygulama hizmeti planı oluşturuldu, hello içinde bir web uygulaması oluşturma `myAppServicePlan` uygulama hizmeti planı. dağıtılan uygulama, bir barındırma alanı toodeploy kodunuzu olduğunuz yanı sıra tooview hello sizin için bir URL sağlar hello web uygulamasını sağlar. Kullanım hello [az appservice web oluşturmak](/cli/azure/appservice/web#create) komutu toocreate hello web uygulaması. 

Merhaba aşağıdaki komutu, lütfen hello gördüğünüz kendi benzersiz uygulama adı yerine `<app_name>` yer tutucu. Merhaba adının toobe benzersiz azure'da tüm uygulamalarında gerekir böylece bu benzersiz bir ad hello varsayılan etki alanı adı hello web uygulaması için hello parçası olarak kullanılır. Hiçbir özel DNS girişi toohello web uygulama daha sonra tooyour kullanıcılar kullanıma önce eşleyebilirsiniz. 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

Merhaba web uygulaması oluşturduğunuzda aşağıdaki örneğine bilgi benzer toohello hello Azure CLI gösterir. 

```json 
{ 
    "clientAffinityEnabled": true, 
    "defaultHostName": "<app_name>.azurewebsites.net", 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/<app_name>", 
    "isDefaultContainer": null, 
    "kind": "app", 
    "location": "West Europe", 
    "name": "<app_name>", 
    "repositorySiteName": "<app_name>", 
    "reserved": true, 
    "resourceGroup": "myResourceGroup", 
    "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "state": "Running", 
    "type": "Microsoft.Web/sites", 
} 
```

Merhaba JSON çıktısını gelen `defaultHostName` web uygulamanızın varsayılan etki alanı adını gösterir. Tarayıcınızda, toothis adresine gidin.

```
http://<app_name>.azurewebsites.net 
``` 
 
![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a>2. adım - DNS eşlemesini yapılandırma

Bu adımda, bir özel etki alanı tooyour web uygulamanızın varsayılan etki alanı adından bir eşleme Ekle `<app_name>.azurewebsites.net`. Genellikle, etki alanı sağlayıcınızın Web sitesinin bu adımı gerçekleştirin. Sağlayıcınızın belgelerine bakmanız gerekir böylece her etki alanı kayıt şirketinizin Web sitesi biraz farklıdır. Ancak, bazı genel yönergeler şunlardır. 

### <a name="navigate-tootoodns-management-page"></a>TootooDNS yönetimi sayfasına gidin

İlk olarak, tooyour etki alanı kayıt şirketinizin Web sitesinde oturum açın.  

Ardından, DNS kayıtlarını yönetme için hello sayfasını bulun. Bağlantılar veya etiketli hello sitesinin alanları arayın **etki alanı adı**, **DNS**, veya **adı sunucu yönetimi**. Genellikle, hesap bilgilerinizi görüntülemek ve bir bağlantı gibi arayan hello bağlantı bulabilirsiniz **My etki alanları**.

Bu sayfayı bulduktan sonra Ekle veya DNS kayıtlarını düzenlemenize olanak sağlayan bir bağlantı için bakın. Bu olabilir bir **bölge dosyası** veya **DNS kayıtlarını** bağlantı veya bir **Gelişmiş Yapılandırma** bağlantı.

### <a name="create-a-cname-record"></a>Bir CNAME kaydı oluşturun

Hello istenen alt etki alanı adı tooyour web uygulamanızın varsayılan etki alanı adı eşleyen bir CNAME kaydı ekleyin (`<app_name>.azurewebsites.net`, burada `<app_name>` , uygulamanızın benzersiz adıdır).

Hello için `www.contoso.com` örnek, hello eşleyen bir CNAME oluşturun `www` ana bilgisayar adı çok`<app_name>.azurewebsites.net`.

## <a name="step-3---configure-hello-custom-domain-on-your-web-app"></a>3. adım - web uygulamanız hello özel etki alanı yapılandırma

Etki alanı sağlayıcınızın Web sitesinin hello hostname eşleme yapılandırmayı bitirdiğinizde, web uygulamanız hazır tooconfigure hello özel etki alanı demektir. Kullanım hello [az appservice web yapılandırma hostname eklemek](/cli/azure/appservice/web/config/hostname#add) tooadd bu yapılandırma komutu. 

Merhaba aşağıdaki komutu, lütfen yerine `<app_name>` benzersiz uygulama adı ve < your_custom_domain > merhaba tam özel etki alanı adı ile (örneğin `www.contoso.com`). 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

Merhaba özel etki alanı artık tam olarak eşlenmiş tooyour web uygulamasıdır. Tarayıcınızda, toohello özel etki alanı adı gidin. Örneğin:

```
http://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-tooyour-web-app"></a>4. adım - BIND özel bir SSL sertifikası tooyour web uygulaması

Şimdi bir Azure web uygulaması hello tarayıcının adres çubuğunda istediğiniz hello etki alanı adı ile sahipsiniz. Ancak, toohello giderseniz `https://<your_custom_domain>` şimdi, bir sertifika hatası alın. 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

Web uygulamanızı henüz özel etki alanı adıyla eşleşen bir SSL sertifikası bağlaması sahip olmadığından bu hata oluşur. Ancak, çok giderseniz, bir hata iletisi yok`https://<app_name>.azurewebsites.net`. Tüm Azure App Service uygulamalarının yanı sıra, uygulamanızı güvenliğinin hello için hello SSL sertifikası ile bunun nedeni `*.azurewebsites.net` joker karakter etki alanı varsayılan olarak. 

Tooaccess web uygulamanızı özel etki alanı adınızı sipariş, özel etki alanı toohello web uygulamanız için toobind hello SSL sertifikası gerekir. Bu adımda yapar. 

### <a name="upload-hello-ssl-certificate"></a>Merhaba SSL sertifikasını karşıya yükle

Özel etki alanı tooyour web uygulamanız için SSL sertifikası Hello hello kullanarak karşıya [az appservice web yapılandırma ssl karşıya yükleme](/cli/azure/appservice/web/config/ssl#upload) komutu.

Merhaba aşağıdaki komutu, lütfen yerine `<app_name>` benzersiz uygulama adınız ile `<path_to_ptx_file>` hello yolu tooyour ile. PFX dosyası ve `<password>` sertifikanızın parolayla. 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

Merhaba sertifika karşıya yüklendiğinde, hello Azure CLI aşağıdaki örneğine benzer toohello bilgileri gösterir:

```json
{
  "cerBlob": null,
  "expirationDate": "2018-03-29T14:12:57+00:00",
  "friendlyName": "",
  "hostNames": [
    "www.contoso.com"
  ],
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/cert
ificates/9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "issueDate": "2017-03-29T14:12:57+00:00",
  "issuer": "www.contoso.com",
  "keyVaultId": null,
  "keyVaultSecretName": null,
  "keyVaultSecretStatus": "Initialized",
  "kind": null,
  "location": "West Europe",
  "name": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "password": null,
 "pfxBlob": null,
  "publicKeyHash": null,
  "resourceGroup": "myResourceGroup",
  "selfLink": null,
  "serverFarmId": null,
  "siteName": null,
  "subjectName": "www.contoso.com",
  "tags": null,
  "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00",
  "type": "Microsoft.Web/certificates",
  "valid": null
}
```

Merhaba JSON çıktısını gelen `thumbprint` karşıya yüklenen sertifikanızın parmak izi gösterir. Merhaba sonraki adımınız değerini kopyalayın.

### <a name="bind-hello-uploaded-ssl-certificate-toohello-web-app"></a>Bağlama hello SSL sertifika toohello web uygulaması karşıya yüklenmedi

Web uygulamanız şimdi istediğiniz hello özel etki alanı adı içeriyor ve bu özel etki alanı güvenliğini sağlar bir SSL sertifikası da sahiptir. Merhaba yalnızca şey sol toodo toobind hello yüklenen sertifikanın toohello web uygulamasıdır. Hello kullanarak bunu [az appservice web yapılandırma ssl bağı](/cli/azure/appservice/web/config/ssl#bind) komutu.

Merhaba aşağıdaki komutu, lütfen yerine `<app_name>` benzersiz uygulama adıyla ve `<thumbprint-from-previous-output>` hello önceki komuttan alma hello sertifika parmak izine sahip. 

az appservice web yapılandırma ssl bağı--ad < app_name >--kaynak-grubu myResourceGroup--sertifika parmak izi < parmak izi-gelen-önceki-output >--ssl türü SNI

Merhaba sertifika ilişkili tooyour web uygulaması olduğunda hello Azure CLI örnek aşağıdaki bilgileri benzer toohello gösterir:

{"availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containersize değeri yok olarak": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "< app_name >. azurewebsites.net", "enabled": true, " enabledHostNames": ["www.contoso.com"," < app_name >. azurewebsites.net "," < app_name >. scm.azurewebsites.net "],"gatewaySiteName": null,"hostNameSslStates": [{"ana":"Standart","name":" < app_name >. azurewebsites.net ","sslState":"Devre dışı","parmak izi": null,"toUpdate": null,"Virtualıp": null}, {"ana":"Repository","ad":" < app_name >. scm.azurewebsites.net ","sslState":"Devre dışı","parmak izi": null,"toUpdate": null,"Virtualıp": null}, {" ana bilgisayar türü":"Standart","name":"www.contoso.com","sslState":"SniEnabled","parmak izi":"9FD1D2D06E2293673E2A8D1CA484A092BD016D00","toUpdate": null,"Virtualıp": null}],"ana bilgisayar adları": ["www.contoso.com","< app_name >. azurewebsites.NET"],"hostNamesDisabled": false,"hostingEnvironmentProfile": null,"id":" /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s / < app_name > "," isDefaultContainer": null,"tür":"WebApp","lastModifiedTimeUtc":" 2017-03-29T14:36:18.803333 ","Konum":"Batı Avrupa","maxNumberOfWorkers": null,"mikro":"false","adı":"< app_name >","outboundIpAddresses":" 13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1 ","premiumAppDeployed": null,"repositorySiteName":"< app_name >","ayrılmış": false,"kaynak grubu":"contoso.com","scmSiteAlsoStopped": false,"Serverfarmıd": "/ abonelikleri/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/sağlayıcıları/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "Durum": "Çalışır", "suspendedTill": null, "etiketler": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "tür": "Microsoft.Web/sites", "usageState": "Normal"}

Tarayıcınızda, özel etki alanı adınızı tooHTTPS uç noktasını gidin. Örneğin:

```
https://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a>Diğer kaynaklar

[Satın alma ve Azure App Service'te özel etki alanı adı yapılandırma](custom-dns-web-site-buydomains-web-app.md)
[satın alın ve Azure uygulama hizmetiniz için bir SSL sertifikası yapılandırma](web-sites-purchase-ssl-web-site.md)
