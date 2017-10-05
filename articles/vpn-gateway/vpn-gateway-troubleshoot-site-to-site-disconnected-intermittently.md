---
title: "Azure sorun giderme siteden siteye VPN bağlantısını keser zaman zaman | Microsoft Docs"
description: "Siteden siteye VPN bağlantısı düzenli olarak bağlantısı kesilmiş sorun giderme öğrenin."
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
ms.openlocfilehash: 99a790617baa65116bfba976cd9279627e8775f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a><span data-ttu-id="a7a92-103">Sorun giderme: Azure siteden siteye VPN aralıklı keser</span><span class="sxs-lookup"><span data-stu-id="a7a92-103">Troubleshooting: Azure Site-to-Site VPN disconnects intermittently</span></span>

<span data-ttu-id="a7a92-104">Yeni veya var olan bir Microsoft Azure noktadan siteye VPN bağlantısı kararlı değilse veya düzenli olarak keser sorunla karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7a92-104">You might experience the problem that a new or existing Microsoft Azure Point-to-Site VPN connection is not stable or disconnects regularly.</span></span> <span data-ttu-id="a7a92-105">Bu makalede, sorun giderme belirlemek ve sorunun nedenini çözümlemenize yardımcı olması için adımlar sağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a7a92-105">This article provides troubleshoot steps to help you identify and resolve the cause of the problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="a7a92-106">Sorun giderme adımları</span><span class="sxs-lookup"><span data-stu-id="a7a92-106">Troubleshooting steps</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="a7a92-107">Önkoşul adım</span><span class="sxs-lookup"><span data-stu-id="a7a92-107">Prerequisite step</span></span>

<span data-ttu-id="a7a92-108">Azure sanal ağ geçidi türünü kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="a7a92-108">Check the type of Azure  virtual network gateway:</span></span>

1. <span data-ttu-id="a7a92-109">Git [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a7a92-109">Go to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a7a92-110">Denetleme **genel bakış** sanal ağ geçidi türü bilgileri için sayfanın.</span><span class="sxs-lookup"><span data-stu-id="a7a92-110">Check the **Overview** page of the virtual network gateway for the type information.</span></span>
    
    ![Ağ geçidi genel bakış](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-the-on-premises-vpn-device-is-validated"></a><span data-ttu-id="a7a92-112">Şirket içi VPN cihazı doğrulanmış olup olmadığını 1 onay adım</span><span class="sxs-lookup"><span data-stu-id="a7a92-112">Step 1 Check whether the on-premises VPN device is validated</span></span>

1. <span data-ttu-id="a7a92-113">Kullanmakta olduğunuz olup olmadığını denetleyin bir [VPN cihazı ve işletim sistemi sürümü doğrulandı](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="a7a92-113">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="a7a92-114">VPN cihazı doğrulanmaz, herhangi bir uyumluluk sorunu olup olmadığını görmek için aygıt üreticisinin başvurmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="a7a92-114">If the VPN device is not validated, you may have to contact the device manufacturer to see if there is any compatibility issue.</span></span>
2. <span data-ttu-id="a7a92-115">VPN cihazı doğru yapılandırıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="a7a92-115">Make sure that the VPN device is correctly configured.</span></span> <span data-ttu-id="a7a92-116">Daha fazla bilgi için bkz: [cihaz yapılandırma örneklerini düzenleme](vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="a7a92-116">For more information, see [Editing device configuration samples](vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-check-the-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a><span data-ttu-id="a7a92-117">2. adım ayarları kontrol edin güvenlik ilişkisi (ilke tabanlı Azure sanal ağ geçitleri)</span><span class="sxs-lookup"><span data-stu-id="a7a92-117">Step 2 Check the Security Association settings(for policy-based Azure virtual network gateways)</span></span>

1. <span data-ttu-id="a7a92-118">Olduğundan emin olun sanal ağ alt ağları ve, aralıkları **yerel ağ geçidi** Microsoft Azure tanımında şirket içi VPN cihazı yapılandırma ile aynı.</span><span class="sxs-lookup"><span data-stu-id="a7a92-118">Make sure that the virtual network, subnets and, ranges in the **Local network gateway** definition in Microsoft Azure are same as the configuration on the on-premises VPN device.</span></span>
2. <span data-ttu-id="a7a92-119">Güvenlik ilişkisinin ayarlarla eşleştiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a7a92-119">Verify that the Security Association settings match.</span></span>

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a><span data-ttu-id="a7a92-120">Ağ geçidi alt ağı üzerinde kullanıcı tanımlı yollar veya ağ güvenlik grupları için 3. adım denetimi</span><span class="sxs-lookup"><span data-stu-id="a7a92-120">Step 3 Check for User-Defined Routes or Network Security Groups on Gateway Subnet</span></span>

<span data-ttu-id="a7a92-121">Bir kullanıcı tarafından tanımlanan rota ağ geçidi alt ağı üzerinde bazı trafiği kısıtlama ve diğer trafiğe izin.</span><span class="sxs-lookup"><span data-stu-id="a7a92-121">A user-defined route on the gateway subnet may be restricting some traffic and allowing other traffic.</span></span> <span data-ttu-id="a7a92-122">Bu VPN bağlantısını güvenilir olmayan bir miktar trafik için ve başkaları için iyi görünmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="a7a92-122">This makes it appear that the VPN connection is unreliable for some traffic and good for others.</span></span> 

### <a name="step-4-check-the-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="a7a92-123">Adım 4 denetleyin "Bir VPN tüneli" alt ağ çifti başına (ilke tabanlı sanal ağ geçitleri için) ayarlama</span><span class="sxs-lookup"><span data-stu-id="a7a92-123">Step 4 Check the "one VPN Tunnel per Subnet Pair" setting (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="a7a92-124">Şirket içi VPN cihazı için ayarlandığından emin olun **alt ağ çifti başına bir VPN tüneli** ilke tabanlı sanal ağ geçitleri için.</span><span class="sxs-lookup"><span data-stu-id="a7a92-124">Make sure that the on-premises VPN device is set to have **one VPN tunnel per subnet pair** for policy-based virtual network gateways.</span></span>

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="a7a92-125">Adım 5 (için ilke tabanlı sanal ağ geçitleri) güvenlik ilişkisi sınırlaması denetle</span><span class="sxs-lookup"><span data-stu-id="a7a92-125">Step 5 Check for Security Association Limitation (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="a7a92-126">İlke tabanlı sanal ağ geçidi 200 alt ağ güvenlik ilişkisi çiftleri sınırı vardır.</span><span class="sxs-lookup"><span data-stu-id="a7a92-126">The Policy-based virtual network gateway has limit of 200 subnet Security Association pairs.</span></span> <span data-ttu-id="a7a92-127">Azure sanal ağ alt ağları sayısının çarpımı kat sayısı, yerel alt ağları tarafından 200'den büyük olan, kesme durumlarıyla alt bakın.</span><span class="sxs-lookup"><span data-stu-id="a7a92-127">If the number of Azure virtual network subnets multiplied times by the number of local subnets is greater than 200, you see sporadic subnets disconnecting.</span></span>

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="a7a92-128">Adım 6 onay içi VPN cihazı dış arabirimi adresi</span><span class="sxs-lookup"><span data-stu-id="a7a92-128">Step 6 Check on-premises VPN device external interface address</span></span>

- <span data-ttu-id="a7a92-129">VPN cihazının IP adresi Internet'e dahil değilse **yerel ağ geçidi** tanımı Azure'da, kullanımın bağlantısının kesilmesi karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7a92-129">If the Internet facing IP address of the VPN device is included in the **Local network gateway** definition in Azure, you may experience sporadic disconnections.</span></span>
- <span data-ttu-id="a7a92-130">Cihazın dış arabirimi doğrudan Internet'te olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7a92-130">The device's external interface must be directly on the Internet.</span></span> <span data-ttu-id="a7a92-131">Hiçbir ağ adresi çevirisi (NAT) veya Güvenlik Duvarı Internet ve aygıt arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a7a92-131">There should be no Network Address Translation (NAT) or firewall between the Internet and the device.</span></span>
-  <span data-ttu-id="a7a92-132">Bir sanal IP sağlamak için güvenlik duvarı kümeleme yapılandırırsanız, küme bölme ve VPN Gereci doğrudan bir ağ geçidi ile arabirim ortak arabirimi kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="a7a92-132">If you configure Firewall Clustering to have a virtual IP, you must break the cluster and expose the VPN appliance directly to a public interface that the gateway can interface with.</span></span>

### <a name="step-7-check-whether-the-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a><span data-ttu-id="a7a92-133">Şirket içi VPN cihazı kusursuz iletme etkin gizliliği olup olmadığını 7 onay adım</span><span class="sxs-lookup"><span data-stu-id="a7a92-133">Step 7 Check whether the on-premises VPN device has Perfect Forward Secrecy enabled</span></span>

<span data-ttu-id="a7a92-134">**Kusursuz iletme gizliliği** özelliği, bağlantı kesme sorunlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="a7a92-134">The **Perfect Forward Secrecy** feature can cause the disconnection problems.</span></span> <span data-ttu-id="a7a92-135">VPN cihazı varsa **kusursuz iletme gizliliği** özelliği etkinse, devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="a7a92-135">If the VPN device has **Perfect forward Secrecy** enabled, disable the feature.</span></span> <span data-ttu-id="a7a92-136">Ardından [sanal ağ geçidi IPSec ilkesi güncelleştirmesi](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span><span class="sxs-lookup"><span data-stu-id="a7a92-136">Then [update the virtual network gateway IPsec policy](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7a92-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a7a92-137">Next steps</span></span>

- [<span data-ttu-id="a7a92-138">Bir sanal ağ için siteden siteye bağlantı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a7a92-138">Configure a Site-to-Site connection to a virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [<span data-ttu-id="a7a92-139">Siteden siteye VPN bağlantıları için IPSec/IKE ilkesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a7a92-139">Configure IPsec/IKE policy for Site-to-Site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)

