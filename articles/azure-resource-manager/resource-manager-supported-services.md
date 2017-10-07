---
title: "aaaAzure kaynak sağlayıcıları ve kaynak türleri | Microsoft Docs"
description: "Resource Manager, şemalar ve kullanılabilir API sürümleri desteği hello kaynak sağlayıcıları ve hello kaynakları barındırabilir hello bölgeler açıklar."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 3c7a6fe4-371a-40da-9ebe-b574f583305b
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 23db1d3808a20166f3b44ec801e1bcc46fbb9bd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-providers-and-types"></a><span data-ttu-id="bc9a8-103">Kaynak sağlayıcıları ve türleri</span><span class="sxs-lookup"><span data-stu-id="bc9a8-103">Resource providers and types</span></span>

<span data-ttu-id="bc9a8-104">Kaynakları dağıtırken sık tooretrieve hello kaynak sağlayıcıları ve türler hakkında bilgi gerekir.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-104">When deploying resources, you frequently need tooretrieve information about hello resource providers and types.</span></span> <span data-ttu-id="bc9a8-105">Bu makalede, öğrenin:</span><span class="sxs-lookup"><span data-stu-id="bc9a8-105">In this article, you learn to:</span></span>

* <span data-ttu-id="bc9a8-106">Tüm kaynak sağlayıcıları Azure içinde görüntüleme</span><span class="sxs-lookup"><span data-stu-id="bc9a8-106">View all resource providers in Azure</span></span>
* <span data-ttu-id="bc9a8-107">Bir kaynak sağlayıcısının kayıt durumunu denetle</span><span class="sxs-lookup"><span data-stu-id="bc9a8-107">Check registration status of a resource provider</span></span>
* <span data-ttu-id="bc9a8-108">Kayıt kaynak sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="bc9a8-108">Register a resource provider</span></span>
* <span data-ttu-id="bc9a8-109">Bir kaynak sağlayıcısı için Görünüm kaynak türü</span><span class="sxs-lookup"><span data-stu-id="bc9a8-109">View resource types for a resource provider</span></span>
* <span data-ttu-id="bc9a8-110">Bir kaynak türü için geçerli konumlar görünümü</span><span class="sxs-lookup"><span data-stu-id="bc9a8-110">View valid locations for a resource type</span></span>
* <span data-ttu-id="bc9a8-111">Bir kaynak türü için geçerli API sürümleri görüntüle</span><span class="sxs-lookup"><span data-stu-id="bc9a8-111">View valid API versions for a resource type</span></span>

<span data-ttu-id="bc9a8-112">Bu adımları hello portal, PowerShell veya Azure CLI aracılığıyla gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-112">You can perform these steps through hello portal, PowerShell, or Azure CLI.</span></span>

## <a name="powershell"></a><span data-ttu-id="bc9a8-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc9a8-113">PowerShell</span></span>

<span data-ttu-id="bc9a8-114">toosee Azure ve hello kayıt durumu, aboneliğiniz için tüm kaynak sağlayıcıları kullanın:</span><span class="sxs-lookup"><span data-stu-id="bc9a8-114">toosee all resource providers in Azure, and hello registration status for your subscription, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

<span data-ttu-id="bc9a8-115">Hangi için benzer sonuçlar getirir:</span><span class="sxs-lookup"><span data-stu-id="bc9a8-115">Which returns results similar to:</span></span>

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="bc9a8-116">Bir kaynak sağlayıcısı kaydediliyor abonelik toowork hello kaynak sağlayıcısı ile yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-116">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="bc9a8-117">Merhaba kaydı için her zaman hello abonelik kapsamıdır.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-117">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="bc9a8-118">Varsayılan olarak, birçok kaynak sağlayıcısı otomatik olarak kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-118">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="bc9a8-119">Ancak, gerekebilir toomanually bazı kaynak sağlayıcılarını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-119">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="bc9a8-120">bir kaynak sağlayıcısı tooregister, izni tooperform hello olmalıdır `/register/action` hello kaynak sağlayıcısı için işlem.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-120">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="bc9a8-121">Bu işlem, hello katkıda bulunan ve sahibi rolleri dahil edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-121">This operation is included in hello Contributor and Owner roles.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="bc9a8-122">Hangi için benzer sonuçlar getirir:</span><span class="sxs-lookup"><span data-stu-id="bc9a8-122">Which returns results similar to:</span></span>

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

<span data-ttu-id="bc9a8-123">Aboneliğinizdeki kaynak türleri bu kaynak Sağlayıcısı'ndan hala varsa, bir kaynak Sağlayıcısı kaydı silinemiyor.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-123">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="bc9a8-124">belirli kaynak sağlayıcı, kullanım için toosee bilgileri:</span><span class="sxs-lookup"><span data-stu-id="bc9a8-124">toosee information for a particular resource provider, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="bc9a8-125">Hangi için benzer sonuçlar getirir:</span><span class="sxs-lookup"><span data-stu-id="bc9a8-125">Which returns results similar to:</span></span>

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

<span data-ttu-id="bc9a8-126">toosee hello kaynak türleri için bir kaynak sağlayıcısı kullanın:</span><span class="sxs-lookup"><span data-stu-id="bc9a8-126">toosee hello resource types for a resource provider, use:</span></span>

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

<span data-ttu-id="bc9a8-127">Hangi döndürür:</span><span class="sxs-lookup"><span data-stu-id="bc9a8-127">Which returns:</span></span>

```powershell
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="bc9a8-128">Merhaba API sürümü hello kaynak sağlayıcısı tarafından yayımlanan REST API işlemleri tooa sürümüne karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-128">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="bc9a8-129">Bir kaynak sağlayıcısı yeni özellikleri etkinleştirir gibi hello REST API yeni bir sürümünü yayımlar.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-129">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> 

<span data-ttu-id="bc9a8-130">tooget hello kullanılabilir API sürümleri için bir kaynak türünü kullanın:</span><span class="sxs-lookup"><span data-stu-id="bc9a8-130">tooget hello available API versions for a resource type, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

<span data-ttu-id="bc9a8-131">Hangi döndürür:</span><span class="sxs-lookup"><span data-stu-id="bc9a8-131">Which returns:</span></span>

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="bc9a8-132">Kaynak Yöneticisi tüm bölgelerde desteklenir, ancak hello kaynakları dağıttığınız tüm bölgelerde desteklenmiyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-132">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="bc9a8-133">Ayrıca, hello kaynak destekleyen bazı bölgelerde kullanmasını önlemek aboneliğinizi sınırlamaları olabilir.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-133">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> 

<span data-ttu-id="bc9a8-134">bir kaynak türü için tooget desteklenen hello konumlarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-134">tooget hello supported locations for a resource type, use.</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

<span data-ttu-id="bc9a8-135">Hangi döndürür:</span><span class="sxs-lookup"><span data-stu-id="bc9a8-135">Which returns:</span></span>

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a><span data-ttu-id="bc9a8-136">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bc9a8-136">Azure CLI</span></span>
<span data-ttu-id="bc9a8-137">toosee Azure ve hello kayıt durumu, aboneliğiniz için tüm kaynak sağlayıcıları kullanın:</span><span class="sxs-lookup"><span data-stu-id="bc9a8-137">toosee all resource providers in Azure, and hello registration status for your subscription, use:</span></span>

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

<span data-ttu-id="bc9a8-138">Hangi için benzer sonuçlar getirir:</span><span class="sxs-lookup"><span data-stu-id="bc9a8-138">Which returns results similar to:</span></span>

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="bc9a8-139">Bir kaynak sağlayıcısı kaydediliyor abonelik toowork hello kaynak sağlayıcısı ile yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-139">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="bc9a8-140">Merhaba kaydı için her zaman hello abonelik kapsamıdır.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-140">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="bc9a8-141">Varsayılan olarak, birçok kaynak sağlayıcısı otomatik olarak kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-141">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="bc9a8-142">Ancak, gerekebilir toomanually bazı kaynak sağlayıcılarını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-142">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="bc9a8-143">bir kaynak sağlayıcısı tooregister, izni tooperform hello olmalıdır `/register/action` hello kaynak sağlayıcısı için işlem.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-143">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="bc9a8-144">Bu işlem, hello katkıda bulunan ve sahibi rolleri dahil edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-144">This operation is included in hello Contributor and Owner roles.</span></span>

```azurecli
az provider register --namespace Microsoft.Batch
```

<span data-ttu-id="bc9a8-145">Devam eden, bu kayıt bir ileti döndürür.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-145">Which returns a message that registration is on-going.</span></span>

<span data-ttu-id="bc9a8-146">Aboneliğinizdeki kaynak türleri bu kaynak Sağlayıcısı'ndan hala varsa, bir kaynak Sağlayıcısı kaydı silinemiyor.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-146">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="bc9a8-147">belirli kaynak sağlayıcı, kullanım için toosee bilgileri:</span><span class="sxs-lookup"><span data-stu-id="bc9a8-147">toosee information for a particular resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch
```

<span data-ttu-id="bc9a8-148">Hangi için benzer sonuçlar getirir:</span><span class="sxs-lookup"><span data-stu-id="bc9a8-148">Which returns results similar to:</span></span>

```azurecli
{
    "id": "/subscriptions/####-####/providers/Microsoft.Batch",
    "namespace": "Microsoft.Batch",
    "registrationsState": "Registering",
    "resourceTypes:" [
        ...
    ]
}
```

<span data-ttu-id="bc9a8-149">toosee hello kaynak türleri için bir kaynak sağlayıcısı kullanın:</span><span class="sxs-lookup"><span data-stu-id="bc9a8-149">toosee hello resource types for a resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

<span data-ttu-id="bc9a8-150">Hangi döndürür:</span><span class="sxs-lookup"><span data-stu-id="bc9a8-150">Which returns:</span></span>

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="bc9a8-151">Merhaba API sürümü hello kaynak sağlayıcısı tarafından yayımlanan REST API işlemleri tooa sürümüne karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-151">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="bc9a8-152">Bir kaynak sağlayıcısı yeni özellikleri etkinleştirir gibi hello REST API yeni bir sürümünü yayımlar.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-152">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> 

<span data-ttu-id="bc9a8-153">tooget hello kullanılabilir API sürümleri için bir kaynak türünü kullanın:</span><span class="sxs-lookup"><span data-stu-id="bc9a8-153">tooget hello available API versions for a resource type, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

<span data-ttu-id="bc9a8-154">Hangi döndürür:</span><span class="sxs-lookup"><span data-stu-id="bc9a8-154">Which returns:</span></span>

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="bc9a8-155">Kaynak Yöneticisi tüm bölgelerde desteklenir, ancak hello kaynakları dağıttığınız tüm bölgelerde desteklenmiyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-155">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="bc9a8-156">Ayrıca, hello kaynak destekleyen bazı bölgelerde kullanmasını önlemek aboneliğinizi sınırlamaları olabilir.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-156">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> 

<span data-ttu-id="bc9a8-157">bir kaynak türü için tooget desteklenen hello konumlarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-157">tooget hello supported locations for a resource type, use.</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

<span data-ttu-id="bc9a8-158">Hangi döndürür:</span><span class="sxs-lookup"><span data-stu-id="bc9a8-158">Which returns:</span></span>

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a><span data-ttu-id="bc9a8-159">Portal</span><span class="sxs-lookup"><span data-stu-id="bc9a8-159">Portal</span></span>

<span data-ttu-id="bc9a8-160">Azure ve hello kayıt durumu, aboneliğiniz için tüm kaynak sağlayıcıları toosee seçin **abonelikleri**.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-160">toosee all resource providers in Azure, and hello registration status for your subscription, select **Subscriptions**.</span></span>

![Abonelik seç](./media/resource-manager-supported-services/select-subscriptions.png)

<span data-ttu-id="bc9a8-162">Merhaba abonelik tooview seçin.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-162">Choose hello subscription tooview.</span></span>

![Abonelik belirtin](./media/resource-manager-supported-services/subscription.png)

<span data-ttu-id="bc9a8-164">Seçin **kaynak sağlayıcıları** ve kullanılabilir kaynak sağlayıcıları hello listesini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-164">Select **Resource providers** and view hello list of available resource providers.</span></span>

![kaynak sağlayıcıları göster](./media/resource-manager-supported-services/show-resource-providers.png)

<span data-ttu-id="bc9a8-166">Bir kaynak sağlayıcısı kaydediliyor abonelik toowork hello kaynak sağlayıcısı ile yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-166">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="bc9a8-167">Merhaba kaydı için her zaman hello abonelik kapsamıdır.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-167">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="bc9a8-168">Varsayılan olarak, birçok kaynak sağlayıcısı otomatik olarak kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-168">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="bc9a8-169">Ancak, gerekebilir toomanually bazı kaynak sağlayıcılarını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-169">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="bc9a8-170">bir kaynak sağlayıcısı tooregister, izni tooperform hello olmalıdır `/register/action` hello kaynak sağlayıcısı için işlem.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-170">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="bc9a8-171">Bu işlem, hello katkıda bulunan ve sahibi rolleri dahil edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-171">This operation is included in hello Contributor and Owner roles.</span></span> <span data-ttu-id="bc9a8-172">tooregister bir kaynak sağlayıcısı seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-172">tooregister a resource provider, select **Register**.</span></span>

![Kayıt kaynak sağlayıcısı](./media/resource-manager-supported-services/register-provider.png)

<span data-ttu-id="bc9a8-174">Aboneliğinizdeki kaynak türleri bu kaynak Sağlayıcısı'ndan hala varsa, bir kaynak Sağlayıcısı kaydı silinemiyor.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-174">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="bc9a8-175">belirli kaynak sağlayıcısı toosee bilgilerini seçme **daha fazla hizmet**.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-175">toosee information for a particular resource provider, select **More services**.</span></span>

![Daha fazla hizmet seçin](./media/resource-manager-supported-services/more-services.png)

<span data-ttu-id="bc9a8-177">Arama **kaynak Gezgini** ve hello kullanılabilir seçeneklerden birini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-177">Search for **Resource Explorer** and select it from hello available options.</span></span>

![Kaynak Gezgini seçin](./media/resource-manager-supported-services/select-resource-explorer.png)

<span data-ttu-id="bc9a8-179">Seçin **sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-179">Select **Providers**.</span></span>

![Sağlayıcı seçin](./media/resource-manager-supported-services/select-providers.png)

<span data-ttu-id="bc9a8-181">Select hello kaynak sağlayıcısı ve kaynak tooview istediğinizi yazın.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-181">Select hello resource provider and resource type that you want tooview.</span></span>

![Kaynak türü seçin](./media/resource-manager-supported-services/select-resource-type.png)

<span data-ttu-id="bc9a8-183">Kaynak Yöneticisi tüm bölgelerde desteklenir, ancak hello kaynakları dağıttığınız tüm bölgelerde desteklenmiyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-183">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="bc9a8-184">Ayrıca, hello kaynak destekleyen bazı bölgelerde kullanmasını önlemek aboneliğinizi sınırlamaları olabilir.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-184">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> <span data-ttu-id="bc9a8-185">Merhaba kaynak Gezgini hello kaynak türü için geçerli konumlarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-185">hello resource explorer displays valid locations for hello resource type.</span></span>

![Konumları göster](./media/resource-manager-supported-services/show-locations.png)

<span data-ttu-id="bc9a8-187">Merhaba API sürümü hello kaynak sağlayıcısı tarafından yayımlanan REST API işlemleri tooa sürümüne karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-187">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="bc9a8-188">Bir kaynak sağlayıcısı yeni özellikleri etkinleştirir gibi hello REST API yeni bir sürümünü yayımlar.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-188">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> <span data-ttu-id="bc9a8-189">Merhaba kaynak Gezgini hello kaynak türü için geçerli API sürümü görüntüler.</span><span class="sxs-lookup"><span data-stu-id="bc9a8-189">hello resource explorer displays valid API versions for hello resource type.</span></span>

![API sürümleri göster](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a><span data-ttu-id="bc9a8-191">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bc9a8-191">Next steps</span></span>
* <span data-ttu-id="bc9a8-192">Resource Manager şablonları oluşturma hakkında daha fazla toolearn bkz [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="bc9a8-192">toolearn about creating Resource Manager templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="bc9a8-193">Kaynakları dağıtma hakkında toolearn bkz [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="bc9a8-193">toolearn about deploying resources, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="bc9a8-194">bir kaynak sağlayıcısı için tooview hello bkz [Azure REST API](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="bc9a8-194">tooview hello operations for a resource provider, see [Azure REST API](/rest/api/).</span></span>

