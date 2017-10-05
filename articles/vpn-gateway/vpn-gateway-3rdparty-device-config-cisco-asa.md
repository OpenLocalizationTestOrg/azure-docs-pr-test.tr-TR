---
title: "Örnek Yapılandırması - Cisco ASA cihaz için Azure VPN ağ geçitlerini bağlama | Microsoft Docs"
description: "Bu makale Azure VPN ağ geçitleri için bağlanma Cisco ASA cihaz için örnek bir yapılandırma sağlar."
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
ms.openlocfilehash: 10466b8928e2cd687f7961a2956b6d60823b82be
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="sample-configuration-cisco-asa-device-ikev2no-bgp"></a>Örnek Yapılandırması: Cisco ASA aygıt (Ikev2/Hayır BGP)
Bu makale Azure VPN ağ geçitleri için bağlanan Cisco ASA cihazları için örnek yapılandırmalarını sağlar.

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
> 1. Yapılandırma bir Azure için Cisco ASA bağlanmasındakiyle **rota tabanlı** açıklandığı gibi özel IPSec/IKE İlkesi "UserPolicyBasedTrafficSelectors" seçeneğiyle kullanarak VPN ağ geçidi [bu makalede](vpn-gateway-connect-multiple-policybased-rm-ps.md).
> 2. ASA cihazlarının kullanmasını gerektirir **Ikev2** erişim listesi temel yapılandırmalarla VTI tabanlı değil.
> 3. Lütfen ilke şirket içi VPN cihazlarınızı üzerinde desteklenen emin olmak için VPN cihaz Satıcı belirtimleri başvurun.

## <a name="vpn-device-requirements"></a>VPN cihaz gereksinimleri
Azure VPN ağ geçitleri standart IPSec/IKE protokolü paketleri S2S VPN tünelleri oluşturmak için kullanın. Başvurmak [VPN cihazları hakkında](vpn-gateway-about-vpn-devices.md) Azure VPN ağ geçitleri için varsayılan şifreleme algoritmaları ve ayrıntılı IPSec/IKE protokol parametreleri için. Bölümünde açıklandığı gibi isteğe bağlı olarak şifreleme algoritmaları ve anahtar gücü belirli bir bağlantı için tam birleşimini belirtebilirsiniz [şifreleme gereksinimleri hakkında](vpn-gateway-about-compliance-crypto.md). Lütfen şifreleme algoritmaları ve anahtar gücü belirli bir bileşimini seçerseniz, VPN aygıtlarınızda karşılık gelen belirtimleri kullandığınızdan emin olun.

## <a name="single-vpn-tunnel"></a>Tek VPN tüneli
Bu topoloji bir Azure VPN ağ geçidi ve şirket içi VPN cihazınız arasındaki tek S2S VPN tüneli oluşur. İsteğe bağlı olarak VPN tüneli üzerinden BGP yapılandırabilirsiniz.

![tek tünel](./media/vpn-gateway-3rdparty-device-config-cisco-asa/singletunnel.png)

Başvurmak [tek tünel Kurulum](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) Azure yapılandırmalarını oluşturmak ayrıntılı, adım adım yönergeler için.

### <a name="network-and-vpn-gateway-information"></a>Ağ ve VPN ağ geçidi bilgileri
Bu bölümde listesinde parametreleri için bu örnek.

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

Aşağıdaki tabloda IPSec/IKE algoritmaları ve örnekte kullanılan parametreler listelenmektedir. Lütfen yukarıda listelenen tüm algoritmalar, VPN aygıt modelleri ve bellenim sürümleri tarafından desteklendiğinden emin olmak için VPN aygıt belirtimlerine bakın.

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
> 3. AES-GCM ve IPSec bütünlüğüyle SHA-256, SHA-384, SHA-512 desteği ile IPSec şifrelemesini gerektiren ASA sürüm 9.x yeni ASA donanımda; ASA 5505, 5510, 5520, 5540, 5550, 5580 olan **değil** desteklenir. (Lütfen onaylamak için satıcı belirtimlerine bakın.)
>


### <a name="sample-device-configurations"></a>Örnek cihaz yapılandırması
Aşağıdaki komut dosyası topoloji ve yukarıda listelenen parametreleri temel alarak örnek bir yapılandırma sağlar. S2S VPN tüneli yapılandırma aşağıdaki bölümlerden oluşur:

1. Arabirimleri & yolları
2. Erişim listeleri
3. IKE İlkesi ve parametreleri (1. aşaması veya ana mod)
4. IPSec ilkesi ve parametreleri (Aşama 2 veya hızlı mod)
5. Diğer parametreler (TCP MSS clamping, vb.)

>[!IMPORTANT] 
>Lütfen aşağıda listelenen ek yapılandırmayı tamamlamak ve yer tutucular yerine gerçek değerler ile emin olun:
> 
> - Arabirim yapılandırması için hem iç ve Dış arabirimler
> - İç/özel ve dış/genel ağlar için yollar
> - Tüm adlarını ve ilke numaralarını cihazda benzersiz olduğundan emin olun
> - Şifreleme algoritmaları aygıtınızda desteklenen olduğundan emin olun
> - Aşağıdaki yer tutucu gerçek değerlerle değiştirin
>   - Arabirim adı dışında: "dış"
>   - Azure_Gateway_Public_IP
>   - OnPrem_Device_Public_IP
>   - IKE Pre_Shared_Key
>   - Sanal ağ ve yerel ağ geçidi adları (vnetname adlı, LNGName)
>   - VNet ve şirket içi adres öneklerini ağ
>   - Uygun ağ maskeleri

#### <a name="sample-configuration"></a>Örnek Yapılandırması

```
! Sample ASA configuration for connecting to Azure VPN gateway
!
! Tested hardware: ASA 5505
! Tested version:  ASA version 9.2(4)
!
! Replace the following place holders with your actual values:
!   - Interface names - default are "outside" and "inside"
!   - <Azure_Gateway_Public_IP>
!   - <OnPrem_Device_Public_IP>
!   - <Pre_Shared_Key>
!   - <VNetName>*
!   - <LNGName>* ==> LocalNetworkGateway - the Azure resource that represents the
!     on-premises network, specifies network prefixes, device public IP, BGP info, etc.
!   - <PrivateIPAddress> ==> Replace it with a private IP address if applicable
!   - <Netmask> ==> Replace it with appropriate netmasks
!   - <Nexthop> ==> Replace it with the actual nexthop IP address
!
! (*) Must be unique names in the device configuration
!
! ==> Interface & route configurations
!
!     > <OnPrem_Device_Public_IP> address on the outside interface or vlan
!     > <PrivateIPAddress> on the inside interface or vlan; e.g., 10.51.0.1/24
!     > Route to connect to <Azure_Gateway_Public_IP> address
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
!       (1) Allow S2S VPN tunnels between the ASA and the Azure gateway public IP address
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
!     > Object group that corresponding to the <LNGName> prefixes.
!       E.g., 10.51.0.0/16 and 10.52.0.0/16. Note that LNG = "local network gateway".
!       In Azure network resource, a local network gateway defines the on-premises
!       network properties (address prefixes, VPN device IP, BGP ASN, etc.)
!
object-group network <LNGName>
 description On-Premises network <LNGName> prefixes
 network-object 10.51.0.0 255.255.0.0
 network-object 10.52.0.0 255.255.0.0
exit
!
!     > Specify the access-list between the Azure VNet and your on-premises network.
!       This access list defines the IPsec SA traffic selectors.
!
access-list Azure-<VNetName>-acl extended permit ip object-group <LNGName> object-group Azure-<VNetName>
!
!     > No NAT required between the on-premises network and Azure VNet
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
!       - Make sure the policy number is not used
!       - integrity and prf must be the same
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
!       - This sample uses "Azure-<VNetName>-map" as the crypto map name
!       - ASA supports only one crypto map per interface, if you already have
!         an existing crypto map assigned to your outside interface, you must use
!         the same crypto map name, but with a different sequence number for
!         this policy
!       - "match address" policy uses the access-list "Azure-<VNetName>-acl" defined 
!         previously
!       - "ipsec-proposal" uses the proposal "AES-256" defined previously 
!       - PFS groups 14 and beyond requires ASA version 9.x.
!
crypto map Azure-<VNetName>-map 1 match address Azure-<VNetName>-acl
crypto map Azure-<VNetName>-map 1 set pfs group24
crypto map Azure-<VNetName>-map 1 set peer <Azure_Gateway_Public_IP>
crypto map Azure-<VNetName>-map 1 set ikev2 ipsec-proposal AES-256
crypto map Azure-<VNetName>-map 1 set security-association lifetime seconds 7200
crypto map Azure-<VNetName>-map interface outside
!
! ==> Set TCP MSS to 1350
!
sysopt connection tcpmss 1350
!
```

## <a name="simple-debugging-commands"></a>Basit hata ayıklama komutları

Hata ayıklama amacıyla bazı ASA komutlar şunlardır:

1. IPSec ve IKE SA'ın Göster
    - "şifre IPSec Göster sa"
    - "crypto Göster IKEv2 sa"
2. Girme hata ayıklama modu - bu konsolda çok gürültülü alabilirsiniz
    - "hata ayıklama şifre IKEv2 platform <level>"
    - "hata ayıklama şifre IKEv2 Protokolü <level>"
3. Liste geçerli yapılandırmaları
    - "Göster" Çalıştır - cihazda geçerli yapılandırmaları gösterir; Liste belirli bölümlerine yapılandırmanın çeşitli alt komutlarını kullanabilirsiniz. Örn., "Çalıştır Göster crypto", "Çalıştır Göster erişim listesinde", "Çalıştır Göster tünel grubu", vb.


## <a name="next-steps"></a>Sonraki adımlar
Etkin-etkin şirket içi ve dışı ile Sanal Ağdan Sanal Ağa bağlantıları yapılandırma adımları için bkz. [Şirket İçi ve Dışı ile Sanal Ağdan Sanal Ağa Bağlantılar için Etkin-Etkin VPN Gateways Yapılandırma](vpn-gateway-activeactive-rm-powershell.md).

