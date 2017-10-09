---
title: "aaaHow tooBuild karmaşık zamanlamalar ve Gelişmiş yineleme Azure Scheduler ile"
description: "Karmaşık tooBuild zamanlar nasıl ve Gelişmiş yineleme Azure Scheduler ile"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 5c124986-9f29-4cbc-ad5a-c667b37fbe5a
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 02172791978b12be0ccb3078125d057b2efe8523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobuild-complex-schedules-and-advanced-recurrence-with-azure-scheduler"></a>Karmaşık tooBuild zamanlar nasıl ve Gelişmiş yineleme Azure Scheduler ile
## <a name="overview"></a>Genel Bakış
Azure Scheduler Hello Kalp hello iş *zamanlama*. ne zaman ve nasıl hello Zamanlayıcı hello iş yürütür Hello zamanlamasını belirler.

Azure Zamanlayıcı toospecify bir iş için farklı bir kerelik ve yinelenen zamanlamalar sağlar. *Tek seferlik* zamanlamaları yangın bir belirtilen zamanda bir kez – etkili bir şekilde, bunlar *yinelenen* yalnızca bir kez yürütme zamanlamaları. Önceden belirlenmiş bir sıklık yinelenen zamanlamalar yangın.

Bu esneklik ile Azure Scheduler, çok çeşitli iş senaryolarını desteklemek olanak sağlar:

* Düzenli veri temizleme – örn., her gün 3 aydan daha eski tüm tweet'leri Sil
* Arşiv – örn., her ay, anında Fatura geçmişi toobackup hizmeti
* Dış veri – istekleri her 15 dakikada örn., NOAA yeni skı hava durumu raporu isteme
* Görüntü işleme – örneğin her hafta içi günü, yoğun olmayan saatlere, bulut bilgi işlem toocompress görüntüleri o gün karşıya kullanın

Bu makalede, Azure Scheduler ile oluşturabileceğiniz örnek işleri size rehberlik eder. Her zamanlamayı açıklar hello JSON verilerini sunuyoruz. Merhaba kullanırsanız [Scheduler REST API](https://msdn.microsoft.com/library/mt629143.aspx), bu aynı JSON için kullanabileceğiniz [Azure Scheduler işi oluşturma](https://msdn.microsoft.com/library/mt629145.aspx).

## <a name="supported-scenarios"></a>Desteklenen senaryolar
Merhaba, bu konudaki birçok örnekler Azure Scheduler destekleyen senaryoları hello derecesini gösterir. Genel anlamıyla nasıl dahil olmak üzere birçok davranış desenleri toocreate zamanlamalarını olanları aşağıdaki hello Bu örneklerde gösterilmiştir:

* Belirli tarih ve saatte bir kez çalıştır
* Çalıştırın ve açık sayısı Yinele
* Hemen çalıştırmak ve Yinele
* Çalıştırın ve tekrarlamayı her  *n*  dakika, saat, gün, hafta veya ay, belirli bir zamanda başlatılıyor
* Çalıştırın ve haftalık veya aylık sıklığı ancak yalnızca belirli gün, haftanın belirli gün veya ayın belirli günlerine Yinele
* Çalıştırın ve birden çok kez – örn., son Cuma ve Pazartesi her ayın ya da 5: 15'da ve 17:15:00 saatleri her gün bir süre içinde adresindeki Yinele

## <a name="dates-and-datetimes"></a>Tarihleri ve tarih/saat
Azure zamanlayıcı işlerinin tarihleri izleyin hello [ISO 8601 belirtimi](http://en.wikipedia.org/wiki/ISO_8601) ve yalnızca başlangıç tarihini içerir.

Azure zamanlayıcı işlerinin tarih-saat başvurularında izleyin hello [ISO 8601 belirtimi](http://en.wikipedia.org/wiki/ISO_8601) ve tarih ve saat bölümleri içerir. UTC uzaklığı belirtmiyor bir tarih-saat toobe UTC varsayılır.  

## <a name="how-to-use-json-and-rest-api-for-creating-schedules"></a>Nasıl yapılır: Zamanlama oluşturmak için JSON ve REST API kullanma
kullanarak bir basit zamanlama toocreate hello [Azure Scheduler REST API](https://msdn.microsoft.com/library/mt629143), ilk [aboneliğinizi kayıt kaynak sağlayıcısı ile](https://msdn.microsoft.com/library/azure/dn790548.aspx) (Zamanlayıcı hello sağlayıcı adı  *Microsoft.Scheduler*), ardından [iş koleksiyonu oluşturma](https://msdn.microsoft.com/library/mt629159.aspx)ve son olarak [bir iş oluşturmak](https://msdn.microsoft.com/library/mt629145.aspx). Bir proje oluşturduğunuzda, zamanlama ve yinelenme biri aşağıda adlı çalışmasından hello gibi JSON kullanarak belirtebilirsiniz:

    {
        "startTime": "2012-08-04T00:00Z", // optional
         …
        "recurrence":                     // optional
        {
            "frequency": "week",     // can be "year" "month" "day" "week" "hour" "minute"
            "interval": 1,                // optional, how often toofire (default too1)
            "schedule":                   // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]                      
            },
            "count": 10,                  // optional (default toorecur infinitely)
            "endTime": "2012-11-04",      // optional (default toorecur infinitely)
        },
        …
    }

## <a name="overview-job-schema-basics"></a>Genel Bakış: İş şema temelleri
Aşağıdaki tablonun hello hello temel öğe ilgili toorecurrence ve bir iş zamanlaması üst düzey bir genel bakış sağlar:

| **JSON adı** | **Açıklama** |
|:--- |:--- |
| ***startTime*** |*startTime* bir tarih-saat değil. Basit tabloları için *startTime* hello ilk geçtiği ve karmaşık zamanlamalar için daha önce hello işi başlatacak *startTime*. |
| ***Yineleme*** |Merhaba *yineleme* hello işi ve hello yinelenme hello işi ile yürütecek için yineleme kuralları nesnesini belirtir. Merhaba yinelenme nesnesi destekler hello öğeleri *sıklığı aralığını, endTime, count,* ve *zamanlama*. Varsa *yineleme* tanımlanan *sıklığı* gereklidir; diğer öğeleri hello *yineleme* isteğe bağlıdır. |
| ***Sıklık*** |Merhaba *sıklığı* işi sırasında hangi hello yinelenen hello sıklığı birim temsil eden dize. Desteklenen değerler *"dakika", "saat", "gün", "hafta",* veya *"ay."* |
| ***aralığı*** |Merhaba *aralığı* pozitif bir tamsayı olan ve hello hello aralığı gösterir *sıklığı* , ne sıklıkta hello iş çalışacağını belirler. Örneğin, varsa *aralığı* 3 ve *sıklığı* "hafta" Merhaba iş yinelenen 3 haftada. Azure Zamanlayıcı destekleyen en *aralığı* aylık sıklık haftalık sıklığı için 78 haftalık veya günlük sıklığı 548 gün 18 ay sayısı. Saat ve dakika sıklığı için desteklenen hello aralığı 1. < = *aralığı* < = 1000. |
| ***endTime*** |Merhaba *endTime* dize hello tarih-saat iş hangi hello değil yürütme belirtir. Geçerli toohave değil bir *endTime* hello geçmiş içinde. Öyle değilse *endTime* veya sayı belirtilirse, hello işi çalıştıktan sonsuz. Her ikisi de *endTime* ve *sayısı* Merhaba dahil edilemez aynı işi. |
| ***sayısı*** |<p>Merhaba *sayısı* hello sayısı bu işlemi gerçekleştirmeden önce çalışmalı belirten bir pozitif tamsayı (sıfırdan büyük).</p><p>Merhaba *sayısı* hello hello işi çalıştıktan tamamlandı olarak belirlenen önce sayısını temsil eder. Örneğin, günlük ile çalıştırılan bir iş için *sayısı* 5 ve başlangıç tarihi Pazartesi, hello işi tamamlandıktan sonra yürütme Cuma günü. Merhaba başlatırsanız hello son tarihi olan, hello ilk yürütme hello oluşturma saati hesaplanır.</p><p>Öyle değilse *endTime* veya *sayısı* belirtilirse, hello işi çalıştıktan sonsuz. Her ikisi de *endTime* ve *sayısı* Merhaba dahil edilemez aynı işi.</p> |
| ***zamanlama*** |Bir iş belirtilen sıklık yinelenme zamanlamaya göre kendi yinelenme değiştirir. A *zamanlama* dakika, saat, haftanın günü, ay gün ve hafta numarasını göre değişiklikleri içerir. |

## <a name="overview-job-schema-defaults-limits-and-examples"></a>Genel Bakış: İş şema Varsayılanları, sınırlar ve örnekler
Bu genel bakışta sonra şimdi ayrıntılı bu öğelerin her biri açıklanmaktadır.

| **JSON adı** | **Değer türü** | **Gerekli?** | **Varsayılan değer** | **Geçerli değerler** | **Örnek** |
|:--- |:--- |:--- |:--- |:--- |:--- |
| ***startTime*** |Dize |Hayır |None |ISO-8601 Tarih-Saatleri |<code>"startTime" : "2013-01-09T09:30:00-08:00"</code> |
| ***Yineleme*** |Nesne |Hayır |None |Yinelenme nesnesi |<code>"recurrence" : { "frequency" : "monthly", "interval" : 1 }</code> |
| ***Sıklık*** |Dize |Evet |None |"dakika", "saat", "gün", "hafta", "ay" |<code>"frequency" : "hour"</code> |
| ***aralığı*** |Sayı |Hayır |1 |1 too1000. |<code>"interval":10</code> |
| ***endTime*** |Dize |Hayır |None |Merhaba gelecekteki bir sürede gösteren tarih saat değeri |<code>"endTime" : "2013-02-09T09:30:00-08:00"</code> |
| ***sayısı*** |Sayı |Hayır |None |>= 1 |<code>"count": 5</code> |
| ***zamanlama*** |Nesne |Hayır |None |Zamanlama nesnesi |<code>"schedule" : { "minute" : [30], "hour" : [8,17] }</code> |

## <a name="deep-dive-starttime"></a>Derin Dalış: *startTime*
Merhaba aşağıdaki tablo yakalamaları nasıl *startTime* bir işlemin nasıl yürütüleceğini denetler.

| **startTime değeri** | **Yineleme yok** | **Yineleme. Hiçbir zamanlama** | **Zamanlama ile yineleme** |
|:--- |:--- |:--- |:--- |
| **Başlangıç saati yok** |Hemen bir kez çalıştır |Hemen bir kez çalıştırın. Sonraki yürütmelerde son yürütme saati hesaplamaya göre Çalıştır |<p>Hemen bir kez çalıştır</p><p>Sonraki çalıştırmaları yinelenme zamanlamasına göre gerçekleştirir</p> |
| **Başlangıç zamanı geçmişte** |Hemen bir kez çalıştır |<p>İlk gelecekteki yürütme zamanı başlangıç zamanından sonra hesaplamak ve o anda çalıştırın</p><p>Son Yürütme saati göre sonraki yürütmelerde oncalculating çalıştırın</p><p>Daha ayrıntılı bir açıklama için bu tablodan sonra örnek bakın</p> |<p>İş başlatır *Hayır sooner daha* hello belirtilen başlangıç saati. Merhaba ilk oluşum hello başlangıç saati hesaplanan hello zamanlama bağlıdır</p><p>Sonraki çalıştırmaları yinelenme zamanlamasına göre gerçekleştirir</p> |
| **Başlangıç zamanı gelecekte veya mevcut** |Bir kez belirtilen başlama saatinde Çalıştır |<p>Bir kez belirtilen başlama saatinde Çalıştır</p><p>Sonraki yürütmelerde son yürütme saati hesaplamaya göre Çalıştır</p> |<p>İş başlatır *Hayır sooner daha* hello belirtilen başlangıç saati. Merhaba ilk oluşum hello başlangıç saati hesaplanan hello zamanlama bağlıdır</p><p>Sonraki çalıştırmaları yinelenme zamanlamasına göre gerçekleştirir</p> |

Neler bir örnek görelim nerede *startTime* hello geçmiş olan ile *yineleme* ancak hiçbir *zamanlama*.  Bu hello geçerli saati 2015-04-08 olduğunu varsayalım 13:00, *startTime* 2015-04-07 14:00 ve *yineleme* 2 her gün (ile tanımlanmış *sıklığı*: gün ve *aralığı*: 2.) Bu hello Not *startTime* hello geçmiş olan ve geçerli saati hello önce gerçekleşir

Bu koşullar altında hello *ilk yürütme* 2015-04-09 14: 00'dan olacaktır\. Merhaba Zamanlayıcı altyapısı yürütme oluşumu hello başlangıç zamanından itibaren hesaplar.  Merhaba geçen tüm örnekleri atılır. Merhaba altyapısı hello gelecekteki oluşan hello sonraki örneği kullanır.  Bu durumda, *startTime* hello sonraki örnek 2:00 2015-04-09 ise o zamandan 2 gündür 2: 00'da, 2015-04-07 olduğundan.

Merhaba ilk yürütme hello aklınızda bulundurun aynı olsa bile hello startTime 2015-04-05 14:00 veya 2015-04-01 14:00\. Merhaba ilk yürütme sonrasında sonraki yürütmelerde hello kullanılarak hesaplanan bunlar 2015-04-11 2:00 pm, ardından 2015-04-13 2:00 pm adresindeki en sonra 2015-04-15 2:00 pm adresindeki durumda olacaktır – zamanlanmış vs.

Saat ve/veya dakika hello zamanlamada, bunlar varsayılan toohello saatleri ve/veya dakika hello ilk yürütme, sırasıyla ayarlanmazsa son olarak, ne zaman bir iş bir zamanlamaya sahiptir.

## <a name="deep-dive-schedule"></a>Derin Dalış: *zamanlama*
Bir yandan, bir *zamanlama* için *sınırı* hello iş yürütmeleri sayısı.  Örneğin, bir iş ile bir "ay" sıklığı sahipse bir *zamanlama* yalnızca günü 31 çalıştırır, hello iş bir 31 olan bu aylarda çalıştırılır<sup>st</sup> gün.

Üzerinde diğer yandan hello bir *zamanlama* ayrıca *genişletin* hello iş yürütmeleri sayısı. Örneğin, bir iş ile bir "ay" sıklığı sahipse bir *zamanlama* ayın günleri 1 ve 2 çalışır, 1 hello üzerinde hello işi çalıştıktan<sup>st</sup> ve 2<sup>nd</sup> yerine yalnızca bir kez hello ayın günleri bir ay.

Birden çok zamanlama öğesi belirtilmişse, hello değerlendirme hello en büyük toosmallest – hafta numarasını, ay gün, haftanın günü, saat ve dakika sırasıdır.

Merhaba aşağıdaki tabloda açıklanmaktadır *zamanlama* ayrıntılı öğeleri.

| **JSON adı** | **Açıklama** | **Geçerli değerler** |
|:--- |:--- |:--- |
| **dakika** |Dakika hangi hello iş çalıştırılır hello saat sayısı |<ul><li>Tamsayı veya</li><li>Tamsayı dizisi</li></ul> |
| **saatleri** |Hangi hello işin çalışacağı hello günün saatleri |<ul><li>Tamsayı veya</li><li>Tamsayı dizisi</li></ul> |
| **Haftanın günü** |Merhaba hafta hello iş günü çalıştırılır. Yalnızca weekly frequency değeri ile belirtilebilir. |<ul><li>"Pazartesi", "Salı", "Çarşamba", "Perşembe", "Cuma", "Cumartesi" ve "Pazar"</li><li>Değerler (en büyük dizi boyutu 7) yukarıdaki hello hiçbirini dizisi</li></ul>*Değil* büyük küçük harfe duyarlı |
| **monthlyOccurrences** |Merhaba ay hello işin hangi günlerde çalışacağını belirler. Yalnızca monthly frequency değeri ile belirtilebilir. |<ul><li>MonthlyOccurrence nesneler dizisi:</li></ul> <pre>{ "day": *day*,<br />  "occurrence": *occurrence*<br />}</pre><p> *gün* olan hello gün hello hafta hello işin çalışacağı, örneğin her Pazar hello ayın {Pazar}. Gereklidir.</p><p>Oluşum *oluşumu* hello ayında hello günün örneğin {Pazar, -1} hello hello ayın son Pazar günü olduğunu. İsteğe bağlı.</p> |
| **monthDays** |Merhaba ay hello iş günü çalıştırılır. Yalnızca monthly frequency değeri ile belirtilebilir. |<ul><li>Herhangi bir değer < = -1 ve >-31 =.</li><li>Herhangi bir değer > = 1 ve < = 31 açın.</li><li>Yukarıdaki değerlerden oluşan bir dizi</li></ul> |

## <a name="examples-recurrence-schedules"></a>Örnekler: Yineleme zamanlamaları
Yineleme zamanlamaları – hello zamanlamaya nesnesi ve alt öğeleri odaklanan çeşitli örnekleri Hello aşağıda verilmiştir.

Merhaba altındaki tüm zamanlamalar varsayın bu hello *aralığı* too1 ayarlayın\. Ayrıca, bir belge toowhat sağ sıklığı hello hello olduğunu varsayalım gerekir *zamanlama* – örn., biri olamaz sıklığı "gün" kullanıyorsanız ve "monthDays" değişiklik hello zamanlama. Tür kısıtlamaları, yukarıda açıklanan.

| **Örnek** | **Açıklama** |
|:--- |:--- |
| <code>{"hours":[5]}</code> |5'te çalıştırmak her gün. Azure Zamanlayıcı her değeri "dakika", tek tek, tüm hello saatler sırasında hangi hello toobe iş listesini çalıştırmak toocreate her değeri olan "saat" eşleşir. |
| <code>{"minutes":[15], "hours":[5]}</code> |5: 15'da çalıştırma her gün |
| <code>{"minutes":[15], "hours":[5,17]}</code> |5: 15'da ve 17:15:00 saatleri sırasında çalıştıran her gün |
| <code>{"minutes":[15,45], "hours":[5,17]}</code> |5: 15'te, 5: 45'te, çalıştırmak 17:15:00 saatleri ve 5:45 PM her gün |
| <code>{"minutes":[0,15,30,45]}</code> |Her 15 dakikada çalıştırın |
| <code>{hours":[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23]}</code> |Her saat çalıştırın. Bu iş saatte çalışır. Merhaba dakika hello tarafından denetlenen *startTime*, belirtilmişse veya hiçbiri hello oluşturulma tarihine göre belirtilmişse,. Merhaba başlangıç saati veya oluşturma zamanı (hangisi) saat 12: 25'e ise, örneğin, hello iş 00:25 ', 01:25, çalıştırılacak 02:25,..., 23:25. Merhaba eşdeğer toohaving bir işlemle zamanlamadır *sıklığı* "saat", bir *aralığı* 1 ve Hayır *zamanlama*. Merhaba Bu zamanlama ile farklı kullanılabilir olduğunu farktır *sıklığı* ve *aralığı* toocreate diğer işleri çok. Örneğin, hello *sıklığı* "ay" olan, hello zamanlama her gün yerine ayda yalnızca bir kez çalışır *sıklığı* "gün" olan |
| <code>{minutes:[0]}</code> |Her saat, saat hello üzerinde çalıştırın. Bu işlemi de her saat çalışır ancak başlangıç saati (örn: 00: 00, 1 AM, 2: 00, vs.) Bu "saat" sıklığını eşdeğer tooa işlemiyle, startTime sıfır dakika ve zamanlama olmadan hello sıklığı olan "gün", ancak hello sıklığı "hafta" veya "ay" olsaydı, hello zamanlama yalnızca bir gününü bir hafta veya ayda bir bir gün sırasıyla yürütülür olur. |
| <code>{"minutes":[15]}</code> |15 dakika olarak çalıştır saati aşan her saat. 00:15'ten başlayarak 01:15, 02:15 gibi saatte bir çalışır ve 22:15 ile 23:15'te biter. |
| <code>{"hours":[17], "weekDays":["saturday"]}</code> |5 PM Cumartesi günleri çalışan her hafta |
| <code>{hours":[17], "weekDays":["monday", "wednesday", "friday"]}</code> |5 PM Pazartesi, Çarşamba ve Cuma çalışan her hafta |
| <code>{"minutes":[15,45], "hours":[17], "weekDays":["monday", "wednesday", "friday"]}</code> |17:15:00 saatleri ve 5:45 PM Pazartesi, Çarşamba ve Cuma çalışan her hafta |
| <code>{"hours":[5,17], "weekDays":["monday", "wednesday", "friday"]}</code> |5 AM ve 17: 00 saatleri Pazartesi, Çarşamba ve Cuma çalışan her hafta |
| <code>{"minutes":[15,45], "hours":[5,17], "weekDays":["monday", "wednesday", "friday"]}</code> |5: 15'te, 5: 45'te, çalıştırmak 17:15:00 saatleri ve 5:45 PM Pazartesi, Çarşamba ve Cuma her hafta |
| <code>{"minutes":[0,15,30,45], "weekDays":["monday", "tuesday", "wednesday", "thursday", "friday"]}</code> |Haftanın her günü 15 dakikada bir çalışır |
| <code>{"minutes":[0,15,30,45], "hours": [9, 10, 11, 12, 13, 14, 15, 16] "weekDays":["monday", "tuesday", "wednesday", "thursday", "friday"]}</code> |09: 00 ve 4:45 PM her 15 dakikada günlerinde Çalıştır |
| <code>{"weekDays":["sunday"]}</code> |Başlangıç saatinde Pazar çalıştırın |
| <code>{"weekDays":["tuesday", "thursday"]}</code> |Salı ve Perşembe başlangıç saatinde Çalıştır |
| <code>{"minutes":[0], "hours":[6], "monthDays":[28]}</code> |6'de Çalıştır hello 28 gün her (ay sıklığını varsayılarak) ayı |
| <code>{"minutes":[0], "hours":[6], "monthDays":[-1]}</code> |6'da hello ayın son gününü hello üzerinde çalıştırın. Ayın son günü toorun hello bir projede kullanmak isterseniz, -1 28, 29, 30 ve 31 gün yerine kullanın. |
| <code>{"minutes":[0], "hours":[6], "monthDays":[1,-1]}</code> |6'da hello üzerinde çalıştır ilk ve her ayın son günü |
| <code>{monthDays":[1,-1]}</code> |Merhaba üzerinde ilk ve her ayın son günü başlangıç zamanında |
| <code>{monthDays":[1,14]}</code> |Merhaba üzerinde ilk ve her ay Fourteenth gün başlangıç zamanında |
| <code>{monthDays":[2]}</code> |Merhaba hello başlangıç saati ay ikinci günü çalıştırın |
| <code>{"minutes":[0], "hours":[5], "monthlyOccurrences":[{"day":"friday", "occurrence":1}]}</code> |5 sabah her ayın ilk Cuma çalıştırın |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":1}]}</code> |: Başlangıç saatinde her ayın ilk Cuma çalıştırın |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":-3}]}</code> |Ay sonundan üçüncü Cuma günü çalıştırmak başlangıç saatinde her ay |
| <code>{"minutes":[15], "hours":[5], "monthlyOccurrences":[{"day":"friday", "occurrence":1},{"day":"friday", "occurrence":-1}]}</code> |İlk ve son Cuma her ayın 5: 15'da çalışır |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":1},{"day":"friday", "occurrence":-1}]}</code> |İlk ve son Cuma her ayın başlama saatinde Çalıştır |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":5}]}</code> |Başlangıç saatinde her ayın beşinci Cuma çalıştırın. Varsa hiçbir beşinci Cuma bir ay içinde olduğundan, çalıştırmamanız bu mu zamanlanmış toorun yalnızca beşinci Cuma günleri. Merhaba Cuma hello ayın son gerçekleşen üzerinde toorun hello iş istiyorsanız -1 hello örneği için 5 yerine kullanarak düşünebilirsiniz. |
| <code>{"minutes":[0,15,30,45], "monthlyOccurrences":[{"day":"friday", "occurrence":-1}]}</code> |15 dakikada bir hello ayın son Cuma günü çalıştırmak |
| <code>{"minutes":[15,45], "hours":[5,17], "monthlyOccurrences":[{"day":"wednesday", "occurrence":3}]}</code> |5: 15'te, 5: 45'te, çalıştırmak 17:15:00 saatleri ve 5:45 her ay 3 Çarşamba hello PM üzerinde |

## <a name="see-also"></a>Ayrıca Bkz.
 [Scheduler nedir?](scheduler-intro.md)

 [Azure Scheduler kavramları, terminolojisi ve varlık hiyerarşisi](scheduler-concepts-terms.md)

 [Zamanlayıcı hello Azure portalını kullanmaya başlama](scheduler-get-started-portal.md)

 [Azure Scheduler’da planlar ve faturalama](scheduler-plans-billing.md)

 [Azure Scheduler REST API başvurusu](https://msdn.microsoft.com/library/mt629143)

 [Azure Scheduler PowerShell cmdlet’leri başvurusu](scheduler-powershell-reference.md)

 [Yüksek Azure Scheduler kullanılabilirliği ve güvenilirliği](scheduler-high-availability-reliability.md)

 [Azure Scheduler sınırları, varsayılanları ve hata kodları](scheduler-limits-defaults-errors.md)

 [Azure Scheduler giden bağlantı kimlik doğrulaması](scheduler-outbound-authentication.md)

