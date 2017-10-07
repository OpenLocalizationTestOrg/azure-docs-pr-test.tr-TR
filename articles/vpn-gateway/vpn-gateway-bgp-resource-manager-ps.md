---
title: "Azure VPN ağ geçitlerinde BGP yapılandırın: Resource Manager: PowerShell | Microsoft Docs"
description: "Bu makalede Azure Resource Manager ve PowerShell kullanarak Azure VPN Gateway'ler ile BGP nasıl yapılandıracağınız anlatılmaktadır."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 905b11a7-1333-482c-820b-0fd0f44238e5
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: yushwang
ms.openlocfilehash: a9d13ae6b319e2efa8965dc2955c9b89ac3fd12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-bgp-on-azure-vpn-gateways-using-powershell"></a>Nasıl tooconfigure BGP Azure VPN ağ geçitlerinde PowerShell'i kullanma
Bu makalede bir şirket içi siteden siteye (S2S) VPN bağlantısı ve hello Resource Manager dağıtım modeli ve PowerShell kullanarak VNet-VNet bağlantısı hello adımları tooenable BGP anlatılmaktadır.

## <a name="about-bgp"></a>BGP hakkında
BGP hello Internet tooexchange Yönlendirme ve ulaşılabilirlik bilgilerini iki veya daha fazla ağ arasında yaygın olarak kullanılan hello standart yönlendirme protokolüdür. BGP hello Azure VPN ağ geçitleri ve BGP eşlikleri veya Komşuları olarak adlandırılan, şirket içi VPN cihazlarınızı etkinleştirir, tooexchange "yolları", her iki ağ geçidini hello kullanılabilirlik size bildirir ve ulaşılabilirlik olanlar için önekleri hello ağ geçitlerinden veya yönlendiricilerden söz konusu aracılığıyla toogo. BGP, bir BGP eş tooall bir BGP ağ geçidinin öğrendiği yolları yayarak birden fazla ağ arasında geçiş yönlendirme de etkinleştirebilir diğer BGP eşleri.

Bkz: [Azure VPN Gateways ile BGP'ye genel bakış](vpn-gateway-bgp-overview.md) BGP ve toounderstand hello teknik gereksinimleri ve konular BGP kullanmanın avantajları hakkında daha fazla tartışma için.

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a>Azure VPN ağ geçitlerinde BGP ile çalışmaya başlama

Bu makale size hello adımları toodo hello görevleri aşağıdaki yardımcı olur:

* [Bölüm 1 - etkinleştir BGP, Azure VPN ağ geçidi](#enablebgp)
* [Bölüm 2 - BGP şirketler arası bağlantı Kur](#crossprembgp)
* [Bölüm 3 - BGP VNet-VNet bağlantı Kur](#v2vbgp)

Her bir parçasını hello yönergeleri BGP ağ bağlantınızı etkinleştirmek için temel yapı bloğu oluşturur. Tüm üç bölümden tamamlarsanız, hello Aşağıdaki diyagramda gösterildiği gibi hello topoloji oluşturun:

![BGP topolojisi](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

Bölümleri birlikte toobuild ihtiyaçlarınıza uygun bir daha karmaşık, çoklu atlamalı geçiş ağ birleştirebilirsiniz.

## <a name ="enablebgp"></a>Bölüm 1 - BGP hello Azure VPN ağ geçidi üzerinde yapılandırma
Merhaba yapılandırma adımlarını hello hello Azure VPN ağ geçidi BGP parametrelerinin hello Aşağıdaki diyagramda gösterildiği gibi ayarlayın:

![BGP ağ geçidi](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a>Başlamadan önce
* Azure aboneliğiniz olduğunu doğrulayın. Henüz Azure aboneliğiniz yoksa [MSDN abonelik avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) etkinleştirebilir veya [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.
* Hello Azure Resource Manager PowerShell cmdlet'lerini yükleyin. Merhaba PowerShell cmdlet'lerini yükleme hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview). 

### <a name="step-1---create-and-configure-vnet1"></a>1. adım - oluşturun ve VNet1 yapılandırın
#### <a name="1-declare-your-variables"></a>1. Değişkenlerinizi bildirme
Bu alıştırmada, değişkenlerimizi bildirerek başlayın. Merhaba aşağıdaki örnekte bu alıştırmada hello değerleri kullanarak hello değişkenler bildirilmektedir. Üretim için yapılandırma emin tooreplace hello değerleri kendi değerlerinizle olabilir. Merhaba adımları toobecome yapılandırma bu tür tanıdık aracılığıyla çalıştırıyorsanız, bu değişkenleri kullanabilirsiniz. Merhaba değişkenleri değiştirin ve sonra kopyalayın ve PowerShell konsolunuza yapıştırın.

```powershell
$Sub1 = "Replace_With_Your_Subcription_Name"
$RG1 = "TestBGPRG1"
$Location1 = "East US"
$VNetName1 = "TestVNet1"
$FESubName1 = "FrontEnd"
$BESubName1 = "Backend"
$GWSubName1 = "GatewaySubnet"
$VNetPrefix11 = "10.11.0.0/16"
$VNetPrefix12 = "10.12.0.0/16"
$FESubPrefix1 = "10.11.0.0/24"
$BESubPrefix1 = "10.12.0.0/24"
$GWSubPrefix1 = "10.12.255.0/27"
$VNet1ASN = 65010
$DNS1 = "8.8.8.8"
$GWName1 = "VNet1GW"
$GWIPName1 = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection12 = "VNet1toVNet2"
$Connection15 = "VNet1toSite5"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Tooyour abonelik bağlanın ve yeni bir kaynak grubu oluştur
toouse hello Resource Manager cmdlet'lerini tooPowerShell moduna geçtiğinizden emin olun. Daha fazla bilgi için [Windows PowerShell’i Resource Manager ile kullanma](../powershell-azure-resource-manager.md) konusuna bakın.

PowerShell Konsolunuzu açın ve tooyour hesap bağlanın. Bağlandığınız örnek toohelp aşağıdaki hello kullan:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a>3. TestVNet1 oluşturma
Merhaba aşağıdaki örnekte TestVNet1 ve üç alt ağ, biri GatewaySubnet, biri FrontEnd ve diğeri Backend'dir adlı bir sanal ağ oluşturur. Kendi değerlerinizi yerleştirirken ağ geçidi alt ağınızı özellikle GatewaySubnet olarak adlandırmanız önem taşır. Başka bir ad kullanırsanız ağ geçidi oluşturma işleminiz başarısız olur.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-bgp-parameters"></a>2. adım - hello VPN ağ geçidi BGP parametrelerle TestVNet1 için oluşturma
#### <a name="1-create-hello-ip-and-subnet-configurations"></a>1. Merhaba IP ve alt ağ yapılandırmaları oluşturma
Ağınız için oluşturacağınız bir ortak IP adresi toobe ayrılmış toohello ağ geçidi isteği. De gerekli hello alt ağ ve IP yapılandırmaları tanımlaması.

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-hello-vpn-gateway-with-hello-as-number"></a>2. Merhaba VPN ağ geçidi ile Merhaba oluşturmak sayı olarak
TestVNet1 için Hello sanal ağ geçidi oluşturun. BGP TestVNet1 için bir rota tabanlı VPN ağ geçidi ve aynı zamanda hello ek parametre, - Asn tooset hello ASN (AS numarası) gerektirir. Merhaba ASN parametre ayarlamazsanız ASN 65515 atanır. Bir ağ geçidi oluşturma biraz zaman alabilir (30 dakika veya daha fazla toocomplete).

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-hello-azure-bgp-peer-ip-address"></a>3. Hello Azure BGP eşdeğer IP adresi al
Merhaba ağ geçidi oluşturulduktan sonra tooobtain hello hello Azure VPN ağ geçidi BGP eşdeğer IP adresi gerekir. Bu adres için şirket içi VPN cihazlarınızı BGP eşi gerekli tooconfigure hello Azure VPN ağ geçidi gibidir.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

Merhaba son komut hello karşılık gelen BGP yapılandırmaları hello Azure VPN ağ geçidi üzerinde gösterir; Örneğin:

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

Merhaba ağ geçidi oluşturulduktan sonra bu ağ geçidi tooestablish şirket içi veya VNet-VNet bağlantısı BGP ile kullanabilirsiniz. Merhaba aşağıdaki bölümlerde hello adımları toocomplete hello alıştırma yol.

## <a name ="crossprembbgp"></a>Bölüm 2 - BGP şirketler arası bağlantı Kur

tooestablish şirketler arası bağlantı, gereksinim duyduğunuz toocreate bir yerel ağ geçidi toorepresent şirket içi VPN aygıtınızın ve hello yerel ağ geçidi ile bağlantı tooconnect hello VPN ağ geçidi. Bu adım adım makaleleri olsa da, bu makalede hello ek özellikler gerekli toospecify hello BGP yapılandırma parametrelerini içerir.

![Şirket içi BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

Devam etmeden önce tamamladığınızdan emin olun [Kısım 1](#enablebgp) Bu alıştırmada.

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a>1. adım - oluşturma ve hello yerel ağ geçidi yapılandırma

#### <a name="1-declare-your-variables"></a>1. Değişkenlerinizi bildirme

Bu alıştırmada hello diyagramda gösterildiği toobuild hello yapılandırma devam eder. Merhaba olanları hello değerlerle emin tooreplace olması yapılandırmanızın toouse istiyor.

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

Şeyler toonote hello yerel ağ geçidi parametreleri ilgili birkaç:

* Merhaba yerel ağ geçidi aynı hello veya VPN ağ geçidi hello farklı bir konum ve kaynak grubu olabilir. Bu örnek, bunları farklı kaynak gruplarında farklı konumlarda gösterir.
* Merhaba minimum önek toodeclare hello yerel ağ geçidi için gereksinim duyduğunuz hello konak BGP eşdeğer IP adresinizin, VPN cihazınızdaki adresidir. Bu durumda, bir /32 olan "10.52.255.254/32" öneki.
* Bir anımsatıcı farklı BGP Asn'ler şirket içi ağlarınız ve Azure VNet arasında kullanmanız gerekir. Olan Merhaba, aynı şirket içi VPN aygıtınızın diğer BGP komşuları ile Merhaba ASN toopeer zaten kullanıyorsa, VNet ASN toochange gerekir.

Devam etmeden önce halen bağlı tooSubscription 1 olduğundan emin olun.

#### <a name="2-create-hello-local-network-gateway-for-site5"></a>2. Merhaba yerel ağ geçidi için Site5 oluşturma

Merhaba yerel ağ geçidi oluşturmadan önce onu, oluşturulmamışsa emin toocreate hello kaynak grubu olabilir. Merhaba yerel ağ geçidi için hello iki ek parametreler dikkat edin: Asn ve BgpPeerAddress.

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a>2. adım - hello VNet ağ geçidi ve yerel ağ geçidi Bağlan

#### <a name="1-get-hello-two-gateways"></a>1. İki ağ geçidi Hello Al

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a>2. Merhaba TestVNet1 tooSite5 bağlantısı oluşturma

Bu adımda TestVNet1 tooSite5 hello bağlantı oluşturun. Belirtmeniz gerekir "-EnableBGP $True" tooenable BGP Bu bağlantı için. Daha önce bahsedildiği gibi BGP ve BGP olmayan bağlantıları için olası toohave olduğu aynı Azure VPN ağ geçidi hello. BGP hello bağlantı özelliği etkin değilse, BGP parametreleri her iki ağ geçidini zaten yapılandırılmış olsa bile Azure BGP Bu bağlantı için izin vermez.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

Merhaba aşağıdaki örnekte bu alıştırmada, şirket içi VPN cihazınızın BGP yapılandırma bölümü hello girin hello parametreleri listelenir:

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being hello VPN tunnel interface on your device
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

Merhaba IPSec bağlantısı kurulduktan sonra birkaç dakika ve hello BGP eşliği oturumu başlatır sonra hello bağlantı kurulur.

## <a name ="v2vbgp"></a>Bölüm 3 - BGP VNet-VNet bağlantı Kur

Bu bölüm BGP ile VNet-VNet bağlantı hello Aşağıdaki diyagramda gösterildiği gibi ekler:

![BGP VNet-VNet için](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

yönergeleri izleyerek hello hello önceki adımlardan devam edin. Tamamlamanız gereken [bölümü ı](#enablebgp) toocreate TestVNet1 yapılandırmak ve VPN ağ geçidi BGP ile Merhaba. 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a>1. adım - TestVNet2 ve hello VPN ağ geçidi oluşturma

Önemli toomake hello IP adres alanı hello yeni sanal ağın TestVNet2, herhangi bir VNet aralıkları ile çakışmaması emin olur.

Bu örnekte, sanal ağlar hello toohello ait aynı abonelik. VNet-VNet bağlantıları farklı abonelikler arasında ayarlayabilirsiniz. Daha fazla bilgi için bkz: [VNet-VNet bağlantı yapılandırma](vpn-gateway-vnet-vnet-rm-ps.md). Merhaba eklediğinizden emin olun "-EnableBgp $True" ne zaman oluşturmaya izin ver hello bağlantıları tooenable BGP.

#### <a name="1-declare-your-variables"></a>1. Değişkenlerinizi bildirme

Merhaba olanları hello değerlerle emin tooreplace olması yapılandırmanızın toouse istiyor.

```powershell
$RG2 = "TestBGPRG2"
$Location2 = "West US"
$VNetName2 = "TestVNet2"
$FESubName2 = "FrontEnd"
$BESubName2 = "Backend"
$GWSubName2 = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$VNet2ASN = 65020
$DNS2 = "8.8.8.8"
$GWName2 = "VNet2GW"
$GWIPName2 = "VNet2GWIP"
$GWIPconfName2 = "gwipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a>2. TestVNet2 hello yeni kaynak grubu oluştur

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-vpn-gateway-for-testvnet2-with-bgp-parameters"></a>3. Merhaba VPN ağ geçidi BGP parametrelerle TestVNet2 için oluşturma

Ağınız için oluşturacak ve gerekli hello alt ağ ve IP yapılandırmaları tanımlamak bir ortak IP adresi toobe ayrılmış toohello ağ geçidi isteği.

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

Merhaba VPN ağ geçidi ile Merhaba oluşturmak sayı olarak. Merhaba varsayılan ASN, Azure VPN ağ geçitlerinde geçersiz kılmanız gerekir. Merhaba Asn'ler hello bağlı sanal ağlar farklı tooenable BGP ve transit yönlendirme olması gerekir.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a>2. adım - hello TestVNet1 ve TestVNet2 ağ geçitleri Bağlan

Bu örnekte, her iki ağ geçitleri hello olan aynı abonelik. Bu adımda hello tamamlayabilirsiniz aynı PowerShell oturumunda.

#### <a name="1-get-both-gateways"></a>1. Her iki ağ geçitleri Al

Oturum açma ve tooSubscription 1 bağlanmak emin olun.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a>2. Her iki bağlantı oluşturma

Bu adımda, TestVNet2 tooTestVNet1 TestVNet1 tooTestVNet2 hello bağlantısından ve hello bağlantı oluşturun.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> Her iki bağlantılarında emin tooenable BGP olması.
> 
> 

Bu adımları tamamladıktan sonra birkaç dakika sonra hello bağlantı kurulur. Merhaba VNet-VNet bağlantı tamamlandığında hello BGP eşliği oturumu çalışıyor.

Bu alıştırmada, tüm üç bölümden tamamladıysa, ağ topolojisi aşağıdaki hello kurduğunuz:

![BGP VNet-VNet için](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a>Sonraki adımlar

Bağlantınız tamamlandıktan sonra sanal makineleri tooyour sanal ağları ekleyebilirsiniz. Adımlar için bkz. [Sanal Makine Oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
