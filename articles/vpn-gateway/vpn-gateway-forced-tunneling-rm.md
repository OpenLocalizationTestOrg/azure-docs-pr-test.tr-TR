---
title: "Zorlamalı tünel Azure siteden siteye bağlantıları için yapılandırın: Resource Manager | Microsoft Docs"
description: "Nasıl tooredirect veya 'force' tüm Internet'e bağlı trafik geri tooyour konumu şirket içi."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cbe58db8-b598-4c9f-ac88-62c865eb8721
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: 6bc52c04ab0749a674c9863be5e4f9a9f7c98df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-azure-resource-manager-deployment-model"></a>Zorlamalı tünel kullanarak yapılandırma hello Azure Resource Manager dağıtım modeli

Yeniden yönlendirme veya "tüm Internet'e bağlı trafik geri tooyour şirket içi konumu denetleme ve denetim için bir siteden siteye VPN tüneli aracılığıyla zorla" sağlar tünel zorlandı. Bu, çoğu kurumsal BT için kritik güvenlik gereksinimdir ilkeleri. Zorlamalı tünel olmadan, Internet'e bağlı trafik, vm'lerden Azure her zaman Azure ağ altyapısından toohello Internet hello seçeneği tooallow olmadan doğrudan çıkışı, tooinspect veya denetim hello trafiğin geçeceğini. Yetkisiz Internet erişimine olası tooinformation açığa çıkmasına veya diğer tür güvenlik ihlallerini yol açabilir.

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

Bu makalede zorlamalı tünel hello Resource Manager dağıtım modeli kullanılarak oluşturulan sanal ağlar için nasıl yapılandıracağınız anlatılmaktadır. Zorlamalı tünel, değil hello Portalı aracılığıyla PowerShell kullanarak yapılandırılabilir. Zorlanan hello Klasik dağıtım modeli için tünel tooconfigure istiyorsanız, Klasik makale açılır listeden aşağıdaki hello seçin:

> [!div class="op_single_selector"]
> * [PowerShell - Klasik](vpn-gateway-about-forced-tunneling.md)
> * [PowerShell - Resource Manager](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a>Zorlanan tünel hakkında

Aşağıdaki diyagramda hello nasıl zorlamalı tünel works gösterilmektedir. 

![Zorlamalı Tünel Oluşturma](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

Merhaba yukarıdaki örnekte, alt ağı değil zorlanır ön uç tünelli hello. Merhaba ön uç alt Hello iş yüklerini tooaccept devam et ve toocustomer isteklerini doğrudan Internet hello yanıt. Merhaba Orta katmanda ve arka uç alt zorlanır tünel. Bu iki alt toohello Internet tüm giden bağlantılar zorlanmış ya da yeniden yönlendirilen geri tooan şirket içi site S2S VPN tünelleri hello biri aracılığıyla olacaktır.

Bu toorestrict sağlar ve Internet erişimi, sanal makinelerden inceleme veya çok katmanlı bir hizmet Mimarinizi gerekli tooenable devam ederken, azure'daki hizmetlere bulut. Sanal ağlarınıza hiçbir Internet'e iş yükleri varsa, zorlamalı tünel toohello tüm sanal ağların de uygulayabilirsiniz.

## <a name="requirements-and-considerations"></a>Gereksinimleri ve konular

Zorlamalı tünel Azure'da sanal ağ kullanıcı tanımlı yollar yapılandırılır. Yeniden yönlendirme trafiği tooan site varsayılan yol toohello Azure VPN ağ geçidi olarak ifade edilir şirket içi. Kullanıcı tanımlı Yönlendirme ve sanal ağlar hakkında daha fazla bilgi için bkz: [kullanıcı tanımlı yollar ve IP iletimini](../virtual-network/virtual-networks-udr-overview.md).

* Her sanal ağ alt yerleşik sistem yönlendirme tablosu vardır. Merhaba sistem yönlendirme tablosu aşağıdaki üç grup yolların hello sahiptir:
  
  * **Yerel VNet yollar:** doğrudan toohello hedef VM'ler hello aynı sanal ağ.
  * **Şirket içi yollar:** toohello Azure VPN ağ geçidi.
  * **Varsayılan yol:** doğrudan toohello Internet. Merhaba önceki iki yolları tarafından kapsanmayan hedefleyen paketler toohello özel IP adresleri bırakılır.
* Bu yordam, kullanıcı tanımlı yolları (UDR) toocreate yönlendirme tablosu tooadd varsayılan bir yol kullanır ve bu alt ağlardaki tünel zorunlu tablo tooyour sanal ağ alt ağı tooenable yönlendirme hello ilişkilendirin.
* Zorlamalı tünel rota tabanlı VPN ağ geçidi sahip bir sanal ağ ile ilişkilendirilmiş olması gerekir. Tooset "varsayılan site" Merhaba şirket içi yerel siteleri bağlı toohello sanal ağ arasında gerekir. Ayrıca, hello VPN cihazı trafiğini Seçici 0.0.0.0/0 kullanılarak yapılandırılmalıdır şirket içi. 
* Zorlanan tünel ExpressRoute bu düzenek yapılandırılmamış, ancak bunun yerine, varsayılan rota hello ExpressRoute BGP üzerinden reklam tarafından etkinleştirilmiş eşliği oturumlarını. Daha fazla bilgi için bkz: Merhaba [ExpressRoute belgeleri](https://azure.microsoft.com/documentation/services/expressroute/).

## <a name="configuration-overview"></a>Yapılandırmasına genel bakış

Aşağıdaki yordamı hello bir kaynak grubu ve bir sanal ağ oluşturmanıza yardımcı olur. Sonra bir VPN ağ geçidi oluşturabilir ve zorlamalı tüneli yapılandırma. Bu yordamda hello sanal ağ 'MultiTier-VNet' üç alt ağa sahip değil: 'Ön uç', 'Midtier' ve 'Backend' dört ile şirket içi bağlantılar: 'DefaultSiteHQ' ve üç dalları.

Merhaba varsayılan site bağlantısı için zorlanan tünel ve hello 'Midtier' ve 'Backend' alt ağlar toouse zorlanan tünel yapılandırırken hello 'DefaultSiteHQ' hello yordam adımları ayarlayın.

## <a name="before-you-begin"></a>Başlamadan önce

Merhaba hello Azure Resource Manager PowerShell cmdlet'lerinin en son sürümünü yükleyin. Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) hello PowerShell cmdlet'lerini yükleme hakkında daha fazla bilgi.

### <a name="toolog-in"></a>içinde toolog

[!INCLUDE [toolog in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a>Zorlamalı tünel yapılandırma

1. Bir kaynak grubu oluşturun.

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. Bir sanal ağ oluşturun ve alt ağları belirtin.

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. Merhaba, yerel ağ geçitleri oluşturun.

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. Merhaba rota tablosu ve yol kuralı oluşturun.

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. Merhaba rota tablosu toohello Midtier ve arka uç alt ağları ilişkilendirin.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. Merhaba ağ geçidi ile bir varsayılan sitesi oluşturun. Oluşturma ve hello ağ geçidi yapılandırma olduğundan bu adımı bazı zaman toocomplete, bazen 45 dakika veya daha fazla sürer.<br> Merhaba **- GatewayDefaultSite** olan hello zorunlu yönlendirme yapılandırması toowork verir cmdlet parametresi Merhaba, bu nedenle bu ayarı düzgün dikkatli tooconfigure alın. Bu parametre, PowerShell 1.0 veya sonraki kullanılabilir.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. Merhaba siteden siteye VPN bağlantıları kurun.

  ```powershell
  $gateway = Get-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling"
  $lng1 = Get-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" 
  $lng2 = Get-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" 
  $lng3 = Get-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" 
  $lng4 = Get-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" 
    
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng1 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng2 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng3 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection4" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng4 -ConnectionType IPsec -SharedKey "preSharedKey"
    
  Get-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling"
  ```