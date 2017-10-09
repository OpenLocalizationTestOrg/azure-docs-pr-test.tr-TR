## <a name="network-security-group"></a><span data-ttu-id="1546e-101">Ağ güvenlik grubu</span><span class="sxs-lookup"><span data-stu-id="1546e-101">Network Security Group</span></span>
<span data-ttu-id="1546e-102">Bir NSG kaynağı hello iş yükleri için güvenlik sınırı oluşturmanıza olanak tanıyan, uygulama tarafından izin ver ve Reddet kurallarının.</span><span class="sxs-lookup"><span data-stu-id="1546e-102">An NSG resource enables hello creation of security boundary for workloads, by implementing allow and deny rules.</span></span> <span data-ttu-id="1546e-103">Bu tür bir kurallar olabilir uygulanan tooa VM, bir NIC veya bir alt ağ.</span><span class="sxs-lookup"><span data-stu-id="1546e-103">Such rules can be applied tooa VM, a NIC, or a subnet.</span></span>

| <span data-ttu-id="1546e-104">Özellik</span><span class="sxs-lookup"><span data-stu-id="1546e-104">Property</span></span> | <span data-ttu-id="1546e-105">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1546e-105">Description</span></span> | <span data-ttu-id="1546e-106">Örnek değerler</span><span class="sxs-lookup"><span data-stu-id="1546e-106">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1546e-107">**alt ağlar**</span><span class="sxs-lookup"><span data-stu-id="1546e-107">**subnets**</span></span> |<span data-ttu-id="1546e-108">Alt ağ kimlikleri hello NSG listesi uygulanır.</span><span class="sxs-lookup"><span data-stu-id="1546e-108">List of subnet ids hello NSG is applied to.</span></span> |<span data-ttu-id="1546e-109">/Subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/Subnets/FrontEnd</span><span class="sxs-lookup"><span data-stu-id="1546e-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span></span> |
| <span data-ttu-id="1546e-110">**securityRules**</span><span class="sxs-lookup"><span data-stu-id="1546e-110">**securityRules**</span></span> |<span data-ttu-id="1546e-111">NSG hello güvenlik kuralları listesi</span><span class="sxs-lookup"><span data-stu-id="1546e-111">List of security rules that make up hello NSG</span></span> |<span data-ttu-id="1546e-112">Bkz: [güvenlik kuralı](#Security-rule) aşağıda</span><span class="sxs-lookup"><span data-stu-id="1546e-112">See [Security rule](#Security-rule) below</span></span> |
| <span data-ttu-id="1546e-113">**defaultSecurityRules**</span><span class="sxs-lookup"><span data-stu-id="1546e-113">**defaultSecurityRules**</span></span> |<span data-ttu-id="1546e-114">Varsayılan güvenlik kuralları her NSG'de mevcut listesi</span><span class="sxs-lookup"><span data-stu-id="1546e-114">List of default security rules present in every NSG</span></span> |<span data-ttu-id="1546e-115">Bkz: [varsayılan güvenlik kuralları](#Default-security-rules) aşağıda</span><span class="sxs-lookup"><span data-stu-id="1546e-115">See [Default security rules](#Default-security-rules) below</span></span> |

* <span data-ttu-id="1546e-116">**Güvenlik kuralı** -bir NSG tanımlanan birden çok güvenlik kuralları sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="1546e-116">**Security rule** - An NSG can have multiple security rules defined.</span></span> <span data-ttu-id="1546e-117">Her bir kural izin verebilir veya trafiği farklı türlerde reddet.</span><span class="sxs-lookup"><span data-stu-id="1546e-117">Each rule can allow or deny different types of traffic.</span></span>

### <a name="security-rule"></a><span data-ttu-id="1546e-118">Güvenlik kuralı</span><span class="sxs-lookup"><span data-stu-id="1546e-118">Security rule</span></span>
<span data-ttu-id="1546e-119">Güvenlik kuralı aşağıdaki hello özelliklerini içeren bir NSG bir alt kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="1546e-119">A security rule is a child resource of an NSG containing hello properties below.</span></span>

| <span data-ttu-id="1546e-120">Özellik</span><span class="sxs-lookup"><span data-stu-id="1546e-120">Property</span></span> | <span data-ttu-id="1546e-121">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1546e-121">Description</span></span> | <span data-ttu-id="1546e-122">Örnek değerler</span><span class="sxs-lookup"><span data-stu-id="1546e-122">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1546e-123">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="1546e-123">**description**</span></span> |<span data-ttu-id="1546e-124">Merhaba kuralı için açıklama</span><span class="sxs-lookup"><span data-stu-id="1546e-124">Description for hello rule</span></span> |<span data-ttu-id="1546e-125">Alt ağda X tüm VM'ler için gelen trafiğe izin ver</span><span class="sxs-lookup"><span data-stu-id="1546e-125">Allow inbound traffic for all VMs in subnet X</span></span> |
| <span data-ttu-id="1546e-126">**Protokolü**</span><span class="sxs-lookup"><span data-stu-id="1546e-126">**protocol**</span></span> |<span data-ttu-id="1546e-127">Protokol toomatch hello kuralı için</span><span class="sxs-lookup"><span data-stu-id="1546e-127">Protocol toomatch for hello rule</span></span> |<span data-ttu-id="1546e-128">TCP, UDP veya *</span><span class="sxs-lookup"><span data-stu-id="1546e-128">TCP, UDP, or *</span></span> |
| <span data-ttu-id="1546e-129">**sourcePortRange**</span><span class="sxs-lookup"><span data-stu-id="1546e-129">**sourcePortRange**</span></span> |<span data-ttu-id="1546e-130">Kaynak bağlantı noktası aralığı toomatch hello kuralı için</span><span class="sxs-lookup"><span data-stu-id="1546e-130">Source port range toomatch for hello rule</span></span> |<span data-ttu-id="1546e-131">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="1546e-131">80, 100-200, *</span></span> |
| <span data-ttu-id="1546e-132">**destinationPortRange**</span><span class="sxs-lookup"><span data-stu-id="1546e-132">**destinationPortRange**</span></span> |<span data-ttu-id="1546e-133">Hedef bağlantı noktası aralığı toomatch hello kuralı için</span><span class="sxs-lookup"><span data-stu-id="1546e-133">Destination port range toomatch for hello rule</span></span> |<span data-ttu-id="1546e-134">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="1546e-134">80, 100-200, *</span></span> |
| <span data-ttu-id="1546e-135">**sourceAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="1546e-135">**sourceAddressPrefix**</span></span> |<span data-ttu-id="1546e-136">Kaynak adres ön eki toomatch hello kuralı için</span><span class="sxs-lookup"><span data-stu-id="1546e-136">Source address prefix toomatch for hello rule</span></span> |<span data-ttu-id="1546e-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="1546e-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="1546e-138">**destinationAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="1546e-138">**destinationAddressPrefix**</span></span> |<span data-ttu-id="1546e-139">Hedef adres ön eki toomatch hello kuralı için</span><span class="sxs-lookup"><span data-stu-id="1546e-139">Destination address prefix toomatch for hello rule</span></span> |<span data-ttu-id="1546e-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="1546e-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="1546e-141">**yönü**</span><span class="sxs-lookup"><span data-stu-id="1546e-141">**direction**</span></span> |<span data-ttu-id="1546e-142">Merhaba kuralı için trafiği toomatch yönü</span><span class="sxs-lookup"><span data-stu-id="1546e-142">Direction of traffic toomatch for hello rule</span></span> |<span data-ttu-id="1546e-143">gelen veya giden</span><span class="sxs-lookup"><span data-stu-id="1546e-143">inbound or outbound</span></span> |
| <span data-ttu-id="1546e-144">**öncelik**</span><span class="sxs-lookup"><span data-stu-id="1546e-144">**priority**</span></span> |<span data-ttu-id="1546e-145">Merhaba kuralı için öncelik.</span><span class="sxs-lookup"><span data-stu-id="1546e-145">Priority for hello rule.</span></span> <span data-ttu-id="1546e-146">Kurallar öncelik sırasına göre denetlenir, bir kural uygulandığı zaman başka hiçbir kural eşleştirme için test edilmez.</span><span class="sxs-lookup"><span data-stu-id="1546e-146">Rules are checked int he order of priority, once a rule applies, no more rules are tested for matching.</span></span> |<span data-ttu-id="1546e-147">10, 100, 65000</span><span class="sxs-lookup"><span data-stu-id="1546e-147">10, 100, 65000</span></span> |
| <span data-ttu-id="1546e-148">**erişim**</span><span class="sxs-lookup"><span data-stu-id="1546e-148">**access**</span></span> |<span data-ttu-id="1546e-149">Merhaba kuralın eşleşmesi durumunda erişim tooapply türü</span><span class="sxs-lookup"><span data-stu-id="1546e-149">Type of access tooapply if hello rule matches</span></span> |<span data-ttu-id="1546e-150">izin ver veya reddet</span><span class="sxs-lookup"><span data-stu-id="1546e-150">allow or deny</span></span> |

<span data-ttu-id="1546e-151">JSON biçiminde NSG örneği:</span><span class="sxs-lookup"><span data-stu-id="1546e-151">Sample NSG in JSON format:</span></span>

    {
        "name": "NSG-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkSecurityGroups",
        "location": "westus",
        "tags": {
            "displayName": "NSG - Front End"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "securityRules": [
                {
                    "name": "rdp-rule",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/rdp-rule",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "description": "Allow RDP",
                        "protocol": "Tcp",
                        "sourcePortRange": "*",
                        "destinationPortRange": "3389",
                        "sourceAddressPrefix": "Internet",
                        "destinationAddressPrefix": "*",
                        "access": "Allow",
                        "priority": 100,
                        "direction": "Inbound"
                    }
                }
            ],
            "defaultSecurityRules": [
                { [...],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                }
            ]
        }
    }

### <a name="default-security-rules"></a><span data-ttu-id="1546e-152">Varsayılan güvenlik kuralları</span><span class="sxs-lookup"><span data-stu-id="1546e-152">Default security rules</span></span>

<span data-ttu-id="1546e-153">Varsayılan güvenlik kuralları olan hello aynı özellikleri güvenlik kurallarında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1546e-153">Default security rules have hello same properties available in security rules.</span></span> <span data-ttu-id="1546e-154">Bunlar tooprovide temel bağlantıyı uygulanan Nsg'ler toothem sahip kaynaklar arasında mevcut.</span><span class="sxs-lookup"><span data-stu-id="1546e-154">They exist tooprovide basic connectivity between resources that have NSGs applied toothem.</span></span> <span data-ttu-id="1546e-155">Hangi bildiğinizden emin olun [güvenlik kuralları varsayılan](../articles/virtual-network/virtual-networks-nsg.md#default-rules) yok.</span><span class="sxs-lookup"><span data-stu-id="1546e-155">Make sure you know which [default security rules](../articles/virtual-network/virtual-networks-nsg.md#default-rules) exist.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="1546e-156">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="1546e-156">Additional resources</span></span>
* <span data-ttu-id="1546e-157">Hakkında daha fazla bilgi almak [Nsg'ler](../articles/virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="1546e-157">Get more information about [NSGs](../articles/virtual-network/virtual-networks-nsg.md).</span></span>
* <span data-ttu-id="1546e-158">Okuma hello [REST API başvuru belgeleri](https://msdn.microsoft.com/library/azure/mt163615.aspx) Nsg'ler için.</span><span class="sxs-lookup"><span data-stu-id="1546e-158">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163615.aspx) for NSGs.</span></span>
* <span data-ttu-id="1546e-159">Okuma hello [REST API başvuru belgeleri](https://msdn.microsoft.com/library/azure/mt163580.aspx) güvenlik kuralları için.</span><span class="sxs-lookup"><span data-stu-id="1546e-159">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163580.aspx) for security rules.</span></span>
