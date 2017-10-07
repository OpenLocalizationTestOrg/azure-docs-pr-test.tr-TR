---
title: "Azure Ağ İzleyicisi ile ağ güvenlik grupları için aaaIntroduction tooflow günlüğü | Microsoft Docs"
description: "Bu sayfa toouse NSG akış Azure Ağ İzleyicisi özelliği nasıl günlüğe yazacağını açıklar"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 47d91341-16f1-45ac-85a5-e5a640f5d59e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: da85e946147b14717144cb47d1c742057c6dfa24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooflow-logging-for-network-security-groups"></a><span data-ttu-id="2c8cb-103">Ağ güvenlik grupları için giriş tooflow günlüğü</span><span class="sxs-lookup"><span data-stu-id="2c8cb-103">Introduction tooflow logging for Network Security Groups</span></span>

<span data-ttu-id="2c8cb-104">Ağ güvenlik grubu akış günlükleri, giriş ve çıkış IP trafiği bir ağ güvenlik grubu aracılığıyla tooview bilgilerini sağlayan Ağ İzleyicisi özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="2c8cb-104">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="2c8cb-105">Bu akış günlükleri json biçiminde yazılmıştır ve giden Göster gelen akış kuralı başına temelinde hello NIC hello akış uygular, 5-tanımlama grubu ilgili bilgilere hello akış (kaynak/hedef IP, kaynak/hedef bağlantı noktası, Protokolü) ve hello varsa trafiğine izin veya engellendi.</span><span class="sxs-lookup"><span data-stu-id="2c8cb-105">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

![Akış günlükleri genel bakış][1]

<span data-ttu-id="2c8cb-107">Hedef ağ güvenlik grupları akış günlükleri, ancak bunlar görüntülenmez aynı hello diğer günlükler hello.</span><span class="sxs-lookup"><span data-stu-id="2c8cb-107">While flow logs target Network Security Groups, they are not displayed hello same as hello other logs.</span></span> <span data-ttu-id="2c8cb-108">Akış günlükleri hello aşağıdaki örnekte gösterildiği gibi yalnızca bir depolama hesabı ve aşağıdaki hello günlük yolu içinde depolanır:</span><span class="sxs-lookup"><span data-stu-id="2c8cb-108">Flow logs are stored only within a storage account and following hello logging path as shown in hello following example:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="2c8cb-109">aynı hello diğer açtığında görülen bekletme ilkeleri uygulamak tooflow günlükleri.</span><span class="sxs-lookup"><span data-stu-id="2c8cb-109">hello same retention policies as seen on other logs apply tooflow logs.</span></span> <span data-ttu-id="2c8cb-110">Günlükleri 1 gün too365 gün ayarlanabilir bir bekletme ilkesi vardır.</span><span class="sxs-lookup"><span data-stu-id="2c8cb-110">Logs have a retention policy that can be set from 1 day too365 days.</span></span> <span data-ttu-id="2c8cb-111">Hello günlükleri sonsuza kadar bir bekletme ilkesi ayarlanmamışsa saklanır.</span><span class="sxs-lookup"><span data-stu-id="2c8cb-111">If a retention policy is not set, hello logs are maintained forever.</span></span>

## <a name="log-file"></a><span data-ttu-id="2c8cb-112">Günlük dosyası</span><span class="sxs-lookup"><span data-stu-id="2c8cb-112">Log file</span></span>

<span data-ttu-id="2c8cb-113">Akış günlükleri, birden çok özelliği vardır.</span><span class="sxs-lookup"><span data-stu-id="2c8cb-113">Flow logs have multiple properties.</span></span> <span data-ttu-id="2c8cb-114">Merhaba liste aşağıda hello NSG akış günlükte döndürülen hello özellikleri listesi verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="2c8cb-114">hello following list is a listing of hello properties that are returned within hello NSG flow log:</span></span>

* <span data-ttu-id="2c8cb-115">**zaman** - hello olayın günlüğe yazıldığı zaman zaman</span><span class="sxs-lookup"><span data-stu-id="2c8cb-115">**time** - Time when hello event was logged</span></span>
* <span data-ttu-id="2c8cb-116">**SistemKimliği** -ağ güvenlik grubu kaynak kimliği</span><span class="sxs-lookup"><span data-stu-id="2c8cb-116">**systemId** - Network Security Group resource Id.</span></span>
* <span data-ttu-id="2c8cb-117">**Kategori** -hello kategorisi başlangıç olayı, bu her zaman olmaya NetworkSecurityGroupFlowEvent</span><span class="sxs-lookup"><span data-stu-id="2c8cb-117">**category** - hello category of hello event, this is always be NetworkSecurityGroupFlowEvent</span></span>
* <span data-ttu-id="2c8cb-118">**ResourceId** -kaynak hello NSG kimliğini hello</span><span class="sxs-lookup"><span data-stu-id="2c8cb-118">**resourceid** - hello resource Id of hello NSG</span></span>
* <span data-ttu-id="2c8cb-119">**operationName** -her zaman NetworkSecurityGroupFlowEvents</span><span class="sxs-lookup"><span data-stu-id="2c8cb-119">**operationName** - Always NetworkSecurityGroupFlowEvents</span></span>
* <span data-ttu-id="2c8cb-120">**Özellikler** -hello akışının özellikleri koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="2c8cb-120">**properties** - A collection of properties of hello flow</span></span>
    * <span data-ttu-id="2c8cb-121">**Sürüm** -hello akış günlüğü olay şeması sürüm numarası</span><span class="sxs-lookup"><span data-stu-id="2c8cb-121">**Version** - Version number of hello Flow Log event schema</span></span>
    * <span data-ttu-id="2c8cb-122">**Akışlar** -akışları koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="2c8cb-122">**flows** - A collection of flows.</span></span> <span data-ttu-id="2c8cb-123">Bu özelliği farklı kurallar için birden fazla varlık içeriyor</span><span class="sxs-lookup"><span data-stu-id="2c8cb-123">This property has multiple entries for different rules</span></span>
        * <span data-ttu-id="2c8cb-124">**Kural** -hangi Merhaba akışları listelenen kuralı</span><span class="sxs-lookup"><span data-stu-id="2c8cb-124">**rule** - Rule for which hello flows are listed</span></span>
            * <span data-ttu-id="2c8cb-125">**Akışlar** -akışları koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="2c8cb-125">**flows** - a collection of flows</span></span>
                * <span data-ttu-id="2c8cb-126">**Mac** -hello NIC hello burada hello akış toplandı VM için MAC adresini hello</span><span class="sxs-lookup"><span data-stu-id="2c8cb-126">**mac** - hello MAC address of hello NIC for hello VM where hello flow was collected</span></span>
                * <span data-ttu-id="2c8cb-127">**flowTuples** -virgülle ayrılmış biçimde hello akış tanımlama grubu için birden çok özellik içeren bir dize</span><span class="sxs-lookup"><span data-stu-id="2c8cb-127">**flowTuples** - A string that contains multiple properties for hello flow tuple in comma-separated format</span></span>
                    * <span data-ttu-id="2c8cb-128">**Zaman damgası** -UNIX dönem biçiminde hello akış oluştuğu sırada bu hello zaman damgası değerdir</span><span class="sxs-lookup"><span data-stu-id="2c8cb-128">**Time Stamp** - This value is hello time stamp of when hello flow occurred in UNIX EPOCH format</span></span>
                    * <span data-ttu-id="2c8cb-129">**Kaynak IP** - hello IP kaynağı</span><span class="sxs-lookup"><span data-stu-id="2c8cb-129">**Source IP** - hello source IP</span></span>
                    * <span data-ttu-id="2c8cb-130">**Hedef IP** -hedef IP hello</span><span class="sxs-lookup"><span data-stu-id="2c8cb-130">**Destination IP** - hello destination IP</span></span>
                    * <span data-ttu-id="2c8cb-131">**Kaynak bağlantı noktası** - hello kaynak bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="2c8cb-131">**Source Port** - hello source port</span></span>
                    * <span data-ttu-id="2c8cb-132">**Hedef bağlantı noktası** -hedef bağlantı noktası hello</span><span class="sxs-lookup"><span data-stu-id="2c8cb-132">**Destination Port** - hello destination Port</span></span>
                    * <span data-ttu-id="2c8cb-133">**Protokol** -hello hello akışının protokolü.</span><span class="sxs-lookup"><span data-stu-id="2c8cb-133">**Protocol** - hello protocol of hello flow.</span></span> <span data-ttu-id="2c8cb-134">Geçerli değerler **T** TCP için ve **U** UDP için</span><span class="sxs-lookup"><span data-stu-id="2c8cb-134">Valid values are **T** for TCP and **U** for UDP</span></span>
                    * <span data-ttu-id="2c8cb-135">**Trafik akışı** -hello hello trafik akış yönü.</span><span class="sxs-lookup"><span data-stu-id="2c8cb-135">**Traffic Flow** - hello direction of hello traffic flow.</span></span> <span data-ttu-id="2c8cb-136">Geçerli değerler **ı** gelen ve **O** için giden.</span><span class="sxs-lookup"><span data-stu-id="2c8cb-136">Valid values are **I** for inbound and **O** for outbound.</span></span>
                    * <span data-ttu-id="2c8cb-137">**Trafik** - trafiğine izin verilen veya reddedilen olup olmadığını.</span><span class="sxs-lookup"><span data-stu-id="2c8cb-137">**Traffic** - Whether traffic was allowed or denied.</span></span> <span data-ttu-id="2c8cb-138">Geçerli değerler **A** izin ve **D** reddedildi için.</span><span class="sxs-lookup"><span data-stu-id="2c8cb-138">Valid values are **A** for allowed and **D** for denied.</span></span>


<span data-ttu-id="2c8cb-139">Merhaba, akış günlüğü örneği verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="2c8cb-139">hello following is an example of a Flow log.</span></span> <span data-ttu-id="2c8cb-140">Gördüğünüz gibi hello önceki bölümde açıklanan hello özellik listesi izleyin birden çok kayıt vardır.</span><span class="sxs-lookup"><span data-stu-id="2c8cb-140">As you can see there are multiple records that follow hello property list described in hello preceding section.</span></span> 

> [!NOTE]
> <span data-ttu-id="2c8cb-141">Merhaba flowTuples özelliği virgülle ayrılmış bir liste değerler.</span><span class="sxs-lookup"><span data-stu-id="2c8cb-141">Values in hello flowTuples property are a comma-separated list.</span></span>
 
```json
{
    "records": 
    [
        
        {
             "time": "2017-02-16T22:00:32.8950000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282421,42.119.146.95,10.1.0.4,51529,5358,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282370,163.28.66.17,10.1.0.4,61771,3389,T,I,A","1487282393,5.39.218.34,10.1.0.4,58596,3389,T,I,A","1487282393,91.224.160.154,10.1.0.4,61540,3389,T,I,A","1487282423,13.76.89.229,10.1.0.4,53163,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:01:32.8960000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282481,195.78.210.194,10.1.0.4,53,1732,U,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282435,61.129.251.68,10.1.0.4,57776,3389,T,I,A","1487282454,84.25.174.170,10.1.0.4,59085,3389,T,I,A","1487282477,77.68.9.50,10.1.0.4,65078,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:02:32.9040000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282492,175.182.69.29,10.1.0.4,28918,5358,T,I,D","1487282505,71.6.216.55,10.1.0.4,8080,8080,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282512,91.224.160.154,10.1.0.4,59046,3389,T,I,A"]}]}]}
        }
        ,
        ...
```

## <a name="next-steps"></a><span data-ttu-id="2c8cb-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2c8cb-142">Next steps</span></span>

<span data-ttu-id="2c8cb-143">Tooenable akış ziyaret ederek nasıl günlüğe yazacağını öğrenin [günlüğü etkinleştirme akışı](network-watcher-nsg-flow-logging-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2c8cb-143">Learn how tooenable Flow logs by visiting [Enabling Flow logging](network-watcher-nsg-flow-logging-portal.md).</span></span>

<span data-ttu-id="2c8cb-144">NSG oturum açma hakkında bilgi edinin ziyaret ederek [günlük analizi için ağ güvenlik grupları (Nsg'ler)](../virtual-network/virtual-network-nsg-manage-log.md).</span><span class="sxs-lookup"><span data-stu-id="2c8cb-144">Learn about NSG logging by visiting [Log analytics for network security groups (NSGs)](../virtual-network/virtual-network-nsg-manage-log.md).</span></span>

<span data-ttu-id="2c8cb-145">Trafik izin verilen veya bir VM'ye ziyaret ederek reddedilen varsa öğrenmek [IP akış ile doğrulama trafiği doğrulayın](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="2c8cb-145">Find out if traffic is allowed or denied on a VM by visiting [Verify traffic with IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

