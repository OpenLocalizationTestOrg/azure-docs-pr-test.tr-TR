---
title: "Azure zaman uyumsuz işlemleri | Microsoft Docs"
description: "Azure içinde zaman uyumsuz işlemleri izlemek açıklar."
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
ms.openlocfilehash: 9fe3d98cd345aae45722295b6c1b7fc3e9036e95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="track-asynchronous-azure-operations"></a><span data-ttu-id="59563-103">Zaman uyumsuz Azure işlemleri izleme</span><span class="sxs-lookup"><span data-stu-id="59563-103">Track asynchronous Azure operations</span></span>
<span data-ttu-id="59563-104">Bazı Azure REST işlemlerini zaman uyumsuz olarak çalışır, çünkü işlem hızlı bir şekilde tamamlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="59563-104">Some Azure REST operations run asynchronously because the operation cannot be completed quickly.</span></span> <span data-ttu-id="59563-105">Bu konu, yanıtta döndürülen değerleri arasında zaman uyumsuz işlemleri durumunu izlemek açıklar.</span><span class="sxs-lookup"><span data-stu-id="59563-105">This topic describes how to track the status of asynchronous operations through values returned in the response.</span></span>  

## <a name="status-codes-for-asynchronous-operations"></a><span data-ttu-id="59563-106">Zaman uyumsuz işlemleri için durum kodları</span><span class="sxs-lookup"><span data-stu-id="59563-106">Status codes for asynchronous operations</span></span>
<span data-ttu-id="59563-107">Zaman uyumsuz bir işlem, başlangıçta bir HTTP durum kodu ya da döndürür:</span><span class="sxs-lookup"><span data-stu-id="59563-107">An asynchronous operation initially returns an HTTP status code of either:</span></span>

* <span data-ttu-id="59563-108">201 (oluşturuldu)</span><span class="sxs-lookup"><span data-stu-id="59563-108">201 (Created)</span></span>
* <span data-ttu-id="59563-109">202 (kabul edilen)</span><span class="sxs-lookup"><span data-stu-id="59563-109">202 (Accepted)</span></span> 

<span data-ttu-id="59563-110">İşlem başarıyla tamamlandığında, ya da döndürür:</span><span class="sxs-lookup"><span data-stu-id="59563-110">When the operation successfully completes, it returns either:</span></span>

* <span data-ttu-id="59563-111">200 (TAMAM)</span><span class="sxs-lookup"><span data-stu-id="59563-111">200 (OK)</span></span>
* <span data-ttu-id="59563-112">204 (içerik yok)</span><span class="sxs-lookup"><span data-stu-id="59563-112">204 (No Content)</span></span> 

<span data-ttu-id="59563-113">Başvurmak [REST API belgeleri](/rest/api/) yürütme işlemi için yanıtlar görmek için.</span><span class="sxs-lookup"><span data-stu-id="59563-113">Refer to the [REST API documentation](/rest/api/) to see the responses for the operation you are executing.</span></span> 

## <a name="monitor-status-of-operation"></a><span data-ttu-id="59563-114">İşlemin durumunu izleyin</span><span class="sxs-lookup"><span data-stu-id="59563-114">Monitor status of operation</span></span>
<span data-ttu-id="59563-115">Zaman uyumsuz REST işlemlerini işlemin durumunu belirlemek için kullanılan üstbilgi değerleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="59563-115">The asynchronous REST operations return header values, which you use to determine the status of the operation.</span></span> <span data-ttu-id="59563-116">İncelemek için büyük olasılıkla üç üstbilgi değerleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="59563-116">There are potentially three header values to examine:</span></span>

* <span data-ttu-id="59563-117">`Azure-AsyncOperation`-İşlemi devam eden durumunu denetlemek için URL.</span><span class="sxs-lookup"><span data-stu-id="59563-117">`Azure-AsyncOperation` - URL for checking the ongoing status of the operation.</span></span> <span data-ttu-id="59563-118">İşleminizi bu değer döndürürse, her zaman bu (konum yerine) işlemin durumunu izlemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="59563-118">If your operation returns this value, always use it (instead of Location) to track the status of the operation.</span></span>
* <span data-ttu-id="59563-119">`Location`-Ne zaman bir işlemin tamamlanmasını belirlemek için URL.</span><span class="sxs-lookup"><span data-stu-id="59563-119">`Location` - URL for determining when an operation has completed.</span></span> <span data-ttu-id="59563-120">Yalnızca Azure AsyncOperation alınmadı olduğunda bu değeri kullanın.</span><span class="sxs-lookup"><span data-stu-id="59563-120">Use this value only when Azure-AsyncOperation is not returned.</span></span>
* <span data-ttu-id="59563-121">`Retry-After`-Zaman uyumsuz işlemin durumunu denetlemeden önce beklenecek saniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="59563-121">`Retry-After` - The number of seconds to wait before checking the status of the asynchronous operation.</span></span>

<span data-ttu-id="59563-122">Bununla birlikte, her zaman uyumsuz işlemi bu tüm değerleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="59563-122">However, not every asynchronous operation returns all these values.</span></span> <span data-ttu-id="59563-123">Örneğin, bir işlem için Azure AsyncOperation üstbilgisi değeri ve başka bir işlem için konum üstbilgisi değeri değerlendirmek gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="59563-123">For example, you may need to evaluate the Azure-AsyncOperation header value for one operation, and the Location header value for another operation.</span></span> 

<span data-ttu-id="59563-124">Bir istek için herhangi bir üstbilgi değerini almak gibi üstbilgi değerlerini alır.</span><span class="sxs-lookup"><span data-stu-id="59563-124">You retrieve the header values as you would retrieve any header value for a request.</span></span> <span data-ttu-id="59563-125">Örneğin, C# ' ta üstbilgi değeri aldığınız bir `HttpWebResponse` adlı nesne `response` aşağıdaki kod ile:</span><span class="sxs-lookup"><span data-stu-id="59563-125">For example, in C#, you retrieve the header value from an `HttpWebResponse` object named `response` with the following code:</span></span>

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a><span data-ttu-id="59563-126">Azure AsyncOperation istek ve yanıt</span><span class="sxs-lookup"><span data-stu-id="59563-126">Azure-AsyncOperation request and response</span></span>

<span data-ttu-id="59563-127">Zaman uyumsuz işlemin durumunu almak için Azure AsyncOperation üstbilgi değeri URL'SİNDE bir GET isteği gönderin.</span><span class="sxs-lookup"><span data-stu-id="59563-127">To get the status of the asynchronous operation, send a GET request to the URL in Azure-AsyncOperation header value.</span></span>

<span data-ttu-id="59563-128">Bu işlem gelen yanıt gövdesini işlemi hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="59563-128">The body of the response from this operation contains information about the operation.</span></span> <span data-ttu-id="59563-129">Aşağıdaki örnek işleminden döndürülen olası değerleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="59563-129">The following example shows the possible values returned from the operation:</span></span>

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

<span data-ttu-id="59563-130">Yalnızca `status` tüm yanıtlar için döndürülür.</span><span class="sxs-lookup"><span data-stu-id="59563-130">Only `status` is returned for all responses.</span></span> <span data-ttu-id="59563-131">Başarısız veya iptal edildi durum olduğunda hata nesnesi döndürülür.</span><span class="sxs-lookup"><span data-stu-id="59563-131">The error object is returned when the status is Failed or Canceled.</span></span> <span data-ttu-id="59563-132">Diğer tüm değerler isteğe bağlıdır; Bu nedenle, aldığınız yanıt örnek farklı görünebilir.</span><span class="sxs-lookup"><span data-stu-id="59563-132">All other values are optional; therefore, the response you receive may look different than the example.</span></span>

## <a name="provisioningstate-values"></a><span data-ttu-id="59563-133">provisioningState değerleri</span><span class="sxs-lookup"><span data-stu-id="59563-133">provisioningState values</span></span>

<span data-ttu-id="59563-134">Bir kaynak oluşturma, güncelleştirme veya silme (PUT, PATCH, Sil) işlemleri genellikle dönmek bir `provisioningState` değeri.</span><span class="sxs-lookup"><span data-stu-id="59563-134">Operations that create, update, or delete (PUT, PATCH, DELETE) a resource typically return a `provisioningState` value.</span></span> <span data-ttu-id="59563-135">Bir işlem tamamlandığında, aşağıdaki üç değerden birini verilir:</span><span class="sxs-lookup"><span data-stu-id="59563-135">When an operation has completed, one of following three values is returned:</span></span> 

* <span data-ttu-id="59563-136">Başarılı oldu</span><span class="sxs-lookup"><span data-stu-id="59563-136">Succeeded</span></span>
* <span data-ttu-id="59563-137">Başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="59563-137">Failed</span></span>
* <span data-ttu-id="59563-138">İptal edildi</span><span class="sxs-lookup"><span data-stu-id="59563-138">Canceled</span></span>

<span data-ttu-id="59563-139">Diğer tüm değerler işlemi hala çalışıyor gösterir.</span><span class="sxs-lookup"><span data-stu-id="59563-139">All other values indicate the operation is still running.</span></span> <span data-ttu-id="59563-140">Kaynak sağlayıcısı durumunu gösteren özelleştirilmiş bir değeri geri dönebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59563-140">The resource provider can return a customized value that indicates its state.</span></span> <span data-ttu-id="59563-141">Örneğin, alabileceğiniz **kabul edilen** alınan ve çalışan istek olduğunda.</span><span class="sxs-lookup"><span data-stu-id="59563-141">For example, you may receive **Accepted** when the request is received and running.</span></span>

## <a name="example-requests-and-responses"></a><span data-ttu-id="59563-142">Örnek istekleri ve yanıtları</span><span class="sxs-lookup"><span data-stu-id="59563-142">Example requests and responses</span></span>

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a><span data-ttu-id="59563-143">Sanal makine (Azure AsyncOperation ile 202) Başlat</span><span class="sxs-lookup"><span data-stu-id="59563-143">Start virtual machine (202 with Azure-AsyncOperation)</span></span>
<span data-ttu-id="59563-144">Bu örnek durumunu belirlemek nasıl gösterir **Başlat** sanal makineler için işlem.</span><span class="sxs-lookup"><span data-stu-id="59563-144">This example shows how to determine the status of **start** operation for virtual machines.</span></span> <span data-ttu-id="59563-145">İlk istek aşağıdaki biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="59563-145">The initial request is in the following format:</span></span>

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

<span data-ttu-id="59563-146">Durum kodu 202 döndürür.</span><span class="sxs-lookup"><span data-stu-id="59563-146">It returns status code 202.</span></span> <span data-ttu-id="59563-147">Üstbilgi değerleri arasında görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="59563-147">Among the header values, you see:</span></span>

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="59563-148">Bu URL başka bir isteği gönderilirken zaman uyumsuz işlemin durumunu denetlemek için.</span><span class="sxs-lookup"><span data-stu-id="59563-148">To check the status of the asynchronous operation, sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="59563-149">Yanıt gövdesi işlemin durumunu içerir:</span><span class="sxs-lookup"><span data-stu-id="59563-149">The response body contains the status of the operation:</span></span>

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a><span data-ttu-id="59563-150">Kaynakları (201 Azure AsyncOperation ile) dağıtma</span><span class="sxs-lookup"><span data-stu-id="59563-150">Deploy resources (201 with Azure-AsyncOperation)</span></span>

<span data-ttu-id="59563-151">Bu örnek durumunu belirlemek nasıl gösterir **dağıtımları** kaynakları Azure'a dağıtma işlemi.</span><span class="sxs-lookup"><span data-stu-id="59563-151">This example shows how to determine the status of **deployments** operation for deploying resources to Azure.</span></span> <span data-ttu-id="59563-152">İlk istek aşağıdaki biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="59563-152">The initial request is in the following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

<span data-ttu-id="59563-153">201 durum kodunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="59563-153">It returns status code 201.</span></span> <span data-ttu-id="59563-154">Yanıtın gövdesini içerir:</span><span class="sxs-lookup"><span data-stu-id="59563-154">The body of the response includes:</span></span>

```json
"provisioningState":"Accepted",
```

<span data-ttu-id="59563-155">Üstbilgi değerleri arasında görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="59563-155">Among the header values, you see:</span></span>

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="59563-156">Bu URL başka bir isteği gönderilirken zaman uyumsuz işlemin durumunu denetlemek için.</span><span class="sxs-lookup"><span data-stu-id="59563-156">To check the status of the asynchronous operation, sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="59563-157">Yanıt gövdesi işlemin durumunu içerir:</span><span class="sxs-lookup"><span data-stu-id="59563-157">The response body contains the status of the operation:</span></span>

```json
{"status":"Running"}
```

<span data-ttu-id="59563-158">Dağıtım tamamlandığında, yanıtın içerir:</span><span class="sxs-lookup"><span data-stu-id="59563-158">When the deployment is finished, the response contains:</span></span>

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a><span data-ttu-id="59563-159">Depolama hesabı (202 konumla ve yeniden deneme sonrasında) oluşturma</span><span class="sxs-lookup"><span data-stu-id="59563-159">Create storage account (202 with Location and Retry-After)</span></span>

<span data-ttu-id="59563-160">Bu örnek durumunu belirlemek nasıl gösterir **oluşturma** işlem depolama hesapları için.</span><span class="sxs-lookup"><span data-stu-id="59563-160">This example shows how to determine the status of the **create** operation for storage accounts.</span></span> <span data-ttu-id="59563-161">İlk istek aşağıdaki biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="59563-161">The initial request is in the following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

<span data-ttu-id="59563-162">Ve istek gövdesi depolama hesabı özellikleri içerir:</span><span class="sxs-lookup"><span data-stu-id="59563-162">And the request body contains properties for the storage account:</span></span>

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

<span data-ttu-id="59563-163">Durum kodu 202 döndürür.</span><span class="sxs-lookup"><span data-stu-id="59563-163">It returns status code 202.</span></span> <span data-ttu-id="59563-164">Üstbilgi değerleri arasında aşağıdaki iki değerden görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="59563-164">Among the header values, you see the following two values:</span></span>

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

<span data-ttu-id="59563-165">Bekleyen sayısı için belirtilen yeniden deneme sonrasında onay zaman uyumsuz işlemin durumunu bu URL başka bir istek göndererek saniye sonra.</span><span class="sxs-lookup"><span data-stu-id="59563-165">After waiting for number of seconds specified in Retry-After, check the status of the asynchronous operation by sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

<span data-ttu-id="59563-166">İstek hala devam ediyorsa, bir durum kodu 202 alırsınız.</span><span class="sxs-lookup"><span data-stu-id="59563-166">If the request is still running, you receive a status code 202.</span></span> <span data-ttu-id="59563-167">İstek tamamladıysa, durum kodu 200'ü alırsınız ve yanıtın gövdesini oluşturulduktan sonra depolama hesabının özelliklerini içerir.</span><span class="sxs-lookup"><span data-stu-id="59563-167">If the request has completed, your receive a status code 200, and the body of the response contains the properties of the storage account that has been created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59563-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="59563-168">Next steps</span></span>

* <span data-ttu-id="59563-169">Her REST işlemini ilgili belgeler için bkz: [REST API belgeleri](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="59563-169">For documentation about each REST operation, see [REST API documentation](/rest/api/).</span></span>
* <span data-ttu-id="59563-170">Resource Manager REST API'si aracılığıyla kaynaklarını yönetme hakkında daha fazla bilgi için bkz: [Resource Manager REST API kullanarak](resource-manager-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="59563-170">For information about managing resources through the Resource Manager REST API, see [Using the Resource Manager REST API](resource-manager-rest-api.md).</span></span>
* <span data-ttu-id="59563-171">Resource Manager REST API'si aracılığıyla şablonları dağıtma hakkında daha fazla bilgi için bkz: [Resource Manager şablonları ve Resource Manager REST API kaynaklarla dağıtmak](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="59563-171">for information about deploying templates through the Resource Manager REST API, see [Deploy resources with Resource Manager templates and Resource Manager REST API](resource-group-template-deploy-rest.md).</span></span>