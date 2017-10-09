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
# <a name="convert-a-scale-set-template-tooa-managed-disk-scale-set-template"></a><span data-ttu-id="dd5ac-104">Bir ölçek kümesi şablonu tooa yönetilen disk ölçek kümesi şablonu Dönüştür</span><span class="sxs-lookup"><span data-stu-id="dd5ac-104">Convert a scale set template tooa managed disk scale set template</span></span>

<span data-ttu-id="dd5ac-105">Müşterilerin bir ölçeği yönetilen disk kullanmayan Ayarla oluşturmak için Resource Manager şablonu ile toomodify istiyor, toouse yönetilen disk.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-105">Customers with a Resource Manager template for creating a scale set not using managed disk may wish toomodify it toouse managed disk.</span></span> <span data-ttu-id="dd5ac-106">Bu makalede gösterilmektedir nasıl toodo kullanarak bu, örneğin hello çekme isteğinden [Azure hızlı başlangıç şablonlarını](https://github.com/Azure/azure-quickstart-templates), örnek Resource Manager şablonları için topluluk odaklı bir depo.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-106">This article shows how toodo this, using as an example a pull request from hello [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates), a community-driven repo for sample Resource Manager templates.</span></span> <span data-ttu-id="dd5ac-107">Merhaba tam çekme isteği görülme burada: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), ve hello ilgili hello fark bölümlerdir aşağıda açıklamalarının yanı sıra:</span><span class="sxs-lookup"><span data-stu-id="dd5ac-107">hello full pull request can be seen here: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), and hello relevant parts of hello diff are below, along with explanations:</span></span>

## <a name="making-hello-os-disks-managed"></a><span data-ttu-id="dd5ac-108">Yönetilen hello OS diskleri yapma</span><span class="sxs-lookup"><span data-stu-id="dd5ac-108">Making hello OS disks managed</span></span>

<span data-ttu-id="dd5ac-109">Aşağıdaki Hello fark içinde birkaç değişkenleri ilgili toostorage hesabı ve disk özelliklerini kaldırdınız görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-109">In hello diff below, we can see that we have removed several variables related toostorage account and disk properties.</span></span> <span data-ttu-id="dd5ac-110">Depolama hesabı türü gereklidir artık (Standard_LRS varsayılandır hello), ancak biz istediğinizde, biz yine da belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-110">Storage account type is no longer necessary (Standard_LRS is hello default), but we could still specify it if we wished to.</span></span> <span data-ttu-id="dd5ac-111">Yalnızca Standard_LRS ve Premium_LRS yönetilen disk ile desteklenir.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-111">Only Standard_LRS and Premium_LRS are supported with managed disk.</span></span> <span data-ttu-id="dd5ac-112">Yeni depolama hesabı soneki, benzersiz bir dize dizisi ve sa sayısı hello eski şablon toogenerate depolama hesabı adları kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-112">New storage account suffix, unique string array, and sa count were used in hello old template toogenerate storage account names.</span></span> <span data-ttu-id="dd5ac-113">Yönetilen disk depolama hesapları hello müşterinin adına otomatik olarak oluşturur. çünkü bu değişkenleri artık hello yeni şablona gereklidir.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-113">These variables are no longer necessary in hello new template because managed disk automatically creates storage accounts on hello customer's behalf.</span></span> <span data-ttu-id="dd5ac-114">Yönetilen disk otomatik olarak adları hello temel alınan depolama blob kapsayıcıları ve diskleri için benzer şekilde, vhd kapsayıcı adı ve işletim sistemi disk adı artık gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-114">Similarly, vhd container name and os disk name are no longer necessary because managed disk automatically names hello underlying storage blob containers and disks.</span></span>

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


<span data-ttu-id="dd5ac-115">Aşağıda, biz hello fark, biz hello güncelleştirilmiş bakın hello erken gerekli sürümü ölçek kümesi ile yönetilen disk destek olduğu API sürümü too2016-04-30-Önizleme, hesaplayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-115">In hello diff below, we can see that we updated hello compute api version too2016-04-30-preview, which is hello earliest required version for managed disk support with scale sets.</span></span> <span data-ttu-id="dd5ac-116">Biz yine yönetilmeyen diskleri hello yeni API sürümüyle hello eski sözdizimi isterseniz kullanabilirsiniz olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-116">Note that we could still use unmanaged disks in hello new api version with hello old syntax if desired.</span></span> <span data-ttu-id="dd5ac-117">Diğer bir deyişle, biz yalnızca güncelleştirme hello işlem API sürümü ve başka bir şey değişmez, hello şablon olarak toowork önce devam etmelidir.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-117">In other words, if we only update hello compute api version and don't change anything else, hello template should continue toowork as before.</span></span>

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

<span data-ttu-id="dd5ac-118">Aşağıdaki Hello fark biz hello depolama hesabı kaynağı hello kaynakları diziden tamamen kaldırdığınızı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-118">In hello diff below, we can see that we are removing hello storage account resource from hello resources array completely.</span></span> <span data-ttu-id="dd5ac-119">Yönetilen disk bunları otomatik olarak bizim adımıza oluşturduğundan artık bunları ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-119">We no longer need them since managed disk creates them automatically on our behalf.</span></span>

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

<span data-ttu-id="dd5ac-120">Merhaba fark Aşağıda, biz de hello kaldırıyorsunuz bakın bağlıdır, depolama hesapları oluşturma hello ölçek kümesi toohello döngüden başvuran yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-120">In hello diff below, we can see that we are removing hello depends on clause referring from hello scale set toohello loop that was creating storage accounts.</span></span> <span data-ttu-id="dd5ac-121">Merhaba eski şablonunda bu hello depolama hesapları hello ölçek kümesi oluşturma başladı, ancak bu yan tümcesi artık yönetilen diskle gereklidir önce oluşturulan sağlama.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-121">In hello old template, this was ensuring that hello storage accounts were created before hello scale set began creation, but this clause is no longer necessary with managed disk.</span></span> <span data-ttu-id="dd5ac-122">Biz de hello vhd kapsayıcıları özelliğini kaldırın ve bu özellikler otomatik olarak tarafından yönetilen disk hello başlık altında işlenir gibi işletim sistemi disk adı özelliği hello.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-122">We also remove hello vhd containers property, and hello os disk name property as these properties are automatically handled under hello hood by managed disk.</span></span> <span data-ttu-id="dd5ac-123">Biz onlardan varsa, eklediğimiz `"managedDisk": { "storageAccountType": "Premium_LRS" }` biz premium OS diskleri istediyseniz hello "osDisk" yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-123">If we wished, we could add `"managedDisk": { "storageAccountType": "Premium_LRS" }` in hello "osDisk" configuration if we wanted premium OS disks.</span></span> <span data-ttu-id="dd5ac-124">Yalnızca bir büyük harf olan VM'ler veya küçük'ın ' hello VM sku premium diskleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-124">Only VMs with an uppercase or lowercase 's' in hello VM sku can use premium disks.</span></span>

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

<span data-ttu-id="dd5ac-125">Merhaba ölçek kümesi yapılandırması olup toouse yönetilen veya yönetilmeyen disk için açık bir özellik yok.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-125">There is no explicit property in hello scale set configuration for whether toouse managed or unmanaged disk.</span></span> <span data-ttu-id="dd5ac-126">Merhaba ölçek kümesini hello depolama profilinde mevcut olan hello özelliklerine göre hangi toouse bilir.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-126">hello scale set knows which toouse based on hello properties that are present in hello storage profile.</span></span> <span data-ttu-id="dd5ac-127">Bu nedenle, hello sağ hello depolama profilinde hello ölçek kümesinin özelliklerdir hello şablonu tooensure değiştirirken önemlidir.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-127">Thus, it is important when modifying hello template tooensure that hello right properties are in hello storage profile of hello scale set.</span></span>


## <a name="data-disks"></a><span data-ttu-id="dd5ac-128">Veri diskleri</span><span class="sxs-lookup"><span data-stu-id="dd5ac-128">Data disks</span></span>

<span data-ttu-id="dd5ac-129">Yukarıdaki Hello değişiklikleri ile Merhaba ölçek kümesi kullanır yönetilen disklerde hello işletim sistemi, ancak, veri diskleri disk? tooadd veri diskleri, aynı "osDisk" düzey hello en altındaki "storageProfile" Merhaba "dataDisks" özelliğini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-129">With hello changes above, hello scale set uses managed disks for hello OS disk, but what about data disks? tooadd data disks, add hello "dataDisks" property under "storageProfile" at hello same level as "osDisk".</span></span> <span data-ttu-id="dd5ac-130">Merhaba hello özelliğinin değeri her biri "(bir VM üzerinde veri disk başına benzersiz olması gerekir) LUN'un" özellikleri vardır, JSON nesnelerini listesidir "("boş"olduğundan şu anda hello yalnızca seçeneği desteklenir) createOption" ve "diskSizeGB" (Merhaba gigabayt cinsinden hello diskin boyutunu; olmalıdır büyüktür 0 ile 1024'ten az) gibi hello aşağıdaki örneğine içinde:</span><span class="sxs-lookup"><span data-stu-id="dd5ac-130">hello value of hello property is a JSON list of objects, each of which has properties "lun" (which must be unique per data disk on a VM), "createOption" ("empty" is currently hello only supported option), and "diskSizeGB" (hello size of hello disk in gigabytes; must be greater than 0 and less than 1024) as in hello following example:</span></span> 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

<span data-ttu-id="dd5ac-131">Belirtirseniz `n` diskleri bu dizideki her VM hello ölçek kümesi alır `n` veri diski.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-131">If you specify `n` disks in this array, each VM in hello scale set gets `n` data disks.</span></span> <span data-ttu-id="dd5ac-132">Ancak, bu veri diskleri ham aygıtların olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-132">Do note, however, that these data disks are raw devices.</span></span> <span data-ttu-id="dd5ac-133">Bunlar biçimlendirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-133">They are not formatted.</span></span> <span data-ttu-id="dd5ac-134">Bu toohello müşteri tooattach, paritition ve biçiminde hello diskleri kullanmadan önce olur.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-134">It is up toohello customer tooattach, paritition, and format hello disks before using them.</span></span> <span data-ttu-id="dd5ac-135">Biz de isteğe bağlı olarak, belirtebilirsiniz `"managedDisk": { "storageAccountType": "Premium_LRS" }` , her veri diski nesnesi toospecify premium veri diski olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-135">Optionally, we could also specify `"managedDisk": { "storageAccountType": "Premium_LRS" }` in each data disk object toospecify that it should be a premium data disk.</span></span> <span data-ttu-id="dd5ac-136">Yalnızca bir büyük harf olan VM'ler veya küçük'ın ' hello VM sku premium diskleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd5ac-136">Only VMs with an uppercase or lowercase 's' in hello VM sku can use premium disks.</span></span>

<span data-ttu-id="dd5ac-137">Veri diskleri ölçek kümeleri ile kullanma hakkında daha fazla toolearn bkz [bu makalede](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="dd5ac-137">toolearn more about using data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="dd5ac-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dd5ac-138">Next steps</span></span>
<span data-ttu-id="dd5ac-139">Örneğin Ölçek kümeleri kullanarak Resource Manager şablonları arama "vmss için" hello [Azure hızlı başlangıç şablonlarını github deposuna](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="dd5ac-139">For example Resource Manager templates using scale sets, search for "vmss" in hello [Azure Quickstart Templates github repo](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="dd5ac-140">Genel bilgi için hello denetleyin [ölçek kümeleri için ana giriş sayfasının](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="dd5ac-140">For general information, check out hello [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>

