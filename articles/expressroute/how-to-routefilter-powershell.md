---
title: "Azure ExpressRoute Microsoft eşliği için rota filtrelerini yapılandırın: PowerShell | Microsoft Docs"
description: "Bu makalede, Microsoft PowerShell kullanarak Peering için yol filtrelerini yapılandırmak açıklar"
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
ms.openlocfilehash: de3550c20439fa809869d98b8a57ea3be9c03e7c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="29f46-103">Microsoft eşlemesi için rota filtreleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="29f46-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="29f46-104">Yol filtreleri Microsoft eşleme yoluyla desteklenen hizmetleri kümesini kullanmak için bir yoldur.</span><span class="sxs-lookup"><span data-stu-id="29f46-104">Route filters are a way to consume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="29f46-105">Bu makaledeki adımları yapılandırmak ve ExpressRoute bağlantı hatları için yol filtreleri yönetmenize yardımcı olması.</span><span class="sxs-lookup"><span data-stu-id="29f46-105">The steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="29f46-106">Dynamics 365 Hizmetleri ve Exchange Online, SharePoint Online ve Skype gibi Office 365 Hizmetleri iş için Microsoft eşleme aracılığıyla erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="29f46-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through the Microsoft peering.</span></span> <span data-ttu-id="29f46-107">Microsoft eşlemesi bir expressroute bağlantı hattı yapılandırıldığında, bu hizmetleri ile ilgili tüm ön eklerin oluşturulmuş BGP oturumları bildirilir.</span><span class="sxs-lookup"><span data-stu-id="29f46-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related to these services are advertised through the BGP sessions that are established.</span></span> <span data-ttu-id="29f46-108">BGP topluluk değeri öneki sunulan Hizmeti'ni tanımlamak için her ön eki eklenir.</span><span class="sxs-lookup"><span data-stu-id="29f46-108">A BGP community value is attached to every prefix to identify the service that is offered through the prefix.</span></span> <span data-ttu-id="29f46-109">BGP topluluk değerlerini ve eşlemek için Hizmetler listesi için bkz: [BGP toplulukları](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="29f46-109">For a list of the BGP community values and the services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="29f46-110">Tüm hizmetleri için bağlantı gerektiriyorsa, çok sayıda önekleri BGP bildirilir.</span><span class="sxs-lookup"><span data-stu-id="29f46-110">If you require connectivity to all services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="29f46-111">Bu, ağınızdaki yönlendiricileri tarafından tutulan yol tablolarını boyutunu önemli ölçüde artırır.</span><span class="sxs-lookup"><span data-stu-id="29f46-111">This significantly increases the size of the route tables maintained by routers within your network.</span></span> <span data-ttu-id="29f46-112">Yalnızca bir alt kümesini Microsoft eşliği ile sunulan hizmetlere kullanmayı planlıyorsanız, yol tablolarınız iki yolla boyutunu azaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29f46-112">If you plan to consume only a subset of services offered through Microsoft peering, you can reduce the size of your route tables in two ways.</span></span> <span data-ttu-id="29f46-113">Şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="29f46-113">You can:</span></span>

- <span data-ttu-id="29f46-114">İstenmeyen önekleri BGP toplulukları yol filtreleri uygulayarak filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="29f46-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="29f46-115">Bu standart bir ağ uygulaması ve birçok ağ içinde yaygın olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="29f46-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="29f46-116">Rota filtrelerini tanımlayın ve bunları, expressroute bağlantı hattı uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29f46-116">Define route filters and apply them to your ExpressRoute circuit.</span></span> <span data-ttu-id="29f46-117">Bir rota filtre Microsoft eşliği ile kullanmak için plan Hizmetleri listesini seçmenize izin veren yeni bir kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="29f46-117">A route filter is a new resource that lets you select the list of services you plan to consume through Microsoft peering.</span></span> <span data-ttu-id="29f46-118">ExpressRoute yönlendiriciler yalnızca rota filtrede tanımlanan hizmetlere ait önekleri listesini gönderir.</span><span class="sxs-lookup"><span data-stu-id="29f46-118">ExpressRoute routers only send the list of prefixes that belong to the services identified in the route filter.</span></span>

### <span data-ttu-id="29f46-119"><a name="about"></a>Rota filtreler hakkında</span><span class="sxs-lookup"><span data-stu-id="29f46-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="29f46-120">Microsoft eşlemesi, expressroute bağlantı hattı üzerinde yapılandırıldığında, sınır yönlendiricileri (sizin ya da bağlantı sağlayıcınızın) BGP oturumları çifti Microsoft sınır yönlendiricileri kurun.</span><span class="sxs-lookup"><span data-stu-id="29f46-120">When Microsoft peering is configured on your ExpressRoute circuit, the Microsoft edge routers establish a pair of BGP sessions with the edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="29f46-121">Yol yok, ağınıza bildirilir.</span><span class="sxs-lookup"><span data-stu-id="29f46-121">No routes are advertised to your network.</span></span> <span data-ttu-id="29f46-122">Yol tanıtımlarını ağınıza etkinleştirmek için bir rota filtre ilişkilendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="29f46-122">To enable route advertisements to your network, you must associate a route filter.</span></span>

<span data-ttu-id="29f46-123">Bir rota filtre expressroute bağlantı hattı 's Microsoft eşliği ile kullanmak istediğiniz hizmetleri tanımlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="29f46-123">A route filter lets you identify services you want to consume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="29f46-124">Tüm BGP topluluk değerlerini temelde beyaz listesi var.</span><span class="sxs-lookup"><span data-stu-id="29f46-124">It is essentially a white list of all the BGP community values.</span></span> <span data-ttu-id="29f46-125">Bir rota filtre kaynak tanımlanmış ve bir expressroute bağlantı hattı bağlı sonra BGP topluluk değerlerine eşlemek tüm ön eklerin ağınıza bildirilir.</span><span class="sxs-lookup"><span data-stu-id="29f46-125">Once a route filter resource is defined and attached to an ExpressRoute circuit, all prefixes that map to the BGP community values are advertised to your network.</span></span>

<span data-ttu-id="29f46-126">Yol filtreleri bunlardaki Office 365 Hizmetleri ile eklemek için Office 365 hizmetlerini ExpressRoute aracılığıyla kullanma yetkisi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="29f46-126">To be able to attach route filters with Office 365 services on them, you must have authorization to consume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="29f46-127">ExpressRoute aracılığıyla Office 365 hizmetlerini kullanma yetkisi olmayan yol filtreleri ekleme işlemi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="29f46-127">If you are not authorized to consume Office 365 services through ExpressRoute, the operation to attach route filters fails.</span></span> <span data-ttu-id="29f46-128">Yetkilendirme işlemi hakkında daha fazla bilgi için bkz: [Office 365 için Azure ExpressRoute](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="29f46-128">For more information about the authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="29f46-129">Dynamics 365 hizmetlerine bağlantıyı önceki tüm yetkilendirme gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="29f46-129">Connectivity to Dynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="29f46-130">1 Ağustos 2017 önce yapılandırılmış olan ExpressRoute bağlantı hatları, Microsoft eşlemesi yol filtreleri tanımlanmamış olsa bile eşleme, Microsoft tarafından tanıtılan tüm hizmet ön eklerin sahip olur.</span><span class="sxs-lookup"><span data-stu-id="29f46-130">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="29f46-131">Ve 1 Ağustos 2017 sonrasında yapılandırılmış ExpressRoute bağlantı hatları, Microsoft eşlemesi sahip olmaz tüm ön eklerin rota filtre devresine bağlanana kadar tanıtılan.</span><span class="sxs-lookup"><span data-stu-id="29f46-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span>
> 
> 

### <span data-ttu-id="29f46-132"><a name="workflow"></a>İş akışı</span><span class="sxs-lookup"><span data-stu-id="29f46-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="29f46-133">Microsoft eşlemesini üzerinden hizmetlere başarıyla bağlanabilmek için için aşağıdaki yapılandırma adımlarını tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="29f46-133">To be able to successfully connect to services through Microsoft peering, you must complete the following configuration steps:</span></span>

- <span data-ttu-id="29f46-134">Microsoft sağlanan eşlemesini sahip etkin bir expressroute olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="29f46-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="29f46-135">Bu görevleri gerçekleştirmek için aşağıdaki yönergeleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="29f46-135">You can use the following instructions to accomplish these tasks:</span></span>
  - <span data-ttu-id="29f46-136">[Bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-arm.md) ve devam etmeden önce bağlantı sağlayıcınız tarafından etkinleştirilen hattı sahip.</span><span class="sxs-lookup"><span data-stu-id="29f46-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="29f46-137">Expressroute bağlantı hattının sağlanmış ve etkin durumda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="29f46-137">The ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="29f46-138">[Microsoft eşlemesi oluşturmak](expressroute-circuit-peerings.md) BGP oturumu doğrudan yönetiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="29f46-138">[Create Microsoft peering](expressroute-circuit-peerings.md) if you manage the BGP session directly.</span></span> <span data-ttu-id="29f46-139">Veya, bağlantı sağlayıcınız hattınız için eşlemesini Microsoft sağlamak.</span><span class="sxs-lookup"><span data-stu-id="29f46-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="29f46-140">Oluşturma ve bir rota filtre yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="29f46-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="29f46-141">Hizmetleri tanımlamak sizinle Microsoft eşliği ile kullanmak için</span><span class="sxs-lookup"><span data-stu-id="29f46-141">Identify the services you with to consume through Microsoft peering</span></span>
    - <span data-ttu-id="29f46-142">BGP topluluk değerlerini servisleri ile ilişkili olan listesini belirlemesini</span><span class="sxs-lookup"><span data-stu-id="29f46-142">Identify the list of BGP community values associated with the services</span></span>
    - <span data-ttu-id="29f46-143">BGP topluluk değerlerini eşleşen Önek listesi izin verecek bir kural oluşturun</span><span class="sxs-lookup"><span data-stu-id="29f46-143">Create a rule to allow the prefix list matching the BGP community values</span></span>

-  <span data-ttu-id="29f46-144">Expressroute bağlantı hattı için rota filtre eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="29f46-144">You must attach the route filter to the ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="29f46-145">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="29f46-145">Before you begin</span></span>

<span data-ttu-id="29f46-146">Yapılandırmaya başlamadan önce aşağıdaki ölçütlere uyan emin olun:</span><span class="sxs-lookup"><span data-stu-id="29f46-146">Before you begin configuration, make sure you meet the following criteria:</span></span>

 - <span data-ttu-id="29f46-147">Azure Resource Manager PowerShell cmdlet'lerinin en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="29f46-147">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="29f46-148">Daha fazla bilgi için bkz: [yükleyin ve Azure PowerShelll yapılandırma](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="29f46-148">For more information, see [Install and configure Azure PowerShelll](/powershell/azure/install-azurerm-ps).</span></span>

  > [!NOTE]
  > <span data-ttu-id="29f46-149">PowerShell Galerisi yerine Yükleyicisi'ni kullanarak en son sürümü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="29f46-149">Download the latest version from the PowerShell Gallery, rather than using the Installer.</span></span> <span data-ttu-id="29f46-150">Yükleyici gerekli cmdlet'lerini şu anda desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="29f46-150">The Installer currently does not support the required cmdlets.</span></span>
  > 

 - <span data-ttu-id="29f46-151">Gözden geçirme [Önkoşullar](expressroute-prerequisites.md) ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="29f46-151">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="29f46-152">Etkin bir ExpressRoute bağlantı hattınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="29f46-152">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="29f46-153">Devam etmeden önce [ExpressRoute bağlantı hattı oluşturma](expressroute-howto-circuit-arm.md) yönergelerini izleyin ve bağlantı sağlayıcınızın bağlantı hattını etkinleştirmesini isteyin.</span><span class="sxs-lookup"><span data-stu-id="29f46-153">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="29f46-154">Expressroute bağlantı hattının sağlanmış ve etkin durumda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="29f46-154">The ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="29f46-155">Etkin bir Microsoft eşlemesi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="29f46-155">You must have an active Microsoft peering.</span></span> <span data-ttu-id="29f46-156">Bölümündeki yönergeleri izleyin [oluşturma ve eşleme yapılandırmasını değiştirme](expressroute-circuit-peerings.md)</span><span class="sxs-lookup"><span data-stu-id="29f46-156">Follow instructions at [Create and modifying peering configuration](expressroute-circuit-peerings.md)</span></span>

### <a name="log-in-to-your-azure-account"></a><span data-ttu-id="29f46-157">Azure hesabınızda oturum açın</span><span class="sxs-lookup"><span data-stu-id="29f46-157">Log in to your Azure account</span></span>

<span data-ttu-id="29f46-158">Bu yapılandırmaya başlamadan önce Azure hesabınızda oturum açmalısınız.</span><span class="sxs-lookup"><span data-stu-id="29f46-158">Before beginning this configuration, you must log in to your Azure account.</span></span> <span data-ttu-id="29f46-159">Bu cmdlet, Azure hesabınıza ilişkin oturum açma kimlik bilgilerinizi girmenizi ister.</span><span class="sxs-lookup"><span data-stu-id="29f46-159">The cmdlet prompts you for the login credentials for your Azure account.</span></span> <span data-ttu-id="29f46-160">Oturum açtıktan sonra, Azure PowerShell'de kullanabilmeniz için hesap ayarlarınızı indirir.</span><span class="sxs-lookup"><span data-stu-id="29f46-160">After logging in, it downloads your account settings so they are available to Azure PowerShell.</span></span>

<span data-ttu-id="29f46-161">PowerShell konsolunuzu yükseltilmiş ayrıcalıklarla açın ve hesabınıza bağlanın.</span><span class="sxs-lookup"><span data-stu-id="29f46-161">Open your PowerShell console with elevated privileges, and connect to your account.</span></span> <span data-ttu-id="29f46-162">Bağlanmanıza yardımcı olması için aşağıdaki örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="29f46-162">Use the following example to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="29f46-163">Birden çok Azure aboneliğiniz varsa, hesabın aboneliklerini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="29f46-163">If you have multiple Azure subscriptions, check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="29f46-164">Kullanmak istediğiniz aboneliği belirtin.</span><span class="sxs-lookup"><span data-stu-id="29f46-164">Specify the subscription that you want to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <span data-ttu-id="29f46-165"><a name="prefixes"></a>1. adım.</span><span class="sxs-lookup"><span data-stu-id="29f46-165"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="29f46-166">Önekleri ve BGP topluluk değerlerini listesini alma</span><span class="sxs-lookup"><span data-stu-id="29f46-166">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="29f46-167">1. BGP topluluk değerlerini listesini al</span><span class="sxs-lookup"><span data-stu-id="29f46-167">1. Get a list of BGP community values</span></span>

<span data-ttu-id="29f46-168">Microsoft eşlemesini erişilebilir hizmetleriyle ilişkili BGP topluluk değerlerini listesi ve bunlarla ilişkilendirilmiş önekleri listesini almak için aşağıdaki cmdlet'i kullanın:</span><span class="sxs-lookup"><span data-stu-id="29f46-168">Use the following cmdlet to get the list of BGP community values associated with services accessible through Microsoft peering, and the list of prefixes associated with them:</span></span>

```powershell
Get-AzureRmBgpServiceCommunity
```
### <a name="2-make-a-list-of-the-values-that-you-want-to-use"></a><span data-ttu-id="29f46-169">2. Kullanmak istediğiniz değerleri listesi olun</span><span class="sxs-lookup"><span data-stu-id="29f46-169">2. Make a list of the values that you want to use</span></span>

<span data-ttu-id="29f46-170">Rota filtrede kullanmak istediğiniz BGP topluluk değerlerini listesini hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="29f46-170">Make a list of BGP community values you want to use in the route filter.</span></span> <span data-ttu-id="29f46-171">Örnek olarak, Dynamics 365 Hizmetleri için BGP topluluk değeri 12076:5040 ' dir.</span><span class="sxs-lookup"><span data-stu-id="29f46-171">As an example, the BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="29f46-172"><a name="filter"></a>2. adım.</span><span class="sxs-lookup"><span data-stu-id="29f46-172"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="29f46-173">Bir rota filtre ve bir filtre kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="29f46-173">Create a route filter and a filter rule</span></span>

<span data-ttu-id="29f46-174">Bir rota filtre yalnızca bir kuralınız olabilir ve kural 'İzin ver' türünde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="29f46-174">A route filter can have only one rule, and the rule must be of type 'Allow'.</span></span> <span data-ttu-id="29f46-175">Bu kural, kendisiyle ilişkilendirilmiş BGP topluluk değerlerini listesini olabilir.</span><span class="sxs-lookup"><span data-stu-id="29f46-175">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="29f46-176">1. Bir rota filtresi oluşturma</span><span class="sxs-lookup"><span data-stu-id="29f46-176">1. Create a route filter</span></span>

<span data-ttu-id="29f46-177">İlk olarak, rota filtre oluşturun.</span><span class="sxs-lookup"><span data-stu-id="29f46-177">First, create the route filter.</span></span> <span data-ttu-id="29f46-178">Komut 'New-AzureRmRouteFilter' yalnızca bir rota filtre kaynak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="29f46-178">The command 'New-AzureRmRouteFilter' only creates a route filter resource.</span></span> <span data-ttu-id="29f46-179">Kaynak oluşturduktan sonra ardından bir kural oluşturmak ve rota filtre nesnesine ekleme gerekir.</span><span class="sxs-lookup"><span data-stu-id="29f46-179">After you create the resource, you must then create a rule and attach it to the route filter object.</span></span> <span data-ttu-id="29f46-180">Bir rota filtre kaynak oluşturmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="29f46-180">Run the following command to create a route filter resource:</span></span>

```powershell
New-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup" -Location "West US"
```

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="29f46-181">2. Bir filtre kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="29f46-181">2. Create a filter rule</span></span>

<span data-ttu-id="29f46-182">Örnekte gösterildiği gibi BGP toplulukları bir dizi virgülle ayrılmış bir liste belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29f46-182">You can specify a set of BGP communities as a comma-separated list, as shown in the example.</span></span> <span data-ttu-id="29f46-183">Yeni bir kural oluşturmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="29f46-183">Run the following command to create a new rule:</span></span>
 
```powershell
$rule = New-AzureRmRouteFilterRuleConfig -Name "Allow-EXO-D365" -Access Allow -RouteFilterRuleType Community -CommunityList "12076:5010,12076:5040"
```

### <a name="3-add-the-rule-to-the-route-filter"></a><span data-ttu-id="29f46-184">3. Rota filtre kuralı Ekle</span><span class="sxs-lookup"><span data-stu-id="29f46-184">3. Add the rule to the route filter</span></span>

<span data-ttu-id="29f46-185">Filtre kuralı için rota filtre eklemek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="29f46-185">Run the following command to add the filter rule to the route filter:</span></span>
 
```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.Rules.Add($rule)
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="29f46-186"><a name="attach"></a>3. adım.</span><span class="sxs-lookup"><span data-stu-id="29f46-186"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="29f46-187">Bir expressroute bağlantı hattı için rota filtre ekleme</span><span class="sxs-lookup"><span data-stu-id="29f46-187">Attach the route filter to an ExpressRoute circuit</span></span>

<span data-ttu-id="29f46-188">Yalnızca Microsoft eşlemesi sahip olduğu varsayılarak expressroute bağlantı hattı için rota filtre eklemek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="29f46-188">Run the following command to attach the route filter to the ExpressRoute circuit, assuming you have only Microsoft peering:</span></span>

```powershell
$ckt.Peerings[0].RouteFilter = $routefilter 
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="29f46-189"><a name="getproperties"></a>Bir rota filtre özelliklerini almak için</span><span class="sxs-lookup"><span data-stu-id="29f46-189"><a name="getproperties"></a>To get the properties of a route filter</span></span>

<span data-ttu-id="29f46-190">Bir rota filtre özelliklerini almak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="29f46-190">To get the properties of a route filter, use the following steps:</span></span>

1. <span data-ttu-id="29f46-191">Rota filtre kaynak almak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="29f46-191">Run the following command to get the route filter resource:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  ```
2. <span data-ttu-id="29f46-192">Yol, aşağıdaki komutu çalıştırarak, rota filtre kaynak için filtre kuralları alın:</span><span class="sxs-lookup"><span data-stu-id="29f46-192">Get the route filter rules for the route-filter resource by running the following command:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  $rule = $routefilter.Rules[0]
  ```

## <span data-ttu-id="29f46-193"><a name="updateproperties"></a>Bir rota filtre özelliklerini güncelleştirmek için</span><span class="sxs-lookup"><span data-stu-id="29f46-193"><a name="updateproperties"></a>To update the properties of a route filter</span></span>

<span data-ttu-id="29f46-194">Rota filtre zaten bir hattına bağlıysa, BGP topluluk listesine güncelleştirmeleri otomatik olarak yayar kurulan BGP oturumları aracılığıyla uygun önek tanıtım değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="29f46-194">If the route filter is already attached to a circuit, updates to the BGP community list automatically propagates appropriate prefix advertisement changes through the established BGP sessions.</span></span> <span data-ttu-id="29f46-195">Aşağıdaki komutu kullanarak, rota filtre BGP topluluk listesini güncelleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="29f46-195">You can update the BGP community list of your route filter using the following command:</span></span>

```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.rules[0].Communities = "12076:5030", "12076:5040"
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="29f46-196"><a name="detach"></a>Bir expressroute bağlantı hattı rota filtresinden ayırmak için</span><span class="sxs-lookup"><span data-stu-id="29f46-196"><a name="detach"></a>To detach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="29f46-197">Bir rota filtre expressroute bağlantı hattı ayrılmış sonra hiçbir önekleri BGP oturumu aracılığıyla bildirilir.</span><span class="sxs-lookup"><span data-stu-id="29f46-197">Once a route filter is detached from the ExpressRoute circuit, no prefixes are advertised through the BGP session.</span></span> <span data-ttu-id="29f46-198">Aşağıdaki komutu kullanarak bir expressroute bağlantı hattı rota filtresinden ayırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="29f46-198">You can detach a route filter from an ExpressRoute circuit using the following command:</span></span>
  
```powershell
$ckt.Peerings[0].RouteFilter = $null
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="29f46-199"><a name="delete"></a>Bir rota filtreyi silmek için</span><span class="sxs-lookup"><span data-stu-id="29f46-199"><a name="delete"></a>To delete a route filter</span></span>

<span data-ttu-id="29f46-200">Tüm devresine bağlı olmayan bir rota filtre yalnızca silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29f46-200">You can only delete a route filter if it is not attached to any circuit.</span></span> <span data-ttu-id="29f46-201">Rota filtre herhangi devresine silmeye çalışmadan önce bağlı olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="29f46-201">Ensure that the route filter is not attached to any circuit before attempting to delete it.</span></span> <span data-ttu-id="29f46-202">Aşağıdaki komutu kullanarak bir rota filtre silebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="29f46-202">You can delete a route filter using the following command:</span></span>

```powershell
Remove-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="29f46-203">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="29f46-203">Next steps</span></span>

<span data-ttu-id="29f46-204">ExpressRoute hakkında daha fazla bilgi için, bkz. [ExpressRoute SSS](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="29f46-204">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>