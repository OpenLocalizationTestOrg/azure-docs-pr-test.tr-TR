---
title: "Azure ExpressRoute Microsoft eşliği için rota filtrelerini yapılandırın: PowerShell | Microsoft Docs"
description: "Bu makalede Microsoft PowerShell kullanarak Peering için nasıl tooconfigure yol filtreleri açıklanır"
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
ms.date: 08/16/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 395bcf7d6ad43c643ff041b154f8e4b797083e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="1d626-103">Microsoft eşlemesi için rota filtreleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1d626-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="1d626-104">Yol filtreleri şekilde tooconsume bir alt kümesini Microsoft eşleme yoluyla desteklenen hizmetler şunlardır.</span><span class="sxs-lookup"><span data-stu-id="1d626-104">Route filters are a way tooconsume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="1d626-105">Bu makale Yardım yapılandırmak ve ExpressRoute bağlantı hatları için yol filtreleri yönetmek Hello adımları.</span><span class="sxs-lookup"><span data-stu-id="1d626-105">hello steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="1d626-106">Dynamics 365 Hizmetleri ve işletme için Office 365 Hizmetleri Exchange Online, SharePoint Online ve Skype gibi hello Microsoft eşleme aracılığıyla erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="1d626-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through hello Microsoft peering.</span></span> <span data-ttu-id="1d626-107">Microsoft eşlemesi bir expressroute bağlantı hattı yapılandırıldığında, tüm ön eklerin ilgili toothese Hizmetleri oluşturulmuş hello BGP oturumları bildirilir.</span><span class="sxs-lookup"><span data-stu-id="1d626-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related toothese services are advertised through hello BGP sessions that are established.</span></span> <span data-ttu-id="1d626-108">BGP topluluk değeri hello önek sunulan ekli tooevery önek tooidentify hello hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="1d626-108">A BGP community value is attached tooevery prefix tooidentify hello service that is offered through hello prefix.</span></span> <span data-ttu-id="1d626-109">Merhaba BGP topluluk değerlerini ve eşlemek için hello Hizmetleri listesi için bkz: [BGP toplulukları](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="1d626-109">For a list of hello BGP community values and hello services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="1d626-110">Bağlantı tooall Hizmetleri gerektiriyorsa, çok sayıda önekleri BGP bildirilir.</span><span class="sxs-lookup"><span data-stu-id="1d626-110">If you require connectivity tooall services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="1d626-111">Bu, ağınızdaki yönlendiricileri tarafından tutulan hello yol tablolarını hello boyutunu önemli ölçüde artırır.</span><span class="sxs-lookup"><span data-stu-id="1d626-111">This significantly increases hello size of hello route tables maintained by routers within your network.</span></span> <span data-ttu-id="1d626-112">Yalnızca bir alt kümesini Hizmetleri Microsoft eşliği ile sunulan tooconsume planlıyorsanız, yol tablolarınız iki yolla hello boyutunu azaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d626-112">If you plan tooconsume only a subset of services offered through Microsoft peering, you can reduce hello size of your route tables in two ways.</span></span> <span data-ttu-id="1d626-113">Şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1d626-113">You can:</span></span>

- <span data-ttu-id="1d626-114">İstenmeyen önekleri BGP toplulukları yol filtreleri uygulayarak filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="1d626-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="1d626-115">Bu standart bir ağ uygulaması ve birçok ağ içinde yaygın olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1d626-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="1d626-116">Rota filtrelerini tanımlayın ve bunları tooyour expressroute bağlantı hattı uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d626-116">Define route filters and apply them tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="1d626-117">Bir rota filtre hello listesi sağlar hizmetlerini, yeni bir kaynak Microsoft eşleme yoluyla tooconsume planlamaktır.</span><span class="sxs-lookup"><span data-stu-id="1d626-117">A route filter is a new resource that lets you select hello list of services you plan tooconsume through Microsoft peering.</span></span> <span data-ttu-id="1d626-118">ExpressRoute yönlendiriciler yalnızca hello rota filtrede tanımlanan toohello Hizmetleri ait önekleri hello listesi gönderir.</span><span class="sxs-lookup"><span data-stu-id="1d626-118">ExpressRoute routers only send hello list of prefixes that belong toohello services identified in hello route filter.</span></span>

### <span data-ttu-id="1d626-119"><a name="about"></a>Rota filtreler hakkında</span><span class="sxs-lookup"><span data-stu-id="1d626-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="1d626-120">Microsoft eşlemesi, expressroute bağlantı hattı üzerinde yapılandırıldığında, hello Microsoft sınır yönlendiricileri hello sınır yönlendiricileri (sizin ya da bağlantı sağlayıcınızın) BGP oturumları çifti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1d626-120">When Microsoft peering is configured on your ExpressRoute circuit, hello Microsoft edge routers establish a pair of BGP sessions with hello edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="1d626-121">Yol yok tanıtılan tooyour ağ tabanlıdır.</span><span class="sxs-lookup"><span data-stu-id="1d626-121">No routes are advertised tooyour network.</span></span> <span data-ttu-id="1d626-122">tooenable yol tanıtımları tooyour ağ, bir rota filtre ilişkilendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d626-122">tooenable route advertisements tooyour network, you must associate a route filter.</span></span>

<span data-ttu-id="1d626-123">Bir rota filtre expressroute bağlantı hattı 's Microsoft eşleme yoluyla tooconsume istediğiniz hizmetleri tanımlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="1d626-123">A route filter lets you identify services you want tooconsume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="1d626-124">Tüm hello BGP topluluk değerlerini temelde beyaz listesi var.</span><span class="sxs-lookup"><span data-stu-id="1d626-124">It is essentially a white list of all hello BGP community values.</span></span> <span data-ttu-id="1d626-125">Bir rota filtre kaynağı tanımlandı ve tooan expressroute bağlantı hattı bağlı sonra toohello BGP topluluk değerlerini eşlemek tüm ön eklerin tanıtılan tooyour ağ tabanlıdır.</span><span class="sxs-lookup"><span data-stu-id="1d626-125">Once a route filter resource is defined and attached tooan ExpressRoute circuit, all prefixes that map toohello BGP community values are advertised tooyour network.</span></span>

<span data-ttu-id="1d626-126">Office 365 Hizmetleri bunlardaki ile toobe mümkün tooattach yol filtreleri, yetkilendirme tooconsume Office 365 Hizmetleri ExpressRoute aracılığıyla olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d626-126">toobe able tooattach route filters with Office 365 services on them, you must have authorization tooconsume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="1d626-127">ExpressRoute aracılığıyla yetkili tooconsume Office 365 Hizmetleri olmayan hello işlemi tooattach yol filtreleri başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="1d626-127">If you are not authorized tooconsume Office 365 services through ExpressRoute, hello operation tooattach route filters fails.</span></span> <span data-ttu-id="1d626-128">Merhaba Yetkilendirme işlemi hakkında daha fazla bilgi için bkz: [Office 365 için Azure ExpressRoute](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="1d626-128">For more information about hello authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="1d626-129">Bağlantı tooDynamics 365 Hizmetleri, önceki tüm yetkilendirme gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="1d626-129">Connectivity tooDynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1d626-130">Önceki tooAugust 1 yapılandırılmış olan ExpressRoute bağlantı hatları Microsoft eşliği, yol filtreleri tanımlanmamış olsa bile 2017 Microsoft eşleme aracılığıyla tanıtılan tüm hizmet ön eklerin sahip olur.</span><span class="sxs-lookup"><span data-stu-id="1d626-130">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="1d626-131">Ve 1 Ağustos 2017 sonrasında yapılandırılmış ExpressRoute bağlantı hatları, Microsoft eşlemesi sahip olmaz tüm ön eklerin rota filtre bağlanana kadar tanıtılan toohello hattı.</span><span class="sxs-lookup"><span data-stu-id="1d626-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span>
> 
> 

### <span data-ttu-id="1d626-132"><a name="workflow"></a>İş akışı</span><span class="sxs-lookup"><span data-stu-id="1d626-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="1d626-133">Microsoft eşleme aracılığıyla toobe mümkün toosuccessfully tooservices bağlanma, hello aşağıdaki yapılandırma adımları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="1d626-133">toobe able toosuccessfully connect tooservices through Microsoft peering, you must complete hello following configuration steps:</span></span>

- <span data-ttu-id="1d626-134">Microsoft sağlanan eşlemesini sahip etkin bir expressroute olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d626-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="1d626-135">Bu görevleri yönergeleri tooaccomplish aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1d626-135">You can use hello following instructions tooaccomplish these tasks:</span></span>
  - <span data-ttu-id="1d626-136">[Bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-arm.md) ve devam etmeden önce bağlantı sağlayıcınız tarafından etkinleştirilen hello hattı sahip.</span><span class="sxs-lookup"><span data-stu-id="1d626-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="1d626-137">Hello expressroute bağlantı hattının sağlanmış ve etkin durumda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d626-137">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="1d626-138">[Microsoft eşlemesi oluşturmak](expressroute-circuit-peerings.md) doğrudan hello BGP oturumu yönetiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="1d626-138">[Create Microsoft peering](expressroute-circuit-peerings.md) if you manage hello BGP session directly.</span></span> <span data-ttu-id="1d626-139">Veya, bağlantı sağlayıcınız hattınız için eşlemesini Microsoft sağlamak.</span><span class="sxs-lookup"><span data-stu-id="1d626-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="1d626-140">Oluşturma ve bir rota filtre yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d626-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="1d626-141">Tanımlamak hello Microsoft eşleme yoluyla tooconsume ile Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="1d626-141">Identify hello services you with tooconsume through Microsoft peering</span></span>
    - <span data-ttu-id="1d626-142">Merhaba BGP topluluk değerlerini hello servisleri ile ilişkili olan listesini belirlemesini</span><span class="sxs-lookup"><span data-stu-id="1d626-142">Identify hello list of BGP community values associated with hello services</span></span>
    - <span data-ttu-id="1d626-143">Bir kural tooallow hello önek listesi eşleşen hello BGP topluluk değerlerini oluşturun</span><span class="sxs-lookup"><span data-stu-id="1d626-143">Create a rule tooallow hello prefix list matching hello BGP community values</span></span>

-  <span data-ttu-id="1d626-144">Merhaba rota filtre toohello expressroute bağlantı hattı ilişkilendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d626-144">You must attach hello route filter toohello ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1d626-145">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="1d626-145">Before you begin</span></span>

<span data-ttu-id="1d626-146">Yapılandırmaya başlamadan önce aşağıdaki ölçütleri hello karşıladığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="1d626-146">Before you begin configuration, make sure you meet hello following criteria:</span></span>

 - <span data-ttu-id="1d626-147">Merhaba hello Azure Resource Manager PowerShell cmdlet'lerinin en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1d626-147">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="1d626-148">Daha fazla bilgi için bkz: [yükleyin ve Azure PowerShelll yapılandırma](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="1d626-148">For more information, see [Install and configure Azure PowerShelll](/powershell/azure/install-azurerm-ps).</span></span>

  > [!NOTE]
  > <span data-ttu-id="1d626-149">Merhaba PowerShell Galerisi yerine hello yükleyici kullanarak Hello en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1d626-149">Download hello latest version from hello PowerShell Gallery, rather than using hello Installer.</span></span> <span data-ttu-id="1d626-150">Merhaba, yükleyici şu anda gerekli hello cmdlet'leri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="1d626-150">hello Installer currently does not support hello required cmdlets.</span></span>
  > 

 - <span data-ttu-id="1d626-151">Gözden geçirme hello [Önkoşullar](expressroute-prerequisites.md) ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="1d626-151">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="1d626-152">Etkin bir ExpressRoute bağlantı hattınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d626-152">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="1d626-153">Çok olarak Hello yönergeleri[bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-arm.md) ve devam etmeden önce bağlantı sağlayıcınız tarafından etkinleştirilen hello hattı sahip.</span><span class="sxs-lookup"><span data-stu-id="1d626-153">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="1d626-154">Hello expressroute bağlantı hattının sağlanmış ve etkin durumda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d626-154">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="1d626-155">Etkin bir Microsoft eşlemesi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d626-155">You must have an active Microsoft peering.</span></span> <span data-ttu-id="1d626-156">Bölümündeki yönergeleri izleyin [oluşturma ve eşleme yapılandırmasını değiştirme](expressroute-circuit-peerings.md)</span><span class="sxs-lookup"><span data-stu-id="1d626-156">Follow instructions at [Create and modifying peering configuration](expressroute-circuit-peerings.md)</span></span>

### <a name="log-in-tooyour-azure-account"></a><span data-ttu-id="1d626-157">Azure hesabı tooyour içinde oturum</span><span class="sxs-lookup"><span data-stu-id="1d626-157">Log in tooyour Azure account</span></span>

<span data-ttu-id="1d626-158">Bu yapılandırmaya başlamadan önce tooyour Azure hesabı oturum açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d626-158">Before beginning this configuration, you must log in tooyour Azure account.</span></span> <span data-ttu-id="1d626-159">Merhaba cmdlet hello Azure hesabınızda oturum açma kimlik bilgilerini ister.</span><span class="sxs-lookup"><span data-stu-id="1d626-159">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="1d626-160">Kullanılabilir tooAzure PowerShell şekilde oturum açtıktan sonra hesap ayarlarınızı indirir.</span><span class="sxs-lookup"><span data-stu-id="1d626-160">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span>

<span data-ttu-id="1d626-161">PowerShell Konsolunuzu yükseltilmiş ayrıcalıklarla açın ve tooyour hesap bağlanın.</span><span class="sxs-lookup"><span data-stu-id="1d626-161">Open your PowerShell console with elevated privileges, and connect tooyour account.</span></span> <span data-ttu-id="1d626-162">Bağlandığınız örnek toohelp aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="1d626-162">Use hello following example toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="1d626-163">Birden çok Azure aboneliğiniz varsa, hello hesabının hello abonelikleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="1d626-163">If you have multiple Azure subscriptions, check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="1d626-164">Merhaba abonelik toouse istediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="1d626-164">Specify hello subscription that you want toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <span data-ttu-id="1d626-165"><a name="prefixes"></a>1. adım.</span><span class="sxs-lookup"><span data-stu-id="1d626-165"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="1d626-166">Önekleri ve BGP topluluk değerlerini listesini alma</span><span class="sxs-lookup"><span data-stu-id="1d626-166">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="1d626-167">1. BGP topluluk değerlerini listesini al</span><span class="sxs-lookup"><span data-stu-id="1d626-167">1. Get a list of BGP community values</span></span>

<span data-ttu-id="1d626-168">Cmdlet tooget hello Microsoft eşleme aracılığıyla erişilebilir hizmetleriyle ilişkili BGP topluluk değerlerini listesi aşağıdaki hello kullanın ve bunlarla ilişkilendirilmiş önekleri listesini hello:</span><span class="sxs-lookup"><span data-stu-id="1d626-168">Use hello following cmdlet tooget hello list of BGP community values associated with services accessible through Microsoft peering, and hello list of prefixes associated with them:</span></span>

```powershell
Get-AzureRmBgpServiceCommunity
```
### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a><span data-ttu-id="1d626-169">2. Merhaba değerler listesini toouse istiyor olun</span><span class="sxs-lookup"><span data-stu-id="1d626-169">2. Make a list of hello values that you want toouse</span></span>

<span data-ttu-id="1d626-170">BGP topluluk değerlerini istediğiniz listesini toouse hello rota filtrede olun.</span><span class="sxs-lookup"><span data-stu-id="1d626-170">Make a list of BGP community values you want toouse in hello route filter.</span></span> <span data-ttu-id="1d626-171">Örnek olarak, hello Dynamics 365 Hizmetleri için BGP topluluk değeri 12076:5040 ' dir.</span><span class="sxs-lookup"><span data-stu-id="1d626-171">As an example, hello BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="1d626-172"><a name="filter"></a>2. adım.</span><span class="sxs-lookup"><span data-stu-id="1d626-172"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="1d626-173">Bir rota filtre ve bir filtre kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1d626-173">Create a route filter and a filter rule</span></span>

<span data-ttu-id="1d626-174">Bir rota filtre yalnızca bir kuralınız olabilir ve hello kural 'İzin ver' türünde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1d626-174">A route filter can have only one rule, and hello rule must be of type 'Allow'.</span></span> <span data-ttu-id="1d626-175">Bu kural, kendisiyle ilişkilendirilmiş BGP topluluk değerlerini listesini olabilir.</span><span class="sxs-lookup"><span data-stu-id="1d626-175">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="1d626-176">1. Bir rota filtresi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1d626-176">1. Create a route filter</span></span>

<span data-ttu-id="1d626-177">İlk olarak, hello rota filtre oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1d626-177">First, create hello route filter.</span></span> <span data-ttu-id="1d626-178">'Yeni-AzureRmRouteFilter' Hello komutu yalnızca bir rota filtre kaynağı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1d626-178">hello command 'New-AzureRmRouteFilter' only creates a route filter resource.</span></span> <span data-ttu-id="1d626-179">Hello kaynak oluşturduktan sonra ardından bir kural oluşturmak ve toohello rota filtre nesnesi ekleme gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d626-179">After you create hello resource, you must then create a rule and attach it toohello route filter object.</span></span> <span data-ttu-id="1d626-180">Komut toocreate aşağıdaki hello rota filtre kaynak çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="1d626-180">Run hello following command toocreate a route filter resource:</span></span>

```powershell
New-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup" -Location "West US"
```

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="1d626-181">2. Bir filtre kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1d626-181">2. Create a filter rule</span></span>

<span data-ttu-id="1d626-182">Merhaba örnekte gösterildiği gibi BGP toplulukları bir dizi virgülle ayrılmış bir liste belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d626-182">You can specify a set of BGP communities as a comma-separated list, as shown in hello example.</span></span> <span data-ttu-id="1d626-183">Komut toocreate aşağıdaki hello yeni bir kural çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="1d626-183">Run hello following command toocreate a new rule:</span></span>
 
```powershell
$rule = New-AzureRmRouteFilterRuleConfig -Name "Allow-EXO-D365" -Access Allow -RouteFilterRuleType Community -CommunityList "12076:5010,12076:5040"
```

### <a name="3-add-hello-rule-toohello-route-filter"></a><span data-ttu-id="1d626-184">3. Merhaba kural toohello rota Filtresi Ekle</span><span class="sxs-lookup"><span data-stu-id="1d626-184">3. Add hello rule toohello route filter</span></span>

<span data-ttu-id="1d626-185">Komut tooadd hello filtre kuralı toohello rota filtresi aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="1d626-185">Run hello following command tooadd hello filter rule toohello route filter:</span></span>
 
```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.Rules.Add($rule)
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="1d626-186"><a name="attach"></a>3. adım.</span><span class="sxs-lookup"><span data-stu-id="1d626-186"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="1d626-187">Merhaba rota filtre tooan expressroute bağlantı hattı ekleme</span><span class="sxs-lookup"><span data-stu-id="1d626-187">Attach hello route filter tooan ExpressRoute circuit</span></span>

<span data-ttu-id="1d626-188">Komut tooattach hello rota filtre toohello expressroute bağlantı hattı, yalnızca Microsoft eşlemesi sahip olduğu varsayılarak aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="1d626-188">Run hello following command tooattach hello route filter toohello ExpressRoute circuit, assuming you have only Microsoft peering:</span></span>

```powershell
$ckt.Peerings[0].RouteFilter = $routefilter 
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="1d626-189"><a name="getproperties"></a>bir rota filtre tooget hello özellikleri</span><span class="sxs-lookup"><span data-stu-id="1d626-189"><a name="getproperties"></a>tooget hello properties of a route filter</span></span>

<span data-ttu-id="1d626-190">bir rota filtre tooget hello özellikleri hello aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="1d626-190">tooget hello properties of a route filter, use hello following steps:</span></span>

1. <span data-ttu-id="1d626-191">Komut tooget hello rota filtre kaynak aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="1d626-191">Run hello following command tooget hello route filter resource:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  ```
2. <span data-ttu-id="1d626-192">Merhaba rota filtre kuralları hello aşağıdaki komutu çalıştırarak hello rota filtre kaynak için alın:</span><span class="sxs-lookup"><span data-stu-id="1d626-192">Get hello route filter rules for hello route-filter resource by running hello following command:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  $rule = $routefilter.Rules[0]
  ```

## <span data-ttu-id="1d626-193"><a name="updateproperties"></a>bir rota filtre tooupdate hello özellikleri</span><span class="sxs-lookup"><span data-stu-id="1d626-193"><a name="updateproperties"></a>tooupdate hello properties of a route filter</span></span>

<span data-ttu-id="1d626-194">Merhaba rota filtre zaten bağlıysa, tooa hattı, güncelleştirmeleri toohello BGP topluluk listesinin otomatik olarak oluşturulan hello BGP oturumları aracılığıyla uygun önek tanıtım değişiklikleri yayar.</span><span class="sxs-lookup"><span data-stu-id="1d626-194">If hello route filter is already attached tooa circuit, updates toohello BGP community list automatically propagates appropriate prefix advertisement changes through hello established BGP sessions.</span></span> <span data-ttu-id="1d626-195">Merhaba BGP topluluk hello aşağıdaki komutu kullanarak, rota filtre listesini güncelleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1d626-195">You can update hello BGP community list of your route filter using hello following command:</span></span>

```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.rules[0].Communities = "12076:5030", "12076:5040"
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="1d626-196"><a name="detach"></a>toodetach bir expressroute bağlantı hattı rota filtresi</span><span class="sxs-lookup"><span data-stu-id="1d626-196"><a name="detach"></a>toodetach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="1d626-197">Bir rota filtre expressroute bağlantı hattı hello ayrılmış sonra hiçbir önekleri hello BGP oturumu aracılığıyla bildirilir.</span><span class="sxs-lookup"><span data-stu-id="1d626-197">Once a route filter is detached from hello ExpressRoute circuit, no prefixes are advertised through hello BGP session.</span></span> <span data-ttu-id="1d626-198">Komutu aşağıdaki hello kullanarak ExpressRoute devresi rota filtresinden ayırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1d626-198">You can detach a route filter from an ExpressRoute circuit using hello following command:</span></span>
  
```powershell
$ckt.Peerings[0].RouteFilter = $null
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="1d626-199"><a name="delete"></a>bir rota filtre toodelete</span><span class="sxs-lookup"><span data-stu-id="1d626-199"><a name="delete"></a>toodelete a route filter</span></span>

<span data-ttu-id="1d626-200">Delete değilse bir rota filtre tooany hattı bağlı yalnızca kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d626-200">You can only delete a route filter if it is not attached tooany circuit.</span></span> <span data-ttu-id="1d626-201">Bu hello rota filtre olmadığından emin olun toodelete denemeden önce tooany hattı bağlı onu.</span><span class="sxs-lookup"><span data-stu-id="1d626-201">Ensure that hello route filter is not attached tooany circuit before attempting toodelete it.</span></span> <span data-ttu-id="1d626-202">Komutu aşağıdaki hello kullanarak bir rota filtre silebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1d626-202">You can delete a route filter using hello following command:</span></span>

```powershell
Remove-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="1d626-203">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1d626-203">Next steps</span></span>

<span data-ttu-id="1d626-204">ExpressRoute hakkında daha fazla bilgi için bkz: Merhaba [ExpressRoute SSS](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="1d626-204">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
