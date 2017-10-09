---
title: "aaaCreate azure'da bir şablondan bir Windows VM | Microsoft Docs"
description: "Resource Manager şablonu kullanın ve PowerShell tooeasily yeni bir Windows VM oluşturun."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 19129d61-8c04-4aa9-a01f-361a09466805
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: davidmu
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 630111482c7dc046091632e2ed458ac143325d59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a>Bir Windows sanal makine bir Resource Manager şablonu oluşturma

Bu makale size nasıl gösterir toodeploy bir Azure Resource Manager PowerShell kullanarak şablonu. oluşturduğunuz hello şablon tek bir alt ağ ile yeni bir sanal ağ içinde Windows Server çalıştıran tek bir sanal makine dağıtır.

Merhaba sanal makine kaynağı ayrıntılı bir açıklaması için bkz: [sanal makineleri bir Azure Resource Manager şablonunda](template-description.md). Bir şablona tüm hello kaynaklar hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonu Kılavuzu](../../azure-resource-manager/resource-manager-template-walkthrough.md).

Toodo hello bu makaledeki adımları yaklaşık beş dakika sürer.

## <a name="install-azure-powershell"></a>Azure PowerShell'i yükleme

Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](../../powershell-install-configure.md) hello Azure PowerShell'in en son sürümünü yükleme, aboneliğinizi seçme ve tooyour hesabında imzalama hakkında bilgi.

## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Tüm kaynaklar dağıtılmalıdır bir [kaynak grubu](../../azure-resource-manager/resource-group-overview.md).

1. Kaynakların oluşturulabileceği kullanılabilir konumların bir listesini alın.
   
    ```powershell   
    Get-AzureRmLocation | sort DisplayName | Select DisplayName
    ```

2. Merhaba kaynak grubu seçtiğiniz hello konumda oluşturun. Bu örnek, bir kaynak grubu hello oluşturulmasını gösterir **myResourceGroup** hello içinde **Batı ABD** konumu:

    ```powershell   
    New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
    ```

## <a name="create-hello-files"></a>Merhaba dosyaları oluşturma

Bu adımda, hello kaynakları dağıtan bir şablonu ve parametre değerlerini toohello şablon sağlayan bir parametre dosyası oluşturun. Kullanılan tooperform Azure Resource Manager operations bir yetkilendirme dosya oluşturabilir.

1. Adlı bir dosya oluşturun *CreateVMTemplate.json* ve bu JSON kodunu tooit ekleyin:

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUsername": { "type": "string" },
        "adminPassword": { "type": "securestring" }
      },
      "variables": {
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks','myVNet')]", 
        "subnetRef": "[concat(variables('vnetID'),'/subnets/mySubnet')]", 
      },
      "resources": [
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "myPublicIPAddress",
          "location": "[resourceGroup().location]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic",
            "dnsSettings": {
              "domainNameLabel": "myresourcegroupdns1"
            }
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "myVNet",
          "location": "[resourceGroup().location]",
          "properties": {
            "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
            "subnets": [
              {
                "name": "mySubnet",
                "properties": { "addressPrefix": "10.0.0.0/24" }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/networkInterfaces",
          "name": "myNic",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/publicIPAddresses/', 'myPublicIPAddress')]",
            "[resourceId('Microsoft.Network/virtualNetworks/', 'myVNet')]"
          ],
          "properties": {
            "ipConfigurations": [
              {
                "name": "ipconfig1",
                "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "publicIPAddress": { "id": "[resourceId('Microsoft.Network/publicIPAddresses','myPublicIPAddress')]" },
                  "subnet": { "id": "[variables('subnetRef')]" }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-04-30-preview",
          "type": "Microsoft.Compute/virtualMachines",
          "name": "myVM",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/networkInterfaces/', 'myNic')]"
          ],
          "properties": {
            "hardwareProfile": { "vmSize": "Standard_DS1" },
            "osProfile": {
              "computerName": "myVM",
              "adminUsername": "[parameters('adminUsername')]",
              "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
              "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "2012-R2-Datacenter",
                "version": "latest"
              },
              "osDisk": {
                "name": "myManagedOSDisk",
                "caching": "ReadWrite",
                "createOption": "FromImage"
              }
            },
            "networkProfile": {
              "networkInterfaces": [
                {
                  "id": "[resourceId('Microsoft.Network/networkInterfaces','myNic')]"
                }
              ]
            }
          }
        }
      ]
    }
    ```

2. Adlı bir dosya oluşturun *Parameters.json* ve bu JSON kodunu tooit ekleyin:

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      "adminUserName": { "value": "azureuser" },
        "adminPassword": { "value": "Azure12345678" }
      }
    }
    ```

3. Yeni depolama hesabı ve kapsayıcı oluşturun:

    ```powershell
    $storageName = "st" + (Get-Random)
    New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
    $accountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
    $context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
    New-AzureStorageContainer -Name "templates" -Context $context -Permission Container
    ```

4. Merhaba dosyaları toohello depolama hesabı karşıya yükle:

    ```powershell
    Set-AzureStorageBlobContent -File "C:\templates\CreateVMTemplate.json" -Context $context -Container "templates"
    Set-AzureStorageBlobContent -File "C:\templates\Parameters.json" -Context $context -Container templates
    ```

    Değişiklik hello - hello dosyaların depolandığı dosya yolları toohello konumu.

## <a name="create-hello-resources"></a>Merhaba kaynakları oluşturun

Merhaba parametreleri kullanarak hello şablonunu dağıtın:

```powershell
$templatePath = "https://" + $storageName + ".blob.core.windows.net/templates/CreateVMTemplate.json"
$parametersPath = "https://" + $storageName + ".blob.core.windows.net/templates/Parameters.json"
New-AzureRmResourceGroupDeployment -ResourceGroupName "myResourceGroup" -Name "myDeployment" -TemplateUri $templatePath -TemplateParameterUri $parametersPath 
```

> [!NOTE]
> Ayrıca, şablonları ve yerel dosyaları parametrelerinden dağıtabilirsiniz. toolearn daha, fazla [Azure Storage ile Azure PowerShell'i kullanma](../../storage/common/storage-powershell-guide-full.md).

## <a name="next-steps"></a>Sonraki Adımlar

- Merhaba dağıtımı ile ilgili sorunlar varsa, bir göz atalım [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](../../resource-manager-common-deployment-errors.md).
- Bilgi nasıl toocreate ve bir sanal makinede yönetmek [oluşturma ve hello Azure PowerShell modülü ile Windows sanal makineleri yönetme](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

