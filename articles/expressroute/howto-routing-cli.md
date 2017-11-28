---
title: "Nasıl tooconfigure bir Azure expressroute bağlantı hattı için yönlendirmeyi: CLI | Microsoft Docs"
description: "Bu makalede, oluşturma ve hello özel, genel ve Microsoft eşleme bir expressroute bağlantı hattı sağlama yardımcı olur. Bu makalede ayrıca nasıl toocheck hello durumu, güncelleştirme veya bağlantı hattınız için eşlemeleri silme gösterilmektedir."
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
ms.openlocfilehash: 33130af050045527cdb316e77821c6d101b6a82a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a><span data-ttu-id="d047e-104">Oluşturma ve CLI kullanarak bir expressroute bağlantı hattı için yönlendirmeyi değiştirme</span><span class="sxs-lookup"><span data-stu-id="d047e-104">Create and modify routing for an ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="d047e-105">Bu makale, CLI kullanarak hello Resource Manager dağıtım modelinde bir expressroute bağlantı hattı için yönlendirme yapılandırması oluşturma ve yönetme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d047e-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using CLI.</span></span> <span data-ttu-id="d047e-106">Ayrıca, hello durumu, güncelleştirme veya silme denetleyin ve bir expressroute bağlantı hattı için eşlemeler sağlamayı sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="d047e-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="d047e-107">Bağlantı hattınız ile toouse farklı yöntem toowork istiyorsanız, bir makale listesi aşağıdaki hello seçin:</span><span class="sxs-lookup"><span data-stu-id="d047e-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d047e-108">Azure portal</span><span class="sxs-lookup"><span data-stu-id="d047e-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="d047e-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d047e-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="d047e-110">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d047e-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="d047e-111">Video - özel eşliği</span><span class="sxs-lookup"><span data-stu-id="d047e-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="d047e-112">Video - ortak eşleme</span><span class="sxs-lookup"><span data-stu-id="d047e-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="d047e-113">Video - Microsoft eşlemesi</span><span class="sxs-lookup"><span data-stu-id="d047e-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="d047e-114">PowerShell (klasik)</span><span class="sxs-lookup"><span data-stu-id="d047e-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="d047e-115">Yapılandırma önkoşulları</span><span class="sxs-lookup"><span data-stu-id="d047e-115">Configuration prerequisites</span></span>

* <span data-ttu-id="d047e-116">Başlamadan önce hello hello CLI komutları (2.0 veya üstü) en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d047e-116">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="d047e-117">Merhaba CLI komutları yükleme hakkında daha fazla bilgi için bkz: [Azure CLI 2.0 yükleme](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d047e-117">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="d047e-118">Merhaba gözden geçirdiğinizden emin olun [Önkoşullar](expressroute-prerequisites.md), [yönlendirme gereksinimleri](expressroute-routing.md), ve [iş akışı](expressroute-workflows.md) yapılandırmaya başlamadan önce sayfaları.</span><span class="sxs-lookup"><span data-stu-id="d047e-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflow](expressroute-workflows.md) pages before you begin configuration.</span></span>
* <span data-ttu-id="d047e-119">Etkin bir ExpressRoute bağlantı hattınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d047e-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="d047e-120">Çok olarak Hello yönergeleri[bir expressroute bağlantı hattı oluşturma](howto-circuit-cli.md) ve devam etmeden önce bağlantı sağlayıcınız tarafından etkinleştirilen hello hattı sahip.</span><span class="sxs-lookup"><span data-stu-id="d047e-120">Follow hello instructions too[Create an ExpressRoute circuit](howto-circuit-cli.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="d047e-121">Merhaba expressroute bağlantı hattı, bu makaledeki toobe mümkün toorun hello komutları için sağlanmış ve etkin durumda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d047e-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello commands in this article.</span></span>

<span data-ttu-id="d047e-122">Bu yönergeler yalnızca Katman 2 bağlantı hizmetleri sunan hizmet sağlayıcıları ile oluşturulan toocircuits geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d047e-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="d047e-123">Yönetilen sunan bir hizmet sağlayıcısı kullanıyorsanız, Katman 3 Hizmetleri (genellikle gibi bir IPVPN MPLS), bağlantı sağlayıcınız yapılandırmak ve yönetmek için yönlendirme.</span><span class="sxs-lookup"><span data-stu-id="d047e-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

<span data-ttu-id="d047e-124">Bir, iki veya üç eşlemenin tamamını (Azure özel, Azure genel ve Microsoft) bir expressroute bağlantı hattı için yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d047e-124">You can configure one, two, or all three peerings (Azure private, Azure public, and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="d047e-125">Eşlemeleri seçtiğiniz herhangi bir sırayla yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d047e-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="d047e-126">Bununla birlikte, her eşleme birer birer başlangıç yapılandırmasını tamamlayın emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d047e-126">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="d047e-127">Azure özel eşlemesi</span><span class="sxs-lookup"><span data-stu-id="d047e-127">Azure private peering</span></span>

<span data-ttu-id="d047e-128">Bu bölümde, oluşturma, alma, güncelleştirme ve hello bir expressroute bağlantı hattı için Azure özel eşleme yapılandırmasını silme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d047e-128">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="d047e-129">Azure özel eşleme toocreate</span><span class="sxs-lookup"><span data-stu-id="d047e-129">toocreate Azure private peering</span></span>

1. <span data-ttu-id="d047e-130">Azure CLI Hello en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d047e-130">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="d047e-131">Merhaba hello Azure komut satırı arabirimi (CLI) en son sürümünü kullanmanız gerekir. * gözden geçirme hello [Önkoşullar](expressroute-prerequisites.md) ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="d047e-131">You must use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="d047e-132">Toocreate expressroute bağlantı hattı hello aboneliği seçin</span><span class="sxs-lookup"><span data-stu-id="d047e-132">Select hello subscription you want toocreate ExpressRoute circuit</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="d047e-133">ExpressRoute bağlantı hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d047e-133">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="d047e-134">Merhaba yönergeleri toocreate izleyin bir [expressroute bağlantı hattı](howto-circuit-cli.md) ve hello bağlantı sağlayıcı tarafından sağlanan sahip.</span><span class="sxs-lookup"><span data-stu-id="d047e-134">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="d047e-135">Bağlantı sağlayıcınız yönetilen Katman 3 Hizmetleri sunuyorsa, bağlantı sağlayıcısı tooenable Azure sizin için eşlemeyi özel isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="d047e-135">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="d047e-136">Bu durumda, hello sonraki bölümlerde listelenen toofollow yönergeleri gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d047e-136">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="d047e-137">Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için hattınızı oluşturduktan sonra yönetmiyorsa yapılandırmanızı hello sonraki adımları kullanarak devam edin.</span><span class="sxs-lookup"><span data-stu-id="d047e-137">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="d047e-138">Merhaba ExpressRoute bağlantı hattı toomake sağlanan ve ayrıca etkin olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d047e-138">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="d047e-139">Aşağıdaki örnek hello kullan:</span><span class="sxs-lookup"><span data-stu-id="d047e-139">Use hello following example:</span></span>

  ```azurecli
  az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
  ```

  <span data-ttu-id="d047e-140">Merhaba yanıt benzer toohello örneği aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="d047e-140">hello response is similar toohello following example:</span></span>

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

4. <span data-ttu-id="d047e-141">Merhaba bağlantı hattı için Azure özel eşlemesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d047e-141">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="d047e-142">Merhaba sonraki adımlara devam etmeden önce aşağıdaki öğelerindeki hello sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="d047e-142">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="d047e-143">Bir/30 alt ağı hello birincil bağlantı için.</span><span class="sxs-lookup"><span data-stu-id="d047e-143">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="d047e-144">Merhaba alt ağ, sanal ağlar için ayrılmış herhangi bir adres alanının parçası olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="d047e-144">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="d047e-145">Bir/30 alt ağı hello ikincil bağlantı için.</span><span class="sxs-lookup"><span data-stu-id="d047e-145">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="d047e-146">Merhaba alt ağ, sanal ağlar için ayrılmış herhangi bir adres alanının parçası olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="d047e-146">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="d047e-147">Geçerli bir VLAN kimliği tooestablish bu eşlemenin.</span><span class="sxs-lookup"><span data-stu-id="d047e-147">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="d047e-148">Hiçbir diğer eşliği emin hello devredeki aynı VLAN kimliğini kullanan hello</span><span class="sxs-lookup"><span data-stu-id="d047e-148">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="d047e-149">Eşleme için AS numarası.</span><span class="sxs-lookup"><span data-stu-id="d047e-149">AS number for peering.</span></span> <span data-ttu-id="d047e-150">2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d047e-150">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="d047e-151">Bu eşleme için özel bir AS numarası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d047e-151">You can use a private AS number for this peering.</span></span> <span data-ttu-id="d047e-152">65515’i kullanmadığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d047e-152">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="d047e-153">**İsteğe bağlı -** toouse birini seçerseniz bir MD5 karma değeri.</span><span class="sxs-lookup"><span data-stu-id="d047e-153">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="d047e-154">Aşağıdaki örnek tooconfigure Azure hattınız için eşlemesini özel hello kullan:</span><span class="sxs-lookup"><span data-stu-id="d047e-154">Use hello following example tooconfigure Azure private peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  <span data-ttu-id="d047e-155">Bir MD5 karma değeri toouse seçerseniz, aşağıdaki örneğine hello kullan:</span><span class="sxs-lookup"><span data-stu-id="d047e-155">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="d047e-156">AS numaranızı müşteri ASN’si değil eşleme ASN’si olarak belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="d047e-156">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  > 

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="d047e-157">tooview Azure özel eşleme ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="d047e-157">tooview Azure private peering details</span></span>

<span data-ttu-id="d047e-158">Aşağıdaki örnek hello kullanarak yapılandırma ayrıntılarını alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d047e-158">You can get configuration details by using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

<span data-ttu-id="d047e-159">Merhaba, benzer toohello aşağıdaki örneğine çıktı:</span><span class="sxs-lookup"><span data-stu-id="d047e-159">hello output is similar toohello following example:</span></span>

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

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="d047e-160">Azure özel eşleme yapılandırmasını tooupdate</span><span class="sxs-lookup"><span data-stu-id="d047e-160">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="d047e-161">Aşağıdaki örneğine hello kullanarak hello yapılandırmasını herhangi bir bölümünü güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d047e-161">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="d047e-162">Bu örnekte, hello hello hattının VLAN kimliği 100 too500 güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="d047e-162">In this example, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="d047e-163">Azure özel eşleme toodelete</span><span class="sxs-lookup"><span data-stu-id="d047e-163">toodelete Azure private peering</span></span>

<span data-ttu-id="d047e-164">Aşağıdaki örnek hello çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d047e-164">You can remove your peering configuration by running hello following example:</span></span>

> [!WARNING]
> <span data-ttu-id="d047e-165">Bu örneği çalıştırmadan önce tüm sanal ağları expressroute bağlantı hattı hello bağlantısız olduğundan emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="d047e-165">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this example.</span></span> 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a><span data-ttu-id="d047e-166">Azure ortak eşleme</span><span class="sxs-lookup"><span data-stu-id="d047e-166">Azure public peering</span></span>

<span data-ttu-id="d047e-167">Bu bölümde, oluşturma, alma, güncelleştirme ve hello bir expressroute bağlantı hattı için Azure ortak eşleme yapılandırmasını silme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d047e-167">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="d047e-168">Azure ortak eşleme toocreate</span><span class="sxs-lookup"><span data-stu-id="d047e-168">toocreate Azure public peering</span></span>

1. <span data-ttu-id="d047e-169">Azure CLI Hello en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d047e-169">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="d047e-170">Merhaba hello Azure komut satırı arabirimi (CLI) en son sürümünü kullanmanız gerekir. * gözden geçirme hello [Önkoşullar](expressroute-prerequisites.md) ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="d047e-170">You must use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="d047e-171">Toocreate expressroute bağlantı hattı istediğiniz hello aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="d047e-171">Select hello subscription for which you want toocreate ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="d047e-172">ExpressRoute bağlantı hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d047e-172">Create an ExpressRoute circuit.</span></span>  <span data-ttu-id="d047e-173">Merhaba yönergeleri toocreate izleyin bir [expressroute bağlantı hattı](howto-circuit-cli.md) ve hello bağlantı sağlayıcı tarafından sağlanan sahip.</span><span class="sxs-lookup"><span data-stu-id="d047e-173">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="d047e-174">Bağlantı sağlayıcınız yönetilen Katman 3 Hizmetleri sunuyorsa, bağlantı sağlayıcınız özel sizin için Azure eşlemeyi sağlar isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="d047e-174">If your connectivity provider offers managed Layer 3 services, you can request that your connectivity provider enables Azure private peering for you.</span></span> <span data-ttu-id="d047e-175">Bu durumda, hello sonraki bölümlerde listelenen toofollow yönergeleri gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d047e-175">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="d047e-176">Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için hattınızı oluşturduktan sonra yönetmiyorsa yapılandırmanızı hello sonraki adımları kullanarak devam edin.</span><span class="sxs-lookup"><span data-stu-id="d047e-176">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="d047e-177">Sağlanan ve ayrıca etkin hello ExpressRoute bağlantı hattı tooensure denetleyin.</span><span class="sxs-lookup"><span data-stu-id="d047e-177">Check hello ExpressRoute circuit tooensure it is provisioned and also enabled.</span></span> <span data-ttu-id="d047e-178">Aşağıdaki örnek hello kullan:</span><span class="sxs-lookup"><span data-stu-id="d047e-178">Use hello following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="d047e-179">Merhaba yanıt benzer toohello örneği aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="d047e-179">hello response is similar toohello following example:</span></span>

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

4. <span data-ttu-id="d047e-180">Merhaba bağlantı hattı için Azure ortak eşlemesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d047e-180">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="d047e-181">Devam etmeden önce aşağıdaki bilgilerle hello sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d047e-181">Make sure that you have hello following information before you proceed further.</span></span>

  * <span data-ttu-id="d047e-182">Bir/30 alt ağı hello birincil bağlantı için.</span><span class="sxs-lookup"><span data-stu-id="d047e-182">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="d047e-183">Bu geçerli bir ortak IPv4 öneki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d047e-183">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="d047e-184">Bir/30 alt ağı hello ikincil bağlantı için.</span><span class="sxs-lookup"><span data-stu-id="d047e-184">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="d047e-185">Bu geçerli bir ortak IPv4 öneki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d047e-185">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="d047e-186">Geçerli bir VLAN kimliği tooestablish bu eşlemenin.</span><span class="sxs-lookup"><span data-stu-id="d047e-186">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="d047e-187">Hiçbir diğer eşliği emin hello devredeki aynı VLAN kimliğini kullanan hello</span><span class="sxs-lookup"><span data-stu-id="d047e-187">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="d047e-188">Eşleme için AS numarası.</span><span class="sxs-lookup"><span data-stu-id="d047e-188">AS number for peering.</span></span> <span data-ttu-id="d047e-189">2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d047e-189">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="d047e-190">**İsteğe bağlı -** toouse birini seçerseniz bir MD5 karma değeri.</span><span class="sxs-lookup"><span data-stu-id="d047e-190">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="d047e-191">Aşağıdaki örnek tooconfigure Azure hattınız için eşlemesini genel hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d047e-191">Run hello following example tooconfigure Azure public peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  <span data-ttu-id="d047e-192">Bir MD5 karma değeri toouse seçerseniz, aşağıdaki örneğine hello kullan:</span><span class="sxs-lookup"><span data-stu-id="d047e-192">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="d047e-193">AS numaranızı müşteri ASN’si değil eşleme ASN’si olarak belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="d047e-193">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="d047e-194">tooview Azure genel eşliği ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="d047e-194">tooview Azure public peering details</span></span>

<span data-ttu-id="d047e-195">Aşağıdaki örnek hello kullanarak yapılandırma ayrıntılarını alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d047e-195">You can get configuration details using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

<span data-ttu-id="d047e-196">Merhaba, benzer toohello aşağıdaki örneğine çıktı:</span><span class="sxs-lookup"><span data-stu-id="d047e-196">hello output is similar toohello following example:</span></span>

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

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="d047e-197">Azure ortak eşleme yapılandırmasını tooupdate</span><span class="sxs-lookup"><span data-stu-id="d047e-197">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="d047e-198">Aşağıdaki örneğine hello kullanarak hello yapılandırmasını herhangi bir bölümünü güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d047e-198">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="d047e-199">Bu örnekte, hello hello hattının VLAN kimliği 200 too600 güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="d047e-199">In this example, hello VLAN ID of hello circuit is being updated from 200 too600.</span></span>

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="d047e-200">Azure ortak eşleme toodelete</span><span class="sxs-lookup"><span data-stu-id="d047e-200">toodelete Azure public peering</span></span>

<span data-ttu-id="d047e-201">Aşağıdaki örnek hello çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d047e-201">You can remove your peering configuration by running hello following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a><span data-ttu-id="d047e-202">Microsoft eşlemesi</span><span class="sxs-lookup"><span data-stu-id="d047e-202">Microsoft peering</span></span>

<span data-ttu-id="d047e-203">Bu bölümde, oluşturma, alma, güncelleştirme ve bir expressroute bağlantı hattı için Microsoft eşleme yapılandırmasını hello silme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d047e-203">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d047e-204">Önceki tooAugust 1 yapılandırılmış olan ExpressRoute bağlantı hatları Microsoft eşliği, yol filtreleri tanımlanmamış olsa bile 2017 hello Microsoft eşleme aracılığıyla tanıtılan tüm hizmet ön eklerin sahip olur.</span><span class="sxs-lookup"><span data-stu-id="d047e-204">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="d047e-205">Ve 1 Ağustos 2017 sonrasında yapılandırılmış ExpressRoute bağlantı hatları, Microsoft eşlemesi sahip olmaz tüm ön eklerin rota filtre bağlanana kadar tanıtılan toohello hattı.</span><span class="sxs-lookup"><span data-stu-id="d047e-205">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="d047e-206">Daha fazla bilgi için bkz: [Microsoft eşliği için rota filtresini Yapılandır](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d047e-206">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="d047e-207">toocreate Microsoft eşlemesi</span><span class="sxs-lookup"><span data-stu-id="d047e-207">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="d047e-208">Azure CLI Hello en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d047e-208">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="d047e-209">Merhaba en son sürümünü kullanın hello Azure komut satırı arabirimi (CLI). * gözden geçirme hello [Önkoşullar](expressroute-prerequisites.md) ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="d047e-209">Use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="d047e-210">Toocreate expressroute bağlantı hattı istediğiniz hello aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="d047e-210">Select hello subscription for which you want toocreate ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="d047e-211">ExpressRoute bağlantı hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d047e-211">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="d047e-212">Merhaba yönergeleri toocreate izleyin bir [expressroute bağlantı hattı](howto-circuit-cli.md) ve hello bağlantı sağlayıcı tarafından sağlanan sahip.</span><span class="sxs-lookup"><span data-stu-id="d047e-212">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="d047e-213">Bağlantı sağlayıcınız yönetilen Katman 3 Hizmetleri sunuyorsa, bağlantı sağlayıcısı tooenable Azure sizin için eşlemeyi özel isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="d047e-213">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="d047e-214">Bu durumda, hello sonraki bölümlerde listelenen toofollow yönergeleri gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d047e-214">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="d047e-215">Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için hattınızı oluşturduktan sonra yönetmiyorsa yapılandırmanızı hello sonraki adımları kullanarak devam edin.</span><span class="sxs-lookup"><span data-stu-id="d047e-215">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>

3. <span data-ttu-id="d047e-216">Merhaba ExpressRoute bağlantı hattı toomake sağlanan ve ayrıca etkin olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d047e-216">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="d047e-217">Aşağıdaki örnek hello kullan:</span><span class="sxs-lookup"><span data-stu-id="d047e-217">Use hello following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="d047e-218">Merhaba yanıt benzer toohello örneği aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="d047e-218">hello response is similar toohello following example:</span></span>

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

4. <span data-ttu-id="d047e-219">Microsoft Hello bağlantı hattı için eşlemesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d047e-219">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="d047e-220">Devam etmeden önce bilgilerini aşağıdaki hello sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d047e-220">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="d047e-221">Bir/30 alt ağı hello birincil bağlantı için.</span><span class="sxs-lookup"><span data-stu-id="d047e-221">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="d047e-222">Bu size ait ve bir RIR / IRR içinde kayıtlı bir geçerli ortak IPv4 ön eki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d047e-222">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="d047e-223">Bir/30 alt ağı hello ikincil bağlantı için.</span><span class="sxs-lookup"><span data-stu-id="d047e-223">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="d047e-224">Bu size ait ve bir RIR / IRR içinde kayıtlı bir geçerli ortak IPv4 ön eki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d047e-224">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="d047e-225">Geçerli bir VLAN kimliği tooestablish bu eşlemenin.</span><span class="sxs-lookup"><span data-stu-id="d047e-225">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="d047e-226">Hiçbir diğer eşliği emin hello devredeki aynı VLAN kimliğini kullanan hello</span><span class="sxs-lookup"><span data-stu-id="d047e-226">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="d047e-227">Eşleme için AS numarası.</span><span class="sxs-lookup"><span data-stu-id="d047e-227">AS number for peering.</span></span> <span data-ttu-id="d047e-228">2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d047e-228">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="d047e-229">Tanıtılan önekler: listesini sağlamanız gerekir tüm ön eklerin hello BGP oturumu üzerinden tooadvertise planlayın.</span><span class="sxs-lookup"><span data-stu-id="d047e-229">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="d047e-230">Yalnızca ortak IP adresi ön ekleri kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="d047e-230">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="d047e-231">Toosend ön ek kümesi planlıyorsanız, virgülle ayrılmış bir liste gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d047e-231">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="d047e-232">Bu ön eklerin bir RIR içinde kayıtlı tooyou olmalıdır / IRR.</span><span class="sxs-lookup"><span data-stu-id="d047e-232">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="d047e-233">**İsteğe bağlı -** müşteri ASN'si: eşleme AS numarasına kayıtlı toohello olmayan önekler Tanıtıyorsanız, kayıtlı oldukları numara toowhich hello belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d047e-233">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="d047e-234">Yönlendirme kayıt defteri adı: Merhaba RIR belirtebilirsiniz / hangi hello karşı AS numarası ve önekleri IRR kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="d047e-234">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="d047e-235">**İsteğe bağlı -** toouse birini seçerseniz bir MD5 karma değeri.</span><span class="sxs-lookup"><span data-stu-id="d047e-235">**Optional -** An MD5 hash if you choose toouse one.</span></span>

   <span data-ttu-id="d047e-236">Aşağıdaki örnek tooconfigure hattınız için Microsoft eşlemesini hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d047e-236">Run hello following example tooconfigure Microsoft peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="tooget-microsoft-peering-details"></a><span data-ttu-id="d047e-237">tooget Microsoft eşleme ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="d047e-237">tooget Microsoft peering details</span></span>

<span data-ttu-id="d047e-238">Aşağıdaki örnek hello kullanarak yapılandırma ayrıntılarını alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d047e-238">You can get configuration details by using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

<span data-ttu-id="d047e-239">Merhaba, benzer toohello aşağıdaki örneğine çıktı:</span><span class="sxs-lookup"><span data-stu-id="d047e-239">hello output is similar toohello following example:</span></span>

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

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="d047e-240">tooupdate Microsoft eşleme yapılandırması</span><span class="sxs-lookup"><span data-stu-id="d047e-240">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="d047e-241">Merhaba yapılandırma herhangi bir bölümünü güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d047e-241">You can update any part of hello configuration.</span></span> <span data-ttu-id="d047e-242">Hello öneklerini hello devrenin aşağıdaki örneğine hello içinde 123.1.0.0/24 too124.1.0.0/24 gelen güncelleştirilmekte olan tanıtılan:</span><span class="sxs-lookup"><span data-stu-id="d047e-242">hello advertised prefixes of hello circuit are being updated from 123.1.0.0/24 too124.1.0.0/24 in hello following example:</span></span>

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="d047e-243">toodelete Microsoft eşlemesi</span><span class="sxs-lookup"><span data-stu-id="d047e-243">toodelete Microsoft peering</span></span>

<span data-ttu-id="d047e-244">Aşağıdaki örnek hello çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d047e-244">You can remove your peering configuration by running hello following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a><span data-ttu-id="d047e-245">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d047e-245">Next steps</span></span>

<span data-ttu-id="d047e-246">Sonraki adım, [VNet tooan expressroute bağlantı hattı bağlantı](howto-linkvnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d047e-246">Next step, [Link a VNet tooan ExpressRoute circuit](howto-linkvnet-cli.md).</span></span>

* <span data-ttu-id="d047e-247">ExpressRoute iş akışları hakkında daha fazla bilgi için bkz. [ExpressRoute iş akışları](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="d047e-247">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="d047e-248">Bağlantı hattı eşlemesi hakkında daha fazla bilgi için bkz. [ExpressRoute bağlantı hattı ve yönlendirme etki alanları](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="d047e-248">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="d047e-249">Sanal ağlarla çalışma hakkında daha fazla bilgi için bkz. [Sanal ağa genel bakış](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d047e-249">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>