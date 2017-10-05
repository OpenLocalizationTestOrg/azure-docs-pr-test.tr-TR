---
title: "Internet'e yönelik Yük Dengeleyici genel bakış | Microsoft Docs"
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
ms.openlocfilehash: c420b38fbe8054bc4b701f89ebc417677ca47a27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="internet-facing-load-balancer-overview"></a><span data-ttu-id="ea1c6-104">Internet kullanıma yönelik Yük Dengeleyici genel bakış</span><span class="sxs-lookup"><span data-stu-id="ea1c6-104">Internet facing load balancer overview</span></span>

<span data-ttu-id="ea1c6-105">Azure yük dengeleyici gelen trafiği ortak IP adresi ve bağlantı noktası numarasını özel IP adresi ve bağlantı noktası numarası sanal makinenin ve tersi yanıt trafiği sanal makineden eşler.</span><span class="sxs-lookup"><span data-stu-id="ea1c6-105">Azure load balancer maps the public IP address and port number of incoming traffic to the private IP address and port number of the virtual machine and vice versa for the response traffic from the virtual machine.</span></span> <span data-ttu-id="ea1c6-106">Yük Dengeleme kurallarında belirli birden çok sanal makineler veya hizmetler arasındaki trafik türlerinin dağıtmak olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ea1c6-106">Load balancing rules allow you to distribute specific types of traffic between multiple virtual machines or services.</span></span> <span data-ttu-id="ea1c6-107">Örneğin, birden çok web sunucuları veya web rolleri web isteği trafik yükünü yayılabilir.</span><span class="sxs-lookup"><span data-stu-id="ea1c6-107">For example, you can spread the load of web request traffic across multiple web servers or web roles.</span></span>

<span data-ttu-id="ea1c6-108">Web rolleri veya çalışan rolleri örneklerini içeren bir bulut hizmeti için hizmet açıklaması (.csdef) dosyasında genel bir uç nokta tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea1c6-108">For a cloud service that contains instances of web roles or worker roles, you can define a public endpoint in the service definition (.csdef) file.</span></span>

<span data-ttu-id="ea1c6-109">*Servicedefinition.csdef* dosyası uç nokta yapılandırması içerir ve bir web veya çalışan rolü dağıtımı için birden çok rol örneği varsa, yük dengeleyici ayarları için olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ea1c6-109">The *servicedefinition.csdef* file contains the endpoint configuration and when you have multiple role instances for a web or worker role deployment, the load balancer will be setup for it.</span></span> <span data-ttu-id="ea1c6-110">Bulut dağıtımınız için örnek eklemek için örnek sayısı hizmet yapılandırma dosyası (.csfg) üzerinde değiştirmektedir.</span><span class="sxs-lookup"><span data-stu-id="ea1c6-110">The way to add instances to your cloud deployment is changing the instance count on the service configuration file (.csfg).</span></span>

<span data-ttu-id="ea1c6-111">Yük dengeli bir uç nokta için genel ve özel TCP bağlantı noktası 80 üç sanal makineler arasında paylaşılan web trafiği için aşağıdaki şekilde gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ea1c6-111">The following figure shows a load-balanced endpoint for web traffic that is shared among three virtual machines for the public and private TCP port of 80.</span></span> <span data-ttu-id="ea1c6-112">Bu üç sanal makine bir yük dengeli kümesi yok.</span><span class="sxs-lookup"><span data-stu-id="ea1c6-112">These three virtual machines are in a load-balanced set.</span></span>

![Ortak yük dengeleyici örneği](./media/load-balancer-internet-overview/IC727496.png)

<span data-ttu-id="ea1c6-114">Şekil 1 - web trafiği için yük dengeli uç nokta</span><span class="sxs-lookup"><span data-stu-id="ea1c6-114">Figure 1 - Load-balanced endpoint for web traffic</span></span>

<span data-ttu-id="ea1c6-115">Internet istemcilerinin, TCP bağlantı noktası 80'bulut hizmetinin genel IP adresine web sayfası istekleri gönderdiğinizde, Azure yük dengeleyici istekleri için yük dengeli kümesi içinde üç sanal makine arasında dağıtır.</span><span class="sxs-lookup"><span data-stu-id="ea1c6-115">When Internet clients send web page requests to the public IP address of the cloud service on TCP port 80, the Azure Load Balancer distributes the requests between the three virtual machines in the load-balanced set.</span></span> <span data-ttu-id="ea1c6-116">Yük Dengeleyici algoritmalar hakkında daha fazla bilgi için bkz: [yük dengeleyici genel bakış sayfasında](load-balancer-overview.md#load-balancer-features).</span><span class="sxs-lookup"><span data-stu-id="ea1c6-116">For more information about load balancer algorithms, see the [load balancer overview page](load-balancer-overview.md#load-balancer-features).</span></span>

<span data-ttu-id="ea1c6-117">Varsayılan olarak, Azure yük dengeleyici ağ trafiği birden çok sanal makine örnekleri arasında eşit olarak dağıtır.</span><span class="sxs-lookup"><span data-stu-id="ea1c6-117">By default, Azure Load Balancer distributes network traffic equally among multiple virtual machine instances.</span></span> <span data-ttu-id="ea1c6-118">Oturum benzeşimi de yapılandırabilirsiniz daha fazla bilgi için bkz: [yük dengeleyici dağıtım modu](load-balancer-distribution-mode.md).</span><span class="sxs-lookup"><span data-stu-id="ea1c6-118">You can also configure session affinity, For more information, see [load balancer distribution mode](load-balancer-distribution-mode.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea1c6-119">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ea1c6-119">Next steps</span></span>

<span data-ttu-id="ea1c6-120">Hakkında bilgi edinin [iç yük dengeleyici](load-balancer-internal-overview.md) daha iyi bir uyum bulut dağıtımınız için hangi yük dengeleyici olduğundan daha iyi anlamak için.</span><span class="sxs-lookup"><span data-stu-id="ea1c6-120">Learn about [Internal load balancer](load-balancer-internal-overview.md) to better understand which load balancer is a better fit for your cloud deployment.</span></span>

<span data-ttu-id="ea1c6-121">Ayrıca [Internet'e yönelik Yük Dengeleyici oluşturmaya başlamak](load-balancer-get-started-internet-arm-ps.md) ve ne tür yapılandırma [dağıtım modu](load-balancer-distribution-mode.md) bir özel yük dengeleyici ağ trafiği davranışı için.</span><span class="sxs-lookup"><span data-stu-id="ea1c6-121">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for an specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="ea1c6-122">Uygulamanızın yük dengeleyici arkasındaki sunucular için bağlantıları canlı tutması gerekiyorsa [yük dengeleyici için boşta kalma TCP zaman aşımı ayarları](load-balancer-tcp-idle-timeout.md) hakkında daha fazla bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea1c6-122">If your application needs to keep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="ea1c6-123">Bu, Azure Load Balancer kullanırken boşta kalan bağlantı davranışları hakkında bilgi edinmenizi sağlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="ea1c6-123">It will help to learn about idle connection behavior when you are using Azure Load Balancer.</span></span>
