---
title: "Benzetimli karma bulut test ortamı | Microsoft Docs"
description: "Bir sanal karma bulut ortamı için oluşturmak BT pro veya iki Azure sanal ağlar ve VNet-VNet bağlantısı kullanarak geliştirme sınama."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ca5bf294-8172-44a9-8fed-d6f38d345364
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: 4ec6f079b762a25894d822bfc098ea5442a1f7e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-simulated-hybrid-cloud-environment-for-testing"></a><span data-ttu-id="5a905-103">Test için sanal karma bulut ortamı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5a905-103">Set up a simulated hybrid cloud environment for testing</span></span>
<span data-ttu-id="5a905-104">Bu makalede Microsoft Azure iki Azure sanal ağları kullanarak bir sanal karma bulut ortamı oluşturmada size adımları.</span><span class="sxs-lookup"><span data-stu-id="5a905-104">This article steps you through creating a simulated hybrid cloud environment with Microsoft Azure using two Azure virtual networks.</span></span> <span data-ttu-id="5a905-105">Sonuçta elde edilen yapılandırma aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="5a905-105">Here is the resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="5a905-106">Bu karma bulut üretim ortamında taklit eder ve oluşur:</span><span class="sxs-lookup"><span data-stu-id="5a905-106">This simulates a hybrid cloud production environment and consists of:</span></span>

* <span data-ttu-id="5a905-107">Bir Azure sanal ağında (sınama laboratuvarı sanal ağ) barındırılan sanal ve Basitleştirilmiş şirket içi ağ.</span><span class="sxs-lookup"><span data-stu-id="5a905-107">A simulated and simplified on-premises network hosted in an Azure virtual network (the TestLab virtual network).</span></span>
* <span data-ttu-id="5a905-108">(TestVNET) Azure üzerinde barındırılan sanal şirket içi sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="5a905-108">A simulated cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="5a905-109">İki sanal ağ arasında VNet-VNet bağlantı.</span><span class="sxs-lookup"><span data-stu-id="5a905-109">A VNet-to-VNet connection between the two virtual networks.</span></span>
* <span data-ttu-id="5a905-110">TestVNET sanal ağı bir ikincil etki alanı denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="5a905-110">A secondary domain controller in the TestVNET virtual network.</span></span>

<span data-ttu-id="5a905-111">Bu, hangi yapabilecekleriniz gelen temel ve ortak başlangıç noktası sağlar:</span><span class="sxs-lookup"><span data-stu-id="5a905-111">This provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="5a905-112">Geliştirme ve uygulamaları benzetimli karma bulut ortamında test etme.</span><span class="sxs-lookup"><span data-stu-id="5a905-112">Develop and test applications in a simulated hybrid cloud environment.</span></span>
* <span data-ttu-id="5a905-113">Test yapılandırmaları bilgisayarlar, bazı sınama laboratuvarı sanal ağ içinde ve bazı karma bulut tabanlı BT iş yüklerini benzetimini yapmak için TestVNET sanal ağ içinde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5a905-113">Create test configurations of computers, some within the TestLab virtual network and some within the TestVNET virtual network, to simulate hybrid cloud-based IT workloads.</span></span>

<span data-ttu-id="5a905-114">Bu karma bulut test ortamını ayarlama için dört ana aşama vardır:</span><span class="sxs-lookup"><span data-stu-id="5a905-114">There are four major phases to setting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="5a905-115">Sınama laboratuvarı sanal ağ yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5a905-115">Configure the TestLab virtual network.</span></span>
2. <span data-ttu-id="5a905-116">Şirket içi sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5a905-116">Create the cross-premises virtual network.</span></span>
3. <span data-ttu-id="5a905-117">VNet-VNet VPN bağlantısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5a905-117">Create the VNet-to-VNet VPN connection.</span></span>
4. <span data-ttu-id="5a905-118">DC2 yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5a905-118">Configure DC2.</span></span> 

<span data-ttu-id="5a905-119">Bu yapılandırma, bir Azure aboneliği gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5a905-119">This configuration requires an Azure subscription.</span></span> <span data-ttu-id="5a905-120">Bir MSDN veya Visual Studio aboneliğiniz varsa, bkz: [Visual Studio aboneleri için aylık Azure kredi](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="5a905-120">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

> [!NOTE]
> <span data-ttu-id="5a905-121">Çalışırken sanal makineler ve sanal ağ geçitlerini azure'da devam eden bir para maliyet doğurur.</span><span class="sxs-lookup"><span data-stu-id="5a905-121">Virtual machines and virtual network gateways in Azure incur an ongoing monetary cost when they are running.</span></span> <span data-ttu-id="5a905-122">Bu maliyet, MSDN karşı faturalandırılır veya Ücretli aboneliği.</span><span class="sxs-lookup"><span data-stu-id="5a905-122">This cost is billed against your MSDN or paid subscription.</span></span> <span data-ttu-id="5a905-123">Bir Azure VPN ağ geçidi iki Azure sanal makineler kümesi olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="5a905-123">An Azure VPN gateway is implemented as a set of two Azure virtual machines.</span></span> <span data-ttu-id="5a905-124">Maliyetleri en aza indirmek için test ortamı oluşturmak ve gerekli test edip tanıtım mümkün olan en kısa sürede gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="5a905-124">To minimize the costs, create the test environment and perform your needed testing and demonstration as quickly as possible.</span></span>
> 
> 

## <a name="phase-1-configure-the-testlab-virtual-network"></a><span data-ttu-id="5a905-125">1. Aşama: sınama laboratuvarı sanal ağı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5a905-125">Phase 1: Configure the TestLab virtual network</span></span>
<span data-ttu-id="5a905-126">Konusundaki yönergeleri kullanın [temel yapılandırma test ortamı](https://technet.microsoft.com/library/mt771177.aspx) sınama laboratuvarı adlı Azure sanal ağında ead1, Uyg1 ve İSTEMCİ1 bilgisayarları yapılandırmak için konu.</span><span class="sxs-lookup"><span data-stu-id="5a905-126">Use the instructions in the [Base Configuration test environment](https://technet.microsoft.com/library/mt771177.aspx) topic to configure the DC1, APP1, and CLIENT1 computers in the Azure virtual network named TestLab.</span></span> 

<span data-ttu-id="5a905-127">Ardından, bir Azure PowerShell istemi başlatın.</span><span class="sxs-lookup"><span data-stu-id="5a905-127">Next, start an Azure PowerShell prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="5a905-128">Aşağıdaki komutu kullanın Azure PowerShell 1.0 ve daha sonra ayarlar.</span><span class="sxs-lookup"><span data-stu-id="5a905-128">The following command sets use Azure PowerShell 1.0 and later.</span></span>
> 
> 

<span data-ttu-id="5a905-129">Hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5a905-129">Sign in to your account.</span></span>

    Login-AzureRMAccount

<span data-ttu-id="5a905-130">Aşağıdaki komutu kullanarak, abonelik adını alın.</span><span class="sxs-lookup"><span data-stu-id="5a905-130">Get your subscription name using the following command.</span></span>

    Get-AzureRMSubscription | Sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="5a905-131">Azure aboneliğiniz ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5a905-131">Set your Azure subscription.</span></span> <span data-ttu-id="5a905-132">Aşama 1 temel yapılandırma oluşturmak için kullanılan aynı abonelik kullanın.</span><span class="sxs-lookup"><span data-stu-id="5a905-132">Use the same subscription that you used to build your base configuration in Phase 1.</span></span> <span data-ttu-id="5a905-133">Dahil olmak üzere tırnak işaretleri içindeki her şeyi değiştirin < ve > karakterleri doğru ada sahip.</span><span class="sxs-lookup"><span data-stu-id="5a905-133">Replace everything within the quotes, including the < and > characters, with the correct name.</span></span>

    $subscr="<subscription name>"
    Get-AzureRmSubscription –SubscriptionName $subscr | Select-AzureRmSubscription

<span data-ttu-id="5a905-134">Ardından, bir ağ geçidi alt ağı Azure ağ geçidi barındırmak için kullanılan, temel yapılandırma sınama laboratuvarı sanal ağa ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5a905-134">Next, add a gateway subnet to the TestLab virtual network of your base configuration, which will be used to host the Azure gateway.</span></span>

    $rgName="<name of your resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed the TestLab virtual network, such as West US>"
    $vnet=Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name TestLab
    Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 10.255.255.248/29 -VirtualNetwork $vnet
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet

<span data-ttu-id="5a905-135">Ardından, sınama laboratuvarı sanal ağ için ağ geçidi atamak için bir ortak IP adresi isteyin.</span><span class="sxs-lookup"><span data-stu-id="5a905-135">Next, request a public IP address to assign to the gateway for the TestLab virtual network.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestLab_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic

<span data-ttu-id="5a905-136">Ardından, ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5a905-136">Next, create your gateway.</span></span>

    $vnet=Get-AzureRmVirtualNetwork -Name TestLab -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name TestLab_GWConfig -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id 
    New-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="5a905-137">Yeni ağ geçitleri 20 dakika veya daha fazla oluşturmak için uygulayabileceğiniz göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="5a905-137">Keep in mind that new gateways can take 20 minutes or more to create.</span></span>

<span data-ttu-id="5a905-138">Yerel bilgisayarınızda Azure portalından CORP\User1 kimlik bilgileriyle DC1'e bağlanın.</span><span class="sxs-lookup"><span data-stu-id="5a905-138">From the Azure portal on your local computer, connect to DC1 with the CORP\User1 credentials.</span></span> <span data-ttu-id="5a905-139">Bilgisayarlar ve kullanıcılar kendi yerel etki alanı denetleyicisi kimlik doğrulaması için kullanabileceğiniz CORP etki alanı yapılandırmak için DC1'de bir yönetici düzeyi Windows PowerShell komut isteminde şu komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5a905-139">To configure the CORP domain so that computers and users use their local domain controller for authentication, run these commands from an administrator-level Windows PowerShell command prompt on DC1.</span></span>

    New-ADReplicationSite -Name "TestLab" 
    New-ADReplicationSite -Name "TestVNET"
    New-ADReplicationSubnet -Name "10.0.0.0/8" -Site "TestLab"
    New-ADReplicationSubnet -Name "192.168.0.0/16" -Site "TestVNET"

<span data-ttu-id="5a905-140">Bu, geçerli bir yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="5a905-140">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph1.png)

## <a name="phase-2-create-the-testvnet-virtual-network"></a><span data-ttu-id="5a905-141">2. Aşama: TestVNET sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="5a905-141">Phase 2: Create the TestVNET virtual network</span></span>
<span data-ttu-id="5a905-142">İlk olarak, TestVNET sanal ağ oluşturma ve bir ağ güvenlik grubu ile koruyun.</span><span class="sxs-lookup"><span data-stu-id="5a905-142">First, create the TestVNET virtual network and protect it with a network security group.</span></span>

    $rgName="<name of the resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed the TestLab virtual network, such as West US>"
    $locShortName="<Azure location name from $locName in all lowercase letters with spaces removed. Example:  westus>"
    $testSubnet=New-AzureRMVirtualNetworkSubnetConfig -Name "TestSubnet" -AddressPrefix 192.168.0.0/24
    $gatewaySubnet=New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 192.168.255.248/29
    New-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName -Location $locName -AddressPrefix 192.168.0.0/16 -Subnet $testSubnet,$gatewaySubnet –DNSServer 10.0.0.4
    $rule1=New-AzureRMNetworkSecurityRuleConfig -Name "RDPTraffic" -Description "Allow RDP to all VMs on the subnet" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 3389
    New-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName -Location $locShortName -SecurityRules $rule1
    $vnet=Get-AzureRMVirtualNetwork -ResourceGroupName $rgName -Name TestVNET
    $nsg=Get-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName
    Set-AzureRMVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet" -AddressPrefix 192.168.0.0/24 -NetworkSecurityGroup $nsg

<span data-ttu-id="5a905-143">Ardından, TestVNET sanal ağ için ağ geçidi için ayrılmış ve ağ geçidi oluşturmak için bir ortak IP adresi isteyin.</span><span class="sxs-lookup"><span data-stu-id="5a905-143">Next, request a public IP address to be allocated to the gateway for the TestVNET virtual network and create your gateway.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestVNET_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $vnet=Get-AzureRmVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name "TestVNET_GWConfig" -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
    New-AzureRmVirtualNetworkGateway -Name "TestVNET_GW" -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="5a905-144">Bu, geçerli bir yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="5a905-144">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph2.png)

## <a name="phase-3-create-the-vnet-to-vnet-connection"></a><span data-ttu-id="5a905-145">3. Aşama: VNet-VNet bağlantısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5a905-145">Phase 3: Create the VNet-to-VNet connection</span></span>
<span data-ttu-id="5a905-146">İlk olarak, rastgele, şifreleme açısından güçlü, 32 karakterlik önceden paylaşılan anahtar, ağ veya Güvenlik Yöneticisi'nden alın.</span><span class="sxs-lookup"><span data-stu-id="5a905-146">First, obtain a random, cryptographically strong, 32-character pre-shared key from your network or security administrator.</span></span> <span data-ttu-id="5a905-147">Alternatif olarak, bilgileri kullanmak [IPSec önceden paylaşılan anahtar için rastgele bir dize oluşturma](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) önceden paylaşılan anahtar elde edilir.</span><span class="sxs-lookup"><span data-stu-id="5a905-147">Alternately, use the information at [Create a random string for an IPsec preshared key](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) to obtain a pre-shared key.</span></span>

<span data-ttu-id="5a905-148">Ardından, tamamlanması biraz zaman alabilir VNet-VNet VPN bağlantısı oluşturmak için şu komutları kullanın.</span><span class="sxs-lookup"><span data-stu-id="5a905-148">Next, use these commands to create the VNet-to-VNet VPN connection, which can take some time to complete.</span></span>

    $sharedKey="<pre-shared key value>"
    $gwTestLab=Get-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName
    $gwTestVNET=Get-AzureRmVirtualNetworkGateway -Name TestVNET_GW -ResourceGroupName $rgName
    New-AzureRmVirtualNetworkGatewayConnection -Name TestLab_to_TestVNET -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestLab -VirtualNetworkGateway2 $gwTestVNET -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey
    New-AzureRmVirtualNetworkGatewayConnection -Name TestVNET_to_TestLab -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestVNET -VirtualNetworkGateway2 $gwTestLab -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey

<span data-ttu-id="5a905-149">Birkaç dakika sonra bağlantı kurulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5a905-149">After a few minutes, the connection should be established.</span></span>

<span data-ttu-id="5a905-150">Bu, geçerli bir yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="5a905-150">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph3.png)

## <a name="phase-4-configure-dc2"></a><span data-ttu-id="5a905-151">4. Aşama: DC2 yapılandırın</span><span class="sxs-lookup"><span data-stu-id="5a905-151">Phase 4: Configure DC2</span></span>
<span data-ttu-id="5a905-152">İlk olarak, DC2 için bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5a905-152">First, create a virtual machine for DC2.</span></span> <span data-ttu-id="5a905-153">Bu komutlar, yerel bilgisayarınızda Azure PowerShell komut isteminde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5a905-153">Run these commands at the Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<the storage account name for the base configuration>"
    $vnet=Get-AzureRMVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $pip=New-AzureRMPublicIpAddress -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -PrivateIpAddress 192.168.0.4
    $vm=New-AzureRMVMConfig -VMName DC2 -VMSize Standard_A1
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestVNET-ADDSDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name ADDS-Data -DiskSizeInGB 20 -VhdUri $vhdURI  -CreateOption empty
    $cred=Get-Credential -Message "Type the name and password of the local administrator account for DC2."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName DC2 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name DC2-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="5a905-154">Ardından, Azure portalından yeni DC2 sanal makineye bağlanın.</span><span class="sxs-lookup"><span data-stu-id="5a905-154">Next, connect to the new DC2 virtual machine from the Azure portal.</span></span>

<span data-ttu-id="5a905-155">Ardından, bir Windows Güvenlik duvarı kuralı temel bağlantıyı test etmek için trafiğe izin verecek şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5a905-155">Next, configure a Windows Firewall rule to allow traffic for basic connectivity testing.</span></span> <span data-ttu-id="5a905-156">Bir yönetici düzeyi Windows PowerShell komut isteminde DC2'de, bu komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5a905-156">From an administrator-level Windows PowerShell command prompt on DC2, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc1.corp.contoso.com

<span data-ttu-id="5a905-157">Ping komutu 10.0.0.4 IP adresinden dört başarılı yanıt neden olur.</span><span class="sxs-lookup"><span data-stu-id="5a905-157">The ping command should result in four successful replies from IP address 10.0.0.4.</span></span> <span data-ttu-id="5a905-158">VNet-VNet bağlantısı üzerinden trafik test budur.</span><span class="sxs-lookup"><span data-stu-id="5a905-158">This is a test of traffic across the VNet-to-VNet connection.</span></span>

<span data-ttu-id="5a905-159">Sonra ek veri diski DC2'de sürücü harfi F: olan yeni bir birim olarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5a905-159">Next, add the extra data disk on DC2 as a new volume with the drive letter F:.</span></span>

1. <span data-ttu-id="5a905-160">Sunucu Yöneticisi'nin sol bölmesinde, **dosya ve depolama hizmetleri**ve ardından **diskleri**.</span><span class="sxs-lookup"><span data-stu-id="5a905-160">In the left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="5a905-161">İçerik bölmesinde içinde **diskleri** grubunda **disk 2** (ile **bölüm** kümesine **bilinmeyen**).</span><span class="sxs-lookup"><span data-stu-id="5a905-161">In the contents pane, in the **Disks** group, click **disk 2** (with the **Partition** set to **Unknown**).</span></span>
3. <span data-ttu-id="5a905-162">Tıklatın **görevleri**ve ardından **yeni birim**.</span><span class="sxs-lookup"><span data-stu-id="5a905-162">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="5a905-163">Önce üzerinde yeni birim Sihirbazı sayfasında başlayan, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5a905-163">On the Before you begin page of the New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="5a905-164">Sunucu ve disk sayfa Seç'i tıklatın **Disk 2**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5a905-164">On the Select the server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="5a905-165">İstendiğinde, tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="5a905-165">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="5a905-166">Birimin boyutunu belirtin sayfasında tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5a905-166">On the Specify the size of the volume page, click **Next**.</span></span>
7. <span data-ttu-id="5a905-167">Bir sürücü harfi veya klasörü sayfasına Ata hakkında'yı tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5a905-167">On the Assign to a drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="5a905-168">Dosya Seç Sistem Ayarları sayfasında, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5a905-168">On the Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="5a905-169">Seçimlerini onaylayın sayfasında, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="5a905-169">On the Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="5a905-170">Tamamlandığında, tıklayın **Kapat**.</span><span class="sxs-lookup"><span data-stu-id="5a905-170">When complete, click **Close**.</span></span>

<span data-ttu-id="5a905-171">Ardından, DC2 corp.contoso.com etki alanında kopya etki alanı denetleyicisi olarak yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5a905-171">Next, configure DC2 as a replica domain controller for the corp.contoso.com domain.</span></span> <span data-ttu-id="5a905-172">Bu komutlar DC2'de Windows PowerShell komut isteminden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5a905-172">Run these commands from the Windows PowerShell command prompt on DC2.</span></span>

    Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
    Install-ADDSDomainController -Credential (Get-Credential CORP\User1) -DomainName "corp.contoso.com" -InstallDns:$true -DatabasePath "F:\NTDS" -LogPath "F:\Logs" -SysvolPath "F:\SYSVOL"

<span data-ttu-id="5a905-173">Not CORP\User1 parola ve Dizin Hizmetleri Geri Yükleme Modu'nda (DSRM) parolasını sağlamanız ve DC2 yeniden başlatmanız istenir.</span><span class="sxs-lookup"><span data-stu-id="5a905-173">Note that you are prompted to supply both the CORP\User1 password and a Directory Services Restore Mode (DSRM) password, and to restart DC2.</span></span>

<span data-ttu-id="5a905-174">Kendi DNS sunucusuna (DC2) TestVNET sanal ağı sahiptir, bu DNS sunucusu kullanacak şekilde TestVNET sanal ağ yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5a905-174">Now that the TestVNET virtual network has its own DNS server (DC2), you must configure the TestVNET virtual network to use this DNS server.</span></span>

1. <span data-ttu-id="5a905-175">Azure portalının sol bölmede, sanal ağlar simgesine tıklayın ve ardından **TestVNET**.</span><span class="sxs-lookup"><span data-stu-id="5a905-175">In the left pane of the Azure portal, click the virtual networks icon, and then click **TestVNET**.</span></span>
2. <span data-ttu-id="5a905-176">Üzerinde **ayarları** sekmesini tıklatın, **DNS sunucuları**.</span><span class="sxs-lookup"><span data-stu-id="5a905-176">On the **Settings** tab, click **DNS servers**.</span></span>
3. <span data-ttu-id="5a905-177">İçinde **birincil DNS sunucusu**, türü **192.168.0.4** 10.0.0.4 değiştirmek için.</span><span class="sxs-lookup"><span data-stu-id="5a905-177">In **Primary DNS server**, type **192.168.0.4** to replace 10.0.0.4.</span></span>
4. <span data-ttu-id="5a905-178">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5a905-178">Click **Save**.</span></span>

<span data-ttu-id="5a905-179">Bu, geçerli bir yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="5a905-179">This is your current configuration.</span></span> 

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="5a905-180">Benzetimli karma bulut ortamınızı artık test etmek için hazırdır.</span><span class="sxs-lookup"><span data-stu-id="5a905-180">Your simulated hybrid cloud environment is now ready for testing.</span></span>

## <a name="next-step"></a><span data-ttu-id="5a905-181">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="5a905-181">Next step</span></span>
* <span data-ttu-id="5a905-182">Ayarlanmış bir [web tabanlı, iş hattı uygulaması](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Bu ortamdaki.</span><span class="sxs-lookup"><span data-stu-id="5a905-182">Set up a [web-based, line of business application](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in this environment.</span></span>

