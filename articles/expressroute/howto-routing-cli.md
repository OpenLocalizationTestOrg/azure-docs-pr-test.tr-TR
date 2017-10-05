---
title: "Bir Azure expressroute bağlantı hattı için yönlendirmeyi yapılandırma: CLI | Microsoft Docs"
description: "Bu makalede, oluşturma ve özel, genel ve Microsoft eşlemesi bir expressroute bağlantı hattı sağlama yardımcı olur. Bu makalede ayrıca bağlantı hattınızın durumunu denetleme, bağlantı hattını güncelleştirme veya silme işlemlerinin nasıl yapıldığı da anlatılmaktadır."
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
ms.date: 07/31/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: fbf0bd9a139c22bbd63755f6df445f6596aaccc5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a><span data-ttu-id="aba06-104">Oluşturma ve CLI kullanarak bir expressroute bağlantı hattı için yönlendirmeyi değiştirme</span><span class="sxs-lookup"><span data-stu-id="aba06-104">Create and modify routing for an ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="aba06-105">Bu makale, CLI kullanarak Resource Manager dağıtım modelinde bir expressroute bağlantı hattı için yönlendirme yapılandırması oluşturma ve yönetme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="aba06-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using CLI.</span></span> <span data-ttu-id="aba06-106">Ayrıca, durumu, güncelleştirme veya silme denetleyin ve bir expressroute bağlantı hattı için eşlemeler sağlamayı sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="aba06-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="aba06-107">Bağlantı hattınız ile çalışmak için farklı bir yöntem kullanmak istiyorsanız, bir makale aşağıdaki listeden seçin:</span><span class="sxs-lookup"><span data-stu-id="aba06-107">If you want to use a different method to work with your circuit, select an article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="aba06-108">Azure portal</span><span class="sxs-lookup"><span data-stu-id="aba06-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="aba06-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aba06-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="aba06-110">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="aba06-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="aba06-111">Video - özel eşliği</span><span class="sxs-lookup"><span data-stu-id="aba06-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="aba06-112">Video - ortak eşleme</span><span class="sxs-lookup"><span data-stu-id="aba06-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="aba06-113">Video - Microsoft eşlemesi</span><span class="sxs-lookup"><span data-stu-id="aba06-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="aba06-114">PowerShell (klasik)</span><span class="sxs-lookup"><span data-stu-id="aba06-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="aba06-115">Yapılandırma önkoşulları</span><span class="sxs-lookup"><span data-stu-id="aba06-115">Configuration prerequisites</span></span>

* <span data-ttu-id="aba06-116">Başlamadan önce, CLI komutlarının en son sürümünü (2.0 veya üzeri) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="aba06-116">Before beginning, install the latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="aba06-117">CLI komutlarını yükleme hakkında bilgi için bkz. [Azure CLI 2.0’ı yükleme](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="aba06-117">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="aba06-118">Gözden geçirdiğinizden emin olun [Önkoşullar](expressroute-prerequisites.md), [yönlendirme gereksinimleri](expressroute-routing.md), ve [iş akışı](expressroute-workflows.md) yapılandırmaya başlamadan önce sayfaları.</span><span class="sxs-lookup"><span data-stu-id="aba06-118">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflow](expressroute-workflows.md) pages before you begin configuration.</span></span>
* <span data-ttu-id="aba06-119">Etkin bir ExpressRoute bağlantı hattınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="aba06-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="aba06-120">Devam etmeden önce [ExpressRoute bağlantı hattı oluşturma](howto-circuit-cli.md) yönergelerini izleyin ve bağlantı sağlayıcınızın bağlantı hattını etkinleştirmesini isteyin.</span><span class="sxs-lookup"><span data-stu-id="aba06-120">Follow the instructions to [Create an ExpressRoute circuit](howto-circuit-cli.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="aba06-121">Expressroute bağlantı hattı, bu makaledeki komutları çalıştırılabilmesi sağlanmış ve etkin durumda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="aba06-121">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the commands in this article.</span></span>

<span data-ttu-id="aba06-122">Bu yönergeler yalnızca Katman 2 bağlantı hizmetleri sunan hizmet sağlayıcıları ile oluşturulan bağlantı hatları için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="aba06-122">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="aba06-123">Yönetilen sunan bir hizmet sağlayıcısı kullanıyorsanız, Katman 3 Hizmetleri (genellikle gibi bir IPVPN MPLS), bağlantı sağlayıcınız yapılandırmak ve yönetmek için yönlendirme.</span><span class="sxs-lookup"><span data-stu-id="aba06-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

<span data-ttu-id="aba06-124">Bir, iki veya üç eşlemenin tamamını (Azure özel, Azure genel ve Microsoft) bir expressroute bağlantı hattı için yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aba06-124">You can configure one, two, or all three peerings (Azure private, Azure public, and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="aba06-125">Eşlemeleri seçtiğiniz herhangi bir sırayla yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aba06-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="aba06-126">Ancak, her eşlemenin yapılandırmasını birer birer tamamladığınızdan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="aba06-126">However, you must make sure that you complete the configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="aba06-127">Azure özel eşlemesi</span><span class="sxs-lookup"><span data-stu-id="aba06-127">Azure private peering</span></span>

<span data-ttu-id="aba06-128">Bu bölümde, oluşturma, alma, güncelleştirme ve bir expressroute bağlantı hattı için Azure özel eşleme yapılandırmasını silme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="aba06-128">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="aba06-129">Azure özel eşlemesi oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="aba06-129">To create Azure private peering</span></span>

1. <span data-ttu-id="aba06-130">Azure CLI'ın en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="aba06-130">Install the latest version of Azure CLI.</span></span> <span data-ttu-id="aba06-131">En son sürümü, Azure komut satırı arabirimi (CLI) kullanmanız gerekir. * gözden geçirme [Önkoşullar](expressroute-prerequisites.md) ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="aba06-131">You must use the latest version of the Azure Command-line Interface (CLI).* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="aba06-132">ExpressRoute bağlantı hattı oluşturmak istediğiniz aboneliği seçin</span><span class="sxs-lookup"><span data-stu-id="aba06-132">Select the subscription you want to create ExpressRoute circuit</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="aba06-133">ExpressRoute bağlantı hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="aba06-133">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="aba06-134">Bir [ExpressRoute bağlantı hattı](howto-circuit-cli.md) oluşturmak için yönergeleri izleyin ve bağlantı sağlayıcısından bağlantı hattını sağlamasını isteyin.</span><span class="sxs-lookup"><span data-stu-id="aba06-134">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="aba06-135">Bağlantı sağlayıcınız yönetilen Katman 3 hizmetleri sunuyorsa, bağlantı sağlayıcınızdan sizin için Azure özel eşlemeyi etkinleştirmesini isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aba06-135">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="aba06-136">Bu durumda, sonraki bölümlerde listelenen yönergeleri izlemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="aba06-136">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="aba06-137">Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için hattınızı oluşturduktan sonra yönetmiyorsa yapılandırmanızı sonraki adımlarla devam edin.</span><span class="sxs-lookup"><span data-stu-id="aba06-137">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="aba06-138">Sağlanan ve ayrıca etkin emin olmak için expressroute bağlantı hattı denetleyin.</span><span class="sxs-lookup"><span data-stu-id="aba06-138">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="aba06-139">Şu örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="aba06-139">Use the following example:</span></span>

  ```azurecli
  az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
  ```

  <span data-ttu-id="aba06-140">Yanıt aşağıdaki örneğe benzer:</span><span class="sxs-lookup"><span data-stu-id="aba06-140">The response is similar to the following example:</span></span>

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="aba06-141">Bağlantı hattı için Azure özel eşlemesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="aba06-141">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="aba06-142">Sonraki adımlara devam etmeden önce aşağıdaki öğelerin bulunduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="aba06-142">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="aba06-143">Birincil bağlantı için bir /30 alt ağı.</span><span class="sxs-lookup"><span data-stu-id="aba06-143">A /30 subnet for the primary link.</span></span> <span data-ttu-id="aba06-144">Alt ağ, sanal ağlar için ayrılmış herhangi bir adres alanının parçası olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="aba06-144">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="aba06-145">İkincil bağlantı için bir /30 alt ağı.</span><span class="sxs-lookup"><span data-stu-id="aba06-145">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="aba06-146">Alt ağ, sanal ağlar için ayrılmış herhangi bir adres alanının parçası olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="aba06-146">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="aba06-147">Bu eşlemenin kurulacağı geçerli bir VLAN kimliği.</span><span class="sxs-lookup"><span data-stu-id="aba06-147">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="aba06-148">Bağlantı hattındaki başka bir eşlemenin aynı VLAN kimliğini kullanmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="aba06-148">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="aba06-149">Eşleme için AS numarası.</span><span class="sxs-lookup"><span data-stu-id="aba06-149">AS number for peering.</span></span> <span data-ttu-id="aba06-150">2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aba06-150">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="aba06-151">Bu eşleme için özel bir AS numarası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aba06-151">You can use a private AS number for this peering.</span></span> <span data-ttu-id="aba06-152">65515’i kullanmadığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="aba06-152">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="aba06-153">**İsteğe bağlı -** kullanmayı seçerseniz bir MD5 karma değeri.</span><span class="sxs-lookup"><span data-stu-id="aba06-153">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="aba06-154">Bağlantı hattınız için Azure özel eşlemesini yapılandırmak için aşağıdaki örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="aba06-154">Use the following example to configure Azure private peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  <span data-ttu-id="aba06-155">Bir MD5 karma değeri kullanmayı seçerseniz, aşağıdaki örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="aba06-155">If you choose to use an MD5 hash, use the following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="aba06-156">AS numaranızı müşteri ASN’si değil eşleme ASN’si olarak belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="aba06-156">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  > 

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="aba06-157">Azure özel eşleme ayrıntılarını görüntülemek için</span><span class="sxs-lookup"><span data-stu-id="aba06-157">To view Azure private peering details</span></span>

<span data-ttu-id="aba06-158">Aşağıdaki örnek kullanarak yapılandırma ayrıntılarını alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="aba06-158">You can get configuration details by using the following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

<span data-ttu-id="aba06-159">Çıktı aşağıdaki örneğe benzer:</span><span class="sxs-lookup"><span data-stu-id="aba06-159">The output is similar to the following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePrivatePeering",
  "ipv6PeeringConfig": null,
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePrivatePeering",
  "peerAsn": 7671,
  "peeringType": "AzurePrivatePeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="aba06-160">Azure özel eşleme yapılandırmasını güncelleştirmek için</span><span class="sxs-lookup"><span data-stu-id="aba06-160">To update Azure private peering configuration</span></span>

<span data-ttu-id="aba06-161">Aşağıdaki örnek kullanarak yapılandırmanın herhangi bir bölümünü güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aba06-161">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="aba06-162">Bu örnekte, bağlantı hattının VLAN kimliği 100'den 500'e güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="aba06-162">In this example, the VLAN ID of the circuit is being updated from 100 to 500.</span></span>

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="aba06-163">Azure özel eşlemeyi silmek için</span><span class="sxs-lookup"><span data-stu-id="aba06-163">To delete Azure private peering</span></span>

<span data-ttu-id="aba06-164">Aşağıdaki örnek çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="aba06-164">You can remove your peering configuration by running the following example:</span></span>

> [!WARNING]
> <span data-ttu-id="aba06-165">Bu örneği çalıştırmadan önce tüm sanal ağları expressroute bağlantı hattı bağlantısız olduğundan emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="aba06-165">You must ensure that all virtual networks are unlinked from the ExpressRoute circuit before running this example.</span></span> 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a><span data-ttu-id="aba06-166">Azure ortak eşleme</span><span class="sxs-lookup"><span data-stu-id="aba06-166">Azure public peering</span></span>

<span data-ttu-id="aba06-167">Bu bölümde, oluşturma, alma, güncelleştirme ve bir expressroute bağlantı hattı için Azure ortak eşleme yapılandırmasını silme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="aba06-167">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="aba06-168">Azure ortak eşlemesi oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="aba06-168">To create Azure public peering</span></span>

1. <span data-ttu-id="aba06-169">Azure CLI'ın en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="aba06-169">Install the latest version of Azure CLI.</span></span> <span data-ttu-id="aba06-170">En son sürümü, Azure komut satırı arabirimi (CLI) kullanmanız gerekir. * gözden geçirme [Önkoşullar](expressroute-prerequisites.md) ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="aba06-170">You must use the latest version of the Azure Command-line Interface (CLI).* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="aba06-171">Expressroute bağlantı hattı oluşturmak istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="aba06-171">Select the subscription for which you want to create ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="aba06-172">ExpressRoute bağlantı hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="aba06-172">Create an ExpressRoute circuit.</span></span>  <span data-ttu-id="aba06-173">Bir [ExpressRoute bağlantı hattı](howto-circuit-cli.md) oluşturmak için yönergeleri izleyin ve bağlantı sağlayıcısından bağlantı hattını sağlamasını isteyin.</span><span class="sxs-lookup"><span data-stu-id="aba06-173">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="aba06-174">Bağlantı sağlayıcınız yönetilen Katman 3 Hizmetleri sunuyorsa, bağlantı sağlayıcınız özel sizin için Azure eşlemeyi sağlar isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="aba06-174">If your connectivity provider offers managed Layer 3 services, you can request that your connectivity provider enables Azure private peering for you.</span></span> <span data-ttu-id="aba06-175">Bu durumda, sonraki bölümlerde listelenen yönergeleri izlemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="aba06-175">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="aba06-176">Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için hattınızı oluşturduktan sonra yönetmiyorsa yapılandırmanızı sonraki adımlarla devam edin.</span><span class="sxs-lookup"><span data-stu-id="aba06-176">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="aba06-177">Sağlanan ve ayrıca etkin emin olmak için expressroute bağlantı hattı denetleyin.</span><span class="sxs-lookup"><span data-stu-id="aba06-177">Check the ExpressRoute circuit to ensure it is provisioned and also enabled.</span></span> <span data-ttu-id="aba06-178">Şu örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="aba06-178">Use the following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="aba06-179">Yanıt aşağıdaki örneğe benzer:</span><span class="sxs-lookup"><span data-stu-id="aba06-179">The response is similar to the following example:</span></span>

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
    "bandwidthInMbps": 200,
    "peeringLocation": "Silicon Valley",
    "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="aba06-180">Bağlantı hattı için Azure ortak eşlemesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="aba06-180">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="aba06-181">Devam etmeden önce aşağıdaki bilgilere sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="aba06-181">Make sure that you have the following information before you proceed further.</span></span>

  * <span data-ttu-id="aba06-182">Birincil bağlantı için bir /30 alt ağı.</span><span class="sxs-lookup"><span data-stu-id="aba06-182">A /30 subnet for the primary link.</span></span> <span data-ttu-id="aba06-183">Bu geçerli bir ortak IPv4 öneki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="aba06-183">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="aba06-184">İkincil bağlantı için bir /30 alt ağı.</span><span class="sxs-lookup"><span data-stu-id="aba06-184">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="aba06-185">Bu geçerli bir ortak IPv4 öneki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="aba06-185">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="aba06-186">Bu eşlemenin kurulacak geçerli bir VLAN kimliği.</span><span class="sxs-lookup"><span data-stu-id="aba06-186">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="aba06-187">Bağlantı hattındaki başka bir eşlemenin aynı VLAN kimliğini kullanmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="aba06-187">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="aba06-188">Eşleme için AS numarası.</span><span class="sxs-lookup"><span data-stu-id="aba06-188">AS number for peering.</span></span> <span data-ttu-id="aba06-189">2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aba06-189">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="aba06-190">**İsteğe bağlı -** kullanmayı seçerseniz bir MD5 karma değeri.</span><span class="sxs-lookup"><span data-stu-id="aba06-190">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="aba06-191">Bağlantı hattınız için Azure ortak eşlemesini yapılandırmak için aşağıdaki örnekte çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="aba06-191">Run the following example to configure Azure public peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  <span data-ttu-id="aba06-192">Bir MD5 karma değeri kullanmayı seçerseniz, aşağıdaki örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="aba06-192">If you choose to use an MD5 hash, use the following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="aba06-193">AS numaranızı müşteri ASN’si değil eşleme ASN’si olarak belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="aba06-193">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="aba06-194">Azure ortak eşleme ayrıntılarını görüntülemek için</span><span class="sxs-lookup"><span data-stu-id="aba06-194">To view Azure public peering details</span></span>

<span data-ttu-id="aba06-195">Aşağıdaki örnek kullanarak yapılandırma ayrıntılarını alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="aba06-195">You can get configuration details using the following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

<span data-ttu-id="aba06-196">Çıktı aşağıdaki örneğe benzer:</span><span class="sxs-lookup"><span data-stu-id="aba06-196">The output is similar to the following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePublicPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePublicPeering",
  "peerAsn": 7671,
  "peeringType": "AzurePublicPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="aba06-197">Azure ortak eşleme yapılandırmasını güncelleştirmek için</span><span class="sxs-lookup"><span data-stu-id="aba06-197">To update Azure public peering configuration</span></span>

<span data-ttu-id="aba06-198">Aşağıdaki örnek kullanarak yapılandırmanın herhangi bir bölümünü güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aba06-198">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="aba06-199">Bu örnekte, bağlantı hattının VLAN kimliği 200'den 600 olarak güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="aba06-199">In this example, the VLAN ID of the circuit is being updated from 200 to 600.</span></span>

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="aba06-200">Azure ortak eşlemesini silmek için</span><span class="sxs-lookup"><span data-stu-id="aba06-200">To delete Azure public peering</span></span>

<span data-ttu-id="aba06-201">Aşağıdaki örnek çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="aba06-201">You can remove your peering configuration by running the following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a><span data-ttu-id="aba06-202">Microsoft eşlemesi</span><span class="sxs-lookup"><span data-stu-id="aba06-202">Microsoft peering</span></span>

<span data-ttu-id="aba06-203">Bu bölümde, oluşturma, alma, güncelleştirme ve bir expressroute bağlantı hattı için Microsoft eşleme yapılandırmasını silme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="aba06-203">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aba06-204">1 Ağustos 2017 önce yapılandırılmış olan ExpressRoute bağlantı hatları, Microsoft eşlemesi yol filtreleri tanımlanmamış olsa bile eşleme, Microsoft tarafından tanıtılan tüm hizmet ön eklerin sahip olur.</span><span class="sxs-lookup"><span data-stu-id="aba06-204">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through the Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="aba06-205">Ve 1 Ağustos 2017 sonrasında yapılandırılmış ExpressRoute bağlantı hatları, Microsoft eşlemesi sahip olmaz tüm ön eklerin rota filtre devresine bağlanana kadar tanıtılan.</span><span class="sxs-lookup"><span data-stu-id="aba06-205">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span> <span data-ttu-id="aba06-206">Daha fazla bilgi için bkz: [Microsoft eşliği için rota filtresini Yapılandır](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="aba06-206">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="aba06-207">Microsoft eşlemesi oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="aba06-207">To create Microsoft peering</span></span>

1. <span data-ttu-id="aba06-208">Azure CLI'ın en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="aba06-208">Install the latest version of Azure CLI.</span></span> <span data-ttu-id="aba06-209">En son sürümü, Azure komut satırı arabirimi (CLI) kullanın. * gözden geçirme [Önkoşullar](expressroute-prerequisites.md) ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="aba06-209">Use the latest version of the Azure Command-line Interface (CLI).* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="aba06-210">Expressroute bağlantı hattı oluşturmak istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="aba06-210">Select the subscription for which you want to create ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="aba06-211">ExpressRoute bağlantı hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="aba06-211">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="aba06-212">Bir [ExpressRoute bağlantı hattı](howto-circuit-cli.md) oluşturmak için yönergeleri izleyin ve bağlantı sağlayıcısından bağlantı hattını sağlamasını isteyin.</span><span class="sxs-lookup"><span data-stu-id="aba06-212">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="aba06-213">Bağlantı sağlayıcınız yönetilen Katman 3 hizmetleri sunuyorsa, bağlantı sağlayıcınızdan sizin için Azure özel eşlemeyi etkinleştirmesini isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aba06-213">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="aba06-214">Bu durumda, sonraki bölümlerde listelenen yönergeleri izlemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="aba06-214">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="aba06-215">Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için hattınızı oluşturduktan sonra yönetmiyorsa yapılandırmanızı sonraki adımlarla devam edin.</span><span class="sxs-lookup"><span data-stu-id="aba06-215">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>

3. <span data-ttu-id="aba06-216">Sağlanan ve ayrıca etkin emin olmak için expressroute bağlantı hattı denetleyin.</span><span class="sxs-lookup"><span data-stu-id="aba06-216">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="aba06-217">Şu örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="aba06-217">Use the following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="aba06-218">Yanıt aşağıdaki örneğe benzer:</span><span class="sxs-lookup"><span data-stu-id="aba06-218">The response is similar to the following example:</span></span>

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
    "bandwidthInMbps": 200,
    "peeringLocation": "Silicon Valley",
    "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="aba06-219">Bağlantı hattı için Microsoft eşlemesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="aba06-219">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="aba06-220">Devam etmeden önce aşağıdaki bilgilere sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="aba06-220">Make sure that you have the following information before you proceed.</span></span>

  * <span data-ttu-id="aba06-221">Birincil bağlantı için bir /30 alt ağı.</span><span class="sxs-lookup"><span data-stu-id="aba06-221">A /30 subnet for the primary link.</span></span> <span data-ttu-id="aba06-222">Bu size ait ve bir RIR / IRR içinde kayıtlı bir geçerli ortak IPv4 ön eki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="aba06-222">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="aba06-223">İkincil bağlantı için bir /30 alt ağı.</span><span class="sxs-lookup"><span data-stu-id="aba06-223">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="aba06-224">Bu size ait ve bir RIR / IRR içinde kayıtlı bir geçerli ortak IPv4 ön eki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="aba06-224">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="aba06-225">Bu eşlemenin kurulacağı geçerli bir VLAN kimliği.</span><span class="sxs-lookup"><span data-stu-id="aba06-225">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="aba06-226">Bağlantı hattındaki başka bir eşlemenin aynı VLAN kimliğini kullanmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="aba06-226">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="aba06-227">Eşleme için AS numarası.</span><span class="sxs-lookup"><span data-stu-id="aba06-227">AS number for peering.</span></span> <span data-ttu-id="aba06-228">2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aba06-228">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="aba06-229">Tanıtılan önekler: BGP oturumunda tanıtmayı planladığınız tüm öneklerin bir listesini sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="aba06-229">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="aba06-230">Yalnızca ortak IP adresi ön ekleri kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="aba06-230">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="aba06-231">Bir ön ek kümesi göndermeyi planlıyorsanız, virgülle ayrılmış bir liste gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aba06-231">If you plan to send a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="aba06-232">Bu ön ekler size bir RIR / IRR içinde kaydedilmiş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="aba06-232">These prefixes must be registered to you in an RIR / IRR.</span></span>
  * <span data-ttu-id="aba06-233">**İsteğe bağlı -** müşteri ASN'si: eşleme AS numarasına kayıtlı olmayan önekler Tanıtıyorsanız, kayıtlı oldukları AS numarasını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aba06-233">**Optional -** Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span>
  * <span data-ttu-id="aba06-234">Yönlendirme Kayıt Defteri Adı: AS numarası ve öneklerinin kaydedildiği RIR / IRR’yi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aba06-234">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="aba06-235">**İsteğe bağlı -** kullanmayı seçerseniz bir MD5 karma değeri.</span><span class="sxs-lookup"><span data-stu-id="aba06-235">**Optional -** An MD5 hash if you choose to use one.</span></span>

   <span data-ttu-id="aba06-236">Microsoft bağlantı hattınız için eşlemesini yapılandırmak için aşağıdaki örnekte çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="aba06-236">Run the following example to configure Microsoft peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="to-get-microsoft-peering-details"></a><span data-ttu-id="aba06-237">Microsoft eşlemesi ayrıntılarını almak için</span><span class="sxs-lookup"><span data-stu-id="aba06-237">To get Microsoft peering details</span></span>

<span data-ttu-id="aba06-238">Aşağıdaki örnek kullanarak yapılandırma ayrıntılarını alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="aba06-238">You can get configuration details by using the following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

<span data-ttu-id="aba06-239">Çıktı aşağıdaki örneğe benzer:</span><span class="sxs-lookup"><span data-stu-id="aba06-239">The output is similar to the following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzureMicrosoftPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": {
    "advertisedPublicPrefixes": [
        ""
      ],
     "advertisedPublicPrefixesState": "",
     "customerASN": ,
     "routingRegistryName": ""
  }
  "name": "AzureMicrosoftPeering",
  "peerAsn": ,
  "peeringType": "AzureMicrosoftPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="aba06-240">Microsoft eşlemesi yapılandırmasını güncelleştirmek için</span><span class="sxs-lookup"><span data-stu-id="aba06-240">To update Microsoft peering configuration</span></span>

<span data-ttu-id="aba06-241">Yapılandırma, herhangi bir bölümünü güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aba06-241">You can update any part of the configuration.</span></span> <span data-ttu-id="aba06-242">Aşağıdaki örnekte 124.1.0.0/24 için bağlantı hattının tanıtılan önekler 123.1.0.0/24 güncelleştirilmekte olan:</span><span class="sxs-lookup"><span data-stu-id="aba06-242">The advertised prefixes of the circuit are being updated from 123.1.0.0/24 to 124.1.0.0/24 in the following example:</span></span>

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="aba06-243">Microsoft eşlemesini silmek için</span><span class="sxs-lookup"><span data-stu-id="aba06-243">To delete Microsoft peering</span></span>

<span data-ttu-id="aba06-244">Aşağıdaki örnek çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="aba06-244">You can remove your peering configuration by running the following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a><span data-ttu-id="aba06-245">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aba06-245">Next steps</span></span>

<span data-ttu-id="aba06-246">Sonraki adım, [ExpressRoute bağlantı hattına bir VNet bağlama](howto-linkvnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="aba06-246">Next step, [Link a VNet to an ExpressRoute circuit](howto-linkvnet-cli.md).</span></span>

* <span data-ttu-id="aba06-247">ExpressRoute iş akışları hakkında daha fazla bilgi için bkz. [ExpressRoute iş akışları](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="aba06-247">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="aba06-248">Bağlantı hattı eşlemesi hakkında daha fazla bilgi için bkz. [ExpressRoute bağlantı hattı ve yönlendirme etki alanları](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="aba06-248">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="aba06-249">Sanal ağlarla çalışma hakkında daha fazla bilgi için bkz. [Sanal ağa genel bakış](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aba06-249">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>