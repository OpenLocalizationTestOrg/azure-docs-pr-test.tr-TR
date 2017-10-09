## <a name="traffic-manager-profile"></a><span data-ttu-id="b6055-101">Trafik Yöneticisi profili</span><span class="sxs-lookup"><span data-stu-id="b6055-101">Traffic Manager Profile</span></span>
<span data-ttu-id="b6055-102">Trafik Yöneticisi ve onun alt uç nokta kaynağının DNS yönlendirme tooendpoints Azure ve Azure dışında etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="b6055-102">Traffic manager and its child endpoint resource enable DNS routing tooendpoints in Azure and outside of Azure.</span></span> <span data-ttu-id="b6055-103">Bu tür trafik dağıtım yönlendirme ilkesi yöntemler tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="b6055-103">Such traffic distribution is governed by routing  policy methods.</span></span> <span data-ttu-id="b6055-104">Trafik Yöneticisi uç noktası durumu toobe izlenen ve uygun şekilde yolu saptırabilir trafiği bir uç nokta hello durumunu temel de sağlar.</span><span class="sxs-lookup"><span data-stu-id="b6055-104">Traffic manager also allows endpoint health toobe monitored, and traffic diverted appropriately based on hello health of an endpoint.</span></span> 

| <span data-ttu-id="b6055-105">Özellik</span><span class="sxs-lookup"><span data-stu-id="b6055-105">Property</span></span> | <span data-ttu-id="b6055-106">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b6055-106">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b6055-107">**trafficRoutingMethod**</span><span class="sxs-lookup"><span data-stu-id="b6055-107">**trafficRoutingMethod**</span></span> |<span data-ttu-id="b6055-108">Olası değerler şunlardır: *performans*, *Weighted*, ve *önceliği*</span><span class="sxs-lookup"><span data-stu-id="b6055-108">possible values are *Performance*, *Weighted*, and *Priority*</span></span> |
| <span data-ttu-id="b6055-109">**dnsConfig**</span><span class="sxs-lookup"><span data-stu-id="b6055-109">**dnsConfig**</span></span> |<span data-ttu-id="b6055-110">Hello profili için FQDN</span><span class="sxs-lookup"><span data-stu-id="b6055-110">FQDN for hello profile</span></span> |
| <span data-ttu-id="b6055-111">**Protokol**</span><span class="sxs-lookup"><span data-stu-id="b6055-111">**Protocol**</span></span> |<span data-ttu-id="b6055-112">Olası değerler şunlardır: İzleme Protokolü, *HTTP* ve *HTTPS*</span><span class="sxs-lookup"><span data-stu-id="b6055-112">monitoring protocol, possible values are *HTTP* and *HTTPS*</span></span> |
| <span data-ttu-id="b6055-113">**Bağlantı Noktası**</span><span class="sxs-lookup"><span data-stu-id="b6055-113">**Port**</span></span> |<span data-ttu-id="b6055-114">bağlantı noktası izlemesi</span><span class="sxs-lookup"><span data-stu-id="b6055-114">monitoring port</span></span> |
| <span data-ttu-id="b6055-115">**Path**</span><span class="sxs-lookup"><span data-stu-id="b6055-115">**Path**</span></span> |<span data-ttu-id="b6055-116">izleme yolu</span><span class="sxs-lookup"><span data-stu-id="b6055-116">monitoring path</span></span> |
| <span data-ttu-id="b6055-117">**Uç noktaları**</span><span class="sxs-lookup"><span data-stu-id="b6055-117">**Endpoints**</span></span> |<span data-ttu-id="b6055-118">uç nokta kaynaklar için kapsayıcı</span><span class="sxs-lookup"><span data-stu-id="b6055-118">container for endpoint resources</span></span> |

### <a name="endpoint"></a><span data-ttu-id="b6055-119">Uç Nokta</span><span class="sxs-lookup"><span data-stu-id="b6055-119">Endpoint</span></span>
<span data-ttu-id="b6055-120">Bir uç nokta Traffic Manager profilinin bir alt kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="b6055-120">An endpoint is a child resource of a Traffic Manager Profile.</span></span> <span data-ttu-id="b6055-121">Web uç noktası toowhich kullanıcı trafiğinin hello trafik Yöneticisi profili kaynak yapılandırılmış hello ilkesine dayanarak dağıtılmış veya bir hizmet temsil eder.</span><span class="sxs-lookup"><span data-stu-id="b6055-121">It represents a service or web endpoint toowhich user traffic is distributed based on hello configured policy in hello Traffic Manager Profile resource.</span></span> 

| <span data-ttu-id="b6055-122">Özellik</span><span class="sxs-lookup"><span data-stu-id="b6055-122">Property</span></span> | <span data-ttu-id="b6055-123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b6055-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b6055-124">**Tür**</span><span class="sxs-lookup"><span data-stu-id="b6055-124">**Type**</span></span> |<span data-ttu-id="b6055-125">Merhaba türü hello uç noktasını, olası değerler şunlardır: *Azure uç noktası*, *dış uç noktası*, ve *iç içe geçmiş uç noktası*</span><span class="sxs-lookup"><span data-stu-id="b6055-125">hello type of hello endpoint, possible values are *Azure End point*, *External Endpoint*, and  *Nested Endpoint*</span></span> |
| <span data-ttu-id="b6055-126">**uç noktası Targetresourceıd**</span><span class="sxs-lookup"><span data-stu-id="b6055-126">**targetResourceId**</span></span> |<span data-ttu-id="b6055-127">bir hizmeti veya web uç noktası genel IP adresi.</span><span class="sxs-lookup"><span data-stu-id="b6055-127">public IP address of a service or web endpoint.</span></span> <span data-ttu-id="b6055-128">Bu, bir Azure ya da dış uç noktası olabilir.</span><span class="sxs-lookup"><span data-stu-id="b6055-128">This can be an Azure or external endpoint.</span></span> |
| <span data-ttu-id="b6055-129">**Ağırlık**</span><span class="sxs-lookup"><span data-stu-id="b6055-129">**Weight**</span></span> |<span data-ttu-id="b6055-130">uç nokta ağırlığı trafiği yönetiminde kullanılan.</span><span class="sxs-lookup"><span data-stu-id="b6055-130">endpoint weight used in traffic management.</span></span> |
| <span data-ttu-id="b6055-131">**Öncelik**</span><span class="sxs-lookup"><span data-stu-id="b6055-131">**Priority**</span></span> |<span data-ttu-id="b6055-132">Merhaba uç noktası, kullanılan toodefine bir yük devretme işlemi önceliği</span><span class="sxs-lookup"><span data-stu-id="b6055-132">priority of hello endpoint, used toodefine a failover action</span></span> |

<span data-ttu-id="b6055-133">Trafik Yöneticisi'nin örnek Json biçiminde:</span><span class="sxs-lookup"><span data-stu-id="b6055-133">Sample of Traffic Manager in Json format:</span></span> 

        {
            "apiVersion": "[variables('tmApiVersion')]",
            "type": "Microsoft.Network/trafficManagerProfiles",
            "name": "VMEndpointExample",
            "location": "global",
            "dependsOn": [
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '0')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '1')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '2')]",
            ],
            "properties": {
                "profileStatus": "Enabled",
                "trafficRoutingMethod": "Weighted",
                "dnsConfig": {
                    "relativeName": "[parameters('dnsname')]",
                    "ttl": 30
                },
                "monitorConfig": {
                    "protocol": "http",
                    "port": 80,
                    "path": "/"
                },
                "endpoints": [
                    {
                        "name": "endpoint0",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 0))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint1",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 1))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint2",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 2))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    }
                ]
            }
        }


## <a name="additional-resources"></a><span data-ttu-id="b6055-134">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b6055-134">Additional resources</span></span>
<span data-ttu-id="b6055-135">Okuma [REST API belgeleri trafik Yöneticisi için](https://msdn.microsoft.com/library/azure/mt163664.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="b6055-135">Read [REST API documentation for Traffic Manager](https://msdn.microsoft.com/library/azure/mt163664.aspx) for more information.</span></span>

