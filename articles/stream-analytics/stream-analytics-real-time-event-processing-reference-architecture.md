---
title: "Stream Analytics olay işleme ile işleme aaaReal zamanı olay | Microsoft Docs"
description: "Gerçek zamanlı Olay işleme ve analizi etkinleştirmek için Azure Hizmetleri kümesi nasıl çalışabilirler öğrenin."
keywords: "gerçek zamanlı işleme, olay işleme, referans mimarisi"
services: stream-analytics,event-hubs,storage,sql-database
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: 
ms.assetid: 11af48bc-313c-4527-8c80-91088dc9f3c6
ms.service: stream-analytics
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: jeffstok
ms.openlocfilehash: a43c503d709609ba61e9932822d30bc2208906ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a>Başvuru mimarisi: Gerçek zamanlı Olay Microsoft Azure akış Analizi ile işleme
gerçek zamanlı Olay Azure akış Analizi ile işleme için Hello başvuru mimarisi hedeflenen tooprovide gerçek zamanlı bir platform Microsoft Azure ile hizmet (PaaS) akış işleme çözümü olarak dağıtmak için genel Şeması ' dir.

## <a name="summary"></a>Özet
Geleneksel olarak, analiz çözümleri yeteneklerine ETL (ayıklama, dönüştürme ve yükleme) ve veri ambarı, gibi veri depolanan önceki tooanalysis nerede dayalı. Daha fazla hızlı bir şekilde gelen veriler dahil değişen gereksinimleri, bu varolan modeli toohello sınırı zorlayan. Yeni bir özellik olmamasına karşın, hello yaklaşım yaygın tüm endüstri verticals benimsemiştir değil ve Hello özelliği tooanalyze veri taşıma akışları önceki toostorage içinde bir çözümüdür. 

Microsoft Azure bir dizi farklı çözüm senaryoları ve gereksinimleri destekleyebildiğini analytics teknolojilerin kapsamlı bir katalog sağlar. Hangi Azure Hizmetleri toodeploy uçtan uca çözümü teklifleri hello derecesini verilen zor olabilir seçme. Bu yazı tasarlanmış toodescribe hello özellikleri olduğunu ve birlikte çalışabilirlik, hello olay akışı çözümünü destekleyen çeşitli Azure Hizmetleri. Ayrıca müşteriler bu yaklaşım türünden yararlanabilir hello senaryolardan bazıları açıklanmaktadır.

## <a name="contents"></a>İçindekiler
* Yönetici Özeti
* Giriş tooReal zamanı analizi
* Değer teklifinde Azure gerçek zamanlı veri
* Gerçek zamanlı analiz için ortak senaryolar
* Mimarisi ve bileşenleri
  * Veri Kaynakları
  * Veri tümleştirme katmanı
  * Gerçek zamanlı analiz katmanı
  * Veri depolama katmanı
  * Sunu / tüketim katman
* Sonuç

**Yazar:** mükemmel, Microsoft Corporation'ın Charles Feddersen, çözümü Mimarı veri Öngörüler Merkezi

**Yayımlanan:** Ocak 2015

**Düzeltme:** 1.0

**İndirin:** [gerçek zamanlı Olay Microsoft Azure akış Analizi ile işleme](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)

## <a name="get-help"></a>Yardım alın
Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.

## <a name="next-steps"></a>Sonraki adımlar
* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)

