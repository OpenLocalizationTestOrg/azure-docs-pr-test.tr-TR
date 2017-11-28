---
title: "Azure siteden siteye VPN bağlantısını keser aralıklı aaaTroubleshoot | Microsoft Docs"
description: "Nasıl tootroubleshoot hello düzenli olarak bağlantısı kesilmiş hangi hello siteden siteye VPN bağlantısı sorun hakkında bilgi edinin."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/21/2017
ms.author: genli
ms.openlocfilehash: 1ce3c4ff9d8f650312e45f33b760ebcc6597fc13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a><span data-ttu-id="af04d-103">Sorun giderme: Azure siteden siteye VPN aralıklı keser</span><span class="sxs-lookup"><span data-stu-id="af04d-103">Troubleshooting: Azure Site-to-Site VPN disconnects intermittently</span></span>

<span data-ttu-id="af04d-104">Yeni veya var olan bir Microsoft Azure noktadan siteye VPN bağlantısı kararlı değilse veya düzenli olarak keser hello sorunla karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af04d-104">You might experience hello problem that a new or existing Microsoft Azure Point-to-Site VPN connection is not stable or disconnects regularly.</span></span> <span data-ttu-id="af04d-105">Bu makalede, sorun giderme adımları toohelp tanımlamak ve hello hello sorunun nedenini çözümleyin sağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="af04d-105">This article provides troubleshoot steps toohelp you identify and resolve hello cause of hello problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="af04d-106">Sorun giderme adımları</span><span class="sxs-lookup"><span data-stu-id="af04d-106">Troubleshooting steps</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="af04d-107">Önkoşul adım</span><span class="sxs-lookup"><span data-stu-id="af04d-107">Prerequisite step</span></span>

<span data-ttu-id="af04d-108">Azure sanal ağ geçidi Hello türünü kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="af04d-108">Check hello type of Azure  virtual network gateway:</span></span>

1. <span data-ttu-id="af04d-109">Çok Git[Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="af04d-109">Go too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="af04d-110">Merhaba denetleyin **genel bakış** hello sanal ağ geçidi hello türü bilgi sayfası.</span><span class="sxs-lookup"><span data-stu-id="af04d-110">Check hello **Overview** page of hello virtual network gateway for hello type information.</span></span>
    
    ![Merhaba ağ geçidi Hello genel bakış](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a><span data-ttu-id="af04d-112">Merhaba VPN cihazı doğrulanır içi olup olmadığını 1 onay adım</span><span class="sxs-lookup"><span data-stu-id="af04d-112">Step 1 Check whether hello on-premises VPN device is validated</span></span>

1. <span data-ttu-id="af04d-113">Kullanmakta olduğunuz olup olmadığını denetleyin bir [VPN cihazı ve işletim sistemi sürümü doğrulandı](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="af04d-113">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="af04d-114">Merhaba VPN cihazı doğrulanmaz, herhangi bir uyumluluk sorunu varsa toocontact hello aygıt üreticisi toosee olabilir.</span><span class="sxs-lookup"><span data-stu-id="af04d-114">If hello VPN device is not validated, you may have toocontact hello device manufacturer toosee if there is any compatibility issue.</span></span>
2. <span data-ttu-id="af04d-115">Bu hello VPN cihazı doğru yapılandırıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="af04d-115">Make sure that hello VPN device is correctly configured.</span></span> <span data-ttu-id="af04d-116">Daha fazla bilgi için bkz: [cihaz yapılandırma örneklerini düzenleme](vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="af04d-116">For more information, see [Editing device configuration samples](vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-check-hello-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a><span data-ttu-id="af04d-117">2. adım onay hello güvenlik ilişkisi ayarlarını (ilke tabanlı Azure sanal ağ geçitleri)</span><span class="sxs-lookup"><span data-stu-id="af04d-117">Step 2 Check hello Security Association settings(for policy-based Azure virtual network gateways)</span></span>

1. <span data-ttu-id="af04d-118">Bu hello sanal ağ, alt ağları ve, aralıkları hello emin olun **yerel ağ geçidi** Microsoft Azure tanımında hello şirket içi VPN cihazı hello yapılandırmasına aynı.</span><span class="sxs-lookup"><span data-stu-id="af04d-118">Make sure that hello virtual network, subnets and, ranges in hello **Local network gateway** definition in Microsoft Azure are same as hello configuration on hello on-premises VPN device.</span></span>
2. <span data-ttu-id="af04d-119">Merhaba güvenlik ilişkisi ayarları eşleşen doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="af04d-119">Verify that hello Security Association settings match.</span></span>

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a><span data-ttu-id="af04d-120">Ağ geçidi alt ağı üzerinde kullanıcı tanımlı yollar veya ağ güvenlik grupları için 3. adım denetimi</span><span class="sxs-lookup"><span data-stu-id="af04d-120">Step 3 Check for User-Defined Routes or Network Security Groups on Gateway Subnet</span></span>

<span data-ttu-id="af04d-121">Bir kullanıcı tarafından tanımlanan rota hello ağ geçidi alt ağı üzerinde bazı trafiği kısıtlama ve diğer trafiğe izin.</span><span class="sxs-lookup"><span data-stu-id="af04d-121">A user-defined route on hello gateway subnet may be restricting some traffic and allowing other traffic.</span></span> <span data-ttu-id="af04d-122">Bu hello VPN bağlantısı güvenilir olmayan bir miktar trafik için ve başkaları için iyi görünmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="af04d-122">This makes it appear that hello VPN connection is unreliable for some traffic and good for others.</span></span> 

### <a name="step-4-check-hello-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="af04d-123">Adım 4 onay "bir VPN tüneli alt ağ çifti başına" Merhaba (ilke tabanlı sanal ağ geçitleri için) ayarlama</span><span class="sxs-lookup"><span data-stu-id="af04d-123">Step 4 Check hello "one VPN Tunnel per Subnet Pair" setting (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="af04d-124">Bu hello şirket içi VPN cihazı toohave ayarlanmış olduğundan emin olun **alt ağ çifti başına bir VPN tüneli** ilke tabanlı sanal ağ geçitleri için.</span><span class="sxs-lookup"><span data-stu-id="af04d-124">Make sure that hello on-premises VPN device is set toohave **one VPN tunnel per subnet pair** for policy-based virtual network gateways.</span></span>

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="af04d-125">Adım 5 (için ilke tabanlı sanal ağ geçitleri) güvenlik ilişkisi sınırlaması denetle</span><span class="sxs-lookup"><span data-stu-id="af04d-125">Step 5 Check for Security Association Limitation (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="af04d-126">Merhaba ilke tabanlı sanal ağ geçidi 200 alt ağ güvenlik ilişkisi çiftleri sınırı vardır.</span><span class="sxs-lookup"><span data-stu-id="af04d-126">hello Policy-based virtual network gateway has limit of 200 subnet Security Association pairs.</span></span> <span data-ttu-id="af04d-127">Azure sanal ağ alt ağları Hello sayısının kez çarpımı varsa hello tarafından yerel alt ağları sayısı 200'den büyükse, kesme durumlarıyla alt bakın.</span><span class="sxs-lookup"><span data-stu-id="af04d-127">If hello number of Azure virtual network subnets multiplied times by hello number of local subnets is greater than 200, you see sporadic subnets disconnecting.</span></span>

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="af04d-128">Adım 6 onay içi VPN cihazı dış arabirimi adresi</span><span class="sxs-lookup"><span data-stu-id="af04d-128">Step 6 Check on-premises VPN device external interface address</span></span>

- <span data-ttu-id="af04d-129">Merhaba, IP adresi hello VPN aygıtının Internet'e hello dahil **yerel ağ geçidi** tanımı Azure'da, kullanımın bağlantısının kesilmesi karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af04d-129">If hello Internet facing IP address of hello VPN device is included in hello **Local network gateway** definition in Azure, you may experience sporadic disconnections.</span></span>
- <span data-ttu-id="af04d-130">Merhaba cihazın dış arabirimi hello üzerinde doğrudan Internet olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="af04d-130">hello device's external interface must be directly on hello Internet.</span></span> <span data-ttu-id="af04d-131">Hiçbir ağ adresi çevirisi (NAT) veya güvenlik duvarı hello Internet ve hello aygıt arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="af04d-131">There should be no Network Address Translation (NAT) or firewall between hello Internet and hello device.</span></span>
-  <span data-ttu-id="af04d-132">Bir sanal IP Güvenlik Duvarı kümeleme toohave yapılandırırsanız, hello küme bölme ve ağ geçidi hello tooa ortak arabirimi ile arabirim doğrudan hello VPN Gereci kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="af04d-132">If you configure Firewall Clustering toohave a virtual IP, you must break hello cluster and expose hello VPN appliance directly tooa public interface that hello gateway can interface with.</span></span>

### <a name="step-7-check-whether-hello-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a><span data-ttu-id="af04d-133">Merhaba içi bağlı VPN cihazı kusursuz iletme etkin gizliliği sahip olup olmadığını 7 onay adım</span><span class="sxs-lookup"><span data-stu-id="af04d-133">Step 7 Check whether hello on-premises VPN device has Perfect Forward Secrecy enabled</span></span>

<span data-ttu-id="af04d-134">Merhaba **kusursuz iletme gizliliği** özelliği hello bağlantı kesme sorunlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="af04d-134">hello **Perfect Forward Secrecy** feature can cause hello disconnection problems.</span></span> <span data-ttu-id="af04d-135">Merhaba VPN cihazı varsa **kusursuz iletme gizliliği** hello özelliği etkinse, devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="af04d-135">If hello VPN device has **Perfect forward Secrecy** enabled, disable hello feature.</span></span> <span data-ttu-id="af04d-136">Ardından [hello sanal ağ geçidi IPSec ilkesi güncelleştirmesi](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span><span class="sxs-lookup"><span data-stu-id="af04d-136">Then [update hello virtual network gateway IPsec policy](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span></span>

## <a name="next-steps"></a><span data-ttu-id="af04d-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="af04d-137">Next steps</span></span>

- [<span data-ttu-id="af04d-138">Siteden siteye bağlantı tooa sanal ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="af04d-138">Configure a Site-to-Site connection tooa virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [<span data-ttu-id="af04d-139">Siteden siteye VPN bağlantıları için IPSec/IKE ilkesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="af04d-139">Configure IPsec/IKE policy for Site-to-Site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)

