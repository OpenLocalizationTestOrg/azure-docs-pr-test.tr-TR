---
title: "Azure Stream Analytics: akış birimleri, iş toouse verimli bir şekilde en iyi duruma getirme | Microsoft Docs"
description: "Ölçekleme ve performans Azure akış analizi için en iyi uygulamaları sorgulayın."
keywords: "Birim, sorgu performansı akış"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 5ad98b34d625190a879260f54c9eff0294e230cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-job-toouse-streaming-units-efficiently"></a>Akış birimleri, iş toouse verimli bir şekilde en iyi duruma getirme

Azure Stream Analytics iş akış birimleri (SUs) çalışan ağırlığı"" Merhaba performans toplar. SUs tüketilen tooexecute bir işi hello bilgi işlem kaynaklarını temsil eder. SUs kapasite CPU, bellek, karışık bir ölçüyü temel bir şekilde toodescribe hello göreli olay işleme sağlamak ve okuma ve oranları yazma. Merhaba sorgu mantığı ve sizden tooknow depolama katmanı performans konuları ihtiyaç duyan işiniz için el ile bellek ayırabilir ve hello CPU gerekli core-sayısı toorun işinizi zamanında yaklaşık kaldırır odaklanmak bu kapasite sağlar.

## <a name="how-many-sus-are-required-for-a-job"></a>Kaç tane SUs bir iş için gerekli?

Belirli bir proje için gerekli SUs Hello sayısını seçmeye hello bölüm yapılandırmasını hello girişleri ve hello iş içinde tanımlanan hello sorgu bağlıdır. Merhaba **ölçek** dikey verir tooset hello SUs sağ sayısı. Bu, en iyi uygulamadır tooallocate gerekli olandan daha fazla SUs olur. Merhaba Stream Analytics işleme altyapısı gecikme süresi ve ek bellek ayırma, hello maliyet verimliliği için en iyi duruma getirir.

Genel olarak, toostart kullanmayan sorgular için 6 SUs ile Merhaba en iyi uygulamalardan biridir *bölüm tarafından*. Ardından hello Lezzetli nokta temsili miktarda veriyi geçirmek ve hello SU % kullanım ölçüm inceleyin sonra SUs hello sayısı değişiklik bir deneme yanılma yöntemi kullanarak belirler.

Azure Stream Analytics herhangi bir işlem başlatmadan önce hello "sipariş arabelleği" adlı bir pencerede olayları tutar. Olayları hello sipariş pencereye zamanına göre sıralanır ve sonraki işlemleri geçici olarak sıralanmış hello olaylarına gerçekleştirilir. Olayları zamanına göre yeniden sıralama sağlar hello işleç sahip tüm görünürlük hello hello olayda belirlenen zaman çerçevesi. Ayrıca hello gerekli işleme gerçekleştirmek ve bir çıktı oluşturmak hello işleci olanak tanır. Bu mekanizma yan etkisi, işleme hello sipariş penceresinde hello süreye göre gecikti ' dir. Merhaba bellek alanını (, SU tüketim etkileyen) hello işin Bu sipariş penceresini açın ve hello içerdiği olayların sayısı hello boyutunun bir işlevdir.

> [!NOTE]
> Okuyucu Hello sayısını iş yükseltmeler sırasında değiştiğinde geçici uyarıları tooaudit günlüklerine yazılır. Akış analizi işleri, bu geçici sorunları otomatik olarak kurtarın.

## <a name="common-high-memory-causes-for-high-su-usage-for-running-jobs"></a>İşlerini çalıştırmak için yüksek SU kullanımı yaygın yüksek bellek nedenleri

### <a name="high-cardinality-for-group-by"></a>GROUP BY için yüksek kardinalite

gelen olayları Hello önemi hello işi için bellek kullanımını belirler.

Örneğin, `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, hello ilişkili numarası **kümelenmiş** hello nicelik hello sorgu.

yüksek kardinalite tarafından neden toomitigate sorunları kullanan bölümler artırarak hello sorguyu dışarıya ölçeklendirme **bölüm tarafından**.

```
Select count(*) from input
Partition By clusterid
GROUP BY clustered tumblingwindow (minutes, 5)
```

Merhaba sayısı *kümelenmiş* burada hello nicelik, GROUP BY.

Merhaba sorgu bölümlenmiş sonra birden çok düğümleri üzerinde dağılmış. Sonuç olarak, hangi sırayla hello hello sipariş arabellek boyutunu azaltır hello her düğümüne gelen olayların sayısı azalır. Ayrıca PartitionID tarafından olay hub'ı bölümler bölüm.

### <a name="high-unmatched-event-count-for-join"></a>BİRLEŞTİRME için yüksek eşleşmeyen olay sayısı

Merhaba birleştirme eşleşmeyen olayların sayısını hello sorgu hello bellek kullanımını etkiler. Örneğin, tıklama oluşturan toofind hello ad izlenim sayısı arayan bir sorgu gerçekleştirin:

```
SELECT id from clicks INNER JOIN,
impressions on impressions.id = clicks.id AND DATEDIFF(hour, impressions, clicks) between 0 AND 10
```

Bu senaryoda, birçok ads gösterilir ve birkaç tıklatmayla oluşturulan mümkündür. Böyle bir sonuç hello iş tookeep hello zaman penceresi içindeki tüm hello olayları gerektirir. Merhaba kullanılan bellek miktarına orantılı toohello pencere boyutu ve olay hızıdır. 

toomitigate bölüm tarafından kullanarak bu durumda, artırarak hello sorgu genişletme bölümler. 

Merhaba sorgu bölümlenmiş sonra birden çok işlem düğümleri üzerinde dağılmış. Sonuç olarak, hangi sırayla hello hello sipariş arabellek boyutunu azaltır hello her düğümüne gelen olayların sayısı azalır.

### <a name="large-number-of-out-of-order-events"></a>Çok fazla sayıda bozuk olayı 

Çok sayıda bozuk olay büyük zaman penceresi içinde hello "arabellek yeniden sıralamak" toobe büyük hello boyutunu neden olur. toomitigate bölüm tarafından kullanarak bu durumda, Ölçek hello sorgu artırarak bölümler. Merhaba sorgu bölümlenmiş sonra birden çok düğümleri üzerinde dağılmış. Sonuç olarak, hangi sırayla hello hello sipariş arabellek boyutunu azaltır hello her düğümüne gelen olayların sayısı azalır. 


## <a name="get-help"></a>Yardım alın
Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Sonraki adımlar
* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics sorgu dili başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Yönetimi REST API Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)
