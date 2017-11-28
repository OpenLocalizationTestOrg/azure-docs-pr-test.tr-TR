---
title: "aaaUsing yönetilen Azure Resource Manager şablonları diskleri | Microsoft Docs"
description: "Azure Resource Manager şablonlarındaki misks toouse nasıl yönetileceğini ayrıntıları"
services: storage
documentationcenter: 
author: jboeshart
manager: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 06/01/2017
ms.author: jaboes
ms.openlocfilehash: ea83f4ed11acfd8f642dbc8331fa8cf077ef577c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-managed-disks-in-azure-resource-manager-templates"></a><span data-ttu-id="8c3f6-103">Azure Resource Manager şablonları diskleri kullanılarak yönetilir</span><span class="sxs-lookup"><span data-stu-id="8c3f6-103">Using Managed Disks in Azure Resource Manager Templates</span></span>

<span data-ttu-id="8c3f6-104">Bu belge, Azure Resource Manager şablonları tooprovision sanal makineleri kullanırken, yönetilen ve yönetilmeyen diskleri hello farklarını size yol göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-104">This document walks through hello differences between managed and unmanaged disks when using Azure Resource Manager templates tooprovision virtual machines.</span></span> <span data-ttu-id="8c3f6-105">Bu, yönetilmeyen diskleri toomanaged diskler kullanarak var olan şablonları tooupdate yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-105">This will help you tooupdate existing templates that are using unmanaged Disks toomanaged disks.</span></span> <span data-ttu-id="8c3f6-106">Başvuru için hello kullanıyoruz [101 vm basit windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) şablon bir kılavuz olarak.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-106">For reference, we are using hello [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) template as a guide.</span></span> <span data-ttu-id="8c3f6-107">Her ikisini de kullanarak hello şablonunu görebilirsiniz [yönetilen disklerde](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) ve kullanarak bir önceki sürüm [yönetilmeyen diskleri](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) isterseniz toodirectly bunları karşılaştırın.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-107">You can see hello template using both [managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) and a prior version using [unmanaged disks](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) if you'd like toodirectly compare them.</span></span>

## <a name="unmanaged-disks-template-formatting"></a><span data-ttu-id="8c3f6-108">Yönetilmeyen diskleri şablonu biçimlendirmesi</span><span class="sxs-lookup"><span data-stu-id="8c3f6-108">Unmanaged Disks template formatting</span></span>

<span data-ttu-id="8c3f6-109">toobegin, biz ele göz nasıl yönetilmeyen disklere dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-109">toobegin, we take a look at how unmanaged disks are deployed.</span></span> <span data-ttu-id="8c3f6-110">Yönetilmeyen diskleri oluştururken, bir depolama hesabı toohold hello VHD dosyaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-110">When creating unmanaged disks, you need a storage account toohold hello VHD files.</span></span> <span data-ttu-id="8c3f6-111">Yeni bir depolama hesabı oluşturun veya zaten varolan bir kullanın.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-111">You can create a new storage account or use one that already exists.</span></span> <span data-ttu-id="8c3f6-112">Bu makale size nasıl gösterir toocreate yeni bir depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-112">This article will show you how toocreate a new storage account.</span></span> <span data-ttu-id="8c3f6-113">tooaccomplish Bu, aşağıda gösterildiği gibi bir depolama hesabı kaynak hello kaynakları bloğundaki gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-113">tooaccomplish this, you need a storage account resource in hello resources block as shown below.</span></span>

```
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2016-01-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {}
}
```

<span data-ttu-id="8c3f6-114">Hello sanal makine nesnesi içinde bir bağımlılığı hello sanal makine önce oluşturduğu hello depolama hesabı tooensure gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-114">Within hello virtual machine object, we need a dependency on hello storage account tooensure that it's created before hello virtual machine.</span></span> <span data-ttu-id="8c3f6-115">Merhaba içinde `storageProfile` bölümünde, ardından belirttiğimiz hello hello depolama hesabına başvuruyor ve hello işletim sistemi diski ve veri diskleri için gerekli VHD konumu tam URI'sini hello.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-115">Within hello `storageProfile` section, we then specify hello full URI of hello VHD location, which references hello storage account and is needed for hello OS disk and any data disks.</span></span> 

```
{
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "name": "osdisk",
                "vhd": {
                    "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/osdisk.vhd')]"
                },
                "caching": "ReadWrite",
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "name": "datadisk1",
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "vhd": {
                        "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/datadisk1.vhd')]"
                    },
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

## <a name="managed-disks-template-formatting"></a><span data-ttu-id="8c3f6-116">Şablon diskleri biçimlendirme yönetilen</span><span class="sxs-lookup"><span data-stu-id="8c3f6-116">Managed disks template formatting</span></span>

<span data-ttu-id="8c3f6-117">Azure yönetilen disklerle hello disk en üst düzey bir kaynağı haline gelir ve artık hello kullanıcı tarafından oluşturulan bir depolama hesabı toobe gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-117">With Azure Managed Disks, hello disk becomes a top-level resource and no longer requires a storage account toobe created by hello user.</span></span> <span data-ttu-id="8c3f6-118">Yönetilen diskleri hello önce açık `2016-04-30-preview` API sürümü, bunlar tüm sonraki API sürümlerinde kullanılabilir ve hello varsayılan disk türü sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-118">Managed disks were first exposed in hello `2016-04-30-preview` API version, they are available in all subsequent API versions and are now hello default disk type.</span></span> <span data-ttu-id="8c3f6-119">Merhaba aşağıdaki bölümlerde hello varsayılan ayarları'nda yol ve nasıl toofurther özelleştirme disklerinizi ayrıntı.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-119">hello following sections walk through hello default settings and detail how toofurther customize your disks.</span></span>

> [!NOTE]
> <span data-ttu-id="8c3f6-120">Toouse bir API sürümü önerilir daha sonraki `2016-04-30-preview` arasında önemli değişiklikler olduğu `2016-04-30-preview` ve `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-120">It is recommended toouse an API version later than `2016-04-30-preview` as there were breaking changes between `2016-04-30-preview` and `2017-03-30`.</span></span>
>
>

### <a name="default-managed-disk-settings"></a><span data-ttu-id="8c3f6-121">Varsayılan yönetilen disk ayarları</span><span class="sxs-lookup"><span data-stu-id="8c3f6-121">Default managed disk settings</span></span>

<span data-ttu-id="8c3f6-122">toocreate artık yönetilen diskleri olan bir VM toocreate hello depolama hesabı kaynağı gerekir ve sanal makine kaynağı gibi güncelleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-122">toocreate a VM with managed disks, you no longer need toocreate hello storage account resource and can update your virtual machine resource as follows.</span></span> <span data-ttu-id="8c3f6-123">Özellikle bu hello Not `apiVersion` yansıtır `2017-03-30` ve hello `osDisk` ve `dataDisks` artık tooa başvurmak hello VHD için özel URI.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-123">Specifically note that hello `apiVersion` reflects `2017-03-30` and hello `osDisk` and `dataDisks` no longer refer tooa specific URI for hello VHD.</span></span> <span data-ttu-id="8c3f6-124">Ek özellikleri belirtmeden dağıtırken hello disk kullanacağı [standart LRS depolama](storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="8c3f6-124">When deploying without specifying additional properties, hello disk will use [Standard LRS storage](storage-redundancy.md).</span></span> <span data-ttu-id="8c3f6-125">Ad belirtilmezse, hello biçimini alır `<VMName>_OsDisk_1_<randomstring>` hello işletim sistemi diski ve `<VMName>_disk<#>_<randomstring>` her veri diski için.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-125">If no name is specified, it takes hello format of `<VMName>_OsDisk_1_<randomstring>` for hello OS disk and `<VMName>_disk<#>_<randomstring>` for each data disk.</span></span> <span data-ttu-id="8c3f6-126">Varsayılan olarak, Azure disk şifrelemesi; devre dışı önbelleğe alma okuma/yazma hello işletim sistemi diski ve veri diskleri için hiçbiri içindir.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-126">By default, Azure disk encryption is disabled; caching is Read/Write for hello OS disk and None for data disks.</span></span> <span data-ttu-id="8c3f6-127">Merhaba aşağıdaki örnekte hala bir depolama hesabı bağımlılık, bu yalnızca tanılama için depolama ve disk depolaması için gerekli değildir ancak fark.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-127">You may notice in hello example below there is still a storage account dependency, though this is only for storage of diagnostics and is not needed for disk storage.</span></span>

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="using-a-top-level-managed-disk-resource"></a><span data-ttu-id="8c3f6-128">Bir üst düzey yönetilen disk kaynağı kullanarak</span><span class="sxs-lookup"><span data-stu-id="8c3f6-128">Using a top-level managed disk resource</span></span>

<span data-ttu-id="8c3f6-129">Bir alternatif toospecifying hello nesnesindeki disk yapılandırmasını hello sanal makine, bir üst düzey disk kaynağı oluşturun ve hello sanal makine oluşturmanın bir parçası olarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-129">As an alternative toospecifying hello disk configuration in hello virtual machine object, you can create a top-level disk resource and attach it as part of hello virtual machine creation.</span></span> <span data-ttu-id="8c3f6-130">Örneğin, bir veri diski olarak toouse aşağıdaki gibi bir disk kaynağı oluşturabiliriz.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-130">For example, we can create a disk resource as follows toouse as a data disk.</span></span>

```
{
    "type": "Microsoft.Compute/disks",
    "name": "[concat(variables('vmName'),'-datadisk1')]",
    "apiVersion": "2017-03-30",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "properties": {
        "creationData": {
            "createOption": "Empty"
        },
        "diskSizeGB": 1023
    }
}
```

<span data-ttu-id="8c3f6-131">Merhaba VM nesnesi içinde biz bağlı bu disk nesne toobe sonra başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-131">Within hello VM object, we can then reference this disk object toobe attached.</span></span> <span data-ttu-id="8c3f6-132">Merhaba Hello kaynak Kimliğini belirtme yönetilen hello oluşturduğumuz disk `managedDisk` özelliği hello disk hello ek VM oluşturulduğunda hello olarak verir.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-132">Specifying hello resource ID of hello managed disk we created in hello `managedDisk` property allows hello attachment of hello disk as hello VM is created.</span></span> <span data-ttu-id="8c3f6-133">Bu hello Not `apiVersion` hello VM kaynak çok ayarlamak için`2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-133">Note that hello `apiVersion` for hello VM resource is set too`2017-03-30`.</span></span> <span data-ttu-id="8c3f6-134">Ayrıca, bir bağımlılık başarıyla VM oluşturması işleminden önce oluşturulan hello disk kaynak tooensure üzerinde oluşturduk olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-134">Also note that we've created a dependency on hello disk resource tooensure it's successfully created before VM creation.</span></span> 

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]",
        "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "lun": 0,
                    "name": "[concat(variables('vmName'),'-datadisk1')]",
                    "createOption": "attach",
                    "managedDisk": {
                        "id": "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
                    }
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a><span data-ttu-id="8c3f6-135">Yönetilen diskleri kullanarak VM'ler ile yönetilen kullanılabilirlik kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="8c3f6-135">Create managed availability sets with VMs using managed disks</span></span>

<span data-ttu-id="8c3f6-136">toocreate yönetilen kullanılabilirlik kümesi yönetilen diskleri kullanarak VMs Ekle hello `sku` nesne toohello kullanılabilirlik kaynak ve ayarlanmış hello `name` özelliği çok`Aligned`.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-136">toocreate managed availability sets with VMs using managed disks, add hello `sku` object toohello availability set resource and set hello `name` property too`Aligned`.</span></span> <span data-ttu-id="8c3f6-137">Bu, her VM için hello diskleri birbiriyle tooavoid tek hata noktaları yeterince yalıtılmış olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-137">This ensures that hello disks for each VM are sufficiently isolated from each other tooavoid single points of failure.</span></span> <span data-ttu-id="8c3f6-138">Ayrıca bu hello unutmayın `apiVersion` kaynak hello kullanılabilirlik kümesi için çok ayarlanır`2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-138">Also note that hello `apiVersion` for hello availability set resource is set too`2017-03-30`.</span></span>

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/availabilitySets",
    "location": "[resourceGroup().location]",
    "name": "[variables('avSetName')]",
    "properties": {
        "PlatformUpdateDomainCount": 3,
        "PlatformFaultDomainCount": 2
    },
    "sku": {
        "name": "Aligned"
    }
}
```

### <a name="additional-scenarios-and-customizations"></a><span data-ttu-id="8c3f6-139">İlave Senaryolar ve özelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="8c3f6-139">Additional scenarios and customizations</span></span>

<span data-ttu-id="8c3f6-140">Merhaba REST API belirtimlerini hakkında tam bilgi toofind Lütfen hello gözden [yönetilen bir disk REST API belgeleri oluşturmak](/rest/api/manageddisks/disks/disks-create-or-update).</span><span class="sxs-lookup"><span data-stu-id="8c3f6-140">toofind full information on hello REST API specifications, please review hello [create a managed disk REST API documentation](/rest/api/manageddisks/disks/disks-create-or-update).</span></span> <span data-ttu-id="8c3f6-141">İlave Senaryolar yanı sıra varsayılan ve şablon dağıtımlarına üzerinden gönderilen toohello API olabilir kabul edilebilir değerler bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-141">You will find additional scenarios, as well as default and acceptable values that can be submitted toohello API through template deployments.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8c3f6-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8c3f6-142">Next steps</span></span>

* <span data-ttu-id="8c3f6-143">Yönetilen diskler kullanan tam şablonları hello Azure hızlı başlangıç depodaki bağlantılar aşağıdaki adresi ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-143">For full templates that use managed disks visit hello following Azure Quickstart Repo links.</span></span>
    * [<span data-ttu-id="8c3f6-144">Windows VM yönetilen diski</span><span class="sxs-lookup"><span data-stu-id="8c3f6-144">Windows VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [<span data-ttu-id="8c3f6-145">Linux VM yönetilen diski</span><span class="sxs-lookup"><span data-stu-id="8c3f6-145">Linux VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [<span data-ttu-id="8c3f6-146">Yönetilen disk şablonları tam listesi</span><span class="sxs-lookup"><span data-stu-id="8c3f6-146">Full list of managed disk templates</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="8c3f6-147">Merhaba ziyaret [Azure yönetilen diskleri genel bakış](storage-managed-disks-overview.md) hakkında daha fazla bilgi belge toolearn yönetilen diskler.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-147">Visit hello [Azure Managed Disks Overview](storage-managed-disks-overview.md) document toolearn more about managed disks.</span></span>
* <span data-ttu-id="8c3f6-148">Sanal Makine kaynakları hello şablon başvuru belgelerine hello ziyaret ederek gözden geçirin [Microsoft.Compute/virtualMachines şablon başvurusu](/templates/microsoft.compute/virtualmachines) belge.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-148">Review hello template reference documentation for virtual machine resources by visiting hello [Microsoft.Compute/virtualMachines template reference](/templates/microsoft.compute/virtualmachines) document.</span></span>
* <span data-ttu-id="8c3f6-149">Merhaba ziyaret ederek hello şablon başvuru belgeleri disk kaynakları için gözden [Microsoft.Compute/disks şablon başvurusu](/templates/microsoft.compute/disks) belge.</span><span class="sxs-lookup"><span data-stu-id="8c3f6-149">Review hello template reference documentation for disk resources by visiting hello [Microsoft.Compute/disks template reference](/templates/microsoft.compute/disks) document.</span></span>
 
