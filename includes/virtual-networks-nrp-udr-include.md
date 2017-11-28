## <a name="route-tables"></a><span data-ttu-id="400bd-101">Yönlendirme tabloları</span><span class="sxs-lookup"><span data-stu-id="400bd-101">Route tables</span></span>
<span data-ttu-id="400bd-102">Rota tablosu kaynakları Azure altyapısı içinde trafiğinin nasıl akacağını belirlemek için kullanılan yolları içerir.</span><span class="sxs-lookup"><span data-stu-id="400bd-102">Route table resources contains routes used to define how traffic flows within your Azure infrastructure.</span></span> <span data-ttu-id="400bd-103">Bir güvenlik duvarı veya izinsiz giriş algılama sistem gibi (Kimlikler) tüm trafik için sanal bir gereç, belirli bir alt ağ üzerinden göndermek için kullanıcı tanımlı yolları (UDR) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="400bd-103">You can use user defined routes (UDR) to send all traffic from a given subnet to a virtual appliance, such as a firewall or intrusion detection system (IDS).</span></span> <span data-ttu-id="400bd-104">Bir yol tablosu alt ağlara ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="400bd-104">You can associate a route table to subnets.</span></span> 

<span data-ttu-id="400bd-105">Yönlendirme tabloları aşağıdaki özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="400bd-105">Route tables contain the following properties.</span></span>

| <span data-ttu-id="400bd-106">Özellik</span><span class="sxs-lookup"><span data-stu-id="400bd-106">Property</span></span> | <span data-ttu-id="400bd-107">Açıklama</span><span class="sxs-lookup"><span data-stu-id="400bd-107">Description</span></span> | <span data-ttu-id="400bd-108">Örnek değerler</span><span class="sxs-lookup"><span data-stu-id="400bd-108">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="400bd-109">**yollar**</span><span class="sxs-lookup"><span data-stu-id="400bd-109">**routes**</span></span> |<span data-ttu-id="400bd-110">Kullanıcı koleksiyonunu rota tablosunda tanımlı yollar</span><span class="sxs-lookup"><span data-stu-id="400bd-110">Collection of user defined routes in the route table</span></span> |<span data-ttu-id="400bd-111">bkz: [kullanıcı tanımlı yollar](#User-defined-routes)</span><span class="sxs-lookup"><span data-stu-id="400bd-111">see [user defined routes](#User-defined-routes)</span></span> |
| <span data-ttu-id="400bd-112">**alt ağlar**</span><span class="sxs-lookup"><span data-stu-id="400bd-112">**subnets**</span></span> |<span data-ttu-id="400bd-113">Alt ağlar koleksiyonunu rota tablosu uygulanır.</span><span class="sxs-lookup"><span data-stu-id="400bd-113">Collection of subnets the route table is applied to</span></span> |<span data-ttu-id="400bd-114">bkz: [alt ağlar](#Subnets)</span><span class="sxs-lookup"><span data-stu-id="400bd-114">see [subnets](#Subnets)</span></span> |

### <a name="user-defined-routes"></a><span data-ttu-id="400bd-115">Kullanıcı tanımlı yollar</span><span class="sxs-lookup"><span data-stu-id="400bd-115">User defined routes</span></span>
<span data-ttu-id="400bd-116">Hedef adresine göre burada trafiği için gönderilmesi gerektiğini belirtmek için Udr'ler oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="400bd-116">You can create UDRs to specify where traffic should be sent to, based on its destination address.</span></span> <span data-ttu-id="400bd-117">Bir ağ paketi hedef adresini temel alarak varsayılan ağ geçidi tanımı bir yolu düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="400bd-117">You can think of a route as the default gateway definition based on the destination address of a network packet.</span></span>

<span data-ttu-id="400bd-118">Udr'ler aşağıdaki özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="400bd-118">UDRs contain the following properties.</span></span> 

| <span data-ttu-id="400bd-119">Özellik</span><span class="sxs-lookup"><span data-stu-id="400bd-119">Property</span></span> | <span data-ttu-id="400bd-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="400bd-120">Description</span></span> | <span data-ttu-id="400bd-121">Örnek değerler</span><span class="sxs-lookup"><span data-stu-id="400bd-121">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="400bd-122">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="400bd-122">**addressPrefix**</span></span> |<span data-ttu-id="400bd-123">Adres ön eki veya hedef için tam IP adresi</span><span class="sxs-lookup"><span data-stu-id="400bd-123">Address prefix, or full IP address for the destination</span></span> |<span data-ttu-id="400bd-124">192.168.1.0/24, 192.168.1.101</span><span class="sxs-lookup"><span data-stu-id="400bd-124">192.168.1.0/24, 192.168.1.101</span></span> |
| <span data-ttu-id="400bd-125">**nextHopType**</span><span class="sxs-lookup"><span data-stu-id="400bd-125">**nextHopType**</span></span> |<span data-ttu-id="400bd-126">Trafiğin gönderileceği aygıt türü</span><span class="sxs-lookup"><span data-stu-id="400bd-126">Type of device the traffic will be sent to</span></span> |<span data-ttu-id="400bd-127">Değerinin VirtualAppliance, VPN ağ geçidi, Internet</span><span class="sxs-lookup"><span data-stu-id="400bd-127">VirtualAppliance, VPN Gateway, Internet</span></span> |
| <span data-ttu-id="400bd-128">**Nexthopıpaddress**</span><span class="sxs-lookup"><span data-stu-id="400bd-128">**nextHopIpAddress**</span></span> |<span data-ttu-id="400bd-129">Sonraki atlama IP adresi</span><span class="sxs-lookup"><span data-stu-id="400bd-129">IP address for the next hop</span></span> |<span data-ttu-id="400bd-130">192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="400bd-130">192.168.1.4</span></span> |

<span data-ttu-id="400bd-131">JSON biçiminde örnek yol tablosu:</span><span class="sxs-lookup"><span data-stu-id="400bd-131">Sample route table in JSON format:</span></span>

    {
        "name": "UDR-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/routeTables",
        "location": "westus",
        "properties": {
            "provisioningState": "Succeeded",
            "routes": [
                {
                    "name": "RouteToFrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd/routes/RouteToFrontEnd",
                    "etag": "W/\"v\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "nextHopType": "VirtualAppliance",
                        "nextHopIpAddress": "192.168.0.4"
                    }
                }
            ],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd"
                }
            ]
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="400bd-132">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="400bd-132">Additional resources</span></span>
* <span data-ttu-id="400bd-133">Hakkında daha fazla bilgi almak [Udr'ler](../articles/virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="400bd-133">Get more information about [UDRs](../articles/virtual-network/virtual-networks-udr-overview.md).</span></span>
* <span data-ttu-id="400bd-134">Okuma [REST API başvuru belgeleri](https://msdn.microsoft.com/library/azure/mt502549.aspx) yönlendirme tabloları için.</span><span class="sxs-lookup"><span data-stu-id="400bd-134">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502549.aspx) for route tables.</span></span>
* <span data-ttu-id="400bd-135">Okuma [REST API başvuru belgeleri](https://msdn.microsoft.com/library/azure/mt502539.aspx) için kullanıcı tanımlı yollar (Udr'ler).</span><span class="sxs-lookup"><span data-stu-id="400bd-135">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502539.aspx) for user defined routes (UDRs).</span></span>

