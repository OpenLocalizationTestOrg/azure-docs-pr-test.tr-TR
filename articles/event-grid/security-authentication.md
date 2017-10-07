---
title: "aaaAzure olay kılavuz güvenlik ve kimlik doğrulama"
description: "Azure olay kılavuz ve onun kavramlarını açıklar."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/14/2017
ms.author: babanisa
ms.openlocfilehash: 74f692c7e3a30856c3a80cbbfe82a26bf4c1c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-security-and-authentication"></a>Olay kılavuz güvenlik ve kimlik doğrulama 

Azure olay kılavuz üç tür kimlik doğrulama vardır:

* Olay abonelikleri
* Olay yayımlama
* Web kancası olay teslimi

## <a name="webhook-event-delivery"></a>Web kancası olay teslimi

Web kancası Azure olay kılavuz gelen gerçek zamanlı birçok yolu tooreceive olayları biridir.

Olduğundan her zaman teslim yeni bir olay hazır toobe, olay kılavuz hello gövdesinde tooyour Web kancası hello olay ile birlikte bir HTTP isteği gönderir.

Olay kılavuzla kendi Web kancası uç noktasını kaydetme zaman, basit bir doğrulama kodu içeren bir POST isteği sipariş tooprove uç nokta sahipliği gönderir. Uygulamanızın arka hello doğrulama kodu Yankı tarafından toorespond gerekir. Olay kılavuz olayları hello doğrulama geçmedi tooWebHook uç noktaları teslim değil.
 
### <a name="validation-details"></a>Doğrulama ayrıntıları:

* Olay aboneliği oluşturma/güncelleştirme Hello sırasında bir "SubscriptionValidationEvent" olay toohello hedef uç noktası olay kılavuz gönderir.
* bir üstbilgi değeri "Olay türü: doğrulama" Merhaba olayı içerir.
* Merhaba olay gövdesi olan hello diğer olay kılavuz olaylarla aynı şema.
* Merhaba olay verilerini bir "ValidationCode" özelliği rastgele oluşturulmuş bir dizeyle örneğin içerir "ValidationCode: acb13...".

Sipariş tooprove uç nokta sahipliği geri hello doğrulama kodu örneğin echo "ValidationResponse: acb13...".

Son olarak, Azure olay kılavuz yalnızca HTTPS Web kancası uç noktaları desteklediğini önemli toonote olur.
## <a name="event-subscription"></a>Olay aboneliği

toosubscribe tooan olay hello olmalıdır **Microsoft.EventGrid/EventSubscriptions/Write** hello izni gerekli kaynak. Merhaba kapsamda yeni bir abonelik hello kaynağının yazma için bu izni gerekiyor. Merhaba, kaynak tooa sistem konu veya özel konuyu abone göre farklı gereklidir. Her iki tür, bu bölümde açıklanmıştır.

### <a name="system-topics-azure-service-publishers"></a>Sistem konuları (Azure hizmeti yayımcılar)

Sistem konuları için izni toowrite hello kapsam hello kaynak yayımlama hello olayının yeni bir olay abonelik gerekir. Merhaba kaynağının Hello biçimdedir:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`

Örneğin, toosubscribe tooan olay adlı bir depolama hesabında **myacct**, üzerinde hello Microsoft.EventGrid/EventSubscriptions/Write izniniz olmalıdır:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`

### <a name="custom-topics"></a>Özel konular

Özel konular için izni toowrite hello kapsam hello olay kılavuz konusunun yeni bir olay abonelik gerekir. Merhaba kaynağının Hello biçimdedir:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`

Adlı Örneğin, toosubscribe tooa özel konu **mytopic**, üzerinde hello Microsoft.EventGrid/EventSubscriptions/Write izniniz olmalıdır:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`

## <a name="topic-publishing"></a>Konu yayımlama

Konular, paylaşılan erişim imzası (SAS) veya anahtar kimlik doğrulaması kullanın. SAS öneririz, ancak anahtar kimlik doğrulaması basit programlama sağlar ve birçok varolan Web kancası yayımcıları ile uyumludur. 

Merhaba HTTP üstbilgisinde hello kimlik doğrulama değeri içerir. SA'ları için kullanmak **aeg sas belirteci** hello üstbilgi değeri. Anahtar kimlik doğrulaması için kullanmak **aeg sas anahtarı** hello üstbilgi değeri.

### <a name="key-authentication"></a>Anahtar kimlik doğrulaması

Anahtar kimlik doğrulaması hello Basit kimlik doğrulama biçimidir. Merhaba biçimi kullanın:`aeg-sas-key: <your key>`

Örneğin, bir anahtar ile geçirin: 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a>SAS belirteçleri

Olay kılavuz için SAS belirteci hello kaynak, bir sona erme zamanı ve imza içerir. Merhaba hello SAS belirteci biçimi şöyledir: `r={resource}&e={expiration}&s={signature}`.

Merhaba kaynak hello yoludur hello konu toowhich için olayları gönderiyor. Örneğin, geçerli bir kaynak yolu şöyledir:`https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`

Merhaba imza bir anahtarı oluşturur.

Örneğin, geçerli **aeg sas belirteci** değer:

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

Aşağıdaki örneğine hello olay kılavuz ile kullanmak için bir SAS belirteci oluşturur:

```cs
static string BuildSharedAccessSignature(string resource, DateTime expirationUtc, string key)
{
    const char Resource = 'r';
    const char Expiration = 'e';
    const char Signature = 's';

    string encodedResource = HttpUtility.UrlEncode(resource);
    string encodedExpirationUtc = HttpUtility.UrlEncode(expirationUtc.ToString());

    string unsignedSas = $"{Resource}={encodedResource}&{Expiration}={encodedExpirationUtc}";
    using (var hmac = new HMACSHA256(Convert.FromBase64String(key)))
    {
        string signature = Convert.ToBase64String(hmac.ComputeHash(Encoding.UTF8.GetBytes(unsignedSas)));
        string encodedSignature = HttpUtility.UrlEncode(signature);
        string signedSas = $"{unsignedSas}&{Signature}={encodedSignature}";

        return signedSas;
    }
}
```

## <a name="management-access-control"></a>Yönetim erişim denetimi

Azure olay kılavuz, toocontrol hello düzeyini verilen erişim toodifferent kullanıcılar toodo listesi olay abonelikleri gibi çeşitli yönetim işlemlerini sağlar. Yeni kampanya oluşturmak ve anahtarları oluştur. Bu olay kılavuz Azure'nın rol tabanlı erişim denetleyin (RBAC) kullanır.

### <a name="operation-types"></a>İşlem türleri

Azure olay kılavuz hello aşağıdaki eylemleri destekler:

* Microsoft.EventGrid/*/read 
* Microsoft.EventGrid/*/write 
* Microsoft.EventGrid/*/delete 
* Microsoft.EventGrid/eventSubscriptions/getFullUrl/action 
* Microsoft.EventGrid/topics/listKeys/action 
* Microsoft.EventGrid/topics/regenerateKey/action

normal okuma işlemleri dışında filtrelenmiş son üç işlemleri dönüş olası gizli bilgi hello. Bu, toorestrict erişim toothese işlemleri için en iyi uygulamadır. Özel roller kullanılarak oluşturulabilir [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure komut satırı arabirimi (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md)ve hello [REST API](../active-directory/role-based-access-control-manage-access-rest.md).

### <a name="enforcing-role-based-access-check-rbac"></a>Rol uygulamaya dayalı erişim denetimi (RBAC)

Farklı kullanıcılar için adımları tooenforce RBAC aşağıdaki hello kullan:

#### <a name="create-a-custom-role-definition-file-json"></a>Bir özel rol tanımı dosyası (.json) oluşturun

Merhaba, hangi kullanıcıların tooperform farklı eylemler kümesi örnek olay kılavuz rol tanımları verilmiştir.

**EventGridReadOnlyRole.json**: yalnızca okuma yalnızca işlemlerine izin verilir.
```json
{ 
  "Name": "Event grid read only role", 
  "Id": "7C0B6B59-A278-4B62-BA19-411B70753856", 
  "IsCustom": true, 
  "Description": "Event grid read only role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/read" 
  ], 
  "NotActions": [ 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription Id>" 
  ] 
}
```

**EventGridNoDeleteListKeysRole.json**: kısıtlı sonrası eylemler ancak silme işlemlerinin izin vermeyecek izin.
```json
{ 
  "Name": "Event grid No Delete Listkeys role", 
  "Id": "B9170838-5F9D-4103-A1DE-60496F7C9174", 
  "IsCustom": true, 
  "Description": "Event grid No Delete Listkeys role", 
  "Actions": [     
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action" 
  ], 
  "NotActions": [ 
    "Microsoft.EventGrid/*/delete" 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription id>" 
  ] 
}
```
 
**EventGridContributorRole.json**: tüm olay kılavuz eylemleri sağlar.  
```json
{ 
  "Name": "Event grid contributor role", 
  "Id": "4BA6FB33-2955-491B-A74F-53C9126C9514", 
  "IsCustom": true, 
  "Description": "Event grid contributor role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/*/delete", 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
  ], 
  "NotActions": [], 
  "AssignableScopes": [ 
    "/subscriptions/d48566a8-2428-4a6c-8347-9675d09fb851" 
  ] 
} 
```

#### <a name="install-and-login-tooazure-cli"></a>Yükleme ve oturum açma tooAzure CLI

* Azure CLI Sürüm 0.8.8 veya sonraki bir sürümü. tooinstall hello en son sürümünü ve ilişkilendirme Azure aboneliğinizle görmek [hello Azure CLI yükleyip](../cli-install-nodejs.md).
* Azure Resource Manager'da Azure CLI. Çok Git[hello Resource Manager ile Azure CLI kullanarak hello](../xplat-cli-azure-resource-manager.md) daha fazla ayrıntı için.

#### <a name="create-a-custom-role"></a>Özel bir rol oluşturun

toocreate özel bir rol kullanın:

    azure role create --inputfile <file path>

#### <a name="assign-hello-role-tooa-user"></a>Merhaba rol tooa kullanıcı atama


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a>Sonraki adımlar

* Bir giriş tooEvent kılavuz için bkz: [olay kılavuz hakkında](overview.md)
