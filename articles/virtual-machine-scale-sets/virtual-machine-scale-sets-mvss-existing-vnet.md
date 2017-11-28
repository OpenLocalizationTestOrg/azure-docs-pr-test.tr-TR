---
title: "Bir Azure ölçek kümesi şablonda mevcut bir sanal ağa başvuran | Microsoft Docs"
description: "Nasıl tooadd sanal bir ağ tooan mevcut Azure sanal makine ölçek kümesi şablon öğrenin"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: negat
ms.openlocfilehash: c3034b577e17abc4643dc26d7c38ad643fa26322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-reference-tooan-existing-virtual-network-in-an-azure-scale-set-template"></a><span data-ttu-id="d839f-103">Bir Azure ölçek kümesi şablonunda başvuru tooan varolan sanal ağ ekleme</span><span class="sxs-lookup"><span data-stu-id="d839f-103">Add reference tooan existing virtual network in an Azure scale set template</span></span>

<span data-ttu-id="d839f-104">Bu makalede gösterilmektedir nasıl toomodify hello [minimum uygun ölçek kümesi şablonu](./virtual-machine-scale-sets-mvss-start.md) yeni bir tane oluşturmak yerine mevcut sanal ağda toodeploy.</span><span class="sxs-lookup"><span data-stu-id="d839f-104">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toodeploy into an existing virtual network instead of creating a new one.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="d839f-105">Merhaba şablon tanımını değiştirin</span><span class="sxs-lookup"><span data-stu-id="d839f-105">Change hello template definition</span></span>

<span data-ttu-id="d839f-106">Bizim minimum uygun ölçek kümesi şablon görülebilir [burada](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), ve hello ölçeği mevcut bir sanal ağı Ayarla dağıtmak için bizim şablon görülebilir [burada](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="d839f-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello scale set into an existing virtual network can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json).</span></span> <span data-ttu-id="d839f-107">Merhaba kullanılan fark toocreate bu şablonu inceleyelim (`git diff minimum-viable-scale-set existing-vnet`) tarafından parça parça:</span><span class="sxs-lookup"><span data-stu-id="d839f-107">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="d839f-108">İlk olarak, eklediğimiz bir `subnetId` parametresi.</span><span class="sxs-lookup"><span data-stu-id="d839f-108">First, we add a `subnetId` parameter.</span></span> <span data-ttu-id="d839f-109">Bu dize hello ölçek kümesi yapılandırması hello ölçek tooidentify hello önceden oluşturulmuş alt ağ toodeploy sanal makinelerine kümesi izin vererek, içine geçirilir.</span><span class="sxs-lookup"><span data-stu-id="d839f-109">This string will be passed into hello scale set configuration, allowing hello scale set tooidentify hello pre-created subnet toodeploy virtual machines into.</span></span> <span data-ttu-id="d839f-110">Bu dize hello biçiminde olmalıdır: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`.</span><span class="sxs-lookup"><span data-stu-id="d839f-110">This string must be of hello form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`.</span></span> <span data-ttu-id="d839f-111">Örneğin, toodeploy hello ölçek kümesine mevcut bir sanal ağ adı ile `myvnet`, alt ağ `mysubnet`, kaynak grubu `myrg`ve abonelik `00000000-0000-0000-0000-000000000000`, hello subnetId olacaktır: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.</span><span class="sxs-lookup"><span data-stu-id="d839f-111">For instance, toodeploy hello scale set into an existing virtual network with name `myvnet`, subnet `mysubnet`, resource group `myrg`, and subscription `00000000-0000-0000-0000-000000000000`, hello subnetId would be: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.</span></span>

```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "subnetId": {
+      "type": "string"
     }
   },
```

<span data-ttu-id="d839f-112">Ardından, biz hello hello sanal ağ kaynak silebilirsiniz `resources` dizi varolan bir sanal ağı kullanıyor ve yeni bir tane toodeploy gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="d839f-112">Next, we can delete hello virtual network resource from hello `resources` array, since we are using an existing virtual network and don't need toodeploy a new one.</span></span>

```diff
   "variables": {},
   "resources": [
-    {
-      "type": "Microsoft.Network/virtualNetworks",
-      "name": "myVnet",
-      "location": "[resourceGroup().location]",
-      "apiVersion": "2016-12-01",
-      "properties": {
-        "addressSpace": {
-          "addressPrefixes": [
-            "10.0.0.0/16"
-          ]
-        },
-        "subnets": [
-          {
-            "name": "mySubnet",
-            "properties": {
-              "addressPrefix": "10.0.0.0/16"
-            }
-          }
-        ]
-      }
-    },
```

<span data-ttu-id="d839f-113">Merhaba şablon dağıtılmadan önce hello sanal ağ zaten var, böylece hiçbir gerek toospecify hello ölçek from dependsOn yan tümcesi toohello sanal ağ ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d839f-113">hello virtual network already exists before hello template is deployed, so there is no need toospecify a dependsOn clause from hello scale set toohello virtual network.</span></span> <span data-ttu-id="d839f-114">Bu nedenle, bu satırları sil:</span><span class="sxs-lookup"><span data-stu-id="d839f-114">Thus, we delete these lines:</span></span>

```diff
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "location": "[resourceGroup().location]",
       "apiVersion": "2016-04-30-preview",
-      "dependsOn": [
-        "Microsoft.Network/virtualNetworks/myVnet"
-      ],
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
```

<span data-ttu-id="d839f-115">Son olarak, biz hello geçirmek `subnetId` hello kullanıcı tarafından ayarlanan parametre (kullanmak yerine `resourceId` sanal ağ içinde şablon hangi hello minimum uygun ölçek kümesi aynı dağıtımında, mu hello tooget hello kimliği).</span><span class="sxs-lookup"><span data-stu-id="d839f-115">Finally, we pass in hello `subnetId` parameter set by hello user (instead of using `resourceId` tooget hello id of a vnet in hello same deployment, which is what hello minimum viable scale set template does).</span></span>

```diff
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
-                          "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
+                          "id": "[parameters('subnetId')]"
                         }
                       }
                     }
```




## <a name="next-steps"></a><span data-ttu-id="d839f-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d839f-116">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
