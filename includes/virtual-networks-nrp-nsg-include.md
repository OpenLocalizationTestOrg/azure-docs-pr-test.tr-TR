## <a name="network-security-group"></a><span data-ttu-id="43507-101">Ağ güvenlik grubu</span><span class="sxs-lookup"><span data-stu-id="43507-101">Network Security Group</span></span>
<span data-ttu-id="43507-102">Bir NSG kaynağı iş yükleri için güvenlik sınırı oluşturmanıza olanak tanıyan, uygulama tarafından izin ver ve Reddet kurallarının.</span><span class="sxs-lookup"><span data-stu-id="43507-102">An NSG resource enables the creation of security boundary for workloads, by implementing allow and deny rules.</span></span> <span data-ttu-id="43507-103">Bu kurallar, bir VM, bir NIC veya bir alt ağ için uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="43507-103">Such rules can be applied to a VM, a NIC, or a subnet.</span></span>

| <span data-ttu-id="43507-104">Özellik</span><span class="sxs-lookup"><span data-stu-id="43507-104">Property</span></span> | <span data-ttu-id="43507-105">Açıklama</span><span class="sxs-lookup"><span data-stu-id="43507-105">Description</span></span> | <span data-ttu-id="43507-106">Örnek değerler</span><span class="sxs-lookup"><span data-stu-id="43507-106">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="43507-107">**alt ağlar**</span><span class="sxs-lookup"><span data-stu-id="43507-107">**subnets**</span></span> |<span data-ttu-id="43507-108">NSG uygulanan alt ağ kimlikleri listesi.</span><span class="sxs-lookup"><span data-stu-id="43507-108">List of subnet ids the NSG is applied to.</span></span> |<span data-ttu-id="43507-109">/Subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/Subnets/FrontEnd</span><span class="sxs-lookup"><span data-stu-id="43507-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span></span> |
| <span data-ttu-id="43507-110">**securityRules**</span><span class="sxs-lookup"><span data-stu-id="43507-110">**securityRules**</span></span> |<span data-ttu-id="43507-111">NSG güvenlik kuralları listesi</span><span class="sxs-lookup"><span data-stu-id="43507-111">List of security rules that make up the NSG</span></span> |<span data-ttu-id="43507-112">Bkz: [güvenlik kuralı](#Security-rule) aşağıda</span><span class="sxs-lookup"><span data-stu-id="43507-112">See [Security rule](#Security-rule) below</span></span> |
| <span data-ttu-id="43507-113">**defaultSecurityRules**</span><span class="sxs-lookup"><span data-stu-id="43507-113">**defaultSecurityRules**</span></span> |<span data-ttu-id="43507-114">Varsayılan güvenlik kuralları her NSG'de mevcut listesi</span><span class="sxs-lookup"><span data-stu-id="43507-114">List of default security rules present in every NSG</span></span> |<span data-ttu-id="43507-115">Bkz: [varsayılan güvenlik kuralları](#Default-security-rules) aşağıda</span><span class="sxs-lookup"><span data-stu-id="43507-115">See [Default security rules](#Default-security-rules) below</span></span> |

* <span data-ttu-id="43507-116">**Güvenlik kuralı** -bir NSG tanımlanan birden çok güvenlik kuralları sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="43507-116">**Security rule** - An NSG can have multiple security rules defined.</span></span> <span data-ttu-id="43507-117">Her bir kural izin verebilir veya trafiği farklı türlerde reddet.</span><span class="sxs-lookup"><span data-stu-id="43507-117">Each rule can allow or deny different types of traffic.</span></span>

### <a name="security-rule"></a><span data-ttu-id="43507-118">Güvenlik kuralı</span><span class="sxs-lookup"><span data-stu-id="43507-118">Security rule</span></span>
<span data-ttu-id="43507-119">Güvenlik kuralı özelliklerini içeren bir NSG bir alt kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="43507-119">A security rule is a child resource of an NSG containing the properties below.</span></span>

| <span data-ttu-id="43507-120">Özellik</span><span class="sxs-lookup"><span data-stu-id="43507-120">Property</span></span> | <span data-ttu-id="43507-121">Açıklama</span><span class="sxs-lookup"><span data-stu-id="43507-121">Description</span></span> | <span data-ttu-id="43507-122">Örnek değerler</span><span class="sxs-lookup"><span data-stu-id="43507-122">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="43507-123">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="43507-123">**description**</span></span> |<span data-ttu-id="43507-124">Kural için açıklama</span><span class="sxs-lookup"><span data-stu-id="43507-124">Description for the rule</span></span> |<span data-ttu-id="43507-125">Alt ağda X tüm VM'ler için gelen trafiğe izin ver</span><span class="sxs-lookup"><span data-stu-id="43507-125">Allow inbound traffic for all VMs in subnet X</span></span> |
| <span data-ttu-id="43507-126">**Protokolü**</span><span class="sxs-lookup"><span data-stu-id="43507-126">**protocol**</span></span> |<span data-ttu-id="43507-127">Kural ile eşleştirilecek protokol</span><span class="sxs-lookup"><span data-stu-id="43507-127">Protocol to match for the rule</span></span> |<span data-ttu-id="43507-128">TCP, UDP veya *</span><span class="sxs-lookup"><span data-stu-id="43507-128">TCP, UDP, or *</span></span> |
| <span data-ttu-id="43507-129">**sourcePortRange**</span><span class="sxs-lookup"><span data-stu-id="43507-129">**sourcePortRange**</span></span> |<span data-ttu-id="43507-130">Kural ile eşleştirilecek kaynak bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="43507-130">Source port range to match for the rule</span></span> |<span data-ttu-id="43507-131">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="43507-131">80, 100-200, *</span></span> |
| <span data-ttu-id="43507-132">**destinationPortRange**</span><span class="sxs-lookup"><span data-stu-id="43507-132">**destinationPortRange**</span></span> |<span data-ttu-id="43507-133">Kural ile eşleştirilecek hedef bağlantı noktası aralığı</span><span class="sxs-lookup"><span data-stu-id="43507-133">Destination port range to match for the rule</span></span> |<span data-ttu-id="43507-134">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="43507-134">80, 100-200, *</span></span> |
| <span data-ttu-id="43507-135">**sourceAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="43507-135">**sourceAddressPrefix**</span></span> |<span data-ttu-id="43507-136">Kural ile eşleştirilecek kaynak adres ön eki</span><span class="sxs-lookup"><span data-stu-id="43507-136">Source address prefix to match for the rule</span></span> |<span data-ttu-id="43507-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="43507-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="43507-138">**destinationAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="43507-138">**destinationAddressPrefix**</span></span> |<span data-ttu-id="43507-139">Kural ile eşleştirilecek hedef adres ön eki</span><span class="sxs-lookup"><span data-stu-id="43507-139">Destination address prefix to match for the rule</span></span> |<span data-ttu-id="43507-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="43507-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="43507-141">**yönü**</span><span class="sxs-lookup"><span data-stu-id="43507-141">**direction**</span></span> |<span data-ttu-id="43507-142">Kural için eşleştirilecek trafik yönü</span><span class="sxs-lookup"><span data-stu-id="43507-142">Direction of traffic to match for the rule</span></span> |<span data-ttu-id="43507-143">gelen veya giden</span><span class="sxs-lookup"><span data-stu-id="43507-143">inbound or outbound</span></span> |
| <span data-ttu-id="43507-144">**öncelik**</span><span class="sxs-lookup"><span data-stu-id="43507-144">**priority**</span></span> |<span data-ttu-id="43507-145">Kural için öncelik.</span><span class="sxs-lookup"><span data-stu-id="43507-145">Priority for the rule.</span></span> <span data-ttu-id="43507-146">Kurallar öncelik sırasına göre denetlenir, bir kural uygulandığı zaman başka hiçbir kural eşleştirme için test edilmez.</span><span class="sxs-lookup"><span data-stu-id="43507-146">Rules are checked int he order of priority, once a rule applies, no more rules are tested for matching.</span></span> |<span data-ttu-id="43507-147">10, 100, 65000</span><span class="sxs-lookup"><span data-stu-id="43507-147">10, 100, 65000</span></span> |
| <span data-ttu-id="43507-148">**erişim**</span><span class="sxs-lookup"><span data-stu-id="43507-148">**access**</span></span> |<span data-ttu-id="43507-149">Kuralın eşleşmesi durumunda uygulanacak erişim türü</span><span class="sxs-lookup"><span data-stu-id="43507-149">Type of access to apply if the rule matches</span></span> |<span data-ttu-id="43507-150">izin ver veya reddet</span><span class="sxs-lookup"><span data-stu-id="43507-150">allow or deny</span></span> |

<span data-ttu-id="43507-151">JSON biçiminde NSG örneği:</span><span class="sxs-lookup"><span data-stu-id="43507-151">Sample NSG in JSON format:</span></span>

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

### <a name="default-security-rules"></a><span data-ttu-id="43507-152">Varsayılan güvenlik kuralları</span><span class="sxs-lookup"><span data-stu-id="43507-152">Default security rules</span></span>

<span data-ttu-id="43507-153">Varsayılan güvenlik kuralları güvenlik kurallarında kullanılabilir aynı özelliklere sahip.</span><span class="sxs-lookup"><span data-stu-id="43507-153">Default security rules have the same properties available in security rules.</span></span> <span data-ttu-id="43507-154">Nsg'ler uygulanmış olan kaynaklar arasındaki temel bağlantı sağlamak için mevcut.</span><span class="sxs-lookup"><span data-stu-id="43507-154">They exist to provide basic connectivity between resources that have NSGs applied to them.</span></span> <span data-ttu-id="43507-155">Hangi bildiğinizden emin olun [güvenlik kuralları varsayılan](../articles/virtual-network/virtual-networks-nsg.md#default-rules) yok.</span><span class="sxs-lookup"><span data-stu-id="43507-155">Make sure you know which [default security rules](../articles/virtual-network/virtual-networks-nsg.md#default-rules) exist.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="43507-156">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="43507-156">Additional resources</span></span>
* <span data-ttu-id="43507-157">Hakkında daha fazla bilgi almak [Nsg'ler](../articles/virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="43507-157">Get more information about [NSGs](../articles/virtual-network/virtual-networks-nsg.md).</span></span>
* <span data-ttu-id="43507-158">Okuma [REST API başvuru belgeleri](https://msdn.microsoft.com/library/azure/mt163615.aspx) Nsg'ler için.</span><span class="sxs-lookup"><span data-stu-id="43507-158">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163615.aspx) for NSGs.</span></span>
* <span data-ttu-id="43507-159">Okuma [REST API başvuru belgeleri](https://msdn.microsoft.com/library/azure/mt163580.aspx) güvenlik kuralları için.</span><span class="sxs-lookup"><span data-stu-id="43507-159">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163580.aspx) for security rules.</span></span>
