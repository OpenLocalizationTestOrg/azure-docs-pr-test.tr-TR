---
title: "Atama ve Azure kaynak ilkelerini yönetme | Microsoft Docs"
description: "Abonelikleriniz ve kaynak gruplarınız için Azure kaynak ilkeleri uygulamak ve kaynak ilkeleri görüntülemeyi açıklar."
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
ms.openlocfilehash: b204cffa8fab0ad27a9f78a81c04f0a0225d95f5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="assign-and-manage-resource-policies"></a><span data-ttu-id="622d1-103">Atama ve kaynak ilkelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="622d1-103">Assign and manage resource policies</span></span>

<span data-ttu-id="622d1-104">Bir ilkeyi uygulamak için aşağıdaki adımları gerçekleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="622d1-104">To implement a policy, you must perform these steps:</span></span>

1. <span data-ttu-id="622d1-105">İlke tanımları (Azure tarafından sağlanan yerleşik ilkeleri dahil) denetleyin gereksinimlerinizi karşılayan, aboneliğinizde zaten bir tane varsa görmek için.</span><span class="sxs-lookup"><span data-stu-id="622d1-105">Check policy definitions (including built-in policies provided by Azure) to see if one already exists in your subscription that fulfills your requirements.</span></span>
2. <span data-ttu-id="622d1-106">Varsa, adını alın.</span><span class="sxs-lookup"><span data-stu-id="622d1-106">If one exists, get its name.</span></span>
3. <span data-ttu-id="622d1-107">Bir mevcut değilse, JSON İlkesi kuralıyla tanımlamak ve bir ilke tanımı aboneliğinizde olarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="622d1-107">If one does not exist, define the policy rule with JSON, and add it as a policy definition in your subscription.</span></span> <span data-ttu-id="622d1-108">Bu adım ilke ataması için kullanılabilir hale getirir, ancak kurallar aboneliğiniz için geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="622d1-108">This step makes the policy available for assignment but does not apply the rules to your subscription.</span></span>
4. <span data-ttu-id="622d1-109">Her iki durumda, ilke kapsamı (örneğin, bir abonelik veya kaynak grubu) atayın.</span><span class="sxs-lookup"><span data-stu-id="622d1-109">For either case, assign the policy to a scope (such as a subscription or resource group).</span></span> <span data-ttu-id="622d1-110">İlke kuralları zorunlu tutulmaz.</span><span class="sxs-lookup"><span data-stu-id="622d1-110">The rules of the policy are now enforced.</span></span>

<span data-ttu-id="622d1-111">Bu makalede, bir ilke tanımı oluşturun ve REST API'si, PowerShell veya Azure CLI aracılığıyla bir kapsam tanımın atamak için adımları odaklanır.</span><span class="sxs-lookup"><span data-stu-id="622d1-111">This article focuses on the steps to create a policy definition and assign that definition to a scope through REST API, PowerShell, or Azure CLI.</span></span> <span data-ttu-id="622d1-112">İlkeler atamak için bkz: Portalı'nı kullanmayı tercih ederseniz, [atamak ve kaynak ilkelerini yönetmek için kullanın Azure portal](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="622d1-112">If you prefer to use the portal to assign policies, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="622d1-113">Bu makalede ilke tanımı oluşturmak için söz dizimi odaklanılmaktadır değil.</span><span class="sxs-lookup"><span data-stu-id="622d1-113">This article does not focus on the syntax for creating the policy definition.</span></span> <span data-ttu-id="622d1-114">İlke sözdizimi hakkında daha fazla bilgi için bkz: [kaynak ilkesine genel bakış](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="622d1-114">For information about policy syntax, see [Resource policy overview](resource-manager-policy.md).</span></span>

## <a name="rest-api"></a><span data-ttu-id="622d1-115">REST API</span><span class="sxs-lookup"><span data-stu-id="622d1-115">REST API</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="622d1-116">İlke tanımı oluşturun</span><span class="sxs-lookup"><span data-stu-id="622d1-116">Create policy definition</span></span>

<span data-ttu-id="622d1-117">İle bir ilke oluşturduğunuzda [ilke tanımları için REST API](/rest/api/resources/policydefinitions).</span><span class="sxs-lookup"><span data-stu-id="622d1-117">You can create a policy with the [REST API for Policy Definitions](/rest/api/resources/policydefinitions).</span></span> <span data-ttu-id="622d1-118">REST API oluşturmak ve ilke tanımları silmek ve varolan tanımları hakkında bilgi almak etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="622d1-118">The REST API enables you to create and delete policy definitions, and get information about existing definitions.</span></span>

<span data-ttu-id="622d1-119">Bir ilke tanımı oluşturmak için çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="622d1-119">To create a policy definition, run:</span></span>

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

<span data-ttu-id="622d1-120">Aşağıdaki örneğe benzer bir istek gövdesi şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="622d1-120">Include a request body similar to the following example:</span></span>

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "The list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you to restrict the locations your organization can specify when deploying resources.",
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

### <a name="assign-policy"></a><span data-ttu-id="622d1-121">İlke atama</span><span class="sxs-lookup"><span data-stu-id="622d1-121">Assign policy</span></span>

<span data-ttu-id="622d1-122">İlke tanımı istenilen kapsamda uygulayabilirsiniz [ilke atamaları için REST API](/rest/api/resources/policyassignments).</span><span class="sxs-lookup"><span data-stu-id="622d1-122">You can apply the policy definition at the desired scope through the [REST API for policy assignments](/rest/api/resources/policyassignments).</span></span> <span data-ttu-id="622d1-123">REST API oluşturmak ve ilke atamalarını silin ve varolan atamaları hakkında bilgi almak etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="622d1-123">The REST API enables you to create and delete policy assignments, and get information about existing assignments.</span></span>

<span data-ttu-id="622d1-124">Bir ilke ataması oluşturmak için çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="622d1-124">To create a policy assignment, run:</span></span>

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

<span data-ttu-id="622d1-125">{İlkesi-atama} ilke ataması adıdır.</span><span class="sxs-lookup"><span data-stu-id="622d1-125">The {policy-assignment} is the name of the policy assignment.</span></span>

<span data-ttu-id="622d1-126">Aşağıdaki örneğe benzer bir istek gövdesi şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="622d1-126">Include a request body similar to the following example:</span></span>

```json
{
  "properties":{
    "displayName":"West US only policy assignment on the subscription ",
    "description":"Resources can only be provisioned in West US regions",
    "parameters": {
      "allowedLocations": { "value": ["northeurope", "westus"] }
     },
    "policyDefinitionId":"/subscriptions/{subscription-id}/providers/Microsoft.Authorization/policyDefinitions/{definition-name}",
      "scope":"/subscriptions/{subscription-id}"
  },
}
```

### <a name="view-policy"></a><span data-ttu-id="622d1-127">İlkesini görüntüle</span><span class="sxs-lookup"><span data-stu-id="622d1-127">View policy</span></span>
<span data-ttu-id="622d1-128">Bir ilkeyi almak üzere kullanmak [alma ilke tanımı](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) işlemi.</span><span class="sxs-lookup"><span data-stu-id="622d1-128">To get a policy, use the [Get policy definition](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operation.</span></span>

### <a name="get-aliases"></a><span data-ttu-id="622d1-129">Diğer adlar Al</span><span class="sxs-lookup"><span data-stu-id="622d1-129">Get aliases</span></span>
<span data-ttu-id="622d1-130">Diğer adlar REST API'si aracılığıyla alabilir:</span><span class="sxs-lookup"><span data-stu-id="622d1-130">You can retrieve aliases through the REST API:</span></span>

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

<span data-ttu-id="622d1-131">Aşağıdaki örnek, bir diğer ad tanımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="622d1-131">The following example shows a definition of an alias.</span></span> <span data-ttu-id="622d1-132">Gördüğünüz gibi bir özellik adı değişikliği olduğunda bile bir diğer ad yolları farklı API sürümlerde tanımlar.</span><span class="sxs-lookup"><span data-stu-id="622d1-132">As you can see, an alias defines paths in different API versions, even when there is a property name change.</span></span> 

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

## <a name="powershell"></a><span data-ttu-id="622d1-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="622d1-133">PowerShell</span></span>

<span data-ttu-id="622d1-134">PowerShell örnekleriyle devam etmeden önce olduğundan emin olun [en son sürümü yüklü](/powershell/azure/install-azurerm-ps) Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="622d1-134">Before proceeding with the PowerShell examples, make sure you have [installed the latest version](/powershell/azure/install-azurerm-ps) of Azure PowerShell.</span></span> <span data-ttu-id="622d1-135">İlke parametreleri sürüm 3.6.0 eklendi.</span><span class="sxs-lookup"><span data-stu-id="622d1-135">Policy parameters were added in version 3.6.0.</span></span> <span data-ttu-id="622d1-136">Önceki bir sürümü varsa, örnekleri parametresi bulunamıyor belirten bir hata döndürür.</span><span class="sxs-lookup"><span data-stu-id="622d1-136">If you have an earlier version, the examples return an error indicating the parameter cannot be found.</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="622d1-137">Görünüm ilke tanımları</span><span class="sxs-lookup"><span data-stu-id="622d1-137">View policy definitions</span></span>
<span data-ttu-id="622d1-138">Aboneliğinizdeki tüm ilke tanımları görmek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="622d1-138">To see all policy definitions in your subscription, use the following command:</span></span>

```powershell
Get-AzureRmPolicyDefinition
```

<span data-ttu-id="622d1-139">Yerleşik ilkeleri de dahil olmak üzere tüm kullanılabilir ilke tanımları döndürür.</span><span class="sxs-lookup"><span data-stu-id="622d1-139">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="622d1-140">Her ilke şu biçimde verilir:</span><span class="sxs-lookup"><span data-stu-id="622d1-140">Each policy is returned in the following format:</span></span>

```powershell
Name               : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceId         : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceName       : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceType       : Microsoft.Authorization/policyDefinitions
Properties         : @{displayName=Allowed locations; policyType=BuiltIn; description=This policy enables you to
                     restrict the locations your organization can specify when deploying resources. Use to enforce
                     your geo-compliance requirements.; parameters=; policyRule=}
PolicyDefinitionId : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
```

<span data-ttu-id="622d1-141">Bir ilke tanımı oluşturmak için devam etmeden önce yerleşik ilkelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="622d1-141">Before proceeding to create a policy definition, look at the built-in policies.</span></span> <span data-ttu-id="622d1-142">Gereksinim duyduğunuz limitleri geçerlidir yerleşik bir ilke bulursanız, bir ilke tanımı oluşturma atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="622d1-142">If you find a built-in policy that applies the limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="622d1-143">Bunun yerine, yerleşik ilkesini istenen kapsamı atayın.</span><span class="sxs-lookup"><span data-stu-id="622d1-143">Instead, assign the built-in policy to the desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="622d1-144">İlke tanımı oluşturun</span><span class="sxs-lookup"><span data-stu-id="622d1-144">Create policy definition</span></span>
<span data-ttu-id="622d1-145">Kullanarak bir ilke tanımı oluşturabilirsiniz `New-AzureRmPolicyDefinition` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="622d1-145">You can create a policy definition using the `New-AzureRmPolicyDefinition` cmdlet.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy to specify access tier." -Policy '{
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

<span data-ttu-id="622d1-146">Çıktı depolanan bir `$definition` ilke ataması sırasında kullanılan nesne.</span><span class="sxs-lookup"><span data-stu-id="622d1-146">The output is stored in a `$definition` object, which is used during policy assignment.</span></span> 

<span data-ttu-id="622d1-147">JSON parametre olarak belirtmek yerine, ilke kuralı içeren bir .json dosyası yolunu sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="622d1-147">Rather than specifying the JSON as a parameter, you can provide the path to a .json file containing the policy rule.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy to specify access tier." -Policy "c:\policies\coolAccessTier.json"
```

<span data-ttu-id="622d1-148">Aşağıdaki örnek, parametreleri içeren bir ilke tanımı oluşturur:</span><span class="sxs-lookup"><span data-stu-id="622d1-148">The following example creates a policy definition that includes parameters:</span></span>

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
          "description": "The list of locations that can be specified when deploying storage accounts.",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
    }
}' 

$definition = New-AzureRmPolicyDefinition -Name storageLocations -Description "Policy to specify locations for storage accounts." -Policy $policy -Parameter $parameters 
```

### <a name="assign-policy"></a><span data-ttu-id="622d1-149">İlke atama</span><span class="sxs-lookup"><span data-stu-id="622d1-149">Assign policy</span></span>

<span data-ttu-id="622d1-150">Kullanarak istenen kapsamı ilkesi uygulamak `New-AzureRmPolicyAssignment` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="622d1-150">You apply the policy at the desired scope by using the `New-AzureRmPolicyAssignment` cmdlet.</span></span> <span data-ttu-id="622d1-151">Aşağıdaki örnek, bir kaynak grubu için ilke atar.</span><span class="sxs-lookup"><span data-stu-id="622d1-151">The following example assigns the policy to a resource group.</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

<span data-ttu-id="622d1-152">Parametreler gerektiren bir ilke atamak için oluşturmak ve bu değerleri nesne.</span><span class="sxs-lookup"><span data-stu-id="622d1-152">To assign a policy that requires parameters, create and object with those values.</span></span> <span data-ttu-id="622d1-153">Aşağıdaki örnek, bir yerleşik ilkesini alır ve parametre değerleri geçirir:</span><span class="sxs-lookup"><span data-stu-id="622d1-153">The following example retrieves a built-in policy and passes in parameters values:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a><span data-ttu-id="622d1-154">Görünüm ilke ataması</span><span class="sxs-lookup"><span data-stu-id="622d1-154">View policy assignment</span></span>

<span data-ttu-id="622d1-155">Belirli bir ilke ataması almak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="622d1-155">To get a specific policy assignment, use:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

<span data-ttu-id="622d1-156">Bir ilke tanımı için ilke kuralı görüntülemek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="622d1-156">To view the policy rule for a policy definition, use:</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="622d1-157">İlke atamasını Kaldır</span><span class="sxs-lookup"><span data-stu-id="622d1-157">Remove policy assignment</span></span> 

<span data-ttu-id="622d1-158">Bir ilke atamasını kaldırmak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="622d1-158">To remove a policy assignment, use:</span></span>

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a><span data-ttu-id="622d1-159">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="622d1-159">Azure CLI</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="622d1-160">Görünüm ilke tanımları</span><span class="sxs-lookup"><span data-stu-id="622d1-160">View policy definitions</span></span>
<span data-ttu-id="622d1-161">Aboneliğinizdeki tüm ilke tanımları görmek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="622d1-161">To see all policy definitions in your subscription, use the following command:</span></span>

```azurecli
az policy definition list
```

<span data-ttu-id="622d1-162">Yerleşik ilkeleri de dahil olmak üzere tüm kullanılabilir ilke tanımları döndürür.</span><span class="sxs-lookup"><span data-stu-id="622d1-162">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="622d1-163">Her ilke şu biçimde verilir:</span><span class="sxs-lookup"><span data-stu-id="622d1-163">Each policy is returned in the following format:</span></span>

```azurecli
{                                                            
  "description": "This policy enables you to restrict the locations your organization can specify when deploying resources. Use to enforce your geo-compliance requirements.",                      
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

<span data-ttu-id="622d1-164">Bir ilke tanımı oluşturmak için devam etmeden önce yerleşik ilkelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="622d1-164">Before proceeding to create a policy definition, look at the built-in policies.</span></span> <span data-ttu-id="622d1-165">Gereksinim duyduğunuz limitleri geçerlidir yerleşik bir ilke bulursanız, bir ilke tanımı oluşturma atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="622d1-165">If you find a built-in policy that applies the limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="622d1-166">Bunun yerine, yerleşik ilkesini istenen kapsamı atayın.</span><span class="sxs-lookup"><span data-stu-id="622d1-166">Instead, assign the built-in policy to the desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="622d1-167">İlke tanımı oluşturun</span><span class="sxs-lookup"><span data-stu-id="622d1-167">Create policy definition</span></span>

<span data-ttu-id="622d1-168">İlke tanımı komutu ile Azure CLI kullanarak bir ilke tanımı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="622d1-168">You can create a policy definition using Azure CLI with the policy definition command.</span></span>

```azurecli
az policy definition create --name coolAccessTier --description "Policy to specify access tier." --rules '{
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

### <a name="assign-policy"></a><span data-ttu-id="622d1-169">İlke atama</span><span class="sxs-lookup"><span data-stu-id="622d1-169">Assign policy</span></span>

<span data-ttu-id="622d1-170">İlke ataması komutunu kullanarak, istenen kapsamı ilkesi uygulayabilir.</span><span class="sxs-lookup"><span data-stu-id="622d1-170">You can apply the policy to the desired scope by using the policy assignment command.</span></span> <span data-ttu-id="622d1-171">Aşağıdaki örnek, bir kaynak grubu için bir ilke atar.</span><span class="sxs-lookup"><span data-stu-id="622d1-171">The following example assigns a policy to a resource group.</span></span>

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a><span data-ttu-id="622d1-172">Görünüm ilke ataması</span><span class="sxs-lookup"><span data-stu-id="622d1-172">View policy assignment</span></span>

<span data-ttu-id="622d1-173">Bir ilke atamasını görüntülemek için ilke ataması adı ve kapsam sağlar:</span><span class="sxs-lookup"><span data-stu-id="622d1-173">To view a policy assignment, provide the policy assignment name and the scope:</span></span>

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="622d1-174">İlke atamasını Kaldır</span><span class="sxs-lookup"><span data-stu-id="622d1-174">Remove policy assignment</span></span> 

<span data-ttu-id="622d1-175">Bir ilke atamasını kaldırmak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="622d1-175">To remove a policy assignment, use:</span></span>

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a><span data-ttu-id="622d1-176">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="622d1-176">Next steps</span></span>
* <span data-ttu-id="622d1-177">Kuruluşların abonelikleri etkili bir şekilde yönetmek için Resource Manager'ı nasıl kullanabileceği hakkında yönergeler için bkz. [Azure kurumsal iskelesi: öngörücü abonelik idaresi](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="622d1-177">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

