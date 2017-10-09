---
title: "aaaTroubleshoot Azure Windows VM dağıtımı | Microsoft Docs"
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
ms.openlocfilehash: c27d4f63b67db2d1c9f117f05a2eba9ef130ef37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-when-creating-a-new-windows-vm-in-azure"></a><span data-ttu-id="c4eb5-103">Azure'da yeni bir Windows VM oluştururken, dağıtım sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="c4eb5-103">Troubleshoot deployment issues when creating a new Windows VM in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a><span data-ttu-id="c4eb5-104">Üst sorunları</span><span class="sxs-lookup"><span data-stu-id="c4eb5-104">Top issues</span></span>
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

<span data-ttu-id="c4eb5-105">Diğer VM Dağıtım sorunlar ve sorular için bkz: [azure'da dağıtma Windows sanal makine sorunlarını giderme](troubleshoot-deploy-vm.md).</span><span class="sxs-lookup"><span data-stu-id="c4eb5-105">For other VM deployment issues and questions, see [Troubleshoot deploying Windows virtual machine issues in Azure](troubleshoot-deploy-vm.md).</span></span>

## <a name="collect-activity-logs"></a><span data-ttu-id="c4eb5-106">Toplama etkinliklerini günlüğe kaydeder</span><span class="sxs-lookup"><span data-stu-id="c4eb5-106">Collect activity logs</span></span>
<span data-ttu-id="c4eb5-107">sorun giderme, toostart toplama hello etkinlik hello sorun ilişkili tooidentify hello hata günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="c4eb5-107">toostart troubleshooting, collect hello activity logs tooidentify hello error associated with hello issue.</span></span> <span data-ttu-id="c4eb5-108">Merhaba aşağıdaki bağlantılar hello işlem toofollow ilgili ayrıntılı bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="c4eb5-108">hello following links contain detailed information on hello process toofollow.</span></span>

[<span data-ttu-id="c4eb5-109">Dağıtım işlemlerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="c4eb5-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="c4eb5-110">Etkinlik günlükleri toomanage Azure görüntülemek kaynakları</span><span class="sxs-lookup"><span data-stu-id="c4eb5-110">View activity logs toomanage Azure resources</span></span>](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-windows-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="c4eb5-111">**Y:** hello işletim sistemi olan genelleştirilmiş, Windows ve bunu karşıya ve/veya hello ayarı genelleştirilmiş yakalanan durumunda hataları olmayacak.</span><span class="sxs-lookup"><span data-stu-id="c4eb5-111">**Y:** If hello OS is Windows generalized, and it is uploaded and/or captured with hello generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="c4eb5-112">Benzer şekilde, Hello işletim sistemi Windows özelleştirilmiş ve bunu karşıya ve/veya ile yakalanan ise hello ayarı, özelleştirilmiş olmayacaktır sonra herhangi bir hata.</span><span class="sxs-lookup"><span data-stu-id="c4eb5-112">Similarly, if hello OS is Windows specialized, and it is uploaded and/or captured with hello specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="c4eb5-113">**Karşıya yükleme hataları:**</span><span class="sxs-lookup"><span data-stu-id="c4eb5-113">**Upload Errors:**</span></span>

<span data-ttu-id="c4eb5-114">**N<sup>1</sup>:** hello OS genelleştirilmiş Windows olarak karşıya ise özelleştirilmiş, VM takılmış hello OOBE ekranında hello sağlama bir zaman aşımı hatasıyla karşılaşırsınız.</span><span class="sxs-lookup"><span data-stu-id="c4eb5-114">**N<sup>1</sup>:** If hello OS is Windows generalized, and it is uploaded as specialized, you will get a provisioning timeout error with hello VM stuck at hello OOBE screen.</span></span>

<span data-ttu-id="c4eb5-115">**N<sup>2</sup>:** hello işletim sistemi Windows özelleştirilmiş ve genelleştirilmiş gibi karşıya ise, VM takılmış hello OOBE ekranında hello yeni VM hello özgün bilgisayarla çalıştığından hello ile sağlama bir hata alırsınız adı, kullanıcı adı ve parolası.</span><span class="sxs-lookup"><span data-stu-id="c4eb5-115">**N<sup>2</sup>:** If hello OS is Windows specialized, and it is uploaded as generalized, you will get a provisioning failure error with hello VM stuck at hello OOBE screen because hello new VM is running with hello original computer name, username and password.</span></span>

<span data-ttu-id="c4eb5-116">**Çözümleme**</span><span class="sxs-lookup"><span data-stu-id="c4eb5-116">**Resolution**</span></span>

<span data-ttu-id="c4eb5-117">Her iki bu hataları tooresolve kullanın [Ekle AzureRmVhd tooupload hello özgün VHD](https://msdn.microsoft.com/library/mt603554.aspx), mevcut şirket içi, hello hello OS (genelleştirilmiş/özel) olarak aynı ayarı.</span><span class="sxs-lookup"><span data-stu-id="c4eb5-117">tooresolve both these errors, use [Add-AzureRmVhd tooupload hello original VHD](https://msdn.microsoft.com/library/mt603554.aspx), available on-premises, with hello same setting as that for hello OS (generalized/specialized).</span></span> <span data-ttu-id="c4eb5-118">Genelleştirilmiş gibi tooupload toorun sysprep ilk unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c4eb5-118">tooupload as generalized, remember toorun sysprep first.</span></span>

<span data-ttu-id="c4eb5-119">**Hata yakalama:**</span><span class="sxs-lookup"><span data-stu-id="c4eb5-119">**Capture Errors:**</span></span>

<span data-ttu-id="c4eb5-120">**N<sup>3</sup>:** hello OS genelleştirilmiş Windows olarak yakalanan ise genelleştirilmiş olarak işaretlenen gibi hello özgün VM kullanılabilir olmadığı için özelleştirilmiş, sağlama zaman aşımı hatası alırsınız.</span><span class="sxs-lookup"><span data-stu-id="c4eb5-120">**N<sup>3</sup>:** If hello OS is Windows generalized, and it is captured as specialized, you will get a provisioning timeout error because hello original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="c4eb5-121">**N<sup>4</sup>:** hello işletim sistemi Windows özelleştirilmiş ve genelleştirilmiş gibi yakalanan ise, hello yeni VM hello özgün bilgisayar adı, kullanıcı adı ve parola ile çalıştığı için sağlama bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="c4eb5-121">**N<sup>4</sup>:** If hello OS is Windows specialized, and it is captured as generalized, you will get a provisioning failure error because hello new VM is running with hello original computer name, username, and password.</span></span> <span data-ttu-id="c4eb5-122">İşaretlendiğinden ayrıca hello özgün VM kullanılamaz olarak özelleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="c4eb5-122">Also, hello original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="c4eb5-123">**Çözümleme**</span><span class="sxs-lookup"><span data-stu-id="c4eb5-123">**Resolution**</span></span>

<span data-ttu-id="c4eb5-124">tooresolve hem bu hataları hello geçerli görüntü hello Portalı'ndan silmek ve [hello yeniden yakalar geçerli VHD'leri](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ile Merhaba Merhaba OS (genelleştirilmiş/özel) ayarı aynı.</span><span class="sxs-lookup"><span data-stu-id="c4eb5-124">tooresolve both these errors, delete hello current image from hello portal, and [recapture it from hello current VHDs](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) with hello same setting as that for hello OS (generalized/specialized).</span></span>

## <a name="issue-customgallerymarketplace-image-allocation-failure"></a><span data-ttu-id="c4eb5-125">Sorun: Galeri/özel/Market görüntüsü; ayırma hatası</span><span class="sxs-lookup"><span data-stu-id="c4eb5-125">Issue: Custom/gallery/marketplace image; allocation failure</span></span>
<span data-ttu-id="c4eb5-126">Bu hata, istenen hello VM boyutu desteklemiyor veya kullanılabilir boş alanı tooaccommodate hello istekte sabitlenmiş tooa küme Hello yeni VM istek olduğunda durumlarda ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="c4eb5-126">This error arises in situations when hello new VM request is pinned tooa cluster that either cannot support hello VM size being requested, or does not have available free space tooaccommodate hello request.</span></span>

<span data-ttu-id="c4eb5-127">**1. neden:** hello küme destekleyemez hello istenen VM boyutu.</span><span class="sxs-lookup"><span data-stu-id="c4eb5-127">**Cause 1:** hello cluster cannot support hello requested VM size.</span></span>

<span data-ttu-id="c4eb5-128">**Çözüm 1:**</span><span class="sxs-lookup"><span data-stu-id="c4eb5-128">**Resolution 1:**</span></span>

* <span data-ttu-id="c4eb5-129">Daha küçük bir VM boyutu kullanarak hello isteği yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="c4eb5-129">Retry hello request using a smaller VM size.</span></span>
* <span data-ttu-id="c4eb5-130">Merhaba, hello VM değiştirilemez istenen boyut:</span><span class="sxs-lookup"><span data-stu-id="c4eb5-130">If hello size of hello requested VM cannot be changed:</span></span>
  * <span data-ttu-id="c4eb5-131">Merhaba kullanılabilirlik kümesindeki tüm hello VM'ler durdurun.</span><span class="sxs-lookup"><span data-stu-id="c4eb5-131">Stop all hello VMs in hello availability set.</span></span>
    <span data-ttu-id="c4eb5-132">Tıklatın **kaynak grupları** > *kaynak grubunuz* > **kaynakları** > *kullanılabilirlik kümesi* > **sanal makineleri** > *sanal makineniz* > **durdurmak**.</span><span class="sxs-lookup"><span data-stu-id="c4eb5-132">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  * <span data-ttu-id="c4eb5-133">Tüm sanal makineleri Dur hello sonra hello oluşturmak hello yeni VM istenen boyutu.</span><span class="sxs-lookup"><span data-stu-id="c4eb5-133">After all hello VMs stop, create hello new VM in hello desired size.</span></span>
  * <span data-ttu-id="c4eb5-134">Başlangıç yeni VM ilk hello ve hello teker tıklayın ve sanal makineleri durdu **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="c4eb5-134">Start hello new VM first, and then select each of hello stopped VMs and click **Start**.</span></span>

<span data-ttu-id="c4eb5-135">**Neden 2:** hello küme kaynakları serbest bırakmak sahip değil.</span><span class="sxs-lookup"><span data-stu-id="c4eb5-135">**Cause 2:** hello cluster does not have free resources.</span></span>

<span data-ttu-id="c4eb5-136">**Çözüm 2:**</span><span class="sxs-lookup"><span data-stu-id="c4eb5-136">**Resolution 2:**</span></span>

* <span data-ttu-id="c4eb5-137">Merhaba isteği daha sonra yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="c4eb5-137">Retry hello request at a later time.</span></span>
* <span data-ttu-id="c4eb5-138">Merhaba yeni VM yapabiliyorsanız, farklı bir kullanılabilirlik parçası ayarlanması</span><span class="sxs-lookup"><span data-stu-id="c4eb5-138">If hello new VM can be part of a different availability set</span></span>
  * <span data-ttu-id="c4eb5-139">Farklı bir kullanılabilirlik kümesinde yeni bir VM oluşturun (Merhaba içinde aynı bölge).</span><span class="sxs-lookup"><span data-stu-id="c4eb5-139">Create a new VM in a different availability set (in hello same region).</span></span>
  * <span data-ttu-id="c4eb5-140">Merhaba yeni VM toohello eklemek aynı sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="c4eb5-140">Add hello new VM toohello same virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4eb5-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c4eb5-141">Next steps</span></span>
<span data-ttu-id="c4eb5-142">Durdurulmuş bir Windows VM başlattığınızda veya varolan bir Windows VM Azure ile yeniden boyutlandırın sorunlarıyla karşılaşırsanız bkz [başlatma veya mevcut bir Windows sanal makine azure'da yeniden boyutlandırma ile ilgili sorunları giderme Resource Manager dağıtım sorunlarını](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c4eb5-142">If you encounter issues when you start a stopped Windows VM or resize an existing Windows VM in Azure, see [Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

