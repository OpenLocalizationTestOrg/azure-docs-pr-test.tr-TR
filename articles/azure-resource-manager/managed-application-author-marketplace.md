---
title: "aaaAzure yönetilen hello Market uygulamalarda | Microsoft Docs"
description: "Azure açıklar yönetilen Market hello kullanılabilir olan uygulamalar."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b3cdf3f1fccdd47db699e4892ae8bce35118bfd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-in-hello-marketplace"></a><span data-ttu-id="24322-103">Azure Market hello uygulamalarda yönetilen</span><span class="sxs-lookup"><span data-stu-id="24322-103">Azure managed applications in hello Marketplace</span></span>

 <span data-ttu-id="24322-104">MSP'ler, ISV ve sistem tümleştiricileri (SIS) kullanabilir Azure yönetilen uygulamaları toooffer çözümleri tooall Azure Marketi müşterilerine.</span><span class="sxs-lookup"><span data-stu-id="24322-104">MSPs, ISVs, and system integrators (SIs) can use Azure managed applications toooffer their solutions tooall Azure Marketplace customers.</span></span> <span data-ttu-id="24322-105">Bu tür çözümler hello Bakım ve müşteriler için ek yükü bakım azaltın.</span><span class="sxs-lookup"><span data-stu-id="24322-105">Such solutions reduce hello maintenance and servicing overhead for customers.</span></span> <span data-ttu-id="24322-106">Yayımcılar, altyapı ve yazılım hello Market aracılığıyla satın.</span><span class="sxs-lookup"><span data-stu-id="24322-106">Publishers can sell infrastructure and software through hello Marketplace.</span></span> <span data-ttu-id="24322-107">Bunlar, hizmetler ve işletimsel destek toomanaged uygulamalar ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24322-107">They can attach services and operational support toomanaged applications.</span></span> <span data-ttu-id="24322-108">Daha fazla bilgi için bkz: [yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="24322-108">For more information, see [Managed application overview](managed-application-overview.md).</span></span>

<span data-ttu-id="24322-109">Bu makalede, nasıl bir MSP, ISV veya SI uygulama toohello Market yayımlayabilir ve geniş çapta kullanılabilir toocustomers olun açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="24322-109">This article explains how an MSP, ISV, or SI can publish an application toohello Marketplace and make it broadly available toocustomers.</span></span>

## <a name="prerequisites-for-publishing-a-managed-application"></a><span data-ttu-id="24322-110">Yönetilen bir uygulamayı yayımlamak için Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="24322-110">Prerequisites for publishing a managed application</span></span>

<span data-ttu-id="24322-111">Önkoşullar toolisting hello Market içinde:</span><span class="sxs-lookup"><span data-stu-id="24322-111">Prerequisites toolisting in hello Marketplace:</span></span>

* <span data-ttu-id="24322-112">Teknik</span><span class="sxs-lookup"><span data-stu-id="24322-112">Technical</span></span>

    *  <span data-ttu-id="24322-113">Merhaba temel yapısını ve Azure Resource Manager şablonları sözdizimi hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="24322-113">For information about hello basic structure and syntax of Azure Resource Manager templates, see [Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
    *  <span data-ttu-id="24322-114">tooview tam şablon çözümleri, bakın [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/en-us/documentation/templates/) veya hello [Hızlı Başlangıç şablonu deposu](https://github.com/azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="24322-114">tooview complete template solutions, see [Azure Quickstart templates](https://azure.microsoft.com/en-us/documentation/templates/) or hello [Quickstart template repository](https://github.com/azure/azure-quickstart-templates).</span></span>
    *  <span data-ttu-id="24322-115">Nasıl toocreate hello arabirimi hello Market üzerinden uygulamanızı dağıtmak müşteriler hakkında daha fazla bilgi için bkz: [bir kullanıcı arabirimi tanımı dosyası oluşturma](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="24322-115">For information about how toocreate hello interface for customers who deploy your application through hello Marketplace, see [Create a user interface definition file](managed-application-createuidefinition-overview.md).</span></span>

* <span data-ttu-id="24322-116">Yedeğin (iş gereksinimlerini)</span><span class="sxs-lookup"><span data-stu-id="24322-116">Nontechnical (business requirements)</span></span>

    *   <span data-ttu-id="24322-117">Şirketiniz veya onun yan burada satış Market hello tarafından desteklenen bir ülkede bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="24322-117">Your company or its subsidiary must be located in a country where sales are supported by hello Marketplace.</span></span>
    *   <span data-ttu-id="24322-118">Ürünü Market hello tarafından desteklenen faturalama modelleri ile uyumlu şekilde lisansına sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="24322-118">Your product must be licensed in a way that is compatible with billing models supported by hello Marketplace.</span></span>
    *   <span data-ttu-id="24322-119">Teknik Destek kullanılabilir toocustomers ticari koşulların elverdiği oranda makul bir biçimde yapmaktan sorumlu.</span><span class="sxs-lookup"><span data-stu-id="24322-119">You're responsible for making technical support available toocustomers in a commercially reasonable manner.</span></span> <span data-ttu-id="24322-120">Merhaba destek Ücretli, boş veya topluluk desteklemez.</span><span class="sxs-lookup"><span data-stu-id="24322-120">hello support can be free, paid, or through community support.</span></span>
    *   <span data-ttu-id="24322-121">Yazılım ve üçüncü taraf yazılım bağımlılıkları lisansı sağlamaktan sorumlu.</span><span class="sxs-lookup"><span data-stu-id="24322-121">You're responsible for licensing your software and any third-party software dependencies.</span></span>
    *   <span data-ttu-id="24322-122">Azure portal teklifi toobe ölçütlerini karşılayan içerik hello Market ve hello listelenen sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="24322-122">You must provide content that meets criteria for your offering toobe listed in hello Marketplace and in hello Azure portal.</span></span>
    *   <span data-ttu-id="24322-123">Toohello hello Azure Market katılım ilkeleri ve yayımcı Sözleşmesi koşullarını kabul etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="24322-123">You must agree toohello terms of hello Azure Marketplace Participation Policies and Publisher Agreement.</span></span>
    *   <span data-ttu-id="24322-124">Merhaba kullanım koşulları, Microsoft gizlilik bildirimi ve Microsoft Azure sertifikalı Program Sözleşmesi ile toocomply kabul etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="24322-124">You must agree toocomply with hello Terms of Use, Microsoft Privacy Statement, and Microsoft Azure Certified Program Agreement.</span></span>

## <a name="create-a-new-azure-application-offer"></a><span data-ttu-id="24322-125">Yeni bir Azure uygulama teklifi oluşturma</span><span class="sxs-lookup"><span data-stu-id="24322-125">Create a new Azure application offer</span></span>

<span data-ttu-id="24322-126">Merhaba önkoşulları karşılaması sonra hazır toocreate olduğunuz yönetilen uygulamayı teklifiniz.</span><span class="sxs-lookup"><span data-stu-id="24322-126">After you meet hello prerequisites, you're ready toocreate your managed application offer.</span></span> <span data-ttu-id="24322-127">Bir teklif ve bir SKU hızlı bir genel bakış atalım.</span><span class="sxs-lookup"><span data-stu-id="24322-127">Let's take a quick overview of an offer and a SKU.</span></span>

### <a name="offer"></a><span data-ttu-id="24322-128">Sunduğu</span><span class="sxs-lookup"><span data-stu-id="24322-128">Offer</span></span>

<span data-ttu-id="24322-129">yönetilen bir uygulama için Hello teklifi tooa sınıf bir yayımcıdan sunumu ürünün karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="24322-129">hello offer for a managed application corresponds tooa class of product offering from a publisher.</span></span> <span data-ttu-id="24322-130">Yeni bir çözüm/uygulama toomake hello Market kullanılabilir istediğiniz türü varsa, bunu yeni bir teklif ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24322-130">If you have a new type of solution/application that you want toomake available in hello Marketplace, you can set it up as a new offer.</span></span> <span data-ttu-id="24322-131">Bir teklif, SKU'ları koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="24322-131">An offer is a collection of SKUs.</span></span> <span data-ttu-id="24322-132">Her teklif hello Market kendi varlık gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="24322-132">Every offer appears as its own entity in hello Marketplace.</span></span>

### <a name="sku"></a><span data-ttu-id="24322-133">SKU</span><span class="sxs-lookup"><span data-stu-id="24322-133">SKU</span></span>

<span data-ttu-id="24322-134">Bir SKU hello en küçük purchasable bir teklif birimidir.</span><span class="sxs-lookup"><span data-stu-id="24322-134">A SKU is hello smallest purchasable unit of an offer.</span></span> <span data-ttu-id="24322-135">Merhaba içinde bir SKU kullanabilirsiniz arasında aynı ürün sınıfı (teklif) toodifferentiate:</span><span class="sxs-lookup"><span data-stu-id="24322-135">You can use a SKU within hello same product class (offer) toodifferentiate between:</span></span>

* <span data-ttu-id="24322-136">Desteklenen farklı özellikleri.</span><span class="sxs-lookup"><span data-stu-id="24322-136">Different features that are supported.</span></span>
* <span data-ttu-id="24322-137">Merhaba teklif yönetilen yönetilmeyen mı.</span><span class="sxs-lookup"><span data-stu-id="24322-137">Whether hello offer is managed or unmanaged.</span></span>
* <span data-ttu-id="24322-138">Desteklenen faturalama modelleri.</span><span class="sxs-lookup"><span data-stu-id="24322-138">Billing models that are supported.</span></span>

<span data-ttu-id="24322-139">Bir SKU hello Market hello üst teklif altında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="24322-139">A SKU appears under hello parent offer in hello Marketplace.</span></span> <span data-ttu-id="24322-140">Hello Azure portal purchasable kendi varlık gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="24322-140">It appears as its own purchasable entity in hello Azure portal.</span></span>

### <a name="set-up-an-offer"></a><span data-ttu-id="24322-141">Bir teklif ayarlayın</span><span class="sxs-lookup"><span data-stu-id="24322-141">Set up an offer</span></span>

1. <span data-ttu-id="24322-142">İçinde toohello oturum [bulut iş ortağı portalına](https://cloudpartner.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="24322-142">Sign in toohello [Cloud Partner portal](https://cloudpartner.azure.com/).</span></span>

2. <span data-ttu-id="24322-143">Merhaba soldaki Hello Gezinti Bölmesi'nde seçin **+ yeni teklif** > **Azure uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="24322-143">In hello navigation pane on hello left, select **+ New offer** > **Azure Applications**.</span></span>

    ![Yeni teklif](./media/managed-application-author-marketplace/newOffer.png)

3. <span data-ttu-id="24322-145">Hello sol hello görünür hello form doldurmak **Düzenleyicisi** görünümü.</span><span class="sxs-lookup"><span data-stu-id="24322-145">Fill out hello forms that appear on hello left in hello **Editor** view.</span></span> <span data-ttu-id="24322-146">Gerekli alanları ile kırmızı yıldız işareti (*) işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="24322-146">Required fields are marked with a red asterisk (*).</span></span>

    ![Teklif ayarları](./media/managed-application-author-marketplace/newOffer_OfferSettings.png)

    <span data-ttu-id="24322-148">Dört ana forms kullanılan toocreate bir yönetilen uygulamayı şunlardır:</span><span class="sxs-lookup"><span data-stu-id="24322-148">Four main forms are used toocreate a managed application:</span></span>

    <span data-ttu-id="24322-149">a.</span><span class="sxs-lookup"><span data-stu-id="24322-149">a.</span></span> <span data-ttu-id="24322-150">Teklif ayarları</span><span class="sxs-lookup"><span data-stu-id="24322-150">Offer Settings</span></span>

    <span data-ttu-id="24322-151">b.</span><span class="sxs-lookup"><span data-stu-id="24322-151">b.</span></span> <span data-ttu-id="24322-152">SKU'ları</span><span class="sxs-lookup"><span data-stu-id="24322-152">SKUs</span></span>

    <span data-ttu-id="24322-153">c.</span><span class="sxs-lookup"><span data-stu-id="24322-153">c.</span></span> <span data-ttu-id="24322-154">Market</span><span class="sxs-lookup"><span data-stu-id="24322-154">Marketplace</span></span>

    <span data-ttu-id="24322-155">d.</span><span class="sxs-lookup"><span data-stu-id="24322-155">d.</span></span> <span data-ttu-id="24322-156">Destek</span><span class="sxs-lookup"><span data-stu-id="24322-156">Support</span></span>

<span data-ttu-id="24322-157">Bu form bölümleri aşağıdaki hello içinde daha ayrıntılı açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="24322-157">These forms are described in greater detail in hello following sections.</span></span>

## <a name="offer-settings-form"></a><span data-ttu-id="24322-158">Teklif ayarları formu</span><span class="sxs-lookup"><span data-stu-id="24322-158">Offer Settings form</span></span>
<span data-ttu-id="24322-159">Bu temel form toospecify hello teklif ayarları kullanın.</span><span class="sxs-lookup"><span data-stu-id="24322-159">Use this basic form toospecify hello offer settings.</span></span>

1. <span data-ttu-id="24322-160">Hello dolgu **teklif ayarları** formu.</span><span class="sxs-lookup"><span data-stu-id="24322-160">Fill in hello **Offer Settings** form.</span></span> <span data-ttu-id="24322-161">Merhaba farklı alanları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="24322-161">hello different fields are:</span></span>

    <span data-ttu-id="24322-162">a.</span><span class="sxs-lookup"><span data-stu-id="24322-162">a.</span></span> <span data-ttu-id="24322-163">**Teklif kodu**: Yayımcı profilindeki hello teklif bu benzersiz tanımlayıcı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="24322-163">**Offer ID**: This unique identifier identifies hello offer within a publisher profile.</span></span> <span data-ttu-id="24322-164">Bu kimliği ürün URL'ler, Resource Manager şablonları görünür ve faturalama raporlar.</span><span class="sxs-lookup"><span data-stu-id="24322-164">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="24322-165">Yalnızca küçük harf alfasayısal karakterler veya tire (-) birleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="24322-165">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="24322-166">Merhaba kimliği, bir tire bitemez.</span><span class="sxs-lookup"><span data-stu-id="24322-166">hello ID can't end in a dash.</span></span> <span data-ttu-id="24322-167">Sınırlı tooa en çok 50 karakter var.</span><span class="sxs-lookup"><span data-stu-id="24322-167">It's limited tooa maximum of 50 characters.</span></span> <span data-ttu-id="24322-168">Bu alan, bir teklif Canlı göründükten sonra kilitlendi.</span><span class="sxs-lookup"><span data-stu-id="24322-168">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="24322-169">b.</span><span class="sxs-lookup"><span data-stu-id="24322-169">b.</span></span> <span data-ttu-id="24322-170">**Yayımcı kimliği**: Bu teklif altında toopublish istediğiniz bu açılan liste toochoose hello yayımcı profili kullanın.</span><span class="sxs-lookup"><span data-stu-id="24322-170">**Publisher ID**: Use this drop-down list toochoose hello publisher profile you want toopublish this offer under.</span></span> <span data-ttu-id="24322-171">Bu alan, bir teklif Canlı göründükten sonra kilitlendi.</span><span class="sxs-lookup"><span data-stu-id="24322-171">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="24322-172">c.</span><span class="sxs-lookup"><span data-stu-id="24322-172">c.</span></span> <span data-ttu-id="24322-173">**Ad**: hello Market ve hello portal teklifiniz için bu görünen ad görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="24322-173">**Name**: This display name for your offer appears in hello Marketplace and in hello portal.</span></span> <span data-ttu-id="24322-174">En çok 50 karakter olabilir.</span><span class="sxs-lookup"><span data-stu-id="24322-174">It can have a maximum of 50 characters.</span></span> <span data-ttu-id="24322-175">Ürününüzün tanınabilir bir marka adını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="24322-175">Include a recognizable brand name for your product.</span></span> <span data-ttu-id="24322-176">Nasıl pazarlama olmadığı sürece, şirketinizin adını buraya dahil etmeyin.</span><span class="sxs-lookup"><span data-stu-id="24322-176">Don't include your company name here unless that's how it's marketed.</span></span> <span data-ttu-id="24322-177">Kendi Web sitesinde bu teklif pazarlama varsa, bu hello adı tam olarak, Web sitenizde görünme olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="24322-177">If you're marketing this offer on your own website, ensure that hello name is exactly how it appears on your website.</span></span>

2. <span data-ttu-id="24322-178">Seçin **kaydetmek** toosave ilerleme durumunuzu.</span><span class="sxs-lookup"><span data-stu-id="24322-178">Select **Save** toosave your progress.</span></span> 

## <a name="skus-form"></a><span data-ttu-id="24322-179">SKU'ları formu</span><span class="sxs-lookup"><span data-stu-id="24322-179">SKUs form</span></span>
<span data-ttu-id="24322-180">Merhaba sonraki teklifiniz için tooadd SKU'ları adımdır.</span><span class="sxs-lookup"><span data-stu-id="24322-180">hello next step is tooadd SKUs for your offer.</span></span>

1. <span data-ttu-id="24322-181">Seçin **SKU'ları** > **yeni SKU**.</span><span class="sxs-lookup"><span data-stu-id="24322-181">Select **SKUs** > **New SKU**.</span></span> 

    ![Yeni SKU seçin](./media/managed-application-author-marketplace/newOffer_skus.png)

2. <span data-ttu-id="24322-183">Girin bir **SKU kimliği**.</span><span class="sxs-lookup"><span data-stu-id="24322-183">Enter a **SKU ID**.</span></span> <span data-ttu-id="24322-184">SKU kimliği hello SKU bir teklif içinde benzersiz tanımlayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="24322-184">A SKU ID is a unique identifier for hello SKU within an offer.</span></span> <span data-ttu-id="24322-185">Bu kimliği ürün URL'ler, Resource Manager şablonları görünür ve faturalama raporlar.</span><span class="sxs-lookup"><span data-stu-id="24322-185">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="24322-186">Yalnızca küçük harf alfasayısal karakterler veya tire (-) birleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="24322-186">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="24322-187">Hello kimliği bir tire bitemez ve sınırlı tooa en çok 50 karakter değil.</span><span class="sxs-lookup"><span data-stu-id="24322-187">hello ID can't end in a dash, and it's limited tooa maximum of 50 characters.</span></span> <span data-ttu-id="24322-188">Bu alan, bir teklif Canlı göründükten sonra kilitlendi.</span><span class="sxs-lookup"><span data-stu-id="24322-188">After an offer goes live, this field is locked.</span></span> <span data-ttu-id="24322-189">Bir teklif içinde birden çok SKU olabilir.</span><span class="sxs-lookup"><span data-stu-id="24322-189">You can have multiple SKUs within an offer.</span></span> <span data-ttu-id="24322-190">Bir SKU gereksinim duyduğunuz her görüntü için toopublish planlayın.</span><span class="sxs-lookup"><span data-stu-id="24322-190">You need a SKU for each image you plan toopublish.</span></span>

3. <span data-ttu-id="24322-191">Merhaba dolgu **SKU ayrıntıları** form aşağıdaki hello bölümünde:</span><span class="sxs-lookup"><span data-stu-id="24322-191">Fill out hello **SKU Details** section on hello following form:</span></span>

    ![Yeni SKU sağlayın](./media/managed-application-author-marketplace/newOffer_newsku.png)

    <span data-ttu-id="24322-193">Alanları aşağıdaki hello doldurun:</span><span class="sxs-lookup"><span data-stu-id="24322-193">Fill out hello following fields:</span></span>
    
    <span data-ttu-id="24322-194">a.</span><span class="sxs-lookup"><span data-stu-id="24322-194">a.</span></span> <span data-ttu-id="24322-195">**Başlık**: Bu SKU için bir başlık girin.</span><span class="sxs-lookup"><span data-stu-id="24322-195">**Title**: Enter a title for this SKU.</span></span> <span data-ttu-id="24322-196">Bu öğe için hello galerisinde bu başlığı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="24322-196">This title appears in hello gallery for this item.</span></span>

    <span data-ttu-id="24322-197">b.</span><span class="sxs-lookup"><span data-stu-id="24322-197">b.</span></span> <span data-ttu-id="24322-198">**Özet**: kısa bir özeti için bu SKU girin.</span><span class="sxs-lookup"><span data-stu-id="24322-198">**Summary**: Enter a short summary for this SKU.</span></span> <span data-ttu-id="24322-199">Bu metin hello başlığı altında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="24322-199">This text appears underneath hello title.</span></span>

    <span data-ttu-id="24322-200">c.</span><span class="sxs-lookup"><span data-stu-id="24322-200">c.</span></span> <span data-ttu-id="24322-201">**Açıklama**: hello SKU hakkında ayrıntılı bir açıklama girin.</span><span class="sxs-lookup"><span data-stu-id="24322-201">**Description**: Enter a detailed description about hello SKU.</span></span>

    <span data-ttu-id="24322-202">d.</span><span class="sxs-lookup"><span data-stu-id="24322-202">d.</span></span> <span data-ttu-id="24322-203">**SKU tür**: hello izin verilen değerler: **yönetilen uygulamayı** ve **çözüm şablonları**.</span><span class="sxs-lookup"><span data-stu-id="24322-203">**SKU Type**: hello allowed values are **Managed Application** and **Solution Templates**.</span></span> <span data-ttu-id="24322-204">Bu durumda, seçin **yönetilen uygulamayı**.</span><span class="sxs-lookup"><span data-stu-id="24322-204">For this case, select **Managed Application**.</span></span>

4. <span data-ttu-id="24322-205">Merhaba dolgu **Paket ayrıntılarını** form aşağıdaki hello bölümünde:</span><span class="sxs-lookup"><span data-stu-id="24322-205">Fill out hello **Package Details** section on hello following form:</span></span>

    ![Paket](./media/managed-application-author-marketplace/newOffer_newsku_package.png)

    <span data-ttu-id="24322-207">Alanları aşağıdaki hello doldurun:</span><span class="sxs-lookup"><span data-stu-id="24322-207">Fill out hello following fields:</span></span>

    <span data-ttu-id="24322-208">a.</span><span class="sxs-lookup"><span data-stu-id="24322-208">a.</span></span> <span data-ttu-id="24322-209">**Geçerli sürüm**: bir sürümü için karşıya yüklediğiniz hello paketi girin.</span><span class="sxs-lookup"><span data-stu-id="24322-209">**Current Version**: Enter a version for hello package you upload.</span></span> <span data-ttu-id="24322-210">Merhaba biçiminde olmalıdır `{number}.{number}.{number}{number}`.</span><span class="sxs-lookup"><span data-stu-id="24322-210">It should be in hello format `{number}.{number}.{number}{number}`.</span></span>

    <span data-ttu-id="24322-211">b.</span><span class="sxs-lookup"><span data-stu-id="24322-211">b.</span></span> <span data-ttu-id="24322-212">**Bir paket dosyası seçmek**: Bu paket, sıkıştırılmış dosyalar bir .zip dosyasına aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="24322-212">**Select a package file**: This package contains hello following files that are compressed into a .zip file:</span></span>
    * <span data-ttu-id="24322-213">**applianceMainTemplate.json**: toodeploy hello çözüm/uygulama kullandı hello dağıtım şablon dosyası.</span><span class="sxs-lookup"><span data-stu-id="24322-213">**applianceMainTemplate.json**: hello deployment template file that's used toodeploy hello solution/application.</span></span> <span data-ttu-id="24322-214">Hakkında bilgi için bkz toocreate dağıtım şablonu dosyalarını [, ilk Azure Resource Manager şablonu oluşturma](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="24322-214">For information about how toocreate deployment template files, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>
    * <span data-ttu-id="24322-215">**appliancecreateUIDefinition.json**: Bu dosya bu çözümü/uygulama tooprovision kullandığı hello Azure portal toogenerate hello kullanıcı arabirimi tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="24322-215">**appliancecreateUIDefinition.json**: This file is used by hello Azure portal toogenerate hello user interface that's used tooprovision this solution/application.</span></span> <span data-ttu-id="24322-216">Daha fazla bilgi için bkz: [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="24322-216">For more information, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
    * <span data-ttu-id="24322-217">**mainTemplate.json**: Bu şablon dosyası, yalnızca hello Microsoft.Solution/appliances kaynak içeriyor.</span><span class="sxs-lookup"><span data-stu-id="24322-217">**mainTemplate.json**: This template file contains only hello Microsoft.Solution/appliances resource.</span></span> <span data-ttu-id="24322-218">Merhaba mainTemplate dosyası, aşağıdaki özelliklere hello içerir:</span><span class="sxs-lookup"><span data-stu-id="24322-218">hello mainTemplate file includes hello following properties:</span></span>

        *  <span data-ttu-id="24322-219">**tür**: kullanım **Market** hello Market yönetilen uygulamalar için.</span><span class="sxs-lookup"><span data-stu-id="24322-219">**kind**: Use **Marketplace** for managed applications in hello Marketplace.</span></span>
        *  <span data-ttu-id="24322-220">**ManagedResourceGroupId**: applianceMainTemplate.json içinde tanımlanan tüm hello kaynaklara dağıtıldığı hello müşterinin aboneliğini bu kaynak grubunda bulunuyor.</span><span class="sxs-lookup"><span data-stu-id="24322-220">**ManagedResourceGroupId**: This resource group in hello customer's subscription is where all hello resources defined in applianceMainTemplate.json are deployed.</span></span>
        *  <span data-ttu-id="24322-221">**PublisherPackageId**: Bu dize hello paketi benzersiz olarak tanımlar.</span><span class="sxs-lookup"><span data-stu-id="24322-221">**PublisherPackageId**: This string uniquely identifies hello package.</span></span> <span data-ttu-id="24322-222">Merhaba biçiminde Hello değer sağlamanız `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span><span class="sxs-lookup"><span data-stu-id="24322-222">Provide hello value in hello format of `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span></span>

<span data-ttu-id="24322-223">Merhaba elde **Teklif kimliği** ve **yayımcı kimliği** hello görüntü aşağıdaki gösterildiği gibi portal, yayımlama hello gelen:</span><span class="sxs-lookup"><span data-stu-id="24322-223">Obtain hello **Offer ID** and **Publisher ID** from hello publishing portal, as shown in hello following image:</span></span>

![Teklif kimliği](./media/managed-application-author-marketplace/UniqueString_pubid_offerid.png)
        
<span data-ttu-id="24322-225">Merhaba elde **SKU kimliği**hello görüntü aşağıdaki gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="24322-225">Obtain hello **SKU ID**, as shown in hello following image:</span></span>

![SKU KİMLİĞİ](./media/managed-application-author-marketplace/UniqueString_skuid.png)
        
<span data-ttu-id="24322-227">Merhaba paketi almasını **sürüm**hello görüntü aşağıdaki gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="24322-227">Obtain hello package **Version**, as shown in hello following image:</span></span>

![Paket sürümü](./media/managed-application-author-marketplace/UniqueString_packageversion.png)
    
  <span data-ttu-id="24322-229">Örnekler önceki hello üzerinde bağlı olarak, hello değerini **PublisherPackageId** olan `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="24322-229">Based on hello preceding examples, hello value of **PublisherPackageId** is `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span></span>

  <span data-ttu-id="24322-230">Örnek mainTemplate.json:</span><span class="sxs-lookup"><span data-stu-id="24322-230">Sample mainTemplate.json:</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "storageAccountNamePrefix": {
        "type": "string",
        "metadata": {
          "description": "Specify hello name of hello storage account"
        }
      },
      "storageAccountType": {
        "type": "string"
      }
    },
    "variables": {
      "managedResourceGroup": "[concat(resourceGroup().id,uniquestring(resourceGroup().id))]"
    },
    "resources": [{
      "type": "Microsoft.Solutions/appliances",
      "apiVersion": "2016-09-01-preview",
      "name": "[concat(parameters('storageAccountNamePrefix'), '-', 'managed')]",
      "location": "[resourceGroup().location]",
      "kind": "marketplace",
      "properties": {
        "managedResourceGroupId": "[variables('managedResourceGroup')]",
        "PublisherPackageId":"azureappliancetest.ravmanagedapptest.ravpreviewmanagedsku.1.0.0",
        "parameters": {
          "storageAccountName": {
            "value": "[parameters('storageAccountNamePrefix')]"
          },
          "storageAccountType": {
            "value": "[parameters('storageAccountType')]"
          }
        }
      }
    }],
    "outputs": {

    }
  }
  ```

<span data-ttu-id="24322-231">Bu paketin diğer iç içe geçmiş şablonları içermesi veya bu uygulamayı gerekli toosuccessfully olan komutlar sağlamak.</span><span class="sxs-lookup"><span data-stu-id="24322-231">This package should contain any other nested templates or scripts that are required toosuccessfully provision this application.</span></span> <span data-ttu-id="24322-232">Merhaba mainTemplate.json, applianceMainTemplate.json ve applianceCreateUIDefinition.json dosyaları hello Kök klasörde mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="24322-232">hello mainTemplate.json, applianceMainTemplate.json, and applianceCreateUIDefinition.json files must be present at hello root folder.</span></span>

* <span data-ttu-id="24322-233">**Yetkilerini**: Bu özellik müşterilerin abonelikleri toohello kaynaklarında kimin erişim ve hello erişim düzeyini alır tanımlar.</span><span class="sxs-lookup"><span data-stu-id="24322-233">**Authorizations**: This property defines who gets access and hello level of access toohello resources in customers' subscriptions.</span></span> <span data-ttu-id="24322-234">Merhaba yayımcı toomanage hello uygulama hello müşteri adına kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24322-234">hello publisher can use it toomanage hello application on behalf of hello customer.</span></span>
* <span data-ttu-id="24322-235">**Principalıd**: Bu özellik hello Azure Active Directory (Azure AD) kullanıcı, kullanıcı grubu veya hello müşterinin aboneliğini hello kaynaklarında belirli izinleri verildi uygulama tanımlayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="24322-235">**PrincipalId**: This property is hello Azure Active Directory (Azure AD) identifier of a user, user group, or application that's granted certain permissions on hello resources in hello customer's subscription.</span></span> <span data-ttu-id="24322-236">Merhaba rol tanımı hello izinleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="24322-236">hello Role Definition describes hello permissions.</span></span> 
* <span data-ttu-id="24322-237">**Rol tanımı**: Bu özellik Azure AD tarafından sağlanan tüm hello yerleşik rol tabanlı erişim denetimi (RBAC) rolleri listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="24322-237">**Role Definition**: This property is a list of all hello built-in Role-Based Access Control (RBAC) roles provided by Azure AD.</span></span> <span data-ttu-id="24322-238">En uygun toouse toomanage hello kaynakları hello müşteri adına hello rolü seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24322-238">You can select hello role that's most appropriate toouse toomanage hello resources on behalf of hello customer.</span></span>

<span data-ttu-id="24322-239">Birden çok yetkilerini ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24322-239">You can add multiple authorizations.</span></span> <span data-ttu-id="24322-240">Bir AD kullanıcı grubu oluşturun ve kendi Kimliğini belirtin öneririz **Principalıd**.</span><span class="sxs-lookup"><span data-stu-id="24322-240">We recommend that you create an AD user group and specify its ID in **PrincipalId**.</span></span> <span data-ttu-id="24322-241">Bu şekilde hello gerek tooupdate hello SKU olmadan daha fazla kullanıcı toohello kullanıcı grubu ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24322-241">This way, you can add more users toohello user group without hello need tooupdate hello SKU.</span></span>

<span data-ttu-id="24322-242">RBAC hakkında daha fazla bilgi için bkz: [hello Azure portalında RBAC ile çalışmaya başlama](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="24322-242">For more information about RBAC, see [Get started with RBAC in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>

## <a name="marketplace-form"></a><span data-ttu-id="24322-243">Market formu</span><span class="sxs-lookup"><span data-stu-id="24322-243">Marketplace form</span></span>

<span data-ttu-id="24322-244">Merhaba Market form ister hello üzerinde görünmesini alanlar için [Azure Marketi](https://azuremarketplace.microsoft.com) ve hello [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="24322-244">hello Marketplace form asks for fields that show up on hello [Azure Marketplace](https://azuremarketplace.microsoft.com) and on hello [Azure portal](https://portal.azure.com/).</span></span>

### <a name="preview-subscription-ids"></a><span data-ttu-id="24322-245">Önizleme abonelik kimlikleri</span><span class="sxs-lookup"><span data-stu-id="24322-245">Preview subscription IDs</span></span>

<span data-ttu-id="24322-246">Azure aboneliği yayımlandıktan sonra hello teklif erişebilirsiniz kimlikleri listesini girin.</span><span class="sxs-lookup"><span data-stu-id="24322-246">Enter a list of Azure subscription IDs that can access hello offer after it's published.</span></span> <span data-ttu-id="24322-247">Bunu yapmadan önce bu abonelikleri beyaz listelenen tootest önizlemesi hello teklif kullanabilirsiniz Canlı.</span><span class="sxs-lookup"><span data-stu-id="24322-247">You can use these white-listed subscriptions tootest hello previewed offer before you make it live.</span></span> <span data-ttu-id="24322-248">Merhaba iş ortağı portalında too100 abonelikleri yukarı beyaz listesi derleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24322-248">You can compile a white list of up too100 subscriptions in hello partner portal.</span></span>

### <a name="suggested-categories"></a><span data-ttu-id="24322-249">Önerilen kategorileri</span><span class="sxs-lookup"><span data-stu-id="24322-249">Suggested categories</span></span>

<span data-ttu-id="24322-250">Toofive kategorileri teklifiniz en iyi ilişkilendirilebilir hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="24322-250">Select up toofive categories from hello list that your offer can be best associated with.</span></span> <span data-ttu-id="24322-251">Bu kategoriler kullanılan toomap hello kullanılabilir, teklif toohello ürün kategorileri şunlardır [Azure Marketi](https://azuremarketplace.microsoft.com) ve hello [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="24322-251">These categories are used toomap your offer toohello product categories that are available in hello [Azure Marketplace](https://azuremarketplace.microsoft.com) and hello [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="azure-marketplace"></a><span data-ttu-id="24322-252">Azure Market</span><span class="sxs-lookup"><span data-stu-id="24322-252">Azure Marketplace</span></span>

<span data-ttu-id="24322-253">Merhaba, yönetilen uygulamanızın özetini alanları izleyen hello görüntüler:</span><span class="sxs-lookup"><span data-stu-id="24322-253">hello summary of your managed application displays hello following fields:</span></span>

![Market özeti](./media/managed-application-author-marketplace/publishvm10.png)

<span data-ttu-id="24322-255">Merhaba **genel bakış** sekmesi, yönetilen uygulamanızın alanları izleyen hello görüntüler:</span><span class="sxs-lookup"><span data-stu-id="24322-255">hello **Overview** tab for your managed application displays hello following fields:</span></span>

![Market’e genel bakış](./media/managed-application-author-marketplace/publishvm11.png)

<span data-ttu-id="24322-257">Merhaba **planları + fiyatlandırma** sekmesi, yönetilen uygulamanızın alanları izleyen hello görüntüler:</span><span class="sxs-lookup"><span data-stu-id="24322-257">hello **Plans + Pricing** tab for your managed application displays hello following fields:</span></span>

![Market planları](./media/managed-application-author-marketplace/publishvm15.png)

#### <a name="azure-portal"></a><span data-ttu-id="24322-259">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="24322-259">Azure portal</span></span>

<span data-ttu-id="24322-260">Merhaba, yönetilen uygulamanızın özetini alanları izleyen hello görüntüler:</span><span class="sxs-lookup"><span data-stu-id="24322-260">hello summary of your managed application displays hello following fields:</span></span>

![Portal özeti](./media/managed-application-author-marketplace/publishvm12.png)

<span data-ttu-id="24322-262">Merhaba genel bakış için yönetilen uygulamanızın alanları izleyen hello görüntüler:</span><span class="sxs-lookup"><span data-stu-id="24322-262">hello overview for your managed application displays hello following fields:</span></span>

![Portal genel bakış](./media/managed-application-author-marketplace/publishvm13.png)

#### <a name="logo-guidelines"></a><span data-ttu-id="24322-264">Logo yönergeleri</span><span class="sxs-lookup"><span data-stu-id="24322-264">Logo guidelines</span></span>

<span data-ttu-id="24322-265">Merhaba bulut iş ortağı Portalı'nda karşıya logo aşağıdaki yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="24322-265">Follow these guidelines for any logo that you upload in hello Cloud Partner portal:</span></span>

*   <span data-ttu-id="24322-266">Hello Azure tasarım basit renk paleti vardır.</span><span class="sxs-lookup"><span data-stu-id="24322-266">hello Azure design has a simple color palette.</span></span> <span data-ttu-id="24322-267">Merhaba sayısı birincil ve ikincil renkleri logonuzun sınırlandırın.</span><span class="sxs-lookup"><span data-stu-id="24322-267">Limit hello number of primary and secondary colors on your logo.</span></span>
*   <span data-ttu-id="24322-268">Merhaba Tema renkleri hello portalı beyaz ve siyah.</span><span class="sxs-lookup"><span data-stu-id="24322-268">hello theme colors of hello portal are white and black.</span></span> <span data-ttu-id="24322-269">Bu renkleri hello arka plan rengi olarak logonuzun için kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="24322-269">Don't use these colors as hello background color for your logo.</span></span> <span data-ttu-id="24322-270">Logonuzun hello portalında belirgin hale getirir bir renk kullanın.</span><span class="sxs-lookup"><span data-stu-id="24322-270">Use a color that makes your logo prominent in hello portal.</span></span> <span data-ttu-id="24322-271">Basit birincil renkleri öneririz.</span><span class="sxs-lookup"><span data-stu-id="24322-271">We recommend simple primary colors.</span></span> <span data-ttu-id="24322-272">*Saydam arka plan kullanırsanız, hello logo ve metin beyaz, olduğundan emin olun siyah veya mavi.*</span><span class="sxs-lookup"><span data-stu-id="24322-272">*If you use a transparent background, make sure that hello logo and text aren't white, black, or blue.*</span></span>
*   <span data-ttu-id="24322-273">Gradyan arka planı hello logosu kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="24322-273">Don't use a gradient background on hello logo.</span></span>
*   <span data-ttu-id="24322-274">Metin hello logosu, bile, şirket veya marka adı yerleştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="24322-274">Don't place text on hello logo, not even your company or brand name.</span></span> <span data-ttu-id="24322-275">logonuzun Hello Görünüm ve yapısını, düz ve gradyan kaçının.</span><span class="sxs-lookup"><span data-stu-id="24322-275">hello look and feel of your logo should be flat and avoid gradients.</span></span>
*   <span data-ttu-id="24322-276">Hello logosu uzatılmış olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="24322-276">Make sure hello logo isn't stretched.</span></span>

#### <a name="hero-logo"></a><span data-ttu-id="24322-277">Kahramanı logosu</span><span class="sxs-lookup"><span data-stu-id="24322-277">Hero logo</span></span>

<span data-ttu-id="24322-278">Merhaba kahramanı logosu isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="24322-278">hello hero logo is optional.</span></span> <span data-ttu-id="24322-279">Merhaba yayımcı değil tooupload kahramanı logosu seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24322-279">hello publisher can choose not tooupload a hero logo.</span></span> <span data-ttu-id="24322-280">Merhaba kahramanı simgesi yüklendikten sonra silinemez.</span><span class="sxs-lookup"><span data-stu-id="24322-280">After hello hero icon is uploaded, it can't be deleted.</span></span> <span data-ttu-id="24322-281">O anda hello ortağı kahramanı simgeler için hello Market yönergelere uyması gerekir.</span><span class="sxs-lookup"><span data-stu-id="24322-281">At that time, hello partner must follow hello Marketplace guidelines for hero icons.</span></span>

<span data-ttu-id="24322-282">Merhaba kahramanı logo simgesini için aşağıdaki yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="24322-282">Follow these guidelines for hello hero logo icon:</span></span>

*   <span data-ttu-id="24322-283">Merhaba yayımcı görünen adı, hello planı başlık ve hello teklif uzun Özet beyaz görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="24322-283">hello publisher display name, hello plan title, and hello offer long summary are displayed in white.</span></span> <span data-ttu-id="24322-284">Bu nedenle, açık bir renk hello kahramanı simgesi hello arka planı için kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="24322-284">Therefore, don't use a light color for hello background of hello hero icon.</span></span> <span data-ttu-id="24322-285">Siyah, beyaz veya saydam arka plan kahramanı simgelerini izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="24322-285">A black, white, or transparent background isn't allowed for hero icons.</span></span>
*   <span data-ttu-id="24322-286">Merhaba teklif listelenen sonra hello publisher görüntüler adı, hello planı başlık, hello teklif uzun Özet ve hello **oluşturma** düğmesi program aracılığıyla hello kahramanı logosunun içinde katıştırılmış.</span><span class="sxs-lookup"><span data-stu-id="24322-286">After hello offer is listed, hello publisher display name, hello plan title, hello offer long summary, and hello **Create** button are embedded programmatically inside hello hero logo.</span></span> <span data-ttu-id="24322-287">Sonuç olarak, hello kahramanı logosu tasarlarken herhangi bir metin girmeyin.</span><span class="sxs-lookup"><span data-stu-id="24322-287">Consequently, don't enter any text while you design hello hero logo.</span></span> <span data-ttu-id="24322-288">Merhaba metni program aracılığıyla bu alana dahil olduğundan boş alanı hello üzerinde sağ bırakın.</span><span class="sxs-lookup"><span data-stu-id="24322-288">Leave empty space on hello right because hello text is included programmatically in that space.</span></span> <span data-ttu-id="24322-289">Merhaba boş alan hello metin hello sağ üzerinde 415 x 100 piksel olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="24322-289">hello empty space for hello text should be 415 x 100 pixels on hello right.</span></span> <span data-ttu-id="24322-290">Merhaba soldan 370 piksel uzakta bulunur.</span><span class="sxs-lookup"><span data-stu-id="24322-290">It's offset by 370 pixels from hello left.</span></span>

    ![Kahramanı logosu örneği](./media/managed-application-author-marketplace/publishvm14.png)

## <a name="support-form"></a><span data-ttu-id="24322-292">Form desteği</span><span class="sxs-lookup"><span data-stu-id="24322-292">Support form</span></span>

<span data-ttu-id="24322-293">Merhaba doldurun **Destek** kişiler şirketinizden desteğiyle formu.</span><span class="sxs-lookup"><span data-stu-id="24322-293">Fill out hello **Support** form with support contacts from your company.</span></span> <span data-ttu-id="24322-294">Bu bilgileri, kişiler ve müşteri destek ilgili kişisi mühendislik.</span><span class="sxs-lookup"><span data-stu-id="24322-294">This information might be engineering contacts and customer support contacts.</span></span>

## <a name="publish-an-offer"></a><span data-ttu-id="24322-295">Bir teklifi yayımlama</span><span class="sxs-lookup"><span data-stu-id="24322-295">Publish an offer</span></span>

<span data-ttu-id="24322-296">Tüm hello bölümleri doldurduktan sonra seçin **Yayımla** , teklif kullanılabilir toocustomers yapar toostart hello işlemi.</span><span class="sxs-lookup"><span data-stu-id="24322-296">After you fill out all hello sections, select **Publish** toostart hello process that makes your offer available toocustomers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24322-297">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="24322-297">Next steps</span></span>

* <span data-ttu-id="24322-298">Bir giriş toomanaged uygulamalar için bkz [yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="24322-298">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="24322-299">Merhaba Market yönetilen bir uygulamadan kullanma hakkında daha fazla bilgi için bkz: [tüketen Azure hello Market uygulamalarda yönetilen](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="24322-299">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="24322-300">Hizmet Kataloğu yönetilen uygulama yayımlama hakkında daha fazla bilgi için bkz: [oluşturma ve bir hizmet Kataloğu yönetilen uygulamayı yayımlayın](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="24322-300">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="24322-301">Hizmet Kataloğu yönetilen uygulama kullanma hakkında daha fazla bilgi için bkz: [bir hizmet Kataloğu yönetilen uygulama tüketen](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="24322-301">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
