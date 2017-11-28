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
# <a name="track-asynchronous-azure-operations"></a><span data-ttu-id="4d121-103">Zaman uyumsuz Azure işlemleri izleme</span><span class="sxs-lookup"><span data-stu-id="4d121-103">Track asynchronous Azure operations</span></span>
<span data-ttu-id="4d121-104">Bazı Azure REST işlemlerini zaman uyumsuz olarak çalışır, çünkü Hello işlem hızlı bir şekilde tamamlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="4d121-104">Some Azure REST operations run asynchronously because hello operation cannot be completed quickly.</span></span> <span data-ttu-id="4d121-105">Bu konuda nasıl tootrack hello değerleri arasında zaman uyumsuz işlemleri durumunu hello yanıtında açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4d121-105">This topic describes how tootrack hello status of asynchronous operations through values returned in hello response.</span></span>  

## <a name="status-codes-for-asynchronous-operations"></a><span data-ttu-id="4d121-106">Zaman uyumsuz işlemleri için durum kodları</span><span class="sxs-lookup"><span data-stu-id="4d121-106">Status codes for asynchronous operations</span></span>
<span data-ttu-id="4d121-107">Zaman uyumsuz bir işlem, başlangıçta bir HTTP durum kodu ya da döndürür:</span><span class="sxs-lookup"><span data-stu-id="4d121-107">An asynchronous operation initially returns an HTTP status code of either:</span></span>

* <span data-ttu-id="4d121-108">201 (oluşturuldu)</span><span class="sxs-lookup"><span data-stu-id="4d121-108">201 (Created)</span></span>
* <span data-ttu-id="4d121-109">202 (kabul edilen)</span><span class="sxs-lookup"><span data-stu-id="4d121-109">202 (Accepted)</span></span> 

<span data-ttu-id="4d121-110">Merhaba işlemi başarıyla tamamlandığında, ya da döndürür:</span><span class="sxs-lookup"><span data-stu-id="4d121-110">When hello operation successfully completes, it returns either:</span></span>

* <span data-ttu-id="4d121-111">200 (TAMAM)</span><span class="sxs-lookup"><span data-stu-id="4d121-111">200 (OK)</span></span>
* <span data-ttu-id="4d121-112">204 (içerik yok)</span><span class="sxs-lookup"><span data-stu-id="4d121-112">204 (No Content)</span></span> 

<span data-ttu-id="4d121-113">Toohello başvuran [REST API belgeleri](/rest/api/) toosee hello yanıtlar yürütme hello işlemi için.</span><span class="sxs-lookup"><span data-stu-id="4d121-113">Refer toohello [REST API documentation](/rest/api/) toosee hello responses for hello operation you are executing.</span></span> 

## <a name="monitor-status-of-operation"></a><span data-ttu-id="4d121-114">İşlemin durumunu izleyin</span><span class="sxs-lookup"><span data-stu-id="4d121-114">Monitor status of operation</span></span>
<span data-ttu-id="4d121-115">toodetermine hello durumunu kullandığınız hello zaman uyumsuz REST işlemlerini dönüş üstbilgi değerleri, işlem hello.</span><span class="sxs-lookup"><span data-stu-id="4d121-115">hello asynchronous REST operations return header values, which you use toodetermine hello status of hello operation.</span></span> <span data-ttu-id="4d121-116">Büyük olasılıkla üç üstbilgi değerleri tooexamine vardır:</span><span class="sxs-lookup"><span data-stu-id="4d121-116">There are potentially three header values tooexamine:</span></span>

* <span data-ttu-id="4d121-117">`Azure-AsyncOperation`-Hello hello işlemi devam eden durumunu denetlemek için URL.</span><span class="sxs-lookup"><span data-stu-id="4d121-117">`Azure-AsyncOperation` - URL for checking hello ongoing status of hello operation.</span></span> <span data-ttu-id="4d121-118">Her zaman işleminizi bu değer döndürürse, BT (konum) yerine tootrack hello hello işlemin durumunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="4d121-118">If your operation returns this value, always use it (instead of Location) tootrack hello status of hello operation.</span></span>
* <span data-ttu-id="4d121-119">`Location`-Ne zaman bir işlemin tamamlanmasını belirlemek için URL.</span><span class="sxs-lookup"><span data-stu-id="4d121-119">`Location` - URL for determining when an operation has completed.</span></span> <span data-ttu-id="4d121-120">Yalnızca Azure AsyncOperation alınmadı olduğunda bu değeri kullanın.</span><span class="sxs-lookup"><span data-stu-id="4d121-120">Use this value only when Azure-AsyncOperation is not returned.</span></span>
* <span data-ttu-id="4d121-121">`Retry-After`-hello saniye toowait sayısı hello hello zaman uyumsuz işlemin durumunu denetlemeden önce.</span><span class="sxs-lookup"><span data-stu-id="4d121-121">`Retry-After` - hello number of seconds toowait before checking hello status of hello asynchronous operation.</span></span>

<span data-ttu-id="4d121-122">Bununla birlikte, her zaman uyumsuz işlemi bu tüm değerleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="4d121-122">However, not every asynchronous operation returns all these values.</span></span> <span data-ttu-id="4d121-123">Örneğin, bir işlemi ve başka bir işlem için hello konum üstbilgisi değeri tooevaluate hello Azure AsyncOperation üstbilgi değeri gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="4d121-123">For example, you may need tooevaluate hello Azure-AsyncOperation header value for one operation, and hello Location header value for another operation.</span></span> 

<span data-ttu-id="4d121-124">Bir istek için herhangi bir üstbilgi değerini almak gibi hello üstbilgi değerlerini alır.</span><span class="sxs-lookup"><span data-stu-id="4d121-124">You retrieve hello header values as you would retrieve any header value for a request.</span></span> <span data-ttu-id="4d121-125">Örneğin, C# ' ta hello üstbilgi değeri aldığınız bir `HttpWebResponse` adlı nesne `response` koddan hello ile:</span><span class="sxs-lookup"><span data-stu-id="4d121-125">For example, in C#, you retrieve hello header value from an `HttpWebResponse` object named `response` with hello following code:</span></span>

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a><span data-ttu-id="4d121-126">Azure AsyncOperation istek ve yanıt</span><span class="sxs-lookup"><span data-stu-id="4d121-126">Azure-AsyncOperation request and response</span></span>

<span data-ttu-id="4d121-127">tooget hello hello zaman uyumsuz işlem durumunu Azure AsyncOperation Üstbilgi değerinde bir GET isteği toohello URL gönderin.</span><span class="sxs-lookup"><span data-stu-id="4d121-127">tooget hello status of hello asynchronous operation, send a GET request toohello URL in Azure-AsyncOperation header value.</span></span>

<span data-ttu-id="4d121-128">Bu işlem hello yanıttan Hello gövdesini hello işlemiyle ilgili bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="4d121-128">hello body of hello response from this operation contains information about hello operation.</span></span> <span data-ttu-id="4d121-129">Merhaba aşağıdaki örnekte hello işleminden döndürülen hello olası değerler gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="4d121-129">hello following example shows hello possible values returned from hello operation:</span></span>

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

<span data-ttu-id="4d121-130">Yalnızca `status` tüm yanıtlar için döndürülür.</span><span class="sxs-lookup"><span data-stu-id="4d121-130">Only `status` is returned for all responses.</span></span> <span data-ttu-id="4d121-131">Merhaba durumu başarısız veya iptal edildi olduğunda hello hata nesnesi döndürülür.</span><span class="sxs-lookup"><span data-stu-id="4d121-131">hello error object is returned when hello status is Failed or Canceled.</span></span> <span data-ttu-id="4d121-132">Diğer tüm değerler isteğe bağlıdır; Bu nedenle, aldığınız hello yanıt hello örnek farklı görünebilir.</span><span class="sxs-lookup"><span data-stu-id="4d121-132">All other values are optional; therefore, hello response you receive may look different than hello example.</span></span>

## <a name="provisioningstate-values"></a><span data-ttu-id="4d121-133">provisioningState değerleri</span><span class="sxs-lookup"><span data-stu-id="4d121-133">provisioningState values</span></span>

<span data-ttu-id="4d121-134">Bir kaynak oluşturma, güncelleştirme veya silme (PUT, PATCH, Sil) işlemleri genellikle dönmek bir `provisioningState` değeri.</span><span class="sxs-lookup"><span data-stu-id="4d121-134">Operations that create, update, or delete (PUT, PATCH, DELETE) a resource typically return a `provisioningState` value.</span></span> <span data-ttu-id="4d121-135">Bir işlem tamamlandığında, aşağıdaki üç değerden birini verilir:</span><span class="sxs-lookup"><span data-stu-id="4d121-135">When an operation has completed, one of following three values is returned:</span></span> 

* <span data-ttu-id="4d121-136">Başarılı oldu</span><span class="sxs-lookup"><span data-stu-id="4d121-136">Succeeded</span></span>
* <span data-ttu-id="4d121-137">Başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="4d121-137">Failed</span></span>
* <span data-ttu-id="4d121-138">İptal edildi</span><span class="sxs-lookup"><span data-stu-id="4d121-138">Canceled</span></span>

<span data-ttu-id="4d121-139">Diğer tüm değerler hello işlemi hala çalışıyor gösterir.</span><span class="sxs-lookup"><span data-stu-id="4d121-139">All other values indicate hello operation is still running.</span></span> <span data-ttu-id="4d121-140">Merhaba kaynak sağlayıcısı durumunu gösteren özelleştirilmiş bir değeri geri dönebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d121-140">hello resource provider can return a customized value that indicates its state.</span></span> <span data-ttu-id="4d121-141">Örneğin, alabileceğiniz **kabul edilen** alınan ve çalışan hello istek olduğunda.</span><span class="sxs-lookup"><span data-stu-id="4d121-141">For example, you may receive **Accepted** when hello request is received and running.</span></span>

## <a name="example-requests-and-responses"></a><span data-ttu-id="4d121-142">Örnek istekleri ve yanıtları</span><span class="sxs-lookup"><span data-stu-id="4d121-142">Example requests and responses</span></span>

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a><span data-ttu-id="4d121-143">Sanal makine (Azure AsyncOperation ile 202) Başlat</span><span class="sxs-lookup"><span data-stu-id="4d121-143">Start virtual machine (202 with Azure-AsyncOperation)</span></span>
<span data-ttu-id="4d121-144">Bu örnek nasıl toodetermine hello durumunu gösterir **Başlat** sanal makineler için işlem.</span><span class="sxs-lookup"><span data-stu-id="4d121-144">This example shows how toodetermine hello status of **start** operation for virtual machines.</span></span> <span data-ttu-id="4d121-145">Hello ilk istek hello biçimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="4d121-145">hello initial request is in hello following format:</span></span>

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

<span data-ttu-id="4d121-146">Durum kodu 202 döndürür.</span><span class="sxs-lookup"><span data-stu-id="4d121-146">It returns status code 202.</span></span> <span data-ttu-id="4d121-147">Merhaba üstbilgi değerleri arasında görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="4d121-147">Among hello header values, you see:</span></span>

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="4d121-148">başka bir istek toothat URL'si gönderme hello zaman uyumsuz işlem toocheck hello durumu.</span><span class="sxs-lookup"><span data-stu-id="4d121-148">toocheck hello status of hello asynchronous operation, sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="4d121-149">Merhaba yanıt gövdesi hello işlemi hello durumunu içerir:</span><span class="sxs-lookup"><span data-stu-id="4d121-149">hello response body contains hello status of hello operation:</span></span>

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a><span data-ttu-id="4d121-150">Kaynakları (201 Azure AsyncOperation ile) dağıtma</span><span class="sxs-lookup"><span data-stu-id="4d121-150">Deploy resources (201 with Azure-AsyncOperation)</span></span>

<span data-ttu-id="4d121-151">Bu örnek nasıl toodetermine hello durumunu gösterir **dağıtımları** kaynakları tooAzure dağıtma işlemi.</span><span class="sxs-lookup"><span data-stu-id="4d121-151">This example shows how toodetermine hello status of **deployments** operation for deploying resources tooAzure.</span></span> <span data-ttu-id="4d121-152">Hello ilk istek hello biçimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="4d121-152">hello initial request is in hello following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

<span data-ttu-id="4d121-153">201 durum kodunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="4d121-153">It returns status code 201.</span></span> <span data-ttu-id="4d121-154">Merhaba hello yanıtın gövdesini içerir:</span><span class="sxs-lookup"><span data-stu-id="4d121-154">hello body of hello response includes:</span></span>

```json
"provisioningState":"Accepted",
```

<span data-ttu-id="4d121-155">Merhaba üstbilgi değerleri arasında görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="4d121-155">Among hello header values, you see:</span></span>

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="4d121-156">başka bir istek toothat URL'si gönderme hello zaman uyumsuz işlem toocheck hello durumu.</span><span class="sxs-lookup"><span data-stu-id="4d121-156">toocheck hello status of hello asynchronous operation, sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="4d121-157">Merhaba yanıt gövdesi hello işlemi hello durumunu içerir:</span><span class="sxs-lookup"><span data-stu-id="4d121-157">hello response body contains hello status of hello operation:</span></span>

```json
{"status":"Running"}
```

<span data-ttu-id="4d121-158">Merhaba dağıtım tamamlandığında, hello yanıtı içerir:</span><span class="sxs-lookup"><span data-stu-id="4d121-158">When hello deployment is finished, hello response contains:</span></span>

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a><span data-ttu-id="4d121-159">Depolama hesabı (202 konumla ve yeniden deneme sonrasında) oluşturma</span><span class="sxs-lookup"><span data-stu-id="4d121-159">Create storage account (202 with Location and Retry-After)</span></span>

<span data-ttu-id="4d121-160">Bu örnek nasıl toodetermine hello hello durumunu gösterir **oluşturma** işlem depolama hesapları için.</span><span class="sxs-lookup"><span data-stu-id="4d121-160">This example shows how toodetermine hello status of hello **create** operation for storage accounts.</span></span> <span data-ttu-id="4d121-161">Hello ilk istek hello biçimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="4d121-161">hello initial request is in hello following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

<span data-ttu-id="4d121-162">Ve hello istek gövdesi hello depolama hesabı için özellikleri içerir:</span><span class="sxs-lookup"><span data-stu-id="4d121-162">And hello request body contains properties for hello storage account:</span></span>

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

<span data-ttu-id="4d121-163">Durum kodu 202 döndürür.</span><span class="sxs-lookup"><span data-stu-id="4d121-163">It returns status code 202.</span></span> <span data-ttu-id="4d121-164">Merhaba üstbilgi değerleri arasında iki değer aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="4d121-164">Among hello header values, you see hello following two values:</span></span>

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

<span data-ttu-id="4d121-165">Sayısı için bekleyen sonra saniye belirtilen yeniden deneme-sonrası, başka bir istek toothat URL'si göndererek hello hello zaman uyumsuz işlemin durumunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="4d121-165">After waiting for number of seconds specified in Retry-After, check hello status of hello asynchronous operation by sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

<span data-ttu-id="4d121-166">Merhaba isteği hala devam ediyorsa, bir durum kodu 202 alırsınız.</span><span class="sxs-lookup"><span data-stu-id="4d121-166">If hello request is still running, you receive a status code 202.</span></span> <span data-ttu-id="4d121-167">Merhaba isteği tamamlanmışsa, durum kodu 200'ü alırsınız ve hello hello yanıtın gövdesini hello oluşturuldu hello depolama hesabının özelliklerini içerir.</span><span class="sxs-lookup"><span data-stu-id="4d121-167">If hello request has completed, your receive a status code 200, and hello body of hello response contains hello properties of hello storage account that has been created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d121-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4d121-168">Next steps</span></span>

* <span data-ttu-id="4d121-169">Her REST işlemini ilgili belgeler için bkz: [REST API belgeleri](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="4d121-169">For documentation about each REST operation, see [REST API documentation](/rest/api/).</span></span>
* <span data-ttu-id="4d121-170">Merhaba Resource Manager REST API'si aracılığıyla kaynaklarını yönetme hakkında daha fazla bilgi için bkz: [kullanma hello Resource Manager REST API'si](resource-manager-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="4d121-170">For information about managing resources through hello Resource Manager REST API, see [Using hello Resource Manager REST API](resource-manager-rest-api.md).</span></span>
* <span data-ttu-id="4d121-171">Şablonları hello Resource Manager REST API'si aracılığıyla dağıtma hakkında daha fazla bilgi için bkz: [Resource Manager şablonları ve Resource Manager REST API kaynaklarla dağıtmak](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="4d121-171">for information about deploying templates through hello Resource Manager REST API, see [Deploy resources with Resource Manager templates and Resource Manager REST API](resource-group-template-deploy-rest.md).</span></span>
