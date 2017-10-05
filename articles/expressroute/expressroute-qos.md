---
title: "ExpressRoute için QoS gereksinimleri | Microsoft Docs"
description: "Bu sayfada, ExpressRoute bağlantı hatları için hizmet kalitesini (QoS) yapılandırma ve yönetmeye yönelik ayrıntılı gereksinimler sağlanmıştır."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: db1c1447-0283-4a09-907b-ae481adc40c7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: cherylmc
ms.openlocfilehash: c097a9ccba91f59b323215d42d37e6d85e0981ce
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="expressroute-qos-requirements"></a><span data-ttu-id="8debb-103">ExpressRoute QoS gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="8debb-103">ExpressRoute QoS requirements</span></span>
<span data-ttu-id="8debb-104">Skype Kurumsal’da farklı QoS davranışları gerektiren çeşitli iş yükleri vardır.</span><span class="sxs-lookup"><span data-stu-id="8debb-104">Skype for Business has various workloads that require differentiated QoS treatment.</span></span> <span data-ttu-id="8debb-105">ExpressRoute aracılığıyla ses hizmetleri kullanmayı planlıyorsanız, aşağıda açıklanan gereksinimlere uymanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8debb-105">If you plan to consume voice services through ExpressRoute, you should adhere to the requirements described below.</span></span>

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> <span data-ttu-id="8debb-106">QoS gereksinimleri yalnızca Microsoft eşlemeleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="8debb-106">QoS requirements apply to the Microsoft peering only.</span></span> <span data-ttu-id="8debb-107">Azure ortak eşleme ve Azure özel eşlemesinde alınan ağ trafiğinizdeki DSCP değerleri 0’a ayarlanacaktır.</span><span class="sxs-lookup"><span data-stu-id="8debb-107">The DSCP values in your network traffic received on Azure public peering and Azure private peering will be reset to 0.</span></span> 
> 
> 

<span data-ttu-id="8debb-108">Aşağıdaki tabloda Skype Kurumsal tarafından kullanılan DSCP işaretlerinin bir listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8debb-108">The following table provides a list of DSCP markings used by Skype for Business.</span></span> <span data-ttu-id="8debb-109">Daha fazla bilgi için [Skype Kurumsal için QoS’i yönetme](https://technet.microsoft.com/library/gg405409.aspx) bölümüne başvurun.</span><span class="sxs-lookup"><span data-stu-id="8debb-109">Refer to [Managing QoS for Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) for more information.</span></span>

| <span data-ttu-id="8debb-110">**Trafik Sınıfı**</span><span class="sxs-lookup"><span data-stu-id="8debb-110">**Traffic Class**</span></span> | <span data-ttu-id="8debb-111">**İşleme (DSCP İşaretleme)**</span><span class="sxs-lookup"><span data-stu-id="8debb-111">**Treatment (DSCP Marking)**</span></span> | <span data-ttu-id="8debb-112">**Skype Kurumsal İş Yükleri**</span><span class="sxs-lookup"><span data-stu-id="8debb-112">**Skype for Business Workloads**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8debb-113">**Ses**</span><span class="sxs-lookup"><span data-stu-id="8debb-113">**Voice**</span></span> |<span data-ttu-id="8debb-114">EF (46)</span><span class="sxs-lookup"><span data-stu-id="8debb-114">EF (46)</span></span> |<span data-ttu-id="8debb-115">Skype / Lync ses</span><span class="sxs-lookup"><span data-stu-id="8debb-115">Skype / Lync voice</span></span> |
| <span data-ttu-id="8debb-116">**Etkileşimli**</span><span class="sxs-lookup"><span data-stu-id="8debb-116">**Interactive**</span></span> |<span data-ttu-id="8debb-117">AF41 (34)</span><span class="sxs-lookup"><span data-stu-id="8debb-117">AF41 (34)</span></span> |<span data-ttu-id="8debb-118">Video, VBSS</span><span class="sxs-lookup"><span data-stu-id="8debb-118">Video, VBSS</span></span> |
| <span data-ttu-id="8debb-119">AF21 (18)</span><span class="sxs-lookup"><span data-stu-id="8debb-119">AF21 (18)</span></span> |<span data-ttu-id="8debb-120">Uygulama paylaşımı</span><span class="sxs-lookup"><span data-stu-id="8debb-120">App sharing</span></span> | |
| <span data-ttu-id="8debb-121">**Varsayılan**</span><span class="sxs-lookup"><span data-stu-id="8debb-121">**Default**</span></span> |<span data-ttu-id="8debb-122">AF11 (10)</span><span class="sxs-lookup"><span data-stu-id="8debb-122">AF11 (10)</span></span> |<span data-ttu-id="8debb-123">Dosya aktarımı</span><span class="sxs-lookup"><span data-stu-id="8debb-123">File transfer</span></span> |
| <span data-ttu-id="8debb-124">CS0 (0)</span><span class="sxs-lookup"><span data-stu-id="8debb-124">CS0 (0)</span></span> |<span data-ttu-id="8debb-125">Diğer</span><span class="sxs-lookup"><span data-stu-id="8debb-125">Anything else</span></span> | |

* <span data-ttu-id="8debb-126">İş yükleri sınıflandırmanız ve doğru DSCP değerlerini işaretlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8debb-126">You should classify the workloads and mark the right DSCP values.</span></span> <span data-ttu-id="8debb-127">Ağınızda DSCP işaretlerini ayarlamak için [burada](https://technet.microsoft.com/library/gg405409.aspx) sağlanan yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="8debb-127">Follow the guidance provided [here](https://technet.microsoft.com/library/gg405409.aspx) on how to set DSCP markings in your network.</span></span>
* <span data-ttu-id="8debb-128">Ağınızda çoklu QoS kuyruklarını yapılandırmanız ve desteklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8debb-128">You should configure and support multiple QoS queues within your network.</span></span> <span data-ttu-id="8debb-129">Ses, tek başına bir sınıf olmalı ve ses için RFC 3246 içinde belirtilen EF işlemi uygulanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8debb-129">Voice must be a standalone class and receive the EF treatment specified in RFC 3246.</span></span> 
* <span data-ttu-id="8debb-130">Kuyruğa alma mekanizması, sıkışma algılama ilkesi ve trafik sınıfı başına bant genişliği ayırmayı siz belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8debb-130">You can decide the queuing mechanism, congestion detection policy, and bandwidth allocation per traffic class.</span></span> <span data-ttu-id="8debb-131">Ancak, Skype Kurumsal iş yükleri için DSCP işaretlemesi korunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8debb-131">But, the DSCP marking for Skype for Business workloads must be preserved.</span></span> <span data-ttu-id="8debb-132">AF31 (26) gibi yukarıda listelenmeyen DSCP işaretlerini kullanıyorsanız, paketi Microsoft'a göndermeden önce bu DSCP değerinin 0 olarak yeniden yazılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8debb-132">If you are using DSCP markings not listed above, e.g. AF31 (26), you must rewrite this DSCP value to 0 before sending the packet to Microsoft.</span></span> <span data-ttu-id="8debb-133">Microsoft yalnızca yukarıdaki tabloda gösterilen DSCP değeriyle işaretlenen paketleri gönderir.</span><span class="sxs-lookup"><span data-stu-id="8debb-133">Microsoft only sends packets marked with the DSCP value shown in the above table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8debb-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8debb-134">Next steps</span></span>
* <span data-ttu-id="8debb-135">[Yönlendirme](expressroute-routing.md) ve [NAT](expressroute-nat.md) için gereksinimlere bakın.</span><span class="sxs-lookup"><span data-stu-id="8debb-135">Refer to the requirements for [Routing](expressroute-routing.md) and [NAT](expressroute-nat.md).</span></span>
* <span data-ttu-id="8debb-136">ExpressRoute bağlantınızı yapılandırmak için aşağıdaki bağlantılara bakın.</span><span class="sxs-lookup"><span data-stu-id="8debb-136">See the following links to configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="8debb-137">ExpressRoute bağlantı hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8debb-137">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-classic.md)
  * [<span data-ttu-id="8debb-138">Yönlendirmeyi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8debb-138">Configure routing</span></span>](expressroute-howto-routing-classic.md)
  * [<span data-ttu-id="8debb-139">ExpressRoute bağlantı hattına bir Sanal Ağ bağlama</span><span class="sxs-lookup"><span data-stu-id="8debb-139">Link a VNet to an ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

