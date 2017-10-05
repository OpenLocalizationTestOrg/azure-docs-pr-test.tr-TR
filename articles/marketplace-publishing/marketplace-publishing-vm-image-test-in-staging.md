---
title: "VM teklifiniz Market için test | Microsoft Docs"
description: "VM görüntüsü için Azure Marketi test etme anlayın."
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
ms.openlocfilehash: 26f856059b381be91b9cdd1f98a11dc90813c0c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="test-your-vm-offer-for-the-azure-marketplace-in-staging"></a><span data-ttu-id="f119f-103">VM teklifiniz için Azure Marketi hazırlamada test etme</span><span class="sxs-lookup"><span data-stu-id="f119f-103">Test your VM offer for the Azure Marketplace in staging</span></span>
<span data-ttu-id="f119f-104">Hazırlama, SKU özel ", test ve Market'te dağıtmadan önce işlevselliğini doğrulamak sandbox" dağıtma anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="f119f-104">Staging means deploying your SKU in a private “sandbox” where you can test and validate its functionality before deploying it to the Marketplace.</span></span> <span data-ttu-id="f119f-105">SKU dağıtmış olan bir müşteriye gibi hazırlama görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f119f-105">The SKU appears in staging just as it would to a customer who has deployed it.</span></span> <span data-ttu-id="f119f-106">VM görüntüsü için hazırlama edilmesini sertifikalı gerekir.</span><span class="sxs-lookup"><span data-stu-id="f119f-106">Your VM image must be certified to be pushed to staging.</span></span>

## <a name="step-1-push-your-offer-to-staging"></a><span data-ttu-id="f119f-107">1. adım: anında iletme teklifiniz için hazırlama</span><span class="sxs-lookup"><span data-stu-id="f119f-107">Step 1: Push your offer to staging</span></span>
1. <span data-ttu-id="f119f-108">Üzerinde **Yayımla** sekmesini tıklatın, **anında hazırlık**.</span><span class="sxs-lookup"><span data-stu-id="f119f-108">On the **Publish** tab, click **Push to Staging**.</span></span>
   
    ![Çizim](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. <span data-ttu-id="f119f-110">Yayımlama Portalı, tüm hataları bildirirse, bunları düzeltin.</span><span class="sxs-lookup"><span data-stu-id="f119f-110">If the Publishing Portal notifies you of any errors, correct them.</span></span>
3. <span data-ttu-id="f119f-111">İçinde **kimin hazırlanmış teklifiniz erişebilir?** iletişim kutusunda, kullanımınız teklifinize önizlemek için kullanacağınız Azure Aboneliklerin listesini girin [Azure Önizleme portalı](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f119f-111">In the **Who can access your staged offer?** dialog box, enter the list of Azure subscriptions that you will use to preview your offer in the [Azure preview portal](https://portal.azure.com).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f119f-112">Sanal makineler durumunda ve çözüm şablonları, lütfen **sağlamadığı** beyaz liste abonelikleri CSP, DreamSpark veya Open ile Azure türü.</span><span class="sxs-lookup"><span data-stu-id="f119f-112">In case of Virtual Machines and Solution templates, please **do not** whitelist subscriptions of type CSP, DreamSpark or Azure in Open.</span></span>
   > 
   > 

    > <span data-ttu-id="f119f-113">Düğmeyi tıkladığınızda, sanal makineleri durumunda **hazırlama anında**, aşağıdaki adımları Sahne gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="f119f-113">In case of Virtual Machines, when you click on the button **PUSH TO STAGING**, the following steps are performed behind the scene.</span></span> <span data-ttu-id="f119f-114">Yayımlama Yayımla sekmesi altında her adımı ilerlemesini görüntülemek kuramaz portal.</span><span class="sxs-lookup"><span data-stu-id="f119f-114">You will be able to view the progress of each step under the PUBLISH tab in the Publishing portal.</span></span> <span data-ttu-id="f119f-115">(Hazırlanmış durumu gösterilir) kadar bu sayfayı düzenli aralıklarla, uçtan düzeltmesi gereken tüm hata bilgileri için işaretlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f119f-115">You must check this page at regular interval (until the status shows STAGED) for any failure information which need correction from your end.</span></span>

    > - <span data-ttu-id="f119f-116">İlk bakışta hazırlama isteğiniz vhd doğrulamak sertifika takımın gider.</span><span class="sxs-lookup"><span data-stu-id="f119f-116">At first your staging request goes to the certification team who validate the vhd.</span></span> <span data-ttu-id="f119f-117">İsteğiniz değişiklik yalnızca pazarlama aldı, ancak sonra sertifika adım atlanır.</span><span class="sxs-lookup"><span data-stu-id="f119f-117">However, if your request has got only marketing change, then the certification step is skipped.</span></span>
    > - <span data-ttu-id="f119f-118">Sertifika tamamlandıktan sonra çoğaltma önerinin tüm Azure veri merkezi arasında başlatın.</span><span class="sxs-lookup"><span data-stu-id="f119f-118">Once the certification is complete, replication of the offer start across all the Azure datacenters.</span></span> <span data-ttu-id="f119f-119">Genellikle, 24-48hours çoğaltmanın tamamlanmasını alır ancak vhd öğesinin boyutuna bağlı olarak bir hafta sürebilir.</span><span class="sxs-lookup"><span data-stu-id="f119f-119">It generally takes 24-48hours for the replication to complete but may take up to a week depending on the size of the vhd.</span></span> <span data-ttu-id="f119f-120">İsteğiniz değişiklik yalnızca pazarlama aldı, ancak sonra çoğaltma daha hızlıdır.</span><span class="sxs-lookup"><span data-stu-id="f119f-120">However, if your request has got only marketing change, then the replication is faster.</span></span>
    > - <span data-ttu-id="f119f-121">Çoğaltma işlemi tamamlandıktan sonra teklif kullanılabilir olması [Azure portal](http:/portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f119f-121">When the replication is complete, then the offer will be available in the [Azure portal](http:/portal.azure.com).</span></span> <span data-ttu-id="f119f-122">Durum zaman at yayımlama HAZIRLANAN hale portal.</span><span class="sxs-lookup"><span data-stu-id="f119f-122">At that time the status become STAGED in the Publishing portal.</span></span> <span data-ttu-id="f119f-123">Aşamalı bir teklif görünür [Azure portal](http:/portal.azure.com) yalnızca ile teklif hazırlanan abonelikle ilişkili e-posta Kimlikleri'ni kullanarak.</span><span class="sxs-lookup"><span data-stu-id="f119f-123">A staged offer is visible in the [Azure portal](http:/portal.azure.com) only using the email id(s) associated with the subscription with which the offer is staged.</span></span>

1. <span data-ttu-id="f119f-124">Oturum [Azure Önizleme portalını](https://portal.azure.com) Azure aboneliklerini birini kullanarak, önceki adımda listelenen.</span><span class="sxs-lookup"><span data-stu-id="f119f-124">Sign in to the [Azure preview portal](https://portal.azure.com) by using one of the Azure subscriptions listed in the previous step.</span></span>
2. <span data-ttu-id="f119f-125">Teklifiniz bulun ve VM görüntü noktaları doğrula:</span><span class="sxs-lookup"><span data-stu-id="f119f-125">Find your offer and validate your VM image points:</span></span>
   
   * <span data-ttu-id="f119f-126">İçerik pazarlama doğru markette gösterildiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f119f-126">Make sure that marketing content shows up correctly in the Marketplace.</span></span>
   * <span data-ttu-id="f119f-127">VM görüntüsü uçtan uca dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="f119f-127">End-to-end deployment of the VM image.</span></span>
     
      ![img harita portalı](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> <span data-ttu-id="f119f-129">Teklifiniz Yayımlama Portalı aracılığıyla Microsoft'a bildirmeyi kadar hazırlama kalacak [**Yayımla** sekmesini > düğmesine tıklayın **"İsteği onayı için anında iletme için üretim"**] için göndermek hazır Üretim.</span><span class="sxs-lookup"><span data-stu-id="f119f-129">Your offer will remain in staging until you notify Microsoft via the Publishing Portal [**Publish** tab > click on the button **"Request Approval to Push to Production"**] that you are ready to push to production.</span></span> <span data-ttu-id="f119f-130">Bu, her şeyi listelenen giderek teklifiniz için hazırlık üzerinden takım onay tüm üyeleri için ideal bir zamandır.</span><span class="sxs-lookup"><span data-stu-id="f119f-130">This is an ideal time to have all members of your team check over everything in preparation for your offer going listed.</span></span>
> 
> <span data-ttu-id="f119f-131">Hazırlama platform yayımcı tarafından önizleme modunda teklif test etmek için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="f119f-131">The staging platform is designed for testing the offer in a preview mode by the publisher.</span></span> <span data-ttu-id="f119f-132">Bu platofrm commerical amaçlı kullanan önleyin.</span><span class="sxs-lookup"><span data-stu-id="f119f-132">We strongly discourage using this platofrm for commerical purposes.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f119f-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f119f-133">Next steps</span></span>
<span data-ttu-id="f119f-134">Artık, teklifiniz "hazırlanan" ve işlevselliğini test ettikten ve içerik pazarlama, son yayımlama aşamasına geçebilirsiniz **4. adım**: [teklifiniz Market'te dağıtma](marketplace-publishing-push-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="f119f-134">Now that your offer is "staged" and you have tested its functionality and marketing content, you can proceed to the final publishing phase, **Step 4**: [Deploying your offer to the Marketplace](marketplace-publishing-push-to-production.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="f119f-135">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="f119f-135">See also</span></span>
* [<span data-ttu-id="f119f-136">Başlarken: bir teklifi Azure Marketinde yayımlama</span><span class="sxs-lookup"><span data-stu-id="f119f-136">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

