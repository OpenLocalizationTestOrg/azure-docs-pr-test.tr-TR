---
title: "aaaCreating hello Azure Marketi için bir sanal makine görüntüsü | Microsoft Docs"
description: "Nasıl toocreate bir sanal makine görüntü hello Azure Marketi başkaları için toopurchase ayrıntılı yönergeler için."
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
ms.openlocfilehash: 65e1c0530bb050fb379a52544e36c55faacd84df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-virtual-machine-image-for-hello-azure-marketplace"></a><span data-ttu-id="d6bf4-103">Kılavuzu toocreate hello Azure Marketi için bir sanal makine görüntüsü</span><span class="sxs-lookup"><span data-stu-id="d6bf4-103">Guide toocreate a virtual machine image for hello Azure Marketplace</span></span>
<span data-ttu-id="d6bf4-104">Bu makalede **2. adım**, hello sanal sabit diskleri (VHD) toohello Azure Marketi dağıtacağınız hazırlama aracılığıyla anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-104">This article, **Step 2**, walks you through preparing hello virtual hard disks (VHDs) that you will deploy toohello Azure Marketplace.</span></span> <span data-ttu-id="d6bf4-105">Vhd'lerinizi, sku'sunun hello temelidir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-105">Your VHDs are hello foundation of your SKU.</span></span> <span data-ttu-id="d6bf4-106">Hello işlemi, bir Windows tabanlı veya Linux tabanlı SKU olup sağlanmaktadır bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-106">hello process differs depending on whether you are providing a Linux-based or Windows-based SKU.</span></span> <span data-ttu-id="d6bf4-107">Bu makalede her iki senaryoyu ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-107">This article covers both scenarios.</span></span> <span data-ttu-id="d6bf4-108">Bu işlem ile paralel olarak gerçekleştirilebilir [hesap oluşturma ve kayıt][link-acct-creation].</span><span class="sxs-lookup"><span data-stu-id="d6bf4-108">This process can be performed in parallel with [Account creation and registration][link-acct-creation].</span></span>

## <a name="1-define-offers-and-skus"></a><span data-ttu-id="d6bf4-109">1. Teklifler ve SKU'ları tanımlayın</span><span class="sxs-lookup"><span data-stu-id="d6bf4-109">1. Define Offers and SKUs</span></span>
<span data-ttu-id="d6bf4-110">Bu bölümde, toodefine hello sunar ve ilişkili SKU'ları öğrenin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-110">In this section, you learn toodefine hello offers and their associated SKUs.</span></span>

<span data-ttu-id="d6bf4-111">Bir teklif, SKU "üst" tooall geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-111">An offer is a "parent" tooall of its SKUs.</span></span> <span data-ttu-id="d6bf4-112">Birden çok teklife sahip olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-112">You can have multiple offers.</span></span> <span data-ttu-id="d6bf4-113">Toostructure karar nasıl Teklifleriniz tooyou olur.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-113">How you decide toostructure your offers is up tooyou.</span></span> <span data-ttu-id="d6bf4-114">Bir teklif toostaging gönderildiğinde tüm kendi SKU'ları ile birlikte gönderilir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-114">When an offer is pushed toostaging, it is pushed along with all of its SKUs.</span></span> <span data-ttu-id="d6bf4-115">Dikkatli bir şekilde hello URL'de görünür olacağından, SKU tanımlayıcıları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="d6bf4-115">Carefully consider your SKU identifiers, because they will be visible in hello URL:</span></span>

* <span data-ttu-id="d6bf4-116">Azure.com: http://azure.microsoft.com/marketplace/partners/ {PartnerNamespace} / {OfferIdentifier}-{SKUidentifier}</span><span class="sxs-lookup"><span data-stu-id="d6bf4-116">Azure.com: http://azure.microsoft.com/marketplace/partners/{PartnerNamespace}/{OfferIdentifier}-{SKUidentifier}</span></span>
* <span data-ttu-id="d6bf4-117">Azure Önizleme portalı: https://portal.azure.com/#gallery/ {PublisherNamespace}. {OfferIdentifier} {SKUIDdentifier}</span><span class="sxs-lookup"><span data-stu-id="d6bf4-117">Azure preview portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{SKUIDdentifier}</span></span>  

<span data-ttu-id="d6bf4-118">Bir SKU hello ticari bir VM görüntüsü adıdır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-118">A SKU is hello commercial name for a VM image.</span></span> <span data-ttu-id="d6bf4-119">Bir VM görüntüsü içeren bir işletim sistemi diski ve sıfır veya daha fazla veri diski.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-119">A VM image contains one operating system disk and zero or more data disks.</span></span> <span data-ttu-id="d6bf4-120">Temelde hello tam depolama profili için bir sanal makine içindir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-120">It is essentially hello complete storage profile for a virtual machine.</span></span> <span data-ttu-id="d6bf4-121">Bir VHD her disk için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-121">One VHD is needed per disk.</span></span> <span data-ttu-id="d6bf4-122">Bile boş veri diskleri oluşturulan bir VHD toobe gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-122">Even blank data disks require a VHD toobe created.</span></span>

<span data-ttu-id="d6bf4-123">Hangi işletim sistemine bağımsız olarak, yalnızca az sayıda veri diski hello SKU tarafından gerekli hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-123">Regardless of which operating system you use, add only hello minimum number of data disks needed by hello SKU.</span></span> <span data-ttu-id="d6bf4-124">Müşteriler görüntünün bir parçasını hello dağıtım zamanında disklerinin kaldırılamıyor ancak bunları ihtiyacınız varsa her zaman diskleri sırasında veya dağıtımdan sonra ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-124">Customers cannot remove disks that are part of an image at hello time of deployment but can always add disks during or after deployment if they need them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6bf4-125">**Yeni bir görüntü sürümü disk sayısı değiştirmeyin.**</span><span class="sxs-lookup"><span data-stu-id="d6bf4-125">**Do not change disk count in a new image version.**</span></span> <span data-ttu-id="d6bf4-126">Merhaba görüntüsü'ndeki veri disklerinin yeniden yapılandırmanız gerekir, yeni bir SKU tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-126">If you must reconfigure Data disks in hello image, define a new SKU.</span></span> <span data-ttu-id="d6bf4-127">Yeni bir görüntü sürümü farklı bir disk sayıları ile yayımlama hello yeni resim sürümünü otomatik ölçeklendirme, otomatik dağıtımları ARM şablonları ve diğer senaryolar aracılığıyla çözümlerinin durumlarda göre yeni dağıtım sonu, hello olası sahip olur.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-127">Publishing a new image version with different disk counts will have hello potential of breaking new deployment based on hello new image version in cases of auto-scaling, automatic deployments of solutions through ARM templates and other scenarios.</span></span>
>
>

### <a name="11-add-an-offer"></a><span data-ttu-id="d6bf4-128">1.1 bir teklif ekleyin</span><span class="sxs-lookup"><span data-stu-id="d6bf4-128">1.1 Add an offer</span></span>
1. <span data-ttu-id="d6bf4-129">İçinde toohello oturum [yayımlama portalında] [ link-pubportal] seller hesabınızı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-129">Sign in toohello [Publishing Portal][link-pubportal] by using your seller account.</span></span>
2. <span data-ttu-id="d6bf4-130">Select hello **sanal makineleri** hello yayımlama portalında sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-130">Select hello **Virtual Machines** tab of hello Publishing Portal.</span></span> <span data-ttu-id="d6bf4-131">Merhaba istendiğinde giriş alanına teklif adınızı girin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-131">In hello prompted entry field, enter your offer name.</span></span> <span data-ttu-id="d6bf4-132">Merhaba teklif adı genellikle hello hello ürün veya hizmet hello Azure Marketi toosell planlama adıdır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-132">hello offer name is typically hello name of hello product or service that you plan toosell in hello Azure Marketplace.</span></span>
3. <span data-ttu-id="d6bf4-133">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-133">Select **Create**.</span></span>

### <a name="12-define-a-sku"></a><span data-ttu-id="d6bf4-134">1.2 bir SKU tanımlayın</span><span class="sxs-lookup"><span data-stu-id="d6bf4-134">1.2 Define a SKU</span></span>
<span data-ttu-id="d6bf4-135">Bir teklif ekledikten sonra toodefine gerekir ve, SKU'ları tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-135">After you have added an offer, you need toodefine and identify your SKUs.</span></span> <span data-ttu-id="d6bf4-136">Birden çok teklifleri olabilir ve her teklif birden çok SKU'ları altındaki olabilir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-136">You can have multiple offers, and each offer can have multiple SKUs under it.</span></span> <span data-ttu-id="d6bf4-137">Bir teklif toostaging gönderildiğinde tüm kendi SKU'ları ile birlikte gönderilir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-137">When an offer is pushed toostaging, it is pushed along with all of its SKUs.</span></span>

1. <span data-ttu-id="d6bf4-138">**Bir SKU ekleyin.**</span><span class="sxs-lookup"><span data-stu-id="d6bf4-138">**Add a SKU.**</span></span> <span data-ttu-id="d6bf4-139">Merhaba SKU hello URL'SİNDE kullanılan bir tanımlayıcı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-139">hello SKU requires an identifier, which is used in hello URL.</span></span> <span data-ttu-id="d6bf4-140">Hello tanımlayıcı yayımlama profili içinde benzersiz olmalıdır, ancak diğer yayımcı ile tanımlayıcı çakışma riski vardır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-140">hello identifier must be unique within your publishing profile, but there is no risk of identifier collision with other publishers.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d6bf4-141">Merhaba teklif ve SKU tanımlayıcıları hello teklif hello Market URL'de görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-141">hello offer and SKU identifiers are displayed in hello offer URL in hello Marketplace.</span></span>
   >
   >
2. <span data-ttu-id="d6bf4-142">**SKU için Özet açıklama ekleyin.**</span><span class="sxs-lookup"><span data-stu-id="d6bf4-142">**Add a summary description for your SKU.**</span></span> <span data-ttu-id="d6bf4-143">Özet açıklamaları görünür toocustomers olduğundan, kolay okunabilir yapmanız.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-143">Summary descriptions are visible toocustomers, so you should make them easily readable.</span></span> <span data-ttu-id="d6bf4-144">Bu bilgiler hello "Anında iletme tooStaging" aşamasında kadar kilitli toobe gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-144">This information does not need toobe locked until hello "Push tooStaging" phase.</span></span> <span data-ttu-id="d6bf4-145">Ücretsiz tooedit olduğunuz o zamana kadar bu.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-145">Until then, you are free tooedit it.</span></span>
3. <span data-ttu-id="d6bf4-146">Windows tabanlı SKU'ları kullanıyorsanız, hello önerilen bağlantıları izleyin tooacquire hello Windows Server sürümlerinde olduğu onaylandı.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-146">If you are using Windows-based SKUs, follow hello suggested links tooacquire hello approved versions of Windows Server.</span></span>

## <a name="2-create-an-azure-compatible-vhd-linux-based"></a><span data-ttu-id="d6bf4-147">2. (Linux tabanlı) bir Azure uyumlu VHD oluşturma</span><span class="sxs-lookup"><span data-stu-id="d6bf4-147">2. Create an Azure-compatible VHD (Linux-based)</span></span>
<span data-ttu-id="d6bf4-148">Bu bölümde hello Azure Marketi için bir Linux tabanlı VM görüntüsü oluşturmak için en iyi uygulamalar odaklanır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-148">This section focuses on best practices for creating a Linux-based VM image for hello Azure Marketplace.</span></span> <span data-ttu-id="d6bf4-149">Bir adım adım kılavuz için belgeleri aşağıdaki toohello bakın: [oluşturma ve bir Sanal Sabit Disk, CONTAINS karşıya hello Linux işletim sistemi](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="d6bf4-149">For a step-by-step walkthrough, refer toohello following documentation: [Creating and Uploading a Virtual Hard Disk that Contains hello Linux Operating System](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

## <a name="3-create-an-azure-compatible-vhd-windows-based"></a><span data-ttu-id="d6bf4-150">3. (Windows tabanlı) bir Azure uyumlu VHD oluşturma</span><span class="sxs-lookup"><span data-stu-id="d6bf4-150">3. Create an Azure-compatible VHD (Windows-based)</span></span>
<span data-ttu-id="d6bf4-151">Bu bölümde Azure Marketi hello için Windows Server tabanlı bir SKU hello adımları toocreate odaklanır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-151">This section focuses on hello steps toocreate a SKU based on Windows Server for hello Azure Marketplace.</span></span>

### <a name="31-ensure-that-you-are-using-hello-correct-base-vhds"></a><span data-ttu-id="d6bf4-152">Hello kullandığınız 3.1 olun temel VHD düzeltin</span><span class="sxs-lookup"><span data-stu-id="d6bf4-152">3.1 Ensure that you are using hello correct base VHDs</span></span>
<span data-ttu-id="d6bf4-153">Merhaba işletim sistemi VHD VM görüntüsü için Windows Server veya SQL Server içeren Azure onaylı temel görüntüde dayalı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-153">hello operating system VHD for your VM image must be based on an Azure-approved base image that contains Windows Server or SQL Server.</span></span>

<span data-ttu-id="d6bf4-154">toobegin, görüntüler, hello bulunan aşağıdaki hello birinden bir VM oluşturma [Microsoft Azure portal][link-azure-portal]:</span><span class="sxs-lookup"><span data-stu-id="d6bf4-154">toobegin, create a VM from one of hello following images, located at hello [Microsoft Azure portal][link-azure-portal]:</span></span>

* <span data-ttu-id="d6bf4-155">Windows Server ([2012 R2 Datacenter][link-datactr-2012-r2], [2012 Datacenter][link-datactr-2012], [2008 R2 SP1] [link-datactr-2008-r2])</span><span class="sxs-lookup"><span data-stu-id="d6bf4-155">Windows Server ([2012 R2 Datacenter][link-datactr-2012-r2], [2012 Datacenter][link-datactr-2012], [2008 R2 SP1][link-datactr-2008-r2])</span></span>
* <span data-ttu-id="d6bf4-156">SQL Server 2014 ([Kurumsal][link-sql-2014-ent], [standart][link-sql-2014-std], [Web] [ link-sql-2014-web])</span><span class="sxs-lookup"><span data-stu-id="d6bf4-156">SQL Server 2014 ([Enterprise][link-sql-2014-ent], [Standard][link-sql-2014-std], [Web][link-sql-2014-web])</span></span>
* <span data-ttu-id="d6bf4-157">SQL Server 2012 SP2'yi ([Kurumsal][link-sql-2012-ent], [standart][link-sql-2012-std], [Web] [ link-sql-2012-web])</span><span class="sxs-lookup"><span data-stu-id="d6bf4-157">SQL Server 2012 SP2 ([Enterprise][link-sql-2012-ent], [Standard][link-sql-2012-std], [Web][link-sql-2012-web])</span></span>

<span data-ttu-id="d6bf4-158">Bu bağlantılar da hello yayımlama portalında hello SKU sayfanın altında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-158">These links can also be found in hello Publishing Portal under hello SKU page.</span></span>

> [!TIP]
> <span data-ttu-id="d6bf4-159">Merhaba geçerli Azure portal veya PowerShell kullanıyorsanız, Windows Server görüntülerini 8 Eylül 2014 yayınlanan ve üzeri onaylanır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-159">If you are using hello current Azure portal or PowerShell, Windows Server images published on September 8, 2014 and later are approved.</span></span>
>
>

### <a name="32-create-your-windows-based-vm"></a><span data-ttu-id="d6bf4-160">3.2, Windows tabanlı VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="d6bf4-160">3.2 Create your Windows-based VM</span></span>
<span data-ttu-id="d6bf4-161">Merhaba Microsoft Azure Portal'dan, yalnızca birkaç basit adımda onaylanmış bir temel görüntü göre VM oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-161">From hello Microsoft Azure portal, you can create your VM based on an approved base image in just a few simple steps.</span></span> <span data-ttu-id="d6bf4-162">Merhaba, hello işlemine genel bakış verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d6bf4-162">hello following is an overview of hello process:</span></span>

1. <span data-ttu-id="d6bf4-163">Merhaba temel görüntü sayfasında seçin **sanal makine oluşturma** toobe toohello yeni yönlendirilmiş [Microsoft Azure portal][link-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="d6bf4-163">From hello base image page, select **Create Virtual Machine** toobe directed toohello new [Microsoft Azure portal][link-azure-portal].</span></span>

    ![Çizim][img-acom-1]
2. <span data-ttu-id="d6bf4-165">Merhaba Microsoft hesabı ile toohello portal ve parolayı hello toouse istediğiniz Azure aboneliği için oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-165">Sign in toohello portal with hello Microsoft account and password for hello Azure subscription you want toouse.</span></span>
3. <span data-ttu-id="d6bf4-166">Seçtiğiniz hello temel görüntü kullanılarak Hello istemleri toocreate VM izleyin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-166">Follow hello prompts toocreate a VM by using hello base image you have selected.</span></span> <span data-ttu-id="d6bf4-167">Tooprovide bir ana bilgisayar adı (Merhaba bilgisayar adı), (yönetici olarak kayıtlı) kullanıcı adı ve parola Merhaba VM gerekir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-167">You need tooprovide a host name (name of hello computer), user name (registered as an administrator), and password for hello VM.</span></span>

    ![Çizim][img-portal-vm-create]
4. <span data-ttu-id="d6bf4-169">Merhaba VM toodeploy Hello boyutunu seçin:</span><span class="sxs-lookup"><span data-stu-id="d6bf4-169">Select hello size of hello VM toodeploy:</span></span>

    <span data-ttu-id="d6bf4-170">a.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-170">a.</span></span>    <span data-ttu-id="d6bf4-171">Toodevelop hello VHD şirket içi planlıyorsanız, hello boyutu önemli değildir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-171">If you plan toodevelop hello VHD on-premises, hello size does not matter.</span></span> <span data-ttu-id="d6bf4-172">Merhaba birini kullanmayı daha küçük VM'ler.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-172">Consider using one of hello smaller VMs.</span></span>

    <span data-ttu-id="d6bf4-173">b.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-173">b.</span></span>    <span data-ttu-id="d6bf4-174">Toodevelop hello Azure görüntüde planlıyorsanız, VM boyutları hello seçilen görüntü için önerilen hello birini kullanarak göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-174">If you plan toodevelop hello image in Azure, consider using one of hello recommended VM sizes for hello selected image.</span></span>

    <span data-ttu-id="d6bf4-175">c.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-175">c.</span></span>    <span data-ttu-id="d6bf4-176">Fiyatlandırma bilgileri için toohello başvuran **fiyatlandırma katmanlarına önerilen** hello portalında görüntülenen Seçici.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-176">For pricing information, refer toohello **Recommended pricing tiers** selector displayed on hello portal.</span></span> <span data-ttu-id="d6bf4-177">Bunu hello hello yayımcı tarafından sağlanan üç önerilen boyut sağlar.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-177">It will provide hello three recommended sizes provided by hello publisher.</span></span> <span data-ttu-id="d6bf4-178">(Bu durumda, Microsoft hello yayımcı olur.)</span><span class="sxs-lookup"><span data-stu-id="d6bf4-178">(In this case, hello publisher is Microsoft.)</span></span>

    ![Çizim][img-portal-vm-size]
5. <span data-ttu-id="d6bf4-180">Özellikleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="d6bf4-180">Set properties:</span></span>

    <span data-ttu-id="d6bf4-181">a.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-181">a.</span></span>    <span data-ttu-id="d6bf4-182">Hızlı dağıtım için hello altında hello özellikleri için varsayılan değer bırakabilirsiniz **isteğe bağlı yapılandırma** ve **kaynak grubu**.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-182">For quick deployment, you can leave hello default values for hello properties under **Optional Configuration** and **Resource Group**.</span></span>

    <span data-ttu-id="d6bf4-183">b.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-183">b.</span></span>    <span data-ttu-id="d6bf4-184">Altında **depolama hesabı**, hello depolama hesabı işletim sistemi hangi hello VHD depolanacağı isteğe bağlı olarak seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-184">Under **Storage Account**, you can optionally select hello storage account in which hello operating system VHD will be stored.</span></span>

    <span data-ttu-id="d6bf4-185">c.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-185">c.</span></span>    <span data-ttu-id="d6bf4-186">Altında **kaynak grubu**, isteğe bağlı olarak hangi tooplace hello VM hello mantıksal grup seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-186">Under **Resource Group**, you can optionally select hello logical group in which tooplace hello VM.</span></span>
6. <span data-ttu-id="d6bf4-187">Select hello **konumu** dağıtımı için:</span><span class="sxs-lookup"><span data-stu-id="d6bf4-187">Select hello **Location** for deployment:</span></span>

    <span data-ttu-id="d6bf4-188">a.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-188">a.</span></span>    <span data-ttu-id="d6bf4-189">Toodevelop hello VHD şirket içi planlıyorsanız, hello görüntü tooAzure daha sonra karşıya yükleyecek çünkü hello konumu önemli değildir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-189">If you plan toodevelop hello VHD on-premises, hello location does not matter because you will upload hello image tooAzure later.</span></span>

    <span data-ttu-id="d6bf4-190">b.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-190">b.</span></span>    <span data-ttu-id="d6bf4-191">Toodevelop hello Azure görüntüde planlıyorsanız, hello ABD tabanlı Microsoft Azure bölgelerinden hello başından kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-191">If you plan toodevelop hello image in Azure, consider using one of hello US-based Microsoft Azure regions from hello beginning.</span></span> <span data-ttu-id="d6bf4-192">Bu sertifika için görüntünüzü gönderdiğinizde, Microsoft sizin adınıza gerçekleştiren hello VHD kopyalama işlemini hızlandırır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-192">This speeds up hello VHD copying process that Microsoft performs on your behalf when you submit your image for certification.</span></span>

    ![Çizim][img-portal-vm-location]
7. <span data-ttu-id="d6bf4-194">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-194">Click **Create**.</span></span> <span data-ttu-id="d6bf4-195">Merhaba VM toodeploy başlatır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-195">hello VM starts toodeploy.</span></span> <span data-ttu-id="d6bf4-196">Dakika içinde başarılı bir dağıtım sahip olur ve toocreate hello görüntü SKU için başlayabilir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-196">Within minutes, you will have a successful deployment and can begin toocreate hello image for your SKU.</span></span>

### <a name="33-develop-your-vhd-in-hello-cloud"></a><span data-ttu-id="d6bf4-197">3.3, VHD hello bulutta geliştirin</span><span class="sxs-lookup"><span data-stu-id="d6bf4-197">3.3 Develop your VHD in hello cloud</span></span>
<span data-ttu-id="d6bf4-198">Uzak Masaüstü Protokolü (RDP) kullanarak, VHD hello bulutta geliştirmek öneririz.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-198">We strongly recommend that you develop your VHD in hello cloud by using Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="d6bf4-199">Merhaba kullanıcı adı ve parolayla sağlama işlemi sırasında belirtilen tooRDP bağlayın.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-199">You connect tooRDP with hello user name and password specified during provisioning.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6bf4-200">VHD geliştiriyorsanız (hangi önerilmez) şirket içi, bkz: [şirket içi bir sanal makine görüntüsü oluşturma](marketplace-publishing-vm-image-creation-on-premise.md).</span><span class="sxs-lookup"><span data-stu-id="d6bf4-200">If you develop your VHD on-premises (which is not recommended), see [Creating a virtual machine image on-premises](marketplace-publishing-vm-image-creation-on-premise.md).</span></span> <span data-ttu-id="d6bf4-201">VHD indirme hello bulutta geliştiriyorsanız gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-201">Downloading your VHD is not necessary if you are developing in hello cloud.</span></span>
>
>

<span data-ttu-id="d6bf4-202">**Hello kullanarak RDP aracılığıyla bağlanma [Microsoft Azure portalı][link-azure-portal]**</span><span class="sxs-lookup"><span data-stu-id="d6bf4-202">**Connect via RDP using hello [Microsoft Azure portal][link-azure-portal]**</span></span>

1. <span data-ttu-id="d6bf4-203">Seçin **Gözat** > **VM'ler**.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-203">Select **Browse** > **VMs**.</span></span>
2. <span data-ttu-id="d6bf4-204">Merhaba sanal makineleri dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-204">hello Virtual machines blade opens.</span></span> <span data-ttu-id="d6bf4-205">Bu hello tooconnect ile istediğiniz VM çalışıyorsa ve dağıtılan VM'ler hello listeden seçip emin olun.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-205">Ensure that hello VM that you want tooconnect with is running, and then select it from hello list of deployed VMs.</span></span>
3. <span data-ttu-id="d6bf4-206">Seçili VM hello açıklayan bir dikey penceresini açar.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-206">A blade opens that describes hello selected VM.</span></span> <span data-ttu-id="d6bf4-207">Merhaba üstünde tıklatın **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-207">At hello top, click **Connect**.</span></span>
4. <span data-ttu-id="d6bf4-208">İstendiğinde tooenter hello kullanıcı adı ve sağlama işlemi sırasında belirtilen parola var.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-208">You are prompted tooenter hello user name and password that you specified during provisioning.</span></span>

<span data-ttu-id="d6bf4-209">**PowerShell kullanarak RDP aracılığıyla bağlanma**</span><span class="sxs-lookup"><span data-stu-id="d6bf4-209">**Connect via RDP using PowerShell**</span></span>

<span data-ttu-id="d6bf4-210">bir Uzak Masaüstü dosyası tooa yerel makine toodownload kullanmak hello [Get-AzureRemoteDesktopFile cmdlet'i][link-technet-2].</span><span class="sxs-lookup"><span data-stu-id="d6bf4-210">toodownload a remote desktop file tooa local machine, use hello [Get-AzureRemoteDesktopFile cmdlet][link-technet-2].</span></span> <span data-ttu-id="d6bf4-211">Bu cmdlet toouse sipariş, tooknow hello hello hizmetin adını ve hello VM adını gerekir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-211">In order toouse this cmdlet, you need tooknow hello name of hello service and name of hello VM.</span></span> <span data-ttu-id="d6bf4-212">Hello hello VM oluşturduysanız [Microsoft Azure portal][link-azure-portal], bu bilgileri VM Özellikleri'nin altında bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d6bf4-212">If you created hello VM from hello [Microsoft Azure portal][link-azure-portal], you can find this information under VM properties:</span></span>

1. <span data-ttu-id="d6bf4-213">Merhaba Microsoft Azure Portalı'nda seçin **Gözat** > **VM'ler**.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-213">In hello Microsoft Azure portal, select **Browse** > **VMs**.</span></span>
2. <span data-ttu-id="d6bf4-214">Merhaba sanal makineleri dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-214">hello Virtual machines blade opens.</span></span> <span data-ttu-id="d6bf4-215">Merhaba, dağıtılan VM seçin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-215">Select hello VM that you deployed.</span></span>
3. <span data-ttu-id="d6bf4-216">Seçili VM hello açıklayan bir dikey penceresini açar.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-216">A blade opens that describes hello selected VM.</span></span>
4. <span data-ttu-id="d6bf4-217">**Özellikler**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-217">Click **Properties**.</span></span>
5. <span data-ttu-id="d6bf4-218">Merhaba ilk hello etki alanı adı hello hizmet adı bölümüdür.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-218">hello first portion of hello domain name is hello service name.</span></span> <span data-ttu-id="d6bf4-219">Merhaba ana bilgisayar adı hello VM adıdır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-219">hello host name is hello VM name.</span></span>

    ![Çizim][img-portal-vm-rdp]
6. <span data-ttu-id="d6bf4-221">oluşturulan hello VM toohello yöneticinin yerel Masaüstü için Hello cmdlet toodownload hello RDP dosyası aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-221">hello cmdlet toodownload hello RDP file for hello created VM toohello administrator's local desktop is as follows.</span></span>

        Get‐AzureRemoteDesktopFile ‐ServiceName “baseimagevm‐6820cq00” ‐Name “BaseImageVM” –LocalPath “C:\Users\Administrator\Desktop\BaseImageVM.rdp”

<span data-ttu-id="d6bf4-222">RDP hakkında daha fazla bilgi MSDN'de hello makalesinde bulunabilir [tooan Azure VM RDP veya SSH ile bağlantı](http://msdn.microsoft.com/library/azure/dn535788.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6bf4-222">More information about RDP can be found on MSDN in hello article [Connect tooan Azure VM with RDP or SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx).</span></span>

<span data-ttu-id="d6bf4-223">**Bir VM yapılandırın ve, SKU oluşturun**</span><span class="sxs-lookup"><span data-stu-id="d6bf4-223">**Configure a VM and create your SKU**</span></span>

<span data-ttu-id="d6bf4-224">Merhaba işletim sistemi VHD indirilir sonra SKU oluşturma VM toobegin yapılandırmak ve Hyper-v kullanın.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-224">After hello operating system VHD is downloaded, use Hyper­V and configure a VM toobegin creating your SKU.</span></span> <span data-ttu-id="d6bf4-225">Ayrıntılı adımlar TechNet bağlantı aşağıdaki hello bulunabilir: [HyperV yükleme ve yapılandırma VM](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6bf4-225">Detailed steps can be found at hello following TechNet link: [Install Hyper­V and Configure a VM](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="34-choose-hello-correct-vhd-size"></a><span data-ttu-id="d6bf4-226">3.4 hello doğru VHD boyutu seçin</span><span class="sxs-lookup"><span data-stu-id="d6bf4-226">3.4 Choose hello correct VHD size</span></span>
<span data-ttu-id="d6bf4-227">VM görüntünüzdeki Hello Windows işletim sistemi VHD 128 GB sabit biçimli VHD oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-227">hello Windows operating system VHD in your VM image should be created as a 128-GB fixed-format VHD.</span></span>  

<span data-ttu-id="d6bf4-228">Merhaba fiziksel boyutu 128 GB daha az ise, hello VHD seyrek olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-228">If hello physical size is less than 128 GB, hello VHD should be sparse.</span></span> <span data-ttu-id="d6bf4-229">sağlanan hello temel Windows ve SQL Server görüntüler zaten bu gereksinimleri karşılayan, böylece hello biçimi veya hello boyutunu VHD elde hello değiştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-229">hello base Windows and SQL Server images provided already meet these requirements, so do not change hello format or hello size of hello VHD obtained.</span></span>  

<span data-ttu-id="d6bf4-230">Veri diskleri 1 TB'ye kadar büyük olabilir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-230">Data disks can be as large as 1 TB.</span></span> <span data-ttu-id="d6bf4-231">Merhaba disk boyutuna karar verirken, müşterilerin dağıtımının hello zaman içinde bir görüntü VHD'ler boyutlandırılamıyor unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-231">When deciding on hello disk size, remember that customers cannot resize VHDs within an image at hello time of deployment.</span></span> <span data-ttu-id="d6bf4-232">Veri diski VHD'leri sabit biçimli VHD oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-232">Data disk VHDs should be created as a fixed-format VHD.</span></span> <span data-ttu-id="d6bf4-233">Bunlar ayrıca seyrek olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-233">They should also be sparse.</span></span> <span data-ttu-id="d6bf4-234">Veri diskleri boş olabilir veya veri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-234">Data disks can be empty or contain data.</span></span>

### <a name="35-install-hello-latest-windows-patches"></a><span data-ttu-id="d6bf4-235">3.5 Merhaba en son Windows düzeltme eklerinin yükleyin</span><span class="sxs-lookup"><span data-stu-id="d6bf4-235">3.5 Install hello latest Windows patches</span></span>
<span data-ttu-id="d6bf4-236">Merhaba taban görüntüleri içeren hello en son düzeltme eklerinin tootheir yayımlanan tarih.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-236">hello base images contain hello latest patches up tootheir published date.</span></span> <span data-ttu-id="d6bf4-237">Merhaba işletim sistemi VHD yayımlamadan önce oluşturmuş olduğunuz, Windows Update'i çalıştırın ve tüm son kritik hello ve önemli güncelleştirmelerin yüklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-237">Before publishing hello operating system VHD you have created, ensure that Windows Update has been run and that all hello latest Critical and Important security updates have been installed.</span></span>

### <a name="36-perform-additional-configuration-and-schedule-tasks-as-necessary"></a><span data-ttu-id="d6bf4-238">3.6 gerektiği gibi ek yapılandırma ve zamanlama görevleri gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="d6bf4-238">3.6 Perform additional configuration and schedule tasks as necessary</span></span>
<span data-ttu-id="d6bf4-239">Ek yapılandırma gerekli olursa, onu dağıtıldıktan sonra tüm son değişiklikleri toohello VM başlangıç toomake sırasında çalışan zamanlanmış bir görev kullanmayı dikkate alın:</span><span class="sxs-lookup"><span data-stu-id="d6bf4-239">If additional configuration is needed, consider using a scheduled task that runs at startup toomake any final changes toohello VM after it has been deployed:</span></span>

* <span data-ttu-id="d6bf4-240">Bu en iyi yöntem toohave hello görev silme kendisini aktarılmadığı olur.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-240">It is a best practice toohave hello task delete itself upon successful execution.</span></span>
* <span data-ttu-id="d6bf4-241">Bunlar her zaman tooexist garanti hello yalnızca iki sürücüleri olduğundan herhangi bir yapılandırma C veya D sürücüsü dışındaki sürücülerde yararlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-241">No configuration should rely on drives other than drives C or D, because these are hello only two drives that are always guaranteed tooexist.</span></span> <span data-ttu-id="d6bf4-242">C sürücüsünün hello işletim sistemi diski ve sürücü D hello geçici yerel disk.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-242">Drive C is hello operating system disk, and drive D is hello temporary local disk.</span></span>

### <a name="37-generalize-hello-image"></a><span data-ttu-id="d6bf4-243">3.7 Merhaba görüntü generalize</span><span class="sxs-lookup"><span data-stu-id="d6bf4-243">3.7 Generalize hello image</span></span>
<span data-ttu-id="d6bf4-244">Hello Azure Marketi tüm görüntüleri genel bir şekilde yeniden kullanılabilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-244">All images in hello Azure Marketplace must be reusable in a generic fashion.</span></span> <span data-ttu-id="d6bf4-245">Diğer bir deyişle, hello işletim sistemi VHD genelleştirilmiş gerekir:</span><span class="sxs-lookup"><span data-stu-id="d6bf4-245">In other words, hello operating system VHD must be generalized:</span></span>

* <span data-ttu-id="d6bf4-246">Windows için "sysprepped" Merhaba görüntü olmalıdır ve hiçbir yapılandırmaları hello desteklemeyen yapılmalıdır **sysprep** komutu.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-246">For Windows, hello image should be "sysprepped," and no configurations should be done that do not support hello **sysprep** command.</span></span>
* <span data-ttu-id="d6bf4-247">Merhaba dizin % windir%\System32\Sysprep komutu aşağıdaki hello çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-247">You can run hello following command from hello directory %windir%\System32\Sysprep.</span></span>

        sysprep.exe /generalize /oobe /shutdown

  <span data-ttu-id="d6bf4-248">MSDN makalesine aşağıdaki hello adımda toosysprep hello işletim sistemini nasıl sağlandığını konusunda yönergeler: [oluşturma ve karşıya yükleme Windows Server VHD tooAzure](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d6bf4-248">Guidance on how toosysprep hello operating system is provided in Step of hello following MSDN article: [Create and upload a Windows Server VHD tooAzure](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="4-deploy-a-vm-from-your-vhds"></a><span data-ttu-id="d6bf4-249">4. Vhd'lerinizi VM'den dağıtma</span><span class="sxs-lookup"><span data-stu-id="d6bf4-249">4. Deploy a VM from your VHDs</span></span>
<span data-ttu-id="d6bf4-250">Vhd'lerinizi (Merhaba genelleştirilmiş bir işletim sistemi ve VHD disk sıfır veya daha fazla veri) karşıya sonra tooan Azure depolama hesabı, size kaydolabilir bunları bir kullanıcı VM görüntüsü olarak.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-250">After you have uploaded your VHDs (hello generalized operating system VHD and zero or more data disk VHDs) tooan Azure storage account, you can register them as a user VM image.</span></span> <span data-ttu-id="d6bf4-251">Ardından, görüntü test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-251">Then you can test that image.</span></span> <span data-ttu-id="d6bf4-252">İşletim sisteminizi VHD genelleştirilmiş olmadığından, doğrudan hello VM hello VHD URL'si sağlayarak dağıtamayacağınızı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-252">Note that because your operating system VHD is generalized, you cannot directly deploy hello VM by providing hello VHD URL.</span></span>

<span data-ttu-id="d6bf4-253">toolearn VM görüntüleri hakkında daha fazla blog gönderileri aşağıdaki gözden geçirme hello:</span><span class="sxs-lookup"><span data-stu-id="d6bf4-253">toolearn more about VM images, review hello following blog posts:</span></span>

* [<span data-ttu-id="d6bf4-254">VM görüntüsü</span><span class="sxs-lookup"><span data-stu-id="d6bf4-254">VM Image</span></span>](https://azure.microsoft.com/blog/vm-image-blog-post/)
* [<span data-ttu-id="d6bf4-255">VM görüntüsü PowerShell nasıl yapılır</span><span class="sxs-lookup"><span data-stu-id="d6bf4-255">VM Image PowerShell How To</span></span>](https://azure.microsoft.com/blog/vm-image-powershell-how-to-blog-post/)
* [<span data-ttu-id="d6bf4-256">Azure'da VM görüntüleri hakkında</span><span class="sxs-lookup"><span data-stu-id="d6bf4-256">About VM images in Azure</span></span>](https://msdn.microsoft.com/library/azure/dn790290.aspx)

### <a name="set-up-hello-necessary-tools-powershell-and-azure-cli"></a><span data-ttu-id="d6bf4-257">Merhaba gerekli araçlarını Kur, PowerShell ve Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d6bf4-257">Set up hello necessary tools, PowerShell and Azure CLI</span></span>
* [<span data-ttu-id="d6bf4-258">Nasıl toosetup PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6bf4-258">How toosetup PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="d6bf4-259">Nasıl toosetup Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d6bf4-259">How toosetup Azure CLI</span></span>](../cli-install-nodejs.md)

### <a name="41-create-a-user-vm-image"></a><span data-ttu-id="d6bf4-260">4.1 kullanıcı VM görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="d6bf4-260">4.1 Create a user VM image</span></span>
#### <a name="capture-vm"></a><span data-ttu-id="d6bf4-261">VM yakalama</span><span class="sxs-lookup"><span data-stu-id="d6bf4-261">Capture VM</span></span>
<span data-ttu-id="d6bf4-262">Lütfen hello PowerShell/API/Azure CLI kullanarak VM yakalama hakkında rehberlik için aşağıda verilen hello bağlantılar okuyun.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-262">Please read hello links given below for guidance on capturing hello VM using API/PowerShell/Azure CLI.</span></span>

* [<span data-ttu-id="d6bf4-263">API</span><span class="sxs-lookup"><span data-stu-id="d6bf4-263">API</span></span>](https://msdn.microsoft.com/library/mt163560.aspx)
* [<span data-ttu-id="d6bf4-264">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6bf4-264">PowerShell</span></span>](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="d6bf4-265">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d6bf4-265">Azure CLI</span></span>](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="generalize-image"></a><span data-ttu-id="d6bf4-266">Görüntü generalize</span><span class="sxs-lookup"><span data-stu-id="d6bf4-266">Generalize Image</span></span>
<span data-ttu-id="d6bf4-267">Lütfen hello PowerShell/API/Azure CLI kullanarak VM yakalama hakkında rehberlik için aşağıda verilen hello bağlantılar okuyun.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-267">Please read hello links given below for guidance on capturing hello VM using API/PowerShell/Azure CLI.</span></span>

* [<span data-ttu-id="d6bf4-268">API</span><span class="sxs-lookup"><span data-stu-id="d6bf4-268">API</span></span>](https://msdn.microsoft.com/library/mt269439.aspx)
* [<span data-ttu-id="d6bf4-269">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6bf4-269">PowerShell</span></span>](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="d6bf4-270">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d6bf4-270">Azure CLI</span></span>](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="42-deploy-a-vm-from-a-user-vm-image"></a><span data-ttu-id="d6bf4-271">4.2 bir kullanıcı VM görüntüsü VM'den dağıtma</span><span class="sxs-lookup"><span data-stu-id="d6bf4-271">4.2 Deploy a VM from a user VM image</span></span>
<span data-ttu-id="d6bf4-272">bir kullanıcı VM görüntüsü VM'den toodeploy, kullanabileceğiniz hello geçerli [Azure portal](https://manage.windowsazure.com) veya PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-272">toodeploy a VM from a user VM image, you can use hello current [Azure portal](https://manage.windowsazure.com) or PowerShell.</span></span>

<span data-ttu-id="d6bf4-273">**Merhaba geçerli Azure portalından bir VM'yi dağıtmak**</span><span class="sxs-lookup"><span data-stu-id="d6bf4-273">**Deploy a VM from hello current Azure portal**</span></span>

1. <span data-ttu-id="d6bf4-274">Çok Git**yeni** > **işlem** > **sanal makine** > **galerisinden**.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-274">Go too**New** > **Compute** > **Virtual machine** > **From gallery**.</span></span>

    ![Çizim][img-manage-vm-new]
2. <span data-ttu-id="d6bf4-276">Çok Git**görüntülerim**, ve ardından seçin hangi toodeploy VM görüntüsünü VM hello:</span><span class="sxs-lookup"><span data-stu-id="d6bf4-276">Go too**My images**, and then select hello VM image from which toodeploy a VM:</span></span>

   1. <span data-ttu-id="d6bf4-277">Ödeme Kapat dikkat toowhich görüntüsü seçin, çünkü hello **görüntülerim** işletim sistemi görüntüleri ve VM görüntüleri listeler.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-277">Pay close attention toowhich image you select, because hello **My images** view lists both operating system images and VM images.</span></span>
   2. <span data-ttu-id="d6bf4-278">Diskleri Hello numaradan arayan VM görüntüleri hello çoğunluğu olduğu için birden fazla disk görüntüsü hangi türü, dağıttığınız, belirlenmesine yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-278">Looking at hello number of disks can help determine what type of image you are deploying, because hello majority of VM images have more than one disk.</span></span> <span data-ttu-id="d6bf4-279">Ancak, yine olası toohave sonra olması gereken bir tek işletim sistemi diskle bir VM görüntüsü olan **disk sayısı** too1 ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-279">However, it is still possible toohave a VM image with only a single operating system disk, which would then have **Number of disks** set too1.</span></span>

      ![Çizim][img-manage-vm-select]
3. <span data-ttu-id="d6bf4-281">Merhaba VM Oluşturma Sihirbazı'nı izleyin ve hello VM adı, VM boyutu, konum, kullanıcı adı ve parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-281">Follow hello VM creation wizard and specify hello VM name, VM size, location, user name, and password.</span></span>

<span data-ttu-id="d6bf4-282">**PowerShell VM'den dağıtma**</span><span class="sxs-lookup"><span data-stu-id="d6bf4-282">**Deploy a VM from PowerShell**</span></span>

<span data-ttu-id="d6bf4-283">Yeni oluşturduğunuz VM görüntüsü hello büyük bir VM'den genelleştirilmiş toodeploy cmdlet'leri aşağıdaki hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-283">toodeploy a large VM from hello generalized VM image just created, you can use hello following cmdlets.</span></span>

    $img = Get-AzureVMImage -ImageName "myVMImage"
    $user = "user123"
    $pass = "adminPassword123"
    $myVM = New-AzureVMConfig -Name "VMImageVM" -InstanceSize "Large" -ImageName $img.ImageName | Add-AzureProvisioningConfig -Windows -AdminUsername $user -Password $pass
    New-AzureVM -ServiceName "VMImageCloudService" -VMs $myVM -Location "West US" -WaitForBoot

> [!IMPORTANT]
> <span data-ttu-id="d6bf4-284">Ek Yardım için lütfen [VHD oluşturma sırasında karşılaşılan sorun giderme ortak sorunları] bakın.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-284">Please refer [Troubleshooting common issues encountered during VHD creation] for additional assistance.</span></span>
>
>

## <a name="5-obtain-certification-for-your-vm-image"></a><span data-ttu-id="d6bf4-285">5. VM görüntüsü için sertifika elde</span><span class="sxs-lookup"><span data-stu-id="d6bf4-285">5. Obtain certification for your VM image</span></span>
<span data-ttu-id="d6bf4-286">VM görüntüsü hello Azure Marketi hazırlama hello sonraki sertifikalı toohave adımıdır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-286">hello next step in preparing your VM image for hello Azure Marketplace is toohave it certified.</span></span>

<span data-ttu-id="d6bf4-287">Merhaba doğrulama sonuçları toohello karşıya Vhd'lerinizi bulunduğu Azure kapsayıcı, bir teklif ekleme, SKU tanımlama ve VM gönderme görüntü için sertifika, bu işlem özel sertifika aracını çalıştıran içerir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-287">This process includes running a special certification tool, uploading hello verification results toohello Azure container where your VHDs reside, adding an offer, defining your SKU, and submitting your VM image for certification.</span></span>

### <a name="51-download-and-run-hello-certification-test-tool-for-azure-certified"></a><span data-ttu-id="d6bf4-288">5.1 indirin ve Azure sertifikalı hello sertifika Test aracı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="d6bf4-288">5.1 Download and run hello Certification Test Tool for Azure Certified</span></span>
<span data-ttu-id="d6bf4-289">Merhaba sertifika Aracı kullanıcı VM görüntüden sağlanan çalışan bir VM için VM görüntüsü hello tooensure Microsoft Azure ile uyumludur.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-289">hello certification tool runs on a running VM, provisioned from your user VM image, tooensure that hello VM image is compatible with Microsoft Azure.</span></span> <span data-ttu-id="d6bf4-290">Merhaba yönerge ve, VHD hazırlama hakkında gereksinimleri karşılandıktan doğrular.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-290">It will verify that hello guidance and requirements about preparing your VHD have been met.</span></span> <span data-ttu-id="d6bf4-291">Merhaba hello aracın çıktısının hello yayımlama portalında sırasında istekte bulunan sertifika karşıya yüklenmelidir uyumluluk rapordur.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-291">hello output of hello tool is a compatibility report, which should be uploaded on hello Publishing Portal while requesting certification.</span></span>

<span data-ttu-id="d6bf4-292">Merhaba sertifika aracı, Windows ve Linux VM'ler ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-292">hello certification tool can be used with both Windows and Linux VMs.</span></span> <span data-ttu-id="d6bf4-293">TooWindows tabanlı VM'ler PowerShell aracılığıyla bağlanır ve tooLinux VM'ler SSH.Net üzerinden bağlanır:</span><span class="sxs-lookup"><span data-stu-id="d6bf4-293">It connects tooWindows-based VMs via PowerShell and connects tooLinux VMs via SSH.Net:</span></span>

1. <span data-ttu-id="d6bf4-294">İlk olarak, hello hello sertifika aracını indirin [Microsoft İndirme sitesi][link-msft-download].</span><span class="sxs-lookup"><span data-stu-id="d6bf4-294">First, download hello certification tool at hello [Microsoft download site][link-msft-download].</span></span>
2. <span data-ttu-id="d6bf4-295">Merhaba sertifikası aracını açın ve hello ardından **yeni Testi Başlat** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-295">Open hello certification tool, and then click hello **Start New Test** button.</span></span>
3. <span data-ttu-id="d6bf4-296">Merhaba gelen **Test bilgi** ekranında, hello test çalışması için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-296">From hello **Test Information** screen, enter a name for hello test run.</span></span>
4. <span data-ttu-id="d6bf4-297">VM'nizin Linux üzerinde veya Windows üzerinde çalıştığına ilişkin seçim yapın.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-297">Choose whether your VM is on Linux or Windows.</span></span> <span data-ttu-id="d6bf4-298">Seçim bağlı olarak, hello sonraki seçenekleri seçin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-298">Depending on which you choose, select hello subsequent options.</span></span>

### <a name="connect-hello-certification-tool-tooa-linux-vm-image"></a><span data-ttu-id="d6bf4-299">**Merhaba sertifika aracı tooa Linux VM görüntüsü Bağlan**</span><span class="sxs-lookup"><span data-stu-id="d6bf4-299">**Connect hello certification tool tooa Linux VM image**</span></span>
1. <span data-ttu-id="d6bf4-300">Select hello SSH kimlik doğrulama modu: parola veya anahtar dosyası.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-300">Select hello SSH authentication mode: password or key file.</span></span>
2. <span data-ttu-id="d6bf4-301">Parola tabanlı kimlik doğrulamasını kullanıyorsanız, hello etki alanı adı sistemi (DNS) adı, kullanıcı adı ve parola girin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-301">If using password-­based authentication, enter hello Domain Name System (DNS) name, user name, and password.</span></span>
3. <span data-ttu-id="d6bf4-302">Anahtar dosyası kimlik doğrulamasını kullanıyorsanız, hello DNS adı, kullanıcı adı ve özel anahtar konumu girin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-302">If using key file authentication, enter hello DNS name, user name, and private key location.</span></span>

   ![Linux VM görüntüsü parola kimlik doğrulaması][img-cert-vm-pswd-lnx]

   ![Linux VM görüntüsü anahtar dosyası kimlik doğrulaması][img-cert-vm-key-lnx]

### <a name="connect-hello-certification-tool-tooa-windows-based-vm-image"></a><span data-ttu-id="d6bf4-305">**Merhaba sertifika aracı tooa Windows tabanlı VM görüntü Bağlan**</span><span class="sxs-lookup"><span data-stu-id="d6bf4-305">**Connect hello certification tool tooa Windows-based VM image**</span></span>
1. <span data-ttu-id="d6bf4-306">Tam hello VM DNS adını (örneğin, MyVMName.Cloudapp.net) girin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-306">Enter hello fully qualified VM DNS name (for example, MyVMName.Cloudapp.net).</span></span>
2. <span data-ttu-id="d6bf4-307">Merhaba kullanıcı adı ve parola girin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-307">Enter hello user name and password.</span></span>

   ![Windows VM görüntüsünü parola kimlik doğrulaması][img-cert-vm-pswd-win]

<span data-ttu-id="d6bf4-309">Linux veya Windows tabanlı VM görüntü için hello doğru seçeneklerini seçtikten sonra Seç **Bağlantıyı Sına** tooensure SSH.Net veya PowerShell test etmek için geçerli bir bağlantı vardır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-309">After you have selected hello correct options for your Linux or Windows-based VM image, select **Test Connection** tooensure that SSH.Net or PowerShell has a valid connection for testing purposes.</span></span> <span data-ttu-id="d6bf4-310">Bağlantı kurulduktan sonra Seç **sonraki** toostart hello test.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-310">After a connection is established, select **Next** toostart hello test.</span></span>

<span data-ttu-id="d6bf4-311">Merhaba test tamamlandıktan sonra her bir test öğesi için hello sonuçları (Geçiş/başarısız/uyarı) alırsınız.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-311">When hello test is complete, you will receive hello results (Pass/Fail/Warning) for each test element.</span></span>

![Linux VM görüntüsü için test çalışmaları][img-cert-vm-test-lnx]

![Windows VM görüntüsü için test çalışmaları][img-cert-vm-test-win]

<span data-ttu-id="d6bf4-314">Merhaba testleri hiçbirini başarısız olursa, görüntünüzü uygunluğu onaylanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-314">If any of hello tests fail, your image will not be certified.</span></span> <span data-ttu-id="d6bf4-315">Bu gerçekleşirse, hello gereksinimleri gözden geçirin ve gerekli değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-315">If this occurs, review hello requirements and make any necessary changes.</span></span>

<span data-ttu-id="d6bf4-316">Test Hello otomatik sonra VM görüntüsüne bir soru formu ekran aracılığıyla tooprovide ek giriş istenir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-316">After hello automated test, you are asked tooprovide additional input on your VM image via a questionnaire screen.</span></span>  <span data-ttu-id="d6bf4-317">Merhaba soruları tamamlayın ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-317">Complete hello questions, and then select **Next**.</span></span>

![Sertifika aracı anket][img-cert-vm-questionnaire]

![Sertifika aracı anket][img-cert-vm-questionnaire-2]

<span data-ttu-id="d6bf4-320">Merhaba soru tamamladıktan sonra hello Linux VM görüntüsü için SSH erişim bilgileri gibi ek bilgileri ve başarısız tüm değerlendirmeleri için bir açıklama sağlar.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-320">After you have completed hello questionnaire, you can provide additional information such as SSH access information for hello Linux VM image and an explanation for any failed assessments.</span></span> <span data-ttu-id="d6bf4-321">Merhaba test sonuçları indirmek ve günlük dosyalarının hello yürütülen test çalışmaları için ek tooyour yanıtlar toohello soru.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-321">You can download hello test results and log files for hello executed test cases in addition tooyour answers toohello questionnaire.</span></span> <span data-ttu-id="d6bf4-322">Hello Hello Sonuçları Kaydet Vhd'lerinizi aynı kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-322">Save hello results in hello same container as your VHDs.</span></span>

![Test sonuçları sertifika Kaydet][img-cert-vm-results]

### <a name="52-get-hello-shared-access-signature-uri-for-your-vm-images"></a><span data-ttu-id="d6bf4-324">5.2 hello paylaşılan erişim imzası URI için VM görüntülerini alın.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-324">5.2 Get hello shared access signature URI for your VM images</span></span>
<span data-ttu-id="d6bf4-325">İşlem yayımlama hello sırasında hello SKU için oluşturduğunuz VHD'leri tooeach sağlama hello Tekdüzen Kaynak Tanımlayıcıları (URI'ler) belirtin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-325">During hello publishing process, you specify hello uniform resource identifiers (URIs) that lead tooeach of hello VHDs you have created for your SKU.</span></span> <span data-ttu-id="d6bf4-326">Microsoft access toothese VHD'ler hello sertifika işlemi sırasında gerekir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-326">Microsoft needs access toothese VHDs during hello certification process.</span></span> <span data-ttu-id="d6bf4-327">Bu nedenle, her VHD için bir paylaşılan erişim imzası URI toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-327">Therefore, you need toocreate a shared access signature URI for each VHD.</span></span> <span data-ttu-id="d6bf4-328">Merhaba girilmesi URI budur **görüntüleri** hello yayımlama portalında sekmesindedir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-328">This is hello URI that should be entered in the **Images** tab in hello Publishing Portal.</span></span>

<span data-ttu-id="d6bf4-329">Merhaba paylaşılan erişim imzası oluşturulan URI gereksinimlerine toohello uyması:</span><span class="sxs-lookup"><span data-stu-id="d6bf4-329">hello shared access signature URI created should adhere toohello following requirements:</span></span>

* <span data-ttu-id="d6bf4-330">Paylaşılan erişim imzası URI'ler Vhd'lerinizi için oluştururken, liste ve Okuma izinleri yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-330">When generating shared access signature URIs for your VHDs, List and Read­ permissions are sufficient.</span></span> <span data-ttu-id="d6bf4-331">Yazma veya Silme erişimi sağlamayın.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-331">Do not provide Write or Delete access.</span></span>
* <span data-ttu-id="d6bf4-332">Merhaba paylaşılan erişim imzası URI oluşturulduğunda hello süresi erişim için üç (3) hafta ila en az olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-332">hello duration for access should be a minimum of three (3) weeks from when hello shared access signature URI is created.</span></span>
* <span data-ttu-id="d6bf4-333">toosafeguard hello geçerli tarih seçin hello günün UTC saati için.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-333">toosafeguard for UTC time, select hello day before hello current date.</span></span> <span data-ttu-id="d6bf4-334">Örneğin, Hello 6 Ekim 2014 geçerli tarih ise 5/10/2014 seçin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-334">For example, if hello current date is October 6, 2014, select 10/5/2014.</span></span>

<span data-ttu-id="d6bf4-335">SAS URL olabilir içinde birden çok yol tooshare, VHD için Azure Marketi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-335">SAS URL can be generated in multiple ways tooshare your VHD for Azure Marketplace.</span></span>
<span data-ttu-id="d6bf4-336">Aşağıdaki 3 önerilen araçları hello:</span><span class="sxs-lookup"><span data-stu-id="d6bf4-336">Following are hello 3 recommended tools:</span></span>

1.  <span data-ttu-id="d6bf4-337">Azure Depolama Gezgini</span><span class="sxs-lookup"><span data-stu-id="d6bf4-337">Azure Storage Explorer</span></span>
2.  <span data-ttu-id="d6bf4-338">Microsoft Storage Gezgini</span><span class="sxs-lookup"><span data-stu-id="d6bf4-338">Microsoft Storage Explorer</span></span>
3.  <span data-ttu-id="d6bf4-339">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d6bf4-339">Azure CLI</span></span>

<span data-ttu-id="d6bf4-340">**Azure Depolama Gezgini (Windows kullanıcıları için önerilir)**</span><span class="sxs-lookup"><span data-stu-id="d6bf4-340">**Azure Storage Explorer (Recommended for Windows Users)**</span></span>

<span data-ttu-id="d6bf4-341">Azure Storage Gezgini kullanarak SAS URL oluşturmak için hello adımlar aşağıda belirtilmiştir</span><span class="sxs-lookup"><span data-stu-id="d6bf4-341">Following are hello steps for generating SAS URL by using Azure Storage Explorer</span></span>

1. <span data-ttu-id="d6bf4-342">Karşıdan [Azure Storage Gezgini 6 Önizleme 3](https://azurestorageexplorer.codeplex.com/) Codeplex.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-342">Download [Azure Storage Explorer 6 Preview 3](https://azurestorageexplorer.codeplex.com/) from CodePlex.</span></span> <span data-ttu-id="d6bf4-343">Çok Git[Azure Storage Gezgini 6 Önizleme](https://azurestorageexplorer.codeplex.com/) tıklatıp **"İndirmeleri"**.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-343">Go too[Azure Storage Explorer 6 Preview](https://azurestorageexplorer.codeplex.com/) and click **"Downloads"**.</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_01.png)

2. <span data-ttu-id="d6bf4-345">Karşıdan [AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668) ve unzipping sonra yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-345">Download [AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668) and install after unzipping it.</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_02.png)

3. <span data-ttu-id="d6bf4-347">Yüklendikten sonra hello uygulamasını açın.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-347">After it is installed, open hello application.</span></span>
4. <span data-ttu-id="d6bf4-348">Tıklatın **hesabı eklemek**.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-348">Click **Add Account**.</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_03.png)

5. <span data-ttu-id="d6bf4-350">Merhaba depolama hesabı adı, depolama hesabı anahtarı ve depolama uç noktaları etki alanı belirtin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-350">Specify hello storage account name, storage account key, and storage endpoints domain.</span></span> <span data-ttu-id="d6bf4-351">Azure Portalı'nda, VHD'yi nerede tutulur Azure aboneliğinizde hello depolama hesap budur.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-351">This is hello storage account in your Azure subscription where you have kept your VHD on Azure portal.</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_04.png)

6. <span data-ttu-id="d6bf4-353">Azure Storage Gezgini bağlandıktan sonra tooyour belirli bir depolama hesabı, bu tüm hello içeren hello depolama hesabında gösteren başlayacak.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-353">Once Azure Storage Explorer is connected tooyour specific storage account, it will start showing all of hello contains within hello storage account.</span></span> <span data-ttu-id="d6bf4-354">Merhaba işletim sistemi disk VHD dosyasını (senaryonuz için uygun olup olmadığını da veri diskleri) kopyaladığınız hello kapsayıcısı seçin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-354">Select hello container where you copied hello operating system disk VHD file (also data disks if they are applicable for your scenario).</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_05.png)

7. <span data-ttu-id="d6bf4-356">Merhaba blob kapsayıcısı seçtikten sonra Azure Storage Gezgini hello kapsayıcıdaki hello dosyaları gösteren başlatır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-356">After selecting hello blob container, Azure Storage Explorer starts showing hello files within hello container.</span></span> <span data-ttu-id="d6bf4-357">Gönderilen toobe gereken hello görüntü dosyası (.vhd) seçin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-357">Select hello image file (.vhd) that needs toobe submitted.</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_06.png)

8.  <span data-ttu-id="d6bf4-359">Merhaba kapsayıcısında Hello .vhd dosyası seçtikten sonra hello tıklatın **güvenlik** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-359">After selecting hello .vhd file in hello container, click hello **Security** tab.</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_07.png)

9.  <span data-ttu-id="d6bf4-361">Merhaba, **Blob kapsayıcı güvenlik** iletişim kutusu, hello bırakın hello varsayılanlarına **erişim düzeyi** sekmesini ve ardından **paylaşılan erişim imzaları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-361">In hello **Blob Container Security** dialog box, leave hello defaults on hello **Access Level** tab, and then click **Shared Access Signatures** tab.</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_08.png)

10. <span data-ttu-id="d6bf4-363">Toogenerate hello .vhd görüntüsü için paylaşılan erişim imzası URI Hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d6bf4-363">Follow hello steps below toogenerate a shared access signature URI for hello .vhd image:</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_09.png)

    <span data-ttu-id="d6bf4-365">a.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-365">a.</span></span> <span data-ttu-id="d6bf4-366">**Erişime izin:** toosafeguard hello geçerli tarih seçin hello günün UTC saati için.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-366">**Access permitted from:** toosafeguard for UTC time, select hello day before hello current date.</span></span> <span data-ttu-id="d6bf4-367">Örneğin, Hello 6 Ekim 2014 geçerli tarih ise 5/10/2014 seçin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-367">For example, if hello current date is October 6, 2014, select 10/5/2014.</span></span>

    <span data-ttu-id="d6bf4-368">b.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-368">b.</span></span> <span data-ttu-id="d6bf4-369">**Erişime izin:** en az 3 hafta hello sonra bir tarihi seçin **erişime izin** tarih.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-369">**Access permitted to:** Select a date that is at least 3 weeks after hello **Access permitted from** date.</span></span>

    <span data-ttu-id="d6bf4-370">c.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-370">c.</span></span> <span data-ttu-id="d6bf4-371">**İzin verilen eylemleri:** Select hello **listesi** ve **okuma** izinleri.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-371">**Actions permitted:** Select hello **List** and **Read** permissions.</span></span>

    <span data-ttu-id="d6bf4-372">d.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-372">d.</span></span> <span data-ttu-id="d6bf4-373">.Vhd dosyası doğru seçtiğiniz sonra dosyanızı görünür **Blob adı tooaccess** uzantısı .vhd ile.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-373">If you have selected your .vhd file correctly, then your file appears in **Blob name tooaccess** with extension .vhd.</span></span>

    <span data-ttu-id="d6bf4-374">e.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-374">e.</span></span> <span data-ttu-id="d6bf4-375">Tıklatın **imzayı üretmek**.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-375">Click **Generate Signature**.</span></span>

    <span data-ttu-id="d6bf4-376">f.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-376">f.</span></span> <span data-ttu-id="d6bf4-377">İçinde **oluşturulan paylaşılan erişim imzası URI bu kapsayıcının**, yukarıda vurgulandığı aşağıdaki hello denetle:</span><span class="sxs-lookup"><span data-stu-id="d6bf4-377">In **Generated Shared Access Signature URI of this container**, check for hello following as highlighted above:</span></span>

       - <span data-ttu-id="d6bf4-378">Görüntünüzü dosya adı olduğundan emin olun ve **".vhd"** hello URI şunlardır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-378">Make sure that your image file name and **".vhd"** are in hello URI.</span></span>
       - <span data-ttu-id="d6bf4-379">Merhaba imza Hello sonunda olduğundan emin olun **"rl ="** görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-379">At hello end of hello signature, make sure that **"=rl"** appears.</span></span> <span data-ttu-id="d6bf4-380">Bu, okuma ve liste erişim başarıyla sağlandı gösterir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-380">This demonstrates that Read and List access was provided successfully.</span></span>
       - <span data-ttu-id="d6bf4-381">Merhaba imza ortadaki olduğundan emin olun **"sr c ="** görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-381">In middle of hello signature, make sure that **"sr=c"** appears.</span></span> <span data-ttu-id="d6bf4-382">Bu kapsayıcı düzeyinde erişime sahip olması gösterir</span><span class="sxs-lookup"><span data-stu-id="d6bf4-382">This demonstrates that you have container level access</span></span>

11. <span data-ttu-id="d6bf4-383">oluşturulan hello tooensure paylaşılan erişim imzası URI çalışır, tıklatın **tarayıcısında Test**.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-383">tooensure that hello generated shared access signature URI works, click **Test in Browser**.</span></span> <span data-ttu-id="d6bf4-384">Merhaba indirme işlemi başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-384">It should start hello download process.</span></span>

12. <span data-ttu-id="d6bf4-385">Merhaba paylaşılan erişim imzası URI kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-385">Copy hello shared access signature URI.</span></span> <span data-ttu-id="d6bf4-386">Merhaba URI toopaste hello yayımlama portalında içine budur.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-386">This is hello URI toopaste into hello Publishing Portal.</span></span>

13. <span data-ttu-id="d6bf4-387">Merhaba SKU'ndaki her VHD için 6-10 adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-387">Repeat steps 6-10 for each VHD in hello SKU.</span></span>

<span data-ttu-id="d6bf4-388">**Microsoft Azure Depolama Gezgini (MAC/Windows/Linux)**</span><span class="sxs-lookup"><span data-stu-id="d6bf4-388">**Microsoft Azure Storage Explorer (Windows/MAC/Linux)**</span></span>

<span data-ttu-id="d6bf4-389">Microsoft Azure Storage Gezgini kullanarak SAS URL oluşturmak için hello adımlar aşağıda belirtilmiştir</span><span class="sxs-lookup"><span data-stu-id="d6bf4-389">Following are hello steps for generating SAS URL by using Microsoft Azure Storage Explorer</span></span>

1.  <span data-ttu-id="d6bf4-390">Microsoft Azure Storage Gezgini form karşıdan [http://storageexplorer.com/](http://storageexplorer.com/) Web sitesi.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-390">Download Microsoft Azure Storage Explorer form [http://storageexplorer.com/](http://storageexplorer.com/) website.</span></span> <span data-ttu-id="d6bf4-391">Çok Git[Microsoft Azure Storage Gezgini](http://storageexplorer.com/releasenotes.html) tıklatıp **"Windows için karşıdan yükleme"**.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-391">Go too[Microsoft Azure Storage Explorer](http://storageexplorer.com/releasenotes.html) and click **“Download for Windows”**.</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_10.png)

2.  <span data-ttu-id="d6bf4-393">Yüklendikten sonra hello uygulamasını açın.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-393">After it is installed, open hello application.</span></span>

3.  <span data-ttu-id="d6bf4-394">Tıklatın **hesabı eklemek**.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-394">Click **Add Account**.</span></span>

4.  <span data-ttu-id="d6bf4-395">Microsoft Azure Storage Gezgini tooyour abonelik tooyour hesabında oturum yapılandırın</span><span class="sxs-lookup"><span data-stu-id="d6bf4-395">Configure Microsoft Azure Storage Explorer tooyour subscription by sign in tooyour account</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_11.png)

5.  <span data-ttu-id="d6bf4-397">Toostorage hesabı gidin ve hello kapsayıcısı seçin</span><span class="sxs-lookup"><span data-stu-id="d6bf4-397">Go toostorage account and select hello Container</span></span>

6.  <span data-ttu-id="d6bf4-398">Seçin **"Paylaşımı erişim imzası Al …"**</span><span class="sxs-lookup"><span data-stu-id="d6bf4-398">Select **“Get Share Access Signature..”**</span></span> <span data-ttu-id="d6bf4-399">Merhaba, sağ tıklatma kullanarak **kapsayıcı**</span><span class="sxs-lookup"><span data-stu-id="d6bf4-399">by using Right Click of hello **container**</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_12.png)

7.  <span data-ttu-id="d6bf4-401">Aşağıdaki gibi başına başlangıç zamanı, bitiş saati ve izinleri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="d6bf4-401">Update Start time, Expiry time and Permissions as per following</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_13.png)

    <span data-ttu-id="d6bf4-403">a.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-403">a.</span></span>  <span data-ttu-id="d6bf4-404">**Başlangıç saati:** toosafeguard hello geçerli tarih seçin hello günün UTC saati için.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-404">**Start Time:** toosafeguard for UTC time, select hello day before hello current date.</span></span> <span data-ttu-id="d6bf4-405">Örneğin, Hello 6 Ekim 2014 geçerli tarih ise 5/10/2014 seçin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-405">For example, if hello current date is October 6, 2014, select 10/5/2014.</span></span>

    <span data-ttu-id="d6bf4-406">b.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-406">b.</span></span>  <span data-ttu-id="d6bf4-407">**Sona erme saati:** en az 3 hafta hello sonra bir tarihi seçin **başlangıç saati** tarih.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-407">**Expiry Time:** Select a date that is at least 3 weeks after hello **Start Time** date.</span></span>

    <span data-ttu-id="d6bf4-408">c.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-408">c.</span></span>  <span data-ttu-id="d6bf4-409">**İzinleri:** Select hello **listesi** ve **okuma** izinleri</span><span class="sxs-lookup"><span data-stu-id="d6bf4-409">**Permissions:** Select hello **List** and **Read** permissions</span></span>

8.  <span data-ttu-id="d6bf4-410">Kapsayıcı paylaşılan erişim imzası URI kopyalayın</span><span class="sxs-lookup"><span data-stu-id="d6bf4-410">Copy Container shared access signature URI</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_14.png)

    <span data-ttu-id="d6bf4-412">Oluşturulan SAS URL için düzeyi kapsayıcıdır ve şimdi biz tooadd VHD adı da gerekir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-412">Generated SAS URL is for container Level and now we need tooadd VHD name in it.</span></span>

    <span data-ttu-id="d6bf4-413">Kapsayıcı düzeyi SAS URL biçimi:`https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span><span class="sxs-lookup"><span data-stu-id="d6bf4-413">Format of Container Level SAS URL: `https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    <span data-ttu-id="d6bf4-414">Aşağıdaki şekilde hello kapsayıcı adı SAS URL sonra VHD adı Ekle`https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span><span class="sxs-lookup"><span data-stu-id="d6bf4-414">Insert VHD name after hello container name in SAS URL as below `https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    <span data-ttu-id="d6bf4-415">Örnek:</span><span class="sxs-lookup"><span data-stu-id="d6bf4-415">Example:</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_15.png)

    <span data-ttu-id="d6bf4-417">VHD SAS URL hello VHD adı TestRGVM201631920152.vhd olduğundan`https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span><span class="sxs-lookup"><span data-stu-id="d6bf4-417">TestRGVM201631920152.vhd is hello VHD Name then VHD SAS URL will be `https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    - <span data-ttu-id="d6bf4-418">Görüntünüzü dosya adı olduğundan emin olun ve **".vhd"** hello URI şunlardır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-418">Make sure that your image file name and **".vhd"** are in hello URI.</span></span>
    - <span data-ttu-id="d6bf4-419">Merhaba imza ortadaki olduğundan emin olun **"sp rl ="** görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-419">In middle of hello signature, make sure that **"sp=rl"** appears.</span></span> <span data-ttu-id="d6bf4-420">Bu, okuma ve liste erişim başarıyla sağlandı gösterir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-420">This demonstrates that Read and List access was provided successfully.</span></span>
    - <span data-ttu-id="d6bf4-421">Merhaba imza ortadaki olduğundan emin olun **"sr c ="** görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-421">In middle of hello signature, make sure that **"sr=c"** appears.</span></span> <span data-ttu-id="d6bf4-422">Bu kapsayıcı düzeyinde erişime sahip olması gösterir</span><span class="sxs-lookup"><span data-stu-id="d6bf4-422">This demonstrates that you have container level access</span></span>

9.  <span data-ttu-id="d6bf4-423">oluşturulan paylaşılan erişim imzası URI works hello tooensure tarayıcıda sınayın.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-423">tooensure that hello generated shared access signature URI works, test it in browser.</span></span> <span data-ttu-id="d6bf4-424">Merhaba indirme işlemi başlamanız gerekir</span><span class="sxs-lookup"><span data-stu-id="d6bf4-424">It should start hello download process</span></span>

10. <span data-ttu-id="d6bf4-425">Merhaba paylaşılan erişim imzası URI kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-425">Copy hello shared access signature URI.</span></span> <span data-ttu-id="d6bf4-426">Merhaba URI toopaste hello yayımlama portalında içine budur.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-426">This is hello URI toopaste into hello Publishing Portal.</span></span>

11. <span data-ttu-id="d6bf4-427">Merhaba SKU'ndaki her VHD için bu adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-427">Repeat these steps for each VHD in hello SKU.</span></span>

<span data-ttu-id="d6bf4-428">**Azure CLI (Windows dışı & sürekli tümleştirme için önerilir)**</span><span class="sxs-lookup"><span data-stu-id="d6bf4-428">**Azure CLI (Recommended for Non-Windows & Continuous Integration)**</span></span>

<span data-ttu-id="d6bf4-429">Azure CLI kullanarak SAS URL oluşturmak için hello adımlar aşağıda belirtilmiştir</span><span class="sxs-lookup"><span data-stu-id="d6bf4-429">Following are hello steps for generating SAS URL by using Azure CLI</span></span>

1.  <span data-ttu-id="d6bf4-430">Microsoft Azure CLI üzerinden indirme [burada](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/).</span><span class="sxs-lookup"><span data-stu-id="d6bf4-430">Download Microsoft Azure CLI from [here](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/).</span></span> <span data-ttu-id="d6bf4-431">Farklı bağlantıları için bulabileceğiniz  **[Windows](http://aka.ms/webpi-azure-cli)**  ve  **[MAC OS](http://aka.ms/mac-azure-cli)**.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-431">You can also find different links for **[Windows](http://aka.ms/webpi-azure-cli)** and **[MAC OS](http://aka.ms/mac-azure-cli)**.</span></span>

2.  <span data-ttu-id="d6bf4-432">Bir kez yüklenir, lütfen yükleyin</span><span class="sxs-lookup"><span data-stu-id="d6bf4-432">Once it is downloaded, please install</span></span>

3.  <span data-ttu-id="d6bf4-433">Aşağıdaki kod ile bir PowerShell dosyası oluşturun ve yerel Kaydet</span><span class="sxs-lookup"><span data-stu-id="d6bf4-433">Create a PowerShell file with following code and save it in local</span></span>

          $conn="DefaultEndpointsProtocol=https;AccountName=<StorageAccountName>;AccountKey=<Storage Account Key>"
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl <Permission End Date> -c $conn --start <Permission Start Date>  

    <span data-ttu-id="d6bf4-434">Merhaba aşağıdaki güncelleştirme yukarıda parametreleri</span><span class="sxs-lookup"><span data-stu-id="d6bf4-434">Update hello following parameters in above</span></span>

    <span data-ttu-id="d6bf4-435">a.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-435">a.</span></span> <span data-ttu-id="d6bf4-436">**`<StorageAccountName>`**: Depolama hesabınızın adını verin</span><span class="sxs-lookup"><span data-stu-id="d6bf4-436">**`<StorageAccountName>`**: Give your storage account name</span></span>

    <span data-ttu-id="d6bf4-437">b.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-437">b.</span></span> <span data-ttu-id="d6bf4-438">**`<Storage Account Key>`**: Depolama hesabı anahtarınızı verin</span><span class="sxs-lookup"><span data-stu-id="d6bf4-438">**`<Storage Account Key>`**: Give your storage account key</span></span>

    <span data-ttu-id="d6bf4-439">c.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-439">c.</span></span> <span data-ttu-id="d6bf4-440">**`<Permission Start Date>`**: toosafeguard hello geçerli tarih seçin hello günün UTC saati için.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-440">**`<Permission Start Date>`**: toosafeguard for UTC time, select hello day before hello current date.</span></span> <span data-ttu-id="d6bf4-441">Örneğin, hello geçerli tarihidir 26 Ekim 2016 sonra değeri 25/10/2016</span><span class="sxs-lookup"><span data-stu-id="d6bf4-441">For example, if hello current date is October 26, 2016, then value should be 10/25/2016</span></span>

    <span data-ttu-id="d6bf4-442">d.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-442">d.</span></span> <span data-ttu-id="d6bf4-443">**`<Permission End Date>`**: En az 3 hafta hello sonra bir tarihi seçin **başlangıç tarihi**.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-443">**`<Permission End Date>`**: Select a date that is at least 3 weeks after hello **Start Date**.</span></span> <span data-ttu-id="d6bf4-444">Değerin olması **02/11/2016**.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-444">Then value should be **11/02/2016**.</span></span>

    <span data-ttu-id="d6bf4-445">Uygun parametreleri güncelleştirdikten sonra hello örnek kod aşağıda verilmiştir</span><span class="sxs-lookup"><span data-stu-id="d6bf4-445">Following is hello example code after updating proper parameters</span></span>

          $conn="DefaultEndpointsProtocol=https;AccountName=st20151;AccountKey=TIQE5QWMKHpT5q2VnF1bb+NUV7NVMY2xmzVx1rdgIVsw7h0pcI5nMM6+DVFO65i4bQevx21dmrflA91r0Vh2Yw=="
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl 11/02/2016 -c $conn --start 10/25/2016  

4.  <span data-ttu-id="d6bf4-446">"Yönetici olarak çalıştır" moduyla PowerShell Düzenleyicisi'ni açın ve #3. adımda dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-446">Open Powershell editor with “Run as Administrator” mode and open file in step #3.</span></span>

5.  <span data-ttu-id="d6bf4-447">Kapsayıcı düzeyinde erişimi için SAS URL hello çalışma hello komut dosyası ve sağlar</span><span class="sxs-lookup"><span data-stu-id="d6bf4-447">Run hello script and it will provide you hello SAS URL for container level access</span></span>

    <span data-ttu-id="d6bf4-448">Aşağıdaki hello SAS imza ve kopyalama vurgulanmış hello bölümü bir Not Defteri'nde hello çıktısını olacaktır</span><span class="sxs-lookup"><span data-stu-id="d6bf4-448">Following will be hello output of hello SAS Signature and copy hello highlighted part in a notepad</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/img5.2_16.png)

6.  <span data-ttu-id="d6bf4-450">Kapsayıcı düzeyi SAS URL artık alacak ve tooadd VHD adı da gerekir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-450">Now you will get container level SAS URL and you need tooadd VHD name in it.</span></span>

    <span data-ttu-id="d6bf4-451">Kapsayıcı düzeyi SAS URL #</span><span class="sxs-lookup"><span data-stu-id="d6bf4-451">Container level SAS URL #</span></span>

    `https://st20151.blob.core.windows.net/vhds?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

7.  <span data-ttu-id="d6bf4-452">Aşağıda gösterildiği gibi hello kapsayıcı adı SAS URL sonra VHD adı Ekle`https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`</span><span class="sxs-lookup"><span data-stu-id="d6bf4-452">Insert VHD name after hello container name in SAS URL as shown below `https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`</span></span>

    <span data-ttu-id="d6bf4-453">Örnek:</span><span class="sxs-lookup"><span data-stu-id="d6bf4-453">Example:</span></span>

    <span data-ttu-id="d6bf4-454">VHD SAS URL hello VHD adı TestRGVM201631920152.vhd olduğundan</span><span class="sxs-lookup"><span data-stu-id="d6bf4-454">TestRGVM201631920152.vhd is hello VHD Name then VHD SAS URL will be</span></span>

    `https://st20151.blob.core.windows.net/vhds/ TestRGVM201631920152.vhd?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    - <span data-ttu-id="d6bf4-455">Yansıma Dosya adı ve ".vhd" Merhaba URI olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-455">Make sure that your image file name and ".vhd" are in hello URI.</span></span>
    -   <span data-ttu-id="d6bf4-456">Merhaba imza ortadaki olduğundan emin olun "sp rl =" görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-456">In middle of hello signature, make sure that "sp=rl" appears.</span></span> <span data-ttu-id="d6bf4-457">Bu, okuma ve liste erişim başarıyla sağlandı gösterir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-457">This demonstrates that Read and List access was provided successfully.</span></span>
    -   <span data-ttu-id="d6bf4-458">Merhaba imza ortadaki olduğundan emin olun "sr c =" görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-458">In middle of hello signature, make sure that "sr=c" appears.</span></span> <span data-ttu-id="d6bf4-459">Bu kapsayıcı düzeyinde erişime sahip olması gösterir</span><span class="sxs-lookup"><span data-stu-id="d6bf4-459">This demonstrates that you have container level access</span></span>

8.  <span data-ttu-id="d6bf4-460">oluşturulan paylaşılan erişim imzası URI works hello tooensure tarayıcıda sınayın.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-460">tooensure that hello generated shared access signature URI works, test it in browser.</span></span> <span data-ttu-id="d6bf4-461">Merhaba indirme işlemi başlamanız gerekir</span><span class="sxs-lookup"><span data-stu-id="d6bf4-461">It should start hello download process</span></span>

9.  <span data-ttu-id="d6bf4-462">Merhaba paylaşılan erişim imzası URI kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-462">Copy hello shared access signature URI.</span></span> <span data-ttu-id="d6bf4-463">Merhaba URI toopaste hello yayımlama portalında içine budur.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-463">This is hello URI toopaste into hello Publishing Portal.</span></span>

10. <span data-ttu-id="d6bf4-464">Merhaba SKU'ndaki her VHD için bu adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-464">Repeat these steps for each VHD in hello SKU.</span></span>


### <a name="53-provide-information-about-hello-vm-image-and-request-certification-in-hello-publishing-portal"></a><span data-ttu-id="d6bf4-465">5.3 hello VM görüntü ile ilgili bilgileri sağlayın ve hello Yayımlama Portalı sertifika isteği</span><span class="sxs-lookup"><span data-stu-id="d6bf4-465">5.3 Provide information about hello VM image and request certification in hello Publishing Portal</span></span>
<span data-ttu-id="d6bf4-466">Teklif ve SKU oluşturduktan sonra SKU ile ilişkili hello görüntü ayrıntıları girmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="d6bf4-466">After you have created your offer and SKU, you should enter hello image details associated with that SKU:</span></span>

1. <span data-ttu-id="d6bf4-467">Toohello Git [yayımlama portalında][link-pubportal]ve satıcının hesabınızla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-467">Go toohello [Publishing Portal][link-pubportal], and then sign in with your seller account.</span></span>
2. <span data-ttu-id="d6bf4-468">Select hello **VM görüntüleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-468">Select hello **VM images** tab.</span></span>
3. <span data-ttu-id="d6bf4-469">Merhaba hello sayfanın başında listelenen hello gerçekte hello teklif tanımlayıcısı ve hello SKU tanımlayıcısı tanımlayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-469">hello identifier listed at hello top of hello page is actually hello offer identifier and not hello SKU identifier.</span></span>
4. <span data-ttu-id="d6bf4-470">Merhaba özellikleri hello altında doldurmak **SKU'ları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-470">Fill out hello properties under hello **SKUs** section.</span></span>
5. <span data-ttu-id="d6bf4-471">Altında **işletim sistemi ailesi**, VHD hello işletim sistemiyle ilişkili hello işletim sistemi türü'nü tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-471">Under **Operating system family**, click hello operating system type associated with hello operating system VHD.</span></span>
6. <span data-ttu-id="d6bf4-472">Merhaba, **işletim sistemi** kutusunda, hello işletim sistemi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-472">In hello **Operating system** box, describe hello operating system.</span></span> <span data-ttu-id="d6bf4-473">İşletim sistemi ailesi, türü, sürüm ve güncelleştirmeler gibi bir biçim göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-473">Consider a format such as operating system family, type, version, and updates.</span></span> <span data-ttu-id="d6bf4-474">"Windows Server Datacenter 2014 R2." örneğidir</span><span class="sxs-lookup"><span data-stu-id="d6bf4-474">An example is "Windows Server Datacenter 2014 R2."</span></span>
7. <span data-ttu-id="d6bf4-475">Sanal makine boyutlarını önerilen toosix seçin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-475">Select up toosix recommended virtual machine sizes.</span></span> <span data-ttu-id="d6bf4-476">Bunlar toopurchase karar verin ve görüntünüzü dağıtmak, görüntülenen toohello müşteri hello fiyatlandırma katmanı dikey penceresinde hello Azure Portal almak önerilerdir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-476">These are recommendations that get displayed toohello customer in hello Pricing tier blade in hello Azure Portal when they decide toopurchase and deploy your image.</span></span> <span data-ttu-id="d6bf4-477">**Bunlar yalnızca önerilerdir. Merhaba müşteri yansımanıza hello diskleri düzenler herhangi bir VM boyutta belirtilen mümkün tooselect olur.**</span><span class="sxs-lookup"><span data-stu-id="d6bf4-477">**These are only recommendations. hello customer is able tooselect any VM size that accommodates hello disks specified in your image.**</span></span>
8. <span data-ttu-id="d6bf4-478">Merhaba sürümü girin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-478">Enter hello version.</span></span> <span data-ttu-id="d6bf4-479">Merhaba sürüm alanı bir anlamsal sürüm tooidentify hello ürün ve kendi güncellemeleri yalıtır:</span><span class="sxs-lookup"><span data-stu-id="d6bf4-479">hello version field encapsulates a semantic version tooidentify hello product and its updates:</span></span>
   * <span data-ttu-id="d6bf4-480">Sürümleri X, Y ve Z tamsayılar nerede X.Y.Z hello biçiminde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-480">Versions should be of hello form X.Y.Z, where X, Y, and Z are integers.</span></span>
   * <span data-ttu-id="d6bf4-481">Farklı SKU'ları görüntülerinde farklı birincil ve ikincil sürümleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-481">Images in different SKUs can have different major and minor versions.</span></span>
   * <span data-ttu-id="d6bf4-482">İçinde bir SKU sürümlerinde yalnızca hello düzeltme eki sürümü (Z X.Y.Z gelen) artırmak artımlı değişiklikler olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-482">Versions within a SKU should only be incremental changes, which increase hello patch version (Z from X.Y.Z).</span></span>
9. <span data-ttu-id="d6bf4-483">Merhaba, **OS VHD URL'si** kutusuna, hello paylaşılan erişim imzası hello işletim sistemi VHD için oluşturulan URI girin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-483">In hello **OS VHD URL** box, enter hello shared access signature URI created for hello operating system VHD.</span></span>
10. <span data-ttu-id="d6bf4-484">Bu SKU ile ilişkili veri disklerinin varsa, bu veri diski toobe dağıtım takılı istediğiniz hello mantıksal birim numarası (LUN) toowhich seçin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-484">If there are data disks associated with this SKU, select hello logical unit number (LUN) toowhich you would like this data disk toobe mounted upon deployment.</span></span>
11. <span data-ttu-id="d6bf4-485">Merhaba, **LUN X VHD URL'si** kutusuna, hello paylaşılan erişim imzası oluşturulan hello ilk veri VHD URI girin.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-485">In hello **LUN X VHD URL** box, enter hello shared access signature URI created for hello first data VHD.</span></span>

    ![Çizim](media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-3.png)


## <a name="common-sas-url-issues--fixes"></a><span data-ttu-id="d6bf4-487">Ortak SAS URL sorunları ve düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="d6bf4-487">Common SAS URL issues & fixes</span></span>

|<span data-ttu-id="d6bf4-488">Sorun</span><span class="sxs-lookup"><span data-stu-id="d6bf4-488">Issue</span></span>|<span data-ttu-id="d6bf4-489">Hata iletisi</span><span class="sxs-lookup"><span data-stu-id="d6bf4-489">Failure Message</span></span>|<span data-ttu-id="d6bf4-490">Düzeltme</span><span class="sxs-lookup"><span data-stu-id="d6bf4-490">Fix</span></span>|<span data-ttu-id="d6bf4-491">Belge bağlantı</span><span class="sxs-lookup"><span data-stu-id="d6bf4-491">Documentation Link</span></span>|
|---|---|---|---|
|<span data-ttu-id="d6bf4-492">Kopyalama hatası görüntüleri - "?" SAS URL'si bulunamadı</span><span class="sxs-lookup"><span data-stu-id="d6bf4-492">Failure in copying images - "?" is not found in SAS url</span></span>|<span data-ttu-id="d6bf4-493">Hata: Görüntüleri kopyalama.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-493">Failure: Copying Images.</span></span> <span data-ttu-id="d6bf4-494">Sağlanan SAS URI'sini blob erişilemiyor toodownload kullanarak.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-494">Not able toodownload blob using provided SAS Uri.</span></span>|<span data-ttu-id="d6bf4-495">Güncelleştirme hello SAS URL'yi kullanarak önerilen araçları</span><span class="sxs-lookup"><span data-stu-id="d6bf4-495">Update hello SAS Url using recommended tools</span></span>|[<span data-ttu-id="d6bf4-496">https://Azure.microsoft.com/en-us/documentation/articles/Storage-dotnet-Shared-Access-Signature-Part-1/</span><span class="sxs-lookup"><span data-stu-id="d6bf4-496">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="d6bf4-497">Görüntüleri kopyalama hatası - SAS URL'si değil, "st" ve "se" parametreleri</span><span class="sxs-lookup"><span data-stu-id="d6bf4-497">Failure in copying images - “st” and “se” parameters not in SAS url</span></span>|<span data-ttu-id="d6bf4-498">Hata: Görüntüleri kopyalama.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-498">Failure: Copying Images.</span></span> <span data-ttu-id="d6bf4-499">Sağlanan SAS URI'sini blob erişilemiyor toodownload kullanarak.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-499">Not able toodownload blob using provided SAS Uri.</span></span>|<span data-ttu-id="d6bf4-500">Başlangıç ve bitiş tarihleri üzerindeki ile güncelleştirme hello SAS URL'si</span><span class="sxs-lookup"><span data-stu-id="d6bf4-500">Update hello SAS Url with Start and End dates on it</span></span>|[<span data-ttu-id="d6bf4-501">https://Azure.microsoft.com/en-us/documentation/articles/Storage-dotnet-Shared-Access-Signature-Part-1/</span><span class="sxs-lookup"><span data-stu-id="d6bf4-501">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="d6bf4-502">Görüntüleri - "sp rl SAS url değil =" kopyalama hatası</span><span class="sxs-lookup"><span data-stu-id="d6bf4-502">Failure in copying images - “sp=rl” not in SAS url</span></span>|<span data-ttu-id="d6bf4-503">Hata: Görüntüleri kopyalama.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-503">Failure: Copying Images.</span></span> <span data-ttu-id="d6bf4-504">SAS URI'sini sağlanan blob erişilemiyor toodownload kullanarak</span><span class="sxs-lookup"><span data-stu-id="d6bf4-504">Not able toodownload blob using provided SAS Uri</span></span>|<span data-ttu-id="d6bf4-505">"Okuma" & "listesi olarak ayarla izinlerle güncelleştirme hello SAS URL'si</span><span class="sxs-lookup"><span data-stu-id="d6bf4-505">Update hello SAS Url with permissions set as “Read” & “List</span></span>|[<span data-ttu-id="d6bf4-506">https://Azure.microsoft.com/en-us/documentation/articles/Storage-dotnet-Shared-Access-Signature-Part-1/</span><span class="sxs-lookup"><span data-stu-id="d6bf4-506">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="d6bf4-507">Görüntüleri - SAS url kopyalama hatası vhd adlarında boşluk sahip</span><span class="sxs-lookup"><span data-stu-id="d6bf4-507">Failure in copying images - SAS url have white spaces in vhd name</span></span>|<span data-ttu-id="d6bf4-508">Hata: Görüntüleri kopyalama.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-508">Failure: Copying Images.</span></span> <span data-ttu-id="d6bf4-509">Sağlanan SAS URI'sini blob erişilemiyor toodownload kullanarak.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-509">Not able toodownload blob using provided SAS Uri.</span></span>|<span data-ttu-id="d6bf4-510">Boşluk olmadan güncelleştirme hello SAS URL'si</span><span class="sxs-lookup"><span data-stu-id="d6bf4-510">Update hello SAS Url without white spaces</span></span>|[<span data-ttu-id="d6bf4-511">https://Azure.microsoft.com/en-us/documentation/articles/Storage-dotnet-Shared-Access-Signature-Part-1/</span><span class="sxs-lookup"><span data-stu-id="d6bf4-511">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="d6bf4-512">Görüntüleri – SAS Url yetkilendirmesi hata kopyalama hatası</span><span class="sxs-lookup"><span data-stu-id="d6bf4-512">Failure in copying images – SAS Url Authorization error</span></span>|<span data-ttu-id="d6bf4-513">Hata: Görüntüleri kopyalama.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-513">Failure: Copying Images.</span></span> <span data-ttu-id="d6bf4-514">Tooauthorization hatası nedeniyle erişilemiyor toodownload blob</span><span class="sxs-lookup"><span data-stu-id="d6bf4-514">Not able toodownload blob due tooauthorization error</span></span>|<span data-ttu-id="d6bf4-515">Merhaba SAS Url yeniden oluştur</span><span class="sxs-lookup"><span data-stu-id="d6bf4-515">Regenerate hello SAS Url</span></span>|[<span data-ttu-id="d6bf4-516">https://Azure.microsoft.com/en-us/documentation/articles/Storage-dotnet-Shared-Access-Signature-Part-1/</span><span class="sxs-lookup"><span data-stu-id="d6bf4-516">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|


## <a name="next-step"></a><span data-ttu-id="d6bf4-517">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="d6bf4-517">Next step</span></span>
<span data-ttu-id="d6bf4-518">Merhaba SKU ayrıntılarla tamamladıktan sonra İleri toohello taşıyabilirsiniz [Azure Marketi pazarlama içerik Kılavuzu][link-pushstaging].</span><span class="sxs-lookup"><span data-stu-id="d6bf4-518">After you are done with hello SKU details, you can move forward toohello [Azure Marketplace marketing content guide][link-pushstaging].</span></span> <span data-ttu-id="d6bf4-519">İşlem yayımlama hello Bu adım çok pazarlama içeriği, fiyatlandırma ve diğer bilgileri gerekli önceki hello sağlamak**adım 3: VM sınama teklif hazırlamada**, burada dağıtmadan önce çeşitli kullanım örneği senaryoları test Genel görünürlük için Azure Marketi teklifi toohello hello ve satın alma.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-519">In that step of hello publishing process, you provide hello marketing content, pricing, and other information necessary prior too**Step 3: Testing your VM offer in staging**, where you test various use-case scenarios before deploying hello offer toohello Azure Marketplace for public visibility and purchase.</span></span>  

## <a name="see-also"></a><span data-ttu-id="d6bf4-520">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="d6bf4-520">See also</span></span>
* [<span data-ttu-id="d6bf4-521">Başlarken: nasıl toopublish bir teklif toohello Azure Market</span><span class="sxs-lookup"><span data-stu-id="d6bf4-521">Getting started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

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
