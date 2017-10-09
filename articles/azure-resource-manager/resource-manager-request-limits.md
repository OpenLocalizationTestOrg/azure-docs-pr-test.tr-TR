---
title: "aaaAzure Resource Manager istek sınırlarını | Microsoft Docs"
description: "Abonelik sınırları erişildiğinde Azure Resource Manager ile azaltma toouse nasıl istekleri açıklar."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: e1047233-b8e4-4232-8919-3268d93a3824
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: ea274f3145af36aac753730e1f280d8a8b59c3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-resource-manager-requests"></a>Resource Manager istekleri azaltma
Her abonelik ve Kiracı, Resource Manager sınırları istekleri too15, saat başına 000 okuma ve istekleri too1, saat başına 200 yazma. Bu sınırlar tooeach Azure Resource Manager örneğinin geçerli; Her Azure bölgesi birden çok örneği vardır ve Azure Resource Manager olduğu dağıtılan tooall Azure bölgeleri.  Sınırları pratikte, yukarıda listelenen daha etkili bir şekilde çok daha yüksek olacak şekilde bir kullanıcı olarak istekleri genellikle birçok farklı örnekleri tarafından sunulur.

Uygulama veya betik bu sınırları ulaşırsa, isteklerinizi toothrottle gerekir. Bu konuda sahip hello sınırı ulaşmadan önce kalan toodetermine hello istekleri nasıl ve ne gösterilmektedir hello sınıra ulaştığınızda toorespond.

Merhaba sınırına ulaştığında, hello HTTP durum kodu alırsınız **429 çok fazla istek**.

Merhaba istek sayısı aboneliğinizi veya Kiracı kapsamlı tooeither değil. Eş zamanlı uygulamaları, aboneliğinizde istekleri yapan birden çok varsa, bu uygulamalardan hello istekler toodetermine hello kalan istek sayısı birlikte eklenir.

Kapsamlı abonelik olanları hello içeren hello kaynak grupları, aboneliğinizdeki alma gibi abonelik kimliğinizi geçirme isteklerdir. Kapsamlı Kiracı isteklerini alma geçerli Azure konumları gibi abonelik kimliğinizi dahil etmeyin.

## <a name="remaining-requests"></a>Kalan istekleri
Yanıt Üstbilgileri inceleyerek kalan istekleri hello sayısını belirleyebilirsiniz. Her istek hello numarasının kalan okuma ve yazma isteklerini değerlerini içerir. Merhaba aşağıdaki tabloda bu değerleri inceleyebilirsiniz hello yanıt üstbilgilerini açıklanmaktadır:

| Yanıt üst bilgisi | Açıklama |
| --- | --- |
| x-MS-ratelimit-Remaining-Subscription-Reads |Kalan abonelik kapsamlı okur |
| x-MS-ratelimit-Remaining-Subscription-Writes |Kalan abonelik kapsamlı Yazar |
| x-MS-ratelimit-Remaining-tenant-Reads |Kalan kapsamlı kiracı okur |
| x-MS-ratelimit-Remaining-tenant-Writes |Kalan kapsamlı Kiracı Yazar |
| x-MS-ratelimit-Remaining-Subscription-Resource-Requests |Abonelik, kaynak türü istekleri kalan kapsamlı.<br /><br />Bu üstbilgi değerini yalnızca bir hizmet hello varsayılan sınır kılınmış döndürülür. Resource Manager hello abonelik okuma veya yazmaları yerine bu değer ekler. |
| x-MS-ratelimit-Remaining-Subscription-Resource-entities-Read |Abonelik, kaynak türü koleksiyonu isteklerini kalan kapsamlı.<br /><br />Bu üstbilgi değerini yalnızca bir hizmet hello varsayılan sınır kılınmış döndürülür. Bu değer kalan koleksiyonu isteklerini (liste kaynakları) hello sayısını sağlar. |
| x-MS-ratelimit-Remaining-tenant-Resource-Requests |Kiracı kaynak türü istekleri kalan kapsamlı.<br /><br />Bu üst yalnızca Kiracı düzeyinde istekleri için eklenir ve yalnızca bir hizmet hello varsayılan sınır geçersiz kılınmış. Resource Manager hello Kiracı okuma veya yazmaları yerine bu değer ekler. |
| x-MS-ratelimit-Remaining-tenant-Resource-entities-Read |Kiracı kaynak türü koleksiyonu isteklerini kalan kapsamlı.<br /><br />Bu üst yalnızca Kiracı düzeyinde istekleri için eklenir ve yalnızca bir hizmet hello varsayılan sınır geçersiz kılınmış. |

## <a name="retrieving-hello-header-values"></a>Merhaba üstbilgi değerlerini alma
Kod ya da komut dosyasında bu üstbilgi değerlerini alma herhangi bir üstbilgi değeri almaktan farklı değildir. 

Örneğin, **C#**, hello üstbilgi değeri almak bir **HttpWebResponse** adlı nesne **yanıt** koddan hello ile:

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

İçinde **PowerShell**, bir Invoke-WebRequest işlemden hello üstbilgi değeri alır.

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

Veya, toosee hello kalan istekleri hata ayıklama için hello sağlayabilir istiyorsanız **-Debug** parametresi, **PowerShell** cmdlet'i.

```powershell
Get-AzureRmResourceGroup -Debug
```

Aşağıdaki yanıt değeri hello dahil olmak üzere birden fazla değer döndüren:

```powershell
...
DEBUG: ============================ HTTP RESPONSE ============================

Status Code:
OK

Headers:
Pragma                        : no-cache
x-ms-ratelimit-remaining-subscription-reads: 14999
...
```

İçinde **Azure CLI**, kullanarak hello üstbilgi değeri almak hello daha ayrıntılı seçeneği.

```azurecli
azure group list -vv --json
```

Hangi nesne aşağıdaki hello dahil olmak üzere birçok değerleri döndürür:

```azurecli
...
silly: returnObject
{
  "statusCode": 200,
  "header": {
    "cache-control": "no-cache",
    "pragma": "no-cache",
    "content-type": "application/json; charset=utf-8",
    "expires": "-1",
    "x-ms-ratelimit-remaining-subscription-reads": "14998",
    ...
```

## <a name="waiting-before-sending-next-request"></a>Sonraki istek gönderilmeden önce bekleniyor
Merhaba istek sınırına ulaştığında, Resource Manager hello döndürür **429** HTTP durum kodu ve **yeniden deneme sonrasında** hello üstbilgi değeri. Merhaba **yeniden deneme sonrasında** değeri hello sonraki istek gönderilmeden önce uygulamanız beklemesi gereken saniye (veya uyku) hello sayısını belirtir. Merhaba yeniden deneme değeri geçmeden önce bir isteği gönderirseniz, isteğiniz işlenmedi ve yeni bir yeniden deneme değeri döndürülür.

## <a name="next-steps"></a>Sonraki adımlar

* Sınırları ve kotalar hakkında daha fazla bilgi için bkz: [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md).
* zaman uyumsuz REST istekleri işleme hakkında toolearn bkz [izlemek zaman uyumsuz Azure işlemleri](resource-manager-async-operations.md).
