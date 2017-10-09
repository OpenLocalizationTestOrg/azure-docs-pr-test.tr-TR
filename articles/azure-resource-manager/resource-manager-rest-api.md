---
title: aaaResource Manager REST API'leri | Microsoft Docs
description: "Merhaba Resource Manager REST API'leri kimlik doğrulama ve kullanım örnekleri genel bakış"
services: azure-resource-manager
documentationcenter: na
author: navalev
manager: timlt
editor: 
ms.assetid: e8d7a1d2-1e82-4212-8288-8697341408c5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/13/2017
ms.author: navale;tomfitz;
ms.openlocfilehash: 3ccc3575c5e06c41f2fdc5317711980fc6a2f649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-manager-rest-apis"></a>Resource Manager REST API'leri
> [!div class="op_single_selector"]
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [Azure CLI](xplat-cli-azure-resource-manager.md)
> * [Portal](resource-group-portal.md) 
> * [REST API](resource-manager-rest-api.md)
> 
> 

Kaynak Yöneticisi, dağıtılan her şablon arkasında her çağrı tooAzure arkasında her yapılandırılan depolama hesabı var. bir veya daha fazla çağrıları toohello Azure Kaynak Yöneticisi'nin RESTful API'si Bu konuda hoşlanıyorsanız toothose olan API'ler ve nasıl bunları herhangi SDK kullanmadan çağırabilirsiniz. Bu yaklaşım, istekleri tooAzure üzerinde tam denetim istiyorsanız veya hello SDK tercih ettiğiniz dili için kullanılabilir değilse veya gereksinim duyduğunuz hello işlemlerini desteklemediğinden yararlıdır.

Bu makalede, Azure'da gösterilir, ancak yerine bazı işlemler toothem nasıl bağlanacağını örnekleri kullanan her bir API üzerinden geçmez. Merhaba temel kavramları öğrendikten sonra hello okuyabilirsiniz [Azure Resource Manager REST API Başvurusu](https://docs.microsoft.com/rest/api/resources/) toofind ayrıntılı nasıl toouse hello kalan hello API'ler hakkında daha fazla bilgi.

## <a name="authentication"></a>Kimlik Doğrulaması
Kimlik doğrulama kaynak yöneticisi için Azure Active Directory (AD tarafından) ele alınır. tooconnect tooany API, ilk Azure AD tooreceive tooevery isteğinde geçirebilirsiniz bir kimlik doğrulama belirteci ile tooauthenticate gerekir. Toohello REST API'leri, bir kullanıcı adı ve parola istendiğinde tarafından tooauthenticate istemediğiniz olan varsayıyoruz doğrudan saf çağrı tanımlamakta olduğunuz gibi. İki faktörlü kimlik doğrulama mekanizmaları kullanmıyorsanız varsayıyoruz. Bu nedenle, hangi Azure AD uygulaması ve içinde kullanılan toolog olan bir hizmet asıl adı verilir oluşturun. Ancak Azure AD birden fazla kimlik doğrulama yordamları ve bunların tümünün desteklediğini unutmayın kullanılan tooretrieve sonraki API istekleri için ihtiyacımız bu kimlik doğrulama belirteci olabilir.
İzleyin [oluşturma Azure AD uygulaması ve hizmet sorumlusu](resource-group-create-service-principal-portal.md) adım adım yönergeler için.

### <a name="generating-an-access-token"></a>Bir erişim belirteci oluşturma
Azure AD kimlik doğrulaması login.microsoftonline.com bulunan tooAzure AD, çağıran gerçekleştirilir. tooauthenticate, aşağıdaki bilgilerle toohave hello gerekir:

* Azure AD Kiracı kimliği (Merhaba ad içinde toolog kullanıyorsanız bu Azure ad, şirketinizin aynı ancak gerekli değildir genellikle hello)
* Uygulama Kimliği (hello Azure AD uygulama oluşturma adımında taken)
* (Seçtiğiniz hello Azure AD uygulaması oluşturulurken) parola

HTTP isteği aşağıdaki hello emin tooreplace "Azure AD Kiracı kimliği", "Uygulama kimliği" ve "Parola" Merhaba doğru değerlere sahip olun.

**Genel HTTP isteği:**

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

... (doğrulama başarılı olursa) olacak neden yanıt izleyen bir yanıt benzer toohello içinde:

```json
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1448199959",
  "not_before": "1448196059",
  "resource": "https://management.core.windows.net/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhb...86U3JI_0InPUk_lZqWvKiEWsayA"
}
```
(Merhaba access_token yanıt önceki hello içinde kısaltılmış tooincrease okunabilirlik edilmiştir)

**Erişim belirteci Bash kullanarak oluşturuluyor:**

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

**PowerShell kullanarak erişim belirteci oluşturuluyor:**

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

Merhaba yanıt, bir erişim belirteci, ne kadar bu belirtecin geçerli olduğu hakkında bilgi ve hangi kaynak için bu belirteci kullanabilirsiniz hakkında bilgiler içerir.
Merhaba erişim belirteci hello önceki HTTP çağrısında alınan tüm istek toohello için kaynak yöneticisi API'si geçirilmesi gerekir. "Taşıyıcı YOUR_ACCESS_TOKEN" Merhaba değerle "Yetkilendirme" adlı bir üstbilgi değeri olarak geçirin. "Bearer" ile erişim belirtecinizi arasında Hello boşluk dikkat edin.

HTTP sonuç yukarıda hello görüldüğü gibi hello belirteç bir belirli süre boyunca önbelleğe ve gerekir, aynı belirteci yeniden için geçerli olur. Her API çağrısı için Azure ad olası tooauthenticate olsa bile, yüksek oranda verimsiz olacaktır.

## <a name="calling-resource-manager-rest-apis"></a>Arama Resource Manager REST API'leri
Bu konuda, yalnızca birkaç API'leri tooexplain hello temel kullanımını hello REST işlemlerini kullanır. Tüm hello işlemleri hakkında daha fazla bilgi için bkz: [Azure Resource Manager REST API'leri](https://docs.microsoft.com/rest/api/resources/).

### <a name="list-all-subscriptions"></a>Tüm abonelikleri listeler
Merhaba basit işlemleri yapabileceğiniz erişebileceğiniz toolist hello kullanılabilir abonelikler biridir. İstek aşağıdaki hello nasıl hello erişim belirteci başlık olarak geçirilen bakın:

(YOUR_ACCESS_TOKEN, gerçek erişim belirteci ile değiştirin.)

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

... ve sonuç olarak, bu hizmet sorumlusu tooaccess izin verildiğini Aboneliklerin listesini alın

(Abonelik kimlikleri okunabilirlik için kısaltılmıştır)

```json
{
  "value": [
    {
      "id": "/subscriptions/3a8555...555995",
      "subscriptionId": "3a8555...555995",
      "displayName": "Azure Subscription",
      "state": "Enabled",
      "subscriptionPolicies": {
        "locationPlacementId": "Internal_2014-09-01",
        "quotaId": "Internal_2014-09-01"
      }
    }
  ]
}
```

### <a name="list-all-resource-groups-in-a-specific-subscription"></a>Belirli bir Abonelikteki tüm kaynak gruplarının listesi
Bir kaynak grubu içinde hello Resource Manager API'leri ile tüm kaynaklar yerleştirilir. Resource Manager için mevcut kaynak grupları aboneliğinizi HTTP GET isteği aşağıdaki hello kullanarak sorgulama yapabilirsiniz. Nasıl hello abonelik kimliği hello URL'SİNİN bir parçası bu süre geçirilen dikkat edin.

(YOUR_ACCESS_TOKEN ve ABONELİK_KİMLİĞİ gerçek erişim belirtecini ve abonelik Kimliğinizle değiştirin)

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

Merhaba, get yanıtında tanımlanmış bir kaynak grubu olup olmadığına bağlıdır ve bu durumda, kaç tane.

(Abonelik kimlikleri okunabilirlik için kısaltılmıştır)

```json
{
    "value": [
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/myfirstresourcegroup",
            "name": "myfirstresourcegroup",
            "location": "eastus",
            "properties": {
                "provisioningState": "Succeeded"
            }
        },
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/mysecondresourcegroup",
            "name": "mysecondresourcegroup",
            "location": "northeurope",
            "tags": {
                "tagname1": "My first tag"
            },
            "properties": {
                "provisioningState": "Succeeded"
            }
        }
    ]
}
```

### <a name="create-a-resource-group"></a>Kaynak grubu oluşturma
Şu ana kadar biz yalnızca bilgi için Resource Manager API'leri hello sorgulama. Biz bazı kaynaklar oluşturabilir ve hello bunları tümü, bir kaynak grubu kolay başlayalım zamanı geldi. Merhaba aşağıdaki HTTP isteği bir bölge/konum tercih ettiğiniz bir kaynak grubu oluşturur ve bir etiket tooit ekler.

(YOUR_ACCESS_TOKEN, ABONELİK_KİMLİĞİ, RESOURCE_GROUP_NAME, gerçek erişim belirteci, abonelik kimliği ve hello toocreate istediğiniz kaynak grubunun adını adıyla değiştirin)

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  }
}
```

Başarılı olursa, yanıt aşağıdaki benzer toohello bir yanıt alın:

```json
{
  "id": "/subscriptions/3a8555...555995/resourceGroups/RESOURCE_GROUP_NAME",
  "name": "RESOURCE_GROUP_NAME",
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  },
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

Azure'da bir kaynak grubu başarıyla oluşturdunuz. Tebrikler!

### <a name="deploy-resources-tooa-resource-group-using-a-resource-manager-template"></a>Resource Manager şablonu kullanarak kaynak tooa kaynak grubu dağıtma
Resource Manager ile şablonları kullanarak kaynaklarınızı dağıtabilirsiniz. Bir şablonu bazı kaynaklar ve bağımlılıklarını tanımlar. Bu bölüm için Resource Manager şablonları hakkında bilginiz ve yalnızca nasıl toomake hello API çağrısı toostart dağıtım gösteriyoruz varsayıyoruz. Şablonları oluşturma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).

Dağıtım şablonu, diğer API'leri çağırmak kadar toohow farklı değil. Önemli bir özelliği, bir şablon dağıtımını oldukça uzun zaman alabilir ' dir. Merhaba API çağrısı yalnızca döndürür ve hello dağıtım yapıldığında, tooyou hello dağıtım toofind durumunu Geliştirici tooquery gibidir. Daha fazla bilgi için bkz: [izlemek zaman uyumsuz Azure işlemleri](resource-manager-async-operations.md).

Bu örnekte, kullanılabilir bir genel olarak sunulan şablon kullanırız [GitHub](https://github.com/Azure/azure-quickstart-templates). Merhaba şablon kullandığımız bir Linux VM toohello Batı ABD bölgesi dağıtır. Bu örnek, GitHub gibi ortak bir havuzda kullanılabilir bir şablonu kullanıyor olsa bile, bunun yerine hello tam şablon hello isteğin bir parçası geçiş yapabilir. Merhaba içinde kullanılan parametre değerlerini hello isteğindeki sağladığımız Not şablonu dağıtıldı.

(ABONELİK_KİMLİĞİ, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD ve DNS_NAME_FOR_PUBLIC_IP toovalues isteğiniz uygun değiştirin)

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME/providers/microsoft.resources/deployments/DEPLOYMENT_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "properties": {
    "templateLink": {
      "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json",
      "contentVersion": "1.0.0.0",
    },
    "mode": "Incremental",
    "parameters": {
        "newStorageAccountName": {
          "value": "GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME"
        },
        "adminUsername": {
          "value": "ADMIN_USER_NAME"
        },
        "adminPassword": {
          "value": "ADMIN_PASSWORD"
        },
        "dnsNameForPublicIP": {
          "value": "DNS_NAME_FOR_PUBLIC_IP"
        },
        "ubuntuOSVersion": {
          "value": "15.04"
        }
    }
  }
}
```

Bu istek için uzun JSON yanıt Hello belirtilmemişse tooimprove okunabilirlik bu belgelerin olmuştur. Merhaba yanıt oluşturduğunuz hello şablonlu dağıtımı hakkında bilgi içerir.

## <a name="next-steps"></a>Sonraki adımlar

- zaman uyumsuz REST işlemlerini işleme hakkında toolearn bkz [izlemek zaman uyumsuz Azure işlemleri](resource-manager-async-operations.md).
