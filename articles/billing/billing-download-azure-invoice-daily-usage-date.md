---
title: "Azure faturalama faturayı ve günlük kullanım verileri aaaDownload | Microsoft Docs"
description: "Azure faturalama toodownload veya görünüm nasıl fatura ve günlük kullanım verilerini açıklar."
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
ms.openlocfilehash: 2826df10f39914fcaeb9985271dadde550c68dfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="download-or-view-your-azure-billing-invoice-and-daily-usage-data"></a>İndirme veya Azure fatura faturayı ve günlük kullanım verilerini görüntüleme
Faturanız hello indirebilirsiniz [Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) veya e-posta ile gönderilen sahip. toodownload günlük kullanımı, Git toohello [Azure hesap Merkezi](https://account.windowsazure.com). Yalnızca belirli rolleri hello Hesap Yöneticisi gibi fatura ve kullanım bilgilerini Faturalama izni tooget sahiptir. erişim toobilling bilgi alma hakkında daha fazla toolearn bkz [rollerini kullanarak faturalama Yönet erişim tooAzure](billing-manage-access.md).

## <a name="get-your-invoice-in-email-pdf"></a>E-postayla (.pdf) faturanızı Al
Kabul ve Azure fatura ek alıcılar tooreceive bir e-posta ile yapılandırın. Bu özellik için destek sunar, Kurumsal Anlaşma ya da Open ile Azure gibi belirli abonelikleri kullanılamayabilir.

1. Hello aboneliğinizi seçin [abonelikleri dikey](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade). Sahip olduğunuz her abonelik için katılımı. Tıklatın **faturalar** sonra **my fatura e-posta**. 

    ![Merhaba katılımı akışını gösteren ekran görüntüsü](./media/billing-download-azure-invoice-daily-usage-date/InvoicesDeepLink.PNG)
    
2. Tıklatın **kabul** hello koşullarını ve kabul edin.

    ![Merhaba katılımı akışını gösteren ekran görüntüsü](./media/billing-download-azure-invoice-daily-usage-date/InvoiceArticleStep2.PNG)
 
3. Merhaba sözleşmesini kabul ettiğiniz sonra ek alıcılar yapılandırabilirsiniz.

    ![Merhaba katılımı akışını gösteren ekran görüntüsü](./media/billing-download-azure-invoice-daily-usage-date/InvoiceArticleStep3.PNG)
    
Bir e-posta hello adımları izledikten sonra alamazsanız e-posta adresinizi hello doğru olduğundan emin olun [iletişim tercihleri profilinizde](https://account.windowsazure.com/profile).

## <a name="download-invoice-from-azure-portal-pdf"></a>Azure Portalı'ndan (.pdf) fatura indirin

1. Hello aboneliğinizi seçin [abonelikleri dikey](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) olarak Azure Portalı'nda [erişim tooinvoices bir kullanıcıyla](billing-manage-access.md).

2. Seçin **faturalar**. 

    ![Merhaba faturalama & kullanım seçeneği gösteren ekran görüntüsü](./media/billing-download-azure-invoice-daily-usage-date/billingandusage.png) 

3. Tıklatın **karşıdan fatura** tooview PDF faturanızı bir kopyası. Bunu diyorsa **kullanılamaz**, bkz: [yok görmemin nedeni hello son fatura dönemi için fatura?](#noinvoice)

    ![Fatura her dönem için fatura süreleri, hello yükleme seçeneği ve toplam ücretleri gösteren ekran görüntüsü](./media/billing-download-azure-invoice-daily-usage-date/billing4.png)

4. Günlük kullanımı hello fatura döneminde tıklayarak da görüntüleyebilirsiniz. 

Faturanız hakkında daha fazla bilgi için bkz: [faturanızı anlamak için Microsoft Azure](billing-understand-your-bill.md). Maliyetleri yönetme hakkında Yardım için bkz: [Azure faturalama ve maliyet yönetimi ile beklenmeyen maliyetleri önlemek](billing-getting-started.md).

## <a name="download-usage-from-hello-account-center-csv"></a>Hesap Merkezi'nde (.csv) hello kullanım indirin

1. Merhaba içine oturum [Azure hesap Merkezi](https://account.windowsazure.com/subscriptions) Hesap Yöneticisi hello gibi.

2. Merhaba fatura ve kullanım bilgilerini istediğiniz hello aboneliği seçin.

3. Seçin **FATURALAMA GEÇMİŞİ**. 

    ![Fatura geçmişi seçeneğini gösteren ekran görüntüsü](./media/billing-download-azure-invoice-daily-usage-date/Billinghisotry.png)

4. Son altı fatura dönemi ve geçerli dönem faturalanmamış Merhaba, deyimleri hello için görebilirsiniz. 

    ![Fatura her dönem için fatura dönemleri, seçenekleri toodownload fatura ve günlük kullanımı ve toplam ücretleri gösteren ekran görüntüsü](./media/billing-download-azure-invoice-daily-usage-date/billingSum.png)

5. Seçin **geçerli bildirimini görüntüle** hello zaman hello tahmin, giderlerin tahmini üretilen toosee. Bu bilgiler yalnızca her gün güncelleştirilir ve tüm kullanımınızı içermeyebilir. Aylık faturanızı bu tahmin farklı olabilir.

    ![Merhaba geçerli bildirimini görüntüle seçeneğini gösteren ekran görüntüsü](./media/billing-download-azure-invoice-daily-usage-date/billingSum2.png)

    ![Geçerli ücretler hello tahmini gösteren ekran görüntüsü](./media/billing-download-azure-invoice-daily-usage-date/billingSum3.png)

6. Seçin **kullanımı indir** toodownload hello günlük kullanım verilerini bir CSV dosyası olarak. Kullanılabilir iki sürümlerini görürseniz, sürüm 2 indirin.

    ![Merhaba kullanımı indir seçeneğini gösteren ekran görüntüsü](./media/billing-download-azure-invoice-daily-usage-date/DLusage.png)

Yalnızca Hesap Yöneticisi hello hello Azure hesap merkezi erişebilir. Bir sahip gibi diğer faturalama yöneticileri hello kullanarak kullanım bilgilerini alabilir [fatura API'leri](billing-usage-rate-card-overview.md).

Günlük kullanımı hakkında daha fazla bilgi için bkz: [faturanızı anlamak için Microsoft Azure](billing-understand-your-bill.md). Maliyetleri yönetme hakkında Yardım için bkz: [Azure faturalama ve maliyet yönetimi ile beklenmeyen maliyetleri önlemek](billing-getting-started.md).

## <a name="noinvoice"></a>Merhaba son fatura dönemi için fatura neden göremiyorum?

Fatura görmüyorum çeşitli nedenleri olabilir:

- Aboneliğinizle aşan kaydetmedi aylık bir kredi tutarına sahip veya ücretsiz deneme sürümü vardır. Para borçlu faturaya yalnızca oluşturulur.

- 30 günden kısa bir süre hello günden tooAzure abone değil.

- Merhaba fatura henüz oluşturulan değil. Merhaba hello fatura döneminin sonuna kadar bekleyin.

- Merhaba hesap yöneticisi değilseniz, eski faturalar avaialbe tooyou olmayabilir.

## <a name="need-help-contact-support"></a>Yardım mı gerekiyor? Desteğe başvurun.
Hala daha fazla, sorularınız varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) sorunu Çözümlendi hızla tooget.

