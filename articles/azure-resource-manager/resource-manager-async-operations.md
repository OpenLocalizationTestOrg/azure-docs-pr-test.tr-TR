---
title: "zaman uyumsuz işlemleri aaaAzure | Microsoft Docs"
description: "Açıklar nasıl azure'da tootrack zaman uyumsuz işlemleri."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: b81254196013adf87998eff11a50993efa52d40d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="track-asynchronous-azure-operations"></a>Zaman uyumsuz Azure işlemleri izleme
Bazı Azure REST işlemlerini zaman uyumsuz olarak çalışır, çünkü Hello işlem hızlı bir şekilde tamamlanamıyor. Bu konuda nasıl tootrack hello değerleri arasında zaman uyumsuz işlemleri durumunu hello yanıtında açıklanmaktadır.  

## <a name="status-codes-for-asynchronous-operations"></a>Zaman uyumsuz işlemleri için durum kodları
Zaman uyumsuz bir işlem, başlangıçta bir HTTP durum kodu ya da döndürür:

* 201 (oluşturuldu)
* 202 (kabul edilen) 

Merhaba işlemi başarıyla tamamlandığında, ya da döndürür:

* 200 (TAMAM)
* 204 (içerik yok) 

Toohello başvuran [REST API belgeleri](/rest/api/) toosee hello yanıtlar yürütme hello işlemi için. 

## <a name="monitor-status-of-operation"></a>İşlemin durumunu izleyin
toodetermine hello durumunu kullandığınız hello zaman uyumsuz REST işlemlerini dönüş üstbilgi değerleri, işlem hello. Büyük olasılıkla üç üstbilgi değerleri tooexamine vardır:

* `Azure-AsyncOperation`-Hello hello işlemi devam eden durumunu denetlemek için URL. Her zaman işleminizi bu değer döndürürse, BT (konum) yerine tootrack hello hello işlemin durumunu kullanın.
* `Location`-Ne zaman bir işlemin tamamlanmasını belirlemek için URL. Yalnızca Azure AsyncOperation alınmadı olduğunda bu değeri kullanın.
* `Retry-After`-hello saniye toowait sayısı hello hello zaman uyumsuz işlemin durumunu denetlemeden önce.

Bununla birlikte, her zaman uyumsuz işlemi bu tüm değerleri döndürür. Örneğin, bir işlemi ve başka bir işlem için hello konum üstbilgisi değeri tooevaluate hello Azure AsyncOperation üstbilgi değeri gerekebilir. 

Bir istek için herhangi bir üstbilgi değerini almak gibi hello üstbilgi değerlerini alır. Örneğin, C# ' ta hello üstbilgi değeri aldığınız bir `HttpWebResponse` adlı nesne `response` koddan hello ile:

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a>Azure AsyncOperation istek ve yanıt

tooget hello hello zaman uyumsuz işlem durumunu Azure AsyncOperation Üstbilgi değerinde bir GET isteği toohello URL gönderin.

Bu işlem hello yanıttan Hello gövdesini hello işlemiyle ilgili bilgi içerir. Merhaba aşağıdaki örnekte hello işleminden döndürülen hello olası değerler gösterilmektedir:

```json
{
    "id": "{resource path from GET operation}",
    "name": "{operation-id}", 
    "status" : "Succeeded | Failed | Canceled | {resource provider values}", 
    "startTime": "2017-01-06T20:56:36.002812+00:00",
    "endTime": "2017-01-06T20:56:56.002812+00:00",
    "percentComplete": {double between 0 and 100 },
    "properties": {
        /* Specific resource provider values for successful operations */
    },
    "error" : { 
        "code": "{error code}",  
        "message": "{error description}" 
    }
}
```

Yalnızca `status` tüm yanıtlar için döndürülür. Merhaba durumu başarısız veya iptal edildi olduğunda hello hata nesnesi döndürülür. Diğer tüm değerler isteğe bağlıdır; Bu nedenle, aldığınız hello yanıt hello örnek farklı görünebilir.

## <a name="provisioningstate-values"></a>provisioningState değerleri

Bir kaynak oluşturma, güncelleştirme veya silme (PUT, PATCH, Sil) işlemleri genellikle dönmek bir `provisioningState` değeri. Bir işlem tamamlandığında, aşağıdaki üç değerden birini verilir: 

* Başarılı oldu
* Başarısız oldu
* İptal edildi

Diğer tüm değerler hello işlemi hala çalışıyor gösterir. Merhaba kaynak sağlayıcısı durumunu gösteren özelleştirilmiş bir değeri geri dönebilirsiniz. Örneğin, alabileceğiniz **kabul edilen** alınan ve çalışan hello istek olduğunda.

## <a name="example-requests-and-responses"></a>Örnek istekleri ve yanıtları

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a>Sanal makine (Azure AsyncOperation ile 202) Başlat
Bu örnek nasıl toodetermine hello durumunu gösterir **Başlat** sanal makineler için işlem. Hello ilk istek hello biçimi aşağıdaki gibidir:

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

Durum kodu 202 döndürür. Merhaba üstbilgi değerleri arasında görürsünüz:

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

başka bir istek toothat URL'si gönderme hello zaman uyumsuz işlem toocheck hello durumu.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

Merhaba yanıt gövdesi hello işlemi hello durumunu içerir:

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a>Kaynakları (201 Azure AsyncOperation ile) dağıtma

Bu örnek nasıl toodetermine hello durumunu gösterir **dağıtımları** kaynakları tooAzure dağıtma işlemi. Hello ilk istek hello biçimi aşağıdaki gibidir:

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

201 durum kodunu döndürür. Merhaba hello yanıtın gövdesini içerir:

```json
"provisioningState":"Accepted",
```

Merhaba üstbilgi değerleri arasında görürsünüz:

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

başka bir istek toothat URL'si gönderme hello zaman uyumsuz işlem toocheck hello durumu.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

Merhaba yanıt gövdesi hello işlemi hello durumunu içerir:

```json
{"status":"Running"}
```

Merhaba dağıtım tamamlandığında, hello yanıtı içerir:

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a>Depolama hesabı (202 konumla ve yeniden deneme sonrasında) oluşturma

Bu örnek nasıl toodetermine hello hello durumunu gösterir **oluşturma** işlem depolama hesapları için. Hello ilk istek hello biçimi aşağıdaki gibidir:

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

Ve hello istek gövdesi hello depolama hesabı için özellikleri içerir:

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

Durum kodu 202 döndürür. Merhaba üstbilgi değerleri arasında iki değer aşağıdaki hello bakın:

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

Sayısı için bekleyen sonra saniye belirtilen yeniden deneme-sonrası, başka bir istek toothat URL'si göndererek hello hello zaman uyumsuz işlemin durumunu denetleyin.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

Merhaba isteği hala devam ediyorsa, bir durum kodu 202 alırsınız. Merhaba isteği tamamlanmışsa, durum kodu 200'ü alırsınız ve hello hello yanıtın gövdesini hello oluşturuldu hello depolama hesabının özelliklerini içerir.

## <a name="next-steps"></a>Sonraki adımlar

* Her REST işlemini ilgili belgeler için bkz: [REST API belgeleri](/rest/api/).
* Merhaba Resource Manager REST API'si aracılığıyla kaynaklarını yönetme hakkında daha fazla bilgi için bkz: [kullanma hello Resource Manager REST API'si](resource-manager-rest-api.md).
* Şablonları hello Resource Manager REST API'si aracılığıyla dağıtma hakkında daha fazla bilgi için bkz: [Resource Manager şablonları ve Resource Manager REST API kaynaklarla dağıtmak](resource-group-template-deploy-rest.md).
