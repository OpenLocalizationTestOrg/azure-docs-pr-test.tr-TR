---
title: "aaaDeploy Azure kaynaklarını birden çok örneğini | Microsoft Docs"
description: "Kopyalama işlemi ve Azure Resource Manager şablonu tooiterate dizilerde birden çok kez kaynakları dağıtırken kullanın."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 94d95810-a87b-460f-8e82-c69d462ac3ca
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/26/2017
ms.author: tomfitz
ms.openlocfilehash: a3bd42f694053317c30b639c33dc4efae41a9a9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a>Bir kaynak veya Azure Resource Manager şablonları özelliğinde birden fazla örneğini dağıtma
Bu konu, nasıl gösterir, Azure Resource Manager şablonu toocreate tooiterate kaynak birden çok örneğini veya birden çok örneğini bir kaynakta bir özellik.

Toospecify sağlayan tooadd mantık tooyour şablonu gerekiyorsa bir kaynak olup olmadığını dağıtılır, bkz: [koşullu kaynağını dağıtma](#conditionally-deploy-resource).

## <a name="resource-iteration"></a>Kaynak yineleme
bir kaynak türü birden çok örneğini toocreate eklemek bir `copy` öğesi toohello kaynak türü. Merhaba copy öğesinde hello sayısını yineleme ve bu döngü için bir ad belirtin. Merhaba sayısı değeri pozitif bir tamsayı olmalıdır ve 800 aşamaz. Resource Manager hello kaynakları paralel olarak oluşturur. Bu nedenle, oluşturulan hello sipariş garanti edilmez. sıralı yinelendiğinde toocreate kaynaklara bakın [seri kopyalama](#serial-copy). 

Merhaba kaynak toocreate birden çok kez biçimini izleyen hello alır:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        }
    ],
    "outputs": {}
}
```

Bu hello fark her bir kaynağın adını içeren hello `copyIndex()` hello geçerli yineleme hello döngüde döndürür işlevi. `copyIndex()`sıfır tabanlı olur. Bu nedenle, örnek hello:

```json
"name": "[concat('storage', copyIndex())]",
```

Bu adları oluşturur:

* storage0
* storage1
* storage2.

toooffset hello dizin değeri hello copyındex () işlevini bir değer geçirebilirsiniz. Merhaba yineleme tooperform sayısı hala hello copy öğesinde belirtildi, ancak Copyındex hello değeri tarafından belirtilen başlangıç uzaklık değeri. Bu nedenle, örnek hello:

```json
"name": "[concat('storage', copyIndex(1))]",
```

Bu adları oluşturur:

* storage1
* storage2
* Depolaması3

Merhaba kopyalama işlemi hello dizideki her öğe aracılığıyla yineleyebilirsiniz çünkü dizilerle çalışırken yararlıdır. Kullanım hello `length` yineleme için hello dizi toospecify hello sayısı işlevini ve `copyIndex` tooretrieve hello geçerli dizinde hello dizi. Bu nedenle, örnek hello:

```json
"parameters": { 
  "org": { 
     "type": "array", 
     "defaultValue": [ 
         "contoso", 
         "fabrikam", 
         "coho" 
      ] 
  }
}, 
"resources": [ 
  { 
      "name": "[concat('storage', parameters('org')[copyIndex()])]", 
      "copy": { 
         "name": "storagecopy", 
         "count": "[length(parameters('org'))]" 
      }, 
      ...
  } 
]
```

Bu adları oluşturur:

* storagecontoso
* storagefabrikam
* storagecoho

## <a name="serial-copy"></a>Seri kopyalama

Merhaba kopyalama öğesi toocreate kullandığınızda bir kaynak türü, kaynak yöneticisi, varsayılan olarak, birden çok örneğini Bu örneklerde paralel dağıtır. Ancak, kaynakları sırayla dağıtılan o hello toospecify isteyebilirsiniz. Örneğin, bir üretim ortamında güncelleştirirken, toostagger hello güncelleştirmeleri yalnızca belirli sayıda isteyebilirsiniz herhangi bir zamanda güncelleştirilir.

Resource Manager, tooserially sağlayan özellikleri hello kopyalama öğede birden çok örneği dağıtmak sunar. Merhaba kopyalama öğe kümesindeki `mode` çok**seri** ve `batchSize` örnekleri toodeploy birer birer toohello sayısı. Merhaba önceki toplu iş tamamlanana kadar tek bir toplu başlamıyor şekilde seri moduyla, Resource Manager hello Döngüdeki önceki örnekleri bir bağımlılık oluşturur.

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

Merhaba modu özelliği de kabul eder **paralel**, hello varsayılan değeri olduğu.

Fiili kaynaklar oluşturmadan tootest seri kopya boş iç içe geçmiş şablonları dağıtır şablon aşağıdaki kullanım hello:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "numberToDeploy": {
      "type": "int",
      "minValue": 2,
      "defaultValue": 5
    }
  },
  "resources": [
    {
      "apiVersion": "2015-01-01",
      "type": "Microsoft.Resources/deployments",
      "name": "[concat('loop-', copyIndex())]",
      "copy": {
        "name": "iterator",
        "count": "[parameters('numberToDeploy')]",
        "mode": "serial",
        "batchSize": 1
      },
      "properties": {
        "mode": "Incremental",
        "template": {
          "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {},
          "variables": {},
          "resources": [],
          "outputs": {
          }
        }
      }
    }
  ],
  "outputs": {
  }
}
```

Hello dağıtım geçmişini iç içe geçmiş dağıtımları hello bildirimi sırada işlenir.

![Seri dağıtımı](./media/resource-group-create-multiple/serial-copy.png)

Daha gerçekçi bir senaryo için aşağıdaki örneğine hello birer birer iç içe geçmiş bir şablondan bir Linux VM, iki örnek dağıtır:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "User name for hello Virtual Machine."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Password for hello Virtual Machine."
            }
        },
        "dnsLabelPrefix": {
            "type": "string",
            "metadata": {
                "description": "Unique DNS Name for hello Public IP used tooaccess hello Virtual Machine."
            }
        },
        "ubuntuOSVersion": {
            "type": "string",
            "defaultValue": "16.04.0-LTS",
            "allowedValues": [
                "12.04.5-LTS",
                "14.04.5-LTS",
                "15.10",
                "16.04.0-LTS"
            ],
            "metadata": {
                "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version."
            }
        }
    },
    "variables": {
        "templatelink": "https://raw.githubusercontent.com/rjmax/Build2017/master/Act1.TemplateEnhancements/Chapter03.LinuxVM.json"
    },
    "resources": [
        {
            "apiVersion": "2015-01-01",
            "name": "[concat('nestedDeployment',copyIndex())]",
            "type": "Microsoft.Resources/deployments",
            "copy": {
                "name": "myCopySet",
                "count": 4,
                "mode": "serial",
                "batchSize": 2
            },
            "properties": {
                "mode": "Incremental",
                "templateLink": {
                    "uri": "[variables('templatelink')]",
                    "contentVersion": "1.0.0.0"
                },
                "parameters": {
                    "adminUsername": {
                        "value": "[parameters('adminUsername')]"
                    },
                    "adminPassword": {
                        "value": "[parameters('adminPassword')]"
                    },
                    "dnsLabelPrefix": {
                        "value": "[parameters('dnsLabelPrefix')]"
                    },
                    "ubuntuOSVersion": {
                        "value": "[parameters('ubuntuOSVersion')]"
                    },
                    "index":{
                        "value": "[copyIndex()]"
                    }
                }
            }
        }
    ]
}
```

## <a name="property-iteration"></a>Özellik yineleme

bir kaynak, bir özellik için birden çok değer toocreate eklemek bir `copy` hello özellikler öğesindeki dizi. Bu dizi nesnelerini içerir ve her nesne hello aşağıdaki özelliklere sahiptir:

* ad - hello hello özelliği toocreate için birden çok değer
* sayısı - değerleri toocreate hello sayısı
* Giriş - hello değerleri tooassign toohello özelliği içeren bir nesne  

örnekte gösterildiği nasıl aşağıdaki hello tooapply `copy` toohello dataDisks özelliği bir sanal makinede:

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "copy": [{
          "name": "dataDisks",
          "count": 3,
          "input": {
              "lun": "[copyIndex('dataDisks')]",
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

Kullanırken dikkat `copyIndex` özelliği yineleme içinde hello yineleme hello adı sağlamanız gerekir. Kaynak bir yineleme kullanıldığında tooprovide hello ada sahip değil.

Kaynak Yöneticisi'ni genişletir hello `copy` dağıtımı sırasında dizi. Merhaba dizi Hello adı hello özelliğinin hello adı haline gelir. Merhaba giriş değerleri hello nesne özellikleri haline gelir. dağıtılan hello şablonu olur:

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "dataDisks": [
          {
              "lun": 0,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 1,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 2,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

Kaynak ve özellik yineleme birlikte kullanabilirsiniz. Ada göre başvuru hello özelliği yineleme.

```json
{
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[concat(parameters('vnetname'), copyIndex())]",
    "apiVersion": "2016-06-01",
    "copy":{
        "count": 2,
        "name": "vnetloop"
    },
    "location": "[resourceGroup().location]",
    "properties": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "copy": [
            {
                "name": "subnets",
                "count": 2,
                "input": {
                    "name": "[concat('subnet-', copyIndex('subnets'))]",
                    "properties": {
                        "addressPrefix": "[variables('subnetAddressPrefix')[copyIndex('subnets')]]"
                    }
                }
            }
        ]
    }
}
```

Her kaynak için hello özelliklerinde bir kopya öğe yalnızca içerebilir. toospecify birden fazla özellik için bir yineleme döngüsü hello kopyalama dizideki birden çok nesne tanımlayın. Her nesneyi ayrı olarak yinelendiğinde. Örneğin, toocreate hem hello birden çok örneğini `frontendIPConfigurations` özelliği ve hello `loadBalancingRules` bir yük dengeleyici özelliği tek bir kopya öğesinde hem nesnelerini tanımlayın: 

```json
{
    "name": "[variables('loadBalancerName')]",
    "type": "Microsoft.Network/loadBalancers",
    "properties": {
        "copy": [
          {
              "name": "frontendIPConfigurations",
              "count": 2,
              "input": {
                  "name": "[concat('loadBalancerFrontEnd', copyIndex('frontendIPConfigurations', 1))]",
                  "properties": {
                      "publicIPAddress": {
                          "id": "[variables(concat('publicIPAddressID', copyIndex('frontendIPConfigurations', 1)))]"
                      }
                  }
              }
          },
          {
              "name": "loadBalancingRules",
              "count": 2,
              "input": {
                  "name": "[concat('LBRuleForVIP', copyIndex('loadBalancingRules', 1))]",
                  "properties": {
                      "frontendIPConfiguration": {
                          "id": "[variables(concat('frontEndIPConfigID', copyIndex('loadBalancingRules', 1)))]"
                      },
                      "backendAddressPool": {
                          "id": "[variables('lbBackendPoolID')]"
                      },
                      "protocol": "tcp",
                      "frontendPort": "[variables(concat('frontEndPort' copyIndex('loadBalancingRules', 1))]",
                      "backendPort": "[variables(concat('backEndPort' copyIndex('loadBalancingRules', 1))]",
                      "probe": {
                          "id": "[variables('lbProbeID')]"
                      }
                  }
              }
          }
        ],
        ...
    }
}
```

## <a name="depend-on-resources-in-a-loop"></a>Döngü kaynakları bağlıdır
Hello kullanarak bir kaynak sonra başka bir kaynak dağıtıldığını belirten `dependsOn` öğesi. toodeploy bir döngü kaynaklarında hello koleksiyonunu bağımlı bir kaynak hello kopyalama döngüsü hello dependsOn öğesindeki hello adını sağlayın. Aşağıdaki örnek hello nasıl sanal makine dağıtmadan önce toodeploy üç depolama hesapları hello gösterir. Merhaba tam sanal makine tanımı gösterilmez. Bu hello kopyalama öğe adı çok ayarlanmış sahip dikkat edin`storagecopy` ve hello dependsOn öğesi hello sanal makineler için de ayarlanmış çok`storagecopy`.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        },
        {
            "apiVersion": "2015-06-15", 
            "type": "Microsoft.Compute/virtualMachines", 
            "name": "[concat('VM', uniqueString(resourceGroup().id))]",  
            "dependsOn": ["storagecopy"],
            ...
        }
    ],
    "outputs": {}
}
```

## <a name="create-multiple-instances-of-a-child-resource"></a>Bir alt kaynak birden çok örneğini oluşturma
Bir alt kaynak kopyalama döngüsü kullanamazsınız. içindeki başka bir kaynak birden çok örneğini tipik olarak tanımlayan kaynak içe toocreate, bunun yerine bu kaynak en üst düzey bir kaynak olarak oluşturmanız gerekir. Merhaba ilişkisi hello türü ve adı özellikleri aracılığıyla hello üst kaynakla tanımlayın.

Örneğin, data factory içinde alt kaynağı olarak bir veri kümesini tanımlama varsayalım.

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
    "resources": [
    {
        "type": "datasets",
        "name": "exampleDataSet",
        "dependsOn": [
            "exampleDataFactory"
        ],
        ...
    }
}]
```

toocreate veri kümeleri, birden çok örneğini taşıyın hello veri fabrikası dışında. Merhaba veri kümesi hello veri fabrikası aynı düzeydeki hello olmalıdır, ancak hala bir alt kaynak hello veri fabrikasının değildir. Veri kümesi ve veri fabrikası hello türü ve adı özellikleri aracılığıyla arasındaki hello ilişki korur. Türü artık hello şablonda onun konumdan çıkarsanabileceği beri hello biçiminde hello tam olarak nitelenmiş tür sağlamanız gerekir: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.

tooestablish hello veri fabrikası örneği ile bir üst/alt ilişkisi hello üst kaynak adını içeren bir hello veri kümesi için bir ad sağlayın. Kullanım hello biçimi: `{parent-resource-name}/{child-resource-name}`.  

Merhaba aşağıdaki örnek hello uygulamasını gösterir:

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
},
{
    "type": "Microsoft.DataFactory/datafactories/datasets",
    "name": "[concat('exampleDataFactory', '/', 'exampleDataSet', copyIndex())]",
    "dependsOn": [
        "exampleDataFactory"
    ],
    "copy": { 
        "name": "datasetcopy", 
        "count": "3" 
    } 
    ...
}]
```

## <a name="conditionally-deploy-resource"></a>Koşullu kaynağını dağıtma

toospecify kaynak dağıtmış olup olmadığını hello kullan `condition` öğesi. Bu öğe için başlangıç değerini tootrue ya da yanlış çözümler. Merhaba değer doğru olduğunda hello kaynak dağıtılır. Merhaba değeri false olduğunda hello kaynak dağıtılmaz. Örneğin, yeni bir depolama hesabı dağıtılan veya varolan bir depolama hesabı kullanılır, toospecify kullanın:

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

Yeni veya mevcut bir kaynağı kullanarak bir örnek için bkz: [yeni veya varolan bir koşul şablonu](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).

Bir parola veya SSH anahtar toodeploy sanal makine kullanarak bir örnek için bkz: [kullanıcı adı veya SSH koşul şablon](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).

## <a name="next-steps"></a>Sonraki adımlar
* Bir şablon hello bölümlerini hakkında toolearn istiyorsanız, bkz: [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).
* toolearn nasıl toodeploy, şablonunuzu bkz [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md).

