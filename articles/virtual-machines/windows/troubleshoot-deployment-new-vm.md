---
title: "Azure Windows VM dağıtımı sorunlarını giderme | Microsoft Docs"
description: "Azure'da yeni bir Windows sanal makine oluşturduğunuzda, Resource Manager dağıtım sorunlarını giderme"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: afc6c1a4-2769-41f6-bbf9-76f9f23bcdf4
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: cjiang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 86795ba6eab3505a3d539e4fc4e032bdeecc2e78
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-deployment-issues-when-creating-a-new-windows-vm-in-azure"></a><span data-ttu-id="e8827-103">Azure'da yeni bir Windows VM oluştururken, dağıtım sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="e8827-103">Troubleshoot deployment issues when creating a new Windows VM in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a><span data-ttu-id="e8827-104">Üst sorunları</span><span class="sxs-lookup"><span data-stu-id="e8827-104">Top issues</span></span>
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

<span data-ttu-id="e8827-105">Diğer VM Dağıtım sorunlar ve sorular için bkz: [azure'da dağıtma Windows sanal makine sorunlarını giderme](troubleshoot-deploy-vm.md).</span><span class="sxs-lookup"><span data-stu-id="e8827-105">For other VM deployment issues and questions, see [Troubleshoot deploying Windows virtual machine issues in Azure](troubleshoot-deploy-vm.md).</span></span>

## <a name="collect-activity-logs"></a><span data-ttu-id="e8827-106">Toplama etkinliklerini günlüğe kaydeder</span><span class="sxs-lookup"><span data-stu-id="e8827-106">Collect activity logs</span></span>
<span data-ttu-id="e8827-107">Sorun giderme başlatmak için sorunu ile ilişkili hata tanımlamak için etkinlik günlüklerini toplayın.</span><span class="sxs-lookup"><span data-stu-id="e8827-107">To start troubleshooting, collect the activity logs to identify the error associated with the issue.</span></span> <span data-ttu-id="e8827-108">Aşağıdaki bağlantıları izleyin işlemi ile ilgili ayrıntılı bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="e8827-108">The following links contain detailed information on the process to follow.</span></span>

[<span data-ttu-id="e8827-109">Dağıtım işlemlerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="e8827-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="e8827-110">Azure kaynaklarınızı yönetmek için etkinlik günlüklerini görüntüle</span><span class="sxs-lookup"><span data-stu-id="e8827-110">View activity logs to manage Azure resources</span></span>](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-windows-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="e8827-111">**Y:** genelleştirilmiş, Windows işletim sistemi olan ve bunu karşıya ve/veya genelleştirilmiş ayarıyla yakalanan durumunda hataları olmayacak.</span><span class="sxs-lookup"><span data-stu-id="e8827-111">**Y:** If the OS is Windows generalized, and it is uploaded and/or captured with the generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="e8827-112">Benzer şekilde, işletim sistemi ise Windows özelleştirilmiş ve bunu karşıya ve/veya özel ayarlarla yakalanan ardından hataları olmayacak.</span><span class="sxs-lookup"><span data-stu-id="e8827-112">Similarly, if the OS is Windows specialized, and it is uploaded and/or captured with the specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="e8827-113">**Karşıya yükleme hataları:**</span><span class="sxs-lookup"><span data-stu-id="e8827-113">**Upload Errors:**</span></span>

<span data-ttu-id="e8827-114">**N<sup>1</sup>:** genelleştirilmiş Windows işletim sistemi ise ve olarak karşıya özelleştirilmiş, OOBE ekranında takılmış VM ile bir sağlama zaman aşımı hatası alırsınız.</span><span class="sxs-lookup"><span data-stu-id="e8827-114">**N<sup>1</sup>:** If the OS is Windows generalized, and it is uploaded as specialized, you will get a provisioning timeout error with the VM stuck at the OOBE screen.</span></span>

<span data-ttu-id="e8827-115">**N<sup>2</sup>:** işletim sistemi Windows özelleştirilmiş ve genelleştirilmiş gibi karşıya varsa, yeni VM özgün bilgisayar adı, kullanıcı adı ve parola ile çalıştığı için OOBE ekranında takılmış VM ile sağlama bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="e8827-115">**N<sup>2</sup>:** If the OS is Windows specialized, and it is uploaded as generalized, you will get a provisioning failure error with the VM stuck at the OOBE screen because the new VM is running with the original computer name, username and password.</span></span>

<span data-ttu-id="e8827-116">**Çözümleme**</span><span class="sxs-lookup"><span data-stu-id="e8827-116">**Resolution**</span></span>

<span data-ttu-id="e8827-117">Her iki bu hataları gidermek için [özgün VHD yüklemek için Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx), mevcut şirket içi, işletim sistemi (genelleştirilmiş/özel) olarak aynı ayarı.</span><span class="sxs-lookup"><span data-stu-id="e8827-117">To resolve both these errors, use [Add-AzureRmVhd to upload the original VHD](https://msdn.microsoft.com/library/mt603554.aspx), available on-premises, with the same setting as that for the OS (generalized/specialized).</span></span> <span data-ttu-id="e8827-118">Genelleştirilmiş gibi karşıya yüklemek için öncelikle, sysprep çalıştırılamıyor unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e8827-118">To upload as generalized, remember to run sysprep first.</span></span>

<span data-ttu-id="e8827-119">**Hata yakalama:**</span><span class="sxs-lookup"><span data-stu-id="e8827-119">**Capture Errors:**</span></span>

<span data-ttu-id="e8827-120">**N<sup>3</sup>:** genelleştirilmiş Windows işletim sistemi ise ve olarak yakalanan orijinal VM kullanılabilir olmadığından genelleştirilmiş olarak işaretlenen gibi özelleştirilmiş, sağlama zaman aşımı hatası alırsınız.</span><span class="sxs-lookup"><span data-stu-id="e8827-120">**N<sup>3</sup>:** If the OS is Windows generalized, and it is captured as specialized, you will get a provisioning timeout error because the original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="e8827-121">**N<sup>4</sup>:** Windows özelleştirilmiş ve genelleştirilmiş gibi yakalanan işletim sistemi ise, yeni VM özgün bilgisayar adı, kullanıcı adı ve parola ile çalıştığı için sağlama bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="e8827-121">**N<sup>4</sup>:** If the OS is Windows specialized, and it is captured as generalized, you will get a provisioning failure error because the new VM is running with the original computer name, username, and password.</span></span> <span data-ttu-id="e8827-122">İşaretlendiğinden Ayrıca, orijinal VM kullanılamaz olarak özelleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="e8827-122">Also, the original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="e8827-123">**Çözümleme**</span><span class="sxs-lookup"><span data-stu-id="e8827-123">**Resolution**</span></span>

<span data-ttu-id="e8827-124">Her iki bu hataları gidermek için geçerli görüntü Portalı'ndan silmek ve [geçerli VHD'leri yeniden yakalar](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ayarıyla aynı olarak işletim sistemi (genelleştirilmiş/özel) için.</span><span class="sxs-lookup"><span data-stu-id="e8827-124">To resolve both these errors, delete the current image from the portal, and [recapture it from the current VHDs](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) with the same setting as that for the OS (generalized/specialized).</span></span>

## <a name="issue-customgallerymarketplace-image-allocation-failure"></a><span data-ttu-id="e8827-125">Sorun: Galeri/özel/Market görüntüsü; ayırma hatası</span><span class="sxs-lookup"><span data-stu-id="e8827-125">Issue: Custom/gallery/marketplace image; allocation failure</span></span>
<span data-ttu-id="e8827-126">Bu hata istenen VM boyutu desteklemiyor veya isteği gerçekleştirmek için kullanılabilir boş alan yok bir kümeye yeni VM isteği sabitlenmiş durumlarda oluşur.</span><span class="sxs-lookup"><span data-stu-id="e8827-126">This error arises in situations when the new VM request is pinned to a cluster that either cannot support the VM size being requested, or does not have available free space to accommodate the request.</span></span>

<span data-ttu-id="e8827-127">**1. neden:** küme istenen VM boyutu destekleyemez.</span><span class="sxs-lookup"><span data-stu-id="e8827-127">**Cause 1:** The cluster cannot support the requested VM size.</span></span>

<span data-ttu-id="e8827-128">**Çözüm 1:**</span><span class="sxs-lookup"><span data-stu-id="e8827-128">**Resolution 1:**</span></span>

* <span data-ttu-id="e8827-129">Daha küçük bir VM boyutu kullanarak isteği yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="e8827-129">Retry the request using a smaller VM size.</span></span>
* <span data-ttu-id="e8827-130">İstenen VM boyutu değiştirilemiyorsa:</span><span class="sxs-lookup"><span data-stu-id="e8827-130">If the size of the requested VM cannot be changed:</span></span>
  * <span data-ttu-id="e8827-131">Kullanılabilirlik kümesindeki tüm sanal makineleri durdurun.</span><span class="sxs-lookup"><span data-stu-id="e8827-131">Stop all the VMs in the availability set.</span></span>
    <span data-ttu-id="e8827-132">Tıklatın **kaynak grupları** > *kaynak grubunuz* > **kaynakları** > *kullanılabilirlik kümesi* > **sanal makineleri** > *sanal makineniz* > **durdurmak**.</span><span class="sxs-lookup"><span data-stu-id="e8827-132">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  * <span data-ttu-id="e8827-133">Tüm sanal makineleri durdurduktan sonra istenen boyutta yeni bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e8827-133">After all the VMs stop, create the new VM in the desired size.</span></span>
  * <span data-ttu-id="e8827-134">İlk olarak, yeni VM Başlat durdurulmuş VM'lerin her birinde seçin ve tıklatın **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="e8827-134">Start the new VM first, and then select each of the stopped VMs and click **Start**.</span></span>

<span data-ttu-id="e8827-135">**Neden 2:** küme kaynakları serbest bırakmak yok.</span><span class="sxs-lookup"><span data-stu-id="e8827-135">**Cause 2:** The cluster does not have free resources.</span></span>

<span data-ttu-id="e8827-136">**Çözüm 2:**</span><span class="sxs-lookup"><span data-stu-id="e8827-136">**Resolution 2:**</span></span>

* <span data-ttu-id="e8827-137">İstek daha sonra yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="e8827-137">Retry the request at a later time.</span></span>
* <span data-ttu-id="e8827-138">Yeni VM'yi farklı bir kullanılabilirlik kümesinin bir parçası olarak</span><span class="sxs-lookup"><span data-stu-id="e8827-138">If the new VM can be part of a different availability set</span></span>
  * <span data-ttu-id="e8827-139">Farklı bir kullanılabilirlik (aynı bölgede) kümesinde yeni bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e8827-139">Create a new VM in a different availability set (in the same region).</span></span>
  * <span data-ttu-id="e8827-140">Yeni VM aynı sanal ağa ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e8827-140">Add the new VM to the same virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8827-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e8827-141">Next steps</span></span>
<span data-ttu-id="e8827-142">Durdurulmuş bir Windows VM başlattığınızda veya varolan bir Windows VM Azure ile yeniden boyutlandırın sorunlarıyla karşılaşırsanız bkz [başlatma veya mevcut bir Windows sanal makine azure'da yeniden boyutlandırma ile ilgili sorunları giderme Resource Manager dağıtım sorunlarını](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e8827-142">If you encounter issues when you start a stopped Windows VM or resize an existing Windows VM in Azure, see [Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

