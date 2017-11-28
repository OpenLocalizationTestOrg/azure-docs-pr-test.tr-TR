---
title: "ExpressRoute bağlantı hatlarını Klasikten Resource Manager taşıma: PowerShell: Azure | Microsoft Docs"
description: "Bu sayfa, Klasik hattı PowerShell kullanarak Resource Manager dağıtım modeline taşıma açıklar."
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
ms.openlocfilehash: c407e01e6d881cb8adcfe55faa246468669be883
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="move-expressroute-circuits-from-the-classic-to-the-resource-manager-deployment-model-using-powershell"></a><span data-ttu-id="56f7c-103">ExpressRoute bağlantı hatları Klasikten Resource Manager dağıtım modeline PowerShell kullanarak Taşı</span><span class="sxs-lookup"><span data-stu-id="56f7c-103">Move ExpressRoute circuits from the classic to the Resource Manager deployment model using PowerShell</span></span>

<span data-ttu-id="56f7c-104">Bir expressroute bağlantı hattı Klasik ve Resource Manager dağıtım modelleri için kullanmak için bağlantı hattı Resource Manager dağıtım modeline taşımanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="56f7c-104">To use an ExpressRoute circuit for both the classic and Resource Manager deployment models, you must move the circuit to the Resource Manager deployment model.</span></span> <span data-ttu-id="56f7c-105">Aşağıdaki bölümlerde, PowerShell kullanarak hattınız taşımanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="56f7c-105">The following sections help you move your circuit by using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="56f7c-106">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="56f7c-106">Before you begin</span></span>

* <span data-ttu-id="56f7c-107">Azure PowerShell modüllerinin en son sürümüne sahip olduğunu doğrulayın (en az sürüm 1.0).</span><span class="sxs-lookup"><span data-stu-id="56f7c-107">Verify that you have the latest version of the Azure PowerShell modules (at least version 1.0).</span></span> <span data-ttu-id="56f7c-108">Daha fazla bilgi için bkz. [Azure PowerShell’i yükleme ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="56f7c-108">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="56f7c-109">Gözden geçirdiğinizden emin olun [Önkoşullar](expressroute-prerequisites.md), [yönlendirme gereksinimleri](expressroute-routing.md), ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="56f7c-109">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="56f7c-110">Altında sağlanan bilgileri gözden [bir expressroute bağlantı hattını Klasikten Resource Manager taşıma](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="56f7c-110">Review the information that is provided under [Moving an ExpressRoute circuit from classic to Resource Manager](expressroute-move.md).</span></span> <span data-ttu-id="56f7c-111">Tam olarak sınırları ve kısıtlamaları anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="56f7c-111">Make sure that you fully understand the limits and limitations.</span></span>
* <span data-ttu-id="56f7c-112">Bağlantı hattı Klasik dağıtım modelinde tam olarak işlevsel olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="56f7c-112">Verify that the circuit is fully operational in the classic deployment model.</span></span>
* <span data-ttu-id="56f7c-113">Resource Manager dağıtım modelinde oluşturulmuş bir kaynak grubu olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="56f7c-113">Ensure that you have a resource group that was created in the Resource Manager deployment model.</span></span>

## <a name="move-an-expressroute-circuit"></a><span data-ttu-id="56f7c-114">Bir expressroute bağlantı hattı taşıma</span><span class="sxs-lookup"><span data-stu-id="56f7c-114">Move an ExpressRoute circuit</span></span>

### <a name="step-1-gather-circuit-details-from-the-classic-deployment-model"></a><span data-ttu-id="56f7c-115">Adım 1: Klasik dağıtım modelinden bağlantı hattı ayrıntılarını toplama</span><span class="sxs-lookup"><span data-stu-id="56f7c-115">Step 1: Gather circuit details from the classic deployment model</span></span>

<span data-ttu-id="56f7c-116">Azure Klasik ortama oturum açabilir ve hizmet anahtarı toplayın.</span><span class="sxs-lookup"><span data-stu-id="56f7c-116">Sign in to the Azure classic environment and gather the service key.</span></span>

1. <span data-ttu-id="56f7c-117">Azure hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="56f7c-117">Sign in to your Azure account.</span></span>

  ```powershell
  Add-AzureAccount
  ```

2. <span data-ttu-id="56f7c-118">Uygun Azure aboneliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="56f7c-118">Select the appropriate Azure subscription.</span></span>

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. <span data-ttu-id="56f7c-119">Azure ve ExpressRoute için PowerShell modülleri içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="56f7c-119">Import the PowerShell modules for Azure and ExpressRoute.</span></span>

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. <span data-ttu-id="56f7c-120">Tüm ExpressRoute bağlantı hatları için hizmet anahtarları almak için aşağıdaki cmdlet'i kullanın.</span><span class="sxs-lookup"><span data-stu-id="56f7c-120">Use the cmdlet below to get the service keys for all of your ExpressRoute circuits.</span></span> <span data-ttu-id="56f7c-121">Anahtarları aldıktan sonra kopyalama **hizmet anahtarı** Resource Manager dağıtım modeline taşımak istediğiniz bağlantı hattının.</span><span class="sxs-lookup"><span data-stu-id="56f7c-121">After retrieving the keys, copy the **service key** of the circuit that you want to move to the Resource Manager deployment model.</span></span>

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a><span data-ttu-id="56f7c-122">2. adım: Oturum açın ve bir kaynak grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="56f7c-122">Step 2: Sign in and create a resource group</span></span>

<span data-ttu-id="56f7c-123">Resource Manager ortamına oturum açın ve yeni bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="56f7c-123">Sign in to the Resource Manager environment and create a new resource group.</span></span>

1. <span data-ttu-id="56f7c-124">Azure Resource Manager ortamınız için oturum açın.</span><span class="sxs-lookup"><span data-stu-id="56f7c-124">Sign in to your Azure Resource Manager environment.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="56f7c-125">Uygun Azure aboneliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="56f7c-125">Select the appropriate Azure subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. <span data-ttu-id="56f7c-126">Bir kaynak grubu zaten yoksa yeni bir kaynak grubu oluşturmak için aşağıdaki kod parçacığında değiştirin.</span><span class="sxs-lookup"><span data-stu-id="56f7c-126">Modify the snippet below to create a new resource group if you don't already have a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-the-expressroute-circuit-to-the-resource-manager-deployment-model"></a><span data-ttu-id="56f7c-127">3. adım: expressroute bağlantı hattı Resource Manager dağıtım modeline taşıma</span><span class="sxs-lookup"><span data-stu-id="56f7c-127">Step 3: Move the ExpressRoute circuit to the Resource Manager deployment model</span></span>

<span data-ttu-id="56f7c-128">Şimdi, expressroute bağlantı hattı Klasik dağıtım modelinden Resource Manager dağıtım modeline taşıma hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="56f7c-128">You are now ready to move your ExpressRoute circuit from the classic deployment model to the Resource Manager deployment model.</span></span> <span data-ttu-id="56f7c-129">Devam etmeden önce sağlanan bilgileri gözden [bir expressroute bağlantı hattını Klasikten Resource Manager dağıtım modeline taşıma](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="56f7c-129">Before proceeding, review the information provided in [Moving an ExpressRoute circuit from the classic to the Resource Manager deployment model](expressroute-move.md).</span></span>

<span data-ttu-id="56f7c-130">Bağlantı hattınız taşımak için değiştirin ve aşağıdaki kod parçacığında çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="56f7c-130">To move your circuit, modify and run the following snippet:</span></span>

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> <span data-ttu-id="56f7c-131">Taşıma tamamlandıktan sonra önceki cmdlet'te listelenen yeni adı kaynak adres için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="56f7c-131">After the move has finished, the new name that is listed in the previous cmdlet will be used to address the resource.</span></span> <span data-ttu-id="56f7c-132">Bağlantı hattı temelde yeniden adlandırılacak.</span><span class="sxs-lookup"><span data-stu-id="56f7c-132">The circuit will essentially be renamed.</span></span>
> 

## <a name="modify-circuit-access"></a><span data-ttu-id="56f7c-133">Bağlantı hattı erişimi değiştirme</span><span class="sxs-lookup"><span data-stu-id="56f7c-133">Modify circuit access</span></span>

### <a name="to-enable-expressroute-circuit-access-for-both-deployment-models"></a><span data-ttu-id="56f7c-134">Her iki dağıtım modeli için ExpressRoute bağlantı hattı erişimini etkinleştirmek için</span><span class="sxs-lookup"><span data-stu-id="56f7c-134">To enable ExpressRoute circuit access for both deployment models</span></span>

<span data-ttu-id="56f7c-135">Klasik expressroute bağlantı hattı Resource Manager dağıtım modeline taşıdıktan sonra her iki dağıtım modeline erişimi etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56f7c-135">After moving your classic ExpressRoute circuit to the Resource Manager deployment model, you can enable access to both deployment models.</span></span> <span data-ttu-id="56f7c-136">Her iki dağıtım modeline erişimi etkinleştirmek için aşağıdaki cmdlet'leri çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="56f7c-136">Run the following cmdlets to enable access to both deployment models:</span></span>

1. <span data-ttu-id="56f7c-137">Bağlantı hattı ayrıntıları öğrenin.</span><span class="sxs-lookup"><span data-stu-id="56f7c-137">Get the circuit details.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="56f7c-138">"Klasik işlemleri TRUE izin ver" olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="56f7c-138">Set "Allow Classic Operations" to TRUE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. <span data-ttu-id="56f7c-139">Bağlantı hattı güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="56f7c-139">Update the circuit.</span></span> <span data-ttu-id="56f7c-140">Bu işlemi başarıyla tamamlandıktan sonra Klasik dağıtım modelinde bağlantı hattına görmeye olacaktır.</span><span class="sxs-lookup"><span data-stu-id="56f7c-140">After this operation has finished successfully, you will be able to view the circuit in the classic deployment model.</span></span>

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. <span data-ttu-id="56f7c-141">Expressroute bağlantı hattı ayrıntılarını almak için aşağıdaki cmdlet'i çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="56f7c-141">Run the following cmdlet to get the details of the ExpressRoute circuit.</span></span> <span data-ttu-id="56f7c-142">Listelenen hizmet anahtarı görüyor olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="56f7c-142">You must be able to see the service key listed.</span></span>

  ```powershell
  get-azurededicatedcircuit
  ```

5. <span data-ttu-id="56f7c-143">Resource Manager sanal ağlar için Klasik sanal ağlar ve Resource Manager komutları için Klasik dağıtım modeli komutları kullanarak expressroute bağlantı hattı bağlantıları artık yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56f7c-143">You can now manage links to the ExpressRoute circuit using the classic deployment model commands for classic VNets, and the Resource Manager commands for Resource Manager VNets.</span></span> <span data-ttu-id="56f7c-144">Aşağıdaki makaleleri expressroute bağlantı hattı bağlantıları yönetmenize yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="56f7c-144">The following articles help you manage links to the ExpressRoute circuit:</span></span>

    * [<span data-ttu-id="56f7c-145">Expressroute bağlantı hattı Resource Manager dağıtım modelinde sanal ağınıza bağlamak</span><span class="sxs-lookup"><span data-stu-id="56f7c-145">Link your virtual network to your ExpressRoute circuit in the Resource Manager deployment model</span></span>](expressroute-howto-linkvnet-arm.md)
    * [<span data-ttu-id="56f7c-146">Expressroute bağlantı hattı Klasik dağıtım modelinde sanal ağınıza bağlamak</span><span class="sxs-lookup"><span data-stu-id="56f7c-146">Link your virtual network to your ExpressRoute circuit in the classic deployment model</span></span>](expressroute-howto-linkvnet-classic.md)

### <a name="to-disable-expressroute-circuit-access-to-the-classic-deployment-model"></a><span data-ttu-id="56f7c-147">Klasik dağıtım modeli için ExpressRoute bağlantı hattı erişimi devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="56f7c-147">To disable ExpressRoute circuit access to the classic deployment model</span></span>

<span data-ttu-id="56f7c-148">Klasik dağıtım modeline erişimi devre dışı bırakmak için aşağıdaki cmdlet'leri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="56f7c-148">Run the following cmdlets to disable access to the classic deployment model.</span></span>

1. <span data-ttu-id="56f7c-149">Expressroute bağlantı hattı ayrıntılarını alın.</span><span class="sxs-lookup"><span data-stu-id="56f7c-149">Get details of the ExpressRoute circuit.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="56f7c-150">"Klasik işlemleri FALSE izin ver" olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="56f7c-150">Set "Allow Classic Operations" to FALSE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. <span data-ttu-id="56f7c-151">Bağlantı hattı güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="56f7c-151">Update the circuit.</span></span> <span data-ttu-id="56f7c-152">Bu işlemi başarıyla tamamlandıktan sonra Klasik dağıtım modelinde bağlantı hattına görmeye olmaz.</span><span class="sxs-lookup"><span data-stu-id="56f7c-152">After this operation has finished successfully, you will not be able to view the circuit in the classic deployment model.</span></span>

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a><span data-ttu-id="56f7c-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="56f7c-153">Next steps</span></span>

* [<span data-ttu-id="56f7c-154">Oluşturma ve expressroute bağlantı hattı için yönlendirmeyi değiştirme</span><span class="sxs-lookup"><span data-stu-id="56f7c-154">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="56f7c-155">Sanal ağ, ExpressRoute devresine bağlama</span><span class="sxs-lookup"><span data-stu-id="56f7c-155">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)