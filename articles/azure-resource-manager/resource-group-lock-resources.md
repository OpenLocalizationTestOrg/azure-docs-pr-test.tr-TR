---
title: "aaaLock Azure kaynaklarını tooprevent değişiklikleri | Microsoft Docs"
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
ms.openlocfilehash: 1f0d8911b2b129069bd2f01a9a4ec0a3cf700118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="lock-resources-tooprevent-unexpected-changes"></a><span data-ttu-id="4a156-103">Kilitleme kaynakları tooprevent beklenmeyen değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="4a156-103">Lock resources tooprevent unexpected changes</span></span> 
<span data-ttu-id="4a156-104">Yönetici olarak, yanlışlıkla silinmesi ya da kritik kaynaklara değiştirme kuruluşunuzdaki diğer kullanıcıların toolock bir abonelik, kaynak grubu veya kaynak tooprevent gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="4a156-104">As an administrator, you may need toolock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="4a156-105">Merhaba kilit düzeyi çok ayarlayabilirsiniz**CanNotDelete** veya **salt okunur**.</span><span class="sxs-lookup"><span data-stu-id="4a156-105">You can set hello lock level too**CanNotDelete** or **ReadOnly**.</span></span> 

* <span data-ttu-id="4a156-106">**CanNotDelete** yetkili kullanıcıların, hala okuyun ve kaynak değiştirebilirsiniz, ancak hello kaynağı silemezsiniz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="4a156-106">**CanNotDelete** means authorized users can still read and modify a resource, but they can't delete hello resource.</span></span> 
* <span data-ttu-id="4a156-107">**Salt okunur** yetkili kullanıcılar, bir kaynak okuyabilir, ancak delete veya update hello kaynak anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="4a156-107">**ReadOnly** means authorized users can read a resource, but they can't delete or update hello resource.</span></span> <span data-ttu-id="4a156-108">Bu kilit uygulama olan tüm yetkili kullanıcıların toohello hello tarafından izinler benzer toorestricting **okuyucu** rol.</span><span class="sxs-lookup"><span data-stu-id="4a156-108">Applying this lock is similar toorestricting all authorized users toohello permissions granted by hello **Reader** role.</span></span> 

## <a name="how-locks-are-applied"></a><span data-ttu-id="4a156-109">Kilitleri nasıl uygulanır</span><span class="sxs-lookup"><span data-stu-id="4a156-109">How locks are applied</span></span>

<span data-ttu-id="4a156-110">Bir üst kapsamda kilit uyguladığınızda, kapsamı içindeki tüm kaynakların hello devral aynı kilitle.</span><span class="sxs-lookup"><span data-stu-id="4a156-110">When you apply a lock at a parent scope, all resources within that scope inherit hello same lock.</span></span> <span data-ttu-id="4a156-111">Hatta kaynak daha sonra Ekle hello kilit hello üst öğeden devralır.</span><span class="sxs-lookup"><span data-stu-id="4a156-111">Even resources you add later inherit hello lock from hello parent.</span></span> <span data-ttu-id="4a156-112">Merhaba en kısıtlayıcı kilit hello Devralmada önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="4a156-112">hello most restrictive lock in hello inheritance takes precedence.</span></span>

<span data-ttu-id="4a156-113">Rol tabanlı erişim denetimi farklı olarak, tüm kullanıcılar ve roller yönetim kilitleri tooapply bir kısıtlama kullanın.</span><span class="sxs-lookup"><span data-stu-id="4a156-113">Unlike role-based access control, you use management locks tooapply a restriction across all users and roles.</span></span> <span data-ttu-id="4a156-114">Kullanıcılar ve roller için izinleri ayarlama hakkında toolearn bkz [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="4a156-114">toolearn about setting permissions for users and roles, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>

<span data-ttu-id="4a156-115">Resource Manager kilitleri uygulamak çok gönderilen işlemden oluşur hello Yönetim düzeyi içinde gerçekleşen toooperations`https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="4a156-115">Resource Manager locks apply only toooperations that happen in hello management plane, which consists of operations sent too`https://management.azure.com`.</span></span> <span data-ttu-id="4a156-116">Merhaba kilitleri nasıl kaynakları kendi işlevleri gerçekleştirmek kısıtlamaz.</span><span class="sxs-lookup"><span data-stu-id="4a156-116">hello locks do not restrict how resources perform their own functions.</span></span> <span data-ttu-id="4a156-117">Kaynak kısıtlı değişir, ancak kaynak işlemlerinin sınırlı değildir.</span><span class="sxs-lookup"><span data-stu-id="4a156-117">Resource changes are restricted, but resource operations are not restricted.</span></span> <span data-ttu-id="4a156-118">Örneğin, bir SQL veritabanında salt okunur kilit silmesini engeller veya hello veritabanı, ancak değiştirme, oluşturma, güncelleştirme ya da hello veritabanındaki verileri silme engellemez.</span><span class="sxs-lookup"><span data-stu-id="4a156-118">For example, a ReadOnly lock on a SQL Database prevents you from deleting or modifying hello database, but it does not prevent you from creating, updating, or deleting data in hello database.</span></span> <span data-ttu-id="4a156-119">Bu işlemler çok gönderilmediği için veri hareketlerini izin verilen`https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="4a156-119">Data transactions are permitted because those operations are not sent too`https://management.azure.com`.</span></span>

<span data-ttu-id="4a156-120">Uygulama **ReadOnly** gibi görünen bazı işlemler gerçekten ek eylemleri gerektirir okuma olduğundan toounexpected sonuçları yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="4a156-120">Applying **ReadOnly** can lead toounexpected results because some operations that seem like read operations actually require additional actions.</span></span> <span data-ttu-id="4a156-121">Örneğin, yerleştirme bir **ReadOnly** bir depolama hesabı üzerinde kilit hello anahtarları listeleme tüm kullanıcıları engeller.</span><span class="sxs-lookup"><span data-stu-id="4a156-121">For example, placing a **ReadOnly** lock on a storage account prevents all users from listing hello keys.</span></span> <span data-ttu-id="4a156-122">yazma işlemlerini hello listesi Hello anahtarların döndürdüğünden anahtarları işlemi bir POST isteği gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="4a156-122">hello list keys operation is handled through a POST request because hello returned keys are available for write operations.</span></span> <span data-ttu-id="4a156-123">Başka bir örneğin yerleştirme bir **ReadOnly** kilit bir uygulama hizmeti kaynağına yazma erişimi bu etkileşimi gerektirmesi nedeniyle hello kaynak dosyalarını görüntüleme Visual Studio Sunucu Gezgini engeller.</span><span class="sxs-lookup"><span data-stu-id="4a156-123">For another example, placing a **ReadOnly** lock on an App Service resource prevents Visual Studio Server Explorer from displaying files for hello resource because that interaction requires write access.</span></span>

## <a name="who-can-create-or-delete-locks-in-your-organization"></a><span data-ttu-id="4a156-124">Kimin oluşturmak veya kuruluşunuzdaki kilitleri silmek mi</span><span class="sxs-lookup"><span data-stu-id="4a156-124">Who can create or delete locks in your organization</span></span>
<span data-ttu-id="4a156-125">Yönetim kilit toocreate ya da delete gerekir erişiminiz çok`Microsoft.Authorization/*` veya `Microsoft.Authorization/locks/*` eylemler.</span><span class="sxs-lookup"><span data-stu-id="4a156-125">toocreate or delete management locks, you must have access too`Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="4a156-126">Merhaba yerleşik roller, yalnızca **sahibi** ve **kullanıcı erişimi Yöneticisi** bu eylemleri verilir.</span><span class="sxs-lookup"><span data-stu-id="4a156-126">Of hello built-in roles, only **Owner** and **User Access Administrator** are granted those actions.</span></span>

## <a name="portal"></a><span data-ttu-id="4a156-127">Portal</span><span class="sxs-lookup"><span data-stu-id="4a156-127">Portal</span></span>
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a><span data-ttu-id="4a156-128">Şablon</span><span class="sxs-lookup"><span data-stu-id="4a156-128">Template</span></span>
<span data-ttu-id="4a156-129">Hello aşağıdaki örnekte bir depolama hesabı üzerinde bir kilit oluşturan bir şablonu gösterir.</span><span class="sxs-lookup"><span data-stu-id="4a156-129">hello following example shows a template that creates a lock on a storage account.</span></span> <span data-ttu-id="4a156-130">Merhaba depolama hesabı üzerinde hangi tooapply hello kilit parametre olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="4a156-130">hello storage account on which tooapply hello lock is provided as a parameter.</span></span> <span data-ttu-id="4a156-131">Merhaba hello kilit adı hello kaynak adı ile birleştirerek oluşturulan **/Microsoft.Authorization/** ve bu durumda hello hello kilit adı **myLock**.</span><span class="sxs-lookup"><span data-stu-id="4a156-131">hello name of hello lock is created by concatenating hello resource name with **/Microsoft.Authorization/** and hello name of hello lock, in this case **myLock**.</span></span>

<span data-ttu-id="4a156-132">sağlanan hello türü belirli toohello kaynak türüdür.</span><span class="sxs-lookup"><span data-stu-id="4a156-132">hello type provided is specific toohello resource type.</span></span> <span data-ttu-id="4a156-133">Depolama alanı için hello türü too"Microsoft.Storage/storageaccounts/providers/locks"ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4a156-133">For storage, set hello type too"Microsoft.Storage/storageaccounts/providers/locks".</span></span>

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

## <a name="powershell"></a><span data-ttu-id="4a156-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4a156-134">PowerShell</span></span>
<span data-ttu-id="4a156-135">Kilit hello kullanarak kaynakları Azure PowerShell ile dağıtılan [yeni AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) komutu.</span><span class="sxs-lookup"><span data-stu-id="4a156-135">You lock deployed resources with Azure PowerShell by using hello [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) command.</span></span>

<span data-ttu-id="4a156-136">toolock bir kaynak hello kaynağın hello adı, kaynak türü ve kaynak grubu adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="4a156-136">toolock a resource, provide hello name of hello resource, its resource type, and its resource group name.</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="4a156-137">bir kaynak grubu toolock hello hello kaynak grubunun adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="4a156-137">toolock a resource group, provide hello name of hello resource group.</span></span>

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="4a156-138">kilit, kullanım bilgilerini tooget [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span><span class="sxs-lookup"><span data-stu-id="4a156-138">tooget information about a lock, use [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span></span> <span data-ttu-id="4a156-139">tooget, aboneliğinizdeki tüm hello kilitleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="4a156-139">tooget all hello locks in your subscription, use:</span></span>

```powershell
Get-AzureRmResourceLock
```

<span data-ttu-id="4a156-140">bir kaynak için tüm kilitleri tooget kullanın:</span><span class="sxs-lookup"><span data-stu-id="4a156-140">tooget all locks for a resource, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="4a156-141">bir kaynak grubu için tüm kilitleri tooget kullanın:</span><span class="sxs-lookup"><span data-stu-id="4a156-141">tooget all locks for a resource group, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="4a156-142">Azure PowerShell diğer komutları gibi çalışma kilitlerini sağlar [kümesi AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate bir kilit ve [Kaldır AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete kilit.</span><span class="sxs-lookup"><span data-stu-id="4a156-142">Azure PowerShell provides other commands for working locks, such as [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate a lock, and [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete a lock.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="4a156-143">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4a156-143">Azure CLI</span></span>

<span data-ttu-id="4a156-144">Kilit hello kullanarak Azure CLI kaynaklarla dağıtılan [az kilit oluşturmak](/cli/azure/lock#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="4a156-144">You lock deployed resources with Azure CLI by using hello [az lock create](/cli/azure/lock#create) command.</span></span>

<span data-ttu-id="4a156-145">toolock bir kaynak hello kaynağın hello adı, kaynak türü ve kaynak grubu adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="4a156-145">toolock a resource, provide hello name of hello resource, its resource type, and its resource group name.</span></span>

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

<span data-ttu-id="4a156-146">bir kaynak grubu toolock hello hello kaynak grubunun adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="4a156-146">toolock a resource group, provide hello name of hello resource group.</span></span>

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

<span data-ttu-id="4a156-147">kilit, kullanım bilgilerini tooget [az kilit listesi](/cli/azure/lock#list).</span><span class="sxs-lookup"><span data-stu-id="4a156-147">tooget information about a lock, use [az lock list](/cli/azure/lock#list).</span></span> <span data-ttu-id="4a156-148">tooget, aboneliğinizdeki tüm hello kilitleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="4a156-148">tooget all hello locks in your subscription, use:</span></span>

```azurecli
az lock list
```

<span data-ttu-id="4a156-149">bir kaynak için tüm kilitleri tooget kullanın:</span><span class="sxs-lookup"><span data-stu-id="4a156-149">tooget all locks for a resource, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

<span data-ttu-id="4a156-150">bir kaynak grubu için tüm kilitleri tooget kullanın:</span><span class="sxs-lookup"><span data-stu-id="4a156-150">tooget all locks for a resource group, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup
```

<span data-ttu-id="4a156-151">Azure CLI diğer komutları gibi çalışma kilitlerini sağlar [az kilit güncelleştirme](/cli/azure/lock#update) tooupdate bir kilit ve [az kilit silme](/cli/azure/lock#delete) toodelete kilit.</span><span class="sxs-lookup"><span data-stu-id="4a156-151">Azure CLI provides other commands for working locks, such as [az lock update](/cli/azure/lock#update) tooupdate a lock, and [az lock delete](/cli/azure/lock#delete) toodelete a lock.</span></span>

## <a name="rest-api"></a><span data-ttu-id="4a156-152">REST API</span><span class="sxs-lookup"><span data-stu-id="4a156-152">REST API</span></span>
<span data-ttu-id="4a156-153">Dağıtılan hello kaynaklarla kilitleyebilirsiniz [yönetim kilitleri için REST API](https://docs.microsoft.com/rest/api/resources/managementlocks).</span><span class="sxs-lookup"><span data-stu-id="4a156-153">You can lock deployed resources with hello [REST API for management locks](https://docs.microsoft.com/rest/api/resources/managementlocks).</span></span> <span data-ttu-id="4a156-154">Merhaba REST API toocreate sağlar ve kilitleri silin ve varolan kilitler hakkında bilgi alın.</span><span class="sxs-lookup"><span data-stu-id="4a156-154">hello REST API enables you toocreate and delete locks, and retrieve information about existing locks.</span></span>

<span data-ttu-id="4a156-155">toocreate bir kilit çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4a156-155">toocreate a lock, run:</span></span>

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

<span data-ttu-id="4a156-156">Merhaba kapsam abonelik, kaynak grubu veya kaynak olabilir.</span><span class="sxs-lookup"><span data-stu-id="4a156-156">hello scope could be a subscription, resource group, or resource.</span></span> <span data-ttu-id="4a156-157">Merhaba kilit-istediğiniz addır toocall hello kilitle.</span><span class="sxs-lookup"><span data-stu-id="4a156-157">hello lock-name is whatever you want toocall hello lock.</span></span> <span data-ttu-id="4a156-158">API sürümü için kullanmak **2015-01-01**.</span><span class="sxs-lookup"><span data-stu-id="4a156-158">For api-version, use **2015-01-01**.</span></span>

<span data-ttu-id="4a156-159">Merhaba istekte hello kilitleme hello özelliklerini belirten bir JSON nesnesi içerir.</span><span class="sxs-lookup"><span data-stu-id="4a156-159">In hello request, include a JSON object that specifies hello properties for hello lock.</span></span>

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a><span data-ttu-id="4a156-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4a156-160">Next steps</span></span>
* <span data-ttu-id="4a156-161">Kaynak kilitleri ile çalışma hakkında daha fazla bilgi için bkz: [kilit aşağı bilgisayarınızı Azure kaynakları](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span><span class="sxs-lookup"><span data-stu-id="4a156-161">For more information about working with resource locks, see [Lock Down Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span></span>
* <span data-ttu-id="4a156-162">mantıksal olarak kaynaklarınızı düzenleme hakkında toolearn bakın [kullanarak kaynaklarınızı tooorganize etiketleri](resource-group-using-tags.md)</span><span class="sxs-lookup"><span data-stu-id="4a156-162">toolearn about logically organizing your resources, see [Using tags tooorganize your resources](resource-group-using-tags.md)</span></span>
* <span data-ttu-id="4a156-163">hangi kaynak grubu bir kaynak bulunur, toochange bakın [kaynakları toonew kaynak grubu taşıma](resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="4a156-163">toochange which resource group a resource resides in, see [Move resources toonew resource group](resource-group-move-resources.md)</span></span>
* <span data-ttu-id="4a156-164">Özelleştirilmiş ilkeler aboneliğinizle arasında kısıtlamaları ve kuralları uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a156-164">You can apply restrictions and conventions across your subscription with customized policies.</span></span> <span data-ttu-id="4a156-165">Daha fazla bilgi için bkz: [kullanım ilkesi toomanage kaynakları ve erişimi denetleme](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="4a156-165">For more information, see [Use Policy toomanage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="4a156-166">Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="4a156-166">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

