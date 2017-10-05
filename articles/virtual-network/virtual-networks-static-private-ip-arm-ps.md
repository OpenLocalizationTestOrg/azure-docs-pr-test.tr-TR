---
title: "Özel IP adresleri - Azure PowerShell VM'ler için yapılandırma | Microsoft Docs"
description: "PowerShell kullanarak sanal makineleri için özel IP adresleri yapılandırmayı öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: d5f18929-15e3-40a2-9ee3-8188bc248ed8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2810190897c44c944912ef3325b1f40479aa3078
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-powershell"></a><span data-ttu-id="76de2-103">PowerShell kullanarak bir sanal makine için özel IP adreslerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="76de2-103">Configure private IP addresses for a virtual machine using PowerShell</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

<span data-ttu-id="76de2-104">Azure'un iki dağıtım modeli vardır: Azure Resource Manager ve klasik.</span><span class="sxs-lookup"><span data-stu-id="76de2-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="76de2-105">Microsoft, kaynakların Resource Manager dağıtım modeliyle oluşturulmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="76de2-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="76de2-106">İki model arasındaki farkları öğrenmek için [Azure dağıtım modellerini anlama](../azure-resource-manager/resource-manager-deployment-model.md) makalesini okuyun.</span><span class="sxs-lookup"><span data-stu-id="76de2-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="76de2-107">Bu makalede Resource Manager dağıtım modeli anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="76de2-107">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="76de2-108">Ayrıca [Klasik dağıtım modelinde statik özel IP adresi yönetmek](virtual-networks-static-private-ip-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="76de2-108">You can also [manage static private IP address in the classic deployment model](virtual-networks-static-private-ip-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="76de2-109">Aşağıdaki komutları önceden oluşturulmuş basit bir ortam beklediğiniz PowerShell örnek yukarıdaki senaryo tabanlı.</span><span class="sxs-lookup"><span data-stu-id="76de2-109">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="76de2-110">Bu belgede gösterildiği komutları çalıştırmak istiyorsanız, önce açıklanan test ortamı oluşturmak [vnet oluşturma](virtual-networks-create-vnet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="76de2-110">If you want to run the commands as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-arm-ps.md).</span></span>

## <a name="create-a-vm-with-a-static-private-ip-address"></a><span data-ttu-id="76de2-111">Statik özel IP adresiyle VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="76de2-111">Create a VM with a static private IP address</span></span>
<span data-ttu-id="76de2-112">Adlı bir VM oluşturmak için *DNS01* içinde *ön uç* adlı bir sanal ağ alt ağı *TestVNet* özel bir statik IP *192.168.1.101*, aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="76de2-112">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span></span>

1. <span data-ttu-id="76de2-113">Depolama hesabı, konumu, kaynak grubu ve kimlik bilgileri kullanılacak değişkenleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="76de2-113">Set variables for the storage account, location, resource group, and credentials to be used.</span></span> <span data-ttu-id="76de2-114">VM için bir kullanıcı adı ve parola girmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="76de2-114">You will need to enter a user name and password for the VM.</span></span> <span data-ttu-id="76de2-115">Depolama hesabı ve kaynak grubu zaten mevcut olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="76de2-115">The storage account and resource group must already exist.</span></span>

    ```powershell
    $stName  = "vnetstorage"
    $locName = "Central US"
    $rgName  = "TestRG"
    $cred    = Get-Credential -Message "Type the name and password of the local administrator account."
    ```

2. <span data-ttu-id="76de2-116">VM'yi oluşturmak istediğiniz alt ağ ve sanal ağ alın.</span><span class="sxs-lookup"><span data-stu-id="76de2-116">Retrieve the virtual network and subnet you want to create the VM in.</span></span>

    ```powershell
    $vnet   = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    $subnet = $vnet.Subnets[0].Id
    ```

3. <span data-ttu-id="76de2-117">Gerekirse, VM Internet'ten erişmek için genel bir IP adresi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="76de2-117">If necessary, create a public IP address to access the VM from the Internet.</span></span>

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name TestPIP -ResourceGroupName $rgName `
    -Location $locName -AllocationMethod Dynamic
    ```

4. <span data-ttu-id="76de2-118">VM atamak istediğiniz özel statik IP adresi kullanarak bir NIC oluşturun.</span><span class="sxs-lookup"><span data-stu-id="76de2-118">Create a NIC using the static private IP address you want to assign to the VM.</span></span> <span data-ttu-id="76de2-119">IP alt ağı aralığından VM'ye ekleniyor olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="76de2-119">Make sure the IP is from the subnet range you are adding the VM to.</span></span> <span data-ttu-id="76de2-120">Statik olarak özel IP ayarladığınız Bu makale için ana adım budur.</span><span class="sxs-lookup"><span data-stu-id="76de2-120">This is the main step for this article, where you set the private IP to be static.</span></span>

    ```powershell
    $nic = New-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName $rgName `
    -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id `
    -PrivateIpAddress 192.168.1.101
    ```

5. <span data-ttu-id="76de2-121">Yukarıda oluşturduğunuz NIC kullanarak VM oluşturma.</span><span class="sxs-lookup"><span data-stu-id="76de2-121">Create the VM using the NIC created above.</span></span>

    ```powershell
    $vm = New-AzureRmVMConfig -VMName DNS01 -VMSize "Standard_A1"
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName DNS01 `
    -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri = $storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/WindowsVMosDisk.vhd"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name "windowsvmosdisk" -VhdUri $osDiskUri `
    -CreateOption fromImage
    New-AzureRmVM -ResourceGroupName $rgName -Location $locName -VM $vm 
    ```

    <span data-ttu-id="76de2-122">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="76de2-122">Expected output:</span></span>
    
        EndTime             : [Date and time]
        Error               : 
        Output              : 
        StartTime           : [Date and time]
        Status              : Succeeded
        TrackingOperationId : [Id]
        RequestId           : [Id]
        StatusCode          : OK 

## <a name="retrieve-static-private-ip-address-information-for-a-network-interface"></a><span data-ttu-id="76de2-123">Bir ağ arabirimi için özel statik IP adresi bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="76de2-123">Retrieve static private IP address information for a network interface</span></span>
<span data-ttu-id="76de2-124">Komut dosyası yukarıdaki VM oluşturulan için statik özel IP adresi bilgilerini görüntülemek için aşağıdaki PowerShell komutunu çalıştırın ve değerlerini uyun *PrivateIpAddress* ve *Privateıpallocationmethod*:</span><span class="sxs-lookup"><span data-stu-id="76de2-124">To view the static private IP address information for the VM created with the script above, run the following PowerShell command and observe the values for *PrivateIpAddress* and *PrivateIpAllocationMethod*:</span></span>

```powershell
Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
```

<span data-ttu-id="76de2-125">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="76de2-125">Expected output:</span></span>

    Name                 : TestNIC
    ResourceGroupName    : TestRG
    Location             : centralus
    Id                   : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    Etag                 : W/"[Id]"
    ProvisioningState    : Succeeded
    Tags                 : 
    VirtualMachine       : {
                             "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01"
                           }
    IpConfigurations     : [
                             {
                               "Name": "ipconfig1",
                               "Etag": "W/\"[Id]\"",
                               "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                               "PrivateIpAddress": "192.168.1.101",
                               "PrivateIpAllocationMethod": "Static",
                               "Subnet": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                               },
                               "PublicIpAddress": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP"
                               },
                               "LoadBalancerBackendAddressPools": [],
                               "LoadBalancerInboundNatRules": [],
                               "ProvisioningState": "Succeeded"
                             }
                           ]
    DnsSettings          : {
                             "DnsServers": [],
                             "AppliedDnsServers": [],
                             "InternalDnsNameLabel": null,
                             "InternalFqdn": null
                           }
    EnableIPForwarding   : False
    NetworkSecurityGroup : null
    Primary              : True

## <a name="remove-a-static-private-ip-address-from-a-network-interface"></a><span data-ttu-id="76de2-126">Özel bir statik IP adresi bir ağ arabiriminden Kaldır</span><span class="sxs-lookup"><span data-stu-id="76de2-126">Remove a static private IP address from a network interface</span></span>
<span data-ttu-id="76de2-127">Özel statik IP adresi kaldırmak için yukarıdaki komut VM'ye aşağıdaki PowerShell komutlarını çalıştırın ekledi:</span><span class="sxs-lookup"><span data-stu-id="76de2-127">To remove the static private IP address added to the VM in the script above, run the following PowerShell commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Dynamic"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="76de2-128">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="76de2-128">Expected output:</span></span>

    Name                 : TestNIC
    ResourceGroupName    : TestRG
    Location             : centralus
    Id                   : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    Etag                 : W/"[Id]"
    ProvisioningState    : Succeeded
    Tags                 : 
    VirtualMachine       : {
                             "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/WindowsVM"
                           }
    IpConfigurations     : [
                             {
                               "Name": "ipconfig1",
                               "Etag": "W/\"[Id]\"",
                               "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                               "PrivateIpAddress": "192.168.1.101",
                               "PrivateIpAllocationMethod": "Dynamic",
                               "Subnet": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                               },
                               "PublicIpAddress": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP"
                               },
                               "LoadBalancerBackendAddressPools": [],
                               "LoadBalancerInboundNatRules": [],
                               "ProvisioningState": "Succeeded"
                             }
                           ]
    DnsSettings          : {
                             "DnsServers": [],
                             "AppliedDnsServers": [],
                             "InternalDnsNameLabel": null,
                             "InternalFqdn": null
                           }
    EnableIPForwarding   : False
    NetworkSecurityGroup : null
    Primary              : True

## <a name="add-a-static-private-ip-address-to-a-network-interface"></a><span data-ttu-id="76de2-129">Bir ağ arabirimi için özel bir statik IP adresi Ekle</span><span class="sxs-lookup"><span data-stu-id="76de2-129">Add a static private IP address to a network interface</span></span>
<span data-ttu-id="76de2-130">Yukarıdaki komut dosyası kullanılarak oluşturulan VM için özel bir statik IP adresi eklemek için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="76de2-130">To add a static private IP address to the VM created using the script above, run the following commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Static"
$nic.IpConfigurations[0].PrivateIpAddress = "192.168.1.101"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```
## <a name="change-the-allocation-method-for-a-private-ip-address-assigned-to-a-network-interface"></a><span data-ttu-id="76de2-131">Bir ağ arabirimine atanmış özel bir IP adresi ayırma yöntemini değiştirme</span><span class="sxs-lookup"><span data-stu-id="76de2-131">Change the allocation method for a private IP address assigned to a network interface</span></span>

<span data-ttu-id="76de2-132">Özel bir IP adresi statik veya dinamik ayırma yöntemiyle bir NIC'ye atanır.</span><span class="sxs-lookup"><span data-stu-id="76de2-132">A private IP address is assigned to a NIC with the static or dynamic allocation method.</span></span> <span data-ttu-id="76de2-133">Dinamik IP adresleri, daha önce durduruldu (serbest bırakıldığında) durumdaydı bir VM başlattıktan sonra değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76de2-133">Dynamic IP addresses can change after starting a VM that was previously in the stopped (deallocated) state.</span></span> <span data-ttu-id="76de2-134">VM durduruldu (serbest bırakıldığında) durumundan yeniden başlatıldıktan sonra bile aynı IP adresi gerektiren bir hizmeti barındırma varsa bu olası sorunlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="76de2-134">This can potentially cause issues if the VM is hosting a service that requires the same IP address, even after restarts from a stopped (deallocated) state.</span></span> <span data-ttu-id="76de2-135">Statik IP adresleri, VM silinene kadar bekletilir.</span><span class="sxs-lookup"><span data-stu-id="76de2-135">Static IP addresses are retained until the VM is deleted.</span></span> <span data-ttu-id="76de2-136">Bir IP adresi ayırma yöntemini değiştirmek için ayırma yöntemi dinamik statik olarak değiştirir aşağıdaki betiği çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="76de2-136">To change the allocation method of an IP address, run the following script, which changes the allocation method from dynamic to static.</span></span> <span data-ttu-id="76de2-137">Geçerli özel IP adresi için ayırma yöntemi statik ise, değiştirme *statik* için *dinamik* komut dosyasını çalıştırmadan önce.</span><span class="sxs-lookup"><span data-stu-id="76de2-137">If the allocation method for the current private IP address is static, change *Static* to *Dynamic* before executing the script.</span></span>

```powershell
$RG = "TestRG"
$NIC_name = "testnic1"

$nic = Get-AzureRmNetworkInterface -ResourceGroupName $RG -Name $NIC_name
$nic.IpConfigurations[0].PrivateIpAllocationMethod = 'Static'
Set-AzureRmNetworkInterface -NetworkInterface $nic 
$IP = $nic.IpConfigurations[0].PrivateIpAddress

Write-Host "The allocation method is now set to"$nic.IpConfigurations[0].PrivateIpAllocationMethod"for the IP address" $IP"." -NoNewline
```

<span data-ttu-id="76de2-138">NIC adını bilmiyorsanız, aşağıdaki komutu girerek NIC'ler listesini bir kaynak grubu içinde görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="76de2-138">If you don't know the name of the NIC, you can view a list of NICs within a resource group by entering the following command:</span></span>

```powershell
Get-AzureRmNetworkInterface -ResourceGroupName $RG | Where-Object {$_.ProvisioningState -eq 'Succeeded'} 
```

## <a name="next-steps"></a><span data-ttu-id="76de2-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="76de2-139">Next steps</span></span>
* <span data-ttu-id="76de2-140">Hakkında bilgi edinin [ayrılmış genel IP](virtual-networks-reserved-public-ip.md) adresleri.</span><span class="sxs-lookup"><span data-stu-id="76de2-140">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="76de2-141">Hakkında bilgi edinin [örnek düzeyinde ortak IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresleri.</span><span class="sxs-lookup"><span data-stu-id="76de2-141">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="76de2-142">Başvurun [ayrılmış IP REST API'leri](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="76de2-142">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

