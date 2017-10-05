---
title: "Birden çok örneğini Azure kaynaklarınızı dağıtma | Microsoft Docs"
description: "Kopyalama işlemi ve kullanma diziler bir Azure Resource Manager şablonu yinelemek için birden çok kez kaynakları dağıtırken."
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
ms.openlocfilehash: ed8e3081d2b2e07938d7cf3aa5f95f6dde81bc66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a><span data-ttu-id="7954f-103">Bir kaynak veya Azure Resource Manager şablonları özelliğinde birden fazla örneğini dağıtma</span><span class="sxs-lookup"><span data-stu-id="7954f-103">Deploy multiple instances of a resource or property in Azure Resource Manager templates</span></span>
<span data-ttu-id="7954f-104">Bu konu bir kaynak birden çok örneğini veya bir özelliği birden çok örneği üzerinde bir kaynak oluşturmak için Azure Resource Manager şablonu yineleme gösterir.</span><span class="sxs-lookup"><span data-stu-id="7954f-104">This topic shows you how to iterate in your Azure Resource Manager template to create multiple instances of a resource, or multiple instances of a property on a resource.</span></span>

<span data-ttu-id="7954f-105">Kaynak dağıtılabilir olup olmadığını belirlemek bkz olanak tanıyan şablonunuza mantığı eklemeniz gerekiyorsa, [koşullu kaynağını dağıtma](#conditionally-deploy-resource).</span><span class="sxs-lookup"><span data-stu-id="7954f-105">If you need to add logic to your template that enables you to specify whether a resource is deployed, see [Conditionally deploy resource](#conditionally-deploy-resource).</span></span>

## <a name="resource-iteration"></a><span data-ttu-id="7954f-106">Kaynak yineleme</span><span class="sxs-lookup"><span data-stu-id="7954f-106">Resource iteration</span></span>
<span data-ttu-id="7954f-107">Bir kaynak türü birden çok örneğini oluşturmak için Ekle bir `copy` öğesi için kaynak türü.</span><span class="sxs-lookup"><span data-stu-id="7954f-107">To create multiple instances of a resource type, add a `copy` element to the resource type.</span></span> <span data-ttu-id="7954f-108">Copy öğesinde sayısı yinelemeleri ve bu döngü için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="7954f-108">In the copy element, you specify the number of iterations and a name for this loop.</span></span> <span data-ttu-id="7954f-109">Sayaç değerinin pozitif bir tamsayı olmalıdır ve 800 aşamaz.</span><span class="sxs-lookup"><span data-stu-id="7954f-109">The count value must be a positive integer and cannot exceed 800.</span></span> <span data-ttu-id="7954f-110">Resource Manager kaynakları paralel olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7954f-110">Resource Manager creates the resources in parallel.</span></span> <span data-ttu-id="7954f-111">Bu nedenle, oluşturulan siparişi garanti edilmez.</span><span class="sxs-lookup"><span data-stu-id="7954f-111">Therefore, the order in which they are created is not guaranteed.</span></span> <span data-ttu-id="7954f-112">Sırayla tekrarlayan kaynakları oluşturmak için bkz [seri kopyalama](#serial-copy).</span><span class="sxs-lookup"><span data-stu-id="7954f-112">To create iterated resources in sequence, see [Serial copy](#serial-copy).</span></span> 

<span data-ttu-id="7954f-113">Kaynak birden çok kez oluşturmak için aşağıdaki biçimi alır:</span><span class="sxs-lookup"><span data-stu-id="7954f-113">The resource to create multiple times takes the following format:</span></span>

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

<span data-ttu-id="7954f-114">Her bir kaynağın adını içeren bildirim `copyIndex()` geçerli yineleme döngüde döndürür işlevi.</span><span class="sxs-lookup"><span data-stu-id="7954f-114">Notice that the name of each resource includes the `copyIndex()` function, which returns the current iteration in the loop.</span></span> <span data-ttu-id="7954f-115">`copyIndex()`sıfır tabanlı olur.</span><span class="sxs-lookup"><span data-stu-id="7954f-115">`copyIndex()` is zero-based.</span></span> <span data-ttu-id="7954f-116">Bunu, aşağıdaki örnek:</span><span class="sxs-lookup"><span data-stu-id="7954f-116">So, the following example:</span></span>

```json
"name": "[concat('storage', copyIndex())]",
```

<span data-ttu-id="7954f-117">Bu adları oluşturur:</span><span class="sxs-lookup"><span data-stu-id="7954f-117">Creates these names:</span></span>

* <span data-ttu-id="7954f-118">storage0</span><span class="sxs-lookup"><span data-stu-id="7954f-118">storage0</span></span>
* <span data-ttu-id="7954f-119">storage1</span><span class="sxs-lookup"><span data-stu-id="7954f-119">storage1</span></span>
* <span data-ttu-id="7954f-120">storage2.</span><span class="sxs-lookup"><span data-stu-id="7954f-120">storage2.</span></span>

<span data-ttu-id="7954f-121">Dizin değeri uzaklığı copyındex () işlevini bir değer geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7954f-121">To offset the index value, you can pass a value in the copyIndex() function.</span></span> <span data-ttu-id="7954f-122">Gerçekleştirmek için yineleme sayısı hala copy öğesinde belirtilen ancak Copyındex değeri belirtilen değere uzaklığı.</span><span class="sxs-lookup"><span data-stu-id="7954f-122">The number of iterations to perform is still specified in the copy element, but the value of copyIndex is offset by the specified value.</span></span> <span data-ttu-id="7954f-123">Bunu, aşağıdaki örnek:</span><span class="sxs-lookup"><span data-stu-id="7954f-123">So, the following example:</span></span>

```json
"name": "[concat('storage', copyIndex(1))]",
```

<span data-ttu-id="7954f-124">Bu adları oluşturur:</span><span class="sxs-lookup"><span data-stu-id="7954f-124">Creates these names:</span></span>

* <span data-ttu-id="7954f-125">storage1</span><span class="sxs-lookup"><span data-stu-id="7954f-125">storage1</span></span>
* <span data-ttu-id="7954f-126">storage2</span><span class="sxs-lookup"><span data-stu-id="7954f-126">storage2</span></span>
* <span data-ttu-id="7954f-127">Depolaması3</span><span class="sxs-lookup"><span data-stu-id="7954f-127">storage3</span></span>

<span data-ttu-id="7954f-128">Kopyalama işlemi, dizideki her öğe aracılığıyla yineleyebilirsiniz çünkü dizilerle çalışırken yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="7954f-128">The copy operation is helpful when working with arrays because you can iterate through each element in the array.</span></span> <span data-ttu-id="7954f-129">Kullanım `length` yineleme sayısını belirtmek için dizisindeki işlevi ve `copyIndex` dizideki geçerli dizini alınamadı.</span><span class="sxs-lookup"><span data-stu-id="7954f-129">Use the `length` function on the array to specify the count for iterations, and `copyIndex` to retrieve the current index in the array.</span></span> <span data-ttu-id="7954f-130">Bunu, aşağıdaki örnek:</span><span class="sxs-lookup"><span data-stu-id="7954f-130">So, the following example:</span></span>

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

<span data-ttu-id="7954f-131">Bu adları oluşturur:</span><span class="sxs-lookup"><span data-stu-id="7954f-131">Creates these names:</span></span>

* <span data-ttu-id="7954f-132">storagecontoso</span><span class="sxs-lookup"><span data-stu-id="7954f-132">storagecontoso</span></span>
* <span data-ttu-id="7954f-133">storagefabrikam</span><span class="sxs-lookup"><span data-stu-id="7954f-133">storagefabrikam</span></span>
* <span data-ttu-id="7954f-134">storagecoho</span><span class="sxs-lookup"><span data-stu-id="7954f-134">storagecoho</span></span>

## <a name="serial-copy"></a><span data-ttu-id="7954f-135">Seri kopyalama</span><span class="sxs-lookup"><span data-stu-id="7954f-135">Serial copy</span></span>

<span data-ttu-id="7954f-136">Bir kaynak türü, kaynak yöneticisi, varsayılan olarak, birden çok örneğini oluşturmak için kopyalama öğesi kullandığınızda bu örneklerde paralel dağıtır.</span><span class="sxs-lookup"><span data-stu-id="7954f-136">When you use the copy element to create multiple instances of a resource type, Resource Manager, by default, deploys those instances in parallel.</span></span> <span data-ttu-id="7954f-137">Ancak, kaynakları sırayla dağıtılan belirtmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7954f-137">However, you may want to specify that the resources are deployed in sequence.</span></span> <span data-ttu-id="7954f-138">Örneğin, bir üretim ortamında güncelleştirirken, güncelleştirmeleri bu nedenle kademelendirebilirsiniz isteyebilirsiniz yalnızca belirli sayıda herhangi bir zamanda güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="7954f-138">For example, when updating a production environment, you may want to stagger the updates so only a certain number are updated at any one time.</span></span>

<span data-ttu-id="7954f-139">Resource Manager seri olarak birden çok örneği dağıtmanıza olanak sağlayan kopyalama öğede özellikleri sunar.</span><span class="sxs-lookup"><span data-stu-id="7954f-139">Resource Manager provides properties on the copy element that enable you to serially deploy multiple instances.</span></span> <span data-ttu-id="7954f-140">Kopya öğe kümesindeki `mode` için **seri** ve `batchSize` aynı anda dağıtılacak örnek sayısı.</span><span class="sxs-lookup"><span data-stu-id="7954f-140">In the copy element, set `mode` to **serial** and `batchSize` to the number of instances to deploy at a time.</span></span> <span data-ttu-id="7954f-141">Önceki toplu iş tamamlanana kadar tek bir toplu başlamıyor şekilde seri moduyla, Resource Manager döngü önceki durumlarda bir bağımlılık oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7954f-141">With serial mode, Resource Manager creates a dependency on earlier instances in the loop, so it does not start one batch until the previous batch completes.</span></span>

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

<span data-ttu-id="7954f-142">Mode özelliğini de kabul eder **paralel**, varsayılan değer olan.</span><span class="sxs-lookup"><span data-stu-id="7954f-142">The mode property also accepts **parallel**, which is the default value.</span></span>

<span data-ttu-id="7954f-143">Fiili kaynaklar oluşturmadan seri kopyalama test etmek için boş iç içe geçmiş şablonları dağıtır aşağıdaki şablonu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7954f-143">To test serial copy without creating actual resources, use the following template that deploys empty nested templates:</span></span>

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

<span data-ttu-id="7954f-144">Dağıtım geçmişi iç içe geçmiş dağıtımları sırada işlenir dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="7954f-144">In the deployment history, notice that the nested deployments are processed in sequence.</span></span>

![Seri dağıtımı](./media/resource-group-create-multiple/serial-copy.png)

<span data-ttu-id="7954f-146">Daha gerçekçi bir senaryo için aşağıdaki örnekte iki örneği birer birer iç içe geçmiş bir şablondan bir Linux VM dağıtır:</span><span class="sxs-lookup"><span data-stu-id="7954f-146">For a more realistic scenario, the following example deploys two instances at a time of a Linux VM from a nested template:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "User name for the Virtual Machine."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Password for the Virtual Machine."
            }
        },
        "dnsLabelPrefix": {
            "type": "string",
            "metadata": {
                "description": "Unique DNS Name for the Public IP used to access the Virtual Machine."
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
                "description": "The Ubuntu version for the VM. This will pick a fully patched image of this given Ubuntu version."
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

## <a name="property-iteration"></a><span data-ttu-id="7954f-147">Özellik yineleme</span><span class="sxs-lookup"><span data-stu-id="7954f-147">Property iteration</span></span>

<span data-ttu-id="7954f-148">Bir özellik için birden çok değer bir kaynak oluşturmak için Ekle bir `copy` özellikler öğesindeki dizi.</span><span class="sxs-lookup"><span data-stu-id="7954f-148">To create multiple values for a property on a resource, add a `copy` array in the properties element.</span></span> <span data-ttu-id="7954f-149">Bu dizi nesnelerini içerir ve her nesnesi aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="7954f-149">This array contains objects, and each object has the following properties:</span></span>

* <span data-ttu-id="7954f-150">ad - için birden çok değer oluşturmak için özelliğinin adı</span><span class="sxs-lookup"><span data-stu-id="7954f-150">name - the name of the property to create multiple values for</span></span>
* <span data-ttu-id="7954f-151">sayısı - oluşturulacak değer sayısı</span><span class="sxs-lookup"><span data-stu-id="7954f-151">count - the number of values to create</span></span>
* <span data-ttu-id="7954f-152">Giriş - özellik atama değerleri içeren bir nesne</span><span class="sxs-lookup"><span data-stu-id="7954f-152">input - an object that contains the values to assign to the property</span></span>  

<span data-ttu-id="7954f-153">Aşağıdaki örnekte nasıl uygulanacağını gösterir `copy` bir sanal makinede dataDisks özelliğine:</span><span class="sxs-lookup"><span data-stu-id="7954f-153">The following example shows how to apply `copy` to the dataDisks property on a virtual machine:</span></span>

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

<span data-ttu-id="7954f-154">Kullanırken dikkat `copyIndex` özelliği yineleme içinde yineleme adı sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7954f-154">Notice that when using `copyIndex` inside a property iteration, you must provide the name of the iteration.</span></span> <span data-ttu-id="7954f-155">Kaynak bir yineleme kullanıldığında ad gerekmez.</span><span class="sxs-lookup"><span data-stu-id="7954f-155">You do not have to provide the name when used with resource iteration.</span></span>

<span data-ttu-id="7954f-156">Kaynak Yöneticisi'ni genişletir `copy` dağıtımı sırasında dizi.</span><span class="sxs-lookup"><span data-stu-id="7954f-156">Resource Manager expands the `copy` array during deployment.</span></span> <span data-ttu-id="7954f-157">Dizi adı özelliğinin adı haline gelir.</span><span class="sxs-lookup"><span data-stu-id="7954f-157">The name of the array becomes the name of the property.</span></span> <span data-ttu-id="7954f-158">Giriş değerleri nesne özellikleri haline gelir.</span><span class="sxs-lookup"><span data-stu-id="7954f-158">The input values become the object properties.</span></span> <span data-ttu-id="7954f-159">Dağıtılan şablonu olur:</span><span class="sxs-lookup"><span data-stu-id="7954f-159">The deployed template becomes:</span></span>

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

<span data-ttu-id="7954f-160">Kaynak ve özellik yineleme birlikte kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7954f-160">You can use resource and property iteration together.</span></span> <span data-ttu-id="7954f-161">Özellik yineleme adlarıyla başvurmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7954f-161">Reference the property iteration by name.</span></span>

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

<span data-ttu-id="7954f-162">Yalnızca bir kopya öğesi her bir kaynağın özelliklerini ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7954f-162">You can only include one copy element in the properties for each resource.</span></span> <span data-ttu-id="7954f-163">Birden fazla özellik için bir yineleme döngüsü belirtmek için kopya dizideki birden çok nesneleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7954f-163">To specify an iteration loop for more than one property, define multiple objects in the copy array.</span></span> <span data-ttu-id="7954f-164">Her nesneyi ayrı olarak yinelendiğinde.</span><span class="sxs-lookup"><span data-stu-id="7954f-164">Each object is iterated separately.</span></span> <span data-ttu-id="7954f-165">Örneğin, her ikisini birden çok örneğini oluşturmak için `frontendIPConfigurations` özelliği ve `loadBalancingRules` bir yük dengeleyici özelliği tek bir kopya öğesinde hem nesnelerini tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="7954f-165">For example, to create multiple instances of both the `frontendIPConfigurations` property and the `loadBalancingRules` property on a load balancer, define both objects in a single copy element:</span></span> 

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

## <a name="depend-on-resources-in-a-loop"></a><span data-ttu-id="7954f-166">Döngü kaynakları bağlıdır</span><span class="sxs-lookup"><span data-stu-id="7954f-166">Depend on resources in a loop</span></span>
<span data-ttu-id="7954f-167">Bir kaynak sonra başka bir kaynak kullanarak dağıtılmış belirttiğiniz `dependsOn` öğesi.</span><span class="sxs-lookup"><span data-stu-id="7954f-167">You specify that a resource is deployed after another resource by using the `dependsOn` element.</span></span> <span data-ttu-id="7954f-168">Döngü kaynaklar topluluğu bağımlı bir kaynak dağıtmak için ' dependsOn'öğesinde kopyalama döngüsü adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="7954f-168">To deploy a resource that depends on the collection of resources in a loop, provide the name of the copy loop in the dependsOn element.</span></span> <span data-ttu-id="7954f-169">Aşağıdaki örnekte, sanal makineyi dağıtmadan önce üç depolama hesapları dağıtmayı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="7954f-169">The following example shows how to deploy three storage accounts before deploying the Virtual Machine.</span></span> <span data-ttu-id="7954f-170">Tam sanal makine tanımı gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="7954f-170">The full Virtual Machine definition is not shown.</span></span> <span data-ttu-id="7954f-171">Copy öğesi kümesine adı olduğuna dikkat edin `storagecopy` ve sanal makineler için dependsOn öğesini de ayarlamak `storagecopy`.</span><span class="sxs-lookup"><span data-stu-id="7954f-171">Notice that the copy element has name set to `storagecopy` and the dependsOn element for the Virtual Machines is also set to `storagecopy`.</span></span>

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

## <a name="create-multiple-instances-of-a-child-resource"></a><span data-ttu-id="7954f-172">Bir alt kaynak birden çok örneğini oluşturma</span><span class="sxs-lookup"><span data-stu-id="7954f-172">Create multiple instances of a child resource</span></span>
<span data-ttu-id="7954f-173">Bir alt kaynak kopyalama döngüsü kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="7954f-173">You cannot use a copy loop for a child resource.</span></span> <span data-ttu-id="7954f-174">Birden çok örneğini genellikle başka bir kaynak içinde iç içe olarak tanımlayan bir kaynak oluşturmak için bunun yerine, kaynak en üst düzey bir kaynak olarak oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7954f-174">To create multiple instances of a resource that you typically define as nested within another resource, you must instead create that resource as a top-level resource.</span></span> <span data-ttu-id="7954f-175">İlişki türü ve adı özellikleri aracılığıyla üst kaynakla tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="7954f-175">You define the relationship with the parent resource through the type and name properties.</span></span>

<span data-ttu-id="7954f-176">Örneğin, data factory içinde alt kaynağı olarak bir veri kümesini tanımlama varsayalım.</span><span class="sxs-lookup"><span data-stu-id="7954f-176">For example, suppose you typically define a dataset as a child resource within a data factory.</span></span>

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

<span data-ttu-id="7954f-177">Veri kümeleri birden çok örneğini oluşturmak için veri fabrikası dışında taşıyın.</span><span class="sxs-lookup"><span data-stu-id="7954f-177">To create multiple instances of data sets, move it outside of the data factory.</span></span> <span data-ttu-id="7954f-178">Veri kümesi, veri fabrikası aynı düzeyde olması gerekir, ancak hala bir alt kaynak data Factory değildir.</span><span class="sxs-lookup"><span data-stu-id="7954f-178">The dataset must be at the same level as the data factory, but it is still a child resource of the data factory.</span></span> <span data-ttu-id="7954f-179">Veri kümesi ve veri fabrikası türü ve adı özellikleri aracılığıyla arasındaki ilişkiyi korur.</span><span class="sxs-lookup"><span data-stu-id="7954f-179">You preserve the relationship between data set and data factory through the type and name properties.</span></span> <span data-ttu-id="7954f-180">Türü artık şablonda onun konumdan çıkarsanabileceği olduğundan, tam olarak nitelenmiş tür biçimde sağlamanız gerekir: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span><span class="sxs-lookup"><span data-stu-id="7954f-180">Since type can no longer be inferred from its position in the template, you must provide the fully qualified type in the format: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span></span>

<span data-ttu-id="7954f-181">Veri Fabrikası örneğiyle birlikte bir üst/alt ilişkisi oluşturmak için üst kaynak adını içeren bir veri kümesi için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="7954f-181">To establish a parent/child relationship with an instance of the data factory, provide a name for the data set that includes the parent resource name.</span></span> <span data-ttu-id="7954f-182">Biçimi kullanın: `{parent-resource-name}/{child-resource-name}`.</span><span class="sxs-lookup"><span data-stu-id="7954f-182">Use the format: `{parent-resource-name}/{child-resource-name}`.</span></span>  

<span data-ttu-id="7954f-183">Aşağıdaki örnek uygulamasını gösterir:</span><span class="sxs-lookup"><span data-stu-id="7954f-183">The following example shows the implementation:</span></span>

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

## <a name="conditionally-deploy-resource"></a><span data-ttu-id="7954f-184">Koşullu kaynağını dağıtma</span><span class="sxs-lookup"><span data-stu-id="7954f-184">Conditionally deploy resource</span></span>

<span data-ttu-id="7954f-185">Bir kaynak dağıtılabilir olup olmadığını belirtmek için kullanın `condition` öğesi.</span><span class="sxs-lookup"><span data-stu-id="7954f-185">To specify whether a resource is deployed, use the `condition` element.</span></span> <span data-ttu-id="7954f-186">Bu öğe için değer true veya false değerine çözümler.</span><span class="sxs-lookup"><span data-stu-id="7954f-186">The value for this element resolves to true or false.</span></span> <span data-ttu-id="7954f-187">Değer doğru olduğunda, kaynak dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="7954f-187">When the value is true, the resource is deployed.</span></span> <span data-ttu-id="7954f-188">Değer false olduğunda, kaynak dağıtılmaz.</span><span class="sxs-lookup"><span data-stu-id="7954f-188">When the value is false, the resource is not deployed.</span></span> <span data-ttu-id="7954f-189">Örneğin, yeni bir depolama hesabı dağıtılan ya da mevcut bir depolama hesabını kullanılan belirtmek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="7954f-189">For example, to specify whether a new storage account is deployed or an existing storage account is used, use:</span></span>

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

<span data-ttu-id="7954f-190">Yeni veya mevcut bir kaynağı kullanarak bir örnek için bkz: [yeni veya varolan bir koşul şablonu](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="7954f-190">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="7954f-191">Sanal makineyi dağıtmak için bir parola veya SSH anahtarı kullanarak bir örnek için bkz: [kullanıcı adı veya SSH koşul şablon](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="7954f-191">For an example of using a password or SSH key to deploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7954f-192">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7954f-192">Next steps</span></span>
* <span data-ttu-id="7954f-193">Bir şablon bölümleri hakkında bilgi edinmek istiyorsanız, bkz: [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7954f-193">If you want to learn about the sections of a template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="7954f-194">Şablonunuzu dağıtma hakkında bilgi edinmek için bkz: [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="7954f-194">To learn how to deploy your template, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>

