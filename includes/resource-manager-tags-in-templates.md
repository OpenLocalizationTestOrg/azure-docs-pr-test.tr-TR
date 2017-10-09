<span data-ttu-id="c9c9b-101">tootag dağıtımı sırasında bir kaynak ekleyin hello `tags` dağıttığınız öğesi toohello kaynak.</span><span class="sxs-lookup"><span data-stu-id="c9c9b-101">tootag a resource during deployment, add hello `tags` element toohello resource you are deploying.</span></span> <span data-ttu-id="c9c9b-102">Merhaba etiket adını ve değerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="c9c9b-102">Provide hello tag name and value.</span></span>

### <a name="apply-a-literal-value-toohello-tag-name"></a><span data-ttu-id="c9c9b-103">Değişmez değer toohello etiket adı Uygula</span><span class="sxs-lookup"><span data-stu-id="c9c9b-103">Apply a literal value toohello tag name</span></span>
<span data-ttu-id="c9c9b-104">Merhaba aşağıdaki örnekte gösterilir iki etiket depolama hesabıyla (`Dept` ve `Environment`) tooliteral değerlerini ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c9c9b-104">hello following example shows a storage account with two tags (`Dept` and `Environment`) that are set tooliteral values:</span></span>

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

### <a name="apply-an-object-toohello-tag-element"></a><span data-ttu-id="c9c9b-105">Bir nesne toohello etiket öğesi uygulayın</span><span class="sxs-lookup"><span data-stu-id="c9c9b-105">Apply an object toohello tag element</span></span>
<span data-ttu-id="c9c9b-106">Birkaç etiket depolayan bir nesne parametre tanımlayın ve bu nesne toohello etiketi öğe uygulayın.</span><span class="sxs-lookup"><span data-stu-id="c9c9b-106">You can define an object parameter that stores several tags, and apply that object toohello tag element.</span></span> <span data-ttu-id="c9c9b-107">Merhaba nesnedeki her özellik hello kaynak için ayrı bir etiket olur.</span><span class="sxs-lookup"><span data-stu-id="c9c9b-107">Each property in hello object becomes a separate tag for hello resource.</span></span> <span data-ttu-id="c9c9b-108">Merhaba aşağıdaki örnek adlı bir parametre içeriyor `tagValues` diğer bir deyişle uygulanan toohello etiketi öğe.</span><span class="sxs-lookup"><span data-stu-id="c9c9b-108">hello following example has a parameter named `tagValues` that is applied toohello tag element.</span></span>

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

### <a name="apply-a-json-string-toohello-tag-name"></a><span data-ttu-id="c9c9b-109">Bir JSON dizesi toohello etiket adı Uygula</span><span class="sxs-lookup"><span data-stu-id="c9c9b-109">Apply a JSON string toohello tag name</span></span>

<span data-ttu-id="c9c9b-110">toostore tek bir etiket birçok değerleri hello değerlerini temsil eden bir JSON dizesi uygulayın.</span><span class="sxs-lookup"><span data-stu-id="c9c9b-110">toostore many values in a single tag, apply a JSON string that represents hello values.</span></span> <span data-ttu-id="c9c9b-111">Merhaba tüm JSON dizesi 256 karakterden uzun olamaz bir etiket olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="c9c9b-111">hello entire JSON string is stored as one tag that cannot exceed 256 characters.</span></span> <span data-ttu-id="c9c9b-112">Merhaba aşağıdaki örnekte sahip adlı tek bir etiket `CostCenter` bir JSON dizesinde birkaç değerleri içerir:</span><span class="sxs-lookup"><span data-stu-id="c9c9b-112">hello following example has a single tag named `CostCenter` that contains several values from a JSON string:</span></span>  

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