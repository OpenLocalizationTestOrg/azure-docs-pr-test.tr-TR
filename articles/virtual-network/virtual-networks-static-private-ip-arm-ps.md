---
title: "aaaConfigure özel IP adresleri VM'ler - Azure PowerShell | Microsoft Docs"
description: "PowerShell kullanarak sanal makineleri için nasıl tooconfigure özel IP adresleri öğrenin."
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
ms.openlocfilehash: 4a3eb67de583e08208fcab40de1c2a8a9b65618c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-powershell"></a><span data-ttu-id="75a34-103">PowerShell kullanarak bir sanal makine için özel IP adreslerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="75a34-103">Configure private IP addresses for a virtual machine using PowerShell</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

<span data-ttu-id="75a34-104">Azure'un iki dağıtım modeli vardır: Azure Resource Manager ve klasik.</span><span class="sxs-lookup"><span data-stu-id="75a34-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="75a34-105">Microsoft, kaynakları hello Resource Manager dağıtım modeli üzerinden oluşturma önerir.</span><span class="sxs-lookup"><span data-stu-id="75a34-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="75a34-106">Merhaba iki modelleri arasındaki farklar hakkında daha fazla bilgi toolearn hello okuma hello [anlamak Azure dağıtım modelleri](../azure-resource-manager/resource-manager-deployment-model.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="75a34-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="75a34-107">Bu makalede, hello Resource Manager dağıtım modeli yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="75a34-107">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="75a34-108">Ayrıca [hello Klasik dağıtım modelinde statik özel IP adresi yönetmek](virtual-networks-static-private-ip-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="75a34-108">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="75a34-109">Merhaba örnek PowerShell önceden oluşturulmuş basit bir ortam aşağıdaki komutları beklediğiniz senaryosunda hello yukarıdaki temel.</span><span class="sxs-lookup"><span data-stu-id="75a34-109">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="75a34-110">Bu belgede gösterildiği toorun hello komutları istiyorsanız, ilk derleme açıklanan hello test ortamı [vnet oluşturma](virtual-networks-create-vnet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="75a34-110">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-ps.md).</span></span>

## <a name="create-a-vm-with-a-static-private-ip-address"></a><span data-ttu-id="75a34-111">Statik özel IP adresiyle VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="75a34-111">Create a VM with a static private IP address</span></span>
<span data-ttu-id="75a34-112">toocreate adlı bir VM'den *DNS01* hello içinde *ön uç* adlı bir sanal ağ alt ağı *TestVNet* özel bir statik IP *192.168.1.101*, Merhaba adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="75a34-112">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="75a34-113">Merhaba depolama hesabı, konumu, kaynak grubu ve kullanılan kimlik bilgileri toobe değişkenleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="75a34-113">Set variables for hello storage account, location, resource group, and credentials toobe used.</span></span> <span data-ttu-id="75a34-114">Merhaba VM tooenter bir kullanıcı adı ve parola gerekir.</span><span class="sxs-lookup"><span data-stu-id="75a34-114">You will need tooenter a user name and password for hello VM.</span></span> <span data-ttu-id="75a34-115">Merhaba depolama hesabı ve kaynak grubu zaten mevcut olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="75a34-115">hello storage account and resource group must already exist.</span></span>

    ```powershell
    $stName  = "vnetstorage"
    $locName = "Central US"
    $rgName  = "TestRG"
    $cred    = Get-Credential -Message "Type hello name and password of hello local administrator account."
    ```

2. <span data-ttu-id="75a34-116">Alma hello sanal ağ ve alt toocreate istediğiniz VM ile Merhaba.</span><span class="sxs-lookup"><span data-stu-id="75a34-116">Retrieve hello virtual network and subnet you want toocreate hello VM in.</span></span>

    ```powershell
    $vnet   = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    $subnet = $vnet.Subnets[0].Id
    ```

3. <span data-ttu-id="75a34-117">Gerekirse, bir ortak IP adresi tooaccess hello VM Internet hello oluşturun.</span><span class="sxs-lookup"><span data-stu-id="75a34-117">If necessary, create a public IP address tooaccess hello VM from hello Internet.</span></span>

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name TestPIP -ResourceGroupName $rgName `
    -Location $locName -AllocationMethod Dynamic
    ```

4. <span data-ttu-id="75a34-118">Tooassign toohello VM istediğiniz hello statik özel IP adresini kullanarak bir NIC oluşturun.</span><span class="sxs-lookup"><span data-stu-id="75a34-118">Create a NIC using hello static private IP address you want tooassign toohello VM.</span></span> <span data-ttu-id="75a34-119">Emin hello IP olduğu eklemekte olduğunuz hello alt ağı aralığından hello VM olun.</span><span class="sxs-lookup"><span data-stu-id="75a34-119">Make sure hello IP is from hello subnet range you are adding hello VM to.</span></span> <span data-ttu-id="75a34-120">Bu hello ana hello özel IP toobe statik ayarladığınız Bu makale için bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="75a34-120">This is hello main step for this article, where you set hello private IP toobe static.</span></span>

    ```powershell
    $nic = New-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName $rgName `
    -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id `
    -PrivateIpAddress 192.168.1.101
    ```

5. <span data-ttu-id="75a34-121">Merhaba NIC kullanarak VM yukarıda oluşturduğunuz hello oluşturun.</span><span class="sxs-lookup"><span data-stu-id="75a34-121">Create hello VM using hello NIC created above.</span></span>

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

    <span data-ttu-id="75a34-122">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="75a34-122">Expected output:</span></span>
    
        EndTime             : [Date and time]
        Error               : 
        Output              : 
        StartTime           : [Date and time]
        Status              : Succeeded
        TrackingOperationId : [Id]
        RequestId           : [Id]
        StatusCode          : OK 

## <a name="retrieve-static-private-ip-address-information-for-a-network-interface"></a><span data-ttu-id="75a34-123">Bir ağ arabirimi için özel statik IP adresi bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="75a34-123">Retrieve static private IP address information for a network interface</span></span>
<span data-ttu-id="75a34-124">tooview hello statik özel IP adres bilgilerinin hello için VM oluşturulan yukarıdaki hello komut dosyasıyla hello aşağıdaki PowerShell komutunu çalıştırın ve başlangıç değerleri uyun *PrivateIpAddress* ve  *Privateıpallocationmethod*:</span><span class="sxs-lookup"><span data-stu-id="75a34-124">tooview hello static private IP address information for hello VM created with hello script above, run hello following PowerShell command and observe hello values for *PrivateIpAddress* and *PrivateIpAllocationMethod*:</span></span>

```powershell
Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
```

<span data-ttu-id="75a34-125">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="75a34-125">Expected output:</span></span>

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

## <a name="remove-a-static-private-ip-address-from-a-network-interface"></a><span data-ttu-id="75a34-126">Özel bir statik IP adresi bir ağ arabiriminden Kaldır</span><span class="sxs-lookup"><span data-stu-id="75a34-126">Remove a static private IP address from a network interface</span></span>
<span data-ttu-id="75a34-127">tooremove hello statik özel IP adresi toohello VM üzerinde aşağıdaki PowerShell komutlarını çalıştırma hello hello betikteki eklendi:</span><span class="sxs-lookup"><span data-stu-id="75a34-127">tooremove hello static private IP address added toohello VM in hello script above, run hello following PowerShell commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Dynamic"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="75a34-128">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="75a34-128">Expected output:</span></span>

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

## <a name="add-a-static-private-ip-address-tooa-network-interface"></a><span data-ttu-id="75a34-129">Statik özel IP adresi tooa ağ arabirimi ekleyin</span><span class="sxs-lookup"><span data-stu-id="75a34-129">Add a static private IP address tooa network interface</span></span>
<span data-ttu-id="75a34-130">tooadd bir statik özel IP adresi toohello hello betik yukarıdaki kullanılarak oluşturulan VM hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="75a34-130">tooadd a static private IP address toohello VM created using hello script above, run hello following commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Static"
$nic.IpConfigurations[0].PrivateIpAddress = "192.168.1.101"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```
## <a name="change-hello-allocation-method-for-a-private-ip-address-assigned-tooa-network-interface"></a><span data-ttu-id="75a34-131">Tooa ağ arabirimine atanmış bir özel IP adresi için Hello ayırma yöntemini değiştirin</span><span class="sxs-lookup"><span data-stu-id="75a34-131">Change hello allocation method for a private IP address assigned tooa network interface</span></span>

<span data-ttu-id="75a34-132">Özel bir IP adresi tooa NIC hello statik veya dinamik ayırma yöntemiyle atanır.</span><span class="sxs-lookup"><span data-stu-id="75a34-132">A private IP address is assigned tooa NIC with hello static or dynamic allocation method.</span></span> <span data-ttu-id="75a34-133">Dinamik IP adreslerini hello öncekinden VM başlatma durduruldu (serbest bırakıldığında) durumu sonra değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75a34-133">Dynamic IP addresses can change after starting a VM that was previously in hello stopped (deallocated) state.</span></span> <span data-ttu-id="75a34-134">Merhaba VM hello gerektiren bir hizmeti barındırma varsa bu olası sorunlara neden olabilir durduruldu (serbest bırakıldığında) durumundan yeniden başlatıldıktan sonra bile aynı IP adresi.</span><span class="sxs-lookup"><span data-stu-id="75a34-134">This can potentially cause issues if hello VM is hosting a service that requires hello same IP address, even after restarts from a stopped (deallocated) state.</span></span> <span data-ttu-id="75a34-135">Statik IP adresleri Hello VM silinene kadar bekletilir.</span><span class="sxs-lookup"><span data-stu-id="75a34-135">Static IP addresses are retained until hello VM is deleted.</span></span> <span data-ttu-id="75a34-136">toochange hello ayırma yöntemi hello ayırma yöntemi dinamik toostatic değişiklikler komut dosyası izleyen hello çalıştırmak bir IP adresi.</span><span class="sxs-lookup"><span data-stu-id="75a34-136">toochange hello allocation method of an IP address, run hello following script, which changes hello allocation method from dynamic toostatic.</span></span> <span data-ttu-id="75a34-137">Merhaba ayırma yöntemi hello geçerli özel IP adresi statik ise değiştirmek *statik* çok*dinamik* hello betiği çalıştırmadan önce.</span><span class="sxs-lookup"><span data-stu-id="75a34-137">If hello allocation method for hello current private IP address is static, change *Static* too*Dynamic* before executing hello script.</span></span>

```powershell
$RG = "TestRG"
$NIC_name = "testnic1"

$nic = Get-AzureRmNetworkInterface -ResourceGroupName $RG -Name $NIC_name
$nic.IpConfigurations[0].PrivateIpAllocationMethod = 'Static'
Set-AzureRmNetworkInterface -NetworkInterface $nic 
$IP = $nic.IpConfigurations[0].PrivateIpAddress

Write-Host "hello allocation method is now set to"$nic.IpConfigurations[0].PrivateIpAllocationMethod"for hello IP address" $IP"." -NoNewline
```

<span data-ttu-id="75a34-138">Merhaba NIC hello adını bilmiyorsanız, komutu aşağıdaki hello girerek NIC'ler listesini bir kaynak grubu içinde görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="75a34-138">If you don't know hello name of hello NIC, you can view a list of NICs within a resource group by entering hello following command:</span></span>

```powershell
Get-AzureRmNetworkInterface -ResourceGroupName $RG | Where-Object {$_.ProvisioningState -eq 'Succeeded'} 
```

## <a name="next-steps"></a><span data-ttu-id="75a34-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="75a34-139">Next steps</span></span>
* <span data-ttu-id="75a34-140">Hakkında bilgi edinin [ayrılmış genel IP](virtual-networks-reserved-public-ip.md) adresleri.</span><span class="sxs-lookup"><span data-stu-id="75a34-140">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="75a34-141">Hakkında bilgi edinin [örnek düzeyinde ortak IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresleri.</span><span class="sxs-lookup"><span data-stu-id="75a34-141">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="75a34-142">Merhaba başvurun [ayrılmış IP REST API'leri](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="75a34-142">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

