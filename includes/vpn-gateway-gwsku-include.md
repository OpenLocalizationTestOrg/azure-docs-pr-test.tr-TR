<span data-ttu-id="cab8d-101">Bir sanal ağ geçidi oluştururken toospecify hello ağ geçidi SKU'su toouse istediğiniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cab8d-101">When you create a virtual network gateway, you need toospecify hello gateway SKU that you want toouse.</span></span> <span data-ttu-id="cab8d-102">İş yükleri, kapatma, özellikleri ve SLA hello türlerine göre gereksinimlerinizi karşılayan hello SKU'ları seçin.</span><span class="sxs-lookup"><span data-stu-id="cab8d-102">Select hello SKUs that satisfy your requirements based on hello types of workloads, throughputs, features, and SLAs.</span></span>

[!INCLUDE [classic SKU](./vpn-gateway-classic-sku-support-include.md)]

[!INCLUDE [Aggregated throughput by SKU](./vpn-gateway-table-gwtype-aggtput-include.md)]

###  <span data-ttu-id="cab8d-103"><a name="workloads"></a>Üretim *ve* Geliştirme-Test İş Yükleri Karşılaştırması</span><span class="sxs-lookup"><span data-stu-id="cab8d-103"><a name="workloads"></a>Production *vs.* Dev-Test Workloads</span></span>

<span data-ttu-id="cab8d-104">Üretim için SKU'ları aşağıdaki hello öneririz SLA ve özellik kümeleri toohello farklılıkları *karşılaştırması* geliştirme, test:</span><span class="sxs-lookup"><span data-stu-id="cab8d-104">Due toohello differences in SLAs and feature sets, we recommend hello following SKUs for production *vs.* dev-test:</span></span>

| <span data-ttu-id="cab8d-105">**İş yükü**</span><span class="sxs-lookup"><span data-stu-id="cab8d-105">**Workload**</span></span>                       | <span data-ttu-id="cab8d-106">**SKU'lar**</span><span class="sxs-lookup"><span data-stu-id="cab8d-106">**SKUs**</span></span>               |
| ---                                | ---                    |
| <span data-ttu-id="cab8d-107">**Üretim, kritik iş yükleri**</span><span class="sxs-lookup"><span data-stu-id="cab8d-107">**Production, critical workloads**</span></span> | <span data-ttu-id="cab8d-108">VpnGw1, VpnGw2, VpnGw3</span><span class="sxs-lookup"><span data-stu-id="cab8d-108">VpnGw1, VpnGw2, VpnGw3</span></span> |
| <span data-ttu-id="cab8d-109">**Geliştirme-test veya kavram kanıtı**</span><span class="sxs-lookup"><span data-stu-id="cab8d-109">**Dev-test or proof of concept**</span></span>   | <span data-ttu-id="cab8d-110">Temel</span><span class="sxs-lookup"><span data-stu-id="cab8d-110">Basic</span></span>                  |
|                                    |                        |

<span data-ttu-id="cab8d-111">Merhaba eski kullanıyorsanız, hello üretim SKU önerileri standart ve HighPerformance SKU'ları SKU'lar.</span><span class="sxs-lookup"><span data-stu-id="cab8d-111">If you are using hello old SKUs, hello production SKU recommendations are Standard and HighPerformance SKUs.</span></span> <span data-ttu-id="cab8d-112">Eski SKU hello hakkında bilgi için bkz: [ağ geçidi SKU'ları (eski SKU)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="cab8d-112">For information on hello old SKUs, see [Gateway SKUs (legacy SKUs)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md).</span></span>

###  <span data-ttu-id="cab8d-113"><a name="feature"></a>Ağ geçidi SKU'su özellik kümeleri</span><span class="sxs-lookup"><span data-stu-id="cab8d-113"><a name="feature"></a>Gateway SKU feature sets</span></span>

<span data-ttu-id="cab8d-114">Merhaba gateway'lerinde sunulan hello yeni ağ geçidi SKU'ları daha verimli hale hello özellik kümeleri:</span><span class="sxs-lookup"><span data-stu-id="cab8d-114">hello new gateway SKUs streamline hello feature sets offered on hello gateways:</span></span>

| <span data-ttu-id="cab8d-115">**SKU**</span><span class="sxs-lookup"><span data-stu-id="cab8d-115">**SKU**</span></span>| <span data-ttu-id="cab8d-116">**Özellikler**</span><span class="sxs-lookup"><span data-stu-id="cab8d-116">**Features**</span></span>|
| ---    | ---         |
|<span data-ttu-id="cab8d-117">**Temel**</span><span class="sxs-lookup"><span data-stu-id="cab8d-117">**Basic**</span></span>   | <span data-ttu-id="cab8d-118">**Rota tabanlı VPN**: P2S ile 10 tünel</span><span class="sxs-lookup"><span data-stu-id="cab8d-118">**Route-based VPN**: 10 tunnels with P2S</span></span><br><br><span data-ttu-id="cab8d-119">**İlke tabanlı VPN** (IKEv1): 1 tünel; P2S yok</span><span class="sxs-lookup"><span data-stu-id="cab8d-119">**Policy-based VPN**: (IKEv1): 1 tunnel; no P2S</span></span>|
| <span data-ttu-id="cab8d-120">**VpnGw1, VpnGw2 ve VpnGw3**</span><span class="sxs-lookup"><span data-stu-id="cab8d-120">**VpnGw1, VpnGw2, and VpnGw3**</span></span> | <span data-ttu-id="cab8d-121">**Rota tabanlı VPN**: too30 tünelleri (*), P2S, BGP yukarı etkin-etkin, özel IPSec/IKE İlkesi, ExpressRoute/VPN birlikte bulunma</span><span class="sxs-lookup"><span data-stu-id="cab8d-121">**Route-based VPN**: up too30 tunnels (*), P2S, BGP, active-active, custom IPsec/IKE policy, ExpressRoute/VPN co-existence</span></span> |
|        |             |

<span data-ttu-id="cab8d-122">(*) Bir rota tabanlı VPN ağ geçidi (VpnGw1, VpnGw2, VpnGw3) toomultiple şirket içi ilke tabanlı güvenlik duvarı aygıtları "PolicyBasedTrafficSelectors" tooconnect yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cab8d-122">(*) You can configure "PolicyBasedTrafficSelectors" tooconnect a route-based VPN gateway (VpnGw1, VpnGw2, VpnGw3) toomultiple on-premises policy-based firewall devices.</span></span> <span data-ttu-id="cab8d-123">Çok başvuran[bağlanmak VPN ağ geçitleri toomultiple şirket içi ilke tabanlı VPN aygıtları PowerShell kullanarak](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="cab8d-123">Refer too[Connect VPN gateways toomultiple on-premises policy-based VPN devices using PowerShell](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) for details.</span></span>

###  <span data-ttu-id="cab8d-124"><a name="resize"></a>Ağ geçidi SKU'larını yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="cab8d-124"><a name="resize"></a>Resizing gateway SKUs</span></span>

1. <span data-ttu-id="cab8d-125">VpnGw1, VpnGw2 ve VpnGw3 SKU'ları arasında yeniden boyutlandırma gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cab8d-125">You can resize between VpnGw1, VpnGw2, and VpnGw3 SKUs.</span></span>
2. <span data-ttu-id="cab8d-126">Merhaba eski gateway SKU'ları ile çalışırken, temel, standart ve HighPerformance SKU'ları arasında yeniden boyutlandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cab8d-126">When working with hello old gateway SKUs, you can resize between Basic, Standard, and HighPerformance SKUs.</span></span>
2. <span data-ttu-id="cab8d-127">**Olamaz** standart/Basic/HighPerformance SKU'ları toohello yeniden boyutlandırma yeni VpnGw2/VpnGw1/VpnGw3 SKU'ları.</span><span class="sxs-lookup"><span data-stu-id="cab8d-127">You **cannot** resize from Basic/Standard/HighPerformance SKUs toohello new VpnGw1/VpnGw2/VpnGw3 SKUs.</span></span> <span data-ttu-id="cab8d-128">Bunun yerine, gerekir [geçirmek](#migrate) toohello yeni SKU'ları.</span><span class="sxs-lookup"><span data-stu-id="cab8d-128">You must, instead, [migrate](#migrate) toohello new SKUs.</span></span>

###  <span data-ttu-id="cab8d-129"><a name="migrate"></a>Eski SKU'ları toohello geçiş yeni SKU'ları</span><span class="sxs-lookup"><span data-stu-id="cab8d-129"><a name="migrate"></a>Migrating from old SKUs toohello new SKUs</span></span>

[!INCLUDE [Migrate SKU](./vpn-gateway-migrate-legacy-sku-include.md)]
