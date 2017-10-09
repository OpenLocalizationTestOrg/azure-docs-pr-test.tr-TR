---
title: "aaaUnderstand faturanızı Azure | Microsoft Docs"
description: "Bilgi nasıl tooread ve kullanım ve fatura Azure aboneliğiniz için anlama"
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.assetid: 32eea268-161c-4b93-8774-bc435d78a8c9
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/14/2017
ms.author: tonguyen
ms.openlocfilehash: a3195eb129b1576e8cb665aa6f88a1a2647edd78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-your-bill-for-microsoft-azure"></a>Microsoft Azure faturanızı anlama
toounderstand Azure fatura, faturanızı hello ayrıntılı günlük kullanım dosyasını ve yönetim raporları hello Azure portal'ın maliyet hello ile karşılaştırın.

tooobtain bir PDF, fatura ve ayrıntılı günlük kullanım dosya CSV karşıdan, bir kopyasını bkz [faturayı ve günlük kullanım verileri faturalama Azure alma](billing-download-azure-invoice-daily-usage-date.md). 

Ayrıntılı hüküm ve fatura ve ayrıntılı günlük kullanım dosya açıklamaları için bkz: [anlamak, Microsoft Azure fatura koşullarınızda](billing-understand-your-invoice.md) ve [anlayın koşulları, Microsoft Azure ile ilgili ayrıntılı kullanım](billing-understand-your-usage.md). 

Yönetim raporları maliyet hello hakkında daha fazla bilgi için bkz: [Azure portal maliyet Yönetim](https://docs.microsoft.com/en-us/azure/billing/billing-getting-started).


## <a name="charges"></a>My fatura hello ücretlere doğru olup olmadığını nasıl emin?
Daha fazla ayrıntı almak istediğiniz faturanızı üzerinde bir ücret ise, birkaç seçeneğiniz vardır.

### <a name="option-1-review-your-invoice-and-compare-hello-usage-and-costs-with-hello-detailed-usage-csv-file"></a>Seçenek 1: faturanızı gözden geçir ve hello kullanım ve maliyetleri ayrıntılı hello ile Karşılaştır kullanım CSV dosyası

Merhaba ayrıntılı kullanımı CSV dosyası ücretlerinizi fatura döneminin ve günlük kullanımı tarafından gösterir. ayrıntılı kullanımınızı CSV dosyası tooget bkz [faturayı ve günlük kullanım verileri faturalama Azure alma](https://docs.microsoft.com/en-us/azure/billing/billing-download-azure-invoice-daily-usage-date).

Kullanım ücretleri hello ölçer düzeyinde görüntülenir. Merhaba aşağıdaki terimler hem hello fatura aynı şeyi hello ayrıntılı kullanım dosyasını hello anlamına gelir. Örneğin, eşdeğer toohello fatura döneminde hello ayrıntılı kullanımı dosyasında gösterilen hello fatura döngüsünde faturalama hello olur.

 | Fatura (PDF) | Ayrıntılı kullanımı (CSV)|
 | --- | --- |
|Fatura döngüsü | Fatura Dönemi |
 |Ad |Ölçüm Kategorisi |
 |Tür |Ölçer alt kategorisi |
 |Kaynak |Ölçüm Adı |
 |Bölge |Ölçüm Bölgesi |
 |Kullanılan |Kullanılan Miktar |
 |Dahil |Dahil Edilen Miktar |
 |Faturalanabilir |Kapasite Aşım Miktarı |

Merhaba **kullanım ücretleri** faturanızı bölümünü fatura döneminde tüketilen her ölçüm için hello toplam değer içeriyor. Örneğin, hello aşağıdaki ekran görüntüsü hello Azure Zamanlayıcı hizmeti için bir kullanım ücret gösterir.

![Fatura kullanım ücretleri](./media/billing-understand-your-bill/1.png)

Merhaba **deyimi** bölüm aynı ücret gösterir, ayrıntılı kullanımı CSV hello. Her iki hello *tüketilen* tutar ve *değeri* eşleşme hello fatura.

![CSV kullanım ücretleri](./media/billing-understand-your-bill/2.png)

toosee bu Ücret günlük olarak, Git toohello dökümünü **günlük kullanımı** hello CSV bölümü. Altında "Zamanlayıcısı" filtre *ölçer kategori* hangi gün hello ölçer kullanıldı ve ne kadar tüketilen görebilirsiniz. Merhaba *kaynak* ve *kaynak grubu* bilgi karşılaştırma için de listelenir. Merhaba *tüketilen* değerleri eklemek toowhat 's hello fatura üzerinde gösterilen.

![Merhaba CSV günlük kullanım bölümünde](./media/billing-understand-your-bill/3.png)

tooget hello maliyeti günde Çarp hello *tüketilen* tutarlar hello ile *oranı* başlangıç değerinden **deyimi** bölümü.

toolearn hello fatura hakkında daha fazla bilgi görmek [Azure faturanızı anlamak](billing-understand-your-invoice.md).

toolearn her hello CSV, hello sütunların hakkında bkz [Azure ayrıntılı kullanımınızı anlamak](billing-understand-your-invoice.md).

### <a name="option-2-review-your-invoice-and-compare-with-hello-usage-and-costs-in-hello-azure-portal"></a>Seçenek 2: faturanızı gözden geçir ve hello kullanım ve maliyetleri de hello Azure portal ile Karşılaştır

Hello Azure portal Ayrıca, ücretlerinizi doğrulamanıza yardımcı olabilir. Hello Azure portal maliyet yönetim grafikleri kullanım ve hello ücretlerinizi faturanızı üzerinde hızlı bir genel bakış sağlar.

Yukarıda, hello örnekle toocontinue ziyaret hello [abonelikler sayfası](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade), aboneliğinizi seçin ve ardından **analiz maliyetiyle**. Buradan, hello zaman aralığı belirtin ve kullanım ücret hello Azure Zamanlayıcı hizmeti için bkz.

![Azure portalında maliyet analiz görünümü](./media/billing-understand-your-bill/4.png)

toosee hello günlük Maliyet dökümü içinde **geçmiş maliyet**, hello satıra tıklayın.

![Azure portalında maliyet geçmişini görüntüle](./media/billing-understand-your-bill/5.png)

toolearn daha, fazla [Azure faturalama ve maliyet yönetimi ile beklenmeyen maliyetleri önlemek](billing-getting-started.md#costs).

## <a name="external"></a>Dış servis ücretleri nasıldır?
Dış hizmetler (olarak da bilinen Azure Marketi siparişler) bağımsız hizmet satıcıları tarafından sağlanan ve ayrı olarak faturalandırılır. Merhaba ücretler Azure faturanızı gösterme. toolearn daha, fazla [, Azure dış hizmet ücretlerini anlama](billing-understand-your-azure-marketplace-charges.md).

## <a name="payment"></a>Ödeme nasıl sağlarım?

Ödeme yönteminiz olarak bir kredi kartı veya ATM kartı ayarlamak, hello ödeme hello fatura dönemi sona erdikten sonra otomatik olarak 10 gün içinde ücretlendirilir. Kredi kartı deyiminizde hello satır öğesi diyor **MSFT Azure**.

Varsa, [faturalama tarafından ödeme](billing-how-to-pay-by-invoice.md), ödeme toohello konumunuz faturanızı hello alt kısmında listelenen Gönder. Daha fazla yardım için [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

## <a name="how-do-i-check-hello-status-of-a-payment-made-by-credit-card"></a>Kredi kartı ile yapılan bir ödeme hello durumunu nasıl kontrol?

[Destek bileti oluşturma](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooask ödemenizi hello durumu için. 

## <a name="tips-for-cost-management"></a>Maliyet yönetimi için ipuçları
- Hello kullanarak maliyetleri tahmin [fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/pricing/calculator/) ve [toplam sahip olma hesaplayıcı maliyeti](https://aka.ms/azure-tco-calculator)ve hello [ayrıntılı fiyatlandırma bilgileri her hizmet için](https://azure.microsoft.com/en-us/pricing/).
- [Uyarıları faturalama yukarı ayarlamak](billing-set-up-alerts.md).
- [Kullanım ve düzenli olarak hello Azure portal maliyetlerini gözden](billing-getting-started.md#costs).

## <a name="need-help-contact-support"></a>Yardım mı gerekiyor? Desteğe başvurun.

Hala yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) sorunu Çözümlendi hızla tooget.
