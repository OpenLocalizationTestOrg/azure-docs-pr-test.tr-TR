---
title: "Bir statik genel IP adresi ile - Azure PowerShell bir VM oluşturma | Microsoft Docs"
description: "PowerShell kullanarak bir statik genel IP adresi ile VM oluşturmayı öğrenin."
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
ms.openlocfilehash: e4c413d3cb5c242a16f3e534dafe322785a35141
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-powershell"></a><span data-ttu-id="dd64f-103">PowerShell kullanarak bir statik genel IP adresiyle bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd64f-103">Create a VM with a static public IP address using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="dd64f-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="dd64f-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="dd64f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd64f-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="dd64f-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="dd64f-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="dd64f-107">Şablon</span><span class="sxs-lookup"><span data-stu-id="dd64f-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="dd64f-108">PowerShell (Klasik)</span><span class="sxs-lookup"><span data-stu-id="dd64f-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="dd64f-109">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="dd64f-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="dd64f-110">Bu makalede, Klasik dağıtım modeli yerine en yeni dağıtımlar için Microsoft önerir Resource Manager dağıtım modelini kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="dd64f-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="step-1---start-your-script"></a><span data-ttu-id="dd64f-111">1. adım - kodunuzu Başlat</span><span class="sxs-lookup"><span data-stu-id="dd64f-111">Step 1 - Start your script</span></span>
<span data-ttu-id="dd64f-112">Kullanılan tam PowerShell komut dosyası indirebilirsiniz [burada](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="dd64f-112">You can download the full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-ps.ps1).</span></span> <span data-ttu-id="dd64f-113">Ortamınızda çalışması için komut dosyasını değiştirmek için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="dd64f-113">Follow the steps below to change the script to work in your environment.</span></span>

<span data-ttu-id="dd64f-114">Dağıtımınız için kullanmak istediğiniz değerleri temel alarak aşağıdaki değişkenlerinin değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="dd64f-114">Change the values of the variables below based on the values you want to use for your deployment.</span></span> <span data-ttu-id="dd64f-115">Bu makalede kullanılan senaryo için aşağıdaki değerleri eşleyin:</span><span class="sxs-lookup"><span data-stu-id="dd64f-115">The following values map to the scenario used in this article:</span></span>

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

## <a name="step-2---create-the-necessary-resources-for-your-vm"></a><span data-ttu-id="dd64f-116">Adım 2 - gerekli kaynaklar için VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd64f-116">Step 2 - Create the necessary resources for your VM</span></span>
<span data-ttu-id="dd64f-117">Bir VM oluşturmadan önce bir kaynak grubu, VNet, genel IP ve NIC VM tarafından kullanılacak gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd64f-117">Before creating a VM, you need a resource group, VNet, public IP, and NIC to be used by the VM.</span></span>

1. <span data-ttu-id="dd64f-118">Yeni bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dd64f-118">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $rgName -Location $location
    ```

2. <span data-ttu-id="dd64f-119">VNet ve alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dd64f-119">Create the VNet and subnet.</span></span>

    ```powershell
    $vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName `
        -AddressPrefix $vnetPrefix -Location $location

    Add-AzureRmVirtualNetworkSubnetConfig -Name $subnetName `
        -VirtualNetwork $vnet -AddressPrefix $subnetPrefix

    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

3. <span data-ttu-id="dd64f-120">Genel IP kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dd64f-120">Create the public IP resource.</span></span> 

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name $pipName -ResourceGroupName $rgName `
        -AllocationMethod Static -DomainNameLabel $dnsName -Location $location
    ```

4. <span data-ttu-id="dd64f-121">Yukarıdaki genel IP ile oluşturulan alt ağdaki sanal makine için ağ arabirimi (NIC) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dd64f-121">Create the network interface (NIC) for the VM in the subnet created above, with the public IP.</span></span> <span data-ttu-id="dd64f-122">Azure VNet alma ilk cmdlet dikkat edin, bu yana gereklidir bir `Set-AzureRmVirtualNetwork` mevcut VNet değiştirmek için yürütüldü.</span><span class="sxs-lookup"><span data-stu-id="dd64f-122">Notice the first cmdlet retrieving the VNet from Azure, this is necessary since a `Set-AzureRmVirtualNetwork` was executed to change the existing VNet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name $subnetName
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
        -Subnet $subnet -Location $location -PrivateIpAddress $privateIPAddress `
        -PublicIpAddress $pip
    ```

5. <span data-ttu-id="dd64f-123">VM işletim sistemi sürücüsünü barındırmak için bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dd64f-123">Create a storage account to host the VM OS drive.</span></span>

    ```powershell
    $stdStorageAccount = New-AzureRmStorageAccount -Name $stdStorageAccountName `
    -ResourceGroupName $rgName -Type Standard_LRS -Location $location
    ```

## <a name="step-3---create-the-vm"></a><span data-ttu-id="dd64f-124">3. adım - VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd64f-124">Step 3 - Create the VM</span></span>
<span data-ttu-id="dd64f-125">Gereken tüm kaynakların yerine getirildiğinden, yeni bir VM oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd64f-125">Now that all necessary resources are in place, you can create a new VM.</span></span>

1. <span data-ttu-id="dd64f-126">VM için yapılandırma nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dd64f-126">Create the configuration object for the VM.</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
    ```

2. <span data-ttu-id="dd64f-127">VM yerel yönetici hesabı için kimlik bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="dd64f-127">Get credentials for the VM local administrator account.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type the name and password for the local administrator account."
    ```

3. <span data-ttu-id="dd64f-128">Bir VM yapılandırma nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dd64f-128">Create a VM configuration object.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    ```

4. <span data-ttu-id="dd64f-129">VM için işletim sistemi görüntüsünü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="dd64f-129">Set the operating system image for the VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher `
        -Offer $offer -Skus $sku -Version $version
    ```

5. <span data-ttu-id="dd64f-130">İşletim sistemi diski yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="dd64f-130">Configure the OS disk.</span></span>

    ```powershell
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    ```

6. <span data-ttu-id="dd64f-131">NIC VM'ye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="dd64f-131">Add the NIC to the VM.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id -Primary
    ```

7. <span data-ttu-id="dd64f-132">VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dd64f-132">Create the VM.</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $rgName -Location $location
    ```

8. <span data-ttu-id="dd64f-133">Komut dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="dd64f-133">Save the script file.</span></span>

## <a name="step-4---run-the-script"></a><span data-ttu-id="dd64f-134">Adım 4 - komut dosyasını çalıştır</span><span class="sxs-lookup"><span data-stu-id="dd64f-134">Step 4 - Run the script</span></span>
<span data-ttu-id="dd64f-135">Gerekli değişiklikleri yapma ve komut dosyası anlama sonra yukarıda Göster, komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="dd64f-135">After making any necessary changes, and understanding the script show above, run the script.</span></span> 

1. <span data-ttu-id="dd64f-136">Bir PowerShell konsolunu veya PowerShell ISE, yukarıdaki komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="dd64f-136">From a PowerShell console, or PowerShell ISE, run the script above.</span></span>
2. <span data-ttu-id="dd64f-137">Birkaç dakika sonra aşağıdaki çıkış görüntülenmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="dd64f-137">The following output should be displayed after a few minutes:</span></span>
   
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

