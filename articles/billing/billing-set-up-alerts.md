---
title: "Azure abonelikleri için faturalama veya kredi uyarılar aaaSet | Microsoft Docs"
description: "Fatura beklenmeyen durumları kaçınmak için nasıl uyarılarını Azure faturanızda ayarlayabileceğiniz açıklar."
keywords: "Kredi uyarı, fatura Uyarısı"
services: 
documentationcenter: 
author: vikdesai
manager: tonguyen
editor: 
tags: billing
ms.assetid: 9b7b3eeb-cd9d-4690-86a3-51b1e2a8974f
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: vikdesai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 711b9c72c59874792b0e229cdc5ec0fa517c24c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a><span data-ttu-id="6374a-104">Microsoft Azure Abonelikleriniz için faturalama veya kredi uyarıları ayarlama</span><span class="sxs-lookup"><span data-stu-id="6374a-104">Set up billing or credit alerts for your Microsoft Azure subscriptions</span></span>
<span data-ttu-id="6374a-105">Bir Azure aboneliğine yönelik hello hesap yöneticisi değilseniz, hello Azure faturalama uyarı özelleştirilmiş toocreate faturalama izlemek ve fatura etkinlik, Azure hesaplarını yönetme yardımcı olacak uyarı hizmetini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6374a-105">If you’re hello Account Admin for an Azure subscription, you can use hello Azure Billing Alert Service toocreate customized billing alerts that help you monitor and manage billing activity for your Azure accounts.</span></span>

<span data-ttu-id="6374a-106">Tooenable gerekir böylece bu Önizleme'de, bu hello Önizleme özellikleri sayfasında ilk hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="6374a-106">This service is in preview, so you need tooenable it in hello Preview Features page first.</span></span>

## <a name="set-hello-alert-threshold-and-email-recipients"></a><span data-ttu-id="6374a-107">Merhaba uyarı eşiği ve e-posta alıcılarının ayarlama</span><span class="sxs-lookup"><span data-stu-id="6374a-107">Set hello alert threshold and email recipients</span></span>
1. <span data-ttu-id="6374a-108">Ziyaret [hello Önizleme özellikleri sayfasında](https://account.windowsazure.com/PreviewFeatures) ve etkinleştirme **faturalama uyarı hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="6374a-108">Visit [hello Preview Features page](https://account.windowsazure.com/PreviewFeatures) and enable **Billing Alert Service**.</span></span>

1. <span data-ttu-id="6374a-109">Aboneliğiniz için hello faturalama hizmeti açık hello e-posta onayı aldıktan sonra ziyaret [hello abonelikler sayfası](https://account.windowsazure.com/Subscriptions) hello hesap portalındaki.</span><span class="sxs-lookup"><span data-stu-id="6374a-109">After you receive hello email confirmation that hello billing service is turned on for your subscription, visit [hello Subscriptions page](https://account.windowsazure.com/Subscriptions) in hello account portal.</span></span> <span data-ttu-id="6374a-110">Toomonitor istediğiniz ve ardından hello aboneliğe tıklayın **uyarıları**.</span><span class="sxs-lookup"><span data-stu-id="6374a-110">Click hello subscription you want toomonitor, and then click **Alerts**.</span></span>

    ![Merhaba abonelikleri Azure hesap merkezi görünümünü ekran vurgulanmış uyarılar][Image1]

2. <span data-ttu-id="6374a-112">Bundan sonra öğesini **eklemek uyarı** toocreate, birinci.</span><span class="sxs-lookup"><span data-stu-id="6374a-112">Next, click **Add Alert** toocreate your first one.</span></span> <span data-ttu-id="6374a-113">Farklı bir eşik ile abonelik başına beş faturalama uyarılarını toplam yukarı ve tootwo e-posta alıcılarını her uyarı için ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6374a-113">You can set up a total of five billing alerts per subscription, with a different threshold and up tootwo email recipients for each alert.</span></span>

    ![Merhaba, uyarı ekleyebileceğiniz uyarılar görünümü ekran görüntüsü][Image2]

3. <span data-ttu-id="6374a-115">Bir uyarı eklediğinizde, harcama eşik seçin benzersiz bir ad verin ve hello uyarıları gönderildiği e-posta adresi seçin.</span><span class="sxs-lookup"><span data-stu-id="6374a-115">When you add an alert, you give it a unique name, choose a spending threshold, and choose hello email addresses where alerts are sent.</span></span> <span data-ttu-id="6374a-116">Merhaba eşiği ayarlarken ya da seçebilirsiniz bir **faturalama toplamı** veya **kredi** hello gelen **için uyarı** listesi.</span><span class="sxs-lookup"><span data-stu-id="6374a-116">When setting up hello threshold, you can choose either a **Billing Total** or a **Monetary Credit** from hello **Alert For** list.</span></span> <span data-ttu-id="6374a-117">Abonelik harcama hello eşiğini aştığında bir faturalama toplamı bir uyarı gönderilir.</span><span class="sxs-lookup"><span data-stu-id="6374a-117">For a billing total, an alert is sent when subscription spending exceeds hello threshold.</span></span> <span data-ttu-id="6374a-118">Parasal kredileriniz hello limitin altında bıraktığınızda kredi için bir uyarı gönderilir.</span><span class="sxs-lookup"><span data-stu-id="6374a-118">For a monetary credit, an alert is sent when monetary credits drop below hello limit.</span></span> <span data-ttu-id="6374a-119">Parasal kredileriniz genellikle tooFree deneme ve Visual Studio abonelikleri uygular.</span><span class="sxs-lookup"><span data-stu-id="6374a-119">Monetary credits usually apply tooFree Trial and Visual Studio subscriptions.</span></span>

    ![Alıcılar yapılandırabileceğiniz hello uyarı toplama görünümünün ekran görüntüsü][Image3]

<span data-ttu-id="6374a-121">Herhangi bir e-posta adresi Azure destekler ancak değil hello e-posta adresi çalıştığını doğrulamak, böylece yazım hataları denetleyin.</span><span class="sxs-lookup"><span data-stu-id="6374a-121">Azure supports any email address but doesn't verify that hello email address works, so double-check for typos.</span></span>

## <a name="check-on-your-alerts"></a><span data-ttu-id="6374a-122">Uyarılarınızı üzerinde denetleyin</span><span class="sxs-lookup"><span data-stu-id="6374a-122">Check on your alerts</span></span>
<span data-ttu-id="6374a-123">Uyarıları ayarlamak sonra hello hesap merkezi bunları listeler ve daha ayarlayabilirsiniz kaç gösterir.</span><span class="sxs-lookup"><span data-stu-id="6374a-123">After you set up alerts, hello Account Center lists them and shows how many more you can set up.</span></span> <span data-ttu-id="6374a-124">Her uyarı için hello tarih ve Saat Faturalama toplamı veya kredi için bir uyarı olup olmadığını gönderildiği ile ayarladığınız hello sınırı bakın.</span><span class="sxs-lookup"><span data-stu-id="6374a-124">For each alert, you see hello date and time it was sent, whether it’s an alert for Billing Total or Monetary Credit, and hello limit you set up.</span></span> <span data-ttu-id="6374a-125">Merhaba tarih ve saat biçimi 24 saat Evrensel Saat koordinatı'nı (UTC) ve hello tarih yyyy-aa-gg biçiminde.</span><span class="sxs-lookup"><span data-stu-id="6374a-125">hello date and time format is 24-hour Universal Time Coordinate (UTC) and hello date is yyyy-mm-dd format.</span></span> <span data-ttu-id="6374a-126">Merhaba artı oturum hello listesi tooedit bir uyarıyla ilgili onu veya hello çöp can toodelete tıklatın.</span><span class="sxs-lookup"><span data-stu-id="6374a-126">Click hello plus sign for an alert in hello list tooedit it, or click hello trash-can toodelete it.</span></span>

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="6374a-127">Kurumsal Anlaşma (Kurumsal Sözleşme) müşteriler için fatura uyarıları</span><span class="sxs-lookup"><span data-stu-id="6374a-127">Billing alerts for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="6374a-128">EA müşteriler, bir kayıt kotaları harcama ayarlayarak altında her bölüm için uyarıları alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6374a-128">EA customers can get alerts for each department under an enrollment by setting spending quotas.</span></span> <span data-ttu-id="6374a-129">Bkz: [departmanı harcama kotaları](https://ea.azure.com/helpdocs/departmentSpendingQuotas) hello EA portal tooget başlatılan içinde.</span><span class="sxs-lookup"><span data-stu-id="6374a-129">See [Department Spending Quotas](https://ea.azure.com/helpdocs/departmentSpendingQuotas) in hello EA portal tooget started.</span></span>

## <a name="learn-more-about-azure-cost-management"></a><span data-ttu-id="6374a-130">Azure maliyeti yönetimi hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="6374a-130">Learn more about Azure cost management</span></span>
- <span data-ttu-id="6374a-131">Hello kullanarak maliyetleri tahmin [fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/pricing/calculator/), [toplam sahip olma hesaplayıcı maliyeti](https://aka.ms/azure-tco-calculator), ve bir hizmet eklediğinizde.</span><span class="sxs-lookup"><span data-stu-id="6374a-131">Estimate costs using hello [pricing calculator](https://azure.microsoft.com/pricing/calculator/), [total cost of ownership calculator](https://aka.ms/azure-tco-calculator), and when you add a service.</span></span>
- <span data-ttu-id="6374a-132">[Kullanım ve maliyetler Azure portalında düzenli olarak gözden](billing-getting-started.md#costs).</span><span class="sxs-lookup"><span data-stu-id="6374a-132">[Review your usage and costs regularly in Azure portal](billing-getting-started.md#costs).</span></span>
- <span data-ttu-id="6374a-133">Aç [Azure Advisor önerileri maliyet](../advisor/advisor-cost-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="6374a-133">Turn on [Azure Advisor cost recommendations](../advisor/advisor-cost-recommendations.md).</span></span>

<span data-ttu-id="6374a-134">toolearn daha, fazla [Azure maliyeti Yönetim Kılavuzu](billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="6374a-134">toolearn more, see [Azure cost management guidance](billing-getting-started.md).</span></span>

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 
