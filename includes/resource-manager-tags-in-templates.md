<span data-ttu-id="da741-101">Dağıtım sırasında bir kaynağı etiketlemek için `tags` öğesini dağıtmakta olduğunuz kaynağa ekleyin.</span><span class="sxs-lookup"><span data-stu-id="da741-101">To tag a resource during deployment, add the `tags` element to the resource you are deploying.</span></span> <span data-ttu-id="da741-102">Etiket adını ve değerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="da741-102">Provide the tag name and value.</span></span>

### <a name="apply-a-literal-value-to-the-tag-name"></a><span data-ttu-id="da741-103">Etiket adına değişmez değer uygulama</span><span class="sxs-lookup"><span data-stu-id="da741-103">Apply a literal value to the tag name</span></span>
<span data-ttu-id="da741-104">Aşağıdaki örnekte değişmez değerlere ayarlanmış iki etiketi (`Dept` ve `Environment`) olan bir depolama hesabı gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="da741-104">The following example shows a storage account with two tags (`Dept` and `Environment`) that are set to literal values:</span></span>

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

### <a name="apply-an-object-to-the-tag-element"></a><span data-ttu-id="da741-105">Nesne etiketine öğe uygulama</span><span class="sxs-lookup"><span data-stu-id="da741-105">Apply an object to the tag element</span></span>
<span data-ttu-id="da741-106">Birkaç etiketi depolayan bir nesne parametresi tanımlayabilir ve bu nesneyi etiket öğesine uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da741-106">You can define an object parameter that stores several tags, and apply that object to the tag element.</span></span> <span data-ttu-id="da741-107">Nesnedeki her özellik, kaynak için ayrı bir etiket haline gelir.</span><span class="sxs-lookup"><span data-stu-id="da741-107">Each property in the object becomes a separate tag for the resource.</span></span> <span data-ttu-id="da741-108">Aşağıdaki örnekte etiket parametresine uygulanan `tagValues` adlı bir parametre kullanılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="da741-108">The following example has a parameter named `tagValues` that is applied to the tag element.</span></span>

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

### <a name="apply-a-json-string-to-the-tag-name"></a><span data-ttu-id="da741-109">Etiket adına JSON dizesi uygulama</span><span class="sxs-lookup"><span data-stu-id="da741-109">Apply a JSON string to the tag name</span></span>

<span data-ttu-id="da741-110">Çok sayıda değeri tek bir etikete depolamak için, değerleri temsil eden bir JSON dizesi uygulayın.</span><span class="sxs-lookup"><span data-stu-id="da741-110">To store many values in a single tag, apply a JSON string that represents the values.</span></span> <span data-ttu-id="da741-111">Tüm JSON dizesi, 256 karakterden uzun olmayan bir etiket olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="da741-111">The entire JSON string is stored as one tag that cannot exceed 256 characters.</span></span> <span data-ttu-id="da741-112">Aşağıdaki örnekte bir JSON dizesindeki çok sayıda değeri içeren `CostCenter` adlı tek bir etiket kullanılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="da741-112">The following example has a single tag named `CostCenter` that contains several values from a JSON string:</span></span>  

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