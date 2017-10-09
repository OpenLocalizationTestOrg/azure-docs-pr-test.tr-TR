---
title: "ExpressRoute bağlantı hatları Klasik tooResource Yöneticisi taşıma: PowerShell: Azure | Microsoft Docs"
description: "Bu sayfayı nasıl toomove Klasik hattı toohello Resource Manager dağıtım modeli PowerShell kullanarak açıklar."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 08152836-23e7-42d1-9a56-8306b341cd91
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/03/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8dcadafca5e4f40773902cec5786eba1dbe133eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model-using-powershell"></a><span data-ttu-id="1102f-103">PowerShell kullanarak hello Klasik toohello Resource Manager dağıtım modelinden ExpressRoute bağlantı hatları taşıma</span><span class="sxs-lookup"><span data-stu-id="1102f-103">Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model using PowerShell</span></span>

<span data-ttu-id="1102f-104">toouse hello Klasik ve Resource Manager dağıtım modeli için expressroute bağlantı hattı, hello hattı toohello Resource Manager dağıtım modeli taşımanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1102f-104">toouse an ExpressRoute circuit for both hello classic and Resource Manager deployment models, you must move hello circuit toohello Resource Manager deployment model.</span></span> <span data-ttu-id="1102f-105">Merhaba aşağıdaki bölümlerde, PowerShell kullanarak hattınız taşımanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="1102f-105">hello following sections help you move your circuit by using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1102f-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="1102f-106">Before you begin</span></span>

* <span data-ttu-id="1102f-107">Merhaba hello Azure PowerShell modüllerinin en son sürümüne sahip olduğunuzdan emin olun (en az sürüm 1.0).</span><span class="sxs-lookup"><span data-stu-id="1102f-107">Verify that you have hello latest version of hello Azure PowerShell modules (at least version 1.0).</span></span> <span data-ttu-id="1102f-108">Daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1102f-108">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="1102f-109">Merhaba gözden geçirdiğinizden emin olun [Önkoşullar](expressroute-prerequisites.md), [yönlendirme gereksinimleri](expressroute-routing.md), ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="1102f-109">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="1102f-110">Altında sağlanan hello bilgileri gözden [bir expressroute bağlantı hattı Klasik tooResource Yöneticisi taşıma](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="1102f-110">Review hello information that is provided under [Moving an ExpressRoute circuit from classic tooResource Manager](expressroute-move.md).</span></span> <span data-ttu-id="1102f-111">Tam olarak hello sınırları ve kısıtlamaları anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="1102f-111">Make sure that you fully understand hello limits and limitations.</span></span>
* <span data-ttu-id="1102f-112">Merhaba hattı hello Klasik dağıtım modelinde tam olarak işlevsel olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="1102f-112">Verify that hello circuit is fully operational in hello classic deployment model.</span></span>
* <span data-ttu-id="1102f-113">Merhaba Resource Manager dağıtım modelinde oluşturulmuş bir kaynak grubu olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="1102f-113">Ensure that you have a resource group that was created in hello Resource Manager deployment model.</span></span>

## <a name="move-an-expressroute-circuit"></a><span data-ttu-id="1102f-114">Bir expressroute bağlantı hattı taşıma</span><span class="sxs-lookup"><span data-stu-id="1102f-114">Move an ExpressRoute circuit</span></span>

### <a name="step-1-gather-circuit-details-from-hello-classic-deployment-model"></a><span data-ttu-id="1102f-115">Adım 1: hello Klasik dağıtım modelinden bağlantı hattı ayrıntılarını toplama</span><span class="sxs-lookup"><span data-stu-id="1102f-115">Step 1: Gather circuit details from hello classic deployment model</span></span>

<span data-ttu-id="1102f-116">Toohello Azure Klasik ortamı oturum ve hello hizmet anahtarı toplayın.</span><span class="sxs-lookup"><span data-stu-id="1102f-116">Sign in toohello Azure classic environment and gather hello service key.</span></span>

1. <span data-ttu-id="1102f-117">İçinde tooyour Azure hesabı oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1102f-117">Sign in tooyour Azure account.</span></span>

  ```powershell
  Add-AzureAccount
  ```

2. <span data-ttu-id="1102f-118">Merhaba uygun Azure aboneliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="1102f-118">Select hello appropriate Azure subscription.</span></span>

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. <span data-ttu-id="1102f-119">Merhaba PowerShell modülleri Azure ve ExpressRoute için içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="1102f-119">Import hello PowerShell modules for Azure and ExpressRoute.</span></span>

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. <span data-ttu-id="1102f-120">Tooget hello hizmeti anahtarları aşağıda Hello cmdlet'ini tüm ExpressRoute bağlantı hatları için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1102f-120">Use hello cmdlet below tooget hello service keys for all of your ExpressRoute circuits.</span></span> <span data-ttu-id="1102f-121">Merhaba Hello anahtarları aldıktan sonra kopyalama **hizmet anahtarı** hello devrenin toomove toohello Resource Manager dağıtım modeli istiyor.</span><span class="sxs-lookup"><span data-stu-id="1102f-121">After retrieving hello keys, copy hello **service key** of hello circuit that you want toomove toohello Resource Manager deployment model.</span></span>

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a><span data-ttu-id="1102f-122">2. adım: Oturum açın ve bir kaynak grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="1102f-122">Step 2: Sign in and create a resource group</span></span>

<span data-ttu-id="1102f-123">Toohello Resource Manager ortamında oturum açın ve yeni bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1102f-123">Sign in toohello Resource Manager environment and create a new resource group.</span></span>

1. <span data-ttu-id="1102f-124">Tooyour Azure Resource Manager ortamında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1102f-124">Sign in tooyour Azure Resource Manager environment.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="1102f-125">Merhaba uygun Azure aboneliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="1102f-125">Select hello appropriate Azure subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. <span data-ttu-id="1102f-126">Bir kaynak grubu zaten yoksa toocreate yeni bir kaynak grubu aşağıdaki kod parçacığını hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1102f-126">Modify hello snippet below toocreate a new resource group if you don't already have a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-hello-expressroute-circuit-toohello-resource-manager-deployment-model"></a><span data-ttu-id="1102f-127">3. adım: Merhaba ExpressRoute bağlantı hattı toohello Resource Manager dağıtım modeline taşıma</span><span class="sxs-lookup"><span data-stu-id="1102f-127">Step 3: Move hello ExpressRoute circuit toohello Resource Manager deployment model</span></span>

<span data-ttu-id="1102f-128">Artık hazır toomove hello Klasik dağıtım modeli toohello Resource Manager dağıtım modeli, expressroute bağlantı hattı şunlardır.</span><span class="sxs-lookup"><span data-stu-id="1102f-128">You are now ready toomove your ExpressRoute circuit from hello classic deployment model toohello Resource Manager deployment model.</span></span> <span data-ttu-id="1102f-129">Devam etmeden önce sağlanan hello bilgileri gözden [hello Klasik toohello Resource Manager dağıtım modelinden bir expressroute bağlantı hattı taşıma](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="1102f-129">Before proceeding, review hello information provided in [Moving an ExpressRoute circuit from hello classic toohello Resource Manager deployment model](expressroute-move.md).</span></span>

<span data-ttu-id="1102f-130">toomove hattınızı değiştirin ve aşağıdaki kod parçacığında hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="1102f-130">toomove your circuit, modify and run hello following snippet:</span></span>

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> <span data-ttu-id="1102f-131">Merhaba taşıma tamamlandıktan sonra hello önceki cmdlet'te listelenen hello yeni adı kullanılan tooaddress hello kaynak olacaktır.</span><span class="sxs-lookup"><span data-stu-id="1102f-131">After hello move has finished, hello new name that is listed in hello previous cmdlet will be used tooaddress hello resource.</span></span> <span data-ttu-id="1102f-132">Merhaba hattı temelde yeniden adlandırılacak.</span><span class="sxs-lookup"><span data-stu-id="1102f-132">hello circuit will essentially be renamed.</span></span>
> 

## <a name="modify-circuit-access"></a><span data-ttu-id="1102f-133">Bağlantı hattı erişimi değiştirme</span><span class="sxs-lookup"><span data-stu-id="1102f-133">Modify circuit access</span></span>

### <a name="tooenable-expressroute-circuit-access-for-both-deployment-models"></a><span data-ttu-id="1102f-134">tooenable her iki dağıtım modeli için ExpressRoute bağlantı hattı erişim</span><span class="sxs-lookup"><span data-stu-id="1102f-134">tooenable ExpressRoute circuit access for both deployment models</span></span>

<span data-ttu-id="1102f-135">Klasik ExpressRoute bağlantı hattı toohello Resource Manager dağıtım modeli taşıdıktan sonra erişim tooboth dağıtım modellerini etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1102f-135">After moving your classic ExpressRoute circuit toohello Resource Manager deployment model, you can enable access tooboth deployment models.</span></span> <span data-ttu-id="1102f-136">Aşağıdaki cmdlet'leri tooenable erişim tooboth dağıtım modellerini hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="1102f-136">Run hello following cmdlets tooenable access tooboth deployment models:</span></span>

1. <span data-ttu-id="1102f-137">Merhaba hattı ayrıntıları alın.</span><span class="sxs-lookup"><span data-stu-id="1102f-137">Get hello circuit details.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="1102f-138">"Klasik işlemleri izin ver" tooTRUE ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1102f-138">Set "Allow Classic Operations" tooTRUE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. <span data-ttu-id="1102f-139">Merhaba hattı güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="1102f-139">Update hello circuit.</span></span> <span data-ttu-id="1102f-140">Bu işlemi başarıyla tamamlandıktan sonra mümkün tooview hello hattı hello Klasik dağıtım modelinde olacaktır.</span><span class="sxs-lookup"><span data-stu-id="1102f-140">After this operation has finished successfully, you will be able tooview hello circuit in hello classic deployment model.</span></span>

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. <span data-ttu-id="1102f-141">Aşağıdaki cmdlet'i tooget hello hello expressroute bağlantı hattı ayrıntılarını hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1102f-141">Run hello following cmdlet tooget hello details of hello ExpressRoute circuit.</span></span> <span data-ttu-id="1102f-142">Listelenen mümkün toosee hello hizmet anahtarı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1102f-142">You must be able toosee hello service key listed.</span></span>

  ```powershell
  get-azurededicatedcircuit
  ```

5. <span data-ttu-id="1102f-143">Artık bağlantılar toohello expressroute bağlantı hattı Resource Manager sanal ağlar için Klasik sanal ağlar ve hello Resource Manager komutları için hello Klasik dağıtım modeli komutlarını kullanarak da yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1102f-143">You can now manage links toohello ExpressRoute circuit using hello classic deployment model commands for classic VNets, and hello Resource Manager commands for Resource Manager VNets.</span></span> <span data-ttu-id="1102f-144">Merhaba aşağıdaki makalelere bağlantılar toohello expressroute bağlantı hattı yönetmenize yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="1102f-144">hello following articles help you manage links toohello ExpressRoute circuit:</span></span>

    * [<span data-ttu-id="1102f-145">Sanal ağ tooyour expressroute bağlantı hattı hello Resource Manager dağıtım modelinde bağlantı</span><span class="sxs-lookup"><span data-stu-id="1102f-145">Link your virtual network tooyour ExpressRoute circuit in hello Resource Manager deployment model</span></span>](expressroute-howto-linkvnet-arm.md)
    * [<span data-ttu-id="1102f-146">Sanal ağ tooyour expressroute bağlantı hattı hello Klasik dağıtım modelinde bağlantı</span><span class="sxs-lookup"><span data-stu-id="1102f-146">Link your virtual network tooyour ExpressRoute circuit in hello classic deployment model</span></span>](expressroute-howto-linkvnet-classic.md)

### <a name="toodisable-expressroute-circuit-access-toohello-classic-deployment-model"></a><span data-ttu-id="1102f-147">toodisable ExpressRoute bağlantı hattı erişim toohello Klasik dağıtım modeli</span><span class="sxs-lookup"><span data-stu-id="1102f-147">toodisable ExpressRoute circuit access toohello classic deployment model</span></span>

<span data-ttu-id="1102f-148">Cmdlet'leri toodisable erişim toohello Klasik dağıtım modeli izleyen hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1102f-148">Run hello following cmdlets toodisable access toohello classic deployment model.</span></span>

1. <span data-ttu-id="1102f-149">Merhaba expressroute bağlantı hattı ayrıntılarını alın.</span><span class="sxs-lookup"><span data-stu-id="1102f-149">Get details of hello ExpressRoute circuit.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="1102f-150">"Klasik işlemleri izin ver" tooFALSE ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1102f-150">Set "Allow Classic Operations" tooFALSE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. <span data-ttu-id="1102f-151">Merhaba hattı güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="1102f-151">Update hello circuit.</span></span> <span data-ttu-id="1102f-152">Bu işlemi başarıyla tamamlandıktan sonra mümkün tooview hello hattı hello Klasik dağıtım modelinde olmaz.</span><span class="sxs-lookup"><span data-stu-id="1102f-152">After this operation has finished successfully, you will not be able tooview hello circuit in hello classic deployment model.</span></span>

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a><span data-ttu-id="1102f-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1102f-153">Next steps</span></span>

* [<span data-ttu-id="1102f-154">Oluşturma ve expressroute bağlantı hattı için yönlendirmeyi değiştirme</span><span class="sxs-lookup"><span data-stu-id="1102f-154">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="1102f-155">Sanal ağ tooyour expressroute bağlantı hattı bağlantı</span><span class="sxs-lookup"><span data-stu-id="1102f-155">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)
