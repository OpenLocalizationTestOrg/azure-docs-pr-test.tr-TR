## <a name="public-ip-address"></a><span data-ttu-id="ad811-101">Genel IP adresi</span><span class="sxs-lookup"><span data-stu-id="ad811-101">Public IP address</span></span>
<span data-ttu-id="ad811-102">Ya da IP adresi bir ayrılmış veya dinamik Internet'e yönelik genel bir IP adresi kaynağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="ad811-102">A public IP address resource provides either a reserved or dynamic Internet facing IP address.</span></span> <span data-ttu-id="ad811-103">Tek başına nesne olarak genel bir IP adresi oluşturabilseniz de tooassociate gerekir, tooanother nesne tooactually hello adresi kullanın.</span><span class="sxs-lookup"><span data-stu-id="ad811-103">Although you can create a public IP address as a stand alone object, you need tooassociate it tooanother object tooactually use hello address.</span></span> <span data-ttu-id="ad811-104">Bir ortak IP adresi tooa yük dengeleyici, uygulama ağ geçidini veya bir NIC tooprovide Internet erişimi toothose kaynaklarını ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad811-104">You can associate a public IP address tooa load balancer, application  gateway, or a NIC tooprovide Internet access toothose resources.</span></span>  

| <span data-ttu-id="ad811-105">Özellik</span><span class="sxs-lookup"><span data-stu-id="ad811-105">Property</span></span> | <span data-ttu-id="ad811-106">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ad811-106">Description</span></span> | <span data-ttu-id="ad811-107">Örnek değerler</span><span class="sxs-lookup"><span data-stu-id="ad811-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ad811-108">**Publicıpallocationmethod**</span><span class="sxs-lookup"><span data-stu-id="ad811-108">**publicIPAllocationMethod**</span></span> |<span data-ttu-id="ad811-109">Başlangıç IP adresi ise tanımlar *statik* veya *dinamik*.</span><span class="sxs-lookup"><span data-stu-id="ad811-109">Defines if hello IP address is *static* or *dynamic*.</span></span> |<span data-ttu-id="ad811-110">statik, dinamik</span><span class="sxs-lookup"><span data-stu-id="ad811-110">static, dynamic</span></span> |
| <span data-ttu-id="ad811-111">**idleTimeoutInMinutes**</span><span class="sxs-lookup"><span data-stu-id="ad811-111">**idleTimeoutInMinutes**</span></span> |<span data-ttu-id="ad811-112">Merhaba boşta kalma zaman aşımı, 4 dakikaya varsayılan değerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ad811-112">Defines hello idle time out, with a default value of 4 minutes.</span></span> <span data-ttu-id="ad811-113">Belirli bir oturum için daha fazla hiçbir paket alındığında, bu süre içinde hello oturum sonlandırıldı.</span><span class="sxs-lookup"><span data-stu-id="ad811-113">If no more packets for a given session is received within this time, hello session is terminated.</span></span> |<span data-ttu-id="ad811-114">4 ile 30 arasında herhangi bir değer</span><span class="sxs-lookup"><span data-stu-id="ad811-114">any value between 4 and 30</span></span> |
| <span data-ttu-id="ad811-115">**IP adresi**</span><span class="sxs-lookup"><span data-stu-id="ad811-115">**ipAddress**</span></span> |<span data-ttu-id="ad811-116">IP adresi tooobject atanır.</span><span class="sxs-lookup"><span data-stu-id="ad811-116">IP address assigned tooobject.</span></span> <span data-ttu-id="ad811-117">Bu salt okunur bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="ad811-117">This is a read-only property.</span></span> |<span data-ttu-id="ad811-118">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="ad811-118">104.42.233.77</span></span> |

### <a name="dns-settings"></a><span data-ttu-id="ad811-119">DNS ayarları</span><span class="sxs-lookup"><span data-stu-id="ad811-119">DNS settings</span></span>
<span data-ttu-id="ad811-120">Genel IP adresine sahip adlı bir alt nesne **dnsSettings** aşağıdaki özelliklere hello içeren:</span><span class="sxs-lookup"><span data-stu-id="ad811-120">Public IP addresses have a child object named **dnsSettings** containing hello following properties:</span></span>

| <span data-ttu-id="ad811-121">Özellik</span><span class="sxs-lookup"><span data-stu-id="ad811-121">Property</span></span> | <span data-ttu-id="ad811-122">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ad811-122">Description</span></span> | <span data-ttu-id="ad811-123">Örnek değerler</span><span class="sxs-lookup"><span data-stu-id="ad811-123">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ad811-124">**domainNameLabel**</span><span class="sxs-lookup"><span data-stu-id="ad811-124">**domainNameLabel**</span></span> |<span data-ttu-id="ad811-125">Adlı ana bilgisayar adı çözümlemesi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ad811-125">Host named used for name resolution.</span></span> |<span data-ttu-id="ad811-126">www, ftp, vm1</span><span class="sxs-lookup"><span data-stu-id="ad811-126">www, ftp, vm1</span></span> |
| <span data-ttu-id="ad811-127">**FQDN**</span><span class="sxs-lookup"><span data-stu-id="ad811-127">**fqdn**</span></span> |<span data-ttu-id="ad811-128">Merhaba genel IP için tam adı.</span><span class="sxs-lookup"><span data-stu-id="ad811-128">Fully qualified name for hello public IP.</span></span> |<span data-ttu-id="ad811-129">www.westus.cloudapp.Azure.com</span><span class="sxs-lookup"><span data-stu-id="ad811-129">www.westus.cloudapp.azure.com</span></span> |
| <span data-ttu-id="ad811-130">**reverseFqdn**</span><span class="sxs-lookup"><span data-stu-id="ad811-130">**reverseFqdn**</span></span> |<span data-ttu-id="ad811-131">Toohello IP adresine çözümler ve DNS PTR kaydı olarak kaydedilmiş tam etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="ad811-131">Fully qualified domain name that resolves toohello IP address and is registered in DNS as a PTR record.</span></span> |<span data-ttu-id="ad811-132">www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="ad811-132">www.contoso.com.</span></span> |

<span data-ttu-id="ad811-133">Örnek genel IP adresi JSON biçiminde:</span><span class="sxs-lookup"><span data-stu-id="ad811-133">Sample public IP address in JSON format:</span></span>

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

### <a name="additional-resources"></a><span data-ttu-id="ad811-134">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ad811-134">Additional resources</span></span>
* <span data-ttu-id="ad811-135">Hakkında daha fazla bilgi almak [genel IP adresleri](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="ad811-135">Get more information about [public IP addresses](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span></span>
* <span data-ttu-id="ad811-136">Hakkında bilgi edinin [örnek düzeyinde ortak IP adresleri](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="ad811-136">Learn about [instance level public IP addresses](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span></span>
* <span data-ttu-id="ad811-137">Okuma hello [REST API başvuru belgeleri](https://msdn.microsoft.com/library/azure/mt163638.aspx) için ortak IP adresleri.</span><span class="sxs-lookup"><span data-stu-id="ad811-137">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163638.aspx) for public IP addresses.</span></span>

