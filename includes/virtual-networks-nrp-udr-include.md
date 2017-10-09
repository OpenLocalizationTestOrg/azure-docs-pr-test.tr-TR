## <a name="route-tables"></a><span data-ttu-id="90333-101">Yönlendirme tabloları</span><span class="sxs-lookup"><span data-stu-id="90333-101">Route tables</span></span>
<span data-ttu-id="90333-102">Rota tablosu kaynakları Azure altyapısı içinde trafiğinin nasıl akacağını kullanılan yolları toodefine içerir.</span><span class="sxs-lookup"><span data-stu-id="90333-102">Route table resources contains routes used toodefine how traffic flows within your Azure infrastructure.</span></span> <span data-ttu-id="90333-103">Belirli alt ağ tooa sanal gereç, bir güvenlik duvarı veya izinsiz giriş algılama sistemi gibi (Kimlikler) gelen tüm trafiği kullanıcı tanımlı yolları (UDR) toosend kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90333-103">You can use user defined routes (UDR) toosend all traffic from a given subnet tooa virtual appliance, such as a firewall or intrusion detection system (IDS).</span></span> <span data-ttu-id="90333-104">Bir rota tablosu toosubnets ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90333-104">You can associate a route table toosubnets.</span></span> 

<span data-ttu-id="90333-105">Yönlendirme tabloları aşağıdaki özelliklere hello içerir.</span><span class="sxs-lookup"><span data-stu-id="90333-105">Route tables contain hello following properties.</span></span>

| <span data-ttu-id="90333-106">Özellik</span><span class="sxs-lookup"><span data-stu-id="90333-106">Property</span></span> | <span data-ttu-id="90333-107">Açıklama</span><span class="sxs-lookup"><span data-stu-id="90333-107">Description</span></span> | <span data-ttu-id="90333-108">Örnek değerler</span><span class="sxs-lookup"><span data-stu-id="90333-108">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="90333-109">**yollar**</span><span class="sxs-lookup"><span data-stu-id="90333-109">**routes**</span></span> |<span data-ttu-id="90333-110">Kullanıcı koleksiyonu yolları hello rota tablosunda tanımlı.</span><span class="sxs-lookup"><span data-stu-id="90333-110">Collection of user defined routes in hello route table</span></span> |<span data-ttu-id="90333-111">bkz: [kullanıcı tanımlı yollar](#User-defined-routes)</span><span class="sxs-lookup"><span data-stu-id="90333-111">see [user defined routes](#User-defined-routes)</span></span> |
| <span data-ttu-id="90333-112">**alt ağlar**</span><span class="sxs-lookup"><span data-stu-id="90333-112">**subnets**</span></span> |<span data-ttu-id="90333-113">Alt ağlar hello yol tablosu koleksiyonunu çok uygulanır</span><span class="sxs-lookup"><span data-stu-id="90333-113">Collection of subnets hello route table is applied too</span></span>|<span data-ttu-id="90333-114">bkz: [alt ağlar](#Subnets)</span><span class="sxs-lookup"><span data-stu-id="90333-114">see [subnets](#Subnets)</span></span> |

### <a name="user-defined-routes"></a><span data-ttu-id="90333-115">Kullanıcı tanımlı yollar</span><span class="sxs-lookup"><span data-stu-id="90333-115">User defined routes</span></span>
<span data-ttu-id="90333-116">Hedef adresine göre burada trafiği, gönderilmesi gereken Udr'ler toospecify oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90333-116">You can create UDRs toospecify where traffic should be sent to, based on its destination address.</span></span> <span data-ttu-id="90333-117">Bir yolu, bir ağ paketinin hello hedef adresine göre hello varsayılan ağ geçidi tanımı olarak düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90333-117">You can think of a route as hello default gateway definition based on hello destination address of a network packet.</span></span>

<span data-ttu-id="90333-118">Aşağıdaki özelliklere hello Udr'ler içerir.</span><span class="sxs-lookup"><span data-stu-id="90333-118">UDRs contain hello following properties.</span></span> 

| <span data-ttu-id="90333-119">Özellik</span><span class="sxs-lookup"><span data-stu-id="90333-119">Property</span></span> | <span data-ttu-id="90333-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="90333-120">Description</span></span> | <span data-ttu-id="90333-121">Örnek değerler</span><span class="sxs-lookup"><span data-stu-id="90333-121">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="90333-122">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="90333-122">**addressPrefix**</span></span> |<span data-ttu-id="90333-123">Merhaba hedef tam IP adresini veya adres öneki</span><span class="sxs-lookup"><span data-stu-id="90333-123">Address prefix, or full IP address for hello destination</span></span> |<span data-ttu-id="90333-124">192.168.1.0/24, 192.168.1.101</span><span class="sxs-lookup"><span data-stu-id="90333-124">192.168.1.0/24, 192.168.1.101</span></span> |
| <span data-ttu-id="90333-125">**nextHopType**</span><span class="sxs-lookup"><span data-stu-id="90333-125">**nextHopType**</span></span> |<span data-ttu-id="90333-126">Cihaz hello trafik türü çok gönderilir</span><span class="sxs-lookup"><span data-stu-id="90333-126">Type of device hello traffic will be sent too</span></span>|<span data-ttu-id="90333-127">Değerinin VirtualAppliance, VPN ağ geçidi, Internet</span><span class="sxs-lookup"><span data-stu-id="90333-127">VirtualAppliance, VPN Gateway, Internet</span></span> |
| <span data-ttu-id="90333-128">**Nexthopıpaddress**</span><span class="sxs-lookup"><span data-stu-id="90333-128">**nextHopIpAddress**</span></span> |<span data-ttu-id="90333-129">Merhaba sonraki atlama IP adresi</span><span class="sxs-lookup"><span data-stu-id="90333-129">IP address for hello next hop</span></span> |<span data-ttu-id="90333-130">192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="90333-130">192.168.1.4</span></span> |

<span data-ttu-id="90333-131">JSON biçiminde örnek yol tablosu:</span><span class="sxs-lookup"><span data-stu-id="90333-131">Sample route table in JSON format:</span></span>

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

### <a name="additional-resources"></a><span data-ttu-id="90333-132">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="90333-132">Additional resources</span></span>
* <span data-ttu-id="90333-133">Hakkında daha fazla bilgi almak [Udr'ler](../articles/virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="90333-133">Get more information about [UDRs](../articles/virtual-network/virtual-networks-udr-overview.md).</span></span>
* <span data-ttu-id="90333-134">Okuma hello [REST API başvuru belgeleri](https://msdn.microsoft.com/library/azure/mt502549.aspx) yönlendirme tabloları için.</span><span class="sxs-lookup"><span data-stu-id="90333-134">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502549.aspx) for route tables.</span></span>
* <span data-ttu-id="90333-135">Okuma hello [REST API başvuru belgeleri](https://msdn.microsoft.com/library/azure/mt502539.aspx) için kullanıcı tanımlı yollar (Udr'ler).</span><span class="sxs-lookup"><span data-stu-id="90333-135">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502539.aspx) for user defined routes (UDRs).</span></span>

