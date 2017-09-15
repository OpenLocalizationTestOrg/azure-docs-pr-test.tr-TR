# <a name="using-managed-disks-in-azure-resource-manager-templates"></a><span data-ttu-id="df892-101">Azure Resource Manager şablonları diskleri kullanılarak yönetilir</span><span class="sxs-lookup"><span data-stu-id="df892-101">Using Managed Disks in Azure Resource Manager Templates</span></span>

<span data-ttu-id="df892-102">Bu belge sanal makineler sağlamak için Azure Resource Manager şablonları kullanarak yönetilen ve yönetilmeyen diskler arasındaki farklar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="df892-102">This document walks through the differences between managed and unmanaged disks when using Azure Resource Manager templates to provision virtual machines.</span></span> <span data-ttu-id="df892-103">Bu, yönetilmeyen diskleri yönetilen disklere kullanarak var olan şablonları güncelleştirme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="df892-103">This will help you to update existing templates that are using unmanaged Disks to managed disks.</span></span> <span data-ttu-id="df892-104">Başvuru için kullanıyoruz [101 vm basit windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) şablon bir kılavuz olarak.</span><span class="sxs-lookup"><span data-stu-id="df892-104">For reference, we are using the [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) template as a guide.</span></span> <span data-ttu-id="df892-105">Her ikisini de kullanarak şablonu görebilirsiniz [yönetilen disklerde](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) ve kullanarak bir önceki sürüm [yönetilmeyen diskleri](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) doğrudan karşılaştırmak istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="df892-105">You can see the template using both [managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) and a prior version using [unmanaged disks](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) if you'd like to directly compare them.</span></span>

## <a name="unmanaged-disks-template-formatting"></a><span data-ttu-id="df892-106">Yönetilmeyen diskleri şablonu biçimlendirmesi</span><span class="sxs-lookup"><span data-stu-id="df892-106">Unmanaged Disks template formatting</span></span>

<span data-ttu-id="df892-107">Başlamak için biz göz nasıl yönetilmeyen disklere dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="df892-107">To begin, we take a look at how unmanaged disks are deployed.</span></span> <span data-ttu-id="df892-108">Yönetilmeyen diskleri oluştururken, VHD dosyalarını tutmak için bir depolama hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="df892-108">When creating unmanaged disks, you need a storage account to hold the VHD files.</span></span> <span data-ttu-id="df892-109">Yeni bir depolama hesabı oluşturun veya zaten varolan bir kullanın.</span><span class="sxs-lookup"><span data-stu-id="df892-109">You can create a new storage account or use one that already exists.</span></span> <span data-ttu-id="df892-110">Bu makale yeni bir depolama hesabının nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="df892-110">This article will show you how to create a new storage account.</span></span> <span data-ttu-id="df892-111">Bunu başarmak için aşağıda gösterildiği gibi kaynakları blok depolama hesabı kaynak gerekir.</span><span class="sxs-lookup"><span data-stu-id="df892-111">To accomplish this, you need a storage account resource in the resources block as shown below.</span></span>

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

<span data-ttu-id="df892-112">Sanal makine nesnesi içinde bir bağımlılığı önce sanal makine oluşturulduğundan emin olmak için depolama hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="df892-112">Within the virtual machine object, we need a dependency on the storage account to ensure that it's created before the virtual machine.</span></span> <span data-ttu-id="df892-113">İçinde `storageProfile` bölümünde, ardından belirttiğimiz depolama hesabına başvuruyor ve işletim sistemi diski ve veri diskleri için gerekli VHD konumunun tam URI.</span><span class="sxs-lookup"><span data-stu-id="df892-113">Within the `storageProfile` section, we then specify the full URI of the VHD location, which references the storage account and is needed for the OS disk and any data disks.</span></span> 

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

## <a name="managed-disks-template-formatting"></a><span data-ttu-id="df892-114">Şablon diskleri biçimlendirme yönetilen</span><span class="sxs-lookup"><span data-stu-id="df892-114">Managed disks template formatting</span></span>

<span data-ttu-id="df892-115">Azure yönetilen disklerle diski bir üst düzey kaynak haline gelir ve artık kullanıcı tarafından oluşturulacak bir depolama hesabı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="df892-115">With Azure Managed Disks, the disk becomes a top-level resource and no longer requires a storage account to be created by the user.</span></span> <span data-ttu-id="df892-116">Yönetilen diskleri ilk ortaya çıkarılan `2016-04-30-preview` API sürümü, bunlar tüm sonraki API sürümlerinde kullanılabilir ve varsayılan disk türü sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="df892-116">Managed disks were first exposed in the `2016-04-30-preview` API version, they are available in all subsequent API versions and are now the default disk type.</span></span> <span data-ttu-id="df892-117">Aşağıdaki bölümlerde, varsayılan ayarları'nda yol ve disklerinizi daha fazla özelleştirmek nasıl ayrıntı.</span><span class="sxs-lookup"><span data-stu-id="df892-117">The following sections walk through the default settings and detail how to further customize your disks.</span></span>

> [!NOTE]
> <span data-ttu-id="df892-118">Bir API sürümü kullanmak için önerilen daha `2016-04-30-preview` arasında önemli değişiklikler olduğu `2016-04-30-preview` ve `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="df892-118">It is recommended to use an API version later than `2016-04-30-preview` as there were breaking changes between `2016-04-30-preview` and `2017-03-30`.</span></span>
>
>

### <a name="default-managed-disk-settings"></a><span data-ttu-id="df892-119">Varsayılan yönetilen disk ayarları</span><span class="sxs-lookup"><span data-stu-id="df892-119">Default managed disk settings</span></span>

<span data-ttu-id="df892-120">Yönetilen disklerle bir VM oluşturmak için artık depolama oluşturmanıza gerek hesap kaynak ve sanal makine kaynağınızın şu şekilde güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="df892-120">To create a VM with managed disks, you no longer need to create the storage account resource and can update your virtual machine resource as follows.</span></span> <span data-ttu-id="df892-121">Özellikle dikkat edin `apiVersion` yansıtır `2017-03-30` ve `osDisk` ve `dataDisks` artık VHD için belirli bir URI bakın.</span><span class="sxs-lookup"><span data-stu-id="df892-121">Specifically note that the `apiVersion` reflects `2017-03-30` and the `osDisk` and `dataDisks` no longer refer to a specific URI for the VHD.</span></span> <span data-ttu-id="df892-122">Ek özellikleri belirtmeden dağıtırken diski kullanacak [standart LRS depolama](../articles/storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="df892-122">When deploying without specifying additional properties, the disk will use [Standard LRS storage](../articles/storage/common/storage-redundancy.md).</span></span> <span data-ttu-id="df892-123">Ad belirtilmezse, biçimini alır `<VMName>_OsDisk_1_<randomstring>` işletim sistemi diski için ve `<VMName>_disk<#>_<randomstring>` her veri diski için.</span><span class="sxs-lookup"><span data-stu-id="df892-123">If no name is specified, it takes the format of `<VMName>_OsDisk_1_<randomstring>` for the OS disk and `<VMName>_disk<#>_<randomstring>` for each data disk.</span></span> <span data-ttu-id="df892-124">Varsayılan olarak, Azure disk şifrelemesi; devre dışı önbelleğe alma okuma/yazma işletim sistemi diski ve veri diskleri için hiçbiri içindir.</span><span class="sxs-lookup"><span data-stu-id="df892-124">By default, Azure disk encryption is disabled; caching is Read/Write for the OS disk and None for data disks.</span></span> <span data-ttu-id="df892-125">Aşağıdaki örnekte hala bir depolama hesabı bağımlılık, bu yalnızca tanılama için depolama ve disk depolaması için gerekli değildir ancak fark.</span><span class="sxs-lookup"><span data-stu-id="df892-125">You may notice in the example below there is still a storage account dependency, though this is only for storage of diagnostics and is not needed for disk storage.</span></span>

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

### <a name="using-a-top-level-managed-disk-resource"></a><span data-ttu-id="df892-126">Bir üst düzey yönetilen disk kaynağı kullanarak</span><span class="sxs-lookup"><span data-stu-id="df892-126">Using a top-level managed disk resource</span></span>

<span data-ttu-id="df892-127">Disk yapılandırması sanal makine nesnesinde belirterek alternatif olarak, bir üst düzey disk kaynağı oluşturun ve sanal makine oluşturmanın bir parçası olarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="df892-127">As an alternative to specifying the disk configuration in the virtual machine object, you can create a top-level disk resource and attach it as part of the virtual machine creation.</span></span> <span data-ttu-id="df892-128">Örneğin, aşağıdaki gibi bir veri diski kullanmak için bir disk kaynağı oluşturabiliriz.</span><span class="sxs-lookup"><span data-stu-id="df892-128">For example, we can create a disk resource as follows to use as a data disk.</span></span>

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

<span data-ttu-id="df892-129">VM nesnesi içinde Biz bu disk nesne eklenmiş sonra başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="df892-129">Within the VM object, we can then reference this disk object to be attached.</span></span> <span data-ttu-id="df892-130">Oluşturduğumuz, yönetilen disk kaynak Kimliğini belirtme `managedDisk` özelliği VM oluşturulduğunda ek diskin izin verir.</span><span class="sxs-lookup"><span data-stu-id="df892-130">Specifying the resource ID of the managed disk we created in the `managedDisk` property allows the attachment of the disk as the VM is created.</span></span> <span data-ttu-id="df892-131">Unutmayın `apiVersion` VM için kaynak ayarlamak `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="df892-131">Note that the `apiVersion` for the VM resource is set to `2017-03-30`.</span></span> <span data-ttu-id="df892-132">Ayrıca, bir bağımlılık başarıyla VM oluşturması işleminden önce oluşturulan emin olmak için disk kaynağına oluşturduk olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="df892-132">Also note that we've created a dependency on the disk resource to ensure it's successfully created before VM creation.</span></span> 

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

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a><span data-ttu-id="df892-133">Yönetilen diskleri kullanarak VM'ler ile yönetilen kullanılabilirlik kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="df892-133">Create managed availability sets with VMs using managed disks</span></span>

<span data-ttu-id="df892-134">Yönetilen oluşturmak için kullanılabilirlik VM'ler ile yönetilen diskleri kullanarak ayarlar, ekleme `sku` kaynak ve ayarlanmış kullanılabilirlik nesnesine `name` özelliğine `Aligned`.</span><span class="sxs-lookup"><span data-stu-id="df892-134">To create managed availability sets with VMs using managed disks, add the `sku` object to the availability set resource and set the `name` property to `Aligned`.</span></span> <span data-ttu-id="df892-135">Bu, diskler her VM için yeterince yalıtılmış tek hata noktaları bulundurmaktan önlemek için birbirinden olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="df892-135">This ensures that the disks for each VM are sufficiently isolated from each other to avoid single points of failure.</span></span> <span data-ttu-id="df892-136">Ayrıca `apiVersion` kaynak kullanılabilirlik kümesi için ayarlamak `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="df892-136">Also note that the `apiVersion` for the availability set resource is set to `2017-03-30`.</span></span>

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

### <a name="additional-scenarios-and-customizations"></a><span data-ttu-id="df892-137">İlave Senaryolar ve özelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="df892-137">Additional scenarios and customizations</span></span>

<span data-ttu-id="df892-138">REST API belirtimlerini hakkında tam bilgi bulmak için lütfen inceleyin [yönetilen bir disk REST API belgeleri oluşturmak](/rest/api/manageddisks/disks/disks-create-or-update).</span><span class="sxs-lookup"><span data-stu-id="df892-138">To find full information on the REST API specifications, please review the [create a managed disk REST API documentation](/rest/api/manageddisks/disks/disks-create-or-update).</span></span> <span data-ttu-id="df892-139">Varsayılan ve API şablon dağıtımlarına aracılığıyla gönderilebilir kabul edilebilir değerler yanı sıra ek senaryolar bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="df892-139">You will find additional scenarios, as well as default and acceptable values that can be submitted to the API through template deployments.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="df892-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="df892-140">Next steps</span></span>

* <span data-ttu-id="df892-141">Yönetilen diskleri kullanmak için tam şablonları aşağıdaki Azure hızlı başlangıç depodaki bağlantıları ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="df892-141">For full templates that use managed disks visit the following Azure Quickstart Repo links.</span></span>
    * [<span data-ttu-id="df892-142">Windows VM yönetilen diski</span><span class="sxs-lookup"><span data-stu-id="df892-142">Windows VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [<span data-ttu-id="df892-143">Linux VM yönetilen diski</span><span class="sxs-lookup"><span data-stu-id="df892-143">Linux VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [<span data-ttu-id="df892-144">Yönetilen disk şablonları tam listesi</span><span class="sxs-lookup"><span data-stu-id="df892-144">Full list of managed disk templates</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="df892-145">Ziyaret [Azure yönetilen diskleri genel bakış](../articles/virtual-machines/windows/managed-disks-overview.md) belge yönetilen diskler hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="df892-145">Visit the [Azure Managed Disks Overview](../articles/virtual-machines/windows/managed-disks-overview.md) document to learn more about managed disks.</span></span>
* <span data-ttu-id="df892-146">Sanal Makine kaynakları için şablon başvuru belgeleri ziyaret ederek gözden [Microsoft.Compute/virtualMachines şablon başvurusu](/templates/microsoft.compute/virtualmachines) belge.</span><span class="sxs-lookup"><span data-stu-id="df892-146">Review the template reference documentation for virtual machine resources by visiting the [Microsoft.Compute/virtualMachines template reference](/templates/microsoft.compute/virtualmachines) document.</span></span>
* <span data-ttu-id="df892-147">Disk kaynakları için şablon başvuru belgeleri ziyaret ederek gözden [Microsoft.Compute/disks şablon başvurusu](/templates/microsoft.compute/disks) belge.</span><span class="sxs-lookup"><span data-stu-id="df892-147">Review the template reference documentation for disk resources by visiting the [Microsoft.Compute/disks template reference](/templates/microsoft.compute/disks) document.</span></span>
 
