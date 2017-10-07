---
title: "aaaQoS ExpressRoute için gereksinimleri | Microsoft Docs"
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
ms.openlocfilehash: 46cc81bd38ff50dd9e7a1bfdd0faa457ff7b2fa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-qos-requirements"></a><span data-ttu-id="40802-103">ExpressRoute QoS gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="40802-103">ExpressRoute QoS requirements</span></span>
<span data-ttu-id="40802-104">Skype Kurumsal’da farklı QoS davranışları gerektiren çeşitli iş yükleri vardır.</span><span class="sxs-lookup"><span data-stu-id="40802-104">Skype for Business has various workloads that require differentiated QoS treatment.</span></span> <span data-ttu-id="40802-105">ExpressRoute aracılığıyla ses Hizmetleri tooconsume planlıyorsanız, aşağıda açıklanan toohello gereksinimlere uymanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="40802-105">If you plan tooconsume voice services through ExpressRoute, you should adhere toohello requirements described below.</span></span>

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> <span data-ttu-id="40802-106">QoS gereksinimleri yalnızca Microsoft toohello eşlemesi geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="40802-106">QoS requirements apply toohello Microsoft peering only.</span></span> <span data-ttu-id="40802-107">Azure ortak eşleme ve Azure özel eşleme alınan, ağ trafiğinin Hello DSCP değerlerini sıfırlama too0 olacaktır.</span><span class="sxs-lookup"><span data-stu-id="40802-107">hello DSCP values in your network traffic received on Azure public peering and Azure private peering will be reset too0.</span></span> 
> 
> 

<span data-ttu-id="40802-108">Merhaba aşağıdaki tabloda işletmeler için Skype tarafından kullanılan DSCP işaretlerinin bir listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="40802-108">hello following table provides a list of DSCP markings used by Skype for Business.</span></span> <span data-ttu-id="40802-109">Çok başvuran[Skype Kurumsal için Qos'i yönetme](https://technet.microsoft.com/library/gg405409.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="40802-109">Refer too[Managing QoS for Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) for more information.</span></span>

| <span data-ttu-id="40802-110">**Trafik Sınıfı**</span><span class="sxs-lookup"><span data-stu-id="40802-110">**Traffic Class**</span></span> | <span data-ttu-id="40802-111">**İşleme (DSCP İşaretleme)**</span><span class="sxs-lookup"><span data-stu-id="40802-111">**Treatment (DSCP Marking)**</span></span> | <span data-ttu-id="40802-112">**Skype Kurumsal İş Yükleri**</span><span class="sxs-lookup"><span data-stu-id="40802-112">**Skype for Business Workloads**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40802-113">**Ses**</span><span class="sxs-lookup"><span data-stu-id="40802-113">**Voice**</span></span> |<span data-ttu-id="40802-114">EF (46)</span><span class="sxs-lookup"><span data-stu-id="40802-114">EF (46)</span></span> |<span data-ttu-id="40802-115">Skype / Lync ses</span><span class="sxs-lookup"><span data-stu-id="40802-115">Skype / Lync voice</span></span> |
| <span data-ttu-id="40802-116">**Etkileşimli**</span><span class="sxs-lookup"><span data-stu-id="40802-116">**Interactive**</span></span> |<span data-ttu-id="40802-117">AF41 (34)</span><span class="sxs-lookup"><span data-stu-id="40802-117">AF41 (34)</span></span> |<span data-ttu-id="40802-118">Video, VBSS</span><span class="sxs-lookup"><span data-stu-id="40802-118">Video, VBSS</span></span> |
| <span data-ttu-id="40802-119">AF21 (18)</span><span class="sxs-lookup"><span data-stu-id="40802-119">AF21 (18)</span></span> |<span data-ttu-id="40802-120">Uygulama paylaşımı</span><span class="sxs-lookup"><span data-stu-id="40802-120">App sharing</span></span> | |
| <span data-ttu-id="40802-121">**Varsayılan**</span><span class="sxs-lookup"><span data-stu-id="40802-121">**Default**</span></span> |<span data-ttu-id="40802-122">AF11 (10)</span><span class="sxs-lookup"><span data-stu-id="40802-122">AF11 (10)</span></span> |<span data-ttu-id="40802-123">Dosya aktarımı</span><span class="sxs-lookup"><span data-stu-id="40802-123">File transfer</span></span> |
| <span data-ttu-id="40802-124">CS0 (0)</span><span class="sxs-lookup"><span data-stu-id="40802-124">CS0 (0)</span></span> |<span data-ttu-id="40802-125">Diğer</span><span class="sxs-lookup"><span data-stu-id="40802-125">Anything else</span></span> | |

* <span data-ttu-id="40802-126">Merhaba iş yükleri sınıflandırmanız ve hello doğru DSCP değerlerini işaretlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="40802-126">You should classify hello workloads and mark hello right DSCP values.</span></span> <span data-ttu-id="40802-127">Sağlanan hello yönergeleri izlemelidir [burada](https://technet.microsoft.com/library/gg405409.aspx) nasıl ağınızda DSCP işaretlerini tooset.</span><span class="sxs-lookup"><span data-stu-id="40802-127">Follow hello guidance provided [here](https://technet.microsoft.com/library/gg405409.aspx) on how tooset DSCP markings in your network.</span></span>
* <span data-ttu-id="40802-128">Ağınızda çoklu QoS kuyruklarını yapılandırmanız ve desteklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="40802-128">You should configure and support multiple QoS queues within your network.</span></span> <span data-ttu-id="40802-129">Ses, tek başına bir sınıf olması ve ses için RFC 3246 içinde belirtilen hello EF işlemi uygulanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="40802-129">Voice must be a standalone class and receive hello EF treatment specified in RFC 3246.</span></span> 
* <span data-ttu-id="40802-130">Mekanizması, sıkışma algılama İlkesi ve trafik sınıfı başına bant genişliği ayırma queuing hello karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40802-130">You can decide hello queuing mechanism, congestion detection policy, and bandwidth allocation per traffic class.</span></span> <span data-ttu-id="40802-131">Ancak, hello DSCP Skype kurumsal iş yükleri için işaretleme korunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="40802-131">But, hello DSCP marking for Skype for Business workloads must be preserved.</span></span> <span data-ttu-id="40802-132">Yukarıda listelenmeyen DSCP işaretlerini kullanıyorsanız AF31 (26) yeniden yazılması gerekir bu DSCP değeri too0 hello paket tooMicrosoft göndermeden önce.</span><span class="sxs-lookup"><span data-stu-id="40802-132">If you are using DSCP markings not listed above, e.g. AF31 (26), you must rewrite this DSCP value too0 before sending hello packet tooMicrosoft.</span></span> <span data-ttu-id="40802-133">Microsoft, yalnızca hello hello yukarıdaki tabloda gösterilen DSCP değeri ile işaretlenen paketleri gönderir.</span><span class="sxs-lookup"><span data-stu-id="40802-133">Microsoft only sends packets marked with hello DSCP value shown in hello above table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="40802-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="40802-134">Next steps</span></span>
* <span data-ttu-id="40802-135">Toohello gereksinimleri başvuran [yönlendirme](expressroute-routing.md) ve [NAT](expressroute-nat.md).</span><span class="sxs-lookup"><span data-stu-id="40802-135">Refer toohello requirements for [Routing](expressroute-routing.md) and [NAT](expressroute-nat.md).</span></span>
* <span data-ttu-id="40802-136">ExpressRoute bağlantınızı tooconfigure Hello aşağıdaki bağlantılar bakın.</span><span class="sxs-lookup"><span data-stu-id="40802-136">See hello following links tooconfigure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="40802-137">ExpressRoute bağlantı hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="40802-137">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-classic.md)
  * [<span data-ttu-id="40802-138">Yönlendirmeyi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="40802-138">Configure routing</span></span>](expressroute-howto-routing-classic.md)
  * [<span data-ttu-id="40802-139">VNet tooan expressroute bağlantı hattı bağlantı</span><span class="sxs-lookup"><span data-stu-id="40802-139">Link a VNet tooan ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

