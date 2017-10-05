---
title: "Azure ExpressRoute Microsoft eşliği için rota filtrelerini yapılandırın: portalı | Microsoft Docs"
description: "Bu makalede, Microsoft Azure portalını kullanarak Peering için yol filtrelerini yapılandırmak açıklar"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: f17bf3e475a33cfc617e8a026e9606b3792101f3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="539b6-103">Microsoft eşlemesi için rota filtreleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="539b6-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="539b6-104">Yol filtreleri Microsoft eşleme yoluyla desteklenen hizmetleri kümesini kullanmak için bir yoldur.</span><span class="sxs-lookup"><span data-stu-id="539b6-104">Route filters are a way to consume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="539b6-105">Bu makaledeki adımları yapılandırmak ve ExpressRoute bağlantı hatları için yol filtreleri yönetmenize yardımcı olması.</span><span class="sxs-lookup"><span data-stu-id="539b6-105">The steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="539b6-106">Dynamics 365 Hizmetleri ve Exchange Online, SharePoint Online ve Skype gibi Office 365 Hizmetleri iş için Microsoft eşleme aracılığıyla erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="539b6-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through the Microsoft peering.</span></span> <span data-ttu-id="539b6-107">Microsoft eşlemesi bir expressroute bağlantı hattı yapılandırıldığında, bu hizmetleri ile ilgili tüm ön eklerin oluşturulmuş BGP oturumları bildirilir.</span><span class="sxs-lookup"><span data-stu-id="539b6-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related to these services are advertised through the BGP sessions that are established.</span></span> <span data-ttu-id="539b6-108">BGP topluluk değeri öneki sunulan Hizmeti'ni tanımlamak için her ön eki eklenir.</span><span class="sxs-lookup"><span data-stu-id="539b6-108">A BGP community value is attached to every prefix to identify the service that is offered through the prefix.</span></span> <span data-ttu-id="539b6-109">BGP topluluk değerlerini ve eşlemek için Hizmetler listesi için bkz: [BGP toplulukları](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="539b6-109">For a list of the BGP community values and the services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="539b6-110">Tüm hizmetleri için bağlantı gerektiriyorsa, çok sayıda önekleri BGP bildirilir.</span><span class="sxs-lookup"><span data-stu-id="539b6-110">If you require connectivity to all services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="539b6-111">Bu, ağınızdaki yönlendiricileri tarafından tutulan yol tablolarını boyutunu önemli ölçüde artırır.</span><span class="sxs-lookup"><span data-stu-id="539b6-111">This significantly increases the size of the route tables maintained by routers within your network.</span></span> <span data-ttu-id="539b6-112">Yalnızca bir alt kümesini Microsoft eşliği ile sunulan hizmetlere kullanmayı planlıyorsanız, yol tablolarınız iki yolla boyutunu azaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="539b6-112">If you plan to consume only a subset of services offered through Microsoft peering, you can reduce the size of your route tables in two ways.</span></span> <span data-ttu-id="539b6-113">Şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="539b6-113">You can:</span></span>

- <span data-ttu-id="539b6-114">İstenmeyen önekleri BGP toplulukları yol filtreleri uygulayarak filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="539b6-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="539b6-115">Bu standart bir ağ uygulaması ve birçok ağ içinde yaygın olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="539b6-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="539b6-116">Rota filtrelerini tanımlayın ve bunları, expressroute bağlantı hattı uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="539b6-116">Define route filters and apply them to your ExpressRoute circuit.</span></span> <span data-ttu-id="539b6-117">Bir rota filtre Microsoft eşliği ile kullanmak için plan Hizmetleri listesini seçmenize izin veren yeni bir kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="539b6-117">A route filter is a new resource that lets you select the list of services you plan to consume through Microsoft peering.</span></span> <span data-ttu-id="539b6-118">ExpressRoute yönlendiriciler yalnızca rota filtrede tanımlanan hizmetlere ait önekleri listesini gönderir.</span><span class="sxs-lookup"><span data-stu-id="539b6-118">ExpressRoute routers only send the list of prefixes that belong to the services identified in the route filter.</span></span>

### <span data-ttu-id="539b6-119"><a name="about"></a>Rota filtreler hakkında</span><span class="sxs-lookup"><span data-stu-id="539b6-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="539b6-120">Microsoft eşlemesi, expressroute bağlantı hattı üzerinde yapılandırıldığında, sınır yönlendiricileri (sizin ya da bağlantı sağlayıcınızın) BGP oturumları çifti Microsoft sınır yönlendiricileri kurun.</span><span class="sxs-lookup"><span data-stu-id="539b6-120">When Microsoft peering is configured on your ExpressRoute circuit, the Microsoft edge routers establish a pair of BGP sessions with the edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="539b6-121">Yol yok, ağınıza bildirilir.</span><span class="sxs-lookup"><span data-stu-id="539b6-121">No routes are advertised to your network.</span></span> <span data-ttu-id="539b6-122">Yol tanıtımlarını ağınıza etkinleştirmek için bir rota filtre ilişkilendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="539b6-122">To enable route advertisements to your network, you must associate a route filter.</span></span>

<span data-ttu-id="539b6-123">Bir rota filtre expressroute bağlantı hattı 's Microsoft eşliği ile kullanmak istediğiniz hizmetleri tanımlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="539b6-123">A route filter lets you identify services you want to consume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="539b6-124">Tüm BGP topluluk değerlerini temelde beyaz listesi var.</span><span class="sxs-lookup"><span data-stu-id="539b6-124">It is essentially a white list of all the BGP community values.</span></span> <span data-ttu-id="539b6-125">Bir rota filtre kaynak tanımlanmış ve bir expressroute bağlantı hattı bağlı sonra BGP topluluk değerlerine eşlemek tüm ön eklerin ağınıza bildirilir.</span><span class="sxs-lookup"><span data-stu-id="539b6-125">Once a route filter resource is defined and attached to an ExpressRoute circuit, all prefixes that map to the BGP community values are advertised to your network.</span></span>

<span data-ttu-id="539b6-126">Yol filtreleri bunlardaki Office 365 Hizmetleri ile eklemek için Office 365 hizmetlerini ExpressRoute aracılığıyla kullanma yetkisi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="539b6-126">To be able to attach route filters with Office 365 services on them, you must have authorization to consume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="539b6-127">ExpressRoute aracılığıyla Office 365 hizmetlerini kullanma yetkisi olmayan yol filtreleri ekleme işlemi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="539b6-127">If you are not authorized to consume Office 365 services through ExpressRoute, the operation to attach route filters fails.</span></span> <span data-ttu-id="539b6-128">Yetkilendirme işlemi hakkında daha fazla bilgi için bkz: [Office 365 için Azure ExpressRoute](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="539b6-128">For more information about the authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="539b6-129">Dynamics 365 hizmetlerine bağlantıyı önceki tüm yetkilendirme gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="539b6-129">Connectivity to Dynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="539b6-130">1 Ağustos 2017 önce yapılandırılmış olan ExpressRoute bağlantı hatları, Microsoft eşlemesi yol filtreleri tanımlanmamış olsa bile eşleme, Microsoft tarafından tanıtılan tüm hizmet ön eklerin sahip olur.</span><span class="sxs-lookup"><span data-stu-id="539b6-130">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="539b6-131">Ve 1 Ağustos 2017 sonrasında yapılandırılmış ExpressRoute bağlantı hatları, Microsoft eşlemesi sahip olmaz tüm ön eklerin rota filtre devresine bağlanana kadar tanıtılan.</span><span class="sxs-lookup"><span data-stu-id="539b6-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span>
> 
> 

### <span data-ttu-id="539b6-132"><a name="workflow"></a>İş akışı</span><span class="sxs-lookup"><span data-stu-id="539b6-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="539b6-133">Microsoft eşlemesini üzerinden hizmetlere başarıyla bağlanabilmek için için aşağıdaki yapılandırma adımlarını tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="539b6-133">To be able to successfully connect to services through Microsoft peering, you must complete the following configuration steps:</span></span>

- <span data-ttu-id="539b6-134">Microsoft sağlanan eşlemesini sahip etkin bir expressroute olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="539b6-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="539b6-135">Bu görevleri gerçekleştirmek için aşağıdaki yönergeleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="539b6-135">You can use the following instructions to accomplish these tasks:</span></span>
  - <span data-ttu-id="539b6-136">[Bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-portal-resource-manager.md) ve devam etmeden önce bağlantı sağlayıcınız tarafından etkinleştirilen hattı sahip.</span><span class="sxs-lookup"><span data-stu-id="539b6-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="539b6-137">Expressroute bağlantı hattının sağlanmış ve etkin durumda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="539b6-137">The ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="539b6-138">[Microsoft eşlemesi oluşturmak](expressroute-howto-routing-portal-resource-manager.md) BGP oturumu doğrudan yönetiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="539b6-138">[Create Microsoft peering](expressroute-howto-routing-portal-resource-manager.md) if you manage the BGP session directly.</span></span> <span data-ttu-id="539b6-139">Veya, bağlantı sağlayıcınız hattınız için eşlemesini Microsoft sağlamak.</span><span class="sxs-lookup"><span data-stu-id="539b6-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="539b6-140">Oluşturma ve bir rota filtre yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="539b6-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="539b6-141">Hizmetleri tanımlamak sizinle Microsoft eşliği ile kullanmak için</span><span class="sxs-lookup"><span data-stu-id="539b6-141">Identify the services you with to consume through Microsoft peering</span></span>
    - <span data-ttu-id="539b6-142">BGP topluluk değerlerini servisleri ile ilişkili olan listesini belirlemesini</span><span class="sxs-lookup"><span data-stu-id="539b6-142">Identify the list of BGP community values associated with the services</span></span>
    - <span data-ttu-id="539b6-143">BGP topluluk değerlerini eşleşen Önek listesi izin verecek bir kural oluşturun</span><span class="sxs-lookup"><span data-stu-id="539b6-143">Create a rule to allow the prefix list matching the BGP community values</span></span>

-  <span data-ttu-id="539b6-144">Expressroute bağlantı hattı için rota filtre eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="539b6-144">You must attach the route filter to the ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="539b6-145">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="539b6-145">Before you begin</span></span>

<span data-ttu-id="539b6-146">Yapılandırmaya başlamadan önce aşağıdaki ölçütlere uyan emin olun:</span><span class="sxs-lookup"><span data-stu-id="539b6-146">Before you begin configuration, make sure you meet the following criteria:</span></span>

 - <span data-ttu-id="539b6-147">Gözden geçirme [Önkoşullar](expressroute-prerequisites.md) ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="539b6-147">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="539b6-148">Etkin bir ExpressRoute bağlantı hattınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="539b6-148">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="539b6-149">Devam etmeden önce [ExpressRoute bağlantı hattı oluşturma](expressroute-howto-circuit-portal-resource-manager.md) yönergelerini izleyin ve bağlantı sağlayıcınızın bağlantı hattını etkinleştirmesini isteyin.</span><span class="sxs-lookup"><span data-stu-id="539b6-149">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="539b6-150">Expressroute bağlantı hattının sağlanmış ve etkin durumda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="539b6-150">The ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="539b6-151">Etkin bir Microsoft eşlemesi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="539b6-151">You must have an active Microsoft peering.</span></span> <span data-ttu-id="539b6-152">Bölümündeki yönergeleri izleyin [oluşturma ve eşleme yapılandırmasını değiştirme](expressroute-howto-routing-portal-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="539b6-152">Follow instructions at [Create and modifying peering configuration](expressroute-howto-routing-portal-resource-manager.md)</span></span>


## <span data-ttu-id="539b6-153"><a name="prefixes"></a>1. adım.</span><span class="sxs-lookup"><span data-stu-id="539b6-153"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="539b6-154">Önekleri ve BGP topluluk değerlerini listesini alma</span><span class="sxs-lookup"><span data-stu-id="539b6-154">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="539b6-155">1. BGP topluluk değerlerini listesini al</span><span class="sxs-lookup"><span data-stu-id="539b6-155">1. Get a list of BGP community values</span></span>

<span data-ttu-id="539b6-156">Microsoft eşleme aracılığıyla erişilebilir hizmetleriyle ilişkili BGP topluluk değerlerini sağlanmıştır [ExpressRoute yönlendirme gereksinimleri](expressroute-routing.md) sayfası.</span><span class="sxs-lookup"><span data-stu-id="539b6-156">BGP community values associated with services accessible through Microsoft peering is available in the [ExpressRoute routing requirements](expressroute-routing.md) page.</span></span>

### <a name="2-make-a-list-of-the-values-that-you-want-to-use"></a><span data-ttu-id="539b6-157">2. Kullanmak istediğiniz değerleri listesi olun</span><span class="sxs-lookup"><span data-stu-id="539b6-157">2. Make a list of the values that you want to use</span></span>

<span data-ttu-id="539b6-158">Rota filtrede kullanmak istediğiniz BGP topluluk değerlerini listesini hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="539b6-158">Make a list of BGP community values you want to use in the route filter.</span></span> <span data-ttu-id="539b6-159">Örnek olarak, Dynamics 365 Hizmetleri için BGP topluluk değeri 12076:5040 ' dir.</span><span class="sxs-lookup"><span data-stu-id="539b6-159">As an example, the BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="539b6-160"><a name="filter"></a>2. adım.</span><span class="sxs-lookup"><span data-stu-id="539b6-160"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="539b6-161">Bir rota filtre ve bir filtre kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="539b6-161">Create a route filter and a filter rule</span></span>

<span data-ttu-id="539b6-162">Bir rota filtre yalnızca bir kuralınız olabilir ve kural 'İzin ver' türünde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="539b6-162">A route filter can have only one rule, and the rule must be of type 'Allow'.</span></span> <span data-ttu-id="539b6-163">Bu kural, kendisiyle ilişkilendirilmiş BGP topluluk değerlerini listesini olabilir.</span><span class="sxs-lookup"><span data-stu-id="539b6-163">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="539b6-164">1. Bir rota filtresi oluşturma</span><span class="sxs-lookup"><span data-stu-id="539b6-164">1. Create a route filter</span></span>
<span data-ttu-id="539b6-165">Yeni bir kaynak oluşturma seçeneğini seçerek bir rota filtre oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="539b6-165">You can create a route filter by selecting the option to create a new resource.</span></span> <span data-ttu-id="539b6-166">Tıklatın **yeni** > **ağ** > **RouteFilter**aşağıdaki görüntüde gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="539b6-166">Click **New** > **Networking** > **RouteFilter**, as shown in the following image:</span></span>

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\CreateRouteFilter1.png)

<span data-ttu-id="539b6-168">Bir kaynak grubunda rota filtre yerleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="539b6-168">You must place the route filter in a resource group.</span></span> 

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\CreateRouteFilter.png)

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="539b6-170">2. Bir filtre kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="539b6-170">2. Create a filter rule</span></span>

<span data-ttu-id="539b6-171">Ekleme ve rota filtre Yönet kural sekmesini seçerek kuralları güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="539b6-171">You can add and update rules by selecting the manage rule tab for your route filter.</span></span>

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\ManageRouteFilter.png)


<span data-ttu-id="539b6-173">Açılır listeden bağlanmak ve bittiğinde kuralını kaydetmek istediğiniz hizmetleri seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="539b6-173">You can select the services you want to connect to from the drop down list and save the rule when done.</span></span>

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\AddRouteFilterRule.png)


## <span data-ttu-id="539b6-175"><a name="attach"></a>3. adım.</span><span class="sxs-lookup"><span data-stu-id="539b6-175"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="539b6-176">Bir expressroute bağlantı hattı için rota filtre ekleme</span><span class="sxs-lookup"><span data-stu-id="539b6-176">Attach the route filter to an ExpressRoute circuit</span></span>

<span data-ttu-id="539b6-177">"Hattı Ekle" düğmesini seçerek ve expressroute bağlantı hattı açılır listeden seçerek bağlantı hattı için rota filtresi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="539b6-177">You can attach the route filter to a circuit by selecting the "add Circuit" button and selecting the ExpressRoute circuit from the drop down list.</span></span>

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\AddCktToRouteFilter.png)

## <span data-ttu-id="539b6-179"><a name="getproperties"></a>Bir rota filtre özelliklerini almak için</span><span class="sxs-lookup"><span data-stu-id="539b6-179"><a name="getproperties"></a>To get the properties of a route filter</span></span>

<span data-ttu-id="539b6-180">Portalda kaynak açtığınızda, bir rota filtre özelliklerini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="539b6-180">You can view properties of a route filter when you open the resource in the portal.</span></span>

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\ViewRouteFilter.png)


## <span data-ttu-id="539b6-182"><a name="updateproperties"></a>Bir rota filtre özelliklerini güncelleştirmek için</span><span class="sxs-lookup"><span data-stu-id="539b6-182"><a name="updateproperties"></a>To update the properties of a route filter</span></span>

<span data-ttu-id="539b6-183">BGP topluluk değerlerini "Yönet kuralı" düğmesini seçerek bir devresine bağlı listesini güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="539b6-183">You can update the list of BGP community values attached to a circuit by selecting the "Manage rule" button.</span></span>


![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\ManageRouteFilter.png)

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\AddRouteFilterRule.png) 


## <span data-ttu-id="539b6-186"><a name="detach"></a>Bir expressroute bağlantı hattı rota filtresinden ayırmak için</span><span class="sxs-lookup"><span data-stu-id="539b6-186"><a name="detach"></a>To detach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="539b6-187">Rota filtre hattından ayırmak için bağlantı hattındaki sağ tıklatın ve "ilişkisini üzerinde"'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="539b6-187">To detach a circuit from the route filter, right click on the circuit and click on "disassociate".</span></span>

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\DetachRouteFilter.png) 


## <span data-ttu-id="539b6-189"><a name="delete"></a>Bir rota filtreyi silmek için</span><span class="sxs-lookup"><span data-stu-id="539b6-189"><a name="delete"></a>To delete a route filter</span></span>

<span data-ttu-id="539b6-190">Bir rota filtre Sil düğmesini seçerek silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="539b6-190">You can delete a route filter by selecting the delete button.</span></span> 

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\DeleteRouteFilter.png) 

## <a name="next-steps"></a><span data-ttu-id="539b6-192">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="539b6-192">Next steps</span></span>

<span data-ttu-id="539b6-193">ExpressRoute hakkında daha fazla bilgi için, bkz. [ExpressRoute SSS](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="539b6-193">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>