---
title: "Bağlanamıyor bir Azure siteden siteye VPN bağlantısı sorunlarını giderme | Microsoft Docs"
description: "Aniden çalışmayı durduruyor ve bağlanılamaz bir siteden siteye VPN bağlantısı sorunlarını giderme öğrenin."
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
ms.openlocfilehash: e7a3da64895f0307e5d6c3563672205a2f93a7d2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a><span data-ttu-id="bdb4e-103">Sorun giderme: Bir Azure siteden siteye VPN bağlantısı bağlanamıyor ve çalışmayı durduruyor</span><span class="sxs-lookup"><span data-stu-id="bdb4e-103">Troubleshooting: An Azure site-to-site VPN connection cannot connect and stops working</span></span>

<span data-ttu-id="bdb4e-104">Bir şirket içi ağınız ve Azure sanal ağı arasında siteden siteye VPN bağlantısı yapılandırdıktan sonra VPN bağlantısı aniden çalışmayı durdurur ve yeniden bağlanılamaz.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-104">After you configure a site-to-site VPN connection between an on-premises network and an Azure virtual network, the VPN connection suddenly stops working and cannot be reconnected.</span></span> <span data-ttu-id="bdb4e-105">Bu makalede, bu sorunu gidermenize yardımcı olmak için sorun giderme adımlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-105">This article provides troubleshooting steps to help you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="bdb4e-106">Sorun giderme adımları</span><span class="sxs-lookup"><span data-stu-id="bdb4e-106">Troubleshooting steps</span></span>

<span data-ttu-id="bdb4e-107">Sorunu gidermek için önce dener [Azure VPN gateway sıfırlama](vpn-gateway-resetgw-classic.md) ve şirket içi VPN aygıttan tünel sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-107">To resolve the problem, first try to [reset the Azure VPN gateway](vpn-gateway-resetgw-classic.md) and reset the tunnel from the on-premises VPN device.</span></span> <span data-ttu-id="bdb4e-108">Sorun devam ederse, sorunun nedenini belirlemek için şu adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-108">If the problem persists, follow these steps to identify the cause of the problem.</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="bdb4e-109">Önkoşul adım</span><span class="sxs-lookup"><span data-stu-id="bdb4e-109">Prerequisite step</span></span>

<span data-ttu-id="bdb4e-110">Azure VPN ağ geçidi türünü kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-110">Check the type of the Azure VPN gateway.</span></span>

1. <span data-ttu-id="bdb4e-111">[Azure Portal](https://portal.azure.com) gidin.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-111">Go to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="bdb4e-112">Denetleme **genel bakış** VPN ağ geçidi türü bilgi sayfası.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-112">Check the **Overview** page of the VPN gateway for the type information.</span></span>
    
    ![Ağ Geçidi'ne genel bakış](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-the-on-premises-vpn-device-is-validated"></a><span data-ttu-id="bdb4e-114">1. Adım</span><span class="sxs-lookup"><span data-stu-id="bdb4e-114">Step 1.</span></span> <span data-ttu-id="bdb4e-115">Şirket içi VPN cihazı doğrulanıp doğrulanmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="bdb4e-115">Check whether the on-premises VPN device is validated</span></span>

1. <span data-ttu-id="bdb4e-116">Kullanmakta olduğunuz olup olmadığını denetleyin bir [VPN cihazı ve işletim sistemi sürümü doğrulandı](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="bdb4e-116">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="bdb4e-117">Cihaz doğrulanan VPN cihazı değilse, bir uyumluluk sorunu olup olmadığını görmek için herhangi bir tuşa basın gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-117">If the device is not a validated VPN device, you might have to contact the device manufacturer to see if there is a compatibility issue.</span></span>

2. <span data-ttu-id="bdb4e-118">VPN cihazı doğru yapılandırıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-118">Make sure that the VPN device is correctly configured.</span></span> <span data-ttu-id="bdb4e-119">Daha fazla bilgi için bkz: [cihaz yapılandırma örneklerini düzenleme](/vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="bdb4e-119">For more information, see [Edit device configuration samples](/vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-verify-the-shared-key"></a><span data-ttu-id="bdb4e-120">2. Adım</span><span class="sxs-lookup"><span data-stu-id="bdb4e-120">Step 2.</span></span> <span data-ttu-id="bdb4e-121">Paylaşılan anahtar doğrulayın</span><span class="sxs-lookup"><span data-stu-id="bdb4e-121">Verify the shared key</span></span>

<span data-ttu-id="bdb4e-122">Paylaşılan anahtar Azure sanal ağ anahtarların eşleştiğinden emin olmak için VPN için şirket içi VPN aygıtınızın karşılaştırın.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-122">Compare the shared key for the on-premises VPN device to the Azure Virtual Network VPN to make sure that the keys match.</span></span> 

<span data-ttu-id="bdb4e-123">Azure VPN bağlantısı için paylaşılan anahtar görüntülemek için aşağıdaki yöntemlerden birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="bdb4e-123">To view the shared key for the Azure VPN connection, use one of the following methods:</span></span>

<span data-ttu-id="bdb4e-124">**Azure portal**</span><span class="sxs-lookup"><span data-stu-id="bdb4e-124">**Azure portal**</span></span>

1. <span data-ttu-id="bdb4e-125">Oluşturduğunuz VPN ağ geçidi siteden siteye bağlantısı gidin.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-125">Go to the VPN gateway site-to-site connection that you created.</span></span>

2. <span data-ttu-id="bdb4e-126">İçinde **ayarları** 'yi tıklatın **paylaşılan anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-126">In the **Settings** section, click **Shared key**.</span></span>
    
    ![Paylaşılan anahtar](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

<span data-ttu-id="bdb4e-128">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="bdb4e-128">**Azure PowerShell**</span></span>

<span data-ttu-id="bdb4e-129">Azure Resource Manager dağıtım modeli için:</span><span class="sxs-lookup"><span data-stu-id="bdb4e-129">For the Azure Resource Manager deployment model:</span></span>

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

<span data-ttu-id="bdb4e-130">Klasik dağıtım modeli için:</span><span class="sxs-lookup"><span data-stu-id="bdb4e-130">For the classic deployment model:</span></span>

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-the-vpn-peer-ips"></a><span data-ttu-id="bdb4e-131">3. Adım</span><span class="sxs-lookup"><span data-stu-id="bdb4e-131">Step 3.</span></span> <span data-ttu-id="bdb4e-132">VPN eş IP doğrulayın</span><span class="sxs-lookup"><span data-stu-id="bdb4e-132">Verify the VPN peer IPs</span></span>

-   <span data-ttu-id="bdb4e-133">IP tanımında **yerel ağ geçidi** Azure nesnesinde, şirket içi cihaz IP eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-133">The IP definition in the **Local Network Gateway** object in Azure should match the on-premises device IP.</span></span>
-   <span data-ttu-id="bdb4e-134">Şirket içi cihaz üzerinde ayarlanır Azure ağ geçidi IP tanımı Azure ağ geçidi IP eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-134">The Azure gateway IP definition that is set on the on-premises device should match the Azure gateway IP.</span></span>

### <a name="step-4-check-udr-and-nsgs-on-the-gateway-subnet"></a><span data-ttu-id="bdb4e-135">4. Adım.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-135">Step 4.</span></span> <span data-ttu-id="bdb4e-136">Ağ geçidi alt ağı üzerinde UDR ve Nsg'ler denetleyin</span><span class="sxs-lookup"><span data-stu-id="bdb4e-136">Check UDR and NSGs on the gateway subnet</span></span>

<span data-ttu-id="bdb4e-137">Denetleyin ve kullanıcı tanımlı yönlendirme (UDR) veya ağ güvenlik grupları (Nsg'ler) ağ geçidi alt ağda kaldırın ve ardından test sonucu.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-137">Check for and remove user-defined routing (UDR) or Network Security Groups (NSGs) on the gateway subnet, and then test the result.</span></span> <span data-ttu-id="bdb4e-138">Bu sorun çözülene, UDR veya NSG uygulanan ayarlarını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-138">If the problem is resolved, validate the settings that UDR or NSG applied.</span></span>

### <a name="step-5-check-the-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="bdb4e-139">5. Adım.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-139">Step 5.</span></span> <span data-ttu-id="bdb4e-140">Şirket içi VPN cihazı dış arabirimi adresi denetleyin</span><span class="sxs-lookup"><span data-stu-id="bdb4e-140">Check the on-premises VPN device external interface address</span></span>

- <span data-ttu-id="bdb4e-141">VPN cihazı Internet'e yönelik IP adresini de dahil edilmişse **yerel ağ** tanımı Azure'da, kullanımın bağlantısının kesilmesi karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-141">If the Internet-facing IP address of the VPN device is included in the **Local network** definition in Azure, you might experience sporadic disconnections.</span></span>
- <span data-ttu-id="bdb4e-142">Cihazın dış arabirimi doğrudan Internet'te olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-142">The device's external interface must be directly on the Internet.</span></span> <span data-ttu-id="bdb4e-143">Herhangi bir ağ adresi çevirisi veya Güvenlik Duvarı Internet ve aygıt arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-143">There should be no network address translation or firewall between the Internet and the device.</span></span>
- <span data-ttu-id="bdb4e-144">Sanal bir IP için kümeleme güvenlik duvarını yapılandırmak için küme bölme ve VPN Gereci doğrudan bir ağ geçidi ile arabirim ortak arabirimi kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-144">To configure firewall clustering to have a virtual IP, you must break the cluster and expose the VPN appliance directly to a public interface that the gateway can interface with.</span></span>

### <a name="step-6-verify-that-the-subnets-match-exactly-azure-policy-based-gateways"></a><span data-ttu-id="bdb4e-145">6. Adım.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-145">Step 6.</span></span> <span data-ttu-id="bdb4e-146">Alt ağlar tam olarak eşleştiğinden emin olun (Azure ilke tabanlı ağ geçitleri)</span><span class="sxs-lookup"><span data-stu-id="bdb4e-146">Verify that the subnets match exactly (Azure policy-based gateways)</span></span>

-   <span data-ttu-id="bdb4e-147">Alt ağlar Azure sanal ağı ve Azure sanal ağı için şirket içi tanımları arasında tam olarak eşleştiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-147">Verify that the subnets match exactly between the Azure virtual network and on-premises definitions for the Azure virtual network.</span></span>
-   <span data-ttu-id="bdb4e-148">Alt ağlar arasında tam olarak eşleştiğinden emin olun **yerel ağ geçidi** ve şirket içi ağınız için tanımları.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-148">Verify that the subnets match exactly between the **Local Network Gateway** and on-premises definitions for the on-premises network.</span></span>

### <a name="step-7-verify-the-azure-gateway-health-probe"></a><span data-ttu-id="bdb4e-149">7. Adım.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-149">Step 7.</span></span> <span data-ttu-id="bdb4e-150">Azure ağ geçidi durumu araştırması doğrulayın</span><span class="sxs-lookup"><span data-stu-id="bdb4e-150">Verify the Azure gateway health probe</span></span>

1. <span data-ttu-id="bdb4e-151">Git [durumu araştırması](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span><span class="sxs-lookup"><span data-stu-id="bdb4e-151">Go to the [health probe](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span></span>

2. <span data-ttu-id="bdb4e-152">Sertifika uyarısı aracılığıyla'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-152">Click through the certificate warning.</span></span>
3. <span data-ttu-id="bdb4e-153">Bir yanıtı alırsanız, VPN ağ geçidi sağlıklı olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-153">If you receive a response, the VPN gateway is considered healthy.</span></span> <span data-ttu-id="bdb4e-154">Bir yanıt almazsanız, ağ geçidi sağlıklı olmayabilir veya ağ geçidi alt ağı üzerinde bir NSG sorunu neden oluyor.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-154">If you don't receive a response, the gateway might not be healthy or an NSG on the gateway subnet is causing the problem.</span></span> <span data-ttu-id="bdb4e-155">Aşağıdaki örnek yanıt metindir:</span><span class="sxs-lookup"><span data-stu-id="bdb4e-155">The following text is a sample response:</span></span>

    <span data-ttu-id="bdb4e-156">&lt;? xml version = "1.0"? > <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">birincil örneği: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6 < / dize&gt;</span><span class="sxs-lookup"><span data-stu-id="bdb4e-156">&lt;?xml version="1.0"?>  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Primary Instance: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span></span>

### <a name="step-8-check-whether-the-on-premises-vpn-device-has-the-perfect-forward-secrecy-feature-enabled"></a><span data-ttu-id="bdb4e-157">8. adım.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-157">Step 8.</span></span> <span data-ttu-id="bdb4e-158">Şirket içi VPN cihazı kusursuz iletme gizliliği özelliğinin etkin olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="bdb4e-158">Check whether the on-premises VPN device has the perfect forward secrecy feature enabled</span></span>

<span data-ttu-id="bdb4e-159">Kusursuz iletme gizliliği özelliği, bağlantı kesme sorunlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-159">The perfect forward secrecy feature can cause disconnection problems.</span></span> <span data-ttu-id="bdb4e-160">VPN cihazı etkin kusursuz iletme gizliliği varsa, özelliği devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-160">If the VPN device has perfect forward secrecy enabled, disable the feature.</span></span> <span data-ttu-id="bdb4e-161">Ardından VPN ağ geçidi IPSec ilkesi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="bdb4e-161">Then update the VPN gateway IPsec policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bdb4e-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bdb4e-162">Next steps</span></span>

-   [<span data-ttu-id="bdb4e-163">Bir sanal ağ için siteden siteye bağlantı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bdb4e-163">Configure a site-to-site connection to a virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [<span data-ttu-id="bdb4e-164">Siteden siteye VPN bağlantıları için bir IPSec/IKE ilkesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bdb4e-164">Configure an IPsec/IKE policy for site-to-site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)
