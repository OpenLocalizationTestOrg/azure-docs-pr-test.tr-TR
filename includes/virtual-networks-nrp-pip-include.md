## <a name="public-ip-address"></a><span data-ttu-id="a7ca2-101">Genel IP adresi</span><span class="sxs-lookup"><span data-stu-id="a7ca2-101">Public IP address</span></span>
<span data-ttu-id="a7ca2-102">Ya da IP adresi bir ayrılmış veya dinamik Internet'e yönelik genel bir IP adresi kaynağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="a7ca2-102">A public IP address resource provides either a reserved or dynamic Internet facing IP address.</span></span> <span data-ttu-id="a7ca2-103">Tek başına nesne olarak genel bir IP adresi oluşturabilirsiniz, ancak gerçekte adresini kullanmak için başka bir nesneye ilişkilendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7ca2-103">Although you can create a public IP address as a stand alone object, you need to associate it to another object to actually use the address.</span></span> <span data-ttu-id="a7ca2-104">Bir ortak IP adresi bir yük dengeleyici, uygulama ağ geçidi ya da bu kaynakları Internet erişimi sağlamak için bir NIC ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7ca2-104">You can associate a public IP address to a load balancer, application  gateway, or a NIC to provide Internet access to those resources.</span></span>  

| <span data-ttu-id="a7ca2-105">Özellik</span><span class="sxs-lookup"><span data-stu-id="a7ca2-105">Property</span></span> | <span data-ttu-id="a7ca2-106">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a7ca2-106">Description</span></span> | <span data-ttu-id="a7ca2-107">Örnek değerler</span><span class="sxs-lookup"><span data-stu-id="a7ca2-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a7ca2-108">**Publicıpallocationmethod**</span><span class="sxs-lookup"><span data-stu-id="a7ca2-108">**publicIPAllocationMethod**</span></span> |<span data-ttu-id="a7ca2-109">IP adresi ise tanımlar *statik* veya *dinamik*.</span><span class="sxs-lookup"><span data-stu-id="a7ca2-109">Defines if the IP address is *static* or *dynamic*.</span></span> |<span data-ttu-id="a7ca2-110">statik, dinamik</span><span class="sxs-lookup"><span data-stu-id="a7ca2-110">static, dynamic</span></span> |
| <span data-ttu-id="a7ca2-111">**idleTimeoutInMinutes**</span><span class="sxs-lookup"><span data-stu-id="a7ca2-111">**idleTimeoutInMinutes**</span></span> |<span data-ttu-id="a7ca2-112">4 dakikalık varsayılan bir değerle boşta kalma zaman aşımı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a7ca2-112">Defines the idle time out, with a default value of 4 minutes.</span></span> <span data-ttu-id="a7ca2-113">Belirli bir oturum için daha fazla hiçbir paket alındığında bu süre içinde oturum sonlandırılır.</span><span class="sxs-lookup"><span data-stu-id="a7ca2-113">If no more packets for a given session is received within this time, the session is terminated.</span></span> |<span data-ttu-id="a7ca2-114">4 ile 30 arasında herhangi bir değer</span><span class="sxs-lookup"><span data-stu-id="a7ca2-114">any value between 4 and 30</span></span> |
| <span data-ttu-id="a7ca2-115">**IP adresi**</span><span class="sxs-lookup"><span data-stu-id="a7ca2-115">**ipAddress**</span></span> |<span data-ttu-id="a7ca2-116">Nesne için atanan IP adresi.</span><span class="sxs-lookup"><span data-stu-id="a7ca2-116">IP address assigned to object.</span></span> <span data-ttu-id="a7ca2-117">Bu salt okunur bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="a7ca2-117">This is a read-only property.</span></span> |<span data-ttu-id="a7ca2-118">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="a7ca2-118">104.42.233.77</span></span> |

### <a name="dns-settings"></a><span data-ttu-id="a7ca2-119">DNS ayarları</span><span class="sxs-lookup"><span data-stu-id="a7ca2-119">DNS settings</span></span>
<span data-ttu-id="a7ca2-120">Genel IP adresine sahip adlı bir alt nesne **dnsSettings** aşağıdaki özellikleri içeren:</span><span class="sxs-lookup"><span data-stu-id="a7ca2-120">Public IP addresses have a child object named **dnsSettings** containing the following properties:</span></span>

| <span data-ttu-id="a7ca2-121">Özellik</span><span class="sxs-lookup"><span data-stu-id="a7ca2-121">Property</span></span> | <span data-ttu-id="a7ca2-122">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a7ca2-122">Description</span></span> | <span data-ttu-id="a7ca2-123">Örnek değerler</span><span class="sxs-lookup"><span data-stu-id="a7ca2-123">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a7ca2-124">**domainNameLabel**</span><span class="sxs-lookup"><span data-stu-id="a7ca2-124">**domainNameLabel**</span></span> |<span data-ttu-id="a7ca2-125">Adlı ana bilgisayar adı çözümlemesi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a7ca2-125">Host named used for name resolution.</span></span> |<span data-ttu-id="a7ca2-126">www, ftp, vm1</span><span class="sxs-lookup"><span data-stu-id="a7ca2-126">www, ftp, vm1</span></span> |
| <span data-ttu-id="a7ca2-127">**FQDN**</span><span class="sxs-lookup"><span data-stu-id="a7ca2-127">**fqdn**</span></span> |<span data-ttu-id="a7ca2-128">Genel IP için tam adı.</span><span class="sxs-lookup"><span data-stu-id="a7ca2-128">Fully qualified name for the public IP.</span></span> |<span data-ttu-id="a7ca2-129">www.westus.cloudapp.Azure.com</span><span class="sxs-lookup"><span data-stu-id="a7ca2-129">www.westus.cloudapp.azure.com</span></span> |
| <span data-ttu-id="a7ca2-130">**reverseFqdn**</span><span class="sxs-lookup"><span data-stu-id="a7ca2-130">**reverseFqdn**</span></span> |<span data-ttu-id="a7ca2-131">IP adresine çözümler ve DNS PTR kaydı olarak kaydedilmiş tam etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="a7ca2-131">Fully qualified domain name that resolves to the IP address and is registered in DNS as a PTR record.</span></span> |<span data-ttu-id="a7ca2-132">www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="a7ca2-132">www.contoso.com.</span></span> |

<span data-ttu-id="a7ca2-133">Örnek genel IP adresi JSON biçiminde:</span><span class="sxs-lookup"><span data-stu-id="a7ca2-133">Sample public IP address in JSON format:</span></span>

    {
       "name": "PIP01",
       "location": "North US",
       "tags": { "key": "value" },
       "properties": {
          "publicIPAllocationMethod": "Static",
          "idleTimeoutInMinutes": 4,
          "ipAddress": "104.42.233.77",
          "dnsSettings": {
             "domainNameLabel": "mylabel",
             "fqdn": "mylabel.westus.cloudapp.azure.com",
             "reverseFqdn": "contoso.com."
          }
       }
    } 

### <a name="additional-resources"></a><span data-ttu-id="a7ca2-134">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a7ca2-134">Additional resources</span></span>
* <span data-ttu-id="a7ca2-135">Hakkında daha fazla bilgi almak [genel IP adresleri](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="a7ca2-135">Get more information about [public IP addresses](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span></span>
* <span data-ttu-id="a7ca2-136">Hakkında bilgi edinin [örnek düzeyinde ortak IP adresleri](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="a7ca2-136">Learn about [instance level public IP addresses](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span></span>
* <span data-ttu-id="a7ca2-137">Okuma [REST API başvuru belgeleri](https://msdn.microsoft.com/library/azure/mt163638.aspx) için ortak IP adresleri.</span><span class="sxs-lookup"><span data-stu-id="a7ca2-137">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163638.aspx) for public IP addresses.</span></span>

