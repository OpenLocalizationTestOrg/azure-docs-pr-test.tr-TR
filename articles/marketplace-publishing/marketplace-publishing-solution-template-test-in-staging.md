---
title: "Çözüm şablonu teklifiniz Market için test etme | Microsoft Docs"
description: "Çözüm şablonu teklifiniz Azure Marketi için test etme anlayın."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: ef8f9b5e-b98c-49f3-913f-cdf772c14c12
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/04/2015
ms.author: hascipio; v-divte
ms.openlocfilehash: da1fc4713fd1d832c7ba91226f72cbef63b241bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="test-your-solution-template-offer-in-staging"></a><span data-ttu-id="ef91f-103">Çözüm şablonu teklifiniz hazırlamada test etme</span><span class="sxs-lookup"><span data-stu-id="ef91f-103">Test your solution template offer in staging</span></span>
<span data-ttu-id="ef91f-104">Hazırlama teklifiniz özel ", test ve üretim göndermeden önce işlevselliğini doğrulayın sandbox" dağıtma anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="ef91f-104">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it to production.</span></span> <span data-ttu-id="ef91f-105">Teklif hazırlama dağıtmış olan bir müşteriye gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="ef91f-105">The offer appears in staging just as it would to a customer who has deployed it.</span></span> <span data-ttu-id="ef91f-106">Teklifiniz için hazırlama edilmesini sertifikalı gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef91f-106">Your offer must be certified to be pushed to staging.</span></span>

<span data-ttu-id="ef91f-107">Teklif hazırlanan sonra görüntülemek ve teklif test [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ef91f-107">After the offer is staged, you can view and test the offer in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="ef91f-108">Teklifiniz hazırlama için anında ve bunu test etmek için aşağıdaki adımları izleyin [Azure Portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="ef91f-108">Follow the steps below to push your offer to staging and test it in the [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="ef91f-109">Git [yayımlama portalında](https://publish.windowsazure.com) > **çözüm şablonları** sekmesini > teklifiniz > **Yayımla** > **anındahazırlama**.</span><span class="sxs-lookup"><span data-stu-id="ef91f-109">Go to the [Publishing Portal](https://publish.windowsazure.com) > **Solution Templates** tab > your offer > **Publish** > **Push to Staging**.</span></span>
2. <span data-ttu-id="ef91f-110">Önizleme ve teklifiniz test etmek için kullanacağınız Azure abonelikleri listesini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="ef91f-110">Provide the list of Azure subscriptions that you will use to preview and test your offer.</span></span>
3. <span data-ttu-id="ef91f-111">Önceki adımda kullanılan abonelik kimliği'ni kullanarak Azure Önizleme portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ef91f-111">Sign in to the Azure preview portal by using the subscription ID that you used in the previous step.</span></span>
4. <span data-ttu-id="ef91f-112">Aşağıda adı geçen noktalarında Azure Önizleme portalında sınama en az bir gidiş gerçekleştiremeyen:</span><span class="sxs-lookup"><span data-stu-id="ef91f-112">Carry out at least one round of testing in the Azure preview portal on the points mentioned below:</span></span>
   * <span data-ttu-id="ef91f-113">İçerik pazarlama doğru Azure Marketi'nde gösterildiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="ef91f-113">Make sure that marketing content shows up correctly in the Azure Marketplace.</span></span>
   * <span data-ttu-id="ef91f-114">Uçtan uca dağıtım topolojisinin.</span><span class="sxs-lookup"><span data-stu-id="ef91f-114">End-to-end deployment of the topology.</span></span>
   * <span data-ttu-id="ef91f-115">Performans testi ve stres testi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="ef91f-115">Perform performance testing and stress testing.</span></span>
   * <span data-ttu-id="ef91f-116">Topolojiniz için en iyi yöntemleri uyduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ef91f-116">Ensure that your topology adheres to the best practices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef91f-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ef91f-117">Next steps</span></span>
<span data-ttu-id="ef91f-118">Sonuçlardan memnun sonra son teklif yayımlama aşamasına geçebilirsiniz **4. adım**: [teklifiniz Market'te dağıtma](marketplace-publishing-push-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="ef91f-118">If you are satisfied with the results, then you can proceed to the final offer publishing phase, **Step 4**:  [Deploying your offer to the Marketplace](marketplace-publishing-push-to-production.md).</span></span> <span data-ttu-id="ef91f-119">Aksi takdirde, Teklifte değişiklik ve yeniden sertifika isteyin.</span><span class="sxs-lookup"><span data-stu-id="ef91f-119">Otherwise, make changes in your offer and request certification again.</span></span>

> [!NOTE]
> <span data-ttu-id="ef91f-120">Pazarlama içeriği değişiklikleri için sertifika gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="ef91f-120">For marketing content changes, certification is not required.</span></span>
> 
> 

<span data-ttu-id="ef91f-121">Bkz: [Başlarken: bir teklifi Azure Marketinde yayımlama](marketplace-publishing-getting-started.md) Kılavuzu tüm yayımcı görevleri için.</span><span class="sxs-lookup"><span data-stu-id="ef91f-121">See [Getting started: How to publish an offer to the Azure Marketplace](marketplace-publishing-getting-started.md) for a guide to all publisher tasks.</span></span>

