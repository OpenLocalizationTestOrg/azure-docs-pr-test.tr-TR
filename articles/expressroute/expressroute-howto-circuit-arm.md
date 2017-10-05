---
title: "Oluşturma ve bir expressroute bağlantı hattı değiştirme: PowerShell: Azure Resource Manager | Microsoft Docs"
description: "Bu makalede, oluşturmak, sağlamak, doğrulayın, güncelleştirme, silme ve bir expressroute bağlantı hattı yetkisini kaldırma açıklar."
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
ms.openlocfilehash: 8bfae39d84aaac3b9527084df9dcfbd51f591dfe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="1a554-103">Oluşturma ve PowerShell kullanarak bir expressroute bağlantı hattı değiştirme</span><span class="sxs-lookup"><span data-stu-id="1a554-103">Create and modify an ExpressRoute circuit using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1a554-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="1a554-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="1a554-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1a554-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="1a554-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1a554-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="1a554-107">Video - Azure portalı</span><span class="sxs-lookup"><span data-stu-id="1a554-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="1a554-108">PowerShell (klasik)</span><span class="sxs-lookup"><span data-stu-id="1a554-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="1a554-109">Bu makalede PowerShell cmdlet'leri ve Azure Resource Manager dağıtım modeli kullanarak bir Azure expressroute oluşturmayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="1a554-109">This article describes how to create an Azure ExpressRoute circuit by using PowerShell cmdlets and the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="1a554-110">Bu makalede ayrıca devrenin durumunu denetleyin, güncelleştirme veya silme ve onu yetkisini kaldırma kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="1a554-110">This article also shows you how to check the status of the circuit, update it, or delete and deprovision it.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1a554-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="1a554-111">Before you begin</span></span>
* <span data-ttu-id="1a554-112">Azure Resource Manager PowerShell cmdlet'lerinin en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1a554-112">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="1a554-113">Daha fazla bilgi için bkz: [Azure PowerShell genel bakış](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1a554-113">For more information, see [Overview of Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="1a554-114">Gözden geçirme [Önkoşullar](expressroute-prerequisites.md) ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="1a554-114">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>


## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="1a554-115">Oluşturma ve bir expressroute bağlantı hattı sağlama</span><span class="sxs-lookup"><span data-stu-id="1a554-115">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-to-your-azure-account-and-select-your-subscription"></a><span data-ttu-id="1a554-116">1. Azure hesabınızda oturum açın ve aboneliğinizi seçin</span><span class="sxs-lookup"><span data-stu-id="1a554-116">1. Sign in to your Azure account and select your subscription</span></span>
<span data-ttu-id="1a554-117">Yapılandırmanızı başlamak için Azure hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1a554-117">To begin your configuration, sign in to your Azure account.</span></span> <span data-ttu-id="1a554-118">Aşağıdaki örnekler bağlanmanıza yardımcı olması için kullanın:</span><span class="sxs-lookup"><span data-stu-id="1a554-118">Use the following examples to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="1a554-119">Hesap için abonelikleri kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="1a554-119">Check the subscriptions for the account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="1a554-120">Bir expressroute bağlantı hattı için oluşturmak istediğiniz aboneliği seçin:</span><span class="sxs-lookup"><span data-stu-id="1a554-120">Select the subscription that you want to create an ExpressRoute circuit for:</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-the-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="1a554-121">2. Desteklenen sağlayıcılar, konumları ve bant genişlikleri listesini alma</span><span class="sxs-lookup"><span data-stu-id="1a554-121">2. Get the list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="1a554-122">Bir expressroute bağlantı hattı oluşturmadan önce desteklenen bağlantı sağlayıcıları, konumları ve bant seçeneklerini listesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="1a554-122">Before you create an ExpressRoute circuit, you need the list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="1a554-123">PowerShell cmdlet **Get-AzureRmExpressRouteServiceProvider** , sonraki adımlarda kullanacağınız bu bilgiler verir:</span><span class="sxs-lookup"><span data-stu-id="1a554-123">The PowerShell cmdlet **Get-AzureRmExpressRouteServiceProvider** returns this information, which you’ll use in later steps:</span></span>

```powershell
Get-AzureRmExpressRouteServiceProvider
```

<span data-ttu-id="1a554-124">Bağlantı sağlayıcınız listelenip listelenmediğini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="1a554-124">Check to see if your connectivity provider is listed there.</span></span> <span data-ttu-id="1a554-125">Aşağıdaki bilgileri not edin.</span><span class="sxs-lookup"><span data-stu-id="1a554-125">Make a note of the following information.</span></span> <span data-ttu-id="1a554-126">Bir bağlantı hattı oluşturduğunuzda, daha sonra gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="1a554-126">You'll need it later when you create a circuit.</span></span>

* <span data-ttu-id="1a554-127">Ad</span><span class="sxs-lookup"><span data-stu-id="1a554-127">Name</span></span>
* <span data-ttu-id="1a554-128">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="1a554-128">PeeringLocations</span></span>
* <span data-ttu-id="1a554-129">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="1a554-129">BandwidthsOffered</span></span>

<span data-ttu-id="1a554-130">Artık bir expressroute bağlantı hattı oluşturmak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="1a554-130">You're now ready to create an ExpressRoute circuit.</span></span>   

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="1a554-131">3. ExpressRoute bağlantı hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1a554-131">3. Create an ExpressRoute circuit</span></span>
<span data-ttu-id="1a554-132">Bir kaynak grubu zaten yoksa, expressroute bağlantı hattı oluşturmadan önce bir oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1a554-132">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="1a554-133">Aşağıdaki komutu çalıştırarak bunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1a554-133">You can do so by running the following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


<span data-ttu-id="1a554-134">Aşağıdaki örnek 200 MB/sn expressroute bağlantı hattı üzerinden Equinix Silikon Vadisi'nde oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="1a554-134">The following example shows how to create a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="1a554-135">Farklı bir sağlayıcı ve farklı ayarlar kullanıyorsanız, bu bilgileri isteğiniz yaptığınızda değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1a554-135">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> <span data-ttu-id="1a554-136">Yeni bir hizmet anahtarı için bir örnek isteği verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1a554-136">The following is an example request for a new service key:</span></span>

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

<span data-ttu-id="1a554-137">SKU ailesi ve doğru SKU katmanı belirttiğinizden emin olun:</span><span class="sxs-lookup"><span data-stu-id="1a554-137">Make sure that you specify the correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="1a554-138">SKU katmanı, bir ExpressRoute standart ya da bir ExpressRoute premium Eklentisi etkin olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="1a554-138">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="1a554-139">Belirleyebileceğiniz *standart* standart SKU almak için veya *Premium* premium eklenti için.</span><span class="sxs-lookup"><span data-stu-id="1a554-139">You can specify *Standard* to get the standard SKU or *Premium* for the premium add-on.</span></span>
* <span data-ttu-id="1a554-140">SKU ailesi faturalama türü belirler.</span><span class="sxs-lookup"><span data-stu-id="1a554-140">SKU family determines the billing type.</span></span> <span data-ttu-id="1a554-141">Belirleyebileceğiniz *Metereddata* ölçülen veri planı için ve *Unlimiteddata* sınırsız veri planı için.</span><span class="sxs-lookup"><span data-stu-id="1a554-141">You can specify *Metereddata* for a metered data plan and *Unlimiteddata* for an unlimited data plan.</span></span> <span data-ttu-id="1a554-142">Fatura türünden değiştirebileceğiniz *Metereddata* için *Unlimiteddata*, ancak türünden değiştiremezsiniz *Unlimiteddata* için *Metereddata*.</span><span class="sxs-lookup"><span data-stu-id="1a554-142">You can change the billing type from *Metereddata* to *Unlimiteddata*, but you can't change the type from *Unlimiteddata* to *Metereddata*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a554-143">ExpressRoute bağlantı hattınız bir hizmet anahtarı verilen andan itibaren Fatura edilecek.</span><span class="sxs-lookup"><span data-stu-id="1a554-143">Your ExpressRoute circuit will be billed from the moment a service key is issued.</span></span> <span data-ttu-id="1a554-144">Bağlantı sağlayıcı bağlantı hattı sağlamak hazır olduğunda bu işlemi gerçekleştirmek emin olun.</span><span class="sxs-lookup"><span data-stu-id="1a554-144">Ensure that you perform this operation when the connectivity provider is ready to provision the circuit.</span></span>
> 
> 

<span data-ttu-id="1a554-145">Yanıt hizmet anahtarını içerir.</span><span class="sxs-lookup"><span data-stu-id="1a554-145">The response contains the service key.</span></span> <span data-ttu-id="1a554-146">Aşağıdaki komutu çalıştırarak tüm parametrelerin ayrıntılı açıklamaları alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1a554-146">You can get detailed descriptions of all the parameters by running the following command:</span></span>

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="1a554-147">4. Tüm ExpressRoute bağlantı hatları listesi</span><span class="sxs-lookup"><span data-stu-id="1a554-147">4. List all ExpressRoute circuits</span></span>
<span data-ttu-id="1a554-148">Oluşturduğunuz tüm expressroute bağlantı hatları listesini almak için çalıştırın **Get-AzureRmExpressRouteCircuit** komutu:</span><span class="sxs-lookup"><span data-stu-id="1a554-148">To get a list of all the ExpressRoute circuits that you created, run the **Get-AzureRmExpressRouteCircuit** command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

<span data-ttu-id="1a554-149">Yanıt aşağıdaki örneğe benzer görünür:</span><span class="sxs-lookup"><span data-stu-id="1a554-149">The response will look similar to the following example:</span></span>

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

<span data-ttu-id="1a554-150">Herhangi bir zamanda bu bilgileri kullanarak alabilirsiniz `Get-AzureRmExpressRouteCircuit` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="1a554-150">You can retrieve this information at any time by using the `Get-AzureRmExpressRouteCircuit` cmdlet.</span></span> <span data-ttu-id="1a554-151">Hiçbir parametre çağrıyı yapan tüm devreler listeler.</span><span class="sxs-lookup"><span data-stu-id="1a554-151">Making the call with no parameters lists all the circuits.</span></span> <span data-ttu-id="1a554-152">Hizmet anahtarınız listelenen *ServiceKey* alan:</span><span class="sxs-lookup"><span data-stu-id="1a554-152">Your service key will be listed in the *ServiceKey* field:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="1a554-153">Yanıt aşağıdaki örneğe benzer görünür:</span><span class="sxs-lookup"><span data-stu-id="1a554-153">The response will look similar to the following example:</span></span>

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


<span data-ttu-id="1a554-154">Aşağıdaki komutu çalıştırarak tüm parametrelerin ayrıntılı açıklamaları alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1a554-154">You can get detailed descriptions of all the parameters by running the following command:</span></span>

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="1a554-155">5. Hizmet anahtarı sağlamak için bağlantı sağlayıcınızı Gönder</span><span class="sxs-lookup"><span data-stu-id="1a554-155">5. Send the service key to your connectivity provider for provisioning</span></span>
<span data-ttu-id="1a554-156">*ServiceProviderProvisioningState* hizmet sağlayıcı tarafında sağlama geçerli durumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1a554-156">*ServiceProviderProvisioningState* provides information about the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="1a554-157">Durum Microsoft tarafında durumunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="1a554-157">Status provides the state on the Microsoft side.</span></span> <span data-ttu-id="1a554-158">Bağlantı hattı durumları sağlama hakkında daha fazla bilgi için bkz: [iş akışları](expressroute-workflows.md#expressroute-circuit-provisioning-states) makalesi.</span><span class="sxs-lookup"><span data-stu-id="1a554-158">For more information about circuit provisioning states, see the [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="1a554-159">Yeni bir expressroute bağlantı hattı oluşturduğunuzda, bağlantı hattı şu durumda olacaktır:</span><span class="sxs-lookup"><span data-stu-id="1a554-159">When you create a new ExpressRoute circuit, the circuit will be in the following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



<span data-ttu-id="1a554-160">Bağlantı sağlayıcı onu sizin için etkinleştirme sürecinde olduğunda bağlantı hattı aşağıdaki durumuna değiştirin:</span><span class="sxs-lookup"><span data-stu-id="1a554-160">The circuit will change to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="1a554-161">Bir expressroute bağlantı hattı kullanabilmek için şu durumda olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="1a554-161">For you to be able to use an ExpressRoute circuit, it must be in the following state:</span></span>

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="1a554-162">6. Durum ve hattı anahtar durumunu düzenli aralıklarla denetleyin</span><span class="sxs-lookup"><span data-stu-id="1a554-162">6. Periodically check the status and the state of the circuit key</span></span>
<span data-ttu-id="1a554-163">Durum ve hattı anahtar durumunu denetleme, sağlayıcınız hattınız etkin olduğunda bilmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1a554-163">Checking the status and the state of the circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="1a554-164">Bağlantı hattı yapılandırıldıktan sonra *ServiceProviderProvisioningState* olarak görünür *hazırlandı*, aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="1a554-164">After the circuit has been configured, *ServiceProviderProvisioningState* appears as *Provisioned*, as shown in the following example:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="1a554-165">Yanıt aşağıdaki örneğe benzer görünür:</span><span class="sxs-lookup"><span data-stu-id="1a554-165">The response will look similar to the following example:</span></span>

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

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="1a554-166">7. Yönlendirme yapılandırması oluşturma</span><span class="sxs-lookup"><span data-stu-id="1a554-166">7. Create your routing configuration</span></span>
<span data-ttu-id="1a554-167">Adım adım yönergeler için bkz: [expressroute bağlantı hattı yönlendirme yapılandırması](expressroute-howto-routing-arm.md) oluşturup hattı eşlemeler değiştirmek için makale.</span><span class="sxs-lookup"><span data-stu-id="1a554-167">For step-by-step instructions, see the [ExpressRoute circuit routing configuration](expressroute-howto-routing-arm.md) article to create and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a554-168">Bu yönergeler yalnızca Katman 2 bağlantı hizmetleri sunan hizmet sağlayıcıları ile oluşturulan bağlantı hatları için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1a554-168">These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="1a554-169">Yönetilen sunan bir hizmet sağlayıcısı kullanıyorsanız, Katman 3 Hizmetleri (genellikle bir IP VPN, MPLS gibi), bağlantı sağlayıcınız yapılandırmak ve yönetmek için yönlendirme.</span><span class="sxs-lookup"><span data-stu-id="1a554-169">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="1a554-170">8. ExpressRoute bağlantı hattına bir sanal ağı bağlama</span><span class="sxs-lookup"><span data-stu-id="1a554-170">8. Link a virtual network to an ExpressRoute circuit</span></span>
<span data-ttu-id="1a554-171">Ardından, bir sanal ağ, expressroute bağlantı hattına bağlayın.</span><span class="sxs-lookup"><span data-stu-id="1a554-171">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="1a554-172">Kullanım [ExpressRoute bağlantı hatları için sanal ağları bağlama](expressroute-howto-linkvnet-arm.md) makale Resource Manager dağıtım modeliyle çalışırken.</span><span class="sxs-lookup"><span data-stu-id="1a554-172">Use the [Linking virtual networks to ExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with the Resource Manager deployment model.</span></span>

## <a name="getting-the-status-of-an-expressroute-circuit"></a><span data-ttu-id="1a554-173">Bir expressroute bağlantı hattı durumunu alma</span><span class="sxs-lookup"><span data-stu-id="1a554-173">Getting the status of an ExpressRoute circuit</span></span>
<span data-ttu-id="1a554-174">Herhangi bir zamanda bu bilgileri kullanarak alabilirsiniz **Get-AzureRmExpressRouteCircuit** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="1a554-174">You can retrieve this information at any time by using the **Get-AzureRmExpressRouteCircuit** cmdlet.</span></span> <span data-ttu-id="1a554-175">Hiçbir parametre çağrıyı yapan tüm devreler listeler.</span><span class="sxs-lookup"><span data-stu-id="1a554-175">Making the call with no parameters lists all the circuits.</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="1a554-176">Yanıt aşağıdaki örneğe benzer olacaktır:</span><span class="sxs-lookup"><span data-stu-id="1a554-176">The response will be similar to the following example:</span></span>

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


<span data-ttu-id="1a554-177">Kaynak grubu adı ve bağlantı hattı adı çağrısına parametre olarak geçirerek belirli bir expressroute bağlantı hattı hakkında bilgi alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1a554-177">You can get information on a specific ExpressRoute circuit by passing the resource group name and circuit name as a parameter to the call:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="1a554-178">Yanıt aşağıdaki örneğe benzer görünür:</span><span class="sxs-lookup"><span data-stu-id="1a554-178">The response will look similar to the following example:</span></span>

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


<span data-ttu-id="1a554-179">Aşağıdaki komutu çalıştırarak tüm parametrelerin ayrıntılı açıklamaları alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1a554-179">You can get detailed descriptions of all the parameters by running the following command:</span></span>

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <span data-ttu-id="1a554-180"><a name="modify"></a>Bir expressroute bağlantı hattı değiştirme</span><span class="sxs-lookup"><span data-stu-id="1a554-180"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="1a554-181">Bağlantı etkilemeden belirli bir expressroute bağlantı hattı özelliklerini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a554-181">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="1a554-182">Kapalı kalma süresi olmadan aşağıdakileri yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1a554-182">You can do the following with no downtime:</span></span>

* <span data-ttu-id="1a554-183">Etkinleştirmek veya devre dışı bir expressroute bağlantı hattı için ExpressRoute premium eklentisi.</span><span class="sxs-lookup"><span data-stu-id="1a554-183">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="1a554-184">Sağlanmış kapasite kullanılabilir bağlantı noktası, expressroute bağlantı hattı bant genişliğini artırır.</span><span class="sxs-lookup"><span data-stu-id="1a554-184">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="1a554-185">Bir bağlantı hattının bant genişliğini önceki sürüme indirme desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="1a554-185">Downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="1a554-186">Ölçüm plan sınırsız veri ölçülen verilerden değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1a554-186">Change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="1a554-187">Ölçüm plan sınırsız verilerden ölçülen verileri değiştirme desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="1a554-187">Changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="1a554-188">Etkinleştirme ve devre dışı *izin Klasik işlemleri*.</span><span class="sxs-lookup"><span data-stu-id="1a554-188">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="1a554-189">Sınırlar ve sınırlamalar hakkında daha fazla bilgi için başvurmak [ExpressRoute SSS](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="1a554-189">For more information on limits and limitations, refer to the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="to-enable-the-expressroute-premium-add-on"></a><span data-ttu-id="1a554-190">ExpressRoute premium eklentisi etkinleştirmek için</span><span class="sxs-lookup"><span data-stu-id="1a554-190">To enable the ExpressRoute premium add-on</span></span>
<span data-ttu-id="1a554-191">Aşağıdaki PowerShell parçacığını kullanarak, varolan bağlantı hattınız için ExpressRoute premium eklentisi etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1a554-191">You can enable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

<span data-ttu-id="1a554-192">Bağlantı hattı şimdi etkin ExpressRoute premium eklentisi özellikleri sahip olur.</span><span class="sxs-lookup"><span data-stu-id="1a554-192">The circuit will now have the ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="1a554-193">Komut başarıyla çalıştırıldı hemen premium eklenti özellik faturalama işlemini başlatacak.</span><span class="sxs-lookup"><span data-stu-id="1a554-193">We will begin billing you for the premium add-on capability as soon as the command has successfully run.</span></span>

### <a name="to-disable-the-expressroute-premium-add-on"></a><span data-ttu-id="1a554-194">ExpressRoute premium eklentisi devre dışı bırakmak için</span><span class="sxs-lookup"><span data-stu-id="1a554-194">To disable the ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1a554-195">Standart bağlantı hattı için izin daha büyük olan kaynaklar kullanıyorsanız, bu işlemi başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="1a554-195">This operation can fail if you're using resources that are greater than what is permitted for the standard circuit.</span></span>
> 
> 

<span data-ttu-id="1a554-196">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="1a554-196">Note the following:</span></span>

* <span data-ttu-id="1a554-197">Standart Premium'dan düşürmek önce devresine bağlı sanal ağlar sayısı 10'dan az olduğundan emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="1a554-197">Before you downgrade from premium to standard, you must ensure that the number of virtual networks that are linked to the circuit is less than 10.</span></span> <span data-ttu-id="1a554-198">Bunu yapmazsanız, güncelleştirme isteği başarısız olur ve biz premium oranlarda faturalanacağı.</span><span class="sxs-lookup"><span data-stu-id="1a554-198">If you don't do this, your update request fails, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="1a554-199">Tüm sanal ağları diğer coğrafi bölgelerde bağlantısını gerekir.</span><span class="sxs-lookup"><span data-stu-id="1a554-199">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="1a554-200">Bunu yapmazsanız, güncelleştirme isteği başarısız olur ve biz premium oranlarda faturalanacağı.</span><span class="sxs-lookup"><span data-stu-id="1a554-200">If you don't do this, your update request will fail, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="1a554-201">Yol tablosu özel eşleme için 4. 000'den az yolları olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1a554-201">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="1a554-202">Rota tablosu boyutunuz 4.000 yolları büyükse, BGP oturumu bırakır ve 4.000 tanıtılan ön ek sayısı gider kadar yeniden iler hale olmaz.</span><span class="sxs-lookup"><span data-stu-id="1a554-202">If your route table size is greater than 4,000 routes, the BGP session drops and won't be reenabled until the number of advertised prefixes goes below 4,000.</span></span>

<span data-ttu-id="1a554-203">Aşağıdaki PowerShell cmdlet'ini kullanarak var olan bağlantı hattı için ExpressRoute premium eklentisi devre dışı bırakabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1a554-203">You can disable the ExpressRoute premium add-on for the existing circuit by using the following PowerShell cmdlet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-update-the-expressroute-circuit-bandwidth"></a><span data-ttu-id="1a554-204">ExpressRoute bağlantı hattı bant genişliğini güncelleştirmek için</span><span class="sxs-lookup"><span data-stu-id="1a554-204">To update the ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="1a554-205">Denetimi sağlayıcınız için desteklenen bant genişliği seçenekleri için [ExpressRoute SSS](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="1a554-205">For supported bandwidth options for your provider, check the [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="1a554-206">Var olan bağlantı hattınız boyutundan büyük herhangi bir boyutta seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a554-206">You can pick any size greater than the size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a554-207">Varolan bir bağlantı üzerinde yetersiz kapasite ise expressroute bağlantı hattı yeniden başlatmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="1a554-207">You may have to recreate the ExpressRoute circuit if there is inadequate capacity on the existing port.</span></span> <span data-ttu-id="1a554-208">Varsa hiçbir ek kapasite kullanılabilir o konumda bağlantı hattı yükseltemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a554-208">You cannot upgrade the circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="1a554-209">Bir expressroute bağlantı hattı kesintiye uğratmadan bant indiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a554-209">You cannot reduce the bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="1a554-210">Bant genişliği eski sürüme düşürmeyi expressroute bağlantı hattı yetkisini kaldırma ve yeni bir expressroute bağlantı hattı yeniden hazırlayana gerektirir.</span><span class="sxs-lookup"><span data-stu-id="1a554-210">Downgrading bandwidth requires you to deprovision the ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 

<span data-ttu-id="1a554-211">Gereksinim boyutu karar verdikten sonra bağlantı hattınız yeniden boyutlandırmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1a554-211">After you decide what size you need, use the following command to resize your circuit:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


<span data-ttu-id="1a554-212">Bağlantı hattınız Microsoft tarafında boyutlandırılıp.</span><span class="sxs-lookup"><span data-stu-id="1a554-212">Your circuit will be sized up on the Microsoft side.</span></span> <span data-ttu-id="1a554-213">Ardından bu değişikliği eşleşecek şekilde kendi tarafında yapılandırmalar güncelleştirileceğini bağlantı sağlayıcınız başvurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1a554-213">Then you must contact your connectivity provider to update configurations on their side to match this change.</span></span> <span data-ttu-id="1a554-214">Bu bildirim yaptıktan sonra biz güncelleştirilmiş bant seçeneği için faturalama başlar.</span><span class="sxs-lookup"><span data-stu-id="1a554-214">After you make this notification, we will begin billing you for the updated bandwidth option.</span></span>

### <a name="to-move-the-sku-from-metered-to-unlimited"></a><span data-ttu-id="1a554-215">SKU taşımak için sınırsız olarak ölçülen</span><span class="sxs-lookup"><span data-stu-id="1a554-215">To move the SKU from metered to unlimited</span></span>
<span data-ttu-id="1a554-216">Aşağıdaki PowerShell parçacığını kullanarak ExpressRoute devresi SKU'su değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1a554-216">You can change the SKU of an ExpressRoute circuit by using the following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-control-access-to-the-classic-and-resource-manager-environments"></a><span data-ttu-id="1a554-217">Klasik ve Resource Manager ortamları erişimi denetlemek için</span><span class="sxs-lookup"><span data-stu-id="1a554-217">To control access to the classic and Resource Manager environments</span></span>
<span data-ttu-id="1a554-218">' Ndaki yönergeleri gözden [Resource Manager dağıtım modeline taşıma ExpressRoute bağlantı hatları Klasik](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="1a554-218">Review the instructions in [Move ExpressRoute circuits from the classic to the Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>  

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="1a554-219">Sağlamayı kaldırmayı ve bir expressroute bağlantı hattı silme</span><span class="sxs-lookup"><span data-stu-id="1a554-219">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="1a554-220">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="1a554-220">Note the following:</span></span>

* <span data-ttu-id="1a554-221">Expressroute bağlantı hattı tüm sanal ağlardan bağlantısını gerekir.</span><span class="sxs-lookup"><span data-stu-id="1a554-221">You must unlink all virtual networks from the ExpressRoute circuit.</span></span> <span data-ttu-id="1a554-222">Bu işlem başarısız olursa, bağlantı hattı için herhangi bir sanal ağa bağlı olan denetleyin.</span><span class="sxs-lookup"><span data-stu-id="1a554-222">If this operation fails, check to see if any virtual networks are linked to the circuit.</span></span>
* <span data-ttu-id="1a554-223">Sağlama durumu ExpressRoute bağlantı hattı hizmet sağlayıcı ise **sağlama** veya **hazırlandı** kendi tarafında hattı yetkisini kaldırma için hizmet sağlayıcınıza birlikte çalışmalısınız.</span><span class="sxs-lookup"><span data-stu-id="1a554-223">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="1a554-224">Kaynakları ayırabilir ve hizmet sağlayıcısı devre sağlama kaldırma işlemi tamamlandıktan ve bize bildiren kadar sizi faturalandırmak devam eder.</span><span class="sxs-lookup"><span data-stu-id="1a554-224">We will continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="1a554-225">Hizmet sağlayıcısı hattı sağlaması kaldırılıyor. sağlaması değilse (sağlama durumu hizmet sağlayıcısı kümesine **sağlanmadı**), ardından bağlantı hattı silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a554-225">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**) you can then delete the circuit.</span></span> <span data-ttu-id="1a554-226">Bu bağlantı hattı için fatura durdurur</span><span class="sxs-lookup"><span data-stu-id="1a554-226">This will stop billing for the circuit</span></span>

<span data-ttu-id="1a554-227">Aşağıdaki komutu çalıştırarak, expressroute bağlantı hattı silebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1a554-227">You can delete your ExpressRoute circuit by running the following command:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a><span data-ttu-id="1a554-228">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1a554-228">Next steps</span></span>

<span data-ttu-id="1a554-229">Bağlantı hattınız oluşturduktan sonra aşağıdakileri yaptığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="1a554-229">After you create your circuit, make sure that you do the following:</span></span>

* [<span data-ttu-id="1a554-230">Oluşturma ve expressroute bağlantı hattı için yönlendirmeyi değiştirme</span><span class="sxs-lookup"><span data-stu-id="1a554-230">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="1a554-231">Sanal ağ, ExpressRoute devresine bağlama</span><span class="sxs-lookup"><span data-stu-id="1a554-231">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)
