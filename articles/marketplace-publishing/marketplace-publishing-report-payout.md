---
title: "Azure Market ödeme raporlama anlama | Microsoft Docs"
description: "Gözden geçirin ve Azure Marketi ödeme rapor alma hakkında bilgi edinin."
services: marketplace-publishing
documentationcenter: na
author: v-jeana
manager: lakoch
editor: 
ms.assetid: 3e99aefe-abeb-414c-8689-15352d25aefd
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: v-jeana; hascipio; v-dabosl
ms.openlocfilehash: 5a89e9ba4376d0c4f49feb3783692e28a28902a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="understand-your-azure-marketplace-payout-reports"></a><span data-ttu-id="97c3a-103">Azure Market ödeme raporlarınızı anlama</span><span class="sxs-lookup"><span data-stu-id="97c3a-103">Understand your Azure Marketplace payout reports</span></span>
## <a name="access-and-view-your-payout-reports"></a><span data-ttu-id="97c3a-104">Erişim ve ödeme raporlarınızı görüntüleme</span><span class="sxs-lookup"><span data-stu-id="97c3a-104">Access and view your payout reports</span></span>
<span data-ttu-id="97c3a-105">Biz geliştirme Merkezi'ne geçiş sırasında diğer hala yayımlama portalında https://publish.windowsazure.com bulunabilir ancak bazı ödeme raporlarınızı https://dev.windows.com/en-us geliştirme Merkezi'nde kullanılabilir olabilir.</span><span class="sxs-lookup"><span data-stu-id="97c3a-105">While we transition to Dev Center some of your payout reports may be available in the Dev Center at https://dev.windows.com/en-us while others may still be found in Publishing Portal at https://publish.windowsazure.com.</span></span>

<span data-ttu-id="97c3a-106">Ödeme raporlama şimdi kullanılabilir içinde **Dev Center** modern ödeme ile; ilişkili tüm Market sunumları için bu şu anda içerir:</span><span class="sxs-lookup"><span data-stu-id="97c3a-106">Payout reporting will now be available in **Dev Center** for any Marketplace offerings that are associated with modern payouts; this currently includes:</span></span>

* <span data-ttu-id="97c3a-107">VM'ler</span><span class="sxs-lookup"><span data-stu-id="97c3a-107">VMs</span></span>
* <span data-ttu-id="97c3a-108">B + C sunar</span><span class="sxs-lookup"><span data-stu-id="97c3a-108">B+C offers</span></span>
* <span data-ttu-id="97c3a-109">Veri ve geliştirici Hizmetleri EA altında sunulan</span><span class="sxs-lookup"><span data-stu-id="97c3a-109">Data and Dev Services offered under EA</span></span>

<span data-ttu-id="97c3a-110">Ödeme raporlama hala olacak **yayımlama portalında** için:</span><span class="sxs-lookup"><span data-stu-id="97c3a-110">Payout reporting will still be in **Publishing Portal** for:</span></span>

* <span data-ttu-id="97c3a-111">Veri ve geliştirici Hizmetleri Web (hala eski ödeme sistemi kullanır) doğrudan erişimli altında sunmuştur.</span><span class="sxs-lookup"><span data-stu-id="97c3a-111">Data and Dev Services offered under Web Direct (which still uses the legacy payout system).</span></span>

<span data-ttu-id="97c3a-112">Raporlar kullanılabilir 45 gün sonra Çeyreğin kapanışı ve sonra herhangi bir para iadesi hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="97c3a-112">Reports are available 45 days after the close of the quarter and are calculated after any refunds.</span></span>

### <a name="access-payout-reports-in-dev-center"></a><span data-ttu-id="97c3a-113">Geliştirme Merkezi'ndeki Access ödeme raporları</span><span class="sxs-lookup"><span data-stu-id="97c3a-113">Access payout reports in Dev Center</span></span>
1. <span data-ttu-id="97c3a-114">Https://dev.windows.com/en-us geliştirme Merkezi'ne gidin.</span><span class="sxs-lookup"><span data-stu-id="97c3a-114">Navigate to Dev Center at https://dev.windows.com/en-us.</span></span>
2. <span data-ttu-id="97c3a-115">Tıklatın **Pano**.</span><span class="sxs-lookup"><span data-stu-id="97c3a-115">Click **Dashboard**.</span></span>

    ![LandingPageDashboardHighlight][1]
3. <span data-ttu-id="97c3a-117">Tıklatın **ödeme özeti**.</span><span class="sxs-lookup"><span data-stu-id="97c3a-117">Click **Payout Summary**.</span></span>

    ![DashboardPayoutSummary][2]

## <a name="view-your-payout-reports-in-dev-center"></a><span data-ttu-id="97c3a-119">Geliştirme Merkezi'nde ödeme raporlarınızı görüntüleme</span><span class="sxs-lookup"><span data-stu-id="97c3a-119">View your payout reports in Dev Center</span></span>
<span data-ttu-id="97c3a-120">Ödeme rapor her üç aylık, üç ay içinde gerçekleşen tüm işlemleri kaydeder.</span><span class="sxs-lookup"><span data-stu-id="97c3a-120">The payout report for each quarter records all transactions that occurred within that quarter.</span></span>

* <span data-ttu-id="97c3a-121">Ayrılmış (örn. Bu miktar aşağıdaki aylık yaklaşan ödeme taşınır) yaklaşan ödeme döngüsü dışında tahakkuk ödemeler gösterir.</span><span class="sxs-lookup"><span data-stu-id="97c3a-121">The Reserved amount indicates any payments that are accruing outside of the upcoming payment cycle (e.g. this amount will move to upcoming payment the following month).</span></span>  <span data-ttu-id="97c3a-122">(İyi öncelikli bir müşteri ödeme sürece) bu miktar genellikle $0 olacaktır.</span><span class="sxs-lookup"><span data-stu-id="97c3a-122">This amount will typically be $0 (unless a customer pays well in advance).</span></span>
* <span data-ttu-id="97c3a-123">Yaklaşan ödeme ya da en son ödeme tıklatın **ayrıntıları görüntüleyin** bağlantılar bu ödeme hakkında nota bakın.</span><span class="sxs-lookup"><span data-stu-id="97c3a-123">Click on the Upcoming payment or Most recent payment **View details** links to see a note about those payouts.</span></span>
* <span data-ttu-id="97c3a-124">Tıklayın **ödeme deyimleri** uygulama/ürün kazançlar altında ayrıntılarını görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="97c3a-124">Click on **Payment Statements** to view the details under proceeds by app/product.</span></span>
* <span data-ttu-id="97c3a-125">Tıklayın **Görünüm** tek tek deyimleri görmek için bağlantı.</span><span class="sxs-lookup"><span data-stu-id="97c3a-125">Click on the **View** link to see individual statements.</span></span>

    ![PayoutSummaryUpcomingMostRecentLinksStatement][3]
* <span data-ttu-id="97c3a-127">Kullanım **geçer çözümleme** varsa bunlar birden çok apps/ürünleri görüntülemek için ayrı ayrı deyim ekranın alt kısmındaki filtre.</span><span class="sxs-lookup"><span data-stu-id="97c3a-127">Use the **Proceeds Breakdown** filter at the bottom of the individual statement to view multiple apps/products if they exist.</span></span>

    ![PayoutSummaryPaymentStatementsFilterControl][4]

## <a name="view-your-payout-reports-in-publishing-portal"></a><span data-ttu-id="97c3a-129">Yayımlama portalında ödeme raporlarınızı görüntüleme</span><span class="sxs-lookup"><span data-stu-id="97c3a-129">View your payout reports in Publishing Portal</span></span>
<span data-ttu-id="97c3a-130">Ödeme rapor her üç aylık, üç ay içinde gerçekleşen tüm işlemleri kaydeder.</span><span class="sxs-lookup"><span data-stu-id="97c3a-130">The payout report for each quarter records all transactions that occurred within that quarter.</span></span>

1. <span data-ttu-id="97c3a-131">Https://publish.windowsazure.com yayımlama portalında gidin.</span><span class="sxs-lookup"><span data-stu-id="97c3a-131">Navigate to the publishing portal at https://publish.windowsazure.com.</span></span>
2. <span data-ttu-id="97c3a-132">Gelen **yayımcılar** 'yi tıklatın **ödeme raporları**.</span><span class="sxs-lookup"><span data-stu-id="97c3a-132">From the **Publishers** section, click **Payout Reports**.</span></span>
3. <span data-ttu-id="97c3a-133">Tüm kullanılabilir üç aylık ödeme raporlarını görüntülemek için açılan'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="97c3a-133">Click the drop-down to display all available quarterly payout reports.</span></span>

    ![accessingpayoutreport][5]

### <a name="read-your-payout-reports"></a><span data-ttu-id="97c3a-135">Ödeme raporları okuma</span><span class="sxs-lookup"><span data-stu-id="97c3a-135">Read your payout reports</span></span>
<span data-ttu-id="97c3a-136">Ödeme rapor her üç aylık, üç ay içinde gerçekleşen tüm işlemleri kaydeder.</span><span class="sxs-lookup"><span data-stu-id="97c3a-136">The payout report for each quarter records all transactions that occurred within that quarter.</span></span>

* <span data-ttu-id="97c3a-137">Belirli bir üç aylık dönem için ilişkili girişleri arıyorsanız, aşağı açılan ilk o üç aylık dönem için ödeme raporu seçin.</span><span class="sxs-lookup"><span data-stu-id="97c3a-137">If you are looking for ledger entries that relate to a particular quarter, select the payout report for that quarter from the drop-down.</span></span> <span data-ttu-id="97c3a-138">Örneğin, Haziran 2015 Nisan için defter girişleri ilgileniyorsanız, o tarih aralığını açılan listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="97c3a-138">For example, if you are interested in ledger entries for April to June 2015, select that date range from the drop-down.</span></span>
* <span data-ttu-id="97c3a-139">Belirli bir üç aylık dönem için ilişkili ödeme ayrıntılarını arıyorsanız, sonraki üç aylık dönem için ödeme raporu seçin.</span><span class="sxs-lookup"><span data-stu-id="97c3a-139">If you are looking for details of payouts that relate to a particular quarter, select the payout report for the subsequent quarter.</span></span> <span data-ttu-id="97c3a-140">Haziran 2015 Nisan için ödeme ilgileniyorsanız, örneğin, bu miktarda sonraki ödeme raporu Eylül 2015 Temmuz için görünür.</span><span class="sxs-lookup"><span data-stu-id="97c3a-140">For example, if you are interested in the payouts for April to June 2015, these amounts will appear in the subsequent payout report for July to September 2015.</span></span>
  <span data-ttu-id="97c3a-141">![readingpayoutreport][6]</span><span class="sxs-lookup"><span data-stu-id="97c3a-141">![readingpayoutreport][6]</span></span>
* <span data-ttu-id="97c3a-142">Mali Özet panelini bakiyelerini, alacakları ve Borçları kategoriye göre gösterir.</span><span class="sxs-lookup"><span data-stu-id="97c3a-142">The financial summary panel shows balances, credits, and debits by category.</span></span>
* <span data-ttu-id="97c3a-143">Girişleri tek tek işlemleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="97c3a-143">Ledger entries show individual transactions.</span></span>

## <a name="definitions"></a><span data-ttu-id="97c3a-144">Tanımlar</span><span class="sxs-lookup"><span data-stu-id="97c3a-144">Definitions</span></span>
<span data-ttu-id="97c3a-145">**Mali Özet panelini:**</span><span class="sxs-lookup"><span data-stu-id="97c3a-145">**Financial summary panel:**</span></span>

![financialdefinitions][7]

<span data-ttu-id="97c3a-147">**Girişleri:**</span><span class="sxs-lookup"><span data-stu-id="97c3a-147">**Ledger entries:**</span></span>

![ledgerdefinitions][8]

## <a name="payout-questions"></a><span data-ttu-id="97c3a-149">Ödeme sorular</span><span class="sxs-lookup"><span data-stu-id="97c3a-149">Payout questions</span></span>
<span data-ttu-id="97c3a-150">Ödeme ilgili bir sorunuz varsa, bizim Destek ekibine başvurun.</span><span class="sxs-lookup"><span data-stu-id="97c3a-150">If you have a question related to your payouts, contact our support team.</span></span>

![payoutquestions][9]

1. <span data-ttu-id="97c3a-152">Destek sayfalara gidin.</span><span class="sxs-lookup"><span data-stu-id="97c3a-152">Navigate to the support pages.</span></span>
2. <span data-ttu-id="97c3a-153">Seçin **ödeme**.</span><span class="sxs-lookup"><span data-stu-id="97c3a-153">Select **Payouts**.</span></span>
3. <span data-ttu-id="97c3a-154">Seçin **ödeme ilgili sorgular**.</span><span class="sxs-lookup"><span data-stu-id="97c3a-154">Select **Payout related inquiries**.</span></span>
4. <span data-ttu-id="97c3a-155">Tıklatın **başlatma isteği**.</span><span class="sxs-lookup"><span data-stu-id="97c3a-155">Click **Start request**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97c3a-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="97c3a-156">Next steps</span></span>
<span data-ttu-id="97c3a-157">Diğer destek sorgular için lütfen bir sorununu oturum <https://portal.azure.com>.</span><span class="sxs-lookup"><span data-stu-id="97c3a-157">For other support queries, please log an issue at <https://portal.azure.com>.</span></span>

[1]: ./media/marketplace-publishing-report-payout/LandingPage-DashboardHighlight.png
[2]: ./media/marketplace-publishing-report-payout/Dashboard-PayoutSummary.png
[3]: ./media/marketplace-publishing-report-payout/PayoutSummary-UpcomingOrMostRecentPaymentLinksSingleStatementLink.png
[4]: ./media/marketplace-publishing-report-payout/PayoutSummary-PaymentStatements-SingleStatement-FilterControl.png
[5]: ./media/marketplace-publishing-report-payout/accessingpayoutreport.png
[6]: ./media/marketplace-publishing-report-payout/readingpayoutreport.png
[7]: ./media/marketplace-publishing-report-payout/financialdefinitions.png
[8]: ./media/marketplace-publishing-report-payout/ledgerdefinitions.png
[9]: ./media/marketplace-publishing-report-payout/payoutquestions.png
