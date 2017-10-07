---
title: "Azure günlük analizi aaaUnderstanding uyarılar | Microsoft Docs"
description: "Günlük analizi uyarılarını OMS deponuzun önemli bilgileri tanımlamak ve önceden sorunları size bildiren veya Eylemler tooattempt toocorrect çağırma bunları.  Bu makalede hello farklı türdeki uyarı kuralları ve nasıl tanımlanır."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: bfa0a5aaeca81674e79a6d647f36d937efeeb439
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-alerts-in-log-analytics"></a>Günlük analizi, uyarıları anlama

Günlük analizi uyarılarını günlük analizi deponuzun önemli bilgiler tanımlayın.  Bu makalede, günlük analizi çalışma nasıl uyarı kuralları ayrıntılarını sağlar ve hello uyarı kuralları farklı türleri arasındaki farklar açıklanmaktadır.

Hello işlemi uyarı kuralları oluşturma, aşağıdaki makaleler hello bakın:

- Kullanarak uyarı kuralları oluşturmak [Azure portalı](log-analytics-alerts-creating.md)
- Kullanarak uyarı kuralları oluşturmak [Resource Manager şablonu](../operations-management-suite/operations-management-suite-solutions-resources-searches-alerts.md)
- Kullanarak uyarı kuralları oluşturmak [REST API'si](log-analytics-api-alerts.md)


## <a name="alert-rules"></a>Uyarı kuralları

Uyarılar, günlük aramaları düzenli aralıklarla otomatik olarak çalışacak uyarı kuralları tarafından oluşturulur.  Merhaba hello günlük arama sonuçlarını belirli ölçütlere uyan varsa bir uyarı kaydı oluşturulur.  Merhaba kuralı daha sonra otomatik olarak bir çalıştırabilirsiniz veya daha fazla Eylemler tooproactively hello uyarı bildiren veya başka bir işlem çağırma.  Farklı türde bir uyarı kuralları bu çözümleme farklı mantık tooperform kullanın.

![Log Analytics uyarıları](media/log-analytics-alerts/overview.png)

Uyarı kuralları aşağıdaki ayrıntılara hello tarafından tanımlanır:

- **Günlük arama**.  her zaman hello uyarı kuralı çalıştıran hello sorgusu gönderir.  Bu sorgu tarafından döndürülen hello kayıtları olup kullanılan toodetermine bir uyarı oluşturulur.
- **Zaman penceresi**.  Merhaba sorgu Hello zaman aralığını belirtir.  Merhaba sorgu bu hello aralığında geçerli saati oluşturulan kayıtları döndürür.  Bu, 5 dakika ile 24 saat arasında herhangi bir değer olabilir. Örneğin, hello zaman penceresi too60 dakika ve hello sorgu ayarlanmış 13: 15'te çalıştırılırsa, yalnızca saat 12: 15'e ve 13: 15'te arasında oluşturulan kayıtları döndürülür.
- **Sıklık**.  Ne sıklıkta hello sorgu çalıştırılması gerektiğini belirtir. 5 dakika ile 24 saat arasında herhangi bir değer olabilir. Merhaba zaman penceresi'den küçük eşit tooor olmalıdır.  Merhaba değeri hello zaman penceresi'den büyükse, eksik kayıtları riski oluşur.<br>Örneğin, 30 dakikalık bir zaman penceresi ve 60 dakika sıklığını göz önünde bulundurun.  Merhaba sorgu 1: 00'dan çalıştırırsanız, 12:30 ve 1:00 arasında kayıt döndürür.  Merhaba hello sorguyu çalıştırabilir sonraki 2:00 kayıtlar 1:30 ve 2:00 arasında ne zaman döndürecektir saattir.  1:00-1:30 arasında oluşturulan kayıtları hiçbir zaman değerlendirilmesi.
- **Eşik**.  bir uyarı oluşturulup oluşturulmayacağını hello hello günlük arama sonuçlarını değerlendirilen toodetermine ' dir.  Merhaba eşik hello farklı türlerde uyarı kuralları için farklıdır.

Günlük analizi her uyarı kuralı iki türlerinden biridir.  Bu türleri izleyin hello bölümlerde ayrıntılı olarak açıklanmıştır.

- **[Sonuç sayısı](#number-of-results-alert-rules)**. Merhaba sayı kayıtları hello günlük araması tarafından döndürülen oluşturulan tek bir uyarı belirtilen sayıyı aşıyor.
- **[Ölçüm ölçüm](#metric-measurement-alert-rules)**.  Belirtilen eşiğini aşan değerlerle hello günlük arama sonuçlarını hello her nesne için oluşturulan bir uyarı.

Uyarı kuralı türleri arasındaki farkları Hello aşağıdaki gibidir.

- **Sonuç sayısı** uyarı kuralı her zaman tek bir uyarı while Oluştur **ölçüm ölçüm** uyarı kuralı hello eşiğini aştığında her nesne için bir uyarı oluşturur.
- **Sonuç sayısı** tek bir kez hello eşiği aştığında bir uyarı uyarı kuralları oluşturmak. **Ölçüm ölçüm** uyarı kuralları, bir uyarı oluşturabilir, başlangıç eşiği aşıldığında, belirli bir süre boyunca belirli sayıda.

## <a name="number-of-results-alert-rules"></a>Sonuçları uyarı kuralları sayısı
**Sonuç sayısı** hello hello arama sorgusu tarafından döndürülen kayıt sayısını hello belirtilen eşiği aştığında uyarı kuralları oluşturmak tek bir uyarı.

### <a name="threshold"></a>Eşik
Merhaba eşiği için bir **sonuç sayısı** yalnızca büyük veya belirli bir değerden daha az uyarı kuralı.  Merhaba hello günlük araması tarafından döndürülen kayıt sayısını bu ölçütlere uyan varsa bir uyarı oluşturulur.

### <a name="scenarios"></a>Senaryolar

#### <a name="events"></a>Olaylar
Bu tür bir uyarı kuralı olaylar Windows olay günlükleri, Syslog, gibi ile çalışmak için idealdir ve özel günlüğe kaydeder.  Belirli hata olayı oluştururken ya da birden çok hata olayları belirli zaman penceresi içinde oluşturulduğunda, toocreate bir uyarı isteyebilirsiniz.

tek bir olay tooalert sonuçları toogreater 0 ve her ikisi de hello sıklığından hello sayısını ayarlayın ve pencere too5 dakika süresi.  Her 5 dakikada bir ve onay hello son zaman hello sorgu çalıştırıldıktan sonra oluşturulan tek bir olay hello geçtiği, hello sorguyu çalıştırır.  Bir uzun sıklığı hello olay olma toplanan ve oluşturulmakta hello uyarı arasındaki hello süre geciktirebilir.

Bazı uygulamalar, mutlaka bir uyarı oluşturmadan döndürmemelidir hatayla zaman oturum açabilir.  Örneğin, hello uygulama hello hata olayı oluşturan hello işlemi yeniden deneyin ve ardından bir sonraki sefer hello başarılı.  Bu durumda, birden çok olay belirli zaman penceresi içinde oluşturulan sürece toocreate hello uyarı istemeyebilirsiniz.  

Bazı durumlarda, bir olay hello olmaması durumunda toocreate bir uyarı isteyebilirsiniz.  Örneğin, bir işlem düzgün çalıştığını normal olaylarla tooindicate oturum açabilir.  Belirli bir zaman penceresi içinde aşağıdaki olaylardan biri oturum değil, bir uyarı oluşturulmalıdır.  Bu durumda, hello eşik çok ayarlamalısınız**değerinden 1**.

#### <a name="performance-alerts"></a>Performans uyarıları
[Performans verileri](log-analytics-data-sources-performance-counters.md) hello OMS deposu benzer tooevents kayıt olarak depolanır.  Bir performans sayacı belirli bir eşiği aştığında tooalert istiyorsanız, bu eşiği hello sorguda bulunması gerekir.

Tooalert hello zaman istediyseniz Örneğin, işlemci çalıştıran % 90'de, kullandığınız hello hello uyarı kuralı için başlangıç eşik ile aşağıdaki gibi bir sorgu **0'dan büyük**.

    Type=Perf ObjectName=Processor CounterName="% Processor Time" CounterValue>90

Merhaba işlemci üzerinde belirli bir zaman penceresi için % 90 ortalama zaman tooalert istediyseniz, hello kullanarak bir sorgu kullanırsınız [ölçmek komutu](log-analytics-search-reference.md#commands) ister hello uyarı kuralı için başlangıç eşiği hello aşağıdakilerle **0'dan büyük** .

    Type=Perf ObjectName=Processor CounterName="% Processor Time" | measure avg(CounterValue) by Computer | where AggregatedValue>90

>[!NOTE]
> Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), sorguları yukarıda hello toohello aşağıdaki değişeceğinden sonra:`Perf | where ObjectName=="Processor" and CounterName=="% Processor Time" and CounterValue>90`
> `Perf | where ObjectName=="Processor" and CounterName=="% Processor Time" | summarize avg(CounterValue) by Computer | where CounterValue>90`


## <a name="metric-measurement-alert-rules"></a>Ölçüm ölçüm uyarı kuralları

>[!NOTE]
> Ölçüm ölçüm uyarı kuralları şu anda genel önizlemede.

**Ölçüm ölçüm** uyarı kuralları bir sorguda belirtilen eşiği aşarsa bir değerle her nesne için bir uyarı oluştur.  Ayrı farkları aşağıdaki hello sahip oldukları **sonuç sayısı** uyarı kuralları.

#### <a name="log-search"></a>Günlük araması
Herhangi bir sorgu için kullanabilirsiniz, ancak bir **sonuç sayısı** uyarı kuralı, belirli gereksinimleri hello sorgusunu ölçüm ölçüm bir uyarı kuralı vardır.  İçermesi gerekir bir [ölçmek komutu](log-analytics-search-reference.md#commands) toogroup hello sonuçları belirli bir alan. Bu komut, öğeleri aşağıdaki hello eklemeniz gerekir.

- **Toplama işlevi**.  Gerçekleştirilen hello hesaplama ve büyük olasılıkla bir sayısal alana tooaggregate belirler.  Örneğin, **count()** kayıt hello sayısını hello sorguda döndürülecek **avg(CounterValue)** hello aralığı içinde hello CounterValue alanının hello ortalamasını döndürür.
- **Alan grup**.  Bu alan her örneği için bir toplu değeri içeren bir kayıt oluşturulur ve her biri için bir uyarı oluşturulabilir.  Örneğin, her bilgisayar için bir uyarı toogenerate istediyseniz, kullanacağınız **bilgisayar tarafından**.   
- **Aralığı**.  Merhaba zaman aralığı üzerinde hello verileri toplanır tanımlar.  Örneğin, belirttiğiniz **5minutes**, hello uyarı için belirtilen hello zaman penceresi üzerinden 5 dakikalık aralıklarla toplanan hello grup alanı her örneği için bir kayıt oluşturulması.

#### <a name="threshold"></a>Eşik
Merhaba eşiği ölçüm ölçüm uyarı kuralları için bir toplam değerini ve bir dizi tarafından tanımlanır.  Merhaba günlük arama herhangi bir veri noktasını bu değeri aştığında bir ihlal dikkate almıştır.  Merhaba dizi içinde herhangi bir nesnenin hello sonuçlarında aşarsa hello belirtilen değer, ardından bu nesne için bir uyarı oluşturulur.

#### <a name="example"></a>Örnek
Burada herhangi bir bilgisayar işlemci kullanımı % 90'ın üç kez üzerinde 30 dakika aşılırsa bir uyarı isteyen bir senaryo düşünün.  Aşağıdaki ayrıntılara hello ile bir uyarı kuralı oluşturursunuz.  

**Sorgu:** türü Perf ObjectName = işlemci CounterName = "% işlemci zamanı" = | avg(CounterValue) 5 dakika bilgisayar aralığına göre ölçün<br>
**Zaman penceresi:** 30 dakika<br>
**Uyarı sıklığı:** 5 dakika<br>
**Toplam değer:** 90'dan büyük<br>
**Tetikleyici uyarı temel alarak:** toplam ihlal 5'ten büyük<br>

Merhaba sorgu her bilgisayar için bir ortalama değer 5 dakika aralıklarla oluşturursunuz.  Bu sorguyu her 5 dakikada bir toplanan veriler için önceki 30 dakika içinde hello çalıştırılmaz.  Örnek verileri varsayılan olarak, üç bilgisayarlar için aşağıda gösterilmiştir.

![Örnek sorgu sonuçları](media/log-analytics-alerts/metrics-measurement-sample-graph.png)

Bunlar hello % 90 eşiği 3 kez hello zaman penceresi ihlal beri bu örnekte, ayrı uyarılar srv02 ve srv03 oluşturulması.  Merhaba, **tetikleyici uyarı temel alarak:** çok değiştirilen**art arda** ardışık 3 örnek hello eşiği ihlal bu yana bir uyarı yalnızca srv03 için oluşturulacak sonra.

## <a name="alert-records"></a>Uyarı kaydeder
Günlük analizi uyarı kuralları tarafından oluşturulan uyarı kayıtlarına sahip bir **türü** , **uyarı** ve **SourceSystem** , **OMS**.  Bunlar, aşağıdaki tablonun hello hello özelliklere sahiptir.

| Özellik | Açıklama |
|:--- |:--- |
| Tür |*Uyarı* |
| SourceSystem |*OMS* |
| *Nesne*  | [Ölçüm ölçüm uyarıları](#metric-measurement-alert-rules) hello Grup alan için bir özelliğe sahiptir.  Örneğin, bilgisayarda hello günlük arama grupları hello uyarı kaydıyla varsa hello bilgisayarın hello ada sahip bir bilgisayar alan hello değeri olarak.
| AlertName |Merhaba uyarı adı. |
| AlertSeverity |Merhaba uyarı önem derecesi. |
| LinkToSearchResults |Merhaba uyarı oluşturulan hello sorgudan hello kayıtları döndüren tooLog Analytics günlük arama bağlayın. |
| Sorgu |Çalıştırıldığı hello sorgu metni. |
| QueryExecutionEndTime |Merhaba sorgu için hello zaman aralığı sonu. |
| QueryExecutionStartTime |Merhaba sorgu hello zaman aralığını başlangıcı. |
| ThresholdOperator | Merhaba uyarı kuralı tarafından kullanılan işleci. |
| ThresholdValue | Merhaba uyarı kuralı tarafından kullanılan değeri. |
| TimeGenerated |Tarih ve saat hello uyarı oluşturuldu. |

Merhaba tarafından oluşturulan uyarı kayıtları diğer tür vardır [uyarı yönetim çözümü](log-analytics-solution-alert-management.md) kullanarak ve [Power BI dışarı aktarır](log-analytics-powerbi.md).  Bunların tümüne sahip bir **türü** , **uyarı** göre ayırt edilen ancak kendi **SourceSystem**.


## <a name="next-steps"></a>Sonraki adımlar
* Merhaba yüklemek [uyarı yönetimi çözümü](log-analytics-solution-alert-management.md) günlük analizi ile birlikte uyarıları oluşturulan tooanalyze uyarıların toplanan System Center Operations Manager'dan.
* Daha fazla bilgi edinin [oturum aramaları](log-analytics-log-searches.md) uyarılar oluşturabilir.
* İzlenecek yollar için tamamlamak [bir webook yapılandırma](log-analytics-alerts-webhooks.md) bir uyarı kuralı ile.  
* Öğrenin nasıl toowrite [Azure automation'daki runbook'lar](https://azure.microsoft.com/documentation/services/automation) tooremediate sorunları uyarıları ile tanımlanır.
