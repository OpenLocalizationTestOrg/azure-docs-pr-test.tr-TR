---
title: "aaaSelect Windows VM görüntüleri Azure'da | Microsoft Docs"
description: "Toouse Azure PowerSHell toodetermine nasıl hello publisher, teklif, SKU ve sürümü Market VM görüntüleri öğrenin."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 188b8974-fabd-4cd3-b7dc-559cbb86b98a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 752edcd0935f5141832e49503ae800ea0145e219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-windows-vm-images-in-hello-azure-marketplace-with-azure-powershell"></a><span data-ttu-id="6bb04-103">Nasıl hello Azure PowerShell ile Azure Marketi içinde toofind Windows VM görüntüleri</span><span class="sxs-lookup"><span data-stu-id="6bb04-103">How toofind Windows VM images in hello Azure Marketplace with Azure PowerShell</span></span>

<span data-ttu-id="6bb04-104">Bu konuda nasıl hello Azure Marketi toouse Azure PowerShell toofind VM görüntüleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="6bb04-104">This topic describes how toouse Azure PowerShell toofind VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="6bb04-105">Bir Windows VM oluşturduğunuzda, bu bilgileri toospecify bir Market görüntüsü kullanın.</span><span class="sxs-lookup"><span data-stu-id="6bb04-105">Use this information toospecify a Marketplace image when you create a Windows VM.</span></span>

<span data-ttu-id="6bb04-106">Yüklü ve hello son yapılandırıldığından emin olun [Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="6bb04-106">Make sure that you installed and configured hello latest [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>



## <a name="table-of-commonly-used-windows-images"></a><span data-ttu-id="6bb04-107">Yaygın olarak kullanılan Windows görüntülerinin tablosu</span><span class="sxs-lookup"><span data-stu-id="6bb04-107">Table of commonly used Windows images</span></span>
| <span data-ttu-id="6bb04-108">PublisherName</span><span class="sxs-lookup"><span data-stu-id="6bb04-108">PublisherName</span></span> | <span data-ttu-id="6bb04-109">Sunduğu</span><span class="sxs-lookup"><span data-stu-id="6bb04-109">Offer</span></span> | <span data-ttu-id="6bb04-110">Sku</span><span class="sxs-lookup"><span data-stu-id="6bb04-110">Sku</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6bb04-111">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="6bb04-111">MicrosoftWindowsServer</span></span> |<span data-ttu-id="6bb04-112">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="6bb04-112">WindowsServer</span></span> |<span data-ttu-id="6bb04-113">2016 Datacenter</span><span class="sxs-lookup"><span data-stu-id="6bb04-113">2016-Datacenter</span></span> |
| <span data-ttu-id="6bb04-114">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="6bb04-114">MicrosoftWindowsServer</span></span> |<span data-ttu-id="6bb04-115">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="6bb04-115">WindowsServer</span></span> |<span data-ttu-id="6bb04-116">Veri Merkezi Sunucu Çekirdek 2016</span><span class="sxs-lookup"><span data-stu-id="6bb04-116">2016-Datacenter-Server-Core</span></span> |
| <span data-ttu-id="6bb04-117">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="6bb04-117">MicrosoftWindowsServer</span></span> |<span data-ttu-id="6bb04-118">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="6bb04-118">WindowsServer</span></span> |<span data-ttu-id="6bb04-119">Kapsayıcılar ile 2016 Datacenter</span><span class="sxs-lookup"><span data-stu-id="6bb04-119">2016-Datacenter-with-Containers</span></span> |
| <span data-ttu-id="6bb04-120">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="6bb04-120">MicrosoftWindowsServer</span></span> |<span data-ttu-id="6bb04-121">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="6bb04-121">WindowsServer</span></span> |<span data-ttu-id="6bb04-122">2016 Nano Server</span><span class="sxs-lookup"><span data-stu-id="6bb04-122">2016-Nano-Server</span></span> |
| <span data-ttu-id="6bb04-123">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="6bb04-123">MicrosoftWindowsServer</span></span> |<span data-ttu-id="6bb04-124">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="6bb04-124">WindowsServer</span></span> |<span data-ttu-id="6bb04-125">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="6bb04-125">2012-R2-Datacenter</span></span> |
| <span data-ttu-id="6bb04-126">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="6bb04-126">MicrosoftWindowsServer</span></span> |<span data-ttu-id="6bb04-127">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="6bb04-127">WindowsServer</span></span> |<span data-ttu-id="6bb04-128">2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="6bb04-128">2008-R2-SP1</span></span> |
| <span data-ttu-id="6bb04-129">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="6bb04-129">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="6bb04-130">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="6bb04-130">DynamicsNAV</span></span> |<span data-ttu-id="6bb04-131">2017</span><span class="sxs-lookup"><span data-stu-id="6bb04-131">2017</span></span> |
| <span data-ttu-id="6bb04-132">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="6bb04-132">MicrosoftSharePoint</span></span> |<span data-ttu-id="6bb04-133">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="6bb04-133">MicrosoftSharePointServer</span></span> |<span data-ttu-id="6bb04-134">2016</span><span class="sxs-lookup"><span data-stu-id="6bb04-134">2016</span></span> |
| <span data-ttu-id="6bb04-135">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="6bb04-135">MicrosoftSQLServer</span></span> |<span data-ttu-id="6bb04-136">SQL2016 WS2016</span><span class="sxs-lookup"><span data-stu-id="6bb04-136">SQL2016-WS2016</span></span> |<span data-ttu-id="6bb04-137">Enterprise</span><span class="sxs-lookup"><span data-stu-id="6bb04-137">Enterprise</span></span> |
| <span data-ttu-id="6bb04-138">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="6bb04-138">MicrosoftSQLServer</span></span> |<span data-ttu-id="6bb04-139">SQL2014SP2 WS2012R2</span><span class="sxs-lookup"><span data-stu-id="6bb04-139">SQL2014SP2-WS2012R2</span></span> |<span data-ttu-id="6bb04-140">Enterprise</span><span class="sxs-lookup"><span data-stu-id="6bb04-140">Enterprise</span></span> |
| <span data-ttu-id="6bb04-141">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="6bb04-141">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="6bb04-142">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="6bb04-142">WindowsServerHPCPack</span></span> |<span data-ttu-id="6bb04-143">2012R2</span><span class="sxs-lookup"><span data-stu-id="6bb04-143">2012R2</span></span> |
| <span data-ttu-id="6bb04-144">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="6bb04-144">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="6bb04-145">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="6bb04-145">WindowsServerEssentials</span></span> |<span data-ttu-id="6bb04-146">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="6bb04-146">WindowsServerEssentials</span></span> |

## <a name="find-specific-images"></a><span data-ttu-id="6bb04-147">Belirli görüntüleri bulma</span><span class="sxs-lookup"><span data-stu-id="6bb04-147">Find specific images</span></span>


<span data-ttu-id="6bb04-148">Azure Resource Manager ile yeni bir sanal makine oluştururken, bazı durumlarda, toospecify görüntünün görüntü özelliklerini aşağıdaki hello hello birlikte gerekir:</span><span class="sxs-lookup"><span data-stu-id="6bb04-148">When creating a new virtual machine with Azure Resource Manager, in some cases you need toospecify an image with hello combination of hello following image properties:</span></span>

* <span data-ttu-id="6bb04-149">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="6bb04-149">Publisher</span></span>
* <span data-ttu-id="6bb04-150">Sunduğu</span><span class="sxs-lookup"><span data-stu-id="6bb04-150">Offer</span></span>
* <span data-ttu-id="6bb04-151">SKU</span><span class="sxs-lookup"><span data-stu-id="6bb04-151">SKU</span></span>

<span data-ttu-id="6bb04-152">Örneğin, bu değerleri ile Merhaba kullanın [kümesi AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) PowerShell cmdlet'ini veya bir kaynak grubu şablonu içinde belirtmelisiniz oluşturulan VM toobe hello türü.</span><span class="sxs-lookup"><span data-stu-id="6bb04-152">For example, use these values with hello [Set-AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) PowerShell cmdlet, or with a resource group template in which you must specify hello type of VM toobe created.</span></span>

<span data-ttu-id="6bb04-153">Bu değerleri toodetermine gerekiyorsa, hello çalıştırabilirsiniz [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), ve [Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlet'leri toonavigate hello görüntüler.</span><span class="sxs-lookup"><span data-stu-id="6bb04-153">If you need toodetermine these values, you can run hello [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), and [Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlets toonavigate hello images.</span></span> <span data-ttu-id="6bb04-154">Bu değerler belirler:</span><span class="sxs-lookup"><span data-stu-id="6bb04-154">You determine these values:</span></span>

1. <span data-ttu-id="6bb04-155">Liste hello görüntü yayımcılar.</span><span class="sxs-lookup"><span data-stu-id="6bb04-155">List hello image publishers.</span></span>
2. <span data-ttu-id="6bb04-156">Belirli bir yayımcı varsa yayımcının tekliflerini listeleyin.</span><span class="sxs-lookup"><span data-stu-id="6bb04-156">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="6bb04-157">Belirli bir teklif varsa SKU’larını listeleyin.</span><span class="sxs-lookup"><span data-stu-id="6bb04-157">For a given offer, list their SKUs.</span></span>

<span data-ttu-id="6bb04-158">İlk olarak, aşağıdaki komutları hello ile hello yayımcılar listesi:</span><span class="sxs-lookup"><span data-stu-id="6bb04-158">First, list hello publishers with hello following commands:</span></span>

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

<span data-ttu-id="6bb04-159">Seçilen yayımcı adınızı doldurmanız ve hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6bb04-159">Fill in your chosen publisher name and run hello following commands:</span></span>

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="6bb04-160">Seçilen teklif adınızı doldurun ve hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6bb04-160">Fill in your chosen offer name and run hello following commands:</span></span>

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="6bb04-161">Merhaba, hello çıktısından `Get-AzureRMVMImageSku` komut, tüm hello bilgilerin için yeni bir sanal makine toospecify hello görüntü gerekir.</span><span class="sxs-lookup"><span data-stu-id="6bb04-161">From hello output of hello `Get-AzureRMVMImageSku` command, you have all hello information you need toospecify hello image for a new virtual machine.</span></span>

<span data-ttu-id="6bb04-162">Merhaba aşağıdaki tam bir örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="6bb04-162">hello following shows a full example:</span></span>

```powershell
$locName="West US"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

```

<span data-ttu-id="6bb04-163">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="6bb04-163">Output:</span></span>

```
PublisherName
-------------
a10networks
aiscaler-cache-control-ddos-and-url-rewriting-
alertlogic
AlertLogic.Extension
Barracuda.Azure.ConnectivityAgent
barracudanetworks
basho
boxless
bssw
Canonical
...
```

<span data-ttu-id="6bb04-164">Merhaba "MicrosoftWindowsServer" publisher için:</span><span class="sxs-lookup"><span data-stu-id="6bb04-164">For hello "MicrosoftWindowsServer" publisher:</span></span>

```powershell
$pubName="MicrosoftWindowsServer"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="6bb04-165">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="6bb04-165">Output:</span></span>

```
Offer
-----
Windows-HUB
WindowsServer
WindowsServer-HUB
```

<span data-ttu-id="6bb04-166">"Windows Server" Merhaba sunar:</span><span class="sxs-lookup"><span data-stu-id="6bb04-166">For hello "WindowsServer" offer:</span></span>

```powershell
$offerName="WindowsServer"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="6bb04-167">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="6bb04-167">Output:</span></span>

```
Skus
----
2008-R2-SP1
2008-R2-SP1-smalldisk
2012-Datacenter
2012-Datacenter-smalldisk
2012-R2-Datacenter
2012-R2-Datacenter-smalldisk
2016-Datacenter
2016-Datacenter-Server-Core
2016-Datacenter-Server-Core-smalldisk
2016-Datacenter-smalldisk
2016-Datacenter-with-Containers
2016-Nano-Server
```

<span data-ttu-id="6bb04-168">Bu listeden SKU Adı Seçilen hello kopyalayın ve hello tüm hello bilgisine sahip `Set-AzureRMVMSourceImage` PowerShell cmdlet'ini veya bir kaynak grubu şablonu için.</span><span class="sxs-lookup"><span data-stu-id="6bb04-168">From this list, copy hello chosen SKU name, and you have all hello information for hello `Set-AzureRMVMSourceImage` PowerShell cmdlet or for a resource group template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6bb04-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6bb04-169">Next steps</span></span>
<span data-ttu-id="6bb04-170">Tam olarak hello görüntüsünü seçebilirsiniz artık toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="6bb04-170">Now you can choose precisely hello image you want toouse.</span></span> <span data-ttu-id="6bb04-171">yalnızca bulundu, hello görüntü bilgileri kullanarak hızlı bir şekilde bir sanal makine toocreate bkz [PowerShell ile Windows sanal makine oluşturma](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6bb04-171">toocreate a virtual machine quickly by using hello image information, which you just found, see [Create a Windows virtual machine with PowerShell](quick-create-powershell.md).</span></span>
