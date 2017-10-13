---
title: "Bir Azure ölçek kümesi şablonu özel görüntü başvurusu | Microsoft Docs"
description: "Özel görüntü mevcut bir Azure sanal makine ölçek kümesi şablona eklemeyi öğrenin"
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
ms.date: 5/10/2017
ms.author: negat
ms.openlocfilehash: cf52fc9e95267c4bc5c0106aadf626685ddd5c24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-custom-image-to-an-azure-scale-set-template"></a>Bir Azure ölçek kümesi şablonuna özel bir görüntü ekleme

Bu makalede nasıl değiştirileceğini gösterir [minimum uygun ölçek kümesi şablonu](./virtual-machine-scale-sets-mvss-start.md) özel görüntüsünü dağıtmak için.

## <a name="change-the-template-definition"></a>Şablon tanımını değiştirin

Bizim minimum uygun ölçek kümesi şablon görülebilir [burada](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), ve ölçek dağıtma özel bir görüntüden ayarlamak için bizim şablon görülebilir [burada](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json). Bu şablon oluşturmak için kullanılan fark inceleyelim (`git diff minimum-viable-scale-set custom-image`) tarafından parça parça:

### <a name="creating-a-managed-disk-image"></a>Yönetilen disk görüntüsü oluşturma

Bir özel yönetilen disk görüntüsü zaten varsa (bir kaynak türü `Microsoft.Compute/images`), sonra da bu bölümü atlayabilirsiniz.

İlk olarak, eklediğimiz bir `sourceImageVhdUri` dağıtım yapmak özel görüntüsünü içeren Azure depolama alanında genelleştirilmiş blob URI'si olan parametre.


```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "sourceImageVhdUri": {
+      "type": "string",
+      "metadata": {
+        "description": "The source of the generalized blob containing the custom image"
+      }
     }
   },
   "variables": {},
```

Ardından, bir kaynak türü eklediğimiz `Microsoft.Compute/images`, yönetilen disk görüntüyü URI'da bulunan genelleştirilmiş blob dayalı olduğu `sourceImageVhdUri`. Bu görüntü kullandığı ölçek kümesi ile aynı bölgede olması gerekir. Görüntü özelliklerinde biz işletim sistemi türü, blob konumunu belirtin (gelen `sourceImageVhdUri` parametresi) ve depolama hesabı türü:

```diff
   "resources": [
     {
+      "type": "Microsoft.Compute/images",
+      "apiVersion": "2016-04-30-preview",
+      "name": "myCustomImage",
+      "location": "[resourceGroup().location]",
+      "properties": {
+        "storageProfile": {
+          "osDisk": {
+            "osType": "Linux",
+            "osState": "Generalized",
+            "blobUri": "[parameters('sourceImageVhdUri')]",
+            "storageAccountType": "Standard_LRS"
+          }
+        }
+      }
+    },
+    {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "location": "[resourceGroup().location]",

```

Eklediğimiz kaynak, Ölçek kümesindeki bir `dependsOn` ölçek kümesi bu görüntüden dağıtmayı denemeden önce görüntünün emin olmak için özel görüntü başvuran yan tümcesi oluşturulmuş:

```diff
       "location": "[resourceGroup().location]",
       "apiVersion": "2016-04-30-preview",
       "dependsOn": [
-        "Microsoft.Network/virtualNetworks/myVnet"
+        "Microsoft.Network/virtualNetworks/myVnet",
+        "Microsoft.Compute/images/myCustomImage"
       ],
       "sku": {
         "name": "Standard_A1",

```

### <a name="changing-scale-set-properties-to-use-the-managed-disk-image"></a>Ölçeğin değiştirilmesi yönetilen disk görüntüsü kullanmak için özelliklerini ayarlama

İçinde `imageReference` ölçeğini ayarlama `storageProfile`, yayımcı, teklif, sku ve platform görüntüsü belirtmek yerine, biz belirtin `id` , `Microsoft.Compute/images` kaynak:

```diff
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
-              "publisher": "Canonical",
-              "offer": "UbuntuServer",
-              "sku": "16.04-LTS",
-              "version": "latest"
+              "id": "[resourceId('Microsoft.Compute/images', 'myCustomImage')]"
             }
           },
           "osProfile": {
```

Bu örnekte, kullandığımız `resourceId` aynı şablonunda oluşturulan görüntü kaynak kimliği almak için işlevi. Yönetilen disk görüntüsü önceden oluşturduysanız, bunun yerine, görüntü kimliğini sağlamalıdır. Bu kimliği biçiminde olmalıdır: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.


## <a name="next-steps"></a>Sonraki Adımlar

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
