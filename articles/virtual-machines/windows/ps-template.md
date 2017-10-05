---
title: "Azure'da bir şablondan bir Windows VM oluşturma | Microsoft Docs"
description: "Resource Manager şablonu ve PowerShell kolayca yeni bir Windows VM oluşturmak için kullanın."
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
ms.openlocfilehash: ddab80262fe27c1f5995858ec7de75d7c46df081
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a><span data-ttu-id="15a75-103">Bir Windows sanal makine bir Resource Manager şablonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="15a75-103">Create a Windows virtual machine from a Resource Manager template</span></span>

<span data-ttu-id="15a75-104">Bu makalede PowerShell kullanarak bir Azure Resource Manager şablonu dağıtma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="15a75-104">This article shows you how to deploy an Azure Resource Manager template using PowerShell.</span></span> <span data-ttu-id="15a75-105">Oluşturduğunuz şablon, tek bir alt ağ ile yeni bir sanal ağ içinde Windows Server çalıştıran tek bir sanal makine dağıtır.</span><span class="sxs-lookup"><span data-stu-id="15a75-105">The template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="15a75-106">Sanal makine kaynağı ayrıntılı bir açıklaması için bkz: [sanal makineleri bir Azure Resource Manager şablonunda](template-description.md).</span><span class="sxs-lookup"><span data-stu-id="15a75-106">For a detailed description of the virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="15a75-107">Bir şablona tüm kaynaklar hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonu Kılavuzu](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="15a75-107">For more information about all the resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="15a75-108">Bu makaledeki adımları yapmak için yaklaşık beş dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="15a75-108">It should take about five minutes to do the steps in this article.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="15a75-109">Azure PowerShell'i yükleme</span><span class="sxs-lookup"><span data-stu-id="15a75-109">Install Azure PowerShell</span></span>

<span data-ttu-id="15a75-110">Azure PowerShell’in en son sürümünü yükleme, aboneliğinizi seçme ve hesabınızda oturum açma hakkında bilgi almak için bkz. [Azure PowerShell’i yükleme ve yapılandırma](../../powershell-install-configure.md).</span><span class="sxs-lookup"><span data-stu-id="15a75-110">See [How to install and configure Azure PowerShell](../../powershell-install-configure.md) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to your account.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="15a75-111">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="15a75-111">Create a resource group</span></span>

<span data-ttu-id="15a75-112">Tüm kaynaklar dağıtılmalıdır bir [kaynak grubu](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="15a75-112">All resources must be deployed in a [resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="15a75-113">Kaynakların oluşturulabileceği kullanılabilir konumların bir listesini alın.</span><span class="sxs-lookup"><span data-stu-id="15a75-113">Get a list of available locations where resources can be created.</span></span>
   
    ```powershell   
    Get-AzureRmLocation | sort DisplayName | Select DisplayName
    ```

2. <span data-ttu-id="15a75-114">Kaynak grubu seçtiğiniz konumda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="15a75-114">Create the resource group in the location that you select.</span></span> <span data-ttu-id="15a75-115">Bu örnek, bir kaynak grubu oluşturulmasını gösterir **myResourceGroup** içinde **Batı ABD** konumu:</span><span class="sxs-lookup"><span data-stu-id="15a75-115">This example shows the creation of a resource group named **myResourceGroup** in the **West US** location:</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
    ```

## <a name="create-the-files"></a><span data-ttu-id="15a75-116">Dosyaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="15a75-116">Create the files</span></span>

<span data-ttu-id="15a75-117">Bu adımda, kaynakları dağıtan bir şablon dosyası ve şablon parametre değerlerini sağlayan bir parametre dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="15a75-117">In this step, you create a template file that deploys the resources and a parameters file that supplies parameter values to the template.</span></span> <span data-ttu-id="15a75-118">Ayrıca Azure Resource Manager işlemlerini gerçekleştirmek için kullanılan bir yetkilendirme dosyasını oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="15a75-118">You also create an authorization file that is used to perform Azure Resource Manager operations.</span></span>

1. <span data-ttu-id="15a75-119">Adlı bir dosya oluşturun *CreateVMTemplate.json* ve bu JSON kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="15a75-119">Create a file named *CreateVMTemplate.json* and add this JSON code to it:</span></span>

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

2. <span data-ttu-id="15a75-120">Adlı bir dosya oluşturun *Parameters.json* ve bu JSON kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="15a75-120">Create a file named *Parameters.json* and add this JSON code to it:</span></span>

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

3. <span data-ttu-id="15a75-121">Yeni depolama hesabı ve kapsayıcı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="15a75-121">Create a new storage account and container:</span></span>

    ```powershell
    $storageName = "st" + (Get-Random)
    New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
    $accountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
    $context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
    New-AzureStorageContainer -Name "templates" -Context $context -Permission Container
    ```

4. <span data-ttu-id="15a75-122">Dosyaları karşıya yükleme için depolama hesabı:</span><span class="sxs-lookup"><span data-stu-id="15a75-122">Upload the files to the storage account:</span></span>

    ```powershell
    Set-AzureStorageBlobContent -File "C:\templates\CreateVMTemplate.json" -Context $context -Container "templates"
    Set-AzureStorageBlobContent -File "C:\templates\Parameters.json" -Context $context -Container templates
    ```

    <span data-ttu-id="15a75-123">Değişiklik dosyaların depolandığı konumun dosya yolları.</span><span class="sxs-lookup"><span data-stu-id="15a75-123">Change the -File paths to the location where you stored the files.</span></span>

## <a name="create-the-resources"></a><span data-ttu-id="15a75-124">Kaynakları oluşturun</span><span class="sxs-lookup"><span data-stu-id="15a75-124">Create the resources</span></span>

<span data-ttu-id="15a75-125">Parametreleri kullanarak şablonu dağıtmak:</span><span class="sxs-lookup"><span data-stu-id="15a75-125">Deploy the template using the parameters:</span></span>

```powershell
$templatePath = "https://" + $storageName + ".blob.core.windows.net/templates/CreateVMTemplate.json"
$parametersPath = "https://" + $storageName + ".blob.core.windows.net/templates/Parameters.json"
New-AzureRmResourceGroupDeployment -ResourceGroupName "myResourceGroup" -Name "myDeployment" -TemplateUri $templatePath -TemplateParameterUri $parametersPath 
```

> [!NOTE]
> <span data-ttu-id="15a75-126">Ayrıca, şablonları ve yerel dosyaları parametrelerinden dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15a75-126">You can also deploy templates and parameters from local files.</span></span> <span data-ttu-id="15a75-127">Daha fazla bilgi için bkz: [Azure Storage ile Azure PowerShell'i kullanma](../../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="15a75-127">To learn more, see [Using Azure PowerShell with Azure Storage](../../storage/common/storage-powershell-guide-full.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="15a75-128">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="15a75-128">Next Steps</span></span>

- <span data-ttu-id="15a75-129">Dağıtım ile ilgili sorunlar varsa, bir göz atalım [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="15a75-129">If there were issues with the deployment, you might take a look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
- <span data-ttu-id="15a75-130">Oluşturma ve bir sanal makinede yönetme hakkında bilgi edinin [oluşturma ve Azure PowerShell modülü ile Windows sanal makineleri yönetme](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="15a75-130">Learn how to create and manage a virtual machine in [Create and manage Windows VMs with the Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

