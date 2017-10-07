---
title: "Oluşturma ve bir Azure expressroute değiştirme: CLI | Microsoft Docs"
description: "Bu makalede nasıl toocreate, sağlama, doğrulayın, güncelleştirme, silme ve CLI kullanarak bir expressroute bağlantı hattı yetkisini kaldırma açıklanmaktadır."
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
ms.date: 07/25/2017
ms.author: anzaman;cherylmc
ms.openlocfilehash: 396e325658a59afadb209bb525cbb59ac775ae6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-cli"></a><span data-ttu-id="18224-103">Oluşturma ve CLI kullanarak bir expressroute bağlantı hattı değiştirme</span><span class="sxs-lookup"><span data-stu-id="18224-103">Create and modify an ExpressRoute circuit using CLI</span></span>


<span data-ttu-id="18224-104">Bu makalede nasıl toocreate kullanarak bir Azure expressroute bağlantı hattı hello komut satırı arabirimi (CLI) açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="18224-104">This article describes how toocreate an Azure ExpressRoute circuit by using hello Command Line Interface (CLI).</span></span> <span data-ttu-id="18224-105">Bu makalede ayrıca, nasıl toocheck hello durumu, güncelleştirme veya silme ve bir bağlantı hattı yetkisini kaldırma gösterir.</span><span class="sxs-lookup"><span data-stu-id="18224-105">This article also shows you how toocheck hello status, update, or delete and deprovision a circuit.</span></span> <span data-ttu-id="18224-106">Toouse ExpressRoute bağlantı hatları ile farklı yöntem toowork istiyorsanız, liste aşağıdaki hello hello makale seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="18224-106">If you want toouse a different method toowork with ExpressRoute circuits, you can select hello article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="18224-107">Azure portal</span><span class="sxs-lookup"><span data-stu-id="18224-107">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="18224-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="18224-108">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="18224-109">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="18224-109">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="18224-110">Video - Azure portalı</span><span class="sxs-lookup"><span data-stu-id="18224-110">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="18224-111">PowerShell (klasik)</span><span class="sxs-lookup"><span data-stu-id="18224-111">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
> 

## <a name="before-you-begin"></a><span data-ttu-id="18224-112">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="18224-112">Before you begin</span></span>

* <span data-ttu-id="18224-113">Başlamadan önce hello hello CLI komutları (2.0 veya üstü) en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="18224-113">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="18224-114">Merhaba CLI komutları yükleme hakkında daha fazla bilgi için bkz: [Azure CLI 2.0 yükleme](/cli/azure/install-azure-cli) ve [Azure CLI 2.0 ile çalışmaya başlama](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="18224-114">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="18224-115">Gözden geçirme hello [Önkoşullar](expressroute-prerequisites.md) ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="18224-115">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="18224-116">Oluşturma ve bir expressroute bağlantı hattı sağlama</span><span class="sxs-lookup"><span data-stu-id="18224-116">Create and provision an ExpressRoute circuit</span></span>

### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a><span data-ttu-id="18224-117">1. Tooyour Azure hesabı oturum ve aboneliğinizi seçin</span><span class="sxs-lookup"><span data-stu-id="18224-117">1. Sign in tooyour Azure account and select your subscription</span></span>

<span data-ttu-id="18224-118">toobegin yapılandırmanıza, oturum açma tooyour Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="18224-118">toobegin your configuration, sign in tooyour Azure account.</span></span> <span data-ttu-id="18224-119">Bağlandığınız örnekler toohelp aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="18224-119">Use hello following examples toohelp you connect:</span></span>

```azurecli
az login
```

<span data-ttu-id="18224-120">Merhaba hesabının Hello abonelikleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="18224-120">Check hello subscriptions for hello account.</span></span>

```azurecli
az account list
```

<span data-ttu-id="18224-121">Bir expressroute bağlantı hattı toocreate istediğiniz hello aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="18224-121">Select hello subscription for which you want toocreate an ExpressRoute circuit.</span></span>

```azurecli
az account set --subscription "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="18224-122">2. Desteklenen sağlayıcılar, konumları ve bant genişlikleri Hello listesini alma</span><span class="sxs-lookup"><span data-stu-id="18224-122">2. Get hello list of supported providers, locations, and bandwidths</span></span>

<span data-ttu-id="18224-123">Bir expressroute bağlantı hattı oluşturmadan önce desteklenen bağlantı sağlayıcıları, konumları ve bant genişliği seçenekleri hello listesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="18224-123">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span> <span data-ttu-id="18224-124">Merhaba CLI komut 'az ağ hızlı rota listesi-service-providers', sonraki adımlarda kullanacağınız bu bilgiler verir:</span><span class="sxs-lookup"><span data-stu-id="18224-124">hello CLI command 'az network express-route list-service-providers' returns this information, which you’ll use in later steps:</span></span>

```azurecli
az network express-route list-service-providers
```

<span data-ttu-id="18224-125">Merhaba yanıt benzer toohello örneği aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="18224-125">hello response is similar toohello following example:</span></span>

```azurecli
[
  {
    "bandwidthsOffered": [
      {
        "offerName": "50Mbps",
        "valueInMbps": 50
      },
      {
        "offerName": "100Mbps",
        "valueInMbps": 100
      },
      {
        "offerName": "200Mbps",
        "valueInMbps": 200
      },
      {
        "offerName": "500Mbps",
        "valueInMbps": 500
      },
      {
        "offerName": "1Gbps",
        "valueInMbps": 1000
      },
      {
        "offerName": "2Gbps",
        "valueInMbps": 2000
      },
      {
        "offerName": "5Gbps",
        "valueInMbps": 5000
      },
      {
        "offerName": "10Gbps",
        "valueInMbps": 10000
      }
    ],
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/expressRouteServiceProviders/",
    "location": null,
    "name": "AARNet",
    "peeringLocations": [
      "Melbourne",
      "Sydney"
    ],
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "tags": null,
    "type": "Microsoft.Network/expressRouteServiceProviders"
  },
```

<span data-ttu-id="18224-126">Bağlantı sağlayıcınız listeleniyorsa hello yanıt toosee denetleyin.</span><span class="sxs-lookup"><span data-stu-id="18224-126">Check hello response toosee if your connectivity provider is listed.</span></span> <span data-ttu-id="18224-127">Bir bağlantı hattı oluştururken ihtiyacınız olacak bilgileri, aşağıdaki hello not edin:</span><span class="sxs-lookup"><span data-stu-id="18224-127">Make a note of hello following information, which you will need when you create a circuit:</span></span>

* <span data-ttu-id="18224-128">Ad</span><span class="sxs-lookup"><span data-stu-id="18224-128">Name</span></span>
* <span data-ttu-id="18224-129">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="18224-129">PeeringLocations</span></span>
* <span data-ttu-id="18224-130">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="18224-130">BandwidthsOffered</span></span>

<span data-ttu-id="18224-131">Şimdi hazır toocreate bir expressroute bağlantı hattı olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="18224-131">You're now ready toocreate an ExpressRoute circuit.</span></span>

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="18224-132">3. ExpressRoute bağlantı hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="18224-132">3. Create an ExpressRoute circuit</span></span>

> [!IMPORTANT]
> <span data-ttu-id="18224-133">ExpressRoute bağlantı hattınız bir hizmet anahtarı verilen hello andan itibaren faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="18224-133">Your ExpressRoute circuit is billed from hello moment a service key is issued.</span></span> <span data-ttu-id="18224-134">Merhaba bağlantı sağlayıcı hazır tooprovision hello hattı olduğunda bu işlemi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="18224-134">Perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="18224-135">Bir kaynak grubu zaten yoksa, expressroute bağlantı hattı oluşturmadan önce bir oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="18224-135">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="18224-136">Bir kaynak grubu hello aşağıdaki komutu çalıştırarak oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="18224-136">You can create a resource group by running hello following command:</span></span>

```azurecli
az group create -n ExpressRouteResourceGroup -l "West US"
```

<span data-ttu-id="18224-137">Aşağıdaki örnek hello nasıl toocreate 200 MB/sn expressroute bağlantı hattı Silikon vadisi Equinix aracılığıyla gösterir.</span><span class="sxs-lookup"><span data-stu-id="18224-137">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="18224-138">Farklı bir sağlayıcı ve farklı ayarlar kullanıyorsanız, bu bilgileri isteğiniz yaptığınızda değiştirin.</span><span class="sxs-lookup"><span data-stu-id="18224-138">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> 

<span data-ttu-id="18224-139">Merhaba doğru SKU katmanı ve SKU ailesi belirttiğinizden emin olun:</span><span class="sxs-lookup"><span data-stu-id="18224-139">Make sure that you specify hello correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="18224-140">SKU katmanı, bir ExpressRoute standart ya da bir ExpressRoute premium Eklentisi etkin olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="18224-140">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="18224-141">'Standart' tooget Merhaba standart SKU veya 'Premium' hello premium eklenti belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="18224-141">You can specify 'Standard' tooget hello standard SKU or 'Premium' for hello premium add-on.</span></span>
* <span data-ttu-id="18224-142">SKU ailesi hello faturalama türü belirler.</span><span class="sxs-lookup"><span data-stu-id="18224-142">SKU family determines hello billing type.</span></span> <span data-ttu-id="18224-143">Ölçülen veri planı ve 'Unlimiteddata' için 'Metereddata' için bir sınırsız veri planı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="18224-143">You can specify 'Metereddata' for a metered data plan and 'Unlimiteddata' for an unlimited data plan.</span></span> <span data-ttu-id="18224-144">'Metereddata 'too'Unlimiteddata', ancak başlangıç türü 'Unlimiteddata' too'Metereddata değiştirilemez' hello fatura türünü değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="18224-144">You can change hello billing type from 'Metereddata' too'Unlimiteddata', but you can't change hello type from 'Unlimiteddata' too'Metereddata'.</span></span>


<span data-ttu-id="18224-145">ExpressRoute bağlantı hattınız bir hizmet anahtarı verilen hello andan itibaren faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="18224-145">Your ExpressRoute circuit is billed from hello moment a service key is issued.</span></span> <span data-ttu-id="18224-146">Yeni bir hizmet anahtarı için bir istek hello örneği aşağıdaki verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="18224-146">hello following example is a request for a new service key:</span></span>

```azurecli
az network express-route create --bandwidth 200 -n MyCircuit --peering-location "Silicon Valley" -g ExpressRouteResourceGroup --provider "Equinix" -l "West US" --sku-family MeteredData --sku-tier Standard
```

<span data-ttu-id="18224-147">Merhaba yanıt hello hizmet anahtarı içerir.</span><span class="sxs-lookup"><span data-stu-id="18224-147">hello response contains hello service key.</span></span>

### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="18224-148">4. Tüm ExpressRoute bağlantı hatları listesi</span><span class="sxs-lookup"><span data-stu-id="18224-148">4. List all ExpressRoute circuits</span></span>

<span data-ttu-id="18224-149">tooget, oluşturduğunuz tüm hello ExpressRoute bağlantı hatları listesini hello 'az ağ hızlı rota listesi' komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="18224-149">tooget a list of all hello ExpressRoute circuits that you created, run hello 'az network express-route list' command.</span></span> <span data-ttu-id="18224-150">Bu komutu kullanarak bu bilgileri dilediğiniz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="18224-150">You can retrieve this information at any time by using this command.</span></span> <span data-ttu-id="18224-151">toolist tüm devreler hello parametresiz çağrısı yapın.</span><span class="sxs-lookup"><span data-stu-id="18224-151">toolist all circuits, make hello call with no parameters.</span></span>

```azurecli
az network express-route list
```

<span data-ttu-id="18224-152">Hizmet anahtarınız hello listelenen *ServiceKey* hello yanıtının alan.</span><span class="sxs-lookup"><span data-stu-id="18224-152">Your service key is listed in hello *ServiceKey* field of hello response.</span></span>

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
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

<span data-ttu-id="18224-153">Tüm hello parametrelerin ayrıntılı açıklamaları hello kullanarak çalışan hello komutu tarafından alabilirsiniz '-h' parametresi.</span><span class="sxs-lookup"><span data-stu-id="18224-153">You can get detailed descriptions of all hello parameters by running hello command using hello '-h' parameter.</span></span>

```azurecli
az network express-route list -h
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="18224-154">5. Merhaba hizmet anahtar tooyour bağlantı sağlayıcı sağlamak için Gönder</span><span class="sxs-lookup"><span data-stu-id="18224-154">5. Send hello service key tooyour connectivity provider for provisioning</span></span>

<span data-ttu-id="18224-155">'ServiceProviderProvisioningState' hello hizmet sağlayıcı tarafında sağlama hello geçerli durumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="18224-155">'ServiceProviderProvisioningState' provides information about hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="18224-156">Merhaba durum Microsoft yan hello üzerinde hello durumunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="18224-156">hello status provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="18224-157">Daha fazla bilgi için bkz: Merhaba [iş akışları makale](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span><span class="sxs-lookup"><span data-stu-id="18224-157">For more information, see hello [Workflows article](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span></span>

<span data-ttu-id="18224-158">Yeni bir expressroute bağlantı hattı oluşturduğunuzda, hello devre durumunu izleyen hello oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="18224-158">When you create a new ExpressRoute circuit, hello circuit is in hello following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "NotProvisioned"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="18224-159">Merhaba hattı hello bağlantı sağlayıcı için etkinleştirme işleminin hello olduğunda durumu aşağıdaki toohello değiştirir:</span><span class="sxs-lookup"><span data-stu-id="18224-159">hello circuit changes toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioning"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="18224-160">Toobe mümkün toouse için bir expressroute bağlantı hattı, durumu aşağıdaki hello olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="18224-160">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioned"
"circuitProvisioningState": "Enabled
```

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="18224-161">6. Merhaba durumunu ve hello hattı anahtar hello durumunu düzenli aralıklarla denetleyin</span><span class="sxs-lookup"><span data-stu-id="18224-161">6. Periodically check hello status and hello state of hello circuit key</span></span>

<span data-ttu-id="18224-162">Merhaba durumu ve hello hattı anahtar hello durumunu denetleme, sağlayıcınız hattınız etkinleştirildiğinde bilmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="18224-162">Checking hello status and hello state of hello circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="18224-163">Merhaba hattı yapılandırıldıktan sonra 'ServiceProviderProvisioningState' 'Hazırlandı ' hello aşağıdaki örnekte gösterildiği gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="18224-163">After hello circuit has been configured, 'ServiceProviderProvisioningState' appears as 'Provisioned', as shown in hello following example:</span></span>

```azurecli
az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
```

<span data-ttu-id="18224-164">Merhaba yanıt benzer toohello örneği aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="18224-164">hello response is similar toohello following example:</span></span>

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
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="18224-165">7. Yönlendirme yapılandırması oluşturma</span><span class="sxs-lookup"><span data-stu-id="18224-165">7. Create your routing configuration</span></span>

<span data-ttu-id="18224-166">Merhaba adım adım yönergeler için bkz: [expressroute bağlantı hattı yönlendirme yapılandırması](howto-routing-cli.md) makale toocreate ve hattı eşlemeler değiştirin.</span><span class="sxs-lookup"><span data-stu-id="18224-166">For step-by-step instructions, see hello [ExpressRoute circuit routing configuration](howto-routing-cli.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="18224-167">Bu yönergeler yalnızca Katman 2 bağlantı hizmetleri sunan hizmet sağlayıcıları ile oluşturulan toocircuits geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="18224-167">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="18224-168">Yönetilen sunan bir hizmet sağlayıcısı kullanıyorsanız, Katman 3 Hizmetleri (genellikle bir IP VPN, MPLS gibi), bağlantı sağlayıcınız yönlendirmeyi sizin için yönetir ve yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="18224-168">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="18224-169">8. Sanal ağ tooan expressroute bağlantı hattı bağlantı</span><span class="sxs-lookup"><span data-stu-id="18224-169">8. Link a virtual network tooan ExpressRoute circuit</span></span>

<span data-ttu-id="18224-170">Ardından, sanal ağ tooyour expressroute bağlantı hattı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="18224-170">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="18224-171">Kullanım hello [sanal bağlama ağları tooExpressRoute devreler](howto-linkvnet-cli.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="18224-171">Use hello [Linking virtual networks tooExpressRoute circuits](howto-linkvnet-cli.md) article.</span></span>

## <span data-ttu-id="18224-172"><a name="modify"></a>Bir expressroute bağlantı hattı değiştirme</span><span class="sxs-lookup"><span data-stu-id="18224-172"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>

<span data-ttu-id="18224-173">Bağlantı etkilemeden belirli bir expressroute bağlantı hattı özelliklerini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="18224-173">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span> <span data-ttu-id="18224-174">Aşağıdaki değişiklikler kapalı kalma süresi olmadan hello yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="18224-174">You can make hello following changes with no downtime:</span></span>

* <span data-ttu-id="18224-175">Etkinleştirmek veya expressroute bağlantı hattı için ExpressRoute premium eklentisi devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="18224-175">You can enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="18224-176">Sağlanmış kapasite kullanılabilir hello bağlantı noktasında hello bant genişliği, expressroute bağlantı hattı artırabilir.</span><span class="sxs-lookup"><span data-stu-id="18224-176">You can increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="18224-177">Ancak, bir bağlantı hattının hello bant genişliği önceki sürüme indirme desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="18224-177">However, downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="18224-178">Ölçülen veri tooUnlimited veri hello ölçüm planı değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="18224-178">You can change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="18224-179">Ancak, veri desteklenmiyor sınırsız veri tooMetered planından ölçümü hello değiştirme.</span><span class="sxs-lookup"><span data-stu-id="18224-179">However, changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="18224-180">Etkinleştirme ve devre dışı *izin Klasik işlemleri*.</span><span class="sxs-lookup"><span data-stu-id="18224-180">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="18224-181">Merhaba sınırlar ve sınırlamalar hakkında daha fazla bilgi için bkz: [ExpressRoute SSS](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="18224-181">For more information on limits and limitations, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="18224-182">tooenable hello ExpressRoute premium eklentisi</span><span class="sxs-lookup"><span data-stu-id="18224-182">tooenable hello ExpressRoute premium add-on</span></span>

<span data-ttu-id="18224-183">Hello aşağıdaki komutu kullanarak, varolan bağlantı hattınız için hello ExpressRoute premium eklentisi etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="18224-183">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following command:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Premium
```

<span data-ttu-id="18224-184">Merhaba hattı artık etkin hello ExpressRoute premium eklentisi özellikler sahiptir.</span><span class="sxs-lookup"><span data-stu-id="18224-184">hello circuit now has hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="18224-185">Merhaba komutu başarıyla çalıştırıldı hemen için hello premium eklenti özelliğini faturalama başlayın.</span><span class="sxs-lookup"><span data-stu-id="18224-185">We begin billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="18224-186">toodisable hello ExpressRoute premium eklentisi</span><span class="sxs-lookup"><span data-stu-id="18224-186">toodisable hello ExpressRoute premium add-on</span></span>

> [!IMPORTANT]
> <span data-ttu-id="18224-187">Merhaba standart bağlantı hattı için izin daha büyük olan kaynaklar kullanıyorsanız, bu işlemi başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="18224-187">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

<span data-ttu-id="18224-188">Merhaba ExpressRoute premium eklentisi'nı devre dışı bırakmadan önce aşağıdaki ölçütleri hello anlama:</span><span class="sxs-lookup"><span data-stu-id="18224-188">Before disabling hello ExpressRoute premium add-on, understand hello following criteria:</span></span>

* <span data-ttu-id="18224-189">Premium toostandard düşürmek önce 10'dan az sanal ağlar bağlantılı toohello hattı sahip olduğunuzdan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="18224-189">Before you downgrade from premium toostandard, you must make sure that you have fewer than 10 virtual networks linked toohello circuit.</span></span> <span data-ttu-id="18224-190">Birden fazla 10 varsa, güncelleştirme isteği başarısız olur ve biz premium oranlarda fatura.</span><span class="sxs-lookup"><span data-stu-id="18224-190">If you have more than 10, your update request fails, and we bill you at premium rates.</span></span>
* <span data-ttu-id="18224-191">Tüm sanal ağları diğer coğrafi bölgelerde bağlantısını gerekir.</span><span class="sxs-lookup"><span data-stu-id="18224-191">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="18224-192">Tüm sanal ağları bağlantısını yok, güncelleştirme isteği başarısız olur ve biz premium oranlarda fatura.</span><span class="sxs-lookup"><span data-stu-id="18224-192">If you don't unlink all your virtual networks, your update request fails and we bill you at premium rates.</span></span>
* <span data-ttu-id="18224-193">Yol tablosu özel eşleme için 4. 000'den az yolları olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="18224-193">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="18224-194">Rota tablosu boyutunuz 4.000 yolları büyükse, hello BGP oturumu bırakır.</span><span class="sxs-lookup"><span data-stu-id="18224-194">If your route table size is greater than 4,000 routes, hello BGP session drops.</span></span> <span data-ttu-id="18224-195">tanıtılan önekler Hello sayısı 4.000 kadar hello oturumu yeniden iler hale olmaz.</span><span class="sxs-lookup"><span data-stu-id="18224-195">hello session won't be reenabled until hello number of advertised prefixes is below 4,000.</span></span>

<span data-ttu-id="18224-196">Aşağıdaki örneğine hello kullanarak hello ExpressRoute premium eklentisi hello varolan hattı için devre dışı bırakabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="18224-196">You can disable hello ExpressRoute premium add-on for hello existing circuit by using hello following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Standard
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="18224-197">tooupdate hello ExpressRoute devresi bant genişliği</span><span class="sxs-lookup"><span data-stu-id="18224-197">tooupdate hello ExpressRoute circuit bandwidth</span></span>

<span data-ttu-id="18224-198">Merhaba denetimi sağlayıcınız için desteklenen hello bant genişliği seçenekleri için [ExpressRoute SSS](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="18224-198">For hello supported bandwidth options for your provider, check hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="18224-199">Var olan bağlantı hattınız hello boyutundan büyük herhangi bir boyutta seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="18224-199">You can pick any size greater than hello size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="18224-200">Merhaba varolan bağlantı noktasında yetersiz kapasite ise toorecreate hello expressroute bağlantı hattı olabilir.</span><span class="sxs-lookup"><span data-stu-id="18224-200">If there is inadequate capacity on hello existing port, you may have toorecreate hello ExpressRoute circuit.</span></span> <span data-ttu-id="18224-201">Varsa hiçbir ek kapasite kullanılabilir o konumda hello hattı yükseltemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="18224-201">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="18224-202">Bir expressroute bağlantı hattı kesintiye uğratmadan hello bant genişliği azaltma olamaz.</span><span class="sxs-lookup"><span data-stu-id="18224-202">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="18224-203">Bant genişliği eski sürüme düşürmeyi, toodeprovision hello expressroute bağlantı hattı gerektirir ve yeni bir expressroute bağlantı hattı yeniden sağlayın.</span><span class="sxs-lookup"><span data-stu-id="18224-203">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit, and then reprovision a new ExpressRoute circuit.</span></span>
>

<span data-ttu-id="18224-204">Gereksinim duyduğunuz hello boyutu karar verdikten sonra komutu tooresize aşağıdaki hello hattınız kullanın:</span><span class="sxs-lookup"><span data-stu-id="18224-204">After you decide hello size you need, use hello following command tooresize your circuit:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --bandwidth 1000
```

<span data-ttu-id="18224-205">Bağlantı hattınız hello Microsoft tarafında boyutlandırılır.</span><span class="sxs-lookup"><span data-stu-id="18224-205">Your circuit is sized up on hello Microsoft side.</span></span> <span data-ttu-id="18224-206">Ardından, bu değişikliği kendi yan toomatch, bağlantı sağlayıcısı tooupdate yapılandırmalarında başvurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="18224-206">Next, you must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="18224-207">Bu bildirim yaptıktan sonra güncelleştirilmiş hello bant seçeneği için faturalama başlayın.</span><span class="sxs-lookup"><span data-stu-id="18224-207">After you make this notification, we begin billing you for hello updated bandwidth option.</span></span>

### <a name="toomove-hello-sku-from-metered-toounlimited"></a><span data-ttu-id="18224-208">ölçülen toounlimited gelen toomove hello SKU</span><span class="sxs-lookup"><span data-stu-id="18224-208">toomove hello SKU from metered toounlimited</span></span>

<span data-ttu-id="18224-209">Aşağıdaki örneğine hello kullanarak hello ExpressRoute devresi SKU'su değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="18224-209">You can change hello SKU of an ExpressRoute circuit by using hello following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-family UnlimitedData
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a><span data-ttu-id="18224-210">toocontrol erişim toohello Klasik ve Resource Manager ortamları</span><span class="sxs-lookup"><span data-stu-id="18224-210">toocontrol access toohello classic and Resource Manager environments</span></span>

<span data-ttu-id="18224-211">Merhaba yönergeleri gözden [taşıma ExpressRoute bağlantı hatları hello Klasik toohello Resource Manager dağıtım modelinde](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="18224-211">Review hello instructions in [Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="18224-212">Sağlamayı kaldırmayı ve bir expressroute bağlantı hattı silme</span><span class="sxs-lookup"><span data-stu-id="18224-212">Deprovisioning and deleting an ExpressRoute circuit</span></span>

<span data-ttu-id="18224-213">toodeprovision ve delete bir expressroute bağlantı hattı ölçütleri aşağıdaki hello anladığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="18224-213">toodeprovision and delete an ExpressRoute circuit, make sure you understand hello following criteria:</span></span>

* <span data-ttu-id="18224-214">Tüm sanal ağlardan hello expressroute bağlantı hattı bağlantısını gerekir.</span><span class="sxs-lookup"><span data-stu-id="18224-214">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="18224-215">Bu işlem başarısız olursa, tüm sanal ağ olup olmadığını toosee toohello hattı bağlı denetleyin.</span><span class="sxs-lookup"><span data-stu-id="18224-215">If this operation fails, check toosee if any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="18224-216">Merhaba ExpressRoute bağlantı hattı Hizmet Sağlayıcısı sağlama durumu ise **sağlama** veya **hazırlandı**, kendi tarafında hizmet sağlayıcısı toodeprovision hello hattınız ile çalışmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="18224-216">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned**, you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="18224-217">Biz tooreserve kaynakları devam et ve hello hizmet sağlayıcısı sağlamayı hello hattı tamamlandıktan ve bize bildiren kadar sizi faturalandırmak.</span><span class="sxs-lookup"><span data-stu-id="18224-217">We continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="18224-218">Merhaba hizmet sağlayıcısı hello hattı sağlaması kaldırılıyor. sağlaması hello hattı silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="18224-218">You can delete hello circuit if hello service provider has deprovisioned hello circuit.</span></span> <span data-ttu-id="18224-219">Bir bağlantı hattı sağlaması kaldırılıyor. sağlaması durumlar hello Hizmet Sağlayıcısı sağlama durumu çok ayarlanır**sağlanmadı**.</span><span class="sxs-lookup"><span data-stu-id="18224-219">When a circuit is deprovisioned, hello service provider provisioning state is set too**Not provisioned**.</span></span> <span data-ttu-id="18224-220">Merhaba hattı için fatura durdurur.</span><span class="sxs-lookup"><span data-stu-id="18224-220">This stops billing for hello circuit.</span></span>

<span data-ttu-id="18224-221">Hello aşağıdaki komutu çalıştırarak, expressroute bağlantı hattı silebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="18224-221">You can delete your ExpressRoute circuit by running hello following command:</span></span>

```azurecli
az network express-route delete  -n MyCircuit -g ExpressRouteResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="18224-222">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="18224-222">Next steps</span></span>

<span data-ttu-id="18224-223">Bağlantı hattınız oluşturduktan sonra görevleri hello emin olun:</span><span class="sxs-lookup"><span data-stu-id="18224-223">After you create your circuit, make sure that you do hello following tasks:</span></span>

* [<span data-ttu-id="18224-224">Oluşturma ve expressroute bağlantı hattı için yönlendirmeyi değiştirme</span><span class="sxs-lookup"><span data-stu-id="18224-224">Create and modify routing for your ExpressRoute circuit</span></span>](howto-routing-cli.md)
* [<span data-ttu-id="18224-225">Sanal ağ tooyour expressroute bağlantı hattı bağlantı</span><span class="sxs-lookup"><span data-stu-id="18224-225">Link your virtual network tooyour ExpressRoute circuit</span></span>](howto-linkvnet-cli.md)
