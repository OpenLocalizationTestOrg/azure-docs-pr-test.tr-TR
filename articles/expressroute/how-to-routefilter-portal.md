---
title: "Azure ExpressRoute Microsoft eşliği için rota filtrelerini yapılandırın: portalı | Microsoft Docs"
description: "Bu makalede Microsoft Peering kullanma tooconfigure yol filtreleri Azure portalına nasıl hello açıklanır"
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
ms.openlocfilehash: 2a47d465ec5f175d9510cef94606f70f036f0862
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="914fd-103">Microsoft eşlemesi için rota filtreleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="914fd-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="914fd-104">Yol filtreleri şekilde tooconsume bir alt kümesini Microsoft eşleme yoluyla desteklenen hizmetler şunlardır.</span><span class="sxs-lookup"><span data-stu-id="914fd-104">Route filters are a way tooconsume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="914fd-105">Bu makale Yardım yapılandırmak ve ExpressRoute bağlantı hatları için yol filtreleri yönetmek Hello adımları.</span><span class="sxs-lookup"><span data-stu-id="914fd-105">hello steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="914fd-106">Dynamics 365 Hizmetleri ve işletme için Office 365 Hizmetleri Exchange Online, SharePoint Online ve Skype gibi hello Microsoft eşleme aracılığıyla erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="914fd-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through hello Microsoft peering.</span></span> <span data-ttu-id="914fd-107">Microsoft eşlemesi bir expressroute bağlantı hattı yapılandırıldığında, tüm ön eklerin ilgili toothese Hizmetleri oluşturulmuş hello BGP oturumları bildirilir.</span><span class="sxs-lookup"><span data-stu-id="914fd-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related toothese services are advertised through hello BGP sessions that are established.</span></span> <span data-ttu-id="914fd-108">BGP topluluk değeri hello önek sunulan ekli tooevery önek tooidentify hello hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="914fd-108">A BGP community value is attached tooevery prefix tooidentify hello service that is offered through hello prefix.</span></span> <span data-ttu-id="914fd-109">Merhaba BGP topluluk değerlerini ve eşlemek için hello Hizmetleri listesi için bkz: [BGP toplulukları](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="914fd-109">For a list of hello BGP community values and hello services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="914fd-110">Bağlantı tooall Hizmetleri gerektiriyorsa, çok sayıda önekleri BGP bildirilir.</span><span class="sxs-lookup"><span data-stu-id="914fd-110">If you require connectivity tooall services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="914fd-111">Bu, ağınızdaki yönlendiricileri tarafından tutulan hello yol tablolarını hello boyutunu önemli ölçüde artırır.</span><span class="sxs-lookup"><span data-stu-id="914fd-111">This significantly increases hello size of hello route tables maintained by routers within your network.</span></span> <span data-ttu-id="914fd-112">Yalnızca bir alt kümesini Hizmetleri Microsoft eşliği ile sunulan tooconsume planlıyorsanız, yol tablolarınız iki yolla hello boyutunu azaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="914fd-112">If you plan tooconsume only a subset of services offered through Microsoft peering, you can reduce hello size of your route tables in two ways.</span></span> <span data-ttu-id="914fd-113">Şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="914fd-113">You can:</span></span>

- <span data-ttu-id="914fd-114">İstenmeyen önekleri BGP toplulukları yol filtreleri uygulayarak filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="914fd-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="914fd-115">Bu standart bir ağ uygulaması ve birçok ağ içinde yaygın olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="914fd-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="914fd-116">Rota filtrelerini tanımlayın ve bunları tooyour expressroute bağlantı hattı uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="914fd-116">Define route filters and apply them tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="914fd-117">Bir rota filtre hello listesi sağlar hizmetlerini, yeni bir kaynak Microsoft eşleme yoluyla tooconsume planlamaktır.</span><span class="sxs-lookup"><span data-stu-id="914fd-117">A route filter is a new resource that lets you select hello list of services you plan tooconsume through Microsoft peering.</span></span> <span data-ttu-id="914fd-118">ExpressRoute yönlendiriciler yalnızca hello rota filtrede tanımlanan toohello Hizmetleri ait önekleri hello listesi gönderir.</span><span class="sxs-lookup"><span data-stu-id="914fd-118">ExpressRoute routers only send hello list of prefixes that belong toohello services identified in hello route filter.</span></span>

### <span data-ttu-id="914fd-119"><a name="about"></a>Rota filtreler hakkında</span><span class="sxs-lookup"><span data-stu-id="914fd-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="914fd-120">Microsoft eşlemesi, expressroute bağlantı hattı üzerinde yapılandırıldığında, hello Microsoft sınır yönlendiricileri hello sınır yönlendiricileri (sizin ya da bağlantı sağlayıcınızın) BGP oturumları çifti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="914fd-120">When Microsoft peering is configured on your ExpressRoute circuit, hello Microsoft edge routers establish a pair of BGP sessions with hello edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="914fd-121">Yol yok tanıtılan tooyour ağ tabanlıdır.</span><span class="sxs-lookup"><span data-stu-id="914fd-121">No routes are advertised tooyour network.</span></span> <span data-ttu-id="914fd-122">tooenable yol tanıtımları tooyour ağ, bir rota filtre ilişkilendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="914fd-122">tooenable route advertisements tooyour network, you must associate a route filter.</span></span>

<span data-ttu-id="914fd-123">Bir rota filtre expressroute bağlantı hattı 's Microsoft eşleme yoluyla tooconsume istediğiniz hizmetleri tanımlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="914fd-123">A route filter lets you identify services you want tooconsume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="914fd-124">Tüm hello BGP topluluk değerlerini temelde beyaz listesi var.</span><span class="sxs-lookup"><span data-stu-id="914fd-124">It is essentially a white list of all hello BGP community values.</span></span> <span data-ttu-id="914fd-125">Bir rota filtre kaynağı tanımlandı ve tooan expressroute bağlantı hattı bağlı sonra toohello BGP topluluk değerlerini eşlemek tüm ön eklerin tanıtılan tooyour ağ tabanlıdır.</span><span class="sxs-lookup"><span data-stu-id="914fd-125">Once a route filter resource is defined and attached tooan ExpressRoute circuit, all prefixes that map toohello BGP community values are advertised tooyour network.</span></span>

<span data-ttu-id="914fd-126">Office 365 Hizmetleri bunlardaki ile toobe mümkün tooattach yol filtreleri, yetkilendirme tooconsume Office 365 Hizmetleri ExpressRoute aracılığıyla olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="914fd-126">toobe able tooattach route filters with Office 365 services on them, you must have authorization tooconsume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="914fd-127">ExpressRoute aracılığıyla yetkili tooconsume Office 365 Hizmetleri olmayan hello işlemi tooattach yol filtreleri başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="914fd-127">If you are not authorized tooconsume Office 365 services through ExpressRoute, hello operation tooattach route filters fails.</span></span> <span data-ttu-id="914fd-128">Merhaba Yetkilendirme işlemi hakkında daha fazla bilgi için bkz: [Office 365 için Azure ExpressRoute](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="914fd-128">For more information about hello authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="914fd-129">Bağlantı tooDynamics 365 Hizmetleri, önceki tüm yetkilendirme gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="914fd-129">Connectivity tooDynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="914fd-130">Önceki tooAugust 1 yapılandırılmış olan ExpressRoute bağlantı hatları Microsoft eşliği, yol filtreleri tanımlanmamış olsa bile 2017 Microsoft eşleme aracılığıyla tanıtılan tüm hizmet ön eklerin sahip olur.</span><span class="sxs-lookup"><span data-stu-id="914fd-130">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="914fd-131">Ve 1 Ağustos 2017 sonrasında yapılandırılmış ExpressRoute bağlantı hatları, Microsoft eşlemesi sahip olmaz tüm ön eklerin rota filtre bağlanana kadar tanıtılan toohello hattı.</span><span class="sxs-lookup"><span data-stu-id="914fd-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span>
> 
> 

### <span data-ttu-id="914fd-132"><a name="workflow"></a>İş akışı</span><span class="sxs-lookup"><span data-stu-id="914fd-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="914fd-133">Microsoft eşleme aracılığıyla toobe mümkün toosuccessfully tooservices bağlanma, hello aşağıdaki yapılandırma adımları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="914fd-133">toobe able toosuccessfully connect tooservices through Microsoft peering, you must complete hello following configuration steps:</span></span>

- <span data-ttu-id="914fd-134">Microsoft sağlanan eşlemesini sahip etkin bir expressroute olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="914fd-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="914fd-135">Bu görevleri yönergeleri tooaccomplish aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="914fd-135">You can use hello following instructions tooaccomplish these tasks:</span></span>
  - <span data-ttu-id="914fd-136">[Bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-portal-resource-manager.md) ve devam etmeden önce bağlantı sağlayıcınız tarafından etkinleştirilen hello hattı sahip.</span><span class="sxs-lookup"><span data-stu-id="914fd-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="914fd-137">Hello expressroute bağlantı hattının sağlanmış ve etkin durumda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="914fd-137">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="914fd-138">[Microsoft eşlemesi oluşturmak](expressroute-howto-routing-portal-resource-manager.md) doğrudan hello BGP oturumu yönetiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="914fd-138">[Create Microsoft peering](expressroute-howto-routing-portal-resource-manager.md) if you manage hello BGP session directly.</span></span> <span data-ttu-id="914fd-139">Veya, bağlantı sağlayıcınız hattınız için eşlemesini Microsoft sağlamak.</span><span class="sxs-lookup"><span data-stu-id="914fd-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="914fd-140">Oluşturma ve bir rota filtre yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="914fd-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="914fd-141">Tanımlamak hello Microsoft eşleme yoluyla tooconsume ile Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="914fd-141">Identify hello services you with tooconsume through Microsoft peering</span></span>
    - <span data-ttu-id="914fd-142">Merhaba BGP topluluk değerlerini hello servisleri ile ilişkili olan listesini belirlemesini</span><span class="sxs-lookup"><span data-stu-id="914fd-142">Identify hello list of BGP community values associated with hello services</span></span>
    - <span data-ttu-id="914fd-143">Bir kural tooallow hello önek listesi eşleşen hello BGP topluluk değerlerini oluşturun</span><span class="sxs-lookup"><span data-stu-id="914fd-143">Create a rule tooallow hello prefix list matching hello BGP community values</span></span>

-  <span data-ttu-id="914fd-144">Merhaba rota filtre toohello expressroute bağlantı hattı ilişkilendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="914fd-144">You must attach hello route filter toohello ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="914fd-145">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="914fd-145">Before you begin</span></span>

<span data-ttu-id="914fd-146">Yapılandırmaya başlamadan önce aşağıdaki ölçütleri hello karşıladığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="914fd-146">Before you begin configuration, make sure you meet hello following criteria:</span></span>

 - <span data-ttu-id="914fd-147">Gözden geçirme hello [Önkoşullar](expressroute-prerequisites.md) ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="914fd-147">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="914fd-148">Etkin bir ExpressRoute bağlantı hattınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="914fd-148">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="914fd-149">Çok olarak Hello yönergeleri[bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-portal-resource-manager.md) ve devam etmeden önce bağlantı sağlayıcınız tarafından etkinleştirilen hello hattı sahip.</span><span class="sxs-lookup"><span data-stu-id="914fd-149">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="914fd-150">Hello expressroute bağlantı hattının sağlanmış ve etkin durumda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="914fd-150">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="914fd-151">Etkin bir Microsoft eşlemesi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="914fd-151">You must have an active Microsoft peering.</span></span> <span data-ttu-id="914fd-152">Bölümündeki yönergeleri izleyin [oluşturma ve eşleme yapılandırmasını değiştirme](expressroute-howto-routing-portal-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="914fd-152">Follow instructions at [Create and modifying peering configuration](expressroute-howto-routing-portal-resource-manager.md)</span></span>


## <span data-ttu-id="914fd-153"><a name="prefixes"></a>1. adım.</span><span class="sxs-lookup"><span data-stu-id="914fd-153"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="914fd-154">Önekleri ve BGP topluluk değerlerini listesini alma</span><span class="sxs-lookup"><span data-stu-id="914fd-154">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="914fd-155">1. BGP topluluk değerlerini listesini al</span><span class="sxs-lookup"><span data-stu-id="914fd-155">1. Get a list of BGP community values</span></span>

<span data-ttu-id="914fd-156">Microsoft eşleme aracılığıyla erişilebilir hizmetleriyle ilişkili BGP topluluk değerlerini hello kullanılabilir [ExpressRoute yönlendirme gereksinimleri](expressroute-routing.md) sayfası.</span><span class="sxs-lookup"><span data-stu-id="914fd-156">BGP community values associated with services accessible through Microsoft peering is available in hello [ExpressRoute routing requirements](expressroute-routing.md) page.</span></span>

### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a><span data-ttu-id="914fd-157">2. Merhaba değerler listesini toouse istiyor olun</span><span class="sxs-lookup"><span data-stu-id="914fd-157">2. Make a list of hello values that you want toouse</span></span>

<span data-ttu-id="914fd-158">BGP topluluk değerlerini istediğiniz listesini toouse hello rota filtrede olun.</span><span class="sxs-lookup"><span data-stu-id="914fd-158">Make a list of BGP community values you want toouse in hello route filter.</span></span> <span data-ttu-id="914fd-159">Örnek olarak, hello Dynamics 365 Hizmetleri için BGP topluluk değeri 12076:5040 ' dir.</span><span class="sxs-lookup"><span data-stu-id="914fd-159">As an example, hello BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="914fd-160"><a name="filter"></a>2. adım.</span><span class="sxs-lookup"><span data-stu-id="914fd-160"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="914fd-161">Bir rota filtre ve bir filtre kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="914fd-161">Create a route filter and a filter rule</span></span>

<span data-ttu-id="914fd-162">Bir rota filtre yalnızca bir kuralınız olabilir ve hello kural 'İzin ver' türünde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="914fd-162">A route filter can have only one rule, and hello rule must be of type 'Allow'.</span></span> <span data-ttu-id="914fd-163">Bu kural, kendisiyle ilişkilendirilmiş BGP topluluk değerlerini listesini olabilir.</span><span class="sxs-lookup"><span data-stu-id="914fd-163">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="914fd-164">1. Bir rota filtresi oluşturma</span><span class="sxs-lookup"><span data-stu-id="914fd-164">1. Create a route filter</span></span>
<span data-ttu-id="914fd-165">Yeni bir kaynak hello seçeneği toocreate seçerek bir rota filtre oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="914fd-165">You can create a route filter by selecting hello option toocreate a new resource.</span></span> <span data-ttu-id="914fd-166">Tıklatın **yeni** > **ağ** > **RouteFilter**hello görüntü aşağıdaki gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="914fd-166">Click **New** > **Networking** > **RouteFilter**, as shown in hello following image:</span></span>

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\CreateRouteFilter1.png)

<span data-ttu-id="914fd-168">Bir kaynak grubunda hello rota filtre yerleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="914fd-168">You must place hello route filter in a resource group.</span></span> 

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\CreateRouteFilter.png)

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="914fd-170">2. Bir filtre kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="914fd-170">2. Create a filter rule</span></span>

<span data-ttu-id="914fd-171">Ekleyebilir ve kural sekmesi rota filtreniz için hello seçerek güncelleştirme kurallarını yönetin.</span><span class="sxs-lookup"><span data-stu-id="914fd-171">You can add and update rules by selecting hello manage rule tab for your route filter.</span></span>

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\ManageRouteFilter.png)


<span data-ttu-id="914fd-173">Tooconnect toofrom hello istediğiniz hizmetleri açılan liste ve bittiğinde hello kuralını kaydetmek hello seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="914fd-173">You can select hello services you want tooconnect toofrom hello drop down list and save hello rule when done.</span></span>

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\AddRouteFilterRule.png)


## <span data-ttu-id="914fd-175"><a name="attach"></a>3. adım.</span><span class="sxs-lookup"><span data-stu-id="914fd-175"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="914fd-176">Merhaba rota filtre tooan expressroute bağlantı hattı ekleme</span><span class="sxs-lookup"><span data-stu-id="914fd-176">Attach hello route filter tooan ExpressRoute circuit</span></span>

<span data-ttu-id="914fd-177">Merhaba "Hattı Ekle" düğmesini seçerek ve hello expressroute bağlantı hattı hello açılır listeden seçerek hello rota filtre tooa devresi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="914fd-177">You can attach hello route filter tooa circuit by selecting hello "add Circuit" button and selecting hello ExpressRoute circuit from hello drop down list.</span></span>

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\AddCktToRouteFilter.png)

## <span data-ttu-id="914fd-179"><a name="getproperties"></a>bir rota filtre tooget hello özellikleri</span><span class="sxs-lookup"><span data-stu-id="914fd-179"><a name="getproperties"></a>tooget hello properties of a route filter</span></span>

<span data-ttu-id="914fd-180">Merhaba Portalı'nda hello kaynak açtığınızda, bir rota filtre özelliklerini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="914fd-180">You can view properties of a route filter when you open hello resource in hello portal.</span></span>

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\ViewRouteFilter.png)


## <span data-ttu-id="914fd-182"><a name="updateproperties"></a>bir rota filtre tooupdate hello özellikleri</span><span class="sxs-lookup"><span data-stu-id="914fd-182"><a name="updateproperties"></a>tooupdate hello properties of a route filter</span></span>

<span data-ttu-id="914fd-183">Merhaba "kuralı Yönet" düğmesini seçerek BGP topluluk değerlerini ekli tooa hattı hello listesini güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="914fd-183">You can update hello list of BGP community values attached tooa circuit by selecting hello "Manage rule" button.</span></span>


![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\ManageRouteFilter.png)

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\AddRouteFilterRule.png) 


## <span data-ttu-id="914fd-186"><a name="detach"></a>toodetach bir expressroute bağlantı hattı rota filtresi</span><span class="sxs-lookup"><span data-stu-id="914fd-186"><a name="detach"></a>toodetach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="914fd-187">toodetach hello rota filtre hattından hello hattındaki sağ tıklayın ve "ilişkisini üzerinde"'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="914fd-187">toodetach a circuit from hello route filter, right click on hello circuit and click on "disassociate".</span></span>

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\DetachRouteFilter.png) 


## <span data-ttu-id="914fd-189"><a name="delete"></a>bir rota filtre toodelete</span><span class="sxs-lookup"><span data-stu-id="914fd-189"><a name="delete"></a>toodelete a route filter</span></span>

<span data-ttu-id="914fd-190">Bir rota filtre hello Sil düğmesini seçerek silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="914fd-190">You can delete a route filter by selecting hello delete button.</span></span> 

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\DeleteRouteFilter.png) 

## <a name="next-steps"></a><span data-ttu-id="914fd-192">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="914fd-192">Next steps</span></span>

<span data-ttu-id="914fd-193">ExpressRoute hakkında daha fazla bilgi için bkz: Merhaba [ExpressRoute SSS](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="914fd-193">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
