---
title: "aaaScheduling ve Data Factory ile yürütme | Microsoft Docs"
description: "Azure Data Factory uygulama modelinin zamanlama ve yürütme yönleri hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 088a83df-4d1b-4ac1-afb3-0787a9bd1ca5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 6114dd4896f5537c789c3b632fb90e501b694285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-factory-scheduling-and-execution"></a>Veri Fabrikası zamanlama ve yürütme
Bu makalede hello hello Azure Data Factory uygulama modelinin zamanlama ve yürütme yönleri açıklanmaktadır. Bu makalede, etkinlik, ardışık düzen, bağlı hizmetler ve veri kümeleri dahil olmak üzere, veri fabrikası uygulama modeli kavramlarını temelleri anladığınızı varsayar. Azure Data Factory temel kavramları makaleler hello bakın:

* [Giriş tooData Fabrika](data-factory-introduction.md)
* [İşlem hatları](data-factory-create-pipelines.md)
* [Veri kümeleri](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a>Başlangıç ve bitiş zamanlarını ardışık
İşlem hattı yalnızca arasında etkin olduğu kendi **Başlat** zaman ve **son** saat. Bunu hello başlangıç saatinden önce veya sonra hello bitiş saati yürütülmedi. Merhaba ardışık düzen duraklatıldığında, kendi başlangıç ve bitiş zamanı bağımsız olarak yürütülemiyor. Ardışık Düzen toorun için bunu duraklatılması değil. Bu ayarları (Başlangıç, son, duraklatıldı) hello ardışık düzen tanımında bulun: 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

Bu özellikleri daha fazla bilgi için bkz: [işlem hatlarını oluşturmak](data-factory-create-pipelines.md) makalesi. 


## <a name="specify-schedule-for-an-activity"></a>Bir etkinlik için zamanlamayı belirtin
Yürütülen hello ardışık düzen değil. Hello yürütülen hello ardışık düzendeki hello etkinlik olduğu hello ardışık genel bağlam. Hello kullanarak bir etkinlik için yinelenen bir zamanlama belirtebilirsiniz **Zamanlayıcı** JSON etkinliği bölümü. Örneğin, bir etkinlik toorun saatlik şu şekilde zamanlayabilirsiniz:  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

Hello Aşağıdaki diyagramda gösterildiği gibi hello dönen windows ile birlikte bir dizi etkinlik için bir zamanlama oluşturur belirtme kanal başlangıç ve bitiş saatlerini. Dönen windows sabit boyutlu çakışmayan, bitişik zaman aralıkları bir dizi var. Bir etkinlik için bu mantıksal dönen windows adlı **etkinlik windows**.

![Etkinlik Zamanlayıcısı örneği](media/data-factory-scheduling-and-execution/scheduler-example.png)

Merhaba **Zamanlayıcı** özelliği bir etkinlik için isteğe bağlı. Bu özelliği belirtirseniz, hello tanımında hello etkinliğinin çıkış veri kümesi, belirttiğiniz hello tempoyla eşleşmesi gerekir. Şu anda, hangi sürücü zamanlama hello çıktı veri kümesi değil. Bu nedenle, Hello etkinlik herhangi bir çıktı üretmez olsa bile bir çıkış veri kümesi oluşturmanız gerekir. 

## <a name="specify-schedule-for-a-dataset"></a>Bir veri kümesi için zamanlamayı belirtin
Data Factory işlem hattı bir etkinlikte sıfır veya daha fazla giriş alabilir **veri kümeleri** ve bir veya daha fazla çıkış veri kümeleri oluşturma. Bir etkinlik için hangi hello giriş verileri kullanılabilir hello tempoyla belirtebilir ya da hello çıktı verilerini hello kullanarak oluşturulur **kullanılabilirlik** hello dataset tanımları bölümünde. 

**Sıklık** hello içinde **kullanılabilirlik** bölümü hello zaman birimini belirtir. Merhaba izin verilen değerler Sıklık: dakika, saat, gün, hafta ve ay. Merhaba **aralığı** özelliği hello kullanılabilirlik bölümünde sıklığı çarpanı belirtir. Örneğin: hello sıklığını tooDay ayarlamak ve aralığı too1 bir çıkış veri kümesi için ayarlamak, hello çıktı verilerini günlük üretilir. Merhaba sıklığını dakika belirtirseniz, 15'den küçük hello aralığı toono ayarlamanızı öneririz. 

Aşağıdaki örneğine hello hello giriş verisi saatlik kullanılabilir ve hello çıktı verilerini saatlik üretilen (`"frequency": "Hour", "interval": 1`). 

**Girdi veri kümesi:** 

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```


**Çıktı veri kümesi**

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mypath/{Year}/{Month}/{Day}/{Hour}",
            "format": {
                "type": "TextFormat"
            },
            "partitionedBy": [
                { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
                { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" }}
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Şu anda **çıkış veri kümesi sürücüleri hello zamanlama**. Diğer bir deyişle, hello çıkış veri kümesi için belirtilen hello kullanılan toorun çalışma zamanında bir etkinlik zamanlamadır. Bu nedenle, Hello etkinlik herhangi bir çıktı üretmez olsa bile bir çıkış veri kümesi oluşturmanız gerekir. Merhaba etkinlik herhangi bir girdi almazsa oluşturma hello girdi veri kümesi atlayabilirsiniz. 

Merhaba aşağıdakileri tanımı hello kanal **Zamanlayıcı** hello etkinliği için kullanılan toospecify zamanlama bir özelliktir. Bu özellik isteğe bağlıdır. Şu anda hello zamanlama hello etkinliğinin hello çıkış veri kümesi için belirtilen hello zamanlaması eşleşmesi gerekir.
 
```json
{
    "name": "SamplePipeline",
    "properties": {
        "description": "copy activity",
        "activities": [
            {
                "type": "Copy",
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 100000,
                        "writeBatchTimeout": "00:05:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureSQLInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
        ],
        "start": "2017-04-01T08:00:00Z",
        "end": "2017-04-01T11:00:00Z"
    }
}
```

Bu örnekte, saatlik hello etkinlik çalışması hello arasında başlangıç ve bitiş hello ardışık saatlerini. Merhaba çıktı verilerini saatlik üç saatlik windows (8: 00 - 9'da, 09: 00 - 10'da ve 10: 00 - 11: 00) oluşturulur. 

Her birim tüketilen veya bir etkinlik tarafından üretilen verilerin adlı bir **veri dilimi**. Aşağıdaki diyagramda hello bir giriş veri kümesi ve bir çıkış veri kümesi olmayan bir etkinliği örneği gösterilmektedir: 

![Kullanılabilirlik Zamanlayıcı](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

Merhaba diyagramı hello saatlik hello veri dilimleri giriş ve çıkış dataset gösterir. Merhaba diyagramı işlenmeye hazır üç girdi dilimlerinin gösterir. Merhaba 10-11 AM etkinlik hello 10-11 AM çıktı diliminin oluşturan devam ediyor. 

Değişkenleri kullanılarak JSON hello kümesindeki geçerli dilimin hello ilişkili hello zaman aralığı erişebilirsiniz: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) ve [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables). Benzer şekilde, bir etkinlik penceresiyle hello WindowStart ve WindowEnd kullanarak ilişkili hello zaman aralığı erişebilir. Etkinliğin başlangıç zamanlama hello çıktı veri kümesi hello etkinliğinin hello zamanlamasını eşleşmesi gerekir. Bu nedenle, hello SliceStart ve SliceEnd değerlerini olduğunuz hello aynı WindowStart ve WindowEnd değerleri olarak sırasıyla. Bu değişkenleri hakkında daha fazla bilgi için bkz: [Data Factory işlevler ve sistem değişkenleri](data-factory-functions-variables.md#data-factory-system-variables) makaleleri.  

Etkinlik JSON farklı amaçlar için bu değişkenleri kullanabilirsiniz. Örneğin, bunları zaman serisi verilerini temsil eden giriş ve çıkış veri kümeleri tooselect verileri kullanabilirsiniz (örneğin: 8 AM too9 'M). Bu örnek ayrıca kullanır **WindowStart** ve **WindowEnd** tooselect ilgili verileri etkinlik için çalıştırın ve uygun hello ile tooa blob kopyalama **folderPath**. Merhaba **folderPath** parametreli toohave her saat için ayrı bir klasör değil.  

Örnek önceki hello girdi ve çıktı veri kümeleri için belirtilen hello zamanlaması olan hello aynı (saat). Hello hello etkinliğinin girdi veri kümesi deyin 15 dakikada bir farklı bir sıklık, varsa, hangi sürücü etkinlik zamanlaması hello hello çıktı veri kümesi olduğu gibi bu çıkış veri kümesini üreten hello etkinlik hala saatte bir kez çalışır. Daha fazla bilgi için bkz: [modeli farklı sıklıklarını veri kümeleriyle](#model-datasets-with-different-frequencies).

## <a name="dataset-availability-and-policies"></a>DataSet kullanılabilirliği ve ilkeleri
Veri kümesi tanımı hello kullanılabilirlik bölümünü sıklık ve aralığı özelliklerinde hello kullanımını gördünüz. Merhaba zamanlama ve yürütme etkinliğin etkileyen birkaç diğer özellikler vardır. 

### <a name="dataset-availability"></a>DataSet kullanılabilirliği 
Merhaba aşağıdaki tabloda açıklanmaktadır hello kullanabileceğiniz özellikleri **kullanılabilirlik** bölümü:

| Özellik | Açıklama | Gerekli | Varsayılan |
| --- | --- | --- | --- |
| frequency |Veri kümesi dilim üretim Hello zaman birimini belirtir.<br/><br/><b>Sıklık desteklenen</b>: dakika, saat, gün, hafta, ay |Evet |NA |
| interval |Sıklığı çarpanı belirtir<br/><br/>"X sıklığı aralığını" ne sıklıkta hello dilim üretilen belirler.<br/><br/>Saatlik olarak başka bir dilimlenebilir dataset toobe hello varsa, ayarladığınız <b>sıklığı</b> çok<b>saat</b>, ve <b>aralığı</b> çok<b>1</b>.<br/><br/><b>Not</b>: sıklığını dakika belirtirseniz, 15'den küçük hello aralığı toono ayarlamanızı öneririz |Evet |NA |
| stili |Merhaba dilim hello başlangıç/bitiş hello aralığının üretilen olup olmadığını belirtir.<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul><br/><br/>Sıklık tooMonth ayarlanır ve stil tooEndOfInterval hello dilim ayın son günü hello üzerinde üretilmez. Merhaba stili tooStartOfInterval ayarlarsanız hello dilim ayın ilk günü hello üzerinde oluşturulur.<br/><br/>Sıklık tooDay ayarlanır ve stil tooEndOfInterval hello dilim hello hello günün son bir saat üretilmez.<br/><br/>Sıklık tooHour ayarlanır ve stil tooEndOfInterval hello dilim hello hello saat sonunda üretilmez. Örneğin, 13'te – 2 PM dönem için bir dilim için 2 saat hello dilim oluşturulur. |Hayır |EndOfInterval |
| anchorDateTime |Zamanlayıcı toocompute dataset dilim sınırları tarafından kullanılan süre içinde mutlak konum Hello tanımlar. <br/><br/><b>Not</b>: Merhaba AnchorDateTime sahip hello sıklığından daha ayrıntılı tarih kısımlarını sonra hello daha ayrıntılı bölümleri göz ardı edilir. <br/><br/>Örneğin, hello <b>aralığı</b> olan <b>saatlik</b> (sıklığı: saat ve aralığı: 1) ve hello <b>AnchorDateTime</b> içeren <b>dakika ve saniyeleri</b>, ardından hello <b>dakika ve saniyeleri</b> hello AnchorDateTime bölümlerini yok sayılır. |Hayır |01/01/0001 |
| uzaklık |Tarafından hangi hello başlangıç ve bitiş tüm veri kümesi dilim gölgeye Timespan. <br/><br/><b>Not</b>: anchorDateTime ve uzaklık belirtilirse, hello birleştirilmiş hello shift sonucudur. |Hayır |NA |

### <a name="offset-example"></a>uzaklık örneği
Varsayılan olarak, her gün (`"frequency": "Day", "interval": 1`) dilimler 00: 00 UTC zaman (gece yarısı) başlatın. Merhaba başlangıç saati toobe 6'da UTC saati bunun yerine isterseniz, hello aşağıdaki kod parçacığında gösterildiği gibi uzaklığı hello ayarlayın: 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a>anchorDateTime örneği
Aşağıdaki örneğine hello hello dataset 23 saatte bir kez oluşturulur. Merhaba ilk dilim çok ayarlanır hello anchorDateTime tarafından belirtilen hello süresi başlar`2017-04-19T08:00:00` (UTC saati).

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a>uzaklık/örnek stili
Merhaba aşağıdaki veri kümesi bir aylık veri kümesidir ve 8: 00'da her ayın 3 üretilir (`3.08:00:00`):

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a>Veri kümesi İlkesi
Bir veri kümesi kullanıma hazır hale gelmeden önce bir dilim yürütme tarafından oluşturulan hello verilerini nasıl doğrulanabilir belirten bir doğrulama ilkesi tanımlı olabilir. Merhaba dilim yürütme sona erdikten sonra bu gibi durumlarda hello çıkış dilim durumu çok değiştirilir**bekleyen** substatus ile **doğrulama**. Merhaba dilimler doğrulandıktan sonra hello dilim çok durumuna**hazır**. Veri dilimi üretilen ancak hello doğrulamayı geçemedi, etkinlik çalışması için bu dilimine bağlıdır aşağı akış dilimleri işlenmez. [İzleme ve ardışık düzen yönetme](data-factory-monitor-manage-pipelines.md) kapsar hello veri fabrikasında veri dilimleri çeşitli durumları.

Merhaba **İlkesi** gerekir dataset dilimler hello hello koşulu karşılayan veya veri kümesi tanımı bölümünde hello ölçütleri tanımlar. Merhaba aşağıdaki tabloda açıklanmaktadır hello kullanabileceğiniz özellikleri **İlkesi** bölümü:

| İlke adı | Açıklama | Çok uygulanan| Gerekli | Varsayılan |
| --- | --- | --- | --- | --- |
| minimumSizeMB | Merhaba verilerin doğrulayan bir **Azure blob** karşılıyor hello minimum boyut gereksinimlerini (megabayt cinsinden). |Azure Blob |Hayır |NA |
| minimumRows | Merhaba verilerin doğrulayan bir **Azure SQL veritabanı** veya bir **Azure tablo** hello en az satır sayısını içerir. |<ul><li>Azure SQL Database</li><li>Azure tablo</li></ul> |Hayır |NA |

#### <a name="examples"></a>Örnekler
**minimumSizeMB:**

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

**minimumRows**

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

Bu özellikler ve örnekler hakkında daha fazla bilgi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi. 

## <a name="activity-policies"></a>Etkinlik ilkeleri
İlkeler, özellikle bir tablonun hello dilim işlendiğinde bir etkinlik hello çalışma zamanı davranışını etkiler. Aşağıdaki tablonun hello hello ayrıntılar sağlar.

| Özellik | İzin verilen değerler | Varsayılan değer | Açıklama |
| --- | --- | --- | --- |
| Eşzamanlılık |Tamsayı <br/><br/>En yüksek değeri: 10 |1 |Eşzamanlı yürütmeleri hello etkinlik sayısı.<br/><br/>Üzerinde farklı dilimler oluşabilir paralel etkinlik yürütmeleri hello sayısını belirler. Örneğin, bir etkinlik toogo aracılığıyla gerekiyorsa kullanılabilir veri, daha büyük bir eşzamanlılık değer sahip büyük bir dizi hello veri işleme hızı artar. |
| executionPriorityOrder |NewestFirst<br/><br/>OldestFirst |OldestFirst |İşlenen veri dilimleri Hello sıralama belirler.<br/><br/>Örneğin, varsa (bir oluşmasını 4 pm adresindeki ve 17: 00 saatleri sırasında başka bir) 2 böler ve hem de yürütme olması. Merhaba executionPriorityOrder toobe NewestFirst ayarlarsanız, 17: 00 saatleri sırasında hello dilim önce işlenir. Merhaba executionPriorityORder toobe OldestFIrst ayarlarsanız, benzer şekilde ardından 4 PM adresindeki hello dilim işlenir. |
| retry |Tamsayı<br/><br/>En büyük değer 10 olabilir |0 |Hata olarak işaretlenmiş hello veri işleme hello dilim için önce yeniden deneme sayısı. Etkinlik yürütme veri dilimi için belirtilen toohello denenen yeniden deneme sayısı. mümkün olan en kısa sürede hello hatasından sonra Hello yeniden deneme yapılır. |
| timeout |TimeSpan |00:00:00 |Merhaba etkinlik için zaman aşımı. Örnek: 00:10: (zaman aşımı 10 dakika anlamına gelir) 00<br/><br/>Bir değer belirtilmemiş ya da 0 hello zaman aşımı sonsuzdur.<br/><br/>Merhaba veri işleme saat dilimi hello zaman aşımı değerini aşarsa, iptal edilir ve tooretry hello işleme hello sistem dener. yeniden deneme sayısı Hello hello yeniden deneme özelliğe bağlıdır. Zaman aşımı oluştuğunda hello durumu tooTimedOut ayarlanır. |
| gecikme |TimeSpan |00:00:00 |Veri işleme hello dilim başlatır önce Hello gecikme belirtin.<br/><br/>Merhaba gecikme hello beklenen yürütme zamanı geçmişte sonra veri dilimi için etkinliğin hello yürütme başlatılır.<br/><br/>Örnek: 00:10: (10 dakika gecikme anlamına gelir) 00 |
| longRetry |Tamsayı<br/><br/>En yüksek değeri: 10 |1 |Dilim yürütülemedi Hello hello uzun yeniden deneme girişimi sayısı.<br/><br/>longRetry girişimleri tarafından longRetryInterval aralarına aralık eklenir. Yeniden deneme girişimleri arasındaki süre toospecify gerekiyorsa, bu nedenle longRetry kullanın. Yeniden deneme ve longRetry belirtilirse, her bir longRetry denemesi denemeleri içerir ve hello en fazla deneme sayısı yeniden deneme * longRetry.<br/><br/>Örneğin, biz hello etkinlik İlkesi ayarlarında aşağıdaki hello varsa:<br/>Yeniden deneme: 3<br/>longRetry: 2<br/>longRetryInterval: 01:00:00<br/><br/>Yalnızca bir dilim tooexecute olduğu varsayılır (Durum Bekliyor) ve hello Etkinlik yürütme her zaman başarısız olur. Başlangıçta 3 ardışık yürütme deneme olacaktır. Her girişiminden sonra Yeniden Dene'yi hello dilim durum olacaktır. İlk 3 deneme üzerinden sonra hello dilim durumunu LongRetry olacaktır.<br/><br/>Bir saat sonra (diğer bir deyişle, longRetryInteval'ın değeri), 3 ardışık yürütme deneme başka bir dizi olacaktır. Bundan sonra hello dilim durumu başarısız ve daha fazla yeniden deneme yok denenmesi. Bu nedenle genel 6 deneme yapıldı.<br/><br/>Hiçbir yürütme başarılı olursa, hello dilim durum hazır olur ve daha fazla yeniden deneme yok çalıştı.<br/><br/>longRetry, belirleyici olmayan zamanlarda bağımlı veri ulaştığında veya hello genel ortamında hangi veri işleme gerçekleşir altında anormal olduğu durumlarda kullanılabilir. Böyle durumlarda, yeniden deneme birbiri ardından yapılması yardımcı ve bunun hello sonuçlarında zaman aralığını sonra yapılması istenen çıkış.<br/><br/>Uyarı: longRetry veya longRetryInterval yüksek değerleri ayarlı değil. Genellikle, daha yüksek değerleri sistemle ilgili diğer sorunlar kapsıyor. |
| longRetryInterval |TimeSpan |00:00:00 |uzun yeniden deneme girişimleri arasında gecikme Hello |

Daha fazla bilgi için bkz: [ardışık düzen](data-factory-create-pipelines.md) makalesi. 

## <a name="parallel-processing-of-data-slices"></a>Veri dilimi paralel işlenmesi
Merhaba hello ardışık düzeni için başlangıç tarihi geçmiş hello ayarlayabilirsiniz. Bunu yaptığınızda, veri fabrikası otomatik olarak hello geçen tüm veri dilimleri (arka dolgu) hesaplar ve bunları işlemeye başlar. Örneğin: 2017-04-01 başlangıç tarihi ile işlem hattı oluşturma ve hello geçerli tarih olan 2017-04-10. Merhaba tempoyla Merhaba, veri kümesi günlük 2017-04-01 gelen tüm hello dilimler işleme Data Factory başlatır olduğundan çıktısını alırsanız hello başlangıç tarihi too2017-04-09 hemen hello son olmasıdır. Stil özelliği hello kullanılabilirlik bölümdeki Hello değeri EndOfInterval olduğundan 2017-04-10 hello dilimden varsayılan olarak henüz işlenmedi. Merhaba eski dilim işlenir ilk hello varsayılan olarak executionPriorityOrder OldestFirst değeri. Merhaba stil özelliği açıklaması için bkz: [dataset kullanılabilirliği](#dataset-availability) bölümü. Merhaba hello executionPriorityOrder bölüm açıklaması için bkz: [etkinlik ilkeleri](#activity-policies) bölümü. 

Paralel olarak ayarlama hello tarafından işlenen geri doldurulmuş veri dilimleri toobe yapılandırabilirsiniz **eşzamanlılık** hello özelliğinde **İlkesi** JSON hello etkinliği bölümü. Bu özellik üzerinde farklı dilimler oluşabilir paralel etkinlik yürütmeleri hello sayısını belirler. Merhaba hello eşzamanlılık özelliği için varsayılan değer 1'dir. Bu nedenle, bir dilim aynı anda varsayılan olarak işlenir. Merhaba en büyük değer 10'dur. Bir işlem hattı aracılığıyla kullanılabilir veri, daha büyük bir eşzamanlılık değer sahip büyük bir dizi toogo gerektiği zaman hello veri işleme hızı artar. 

## <a name="rerun-a-failed-data-slice"></a>Başarısız olan veri dilimi yeniden çalıştırın
Veri dilimi işlenirken bir hata ortaya çıkarsa, Azure portal dikey penceresi veya izleme ve yönetme uygulaması'nı kullanarak bir dilim hello işlenmesini neden başarısız anlamak bulabilirsiniz. Bkz: [izleme ve Azure portal dikey penceresi kullanılarak işlem hatlarını yönetme](data-factory-monitor-manage-pipelines.md) veya [izleme ve yönetim uygulaması](data-factory-monitor-manage-app.md) Ayrıntılar için.

Aşağıdaki iki etkinlik gösterir örneğine hello göz önünde bulundurun. Activity1 ve aktivite 2. Activity1 Dataset1 dilimin kullanır ve bir giriş olarak Activity2 tooproduce hello son veri kümesi, bir dilim tarafından tüketilen Dataset2 dilimin üretir.

![Başarısız dilim](./media/data-factory-scheduling-and-execution/failed-slice.png)

Merhaba diyagramı hatası üretmeye hello 9-10'da dilim Dataset2 için vardı üç son dilim dışında gösterir. Veri Fabrikası bağımlılık hello zaman serisi veri kümesi için otomatik olarak izler. Sonuç olarak, hello 9-10'da aşağı akış dilimi çalıştırın hello etkinlik başlatılmaz.

Merhaba başarısız dilim tooeasily Bul hello kök hello sorunu neden ve düzeltmek için data Factory izleme ve Yönetim Araçları toodrill hello tanılama günlüklerine sağlar. Merhaba sorunu düzelttikten sonra tooproduce hello başarısız dilim hello etkinlik kolayca başlatabilirsiniz. Hakkında daha fazla bilgi için toorerun ve veri dilimi için durumu geçişleri anlamak, [izleme ve Azure portal dikey penceresi kullanılarak işlem hatlarını yönetme](data-factory-monitor-manage-pipelines.md) veya [izleme ve yönetim uygulaması](data-factory-monitor-manage-app.md).

Merhaba yeniden sonra için 9-10'da dilim **Dataset2**, veri fabrikası başlatır hello hello 9-10'da bağımlı dilimi için hello son dataset üzerinde çalıştırın.

![Başarısız dilimi yeniden çalıştırın](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a>Bir işlem hattında birden çok etkinlik
Bir işlem hattında birden fazla etkinliğiniz olabilir. Merhaba etkinlikler için giriş veri dilimi hazır olup olmadığını hello etkinlikleri bir ardışık düzende birden çok etkinliği varsa ve bir etkinlik hello çıktısını başka bir etkinliğin bir giriş değil, paralel olarak çalışabilir.

Merhaba çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir. Merhaba etkinlikleri hello olabilir aynı ardışık düzen veya farklı ardışık düzenler. yalnızca hello önce bir başarıyla tamamlandığında hello ikinci etkinlik yürütür.

Örneğin, bir işlem hattı iki etkinlik sahip olduğu durumda aşağıdaki hello göz önünde bulundurun:

1. Dış giriş veri kümesi D1 ve D2 üretir çıktı veri kümesi gerektiren etkinlik A1.
2. Çıkış dataset D3 D2 kümesinden giriş gerektirir ve üreten etkinlik A2.

Bu senaryo, etkinlikleri A1 ve A2 olan hello aynı kanalı. Merhaba etkinliği hello dış veriler kullanılabilir ve zamanlanmış hello kullanılabilirlik sıklığı sınırına a1 çalıştırılır. Merhaba etkinlik A2 hello D2 gelen zamanlanmış dilimler kullanılabilir hale gelir ve hello zamanlanan kullanılabilirlik sıklığı ulaşıldığında çalışır. Veri kümesi D2 hello dilimleri birinde bir hata varsa, kullanılabilir oluncaya kadar A2 bu dilim için çalışmaz.

aynı ardışık düzen hello diyagramı aşağıdaki gibi görünür diyagram görünümü hello hem etkinliklerle hello:

![Merhaba aktivitelerde zincirleme aynı kanalı](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

Daha önce belirtildiği gibi hello etkinlikler farklı ardışık düzenlerinde olabilir. Böyle bir senaryoda hello diyagram görünümü diyagramda aşağıdaki hello gibi görünür:

![İki ardışık düzende zincirleme etkinlikleri](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

Merhaba bkz [sırayla kopyalamak](#copy-sequentially) hello ek bir örnek bölümünde.

## <a name="model-datasets-with-different-frequencies"></a>Farklı sıklıklarını modeli kümeleriyle
Merhaba örnekleri için girdi ve çıktı veri kümelerini ve hello etkinlik zamanlama penceresi hello sıklıkları olan hello aynı. Bazı senaryolar hello özelliği tooproduce çıktıyı bir veya daha fazla girdi hello sıklık farklı bir sıklık gerektirir. Veri Fabrikası bu senaryo modelleme destekler.

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a>Örnek 1: her saat kullanılabilir giriş verileri için bir günlük çıkışı raporu oluşturmak
Azure Blob storage'da her saat algılayıcılar kullanılabilir ölçüm verileri Giriş bir senaryo düşünün. Tooproduce ortalama, maksimum ve minimum gibi istatistikleri içeren bir günlük toplama rapor ile Merhaba gün için istediğiniz [Data Factory hive etkinliği](data-factory-hive-activity.md).

Bu senaryo Data Factory ile nasıl model aşağıda verilmiştir:

**Girdi veri kümesi**

Merhaba, saatlik gün verilen hello hello klasöründeki dosyaları bırakılan giriş. Giriş için kullanılabilirlik ayarlanırsa **saat** (sıklığı: saat, aralığı: 1).

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
**Çıktı veri kümesi**

Bir çıkış dosyası her gün hello günün klasöründe oluşturulur. Çıktı kullanılabilirliğini ayarlanırsa **gün** (sıklığı: gün ve aralığı: 1).

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Etkinlik: ardışık düzeninde hive etkinliği**

Merhaba hive betiğini alır hello uygun *DateTime* bilgileri hello kullandığınız parametre olarak **WindowStart** hello aşağıdaki kod parçacığında gösterildiği gibi değişkeni. Merhaba hive betiğini Bu değişken tooload hello veri hello doğru klasöründen hello gün için kullanır ve hello toplama toogenerate hello çıkış çalıştırın.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
        {
            "name": "SampleHiveActivity",
            "inputs": [
                {
                    "name": "AzureBlobInput"
                }
            ],
            "outputs": [
                {
                    "name": "AzureBlobOutput"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adftutorial\\hivequery.hql",
                "scriptLinkedService": "StorageLinkedService",
                "defines": {
                    "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
                    "Month": "$$Text.Format('{0:MM}',WindowStart)",
                    "Day": "$$Text.Format('{0:dd}',WindowStart)"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },            
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 2,
                "timeout": "01:00:00"
            }
         }
     ]
   }
}
```

Merhaba Aşağıdaki diyagramda açısından bir veri bağımlılığı hello senaryo gösterilmektedir.

![Veri bağımlılığı](./media/data-factory-scheduling-and-execution/data-dependency.png)

Merhaba çıktı diliminin her gün için bir giriş veri kümesinden 24 saat dilimi bağlıdır. Veri Fabrikası hesaplar çözülmesi tarafından otomatik olarak bu bağımlılıklar hello kalan giriş veri dilimleri hello aynı üretilen çıkış dilim toobe hello olarak süre. Merhaba 24 girdi dilimlerinin hiçbirinde yoksa, veri fabrikası hello girdi dilimi toobe hello günlük etkinlik başlatmadan önce hazır bekler.

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a>Örnek 2: bağımlılık, ifadeler ve Data Factory işlevleri ile belirtin.
Şirketinizdeki başka bir senaryo düşünün. İki giriş veri kümesi işleyen bir hive etkinliği olduğunu varsayalım. Bunlardan birini yeni veri günlük olsa da, bunlardan biri her hafta yeni verileri alır. Merhaba iki girdi arasında toodo bir birleştirme istediğinizi varsayın ve her gün bir çıktı üretir.

Merhaba basit yaklaşım, veri fabrikası hello sağ girişi otomatik olarak rakamları toohello çıkış veri dilimin zaman dönemi çalışmıyor hizalayarak tooprocess böler.

Çalıştıran her etkinlik için hello haftalık girdi veri kümesi için geçen haftaki veri dilimi hello Data Factory kullanmalısınız belirtmeniz gerekir. Bu davranış hello parçacığı tooimplement aşağıdaki gösterildiği gibi Azure Data Factory işlevlerini kullanın.

**Input1: Azure blob**

Merhaba, ilk hello Azure blob günlük güncelleştiriliyor giriş.

```json
{
  "name": "AzureBlobInputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Input2: Azure blob**

Input2 hello haftalık güncelleştirilmekte Azure blob ' dir.

```json
{
  "name": "AzureBlobInputWeekly",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 7
    }
  }
}
```

**Çıkış: Azure blob**

Bir çıkış dosyası her gün hello gün için hello klasöründe oluşturulur. Çıktı kullanılabilirliğini çok ayarlamak**gün** (sıklığı: Day, aralığı: 1).

```json
{
  "name": "AzureBlobOutputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Etkinlik: ardışık düzeninde hive etkinliği**

Merhaba hive etkinliği hello iki girdi alır ve her gün bir çıktı diliminin üretir. Her günün çıkış dilim toodepend üzerinde hello önceki haftanın girdi dilimi haftalık girişi için şu şekilde belirtebilirsiniz.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
      {
        "name": "SampleHiveActivity",
        "inputs": [
          {
            "name": "AzureBlobInputDaily"
          },
          {
            "name": "AzureBlobInputWeekly",
            "startTime": "Date.AddDays(SliceStart, - Date.DayOfWeek(SliceStart))",
            "endTime": "Date.AddDays(SliceEnd,  -Date.DayOfWeek(SliceEnd))"  
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutputDaily"
          }
        ],
        "linkedServiceName": "HDInsightLinkedService",
        "type": "HDInsightHive",
        "typeProperties": {
          "scriptPath": "adftutorial\\hivequery.hql",
          "scriptLinkedService": "StorageLinkedService",
          "defines": {
            "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
            "Month": "$$Text.Format('{0:MM}',WindowStart)",
            "Day": "$$Text.Format('{0:dd}',WindowStart)"
          }
        },
        "scheduler": {
          "frequency": "Day",
          "interval": 1
        },            
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 2,  
          "timeout": "01:00:00"
        }
       }
     ]
   }
}
```

Bkz: [Data Factory işlevler ve sistem değişkenleri](data-factory-functions-variables.md) işlevler ve Data Factory destekleyen sistem değişkenleri listesi.

## <a name="appendix"></a>Ek

### <a name="example-copy-sequentially"></a>Örnek: sıralı olarak Kopyala
Bu olası toorun birden çok kopyalama işlemleri birbiri ardından sıralı/sıralı bir biçimde değil. Örneğin, iki kopyalama aşağıdaki hello ile bir ardışık düzendeki (CopyActivity1 ve CopyActivity2) etkinlik giriş verileri çıkış veri kümeleri olabilir:   

CopyActivity1

Giriş: veri kümesi. Çıkış: Dataset2.

CopyActivity2

Giriş: Dataset2.  Çıkış: Dataset3.

CopyActivity2 yalnızca hello CopyActivity1 başarıyla çalıştırıldı ve Dataset2 kullanılabilir çalışır.

Merhaba örnek JSON ardışık düzeni şöyledir:

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob1ToBlob2",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset3"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob2ToBlob3",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

Merhaba ikinci etkinlik için giriş olarak hello çıkış veri kümesi hello ilk kopyalama etkinliği (Dataset2) Hello örnekte belirtilen dikkat edin. Bu nedenle, yalnızca hello ilk etkinliğinden hello çıktı veri kümesi hazır olduğunda hello ikinci etkinliği çalıştırır.  

Merhaba örnekte CopyActivity2 Dataset3 gibi farklı bir giriş olabilir ancak CopyActivity1 tamamlanana kadar hello etkinlik çalışmaz için bir giriş tooCopyActivity2 Dataset2 belirtin. Örneğin:

CopyActivity1

Giriş: Dataset1. Çıkış: Dataset2.

CopyActivity2

Girişler: Dataset3, Dataset2. Çıkış: Dataset4.

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlobToBlob",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset3"
                    },
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset4"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob3ToBlob4",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

Merhaba ikinci kopya etkinliği için iki giriş veri kümesi Hello örnekte belirtilen dikkat edin. Birden çok girişi belirtildiğinde, yalnızca hello ilk girdi veri kümesi veri kopyalamak için kullanılır, ancak diğer veri kümeleri bağımlılıklar olarak kullanılır. Yalnızca hello aşağıdaki koşulların karşılandığından sonra CopyActivity2 başlatmak:

* CopyActivity1 başarıyla tamamlandı ve Dataset2 kullanılabilir. Bu veri kümesi, veri tooDataset4 kopyalarken kullanılmaz. Yalnızca CopyActivity2 için zamanlama bağımlılık olarak davranır.   
* Dataset3 kullanılabilir. Bu veri kümesi kopyalanan toohello hedef hello verileri temsil eder. 
