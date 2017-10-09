# <a name="using-managed-disks-in-azure-resource-manager-templates"></a>Azure Resource Manager şablonları diskleri kullanılarak yönetilir

Bu belge, Azure Resource Manager şablonları tooprovision sanal makineleri kullanırken, yönetilen ve yönetilmeyen diskleri hello farklarını size yol göstermektedir. Bu, yönetilmeyen diskleri toomanaged diskler kullanarak var olan şablonları tooupdate yardımcı olur. Başvuru için hello kullanıyoruz [101 vm basit windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) şablon bir kılavuz olarak. Her ikisini de kullanarak hello şablonunu görebilirsiniz [yönetilen disklerde](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) ve kullanarak bir önceki sürüm [yönetilmeyen diskleri](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) isterseniz toodirectly bunları karşılaştırın.

## <a name="unmanaged-disks-template-formatting"></a>Yönetilmeyen diskleri şablonu biçimlendirmesi

toobegin, biz ele göz nasıl yönetilmeyen disklere dağıtılır. Yönetilmeyen diskleri oluştururken, bir depolama hesabı toohold hello VHD dosyaları gerekir. Yeni bir depolama hesabı oluşturun veya zaten varolan bir kullanın. Bu makale size nasıl gösterir toocreate yeni bir depolama hesabı. tooaccomplish Bu, aşağıda gösterildiği gibi bir depolama hesabı kaynak hello kaynakları bloğundaki gerekir.

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

Hello sanal makine nesnesi içinde bir bağımlılığı hello sanal makine önce oluşturduğu hello depolama hesabı tooensure gerekir. Merhaba içinde `storageProfile` bölümünde, ardından belirttiğimiz hello hello depolama hesabına başvuruyor ve hello işletim sistemi diski ve veri diskleri için gerekli VHD konumu tam URI'sini hello. 

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

## <a name="managed-disks-template-formatting"></a>Şablon diskleri biçimlendirme yönetilen

Azure yönetilen disklerle hello disk en üst düzey bir kaynağı haline gelir ve artık hello kullanıcı tarafından oluşturulan bir depolama hesabı toobe gerektirir. Yönetilen diskleri hello önce açık `2016-04-30-preview` API sürümü, bunlar tüm sonraki API sürümlerinde kullanılabilir ve hello varsayılan disk türü sunulmuştur. Merhaba aşağıdaki bölümlerde hello varsayılan ayarları'nda yol ve nasıl toofurther özelleştirme disklerinizi ayrıntı.

> [!NOTE]
> Toouse bir API sürümü önerilir daha sonraki `2016-04-30-preview` arasında önemli değişiklikler olduğu `2016-04-30-preview` ve `2017-03-30`.
>
>

### <a name="default-managed-disk-settings"></a>Varsayılan yönetilen disk ayarları

toocreate artık yönetilen diskleri olan bir VM toocreate hello depolama hesabı kaynağı gerekir ve sanal makine kaynağı gibi güncelleştirebilir. Özellikle bu hello Not `apiVersion` yansıtır `2017-03-30` ve hello `osDisk` ve `dataDisks` artık tooa başvurmak hello VHD için özel URI. Ek özellikleri belirtmeden dağıtırken hello disk kullanacağı [standart LRS depolama](../articles/storage/common/storage-redundancy.md). Ad belirtilmezse, hello biçimini alır `<VMName>_OsDisk_1_<randomstring>` hello işletim sistemi diski ve `<VMName>_disk<#>_<randomstring>` her veri diski için. Varsayılan olarak, Azure disk şifrelemesi; devre dışı önbelleğe alma okuma/yazma hello işletim sistemi diski ve veri diskleri için hiçbiri içindir. Merhaba aşağıdaki örnekte hala bir depolama hesabı bağımlılık, bu yalnızca tanılama için depolama ve disk depolaması için gerekli değildir ancak fark.

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

### <a name="using-a-top-level-managed-disk-resource"></a>Bir üst düzey yönetilen disk kaynağı kullanarak

Bir alternatif toospecifying hello nesnesindeki disk yapılandırmasını hello sanal makine, bir üst düzey disk kaynağı oluşturun ve hello sanal makine oluşturmanın bir parçası olarak ekleyin. Örneğin, bir veri diski olarak toouse aşağıdaki gibi bir disk kaynağı oluşturabiliriz.

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

Merhaba VM nesnesi içinde biz bağlı bu disk nesne toobe sonra başvurabilirsiniz. Merhaba Hello kaynak Kimliğini belirtme yönetilen hello oluşturduğumuz disk `managedDisk` özelliği hello disk hello ek VM oluşturulduğunda hello olarak verir. Bu hello Not `apiVersion` hello VM kaynak çok ayarlamak için`2017-03-30`. Ayrıca, bir bağımlılık başarıyla VM oluşturması işleminden önce oluşturulan hello disk kaynak tooensure üzerinde oluşturduk olduğunu unutmayın. 

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

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a>Yönetilen diskleri kullanarak VM'ler ile yönetilen kullanılabilirlik kümeleri oluşturma

toocreate yönetilen kullanılabilirlik kümesi yönetilen diskleri kullanarak VMs Ekle hello `sku` nesne toohello kullanılabilirlik kaynak ve ayarlanmış hello `name` özelliği çok`Aligned`. Bu, her VM için hello diskleri birbiriyle tooavoid tek hata noktaları yeterince yalıtılmış olmasını sağlar. Ayrıca bu hello unutmayın `apiVersion` kaynak hello kullanılabilirlik kümesi için çok ayarlanır`2017-03-30`.

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

### <a name="additional-scenarios-and-customizations"></a>İlave Senaryolar ve özelleştirmeleri

Merhaba REST API belirtimlerini hakkında tam bilgi toofind Lütfen hello gözden [yönetilen bir disk REST API belgeleri oluşturmak](/rest/api/manageddisks/disks/disks-create-or-update). İlave Senaryolar yanı sıra varsayılan ve şablon dağıtımlarına üzerinden gönderilen toohello API olabilir kabul edilebilir değerler bulacaksınız. 

## <a name="next-steps"></a>Sonraki adımlar

* Yönetilen diskler kullanan tam şablonları hello Azure hızlı başlangıç depodaki bağlantılar aşağıdaki adresi ziyaret edin.
    * [Windows VM yönetilen diski](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [Linux VM yönetilen diski](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [Yönetilen disk şablonları tam listesi](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* Merhaba ziyaret [Azure yönetilen diskleri genel bakış](../articles/virtual-machines/windows/managed-disks-overview.md) hakkında daha fazla bilgi belge toolearn yönetilen diskler.
* Sanal Makine kaynakları hello şablon başvuru belgelerine hello ziyaret ederek gözden geçirin [Microsoft.Compute/virtualMachines şablon başvurusu](/templates/microsoft.compute/virtualmachines) belge.
* Merhaba ziyaret ederek hello şablon başvuru belgeleri disk kaynakları için gözden [Microsoft.Compute/disks şablon başvurusu](/templates/microsoft.compute/disks) belge.
 
