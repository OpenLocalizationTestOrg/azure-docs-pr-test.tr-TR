---
title: "İç yük dengeleyici genel bakış | Microsoft Docs"
description: "İç yük dengeleyici ve özellikleri için genel bakış. Bir yük dengeleyici iç uç noktalar yapılandırmak Azure ve olası senaryoları için nasıl çalışır?"
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
ms.openlocfilehash: d324aaf8ec2c8766d5cf11452158d14c19cba4d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="internal-load-balancer-overview"></a><span data-ttu-id="fbc39-103">İç yük dengeleyiciye genel bakış</span><span class="sxs-lookup"><span data-stu-id="fbc39-103">Internal load balancer overview</span></span>

<span data-ttu-id="fbc39-104">Yük Dengeleyici Internet'e, iç yük dengeleyiciye (ILB) yalnızca bulut hizmeti ya da Azure altyapı erişmek için VPN kullanarak iç kaynaklara trafiğini yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="fbc39-104">Unlike the Internet facing load balancer, the internal load balancer (ILB) directs traffic only to resources inside the cloud service or using VPN to access the Azure infrastructure.</span></span> <span data-ttu-id="fbc39-105">Böylece bunlar hiçbir zaman doğrudan bir Internet uç noktasına sunulur altyapı yük dengeli sanal IP adreslerine bir bulut hizmeti ya da bir sanal ağ (VIP) erişimi sınırlandırır.</span><span class="sxs-lookup"><span data-stu-id="fbc39-105">The infrastructure restricts access to the load balanced virtual IP addresses (VIPs) of a Cloud Service or a Virtual Network so that they will never be directly exposed to an Internet endpoint.</span></span> <span data-ttu-id="fbc39-106">Bu, iç Azure'da çalıştırmak ve bulut içinde veya kaynakları şirket içi erişilen için iş kolu (LOB) uygulamaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="fbc39-106">This enables internal line of business (LOB) applications to run in Azure and be accessed from within the cloud or from resources on-premises.</span></span>

## <a name="why-you-may-need-an-internal-load-balancer"></a><span data-ttu-id="fbc39-107">Bir iç yük dengeleyici neden ihtiyacınız</span><span class="sxs-lookup"><span data-stu-id="fbc39-107">Why you may need an internal load balancer</span></span>

<span data-ttu-id="fbc39-108">Azure iç yük dengeleyici (ILB) Yük Dengeleme bir bulut hizmeti veya bölgesel kapsama sahip bir sanal ağ içinde bulunan sanal makineler arasında sağlar.</span><span class="sxs-lookup"><span data-stu-id="fbc39-108">Azure Internal Load Balancing (ILB) provides load balancing between virtual machines that reside inside of a cloud service or a virtual network with a regional scope.</span></span> <span data-ttu-id="fbc39-109">Kullanım ve bölgesel kapsama sahip sanal ağ yapılandırması hakkında daha fazla bilgi için bkz: [bölgesel sanal ağlar](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) Azure Web günlüğündeki.</span><span class="sxs-lookup"><span data-stu-id="fbc39-109">For information about the use and configuration of virtual networks with a regional scope, see [Regional Virtual Networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in the Azure blog.</span></span> <span data-ttu-id="fbc39-110">Benzeşim grubu için yapılandırılmış mevcut sanal ağlar ILB’yi kullanamaz.</span><span class="sxs-lookup"><span data-stu-id="fbc39-110">Existing virtual networks that have been configured for an affinity group cannot use ILB.</span></span>

<span data-ttu-id="fbc39-111">ILB Yük Dengeleme aşağıdaki türleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="fbc39-111">ILB enables the following types of load balancing:</span></span>

* <span data-ttu-id="fbc39-112">Sanal makineler aynı bulut hizmetinde bulunan sanal makineler kümesi için bir bulut hizmetinden içinde (bkz: Şekil 1).</span><span class="sxs-lookup"><span data-stu-id="fbc39-112">Within a cloud service, from virtual machines to a set of virtual machines that reside within the same cloud service (see Figure 1).</span></span>
* <span data-ttu-id="fbc39-113">(Bkz: Şekil 2) sanal aynı bulut hizmetinde bulunan sanal makineler kümesi için sanal ağdaki sanal makinelerden bir sanal ağ içindeki ağ.</span><span class="sxs-lookup"><span data-stu-id="fbc39-113">Within a virtual network, from virtual machines in the virtual network to a set of virtual machines that reside within the same cloud service of the virtual network (see Figure 2).</span></span>
* <span data-ttu-id="fbc39-114">(Bkz: Şekil 3) şirket içi bilgisayarlardan sanal aynı bulut hizmetinde bulunan sanal makineler kümesi için şirket içi sanal ağ için ağ.</span><span class="sxs-lookup"><span data-stu-id="fbc39-114">For a cross-premises virtual network, from on-premises computers to a set of virtual machines that reside within the same cloud service of the virtual network (see Figure 3).</span></span>
* <span data-ttu-id="fbc39-115">Arka uç katmanları Internet'e değildir ancak Internet'e yönelik katmanından trafiği için Yük Dengeleme gerektiren Internet'e, çok katmanlı uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="fbc39-115">Internet-facing, multi-tier applications in which the back-end tiers are not Internet-facing but require load balancing for traffic from the Internet-facing tier.</span></span>
* <span data-ttu-id="fbc39-116">Yük Dengeleme ek yük dengeleyici donanım veya yazılım gerektirmeden Azure üzerinde barındırılan LOB uygulamaları için.</span><span class="sxs-lookup"><span data-stu-id="fbc39-116">Load balancing for LOB applications hosted in Azure without requiring additional load balancer hardware or software.</span></span> <span data-ttu-id="fbc39-117">Şirket içi sunucular, trafik yükü olduğu bilgisayarları kümesinde dahil dengeli.</span><span class="sxs-lookup"><span data-stu-id="fbc39-117">Including on-premises servers in the set of computers whose traffic is load balanced.</span></span>

## <a name="internet-facing-multi-tier-applications"></a><span data-ttu-id="fbc39-118">Internet'e yönelik çok katmanlı uygulamalar</span><span class="sxs-lookup"><span data-stu-id="fbc39-118">Internet facing multi-tier applications</span></span>

<span data-ttu-id="fbc39-119">Web katmanı Internet istemciler için Internet'e yönelik uç noktalar vardır ve Yük Dengelemesi kümesinin bir parçası olur.</span><span class="sxs-lookup"><span data-stu-id="fbc39-119">The web tier has Internet facing endpoints for Internet clients and is part of a load-balanced set.</span></span> <span data-ttu-id="fbc39-120">Yük Dengeleyici web sunucularına TCP bağlantı noktası 443 (HTTPS) için web istemcilerinden gelen trafiği dağıtır.</span><span class="sxs-lookup"><span data-stu-id="fbc39-120">The load balancer  distributes incoming traffic from web clients for TCP port 443 (HTTPS) to the web servers.</span></span>

<span data-ttu-id="fbc39-121">Veritabanı sunucuları, web sunucuları için depolama alanı kullanan bir ILB uç nokta arkasındaki.</span><span class="sxs-lookup"><span data-stu-id="fbc39-121">The database servers are behind an ILB endpoint which the web servers use for storage.</span></span> <span data-ttu-id="fbc39-122">ILB kümesindeki veritabanı sunucuları arasında dengeli trafiğidir uç nokta, bu veritabanı hizmeti yük dengeli.</span><span class="sxs-lookup"><span data-stu-id="fbc39-122">This database service load balanced endpoint, which traffic is load balanced across the database servers in the ILB set.</span></span>

<span data-ttu-id="fbc39-123">Aşağıdaki görüntüde aynı bulut hizmetinde çok katmanlı uygulama Internet'e gösterir.</span><span class="sxs-lookup"><span data-stu-id="fbc39-123">The following image shows the Internet facing multi-tier application within the same cloud service.</span></span>

![İç Yük Dengeleme tek bulut hizmeti](./media/load-balancer-internal-overview/IC736321.png)

<span data-ttu-id="fbc39-125">Şekil 1 - Internet'e yönelik çok katmanlı uygulama</span><span class="sxs-lookup"><span data-stu-id="fbc39-125">Figure 1 - Internet facing multi-tier application</span></span>

<span data-ttu-id="fbc39-126">ILB hizmet ILB için tüketen olandan farklı bir bulut hizmeti dağıtıldığında çok katmanlı bir uygulama için başka bir olası kullanılmasıdır.</span><span class="sxs-lookup"><span data-stu-id="fbc39-126">Another possible use for a multi-tier application is when the ILB deployed to a different cloud service than the one consuming the service for the ILB.</span></span>

<span data-ttu-id="fbc39-127">ILB uç noktası aynı sanal ağ kullanarak bulut hizmetlerine erişebilir.</span><span class="sxs-lookup"><span data-stu-id="fbc39-127">Cloud services using the same virtual network will have access to the ILB endpoint.</span></span> <span data-ttu-id="fbc39-128">Aşağıdaki resimde, ön uç web sunucusu farklı bir bulut hizmeti veritabanı arka uç ve ILB uç noktası aynı sanal ağda kullanarak olduğundan gösterir.</span><span class="sxs-lookup"><span data-stu-id="fbc39-128">The following image shows front-end web servers are in a different cloud service from the database back-end and using the ILB endpoint within the same virtual network.</span></span>

![İç Yük Dengeleme bulut hizmetleri arasında](./media/load-balancer-internal-overview/IC744147.png)

<span data-ttu-id="fbc39-130">Şekil 2 - farklı bir bulut hizmeti ön uç sunucuları</span><span class="sxs-lookup"><span data-stu-id="fbc39-130">Figure 2 - Front-end servers in a different cloud service</span></span>

## <a name="intranet-line-of-business-applications"></a><span data-ttu-id="fbc39-131">İntranet iş kolu uygulamaları</span><span class="sxs-lookup"><span data-stu-id="fbc39-131">Intranet line of business applications</span></span>

<span data-ttu-id="fbc39-132">Şirket içi ağda istemcilerinden gelen trafiği almak Azure ağı için VPN bağlantısını kullanarak iş KOLU sunucuları arasında Yük Dengelemesi.</span><span class="sxs-lookup"><span data-stu-id="fbc39-132">Traffic from clients on the on-premises network get load-balanced across the set of LOB servers using VPN connection to Azure network.</span></span>

<span data-ttu-id="fbc39-133">İstemci makine erişimine, noktasını site VPN kullanarak Azure VPN hizmetinden bir IP adresine sahip olur.</span><span class="sxs-lookup"><span data-stu-id="fbc39-133">The client machine will have access to an IP address from Azure VPN service using point to site VPN.</span></span> <span data-ttu-id="fbc39-134">ILB uç nokta barındırılan LOB uygulaması kullanımına izin verir.</span><span class="sxs-lookup"><span data-stu-id="fbc39-134">It allows the use the LOB application hosted behind the ILB endpoint.</span></span>

![Noktası site VPN kullanarak iç Yük Dengeleme](./media/load-balancer-internal-overview/IC744148.png)

<span data-ttu-id="fbc39-136">Şekil 3 - LB bitiş noktasının ardındaki barındırılan LOB uygulamaları</span><span class="sxs-lookup"><span data-stu-id="fbc39-136">Figure 3 - LOB applications hosted behind the LB endpoint</span></span>

<span data-ttu-id="fbc39-137">Başka bir senaryo için LOB ILB uç nokta yapılandırıldığı sanal ağ için siteden siteye VPN olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fbc39-137">Another scenario for the LOB is to have a site to site VPN to the virtual network where the ILB endpoint is configured.</span></span> <span data-ttu-id="fbc39-138">Bu, şirket içi ağ trafiğini ILB uç noktasına yönlendirilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="fbc39-138">This allows on-premises network traffic to be routed to the ILB endpoint.</span></span>

![Siteden siteye VPN kullanarak iç Yük Dengeleme](./media/load-balancer-internal-overview/IC744150.png)

<span data-ttu-id="fbc39-140">Şekil 4 - ILB uç noktasına yönlendirilen şirket içi ağ trafiği</span><span class="sxs-lookup"><span data-stu-id="fbc39-140">Figure 4 - On-premises network traffic routed to the ILB endpoint</span></span>

## <a name="limitations"></a><span data-ttu-id="fbc39-141">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="fbc39-141">Limitations</span></span>

<span data-ttu-id="fbc39-142">İç yük dengeleyici yapılandırmalarının SNAT desteklemez.</span><span class="sxs-lookup"><span data-stu-id="fbc39-142">Internal Load Balancer configurations do not support SNAT.</span></span> <span data-ttu-id="fbc39-143">Bu belge bağlamında, bağlantı noktası maskelenmiş kaynak ağ adresi çevirisi için SNAT başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="fbc39-143">In the context of this document, SNAT refers to port masquerading source  network address translation.</span></span>  <span data-ttu-id="fbc39-144">Burada ilgili iç yük dengeleyicinin ön uç IP adresi ulaşmak için bir VM'de yük dengeleyici havuzu gerekiyor senaryoları için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="fbc39-144">This applies to scenarios where a VM in a load balancer pool needs to reach the respective internal Load Balancer's frontend IP address.</span></span> <span data-ttu-id="fbc39-145">Bu senaryo için iç yük dengeleyici desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="fbc39-145">This scenario is not supported for internal Load Balancer.</span></span> <span data-ttu-id="fbc39-146">Bağlantı hataları Akış akış kaynaklanan VM dengelendiği olduğunda meydana gelir.</span><span class="sxs-lookup"><span data-stu-id="fbc39-146">Connection failures will occur when the flow is load balanced to the VM which originated the flow.</span></span> <span data-ttu-id="fbc39-147">Bir proxy stili yük dengeleyici gibi senaryolar için kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fbc39-147">You must use a proxy style load balancer for such scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbc39-148">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="fbc39-148">Next Steps</span></span>

[<span data-ttu-id="fbc39-149">Azure yük dengeleyici için Azure Resource Manager desteği</span><span class="sxs-lookup"><span data-stu-id="fbc39-149">Azure Resource Manager support for Azure Load Balancer</span></span>](load-balancer-arm.md)

[<span data-ttu-id="fbc39-150">Internet'e yönelik Yük Dengeleyici yapılandırma kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="fbc39-150">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="fbc39-151">Bir iç yük dengeleyici yapılandırma kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="fbc39-151">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="fbc39-152">Yük dengeleyici dağıtım modu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fbc39-152">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="fbc39-153">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fbc39-153">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
