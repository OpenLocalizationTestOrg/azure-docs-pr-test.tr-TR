Dağıtım sırasında bir parametre dosyası toopass parametre değerlerini kullanırsanız toocreate bir biçim benzer toohello aşağıdaki örneğine bir JSON dosyası gerekir:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "webSiteName": {
            "value": "ExampleSite"
        },
        "webSiteHostingPlanName": {
            "value": "DefaultPlan"
        },
        "webSiteLocation": {
            "value": "West US"
        },
        "adminPassword": {
            "reference": {
               "keyVault": {
                  "id": "/subscriptions/{guid}/resourceGroups/{group-name}/providers/Microsoft.KeyVault/vaults/{vault-name}"
               }, 
               "secretName": "sqlAdminPassword" 
            }   
        }
   }
}
```

hello parametre dosyası başlangıç boyutu 64 KB'den büyük olamaz.

Bir parametre (örneğin, parola) için tooprovide duyarlı bir değer gerekiyorsa, bu değer tooa anahtar kasası ekleyin. Merhaba önceki örnekte gösterildiği gibi dağıtım sırasında Hello anahtar kasası alın. Daha fazla bilgi için bkz: [dağıtımı sırasında güvenli değerlerini geçirin](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md). 

