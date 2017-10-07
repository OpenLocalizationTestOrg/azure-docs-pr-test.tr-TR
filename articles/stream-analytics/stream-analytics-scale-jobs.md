---
title: "aaaScale Stream Analytics işleri tooincrease işleme | Microsoft Docs"
description: "Akış birimleri nasıl giriş bölümlerini yapılandırma, hello sorgu tanımı ayarlama ve ayarlayarak tooscale akış analizi işleri iş öğrenin."
keywords: "veri akış, veri işleme, akış analizi ayarlama"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 7e857ddb-71dd-4537-b7ab-4524335d7b35
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/22/2017
ms.author: jeffstok
ms.openlocfilehash: 4ba8f6b2f8bfebd52cfa07696b501b42cda21f75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-azure-stream-analytics-jobs-tooincrease-stream-data-processing-throughput"></a>Ölçek Azure akış analizi işleri tooincrease akış veri işleme işleme
Bu makalede nasıl tootune Stream Analytics sorgu tooincrease üretilen iş akış analizi işleri için gösterilmektedir. Ayarlama hello analytics sorgu tanımı ve hesaplama ve ayarlama işi nasıl giriş bölümleri yapılandırarak tooscale Stream Analytics işleri öğrenin *akış birimleri* (SUs). 

## <a name="what-are-hello-parts-of-a-stream-analytics-job"></a>Akış analizi işi hello bölümlerini nelerdir?
Stream Analytics iş tanımı girişleri, sorgu ve çıktıyı içerir. Burada hello iş hello veri akışından okuma girdileridir. Merhaba sorgu kullanılan tootransform hello veri giriş akışı ve hello çıktı hello işini hello iş sonuçları yere gönderir.  

Bir işi veri akış için en az bir giriş kaynağı gerektirir. Merhaba veri akışı giriş kaynağı Azure event hub'ındaki veya Azure blob depolama alanındaki depolanabilir. Daha fazla bilgi için bkz: [giriş tooAzure Stream Analytics](stream-analytics-introduction.md) ve [Azure Stream Analytics ile çalışmaya başlamak](stream-analytics-real-time-fraud-detection.md).

## <a name="partitions-in-event-hubs-and-azure-storage"></a>Bölümler event hubs'a ve Azure depolama
Akış analizi işi ölçeklendirme bölümleri giriş veya çıkış hello yararlanır. Bir bölüm anahtarına göre alt kümeleri veri bölmek sağlar bölümleme. Merhaba verileri (örneğin, bir akış analizi işine) kullanır bir işlem kullanabilir ve verimliliğini artırır paralel olarak farklı bölümleri yazma. Akış Analizi ile çalışırken, olay hub'ları ve Blob Depolama bölümlendirme, yararlanabilirsiniz. 

Bölümleri hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın:

* [Olay hub'ları özelliklere genel bakış](../event-hubs/event-hubs-features.md#partitions)
* [Veri bölümlendirme](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a>Akış birimleri (SUs)
Akış birimleri (SUs) temsil eder hello kaynakları ve gereken gücünün tooexecute bir Azure akış analizi işi sipariş. SUs kapasite CPU, bellek, karışık bir ölçüyü temel bir şekilde toodescribe hello göreli olay işleme sağlamak ve okuma ve oranları yazma. Her SU tooroughly karşılık gelen 1 MB/sn'ye saniye. 

Kaç tane SUs seçme hello girişleri için hello bölüm yapılandırmasını ve hello sorgu hello iş için tanımlanan belirli bir işin bağlıdır için gereklidir. SUs tooyour kota bir iş için yukarı seçebilirsiniz. Varsayılan olarak, her Azure aboneliğinin kotası too50 SUs tüm hello analytics işleri yukarı belirli bir bölgede sahiptir. Bu kota, kişi ötesinde, abonelikler için SUs tooincrease [Microsoft Support](http://support.microsoft.com). İş başına SUs için geçerli değerler: 1, 3, 6 ve 6'ın artışlarla yukarı.

## <a name="embarrassingly-parallel-jobs"></a>Utandırıcı derecede paralel işi
Bir *utandırıcı derecede paralel* iş hello en ölçeklenebilir senaryo Azure akış analizi sunuyoruz. Bir bölüm hello sorgu tooone bölümünün hello çıktı hello giriş tooone örneğinin bağlanır. Bu paralellik hello gereksinimlerine sahiptir:

1. Sorgu mantığınızı aynı anahtar işlenmekte olan hello üzerinde bağımlıysa hello tarafından aynı örnek sorgu, hello olayları toohello Git emin olmanız gerekir, giriş aynı bölüm. Olay hub'ları için bu hello olay verilerini hello olmalıdır anlamına gelir **PartitionKey** değerinin ayarlanmış. Alternatif olarak, bölümlenmiş Gönderenler kullanabilirsiniz. BLOB Depolama için bu hello olayları toohello gönderilir anlamına gelir aynı bölüm klasör. Sorgu mantığınızı aynı işlenen toobe anahtarın hello gerektirmiyorsa hello tarafından aynı örnek sorgu, bu gereksinimin göz ardı edebilirsiniz. Bu mantık örneği basit bir select proje filtresi sorgu olacaktır.  

2. Merhaba veriler hello giriş tarafında düzenlendiğini sonra sorgunuzu bölümlenen emin olmanız gerekir. Bu toouse gerektirir **bölüm tarafından** tüm hello adımlarda. Birden çok adımı izin verilir, ancak hepsi tarafından hello bölümlenmiş gerekir aynı anahtarı. Şu anda, bölümlendirme anahtarı hello çok ayarlanmalıdır**PartitionID** hello iş toobe tam olarak paralel sırayla.  

3. Şu anda yalnızca olay hub'ları ve blob depolama bölümlenmiş çıkış destekler. Olay hub'ı çıkışı için hello bölüm anahtarı toobe yapılandırmalısınız **PartitionID**. BLOB Depolama çıktı için toodo herhangi bir şey yok.  

4. Giriş bölüm sayısı Hello hello çıkış bölüm sayısı eşit olmalıdır. BLOB Depolama çıkış bölümleri şu anda desteklemiyor. Ancak hello Yukarı Akış sorgusunun bölümleme hello devralır Tamam, olmasıdır. Örnek bir tam olarak paralel iş izin bölüm değerler şunlardır:  

   * 8 olay hub'ı giriş bölümleri ve 8 olay hub'ı bölümleri çıkış
   * 8 olay hub'ı giriş bölümleri ve blob depolama çıktı  
   * 8 blob depolama giriş bölümleri ve blob depolama çıkış  
   * Depolama giriş bölümleri ve 8 olay hub'ı çıkış bölümleri 8 blob  

Merhaba aşağıdaki bölümlerde utandırıcı derecede paralel bazı örnek senaryolar açıklanmaktadır.

### <a name="simple-query"></a>Basit Sorgu

* Giriş: 8 bölümlerle olay hub'ı
* Çıktı: 8 bölümlerle olay hub'ı

Sorgu:

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

Bu sorgu basit bir filtredir. Bu nedenle, event hub'ı toohello gönderilen hello giriş bölümleme hakkında tooworry gerekmez. Merhaba sorgulayan içerir dikkat edin **bölüm tarafından PartitionID**, gereksinimden #2 önceki yerine getirir. Merhaba çıktı için tooconfigure hello olay hub'ı çıkışı hello iş toohave hello bölümlendirmesini anahtar kümesi çok ihtiyacımız**PartitionID**. Bir son denetimi toomake hello giriş bölüm sayısı eşit toohello çıkış bölüm sayısı olduğundan emin olur.

### <a name="query-with-a-grouping-key"></a>Gruplandırma anahtarı ile sorgulama

* Giriş: 8 bölümlerle olay hub'ı
* Çıktı: Blob storage'ı

Sorgu:

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Bu sorgu gruplandırma anahtarı yok. Bu nedenle, aynı anahtar gereksinimlerini toobe aynı olayları toohello olay hub'ı bölümlenmiş bir şekilde gönderilmesi gerektiğini anlamına gelir örnek sorgu hello tarafından işlenen hello. Ancak, hangi anahtar kullanılmalıdır? **PartitionID** bir iş mantığı kavramdır. Biz gerçekte çok önem verdiğiniz hello anahtarı **TollBoothId**, bu nedenle hello **PartitionKey** hello olay verilerini değeri olmalıdır **TollBoothId**. Merhaba sorguda ayarlayarak bunu **bölüm tarafından** çok**PartitionID**. Merhaba çıkış blob depolama olduğundan, gereksinim #4 göre bir bölüm anahtarı değerini yapılandırma hakkında daha fazla tooworry gerekmez.

### <a name="multi-step-query-with-a-grouping-key"></a>Çok adımlı sorgusu gruplandırma anahtarı ile
* Giriş: 8 bölümlerle olay hub'ı
* Çıktı: 8 bölümlerle olay hub'ı örneği

Sorgu:

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Bu sorgu gruplandırma anahtara sahip; bu nedenle aynı anahtar gereksinimlerini toobe hello tarafından işlenen hello aynı sorgu örneği. Biz kullanabilirsiniz hello hello önceki örnekte olduğu gibi aynı stratejisi. Bu durumda, hello sorgu birden fazla adım vardır. Her adım sahip **bölüm tarafından PartitionID**? Evet, şekilde Hello sorgu #3 gereksinimini yerine getirir. Merhaba çıktı için tooset hello bölüm anahtarı çok ihtiyacımız**PartitionID**, daha önce bahsedildiği gibi. Ayrıca hello olduğunu görebiliriz aynı sayıda hello giriş bölümler.

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a>Örnek senaryoların *değil* utandırıcı derecede paralel

Merhaba önceki bölümde utandırıcı derecede paralel bazı senaryolar gösterilmiştir. Bu bölümde, tüm başlangıç gereksinimlerini toobe utandırıcı derecede paralel uymayan senaryolar açıklanmaktadır. 

### <a name="mismatched-partition-count"></a>Uyuşmayan bölüm sayısı
* Giriş: 8 bölümlerle olay hub'ı
* Çıkış: Olay hub'ı 32 bölümlerle

Bu durumda, önemli değildir hangi hello sorgudur. Merhaba giriş bölüm sayısı hello çıkış bölüm sayısı eşleşmiyorsa, hello topoloji utandırıcı derecede paralel değil.

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a>Olay hub'ları veya blob depolama çıkış olarak kullanan değil
* Giriş: 8 bölümlerle olay hub'ı
* Çıkış: Powerbı

Powerbı çıkış bölümleme şu anda desteklemiyor. Bu nedenle, bu senaryo utandırıcı derecede paralel değil.

### <a name="multi-step-query-with-different-partition-by-values"></a>Çok adımlı sorgu bölüm tarafından farklı değerlere sahip
* Giriş: 8 bölümlerle olay hub'ı
* Çıktı: 8 bölümlerle olay hub'ı

Sorgu:

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

Gördüğünüz gibi hello ikinci adımı kullanan **TollBoothId** bölümlendirme anahtarı hello olarak. Bu adım olan değil hello aynı hello ilk adım olarak ve bu nedenle bize toodo bir karışık gerektirir. 

Önceki örneklerde utandırıcı derecede paralel bir topoloji çok uygun (veya yok) bazı Stream Analytics işleri hello. Uygun değilse, bunlar en fazla ölçek hello potansiyeline sahiptir. Kılavuzu ölçeklendirme bu profillerinden birini uymayan işleri gelecekte kullanılabilecek yönelik güncelleştirmeler. Şimdilik, hello genel rehberlik hello aşağıdaki bölümleri kullanın.

## <a name="calculate-hello-maximum-streaming-units-of-a-job"></a>Merhaba maksimum akış birimleri, bir işin Hesapla
Hello toplam akış analizi işi tarafından kullanılan akış birim sayısını hello iş ve her adımı için bölüm hello sayısı için tanımlanan hello sorgusu adımlarda hello sayısına bağlıdır.

### <a name="steps-in-a-query"></a>Sorguda adımları
Sorguda bir veya daha fazla adım olabilir. Her bir adımdır hello tarafından tanımlanan alt sorgu **ile** anahtar sözcüğü. Merhaba dışında hello sorgu **ile** anahtar sözcüğü (yalnızca bir sorgu) hello gibi bir adım olarak ayrıca sayılan **seçin** sorgu aşağıdaki hello deyiminde:

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

Bu sorgu iki adımı vardır.

> [!NOTE]
> Bu sorgu hello makalenin sonraki bölümlerinde daha ayrıntılı ele alınmıştır.
>  

### <a name="partition-a-step"></a>Bir adımı bölüm
Bir adımı bölümleme hello aşağıdaki koşulları gerektirir:

* Merhaba giriş kaynağı bölümlenmiş olması gerekir. 
* Merhaba **seçin** hello sorgu deyimi bölümlenmiş bir giriş kaynağından okuma gerekir.
* Merhaba adım Hello sorguyla hello olmalıdır **bölüm tarafından** anahtar sözcüğü.

Bir sorgu bölümlenmiş hello giriş işlenen ve toplu olarak ayrı bölüm grupları olaylardır ve çıkışları olayları hello gruplarının her biri için oluşturulur. Birleştirilmiş bir toplama istiyorsanız, ikinci bir adım bölümlenmemiş tooaggregate oluşturmanız gerekir.

### <a name="calculate-hello-max-streaming-units-for-a-job"></a>Akış birimleri işi için hello en fazla Hesapla
Tüm bölümlenmemiş adımları birlikte Yukarı Akış birimleri (SUs) Stream Analytics işi için toosix ölçeklendirebilirsiniz. tooadd SUs, bir adım bölümlenmiş olması gerekir. Her bölüm altı SUs olabilir.

<table border="1">
<tr><th>Sorgu</th><th>Merhaba işi için en çok SUs</th></td>

<tr><td>
<ul>
<li>Merhaba sorgu bir adım içerir.</li>
<li>Merhaba adım bölümlenmiş değil.</li>
</ul>
</td>
<td>6</td></tr>

<tr><td>
<ul>
<li>Merhaba giriş veri akışı 3 ile bölümlenmiş.</li>
<li>Merhaba sorgu bir adım içerir.</li>
<li>Merhaba adım bölümlenmiş.</li>
</ul>
</td>
<td>18</td></tr>

<tr><td>
<ul>
<li>Merhaba sorgu iki adımı içerir.</li>
<li>Merhaba adımları hiçbiri bölümlenmiş.</li>
</ul>
</td>
<td>6</td></tr>

<tr><td>
<ul>
<li>Merhaba giriş veri akışı 3 ile bölümlenmiş.</li>
<li>Merhaba sorgu iki adımı içerir. Merhaba giriş adım bölümlenmiş ve hello ikinci adım değildir.</li>
<li>Merhaba <strong>seçin</strong> deyimi bölümlenmiş hello girişten okur.</li>
</ul>
</td>
<td>24 (bölümlenmiş adımlar için 18) + bölümlenmemiş adımları için 6</td></tr>
</table>

### <a name="examples-of-scaling"></a>Ölçeklendirme örnekleri

Merhaba aşağıdaki sorguyu araba üç tollbooths sahip Ücretli istasyonu giderek üç dakikalık penceresinde hello sayısını hesaplar. Bu sorgu SUs toosix genişletilebilir.

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Daha fazla toouse SUs hello sorgu, her ikisi de giriş veri akışı hello ve hello sorgu bölümlenmiş olması gerekir. Merhaba veri akışı bölümü too3 ayarlandığından, hello aşağıdaki değiştirilmiş sorgu too18 SUs Genişletilebilir:

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Bir sorgu bölümlenmiş, hello giriş olaylarını işlenir ve ayrı bölüm grupları bir araya getirilir. Çıkış olayları da hello gruplarının her biri için oluşturulur. Bölümleme hello olduğunda bazı beklenmeyen sonuçlara neden olabilecek **GROUP BY** alan hello giriş veri akışında hello bölüm anahtarı değil. Örneğin, hello **TollBoothId** hello önceki sorgu alanında hello bölüm anahtarı değil **Input1**. Merhaba, gişe #1 verileri birden çok bölüm yayılabilir bu hello sonucudur.

Her hello **Input1** bölümleri işlenmeyecek ayrı olarak akış analizi tarafından. Sonuç olarak, birden çok kayıt hello araba sayısı aynı atlayan pencere oluşturulacak hello içinde aynı gişe hello. Merhaba giriş bölüm anahtarı değiştirilemez, bu sorun aşağıdaki örneğine hello gibi bir bölüm dışı adımı ekleyerek sabit:

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

Bu sorgu ölçeklendirilmiş too24 SUs olabilir.

> [!NOTE]
> İki akışları birleştirilecekse toocreate hello birleştirmeler kullandığınız hello akışları tarafından hello sütunun hello bölüm anahtarı bölümlenir emin olun. Ayrıca hello sahip olduğunuzdan emin olun hem akışları bölüm aynı sayısı.
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a>Stream Analytics akış birimleri yapılandırın

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Kaynakları Hello listesinde tooscale istediğiniz ve açın hello Stream Analytics işi bulun.
3. Dikey penceresinde Hello altında iş **yapılandırma**, tıklatın **ölçek**.

    ![Azure portal Stream Analytics işi yapılandırma][img.stream.analytics.preview.portal.settings.scale]

4. Merhaba kaydırıcı tooset hello SUs hello iş için kullanın. Sınırlı toospecific SU ayarları olduğuna dikkat edin.


## <a name="monitor-job-performance"></a>İş performansını izleme
Hello Azure portal kullanarak, bir işin hello verimlilik izleyebilirsiniz:

![Azure Stream Analytics işleri izleme][img.stream.analytics.monitor.job]

Merhaba iş yükünün beklenen hello verimliliği hesaplayın. Merhaba verimlilik beklenenden daha az ise, hello giriş bölümü ayarlamak, hello sorgu ayarlamak ve SUs tooyour iş ekleyin.


## <a name="visualize-stream-analytics-throughput-at-scale-hello-raspberry-pi-scenario"></a>Stream Analytics verimlilik ölçekte görselleştirmek: Merhaba Raspberry Pi'yi senaryosu
toohelp nasıl Stream Analytics işlerini ölçeklendirme anlamak, giriş Raspberry Pi'yi aygıttan dayalı bir denemeyi gerçekleştirilir. Bu deneme birden çok akış birimleri ile bölümleri verimini hello etkisini görmek bize.

Bu senaryoda, algılayıcı verileri (istemciler) tooan olay hub'ı hello aygıt gönderir. Analytics akış hello veri işler ve bir uyarı ya da istatistikleri çıktı tooanother olay hub ' gönderir. 

Merhaba istemci algılayıcı verileri JSON biçiminde gönderir. Merhaba veri çıkışı da JSON biçimindedir. Merhaba veri şöyle görünür:

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

bir açık kapalı olduğunda sorgu aşağıdaki hello kullanılan toosend bir uyarı değildir:

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a>Ölçü işleme

Bu bağlamda verimlilik hello Sabit sürede akış analizi tarafından işlenen giriş veri miktarıdır. (Biz 10 dakika cinsinden ölçülen.) tooachieve hello hello için en iyi işleme işleme giriş, giriş iki hello veri akışı ve hello sorgu bölümlenmiş. Biz dahil **COUNT()** hello sorgu toomeasure kaç tane giriş olaylarını işlendi. toomake emin hello işi yalnızca giriş olaylarını toocome için beklediği değil, her bölüm hello giriş olay hub'ın yaklaşık 300 MB ile giriş verilerini önceden.

Merhaba aşağıdaki tabloda biz hello akış birim sayısını artar ve olay hub ' hello karşılık gelen bölüm sayar gördüğümüz hello sonuçları gösterilmektedir.  

<table border="1">
<tr><th>Giriş bölümleri</th><th>Çıktı bölümleri</th><th>Akış Birimleri</th><th>Aralıksız üretilen
</th></td>

<tr><td>12</td>
<td>12</td>
<td>6</td>
<td>4.06 MB/sn</td>
</tr>

<tr><td>12</td>
<td>12</td>
<td>12</td>
<td>8.06 MB/sn</td>
</tr>

<tr><td>48</td>
<td>48</td>
<td>48</td>
<td>38.32 MB/sn</td>
</tr>

<tr><td>192</td>
<td>192</td>
<td>192</td>
<td>172.67 MB/sn</td>
</tr>

<tr><td>480</td>
<td>480</td>
<td>480</td>
<td>454.27 MB/sn</td>
</tr>

<tr><td>720</td>
<td>720</td>
<td>720</td>
<td>609.69 MB/sn</td>
</tr>
</table>

Ve hello aşağıdaki grafiği gösterir SUs ve işleme arasında hello ilişkinin bir görsel öğe.

![img.Stream.Analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a>Yardım alın
Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Sonraki adımlar
* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->

[img.stream.analytics.monitor.job]: ./media/stream-analytics-scale-jobs/StreamAnalytics.job.monitor-NewPortal.png
[img.stream.analytics.configure.scale]: ./media/stream-analytics-scale-jobs/StreamAnalytics.configure.scale.png
[img.stream.analytics.perfgraph]: ./media/stream-analytics-scale-jobs/perf.png
[img.stream.analytics.streaming.units.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsStreamingUnitsExample.jpg
[img.stream.analytics.preview.portal.settings.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsPreviewPortalJobSettings-NewPortal.png   

<!--Link references-->

[microsoft.support]: http://support.microsoft.com
[azure.management.portal]: http://manage.windowsazure.com
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

