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
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a><span data-ttu-id="ddf36-103">Bir Windows sanal makine bir Resource Manager şablonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="ddf36-103">Create a Windows virtual machine from a Resource Manager template</span></span>

<span data-ttu-id="ddf36-104">Bu makale size nasıl gösterir toodeploy bir Azure Resource Manager PowerShell kullanarak şablonu.</span><span class="sxs-lookup"><span data-stu-id="ddf36-104">This article shows you how toodeploy an Azure Resource Manager template using PowerShell.</span></span> <span data-ttu-id="ddf36-105">oluşturduğunuz hello şablon tek bir alt ağ ile yeni bir sanal ağ içinde Windows Server çalıştıran tek bir sanal makine dağıtır.</span><span class="sxs-lookup"><span data-stu-id="ddf36-105">hello template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="ddf36-106">Merhaba sanal makine kaynağı ayrıntılı bir açıklaması için bkz: [sanal makineleri bir Azure Resource Manager şablonunda](template-description.md).</span><span class="sxs-lookup"><span data-stu-id="ddf36-106">For a detailed description of hello virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="ddf36-107">Bir şablona tüm hello kaynaklar hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonu Kılavuzu](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="ddf36-107">For more information about all hello resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="ddf36-108">Toodo hello bu makaledeki adımları yaklaşık beş dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="ddf36-108">It should take about five minutes toodo hello steps in this article.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="ddf36-109">Azure PowerShell'i yükleme</span><span class="sxs-lookup"><span data-stu-id="ddf36-109">Install Azure PowerShell</span></span>

<span data-ttu-id="ddf36-110">Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](../../powershell-install-configure.md) hello Azure PowerShell'in en son sürümünü yükleme, aboneliğinizi seçme ve tooyour hesabında imzalama hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="ddf36-110">See [How tooinstall and configure Azure PowerShell](../../powershell-install-configure.md) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="ddf36-111">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="ddf36-111">Create a resource group</span></span>

<span data-ttu-id="ddf36-112">Tüm kaynaklar dağıtılmalıdır bir [kaynak grubu](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ddf36-112">All resources must be deployed in a [resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="ddf36-113">Kaynakların oluşturulabileceği kullanılabilir konumların bir listesini alın.</span><span class="sxs-lookup"><span data-stu-id="ddf36-113">Get a list of available locations where resources can be created.</span></span>
   
    ```powershell   
    Get-AzureRmLocation | sort DisplayName | Select DisplayName
    ```

2. <span data-ttu-id="ddf36-114">Merhaba kaynak grubu seçtiğiniz hello konumda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ddf36-114">Create hello resource group in hello location that you select.</span></span> <span data-ttu-id="ddf36-115">Bu örnek, bir kaynak grubu hello oluşturulmasını gösterir **myResourceGroup** hello içinde **Batı ABD** konumu:</span><span class="sxs-lookup"><span data-stu-id="ddf36-115">This example shows hello creation of a resource group named **myResourceGroup** in hello **West US** location:</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
    ```

## <a name="create-hello-files"></a><span data-ttu-id="ddf36-116">Merhaba dosyaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="ddf36-116">Create hello files</span></span>

<span data-ttu-id="ddf36-117">Bu adımda, hello kaynakları dağıtan bir şablonu ve parametre değerlerini toohello şablon sağlayan bir parametre dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ddf36-117">In this step, you create a template file that deploys hello resources and a parameters file that supplies parameter values toohello template.</span></span> <span data-ttu-id="ddf36-118">Kullanılan tooperform Azure Resource Manager operations bir yetkilendirme dosya oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="ddf36-118">You also create an authorization file that is used tooperform Azure Resource Manager operations.</span></span>

1. <span data-ttu-id="ddf36-119">Adlı bir dosya oluşturun *CreateVMTemplate.json* ve bu JSON kodunu tooit ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ddf36-119">Create a file named *CreateVMTemplate.json* and add this JSON code tooit:</span></span>

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

2. <span data-ttu-id="ddf36-120">Adlı bir dosya oluşturun *Parameters.json* ve bu JSON kodunu tooit ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ddf36-120">Create a file named *Parameters.json* and add this JSON code tooit:</span></span>

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

3. <span data-ttu-id="ddf36-121">Yeni depolama hesabı ve kapsayıcı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ddf36-121">Create a new storage account and container:</span></span>

    ```powershell
    $storageName = "st" + (Get-Random)
    New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
    $accountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
    $context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
    New-AzureStorageContainer -Name "templates" -Context $context -Permission Container
    ```

4. <span data-ttu-id="ddf36-122">Merhaba dosyaları toohello depolama hesabı karşıya yükle:</span><span class="sxs-lookup"><span data-stu-id="ddf36-122">Upload hello files toohello storage account:</span></span>

    ```powershell
    Set-AzureStorageBlobContent -File "C:\templates\CreateVMTemplate.json" -Context $context -Container "templates"
    Set-AzureStorageBlobContent -File "C:\templates\Parameters.json" -Context $context -Container templates
    ```

    <span data-ttu-id="ddf36-123">Değişiklik hello - hello dosyaların depolandığı dosya yolları toohello konumu.</span><span class="sxs-lookup"><span data-stu-id="ddf36-123">Change hello -File paths toohello location where you stored hello files.</span></span>

## <a name="create-hello-resources"></a><span data-ttu-id="ddf36-124">Merhaba kaynakları oluşturun</span><span class="sxs-lookup"><span data-stu-id="ddf36-124">Create hello resources</span></span>

<span data-ttu-id="ddf36-125">Merhaba parametreleri kullanarak hello şablonunu dağıtın:</span><span class="sxs-lookup"><span data-stu-id="ddf36-125">Deploy hello template using hello parameters:</span></span>

```powershell
$templatePath = "https://" + $storageName + ".blob.core.windows.net/templates/CreateVMTemplate.json"
$parametersPath = "https://" + $storageName + ".blob.core.windows.net/templates/Parameters.json"
New-AzureRmResourceGroupDeployment -ResourceGroupName "myResourceGroup" -Name "myDeployment" -TemplateUri $templatePath -TemplateParameterUri $parametersPath 
```

> [!NOTE]
> <span data-ttu-id="ddf36-126">Ayrıca, şablonları ve yerel dosyaları parametrelerinden dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddf36-126">You can also deploy templates and parameters from local files.</span></span> <span data-ttu-id="ddf36-127">toolearn daha, fazla [Azure Storage ile Azure PowerShell'i kullanma](../../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="ddf36-127">toolearn more, see [Using Azure PowerShell with Azure Storage](../../storage/common/storage-powershell-guide-full.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddf36-128">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="ddf36-128">Next Steps</span></span>

- <span data-ttu-id="ddf36-129">Merhaba dağıtımı ile ilgili sorunlar varsa, bir göz atalım [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="ddf36-129">If there were issues with hello deployment, you might take a look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
- <span data-ttu-id="ddf36-130">Bilgi nasıl toocreate ve bir sanal makinede yönetmek [oluşturma ve hello Azure PowerShell modülü ile Windows sanal makineleri yönetme](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ddf36-130">Learn how toocreate and manage a virtual machine in [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

