---
title: "Azure Market uygulamalarda yönetilen | Microsoft Docs"
description: "Azure açıklar yönetilen Market üzerinden kullanılabilir uygulamalar."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 58ac7665abf7e75a43bb0b92bdf6f41005c3efe8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-managed-applications-in-the-marketplace"></a><span data-ttu-id="a0369-103">Market'te Azure yönetilen uygulamalar</span><span class="sxs-lookup"><span data-stu-id="a0369-103">Azure managed applications in the Marketplace</span></span>

 <span data-ttu-id="a0369-104">MSP'ler, ISV ve sistem tümleştiricileri (SIS) Azure kullanabileceğiniz yönetilen tüm Azure Marketi müşterilere çözümleri sunmak için uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="a0369-104">MSPs, ISVs, and system integrators (SIs) can use Azure managed applications to offer their solutions to all Azure Marketplace customers.</span></span> <span data-ttu-id="a0369-105">Bu tür çözümler, Bakım ve müşteriler için ek yükü bakım azaltın.</span><span class="sxs-lookup"><span data-stu-id="a0369-105">Such solutions reduce the maintenance and servicing overhead for customers.</span></span> <span data-ttu-id="a0369-106">Yayımcılar, altyapı ve yazılım Market üzerinden satmak.</span><span class="sxs-lookup"><span data-stu-id="a0369-106">Publishers can sell infrastructure and software through the Marketplace.</span></span> <span data-ttu-id="a0369-107">Yönetilen uygulamaların bunlar Hizmetleri ve işletimsel destek ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0369-107">They can attach services and operational support to managed applications.</span></span> <span data-ttu-id="a0369-108">Daha fazla bilgi için bkz: [yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a0369-108">For more information, see [Managed application overview](managed-application-overview.md).</span></span>

<span data-ttu-id="a0369-109">Bu makalede, nasıl bir MSP, ISV veya SI Marketi'nde uygulama yayımlama ve müşterilere geniş çapta kullanılabilir hale açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a0369-109">This article explains how an MSP, ISV, or SI can publish an application to the Marketplace and make it broadly available to customers.</span></span>

## <a name="prerequisites-for-publishing-a-managed-application"></a><span data-ttu-id="a0369-110">Yönetilen bir uygulamayı yayımlamak için Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="a0369-110">Prerequisites for publishing a managed application</span></span>

<span data-ttu-id="a0369-111">Market listesindeki için Önkoşullar:</span><span class="sxs-lookup"><span data-stu-id="a0369-111">Prerequisites to listing in the Marketplace:</span></span>

* <span data-ttu-id="a0369-112">Teknik</span><span class="sxs-lookup"><span data-stu-id="a0369-112">Technical</span></span>

    *  <span data-ttu-id="a0369-113">Temel yapısını ve Azure Resource Manager şablonları sözdizimi hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a0369-113">For information about the basic structure and syntax of Azure Resource Manager templates, see [Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
    *  <span data-ttu-id="a0369-114">Tam veri şablonunun çözümleri görüntülemek için bkz: [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/en-us/documentation/templates/) veya [Hızlı Başlangıç şablonu deposu](https://github.com/azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="a0369-114">To view complete template solutions, see [Azure Quickstart templates](https://azure.microsoft.com/en-us/documentation/templates/) or the [Quickstart template repository](https://github.com/azure/azure-quickstart-templates).</span></span>
    *  <span data-ttu-id="a0369-115">Market üzerinden uygulamanızı dağıtmak müşteriler arabirimi oluşturma hakkında daha fazla bilgi için bkz: [bir kullanıcı arabirimi tanımı dosyası oluşturma](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a0369-115">For information about how to create the interface for customers who deploy your application through the Marketplace, see [Create a user interface definition file](managed-application-createuidefinition-overview.md).</span></span>

* <span data-ttu-id="a0369-116">Yedeğin (iş gereksinimlerini)</span><span class="sxs-lookup"><span data-stu-id="a0369-116">Nontechnical (business requirements)</span></span>

    *   <span data-ttu-id="a0369-117">Şirketiniz veya onun yan burada satış Marketi tarafından desteklenen bir ülkede bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a0369-117">Your company or its subsidiary must be located in a country where sales are supported by the Marketplace.</span></span>
    *   <span data-ttu-id="a0369-118">Ürünü Marketi tarafından desteklenen faturalama modelleri ile uyumlu şekilde lisansına sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a0369-118">Your product must be licensed in a way that is compatible with billing models supported by the Marketplace.</span></span>
    *   <span data-ttu-id="a0369-119">Teknik Destek kullanılabilir müşterilere bir ticari koşulların elverdiği oranda makul şekilde yapmaktan sorumlu.</span><span class="sxs-lookup"><span data-stu-id="a0369-119">You're responsible for making technical support available to customers in a commercially reasonable manner.</span></span> <span data-ttu-id="a0369-120">Destek Ücretli, boş veya topluluk desteklemez.</span><span class="sxs-lookup"><span data-stu-id="a0369-120">The support can be free, paid, or through community support.</span></span>
    *   <span data-ttu-id="a0369-121">Yazılım ve üçüncü taraf yazılım bağımlılıkları lisansı sağlamaktan sorumlu.</span><span class="sxs-lookup"><span data-stu-id="a0369-121">You're responsible for licensing your software and any third-party software dependencies.</span></span>
    *   <span data-ttu-id="a0369-122">Teklifinizle Market ve Azure portalını listelenmiş ölçütlerini karşılayan içerik sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a0369-122">You must provide content that meets criteria for your offering to be listed in the Marketplace and in the Azure portal.</span></span>
    *   <span data-ttu-id="a0369-123">Azure Market katılım ilkeleri ve yayımcı Sözleşmesi koşullarını kabul etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a0369-123">You must agree to the terms of the Azure Marketplace Participation Policies and Publisher Agreement.</span></span>
    *   <span data-ttu-id="a0369-124">Kullanım koşulları, Microsoft gizlilik bildirimi ve Microsoft Azure sertifikalı Program sözleşmesi uymak kabul etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a0369-124">You must agree to comply with the Terms of Use, Microsoft Privacy Statement, and Microsoft Azure Certified Program Agreement.</span></span>

## <a name="create-a-new-azure-application-offer"></a><span data-ttu-id="a0369-125">Yeni bir Azure uygulama teklifi oluşturma</span><span class="sxs-lookup"><span data-stu-id="a0369-125">Create a new Azure application offer</span></span>

<span data-ttu-id="a0369-126">Önkoşulları karşılaması sonra yönetilen uygulamayı teklifiniz oluşturmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="a0369-126">After you meet the prerequisites, you're ready to create your managed application offer.</span></span> <span data-ttu-id="a0369-127">Bir teklif ve bir SKU hızlı bir genel bakış atalım.</span><span class="sxs-lookup"><span data-stu-id="a0369-127">Let's take a quick overview of an offer and a SKU.</span></span>

### <a name="offer"></a><span data-ttu-id="a0369-128">Sunduğu</span><span class="sxs-lookup"><span data-stu-id="a0369-128">Offer</span></span>

<span data-ttu-id="a0369-129">Teklif yönetilen bir uygulama için bir sınıf bir yayımcıdan sunumu ürünün karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="a0369-129">The offer for a managed application corresponds to a class of product offering from a publisher.</span></span> <span data-ttu-id="a0369-130">Market kullanılabilir hale getirmek istediğiniz çözüm/uygulama yeni bir tür varsa, bunu yeni bir teklif ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0369-130">If you have a new type of solution/application that you want to make available in the Marketplace, you can set it up as a new offer.</span></span> <span data-ttu-id="a0369-131">Bir teklif, SKU'ları koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="a0369-131">An offer is a collection of SKUs.</span></span> <span data-ttu-id="a0369-132">Her teklif Market'te kendi varlık olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="a0369-132">Every offer appears as its own entity in the Marketplace.</span></span>

### <a name="sku"></a><span data-ttu-id="a0369-133">SKU</span><span class="sxs-lookup"><span data-stu-id="a0369-133">SKU</span></span>

<span data-ttu-id="a0369-134">Bir SKU en küçük purchasable bir teklif birimidir.</span><span class="sxs-lookup"><span data-stu-id="a0369-134">A SKU is the smallest purchasable unit of an offer.</span></span> <span data-ttu-id="a0369-135">Aynı ürün sınıfı (teklif) içinde bir SKU arasında ayırt etmek için kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a0369-135">You can use a SKU within the same product class (offer) to differentiate between:</span></span>

* <span data-ttu-id="a0369-136">Desteklenen farklı özellikleri.</span><span class="sxs-lookup"><span data-stu-id="a0369-136">Different features that are supported.</span></span>
* <span data-ttu-id="a0369-137">Teklif yönetilen yönetilmeyen mı.</span><span class="sxs-lookup"><span data-stu-id="a0369-137">Whether the offer is managed or unmanaged.</span></span>
* <span data-ttu-id="a0369-138">Desteklenen faturalama modelleri.</span><span class="sxs-lookup"><span data-stu-id="a0369-138">Billing models that are supported.</span></span>

<span data-ttu-id="a0369-139">Bir SKU Market'te üst teklif altında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a0369-139">A SKU appears under the parent offer in the Marketplace.</span></span> <span data-ttu-id="a0369-140">Azure portalında purchasable kendi varlık olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="a0369-140">It appears as its own purchasable entity in the Azure portal.</span></span>

### <a name="set-up-an-offer"></a><span data-ttu-id="a0369-141">Bir teklif ayarlayın</span><span class="sxs-lookup"><span data-stu-id="a0369-141">Set up an offer</span></span>

1. <span data-ttu-id="a0369-142">Oturum [bulut iş ortağı portalına](https://cloudpartner.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a0369-142">Sign in to the [Cloud Partner portal](https://cloudpartner.azure.com/).</span></span>

2. <span data-ttu-id="a0369-143">Sol gezinti bölmesinde seçin **+ yeni teklif** > **Azure uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="a0369-143">In the navigation pane on the left, select **+ New offer** > **Azure Applications**.</span></span>

    ![Yeni teklif](./media/managed-application-author-marketplace/newOffer.png)

3. <span data-ttu-id="a0369-145">Sol tarafta görünür form doldurmak **Düzenleyicisi** görünümü.</span><span class="sxs-lookup"><span data-stu-id="a0369-145">Fill out the forms that appear on the left in the **Editor** view.</span></span> <span data-ttu-id="a0369-146">Gerekli alanları ile kırmızı yıldız işareti (*) işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="a0369-146">Required fields are marked with a red asterisk (*).</span></span>

    ![Teklif ayarları](./media/managed-application-author-marketplace/newOffer_OfferSettings.png)

    <span data-ttu-id="a0369-148">Dört ana formlar, yönetilen bir uygulama oluşturmak için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="a0369-148">Four main forms are used to create a managed application:</span></span>

    <span data-ttu-id="a0369-149">a.</span><span class="sxs-lookup"><span data-stu-id="a0369-149">a.</span></span> <span data-ttu-id="a0369-150">Teklif ayarları</span><span class="sxs-lookup"><span data-stu-id="a0369-150">Offer Settings</span></span>

    <span data-ttu-id="a0369-151">b.</span><span class="sxs-lookup"><span data-stu-id="a0369-151">b.</span></span> <span data-ttu-id="a0369-152">SKU'ları</span><span class="sxs-lookup"><span data-stu-id="a0369-152">SKUs</span></span>

    <span data-ttu-id="a0369-153">c.</span><span class="sxs-lookup"><span data-stu-id="a0369-153">c.</span></span> <span data-ttu-id="a0369-154">Market</span><span class="sxs-lookup"><span data-stu-id="a0369-154">Marketplace</span></span>

    <span data-ttu-id="a0369-155">d.</span><span class="sxs-lookup"><span data-stu-id="a0369-155">d.</span></span> <span data-ttu-id="a0369-156">Destek</span><span class="sxs-lookup"><span data-stu-id="a0369-156">Support</span></span>

<span data-ttu-id="a0369-157">Bu form, aşağıdaki bölümlerde daha ayrıntılı açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a0369-157">These forms are described in greater detail in the following sections.</span></span>

## <a name="offer-settings-form"></a><span data-ttu-id="a0369-158">Teklif ayarları formu</span><span class="sxs-lookup"><span data-stu-id="a0369-158">Offer Settings form</span></span>
<span data-ttu-id="a0369-159">Teklif ayarlarını belirtmek için temel bu formu kullanın.</span><span class="sxs-lookup"><span data-stu-id="a0369-159">Use this basic form to specify the offer settings.</span></span>

1. <span data-ttu-id="a0369-160">Doldurmak **teklif ayarları** formu.</span><span class="sxs-lookup"><span data-stu-id="a0369-160">Fill in the **Offer Settings** form.</span></span> <span data-ttu-id="a0369-161">Farklı alanları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a0369-161">The different fields are:</span></span>

    <span data-ttu-id="a0369-162">a.</span><span class="sxs-lookup"><span data-stu-id="a0369-162">a.</span></span> <span data-ttu-id="a0369-163">**Teklif kodu**: Yayımcı profilindeki teklif bu benzersiz tanımlayıcı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a0369-163">**Offer ID**: This unique identifier identifies the offer within a publisher profile.</span></span> <span data-ttu-id="a0369-164">Bu kimliği ürün URL'ler, Resource Manager şablonları görünür ve faturalama raporlar.</span><span class="sxs-lookup"><span data-stu-id="a0369-164">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="a0369-165">Yalnızca küçük harf alfasayısal karakterler veya tire (-) birleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="a0369-165">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="a0369-166">Kimliği, bir tire bitemez.</span><span class="sxs-lookup"><span data-stu-id="a0369-166">The ID can't end in a dash.</span></span> <span data-ttu-id="a0369-167">Buna ait sınırlı en çok 50 karakter.</span><span class="sxs-lookup"><span data-stu-id="a0369-167">It's limited to a maximum of 50 characters.</span></span> <span data-ttu-id="a0369-168">Bu alan, bir teklif Canlı göründükten sonra kilitlendi.</span><span class="sxs-lookup"><span data-stu-id="a0369-168">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="a0369-169">b.</span><span class="sxs-lookup"><span data-stu-id="a0369-169">b.</span></span> <span data-ttu-id="a0369-170">**Yayımcı kimliği**: Bu teklif altında yayımlamak istediğiniz yayımcı profilini seçmek için bu açılan listeyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="a0369-170">**Publisher ID**: Use this drop-down list to choose the publisher profile you want to publish this offer under.</span></span> <span data-ttu-id="a0369-171">Bu alan, bir teklif Canlı göründükten sonra kilitlendi.</span><span class="sxs-lookup"><span data-stu-id="a0369-171">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="a0369-172">c.</span><span class="sxs-lookup"><span data-stu-id="a0369-172">c.</span></span> <span data-ttu-id="a0369-173">**Ad**: teklifiniz için bu görünen ad Market ve Portalı'nda görünür.</span><span class="sxs-lookup"><span data-stu-id="a0369-173">**Name**: This display name for your offer appears in the Marketplace and in the portal.</span></span> <span data-ttu-id="a0369-174">En çok 50 karakter olabilir.</span><span class="sxs-lookup"><span data-stu-id="a0369-174">It can have a maximum of 50 characters.</span></span> <span data-ttu-id="a0369-175">Ürününüzün tanınabilir bir marka adını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a0369-175">Include a recognizable brand name for your product.</span></span> <span data-ttu-id="a0369-176">Nasıl pazarlama olmadığı sürece, şirketinizin adını buraya dahil etmeyin.</span><span class="sxs-lookup"><span data-stu-id="a0369-176">Don't include your company name here unless that's how it's marketed.</span></span> <span data-ttu-id="a0369-177">Kendi Web sitesinde bu teklif pazarlama, adı tam olarak, Web sitenizde şu şekilde görünür durumda olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a0369-177">If you're marketing this offer on your own website, ensure that the name is exactly how it appears on your website.</span></span>

2. <span data-ttu-id="a0369-178">Seçin **kaydetmek** ilerleme durumunuzu kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="a0369-178">Select **Save** to save your progress.</span></span> 

## <a name="skus-form"></a><span data-ttu-id="a0369-179">SKU'ları formu</span><span class="sxs-lookup"><span data-stu-id="a0369-179">SKUs form</span></span>
<span data-ttu-id="a0369-180">Sonraki adım, teklifiniz için SKU'ları eklemektir.</span><span class="sxs-lookup"><span data-stu-id="a0369-180">The next step is to add SKUs for your offer.</span></span>

1. <span data-ttu-id="a0369-181">Seçin **SKU'ları** > **yeni SKU**.</span><span class="sxs-lookup"><span data-stu-id="a0369-181">Select **SKUs** > **New SKU**.</span></span> 

    ![Yeni SKU seçin](./media/managed-application-author-marketplace/newOffer_skus.png)

2. <span data-ttu-id="a0369-183">Girin bir **SKU kimliği**.</span><span class="sxs-lookup"><span data-stu-id="a0369-183">Enter a **SKU ID**.</span></span> <span data-ttu-id="a0369-184">Bir teklif içinde SKU için benzersiz bir tanımlayıcı SKU kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="a0369-184">A SKU ID is a unique identifier for the SKU within an offer.</span></span> <span data-ttu-id="a0369-185">Bu kimliği ürün URL'ler, Resource Manager şablonları görünür ve faturalama raporlar.</span><span class="sxs-lookup"><span data-stu-id="a0369-185">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="a0369-186">Yalnızca küçük harf alfasayısal karakterler veya tire (-) birleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="a0369-186">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="a0369-187">Kimliği, tire ve buna ait en çok 50 karakter sınırlı bitemez.</span><span class="sxs-lookup"><span data-stu-id="a0369-187">The ID can't end in a dash, and it's limited to a maximum of 50 characters.</span></span> <span data-ttu-id="a0369-188">Bu alan, bir teklif Canlı göründükten sonra kilitlendi.</span><span class="sxs-lookup"><span data-stu-id="a0369-188">After an offer goes live, this field is locked.</span></span> <span data-ttu-id="a0369-189">Bir teklif içinde birden çok SKU olabilir.</span><span class="sxs-lookup"><span data-stu-id="a0369-189">You can have multiple SKUs within an offer.</span></span> <span data-ttu-id="a0369-190">Bir SKU yayımlamayı düşündüğünüz her görüntü için gerekir.</span><span class="sxs-lookup"><span data-stu-id="a0369-190">You need a SKU for each image you plan to publish.</span></span>

3. <span data-ttu-id="a0369-191">Doldurmak **SKU ayrıntıları** aşağıdaki formda bölümü:</span><span class="sxs-lookup"><span data-stu-id="a0369-191">Fill out the **SKU Details** section on the following form:</span></span>

    ![Yeni SKU sağlayın](./media/managed-application-author-marketplace/newOffer_newsku.png)

    <span data-ttu-id="a0369-193">Aşağıdaki alanları doldurun:</span><span class="sxs-lookup"><span data-stu-id="a0369-193">Fill out the following fields:</span></span>
    
    <span data-ttu-id="a0369-194">a.</span><span class="sxs-lookup"><span data-stu-id="a0369-194">a.</span></span> <span data-ttu-id="a0369-195">**Başlık**: Bu SKU için bir başlık girin.</span><span class="sxs-lookup"><span data-stu-id="a0369-195">**Title**: Enter a title for this SKU.</span></span> <span data-ttu-id="a0369-196">Bu öğe için galerisinde bu başlığı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a0369-196">This title appears in the gallery for this item.</span></span>

    <span data-ttu-id="a0369-197">b.</span><span class="sxs-lookup"><span data-stu-id="a0369-197">b.</span></span> <span data-ttu-id="a0369-198">**Özet**: kısa bir özeti için bu SKU girin.</span><span class="sxs-lookup"><span data-stu-id="a0369-198">**Summary**: Enter a short summary for this SKU.</span></span> <span data-ttu-id="a0369-199">Bu metin başlığı altında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a0369-199">This text appears underneath the title.</span></span>

    <span data-ttu-id="a0369-200">c.</span><span class="sxs-lookup"><span data-stu-id="a0369-200">c.</span></span> <span data-ttu-id="a0369-201">**Açıklama**: SKU hakkında ayrıntılı bir açıklama girin.</span><span class="sxs-lookup"><span data-stu-id="a0369-201">**Description**: Enter a detailed description about the SKU.</span></span>

    <span data-ttu-id="a0369-202">d.</span><span class="sxs-lookup"><span data-stu-id="a0369-202">d.</span></span> <span data-ttu-id="a0369-203">**SKU tür**: izin verilen değerler: **yönetilen uygulamayı** ve **çözüm şablonları**.</span><span class="sxs-lookup"><span data-stu-id="a0369-203">**SKU Type**: The allowed values are **Managed Application** and **Solution Templates**.</span></span> <span data-ttu-id="a0369-204">Bu durumda, seçin **yönetilen uygulamayı**.</span><span class="sxs-lookup"><span data-stu-id="a0369-204">For this case, select **Managed Application**.</span></span>

4. <span data-ttu-id="a0369-205">Doldurmak **Paket ayrıntılarını** aşağıdaki formda bölümü:</span><span class="sxs-lookup"><span data-stu-id="a0369-205">Fill out the **Package Details** section on the following form:</span></span>

    ![Paket](./media/managed-application-author-marketplace/newOffer_newsku_package.png)

    <span data-ttu-id="a0369-207">Aşağıdaki alanları doldurun:</span><span class="sxs-lookup"><span data-stu-id="a0369-207">Fill out the following fields:</span></span>

    <span data-ttu-id="a0369-208">a.</span><span class="sxs-lookup"><span data-stu-id="a0369-208">a.</span></span> <span data-ttu-id="a0369-209">**Geçerli sürüm**: karşıya yüklediğiniz paket için bir sürümü girin.</span><span class="sxs-lookup"><span data-stu-id="a0369-209">**Current Version**: Enter a version for the package you upload.</span></span> <span data-ttu-id="a0369-210">Şu biçimde olmalıdır `{number}.{number}.{number}{number}`.</span><span class="sxs-lookup"><span data-stu-id="a0369-210">It should be in the format `{number}.{number}.{number}{number}`.</span></span>

    <span data-ttu-id="a0369-211">b.</span><span class="sxs-lookup"><span data-stu-id="a0369-211">b.</span></span> <span data-ttu-id="a0369-212">**Bir paket dosyası seçmek**: Bu paket bir .zip dosyasına sıkıştırılmış aşağıdaki dosyaları içerir:</span><span class="sxs-lookup"><span data-stu-id="a0369-212">**Select a package file**: This package contains the following files that are compressed into a .zip file:</span></span>
    * <span data-ttu-id="a0369-213">**applianceMainTemplate.json**: Çözüm/uygulama dağıtmak için kullanılan dağıtım şablon dosyası.</span><span class="sxs-lookup"><span data-stu-id="a0369-213">**applianceMainTemplate.json**: The deployment template file that's used to deploy the solution/application.</span></span> <span data-ttu-id="a0369-214">Dağıtım şablonu dosyaları oluşturma hakkında daha fazla bilgi için bkz: [, ilk Azure Resource Manager şablonu oluşturma](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="a0369-214">For information about how to create deployment template files, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>
    * <span data-ttu-id="a0369-215">**appliancecreateUIDefinition.json**: Bu dosya bu çözümü/uygulama sağlamak için kullanılan kullanıcı arabirimi oluşturmak için Azure portal tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a0369-215">**appliancecreateUIDefinition.json**: This file is used by the Azure portal to generate the user interface that's used to provision this solution/application.</span></span> <span data-ttu-id="a0369-216">Daha fazla bilgi için bkz: [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a0369-216">For more information, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
    * <span data-ttu-id="a0369-217">**mainTemplate.json**: Bu şablon dosyası, yalnızca Microsoft.Solution/appliances kaynak içeriyor.</span><span class="sxs-lookup"><span data-stu-id="a0369-217">**mainTemplate.json**: This template file contains only the Microsoft.Solution/appliances resource.</span></span> <span data-ttu-id="a0369-218">MainTemplate dosyası, aşağıdaki özellikleri içerir:</span><span class="sxs-lookup"><span data-stu-id="a0369-218">The mainTemplate file includes the following properties:</span></span>

        *  <span data-ttu-id="a0369-219">**tür**: kullanım **Market** Market'te yönetilen uygulamalar için.</span><span class="sxs-lookup"><span data-stu-id="a0369-219">**kind**: Use **Marketplace** for managed applications in the Marketplace.</span></span>
        *  <span data-ttu-id="a0369-220">**ManagedResourceGroupId**: applianceMainTemplate.json içinde tanımlanan tüm kaynaklara dağıtıldığı müşterinin aboneliğini bu kaynak grubunda bulunuyor.</span><span class="sxs-lookup"><span data-stu-id="a0369-220">**ManagedResourceGroupId**: This resource group in the customer's subscription is where all the resources defined in applianceMainTemplate.json are deployed.</span></span>
        *  <span data-ttu-id="a0369-221">**PublisherPackageId**: Bu dize paketi benzersiz olarak tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a0369-221">**PublisherPackageId**: This string uniquely identifies the package.</span></span> <span data-ttu-id="a0369-222">Değer biçiminde sağlayın `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span><span class="sxs-lookup"><span data-stu-id="a0369-222">Provide the value in the format of `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span></span>

<span data-ttu-id="a0369-223">Elde **Teklif kimliği** ve **yayımcı kimliği** Yayımlama Portalı, aşağıdaki resimde gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="a0369-223">Obtain the **Offer ID** and **Publisher ID** from the publishing portal, as shown in the following image:</span></span>

![Teklif kimliği](./media/managed-application-author-marketplace/UniqueString_pubid_offerid.png)
        
<span data-ttu-id="a0369-225">Elde **SKU kimliği**aşağıdaki görüntüde gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="a0369-225">Obtain the **SKU ID**, as shown in the following image:</span></span>

![SKU KİMLİĞİ](./media/managed-application-author-marketplace/UniqueString_skuid.png)
        
<span data-ttu-id="a0369-227">Paket elde **sürüm**aşağıdaki görüntüde gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="a0369-227">Obtain the package **Version**, as shown in the following image:</span></span>

![Paket sürümü](./media/managed-application-author-marketplace/UniqueString_packageversion.png)
    
  <span data-ttu-id="a0369-229">Değerini önceki örneklerde dayalı **PublisherPackageId** olan `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="a0369-229">Based on the preceding examples, the value of **PublisherPackageId** is `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span></span>

  <span data-ttu-id="a0369-230">Örnek mainTemplate.json:</span><span class="sxs-lookup"><span data-stu-id="a0369-230">Sample mainTemplate.json:</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "storageAccountNamePrefix": {
        "type": "string",
        "metadata": {
          "description": "Specify the name of the storage account"
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

<span data-ttu-id="a0369-231">Bu paket, herhangi bir iç içe geçmiş şablonları veya bu uygulama başarıyla hazırlamak için gereken komut dosyaları içermelidir.</span><span class="sxs-lookup"><span data-stu-id="a0369-231">This package should contain any other nested templates or scripts that are required to successfully provision this application.</span></span> <span data-ttu-id="a0369-232">MainTemplate.json applianceMainTemplate.json applianceCreateUIDefinition.json dosyaları ve kök klasörde mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a0369-232">The mainTemplate.json, applianceMainTemplate.json, and applianceCreateUIDefinition.json files must be present at the root folder.</span></span>

* <span data-ttu-id="a0369-233">**Yetkilerini**: Bu özellik müşterilerin Aboneliklerde kimlerin erişimi ve kaynaklara erişim düzeyini alır tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a0369-233">**Authorizations**: This property defines who gets access and the level of access to the resources in customers' subscriptions.</span></span> <span data-ttu-id="a0369-234">Yayımcı, uygulama müşteri adına yönetmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0369-234">The publisher can use it to manage the application on behalf of the customer.</span></span>
* <span data-ttu-id="a0369-235">**Principalıd**: Bu özellik bir kullanıcının, kullanıcı grubu veya Müşteri'nin aboneliğindeki kaynaklar belirli izinleri verildi uygulama Azure Active Directory (Azure AD) tanımlayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="a0369-235">**PrincipalId**: This property is the Azure Active Directory (Azure AD) identifier of a user, user group, or application that's granted certain permissions on the resources in the customer's subscription.</span></span> <span data-ttu-id="a0369-236">Rol tanımı izinleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="a0369-236">The Role Definition describes the permissions.</span></span> 
* <span data-ttu-id="a0369-237">**Rol tanımı**: Bu özellik Azure AD tarafından sağlanan tüm yerleşik rol tabanlı erişim denetimi (RBAC) rollerini listesidir.</span><span class="sxs-lookup"><span data-stu-id="a0369-237">**Role Definition**: This property is a list of all the built-in Role-Based Access Control (RBAC) roles provided by Azure AD.</span></span> <span data-ttu-id="a0369-238">Kaynakları müşteri adına yönetmek üzere kullanmak en uygun olan rolü seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0369-238">You can select the role that's most appropriate to use to manage the resources on behalf of the customer.</span></span>

<span data-ttu-id="a0369-239">Birden çok yetkilerini ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0369-239">You can add multiple authorizations.</span></span> <span data-ttu-id="a0369-240">Bir AD kullanıcı grubu oluşturun ve kendi Kimliğini belirtin öneririz **Principalıd**.</span><span class="sxs-lookup"><span data-stu-id="a0369-240">We recommend that you create an AD user group and specify its ID in **PrincipalId**.</span></span> <span data-ttu-id="a0369-241">Bu şekilde, kullanıcı grubu SKU güncelleştirmeye gerek olmadan daha fazla kullanıcı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0369-241">This way, you can add more users to the user group without the need to update the SKU.</span></span>

<span data-ttu-id="a0369-242">RBAC hakkında daha fazla bilgi için bkz: [Azure portalında RBAC ile çalışmaya başlama](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="a0369-242">For more information about RBAC, see [Get started with RBAC in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>

## <a name="marketplace-form"></a><span data-ttu-id="a0369-243">Market formu</span><span class="sxs-lookup"><span data-stu-id="a0369-243">Marketplace form</span></span>

<span data-ttu-id="a0369-244">Market form üzerinde göster alanların ister [Azure Marketi](https://azuremarketplace.microsoft.com) ve [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a0369-244">The Marketplace form asks for fields that show up on the [Azure Marketplace](https://azuremarketplace.microsoft.com) and on the [Azure portal](https://portal.azure.com/).</span></span>

### <a name="preview-subscription-ids"></a><span data-ttu-id="a0369-245">Önizleme abonelik kimlikleri</span><span class="sxs-lookup"><span data-stu-id="a0369-245">Preview subscription IDs</span></span>

<span data-ttu-id="a0369-246">Azure aboneliği yayımlandıktan sonra teklif erişebileceği kimlikleri listesini girin.</span><span class="sxs-lookup"><span data-stu-id="a0369-246">Enter a list of Azure subscription IDs that can access the offer after it's published.</span></span> <span data-ttu-id="a0369-247">Bunu yapmadan önce önizleme uygulanan teklif test etmek için bu beyaz listelenen abonelikleri kullanabileceğiniz Canlı.</span><span class="sxs-lookup"><span data-stu-id="a0369-247">You can use these white-listed subscriptions to test the previewed offer before you make it live.</span></span> <span data-ttu-id="a0369-248">İş ortağı portalında en fazla 100 abonelikleri beyaz listesi derleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0369-248">You can compile a white list of up to 100 subscriptions in the partner portal.</span></span>

### <a name="suggested-categories"></a><span data-ttu-id="a0369-249">Önerilen kategorileri</span><span class="sxs-lookup"><span data-stu-id="a0369-249">Suggested categories</span></span>

<span data-ttu-id="a0369-250">Teklifiniz en iyi ile ilişkilendirilebilir listesinden en fazla beş kategorilerini seçin.</span><span class="sxs-lookup"><span data-stu-id="a0369-250">Select up to five categories from the list that your offer can be best associated with.</span></span> <span data-ttu-id="a0369-251">Bu kategoriler kullanılabilir olan ürün kategorilerini teklifiniz eşlemek için kullanılır [Azure Marketi](https://azuremarketplace.microsoft.com) ve [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a0369-251">These categories are used to map your offer to the product categories that are available in the [Azure Marketplace](https://azuremarketplace.microsoft.com) and the [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="azure-marketplace"></a><span data-ttu-id="a0369-252">Azure Market</span><span class="sxs-lookup"><span data-stu-id="a0369-252">Azure Marketplace</span></span>

<span data-ttu-id="a0369-253">Aşağıdaki alanları, yönetilen uygulamanızın özetini görüntüler:</span><span class="sxs-lookup"><span data-stu-id="a0369-253">The summary of your managed application displays the following fields:</span></span>

![Market özeti](./media/managed-application-author-marketplace/publishvm10.png)

<span data-ttu-id="a0369-255">**Genel bakış** aşağıdaki alanları, yönetilen uygulamanızın görüntüler sekmesi:</span><span class="sxs-lookup"><span data-stu-id="a0369-255">The **Overview** tab for your managed application displays the following fields:</span></span>

![Market’e genel bakış](./media/managed-application-author-marketplace/publishvm11.png)

<span data-ttu-id="a0369-257">**Planları + fiyatlandırma** aşağıdaki alanları, yönetilen uygulamanızın görüntüler sekmesi:</span><span class="sxs-lookup"><span data-stu-id="a0369-257">The **Plans + Pricing** tab for your managed application displays the following fields:</span></span>

![Market planları](./media/managed-application-author-marketplace/publishvm15.png)

#### <a name="azure-portal"></a><span data-ttu-id="a0369-259">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="a0369-259">Azure portal</span></span>

<span data-ttu-id="a0369-260">Aşağıdaki alanları, yönetilen uygulamanızın özetini görüntüler:</span><span class="sxs-lookup"><span data-stu-id="a0369-260">The summary of your managed application displays the following fields:</span></span>

![Portal özeti](./media/managed-application-author-marketplace/publishvm12.png)

<span data-ttu-id="a0369-262">Genel bakış, yönetilen uygulamanızın için aşağıdaki alanları görüntüler:</span><span class="sxs-lookup"><span data-stu-id="a0369-262">The overview for your managed application displays the following fields:</span></span>

![Portal genel bakış](./media/managed-application-author-marketplace/publishvm13.png)

#### <a name="logo-guidelines"></a><span data-ttu-id="a0369-264">Logo yönergeleri</span><span class="sxs-lookup"><span data-stu-id="a0369-264">Logo guidelines</span></span>

<span data-ttu-id="a0369-265">Bulut iş ortağı Portalı'nda karşıya logo aşağıdaki yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="a0369-265">Follow these guidelines for any logo that you upload in the Cloud Partner portal:</span></span>

*   <span data-ttu-id="a0369-266">Azure tasarım basit renk paletini sahiptir.</span><span class="sxs-lookup"><span data-stu-id="a0369-266">The Azure design has a simple color palette.</span></span> <span data-ttu-id="a0369-267">Logonuzun ikincil renkleri ve birincil sayısını sınırlayın.</span><span class="sxs-lookup"><span data-stu-id="a0369-267">Limit the number of primary and secondary colors on your logo.</span></span>
*   <span data-ttu-id="a0369-268">Tema renkleri portalı beyaz ve siyah.</span><span class="sxs-lookup"><span data-stu-id="a0369-268">The theme colors of the portal are white and black.</span></span> <span data-ttu-id="a0369-269">Bu renkler arka plan rengi olarak logonuzun için kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="a0369-269">Don't use these colors as the background color for your logo.</span></span> <span data-ttu-id="a0369-270">Logonuzun portalında belirgin hale getirir bir renk kullanın.</span><span class="sxs-lookup"><span data-stu-id="a0369-270">Use a color that makes your logo prominent in the portal.</span></span> <span data-ttu-id="a0369-271">Basit birincil renkleri öneririz.</span><span class="sxs-lookup"><span data-stu-id="a0369-271">We recommend simple primary colors.</span></span> <span data-ttu-id="a0369-272">*Saydam arka plan kullanırsanız, logo ve metin beyaz, olduğundan emin olun siyah veya mavi.*</span><span class="sxs-lookup"><span data-stu-id="a0369-272">*If you use a transparent background, make sure that the logo and text aren't white, black, or blue.*</span></span>
*   <span data-ttu-id="a0369-273">Gradyan arka planı logosunu kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="a0369-273">Don't use a gradient background on the logo.</span></span>
*   <span data-ttu-id="a0369-274">Metin, logo, bile, şirket veya marka adı yerleştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="a0369-274">Don't place text on the logo, not even your company or brand name.</span></span> <span data-ttu-id="a0369-275">Logonuzun Görünüm ve yapısını düz ve gradyan olmaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a0369-275">The look and feel of your logo should be flat and avoid gradients.</span></span>
*   <span data-ttu-id="a0369-276">Logo uzatılmış olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="a0369-276">Make sure the logo isn't stretched.</span></span>

#### <a name="hero-logo"></a><span data-ttu-id="a0369-277">Kahramanı logosu</span><span class="sxs-lookup"><span data-stu-id="a0369-277">Hero logo</span></span>

<span data-ttu-id="a0369-278">Kahramanı logosu isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="a0369-278">The hero logo is optional.</span></span> <span data-ttu-id="a0369-279">Yayımcı kahramanı logosu yüklemek değil seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0369-279">The publisher can choose not to upload a hero logo.</span></span> <span data-ttu-id="a0369-280">Kahramanı simgesi yüklendikten sonra silinemez.</span><span class="sxs-lookup"><span data-stu-id="a0369-280">After the hero icon is uploaded, it can't be deleted.</span></span> <span data-ttu-id="a0369-281">O anda iş ortağı kahramanı simgeler Market yönergeleri izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a0369-281">At that time, the partner must follow the Marketplace guidelines for hero icons.</span></span>

<span data-ttu-id="a0369-282">Kahramanı logo simgesini için aşağıdaki yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="a0369-282">Follow these guidelines for the hero logo icon:</span></span>

*   <span data-ttu-id="a0369-283">Yayımcı görünen adı, planı başlık ve uzun Özet teklif beyaz görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a0369-283">The publisher display name, the plan title, and the offer long summary are displayed in white.</span></span> <span data-ttu-id="a0369-284">Bu nedenle, açık bir renk kahramanı simgesi arka plan için kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="a0369-284">Therefore, don't use a light color for the background of the hero icon.</span></span> <span data-ttu-id="a0369-285">Siyah, beyaz veya saydam arka plan kahramanı simgelerini izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="a0369-285">A black, white, or transparent background isn't allowed for hero icons.</span></span>
*   <span data-ttu-id="a0369-286">Teklif listelenen sonra yayımcı görüntüleme adı, planı başlık, uzun Özet teklif ve **oluşturma** düğmesi program aracılığıyla kahramanı logosunun içinde katıştırılmış.</span><span class="sxs-lookup"><span data-stu-id="a0369-286">After the offer is listed, the publisher display name, the plan title, the offer long summary, and the **Create** button are embedded programmatically inside the hero logo.</span></span> <span data-ttu-id="a0369-287">Sonuç olarak, kahramanı logosu tasarlarken herhangi bir metin girmeyin.</span><span class="sxs-lookup"><span data-stu-id="a0369-287">Consequently, don't enter any text while you design the hero logo.</span></span> <span data-ttu-id="a0369-288">Metni program aracılığıyla bu alana dahil olduğundan boş alanı sağ tarafta bırakın.</span><span class="sxs-lookup"><span data-stu-id="a0369-288">Leave empty space on the right because the text is included programmatically in that space.</span></span> <span data-ttu-id="a0369-289">Metin için boş alan sağdaki 415 x 100 piksel olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a0369-289">The empty space for the text should be 415 x 100 pixels on the right.</span></span> <span data-ttu-id="a0369-290">Soldan 370 piksel uzakta bulunur.</span><span class="sxs-lookup"><span data-stu-id="a0369-290">It's offset by 370 pixels from the left.</span></span>

    ![Kahramanı logosu örneği](./media/managed-application-author-marketplace/publishvm14.png)

## <a name="support-form"></a><span data-ttu-id="a0369-292">Form desteği</span><span class="sxs-lookup"><span data-stu-id="a0369-292">Support form</span></span>

<span data-ttu-id="a0369-293">Doldurmak **Destek** kişiler şirketinizden desteğiyle formu.</span><span class="sxs-lookup"><span data-stu-id="a0369-293">Fill out the **Support** form with support contacts from your company.</span></span> <span data-ttu-id="a0369-294">Bu bilgileri, kişiler ve müşteri destek ilgili kişisi mühendislik.</span><span class="sxs-lookup"><span data-stu-id="a0369-294">This information might be engineering contacts and customer support contacts.</span></span>

## <a name="publish-an-offer"></a><span data-ttu-id="a0369-295">Bir teklifi yayımlama</span><span class="sxs-lookup"><span data-stu-id="a0369-295">Publish an offer</span></span>

<span data-ttu-id="a0369-296">Tüm bölümleri doldurduktan sonra seçin **Yayımla** teklifiniz müşteriler için kullanılabilir hale getirir işlemini başlatmak üzere.</span><span class="sxs-lookup"><span data-stu-id="a0369-296">After you fill out all the sections, select **Publish** to start the process that makes your offer available to customers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0369-297">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a0369-297">Next steps</span></span>

* <span data-ttu-id="a0369-298">Yönetilen uygulamaların giriş için bkz: [yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a0369-298">For an introduction to managed applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="a0369-299">Marketten bir yönetilen uygulamayı kullanma hakkında daha fazla bilgi için bkz: [tüketen Azure Market uygulamalarda yönetilen](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="a0369-299">For information about consuming a managed application from the Marketplace, see [Consume Azure managed applications in the Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="a0369-300">Hizmet Kataloğu yönetilen uygulama yayımlama hakkında daha fazla bilgi için bkz: [oluşturma ve bir hizmet Kataloğu yönetilen uygulamayı yayımlayın](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="a0369-300">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="a0369-301">Hizmet Kataloğu yönetilen uygulama kullanma hakkında daha fazla bilgi için bkz: [bir hizmet Kataloğu yönetilen uygulama tüketen](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="a0369-301">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
