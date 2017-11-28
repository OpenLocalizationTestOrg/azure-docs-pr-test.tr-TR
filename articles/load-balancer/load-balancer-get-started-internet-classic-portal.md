---
title: "aaaCreate bir Internet'e yönelik Yük Dengeleyici - Klasik Azure portalı | Microsoft Docs"
description: "Klasik Azure portalı toocreate Klasik dağıtım modeli kullanarak bir Internet'e yönelik Yük Dengeleyici hello nasıl öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fa3e93c0-968a-472d-a17c-65665c050db2
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 27b0d5af6e7b493fa94a9dfbfa260483ae95a2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-classic-portal"></a><span data-ttu-id="691e5-103">Internet'e yönelik yük dengeleyicisi (Klasik) hello Klasik Azure portalı oluşturmaya başlamak</span><span class="sxs-lookup"><span data-stu-id="691e5-103">Get started creating an Internet facing load balancer (classic) in hello Azure classic portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="691e5-104">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="691e5-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="691e5-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="691e5-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="691e5-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="691e5-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="691e5-107">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="691e5-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="691e5-108">Azure kaynaklarıyla çalışmadan önce Azure'da şu anda iki dağıtım modeli olduğunu önemli toounderstand olduğu: Azure Resource Manager ve klasik.</span><span class="sxs-lookup"><span data-stu-id="691e5-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="691e5-109">Azure kaynaklarıyla çalışmadan önce [dağıtım modellerini ve araçlarlarını](../azure-classic-rm.md) iyice anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="691e5-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="691e5-110">Bu makalenin hello üstünde hello sekmeleri tıklayarak farklı araçlarla ilgili hello belgeleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="691e5-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="691e5-111">Bu makalede, hello Klasik dağıtım modeli yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="691e5-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="691e5-112">Ayrıca [nasıl toocreate Internet'e yönelik Yük Dengeleyici Azure Resource Manager kullanarak bilgi](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="691e5-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a><span data-ttu-id="691e5-113">Sanal makineler için İnternet’e yönelik yük dengeleyici kurma</span><span class="sxs-lookup"><span data-stu-id="691e5-113">Set up an Internet-facing load balancer for virtual machines</span></span>

<span data-ttu-id="691e5-114">Sipariş tooload Bakiye gelen ağ trafiğinin içinde hello Internet hello sanal makineler bir bulut hizmeti arasında yük dengeli kümesi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="691e5-114">In order tooload balance network traffic from hello Internet across hello virtual machines of a cloud service, you must create a load-balanced set.</span></span> <span data-ttu-id="691e5-115">Bu yordam hello sanal makineleri oluşturmuş ve tüm varsayar hello içinde aynı bulut hizmeti.</span><span class="sxs-lookup"><span data-stu-id="691e5-115">This procedure assumes that you have already created hello virtual machines and that they are all within hello same cloud service.</span></span>

<span data-ttu-id="691e5-116">**sanal makineler için yük dengeli kümesi tooconfigure**</span><span class="sxs-lookup"><span data-stu-id="691e5-116">**tooconfigure a load-balanced set for virtual machines**</span></span>

1. <span data-ttu-id="691e5-117">Hello Klasik Azure portalı, tıklatın **sanal makineleri**ve ardından Yük dengeli hello kümesindeki bir sanal makine hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="691e5-117">In hello Azure classic portal, click **Virtual Machines**, and then click hello name of a virtual machine in hello load-balanced set.</span></span>
2. <span data-ttu-id="691e5-118">**Uç noktaları**’na ve ardından **Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="691e5-118">Click **Endpoints**, and then click **Add**.</span></span>
3. <span data-ttu-id="691e5-119">Merhaba üzerinde **bir uç nokta tooa sanal makine eklemek** sayfasında, hello sağ oka tıklayın.</span><span class="sxs-lookup"><span data-stu-id="691e5-119">On hello **Add an endpoint tooa virtual machine** page, click hello right arrow.</span></span>
4. <span data-ttu-id="691e5-120">Merhaba üzerinde **hello hello uç nokta ayrıntılarını belirtin** sayfa:</span><span class="sxs-lookup"><span data-stu-id="691e5-120">On hello **Specify hello details of hello endpoint** page:</span></span>

   * <span data-ttu-id="691e5-121">İçinde **adı**hello uç noktası için bir ad yazın veya yaygın protokoller için önceden tanımlanmış uç noktaları hello listeden hello adı seçin.</span><span class="sxs-lookup"><span data-stu-id="691e5-121">In **Name**, type a name for hello endpoint or select hello name from hello list of predefined endpoints for common protocols.</span></span>
   * <span data-ttu-id="691e5-122">İçinde **Protokolü**, gerektiğinde uç noktası, TCP veya UDP, hello türü tarafından gerekli hello protokolü seçin.</span><span class="sxs-lookup"><span data-stu-id="691e5-122">In **Protocol**, select hello protocol required by hello type of endpoint, either TCP or UDP, as needed.</span></span>
   * <span data-ttu-id="691e5-123">İçinde **genel bağlantı noktası ve özel bağlantı noktası**, sanal makine toouse hello gerektiği gibi istediğiniz başlangıç bağlantı noktası numaralarını yazın.</span><span class="sxs-lookup"><span data-stu-id="691e5-123">In **Public Port and Private Port**, type hello port numbers that you want hello virtual machine toouse, as needed.</span></span> <span data-ttu-id="691e5-124">Uygulamanız için uygun şekilde hello sanal makine tooredirect trafiği üzerinde hello özel bağlantı noktası ve güvenlik duvarı kuralları'nı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="691e5-124">You can use hello private port and firewall rules on hello virtual machine tooredirect traffic in a way that is appropriate for your application.</span></span> <span data-ttu-id="691e5-125">Merhaba özel bağlantı noktası olması hello hello genel bağlantı noktası ile aynı.</span><span class="sxs-lookup"><span data-stu-id="691e5-125">hello private port can be hello same as hello public port.</span></span> <span data-ttu-id="691e5-126">Örneğin, web (HTTP) trafiği için bir uç nokta için bağlantı noktası, 80 tooboth hello ortak ve özel bağlantı noktası atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="691e5-126">For example, for an endpoint for web (HTTP) traffic, you could assign port 80 tooboth hello public and private port.</span></span>

5. <span data-ttu-id="691e5-127">Seçin **bir yük dengeli kümesi oluşturma**ve ardından hello sağ oka tıklayın.</span><span class="sxs-lookup"><span data-stu-id="691e5-127">Select **Create a load-balanced set**, and then click hello right arrow.</span></span>
6. <span data-ttu-id="691e5-128">Merhaba üzerinde **hello yük dengeli küme Yapılandır** sayfasında, hello yük dengeli kümesi için bir ad yazın ve hello Azure yük dengeleyici araştırması davranışını hello değerlerini atayın.</span><span class="sxs-lookup"><span data-stu-id="691e5-128">On hello **Configure hello load-balanced set** page, type a name for hello load-balanced set, and then assign hello values for probe behavior of hello Azure Load Balancer.</span></span> <span data-ttu-id="691e5-129">Merhaba yük dengeli kümesi Hello sanal makinelerin kullanılabilir tooreceive gelen trafiği varsa hello yük dengeleyici araştırmalar toodetermine kullanır.</span><span class="sxs-lookup"><span data-stu-id="691e5-129">hello Load Balancer uses probes toodetermine if hello virtual machines in hello load-balanced set are available tooreceive incoming traffic.</span></span>
7. <span data-ttu-id="691e5-130">Merhaba onay işareti toocreate hello yük dengeli uç'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="691e5-130">Click hello check mark toocreate hello load-balanced endpoint.</span></span> <span data-ttu-id="691e5-131">Görürsünüz **Evet** hello içinde **yük dengeli kümesi adı** hello sütunu **uç noktaları** hello sanal makine için sayfa.</span><span class="sxs-lookup"><span data-stu-id="691e5-131">You will see **Yes** in hello **Load-balanced set name** column of hello **Endpoints** page for hello virtual machine.</span></span>
8. <span data-ttu-id="691e5-132">Merhaba Portalı'nda tıklatın **sanal makineleri**, ek bir sanal makine yükü dengelenmiş hello kümesindeki hello adına tıklayın, tıklatın **uç noktaları**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="691e5-132">In hello portal, click **Virtual Machines**, click hello name of an additional virtual machine in hello load-balanced set, click **Endpoints**, and then click **Add**.</span></span>
9. <span data-ttu-id="691e5-133">Merhaba üzerinde **bir uç nokta tooa sanal makine eklemek** sayfasında, **uç nokta tooan varolan yük dengeli kümesi ekleme**hello yük dengeli kümesi hello adını seçin ve ardından hello sağ oka tıklayın.</span><span class="sxs-lookup"><span data-stu-id="691e5-133">On hello **Add an endpoint tooa virtual machine** page, click **Add endpoint tooan existing load-balanced set**, select hello name of hello load-balanced set, and then click hello right arrow.</span></span>
10. <span data-ttu-id="691e5-134">Merhaba üzerinde **hello hello uç nokta ayrıntılarını belirtin** sayfasında, hello uç noktası için bir ad yazın ve ardından hello onay işaretine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="691e5-134">On hello **Specify hello details of hello endpoint** page, type a name for hello endpoint, and then click hello check mark.</span></span>

<span data-ttu-id="691e5-135">Merhaba ek sanal makineler için yük dengeli hello kümesinde, 8-10 adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="691e5-135">For hello additional virtual machines in hello load-balanced set, repeat steps 8-10.</span></span>

## <a name="next-steps"></a><span data-ttu-id="691e5-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="691e5-136">Next steps</span></span>

[<span data-ttu-id="691e5-137">Bir iç yük dengeleyici yapılandırmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="691e5-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="691e5-138">Yük dengeleyici dağıtım modu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="691e5-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="691e5-139">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="691e5-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
