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
# <a name="add-a-custom-image-to-an-azure-scale-set-template"></a><span data-ttu-id="baa38-103">Bir Azure ölçek kümesi şablonuna özel bir görüntü ekleme</span><span class="sxs-lookup"><span data-stu-id="baa38-103">Add a custom image to an Azure scale set template</span></span>

<span data-ttu-id="baa38-104">Bu makalede nasıl değiştirileceğini gösterir [minimum uygun ölçek kümesi şablonu](./virtual-machine-scale-sets-mvss-start.md) özel görüntüsünü dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="baa38-104">This article shows how to modify the [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) to deploy from custom image.</span></span>

## <a name="change-the-template-definition"></a><span data-ttu-id="baa38-105">Şablon tanımını değiştirin</span><span class="sxs-lookup"><span data-stu-id="baa38-105">Change the template definition</span></span>

<span data-ttu-id="baa38-106">Bizim minimum uygun ölçek kümesi şablon görülebilir [burada](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), ve ölçek dağıtma özel bir görüntüden ayarlamak için bizim şablon görülebilir [burada](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="baa38-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying the scale set from a custom image can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json).</span></span> <span data-ttu-id="baa38-107">Bu şablon oluşturmak için kullanılan fark inceleyelim (`git diff minimum-viable-scale-set custom-image`) tarafından parça parça:</span><span class="sxs-lookup"><span data-stu-id="baa38-107">Let's examine the diff used to create this template (`git diff minimum-viable-scale-set custom-image`) piece by piece:</span></span>

### <a name="creating-a-managed-disk-image"></a><span data-ttu-id="baa38-108">Yönetilen disk görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="baa38-108">Creating a managed disk image</span></span>

<span data-ttu-id="baa38-109">Bir özel yönetilen disk görüntüsü zaten varsa (bir kaynak türü `Microsoft.Compute/images`), sonra da bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="baa38-109">If you already have a custom managed disk image (a resource of type `Microsoft.Compute/images`), then you can skip this section.</span></span>

<span data-ttu-id="baa38-110">İlk olarak, eklediğimiz bir `sourceImageVhdUri` dağıtım yapmak özel görüntüsünü içeren Azure depolama alanında genelleştirilmiş blob URI'si olan parametre.</span><span class="sxs-lookup"><span data-stu-id="baa38-110">First, we add a `sourceImageVhdUri` parameter, which is the URI to the generalized blob in Azure Storage that contains the custom image to deploy from.</span></span>


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

<span data-ttu-id="baa38-111">Ardından, bir kaynak türü eklediğimiz `Microsoft.Compute/images`, yönetilen disk görüntüyü URI'da bulunan genelleştirilmiş blob dayalı olduğu `sourceImageVhdUri`.</span><span class="sxs-lookup"><span data-stu-id="baa38-111">Next, we add a resource of type `Microsoft.Compute/images`, which is the managed disk image based on the generalized blob located at URI `sourceImageVhdUri`.</span></span> <span data-ttu-id="baa38-112">Bu görüntü kullandığı ölçek kümesi ile aynı bölgede olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="baa38-112">This image must be in the same region as the scale set that uses it.</span></span> <span data-ttu-id="baa38-113">Görüntü özelliklerinde biz işletim sistemi türü, blob konumunu belirtin (gelen `sourceImageVhdUri` parametresi) ve depolama hesabı türü:</span><span class="sxs-lookup"><span data-stu-id="baa38-113">In the properties of the image, we specify the OS type, the location of the blob (from the `sourceImageVhdUri` parameter), and the storage account type:</span></span>

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

<span data-ttu-id="baa38-114">Eklediğimiz kaynak, Ölçek kümesindeki bir `dependsOn` ölçek kümesi bu görüntüden dağıtmayı denemeden önce görüntünün emin olmak için özel görüntü başvuran yan tümcesi oluşturulmuş:</span><span class="sxs-lookup"><span data-stu-id="baa38-114">In the scale set resource, we add a `dependsOn` clause referring to the custom image to make sure the image gets created before the scale set tries to deploy from that image:</span></span>

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

### <a name="changing-scale-set-properties-to-use-the-managed-disk-image"></a><span data-ttu-id="baa38-115">Ölçeğin değiştirilmesi yönetilen disk görüntüsü kullanmak için özelliklerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="baa38-115">Changing scale set properties to use the managed disk image</span></span>

<span data-ttu-id="baa38-116">İçinde `imageReference` ölçeğini ayarlama `storageProfile`, yayımcı, teklif, sku ve platform görüntüsü belirtmek yerine, biz belirtin `id` , `Microsoft.Compute/images` kaynak:</span><span class="sxs-lookup"><span data-stu-id="baa38-116">In the `imageReference` of the scale set `storageProfile`, instead of specifying the publisher, offer, sku, and version of a platform image, we specify the `id` of the `Microsoft.Compute/images` resource:</span></span>

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

<span data-ttu-id="baa38-117">Bu örnekte, kullandığımız `resourceId` aynı şablonunda oluşturulan görüntü kaynak kimliği almak için işlevi.</span><span class="sxs-lookup"><span data-stu-id="baa38-117">In this example, we use the `resourceId` function to get the resource ID of the image created in the same template.</span></span> <span data-ttu-id="baa38-118">Yönetilen disk görüntüsü önceden oluşturduysanız, bunun yerine, görüntü kimliğini sağlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="baa38-118">If you have created the managed disk image beforehand, you should provide the id of that image instead.</span></span> <span data-ttu-id="baa38-119">Bu kimliği biçiminde olmalıdır: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.</span><span class="sxs-lookup"><span data-stu-id="baa38-119">This id must be of the form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.</span></span>


## <a name="next-steps"></a><span data-ttu-id="baa38-120">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="baa38-120">Next Steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
