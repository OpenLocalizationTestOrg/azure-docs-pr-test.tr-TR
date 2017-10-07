---
title: "Oluşturma ve bir expressroute bağlantı hattı değiştirme: Azure portal | Microsoft Docs"
description: "Bu makalede nasıl toocreate, sağlama, doğrulayın, güncelleştirme, silme ve bir expressroute bağlantı hattı yetkisini kaldırma açıklanmaktadır."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68d59d59-ed4d-482f-9cbc-534ebb090613
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/07/2017
ms.author: cherylmc;ganesr
ms.openlocfilehash: 200418aed6bdebace43a2f57cf532d1c8d13cb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a><span data-ttu-id="10800-103">Oluşturma ve bir expressroute bağlantı hattı değiştirme</span><span class="sxs-lookup"><span data-stu-id="10800-103">Create and modify an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="10800-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="10800-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="10800-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="10800-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="10800-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="10800-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="10800-107">Video - Azure portalı</span><span class="sxs-lookup"><span data-stu-id="10800-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="10800-108">PowerShell (klasik)</span><span class="sxs-lookup"><span data-stu-id="10800-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="10800-109">Bu makalede nasıl toocreate kullanarak bir Azure expressroute bağlantı hattı hello Azure portal ve hello Azure Resource Manager dağıtım modeli açıklanır.</span><span class="sxs-lookup"><span data-stu-id="10800-109">This article describes how toocreate an Azure ExpressRoute circuit by using hello Azure portal and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="10800-110">Ayrıca aşağıdaki adımları hello nasıl toocheck hello hello devrenin durumunu, güncelleştirin veya silin ve onu yetkisini kaldırma gösterir.</span><span class="sxs-lookup"><span data-stu-id="10800-110">hello following steps also show you how toocheck hello status of hello circuit, update it, or delete and deprovision it.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="10800-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="10800-111">Before you begin</span></span>
* <span data-ttu-id="10800-112">Gözden geçirme hello [Önkoşullar](expressroute-prerequisites.md) ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="10800-112">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="10800-113">Erişim toohello sahip olduğundan emin olun [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="10800-113">Ensure that you have access toohello [Azure portal](https://portal.azure.com).</span></span>
* <span data-ttu-id="10800-114">İzinleri toocreate yeni ağ kaynaklarını olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="10800-114">Ensure that you have permissions toocreate new networking resources.</span></span> <span data-ttu-id="10800-115">Merhaba doğru izinler yoksa, hesap yöneticinize başvurun.</span><span class="sxs-lookup"><span data-stu-id="10800-115">Contact your account administrator if you do not have hello right permissions.</span></span>
* <span data-ttu-id="10800-116">Yapabilecekleriniz [bir video izlemek](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) toobetter sırayla başlamadan önce hello adımları anlayın.</span><span class="sxs-lookup"><span data-stu-id="10800-116">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) before beginning in order toobetter understand hello steps.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="10800-117">Oluşturma ve bir expressroute bağlantı hattı sağlama</span><span class="sxs-lookup"><span data-stu-id="10800-117">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-toohello-azure-portal"></a><span data-ttu-id="10800-118">1. Toohello Azure portalında oturum açın</span><span class="sxs-lookup"><span data-stu-id="10800-118">1. Sign in toohello Azure portal</span></span>
<span data-ttu-id="10800-119">Tarayıcıdan toohello gidin [Azure portal](http://portal.azure.com) ve Azure hesabınızla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="10800-119">From a browser, navigate toohello [Azure portal](http://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="2-create-a-new-expressroute-circuit"></a><span data-ttu-id="10800-120">2. Yeni bir expressroute bağlantı hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="10800-120">2. Create a new ExpressRoute circuit</span></span>
> [!IMPORTANT]
> <span data-ttu-id="10800-121">ExpressRoute bağlantı hattınız bir hizmet anahtarı verilen hello andan itibaren Fatura edilecek.</span><span class="sxs-lookup"><span data-stu-id="10800-121">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="10800-122">Merhaba bağlantı sağlayıcı hazır tooprovision hello hattı olduğunda bu işlemi gerçekleştirmek emin olun.</span><span class="sxs-lookup"><span data-stu-id="10800-122">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

1. <span data-ttu-id="10800-123">Yeni bir kaynak hello seçeneği toocreate seçerek bir expressroute bağlantı hattı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10800-123">You can create an ExpressRoute circuit by selecting hello option toocreate a new resource.</span></span> <span data-ttu-id="10800-124">Tıklatın **yeni** > **ağ** > **ExpressRoute**hello görüntü aşağıdaki gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="10800-124">Click **New** > **Networking** > **ExpressRoute**, as shown in hello following image:</span></span>
   
    ![ExpressRoute bağlantı hattı oluşturma](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. <span data-ttu-id="10800-126">Tıklattıktan sonra **ExpressRoute**, hello görürsünüz **oluşturma expressroute bağlantı hattı** dikey.</span><span class="sxs-lookup"><span data-stu-id="10800-126">After you click **ExpressRoute**, you'll see hello **Create ExpressRoute circuit** blade.</span></span> <span data-ttu-id="10800-127">Bu dikey penceresinde hello değerleri doldurma sırasında hello doğru SKU katmanı ve ölçüm verilerini belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="10800-127">When you're filling in hello values on this blade, make sure that you specify hello correct SKU tier and data metering.</span></span>
   
   * <span data-ttu-id="10800-128">**Katman** bir expressroute bağlantı standart ExpressRoute premium Eklentisi etkin olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="10800-128">**Tier** determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="10800-129">Belirleyebileceğiniz **standart** tooget hello standart SKU veya **Premium** hello premium eklenti için.</span><span class="sxs-lookup"><span data-stu-id="10800-129">You can specify **Standard** tooget hello standard SKU or **Premium** for hello premium add-on.</span></span>
   * <span data-ttu-id="10800-130">**Ölçüm verilerini** hello faturalama türü belirler.</span><span class="sxs-lookup"><span data-stu-id="10800-130">**Data metering** determines hello billing type.</span></span> <span data-ttu-id="10800-131">Belirleyebileceğiniz **Metered** ölçülen veri planı için ve **sınırsız** sınırsız veri planı için.</span><span class="sxs-lookup"><span data-stu-id="10800-131">You can specify **Metered** for a metered data plan and **Unlimited** for an unlimited data plan.</span></span> <span data-ttu-id="10800-132">Merhaba fatura türünden değiştirebileceğinizi unutmayın **Metered** çok**sınırsız**, ancak hello türünden değiştiremezsiniz **sınırsız** çok**Metered**.</span><span class="sxs-lookup"><span data-stu-id="10800-132">Note that you can change hello billing type from **Metered** too**Unlimited**, but you can't change hello type from **Unlimited** too**Metered**.</span></span>
     
     ![Merhaba SKU katmanı ve ölçüm verilerini Yapılandır](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> <span data-ttu-id="10800-134">Lütfen bu hello eşleme konumu gösterir hello unutmayın [fiziksel konumu](expressroute-locations.md) Burada sizin eşlemeyi Microsoft ile.</span><span class="sxs-lookup"><span data-stu-id="10800-134">Please be aware that hello Peering Location indicates hello [physical location](expressroute-locations.md) where you are peering with Microsoft.</span></span> <span data-ttu-id="10800-135">Bu **değil** çok bağlantılı hello Azure ağ kaynak sağlayıcısı bulunduğu toohello Coğrafya başvuruyor "Konum" özelliği.</span><span class="sxs-lookup"><span data-stu-id="10800-135">This is **not** linked too"Location" property, which refers toohello geography where hello Azure Network Resource Provider is located.</span></span> <span data-ttu-id="10800-136">Bunlar ilişkili olsa da, iyi bir uygulama toochoose ağ kaynak sağlayıcısı coğrafi olarak Kapat toohello hello hattı eşlemesi konumunu durumdur.</span><span class="sxs-lookup"><span data-stu-id="10800-136">While they are not related, it is a good practice toochoose a Network Resource Provider geographically close toohello Peering Location of hello circuit.</span></span> 
> 
> 

### <a name="3-view-hello-circuits-and-properties"></a><span data-ttu-id="10800-137">3. Görünüm hello devreler ve özellikleri</span><span class="sxs-lookup"><span data-stu-id="10800-137">3. View hello circuits and properties</span></span>
<span data-ttu-id="10800-138">**Tüm hello devreler görüntüleyin**</span><span class="sxs-lookup"><span data-stu-id="10800-138">**View all hello circuits**</span></span>

<span data-ttu-id="10800-139">Seçerek oluşturulan tüm hello devreler görüntüleyebilirsiniz **tüm kaynakları** hello sol taraftaki menüsünde.</span><span class="sxs-lookup"><span data-stu-id="10800-139">You can view all hello circuits that you created by selecting **All resources** on hello left-side menu.</span></span>

![Görünüm bağlantı hatları](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

<span data-ttu-id="10800-141">**Merhaba özellikleri görüntüle**</span><span class="sxs-lookup"><span data-stu-id="10800-141">**View hello properties**</span></span>

    You can view hello properties of hello circuit by selecting it. On this blade, note hello service key for hello circuit. You must copy hello circuit key for your circuit and pass it down toohello service provider toocomplete hello provisioning process. hello circuit key is specific tooyour circuit.

![Özellikleri görüntüle](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="10800-143">4. Merhaba hizmet anahtar tooyour bağlantı sağlayıcı sağlamak için Gönder</span><span class="sxs-lookup"><span data-stu-id="10800-143">4. Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="10800-144">Bu dikey penceredeki **sağlayıcı durumu** hello hizmet sağlayıcı tarafında sağlama hello geçerli durumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="10800-144">On this blade, **Provider status** provides information on hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="10800-145">**Hattı durum** Microsoft yan hello üzerinde hello durumunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="10800-145">**Circuit status** provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="10800-146">Merhaba hattı durumları sağlama hakkında daha fazla bilgi için bkz: [iş akışları](expressroute-workflows.md#expressroute-circuit-provisioning-states) makalesi.</span><span class="sxs-lookup"><span data-stu-id="10800-146">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="10800-147">Yeni bir expressroute bağlantı hattı oluşturduğunuzda, hello hattı durumu aşağıdaki hello olacaktır:</span><span class="sxs-lookup"><span data-stu-id="10800-147">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

<span data-ttu-id="10800-148">Sağlayıcı Durumu: sağlanmadı</span><span class="sxs-lookup"><span data-stu-id="10800-148">Provider status: Not provisioned</span></span><BR>
<span data-ttu-id="10800-149">Devre, durum: etkin</span><span class="sxs-lookup"><span data-stu-id="10800-149">Circuit status: Enabled</span></span>

![Sağlama işlemini başlatın](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

<span data-ttu-id="10800-151">Merhaba hattı hello bağlantı sağlayıcı için etkinleştirme işleminin hello olduğunda durumu aşağıdaki toohello değişir:</span><span class="sxs-lookup"><span data-stu-id="10800-151">hello circuit will change toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

<span data-ttu-id="10800-152">Sağlayıcı Durumu: sağlama</span><span class="sxs-lookup"><span data-stu-id="10800-152">Provider status: Provisioning</span></span><BR>
<span data-ttu-id="10800-153">Devre, durum: etkin</span><span class="sxs-lookup"><span data-stu-id="10800-153">Circuit status: Enabled</span></span>

<span data-ttu-id="10800-154">Toobe mümkün toouse için bir expressroute bağlantı hattı, durumu aşağıdaki hello olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="10800-154">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

<span data-ttu-id="10800-155">Sağlayıcı Durumu: sağlanan</span><span class="sxs-lookup"><span data-stu-id="10800-155">Provider status: Provisioned</span></span><BR>
<span data-ttu-id="10800-156">Devre, durum: etkin</span><span class="sxs-lookup"><span data-stu-id="10800-156">Circuit status: Enabled</span></span>

### <a name="5-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="10800-157">5. Merhaba durumunu ve hello hattı anahtar hello durumunu düzenli aralıklarla denetleyin</span><span class="sxs-lookup"><span data-stu-id="10800-157">5. Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="10800-158">Merhaba, içinde seçerek ilgileniyor hello hattı özelliklerini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10800-158">You can view hello properties of hello circuit that you're interested in by selecting it.</span></span> <span data-ttu-id="10800-159">Merhaba denetleyin **sağlayıcı durumu** ve çok taşımadığından emin olun**hazırlandı** devam etmeden önce.</span><span class="sxs-lookup"><span data-stu-id="10800-159">Check hello **Provider status** and ensure that it has moved too**Provisioned** before you continue.</span></span>

![Bağlantı hattı ve sağlayıcı durumu](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a><span data-ttu-id="10800-161">6. Yönlendirme yapılandırması oluşturma</span><span class="sxs-lookup"><span data-stu-id="10800-161">6. Create your routing configuration</span></span>
<span data-ttu-id="10800-162">Adım adım yönergeler için toohello bakın [expressroute bağlantı hattı yönlendirme yapılandırması](expressroute-howto-routing-portal-resource-manager.md) makale toocreate ve hattı eşlemeler değiştirin.</span><span class="sxs-lookup"><span data-stu-id="10800-162">For step-by-step instructions, refer toohello [ExpressRoute circuit routing configuration](expressroute-howto-routing-portal-resource-manager.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="10800-163">Bu yönergeler yalnızca Katman 2 bağlantı hizmetleri sunan hizmet sağlayıcıları ile oluşturulan toocircuits geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="10800-163">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="10800-164">Yönetilen sunan bir hizmet sağlayıcısı kullanıyorsanız, Katman 3 Hizmetleri (genellikle bir IP VPN, MPLS gibi), bağlantı sağlayıcınız yapılandırmak ve yönetmek için yönlendirme.</span><span class="sxs-lookup"><span data-stu-id="10800-164">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="7-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="10800-165">7. Sanal ağ tooan expressroute bağlantı hattı bağlantı</span><span class="sxs-lookup"><span data-stu-id="10800-165">7. Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="10800-166">Ardından, sanal ağ tooyour expressroute bağlantı hattı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="10800-166">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="10800-167">Kullanım hello [sanal bağlama ağları tooExpressRoute devreler](expressroute-howto-linkvnet-arm.md) hello Resource Manager dağıtım modeliyle çalışırken makalesi.</span><span class="sxs-lookup"><span data-stu-id="10800-167">Use hello [Linking virtual networks tooExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with hello Resource Manager deployment model.</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="10800-168">Bir expressroute bağlantı hattı Hello durumunu alma</span><span class="sxs-lookup"><span data-stu-id="10800-168">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="10800-169">Bir bağlantı hattı hello durumunu seçerek görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10800-169">You can view hello status of a circuit by selecting it.</span></span> 

![Bir expressroute bağlantı hattı durumu](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="10800-171">Bir expressroute bağlantı hattı değiştirme</span><span class="sxs-lookup"><span data-stu-id="10800-171">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="10800-172">Bağlantı etkilemeden belirli bir expressroute bağlantı hattı özelliklerini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10800-172">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="10800-173">Yapabileceğiniz kapalı kalma süresi ile aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="10800-173">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="10800-174">Etkinleştirmek veya devre dışı bir expressroute bağlantı hattı için ExpressRoute premium eklentisi.</span><span class="sxs-lookup"><span data-stu-id="10800-174">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="10800-175">Artış hello bant genişliği, expressroute bağlantı hattı var. kapasite kullanılabilir hello bağlantı noktasında sağlanır.</span><span class="sxs-lookup"><span data-stu-id="10800-175">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="10800-176">Önceki sürüme indirme bir bağlantı hattının bant genişliği hello Not desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="10800-176">Note that downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="10800-177">Ölçülen veri tooUnlimited veri planından ölçümü hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="10800-177">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="10800-178">Bu değişen hello ölçüm planından veri desteklenmiyor sınırsız veri tooMetered unutmayın.</span><span class="sxs-lookup"><span data-stu-id="10800-178">Note that changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="10800-179">Etkinleştirme ve devre dışı *izin Klasik işlemleri*.</span><span class="sxs-lookup"><span data-stu-id="10800-179">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="10800-180">Toohello sınırlar ve sınırlamalar hakkında daha fazla bilgi için bkz [ExpressRoute SSS](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="10800-180">For more information on limits and limitations, refer toohello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

<span data-ttu-id="10800-181">toomodify bir expressroute bağlantı hattı üzerinde hello tıklatın **yapılandırma** hello aşağıdaki çizimde gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="10800-181">toomodify an ExpressRoute circuit, click on hello **Configuration** as shown in hello figure below.</span></span>

![Bağlantı hattı değiştirme](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

<span data-ttu-id="10800-183">Merhaba bant genişliği, SKU, fatura modelini değiştirin ve klasik işlemleri hello yapılandırma dikey izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10800-183">You can modify hello bandwidth, SKU, billing model and allow classic operations within hello configuration blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="10800-184">Merhaba varolan bağlantı noktasında yetersiz kapasite ise toorecreate hello expressroute bağlantı hattı olabilir.</span><span class="sxs-lookup"><span data-stu-id="10800-184">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="10800-185">Varsa hiçbir ek kapasite kullanılabilir o konumda hello hattı yükseltemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="10800-185">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="10800-186">Bir expressroute bağlantı hattı kesintiye uğratmadan hello bant genişliği azaltma olamaz.</span><span class="sxs-lookup"><span data-stu-id="10800-186">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="10800-187">Bant genişliği eski sürüme düşürmeyi toodeprovision hello expressroute bağlantı hattı gerektirir ve yeni bir expressroute bağlantı hattı yeniden sağlayın.</span><span class="sxs-lookup"><span data-stu-id="10800-187">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> <span data-ttu-id="10800-188">Premium eklentisi devre dışı bırakma işlemi hello standart bağlantı hattı için izin daha büyük olan kaynakları kullanıyorsanız başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="10800-188">Disable premium add-on operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="10800-189">Sağlamayı kaldırmayı ve bir expressroute bağlantı hattı silme</span><span class="sxs-lookup"><span data-stu-id="10800-189">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="10800-190">Expressroute bağlantı hattı hello seçerek silebilirsiniz **silmek** simgesi.</span><span class="sxs-lookup"><span data-stu-id="10800-190">You can delete your ExpressRoute circuit by selecting hello **delete** icon.</span></span> <span data-ttu-id="10800-191">Merhaba aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="10800-191">Note hello following:</span></span>

* <span data-ttu-id="10800-192">Tüm sanal ağlardan hello expressroute bağlantı hattı bağlantısını gerekir.</span><span class="sxs-lookup"><span data-stu-id="10800-192">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="10800-193">Bu işlem başarısız olursa, herhangi bir sanal ağa bağlı olup olmadığını denetleyin toohello hattı.</span><span class="sxs-lookup"><span data-stu-id="10800-193">If this operation fails, check whether any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="10800-194">Merhaba ExpressRoute bağlantı hattı Hizmet Sağlayıcısı sağlama durumu ise **sağlama** veya **hazırlandı** kendi tarafında hizmet sağlayıcısı toodeprovision hello hattınız ile çalışmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="10800-194">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="10800-195">Biz tooreserve kaynakları devam edecek ve hello hizmet sağlayıcısı sağlamayı hello hattı tamamlandıktan ve bize bildiren kadar sizi faturalandırmak.</span><span class="sxs-lookup"><span data-stu-id="10800-195">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="10800-196">Merhaba hizmet sağlayıcısı hello hattı sağlaması kaldırılıyor. sağlaması değilse (Merhaba Hizmet Sağlayıcısı sağlama durumu çok ayarlamak**sağlanmadı**) hello hattı sonra silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10800-196">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="10800-197">Bu hello hattı için fatura durdurur</span><span class="sxs-lookup"><span data-stu-id="10800-197">This will stop billing for hello circuit</span></span>

## <a name="next-steps"></a><span data-ttu-id="10800-198">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="10800-198">Next steps</span></span>
<span data-ttu-id="10800-199">Bağlantı hattınız oluşturduktan sonra aşağıdaki hello emin olun:</span><span class="sxs-lookup"><span data-stu-id="10800-199">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="10800-200">Oluşturma ve expressroute bağlantı hattı için yönlendirmeyi değiştirme</span><span class="sxs-lookup"><span data-stu-id="10800-200">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-portal-resource-manager.md)
* [<span data-ttu-id="10800-201">Sanal ağ tooyour expressroute bağlantı hattı bağlantı</span><span class="sxs-lookup"><span data-stu-id="10800-201">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

