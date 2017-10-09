tootag dağıtımı sırasında bir kaynak ekleyin hello `tags` dağıttığınız öğesi toohello kaynak. Merhaba etiket adını ve değerini belirtin.

### <a name="apply-a-literal-value-toohello-tag-name"></a>Değişmez değer toohello etiket adı Uygula
Merhaba aşağıdaki örnekte gösterilir iki etiket depolama hesabıyla (`Dept` ve `Environment`) tooliteral değerlerini ayarlayabilirsiniz:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

### <a name="apply-an-object-toohello-tag-element"></a>Bir nesne toohello etiket öğesi uygulayın
Birkaç etiket depolayan bir nesne parametre tanımlayın ve bu nesne toohello etiketi öğe uygulayın. Merhaba nesnedeki her özellik hello kaynak için ayrı bir etiket olur. Merhaba aşağıdaki örnek adlı bir parametre içeriyor `tagValues` diğer bir deyişle uygulanan toohello etiketi öğe.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "tagValues": {
      "type": "object",
      "defaultValue": {
        "Dept": "Finance",
        "Environment": "Production"
      }
    }
  },
  "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": "[parameters('tagValues')]",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": {}
    }
  ]
}
```

### <a name="apply-a-json-string-toohello-tag-name"></a>Bir JSON dizesi toohello etiket adı Uygula

toostore tek bir etiket birçok değerleri hello değerlerini temsil eden bir JSON dizesi uygulayın. Merhaba tüm JSON dizesi 256 karakterden uzun olamaz bir etiket olarak depolanır. Merhaba aşağıdaki örnekte sahip adlı tek bir etiket `CostCenter` bir JSON dizesinde birkaç değerleri içerir:  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": {
        "CostCenter": "{\"Dept\":\"Finance\",\"Environment\":\"Production\"}"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```