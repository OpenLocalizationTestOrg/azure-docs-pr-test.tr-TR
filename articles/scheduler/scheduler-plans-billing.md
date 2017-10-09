---
title: "aaaPlans ve Azure Scheduler'ın faturalama"
description: "Planlar ve faturalama içinde Azure Zamanlayıcı"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 13a2be8c-dc14-46cc-ab7d-5075bfd4d724
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 051b8eeb1ea19678b3cef4db3237ebf04c8b0e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="plans-and-billing-in-azure-scheduler"></a>Planlar ve faturalama içinde Azure Zamanlayıcı
## <a name="job-collection-plans"></a>İş koleksiyonu planları
İş, Azure Scheduler Faturalanabilir varlık hello koleksiyonlarıdır. İş koleksiyonları ve aşağıda açıklanan üç planlarda – ücretsiz, standart ve Premium – gelen işleri sayısını içerir.

| **İş koleksiyonu planı** | **İşler iş koleksiyonu başına maksimum sayısı** | **En fazla yineleme** | **Abonelik başına en fazla iş koleksiyonları** | **Limitler** |
|:--- |:--- |:--- |:--- |:--- |
| **Boş** |İş koleksiyonu her 5 işleri |Saatte bir kez. İşlerini saatte bir kez daha sık yürütülemiyor |Bir abonelik too1 ücretsiz iş koleksiyonunu izin verilir |Kullanamazsınız [HTTP giden yetkilendirme nesnesi](scheduler-outbound-authentication.md) |
| **Standart** |İş koleksiyonu başına 50 işleri |Dakikada bir kez. İşlerini bir dakika daha sık yürütülemiyor |Bir abonelik too100 standart iş koleksiyonları izin verilir |Zamanlayıcı erişim toofull özellik kümesi |
| **P10 Premium** |İş koleksiyonu başına 50 işleri |Dakikada bir kez. İşlerini bir dakika daha sık yürütülemiyor |Bir abonelik too10, 000 P10 Premium iş koleksiyonları izin verilir. <a href="mailto:wapteams@microsoft.com">Bize Ulaşın</a> daha fazla bilgi için. |Zamanlayıcı erişim toofull özellik kümesi |
| **P20 Premium** |İş koleksiyonu başına 1000 işleri |Dakikada bir kez. İşlerini bir dakika daha sık yürütülemiyor |Bir abonelik too10, 000 P20 Premium iş koleksiyonları izin verilir. <a href="mailto:wapteams@microsoft.com">Bize Ulaşın</a> daha fazla bilgi için. |Zamanlayıcı erişim toofull özellik kümesi |

## <a name="upgrades-and-downgrades-of-job-collection-plans"></a>Yükseltmeleri ve Downgrades iş koleksiyonu planı
Yükseltme veya bir iş koleksiyonu planı dilediğiniz zaman hello ücretsiz, standart ve Premium planları arasında düşürmek. Ancak, tooa ücretsiz iş koleksiyonu eski sürüme düşürmeyi, hello indirgeme hello aşağıdaki nedenlerden birinden dolayı başarısız olabilir:

* Merhaba abonelikte bir ücretsiz iş koleksiyonu zaten var
* Merhaba iş koleksiyonu işinde ücretsiz iş koleksiyonlarındaki işleri için izin verilenden daha yüksek bir yinelenme içeriyor. saatte bir kez bir ücretsiz iş koleksiyonu izin hello en büyük yinelenme:
* Merhaba iş koleksiyonunda 5'ten fazla işleri vardır
* Bir işin hello iş koleksiyonundaki kullanan bir HTTP veya HTTPS eylemi var. bir [HTTP giden yetkilendirme nesnesi](scheduler-outbound-authentication.md)

## <a name="billing-and-azure-plans"></a>Faturalama ve Azure planları
Abonelikleri ücretsiz iş koleksiyonları ücretlendirilen değil. Daha iyi bir anlaşma toohave ise 100'den fazla standart iş koleksiyonları (10 standart fatura birimleri), varsa, tüm koleksiyonlar hello premium planında işi.

Bir standart iş koleksiyonu ve bir premium iş koleksiyonu varsa, faturalanan bir standart fatura birimi olan *ve* bir premium faturalandırma birimidir. Zamanlayıcı hizmeti faturaları Hello tooeither standart veya premium ayarlamak etkin iş koleksiyonları sayısına göre hello; Bu açıklanmıştır hello sonraki iki bölümde ilgili daha fazla.

## <a name="standard-billable-units"></a>Standart Faturalanabilir birimleri
Standart Faturalanabilir birim too10 standart iş koleksiyonlarını içerebilir. Standart iş koleksiyonu her bir iş koleksiyonu too50 işi yukarı sahip olduğundan, bir standart fatura birimi bir abonelik toohave too500 işleri kurma – tooalmost 22 milyon iş yürütmeleri aylık yedekleme sağlar.

1 ile 10 standart iş koleksiyonları arasında varsa, 1 standart Fatura birim için faturalandırılırsınız. 11-20 standart iş koleksiyonları arasında varsa, 2 standart fatura birimler için faturalandırılırsınız. 21 ve 30 standart iş koleksiyonları arasında varsa, 3 standart fatura birimler için faturalandırılırsınız ve benzeri.

## <a name="p10-premium-billable-units"></a>P10 Premium Faturalanabilir birimleri
P10 premium Faturalanabilir birim too10, 000 P10 premium iş koleksiyonları dahil edebilirsiniz. P10 premium iş koleksiyonu her bir iş koleksiyonu too50 işi yukarı sahip olduğundan, bir premium faturalama birimi bir abonelik toohave too500, 000 işleri kurma – tooalmost 22 milyar iş yürütmeleri aylık yedekleme sağlar.

1 ila 10.000 premium iş koleksiyonları arasında varsa, 1 P10 premium faturalama birim için faturalandırılırsınız. 10,001 ve 20.000 premium iş koleksiyonları arasında varsa, 2 P10 premium faturalama birimleri için faturalandırılırsınız ve benzeri.

Bu nedenle, P10 premium iş koleksiyonları sahip hello aynı işlevselliği durumda çok miktarda iş koleksiyonları uygulamanızın gerektirdiği hello standart iş koleksiyonları ancak bir fiyat sonu sağlayın.

## <a name="p20-premium-billable-units"></a>P20 Premium Faturalanabilir birimleri
P20 premium Faturalanabilir birim too5, 000 P20 premium iş koleksiyonları dahil edebilirsiniz. P20 premium iş koleksiyonu too1, her bir iş koleksiyonu 000 işi yukarı olabileceği için bir premium faturalama birimi abonelik toohave too5, 000 000 işleri – tooalmost 220 milyar iş yürütmeleri aylık yedekleme sağlar.

P20 premium iş koleksiyonları hello P10 premium iş koleksiyonları olarak aynı yetenekleri sunar, ancak her bir iş koleksiyonu ve bir büyük işlerin toplam sayısı genel P10 premium izin verme, toohave daha büyük bir sayı işi daha fazla ölçeklenebilirlik de destekler.

## <a name="billing-and-active-status"></a>Faturalama ve etkin durumu
Tüm aboneliğinizi toobilling sorunları nedeniyle bazı geçici devre dışı duruma geçti sürece iş koleksiyonları her zaman etkindir. Merhaba yalnızca iş koleksiyonu değil faturalandırılır yolu tooensure tooeither toohello ayarlanabilir olduğu *serbest* plan veya toodelete hello iş koleksiyonu.

Tek bir işlemde bir iş koleksiyonundaki tüm işleri devre dışı bırakabilir rağmen hello fatura hello iş koleksiyonu durumunu değiştirmez – hello iş koleksiyonu olacak *hala* faturalandırılacaksınız. Benzer şekilde, boş iş koleksiyonları etkin olarak kabul edilir ve Fatura edilecek.

## <a name="pricing"></a>Fiyatlandırma
Fiyatlandırma ayrıntıları için lütfen bkz [Zamanlayıcı fiyatlandırma](https://azure.microsoft.com/pricing/details/scheduler/).

## <a name="see-also"></a>Ayrıca Bkz.
 [Scheduler nedir?](scheduler-intro.md)

 [Azure Scheduler kavramları, terminolojisi ve varlık hiyerarşisi](scheduler-concepts-terms.md)

 [Zamanlayıcı hello Azure portalını kullanmaya başlama](scheduler-get-started-portal.md)

 [Azure Scheduler REST API başvurusu](https://msdn.microsoft.com/library/mt629143)

 [Azure Scheduler PowerShell cmdlet’leri başvurusu](scheduler-powershell-reference.md)

 [Yüksek Azure Scheduler kullanılabilirliği ve güvenilirliği](scheduler-high-availability-reliability.md)

 [Azure Scheduler sınırları, varsayılanları ve hata kodları](scheduler-limits-defaults-errors.md)

 [Azure Scheduler giden bağlantı kimlik doğrulaması](scheduler-outbound-authentication.md)

