---
title: "Azure'da dağıtma Linux sanal makine sorunlarını giderme | Microsoft Docs"
description: "Azurethe Resource Manager dağıtım modelinde dağıtma Linux sanal makine sorunlarını giderin."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: genli
ms.openlocfilehash: 8bc9de90a49caf9155073caaa160585c6cc3728b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a><span data-ttu-id="f065f-103">Azure'da dağıtma Linux sanal makine sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="f065f-103">Troubleshoot deploying Linux virtual machine issues in Azure</span></span>

<span data-ttu-id="f065f-104">Azure'da sanal makine (VM) dağıtım sorunlarını gidermek için inceleyin [üst sorunları](#top-issues) yaygın hatalar ve çözümleri için.</span><span class="sxs-lookup"><span data-stu-id="f065f-104">To troubleshoot virtual machine (VM) deployment issues in Azure, review the [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="f065f-105">Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, üzerinde Azure uzmanlar başvurabilirsiniz [MSDN Azure ve yığın taşması forumları](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="f065f-105">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="f065f-106">Alternatif olarak, Azure destek olay dosya.</span><span class="sxs-lookup"><span data-stu-id="f065f-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="f065f-107">Git [Azure Destek sitesi](https://azure.microsoft.com/support/options/) seçip **alma desteği**.</span><span class="sxs-lookup"><span data-stu-id="f065f-107">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="f065f-108">Üst sorunları</span><span class="sxs-lookup"><span data-stu-id="f065f-108">Top issues</span></span>
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="the-cluster-cannot-support-the-requested-vm-size"></a><span data-ttu-id="f065f-109">Küme istenen VM boyutu desteklemiyor</span><span class="sxs-lookup"><span data-stu-id="f065f-109">The cluster cannot support the requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="f065f-110">Daha küçük bir VM boyutu kullanarak isteği yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="f065f-110">Retry the request using a smaller VM size.</span></span>
- <span data-ttu-id="f065f-111">İstenen VM boyutu değiştirilemiyorsa:</span><span class="sxs-lookup"><span data-stu-id="f065f-111">If the size of the requested VM cannot be changed:</span></span>
    - <span data-ttu-id="f065f-112">Kullanılabilirlik kümesindeki tüm sanal makineleri durdurun.</span><span class="sxs-lookup"><span data-stu-id="f065f-112">Stop all the VMs in the availability set.</span></span> <span data-ttu-id="f065f-113">Tıklatın **kaynak grupları** > kaynak grubunuz > **kaynakları** > kullanılabilirlik kümesi > **sanal makineleri** > sanal makineniz > **durdurmak**.</span><span class="sxs-lookup"><span data-stu-id="f065f-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="f065f-114">Tüm sanal makineleri durdurduktan sonra istenen boyutta VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f065f-114">After all the VMs stop, create the VM in the desired size.</span></span>
    - <span data-ttu-id="f065f-115">İlk olarak, yeni VM başlatmak ve durdurulmuş VM'lerin her birinde seçin ve Başlat'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f065f-115">Start the new VM first, and then select each of the stopped VMs and click Start.</span></span>


## <a name="the-cluster-does-not-have-free-resources"></a><span data-ttu-id="f065f-116">Küme kaynakları serbest bırakmak yok</span><span class="sxs-lookup"><span data-stu-id="f065f-116">The cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="f065f-117">İstek daha sonra yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="f065f-117">Retry the request later.</span></span>
- <span data-ttu-id="f065f-118">Yeni VM'yi farklı bir kullanılabilirlik kümesinin bir parçası olarak</span><span class="sxs-lookup"><span data-stu-id="f065f-118">If the new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="f065f-119">Farklı bir kullanılabilirlik (aynı bölgede) kümesindeki bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f065f-119">Create a VM in a different availability set (in the same region).</span></span>
    - <span data-ttu-id="f065f-120">Yeni VM aynı sanal ağa ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f065f-120">Add the new VM to the same virtual network.</span></span>

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="f065f-121">Visual studio Enterprise (BizSpark) için aylık my kredi nasıl etkinleştirilsin mi</span><span class="sxs-lookup"><span data-stu-id="f065f-121">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="f065f-122">Aylık kredinizin etkinleştirmek için bu bkz [makale](https://azure.microsoft.com/offers/ms-azr-0064p/).</span><span class="sxs-lookup"><span data-stu-id="f065f-122">To activate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="why-can-i-not-install-the-gpu-driver-for-an-ubuntu-nv-vm"></a><span data-ttu-id="f065f-123">Neden GPU sürücüsünün bir Ubuntu NV VM için yükleyebilir miyim değil mi?</span><span class="sxs-lookup"><span data-stu-id="f065f-123">Why can I not install the GPU driver for an Ubuntu NV VM?</span></span>

<span data-ttu-id="f065f-124">Linux GPU desteği şu anda yalnızca Azure NC Ubuntu Server 16.04 LTS çalıştıran Vm'lerinde olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f065f-124">Currently, Linux GPU support is only available on Azure NC VMs running Ubuntu Server 16.04 LTS.</span></span> <span data-ttu-id="f065f-125">Daha fazla bilgi için bkz: [GPU sürücüleri Linux çalıştıran N-serisi VM'ler için ayarlanmış](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="f065f-125">For more information, see [Set up GPU drivers for N-series VMs running Linux](n-series-driver-setup.md).</span></span>

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a><span data-ttu-id="f065f-126">My sürücüleri için Linux N-serisi VM'ime eksik</span><span class="sxs-lookup"><span data-stu-id="f065f-126">My drivers are missing for my Linux N-Series VM</span></span>

<span data-ttu-id="f065f-127">Linux tabanlı VM'ler için sürücülerin bulunduğu [burada](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="f065f-127">Drivers for Linux-based VMs are located [here](n-series-driver-setup.md).</span></span> 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="f065f-128">GPU örneği N-serisi VM'im içinde bulunamıyor</span><span class="sxs-lookup"><span data-stu-id="f065f-128">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="f065f-129">Windows Server 2016 veya Windows Server 2012 R2 çalıştıran Azure N-serisi VM'ler GPU yeteneklerinden yararlanabilmek için NVIDIA grafik sürücüleri dağıtımdan sonra her VM yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f065f-129">To take advantage of the GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="f065f-130">Sürücü Kurulum bilgileri yüklenebilir [Windows Vm'lerini](../windows/n-series-driver-setup.md) ve [Linux VM'ler](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="f065f-130">Driver setup information is available for [Windows VMs](../windows/n-series-driver-setup.md) and [Linux VMs](n-series-driver-setup.md).</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="f065f-131">N-serisi VM'ler bulunduğum bölgede var mı?</span><span class="sxs-lookup"><span data-stu-id="f065f-131">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="f065f-132">Kullanılabilirlik denetleyebilirsiniz [bölge tablosu tarafından kullanılabilen ürünler](https://azure.microsoft.com/regions/services)ve fiyatlandırma [burada](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span><span class="sxs-lookup"><span data-stu-id="f065f-132">You can check the availability from the [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="i-am-not-able-to-see-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="f065f-133">VM'im yeniden boyutlandırılırken istediğiniz VM boyutu ailesi görmeye değilim.</span><span class="sxs-lookup"><span data-stu-id="f065f-133">I am not able to see VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="f065f-134">Bir VM çalışırken, bir fiziksel sunucuya dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="f065f-134">When a VM is running, it is deployed to a physical server.</span></span> <span data-ttu-id="f065f-135">Fiziksel sunuculardan Azure bölgelerindeki ortak fiziksel donanım kümelerde gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="f065f-135">The physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="f065f-136">Farklı donanım kümelerine taşınacak VM gerektiren bir VM'yi yeniden boyutlandırılırken hangi dağıtım modeli VM dağıtmak için kullanılan bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="f065f-136">Resizing a VM that requires the VM to be moved to different hardware clusters is different depending on which deployment model was used to deploy the VM.</span></span>

- <span data-ttu-id="f065f-137">Klasik dağıtım modeli, bulut hizmeti dağıtımı dağıtılan VM'ler kaldırıldı ve sanal makineleri başka bir boyutu ailesindeki bir boyutu değiştirmek için imzalanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f065f-137">VMs deployed in Classic deployment model, the cloud service deployment must be removed and redeployed to change the VMs to a size in another size family.</span></span>

- <span data-ttu-id="f065f-138">Resource Manager dağıtım modelinde dağıtılan VM'ler, tüm sanal makineleri kullanılabilirlik kullanılabilirlik kümesindeki herhangi bir VM boyutunu değiştirmeden önce kümesini durdurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f065f-138">VMs deployed in Resource Manager deployment model, you must stop all VMs in the availability set before changing the size of any VM in the availability set.</span></span>

## <a name="the-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="f065f-139">Listelenen VM boyutu kullanılabilirlik kümesinde dağıtırken desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="f065f-139">The listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="f065f-140">Kullanılabilirlik kümesinin kümede desteklenen bir boyutu seçin.</span><span class="sxs-lookup"><span data-stu-id="f065f-140">Choose a size that is supported on the availability set's cluster.</span></span> <span data-ttu-id="f065f-141">Bir kullanılabilirlik ilk dağıtımınızı kullanılabilirlik kümesi olması gerekir ve sahip düşündüğünüz en büyük VM boyutu seçmek için kümesi oluştururken önerilir.</span><span class="sxs-lookup"><span data-stu-id="f065f-141">It is recommended when creating an availability set to choose the largest VM size you think you need, and have that be your first deployment to the Availability set.</span></span>

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a><span data-ttu-id="f065f-142">Hangi Linux dağıtımları/sürümleri, Azure üzerinde desteklenir?</span><span class="sxs-lookup"><span data-stu-id="f065f-142">What Linux distributions/versions are supported on Azure?</span></span>

<span data-ttu-id="f065f-143">Linux listesini bulabilirsiniz [Azure-Endorsed dağıtımları](endorsed-distros.md).</span><span class="sxs-lookup"><span data-stu-id="f065f-143">You can find the list at Linux on [Azure-Endorsed Distributions](endorsed-distros.md).</span></span>

## <a name="can-i-add-an-existing-classic-vm-to-an-availability-set"></a><span data-ttu-id="f065f-144">Mevcut bir Klasik VM'yi bir kullanılabilirlik kümesi ekleyebilir miyim?</span><span class="sxs-lookup"><span data-stu-id="f065f-144">Can I add an existing Classic VM to an availability set?</span></span>

<span data-ttu-id="f065f-145">Evet.</span><span class="sxs-lookup"><span data-stu-id="f065f-145">Yes.</span></span> <span data-ttu-id="f065f-146">Mevcut bir Klasik VM'yi bir yeni veya var olan kullanılabilirlik kümesine ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f065f-146">You can add an existing classic VM to a new or existing Availability Set.</span></span> <span data-ttu-id="f065f-147">Daha fazla bilgi için bkz: [var olan bir sanal makine bir kullanılabilirlik kümesine ekleme](../windows/classic/configure-availability.md#addmachine).</span><span class="sxs-lookup"><span data-stu-id="f065f-147">For more information see [Add an existing virtual machine to an availability set](../windows/classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="f065f-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f065f-148">Next steps</span></span>
<span data-ttu-id="f065f-149">Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, üzerinde Azure uzmanlar başvurabilirsiniz [MSDN Azure ve yığın taşması forumları](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="f065f-149">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="f065f-150">Alternatif olarak, Azure destek olay dosya.</span><span class="sxs-lookup"><span data-stu-id="f065f-150">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="f065f-151">Git [Azure Destek sitesi](https://azure.microsoft.com/support/options/) seçip **alma desteği**.</span><span class="sxs-lookup"><span data-stu-id="f065f-151">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
