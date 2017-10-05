---
title: "Yönlendirme (bir ExpressRoute için eşliği) hattı yapılandırma: Resource Manager: PowerShell: Azure | Microsoft Docs"
description: "Bu makalede, bir ExpressRoute bağlantı hattı için özel, ortak ve Microsoft eşlemesinin nasıl oluşturulduğu ve sağlandığı adım adım anlatılmaktadır. Bu makalede ayrıca bağlantı hattınızın durumunu denetleme, bağlantı hattını güncelleştirme veya silme işlemlerinin nasıl yapıldığı da anlatılmaktadır."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a036d51-77ae-4fee-9ddb-35f040fbdcdf
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: af68955b78239832e413e1b59e033d7d3da8d599
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="7b4ca-104">Oluşturma ve PowerShell kullanarak bir ExpressRoute bağlantı hattı için eşlemesini değiştirme</span><span class="sxs-lookup"><span data-stu-id="7b4ca-104">Create and modify peering for an ExpressRoute circuit using PowerShell</span></span>

<span data-ttu-id="7b4ca-105">Bu makalede, Resource Manager dağıtım modelinde PowerShell kullanarak bir expressroute bağlantı hattı için yönlendirme yapılandırması oluşturma ve yönetme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="7b4ca-106">Ayrıca, durumu, güncelleştirme veya silme denetleyin ve bir expressroute bağlantı hattı için eşlemeler sağlamayı sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="7b4ca-107">Bağlantı hattınız ile çalışmak için farklı bir yöntem kullanmak istiyorsanız, bir makale aşağıdaki listeden seçin:</span><span class="sxs-lookup"><span data-stu-id="7b4ca-107">If you want to use a different method to work with your circuit, select an article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7b4ca-108">Azure portal</span><span class="sxs-lookup"><span data-stu-id="7b4ca-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="7b4ca-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b4ca-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="7b4ca-110">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7b4ca-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="7b4ca-111">Video - özel eşliği</span><span class="sxs-lookup"><span data-stu-id="7b4ca-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="7b4ca-112">Video - ortak eşleme</span><span class="sxs-lookup"><span data-stu-id="7b4ca-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="7b4ca-113">Video - Microsoft eşlemesi</span><span class="sxs-lookup"><span data-stu-id="7b4ca-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="7b4ca-114">PowerShell (klasik)</span><span class="sxs-lookup"><span data-stu-id="7b4ca-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="7b4ca-115">Yapılandırma önkoşulları</span><span class="sxs-lookup"><span data-stu-id="7b4ca-115">Configuration prerequisites</span></span>

* <span data-ttu-id="7b4ca-116">Azure Resource Manager PowerShell cmdlet'lerinin en yeni sürümünü gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-116">You will need the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="7b4ca-117">Daha fazla bilgi için bkz. [Azure PowerShell’i yükleme ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7b4ca-117">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> 
* <span data-ttu-id="7b4ca-118">Yapılandırmaya başlamadan önce [önkoşullar](expressroute-prerequisites.md) sayfasını, [yönlendirme gereksinimleri](expressroute-routing.md) sayfasını ve [iş akışları](expressroute-workflows.md) sayfasını gözden geçirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-118">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="7b4ca-119">Etkin bir ExpressRoute bağlantı hattınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="7b4ca-120">Devam etmeden önce [ExpressRoute bağlantı hattı oluşturma](expressroute-howto-circuit-arm.md) yönergelerini izleyin ve bağlantı sağlayıcınızın bağlantı hattını etkinleştirmesini isteyin.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-120">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="7b4ca-121">Expressroute bağlantı hattı, bu makaledeki cmdlet'leri çalıştırılabilmesi sağlanmış ve etkin durumda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-121">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets in this article.</span></span>

<span data-ttu-id="7b4ca-122">Bu yönergeler yalnızca Katman 2 bağlantı hizmetleri sunan hizmet sağlayıcıları ile oluşturulan bağlantı hatları için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-122">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="7b4ca-123">Yönetilen sunan bir hizmet sağlayıcısı kullanıyorsanız, Katman 3 Hizmetleri (genellikle gibi bir IPVPN MPLS), bağlantı sağlayıcınız yapılandırmak ve yönetmek için yönlendirme.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b4ca-124">Şu anda hizmet yönetim portalı aracılığıyla hizmet sağlayıcılar tarafından yapılandırılan eşlemeleri tanıtmıyoruz.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-124">We currently do not advertise peerings configured by service providers through the service management portal.</span></span> <span data-ttu-id="7b4ca-125">Bu özelliği yakında etkinleştirmek için çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-125">We are working on enabling this capability soon.</span></span> <span data-ttu-id="7b4ca-126">BGP eşlemelerini yapılandırmadan önce hizmet sağlayıcınıza başvurun.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-126">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="7b4ca-127">Bir ExpressRoute bağlantı hattı için bir, iki veya üç eşlemenin tamamını (Azure özel, Azure ortak ve Microsoft) yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-127">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="7b4ca-128">Eşlemeleri seçtiğiniz herhangi bir sırayla yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-128">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="7b4ca-129">Ancak, her eşlemenin yapılandırmasını birer birer tamamladığınızdan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-129">However, you must make sure that you complete the configuration of each peering one at a time.</span></span> 

## <a name="azure-private-peering"></a><span data-ttu-id="7b4ca-130">Azure özel eşlemesi</span><span class="sxs-lookup"><span data-stu-id="7b4ca-130">Azure private peering</span></span>

<span data-ttu-id="7b4ca-131">Bu bölümde, oluşturma, alma, güncelleştirme ve bir expressroute bağlantı hattı için Azure özel eşleme yapılandırmasını silme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-131">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="7b4ca-132">Azure özel eşlemesi oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="7b4ca-132">To create Azure private peering</span></span>

1. <span data-ttu-id="7b4ca-133">ExpressRoute için PowerShell modülünü içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-133">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="7b4ca-134">ExpressRoute cmdlet’lerini kullanmaya başlamak için [PowerShell Galerisi](http://www.powershellgallery.com/)’nden en yeni PowerShell yükleyicisini yüklemeniz ve Azure Resource Manager modüllerini PowerShell oturumuna aktarmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-134">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="7b4ca-135">PowerShell'i Yönetici olarak çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-135">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  <span data-ttu-id="7b4ca-136">Tüm bilinen semantik sürüm aralığı içinde AzureRM.* modüllerini içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-136">Import all of the AzureRM.* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="7b4ca-137">Aynı zamanda yalnızca bilinen semantik sürüm aralığı içinde seçili bir modülü içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-137">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network 
  ```

  <span data-ttu-id="7b4ca-138">Hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-138">Sign in to your account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="7b4ca-139">Expressroute bağlantı hattı oluşturmak istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-139">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="7b4ca-140">ExpressRoute bağlantı hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-140">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="7b4ca-141">Bir [ExpressRoute bağlantı hattı](expressroute-howto-circuit-arm.md) oluşturmak için yönergeleri izleyin ve bağlantı sağlayıcısından bağlantı hattını sağlamasını isteyin.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-141">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="7b4ca-142">Bağlantı sağlayıcınız yönetilen Katman 3 hizmetleri sunuyorsa, bağlantı sağlayıcınızdan sizin için Azure özel eşlemeyi etkinleştirmesini isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-142">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="7b4ca-143">Bu durumda, sonraki bölümlerde listelenen yönergeleri izlemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-143">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="7b4ca-144">Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için hattınızı oluşturduktan sonra yönetmiyorsa yapılandırmanızı sonraki adımlarla devam edin.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-144">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="7b4ca-145">Sağlanan ve ayrıca etkin emin olmak için expressroute bağlantı hattı denetleyin.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-145">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="7b4ca-146">Şu örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="7b4ca-146">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="7b4ca-147">Yanıt aşağıdaki örneğe benzer:</span><span class="sxs-lookup"><span data-stu-id="7b4ca-147">The response is similar to the following example:</span></span>

  ```
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
  ```
4. <span data-ttu-id="7b4ca-148">Bağlantı hattı için Azure özel eşlemesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-148">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="7b4ca-149">Sonraki adımlara devam etmeden önce aşağıdaki öğelerin bulunduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="7b4ca-149">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="7b4ca-150">Birincil bağlantı için bir /30 alt ağı.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-150">A /30 subnet for the primary link.</span></span> <span data-ttu-id="7b4ca-151">Alt ağ, sanal ağlar için ayrılmış herhangi bir adres alanının parçası olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-151">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="7b4ca-152">İkincil bağlantı için bir /30 alt ağı.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-152">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="7b4ca-153">Alt ağ, sanal ağlar için ayrılmış herhangi bir adres alanının parçası olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-153">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="7b4ca-154">Bu eşlemenin kurulacağı geçerli bir VLAN kimliği.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-154">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="7b4ca-155">Bağlantı hattındaki başka bir eşlemenin aynı VLAN kimliğini kullanmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-155">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="7b4ca-156">Eşleme için AS numarası.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-156">AS number for peering.</span></span> <span data-ttu-id="7b4ca-157">2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-157">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="7b4ca-158">Bu eşleme için özel bir AS numarası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-158">You can use a private AS number for this peering.</span></span> <span data-ttu-id="7b4ca-159">65515’i kullanmadığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-159">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="7b4ca-160">**İsteğe bağlı -** kullanmayı seçerseniz bir MD5 karma değeri.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-160">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="7b4ca-161">Bağlantı hattınız için Azure özel eşlemesini yapılandırmak için aşağıdaki örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="7b4ca-161">Use the following example to configure Azure private peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="7b4ca-162">Bir MD5 karma değeri kullanmayı seçerseniz, aşağıdaki örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="7b4ca-162">If you choose to use an MD5 hash, use the following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="7b4ca-163">AS numaranızı müşteri ASN’si değil eşleme ASN’si olarak belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-163">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="7b4ca-164">Azure özel eşleme ayrıntılarını görüntülemek için</span><span class="sxs-lookup"><span data-stu-id="7b4ca-164">To view Azure private peering details</span></span>

<span data-ttu-id="7b4ca-165">Aşağıdaki örnek kullanarak yapılandırma ayrıntılarını alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7b4ca-165">You can get configuration details by using the following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="7b4ca-166">Azure özel eşleme yapılandırmasını güncelleştirmek için</span><span class="sxs-lookup"><span data-stu-id="7b4ca-166">To update Azure private peering configuration</span></span>

<span data-ttu-id="7b4ca-167">Aşağıdaki örnek kullanarak yapılandırmanın herhangi bir bölümünü güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-167">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="7b4ca-168">Bu örnekte, bağlantı hattının VLAN kimliği 100'den 500'e güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-168">In this example, the VLAN ID of the circuit is being updated from 100 to 500.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="7b4ca-169">Azure özel eşlemeyi silmek için</span><span class="sxs-lookup"><span data-stu-id="7b4ca-169">To delete Azure private peering</span></span>

<span data-ttu-id="7b4ca-170">Aşağıdaki örnek çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7b4ca-170">You can remove your peering configuration by running the following example:</span></span>

> [!WARNING]
> <span data-ttu-id="7b4ca-171">Bu örneği çalıştırmadan önce tüm sanal ağları expressroute bağlantı hattı bağlantısız olduğundan emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-171">You must ensure that all virtual networks are unlinked from the ExpressRoute circuit before running this example.</span></span> 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a><span data-ttu-id="7b4ca-172">Azure ortak eşleme</span><span class="sxs-lookup"><span data-stu-id="7b4ca-172">Azure public peering</span></span>

<span data-ttu-id="7b4ca-173">Bu bölümde, oluşturma, alma, güncelleştirme ve bir expressroute bağlantı hattı için Azure ortak eşleme yapılandırmasını silme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-173">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="7b4ca-174">Azure ortak eşlemesi oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="7b4ca-174">To create Azure public peering</span></span>

1. <span data-ttu-id="7b4ca-175">ExpressRoute için PowerShell modülünü içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-175">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="7b4ca-176">ExpressRoute cmdlet’lerini kullanmaya başlamak için [PowerShell Galerisi](http://www.powershellgallery.com/)’nden en yeni PowerShell yükleyicisini yüklemeniz ve Azure Resource Manager modüllerini PowerShell oturumuna aktarmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-176">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="7b4ca-177">PowerShell'i Yönetici olarak çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-177">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  <span data-ttu-id="7b4ca-178">Tüm bilinen semantik sürüm aralığı içinde AzureRM.* modüllerini içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-178">Import all of the AzureRM.* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="7b4ca-179">Aynı zamanda yalnızca bilinen semantik sürüm aralığı içinde seçili bir modülü içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-179">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
```

  <span data-ttu-id="7b4ca-180">Hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-180">Sign in to your account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="7b4ca-181">Expressroute bağlantı hattı oluşturmak istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-181">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="7b4ca-182">ExpressRoute bağlantı hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-182">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="7b4ca-183">Bir [ExpressRoute bağlantı hattı](expressroute-howto-circuit-arm.md) oluşturmak için yönergeleri izleyin ve bağlantı sağlayıcısından bağlantı hattını sağlamasını isteyin.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-183">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="7b4ca-184">Bağlantı sağlayıcınız yönetilen Katman 3 hizmetleri sunuyorsa, bağlantı sağlayıcınızdan sizin için Azure özel eşlemeyi etkinleştirmesini isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="7b4ca-185">Bu durumda, sonraki bölümlerde listelenen yönergeleri izlemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-185">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="7b4ca-186">Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için hattınızı oluşturduktan sonra yönetmiyorsa yapılandırmanızı sonraki adımlarla devam edin.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="7b4ca-187">Sağlanan ve ayrıca etkin emin olmak için expressroute bağlantı hattı denetleyin.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-187">Check the ExpressRoute circuit to ensure it is provisioned and also enabled.</span></span> <span data-ttu-id="7b4ca-188">Şu örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="7b4ca-188">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="7b4ca-189">Yanıt aşağıdaki örneğe benzer:</span><span class="sxs-lookup"><span data-stu-id="7b4ca-189">The response is similar to the following example:</span></span>

  ```
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
  ```
4. <span data-ttu-id="7b4ca-190">Bağlantı hattı için Azure ortak eşlemesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-190">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="7b4ca-191">Devam etmeden önce aşağıdaki bilgilere sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-191">Make sure that you have the following information before you proceed further.</span></span>

  * <span data-ttu-id="7b4ca-192">Birincil bağlantı için bir /30 alt ağı.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-192">A /30 subnet for the primary link.</span></span> <span data-ttu-id="7b4ca-193">Bu geçerli bir ortak IPv4 öneki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-193">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="7b4ca-194">İkincil bağlantı için bir /30 alt ağı.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-194">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="7b4ca-195">Bu geçerli bir ortak IPv4 öneki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-195">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="7b4ca-196">Bu eşlemenin kurulacak geçerli bir VLAN kimliği.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-196">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="7b4ca-197">Bağlantı hattındaki başka bir eşlemenin aynı VLAN kimliğini kullanmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-197">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="7b4ca-198">Eşleme için AS numarası.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-198">AS number for peering.</span></span> <span data-ttu-id="7b4ca-199">2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-199">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="7b4ca-200">**İsteğe bağlı -** kullanmayı seçerseniz bir MD5 karma değeri.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-200">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="7b4ca-201">Bağlantı hattınız için Azure ortak eşlemesini yapılandırmak için aşağıdaki örneği çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7b4ca-201">Run the following example to configure Azure public peering for your circuit</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="7b4ca-202">Bir MD5 karma değeri kullanmayı seçerseniz, aşağıdaki örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="7b4ca-202">If you choose to use an MD5 hash, use the following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="7b4ca-203">AS numaranızı müşteri ASN’si değil eşleme ASN’si olarak belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-203">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="7b4ca-204">Azure ortak eşleme ayrıntılarını görüntülemek için</span><span class="sxs-lookup"><span data-stu-id="7b4ca-204">To view Azure public peering details</span></span>

<span data-ttu-id="7b4ca-205">Aşağıdaki cmdlet'i kullanarak yapılandırma ayrıntılarını alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7b4ca-205">You can get configuration details using the following cmdlet:</span></span>

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="7b4ca-206">Azure ortak eşleme yapılandırmasını güncelleştirmek için</span><span class="sxs-lookup"><span data-stu-id="7b4ca-206">To update Azure public peering configuration</span></span>

<span data-ttu-id="7b4ca-207">Aşağıdaki örnek kullanarak yapılandırmanın herhangi bir bölümünü güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-207">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="7b4ca-208">Bu örnekte, bağlantı hattının VLAN kimliği 200'den 600 olarak güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-208">In this example, the VLAN ID of the circuit is being updated from 200 to 600.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="7b4ca-209">Azure ortak eşlemesini silmek için</span><span class="sxs-lookup"><span data-stu-id="7b4ca-209">To delete Azure public peering</span></span>

<span data-ttu-id="7b4ca-210">Aşağıdaki örnek çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7b4ca-210">You can remove your peering configuration by running the following example:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a><span data-ttu-id="7b4ca-211">Microsoft eşlemesi</span><span class="sxs-lookup"><span data-stu-id="7b4ca-211">Microsoft peering</span></span>

<span data-ttu-id="7b4ca-212">Bu bölümde, oluşturma, alma, güncelleştirme ve bir expressroute bağlantı hattı için Microsoft eşleme yapılandırmasını silme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-212">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b4ca-213">1 Ağustos 2017 önce yapılandırılmış olan ExpressRoute bağlantı hatları, Microsoft eşlemesi yol filtreleri tanımlanmamış olsa bile eşleme, Microsoft tarafından tanıtılan tüm hizmet ön eklerin sahip olur.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-213">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through the Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="7b4ca-214">Ve 1 Ağustos 2017 sonrasında yapılandırılmış ExpressRoute bağlantı hatları, Microsoft eşlemesi sahip olmaz tüm ön eklerin rota filtre devresine bağlanana kadar tanıtılan.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-214">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span> <span data-ttu-id="7b4ca-215">Daha fazla bilgi için bkz: [Microsoft eşliği için rota filtresini Yapılandır](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7b4ca-215">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="7b4ca-216">Microsoft eşlemesi oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="7b4ca-216">To create Microsoft peering</span></span>

1. <span data-ttu-id="7b4ca-217">ExpressRoute için PowerShell modülünü içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-217">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="7b4ca-218">ExpressRoute cmdlet’lerini kullanmaya başlamak için [PowerShell Galerisi](http://www.powershellgallery.com/)’nden en yeni PowerShell yükleyicisini yüklemeniz ve Azure Resource Manager modüllerini PowerShell oturumuna aktarmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-218">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="7b4ca-219">PowerShell'i Yönetici olarak çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-219">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  <span data-ttu-id="7b4ca-220">Tüm bilinen semantik sürüm aralığı içinde AzureRM.* modüllerini içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-220">Import all of the AzureRM.* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="7b4ca-221">Aynı zamanda yalnızca bilinen semantik sürüm aralığı içinde seçili bir modülü içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-221">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
  ```

  <span data-ttu-id="7b4ca-222">Hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-222">Sign in to your account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="7b4ca-223">Expressroute bağlantı hattı oluşturmak istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-223">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="7b4ca-224">ExpressRoute bağlantı hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-224">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="7b4ca-225">Bir [ExpressRoute bağlantı hattı](expressroute-howto-circuit-arm.md) oluşturmak için yönergeleri izleyin ve bağlantı sağlayıcısından bağlantı hattını sağlamasını isteyin.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-225">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="7b4ca-226">Bağlantı sağlayıcınız yönetilen Katman 3 hizmetleri sunuyorsa, bağlantı sağlayıcınızdan sizin için Azure özel eşlemeyi etkinleştirmesini isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-226">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="7b4ca-227">Bu durumda, sonraki bölümlerde listelenen yönergeleri izlemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-227">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="7b4ca-228">Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için hattınızı oluşturduktan sonra yönetmiyorsa yapılandırmanızı sonraki adımlarla devam edin.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-228">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="7b4ca-229">Sağlanan ve ayrıca etkin emin olmak için expressroute bağlantı hattı denetleyin.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-229">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="7b4ca-230">Şu örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="7b4ca-230">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="7b4ca-231">Yanıt aşağıdaki örneğe benzer:</span><span class="sxs-lookup"><span data-stu-id="7b4ca-231">The response is similar to the following example:</span></span>

  ```
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
  ```
4. <span data-ttu-id="7b4ca-232">Bağlantı hattı için Microsoft eşlemesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-232">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="7b4ca-233">Devam etmeden önce aşağıdaki bilgilere sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-233">Make sure that you have the following information before you proceed.</span></span>

  * <span data-ttu-id="7b4ca-234">Birincil bağlantı için bir /30 alt ağı.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-234">A /30 subnet for the primary link.</span></span> <span data-ttu-id="7b4ca-235">Bu size ait ve bir RIR / IRR içinde kayıtlı bir geçerli ortak IPv4 ön eki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-235">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="7b4ca-236">İkincil bağlantı için bir /30 alt ağı.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-236">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="7b4ca-237">Bu size ait ve bir RIR / IRR içinde kayıtlı bir geçerli ortak IPv4 ön eki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-237">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="7b4ca-238">Bu eşlemenin kurulacağı geçerli bir VLAN kimliği.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-238">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="7b4ca-239">Bağlantı hattındaki başka bir eşlemenin aynı VLAN kimliğini kullanmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-239">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="7b4ca-240">Eşleme için AS numarası.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-240">AS number for peering.</span></span> <span data-ttu-id="7b4ca-241">2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-241">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="7b4ca-242">Tanıtılan önekler: BGP oturumunda tanıtmayı planladığınız tüm öneklerin bir listesini sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-242">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="7b4ca-243">Yalnızca ortak IP adresi ön ekleri kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-243">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="7b4ca-244">Bir ön ek kümesi göndermeyi planlıyorsanız, virgülle ayrılmış bir liste gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-244">If you plan to send a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="7b4ca-245">Bu ön ekler size bir RIR / IRR içinde kaydedilmiş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-245">These prefixes must be registered to you in an RIR / IRR.</span></span>
  * <span data-ttu-id="7b4ca-246">**İsteğe bağlı -** müşteri ASN'si: eşleme AS numarasına kayıtlı olmayan önekler Tanıtıyorsanız, kayıtlı oldukları AS numarasını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-246">**Optional -** Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span>
  * <span data-ttu-id="7b4ca-247">Yönlendirme Kayıt Defteri Adı: AS numarası ve öneklerinin kaydedildiği RIR / IRR’yi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-247">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="7b4ca-248">**İsteğe bağlı -** kullanmayı seçerseniz bir MD5 karma değeri.</span><span class="sxs-lookup"><span data-stu-id="7b4ca-248">**Optional -** An MD5 hash if you choose to use one.</span></span>

   <span data-ttu-id="7b4ca-249">Microsoft bağlantı hattınız için eşlemesini yapılandırmak için aşağıdaki örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="7b4ca-249">Use the following example to configure Microsoft peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="to-get-microsoft-peering-details"></a><span data-ttu-id="7b4ca-250">Microsoft eşlemesi ayrıntılarını almak için</span><span class="sxs-lookup"><span data-stu-id="7b4ca-250">To get Microsoft peering details</span></span>

<span data-ttu-id="7b4ca-251">Aşağıdaki örnek kullanarak yapılandırma ayrıntılarını alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7b4ca-251">You can get configuration details using the following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="7b4ca-252">Microsoft eşlemesi yapılandırmasını güncelleştirmek için</span><span class="sxs-lookup"><span data-stu-id="7b4ca-252">To update Microsoft peering configuration</span></span>

<span data-ttu-id="7b4ca-253">Aşağıdaki örnek kullanarak yapılandırmanın herhangi bir bölümünü güncelleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7b4ca-253">You can update any part of the configuration using the following example:</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="7b4ca-254">Microsoft eşlemesini silmek için</span><span class="sxs-lookup"><span data-stu-id="7b4ca-254">To delete Microsoft peering</span></span>

<span data-ttu-id="7b4ca-255">Aşağıdaki cmdlet'i çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7b4ca-255">You can remove your peering configuration by running the following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a><span data-ttu-id="7b4ca-256">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7b4ca-256">Next steps</span></span>

<span data-ttu-id="7b4ca-257">Sonraki adım, [ExpressRoute bağlantı hattına bir VNet bağlama](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="7b4ca-257">Next step, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

* <span data-ttu-id="7b4ca-258">ExpressRoute iş akışları hakkında daha fazla bilgi için bkz. [ExpressRoute iş akışları](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="7b4ca-258">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="7b4ca-259">Bağlantı hattı eşlemesi hakkında daha fazla bilgi için bkz. [ExpressRoute bağlantı hattı ve yönlendirme etki alanları](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="7b4ca-259">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="7b4ca-260">Sanal ağlarla çalışma hakkında daha fazla bilgi için bkz. [Sanal ağa genel bakış](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7b4ca-260">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
