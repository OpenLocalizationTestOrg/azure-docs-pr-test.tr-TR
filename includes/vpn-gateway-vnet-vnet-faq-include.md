<span data-ttu-id="9894a-101">Merhaba VNet-VNet SSS tooVPN ağ geçidi bağlantılara uygulanır.</span><span class="sxs-lookup"><span data-stu-id="9894a-101">hello VNet-to-VNet FAQ applies tooVPN Gateway connections.</span></span> <span data-ttu-id="9894a-102">Sanal Ağ Eşleme konusunu arıyorsanız bkz. [Sanal Ağ Eşleme](../articles/virtual-network/virtual-network-peering-overview.md)</span><span class="sxs-lookup"><span data-stu-id="9894a-102">If you are looking for VNet Peering, see [Virtual Network Peering](../articles/virtual-network/virtual-network-peering-overview.md)</span></span>

### <a name="does-azure-charge-for-traffic-between-vnets"></a><span data-ttu-id="9894a-103">Azure sanal ağlar arasındaki trafik için ücretli midir?</span><span class="sxs-lookup"><span data-stu-id="9894a-103">Does Azure charge for traffic between VNets?</span></span>

<span data-ttu-id="9894a-104">VNet-VNet trafiği hello içinde aynı bölge olduğunda her iki yön için boş bir VPN ağ geçidi bağlantısı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="9894a-104">VNet-to-VNet traffic within hello same region is free for both directions when using a VPN gateway connection.</span></span> <span data-ttu-id="9894a-105">Bölge sanal ağdan sanal ağa çıkış trafiği hello giden arası VNet veri aktarım hızı hello kaynak bölgelerine bağlı ücretlendirilir.</span><span class="sxs-lookup"><span data-stu-id="9894a-105">Cross region VNet-to-VNet egress traffic is charged with hello outbound inter-VNet data transfer rates based on hello source regions.</span></span> <span data-ttu-id="9894a-106">Toohello başvuran [VPN ağ geçidi fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/vpn-gateway/) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="9894a-106">Refer toohello [VPN Gateway pricing page](https://azure.microsoft.com/pricing/details/vpn-gateway/) for details.</span></span> <span data-ttu-id="9894a-107">VNet eşlemesi, VPN ağ geçidi yerine, sanal ağlar bağlanıyorsanız hello bkz [sanal ağ fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="9894a-107">If you are connecting your VNets using VNet Peering, rather than VPN Gateway, see hello [Virtual Network pricing page](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>

### <a name="does-vnet-to-vnet-traffic-travel-across-hello-internet"></a><span data-ttu-id="9894a-108">VNet-VNet trafiği hello Internet yolculuk ediyor mu?</span><span class="sxs-lookup"><span data-stu-id="9894a-108">Does VNet-to-VNet traffic travel across hello Internet?</span></span>

<span data-ttu-id="9894a-109">Hayır.</span><span class="sxs-lookup"><span data-stu-id="9894a-109">No.</span></span> <span data-ttu-id="9894a-110">VNet-VNet trafiği hello Microsoft Azure omurga, hello Internet geçen.</span><span class="sxs-lookup"><span data-stu-id="9894a-110">VNet-to-VNet traffic travels across hello Microsoft Azure backbone, not hello Internet.</span></span>

### <a name="is-vnet-to-vnet-traffic-secure"></a><span data-ttu-id="9894a-111">Sanal Ağdan Sanal Ağa trafiği güvenli mi?</span><span class="sxs-lookup"><span data-stu-id="9894a-111">Is VNet-to-VNet traffic secure?</span></span>

<span data-ttu-id="9894a-112">Evet, IPsec/IKE şifrelemesiyle korunur.</span><span class="sxs-lookup"><span data-stu-id="9894a-112">Yes, it is protected by IPsec/IKE encryption.</span></span>

### <a name="do-i-need-a-vpn-device-tooconnect-vnets-together"></a><span data-ttu-id="9894a-113">Bir VPN cihazı tooconnect sanal ağlar birlikte gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="9894a-113">Do I need a VPN device tooconnect VNets together?</span></span>

<span data-ttu-id="9894a-114">Hayır.</span><span class="sxs-lookup"><span data-stu-id="9894a-114">No.</span></span> <span data-ttu-id="9894a-115">İşletmeler arası bağlantı gerekmediği sürece birden fazla Azure sanal ağını birleştirmek için VPN cihazına gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="9894a-115">Connecting multiple Azure virtual networks together doesn't require a VPN device unless cross-premises connectivity is required.</span></span>

### <a name="do-my-vnets-need-toobe-in-hello-same-region"></a><span data-ttu-id="9894a-116">My sanal ağlar hello toobe gerek aynı bölgede?</span><span class="sxs-lookup"><span data-stu-id="9894a-116">Do my VNets need toobe in hello same region?</span></span>

<span data-ttu-id="9894a-117">Hayır.</span><span class="sxs-lookup"><span data-stu-id="9894a-117">No.</span></span> <span data-ttu-id="9894a-118">Merhaba sanal ağlar hello olabilir aynı veya farklı Azure bölgeleri (konumlara).</span><span class="sxs-lookup"><span data-stu-id="9894a-118">hello virtual networks can be in hello same or different Azure regions (locations).</span></span>

### <a name="if-hello-vnets-are-not-in-hello-same-subscription-do-hello-subscriptions-need-toobe-associated-with-hello-same-ad-tenant"></a><span data-ttu-id="9894a-119">Merhaba sanal ağlar içinde değilse aynı hello hello abonelikleri aboneliğiniz hello aynı AD Kiracı ile ilişkilendirilen toobe?</span><span class="sxs-lookup"><span data-stu-id="9894a-119">If hello VNets are not in hello same subscription, do hello subscriptions need toobe associated with hello same AD tenant?</span></span>

<span data-ttu-id="9894a-120">Hayır.</span><span class="sxs-lookup"><span data-stu-id="9894a-120">No.</span></span>

### <a name="can-i-use-vnet-to-vnet-along-with-multi-site-connections"></a><span data-ttu-id="9894a-121">Sanal Ağdan Sanal Ağa bağlantıyı çoklu site bağlantılarıyla birlikte kullanabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="9894a-121">Can I use VNet-to-VNet along with multi-site connections?</span></span>

<span data-ttu-id="9894a-122">Evet.</span><span class="sxs-lookup"><span data-stu-id="9894a-122">Yes.</span></span> <span data-ttu-id="9894a-123">Sanal ağ bağlantısı, çoklu site VPN’leri ile eşzamanlı olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9894a-123">Virtual network connectivity can be used simultaneously with multi-site VPNs.</span></span>

### <a name="how-many-on-premises-sites-and-virtual-networks-can-one-virtual-network-connect-to"></a><span data-ttu-id="9894a-124">Bir sanal ağ kaç şirket içi siteye ve sanal ağa bağlanabilir?</span><span class="sxs-lookup"><span data-stu-id="9894a-124">How many on-premises sites and virtual networks can one virtual network connect to?</span></span>

<span data-ttu-id="9894a-125">[Ağ geçidi gereksinimleri](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements) tablosuna bakın.</span><span class="sxs-lookup"><span data-stu-id="9894a-125">See [Gateway requirements](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements) table.</span></span>

### <a name="can-i-use-vnet-to-vnet-tooconnect-vms-or-cloud-services-outside-of-a-vnet"></a><span data-ttu-id="9894a-126">I VNet-VNet tooconnect VM'ler kullanabilir veya Bulut hizmetlerini bir sanal ağ dışında?</span><span class="sxs-lookup"><span data-stu-id="9894a-126">Can I use VNet-to-VNet tooconnect VMs or cloud services outside of a VNet?</span></span>

<span data-ttu-id="9894a-127">Hayır.</span><span class="sxs-lookup"><span data-stu-id="9894a-127">No.</span></span> <span data-ttu-id="9894a-128">Sanal Ağdan Sanal Ağa, sanal ağları bağlamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="9894a-128">VNet-to-VNet supports connecting virtual networks.</span></span> <span data-ttu-id="9894a-129">Bir sanal ağ içinde olmayan sanal makineleri veya bulut hizmetlerini bağlamayı desteklemez.</span><span class="sxs-lookup"><span data-stu-id="9894a-129">It does not support connecting virtual machines or cloud services that are not in a virtual network.</span></span>

### <a name="can-a-cloud-service-or-a-load-balancing-endpoint-span-vnets"></a><span data-ttu-id="9894a-130">Bir bulut hizmeti ya da bir yük dengeleme uç noktası sanal ağlara yayılabilir mi?</span><span class="sxs-lookup"><span data-stu-id="9894a-130">Can a cloud service or a load balancing endpoint span VNets?</span></span>

<span data-ttu-id="9894a-131">Hayır.</span><span class="sxs-lookup"><span data-stu-id="9894a-131">No.</span></span> <span data-ttu-id="9894a-132">Bir bulut hizmeti ya da yük dengeleme uç noktası, birbirlerine bağlı olsa da sanal ağlara yayılamaz.</span><span class="sxs-lookup"><span data-stu-id="9894a-132">A cloud service or a load balancing endpoint can't span across virtual networks, even if they are connected together.</span></span>

### <a name="can-i-used-a-policybased-vpn-type-for-vnet-to-vnet-or-multi-site-connections"></a><span data-ttu-id="9894a-133">Sanal Ağdan Sanal Ağa veya Çoklu Site bağlantıları için PolicyBased VPN türü kullanabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="9894a-133">Can I used a PolicyBased VPN type for VNet-to-VNet or Multi-Site connections?</span></span>

<span data-ttu-id="9894a-134">Hayır.</span><span class="sxs-lookup"><span data-stu-id="9894a-134">No.</span></span> <span data-ttu-id="9894a-135">Sanal Ağdan Sanal Ağa ve Çoklu Site bağlantıları, Azure VPN ağ geçitlerinin, önceki adı Dinamik Yönlendirme olan RouteBased VPN türleri ile bağlantılarını VPN geçidi ile bağlamalarını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="9894a-135">VNet-to-VNet and Multi-Site connections require Azure VPN gateways with RouteBased (previously called Dynamic Routing) VPN types.</span></span>

### <a name="can-i-connect-a-vnet-with-a-routebased-vpn-type-tooanother-vnet-with-a-policybased-vpn-type"></a><span data-ttu-id="9894a-136">PolicyBased VPN türüne bir RouteBased VPN türü tooanother VNet t bir VNet bağlanabiliyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="9894a-136">Can I connect a VNet with a RouteBased VPN Type tooanother VNet with a PolicyBased VPN type?</span></span>

<span data-ttu-id="9894a-137">Hayır, her iki sanal ağın da rota tabanlı (önceki adıyla Dinamik Yönlendirme) VPN kullanıyor olması GEREKİR.</span><span class="sxs-lookup"><span data-stu-id="9894a-137">No, both virtual networks MUST be using route-based (previously called Dynamic Routing) VPNs.</span></span>

### <a name="do-vpn-tunnels-share-bandwidth"></a><span data-ttu-id="9894a-138">VPN tünelleri bant genişliğini paylaşır mı?</span><span class="sxs-lookup"><span data-stu-id="9894a-138">Do VPN tunnels share bandwidth?</span></span>

<span data-ttu-id="9894a-139">Evet.</span><span class="sxs-lookup"><span data-stu-id="9894a-139">Yes.</span></span> <span data-ttu-id="9894a-140">Merhaba sanal ağ tüm VPN tünelleri hello hello Azure VPN ağ geçidi üzerinde kullanılabilir bant genişliğini paylaşır ve aynı VPN ağ geçidi çalışma süresi SLA azure'da hello.</span><span class="sxs-lookup"><span data-stu-id="9894a-140">All VPN tunnels of hello virtual network share hello available bandwidth on hello Azure VPN gateway and hello same VPN gateway uptime SLA in Azure.</span></span>

### <a name="are-redundant-tunnels-supported"></a><span data-ttu-id="9894a-141">Yedekli tüneller destekleniyor mu?</span><span class="sxs-lookup"><span data-stu-id="9894a-141">Are redundant tunnels supported?</span></span>

<span data-ttu-id="9894a-142">Bir sanal ağ çifti arasındaki yedekli tüneller, sanal ağ geçitlerinden biri etkin-etkin olarak yapılandırıldığında desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9894a-142">Redundant tunnels between a pair of virtual networks are supported when one virtual network gateway is configured as active-active.</span></span>

### <a name="can-i-have-overlapping-address-spaces-for-vnet-to-vnet-configurations"></a><span data-ttu-id="9894a-143">Sanal Ağdan Sanal Ağa yapılandırmalar için çakışan adres alanları kullanabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="9894a-143">Can I have overlapping address spaces for VNet-to-VNet configurations?</span></span>

<span data-ttu-id="9894a-144">Hayır.</span><span class="sxs-lookup"><span data-stu-id="9894a-144">No.</span></span> <span data-ttu-id="9894a-145">Çakışan IP adresi aralıklarını kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="9894a-145">You can't have overlapping IP address ranges.</span></span>

### <a name="can-there-be-overlapping-address-spaces-among-connected-virtual-networks-and-on-premises-local-sites"></a><span data-ttu-id="9894a-146">Bağlı sanal ağlar ve şirket içi yerel siteleri arasında çakışan adres alanları olabilir mi?</span><span class="sxs-lookup"><span data-stu-id="9894a-146">Can there be overlapping address spaces among connected virtual networks and on-premises local sites?</span></span>

<span data-ttu-id="9894a-147">Hayır.</span><span class="sxs-lookup"><span data-stu-id="9894a-147">No.</span></span> <span data-ttu-id="9894a-148">Çakışan IP adresi aralıklarını kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="9894a-148">You can't have overlapping IP address ranges.</span></span>



