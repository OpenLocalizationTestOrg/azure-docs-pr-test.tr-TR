---
title: "S2S VPN veya VNet-VNet bağlantıları için IPSec/IKE ilkesi yapılandırın: Azure Resource Manager: PowerShell | Microsoft Docs"
description: "Bu makalede Azure Resource Manager ve PowerShell kullanarak Azure VPN Gateway'ler ile IPSec/IKE İlkesi S2S veya VNet-VNet bağlantıları için nasıl yapılandıracağınız anlatılmaktadır."
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
ms.date: 05/12/2017
ms.author: yushwang
ms.openlocfilehash: f8d2e29276efdec7071f2aa0d463b1abd64a5253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ipsecike-policy-for-s2s-vpn-or-vnet-to-vnet-connections"></a>S2S VPN veya VNet-VNet bağlantıları için IPSec/IKE ilkesi yapılandırma

Bu makalede, hello adımları tooconfigure hello Resource Manager dağıtım modeli ve PowerShell kullanarak siteden siteye VPN veya VNet-VNet bağlantıları için IPSec/IKE İlkesi adım adım anlatılmaktadır.

## <a name="about"></a>IPSec ve IKE İlkesi parametreleri hakkında Azure VPN ağ geçitleri için
IPSec ve IKE protokolü standart çeşitli bileşimlerde çok çeşitli şifreleme algoritmalarını destekler. Çok başvuran[şifreleme gereksinimleri ve Azure VPN ağ geçitleri hakkında](vpn-gateway-about-compliance-crypto.md) toosee nasıl bu yardımcı şirketler arası ve VNet-VNet bağlantısı sağlayarak, uyumluluk ve güvenlik gereksinimleri karşılar.

Bu makalede yönergeleri toocreate sağlar ve bir IPSec/IKE ilkesi yapılandırma ve tooa yeni veya var olan bağlantı Uygula:

* [Bölüm 1 - iş akışı toocreate ve IPSec/IKE ilkesini ayarlama](#workflow)
* [Desteklenen bölüm 2 - şifreleme algoritmaları ve anahtar gücü](#params)
* [Bölüm 3 - IPSec/IKE İlkesi ile yeni bir S2S VPN bağlantısı oluşturma](#crossprem)
* [4 Kısım - yeni bir VNet-VNet bağlantı IPSec/IKE ilkesiyle oluşturun.](#vnet2vnet)
* [Bölüm 5 - yönetme (oluşturma, ekleme, kaldırma) bir bağlantı için IPSec/IKE İlkesi](#managepolicy)

> [!IMPORTANT]
> 1. IPSec/IKE ilkesi yalnızca ağ geçidi SKU'ları aşağıdaki hello üzerinde çalıştığını unutmayın:
>    * ***VpnGw1, VpnGw2, VpnGw3*** (rota tabanlı)
>    * ***Standart*** ve ***HighPerformance*** (rota tabanlı)
> 2. Belirli bir bağlantı için yalnızca ***bir*** ilke birleşimi belirtebilirsiniz.
> 3. IKE (ana mod) ve IPSec (hızlı mod) için tüm algoritmalar ve parametreleri belirtmeniz gerekir. Kısmi ilke belirtimine izin verilmez.
> 4. Şirket içi VPN cihazlarınızı tooensure hello İlkesi desteklenen VPN cihaz Satıcı belirtimleri başvurun. Merhaba ilkeleri uyumlu olup olmadığını S2S veya VNet-VNet bağlantı kurulamıyor.

## <a name ="workflow"></a>Bölüm 1 - iş akışı toocreate ve IPSec/IKE ilkesini ayarlama
Bu bölümde bir S2S VPN veya VNet-VNet bağlantısı hello iş akışı toocreate ve güncelleştirme IPSec/IKE İlkesi özetlenmektedir:
1. Sanal ağ ve VPN ağ geçidi oluşturma
2. Bir şirket içi bağlantı veya başka bir sanal ağ çapraz yerel ağ geçidi için ve VNet-VNet bağlantısı için ağ geçidi oluşturun
3. Seçilen algoritmalar ve parametrelerine sahip bir IPSec/IKE ilkesi oluşturun
4. Merhaba IPSec/IKE ilkesiyle (IPSec veya VNet2VNet) bir bağlantı oluştur
5. Ekleme/güncelleştirme/kaldırma mevcut bir bağlantı için bir IPSec/IKE İlkesi

Bu makaledeki yönergeleri Hello ayarlamak ve hello diyagramda gösterildiği gibi IPSec/IKE ilkelerini yapılandırmanıza yardımcı olur:

![IPSec IKE İlkesi](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)

## <a name ="params"></a>Desteklenen bölüm 2 - şifreleme algoritmaları ve anahtar gücü

Merhaba aşağıdaki tabloda desteklenen hello şifreleme algoritmaları ve anahtar gücü yapılandırılabilir hello müşteriler listelenmektedir:

| **IPsec/IKEv2**  | **Seçenekler**    |
| ---  | --- 
| IKEv2 Şifrelemesi | AES256, AES192, AES128, DES3, DES  
| IKEv2 Bütünlüğü  | SHA384, SHA256, SHA1, MD5  |
| DH Grubu         | DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, yok |
| IPsec Şifrelemesi | GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, None    |
| IPsec Bütünlüğü  | GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5 |
| PFS Grubu        | PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, Hiçbiri 
| QM SA Yaşam Süresi   | (**İsteğe bağlı**: varsayılan değerleri kullanılan belirtilmediğinde)<br>Saniye (tamsayı; **en az 300**/varsayılan 27000 saniye)<br>Kilobayt (tamsayı; **en az 1024**/varsayılan 102400000 kilobayt)   |
| Trafik Seçicisi | UsePolicyBasedTrafficSelectors ** ($True/$False; **İsteğe bağlı**, varsayılan $False belirtilmediğinde)    |
|  |  |

> [!IMPORTANT]
> 1. **GCMAES IPSec şifreleme algoritması için kullanılırsa, seçmelisiniz hello aynı GCMAES algoritması ve anahtar uzunluğu için IPSec bütünlüğü; Örneğin, GCMAES128 her ikisi için kullanma**
> 2. Ikev2 ana mod SA ömrü hello Azure VPN ağ geçitlerinde 28.800 saniyedir adresindeki sabit
> 3. "UsePolicyBasedTrafficSelectors" ayarı $True bir bağlantısı çok yapılandıracak Azure VPN ağ geçidi tooconnect toopolicy tabanlı VPN güvenlik duvarı şirket içi hello. PolicyBasedTrafficSelectors etkinleştirdiğinizde, şirket içi ağ (yerel ağ geçidi) önekleri denetleyicisinden hello Azure sanal ağı önekleri tüm bileşimleri ile tanımlanmış hello eşleşen trafik Seçici VPN Cihazınızı sahip tooensure gerekir, any herhangi yerine. Örneğin, 10.1.0.0/16 ve 10.2.0.0/16, şirket içi ağ ön ekleri ve 192.168.0.0/16 ve 172.16.0.0/16, sanal ağ ön ekleri, trafik Seçici aşağıdaki toospecify hello gerekir:
>    * 10.1.0.0/16 <====> 192.168.0.0/16
>    * 10.1.0.0/16 <====> 172.16.0.0/16
>    * 10.2.0.0/16 <====> 192.168.0.0/16
>    * 10.2.0.0/16 <====> 172.16.0.0/16

İlke tabanlı trafik Seçici ile ilgili daha fazla bilgi için bkz: [birden çok şirket içi ilke tabanlı VPN aygıtlarını bağlamak](vpn-gateway-connect-multiple-policybased-rm-ps.md).

Aşağıdaki tabloda hello hello özel ilke tarafından desteklenen karşılık gelen Diffie-Hellman grupları hello:

| **Diffie-Hellman Grubu**  | **DHGroup**              | **PFSGroup** | **Anahtar uzunluğu** |
| --- | --- | --- | --- |
| 1                         | DHGroup1                 | PFS1         | 768 bit MODP   |
| 2                         | DHGroup2                 | PFS2         | 1024 bit MODP  |
| 14                        | DHGroup14<br>DHGroup2048 | PFS2048      | 2048 bit MODP  |
| 19                        | ECP256                   | ECP256       | 256 bit ECP    |
| 20                        | ECP384                   | ECP284       | 384 bit ECP    |
| 24                        | DHGroup24                | PFS24        | 2048 bit MODP  |

Çok başvuran[RFC3526](https://tools.ietf.org/html/rfc3526) ve [RFC5114](https://tools.ietf.org/html/rfc5114) daha fazla ayrıntı için.

## <a name ="crossprem"></a>Bölüm 3 - IPSec/IKE İlkesi ile yeni bir S2S VPN bağlantısı oluşturma

Bu bölümde, bir IPSec/IKE ilkesiyle S2S VPN bağlantısı oluşturma hello adım adım anlatılmaktadır. Merhaba aşağıdaki adımları hello bağlantı hello diyagramda gösterildiği gibi oluşturun:

![s2s İlkesi](./media/vpn-gateway-ipsecikepolicy-rm-powershell/s2spolicy.png)

Bkz: [S2S VPN bağlantısı oluşturmak](vpn-gateway-create-site-to-site-rm-powershell.md) daha ayrıntılı bir S2S VPN bağlantısı oluşturmak için adım adım yönergeler için.

### <a name="before"></a>Başlamadan önce

* Azure aboneliğiniz olduğunu doğrulayın. Henüz Azure aboneliğiniz yoksa [MSDN abonelik avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) etkinleştirebilir veya [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.
* Hello Azure Resource Manager PowerShell cmdlet'lerini yükleyin. Bkz: [Azure PowerShell genel bakış](/powershell/azure/overview) hello PowerShell cmdlet'lerini yükleme hakkında daha fazla bilgi.

### <a name="createvnet1"></a>1. adım - hello sanal ağ, VPN ağ geçidi ve yerel ağ geçidi oluşturma

#### <a name="1-declare-your-variables"></a>1. Değişkenlerinizi bildirme

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

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Tooyour abonelik bağlanın ve yeni bir kaynak grubu oluştur

TooPowerShell modu toouse hello Resource Manager cmdlet'lerini geçtiğinizden emin olun. Daha fazla bilgi için [Windows PowerShell’i Resource Manager ile kullanma](../powershell-azure-resource-manager.md) konusuna bakın.

PowerShell Konsolunuzu açın ve tooyour hesap bağlanın. Bağlandığınız örnek toohelp aşağıdaki hello kullan:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>3. Merhaba sanal ağ, VPN ağ geçidi ve yerel ağ geçidi oluşturma

Aşağıdaki örnek hello hello sanal ağ, TestVNet1, üç alt ağ ve hello VPN ağ geçidi ile oluşturur. Kendi değerlerinizi yerleştirirken ağ geçidi alt ağınızı özellikle GatewaySubnet olarak adlandırmanız önem taşır. Başka bir ad kullanırsanız ağ geçidi oluşturma işleminiz başarısız olur.

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

### <a name="s2sconnection"></a>2. adım - bir IPSec/IKE İlkesi ile bir S2S VPN bağlantısı oluşturun

#### <a name="1-create-an-ipsecike-policy"></a>1. Bir IPSec/IKE ilkesi oluşturun

Aşağıdaki örnek betik hello oluşturur bir IPSec/IKE İlkesi ile Merhaba algoritmaları ve parametreleri aşağıdaki:

* Ikev2: AES256, SHA384 DHGroup24
* IPSec: AES256, SHA256, PFS24, SA ömrü 7200 saniye & 2048KB

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

IPSec için GCMAES kullanıyorsanız, kullanmalısınız aynı GCMAES algoritması ve anahtar uzunluğu IPSec şifreleme ve bütünlüğünü hello örneğin:

* Ikev2: AES256, SHA384 DHGroup24
* IPSec: **GCMAES256, GCMAES256**, PFS24, SA ömrü 7200 saniye & 2048 KB

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption GCMAES256 -IpsecIntegrity GCMAES256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-hello-ipsecike-policy"></a>2. IPSec/IKE İlkesi hello ile Merhaba S2S VPN bağlantısı oluşturun

S2S VPN bağlantısı oluşturun ve daha önce oluşturduğunuz hello IPSec/IKE İlkesi uygulayın.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

İsteğe bağlı olarak ekleyebileceğiniz "-UsePolicyBasedTrafficSelectors $True" toohello oluşturmak bağlantı cmdlet tooenable Azure VPN ağ geçidi tooconnect toopolicy tabanlı VPN aygıtlarını şirket içinde yukarıda açıklandığı gibi.

> [!IMPORTANT]
> Bir IPSec/IKE İlkesi bir bağlantıda belirlendikten sonra hello Azure VPN ağ geçidi yalnızca göndermek veya belirtilen şifreleme algoritmaları ve anahtar gücü belirli bu bağlantıda ile Merhaba IPSec/IKE teklifi kabul edin. Şirket içi VPN aygıtınızın hello bağlantı kullanan veya hello tam İlkesi birleşimi, aksi takdirde hello S2S VPN tüneli değil kuracak kabul emin olun.


## <a name ="vnet2vnet"></a>4 Kısım - yeni bir VNet-VNet bağlantı IPSec/IKE ilkesiyle oluşturun.

bir IPSec/IKE İlkesi ile bir VNet-VNet bağlantısı oluşturma hello S2S VPN bağlantısının benzer toothat adımlardır. Merhaba aşağıdaki örnek komutlar hello bağlantı hello diyagramda gösterildiği gibi oluşturun:

![v2v İlkesi](./media/vpn-gateway-ipsecikepolicy-rm-powershell/v2vpolicy.png)

Bkz: [bir VNet-VNet bağlantısı oluşturma](vpn-gateway-vnet-vnet-rm-ps.md) daha ayrıntılı bir VNet-VNet bağlantı oluşturma adımları için. Tamamlamanız gereken [bölümü 3](#crossprem) toocreate TestVNet1 yapılandırmak ve VPN ağ geçidi hello.

### <a name="createvnet2"></a>1. adım - hello ikinci sanal ağ ve VPN ağ geçidi oluşturma

#### <a name="1-declare-your-variables"></a>1. Değişkenlerinizi bildirme

Merhaba olanları hello değerlerle emin tooreplace olması yapılandırmanızın toouse istiyor.

```powershell
$RG2          = "TestPolicyRG2"
$Location2    = "East US 2"
$VNetName2    = "TestVNet2"
$FESubName2   = "FrontEnd"
$BESubName2   = "Backend"
$GWSubName2   = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$DNS2         = "8.8.8.8"
$GWName2      = "VNet2GW"
$GW2IPName1   = "VNet2GWIP1"
$GW2IPconf1   = "gw2ipconf1"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-hello-second-virtual-network-and-vpn-gateway-in-hello-new-resource-group"></a>2. Merhaba yeni kaynak grubunda Hello ikinci sanal ağ ve VPN ağ geçidi oluşturma

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2

$gw2pip1    = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$vnet2      = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1

New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance
```

### <a name="step-2---create-a-vnet-tovnet-connection-with-hello-ipsecike-policy"></a>2. adım - bir VNet toVNet bağlantı IPSec/IKE İlkesi hello ile oluşturma

Benzer toohello S2S VPN bağlantısı, bir IPSec/IKE ilkesi oluşturun ardından toopolicy toohello yeni bağlantı uygulayın.

#### <a name="1-create-an-ipsecike-policy"></a>1. Bir IPSec/IKE ilkesi oluşturun

Aşağıdaki örnek betik hello hello ile başka bir IPSec/IKE ilke oluşturur algoritmaları ve parametreleri aşağıdaki:
* Ikev2: AES128, SHA1, DHGroup14
* IPSec: GCMAES128, GCMAES128, PFS14, SA ömrü 7200 saniye ve 4096KB

```powershell
$ipsecpolicy2 = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup PFS14 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 4096
```

#### <a name="2-create-vnet-to-vnet-connections-with-hello-ipsecike-policy"></a>2. VNet-VNet bağlantıları hello ile IPSec/IKE ilkesi oluşturma

VNet-VNet bağlantı oluşturun ve oluşturduğunuz hello IPSec/IKE İlkesi uygulayın. Bu örnekte, her iki ağ geçitleri hello olan aynı abonelik. Olası toocreate olduğundan ve her iki bağlantıları ile yapılandırmak için hello aynı IPSec/IKE ilkesinde hello aynı PowerShell oturumunda.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2  -ResourceGroupName $RG2

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'
```

> [!IMPORTANT]
> Bir IPSec/IKE İlkesi bir bağlantıda belirlendikten sonra hello Azure VPN ağ geçidi yalnızca göndermek veya belirtilen şifreleme algoritmaları ve anahtar gücü belirli bu bağlantıda ile Merhaba IPSec/IKE teklifi kabul edin. Hem bağlantılarını olan hello için aynı, aksi takdirde VNet-VNet bağlantısı olmayan kuracak emin hello IPSec ilkeleri hale getirir.

Bu adımları tamamladıktan sonra hello bağlantı birkaç dakika içinde oluşturulur ve ağ topolojisi hello'den itibaren gösterildiği gibi aşağıdaki hello gerekir:

![IPSec IKE İlkesi](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)


## <a name ="managepolicy"></a>Bölüm 5 - bir bağlantı için güncelleştirme IPSec/IKE İlkesi

Merhaba son Kısım gösterir, nasıl toomanage varolan S2S veya VNet-VNet bağlantı IPSec/IKE ilkesi. Merhaba alıştırma aşağıdaki işlemleri bir bağlantısı aşağıdaki hello size yol göstermektedir:

1. Merhaba IPSec/IKE İlkesi bağlantısının Göster
2. Ekleme veya hello IPSec/IKE İlkesi tooa bağlantısını güncelleştir
3. Merhaba IPSec/IKE İlkesi bir bağlantısından Kaldır

Merhaba aynı adımlar tooboth S2S ve VNet-VNet bağlantıları geçerlidir.

> [!IMPORTANT]
> IPSec/IKE İlkesi desteklenir *standart* ve *HighPerformance* rota tabanlı VPN ağ geçitleri yalnızca. Merhaba temel ağ geçidi SKU veya hello ilke tabanlı VPN ağ geçidi çalışmaz.

#### <a name="1-show-hello-ipsecike-policy-of-a-connection"></a>1. Merhaba IPSec/IKE İlkesi bağlantısının Göster

Aşağıdaki örnek hello nasıl tooget hello bağlantı üzerinde yapılandırılmış IPSec/IKE İlkesi gösterir. Merhaba komut dosyaları da alıştırmaları hello yukarıdaki devam edin.

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

varsa hello son komut hello bağlantısında yapılandırılmış hello geçerli IPSec/IKE İlkesi listeler. örnek çıktı aşağıdaki hello hello bağlantı için şöyledir:

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : AES256
IpsecIntegrity      : SHA256
IkeEncryption       : AES256
IkeIntegrity        : SHA384
DhGroup             : DHGroup24
PfsGroup            : PFS24
```

Yapılandırılmış IPSec/IKE İlkesi yok ise, komut hello (PS > $connection6.policy) boş bir dönüş alır. IPSec/IKE hello bağlantısında yapılandırılmamış, ancak hiçbir özel IPSec/IKE ilke olduğu anlamına gelmez. Merhaba gerçek bağlantı hello Azure VPN ağ geçidi ve şirket içi VPN aygıtınızın arasında anlaşılan hello varsayılan ilkesi kullanır.

#### <a name="2-add-or-update-an-ipsecike-policy-for-a-connection"></a>2. Eklemek veya bir bağlantı için bir IPSec/IKE ilkesini güncelleştirin

Merhaba adımları tooadd yeni bir ilke veya var olan bir ilkenin bir bağlantısı olan güncelleştirme aynı hello: yeni bir ilke oluşturun ardından hello yeni ilke toohello bağlantı uygulayın.

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$newpolicy6   = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup None -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6
```

tooenable "tooan bağlanma ilke tabanlı VPN cihazı şirket içi zaman UsePolicyBasedTrafficSelectors" Merhaba Ekle "-UsePolicyBaseTrafficSelectors" parametresi toohello cmdlet'i ya da çok ayarlayın $False toodisable hello seçeneği:

```powershell
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6 -UsePolicyBasedTrafficSelectors $True
```

Merhaba bağlantısını Al yeniden hello İlkesi güncelleştirdiyseniz toocheck.

```powershell
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

Hello aşağıdaki örnekte gösterildiği gibi hello son satırından hello çıktı görmeniz gerekir:

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : GCMAES128
IpsecIntegrity      : GCMAES128
IkeEncryption       : AES128
IkeIntegrity        : SHA1
DhGroup             : DHGroup14--
PfsGroup            : None
```

#### <a name="3-remove-an-ipsecike-policy-from-a-connection"></a>3. Bir IPSec/IKE İlkesi bir bağlantısından Kaldır

Öğesinden bir bağlantı hello özel ilke kaldırdıktan sonra geri toohello hello Azure VPN ağ geçidi döner [IPSec/IKE teklifleri varsayılan listesini](vpn-gateway-about-vpn-devices.md) ve yeniden şirket içi VPN Cihazınızı yeniden anlaşmaya varılır.

```powershell
$RG1           = "TestPolicyRG1"
$Connection16  = "VNet1toSite6"
$connection6   = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$currentpolicy = $connection6.IpsecPolicies[0]
$connection6.IpsecPolicies.Remove($currentpolicy)

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6
```

Kullanabileceğiniz hello İlkesi hello bağlantısından kaldırdıysanız aynı komut dosyasını toocheck hello.

## <a name="next-steps"></a>Sonraki adımlar

Bkz: [birden çok şirket içi ilke tabanlı VPN aygıtlarını bağlamak](vpn-gateway-connect-multiple-policybased-rm-ps.md) ilke tabanlı trafik Seçici ile ilgili daha fazla ayrıntı için.

Bağlantınız tamamlandıktan sonra sanal makineleri tooyour sanal ağları ekleyebilirsiniz. Adımlar için bkz. [Sanal Makine Oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
