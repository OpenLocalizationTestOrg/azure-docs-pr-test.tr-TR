---
title: "aaaAzure Resource Manager şablonu işlevleri - kaynakları | Microsoft Docs"
description: "Bir Azure Resource Manager şablonu tooretrieve değerleri Hello işlevleri toouse kaynaklar hakkında açıklar."
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
ms.date: 08/09/2017
ms.author: tomfitz
ms.openlocfilehash: c9d524b338b8b7ea6d8c9e0135d48e4fb8f167c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="800a8-103">Azure Resource Manager şablonları için kaynak işlevleri</span><span class="sxs-lookup"><span data-stu-id="800a8-103">Resource functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="800a8-104">Resource Manager kaynak değerlerini alma işlevleri aşağıdaki hello sunar:</span><span class="sxs-lookup"><span data-stu-id="800a8-104">Resource Manager provides hello following functions for getting resource values:</span></span>

* [<span data-ttu-id="800a8-105">listKeys ve liste {Value}</span><span class="sxs-lookup"><span data-stu-id="800a8-105">listKeys and list{Value}</span></span>](#listkeys)
* [<span data-ttu-id="800a8-106">sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="800a8-106">providers</span></span>](#providers)
* [<span data-ttu-id="800a8-107">başvuru</span><span class="sxs-lookup"><span data-stu-id="800a8-107">reference</span></span>](#reference)
* [<span data-ttu-id="800a8-108">kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="800a8-108">resourceGroup</span></span>](#resourcegroup)
* [<span data-ttu-id="800a8-109">ResourceId</span><span class="sxs-lookup"><span data-stu-id="800a8-109">resourceId</span></span>](#resourceid)
* [<span data-ttu-id="800a8-110">aboneliği</span><span class="sxs-lookup"><span data-stu-id="800a8-110">subscription</span></span>](#subscription)

<span data-ttu-id="800a8-111">Parametreler, değişkenleri ya da hello geçerli dağıtımı, tooget değerleri görmek [dağıtım değer işlevleri](resource-group-template-functions-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="800a8-111">tooget values from parameters, variables, or hello current deployment, see [Deployment value functions](resource-group-template-functions-deployment.md).</span></span>

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a><span data-ttu-id="800a8-112">listKeys ve liste {Value}</span><span class="sxs-lookup"><span data-stu-id="800a8-112">listKeys and list{Value}</span></span>
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

<span data-ttu-id="800a8-113">Hello liste işlemi destekleyen herhangi bir kaynak türü için değerleri verir hello.</span><span class="sxs-lookup"><span data-stu-id="800a8-113">Returns hello values for any resource type that supports hello list operation.</span></span> <span data-ttu-id="800a8-114">Merhaba en yaygın kullanımı `listKeys`.</span><span class="sxs-lookup"><span data-stu-id="800a8-114">hello most common usage is `listKeys`.</span></span> 

### <a name="parameters"></a><span data-ttu-id="800a8-115">Parametreler</span><span class="sxs-lookup"><span data-stu-id="800a8-115">Parameters</span></span>

| <span data-ttu-id="800a8-116">Parametre</span><span class="sxs-lookup"><span data-stu-id="800a8-116">Parameter</span></span> | <span data-ttu-id="800a8-117">Gerekli</span><span class="sxs-lookup"><span data-stu-id="800a8-117">Required</span></span> | <span data-ttu-id="800a8-118">Tür</span><span class="sxs-lookup"><span data-stu-id="800a8-118">Type</span></span> | <span data-ttu-id="800a8-119">Açıklama</span><span class="sxs-lookup"><span data-stu-id="800a8-119">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="800a8-120">resourceName veya resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="800a8-120">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="800a8-121">Evet</span><span class="sxs-lookup"><span data-stu-id="800a8-121">Yes</span></span> |<span data-ttu-id="800a8-122">Dize</span><span class="sxs-lookup"><span data-stu-id="800a8-122">string</span></span> |<span data-ttu-id="800a8-123">Merhaba kaynak için benzersiz tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="800a8-123">Unique identifier for hello resource.</span></span> |
| <span data-ttu-id="800a8-124">apiVersion</span><span class="sxs-lookup"><span data-stu-id="800a8-124">apiVersion</span></span> |<span data-ttu-id="800a8-125">Evet</span><span class="sxs-lookup"><span data-stu-id="800a8-125">Yes</span></span> |<span data-ttu-id="800a8-126">Dize</span><span class="sxs-lookup"><span data-stu-id="800a8-126">string</span></span> |<span data-ttu-id="800a8-127">Kaynak çalışma zamanı durumunu API sürümü.</span><span class="sxs-lookup"><span data-stu-id="800a8-127">API version of resource runtime state.</span></span> <span data-ttu-id="800a8-128">Genellikle, biçiminde hello **yyyy-aa-gg**.</span><span class="sxs-lookup"><span data-stu-id="800a8-128">Typically, in hello format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="800a8-129">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="800a8-129">Return value</span></span>

<span data-ttu-id="800a8-130">Merhaba listKeys nesnesinden biçimini izleyen hello döndürdü:</span><span class="sxs-lookup"><span data-stu-id="800a8-130">hello returned object from listKeys has hello following format:</span></span>

```json
{
  "keys": [
    {
      "keyName": "key1",
      "permissions": "Full",
      "value": "{value}"
    },
    {
      "keyName": "key2",
      "permissions": "Full",
      "value": "{value}"
    }
  ]
}
```

<span data-ttu-id="800a8-131">Diğer liste işlevler farklı dönüş biçimlerine sahip.</span><span class="sxs-lookup"><span data-stu-id="800a8-131">Other list functions have different return formats.</span></span> <span data-ttu-id="800a8-132">bir işlevin toosee hello biçimi dahil hello çıkışları bölümünde hello örnek şablonda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="800a8-132">toosee hello format of a function, include it in hello outputs section as shown in hello example template.</span></span> 

### <a name="remarks"></a><span data-ttu-id="800a8-133">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="800a8-133">Remarks</span></span>

<span data-ttu-id="800a8-134">İle başlayan herhangi bir işlem **listesi** şablonunuzda bir işlevi olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="800a8-134">Any operation that starts with **list** can be used as a function in your template.</span></span> <span data-ttu-id="800a8-135">Merhaba kullanılabilir işlemleri arasında yalnızca listKeys, ancak ayrıca operations ister `list`, `listAdminKeys`, ve `listStatus`.</span><span class="sxs-lookup"><span data-stu-id="800a8-135">hello available operations include not only listKeys, but also operations like `list`, `listAdminKeys`, and `listStatus`.</span></span> <span data-ttu-id="800a8-136">Ancak, kullanamazsınız **listesi** hello değerleri gerektiren işlemler iste gövde.</span><span class="sxs-lookup"><span data-stu-id="800a8-136">However, you cannot use **list** operations that require values in hello request body.</span></span> <span data-ttu-id="800a8-137">Örneğin, hello [listesi hesap SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) işlem gerektirir istek gövde parametreleri ister *signedExpiry*, dolayısıyla bir şablonda kullanamaz.</span><span class="sxs-lookup"><span data-stu-id="800a8-137">For example, hello [List Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operation requires request body parameters like *signedExpiry*, so you cannot use it within a template.</span></span>

<span data-ttu-id="800a8-138">hangi kaynak türlerinin bir listesini işleme sahip toodetermine, aşağıdaki seçenekleri şu hello vardır:</span><span class="sxs-lookup"><span data-stu-id="800a8-138">toodetermine which resource types have a list operation, you have hello following options:</span></span>

* <span data-ttu-id="800a8-139">Görünüm hello [REST API işlemleri](/rest/api/) için bir kaynak sağlayıcısı ve listeleme işlemleri arayın.</span><span class="sxs-lookup"><span data-stu-id="800a8-139">View hello [REST API operations](/rest/api/) for a resource provider, and look for list operations.</span></span> <span data-ttu-id="800a8-140">Örneğin, depolama hesapları hello sahip [listKeys işlemi](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span><span class="sxs-lookup"><span data-stu-id="800a8-140">For example, storage accounts have hello [listKeys operation](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span></span>
* <span data-ttu-id="800a8-141">Kullanım hello [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="800a8-141">Use hello [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet.</span></span> <span data-ttu-id="800a8-142">Merhaba aşağıdaki örnekte tüm liste işlemler depolama hesapları için alır:</span><span class="sxs-lookup"><span data-stu-id="800a8-142">hello following example gets all list operations for storage accounts:</span></span>

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* <span data-ttu-id="800a8-143">Azure CLI komutu toofilter listeleme işlemleri yalnızca hello aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="800a8-143">Use hello following Azure CLI command toofilter only hello list operations:</span></span>

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

<span data-ttu-id="800a8-144">Merhaba kaynak ya da hello kullanarak belirttiğiniz [ResourceId işlevi](#resourceid), veya hello biçimi `{providerNamespace}/{resourceType}/{resourceName}`.</span><span class="sxs-lookup"><span data-stu-id="800a8-144">Specify hello resource by using either hello [resourceId function](#resourceid), or hello format `{providerNamespace}/{resourceType}/{resourceName}`.</span></span>


### <a name="example"></a><span data-ttu-id="800a8-145">Örnek</span><span class="sxs-lookup"><span data-stu-id="800a8-145">Example</span></span>

<span data-ttu-id="800a8-146">Merhaba aşağıdaki örnekte nasıl hello bir depolama hesabından tooreturn hello birincil ve ikincil anahtarları çıkarır bölümünde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="800a8-146">hello following example shows how tooreturn hello primary and secondary keys from a storage account in hello outputs section.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountId": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "storageKeysOutput": {
            "value": "[listKeys(parameters('storageAccountId'), '2016-01-01')]",
            "type" : "object"
        }
    }
}
``` 

<a id="providers" />

## <a name="providers"></a><span data-ttu-id="800a8-147">sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="800a8-147">providers</span></span>
`providers(providerNamespace, [resourceType])`

<span data-ttu-id="800a8-148">Bir kaynak sağlayıcısı ve desteklenen kaynak türleri hakkında bilgi döndürür.</span><span class="sxs-lookup"><span data-stu-id="800a8-148">Returns information about a resource provider and its supported resource types.</span></span> <span data-ttu-id="800a8-149">Bir kaynak türü belirtmezseniz, tüm desteklenen hello türleri hello kaynak sağlayıcısı için hello işlevi döndürür.</span><span class="sxs-lookup"><span data-stu-id="800a8-149">If you do not provide a resource type, hello function returns all hello supported types for hello resource provider.</span></span>

### <a name="parameters"></a><span data-ttu-id="800a8-150">Parametreler</span><span class="sxs-lookup"><span data-stu-id="800a8-150">Parameters</span></span>

| <span data-ttu-id="800a8-151">Parametre</span><span class="sxs-lookup"><span data-stu-id="800a8-151">Parameter</span></span> | <span data-ttu-id="800a8-152">Gerekli</span><span class="sxs-lookup"><span data-stu-id="800a8-152">Required</span></span> | <span data-ttu-id="800a8-153">Tür</span><span class="sxs-lookup"><span data-stu-id="800a8-153">Type</span></span> | <span data-ttu-id="800a8-154">Açıklama</span><span class="sxs-lookup"><span data-stu-id="800a8-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="800a8-155">providerNamespace</span><span class="sxs-lookup"><span data-stu-id="800a8-155">providerNamespace</span></span> |<span data-ttu-id="800a8-156">Evet</span><span class="sxs-lookup"><span data-stu-id="800a8-156">Yes</span></span> |<span data-ttu-id="800a8-157">Dize</span><span class="sxs-lookup"><span data-stu-id="800a8-157">string</span></span> |<span data-ttu-id="800a8-158">Namespace hello sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="800a8-158">Namespace of hello provider</span></span> |
| <span data-ttu-id="800a8-159">Kaynak türü</span><span class="sxs-lookup"><span data-stu-id="800a8-159">resourceType</span></span> |<span data-ttu-id="800a8-160">Hayır</span><span class="sxs-lookup"><span data-stu-id="800a8-160">No</span></span> |<span data-ttu-id="800a8-161">Dize</span><span class="sxs-lookup"><span data-stu-id="800a8-161">string</span></span> |<span data-ttu-id="800a8-162">Merhaba türde bir hello içindeki kaynak ad alanı belirtildi.</span><span class="sxs-lookup"><span data-stu-id="800a8-162">hello type of resource within hello specified namespace.</span></span> |

### <a name="return-value"></a><span data-ttu-id="800a8-163">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="800a8-163">Return value</span></span>

<span data-ttu-id="800a8-164">Desteklenen her tür biçimi aşağıdaki hello verilir:</span><span class="sxs-lookup"><span data-stu-id="800a8-164">Each supported type is returned in hello following format:</span></span> 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

<span data-ttu-id="800a8-165">Merhaba dizi sıralama değerleri yıkıcıları döndürdü.</span><span class="sxs-lookup"><span data-stu-id="800a8-165">Array ordering of hello returned values is not guaranteed.</span></span>

### <a name="example"></a><span data-ttu-id="800a8-166">Örnek</span><span class="sxs-lookup"><span data-stu-id="800a8-166">Example</span></span>

<span data-ttu-id="800a8-167">Aşağıdaki örnek hello nasıl toouse hello sağlayıcısı işlevi gösterir:</span><span class="sxs-lookup"><span data-stu-id="800a8-167">hello following example shows how toouse hello provider function:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "providerOutput": {
            "value": "[providers('Microsoft.Web', 'sites')]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="800a8-168">Merhaba önceki örnekte bir nesne biçimini izleyen hello döndürür:</span><span class="sxs-lookup"><span data-stu-id="800a8-168">hello preceding example returns an object in hello following format:</span></span>

```json
{
  "resourceType": "sites",
  "locations": [
    "South Central US",
    "North Europe",
    "West Europe",
    "Southeast Asia",
    ...
  ],
  "apiVersions": [
    "2016-08-01",
    "2016-03-01",
    "2015-08-01-preview",
    "2015-08-01",
    ...
  ]
}
```

<a id="reference" />

## <a name="reference"></a><span data-ttu-id="800a8-169">Başvuru</span><span class="sxs-lookup"><span data-stu-id="800a8-169">reference</span></span>
`reference(resourceName or resourceIdentifier, [apiVersion])`

<span data-ttu-id="800a8-170">Bir kaynağın çalışma zamanı durumunu temsil eden bir nesne döndürür.</span><span class="sxs-lookup"><span data-stu-id="800a8-170">Returns an object representing a resource's runtime state.</span></span>

### <a name="parameters"></a><span data-ttu-id="800a8-171">Parametreler</span><span class="sxs-lookup"><span data-stu-id="800a8-171">Parameters</span></span>

| <span data-ttu-id="800a8-172">Parametre</span><span class="sxs-lookup"><span data-stu-id="800a8-172">Parameter</span></span> | <span data-ttu-id="800a8-173">Gerekli</span><span class="sxs-lookup"><span data-stu-id="800a8-173">Required</span></span> | <span data-ttu-id="800a8-174">Tür</span><span class="sxs-lookup"><span data-stu-id="800a8-174">Type</span></span> | <span data-ttu-id="800a8-175">Açıklama</span><span class="sxs-lookup"><span data-stu-id="800a8-175">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="800a8-176">resourceName veya resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="800a8-176">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="800a8-177">Evet</span><span class="sxs-lookup"><span data-stu-id="800a8-177">Yes</span></span> |<span data-ttu-id="800a8-178">Dize</span><span class="sxs-lookup"><span data-stu-id="800a8-178">string</span></span> |<span data-ttu-id="800a8-179">Adı veya bir kaynak benzersiz tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="800a8-179">Name or unique identifier of a resource.</span></span> |
| <span data-ttu-id="800a8-180">apiVersion</span><span class="sxs-lookup"><span data-stu-id="800a8-180">apiVersion</span></span> |<span data-ttu-id="800a8-181">Hayır</span><span class="sxs-lookup"><span data-stu-id="800a8-181">No</span></span> |<span data-ttu-id="800a8-182">Dize</span><span class="sxs-lookup"><span data-stu-id="800a8-182">string</span></span> |<span data-ttu-id="800a8-183">Kaynak hello API sürümü belirtildi.</span><span class="sxs-lookup"><span data-stu-id="800a8-183">API version of hello specified resource.</span></span> <span data-ttu-id="800a8-184">Merhaba kaynak aynı şablonu içinde değil sağlandığında bu parametreyi dahil edin.</span><span class="sxs-lookup"><span data-stu-id="800a8-184">Include this parameter when hello resource is not provisioned within same template.</span></span> <span data-ttu-id="800a8-185">Genellikle, biçiminde hello **yyyy-aa-gg**.</span><span class="sxs-lookup"><span data-stu-id="800a8-185">Typically, in hello format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="800a8-186">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="800a8-186">Return value</span></span>

<span data-ttu-id="800a8-187">Her kaynak türü hello başvuru işlevi için farklı özellikleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="800a8-187">Every resource type returns different properties for hello reference function.</span></span> <span data-ttu-id="800a8-188">Merhaba işlevi tek, önceden tanımlanmış biçimi döndürmez.</span><span class="sxs-lookup"><span data-stu-id="800a8-188">hello function does not return a single, predefined format.</span></span> <span data-ttu-id="800a8-189">bir kaynak türü için toosee hello özellikleri döndürür hello hello nesnesinde hello örnekte gösterildiği gibi bölüm çıkarır.</span><span class="sxs-lookup"><span data-stu-id="800a8-189">toosee hello properties for a resource type, return hello object in hello outputs section as shown in hello example.</span></span>

### <a name="remarks"></a><span data-ttu-id="800a8-190">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="800a8-190">Remarks</span></span>

<span data-ttu-id="800a8-191">Merhaba başvuru işlevi bir çalışma zamanı durumu değerinden türeten ve hello değişkenler bölümünde bu nedenle kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="800a8-191">hello reference function derives its value from a runtime state, and therefore cannot be used in hello variables section.</span></span> <span data-ttu-id="800a8-192">Şablon çıktıları bölümünde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="800a8-192">It can be used in outputs section of a template.</span></span> 

<span data-ttu-id="800a8-193">Merhaba başvuru işlevini kullanarak, dolaylı olarak başvurulan hello kaynak aynı şablonu içinde sağlandığında, bir kaynak üzerinde başka bir kaynak bağlıdır bildirin.</span><span class="sxs-lookup"><span data-stu-id="800a8-193">By using hello reference function, you implicitly declare that one resource depends on another resource if hello referenced resource is provisioned within same template.</span></span> <span data-ttu-id="800a8-194">Tooalso kullanım hello dependsOn özellik gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="800a8-194">You do not need tooalso use hello dependsOn property.</span></span> <span data-ttu-id="800a8-195">Merhaba başvurulan kaynak dağıtımı tamamlanana kadar hello işlevi değerlendirilmez.</span><span class="sxs-lookup"><span data-stu-id="800a8-195">hello function is not evaluated until hello referenced resource has completed deployment.</span></span>

<span data-ttu-id="800a8-196">toosee hello özellik adları ve değerleri bir kaynak türü için hello çıkışları bölümünde hello nesnesi döndüren bir şablon oluşturun.</span><span class="sxs-lookup"><span data-stu-id="800a8-196">toosee hello property names and values for a resource type, create a template that returns hello object in hello outputs section.</span></span> <span data-ttu-id="800a8-197">Bu tür mevcut bir kaynağı varsa, şablonunuzun herhangi yeni kaynaklar dağıtmadan hello nesnesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="800a8-197">If you have an existing resource of that type, your template returns hello object without deploying any new resources.</span></span> 

<span data-ttu-id="800a8-198">Merhaba genellikle, kullandığınız **başvuru** tooreturn hello blob uç noktası URI gibi nesne veya tam etki alanı adı arasında belirli bir değer işlev.</span><span class="sxs-lookup"><span data-stu-id="800a8-198">Typically, you use hello **reference** function tooreturn a particular value from an object, such as hello blob endpoint URI or fully qualified domain name.</span></span>

```json
"outputs": {
    "BlobUri": {
        "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01').primaryEndpoints.blob]",
        "type" : "string"
    },
    "FQDN": {
        "value": "[reference(concat('Microsoft.Network/publicIPAddresses/', parameters('ipAddressName')), '2016-03-30').dnsSettings.fqdn]",
        "type" : "string"
    }
}
```

### <a name="example"></a><span data-ttu-id="800a8-199">Örnek</span><span class="sxs-lookup"><span data-stu-id="800a8-199">Example</span></span>

<span data-ttu-id="800a8-200">Merhaba toodeploy ve başvuru hello kaynağında aynı şablonu, kullanın:</span><span class="sxs-lookup"><span data-stu-id="800a8-200">toodeploy and reference hello resource in hello same template, use:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "storageAccountName": { 
          "type": "string"
      }
  },
  "resources": [
    {
      "name": "[parameters('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-12-01",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {
      "referenceOutput": {
          "type": "object",
          "value": "[reference(parameters('storageAccountName'))]"
      }
    }
}
``` 

<span data-ttu-id="800a8-201">Merhaba önceki örnekte bir nesne biçimini izleyen hello döndürür:</span><span class="sxs-lookup"><span data-stu-id="800a8-201">hello preceding example returns an object in hello following format:</span></span>

```json
{
   "creationTime": "2017-06-13T21:24:46.618364Z",
   "primaryEndpoints": {
     "blob": "https://examplestorage.blob.core.windows.net/",
     "file": "https://examplestorage.file.core.windows.net/",
     "queue": "https://examplestorage.queue.core.windows.net/",
     "table": "https://examplestorage.table.core.windows.net/"
   },
   "primaryLocation": "southcentralus",
   "provisioningState": "Succeeded",
   "statusOfPrimary": "available",
   "supportsHttpsTrafficOnly": false
}
```

<span data-ttu-id="800a8-202">Merhaba aşağıdaki örnekte bu şablonda dağıtılmamış bir depolama hesabı başvurur.</span><span class="sxs-lookup"><span data-stu-id="800a8-202">hello following example references a storage account that is not deployed in this template.</span></span> <span data-ttu-id="800a8-203">Merhaba depolama hesabı hello içinde aynı zaten kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="800a8-203">hello storage account already exists within hello same resource group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "ExistingStorage": {
            "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01')]",
            "type" : "object"
        }
    }
}
```

<a id="resourcegroup" />

## <a name="resourcegroup"></a><span data-ttu-id="800a8-204">kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="800a8-204">resourceGroup</span></span>
`resourceGroup()`

<span data-ttu-id="800a8-205">Merhaba geçerli kaynak grubunda temsil eden bir nesne döndürür.</span><span class="sxs-lookup"><span data-stu-id="800a8-205">Returns an object that represents hello current resource group.</span></span> 

### <a name="return-value"></a><span data-ttu-id="800a8-206">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="800a8-206">Return value</span></span>

<span data-ttu-id="800a8-207">Merhaba nesne biçimini izleyen hello döndürülür:</span><span class="sxs-lookup"><span data-stu-id="800a8-207">hello returned object is in hello following format:</span></span>

```json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}",
  "name": "{resourceGroupName}",
  "location": "{resourceGroupLocation}",
  "tags": {
  },
  "properties": {
    "provisioningState": "{status}"
  }
}
```

### <a name="remarks"></a><span data-ttu-id="800a8-208">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="800a8-208">Remarks</span></span>

<span data-ttu-id="800a8-209">Merhaba toocreate kaynaklarında hello resourceGroup işlevinin yaygın bir kullanımdır hello kaynak grubu olarak aynı konumu.</span><span class="sxs-lookup"><span data-stu-id="800a8-209">A common use of hello resourceGroup function is toocreate resources in hello same location as hello resource group.</span></span> <span data-ttu-id="800a8-210">Merhaba aşağıdaki örnek hello kaynak grubu konumu tooassign hello konumu bir web sitesi için kullanır.</span><span class="sxs-lookup"><span data-stu-id="800a8-210">hello following example uses hello resource group location tooassign hello location for a web site.</span></span>

```json
"resources": [
   {
      "apiVersion": "2016-08-01",
      "type": "Microsoft.Web/sites",
      "name": "[parameters('siteName')]",
      "location": "[resourceGroup().location]",
      ...
   }
]
```

### <a name="example"></a><span data-ttu-id="800a8-211">Örnek</span><span class="sxs-lookup"><span data-stu-id="800a8-211">Example</span></span>

<span data-ttu-id="800a8-212">Merhaba aşağıdaki şablonu hello hello kaynak grubunun özelliklerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="800a8-212">hello following template returns hello properties of hello resource group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[resourceGroup()]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="800a8-213">Merhaba önceki örnekte bir nesne biçimini izleyen hello döndürür:</span><span class="sxs-lookup"><span data-stu-id="800a8-213">hello preceding example returns an object in hello following format:</span></span>

```json
{
  "id": "/subscriptions/{subscription-id}/resourceGroups/examplegroup",
  "name": "examplegroup",
  "location": "southcentralus",
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<a id="resourceid" />

## <a name="resourceid"></a><span data-ttu-id="800a8-214">resourceId</span><span class="sxs-lookup"><span data-stu-id="800a8-214">resourceId</span></span>
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

<span data-ttu-id="800a8-215">Bir kaynak benzersiz tanımlayıcısını döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="800a8-215">Returns hello unique identifier of a resource.</span></span> <span data-ttu-id="800a8-216">Merhaba kaynak adı belirsiz veya hello içinde sağlanan olduğunda bu işlevi kullanın aynı şablonu.</span><span class="sxs-lookup"><span data-stu-id="800a8-216">You use this function when hello resource name is ambiguous or not provisioned within hello same template.</span></span> 

### <a name="parameters"></a><span data-ttu-id="800a8-217">Parametreler</span><span class="sxs-lookup"><span data-stu-id="800a8-217">Parameters</span></span>

| <span data-ttu-id="800a8-218">Parametre</span><span class="sxs-lookup"><span data-stu-id="800a8-218">Parameter</span></span> | <span data-ttu-id="800a8-219">Gerekli</span><span class="sxs-lookup"><span data-stu-id="800a8-219">Required</span></span> | <span data-ttu-id="800a8-220">Tür</span><span class="sxs-lookup"><span data-stu-id="800a8-220">Type</span></span> | <span data-ttu-id="800a8-221">Açıklama</span><span class="sxs-lookup"><span data-stu-id="800a8-221">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="800a8-222">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="800a8-222">subscriptionId</span></span> |<span data-ttu-id="800a8-223">Hayır</span><span class="sxs-lookup"><span data-stu-id="800a8-223">No</span></span> |<span data-ttu-id="800a8-224">dize (içinde GUID biçimi)</span><span class="sxs-lookup"><span data-stu-id="800a8-224">string (In GUID format)</span></span> |<span data-ttu-id="800a8-225">Merhaba geçerli abonelik varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="800a8-225">Default value is hello current subscription.</span></span> <span data-ttu-id="800a8-226">Bir kaynağı başka bir abonelik tooretrieve gerektiğinde bu değeri belirtin.</span><span class="sxs-lookup"><span data-stu-id="800a8-226">Specify this value when you need tooretrieve a resource in another subscription.</span></span> |
| <span data-ttu-id="800a8-227">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="800a8-227">resourceGroupName</span></span> |<span data-ttu-id="800a8-228">Hayır</span><span class="sxs-lookup"><span data-stu-id="800a8-228">No</span></span> |<span data-ttu-id="800a8-229">Dize</span><span class="sxs-lookup"><span data-stu-id="800a8-229">string</span></span> |<span data-ttu-id="800a8-230">Geçerli kaynak grubunda varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="800a8-230">Default value is current resource group.</span></span> <span data-ttu-id="800a8-231">Bir kaynağı başka bir kaynak grubunda tooretrieve gerektiğinde bu değeri belirtin.</span><span class="sxs-lookup"><span data-stu-id="800a8-231">Specify this value when you need tooretrieve a resource in another resource group.</span></span> |
| <span data-ttu-id="800a8-232">Kaynak türü</span><span class="sxs-lookup"><span data-stu-id="800a8-232">resourceType</span></span> |<span data-ttu-id="800a8-233">Evet</span><span class="sxs-lookup"><span data-stu-id="800a8-233">Yes</span></span> |<span data-ttu-id="800a8-234">Dize</span><span class="sxs-lookup"><span data-stu-id="800a8-234">string</span></span> |<span data-ttu-id="800a8-235">Kaynak sağlayıcısı ad alanı dahil olmak üzere kaynak türü.</span><span class="sxs-lookup"><span data-stu-id="800a8-235">Type of resource including resource provider namespace.</span></span> |
| <span data-ttu-id="800a8-236">resourceName1</span><span class="sxs-lookup"><span data-stu-id="800a8-236">resourceName1</span></span> |<span data-ttu-id="800a8-237">Evet</span><span class="sxs-lookup"><span data-stu-id="800a8-237">Yes</span></span> |<span data-ttu-id="800a8-238">Dize</span><span class="sxs-lookup"><span data-stu-id="800a8-238">string</span></span> |<span data-ttu-id="800a8-239">Kaynağın adı.</span><span class="sxs-lookup"><span data-stu-id="800a8-239">Name of resource.</span></span> |
| <span data-ttu-id="800a8-240">resourceName2</span><span class="sxs-lookup"><span data-stu-id="800a8-240">resourceName2</span></span> |<span data-ttu-id="800a8-241">Hayır</span><span class="sxs-lookup"><span data-stu-id="800a8-241">No</span></span> |<span data-ttu-id="800a8-242">Dize</span><span class="sxs-lookup"><span data-stu-id="800a8-242">string</span></span> |<span data-ttu-id="800a8-243">Kaynak iç içe yerleştirilmiş ise sonraki kaynak adı kesimi.</span><span class="sxs-lookup"><span data-stu-id="800a8-243">Next resource name segment if resource is nested.</span></span> |

### <a name="return-value"></a><span data-ttu-id="800a8-244">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="800a8-244">Return value</span></span>

<span data-ttu-id="800a8-245">Merhaba tanımlayıcı biçimini izleyen hello verilir:</span><span class="sxs-lookup"><span data-stu-id="800a8-245">hello identifier is returned in hello following format:</span></span>

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a><span data-ttu-id="800a8-246">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="800a8-246">Remarks</span></span>

<span data-ttu-id="800a8-247">Merhaba, belirttiğiniz parametre değerlerini hello kaynak hello olmasına göre değişir hello geçerli dağıtım aynı abonelik ve kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="800a8-247">hello parameter values you specify depend on whether hello resource is in hello same subscription and resource group as hello current deployment.</span></span>

<span data-ttu-id="800a8-248">tooget hello kaynak kimliği hello depolama hesabı için aynı abonelik ve kaynak grubu kullanın:</span><span class="sxs-lookup"><span data-stu-id="800a8-248">tooget hello resource ID for a storage account in hello same subscription and resource group, use:</span></span>

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="800a8-249">tooget hello kaynak kimliği için bir depolama hesabı aynı abonelikte ancak farklı bir kaynak grubu, kullanımı hello:</span><span class="sxs-lookup"><span data-stu-id="800a8-249">tooget hello resource ID for a storage account in hello same subscription but a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="800a8-250">tooget hello kaynak kimliği için farklı bir abonelik ve kaynak grubu, depolama hesabı kullanın:</span><span class="sxs-lookup"><span data-stu-id="800a8-250">tooget hello resource ID for a storage account in a different subscription and resource group, use:</span></span>

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="800a8-251">tooget hello kaynak kimliği farklı bir kaynak grubu, bir veritabanı için kullanın:</span><span class="sxs-lookup"><span data-stu-id="800a8-251">tooget hello resource ID for a database in a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

<span data-ttu-id="800a8-252">Genellikle, toouse bu işlev bir depolama hesabı veya sanal ağ bir alternatif kaynak grubunda kullanırken gerekir.</span><span class="sxs-lookup"><span data-stu-id="800a8-252">Often, you need toouse this function when using a storage account or virtual network in an alternate resource group.</span></span> <span data-ttu-id="800a8-253">Merhaba aşağıdaki örnek bir dış kaynak grubundan bir kaynak kolayca nasıl kullanılabileceğini gösterir:</span><span class="sxs-lookup"><span data-stu-id="800a8-253">hello following example shows how a resource from an external resource group can easily be used:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "virtualNetworkName": {
          "type": "string"
      },
      "virtualNetworkResourceGroup": {
          "type": "string"
      },
      "subnet1Name": {
          "type": "string"
      },
      "nicName": {
          "type": "string"
      }
  },
  "variables": {
      "vnetID": "[resourceId(parameters('virtualNetworkResourceGroup'), 'Microsoft.Network/virtualNetworks', parameters('virtualNetworkName'))]",
      "subnet1Ref": "[concat(variables('vnetID'),'/subnets/', parameters('subnet1Name'))]"
  },
  "resources": [
  {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[parameters('nicName')]",
      "location": "[parameters('location')]",
      "properties": {
          "ipConfigurations": [{
              "name": "ipconfig1",
              "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "subnet": {
                      "id": "[variables('subnet1Ref')]"
                  }
              }
          }]
       }
  }]
}
```

### <a name="example"></a><span data-ttu-id="800a8-254">Örnek</span><span class="sxs-lookup"><span data-stu-id="800a8-254">Example</span></span>

<span data-ttu-id="800a8-255">Merhaba aşağıdaki örnekte bir depolama hesabı için hello kaynak kimliği hello kaynak grubunda döndürür:</span><span class="sxs-lookup"><span data-stu-id="800a8-255">hello following example returns hello resource ID for a storage account in hello resource group:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "sameRGOutput": {
            "value": "[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentRGOutput": {
            "value": "[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentSubOutput": {
            "value": "[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "nestedResourceOutput": {
            "value": "[resourceId('Microsoft.SQL/servers/databases', 'serverName', 'databaseName')]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="800a8-256">Hello hello önceki hello varsayılan değerlerle örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="800a8-256">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="800a8-257">Ad</span><span class="sxs-lookup"><span data-stu-id="800a8-257">Name</span></span> | <span data-ttu-id="800a8-258">Tür</span><span class="sxs-lookup"><span data-stu-id="800a8-258">Type</span></span> | <span data-ttu-id="800a8-259">Değer</span><span class="sxs-lookup"><span data-stu-id="800a8-259">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="800a8-260">sameRGOutput</span><span class="sxs-lookup"><span data-stu-id="800a8-260">sameRGOutput</span></span> | <span data-ttu-id="800a8-261">Dize</span><span class="sxs-lookup"><span data-stu-id="800a8-261">String</span></span> | <span data-ttu-id="800a8-262">/Subscriptions/{Current-Sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="800a8-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="800a8-263">differentRGOutput</span><span class="sxs-lookup"><span data-stu-id="800a8-263">differentRGOutput</span></span> | <span data-ttu-id="800a8-264">Dize</span><span class="sxs-lookup"><span data-stu-id="800a8-264">String</span></span> | <span data-ttu-id="800a8-265">/Subscriptions/{Current-Sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="800a8-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="800a8-266">differentSubOutput</span><span class="sxs-lookup"><span data-stu-id="800a8-266">differentSubOutput</span></span> | <span data-ttu-id="800a8-267">Dize</span><span class="sxs-lookup"><span data-stu-id="800a8-267">String</span></span> | <span data-ttu-id="800a8-268">/Subscriptions/{Different-Sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="800a8-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="800a8-269">nestedResourceOutput</span><span class="sxs-lookup"><span data-stu-id="800a8-269">nestedResourceOutput</span></span> | <span data-ttu-id="800a8-270">Dize</span><span class="sxs-lookup"><span data-stu-id="800a8-270">String</span></span> | <span data-ttu-id="800a8-271">/Subscriptions/{Current-Sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/Servers/ServerName/Databases/databaseName</span><span class="sxs-lookup"><span data-stu-id="800a8-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span></span> |

<a id="subscription" />

## <a name="subscription"></a><span data-ttu-id="800a8-272">aboneliği</span><span class="sxs-lookup"><span data-stu-id="800a8-272">subscription</span></span>
`subscription()`

<span data-ttu-id="800a8-273">Merhaba abonelik hello geçerli dağıtım için ayrıntılarını döndürür.</span><span class="sxs-lookup"><span data-stu-id="800a8-273">Returns details about hello subscription for hello current deployment.</span></span> 

### <a name="return-value"></a><span data-ttu-id="800a8-274">Dönüş değeri</span><span class="sxs-lookup"><span data-stu-id="800a8-274">Return value</span></span>

<span data-ttu-id="800a8-275">Merhaba işlevi biçimini izleyen hello döndürür:</span><span class="sxs-lookup"><span data-stu-id="800a8-275">hello function returns hello following format:</span></span>

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a><span data-ttu-id="800a8-276">Örnek</span><span class="sxs-lookup"><span data-stu-id="800a8-276">Example</span></span>

<span data-ttu-id="800a8-277">Merhaba aşağıdaki örnek hello çıkışları bölümünde çağrılan hello Abonelik işlevi gösterir.</span><span class="sxs-lookup"><span data-stu-id="800a8-277">hello following example shows hello subscription function called in hello outputs section.</span></span> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[subscription()]",
            "type" : "object"
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="800a8-278">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="800a8-278">Next steps</span></span>
* <span data-ttu-id="800a8-279">Bir Azure Resource Manager şablonu hello bölümlerde açıklaması için bkz: [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="800a8-279">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="800a8-280">birden fazla şablon toomerge bkz [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="800a8-280">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="800a8-281">tooiterate belirtilen sayıda kaynak türünü oluştururken bkz [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="800a8-281">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="800a8-282">toodeploy hello şablonu oluşturduğunuz toosee bkz [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="800a8-282">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

