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
# <a name="router-configuration-samples-tooset-up-and-manage-routing"></a><span data-ttu-id="c34f0-103">Yönlendirici yapılandırması yukarı tooset örnekleri ve yönlendirme yönetme</span><span class="sxs-lookup"><span data-stu-id="c34f0-103">Router configuration samples tooset up and manage routing</span></span>
<span data-ttu-id="c34f0-104">Bu sayfa için Cisco IOS-XE ve Juniper MX series yönlendirici arabirimi ve yönlendirme yapılandırma örnekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="c34f0-104">This page provides interface and routing configuration samples for Cisco IOS-XE and Juniper MX series routers.</span></span> <span data-ttu-id="c34f0-105">Bunlar yalnızca kılavuzu için hedeflenen toobe örnekleri ve olarak kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="c34f0-105">These are intended toobe samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="c34f0-106">İle satıcı toocome uygun yapılandırmalarla ağınız için çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c34f0-106">You can work with your vendor toocome up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c34f0-107">Bu sayfayı örneklerinde zamanıyla ilgili yönergeler için hedeflenen toobe ' dir.</span><span class="sxs-lookup"><span data-stu-id="c34f0-107">Samples in this page are intended toobe purely for guidance.</span></span> <span data-ttu-id="c34f0-108">Gereksinimlerinize satıcınızın satış / teknik ekibi ve, ağ takım toocome yukarı uygun yapılandırmaları toomeet ile birlikte çalışmalısınız.</span><span class="sxs-lookup"><span data-stu-id="c34f0-108">You must work with your vendor's sales / technical team and your networking team toocome up with appropriate configurations toomeet your needs.</span></span> <span data-ttu-id="c34f0-109">Microsoft olmayan sorunlar destek ilgili bu sayfada listelenen tooconfigurations.</span><span class="sxs-lookup"><span data-stu-id="c34f0-109">Microsoft will not support issues related tooconfigurations listed in this page.</span></span> <span data-ttu-id="c34f0-110">Destek sorunları için aygıt satıcınıza başvurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c34f0-110">You must contact your device vendor for support issues.</span></span>
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a><span data-ttu-id="c34f0-111">Yönlendirici arabirimleri MTU ve TCP MSS ayarları</span><span class="sxs-lookup"><span data-stu-id="c34f0-111">MTU and TCP MSS settings on router interfaces</span></span>
* <span data-ttu-id="c34f0-112">Merhaba MTU hello ExpressRoute arabirimi için bir Ethernet arabirimi bir yönlendiricideki hello tipik varsayılan MTU, 1500, olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="c34f0-112">hello MTU for hello ExpressRoute interface is 1500, which is hello typical default MTU for an Ethernet interface on a router.</span></span> <span data-ttu-id="c34f0-113">Yönlendiriciniz varsayılan olarak farklı bir MTU olmadıkça hello yönlendirici arabiriminde bir değer yok gerek toospecify yoktur.</span><span class="sxs-lookup"><span data-stu-id="c34f0-113">Unless your router has a different MTU by default, there is no need toospecify a value on hello router interface.</span></span>
* <span data-ttu-id="c34f0-114">Bir Azure VPN ağ geçidi, bir expressroute bağlantı hattı için TCP MSS hello belirtilen toobe gerekmez.</span><span class="sxs-lookup"><span data-stu-id="c34f0-114">Unlike an Azure VPN Gateway, hello TCP MSS for an ExpressRoute circuit does not need toobe specified.</span></span>

<span data-ttu-id="c34f0-115">Yönlendirici yapılandırma örnekleri aşağıdaki tooall eşlemeler uygulayın.</span><span class="sxs-lookup"><span data-stu-id="c34f0-115">Router configuration samples below apply tooall peerings.</span></span> <span data-ttu-id="c34f0-116">Gözden geçirme [ExpressRoute eşlemeler](expressroute-circuit-peerings.md) ve [ExpressRoute yönlendirme gereksinimleri](expressroute-routing.md) yönlendirme hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="c34f0-116">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute routing requirements](expressroute-routing.md) for more details on routing.</span></span>


## <a name="cisco-ios-xe-based-routers"></a><span data-ttu-id="c34f0-117">Yönlendiriciler Cisco IOS-XE tabanlı</span><span class="sxs-lookup"><span data-stu-id="c34f0-117">Cisco IOS-XE based routers</span></span>
<span data-ttu-id="c34f0-118">Bu bölümdeki Hello örnekler hello IOS XE işletim sistemi ailesi çalıştıran bir yönlendirici için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="c34f0-118">hello samples in this section apply for any router running hello IOS-XE OS family.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="c34f0-119">1. Arabirimleri ve alt arabirimleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c34f0-119">1. Configuring interfaces and sub-interfaces</span></span>
<span data-ttu-id="c34f0-120">Bir alt arabirim başına her yönlendiriciye eşliği bağlanmak tooMicrosoft gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c34f0-120">You will require a sub interface per peering in every router you connect tooMicrosoft.</span></span> <span data-ttu-id="c34f0-121">Bir alt arabirimi, bir VLAN kimliği veya yığın çiftinin VLAN kimlikleri ve bir IP adresi ile tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="c34f0-121">A sub interface can be identified with a VLAN ID or a stacked pair of VLAN IDs and an IP address.</span></span>

<span data-ttu-id="c34f0-122">**Dot1Q arabirim tanımı**</span><span class="sxs-lookup"><span data-stu-id="c34f0-122">**Dot1Q interface definition**</span></span>

<span data-ttu-id="c34f0-123">Bu örnek bir alt arabiriminin tek bir VLAN kimliği hello alt arabirim tanımı sağlar</span><span class="sxs-lookup"><span data-stu-id="c34f0-123">This sample provides hello sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="c34f0-124">Merhaba VLAN ID eşliği başına benzersizdir.</span><span class="sxs-lookup"><span data-stu-id="c34f0-124">hello VLAN ID is unique per peering.</span></span> <span data-ttu-id="c34f0-125">Merhaba son sekizli IPv4 adresinizin her zaman tek sayı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c34f0-125">hello last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

<span data-ttu-id="c34f0-126">**QinQ arabirim tanımı**</span><span class="sxs-lookup"><span data-stu-id="c34f0-126">**QinQ interface definition**</span></span>

<span data-ttu-id="c34f0-127">Bu örnek hello alt arabirim tanımı iki VLAN kimliği ile alt bir arabirim sağlar.</span><span class="sxs-lookup"><span data-stu-id="c34f0-127">This sample provides hello sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="c34f0-128">Dış VLAN kimliği (s-kullandıysanız etiketi), kaldığı hello hello aynı tüm hello eşlemeleri.</span><span class="sxs-lookup"><span data-stu-id="c34f0-128">hello outer VLAN ID (s-tag), if used remains hello same across all hello peerings.</span></span> <span data-ttu-id="c34f0-129">Merhaba iç VLAN kimliği (c-tag) eşliği başına benzersizdir.</span><span class="sxs-lookup"><span data-stu-id="c34f0-129">hello inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="c34f0-130">Merhaba son sekizli IPv4 adresinizin her zaman tek sayı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c34f0-130">hello last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="c34f0-131">2. EBGP oturumları ayarlama</span><span class="sxs-lookup"><span data-stu-id="c34f0-131">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="c34f0-132">Her eşleme için Microsoft ile bir BGP oturumu kurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c34f0-132">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="c34f0-133">Aşağıdaki Hello örneği bir BGP oturumu Microsoft ile toosetup sağlar.</span><span class="sxs-lookup"><span data-stu-id="c34f0-133">hello sample below enables you toosetup a BGP session with Microsoft.</span></span> <span data-ttu-id="c34f0-134">Merhaba alt arabiriminiz için kullanılan bir IPv4 adresi a.b.c.d olduysa, başlangıç IP adresi hello BGP komşu (Microsoft) a.b.c.d+1 olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c34f0-134">If hello IPv4 address you used for your sub interface was a.b.c.d, hello IP address of hello BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="c34f0-135">Merhaba son hello BGP komşu'nın IPv4 adresi sekizlisi her zaman bir çift sayı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c34f0-135">hello last octet of hello BGP neighbor's IPv4 address will always be an even number.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a><span data-ttu-id="c34f0-136">3. Önekleri toobe ayarlama hello BGP oturumu üzerinden tanıtılan</span><span class="sxs-lookup"><span data-stu-id="c34f0-136">3. Setting up prefixes toobe advertised over hello BGP session</span></span>
<span data-ttu-id="c34f0-137">Yönlendirici tooadvertise select önekleri tooMicrosoft yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c34f0-137">You can configure your router tooadvertise select prefixes tooMicrosoft.</span></span> <span data-ttu-id="c34f0-138">Aşağıdaki örneği kullanarak hello şekilde bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c34f0-138">You can do so using hello sample below.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a><span data-ttu-id="c34f0-139">4. Rotayı eşler</span><span class="sxs-lookup"><span data-stu-id="c34f0-139">4. Route maps</span></span>
<span data-ttu-id="c34f0-140">Önek ağınıza yayılan toofilter öneklerini listeler ve rota haritaları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c34f0-140">You can use route-maps and prefix lists toofilter prefixes propagated into your network.</span></span> <span data-ttu-id="c34f0-141">Tooaccomplish hello görev aşağıda hello örneği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c34f0-141">You can use hello sample below tooaccomplish hello task.</span></span> <span data-ttu-id="c34f0-142">Uygun önek listeleri Kurulum olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c34f0-142">Ensure that you have appropriate prefix lists setup.</span></span>

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


## <a name="juniper-mx-series-routers"></a><span data-ttu-id="c34f0-143">Juniper MX series yönlendirici</span><span class="sxs-lookup"><span data-stu-id="c34f0-143">Juniper MX series routers</span></span>
<span data-ttu-id="c34f0-144">Bu bölümdeki Hello örnekler Juniper MX serisi yönlendiricilerden için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="c34f0-144">hello samples in this section apply for any Juniper MX series routers.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="c34f0-145">1. Arabirimleri ve alt arabirimleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c34f0-145">1. Configuring interfaces and sub-interfaces</span></span>

<span data-ttu-id="c34f0-146">**Dot1Q arabirim tanımı**</span><span class="sxs-lookup"><span data-stu-id="c34f0-146">**Dot1Q interface definition**</span></span>

<span data-ttu-id="c34f0-147">Bu örnek bir alt arabiriminin tek bir VLAN kimliği hello alt arabirim tanımı sağlar</span><span class="sxs-lookup"><span data-stu-id="c34f0-147">This sample provides hello sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="c34f0-148">Merhaba VLAN ID eşliği başına benzersizdir.</span><span class="sxs-lookup"><span data-stu-id="c34f0-148">hello VLAN ID is unique per peering.</span></span> <span data-ttu-id="c34f0-149">Merhaba son sekizli IPv4 adresinizin her zaman tek sayı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c34f0-149">hello last octet of your IPv4 address will always be an odd number.</span></span>

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


<span data-ttu-id="c34f0-150">**QinQ arabirim tanımı**</span><span class="sxs-lookup"><span data-stu-id="c34f0-150">**QinQ interface definition**</span></span>

<span data-ttu-id="c34f0-151">Bu örnek hello alt arabirim tanımı iki VLAN kimliği ile alt bir arabirim sağlar.</span><span class="sxs-lookup"><span data-stu-id="c34f0-151">This sample provides hello sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="c34f0-152">Dış VLAN kimliği (s-kullandıysanız etiketi), kaldığı hello hello aynı tüm hello eşlemeleri.</span><span class="sxs-lookup"><span data-stu-id="c34f0-152">hello outer VLAN ID (s-tag), if used remains hello same across all hello peerings.</span></span> <span data-ttu-id="c34f0-153">Merhaba iç VLAN kimliği (c-tag) eşliği başına benzersizdir.</span><span class="sxs-lookup"><span data-stu-id="c34f0-153">hello inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="c34f0-154">Merhaba son sekizli IPv4 adresinizin her zaman tek sayı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c34f0-154">hello last octet of your IPv4 address will always be an odd number.</span></span>

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

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="c34f0-155">2. EBGP oturumları ayarlama</span><span class="sxs-lookup"><span data-stu-id="c34f0-155">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="c34f0-156">Her eşleme için Microsoft ile bir BGP oturumu kurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c34f0-156">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="c34f0-157">Aşağıdaki Hello örneği bir BGP oturumu Microsoft ile toosetup sağlar.</span><span class="sxs-lookup"><span data-stu-id="c34f0-157">hello sample below enables you toosetup a BGP session with Microsoft.</span></span> <span data-ttu-id="c34f0-158">Merhaba alt arabiriminiz için kullanılan bir IPv4 adresi a.b.c.d olduysa, başlangıç IP adresi hello BGP komşu (Microsoft) a.b.c.d+1 olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c34f0-158">If hello IPv4 address you used for your sub interface was a.b.c.d, hello IP address of hello BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="c34f0-159">Merhaba son hello BGP komşu'nın IPv4 adresi sekizlisi her zaman bir çift sayı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c34f0-159">hello last octet of hello BGP neighbor's IPv4 address will always be an even number.</span></span>

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

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a><span data-ttu-id="c34f0-160">3. Önekleri toobe ayarlama hello BGP oturumu üzerinden tanıtılan</span><span class="sxs-lookup"><span data-stu-id="c34f0-160">3. Setting up prefixes toobe advertised over hello BGP session</span></span>
<span data-ttu-id="c34f0-161">Yönlendirici tooadvertise select önekleri tooMicrosoft yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c34f0-161">You can configure your router tooadvertise select prefixes tooMicrosoft.</span></span> <span data-ttu-id="c34f0-162">Aşağıdaki örneği kullanarak hello şekilde bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c34f0-162">You can do so using hello sample below.</span></span>

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


### <a name="4-route-maps"></a><span data-ttu-id="c34f0-163">4. Rotayı eşler</span><span class="sxs-lookup"><span data-stu-id="c34f0-163">4. Route maps</span></span>
<span data-ttu-id="c34f0-164">Önek ağınıza yayılan toofilter öneklerini listeler ve rota haritaları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c34f0-164">You can use route-maps and prefix lists toofilter prefixes propagated into your network.</span></span> <span data-ttu-id="c34f0-165">Tooaccomplish hello görev aşağıda hello örneği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c34f0-165">You can use hello sample below tooaccomplish hello task.</span></span> <span data-ttu-id="c34f0-166">Uygun önek listeleri Kurulum olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c34f0-166">Ensure that you have appropriate prefix lists setup.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c34f0-167">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="c34f0-167">Next Steps</span></span>
<span data-ttu-id="c34f0-168">Merhaba bkz [ExpressRoute SSS](expressroute-faqs.md) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="c34f0-168">See hello [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

