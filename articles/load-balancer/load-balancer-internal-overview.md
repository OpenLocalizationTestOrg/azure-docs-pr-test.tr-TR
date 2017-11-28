---
title: "aaaInternal yük dengeleyici genel bakış | Microsoft Docs"
description: "İç yük dengeleyici ve özellikleri için genel bakış. Bir yük dengeleyici Azure ve olası senaryolar için tooconfigure iç uç noktaları nasıl çalışır?"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 36065bfe-0ef1-46f9-a9e1-80b229105c85
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 9a901aad224d8821c154e130e142699d57282b25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="internal-load-balancer-overview"></a><span data-ttu-id="49c8a-103">İç yük dengeleyiciye genel bakış</span><span class="sxs-lookup"><span data-stu-id="49c8a-103">Internal load balancer overview</span></span>

<span data-ttu-id="49c8a-104">Merhaba Internet'e yönelik Yük Dengeleyici, hello iç yük dengeleyiciye (ILB) trafiği yalnızca tooresources hello bulut hizmeti veya VPN tooaccess hello Azure altyapı kullanarak içinde yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="49c8a-104">Unlike hello Internet facing load balancer, hello internal load balancer (ILB) directs traffic only tooresources inside hello cloud service or using VPN tooaccess hello Azure infrastructure.</span></span> <span data-ttu-id="49c8a-105">böylece hiçbir zaman doğrudan gösterilen tooan Internet uç noktası olmaz hello altyapı erişim toohello yük dengeli sanal IP adresleri (VIP) bir bulut hizmeti ya da bir sanal ağ kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="49c8a-105">hello infrastructure restricts access toohello load balanced virtual IP addresses (VIPs) of a Cloud Service or a Virtual Network so that they will never be directly exposed tooan Internet endpoint.</span></span> <span data-ttu-id="49c8a-106">Bu iş (LOB) uygulamaları toorun Azure iç satırının sağlar ve hello bulut içinde veya kaynakları şirket içi erişilen.</span><span class="sxs-lookup"><span data-stu-id="49c8a-106">This enables internal line of business (LOB) applications toorun in Azure and be accessed from within hello cloud or from resources on-premises.</span></span>

## <a name="why-you-may-need-an-internal-load-balancer"></a><span data-ttu-id="49c8a-107">Bir iç yük dengeleyici neden ihtiyacınız</span><span class="sxs-lookup"><span data-stu-id="49c8a-107">Why you may need an internal load balancer</span></span>

<span data-ttu-id="49c8a-108">Azure iç yük dengeleyici (ILB) Yük Dengeleme bir bulut hizmeti veya bölgesel kapsama sahip bir sanal ağ içinde bulunan sanal makineler arasında sağlar.</span><span class="sxs-lookup"><span data-stu-id="49c8a-108">Azure Internal Load Balancing (ILB) provides load balancing between virtual machines that reside inside of a cloud service or a virtual network with a regional scope.</span></span> <span data-ttu-id="49c8a-109">Merhaba kullanın ve bölgesel kapsama sahip sanal ağ yapılandırması hakkında daha fazla bilgi için bkz: [bölgesel sanal ağlar](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) hello Azure blogu içinde.</span><span class="sxs-lookup"><span data-stu-id="49c8a-109">For information about hello use and configuration of virtual networks with a regional scope, see [Regional Virtual Networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in hello Azure blog.</span></span> <span data-ttu-id="49c8a-110">Benzeşim grubu için yapılandırılmış mevcut sanal ağlar ILB’yi kullanamaz.</span><span class="sxs-lookup"><span data-stu-id="49c8a-110">Existing virtual networks that have been configured for an affinity group cannot use ILB.</span></span>

<span data-ttu-id="49c8a-111">ILB hello şu Yük Dengelemesi türlerini sağlar:</span><span class="sxs-lookup"><span data-stu-id="49c8a-111">ILB enables hello following types of load balancing:</span></span>

* <span data-ttu-id="49c8a-112">Bir bulut hizmetinde hello içinde bulunan sanal makinelerin sanal makineleri tooa kümesinden aynı bulut hizmeti (bkz: Şekil 1).</span><span class="sxs-lookup"><span data-stu-id="49c8a-112">Within a cloud service, from virtual machines tooa set of virtual machines that reside within hello same cloud service (see Figure 1).</span></span>
* <span data-ttu-id="49c8a-113">Bir sanal ağ içindeki sanal makinelerden hello sanal ağ tooa kümesi içinde hello duran sanal makineleri aynı sanal Merhaba, bulut hizmeti (bkz: Şekil 2) ağ.</span><span class="sxs-lookup"><span data-stu-id="49c8a-113">Within a virtual network, from virtual machines in hello virtual network tooa set of virtual machines that reside within hello same cloud service of hello virtual network (see Figure 2).</span></span>
* <span data-ttu-id="49c8a-114">Bir şirket içi sanal ağ için şirket içi bilgisayarları tooa kümesinden hello içinde bulunan sanal makineleri aynı sanal Merhaba, bulut hizmeti (bkz: Şekil 3) ağ.</span><span class="sxs-lookup"><span data-stu-id="49c8a-114">For a cross-premises virtual network, from on-premises computers tooa set of virtual machines that reside within hello same cloud service of hello virtual network (see Figure 3).</span></span>
* <span data-ttu-id="49c8a-115">Merhaba arka uç katmanları Internet'e değildir ancak gerektirir Internet'e, çok katmanlı uygulamalar hello Internet'e katmanından trafiği için Dengeleme yükler.</span><span class="sxs-lookup"><span data-stu-id="49c8a-115">Internet-facing, multi-tier applications in which hello back-end tiers are not Internet-facing but require load balancing for traffic from hello Internet-facing tier.</span></span>
* <span data-ttu-id="49c8a-116">Yük Dengeleme ek yük dengeleyici donanım veya yazılım gerektirmeden Azure üzerinde barındırılan LOB uygulamaları için.</span><span class="sxs-lookup"><span data-stu-id="49c8a-116">Load balancing for LOB applications hosted in Azure without requiring additional load balancer hardware or software.</span></span> <span data-ttu-id="49c8a-117">Şirket içi sunucular, trafik yükü olduğu bilgisayarları hello kümesinde dahil dengeli.</span><span class="sxs-lookup"><span data-stu-id="49c8a-117">Including on-premises servers in hello set of computers whose traffic is load balanced.</span></span>

## <a name="internet-facing-multi-tier-applications"></a><span data-ttu-id="49c8a-118">Internet'e yönelik çok katmanlı uygulamalar</span><span class="sxs-lookup"><span data-stu-id="49c8a-118">Internet facing multi-tier applications</span></span>

<span data-ttu-id="49c8a-119">Merhaba web katmanı Internet istemciler için Internet'e yönelik uç noktalar vardır ve Yük Dengelemesi kümesinin bir parçası olur.</span><span class="sxs-lookup"><span data-stu-id="49c8a-119">hello web tier has Internet facing endpoints for Internet clients and is part of a load-balanced set.</span></span> <span data-ttu-id="49c8a-120">Merhaba yük dengeleyici TCP bağlantı noktası 443 (HTTPS) toohello web sunucuları için web istemcilerinden gelen trafiği dağıtır.</span><span class="sxs-lookup"><span data-stu-id="49c8a-120">hello load balancer  distributes incoming traffic from web clients for TCP port 443 (HTTPS) toohello web servers.</span></span>

<span data-ttu-id="49c8a-121">Merhaba veritabanı hello web sunucuları için depolama alanı kullanan bir ILB uç nokta arkasında sunucularıdır.</span><span class="sxs-lookup"><span data-stu-id="49c8a-121">hello database servers are behind an ILB endpoint which hello web servers use for storage.</span></span> <span data-ttu-id="49c8a-122">Hangi trafiğidir hello ILB kümesindeki hello veritabanı sunucuları arasında dengeli uç nokta, bu veritabanı hizmeti yük dengeli.</span><span class="sxs-lookup"><span data-stu-id="49c8a-122">This database service load balanced endpoint, which traffic is load balanced across hello database servers in hello ILB set.</span></span>

<span data-ttu-id="49c8a-123">Görüntü gösterir aşağıdaki hello hello çok katmanlı uygulama Internet'e hello içinde aynı bulut hizmeti.</span><span class="sxs-lookup"><span data-stu-id="49c8a-123">hello following image shows hello Internet facing multi-tier application within hello same cloud service.</span></span>

![İç Yük Dengeleme tek bulut hizmeti](./media/load-balancer-internal-overview/IC736321.png)

<span data-ttu-id="49c8a-125">Şekil 1 - Internet'e yönelik çok katmanlı uygulama</span><span class="sxs-lookup"><span data-stu-id="49c8a-125">Figure 1 - Internet facing multi-tier application</span></span>

<span data-ttu-id="49c8a-126">Merhaba ILB hello ILB için bir alıcı hello hizmet hello daha tooa farklı bir bulut hizmeti dağıtıldığında çok katmanlı bir uygulama için başka bir olası kullanılmasıdır.</span><span class="sxs-lookup"><span data-stu-id="49c8a-126">Another possible use for a multi-tier application is when hello ILB deployed tooa different cloud service than hello one consuming hello service for hello ILB.</span></span>

<span data-ttu-id="49c8a-127">Bulut Hizmetleri aynı sanal ağ olacaktır hello kullanarak erişim toohello ILB uç noktası.</span><span class="sxs-lookup"><span data-stu-id="49c8a-127">Cloud services using hello same virtual network will have access toohello ILB endpoint.</span></span> <span data-ttu-id="49c8a-128">ön uç web sunucuları hello veritabanı arka uç farklı bir bulut hizmetinden içinde görüntü görülmektedir izleyerek ve kullanarak hello hello ILB uç nokta hello içinde aynı sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="49c8a-128">hello following image shows front-end web servers are in a different cloud service from hello database back-end and using hello ILB endpoint within hello same virtual network.</span></span>

![İç Yük Dengeleme bulut hizmetleri arasında](./media/load-balancer-internal-overview/IC744147.png)

<span data-ttu-id="49c8a-130">Şekil 2 - farklı bir bulut hizmeti ön uç sunucuları</span><span class="sxs-lookup"><span data-stu-id="49c8a-130">Figure 2 - Front-end servers in a different cloud service</span></span>

## <a name="intranet-line-of-business-applications"></a><span data-ttu-id="49c8a-131">İntranet iş kolu uygulamaları</span><span class="sxs-lookup"><span data-stu-id="49c8a-131">Intranet line of business applications</span></span>

<span data-ttu-id="49c8a-132">Merhaba şirket ağındaki istemcilerinden gelen trafiği VPN bağlantısı tooAzure ağ kullanarak LOB sunucularını hello kümesi boyunca alın yük dengeli.</span><span class="sxs-lookup"><span data-stu-id="49c8a-132">Traffic from clients on hello on-premises network get load-balanced across hello set of LOB servers using VPN connection tooAzure network.</span></span>

<span data-ttu-id="49c8a-133">Merhaba istemci makine noktası toosite VPN kullanarak Azure VPN hizmetinden erişim tooan IP adresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="49c8a-133">hello client machine will have access tooan IP address from Azure VPN service using point toosite VPN.</span></span> <span data-ttu-id="49c8a-134">Hello kullan hello hello ILB uç barındırılan LOB uygulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="49c8a-134">It allows hello use hello LOB application hosted behind hello ILB endpoint.</span></span>

![İç Yük Dengeleme noktası toosite VPN kullanarak](./media/load-balancer-internal-overview/IC744148.png)

<span data-ttu-id="49c8a-136">Şekil 3 - hello LB bitiş noktasının ardındaki barındırılan LOB uygulamaları</span><span class="sxs-lookup"><span data-stu-id="49c8a-136">Figure 3 - LOB applications hosted behind hello LB endpoint</span></span>

<span data-ttu-id="49c8a-137">Başka bir hello LOB toohave hello ILB uç nokta yapılandırıldığı bir site toosite VPN toohello sanal ağ senaryodur.</span><span class="sxs-lookup"><span data-stu-id="49c8a-137">Another scenario for hello LOB is toohave a site toosite VPN toohello virtual network where hello ILB endpoint is configured.</span></span> <span data-ttu-id="49c8a-138">Bu, şirket içi ağ trafiği yönlendirilen toobe toohello ILB uç noktası sağlar.</span><span class="sxs-lookup"><span data-stu-id="49c8a-138">This allows on-premises network traffic toobe routed toohello ILB endpoint.</span></span>

![İç Yük Dengeleme site toosite VPN kullanma](./media/load-balancer-internal-overview/IC744150.png)

<span data-ttu-id="49c8a-140">Şekil 4 - şirket içi ağ trafiğini yönlendirilen toohello ILB uç noktası</span><span class="sxs-lookup"><span data-stu-id="49c8a-140">Figure 4 - On-premises network traffic routed toohello ILB endpoint</span></span>

## <a name="limitations"></a><span data-ttu-id="49c8a-141">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="49c8a-141">Limitations</span></span>

<span data-ttu-id="49c8a-142">İç yük dengeleyici yapılandırmalarının SNAT desteklemez.</span><span class="sxs-lookup"><span data-stu-id="49c8a-142">Internal Load Balancer configurations do not support SNAT.</span></span> <span data-ttu-id="49c8a-143">Bu belge Hello bağlamda SNAT tooport maskelenmiş kaynak ağ adresi çevirisi başvurur.</span><span class="sxs-lookup"><span data-stu-id="49c8a-143">In hello context of this document, SNAT refers tooport masquerading source  network address translation.</span></span>  <span data-ttu-id="49c8a-144">Bu, burada bir VM'de yük dengeleyici havuzuna tooreach hello ilgili iç yük dengeleyicinin ön uç IP adresi gerekiyor tooscenarios geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="49c8a-144">This applies tooscenarios where a VM in a load balancer pool needs tooreach hello respective internal Load Balancer's frontend IP address.</span></span> <span data-ttu-id="49c8a-145">Bu senaryo için iç yük dengeleyici desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="49c8a-145">This scenario is not supported for internal Load Balancer.</span></span> <span data-ttu-id="49c8a-146">Bağlantı hataları Hello akış yükü dengelenmiş toohello hello akış kaynaklanan VM olduğunda meydana gelir.</span><span class="sxs-lookup"><span data-stu-id="49c8a-146">Connection failures will occur when hello flow is load balanced toohello VM which originated hello flow.</span></span> <span data-ttu-id="49c8a-147">Bir proxy stili yük dengeleyici gibi senaryolar için kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="49c8a-147">You must use a proxy style load balancer for such scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49c8a-148">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="49c8a-148">Next Steps</span></span>

[<span data-ttu-id="49c8a-149">Azure yük dengeleyici için Azure Resource Manager desteği</span><span class="sxs-lookup"><span data-stu-id="49c8a-149">Azure Resource Manager support for Azure Load Balancer</span></span>](load-balancer-arm.md)

[<span data-ttu-id="49c8a-150">Internet'e yönelik Yük Dengeleyici yapılandırma kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="49c8a-150">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="49c8a-151">Bir iç yük dengeleyici yapılandırma kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="49c8a-151">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="49c8a-152">Yük dengeleyici dağıtım modu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="49c8a-152">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="49c8a-153">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="49c8a-153">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
