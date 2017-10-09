---
title: "azure'da Windows sanal makine sorunlarını dağıtma aaaTroubleshoot | Microsoft Docs"
description: "Azurethe Resource Manager dağıtım modelinde dağıtma Windows sanal makine sorunlarını giderin."
services: virtual-machines-windows
documentationcenter: 
author: genlin
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
ms.openlocfilehash: 30de25827c050cc266761cfc14548bcc64237dac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-windows-virtual-machine-issues-in-azure"></a><span data-ttu-id="b61d2-103">Azure'da dağıtma Windows sanal makine sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="b61d2-103">Troubleshoot deploying Windows virtual machine issues in Azure</span></span>

<span data-ttu-id="b61d2-104">tootroubleshoot sanal makine (VM) dağıtım sorunları, azure'da hello gözden [üst sorunları](#top-issues) yaygın hatalar ve çözümleri için.</span><span class="sxs-lookup"><span data-stu-id="b61d2-104">tootroubleshoot virtual machine (VM) deployment issues in Azure, review hello [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="b61d2-105">Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz üzerinde Azure uzmanlar hello [MSDN Azure ve yığın taşması forumları hello](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="b61d2-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="b61d2-106">Alternatif olarak, Azure destek olay dosya.</span><span class="sxs-lookup"><span data-stu-id="b61d2-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="b61d2-107">Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/support/options/) seçip **alma desteği**.</span><span class="sxs-lookup"><span data-stu-id="b61d2-107">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="b61d2-108">Üst sorunları</span><span class="sxs-lookup"><span data-stu-id="b61d2-108">Top issues</span></span>
[!INCLUDE [virtual-machines-windows-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a><span data-ttu-id="b61d2-109">Merhaba küme destekleyemez hello istenen VM boyutu</span><span class="sxs-lookup"><span data-stu-id="b61d2-109">hello cluster cannot support hello requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="b61d2-110">Daha küçük bir VM boyutu kullanarak hello isteği yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="b61d2-110">Retry hello request using a smaller VM size.</span></span>
- <span data-ttu-id="b61d2-111">Merhaba, hello VM değiştirilemez istenen boyut:</span><span class="sxs-lookup"><span data-stu-id="b61d2-111">If hello size of hello requested VM cannot be changed:</span></span>
    - <span data-ttu-id="b61d2-112">Merhaba kullanılabilirlik kümesindeki tüm hello VM'ler durdurun.</span><span class="sxs-lookup"><span data-stu-id="b61d2-112">Stop all hello VMs in hello availability set.</span></span> <span data-ttu-id="b61d2-113">Tıklatın **kaynak grupları** > kaynak grubunuz > **kaynakları** > kullanılabilirlik kümesi > **sanal makineleri** > sanal makineniz > **durdurmak**.</span><span class="sxs-lookup"><span data-stu-id="b61d2-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="b61d2-114">Tüm VM'ler Dur Merhaba, istenen hello boyutunda hello VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b61d2-114">After all hello VMs stop, create hello VM in hello desired size.</span></span>
    - <span data-ttu-id="b61d2-115">Başlangıç yeni VM ilk hello ve ardından hello teker VM'ler durduruldu ve Başlat'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b61d2-115">Start hello new VM first, and then select each of hello stopped VMs and click Start.</span></span>


## <a name="hello-cluster-does-not-have-free-resources"></a><span data-ttu-id="b61d2-116">Merhaba küme kaynakları serbest bırakmak yok</span><span class="sxs-lookup"><span data-stu-id="b61d2-116">hello cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="b61d2-117">Merhaba isteği daha sonra yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="b61d2-117">Retry hello request later.</span></span>
- <span data-ttu-id="b61d2-118">Merhaba yeni VM yapabiliyorsanız, farklı bir kullanılabilirlik parçası ayarlanması</span><span class="sxs-lookup"><span data-stu-id="b61d2-118">If hello new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="b61d2-119">Farklı bir kullanılabilirlik kümesinde bir VM oluşturun (Merhaba içinde aynı bölge).</span><span class="sxs-lookup"><span data-stu-id="b61d2-119">Create a VM in a different availability set (in hello same region).</span></span>
    - <span data-ttu-id="b61d2-120">Merhaba yeni VM toohello eklemek aynı sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="b61d2-120">Add hello new VM toohello same virtual network.</span></span>

## <a name="how-can-i-use-and-deploy-a-windows-client-image-into-azure"></a><span data-ttu-id="b61d2-121">Nasıl kullanın ve windows istemci görüntüsünü Azure'a dağıtabilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="b61d2-121">How can I use and deploy a windows client image into Azure?</span></span>

<span data-ttu-id="b61d2-122">Uygun bir Visual Studio (önceki adıyla MSDN) aboneliğiniz varsa, Windows 7, Windows 8 veya Windows 10 Azure üzerinde geliştirme ve test senaryoları için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b61d2-122">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios if you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> <span data-ttu-id="b61d2-123">Bu [makale](client-images.md) anahatları hello Azure galeri görüntüleri Windows İstemcisi Azure ve hello kullanımlarını çalıştırmak için uygunluk gereksinimler.</span><span class="sxs-lookup"><span data-stu-id="b61d2-123">This [article](client-images.md) outlines hello eligibility requirements for running Windows client in Azure and uses of hello Azure Gallery images.</span></span>

## <a name="how-can-i-deploy-a-virtual-machine-using-hello-hybrid-use-benefit-hub"></a><span data-ttu-id="b61d2-124">Merhaba karma kullanımı Avantajı (HUB) kullanarak bir sanal makine nasıl dağıtabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="b61d2-124">How can I deploy a virtual machine using hello Hybrid Use Benefit (HUB)?</span></span>

<span data-ttu-id="b61d2-125">Birkaç farklı şekilde toodeploy Windows sanal makinelerin hello Azure karma kullanımı avantajı vardır.</span><span class="sxs-lookup"><span data-stu-id="b61d2-125">There are a couple of different ways toodeploy Windows virtual machines with hello Azure Hybrid Use Benefit.</span></span>

<span data-ttu-id="b61d2-126">Bir Kurumsal Anlaşma abonelik için:</span><span class="sxs-lookup"><span data-stu-id="b61d2-126">For an Enterprise Agreement subscription:</span></span>

<span data-ttu-id="b61d2-127">• Azure karma kullanımı avantajı ile önceden yapılandırılmış belirli Market görüntülerden sanal makineleri dağıtma.</span><span class="sxs-lookup"><span data-stu-id="b61d2-127">•   Deploy VMs from specific Marketplace images that are pre-configured with Azure Hybrid Use Benefit.</span></span>

<span data-ttu-id="b61d2-128">Kurumsal Anlaşma için:</span><span class="sxs-lookup"><span data-stu-id="b61d2-128">For Enterprise agreement:</span></span>

<span data-ttu-id="b61d2-129">• Özel bir VM karşıya yükleyin ve bir Resource Manager şablonu veya Azure PowerShell kullanarak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="b61d2-129">•   Upload a custom VM and deploy using a Resource Manager template or Azure PowerShell.</span></span>

<span data-ttu-id="b61d2-130">Daha fazla bilgi için kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="b61d2-130">For more information, see hello following resources:</span></span>

 - [<span data-ttu-id="b61d2-131">Azure karma kullanımı avantajı genel bakış</span><span class="sxs-lookup"><span data-stu-id="b61d2-131">Azure Hybrid Use Benefit overview </span></span>](https://azure.microsoft.com/pricing/hybrid-use-benefit/)

 - [<span data-ttu-id="b61d2-132">İndirilebilir SSS</span><span class="sxs-lookup"><span data-stu-id="b61d2-132">Downloadable FAQ</span></span>](http://download.microsoft.com/download/4/2/1/4211AC94-D607-4A45-B472-4B30EDF437DE/Windows_Server_Azure_Hybrid_Use_FAQ_EN_US.pdf)

 - <span data-ttu-id="b61d2-133">[Windows Server ve Windows İstemcisi için Azure karma kullanımı avantajı](hybrid-use-benefit-licensing.md).</span><span class="sxs-lookup"><span data-stu-id="b61d2-133">[Azure Hybrid Use Benefit for Windows Server and Windows Client](hybrid-use-benefit-licensing.md).</span></span>

 - [<span data-ttu-id="b61d2-134">Azure'da hello karma kullanma avantajını nasıl kullanabilirim</span><span class="sxs-lookup"><span data-stu-id="b61d2-134">How can I use hello Hybrid Use Benefit in Azure</span></span>](https://blogs.msdn.microsoft.com/azureedu/2016/04/13/how-can-i-use-the-hybrid-use-benefit-in-azure)

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="b61d2-135">Visual studio Enterprise (BizSpark) için aylık my kredi nasıl etkinleştirilsin mi</span><span class="sxs-lookup"><span data-stu-id="b61d2-135">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="b61d2-136">tooactivate, aylık kredi, bu bkz [makale](https://azure.microsoft.com/offers/ms-azr-0064p/).</span><span class="sxs-lookup"><span data-stu-id="b61d2-136">tooactivate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="how-tooadd-enterprise-devtest-toomy-enterprise-agreement-ea-tooget-access-toowindow-client-images"></a><span data-ttu-id="b61d2-137">Nasıl tooadd Enterprise geliştirme ve Test toomy Kurumsal Anlaşma (Kurumsal Sözleşme) tooget tooWindow istemci görüntüleri erişim?</span><span class="sxs-lookup"><span data-stu-id="b61d2-137">How tooadd Enterprise Dev/Test toomy Enterprise Agreement (EA) tooget access tooWindow client images?</span></span>

<span data-ttu-id="b61d2-138">Enterprise geliştirme ve Test Hello üzerinde temel hello özelliği toocreate abonelikler sunma olduğu toodo izin verilen sınırlı tooAccount sahiplerine tarafından kuruluş yöneticisi bunu.</span><span class="sxs-lookup"><span data-stu-id="b61d2-138">hello ability toocreate subscriptions based on hello Enterprise Dev/Test offer is restricted tooAccount Owners who have been given permission toodo so by an Enterprise Administrator.</span></span> <span data-ttu-id="b61d2-139">Merhaba hesap sahibi hello Azure hesap Portalı aracılığıyla abonelikleri oluşturur ve ardından etkin Visual Studio abonelerinden ortak yönetici olarak eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b61d2-139">hello Account Owner creates subscriptions via hello Azure Account Portal, and then should add active Visual Studio subscribers as co-administrators.</span></span> <span data-ttu-id="b61d2-140">Yönetme ve geliştirme ve test için gerekli olan hello kaynaklarını kullanmak böylece.</span><span class="sxs-lookup"><span data-stu-id="b61d2-140">So that they can manage and use hello resources needed for development and testing.</span></span> <span data-ttu-id="b61d2-141">Daha fazla bilgi için bkz: [Enterprise geliştirme ve Test](https://azure.microsoft.com/offers/ms-azr-0148p/).</span><span class="sxs-lookup"><span data-stu-id="b61d2-141">For more information, see [Enterprise Dev/Test](https://azure.microsoft.com/offers/ms-azr-0148p/).</span></span>

## <a name="my-drivers-are-missing-for-my-windows-n-series-vm"></a><span data-ttu-id="b61d2-142">My sürücüleri için Windows N-serisi VM'ime eksik</span><span class="sxs-lookup"><span data-stu-id="b61d2-142">My drivers are missing for my Windows N-Series VM</span></span>

<span data-ttu-id="b61d2-143">Windows tabanlı VM'ler için sürücülerin bulunduğu [burada](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="b61d2-143">Drivers for Windows-based VMs are located [here](n-series-driver-setup.md).</span></span>

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="b61d2-144">GPU örneği N-serisi VM'im içinde bulunamıyor</span><span class="sxs-lookup"><span data-stu-id="b61d2-144">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="b61d2-145">tootake yeteneklerinden hello GPU Windows Server 2016 çalıştıran Azure N-serisi VM'lerin veya Windows Server 2012 R2, dağıtımdan sonra her VM NVIDIA grafik sürücüleri yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b61d2-145">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="b61d2-146">Sürücü Kurulum bilgileri yüklenebilir [Windows Vm'lerini](n-series-driver-setup.md) ve [Linux VM'ler](../linux/n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="b61d2-146">Driver setup information is available for [Windows VMs](n-series-driver-setup.md) and [Linux VMs](../linux/n-series-driver-setup.md).</span></span>

## <a name="are-client-images-supported-for-n-series"></a><span data-ttu-id="b61d2-147">İstemci görüntüleri N-seri için destekleniyor mu?</span><span class="sxs-lookup"><span data-stu-id="b61d2-147">Are client images supported for N-Series?</span></span>

<span data-ttu-id="b61d2-148">Şu anda Azure yalnızca Windows Server ve Linux işletim sistemlerini çalıştıran sanal makinelerin N-serisi destekler.</span><span class="sxs-lookup"><span data-stu-id="b61d2-148">Currently, Azure only supports N-Series on VMs running Windows Server and Linux operating systems.</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="b61d2-149">N-serisi VM'ler bulunduğum bölgede var mı?</span><span class="sxs-lookup"><span data-stu-id="b61d2-149">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="b61d2-150">Merhaba hello kullanılabilirlik denetleyebilirsiniz [bölge tablosu tarafından kullanılabilen ürünler](https://azure.microsoft.com/regions/services)ve fiyatlandırma [burada](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span><span class="sxs-lookup"><span data-stu-id="b61d2-150">You can check hello availability from hello [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="what-client-images-can-i-use-and-deploy-in-azure-and-how-tooi-get-them"></a><span data-ttu-id="b61d2-151">Hangi istemci görüntüleri ı kullanabilir ve Azure'da dağıtmak ve tooI nereden bunları?</span><span class="sxs-lookup"><span data-stu-id="b61d2-151">What client images can I use and deploy in Azure, and how tooI get them?</span></span>

<span data-ttu-id="b61d2-152">Windows 10 azure'da geliştirme ve test senaryoları için uygun bir Visual Studio (önceki adıyla MSDN) aboneliğiniz olması koşuluyla veya Windows 7, Windows 8 kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b61d2-152">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios provided you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> 

- <span data-ttu-id="b61d2-153">Windows 10 görüntüleri kullanılabilir içinde hello Azure galerisinden [uygun geliştirme ve test sunar](client-images.md#eligible-offers).</span><span class="sxs-lookup"><span data-stu-id="b61d2-153">Windows 10 images are available from hello Azure Gallery within [eligible dev/test offers](client-images.md#eligible-offers).</span></span> 
- <span data-ttu-id="b61d2-154">Visual Studio abonelerinden teklif herhangi bir türde içinde için de [yeterli hazırlayın ve oluşturun](prepare-for-upload-vhd-image.md) bir 64-bit Windows 7, Windows 8 veya Windows 10 görüntüsü ve ardından [tooAzure karşıya](upload-generalized-managed.md).</span><span class="sxs-lookup"><span data-stu-id="b61d2-154">Visual Studio subscribers within any type of offer can also [adequately prepare and create](prepare-for-upload-vhd-image.md) a 64-bit Windows 7, Windows 8, or Windows 10 image and then [upload tooAzure](upload-generalized-managed.md).</span></span> <span data-ttu-id="b61d2-155">Hello kullan sınırlı toodev ve test etkin Visual Studio aboneler tarafından kalır.</span><span class="sxs-lookup"><span data-stu-id="b61d2-155">hello use remains limited toodev/test by active Visual Studio subscribers.</span></span>

<span data-ttu-id="b61d2-156">Bu [makale](client-images.md) anahatları hello Azure galeri görüntüleri Windows İstemcisi Azure ve hello kullanımını çalıştırmak için uygunluk gereksinimler.</span><span class="sxs-lookup"><span data-stu-id="b61d2-156">This [article](client-images.md) outlines hello eligibility requirements for running Windows client in Azure and use of hello Azure Gallery images.</span></span>

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="b61d2-157">VM'im yeniden boyutlandırılırken istediğiniz mümkün toosee VM boyutu ailesi değil ben.</span><span class="sxs-lookup"><span data-stu-id="b61d2-157">I am not able toosee VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="b61d2-158">Bir VM çalışırken, dağıtılan tooa fiziksel sunucusu var.</span><span class="sxs-lookup"><span data-stu-id="b61d2-158">When a VM is running, it is deployed tooa physical server.</span></span> <span data-ttu-id="b61d2-159">Merhaba fiziksel sunucuları Azure bölgelerindeki ortak fiziksel donanım kümelerde gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="b61d2-159">hello physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="b61d2-160">Merhaba VM taşınmış toobe toodifferent donanım kümeleri gerektiren bir VM'yi yeniden boyutlandırılırken kullanılan toodeploy hello VM was bağlı olarak hangi dağıtım modeli farklıdır.</span><span class="sxs-lookup"><span data-stu-id="b61d2-160">Resizing a VM that requires hello VM toobe moved toodifferent hardware clusters is different depending on which deployment model was used toodeploy hello VM.</span></span>

- <span data-ttu-id="b61d2-161">Klasik dağıtım modeli hello bulut hizmeti dağıtımı dağıtılan VM'ler kaldırılmalıdır ve toochange hello VM'ler tooa boyutu başka bir boyutu ailesindeki imzalanmasını.</span><span class="sxs-lookup"><span data-stu-id="b61d2-161">VMs deployed in Classic deployment model, hello cloud service deployment must be removed and redeployed toochange hello VMs tooa size in another size family.</span></span>

- <span data-ttu-id="b61d2-162">Resource Manager dağıtım modelinde dağıtılan VM'ler hello kullanılabilirlik hello hello kullanılabilirlik kümesindeki herhangi bir VM boyutunu değiştirmeden önce kümesindeki tüm VM'ler durdurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b61d2-162">VMs deployed in Resource Manager deployment model, you must stop all VMs in hello availability set before changing hello size of any VM in hello availability set.</span></span>

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="b61d2-163">Merhaba listelenen VM boyutu kullanılabilirlik kümesinde dağıtırken desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="b61d2-163">hello listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="b61d2-164">Merhaba kullanılabilirlik kümesinin kümede desteklenen bir boyutu seçin.</span><span class="sxs-lookup"><span data-stu-id="b61d2-164">Choose a size that is supported on hello availability set's cluster.</span></span> <span data-ttu-id="b61d2-165">Kullanılabilirlik kümesi, ilk dağıtım toohello olması gerekir ve sahip düşündüğünüz toochoose hello en büyük VM boyutu kullanılabilirlik kümesi oluştururken önerilir.</span><span class="sxs-lookup"><span data-stu-id="b61d2-165">It is recommended when creating an availability set toochoose hello largest VM size you think you need, and have that be your first deployment toohello Availability set.</span></span>

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a><span data-ttu-id="b61d2-166">Varolan Klasik VM tooan kullanılabilirlik kümesini ekleyebilir miyim?</span><span class="sxs-lookup"><span data-stu-id="b61d2-166">Can I add an existing Classic VM tooan availability set?</span></span>

<span data-ttu-id="b61d2-167">Evet.</span><span class="sxs-lookup"><span data-stu-id="b61d2-167">Yes.</span></span> <span data-ttu-id="b61d2-168">Bir varolan Klasik VM tooa yeni ekleyebilir veya var olan kullanılabilirlik kümesi.</span><span class="sxs-lookup"><span data-stu-id="b61d2-168">You can add an existing classic VM tooa new or existing Availability Set.</span></span> <span data-ttu-id="b61d2-169">Daha fazla bilgi için bkz: [ekleme varolan bir sanal makine tooan kullanılabilirlik kümesini](classic/configure-availability.md#addmachine).</span><span class="sxs-lookup"><span data-stu-id="b61d2-169">For more information see [Add an existing virtual machine tooan availability set](classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="b61d2-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b61d2-170">Next steps</span></span>
<span data-ttu-id="b61d2-171">Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz üzerinde Azure uzmanlar hello [MSDN Azure ve yığın taşması forumları hello](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="b61d2-171">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="b61d2-172">Alternatif olarak, Azure destek olay dosya.</span><span class="sxs-lookup"><span data-stu-id="b61d2-172">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="b61d2-173">Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/support/options/) seçip **alma desteği**.</span><span class="sxs-lookup"><span data-stu-id="b61d2-173">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
