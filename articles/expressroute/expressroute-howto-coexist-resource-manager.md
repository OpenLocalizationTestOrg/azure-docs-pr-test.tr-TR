---
title: "Bir arada var olabilen ExpressRoute ve Siteden Siteye VPN bağlantıları yapılandırma: Resource Manager: Azure | Microsoft Docs"
description: "Bu makalede Resource Manager modeli için bir arada var olabilen ExpressRoute ve bir Siteden Siteye VPN bağlantısını nasıl yapılandıracağınız anlatılmaktadır."
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7717b14-3da3-4a6d-b78e-a5020766bc2c
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: charwen,cherylmc
ms.openlocfilehash: efda9f89d95617c8c4e75af91b20631dc468d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a>Birlikte bulunan ExpressRoute bağlantıları ile Siteden Siteye bağlantıları yapılandırma
> [!div class="op_single_selector"]
> * [PowerShell - Resource Manager](expressroute-howto-coexist-resource-manager.md)
> * [PowerShell - Klasik](expressroute-howto-coexist-classic.md)
> 
> 

Siteden Siteye VPN ve ExpressRoute eşzamanlı bağlantılarını yapılandırmanın çeşitli avantajları vardır. ExressRoute için güvenli bir yük devretme yolu olarak siteden siteye VPN yapılandırmak veya ExpressRoute aracılığıyla bağlanmayan siteden siteye VPN tooconnect toosites kullanın. Biz bu makalede her iki senaryoyu hello adımları tooconfigure kapsar. Bu makalede toohello Resource Manager dağıtım modeli uygular ve PowerShell kullanır. Bu yapılandırma hello Azure portalında kullanılabilir değil.

> [!IMPORTANT]
> Aşağıdaki hello yönergeleri izlemeden önce ExpressRoute bağlantı hatlarının önceden yapılandırılmış olması gerekir. Merhaba kılavuzları çok izlediğinizden emin olun[bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-arm.md) ve [yönlendirmeyi yapılandırma](expressroute-howto-routing-arm.md) devam etmeden önce.
> 
> 

## <a name="limits-and-limitations"></a>Sınırlar ve sınırlamalar
* **Geçiş yönlendirmesi desteklenmez.** Siteden Siteye VPN aracılığıyla bağlanan yerel ağınız ve ExpressRoute aracılığıyla bağlanan yerel ağınız arasında (Azure aracılığıyla) yönlendirme yapamazsınız.
* **Temel SKU ağ geçidi desteklenmez.** Temel SKU olmayan ağ geçidi için her iki hello kullanmalısınız [ExpressRoute ağ geçidi](expressroute-about-virtual-network-gateways.md) ve hello [VPN ağ geçidi](../vpn-gateway/vpn-gateway-about-vpngateways.md).
* **Yalnızca rota tabanlı VPN ağ geçidi desteklenir.** Rota tabanlı [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md) kullanmanız gerekir.
* **VPN ağ geçidiniz için statik rota yapılandırılmalıdır.** Yerel ağınıza bağlı tooboth ExpressRoute ve bir Site siteye VPN, bir statik yol, yerel ağ tooroute hello siteden siteye VPN bağlantısı toohello yapılandırılmış olması gerekiyor, ortak Internet.
* **ExpressRoute ağ geçidi önce yapılandırılmalıdır ve tooa hattı bağlanır.** Merhaba ExpressRoute ağ geçidi ilk oluşturmak ve hello siteden siteye VPN ağ geçidi eklemeden önce tooa hattı bağlamanız gerekir.

## <a name="configuration-designs"></a>Yapılandırma tasarımları
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a>Siteden siteye VPN’i ExpressRoute için bir yük devretme yolu olarak yapılandırma
Siteden siteye bir VPN bağlantısını ExpressRoute için yedek olarak yapılandırabilirsiniz. Bu, yalnızca toovirtual ağlar bağlantılı toohello Azure özel eşleme yoluna geçerlidir. Azure ortak ve Microsoft eşlemeleri aracılığıyla erişilebilen hizmetler için VPN tabanlı yük devretme çözümü yoktur. Merhaba expressroute bağlantı hattı her zaman hello birincil bağlantıdır. Yalnızca hello expressroute bağlantı hattı başarısız olursa veriler hello siteden siteye VPN yolu üzerinden akar.

> [!NOTE]
> Zaman aynı olan iki yollar hello expressroute bağlantı hattı siteden siteye VPN üzerinden tercih edilen olmakla birlikte, Azure doğru hello paketin hedef hello uzun önek eşleştirme toochoose hello rota kullanır.
> 
> 

![Bir arada var olma](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a>ExpressRoute aracılığıyla bağlanılmayan bir siteden siteye VPN tooconnect toosites yapılandırın
Burada bazı siteler tooAzure siteden siteye VPN üzerinden doğrudan bağlanın ve bazı sitelerin ExpressRoute üzerinden bağlanması ağınız yapılandırabilirsiniz. 

![Bir arada var olma](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> Sanal ağı, geçiş yönlendiricisi olarak yapılandıramazsınız.
> 
> 

## <a name="selecting-hello-steps-toouse"></a>Merhaba adımları toouse seçme
Yordamlar toochoose iki farklı kümesi vardır. Seçtiğiniz hello yapılandırma yordamı için tooconnect istediğiniz veya yeni bir sanal ağ toocreate istediğiniz var olan bir sanal ağ olup olmadığına bağlıdır.

* I yoksa bir VNet ve toocreate biri gerekir.
  
    Zaten bir sanal ağınız yoksa, bu yordam Resource Manager dağıtım modelini kullanarak yeni bir sanal ağ oluşturmak ve yeni ExpressRoute ve Siteden Siteye VPN bağlantıları oluşturmak için size yol gösterir. tooconfigure bir sanal ağ içinde hello adımları izleyin [toocreate yeni bir sanal ağ ve bir arada var olabilen bağlantılar](#new).
* Zaten bir Resource Manager dağıtım modeli VNet’im var.
  
    Mevcut bir Siteden Siteye VPN bağlantısı veya ExpressRoute bağlantısına sahip bir sanal ağınız zaten olabilir. Merhaba [tooconfigure arada var olabilen bağlantılar zaten olan bir VNet için](#add) bölüm hello ağ geçidini silme ve ardından yeni ExpressRoute ve siteden siteye VPN bağlantıları oluşturma size yol gösterir. Merhaba adımları Hello yeni bağlantıları oluştururken, belirli bir sırada tamamlanması gerekir. Diğer makaleler toocreate Hello yönergeleri, ağ geçitleri ve bağlantıları kullanmayın.
  
    Bu yordam, bir arada var olabilen bağlantılar oluşturmak, ağ geçidi, toodelete gerektirir ve yeni ağ geçitlerini yapılandırmak. Şirket içi bağlantılarınız için kapalı kalma süresi silin ve ağ geçidiniz ve bağlantıları oluşturun, ancak toomigrate gerekmez herhangi biri sanal makineleri veya hizmetleri tooa yeni sanal ağınız olacaktır. Yapılandırılmış toodo şekilde olmaları durumunda, ağ geçidi yapılandırması sırasında VM'ler ve hizmetler hello yük dengeleyici üzerinden kullanıma mümkün toocommunicate olmaya devam eder.

## <a name="new"></a>toocreate yeni bir sanal ağ ve arada var olabilen bağlantılar
Bu yordamda, bir VNet oluşturma ve bir arada var olabilen Siteden Siteye ve ExpressRoute bağlantıları oluşturma işlemleri adım adım açıklanmıştır.

1. Merhaba hello Azure PowerShell cmdlet'lerinin en son sürümünü yükleyin. Merhaba cmdlet'lerini yükleme hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview). Bu yapılandırma için kullandığınız hello cmdlet'leri ne tanımanız değerinden biraz farklı olabilir. Bu yönergelerde emin toouse hello cmdlet'leri belirtilmiş.
2. Tooyour hesabında oturum ve hello ortamını ayarlama.

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. Ağ Geçidi Alt Ağı içeren bir sanal ağ oluşturun. Merhaba sanal ağ yapılandırması hakkında daha fazla bilgi için bkz: [Azure sanal ağ yapılandırması](../virtual-network/virtual-networks-create-vnet-arm-ps.md).
   
   > [!IMPORTANT]
   > Merhaba ağ geçidi alt ağı/27 veya daha kısa bir önek (örneğin, /26 veya/25) olmalıdır.
   > 
   > 
   
    Yeni bir VNet oluşturun.

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    Alt ağlar ekleyin.

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    Merhaba VNet yapılandırmasını kaydedin.

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <a name="gw"></a>ExpressRoute ağ geçidi oluşturun. Merhaba ExpressRoute ağ geçidi yapılandırması hakkında daha fazla bilgi için bkz: [ExpressRoute ağ geçidi Yapılandırması](expressroute-howto-add-gateway-resource-manager.md). Merhaba gatewaysku *standart*, *HighPerformance*, veya *UltraPerformance*.

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. Merhaba ExpressRoute ağ geçidi toohello expressroute bağlantı hattı bağlayın. Bu adımı tamamladıktan sonra şirket içi ağınız ve ExpressRoute aracılığıyla Azure arasında hello bağlantı kurulur. Merhaba bağlantı işlemi hakkında daha fazla bilgi için bkz: [Vnets'i tooExpressRoute](expressroute-howto-linkvnet-arm.md).

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <a name="vpngw"></a>Ardından, Siteden Siteye VPN ağ geçidinizi oluşturun. Merhaba VPN ağ geçidi yapılandırması hakkında daha fazla bilgi için bkz: [bir VNet ile siteden siteye bağlantı yapılandırma](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md). Merhaba gatewaysku *standart*, *HighPerformance*, veya *UltraPerformance*. Merhaba VpnType gerekir *RouteBased*.

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    Azure VPN ağ geçidi, BGP yönlendirme protokolünü destekler. Bu sanal ağ için komutu aşağıdaki hello hello - Asn anahtarını ekleyerek, ASN (AS numarası) belirtebilirsiniz. Bu parametre belirtmeden varsayılan tooAS 65515 numarası.

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    BGP eşliği IP hello ve hello Azure $azureVpn.BgpSettings.BgpPeeringAddress ve $azureVpn.BgpSettings.Asn hello VPN ağ geçidi için kullandığı bir sayı olarak bulabilir. Daha fazla bilgi için bkz. Azure VPN ağ geçidi için [BGP’yi yapılandırma](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md).
7. Bir yerel site VPN ağ geçidi varlığı oluşturun. Bu komut, şirket içi VPN ağ geçidinizi yapılandırmaz. Bunun yerine, hello genel IP gibi tooprovide hello yerel ağ geçidi ayarları sağlar ve hello Azure VPN ağ geçidi tooit bağlanabilmesi hello şirket içi adres alanı.
   
    Yerel VPN Cihazınızı yalnızca statik yönlendirmeyi destekliyorsa, aşağıdaki şekilde hello hello statik yollar yapılandırabilirsiniz:

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    Yerel VPN Cihazınızı hello BGP destekler ve tooenable dinamik yönlendirme istiyorsanız tooknow hello BGP gereken IP ve yerel VPN numarası gibi hello eşliği aygıt kullanır.

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for hello BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. Yerel VPN cihaz tooconnect toohello yeni Azure VPN ağ geçidinizi yapılandırın. VPN cihazını yapılandırma hakkında daha fazla bilgi için bkz. [VPN Cihazı Yapılandırma](../vpn-gateway/vpn-gateway-about-vpn-devices.md).
9. Bağlantı hello siteden siteye VPN ağ geçidinde Azure toohello yerel ağ geçidi.

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <a name="add"></a>zaten olan bir VNet için tooconfigure arada var olabilen bağlantılar
Varolan bir sanal ağınız varsa, hello ağ geçidi alt ağ boyutunu kontrol edin. Merhaba ağ geçidi alt ağı /28 veya/29 ise, öncelikle hello sanal ağ geçidini silmek ve hello ağ geçidi alt ağ boyutunu artırın. Merhaba bu bölümdeki adımları şunları nasıl yapacağınızı toodo.

Merhaba ağ geçidi alt ağı /27 ise veya daha büyük ve hello sanal ağ ExpressRoute üzerinden bağlı olduğundan, hello adımları atlayın ve çok devam["6. adım - siteden siteye VPN ağ geçidi oluşturma"](#vpngw) hello önceki bölümdeki. 

> [!NOTE]
> Merhaba mevcut ağ geçidini sildiğinizde, bu yapılandırma üzerinde çalışırken, yerel şirket hello bağlantı tooyour sanal ağ kaybedersiniz. 
> 
> 

1. Tooinstall hello en son sürümünü hello Azure PowerShell cmdlet'lerini gerekir. Cmdlet'lerini yükleme hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview). Bu yapılandırma için kullandığınız hello cmdlet'leri ne tanımanız değerinden biraz farklı olabilir. Bu yönergelerde emin toouse hello cmdlet'leri belirtilmiş. 
2. Merhaba mevcut ExpressRoute veya siteden siteye VPN ağ geçidini silin.

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. Ağ Geçidi Alt Ağını silin.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. /27 veya daha büyük bir Ağ Geçidi Alt Ağı ekleyin.
   
   > [!NOTE]
   > Yeterli IP adresi, sanal ağ tooincrease hello ağ geçidi alt ağı boyutuna sahip değilseniz, daha fazla IP adresi alanı tooadd gerekir.
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    Merhaba VNet yapılandırmasını kaydedin.

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. Bu noktada, hiçbir ağ geçidi olmayan bir VNet’e sahip olursunuz. toocreate yeni ağ geçitleri ve bağlantılarınızı tamamlamak, devam edebilmeniz [4. adım - bir ExpressRoute ağ geçidi oluşturma](#gw), önceki adımları kümesini hello bulunan.

## <a name="tooadd-point-to-site-configuration-toohello-vpn-gateway"></a>tooadd noktadan siteye yapılandırması toohello VPN ağ geçidi
Bir arada var olan kurulumda tooadd noktadan siteye yapılandırması tooyour VPN ağ geçidi hello adımları izleyebilirsiniz.

1. VPN İstemcisi adres havuzunu ekleyin.

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. Merhaba VPN kök sertifika tooAzure VPN ağ geçidinizi için karşıya yükleyin. Bu örnekte, bu hello kök sertifikası PowerShell cmdlet'lerini aşağıdaki hello çalıştırdığı hello yerel makinede saklandığı varsayılır.

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

Noktadan Siteye VPN hakkında daha fazla bilgi içini bkz. [Noktadan Siteye bağlantı yapılandırma](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).

## <a name="next-steps"></a>Sonraki adımlar
ExpressRoute hakkında daha fazla bilgi için bkz: Merhaba [ExpressRoute SSS](expressroute-faqs.md).
