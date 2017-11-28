---
title: "Nasıl tooconfigure (eşleme) bir expressroute bağlantı hattı için yönlendirmeyi: Resource Manager: Azure | Microsoft Docs"
description: "Bu makalede, oluşturma ve sağlama hello özel, genel ve Microsoft bir expressroute bağlantı hattı eşlemesi hello adım adım anlatılmaktadır. Bu makalede ayrıca nasıl toocheck hello durumu, güncelleştirme veya bağlantı hattınız için eşlemeleri silme gösterilmektedir."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c2a7ed2-ae5c-4e49-81f6-77cf9f2b2ac9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: a8ca25f488dde728cb3b06cd2c91873f3069feaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a><span data-ttu-id="f8528-104">Oluşturma ve bir ExpressRoute bağlantı hattı için eşlemesini değiştirme</span><span class="sxs-lookup"><span data-stu-id="f8528-104">Create and modify peering for an ExpressRoute circuit</span></span>

<span data-ttu-id="f8528-105">Bu makalede, bir expressroute bağlantı hattı hello Azure portal kullanarak hello Resource Manager dağıtım modelinde için yönlendirme yapılandırması oluşturma ve yönetme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="f8528-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using hello Azure portal.</span></span> <span data-ttu-id="f8528-106">Ayrıca, hello durumu, güncelleştirme veya silme denetleyin ve bir expressroute bağlantı hattı için eşlemeler sağlamayı sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="f8528-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="f8528-107">Bağlantı hattınız ile toouse farklı yöntem toowork istiyorsanız, bir makale listesi aşağıdaki hello seçin:</span><span class="sxs-lookup"><span data-stu-id="f8528-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>


## <a name="configuration-prerequisites"></a><span data-ttu-id="f8528-108">Yapılandırma önkoşulları</span><span class="sxs-lookup"><span data-stu-id="f8528-108">Configuration prerequisites</span></span>

* <span data-ttu-id="f8528-109">Merhaba gözden geçirdiğinizden emin olun [Önkoşullar](expressroute-prerequisites.md) hello sayfasında [yönlendirme gereksinimleri](expressroute-routing.md) sayfası ve hello [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce sayfasında.</span><span class="sxs-lookup"><span data-stu-id="f8528-109">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="f8528-110">Etkin bir ExpressRoute bağlantı hattınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8528-110">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="f8528-111">Çok olarak Hello yönergeleri[bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-portal-resource-manager.md) ve devam etmeden önce bağlantı sağlayıcınız tarafından etkinleştirilen hello hattı sahip.</span><span class="sxs-lookup"><span data-stu-id="f8528-111">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="f8528-112">Merhaba expressroute bağlantı hattı, toobe mümkün toorun hello cmdlet'leri hello sonraki bölümlerde için sağlanmış ve etkin durumda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8528-112">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets in hello next sections.</span></span>
* <span data-ttu-id="f8528-113">Paylaşılan bir anahtar/MD5 karma değeri toouse düşünüyorsanız emin toouse bu hello sayısı tünel ve sınırı hello karakter tooa en fazla 25 her iki tarafında olması.</span><span class="sxs-lookup"><span data-stu-id="f8528-113">If you plan toouse a shared key/MD5 hash, be sure toouse this on both sides of hello tunnel and limit hello number of characters tooa maximum of 25.</span></span>

<span data-ttu-id="f8528-114">Bu yönergeler yalnızca Katman 2 bağlantı hizmetleri sunan hizmet sağlayıcıları ile oluşturulan toocircuits geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="f8528-114">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="f8528-115">Yönetilen sunan bir hizmet sağlayıcısı kullanıyorsanız, Katman 3 Hizmetleri (genellikle gibi bir IPVPN MPLS), bağlantı sağlayıcınız yönlendirmeyi sizin için yönetir ve yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="f8528-115">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f8528-116">Biz hello Hizmet Yönetimi Portalı aracılığıyla hizmet sağlayıcılar tarafından yapılandırılan eşlemeleri şu anda tanıtmıyoruz.</span><span class="sxs-lookup"><span data-stu-id="f8528-116">We currently do not advertise peerings configured by service providers through hello service management portal.</span></span> <span data-ttu-id="f8528-117">Bu özelliği yakında etkinleştirmek için çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="f8528-117">We are working on enabling this capability soon.</span></span> <span data-ttu-id="f8528-118">BGP eşlemelerini yapılandırmadan önce hizmet sağlayıcınıza başvurun.</span><span class="sxs-lookup"><span data-stu-id="f8528-118">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="f8528-119">Bir ExpressRoute bağlantı hattı için bir, iki veya üç eşlemenin tamamını (Azure özel, Azure ortak ve Microsoft) yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8528-119">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="f8528-120">Eşlemeleri seçtiğiniz herhangi bir sırayla yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8528-120">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="f8528-121">Bununla birlikte, her eşleme birer birer başlangıç yapılandırmasını tamamlayın emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8528-121">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="f8528-122">Azure özel eşlemesi</span><span class="sxs-lookup"><span data-stu-id="f8528-122">Azure private peering</span></span>

<span data-ttu-id="f8528-123">Bu bölümde, oluşturma, alma, güncelleştirme ve hello bir expressroute bağlantı hattı için Azure özel eşleme yapılandırmasını silme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="f8528-123">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="f8528-124">Azure özel eşleme toocreate</span><span class="sxs-lookup"><span data-stu-id="f8528-124">toocreate Azure private peering</span></span>

1. <span data-ttu-id="f8528-125">Merhaba expressroute bağlantı hattını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f8528-125">Configure hello ExpressRoute circuit.</span></span> <span data-ttu-id="f8528-126">Merhaba hattı tam olarak hello bağlantı sağlayıcı tarafından devam etmeden önce sağlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="f8528-126">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing.</span></span>

  ![Liste](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="f8528-128">Merhaba bağlantı hattı için Azure özel eşlemesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f8528-128">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="f8528-129">Merhaba sonraki adımlara devam etmeden önce aşağıdaki öğelerindeki hello sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="f8528-129">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="f8528-130">Bir/30 alt ağı hello birincil bağlantı için.</span><span class="sxs-lookup"><span data-stu-id="f8528-130">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="f8528-131">Merhaba alt ağ, sanal ağlar için ayrılmış herhangi bir adres alanının parçası olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="f8528-131">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="f8528-132">Bir/30 alt ağı hello ikincil bağlantı için.</span><span class="sxs-lookup"><span data-stu-id="f8528-132">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="f8528-133">Merhaba alt ağ, sanal ağlar için ayrılmış herhangi bir adres alanının parçası olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="f8528-133">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="f8528-134">Geçerli bir VLAN kimliği tooestablish bu eşlemenin.</span><span class="sxs-lookup"><span data-stu-id="f8528-134">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="f8528-135">Hiçbir diğer eşliği emin hello devredeki aynı VLAN kimliğini kullanan hello</span><span class="sxs-lookup"><span data-stu-id="f8528-135">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="f8528-136">Eşleme için AS numarası.</span><span class="sxs-lookup"><span data-stu-id="f8528-136">AS number for peering.</span></span> <span data-ttu-id="f8528-137">2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8528-137">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="f8528-138">Bu eşleme için özel bir AS numarası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8528-138">You can use a private AS number for this peering.</span></span> <span data-ttu-id="f8528-139">65515’i kullanmadığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f8528-139">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="f8528-140">**İsteğe bağlı -** toouse birini seçerseniz bir MD5 karma değeri.</span><span class="sxs-lookup"><span data-stu-id="f8528-140">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="f8528-141">Hello aşağıdaki örnekte gösterildiği gibi Hello Azure özel eşleme satırını seçin:</span><span class="sxs-lookup"><span data-stu-id="f8528-141">Select hello Azure Private peering row, as shown in hello following example:</span></span>

  ![Özel](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. <span data-ttu-id="f8528-143">Özel eşleme oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f8528-143">Configure private peering.</span></span> <span data-ttu-id="f8528-144">Görüntü aşağıdaki hello bir yapılandırma örneği gösterilir:</span><span class="sxs-lookup"><span data-stu-id="f8528-144">hello following image shows a configuration example:</span></span>

  ![Özel eşleme oluşturun](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. <span data-ttu-id="f8528-146">Tüm parametreleri belirledikten sonra hello yapılandırmayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f8528-146">Save hello configuration once you have specified all parameters.</span></span> <span data-ttu-id="f8528-147">Merhaba yapılandırma başarıyla kabul edildikten sonra aşağıdaki örneğine benzeri toohello bakın:</span><span class="sxs-lookup"><span data-stu-id="f8528-147">After hello configuration has been accepted successfully, you see something similar toohello following example:</span></span>

  ![Özel eşleme Kaydet](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="f8528-149">tooview Azure özel eşleme ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="f8528-149">tooview Azure private peering details</span></span>

<span data-ttu-id="f8528-150">Merhaba eşlemeyi seçerek Azure özel eşleme özelliklerini hello görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8528-150">You can view hello properties of Azure private peering by selecting hello peering.</span></span>

![Özel eşleme görüntüleyin](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="f8528-152">Azure özel eşleme yapılandırmasını tooupdate</span><span class="sxs-lookup"><span data-stu-id="f8528-152">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="f8528-153">Eşleme için başlangıç satırı seçin ve hello eşleme özelliklerini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8528-153">You can select hello row for peering and modify hello peering properties.</span></span>

![Özel eşleme güncelleştir](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="f8528-155">Azure özel eşleme toodelete</span><span class="sxs-lookup"><span data-stu-id="f8528-155">toodelete Azure private peering</span></span>

<span data-ttu-id="f8528-156">Görüntü aşağıdaki hello gösterildiği gibi hello Sil simgesini seçerek eşleme yapılandırmanızı kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f8528-156">You can remove your peering configuration by selecting hello delete icon, as shown in hello following image:</span></span>

![Özel eşleme Sil](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a><span data-ttu-id="f8528-158">Azure ortak eşleme</span><span class="sxs-lookup"><span data-stu-id="f8528-158">Azure public peering</span></span>

<span data-ttu-id="f8528-159">Bu bölümde, oluşturma, alma, güncelleştirme ve hello bir expressroute bağlantı hattı için Azure ortak eşleme yapılandırmasını silme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="f8528-159">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="f8528-160">Azure ortak eşleme toocreate</span><span class="sxs-lookup"><span data-stu-id="f8528-160">toocreate Azure public peering</span></span>

1. <span data-ttu-id="f8528-161">ExpressRoute bağlantı hattını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f8528-161">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="f8528-162">Merhaba hattı tam olarak hello bağlantı sağlayıcı tarafından daha fazla devam etmeden önce sağlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="f8528-162">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing further.</span></span>

  ![Ortak eşleme listesi](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="f8528-164">Merhaba bağlantı hattı için Azure ortak eşlemesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f8528-164">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="f8528-165">Merhaba sonraki adımlara devam etmeden önce aşağıdaki öğelerindeki hello sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="f8528-165">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="f8528-166">Bir/30 alt ağı hello birincil bağlantı için.</span><span class="sxs-lookup"><span data-stu-id="f8528-166">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="f8528-167">Bu geçerli bir ortak IPv4 öneki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f8528-167">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="f8528-168">Bir/30 alt ağı hello ikincil bağlantı için.</span><span class="sxs-lookup"><span data-stu-id="f8528-168">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="f8528-169">Bu geçerli bir ortak IPv4 öneki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f8528-169">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="f8528-170">Geçerli bir VLAN kimliği tooestablish bu eşlemenin.</span><span class="sxs-lookup"><span data-stu-id="f8528-170">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="f8528-171">Hiçbir diğer eşliği emin hello devredeki aynı VLAN kimliğini kullanan hello</span><span class="sxs-lookup"><span data-stu-id="f8528-171">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="f8528-172">Eşleme için AS numarası.</span><span class="sxs-lookup"><span data-stu-id="f8528-172">AS number for peering.</span></span> <span data-ttu-id="f8528-173">2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8528-173">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="f8528-174">**İsteğe bağlı -** toouse birini seçerseniz bir MD5 karma değeri.</span><span class="sxs-lookup"><span data-stu-id="f8528-174">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="f8528-175">Görüntü aşağıdaki hello gösterildiği gibi Hello Azure ortak eşleme satırını seçin:</span><span class="sxs-lookup"><span data-stu-id="f8528-175">Select hello Azure public peering row, as shown in hello following image:</span></span>

  ![Ortak eşleme satırını seçin](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. <span data-ttu-id="f8528-177">Ortak eşlemeyi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f8528-177">Configure public peering.</span></span> <span data-ttu-id="f8528-178">Görüntü aşağıdaki hello bir yapılandırma örneği gösterilir:</span><span class="sxs-lookup"><span data-stu-id="f8528-178">hello following image shows a configuration example:</span></span>

  ![Ortak eşlemeyi yapılandırın](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. <span data-ttu-id="f8528-180">Tüm parametreleri belirledikten sonra hello yapılandırmayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f8528-180">Save hello configuration once you have specified all parameters.</span></span> <span data-ttu-id="f8528-181">Merhaba yapılandırma başarıyla kabul edildikten sonra aşağıdaki örneğine benzeri toohello bakın:</span><span class="sxs-lookup"><span data-stu-id="f8528-181">After hello configuration has been accepted successfully, you see something similar toohello following example:</span></span>

  ![Ortak eşleme yapılandırmasını kaydedin](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="f8528-183">tooview Azure genel eşliği ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="f8528-183">tooview Azure public peering details</span></span>

<span data-ttu-id="f8528-184">Merhaba eşlemeyi seçerek Azure ortak eşleme özelliklerini hello görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8528-184">You can view hello properties of Azure public peering by selecting hello peering.</span></span>

![Ortak eşleme özelliklerini görüntüle](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="f8528-186">Azure ortak eşleme yapılandırmasını tooupdate</span><span class="sxs-lookup"><span data-stu-id="f8528-186">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="f8528-187">Eşleme için başlangıç satırı seçin ve hello eşleme özelliklerini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8528-187">You can select hello row for peering and modify hello peering properties.</span></span>

![Ortak eşleme satırını seçin](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="f8528-189">Azure ortak eşleme toodelete</span><span class="sxs-lookup"><span data-stu-id="f8528-189">toodelete Azure public peering</span></span>

<span data-ttu-id="f8528-190">Hello aşağıdaki örnekte gösterildiği gibi hello Sil simgesini seçerek eşleme yapılandırmanızı kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f8528-190">You can remove your peering configuration by selecting hello delete icon, as shown in hello following example:</span></span>

![Ortak eşleme Sil](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a><span data-ttu-id="f8528-192">Microsoft eşlemesi</span><span class="sxs-lookup"><span data-stu-id="f8528-192">Microsoft peering</span></span>

<span data-ttu-id="f8528-193">Bu bölümde, oluşturma, alma, güncelleştirme ve bir expressroute bağlantı hattı için Microsoft eşleme yapılandırmasını hello silme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="f8528-193">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8528-194">Önceki tooAugust 1 yapılandırılmış olan ExpressRoute bağlantı hatları Microsoft eşliği, yol filtreleri tanımlanmamış olsa bile 2017 hello Microsoft eşleme aracılığıyla tanıtılan tüm hizmet ön eklerin sahip olur.</span><span class="sxs-lookup"><span data-stu-id="f8528-194">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="f8528-195">Ve 1 Ağustos 2017 sonrasında yapılandırılmış ExpressRoute bağlantı hatları, Microsoft eşlemesi sahip olmaz tüm ön eklerin rota filtre bağlanana kadar tanıtılan toohello hattı.</span><span class="sxs-lookup"><span data-stu-id="f8528-195">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="f8528-196">Daha fazla bilgi için bkz: [Microsoft eşliği için rota filtresini Yapılandır](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f8528-196">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="f8528-197">toocreate Microsoft eşlemesi</span><span class="sxs-lookup"><span data-stu-id="f8528-197">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="f8528-198">ExpressRoute bağlantı hattını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f8528-198">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="f8528-199">Merhaba hattı tam olarak hello bağlantı sağlayıcı tarafından daha fazla devam etmeden önce sağlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="f8528-199">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing further.</span></span>

  ![Microsoft eşlemesi listesi](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="f8528-201">Microsoft Hello bağlantı hattı için eşlemesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f8528-201">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="f8528-202">Devam etmeden önce bilgilerini aşağıdaki hello sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f8528-202">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="f8528-203">Bir/30 alt ağı hello birincil bağlantı için.</span><span class="sxs-lookup"><span data-stu-id="f8528-203">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="f8528-204">Bu size ait ve bir RIR / IRR içinde kayıtlı bir geçerli ortak IPv4 ön eki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f8528-204">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="f8528-205">Bir/30 alt ağı hello ikincil bağlantı için.</span><span class="sxs-lookup"><span data-stu-id="f8528-205">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="f8528-206">Bu size ait ve bir RIR / IRR içinde kayıtlı bir geçerli ortak IPv4 ön eki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f8528-206">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="f8528-207">Geçerli bir VLAN kimliği tooestablish bu eşlemenin.</span><span class="sxs-lookup"><span data-stu-id="f8528-207">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="f8528-208">Hiçbir diğer eşliği emin hello devredeki aynı VLAN kimliğini kullanan hello</span><span class="sxs-lookup"><span data-stu-id="f8528-208">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="f8528-209">Eşleme için AS numarası.</span><span class="sxs-lookup"><span data-stu-id="f8528-209">AS number for peering.</span></span> <span data-ttu-id="f8528-210">2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8528-210">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="f8528-211">Tanıtılan önekler: listesini sağlamanız gerekir tüm ön eklerin hello BGP oturumu üzerinden tooadvertise planlayın.</span><span class="sxs-lookup"><span data-stu-id="f8528-211">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="f8528-212">Yalnızca ortak IP adresi ön ekleri kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="f8528-212">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="f8528-213">Toosend ön ek kümesi planlıyorsanız, virgülle ayrılmış bir liste gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8528-213">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="f8528-214">Bu ön eklerin bir RIR içinde kayıtlı tooyou olmalıdır / IRR.</span><span class="sxs-lookup"><span data-stu-id="f8528-214">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="f8528-215">**İsteğe bağlı -** müşteri ASN'si: eşleme AS numarasına kayıtlı toohello olmayan önekler Tanıtıyorsanız, kayıtlı oldukları numara toowhich hello belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8528-215">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="f8528-216">Yönlendirme kayıt defteri adı: Merhaba RIR belirtebilirsiniz / hangi hello karşı AS numarası ve önekleri IRR kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="f8528-216">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="f8528-217">**İsteğe bağlı -** toouse birini seçerseniz bir MD5 karma değeri.</span><span class="sxs-lookup"><span data-stu-id="f8528-217">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="f8528-218">Merhaba tooconfigure, istediğiniz hello aşağıdaki gösterildiği gibi eşliği seçebilirsiniz örnek.</span><span class="sxs-lookup"><span data-stu-id="f8528-218">You can select hello peering you wish tooconfigure, as shown in hello following example.</span></span> <span data-ttu-id="f8528-219">Merhaba Microsoft eşleme satırını seçin.</span><span class="sxs-lookup"><span data-stu-id="f8528-219">Select hello Microsoft peering row.</span></span>

  ![Microsoft eşleme satırını seçin](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. <span data-ttu-id="f8528-221">Microsoft eşlemesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f8528-221">Configure Microsoft peering.</span></span> <span data-ttu-id="f8528-222">Görüntü aşağıdaki hello bir yapılandırma örneği gösterilir:</span><span class="sxs-lookup"><span data-stu-id="f8528-222">hello following image shows a configuration example:</span></span>

  ![Microsoft eşlemesini yapılandırın](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. <span data-ttu-id="f8528-224">Tüm parametreleri belirledikten sonra hello yapılandırmayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f8528-224">Save hello configuration once you have specified all parameters.</span></span>

  <span data-ttu-id="f8528-225">Bağlantı hattınız 'doğrulama gerekli' tooa alırsa (Merhaba görüntüde gösterildiği gibi) durumunda, bir destek bileti tooshow hello öneklerini tooour destek ekibi sahipliğini kanıtını açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8528-225">If your circuit gets tooa 'Validation needed' state (as shown in hello image), you must open a support ticket tooshow proof of ownership of hello prefixes tooour support team.</span></span>

  ![Microsoft eşleme yapılandırmasını kaydedin](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  <span data-ttu-id="f8528-227">Hello aşağıdaki örnekte gösterildiği gibi bir destek bileti doğrudan hello portalından açabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f8528-227">You can open a support ticket directly from hello portal, as shown in hello following example:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. <span data-ttu-id="f8528-228">Merhaba yapılandırma başarıyla kabul edildikten sonra görüntü aşağıdaki benzeri toohello bakın:</span><span class="sxs-lookup"><span data-stu-id="f8528-228">After hello configuration has been accepted successfully, you see something similar toohello following image:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="tooview-microsoft-peering-details"></a><span data-ttu-id="f8528-229">tooview Microsoft eşleme ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="f8528-229">tooview Microsoft peering details</span></span>

<span data-ttu-id="f8528-230">Merhaba eşlemeyi seçerek Azure ortak eşleme özelliklerini hello görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8528-230">You can view hello properties of Azure public peering by selecting hello peering.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="f8528-231">tooupdate Microsoft eşleme yapılandırması</span><span class="sxs-lookup"><span data-stu-id="f8528-231">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="f8528-232">Eşleme için başlangıç satırı seçin ve hello eşleme özelliklerini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8528-232">You can select hello row for peering and modify hello peering properties.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="f8528-233">toodelete Microsoft eşlemesi</span><span class="sxs-lookup"><span data-stu-id="f8528-233">toodelete Microsoft peering</span></span>

<span data-ttu-id="f8528-234">Görüntü aşağıdaki hello gösterildiği gibi hello Sil simgesini seçerek eşleme yapılandırmanızı kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f8528-234">You can remove your peering configuration by selecting hello delete icon, as shown in hello following image:</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a><span data-ttu-id="f8528-235">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f8528-235">Next steps</span></span>

<span data-ttu-id="f8528-236">Sonraki adım, [VNet tooan expressroute bağlantı hattı bağlantı](expressroute-howto-linkvnet-portal-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="f8528-236">Next step, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-portal-resource-manager.md)</span></span>
* <span data-ttu-id="f8528-237">ExpressRoute iş akışları hakkında daha fazla bilgi için bkz. [ExpressRoute iş akışları](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="f8528-237">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="f8528-238">Bağlantı hattı eşlemesi hakkında daha fazla bilgi için bkz. [ExpressRoute bağlantı hattı ve yönlendirme etki alanları](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="f8528-238">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="f8528-239">Sanal ağlarla çalışma hakkında daha fazla bilgi için bkz. [Sanal ağa genel bakış](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f8528-239">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
