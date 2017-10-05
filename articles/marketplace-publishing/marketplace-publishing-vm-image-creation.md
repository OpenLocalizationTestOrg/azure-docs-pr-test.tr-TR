---
title: "Bir sanal makine görüntüsü için Azure Marketi oluşturma | Microsoft Docs"
description: "Satın almak Azure Marketi başkaları için bir sanal makine görüntüsünün nasıl oluşturulacağı hakkında ayrıntılı yönergeler."
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 5c937b8e-e28d-4007-9fef-624046bca2ae
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 01/05/2017
ms.author: hascipio; v-divte
ms.openlocfilehash: 046ce7af40301014746c6aef07d08d81ab4adcc2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="guide-to-create-a-virtual-machine-image-for-the-azure-marketplace"></a><span data-ttu-id="8344c-103">Azure Market bir sanal makine görüntüsü oluşturmak için kılavuz</span><span class="sxs-lookup"><span data-stu-id="8344c-103">Guide to create a virtual machine image for the Azure Marketplace</span></span>
<span data-ttu-id="8344c-104">Bu makalede **2. adım**, sanal sabit Azure Marketi dağıtacağınız diskleri (VHD) hazırlama size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="8344c-104">This article, **Step 2**, walks you through preparing the virtual hard disks (VHDs) that you will deploy to the Azure Marketplace.</span></span> <span data-ttu-id="8344c-105">Vhd'lerinizi, sku'sunun temelidir.</span><span class="sxs-lookup"><span data-stu-id="8344c-105">Your VHDs are the foundation of your SKU.</span></span> <span data-ttu-id="8344c-106">İşlem, bir Windows tabanlı veya Linux tabanlı SKU olup sağlanmaktadır bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="8344c-106">The process differs depending on whether you are providing a Linux-based or Windows-based SKU.</span></span> <span data-ttu-id="8344c-107">Bu makalede her iki senaryoyu ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8344c-107">This article covers both scenarios.</span></span> <span data-ttu-id="8344c-108">Bu işlem ile paralel olarak gerçekleştirilebilir [hesap oluşturma ve kayıt][link-acct-creation].</span><span class="sxs-lookup"><span data-stu-id="8344c-108">This process can be performed in parallel with [Account creation and registration][link-acct-creation].</span></span>

## <a name="1-define-offers-and-skus"></a><span data-ttu-id="8344c-109">1. Teklifler ve SKU'ları tanımlayın</span><span class="sxs-lookup"><span data-stu-id="8344c-109">1. Define Offers and SKUs</span></span>
<span data-ttu-id="8344c-110">Bu bölümde, teklifleri ve ilişkili SKU'ları tanımlayın öğrenin.</span><span class="sxs-lookup"><span data-stu-id="8344c-110">In this section, you learn to define the offers and their associated SKUs.</span></span>

<span data-ttu-id="8344c-111">Teklif, tüm SKU'larının "üst öğesidir".</span><span class="sxs-lookup"><span data-stu-id="8344c-111">An offer is a "parent" to all of its SKUs.</span></span> <span data-ttu-id="8344c-112">Birden çok teklife sahip olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8344c-112">You can have multiple offers.</span></span> <span data-ttu-id="8344c-113">Tekliflerinizi nasıl yapılandıracağınıza siz karar verirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8344c-113">How you decide to structure your offers is up to you.</span></span> <span data-ttu-id="8344c-114">Bir teklif, hazırlamaya gönderilirken tüm SKU'larıyla birlikte gönderilir.</span><span class="sxs-lookup"><span data-stu-id="8344c-114">When an offer is pushed to staging, it is pushed along with all of its SKUs.</span></span> <span data-ttu-id="8344c-115">URL'de görünür olacağından, SKU tanımlayıcıları dikkatlice düşünün:</span><span class="sxs-lookup"><span data-stu-id="8344c-115">Carefully consider your SKU identifiers, because they will be visible in the URL:</span></span>

* <span data-ttu-id="8344c-116">Azure.com: http://azure.microsoft.com/marketplace/partners/ {PartnerNamespace} / {OfferIdentifier}-{SKUidentifier}</span><span class="sxs-lookup"><span data-stu-id="8344c-116">Azure.com: http://azure.microsoft.com/marketplace/partners/{PartnerNamespace}/{OfferIdentifier}-{SKUidentifier}</span></span>
* <span data-ttu-id="8344c-117">Azure Önizleme portalı: https://portal.azure.com/#gallery/ {PublisherNamespace}. {OfferIdentifier} {SKUIDdentifier}</span><span class="sxs-lookup"><span data-stu-id="8344c-117">Azure preview portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{SKUIDdentifier}</span></span>  

<span data-ttu-id="8344c-118">Bir SKU bir VM görüntüsü için ticari adıdır.</span><span class="sxs-lookup"><span data-stu-id="8344c-118">A SKU is the commercial name for a VM image.</span></span> <span data-ttu-id="8344c-119">Bir VM görüntüsü içeren bir işletim sistemi diski ve sıfır veya daha fazla veri diski.</span><span class="sxs-lookup"><span data-stu-id="8344c-119">A VM image contains one operating system disk and zero or more data disks.</span></span> <span data-ttu-id="8344c-120">Özünde, bir sanal makinenin tam depolama profilidir.</span><span class="sxs-lookup"><span data-stu-id="8344c-120">It is essentially the complete storage profile for a virtual machine.</span></span> <span data-ttu-id="8344c-121">Bir VHD her disk için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="8344c-121">One VHD is needed per disk.</span></span> <span data-ttu-id="8344c-122">Bile boş veri diskleri oluşturulacak bir VHD gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8344c-122">Even blank data disks require a VHD to be created.</span></span>

<span data-ttu-id="8344c-123">Kullandığınız işletim sisteminden bağımsız olarak yalnızca SKU için gereken en az sayıda veri diski ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8344c-123">Regardless of which operating system you use, add only the minimum number of data disks needed by the SKU.</span></span> <span data-ttu-id="8344c-124">Müşteriler görüntünün bir parçasını dağıtım zamanında disklerinin kaldırılamıyor ancak bunları ihtiyacınız varsa her zaman diskleri sırasında veya dağıtımdan sonra ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8344c-124">Customers cannot remove disks that are part of an image at the time of deployment but can always add disks during or after deployment if they need them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8344c-125">**Yeni bir görüntü sürümü disk sayısı değiştirmeyin.**</span><span class="sxs-lookup"><span data-stu-id="8344c-125">**Do not change disk count in a new image version.**</span></span> <span data-ttu-id="8344c-126">Veri diskleri görüntüdeki yeniden yapılandırmanız gerekir, yeni bir SKU tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="8344c-126">If you must reconfigure Data disks in the image, define a new SKU.</span></span> <span data-ttu-id="8344c-127">Yeni bir görüntü sürümü farklı bir disk sayıları ile yayımlama sonu yeni dağıtım olasılığı yeni görüntü sürümünü durumlarda ARM şablonları ve diğer senaryolar aracılığıyla çözümlerini otomatik ölçeklendirme, otomatik dağıtımlarının temel.</span><span class="sxs-lookup"><span data-stu-id="8344c-127">Publishing a new image version with different disk counts will have the potential of breaking new deployment based on the new image version in cases of auto-scaling, automatic deployments of solutions through ARM templates and other scenarios.</span></span>
>
>

### <a name="11-add-an-offer"></a><span data-ttu-id="8344c-128">1.1 bir teklif ekleyin</span><span class="sxs-lookup"><span data-stu-id="8344c-128">1.1 Add an offer</span></span>
1. <span data-ttu-id="8344c-129">Oturum [yayımlama portalında] [ link-pubportal] seller hesabınızı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="8344c-129">Sign in to the [Publishing Portal][link-pubportal] by using your seller account.</span></span>
2. <span data-ttu-id="8344c-130">Seçin **sanal makineleri** yayımlama portalında sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="8344c-130">Select the **Virtual Machines** tab of the Publishing Portal.</span></span> <span data-ttu-id="8344c-131">İstendiğinde giriş alanına teklif adınızı girin.</span><span class="sxs-lookup"><span data-stu-id="8344c-131">In the prompted entry field, enter your offer name.</span></span> <span data-ttu-id="8344c-132">Teklif adı genellikle ürün veya Azure Marketi'nde satmak için planlama hizmetin adıdır.</span><span class="sxs-lookup"><span data-stu-id="8344c-132">The offer name is typically the name of the product or service that you plan to sell in the Azure Marketplace.</span></span>
3. <span data-ttu-id="8344c-133">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="8344c-133">Select **Create**.</span></span>

### <a name="12-define-a-sku"></a><span data-ttu-id="8344c-134">1.2 bir SKU tanımlayın</span><span class="sxs-lookup"><span data-stu-id="8344c-134">1.2 Define a SKU</span></span>
<span data-ttu-id="8344c-135">Bir teklif ekledikten sonra SKU'ları tanımlayabilir ve gerekir.</span><span class="sxs-lookup"><span data-stu-id="8344c-135">After you have added an offer, you need to define and identify your SKUs.</span></span> <span data-ttu-id="8344c-136">Birden çok teklifleri olabilir ve her teklif birden çok SKU'ları altındaki olabilir.</span><span class="sxs-lookup"><span data-stu-id="8344c-136">You can have multiple offers, and each offer can have multiple SKUs under it.</span></span> <span data-ttu-id="8344c-137">Bir teklif, hazırlamaya gönderilirken tüm SKU'larıyla birlikte gönderilir.</span><span class="sxs-lookup"><span data-stu-id="8344c-137">When an offer is pushed to staging, it is pushed along with all of its SKUs.</span></span>

1. <span data-ttu-id="8344c-138">**Bir SKU ekleyin.**</span><span class="sxs-lookup"><span data-stu-id="8344c-138">**Add a SKU.**</span></span> <span data-ttu-id="8344c-139">SKU URL'SİNDE kullanılan bir tanımlayıcı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8344c-139">The SKU requires an identifier, which is used in the URL.</span></span> <span data-ttu-id="8344c-140">Tanımlayıcı yayımlama profili içinde benzersiz olmalıdır. ancak diğer yayımcı ile tanımlayıcı çakışma riski vardır.</span><span class="sxs-lookup"><span data-stu-id="8344c-140">The identifier must be unique within your publishing profile, but there is no risk of identifier collision with other publishers.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8344c-141">Teklif ve SKU tanımlayıcıları Market teklifi URL'de görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8344c-141">The offer and SKU identifiers are displayed in the offer URL in the Marketplace.</span></span>
   >
   >
2. <span data-ttu-id="8344c-142">**SKU için Özet açıklama ekleyin.**</span><span class="sxs-lookup"><span data-stu-id="8344c-142">**Add a summary description for your SKU.**</span></span> <span data-ttu-id="8344c-143">Özet açıklamaları, müşterilerin görebildiği olduğundan kolay okunabilir yapmanız.</span><span class="sxs-lookup"><span data-stu-id="8344c-143">Summary descriptions are visible to customers, so you should make them easily readable.</span></span> <span data-ttu-id="8344c-144">Bu bilgiler kadar "Hazırlama itme" aşamasında kilitli gerekmez.</span><span class="sxs-lookup"><span data-stu-id="8344c-144">This information does not need to be locked until the "Push to Staging" phase.</span></span> <span data-ttu-id="8344c-145">Bu aşamaya kadar bilgileri istediğiniz zaman düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8344c-145">Until then, you are free to edit it.</span></span>
3. <span data-ttu-id="8344c-146">Windows tabanlı SKU'lar kullanıyorsanız Windows Server'ın onaylanmış sürümlerini edinmek için önerilen bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="8344c-146">If you are using Windows-based SKUs, follow the suggested links to acquire the approved versions of Windows Server.</span></span>

## <a name="2-create-an-azure-compatible-vhd-linux-based"></a><span data-ttu-id="8344c-147">2. (Linux tabanlı) bir Azure uyumlu VHD oluşturma</span><span class="sxs-lookup"><span data-stu-id="8344c-147">2. Create an Azure-compatible VHD (Linux-based)</span></span>
<span data-ttu-id="8344c-148">Bu bölümde Azure Market Linux tabanlı VM görüntüsü oluşturmak için en iyi uygulamalar odaklanır.</span><span class="sxs-lookup"><span data-stu-id="8344c-148">This section focuses on best practices for creating a Linux-based VM image for the Azure Marketplace.</span></span> <span data-ttu-id="8344c-149">Adım adım kılavuz için aşağıdaki belgelere bakın: [oluşturma ve Linux işletim sistemini içeren bir Sanal Sabit Disk karşıya yükleme](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="8344c-149">For a step-by-step walkthrough, refer to the following documentation: [Creating and Uploading a Virtual Hard Disk that Contains the Linux Operating System](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

## <a name="3-create-an-azure-compatible-vhd-windows-based"></a><span data-ttu-id="8344c-150">3. (Windows tabanlı) bir Azure uyumlu VHD oluşturma</span><span class="sxs-lookup"><span data-stu-id="8344c-150">3. Create an Azure-compatible VHD (Windows-based)</span></span>
<span data-ttu-id="8344c-151">Bu bölüm, Windows Server için Azure Marketi tabanlı bir SKU oluşturmak için aşağıdaki adımları odaklanır.</span><span class="sxs-lookup"><span data-stu-id="8344c-151">This section focuses on the steps to create a SKU based on Windows Server for the Azure Marketplace.</span></span>

### <a name="31-ensure-that-you-are-using-the-correct-base-vhds"></a><span data-ttu-id="8344c-152">3.1 doğru temel VHD kullandığınızdan emin olun</span><span class="sxs-lookup"><span data-stu-id="8344c-152">3.1 Ensure that you are using the correct base VHDs</span></span>
<span data-ttu-id="8344c-153">İşletim sistemi VHD VM görüntüsü için Windows Server veya SQL Server içeren Azure onaylı temel görüntüde dayalı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8344c-153">The operating system VHD for your VM image must be based on an Azure-approved base image that contains Windows Server or SQL Server.</span></span>

<span data-ttu-id="8344c-154">Başlamak için aşağıdaki görüntüleri birinden bir VM oluşturma bulunan [Microsoft Azure portal][link-azure-portal]:</span><span class="sxs-lookup"><span data-stu-id="8344c-154">To begin, create a VM from one of the following images, located at the [Microsoft Azure portal][link-azure-portal]:</span></span>

* <span data-ttu-id="8344c-155">Windows Server ([2012 R2 Datacenter][link-datactr-2012-r2], [2012 Datacenter][link-datactr-2012], [2008 R2 SP1] [link-datactr-2008-r2])</span><span class="sxs-lookup"><span data-stu-id="8344c-155">Windows Server ([2012 R2 Datacenter][link-datactr-2012-r2], [2012 Datacenter][link-datactr-2012], [2008 R2 SP1][link-datactr-2008-r2])</span></span>
* <span data-ttu-id="8344c-156">SQL Server 2014 ([Kurumsal][link-sql-2014-ent], [standart][link-sql-2014-std], [Web] [ link-sql-2014-web])</span><span class="sxs-lookup"><span data-stu-id="8344c-156">SQL Server 2014 ([Enterprise][link-sql-2014-ent], [Standard][link-sql-2014-std], [Web][link-sql-2014-web])</span></span>
* <span data-ttu-id="8344c-157">SQL Server 2012 SP2'yi ([Kurumsal][link-sql-2012-ent], [standart][link-sql-2012-std], [Web] [ link-sql-2012-web])</span><span class="sxs-lookup"><span data-stu-id="8344c-157">SQL Server 2012 SP2 ([Enterprise][link-sql-2012-ent], [Standard][link-sql-2012-std], [Web][link-sql-2012-web])</span></span>

<span data-ttu-id="8344c-158">Bu bağlantılar SKU sayfasındaki Yayımlama Portalı'nda da bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="8344c-158">These links can also be found in the Publishing Portal under the SKU page.</span></span>

> [!TIP]
> <span data-ttu-id="8344c-159">Geçerli Azure portal veya PowerShell kullanıyorsanız, Windows Server görüntülerini 8 Eylül 2014 yayınlanan ve üzeri onaylanır.</span><span class="sxs-lookup"><span data-stu-id="8344c-159">If you are using the current Azure portal or PowerShell, Windows Server images published on September 8, 2014 and later are approved.</span></span>
>
>

### <a name="32-create-your-windows-based-vm"></a><span data-ttu-id="8344c-160">3.2, Windows tabanlı VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="8344c-160">3.2 Create your Windows-based VM</span></span>
<span data-ttu-id="8344c-161">Microsoft Azure Portalı'ndan yalnızca birkaç basit adımda onaylanmış bir temel görüntü göre VM oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8344c-161">From the Microsoft Azure portal, you can create your VM based on an approved base image in just a few simple steps.</span></span> <span data-ttu-id="8344c-162">İşlemine genel bakış verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="8344c-162">The following is an overview of the process:</span></span>

1. <span data-ttu-id="8344c-163">Temel görüntü sayfasından seçin **sanal makine oluşturma** yeni yönlendirilmesine [Microsoft Azure portal][link-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="8344c-163">From the base image page, select **Create Virtual Machine** to be directed to the new [Microsoft Azure portal][link-azure-portal].</span></span>

    ![Çizim][img-acom-1]
2. <span data-ttu-id="8344c-165">Portal kullanmak istediğiniz Azure aboneliği için parola ve Microsoft hesabı ile oturum açın.</span><span class="sxs-lookup"><span data-stu-id="8344c-165">Sign in to the portal with the Microsoft account and password for the Azure subscription you want to use.</span></span>
3. <span data-ttu-id="8344c-166">Seçtiğiniz temel görüntü kullanarak bir VM oluşturmak için istemleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="8344c-166">Follow the prompts to create a VM by using the base image you have selected.</span></span> <span data-ttu-id="8344c-167">VM için bir ana bilgisayar adını (bilgisayar adı), (yönetici olarak kayıtlı) kullanıcı adı ve parolasını sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8344c-167">You need to provide a host name (name of the computer), user name (registered as an administrator), and password for the VM.</span></span>

    ![Çizim][img-portal-vm-create]
4. <span data-ttu-id="8344c-169">Dağıtmak için VM boyutunu seçin:</span><span class="sxs-lookup"><span data-stu-id="8344c-169">Select the size of the VM to deploy:</span></span>

    <span data-ttu-id="8344c-170">a.</span><span class="sxs-lookup"><span data-stu-id="8344c-170">a.</span></span>    <span data-ttu-id="8344c-171">VHD şirket içi geliştirme yapmayı planlıyorsanız, boyutu önemli değildir.</span><span class="sxs-lookup"><span data-stu-id="8344c-171">If you plan to develop the VHD on-premises, the size does not matter.</span></span> <span data-ttu-id="8344c-172">En küçük VM'lerden birini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8344c-172">Consider using one of the smaller VMs.</span></span>

    <span data-ttu-id="8344c-173">b.</span><span class="sxs-lookup"><span data-stu-id="8344c-173">b.</span></span>    <span data-ttu-id="8344c-174">Görüntüyü Azure'da geliştirmeyi planlıyorsanız, seçilen görüntü için önerilen VM boyutlarından birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="8344c-174">If you plan to develop the image in Azure, consider using one of the recommended VM sizes for the selected image.</span></span>

    <span data-ttu-id="8344c-175">c.</span><span class="sxs-lookup"><span data-stu-id="8344c-175">c.</span></span>    <span data-ttu-id="8344c-176">Fiyatlandırma bilgileri için bkz **fiyatlandırma katmanlarına önerilen** portalında görüntülenen Seçici.</span><span class="sxs-lookup"><span data-stu-id="8344c-176">For pricing information, refer to the **Recommended pricing tiers** selector displayed on the portal.</span></span> <span data-ttu-id="8344c-177">Yayımcı tarafından sağlanan üç önerilen boyut burada belirtilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8344c-177">It will provide the three recommended sizes provided by the publisher.</span></span> <span data-ttu-id="8344c-178">(Burada, yayımcı Microsoft'tur.)</span><span class="sxs-lookup"><span data-stu-id="8344c-178">(In this case, the publisher is Microsoft.)</span></span>

    ![Çizim][img-portal-vm-size]
5. <span data-ttu-id="8344c-180">Özellikleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="8344c-180">Set properties:</span></span>

    <span data-ttu-id="8344c-181">a.</span><span class="sxs-lookup"><span data-stu-id="8344c-181">a.</span></span>    <span data-ttu-id="8344c-182">Hızlı dağıtım için altında özellikleri için varsayılan değer bırakabilirsiniz **isteğe bağlı yapılandırma** ve **kaynak grubu**.</span><span class="sxs-lookup"><span data-stu-id="8344c-182">For quick deployment, you can leave the default values for the properties under **Optional Configuration** and **Resource Group**.</span></span>

    <span data-ttu-id="8344c-183">b.</span><span class="sxs-lookup"><span data-stu-id="8344c-183">b.</span></span>    <span data-ttu-id="8344c-184">Altında **depolama hesabı**, işletim sistemi VHD depolanacağı depolama hesabı isteğe bağlı olarak seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8344c-184">Under **Storage Account**, you can optionally select the storage account in which the operating system VHD will be stored.</span></span>

    <span data-ttu-id="8344c-185">c.</span><span class="sxs-lookup"><span data-stu-id="8344c-185">c.</span></span>    <span data-ttu-id="8344c-186">Altında **kaynak grubu**, isteğe bağlı olarak VM yerleştirileceği mantıksal grup seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8344c-186">Under **Resource Group**, you can optionally select the logical group in which to place the VM.</span></span>
6. <span data-ttu-id="8344c-187">Seçin **konumu** dağıtımı için:</span><span class="sxs-lookup"><span data-stu-id="8344c-187">Select the **Location** for deployment:</span></span>

    <span data-ttu-id="8344c-188">a.</span><span class="sxs-lookup"><span data-stu-id="8344c-188">a.</span></span>    <span data-ttu-id="8344c-189">VHD şirket içi geliştirme yapmayı planlıyorsanız, Azure için daha sonra görüntüyü yükler için konumun önemli değildir.</span><span class="sxs-lookup"><span data-stu-id="8344c-189">If you plan to develop the VHD on-premises, the location does not matter because you will upload the image to Azure later.</span></span>

    <span data-ttu-id="8344c-190">b.</span><span class="sxs-lookup"><span data-stu-id="8344c-190">b.</span></span>    <span data-ttu-id="8344c-191">Görüntüyü Azure'da geliştirmeyi planlıyorsanız, başlangıçta ABD tabanlı Microsoft Azure bölgelerinden birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="8344c-191">If you plan to develop the image in Azure, consider using one of the US-based Microsoft Azure regions from the beginning.</span></span> <span data-ttu-id="8344c-192">Bu sertifika için görüntünüzü gönderdiğinizde, Microsoft sizin adınıza gerçekleştiren VHD kopyalama işlemini hızlandırır.</span><span class="sxs-lookup"><span data-stu-id="8344c-192">This speeds up the VHD copying process that Microsoft performs on your behalf when you submit your image for certification.</span></span>

    ![Çizim][img-portal-vm-location]
7. <span data-ttu-id="8344c-194">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8344c-194">Click **Create**.</span></span> <span data-ttu-id="8344c-195">VM dağıtmak başlatır.</span><span class="sxs-lookup"><span data-stu-id="8344c-195">The VM starts to deploy.</span></span> <span data-ttu-id="8344c-196">Dağıtımınız birkaç dakika içinde başarıyla tamamlanır ve SKU'nuz için görüntü oluşturmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8344c-196">Within minutes, you will have a successful deployment and can begin to create the image for your SKU.</span></span>

### <a name="33-develop-your-vhd-in-the-cloud"></a><span data-ttu-id="8344c-197">3.3, VHD bulutta geliştirin</span><span class="sxs-lookup"><span data-stu-id="8344c-197">3.3 Develop your VHD in the cloud</span></span>
<span data-ttu-id="8344c-198">Uzak Masaüstü Protokolü (RDP) kullanarak, VHD bulutta geliştirmek öneririz.</span><span class="sxs-lookup"><span data-stu-id="8344c-198">We strongly recommend that you develop your VHD in the cloud by using Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="8344c-199">Kullanıcı adı ve parolayla sağlama işlemi sırasında belirtilen için RDP bağlayın.</span><span class="sxs-lookup"><span data-stu-id="8344c-199">You connect to RDP with the user name and password specified during provisioning.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8344c-200">VHD geliştiriyorsanız (hangi önerilmez) şirket içi, bkz: [şirket içi bir sanal makine görüntüsü oluşturma](marketplace-publishing-vm-image-creation-on-premise.md).</span><span class="sxs-lookup"><span data-stu-id="8344c-200">If you develop your VHD on-premises (which is not recommended), see [Creating a virtual machine image on-premises](marketplace-publishing-vm-image-creation-on-premise.md).</span></span> <span data-ttu-id="8344c-201">VHD indirme bulutta geliştiriyorsanız gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="8344c-201">Downloading your VHD is not necessary if you are developing in the cloud.</span></span>
>
>

<span data-ttu-id="8344c-202">**RDP aracılığıyla bağlanırken [Microsoft Azure portalı][link-azure-portal]**</span><span class="sxs-lookup"><span data-stu-id="8344c-202">**Connect via RDP using the [Microsoft Azure portal][link-azure-portal]**</span></span>

1. <span data-ttu-id="8344c-203">Seçin **Gözat** > **VM'ler**.</span><span class="sxs-lookup"><span data-stu-id="8344c-203">Select **Browse** > **VMs**.</span></span>
2. <span data-ttu-id="8344c-204">Sanal makineler dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="8344c-204">The Virtual machines blade opens.</span></span> <span data-ttu-id="8344c-205">Bağlanmak istediğiniz VM çalışıyorsa ve dağıtılan VM'ler listesinden seçin emin olun.</span><span class="sxs-lookup"><span data-stu-id="8344c-205">Ensure that the VM that you want to connect with is running, and then select it from the list of deployed VMs.</span></span>
3. <span data-ttu-id="8344c-206">Seçilen VM açıklayan bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="8344c-206">A blade opens that describes the selected VM.</span></span> <span data-ttu-id="8344c-207">En üstte tıklatın **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="8344c-207">At the top, click **Connect**.</span></span>
4. <span data-ttu-id="8344c-208">Kullanıcı adı ve sağlama işlemi sırasında belirtilen parola girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="8344c-208">You are prompted to enter the user name and password that you specified during provisioning.</span></span>

<span data-ttu-id="8344c-209">**PowerShell kullanarak RDP aracılığıyla bağlanma**</span><span class="sxs-lookup"><span data-stu-id="8344c-209">**Connect via RDP using PowerShell**</span></span>

<span data-ttu-id="8344c-210">Uzak Masaüstü dosyası yerel makineye indirmek için kullanacağınız [Get-AzureRemoteDesktopFile cmdlet'i][link-technet-2].</span><span class="sxs-lookup"><span data-stu-id="8344c-210">To download a remote desktop file to a local machine, use the [Get-AzureRemoteDesktopFile cmdlet][link-technet-2].</span></span> <span data-ttu-id="8344c-211">Bu cmdlet kullanabilmeniz için VM adını ve hizmet adını bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8344c-211">In order to use this cmdlet, you need to know the name of the service and name of the VM.</span></span> <span data-ttu-id="8344c-212">Sanal makineden oluşturduysanız [Microsoft Azure portal][link-azure-portal], bu bilgileri VM Özellikleri'nin altında bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8344c-212">If you created the VM from the [Microsoft Azure portal][link-azure-portal], you can find this information under VM properties:</span></span>

1. <span data-ttu-id="8344c-213">Microsoft Azure Portalı'nda seçin **Gözat** > **VM'ler**.</span><span class="sxs-lookup"><span data-stu-id="8344c-213">In the Microsoft Azure portal, select **Browse** > **VMs**.</span></span>
2. <span data-ttu-id="8344c-214">Sanal makineler dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="8344c-214">The Virtual machines blade opens.</span></span> <span data-ttu-id="8344c-215">Dağıttığınız VM'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="8344c-215">Select the VM that you deployed.</span></span>
3. <span data-ttu-id="8344c-216">Seçilen VM açıklayan bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="8344c-216">A blade opens that describes the selected VM.</span></span>
4. <span data-ttu-id="8344c-217">**Özellikler**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8344c-217">Click **Properties**.</span></span>
5. <span data-ttu-id="8344c-218">Etki alanı adının ilk bölümü hizmet adıdır.</span><span class="sxs-lookup"><span data-stu-id="8344c-218">The first portion of the domain name is the service name.</span></span> <span data-ttu-id="8344c-219">Ana bilgisayar adı VM adıdır.</span><span class="sxs-lookup"><span data-stu-id="8344c-219">The host name is the VM name.</span></span>

    ![Çizim][img-portal-vm-rdp]
6. <span data-ttu-id="8344c-221">Yöneticinin yerel Masaüstü için oluşturulan VM için RDP dosyasını karşıdan yüklemek için cmdlet'i aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="8344c-221">The cmdlet to download the RDP file for the created VM to the administrator's local desktop is as follows.</span></span>

        Get‐AzureRemoteDesktopFile ‐ServiceName “baseimagevm‐6820cq00” ‐Name “BaseImageVM” –LocalPath “C:\Users\Administrator\Desktop\BaseImageVM.rdp”

<span data-ttu-id="8344c-222">RDP hakkında daha fazla bilgi MSDN makalesinde bulunabilir [RDP veya SSH ile bir Azure VM Bağlan](http://msdn.microsoft.com/library/azure/dn535788.aspx).</span><span class="sxs-lookup"><span data-stu-id="8344c-222">More information about RDP can be found on MSDN in the article [Connect to an Azure VM with RDP or SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx).</span></span>

<span data-ttu-id="8344c-223">**Bir VM yapılandırın ve, SKU oluşturun**</span><span class="sxs-lookup"><span data-stu-id="8344c-223">**Configure a VM and create your SKU**</span></span>

<span data-ttu-id="8344c-224">VHD indirilir işletim sistemi sonra SKU oluşturmaya başlamak için bir VM yapılandırmak ve Hyper-v kullanın.</span><span class="sxs-lookup"><span data-stu-id="8344c-224">After the operating system VHD is downloaded, use Hyper­V and configure a VM to begin creating your SKU.</span></span> <span data-ttu-id="8344c-225">Ayrıntılı adımlar aşağıdaki TechNet bağlantıda bulunabilir: [HyperV yükleme ve yapılandırma VM](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="8344c-225">Detailed steps can be found at the following TechNet link: [Install Hyper­V and Configure a VM](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="34-choose-the-correct-vhd-size"></a><span data-ttu-id="8344c-226">3.4 doğru VHD boyutu seçin</span><span class="sxs-lookup"><span data-stu-id="8344c-226">3.4 Choose the correct VHD size</span></span>
<span data-ttu-id="8344c-227">Windows işletim sisteminde VHD VM görüntüsü 128 GB sabit biçimli VHD oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8344c-227">The Windows operating system VHD in your VM image should be created as a 128-GB fixed-format VHD.</span></span>  

<span data-ttu-id="8344c-228">Fiziksel boyutu 128 GB daha az ise, VHD'yi seyrek olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8344c-228">If the physical size is less than 128 GB, the VHD should be sparse.</span></span> <span data-ttu-id="8344c-229">Sağlanan temel Windows ve SQL Server görüntüler zaten bu gereksinimleri karşılayan, bu nedenle biçimi veya elde edilen VHD öğesinin boyutuna değiştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="8344c-229">The base Windows and SQL Server images provided already meet these requirements, so do not change the format or the size of the VHD obtained.</span></span>  

<span data-ttu-id="8344c-230">Veri diskleri 1 TB'ye kadar büyük olabilir.</span><span class="sxs-lookup"><span data-stu-id="8344c-230">Data disks can be as large as 1 TB.</span></span> <span data-ttu-id="8344c-231">Disk boyutuna karar verirken, müşterilerin dağıtım zamanında içinde bir görüntü VHD'ler boyutlandırılamıyor unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8344c-231">When deciding on the disk size, remember that customers cannot resize VHDs within an image at the time of deployment.</span></span> <span data-ttu-id="8344c-232">Veri diski VHD'leri sabit biçimli VHD oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8344c-232">Data disk VHDs should be created as a fixed-format VHD.</span></span> <span data-ttu-id="8344c-233">Bunlar ayrıca seyrek olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8344c-233">They should also be sparse.</span></span> <span data-ttu-id="8344c-234">Veri diskleri boş olabilir veya veri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="8344c-234">Data disks can be empty or contain data.</span></span>

### <a name="35-install-the-latest-windows-patches"></a><span data-ttu-id="8344c-235">3.5 en son Windows düzeltme eklerini yükleyin</span><span class="sxs-lookup"><span data-stu-id="8344c-235">3.5 Install the latest Windows patches</span></span>
<span data-ttu-id="8344c-236">Temel görüntüler, yayımlanma tarihlerine göre en son düzeltmeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="8344c-236">The base images contain the latest patches up to their published date.</span></span> <span data-ttu-id="8344c-237">İşletim sistemi VHD yayımlamadan önce oluşturmuş olduğunuz, Windows Update'i çalıştırın ve tüm son kritik ve önemli güvenlik güncelleştirmelerini yüklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="8344c-237">Before publishing the operating system VHD you have created, ensure that Windows Update has been run and that all the latest Critical and Important security updates have been installed.</span></span>

### <a name="36-perform-additional-configuration-and-schedule-tasks-as-necessary"></a><span data-ttu-id="8344c-238">3.6 gerektiği gibi ek yapılandırma ve zamanlama görevleri gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="8344c-238">3.6 Perform additional configuration and schedule tasks as necessary</span></span>
<span data-ttu-id="8344c-239">Ek yapılandırma gerekli olursa, onu dağıtıldıktan sonra VM son değişiklikler yapmak için başlangıçta çalışan zamanlanmış bir görev kullanmayı dikkate alın:</span><span class="sxs-lookup"><span data-stu-id="8344c-239">If additional configuration is needed, consider using a scheduled task that runs at startup to make any final changes to the VM after it has been deployed:</span></span>

* <span data-ttu-id="8344c-240">Görevin başarıyla yürütüldükten sonra kendini silmesi, kullanılabilecek en iyi yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="8344c-240">It is a best practice to have the task delete itself upon successful execution.</span></span>
* <span data-ttu-id="8344c-241">Bunlar her zaman mevcut garanti yalnızca iki sürücüleri olduğundan herhangi bir yapılandırma C veya D sürücüsü dışındaki sürücülerde yararlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8344c-241">No configuration should rely on drives other than drives C or D, because these are the only two drives that are always guaranteed to exist.</span></span> <span data-ttu-id="8344c-242">C sürücüsünün işletim sistemi diski ve sürücü D geçici yerel disk.</span><span class="sxs-lookup"><span data-stu-id="8344c-242">Drive C is the operating system disk, and drive D is the temporary local disk.</span></span>

### <a name="37-generalize-the-image"></a><span data-ttu-id="8344c-243">3.7 görüntü generalize</span><span class="sxs-lookup"><span data-stu-id="8344c-243">3.7 Generalize the image</span></span>
<span data-ttu-id="8344c-244">Tüm Azure Marketi görüntülerinde genel bir şekilde yeniden kullanılabilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8344c-244">All images in the Azure Marketplace must be reusable in a generic fashion.</span></span> <span data-ttu-id="8344c-245">Diğer bir deyişle, işletim sistemi VHD genelleştirilmiş gerekir:</span><span class="sxs-lookup"><span data-stu-id="8344c-245">In other words, the operating system VHD must be generalized:</span></span>

* <span data-ttu-id="8344c-246">Windows için "sysprepped" görüntü olmalıdır ve hiçbir yapılandırmaları desteklemeyen yapılmalıdır **sysprep** komutu.</span><span class="sxs-lookup"><span data-stu-id="8344c-246">For Windows, the image should be "sysprepped," and no configurations should be done that do not support the **sysprep** command.</span></span>
* <span data-ttu-id="8344c-247">Dizin % windir%\System32\Sysprep aşağıdaki komutu çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8344c-247">You can run the following command from the directory %windir%\System32\Sysprep.</span></span>

        sysprep.exe /generalize /oobe /shutdown

  <span data-ttu-id="8344c-248">Sysprep için şu MSDN makalesine adımda işletim sistemini nasıl sağlandığını konusunda yönergeler: [Azure için Windows Server VHD oluşturun ve yükleyin](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8344c-248">Guidance on how to sysprep the operating system is provided in Step of the following MSDN article: [Create and upload a Windows Server VHD to Azure](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="4-deploy-a-vm-from-your-vhds"></a><span data-ttu-id="8344c-249">4. Vhd'lerinizi VM'den dağıtma</span><span class="sxs-lookup"><span data-stu-id="8344c-249">4. Deploy a VM from your VHDs</span></span>
<span data-ttu-id="8344c-250">Vhd'lerinizi (genelleştirilmiş bir işletim sistemi ve VHD disk sıfır veya daha fazla veri) için bir Azure depolama hesabı karşıya yükledikten sonra bunları bir kullanıcı VM görüntüsü olarak kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8344c-250">After you have uploaded your VHDs (the generalized operating system VHD and zero or more data disk VHDs) to an Azure storage account, you can register them as a user VM image.</span></span> <span data-ttu-id="8344c-251">Ardından, görüntü test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8344c-251">Then you can test that image.</span></span> <span data-ttu-id="8344c-252">İşletim sisteminizi VHD genelleştirilmiş olmadığından, doğrudan VM VHD URL'si sağlayarak dağıtamayacağınızı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8344c-252">Note that because your operating system VHD is generalized, you cannot directly deploy the VM by providing the VHD URL.</span></span>

<span data-ttu-id="8344c-253">VM görüntüleri hakkında daha fazla bilgi edinmek için aşağıdaki blog gönderileri gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="8344c-253">To learn more about VM images, review the following blog posts:</span></span>

* [<span data-ttu-id="8344c-254">VM görüntüsü</span><span class="sxs-lookup"><span data-stu-id="8344c-254">VM Image</span></span>](https://azure.microsoft.com/blog/vm-image-blog-post/)
* [<span data-ttu-id="8344c-255">VM görüntüsü PowerShell nasıl yapılır</span><span class="sxs-lookup"><span data-stu-id="8344c-255">VM Image PowerShell How To</span></span>](https://azure.microsoft.com/blog/vm-image-powershell-how-to-blog-post/)
* [<span data-ttu-id="8344c-256">Azure'da VM görüntüleri hakkında</span><span class="sxs-lookup"><span data-stu-id="8344c-256">About VM images in Azure</span></span>](https://msdn.microsoft.com/library/azure/dn790290.aspx)

### <a name="set-up-the-necessary-tools-powershell-and-azure-cli"></a><span data-ttu-id="8344c-257">Gerekli araçlarını Kur, PowerShell ve Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8344c-257">Set up the necessary tools, PowerShell and Azure CLI</span></span>
* [<span data-ttu-id="8344c-258">PowerShell ayarlama</span><span class="sxs-lookup"><span data-stu-id="8344c-258">How to setup PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="8344c-259">Azure CLI ayarlama</span><span class="sxs-lookup"><span data-stu-id="8344c-259">How to setup Azure CLI</span></span>](../cli-install-nodejs.md)

### <a name="41-create-a-user-vm-image"></a><span data-ttu-id="8344c-260">4.1 kullanıcı VM görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="8344c-260">4.1 Create a user VM image</span></span>
#### <a name="capture-vm"></a><span data-ttu-id="8344c-261">VM yakalama</span><span class="sxs-lookup"><span data-stu-id="8344c-261">Capture VM</span></span>
<span data-ttu-id="8344c-262">Lütfen PowerShell/API/Azure CLI kullanarak VM yakalama hakkında rehberlik için aşağıda verilen bağlantıları okuyun.</span><span class="sxs-lookup"><span data-stu-id="8344c-262">Please read the links given below for guidance on capturing the VM using API/PowerShell/Azure CLI.</span></span>

* [<span data-ttu-id="8344c-263">API</span><span class="sxs-lookup"><span data-stu-id="8344c-263">API</span></span>](https://msdn.microsoft.com/library/mt163560.aspx)
* [<span data-ttu-id="8344c-264">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8344c-264">PowerShell</span></span>](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="8344c-265">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8344c-265">Azure CLI</span></span>](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="generalize-image"></a><span data-ttu-id="8344c-266">Görüntü generalize</span><span class="sxs-lookup"><span data-stu-id="8344c-266">Generalize Image</span></span>
<span data-ttu-id="8344c-267">Lütfen PowerShell/API/Azure CLI kullanarak VM yakalama hakkında rehberlik için aşağıda verilen bağlantıları okuyun.</span><span class="sxs-lookup"><span data-stu-id="8344c-267">Please read the links given below for guidance on capturing the VM using API/PowerShell/Azure CLI.</span></span>

* [<span data-ttu-id="8344c-268">API</span><span class="sxs-lookup"><span data-stu-id="8344c-268">API</span></span>](https://msdn.microsoft.com/library/mt269439.aspx)
* [<span data-ttu-id="8344c-269">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8344c-269">PowerShell</span></span>](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="8344c-270">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8344c-270">Azure CLI</span></span>](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="42-deploy-a-vm-from-a-user-vm-image"></a><span data-ttu-id="8344c-271">4.2 bir kullanıcı VM görüntüsü VM'den dağıtma</span><span class="sxs-lookup"><span data-stu-id="8344c-271">4.2 Deploy a VM from a user VM image</span></span>
<span data-ttu-id="8344c-272">Bir kullanıcı VM görüntüsünden bir VM'yi dağıtmak için geçerli kullanabilirsiniz [Azure portal](https://manage.windowsazure.com) veya PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8344c-272">To deploy a VM from a user VM image, you can use the current [Azure portal](https://manage.windowsazure.com) or PowerShell.</span></span>

<span data-ttu-id="8344c-273">**Geçerli Azure portalından bir VM'yi dağıtmak**</span><span class="sxs-lookup"><span data-stu-id="8344c-273">**Deploy a VM from the current Azure portal**</span></span>

1. <span data-ttu-id="8344c-274">Git **yeni** > **işlem** > **sanal makine** > **galerisinden**.</span><span class="sxs-lookup"><span data-stu-id="8344c-274">Go to **New** > **Compute** > **Virtual machine** > **From gallery**.</span></span>

    ![Çizim][img-manage-vm-new]
2. <span data-ttu-id="8344c-276">Git **görüntülerim**ve ardından bir VM'yi dağıtmak VM görüntüsünü seçin:</span><span class="sxs-lookup"><span data-stu-id="8344c-276">Go to **My images**, and then select the VM image from which to deploy a VM:</span></span>

   1. <span data-ttu-id="8344c-277">Hangi görüntüsünü seçin, çünkü dikkat **görüntülerim** işletim sistemi görüntüleri ve VM görüntüleri listeler.</span><span class="sxs-lookup"><span data-stu-id="8344c-277">Pay close attention to which image you select, because the **My images** view lists both operating system images and VM images.</span></span>
   2. <span data-ttu-id="8344c-278">Disk sayısını arayan VM görüntüleri çoğunluğu olduğu için birden fazla disk görüntüsü hangi türü, dağıttığınız, belirlenmesine yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="8344c-278">Looking at the number of disks can help determine what type of image you are deploying, because the majority of VM images have more than one disk.</span></span> <span data-ttu-id="8344c-279">Ancak, bir VM görüntüsü sonra olması gereken bir tek işletim sistemi diskle sağlamak hala mümkündür **disk sayısı** 1 olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8344c-279">However, it is still possible to have a VM image with only a single operating system disk, which would then have **Number of disks** set to 1.</span></span>

      ![Çizim][img-manage-vm-select]
3. <span data-ttu-id="8344c-281">VM Oluşturma Sihirbazı'nı izleyin ve VM adı, VM boyutu, konum, kullanıcı adı ve parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="8344c-281">Follow the VM creation wizard and specify the VM name, VM size, location, user name, and password.</span></span>

<span data-ttu-id="8344c-282">**PowerShell VM'den dağıtma**</span><span class="sxs-lookup"><span data-stu-id="8344c-282">**Deploy a VM from PowerShell**</span></span>

<span data-ttu-id="8344c-283">Yeni oluşturduğunuz genelleştirilmiş VM görüntüsü'dan büyük bir VM'yi dağıtmak için aşağıdaki cmdlet'leri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8344c-283">To deploy a large VM from the generalized VM image just created, you can use the following cmdlets.</span></span>

    $img = Get-AzureVMImage -ImageName "myVMImage"
    $user = "user123"
    $pass = "adminPassword123"
    $myVM = New-AzureVMConfig -Name "VMImageVM" -InstanceSize "Large" -ImageName $img.ImageName | Add-AzureProvisioningConfig -Windows -AdminUsername $user -Password $pass
    New-AzureVM -ServiceName "VMImageCloudService" -VMs $myVM -Location "West US" -WaitForBoot

> [!IMPORTANT]
> <span data-ttu-id="8344c-284">Ek Yardım için lütfen [VHD oluşturma sırasında karşılaşılan sorun giderme ortak sorunları] bakın.</span><span class="sxs-lookup"><span data-stu-id="8344c-284">Please refer [Troubleshooting common issues encountered during VHD creation] for additional assistance.</span></span>
>
>

## <a name="5-obtain-certification-for-your-vm-image"></a><span data-ttu-id="8344c-285">5. VM görüntüsü için sertifika elde</span><span class="sxs-lookup"><span data-stu-id="8344c-285">5. Obtain certification for your VM image</span></span>
<span data-ttu-id="8344c-286">VM görüntüsü için Azure Marketi hazırlama sonraki adım, sertifikalı sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="8344c-286">The next step in preparing your VM image for the Azure Marketplace is to have it certified.</span></span>

<span data-ttu-id="8344c-287">Bu işlem, özel sertifika aracını çalıştıran, doğrulama sonuçlarını Vhd'lerinizi bulunduğu Azure kapsayıcısına yüklenmesi, bir teklif ekleme, SKU tanımlama ve sertifika için VM görüntü gönderme içeriyor.</span><span class="sxs-lookup"><span data-stu-id="8344c-287">This process includes running a special certification tool, uploading the verification results to the Azure container where your VHDs reside, adding an offer, defining your SKU, and submitting your VM image for certification.</span></span>

### <a name="51-download-and-run-the-certification-test-tool-for-azure-certified"></a><span data-ttu-id="8344c-288">5.1 indirin ve Azure sertifikalı için sertifika Test aracı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="8344c-288">5.1 Download and run the Certification Test Tool for Azure Certified</span></span>
<span data-ttu-id="8344c-289">VM görüntüsü Microsoft Azure ile uyumlu olduğundan emin olmak için kullanıcı VM görüntüden sağlanan çalışan bir VM, sertifika Aracı'nı çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="8344c-289">The certification tool runs on a running VM, provisioned from your user VM image, to ensure that the VM image is compatible with Microsoft Azure.</span></span> <span data-ttu-id="8344c-290">Bu araç, VHD'nizi hazırlamaya yönelik yönerge ve gereksinimlerin karşılandığını doğrular.</span><span class="sxs-lookup"><span data-stu-id="8344c-290">It will verify that the guidance and requirements about preparing your VHD have been met.</span></span> <span data-ttu-id="8344c-291">Aracın çıktısının istekte bulunan sertifika sırasında yayımlama portalında yüklenmelidir uyumluluk rapordur.</span><span class="sxs-lookup"><span data-stu-id="8344c-291">The output of the tool is a compatibility report, which should be uploaded on the Publishing Portal while requesting certification.</span></span>

<span data-ttu-id="8344c-292">Sertifika aracı, Windows ve Linux VM'ler ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8344c-292">The certification tool can be used with both Windows and Linux VMs.</span></span> <span data-ttu-id="8344c-293">Windows tabanlı VM'ler PowerShell aracılığıyla bağlanır ve Linux VM'ler SSH.Net üzerinden bağlanır:</span><span class="sxs-lookup"><span data-stu-id="8344c-293">It connects to Windows-based VMs via PowerShell and connects to Linux VMs via SSH.Net:</span></span>

1. <span data-ttu-id="8344c-294">İlk olarak, sertifika aracını indirin [Microsoft İndirme sitesi][link-msft-download].</span><span class="sxs-lookup"><span data-stu-id="8344c-294">First, download the certification tool at the [Microsoft download site][link-msft-download].</span></span>
2. <span data-ttu-id="8344c-295">Sertifika Aracı'nı açın ve ardından **yeni Testi Başlat** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8344c-295">Open the certification tool, and then click the **Start New Test** button.</span></span>
3. <span data-ttu-id="8344c-296">Gelen **Test bilgi** ekranında, test çalışması için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="8344c-296">From the **Test Information** screen, enter a name for the test run.</span></span>
4. <span data-ttu-id="8344c-297">VM'nizin Linux üzerinde veya Windows üzerinde çalıştığına ilişkin seçim yapın.</span><span class="sxs-lookup"><span data-stu-id="8344c-297">Choose whether your VM is on Linux or Windows.</span></span> <span data-ttu-id="8344c-298">Seçiminize bağlı olarak sonraki seçenekleri belirleyin.</span><span class="sxs-lookup"><span data-stu-id="8344c-298">Depending on which you choose, select the subsequent options.</span></span>

### <a name="connect-the-certification-tool-to-a-linux-vm-image"></a><span data-ttu-id="8344c-299">**Bir Linux VM görüntüsü sertifika aracı Bağlan**</span><span class="sxs-lookup"><span data-stu-id="8344c-299">**Connect the certification tool to a Linux VM image**</span></span>
1. <span data-ttu-id="8344c-300">SSH kimlik doğrulama modunu seçin: Parola veya anahtar dosyası.</span><span class="sxs-lookup"><span data-stu-id="8344c-300">Select the SSH authentication mode: password or key file.</span></span>
2. <span data-ttu-id="8344c-301">Parola tabanlı kimlik doğrulamasını kullanıyorsanız, etki alanı adı sistemi (DNS) adı, kullanıcı adı ve parola girin.</span><span class="sxs-lookup"><span data-stu-id="8344c-301">If using password-­based authentication, enter the Domain Name System (DNS) name, user name, and password.</span></span>
3. <span data-ttu-id="8344c-302">Anahtar dosyası kimlik doğrulamasını kullanıyorsanız, DNS adını, kullanıcı adı ve özel anahtar konumu girin.</span><span class="sxs-lookup"><span data-stu-id="8344c-302">If using key file authentication, enter the DNS name, user name, and private key location.</span></span>

   ![Linux VM görüntüsü parola kimlik doğrulaması][img-cert-vm-pswd-lnx]

   ![Linux VM görüntüsü anahtar dosyası kimlik doğrulaması][img-cert-vm-key-lnx]

### <a name="connect-the-certification-tool-to-a-windows-based-vm-image"></a><span data-ttu-id="8344c-305">**Bir Windows tabanlı VM görüntüsü sertifika aracı Bağlan**</span><span class="sxs-lookup"><span data-stu-id="8344c-305">**Connect the certification tool to a Windows-based VM image**</span></span>
1. <span data-ttu-id="8344c-306">Tam VM DNS adını (örneğin, MyVMName.Cloudapp.net) girin.</span><span class="sxs-lookup"><span data-stu-id="8344c-306">Enter the fully qualified VM DNS name (for example, MyVMName.Cloudapp.net).</span></span>
2. <span data-ttu-id="8344c-307">Kullanıcı adı ve parola girin.</span><span class="sxs-lookup"><span data-stu-id="8344c-307">Enter the user name and password.</span></span>

   ![Windows VM görüntüsünü parola kimlik doğrulaması][img-cert-vm-pswd-win]

<span data-ttu-id="8344c-309">Linux veya Windows tabanlı VM görüntü için doğru seçeneklerini seçtikten sonra Seç **Bağlantıyı Sına** SSH.Net veya PowerShell test etmek için geçerli bir bağlantı olduğundan emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="8344c-309">After you have selected the correct options for your Linux or Windows-based VM image, select **Test Connection** to ensure that SSH.Net or PowerShell has a valid connection for testing purposes.</span></span> <span data-ttu-id="8344c-310">Bağlantı kurulduktan sonra Seç **sonraki** testi başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="8344c-310">After a connection is established, select **Next** to start the test.</span></span>

<span data-ttu-id="8344c-311">Test tamamlandığında her bir test öğesine yönelik sonuçları (Başarılı/Başarısız/Uyarı) alırsınız.</span><span class="sxs-lookup"><span data-stu-id="8344c-311">When the test is complete, you will receive the results (Pass/Fail/Warning) for each test element.</span></span>

![Linux VM görüntüsü için test çalışmaları][img-cert-vm-test-lnx]

![Windows VM görüntüsü için test çalışmaları][img-cert-vm-test-win]

<span data-ttu-id="8344c-314">Tüm testler başarısız olursa, görüntünüzü uygunluğu onaylanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="8344c-314">If any of the tests fail, your image will not be certified.</span></span> <span data-ttu-id="8344c-315">Bu gerçekleşirse, gereksinimleri gözden geçirin ve gerekli değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="8344c-315">If this occurs, review the requirements and make any necessary changes.</span></span>

<span data-ttu-id="8344c-316">Otomatikleştirilmiş test sonra VM görüntüsüne bir soru formu ekran aracılığıyla ek giriş vermeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="8344c-316">After the automated test, you are asked to provide additional input on your VM image via a questionnaire screen.</span></span>  <span data-ttu-id="8344c-317">Soruları tamamlayın ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="8344c-317">Complete the questions, and then select **Next**.</span></span>

![Sertifika aracı anket][img-cert-vm-questionnaire]

![Sertifika aracı anket][img-cert-vm-questionnaire-2]

<span data-ttu-id="8344c-320">Soru tamamladıktan sonra görüntü ve başarısız tüm değerlendirmeleri için bir açıklama Linux VM için SSH erişim bilgileri gibi ek bilgiler sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="8344c-320">After you have completed the questionnaire, you can provide additional information such as SSH access information for the Linux VM image and an explanation for any failed assessments.</span></span> <span data-ttu-id="8344c-321">Soru verdiğiniz yanıtlar yanı sıra test sonuçlarını ve yürütülen test çalışmaları için günlük dosyalarını indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8344c-321">You can download the test results and log files for the executed test cases in addition to your answers to the questionnaire.</span></span> <span data-ttu-id="8344c-322">Sonuçları aynı kapsayıcı Vhd'lerinizi olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8344c-322">Save the results in the same container as your VHDs.</span></span>

![Test sonuçları sertifika Kaydet][img-cert-vm-results]

### <a name="52-get-the-shared-access-signature-uri-for-your-vm-images"></a><span data-ttu-id="8344c-324">5.2 VM görüntülerinizi için URI paylaşılan erişim imzası Al</span><span class="sxs-lookup"><span data-stu-id="8344c-324">5.2 Get the shared access signature URI for your VM images</span></span>
<span data-ttu-id="8344c-325">Yayımlama işlemi sırasında her bir SKU için oluşturduğunuz VHD'leri sağlama Tekdüzen Kaynak Tanımlayıcıları (URI'ler) belirtin.</span><span class="sxs-lookup"><span data-stu-id="8344c-325">During the publishing process, you specify the uniform resource identifiers (URIs) that lead to each of the VHDs you have created for your SKU.</span></span> <span data-ttu-id="8344c-326">Sertifika işlemi sırasında Microsoft'un bu VHD'lere erişmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8344c-326">Microsoft needs access to these VHDs during the certification process.</span></span> <span data-ttu-id="8344c-327">Bu nedenle, her VHD için bir paylaşılan erişim imzası URI oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8344c-327">Therefore, you need to create a shared access signature URI for each VHD.</span></span> <span data-ttu-id="8344c-328">İçinde girilmelidir URI budur **görüntüleri** yayımlama portalında sekmesindedir.</span><span class="sxs-lookup"><span data-stu-id="8344c-328">This is the URI that should be entered in the **Images** tab in the Publishing Portal.</span></span>

<span data-ttu-id="8344c-329">Oluşturulan URI paylaşılan erişim imzası aşağıdaki gereksinimlere uyması:</span><span class="sxs-lookup"><span data-stu-id="8344c-329">The shared access signature URI created should adhere to the following requirements:</span></span>

* <span data-ttu-id="8344c-330">Paylaşılan erişim imzası URI'ler Vhd'lerinizi için oluştururken, liste ve Okuma izinleri yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="8344c-330">When generating shared access signature URIs for your VHDs, List and Read­ permissions are sufficient.</span></span> <span data-ttu-id="8344c-331">Yazma veya Silme erişimi sağlamayın.</span><span class="sxs-lookup"><span data-stu-id="8344c-331">Do not provide Write or Delete access.</span></span>
* <span data-ttu-id="8344c-332">Paylaşılan erişim imzası URI oluşturulduğunda süresi erişim için üç (3) hafta ila en az olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8344c-332">The duration for access should be a minimum of three (3) weeks from when the shared access signature URI is created.</span></span>
* <span data-ttu-id="8344c-333">UTC saati için korumak için geçerli tarihten önce gün seçin.</span><span class="sxs-lookup"><span data-stu-id="8344c-333">To safeguard for UTC time, select the day before the current date.</span></span> <span data-ttu-id="8344c-334">Örneğin, geçerli tarihe 6 Ekim 2014 ise 5/10/2014 seçin.</span><span class="sxs-lookup"><span data-stu-id="8344c-334">For example, if the current date is October 6, 2014, select 10/5/2014.</span></span>

<span data-ttu-id="8344c-335">SAS URL, VHD için Azure Marketi paylaşmak için birden çok şekilde oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="8344c-335">SAS URL can be generated in multiple ways to share your VHD for Azure Marketplace.</span></span>
<span data-ttu-id="8344c-336">3 önerilen araçlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8344c-336">Following are the 3 recommended tools:</span></span>

1.  <span data-ttu-id="8344c-337">Azure Depolama Gezgini</span><span class="sxs-lookup"><span data-stu-id="8344c-337">Azure Storage Explorer</span></span>
2.  <span data-ttu-id="8344c-338">Microsoft Storage Gezgini</span><span class="sxs-lookup"><span data-stu-id="8344c-338">Microsoft Storage Explorer</span></span>
3.  <span data-ttu-id="8344c-339">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8344c-339">Azure CLI</span></span>

<span data-ttu-id="8344c-340">**Azure Depolama Gezgini (Windows kullanıcıları için önerilir)**</span><span class="sxs-lookup"><span data-stu-id="8344c-340">**Azure Storage Explorer (Recommended for Windows Users)**</span></span>

<span data-ttu-id="8344c-341">Azure Storage Gezgini kullanarak SAS URL oluşturmak için adımlar aşağıda verilmiştir</span><span class="sxs-lookup"><span data-stu-id="8344c-341">Following are the steps for generating SAS URL by using Azure Storage Explorer</span></span>

1. <span data-ttu-id="8344c-342">Karşıdan [Azure Storage Gezgini 6 Önizleme 3](https://azurestorageexplorer.codeplex.com/) Codeplex.</span><span class="sxs-lookup"><span data-stu-id="8344c-342">Download [Azure Storage Explorer 6 Preview 3](https://azurestorageexplorer.codeplex.com/) from CodePlex.</span></span> <span data-ttu-id="8344c-343">Git [Azure Storage Gezgini 6 Önizleme](https://azurestorageexplorer.codeplex.com/) tıklatıp **"İndirmeleri"**.</span><span class="sxs-lookup"><span data-stu-id="8344c-343">Go to [Azure Storage Explorer 6 Preview](https://azurestorageexplorer.codeplex.com/) and click **"Downloads"**.</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_01.png)

2. <span data-ttu-id="8344c-345">Karşıdan [AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668) ve unzipping sonra yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8344c-345">Download [AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668) and install after unzipping it.</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_02.png)

3. <span data-ttu-id="8344c-347">Yüklendikten sonra uygulamayı açın.</span><span class="sxs-lookup"><span data-stu-id="8344c-347">After it is installed, open the application.</span></span>
4. <span data-ttu-id="8344c-348">Tıklatın **hesabı eklemek**.</span><span class="sxs-lookup"><span data-stu-id="8344c-348">Click **Add Account**.</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_03.png)

5. <span data-ttu-id="8344c-350">Depolama hesabı adı, depolama hesabı anahtarı ve depolama uç noktaları etki alanını belirtin.</span><span class="sxs-lookup"><span data-stu-id="8344c-350">Specify the storage account name, storage account key, and storage endpoints domain.</span></span> <span data-ttu-id="8344c-351">Azure Portalı'nda, VHD'yi nerede tutulur Azure Aboneliğinize depolama hesabında budur.</span><span class="sxs-lookup"><span data-stu-id="8344c-351">This is the storage account in your Azure subscription where you have kept your VHD on Azure portal.</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_04.png)

6. <span data-ttu-id="8344c-353">Azure Storage Gezgini belirli depolama hesabınıza bağlandıktan sonra tüm gösteren başlayacak içinde depolama hesabını içerir.</span><span class="sxs-lookup"><span data-stu-id="8344c-353">Once Azure Storage Explorer is connected to your specific storage account, it will start showing all of the contains within the storage account.</span></span> <span data-ttu-id="8344c-354">İşletim sistemi disk VHD dosyasını (senaryonuz için uygun olup olmadığını da veri diskleri) kopyaladığınız kapsayıcısı seçin.</span><span class="sxs-lookup"><span data-stu-id="8344c-354">Select the container where you copied the operating system disk VHD file (also data disks if they are applicable for your scenario).</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_05.png)

7. <span data-ttu-id="8344c-356">Blob kapsayıcısı seçtikten sonra Azure Storage Gezgini kapsayıcı içindeki dosyaların gösteren başlatır.</span><span class="sxs-lookup"><span data-stu-id="8344c-356">After selecting the blob container, Azure Storage Explorer starts showing the files within the container.</span></span> <span data-ttu-id="8344c-357">Gönderilmesi gereken görüntü dosyası (.vhd) seçin.</span><span class="sxs-lookup"><span data-stu-id="8344c-357">Select the image file (.vhd) that needs to be submitted.</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_06.png)

8.  <span data-ttu-id="8344c-359">Kapsayıcıda .vhd dosyası seçtikten sonra **güvenlik** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="8344c-359">After selecting the .vhd file in the container, click the **Security** tab.</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_07.png)

9.  <span data-ttu-id="8344c-361">İçinde **Blob kapsayıcı güvenlik** iletişim kutusunda, üzerinde Varsayılanları bırakabilir **erişim düzeyi** sekmesini ve ardından **paylaşılan erişim imzaları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="8344c-361">In the **Blob Container Security** dialog box, leave the defaults on the **Access Level** tab, and then click **Shared Access Signatures** tab.</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_08.png)

10. <span data-ttu-id="8344c-363">.Vhd görüntüsü için paylaşılan erişim imzası URI oluşturmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="8344c-363">Follow the steps below to generate a shared access signature URI for the .vhd image:</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_09.png)

    <span data-ttu-id="8344c-365">a.</span><span class="sxs-lookup"><span data-stu-id="8344c-365">a.</span></span> <span data-ttu-id="8344c-366">**Erişime izin:** UTC saati için korumak için geçerli tarihten önce gününü seçin.</span><span class="sxs-lookup"><span data-stu-id="8344c-366">**Access permitted from:** To safeguard for UTC time, select the day before the current date.</span></span> <span data-ttu-id="8344c-367">Örneğin, geçerli tarihe 6 Ekim 2014 ise 5/10/2014 seçin.</span><span class="sxs-lookup"><span data-stu-id="8344c-367">For example, if the current date is October 6, 2014, select 10/5/2014.</span></span>

    <span data-ttu-id="8344c-368">b.</span><span class="sxs-lookup"><span data-stu-id="8344c-368">b.</span></span> <span data-ttu-id="8344c-369">**Erişime izin:** 3 hafta sonra en az bir tarihi seçin **erişime izin** tarih.</span><span class="sxs-lookup"><span data-stu-id="8344c-369">**Access permitted to:** Select a date that is at least 3 weeks after the **Access permitted from** date.</span></span>

    <span data-ttu-id="8344c-370">c.</span><span class="sxs-lookup"><span data-stu-id="8344c-370">c.</span></span> <span data-ttu-id="8344c-371">**İzin verilen eylemleri:** seçin **listesi** ve **okuma** izinleri.</span><span class="sxs-lookup"><span data-stu-id="8344c-371">**Actions permitted:** Select the **List** and **Read** permissions.</span></span>

    <span data-ttu-id="8344c-372">d.</span><span class="sxs-lookup"><span data-stu-id="8344c-372">d.</span></span> <span data-ttu-id="8344c-373">.Vhd dosyası doğru seçtiğiniz sonra dosyanızı görünür **erişmek için Blob adı** uzantısı .vhd ile.</span><span class="sxs-lookup"><span data-stu-id="8344c-373">If you have selected your .vhd file correctly, then your file appears in **Blob name to access** with extension .vhd.</span></span>

    <span data-ttu-id="8344c-374">e.</span><span class="sxs-lookup"><span data-stu-id="8344c-374">e.</span></span> <span data-ttu-id="8344c-375">Tıklatın **imzayı üretmek**.</span><span class="sxs-lookup"><span data-stu-id="8344c-375">Click **Generate Signature**.</span></span>

    <span data-ttu-id="8344c-376">f.</span><span class="sxs-lookup"><span data-stu-id="8344c-376">f.</span></span> <span data-ttu-id="8344c-377">İçinde **oluşturulan paylaşılan erişim imzası URI bu kapsayıcının**, yukarıdaki onay aşağıdaki vurgulanan için:</span><span class="sxs-lookup"><span data-stu-id="8344c-377">In **Generated Shared Access Signature URI of this container**, check for the following as highlighted above:</span></span>

       - <span data-ttu-id="8344c-378">Görüntünüzü dosya adı olduğundan emin olun ve **".vhd"** URI'de şunlardır.</span><span class="sxs-lookup"><span data-stu-id="8344c-378">Make sure that your image file name and **".vhd"** are in the URI.</span></span>
       - <span data-ttu-id="8344c-379">İmza sonunda olduğundan emin olun **"rl ="** görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8344c-379">At the end of the signature, make sure that **"=rl"** appears.</span></span> <span data-ttu-id="8344c-380">Bu, okuma ve liste erişim başarıyla sağlandı gösterir.</span><span class="sxs-lookup"><span data-stu-id="8344c-380">This demonstrates that Read and List access was provided successfully.</span></span>
       - <span data-ttu-id="8344c-381">İmza ortadaki olduğundan emin olun **"sr c ="** görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8344c-381">In middle of the signature, make sure that **"sr=c"** appears.</span></span> <span data-ttu-id="8344c-382">Bu kapsayıcı düzeyinde erişime sahip olması gösterir</span><span class="sxs-lookup"><span data-stu-id="8344c-382">This demonstrates that you have container level access</span></span>

11. <span data-ttu-id="8344c-383">Oluşturulan erişimin imza URI çalıştığı paylaşılan emin olmak için tıklatın **tarayıcısında Test**.</span><span class="sxs-lookup"><span data-stu-id="8344c-383">To ensure that the generated shared access signature URI works, click **Test in Browser**.</span></span> <span data-ttu-id="8344c-384">İndirme işlemi başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8344c-384">It should start the download process.</span></span>

12. <span data-ttu-id="8344c-385">Paylaşılan erişim imzası URI kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="8344c-385">Copy the shared access signature URI.</span></span> <span data-ttu-id="8344c-386">Bu, Yayımlama Portalı'na yapıştırılacak olan URI'dir.</span><span class="sxs-lookup"><span data-stu-id="8344c-386">This is the URI to paste into the Publishing Portal.</span></span>

13. <span data-ttu-id="8344c-387">SKU'ndaki her VHD için 6-10 adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="8344c-387">Repeat steps 6-10 for each VHD in the SKU.</span></span>

<span data-ttu-id="8344c-388">**Microsoft Azure Depolama Gezgini (MAC/Windows/Linux)**</span><span class="sxs-lookup"><span data-stu-id="8344c-388">**Microsoft Azure Storage Explorer (Windows/MAC/Linux)**</span></span>

<span data-ttu-id="8344c-389">Microsoft Azure Storage Gezgini kullanarak SAS URL oluşturmak için adımlar aşağıda verilmiştir</span><span class="sxs-lookup"><span data-stu-id="8344c-389">Following are the steps for generating SAS URL by using Microsoft Azure Storage Explorer</span></span>

1.  <span data-ttu-id="8344c-390">Microsoft Azure Storage Gezgini form karşıdan [http://storageexplorer.com/](http://storageexplorer.com/) Web sitesi.</span><span class="sxs-lookup"><span data-stu-id="8344c-390">Download Microsoft Azure Storage Explorer form [http://storageexplorer.com/](http://storageexplorer.com/) website.</span></span> <span data-ttu-id="8344c-391">Git [Microsoft Azure Storage Gezgini](http://storageexplorer.com/releasenotes.html) tıklatıp **"Windows için karşıdan yükleme"**.</span><span class="sxs-lookup"><span data-stu-id="8344c-391">Go to [Microsoft Azure Storage Explorer](http://storageexplorer.com/releasenotes.html) and click **“Download for Windows”**.</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_10.png)

2.  <span data-ttu-id="8344c-393">Yüklendikten sonra uygulamayı açın.</span><span class="sxs-lookup"><span data-stu-id="8344c-393">After it is installed, open the application.</span></span>

3.  <span data-ttu-id="8344c-394">Tıklatın **hesabı eklemek**.</span><span class="sxs-lookup"><span data-stu-id="8344c-394">Click **Add Account**.</span></span>

4.  <span data-ttu-id="8344c-395">Microsoft Azure Storage Gezgini aboneliğinize hesabınızda oturum açma yapılandırın</span><span class="sxs-lookup"><span data-stu-id="8344c-395">Configure Microsoft Azure Storage Explorer to your subscription by sign in to your account</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_11.png)

5.  <span data-ttu-id="8344c-397">Depolama hesabına gidin ve kapsayıcı seçin</span><span class="sxs-lookup"><span data-stu-id="8344c-397">Go to storage account and select the Container</span></span>

6.  <span data-ttu-id="8344c-398">Seçin **"Paylaşımı erişim imzası Al …"**</span><span class="sxs-lookup"><span data-stu-id="8344c-398">Select **“Get Share Access Signature..”**</span></span> <span data-ttu-id="8344c-399">Sağ tıklatarak kullanarak **kapsayıcı**</span><span class="sxs-lookup"><span data-stu-id="8344c-399">by using Right Click of the **container**</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_12.png)

7.  <span data-ttu-id="8344c-401">Aşağıdaki gibi başına başlangıç zamanı, bitiş saati ve izinleri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="8344c-401">Update Start time, Expiry time and Permissions as per following</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_13.png)

    <span data-ttu-id="8344c-403">a.</span><span class="sxs-lookup"><span data-stu-id="8344c-403">a.</span></span>  <span data-ttu-id="8344c-404">**Başlangıç saati:** UTC saati için korumak için geçerli tarihten önce gününü seçin.</span><span class="sxs-lookup"><span data-stu-id="8344c-404">**Start Time:** To safeguard for UTC time, select the day before the current date.</span></span> <span data-ttu-id="8344c-405">Örneğin, geçerli tarihe 6 Ekim 2014 ise 5/10/2014 seçin.</span><span class="sxs-lookup"><span data-stu-id="8344c-405">For example, if the current date is October 6, 2014, select 10/5/2014.</span></span>

    <span data-ttu-id="8344c-406">b.</span><span class="sxs-lookup"><span data-stu-id="8344c-406">b.</span></span>  <span data-ttu-id="8344c-407">**Sona erme saati:** 3 hafta sonra en az bir tarihi seçin **başlangıç saati** tarih.</span><span class="sxs-lookup"><span data-stu-id="8344c-407">**Expiry Time:** Select a date that is at least 3 weeks after the **Start Time** date.</span></span>

    <span data-ttu-id="8344c-408">c.</span><span class="sxs-lookup"><span data-stu-id="8344c-408">c.</span></span>  <span data-ttu-id="8344c-409">**İzinleri:** seçin **listesi** ve **okuma** izinleri</span><span class="sxs-lookup"><span data-stu-id="8344c-409">**Permissions:** Select the **List** and **Read** permissions</span></span>

8.  <span data-ttu-id="8344c-410">Kapsayıcı paylaşılan erişim imzası URI kopyalayın</span><span class="sxs-lookup"><span data-stu-id="8344c-410">Copy Container shared access signature URI</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_14.png)

    <span data-ttu-id="8344c-412">Oluşturulan SAS URL için düzeyi kapsayıcıdır ve şimdi biz VHD ad içinde eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8344c-412">Generated SAS URL is for container Level and now we need to add VHD name in it.</span></span>

    <span data-ttu-id="8344c-413">Kapsayıcı düzeyi SAS URL biçimi:`https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span><span class="sxs-lookup"><span data-stu-id="8344c-413">Format of Container Level SAS URL: `https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    <span data-ttu-id="8344c-414">SAS URL kapsayıcı adlarında aşağıdaki şekilde sonra VHD adı Ekle`https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span><span class="sxs-lookup"><span data-stu-id="8344c-414">Insert VHD name after the container name in SAS URL as below `https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    <span data-ttu-id="8344c-415">Örnek:</span><span class="sxs-lookup"><span data-stu-id="8344c-415">Example:</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_15.png)

    <span data-ttu-id="8344c-417">VHD adı TestRGVM201631920152.vhd yapılır ve ardından VHD SAS URL'si olacaktır`https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span><span class="sxs-lookup"><span data-stu-id="8344c-417">TestRGVM201631920152.vhd is the VHD Name then VHD SAS URL will be `https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    - <span data-ttu-id="8344c-418">Görüntünüzü dosya adı olduğundan emin olun ve **".vhd"** URI'de şunlardır.</span><span class="sxs-lookup"><span data-stu-id="8344c-418">Make sure that your image file name and **".vhd"** are in the URI.</span></span>
    - <span data-ttu-id="8344c-419">İmza ortadaki olduğundan emin olun **"sp rl ="** görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8344c-419">In middle of the signature, make sure that **"sp=rl"** appears.</span></span> <span data-ttu-id="8344c-420">Bu, okuma ve liste erişim başarıyla sağlandı gösterir.</span><span class="sxs-lookup"><span data-stu-id="8344c-420">This demonstrates that Read and List access was provided successfully.</span></span>
    - <span data-ttu-id="8344c-421">İmza ortadaki olduğundan emin olun **"sr c ="** görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8344c-421">In middle of the signature, make sure that **"sr=c"** appears.</span></span> <span data-ttu-id="8344c-422">Bu kapsayıcı düzeyinde erişime sahip olması gösterir</span><span class="sxs-lookup"><span data-stu-id="8344c-422">This demonstrates that you have container level access</span></span>

9.  <span data-ttu-id="8344c-423">Oluşturulan erişimin imza URI çalıştığı paylaşılan emin olmak için tarayıcıda sınayın.</span><span class="sxs-lookup"><span data-stu-id="8344c-423">To ensure that the generated shared access signature URI works, test it in browser.</span></span> <span data-ttu-id="8344c-424">Yükleme işlemini başlatmak</span><span class="sxs-lookup"><span data-stu-id="8344c-424">It should start the download process</span></span>

10. <span data-ttu-id="8344c-425">Paylaşılan erişim imzası URI kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="8344c-425">Copy the shared access signature URI.</span></span> <span data-ttu-id="8344c-426">Bu, Yayımlama Portalı'na yapıştırılacak olan URI'dir.</span><span class="sxs-lookup"><span data-stu-id="8344c-426">This is the URI to paste into the Publishing Portal.</span></span>

11. <span data-ttu-id="8344c-427">SKU'daki her VHD için bu adımları tekrarlayın.</span><span class="sxs-lookup"><span data-stu-id="8344c-427">Repeat these steps for each VHD in the SKU.</span></span>

<span data-ttu-id="8344c-428">**Azure CLI (Windows dışı & sürekli tümleştirme için önerilir)**</span><span class="sxs-lookup"><span data-stu-id="8344c-428">**Azure CLI (Recommended for Non-Windows & Continuous Integration)**</span></span>

<span data-ttu-id="8344c-429">Azure CLI kullanarak SAS URL oluşturmak için adımlar aşağıda verilmiştir</span><span class="sxs-lookup"><span data-stu-id="8344c-429">Following are the steps for generating SAS URL by using Azure CLI</span></span>

1.  <span data-ttu-id="8344c-430">Microsoft Azure CLI üzerinden indirme [burada](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/).</span><span class="sxs-lookup"><span data-stu-id="8344c-430">Download Microsoft Azure CLI from [here](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/).</span></span> <span data-ttu-id="8344c-431">Farklı bağlantıları için bulabileceğiniz  **[Windows](http://aka.ms/webpi-azure-cli)**  ve  **[MAC OS](http://aka.ms/mac-azure-cli)**.</span><span class="sxs-lookup"><span data-stu-id="8344c-431">You can also find different links for **[Windows](http://aka.ms/webpi-azure-cli)** and **[MAC OS](http://aka.ms/mac-azure-cli)**.</span></span>

2.  <span data-ttu-id="8344c-432">Bir kez yüklenir, lütfen yükleyin</span><span class="sxs-lookup"><span data-stu-id="8344c-432">Once it is downloaded, please install</span></span>

3.  <span data-ttu-id="8344c-433">Aşağıdaki kod ile bir PowerShell dosyası oluşturun ve yerel Kaydet</span><span class="sxs-lookup"><span data-stu-id="8344c-433">Create a PowerShell file with following code and save it in local</span></span>

          $conn="DefaultEndpointsProtocol=https;AccountName=<StorageAccountName>;AccountKey=<Storage Account Key>"
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl <Permission End Date> -c $conn --start <Permission Start Date>  

    <span data-ttu-id="8344c-434">Aşağıdaki parametreleri güncelleştirin yukarıda</span><span class="sxs-lookup"><span data-stu-id="8344c-434">Update the following parameters in above</span></span>

    <span data-ttu-id="8344c-435">a.</span><span class="sxs-lookup"><span data-stu-id="8344c-435">a.</span></span> <span data-ttu-id="8344c-436">**`<StorageAccountName>`**: Depolama hesabınızın adını verin</span><span class="sxs-lookup"><span data-stu-id="8344c-436">**`<StorageAccountName>`**: Give your storage account name</span></span>

    <span data-ttu-id="8344c-437">b.</span><span class="sxs-lookup"><span data-stu-id="8344c-437">b.</span></span> <span data-ttu-id="8344c-438">**`<Storage Account Key>`**: Depolama hesabı anahtarınızı verin</span><span class="sxs-lookup"><span data-stu-id="8344c-438">**`<Storage Account Key>`**: Give your storage account key</span></span>

    <span data-ttu-id="8344c-439">c.</span><span class="sxs-lookup"><span data-stu-id="8344c-439">c.</span></span> <span data-ttu-id="8344c-440">**`<Permission Start Date>`**: UTC saati için korumak için geçerli tarihten önce gün seçin.</span><span class="sxs-lookup"><span data-stu-id="8344c-440">**`<Permission Start Date>`**: To safeguard for UTC time, select the day before the current date.</span></span> <span data-ttu-id="8344c-441">Örneğin, geçerli tarih 26 Ekim 2016 ise ardından değeri olmalıdır 25/10/2016</span><span class="sxs-lookup"><span data-stu-id="8344c-441">For example, if the current date is October 26, 2016, then value should be 10/25/2016</span></span>

    <span data-ttu-id="8344c-442">d.</span><span class="sxs-lookup"><span data-stu-id="8344c-442">d.</span></span> <span data-ttu-id="8344c-443">**`<Permission End Date>`**: En az 3 hafta sonra olan bir tarih seçin **başlangıç tarihi**.</span><span class="sxs-lookup"><span data-stu-id="8344c-443">**`<Permission End Date>`**: Select a date that is at least 3 weeks after the **Start Date**.</span></span> <span data-ttu-id="8344c-444">Değerin olması **02/11/2016**.</span><span class="sxs-lookup"><span data-stu-id="8344c-444">Then value should be **11/02/2016**.</span></span>

    <span data-ttu-id="8344c-445">Uygun parametreleri güncelleştirdikten sonra örnek kod aşağıda verilmiştir</span><span class="sxs-lookup"><span data-stu-id="8344c-445">Following is the example code after updating proper parameters</span></span>

          $conn="DefaultEndpointsProtocol=https;AccountName=st20151;AccountKey=TIQE5QWMKHpT5q2VnF1bb+NUV7NVMY2xmzVx1rdgIVsw7h0pcI5nMM6+DVFO65i4bQevx21dmrflA91r0Vh2Yw=="
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl 11/02/2016 -c $conn --start 10/25/2016  

4.  <span data-ttu-id="8344c-446">"Yönetici olarak çalıştır" moduyla PowerShell Düzenleyicisi'ni açın ve #3. adımda dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="8344c-446">Open Powershell editor with “Run as Administrator” mode and open file in step #3.</span></span>

5.  <span data-ttu-id="8344c-447">Komut dosyasını çalıştırmak ve onu, SAS URL'si için kapsayıcı düzeyinde erişimi sağlar</span><span class="sxs-lookup"><span data-stu-id="8344c-447">Run the script and it will provide you the SAS URL for container level access</span></span>

    <span data-ttu-id="8344c-448">Aşağıdaki SAS imza çıktısını olmalı ve bir Not Defteri'nde vurgulanan bölümünü kopyalama</span><span class="sxs-lookup"><span data-stu-id="8344c-448">Following will be the output of the SAS Signature and copy the highlighted part in a notepad</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_16.png)

6.  <span data-ttu-id="8344c-450">Kapsayıcı düzeyi SAS URL artık alacak ve VHD ad içinde eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8344c-450">Now you will get container level SAS URL and you need to add VHD name in it.</span></span>

    <span data-ttu-id="8344c-451">Kapsayıcı düzeyi SAS URL #</span><span class="sxs-lookup"><span data-stu-id="8344c-451">Container level SAS URL #</span></span>

    `https://st20151.blob.core.windows.net/vhds?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

7.  <span data-ttu-id="8344c-452">Aşağıda gösterildiği gibi SAS URL kapsayıcı adlarında sonra VHD adı Ekle`https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`</span><span class="sxs-lookup"><span data-stu-id="8344c-452">Insert VHD name after the container name in SAS URL as shown below `https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`</span></span>

    <span data-ttu-id="8344c-453">Örnek:</span><span class="sxs-lookup"><span data-stu-id="8344c-453">Example:</span></span>

    <span data-ttu-id="8344c-454">VHD adı TestRGVM201631920152.vhd yapılır ve ardından VHD SAS URL'si olacaktır</span><span class="sxs-lookup"><span data-stu-id="8344c-454">TestRGVM201631920152.vhd is the VHD Name then VHD SAS URL will be</span></span>

    `https://st20151.blob.core.windows.net/vhds/ TestRGVM201631920152.vhd?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    - <span data-ttu-id="8344c-455">Yansıma Dosya adı ve ".vhd" URI'de olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="8344c-455">Make sure that your image file name and ".vhd" are in the URI.</span></span>
    -   <span data-ttu-id="8344c-456">İmza ortadaki olduğundan emin olun "sp rl =" görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8344c-456">In middle of the signature, make sure that "sp=rl" appears.</span></span> <span data-ttu-id="8344c-457">Bu, okuma ve liste erişim başarıyla sağlandı gösterir.</span><span class="sxs-lookup"><span data-stu-id="8344c-457">This demonstrates that Read and List access was provided successfully.</span></span>
    -   <span data-ttu-id="8344c-458">İmza ortadaki olduğundan emin olun "sr c =" görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8344c-458">In middle of the signature, make sure that "sr=c" appears.</span></span> <span data-ttu-id="8344c-459">Bu kapsayıcı düzeyinde erişime sahip olması gösterir</span><span class="sxs-lookup"><span data-stu-id="8344c-459">This demonstrates that you have container level access</span></span>

8.  <span data-ttu-id="8344c-460">Oluşturulan erişimin imza URI çalıştığı paylaşılan emin olmak için tarayıcıda sınayın.</span><span class="sxs-lookup"><span data-stu-id="8344c-460">To ensure that the generated shared access signature URI works, test it in browser.</span></span> <span data-ttu-id="8344c-461">Yükleme işlemini başlatmak</span><span class="sxs-lookup"><span data-stu-id="8344c-461">It should start the download process</span></span>

9.  <span data-ttu-id="8344c-462">Paylaşılan erişim imzası URI kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="8344c-462">Copy the shared access signature URI.</span></span> <span data-ttu-id="8344c-463">Bu, Yayımlama Portalı'na yapıştırılacak olan URI'dir.</span><span class="sxs-lookup"><span data-stu-id="8344c-463">This is the URI to paste into the Publishing Portal.</span></span>

10. <span data-ttu-id="8344c-464">SKU'daki her VHD için bu adımları tekrarlayın.</span><span class="sxs-lookup"><span data-stu-id="8344c-464">Repeat these steps for each VHD in the SKU.</span></span>


### <a name="53-provide-information-about-the-vm-image-and-request-certification-in-the-publishing-portal"></a><span data-ttu-id="8344c-465">5.3 VM görüntü ile ilgili bilgileri sağlayın ve yayımlama portalında sertifika isteği</span><span class="sxs-lookup"><span data-stu-id="8344c-465">5.3 Provide information about the VM image and request certification in the Publishing Portal</span></span>
<span data-ttu-id="8344c-466">Teklif ve SKU oluşturduktan sonra SKU ile ilişkili görüntü ayrıntıları girmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="8344c-466">After you have created your offer and SKU, you should enter the image details associated with that SKU:</span></span>

1. <span data-ttu-id="8344c-467">Git [yayımlama portalında][link-pubportal]ve satıcının hesabınızla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="8344c-467">Go to the [Publishing Portal][link-pubportal], and then sign in with your seller account.</span></span>
2. <span data-ttu-id="8344c-468">Seçin **VM görüntüleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="8344c-468">Select the **VM images** tab.</span></span>
3. <span data-ttu-id="8344c-469">Sayfanın başında listelenen tanımlayıcısı gerçekte teklif tanımlayıcısı ve SKU tanımlayıcısı değil.</span><span class="sxs-lookup"><span data-stu-id="8344c-469">The identifier listed at the top of the page is actually the offer identifier and not the SKU identifier.</span></span>
4. <span data-ttu-id="8344c-470">Özellikleri altında doldurmak **SKU'ları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="8344c-470">Fill out the properties under the **SKUs** section.</span></span>
5. <span data-ttu-id="8344c-471">Altında **işletim sistemi ailesi**, işletim sistemi VHD ile ilişkili işletim sisteminin türünü tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8344c-471">Under **Operating system family**, click the operating system type associated with the operating system VHD.</span></span>
6. <span data-ttu-id="8344c-472">İçinde **işletim sistemi** kutusunda, işletim sistemi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="8344c-472">In the **Operating system** box, describe the operating system.</span></span> <span data-ttu-id="8344c-473">İşletim sistemi ailesi, türü, sürüm ve güncelleştirmeler gibi bir biçim göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="8344c-473">Consider a format such as operating system family, type, version, and updates.</span></span> <span data-ttu-id="8344c-474">"Windows Server Datacenter 2014 R2." örneğidir</span><span class="sxs-lookup"><span data-stu-id="8344c-474">An example is "Windows Server Datacenter 2014 R2."</span></span>
7. <span data-ttu-id="8344c-475">En fazla altı önerilen sanal makine boyutlarını seçin.</span><span class="sxs-lookup"><span data-stu-id="8344c-475">Select up to six recommended virtual machine sizes.</span></span> <span data-ttu-id="8344c-476">Bu satın alıp, görüntüyü dağıtmak karar görüntülenen Azure Portalı'nda fiyatlandırma katmanı dikey penceresinde müşteriye önerilerdir.</span><span class="sxs-lookup"><span data-stu-id="8344c-476">These are recommendations that get displayed to the customer in the Pricing tier blade in the Azure Portal when they decide to purchase and deploy your image.</span></span> <span data-ttu-id="8344c-477">**Bunlar yalnızca önerilerdir. Müşteri yansımanıza belirtilen diskleri düzenler herhangi bir VM boyutu seçebilirsiniz.**</span><span class="sxs-lookup"><span data-stu-id="8344c-477">**These are only recommendations. The customer is able to select any VM size that accommodates the disks specified in your image.**</span></span>
8. <span data-ttu-id="8344c-478">Sürümü girin.</span><span class="sxs-lookup"><span data-stu-id="8344c-478">Enter the version.</span></span> <span data-ttu-id="8344c-479">Sürüm alanı ürünü ve onun güncelleştirmeleri tanımlamak için bir anlamsal sürüm yalıtır:</span><span class="sxs-lookup"><span data-stu-id="8344c-479">The version field encapsulates a semantic version to identify the product and its updates:</span></span>
   * <span data-ttu-id="8344c-480">Sürümleri X, Y ve Z tamsayılar nerede X.Y.Z biçiminde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8344c-480">Versions should be of the form X.Y.Z, where X, Y, and Z are integers.</span></span>
   * <span data-ttu-id="8344c-481">Farklı SKU'ları görüntülerinde farklı birincil ve ikincil sürümleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="8344c-481">Images in different SKUs can have different major and minor versions.</span></span>
   * <span data-ttu-id="8344c-482">İçinde bir SKU sürümlerinde yalnızca düzeltme eki sürümü (Z X.Y.Z gelen) artırmak artımlı değişiklikler olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8344c-482">Versions within a SKU should only be incremental changes, which increase the patch version (Z from X.Y.Z).</span></span>
9. <span data-ttu-id="8344c-483">İçinde **OS VHD URL'si** kutusunda, işletim sistemi VHD için oluşturulan URI paylaşılan erişim imzası girin.</span><span class="sxs-lookup"><span data-stu-id="8344c-483">In the **OS VHD URL** box, enter the shared access signature URI created for the operating system VHD.</span></span>
10. <span data-ttu-id="8344c-484">Bu SKU ile ilişkili veri disklerinin varsa, bu veri diski dağıtım takılı istediğiniz mantıksal birim numarası (LUN) seçin.</span><span class="sxs-lookup"><span data-stu-id="8344c-484">If there are data disks associated with this SKU, select the logical unit number (LUN) to which you would like this data disk to be mounted upon deployment.</span></span>
11. <span data-ttu-id="8344c-485">İçinde **LUN X VHD URL'si** kutusuna, ilk veri VHD için oluşturulan URI paylaşılan erişim imzası girin.</span><span class="sxs-lookup"><span data-stu-id="8344c-485">In the **LUN X VHD URL** box, enter the shared access signature URI created for the first data VHD.</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-3.png)


## <a name="common-sas-url-issues--fixes"></a><span data-ttu-id="8344c-487">Ortak SAS URL sorunları ve düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="8344c-487">Common SAS URL issues & fixes</span></span>

|<span data-ttu-id="8344c-488">Sorun</span><span class="sxs-lookup"><span data-stu-id="8344c-488">Issue</span></span>|<span data-ttu-id="8344c-489">Hata iletisi</span><span class="sxs-lookup"><span data-stu-id="8344c-489">Failure Message</span></span>|<span data-ttu-id="8344c-490">Düzeltme</span><span class="sxs-lookup"><span data-stu-id="8344c-490">Fix</span></span>|<span data-ttu-id="8344c-491">Belge bağlantı</span><span class="sxs-lookup"><span data-stu-id="8344c-491">Documentation Link</span></span>|
|---|---|---|---|
|<span data-ttu-id="8344c-492">Kopyalama hatası görüntüleri - "?" SAS URL'si bulunamadı</span><span class="sxs-lookup"><span data-stu-id="8344c-492">Failure in copying images - "?" is not found in SAS url</span></span>|<span data-ttu-id="8344c-493">Hata: Görüntüleri kopyalama.</span><span class="sxs-lookup"><span data-stu-id="8344c-493">Failure: Copying Images.</span></span> <span data-ttu-id="8344c-494">Blob SAS URI'sini sağlanan kullanarak indirmek erişilemiyor.</span><span class="sxs-lookup"><span data-stu-id="8344c-494">Not able to download blob using provided SAS Uri.</span></span>|<span data-ttu-id="8344c-495">Önerilen SAS URL'yi kullanarak güncelleştirme araçları</span><span class="sxs-lookup"><span data-stu-id="8344c-495">Update the SAS Url using recommended tools</span></span>|[<span data-ttu-id="8344c-496">https://Azure.microsoft.com/en-us/documentation/articles/Storage-dotnet-Shared-Access-Signature-Part-1/</span><span class="sxs-lookup"><span data-stu-id="8344c-496">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="8344c-497">Görüntüleri kopyalama hatası - SAS URL'si değil, "st" ve "se" parametreleri</span><span class="sxs-lookup"><span data-stu-id="8344c-497">Failure in copying images - “st” and “se” parameters not in SAS url</span></span>|<span data-ttu-id="8344c-498">Hata: Görüntüleri kopyalama.</span><span class="sxs-lookup"><span data-stu-id="8344c-498">Failure: Copying Images.</span></span> <span data-ttu-id="8344c-499">Blob SAS URI'sini sağlanan kullanarak indirmek erişilemiyor.</span><span class="sxs-lookup"><span data-stu-id="8344c-499">Not able to download blob using provided SAS Uri.</span></span>|<span data-ttu-id="8344c-500">Başlangıç ve bitiş tarihleri üzerindeki ile SAS Url güncelleştir</span><span class="sxs-lookup"><span data-stu-id="8344c-500">Update the SAS Url with Start and End dates on it</span></span>|[<span data-ttu-id="8344c-501">https://Azure.microsoft.com/en-us/documentation/articles/Storage-dotnet-Shared-Access-Signature-Part-1/</span><span class="sxs-lookup"><span data-stu-id="8344c-501">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="8344c-502">Görüntüleri - "sp rl SAS url değil =" kopyalama hatası</span><span class="sxs-lookup"><span data-stu-id="8344c-502">Failure in copying images - “sp=rl” not in SAS url</span></span>|<span data-ttu-id="8344c-503">Hata: Görüntüleri kopyalama.</span><span class="sxs-lookup"><span data-stu-id="8344c-503">Failure: Copying Images.</span></span> <span data-ttu-id="8344c-504">Blob SAS URI'sini sağlanan kullanarak indirmek için</span><span class="sxs-lookup"><span data-stu-id="8344c-504">Not able to download blob using provided SAS Uri</span></span>|<span data-ttu-id="8344c-505">SAS Url "listeyi ve"Okuma"ayarlanmış olan izinleri ile güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="8344c-505">Update the SAS Url with permissions set as “Read” & “List</span></span>|[<span data-ttu-id="8344c-506">https://Azure.microsoft.com/en-us/documentation/articles/Storage-dotnet-Shared-Access-Signature-Part-1/</span><span class="sxs-lookup"><span data-stu-id="8344c-506">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="8344c-507">Görüntüleri - SAS url kopyalama hatası vhd adlarında boşluk sahip</span><span class="sxs-lookup"><span data-stu-id="8344c-507">Failure in copying images - SAS url have white spaces in vhd name</span></span>|<span data-ttu-id="8344c-508">Hata: Görüntüleri kopyalama.</span><span class="sxs-lookup"><span data-stu-id="8344c-508">Failure: Copying Images.</span></span> <span data-ttu-id="8344c-509">Blob SAS URI'sini sağlanan kullanarak indirmek erişilemiyor.</span><span class="sxs-lookup"><span data-stu-id="8344c-509">Not able to download blob using provided SAS Uri.</span></span>|<span data-ttu-id="8344c-510">Güncelleştirme boşluk olmadan SAS URL'si</span><span class="sxs-lookup"><span data-stu-id="8344c-510">Update the SAS Url without white spaces</span></span>|[<span data-ttu-id="8344c-511">https://Azure.microsoft.com/en-us/documentation/articles/Storage-dotnet-Shared-Access-Signature-Part-1/</span><span class="sxs-lookup"><span data-stu-id="8344c-511">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="8344c-512">Görüntüleri – SAS Url yetkilendirmesi hata kopyalama hatası</span><span class="sxs-lookup"><span data-stu-id="8344c-512">Failure in copying images – SAS Url Authorization error</span></span>|<span data-ttu-id="8344c-513">Hata: Görüntüleri kopyalama.</span><span class="sxs-lookup"><span data-stu-id="8344c-513">Failure: Copying Images.</span></span> <span data-ttu-id="8344c-514">Yetkilendirme hatası nedeniyle blob indirmek için</span><span class="sxs-lookup"><span data-stu-id="8344c-514">Not able to download blob due to authorization error</span></span>|<span data-ttu-id="8344c-515">SAS Url yeniden oluştur</span><span class="sxs-lookup"><span data-stu-id="8344c-515">Regenerate the SAS Url</span></span>|[<span data-ttu-id="8344c-516">https://Azure.microsoft.com/en-us/documentation/articles/Storage-dotnet-Shared-Access-Signature-Part-1/</span><span class="sxs-lookup"><span data-stu-id="8344c-516">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|


## <a name="next-step"></a><span data-ttu-id="8344c-517">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="8344c-517">Next step</span></span>
<span data-ttu-id="8344c-518">SKU ayrıntılarla tamamladıktan sonra İleri taşıyabilirsiniz [Azure Marketi pazarlama içerik Kılavuzu][link-pushstaging].</span><span class="sxs-lookup"><span data-stu-id="8344c-518">After you are done with the SKU details, you can move forward to the [Azure Marketplace marketing content guide][link-pushstaging].</span></span> <span data-ttu-id="8344c-519">Yayımlama işleminin bu adımında pazarlama içeriği, fiyatlandırma ve öncesinde gerekli diğer bilgileri sağladığınız **adım 3: VM sınama teklif hazırlamada**, burada dağıtmadan önce çeşitli kullanım örneği senaryolarını test Genel görünürlük ve satın alma için Azure Marketi sunar.</span><span class="sxs-lookup"><span data-stu-id="8344c-519">In that step of the publishing process, you provide the marketing content, pricing, and other information necessary prior to **Step 3: Testing your VM offer in staging**, where you test various use-case scenarios before deploying the offer to the Azure Marketplace for public visibility and purchase.</span></span>  

## <a name="see-also"></a><span data-ttu-id="8344c-520">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="8344c-520">See also</span></span>
* [<span data-ttu-id="8344c-521">Başlarken: bir teklifi Azure Marketinde yayımlama</span><span class="sxs-lookup"><span data-stu-id="8344c-521">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

[img-acom-1]:media/marketplace-publishing-vm-image-creation/vm-image-acom-datacenter.png
[img-portal-vm-size]:media/marketplace-publishing-vm-image-creation/vm-image-portal-size.png
[img-portal-vm-create]:media/marketplace-publishing-vm-image-creation/vm-image-portal-create-vm.png
[img-portal-vm-location]:media/marketplace-publishing-vm-image-creation/vm-image-portal-location.png
[img-portal-vm-rdp]:media/marketplace-publishing-vm-image-creation/vm-image-portal-rdp.png
[img-azstg-add]:media/marketplace-publishing-vm-image-creation/vm-image-storage-add.png
[img-manage-vm-new]:media/marketplace-publishing-vm-image-creation/vm-image-manage-new.png
[img-manage-vm-select]:media/marketplace-publishing-vm-image-creation/vm-image-manage-select.png
[img-cert-vm-key-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-keyfile-linux.png
[img-cert-vm-pswd-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-linux.png
[img-cert-vm-pswd-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-win.png
[img-cert-vm-test-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-linux.png
[img-cert-vm-test-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-win.png
[img-cert-vm-results]:media/marketplace-publishing-vm-image-creation/vm-image-certification-results.png
[img-cert-vm-questionnaire]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire.png
[img-cert-vm-questionnaire-2]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire-2.png
[img-pubportal-vm-skus]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus.png
[img-pubportal-vm-skus-2]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-2.png

[link-pushstaging]:marketplace-publishing-push-to-staging.md
[link-github-waagent]:https://github.com/Azure/WALinuxAgent
[link-azure-codeplex]:https://azurestorageexplorer.codeplex.com/
[link-azure-2]:../storage/blobs/storage-dotnet-shared-access-signature-part-2.md
[link-azure-1]:../storage/common/storage-dotnet-shared-access-signature-part-1.md
[link-msft-download]:http://www.microsoft.com/download/details.aspx?id=44299
[link-technet-3]:https://technet.microsoft.com/library/hh846766.aspx
[link-technet-2]:https://msdn.microsoft.com/library/dn495261.aspx
[link-azure-portal]:https://portal.azure.com
[link-pubportal]:https://publish.windowsazure.com
[link-sql-2014-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014enterprisewindowsserver2012r2/
[link-sql-2014-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014standardwindowsserver2012r2/
[link-sql-2014-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014webwindowsserver2012r2/
[link-sql-2012-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2enterprisewindowsserver2012/
[link-sql-2012-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2standardwindowsserver2012/
[link-sql-2012-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2webwindowsserver2012/
[link-datactr-2012-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012r2datacenter/
[link-datactr-2012]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012datacenter/
[link-datactr-2008-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2008r2sp1/
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-technet-1]:https://technet.microsoft.com/library/hh848454.aspx
[link-azure-vm-2]:./virtual-machines-linux-agent-user-guide/
[link-openssl]:https://www.openssl.org/
[link-intsvc]:http://www.microsoft.com/download/details.aspx?id=41554
[link-python]:https://www.python.org/
