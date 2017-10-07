---
title: "Bir Azure ölçek kümesi şablonu özel görüntü başvurusu | Microsoft Docs"
description: "Nasıl tooadd özel bir görüntü tooan mevcut Azure sanal makine ölçek kümesi şablon öğrenin"
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
ms.openlocfilehash: 6a17d989e44d241b460238c0106350c3ef038e56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-custom-image-tooan-azure-scale-set-template"></a>Şablon özel görüntü tooan Azure ölçek kümesi ekleme

Bu makalede gösterilmektedir nasıl toomodify hello [minimum uygun ölçek kümesi şablonu](./virtual-machine-scale-sets-mvss-start.md) özel görüntüden toodeploy.

## <a name="change-hello-template-definition"></a>Merhaba şablon tanımını değiştirin

Bizim minimum uygun ölçek kümesi şablon görülebilir [burada](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), ve hello ölçeği özel bir görüntüden Ayarla dağıtmak için bizim şablon görülebilir [burada](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json). Merhaba kullanılan fark toocreate bu şablonu inceleyelim (`git diff minimum-viable-scale-set custom-image`) tarafından parça parça:

### <a name="creating-a-managed-disk-image"></a>Yönetilen disk görüntüsü oluşturma

Bir özel yönetilen disk görüntüsü zaten varsa (bir kaynak türü `Microsoft.Compute/images`), sonra da bu bölümü atlayabilirsiniz.

İlk olarak, eklediğimiz bir `sourceImageVhdUri` hello URI genelleştirilmiş toohello blob hello özel görüntü toodeploy gelen içeren Azure storage'da olan parametre.


```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "sourceImageVhdUri": {
+      "type": "string",
+      "metadata": {
+        "description": "hello source of hello generalized blob containing hello custom image"
+      }
     }
   },
   "variables": {},
```

Ardından, bir kaynak türü eklediğimiz `Microsoft.Compute/images`, hangi hello yönetilen disk görüntüsü URI'da bulunan genelleştirilmiş hello blob temel `sourceImageVhdUri`. Bu görüntü hello olmalıdır kullandığı hello ölçek kümesi aynı bölgede. Merhaba görüntü Hello özelliklerinde biz hello işletim sistemi türü, hello blob hello konumunu belirtin (Merhaba gelen `sourceImageVhdUri` parametresi) ve hello depolama hesabı türü:

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

Hello ölçek kümesi kaynağı, eklediğimiz bir `dependsOn` toohello özel görüntü toomake hello görüntüsünü oluşturan toodeploy bu görüntüden hello ölçek kümesini denemeden önce emin başvuran yan tümcesi:

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

### <a name="changing-scale-set-properties-toouse-hello-managed-disk-image"></a>Ölçeğin değiştirilmesi özellikleri toouse hello yönetilen disk resmi ayarlama

Merhaba, `imageReference` hello ölçeğini ayarlama `storageProfile`, hello publisher, teklif, sku ve platform görüntüsü belirtmek yerine hello belirttiğimiz `id` Merhaba, `Microsoft.Compute/images` kaynak:

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

Bu örnekte, kullandığımız hello `resourceId` işlevi tooget hello kaynak kimliği hello görüntüsünün oluşturulan hello aynı şablonu. Hello yönetilen disk görüntüsü önceden oluşturduysanız, bunun yerine, görüntü hello kimliğini sağlamalıdır. Bu kimliği hello biçiminde olmalıdır: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.


## <a name="next-steps"></a>Sonraki Adımlar

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
