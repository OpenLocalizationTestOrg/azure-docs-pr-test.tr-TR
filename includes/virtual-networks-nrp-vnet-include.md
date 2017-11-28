## <a name="virtual-network"></a><span data-ttu-id="b8b19-101">Sanal Ağ</span><span class="sxs-lookup"><span data-stu-id="b8b19-101">Virtual Network</span></span>
<span data-ttu-id="b8b19-102">Sanal ağ (VNET) ve alt kaynakları Azure'da çalışan iş yükleri için güvenlik sınırı tanımlamaya yardımcı olacak.</span><span class="sxs-lookup"><span data-stu-id="b8b19-102">Virtual Networks (VNET) and subnets resources help define a security boundary for workloads running in Azure.</span></span> <span data-ttu-id="b8b19-103">Bir sanal ağ adres alanları, CIDR bloğu tanımlı bir koleksiyon tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="b8b19-103">A VNet is characterized by a collection of address spaces, defined as CIDR blocks.</span></span> 

> [!NOTE]
> <span data-ttu-id="b8b19-104">Ağ yöneticileri ile CIDR gösteriminde biliyorsunuzdur.</span><span class="sxs-lookup"><span data-stu-id="b8b19-104">Network administrators are familiar with CIDR notation.</span></span> <span data-ttu-id="b8b19-105">CIDR ile bilmiyorsanız [hakkında daha fazla bilgi](http://whatismyipaddress.com/cidr).</span><span class="sxs-lookup"><span data-stu-id="b8b19-105">If you are not familiar with CIDR, [learn more about it](http://whatismyipaddress.com/cidr).</span></span>
> 
> 

![Birden çok alt ağa sahip VNet](./media/resource-groups-networking/Figure4.png)

<span data-ttu-id="b8b19-107">Sanal ağlar aşağıdaki özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="b8b19-107">VNets contain the following properties.</span></span>

| <span data-ttu-id="b8b19-108">Özellik</span><span class="sxs-lookup"><span data-stu-id="b8b19-108">Property</span></span> | <span data-ttu-id="b8b19-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b8b19-109">Description</span></span> | <span data-ttu-id="b8b19-110">Örnek değerler</span><span class="sxs-lookup"><span data-stu-id="b8b19-110">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b8b19-111">**addressSpace**</span><span class="sxs-lookup"><span data-stu-id="b8b19-111">**addressSpace**</span></span> |<span data-ttu-id="b8b19-112">CIDR gösteriminde VNet oluşturan adres öneklerini koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="b8b19-112">Collection of address prefixes that make up the VNet in CIDR notation</span></span> |<span data-ttu-id="b8b19-113">192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="b8b19-113">192.168.0.0/16</span></span> |
| <span data-ttu-id="b8b19-114">**alt ağlar**</span><span class="sxs-lookup"><span data-stu-id="b8b19-114">**subnets**</span></span> |<span data-ttu-id="b8b19-115">VNet yapmak alt koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="b8b19-115">Collection of subnets that make up the VNet</span></span> |<span data-ttu-id="b8b19-116">bkz: [alt ağlar](#Subnets) aşağıda.</span><span class="sxs-lookup"><span data-stu-id="b8b19-116">see [subnets](#Subnets) below.</span></span> |
| <span data-ttu-id="b8b19-117">**IP adresi**</span><span class="sxs-lookup"><span data-stu-id="b8b19-117">**ipAddress**</span></span> |<span data-ttu-id="b8b19-118">Nesne için atanan IP adresi.</span><span class="sxs-lookup"><span data-stu-id="b8b19-118">IP address assigned to object.</span></span> <span data-ttu-id="b8b19-119">Bu salt okunur bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="b8b19-119">This is a read-only property.</span></span> |<span data-ttu-id="b8b19-120">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="b8b19-120">104.42.233.77</span></span> |

### <a name="subnets"></a><span data-ttu-id="b8b19-121">Alt ağlar</span><span class="sxs-lookup"><span data-stu-id="b8b19-121">Subnets</span></span>
<span data-ttu-id="b8b19-122">Bir alt ağ alt bir vnet'in kaynaktır ve adres alanları IP adresi öneklerini kullanarak bir CIDR bloğu içinde kesimleri yardımcı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="b8b19-122">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="b8b19-123">NIC alt ağlara eklendi ve çeşitli iş yükleri için bağlantı sağlama VM'ler bağlı.</span><span class="sxs-lookup"><span data-stu-id="b8b19-123">NICs can be added to subnets, and connected to VMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="b8b19-124">Alt ağları aşağıdaki özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="b8b19-124">Subnets contain the following properties.</span></span> 

| <span data-ttu-id="b8b19-125">Özellik</span><span class="sxs-lookup"><span data-stu-id="b8b19-125">Property</span></span> | <span data-ttu-id="b8b19-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b8b19-126">Description</span></span> | <span data-ttu-id="b8b19-127">Örnek değerler</span><span class="sxs-lookup"><span data-stu-id="b8b19-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b8b19-128">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="b8b19-128">**addressPrefix**</span></span> |<span data-ttu-id="b8b19-129">Alt ağ CIDR gösteriminde oluşturan tek adresi öneki</span><span class="sxs-lookup"><span data-stu-id="b8b19-129">Single address prefix that make up the subnet in CIDR notation</span></span> |<span data-ttu-id="b8b19-130">192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="b8b19-130">192.168.1.0/24</span></span> |
| <span data-ttu-id="b8b19-131">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="b8b19-131">**networkSecurityGroup**</span></span> |<span data-ttu-id="b8b19-132">NSG alt ağına uygulanır</span><span class="sxs-lookup"><span data-stu-id="b8b19-132">NSG applied to the subnet</span></span> |<span data-ttu-id="b8b19-133">bkz: [Nsg'ler](#Network-Security-Group)</span><span class="sxs-lookup"><span data-stu-id="b8b19-133">see [NSGs](#Network-Security-Group)</span></span> |
| <span data-ttu-id="b8b19-134">**routeTable**</span><span class="sxs-lookup"><span data-stu-id="b8b19-134">**routeTable**</span></span> |<span data-ttu-id="b8b19-135">Alt ağa uygulanan yol tablosu</span><span class="sxs-lookup"><span data-stu-id="b8b19-135">Route table applied to the subnet</span></span> |<span data-ttu-id="b8b19-136">bkz: [UDR](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="b8b19-136">see [UDR](#Route-table)</span></span> |
| <span data-ttu-id="b8b19-137">**Ipconfigurations**</span><span class="sxs-lookup"><span data-stu-id="b8b19-137">**ipConfigurations**</span></span> |<span data-ttu-id="b8b19-138">Alt ağına bağlı NIC tarafından kullanılan IP yapılandırma nesnelerinin koleksiyonunu</span><span class="sxs-lookup"><span data-stu-id="b8b19-138">Collection of IP configruation objects used by NICs connected to the subnet</span></span> |<span data-ttu-id="b8b19-139">bkz: [UDR](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="b8b19-139">see [UDR](#Route-table)</span></span> |

<span data-ttu-id="b8b19-140">JSON biçiminde örnek VNet:</span><span class="sxs-lookup"><span data-stu-id="b8b19-140">Sample VNet in JSON format:</span></span>

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

### <a name="additional-resources"></a><span data-ttu-id="b8b19-141">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b8b19-141">Additional resources</span></span>
* <span data-ttu-id="b8b19-142">Hakkında daha fazla bilgi almak [VNet](../articles/virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b8b19-142">Get more information about [VNet](../articles/virtual-network/virtual-networks-overview.md).</span></span>
* <span data-ttu-id="b8b19-143">Okuma [REST API başvuru belgeleri](https://msdn.microsoft.com/library/azure/mt163650.aspx) sanal ağlar için.</span><span class="sxs-lookup"><span data-stu-id="b8b19-143">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163650.aspx) for VNets.</span></span>
* <span data-ttu-id="b8b19-144">Okuma [REST API başvuru belgeleri](https://msdn.microsoft.com/library/azure/mt163618.aspx) alt ağlar için.</span><span class="sxs-lookup"><span data-stu-id="b8b19-144">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163618.aspx) for Subnets.</span></span>

