---
title: "Gerçek zamanlı Olay Stream Analytics olay işleme ile işleme | Microsoft Docs"
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
ms.openlocfilehash: b3057be995e551aac0761c3ce40a8dbf828a5f29
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a>Başvuru mimarisi: Gerçek zamanlı Olay Microsoft Azure akış Analizi ile işleme
Gerçek zamanlı Olay Azure akış Analizi ile işleme için başvuru mimarisi, Microsoft Azure ile hizmet (PaaS) akış işleme çözümü olarak gerçek zamanlı bir platform dağıtmak için genel şeması sağlamaya yöneliktir.

## <a name="summary"></a>Özet
Geleneksel olarak, analiz çözümleri analiz öncesinde verilerin depolandığı yetenekleri ETL (ayıklama, dönüştürme ve yükleme) ve veri ambarı, gibi temel. Daha fazla hızlı bir şekilde gelen veriler dahil değişen gereksinimleri, bu varolan model sınırla zorlayan. Yeni bir özellik olmamasına karşın, bir yaklaşım yaygın olarak tüm endüstri verticals benimsemiştir değil ve depolama önce akışları taşıma içinde verileri analiz etme olanağı bir çözümüdür. 

Microsoft Azure bir dizi farklı çözüm senaryoları ve gereksinimleri destekleyebildiğini analytics teknolojilerin kapsamlı bir katalog sağlar. Uçtan uca çözümünü dağıtmak için hangi Azure Hizmetleri seçme teklifleri derecesini verilen zor olabilir. Bu yazı, birlikte çalışabilirlik olay akışı çözümünü destekleyen çeşitli Azure Hizmetleri ve özellikleri açıklamak için tasarlanmıştır. Ayrıca müşteriler bu yaklaşım türünden yararlanabilir senaryolardan bazıları açıklanmaktadır.

## <a name="contents"></a>İçindekiler
* Yönetici Özeti
* Gerçek zamanlı analiz giriş
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
* [Azure Stream Analytics'e giriş](stream-analytics-introduction.md)
* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)

