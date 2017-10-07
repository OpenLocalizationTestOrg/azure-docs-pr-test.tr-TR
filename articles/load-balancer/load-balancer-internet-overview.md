---
title: "Yük Dengeleyici genel kullanıma yönelik aaaInternet | Microsoft Docs"
description: "Internet'e yönelik Yük Dengeleyici ve özellikleri için genel bakış. Nasıl bir yük dengeleyici sanal makineler ve bulut hizmetlerini kullanarak Azure için çalışır."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 529b37aa-a45c-41d1-8877-fee8cc1fa375
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3514f945d69ec576ed256cdd01069491e3e43936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="internet-facing-load-balancer-overview"></a><span data-ttu-id="f0ccd-104">Internet kullanıma yönelik Yük Dengeleyici genel bakış</span><span class="sxs-lookup"><span data-stu-id="f0ccd-104">Internet facing load balancer overview</span></span>

<span data-ttu-id="f0ccd-105">Azure yük dengeleyici hello ortak IP adresi ve bağlantı noktası numarası gelen trafiği toohello özel IP adresi ve bağlantı noktası numarası hello sanal makinenin ve tersi hello yanıt trafiği hello sanal makineden eşler.</span><span class="sxs-lookup"><span data-stu-id="f0ccd-105">Azure load balancer maps hello public IP address and port number of incoming traffic toohello private IP address and port number of hello virtual machine and vice versa for hello response traffic from hello virtual machine.</span></span> <span data-ttu-id="f0ccd-106">Yük Dengeleme kuralları toodistribute belirli birden çok sanal makineler veya hizmetler arasındaki trafik türlerinin izin verir.</span><span class="sxs-lookup"><span data-stu-id="f0ccd-106">Load balancing rules allow you toodistribute specific types of traffic between multiple virtual machines or services.</span></span> <span data-ttu-id="f0ccd-107">Örneğin, birden çok web sunucuları veya web rolleri web isteği trafiği hello yükünü yayılabilir.</span><span class="sxs-lookup"><span data-stu-id="f0ccd-107">For example, you can spread hello load of web request traffic across multiple web servers or web roles.</span></span>

<span data-ttu-id="f0ccd-108">Web rolleri veya çalışan rolleri örneklerini içeren bir bulut hizmeti için genel bir uç nokta hello hizmet açıklaması (.csdef) dosyasında tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f0ccd-108">For a cloud service that contains instances of web roles or worker roles, you can define a public endpoint in hello service definition (.csdef) file.</span></span>

<span data-ttu-id="f0ccd-109">Merhaba *servicedefinition.csdef* dosyası hello uç nokta yapılandırması içerir ve bir web veya çalışan rolü dağıtımı için birden çok rol örneği varsa, hello yük dengeleyici ayarları için olacaktır.</span><span class="sxs-lookup"><span data-stu-id="f0ccd-109">hello *servicedefinition.csdef* file contains hello endpoint configuration and when you have multiple role instances for a web or worker role deployment, hello load balancer will be setup for it.</span></span> <span data-ttu-id="f0ccd-110">Merhaba yolu tooadd örnekleri tooyour bulut dağıtımı hello örnek sayısı hello hizmet yapılandırma dosyası (.csfg) üzerinde değiştiriyor.</span><span class="sxs-lookup"><span data-stu-id="f0ccd-110">hello way tooadd instances tooyour cloud deployment is changing hello instance count on hello service configuration file (.csfg).</span></span>

<span data-ttu-id="f0ccd-111">Merhaba aşağıdaki şekilde hello ortak ve özel TCP bağlantı noktası 80 için üç sanal makineler arasında paylaşılan web trafiği için yük dengeli bir uç nokta gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f0ccd-111">hello following figure shows a load-balanced endpoint for web traffic that is shared among three virtual machines for hello public and private TCP port of 80.</span></span> <span data-ttu-id="f0ccd-112">Bu üç sanal makine bir yük dengeli kümesi yok.</span><span class="sxs-lookup"><span data-stu-id="f0ccd-112">These three virtual machines are in a load-balanced set.</span></span>

![Ortak yük dengeleyici örneği](./media/load-balancer-internet-overview/IC727496.png)

<span data-ttu-id="f0ccd-114">Şekil 1 - web trafiği için yük dengeli uç nokta</span><span class="sxs-lookup"><span data-stu-id="f0ccd-114">Figure 1 - Load-balanced endpoint for web traffic</span></span>

<span data-ttu-id="f0ccd-115">Internet istemcileri TCP bağlantı noktası 80 üzerinde toohello genel IP adresi hello bulut hizmetinin web sayfası istekleri gönderdiğinizde, hello Azure yük dengeleyici hello isteklerini hello yük dengeli kümesi içindeki hello üç sanal makineler arasında dağıtır.</span><span class="sxs-lookup"><span data-stu-id="f0ccd-115">When Internet clients send web page requests toohello public IP address of hello cloud service on TCP port 80, hello Azure Load Balancer distributes hello requests between hello three virtual machines in hello load-balanced set.</span></span> <span data-ttu-id="f0ccd-116">Yük Dengeleyici algoritmalar hakkında daha fazla bilgi için bkz: Merhaba [yük dengeleyici genel bakış sayfasında](load-balancer-overview.md#load-balancer-features).</span><span class="sxs-lookup"><span data-stu-id="f0ccd-116">For more information about load balancer algorithms, see hello [load balancer overview page](load-balancer-overview.md#load-balancer-features).</span></span>

<span data-ttu-id="f0ccd-117">Varsayılan olarak, Azure yük dengeleyici ağ trafiği birden çok sanal makine örnekleri arasında eşit olarak dağıtır.</span><span class="sxs-lookup"><span data-stu-id="f0ccd-117">By default, Azure Load Balancer distributes network traffic equally among multiple virtual machine instances.</span></span> <span data-ttu-id="f0ccd-118">Oturum benzeşimi de yapılandırabilirsiniz daha fazla bilgi için bkz: [yük dengeleyici dağıtım modu](load-balancer-distribution-mode.md).</span><span class="sxs-lookup"><span data-stu-id="f0ccd-118">You can also configure session affinity, For more information, see [load balancer distribution mode](load-balancer-distribution-mode.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0ccd-119">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f0ccd-119">Next steps</span></span>

<span data-ttu-id="f0ccd-120">Hakkında bilgi edinin [iç yük dengeleyici](load-balancer-internal-overview.md) toobetter anlamak daha iyi bir uyum bulut dağıtımınız için hangi yük dengeleyicidir.</span><span class="sxs-lookup"><span data-stu-id="f0ccd-120">Learn about [Internal load balancer](load-balancer-internal-overview.md) toobetter understand which load balancer is a better fit for your cloud deployment.</span></span>

<span data-ttu-id="f0ccd-121">Ayrıca [Internet'e yönelik Yük Dengeleyici oluşturmaya başlamak](load-balancer-get-started-internet-arm-ps.md) ve ne tür yapılandırma [dağıtım modu](load-balancer-distribution-mode.md) bir özel yük dengeleyici ağ trafiği davranışı için.</span><span class="sxs-lookup"><span data-stu-id="f0ccd-121">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for an specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="f0ccd-122">Uygulamanızı tookeep bağlantıları canlı bir yük dengeleyicinin arkasındaki sunucular için gerekiyorsa, daha fazla hakkında anlayabileceği [boşta bir yük dengeleyici için TCP zaman aşımı ayarları](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="f0ccd-122">If your application needs tookeep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="f0ccd-123">Azure yük dengeleyici kullanırken toolearn boştaki bağlantı davranışı konusunda yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="f0ccd-123">It will help toolearn about idle connection behavior when you are using Azure Load Balancer.</span></span>
