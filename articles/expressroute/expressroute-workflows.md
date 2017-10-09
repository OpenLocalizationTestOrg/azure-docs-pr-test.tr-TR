---
title: "bir expressroute bağlantı hattı yapılandırma aaaWorkflows | Microsoft Docs"
description: "Bu sayfada, expressroute bağlantı hattı ve eşlemeleri yapılandırma hello iş akışları açıklanmaktadır"
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 55e0418c-e0bf-44a7-9aa1-720076df9297
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8e1dfc137401e0d6d53608ae6c8de0085e182eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a><span data-ttu-id="16a5d-103">Devre sağlama ve devre durumları için ExpressRoute iş akışları</span><span class="sxs-lookup"><span data-stu-id="16a5d-103">ExpressRoute workflows for circuit provisioning and circuit states</span></span>
<span data-ttu-id="16a5d-104">Bu sayfayı hello hizmet sağlama ve yüksek düzeyde yönlendirme yapılandırması iş akışları size yol göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="16a5d-104">This page walks you through hello service provisioning and routing configuration workflows at a high level.</span></span>

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

<span data-ttu-id="16a5d-105">Merhaba aşağıdaki şekilde ve ilgili adımlarda hello görevleri bir ExpressRoute bağlantı hattı sağlanan uçtan uca sipariş toohave izlemelisiniz gösterin.</span><span class="sxs-lookup"><span data-stu-id="16a5d-105">hello following figure and corresponding steps show hello tasks you must follow in order toohave an ExpressRoute circuit provisioned end-to-end.</span></span> 

1. <span data-ttu-id="16a5d-106">PowerShell tooconfigure bir expressroute bağlantı hattı kullanın.</span><span class="sxs-lookup"><span data-stu-id="16a5d-106">Use PowerShell tooconfigure an ExpressRoute circuit.</span></span> <span data-ttu-id="16a5d-107">Merhaba Hello yönergeleri izleyin [oluşturma ExpressRoute bağlantı hatları](expressroute-howto-circuit-classic.md) daha fazla ayrıntı için makale.</span><span class="sxs-lookup"><span data-stu-id="16a5d-107">Follow hello instructions in hello [Create ExpressRoute circuits](expressroute-howto-circuit-classic.md) article for more details.</span></span>
2. <span data-ttu-id="16a5d-108">Bağlantı hello hizmet sağlayıcısı'ndan sipariş.</span><span class="sxs-lookup"><span data-stu-id="16a5d-108">Order connectivity from hello service provider.</span></span> <span data-ttu-id="16a5d-109">Bu işlem değişir.</span><span class="sxs-lookup"><span data-stu-id="16a5d-109">This process varies.</span></span> <span data-ttu-id="16a5d-110">Nasıl hakkında daha fazla ayrıntı için bağlantı sağlayıcınıza başvurun tooorder bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="16a5d-110">Contact your connectivity provider for more details about how tooorder connectivity.</span></span>
3. <span data-ttu-id="16a5d-111">Merhaba hattı başarıyla hello expressroute bağlantı hattı sağlama durumu PowerShell aracılığıyla doğrulayarak sağlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="16a5d-111">Ensure that hello circuit has been provisioned successfully by verifying hello ExpressRoute circuit provisioning state through PowerShell.</span></span> 
4. <span data-ttu-id="16a5d-112">Yönlendirme etki alanlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="16a5d-112">Configure routing domains.</span></span> <span data-ttu-id="16a5d-113">Bağlantı sağlayıcınızdan sizin için Katman 3 yönetiyorsa hattı için yönlendirmeyi yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="16a5d-113">If your connectivity provider manages Layer 3 for you, they will configure routing for your circuit.</span></span> <span data-ttu-id="16a5d-114">Bağlantı sağlayıcınız yalnızca Katman 2 Hizmetleri sunuyorsa, hello açıklanan yönergeleri başına yönlendirme yapılandırmalısınız [yönlendirme gereksinimleri](expressroute-routing.md) ve [yönlendirme yapılandırması](expressroute-howto-routing-classic.md) sayfaları.</span><span class="sxs-lookup"><span data-stu-id="16a5d-114">If your connectivity provider only offers Layer 2 services, you must configure routing per guidelines described in hello [routing requirements](expressroute-routing.md) and [routing configuration](expressroute-howto-routing-classic.md) pages.</span></span>
   
   * <span data-ttu-id="16a5d-115">Azure özel eşlemeyi etkinleştirmesini - Bu eşleme tooconnect tooVMs etkinleştir / bulut Hizmetleri sanal ağlar içinde dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="16a5d-115">Enable Azure private peering - You must enable this peering tooconnect tooVMs / cloud services deployed within virtual networks.</span></span>
   * <span data-ttu-id="16a5d-116">Azure ortak eşleme enable - genel IP adresleri üzerinde barındırılan tooconnect tooAzure Hizmetleri isterseniz, Azure ortak eşleme etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="16a5d-116">Enable Azure public peering - You must enable Azure public peering if you wish tooconnect tooAzure services hosted on public IP addresses.</span></span> <span data-ttu-id="16a5d-117">Azure özel eşleme için varsayılan tooenable yönlendirme seçtiyseniz gereksinim tooaccess Azure kaynaklarını budur.</span><span class="sxs-lookup"><span data-stu-id="16a5d-117">This is a requirement tooaccess Azure resources if you have chosen tooenable default routing for Azure private peering.</span></span>
   * <span data-ttu-id="16a5d-118">Microsoft eşlemesi - etkinleştirmek bu tooaccess Office 365 ve Dynamics 365 etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="16a5d-118">Enable Microsoft peering - You must enable this tooaccess Office 365 and Dynamics 365.</span></span> 
     
     > [!IMPORTANT]
     > <span data-ttu-id="16a5d-119">Ayrı bir proxy sunucu kullan / kenar tooconnect tooMicrosoft için kullandığınız hello daha Internet hello sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="16a5d-119">You must ensure that you use a separate proxy / edge tooconnect tooMicrosoft than hello one you use for hello Internet.</span></span> <span data-ttu-id="16a5d-120">Hem ExpressRoute hem de hello Internet için aynı sınır asimetrik yönlendirme neden ve ağ bağlantı kesintileri neden hello kullanma.</span><span class="sxs-lookup"><span data-stu-id="16a5d-120">Using hello same edge for both ExpressRoute and hello Internet will cause asymmetric routing and cause connectivity outages for your network.</span></span>
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. <span data-ttu-id="16a5d-121">Sanal bağlama tooExpressRoute devreler ağları - sanal ağlar tooyour expressroute bağlantı hattı bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="16a5d-121">Linking virtual networks tooExpressRoute circuits - You can link virtual networks tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="16a5d-122">Yönergeleri izleyerek [toolink Vnet'ler](expressroute-howto-linkvnet-arm.md) tooyour hattı.</span><span class="sxs-lookup"><span data-stu-id="16a5d-122">Follow instructions [toolink VNets](expressroute-howto-linkvnet-arm.md) tooyour circuit.</span></span> <span data-ttu-id="16a5d-123">Bu sanal ağlar ya da olabilir hello hello expressroute bağlantı hattı olarak aynı Azure aboneliğinden veya farklı bir abonelikte olabilir.</span><span class="sxs-lookup"><span data-stu-id="16a5d-123">These VNets can either be in hello same Azure subscription as hello ExpressRoute circuit, or can be in a different subscription.</span></span>

## <a name="expressroute-circuit-provisioning-states"></a><span data-ttu-id="16a5d-124">Expressroute bağlantı hattı durumları sağlama</span><span class="sxs-lookup"><span data-stu-id="16a5d-124">ExpressRoute circuit provisioning states</span></span>
<span data-ttu-id="16a5d-125">Her expressroute bağlantı hattı iki durum vardır:</span><span class="sxs-lookup"><span data-stu-id="16a5d-125">Each ExpressRoute circuit has two states:</span></span>

* <span data-ttu-id="16a5d-126">Hizmet Sağlayıcısı sağlama durumu</span><span class="sxs-lookup"><span data-stu-id="16a5d-126">Service provider provisioning state</span></span>
* <span data-ttu-id="16a5d-127">Durum</span><span class="sxs-lookup"><span data-stu-id="16a5d-127">Status</span></span>

<span data-ttu-id="16a5d-128">Durum Microsoft'un sağlama durumunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="16a5d-128">Status represents Microsoft's provisioning state.</span></span> <span data-ttu-id="16a5d-129">Bir expressroute bağlantı hattı oluşturduğunuzda, bu özellik tooEnabled ayarlanır</span><span class="sxs-lookup"><span data-stu-id="16a5d-129">This property is set tooEnabled when you create an Expressroute circuit</span></span>

<span data-ttu-id="16a5d-130">Merhaba bağlantı Sağlayıcısı sağlama durumu hello bağlantı sağlayıcısı tarafında hello durumunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="16a5d-130">hello connectivity provider provisioning state represents hello state on hello connectivity provider's side.</span></span> <span data-ttu-id="16a5d-131">Ya da olabilir *NotProvisioned*, *sağlama*, veya *hazırlandı*.</span><span class="sxs-lookup"><span data-stu-id="16a5d-131">It can either be *NotProvisioned*, *Provisioning*, or *Provisioned*.</span></span> <span data-ttu-id="16a5d-132">Merhaba expressroute bağlantı hattı, toobe mümkün toouse için hazırlandı durumunda bu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="16a5d-132">hello ExpressRoute circuit must be in Provisioned state for you toobe able toouse it.</span></span>

### <a name="possible-states-of-an-expressroute-circuit"></a><span data-ttu-id="16a5d-133">Olası bir expressroute bağlantı hattı durumları</span><span class="sxs-lookup"><span data-stu-id="16a5d-133">Possible states of an ExpressRoute circuit</span></span>
<span data-ttu-id="16a5d-134">Bu bölümde bir expressroute bağlantı hattı için olası durumlar hello çıkışı listelenir.</span><span class="sxs-lookup"><span data-stu-id="16a5d-134">This section lists out hello possible states for an ExpressRoute circuit.</span></span>

<span data-ttu-id="16a5d-135">**Oluşturma sırasında**</span><span class="sxs-lookup"><span data-stu-id="16a5d-135">**At creation time**</span></span>

<span data-ttu-id="16a5d-136">Merhaba expressroute bağlantı hattı durumu kısa sürede, aşağıdaki hello hello PowerShell cmdlet toocreate hello expressroute bağlantı hattı çalıştırmak görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="16a5d-136">You will see hello ExpressRoute circuit in hello following state as soon as you run hello PowerShell cmdlet toocreate hello ExpressRoute circuit.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="16a5d-137">**Bağlantı sağlayıcı hello devre sağlama hello işleminde olduğunda**</span><span class="sxs-lookup"><span data-stu-id="16a5d-137">**When connectivity provider is in hello process of provisioning hello circuit**</span></span>

<span data-ttu-id="16a5d-138">Merhaba expressroute bağlantı hattı durumu kısa sürede, aşağıdaki hello hello hizmet anahtar toohello bağlantı sağlayıcı geçirmek görür ve sağlama işlemi hello başlamış olması.</span><span class="sxs-lookup"><span data-stu-id="16a5d-138">You will see hello ExpressRoute circuit in hello following state as soon as you pass hello service key toohello connectivity provider and they have started hello provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


<span data-ttu-id="16a5d-139">**Bağlantı sağlayıcı sağlama işlemi hello zaman tamamlandı**</span><span class="sxs-lookup"><span data-stu-id="16a5d-139">**When connectivity provider has completed hello provisioning process**</span></span>

<span data-ttu-id="16a5d-140">Göreceğiniz hello durumu hello bağlantı sağlayıcı hello sağlama işlemi tamamlandıktan hemen sonra aşağıdaki hello'daki expressroute bağlantı hattına.</span><span class="sxs-lookup"><span data-stu-id="16a5d-140">You will see hello ExpressRoute circuit in hello following state as soon as hello connectivity provider has completed hello provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

<span data-ttu-id="16a5d-141">Durumu hello hattı içinde toobe mümkün toouse için yalnızca hello sağlanmış ve etkin olduğundan.</span><span class="sxs-lookup"><span data-stu-id="16a5d-141">Provisioned and Enabled is hello only state hello circuit can be in for you toobe able toouse it.</span></span> <span data-ttu-id="16a5d-142">Bir katman 2 sağlayıcısı kullanıyorsanız, yalnızca bu durumda olduğunda, hattı için yönlendirmeyi yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="16a5d-142">If you are using a Layer 2 provider, you can configure routing for your circuit only when it is in this state.</span></span>

<span data-ttu-id="16a5d-143">**Bağlantı sağlayıcı hello hattı zaman sağlamayı kaldırma**</span><span class="sxs-lookup"><span data-stu-id="16a5d-143">**When connectivity provider is deprovisioning hello circuit**</span></span>

<span data-ttu-id="16a5d-144">Merhaba hizmet sağlayıcısı toodeprovision hello expressroute bağlantı hattı istediyseniz hello hattı hello hizmet sağlayıcısı hello sağlamayı kaldırma işlemi tamamlandıktan sonra durumu aşağıdaki toohello ayarlamak görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="16a5d-144">If you requested hello service provider toodeprovision hello ExpressRoute circuit, you will see hello circuit set toohello following state after hello service provider has completed hello deprovisioning process.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="16a5d-145">Toore etkinleştir seçebilirsiniz, gerekli ya da toodelete hello hattı PowerShell cmdlet'lerini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="16a5d-145">You can choose toore-enable it if needed, or run PowerShell cmdlets toodelete hello circuit.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="16a5d-146">Çalıştırırsanız hello hello ServiceProviderProvisioningState sağlama veya hazırlandı hello işlemi olduğunda PowerShell cmdlet toodelete hello hattı başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="16a5d-146">If you run hello PowerShell cmdlet toodelete hello circuit when hello ServiceProviderProvisioningState is Provisioning or Provisioned hello operation will fail.</span></span> <span data-ttu-id="16a5d-147">Lütfen, bağlantı sağlayıcısı toodeprovision hello expressroute bağlantı hattı ile ilk iş ve hello hattı silin.</span><span class="sxs-lookup"><span data-stu-id="16a5d-147">Please work with your connectivity provider toodeprovision hello ExpressRoute circuit first and then delete hello circuit.</span></span> <span data-ttu-id="16a5d-148">Merhaba PowerShell cmdlet toodelete hello hattı çalıştırana kadar Microsoft toobill hello hattı devam edecektir.</span><span class="sxs-lookup"><span data-stu-id="16a5d-148">Microsoft will continue toobill hello circuit until you run hello PowerShell cmdlet toodelete hello circuit.</span></span>
> 
> 

## <a name="routing-session-configuration-state"></a><span data-ttu-id="16a5d-149">Yönlendirme oturum yapılandırma durumu</span><span class="sxs-lookup"><span data-stu-id="16a5d-149">Routing session configuration state</span></span>
<span data-ttu-id="16a5d-150">Merhaba BGP sağlama durumu, hello BGP oturumu Microsoft edge hello üzerinde etkinleştirilirse bilmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="16a5d-150">hello BGP provisioning state lets you know if hello BGP session has been enabled on hello Microsoft edge.</span></span> <span data-ttu-id="16a5d-151">Merhaba durumu sizin için etkinleştirilmelidir toobe mümkün toouse hello eşleme.</span><span class="sxs-lookup"><span data-stu-id="16a5d-151">hello state must be enabled for you toobe able toouse hello peering.</span></span>

<span data-ttu-id="16a5d-152">Microsoft eşlemesi için özellikle önemli toocheck hello BGP oturumu durumu değil.</span><span class="sxs-lookup"><span data-stu-id="16a5d-152">It is important toocheck hello BGP session state especially for Microsoft peering.</span></span> <span data-ttu-id="16a5d-153">Toplama toohello BGP sağlama durumunda, yok adlı başka bir duruma *tanıtılan genel ön ekten durumu*.</span><span class="sxs-lookup"><span data-stu-id="16a5d-153">In addition toohello BGP provisioning state, there is another state called *advertised public prefixes state*.</span></span> <span data-ttu-id="16a5d-154">Merhaba tanıtılan genel ön ekten durumu olmalıdır *yapılandırılmış* durum hem, yönlendirme toowork uçtan uca ve hello BGP oturumu toobe için.</span><span class="sxs-lookup"><span data-stu-id="16a5d-154">hello advertised public prefixes state must be in *configured* state, both for hello BGP session toobe up and for your routing toowork end-to-end.</span></span> 

<span data-ttu-id="16a5d-155">Ortak önek durumu tooa ayarlanmış Hello tanıtılan varsa *gerekli doğrulama* durumunda, hello BGP oturumu etkin değil, hello öneklerini hello eşleşmedi bildirilen herhangi bir kayıt defterlerini yönlendirme hello sayı olarak.</span><span class="sxs-lookup"><span data-stu-id="16a5d-155">If hello advertised public prefix state is set tooa *validation needed* state, hello BGP session is not enabled, as hello advertised prefixes did not match hello AS number in any of hello routing registries.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="16a5d-156">Merhaba tanıtılan genel ön ek durum ise, *el ile doğrulama* durum ile bir destek bileti açmanız [Microsoft Destek](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) ve hello IP adreslerini tanıtılan boyunca kendi kanıt Otonom sistem numarası Hello ile ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="16a5d-156">If hello advertised public prefixes state is in *manual validation* state, you must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and provide evidence that you own hello IP addresses advertised along with hello associated Autonomous System number.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="16a5d-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="16a5d-157">Next steps</span></span>
* <span data-ttu-id="16a5d-158">ExpressRoute bağlantınızı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="16a5d-158">Configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="16a5d-159">ExpressRoute bağlantı hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="16a5d-159">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-arm.md)
  * [<span data-ttu-id="16a5d-160">Yönlendirmeyi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="16a5d-160">Configure routing</span></span>](expressroute-howto-routing-arm.md)
  * [<span data-ttu-id="16a5d-161">VNet tooan expressroute bağlantı hattı bağlantı</span><span class="sxs-lookup"><span data-stu-id="16a5d-161">Link a VNet tooan ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

