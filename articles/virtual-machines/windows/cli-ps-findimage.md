---
title: "Windows VM görüntüleri seçin | Microsoft Docs"
description: "Yayımcı, teklif, SKU ve sürümü Market VM görüntüleri belirlemek için Azure PowerSHell kullanmayı öğrenin."
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
ms.openlocfilehash: 814ae260123c045d4b6766bf4b312f874cd77068
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-find-windows-vm-images-in-the-azure-marketplace-with-azure-powershell"></a><span data-ttu-id="221f1-103">Azure PowerShell ile Azure Market'te Windows VM görüntüleri bulma</span><span class="sxs-lookup"><span data-stu-id="221f1-103">How to find Windows VM images in the Azure Marketplace with Azure PowerShell</span></span>

<span data-ttu-id="221f1-104">Bu konuda, Azure Marketi'nde VM görüntüleri bulmak için Azure PowerShell kullanmayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="221f1-104">This topic describes how to use Azure PowerShell to find VM images in the Azure Marketplace.</span></span> <span data-ttu-id="221f1-105">Bir Windows VM oluşturduğunuzda bir Market görüntüsü belirtmek için bu bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="221f1-105">Use this information to specify a Marketplace image when you create a Windows VM.</span></span>

<span data-ttu-id="221f1-106">Yüklü ve en son yapılandırıldığından emin olun [Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="221f1-106">Make sure that you installed and configured the latest [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>



## <a name="table-of-commonly-used-windows-images"></a><span data-ttu-id="221f1-107">Yaygın olarak kullanılan Windows görüntülerinin tablosu</span><span class="sxs-lookup"><span data-stu-id="221f1-107">Table of commonly used Windows images</span></span>
| <span data-ttu-id="221f1-108">PublisherName</span><span class="sxs-lookup"><span data-stu-id="221f1-108">PublisherName</span></span> | <span data-ttu-id="221f1-109">Sunduğu</span><span class="sxs-lookup"><span data-stu-id="221f1-109">Offer</span></span> | <span data-ttu-id="221f1-110">Sku</span><span class="sxs-lookup"><span data-stu-id="221f1-110">Sku</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="221f1-111">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="221f1-111">MicrosoftWindowsServer</span></span> |<span data-ttu-id="221f1-112">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="221f1-112">WindowsServer</span></span> |<span data-ttu-id="221f1-113">2016 Datacenter</span><span class="sxs-lookup"><span data-stu-id="221f1-113">2016-Datacenter</span></span> |
| <span data-ttu-id="221f1-114">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="221f1-114">MicrosoftWindowsServer</span></span> |<span data-ttu-id="221f1-115">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="221f1-115">WindowsServer</span></span> |<span data-ttu-id="221f1-116">Veri Merkezi Sunucu Çekirdek 2016</span><span class="sxs-lookup"><span data-stu-id="221f1-116">2016-Datacenter-Server-Core</span></span> |
| <span data-ttu-id="221f1-117">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="221f1-117">MicrosoftWindowsServer</span></span> |<span data-ttu-id="221f1-118">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="221f1-118">WindowsServer</span></span> |<span data-ttu-id="221f1-119">Kapsayıcılar ile 2016 Datacenter</span><span class="sxs-lookup"><span data-stu-id="221f1-119">2016-Datacenter-with-Containers</span></span> |
| <span data-ttu-id="221f1-120">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="221f1-120">MicrosoftWindowsServer</span></span> |<span data-ttu-id="221f1-121">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="221f1-121">WindowsServer</span></span> |<span data-ttu-id="221f1-122">2016 Nano Server</span><span class="sxs-lookup"><span data-stu-id="221f1-122">2016-Nano-Server</span></span> |
| <span data-ttu-id="221f1-123">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="221f1-123">MicrosoftWindowsServer</span></span> |<span data-ttu-id="221f1-124">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="221f1-124">WindowsServer</span></span> |<span data-ttu-id="221f1-125">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="221f1-125">2012-R2-Datacenter</span></span> |
| <span data-ttu-id="221f1-126">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="221f1-126">MicrosoftWindowsServer</span></span> |<span data-ttu-id="221f1-127">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="221f1-127">WindowsServer</span></span> |<span data-ttu-id="221f1-128">2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="221f1-128">2008-R2-SP1</span></span> |
| <span data-ttu-id="221f1-129">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="221f1-129">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="221f1-130">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="221f1-130">DynamicsNAV</span></span> |<span data-ttu-id="221f1-131">2017</span><span class="sxs-lookup"><span data-stu-id="221f1-131">2017</span></span> |
| <span data-ttu-id="221f1-132">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="221f1-132">MicrosoftSharePoint</span></span> |<span data-ttu-id="221f1-133">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="221f1-133">MicrosoftSharePointServer</span></span> |<span data-ttu-id="221f1-134">2016</span><span class="sxs-lookup"><span data-stu-id="221f1-134">2016</span></span> |
| <span data-ttu-id="221f1-135">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="221f1-135">MicrosoftSQLServer</span></span> |<span data-ttu-id="221f1-136">SQL2016 WS2016</span><span class="sxs-lookup"><span data-stu-id="221f1-136">SQL2016-WS2016</span></span> |<span data-ttu-id="221f1-137">Enterprise</span><span class="sxs-lookup"><span data-stu-id="221f1-137">Enterprise</span></span> |
| <span data-ttu-id="221f1-138">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="221f1-138">MicrosoftSQLServer</span></span> |<span data-ttu-id="221f1-139">SQL2014SP2 WS2012R2</span><span class="sxs-lookup"><span data-stu-id="221f1-139">SQL2014SP2-WS2012R2</span></span> |<span data-ttu-id="221f1-140">Enterprise</span><span class="sxs-lookup"><span data-stu-id="221f1-140">Enterprise</span></span> |
| <span data-ttu-id="221f1-141">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="221f1-141">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="221f1-142">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="221f1-142">WindowsServerHPCPack</span></span> |<span data-ttu-id="221f1-143">2012R2</span><span class="sxs-lookup"><span data-stu-id="221f1-143">2012R2</span></span> |
| <span data-ttu-id="221f1-144">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="221f1-144">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="221f1-145">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="221f1-145">WindowsServerEssentials</span></span> |<span data-ttu-id="221f1-146">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="221f1-146">WindowsServerEssentials</span></span> |

## <a name="find-specific-images"></a><span data-ttu-id="221f1-147">Belirli görüntüleri bulma</span><span class="sxs-lookup"><span data-stu-id="221f1-147">Find specific images</span></span>


<span data-ttu-id="221f1-148">Azure Resource Manager ile yeni bir sanal makine oluştururken bazı durumlarda aşağıdaki görüntü özelliklerinin birleşimine sahip bir görüntü belirtmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="221f1-148">When creating a new virtual machine with Azure Resource Manager, in some cases you need to specify an image with the combination of the following image properties:</span></span>

* <span data-ttu-id="221f1-149">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="221f1-149">Publisher</span></span>
* <span data-ttu-id="221f1-150">Sunduğu</span><span class="sxs-lookup"><span data-stu-id="221f1-150">Offer</span></span>
* <span data-ttu-id="221f1-151">SKU</span><span class="sxs-lookup"><span data-stu-id="221f1-151">SKU</span></span>

<span data-ttu-id="221f1-152">Örneğin, bu değerler içeren kullanın [kümesi AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) PowerShell cmdlet'ini veya bir kaynak grubu şablonu içinde belirtmelisiniz oluşturulacak VM türü.</span><span class="sxs-lookup"><span data-stu-id="221f1-152">For example, use these values with the [Set-AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) PowerShell cmdlet, or with a resource group template in which you must specify the type of VM to be created.</span></span>

<span data-ttu-id="221f1-153">Bu değerleri belirlemek gerekiyorsa, çalıştırabilirsiniz [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), ve [Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) gitmek için cmdlet'leri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="221f1-153">If you need to determine these values, you can run the [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), and [Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlets to navigate the images.</span></span> <span data-ttu-id="221f1-154">Bu değerler belirler:</span><span class="sxs-lookup"><span data-stu-id="221f1-154">You determine these values:</span></span>

1. <span data-ttu-id="221f1-155">Görüntü yayımcılarını listeleyin.</span><span class="sxs-lookup"><span data-stu-id="221f1-155">List the image publishers.</span></span>
2. <span data-ttu-id="221f1-156">Belirli bir yayımcı varsa yayımcının tekliflerini listeleyin.</span><span class="sxs-lookup"><span data-stu-id="221f1-156">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="221f1-157">Belirli bir teklif varsa SKU’larını listeleyin.</span><span class="sxs-lookup"><span data-stu-id="221f1-157">For a given offer, list their SKUs.</span></span>

<span data-ttu-id="221f1-158">İlk olarak aşağıdaki komutlarla yayımcıları listeleyin:</span><span class="sxs-lookup"><span data-stu-id="221f1-158">First, list the publishers with the following commands:</span></span>

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

<span data-ttu-id="221f1-159">Seçtiğiniz yayımcı adını girin ve aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="221f1-159">Fill in your chosen publisher name and run the following commands:</span></span>

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="221f1-160">Seçtiğiniz teklif adını girin ve aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="221f1-160">Fill in your chosen offer name and run the following commands:</span></span>

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="221f1-161">Çıktısından `Get-AzureRMVMImageSku` komutu, sahip olduğunuz tüm bilgilerin görüntüsü yeni bir sanal makine için belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="221f1-161">From the output of the `Get-AzureRMVMImageSku` command, you have all the information you need to specify the image for a new virtual machine.</span></span>

<span data-ttu-id="221f1-162">Aşağıda tam bir örnek gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="221f1-162">The following shows a full example:</span></span>

```powershell
$locName="West US"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

```

<span data-ttu-id="221f1-163">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="221f1-163">Output:</span></span>

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

<span data-ttu-id="221f1-164">"MicrosoftWindowsServer" yayımcısı için:</span><span class="sxs-lookup"><span data-stu-id="221f1-164">For the "MicrosoftWindowsServer" publisher:</span></span>

```powershell
$pubName="MicrosoftWindowsServer"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="221f1-165">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="221f1-165">Output:</span></span>

```
Offer
-----
Windows-HUB
WindowsServer
WindowsServer-HUB
```

<span data-ttu-id="221f1-166">"WindowsServer" teklifi için:</span><span class="sxs-lookup"><span data-stu-id="221f1-166">For the "WindowsServer" offer:</span></span>

```powershell
$offerName="WindowsServer"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="221f1-167">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="221f1-167">Output:</span></span>

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

<span data-ttu-id="221f1-168">Bu listeden seçtiğiniz SKU adını kopyaladığınızda, `Set-AzureRMVMSourceImage` PowerShell cmdlet’i veya bir kaynak grubu şablonu için ihtiyacınız olan tüm bilgilere sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="221f1-168">From this list, copy the chosen SKU name, and you have all the information for the `Set-AzureRMVMSourceImage` PowerShell cmdlet or for a resource group template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="221f1-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="221f1-169">Next steps</span></span>
<span data-ttu-id="221f1-170">Artık tam olarak kullanmak istediğiniz görüntüyü seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="221f1-170">Now you can choose precisely the image you want to use.</span></span> <span data-ttu-id="221f1-171">Yalnızca bulundu, görüntü bilgileri kullanarak bir sanal makineyi hızlı bir şekilde oluşturmak için bkz: [PowerShell ile Windows sanal makine oluşturma](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="221f1-171">To create a virtual machine quickly by using the image information, which you just found, see [Create a Windows virtual machine with PowerShell](quick-create-powershell.md).</span></span>
