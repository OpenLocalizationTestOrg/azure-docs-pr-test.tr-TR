---
title: "aaaTroubleshoot bağlanamıyor bir Azure siteden siteye VPN bağlantısı | Microsoft Docs"
description: "Bilgi nasıl tootroubleshoot bir siteden siteye VPN bağlantısı aniden çalışmayı durduruyor ve bağlanılamaz."
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
ms.openlocfilehash: 632c75bfcfb93a532eeead2855d43e6614569a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a><span data-ttu-id="8494e-103">Sorun giderme: Bir Azure siteden siteye VPN bağlantısı bağlanamıyor ve çalışmayı durduruyor</span><span class="sxs-lookup"><span data-stu-id="8494e-103">Troubleshooting: An Azure site-to-site VPN connection cannot connect and stops working</span></span>

<span data-ttu-id="8494e-104">Bir şirket içi ağınız ve Azure sanal ağı arasında siteden siteye VPN bağlantısı yapılandırdıktan sonra hello VPN bağlantısı aniden çalışmayı durdurur ve yeniden bağlanılamaz.</span><span class="sxs-lookup"><span data-stu-id="8494e-104">After you configure a site-to-site VPN connection between an on-premises network and an Azure virtual network, hello VPN connection suddenly stops working and cannot be reconnected.</span></span> <span data-ttu-id="8494e-105">Bu makalede, sorun giderme adımları toohelp sağlanmaktadır. Bu sorunu çözün.</span><span class="sxs-lookup"><span data-stu-id="8494e-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="8494e-106">Sorun giderme adımları</span><span class="sxs-lookup"><span data-stu-id="8494e-106">Troubleshooting steps</span></span>

<span data-ttu-id="8494e-107">tooresolve hello sorun, ilk çok deneyin[sıfırlama hello Azure VPN ağ geçidi](vpn-gateway-resetgw-classic.md) ve hello tünel hello şirket içi VPN aygıttan sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="8494e-107">tooresolve hello problem, first try too[reset hello Azure VPN gateway](vpn-gateway-resetgw-classic.md) and reset hello tunnel from hello on-premises VPN device.</span></span> <span data-ttu-id="8494e-108">Merhaba sorun devam ederse, bu adımları tooidentify hello neden hello sorununun izleyin.</span><span class="sxs-lookup"><span data-stu-id="8494e-108">If hello problem persists, follow these steps tooidentify hello cause of hello problem.</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="8494e-109">Önkoşul adım</span><span class="sxs-lookup"><span data-stu-id="8494e-109">Prerequisite step</span></span>

<span data-ttu-id="8494e-110">Merhaba hello Azure VPN ağ geçidi türünü kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="8494e-110">Check hello type of hello Azure VPN gateway.</span></span>

1. <span data-ttu-id="8494e-111">Toohello Git [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8494e-111">Go toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="8494e-112">Merhaba denetleyin **genel bakış** hello VPN ağ geçidi hello türü bilgi sayfası.</span><span class="sxs-lookup"><span data-stu-id="8494e-112">Check hello **Overview** page of hello VPN gateway for hello type information.</span></span>
    
    ![Merhaba ağ geçidi'ne genel bakış](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a><span data-ttu-id="8494e-114">1. Adım</span><span class="sxs-lookup"><span data-stu-id="8494e-114">Step 1.</span></span> <span data-ttu-id="8494e-115">Merhaba şirket içi VPN cihazı doğrulanıp doğrulanmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="8494e-115">Check whether hello on-premises VPN device is validated</span></span>

1. <span data-ttu-id="8494e-116">Kullanmakta olduğunuz olup olmadığını denetleyin bir [VPN cihazı ve işletim sistemi sürümü doğrulandı](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="8494e-116">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="8494e-117">Merhaba cihaz doğrulanan VPN cihazı değilse, bir uyumluluk sorunu varsa toocontact hello aygıt üreticisi toosee olabilir.</span><span class="sxs-lookup"><span data-stu-id="8494e-117">If hello device is not a validated VPN device, you might have toocontact hello device manufacturer toosee if there is a compatibility issue.</span></span>

2. <span data-ttu-id="8494e-118">Bu hello VPN cihazı doğru yapılandırıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="8494e-118">Make sure that hello VPN device is correctly configured.</span></span> <span data-ttu-id="8494e-119">Daha fazla bilgi için bkz: [cihaz yapılandırma örneklerini düzenleme](/vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="8494e-119">For more information, see [Edit device configuration samples](/vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-verify-hello-shared-key"></a><span data-ttu-id="8494e-120">2. Adım</span><span class="sxs-lookup"><span data-stu-id="8494e-120">Step 2.</span></span> <span data-ttu-id="8494e-121">Merhaba paylaşılan anahtar doğrulayın</span><span class="sxs-lookup"><span data-stu-id="8494e-121">Verify hello shared key</span></span>

<span data-ttu-id="8494e-122">Merhaba şirket içi VPN aygıtının toohello Azure sanal ağ VPN toomake hello anahtarların eşleştiğinden emin için paylaşılan anahtar Hello karşılaştırın.</span><span class="sxs-lookup"><span data-stu-id="8494e-122">Compare hello shared key for hello on-premises VPN device toohello Azure Virtual Network VPN toomake sure that hello keys match.</span></span> 

<span data-ttu-id="8494e-123">tooview hello hello Azure VPN bağlantısı için paylaşılan anahtar yöntemleri aşağıdaki hello birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="8494e-123">tooview hello shared key for hello Azure VPN connection, use one of hello following methods:</span></span>

<span data-ttu-id="8494e-124">**Azure portal**</span><span class="sxs-lookup"><span data-stu-id="8494e-124">**Azure portal**</span></span>

1. <span data-ttu-id="8494e-125">Oluşturduğunuz toohello VPN ağ geçidi siteden siteye bağlantı gidin.</span><span class="sxs-lookup"><span data-stu-id="8494e-125">Go toohello VPN gateway site-to-site connection that you created.</span></span>

2. <span data-ttu-id="8494e-126">Merhaba, **ayarları** 'yi tıklatın **paylaşılan anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="8494e-126">In hello **Settings** section, click **Shared key**.</span></span>
    
    ![Paylaşılan anahtar](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

<span data-ttu-id="8494e-128">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="8494e-128">**Azure PowerShell**</span></span>

<span data-ttu-id="8494e-129">Hello Azure Resource Manager dağıtım modeli için:</span><span class="sxs-lookup"><span data-stu-id="8494e-129">For hello Azure Resource Manager deployment model:</span></span>

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

<span data-ttu-id="8494e-130">Merhaba Klasik dağıtım modeli için:</span><span class="sxs-lookup"><span data-stu-id="8494e-130">For hello classic deployment model:</span></span>

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-hello-vpn-peer-ips"></a><span data-ttu-id="8494e-131">3. Adım</span><span class="sxs-lookup"><span data-stu-id="8494e-131">Step 3.</span></span> <span data-ttu-id="8494e-132">Merhaba VPN eş IP doğrulayın</span><span class="sxs-lookup"><span data-stu-id="8494e-132">Verify hello VPN peer IPs</span></span>

-   <span data-ttu-id="8494e-133">Merhaba hello IP tanımında **yerel ağ geçidi** Azure nesnesinde hello şirket içi cihaz IP eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="8494e-133">hello IP definition in hello **Local Network Gateway** object in Azure should match hello on-premises device IP.</span></span>
-   <span data-ttu-id="8494e-134">Merhaba hello üzerinde ayarlanır Azure ağ geçidi IP tanımı aygıt hello Azure ağ geçidi IP eşleşmelidir şirket içi.</span><span class="sxs-lookup"><span data-stu-id="8494e-134">hello Azure gateway IP definition that is set on hello on-premises device should match hello Azure gateway IP.</span></span>

### <a name="step-4-check-udr-and-nsgs-on-hello-gateway-subnet"></a><span data-ttu-id="8494e-135">4. Adım.</span><span class="sxs-lookup"><span data-stu-id="8494e-135">Step 4.</span></span> <span data-ttu-id="8494e-136">UDR ve Nsg'ler hello ağ geçidi alt ağda denetleyin</span><span class="sxs-lookup"><span data-stu-id="8494e-136">Check UDR and NSGs on hello gateway subnet</span></span>

<span data-ttu-id="8494e-137">Denetleyin ve kullanıcı tanımlı yönlendirme (UDR) veya ağ güvenlik grupları (Nsg'ler) hello ağ geçidi alt ağda kaldırın ve sonra hello sonucunu sınayın.</span><span class="sxs-lookup"><span data-stu-id="8494e-137">Check for and remove user-defined routing (UDR) or Network Security Groups (NSGs) on hello gateway subnet, and then test hello result.</span></span> <span data-ttu-id="8494e-138">Merhaba sorun çözülmüşse UDR veya NSG uygulanan hello ayarlarını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="8494e-138">If hello problem is resolved, validate hello settings that UDR or NSG applied.</span></span>

### <a name="step-5-check-hello-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="8494e-139">5. Adım.</span><span class="sxs-lookup"><span data-stu-id="8494e-139">Step 5.</span></span> <span data-ttu-id="8494e-140">Merhaba şirket içi VPN cihazı dış arabirimi adresi denetleyin</span><span class="sxs-lookup"><span data-stu-id="8494e-140">Check hello on-premises VPN device external interface address</span></span>

- <span data-ttu-id="8494e-141">Merhaba hello VPN cihazının Internet'e yönelik IP adresi hello eklenirse **yerel ağ** tanımı Azure'da, kullanımın bağlantısının kesilmesi karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8494e-141">If hello Internet-facing IP address of hello VPN device is included in hello **Local network** definition in Azure, you might experience sporadic disconnections.</span></span>
- <span data-ttu-id="8494e-142">Merhaba cihazın dış arabirimi hello üzerinde doğrudan Internet olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8494e-142">hello device's external interface must be directly on hello Internet.</span></span> <span data-ttu-id="8494e-143">Hiçbir ağ adresi çevirisi veya güvenlik duvarı hello Internet ve hello aygıt arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8494e-143">There should be no network address translation or firewall between hello Internet and hello device.</span></span>
- <span data-ttu-id="8494e-144">tooconfigure kümeleme toohave sanal bir IP Güvenlik Duvarı, hello küme bölün ve tooa ortak arabirimi ile bu hello Ağ Geçidi Arabirimi doğrudan hello VPN Gereci kullanıma sunma.</span><span class="sxs-lookup"><span data-stu-id="8494e-144">tooconfigure firewall clustering toohave a virtual IP, you must break hello cluster and expose hello VPN appliance directly tooa public interface that hello gateway can interface with.</span></span>

### <a name="step-6-verify-that-hello-subnets-match-exactly-azure-policy-based-gateways"></a><span data-ttu-id="8494e-145">6. Adım.</span><span class="sxs-lookup"><span data-stu-id="8494e-145">Step 6.</span></span> <span data-ttu-id="8494e-146">Merhaba alt tam olarak eşleştiğinden emin olun (Azure ilke tabanlı ağ geçitleri)</span><span class="sxs-lookup"><span data-stu-id="8494e-146">Verify that hello subnets match exactly (Azure policy-based gateways)</span></span>

-   <span data-ttu-id="8494e-147">Merhaba alt hello Azure sanal ağı ve şirket içi tanımlarında hello Azure sanal ağı arasında tam olarak eşleştiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="8494e-147">Verify that hello subnets match exactly between hello Azure virtual network and on-premises definitions for hello Azure virtual network.</span></span>
-   <span data-ttu-id="8494e-148">Merhaba alt hello arasında tam olarak eşleştiğinden emin olun **yerel ağ geçidi** ve şirket içi hello şirket içi ağ için tanımlar.</span><span class="sxs-lookup"><span data-stu-id="8494e-148">Verify that hello subnets match exactly between hello **Local Network Gateway** and on-premises definitions for hello on-premises network.</span></span>

### <a name="step-7-verify-hello-azure-gateway-health-probe"></a><span data-ttu-id="8494e-149">7. Adım.</span><span class="sxs-lookup"><span data-stu-id="8494e-149">Step 7.</span></span> <span data-ttu-id="8494e-150">Hello Azure ağ geçidi durumu araştırması doğrulayın</span><span class="sxs-lookup"><span data-stu-id="8494e-150">Verify hello Azure gateway health probe</span></span>

1. <span data-ttu-id="8494e-151">Toohello Git [durumu araştırması](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span><span class="sxs-lookup"><span data-stu-id="8494e-151">Go toohello [health probe](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span></span>

2. <span data-ttu-id="8494e-152">Merhaba Sertifika uyarısı aracılığıyla'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8494e-152">Click through hello certificate warning.</span></span>
3. <span data-ttu-id="8494e-153">Bir yanıtı alırsanız, hello VPN ağ geçidi sağlıklı olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="8494e-153">If you receive a response, hello VPN gateway is considered healthy.</span></span> <span data-ttu-id="8494e-154">Bir yanıt almazsanız, hello ağ geçidi sağlıklı olmayabilir veya hello ağ geçidi alt ağı üzerinde bir NSG hello soruna neden oluyor.</span><span class="sxs-lookup"><span data-stu-id="8494e-154">If you don't receive a response, hello gateway might not be healthy or an NSG on hello gateway subnet is causing hello problem.</span></span> <span data-ttu-id="8494e-155">Merhaba metin aşağıdaki örnek yanıt şöyledir:</span><span class="sxs-lookup"><span data-stu-id="8494e-155">hello following text is a sample response:</span></span>

    <span data-ttu-id="8494e-156">&lt;? xml version = "1.0"? > <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">birincil örneği: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6 < / dize&gt;</span><span class="sxs-lookup"><span data-stu-id="8494e-156">&lt;?xml version="1.0"?>  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Primary Instance: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span></span>

### <a name="step-8-check-whether-hello-on-premises-vpn-device-has-hello-perfect-forward-secrecy-feature-enabled"></a><span data-ttu-id="8494e-157">8. adım.</span><span class="sxs-lookup"><span data-stu-id="8494e-157">Step 8.</span></span> <span data-ttu-id="8494e-158">Merhaba VPN cihazı hello kusursuz iletme gizliliği özelliğinin etkin olduğu şirket içi olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="8494e-158">Check whether hello on-premises VPN device has hello perfect forward secrecy feature enabled</span></span>

<span data-ttu-id="8494e-159">Merhaba kusursuz iletme gizliliği özelliği, bağlantı kesme sorunlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="8494e-159">hello perfect forward secrecy feature can cause disconnection problems.</span></span> <span data-ttu-id="8494e-160">Merhaba VPN cihazı etkin kusursuz iletme gizliliği varsa hello özelliği devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="8494e-160">If hello VPN device has perfect forward secrecy enabled, disable hello feature.</span></span> <span data-ttu-id="8494e-161">Ardından hello VPN ağ geçidi IPSec ilkesi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="8494e-161">Then update hello VPN gateway IPsec policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8494e-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8494e-162">Next steps</span></span>

-   [<span data-ttu-id="8494e-163">Siteden siteye bağlantı tooa sanal ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8494e-163">Configure a site-to-site connection tooa virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [<span data-ttu-id="8494e-164">Siteden siteye VPN bağlantıları için bir IPSec/IKE ilkesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8494e-164">Configure an IPsec/IKE policy for site-to-site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)
