---
title: "Etiketler için Azure kaynak ilkeleri | Microsoft Docs"
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
ms.openlocfilehash: 469bd8d637337e5900ea84c6bfaf88064695fb7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="apply-resource-policies-for-tags"></a><span data-ttu-id="e3250-103">Kaynak etiketleri için geçerlidir</span><span class="sxs-lookup"><span data-stu-id="e3250-103">Apply resource policies for tags</span></span>

<span data-ttu-id="e3250-104">Bu konu, etiketleri kaynaklarına tutarlı kullanımını sağlamak için uygulayabilirsiniz ortak ilke kuralları sağlar.</span><span class="sxs-lookup"><span data-stu-id="e3250-104">This topic provides common policy rules you can apply to ensure consistent use of tags on resources.</span></span>

<span data-ttu-id="e3250-105">Bir kaynak grubuna veya aboneliğe mevcut kaynaklarla bir etiket ilkesi uygulamak firmalarda geriye dönük İlkesi kaynaklarla için geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="e3250-105">Applying a tag policy to a resource group or subscription with existing resources does not retroactively apply the policy to those resources.</span></span> <span data-ttu-id="e3250-106">Bu kaynaklar ilkelerini zorlamak için var olan kaynaklar için bir güncelleştirme tetikler.</span><span class="sxs-lookup"><span data-stu-id="e3250-106">To enforce the policies on those resources, trigger an update to the existing resources.</span></span> <span data-ttu-id="e3250-107">Bu makalede, bir güncelleştirme tetiklemek için bir PowerShell örnek içerir.</span><span class="sxs-lookup"><span data-stu-id="e3250-107">This article includes a PowerShell example for triggering an update.</span></span>

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a><span data-ttu-id="e3250-108">Bir kaynak grubundaki tüm kaynakların bir etiketi/değer sahip olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="e3250-108">Ensure all resources in a resource group have a tag/value</span></span>

<span data-ttu-id="e3250-109">Ortak gerekli bir kaynak grubundaki tüm kaynakların bir özel etiket ve değerine sahip değildir.</span><span class="sxs-lookup"><span data-stu-id="e3250-109">A common requirement is that all resources in a resource group have a particular tag and value.</span></span> <span data-ttu-id="e3250-110">Bu gereksinime genellikle maliyetleri izlemek için bölümünüzün gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e3250-110">This requirement is often needed to track costs by department.</span></span> <span data-ttu-id="e3250-111">Aşağıdaki koşullar karşılanmalıdır:</span><span class="sxs-lookup"><span data-stu-id="e3250-111">The following conditions must be met:</span></span>

* <span data-ttu-id="e3250-112">Gerekli etiket ve değer etiketi olmayan yeni ve güncelleştirilmiş kaynaklara eklenir.</span><span class="sxs-lookup"><span data-stu-id="e3250-112">The required tag and value are appended to new and updated resources that do not have the tag.</span></span>
* <span data-ttu-id="e3250-113">Tüm mevcut kaynaklardan değeri ve gerekli etiketi kaldırılamaz.</span><span class="sxs-lookup"><span data-stu-id="e3250-113">The required tag and value cannot be removed from any existing resources.</span></span>

<span data-ttu-id="e3250-114">Bu gereksinim, bir kaynak grubuna iki yerleşik ilkeleri uygulayarak gerçekleştirmek.</span><span class="sxs-lookup"><span data-stu-id="e3250-114">You accomplish this requirement by applying two built-in policies to a resource group.</span></span>

| <span data-ttu-id="e3250-115">Kimlik</span><span class="sxs-lookup"><span data-stu-id="e3250-115">ID</span></span> | <span data-ttu-id="e3250-116">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e3250-116">Description</span></span> |
| ---- | ---- |
| <span data-ttu-id="e3250-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span><span class="sxs-lookup"><span data-stu-id="e3250-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span></span> | <span data-ttu-id="e3250-118">Kullanıcı tarafından belirtilmediğinde gerekli bir etiket ve varsayılan değerini geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="e3250-118">Applies a required tag and its default value when it is not specified by the user.</span></span> |
| <span data-ttu-id="e3250-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span><span class="sxs-lookup"><span data-stu-id="e3250-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span></span> | <span data-ttu-id="e3250-120">Gerekli bir etiket ve değerini zorlar.</span><span class="sxs-lookup"><span data-stu-id="e3250-120">Enforces a required tag and its value.</span></span> |

### <a name="powershell"></a><span data-ttu-id="e3250-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3250-121">PowerShell</span></span>

<span data-ttu-id="e3250-122">Aşağıdaki PowerShell betiğini iki yerleşik ilke tanımları bir kaynak grubuna atar.</span><span class="sxs-lookup"><span data-stu-id="e3250-122">The following PowerShell script assigns the two built-in policy definitions to a resource group.</span></span> <span data-ttu-id="e3250-123">Komut dosyasını çalıştırmadan önce tüm gerekli etiketleri kaynak grubuna atayın.</span><span class="sxs-lookup"><span data-stu-id="e3250-123">Before running the script, assign all required tags to the resource group.</span></span> <span data-ttu-id="e3250-124">Kaynak grubunda bulunan her bir etiketin grubundaki kaynaklar için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e3250-124">Each tag on the resource group is required for the resources in the group.</span></span> <span data-ttu-id="e3250-125">Aboneliğinizdeki tüm kaynak grupları atamak için sağlıyor mu `-Name` kaynak gruplarını alırken parametresi.</span><span class="sxs-lookup"><span data-stu-id="e3250-125">To assign to all resource groups in your subscription, do not provide the `-Name` parameter when getting the resource groups.</span></span>

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

<span data-ttu-id="e3250-126">İlkeleri atadıktan sonra eklediğiniz etiketi ilkelerini zorlamak için var olan tüm kaynaklar için bir güncelleştirme tetikleyebilir.</span><span class="sxs-lookup"><span data-stu-id="e3250-126">After assigning the policies, you can trigger an update to all existing resources to enforce the tag policies you have added.</span></span> <span data-ttu-id="e3250-127">Aşağıdaki komut dosyası kaynaklardaki varolan herhangi bir etiket korur:</span><span class="sxs-lookup"><span data-stu-id="e3250-127">The following script retains any other tags that existed on the resources:</span></span>

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

## <a name="require-tags-for-a-resource-type"></a><span data-ttu-id="e3250-128">Bir kaynak türü için etiketler gerektirir</span><span class="sxs-lookup"><span data-stu-id="e3250-128">Require tags for a resource type</span></span>
<span data-ttu-id="e3250-129">Aşağıdaki örnek, bir uygulama etiketi yalnızca bir belirtilen kaynak türü (Bu durumda, depolama hesapları için) istemek için mantıksal işleçler iç içe gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e3250-129">The following example shows how to nest logical operators to require an application tag for only a specified resource type (in this case, storage accounts).</span></span>

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

## <a name="require-tag"></a><span data-ttu-id="e3250-130">Etiket gerektirir</span><span class="sxs-lookup"><span data-stu-id="e3250-130">Require tag</span></span>
<span data-ttu-id="e3250-131">Aşağıdaki ilke (herhangi bir değer uygulanabilir) "costCenter" anahtarı içeren bir etiket yok istekleri engeller:</span><span class="sxs-lookup"><span data-stu-id="e3250-131">The following policy denies requests that don't have a tag containing "costCenter" key (any value can be applied):</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e3250-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e3250-132">Next steps</span></span>
* <span data-ttu-id="e3250-133">(Yukarıdaki örneklerde gösterildiği gibi) bir ilke kuralı tanımladıktan sonra ilke tanımı oluşturun ve bir kapsama atamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e3250-133">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="e3250-134">Kapsamı bir abonelik, kaynak grubu veya kaynak olabilir.</span><span class="sxs-lookup"><span data-stu-id="e3250-134">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="e3250-135">Portal üzerinden ilkeler atamak için bkz: [atamak ve kaynak ilkelerini yönetmek için kullanım Azure portal](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e3250-135">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="e3250-136">REST API'si, PowerShell veya Azure CLI aracılığıyla ilkeleri atamak için bkz: [atayın ve komut dosyası aracılığıyla ilkelerini yönetme](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="e3250-136">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="e3250-137">Kaynak ilkelerini giriş için bkz: [kaynak ilkesine genel bakış](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="e3250-137">For an introduction to resource policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="e3250-138">Kuruluşların abonelikleri etkili bir şekilde yönetmek için Resource Manager'ı nasıl kullanabileceği hakkında yönergeler için bkz. [Azure kurumsal iskelesi: öngörücü abonelik idaresi](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="e3250-138">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

