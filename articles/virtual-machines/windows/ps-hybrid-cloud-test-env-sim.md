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
# <a name="set-up-a-simulated-hybrid-cloud-environment-for-testing"></a>Test için sanal karma bulut ortamı oluşturma
Bu makalede Microsoft Azure iki Azure sanal ağları kullanarak bir sanal karma bulut ortamı oluşturmada size adımları. Sonuçta elde edilen yapılandırma aşağıda verilmiştir.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

Bu karma bulut üretim ortamında taklit eder ve oluşur:

* Bir Azure sanal ağında (sınama laboratuvarı sanal ağ) barındırılan sanal ve Basitleştirilmiş şirket içi ağ.
* (TestVNET) Azure üzerinde barındırılan sanal şirket içi sanal ağ.
* İki sanal ağ arasında VNet-VNet bağlantı.
* TestVNET sanal ağı bir ikincil etki alanı denetleyicisi.

Bu, hangi yapabilecekleriniz gelen temel ve ortak başlangıç noktası sağlar:

* Geliştirme ve uygulamaları benzetimli karma bulut ortamında test etme.
* Test yapılandırmaları bilgisayarlar, bazı sınama laboratuvarı sanal ağ içinde ve bazı karma bulut tabanlı BT iş yüklerini benzetimini yapmak için TestVNET sanal ağ içinde oluşturun.

Bu karma bulut test ortamını ayarlama için dört ana aşama vardır:

1. Sınama laboratuvarı sanal ağ yapılandırın.
2. Şirket içi sanal ağ oluşturun.
3. VNet-VNet VPN bağlantısı oluşturun.
4. DC2 yapılandırın. 

Bu yapılandırma, bir Azure aboneliği gerektirir. Bir MSDN veya Visual Studio aboneliğiniz varsa, bkz: [Visual Studio aboneleri için aylık Azure kredi](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).

> [!NOTE]
> Çalışırken sanal makineler ve sanal ağ geçitlerini azure'da devam eden bir para maliyet doğurur. Bu maliyet, MSDN karşı faturalandırılır veya Ücretli aboneliği. Bir Azure VPN ağ geçidi iki Azure sanal makineler kümesi olarak uygulanır. Maliyetleri en aza indirmek için test ortamı oluşturmak ve gerekli test edip tanıtım mümkün olan en kısa sürede gerçekleştirin.
> 
> 

## <a name="phase-1-configure-the-testlab-virtual-network"></a>1. Aşama: sınama laboratuvarı sanal ağı yapılandırma
Konusundaki yönergeleri kullanın [temel yapılandırma test ortamı](https://technet.microsoft.com/library/mt771177.aspx) sınama laboratuvarı adlı Azure sanal ağında ead1, Uyg1 ve İSTEMCİ1 bilgisayarları yapılandırmak için konu. 

Ardından, bir Azure PowerShell istemi başlatın.

> [!NOTE]
> Aşağıdaki komutu kullanın Azure PowerShell 1.0 ve daha sonra ayarlar.
> 
> 

Hesabınızda oturum açın.

    Login-AzureRMAccount

Aşağıdaki komutu kullanarak, abonelik adını alın.

    Get-AzureRMSubscription | Sort SubscriptionName | Select SubscriptionName

Azure aboneliğiniz ayarlayın. Aşama 1 temel yapılandırma oluşturmak için kullanılan aynı abonelik kullanın. Dahil olmak üzere tırnak işaretleri içindeki her şeyi değiştirin < ve > karakterleri doğru ada sahip.

    $subscr="<subscription name>"
    Get-AzureRmSubscription –SubscriptionName $subscr | Select-AzureRmSubscription

Ardından, bir ağ geçidi alt ağı Azure ağ geçidi barındırmak için kullanılan, temel yapılandırma sınama laboratuvarı sanal ağa ekleyin.

    $rgName="<name of your resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed the TestLab virtual network, such as West US>"
    $vnet=Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name TestLab
    Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 10.255.255.248/29 -VirtualNetwork $vnet
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet

Ardından, sınama laboratuvarı sanal ağ için ağ geçidi atamak için bir ortak IP adresi isteyin.

    $gwpip=New-AzureRmPublicIpAddress -Name TestLab_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic

Ardından, ağ geçidi oluşturun.

    $vnet=Get-AzureRmVirtualNetwork -Name TestLab -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name TestLab_GWConfig -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id 
    New-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

Yeni ağ geçitleri 20 dakika veya daha fazla oluşturmak için uygulayabileceğiniz göz önünde bulundurun.

Yerel bilgisayarınızda Azure portalından CORP\User1 kimlik bilgileriyle DC1'e bağlanın. Bilgisayarlar ve kullanıcılar kendi yerel etki alanı denetleyicisi kimlik doğrulaması için kullanabileceğiniz CORP etki alanı yapılandırmak için DC1'de bir yönetici düzeyi Windows PowerShell komut isteminde şu komutları çalıştırın.

    New-ADReplicationSite -Name "TestLab" 
    New-ADReplicationSite -Name "TestVNET"
    New-ADReplicationSubnet -Name "10.0.0.0/8" -Site "TestLab"
    New-ADReplicationSubnet -Name "192.168.0.0/16" -Site "TestVNET"

Bu, geçerli bir yapılandırmadır.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph1.png)

## <a name="phase-2-create-the-testvnet-virtual-network"></a>2. Aşama: TestVNET sanal ağ oluşturma
İlk olarak, TestVNET sanal ağ oluşturma ve bir ağ güvenlik grubu ile koruyun.

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

Ardından, TestVNET sanal ağ için ağ geçidi için ayrılmış ve ağ geçidi oluşturmak için bir ortak IP adresi isteyin.

    $gwpip=New-AzureRmPublicIpAddress -Name TestVNET_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $vnet=Get-AzureRmVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name "TestVNET_GWConfig" -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
    New-AzureRmVirtualNetworkGateway -Name "TestVNET_GW" -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

Bu, geçerli bir yapılandırmadır.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph2.png)

## <a name="phase-3-create-the-vnet-to-vnet-connection"></a>3. Aşama: VNet-VNet bağlantısı oluşturma
İlk olarak, rastgele, şifreleme açısından güçlü, 32 karakterlik önceden paylaşılan anahtar, ağ veya Güvenlik Yöneticisi'nden alın. Alternatif olarak, bilgileri kullanmak [IPSec önceden paylaşılan anahtar için rastgele bir dize oluşturma](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) önceden paylaşılan anahtar elde edilir.

Ardından, tamamlanması biraz zaman alabilir VNet-VNet VPN bağlantısı oluşturmak için şu komutları kullanın.

    $sharedKey="<pre-shared key value>"
    $gwTestLab=Get-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName
    $gwTestVNET=Get-AzureRmVirtualNetworkGateway -Name TestVNET_GW -ResourceGroupName $rgName
    New-AzureRmVirtualNetworkGatewayConnection -Name TestLab_to_TestVNET -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestLab -VirtualNetworkGateway2 $gwTestVNET -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey
    New-AzureRmVirtualNetworkGatewayConnection -Name TestVNET_to_TestLab -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestVNET -VirtualNetworkGateway2 $gwTestLab -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey

Birkaç dakika sonra bağlantı kurulmalıdır.

Bu, geçerli bir yapılandırmadır.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph3.png)

## <a name="phase-4-configure-dc2"></a>4. Aşama: DC2 yapılandırın
İlk olarak, DC2 için bir sanal makine oluşturun. Bu komutlar, yerel bilgisayarınızda Azure PowerShell komut isteminde çalıştırın.

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

Ardından, Azure portalından yeni DC2 sanal makineye bağlanın.

Ardından, bir Windows Güvenlik duvarı kuralı temel bağlantıyı test etmek için trafiğe izin verecek şekilde yapılandırın. Bir yönetici düzeyi Windows PowerShell komut isteminde DC2'de, bu komutları çalıştırın.

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc1.corp.contoso.com

Ping komutu 10.0.0.4 IP adresinden dört başarılı yanıt neden olur. VNet-VNet bağlantısı üzerinden trafik test budur.

Sonra ek veri diski DC2'de sürücü harfi F: olan yeni bir birim olarak ekleyin.

1. Sunucu Yöneticisi'nin sol bölmesinde, **dosya ve depolama hizmetleri**ve ardından **diskleri**.
2. İçerik bölmesinde içinde **diskleri** grubunda **disk 2** (ile **bölüm** kümesine **bilinmeyen**).
3. Tıklatın **görevleri**ve ardından **yeni birim**.
4. Önce üzerinde yeni birim Sihirbazı sayfasında başlayan, tıklatın **sonraki**.
5. Sunucu ve disk sayfa Seç'i tıklatın **Disk 2**ve ardından **sonraki**. İstendiğinde, tıklatın **Tamam**.
6. Birimin boyutunu belirtin sayfasında tıklatın **sonraki**.
7. Bir sürücü harfi veya klasörü sayfasına Ata hakkında'yı tıklatın **sonraki**.
8. Dosya Seç Sistem Ayarları sayfasında, tıklatın **sonraki**.
9. Seçimlerini onaylayın sayfasında, tıklatın **oluşturma**.
10. Tamamlandığında, tıklayın **Kapat**.

Ardından, DC2 corp.contoso.com etki alanında kopya etki alanı denetleyicisi olarak yapılandırın. Bu komutlar DC2'de Windows PowerShell komut isteminden çalıştırın.

    Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
    Install-ADDSDomainController -Credential (Get-Credential CORP\User1) -DomainName "corp.contoso.com" -InstallDns:$true -DatabasePath "F:\NTDS" -LogPath "F:\Logs" -SysvolPath "F:\SYSVOL"

Not CORP\User1 parola ve Dizin Hizmetleri Geri Yükleme Modu'nda (DSRM) parolasını sağlamanız ve DC2 yeniden başlatmanız istenir.

Kendi DNS sunucusuna (DC2) TestVNET sanal ağı sahiptir, bu DNS sunucusu kullanacak şekilde TestVNET sanal ağ yapılandırmanız gerekir.

1. Azure portalının sol bölmede, sanal ağlar simgesine tıklayın ve ardından **TestVNET**.
2. Üzerinde **ayarları** sekmesini tıklatın, **DNS sunucuları**.
3. İçinde **birincil DNS sunucusu**, türü **192.168.0.4** 10.0.0.4 değiştirmek için.
4. **Kaydet** düğmesine tıklayın.

Bu, geçerli bir yapılandırmadır. 

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

Benzetimli karma bulut ortamınızı artık test etmek için hazırdır.

## <a name="next-step"></a>Sonraki adım
* Ayarlanmış bir [web tabanlı, iş hattı uygulaması](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Bu ortamdaki.

