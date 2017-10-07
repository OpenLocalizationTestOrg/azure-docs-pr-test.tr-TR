---
title: "aaaData Fabrika işlevler ve sistem değişkenleri | Microsoft Docs"
description: "Azure Data Factory işlevler ve sistem değişkenleri listesini sağlar"
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
services: data-factory
ms.assetid: b6b3c2ae-b0e8-4e28-90d8-daf20421660d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: d2936c2821797947bb37d9775226a6c19c4b8ab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a>Azure Data Factory - işlevler ve sistem değişkenleri
Bu makalede, işlevleri ve değişkenler Azure Data Factory ile desteklenen hakkında bilgi sağlar.

## <a name="data-factory-system-variables"></a>Veri Fabrikası sistem değişkenleri
| Değişken adı | Açıklama | Nesne kapsamı | JSON kapsamı ve kullanım örnekleri |
| --- | --- | --- | --- |
| WindowStart |Geçerli etkinlik penceresini çalıştırmak için zaman aralığı başlangıcı |Etkinlik |<ol><li>Veri seçimi sorguları belirtin. Hello başvurulan bağlayıcı makalelerine bakın [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalesi.</li> |
| WindowEnd |Geçerli etkinlik penceresini çalıştırmak için zaman aralığı sonu |Etkinlik |WindowStart ile aynıdır. |
| SliceStart |Zaman aralığı için üretilen veri dilimi başlangıcı |Etkinlik<br/>Veri kümesi |<ol><li>Dinamik klasör yolu belirtin ve dosya adları ile çalışırken [Azure Blob](data-factory-azure-blob-connector.md) ve [dosya sistemi veri kümeleri](data-factory-onprem-file-system-connector.md).</li><li>Veri Fabrikası işlevleriyle etkinlik girişleri koleksiyonu giriş bağımlılıkları belirtin.</li></ol> |
| SliceEnd |Geçerli veri dilimi için zaman aralığı sonu. |Etkinlik<br/>Veri kümesi |SliceStart ile aynıdır. |

> [!NOTE]
> Veri Fabrikası bu hello zamanlama içinde belirtilen hello gerektirir şu anda etkinlik hello çıkış dataset kullanılabilirliği içinde belirtilen hello zamanlaması tam olarak eşleşir. Bu nedenle, WindowStart, WindowEnd ve SliceStart ve SliceEnd her zaman toohello eşleme aynı zaman dönemi ve tek bir çıktı dilim.
> 

### <a name="example-for-using-a-system-variable"></a>Bir sistem değişkeni kullanma örneği
Aşağıdaki örnek, yıl, ay, gün ve saat hello içinde **SliceStart** tarafından kullanılan ayrı değişkenleri içine ayıklanan **folderPath** ve **fileName** özellikleri.

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

## <a name="data-factory-functions"></a>Veri Fabrikası işlevleri
Merhaba amacıyla aşağıdaki sistem değişkenleri yanı sıra veri fabrikasında işlevleri kullanabilirsiniz:

1. Veri seçimi sorguları belirtme (Merhaba tarafından başvurulan bağlayıcı makalelerine bakın [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalesi.
   
   Veri Fabrikası işlevi sözdizimi tooinvoke hello:  **$$ <function>**  veri seçim sorguları ve diğer özellikleri hello etkinliği ve veri kümeleri için.  
2. Veri Fabrikası işlevleriyle etkinlik girişleri koleksiyonu giriş bağımlılıkları belirtme.
   
    $$ Giriş bağımlılık ifadeleri belirtmek için gerekli değildir.     

Aşağıdaki örnek, hello içinde **sqlReaderQuery** bir JSON dosyası özelliğinde hello tarafından döndürülen tooa değeri atanmış `Text.Format` işlevi. Bu örnek ayrıca adlı bir sistem değişkeni kullanır **WindowStart**, penceresi hello aktivitesinin hello başlangıç saati temsil eder.

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

Bkz: [özel tarih ve saat biçim dizeleri](https://msdn.microsoft.com/library/8kb3ddd4.aspx) kullanabileceğiniz farklı biçimlendirme seçenekleri açıklar konu (örneğin: yyyy karşılaştırması ay). 

### <a name="functions"></a>İşlevler
Aşağıdaki tablolar hello Azure Data Factory tüm hello işlevlerde listesi:

| Kategori | İşlevi | Parametreler | Açıklama |
| --- | --- | --- | --- |
| Zaman |AddHours(X,Y) |X: DateTime <br/><br/>Y: int |Y saatleri toohello zaman X verilen ekler. <br/><br/>Örnek:`9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM` |
| Zaman |AddMinutes(X,Y) |X: DateTime <br/><br/>Y: int |Y dakika tooX ekler.<br/><br/>Örnek:`9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM` |
| Zaman |StartOfHour(X) |X: Datetime |Hello için x hello saat bileşeni tarafından temsil edilen hello saat başlangıç saati alır. <br/><br/>Örnek:`StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM` |
| Tarih |AddDays(X,Y) |X: DateTime<br/><br/>Y: int |Y gün tooX ekler. <br/><br/>Örnek: 9/15/2013 12:00:00 PM + 2 gün = 9/17/2013 12:00:00 PM.<br/><br/>Negatif bir sayı Y belirterek gün çok çıkarabilirsiniz.<br/><br/>Örnek: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`. |
| Tarih |AddMonths(X,Y) |X: DateTime<br/><br/>Y: int |Y ay tooX ekler.<br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.<br/><br/>Negatif bir sayı Y belirterek ay çok çıkarabilirsiniz.<br/><br/>Örnek: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.|
| Tarih |AddQuarters(X,Y) |X: DateTime <br/><br/>Y: int |Y ekler * 3 ay tooX.<br/><br/>Örnek:`9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM` |
| Tarih |AddWeeks(X,Y) |X: DateTime<br/><br/>Y: int |Y ekler * 7 gün tooX<br/><br/>Örnek: 9/15/2013 12:00:00 PM + 1 hafta = 9/22/2013 12:00:00 PM<br/><br/>Negatif bir sayı Y belirterek hafta çok çıkarabilirsiniz.<br/><br/>Örnek: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`. |
| Tarih |AddYears(X,Y) |X: DateTime<br/><br/>Y: int |Y yıl tooX ekler.<br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/>Negatif bir sayı Y belirterek yıl çok çıkarabilirsiniz.<br/><br/>Örnek: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`. |
| Tarih |Day(X) |X: DateTime |X Hello gün bileşenini alır.<br/><br/>Örnek: `Day of 9/15/2013 12:00:00 PM is 9`. |
| Tarih |DayOfWeek(X) |X: DateTime |Merhaba haftanın günü bileşenini x alır.<br/><br/>Örnek: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`. |
| Tarih |DayOfYear(X) |X: DateTime |Merhaba gün hello yıl bileşenini X tarafından temsil edilen hello yıl içinde alır.<br/><br/>Örnekler:<br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| Tarih |DaysInMonth(X) |X: DateTime |Merhaba gün hello ay bileşenini X parametresi tarafından temsil edilen hello ay içinde alır.<br/><br/>Örnek: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`. |
| Tarih |EndOfDay(X) |X: DateTime |Merhaba son X hello gününün (gün bileşenini) temsil eden Hello tarih-saat alır.<br/><br/>Örnek: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`. |
| Tarih |EndOfMonth(X) |X: DateTime |X parametresi ay bileşen tarafından temsil edilen hello ayın Hello sonunu alır. <br/><br/>Örnek: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (güncel Eylül ayın hello sonunu temsil eden saat) |
| Tarih |StartOfDay(X) |X: DateTime |Merhaba hello gün bileşeninin X parametresi tarafından temsil edilen hello günün başlangıcını alır.<br/><br/>Örnek: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`. |
| Tarih saat |FROM(X) |X: dize |Dize X tooa tarih saat ayrıştırılamadı. |
| Tarih saat |Ticks(X) |X: DateTime |Merhaba çizgilerine X hello parametresi özelliğini alır. Bir değer 100 nanosaniye eşittir. Bu özellik başlangıç değeri 12:00:00 gece'den itibaren 1 Ocak 0001 geçen çizgilerine hello sayısını temsil eder. |
| Metin |Format(X) |X: Dize değişkeni |Biçimleri hello metin (kullanmak `\\'` birleşimi tooescape `'` karakter).|

> [!IMPORTANT]
> Başka bir işlev içinde bir işlevi kullanılırken toouse gerekmez  **$$**  hello iç işlevi için önek. Örneğin: $$Text.Format ('PartitionKey eq \\' my_pkey_filter_value\\' ve RowKey ge \\' {0: yyyy-aa-gg ss: dd:}\\'', Time.AddHours (SliceStart, -6)). Bu örnekte, dikkat  **$$**  öneki Merhaba kullanılmaz **Time.AddHours** işlevi. 

#### <a name="example"></a>Örnek
Hello hello Hive etkinliği için aşağıdaki örnek, giriş ve çıkış parametreleri hello kullanılarak belirlenir `Text.Format` işlevi ve SliceStart sistem değişkeni. 

```json  
{
    "name": "HiveActivitySamplePipeline",
        "properties": {
    "activities": [
            {
            "name": "HiveActivitySample",
            "type": "HDInsightHive",
            "inputs": [
                    {
                    "name": "HiveSampleIn"
                    }
            ],
            "outputs": [
                    {
                    "name": "HiveSampleOut"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                }
            }
            }
    ]
    }
}
```

### <a name="example-2"></a>Örnek 2

Aşağıdaki örneğine hello hello DateTime parametresi için saklı yordam etkinliği kullanılarak belirlenir hello hello metin. İşlev biçimlendirin ve SliceStart değişkeni hello. 

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
            "start": "2016-08-02T00:00:00Z",
            "end": "2016-08-02T05:00:00Z",
        "isPaused": false
    }
}
```

### <a name="example-3"></a>Örnek 3
önceki gün SliceStart, hello tarafından temsil edilen gün yerine tooread verilerden hello aşağıdaki örnekte gösterildiği gibi hello AddDays işlevi kullanın: 

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-01-01T08:00:00",
        "end": "2017-01-01T11:00:00",
        "description": "hive activity",
        "activities": [
            {
                "name": "SampleHiveActivity",
                "inputs": [
                    {
                        "name": "MyAzureBlobInput",
                        "startTime": "Date.AddDays(SliceStart, -1)",
                        "endTime": "Date.AddDays(SliceEnd, -1)"
                    }
                ],
                "outputs": [
                    {
                        "name": "MyAzureBlobOutput"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adftutorial\\hivequery.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Year": "$$Text.Format('{0:yyyy}',WindowsStart)",
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

Bkz: [özel tarih ve saat biçim dizeleri](https://msdn.microsoft.com/library/8kb3ddd4.aspx) kullanabileceğiniz farklı biçimlendirme seçenekleri açıklar konu (örneğin: yy yyyy karşılaştırması). 

