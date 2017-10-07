---
title: VM Merhaba Market teklifi aaaTest | Microsoft Docs
description: "Nasıl tootest VM görüntü hello Azure Marketi anlayın."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 7a41c3c6-625c-4478-b804-e124dee89040
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: hascipio
ms.openlocfilehash: ab166d2c3c536810a3a8f48330f0482b9b4e58d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="test-your-vm-offer-for-hello-azure-marketplace-in-staging"></a><span data-ttu-id="457d3-103">VM teklifiniz hello Azure Marketi için hazırlamada test etme</span><span class="sxs-lookup"><span data-stu-id="457d3-103">Test your VM offer for hello Azure Marketplace in staging</span></span>
<span data-ttu-id="457d3-104">Hazırlama, SKU özel ", test ve toohello Market dağıtmadan önce işlevselliğini doğrulamak sandbox" dağıtma anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="457d3-104">Staging means deploying your SKU in a private “sandbox” where you can test and validate its functionality before deploying it toohello Marketplace.</span></span> <span data-ttu-id="457d3-105">Merhaba SKU dağıtmış olan tooa müşteri gibi hazırlama görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="457d3-105">hello SKU appears in staging just as it would tooa customer who has deployed it.</span></span> <span data-ttu-id="457d3-106">VM görüntüsü gönderilen sertifikalı toobe toostaging olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="457d3-106">Your VM image must be certified toobe pushed toostaging.</span></span>

## <a name="step-1-push-your-offer-toostaging"></a><span data-ttu-id="457d3-107">1. adım: Teklif toostaging bildirme</span><span class="sxs-lookup"><span data-stu-id="457d3-107">Step 1: Push your offer toostaging</span></span>
1. <span data-ttu-id="457d3-108">Merhaba üzerinde **Yayımla** sekmesini tıklatın, **anında tooStaging**.</span><span class="sxs-lookup"><span data-stu-id="457d3-108">On hello **Publish** tab, click **Push tooStaging**.</span></span>
   
    ![Çizim](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. <span data-ttu-id="457d3-110">Merhaba yayımlama portalında size herhangi bir hata bildirirse, bunları düzeltin.</span><span class="sxs-lookup"><span data-stu-id="457d3-110">If hello Publishing Portal notifies you of any errors, correct them.</span></span>
3. <span data-ttu-id="457d3-111">Merhaba, **kimin hazırlanmış teklifiniz erişebilir?** iletişim kutusunda, Azure abonelikleri toopreview hello teklifiniz kullanacağı hello listesini girin [Azure Önizleme portalı](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="457d3-111">In hello **Who can access your staged offer?** dialog box, enter hello list of Azure subscriptions that you will use toopreview your offer in hello [Azure preview portal](https://portal.azure.com).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="457d3-112">Sanal makineler durumunda ve çözüm şablonları, lütfen **sağlamadığı** beyaz liste abonelikleri CSP, DreamSpark veya Open ile Azure türü.</span><span class="sxs-lookup"><span data-stu-id="457d3-112">In case of Virtual Machines and Solution templates, please **do not** whitelist subscriptions of type CSP, DreamSpark or Azure in Open.</span></span>
   > 
   > 

    > <span data-ttu-id="457d3-113">Merhaba düğmesini tıklattığınızda, sanal makineleri durumunda **İTME tooSTAGING**, aşağıdaki adımları hello hello Sahne gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="457d3-113">In case of Virtual Machines, when you click on hello button **PUSH tooSTAGING**, hello following steps are performed behind hello scene.</span></span> <span data-ttu-id="457d3-114">Her bir adımın hello yayımlama hello sekmede altında mümkün tooview hello ilerleme olacaktır portalını yayımlama.</span><span class="sxs-lookup"><span data-stu-id="457d3-114">You will be able tooview hello progress of each step under hello PUBLISH tab in hello Publishing portal.</span></span> <span data-ttu-id="457d3-115">(Hazırlanmış hello durumu gösterilir) kadar bu sayfayı düzenli aralıklarla, uçtan düzeltmesi gereken tüm hata bilgileri için işaretlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="457d3-115">You must check this page at regular interval (until hello status shows STAGED) for any failure information which need correction from your end.</span></span>

    > - <span data-ttu-id="457d3-116">İlk bakışta hazırlama isteğiniz hello vhd doğrulamak toohello sertifika takımın gider.</span><span class="sxs-lookup"><span data-stu-id="457d3-116">At first your staging request goes toohello certification team who validate hello vhd.</span></span> <span data-ttu-id="457d3-117">İsteğiniz değişiklik yalnızca pazarlama aldı, ancak ardından hello sertifika adım atlanır.</span><span class="sxs-lookup"><span data-stu-id="457d3-117">However, if your request has got only marketing change, then hello certification step is skipped.</span></span>
    > - <span data-ttu-id="457d3-118">Merhaba sertifika tamamlandıktan sonra tüm hello Teklif başlangıç çoğaltmasını Azure veri merkezleri hello.</span><span class="sxs-lookup"><span data-stu-id="457d3-118">Once hello certification is complete, replication of hello offer start across all hello Azure datacenters.</span></span> <span data-ttu-id="457d3-119">Genellikle, 24-48hours hello çoğaltma toocomplete için alır ancak tooa hafta hello vhd hello boyutuna bağlı olarak yukarı sürebilir.</span><span class="sxs-lookup"><span data-stu-id="457d3-119">It generally takes 24-48hours for hello replication toocomplete but may take up tooa week depending on hello size of hello vhd.</span></span> <span data-ttu-id="457d3-120">İsteğiniz değişiklik yalnızca pazarlama aldı, ancak ardından hello çoğaltma daha hızlıdır.</span><span class="sxs-lookup"><span data-stu-id="457d3-120">However, if your request has got only marketing change, then hello replication is faster.</span></span>
    > - <span data-ttu-id="457d3-121">Hello çoğaltma işlemi tamamlandıktan sonra hello teklif hello kullanılabilecek [Azure portal](http:/portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="457d3-121">When hello replication is complete, then hello offer will be available in hello [Azure portal](http:/portal.azure.com).</span></span> <span data-ttu-id="457d3-122">O zaman hello durum hale HAZIRLANAN hello portalını yayımlama.</span><span class="sxs-lookup"><span data-stu-id="457d3-122">At that time hello status become STAGED in hello Publishing portal.</span></span> <span data-ttu-id="457d3-123">Aşamalı bir teklif hello görülebilir [Azure portal](http:/portal.azure.com) yalnızca teklif ile hangi hello hazırlanan hello abonelikle ilişkili hello e-posta Kimlikleri'ni kullanarak.</span><span class="sxs-lookup"><span data-stu-id="457d3-123">A staged offer is visible in hello [Azure portal](http:/portal.azure.com) only using hello email id(s) associated with hello subscription with which hello offer is staged.</span></span>

1. <span data-ttu-id="457d3-124">İçinde toohello oturum [Azure Önizleme portalını](https://portal.azure.com) hello birini kullanarak Azure abonelikleri listelenen hello önceki adımda.</span><span class="sxs-lookup"><span data-stu-id="457d3-124">Sign in toohello [Azure preview portal](https://portal.azure.com) by using one of hello Azure subscriptions listed in hello previous step.</span></span>
2. <span data-ttu-id="457d3-125">Teklifiniz bulun ve VM görüntü noktaları doğrula:</span><span class="sxs-lookup"><span data-stu-id="457d3-125">Find your offer and validate your VM image points:</span></span>
   
   * <span data-ttu-id="457d3-126">İçerik pazarlama doğru hello Market gösterildiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="457d3-126">Make sure that marketing content shows up correctly in hello Marketplace.</span></span>
   * <span data-ttu-id="457d3-127">Merhaba VM görüntüsü uçtan uca dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="457d3-127">End-to-end deployment of hello VM image.</span></span>
     
      ![img harita portalı](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> <span data-ttu-id="457d3-129">Teklifiniz hello Yayımlama Portalı Microsoft'a bildirmeyi kadar hazırlama kalacak [**Yayımla** sekmesini > merhaba düğmesine tıklayın **"onay tooPush tooProduction istek"**] hazır toopush olduğunu tooproduction.</span><span class="sxs-lookup"><span data-stu-id="457d3-129">Your offer will remain in staging until you notify Microsoft via hello Publishing Portal [**Publish** tab > click on hello button **"Request Approval tooPush tooProduction"**] that you are ready toopush tooproduction.</span></span> <span data-ttu-id="457d3-130">Her şeyi listelenen giderek teklifiniz için hazırlık üzerinden tüm ekibinizin üyeleri denetleyin ideal zaman toohave budur.</span><span class="sxs-lookup"><span data-stu-id="457d3-130">This is an ideal time toohave all members of your team check over everything in preparation for your offer going listed.</span></span>
> 
> <span data-ttu-id="457d3-131">Platform hazırlama hello hello yayımcı tarafından önizleme modunda test hello teklif için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="457d3-131">hello staging platform is designed for testing hello offer in a preview mode by hello publisher.</span></span> <span data-ttu-id="457d3-132">Bu platofrm commerical amaçlı kullanan önleyin.</span><span class="sxs-lookup"><span data-stu-id="457d3-132">We strongly discourage using this platofrm for commerical purposes.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="457d3-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="457d3-133">Next steps</span></span>
<span data-ttu-id="457d3-134">Teklifiniz "hazırlanan" ve işlevselliği ve içeriği pazarlama test göre toohello son yayımlama geçebilmeniz aşaması, **4. adım**: [, teklif toohello Market dağıtma](marketplace-publishing-push-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="457d3-134">Now that your offer is "staged" and you have tested its functionality and marketing content, you can proceed toohello final publishing phase, **Step 4**: [Deploying your offer toohello Marketplace](marketplace-publishing-push-to-production.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="457d3-135">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="457d3-135">See also</span></span>
* [<span data-ttu-id="457d3-136">Başlarken: nasıl toopublish bir teklif toohello Azure Market</span><span class="sxs-lookup"><span data-stu-id="457d3-136">Getting started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

