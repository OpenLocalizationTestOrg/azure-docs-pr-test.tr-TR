---
title: "aaaExpressRoute müşteri yönlendirici yapılandırma örnekleri | Microsoft Docs"
description: "Bu sayfa için Cisco ve Juniper yönlendirici yönlendirici yapılandırma örnekleri sağlar."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 564826bc-017a-4683-a385-37c9fa814948
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: cherylmc
ms.openlocfilehash: 5c91f24e6082e01c3e8df91b4fcfda46a6c29fa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="router-configuration-samples-tooset-up-and-manage-routing"></a>Yönlendirici yapılandırması yukarı tooset örnekleri ve yönlendirme yönetme
Bu sayfa için Cisco IOS-XE ve Juniper MX series yönlendirici arabirimi ve yönlendirme yapılandırma örnekleri sağlar. Bunlar yalnızca kılavuzu için hedeflenen toobe örnekleri ve olarak kullanılmamalıdır. İle satıcı toocome uygun yapılandırmalarla ağınız için çalışabilirsiniz. 

> [!IMPORTANT]
> Bu sayfayı örneklerinde zamanıyla ilgili yönergeler için hedeflenen toobe ' dir. Gereksinimlerinize satıcınızın satış / teknik ekibi ve, ağ takım toocome yukarı uygun yapılandırmaları toomeet ile birlikte çalışmalısınız. Microsoft olmayan sorunlar destek ilgili bu sayfada listelenen tooconfigurations. Destek sorunları için aygıt satıcınıza başvurmanız gerekir.
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a>Yönlendirici arabirimleri MTU ve TCP MSS ayarları
* Merhaba MTU hello ExpressRoute arabirimi için bir Ethernet arabirimi bir yönlendiricideki hello tipik varsayılan MTU, 1500, olmasıdır. Yönlendiriciniz varsayılan olarak farklı bir MTU olmadıkça hello yönlendirici arabiriminde bir değer yok gerek toospecify yoktur.
* Bir Azure VPN ağ geçidi, bir expressroute bağlantı hattı için TCP MSS hello belirtilen toobe gerekmez.

Yönlendirici yapılandırma örnekleri aşağıdaki tooall eşlemeler uygulayın. Gözden geçirme [ExpressRoute eşlemeler](expressroute-circuit-peerings.md) ve [ExpressRoute yönlendirme gereksinimleri](expressroute-routing.md) yönlendirme hakkında daha fazla bilgi.


## <a name="cisco-ios-xe-based-routers"></a>Yönlendiriciler Cisco IOS-XE tabanlı
Bu bölümdeki Hello örnekler hello IOS XE işletim sistemi ailesi çalıştıran bir yönlendirici için geçerlidir.

### <a name="1-configuring-interfaces-and-sub-interfaces"></a>1. Arabirimleri ve alt arabirimleri yapılandırma
Bir alt arabirim başına her yönlendiriciye eşliği bağlanmak tooMicrosoft gerektirir. Bir alt arabirimi, bir VLAN kimliği veya yığın çiftinin VLAN kimlikleri ve bir IP adresi ile tanımlanabilir.

**Dot1Q arabirim tanımı**

Bu örnek bir alt arabiriminin tek bir VLAN kimliği hello alt arabirim tanımı sağlar Merhaba VLAN ID eşliği başına benzersizdir. Merhaba son sekizli IPv4 adresinizin her zaman tek sayı olacaktır.

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

**QinQ arabirim tanımı**

Bu örnek hello alt arabirim tanımı iki VLAN kimliği ile alt bir arabirim sağlar. Dış VLAN kimliği (s-kullandıysanız etiketi), kaldığı hello hello aynı tüm hello eşlemeleri. Merhaba iç VLAN kimliği (c-tag) eşliği başına benzersizdir. Merhaba son sekizli IPv4 adresinizin her zaman tek sayı olacaktır.

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a>2. EBGP oturumları ayarlama
Her eşleme için Microsoft ile bir BGP oturumu kurmanız gerekir. Aşağıdaki Hello örneği bir BGP oturumu Microsoft ile toosetup sağlar. Merhaba alt arabiriminiz için kullanılan bir IPv4 adresi a.b.c.d olduysa, başlangıç IP adresi hello BGP komşu (Microsoft) a.b.c.d+1 olacaktır. Merhaba son hello BGP komşu'nın IPv4 adresi sekizlisi her zaman bir çift sayı olacaktır.

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a>3. Önekleri toobe ayarlama hello BGP oturumu üzerinden tanıtılan
Yönlendirici tooadvertise select önekleri tooMicrosoft yapılandırabilirsiniz. Aşağıdaki örneği kullanarak hello şekilde bunu yapabilirsiniz.

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a>4. Rotayı eşler
Önek ağınıza yayılan toofilter öneklerini listeler ve rota haritaları kullanabilirsiniz. Tooaccomplish hello görev aşağıda hello örneği kullanabilirsiniz. Uygun önek listeleri Kurulum olduğundan emin olun.

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
      neighbor <IP#2_used_by_Azure> route-map <MS_Prefixes_Inbound> in
     exit-address-family
    !
    route-map <MS_Prefixes_Inbound> permit 10
     match ip address prefix-list <MS_Prefixes>
    !


## <a name="juniper-mx-series-routers"></a>Juniper MX series yönlendirici
Bu bölümdeki Hello örnekler Juniper MX serisi yönlendiricilerden için geçerlidir.

### <a name="1-configuring-interfaces-and-sub-interfaces"></a>1. Arabirimleri ve alt arabirimleri yapılandırma

**Dot1Q arabirim tanımı**

Bu örnek bir alt arabiriminin tek bir VLAN kimliği hello alt arabirim tanımı sağlar Merhaba VLAN ID eşliği başına benzersizdir. Merhaba son sekizli IPv4 adresinizin her zaman tek sayı olacaktır.

    interfaces {
        vlan-tagging;
        <Interface_Number> {
            unit <Number> {
                vlan-id <VLAN_ID>;
                family inet {
                    address <IPv4_Address/Subnet_Mask>;
                }
            }
        }
    }


**QinQ arabirim tanımı**

Bu örnek hello alt arabirim tanımı iki VLAN kimliği ile alt bir arabirim sağlar. Dış VLAN kimliği (s-kullandıysanız etiketi), kaldığı hello hello aynı tüm hello eşlemeleri. Merhaba iç VLAN kimliği (c-tag) eşliği başına benzersizdir. Merhaba son sekizli IPv4 adresinizin her zaman tek sayı olacaktır.

    interfaces {
        <Interface_Number> {
            flexible-vlan-tagging;
            unit <Number> {
                vlan-tags outer <S-tag> inner <C-tag>;
                family inet {
                    address <IPv4_Address/Subnet_Mask>;
                }                           
            }                               
        }                                   
    }                           

### <a name="2-setting-up-ebgp-sessions"></a>2. EBGP oturumları ayarlama
Her eşleme için Microsoft ile bir BGP oturumu kurmanız gerekir. Aşağıdaki Hello örneği bir BGP oturumu Microsoft ile toosetup sağlar. Merhaba alt arabiriminiz için kullanılan bir IPv4 adresi a.b.c.d olduysa, başlangıç IP adresi hello BGP komşu (Microsoft) a.b.c.d+1 olacaktır. Merhaba son hello BGP komşu'nın IPv4 adresi sekizlisi her zaman bir çift sayı olacaktır.

    routing-options {
        autonomous-system <Customer_ASN>;
    }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a>3. Önekleri toobe ayarlama hello BGP oturumu üzerinden tanıtılan
Yönlendirici tooadvertise select önekleri tooMicrosoft yapılandırabilirsiniz. Aşağıdaki örneği kullanarak hello şekilde bunu yapabilirsiniz.

    policy-options {
        policy-statement <Policy_Name> {
            term 1 {
                from protocol OSPF;
        route-filter <Prefix_to_be_advertised/Subnet_Mask> exact;
                then {
                    accept;
                }
            }
        }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                export <Policy_Name>
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }


### <a name="4-route-maps"></a>4. Rotayı eşler
Önek ağınıza yayılan toofilter öneklerini listeler ve rota haritaları kullanabilirsiniz. Tooaccomplish hello görev aşağıda hello örneği kullanabilirsiniz. Uygun önek listeleri Kurulum olduğundan emin olun.

    policy-options {
        prefix-list MS_Prefixes {
            <IP_Prefix_1/Subnet_Mask>;
            <IP_Prefix_2/Subnet_Mask>;
        }
        policy-statement <MS_Prefixes_Inbound> {
            term 1 {
                from {
        prefix-list MS_Prefixes;
                }
                then {
                    accept;
                }
            }
        }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                export <Policy_Name>
                import <MS_Prefixes_Inbound>
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }

## <a name="next-steps"></a>Sonraki Adımlar
Merhaba bkz [ExpressRoute SSS](expressroute-faqs.md) daha fazla ayrıntı için.

