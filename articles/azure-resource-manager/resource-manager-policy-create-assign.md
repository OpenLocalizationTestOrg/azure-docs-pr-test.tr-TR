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
# <a name="assign-and-manage-resource-policies"></a>Atama ve kaynak ilkelerini yönetme

tooimplement bir ilke, şu adımları gerçekleştirmeniz gerekir:

1. Gereksinimlerinizi karşılayan, aboneliğinizde zaten varsa, ilke tanımları (Azure tarafından sağlanan yerleşik ilkeleri dahil) toosee denetleyin.
2. Varsa, adını alın.
3. Bir mevcut değilse, JSON hello İlkesi kuralıyla tanımlamak ve bir ilke tanımı aboneliğinizde olarak ekleyin. Bu adım hello ilke ataması için kullanılabilir hale getirir, ancak hello kuralları tooyour abonelik geçerli değildir.
4. Her iki durumda da hello İlkesi tooa kapsam (örneğin, bir abonelik veya kaynak grubu) atayın. Merhaba kuralı hello İlkesi artık zorunlu tutulmaz.

Bu makalede bir ilke tanımı hello adımları toocreate üzerinde odaklanır ve REST API'si, PowerShell veya Azure CLI aracılığıyla, tanım tooa kapsamı atayın. Toouse hello portal tooassign ilkeleri tercih ederseniz, bkz. [kullanım Azure portal tooassign ve kaynak ilkelerini yönetme](resource-manager-policy-portal.md). Bu makalede hello ilke tanımı oluşturmak için hello sözdizimi odaklanılmaktadır değil. İlke sözdizimi hakkında daha fazla bilgi için bkz: [kaynak ilkesine genel bakış](resource-manager-policy.md).

## <a name="rest-api"></a>REST API

### <a name="create-policy-definition"></a>İlke tanımı oluşturun

Merhaba ile bir ilke oluşturabilirsiniz [ilke tanımları için REST API](/rest/api/resources/policydefinitions). Merhaba REST API toocreate sağlar ve ilke tanımları silin ve varolan tanımları hakkında bilgi alın.

bir ilke tanımı toocreate çalıştırın:

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

Aşağıdaki örnek istek gövdesi benzer bir toohello şunları içerir:

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

### <a name="assign-policy"></a>İlke atama

Merhaba ilke tanımı hello aracılığıyla istenen hello kapsamda uygulayabilirsiniz [ilke atamaları için REST API](/rest/api/resources/policyassignments). Merhaba REST API toocreate sağlar ve ilke atamalarını silin ve varolan atamaları hakkında bilgi alın.

bir ilke atamasını toocreate çalıştırın:

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

Merhaba {ilke ataması} hello ilke ataması hello adıdır.

Aşağıdaki örnek istek gövdesi benzer bir toohello şunları içerir:

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

### <a name="view-policy"></a>İlkesini görüntüle
tooget bir ilke kullanmak hello [alma ilke tanımı](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) işlemi.

### <a name="get-aliases"></a>Diğer adlar Al
Diğer adlar hello REST API aracılığıyla alabilir:

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

Aşağıdaki örneğine hello bir diğer ad tanımını gösterir. Gördüğünüz gibi bir özellik adı değişikliği olduğunda bile bir diğer ad yolları farklı API sürümlerde tanımlar. 

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

## <a name="powershell"></a>PowerShell

Merhaba PowerShell örnekleriyle devam etmeden önce olduğundan emin olun [hello son sürümü yüklü](/powershell/azure/install-azurerm-ps) Azure PowerShell. İlke parametreleri sürüm 3.6.0 eklendi. Önceki bir sürümü varsa, bir hata belirten hello parametresi bulunamıyor hello örnekler döndür.

### <a name="view-policy-definitions"></a>Görünüm ilke tanımları
toosee aşağıdaki kullanım hello aboneliğinizde tüm ilke tanımları komutu:

```powershell
Get-AzureRmPolicyDefinition
```

Yerleşik ilkeleri de dahil olmak üzere tüm kullanılabilir ilke tanımları döndürür. Her ilke biçimini izleyen hello verilir:

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

Devam etmeden toocreate bir ilke tanımı önce hello yerleşik ilkelerine bakın. Gereksinim duyduğunuz hello limitleri geçerlidir yerleşik bir ilke bulursanız, bir ilke tanımı oluşturma atlayabilirsiniz. Bunun yerine, hello yerleşik ilke istenen toohello kapsamı atayın.

### <a name="create-policy-definition"></a>İlke tanımı oluşturun
Hello kullanarak bir ilke tanımı oluşturabilirsiniz `New-AzureRmPolicyDefinition` cmdlet'i.

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

Merhaba çıkış depolanır bir `$definition` ilke ataması sırasında kullanılan nesne. 

Parametre olarak Hello JSON belirtmek yerine hello İlkesi kuralı içeren hello yolu tooa .json dosyası sağlayabilirsiniz.

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy "c:\policies\coolAccessTier.json"
```

Merhaba aşağıdaki örnek parametreleri içeren bir ilke tanımı oluşturur:

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

### <a name="assign-policy"></a>İlke atama

Hello kullanarak istenen hello kapsamlı hello ilkesi uygulamak `New-AzureRmPolicyAssignment` cmdlet'i. Aşağıdaki örnek hello hello İlkesi tooa kaynak grubu atar.

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

tooassign parametreler gerektiren bir ilke oluşturun ve bu değerleri nesne. Hello aşağıdaki örnekte bir yerleşik ilkesini alır ve parametre değerlerini geçirir:

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a>Görünüm ilke ataması

belirli bir ilke ataması tooget kullanın:

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

tooview hello İlkesi kuralı bir ilke tanımı kullanın:

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a>İlke atamasını Kaldır 

bir ilke atamasını tooremove kullanın:

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a>Azure CLI

### <a name="view-policy-definitions"></a>Görünüm ilke tanımları
toosee aşağıdaki kullanım hello aboneliğinizde tüm ilke tanımları komutu:

```azurecli
az policy definition list
```

Yerleşik ilkeleri de dahil olmak üzere tüm kullanılabilir ilke tanımları döndürür. Her ilke biçimini izleyen hello verilir:

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

Devam etmeden toocreate bir ilke tanımı önce hello yerleşik ilkelerine bakın. Gereksinim duyduğunuz hello limitleri geçerlidir yerleşik bir ilke bulursanız, bir ilke tanımı oluşturma atlayabilirsiniz. Bunun yerine, hello yerleşik ilke istenen toohello kapsamı atayın.

### <a name="create-policy-definition"></a>İlke tanımı oluşturun

Merhaba ilke tanımı komutu ile Azure CLI kullanarak bir ilke tanımı oluşturabilirsiniz.

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

### <a name="assign-policy"></a>İlke atama

Merhaba ilke ataması komutunu kullanarak hello İlkesi istenen toohello kapsam uygulayabilirsiniz. Aşağıdaki örnek hello İlkesi tooa kaynak grubu atar.

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a>Görünüm ilke ataması

bir ilke atamasını tooview hello ilke ataması adı ve hello kapsam sağlar:

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a>İlke atamasını Kaldır 

bir ilke atamasını tooremove kullanın:

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a>Sonraki adımlar
* Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).

