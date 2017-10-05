---
title: "Akış günlüğü Azure Ağ İzleyicisi ile ağ güvenlik grupları için giriş | Microsoft Docs"
description: "Bu sayfayı NSG akış günlükleri kullanımı Azure Ağ İzleyicisi, bir özellik açıklanmaktadır"
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
ms.openlocfilehash: b7a9162d6c6219b6b1c51a49cd34b9616e9d3e8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-flow-logging-for-network-security-groups"></a><span data-ttu-id="d0c5a-103">Akış günlüğü ağ güvenlik grupları için giriş</span><span class="sxs-lookup"><span data-stu-id="d0c5a-103">Introduction to flow logging for Network Security Groups</span></span>

<span data-ttu-id="d0c5a-104">Ağ güvenlik grubu akış günlükleri, giriş ve çıkış IP trafiği bir ağ güvenlik grubu ile ilgili bilgileri görüntülemek izin veren bir Ağ İzleyicisi özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="d0c5a-104">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="d0c5a-105">Bu akış günlükleri json biçiminde yazılır ve Kural başına temelinde, akış uygulanır, akış (kaynak/hedef IP, kaynak/hedef bağlantı noktası, Protokolü), 5-tanımlama grubu bilgilerini NIC giden ve gelen akışları gösterir ve trafiğe izin verilen veya reddedilen.</span><span class="sxs-lookup"><span data-stu-id="d0c5a-105">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

![Akış günlükleri genel bakış][1]

<span data-ttu-id="d0c5a-107">Hedef ağ güvenlik grupları akış günlükleri, ancak bunlar değil aynı diğer günlükler görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d0c5a-107">While flow logs target Network Security Groups, they are not displayed the same as the other logs.</span></span> <span data-ttu-id="d0c5a-108">Akış günlükleri, aşağıdaki örnekte gösterildiği gibi yalnızca bir depolama hesabı içinde ve günlük yolu aşağıdaki depolanır:</span><span class="sxs-lookup"><span data-stu-id="d0c5a-108">Flow logs are stored only within a storage account and following the logging path as shown in the following example:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="d0c5a-109">Diğer günlükler üzerinde görülen olarak aynı bekletme ilkeleri, akış günlüklerine uygulanır.</span><span class="sxs-lookup"><span data-stu-id="d0c5a-109">The same retention policies as seen on other logs apply to flow logs.</span></span> <span data-ttu-id="d0c5a-110">Günlükleri günden 1 gün 365 gün olarak ayarlanabilir bir bekletme ilkesi vardır.</span><span class="sxs-lookup"><span data-stu-id="d0c5a-110">Logs have a retention policy that can be set from 1 day to 365 days.</span></span> <span data-ttu-id="d0c5a-111">Bekletme ilkesi ayarlanmazsa günlükler süresiz olarak saklanır.</span><span class="sxs-lookup"><span data-stu-id="d0c5a-111">If a retention policy is not set, the logs are maintained forever.</span></span>

## <a name="log-file"></a><span data-ttu-id="d0c5a-112">Günlük dosyası</span><span class="sxs-lookup"><span data-stu-id="d0c5a-112">Log file</span></span>

<span data-ttu-id="d0c5a-113">Akış günlükleri, birden çok özelliği vardır.</span><span class="sxs-lookup"><span data-stu-id="d0c5a-113">Flow logs have multiple properties.</span></span> <span data-ttu-id="d0c5a-114">Aşağıdaki listede NSG akış günlükte döndürülen özellikleri listesi bulunmaktadır:</span><span class="sxs-lookup"><span data-stu-id="d0c5a-114">The following list is a listing of the properties that are returned within the NSG flow log:</span></span>

* <span data-ttu-id="d0c5a-115">**zaman** - olayın günlüğe yazıldığı zaman zaman</span><span class="sxs-lookup"><span data-stu-id="d0c5a-115">**time** - Time when the event was logged</span></span>
* <span data-ttu-id="d0c5a-116">**SistemKimliği** -ağ güvenlik grubu kaynak kimliği</span><span class="sxs-lookup"><span data-stu-id="d0c5a-116">**systemId** - Network Security Group resource Id.</span></span>
* <span data-ttu-id="d0c5a-117">**Kategori** -kategori olayı, bu her zaman olmaya NetworkSecurityGroupFlowEvent</span><span class="sxs-lookup"><span data-stu-id="d0c5a-117">**category** - The category of the event, this is always be NetworkSecurityGroupFlowEvent</span></span>
* <span data-ttu-id="d0c5a-118">**ResourceId** -kaynak NSG kimliği</span><span class="sxs-lookup"><span data-stu-id="d0c5a-118">**resourceid** - The resource Id of the NSG</span></span>
* <span data-ttu-id="d0c5a-119">**operationName** -her zaman NetworkSecurityGroupFlowEvents</span><span class="sxs-lookup"><span data-stu-id="d0c5a-119">**operationName** - Always NetworkSecurityGroupFlowEvents</span></span>
* <span data-ttu-id="d0c5a-120">**Özellikler** -akışının özellikleri koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="d0c5a-120">**properties** - A collection of properties of the flow</span></span>
    * <span data-ttu-id="d0c5a-121">**Sürüm** -akış günlüğü olay şeması sürüm numarası</span><span class="sxs-lookup"><span data-stu-id="d0c5a-121">**Version** - Version number of the Flow Log event schema</span></span>
    * <span data-ttu-id="d0c5a-122">**Akışlar** -akışları koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="d0c5a-122">**flows** - A collection of flows.</span></span> <span data-ttu-id="d0c5a-123">Bu özelliği farklı kurallar için birden fazla varlık içeriyor</span><span class="sxs-lookup"><span data-stu-id="d0c5a-123">This property has multiple entries for different rules</span></span>
        * <span data-ttu-id="d0c5a-124">**Kural** -kural akışları listelenmiş</span><span class="sxs-lookup"><span data-stu-id="d0c5a-124">**rule** - Rule for which the flows are listed</span></span>
            * <span data-ttu-id="d0c5a-125">**Akışlar** -akışları koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="d0c5a-125">**flows** - a collection of flows</span></span>
                * <span data-ttu-id="d0c5a-126">**Mac** -burada akış toplandı VM için NIC MAC adresi</span><span class="sxs-lookup"><span data-stu-id="d0c5a-126">**mac** - The MAC address of the NIC for the VM where the flow was collected</span></span>
                * <span data-ttu-id="d0c5a-127">**flowTuples** -virgülle ayrılmış biçimde akış tanımlama grubu için birden çok özellik içeren bir dize</span><span class="sxs-lookup"><span data-stu-id="d0c5a-127">**flowTuples** - A string that contains multiple properties for the flow tuple in comma-separated format</span></span>
                    * <span data-ttu-id="d0c5a-128">**Zaman damgası** -akış UNIX dönem biçiminde oluştuğunda bu zaman damgası değerdir</span><span class="sxs-lookup"><span data-stu-id="d0c5a-128">**Time Stamp** - This value is the time stamp of when the flow occurred in UNIX EPOCH format</span></span>
                    * <span data-ttu-id="d0c5a-129">**Kaynak IP** -kaynak IP</span><span class="sxs-lookup"><span data-stu-id="d0c5a-129">**Source IP** - The source IP</span></span>
                    * <span data-ttu-id="d0c5a-130">**Hedef IP** -hedef IP</span><span class="sxs-lookup"><span data-stu-id="d0c5a-130">**Destination IP** - The destination IP</span></span>
                    * <span data-ttu-id="d0c5a-131">**Kaynak bağlantı noktası** -kaynak bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="d0c5a-131">**Source Port** - The source port</span></span>
                    * <span data-ttu-id="d0c5a-132">**Hedef bağlantı noktası** -hedef bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="d0c5a-132">**Destination Port** - The destination Port</span></span>
                    * <span data-ttu-id="d0c5a-133">**Protokol** -Akış Protokolü.</span><span class="sxs-lookup"><span data-stu-id="d0c5a-133">**Protocol** - The protocol of the flow.</span></span> <span data-ttu-id="d0c5a-134">Geçerli değerler **T** TCP için ve **U** UDP için</span><span class="sxs-lookup"><span data-stu-id="d0c5a-134">Valid values are **T** for TCP and **U** for UDP</span></span>
                    * <span data-ttu-id="d0c5a-135">**Trafik akışı** -trafik akış yönü.</span><span class="sxs-lookup"><span data-stu-id="d0c5a-135">**Traffic Flow** - The direction of the traffic flow.</span></span> <span data-ttu-id="d0c5a-136">Geçerli değerler **ı** gelen ve **O** için giden.</span><span class="sxs-lookup"><span data-stu-id="d0c5a-136">Valid values are **I** for inbound and **O** for outbound.</span></span>
                    * <span data-ttu-id="d0c5a-137">**Trafik** - trafiğine izin verilen veya reddedilen olup olmadığını.</span><span class="sxs-lookup"><span data-stu-id="d0c5a-137">**Traffic** - Whether traffic was allowed or denied.</span></span> <span data-ttu-id="d0c5a-138">Geçerli değerler **A** izin ve **D** reddedildi için.</span><span class="sxs-lookup"><span data-stu-id="d0c5a-138">Valid values are **A** for allowed and **D** for denied.</span></span>


<span data-ttu-id="d0c5a-139">Akış günlüğü örneği verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d0c5a-139">The following is an example of a Flow log.</span></span> <span data-ttu-id="d0c5a-140">Gördüğünüz gibi önceki bölümde açıklanan özellik listesi izleyin birden çok kayıt vardır.</span><span class="sxs-lookup"><span data-stu-id="d0c5a-140">As you can see there are multiple records that follow the property list described in the preceding section.</span></span> 

> [!NOTE]
> <span data-ttu-id="d0c5a-141">FlowTuples özelliği virgülle ayrılmış bir liste değerler.</span><span class="sxs-lookup"><span data-stu-id="d0c5a-141">Values in the flowTuples property are a comma-separated list.</span></span>
 
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

## <a name="next-steps"></a><span data-ttu-id="d0c5a-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d0c5a-142">Next steps</span></span>

<span data-ttu-id="d0c5a-143">Akış günlükleri ziyaret ederek etkinleştirmeyi öğrenin [günlüğü etkinleştirme akışı](network-watcher-nsg-flow-logging-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d0c5a-143">Learn how to enable Flow logs by visiting [Enabling Flow logging](network-watcher-nsg-flow-logging-portal.md).</span></span>

<span data-ttu-id="d0c5a-144">NSG oturum açma hakkında bilgi edinin ziyaret ederek [günlük analizi için ağ güvenlik grupları (Nsg'ler)](../virtual-network/virtual-network-nsg-manage-log.md).</span><span class="sxs-lookup"><span data-stu-id="d0c5a-144">Learn about NSG logging by visiting [Log analytics for network security groups (NSGs)](../virtual-network/virtual-network-nsg-manage-log.md).</span></span>

<span data-ttu-id="d0c5a-145">Trafik izin verilen veya bir VM'ye ziyaret ederek reddedilen varsa öğrenmek [IP akış ile doğrulama trafiği doğrulayın](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d0c5a-145">Find out if traffic is allowed or denied on a VM by visiting [Verify traffic with IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

