---
title: "aaaSample yapılandırması - Cisco ASA aygıt tooAzure VPN ağ geçitlerini bağlama | Microsoft Docs"
description: "Bu makale tooAzure VPN ağ geçitlerini bağlama Cisco ASA cihaz için örnek bir yapılandırma sağlar."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: dad13e02afe8dad2379db750eb09602e08e8ea99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-configuration-cisco-asa-device-ikev2no-bgp"></a>Örnek Yapılandırması: Cisco ASA aygıt (Ikev2/Hayır BGP)
Bu makale tooAzure VPN ağ geçitlerini bağlama Cisco ASA cihazlar için örnek yapılandırmalarını sağlar.

## <a name="device-at-a-glance"></a>Bir bakışta cihaz

|                        |                                   |
| ---                    | ---                               |
| Cihaz satıcısından          | Cisco                             |
| Cihaz modeli           | ASA (Uyarlamalı güvenlik Gereci) |
| Hedef sürümü         | 8.4+                              |
| Sınanan modeli           | ASA 5505                          |
| Test edilen sürüm         | 9.2                               |
| IKE sürümü            | **Ikev2**                         |
| BGP                    | **Hayır**                            |
| Azure VPN ağ geçidi türü | **Rota tabanlı** VPN ağ geçidi       |
|                        |                                   |

> [!NOTE]
> 1. Aşağıdaki başlangıç yapılandırmasına bağlandığında bir Cisco ASA aygıt tooan Azure **rota tabanlı** açıklandığı gibi özel IPSec/IKE İlkesi "UserPolicyBasedTrafficSelectors" seçeneğiyle kullanarak VPN ağ geçidi [bu makalede](vpn-gateway-connect-multiple-policybased-rm-ps.md).
> 2. ASA aygıtları toouse gerektirir **Ikev2** erişim listesi temel yapılandırmalarla VTI tabanlı değil.
> 3. Şirket içi VPN cihazlarınızı tooensure hello İlkesi desteklenen VPN cihaz Satıcı belirtimleri başvurun.

## <a name="vpn-device-requirements"></a>VPN cihaz gereksinimleri
Azure VPN ağ geçitleri standart IPSec/IKE protokolü paketleri tooestablish S2S VPN tünelleri kullanın. Çok başvuran[VPN cihazları hakkında](vpn-gateway-about-vpn-devices.md) Merhaba IPSec/IKE protokolü parametreleri ve Azure VPN ağ geçitleri için varsayılan şifreleme algoritmalarının ayrıntılı. Bölümünde açıklandığı gibi hello tam birleşimini şifreleme algoritmaları ve anahtar gücü belirli bir bağlantı için isteğe bağlı olarak belirtebilirsiniz [şifreleme gereksinimleri hakkında](vpn-gateway-about-compliance-crypto.md). Lütfen şifreleme algoritmaları ve anahtar gücü belirli bir bileşimini seçerseniz, VPN aygıtlarınızda hello karşılık gelen belirtimleri kullandığınızdan emin olun.

## <a name="single-vpn-tunnel"></a>Tek VPN tüneli
Bu topoloji bir Azure VPN ağ geçidi ve şirket içi VPN cihazınız arasındaki tek S2S VPN tüneli oluşur. BGP hello VPN tüneli üzerinden isteğe bağlı olarak yapılandırabilirsiniz.

![tek tünel](./media/vpn-gateway-3rdparty-device-config-cisco-asa/singletunnel.png)

Çok başvuran[tek tünel Kurulum](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) ayrıntılı için adım adım yönergeler toobuild hello Azure yapılandırmaları.

### <a name="network-and-vpn-gateway-information"></a>Ağ ve VPN ağ geçidi bilgileri
Bu bölümde, bu örnek hello hello parametrelerini listeler.

| **Parametre**                | **Değer**                    |
| ---                          | ---                          |
| VNet adres önekleri        | 10.11.0.0/16<br>10.12.0.0/16 |
| Azure VPN ağ geçidi IP         | Azure_Gateway_Public_IP      |
| Şirket içi adres önekleri | 10.51.0.0/16<br>10.52.0.0/16 |
| Şirket içi VPN cihazının IP    | OnPrem_Device_Public_IP     |
| * VNet BGP ASN                | 65010                        |
| * Azure BGP eşdeğer IP           | 10.12.255.30                 |
| * Şirket içi BGP ASN         | 65050                        |
| * Şirket içi BGP eşdeğer IP     | 10.52.255.254                |
|                              |                              |

* (*) İsteğe bağlı parametreleri BGP yalnızca.

### <a name="ipsecike-policy--parameters"></a>IPSec/IKE İlkesi & parametreleri

Merhaba tabloda hello IPSec/IKE algoritmaları ve hello örnekte kullanılan parametreleri listeler. Lütfen, VPN aygıt belirtimlerine toomake yukarıda listelenen tüm algoritmalar, VPN aygıt modelleri ve bellenim sürümleri tarafından desteklendiğinden emin bakın.

| **IPsec/IKEv2**  | **Değer**                            |
| ---              | ---                                  |
| IKEv2 Şifrelemesi | AES256                               |
| IKEv2 Bütünlüğü  | SHA384                               |
| DH Grubu         | DHGroup24                            |
| IPsec Şifrelemesi | AES256                               |
| IPsec Bütünlüğü  | SHA1                                 |
| PFS Grubu        | PFS24                                |
| QM SA Yaşam Süresi   | 7200 saniye                         |
| Trafik Seçicisi | UsePolicyBasedTrafficSelectors $True |
| Önceden Paylaşılan Anahtar   | PreSharedKey                         |
|                  |                                      |

- (*) Bazı cihazlarda IPSec bütünlüğünü "GCM AES IPSec şifreleme algoritması olarak kullanılıyorsa, null" olması gerekir.

### <a name="device-notes"></a>Cihaz notları

>[!NOTE]
>
> 1. Ikev2 desteği, ASA sürüm 8.4 gerektirir ve üstü.
> 2. (Ötesinde Grup 5) daha yüksek DH ve PFS grubu desteği ASA sürümünü gerektirir 9.x.
> 3. AES-GCM ve IPSec bütünlüğüyle SHA-256, SHA-384, SHA-512 desteği ile IPSec şifrelemesini gerektiren ASA sürüm 9.x yeni ASA donanımda; ASA 5505, 5510, 5520, 5540, 5550, 5580 olan **değil** desteklenir. (Merhaba Satıcı belirtimleri tooconfirm gözden geçirin.)
>


### <a name="sample-device-configurations"></a>Örnek cihaz yapılandırması
Merhaba topolojisine bağlı örnek bir yapılandırma ve yukarıda listelenen parametreleri aşağıdaki Hello komut dosyası sağlar. Merhaba S2S VPN tüneli yapılandırma bölümü aşağıdaki Merhaba oluşur:

1. Arabirimleri & yolları
2. Erişim listeleri
3. IKE İlkesi ve parametreleri (1. aşaması veya ana mod)
4. IPSec ilkesi ve parametreleri (Aşama 2 veya hızlı mod)
5. Diğer parametreler (TCP MSS clamping, vb.)

>[!IMPORTANT] 
>Lütfen aşağıda listelenen hello ek yapılandırmayı tamamlamak ve hello yer tutucuları hello gerçek değerlerle değiştirin emin olun:
> 
> - Arabirim yapılandırması için hem iç ve Dış arabirimler
> - İç/özel ve dış/genel ağlar için yollar
> - Tüm adlarını ve ilke numaralarını hello aygıtta benzersiz olduğundan emin olun
> - Merhaba şifreleme algoritmaları aygıtınızda desteklenen olduğundan emin olun
> - Yer tutucu hello gerçek değerlerle aşağıdaki hello değiştirin
>   - Arabirim adı dışında: "dış"
>   - Azure_Gateway_Public_IP
>   - OnPrem_Device_Public_IP
>   - IKE Pre_Shared_Key
>   - Sanal ağ ve yerel ağ geçidi adları (vnetname adlı, LNGName)
>   - VNet ve şirket içi adres öneklerini ağ
>   - Uygun ağ maskeleri

#### <a name="sample-configuration"></a>Örnek Yapılandırması

```
! Sample ASA configuration for connecting tooAzure VPN gateway
!
! Tested hardware: ASA 5505
! Tested version:  ASA version 9.2(4)
!
! Replace hello following place holders with your actual values:
!   - Interface names - default are "outside" and "inside"
!   - <Azure_Gateway_Public_IP>
!   - <OnPrem_Device_Public_IP>
!   - <Pre_Shared_Key>
!   - <VNetName>*
!   - <LNGName>* ==> LocalNetworkGateway - hello Azure resource that represents the
!     on-premises network, specifies network prefixes, device public IP, BGP info, etc.
!   - <PrivateIPAddress> ==> Replace it with a private IP address if applicable
!   - <Netmask> ==> Replace it with appropriate netmasks
!   - <Nexthop> ==> Replace it with hello actual nexthop IP address
!
! (*) Must be unique names in hello device configuration
!
! ==> Interface & route configurations
!
!     > <OnPrem_Device_Public_IP> address on hello outside interface or vlan
!     > <PrivateIPAddress> on hello inside interface or vlan; e.g., 10.51.0.1/24
!     > Route tooconnect too<Azure_Gateway_Public_IP> address
!
!     > Example:
!
!       interface Ethernet0/0
!        switchport access vlan 2
!       exit
!
!       interface vlan 1
!        nameif inside
!        security-level 100
!        ip address <PrivateIPAddress> <Netmask>
!       exit
!
!       interface vlan 2
!        nameif outside
!        security-level 0
!        ip address <OnPrem_Device_Public_IP> <Netmask>
!       exit
!
!       route outside 0.0.0.0 0.0.0.0 <NextHop IP> 1
!
! ==> Access lists
!
!     > Most firewall devices deny all traffic by default. Create access lists to
!       (1) Allow S2S VPN tunnels between hello ASA and hello Azure gateway public IP address
!       (2) Construct traffic selectors as part of IPsec policy or proposal
!
access-list outside_access_in extended permit ip host <Azure_Gateway_Public_IP> host <OnPrem_Device_Public_IP>
!
!     > Object group that consists of all VNet prefixes (e.g., 10.11.0.0/16 &
!       10.12.0.0/16)
!
object-group network Azure-<VNetName>
 description Azure virtual network <VNetName> prefixes
 network-object 10.11.0.0 255.255.0.0
 network-object 10.12.0.0 255.255.0.0
exit
!
!     > Object group that corresponding toohello <LNGName> prefixes.
!       E.g., 10.51.0.0/16 and 10.52.0.0/16. Note that LNG = "local network gateway".
!       In Azure network resource, a local network gateway defines hello on-premises
!       network properties (address prefixes, VPN device IP, BGP ASN, etc.)
!
object-group network <LNGName>
 description On-Premises network <LNGName> prefixes
 network-object 10.51.0.0 255.255.0.0
 network-object 10.52.0.0 255.255.0.0
exit
!
!     > Specify hello access-list between hello Azure VNet and your on-premises network.
!       This access list defines hello IPsec SA traffic selectors.
!
access-list Azure-<VNetName>-acl extended permit ip object-group <LNGName> object-group Azure-<VNetName>
!
!     > No NAT required between hello on-premises network and Azure VNet
!
nat (inside,outside) source static <LNGName> <LNGName> destination static Azure-<VNetName> Azure-<VNetName>
!
! ==> IKEv2 configuration
!
!     > General IKEv2 configuration - enable IKEv2 for VPN
!
group-policy DfltGrpPolicy attributes
 vpn-tunnel-protocol ikev1 ikev2
exit
!
crypto isakmp identity address
crypto ikev2 enable outside
!
!     > Define IKEv2 Phase 1/Main Mode policy
!       - Make sure hello policy number is not used
!       - integrity and prf must be hello same
!       - DH group 14 and above require ASA version 9.x.
!
crypto ikev2 policy 1
 encryption       aes-256
 integrity        sha384
 prf              sha384
 group            24
 lifetime seconds 86400
exit
!
!     > Set connection type and pre-shared key
!
tunnel-group <Azure_Gateway_Public_IP> type ipsec-l2l
tunnel-group <Azure_Gateway_Public_IP> ipsec-attributes
 ikev2 remote-authentication pre-shared-key <Pre_Shared_Key> 
 ikev2 local-authentication  pre-shared-key <Pre_Shared_Key> 
exit
!
! ==> IPsec configuration
!
!     > IKEv2 Phase 2/Quick Mode proposal
!       - AES-GCM and SHA-2 requires ASA version 9.x on newer ASA models. ASA
!         5505, 5510, 5520, 5540, 5550, 5580 are not supported.
!       - ESP integrity must be null if AES-GCM is configured as ESP encryption
!
crypto ipsec ikev2 ipsec-proposal AES-256
 protocol esp encryption aes-256
 protocol esp integrity  sha-1
exit
!
!     > Set access list & traffic selectors, PFS, IPsec protposal, SA lifetime
!       - This sample uses "Azure-<VNetName>-map" as hello crypto map name
!       - ASA supports only one crypto map per interface, if you already have
!         an existing crypto map assigned tooyour outside interface, you must use
!         hello same crypto map name, but with a different sequence number for
!         this policy
!       - "match address" policy uses hello access-list "Azure-<VNetName>-acl" defined 
!         previously
!       - "ipsec-proposal" uses hello proposal "AES-256" defined previously 
!       - PFS groups 14 and beyond requires ASA version 9.x.
!
crypto map Azure-<VNetName>-map 1 match address Azure-<VNetName>-acl
crypto map Azure-<VNetName>-map 1 set pfs group24
crypto map Azure-<VNetName>-map 1 set peer <Azure_Gateway_Public_IP>
crypto map Azure-<VNetName>-map 1 set ikev2 ipsec-proposal AES-256
crypto map Azure-<VNetName>-map 1 set security-association lifetime seconds 7200
crypto map Azure-<VNetName>-map interface outside
!
! ==> Set TCP MSS too1350
!
sysopt connection tcpmss 1350
!
```

## <a name="simple-debugging-commands"></a>Basit hata ayıklama komutları

Hata ayıklama amacıyla bazı ASA komutlar şunlardır:

1. Göster IPSec ve IKE SA'ın hello
    - "şifre IPSec Göster sa"
    - "crypto Göster IKEv2 sa"
2. Girme hata ayıklama modu - bu hello konsolda çok gürültülü alabilirsiniz
    - "hata ayıklama şifre IKEv2 platform <level>"
    - "hata ayıklama şifre IKEv2 Protokolü <level>"
3. Liste geçerli yapılandırmaları
    - "çalışma Göster" - gösterir geçerli yapılandırmaları hello aygıtta hello; kullanabileceğiniz çeşitli alt komutları toolist belirli kısımlarını hello yapılandırma hello. Örn., "Çalıştır Göster crypto", "Çalıştır Göster erişim listesinde", "Çalıştır Göster tünel grubu", vb.


## <a name="next-steps"></a>Sonraki adımlar
Bkz: [yapılandırma etkin-etkin VPN ağ geçitleri için şirket içi ve VNet-VNet bağlantıları](vpn-gateway-activeactive-rm-powershell.md) adımları tooconfigure etkin-etkin şirket içi ve VNet-VNet bağlantıları için.

