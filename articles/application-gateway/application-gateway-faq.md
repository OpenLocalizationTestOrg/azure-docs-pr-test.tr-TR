---
title: "Azure uygulama ağ geçidi sorular aaaFrequently | Microsoft Docs"
description: "Bu sayfayı yanıtlar sağlayan Azure uygulama ağ geçidi hakkında sorular toofrequently"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d54ee7ec-4d6b-4db7-8a17-6513fda7e392
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: b2df3a82a71a3264d3d34d317d08e4b4f72c6e3e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-application-gateway"></a><span data-ttu-id="c8e26-103">Uygulama ağ geçidi için sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="c8e26-103">Frequently asked questions for Application Gateway</span></span>

## <a name="general"></a><span data-ttu-id="c8e26-104">Genel</span><span class="sxs-lookup"><span data-stu-id="c8e26-104">General</span></span>

<span data-ttu-id="c8e26-105">**Q. Uygulama ağ geçidi nedir?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-105">**Q. What is Application Gateway?**</span></span>

<span data-ttu-id="c8e26-106">Azure uygulama ağ geçidi uygulama teslim denetleyici (ADC) bir hizmet olarak çeşitli katman 7 Yük Dengeleme, uygulamalarınız için sunumu ' dir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-106">Azure Application Gateway is an Application Delivery Controller (ADC) as a service, offering various layer 7 load balancing capabilities for your applications.</span></span> <span data-ttu-id="c8e26-107">Azure tarafından tam olarak yönetilen, yüksek oranda kullanılabilir ve ölçeklenebilir hizmet sunar.</span><span class="sxs-lookup"><span data-stu-id="c8e26-107">It offers highly available and scalable service, which is fully managed by Azure.</span></span>

<span data-ttu-id="c8e26-108">**Q. Hangi özelliklerin uygulama ağ geçidi destekliyor mu?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-108">**Q. What features does Application Gateway support?**</span></span>

<span data-ttu-id="c8e26-109">Uygulama ağ geçidi SSL boşaltma ve bitiş tooend SSL, Web uygulaması güvenlik duvarı, tanımlama bilgisi tabanlı oturum benzeşimi, url yolu tabanlı yönlendirme, çoklu siteyi barındıran ve diğerleri destekler.</span><span class="sxs-lookup"><span data-stu-id="c8e26-109">Application Gateway supports SSL offloading and end tooend SSL, Web Application Firewall, cookie-based session affinity, url path-based routing, multi site hosting, and others.</span></span> <span data-ttu-id="c8e26-110">Desteklenen özelliklerin tam listesi için ziyaret [giriş tooApplication ağ geçidi](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="c8e26-110">For a full list of supported features, visit [Introduction tooApplication Gateway](application-gateway-introduction.md)</span></span>

<span data-ttu-id="c8e26-111">**Q. Uygulama ağ geçidi ve Azure yük dengeleyici arasındaki hello fark nedir?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-111">**Q. What is hello difference between Application Gateway and Azure Load Balancer?**</span></span>

<span data-ttu-id="c8e26-112">Uygulama ağ geçidi web trafiği ile yalnızca (HTTP/HTTPS/WebSocket) çalıştığı anlamına gelir bir katman 7 yük dengeleyicidir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-112">Application Gateway is a layer 7 load balancer, which means it works with web traffic only (HTTP/HTTPS/WebSocket).</span></span> <span data-ttu-id="c8e26-113">Bu, Yük Dengeleme trafiğini SSL sonlandırma, tanımlama bilgisi tabanlı oturum benzeşimi ve hepsini bir kez gibi özellikleri destekler.</span><span class="sxs-lookup"><span data-stu-id="c8e26-113">It supports capabilities such as SSL termination, cookie-based session affinity, and round robin for load balancing traffic.</span></span> <span data-ttu-id="c8e26-114">Yük Dengeleyici, 4 (TCP/UDP) katmanında bakiyelerini trafiğin yük.</span><span class="sxs-lookup"><span data-stu-id="c8e26-114">Load Balancer, load balances traffic at layer 4 (TCP/UDP).</span></span>

<span data-ttu-id="c8e26-115">**Q. Hangi protokollerin, uygulama ağ geçidi destekliyor mu?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-115">**Q. What protocols does Application Gateway support?**</span></span>

<span data-ttu-id="c8e26-116">Uygulama ağ geçidi, HTTP, HTTPS ve WebSocket destekler.</span><span class="sxs-lookup"><span data-stu-id="c8e26-116">Application Gateway supports HTTP, HTTPS, and WebSocket.</span></span>

<span data-ttu-id="c8e26-117">**Q. Hangi kaynaklara arka uç havuzu bir parçası olarak bugün destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-117">**Q. What resources are supported today as part of backend pool?**</span></span>

<span data-ttu-id="c8e26-118">Arka uç havuzları olan NIC'ler, sanal makine ölçek kümeleri, genel IP'ler birleştirilebilen, iç IP, tam etki alanı adları (FQDN) ve çok kiracılı arka Azure Web Apps gibi uçları.</span><span class="sxs-lookup"><span data-stu-id="c8e26-118">Backend pools can be composed of NICs, virtual machine scale sets, public IPs, internal IPs, fully qualified domain names (FQDN), and multi-tenant back-ends like Azure Web Apps.</span></span> <span data-ttu-id="c8e26-119">Uygulama ağ geçidi arka uç havuzu üye olmayan tooan kullanılabilirlik kümesine bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="c8e26-119">Application Gateway backend pool members are not tied tooan availability set.</span></span> <span data-ttu-id="c8e26-120">IP bağlantısını sahip oldukları sürece arka uç havuzları üyeleri kümeler, veri merkezleri arasında veya Azure dışında olabilir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-120">Members of backend pools can be across clusters, data centers, or outside of Azure as long as they have IP connectivity.</span></span>

<span data-ttu-id="c8e26-121">**Q. Hangi bölgeleri hizmettir hello kullanılabilir?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-121">**Q. What regions is hello service available in?**</span></span>

<span data-ttu-id="c8e26-122">Uygulama ağ geçidi genel Azure tüm bölgelerde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-122">Application Gateway is available in all regions of global Azure.</span></span> <span data-ttu-id="c8e26-123">Ayrıca, kullanılabilir [Azure Çin](https://www.azure.cn/) ve [Azure kamu](https://azure.microsoft.com/en-us/overview/clouds/government/)</span><span class="sxs-lookup"><span data-stu-id="c8e26-123">It is also available in [Azure China](https://www.azure.cn/) and [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)</span></span>

<span data-ttu-id="c8e26-124">**Q. Bu Aboneliğimi için adanmış bir dağıtımı veya müşterileri arasında paylaşılan?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-124">**Q. Is this a dedicated deployment for my subscription or is it shared across customers?**</span></span>

<span data-ttu-id="c8e26-125">Uygulama ağ geçidi, sanal ağınızda adanmış bir dağıtımıdır.</span><span class="sxs-lookup"><span data-stu-id="c8e26-125">Application Gateway is a dedicated deployment in your virtual network.</span></span>

<span data-ttu-id="c8e26-126">**Q. İş HTTP -> desteklenen HTTPS yeniden yönlendirmesi?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-126">**Q. Is HTTP->HTTPS redirection supported?**</span></span>

<span data-ttu-id="c8e26-127">Yeniden yönlendirme desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-127">Redirection is supported.</span></span> <span data-ttu-id="c8e26-128">Ziyaret [uygulama ağ geçidi yeniden yönlendirmeye genel bakış](application-gateway-redirect-overview.md) toolearn daha fazla.</span><span class="sxs-lookup"><span data-stu-id="c8e26-128">Visit [Application Gateway redirect overview](application-gateway-redirect-overview.md) toolearn more.</span></span>

<span data-ttu-id="c8e26-129">**Q. Hangi sırayla dinleyicileri işlenir?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-129">**Q. In what order are listeners processed?**</span></span>

<span data-ttu-id="c8e26-130">Dinleyicileri bunlar gösterilir hello sırada işlenir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-130">Listeners are processed in hello order they are shown.</span></span> <span data-ttu-id="c8e26-131">Gelen bir istek temel dinleyici eşleşiyorsa, bu nedenle ilk işler.</span><span class="sxs-lookup"><span data-stu-id="c8e26-131">For that reason if a basic listener matches an incoming request it processes it first.</span></span>  <span data-ttu-id="c8e26-132">Çok siteli dinleyicileri yönlendirilmiş toohello doğru arka uç temel dinleyici tooensure trafiğidir önce yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-132">Multi-site listeners should be configured before a basic listener tooensure traffic is routed toohello correct back-end.</span></span>

<span data-ttu-id="c8e26-133">**Q. Uygulama ağ geçidi IP ve DNS nerede bulabilirim?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-133">**Q. Where do I find Application Gateway’s IP and DNS?**</span></span>

<span data-ttu-id="c8e26-134">Bir ortak IP adresi bir uç nokta kullanılırken, bu bilgileri hello ortak IP adresi kaynağı veya hello genel bakış sayfasında hello portal hello uygulama ağ geçidi için bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-134">When using a public IP address as an endpoint, this information can be found on hello public IP address resource or on hello Overview page for hello Application Gateway in hello portal.</span></span> <span data-ttu-id="c8e26-135">İç IP adresleri için bu hello genel bakış sayfasında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-135">For internal IP addresses, this can be found on hello Overview page.</span></span>

<span data-ttu-id="c8e26-136">**Q. Merhaba IP veya DNS hello uygulama ağ geçidi hello ömrü boyunca değişiyor mu?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-136">**Q. Does hello IP or DNS change over hello lifetime of hello Application Gateway?**</span></span>

<span data-ttu-id="c8e26-137">Merhaba ağ geçidi durduruldu ve hello müşteri tarafından başlatılan hello VIP değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8e26-137">hello VIP can change if hello gateway is stopped and started by hello customer.</span></span> <span data-ttu-id="c8e26-138">Uygulama ağ geçidi ile ilişkili DNS Hello hello yaşam döngüsü hello ağ geçidi değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="c8e26-138">hello DNS associated with Application Gateway does not change over hello lifecycle of hello gateway.</span></span> <span data-ttu-id="c8e26-139">Bu nedenle, olmasından hello uygulama ağ geçidi toohello DNS adresi gelin ve CNAME diğer adını toouse önerilir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-139">For this reason, it is recommended toouse a CNAME alias and point it toohello DNS address of hello Application Gateway.</span></span>

<span data-ttu-id="c8e26-140">**Q. Uygulama ağ geçidi, statik IP destekliyor mu?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-140">**Q. Does Application Gateway support static IP?**</span></span>

<span data-ttu-id="c8e26-141">Hayır, uygulama ağ geçidi ortak statik IP adresleri desteklemez, ancak statik iç IP desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="c8e26-141">No, Application Gateway does not support static public IP addresses, but it does support static internal IPs.</span></span>

<span data-ttu-id="c8e26-142">**Q. Uygulama ağ geçidi birden çok ortak IP hello ağ geçidinde destekliyor mu?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-142">**Q. Does Application Gateway support multiple public IPs on hello gateway?**</span></span>

<span data-ttu-id="c8e26-143">Yalnızca bir genel IP adresi, bir uygulama ağ geçidi üzerinde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-143">Only one public IP address is supported on an Application Gateway.</span></span>

<span data-ttu-id="c8e26-144">**Q. Uygulama ağ geçidi x-iletilen-için üstbilgiler destekliyor mu?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-144">**Q. Does Application Gateway support x-forwarded-for headers?**</span></span>

<span data-ttu-id="c8e26-145">Evet, uygulama ağ geçidi, x-iletilen-için x iletilen proto ekler ve toohello arka uç x iletilen bağlantı üstbilgileri hello isteği halinde iletilir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-145">Yes, Application Gateway inserts x-forwarded-for, x-forwarded-proto, and x-forwarded-port headers into hello request forwarded toohello backend.</span></span> <span data-ttu-id="c8e26-146">Merhaba x-iletilen-için üstbilgisi IP: BağlantıNoktası, virgülle ayrılmış listesini biçimidir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-146">hello format for x-forwarded-for header is a comma-separated list of IP:Port.</span></span> <span data-ttu-id="c8e26-147">Merhaba geçerli x iletilen proto http veya https değerler.</span><span class="sxs-lookup"><span data-stu-id="c8e26-147">hello valid values for x-forwarded-proto are http or https.</span></span> <span data-ttu-id="c8e26-148">X-iletilen-bağlantı noktası başlangıç bağlantı noktası uygulama ağ geçidi hello üst sınırına hangi hello isteğinde belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-148">X-forwarded-port specifies hello port at which hello request reached at hello Application Gateway.</span></span>

<span data-ttu-id="c8e26-149">**Q. Bir uygulama ağ geçidi toodeploy ne kadar sürer? My uygulama ağ geçidi, güncelleştirilen zaman hala çalışıyor mu?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-149">**Q. How long does it take toodeploy an Application Gateway? Does my Application Gateway still work when being updated?**</span></span>

<span data-ttu-id="c8e26-150">Yeni uygulama ağ geçidi dağıtımları too20 dakika tooprovision alabilir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-150">New Application Gateway deployments can take up too20 minutes tooprovision.</span></span> <span data-ttu-id="c8e26-151">Değişiklikleri tooinstance boyutu/sayısı kesintiye uğratan değildir ve hello ağ geçidi bu süre boyunca etkin kalır.</span><span class="sxs-lookup"><span data-stu-id="c8e26-151">Changes tooinstance size/count are not disruptive, and hello gateway remains active during this time.</span></span>

## <a name="configuration"></a><span data-ttu-id="c8e26-152">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c8e26-152">Configuration</span></span>

<span data-ttu-id="c8e26-153">**Q. Uygulama ağ geçidi, sanal bir ağa her zaman dağıtılır?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-153">**Q. Is Application Gateway always deployed in a virtual network?**</span></span>

<span data-ttu-id="c8e26-154">Evet, uygulama ağ geçidi her zaman bir sanal ağ alt ağında dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="c8e26-154">Yes, Application Gateway is always deployed in a virtual network subnet.</span></span> <span data-ttu-id="c8e26-155">Bu alt ağ yalnızca uygulama ağ geçitleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-155">This subnet can only contain Application Gateways.</span></span>

<span data-ttu-id="c8e26-156">**Q. Uygulama ağ geçidi tooinstances kendi sanal ağ dışından iletişim kurabilirsiniz?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-156">**Q. Can Application Gateway talk tooinstances outside its virtual network?**</span></span>

<span data-ttu-id="c8e26-157">Uygulama ağ geçidi IP bağlantısı var olduğu sürece, olarak hello sanal ağ dışında tooinstances iletişim kurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8e26-157">Application Gateway can talk tooinstances outside of hello virtual network that it is in as long as there is IP connectivity.</span></span> <span data-ttu-id="c8e26-158">Toouse düşünüyorsanız, arka uç havuzu üyeleri, ardından dahili Ips'ler gerektirir [VNET eşlemesi](../virtual-network/virtual-network-peering-overview.md) veya [VPN ağ geçidi](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="c8e26-158">If you plan toouse internal IPs as backend pool members, then it requires [VNET Peering](../virtual-network/virtual-network-peering-overview.md) or [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>

<span data-ttu-id="c8e26-159">**Q. Merhaba uygulama ağ geçidi alt ağdaki başka bir şey dağıtabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-159">**Q. Can I deploy anything else in hello Application Gateway subnet?**</span></span>

<span data-ttu-id="c8e26-160">Hayır, ancak diğer uygulama ağ geçitleri hello alt dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8e26-160">No, but you can deploy other application gateways in hello subnet.</span></span>

<span data-ttu-id="c8e26-161">**Q. Ağ güvenlik grupları hello uygulama ağ geçidi alt ağda destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-161">**Q. Are Network Security Groups supported on hello Application Gateway subnet?**</span></span>

<span data-ttu-id="c8e26-162">Ağ güvenlik grupları hello uygulama ağ geçidi alt ağda ile kısıtlamaları aşağıdaki hello desteklenir:</span><span class="sxs-lookup"><span data-stu-id="c8e26-162">Network Security Groups are supported on hello Application Gateway subnet with hello following restrictions:</span></span>

* <span data-ttu-id="c8e26-163">Özel durumlar gelen trafiği için bağlantı noktalarını 65503 65534 arka uç sistem durumu toowork için doğru koyun gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-163">Exceptions must be put in for incoming traffic on ports 65503-65534 for backend health toowork correctly.</span></span>

* <span data-ttu-id="c8e26-164">Giden internet bağlantısı engellenebilir değil.</span><span class="sxs-lookup"><span data-stu-id="c8e26-164">Outbound internet connectivity can not be blocked.</span></span>

* <span data-ttu-id="c8e26-165">Merhaba AzureLoadBalancer etiketi gelen trafiği için izin verilmelidir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-165">Traffic from hello AzureLoadBalancer tag must be allowed.</span></span>

<span data-ttu-id="c8e26-166">**Q. Uygulama ağ geçidi hello sınırları nelerdir? Bu sınırları artırmak?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-166">**Q. What are hello limits on Application Gateway? Can I increase these limits?**</span></span>

<span data-ttu-id="c8e26-167">Ziyaret [uygulama ağ geçidi sınırları](../azure-subscription-service-limits.md#application-gateway-limits) tooview hello sınırlar.</span><span class="sxs-lookup"><span data-stu-id="c8e26-167">Visit [Application Gateway Limits](../azure-subscription-service-limits.md#application-gateway-limits) tooview hello limits.</span></span>

<span data-ttu-id="c8e26-168">**Q. Uygulama ağ geçidi iç ve dış trafiği için aynı anda kullanabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-168">**Q. Can I use Application Gateway for both external and internal traffic simultaneously?**</span></span>

<span data-ttu-id="c8e26-169">Evet, uygulama ağ geçidini bir iç IP ve bir dış IP başına uygulama ağ geçidi destekler.</span><span class="sxs-lookup"><span data-stu-id="c8e26-169">Yes, Application Gateway supports having one internal IP and one external IP per Application Gateway.</span></span>

<span data-ttu-id="c8e26-170">**Q. VNet eşlemesi destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-170">**Q. Is VNet peering supported?**</span></span>

<span data-ttu-id="c8e26-171">Evet, VNet eşlemesi desteklenir ve Yük Dengeleme trafiğini diğer sanal ağlarda için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="c8e26-171">Yes, VNet peering is supported and is beneficial for load balancing traffic in other virtual networks.</span></span>

<span data-ttu-id="c8e26-172">**Q. Tooon içi sunucular, ExpressRoute ya da VPN tünelleri tarafından bağlıyken iletişim kurabilirsiniz?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-172">**Q. Can I talk tooon-premises servers when they are connected by ExpressRoute or VPN tunnels?**</span></span>

<span data-ttu-id="c8e26-173">Evet, trafiğe izin sürece.</span><span class="sxs-lookup"><span data-stu-id="c8e26-173">Yes, as long as traffic is allowed.</span></span>

<span data-ttu-id="c8e26-174">**Q. Birçok uygulama farklı bağlantı noktaları üzerinde hizmet veren bir arka uç havuzu olabilir mi?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-174">**Q. Can I have one backend pool serving many applications on different ports?**</span></span>

<span data-ttu-id="c8e26-175">Mikro hizmet mimarisi desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-175">Micro service architecture is supported.</span></span> <span data-ttu-id="c8e26-176">Farklı bağlantı noktaları üzerinde birden çok http yapılandırılan ayarları tooprobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-176">You would need multiple http settings configured tooprobe on different ports.</span></span>

<span data-ttu-id="c8e26-177">**Q. Özel araştırmalara joker karakter/regex yanıt verileri destekler mi?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-177">**Q. Do custom probes support wildcards/regex on response data?**</span></span>

<span data-ttu-id="c8e26-178">Özel araştırmalara joker karakter veya regex yanıt verileri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="c8e26-178">Custom probes do not support wildcard or regex on response data.</span></span> 

<span data-ttu-id="c8e26-179">**Q. Kuralları nasıl işlenir?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-179">**Q. How are rules processed?**</span></span>

<span data-ttu-id="c8e26-180">Yapılandırılmış olan hello sırada işlenir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-180">Rules are processed in hello order they are configured.</span></span> <span data-ttu-id="c8e26-181">Merhaba temel kural değerlendirilen bağlantı noktası önceki toohello çok siteli kurala göre trafiği eşleşecek şekilde trafiği temel kurallar tooreduce hello fırsat toohello uygunsuz arka uç yönlendirilen önce çok siteli kuralları yapılandırılır önerilir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-181">It is recommended that multi-site rules are configured before basic rules tooreduce hello chance that traffic is routed toohello inappropriate backend as hello basic rule would match traffic based on port prior toohello multi-site rule being evaluated.</span></span>

<span data-ttu-id="c8e26-182">**Q. Kuralları nasıl işlenir?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-182">**Q. How are rules processed?**</span></span>

<span data-ttu-id="c8e26-183">Oluşturuldukları hello sırada işlenir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-183">Rules are processed in hello order they are created.</span></span> <span data-ttu-id="c8e26-184">Çok siteli kuralları önce temel kurallar yapılandırılır önerilir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-184">It is recommended that multi-site rules are configured before basic rules.</span></span> <span data-ttu-id="c8e26-185">Çok siteli dinleyicileri ilk yapılandırarak, bu yapılandırma yönlendirilmiş toohello uygunsuz arka uç trafiğidir hello olasılığını azaltır.</span><span class="sxs-lookup"><span data-stu-id="c8e26-185">By configuring multi-site listeners first, this configuration reduces hello chance that traffic is routed toohello inappropriate backend.</span></span> <span data-ttu-id="c8e26-186">Merhaba temel kural değerlendirilen bağlantı noktası önceki toohello çok siteli kurala göre trafiği eşleşecek şekilde yönlendirme Bu sorun ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-186">This routing issue can occur as hello basic rule would match traffic based on port prior toohello multi-site rule being evaluated.</span></span>

<span data-ttu-id="c8e26-187">**Q. Hangi özel araştırmalara hello ana bilgisayar alanı belirtmek?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-187">**Q. What does hello Host field for custom probes signify?**</span></span>

<span data-ttu-id="c8e26-188">Ana bilgisayar alanı hello adı toosend hello araştırma için belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-188">Host field specifies hello name toosend hello probe to.</span></span> <span data-ttu-id="c8e26-189">Geçerli yalnızca çok siteli uygulama ağ geçidi üzerinde yapılandırılmış, aksi takdirde '127.0.0.1' kullanın.</span><span class="sxs-lookup"><span data-stu-id="c8e26-189">Applicable only when multi-site is configured on Application Gateway, otherwise use '127.0.0.1'.</span></span> <span data-ttu-id="c8e26-190">Bu değer VM ana bilgisayar adından farklı olduğundan ve biçimde \<Protokolü\>://\<konak\>:\<bağlantı noktası\>\<yolu\>.</span><span class="sxs-lookup"><span data-stu-id="c8e26-190">This value is different from VM host name and is in format \<protocol\>://\<host\>:\<port\>\<path\>.</span></span>

<span data-ttu-id="c8e26-191">**Q. Beyaz liste uygulama ağ geçidi erişim tooa yükleyebilir miyim az IP'leri kaynak?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-191">**Q. Can I whitelist Application Gateway access tooa few source IPs?**</span></span>

<span data-ttu-id="c8e26-192">Bu senaryo yapılabilir uygulama ağ geçidi alt ağda Nsg'leri kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c8e26-192">This scenario can be done using NSGs on Application Gateway subnet.</span></span> <span data-ttu-id="c8e26-193">Merhaba kısıtlamaları aşağıdaki listelenen hello öncelik sırasına göre hello alt ağdaki sokulmalıdır:</span><span class="sxs-lookup"><span data-stu-id="c8e26-193">hello following restrictions should be put on hello subnet in hello listed order of priority:</span></span>

* <span data-ttu-id="c8e26-194">IP/IP aralığı kaynağından gelen trafiğe izin verecek.</span><span class="sxs-lookup"><span data-stu-id="c8e26-194">Allow incoming traffic from source IP/IP range.</span></span>

* <span data-ttu-id="c8e26-195">Tüm kaynakları tooports 65503 65534 için gelen gelen istekleri izin [arka uç sağlık iletişimi](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="c8e26-195">Allow incoming requests from all sources tooports 65503-65534 for [backend health communication](application-gateway-diagnostics.md).</span></span>

* <span data-ttu-id="c8e26-196">Gelen Azure yük dengeleyici araştırmalar (AzureLoadBalancer etiketi) ve gelen sanal ağ trafiğini (VirtualNetwork etiketi) üzerinde hello izin [NSG](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="c8e26-196">Allow incoming Azure Load Balancer probes (AzureLoadBalancer tag) and inbound virtual network traffic (VirtualNetwork tag) on hello [NSG](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="c8e26-197">Bir reddetme ile diğer tüm gelen trafiği engelle tüm kuralı.</span><span class="sxs-lookup"><span data-stu-id="c8e26-197">Block all other incoming traffic with a Deny all rule.</span></span>

* <span data-ttu-id="c8e26-198">Giden trafik toohello izin Internet tüm hedefler için.</span><span class="sxs-lookup"><span data-stu-id="c8e26-198">Allow outbound traffic toohello internet for all destinations.</span></span>

## <a name="performance"></a><span data-ttu-id="c8e26-199">Performans</span><span class="sxs-lookup"><span data-stu-id="c8e26-199">Performance</span></span>

<span data-ttu-id="c8e26-200">**Q. Uygulama ağ geçidi, yüksek kullanılabilirlik ve ölçeklenebilirlik nasıl destekler?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-200">**Q. How does Application Gateway support high availability and scalability?**</span></span>

<span data-ttu-id="c8e26-201">Uygulama ağ geçidi dağıtılan iki veya daha çok örneği varsa, yüksek kullanılabilirlik senaryolarını destekler.</span><span class="sxs-lookup"><span data-stu-id="c8e26-201">Application Gateway supports high availability scenarios when you have two or more instances deployed.</span></span> <span data-ttu-id="c8e26-202">Azure tüm örneklerini hello dönme güncelleştirme ve hata etki alanları tooensure üzerinden bu örnekler dağıtır aynı anda.</span><span class="sxs-lookup"><span data-stu-id="c8e26-202">Azure distributes these instances across update and fault domains tooensure that all instances do not fail at hello same time.</span></span> <span data-ttu-id="c8e26-203">Uygulama ağ geçidi, birden çok örneğini hello ekleyerek ölçeklenebilirlik destekler aynı ağ geçidi tooshare hello yük.</span><span class="sxs-lookup"><span data-stu-id="c8e26-203">Application Gateway supports scalability by adding multiple instances of hello same gateway tooshare hello load.</span></span>

<span data-ttu-id="c8e26-204">**Q. Nasıl ı DR senaryosuna uygulama ağ geçidi ile veri merkezleri arasında elde etmek?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-204">**Q. How do I achieve DR scenario across data centers with Application Gateway?**</span></span>

<span data-ttu-id="c8e26-205">Müşteriler, farklı veri merkezlerinde bulunan birden çok uygulama ağ geçidi üzerinden trafik Yöneticisi toodistribute trafiği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8e26-205">Customers can use Traffic Manager toodistribute traffic across multiple Application Gateways in different datacenters.</span></span>

<span data-ttu-id="c8e26-206">**Q. Otomatik ölçeklendirme destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-206">**Q. Is auto scaling supported?**</span></span>

<span data-ttu-id="c8e26-207">Hayır, ancak uygulama ağ geçidi kullanılan tooalert olabilir bir işleme ölçümü, bir Eşiğe ulaşıldığında.</span><span class="sxs-lookup"><span data-stu-id="c8e26-207">No, but Application Gateway has a throughput metric that can be used tooalert you when a threshold is reached.</span></span> <span data-ttu-id="c8e26-208">El ile örnekleri ekleme veya boyutunu değiştirme hello ağ geçidini yeniden değil ve varolan trafiği etkilemez.</span><span class="sxs-lookup"><span data-stu-id="c8e26-208">Manually adding instances or changing size does not restart hello gateway and does not impact existing traffic.</span></span>

<span data-ttu-id="c8e26-209">**Q. El ile ölçek yukarı/aşağı neden kapalı kalma süresi mu?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-209">**Q. Does manual scale up/down cause downtime?**</span></span>

<span data-ttu-id="c8e26-210">Kapalı kalma süresi olmadan, örnekler yükseltme etki alanları ve hata etki alanları arasında dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="c8e26-210">There is no downtime, instances are distributed across upgrade domains and fault domains.</span></span>

<span data-ttu-id="c8e26-211">**Q. Orta toolarge kesintiye uğratmadan gelen örnek boyutu değiştirebilirim?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-211">**Q. Can I change instance size from medium toolarge without disruption?**</span></span>

<span data-ttu-id="c8e26-212">Evet, Azure örnekleri tüm örneklerini hello dönme güncelleştirme ve hata etki alanları tooensure dağıtır aynı anda.</span><span class="sxs-lookup"><span data-stu-id="c8e26-212">Yes, Azure distributes instances across update and fault domains tooensure that all instances do not fail at hello same time.</span></span> <span data-ttu-id="c8e26-213">Birden çok örneğini ekleyerek ölçeklendirme uygulama ağ geçidi destekler, aynı ağ geçidi tooshare hello yük hello.</span><span class="sxs-lookup"><span data-stu-id="c8e26-213">Application Gateway supports scaling by adding multiple instances of hello same gateway tooshare hello load.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="c8e26-214">SSL yapılandırması</span><span class="sxs-lookup"><span data-stu-id="c8e26-214">SSL Configuration</span></span>

<span data-ttu-id="c8e26-215">**Q. Hangi sertifikaların uygulama ağ geçidinde destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-215">**Q. What certificates are supported on Application Gateway?**</span></span>

<span data-ttu-id="c8e26-216">Otomatik olarak imzalanan sertifikaları, CA sertifikaları ve joker sertifikaları desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-216">Self signed certs, CA certs, and wild-card certs are supported.</span></span> <span data-ttu-id="c8e26-217">EV sertifikaları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="c8e26-217">EV certs are not supported.</span></span>

<span data-ttu-id="c8e26-218">**Q. Uygulama ağ geçidi tarafından desteklenen hello geçerli şifre paketleri nelerdir?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-218">**Q. What are hello current cipher suites supported by Application Gateway?**</span></span>

<span data-ttu-id="c8e26-219">Merhaba, uygulama ağ geçidi tarafından desteklenen hello geçerli şifre paketleri şunlardır.</span><span class="sxs-lookup"><span data-stu-id="c8e26-219">hello following are hello current cipher suites supported by application gateway.</span></span> <span data-ttu-id="c8e26-220">Ziyaret edin: [yapılandırma SSL İlkesi sürümleri ve şifre paketleri uygulama ağ geçidi üzerinde](application-gateway-configure-ssl-policy-powershell.md) toolearn nasıl toocustomize SSL seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="c8e26-220">Visit: [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) toolearn how toocustomize SSL options.</span></span>

- <span data-ttu-id="c8e26-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="c8e26-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="c8e26-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="c8e26-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="c8e26-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="c8e26-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="c8e26-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="c8e26-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="c8e26-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="c8e26-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="c8e26-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="c8e26-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="c8e26-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="c8e26-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="c8e26-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="c8e26-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="c8e26-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="c8e26-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="c8e26-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="c8e26-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="c8e26-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="c8e26-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="c8e26-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="c8e26-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="c8e26-233">TLS_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="c8e26-233">TLS_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="c8e26-234">TLS_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="c8e26-234">TLS_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="c8e26-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="c8e26-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="c8e26-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="c8e26-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="c8e26-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="c8e26-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="c8e26-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="c8e26-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="c8e26-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="c8e26-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="c8e26-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="c8e26-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="c8e26-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="c8e26-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="c8e26-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="c8e26-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="c8e26-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="c8e26-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="c8e26-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="c8e26-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="c8e26-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="c8e26-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span></span>
- <span data-ttu-id="c8e26-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="c8e26-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span></span>

<span data-ttu-id="c8e26-247">**Q. Uygulama ağ geçidi de trafiği toohello arka uç yeniden şifrelenmesini destekliyor mu?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-247">**Q. Does Application Gateway also support re-encryption of traffic toohello backend?**</span></span>

<span data-ttu-id="c8e26-248">Evet, uygulama ağ geçidi destekler SSL boşaltma ve son tooend hello trafiği toohello arka uç yeniden şifreler SSL.</span><span class="sxs-lookup"><span data-stu-id="c8e26-248">Yes, Application Gateway supports SSL offload, and end tooend SSL, which re-encrypts hello traffic toohello backend.</span></span>

<span data-ttu-id="c8e26-249">**Q. SSL ilke toocontrol SSL protokol sürümleri yapılandırabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-249">**Q. Can I configure SSL policy toocontrol SSL Protocol versions?**</span></span>

<span data-ttu-id="c8e26-250">Evet, uygulama ağ geçidi toodeny yapılandırabilirsiniz TLS1.0, TLS1.1 ve TLS1.2.</span><span class="sxs-lookup"><span data-stu-id="c8e26-250">Yes, you can configure Application Gateway toodeny TLS1.0, TLS1.1, and TLS1.2.</span></span> <span data-ttu-id="c8e26-251">SSL 2.0 ve 3.0 zaten varsayılan olarak devre dışıdır ve yapılandırılabilir değildir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-251">SSL 2.0 and 3.0 are already disabled by default and are not configurable.</span></span>

<span data-ttu-id="c8e26-252">**Q. Şifre paketleri ve ilke sırasını yapılandırabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-252">**Q. Can I configure cipher suites and policy order?**</span></span>

<span data-ttu-id="c8e26-253">Evet, [şifre paketleri yapılandırmasını](application-gateway-ssl-policy-overview.md) desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-253">Yes, [configuration of cipher suites](application-gateway-ssl-policy-overview.md) is supported.</span></span> <span data-ttu-id="c8e26-254">Özel bir ilke tanımlandığında, şifre paketleri aşağıdaki hello en az birinin etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-254">When defining a custom policy, at least one of hello following cipher suites must be enabled.</span></span> <span data-ttu-id="c8e26-255">Uygulama ağ geçidi SHA256 toofor arka uç yönetim kullanır.</span><span class="sxs-lookup"><span data-stu-id="c8e26-255">Application gateway uses SHA256 toofor backend management.</span></span>

* <span data-ttu-id="c8e26-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="c8e26-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span></span> 
* <span data-ttu-id="c8e26-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="c8e26-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
* <span data-ttu-id="c8e26-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="c8e26-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="c8e26-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="c8e26-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="c8e26-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="c8e26-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
* <span data-ttu-id="c8e26-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="c8e26-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>

<span data-ttu-id="c8e26-262">**Q. Kaç tane SSL sertifikalarını destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-262">**Q. How many SSL certificates are supported?**</span></span>

<span data-ttu-id="c8e26-263">Too20 SSL sertifikaları desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-263">Up too20 SSL certificates are supported.</span></span>

<span data-ttu-id="c8e26-264">**Q. Arka uç yeniden şifreleme için kaç tane kimlik doğrulama sertifikaları destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-264">**Q. How many authentication certificates for backend re-encryption are supported?**</span></span>

<span data-ttu-id="c8e26-265">Too10 5 bir varsayılan kimlik doğrulama sertifikaları desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-265">Up too10 authentication certificates are supported with a default of 5.</span></span>

<span data-ttu-id="c8e26-266">**Q. Uygulama ağ geçidi, Azure anahtar kasası ile yerel olarak tümleşik çalışıyor mu?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-266">**Q. Does Application Gateway integrate with Azure Key Vault natively?**</span></span>

<span data-ttu-id="c8e26-267">Hayır, bunu Azure anahtar kasası ile tümleşiktir değil.</span><span class="sxs-lookup"><span data-stu-id="c8e26-267">No, it is not integrated with Azure Key Vault.</span></span>

## <a name="web-application-firewall-waf-configuration"></a><span data-ttu-id="c8e26-268">Web uygulaması Güvenlik Duvarı (WAF) yapılandırması</span><span class="sxs-lookup"><span data-stu-id="c8e26-268">Web Application Firewall (WAF) Configuration</span></span>

<span data-ttu-id="c8e26-269">**Q. Merhaba WAF SKU standart SKU hello ile kullanılabilen tüm hello özellikleri sunar?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-269">**Q. Does hello WAF SKU offer all hello features available with hello Standard SKU?**</span></span>

<span data-ttu-id="c8e26-270">Evet, WAF hello standart SKU tüm hello özelliklerini destekler.</span><span class="sxs-lookup"><span data-stu-id="c8e26-270">Yes, WAF supports all hello features in hello Standard SKU.</span></span>

<span data-ttu-id="c8e26-271">**Q. Uygulama ağ geçidi destekleyen hello CRS sürümü nedir?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-271">**Q. What is hello CRS version Application Gateway supports?**</span></span>

<span data-ttu-id="c8e26-272">Uygulama ağ geçidi destekleyen CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) ve CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span><span class="sxs-lookup"><span data-stu-id="c8e26-272">Application Gateway supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span></span>

<span data-ttu-id="c8e26-273">**Q. WAF nasıl izlerim?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-273">**Q. How do I monitor WAF?**</span></span>

<span data-ttu-id="c8e26-274">WAF tanılama günlük aracılığıyla izlenen, tanılama günlüğe kaydetme hakkında daha fazla bilgi bulunabilir [tanılama günlüğe kaydetme ve uygulama ağ geçidi ölçümleri](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="c8e26-274">WAF is monitored through diagnostic logging, more information on diagnostic logging can be found at [Diagnostics Logging and Metrics for Application Gateway](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="c8e26-275">**Q. Algılama modunu akışa mu?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-275">**Q. Does detection mode block traffic?**</span></span>

<span data-ttu-id="c8e26-276">Hayır, algılama modunu yalnızca WAF kuralını tetikleyen trafiği günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="c8e26-276">No, detection mode only logs traffic, which triggered a WAF rule.</span></span>

<span data-ttu-id="c8e26-277">**Q. WAF kuralları nasıl özelleştirebilirim?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-277">**Q. How do I customize WAF rules?**</span></span>

<span data-ttu-id="c8e26-278">Evet, WAF kuralları nasıl toocustomize ziyaret hakkında daha fazla bilgi için özelleştirilebilir [özelleştirme WAF kural gruplar ve kurallar](application-gateway-customize-waf-rules-portal.md)</span><span class="sxs-lookup"><span data-stu-id="c8e26-278">Yes, WAF rules are customizable, for more information on how toocustomize them visit [Customize WAF rule groups and rules](application-gateway-customize-waf-rules-portal.md)</span></span>

<span data-ttu-id="c8e26-279">**Q. Hangi kuralları şu anda kullanılabilir?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-279">**Q. What rules are currently available?**</span></span>

<span data-ttu-id="c8e26-280">WAF şu anda CRS destekler [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) ve [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), ilk 10 güvenlik açıkları hello açık Web uygulaması güvenlik proje (burada bulunan OWASP) tarafından tanımlanan hello çoğunu karşı temel güvenlik sağlayın [OWASP ilk 10 güvenlik açıkları](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span><span class="sxs-lookup"><span data-stu-id="c8e26-280">WAF currently supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), which provide baseline security against most of hello top 10 vulnerabilities identified by hello Open Web Application Security Project (OWASP) found here [OWASP top 10 Vulnerabilities](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span></span>

* <span data-ttu-id="c8e26-281">SQL ekleme koruması</span><span class="sxs-lookup"><span data-stu-id="c8e26-281">SQL injection protection</span></span>

* <span data-ttu-id="c8e26-282">Siteler arası komut dosyası koruması</span><span class="sxs-lookup"><span data-stu-id="c8e26-282">Cross site scripting protection</span></span>

* <span data-ttu-id="c8e26-283">Komut ekleme, HTTP isteği kaçakçılığı, HTTP yanıtı bölme ve uzak dosya ekleme saldırıcı gibi Yaygın Web Saldırıları Koruması</span><span class="sxs-lookup"><span data-stu-id="c8e26-283">Common Web Attacks Protection such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion attack</span></span>

* <span data-ttu-id="c8e26-284">HTTP protokolü ihlallerine karşı koruma</span><span class="sxs-lookup"><span data-stu-id="c8e26-284">Protection against HTTP protocol violations</span></span>

* <span data-ttu-id="c8e26-285">Eksik konak kullanıcısı-aracısı ve kabul üst bilgileri gibi HTTP protokolü anormalliklerine karşı koruma</span><span class="sxs-lookup"><span data-stu-id="c8e26-285">Protection against HTTP protocol anomalies such as missing host user-agent and accept headers</span></span>

* <span data-ttu-id="c8e26-286">Robotlar, gezginler ve tarayıcıları önleme</span><span class="sxs-lookup"><span data-stu-id="c8e26-286">Prevention against bots, crawlers, and scanners</span></span>

* <span data-ttu-id="c8e26-287">Ortak uygulama yapılandırma hataları (diğer bir deyişle, Apache, IIS, vb.) algılanması</span><span class="sxs-lookup"><span data-stu-id="c8e26-287">Detection of common application misconfigurations (that is, Apache, IIS, etc.)</span></span>

<span data-ttu-id="c8e26-288">**Q. WAF de DDoS önleme destekliyor mu?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-288">**Q. Does WAF also support DDoS prevention?**</span></span>

<span data-ttu-id="c8e26-289">Hayır, WAF DDoS önleme sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="c8e26-289">No, WAF does not provide DDoS prevention.</span></span>

## <a name="diagnostics-and-logging"></a><span data-ttu-id="c8e26-290">Tanılama ve günlüğe kaydetme</span><span class="sxs-lookup"><span data-stu-id="c8e26-290">Diagnostics and Logging</span></span>

<span data-ttu-id="c8e26-291">**Q. Ne tür günlükleri ile uygulama ağ geçidi var mı?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-291">**Q. What types of logs are available with Application Gateway?**</span></span>

<span data-ttu-id="c8e26-292">Uygulama ağ geçidi için üç günlükleri vardır.</span><span class="sxs-lookup"><span data-stu-id="c8e26-292">There are three logs available for Application Gateway.</span></span> <span data-ttu-id="c8e26-293">Bu günlükler ve diğer tanılama yetenekleri hakkında daha fazla bilgi için ziyaret [arka uç sistem durumu, tanılama günlüklerini ve uygulama ağ geçidi ölçümleri](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="c8e26-293">For more information on these logs and other diagnostic capabilities, visit [Backend health, diagnostics logs, and metrics for Application Gateway](application-gateway-diagnostics.md).</span></span>

- <span data-ttu-id="c8e26-294">**ApplicationGatewayAccessLog** -hello erişim günlüğü içerir gönderilen her isteği toohello uygulama ağ geçidi ön uç.</span><span class="sxs-lookup"><span data-stu-id="c8e26-294">**ApplicationGatewayAccessLog** - hello access log contains each request submitted toohello Application Gateway frontend.</span></span> <span data-ttu-id="c8e26-295">Dönüş kodu, bayt ve kapatma, hello arayanın IP, istenen URL yanıt gecikme Hello veri içerir. Erişim günlüğüne 300 saniyede toplanır.</span><span class="sxs-lookup"><span data-stu-id="c8e26-295">hello data includes hello caller's IP, URL requested, response latency, return code, bytes in and out. Access log is collected every 300 seconds.</span></span> <span data-ttu-id="c8e26-296">Bu günlük, uygulama ağ geçidi örneği başına bir kayıt içerir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-296">This log contains one record per instance of Application Gateway.</span></span>
- <span data-ttu-id="c8e26-297">**ApplicationGatewayPerformanceLog** -hello performans günlüğü sunulan, toplam istek dahil olmak üzere her örneği bazında üretilen iş bayt performans bilgilerini yakalar, toplam istek sayısı sunulan, sağlıklı ve sağlıksız başarısız istek sayısı arka uç örnek sayısı.</span><span class="sxs-lookup"><span data-stu-id="c8e26-297">**ApplicationGatewayPerformanceLog** - hello performance log captures performance information on per instance basis including total request served, throughput in bytes, total requests served, failed request count, healthy and unhealthy back-end instance count.</span></span>
- <span data-ttu-id="c8e26-298">**ApplicationGatewayFirewallLog** -hello güvenlik duvarı günlüğü, web uygulaması güvenlik duvarı ile yapılandırılmış bir uygulama Ağ Geçidi algılama veya önleme modu üzerinden oturum isteklerini içerir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-298">**ApplicationGatewayFirewallLog** - hello firewall log contains requests that are logged through either detection or prevention mode of an application gateway that is configured with web application firewall.</span></span>

<span data-ttu-id="c8e26-299">**Q. My arka uç havuzu üyeleri sağlıklı olup olmadığını nasıl anlayabilirim?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-299">**Q. How do I know if my backend pool members are healthy?**</span></span>

<span data-ttu-id="c8e26-300">Merhaba PowerShell cmdlet'ini kullanabilirsiniz `Get-AzureRmApplicationGatewayBackendHealth` veya sistem durumu hello Portalı aracılığıyla ziyaret ederek doğrulamak [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="c8e26-300">You can use hello PowerShell cmdlet `Get-AzureRmApplicationGatewayBackendHealth` or verify health through hello portal by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="c8e26-301">**Q. Merhaba bekletme ilkesi hello tanılama günlükleri'nedir?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-301">**Q. What is hello retention policy on hello diagnostics logs?**</span></span>

<span data-ttu-id="c8e26-302">Akış toohello müşteri depolama hesabına tanılama günlükleri ve müşterilerin kendi tercihine göre hello bekletme ilkesi ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8e26-302">Diagnostic logs flow toohello customers storage account and customers can set hello retention policy based on their preference.</span></span> <span data-ttu-id="c8e26-303">Tanılama günlüklerini de tooan olay hub'ı veya günlük analizi gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-303">Diagnostic logs can also be sent tooan Event Hub or Log Analytics.</span></span> <span data-ttu-id="c8e26-304">Ziyaret [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="c8e26-304">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) for more details.</span></span>

<span data-ttu-id="c8e26-305">**Q. Uygulama ağ geçidi için denetim günlüklerini nasıl sağlarım?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-305">**Q. How do I get audit logs for Application Gateway?**</span></span>

<span data-ttu-id="c8e26-306">Denetim günlükleri, uygulama ağ geçidi için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c8e26-306">Audit logs are available for Application Gateway.</span></span> <span data-ttu-id="c8e26-307">Merhaba Portalı'nda tıklatın **etkinlik günlüğü** hello menü dikey bir uygulama ağ geçidi tooaccess hello denetim günlüğü.</span><span class="sxs-lookup"><span data-stu-id="c8e26-307">In hello portal, click **Activity Log** in hello menu blade of an Application Gateway tooaccess hello audit log.</span></span> 

<span data-ttu-id="c8e26-308">**Q. Uygulama ağ geçidi uyarılarla ayarlayabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-308">**Q. Can I set alerts with Application Gateway?**</span></span>

<span data-ttu-id="c8e26-309">Evet, uygulama ağ geçidi uyarıları destek, uyarılar ölçümleri yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="c8e26-309">Yes, Application Gateway does support alerts, alerts are configured off metrics.</span></span>  <span data-ttu-id="c8e26-310">Uygulama ağ geçidi şu anda yapılandırılmış tooalert olabilir "işleme" ölçüsü yok.</span><span class="sxs-lookup"><span data-stu-id="c8e26-310">Application Gateway currently has a metric of "throughput", which can be configured tooalert.</span></span> <span data-ttu-id="c8e26-311">Uyarıları hakkında daha fazla toolearn ziyaret [uyarı bildirimleri alma](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="c8e26-311">toolearn more about alerts, visit [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="c8e26-312">**Q. Arka uç sistem durumu bilinmeyen durum, bu durum neden olabilecek verir?**</span><span class="sxs-lookup"><span data-stu-id="c8e26-312">**Q. Backend health returns unknown status, what could be causing this status?**</span></span>

<span data-ttu-id="c8e26-313">Merhaba en yaygın nedeni, bir NSG veya özel DNS tarafından erişim toohello arka uç engelleniyor olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="c8e26-313">hello most common reason is access toohello backend is being blocked by an NSG or custom DNS.</span></span> <span data-ttu-id="c8e26-314">Ziyaret [arka uç sistem durumu, tanılama günlüğe kaydetme ve uygulama ağ geçidi ölçümleri](application-gateway-diagnostics.md) toolearn daha fazla.</span><span class="sxs-lookup"><span data-stu-id="c8e26-314">Visit [Backend health, diagnostics logging, and metrics for Application Gateway](application-gateway-diagnostics.md) toolearn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8e26-315">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="c8e26-315">Next Steps</span></span>

<span data-ttu-id="c8e26-316">Uygulama ağ geçidi hakkında daha fazla ziyaret toolearn [giriş tooApplication ağ geçidi](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c8e26-316">toolearn more about Application Gateway visit [Introduction tooApplication Gateway](application-gateway-introduction.md).</span></span>
