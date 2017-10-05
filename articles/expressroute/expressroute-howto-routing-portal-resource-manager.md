---
title: "Yönlendirme (bir ExpressRoute için eşliği) hattı yapılandırma: Resource Manager: Azure | Microsoft Docs"
description: "Bu makalede, bir ExpressRoute bağlantı hattı için özel, ortak ve Microsoft eşlemesinin nasıl oluşturulduğu ve sağlandığı adım adım anlatılmaktadır. Bu makalede ayrıca bağlantı hattınızın durumunu denetleme, bağlantı hattını güncelleştirme veya silme işlemlerinin nasıl yapıldığı da anlatılmaktadır."
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
ms.openlocfilehash: 55ccadfea55b8098ee58dcaef942f6ba54093665
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a><span data-ttu-id="9a859-104">Oluşturma ve bir ExpressRoute bağlantı hattı için eşlemesini değiştirme</span><span class="sxs-lookup"><span data-stu-id="9a859-104">Create and modify peering for an ExpressRoute circuit</span></span>

<span data-ttu-id="9a859-105">Bu makalede, Azure portalını kullanarak Resource Manager dağıtım modelinde bir expressroute bağlantı hattı için yönlendirme yapılandırması oluşturma ve yönetme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="9a859-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using the Azure portal.</span></span> <span data-ttu-id="9a859-106">Ayrıca, durumu, güncelleştirme veya silme denetleyin ve bir expressroute bağlantı hattı için eşlemeler sağlamayı sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="9a859-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="9a859-107">Bağlantı hattınız ile çalışmak için farklı bir yöntem kullanmak istiyorsanız, bir makale aşağıdaki listeden seçin:</span><span class="sxs-lookup"><span data-stu-id="9a859-107">If you want to use a different method to work with your circuit, select an article from the following list:</span></span>


## <a name="configuration-prerequisites"></a><span data-ttu-id="9a859-108">Yapılandırma önkoşulları</span><span class="sxs-lookup"><span data-stu-id="9a859-108">Configuration prerequisites</span></span>

* <span data-ttu-id="9a859-109">Yapılandırmaya başlamadan önce [önkoşullar](expressroute-prerequisites.md) sayfasını, [yönlendirme gereksinimleri](expressroute-routing.md) sayfasını ve [iş akışları](expressroute-workflows.md) sayfasını gözden geçirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="9a859-109">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="9a859-110">Etkin bir ExpressRoute bağlantı hattınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a859-110">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="9a859-111">Devam etmeden önce [ExpressRoute bağlantı hattı oluşturma](expressroute-howto-circuit-portal-resource-manager.md) yönergelerini izleyin ve bağlantı sağlayıcınızın bağlantı hattını etkinleştirmesini isteyin.</span><span class="sxs-lookup"><span data-stu-id="9a859-111">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="9a859-112">Expressroute bağlantı hattı, sonraki bölümlerde cmdlet'leri çalıştırılabilmesi sağlanmış ve etkin durumda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a859-112">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets in the next sections.</span></span>
* <span data-ttu-id="9a859-113">Paylaşılan bir anahtar/MD5 karma değeri kullanmayı planlıyorsanız, bu tünel her iki tarafında kullanın ve en fazla 25 karakter sayısını sınırlamak emin olun.</span><span class="sxs-lookup"><span data-stu-id="9a859-113">If you plan to use a shared key/MD5 hash, be sure to use this on both sides of the tunnel and limit the number of characters to a maximum of 25.</span></span>

<span data-ttu-id="9a859-114">Bu yönergeler yalnızca Katman 2 bağlantı hizmetleri sunan hizmet sağlayıcıları ile oluşturulan bağlantı hatları için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="9a859-114">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="9a859-115">Yönetilen sunan bir hizmet sağlayıcısı kullanıyorsanız, Katman 3 Hizmetleri (genellikle gibi bir IPVPN MPLS), bağlantı sağlayıcınız yönlendirmeyi sizin için yönetir ve yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="9a859-115">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9a859-116">Şu anda hizmet yönetim portalı aracılığıyla hizmet sağlayıcılar tarafından yapılandırılan eşlemeleri tanıtmıyoruz.</span><span class="sxs-lookup"><span data-stu-id="9a859-116">We currently do not advertise peerings configured by service providers through the service management portal.</span></span> <span data-ttu-id="9a859-117">Bu özelliği yakında etkinleştirmek için çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="9a859-117">We are working on enabling this capability soon.</span></span> <span data-ttu-id="9a859-118">BGP eşlemelerini yapılandırmadan önce hizmet sağlayıcınıza başvurun.</span><span class="sxs-lookup"><span data-stu-id="9a859-118">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="9a859-119">Bir ExpressRoute bağlantı hattı için bir, iki veya üç eşlemenin tamamını (Azure özel, Azure ortak ve Microsoft) yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a859-119">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="9a859-120">Eşlemeleri seçtiğiniz herhangi bir sırayla yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a859-120">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="9a859-121">Ancak, her eşlemenin yapılandırmasını birer birer tamamladığınızdan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a859-121">However, you must make sure that you complete the configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="9a859-122">Azure özel eşlemesi</span><span class="sxs-lookup"><span data-stu-id="9a859-122">Azure private peering</span></span>

<span data-ttu-id="9a859-123">Bu bölümde, oluşturma, alma, güncelleştirme ve bir expressroute bağlantı hattı için Azure özel eşleme yapılandırmasını silme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="9a859-123">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="9a859-124">Azure özel eşlemesi oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="9a859-124">To create Azure private peering</span></span>

1. <span data-ttu-id="9a859-125">ExpressRoute bağlantı hattını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9a859-125">Configure the ExpressRoute circuit.</span></span> <span data-ttu-id="9a859-126">Devam etmeden önce bağlantı sağlayıcı tarafından bağlantı hattının tam olarak sağlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="9a859-126">Ensure that the circuit is fully provisioned by the connectivity provider before continuing.</span></span>

  ![Liste](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="9a859-128">Bağlantı hattı için Azure özel eşlemesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9a859-128">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="9a859-129">Sonraki adımlara devam etmeden önce aşağıdaki öğelerin bulunduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="9a859-129">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="9a859-130">Birincil bağlantı için bir /30 alt ağı.</span><span class="sxs-lookup"><span data-stu-id="9a859-130">A /30 subnet for the primary link.</span></span> <span data-ttu-id="9a859-131">Alt ağ, sanal ağlar için ayrılmış herhangi bir adres alanının parçası olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="9a859-131">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="9a859-132">İkincil bağlantı için bir /30 alt ağı.</span><span class="sxs-lookup"><span data-stu-id="9a859-132">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="9a859-133">Alt ağ, sanal ağlar için ayrılmış herhangi bir adres alanının parçası olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="9a859-133">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="9a859-134">Bu eşlemenin kurulacağı geçerli bir VLAN kimliği.</span><span class="sxs-lookup"><span data-stu-id="9a859-134">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="9a859-135">Bağlantı hattındaki başka bir eşlemenin aynı VLAN kimliğini kullanmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="9a859-135">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="9a859-136">Eşleme için AS numarası.</span><span class="sxs-lookup"><span data-stu-id="9a859-136">AS number for peering.</span></span> <span data-ttu-id="9a859-137">2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a859-137">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="9a859-138">Bu eşleme için özel bir AS numarası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a859-138">You can use a private AS number for this peering.</span></span> <span data-ttu-id="9a859-139">65515’i kullanmadığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9a859-139">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="9a859-140">**İsteğe bağlı -** kullanmayı seçerseniz bir MD5 karma değeri.</span><span class="sxs-lookup"><span data-stu-id="9a859-140">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="9a859-141">Aşağıdaki örnekte gösterildiği gibi Azure Private eşleme satırını seçin:</span><span class="sxs-lookup"><span data-stu-id="9a859-141">Select the Azure Private peering row, as shown in the following example:</span></span>

  ![Özel](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. <span data-ttu-id="9a859-143">Özel eşleme oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9a859-143">Configure private peering.</span></span> <span data-ttu-id="9a859-144">Aşağıdaki resimde bir yapılandırma örneği gösterilir:</span><span class="sxs-lookup"><span data-stu-id="9a859-144">The following image shows a configuration example:</span></span>

  ![Özel eşleme oluşturun](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. <span data-ttu-id="9a859-146">Tüm parametreleri belirledikten sonra yapılandırmayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9a859-146">Save the configuration once you have specified all parameters.</span></span> <span data-ttu-id="9a859-147">Yapılandırma başarıyla kabul edildikten sonra aşağıdaki örneğe benzer bir şey görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="9a859-147">After the configuration has been accepted successfully, you see something similar to the following example:</span></span>

  ![Özel eşleme Kaydet](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="9a859-149">Azure özel eşleme ayrıntılarını görüntülemek için</span><span class="sxs-lookup"><span data-stu-id="9a859-149">To view Azure private peering details</span></span>

<span data-ttu-id="9a859-150">Eşlemeyi seçerek Azure özel eşleme özelliklerini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a859-150">You can view the properties of Azure private peering by selecting the peering.</span></span>

![Özel eşleme görüntüleyin](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="9a859-152">Azure özel eşleme yapılandırmasını güncelleştirmek için</span><span class="sxs-lookup"><span data-stu-id="9a859-152">To update Azure private peering configuration</span></span>

<span data-ttu-id="9a859-153">Eşleme için satırı seçebilir ve eşleme özelliklerini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a859-153">You can select the row for peering and modify the peering properties.</span></span>

![Özel eşleme güncelleştir](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="9a859-155">Azure özel eşlemeyi silmek için</span><span class="sxs-lookup"><span data-stu-id="9a859-155">To delete Azure private peering</span></span>

<span data-ttu-id="9a859-156">Aşağıdaki görüntüde gösterildiği gibi silme simgesini seçerek eşleme yapılandırmanızı kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9a859-156">You can remove your peering configuration by selecting the delete icon, as shown in the following image:</span></span>

![Özel eşleme Sil](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a><span data-ttu-id="9a859-158">Azure ortak eşleme</span><span class="sxs-lookup"><span data-stu-id="9a859-158">Azure public peering</span></span>

<span data-ttu-id="9a859-159">Bu bölümde, oluşturma, alma, güncelleştirme ve bir expressroute bağlantı hattı için Azure ortak eşleme yapılandırmasını silme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="9a859-159">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="9a859-160">Azure ortak eşlemesi oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="9a859-160">To create Azure public peering</span></span>

1. <span data-ttu-id="9a859-161">ExpressRoute bağlantı hattını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9a859-161">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="9a859-162">Daha ileriye devam etmeden önce bağlantı sağlayıcı tarafından bağlantı hattının tam olarak sağlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="9a859-162">Ensure that the circuit is fully provisioned by the connectivity provider before continuing further.</span></span>

  ![Ortak eşleme listesi](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="9a859-164">Bağlantı hattı için Azure ortak eşlemesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9a859-164">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="9a859-165">Sonraki adımlara devam etmeden önce aşağıdaki öğelerin bulunduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="9a859-165">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="9a859-166">Birincil bağlantı için bir /30 alt ağı.</span><span class="sxs-lookup"><span data-stu-id="9a859-166">A /30 subnet for the primary link.</span></span> <span data-ttu-id="9a859-167">Bu geçerli bir ortak IPv4 öneki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9a859-167">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="9a859-168">İkincil bağlantı için bir /30 alt ağı.</span><span class="sxs-lookup"><span data-stu-id="9a859-168">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="9a859-169">Bu geçerli bir ortak IPv4 öneki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9a859-169">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="9a859-170">Bu eşlemenin kurulacak geçerli bir VLAN kimliği.</span><span class="sxs-lookup"><span data-stu-id="9a859-170">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="9a859-171">Bağlantı hattındaki başka bir eşlemenin aynı VLAN kimliğini kullanmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="9a859-171">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="9a859-172">Eşleme için AS numarası.</span><span class="sxs-lookup"><span data-stu-id="9a859-172">AS number for peering.</span></span> <span data-ttu-id="9a859-173">2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a859-173">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="9a859-174">**İsteğe bağlı -** kullanmayı seçerseniz bir MD5 karma değeri.</span><span class="sxs-lookup"><span data-stu-id="9a859-174">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="9a859-175">Aşağıdaki görüntüde gösterildiği gibi Azure public eşleme satırını seçin:</span><span class="sxs-lookup"><span data-stu-id="9a859-175">Select the Azure public peering row, as shown in the following image:</span></span>

  ![Ortak eşleme satırını seçin](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. <span data-ttu-id="9a859-177">Ortak eşlemeyi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9a859-177">Configure public peering.</span></span> <span data-ttu-id="9a859-178">Aşağıdaki resimde bir yapılandırma örneği gösterilir:</span><span class="sxs-lookup"><span data-stu-id="9a859-178">The following image shows a configuration example:</span></span>

  ![Ortak eşlemeyi yapılandırın](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. <span data-ttu-id="9a859-180">Tüm parametreleri belirledikten sonra yapılandırmayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9a859-180">Save the configuration once you have specified all parameters.</span></span> <span data-ttu-id="9a859-181">Yapılandırma başarıyla kabul edildikten sonra aşağıdaki örneğe benzer bir şey görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="9a859-181">After the configuration has been accepted successfully, you see something similar to the following example:</span></span>

  ![Ortak eşleme yapılandırmasını kaydedin](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="9a859-183">Azure ortak eşleme ayrıntılarını görüntülemek için</span><span class="sxs-lookup"><span data-stu-id="9a859-183">To view Azure public peering details</span></span>

<span data-ttu-id="9a859-184">Eşlemeyi seçerek Azure ortak eşleme özelliklerini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a859-184">You can view the properties of Azure public peering by selecting the peering.</span></span>

![Ortak eşleme özelliklerini görüntüle](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="9a859-186">Azure ortak eşleme yapılandırmasını güncelleştirmek için</span><span class="sxs-lookup"><span data-stu-id="9a859-186">To update Azure public peering configuration</span></span>

<span data-ttu-id="9a859-187">Eşleme için satırı seçebilir ve eşleme özelliklerini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a859-187">You can select the row for peering and modify the peering properties.</span></span>

![Ortak eşleme satırını seçin](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="9a859-189">Azure ortak eşlemesini silmek için</span><span class="sxs-lookup"><span data-stu-id="9a859-189">To delete Azure public peering</span></span>

<span data-ttu-id="9a859-190">Aşağıdaki örnekte gösterildiği gibi silme simgesini seçerek eşleme yapılandırmanızı kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9a859-190">You can remove your peering configuration by selecting the delete icon, as shown in the following example:</span></span>

![Ortak eşleme Sil](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a><span data-ttu-id="9a859-192">Microsoft eşlemesi</span><span class="sxs-lookup"><span data-stu-id="9a859-192">Microsoft peering</span></span>

<span data-ttu-id="9a859-193">Bu bölümde, oluşturma, alma, güncelleştirme ve bir expressroute bağlantı hattı için Microsoft eşleme yapılandırmasını silme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="9a859-193">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9a859-194">1 Ağustos 2017 önce yapılandırılmış olan ExpressRoute bağlantı hatları, Microsoft eşlemesi yol filtreleri tanımlanmamış olsa bile eşleme, Microsoft tarafından tanıtılan tüm hizmet ön eklerin sahip olur.</span><span class="sxs-lookup"><span data-stu-id="9a859-194">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through the Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="9a859-195">Ve 1 Ağustos 2017 sonrasında yapılandırılmış ExpressRoute bağlantı hatları, Microsoft eşlemesi sahip olmaz tüm ön eklerin rota filtre devresine bağlanana kadar tanıtılan.</span><span class="sxs-lookup"><span data-stu-id="9a859-195">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span> <span data-ttu-id="9a859-196">Daha fazla bilgi için bkz: [Microsoft eşliği için rota filtresini Yapılandır](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9a859-196">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="9a859-197">Microsoft eşlemesi oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="9a859-197">To create Microsoft peering</span></span>

1. <span data-ttu-id="9a859-198">ExpressRoute bağlantı hattını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9a859-198">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="9a859-199">Daha ileriye devam etmeden önce bağlantı sağlayıcı tarafından bağlantı hattının tam olarak sağlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="9a859-199">Ensure that the circuit is fully provisioned by the connectivity provider before continuing further.</span></span>

  ![Microsoft eşlemesi listesi](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="9a859-201">Bağlantı hattı için Microsoft eşlemesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9a859-201">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="9a859-202">Devam etmeden önce aşağıdaki bilgilere sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9a859-202">Make sure that you have the following information before you proceed.</span></span>

  * <span data-ttu-id="9a859-203">Birincil bağlantı için bir /30 alt ağı.</span><span class="sxs-lookup"><span data-stu-id="9a859-203">A /30 subnet for the primary link.</span></span> <span data-ttu-id="9a859-204">Bu size ait ve bir RIR / IRR içinde kayıtlı bir geçerli ortak IPv4 ön eki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9a859-204">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="9a859-205">İkincil bağlantı için bir /30 alt ağı.</span><span class="sxs-lookup"><span data-stu-id="9a859-205">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="9a859-206">Bu size ait ve bir RIR / IRR içinde kayıtlı bir geçerli ortak IPv4 ön eki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9a859-206">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="9a859-207">Bu eşlemenin kurulacağı geçerli bir VLAN kimliği.</span><span class="sxs-lookup"><span data-stu-id="9a859-207">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="9a859-208">Bağlantı hattındaki başka bir eşlemenin aynı VLAN kimliğini kullanmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="9a859-208">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="9a859-209">Eşleme için AS numarası.</span><span class="sxs-lookup"><span data-stu-id="9a859-209">AS number for peering.</span></span> <span data-ttu-id="9a859-210">2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a859-210">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="9a859-211">Tanıtılan önekler: BGP oturumunda tanıtmayı planladığınız tüm öneklerin bir listesini sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a859-211">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="9a859-212">Yalnızca ortak IP adresi ön ekleri kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="9a859-212">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="9a859-213">Bir ön ek kümesi göndermeyi planlıyorsanız, virgülle ayrılmış bir liste gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a859-213">If you plan to send a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="9a859-214">Bu ön ekler size bir RIR / IRR içinde kaydedilmiş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9a859-214">These prefixes must be registered to you in an RIR / IRR.</span></span>
  * <span data-ttu-id="9a859-215">**İsteğe bağlı -** müşteri ASN'si: eşleme AS numarasına kayıtlı olmayan önekler Tanıtıyorsanız, kayıtlı oldukları AS numarasını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a859-215">**Optional -** Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span>
  * <span data-ttu-id="9a859-216">Yönlendirme Kayıt Defteri Adı: AS numarası ve öneklerinin kaydedildiği RIR / IRR’yi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a859-216">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="9a859-217">**İsteğe bağlı -** kullanmayı seçerseniz bir MD5 karma değeri.</span><span class="sxs-lookup"><span data-stu-id="9a859-217">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="9a859-218">Aşağıdaki örnekte gösterildiği gibi yapılandırmak için istediğiniz eşlemeyi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a859-218">You can select the peering you wish to configure, as shown in the following example.</span></span> <span data-ttu-id="9a859-219">Microsoft eşleme satırını seçin.</span><span class="sxs-lookup"><span data-stu-id="9a859-219">Select the Microsoft peering row.</span></span>

  ![Microsoft eşleme satırını seçin](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. <span data-ttu-id="9a859-221">Microsoft eşlemesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9a859-221">Configure Microsoft peering.</span></span> <span data-ttu-id="9a859-222">Aşağıdaki resimde bir yapılandırma örneği gösterilir:</span><span class="sxs-lookup"><span data-stu-id="9a859-222">The following image shows a configuration example:</span></span>

  ![Microsoft eşlemesini yapılandırın](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. <span data-ttu-id="9a859-224">Tüm parametreleri belirledikten sonra yapılandırmayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9a859-224">Save the configuration once you have specified all parameters.</span></span>

  <span data-ttu-id="9a859-225">Bağlantı hattınız 'gerekli bir doğrulama' alır, (görüntüde gösterildiği gibi) durumunda, kanıtı destek ekibimize önekleri sahipliğini göstermek için bir destek bileti açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a859-225">If your circuit gets to a 'Validation needed' state (as shown in the image), you must open a support ticket to show proof of ownership of the prefixes to our support team.</span></span>

  ![Microsoft eşleme yapılandırmasını kaydedin](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  <span data-ttu-id="9a859-227">Aşağıdaki örnekte gösterildiği gibi bir destek bileti doğrudan portalından açabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9a859-227">You can open a support ticket directly from the portal, as shown in the following example:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. <span data-ttu-id="9a859-228">Yapılandırma başarıyla kabul edildikten sonra aşağıdaki görüntüye benzer bir şey görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="9a859-228">After the configuration has been accepted successfully, you see something similar to the following image:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="to-view-microsoft-peering-details"></a><span data-ttu-id="9a859-229">Microsoft eşleme ayrıntılarını görüntülemek için</span><span class="sxs-lookup"><span data-stu-id="9a859-229">To view Microsoft peering details</span></span>

<span data-ttu-id="9a859-230">Eşlemeyi seçerek Azure ortak eşleme özelliklerini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a859-230">You can view the properties of Azure public peering by selecting the peering.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="9a859-231">Microsoft eşlemesi yapılandırmasını güncelleştirmek için</span><span class="sxs-lookup"><span data-stu-id="9a859-231">To update Microsoft peering configuration</span></span>

<span data-ttu-id="9a859-232">Eşleme için satırı seçebilir ve eşleme özelliklerini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a859-232">You can select the row for peering and modify the peering properties.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="9a859-233">Microsoft eşlemesini silmek için</span><span class="sxs-lookup"><span data-stu-id="9a859-233">To delete Microsoft peering</span></span>

<span data-ttu-id="9a859-234">Aşağıdaki görüntüde gösterildiği gibi silme simgesini seçerek eşleme yapılandırmanızı kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9a859-234">You can remove your peering configuration by selecting the delete icon, as shown in the following image:</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a><span data-ttu-id="9a859-235">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9a859-235">Next steps</span></span>

<span data-ttu-id="9a859-236">Sonraki adım, [expressroute bağlantı hattına bir VNet bağlama](expressroute-howto-linkvnet-portal-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="9a859-236">Next step, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-portal-resource-manager.md)</span></span>
* <span data-ttu-id="9a859-237">ExpressRoute iş akışları hakkında daha fazla bilgi için bkz. [ExpressRoute iş akışları](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="9a859-237">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="9a859-238">Bağlantı hattı eşlemesi hakkında daha fazla bilgi için bkz. [ExpressRoute bağlantı hattı ve yönlendirme etki alanları](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="9a859-238">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="9a859-239">Sanal ağlarla çalışma hakkında daha fazla bilgi için bkz. [Sanal ağa genel bakış](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9a859-239">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
