---
title: "azure'daki Linux sanal makine sorunlarını dağıtma aaaTroubleshoot | Microsoft Docs"
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
ms.openlocfilehash: d1092ca3d9d51af7510b19c8c9a79e6dda588697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a><span data-ttu-id="478c0-103">Azure'da dağıtma Linux sanal makine sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="478c0-103">Troubleshoot deploying Linux virtual machine issues in Azure</span></span>

<span data-ttu-id="478c0-104">tootroubleshoot sanal makine (VM) dağıtım sorunları, azure'da hello gözden [üst sorunları](#top-issues) yaygın hatalar ve çözümleri için.</span><span class="sxs-lookup"><span data-stu-id="478c0-104">tootroubleshoot virtual machine (VM) deployment issues in Azure, review hello [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="478c0-105">Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz üzerinde Azure uzmanlar hello [MSDN Azure ve yığın taşması forumları hello](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="478c0-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="478c0-106">Alternatif olarak, Azure destek olay dosya.</span><span class="sxs-lookup"><span data-stu-id="478c0-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="478c0-107">Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/support/options/) seçip **alma desteği**.</span><span class="sxs-lookup"><span data-stu-id="478c0-107">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="478c0-108">Üst sorunları</span><span class="sxs-lookup"><span data-stu-id="478c0-108">Top issues</span></span>
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a><span data-ttu-id="478c0-109">Merhaba küme destekleyemez hello istenen VM boyutu</span><span class="sxs-lookup"><span data-stu-id="478c0-109">hello cluster cannot support hello requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="478c0-110">Daha küçük bir VM boyutu kullanarak hello isteği yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="478c0-110">Retry hello request using a smaller VM size.</span></span>
- <span data-ttu-id="478c0-111">Merhaba, hello VM değiştirilemez istenen boyut:</span><span class="sxs-lookup"><span data-stu-id="478c0-111">If hello size of hello requested VM cannot be changed:</span></span>
    - <span data-ttu-id="478c0-112">Merhaba kullanılabilirlik kümesindeki tüm hello VM'ler durdurun.</span><span class="sxs-lookup"><span data-stu-id="478c0-112">Stop all hello VMs in hello availability set.</span></span> <span data-ttu-id="478c0-113">Tıklatın **kaynak grupları** > kaynak grubunuz > **kaynakları** > kullanılabilirlik kümesi > **sanal makineleri** > sanal makineniz > **durdurmak**.</span><span class="sxs-lookup"><span data-stu-id="478c0-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="478c0-114">Tüm VM'ler Dur Merhaba, istenen hello boyutunda hello VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="478c0-114">After all hello VMs stop, create hello VM in hello desired size.</span></span>
    - <span data-ttu-id="478c0-115">Başlangıç yeni VM ilk hello ve ardından hello teker VM'ler durduruldu ve Başlat'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="478c0-115">Start hello new VM first, and then select each of hello stopped VMs and click Start.</span></span>


## <a name="hello-cluster-does-not-have-free-resources"></a><span data-ttu-id="478c0-116">Merhaba küme kaynakları serbest bırakmak yok</span><span class="sxs-lookup"><span data-stu-id="478c0-116">hello cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="478c0-117">Merhaba isteği daha sonra yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="478c0-117">Retry hello request later.</span></span>
- <span data-ttu-id="478c0-118">Merhaba yeni VM yapabiliyorsanız, farklı bir kullanılabilirlik parçası ayarlanması</span><span class="sxs-lookup"><span data-stu-id="478c0-118">If hello new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="478c0-119">Farklı bir kullanılabilirlik kümesinde bir VM oluşturun (Merhaba içinde aynı bölge).</span><span class="sxs-lookup"><span data-stu-id="478c0-119">Create a VM in a different availability set (in hello same region).</span></span>
    - <span data-ttu-id="478c0-120">Merhaba yeni VM toohello eklemek aynı sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="478c0-120">Add hello new VM toohello same virtual network.</span></span>

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="478c0-121">Visual studio Enterprise (BizSpark) için aylık my kredi nasıl etkinleştirilsin mi</span><span class="sxs-lookup"><span data-stu-id="478c0-121">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="478c0-122">tooactivate, aylık kredi, bu bkz [makale](https://azure.microsoft.com/offers/ms-azr-0064p/).</span><span class="sxs-lookup"><span data-stu-id="478c0-122">tooactivate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="why-can-i-not-install-hello-gpu-driver-for-an-ubuntu-nv-vm"></a><span data-ttu-id="478c0-123">Neden hello GPU sürücüsünün bir Ubuntu NV VM için yükleyebilir miyim değil mi?</span><span class="sxs-lookup"><span data-stu-id="478c0-123">Why can I not install hello GPU driver for an Ubuntu NV VM?</span></span>

<span data-ttu-id="478c0-124">Linux GPU desteği şu anda yalnızca Azure NC Ubuntu Server 16.04 LTS çalıştıran Vm'lerinde olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="478c0-124">Currently, Linux GPU support is only available on Azure NC VMs running Ubuntu Server 16.04 LTS.</span></span> <span data-ttu-id="478c0-125">Daha fazla bilgi için bkz: [GPU sürücüleri Linux çalıştıran N-serisi VM'ler için ayarlanmış](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="478c0-125">For more information, see [Set up GPU drivers for N-series VMs running Linux](n-series-driver-setup.md).</span></span>

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a><span data-ttu-id="478c0-126">My sürücüleri için Linux N-serisi VM'ime eksik</span><span class="sxs-lookup"><span data-stu-id="478c0-126">My drivers are missing for my Linux N-Series VM</span></span>

<span data-ttu-id="478c0-127">Linux tabanlı VM'ler için sürücülerin bulunduğu [burada](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="478c0-127">Drivers for Linux-based VMs are located [here](n-series-driver-setup.md).</span></span> 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="478c0-128">GPU örneği N-serisi VM'im içinde bulunamıyor</span><span class="sxs-lookup"><span data-stu-id="478c0-128">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="478c0-129">tootake yeteneklerinden hello GPU Windows Server 2016 çalıştıran Azure N-serisi VM'lerin veya Windows Server 2012 R2, dağıtımdan sonra her VM NVIDIA grafik sürücüleri yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="478c0-129">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="478c0-130">Sürücü Kurulum bilgileri yüklenebilir [Windows Vm'lerini](../windows/n-series-driver-setup.md) ve [Linux VM'ler](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="478c0-130">Driver setup information is available for [Windows VMs](../windows/n-series-driver-setup.md) and [Linux VMs](n-series-driver-setup.md).</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="478c0-131">N-serisi VM'ler bulunduğum bölgede var mı?</span><span class="sxs-lookup"><span data-stu-id="478c0-131">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="478c0-132">Merhaba hello kullanılabilirlik denetleyebilirsiniz [bölge tablosu tarafından kullanılabilen ürünler](https://azure.microsoft.com/regions/services)ve fiyatlandırma [burada](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span><span class="sxs-lookup"><span data-stu-id="478c0-132">You can check hello availability from hello [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="478c0-133">VM'im yeniden boyutlandırılırken istediğiniz mümkün toosee VM boyutu ailesi değil ben.</span><span class="sxs-lookup"><span data-stu-id="478c0-133">I am not able toosee VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="478c0-134">Bir VM çalışırken, dağıtılan tooa fiziksel sunucusu var.</span><span class="sxs-lookup"><span data-stu-id="478c0-134">When a VM is running, it is deployed tooa physical server.</span></span> <span data-ttu-id="478c0-135">Merhaba fiziksel sunucuları Azure bölgelerindeki ortak fiziksel donanım kümelerde gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="478c0-135">hello physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="478c0-136">Merhaba VM taşınmış toobe toodifferent donanım kümeleri gerektiren bir VM'yi yeniden boyutlandırılırken kullanılan toodeploy hello VM was bağlı olarak hangi dağıtım modeli farklıdır.</span><span class="sxs-lookup"><span data-stu-id="478c0-136">Resizing a VM that requires hello VM toobe moved toodifferent hardware clusters is different depending on which deployment model was used toodeploy hello VM.</span></span>

- <span data-ttu-id="478c0-137">Klasik dağıtım modeli hello bulut hizmeti dağıtımı dağıtılan VM'ler kaldırılmalıdır ve toochange hello VM'ler tooa boyutu başka bir boyutu ailesindeki imzalanmasını.</span><span class="sxs-lookup"><span data-stu-id="478c0-137">VMs deployed in Classic deployment model, hello cloud service deployment must be removed and redeployed toochange hello VMs tooa size in another size family.</span></span>

- <span data-ttu-id="478c0-138">Resource Manager dağıtım modelinde dağıtılan VM'ler hello kullanılabilirlik hello hello kullanılabilirlik kümesindeki herhangi bir VM boyutunu değiştirmeden önce kümesindeki tüm VM'ler durdurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="478c0-138">VMs deployed in Resource Manager deployment model, you must stop all VMs in hello availability set before changing hello size of any VM in hello availability set.</span></span>

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="478c0-139">Merhaba listelenen VM boyutu kullanılabilirlik kümesinde dağıtırken desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="478c0-139">hello listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="478c0-140">Merhaba kullanılabilirlik kümesinin kümede desteklenen bir boyutu seçin.</span><span class="sxs-lookup"><span data-stu-id="478c0-140">Choose a size that is supported on hello availability set's cluster.</span></span> <span data-ttu-id="478c0-141">Kullanılabilirlik kümesi, ilk dağıtım toohello olması gerekir ve sahip düşündüğünüz toochoose hello en büyük VM boyutu kullanılabilirlik kümesi oluştururken önerilir.</span><span class="sxs-lookup"><span data-stu-id="478c0-141">It is recommended when creating an availability set toochoose hello largest VM size you think you need, and have that be your first deployment toohello Availability set.</span></span>

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a><span data-ttu-id="478c0-142">Hangi Linux dağıtımları/sürümleri, Azure üzerinde desteklenir?</span><span class="sxs-lookup"><span data-stu-id="478c0-142">What Linux distributions/versions are supported on Azure?</span></span>

<span data-ttu-id="478c0-143">Linux hello listesini bulabilirsiniz [Azure-Endorsed dağıtımları](endorsed-distros.md).</span><span class="sxs-lookup"><span data-stu-id="478c0-143">You can find hello list at Linux on [Azure-Endorsed Distributions](endorsed-distros.md).</span></span>

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a><span data-ttu-id="478c0-144">Varolan Klasik VM tooan kullanılabilirlik kümesini ekleyebilir miyim?</span><span class="sxs-lookup"><span data-stu-id="478c0-144">Can I add an existing Classic VM tooan availability set?</span></span>

<span data-ttu-id="478c0-145">Evet.</span><span class="sxs-lookup"><span data-stu-id="478c0-145">Yes.</span></span> <span data-ttu-id="478c0-146">Bir varolan Klasik VM tooa yeni ekleyebilir veya var olan kullanılabilirlik kümesi.</span><span class="sxs-lookup"><span data-stu-id="478c0-146">You can add an existing classic VM tooa new or existing Availability Set.</span></span> <span data-ttu-id="478c0-147">Daha fazla bilgi için bkz: [ekleme varolan bir sanal makine tooan kullanılabilirlik kümesini](../windows/classic/configure-availability.md#addmachine).</span><span class="sxs-lookup"><span data-stu-id="478c0-147">For more information see [Add an existing virtual machine tooan availability set](../windows/classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="478c0-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="478c0-148">Next steps</span></span>
<span data-ttu-id="478c0-149">Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz üzerinde Azure uzmanlar hello [MSDN Azure ve yığın taşması forumları hello](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="478c0-149">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="478c0-150">Alternatif olarak, Azure destek olay dosya.</span><span class="sxs-lookup"><span data-stu-id="478c0-150">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="478c0-151">Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/support/options/) seçip **alma desteği**.</span><span class="sxs-lookup"><span data-stu-id="478c0-151">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
