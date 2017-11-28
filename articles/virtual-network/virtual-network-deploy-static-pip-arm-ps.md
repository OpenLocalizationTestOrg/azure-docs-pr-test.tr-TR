---
title: bir statik genel IP adresi - Azure PowerShell ile bir VM aaaCreate | Microsoft Docs
description: "Nasıl toocreate VM bir statik genel IP adresi PowerShell'i kullanma hakkında bilgi edinin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ad975ab9-d69f-45c1-9e45-0d3f0f51e87e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d2b88319cb114b8616f60dbee41e8fdc6d8b1b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-powershell"></a><span data-ttu-id="9463d-103">PowerShell kullanarak bir statik genel IP adresiyle bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="9463d-103">Create a VM with a static public IP address using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9463d-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="9463d-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="9463d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9463d-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="9463d-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9463d-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="9463d-107">Şablon</span><span class="sxs-lookup"><span data-stu-id="9463d-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="9463d-108">PowerShell (Klasik)</span><span class="sxs-lookup"><span data-stu-id="9463d-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="9463d-109">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9463d-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9463d-110">Bu makalede, Microsoft hello Klasik dağıtım modeli yerine çoğu yeni dağıtımlar için önerir hello Resource Manager dağıtım modeli kullanılarak kapsar.</span><span class="sxs-lookup"><span data-stu-id="9463d-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="step-1---start-your-script"></a><span data-ttu-id="9463d-111">1. adım - kodunuzu Başlat</span><span class="sxs-lookup"><span data-stu-id="9463d-111">Step 1 - Start your script</span></span>
<span data-ttu-id="9463d-112">Kullanılan hello tam PowerShell komut dosyası indirebilirsiniz [burada](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="9463d-112">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-ps.ps1).</span></span> <span data-ttu-id="9463d-113">Ortamınızdaki toochange hello betik toowork Hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="9463d-113">Follow hello steps below toochange hello script toowork in your environment.</span></span>

<span data-ttu-id="9463d-114">Merhaba değerlerini değiştirin dağıtımınız için toouse istediğiniz hello değişkenleri aşağıdaki hello değerlerine göre.</span><span class="sxs-lookup"><span data-stu-id="9463d-114">Change hello values of hello variables below based on hello values you want toouse for your deployment.</span></span> <span data-ttu-id="9463d-115">Bu makalede kullanılan değerleri harita toohello senaryo aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="9463d-115">hello following values map toohello scenario used in this article:</span></span>

```powershell
# Set variables resource group
$rgName                = "IaaSStory"
$location              = "West US"

# Set variables for VNet
$vnetName              = "WTestVNet"
$vnetPrefix            = "192.168.0.0/16"
$subnetName            = "FrontEnd"
$subnetPrefix          = "192.168.1.0/24"

# Set variables for storage
$stdStorageAccountName = "iaasstorystorage"

# Set variables for VM
$vmSize                = "Standard_A1"
$diskSize              = 127
$publisher             = "MicrosoftWindowsServer"
$offer                 = "WindowsServer"
$sku                   = "2012-R2-Datacenter"
$version               = "latest"
$vmName                = "WEB1"
$osDiskName            = "osdisk"
$nicName               = "NICWEB1"
$privateIPAddress      = "192.168.1.101"
$pipName               = "PIPWEB1"
$dnsName               = "iaasstoryws1"
```

## <a name="step-2---create-hello-necessary-resources-for-your-vm"></a><span data-ttu-id="9463d-116">2. adım - hello gerekli kaynaklar için VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="9463d-116">Step 2 - Create hello necessary resources for your VM</span></span>
<span data-ttu-id="9463d-117">Bir VM oluşturmadan önce bir kaynak grubu, VNet, ortak IP ve NIC ihtiyacınız toobe hello VM tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9463d-117">Before creating a VM, you need a resource group, VNet, public IP, and NIC toobe used by hello VM.</span></span>

1. <span data-ttu-id="9463d-118">Yeni bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9463d-118">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $rgName -Location $location
    ```

2. <span data-ttu-id="9463d-119">Oluşturma VNet ve alt ağ hello.</span><span class="sxs-lookup"><span data-stu-id="9463d-119">Create hello VNet and subnet.</span></span>

    ```powershell
    $vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName `
        -AddressPrefix $vnetPrefix -Location $location

    Add-AzureRmVirtualNetworkSubnetConfig -Name $subnetName `
        -VirtualNetwork $vnet -AddressPrefix $subnetPrefix

    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

3. <span data-ttu-id="9463d-120">Merhaba genel IP kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9463d-120">Create hello public IP resource.</span></span> 

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name $pipName -ResourceGroupName $rgName `
        -AllocationMethod Static -DomainNameLabel $dnsName -Location $location
    ```

4. <span data-ttu-id="9463d-121">Yukarıdaki hello genel IP ile oluşturulan hello alt hello VM için Hello ağ arabirimi (NIC) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9463d-121">Create hello network interface (NIC) for hello VM in hello subnet created above, with hello public IP.</span></span> <span data-ttu-id="9463d-122">Azure'dan Hello VNet alma ilk cmdlet hello dikkat edin, bu yana gereklidir bir `Set-AzureRmVirtualNetwork` oluştu yürütülen toochange hello mevcut VNet.</span><span class="sxs-lookup"><span data-stu-id="9463d-122">Notice hello first cmdlet retrieving hello VNet from Azure, this is necessary since a `Set-AzureRmVirtualNetwork` was executed toochange hello existing VNet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name $subnetName
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
        -Subnet $subnet -Location $location -PrivateIpAddress $privateIPAddress `
        -PublicIpAddress $pip
    ```

5. <span data-ttu-id="9463d-123">Bir depolama hesabı toohost hello VM işletim sistemi sürücüsü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9463d-123">Create a storage account toohost hello VM OS drive.</span></span>

    ```powershell
    $stdStorageAccount = New-AzureRmStorageAccount -Name $stdStorageAccountName `
    -ResourceGroupName $rgName -Type Standard_LRS -Location $location
    ```

## <a name="step-3---create-hello-vm"></a><span data-ttu-id="9463d-124">3. adım - hello VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="9463d-124">Step 3 - Create hello VM</span></span>
<span data-ttu-id="9463d-125">Gereken tüm kaynakların yerine getirildiğinden, yeni bir VM oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9463d-125">Now that all necessary resources are in place, you can create a new VM.</span></span>

1. <span data-ttu-id="9463d-126">Merhaba VM için Hello yapılandırma nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9463d-126">Create hello configuration object for hello VM.</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
    ```

2. <span data-ttu-id="9463d-127">Merhaba VM yerel yönetici hesabının kimlik bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="9463d-127">Get credentials for hello VM local administrator account.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type hello name and password for hello local administrator account."
    ```

3. <span data-ttu-id="9463d-128">Bir VM yapılandırma nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9463d-128">Create a VM configuration object.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    ```

4. <span data-ttu-id="9463d-129">Merhaba işletim sistemi görüntüsü hello VM için ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9463d-129">Set hello operating system image for hello VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher `
        -Offer $offer -Skus $sku -Version $version
    ```

5. <span data-ttu-id="9463d-130">Merhaba işletim sistemi diski yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9463d-130">Configure hello OS disk.</span></span>

    ```powershell
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    ```

6. <span data-ttu-id="9463d-131">Merhaba NIC toohello VM ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9463d-131">Add hello NIC toohello VM.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id -Primary
    ```

7. <span data-ttu-id="9463d-132">Merhaba VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9463d-132">Create hello VM.</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $rgName -Location $location
    ```

8. <span data-ttu-id="9463d-133">Merhaba komut dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9463d-133">Save hello script file.</span></span>

## <a name="step-4---run-hello-script"></a><span data-ttu-id="9463d-134">Adım 4 - çalışma hello komut dosyası</span><span class="sxs-lookup"><span data-stu-id="9463d-134">Step 4 - Run hello script</span></span>
<span data-ttu-id="9463d-135">Gerekli değişiklikleri yapma ve hello betik anlama sonra yukarıda Göster, hello komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9463d-135">After making any necessary changes, and understanding hello script show above, run hello script.</span></span> 

1. <span data-ttu-id="9463d-136">Bir PowerShell konsolunu veya PowerShell ISE, yukarıdaki hello betiği çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9463d-136">From a PowerShell console, or PowerShell ISE, run hello script above.</span></span>
2. <span data-ttu-id="9463d-137">Çıktı aşağıdaki hello birkaç dakika sonra görüntülenmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="9463d-137">hello following output should be displayed after a few minutes:</span></span>
   
        ResourceGroupName : IaaSStory
        Location          : westus
        ProvisioningState : Succeeded
        Tags              : 
        ResourceId        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory
   
        AddressSpace      : Microsoft.Azure.Commands.Network.Models.PSAddressSpace
        DhcpOptions       : Microsoft.Azure.Commands.Network.Models.PSDhcpOptions
        Subnets           : {FrontEnd}
        ProvisioningState : Succeeded
        AddressSpaceText  : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptionsText   : {}
        SubnetsText       : [
                              {
                                "Name": "FrontEnd",
                                "AddressPrefix": "192.168.1.0/24"
                              }
                            ]
        ResourceGroupName : IaaSStory
        Location          : westus
        ResourceGuid      : [Id]
        Tag               : {}
        TagsTable         : 
        Name              : WTestVNet
        Etag              : W/"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        Id                : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet
   
        AddressSpace      : Microsoft.Azure.Commands.Network.Models.PSAddressSpace
        DhcpOptions       : Microsoft.Azure.Commands.Network.Models.PSDhcpOptions
        Subnets           : {FrontEnd}
        ProvisioningState : Succeeded
        AddressSpaceText  : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptionsText   : {
                              "DnsServers": []
                            }
        SubnetsText       : [
                              {
                                "Name": "FrontEnd",
                                "Etag": [Id],
                                "Id": "/subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "ProvisioningState": "Succeeded"
                              }
                            ]
        ResourceGroupName : IaaSStory
        Location          : westus
        ResourceGuid      : [Id]
        Tag               : {}
        TagsTable         : 
        Name              : WTestVNet
        Etag              : [Id]
        Id                : /subscriptions/[Subscription Id]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet
   
        TrackingOperationId : [Id]
        RequestId           : [Id]
        Status              : Succeeded
        StatusCode          : OK
        Output              : 
        StartTime           : [Subscription Id]
        EndTime             : [Subscription Id]
        Error               : 
        ErrorText           : 

