---
title: "Bir arada var olabilen ExpressRoute ve Siteden Siteye VPN bağlantıları yapılandırma: klasik: Azure | Microsoft Docs"
description: "Bu makalede ExpressRoute ve hello Klasik dağıtım modeli için bir arada var olabilen siteden siteye VPN bağlantısını nasıl yapılandıracağınız anlatılmaktadır."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: dcf1a5af-a289-466a-b812-0bfedbd2bda0
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: abb30fff55e8ec243f2920c5b2f70c43717755fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a><span data-ttu-id="60dd9-103">Birlikte bulunan ExpressRoute bağlantıları ile Siteden Siteye bağlantıları yapılandırma (klasik)</span><span class="sxs-lookup"><span data-stu-id="60dd9-103">Configure ExpressRoute and Site-to-Site coexisting connections (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="60dd9-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="60dd9-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="60dd9-105">PowerShell - Klasik</span><span class="sxs-lookup"><span data-stu-id="60dd9-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="60dd9-106">Merhaba özelliği tooconfigure siteden siteye VPN ve ExpressRoute sahip olmanın çeşitli avantajları vardır.</span><span class="sxs-lookup"><span data-stu-id="60dd9-106">Having hello ability tooconfigure Site-to-Site VPN and ExpressRoute has several advantages.</span></span> <span data-ttu-id="60dd9-107">ExressRoute için Güvenli Yük devretme yolu olarak siteden siteye VPN yapılandırabilir veya ExpressRoute aracılığıyla bağlanmayan siteden siteye VPN tooconnect toosites kullanın.</span><span class="sxs-lookup"><span data-stu-id="60dd9-107">You can configure Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs tooconnect toosites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="60dd9-108">Biz bu makalede her iki senaryoyu hello adımları tooconfigure ele alınacaktır.</span><span class="sxs-lookup"><span data-stu-id="60dd9-108">We will cover hello steps tooconfigure both scenarios in this article.</span></span> <span data-ttu-id="60dd9-109">Bu makale toohello Klasik dağıtım modeli için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="60dd9-109">This article applies toohello classic deployment model.</span></span> <span data-ttu-id="60dd9-110">Bu yapılandırma hello Portalı'nda kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="60dd9-110">This configuration is not available in hello portal.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="60dd9-111">**Azure dağıtım modelleri hakkında**</span><span class="sxs-lookup"><span data-stu-id="60dd9-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="60dd9-112">Aşağıdaki hello yönergeleri izlemeden önce ExpressRoute bağlantı hatlarının önceden yapılandırılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="60dd9-112">ExpressRoute circuits must be pre-configured before you follow hello instructions below.</span></span> <span data-ttu-id="60dd9-113">Merhaba kılavuzları çok izlediğinizden emin olun[bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-classic.md) ve [yönlendirmeyi yapılandırma](expressroute-howto-routing-classic.md) hello adımları izlemeden önce.</span><span class="sxs-lookup"><span data-stu-id="60dd9-113">Make sure that you have followed hello guides too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and [configure routing](expressroute-howto-routing-classic.md) before you follow hello steps below.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="60dd9-114">Sınırlar ve sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="60dd9-114">Limits and limitations</span></span>
* <span data-ttu-id="60dd9-115">**Geçiş yönlendirmesi desteklenmez.**</span><span class="sxs-lookup"><span data-stu-id="60dd9-115">**Transit routing is not supported.**</span></span> <span data-ttu-id="60dd9-116">Siteden Siteye VPN aracılığıyla bağlanan yerel ağınız ve ExpressRoute aracılığıyla bağlanan yerel ağınız arasında (Azure aracılığıyla) yönlendirme yapamazsınız.</span><span class="sxs-lookup"><span data-stu-id="60dd9-116">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="60dd9-117">**Noktadan siteye desteklenmez.**</span><span class="sxs-lookup"><span data-stu-id="60dd9-117">**Point-to-site is not supported.**</span></span> <span data-ttu-id="60dd9-118">Noktadan siteye VPN bağlantıları toohello etkinleştiremiyor bağlı tooExpressRoute olduğu aynı sanal ağı.</span><span class="sxs-lookup"><span data-stu-id="60dd9-118">You can't enable point-to-site VPN connections toohello same VNet that is connected tooExpressRoute.</span></span> <span data-ttu-id="60dd9-119">Noktadan siteye VPN ve ExpressRoute birlikte bulunamaz Merhaba aynı sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="60dd9-119">Point-to-site VPN and ExpressRoute cannot coexist for hello same VNet.</span></span>
* <span data-ttu-id="60dd9-120">**Zorlamalı tünel hello siteden siteye VPN ağ geçidinde etkinleştirilemez.**</span><span class="sxs-lookup"><span data-stu-id="60dd9-120">**Forced tunneling cannot be enabled on hello Site-to-Site VPN gateway.**</span></span> <span data-ttu-id="60dd9-121">Yalnızca "tüm Internet'e bağlı trafik geri tooyour şirket içi ağ ExpressRoute aracılığıyla zorlayabilirsiniz".</span><span class="sxs-lookup"><span data-stu-id="60dd9-121">You can only "force" all Internet-bound traffic back tooyour on-premises network via ExpressRoute.</span></span>
* <span data-ttu-id="60dd9-122">**Temel SKU ağ geçidi desteklenmez.**</span><span class="sxs-lookup"><span data-stu-id="60dd9-122">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="60dd9-123">Temel SKU olmayan ağ geçidi için her iki hello kullanmalısınız [ExpressRoute ağ geçidi](expressroute-about-virtual-network-gateways.md) ve hello [VPN ağ geçidi](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="60dd9-123">You must use a non-Basic SKU gateway for both hello [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and hello [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="60dd9-124">**Yalnızca rota tabanlı VPN ağ geçidi desteklenir.**</span><span class="sxs-lookup"><span data-stu-id="60dd9-124">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="60dd9-125">Rota tabanlı [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md) kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="60dd9-125">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="60dd9-126">**VPN ağ geçidiniz için statik rota yapılandırılmalıdır.**</span><span class="sxs-lookup"><span data-stu-id="60dd9-126">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="60dd9-127">Yerel ağınıza bağlı tooboth ExpressRoute ve bir Site siteye VPN, bir statik yol, yerel ağ tooroute hello siteden siteye VPN bağlantısı toohello yapılandırılmış olması gerekiyor, ortak Internet.</span><span class="sxs-lookup"><span data-stu-id="60dd9-127">If your local network is connected tooboth ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network tooroute hello Site-to-Site VPN connection toohello public Internet.</span></span>
* <span data-ttu-id="60dd9-128">**İlk olarak ExpressRoute ağ geçidi yapılandırılmalıdır.**</span><span class="sxs-lookup"><span data-stu-id="60dd9-128">**ExpressRoute gateway must be configured first.**</span></span> <span data-ttu-id="60dd9-129">Merhaba siteden siteye VPN ağ geçidi eklemeden önce ilk hello ExpressRoute ağ geçidi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="60dd9-129">You must create hello ExpressRoute gateway first before you add hello Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="60dd9-130">Yapılandırma tasarımları</span><span class="sxs-lookup"><span data-stu-id="60dd9-130">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="60dd9-131">Siteden siteye VPN’i ExpressRoute için bir yük devretme yolu olarak yapılandırma</span><span class="sxs-lookup"><span data-stu-id="60dd9-131">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="60dd9-132">Siteden siteye bir VPN bağlantısını ExpressRoute için yedek olarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="60dd9-132">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="60dd9-133">Bu, yalnızca toovirtual ağlar bağlantılı toohello Azure özel eşleme yoluna geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="60dd9-133">This applies only toovirtual networks linked toohello Azure private peering path.</span></span> <span data-ttu-id="60dd9-134">Azure ortak ve Microsoft eşlemeleri aracılığıyla erişilebilen hizmetler için VPN tabanlı yük devretme çözümü yoktur.</span><span class="sxs-lookup"><span data-stu-id="60dd9-134">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="60dd9-135">Merhaba expressroute bağlantı hattı her zaman hello birincil bağlantıdır.</span><span class="sxs-lookup"><span data-stu-id="60dd9-135">hello ExpressRoute circuit is always hello primary link.</span></span> <span data-ttu-id="60dd9-136">Yalnızca hello expressroute bağlantı hattı başarısız olursa veri hello siteden siteye VPN üzerinden akar.</span><span class="sxs-lookup"><span data-stu-id="60dd9-136">Data will flow through hello Site-to-Site VPN path only if hello ExpressRoute circuit fails.</span></span> 

> [!NOTE]
> <span data-ttu-id="60dd9-137">Zaman aynı olan iki yollar hello expressroute bağlantı hattı siteden siteye VPN üzerinden tercih edilen olmakla birlikte, Azure doğru hello paketin hedef hello uzun önek eşleştirme toochoose hello rota kullanır.</span><span class="sxs-lookup"><span data-stu-id="60dd9-137">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are hello same, Azure will use hello longest prefix match toochoose hello route towards hello packet's destination.</span></span>
> 
> 

![Bir arada var olma](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a><span data-ttu-id="60dd9-139">ExpressRoute aracılığıyla bağlanılmayan bir siteden siteye VPN tooconnect toosites yapılandırın</span><span class="sxs-lookup"><span data-stu-id="60dd9-139">Configure a Site-to-Site VPN tooconnect toosites not connected through ExpressRoute</span></span>
<span data-ttu-id="60dd9-140">Burada bazı siteler tooAzure siteden siteye VPN üzerinden doğrudan bağlanın ve bazı sitelerin ExpressRoute üzerinden bağlanması ağınız yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="60dd9-140">You can configure your network where some sites connect directly tooAzure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Bir arada var olma](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="60dd9-142">Bir sanal ağı geçiş yönlendiricisi olarak yapılandıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="60dd9-142">You cannot a configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-hello-steps-toouse"></a><span data-ttu-id="60dd9-143">Merhaba adımları toouse seçme</span><span class="sxs-lookup"><span data-stu-id="60dd9-143">Selecting hello steps toouse</span></span>
<span data-ttu-id="60dd9-144">Bir arada var olabilen sipariş tooconfigure bağlantıları yordamları toochoose iki farklı kümesi vardır.</span><span class="sxs-lookup"><span data-stu-id="60dd9-144">There are two different sets of procedures toochoose from in order tooconfigure connections that can coexist.</span></span> <span data-ttu-id="60dd9-145">Seçtiğiniz hello yapılandırma yordamı için tooconnect istediğiniz veya yeni bir sanal ağ toocreate istediğiniz var olan bir sanal ağ olup olmadığına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="60dd9-145">hello configuration procedure that you select will depend on whether you have an existing virtual network that you want tooconnect to, or you want toocreate a new virtual network.</span></span>

* <span data-ttu-id="60dd9-146">I yoksa bir VNet ve toocreate biri gerekir.</span><span class="sxs-lookup"><span data-stu-id="60dd9-146">I don't have a VNet and need toocreate one.</span></span>
  
    <span data-ttu-id="60dd9-147">Bir sanal ağ zaten sahip değilseniz, bu yordamı, hello Klasik dağıtım modeli kullanılarak ve yeni ExpressRoute ve siteden siteye VPN bağlantıları oluşturma yeni bir sanal ağ oluşturma size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="60dd9-147">If you don’t already have a virtual network, this procedure will walk you through creating a new virtual network using hello classic deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="60dd9-148">tooconfigure, hello makale bölümdeki hello adımları [toocreate yeni bir sanal ağ ve bir arada var olabilen bağlantılar](#new).</span><span class="sxs-lookup"><span data-stu-id="60dd9-148">tooconfigure, follow hello steps in hello article section [toocreate a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="60dd9-149">Zaten bir klasik dağıtım modeli VNet’im var.</span><span class="sxs-lookup"><span data-stu-id="60dd9-149">I already have a classic deployment model VNet.</span></span>
  
    <span data-ttu-id="60dd9-150">Mevcut bir Siteden Siteye VPN bağlantısı veya ExpressRoute bağlantısına sahip bir sanal ağınız zaten olabilir.</span><span class="sxs-lookup"><span data-stu-id="60dd9-150">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="60dd9-151">Merhaba makale bölümüne [tooconfigure zaten olan bir VNet için aynı anda mevcut bağlantılar](#add) hello ağ geçidini silme ve ardından yeni ExpressRoute ve siteden siteye VPN bağlantıları oluşturma size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="60dd9-151">hello article section [tooconfigure coexsiting connections for an already existing VNet](#add) will walk you through deleting hello gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="60dd9-152">Hello adımları Hello yeni bağlantıları oluştururken, belirli bir sırada doldurulmalıdır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="60dd9-152">Note that when creating hello new connections, hello steps must be completed in a very specific order.</span></span> <span data-ttu-id="60dd9-153">Diğer makaleler toocreate Hello yönergeleri, ağ geçitleri ve bağlantıları kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="60dd9-153">Don't use hello instructions in other articles toocreate your gateways and connections.</span></span>
  
    <span data-ttu-id="60dd9-154">Bu yordamda, bir arada var olabilen bağlantılar oluşturmayı, ağ geçidi, toodelete gerektirir ve yeni ağ geçitlerini yapılandırmak.</span><span class="sxs-lookup"><span data-stu-id="60dd9-154">In this procedure, creating connections that can coexist will require you toodelete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="60dd9-155">Bu, şirket içi bağlantılarınız için kapalı kalma süresi silin ve ağ geçidiniz ve bağlantıları oluşturun, ancak toomigrate gerekmez tüm sanal makineleri veya hizmetleri tooa yeni sanal ağınızın olacağı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="60dd9-155">This means you will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need toomigrate any of your VMs or services tooa new virtual network.</span></span> <span data-ttu-id="60dd9-156">Yapılandırılmış toodo şekilde olmaları durumunda, ağ geçidi yapılandırması sırasında VM'ler ve hizmetler hello yük dengeleyici üzerinden kullanıma mümkün toocommunicate olmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="60dd9-156">Your VMs and services will still be able toocommunicate out through hello load balancer while you configure your gateway if they are configured toodo so.</span></span>

## <span data-ttu-id="60dd9-157"><a name="new"></a>toocreate yeni bir sanal ağ ve arada var olabilen bağlantılar</span><span class="sxs-lookup"><span data-stu-id="60dd9-157"><a name="new"></a>toocreate a new virtual network and coexisting connections</span></span>
<span data-ttu-id="60dd9-158">Bu yordamda, bir VNet oluşturma ve bir arada var olabilen Siteden Siteye ve ExpressRoute bağlantıları oluşturma adım adım açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="60dd9-158">This procedure will walk you through creating a VNet and create Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="60dd9-159">Tooinstall hello en son sürümünü hello Azure PowerShell cmdlet'lerini gerekir.</span><span class="sxs-lookup"><span data-stu-id="60dd9-159">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="60dd9-160">Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) hello PowerShell cmdlet'lerini yükleme hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="60dd9-160">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span> <span data-ttu-id="60dd9-161">Bu yapılandırma için kullanacağınız hello cmdlet'leri ne tanımanız değerinden biraz farklı olabileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="60dd9-161">Note that hello cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="60dd9-162">Bu yönergelerde emin toouse hello cmdlet'leri belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="60dd9-162">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="60dd9-163">Sanal ağınız için bir şema oluşturun.</span><span class="sxs-lookup"><span data-stu-id="60dd9-163">Create a schema for your virtual network.</span></span> <span data-ttu-id="60dd9-164">Merhaba yapılandırma şeması hakkında daha fazla bilgi için bkz: [Azure Virtual Network yapılandırma şeması](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="60dd9-164">For more information about hello configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   
    <span data-ttu-id="60dd9-165">Şemanızı oluşturduğunuzda, aşağıdaki değerleri hello kullandığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="60dd9-165">When you create your schema, make sure you use hello following values:</span></span>
   
   * <span data-ttu-id="60dd9-166">Merhaba hello sanal ağ ağ geçidi alt ağı/27 veya daha kısa bir önek (örneğin, /26 veya/25) olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="60dd9-166">hello gateway subnet for hello virtual network must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   * <span data-ttu-id="60dd9-167">Merhaba ağ geçidi bağlantı türü "ayrılmış" olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="60dd9-167">hello gateway connection type is "Dedicated".</span></span>
     
             <VirtualNetworkSite name="MyAzureVNET" Location="Central US">
               <AddressSpace>
                 <AddressPrefix>10.17.159.192/26</AddressPrefix>
               </AddressSpace>
               <Subnets>
                 <Subnet name="Subnet-1">
                   <AddressPrefix>10.17.159.192/27</AddressPrefix>
                 </Subnet>
                 <Subnet name="GatewaySubnet">
                   <AddressPrefix>10.17.159.224/27</AddressPrefix>
                 </Subnet>
               </Subnets>
               <Gateway>
                 <ConnectionsToLocalNetwork>
                   <LocalNetworkSiteRef name="MyLocalNetwork">
                     <Connection type="Dedicated" />
                   </LocalNetworkSiteRef>
                 </ConnectionsToLocalNetwork>
               </Gateway>
             </VirtualNetworkSite>
3. <span data-ttu-id="60dd9-168">Oluşturma ve xml şeması dosyanızı yapılandırdıktan sonra hello dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="60dd9-168">After creating and configuring your xml schema file, upload hello file.</span></span> <span data-ttu-id="60dd9-169">Bu, sanal ağınızı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="60dd9-169">This will create your virtual network.</span></span>
   
    <span data-ttu-id="60dd9-170">Cmdlet tooupload aşağıdaki hello dosyanızı hello değerini kendi değerlerinizle değiştirerek kullanın.</span><span class="sxs-lookup"><span data-stu-id="60dd9-170">Use hello following cmdlet tooupload your file, replacing hello value with your own.</span></span>
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <span data-ttu-id="60dd9-171"><a name="gw"></a>ExpressRoute ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="60dd9-171"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="60dd9-172">Emin toospecify olması olarak hello *standart*, *HighPerformance*, veya *UltraPerformance* ve GatewayType hello *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="60dd9-172">Be sure toospecify hello GatewaySKU as *Standard*, *HighPerformance*, or *UltraPerformance* and hello GatewayType as *DynamicRouting*.</span></span>
   
    <span data-ttu-id="60dd9-173">Aşağıdaki örnek, hello değerleri kendinizinkilerle değiştirerek hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="60dd9-173">Use hello following sample, substituting hello values for your own.</span></span>
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. <span data-ttu-id="60dd9-174">Merhaba ExpressRoute ağ geçidi toohello expressroute bağlantı hattı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="60dd9-174">Link hello ExpressRoute gateway toohello ExpressRoute circuit.</span></span> <span data-ttu-id="60dd9-175">Bu adımı tamamladıktan sonra şirket içi ağınız ve ExpressRoute aracılığıyla Azure arasında hello bağlantı kurulur.</span><span class="sxs-lookup"><span data-stu-id="60dd9-175">After this step has been completed, hello connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span>
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <span data-ttu-id="60dd9-176"><a name="vpngw"></a>Ardından, Siteden Siteye VPN ağ geçidinizi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="60dd9-176"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="60dd9-177">Merhaba gatewaysku *standart*, *HighPerformance*, veya *UltraPerformance* ve hello GatewayType olmalıdır *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="60dd9-177">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance* and hello GatewayType must be *DynamicRouting*.</span></span>
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    <span data-ttu-id="60dd9-178">Merhaba ağ geçidi kimliği ve hello ortak IP dahil olmak üzere tooretrieve hello sanal ağ ağ geçidi ayarlarını kullanabilir hello `Get-AzureVirtualNetworkGateway` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="60dd9-178">tooretrieve hello virtual network gateway settings, including hello gateway ID and hello public IP, use hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span>
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for hello following virtual network: GNSDesMoines
        LastEventID          : 23002
        State                : Provisioned
        VIPAddress           : 104.43.x.y
        DefaultSite          :
        GatewaySKU           : HighPerformance
        Location             :
        VnetId               : 979aabcf-e47f-4136-ab9b-b4780c1e1bd5
        SubnetId             :
        EnableBgp            : False
        OperationDescription : Get-AzureVirtualNetworkGateway
        OperationId          : 42773656-85e1-a6b6-8705-35473f1e6f6a
        OperationStatus      : Succeeded
7. <span data-ttu-id="60dd9-179">Bir yerel site VPN ağ geçidi varlığı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="60dd9-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="60dd9-180">Bu komut, şirket içi VPN ağ geçidinizi yapılandırmaz.</span><span class="sxs-lookup"><span data-stu-id="60dd9-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="60dd9-181">Bunun yerine, hello genel IP gibi tooprovide hello yerel ağ geçidi ayarları sağlar ve hello Azure VPN ağ geçidi tooit bağlanabilmesi hello şirket içi adres alanı.</span><span class="sxs-lookup"><span data-stu-id="60dd9-181">Rather, it allows you tooprovide hello local gateway settings, such as hello public IP and hello on-premises address space, so that hello Azure VPN gateway can connect tooit.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="60dd9-182">Merhaba siteden siteye VPN için yerel site Hello hello netcfg içinde tanımlı değil.</span><span class="sxs-lookup"><span data-stu-id="60dd9-182">hello local site for hello Site-to-Site VPN is not defined in hello netcfg.</span></span> <span data-ttu-id="60dd9-183">Bunun yerine, bu cmdlet toospecify hello yerel site parametrelerini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="60dd9-183">Instead, you must use this cmdlet toospecify hello local site parameters.</span></span> <span data-ttu-id="60dd9-184">Portalı veya hello netcfg dosyasını kullanarak tanımlayamazsınız.</span><span class="sxs-lookup"><span data-stu-id="60dd9-184">You cannot define it using either portal, or hello netcfg file.</span></span>
   > 
   > 
   
    <span data-ttu-id="60dd9-185">Aşağıdaki örnek, hello değerleri kendi değerlerinizle değiştirerek hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="60dd9-185">Use hello following sample, replacing hello values with your own.</span></span>
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > <span data-ttu-id="60dd9-186">Yerel ağınızda birden çok yol varsa, hepsini bir dizi olarak geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="60dd9-186">If your local network has multiple routes, you can pass them all in as an array.</span></span>  <span data-ttu-id="60dd9-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span><span class="sxs-lookup"><span data-stu-id="60dd9-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span></span>  
   > 
   > 

    <span data-ttu-id="60dd9-188">Merhaba ağ geçidi kimliği ve hello ortak IP dahil olmak üzere tooretrieve hello sanal ağ ağ geçidi ayarlarını kullanabilir hello `Get-AzureVirtualNetworkGateway` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="60dd9-188">tooretrieve hello virtual network gateway settings, including hello gateway ID and hello public IP, use hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="60dd9-189">Merhaba aşağıdaki örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="60dd9-189">See hello following example.</span></span>

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. <span data-ttu-id="60dd9-190">Yerel VPN cihaz tooconnect toohello yeni ağ geçidinizi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="60dd9-190">Configure your local VPN device tooconnect toohello new gateway.</span></span> <span data-ttu-id="60dd9-191">VPN Cihazınızı yapılandırırken 6. adımda alınan hello bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="60dd9-191">Use hello information that you retrieved in step 6 when configuring your VPN device.</span></span> <span data-ttu-id="60dd9-192">VPN cihazını yapılandırma hakkında daha fazla bilgi için bkz. [VPN Cihazı Yapılandırma](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="60dd9-192">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
2. <span data-ttu-id="60dd9-193">Bağlantı hello siteden siteye VPN ağ geçidinde Azure toohello yerel ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="60dd9-193">Link hello Site-to-Site VPN gateway on Azure toohello local gateway.</span></span>
   
    <span data-ttu-id="60dd9-194">Bu örnekte, Connectedentityıd çalıştırarak bulabilirsiniz hello yerel ağ geçidi kimliği olan `Get-AzureLocalNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="60dd9-194">In this example, connectedEntityId is hello local gateway ID, which you can find by running `Get-AzureLocalNetworkGateway`.</span></span> <span data-ttu-id="60dd9-195">Hello kullanarak Virtualnetworkgatewayıd'yi bulabilirsiniz `Get-AzureVirtualNetworkGateway` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="60dd9-195">You can find virtualNetworkGatewayId by using hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="60dd9-196">Bu adımdan sonra hello siteden siteye VPN bağlantısı aracılığıyla yerel ağınız ve Azure arasında hello bağlantı kurulur.</span><span class="sxs-lookup"><span data-stu-id="60dd9-196">After this step, hello connection between your local network and Azure via hello Site-to-Site VPN connection is established.</span></span>

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <span data-ttu-id="60dd9-197"><a name="add"></a>zaten olan bir VNet için tooconfigure aynı anda mevcut bağlantılar</span><span class="sxs-lookup"><span data-stu-id="60dd9-197"><a name="add"></a>tooconfigure coexsiting connections for an already existing VNet</span></span>
<span data-ttu-id="60dd9-198">Varolan bir sanal ağınız varsa, hello ağ geçidi alt ağ boyutunu kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="60dd9-198">If you have an existing virtual network, check hello gateway subnet size.</span></span> <span data-ttu-id="60dd9-199">Merhaba ağ geçidi alt ağı /28 veya/29 ise, öncelikle hello sanal ağ geçidini silmek ve hello ağ geçidi alt ağ boyutunu artırın.</span><span class="sxs-lookup"><span data-stu-id="60dd9-199">If hello gateway subnet is /28 or /29, you must first delete hello virtual network gateway and increase hello gateway subnet size.</span></span> <span data-ttu-id="60dd9-200">Merhaba bu bölümdeki adımlar bunu nasıl yapacağınızı gösterir toodo.</span><span class="sxs-lookup"><span data-stu-id="60dd9-200">hello steps in this section will show you how toodo that.</span></span>

<span data-ttu-id="60dd9-201">Merhaba ağ geçidi alt ağı /27 ise veya daha büyük ve hello sanal ağ ExpressRoute üzerinden bağlı olduğundan, hello adımları atlayın ve çok devam["6. adım - siteden siteye VPN ağ geçidi oluşturma"](#vpngw) hello önceki bölümdeki.</span><span class="sxs-lookup"><span data-stu-id="60dd9-201">If hello gateway subnet is /27 or larger and hello virtual network is connected via ExpressRoute, you can skip hello steps below and proceed too["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in hello previous section.</span></span>

> [!NOTE]
> <span data-ttu-id="60dd9-202">Merhaba mevcut ağ geçidini sildiğinizde, bu yapılandırma üzerinde çalışırken, yerel şirket hello bağlantı tooyour sanal ağ kaybedersiniz.</span><span class="sxs-lookup"><span data-stu-id="60dd9-202">When you delete hello existing gateway, your local premises will lose hello connection tooyour virtual network while you are working on this configuration.</span></span>
> 
> 

1. <span data-ttu-id="60dd9-203">Tooinstall hello en son sürümünü hello Azure Resource Manager PowerShell cmdlet'lerini gerekir.</span><span class="sxs-lookup"><span data-stu-id="60dd9-203">You'll need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="60dd9-204">Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) hello PowerShell cmdlet'lerini yükleme hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="60dd9-204">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span> <span data-ttu-id="60dd9-205">Bu yapılandırma için kullanacağınız hello cmdlet'leri ne tanımanız değerinden biraz farklı olabileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="60dd9-205">Note that hello cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="60dd9-206">Bu yönergelerde emin toouse hello cmdlet'leri belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="60dd9-206">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="60dd9-207">Merhaba mevcut ExpressRoute veya siteden siteye VPN ağ geçidini silin.</span><span class="sxs-lookup"><span data-stu-id="60dd9-207">Delete hello existing ExpressRoute or Site-to-Site VPN gateway.</span></span> <span data-ttu-id="60dd9-208">Aşağıdaki cmdlet, hello değerleri kendi değerlerinizle değiştirerek hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="60dd9-208">Use hello following cmdlet, replacing hello values with your own.</span></span>
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. <span data-ttu-id="60dd9-209">Merhaba sanal ağ şemasını dışarı aktarın.</span><span class="sxs-lookup"><span data-stu-id="60dd9-209">Export hello virtual network schema.</span></span> <span data-ttu-id="60dd9-210">Aşağıdaki PowerShell cmdlet'ini, hello değerleri kendi değerlerinizle değiştirerek hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="60dd9-210">Use hello following PowerShell cmdlet, replacing hello values with your own.</span></span>
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. <span data-ttu-id="60dd9-211">Merhaba ağ geçidi alt ağı/27 veya daha kısa bir önek (örneğin, / 26 veya /25) böylece hello ağ yapılandırma dosyası şeması düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="60dd9-211">Edit hello network configuration file schema so that hello gateway subnet is /27 or a shorter prefix (such as /26 or /25).</span></span> <span data-ttu-id="60dd9-212">Merhaba aşağıdaki örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="60dd9-212">See hello following example.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="60dd9-213">Yeterli IP adresi, sanal ağ tooincrease hello ağ geçidi alt ağı boyutuna sahip değilseniz, daha fazla IP adresi alanı tooadd gerekir.</span><span class="sxs-lookup"><span data-stu-id="60dd9-213">If you don't have enough IP addresses left in your virtual network tooincrease hello gateway subnet size, you need tooadd more IP address space.</span></span> <span data-ttu-id="60dd9-214">Merhaba yapılandırma şeması hakkında daha fazla bilgi için bkz: [Azure Virtual Network yapılandırma şeması](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="60dd9-214">For more information about hello configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. <span data-ttu-id="60dd9-215">Önceki ağ geçidiniz siteden siteye VPN ise, da hello bağlantı türü çok değiştirmelisiniz**adanmış**.</span><span class="sxs-lookup"><span data-stu-id="60dd9-215">If your previous gateway was a Site-to-Site VPN, you must also change hello connection type too**Dedicated**.</span></span>
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. <span data-ttu-id="60dd9-216">Bu noktada, hiçbir ağ geçidi olmayan bir VNet’e sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="60dd9-216">At this point, you'll have a VNet with no gateways.</span></span> <span data-ttu-id="60dd9-217">toocreate yeni ağ geçitleri ve bağlantılarınızı tamamlamak, devam edebilmeniz [4. adım - bir ExpressRoute ağ geçidi oluşturma](#gw), önceki adımları kümesini hello bulunan.</span><span class="sxs-lookup"><span data-stu-id="60dd9-217">toocreate new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in hello preceding set of steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60dd9-218">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="60dd9-218">Next steps</span></span>
<span data-ttu-id="60dd9-219">ExpressRoute hakkında daha fazla bilgi için bkz: Merhaba [ExpressRoute SSS](expressroute-faqs.md)</span><span class="sxs-lookup"><span data-stu-id="60dd9-219">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md)</span></span>

