---
title: "Günlük analizi aaaAzure Arama başvurusu | Microsoft Docs"
description: "Merhaba günlük analizi Arama başvurusu hello arama dili açıklar ve verileri için arama ve filtreleme ifadeleri toohelp aramanızı olduğunda kullanabileceğiniz hello genel sorgu sözdizimi seçenekleri sağlar."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 402615a2-bed0-4831-ba69-53be49059718
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7478a1139b88a1ce76ebb7b76027a6ccd66f4f27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-search-reference"></a>Günlük analizi başvuru arama

>[!NOTE]
> Bu makalede günlük analizi hello geçerli sorgu dili kullanarak günlük arar.  Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), çok başvurmalıdır sonra[hello hello yeni dil için dil başvurusu](https://go.microsoft.com/fwlink/?linkid=856079).

Hello arama dili ile ilgili aşağıdaki bölüme verileri için arama ve filtreleme ifadeleri toohelp aramanızı olduğunda kullanabileceğiniz hello genel sorgu sözdizimi seçenekleri açıklar. Ayrıca, alınan hello veri üzerinde tootake eylem kullanabileceğiniz komutlar anlatır.

Aramalarda döndürülen hello alanları hakkında bilgi edinebilirsiniz ve yardımcı hello modelleri verilerde hello benzer kategorileri hakkında daha fazla bilgi bulmak [arama alanı ve model başvuru bölüm](#search-field-and-facet-reference).

## <a name="general-query-syntax"></a>Genel sorgu söz dizimi
Genel sorgulama hello söz dizimi aşağıdaki gibidir:

```
filterExpression | command1 | command2 …
```

Merhaba filtre ifadesi (`filterExpression`) "" koşul için sorgu hello hello tanımlar. Merhaba komutlar hello sorgu tarafından döndürülen toohello sonuçları uygulanır. Birden çok komut hello dikey çizgi karakterinden (|) tarafından ayrılmış olması gerekir.

### <a name="general-syntax-examples"></a>Genel sözdizimi örnekleri
Örnekler:

```
system
```

Bu sorgunun döndürdüğü hello sözcüğünü içeren sonuçları *sistem* için tam metin dizinli veya arama koşulları herhangi bir alanda.

> [!NOTE]
> Merhaba metinsel (açıklamaları ve adları gibi) genellikle alanları en yaygın olan ancak bu şekilde tüm alanlar dizinlenir.
>
>

```
system error
```

Bu sorgunun döndürdüğü hello sözcüklerini sonuçları *sistem* ve *hata*.

```
system error | sort ManagementGroupName, TimeGenerated desc | top 10
```

Bu sorgunun döndürdüğü hello sözcüklerini sonuçları *sistem* ve *hata*. Ardından hello tarafından hello sonuçlarını sıralar *ManagementGroupName* (artan düzende), alan ve sonra hello *TimeGenerated* alanındaki (Azalan). İlk 10 sonuçları yalnızca hello sürer.

> [!IMPORTANT]
> Tüm alan adları hello ve hello hello dize ve metin alanları için büyük küçük harfe duyarlı değerlerdir.
>
>

## <a name="filter-expressions"></a>Filtre ifadeleri
Aşağıdaki alt bölümleri hello hello filtre ifadeleri açıklanmaktadır.

### <a name="string-literals"></a>Dize değişmez değerleri
Bir dize hazır değer hello ayrıştırıcı tarafından bir anahtar sözcük veya önceden tanımlanmış veri türü (örneğin, bir sayı veya tarih) tanınmıyor herhangi bir dize ' dir.

Örnekler:

```
These all are string literals
```

Bu sorgu için tüm beş sözcükleri oluşumları içeren sonuçları arar. tooperform karmaşık dize arama hello dize tırnak işaretleri içine alın. Örneğin:

```
"Windows Server"
```

Bu yalnızca tam eşleşmeleri olan sonuçlar döndürür *Windows Server*.

### <a name="numbers"></a>Sayılar
Merhaba ayrıştırıcı hello ondalık tamsayı ve kayan noktalı sayı sözdizimi sayısal alanlar için destekler.

Örnekler:

```
Type:Perf 0.5
```

```
HTTP 500
```

### <a name="dates-and-times"></a>Tarihler ve saatler
Her bir veri hello sisteminde parçası olan bir *TimeGenerated* hello özgün tarih ve saat hello kaydının temsil eden özellik. Bazı veri türleri ek tarih ve saat alanları olabilir (örneğin, *LastModified*).

Zaman Çizelgesi hello **grafik/saat** Azure günlük analizi seçicide sonuçlar dağıtılması (çalıştırılmayı according toohello geçerli sorgu) zamanla gösterilir. Bu hello üzerinde temel *TimeGenerated* alan. Tarih ve saat alanları sorgular toorestrict hello sorgu tooa belirli bir zaman çerçevesi içinde kullanılan belirli dize biçimi sahiptir. Sözdizimi toorefer toorelative arasındaki zaman aralığı (örneğin, "3 gün önce ve 2 saat önce") de kullanabilirsiniz.

Merhaba geçerli tür sözdizimi tarihler ve saatler için şunlardır:

```
yyyy-mm-ddThh:mm:ss.dddZ
```

```
yyyy-mm-ddThh:mm:ss.ddd
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm
```

```
yyyy-mm-dd
```


Örneğin:

```
TimeGenerated:2013-10-01T12:20
```

Hello önceki komutu yalnızca kayıtları döndüren bir *TimeGenerated* değeri tam olarak 12:20 1 Ekim 2013.

Merhaba ayrıştırıcı hello anımsatıcı tarih/saat değeri, şimdi de destekler. (Verileri bu hızlı başlangıç sistemi üzerinden yapmaz olduğundan, bu herhangi bir sonuç sunacak düşüktür.)

Bu yapı taşları toouse mutlak tarihler için verilebilir. İçinde sonraki üç alt bölümleri Merhaba, nasıl toouse bunları daha gelişmiş görürsünüz göreli bir tarih aralıkları kullanmanız örnekleriyle filtreler.

### <a name="datetime-math"></a>Matematik tarih
Merhaba tarih matematik işleçleri toooffset kullanın veya basit tarih hesaplamaları kullanarak hello tarih/saat değerine YUVARLA.

Sözdizimi:

```
datetime/unit
```

```
datetime[+|-]count unit
```

| işleci | Açıklama |
| --- | --- |
| / |Yuvarlar tarih toohello birim belirtildi. Örneğin, şimdi / gün hello geçerli tarih toomidnight Merhaba, geçerli gün yuvarlar. |
| + veya - |Uzaklıkları tarih hello tarafından birim sayısı belirtildi. Örneğin, şimdi + 1 saat kaydırır hello geçerli tarih şimdi bir saat. 2013-10-01T12:00-10 gün hello tarih değeri 10 gün tarafından yeniden kaydırır. |

Merhaba tarih matematik işleçleri birlikte zincir. Örneğin:

```
NOW+1HOUR-10MONTHS/MINUTE
```

Merhaba aşağıdaki tabloda desteklenen hello tarih birimleri listeler.

| Tarih/saat birim | Açıklama |
| --- | --- |
| YIL, YIL |Yuvarlar toocurrent yıl veya hello tarafından uzaklıkları yıl sayısı belirtilmiş. |
| AY, AY |Ay sayısı belirtilen yuvarlar toocurrent ay veya uzaklıkları hello tarafından. |
| GÜN, TARİH |Yuvarlar toocurrent gününü hello ay veya uzaklıkları hello tarafından belirlenen gün sayısı. |
| SAAT, SAAT |Yuvarlar toocurrent saat veya hello tarafından uzaklıkları saat sayısı belirtildi. |
| DAKİKA, DAKİKA |Yuvarlar toocurrent minute veya uzaklıkları hello tarafından dakika sayısı belirtilmiş. |
| İKİNCİ OLARAK, SANİYE |Toocurrent ikinci yuvarlar veya kaydırır tarafından belirtilen hello saniye sayısı. |
| MİLİSANİYE, MİLİSANİYE CİNSİNDEN MİLİSANİYE, MILLIS |Yuvarlar toocurrent milisaniye veya uzaklıkları hello tarafından milisaniye sayısı belirtilmiş. |

### <a name="field-facets"></a>Alan modelleri
Alan modelleri kullanarak, belirli alanları ve tam değerlerine ilişkin hello arama koşulu belirtebilirsiniz. Bu, "serbest metin" sorguları yazma hello dizin boyunca çeşitli koşullar için farklıdır. Bu teknik birkaç önceki örneklerde zaten gördünüz. Merhaba, daha karmaşık örnekler verilmiştir.

**Sözdizimi**

```
field:value
```

```
field=value
```

**Açıklama**

Aramaları hello belirli değeri alanı hello. Merhaba değer bir dize sabit değeri, sayı veya tarih ve saat olabilir.

Örneğin:

```
TimeGenerated:NOW
```

```
ObjectDisplayName:"server01.contoso.com"
```

```
SampleValue:0.3
```

**Sözdizimi**

*alan > değeri*

*alan < değeri*

*alan > = değer*

*alan < value =*

*alan! = değer*

**Açıklama**

Karşılaştırmaları sağlar.

Örneğin:

```
TimeGenerated>NOW+2HOURS
```

**Sözdizimi**

```
field:[from..to]
```

**Açıklama**

Aralık olduğunu sağlar.

Örneğin:

```
TimeGenerated:[NOW..NOW+1DAY]
```

```
SampleValue:[0..2]
```

### <a name="in"></a>IN
Merhaba **IN** anahtar sözcüğü değerleri listesinden tooselect sağlar. Kullandığınız hello sözdizimi bağlı olarak bu basit sağladığınız değerler listesini ya da bir toplama değerleri listesi olabilir.

Sözdizimi 1:

```
field IN {value1,value2,value3,...}
```

Bu sözdiziminin basit bir listedeki tüm değerleri tooinclude sağlar.



Örnekler:

```
EventID IN {1201,1204,1210}
```

```
Computer IN {"srv01.contoso.com","srv02.contoso.com"}
```

Sözdizimi 2:

```
(Outer query) (Field toouse with inner query results) IN {Inner query | measure count() by (Field toosend tooouter query)} (rest  of outer query)  
```

Bu sözdiziminin toocreate bir toplama sağlar. Bu toplama bu değerle olaylarını arar başka bir dış (birincil) arama içine öğesinden sonra değer hello listesi akış. Merhaba iç arama ayraçlar içinde kapsayan ve hello IN işlecini kullanarak sonuçları hello dış arama alanında için olası değerler olarak besleme bunu.

İç sorgu örnek: *şu anda güvenlik güncelleştirmeleri eksik olan bilgisayarlar* toplama sorgu aşağıdaki hello ile:

```
Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer
```    

bulur hello son sorgu *şu anda güvenlik güncelleştirmeleri eksik olan bilgisayarlar için tüm Windows olayları* hello aşağıdakine benzer:

```
Type=Event Computer IN {Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer}
```

### <a name="contains"></a>Contains
Merhaba **içerir** anahtar sözcüğü, belirtilen dizeyi içeren bir alanı ile kayıt toofilter sağlar. Bu büyük küçük harfe duyarlıdır, yalnızca dize alanları ile çalışır ve herhangi bir kaçış karakteri içeremez.

Sözdizimi:

```
field:contains("string")
```

Örnek:

```
Type:contains("Event")
```

Bu, "Olay" Merhaba dizesi içeren bir türü kayıtlarıyla döndürür. Örnekler **olay**, **SecurityEvent**, ve **ServiceFabricOperationEvent**.



### <a name="regular-expressions"></a>Normal ifadeler
Hello kullanarak bir normal ifade ile bir alan için bir arama koşulu belirtebilirsiniz **Regex** anahtar sözcüğü. Normal ifadelerde kullanabileceğiniz hello sözdizimi tam bir açıklaması için bkz: [normal ifadeler toofilter günlük aramaları günlük analizi kullanarak](log-analytics-log-searches-regex.md).

Sözdizimi:

```
field:Regex("Regular Expression")
```

Örnek:

```
Computer:Regex("^C.*")
```

### <a name="logical-operators"></a>Mantıksal işleçler
Merhaba sorgu dilleri desteklemek hello mantıksal işleçler (*ve*, *veya*, ve *değil*) ve C tarzı benzersizse (*&&*,  *||* , ve *!*sırasıyla). Bu işleçlere parantez toogroup kullanabilirsiniz.

Örnekler:

```
system OR error

```

```
Type:Alert AND NOT(Severity:1 OR ObjectId:"8066bbc0-9ec8-ca83-1edc-6f30d4779bcb8066bbc0-9ec8-ca83-1edc-6f30d4779bcb")
```

Merhaba mantıksal işleç hello üst düzey filtre bağımsız değişkenler için atlayabilirsiniz. Bu durumda, hello AND işleci varsayılır.

| Filtre ifadesi | Eşdeğer çok|
| --- | --- |
| Sistem hatası |Sistem ve hata |
| Sistem "Windows Server" veya önem derecesi: 1 |Sistem ve ("Windows Server" veya önem derecesi: 1) |

### <a name="wildcarding"></a>Joker karakterler
Merhaba sorgu dili destekleyen hello kullanarak ( \* ) karakteri çok sorguda bir değer için bir veya daha fazla karakter temsil eder.

Örnek:

 Tüm bilgisayarlar "SQL" ile "Redmond-SQL" gibi hello adı bulabilirsiniz.

```
Type=Event Computer=*SQL*
```

> [!NOTE]
> Şu anda tırnak işaretleri joker karakterler kullanılamaz. Örneğin, selamlama iletisine `"*This text*"` hello göz önünde bulundurur (\*) sabit değer olarak kullanılan (\*) karakter.


## <a name="commands"></a>Komutlar


Merhaba komutlar hello sorgu tarafından döndürülen toohello sonuçları uygulanır. Kullanım hello dikey çizgi karakteri (|) tooapply komutu toohello sonuçları aldı. Birden çok komut hello dikey çizgi karakteriyle ayrılmış olması gerekir.

> [!NOTE]
> Komut adlarını büyük harflerle veya hello alan adları ve hello veri aksine, küçük harf yazılabilir.
>
>

### <a name="sort"></a>Sırala
Sözdizimi:

    sort field1 asc|desc, field2 asc|desc, …

Merhaba sonuçları belirli alanlara göre sıralar. artan veya azalan düzende hello asc/desc soneki toosort hello sonuçları isteğe bağlıdır. Belirtilmezse, hello *asc* sıralama düzeni varsayılır. Hello için **TimeGenerated** alanı *desc* sıralama düzeni varsayılır, varsayılan olarak hello en son sonuçları ilk döndürecek şekilde.

### <a name="toplimit"></a>Üst/sınırı
Sözdizimi:

    top number


    limit number
Sınırları yanıt toohello üst N sonuçları hello.

Örnek:

    Type:Alert errors detected | top 10

Eşleşen sonuçların ilk 10 döndürür hello.

### <a name="skip"></a>Atla
Sözdizimi:

    skip number

Atlar listelenen sonuç sayısı hello.

Örnek:

    Type:Alert errors detected | top 10 | skip 200

200 sonucunda başlangıç üst 10 eşleşen sonuç döndürür.

### <a name="select"></a>Şunu seçin:
Sözdizimi:

    select field1, field2, ...

Seçtiğiniz sonuçları toohello alanları sınırlar.

Örnek:

    Type:Alert errors detected | select Name, Severity

Sınırları hello döndürülen sonuçları alanları çok*adı* ve *önem*.

### <a name="measure"></a>Ölçü birimi
Merhaba *ölçü* kullanılan tooapply istatistik işlevleri toohello ham arama sonuçları bir komuttur. Bu çok yararlı tooget olan *grubu tarafından* görünümleri hello veriler üzerinde. Merhaba ölçü komutunu kullandığınızda, günlük analizi arama toplanmış sonuçlarını içeren bir tablo görüntüler.

**Sözdizimi:**

    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]] by groupField1 [, groupField2 [, groupField3]]  [interval interval]


    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]]  interval interval



Merhaba sonuçlarına göre toplayan *grup alanı*ve toplanan hello ölçü değerlerini kullanarak hesaplar *aggregatedField*.

| Ölçü istatistiksel işlevi | Açıklama |
| --- | --- |
| *aggregateFunction* |Merhaba adı hello toplama işlevinin (büyük küçük harfe duyarlı). Toplama işlevleri aşağıdaki hello desteklenir: COUNT, MAX, MIN, SUM, AVG, STDDEV, COUNTDISTINCT, yüzdebirlik ## veya PCT ## (## herhangi bir sayı 1 ile 99 arasında). |
| *aggregatedField* |toplanmakta hello alanı. Bu alan hello sayısı toplama işlevi için isteğe bağlıdır, ancak toobe SUM, MAX, MIN, AVG, STDDEV, yüzdebirlik ## veya PCT ## için varolan bir sayısal alana sahip (## herhangi bir sayı 1 ile 99 arasında). Merhaba aggregatedField de olabilir hello hiçbirini **Genişlet** işlevleri desteklenir. |
| *fieldAlias* |(isteğe bağlı) Hello hesaplanan hello için toplanan diğer ad değeri. Belirtilmezse, hello alan adıdır **AggregatedValue**. |
| *Grup alanı* |Merhaba hello sonuç kümesi hello alanın adını göre gruplandırılır. |
| *Aralığı* |Merhaba biçiminde Hello zaman aralığı:**nnnNAME**. **nnn**Merhaba pozitif bir tamsayı değil. **AD** hello aralığı adıdır. Desteklenen aralık adları büyük küçük harfe duyarlı bağlıdır ve şunları içerir: MİLİSANİYE [S] ikinci [S] DAKİKADA [S], saat [S] günü [S], [S] ay ve yıl [S]. |

Merhaba aralığı seçeneği yalnızca tarih/saat grubu alanlarında kullanılabilir (gibi *TimeGenerated* ve *TimeCreated*). Şu anda bu hello hizmeti tarafından zorlanmaz ancak toohello arka uç geçirilen tarih/saat olmayan bir alan bir çalışma zamanı hatası neden olur. Merhaba şema doğrulaması uygulandığında hello hizmeti API'si için aralığı toplama alanları tarih olmadan kullanan sorguları reddeder. Merhaba geçerli *ölçü* uygulaması herhangi bir toplama işlevi için aralığı gruplandırma destekler.

Merhaba BY yan tümcesi atlanırsa, ancak bir zaman aralığı (ikinci bir sözdizimi) belirtilmemişse, hello *TimeGenerated* alan varsayılan olarak kabul edilir.

Örnekler:

**Örnek 1**

    Type:Alert | measure count() as Count by ObjectId

Grupları uyarıları ile Merhaba *objectID*ve her grup için uyarıları hello sayısını hesaplar. Merhaba toplu değer hello döndürülür *sayısı* alan (diğer ad).

**Örnek 2**

    Type:Alert | measure count() interval 1HOUR

Grupları hello uyarıları 1 saat aralıklarına göre hello kullanarak *TimeGenerated* alan ve her aralığı içindeki uyarıları döndürür hello sayısı.

**Örnek 3**

    Type:Alert | measure count() as AlertsPerHour interval 1HOUR

Aynı hello önceki örnekte, ancak toplu alan diğer ad ile (*AlertsPerHour*).

**Örnek 4**

    * | Ölçü count() TimeCreated aralığı 5DAYS tarafından

Gruplar hello sonuçları 5 gün aralıklarına göre hello kullanarak *TimeCreated* alan ve her aralığı sonuçlarında hello sayısını döndürür.

**Örnek 5**

    Type:Alert | measure max(Severity) by WorkflowName

Grupları, iş yükü ada göre uyarıları hello ve her bir iş akışı için en fazla uyarı önem derecesi değeri döndürür hello.

**Örnek 6**

    Type:Alert | measure min(Severity) by WorkflowName

Aynı hello önceki örnek olarak, ancak hello *min* işlevi bir araya getirilir.

**Örnek 7**

    Type:Perf | measure avg(CounterValue) by Computer

Bilgisayar tarafından Perf grupları ve hello ortalama (Ort) hesaplar.

**Örnek 8**

    Type:Perf | measure sum(CounterValue) by Computer

Merhaba önceki örnekte, aynı ancak kullanan *toplam*.

**Örnek 9**

    Type:Perf | measure stddev(CounterValue) by Computer

Merhaba önceki örnekte, aynı ancak kullanan *stddev*.

**Örnek 10**

    Type:Perf | measure percentile70(CounterValue) by Computer

Merhaba önceki örnekte, aynı ancak kullanan *percentile70*.

**Örnek 11**

    Type:Perf | measure pct70(CounterValue) by Computer

Merhaba önceki örnekte, aynı ancak kullanan *pct70*. Unutmayın *PCT ##* yalnızca için diğer ad olduğu *yüzdebirlik ##* işlevi.

**Örnek 12**

    Type:Perf | measure avg(CounterValue) by Computer, CounterName

Perf ilk bilgisayar tarafından grupları ve ardından CounterName ve hello ortalama (Ort) hesaplar.

**Örnek 13**

    Type:Alert | measure count() as Count by WorkflowName | sort Count desc | top 5

Merhaba hello en fazla uyarı sayısı üst beş akışlarıyla alır.

**Örnek 14**

    * | countdistinct(Computer) türüne göre ölçün

Merhaba raporlama her türü için benzersiz bilgisayar sayısını sayar.

**Örnek 15**

    * | Ölçü countdistinct(Computer) aralığı 1 saat

Merhaba her saat için raporlama benzersiz bilgisayar sayısını sayar.

**Örnek 16**

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total” | measure avg(CounterValue) by Computer Interval 1HOUR
```

% İşlemci zamanı bilgisayara göre gruplandırır ve her saat için hello ortalamasını döndürür.

**Örnek 17**

    Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES

Yöntemi tarafından W3CIISLog grupları ve hello 5 dakikada en fazla döndürür.

**Örnek 18**

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer Interval 1HOUR
```

Bilgisayar ve döndürür hello minimum, ortalama, 75. yüzdebirlik ve her saat için üst sınır grupları % işlemci zamanı.

**Örnek 19**

```
Type:Perf CounterName=”% Processor Time”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer, InstanceName Interval 1HOUR
```

Grupları % işlemci zamanı ilk bilgisayar tarafından ardından örnek adını ve değerini döndürür hello en, ortalama, 75. yüzdebirlik ve her saat için üst sınır.

**Örnek 20**

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | measure max(product(CounterValue,60)) as MaxDWPerMin by InstanceName Interval 1HOUR
```

Bilgisayarınızda disk yazma işlemleri her disk için dakika başına Hello maksimum hesaplar.

### <a name="where"></a>Burada
Sözdizimi:

```
**where** AggregatedValue>20
```

Yalnızca sonra kullanılabilir bir *ölçü* komutu toofurther filtre hello toplanan sonuçları bu hello *ölçü* toplama işlevine üretilen.

Örnekler:

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) as MAXCPU by Computer

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) by Computer | where (AggregatedValue>50 and AggregatedValue<90)



### <a name="dedup"></a>Yinelenenleri kaldırma
Sözdizimi:

    Dedup FieldName

Alan verilen hello için her benzersiz değer bulundu hello ilk belgeyi döndürür.

Örnek:

    Type=Event | Dedup EventID | sort TimeGenerated DESC

Bu örnek olay kimliği başına bir olay (Merhaba son olay) döndürür.

### <a name="join"></a>Birleştir
Birleştirmeler hello sonuçları iki sorguları tooform tek bir sonuç kümesi.  Birden fazla birleştirme türü hello açıklanan destekler tablo izleyin.

| Katılım Türü | Açıklama |
|:--|:--|
| İç | Yalnızca kayıtları eşleşen değere sahip iki sorgularda döndür. |
| Dış | Tüm kayıtları hem sorgularından döndür.  |
| Sol  | Sol sorgu ve eşleşen kayıtları doğru sorgudan tüm kayıtları döndürür. |


- Birleştirmeler şu anda desteklemediği hello içeren sorgularını **IN** anahtar sözcüğü, hello **ölçü** komut veya hello **Genişlet** hello sağ sorgu alandan hedefler komutu.
- Bu gibi durumlarda, yalnızca tek bir alan şu anda bir birleştirme ekleyebilirsiniz.
- Tek bir arama birden fazla birleşim içermeyebilir.

**Sözdizimi**

```
<left-query> | JOIN <join-type> <left-query-field-name> (<right-query>) <right-query-field-name>
```

**Örnekler**

tooillustrate hello farklı birleştirme türü, bir veri türü birleştirme MyBackup_CL hello sinyal ile her bilgisayar için adlı özel bir günlük toplanan göz önünde bulundurun.  Bu veri türleri veri aşağıdaki hello vardır.

`Type = MyBackup_CL`

| TimeGenerated | Bilgisayar | LastBackupStatus |
|:---|:---|:---|
| 20/4/2017 01:26:32.137 AM | Srv01.contoso.com | Başarılı |
| 20/4/2017 02:13:12.381 AM | SRV02.contoso.com | Başarılı |
| 20/4/2017 02:13:12.381 AM | srv03.contoso.com | Hata |

`Type = Hearbeat`(Yalnızca bir alt kümesini gösterilen alanları)

| TimeGenerated | Bilgisayar | ComputerIP |
|:---|:---|:---|
| 21/4/2017 12:01:34.482 PM | Srv01.contoso.com | 10.10.100.1 |
| 21/4/2017 12:02:21.916 PM | SRV02.contoso.com | 10.10.100.2 |
| 21/4/2017 12:01:47.373 PM | srv04.contoso.com | 10.10.100.4 |

#### <a name="inner-join"></a>iç birleşim

`Type=MyBackup_CL | join inner Computer (Type=Heartbeat) Computer`

Aşağıdaki kayıtları hello bilgisayar alanı hem de veri türleri için eşleştiği hello döndürür.

| Bilgisayar| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| Srv01.contoso.com | 20/4/2017 01:26:32.137 AM | Başarılı | 21/4/2017 12:01:34.482 PM | 10.10.100.1 | Sinyal |
| SRV02.contoso.com | 20/4/2017 02:13:12.381 AM | Başarılı | 21/4/2017 12:02:21.916 PM | 10.10.100.2 | Sinyal |


#### <a name="outer-join"></a>dış birleşim

`Type=MyBackup_CL | join outer Computer (Type=Heartbeat) Computer`

Aşağıdaki her iki veri türleri için kayıtları hello döndürür.

| Bilgisayar| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| Srv01.contoso.com | 20/4/2017 01:26:32.137 AM | Başarılı  | 21/4/2017 12:01:34.482 PM | 10.10.100.1 | Sinyal |
| SRV02.contoso.com | 20/4/2017 02:14:12.381 AM | Başarılı  | 21/4/2017 12:02:21.916 PM | 10.10.100.2 | Sinyal |
| srv03.contoso.com | 20/4/2017 01:33:35.974 AM | Hata  | 21/4/2017 12:01:47.373 PM | | |
| srv04.contoso.com |                           |          | 21/4/2017 12:01:47.373 PM | 10.10.100.2 | Sinyal |



#### <a name="left-join"></a>Sol birleştirme

`Type=MyBackup_CL | join left Computer (Type=Heartbeat) Computer`

Merhaba MyBackup_CL sinyal eşleşen tüm alanları ile aşağıdaki kayıtları döndürür.

| Bilgisayar| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| Srv01.contoso.com | 20/4/2017 01:26:32.137 AM | Başarılı | 21/4/2017 12:01:34.482 PM | 10.10.100.1 | Sinyal |
| SRV02.contoso.com | 20/4/2017 02:13:12.381 AM | Başarılı | 21/4/2017 12:02:21.916 PM | 10.10.100.2 | Sinyal |
| srv03.contoso.com | 20/4/2017 02:13:12.381 AM | Hata | | | |


### <a name="extend"></a>Genişletme
Sorgularda toocreate çalışma zamanı alanları sağlar. Çalışma zamanı alanlar hello ölçü komutu tooperform toplama kullanılamaz unutmayın.

**Örnek 1**

    Type=SQLAssessmentRecommendation | Extend product(RecommendationScore, RecommendationWeight) AS RecommendationWeightedScore
Gösterir SQL değerlendirmesi önerileri için öneri puan ağırlıklı.

**Örnek 2**

    Type=Perf CounterName="Private Bytes" | EXTEND div(CounterValue,1024) AS KBs | Select CounterValue,Computer,KBs
Sayaç değeri içinde KB yerine bayt gösterir.

**Örnek 3**

    Type=WireData | EXTEND scale(TotalBytes,0,100) AS ScaledTotalBytes | Select ScaledTotalBytes,TotalBytes | SORT TotalBytes DESC
Tüm sonuçları 0 ile 100 arasında olduğu şekilde ölçekler WireData TotalBytes değerini hello.

**Örnek 4**

```
Type=Perf CounterName="% Processor Time" | EXTEND if(map(CounterValue,0,50,0,1),"HIGH","LOW") as UTILIZATION
```
Yüzde 50 olarak düşük ve diğerleri olarak yüksek değerinden performans sayacı değerlerini etiketler.

**Örnek 5**

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | Extend product(CounterValue,60) as DWPerMin| measure max(DWPerMin) by InstanceName Interval 1HOUR
```
Bilgisayarınızda disk yazma işlemleri her disk için dakika başına Hello maksimum hesaplar.

**Desteklenen işlevler**

| İşlevi | Açıklama | Sözdizimi örnekleri |
| --- | --- | --- |
| Abs |Belirtilen değer veya işlevi hello hello mutlak değeri döndürür. |`abs(x)` <br> `abs(-5)` |
| ACOS |Bir değer veya bir işlev ARC kosinüsünü döndürür. |`acos(x)` |
| ve |Tüm işlenenleri tootrue değerlendirmek ve yalnızca, true değerini döndürür. |`and(not(exists(popularity)),exists(price))` |
| asin |Bir değer veya bir işlev ARC sinüsünü döndürür. |`asin(x)` |
| atan |Bir değer veya bir işlev ARC tanjantını döndürür. |`atan(x)` |
| ATAN2 |Merhaba dikdörtgen koordinatları x, y toopolar koordinatları hello dönüştürülmesi kaynaklanan hello açıyı döndürür. |`atan2(x,y)` |
| cbrt |Küp kökü. |`cbrt(x)` |
| ceil |Tooan tamsayı yukarı yuvarlar. |`ceil(x)`  <br> `ceil(5.6)`6'yı döndürür |
| cos |Bir açının kosinüsünü döndürür. |`cos(x)` |
| COSH |Bir açının hiperbolik kosinüsünü döndürür. |`cosh(x)` |
| def |Varsayılan kısaltması. Alan "alanını" değerini döndürür hello. Merhaba alanı mevcut değilse, belirtilen hello varsayılan değerini döndürür ve hello ilk değer verir nerede: `exists()==true`. |`def(rating,5)`. Bu def() işlevi hello derecelendirme döndürür veya derecelendirmesi hello belgede belirtilmişse, 5 döndürür. <br> `def(myfield, 1.0)`çok eşdeğerdir`if(exists(myfield),myfield,1.0)`. |
| derece |Radyan cinsinden toodegrees dönüştürür. |`deg(x)` |
| div |`div(x,y)`böler y x. |`div(1,y)` <br> `div(sum(x,100),max(y,1))` |
| Dağıtım |İki vektörüne (nokta) n boyutlu bir alanda arasında Hello uzaklığını döndürür. Merhaba güç artı iki veya daha çok, ValueSource örneği alır ve hello iki vektör arasındaki hello uzaklıkları hesaplar. Her ValueSource bir sayı olmalıdır. Geçirilen ValueSource örneklerinin bir çift sayı olmalıdır ve hello yöntemi hello ilk yarı hello ilk vektör temsil eder ve hello ikinci yarısındaki temsil hello ikinci vektör varsayar. |`dist(2, x, y, 0, 0)`(0,0) arasındaki Hello Euclidean uzaklığı hesaplar ve (x, y) her belge için. <br> `dist(1, x, y, 0, 0)`(0,0) arasındaki Hello Manhattan (taxicab) uzaklığı hesaplar ve (x, y) her belge için. <br> `dist(2,,x,y,z,0,0,0)`(0,0,0) arasındaki Euclidean uzaklığı ve (x, y, z) her belge için.<br>`dist(1,x,y,z,e,f,g)`Arasındaki Manhattan uzaklığı (x, y, z) ve (e, f, g), burada her harf, bir alan adı. |
| var |Merhaba alan varsa TRUE üyesi döndürür bulunmaktadır. |`exists(author)`Merhaba "Yazar" alanda bir değere sahip herhangi bir belgeyi TRUE döndürür.<br>`exists(query(price:5.00))`"Fiyat" eşleşirse, TRUE döndürür "5.00". |
| exp |Döndürür Euler'ın sayının yükseltildiği toopower x. |`exp(x)` |
| Kat |Tooan tamsayı aşağı yuvarlar. |`floor(x)`  <br> `floor(5.6)`5 döndürür |
| hypo |Ara taşması veya underflow olmadan Sqrt(SUM(pow(x,2),pow(y,2))) döndürür. |`hypo(x,y)`  <br> ` |
| Eğer |Koşullu işlevi sorguları sağlar. İçinde `if(test,value1,value2)`, test olduğu veya tooa mantıksal bir değer veya bir mantıksal bir değer (TRUE veya FALSE) döndüren ifadesini gösterir. `value1`Merhaba değeri, test TRUE verir durumunda hello işlevi tarafından döndürülür. `value2`Merhaba değeri, test FALSE verir durumunda hello işlevi tarafından döndürülür. Bir ifade, Boole değerleri çıkarır herhangi bir işlev olabilir. Ayrıca, durum değeri 0 false olarak yorumlanır veya dizeler, döndürme case hangi boş dize false olarak yorumlanır sayısal değerler döndüren bir işlev olabilir. |`if(termfreq(cat,'electronics'),popularity,42)`Merhaba terimi "elektronik" Merhaba kat alanında içeriyorsa, bu işlev her belge toosee denetler. Ardından Merhaba hello popülerliği alanının değeri döndürülür. Aksi takdirde, 42 hello değeri döndürülür. |
| Doğrusal |Implements `m*x+c`, burada m ve c sabitleri ve x, rasgele bir işlev. Bu çok eşdeğerdir`sum(product(m,x),c)`, ancak tek bir işlevi uygulanan biraz daha verimlidir. |`linear(x,m,c) linear(x,2,4)`döndürür`2*x+4` |
| ln |Döndürür hello doğal günlüğünü hello işlevi belirtilmiş. |`ln(x)` |
| Günlük |Döndürür hello günlük hello temel 10 belirtilen işlevi. |`log(x)   log(sum(x,100))` |
| eşleme |Min ve max ve kapsamlı toohello belirtilen hedef içinde kalan herhangi bir giriş işlevi x değerleri eşler. Merhaba bağımsız değişkenleri min ve Mak olmalıdır. Merhaba bağımsız değişken hedef ve varsayılan sabitler veya İşlevler olabilir. X değerini Hello min ve max arasında uymazsa sonra ya da x hello değeri döndürülür veya 5 bağımsız değişkeni olarak belirtilen bir varsayılan değeri döndürülür. |`map(x,min,max,target) map(x,0,0,1)`0 too1 tüm değerleri değiştirir. Bu, varsayılan 0 değerleri işleme yararlı olabilir.<br> `map(x,min,max,target,default)    map(x,0,100,1,-1)`0 ile 100 too1 ve tüm diğer değerleri çok-1 arasında herhangi bir değeri değiştirir.<br>  `map(x,0,100,sum(x,599),docfreq(text,solr))`Tüm değerleri 0 ile 100 toox arasında + 599 ve diğer tüm değerler toofrequency hello döneminin 'solr' hello alan metin değiştirir. |
| max |Merhaba, birden çok iç içe geçmiş işlevler veya bağımsız değişken olarak belirtilmiş sabitleri en büyük sayısal değeri döndürür: `max(x,y,...)`. Bazı alan sabiti belirtilen veya Hello max işlevi de "başka bir işlev bottoming" için yararlı olabilir.  Kullanım hello `field(myfield,max)` tek değerli bir alanı en büyük değerini hello seçmek için sözdizimi. |`max(myfield,myotherfield,0)` |
| dk |Merhaba bağımsız değişken olarak belirtilmiş sabitlerin birden çok iç içe geçmiş işlevler en küçük sayısal değeri döndürür: `min(x,y,...)`. Merhaba min işlevi de "üst sınırı" bir sabit kullanarak bir işlev sağlamak için yararlı olabilir. Kullanım hello `field(myfield,min)` hello en küçük değeri tek değerli bir alanı seçmek için sözdizimi. |`min(myfield,myotherfield,0)` |
| mod |Merhaba modulus hello işlevi y tarafından x hello işlevinin hesaplar. |`mod(1,x)` <br> `mod(sum(x,100), max(y,1))` |
| MS |Bağımsız değişkenler arasındaki farkı milisaniye olarak döndürür. Tarih saat dönem, gece yarısı, 1 Ocak 1970 UTC göreli toohello UNIX ya da POSIX var. Bağımsız değişkenler bir dizinlenmiş TrieDateField ya da sabit tarih temelli tarih matematik hello adı olması veya artık olabilir. `ms()`çok eşdeğerdir`ms(NOW)`, hello dönem itibaren milisaniye sayısı. `ms(a)`Merhaba bağımsız değişkeni temsil eden hello dönem itibaren Hello milisaniye sayısını döndürür. `ms(a,b)`Bu b Hello milisaniye sayısını döndürür önce oluşur olduğu `a - b`. |`ms(NOW/DAY)`<br>`ms(2000-01-01T00:00:00Z)`<br>`ms(mydatefield)`<br>`ms(NOW,mydatefield)`<br>`ms(mydatefield,2000-01-01T00:00:00Z)`<br>`ms(datefield1,datefield2)` |
| değil |Merhaba mantıksal olarak tasarruflarını hello değerini işlevi sarılır. |`not(exists(author))`Yalnızca TRUE olduğunda `exists(author)` false olur. |
| or |Mantıksal ayrım. |`or(value1,value2)`TRUE ya da value1 veya value2 doğrudur. |
| POW |Belirtilen temel toohello başlatır hello belirtilen güç. `pow(x,y)`y x toohello gücünü başlatır. |`pow(x,y)`<br>`pow(x,log(y))`<br>`pow(x,0.5)`aynı sqrt hello. |
| Ürün |Birden çok değerleri veya virgülle ayrılmış bir listede belirtilen İşlevler, ürünün döndürür hello. `mul(...)`Ayrıca bir diğer ad olarak bu işlev için kullanılabilir. |`product(x,y,...)`<br>`product(x,2)`<br>`product(x,y)`<br>`mul(x,y)` |
| Alıcı |İle karşılıklı bir işlev gerçekleştirir `recip(x,m,a,b)` uygulama `a/(m*x+b)`, burada m, a, b olan sabitleri ve x, herhangi bir rastgele karmaşık işlev. Zaman bir ve b eşittir ve x > = 0, bu işlev bir maksimum değer olarak artar x bırakır 1 sahiptir. Merhaba değerini artırmayı bir ve b birlikte hello tüm işlevi tooa hareketini sonuçlarında daha düz hello eğri parçası. Bu özellikler bu x olduğunda daha yeni belgeleri artırmanın için ideal bir işlev yapabilirsiniz `rord(datefield)`. |`recip(myfield,m,a,b)`<br>`recip(rord(creationDate),1,1000,1000)` |
| RAD |Derece tooradians dönüştürür. |`rad(x)` |
| Yazdır |Tamsayı en yakın toohello yuvarlar. |`rint(x)`  <br> `rint(5.6)`6'yı döndürür |
| sin |Bir açının sinüsünü döndürür. |`sin(x)` |
| SİNH |Bir açının hiperbolik sinüsünü döndürür. |`sinh(x)` |
| Ölçek |Ölçek değerleri x hello işlevinin hello arasında kalmıyor gibi minTarget ve maxTarget (bunlar dahil) belirtti. Merhaba doğru ölçek seçebilirsiniz şekilde hello geçerli uygulama tüm hello işlevi değerleri tooobtain hello min ve Mak erişir. Merhaba geçerli uygulaması'nın olamaz ayırt etmek belgeleri sildikten sonra ya da herhangi bir değer olan belgeler. Bu durumlarda 0.0 değerleri kullanır. Bu değerler normalde 0. 0 ' tüm büyük ise, bir hala 0,0 ile en küçük değer toomap gelen hello olarak düşebilir olduğunu anlamına gelir. Bu durumda, uygun bir `map()` işlevi kullanılabilirdi hello gerçek aralığındaki bir geçici çözüm toochange 0,0 tooa değeri olarak aşağıda gösterildiği gibi:`scale(map(x,0,0,5),1,2)` |`scale(x,minTarget,maxTarget)`<br>`scale(x,1,2)`Tüm 1 ve 2 (bunlar dahil) arasında değerler şekilde ölçekler x değerleri hello. |
| Sqrt |Belirtilen değer veya işlevi hello hello kare kökünü döndürür. |`sqrt(x)`<br>`sqrt(100)`<br>`sqrt(sum(x,100))` |
| strdist |İki dizeyi arasındaki Hello uzaklığı hesaplar. Merhaba Lucene yazım denetleyicisi StringDistance arabirimini kullanır ve tüm bu pakette hello uygulamaları destekler. Ayrıca uygulamalar tooplug kendi Solr'ın kaynak aracılığıyla yükleme özellikleri sağlar. strdist geçen `(string1, string2, distance measure)`. Uzaklık ölçü için olası değerler şunlardır:<ul><li>jw: Jaro Winkler</li><li>Düzenle: Levenstein veya düzenleme uzaklığı</li><li>ngram: Merhaba NGramDistance, belirtilmişse, isteğe bağlı olarak iletebilir hello ngram boyutu çok. Varsayılan 2'dir.</li><li>FQN: Sınıf adı hello StringDistance arabirimi bir uygulama için tam. Hayır arg oluşturucuya sahip olmalıdır.</li></ul> |`strdist("SOLR",id,edit)` |
| Sub |X-y döndürür `sub(x,y)`. |`sub(myfield,myfield2)`<br>`sub(100,sqrt(myfield))` |
| TOPLA |Birden çok değerler veya virgülle ayrılmış bir listede belirtilen işlevler toplamını döndürür hello. `add(...)`Bu işlev için bir diğer ad olarak kullanılabilir. |`sum(x,y,...)`<br>`sum(x,1)`<br>`sum(x,y)`<br>`sum(sqrt(x),log(y),z,0.5)`<br>`add(x,y)` |
| termfreq |Bu belge için hello alanında hello terim görünür kez Hello sayısını döndürür. |termfreq(Text,'memory') |
| tan |Bir açının tanjantını döndürür. |`tan(x)` |
| TANH |Bir açının hiperbolik tanjantını döndürür. |`tanh(x)` |

## <a name="search-field-and-facet-reference"></a>Arama alanı ve modeli başvurusu
Günlük arama toofind veri kullandığınızda, sonuçlar çeşitli alan ve modelleri görüntüler. Merhaba bilgi bir bölümü çok açıklayıcı görünmeyebilir. Merhaba sonuçlar anlamak bilgi toohelp aşağıdaki hello kullanın.

| Alan | Arama türü | Açıklama |
| --- | --- | --- |
| Tenantıd |Tümü |Toopartition veri kullanılır. |
| TimeGenerated |Tümü |Toodrive hello zaman çizelgesi, timeselectors (arama ve diğer ekranlar) kullanılır. Veri Hello parçası (genellikle hello aracısında) oluşturulduğunda temsil eder. Başlangıç saati ISO biçiminde ifade edilir ve her zaman UTC. Varolan Araçları'nı (diğer bir deyişle, olay günlüğü'ndeki) temel alan türlerinin Hello durumda da, bu genellikle hello bu hello günlük girişi/satır/kaydı günlüğe gerçek zaman olur. Merhaba bazıları için yönetim paketleri aracılığıyla veya hello bulutta (örneğin, önerileri veya Uyarıları) üretilen diğer türleri hello saati gösteren bir şey farklı. Bu zaman bu yeni veri parçası çeşit yapılandırmanın bir anlık görüntüsünü ile toplanan veya bir öneri/Uyarısı, göre üretilmiştir hello zamandır. |
| Olay Kimliği |Olay |Merhaba Windows olay günlüğünde olay kimliği. |
| Olay günlüğü |Olay |Olay günlüğü hello olay Windows tarafından burada günlüğe kaydedildi. |
| EventLevelName |Olay |Kritik/Uyarı/bilgi/başarılı |
| eventLevel |Olay |Kritik/Uyarı/bilgi/başarı ilişkin sayısal değer (EventLevelName daha kolay/daha okunabilir sorgular için bunun yerine kullanın). |
| SourceSystem |Tümü |Merhaba veri nereden geldiğini (cinsinden modu toohello hizmeti eklemek). Örnek Microsoft System Center Operations Manager ve Azure Storage verilebilir. |
| ObjectName |PerfHourly |Windows performans nesnesi adı. |
| InstanceName |PerfHourly |Windows performans sayacı örneği adı. |
| CounteName |PerfHourly |Windows performans sayacı adı. |
| ObjectDisplayName |PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty |Operations Manager bir performans toplama kuralı tarafından hedeflenen hello nesnesinin görünen adı. Merhaba, nesnenin görünen adını operasyonel Öngörüler tarafından bulunan hello de olabilir veya hangi hello karşı uyarı oluşturuldu. |
| RootObjectName |PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty |Merhaba üst hello üstünün (çift bir barındırma ilişkisi) Operations Manager bir performans toplama kuralı tarafından hedeflenen hello nesnesinin görünen adı. Merhaba, nesnenin görünen adını operasyonel Öngörüler tarafından bulunan hello de olabilir veya hangi hello karşı uyarı oluşturuldu. |
| Bilgisayar |Çoğu türleri |Merhaba veri ait olduğu bilgisayar adı. |
| DeviceName |ProtectionStatus |Bilgisayar adı hello veri ait çok (aynı "Bilgisayar"). |
| DetectionId |ProtectionStatus | |
| ThreatStatusRank |ProtectionStatus |Tehdit durum derece hello tehdit durum sayısal bir gösterimi ' dir. Benzer tooHTTP yanıt kodları hello derecelendirme sahip hello sayılar arasında boşluk (herhangi bir tehdit neden olduğu 150 ve değil 100 veya 0 değil), yer tooadd yeni durum çıkılıyor. İş parçacığı durumu ve koruma durumu toplu için bilgisayar hello tooshow hello en kötü durumu süre seçili hello sırasında düzeltilme hello amacınıza paketidir. Merhaba yüksek numarasıyla hello kaydı görebilecekleri hello sayıları farklı durumlara hello rank. |
| ThreatStatus |ProtectionStatus |ThreatStatus, açıklaması, 1:1 ThreatStatusRank ile eşler. |
| TypeofProtection |ProtectionStatus |Merhaba bilgisayarda Algılanan kötü amaçlı yazılımdan koruma ürün: none, Microsoft kötü amaçlı yazılım kaldırma aracını, Forefront ve benzeri. |
| ComputerName |ProtectionStatus | |
| SourceHealthServiceId |ProtectionStatus, RequiredUpdate |Bu bilgisayarın aracı için sistem sağlığı hizmeti kimliği. |
| HealthServiceId |Çoğu türleri |Bu bilgisayarın aracı için sistem sağlığı hizmeti kimliği. |
| ManagementGroupName |Çoğu türleri |Operations Manager bağlı aracılar için yönetim grubu adı. Aksi takdirde, null/boş olur. |
| ObjectType |ConfigurationObject |Günlük analizi yapılandırması değerlendirme tarafından bulunan bu nesne için (Operations Manager Yönetim Paketi türü/sınıfı olduğu gibi) yazın. |
| UpdateTitle |RequiredUpdate |Yüklü bulunamadı hello güncelleştirme adı. |
| PublishDate |RequiredUpdate |Ne zaman hello güncelleştirme Microsoft Update sitesinde yayımlandı. |
| Sunucu |RequiredUpdate |Bilgisayar adı hello veri ait çok (aynı "Bilgisayar"). |
| Ürün |RequiredUpdate |Güncelleştirme hello ürün için geçerlidir. |
| UpdateClassification |RequiredUpdate |Güncelleştirme (örneğin, güncelleştirme paketi veya hizmet paketi) türü. |
| KBID |RequiredUpdate |Bu en iyi yöntem veya güncelleştirmeyi açıklayan KB makalesi kimliği. |
| WorkflowName |ConfigurationAlert |Merhaba kural veya hello uyarı üretilen İzleyici adı. |
| Önem Derecesi |ConfigurationAlert |Uyarının önem derecesini hello. |
| Öncelik |ConfigurationAlert |Merhaba uyarı önceliği. |
| IsMonitorAlert |ConfigurationAlert |Bu uyarı bir izleyici (true) veya bir kural (false) tarafından oluşturulur? |
| AlertParameters |ConfigurationAlert |XML hello günlük analizi uyarının hello parametrelere sahip. |
| Bağlam |ConfigurationAlert |XML hello günlük analizi uyarı Merhaba içeriğine sahip. |
| İş yükü |ConfigurationAlert |Teknoloji veya uyarı hello iş yükü başvuruyor. |
| AdvisorWorkload |Öneri |Teknoloji veya öneri hello iş yükü başvuruyor. |
| Açıklama |ConfigurationAlert |Uyarı açıklaması (kısa). |
| DaysSinceLastUpdate |UpdateAgent |Kaç gün önce (Bu kaydın göreli tooTimeGenerated) bu aracının herhangi bir güncelleştirme Windows Server Update Service (WSUS) veya Microsoft Update yüklediniz mi? |
| DaysSinceLastUpdateBucket |UpdateAgent |DaysSinceLastUpdate, kategori, ne kadar zaman önce bir bilgisayar son herhangi bir güncelleştirme WSUS/Microsoft Update sitesinden yüklenen zaman demet içinde temel. |
| AutomaticUpdateEnabled |UpdateAgent |Otomatik Güncelleştirme denetimi etkinleştirildiğini veya bu Aracısı'nı devre dışı? |
| AutomaticUpdateValue |UpdateAgent |Otomatik Güncelleştirme denetimi kümesi tooautomatically indirilir ve yükleme, yalnızca yükleyin veya yalnızca denetle? |
| WindowsUpdateAgentVersion |UpdateAgent |Merhaba Microsoft Update Aracı sürüm numarası. |
| WSUSServer |UpdateAgent |Hangi WSUS sunucusu, bu güncelleştirme Aracısı hedeflediği? |
| OSVersion |UpdateAgent |Bu güncelleştirme Aracısı çalışan hello işletim sistemi sürümü. |
| Ad |Öneri, ConfigurationObjectProperty |Ad/başlığı hello öneri ya da günlük analizi yapılandırması değerlendirme hello özelliğinin adı. |
| Değer |ConfigurationObjectProperty |Günlük analizi yapılandırması değerlendirme özelliğinden değeri. |
| KBLink |Öneri |Bu en iyi uygulama veya güncelleştirme açıklayan URL toohello KB makalesi. |
| RecommendationStatus |Öneri |Öneriler arasında hello güncelleştirilmiş, yeni eklenen toohello arama dizini kayıtlarını almak birkaç türleridir. Bu durum hello öneri etkin/açık olup olmadığını veya günlük analizi çözümlendiğini doğrulamaktadır algılarsa değiştirir. |
| RenderedDescription |Olay |Bir Windows olayı (doldurulmuş parametrelerle yeniden kullanılan metin) açıklaması çizilir. |
| ParameterXml |Olay |XML (Olay Görüntüleyicisi'nde görüldüğü gibi) bir Windows olayı hello veri bölümünde hello parametrelere sahip. |
| EventData |Olay |XML ile Windows (Olay Görüntüleyicisi'nde görüldüğü gibi) olay hello tüm veri bölümü. |
| Kaynak |Olay |Merhaba olayı oluşturan olay günlüğü kaynağı. |
| EventCategory |Olay |Doğrudan hello Windows olay günlüğünden hello olay kategorisi. |
| Kullanıcı adı |Olay |Merhaba Windows olay (genellikle, NT AUTHORITY\LOCALSYSTEM) kullanıcı adı. |
| Görüntülendiğinden |PerfHourly |Merhaba saatlik toplama, bir performans sayacının ortalama değeri. |
| Min |PerfHourly |Bir performans sayacı saatlik toplama hello saatlik aralığı en düşük değer. |
| Maks. |PerfHourly |Bir performans sayacı saatlik toplama hello saatlik aralığı en büyük değeri. |
| Percentile95 |PerfHourly |Merhaba 95 yüzdelik değer için bir performans sayacı saatlik toplama hello saatlik aralığı. |
| SampleCount |PerfHourly |Kaç tane ham performans sayacı örneklerinin kullanılan tooproduce bu saatlik olan kayıt toplama. |
| Tehdit |ProtectionStatus |Kötü amaçlı yazılım bulundu adı. |
| StorageAccount |W3CIISLog |Azure depolama hesabı hello günlük gelen okundu. |
| AzureDeploymentID |W3CIISLog |Azure dağıtım kimliği hello bulut hizmeti hello günlüğünün ait. |
| Rol |W3CIISLog |Rol hello Azure bulut hizmeti hello günlüğünün ait. |
| RoleInstance |W3CIISLog |Merhaba günlük hello Azure rol RoleInstance ait. |
| sSiteName |W3CIISLog |Günlük hello IIS Web sitesi too(metabase notation) ait; s-sitename alanında hello özgün günlük Hello. |
| sComputerName |W3CIISLog |s-computername alanında hello özgün günlük Hello. |
| SIP |W3CIISLog |Sunucu IP adresi hello HTTP isteği için giderilmiştir. s-ip alanında hello özgün günlük Hello. |
| csMethod |W3CIISLog |Merhaba HTTP isteği hello istemci tarafından kullanılan HTTP yöntemini (örneğin, GET/POST). Merhaba cs-yöntem hello özgün günlük. |
| CIP |W3CIISLog |İstemci IP adresi hello HTTP isteği geldi. c-ip alanında hello özgün günlük Hello. |
| csUserAgent |W3CIISLog |HTTP User-Agent hello istemci tarafından bildirilen (tarayıcı veya aksi halde). cs-user-agent hello özgün günlüğünde hello. |
| scStatus |W3CIISLog |Merhaba sunucu toohello istemci tarafından döndürülen HTTP durum kodu (örneğin, 200/403/500). Merhaba cs-durumu hello özgün günlüğünde. |
| TimeTaken |W3CIISLog |Ne kadar süre (milisaniye cinsinden) toocomplete bu hello isteği aldı. Merhaba özgün günlük Hello timetaken alanı. |
| csUriStem |W3CIISLog |Göreli URI (ana bilgisayar adresi olmadan, / arama) işlemi istendi. Merhaba özgün günlük Hello cs bulunamadı.%n alanı. |
| csUriQuery |W3CIISLog |URI sorgusu. Bu alan bir tire statik sayfaları için genellikle içerecek şekilde URI sorgular yalnızca ASP sayfalarının gibi dinamik sayfalar için gereklidir. |
| Spor |W3CIISLog |HTTP isteği hello sunucu bağlantı noktası çok gönderildiği (ve bu toplanma beri için IIS'in dinler). |
| csUserName |W3CIISLog |Merhaba istek kimliği doğrulanmış ve değil anonim ise kullanıcı adı kimlik doğrulaması. |
| csVersion |W3CIISLog |(Örneğin, HTTP/1.1) Hello istekte kullanılan HTTP protokolü sürümü. |
| csCookie |W3CIISLog |Tanımlama bilgileri. |
| csReferer |W3CIISLog |Son ziyaret hello kullanıcı site. Bu site bağlantı toohello geçerli site sağladı. |
| csHost |W3CIISLog |İstenen ana bilgisayar üst bilgisi (örneğin, www.mysite.com). |
| scSubStatus |W3CIISLog |Alt durum hata kodu. |
| scWin32Status |W3CIISLog |Windows durum kodu. |
| csBytes |W3CIISLog |Merhaba istekte hello istemci toohello sunucusundan gönderilen bayt sayısı. |
| scBytes |W3CIISLog |Bayt geri hello sunucu toohello istemciden hello yanıt döndürdü. |
| ConfigChangeType |ConfigurationChange |Değişiklik (örneğin, WindowsServices/yazılım) türü. |
| ChangeCategory |ConfigurationChange |Merhaba değişiklik (değiştirilen/eklenen/kaldırıldı) kategorisi. |
| SoftwareType |ConfigurationChange |Yazılım (güncelleştirme/uygulama) türü. |
| SoftwareName |ConfigurationChange |Merhaba yazılım (yalnızca geçerli toosoftware değişiklikler) adı. |
| Yayımcı |ConfigurationChange |Merhaba yazılım (yalnızca geçerli toosoftware değişiklikler) yayımlar satıcı. |
| SvcChangeType |ConfigurationChange |Bir Windows hizmeti (durumu/StartupType/yol/HizmetHesabı) uygulandı değişiklik türü. Yalnızca geçerli tooWindows hizmet değişikliklerini budur. |
| SvcDisplayName |ConfigurationChange |Değiştirilen hello hizmet görünen adı. |
| SvcName |ConfigurationChange |Değiştirilen hello hizmetin adı. |
| SvcState |ConfigurationChange |Merhaba hizmeti yeni (geçerli) durumu. |
| SvcPreviousState |ConfigurationChange |(Yalnızca hizmet durumu değişirse geçerlidir) hello hizmetinin durumunu bilinen önceki. |
| SvcStartupType |ConfigurationChange |Hizmet başlangıç türü. |
| SvcPreviousStartupType |ConfigurationChange |Önceki hizmet başlatma türünü (yalnızca hizmet başlatma türünü değiştirdiyseniz geçerlidir). |
| SvcAccount |ConfigurationChange |Hizmet hesabı. |
| SvcPreviousAccount |ConfigurationChange |Önceki hizmet hesabı (yalnızca hizmet hesabı değiştirdiyseniz geçerlidir). |
| SvcPath |ConfigurationChange |Merhaba Windows hizmetinin yolu toohello yürütülebilir. |
| SvcPreviousPath |ConfigurationChange |Merhaba hello (yalnızca onu değiştirdiyseniz geçerlidir) Windows hizmeti için yürütülebilir önceki yolu. |
| SvcDescription |ConfigurationChange |Merhaba hizmet açıklaması. |
| Önceki |ConfigurationChange |Bu yazılımı (yüklü/değil yüklü/önceki sürüm) önceki durumu. |
| Geçerli |ConfigurationChange |Son durum bu yazılımın (yüklü/değil yüklü/geçerli sürüm). |

## <a name="next-steps"></a>Sonraki adımlar
Günlük aramaları hakkında ek bilgi için:

* İle tanışın [oturum aramaları](log-analytics-log-searches.md) tooview ayrıntılı çözümler tarafından toplanan bilgiler.
* Kullanım [günlük analizi içinde özel alanlar](log-analytics-custom-fields.md) tooextend günlük arar.
