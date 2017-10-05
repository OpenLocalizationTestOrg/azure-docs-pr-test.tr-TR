---
title: "Fatura ve günlük kullanım verileri faturalama Azure karşıdan | Microsoft Docs"
description: "İndirme veya, Azure fatura faturayı ve günlük kullanım verilerini görüntülemek açıklar."
keywords: "Fatura Fatura, fatura indirme, azure fatura, azure kullanımı"
services: 
documentationcenter: 
author: genlin
manager: tonguyen
editor: 
tags: billing
ms.assetid: 6d568d1d-3bd6-4348-97d0-1098b5fe0661
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: genli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c63d9523555f47b4e5c0f3766f3ba080f76ac19e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="download-or-view-your-azure-billing-invoice-and-daily-usage-data"></a><span data-ttu-id="047eb-104">İndirme veya Azure fatura faturayı ve günlük kullanım verilerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="047eb-104">Download or view your Azure billing invoice and daily usage data</span></span>
<span data-ttu-id="047eb-105">Faturanız dan indirebilirsiniz [Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) veya e-posta ile gönderilen sahip.</span><span class="sxs-lookup"><span data-stu-id="047eb-105">You can download your invoice from the [Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) or have it sent in email.</span></span> <span data-ttu-id="047eb-106">Günlük kullanımı indirmek için Git [Azure hesap Merkezi](https://account.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="047eb-106">To download your daily usage, go to the [Azure Account Center](https://account.windowsazure.com).</span></span> <span data-ttu-id="047eb-107">Yalnızca belirli rolleri fatura fatura ve kullanım bilgilerini, Hesap Yöneticisi gibi alma iznine sahip.</span><span class="sxs-lookup"><span data-stu-id="047eb-107">Only certain roles have permission to get billing invoice and usage information, like the Account Administrator.</span></span> <span data-ttu-id="047eb-108">Fatura bilgilere erişim sağlama hakkında daha fazla bilgi için bkz: [rollerini kullanarak faturalama Azure erişimi yönetme](billing-manage-access.md).</span><span class="sxs-lookup"><span data-stu-id="047eb-108">To learn more about getting access to billing information, see [Manage access to Azure billing using roles](billing-manage-access.md).</span></span>

## <a name="get-your-invoice-in-email-pdf"></a><span data-ttu-id="047eb-109">E-postayla (.pdf) faturanızı Al</span><span class="sxs-lookup"><span data-stu-id="047eb-109">Get your invoice in email (.pdf)</span></span>
<span data-ttu-id="047eb-110">Kabul ve Azure almak için ek alıcılar yapılandırma fatura bir e-posta.</span><span class="sxs-lookup"><span data-stu-id="047eb-110">You can opt in and configure additional recipients to receive your Azure invoice in an email.</span></span> <span data-ttu-id="047eb-111">Bu özellik için destek sunar, Kurumsal Anlaşma ya da Open ile Azure gibi belirli abonelikleri kullanılamayabilir.</span><span class="sxs-lookup"><span data-stu-id="047eb-111">This feature may not be available for certain subscriptions such as support offers, Enterprise Agreements, or Azure in Open.</span></span>

1. <span data-ttu-id="047eb-112">Aboneliğinizden seçin [abonelikleri dikey](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span><span class="sxs-lookup"><span data-stu-id="047eb-112">Select your subscription from the [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span></span> <span data-ttu-id="047eb-113">Sahip olduğunuz her abonelik için katılımı.</span><span class="sxs-lookup"><span data-stu-id="047eb-113">Opt-in for each subscription you own.</span></span> <span data-ttu-id="047eb-114">Tıklatın **faturalar** sonra **my fatura e-posta**.</span><span class="sxs-lookup"><span data-stu-id="047eb-114">Click **Invoices** then **Email my invoice**.</span></span> 

    ![Katılımı akışını gösteren ekran görüntüsü](./media/billing-download-azure-invoice-daily-usage-date/InvoicesDeepLink.PNG)
    
2. <span data-ttu-id="047eb-116">Tıklatın **kabul** ve koşulları kabul edin.</span><span class="sxs-lookup"><span data-stu-id="047eb-116">Click **Opt in** and accept the terms.</span></span>

    ![Katılımı akışını gösteren ekran görüntüsü](./media/billing-download-azure-invoice-daily-usage-date/InvoiceArticleStep2.PNG)
 
3. <span data-ttu-id="047eb-118">Anlaşmayı kabul ettiğiniz sonra ek alıcılar yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="047eb-118">Once you've accepted the agreement, you can configure additional recipients.</span></span>

    ![Katılımı akışını gösteren ekran görüntüsü](./media/billing-download-azure-invoice-daily-usage-date/InvoiceArticleStep3.PNG)
    
<span data-ttu-id="047eb-120">Bir e-posta adımları izledikten sonra alamazsanız e-posta adresinizi doğru olduğundan emin olun [iletişim tercihleri profilinizde](https://account.windowsazure.com/profile).</span><span class="sxs-lookup"><span data-stu-id="047eb-120">If you don't get an email after following the steps, make sure your email address is correct in the [communication preferences on your profile](https://account.windowsazure.com/profile).</span></span>

## <a name="download-invoice-from-azure-portal-pdf"></a><span data-ttu-id="047eb-121">Azure Portalı'ndan (.pdf) fatura indirin</span><span class="sxs-lookup"><span data-stu-id="047eb-121">Download invoice from Azure portal (.pdf)</span></span>

1. <span data-ttu-id="047eb-122">Aboneliğinizden seçin [abonelikleri dikey](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) olarak Azure Portalı'nda [faturalar erişimi olan bir kullanıcı](billing-manage-access.md).</span><span class="sxs-lookup"><span data-stu-id="047eb-122">Select your subscription from the [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal as [an user with access to invoices](billing-manage-access.md).</span></span>

2. <span data-ttu-id="047eb-123">Seçin **faturalar**.</span><span class="sxs-lookup"><span data-stu-id="047eb-123">Select **Invoices**.</span></span> 

    ![Faturalama ve kullanım seçeneği gösteren ekran görüntüsü](./media/billing-download-azure-invoice-daily-usage-date/billingandusage.png) 

3. <span data-ttu-id="047eb-125">Tıklatın **karşıdan fatura** PDF faturanızı kopyasını görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="047eb-125">Click **Download Invoice** to view a copy of your PDF invoice.</span></span> <span data-ttu-id="047eb-126">Bunu diyorsa **kullanılamaz**, bkz: [yok görmemin nedeni fatura son fatura dönemine ait?](#noinvoice)</span><span class="sxs-lookup"><span data-stu-id="047eb-126">If it says **Not available**, see [Why don't I see an invoice for the last billing period?](#noinvoice)</span></span>

    ![Fatura her dönem için fatura süreleri, yükleme seçeneği ve toplam ücretleri gösteren ekran görüntüsü](./media/billing-download-azure-invoice-daily-usage-date/billing4.png)

4. <span data-ttu-id="047eb-128">Günlük kullanımı fatura döneminde tıklayarak da görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="047eb-128">You can also view your daily usage by clicking the billing period.</span></span> 

<span data-ttu-id="047eb-129">Faturanız hakkında daha fazla bilgi için bkz: [faturanızı anlamak için Microsoft Azure](billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="047eb-129">For more information about your invoice, see [Understand your bill for Microsoft Azure](billing-understand-your-bill.md).</span></span> <span data-ttu-id="047eb-130">Maliyetleri yönetme hakkında Yardım için bkz: [Azure faturalama ve maliyet yönetimi ile beklenmeyen maliyetleri önlemek](billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="047eb-130">For help managing costs, see [Prevent unexpected costs with Azure billing and cost management](billing-getting-started.md).</span></span>

## <a name="download-usage-from-the-account-center-csv"></a><span data-ttu-id="047eb-131">Kullanım (.csv) hesap Merkezi'nden indirin</span><span class="sxs-lookup"><span data-stu-id="047eb-131">Download usage from the Account Center (.csv)</span></span>

1. <span data-ttu-id="047eb-132">Oturum [Azure hesap Merkezi](https://account.windowsazure.com/subscriptions) hesap yöneticisi olarak.</span><span class="sxs-lookup"><span data-stu-id="047eb-132">Sign into the [Azure Account Center](https://account.windowsazure.com/subscriptions) as the Account Administrator.</span></span>

2. <span data-ttu-id="047eb-133">Fatura ve kullanım bilgilerini istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="047eb-133">Select the subscription for which you want the invoice and usage information.</span></span>

3. <span data-ttu-id="047eb-134">Seçin **FATURALAMA GEÇMİŞİ**.</span><span class="sxs-lookup"><span data-stu-id="047eb-134">Select **BILLING HISTORY**.</span></span> 

    ![Fatura geçmişi seçeneğini gösteren ekran görüntüsü](./media/billing-download-azure-invoice-daily-usage-date/Billinghisotry.png)

4. <span data-ttu-id="047eb-136">Son altı fatura dönemi ve geçerli faturalanmamış dönemin, deyimleri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="047eb-136">You can see your statements for the last six billing periods and the current unbilled period.</span></span> 

    ![Fatura dönemleri, fatura ve günlük kullanımı ve toplam ücretleri her fatura dönemi için indirme seçeneklerini gösteren ekran görüntüsü](./media/billing-download-azure-invoice-daily-usage-date/billingSum.png)

5. <span data-ttu-id="047eb-138">Seçin **geçerli bildirimini görüntüle** tahmin oluşturulma zamanında ücretlerinizi tahmini görmek için.</span><span class="sxs-lookup"><span data-stu-id="047eb-138">Select **View Current Statement** to see an estimate of your charges at the time the estimate was generated.</span></span> <span data-ttu-id="047eb-139">Bu bilgiler yalnızca her gün güncelleştirilir ve tüm kullanımınızı içermeyebilir.</span><span class="sxs-lookup"><span data-stu-id="047eb-139">This information is only updated daily and may not include all your usage.</span></span> <span data-ttu-id="047eb-140">Aylık faturanızı bu tahmin farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="047eb-140">Your monthly invoice may differ from this estimate.</span></span>

    ![Geçerli bildirimini görüntüle seçeneğini gösteren ekran görüntüsü](./media/billing-download-azure-invoice-daily-usage-date/billingSum2.png)

    ![Geçerli ücretler tahmin gösteren ekran görüntüsü](./media/billing-download-azure-invoice-daily-usage-date/billingSum3.png)

6. <span data-ttu-id="047eb-143">Seçin **kullanımı indir** günlük kullanım verileri bir CSV dosyası olarak karşıdan yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="047eb-143">Select **Download Usage** to download the daily usage data as a CSV file.</span></span> <span data-ttu-id="047eb-144">Kullanılabilir iki sürümlerini görürseniz, sürüm 2 indirin.</span><span class="sxs-lookup"><span data-stu-id="047eb-144">If you see two versions available, download version 2.</span></span>

    ![Kullanımı indir seçeneğini gösteren ekran görüntüsü](./media/billing-download-azure-invoice-daily-usage-date/DLusage.png)

<span data-ttu-id="047eb-146">Yalnızca Hesap Yöneticisi Azure hesap merkezi erişebilir.</span><span class="sxs-lookup"><span data-stu-id="047eb-146">Only the Account Administrator can access the Azure Account Center.</span></span> <span data-ttu-id="047eb-147">Bir sahip gibi diğer faturalama yöneticileri kullanım bilgileri kullanarak elde edebilirsiniz [fatura API'leri](billing-usage-rate-card-overview.md).</span><span class="sxs-lookup"><span data-stu-id="047eb-147">Other billing admins, such as an Owner, can get usage information using the [Billing APIs](billing-usage-rate-card-overview.md).</span></span>

<span data-ttu-id="047eb-148">Günlük kullanımı hakkında daha fazla bilgi için bkz: [faturanızı anlamak için Microsoft Azure](billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="047eb-148">For more information about your daily usage, see [Understand your bill for Microsoft Azure](billing-understand-your-bill.md).</span></span> <span data-ttu-id="047eb-149">Maliyetleri yönetme hakkında Yardım için bkz: [Azure faturalama ve maliyet yönetimi ile beklenmeyen maliyetleri önlemek](billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="047eb-149">For help managing costs, see [Prevent unexpected costs with Azure billing and cost management](billing-getting-started.md).</span></span>

## <span data-ttu-id="047eb-150"><a name="noinvoice"></a>Son fatura dönemine ait bir fatura neden göremiyorum?</span><span class="sxs-lookup"><span data-stu-id="047eb-150"><a name="noinvoice"></a> Why don't I see an invoice for the last billing period?</span></span>

<span data-ttu-id="047eb-151">Fatura görmüyorum çeşitli nedenleri olabilir:</span><span class="sxs-lookup"><span data-stu-id="047eb-151">There could be several reasons that you don't see an invoice:</span></span>

- <span data-ttu-id="047eb-152">Aboneliğinizle aşan kaydetmedi aylık bir kredi tutarına sahip veya ücretsiz deneme sürümü vardır.</span><span class="sxs-lookup"><span data-stu-id="047eb-152">You have a monthly credit amount with your subscription that you didn't exceed or you have a Free Trial.</span></span> <span data-ttu-id="047eb-153">Para borçlu faturaya yalnızca oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="047eb-153">An invoice is only generated when you owe money.</span></span>

- <span data-ttu-id="047eb-154">30 günden kısa bir süre için Azure abone günden değil.</span><span class="sxs-lookup"><span data-stu-id="047eb-154">It's less than 30 days from the day you subscribed to Azure.</span></span>

- <span data-ttu-id="047eb-155">Fatura henüz oluşturulan değil.</span><span class="sxs-lookup"><span data-stu-id="047eb-155">The invoice isn't generated yet.</span></span> <span data-ttu-id="047eb-156">Fatura döneminin sonuna kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="047eb-156">Wait until the end of the billing period.</span></span>

- <span data-ttu-id="047eb-157">Hesap Yöneticisi değilseniz, eski faturalar avaialbe size olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="047eb-157">If you're not the Account Administrator, older invoices may not be avaialbe to you.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="047eb-158">Yardım mı gerekiyor?</span><span class="sxs-lookup"><span data-stu-id="047eb-158">Need help?</span></span> <span data-ttu-id="047eb-159">Desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="047eb-159">Contact support.</span></span>
<span data-ttu-id="047eb-160">Hala daha fazla, sorularınız varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) hızla çözümlenen sorunu almak için.</span><span class="sxs-lookup"><span data-stu-id="047eb-160">If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>

