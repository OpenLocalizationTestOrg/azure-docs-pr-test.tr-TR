---
title: "Oluşturma ve bir expressroute bağlantı hattı değiştirme: PowerShell: Azure Resource Manager | Microsoft Docs"
description: "Bu makalede nasıl toocreate, sağlama, doğrulayın, güncelleştirme, silme ve bir expressroute bağlantı hattı yetkisini kaldırma açıklanmaktadır."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f997182e-9b25-4a7a-b079-b004221dadcc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8d76c577a9cffdd393abac1b76cccc27d92e9e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="6dbf5-103">Oluşturma ve PowerShell kullanarak bir expressroute bağlantı hattı değiştirme</span><span class="sxs-lookup"><span data-stu-id="6dbf5-103">Create and modify an ExpressRoute circuit using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6dbf5-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="6dbf5-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="6dbf5-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6dbf5-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="6dbf5-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6dbf5-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="6dbf5-107">Video - Azure portalı</span><span class="sxs-lookup"><span data-stu-id="6dbf5-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="6dbf5-108">PowerShell (klasik)</span><span class="sxs-lookup"><span data-stu-id="6dbf5-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="6dbf5-109">Bu makalede nasıl toocreate bir Azure expressroute bağlantı hattı PowerShell cmdlet'leri ve hello Azure Resource Manager dağıtım modelini kullanarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-109">This article describes how toocreate an Azure ExpressRoute circuit by using PowerShell cmdlets and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="6dbf5-110">Bu makalede ayrıca, nasıl toocheck hello hello devrenin durumunu, güncelleştirme veya silme ve onu yetkisini kaldırma gösterir.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-110">This article also shows you how toocheck hello status of hello circuit, update it, or delete and deprovision it.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6dbf5-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="6dbf5-111">Before you begin</span></span>
* <span data-ttu-id="6dbf5-112">Merhaba hello Azure Resource Manager PowerShell cmdlet'lerinin en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-112">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="6dbf5-113">Daha fazla bilgi için bkz: [Azure PowerShell genel bakış](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6dbf5-113">For more information, see [Overview of Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="6dbf5-114">Gözden geçirme hello [Önkoşullar](expressroute-prerequisites.md) ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-114">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>


## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="6dbf5-115">Oluşturma ve bir expressroute bağlantı hattı sağlama</span><span class="sxs-lookup"><span data-stu-id="6dbf5-115">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a><span data-ttu-id="6dbf5-116">1. Tooyour Azure hesabı oturum ve aboneliğinizi seçin</span><span class="sxs-lookup"><span data-stu-id="6dbf5-116">1. Sign in tooyour Azure account and select your subscription</span></span>
<span data-ttu-id="6dbf5-117">toobegin yapılandırmanıza, oturum açma tooyour Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-117">toobegin your configuration, sign in tooyour Azure account.</span></span> <span data-ttu-id="6dbf5-118">Bağlandığınız örnekler toohelp aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-118">Use hello following examples toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="6dbf5-119">Merhaba hesabının Hello abonelikleri kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-119">Check hello subscriptions for hello account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="6dbf5-120">Bir expressroute bağlantı hattı için toocreate istediğiniz hello aboneliği seçin:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-120">Select hello subscription that you want toocreate an ExpressRoute circuit for:</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="6dbf5-121">2. Desteklenen sağlayıcılar, konumları ve bant genişlikleri Hello listesini alma</span><span class="sxs-lookup"><span data-stu-id="6dbf5-121">2. Get hello list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="6dbf5-122">Bir expressroute bağlantı hattı oluşturmadan önce desteklenen bağlantı sağlayıcıları, konumları ve bant genişliği seçenekleri hello listesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-122">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="6dbf5-123">PowerShell cmdlet hello **Get-AzureRmExpressRouteServiceProvider** , sonraki adımlarda kullanacağınız bu bilgiler verir:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-123">hello PowerShell cmdlet **Get-AzureRmExpressRouteServiceProvider** returns this information, which you’ll use in later steps:</span></span>

```powershell
Get-AzureRmExpressRouteServiceProvider
```

<span data-ttu-id="6dbf5-124">Bağlantı sağlayıcınız listelenip toosee kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-124">Check toosee if your connectivity provider is listed there.</span></span> <span data-ttu-id="6dbf5-125">Aşağıdaki bilgilerle hello not edin.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-125">Make a note of hello following information.</span></span> <span data-ttu-id="6dbf5-126">Bir bağlantı hattı oluşturduğunuzda, daha sonra gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-126">You'll need it later when you create a circuit.</span></span>

* <span data-ttu-id="6dbf5-127">Ad</span><span class="sxs-lookup"><span data-stu-id="6dbf5-127">Name</span></span>
* <span data-ttu-id="6dbf5-128">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="6dbf5-128">PeeringLocations</span></span>
* <span data-ttu-id="6dbf5-129">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="6dbf5-129">BandwidthsOffered</span></span>

<span data-ttu-id="6dbf5-130">Şimdi hazır toocreate bir expressroute bağlantı hattı olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-130">You're now ready toocreate an ExpressRoute circuit.</span></span>   

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="6dbf5-131">3. ExpressRoute bağlantı hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6dbf5-131">3. Create an ExpressRoute circuit</span></span>
<span data-ttu-id="6dbf5-132">Bir kaynak grubu zaten yoksa, expressroute bağlantı hattı oluşturmadan önce bir oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-132">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="6dbf5-133">Merhaba aşağıdaki komutu çalıştırarak bunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-133">You can do so by running hello following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


<span data-ttu-id="6dbf5-134">Aşağıdaki örnek hello nasıl toocreate 200 MB/sn expressroute bağlantı hattı Silikon vadisi Equinix aracılığıyla gösterir.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-134">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="6dbf5-135">Farklı bir sağlayıcı ve farklı ayarlar kullanıyorsanız, bu bilgileri isteğiniz yaptığınızda değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-135">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> <span data-ttu-id="6dbf5-136">Merhaba, yeni bir hizmet anahtarı için bir örnek isteği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-136">hello following is an example request for a new service key:</span></span>

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

<span data-ttu-id="6dbf5-137">Merhaba doğru SKU katmanı ve SKU ailesi belirttiğinizden emin olun:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-137">Make sure that you specify hello correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="6dbf5-138">SKU katmanı, bir ExpressRoute standart ya da bir ExpressRoute premium Eklentisi etkin olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-138">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="6dbf5-139">Belirleyebileceğiniz *standart* tooget hello standart SKU veya *Premium* hello premium eklenti için.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-139">You can specify *Standard* tooget hello standard SKU or *Premium* for hello premium add-on.</span></span>
* <span data-ttu-id="6dbf5-140">SKU ailesi hello faturalama türü belirler.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-140">SKU family determines hello billing type.</span></span> <span data-ttu-id="6dbf5-141">Belirleyebileceğiniz *Metereddata* ölçülen veri planı için ve *Unlimiteddata* sınırsız veri planı için.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-141">You can specify *Metereddata* for a metered data plan and *Unlimiteddata* for an unlimited data plan.</span></span> <span data-ttu-id="6dbf5-142">Merhaba fatura türünden değiştirebileceğiniz *Metereddata* çok*Unlimiteddata*, ancak hello türünden değiştiremezsiniz *Unlimiteddata* çok*Metereddata* .</span><span class="sxs-lookup"><span data-stu-id="6dbf5-142">You can change hello billing type from *Metereddata* too*Unlimiteddata*, but you can't change hello type from *Unlimiteddata* too*Metereddata*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6dbf5-143">ExpressRoute bağlantı hattınız bir hizmet anahtarı verilen hello andan itibaren Fatura edilecek.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-143">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="6dbf5-144">Merhaba bağlantı sağlayıcı hazır tooprovision hello hattı olduğunda bu işlemi gerçekleştirmek emin olun.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-144">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="6dbf5-145">Merhaba yanıt hello hizmet anahtarı içerir.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-145">hello response contains hello service key.</span></span> <span data-ttu-id="6dbf5-146">Merhaba aşağıdaki komutu çalıştırarak tüm hello parametrelerin ayrıntılı açıklamaları alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-146">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="6dbf5-147">4. Tüm ExpressRoute bağlantı hatları listesi</span><span class="sxs-lookup"><span data-stu-id="6dbf5-147">4. List all ExpressRoute circuits</span></span>
<span data-ttu-id="6dbf5-148">Tüm listesini Merhaba, oluşturduğunuz ExpressRoute bağlantı hatları tooget çalıştırmak hello **Get-AzureRmExpressRouteCircuit** komutu:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-148">tooget a list of all hello ExpressRoute circuits that you created, run hello **Get-AzureRmExpressRouteCircuit** command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

<span data-ttu-id="6dbf5-149">Merhaba yanıt aşağıdaki örneğine benzer toohello görünür:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-149">hello response will look similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                          }
    CircuitProvisioningState          : Enabled
    ServiceProviderProvisioningState  : NotProvisioned
    ServiceProviderNotes              :
    ServiceProviderProperties         : {
                                          "ServiceProviderName": "Equinix",
                                          "PeeringLocation": "Silicon Valley",
                                          "BandwidthInMbps": 200
                                        }
    ServiceKey                        : **************************************
    Peerings                          : []

<span data-ttu-id="6dbf5-150">Hello kullanarak herhangi bir zamanda bu bilgiler alabilirsiniz `Get-AzureRmExpressRouteCircuit` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-150">You can retrieve this information at any time by using hello `Get-AzureRmExpressRouteCircuit` cmdlet.</span></span> <span data-ttu-id="6dbf5-151">Merhaba parametresiz çağrısı yaparak tüm hello devreleri listeler.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-151">Making hello call with no parameters lists all hello circuits.</span></span> <span data-ttu-id="6dbf5-152">Hizmet anahtarınız hello listelenmez *ServiceKey* alan:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-152">Your service key will be listed in hello *ServiceKey* field:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="6dbf5-153">Merhaba yanıt aşağıdaki örneğine benzer toohello görünür:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-153">hello response will look similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                          }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : NotProvisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


<span data-ttu-id="6dbf5-154">Merhaba aşağıdaki komutu çalıştırarak tüm hello parametrelerin ayrıntılı açıklamaları alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-154">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="6dbf5-155">5. Merhaba hizmet anahtar tooyour bağlantı sağlayıcı sağlamak için Gönder</span><span class="sxs-lookup"><span data-stu-id="6dbf5-155">5. Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="6dbf5-156">*ServiceProviderProvisioningState* hello hizmet sağlayıcı tarafında sağlama hello geçerli durumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-156">*ServiceProviderProvisioningState* provides information about hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="6dbf5-157">Durum Microsoft yan hello üzerinde hello durumunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-157">Status provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="6dbf5-158">Merhaba hattı durumları sağlama hakkında daha fazla bilgi için bkz: [iş akışları](expressroute-workflows.md#expressroute-circuit-provisioning-states) makalesi.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-158">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="6dbf5-159">Yeni bir expressroute bağlantı hattı oluşturduğunuzda, hello hattı durumu aşağıdaki hello olacaktır:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-159">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



<span data-ttu-id="6dbf5-160">Merhaba hattı hello bağlantı sağlayıcı için etkinleştirme işleminin hello olduğunda durumu aşağıdaki toohello değişir:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-160">hello circuit will change toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="6dbf5-161">Toobe mümkün toouse için bir expressroute bağlantı hattı, durumu aşağıdaki hello olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-161">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="6dbf5-162">6. Merhaba durumunu ve hello hattı anahtar hello durumunu düzenli aralıklarla denetleyin</span><span class="sxs-lookup"><span data-stu-id="6dbf5-162">6. Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="6dbf5-163">Merhaba durumu ve hello hattı anahtar hello durumunu denetleme, sağlayıcınız hattınız etkinleştirildiğinde bilmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-163">Checking hello status and hello state of hello circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="6dbf5-164">Merhaba hattı yapılandırıldıktan sonra *ServiceProviderProvisioningState* olarak görünür *hazırlandı*hello aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-164">After hello circuit has been configured, *ServiceProviderProvisioningState* appears as *Provisioned*, as shown in hello following example:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="6dbf5-165">Merhaba yanıt aşağıdaki örneğine benzer toohello görünür:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-165">hello response will look similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                       }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                       }
    ServiceKey                       : **************************************
    Peerings                         : []

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="6dbf5-166">7. Yönlendirme yapılandırması oluşturma</span><span class="sxs-lookup"><span data-stu-id="6dbf5-166">7. Create your routing configuration</span></span>
<span data-ttu-id="6dbf5-167">Merhaba adım adım yönergeler için bkz: [expressroute bağlantı hattı yönlendirme yapılandırması](expressroute-howto-routing-arm.md) makale toocreate ve hattı eşlemeler değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-167">For step-by-step instructions, see hello [ExpressRoute circuit routing configuration](expressroute-howto-routing-arm.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6dbf5-168">Bu yönergeler yalnızca Katman 2 bağlantı hizmetleri sunan hizmet sağlayıcıları ile oluşturulan toocircuits geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-168">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="6dbf5-169">Yönetilen sunan bir hizmet sağlayıcısı kullanıyorsanız, Katman 3 Hizmetleri (genellikle bir IP VPN, MPLS gibi), bağlantı sağlayıcınız yapılandırmak ve yönetmek için yönlendirme.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-169">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="6dbf5-170">8. Sanal ağ tooan expressroute bağlantı hattı bağlantı</span><span class="sxs-lookup"><span data-stu-id="6dbf5-170">8. Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="6dbf5-171">Ardından, sanal ağ tooyour expressroute bağlantı hattı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-171">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="6dbf5-172">Kullanım hello [sanal bağlama ağları tooExpressRoute devreler](expressroute-howto-linkvnet-arm.md) hello Resource Manager dağıtım modeliyle çalışırken makalesi.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-172">Use hello [Linking virtual networks tooExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with hello Resource Manager deployment model.</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="6dbf5-173">Bir expressroute bağlantı hattı Hello durumunu alma</span><span class="sxs-lookup"><span data-stu-id="6dbf5-173">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="6dbf5-174">Hello kullanarak herhangi bir zamanda bu bilgiler alabilirsiniz **Get-AzureRmExpressRouteCircuit** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-174">You can retrieve this information at any time by using hello **Get-AzureRmExpressRouteCircuit** cmdlet.</span></span> <span data-ttu-id="6dbf5-175">Merhaba parametresiz çağrısı yaparak tüm hello devreleri listeler.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-175">Making hello call with no parameters lists all hello circuits.</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="6dbf5-176">Merhaba yanıt aşağıdaki örneğine benzer toohello olacaktır:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-176">hello response will be similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                       }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                            "ServiceProviderName": "Equinix",
                                            "PeeringLocation": "Silicon Valley",
                                            "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


<span data-ttu-id="6dbf5-177">Merhaba kaynak grubu adı ve bağlantı hattı adı parametresi toohello araması olarak geçirerek belirli bir expressroute bağlantı hattı hakkında bilgi alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-177">You can get information on a specific ExpressRoute circuit by passing hello resource group name and circuit name as a parameter toohello call:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="6dbf5-178">Merhaba yanıt aşağıdaki örneğine benzer toohello görünür:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-178">hello response will look similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                            "Tier": "Standard",
                                            "Family": "MeteredData"
                                          }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


<span data-ttu-id="6dbf5-179">Merhaba aşağıdaki komutu çalıştırarak tüm hello parametrelerin ayrıntılı açıklamaları alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-179">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <span data-ttu-id="6dbf5-180"><a name="modify"></a>Bir expressroute bağlantı hattı değiştirme</span><span class="sxs-lookup"><span data-stu-id="6dbf5-180"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="6dbf5-181">Bağlantı etkilemeden belirli bir expressroute bağlantı hattı özelliklerini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-181">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="6dbf5-182">Yapabileceğiniz kapalı kalma süresi ile aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-182">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="6dbf5-183">Etkinleştirmek veya devre dışı bir expressroute bağlantı hattı için ExpressRoute premium eklentisi.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-183">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="6dbf5-184">Artış hello bant genişliği, expressroute bağlantı hattı var. kapasite kullanılabilir hello bağlantı noktasında sağlanır.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-184">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="6dbf5-185">Bir bağlantı hattının Hello bant genişliği önceki sürüme indirme desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-185">Downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="6dbf5-186">Ölçülen veri tooUnlimited veri planından ölçümü hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-186">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="6dbf5-187">Sınırsız veri tooMetered veri desteklenmiyor planından ölçümü hello değiştirme.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-187">Changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="6dbf5-188">Etkinleştirme ve devre dışı *izin Klasik işlemleri*.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-188">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="6dbf5-189">Toohello sınırlar ve sınırlamalar hakkında daha fazla bilgi için bkz [ExpressRoute SSS](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="6dbf5-189">For more information on limits and limitations, refer toohello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="6dbf5-190">tooenable hello ExpressRoute premium eklentisi</span><span class="sxs-lookup"><span data-stu-id="6dbf5-190">tooenable hello ExpressRoute premium add-on</span></span>
<span data-ttu-id="6dbf5-191">PowerShell parçacığını aşağıdaki hello kullanarak, varolan bağlantı hattınız için hello ExpressRoute premium eklentisi etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-191">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

<span data-ttu-id="6dbf5-192">Merhaba hattı şimdi hello ExpressRoute premium eklentisi özellikleri etkin olacaktır.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-192">hello circuit will now have hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="6dbf5-193">Merhaba komutu başarıyla çalıştırıldı hemen için hello premium eklenti özelliğini faturalama işlemini başlatacak.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-193">We will begin billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="6dbf5-194">toodisable hello ExpressRoute premium eklentisi</span><span class="sxs-lookup"><span data-stu-id="6dbf5-194">toodisable hello ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6dbf5-195">Merhaba standart bağlantı hattı için izin daha büyük olan kaynaklar kullanıyorsanız, bu işlemi başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-195">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

<span data-ttu-id="6dbf5-196">Merhaba aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-196">Note hello following:</span></span>

* <span data-ttu-id="6dbf5-197">Premium toostandard düşürmek önce bağlı sanal ağlar hello sayıdaki emin olmalısınız toohello devre 10'dan oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-197">Before you downgrade from premium toostandard, you must ensure that hello number of virtual networks that are linked toohello circuit is less than 10.</span></span> <span data-ttu-id="6dbf5-198">Bunu yapmazsanız, güncelleştirme isteği başarısız olur ve biz premium oranlarda faturalanacağı.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-198">If you don't do this, your update request fails, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="6dbf5-199">Tüm sanal ağları diğer coğrafi bölgelerde bağlantısını gerekir.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-199">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="6dbf5-200">Bunu yapmazsanız, güncelleştirme isteği başarısız olur ve biz premium oranlarda faturalanacağı.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-200">If you don't do this, your update request will fail, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="6dbf5-201">Yol tablosu özel eşleme için 4. 000'den az yolları olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-201">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="6dbf5-202">Rota tablosu boyutunuz 4.000 yolları büyükse hello BGP oturumu bırakır ve 4.000 tanıtılan önekler hello sayısı gider kadar yeniden iler hale olmaz.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-202">If your route table size is greater than 4,000 routes, hello BGP session drops and won't be reenabled until hello number of advertised prefixes goes below 4,000.</span></span>

<span data-ttu-id="6dbf5-203">Merhaba ExpressRoute premium eklentisi hello varolan hattı için PowerShell cmdlet aşağıdaki hello kullanarak devre dışı bırakabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-203">You can disable hello ExpressRoute premium add-on for hello existing circuit by using hello following PowerShell cmdlet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="6dbf5-204">tooupdate hello ExpressRoute devresi bant genişliği</span><span class="sxs-lookup"><span data-stu-id="6dbf5-204">tooupdate hello ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="6dbf5-205">Merhaba denetimi sağlayıcınız için desteklenen bant genişliği seçenekleri için [ExpressRoute SSS](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="6dbf5-205">For supported bandwidth options for your provider, check hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="6dbf5-206">Var olan bağlantı hattınız hello boyutundan büyük herhangi bir boyutta seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-206">You can pick any size greater than hello size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6dbf5-207">Merhaba varolan bağlantı noktasında yetersiz kapasite ise toorecreate hello expressroute bağlantı hattı olabilir.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-207">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="6dbf5-208">Varsa hiçbir ek kapasite kullanılabilir o konumda hello hattı yükseltemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-208">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="6dbf5-209">Bir expressroute bağlantı hattı kesintiye uğratmadan hello bant genişliği azaltma olamaz.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-209">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="6dbf5-210">Bant genişliği eski sürüme düşürmeyi toodeprovision hello expressroute bağlantı hattı gerektirir ve yeni bir expressroute bağlantı hattı yeniden sağlayın.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-210">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 

<span data-ttu-id="6dbf5-211">Gereksinim boyutu karar verdikten sonra komutu tooresize aşağıdaki hello hattınız kullanın:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-211">After you decide what size you need, use hello following command tooresize your circuit:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


<span data-ttu-id="6dbf5-212">Bağlantı hattınız hello Microsoft tarafında boyutlandırılıp.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-212">Your circuit will be sized up on hello Microsoft side.</span></span> <span data-ttu-id="6dbf5-213">Ardından bu değişikliği kendi yan toomatch, bağlantı sağlayıcısı tooupdate yapılandırmalarında başvurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-213">Then you must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="6dbf5-214">Bu bildirim yaptıktan sonra biz güncelleştirilmiş hello bant seçeneği için faturalama başlar.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-214">After you make this notification, we will begin billing you for hello updated bandwidth option.</span></span>

### <a name="toomove-hello-sku-from-metered-toounlimited"></a><span data-ttu-id="6dbf5-215">ölçülen toounlimited gelen toomove hello SKU</span><span class="sxs-lookup"><span data-stu-id="6dbf5-215">toomove hello SKU from metered toounlimited</span></span>
<span data-ttu-id="6dbf5-216">PowerShell parçacığını aşağıdaki hello kullanarak hello ExpressRoute devresi SKU'su değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-216">You can change hello SKU of an ExpressRoute circuit by using hello following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a><span data-ttu-id="6dbf5-217">toocontrol erişim toohello Klasik ve Resource Manager ortamları</span><span class="sxs-lookup"><span data-stu-id="6dbf5-217">toocontrol access toohello classic and Resource Manager environments</span></span>
<span data-ttu-id="6dbf5-218">Merhaba yönergeleri gözden [taşıma ExpressRoute bağlantı hatları hello Klasik toohello Resource Manager dağıtım modelinde](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="6dbf5-218">Review hello instructions in [Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>  

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="6dbf5-219">Sağlamayı kaldırmayı ve bir expressroute bağlantı hattı silme</span><span class="sxs-lookup"><span data-stu-id="6dbf5-219">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="6dbf5-220">Merhaba aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-220">Note hello following:</span></span>

* <span data-ttu-id="6dbf5-221">Tüm sanal ağlardan hello expressroute bağlantı hattı bağlantısını gerekir.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-221">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="6dbf5-222">Bu işlem başarısız olursa, tüm sanal ağ olup olmadığını toosee toohello hattı bağlı denetleyin.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-222">If this operation fails, check toosee if any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="6dbf5-223">Merhaba ExpressRoute bağlantı hattı Hizmet Sağlayıcısı sağlama durumu ise **sağlama** veya **hazırlandı** kendi tarafında hizmet sağlayıcısı toodeprovision hello hattınız ile çalışmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-223">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="6dbf5-224">Biz tooreserve kaynakları devam edecek ve hello hizmet sağlayıcısı sağlamayı hello hattı tamamlandıktan ve bize bildiren kadar sizi faturalandırmak.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-224">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="6dbf5-225">Merhaba hizmet sağlayıcısı hello hattı sağlaması kaldırılıyor. sağlaması değilse (Merhaba Hizmet Sağlayıcısı sağlama durumu çok ayarlamak**sağlanmadı**) hello hattı sonra silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6dbf5-225">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="6dbf5-226">Bu hello hattı için fatura durdurur</span><span class="sxs-lookup"><span data-stu-id="6dbf5-226">This will stop billing for hello circuit</span></span>

<span data-ttu-id="6dbf5-227">Hello aşağıdaki komutu çalıştırarak, expressroute bağlantı hattı silebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-227">You can delete your ExpressRoute circuit by running hello following command:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a><span data-ttu-id="6dbf5-228">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6dbf5-228">Next steps</span></span>

<span data-ttu-id="6dbf5-229">Bağlantı hattınız oluşturduktan sonra aşağıdaki hello emin olun:</span><span class="sxs-lookup"><span data-stu-id="6dbf5-229">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="6dbf5-230">Oluşturma ve expressroute bağlantı hattı için yönlendirmeyi değiştirme</span><span class="sxs-lookup"><span data-stu-id="6dbf5-230">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="6dbf5-231">Sanal ağ tooyour expressroute bağlantı hattı bağlantı</span><span class="sxs-lookup"><span data-stu-id="6dbf5-231">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)
