<span data-ttu-id="8e294-101">Bir sanal ağ geçidi oluşturduğunuzda, kullanmak istediğiniz ağ geçidi SKU’sunu belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8e294-101">When you create a virtual network gateway, you need to specify the gateway SKU that you want to use.</span></span> <span data-ttu-id="8e294-102">İş yükü, aktarım hızı, özellik ve SLA türlerine bağlı olarak gereksinimlerinize uyan SKU'ları seçin.</span><span class="sxs-lookup"><span data-stu-id="8e294-102">Select the SKUs that satisfy your requirements based on the types of workloads, throughputs, features, and SLAs.</span></span>

[!INCLUDE [classic SKU](./vpn-gateway-classic-sku-support-include.md)]

[!INCLUDE [Aggregated throughput by SKU](./vpn-gateway-table-gwtype-aggtput-include.md)]

###  <span data-ttu-id="8e294-103"><a name="workloads"></a>Üretim *ve* Geliştirme-Test İş Yükleri Karşılaştırması</span><span class="sxs-lookup"><span data-stu-id="8e294-103"><a name="workloads"></a>Production *vs.* Dev-Test Workloads</span></span>

<span data-ttu-id="8e294-104">SLA'lardaki ve özellik kümelerindeki farklılıklar nedeniyle üretim ve geliştirme-test iş yükleri için aşağıdaki *farklı*  SKU'ları öneririz:</span><span class="sxs-lookup"><span data-stu-id="8e294-104">Due to the differences in SLAs and feature sets, we recommend the following SKUs for production *vs.* dev-test:</span></span>

| <span data-ttu-id="8e294-105">**İş yükü**</span><span class="sxs-lookup"><span data-stu-id="8e294-105">**Workload**</span></span>                       | <span data-ttu-id="8e294-106">**SKU'lar**</span><span class="sxs-lookup"><span data-stu-id="8e294-106">**SKUs**</span></span>               |
| ---                                | ---                    |
| <span data-ttu-id="8e294-107">**Üretim, kritik iş yükleri**</span><span class="sxs-lookup"><span data-stu-id="8e294-107">**Production, critical workloads**</span></span> | <span data-ttu-id="8e294-108">VpnGw1, VpnGw2, VpnGw3</span><span class="sxs-lookup"><span data-stu-id="8e294-108">VpnGw1, VpnGw2, VpnGw3</span></span> |
| <span data-ttu-id="8e294-109">**Geliştirme-test veya kavram kanıtı**</span><span class="sxs-lookup"><span data-stu-id="8e294-109">**Dev-test or proof of concept**</span></span>   | <span data-ttu-id="8e294-110">Temel</span><span class="sxs-lookup"><span data-stu-id="8e294-110">Basic</span></span>                  |
|                                    |                        |

<span data-ttu-id="8e294-111">Eski SKU'ları kullanıyorsanız üretim için Standart ve Yüksek Performanslı SKU'lar önerilir.</span><span class="sxs-lookup"><span data-stu-id="8e294-111">If you are using the old SKUs, the production SKU recommendations are Standard and HighPerformance SKUs.</span></span> <span data-ttu-id="8e294-112">Eski SKU'lar hakkında bilgi için bkz. [Ağ geçidi SKU'ları (eski SKU’lar)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="8e294-112">For information on the old SKUs, see [Gateway SKUs (legacy SKUs)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md).</span></span>

###  <span data-ttu-id="8e294-113"><a name="feature"></a>Ağ geçidi SKU'su özellik kümeleri</span><span class="sxs-lookup"><span data-stu-id="8e294-113"><a name="feature"></a>Gateway SKU feature sets</span></span>

<span data-ttu-id="8e294-114">Yeni ağ geçidi SKU'ları, ağ geçitlerinde sunulan özellik kümeleri açısından kolaylık sağlar:</span><span class="sxs-lookup"><span data-stu-id="8e294-114">The new gateway SKUs streamline the feature sets offered on the gateways:</span></span>

| <span data-ttu-id="8e294-115">**SKU**</span><span class="sxs-lookup"><span data-stu-id="8e294-115">**SKU**</span></span>| <span data-ttu-id="8e294-116">**Özellikler**</span><span class="sxs-lookup"><span data-stu-id="8e294-116">**Features**</span></span>|
| ---    | ---         |
|<span data-ttu-id="8e294-117">**Temel**</span><span class="sxs-lookup"><span data-stu-id="8e294-117">**Basic**</span></span>   | <span data-ttu-id="8e294-118">**Rota tabanlı VPN**: P2S ile 10 tünel</span><span class="sxs-lookup"><span data-stu-id="8e294-118">**Route-based VPN**: 10 tunnels with P2S</span></span><br><br><span data-ttu-id="8e294-119">**İlke tabanlı VPN** (IKEv1): 1 tünel; P2S yok</span><span class="sxs-lookup"><span data-stu-id="8e294-119">**Policy-based VPN**: (IKEv1): 1 tunnel; no P2S</span></span>|
| <span data-ttu-id="8e294-120">**VpnGw1, VpnGw2 ve VpnGw3**</span><span class="sxs-lookup"><span data-stu-id="8e294-120">**VpnGw1, VpnGw2, and VpnGw3**</span></span> | <span data-ttu-id="8e294-121">**Rol tabanlı VPN**: 30 tünele kadar (*), P2S, BGP, etkin-etkin, özel IPsec/IKE ilkesi, ExpressRoute/VPN birlikte kullanımı</span><span class="sxs-lookup"><span data-stu-id="8e294-121">**Route-based VPN**: up to 30 tunnels (*), P2S, BGP, active-active, custom IPsec/IKE policy, ExpressRoute/VPN co-existence</span></span> |
|        |             |

<span data-ttu-id="8e294-122">(*) Rota tabanlı bir VPN ağ geçidini (VpnGw1, VpnGw2, VpnGw3) şirket içi ilke tabanlı birden fazla güvenlik duvarı cihazına bağlamak için "PolicyBasedTrafficSelectors" yapılandırması gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e294-122">(*) You can configure "PolicyBasedTrafficSelectors" to connect a route-based VPN gateway (VpnGw1, VpnGw2, VpnGw3) to multiple on-premises policy-based firewall devices.</span></span> <span data-ttu-id="8e294-123">Ayrıntılı bilgi için bkz. [PowerShell kullanarak VPN ağ geçitlerini şirket içi ilke tabanlı birden fazla VPN cihazına bağlama](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="8e294-123">Refer to [Connect VPN gateways to multiple on-premises policy-based VPN devices using PowerShell](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) for details.</span></span>

###  <span data-ttu-id="8e294-124"><a name="resize"></a>Ağ geçidi SKU'larını yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="8e294-124"><a name="resize"></a>Resizing gateway SKUs</span></span>

1. <span data-ttu-id="8e294-125">VpnGw1, VpnGw2 ve VpnGw3 SKU'ları arasında yeniden boyutlandırma gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e294-125">You can resize between VpnGw1, VpnGw2, and VpnGw3 SKUs.</span></span>
2. <span data-ttu-id="8e294-126">Eski ağ geçidi SKU'larıyla çalışırken Temel, Standart ve Yüksek Performanslı SKU'lar arasında yeniden boyutlandırma yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e294-126">When working with the old gateway SKUs, you can resize between Basic, Standard, and HighPerformance SKUs.</span></span>
2. <span data-ttu-id="8e294-127">Temel/Standart/Yüksek Performanslı SKU'ları yeni VpnGw1/VpnGw2/VpnGw3 SKU'larıyla aynı olacak şekilde **yeniden boyutlandıramazsınız**.</span><span class="sxs-lookup"><span data-stu-id="8e294-127">You **cannot** resize from Basic/Standard/HighPerformance SKUs to the new VpnGw1/VpnGw2/VpnGw3 SKUs.</span></span> <span data-ttu-id="8e294-128">Bunun yerine yeni SKU'lara [geçiş](#migrate) yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8e294-128">You must, instead, [migrate](#migrate) to the new SKUs.</span></span>

###  <span data-ttu-id="8e294-129"><a name="migrate"></a>Eski SKU'lardan yeni SKU'lara geçiş</span><span class="sxs-lookup"><span data-stu-id="8e294-129"><a name="migrate"></a>Migrating from old SKUs to the new SKUs</span></span>

[!INCLUDE [Migrate SKU](./vpn-gateway-migrate-legacy-sku-include.md)]
