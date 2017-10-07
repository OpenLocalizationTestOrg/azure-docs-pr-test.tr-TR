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
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a><span data-ttu-id="4b761-103">Bir kaynak veya Azure Resource Manager şablonları özelliğinde birden fazla örneğini dağıtma</span><span class="sxs-lookup"><span data-stu-id="4b761-103">Deploy multiple instances of a resource or property in Azure Resource Manager templates</span></span>
<span data-ttu-id="4b761-104">Bu konu, nasıl gösterir, Azure Resource Manager şablonu toocreate tooiterate kaynak birden çok örneğini veya birden çok örneğini bir kaynakta bir özellik.</span><span class="sxs-lookup"><span data-stu-id="4b761-104">This topic shows you how tooiterate in your Azure Resource Manager template toocreate multiple instances of a resource, or multiple instances of a property on a resource.</span></span>

<span data-ttu-id="4b761-105">Toospecify sağlayan tooadd mantık tooyour şablonu gerekiyorsa bir kaynak olup olmadığını dağıtılır, bkz: [koşullu kaynağını dağıtma](#conditionally-deploy-resource).</span><span class="sxs-lookup"><span data-stu-id="4b761-105">If you need tooadd logic tooyour template that enables you toospecify whether a resource is deployed, see [Conditionally deploy resource](#conditionally-deploy-resource).</span></span>

## <a name="resource-iteration"></a><span data-ttu-id="4b761-106">Kaynak yineleme</span><span class="sxs-lookup"><span data-stu-id="4b761-106">Resource iteration</span></span>
<span data-ttu-id="4b761-107">bir kaynak türü birden çok örneğini toocreate eklemek bir `copy` öğesi toohello kaynak türü.</span><span class="sxs-lookup"><span data-stu-id="4b761-107">toocreate multiple instances of a resource type, add a `copy` element toohello resource type.</span></span> <span data-ttu-id="4b761-108">Merhaba copy öğesinde hello sayısını yineleme ve bu döngü için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="4b761-108">In hello copy element, you specify hello number of iterations and a name for this loop.</span></span> <span data-ttu-id="4b761-109">Merhaba sayısı değeri pozitif bir tamsayı olmalıdır ve 800 aşamaz.</span><span class="sxs-lookup"><span data-stu-id="4b761-109">hello count value must be a positive integer and cannot exceed 800.</span></span> <span data-ttu-id="4b761-110">Resource Manager hello kaynakları paralel olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4b761-110">Resource Manager creates hello resources in parallel.</span></span> <span data-ttu-id="4b761-111">Bu nedenle, oluşturulan hello sipariş garanti edilmez.</span><span class="sxs-lookup"><span data-stu-id="4b761-111">Therefore, hello order in which they are created is not guaranteed.</span></span> <span data-ttu-id="4b761-112">sıralı yinelendiğinde toocreate kaynaklara bakın [seri kopyalama](#serial-copy).</span><span class="sxs-lookup"><span data-stu-id="4b761-112">toocreate iterated resources in sequence, see [Serial copy](#serial-copy).</span></span> 

<span data-ttu-id="4b761-113">Merhaba kaynak toocreate birden çok kez biçimini izleyen hello alır:</span><span class="sxs-lookup"><span data-stu-id="4b761-113">hello resource toocreate multiple times takes hello following format:</span></span>

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

<span data-ttu-id="4b761-114">Bu hello fark her bir kaynağın adını içeren hello `copyIndex()` hello geçerli yineleme hello döngüde döndürür işlevi.</span><span class="sxs-lookup"><span data-stu-id="4b761-114">Notice that hello name of each resource includes hello `copyIndex()` function, which returns hello current iteration in hello loop.</span></span> <span data-ttu-id="4b761-115">`copyIndex()`sıfır tabanlı olur.</span><span class="sxs-lookup"><span data-stu-id="4b761-115">`copyIndex()` is zero-based.</span></span> <span data-ttu-id="4b761-116">Bu nedenle, örnek hello:</span><span class="sxs-lookup"><span data-stu-id="4b761-116">So, hello following example:</span></span>

```json
"name": "[concat('storage', copyIndex())]",
```

<span data-ttu-id="4b761-117">Bu adları oluşturur:</span><span class="sxs-lookup"><span data-stu-id="4b761-117">Creates these names:</span></span>

* <span data-ttu-id="4b761-118">storage0</span><span class="sxs-lookup"><span data-stu-id="4b761-118">storage0</span></span>
* <span data-ttu-id="4b761-119">storage1</span><span class="sxs-lookup"><span data-stu-id="4b761-119">storage1</span></span>
* <span data-ttu-id="4b761-120">storage2.</span><span class="sxs-lookup"><span data-stu-id="4b761-120">storage2.</span></span>

<span data-ttu-id="4b761-121">toooffset hello dizin değeri hello copyındex () işlevini bir değer geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4b761-121">toooffset hello index value, you can pass a value in hello copyIndex() function.</span></span> <span data-ttu-id="4b761-122">Merhaba yineleme tooperform sayısı hala hello copy öğesinde belirtildi, ancak Copyındex hello değeri tarafından belirtilen başlangıç uzaklık değeri.</span><span class="sxs-lookup"><span data-stu-id="4b761-122">hello number of iterations tooperform is still specified in hello copy element, but hello value of copyIndex is offset by hello specified value.</span></span> <span data-ttu-id="4b761-123">Bu nedenle, örnek hello:</span><span class="sxs-lookup"><span data-stu-id="4b761-123">So, hello following example:</span></span>

```json
"name": "[concat('storage', copyIndex(1))]",
```

<span data-ttu-id="4b761-124">Bu adları oluşturur:</span><span class="sxs-lookup"><span data-stu-id="4b761-124">Creates these names:</span></span>

* <span data-ttu-id="4b761-125">storage1</span><span class="sxs-lookup"><span data-stu-id="4b761-125">storage1</span></span>
* <span data-ttu-id="4b761-126">storage2</span><span class="sxs-lookup"><span data-stu-id="4b761-126">storage2</span></span>
* <span data-ttu-id="4b761-127">Depolaması3</span><span class="sxs-lookup"><span data-stu-id="4b761-127">storage3</span></span>

<span data-ttu-id="4b761-128">Merhaba kopyalama işlemi hello dizideki her öğe aracılığıyla yineleyebilirsiniz çünkü dizilerle çalışırken yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="4b761-128">hello copy operation is helpful when working with arrays because you can iterate through each element in hello array.</span></span> <span data-ttu-id="4b761-129">Kullanım hello `length` yineleme için hello dizi toospecify hello sayısı işlevini ve `copyIndex` tooretrieve hello geçerli dizinde hello dizi.</span><span class="sxs-lookup"><span data-stu-id="4b761-129">Use hello `length` function on hello array toospecify hello count for iterations, and `copyIndex` tooretrieve hello current index in hello array.</span></span> <span data-ttu-id="4b761-130">Bu nedenle, örnek hello:</span><span class="sxs-lookup"><span data-stu-id="4b761-130">So, hello following example:</span></span>

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

<span data-ttu-id="4b761-131">Bu adları oluşturur:</span><span class="sxs-lookup"><span data-stu-id="4b761-131">Creates these names:</span></span>

* <span data-ttu-id="4b761-132">storagecontoso</span><span class="sxs-lookup"><span data-stu-id="4b761-132">storagecontoso</span></span>
* <span data-ttu-id="4b761-133">storagefabrikam</span><span class="sxs-lookup"><span data-stu-id="4b761-133">storagefabrikam</span></span>
* <span data-ttu-id="4b761-134">storagecoho</span><span class="sxs-lookup"><span data-stu-id="4b761-134">storagecoho</span></span>

## <a name="serial-copy"></a><span data-ttu-id="4b761-135">Seri kopyalama</span><span class="sxs-lookup"><span data-stu-id="4b761-135">Serial copy</span></span>

<span data-ttu-id="4b761-136">Merhaba kopyalama öğesi toocreate kullandığınızda bir kaynak türü, kaynak yöneticisi, varsayılan olarak, birden çok örneğini Bu örneklerde paralel dağıtır.</span><span class="sxs-lookup"><span data-stu-id="4b761-136">When you use hello copy element toocreate multiple instances of a resource type, Resource Manager, by default, deploys those instances in parallel.</span></span> <span data-ttu-id="4b761-137">Ancak, kaynakları sırayla dağıtılan o hello toospecify isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4b761-137">However, you may want toospecify that hello resources are deployed in sequence.</span></span> <span data-ttu-id="4b761-138">Örneğin, bir üretim ortamında güncelleştirirken, toostagger hello güncelleştirmeleri yalnızca belirli sayıda isteyebilirsiniz herhangi bir zamanda güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="4b761-138">For example, when updating a production environment, you may want toostagger hello updates so only a certain number are updated at any one time.</span></span>

<span data-ttu-id="4b761-139">Resource Manager, tooserially sağlayan özellikleri hello kopyalama öğede birden çok örneği dağıtmak sunar.</span><span class="sxs-lookup"><span data-stu-id="4b761-139">Resource Manager provides properties on hello copy element that enable you tooserially deploy multiple instances.</span></span> <span data-ttu-id="4b761-140">Merhaba kopyalama öğe kümesindeki `mode` çok**seri** ve `batchSize` örnekleri toodeploy birer birer toohello sayısı.</span><span class="sxs-lookup"><span data-stu-id="4b761-140">In hello copy element, set `mode` too**serial** and `batchSize` toohello number of instances toodeploy at a time.</span></span> <span data-ttu-id="4b761-141">Merhaba önceki toplu iş tamamlanana kadar tek bir toplu başlamıyor şekilde seri moduyla, Resource Manager hello Döngüdeki önceki örnekleri bir bağımlılık oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4b761-141">With serial mode, Resource Manager creates a dependency on earlier instances in hello loop, so it does not start one batch until hello previous batch completes.</span></span>

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

<span data-ttu-id="4b761-142">Merhaba modu özelliği de kabul eder **paralel**, hello varsayılan değeri olduğu.</span><span class="sxs-lookup"><span data-stu-id="4b761-142">hello mode property also accepts **parallel**, which is hello default value.</span></span>

<span data-ttu-id="4b761-143">Fiili kaynaklar oluşturmadan tootest seri kopya boş iç içe geçmiş şablonları dağıtır şablon aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="4b761-143">tootest serial copy without creating actual resources, use hello following template that deploys empty nested templates:</span></span>

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

<span data-ttu-id="4b761-144">Hello dağıtım geçmişini iç içe geçmiş dağıtımları hello bildirimi sırada işlenir.</span><span class="sxs-lookup"><span data-stu-id="4b761-144">In hello deployment history, notice that hello nested deployments are processed in sequence.</span></span>

![Seri dağıtımı](./media/resource-group-create-multiple/serial-copy.png)

<span data-ttu-id="4b761-146">Daha gerçekçi bir senaryo için aşağıdaki örneğine hello birer birer iç içe geçmiş bir şablondan bir Linux VM, iki örnek dağıtır:</span><span class="sxs-lookup"><span data-stu-id="4b761-146">For a more realistic scenario, hello following example deploys two instances at a time of a Linux VM from a nested template:</span></span>

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

## <a name="property-iteration"></a><span data-ttu-id="4b761-147">Özellik yineleme</span><span class="sxs-lookup"><span data-stu-id="4b761-147">Property iteration</span></span>

<span data-ttu-id="4b761-148">bir kaynak, bir özellik için birden çok değer toocreate eklemek bir `copy` hello özellikler öğesindeki dizi.</span><span class="sxs-lookup"><span data-stu-id="4b761-148">toocreate multiple values for a property on a resource, add a `copy` array in hello properties element.</span></span> <span data-ttu-id="4b761-149">Bu dizi nesnelerini içerir ve her nesne hello aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="4b761-149">This array contains objects, and each object has hello following properties:</span></span>

* <span data-ttu-id="4b761-150">ad - hello hello özelliği toocreate için birden çok değer</span><span class="sxs-lookup"><span data-stu-id="4b761-150">name - hello name of hello property toocreate multiple values for</span></span>
* <span data-ttu-id="4b761-151">sayısı - değerleri toocreate hello sayısı</span><span class="sxs-lookup"><span data-stu-id="4b761-151">count - hello number of values toocreate</span></span>
* <span data-ttu-id="4b761-152">Giriş - hello değerleri tooassign toohello özelliği içeren bir nesne</span><span class="sxs-lookup"><span data-stu-id="4b761-152">input - an object that contains hello values tooassign toohello property</span></span>  

<span data-ttu-id="4b761-153">örnekte gösterildiği nasıl aşağıdaki hello tooapply `copy` toohello dataDisks özelliği bir sanal makinede:</span><span class="sxs-lookup"><span data-stu-id="4b761-153">hello following example shows how tooapply `copy` toohello dataDisks property on a virtual machine:</span></span>

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

<span data-ttu-id="4b761-154">Kullanırken dikkat `copyIndex` özelliği yineleme içinde hello yineleme hello adı sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4b761-154">Notice that when using `copyIndex` inside a property iteration, you must provide hello name of hello iteration.</span></span> <span data-ttu-id="4b761-155">Kaynak bir yineleme kullanıldığında tooprovide hello ada sahip değil.</span><span class="sxs-lookup"><span data-stu-id="4b761-155">You do not have tooprovide hello name when used with resource iteration.</span></span>

<span data-ttu-id="4b761-156">Kaynak Yöneticisi'ni genişletir hello `copy` dağıtımı sırasında dizi.</span><span class="sxs-lookup"><span data-stu-id="4b761-156">Resource Manager expands hello `copy` array during deployment.</span></span> <span data-ttu-id="4b761-157">Merhaba dizi Hello adı hello özelliğinin hello adı haline gelir.</span><span class="sxs-lookup"><span data-stu-id="4b761-157">hello name of hello array becomes hello name of hello property.</span></span> <span data-ttu-id="4b761-158">Merhaba giriş değerleri hello nesne özellikleri haline gelir.</span><span class="sxs-lookup"><span data-stu-id="4b761-158">hello input values become hello object properties.</span></span> <span data-ttu-id="4b761-159">dağıtılan hello şablonu olur:</span><span class="sxs-lookup"><span data-stu-id="4b761-159">hello deployed template becomes:</span></span>

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

<span data-ttu-id="4b761-160">Kaynak ve özellik yineleme birlikte kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4b761-160">You can use resource and property iteration together.</span></span> <span data-ttu-id="4b761-161">Ada göre başvuru hello özelliği yineleme.</span><span class="sxs-lookup"><span data-stu-id="4b761-161">Reference hello property iteration by name.</span></span>

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

<span data-ttu-id="4b761-162">Her kaynak için hello özelliklerinde bir kopya öğe yalnızca içerebilir.</span><span class="sxs-lookup"><span data-stu-id="4b761-162">You can only include one copy element in hello properties for each resource.</span></span> <span data-ttu-id="4b761-163">toospecify birden fazla özellik için bir yineleme döngüsü hello kopyalama dizideki birden çok nesne tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="4b761-163">toospecify an iteration loop for more than one property, define multiple objects in hello copy array.</span></span> <span data-ttu-id="4b761-164">Her nesneyi ayrı olarak yinelendiğinde.</span><span class="sxs-lookup"><span data-stu-id="4b761-164">Each object is iterated separately.</span></span> <span data-ttu-id="4b761-165">Örneğin, toocreate hem hello birden çok örneğini `frontendIPConfigurations` özelliği ve hello `loadBalancingRules` bir yük dengeleyici özelliği tek bir kopya öğesinde hem nesnelerini tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="4b761-165">For example, toocreate multiple instances of both hello `frontendIPConfigurations` property and hello `loadBalancingRules` property on a load balancer, define both objects in a single copy element:</span></span> 

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

## <a name="depend-on-resources-in-a-loop"></a><span data-ttu-id="4b761-166">Döngü kaynakları bağlıdır</span><span class="sxs-lookup"><span data-stu-id="4b761-166">Depend on resources in a loop</span></span>
<span data-ttu-id="4b761-167">Hello kullanarak bir kaynak sonra başka bir kaynak dağıtıldığını belirten `dependsOn` öğesi.</span><span class="sxs-lookup"><span data-stu-id="4b761-167">You specify that a resource is deployed after another resource by using hello `dependsOn` element.</span></span> <span data-ttu-id="4b761-168">toodeploy bir döngü kaynaklarında hello koleksiyonunu bağımlı bir kaynak hello kopyalama döngüsü hello dependsOn öğesindeki hello adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="4b761-168">toodeploy a resource that depends on hello collection of resources in a loop, provide hello name of hello copy loop in hello dependsOn element.</span></span> <span data-ttu-id="4b761-169">Aşağıdaki örnek hello nasıl sanal makine dağıtmadan önce toodeploy üç depolama hesapları hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="4b761-169">hello following example shows how toodeploy three storage accounts before deploying hello Virtual Machine.</span></span> <span data-ttu-id="4b761-170">Merhaba tam sanal makine tanımı gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="4b761-170">hello full Virtual Machine definition is not shown.</span></span> <span data-ttu-id="4b761-171">Bu hello kopyalama öğe adı çok ayarlanmış sahip dikkat edin`storagecopy` ve hello dependsOn öğesi hello sanal makineler için de ayarlanmış çok`storagecopy`.</span><span class="sxs-lookup"><span data-stu-id="4b761-171">Notice that hello copy element has name set too`storagecopy` and hello dependsOn element for hello Virtual Machines is also set too`storagecopy`.</span></span>

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

## <a name="create-multiple-instances-of-a-child-resource"></a><span data-ttu-id="4b761-172">Bir alt kaynak birden çok örneğini oluşturma</span><span class="sxs-lookup"><span data-stu-id="4b761-172">Create multiple instances of a child resource</span></span>
<span data-ttu-id="4b761-173">Bir alt kaynak kopyalama döngüsü kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="4b761-173">You cannot use a copy loop for a child resource.</span></span> <span data-ttu-id="4b761-174">içindeki başka bir kaynak birden çok örneğini tipik olarak tanımlayan kaynak içe toocreate, bunun yerine bu kaynak en üst düzey bir kaynak olarak oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4b761-174">toocreate multiple instances of a resource that you typically define as nested within another resource, you must instead create that resource as a top-level resource.</span></span> <span data-ttu-id="4b761-175">Merhaba ilişkisi hello türü ve adı özellikleri aracılığıyla hello üst kaynakla tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="4b761-175">You define hello relationship with hello parent resource through hello type and name properties.</span></span>

<span data-ttu-id="4b761-176">Örneğin, data factory içinde alt kaynağı olarak bir veri kümesini tanımlama varsayalım.</span><span class="sxs-lookup"><span data-stu-id="4b761-176">For example, suppose you typically define a dataset as a child resource within a data factory.</span></span>

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

<span data-ttu-id="4b761-177">toocreate veri kümeleri, birden çok örneğini taşıyın hello veri fabrikası dışında.</span><span class="sxs-lookup"><span data-stu-id="4b761-177">toocreate multiple instances of data sets, move it outside of hello data factory.</span></span> <span data-ttu-id="4b761-178">Merhaba veri kümesi hello veri fabrikası aynı düzeydeki hello olmalıdır, ancak hala bir alt kaynak hello veri fabrikasının değildir.</span><span class="sxs-lookup"><span data-stu-id="4b761-178">hello dataset must be at hello same level as hello data factory, but it is still a child resource of hello data factory.</span></span> <span data-ttu-id="4b761-179">Veri kümesi ve veri fabrikası hello türü ve adı özellikleri aracılığıyla arasındaki hello ilişki korur.</span><span class="sxs-lookup"><span data-stu-id="4b761-179">You preserve hello relationship between data set and data factory through hello type and name properties.</span></span> <span data-ttu-id="4b761-180">Türü artık hello şablonda onun konumdan çıkarsanabileceği beri hello biçiminde hello tam olarak nitelenmiş tür sağlamanız gerekir: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span><span class="sxs-lookup"><span data-stu-id="4b761-180">Since type can no longer be inferred from its position in hello template, you must provide hello fully qualified type in hello format: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span></span>

<span data-ttu-id="4b761-181">tooestablish hello veri fabrikası örneği ile bir üst/alt ilişkisi hello üst kaynak adını içeren bir hello veri kümesi için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="4b761-181">tooestablish a parent/child relationship with an instance of hello data factory, provide a name for hello data set that includes hello parent resource name.</span></span> <span data-ttu-id="4b761-182">Kullanım hello biçimi: `{parent-resource-name}/{child-resource-name}`.</span><span class="sxs-lookup"><span data-stu-id="4b761-182">Use hello format: `{parent-resource-name}/{child-resource-name}`.</span></span>  

<span data-ttu-id="4b761-183">Merhaba aşağıdaki örnek hello uygulamasını gösterir:</span><span class="sxs-lookup"><span data-stu-id="4b761-183">hello following example shows hello implementation:</span></span>

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

## <a name="conditionally-deploy-resource"></a><span data-ttu-id="4b761-184">Koşullu kaynağını dağıtma</span><span class="sxs-lookup"><span data-stu-id="4b761-184">Conditionally deploy resource</span></span>

<span data-ttu-id="4b761-185">toospecify kaynak dağıtmış olup olmadığını hello kullan `condition` öğesi.</span><span class="sxs-lookup"><span data-stu-id="4b761-185">toospecify whether a resource is deployed, use hello `condition` element.</span></span> <span data-ttu-id="4b761-186">Bu öğe için başlangıç değerini tootrue ya da yanlış çözümler.</span><span class="sxs-lookup"><span data-stu-id="4b761-186">hello value for this element resolves tootrue or false.</span></span> <span data-ttu-id="4b761-187">Merhaba değer doğru olduğunda hello kaynak dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="4b761-187">When hello value is true, hello resource is deployed.</span></span> <span data-ttu-id="4b761-188">Merhaba değeri false olduğunda hello kaynak dağıtılmaz.</span><span class="sxs-lookup"><span data-stu-id="4b761-188">When hello value is false, hello resource is not deployed.</span></span> <span data-ttu-id="4b761-189">Örneğin, yeni bir depolama hesabı dağıtılan veya varolan bir depolama hesabı kullanılır, toospecify kullanın:</span><span class="sxs-lookup"><span data-stu-id="4b761-189">For example, toospecify whether a new storage account is deployed or an existing storage account is used, use:</span></span>

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

<span data-ttu-id="4b761-190">Yeni veya mevcut bir kaynağı kullanarak bir örnek için bkz: [yeni veya varolan bir koşul şablonu](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="4b761-190">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="4b761-191">Bir parola veya SSH anahtar toodeploy sanal makine kullanarak bir örnek için bkz: [kullanıcı adı veya SSH koşul şablon](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="4b761-191">For an example of using a password or SSH key toodeploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b761-192">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4b761-192">Next steps</span></span>
* <span data-ttu-id="4b761-193">Bir şablon hello bölümlerini hakkında toolearn istiyorsanız, bkz: [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="4b761-193">If you want toolearn about hello sections of a template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="4b761-194">toolearn nasıl toodeploy, şablonunuzu bkz [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="4b761-194">toolearn how toodeploy your template, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>

