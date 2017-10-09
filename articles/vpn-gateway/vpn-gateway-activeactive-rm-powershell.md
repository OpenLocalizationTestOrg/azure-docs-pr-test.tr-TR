---
title: "VPN ağ geçitleri için etkin-etkin S2S VPN bağlantılarını yapılandırma: Azure Resource Manager: PowerShell | Microsoft Docs"
description: "Bu makalede Azure Resource Manager ve PowerShell kullanarak Azure VPN Gateway'ler ile etkin-etkin bağlantıları nasıl yapılandıracağınız anlatılmaktadır."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2017
ms.author: yushwang
ms.openlocfilehash: 964eedc7698e42bf0e082f0105845f2a339daf57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a>Azure VPN ağ geçitleri ile etkin-etkin S2S VPN bağlantılarını yapılandırma

Bu makalede hello adımları toocreate etkin-etkin şirket içi ve hello Resource Manager dağıtım modeli ve PowerShell kullanarak VNet-VNet bağlantıları anlatılmaktadır.

## <a name="about-highly-available-cross-premises-connections"></a>Yüksek oranda kullanılabilir şirket içi bağlantılar hakkında
tooachieve yüksek kullanılabilirlik şirketler arası ve VNet-VNet bağlantısı için birden çok VPN ağ geçidi dağıtmak ve birden çok paralel ağlarınız ve Azure arasında bağlantı kurabilir gerekir. Lütfen bakın [yüksek oranda kullanılabilir şirketler arası ve VNet-VNet bağlantısı](vpn-gateway-highlyavailable.md) bağlantı seçenekleri ve topolojisini genel bakış.

Bu makalede bir aktif-aktif yukarı tooset VPN bağlantısı ve iki sanal ağlar arasında etkin-etkin bağlantı şirketler arası hello yönergeler sağlar:

* [Bölüm 1 - oluşturun ve Azure VPN ağ geçidinizi etkin-etkin modunda yapılandırın](#aagateway)
* [Bölüm 2 - etkin-etkin şirketler arası bağlantı](#aacrossprem)
* [Bölüm 3 - etkin-etkin VNet-VNet bağlantıları kurmak](#aav2v)
* [Bölüm 4 - Güncelleştirme etkin-etkin ve etkin bekleme arasında varolan ağ geçidi](#aaupdate)

Bu arada toobuild ihtiyaçlarınıza uygun bir yüksek oranda kullanılabilir, daha karmaşık ağ topolojisi birleştirebilirsiniz.

> [!IMPORTANT]
> Lütfen bu hello etkin-etkin modu SKU'ları aşağıdaki yalnızca hello kullandığına dikkat edin: 
  * VpnGw1, VpnGw2, VpnGw3
  * HighPerformance (için eski eski SKU)
> 
> 

## <a name ="aagateway"></a>Bölüm 1 - oluşturma ve etkin-etkin VPN ağ geçitlerini yapılandırma
Aşağıdaki adımları hello Azure VPN ağ geçidinizi etkin-etkin modlarında yapılandırır. Merhaba arasındaki farklar hello etkin-etkin ve etkin bekleme ağ geçitleri:

* İki ortak IP adresi ile iki ağ geçidi IP yapılandırması toocreate gerekir
* Merhaba EnableActiveActiveFeature bayrağı ayarlı
* Merhaba ağ geçidi SKU'su VpnGw1, VpnGw2, VpnGw3 veya HighPerformance (eski SKU) olmalıdır.

Merhaba diğer özellikleri olan hello hello etkin-etkin olmayan ağ geçitleri ile aynı. 

### <a name="before-you-begin"></a>Başlamadan önce
* Azure aboneliğiniz olduğunu doğrulayın. Henüz Azure aboneliğiniz yoksa [MSDN abonelik avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) etkinleştirebilir veya [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.
* Tooinstall hello Azure Resource Manager PowerShell cmdlet'lerini gerekir. Bkz: [Azure PowerShell genel bakış](/powershell/azure/overview) hello PowerShell cmdlet'lerini yükleme hakkında daha fazla bilgi.

### <a name="step-1---create-and-configure-vnet1"></a>1. adım - oluşturun ve VNet1 yapılandırın
#### <a name="1-declare-your-variables"></a>1. Değişkenlerinizi bildirme
Bu alıştırmaya değişkenlerimizi bildirerek başlayacağız. Merhaba örnekte bu alıştırmada hello değerleri kullanarak hello değişkenler bildirilmektedir. Üretim için yapılandırma emin tooreplace hello değerleri kendi değerlerinizle olabilir. Merhaba adımları toobecome yapılandırma bu tür tanıdık aracılığıyla çalıştırıyorsanız, bu değişkenleri kullanabilirsiniz. Merhaba değişkenleri değiştirin ve sonra kopyalayın ve PowerShell konsolunuza yapıştırın.

```powershell
$Sub1 = "Ross"
$RG1 = "TestAARG1"
$Location1 = "West US"
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
$GW1IPName1 = "VNet1GWIP1"
$GW1IPName2 = "VNet1GWIP2"
$GW1IPconf1 = "gw1ipconf1"
$GW1IPconf2 = "gw1ipconf2"
$Connection12 = "VNet1toVNet2"
$Connection151 = "VNet1toSite5_1"
$Connection152 = "VNet1toSite5_2"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Tooyour abonelik bağlanın ve yeni bir kaynak grubu oluştur
TooPowerShell modu toouse hello Resource Manager cmdlet'lerini geçtiğinizden emin olun. Daha fazla bilgi için [Windows PowerShell’i Resource Manager ile kullanma](../powershell-azure-resource-manager.md) konusuna bakın.

PowerShell Konsolunuzu açın ve tooyour hesap bağlanın. Bağlandığınız örnek toohelp aşağıdaki hello kullan:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a>3. TestVNet1 oluşturma
Aşağıdaki Hello örneği TestVNet1 ve üç alt ağ, biri GatewaySubnet, biri FrontEnd ve diğeri Backend'dir adlı bir sanal ağ oluşturur. Kendi değerlerinizi yerleştirirken ağ geçidi alt ağınızı özellikle GatewaySubnet olarak adlandırmanız önem taşır. Başka bir ad kullanırsanız ağ oluşturma işleminiz başarısız olur.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-active-active-mode"></a>2. adım - etkin-etkin moduyla TestVNet1 için hello VPN ağ geçidi oluşturma
#### <a name="1-create-hello-public-ip-addresses-and-gateway-ip-configurations"></a>1. Merhaba ortak IP adresleri ve ağ geçidi IP yapılandırmaları oluşturma
Ağınız için oluşturacağınız isteği iki ortak IP adresleri toobe ayrılmış toohello ağ geçidi. De hello alt ağı ve gerekli IP yapılandırmaları tanımlaması.

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-hello-vpn-gateway-with-active-active-configuration"></a>2. Etkin-etkin yapılandırmayla Hello VPN ağ geçidi oluşturma
TestVNet1 için Hello sanal ağ geçidi oluşturun. İki GatewayIpConfig giriş ve hello EnableActiveActiveFeature bayrağı ayarlanmış unutmayın. Bir ağ geçidi oluşturma biraz zaman alabilir (45 dakika veya daha fazla toocomplete).

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-hello-gateway-public-ip-addresses-and-hello-bgp-peer-ip-address"></a>3. Merhaba ağ geçidi genel IP adresleri ve hello BGP eş IP adresi alın
Merhaba ağ geçidi oluşturulduktan sonra tooobtain hello hello Azure VPN ağ geçidi BGP eşdeğer IP adresi gerekir. Bu adres için şirket içi VPN cihazlarınızı BGP eşi gerekli tooconfigure hello Azure VPN ağ geçidi gibidir.

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

VPN ağ geçidinizi ve ilgili BGP eş IP adreslerini her ağ geçidi örneği için ayrılan cmdlet'leri tooshow hello iki ortak IP adresleri aşağıdaki hello kullan:

```powershell

    PS D:\> $gw1pip1.IpAddress
    40.112.190.5

    PS D:\> $gw1pip2.IpAddress
    138.91.156.129

    PS D:\> $vnet1gw.BgpSettingsText
    {
      "Asn": 65010,
      "BgpPeeringAddress": "10.12.255.4,10.12.255.5",
      "PeerWeight": 0
    }
```

Merhaba genel IP adresleri Hello sırasını hello ağ geçidi örnekleri ve karşılık gelen BGP eşliği adresleri hello için aynı hello. Bu örnekte, hello ağ geçidi VM 40.112.190.5, genel IP ile BGP eşliği adresini 10.12.255.4 kullanır ve 138.91.156.129 hello ağ geçidiyle 10.12.255.5 kullanır. Şirketinizdeki toohello etkin-etkin ağ geçidi bağlanan VPN cihazları ayarladığınızda, bu bilgiler gereklidir. Merhaba ağ geçidi tüm adresleri ile Merhaba diyagramı gösterilmiştir:

![etkin-etkin ağ geçidi](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

Merhaba ağ geçidi oluşturulduktan sonra bu ağ geçidi tooestablish etkin-etkin şirket içi veya VNet-VNet bağlantısı kullanabilirsiniz. Aşağıdaki bölümlerde hello hello adımları toocomplete hello alıştırma yol gösterir.

## <a name ="aacrossprem"></a>Bölüm 2 - bir aktif-aktif şirketler arası bağlantı kuramadı
tooestablish şirketler arası bağlantı, gereksinim duyduğunuz toocreate bir yerel ağ geçidi toorepresent şirket içi VPN aygıtınızın ve hello yerel ağ geçidi ile bağlantı tooconnect hello Azure VPN ağ geçidi. Bu örnekte, hello Azure VPN ağ geçidi etkin-etkin modunda değil. Sonuç olarak, olsa bile yalnızca bir VPN cihazı (yerel ağ geçidi) ve bir bağlantı kaynak şirket, hem Azure VPN ağ geçidi örnekleri hello şirket içi aygıtla S2S VPN tünelleri oluşturacaktır.

Devam etmeden önce lütfen tamamladığınızdan emin olun [Kısım 1](#aagateway) Bu alıştırmada.

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a>1. adım - oluşturma ve hello yerel ağ geçidi yapılandırma
#### <a name="1-declare-your-variables"></a>1. Değişkenlerinizi bildirme
Bu alıştırmada hello diyagramda gösterildiği toobuild hello yapılandırma devam eder. Merhaba olanları hello değerlerle emin tooreplace olması yapılandırmanızın toouse istiyor.

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

Şeyler toonote hello yerel ağ geçidi parametreleri ilgili birkaç:

* Merhaba yerel ağ geçidi aynı hello veya VPN ağ geçidi hello farklı bir konum ve kaynak grubu olabilir. Bu örnek bunları farklı kaynak gruplarında hello içinde gösterir, ancak aynı Azure konumu.
* Yukarıda gösterildiği gibi yalnızca bir şirket içi VPN cihazı ise hello etkin-etkin bağlantısı ile veya BGP protokolüne olmadan çalışabilir. Bu örnek BGP hello şirketler arası bağlantı için kullanır.
* BGP etkinleştirilirse, toodeclare hello yerel ağ geçidi için gereksinim duyduğunuz hello önek hello konak BGP eşdeğer IP adresinizin, VPN cihazınızdaki adresidir. Bu durumda, bir /32 olan "10.52.255.253/32" öneki.
* Bir anımsatıcı farklı BGP Asn'ler şirket içi ağlarınız ve Azure VNet arasında kullanmanız gerekir. Olan Merhaba, aynı şirket içi VPN aygıtınızın diğer BGP komşuları ile Merhaba ASN toopeer zaten kullanıyorsa, VNet ASN toochange gerekir.

#### <a name="2-create-hello-local-network-gateway-for-site5"></a>2. Merhaba yerel ağ geçidi için Site5 oluşturma
Lütfen devam etmeden önce hala bağlı tooSubscription 1 olduğundan emin olun. Henüz oluşturulmaz hello kaynak grubu oluşturun.

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a>2. adım - hello VNet ağ geçidi ve yerel ağ geçidi Bağlan
#### <a name="1-get-hello-two-gateways"></a>1. İki ağ geçidi Hello Al

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a>2. Merhaba TestVNet1 tooSite5 bağlantısı oluşturma
Bu adımda, hello bağlantı TestVNet1 tooSite5_1 "ile EnableBGP çok Ayarla" oluşturacağınız $True.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a>3. Şirket içi VPN cihazınız için VPN ve BGP parametreleri
Aşağıdaki örnek Hello bu alıştırma için şirket içi VPN cihazınızdaki BGP yapılandırma bölümü hello girer hello parametreleri listelenir:

    - Site5 ASN: 65050
    - Site5 BGP IP: 10.52.255.253
    - Tooannounce önekleri: (örneğin) 10.51.0.0/16 ve 10.52.0.0/16
    - Azure VNet ASN: 65010
    - Azure VNet BGP IP 1: 10.12.255.4 tünel too40.112.190.5 için
    - Azure VNet BGP IP 2: 10.12.255.5 tünel too138.91.156.129 için
    - Statik yollar: Hedef 10.12.255.4/32, nexthop hello VPN tüneli arabirimi too40.112.190.5 hedef 10.12.255.5/32, nexthop hello VPN tüneli arabirimi too138.91.156.129
    - eBGP Multihop: eBGP Cihazınızda gerekirse etkinleştirilmişse hello "multihop" seçeneği emin olun.

Merhaba IPSec bağlantısı kurulduktan sonra birkaç dakika ile Merhaba BGP eşliği oturumu başlatacak sonra hello bağlantı kurulmalıdır. Bu örnek, o ana kadarki aşağıda gösterilen hello diyagramı bunun sonucunda, yalnızca bir şirket içi VPN cihazı yapılandırmış:

![etkin etkin crossprem](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-toohello-active-active-vpn-gateway"></a>3. adım - iki şirket içi VPN aygıtları toohello etkin-etkin VPN ağ geçidi Bağlan
Merhaba iki VPN aygıtları varsa aynı ağ şirket içi, bağlanan hello Azure VPN ağ geçidi toohello ikinci VPN cihazı tarafından çift artıklık elde edebilirsiniz.

#### <a name="1-create-hello-second-local-network-gateway-for-site5"></a>1. Merhaba ikinci yerel ağ geçidi için Site5 oluşturma
Merhaba ağ geçidi IP adresi, adres öneki ve hello ikinci yerel ağ geçidi için BGP eşliği adresi hello hello önceki yerel ağ geçidi ile aynı çakışmaması gerekir, Not ağ şirket içi.

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-hello-vnet-gateway-and-hello-second-local-network-gateway"></a>2. Merhaba VNet ağ geçidi ve hello ikinci yerel ağ geçidi Bağlan
Merhaba bağlantı "ile EnableBGP çok Ayarla" TestVNet1 tooSite5_2 oluşturmak $True

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a>3. İkinci şirket içi VPN cihazınız için VPN ve BGP parametreleri
Benzer şekilde, aşağıdaki listeleri hello parametrelerin hello ikinci VPN cihazı girer:

```
- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5
- Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129
- Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5
                         Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

Merhaba (tüneller) bağlantı sonra çift yedekli VPN cihazları ve şirket içi ağınız ve Azure bağlanma tüneller olacaktır:

![çift artıklık crossprem](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <a name ="aav2v"></a>Bölüm 3 - bir aktif-aktif VNet-VNet bağlantı kuramadı
Bu bölüm BGP özellikli bir aktif-aktif VNet-VNet bağlantısı oluşturur. 

Merhaba yönergelerde hello önceki adımlardan, yukarıda listelenen devam edin. Tamamlamanız gereken [Kısım 1](#aagateway) toocreate TestVNet1 yapılandırmak ve VPN ağ geçidi BGP ile Merhaba. 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a>1. adım - TestVNet2 ve hello VPN ağ geçidi oluşturma
Önemli toomake hello IP adres alanı hello yeni sanal ağın TestVNet2, herhangi bir VNet aralıkları ile çakışmaması emin olur.

Bu örnekte, sanal ağlar hello toohello ait aynı abonelik. VNet-VNet bağlantıları farklı abonelikler arasında ayarlayabilirsiniz; Lütfen çok başvurun[VNet-VNet bağlantı yapılandırma](vpn-gateway-vnet-vnet-rm-ps.md) toolearn daha ayrıntıları. Merhaba eklediğinizden emin olun "-EnableBgp $True" ne zaman oluşturmaya izin ver hello bağlantıları tooenable BGP.

#### <a name="1-declare-your-variables"></a>1. Değişkenlerinizi bildirme
Merhaba olanları hello değerlerle emin tooreplace olması yapılandırmanızın toouse istiyor.

```powershell
$RG2 = "TestAARG2"
$Location2 = "East US"
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
$GW2IPName1 = "VNet2GWIP1"
$GW2IPconf1 = "gw2ipconf1"
$GW2IPName2 = "VNet2GWIP2"
$GW2IPconf2 = "gw2ipconf2"
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

#### <a name="3-create-hello-active-active-vpn-gateway-for-testvnet2"></a>3. Merhaba etkin-etkin VPN ağ geçidi için TestVNet2 oluşturma
Ağınız için oluşturacağınız isteği iki ortak IP adresleri toobe ayrılmış toohello ağ geçidi. De hello alt ağı ve gerekli IP yapılandırmaları tanımlaması.

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

Merhaba VPN ağ geçidi ile Merhaba numarası ve hello "EnableActiveActiveFeature" bayrak olarak oluşturun. Azure VPN gateway'lerinde hello varsayılan ASN kılmalıdır unutmayın. Merhaba Asn'ler hello bağlı sanal ağlar farklı tooenable BGP ve transit yönlendirme olması gerekir.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
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
Bu adımda TestVNet1 tooTestVNet2 hello bağlantısından ve hello bağlantı TestVNet2 tooTestVNet1 oluşturur.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> Her iki bağlantılarında emin tooenable BGP olması.
> 
> 

Bu adımları tamamladıktan sonra hello olması bağlantı birkaç dakika içinde ve hello BGP eşliği oturumu olacaktır yukarı hello VNet-VNet bağlantısı ile çift artıklık tamamlandıktan sonra:

![etkin etkin v2v](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <a name ="aaupdate"></a>Bölüm 4 - Güncelleştirme etkin-etkin ve etkin bekleme arasında varolan ağ geçidi
Merhaba son kısım, mevcut bir Azure VPN ağ geçidi nasıl yapılandırabileceğiniz olmadığını açıklamak etkin bekleme tooactive etkin modundan veya tersi.

> [!NOTE]
> Bu bölüm, önceden oluşturulmuş bir VPN ağ geçidi'nden standart tooHighPerformance, hello adımları tooresize eski SKU (eski SKU) içerir. Bu adımları Merhaba, eski eski SKU tooone yükseltmeyin yeni SKU'ları.
> 
> 

### <a name="configure-an-active-standby-gateway-tooactive-active-gateway"></a>Etkin bekleme ağ geçidi tooactive etkin ağ geçidini yapılandırma
#### <a name="1-gateway-parameters"></a>1. Ağ geçidi parametreleri
Aşağıdaki örneğine hello bir etkin-etkin ağ geçidi etkin bekleme ağ geçidi dönüştürür. Başka bir ortak IP adresi toocreate gerekir, ardından ikinci bir ağ geçidi IP yapılandırması ekleyin. Gösterildiği hello parametreleri kullanılır:

```powershell
$GWName = "TestVNetAA1GW"
$VNetName = "TestVNetAA1"
$RG = "TestVPNActiveActive01"
$GWIPName2 = "gwpip2"
$GWIPconf2 = "gw1ipconf2"

$vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$location = $gw.Location
```

#### <a name="2-create-hello-public-ip-address-then-add-hello-second-gateway-ip-configuration"></a>2. Merhaba genel IP adresi oluşturun, sonra hello ikinci ağ geçidi IP Yapılandırması Ekle

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-hello-gateway"></a>3. Etkin-etkin modu ve güncelleştirme hello ağ geçidini etkinleştir
PowerShell tootrigger hello gerçek güncelleştirmesi hello ağ geçidi nesnesi ayarlamanız gerekir. Standart olarak daha önce oluşturulmasından bu yana (yeniden boyutlandırılan) tooHighPerformance hello hello sanal ağ geçidi SKU'su aynı zamanda değiştirilmesi gerekir.

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

Bu güncelleştirme 30 too45 dakika sürebilir.

### <a name="configure-an-active-active-gateway-tooactive-standby-gateway"></a>Etkin-etkin ağ geçidi tooactive bekleme ağ geçidini yapılandırma
#### <a name="1-gateway-parameters"></a>1. Ağ geçidi parametreleri
Kullanım hello aynı yukarıdaki gibi parametreleri almak istediğiniz hello IP yapılandırmasının hello adı tooremove.

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-hello-gateway-ip-configuration-and-disable-hello-active-active-mode"></a>2. Merhaba ağ geçidi IP yapılandırmasını kaldırıp hello etkin-etkin modu devre dışı bırakma
Benzer şekilde, PowerShell tootrigger hello gerçek güncelleştirmesi hello ağ geçidi nesnesi ayarlamanız gerekir.

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

Bu güncelleştirme too30 çok 45 dakika sürebilir.

## <a name="next-steps"></a>Sonraki adımlar
Bağlantınız tamamlandıktan sonra sanal makineleri tooyour sanal ağları ekleyebilirsiniz. Adımlar için bkz. [Sanal Makine Oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
