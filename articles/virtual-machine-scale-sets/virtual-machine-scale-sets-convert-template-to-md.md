---
title: "Yönetilen disk kullanmak üzere bir Azure Resource Manager ölçek kümesi şablonu Dönüştür | Microsoft Docs"
description: "Ölçek kümesi şablon yönetilen disk ölçek kümesi şablona dönüştürebilirsiniz."
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
ms.openlocfilehash: 2f5cb85703888c5056611d466f508547ee72e44b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="convert-a-scale-set-template-to-a-managed-disk-scale-set-template"></a><span data-ttu-id="15f68-104">Ölçek kümesi şablon yönetilen disk ölçek kümesi şablona dönüştürme</span><span class="sxs-lookup"><span data-stu-id="15f68-104">Convert a scale set template to a managed disk scale set template</span></span>

<span data-ttu-id="15f68-105">Yönetilen disk kullanmayan bir ölçek kümesi oluşturmak için Resource Manager şablonu ile müşteriler, yönetilen disk kullanacak şekilde değiştirmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15f68-105">Customers with a Resource Manager template for creating a scale set not using managed disk may wish to modify it to use managed disk.</span></span> <span data-ttu-id="15f68-106">Bu makalede, örnek olarak bir çekme isteğinden kullanarak bunu gösterilmektedir [Azure hızlı başlangıç şablonlarını](https://github.com/Azure/azure-quickstart-templates), örnek Resource Manager şablonları için topluluk odaklı bir depo.</span><span class="sxs-lookup"><span data-stu-id="15f68-106">This article shows how to do this, using as an example a pull request from the [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates), a community-driven repo for sample Resource Manager templates.</span></span> <span data-ttu-id="15f68-107">Tam çekme isteği burada görülebilir: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), ve açıklamalarının yanı sıra bazı aşağıda fark ilgili bölümleri:</span><span class="sxs-lookup"><span data-stu-id="15f68-107">The full pull request can be seen here: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), and the relevant parts of the diff are below, along with explanations:</span></span>

## <a name="making-the-os-disks-managed"></a><span data-ttu-id="15f68-108">Yönetilen işletim sistemi diskleri yapma</span><span class="sxs-lookup"><span data-stu-id="15f68-108">Making the OS disks managed</span></span>

<span data-ttu-id="15f68-109">Depolama hesabı ve disk özelliklerine ilgili çeşitli değişkenler kaldırdınız aşağıdaki fark görebiliriz.</span><span class="sxs-lookup"><span data-stu-id="15f68-109">In the diff below, we can see that we have removed several variables related to storage account and disk properties.</span></span> <span data-ttu-id="15f68-110">Depolama hesabı türü gereklidir artık (Standard_LRS varsayılan değerdir), ancak biz istediğinizde, biz yine da belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15f68-110">Storage account type is no longer necessary (Standard_LRS is the default), but we could still specify it if we wished to.</span></span> <span data-ttu-id="15f68-111">Yalnızca Standard_LRS ve Premium_LRS yönetilen disk ile desteklenir.</span><span class="sxs-lookup"><span data-stu-id="15f68-111">Only Standard_LRS and Premium_LRS are supported with managed disk.</span></span> <span data-ttu-id="15f68-112">Yeni depolama hesabı soneki, benzersiz bir dize dizisi ve sa sayısı eski şablonunda depolama hesabı adları oluşturmak için kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="15f68-112">New storage account suffix, unique string array, and sa count were used in the old template to generate storage account names.</span></span> <span data-ttu-id="15f68-113">Yönetilen disk depolama hesapları müşterinin adına otomatik olarak oluşturur. çünkü bu değişkenleri artık yeni şablona gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="15f68-113">These variables are no longer necessary in the new template because managed disk automatically creates storage accounts on the customer's behalf.</span></span> <span data-ttu-id="15f68-114">Yönetilen disk otomatik olarak adları temel alınan depolama blob kapsayıcıları ve diskleri olduğundan benzer şekilde, vhd kapsayıcı adı ve işletim sistemi disk adı artık gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="15f68-114">Similarly, vhd container name and os disk name are no longer necessary because managed disk automatically names the underlying storage blob containers and disks.</span></span>

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


<span data-ttu-id="15f68-115">Aşağıdaki fark biz işlem güncelleştirilmiş görebiliriz 2016-04-30-ölçek kümesi ile yönetilen disk desteği için gerekli en erken sürümü olan önizlemeye API sürümü.</span><span class="sxs-lookup"><span data-stu-id="15f68-115">In the diff below, we can see that we updated the compute api version to 2016-04-30-preview, which is the earliest required version for managed disk support with scale sets.</span></span> <span data-ttu-id="15f68-116">Biz yine yönetilmeyen diskleri eski sözdizimi yeni API sürümüyle isterseniz kullanabilirsiniz olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="15f68-116">Note that we could still use unmanaged disks in the new api version with the old syntax if desired.</span></span> <span data-ttu-id="15f68-117">Diğer bir deyişle, biz yalnızca işlem güncelleştirirseniz API sürümü ve başka bir şey değişmez, şablon önceki gibi çalışmaya devam etmelidir.</span><span class="sxs-lookup"><span data-stu-id="15f68-117">In other words, if we only update the compute api version and don't change anything else, the template should continue to work as before.</span></span>

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

<span data-ttu-id="15f68-118">Aşağıdaki fark biz depolama hesabı kaynağı kaynakları diziden tamamen kaldırdığınızı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15f68-118">In the diff below, we can see that we are removing the storage account resource from the resources array completely.</span></span> <span data-ttu-id="15f68-119">Yönetilen disk bunları otomatik olarak bizim adımıza oluşturduğundan artık bunları ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="15f68-119">We no longer need them since managed disk creates them automatically on our behalf.</span></span>

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

<span data-ttu-id="15f68-120">Aşağıdaki fark biz kaldırma görebiliriz depolama hesapları oluşturma döngü ayarlamak ölçekten başvuran yan tümcesi bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="15f68-120">In the diff below, we can see that we are removing the depends on clause referring from the scale set to the loop that was creating storage accounts.</span></span> <span data-ttu-id="15f68-121">Eski şablonunda, bu depolama hesapları ölçek kümesi oluşturma başladı, ancak bu yan tümcesi artık yönetilen diskle gereklidir önce oluşturulan sağlama.</span><span class="sxs-lookup"><span data-stu-id="15f68-121">In the old template, this was ensuring that the storage accounts were created before the scale set began creation, but this clause is no longer necessary with managed disk.</span></span> <span data-ttu-id="15f68-122">Bu özellikler otomatik olarak başlık altında yönetilen disk tarafından işlenen olarak biz de vhd kapsayıcıları özelliği ve işletim sistemi disk adı özelliği kaldırın.</span><span class="sxs-lookup"><span data-stu-id="15f68-122">We also remove the vhd containers property, and the os disk name property as these properties are automatically handled under the hood by managed disk.</span></span> <span data-ttu-id="15f68-123">Biz onlardan varsa, eklediğimiz `"managedDisk": { "storageAccountType": "Premium_LRS" }` biz premium OS diskleri istediyseniz "osDisk" yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="15f68-123">If we wished, we could add `"managedDisk": { "storageAccountType": "Premium_LRS" }` in the "osDisk" configuration if we wanted premium OS disks.</span></span> <span data-ttu-id="15f68-124">Yalnızca bir büyük harf olan VM'ler veya küçük'ın ' VM'yi sku premium diskleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15f68-124">Only VMs with an uppercase or lowercase 's' in the VM sku can use premium disks.</span></span>

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

<span data-ttu-id="15f68-125">Yönetilen veya yönetilmeyen disk kullanıp kullanmayacağınızı için ölçek kümesi yapılandırmasında açık bir özellik yok.</span><span class="sxs-lookup"><span data-stu-id="15f68-125">There is no explicit property in the scale set configuration for whether to use managed or unmanaged disk.</span></span> <span data-ttu-id="15f68-126">Ölçek kümesini kullanmak için depolama profilinde mevcut özelliklerine göre bilir.</span><span class="sxs-lookup"><span data-stu-id="15f68-126">The scale set knows which to use based on the properties that are present in the storage profile.</span></span> <span data-ttu-id="15f68-127">Bu nedenle, Ölçek kümesi depolama profilinde hakkı özellikleri sağlamak için şablon değiştirirken önemlidir.</span><span class="sxs-lookup"><span data-stu-id="15f68-127">Thus, it is important when modifying the template to ensure that the right properties are in the storage profile of the scale set.</span></span>


## <a name="data-disks"></a><span data-ttu-id="15f68-128">Veri diskleri</span><span class="sxs-lookup"><span data-stu-id="15f68-128">Data disks</span></span>

<span data-ttu-id="15f68-129">Yukarıdaki değişikliklerle ölçek kümesi kullanan yönetilen diskler işletim sistemi için ancak, veri diskleri disk?</span><span class="sxs-lookup"><span data-stu-id="15f68-129">With the changes above, the scale set uses managed disks for the OS disk, but what about data disks?</span></span> <span data-ttu-id="15f68-130">Veri diskleri eklemek için "storageProfile" altında "dataDisks" özelliği "osDisk" ile aynı düzeyde ekleyin.</span><span class="sxs-lookup"><span data-stu-id="15f68-130">To add data disks, add the "dataDisks" property under "storageProfile" at the same level as "osDisk".</span></span> <span data-ttu-id="15f68-131">Her biri "(bir VM üzerinde veri disk başına benzersiz olması gerekir) LUN'un" özellikleri vardır, JSON nesnelerin bir listesini, özellik değeri "createOption" ("boş" şu anda yalnızca desteklenen seçenektir) ve "diskSizeGB" (gigabayt olarak; disk boyutu büyük olmalı 0 ile 1024'ten az) aşağıdaki örnekteki gibi:</span><span class="sxs-lookup"><span data-stu-id="15f68-131">The value of the property is a JSON list of objects, each of which has properties "lun" (which must be unique per data disk on a VM), "createOption" ("empty" is currently the only supported option), and "diskSizeGB" (the size of the disk in gigabytes; must be greater than 0 and less than 1024) as in the following example:</span></span> 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

<span data-ttu-id="15f68-132">Belirtirseniz `n` diskleri bu dizideki her VM ölçek kümesi alır `n` veri diski.</span><span class="sxs-lookup"><span data-stu-id="15f68-132">If you specify `n` disks in this array, each VM in the scale set gets `n` data disks.</span></span> <span data-ttu-id="15f68-133">Ancak, bu veri diskleri ham aygıtların olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="15f68-133">Do note, however, that these data disks are raw devices.</span></span> <span data-ttu-id="15f68-134">Bunlar biçimlendirilmemiş.</span><span class="sxs-lookup"><span data-stu-id="15f68-134">They are not formatted.</span></span> <span data-ttu-id="15f68-135">Bu, paritition, ekleme ve kullanmadan önce diskleri biçimlendirin müşteriye kadar olur.</span><span class="sxs-lookup"><span data-stu-id="15f68-135">It is up to the customer to attach, paritition, and format the disks before using them.</span></span> <span data-ttu-id="15f68-136">Biz de isteğe bağlı olarak, belirtebilirsiniz `"managedDisk": { "storageAccountType": "Premium_LRS" }` her veri diski nesnesinde bir premium veri diski gerektiğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="15f68-136">Optionally, we could also specify `"managedDisk": { "storageAccountType": "Premium_LRS" }` in each data disk object to specify that it should be a premium data disk.</span></span> <span data-ttu-id="15f68-137">Yalnızca bir büyük harf olan VM'ler veya küçük'ın ' VM'yi sku premium diskleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15f68-137">Only VMs with an uppercase or lowercase 's' in the VM sku can use premium disks.</span></span>

<span data-ttu-id="15f68-138">Veri diskleri ölçek kümeleri ile kullanma hakkında daha fazla bilgi için bkz: [bu makalede](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="15f68-138">To learn more about using data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="15f68-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="15f68-139">Next steps</span></span>
<span data-ttu-id="15f68-140">Örneğin Ölçek kümeleri kullanarak Resource Manager şablonları arama "vmss için" içinde [Azure hızlı başlangıç şablonlarını github deposuna](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="15f68-140">For example Resource Manager templates using scale sets, search for "vmss" in the [Azure Quickstart Templates github repo](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="15f68-141">Genel bilgi için kullanıma [ölçek kümeleri için ana giriş sayfasının](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="15f68-141">For general information, check out the [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>

