---
title: "Değişiklikleri önlemek için Azure kaynakları kilitleme | Microsoft Docs"
description: "Kullanıcının güncelleştirme veya tüm kullanıcılar ve roller için bir kilit uygulayarak kritik Azure kaynakları silmesini engeller."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 53c57e8f-741c-4026-80e0-f4c02638c98b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 44c87b00f4fc63dbfd45a07d9a8cddc5eaf1a65c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="lock-resources-to-prevent-unexpected-changes"></a><span data-ttu-id="1e9db-103">Beklenmeyen değişiklikleri önlemek için kaynakları kilitleme</span><span class="sxs-lookup"><span data-stu-id="1e9db-103">Lock resources to prevent unexpected changes</span></span> 
<span data-ttu-id="1e9db-104">Yönetici olarak, abonelik, kaynak grubu veya kaynak yanlışlıkla silinmesi ya da kritik kaynaklara değiştirme kuruluşunuzda bulunan diğer kullanıcıların önlemek için kilitleme gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="1e9db-104">As an administrator, you may need to lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="1e9db-105">Kilit düzeyini ayarlayabilirsiniz **CanNotDelete** veya **salt okunur**.</span><span class="sxs-lookup"><span data-stu-id="1e9db-105">You can set the lock level to **CanNotDelete** or **ReadOnly**.</span></span> 

* <span data-ttu-id="1e9db-106">**CanNotDelete** yetkili kullanıcıların, hala okuyun ve kaynak değiştirebilirsiniz, ancak bir kaynağı silemezsiniz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="1e9db-106">**CanNotDelete** means authorized users can still read and modify a resource, but they can't delete the resource.</span></span> 
* <span data-ttu-id="1e9db-107">**Salt okunur** yetkili kullanıcılar, bir kaynak okuyabilir, ancak silebilir veya kaynak güncelleştirme anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="1e9db-107">**ReadOnly** means authorized users can read a resource, but they can't delete or update the resource.</span></span> <span data-ttu-id="1e9db-108">Bu kilit uygulama benzer tüm yetkili kullanıcılar tarafından verilen izinleri kısıtlamak için **okuyucu** rol.</span><span class="sxs-lookup"><span data-stu-id="1e9db-108">Applying this lock is similar to restricting all authorized users to the permissions granted by the **Reader** role.</span></span> 

## <a name="how-locks-are-applied"></a><span data-ttu-id="1e9db-109">Kilitleri nasıl uygulanır</span><span class="sxs-lookup"><span data-stu-id="1e9db-109">How locks are applied</span></span>

<span data-ttu-id="1e9db-110">Bir üst kapsamda kilit uyguladığınızda, kapsamı içindeki tüm kaynakların aynı kilit devralır.</span><span class="sxs-lookup"><span data-stu-id="1e9db-110">When you apply a lock at a parent scope, all resources within that scope inherit the same lock.</span></span> <span data-ttu-id="1e9db-111">Daha sonra eklediğiniz bile kaynakları kilidi üst devralır.</span><span class="sxs-lookup"><span data-stu-id="1e9db-111">Even resources you add later inherit the lock from the parent.</span></span> <span data-ttu-id="1e9db-112">Devralmada en kısıtlayıcı kilidi önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="1e9db-112">The most restrictive lock in the inheritance takes precedence.</span></span>

<span data-ttu-id="1e9db-113">Rol tabanlı erişim denetimi farklı olarak, tüm kullanıcılar ve roller bir kısıtlama uygulamak için yönetim kilitleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="1e9db-113">Unlike role-based access control, you use management locks to apply a restriction across all users and roles.</span></span> <span data-ttu-id="1e9db-114">Kullanıcılar ve roller için izinleri ayarlama bilgi edinmek için [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="1e9db-114">To learn about setting permissions for users and roles, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>

<span data-ttu-id="1e9db-115">Resource Manager kilitleri uygulamak gönderilen işlemleri oluşan yönetim düzeyi gerçekleşen işlemlerine `https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="1e9db-115">Resource Manager locks apply only to operations that happen in the management plane, which consists of operations sent to `https://management.azure.com`.</span></span> <span data-ttu-id="1e9db-116">Kilitler nasıl kaynakları kendi işlevleri gerçekleştirmek kısıtlamaz.</span><span class="sxs-lookup"><span data-stu-id="1e9db-116">The locks do not restrict how resources perform their own functions.</span></span> <span data-ttu-id="1e9db-117">Kaynak kısıtlı değişir, ancak kaynak işlemlerinin sınırlı değildir.</span><span class="sxs-lookup"><span data-stu-id="1e9db-117">Resource changes are restricted, but resource operations are not restricted.</span></span> <span data-ttu-id="1e9db-118">Örneğin, bir SQL veritabanı salt okunur kilit silme veya veritabanı değiştirme engeller, ancak bu, oluşturma, güncelleştirme veya silme verilerden veritabanındaki engellemez.</span><span class="sxs-lookup"><span data-stu-id="1e9db-118">For example, a ReadOnly lock on a SQL Database prevents you from deleting or modifying the database, but it does not prevent you from creating, updating, or deleting data in the database.</span></span> <span data-ttu-id="1e9db-119">Bu işlemler için gönderilmediği için veri hareketlerini izin verilen `https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="1e9db-119">Data transactions are permitted because those operations are not sent to `https://management.azure.com`.</span></span>

<span data-ttu-id="1e9db-120">Uygulama **ReadOnly** gibi görünen bazı işlemler gerçekten ek eylemleri gerektirir okuma olduğundan beklenmeyen sonuçlara yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="1e9db-120">Applying **ReadOnly** can lead to unexpected results because some operations that seem like read operations actually require additional actions.</span></span> <span data-ttu-id="1e9db-121">Örneğin, yerleştirme bir **ReadOnly** kilit bir depolama hesabında anahtarları listeleme tüm kullanıcıları engeller.</span><span class="sxs-lookup"><span data-stu-id="1e9db-121">For example, placing a **ReadOnly** lock on a storage account prevents all users from listing the keys.</span></span> <span data-ttu-id="1e9db-122">Yazma işlemlerini listenin döndürülen anahtarları için kullanılabilir olmadığından anahtarları işlemi bir POST isteği gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="1e9db-122">The list keys operation is handled through a POST request because the returned keys are available for write operations.</span></span> <span data-ttu-id="1e9db-123">Başka bir örneğin yerleştirme bir **ReadOnly** kilit bir uygulama hizmeti kaynağına yazma erişimi bu etkileşimi gerektirmesi nedeniyle kaynak dosyalarını görüntüleme Visual Studio Sunucu Gezgini engeller.</span><span class="sxs-lookup"><span data-stu-id="1e9db-123">For another example, placing a **ReadOnly** lock on an App Service resource prevents Visual Studio Server Explorer from displaying files for the resource because that interaction requires write access.</span></span>

## <a name="who-can-create-or-delete-locks-in-your-organization"></a><span data-ttu-id="1e9db-124">Kimin oluşturmak veya kuruluşunuzdaki kilitleri silmek mi</span><span class="sxs-lookup"><span data-stu-id="1e9db-124">Who can create or delete locks in your organization</span></span>
<span data-ttu-id="1e9db-125">Oluşturmak veya yönetim kilitleri silmek için erişimi olmalıdır `Microsoft.Authorization/*` veya `Microsoft.Authorization/locks/*` eylemler.</span><span class="sxs-lookup"><span data-stu-id="1e9db-125">To create or delete management locks, you must have access to `Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="1e9db-126">Yerleşik roller, yalnızca **sahibi** ve **kullanıcı erişimi Yöneticisi** bu eylemleri verilir.</span><span class="sxs-lookup"><span data-stu-id="1e9db-126">Of the built-in roles, only **Owner** and **User Access Administrator** are granted those actions.</span></span>

## <a name="portal"></a><span data-ttu-id="1e9db-127">Portal</span><span class="sxs-lookup"><span data-stu-id="1e9db-127">Portal</span></span>
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a><span data-ttu-id="1e9db-128">Şablon</span><span class="sxs-lookup"><span data-stu-id="1e9db-128">Template</span></span>
<span data-ttu-id="1e9db-129">Aşağıdaki örnek, bir depolama hesabı üzerinde bir kilit oluşturan bir şablonu gösterir.</span><span class="sxs-lookup"><span data-stu-id="1e9db-129">The following example shows a template that creates a lock on a storage account.</span></span> <span data-ttu-id="1e9db-130">Depolama hesabı kilidi uygulanacağı parametre olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="1e9db-130">The storage account on which to apply the lock is provided as a parameter.</span></span> <span data-ttu-id="1e9db-131">Kilit adı ile kaynak adı birleştirerek oluşturulan **/Microsoft.Authorization/** ve bu durumda kilit adı **myLock**.</span><span class="sxs-lookup"><span data-stu-id="1e9db-131">The name of the lock is created by concatenating the resource name with **/Microsoft.Authorization/** and the name of the lock, in this case **myLock**.</span></span>

<span data-ttu-id="1e9db-132">Sağlanan kaynak türü için belirli türüdür.</span><span class="sxs-lookup"><span data-stu-id="1e9db-132">The type provided is specific to the resource type.</span></span> <span data-ttu-id="1e9db-133">Depolama için türü "Microsoft.Storage/storageaccounts/providers/locks" olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1e9db-133">For storage, set the type to "Microsoft.Storage/storageaccounts/providers/locks".</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "lockedResource": {
          "type": "string"
        }
      },
      "resources": [
        {
          "name": "[concat(parameters('lockedResource'), '/Microsoft.Authorization/myLock')]",
          "type": "Microsoft.Storage/storageAccounts/providers/locks",
          "apiVersion": "2015-01-01",
          "properties": {
            "level": "CannotDelete"
          }
        }
      ]
    }

## <a name="powershell"></a><span data-ttu-id="1e9db-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e9db-134">PowerShell</span></span>
<span data-ttu-id="1e9db-135">Kilit kullanarak kaynakları Azure PowerShell ile dağıtılan [yeni AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) komutu.</span><span class="sxs-lookup"><span data-stu-id="1e9db-135">You lock deployed resources with Azure PowerShell by using the [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) command.</span></span>

<span data-ttu-id="1e9db-136">Bir kaynağı kilitlemek için adını kaynak, kaynak türü ve kaynak grubu adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="1e9db-136">To lock a resource, provide the name of the resource, its resource type, and its resource group name.</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="1e9db-137">Bir kaynak grubu kilitlemek için kaynak grubu adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="1e9db-137">To lock a resource group, provide the name of the resource group.</span></span>

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="1e9db-138">Kilit hakkında bilgi almak için kullanmak [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span><span class="sxs-lookup"><span data-stu-id="1e9db-138">To get information about a lock, use [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span></span> <span data-ttu-id="1e9db-139">Aboneliğinizdeki tüm kilitler almak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="1e9db-139">To get all the locks in your subscription, use:</span></span>

```powershell
Get-AzureRmResourceLock
```

<span data-ttu-id="1e9db-140">Bir kaynak için tüm kilitleri almak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="1e9db-140">To get all locks for a resource, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="1e9db-141">Bir kaynak grubu için tüm kilitleri almak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="1e9db-141">To get all locks for a resource group, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="1e9db-142">Azure PowerShell diğer komutları gibi çalışma kilitlerini sağlar [kümesi AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) kilit, güncelleştirmeye ve [Kaldır AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) kilit silmek için.</span><span class="sxs-lookup"><span data-stu-id="1e9db-142">Azure PowerShell provides other commands for working locks, such as [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) to update a lock, and [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) to delete a lock.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="1e9db-143">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1e9db-143">Azure CLI</span></span>

<span data-ttu-id="1e9db-144">Kilit kullanarak Azure CLI kaynaklarla dağıtılan [az kilit oluşturmak](/cli/azure/lock#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="1e9db-144">You lock deployed resources with Azure CLI by using the [az lock create](/cli/azure/lock#create) command.</span></span>

<span data-ttu-id="1e9db-145">Bir kaynağı kilitlemek için adını kaynak, kaynak türü ve kaynak grubu adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="1e9db-145">To lock a resource, provide the name of the resource, its resource type, and its resource group name.</span></span>

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

<span data-ttu-id="1e9db-146">Bir kaynak grubu kilitlemek için kaynak grubu adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="1e9db-146">To lock a resource group, provide the name of the resource group.</span></span>

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

<span data-ttu-id="1e9db-147">Kilit hakkında bilgi almak için kullanmak [az kilit listesi](/cli/azure/lock#list).</span><span class="sxs-lookup"><span data-stu-id="1e9db-147">To get information about a lock, use [az lock list](/cli/azure/lock#list).</span></span> <span data-ttu-id="1e9db-148">Aboneliğinizdeki tüm kilitler almak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="1e9db-148">To get all the locks in your subscription, use:</span></span>

```azurecli
az lock list
```

<span data-ttu-id="1e9db-149">Bir kaynak için tüm kilitleri almak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="1e9db-149">To get all locks for a resource, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

<span data-ttu-id="1e9db-150">Bir kaynak grubu için tüm kilitleri almak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="1e9db-150">To get all locks for a resource group, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup
```

<span data-ttu-id="1e9db-151">Azure CLI diğer komutları gibi çalışma kilitlerini sağlar [az kilit güncelleştirme](/cli/azure/lock#update) kilit, güncelleştirmeye ve [az kilit silmek](/cli/azure/lock#delete) kilit silmek için.</span><span class="sxs-lookup"><span data-stu-id="1e9db-151">Azure CLI provides other commands for working locks, such as [az lock update](/cli/azure/lock#update) to update a lock, and [az lock delete](/cli/azure/lock#delete) to delete a lock.</span></span>

## <a name="rest-api"></a><span data-ttu-id="1e9db-152">REST API</span><span class="sxs-lookup"><span data-stu-id="1e9db-152">REST API</span></span>
<span data-ttu-id="1e9db-153">Dağıtılan kaynaklarla kilitleyebilirsiniz [yönetim kilitleri için REST API](https://docs.microsoft.com/rest/api/resources/managementlocks).</span><span class="sxs-lookup"><span data-stu-id="1e9db-153">You can lock deployed resources with the [REST API for management locks](https://docs.microsoft.com/rest/api/resources/managementlocks).</span></span> <span data-ttu-id="1e9db-154">REST API oluşturmak ve kilitleri silin ve varolan kilitler hakkında bilgi almak etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="1e9db-154">The REST API enables you to create and delete locks, and retrieve information about existing locks.</span></span>

<span data-ttu-id="1e9db-155">Kilit oluşturmak için çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="1e9db-155">To create a lock, run:</span></span>

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

<span data-ttu-id="1e9db-156">Kapsamı bir abonelik, kaynak grubu veya kaynak olabilir.</span><span class="sxs-lookup"><span data-stu-id="1e9db-156">The scope could be a subscription, resource group, or resource.</span></span> <span data-ttu-id="1e9db-157">Kilit-ne olursa olsun kilidi aramak istediğiniz addır.</span><span class="sxs-lookup"><span data-stu-id="1e9db-157">The lock-name is whatever you want to call the lock.</span></span> <span data-ttu-id="1e9db-158">API sürümü için kullanmak **2015-01-01**.</span><span class="sxs-lookup"><span data-stu-id="1e9db-158">For api-version, use **2015-01-01**.</span></span>

<span data-ttu-id="1e9db-159">İstekte kilidi özelliklerini belirten bir JSON nesnesi içerir.</span><span class="sxs-lookup"><span data-stu-id="1e9db-159">In the request, include a JSON object that specifies the properties for the lock.</span></span>

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a><span data-ttu-id="1e9db-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1e9db-160">Next steps</span></span>
* <span data-ttu-id="1e9db-161">Kaynak kilitleri ile çalışma hakkında daha fazla bilgi için bkz: [kilit aşağı bilgisayarınızı Azure kaynakları](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span><span class="sxs-lookup"><span data-stu-id="1e9db-161">For more information about working with resource locks, see [Lock Down Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span></span>
* <span data-ttu-id="1e9db-162">Mantıksal olarak kaynaklarınızı düzenleme hakkında bilgi edinmek için [etiketleri kullanarak kaynaklarınızı düzenleme](resource-group-using-tags.md)</span><span class="sxs-lookup"><span data-stu-id="1e9db-162">To learn about logically organizing your resources, see [Using tags to organize your resources](resource-group-using-tags.md)</span></span>
* <span data-ttu-id="1e9db-163">Kaynağın bulunduğu hangi kaynak grubunu değiştirmek için bkz: [kaynakları yeni kaynak grubuna taşıma](resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="1e9db-163">To change which resource group a resource resides in, see [Move resources to new resource group](resource-group-move-resources.md)</span></span>
* <span data-ttu-id="1e9db-164">Özelleştirilmiş ilkeler aboneliğinizle arasında kısıtlamaları ve kuralları uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e9db-164">You can apply restrictions and conventions across your subscription with customized policies.</span></span> <span data-ttu-id="1e9db-165">Daha fazla bilgi için bkz. [Kaynakları yönetmek ve erişimi denetlemek için İlke kullanma](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="1e9db-165">For more information, see [Use Policy to manage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="1e9db-166">Kuruluşların abonelikleri etkili bir şekilde yönetmek için Resource Manager'ı nasıl kullanabileceği hakkında yönergeler için bkz. [Azure kurumsal iskelesi: öngörücü abonelik idaresi](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="1e9db-166">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

