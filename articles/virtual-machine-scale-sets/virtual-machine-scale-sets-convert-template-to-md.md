---
title: "aaaConvert bir Azure Resource Manager ölçeği ayarlamak şablonu toouse yönetilen disk | Microsoft Docs"
description: "Bir ölçek kümesi şablonu tooa yönetilen disk ölçek kümesi şablonu dönüştürün."
keywords: "Sanal makine ölçekleme kümeleri"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: bc8c377a-8c3f-45b8-8b2d-acc2d6d0b1e8
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/18/2017
ms.author: negat
ms.openlocfilehash: 66c2217647e57ed2cfa39660c0175710ae2e63be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-scale-set-template-tooa-managed-disk-scale-set-template"></a>Bir ölçek kümesi şablonu tooa yönetilen disk ölçek kümesi şablonu Dönüştür

Müşterilerin bir ölçeği yönetilen disk kullanmayan Ayarla oluşturmak için Resource Manager şablonu ile toomodify istiyor, toouse yönetilen disk. Bu makalede gösterilmektedir nasıl toodo kullanarak bu, örneğin hello çekme isteğinden [Azure hızlı başlangıç şablonlarını](https://github.com/Azure/azure-quickstart-templates), örnek Resource Manager şablonları için topluluk odaklı bir depo. Merhaba tam çekme isteği görülme burada: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), ve hello ilgili hello fark bölümlerdir aşağıda açıklamalarının yanı sıra:

## <a name="making-hello-os-disks-managed"></a>Yönetilen hello OS diskleri yapma

Aşağıdaki Hello fark içinde birkaç değişkenleri ilgili toostorage hesabı ve disk özelliklerini kaldırdınız görebilirsiniz. Depolama hesabı türü gereklidir artık (Standard_LRS varsayılandır hello), ancak biz istediğinizde, biz yine da belirtebilirsiniz. Yalnızca Standard_LRS ve Premium_LRS yönetilen disk ile desteklenir. Yeni depolama hesabı soneki, benzersiz bir dize dizisi ve sa sayısı hello eski şablon toogenerate depolama hesabı adları kullanılmıştır. Yönetilen disk depolama hesapları hello müşterinin adına otomatik olarak oluşturur. çünkü bu değişkenleri artık hello yeni şablona gereklidir. Yönetilen disk otomatik olarak adları hello temel alınan depolama blob kapsayıcıları ve diskleri için benzer şekilde, vhd kapsayıcı adı ve işletim sistemi disk adı artık gerekli değildir.

```diff
   "variables": {
-    "storageAccountType": "Standard_LRS",
     "namingInfix": "[toLower(substring(concat(parameters('vmssName'), uniqueString(resourceGroup().id)), 0, 9))]",
     "longNamingInfix": "[toLower(parameters('vmssName'))]",
-    "newStorageAccountSuffix": "[concat(variables('namingInfix'), 'sa')]",
-    "uniqueStringArray": [
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '0')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '1')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '2')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '3')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '4')))]"
-    ],
-    "saCount": "[length(variables('uniqueStringArray'))]",
-    "vhdContainerName": "[concat(variables('namingInfix'), 'vhd')]",
-    "osDiskName": "[concat(variables('namingInfix'), 'osdisk')]",
     "addressPrefix": "10.0.0.0/16",
     "subnetPrefix": "10.0.0.0/24",
     "virtualNetworkName": "[concat(variables('namingInfix'), 'vnet')]",
```


Aşağıda, biz hello fark, biz hello güncelleştirilmiş bakın hello erken gerekli sürümü ölçek kümesi ile yönetilen disk destek olduğu API sürümü too2016-04-30-Önizleme, hesaplayabilirsiniz. Biz yine yönetilmeyen diskleri hello yeni API sürümüyle hello eski sözdizimi isterseniz kullanabilirsiniz olduğunu unutmayın. Diğer bir deyişle, biz yalnızca güncelleştirme hello işlem API sürümü ve başka bir şey değişmez, hello şablon olarak toowork önce devam etmelidir.

```diff
@@ -86,7 +74,7 @@
       "version": "latest"
     },
     "imageReference": "[variables('osType')]",
-    "computeApiVersion": "2016-03-30",
+    "computeApiVersion": "2016-04-30-preview",
     "networkApiVersion": "2016-03-30",
     "storageApiVersion": "2015-06-15"
   },
```

Aşağıdaki Hello fark biz hello depolama hesabı kaynağı hello kaynakları diziden tamamen kaldırdığınızı görebilirsiniz. Yönetilen disk bunları otomatik olarak bizim adımıza oluşturduğundan artık bunları ihtiyacımız var.

```diff
@@ -113,19 +101,6 @@
       }
     },
-    {
-      "type": "Microsoft.Storage/storageAccounts",
-      "name": "[concat(variables('uniqueStringArray')[copyIndex()], variables('newStorageAccountSuffix'))]",
-      "location": "[resourceGroup().location]",
-      "apiVersion": "[variables('storageApiVersion')]",
-      "copy": {
-        "name": "storageLoop",
-        "count": "[variables('saCount')]"
-      },
-      "properties": {
-        "accountType": "[variables('storageAccountType')]"
-      }
-    },
     {
       "type": "Microsoft.Network/publicIPAddresses",
       "name": "[variables('publicIPAddressName')]",
       "location": "[resourceGroup().location]",
```

Merhaba fark Aşağıda, biz de hello kaldırıyorsunuz bakın bağlıdır, depolama hesapları oluşturma hello ölçek kümesi toohello döngüden başvuran yan tümcesi. Merhaba eski şablonunda bu hello depolama hesapları hello ölçek kümesi oluşturma başladı, ancak bu yan tümcesi artık yönetilen diskle gereklidir önce oluşturulan sağlama. Biz de hello vhd kapsayıcıları özelliğini kaldırın ve bu özellikler otomatik olarak tarafından yönetilen disk hello başlık altında işlenir gibi işletim sistemi disk adı özelliği hello. Biz onlardan varsa, eklediğimiz `"managedDisk": { "storageAccountType": "Premium_LRS" }` biz premium OS diskleri istediyseniz hello "osDisk" yapılandırma. Yalnızca bir büyük harf olan VM'ler veya küçük'ın ' hello VM sku premium diskleri kullanabilirsiniz.

```diff
@@ -183,7 +158,6 @@
       "location": "[resourceGroup().location]",
       "apiVersion": "[variables('computeApiVersion')]",
       "dependsOn": [
-        "storageLoop",
         "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
         "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
       ],
@@ -200,16 +174,8 @@
         "virtualMachineProfile": {
           "storageProfile": {
             "osDisk": {
-              "vhdContainers": [
-                "[concat('https://', variables('uniqueStringArray')[0], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[1], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[2], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[3], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[4], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]"
-              ],
-              "name": "[variables('osDiskName')]",
             },
             "imageReference": "[variables('imageReference')]"
           },

```

Merhaba ölçek kümesi yapılandırması olup toouse yönetilen veya yönetilmeyen disk için açık bir özellik yok. Merhaba ölçek kümesini hello depolama profilinde mevcut olan hello özelliklerine göre hangi toouse bilir. Bu nedenle, hello sağ hello depolama profilinde hello ölçek kümesinin özelliklerdir hello şablonu tooensure değiştirirken önemlidir.


## <a name="data-disks"></a>Veri diskleri

Yukarıdaki Hello değişiklikleri ile Merhaba ölçek kümesi kullanır yönetilen disklerde hello işletim sistemi, ancak, veri diskleri disk? tooadd veri diskleri, aynı "osDisk" düzey hello en altındaki "storageProfile" Merhaba "dataDisks" özelliğini ekleyin. Merhaba hello özelliğinin değeri her biri "(bir VM üzerinde veri disk başına benzersiz olması gerekir) LUN'un" özellikleri vardır, JSON nesnelerini listesidir "("boş"olduğundan şu anda hello yalnızca seçeneği desteklenir) createOption" ve "diskSizeGB" (Merhaba gigabayt cinsinden hello diskin boyutunu; olmalıdır büyüktür 0 ile 1024'ten az) gibi hello aşağıdaki örneğine içinde: 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

Belirtirseniz `n` diskleri bu dizideki her VM hello ölçek kümesi alır `n` veri diski. Ancak, bu veri diskleri ham aygıtların olduğunu unutmayın. Bunlar biçimlendirilmemiş. Bu toohello müşteri tooattach, paritition ve biçiminde hello diskleri kullanmadan önce olur. Biz de isteğe bağlı olarak, belirtebilirsiniz `"managedDisk": { "storageAccountType": "Premium_LRS" }` , her veri diski nesnesi toospecify premium veri diski olması gerekir. Yalnızca bir büyük harf olan VM'ler veya küçük'ın ' hello VM sku premium diskleri kullanabilirsiniz.

Veri diskleri ölçek kümeleri ile kullanma hakkında daha fazla toolearn bkz [bu makalede](./virtual-machine-scale-sets-attached-disks.md).


## <a name="next-steps"></a>Sonraki adımlar
Örneğin Ölçek kümeleri kullanarak Resource Manager şablonları arama "vmss için" hello [Azure hızlı başlangıç şablonlarını github deposuna](https://github.com/Azure/azure-quickstart-templates).

Genel bilgi için hello denetleyin [ölçek kümeleri için ana giriş sayfasının](https://azure.microsoft.com/services/virtual-machine-scale-sets/).

