<span data-ttu-id="170bb-101">Dağıtım sırasında bir parametre dosyası toopass parametre değerlerini kullanırsanız toocreate bir biçim benzer toohello aşağıdaki örneğine bir JSON dosyası gerekir:</span><span class="sxs-lookup"><span data-stu-id="170bb-101">If you use a parameter file toopass parameter values during deployment, you need toocreate a JSON file with a format similar toohello following example:</span></span>

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

<span data-ttu-id="170bb-102">hello parametre dosyası başlangıç boyutu 64 KB'den büyük olamaz.</span><span class="sxs-lookup"><span data-stu-id="170bb-102">hello size of hello parameter file cannot be more than 64 KB.</span></span>

<span data-ttu-id="170bb-103">Bir parametre (örneğin, parola) için tooprovide duyarlı bir değer gerekiyorsa, bu değer tooa anahtar kasası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="170bb-103">If you need tooprovide a sensitive value for a parameter (such as a password), add that value tooa key vault.</span></span> <span data-ttu-id="170bb-104">Merhaba önceki örnekte gösterildiği gibi dağıtım sırasında Hello anahtar kasası alın.</span><span class="sxs-lookup"><span data-stu-id="170bb-104">Retrieve hello key vault during deployment as shown in hello previous example.</span></span> <span data-ttu-id="170bb-105">Daha fazla bilgi için bkz: [dağıtımı sırasında güvenli değerlerini geçirin](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="170bb-105">For more information, see [Pass secure values during deployment](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span> 

