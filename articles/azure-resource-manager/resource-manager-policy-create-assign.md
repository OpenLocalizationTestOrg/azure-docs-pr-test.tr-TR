---
title: "aaaAssign ve Azure kaynak ilkelerini yönetme | Microsoft Docs"
description: "Açıklar nasıl tooapply Azure kaynak ilkeleri toosubscriptions ve kaynak grupları ve nasıl tooview kaynak ilkeleri."
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
ms.date: 07/26/2017
ms.author: tomfitz
ms.openlocfilehash: b6999b43bbcc80d2fde9911352fd4352fa453443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-and-manage-resource-policies"></a><span data-ttu-id="94d55-103">Atama ve kaynak ilkelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="94d55-103">Assign and manage resource policies</span></span>

<span data-ttu-id="94d55-104">tooimplement bir ilke, şu adımları gerçekleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="94d55-104">tooimplement a policy, you must perform these steps:</span></span>

1. <span data-ttu-id="94d55-105">Gereksinimlerinizi karşılayan, aboneliğinizde zaten varsa, ilke tanımları (Azure tarafından sağlanan yerleşik ilkeleri dahil) toosee denetleyin.</span><span class="sxs-lookup"><span data-stu-id="94d55-105">Check policy definitions (including built-in policies provided by Azure) toosee if one already exists in your subscription that fulfills your requirements.</span></span>
2. <span data-ttu-id="94d55-106">Varsa, adını alın.</span><span class="sxs-lookup"><span data-stu-id="94d55-106">If one exists, get its name.</span></span>
3. <span data-ttu-id="94d55-107">Bir mevcut değilse, JSON hello İlkesi kuralıyla tanımlamak ve bir ilke tanımı aboneliğinizde olarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="94d55-107">If one does not exist, define hello policy rule with JSON, and add it as a policy definition in your subscription.</span></span> <span data-ttu-id="94d55-108">Bu adım hello ilke ataması için kullanılabilir hale getirir, ancak hello kuralları tooyour abonelik geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="94d55-108">This step makes hello policy available for assignment but does not apply hello rules tooyour subscription.</span></span>
4. <span data-ttu-id="94d55-109">Her iki durumda da hello İlkesi tooa kapsam (örneğin, bir abonelik veya kaynak grubu) atayın.</span><span class="sxs-lookup"><span data-stu-id="94d55-109">For either case, assign hello policy tooa scope (such as a subscription or resource group).</span></span> <span data-ttu-id="94d55-110">Merhaba kuralı hello İlkesi artık zorunlu tutulmaz.</span><span class="sxs-lookup"><span data-stu-id="94d55-110">hello rules of hello policy are now enforced.</span></span>

<span data-ttu-id="94d55-111">Bu makalede bir ilke tanımı hello adımları toocreate üzerinde odaklanır ve REST API'si, PowerShell veya Azure CLI aracılığıyla, tanım tooa kapsamı atayın.</span><span class="sxs-lookup"><span data-stu-id="94d55-111">This article focuses on hello steps toocreate a policy definition and assign that definition tooa scope through REST API, PowerShell, or Azure CLI.</span></span> <span data-ttu-id="94d55-112">Toouse hello portal tooassign ilkeleri tercih ederseniz, bkz. [kullanım Azure portal tooassign ve kaynak ilkelerini yönetme](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="94d55-112">If you prefer toouse hello portal tooassign policies, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="94d55-113">Bu makalede hello ilke tanımı oluşturmak için hello sözdizimi odaklanılmaktadır değil.</span><span class="sxs-lookup"><span data-stu-id="94d55-113">This article does not focus on hello syntax for creating hello policy definition.</span></span> <span data-ttu-id="94d55-114">İlke sözdizimi hakkında daha fazla bilgi için bkz: [kaynak ilkesine genel bakış](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="94d55-114">For information about policy syntax, see [Resource policy overview](resource-manager-policy.md).</span></span>

## <a name="rest-api"></a><span data-ttu-id="94d55-115">REST API</span><span class="sxs-lookup"><span data-stu-id="94d55-115">REST API</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="94d55-116">İlke tanımı oluşturun</span><span class="sxs-lookup"><span data-stu-id="94d55-116">Create policy definition</span></span>

<span data-ttu-id="94d55-117">Merhaba ile bir ilke oluşturabilirsiniz [ilke tanımları için REST API](/rest/api/resources/policydefinitions).</span><span class="sxs-lookup"><span data-stu-id="94d55-117">You can create a policy with hello [REST API for Policy Definitions](/rest/api/resources/policydefinitions).</span></span> <span data-ttu-id="94d55-118">Merhaba REST API toocreate sağlar ve ilke tanımları silin ve varolan tanımları hakkında bilgi alın.</span><span class="sxs-lookup"><span data-stu-id="94d55-118">hello REST API enables you toocreate and delete policy definitions, and get information about existing definitions.</span></span>

<span data-ttu-id="94d55-119">bir ilke tanımı toocreate çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="94d55-119">toocreate a policy definition, run:</span></span>

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

<span data-ttu-id="94d55-120">Aşağıdaki örnek istek gövdesi benzer bir toohello şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="94d55-120">Include a request body similar toohello following example:</span></span>

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

### <a name="assign-policy"></a><span data-ttu-id="94d55-121">İlke atama</span><span class="sxs-lookup"><span data-stu-id="94d55-121">Assign policy</span></span>

<span data-ttu-id="94d55-122">Merhaba ilke tanımı hello aracılığıyla istenen hello kapsamda uygulayabilirsiniz [ilke atamaları için REST API](/rest/api/resources/policyassignments).</span><span class="sxs-lookup"><span data-stu-id="94d55-122">You can apply hello policy definition at hello desired scope through hello [REST API for policy assignments](/rest/api/resources/policyassignments).</span></span> <span data-ttu-id="94d55-123">Merhaba REST API toocreate sağlar ve ilke atamalarını silin ve varolan atamaları hakkında bilgi alın.</span><span class="sxs-lookup"><span data-stu-id="94d55-123">hello REST API enables you toocreate and delete policy assignments, and get information about existing assignments.</span></span>

<span data-ttu-id="94d55-124">bir ilke atamasını toocreate çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="94d55-124">toocreate a policy assignment, run:</span></span>

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

<span data-ttu-id="94d55-125">Merhaba {ilke ataması} hello ilke ataması hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="94d55-125">hello {policy-assignment} is hello name of hello policy assignment.</span></span>

<span data-ttu-id="94d55-126">Aşağıdaki örnek istek gövdesi benzer bir toohello şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="94d55-126">Include a request body similar toohello following example:</span></span>

```json
{
  "properties":{
    "displayName":"West US only policy assignment on hello subscription ",
    "description":"Resources can only be provisioned in West US regions",
    "parameters": {
      "allowedLocations": { "value": ["northeurope", "westus"] }
     },
    "policyDefinitionId":"/subscriptions/{subscription-id}/providers/Microsoft.Authorization/policyDefinitions/{definition-name}",
      "scope":"/subscriptions/{subscription-id}"
  },
}
```

### <a name="view-policy"></a><span data-ttu-id="94d55-127">İlkesini görüntüle</span><span class="sxs-lookup"><span data-stu-id="94d55-127">View policy</span></span>
<span data-ttu-id="94d55-128">tooget bir ilke kullanmak hello [alma ilke tanımı](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) işlemi.</span><span class="sxs-lookup"><span data-stu-id="94d55-128">tooget a policy, use hello [Get policy definition](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operation.</span></span>

### <a name="get-aliases"></a><span data-ttu-id="94d55-129">Diğer adlar Al</span><span class="sxs-lookup"><span data-stu-id="94d55-129">Get aliases</span></span>
<span data-ttu-id="94d55-130">Diğer adlar hello REST API aracılığıyla alabilir:</span><span class="sxs-lookup"><span data-stu-id="94d55-130">You can retrieve aliases through hello REST API:</span></span>

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

<span data-ttu-id="94d55-131">Aşağıdaki örneğine hello bir diğer ad tanımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="94d55-131">hello following example shows a definition of an alias.</span></span> <span data-ttu-id="94d55-132">Gördüğünüz gibi bir özellik adı değişikliği olduğunda bile bir diğer ad yolları farklı API sürümlerde tanımlar.</span><span class="sxs-lookup"><span data-stu-id="94d55-132">As you can see, an alias defines paths in different API versions, even when there is a property name change.</span></span> 

```json
"aliases": [
    {
      "name": "Microsoft.Storage/storageAccounts/sku.name",
      "paths": [
        {
          "path": "properties.accountType",
          "apiVersions": [
            "2015-06-15",
            "2015-05-01-preview"
          ]
        },
        {
          "path": "sku.name",
          "apiVersions": [
            "2016-01-01"
          ]
        }
      ]
    }
]
```

## <a name="powershell"></a><span data-ttu-id="94d55-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="94d55-133">PowerShell</span></span>

<span data-ttu-id="94d55-134">Merhaba PowerShell örnekleriyle devam etmeden önce olduğundan emin olun [hello son sürümü yüklü](/powershell/azure/install-azurerm-ps) Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="94d55-134">Before proceeding with hello PowerShell examples, make sure you have [installed hello latest version](/powershell/azure/install-azurerm-ps) of Azure PowerShell.</span></span> <span data-ttu-id="94d55-135">İlke parametreleri sürüm 3.6.0 eklendi.</span><span class="sxs-lookup"><span data-stu-id="94d55-135">Policy parameters were added in version 3.6.0.</span></span> <span data-ttu-id="94d55-136">Önceki bir sürümü varsa, bir hata belirten hello parametresi bulunamıyor hello örnekler döndür.</span><span class="sxs-lookup"><span data-stu-id="94d55-136">If you have an earlier version, hello examples return an error indicating hello parameter cannot be found.</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="94d55-137">Görünüm ilke tanımları</span><span class="sxs-lookup"><span data-stu-id="94d55-137">View policy definitions</span></span>
<span data-ttu-id="94d55-138">toosee aşağıdaki kullanım hello aboneliğinizde tüm ilke tanımları komutu:</span><span class="sxs-lookup"><span data-stu-id="94d55-138">toosee all policy definitions in your subscription, use hello following command:</span></span>

```powershell
Get-AzureRmPolicyDefinition
```

<span data-ttu-id="94d55-139">Yerleşik ilkeleri de dahil olmak üzere tüm kullanılabilir ilke tanımları döndürür.</span><span class="sxs-lookup"><span data-stu-id="94d55-139">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="94d55-140">Her ilke biçimini izleyen hello verilir:</span><span class="sxs-lookup"><span data-stu-id="94d55-140">Each policy is returned in hello following format:</span></span>

```powershell
Name               : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceId         : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceName       : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceType       : Microsoft.Authorization/policyDefinitions
Properties         : @{displayName=Allowed locations; policyType=BuiltIn; description=This policy enables you to
                     restrict hello locations your organization can specify when deploying resources. Use tooenforce
                     your geo-compliance requirements.; parameters=; policyRule=}
PolicyDefinitionId : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
```

<span data-ttu-id="94d55-141">Devam etmeden toocreate bir ilke tanımı önce hello yerleşik ilkelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="94d55-141">Before proceeding toocreate a policy definition, look at hello built-in policies.</span></span> <span data-ttu-id="94d55-142">Gereksinim duyduğunuz hello limitleri geçerlidir yerleşik bir ilke bulursanız, bir ilke tanımı oluşturma atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94d55-142">If you find a built-in policy that applies hello limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="94d55-143">Bunun yerine, hello yerleşik ilke istenen toohello kapsamı atayın.</span><span class="sxs-lookup"><span data-stu-id="94d55-143">Instead, assign hello built-in policy toohello desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="94d55-144">İlke tanımı oluşturun</span><span class="sxs-lookup"><span data-stu-id="94d55-144">Create policy definition</span></span>
<span data-ttu-id="94d55-145">Hello kullanarak bir ilke tanımı oluşturabilirsiniz `New-AzureRmPolicyDefinition` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="94d55-145">You can create a policy definition using hello `New-AzureRmPolicyDefinition` cmdlet.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy '{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}'
```            

<span data-ttu-id="94d55-146">Merhaba çıkış depolanır bir `$definition` ilke ataması sırasında kullanılan nesne.</span><span class="sxs-lookup"><span data-stu-id="94d55-146">hello output is stored in a `$definition` object, which is used during policy assignment.</span></span> 

<span data-ttu-id="94d55-147">Parametre olarak Hello JSON belirtmek yerine hello İlkesi kuralı içeren hello yolu tooa .json dosyası sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94d55-147">Rather than specifying hello JSON as a parameter, you can provide hello path tooa .json file containing hello policy rule.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy "c:\policies\coolAccessTier.json"
```

<span data-ttu-id="94d55-148">Merhaba aşağıdaki örnek parametreleri içeren bir ilke tanımı oluşturur:</span><span class="sxs-lookup"><span data-stu-id="94d55-148">hello following example creates a policy definition that includes parameters:</span></span>

```powershell
$policy = '{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Storage/storageAccounts"
            },
            {
                "not": {
                    "field": "location",
                    "in": "[parameters(''allowedLocations'')]"
                }
            }
        ]
    },
    "then": {
        "effect": "Deny"
    }
}'

$parameters = '{
    "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying storage accounts.",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
    }
}' 

$definition = New-AzureRmPolicyDefinition -Name storageLocations -Description "Policy toospecify locations for storage accounts." -Policy $policy -Parameter $parameters 
```

### <a name="assign-policy"></a><span data-ttu-id="94d55-149">İlke atama</span><span class="sxs-lookup"><span data-stu-id="94d55-149">Assign policy</span></span>

<span data-ttu-id="94d55-150">Hello kullanarak istenen hello kapsamlı hello ilkesi uygulamak `New-AzureRmPolicyAssignment` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="94d55-150">You apply hello policy at hello desired scope by using hello `New-AzureRmPolicyAssignment` cmdlet.</span></span> <span data-ttu-id="94d55-151">Aşağıdaki örnek hello hello İlkesi tooa kaynak grubu atar.</span><span class="sxs-lookup"><span data-stu-id="94d55-151">hello following example assigns hello policy tooa resource group.</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

<span data-ttu-id="94d55-152">tooassign parametreler gerektiren bir ilke oluşturun ve bu değerleri nesne.</span><span class="sxs-lookup"><span data-stu-id="94d55-152">tooassign a policy that requires parameters, create and object with those values.</span></span> <span data-ttu-id="94d55-153">Hello aşağıdaki örnekte bir yerleşik ilkesini alır ve parametre değerlerini geçirir:</span><span class="sxs-lookup"><span data-stu-id="94d55-153">hello following example retrieves a built-in policy and passes in parameters values:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a><span data-ttu-id="94d55-154">Görünüm ilke ataması</span><span class="sxs-lookup"><span data-stu-id="94d55-154">View policy assignment</span></span>

<span data-ttu-id="94d55-155">belirli bir ilke ataması tooget kullanın:</span><span class="sxs-lookup"><span data-stu-id="94d55-155">tooget a specific policy assignment, use:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

<span data-ttu-id="94d55-156">tooview hello İlkesi kuralı bir ilke tanımı kullanın:</span><span class="sxs-lookup"><span data-stu-id="94d55-156">tooview hello policy rule for a policy definition, use:</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="94d55-157">İlke atamasını Kaldır</span><span class="sxs-lookup"><span data-stu-id="94d55-157">Remove policy assignment</span></span> 

<span data-ttu-id="94d55-158">bir ilke atamasını tooremove kullanın:</span><span class="sxs-lookup"><span data-stu-id="94d55-158">tooremove a policy assignment, use:</span></span>

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a><span data-ttu-id="94d55-159">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="94d55-159">Azure CLI</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="94d55-160">Görünüm ilke tanımları</span><span class="sxs-lookup"><span data-stu-id="94d55-160">View policy definitions</span></span>
<span data-ttu-id="94d55-161">toosee aşağıdaki kullanım hello aboneliğinizde tüm ilke tanımları komutu:</span><span class="sxs-lookup"><span data-stu-id="94d55-161">toosee all policy definitions in your subscription, use hello following command:</span></span>

```azurecli
az policy definition list
```

<span data-ttu-id="94d55-162">Yerleşik ilkeleri de dahil olmak üzere tüm kullanılabilir ilke tanımları döndürür.</span><span class="sxs-lookup"><span data-stu-id="94d55-162">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="94d55-163">Her ilke biçimini izleyen hello verilir:</span><span class="sxs-lookup"><span data-stu-id="94d55-163">Each policy is returned in hello following format:</span></span>

```azurecli
{                                                            
  "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources. Use tooenforce your geo-compliance requirements.",                      
  "displayName": "Allowed locations",
  "id": "/providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c",
  "name": "e56962a6-4747-49cd-b67b-bf8b01975c4c",
  "policyRule": {
    "if": {
      "not": {
        "field": "location",
        "in": "[parameters('listOfAllowedLocations')]"
      }
    },
    "then": {
      "effect": "Deny"
    }
  },
  "policyType": "BuiltIn"
}
```

<span data-ttu-id="94d55-164">Devam etmeden toocreate bir ilke tanımı önce hello yerleşik ilkelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="94d55-164">Before proceeding toocreate a policy definition, look at hello built-in policies.</span></span> <span data-ttu-id="94d55-165">Gereksinim duyduğunuz hello limitleri geçerlidir yerleşik bir ilke bulursanız, bir ilke tanımı oluşturma atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94d55-165">If you find a built-in policy that applies hello limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="94d55-166">Bunun yerine, hello yerleşik ilke istenen toohello kapsamı atayın.</span><span class="sxs-lookup"><span data-stu-id="94d55-166">Instead, assign hello built-in policy toohello desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="94d55-167">İlke tanımı oluşturun</span><span class="sxs-lookup"><span data-stu-id="94d55-167">Create policy definition</span></span>

<span data-ttu-id="94d55-168">Merhaba ilke tanımı komutu ile Azure CLI kullanarak bir ilke tanımı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94d55-168">You can create a policy definition using Azure CLI with hello policy definition command.</span></span>

```azurecli
az policy definition create --name coolAccessTier --description "Policy toospecify access tier." --rules '{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}'    
```

### <a name="assign-policy"></a><span data-ttu-id="94d55-169">İlke atama</span><span class="sxs-lookup"><span data-stu-id="94d55-169">Assign policy</span></span>

<span data-ttu-id="94d55-170">Merhaba ilke ataması komutunu kullanarak hello İlkesi istenen toohello kapsam uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94d55-170">You can apply hello policy toohello desired scope by using hello policy assignment command.</span></span> <span data-ttu-id="94d55-171">Aşağıdaki örnek hello İlkesi tooa kaynak grubu atar.</span><span class="sxs-lookup"><span data-stu-id="94d55-171">hello following example assigns a policy tooa resource group.</span></span>

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a><span data-ttu-id="94d55-172">Görünüm ilke ataması</span><span class="sxs-lookup"><span data-stu-id="94d55-172">View policy assignment</span></span>

<span data-ttu-id="94d55-173">bir ilke atamasını tooview hello ilke ataması adı ve hello kapsam sağlar:</span><span class="sxs-lookup"><span data-stu-id="94d55-173">tooview a policy assignment, provide hello policy assignment name and hello scope:</span></span>

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="94d55-174">İlke atamasını Kaldır</span><span class="sxs-lookup"><span data-stu-id="94d55-174">Remove policy assignment</span></span> 

<span data-ttu-id="94d55-175">bir ilke atamasını tooremove kullanın:</span><span class="sxs-lookup"><span data-stu-id="94d55-175">tooremove a policy assignment, use:</span></span>

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a><span data-ttu-id="94d55-176">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="94d55-176">Next steps</span></span>
* <span data-ttu-id="94d55-177">Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="94d55-177">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

