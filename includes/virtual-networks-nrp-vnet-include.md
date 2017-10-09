## <a name="virtual-network"></a><span data-ttu-id="061fb-101">Sanal Ağ</span><span class="sxs-lookup"><span data-stu-id="061fb-101">Virtual Network</span></span>
<span data-ttu-id="061fb-102">Sanal ağ (VNET) ve alt kaynakları Azure'da çalışan iş yükleri için güvenlik sınırı tanımlamaya yardımcı olacak.</span><span class="sxs-lookup"><span data-stu-id="061fb-102">Virtual Networks (VNET) and subnets resources help define a security boundary for workloads running in Azure.</span></span> <span data-ttu-id="061fb-103">Bir sanal ağ adres alanları, CIDR bloğu tanımlı bir koleksiyon tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="061fb-103">A VNet is characterized by a collection of address spaces, defined as CIDR blocks.</span></span> 

> [!NOTE]
> <span data-ttu-id="061fb-104">Ağ yöneticileri ile CIDR gösteriminde biliyorsunuzdur.</span><span class="sxs-lookup"><span data-stu-id="061fb-104">Network administrators are familiar with CIDR notation.</span></span> <span data-ttu-id="061fb-105">CIDR ile bilmiyorsanız [hakkında daha fazla bilgi](http://whatismyipaddress.com/cidr).</span><span class="sxs-lookup"><span data-stu-id="061fb-105">If you are not familiar with CIDR, [learn more about it](http://whatismyipaddress.com/cidr).</span></span>
> 
> 

![Birden çok alt ağa sahip VNet](./media/resource-groups-networking/Figure4.png)

<span data-ttu-id="061fb-107">Sanal ağlar, aşağıdaki özelliklere hello içerir.</span><span class="sxs-lookup"><span data-stu-id="061fb-107">VNets contain hello following properties.</span></span>

| <span data-ttu-id="061fb-108">Özellik</span><span class="sxs-lookup"><span data-stu-id="061fb-108">Property</span></span> | <span data-ttu-id="061fb-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="061fb-109">Description</span></span> | <span data-ttu-id="061fb-110">Örnek değerler</span><span class="sxs-lookup"><span data-stu-id="061fb-110">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="061fb-111">**addressSpace**</span><span class="sxs-lookup"><span data-stu-id="061fb-111">**addressSpace**</span></span> |<span data-ttu-id="061fb-112">CIDR gösteriminde hello VNet oluşturan adres öneklerini koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="061fb-112">Collection of address prefixes that make up hello VNet in CIDR notation</span></span> |<span data-ttu-id="061fb-113">192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="061fb-113">192.168.0.0/16</span></span> |
| <span data-ttu-id="061fb-114">**alt ağlar**</span><span class="sxs-lookup"><span data-stu-id="061fb-114">**subnets**</span></span> |<span data-ttu-id="061fb-115">VNet hello yapmak alt koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="061fb-115">Collection of subnets that make up hello VNet</span></span> |<span data-ttu-id="061fb-116">bkz: [alt ağlar](#Subnets) aşağıda.</span><span class="sxs-lookup"><span data-stu-id="061fb-116">see [subnets](#Subnets) below.</span></span> |
| <span data-ttu-id="061fb-117">**IP adresi**</span><span class="sxs-lookup"><span data-stu-id="061fb-117">**ipAddress**</span></span> |<span data-ttu-id="061fb-118">IP adresi tooobject atanır.</span><span class="sxs-lookup"><span data-stu-id="061fb-118">IP address assigned tooobject.</span></span> <span data-ttu-id="061fb-119">Bu salt okunur bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="061fb-119">This is a read-only property.</span></span> |<span data-ttu-id="061fb-120">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="061fb-120">104.42.233.77</span></span> |

### <a name="subnets"></a><span data-ttu-id="061fb-121">Alt ağlar</span><span class="sxs-lookup"><span data-stu-id="061fb-121">Subnets</span></span>
<span data-ttu-id="061fb-122">Bir alt ağ alt bir vnet'in kaynaktır ve adres alanları IP adresi öneklerini kullanarak bir CIDR bloğu içinde kesimleri yardımcı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="061fb-122">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="061fb-123">NIC toosubnets ve çeşitli iş yükleri için bağlantı sağlama bağlı tooVMs eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="061fb-123">NICs can be added toosubnets, and connected tooVMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="061fb-124">Alt ağları aşağıdaki özelliklere hello içerir.</span><span class="sxs-lookup"><span data-stu-id="061fb-124">Subnets contain hello following properties.</span></span> 

| <span data-ttu-id="061fb-125">Özellik</span><span class="sxs-lookup"><span data-stu-id="061fb-125">Property</span></span> | <span data-ttu-id="061fb-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="061fb-126">Description</span></span> | <span data-ttu-id="061fb-127">Örnek değerler</span><span class="sxs-lookup"><span data-stu-id="061fb-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="061fb-128">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="061fb-128">**addressPrefix**</span></span> |<span data-ttu-id="061fb-129">Merhaba alt ağ CIDR gösteriminde oluşturan tek adresi öneki</span><span class="sxs-lookup"><span data-stu-id="061fb-129">Single address prefix that make up hello subnet in CIDR notation</span></span> |<span data-ttu-id="061fb-130">192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="061fb-130">192.168.1.0/24</span></span> |
| <span data-ttu-id="061fb-131">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="061fb-131">**networkSecurityGroup**</span></span> |<span data-ttu-id="061fb-132">NSG uygulanır toohello alt ağ</span><span class="sxs-lookup"><span data-stu-id="061fb-132">NSG applied toohello subnet</span></span> |<span data-ttu-id="061fb-133">bkz: [Nsg'ler](#Network-Security-Group)</span><span class="sxs-lookup"><span data-stu-id="061fb-133">see [NSGs](#Network-Security-Group)</span></span> |
| <span data-ttu-id="061fb-134">**routeTable**</span><span class="sxs-lookup"><span data-stu-id="061fb-134">**routeTable**</span></span> |<span data-ttu-id="061fb-135">Yol tablosu toohello alt uygulanan</span><span class="sxs-lookup"><span data-stu-id="061fb-135">Route table applied toohello subnet</span></span> |<span data-ttu-id="061fb-136">bkz: [UDR](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="061fb-136">see [UDR](#Route-table)</span></span> |
| <span data-ttu-id="061fb-137">**Ipconfigurations**</span><span class="sxs-lookup"><span data-stu-id="061fb-137">**ipConfigurations**</span></span> |<span data-ttu-id="061fb-138">NIC bağlı toohello alt ağı tarafından kullanılan IP yapılandırma nesneleri koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="061fb-138">Collection of IP configruation objects used by NICs connected toohello subnet</span></span> |<span data-ttu-id="061fb-139">bkz: [UDR](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="061fb-139">see [UDR](#Route-table)</span></span> |

<span data-ttu-id="061fb-140">JSON biçiminde örnek VNet:</span><span class="sxs-lookup"><span data-stu-id="061fb-140">Sample VNet in JSON format:</span></span>

    {
        "name": "TestVNet",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/virtualNetworks",
        "location": "westus",
        "tags": {
            "displayName": "VNet"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "addressSpace": {
                "addressPrefixes": [
                    "192.168.0.0/16"
                ]
            },
            "subnets": [
                {
                    "name": "FrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "networkSecurityGroup": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "routeTable": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd"
                        },
                        "ipConfigurations": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConfigurations/ipconfig1"
                            },
                            ...]
                    }
                },
                ...]
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="061fb-141">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="061fb-141">Additional resources</span></span>
* <span data-ttu-id="061fb-142">Hakkında daha fazla bilgi almak [VNet](../articles/virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="061fb-142">Get more information about [VNet](../articles/virtual-network/virtual-networks-overview.md).</span></span>
* <span data-ttu-id="061fb-143">Okuma hello [REST API başvuru belgeleri](https://msdn.microsoft.com/library/azure/mt163650.aspx) sanal ağlar için.</span><span class="sxs-lookup"><span data-stu-id="061fb-143">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163650.aspx) for VNets.</span></span>
* <span data-ttu-id="061fb-144">Okuma hello [REST API başvuru belgeleri](https://msdn.microsoft.com/library/azure/mt163618.aspx) alt ağlar için.</span><span class="sxs-lookup"><span data-stu-id="061fb-144">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163618.aspx) for Subnets.</span></span>

