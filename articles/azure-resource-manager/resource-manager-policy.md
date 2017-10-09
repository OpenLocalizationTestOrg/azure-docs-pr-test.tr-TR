---
title: aaaAzure kaynak ilkeleri | Microsoft Docs
description: "Dağıtım sırasında toouse Azure Resource Manager ilkeleri tooensure tutarlı kaynak özellikleri nasıl ayarlanacağını açıklar. Merhaba abonelik veya kaynak gruplarının ilkeleri uygulanabilir."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: abde0f73-c0fe-4e6d-a1ee-32a6fce52a2d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: tomfitz
ms.openlocfilehash: f1b0bbb5f838f6bb70721e1040ad3eac2d881cea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-policy-overview"></a><span data-ttu-id="9732a-104">Kaynak ilkesine genel bakış</span><span class="sxs-lookup"><span data-stu-id="9732a-104">Resource policy overview</span></span>
<span data-ttu-id="9732a-105">Kaynak ilkeleri, kuruluşunuzdaki kaynakların tooestablish kuralları etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="9732a-105">Resource policies enable you tooestablish conventions for resources in your organization.</span></span> <span data-ttu-id="9732a-106">Kuralları tanımlayarak, daha kolay kaynaklarınızı yönetmek ve maliyetleri denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9732a-106">By defining conventions, you can control costs and more easily manage your resources.</span></span> <span data-ttu-id="9732a-107">Örneğin, sanal makineler yalnızca belirli türdeki izin verildiğini belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9732a-107">For example, you can specify that only certain types of virtual machines are allowed.</span></span> <span data-ttu-id="9732a-108">Veya, tüm kaynakların belirli bir etikete sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9732a-108">Or, you can require that all resources have a particular tag.</span></span> <span data-ttu-id="9732a-109">İlkeler tüm alt kaynaklar tarafından devralınır.</span><span class="sxs-lookup"><span data-stu-id="9732a-109">Policies are inherited by all child resources.</span></span> <span data-ttu-id="9732a-110">Bu nedenle, bir ilke uygulanmış tooa kaynak grubu ise, uygun tooall hello kaynakların kaynak grubunda olur.</span><span class="sxs-lookup"><span data-stu-id="9732a-110">So, if a policy is applied tooa resource group, it is applicable tooall hello resources in that resource group.</span></span>

<span data-ttu-id="9732a-111">İki kavramları toounderstand ilkeleri hakkında vardır:</span><span class="sxs-lookup"><span data-stu-id="9732a-111">There are two concepts toounderstand about policies:</span></span>

* <span data-ttu-id="9732a-112">ilke tanımı - hello İlkesi uygulandığında ne zaman ve hangi eylemini tootake açıklanmaktadır</span><span class="sxs-lookup"><span data-stu-id="9732a-112">policy definition - you describe when hello policy is enforced and what action tootake</span></span>
* <span data-ttu-id="9732a-113">ilke ataması - hello ilke tanımı tooa kapsamı (abonelik veya kaynak grubu) Uygula</span><span class="sxs-lookup"><span data-stu-id="9732a-113">policy assignment - you apply hello policy definition tooa scope (subscription or resource group)</span></span>

<span data-ttu-id="9732a-114">Bu konu, ilke tanımı odaklanır.</span><span class="sxs-lookup"><span data-stu-id="9732a-114">This topic focuses on policy definition.</span></span> <span data-ttu-id="9732a-115">İlke ataması hakkında daha fazla bilgi için bkz: [kullanım Azure portal tooassign ve kaynak ilkelerini yönetme](resource-manager-policy-portal.md) veya [atayın ve komut dosyası aracılığıyla ilkelerini yönetme](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="9732a-115">For information about policy assignment, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md) or [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>

<span data-ttu-id="9732a-116">İlkeleri oluşturma ve (PUT ve işlemleri düzeltme eki) kaynakları güncelleştirme değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="9732a-116">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

> [!NOTE]
> <span data-ttu-id="9732a-117">Şu anda, ilke etiketleri, türü ve konumu hello Microsoft.Resources/deployments kaynak türü gibi desteklemez kaynak türleri değerlendirmez.</span><span class="sxs-lookup"><span data-stu-id="9732a-117">Currently, policy does not evaluate resource types that do not support tags, kind, and location, such as hello Microsoft.Resources/deployments resource type.</span></span> <span data-ttu-id="9732a-118">Bu destek gelecek bir zamanda eklenir.</span><span class="sxs-lookup"><span data-stu-id="9732a-118">This support will be added at a future time.</span></span> <span data-ttu-id="9732a-119">tooavoid geriye dönük uyumluluk sorunları, ilkeleri yazarken daha açıkça belirtilen türünü belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9732a-119">tooavoid backward compatibility issues, you should explicitly specify type when authoring policies.</span></span> <span data-ttu-id="9732a-120">Örneğin, türleri belirtmeyen bir etiket İlkesi tüm türleri için uygulanır.</span><span class="sxs-lookup"><span data-stu-id="9732a-120">For example, a tag policy that does not specify types is applied for all types.</span></span> <span data-ttu-id="9732a-121">Bu durumda, bir şablon dağıtımı etiketleri desteklemiyor iç içe geçmiş bir kaynak yoksa başarısız olabilir ve hello dağıtım kaynak türü toopolicy değerlendirme eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="9732a-121">In that case, a template deployment may fail if there is a nested resource that doesn't support tags, and hello deployment resource type has been added toopolicy evaluation.</span></span> 
> 
> 

## <a name="how-is-it-different-from-rbac"></a><span data-ttu-id="9732a-122">Nasıl RBAC farklı mı?</span><span class="sxs-lookup"><span data-stu-id="9732a-122">How is it different from RBAC?</span></span>
<span data-ttu-id="9732a-123">İlke ve rol tabanlı erişim denetimi (RBAC) arasındaki bazı farklar vardır.</span><span class="sxs-lookup"><span data-stu-id="9732a-123">There are a few key differences between policy and role-based access control (RBAC).</span></span> <span data-ttu-id="9732a-124">RBAC odaklanır **kullanıcı** farklı kapsamlar eylemlerini.</span><span class="sxs-lookup"><span data-stu-id="9732a-124">RBAC focuses on **user** actions at different scopes.</span></span> <span data-ttu-id="9732a-125">Örneğin, değişiklikleri toothat kaynak grubu olabilmeniz toohello katkıda bulunan rolü bir kaynak grubu için istenen hello kapsamda eklenir.</span><span class="sxs-lookup"><span data-stu-id="9732a-125">For example, you are added toohello contributor role for a resource group at hello desired scope, so you can make changes toothat resource group.</span></span> <span data-ttu-id="9732a-126">İlke odaklanır **kaynak** dağıtımı sırasında özellikler.</span><span class="sxs-lookup"><span data-stu-id="9732a-126">Policy focuses on **resource** properties during deployment.</span></span> <span data-ttu-id="9732a-127">Örneğin, ilkeler aracılığıyla sağlanabilir kaynak hello türleri kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9732a-127">For example, through policies, you can control hello types of resources that can be provisioned.</span></span> <span data-ttu-id="9732a-128">Ya da hello kaynakları sağlanabilir hello konumları kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9732a-128">Or, you can restrict hello locations in which hello resources can be provisioned.</span></span> <span data-ttu-id="9732a-129">RBAC, bir varsayılan izin ilkedir ve açık sistem engelle.</span><span class="sxs-lookup"><span data-stu-id="9732a-129">Unlike RBAC, policy is a default allow and explicit deny system.</span></span> 

<span data-ttu-id="9732a-130">toouse ilkeleri RBAC kimliğinin doğrulanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9732a-130">toouse policies, you must be authenticated through RBAC.</span></span> <span data-ttu-id="9732a-131">Özellikle, hesabınızı gerekir:</span><span class="sxs-lookup"><span data-stu-id="9732a-131">Specifically, your account needs the:</span></span>

* <span data-ttu-id="9732a-132">`Microsoft.Authorization/policydefinitions/write`izin toodefine bir ilke</span><span class="sxs-lookup"><span data-stu-id="9732a-132">`Microsoft.Authorization/policydefinitions/write` permission toodefine a policy</span></span>
* <span data-ttu-id="9732a-133">`Microsoft.Authorization/policyassignments/write`izin tooassign bir ilke</span><span class="sxs-lookup"><span data-stu-id="9732a-133">`Microsoft.Authorization/policyassignments/write` permission tooassign a policy</span></span> 

<span data-ttu-id="9732a-134">Bu izinleri hello dahil edilmeyen **katkıda bulunan** rol.</span><span class="sxs-lookup"><span data-stu-id="9732a-134">These permissions are not included in hello **Contributor** role.</span></span>

## <a name="built-in-policies"></a><span data-ttu-id="9732a-135">Yerleşik ilkeleri</span><span class="sxs-lookup"><span data-stu-id="9732a-135">Built-in policies</span></span>

<span data-ttu-id="9732a-136">Azure sağlar hello sayısını azaltabilir bazı yerleşik ilke tanımları ilkelerini toodefine sahip.</span><span class="sxs-lookup"><span data-stu-id="9732a-136">Azure provides some built-in policy definitions that may reduce hello number of policies you have toodefine.</span></span> <span data-ttu-id="9732a-137">İlke tanımları ile devam etmeden önce yerleşik bir ilke zaten ihtiyaç hello tanımı sağlayıp sağlamadığını göz önünde bulundurmalısınız.</span><span class="sxs-lookup"><span data-stu-id="9732a-137">Before proceeding with policy definitions, you should consider whether a built-in policy already provides hello definition you need.</span></span> <span data-ttu-id="9732a-138">Merhaba yerleşik ilke tanımları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9732a-138">hello built-in policy definitions are:</span></span>

* <span data-ttu-id="9732a-139">İzin verilen konumların</span><span class="sxs-lookup"><span data-stu-id="9732a-139">Allowed locations</span></span>
* <span data-ttu-id="9732a-140">İzin verilen kaynak türleri</span><span class="sxs-lookup"><span data-stu-id="9732a-140">Allowed resource types</span></span>
* <span data-ttu-id="9732a-141">Depolama hesabı SKU'ları izin</span><span class="sxs-lookup"><span data-stu-id="9732a-141">Allowed storage account SKUs</span></span>
* <span data-ttu-id="9732a-142">Sanal makine SKU'ları izin</span><span class="sxs-lookup"><span data-stu-id="9732a-142">Allowed virtual machine SKUs</span></span>
* <span data-ttu-id="9732a-143">Etiket ve varsayılan değer Uygula</span><span class="sxs-lookup"><span data-stu-id="9732a-143">Apply tag and default value</span></span>
* <span data-ttu-id="9732a-144">Etiket ve değer zorla</span><span class="sxs-lookup"><span data-stu-id="9732a-144">Enforce tag and value</span></span>
* <span data-ttu-id="9732a-145">Kaynak türleri izin verilmiyor</span><span class="sxs-lookup"><span data-stu-id="9732a-145">Not allowed resource types</span></span>
* <span data-ttu-id="9732a-146">SQL Server sürüm 12.0 gerektirir</span><span class="sxs-lookup"><span data-stu-id="9732a-146">Require SQL Server version 12.0</span></span>
* <span data-ttu-id="9732a-147">Depolama hesabı şifreleme iste</span><span class="sxs-lookup"><span data-stu-id="9732a-147">Require storage account encryption</span></span>

<span data-ttu-id="9732a-148">Herhangi bir hello aracılığıyla bu ilkeleri atayabilirsiniz [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), veya [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9732a-148">You can assign any of these policies through hello [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), or [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).</span></span>

## <a name="policy-definition-structure"></a><span data-ttu-id="9732a-149">İlke tanımı yapısı</span><span class="sxs-lookup"><span data-stu-id="9732a-149">Policy definition structure</span></span>
<span data-ttu-id="9732a-150">JSON toocreate bir ilke tanımı kullanın.</span><span class="sxs-lookup"><span data-stu-id="9732a-150">You use JSON toocreate a policy definition.</span></span> <span data-ttu-id="9732a-151">Merhaba ilke tanımı için öğeleri içerir:</span><span class="sxs-lookup"><span data-stu-id="9732a-151">hello policy definition contains elements for:</span></span>

* <span data-ttu-id="9732a-152">parametreler</span><span class="sxs-lookup"><span data-stu-id="9732a-152">parameters</span></span>
* <span data-ttu-id="9732a-153">Görünen ad</span><span class="sxs-lookup"><span data-stu-id="9732a-153">display name</span></span>
* <span data-ttu-id="9732a-154">açıklama</span><span class="sxs-lookup"><span data-stu-id="9732a-154">description</span></span>
* <span data-ttu-id="9732a-155">İlke kuralı</span><span class="sxs-lookup"><span data-stu-id="9732a-155">policy rule</span></span>
  * <span data-ttu-id="9732a-156">mantıksal değerlendirme</span><span class="sxs-lookup"><span data-stu-id="9732a-156">logical evaluation</span></span>
  * <span data-ttu-id="9732a-157">Etkisi</span><span class="sxs-lookup"><span data-stu-id="9732a-157">effect</span></span>

<span data-ttu-id="9732a-158">Aşağıdaki örnek hello kaynakları dağıtıldığı sınırlar bir ilke gösterir:</span><span class="sxs-lookup"><span data-stu-id="9732a-158">hello following example shows a policy that limits where resources are deployed:</span></span>

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "not": {
          "field": "location",
          "in": "[parameters('allowedLocations')]"
        }
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

## <a name="parameters"></a><span data-ttu-id="9732a-159">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9732a-159">Parameters</span></span>
<span data-ttu-id="9732a-160">Parametrelerini kullanarak ilke tanımları hello sayısını azaltarak ilke yönetimini basitleştirmeye yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="9732a-160">Using parameters helps simplify your policy management by reducing hello number of policy definitions.</span></span> <span data-ttu-id="9732a-161">(Örneğin kaynaklar dağıtıldığı hello konumları sınırlama) kaynak özelliği için bir ilke tanımlayın ve hello tanımında parametreleri içerir.</span><span class="sxs-lookup"><span data-stu-id="9732a-161">You define a policy for a resource property (such as limiting hello locations where resources can be deployed), and include parameters in hello definition.</span></span> <span data-ttu-id="9732a-162">Ardından, bu ilke tanımı farklı senaryolar için (örneğin, bir dizi bir abonelik için konumları belirtme) farklı değerler geçirerek ne zaman yeniden hello ilkesi atama.</span><span class="sxs-lookup"><span data-stu-id="9732a-162">Then, you reuse that policy definition for different scenarios by passing in different values (such as specifying one set of locations for a subscription) when assigning hello policy.</span></span>

<span data-ttu-id="9732a-163">İlke tanımları oluşturduğunuzda parametreleri bildirin.</span><span class="sxs-lookup"><span data-stu-id="9732a-163">You declare parameters when you create policy definitions.</span></span>

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "hello list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

<span data-ttu-id="9732a-164">parametrenin Hello türü string veya dizi olabilir.</span><span class="sxs-lookup"><span data-stu-id="9732a-164">hello type of a parameter can be either string or array.</span></span> <span data-ttu-id="9732a-165">Merhaba meta veri özelliği, Azure portal toodisplay kullanıcı dostu bilgiler gibi araçları için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9732a-165">hello metadata property is used for tools like Azure portal toodisplay user-friendly information.</span></span> 

<span data-ttu-id="9732a-166">Hello İlkesi kuralında sözdizimi aşağıdaki hello ile parametreleri başvuru:</span><span class="sxs-lookup"><span data-stu-id="9732a-166">In hello policy rule, you reference parameters with hello following syntax:</span></span> 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a><span data-ttu-id="9732a-167">Görünen ad ve açıklama</span><span class="sxs-lookup"><span data-stu-id="9732a-167">Display name and description</span></span>

<span data-ttu-id="9732a-168">Merhaba kullandığınız **displayName** ve **açıklama** tooidentify hello ilke tanımı ve ne zaman kullanıldığı için bağlamı sağlar.</span><span class="sxs-lookup"><span data-stu-id="9732a-168">You use hello **displayName** and **description** tooidentify hello policy definition, and provide context for when it is used.</span></span>

## <a name="policy-rule"></a><span data-ttu-id="9732a-169">İlke kuralı</span><span class="sxs-lookup"><span data-stu-id="9732a-169">Policy rule</span></span>

<span data-ttu-id="9732a-170">Hello İlkesi kuralı oluşur **varsa** ve **sonra** engeller.</span><span class="sxs-lookup"><span data-stu-id="9732a-170">hello policy rule consists of **If** and **Then** blocks.</span></span> <span data-ttu-id="9732a-171">Merhaba, **varsa** bloğu, ne zaman hello İlkesi uygulandığında belirten bir veya daha fazla koşullarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-171">In hello **If** block, you define one or more conditions that specify when hello policy is enforced.</span></span> <span data-ttu-id="9732a-172">Mantıksal işleçler toothese koşullar geçerli tooprecisely hello senaryo için bir ilke tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-172">You can apply logical operators toothese conditions tooprecisely define hello scenario for a policy.</span></span> <span data-ttu-id="9732a-173">Merhaba, **sonra** bloğu hello olur hello etkisi tanımladığınız **varsa** koşullar yerine.</span><span class="sxs-lookup"><span data-stu-id="9732a-173">In hello **Then** block, you define hello effect that happens when hello **If** conditions are fulfilled.</span></span>

```json
{
  "if": {
    <condition> | <logical operator>
  },
  "then": {
    "effect": "deny | audit | append"
  }
}
```

### <a name="logical-operators"></a><span data-ttu-id="9732a-174">Mantıksal işleçler</span><span class="sxs-lookup"><span data-stu-id="9732a-174">Logical operators</span></span>
<span data-ttu-id="9732a-175">desteklenen hello mantıksal işleçler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9732a-175">hello supported logical operators are:</span></span>

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

<span data-ttu-id="9732a-176">Merhaba **değil** sözdizimi hello koşul hello sonucunu tersine çevirir.</span><span class="sxs-lookup"><span data-stu-id="9732a-176">hello **not** syntax inverts hello result of hello condition.</span></span> <span data-ttu-id="9732a-177">Merhaba **tümü** sözdizimi (benzer toohello mantıksal **ve** işlemi) tüm koşullar toobe true gerektirir.</span><span class="sxs-lookup"><span data-stu-id="9732a-177">hello **allOf** syntax (similar toohello logical **And** operation) requires all conditions toobe true.</span></span> <span data-ttu-id="9732a-178">Merhaba **herhangi** sözdizimi (benzer toohello mantıksal **veya** işlemi) bir veya daha fazla koşullar toobe true gerektirir.</span><span class="sxs-lookup"><span data-stu-id="9732a-178">hello **anyOf** syntax (similar toohello logical **Or** operation) requires one or more conditions toobe true.</span></span>

<span data-ttu-id="9732a-179">Mantıksal işleçler yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9732a-179">You can nest logical operators.</span></span> <span data-ttu-id="9732a-180">Aşağıdaki örnekte gösterildiği hello bir **değil** içinde iç içe işlemi bir **tümü** işlemi.</span><span class="sxs-lookup"><span data-stu-id="9732a-180">hello following example shows a **not** operation that is nested within an **allOf** operation.</span></span> 

```json
"if": {
  "allOf": [
    {
      "not": {
        "field": "tags",
        "containsKey": "application"
      }
    },
    {
      "field": "type",
      "equals": "Microsoft.Storage/storageAccounts"
    }
  ]
},
```

### <a name="conditions"></a><span data-ttu-id="9732a-181">Koşullar</span><span class="sxs-lookup"><span data-stu-id="9732a-181">Conditions</span></span>
<span data-ttu-id="9732a-182">Merhaba koşulu değerlendirir olup bir **alan** belirli kriterlere uyan.</span><span class="sxs-lookup"><span data-stu-id="9732a-182">hello condition evaluates whether a **field** meets certain criteria.</span></span> <span data-ttu-id="9732a-183">desteklenen hello koşullar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9732a-183">hello supported conditions are:</span></span>

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

<span data-ttu-id="9732a-184">Merhaba kullanırken **gibi** koşulu, bir joker (*) hello değer sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="9732a-184">When using hello **like** condition, you can provide a wildcard (*) in hello value.</span></span>

<span data-ttu-id="9732a-185">Merhaba kullanırken **eşleşen** koşul, sağlayın `#` toorepresent bir basamak `?` bir harf ve diğer toorepresent Bu gerçek karakteri için.</span><span class="sxs-lookup"><span data-stu-id="9732a-185">When using hello **match** condition, provide `#` toorepresent a digit, `?` for a letter, and any other character toorepresent that actual character.</span></span> <span data-ttu-id="9732a-186">Örnekler için bkz: [adları ve metin için kaynak ilkelerini uygulamak](resource-manager-policy-naming-convention.md).</span><span class="sxs-lookup"><span data-stu-id="9732a-186">For examples, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>

### <a name="fields"></a><span data-ttu-id="9732a-187">Alanları</span><span class="sxs-lookup"><span data-stu-id="9732a-187">Fields</span></span>
<span data-ttu-id="9732a-188">Koşullar alanlar kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9732a-188">Conditions are formed by using fields.</span></span> <span data-ttu-id="9732a-189">Bir alan hello kaynak isteği yükü özelliklerinde temsil eden başka bir deyişle kullanılan toodescribe hello hello kaynağının durumu.</span><span class="sxs-lookup"><span data-stu-id="9732a-189">A field represents properties in hello resource request payload that is used toodescribe hello state of hello resource.</span></span>  

<span data-ttu-id="9732a-190">alanları aşağıdaki hello desteklenir:</span><span class="sxs-lookup"><span data-stu-id="9732a-190">hello following fields are supported:</span></span>

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* <span data-ttu-id="9732a-191">özellik diğer adlar - bir listesi için bkz: [diğer adlar](#aliases).</span><span class="sxs-lookup"><span data-stu-id="9732a-191">property aliases - for a list, see [Aliases](#aliases).</span></span>

### <a name="effect"></a><span data-ttu-id="9732a-192">Etki</span><span class="sxs-lookup"><span data-stu-id="9732a-192">Effect</span></span>
<span data-ttu-id="9732a-193">İlke etkili - üç tür destekler `deny`, `audit`, ve `append`.</span><span class="sxs-lookup"><span data-stu-id="9732a-193">Policy supports three types of effect - `deny`, `audit`, and `append`.</span></span> 

* <span data-ttu-id="9732a-194">**Reddetme** hello Denetim günlüğüne bir olay oluşturur ve hello isteği başarısız olur</span><span class="sxs-lookup"><span data-stu-id="9732a-194">**Deny** generates an event in hello audit log and fails hello request</span></span>
* <span data-ttu-id="9732a-195">**Denetim** Denetim günlüğüne bir uyarı olayı oluşturur ama hello isteği başarısız değil</span><span class="sxs-lookup"><span data-stu-id="9732a-195">**Audit** generates a warning event in audit log but does not fail hello request</span></span>
* <span data-ttu-id="9732a-196">**Append** alanları toohello isteği tanımlanan hello kümesi ekler</span><span class="sxs-lookup"><span data-stu-id="9732a-196">**Append** adds hello defined set of fields toohello request</span></span> 

<span data-ttu-id="9732a-197">İçin **sona**, aşağıdaki ayrıntılara hello sağlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="9732a-197">For **append**, you must provide hello following details:</span></span>

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of hello field"
  }
]
```

<span data-ttu-id="9732a-198">Merhaba değer bir dize veya bir JSON biçimi nesnesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="9732a-198">hello value can be either a string or a JSON format object.</span></span> 

## <a name="aliases"></a><span data-ttu-id="9732a-199">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="9732a-199">Aliases</span></span>

<span data-ttu-id="9732a-200">Bir kaynak türü için özellik diğer adlar tooaccess belirli özelliklerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="9732a-200">You use property aliases tooaccess specific properties for a resource type.</span></span> <span data-ttu-id="9732a-201">Diğer adlar hangi değerleri veya koşullara bir özelliği bir kaynak için izin verilen toorestrict etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="9732a-201">Aliases enable you toorestrict what values or conditions are permitted for a property on a resource.</span></span> <span data-ttu-id="9732a-202">Her bir diğer ad toopaths belirli kaynak türlerine yönelik farklı API sürümlerindeki eşler.</span><span class="sxs-lookup"><span data-stu-id="9732a-202">Each alias maps toopaths in different API versions for a given resource type.</span></span> <span data-ttu-id="9732a-203">İlke değerlendirmesi sırasında hello ilke altyapısı, API sürümü hello özelliği yolunu alır.</span><span class="sxs-lookup"><span data-stu-id="9732a-203">During policy evaluation, hello policy engine gets hello property path for that API version.</span></span>

<span data-ttu-id="9732a-204">**Microsoft.Cache/Redis**</span><span class="sxs-lookup"><span data-stu-id="9732a-204">**Microsoft.Cache/Redis**</span></span>

| <span data-ttu-id="9732a-205">Diğer ad</span><span class="sxs-lookup"><span data-stu-id="9732a-205">Alias</span></span> | <span data-ttu-id="9732a-206">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9732a-206">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="9732a-207">Microsoft.Cache/Redis/enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="9732a-207">Microsoft.Cache/Redis/enableNonSslPort</span></span> | <span data-ttu-id="9732a-208">Ayarlanmış olup olmadığını hello ssl olmayan Redis bağlantı noktası (6379) etkindir.</span><span class="sxs-lookup"><span data-stu-id="9732a-208">Set whether hello non-ssl Redis server port (6379) is enabled.</span></span> |
| <span data-ttu-id="9732a-209">Microsoft.Cache/Redis/shardCount</span><span class="sxs-lookup"><span data-stu-id="9732a-209">Microsoft.Cache/Redis/shardCount</span></span> | <span data-ttu-id="9732a-210">Premium küme önbelleği üzerinde oluşturulan parça toobe Hello sayısını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-210">Set hello number of shards toobe created on a Premium Cluster Cache.</span></span>  |
| <span data-ttu-id="9732a-211">Microsoft.Cache/Redis/sku.capacity</span><span class="sxs-lookup"><span data-stu-id="9732a-211">Microsoft.Cache/Redis/sku.capacity</span></span> | <span data-ttu-id="9732a-212">Merhaba Redis önbelleği toodeploy Hello boyutunu ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-212">Set hello size of hello Redis cache toodeploy.</span></span>  |
| <span data-ttu-id="9732a-213">Microsoft.Cache/Redis/sku.family</span><span class="sxs-lookup"><span data-stu-id="9732a-213">Microsoft.Cache/Redis/sku.family</span></span> | <span data-ttu-id="9732a-214">Merhaba SKU ailesi toouse ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-214">Set hello SKU family toouse.</span></span> |
| <span data-ttu-id="9732a-215">Microsoft.Cache/Redis/sku.name</span><span class="sxs-lookup"><span data-stu-id="9732a-215">Microsoft.Cache/Redis/sku.name</span></span> | <span data-ttu-id="9732a-216">Redis önbelleği toodeploy Hello türünü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-216">Set hello type of Redis Cache toodeploy.</span></span> |

<span data-ttu-id="9732a-217">**Microsoft.Cdn/profiles**</span><span class="sxs-lookup"><span data-stu-id="9732a-217">**Microsoft.Cdn/profiles**</span></span>

| <span data-ttu-id="9732a-218">Diğer ad</span><span class="sxs-lookup"><span data-stu-id="9732a-218">Alias</span></span> | <span data-ttu-id="9732a-219">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9732a-219">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="9732a-220">Microsoft.CDN/profiles/sku.name</span><span class="sxs-lookup"><span data-stu-id="9732a-220">Microsoft.CDN/profiles/sku.name</span></span> | <span data-ttu-id="9732a-221">Fiyatlandırma katmanı hello Hello adını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-221">Set hello name of hello pricing tier.</span></span> |

<span data-ttu-id="9732a-222">**Microsoft.Compute/disks**</span><span class="sxs-lookup"><span data-stu-id="9732a-222">**Microsoft.Compute/disks**</span></span>

| <span data-ttu-id="9732a-223">Diğer ad</span><span class="sxs-lookup"><span data-stu-id="9732a-223">Alias</span></span> | <span data-ttu-id="9732a-224">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9732a-224">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="9732a-225">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="9732a-225">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="9732a-226">Set hello teklif hello platform görüntüsü veya Market görüntüsü toocreate hello sanal makine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9732a-226">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="9732a-227">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="9732a-227">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="9732a-228">Merhaba platform görüntüsü veya Market görüntüsü kümesi hello yayımcısına toocreate hello sanal makine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9732a-228">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="9732a-229">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="9732a-229">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="9732a-230">Set hello hello platform görüntüsü veya Market görüntüsü SKU'su toocreate hello sanal makine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9732a-230">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="9732a-231">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="9732a-231">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="9732a-232">Merhaba platform görüntüsü veya Market görüntüsü sürümü kümesi hello toocreate hello sanal makine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9732a-232">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |


<span data-ttu-id="9732a-233">**Microsoft.Compute/virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="9732a-233">**Microsoft.Compute/virtualMachines**</span></span>

| <span data-ttu-id="9732a-234">Diğer ad</span><span class="sxs-lookup"><span data-stu-id="9732a-234">Alias</span></span> | <span data-ttu-id="9732a-235">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9732a-235">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="9732a-236">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="9732a-236">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="9732a-237">Merhaba kullanılan görüntü toocreate hello sanal makine Hello tanıtıcısı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-237">Set hello identifier of hello image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="9732a-238">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="9732a-238">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="9732a-239">Set hello teklif hello platform görüntüsü veya Market görüntüsü toocreate hello sanal makine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9732a-239">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="9732a-240">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="9732a-240">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="9732a-241">Merhaba platform görüntüsü veya Market görüntüsü kümesi hello yayımcısına toocreate hello sanal makine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9732a-241">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="9732a-242">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="9732a-242">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="9732a-243">Set hello hello platform görüntüsü veya Market görüntüsü SKU'su toocreate hello sanal makine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9732a-243">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="9732a-244">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="9732a-244">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="9732a-245">Merhaba platform görüntüsü veya Market görüntüsü sürümü kümesi hello toocreate hello sanal makine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9732a-245">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="9732a-246">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="9732a-246">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="9732a-247">Merhaba görüntü veya disk içi lisanslı ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="9732a-247">Set that hello image or disk is licensed on-premises.</span></span> <span data-ttu-id="9732a-248">Bu değer yalnızca hello Windows Server işletim sistemi içeren görüntüler için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9732a-248">This value is only used for images that contain hello Windows Server operating system.</span></span>  |
| <span data-ttu-id="9732a-249">Microsoft.Compute/virtualMachines/imageOffer</span><span class="sxs-lookup"><span data-stu-id="9732a-249">Microsoft.Compute/virtualMachines/imageOffer</span></span> | <span data-ttu-id="9732a-250">Set hello teklif hello platform görüntüsü veya Market görüntüsü toocreate hello sanal makine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9732a-250">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="9732a-251">Microsoft.Compute/virtualMachines/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="9732a-251">Microsoft.Compute/virtualMachines/imagePublisher</span></span> | <span data-ttu-id="9732a-252">Merhaba platform görüntüsü veya Market görüntüsü kümesi hello yayımcısına toocreate hello sanal makine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9732a-252">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="9732a-253">Microsoft.Compute/virtualMachines/imageSku</span><span class="sxs-lookup"><span data-stu-id="9732a-253">Microsoft.Compute/virtualMachines/imageSku</span></span> | <span data-ttu-id="9732a-254">Set hello hello platform görüntüsü veya Market görüntüsü SKU'su toocreate hello sanal makine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9732a-254">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="9732a-255">Microsoft.Compute/virtualMachines/imageVersion</span><span class="sxs-lookup"><span data-stu-id="9732a-255">Microsoft.Compute/virtualMachines/imageVersion</span></span> | <span data-ttu-id="9732a-256">Merhaba platform görüntüsü veya Market görüntüsü sürümü kümesi hello toocreate hello sanal makine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9732a-256">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="9732a-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span><span class="sxs-lookup"><span data-stu-id="9732a-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span></span> | <span data-ttu-id="9732a-258">Merhaba vhd URI ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-258">Set hello vhd URI.</span></span> |
| <span data-ttu-id="9732a-259">Microsoft.Compute/virtualMachines/sku.name</span><span class="sxs-lookup"><span data-stu-id="9732a-259">Microsoft.Compute/virtualMachines/sku.name</span></span> | <span data-ttu-id="9732a-260">Merhaba hello sanal makine boyutunu ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-260">Set hello size of hello virtual machine.</span></span> |

<span data-ttu-id="9732a-261">**Microsoft.Compute/virtualMachines/extensions**</span><span class="sxs-lookup"><span data-stu-id="9732a-261">**Microsoft.Compute/virtualMachines/extensions**</span></span>

| <span data-ttu-id="9732a-262">Diğer ad</span><span class="sxs-lookup"><span data-stu-id="9732a-262">Alias</span></span> | <span data-ttu-id="9732a-263">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9732a-263">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="9732a-264">Microsoft.Compute/virtualMachines/extensions/publisher</span><span class="sxs-lookup"><span data-stu-id="9732a-264">Microsoft.Compute/virtualMachines/extensions/publisher</span></span> | <span data-ttu-id="9732a-265">Merhaba hello uzantının yayımcının adını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-265">Set hello name of hello extension’s publisher.</span></span> |
| <span data-ttu-id="9732a-266">Microsoft.Compute/virtualMachines/extensions/type</span><span class="sxs-lookup"><span data-stu-id="9732a-266">Microsoft.Compute/virtualMachines/extensions/type</span></span> | <span data-ttu-id="9732a-267">Uzantı Hello türünü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-267">Set hello type of extension.</span></span> |
| <span data-ttu-id="9732a-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="9732a-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span></span> | <span data-ttu-id="9732a-269">Merhaba uzantıları Hello sürümünü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-269">Set hello version of hello extension.</span></span> |

<span data-ttu-id="9732a-270">**Microsoft.Compute/virtualMachineScaleSets**</span><span class="sxs-lookup"><span data-stu-id="9732a-270">**Microsoft.Compute/virtualMachineScaleSets**</span></span>

| <span data-ttu-id="9732a-271">Diğer ad</span><span class="sxs-lookup"><span data-stu-id="9732a-271">Alias</span></span> | <span data-ttu-id="9732a-272">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9732a-272">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="9732a-273">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="9732a-273">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="9732a-274">Merhaba kullanılan görüntü toocreate hello sanal makine Hello tanıtıcısı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-274">Set hello identifier of hello image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="9732a-275">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="9732a-275">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="9732a-276">Set hello teklif hello platform görüntüsü veya Market görüntüsü toocreate hello sanal makine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9732a-276">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="9732a-277">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="9732a-277">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="9732a-278">Merhaba platform görüntüsü veya Market görüntüsü kümesi hello yayımcısına toocreate hello sanal makine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9732a-278">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="9732a-279">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="9732a-279">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="9732a-280">Set hello hello platform görüntüsü veya Market görüntüsü SKU'su toocreate hello sanal makine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9732a-280">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="9732a-281">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="9732a-281">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="9732a-282">Merhaba platform görüntüsü veya Market görüntüsü sürümü kümesi hello toocreate hello sanal makine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9732a-282">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="9732a-283">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="9732a-283">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="9732a-284">Merhaba görüntü veya disk içi lisanslı ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="9732a-284">Set that hello image or disk is licensed on-premises.</span></span> <span data-ttu-id="9732a-285">Bu değer yalnızca hello Windows Server işletim sistemi içeren görüntüler için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9732a-285">This value is only used for images that contain hello Windows Server operating system.</span></span> |
| <span data-ttu-id="9732a-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="9732a-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span></span> | <span data-ttu-id="9732a-287">Merhaba bilgisayar adı öneki tüm hello sanal makineler için hello ölçek kümesinde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-287">Set hello computer name prefix for all  hello virtual machines in hello scale set.</span></span> |
| <span data-ttu-id="9732a-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span><span class="sxs-lookup"><span data-stu-id="9732a-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span></span> | <span data-ttu-id="9732a-289">Kullanıcı görüntüsü için Hello blob URI'si ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-289">Set hello blob URI for user image.</span></span> |
| <span data-ttu-id="9732a-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span><span class="sxs-lookup"><span data-stu-id="9732a-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span></span> | <span data-ttu-id="9732a-291">Merhaba ölçek kümesi için kullanılan toostore işletim sistemi diskler hello kapsayıcı URL'lerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-291">Set hello container URLs that are used toostore operating system disks for hello scale set.</span></span> |
| <span data-ttu-id="9732a-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span><span class="sxs-lookup"><span data-stu-id="9732a-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span></span> | <span data-ttu-id="9732a-293">Sanal makineler Hello boyutunu ölçek kümesinde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-293">Set hello size of virtual machines in a scale set.</span></span> |
| <span data-ttu-id="9732a-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span><span class="sxs-lookup"><span data-stu-id="9732a-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span></span> | <span data-ttu-id="9732a-295">Sanal makinelerin Hello katmanı ölçek kümesinde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-295">Set hello tier of virtual machines in a scale set.</span></span> |
  
<span data-ttu-id="9732a-296">**Microsoft.Network/applicationGateways**</span><span class="sxs-lookup"><span data-stu-id="9732a-296">**Microsoft.Network/applicationGateways**</span></span>

| <span data-ttu-id="9732a-297">Diğer ad</span><span class="sxs-lookup"><span data-stu-id="9732a-297">Alias</span></span> | <span data-ttu-id="9732a-298">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9732a-298">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="9732a-299">Microsoft.Network/applicationGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="9732a-299">Microsoft.Network/applicationGateways/sku.name</span></span> | <span data-ttu-id="9732a-300">Merhaba ağ geçidi Hello boyutunu ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-300">Set hello size of hello gateway.</span></span> |

<span data-ttu-id="9732a-301">**Microsoft.Network/virtualNetworkGateways**</span><span class="sxs-lookup"><span data-stu-id="9732a-301">**Microsoft.Network/virtualNetworkGateways**</span></span>

| <span data-ttu-id="9732a-302">Diğer ad</span><span class="sxs-lookup"><span data-stu-id="9732a-302">Alias</span></span> | <span data-ttu-id="9732a-303">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9732a-303">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="9732a-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span><span class="sxs-lookup"><span data-stu-id="9732a-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span></span> | <span data-ttu-id="9732a-305">Bu sanal ağ geçidi Hello türünü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-305">Set hello type of this virtual network gateway.</span></span> |
| <span data-ttu-id="9732a-306">Microsoft.Network/virtualNetworkGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="9732a-306">Microsoft.Network/virtualNetworkGateways/sku.name</span></span> | <span data-ttu-id="9732a-307">Merhaba ağ geçidi SKU adına ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-307">Set hello gateway SKU name.</span></span> |

<span data-ttu-id="9732a-308">**Microsoft.Sql/servers**</span><span class="sxs-lookup"><span data-stu-id="9732a-308">**Microsoft.Sql/servers**</span></span>

| <span data-ttu-id="9732a-309">Diğer ad</span><span class="sxs-lookup"><span data-stu-id="9732a-309">Alias</span></span> | <span data-ttu-id="9732a-310">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9732a-310">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="9732a-311">Microsoft.Sql/servers/version</span><span class="sxs-lookup"><span data-stu-id="9732a-311">Microsoft.Sql/servers/version</span></span> | <span data-ttu-id="9732a-312">Merhaba server Hello sürümünü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-312">Set hello version of hello server.</span></span> |

<span data-ttu-id="9732a-313">**Microsoft.Sql/databases**</span><span class="sxs-lookup"><span data-stu-id="9732a-313">**Microsoft.Sql/databases**</span></span>

| <span data-ttu-id="9732a-314">Diğer ad</span><span class="sxs-lookup"><span data-stu-id="9732a-314">Alias</span></span> | <span data-ttu-id="9732a-315">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9732a-315">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="9732a-316">Microsoft.Sql/servers/databases/edition</span><span class="sxs-lookup"><span data-stu-id="9732a-316">Microsoft.Sql/servers/databases/edition</span></span> | <span data-ttu-id="9732a-317">Merhaba veritabanı Hello sürümünü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-317">Set hello edition of hello database.</span></span> |
| <span data-ttu-id="9732a-318">Microsoft.Sql/servers/databases/elasticPoolName</span><span class="sxs-lookup"><span data-stu-id="9732a-318">Microsoft.Sql/servers/databases/elasticPoolName</span></span> | <span data-ttu-id="9732a-319">Merhaba esnek havuz hello veritabanının kümesi hello adı kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="9732a-319">Set hello name of hello elastic pool hello database is in.</span></span> |
| <span data-ttu-id="9732a-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span><span class="sxs-lookup"><span data-stu-id="9732a-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span></span> | <span data-ttu-id="9732a-321">Hello yapılandırılan hizmet düzeyi hedefi kimliği hello veritabanının ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-321">Set hello configured service level objective ID of hello database.</span></span> |
| <span data-ttu-id="9732a-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span><span class="sxs-lookup"><span data-stu-id="9732a-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span></span> | <span data-ttu-id="9732a-323">Merhaba hello yapılandırılan hizmet düzeyi hedefi hello veritabanının adını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-323">Set hello name of hello configured service level objective of hello database.</span></span>  |

<span data-ttu-id="9732a-324">**Microsoft.Sql/elasticpools**</span><span class="sxs-lookup"><span data-stu-id="9732a-324">**Microsoft.Sql/elasticpools**</span></span>

| <span data-ttu-id="9732a-325">Diğer ad</span><span class="sxs-lookup"><span data-stu-id="9732a-325">Alias</span></span> | <span data-ttu-id="9732a-326">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9732a-326">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="9732a-327">sunucuları/elasticpools</span><span class="sxs-lookup"><span data-stu-id="9732a-327">servers/elasticpools</span></span> | <span data-ttu-id="9732a-328">Microsoft.Sql/servers/elasticPools/dtu</span><span class="sxs-lookup"><span data-stu-id="9732a-328">Microsoft.Sql/servers/elasticPools/dtu</span></span> | <span data-ttu-id="9732a-329">Set hello toplam DTU hello veritabanı esnek havuz için paylaşılan.</span><span class="sxs-lookup"><span data-stu-id="9732a-329">Set hello total shared DTU for hello database elastic pool.</span></span> |
| <span data-ttu-id="9732a-330">sunucuları/elasticpools</span><span class="sxs-lookup"><span data-stu-id="9732a-330">servers/elasticpools</span></span> | <span data-ttu-id="9732a-331">Microsoft.Sql/servers/elasticPools/edition</span><span class="sxs-lookup"><span data-stu-id="9732a-331">Microsoft.Sql/servers/elasticPools/edition</span></span> | <span data-ttu-id="9732a-332">Merhaba esnek havuz Hello sürümünü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-332">Set hello edition of hello elastic pool.</span></span> |

<span data-ttu-id="9732a-333">**Microsoft.Storage/storageAccounts**</span><span class="sxs-lookup"><span data-stu-id="9732a-333">**Microsoft.Storage/storageAccounts**</span></span>

| <span data-ttu-id="9732a-334">Diğer ad</span><span class="sxs-lookup"><span data-stu-id="9732a-334">Alias</span></span> | <span data-ttu-id="9732a-335">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9732a-335">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="9732a-336">Microsoft.Storage/storageAccounts/accessTier</span><span class="sxs-lookup"><span data-stu-id="9732a-336">Microsoft.Storage/storageAccounts/accessTier</span></span> | <span data-ttu-id="9732a-337">Set hello erişim katmanı için fatura kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9732a-337">Set hello access tier used for billing.</span></span> |
| <span data-ttu-id="9732a-338">Microsoft.Storage/storageAccounts/accountType</span><span class="sxs-lookup"><span data-stu-id="9732a-338">Microsoft.Storage/storageAccounts/accountType</span></span> | <span data-ttu-id="9732a-339">Merhaba SKU adına ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-339">Set hello SKU name.</span></span> |
| <span data-ttu-id="9732a-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span><span class="sxs-lookup"><span data-stu-id="9732a-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span></span> | <span data-ttu-id="9732a-341">Merhaba blob depolama hizmetinde depolanan gibi hello hizmet hello verileri şifreler gerekip gerekmediğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="9732a-341">Set whether hello service encrypts hello data as it is stored in hello blob storage service.</span></span> |
| <span data-ttu-id="9732a-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span><span class="sxs-lookup"><span data-stu-id="9732a-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span></span> | <span data-ttu-id="9732a-343">Merhaba dosya depolama hizmetinde depolanan gibi hello hizmet hello verileri şifreler gerekip gerekmediğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="9732a-343">Set whether hello service encrypts hello data as it is stored in hello file storage service.</span></span> |
| <span data-ttu-id="9732a-344">Microsoft.Storage/storageAccounts/sku.name</span><span class="sxs-lookup"><span data-stu-id="9732a-344">Microsoft.Storage/storageAccounts/sku.name</span></span> | <span data-ttu-id="9732a-345">Merhaba SKU adına ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-345">Set hello SKU name.</span></span> |
| <span data-ttu-id="9732a-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span><span class="sxs-lookup"><span data-stu-id="9732a-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span></span> | <span data-ttu-id="9732a-347">Tooallow yalnızca https trafiği toostorage hizmetini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-347">Set tooallow only https traffic toostorage service.</span></span> |


## <a name="policy-examples"></a><span data-ttu-id="9732a-348">İlke örnekleri</span><span class="sxs-lookup"><span data-stu-id="9732a-348">Policy examples</span></span>

<span data-ttu-id="9732a-349">Aşağıdaki konularda hello ilkesi örnekleri içerir:</span><span class="sxs-lookup"><span data-stu-id="9732a-349">hello following topics contain policy examples:</span></span>

* <span data-ttu-id="9732a-350">Etiket örnekleri ilkeleri için bkz: [etiketleri için kaynak ilkelerini uygulamak](resource-manager-policy-tags.md).</span><span class="sxs-lookup"><span data-stu-id="9732a-350">For examples of tag polices, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>
* <span data-ttu-id="9732a-351">Adlandırma ve metin düzeni örnekleri için bkz: [adları ve metin için kaynak ilkelerini uygulamak](resource-manager-policy-naming-convention.md).</span><span class="sxs-lookup"><span data-stu-id="9732a-351">For examples of naming and text patterns, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>
* <span data-ttu-id="9732a-352">Depolama ilkeleri örnekleri için bkz: [kaynak ilkeleri toostorage hesapları geçerli](resource-manager-policy-storage.md).</span><span class="sxs-lookup"><span data-stu-id="9732a-352">For examples of storage policies, see [Apply resource policies toostorage accounts](resource-manager-policy-storage.md).</span></span>
* <span data-ttu-id="9732a-353">Sanal makine ilkeleri örnekleri için bkz: [kaynak ilkeleri tooLinux VM'ler uygulamak](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) ve [kaynak ilkeleri tooWindows VM'ler Uygula](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="9732a-353">For examples of virtual machine policies, see [Apply resource policies tooLinux VMs](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) and [Apply resource policies tooWindows VMs](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span></span>


## <a name="next-steps"></a><span data-ttu-id="9732a-354">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9732a-354">Next steps</span></span>
* <span data-ttu-id="9732a-355">İlke kuralı tanımladıktan sonra tooa kapsamı atayın.</span><span class="sxs-lookup"><span data-stu-id="9732a-355">After defining a policy rule, assign it tooa scope.</span></span> <span data-ttu-id="9732a-356">Merhaba portal aracılığıyla tooassign ilkeleri Bkz [kullanım Azure portal tooassign ve kaynak ilkelerini yönetme](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9732a-356">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="9732a-357">REST API'si, PowerShell veya Azure CLI aracılığıyla tooassign ilkeleri Bkz [atayın ve komut dosyası aracılığıyla ilkelerini yönetme](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="9732a-357">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="9732a-358">Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="9732a-358">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="9732a-359">Hello İlkesi Şema konumunda yayımlanır [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="9732a-359">hello policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

