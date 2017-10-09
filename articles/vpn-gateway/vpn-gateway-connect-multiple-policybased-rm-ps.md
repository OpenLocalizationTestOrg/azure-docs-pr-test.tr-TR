---
title: "Azure VPN ağ geçitleri toomultiple şirket içi ilke tabanlı VPN aygıtlarını bağlamak: Azure Resource Manager: PowerShell | Microsoft Docs"
description: "Bu makalede Azure Resource Manager ve PowerShell kullanarak Azure yol tabanlı VPN ağ geçidi toomultiple ilke tabanlı VPN aygıtları nasıl yapılandıracağınız anlatılmaktadır."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/27/2017
ms.author: yushwang
ms.openlocfilehash: 866c78d96305207106a66cc3300c355e4b6bfbb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-vpn-gateways-toomultiple-on-premises-policy-based-vpn-devices-using-powershell"></a>PowerShell kullanarak Azure VPN ağ geçitleri toomultiple şirket içi ilke tabanlı VPN aygıtlarını bağlamak

Bu makalede özel IPSec/IKE ilkeler S2S VPN bağlantılarında yararlanan bir Azure yol tabanlı VPN ağ geçidi tooconnect toomultiple şirket içi ilke tabanlı VPN aygıtları yapılandırmanıza yardımcı olur.

## <a name="about-policy-based-and-route-based-vpn-gateways"></a>İlke tabanlı ve rota tabanlı VPN ağ geçitleri hakkında

İlke - *karşılaştırması* rota tabanlı VPN aygıtları farklı hello IPSec trafiği seçici bir bağlantıda nasıl ayarlanır:

* **İlke tabanlı** VPN aygıtları nasıl trafiği şifrelenmiş/şifresi IPSec tüneller hem ağları toodefine ön ekleri hello birleşimlerini kullanın. Bu genelde paket filtreleme gerçekleştiren güvenlik duvarı cihazlarda yerleşik olarak bulunur. IPSec tüneli şifreleme ve şifre çözme toohello paket filtreleme ve işleme altyapısı eklenir.
* **Rota tabanlı** let yönlendirme iletme tabloları doğrudan trafiği toodifferent IPSec tünelleri ve VPN aygıtları kullanın herhangi herhangi (joker karakterler) trafiği seçicileri. Genellikle, burada her IPSec tüneli bir ağ arabirimi veya VTI (sanal tünel arabirimi) olarak modellenir yönlendirici platformlarda oluşturulmuştur.

Merhaba aşağıdaki diyagramlarda hello iki modeli vurgula:

### <a name="policy-based-vpn-example"></a>İlke tabanlı VPN örneği
![İlke tabanlı](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a>Rota tabanlı VPN örneği
![Rota tabanlı](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a>Azure ilke temelli VPN desteği
Şu anda Azure VPN ağ geçitlerinin iki modlarını destekler: rota tabanlı VPN ağ geçitleri ve ilke tabanlı VPN ağ geçitleri. Farklı teknik özelliklerine sonucunda, farklı platformlarda iç oluşturulur:

|                          | **PolicyBased VPN ağ geçidi** | **RouteBased VPN ağ geçidi**               |
| ---                      | ---                         | ---                                      |
| **Azure ağ geçidi SKU'su**    | Temel                       | Temel, standart, HighPerformance         |
| **IKE sürümü**          | IKEv1                       | IKEv2                                    |
| **Maks. S2S bağlantılarının** | **1**                       | Basic/standart: 10<br> HighPerformance: 30 |
|                          |                             |                                          |

Merhaba özel IPSec/IKE ilkesiyle Azure rota tabanlı VPN ağ geçitleri toouse öneki tabanlı trafik Seçici seçeneği ile artık yapılandırabilirsiniz "**PolicyBasedTrafficSelectors**", tooconnect tooon içi ilke tabanlı VPN aygıtları. Bu özellik bir Azure sanal ağdan tooconnect sağlar ve VPN ağ geçidi toomultiple ilke tabanlı VPN/güvenlik duvarı aygıtları hello tek bağlantı sınırı hello geçerli Azure ilke tabanlı VPN Gateway bileşenlerinden kaldırma, şirket içi.

> [!IMPORTANT]
> 1. tooenable Bu bağlantı, şirket içi ilke tabanlı VPN aygıtları desteklemelidir **Ikev2** tooconnect toohello Azure yol tabanlı VPN ağ geçitleri. VPN aygıt belirtimlerine bakın.
> 2. Merhaba şirket içi ağlar ile bu düzenek ilke tabanlı VPN aygıtları bağlanma yalnızca toohello Azure sanal ağı bağlanabilir; **tooother şirket içi ağlar transit olamaz veya aracılığıyla sanal ağlar aynı Azure VPN ağ geçidi hello**.
> 3. Merhaba yapılandırma seçeneği hello özel IPSec/IKE bağlantı İlkesi bir parçasıdır. Merhaba ilke tabanlı trafik Seçici seçeneği etkinleştirirseniz, hello tam İlkesi (IPSec/IKE şifreleme ve bütünlük algoritmalar, anahtar gücü ve SA yaşam süreleri) belirtmeniz gerekir.

Aşağıdaki diyagramda hello Azure VPN ağ geçidi transit yönlendirme hello ilke tabanlı seçeneğiyle neden çalışmıyor gösterir:

![İlke tabanlı geçiş](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

Hello diyagramda gösterildiği gibi hello Azure VPN ağ geçidi hello sanal ağ tooeach hello şirket içi ağ önekleri ancak hello arası bağlantı önekleri gelen trafik Seçici vardır. Örneğin, şirket içi site 2, 3 site ve site 4 her tooVNet1 sırasıyla iletişim kurabilir ancak hello Azure VPN ağ geçidi tooeach diğer bağlanamıyor. Merhaba diyagramda gösterilmektedir hello hello Azure VPN ağ geçidi bu yapılandırma bölümünde kullanılamayan trafiğini Seçici arası bağlanın.

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a>İlke tabanlı trafik seçici bir bağlantıda yapılandırın

Merhaba bu makalede İzleme'ndaki yönergeleri aynı hello açıklandığı gibi örnek [S2S veya VNet-VNet bağlantıları için IPSec/IKE yapılandırma İlkesi](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish S2S VPN bağlantısı. Bu diyagramda aşağıdaki hello gösterilir:

![s2s İlkesi](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

İş akışı tooenable Bu bağlantı hello:
1. Hello sanal ağ, VPN ağ geçidi ve yerel ağ geçidi, şirket içi bağlantı oluşturma
2. Bir IPSec/IKE ilkesi oluşturun
3. S2S veya VNet-VNet bağlantısı oluşturduğunuzda hello ilkesi uygulamak ve **hello ilke tabanlı trafik Seçici etkinleştirmek** hello bağlantısı
4. Merhaba bağlantıyı zaten oluşturduysanız, uygulama veya hello İlkesi tooan var olan bağlantıyı güncelleştir

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a>İlke tabanlı trafik seçici bir bağlantısı etkinleştir

Tamamladığınızdan emin olun [bölümü 3 hello IPSec/IKE yapılandırma İlkesi makalenin](vpn-gateway-ipsecikepolicy-rm-powershell.md) Bu bölüm için. örnek kullanımları aşağıdaki hello aynı parametreleri ve adımları hello:

### <a name="step-1---create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>1. adım - hello sanal ağ, VPN ağ geçidi ve yerel ağ geçidi oluşturma

#### <a name="1-declare-your-variables--connect-tooyour-subscription"></a>1. Değişkenlerinizi bildirme & tooyour. abonelik'e bağlanma
Bu alıştırmada, değişkenlerimizi bildirerek başlayın. Üretim için yapılandırma emin tooreplace hello değerleri kendi değerlerinizle olabilir.

```powershell
$Sub1          = "<YourSubscriptionName>"
$RG1           = "TestPolicyRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GW1IPName1    = "VNet1GWIP1"
$GW1IPconf1    = "gw1ipconf1"
$Connection16  = "VNet1toSite6"

$LNGName6      = "Site6"
$LNGPrefix61   = "10.61.0.0/16"
$LNGPrefix62   = "10.62.0.0/16"
$LNGIP6        = "131.107.72.22"
```
toouse hello Resource Manager cmdlet'lerini tooPowerShell moduna geçtiğinizden emin olun. Daha fazla bilgi için [Windows PowerShell’i Resource Manager ile kullanma](../powershell-azure-resource-manager.md) konusuna bakın.

PowerShell Konsolunuzu açın ve tooyour hesap bağlanın. Bağlandığınız örnek toohelp aşağıdaki hello kullan:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>2. Merhaba sanal ağ, VPN ağ geçidi ve yerel ağ geçidi oluşturma
Aşağıdaki örneğine hello hello sanal ağ, TestVNet1 üç alt ağları ve hello VPN ağ geçidi ile oluşturur. Değerleri değiştirerek, ağ geçidi alt ağınızı her zaman özellikle 'GatewaySubnet' adını önemlidir. Başka bir ad kullanırsanız ağ geçidi oluşturma işleminiz başarısız olur.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

$gw1pip1    = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1      = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance

New-AzureRmLocalNetworkGateway -Name $LNGName6 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP6 -AddressPrefix $LNGPrefix61,$LNGPrefix62
```

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a>2. adım - bir IPSec/IKE İlkesi ile bir S2S VPN bağlantısı oluşturun

#### <a name="1-create-an-ipsecike-policy"></a>1. Bir IPSec/IKE ilkesi oluşturun

> [!IMPORTANT]
> Toocreate sipariş tooenable "UsePolicyBasedTrafficSelectors" seçeneği hello bağlantı IPSec/IKE ilkesinde gerekir.

Merhaba aşağıdaki örnekte bir IPSec/IKE İlkesi bu algoritmaları ve parametreleri oluşturur:
* Ikev2: AES256, SHA384 DHGroup24
* IPSec: AES256, SHA256, PFS24, SA ömrü 3600 saniye & 2048KB

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a>2. İlke tabanlı trafik Seçici ve IPSec/IKE İlkesi ile Merhaba S2S VPN bağlantısı oluşturun
S2S VPN bağlantısı oluşturun ve hello önceki adımda oluşturduğunuz hello IPSec/IKE İlkesi uygulayın. Merhaba ek parametresinin unutmayın "-UsePolicyBasedTrafficSelectors $True" Merhaba bağlantıda ilke tabanlı trafik Seçici sağlar.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

Hello adımları tamamladıktan sonra hello S2S VPN bağlantısı hello IPSec/IKE ilkesi tanımlı kullanın ve ilke tabanlı trafik Seçici hello bağlantıda etkinleştirin. Daha fazla bağlantıları tooadditional şirket içi ilke tabanlı VPN aygıtlardan aynı adımları tooadd hello yineleyebilirsiniz hello aynı Azure VPN ağ geçidi.

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a>İlke tabanlı trafik Seçici bağlantı güncelleştir
Merhaba son Kısım nasıl var olan bir S2S VPN bağlantısı için tooupdate hello ilke tabanlı trafik Seçici seçeneği gösterir.

### <a name="1-get-hello-connection"></a>1. Merhaba bağlantısını Al
Merhaba bağlantı kaynağı alın.

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-hello-policy-based-traffic-selectors-option"></a>2. Merhaba ilke tabanlı trafik Seçici seçeneği işaretleyin.
Merhaba aşağıdaki satırı hello ilke tabanlı trafik Seçici hello bağlantı için kullanılıp kullanılmadığını gösterir:

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

Merhaba satır döndürürse "**True**", ardından ilke tabanlı trafik Seçici hello bağlantısında yapılandırılmış; Aksi halde döndürür "**False**."

### <a name="3-update-hello-policy-based-traffic-selectors-on-a-connection"></a>3. Merhaba ilke tabanlı trafik seçici bir bağlantısı güncelleştir
Merhaba bağlantı kaynağı edindikten sonra etkinleştirebilir veya hello seçeneğini devre dışı bırakın.

#### <a name="disable-usepolicybasedtrafficselectors"></a>UsePolicyBasedTrafficSelectors devre dışı bırak
Merhaba aşağıdaki örnek hello ilke tabanlı trafik Seçici seçeneği devre dışı bırakır, ancak IPSec/IKE İlkesi değiştirmeden bırakır hello:

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a>UsePolicyBasedTrafficSelectors etkinleştir
Merhaba aşağıdaki örnek hello ilke tabanlı trafik Seçici seçeneği sağlar, ancak IPSec/IKE İlkesi değiştirmeden bırakır hello:

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a>Sonraki adımlar
Bağlantınız tamamlandıktan sonra sanal makineleri tooyour sanal ağları ekleyebilirsiniz. Adımlar için bkz. [Sanal Makine Oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Ayrıca gözden [S2S VPN veya VNet-VNet bağlantıları için IPSec/IKE yapılandırma İlkesi](vpn-gateway-ipsecikepolicy-rm-powershell.md) özel IPSec/IKE ilkeleri hakkında daha fazla ayrıntı için.
