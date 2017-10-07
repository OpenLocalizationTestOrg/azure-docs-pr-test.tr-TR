---
title: "etiketleri için aaaAzure kaynak ilkeleri | Microsoft Docs"
description: "Etiketler kaynaklardaki yönetmek için kaynak ilkeleri örnekleri sağlar"
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
ms.date: 08/24/2017
ms.author: tomfitz
ms.openlocfilehash: 5a5b3d5ed52b47544b397694b9da0070f61b1faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-tags"></a><span data-ttu-id="d0773-103">Kaynak etiketleri için geçerlidir</span><span class="sxs-lookup"><span data-stu-id="d0773-103">Apply resource policies for tags</span></span>

<span data-ttu-id="d0773-104">Bu konu, kaynakları tooensure tutarlı etiketleri kullanımını uygulayabilirsiniz ortak ilke kuralları sağlar.</span><span class="sxs-lookup"><span data-stu-id="d0773-104">This topic provides common policy rules you can apply tooensure consistent use of tags on resources.</span></span>

<span data-ttu-id="d0773-105">Bir etiketi İlkesi tooa kaynak grubuna veya aboneliğe mevcut kaynaklarla uygulama firmalarda geriye dönük hello İlkesi toothose kaynaklar için geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="d0773-105">Applying a tag policy tooa resource group or subscription with existing resources does not retroactively apply hello policy toothose resources.</span></span> <span data-ttu-id="d0773-106">Bu kaynaklar üzerindeki tooenforce hello ilkeleri kaynakları var olan bir güncelleştirme toohello tetikler.</span><span class="sxs-lookup"><span data-stu-id="d0773-106">tooenforce hello policies on those resources, trigger an update toohello existing resources.</span></span> <span data-ttu-id="d0773-107">Bu makalede, bir güncelleştirme tetiklemek için bir PowerShell örnek içerir.</span><span class="sxs-lookup"><span data-stu-id="d0773-107">This article includes a PowerShell example for triggering an update.</span></span>

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a><span data-ttu-id="d0773-108">Bir kaynak grubundaki tüm kaynakların bir etiketi/değer sahip olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="d0773-108">Ensure all resources in a resource group have a tag/value</span></span>

<span data-ttu-id="d0773-109">Ortak gerekli bir kaynak grubundaki tüm kaynakların bir özel etiket ve değerine sahip değildir.</span><span class="sxs-lookup"><span data-stu-id="d0773-109">A common requirement is that all resources in a resource group have a particular tag and value.</span></span> <span data-ttu-id="d0773-110">Bu gereksinim gerekli tootrack maliyetleri departmanı tarafından görülür.</span><span class="sxs-lookup"><span data-stu-id="d0773-110">This requirement is often needed tootrack costs by department.</span></span> <span data-ttu-id="d0773-111">hello aşağıdaki koşullar karşılanmalıdır:</span><span class="sxs-lookup"><span data-stu-id="d0773-111">hello following conditions must be met:</span></span>

* <span data-ttu-id="d0773-112">Merhaba, etiket ve değer eklenmiş toonew ve hello etiketi olmayan kaynakları güncelleştirilmiş gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d0773-112">hello required tag and value are appended toonew and updated resources that do not have hello tag.</span></span>
* <span data-ttu-id="d0773-113">Etiket Hello gerekli ve tüm mevcut kaynaklardan değeri kaldırılamaz.</span><span class="sxs-lookup"><span data-stu-id="d0773-113">hello required tag and value cannot be removed from any existing resources.</span></span>

<span data-ttu-id="d0773-114">Bu gereksinim, iki yerleşik ilkeleri tooa kaynak grubu uygulayarak gerçekleştirmek.</span><span class="sxs-lookup"><span data-stu-id="d0773-114">You accomplish this requirement by applying two built-in policies tooa resource group.</span></span>

| <span data-ttu-id="d0773-115">Kimlik</span><span class="sxs-lookup"><span data-stu-id="d0773-115">ID</span></span> | <span data-ttu-id="d0773-116">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d0773-116">Description</span></span> |
| ---- | ---- |
| <span data-ttu-id="d0773-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span><span class="sxs-lookup"><span data-stu-id="d0773-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span></span> | <span data-ttu-id="d0773-118">Merhaba kullanıcı tarafından belirtilmediğinde gerekli bir etiket ve varsayılan değerini geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d0773-118">Applies a required tag and its default value when it is not specified by hello user.</span></span> |
| <span data-ttu-id="d0773-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span><span class="sxs-lookup"><span data-stu-id="d0773-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span></span> | <span data-ttu-id="d0773-120">Gerekli bir etiket ve değerini zorlar.</span><span class="sxs-lookup"><span data-stu-id="d0773-120">Enforces a required tag and its value.</span></span> |

### <a name="powershell"></a><span data-ttu-id="d0773-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d0773-121">PowerShell</span></span>

<span data-ttu-id="d0773-122">PowerShell Betiği aşağıdaki hello hello iki yerleşik ilke tanımları tooa kaynak grubu atar.</span><span class="sxs-lookup"><span data-stu-id="d0773-122">hello following PowerShell script assigns hello two built-in policy definitions tooa resource group.</span></span> <span data-ttu-id="d0773-123">Merhaba betiği çalıştırmadan önce tüm gerekli etiketleri toohello kaynak grubu atayın.</span><span class="sxs-lookup"><span data-stu-id="d0773-123">Before running hello script, assign all required tags toohello resource group.</span></span> <span data-ttu-id="d0773-124">Her etiket hello kaynak grubu üzerinde hello grubundaki hello kaynaklar için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d0773-124">Each tag on hello resource group is required for hello resources in hello group.</span></span> <span data-ttu-id="d0773-125">tooassign tooall kaynak grupları, aboneliğinizdeki hello sağlamaz `-Name` hello kaynak grupları alınırken parametresi.</span><span class="sxs-lookup"><span data-stu-id="d0773-125">tooassign tooall resource groups in your subscription, do not provide hello `-Name` parameter when getting hello resource groups.</span></span>

```powershell
$appendpolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '2a0e14a6-b0a6-4fab-991a-187a4f81c498'}
$denypolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '1e30110a-5ceb-460c-a204-c1c3969c6d62'}

$rgs = Get-AzureRMResourceGroup -Name ExampleGroup

foreach($rg in $rgs)
{
    $tags = $rg.Tags
    foreach($key in $tags.Keys){
        $key 
        $tags[$key]
        New-AzureRmPolicyAssignment -Name ("append"+$key+"tag") -PolicyDefinition $appendpolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
        New-AzureRmPolicyAssignment -Name ("denywithout"+$key+"tag") -PolicyDefinition $denypolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
    }
}
```

<span data-ttu-id="d0773-126">Merhaba ilkeleri atadıktan sonra eklediğiniz kaynakları tooenforce hello etiketi ilkeleri var olan bir güncelleştirme tooall tetikleyebilir.</span><span class="sxs-lookup"><span data-stu-id="d0773-126">After assigning hello policies, you can trigger an update tooall existing resources tooenforce hello tag policies you have added.</span></span> <span data-ttu-id="d0773-127">Merhaba aşağıdaki betiği hello kaynaklardaki varolan herhangi bir etiket korur:</span><span class="sxs-lookup"><span data-stu-id="d0773-127">hello following script retains any other tags that existed on hello resources:</span></span>

```powershell
$group = Get-AzureRmResourceGroup -Name "ExampleGroup" 

$resources = Find-AzureRmResource -ResourceGroupName $group.ResourceGroupName 

foreach($r in $resources)
{
    try{
        $r | Set-AzureRmResource -Tags ($a=if($r.Tags -eq $NULL) { @{}} else {$r.Tags}) -Force -UsePatchSemantics
    }
    catch{
        Write-Host  $r.ResourceId + "can't be updated"
    }
}
```

## <a name="require-tags-for-a-resource-type"></a><span data-ttu-id="d0773-128">Bir kaynak türü için etiketler gerektirir</span><span class="sxs-lookup"><span data-stu-id="d0773-128">Require tags for a resource type</span></span>
<span data-ttu-id="d0773-129">Aşağıdaki örnek hello toonest mantıksal işleçler toorequire bir uygulamanın nasıl etiketi yalnızca bir belirtilen kaynak türü için (Bu durumda, depolama hesapları için) gösterir.</span><span class="sxs-lookup"><span data-stu-id="d0773-129">hello following example shows how toonest logical operators toorequire an application tag for only a specified resource type (in this case, storage accounts).</span></span>

```json
{
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
    "then": {
        "effect": "audit"
    }
}
```

## <a name="require-tag"></a><span data-ttu-id="d0773-130">Etiket gerektirir</span><span class="sxs-lookup"><span data-stu-id="d0773-130">Require tag</span></span>
<span data-ttu-id="d0773-131">Merhaba aşağıdaki İlkesi (herhangi bir değer uygulanabilir) "costCenter" anahtarı içeren bir etiket yok isteklerini reddeder:</span><span class="sxs-lookup"><span data-stu-id="d0773-131">hello following policy denies requests that don't have a tag containing "costCenter" key (any value can be applied):</span></span>

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="d0773-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d0773-132">Next steps</span></span>
* <span data-ttu-id="d0773-133">(Örnekler önceki hello gösterildiği gibi) bir ilke kuralı tanımlama sonra toocreate hello ilke tanımı gerekir ve tooa kapsamı atayın.</span><span class="sxs-lookup"><span data-stu-id="d0773-133">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="d0773-134">Merhaba kapsam abonelik, kaynak grubu veya kaynak olabilir.</span><span class="sxs-lookup"><span data-stu-id="d0773-134">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="d0773-135">Merhaba portal aracılığıyla tooassign ilkeleri Bkz [kullanım Azure portal tooassign ve kaynak ilkelerini yönetme](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d0773-135">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="d0773-136">REST API'si, PowerShell veya Azure CLI aracılığıyla tooassign ilkeleri Bkz [atayın ve komut dosyası aracılığıyla ilkelerini yönetme](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="d0773-136">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="d0773-137">Bir giriş tooresource ilkeleri için bkz: [kaynak ilkesine genel bakış](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="d0773-137">For an introduction tooresource policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="d0773-138">Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="d0773-138">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

