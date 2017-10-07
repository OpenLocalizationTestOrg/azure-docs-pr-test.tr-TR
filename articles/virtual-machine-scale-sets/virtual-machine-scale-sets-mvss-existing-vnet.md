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
# <a name="add-reference-tooan-existing-virtual-network-in-an-azure-scale-set-template"></a>Bir Azure ölçek kümesi şablonunda başvuru tooan varolan sanal ağ ekleme

Bu makalede gösterilmektedir nasıl toomodify hello [minimum uygun ölçek kümesi şablonu](./virtual-machine-scale-sets-mvss-start.md) yeni bir tane oluşturmak yerine mevcut sanal ağda toodeploy.

## <a name="change-hello-template-definition"></a>Merhaba şablon tanımını değiştirin

Bizim minimum uygun ölçek kümesi şablon görülebilir [burada](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), ve hello ölçeği mevcut bir sanal ağı Ayarla dağıtmak için bizim şablon görülebilir [burada](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json). Merhaba kullanılan fark toocreate bu şablonu inceleyelim (`git diff minimum-viable-scale-set existing-vnet`) tarafından parça parça:

İlk olarak, eklediğimiz bir `subnetId` parametresi. Bu dize hello ölçek kümesi yapılandırması hello ölçek tooidentify hello önceden oluşturulmuş alt ağ toodeploy sanal makinelerine kümesi izin vererek, içine geçirilir. Bu dize hello biçiminde olmalıdır: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`. Örneğin, toodeploy hello ölçek kümesine mevcut bir sanal ağ adı ile `myvnet`, alt ağ `mysubnet`, kaynak grubu `myrg`ve abonelik `00000000-0000-0000-0000-000000000000`, hello subnetId olacaktır: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.

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

Ardından, biz hello hello sanal ağ kaynak silebilirsiniz `resources` dizi varolan bir sanal ağı kullanıyor ve yeni bir tane toodeploy gerek yoktur.

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

Merhaba şablon dağıtılmadan önce hello sanal ağ zaten var, böylece hiçbir gerek toospecify hello ölçek from dependsOn yan tümcesi toohello sanal ağ ayarlayın. Bu nedenle, bu satırları sil:

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

Son olarak, biz hello geçirmek `subnetId` hello kullanıcı tarafından ayarlanan parametre (kullanmak yerine `resourceId` sanal ağ içinde şablon hangi hello minimum uygun ölçek kümesi aynı dağıtımında, mu hello tooget hello kimliği).

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




## <a name="next-steps"></a>Sonraki adımlar

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
