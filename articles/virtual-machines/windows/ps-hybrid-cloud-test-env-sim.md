---
title: "aaaSimulated karma bulut test ortamı | Microsoft Docs"
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
ms.openlocfilehash: 6063022e373c2b3564e040c4fbee122e2438974b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-simulated-hybrid-cloud-environment-for-testing"></a><span data-ttu-id="41df6-103">Test için sanal karma bulut ortamı oluşturma</span><span class="sxs-lookup"><span data-stu-id="41df6-103">Set up a simulated hybrid cloud environment for testing</span></span>
<span data-ttu-id="41df6-104">Bu makalede Microsoft Azure iki Azure sanal ağları kullanarak bir sanal karma bulut ortamı oluşturmada size adımları.</span><span class="sxs-lookup"><span data-stu-id="41df6-104">This article steps you through creating a simulated hybrid cloud environment with Microsoft Azure using two Azure virtual networks.</span></span> <span data-ttu-id="41df6-105">Merhaba sonuçta elde edilen yapılandırma aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="41df6-105">Here is hello resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="41df6-106">Bu karma bulut üretim ortamında taklit eder ve oluşur:</span><span class="sxs-lookup"><span data-stu-id="41df6-106">This simulates a hybrid cloud production environment and consists of:</span></span>

* <span data-ttu-id="41df6-107">Bir Azure sanal ağında (Merhaba sınama laboratuvarı sanal ağ) barındırılan sanal ve Basitleştirilmiş şirket içi ağ.</span><span class="sxs-lookup"><span data-stu-id="41df6-107">A simulated and simplified on-premises network hosted in an Azure virtual network (hello TestLab virtual network).</span></span>
* <span data-ttu-id="41df6-108">(TestVNET) Azure üzerinde barındırılan sanal şirket içi sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="41df6-108">A simulated cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="41df6-109">Merhaba iki sanal ağlar arasında VNet-VNet bağlantı.</span><span class="sxs-lookup"><span data-stu-id="41df6-109">A VNet-to-VNet connection between hello two virtual networks.</span></span>
* <span data-ttu-id="41df6-110">Merhaba TestVNET sanal ağ bir ikincil etki alanı denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="41df6-110">A secondary domain controller in hello TestVNET virtual network.</span></span>

<span data-ttu-id="41df6-111">Bu, hangi yapabilecekleriniz gelen temel ve ortak başlangıç noktası sağlar:</span><span class="sxs-lookup"><span data-stu-id="41df6-111">This provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="41df6-112">Geliştirme ve uygulamaları benzetimli karma bulut ortamında test etme.</span><span class="sxs-lookup"><span data-stu-id="41df6-112">Develop and test applications in a simulated hybrid cloud environment.</span></span>
* <span data-ttu-id="41df6-113">Test yapılandırmaları bilgisayarlar, bazı hello sınama laboratuvarı sanal ağ içinde ve bazı hello TestVNET sanal ağ, toosimulate karma bulut tabanlı BT iş yüklerini içinde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41df6-113">Create test configurations of computers, some within hello TestLab virtual network and some within hello TestVNET virtual network, toosimulate hybrid cloud-based IT workloads.</span></span>

<span data-ttu-id="41df6-114">Bu karma bulut test ortamını oluşturan dört ana aşamaları toosetting vardır:</span><span class="sxs-lookup"><span data-stu-id="41df6-114">There are four major phases toosetting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="41df6-115">Merhaba sınama laboratuvarı sanal ağ yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="41df6-115">Configure hello TestLab virtual network.</span></span>
2. <span data-ttu-id="41df6-116">Merhaba şirket içi sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41df6-116">Create hello cross-premises virtual network.</span></span>
3. <span data-ttu-id="41df6-117">Merhaba VNet-VNet VPN bağlantısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41df6-117">Create hello VNet-to-VNet VPN connection.</span></span>
4. <span data-ttu-id="41df6-118">DC2 yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="41df6-118">Configure DC2.</span></span> 

<span data-ttu-id="41df6-119">Bu yapılandırma, bir Azure aboneliği gerektirir.</span><span class="sxs-lookup"><span data-stu-id="41df6-119">This configuration requires an Azure subscription.</span></span> <span data-ttu-id="41df6-120">Bir MSDN veya Visual Studio aboneliğiniz varsa, bkz: [Visual Studio aboneleri için aylık Azure kredi](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="41df6-120">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

> [!NOTE]
> <span data-ttu-id="41df6-121">Çalışırken sanal makineler ve sanal ağ geçitlerini azure'da devam eden bir para maliyet doğurur.</span><span class="sxs-lookup"><span data-stu-id="41df6-121">Virtual machines and virtual network gateways in Azure incur an ongoing monetary cost when they are running.</span></span> <span data-ttu-id="41df6-122">Bu maliyet, MSDN karşı faturalandırılır veya Ücretli aboneliği.</span><span class="sxs-lookup"><span data-stu-id="41df6-122">This cost is billed against your MSDN or paid subscription.</span></span> <span data-ttu-id="41df6-123">Bir Azure VPN ağ geçidi iki Azure sanal makineler kümesi olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="41df6-123">An Azure VPN gateway is implemented as a set of two Azure virtual machines.</span></span> <span data-ttu-id="41df6-124">toominimize hello maliyetleri hello test ortamı oluşturmak ve gerekli test edip tanıtım mümkün olan en kısa sürede gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="41df6-124">toominimize hello costs, create hello test environment and perform your needed testing and demonstration as quickly as possible.</span></span>
> 
> 

## <a name="phase-1-configure-hello-testlab-virtual-network"></a><span data-ttu-id="41df6-125">1. Aşama: hello sınama laboratuvarı sanal ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="41df6-125">Phase 1: Configure hello TestLab virtual network</span></span>
<span data-ttu-id="41df6-126">Hello Hello yönergeleri kullanın [temel yapılandırma test ortamı](https://technet.microsoft.com/library/mt771177.aspx) konu tooconfigure hello ead1, Uyg1 ve İSTEMCİ1 bilgisayarların hello sınama laboratuvarı adlı Azure sanal ağı.</span><span class="sxs-lookup"><span data-stu-id="41df6-126">Use hello instructions in hello [Base Configuration test environment](https://technet.microsoft.com/library/mt771177.aspx) topic tooconfigure hello DC1, APP1, and CLIENT1 computers in hello Azure virtual network named TestLab.</span></span> 

<span data-ttu-id="41df6-127">Ardından, bir Azure PowerShell istemi başlatın.</span><span class="sxs-lookup"><span data-stu-id="41df6-127">Next, start an Azure PowerShell prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="41df6-128">Aşağıdaki komut kümelerini hello Azure PowerShell 1.0 ve sonrasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="41df6-128">hello following command sets use Azure PowerShell 1.0 and later.</span></span>
> 
> 

<span data-ttu-id="41df6-129">Tooyour hesabında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="41df6-129">Sign in tooyour account.</span></span>

    Login-AzureRMAccount

<span data-ttu-id="41df6-130">Merhaba aşağıdaki komutu kullanarak, abonelik adını alın.</span><span class="sxs-lookup"><span data-stu-id="41df6-130">Get your subscription name using hello following command.</span></span>

    Get-AzureRMSubscription | Sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="41df6-131">Azure aboneliğiniz ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="41df6-131">Set your Azure subscription.</span></span> <span data-ttu-id="41df6-132">Kullanım hello aynı abonelik Aşama 1'de, temel yapılandırma toobuild kullanılır.</span><span class="sxs-lookup"><span data-stu-id="41df6-132">Use hello same subscription that you used toobuild your base configuration in Phase 1.</span></span> <span data-ttu-id="41df6-133">Merhaba < ve > karakterleri dahil olmak üzere hello tırnak içindeki her şeyi hello doğru adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="41df6-133">Replace everything within hello quotes, including hello < and > characters, with hello correct name.</span></span>

    $subscr="<subscription name>"
    Get-AzureRmSubscription –SubscriptionName $subscr | Select-AzureRmSubscription

<span data-ttu-id="41df6-134">Ardından, bir ağ geçidi alt ağı toohello sınama laboratuvarı sanal ağ kullanılan toohost hello Azure ağ geçidi olacaktır, temel yapılandırma ekleyin.</span><span class="sxs-lookup"><span data-stu-id="41df6-134">Next, add a gateway subnet toohello TestLab virtual network of your base configuration, which will be used toohost hello Azure gateway.</span></span>

    $rgName="<name of your resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $vnet=Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name TestLab
    Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 10.255.255.248/29 -VirtualNetwork $vnet
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet

<span data-ttu-id="41df6-135">Ardından, bir ortak IP adresi tooassign toohello ağ geçidi hello sınama laboratuvarı sanal ağ için istek.</span><span class="sxs-lookup"><span data-stu-id="41df6-135">Next, request a public IP address tooassign toohello gateway for hello TestLab virtual network.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestLab_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic

<span data-ttu-id="41df6-136">Ardından, ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41df6-136">Next, create your gateway.</span></span>

    $vnet=Get-AzureRmVirtualNetwork -Name TestLab -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name TestLab_GWConfig -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id 
    New-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="41df6-137">Yeni ağ geçitleri 20 dakika veya daha fazla toocreate sürebilir göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="41df6-137">Keep in mind that new gateways can take 20 minutes or more toocreate.</span></span>

<span data-ttu-id="41df6-138">Azure portal, yerel bilgisayarınızda Hello tooDC1 hello CORP\User1 kimlik bilgileriyle bağlayın.</span><span class="sxs-lookup"><span data-stu-id="41df6-138">From hello Azure portal on your local computer, connect tooDC1 with hello CORP\User1 credentials.</span></span> <span data-ttu-id="41df6-139">tooconfigure hello CORP etki alanı bilgisayarlar ve kullanıcılar kendi yerel etki alanı denetleyicisi kimlik doğrulaması için kullanabileceğiniz çalıştırın Bu komutlar bir yönetici düzeyi Windows PowerShell komut isteminde DC1'de.</span><span class="sxs-lookup"><span data-stu-id="41df6-139">tooconfigure hello CORP domain so that computers and users use their local domain controller for authentication, run these commands from an administrator-level Windows PowerShell command prompt on DC1.</span></span>

    New-ADReplicationSite -Name "TestLab" 
    New-ADReplicationSite -Name "TestVNET"
    New-ADReplicationSubnet -Name "10.0.0.0/8" -Site "TestLab"
    New-ADReplicationSubnet -Name "192.168.0.0/16" -Site "TestVNET"

<span data-ttu-id="41df6-140">Bu, geçerli bir yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="41df6-140">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph1.png)

## <a name="phase-2-create-hello-testvnet-virtual-network"></a><span data-ttu-id="41df6-141">2. Aşama: Merhaba TestVNET sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="41df6-141">Phase 2: Create hello TestVNET virtual network</span></span>
<span data-ttu-id="41df6-142">İlk olarak, hello TestVNET sanal ağ oluşturma ve bir ağ güvenlik grubu ile koruyun.</span><span class="sxs-lookup"><span data-stu-id="41df6-142">First, create hello TestVNET virtual network and protect it with a network security group.</span></span>

    $rgName="<name of hello resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $locShortName="<Azure location name from $locName in all lowercase letters with spaces removed. Example:  westus>"
    $testSubnet=New-AzureRMVirtualNetworkSubnetConfig -Name "TestSubnet" -AddressPrefix 192.168.0.0/24
    $gatewaySubnet=New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 192.168.255.248/29
    New-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName -Location $locName -AddressPrefix 192.168.0.0/16 -Subnet $testSubnet,$gatewaySubnet –DNSServer 10.0.0.4
    $rule1=New-AzureRMNetworkSecurityRuleConfig -Name "RDPTraffic" -Description "Allow RDP tooall VMs on hello subnet" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 3389
    New-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName -Location $locShortName -SecurityRules $rule1
    $vnet=Get-AzureRMVirtualNetwork -ResourceGroupName $rgName -Name TestVNET
    $nsg=Get-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName
    Set-AzureRMVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet" -AddressPrefix 192.168.0.0/24 -NetworkSecurityGroup $nsg

<span data-ttu-id="41df6-143">Ardından, istek bir ortak IP adresi toobe toohello ağ geçidi hello TestVNET sanal ağ için ayrılan ve ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41df6-143">Next, request a public IP address toobe allocated toohello gateway for hello TestVNET virtual network and create your gateway.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestVNET_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $vnet=Get-AzureRmVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name "TestVNET_GWConfig" -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
    New-AzureRmVirtualNetworkGateway -Name "TestVNET_GW" -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="41df6-144">Bu, geçerli bir yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="41df6-144">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph2.png)

## <a name="phase-3-create-hello-vnet-to-vnet-connection"></a><span data-ttu-id="41df6-145">3. Aşama: Merhaba VNet-VNet bağlantısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="41df6-145">Phase 3: Create hello VNet-to-VNet connection</span></span>
<span data-ttu-id="41df6-146">İlk olarak, rastgele, şifreleme açısından güçlü, 32 karakterlik önceden paylaşılan anahtar, ağ veya Güvenlik Yöneticisi'nden alın.</span><span class="sxs-lookup"><span data-stu-id="41df6-146">First, obtain a random, cryptographically strong, 32-character pre-shared key from your network or security administrator.</span></span> <span data-ttu-id="41df6-147">Alternatif olarak, hello bilgileri kullanmak [IPSec önceden paylaşılan anahtar için rastgele bir dize oluşturma](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) tooobtain önceden paylaşılan anahtar.</span><span class="sxs-lookup"><span data-stu-id="41df6-147">Alternately, use hello information at [Create a random string for an IPsec preshared key](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) tooobtain a pre-shared key.</span></span>

<span data-ttu-id="41df6-148">Ardından, bazı zaman toocomplete sürebilir bu komutları toocreate hello VNet-VNet VPN bağlantısı kullanın.</span><span class="sxs-lookup"><span data-stu-id="41df6-148">Next, use these commands toocreate hello VNet-to-VNet VPN connection, which can take some time toocomplete.</span></span>

    $sharedKey="<pre-shared key value>"
    $gwTestLab=Get-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName
    $gwTestVNET=Get-AzureRmVirtualNetworkGateway -Name TestVNET_GW -ResourceGroupName $rgName
    New-AzureRmVirtualNetworkGatewayConnection -Name TestLab_to_TestVNET -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestLab -VirtualNetworkGateway2 $gwTestVNET -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey
    New-AzureRmVirtualNetworkGatewayConnection -Name TestVNET_to_TestLab -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestVNET -VirtualNetworkGateway2 $gwTestLab -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey

<span data-ttu-id="41df6-149">Birkaç dakika sonra hello bağlantı kurulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="41df6-149">After a few minutes, hello connection should be established.</span></span>

<span data-ttu-id="41df6-150">Bu, geçerli bir yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="41df6-150">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph3.png)

## <a name="phase-4-configure-dc2"></a><span data-ttu-id="41df6-151">4. Aşama: DC2 yapılandırın</span><span class="sxs-lookup"><span data-stu-id="41df6-151">Phase 4: Configure DC2</span></span>
<span data-ttu-id="41df6-152">İlk olarak, DC2 için bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41df6-152">First, create a virtual machine for DC2.</span></span> <span data-ttu-id="41df6-153">Bu komutlar, yerel bilgisayarınızda hello Azure PowerShell komut isteminde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="41df6-153">Run these commands at hello Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<hello storage account name for hello base configuration>"
    $vnet=Get-AzureRMVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $pip=New-AzureRMPublicIpAddress -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -PrivateIpAddress 192.168.0.4
    $vm=New-AzureRMVMConfig -VMName DC2 -VMSize Standard_A1
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestVNET-ADDSDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name ADDS-Data -DiskSizeInGB 20 -VhdUri $vhdURI  -CreateOption empty
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for DC2."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName DC2 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name DC2-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="41df6-154">Ardından, toohello yeni DC2 sanal makine hello Azure portal ' bağlayın.</span><span class="sxs-lookup"><span data-stu-id="41df6-154">Next, connect toohello new DC2 virtual machine from hello Azure portal.</span></span>

<span data-ttu-id="41df6-155">Ardından, temel bağlantıyı test etmek için bir Windows Güvenlik duvarı kuralı tooallow trafiği yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="41df6-155">Next, configure a Windows Firewall rule tooallow traffic for basic connectivity testing.</span></span> <span data-ttu-id="41df6-156">Bir yönetici düzeyi Windows PowerShell komut isteminde DC2'de, bu komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="41df6-156">From an administrator-level Windows PowerShell command prompt on DC2, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc1.corp.contoso.com

<span data-ttu-id="41df6-157">Merhaba ping komutu 10.0.0.4 IP adresinden dört başarılı yanıt neden olur.</span><span class="sxs-lookup"><span data-stu-id="41df6-157">hello ping command should result in four successful replies from IP address 10.0.0.4.</span></span> <span data-ttu-id="41df6-158">Merhaba VNet-VNet bağlantısı trafik test budur.</span><span class="sxs-lookup"><span data-stu-id="41df6-158">This is a test of traffic across hello VNet-to-VNet connection.</span></span>

<span data-ttu-id="41df6-159">Ardından, hello eklemek DC2'hello sürücü harfi F: olan yeni bir birim olarak ek veri diski.</span><span class="sxs-lookup"><span data-stu-id="41df6-159">Next, add hello extra data disk on DC2 as a new volume with hello drive letter F:.</span></span>

1. <span data-ttu-id="41df6-160">Merhaba sol bölmesinde Sunucu Yöneticisi'nin, **dosya ve depolama hizmetleri**ve ardından **diskleri**.</span><span class="sxs-lookup"><span data-stu-id="41df6-160">In hello left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="41df6-161">Merhaba içeriği bölmesinde hello **diskleri** grubunda **disk 2** (Merhaba ile **bölüm** çok ayarlamak**bilinmeyen**).</span><span class="sxs-lookup"><span data-stu-id="41df6-161">In hello contents pane, in hello **Disks** group, click **disk 2** (with hello **Partition** set too**Unknown**).</span></span>
3. <span data-ttu-id="41df6-162">Tıklatın **görevleri**ve ardından **yeni birim**.</span><span class="sxs-lookup"><span data-stu-id="41df6-162">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="41df6-163">Merhaba Yeni Birim Sihirbazı sayfasında başlamadan önce üzerinde Hello tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="41df6-163">On hello Before you begin page of hello New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="41df6-164">Merhaba Select hello sunucu ve disk sayfasında tıklatın **Disk 2**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="41df6-164">On hello Select hello server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="41df6-165">İstendiğinde, tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="41df6-165">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="41df6-166">Hello hello birim sayfasının hello boyut belirtin, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="41df6-166">On hello Specify hello size of hello volume page, click **Next**.</span></span>
7. <span data-ttu-id="41df6-167">Merhaba Ata tooa sürücü harfi veya klasörü sayfasında, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="41df6-167">On hello Assign tooa drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="41df6-168">Merhaba Select dosya sistemi Ayarları sayfasında, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="41df6-168">On hello Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="41df6-169">Merhaba seçimlerini onaylayın sayfasında, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="41df6-169">On hello Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="41df6-170">Tamamlandığında, tıklayın **Kapat**.</span><span class="sxs-lookup"><span data-stu-id="41df6-170">When complete, click **Close**.</span></span>

<span data-ttu-id="41df6-171">Ardından, DC2 hello corp.contoso.com etki alanı için bir kopya etki alanı denetleyicisi olarak yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="41df6-171">Next, configure DC2 as a replica domain controller for hello corp.contoso.com domain.</span></span> <span data-ttu-id="41df6-172">Bu komutlar DC2'hello Windows PowerShell komut isteminden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="41df6-172">Run these commands from hello Windows PowerShell command prompt on DC2.</span></span>

    Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
    Install-ADDSDomainController -Credential (Get-Credential CORP\User1) -DomainName "corp.contoso.com" -InstallDns:$true -DatabasePath "F:\NTDS" -LogPath "F:\Logs" -SysvolPath "F:\SYSVOL"

<span data-ttu-id="41df6-173">İstendiğinde toosupply olduğunu unutmayın her ikisi de hello CORP\User1 parola ve Dizin Hizmetleri Geri Yükleme Modu'nda (DSRM) parolasını ve toorestart DC2.</span><span class="sxs-lookup"><span data-stu-id="41df6-173">Note that you are prompted toosupply both hello CORP\User1 password and a Directory Services Restore Mode (DSRM) password, and toorestart DC2.</span></span>

<span data-ttu-id="41df6-174">Merhaba TestVNET sanal ağ olan kendi DNS sunucusuna (DC2), bu DNS sunucusu hello TestVNET sanal ağ toouse yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="41df6-174">Now that hello TestVNET virtual network has its own DNS server (DC2), you must configure hello TestVNET virtual network toouse this DNS server.</span></span>

1. <span data-ttu-id="41df6-175">Merhaba hello Azure portalında, sol bölmede, hello sanal ağlar simgesine tıklayın ve ardından **TestVNET**.</span><span class="sxs-lookup"><span data-stu-id="41df6-175">In hello left pane of hello Azure portal, click hello virtual networks icon, and then click **TestVNET**.</span></span>
2. <span data-ttu-id="41df6-176">Merhaba üzerinde **ayarları** sekmesini tıklatın, **DNS sunucuları**.</span><span class="sxs-lookup"><span data-stu-id="41df6-176">On hello **Settings** tab, click **DNS servers**.</span></span>
3. <span data-ttu-id="41df6-177">İçinde **birincil DNS sunucusu**, türü **192.168.0.4** tooreplace 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="41df6-177">In **Primary DNS server**, type **192.168.0.4** tooreplace 10.0.0.4.</span></span>
4. <span data-ttu-id="41df6-178">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="41df6-178">Click **Save**.</span></span>

<span data-ttu-id="41df6-179">Bu, geçerli bir yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="41df6-179">This is your current configuration.</span></span> 

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="41df6-180">Benzetimli karma bulut ortamınızı artık test etmek için hazırdır.</span><span class="sxs-lookup"><span data-stu-id="41df6-180">Your simulated hybrid cloud environment is now ready for testing.</span></span>

## <a name="next-step"></a><span data-ttu-id="41df6-181">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="41df6-181">Next step</span></span>
* <span data-ttu-id="41df6-182">Ayarlanmış bir [web tabanlı, iş hattı uygulaması](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Bu ortamdaki.</span><span class="sxs-lookup"><span data-stu-id="41df6-182">Set up a [web-based, line of business application](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in this environment.</span></span>

