---
title: "aaaAzure Data Factory - JSON betik oluşturma başvurusu | Microsoft Docs"
description: "Data Factory varlıkları için JSON şemaları sağlar."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 813fd752bb0ecb1b513d022b9f302325105dac31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a>Azure Data Factory - JSON betik oluşturma başvurusu
Bu makalede, Azure Data Factory varlıkları (ardışık düzen, etkinlik, veri kümesi ve bağlantılı hizmet) tanımlamak için JSON şemaları ve örnekler sağlar.  

## <a name="pipeline"></a>İşlem hattı 
Ardışık düzen tanımı için üst düzey yapısı Hello aşağıdaki gibidir: 

```json
{
  "name": "SamplePipeline",
  "properties": {
    "description": "Describe what pipeline does",
    "activities": [
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

Aşağıdaki tabloda hello özellikleri hello ardışık düzen JSON tanımı içinde açıklanmaktadır:

| Özellik | Açıklama | Gerekli
-------- | ----------- | --------
| ad | Merhaba ardışık düzen adı. Etkinlik hello hello eylemi temsil eden bir ad belirtin veya yapılandırılmış toodo ardışık düzen değil<br/><ul><li>En fazla karakter sayısı: 260</li><li>Bir harf, sayı veya alt çizgi (_) ile başlamalıdır</li><li>Şu karakterler kullanılamaz: ".", "+","?", "/", "<",">", "*", "%", "&", ":","\\"</li></ul> |Evet |
| açıklama |Hangi hello etkinlik veya ardışık düzen açıklayan metin için kullanılır | Hayır |
| etkinlikler | Etkinliklerin listesini içerir. | Evet |
| start |Merhaba ardışık düzeni için başlangıç tarihi / saati. Olmalıdır [ISO biçiminde](http://en.wikipedia.org/wiki/ISO_8601). Örneğin: 2014-10-14T16:32:41. <br/><br/>Olası toospecify yerel saat örneğin bir EST zamanı. Örnek aşağıda verilmiştir: `2016-02-27T06:00:00**-05:00`, 6'da tahmini olduğu<br/><br/>Merhaba başlangıç ve bitiş özellikleri birlikte hello ardışık düzen etkin süresini belirtin. Çıktı dilimler yalnızca ile etkin bu dönemde üretilir. |Hayır<br/><br/>Merhaba end özelliği için bir değer belirtirseniz, hello başlangıç özelliği için değer belirtmeniz gerekir.<br/><br/>Merhaba başlangıç ve bitiş zamanlarını hem de boş toocreate işlem hattı olabilir. Her iki değeri de belirtilmelisiniz tooset etkin dönem hello ardışık düzen toorun için bir. Başlangıç ve bitiş zamanlarını belirtmezseniz, bir işlem hattı oluştururken, bunları ayarlayabilirsiniz daha sonra hello kümesi AzureRmDataFactoryPipelineActivePeriod cmdlet'ini kullanarak. |
| Bitiş |Merhaba ardışık düzeni için bitiş tarihi / saati. Belirtilen ISO biçiminde olmalıdır. Örneğin: 2014-10-14T17:32:41 <br/><br/>Olası toospecify yerel saat örneğin bir EST zamanı. Örnek aşağıda verilmiştir: `2016-02-27T06:00:00**-05:00`, 6'da tahmini olduğu<br/><br/>toorun hello ardışık kalıcı olarak belirtin 9999-09-09 hello end özelliği hello değeri olarak. |Hayır <br/><br/>Merhaba başlangıç özelliği için bir değer belirtirseniz, hello end özelliği için değer belirtmeniz gerekir.<br/><br/>Hello için notlarına bakın **Başlat** özelliği. |
| isPaused |Set tootrue hello ardışık çalışmazsa. Varsayılan değer = false. Bu özellik tooenable kullanın veya devre dışı bırakabilirsiniz. |Hayır |
| pipelineMode |zamanlama için başlangıç yöntemi hello ardışık düzeni için çalışır. İzin verilen değerler: (varsayılan), zamanlanmış kez.<br/><br/>'Zamanlanmış' Bu hello ardışık düzen tooits etkin dönemi (başlangıç ve bitiş saati) göre belirli bir zaman aralığında çalışır gösterir. 'Kez' Bu hello ardışık düzen yalnızca bir kez çalışır gösterir. Oluşturulduktan sonra kez ardışık düzen şu anda değiştiren/güncelleştirilemiyor. Bkz: [Onetime ardışık düzen](data-factory-create-pipelines.md#onetime-pipeline) kez ayar hakkındaki ayrıntılar için. |Hayır |
| expirationTime |Hangi hello ardışık düzeni geçerli değil ve sağlanan kalacağı oluşturulduktan sonra süre. Tüm etkin başarısız oldu, yok veya hello süre Dolum zamanına ulaştığında çalıştırır hello ardışık düzen otomatik olarak silinmesi durumunda. |Hayır |


## <a name="activity"></a>Etkinlik 
Ardışık düzen tanımı (etkinlikleri öğesi) içinde bir etkinlik için üst düzey yapısı Hello aşağıdaki gibidir:

```json
{
    "name": "ActivityName",
    "description": "description", 
    "type": "<ActivityType>",
    "inputs":  "[]",
    "outputs":  "[]",
    "linkedServiceName": "MyLinkedService",
    "typeProperties":
    {

    },
    "policy":
    {
    }
    "scheduler":
    {
    }
}
```

Tablo hello etkinlik JSON tanımını hello özellikleri açıklar:

| Etiket | Açıklama | Gerekli |
| --- | --- | --- |
| ad |Merhaba etkinlik adı. Merhaba etkinlik hello eylemi temsil eden adını toodo yapılandırılmış belirtin<br/><ul><li>En fazla karakter sayısı: 260</li><li>Bir harf, sayı veya alt çizgi (_) ile başlamalıdır</li><li>Şu karakterler kullanılamaz: ".", "+","?", "/", "<",">", "*", "%", "&", ":","\\"</li></ul> |Evet |
| açıklama |Hangi hello etkinliği açıklayan bir metin için kullanılır. |Evet |
| type |Merhaba etkinlik Hello türünü belirtir. Merhaba bkz [veri DEPOLARINA](#data-stores) ve [veri dönüştürme etkinlikleri](#data-transformation-activities) bölümleri etkinlikler farklı türde. |Evet |
| Girişleri |Merhaba etkinlik tarafından kullanılan giriş tabloları<br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |Evet |
| Çıkışları |Merhaba etkinlik tarafından kullanılan çıkış tabloları.<br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |Evet |
| linkedServiceName |Merhaba etkinlik tarafından kullanılan hello bağlı hizmetin adı. <br/><br/>Bir etkinlik toohello gerekli hesaplama ortamı bağlantılar hello bağlantılı hizmeti belirtin gerektirebilir. |Hdınsight etkinlikleri, Azure Machine Learning etkinlikleri ve saklı yordam etkinliği için Evet. <br/><br/>Diğer tümü için hayır |
| typeProperties |Merhaba typeProperties bölümündeki özellikler hello etkinlik türüne bağlıdır. |Hayır |
| ilke |Merhaba etkinlik hello çalışma zamanı davranışını etkileyen ilkeleri. Belirtilmezse, varsayılan ilkeler kullanılır. |Hayır |
| Zamanlayıcı |"Zamanlayıcı" Merhaba etkinliği için zamanlama kullanılan toodefine istenen özelliğidir. Onun alt olanları hello içinde hello aynı hello olan [dataset kullanılabilirliği özelliğinde](data-factory-create-datasets.md#dataset-availability). |Hayır |

### <a name="policies"></a>İlkeler
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

### <a name="typeproperties-section"></a>typeProperties bölümü
Merhaba typeProperties bölümü, her etkinlik için farklıdır. Dönüştürme etkinlikleri yalnızca hello türü özellikleri vardır. Bkz: [veri dönüştürme etkinlikleri](#data-transformation-activities) ardışık düzeninde dönüştürme etkinlikleri tanımlayan JSON örnekleri için bu makalenin bölümünde. 

**Kopya etkinliği** hello typeProperties bölümünde iki alt bölümleri vardır: **kaynak** ve **havuz**. Bkz: [veri DEPOLARINA](#data-stores) nasıl toouse veri depolayan bir kaynak ve/veya havuz gösteren JSON örnekleri için bu makaledeki bölüm. 

### <a name="sample-copy-pipeline"></a>Örnek kopyalama işlem hattı
Aşağıdaki örnek ardışık düzen hello türünde bir etkinlik yok **kopyalama** hello içinde **etkinlikleri** bölüm. Bu örnekte, hello [kopyalama etkinliğini](data-factory-data-movement-activities.md) Azure Blob Depolama tooan Azure SQL veritabanından veri kopyalar. 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputDataset"
          }
        ],
        "outputs": [
          {
            "name": "OutputDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

Hello aşağıdaki noktaları göz önünde bulundurun:

* Merhaba etkinlikler bölümünde, yalnızca bir etkinlik olduğundan, **türü** çok ayarlanır**kopya**.
* Merhaba etkinlik çok kümesi için giriş**InputDataset** ve hello etkinlik çok kümesi için çıkış**OutputDataset**.
* Merhaba, **typeProperties** bölümünde **BlobSource** hello kaynak türü olarak belirtilir ve **SqlSink** hello Havuz türü olarak belirtilir.

Bkz: [veri DEPOLARINA](#data-stores) nasıl toouse veri depolayan bir kaynak ve/veya havuz gösteren JSON örnekleri için bu makaledeki bölüm.    

Bu ardışık düzen oluşturma izlenecek tam yol için bkz: [Öğreticisi: Blob Storage tooSQL veritabanı ' veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

### <a name="sample-transformation-pipeline"></a>Örnek dönüştürme işlem hattı
Aşağıdaki örnek ardışık düzen hello türünde bir etkinlik yok **Hdınsighthive** hello içinde **etkinlikleri** bölümü. Bu örnekte, hello [Hdınsight Hive etkinliği](data-factory-hive-activity.md) Azure Hdınsight Hadoop kümesindeki Hive betiği çalıştırılarak verileri Azure Blob depolama biriminden dönüştürür. 

```json
{
    "name": "TransformPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "AzureStorageLinkedService",
                    "defines": {
                        "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                        "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                    }
                },
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
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Month",
                    "interval": 1
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00",
        "isPaused": false
    }
}
```

Hello aşağıdaki noktaları göz önünde bulundurun: 

* Merhaba etkinlikler bölümünde, yalnızca bir etkinlik olduğundan, **türü** çok ayarlanır**Hdınsighthive**.
* Merhaba Hive betik dosyası **partitionweblogs.hql**, hello Azure depolama hesabı depolanır (adlı hello scriptLinkedService tarafından belirtilen **AzureStorageLinkedService**) ve  **komut dosyası** hello kapsayıcı klasöründe **adfgetstarted**.
* Merhaba **tanımlar** bölümdür toohello hive betiğini Hive yapılandırma değerleri olarak geçirilir kullanılan toospecify hello çalışma zamanı ayarları (örneğin `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).

Bkz: [veri dönüştürme etkinlikleri](#data-transformation-activities) ardışık düzeninde dönüştürme etkinlikleri tanımlayan JSON örnekleri için bu makalenin bölümünde.

Bu ardışık düzen oluşturma izlenecek tam yol için bkz: [Öğreticisi: Hadoop kümesi kullanarak ilk ardışık düzen tooprocess verilerinizi yapı](data-factory-build-your-first-pipeline.md). 

## <a name="linked-service"></a>Bağlı hizmet
bağlantılı hizmet tanımı için üst düzey yapısı Hello aşağıdaki gibidir:

```json
{
    "name": "<name of hello linked service>",
    "properties": {
        "type": "<type of hello linked service>",
        "typeProperties": {
        }
    }
}
```

Tablo hello etkinlik JSON tanımını hello özellikleri açıklar:

| Özellik | Açıklama | Gerekli |
| -------- | ----------- | -------- | 
| ad | Merhaba bağlı hizmetin adı. | Evet | 
| özellikleri - türü | Merhaba bağlantılı hizmet türü. Örneğin: Azure Storage, Azure SQL veritabanı. |
| typeProperties | Merhaba typeProperties bölüm için her bir veri deposu farklı veya ortam işlem öğesine sahip. Bkz: [veri depolarına](#datastores) bağlı hizmetler tüm hello verilerini depolamak için bölüm ve [ortamları işlem](#compute-environments) tüm Merhaba işlem bağlı Hizmetleri |   

## <a name="dataset"></a>Veri kümesi 
Azure Data Factory kümesinde aşağıdaki gibi tanımlanır:

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

Aşağıdaki tablonun hello JSON yukarıda hello özelliklerinde açıklanmaktadır:   

| Özellik | Açıklama | Gerekli | Varsayılan |
| --- | --- | --- | --- |
| ad | Merhaba DataSet'in adı. Bkz: [Azure Data Factory - adlandırma kuralları](data-factory-naming-rules.md) adlandırma kuralları. |Evet |NA |
| type | Merhaba veri kümesi türü. Azure Data Factory ile desteklenen hello türlerinden birini belirtin (örneğin: AzureBlob, AzureSqlTable). Bkz: [veri DEPOLARINA](#data-stores) tüm veri depoları ve veri fabrikası tarafından desteklenen veri türleri hello için bölüm. | 
| yapısı | Merhaba dataset şema. Bu sütun, türleri, vb. içerir. | Hayır |NA |
| typeProperties | Özellikler toohello karşılık gelen seçili türü. Bkz: [veri DEPOLARINA](#data-stores) desteklenen türlerini ve bunların özelliklerini bölümü. |Evet |NA |
| external | Boole veya bir veri kümesi açıkça data factory işlem hattı tarafından üretilir olup olmadığını toospecify bayrağı. |Hayır |False |
| availability | Pencere veya model hello dataset üretim için dilimleme hello işleme hello tanımlar. Model dilimleme hello veri kümesi hakkında daha fazla bilgi için bkz: [zamanlama ve yürütme](data-factory-scheduling-and-execution.md) makalesi. |Evet |NA |
| ilke |Merhaba ölçütleri veya hello dataset dilimler karşılamanız gerekmektedir hello koşulu tanımlar. <br/><br/>Ayrıntılar için bkz [Dataset İlkesi](#Policy) bölümü. |Hayır |NA |

Her sütunda hello **yapısı** bölüm, aşağıdaki özelliklere hello içerir:

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| ad |Merhaba sütunun adı. |Evet |
| type |Merhaba sütununun veri türü.  |Hayır |
| Kültür |.NET tabanlı türü belirtilir ve .NET türü olduğunda kullanılan kültür toobe `Datetime` veya `Datetimeoffset`. Varsayılan değer `en-us`. |Hayır |
| Biçimi |Biçim türü belirtilir ve .NET türü olduğunda kullanılan dize toobe `Datetime` veya `Datetimeoffset`. |Hayır |

Aşağıdaki örneğine hello hello dataset üç sütun sahip `slicetimestamp`, `projectname`, ve `pageviews` ve bunlar türü: dize, dize ve ondalık sırasıyla.

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

Merhaba aşağıdaki tabloda açıklanmaktadır hello kullanabileceğiniz özellikleri **kullanılabilirlik** bölümü:

| Özellik | Açıklama | Gerekli | Varsayılan |
| --- | --- | --- | --- |
| frequency |Veri kümesi dilim üretim Hello zaman birimini belirtir.<br/><br/><b>Sıklık desteklenen</b>: dakika, saat, gün, hafta, ay |Evet |NA |
| interval |Sıklığı çarpanı belirtir<br/><br/>"X sıklığı aralığını" ne sıklıkta hello dilim üretilen belirler.<br/><br/>Saatlik olarak başka bir dilimlenebilir dataset toobe hello varsa, ayarladığınız <b>sıklığı</b> çok<b>saat</b>, ve <b>aralığı</b> çok<b>1</b>.<br/><br/><b>Not</b>: sıklığını dakika belirtirseniz, 15'den küçük hello aralığı toono ayarlamanızı öneririz |Evet |NA |
| stili |Merhaba dilim hello başlangıç/bitiş hello aralığının üretilen olup olmadığını belirtir.<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul><br/><br/>Sıklık tooMonth ayarlanır ve stil tooEndOfInterval hello dilim ayın son günü hello üzerinde üretilmez. Merhaba stili tooStartOfInterval ayarlarsanız hello dilim ayın ilk günü hello üzerinde oluşturulur.<br/><br/>Sıklık tooDay ayarlanır ve stil tooEndOfInterval hello dilim hello hello günün son bir saat üretilmez.<br/><br/>Sıklık tooHour ayarlanır ve stil tooEndOfInterval hello dilim hello hello saat sonunda üretilmez. Örneğin, 13'te – 2 PM dönem için bir dilim için 2 saat hello dilim oluşturulur. |Hayır |EndOfInterval |
| anchorDateTime |Zamanlayıcı toocompute dataset dilim sınırları tarafından kullanılan süre içinde mutlak konum Hello tanımlar. <br/><br/><b>Not</b>: Merhaba AnchorDateTime sahip hello sıklığından daha ayrıntılı tarih kısımlarını sonra hello daha ayrıntılı bölümleri göz ardı edilir. <br/><br/>Örneğin, hello <b>aralığı</b> olan <b>saatlik</b> (sıklığı: saat ve aralığı: 1) ve hello <b>AnchorDateTime</b> içeren <b>dakika ve saniyeleri</b>sonra hello <b>dakika ve saniyeleri</b> hello AnchorDateTime bölümlerini yok sayılır. |Hayır |01/01/0001 |
| uzaklık |Tarafından hangi hello başlangıç ve bitiş tüm veri kümesi dilim gölgeye Timespan. <br/><br/><b>Not</b>: anchorDateTime ve uzaklık belirtilirse, hello birleştirilmiş hello shift sonucudur. |Hayır |NA |

Kullanılabilirlik bölümden hello belirtir, hello çıktı veri kümesi olan üretilen saatlik (veya) giriş veri kümesi kullanılabilir saatlik:

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

Merhaba **İlkesi** gerekir dataset dilimler hello hello koşulu karşılayan veya veri kümesi tanımı bölümünde hello ölçütleri tanımlar.

| İlke adı | Açıklama | Çok uygulanan| Gerekli | Varsayılan |
| --- | --- | --- | --- | --- |
| minimumSizeMB |Merhaba verilerin doğrulayan bir **Azure blob** karşılıyor hello minimum boyut gereksinimlerini (megabayt cinsinden). |Azure Blob |Hayır |NA |
| minimumRows |Merhaba verilerin doğrulayan bir **Azure SQL veritabanı** veya bir **Azure tablo** hello en az satır sayısını içerir. |<ul><li>Azure SQL Database</li><li>Azure tablo</li></ul> |Hayır |NA |

**Örnek:**

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

Azure Data Factory tarafından üretilen bir veri kümesi sürece bunu olarak işaretlenmelidir **dış**. Etkinlik veya ardışık düzen zincirleme kullanılmadığı sürece bu ayar genellikle bir ardışık düzendeki ilk etkinliğin toohello girişleri uygulanır.

| Ad | Açıklama | Gerekli | Varsayılan değer |
| --- | --- | --- | --- |
| dataDelay |Dilim verilen hello için dış veri hello hello kullanılabilirliğine zaman toodelay hello denetleyin. Örneğin, hello veri saatlik varsa, hello onay toosee hello dış veriler kullanılabilir ve hello karşılık gelen dilim hazır dataDelay kullanılarak ertelenebilir.<br/><br/>Yalnızca toohello şimdiki zaman geçerlidir.  Örneğin, 1:00 PM şimdi ise ve bu değer 10 dakikadır hello doğrulama 13: 10'te başlatır.<br/><br/>Bu ayar hello geçmiş dilimleri etkilemez (dilimler dilim bitiş saati + dataDelay < şimdi) herhangi bir gecikme işlenir.<br/><br/>Saat 23: saat gereksinim hello kullanarak toospecified 59'dan büyük `day.hours:minutes:seconds` biçimi. Örneğin, toospecify 24 saat 24:00:00 kullanmayın; Bunun yerine, 1.00:00:00 kullanın. 24:00:00 kullanırsanız, 24 gün (24.00:00:00) kabul edilir. 1 gün ve 4 saat için 1:04:00:00 belirtin. |Hayır |0 |
| Retryınterval |Merhaba hatası ve hello sonraki yeniden deneme girişimi arasındaki süre bekleyin. Bir deneme başarısız olursa hello sonraki deneyin sonra Retryınterval olur. <br/><br/>1:00 PM şimdi ise, biz hello ilk denemede başlayın. Merhaba süresi toocomplete hello ilk doğrulama denetimi hello işlemi başarısız oldu ve 1 dakikalık hello sonraki yeniden deneme ise, 1:00 1 dak (süresi) + 1 dak (yeniden deneme aralığı) = 1:02 PM. <br/><br/>Merhaba son dilim için gecikme yoktur. Merhaba yeniden deneme hemen gerçekleşir. |Hayır |00:01:00 (1 dakika) |
| retryTimeout |yeniden deneme girişimleri için Hello zaman aşımı.<br/><br/>Bu özellik ayarlanırsa too10 dakika hello doğrulama gereksinimlerini toobe 10 dakika içinde tamamlandı. 10 dakika tooperform hello doğrulama uzun sürerse hello zaman aşımına yeniden deneyin.<br/><br/>Tüm denemeleri hello doğrulama için zaman aşımına uğrarsa, hello dilim süresi sona erdi işaretlenir. |Hayır |00:10:00 (10 dakika) |
| maximumRetry |Sayısı toocheck hello dış veri hello kullanılabilirlik için zaman. Merhaba izin verilen en büyük değer 10'dur. |Hayır |3 |


## <a name="data-stores"></a>VERİ DEPOLARI
Merhaba [bağlantılı hizmeti](#linked-service) bağlı hizmetler ortak tooall türleri JSON öğeleri için sağlanan bölüm açıklamalar. Bu bölümde, belirli tooeach veri deposu JSON öğelerini hakkında ayrıntılar sağlar.

Merhaba [Dataset](#dataset) veri kümeleri ortak tooall türleri JSON öğeleri için sağlanan bölüm açıklamalar. Bu bölümde, belirli tooeach veri deposu JSON öğelerini hakkında ayrıntılar sağlar.

Merhaba [etkinlik](#activity) etkinlik ortak tooall türlerini JSON öğeleri için sağlanan bölüm açıklamalar. Bu bölümde bir kopyalama etkinliği kaynak/havuz olarak kullanıldığında, belirli tooeach veri deposu JSON öğelerini hakkında ayrıntılar sağlar.  

Şemalardaki toosee hello JSON bağlantılı hizmeti, veri kümesi, ilgilendiğiniz ve kaynak/havuz hello kopyalama etkinliği için hello hello deposu Hello bağlantısına tıklayın.

| Kategori | Veri deposu 
|:--- |:--- |
| **Azure** |[Azure Blob Depolama](#azure-blob-storage) |
| &nbsp; |[Azure Data Lake Store](#azure-datalake-store) |
| &nbsp; |[Azure Cosmos DB](#azure-cosmos-db) |
| &nbsp; |[Azure SQL Veritabanı](#azure-sql-database) |
| &nbsp; |[Azure SQL Veri Ambarı](#azure-sql-data-warehouse) |
| &nbsp; |[Azure Search](#azure-search) |
| &nbsp; |[Azure Tablo Depolama](#azure-table-storage) |
| **Veritabanları** |[Amazon Redshift](#amazon-redshift) |
| &nbsp; |[IBM DB2](#ibm-db2) |
| &nbsp; |[MySQL](#mysql) |
| &nbsp; |[Oracle](#oracle) |
| &nbsp; |[PostgreSQL](#postgresql) |
| &nbsp; |[SAP Business Warehouse](#sap-business-warehouse) |
| &nbsp; |[SAP HANA](#sap-hana) |
| &nbsp; |[SQL Server](#sql-server) |
| &nbsp; |[Sybase](#sybase) |
| &nbsp; |[Teradata](#teradata) |
| **NoSQL** |[Cassandra](#cassandra) |
| &nbsp; |[MongoDB](#mongodb) |
| **Dosya** |[Amazon S3](#amazon-s3) |
| &nbsp; |[Dosya Sistemi](#file-system) |
| &nbsp; |[FTP](#ftp) |
| &nbsp; |[HDFS](#hdfs) |
| &nbsp; |[SFTP](#sftp) |
| **Diğer** |[HTTP](#http) |
| &nbsp; |[OData](#odata) |
| &nbsp; |[ODBC](#odbc) |
| &nbsp; |[Salesforce](#salesforce) |
| &nbsp; |[Web tablo](#web-table) |

## <a name="azure-blob-storage"></a>Azure Blob Depolama

### <a name="linked-service"></a>Bağlı hizmet
Bağlı hizmetler iki tür vardır: Azure depolama bağlantılı hizmeti ve Azure depolama SAS bağlantılı hizmeti.

#### <a name="azure-storage-linked-service"></a>Azure Storage Bağlı Hizmeti
toolink hello kullanarak Azure depolama hesabı tooa veri fabrikası **hesap anahtarı**, bir Azure Storage bağlı hizmeti oluşturma. toodefine bir Azure depolama bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**AzureStorage**. Ardından hello özelliklerinde aşağıdaki belirtebilirsiniz **typeProperties** bölümü:  

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| connectionString |Tooconnect tooAzure depolama hello connectionString özelliği için gerekli bilgiler belirtin. |Evet |

##### <a name="example"></a>Örnek  

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

#### <a name="azure-storage-sas-linked-service"></a>Azure Storage SAS bağlı hizmeti
Hello Azure depolama bağlı SAS hizmeti bir paylaşılan erişim imzası (SAS) kullanarak toolink bir Azure depolama hesabı tooan Azure data factory sağlar. Kısıtlanmış/zaman sınırlı erişimi hello veri fabrikası hello depolama tooall/özel kaynakları (blob/kapsayıcısı) sağlar. bir Azure depolama bağlı SAS hizmeti toolink paylaşılan erişim imzası kullanarak Azure depolama hesabı tooa veri fabrikası oluşturun. toodefine bir Azure depolama SAS bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**AzureStorageSas**. Ardından hello özelliklerinde aşağıdaki belirtebilirsiniz **typeProperties** bölümü:   

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| sasUri |Blob, kapsayıcı ya da tablo gibi paylaşılan erişim imzası URI toohello Azure Storage kaynakları belirtin. |Evet |

##### <a name="example"></a>Örnek

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

Bu bağlantılı hizmetler hakkında daha fazla bilgi için bkz: [Azure Blob Storage bağlayıcı](data-factory-azure-blob-connector.md#linked-service-properties) makalesi. 

### <a name="dataset"></a>Veri kümesi
toodefine bir Azure Blob dataset kümesi hello **türü** hello kümesinin çok**AzureBlob**. Ardından, Azure Blob belirli hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü: 

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| folderPath |Yol toohello kapsayıcı ve klasöre hello blob depolama. Örnek: myblobcontainer\myblobfolder\ |Evet |
| fileName |Merhaba blob adı. isteğe bağlıdır ve büyük küçük harfe duyarlı dosya adıdır.<br/><br/>Üzerinde bir dosya adı, hello (kopyalama dahil) etkinlik works belirtirseniz, belirli Blob hello.<br/><br/>FileName belirtilmediğinde kopyalama tüm BLOB'lar girdi veri kümesi için hello folderPath içerir.<br/><br/>FileName bir çıkış veri kümesi için belirtilmediğinde oluşturulan hello dosyasının hello adı Bu biçim aşağıdaki hello olacaktır: veri. <Guid>.txt (örnek:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Hayır |
| partitionedBy |partitionedBy isteğe bağlı bir özelliktir. Bunu toospecify dinamik folderPath ve dosya adı için zaman serisi veri kullanabilirsiniz. Örneğin, folderPath için verileri saatte parametreli olabilir. |Hayır |
| Biçimi | şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set hello **türü** biçimi tooone şu değerlerden biri altında özellik. Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler. <br><br> Çok istiyorsanız**olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında hello Biçim bölümü atlayın. |Hayır |
| Sıkıştırma | Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin. Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**. Desteklenen düzeyler: **Optimal** ve **en hızlı**. Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support). |Hayır |

#### <a name="example"></a>Örnek

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
 ```


Daha fazla bilgi için bkz: [Azure Blob bağlayıcı](data-factory-azure-blob-connector.md#dataset-properties) makalesi.

### <a name="blobsource-in-copy-activity"></a>Kopyalama etkinliğinde BlobSource
Bir Azure Blob depolama alanından veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**BlobSource**ve hello özelliklerinde aşağıdaki belirtin ** kaynak ** bölümü:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| Özyinelemeli |Merhaba alt klasörler veya yalnızca hello belirtilen klasör Hello veri yinelemeli olarak okunur olup olmadığını gösterir. |(Varsayılan değer) false değerini true |Hayır |

#### <a name="example-blobsource"></a>Örnek: BlobSource **
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
### <a name="blobsink-in-copy-activity"></a>Kopyalama etkinliğinde BlobSink
Veri tooan Azure Blob Storage kopyalıyorsanız hello ayarlamak **Havuz türü** Merhaba kopya etkinliği çok**BlobSink**ve hello özelliklerinde aşağıdaki belirtin **havuz** bölümü:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| copyBehavior |Merhaba kaynağı BlobSource veya dosya sistemi olduğunda hello kopyalama davranışını tanımlar. |<b>PreserveHierarchy</b>: korur hello hello hedef klasörü içinde dosya hiyerarşisi. Kaynak dosya toosource klasörünün göreli yolu Hello aynı toohello göreli hedef dosya tootarget klasör yoludur.<br/><br/><b>FlattenHierarchy</b>: hello kaynak klasördeki tüm dosyaları hello ilk hedef klasörü düzeyi. Merhaba hedef dosyalara otomatik adına sahip. <br/><br/><b>MergeFiles (varsayılan):</b> hello kaynak klasör tooone dosyasından tüm dosyaları birleştirir. Merhaba dosya/Blob adı belirtilirse, hello birleştirilmiş dosya adı hello belirtilen adı olur; Aksi takdirde otomatik olarak oluşturulan dosya adı olacaktır. |Hayır |

#### <a name="example-blobsink"></a>Örnek: BlobSink

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Daha fazla bilgi için bkz: [Azure Blob bağlayıcı](data-factory-azure-blob-connector.md#copy-activity-properties) makalesi. 

## <a name="azure-data-lake-store"></a>Azure Data Lake Store

### <a name="linked-service"></a>Bağlı hizmet
bir Azure Data Lake Store bağlantılı hizmeti toodefine, kümesi hello tür hello bağlı hizmeti çok**AzureDataLakeStore**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** bölümü:  

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| type | Merhaba type özelliği ayarlanmalıdır: **AzureDataLakeStore** | Evet |
| dataLakeStoreUri | Hello Azure Data Lake Store hesabı bilgilerini belirtin. Biçim aşağıdaki hello olduğu: `https://[accountname].azuredatalakestore.net/webhdfs/v1` veya `adl://[accountname].azuredatalakestore.net/`. | Evet |
| subscriptionId | Azure abonelik kimliği toowhich Data Lake Store aittir. | Havuz için gerekli |
| resourceGroupName | Azure kaynak grubu adı toowhich Data Lake Store aittir. | Havuz için gerekli |
| servicePrincipalId | Merhaba uygulamanın istemci kimliği belirtin. | Evet (hizmet sorumlusu kimlik doğrulaması için) |
| servicePrincipalKey | Merhaba uygulamanın anahtarını belirtin. | Evet (hizmet sorumlusu kimlik doğrulaması için) |
| Kiracı | Uygulamanızın bulunduğu altında Hello Kiracı bilgileri (etki alanı adı veya Kiracı kimliği) belirtin. Vurgulama hello fare hello sağ üst köşesindeki hello Azure portal tarafından alabilir. | Evet (hizmet sorumlusu kimlik doğrulaması için) |
| Yetkilendirme | Tıklatın **Authorize** hello düğmesini **Data Factory düzenleyici** ve hello otomatik olarak oluşturulan yetkilendirme URL'si toothis özelliği atar kimlik bilgilerinizi girin. | Evet (kullanıcı kimlik bilgileri doğrulaması için)|
| SessionID | Merhaba OAuth yetkilendirme oturumundan OAuth oturum kimliği. Her oturum kimliği benzersiz olup yalnızca bir kez kullanılabilir. Data Factory Düzenleyici kullandığınızda bu ayarı otomatik olarak oluşturulur. | Evet (kullanıcı kimlik bilgileri doğrulaması için) |

#### <a name="example-using-service-principal-authentication"></a>Örnek: hizmet asıl kimlik doğrulaması kullanma
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info. Example: microsoft.onmicrosoft.com>"
        }
    }
}
```

#### <a name="example-using-user-credential-authentication"></a>Örnek: kullanıcı kimlik bilgilerinin kullanma
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

Daha fazla bilgi için bkz: [Azure Data Lake Store bağlayıcı](data-factory-azure-datalake-connector.md#linked-service-properties) makalesi. 

### <a name="dataset"></a>Veri kümesi
toodefine bir Azure Data Lake Store dataset kümesi hello **türü** hello kümesinin çok**AzureDataLakeStore**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties**bölümü: 

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| folderPath |Yol toohello kapsayıcı ve hello Azure Data Lake klasöründe depolayın. |Evet |
| fileName |Hello Azure Data Lake Store'da hello dosyasının adı. isteğe bağlıdır ve büyük küçük harfe duyarlı dosya adıdır. <br/><br/>Bir dosya adı belirtirseniz, (kopyalama dahil) hello etkinlik hello belirli dosya üzerinde çalışır.<br/><br/>FileName belirtilmediğinde kopyalama hello folderPath girdi veri kümesi için tüm dosyaları içerir.<br/><br/>FileName bir çıkış veri kümesi için belirtilmediğinde oluşturulan hello dosyasının hello adı Bu biçim aşağıdaki hello olacaktır: veri. <Guid>.txt (örnek:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Hayır |
| partitionedBy |partitionedBy isteğe bağlı bir özelliktir. Bunu toospecify dinamik folderPath ve dosya adı için zaman serisi veri kullanabilirsiniz. Örneğin, folderPath için verileri saatte parametreli olabilir. |Hayır |
| Biçimi | şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set hello **türü** biçimi tooone şu değerlerden biri altında özellik. Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler. <br><br> Çok istiyorsanız**olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında hello Biçim bölümü atlayın. |Hayır |
| Sıkıştırma | Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin. Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**. Desteklenen düzeyler: **Optimal** ve **en hızlı**. Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support). |Hayır |

#### <a name="example"></a>Örnek
```json
{
    "name": "AzureDataLakeStoreInput",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Daha fazla bilgi için bkz: [Azure Data Lake Store bağlayıcı](data-factory-azure-datalake-connector.md#dataset-properties) makalesi. 

### <a name="azure-data-lake-store-source-in-copy-activity"></a>Kopya etkinliği Azure Data Lake Store kaynağında
Bir Azure Data Lake Deposu'ndan veri veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**AzureDataLakeStoreSource**ve hello özelliklerinde aşağıdaki belirtin **kaynağı**  bölümü:

**AzureDataLakeStoreSource** aşağıdaki özelliklere hello destekleyen **typeProperties** bölümü:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| Özyinelemeli |Merhaba alt klasörler veya yalnızca hello belirtilen klasör Hello veri yinelemeli olarak okunur olup olmadığını gösterir. |(Varsayılan değer) false değerini true |Hayır |

#### <a name="example-azuredatalakestoresource"></a>Örnek: AzureDataLakeStoreSource

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureDakeLaketoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureDataLakeStoreInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureDataLakeStoreSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Daha fazla bilgi için bkz: [Azure Data Lake Store bağlayıcı](data-factory-azure-datalake-connector.md#copy-activity-properties) makalesi.

### <a name="azure-data-lake-store-sink-in-copy-activity"></a>Kopya etkinliği Azure Data Lake Store havuzunda
Veri tooan Azure Data Lake Store kopyalıyorsanız hello ayarlamak **Havuz türü** Merhaba kopya etkinliği çok**AzureDataLakeStoreSink**ve hello özelliklerinde aşağıdaki belirtin **havuz**bölümü:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| copyBehavior |Merhaba kopyalama davranışını belirtir. |<b>PreserveHierarchy</b>: korur hello hello hedef klasörü içinde dosya hiyerarşisi. Kaynak dosya toosource klasörünün göreli yolu Hello aynı toohello göreli hedef dosya tootarget klasör yoludur.<br/><br/><b>FlattenHierarchy</b>: hello kaynak klasördeki tüm dosyaları hedef klasörün hello ilk düzeyi oluşturulur. Merhaba hedef dosyaları otomatik adıyla oluşturulur.<br/><br/><b>MergeFiles</b>: hello kaynak klasör tooone dosyasından tüm dosyaları birleştirir. Merhaba dosya/Blob adı belirtilirse, hello birleştirilmiş dosya adı hello belirtilen adı olur; Aksi takdirde otomatik olarak oluşturulan dosya adı olacaktır. |Hayır |

#### <a name="example-azuredatalakestoresink"></a>Örnek: AzureDataLakeStoreSink
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoDataLake",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureDataLakeStoreOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureDataLakeStoreSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Daha fazla bilgi için bkz: [Azure Data Lake Store bağlayıcı](data-factory-azure-datalake-connector.md#copy-activity-properties) makalesi. 

## <a name="azure-cosmos-db"></a>Azure Cosmos DB  

### <a name="linked-service"></a>Bağlı hizmet
bir Azure Cosmos DB toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**DocumentDb**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** Bölüm:  

| **Özellik** | **Açıklama** | **Gerekli** |
| --- | --- | --- |
| connectionString |Gerekli bilgiler tooconnect tooAzure Cosmos DB veritabanı belirtin. |Evet |

#### <a name="example"></a>Örnek

```json
{
    "name": "CosmosDBLinkedService",
    "properties": {
        "type": "DocumentDb",
        "typeProperties": {
            "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
        }
    }
}
```
Daha fazla bilgi için bkz: [Azure Cosmos DB bağlayıcı](data-factory-azure-documentdb-connector.md#linked-service-properties) makalesi.

### <a name="dataset"></a>Veri kümesi
toodefine bir Azure Cosmos DB dataset kümesi hello **türü** hello kümesinin çok**DocumentDbCollection**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** Bölüm: 

| **Özellik** | **Açıklama** | **Gerekli** |
| --- | --- | --- |
| collectionName |Hello Azure Cosmos DB koleksiyon adı. |Evet |

#### <a name="example"></a>Örnek

```json
{
    "name": "PersonCosmosDBTable",
    "properties": {
        "type": "DocumentDbCollection",
        "linkedServiceName": "CosmosDBLinkedService",
        "typeProperties": {
            "collectionName": "Person"
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```
Daha fazla bilgi için bkz: [Azure Cosmos DB bağlayıcı](data-factory-azure-documentdb-connector.md#dataset-properties) makalesi.

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a>Kopya etkinliği Azure Cosmos DB koleksiyon kaynağında
Bir Azure Cosmos Veritabanından veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**DocumentDbCollectionSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** bölümü:


| **Özellik** | **Açıklama** | **İzin verilen değerler** | **Gerekli** |
| --- | --- | --- | --- |
| sorgu |Merhaba sorgu tooread verileri belirtin. |Sorgu dizesindeki Azure Cosmos DB tarafından desteklenir. <br/><br/>Örnek:`SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"` |Hayır <br/><br/>Belirtilmezse, yürütülen SQL deyimini hello:`select <columns defined in structure> from mycollection` |
| nestingSeparator |Belge hello özel karakter tooindicate iç içe geçmiş |Herhangi bir karakter. <br/><br/>Azure Cosmos DB iç içe geçmiş yapılar burada izin verilen bir NoSQL JSON belgeleri için deposudur. Azure Data Factory sağlayan kullanıcı toodenote hiyerarşisi olan nestingSeparator aracılığıyla "." Yukarıdaki örneklerde Hello. Merhaba ayırıcı ile üç alt öğeleri olan hello "Ad" nesne hello kopyalama etkinliği oluşturacaktır ilk, Orta ve son, according too"Name.First", "Name.Middle" ve "Name.Last" hello, tablo tanımı. |Hayır |

#### <a name="example"></a>Örnek

```json
{
    "name": "DocDbToBlobPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "DocumentDbCollectionSource",
                    "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
                    "nestingSeparator": "."
                },
                "sink": {
                    "type": "BlobSink",
                    "blobWriterAddHeader": true,
                    "writeBatchSize": 1000,
                    "writeBatchTimeout": "00:00:59"
                }
            },
            "inputs": [{
                "name": "PersonCosmosDBTable"
            }],
            "outputs": [{
                "name": "PersonBlobTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromCosmosDbToBlob"
        }],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00"
    }
}
```

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a>Kopya etkinliği Azure Cosmos DB koleksiyonu havuzunda
Veri tooAzure Cosmos DB kopyalıyorsanız hello ayarlamak **Havuz türü** Merhaba kopya etkinliği çok**DocumentDbCollectionSink**ve hello özelliklerinde aşağıdaki belirtin **havuz**bölümü:

| **Özellik** | **Açıklama** | **İzin verilen değerler** | **Gerekli** |
| --- | --- | --- | --- |
| nestingSeparator |Bir özel karakter belge iç içe geçmiş hello kaynak sütun adı tooindicate gereklidir. <br/><br/>Örneğin yukarıdaki: `Name.First` hello çıktısında JSON yapısındaki hello Cosmos DB belgede aşağıdaki hello tablo oluşturur:<br/><br/>"Name": {<br/>    "İlk": "John"<br/>}, |Kullanılan tooseparate iç içe geçme düzeyi karakter.<br/><br/>Varsayılan değer `.` (nokta). |Kullanılan tooseparate iç içe geçme düzeyi karakter. <br/><br/>Varsayılan değer `.` (nokta). |
| writeBatchSize |TooAzure Cosmos DB hizmet toocreate belgeleri istekleri paralel sayısı.<br/><br/>Bu özelliği kullanarak Azure Cosmos DB öğesine/öğesinden veri kopyalama işlemi sırasında hello performans ince ayar yapabilirsiniz. Daha fazla paralel istekler tooAzure Cosmos DB gönderilir çünkü writeBatchSize artırdığınızda daha iyi bir performans düşüklüğü görebilir. Ancak, azaltma tooavoid gerekir hello hata iletisi atabilirsiniz: "oranıdır büyük istek".<br/><br/>Azaltmayı bir dizi etkene, belgeler, belgeleri koşullarını sayısı boyutunu dahil olmak üzere, hedef koleksiyon, vb. İlkesi dizin tarafından belirlenir. Kopyalama işlemleri için daha iyi bir koleksiyonu (örneğin, S3) toohave hello çoğu üretilen iş kullanabilirsiniz (2.500 istek birimleri/saniye). |Tamsayı |Hayır (varsayılan: 5) |
| writeBatchTimeout |Zaman aşımına uğramadan önce hello işlemi toocomplete bir süre bekleyin. |TimeSpan<br/><br/> Örnek: "00: 30:00" (30 dakika). |Hayır |

#### <a name="example"></a>Örnek

```json
{
    "name": "BlobToDocDbPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "DocumentDbCollectionSink",
                    "nestingSeparator": ".",
                    "writeBatchSize": 2,
                    "writeBatchTimeout": "00:00:00"
                },
                "translator": {
                    "type": "TabularTranslator",
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix"
                }
            },
            "inputs": [{
                "name": "PersonBlobTableIn"
            }],
            "outputs": [{
                "name": "PersonCosmosDbTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromBlobToCosmosDb"
        }],
        "start": "2016-04-14T00:00:00",
        "end": "2016-04-15T00:00:00"
    }
}
```

Daha fazla bilgi için bkz: [Azure Cosmos DB bağlayıcı](data-factory-azure-documentdb-connector.md#copy-activity-properties) makalesi.

## <a name="azure-sql-database"></a>Azure SQL Database

### <a name="linked-service"></a>Bağlı hizmet
bir Azure SQL veritabanı toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**AzureSqlDatabase**ve hello özelliklerinde aşağıdaki belirtin **typeProperties**bölümü:  

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| connectionString |Tooconnect toohello Azure SQL veritabanı örneğinde hello connectionString özelliği için gerekli bilgiler belirtin. |Evet |

#### <a name="example"></a>Örnek
```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Daha fazla bilgi için bkz: [Azure SQL bağlayıcı](data-factory-azure-sql-connector.md#linked-service-properties) makalesi. 

### <a name="dataset"></a>Veri kümesi
toodefine bir Azure SQL veritabanı veri kümesini kümesi hello **türü** hello kümesinin çok**AzureSqlTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** Bölüm: 

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| tableName |Merhaba tablo veya Görünüm hizmeti bağlı hello Azure SQL veritabanı örneğinde başvurduğu adı. |Evet |

#### <a name="example"></a>Örnek

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
Daha fazla bilgi için bkz: [Azure SQL bağlayıcı](data-factory-azure-sql-connector.md#dataset-properties) makalesi. 

### <a name="sql-source-in-copy-activity"></a>Kopyalama etkinliğinde SQL kaynağı
Bir Azure SQL veritabanından veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**SqlSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** Bölüm:


| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| sqlReaderQuery |Merhaba özel sorgu tooread verileri kullanın. |SQL sorgu dizesi. Örnek: `select * from MyTable`. |Hayır |
| sqlReaderStoredProcedureName |Merhaba adını hello kaynak tablodan veri okuyan yordamı depolanır. |Saklı yordam hello adı. |Hayır |
| storedProcedureParameters |Saklı yordam hello için parametreler. |Ad/değer çiftleri. Adları ve büyük/küçük harf parametrelerinin hello adları ve büyük küçük harf kullanımını hello saklı yordam parametreleri eşleşmelidir. |Hayır |

#### <a name="example"></a>Örnek

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
Daha fazla bilgi için bkz: [Azure SQL bağlayıcı](data-factory-azure-sql-connector.md#copy-activity-properties) makalesi. 

### <a name="sql-sink-in-copy-activity"></a>Kopyalama etkinliği SQL havuzunda
Veri tooAzure SQL veritabanı kopyalıyorsanız hello ayarlamak **Havuz türü** Merhaba kopya etkinliği çok**SqlSink**ve hello özelliklerinde aşağıdaki belirtin **havuz** bölümü:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| writeBatchTimeout |Zaman aşımına uğramadan önce hello toplu ekleme işlemi toocomplete bir süre bekleyin. |TimeSpan<br/><br/> Örnek: "00: 30:00" (30 dakika). |Hayır |
| writeBatchSize |Merhaba arabellek boyutu writeBatchSize ulaştığında veri hello SQL tablosuna ekler. |Tamsayı (satır sayısı) |Hayır (varsayılan: 10000) |
| sqlWriterCleanupScript |Belirli bir dilimle verilerinin temizlenmesini gibi bir sorgu için kopyalama etkinliği tooexecute belirtin. |Sorgu bildirimi. |Hayır |
| Sliceıdentifiercolumnname |Kopyalama etkinliği toofill bir sütun adı, ne zaman yeniden çalıştırılacağını belirli bir dilim verilerini kullanılan tooclean olduğu otomatik dilim tanımlayıcı ile belirtin. |Binary(32) veri türüne sahip bir sütunun sütun adı. |Hayır |
| sqlWriterStoredProcedureName |Merhaba adını upserts (güncelleştirmeler/ekler) verileri hello hedef tabloya saklı yordamı. |Saklı yordam hello adı. |Hayır |
| storedProcedureParameters |Saklı yordam hello için parametreler. |Ad/değer çiftleri. Adları ve büyük/küçük harf parametrelerinin hello adları ve büyük küçük harf kullanımını hello saklı yordam parametreleri eşleşmelidir. |Hayır |
| sqlWriterTableType |Merhaba saklı yordamda kullanılan bir tablo türü adı toobe belirtin. Kopyalama etkinliği taşınan hello veri geçici bir tablo bu tablo türü ile kullanılabilir hale getirir. Saklı yordam kodu sonra varolan verilerin kopyalanmasını hello verileri birleştirebilirsiniz. |Bir tablo türü adı. |Hayır |

#### <a name="example"></a>Örnek

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Daha fazla bilgi için bkz: [Azure SQL bağlayıcı](data-factory-azure-sql-connector.md#copy-activity-properties) makalesi. 

## <a name="azure-sql-data-warehouse"></a>Azure SQL Veri Ambarı

### <a name="linked-service"></a>Bağlı hizmet
Azure SQL Data Warehouse toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**AzureSqlDW**ve hello özelliklerinde aşağıdaki belirtin **typeProperties**bölümü:  

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| connectionString |Tooconnect toohello Azure SQL Data Warehouse örneğine hello connectionString özelliği için gerekli bilgiler belirtin. |Evet |



#### <a name="example"></a>Örnek

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Daha fazla bilgi için bkz: [Azure SQL Data Warehouse Bağlayıcısı](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) makalesi. 

### <a name="dataset"></a>Veri kümesi
toodefine bir Azure SQL veri ambarı veri kümesi kümesi hello **türü** hello kümesinin çok**AzureSqlDWTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties**bölümü: 

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| tableName |Merhaba tablonun veya bağlantılı hizmet hello hello Azure SQL Data Warehouse Veritabanı görünümünde adı ifade eder. |Evet |

#### <a name="example"></a>Örnek

```json
{
    "name": "AzureSqlDWInput",
    "properties": {
    "type": "AzureSqlDWTable",
        "linkedServiceName": "AzureSqlDWLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Daha fazla bilgi için bkz: [Azure SQL Data Warehouse Bağlayıcısı](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) makalesi. 

### <a name="sql-dw-source-in-copy-activity"></a>Kopyalama etkinliğinde SQL DW kaynağı
Azure SQL veri ambarından veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**SqlDWSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak**bölümü:


| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| sqlReaderQuery |Merhaba özel sorgu tooread verileri kullanın. |SQL sorgu dizesi. Örneğin: `select * from MyTable`. |Hayır |
| sqlReaderStoredProcedureName |Merhaba adını hello kaynak tablodan veri okuyan yordamı depolanır. |Saklı yordam hello adı. |Hayır |
| storedProcedureParameters |Saklı yordam hello için parametreler. |Ad/değer çiftleri. Adları ve büyük/küçük harf parametrelerinin hello adları ve büyük küçük harf kullanımını hello saklı yordam parametreleri eşleşmelidir. |Hayır |

#### <a name="example"></a>Örnek

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLDWtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSqlDWInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlDWSource",
                    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Daha fazla bilgi için bkz: [Azure SQL Data Warehouse Bağlayıcısı](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) makalesi. 

### <a name="sql-dw-sink-in-copy-activity"></a>SQL DW havuz kopyalama etkinliğinde
SQL veri ambarı veri tooAzure kopyalıyorsanız hello ayarlamak **Havuz türü** Merhaba kopya etkinliği çok**SqlDWSink**ve hello özelliklerinde aşağıdaki belirtin **havuz** Bölüm:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| sqlWriterCleanupScript |Belirli bir dilimle verilerinin temizlenmesini gibi bir sorgu için kopyalama etkinliği tooexecute belirtin. |Sorgu bildirimi. |Hayır |
| Bulunan'allowpolybase |Gösterir olup olmadığını BULKINSERT mekanizması yerine toouse PolyBase (varsa). <br/><br/> **PolyBase kullanarak SQL Data Warehouse'a veri yolu tooload veri önerilen hello değildir.** |True <br/>False (varsayılan) |Hayır |
| polyBaseSettings |Bir grup hello belirtilebilir özellik **Bulunan'allowpolybase** özelliği çok ayarlanmış**doğru**. |&nbsp; |Hayır |
| rejectValue |Merhaba numarası veya hello sorgu başarısız olmadan önce reddedilemiyor satırları yüzdesini belirtir. <br/><br/>Merhaba seçeneklerinde Reddet hello PolyBase'nın hakkında daha fazla bilgi edinin **bağımsız değişkenleri** bölümünü [CREATE dış TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) konu. |0 (varsayılan), 1, 2... |Hayır |
| rejectType |Merhaba rejectValue seçeneği bir hazır değer veya bir yüzde belirtilen belirtir. |Değer (varsayılan), yüzde |Hayır |
| Havuzu'na ilişkin |Merhaba PolyBase reddedilen satırları hello yüzdesini yeniden hesaplar önce satırları tooretrieve hello sayısını belirler. |1, 2, … |Evet, varsa **rejectType** olan **yüzdesi** |
| useTypeDefault |PolyBase hello metin dosyasından veri aldığında değerlerde eksik toohandle metin dosyaları nasıl ayrılmış belirtir.<br/><br/>Merhaba bağımsız değişkenler bölümünde bu özelliği hakkında daha fazla bilgi [oluşturma EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx). |TRUE, False (varsayılan) |Hayır |
| writeBatchSize |Merhaba arabellek boyutu writeBatchSize ulaştığında veri hello SQL tablosuna ekler. |Tamsayı (satır sayısı) |Hayır (varsayılan: 10000) |
| writeBatchTimeout |Zaman aşımına uğramadan önce hello toplu ekleme işlemi toocomplete bir süre bekleyin. |TimeSpan<br/><br/> Örnek: "00: 30:00" (30 dakika). |Hayır |

#### <a name="example"></a>Örnek

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQLDW",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlDWOutput"
            }],
            "typeProperties": {
                "source": {
                "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlDWSink",
                    "allowPolyBase": true
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Daha fazla bilgi için bkz: [Azure SQL Data Warehouse Bağlayıcısı](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) makalesi. 

## <a name="azure-search"></a>Azure Search

### <a name="linked-service"></a>Bağlı hizmet
Azure Search toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**AzureSearch**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** Bölüm:  

| Özellik | Açıklama | Gerekli |
| -------- | ----------- | -------- |
| URL | Hello Azure Search hizmeti için URL. | Evet |
| anahtar | Hello Azure Search hizmeti için yönetici anahtarı. | Evet |

#### <a name="example"></a>Örnek

```json
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

Daha fazla bilgi için bkz: [Azure Search Bağlayıcısı](data-factory-azure-search-connector.md#linked-service-properties) makalesi.

### <a name="dataset"></a>Veri kümesi
toodefine bir Azure Search dataset kümesi hello **türü** hello kümesinin çok**AzureSearchIndex**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü : 

| Özellik | Açıklama | Gerekli |
| -------- | ----------- | -------- |
| type | Merhaba type özelliği çok ayarlanmalıdır**AzureSearchIndex**.| Evet |
| indexName | Hello Azure Search dizini adı. Veri Fabrikası hello dizin oluşturmaz. Başlangıç dizini, Azure Search'te mevcut olması gerekir. | Evet |

#### <a name="example"></a>Örnek

```json
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties": {
            "indexName": "products"
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
    }
}
```

Daha fazla bilgi için bkz: [Azure Search Bağlayıcısı](data-factory-azure-search-connector.md#dataset-properties) makalesi.

### <a name="azure-search-index-sink-in-copy-activity"></a>Kopya etkinliği Azure arama dizini havuzunda
Veri tooan Azure Search dizini kopyalıyorsanız hello ayarlamak **Havuz türü** Merhaba kopya etkinliği çok**AzureSearchIndexSink**ve hello özelliklerinde aşağıdaki belirtin **havuz**bölümü:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| -------- | ----------- | -------------- | -------- |
| WriteBehavior | Toomerge veya Değiştir bir belgeyi açtığında hello dizinde zaten olup olmadığını belirtir. | Merge (varsayılan)<br/>Karşıya Yükle| Hayır |
| writeBatchSize | Hello arabellek boyutu writeBatchSize ulaştığında hello Azure Search dizinine veri yükler. | 1 too1, 000. Varsayılan değer 1000'dir. | Hayır |

#### <a name="example"></a>Örnek

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoAzureSearchIndex",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureSearchIndexDataset"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "AzureSearchIndexSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Daha fazla bilgi için bkz: [Azure Search Bağlayıcısı](data-factory-azure-search-connector.md#copy-activity-properties) makalesi.

## <a name="azure-table-storage"></a>Azure Table Storage

### <a name="linked-service"></a>Bağlı hizmet
Bağlı hizmetler iki tür vardır: Azure depolama bağlantılı hizmeti ve Azure depolama SAS bağlantılı hizmeti.

#### <a name="azure-storage-linked-service"></a>Azure Storage Bağlı Hizmeti
toolink hello kullanarak Azure depolama hesabı tooa veri fabrikası **hesap anahtarı**, bir Azure Storage bağlı hizmeti oluşturma. toodefine bir Azure depolama bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**AzureStorage**. Ardından hello özelliklerinde aşağıdaki belirtebilirsiniz **typeProperties** bölümü:  

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| type |Merhaba type özelliği ayarlanmalıdır: **AzureStorage** |Evet |
| connectionString |Tooconnect tooAzure depolama hello connectionString özelliği için gerekli bilgiler belirtin. |Evet |

**Örnek:**  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

#### <a name="azure-storage-sas-linked-service"></a>Azure Storage SAS bağlı hizmeti
Hello Azure depolama bağlı SAS hizmeti bir paylaşılan erişim imzası (SAS) kullanarak toolink bir Azure depolama hesabı tooan Azure data factory sağlar. Kısıtlanmış/zaman sınırlı erişimi hello veri fabrikası hello depolama tooall/özel kaynakları (blob/kapsayıcısı) sağlar. bir Azure depolama bağlı SAS hizmeti toolink paylaşılan erişim imzası kullanarak Azure depolama hesabı tooa veri fabrikası oluşturun. toodefine bir Azure depolama SAS bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**AzureStorageSas**. Ardından hello özelliklerinde aşağıdaki belirtebilirsiniz **typeProperties** bölümü:   

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| type |Merhaba type özelliği ayarlanmalıdır: **AzureStorageSas** |Evet |
| sasUri |Blob, kapsayıcı ya da tablo gibi paylaşılan erişim imzası URI toohello Azure Storage kaynakları belirtin. |Evet |

**Örnek:**

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

Bu bağlantılı hizmetler hakkında daha fazla bilgi için bkz: [Azure Table Storage bağlayıcı](data-factory-azure-table-connector.md#linked-service-properties) makalesi. 

### <a name="dataset"></a>Veri kümesi
toodefine bir Azure tablosu veri kümesi kümesi hello **türü** hello kümesinin çok**AzureTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü: 

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| tableName |Bağlantılı hizmetinin hello Azure tablo veritabanı örneğinde Merhaba tablonun adını gösterir. |Evet. Bir tableName bir azureTableSourceQuery belirtildiğinde, tüm hello tablosundan kopyalanan toohello hedef kayıtlarıdır. Bir azureTableSourceQuery de belirtilirse hello sorguyu karşılayan hello tablosundan kopyalanan toohello hedef kayıtlarıdır. |

#### <a name="example"></a>Örnek

```json
{
    "name": "AzureTableInput",
    "properties": {
        "type": "AzureTable",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Bu bağlantılı hizmetler hakkında daha fazla bilgi için bkz: [Azure Table Storage bağlayıcı](data-factory-azure-table-connector.md#dataset-properties) makalesi. 

### <a name="azure-table-source-in-copy-activity"></a>Kopya etkinliği Azure tablo kaynağında
Azure tablo depolamasından veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**AzureTableSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak**bölümü:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| azureTableSourceQuery |Merhaba özel sorgu tooread verileri kullanın. |Azure tablo sorgu dizesi. Merhaba sonraki bölümdeki örneklere bakın. |Hayır. Bir tableName bir azureTableSourceQuery belirtildiğinde, tüm hello tablosundan kopyalanan toohello hedef kayıtlarıdır. Bir azureTableSourceQuery de belirtilirse hello sorguyu karşılayan hello tablosundan kopyalanan toohello hedef kayıtlarıdır. |
| azureTableSourceIgnoreTableNotFound |Tablonun swallow hello özel durum var olup olmadığını gösterir. |TRUE<br/>FALSE |Hayır |

#### <a name="example"></a>Örnek

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureTabletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureTableSource",
                    "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Bu bağlantılı hizmetler hakkında daha fazla bilgi için bkz: [Azure Table Storage bağlayıcı](data-factory-azure-table-connector.md#copy-activity-properties) makalesi. 

### <a name="azure-table-sink-in-copy-activity"></a>Kopya etkinliği Azure tablo havuzunda
Veri tooAzure Table Storage kopyalıyorsanız hello ayarlamak **Havuz türü** Merhaba kopya etkinliği çok**AzureTableSink**ve hello özelliklerinde aşağıdaki belirtin **havuz** Bölüm:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| azureTableDefaultPartitionKeyValue |Merhaba havuzu tarafından kullanılan varsayılan bölüm anahtar değeri. |Bir dize değeri. |Hayır |
| azureTablePartitionKeyName |Değerleri bölüm anahtarları olarak kullanılan hello sütunun adını belirtin. Belirtilmezse, AzureTableDefaultPartitionKeyValue hello bölüm anahtarı olarak kullanılır. |Sütun adı. |Hayır |
| azureTableRowKeyName |Sütun değerleri satır anahtarı olarak kullanılan hello sütunun adını belirtin. Belirtilmezse, her satır için bir GUID kullanın. |Sütun adı. |Hayır |
| azureTableInsertType |başlangıç modu tooinsert verileri Azure tablosuna.<br/><br/>Bu özellik, varolan satırlardan eşleşen bölüm ve satır anahtarlarla hello çıkış tablodaki birleştirilmiş veya değiştirilmesi değerlerine sahip olup olmadığını denetler. <br/><br/>Bu ayarların (birleştirme ve değiştirme) nasıl çalıştığını, ilgili toolearn bkz [ekleme veya birleştirme varlık](https://msdn.microsoft.com/library/azure/hh452241.aspx) ve [ekleme veya değiştirme varlık](https://msdn.microsoft.com/library/azure/hh452242.aspx) konuları. <br/><br> Hello satır düzeyinde, hello tablo düzeyinde değil, bu ayar uygulanır ve her iki seçenek hello giriş yok hello çıkış tablosundaki satırları siler. |Merge (varsayılan)<br/>Değiştir |Hayır |
| writeBatchSize |Merhaba writeBatchSize veya writeBatchTimeout gelindiğinde veri hello Azure tablo ekler. |Tamsayı (satır sayısı) |Hayır (varsayılan: 10000) |
| writeBatchTimeout |Merhaba writeBatchSize veya writeBatchTimeout gelindiğinde veri hello Azure tablo ekler. |TimeSpan<br/><br/>Örnek: "00: 20:00" (20 dakika) |Hayır (varsayılan toostorage istemci varsayılan zaman aşımı değeri 90 saniye) |

#### <a name="example"></a>Örnek

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoTable",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureTableOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureTableSink",
                    "writeBatchSize": 100,
                    "writeBatchTimeout": "01:00:00"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
Bu bağlantılı hizmetler hakkında daha fazla bilgi için bkz: [Azure Table Storage bağlayıcı](data-factory-azure-table-connector.md#copy-activity-properties) makalesi. 

## <a name="amazon-redshift"></a>Amazon RedShift

### <a name="linked-service"></a>Bağlı hizmet
toodefine bir Amazon Redshift bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**AmazonRedshift**ve hello özelliklerinde aşağıdaki belirtin **typeProperties**bölümü:  

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| sunucu |IP adresi veya ana bilgisayar hello Amazon Redshift sunucunun adıdır. |Evet |
| port |Amazon Redshift sunucu hello hello TCP bağlantı noktası sayısı Hello toolisten istemci bağlantıları için kullanır. |Hayır, varsayılan değer: 5439 |
| Veritabanı |Merhaba Amazon Redshift veritabanının adı. |Evet |
| kullanıcı adı |Erişim toohello veritabanı olan kullanıcı adı. |Evet |
| password |Merhaba kullanıcı hesabının parolası. |Evet |

#### <a name="example"></a>Örnek

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties": {
        "type": "AmazonRedshift",
        "typeProperties": {
            "server": "<Amazon Redshift host name or IP address>",
            "port": 5439,
            "database": "<database name>",
            "username": "user",
            "password": "password"
        }
    }
}
```

Daha fazla bilgi için bkz: [Amazon Redshift bağlayıcı](#data-factory-amazon-redshift-connector.md#linked-service-properties) makalesi. 

### <a name="dataset"></a>Veri kümesi
toodefine bir Amazon Redshift dataset kümesi hello **türü** hello kümesinin çok**RelationalTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** Bölüm: 

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| tableName |Bağlantılı hizmetinin hello Amazon Redshift veritabanında Merhaba tablonun adını gösterir. |Hayır (varsa **sorgu** , **RelationalSource** belirtilir) |


#### <a name="example"></a>Örnek

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
Daha fazla bilgi için bkz: [Amazon Redshift bağlayıcı](#data-factory-amazon-redshift-connector.md#dataset-properties) makalesi.

### <a name="relational-source-in-copy-activity"></a>Kopyalama etkinliği ilişkisel kaynağında 
Amazon Redshift veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**RelationalSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** Bölüm:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| sorgu |Merhaba özel sorgu tooread verileri kullanın. |SQL sorgu dizesi. Örneğin: `select * from MyTable`. |Hayır (varsa **tableName** , **dataset** belirtilir) |

#### <a name="example"></a>Örnek

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonRedshiftInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonRedshiftToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
Daha fazla bilgi için bkz: [Amazon Redshift bağlayıcı](#data-factory-amazon-redshift-connector.md#copy-activity-properties) makalesi.

## <a name="ibm-db2"></a>IBM DB2

### <a name="linked-service"></a>Bağlı hizmet
toodefine bir IBM DB2 bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**OnPremisesDB2**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** bölümü:  

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| sunucu |Merhaba DB2 sunucunun adıdır. |Evet |
| Veritabanı |Merhaba DB2 veritabanının adı. |Evet |
| Şema |Merhaba veritabanındaki hello şema adı. Merhaba şema adı büyük/küçük harf duyarlıdır. |Hayır |
| authenticationType |Kimlik doğrulama türü tooconnect toohello DB2 veritabanına kullanılır. Olası değerler şunlardır: Anonim, temel ve Windows. |Evet |
| kullanıcı adı |Temel veya Windows kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin. |Hayır |
| password |Merhaba username için belirtilen hello kullanıcı hesabı için parola belirtin. |Hayır |
| gatewayName |Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi DB2 veritabanına kullanmanız gerekir. |Evet |

#### <a name="example"></a>Örnek
```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
Daha fazla bilgi için bkz: [IBM DB2 Bağlayıcısı](#data-factory-onprem-db2-connector.md#linked-service-properties) makalesi.

### <a name="dataset"></a>Veri kümesi
toodefine bir DB2 veri kümesi, kümesi hello **türü** hello kümesinin çok**RelationalTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü:

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| tableName |Bağlantılı hizmetinin hello DB2 veritabanı örneğinde Merhaba tablonun adını gösterir. Merhaba tableName büyük/küçük harf duyarlıdır. |Hayır (varsa **sorgu** , **RelationalSource** belirtilir) 

#### <a name="example"></a>Örnek
```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Daha fazla bilgi için bkz: [IBM DB2 Bağlayıcısı](#data-factory-onprem-db2-connector.md#dataset-properties) makalesi.

### <a name="relational-source-in-copy-activity"></a>Kopyalama etkinliği ilişkisel kaynağında
IBM DB2'den veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**RelationalSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** bölümü:


| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| sorgu |Merhaba özel sorgu tooread verileri kullanın. |SQL sorgu dizesi. Örneğin: `"query": "select * from "MySchema"."MyTable""`. |Hayır (varsa **tableName** , **dataset** belirtilir) |

#### <a name="example"></a>Örnek
```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"Orders\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "Db2DataSet"
            }],
            "outputs": [{
                "name": "AzureBlobDb2DataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Db2ToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
Daha fazla bilgi için bkz: [IBM DB2 Bağlayıcısı](#data-factory-onprem-db2-connector.md#copy-activity-properties) makalesi.

## <a name="mysql"></a>MySQL

### <a name="linked-service"></a>Bağlı hizmet
bir MySQL toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**OnPremisesMySql**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** bölümü:  

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| sunucu |Merhaba MySQL sunucunun adıdır. |Evet |
| Veritabanı |Merhaba MySQL veritabanının adı. |Evet |
| Şema |Merhaba veritabanındaki hello şema adı. |Hayır |
| authenticationType |Kimlik doğrulama türü tooconnect toohello MySQL veritabanı kullanılır. Olası değerler şunlardır: `Basic`. |Evet |
| kullanıcı adı |Kullanıcı adı tooconnect toohello MySQL veritabanı belirtin. |Evet |
| password |Belirttiğiniz hello kullanıcı hesabı için parola belirtin. |Evet |
| gatewayName |Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi MySQL veritabanına kullanmanız gerekir. |Evet |

#### <a name="example"></a>Örnek

```json
{
    "name": "OnPremMySqlLinkedService",
    "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
            "server": "<server name>",
            "database": "<database name>",
            "schema": "<schema name>",
            "authenticationType": "<authentication type>",
            "userName": "<user name>",
            "password": "<password>",
            "gatewayName": "<gateway>"
        }
    }
}
```

Daha fazla bilgi için bkz: [MySQL bağlayıcı](data-factory-onprem-mysql-connector.md#linked-service-properties) makalesi. 

### <a name="dataset"></a>Veri kümesi
toodefine bir MySQL veri kümesi hello **türü** hello kümesinin çok**RelationalTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü: 

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| tableName |Merhaba bağlı MySQL veritabanı örneğinde Merhaba tablonun adını gösterir. |Hayır (varsa **sorgu** , **RelationalSource** belirtilir) |

#### <a name="example"></a>Örnek

```json
{
    "name": "MySqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremMySqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
Daha fazla bilgi için bkz: [MySQL bağlayıcı](data-factory-onprem-mysql-connector.md#dataset-properties) makalesi. 

### <a name="relational-source-in-copy-activity"></a>Kopyalama etkinliği ilişkisel kaynağında
Bir MySQL veritabanından veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**RelationalSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** Bölüm:


| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| sorgu |Merhaba özel sorgu tooread verileri kullanın. |SQL sorgu dizesi. Örneğin: `select * from MyTable`. |Hayır (varsa **tableName** , **dataset** belirtilir) |


#### <a name="example"></a>Örnek
```json
{
    "name": "CopyMySqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MySqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobMySqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MySqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Daha fazla bilgi için bkz: [MySQL bağlayıcı](data-factory-onprem-mysql-connector.md#copy-activity-properties) makalesi. 

## <a name="oracle"></a>Oracle 

### <a name="linked-service"></a>Bağlı hizmet
bir Oracle toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**OnPremisesOracle**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** Bölüm:  

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| driverType | Hangi sürücü toouse toocopy verilerden belirtin / tooOracle veritabanı. İzin verilen değerler **Microsoft** veya **ODP** (varsayılan). Bkz: [desteklenen sürümü ve yükleme](#supported-versions-and-installation) sürücü ayrıntıları bölümü. | Hayır |
| connectionString | Tooconnect toohello Oracle veritabanı örneği hello connectionString özelliği için gerekli bilgiler belirtin. | Evet |
| gatewayName | Kullanılan tooconnect toohello olan şirket içi Oracle Sunucusu hello ağ geçidi adı |Evet |

#### <a name="example"></a>Örnek
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString": "Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Daha fazla bilgi için bkz: [Oracle bağlayıcı](data-factory-onprem-oracle-connector.md#linked-service-properties) makalesi.

### <a name="dataset"></a>Veri kümesi
toodefine bir Oracle veri kümesini kümesi hello **türü** hello kümesinin çok**OracleTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü: 

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| tableName |Merhaba bağlantılı hizmet hello Oracle veritabanı Merhaba tablonun adını gösterir. |Hayır (varsa **oracleReaderQuery** , **OracleSource** belirtilir) |

#### <a name="example"></a>Örnek

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2016-02-27T12:00:00",
            "frequency": "Hour"
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
Daha fazla bilgi için bkz: [Oracle bağlayıcı](data-factory-onprem-oracle-connector.md#dataset-properties) makalesi.

### <a name="oracle-source-in-copy-activity"></a>Kopyalama etkinliği Oracle kaynağında
Bir Oracle veritabanından veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**OracleSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** Bölüm:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| oracleReaderQuery |Merhaba özel sorgu tooread verileri kullanın. |SQL sorgu dizesi. Örneğin, `select * from MyTable` <br/><br/>Belirtilmezse, yürütülen SQL deyimini hello:`select * from MyTable` |Hayır (varsa **tableName** , **dataset** belirtilir) |

#### <a name="example"></a>Örnek

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "OracletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " OracleInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "OracleSource",
                    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Daha fazla bilgi için bkz: [Oracle bağlayıcı](data-factory-onprem-oracle-connector.md#copy-activity-properties) makalesi.

### <a name="oracle-sink-in-copy-activity"></a>Kopyalama etkinliği Oracle havuzunda
Veri tooam Oracle veritabanı kopyalıyorsanız hello ayarlamak **Havuz türü** Merhaba kopya etkinliği çok**OracleSink**ve hello özelliklerinde aşağıdaki belirtin **havuz** bölümü:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| writeBatchTimeout |Zaman aşımına uğramadan önce hello toplu ekleme işlemi toocomplete bir süre bekleyin. |TimeSpan<br/><br/> Örnek: 00:30:00 (30 dakika). |Hayır |
| writeBatchSize |Merhaba arabellek boyutu writeBatchSize ulaştığında veri hello SQL tablosuna ekler. |Tamsayı (satır sayısı) |Hayır (varsayılan: 100) |
| sqlWriterCleanupScript |Belirli bir dilimle verilerinin temizlenmesini gibi bir sorgu için kopyalama etkinliği tooexecute belirtin. |Sorgu bildirimi. |Hayır |
| Sliceıdentifiercolumnname |Kopyalama etkinliği toofill sütun adı, ne zaman yeniden çalıştırılacağını belirli bir dilim verilerini kullanılan tooclean olduğu otomatik dilim tanımlayıcı ile belirtin. |Binary(32) veri türüne sahip bir sütunun sütun adı. |Hayır |

#### <a name="example"></a>Örnek
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-05T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoOracle",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "OracleOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "OracleSink"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
Daha fazla bilgi için bkz: [Oracle bağlayıcı](data-factory-onprem-oracle-connector.md#copy-activity-properties) makalesi.

## <a name="postgresql"></a>PostgreSQL

### <a name="linked-service"></a>Bağlı hizmet
bir PostgreSQL toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**OnPremisesPostgreSql**ve hello özelliklerinde aşağıdaki belirtin **typeProperties**bölümü:  

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| sunucu |Merhaba PostgreSQL sunucunun adıdır. |Evet |
| Veritabanı |Merhaba PostgreSQL veritabanının adı. |Evet |
| Şema |Merhaba veritabanındaki hello şema adı. Merhaba şema adı büyük/küçük harf duyarlıdır. |Hayır |
| authenticationType |Kimlik doğrulama türü tooconnect toohello PostgreSQL veritabanına kullanılır. Olası değerler şunlardır: Anonim, temel ve Windows. |Evet |
| kullanıcı adı |Temel veya Windows kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin. |Hayır |
| password |Merhaba username için belirtilen hello kullanıcı hesabı için parola belirtin. |Hayır |
| gatewayName |Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi PostgreSQL veritabanına kullanmanız gerekir. |Evet |

#### <a name="example"></a>Örnek

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
Daha fazla bilgi için bkz: [PostgreSQL bağlayıcı](data-factory-onprem-postgresql-connector.md#linked-service-properties) makalesi.

### <a name="dataset"></a>Veri kümesi
toodefine bir PostgreSQL veri kümesi hello **türü** hello kümesinin çok**RelationalTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü: 

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| tableName |Merhaba bağlı PostgreSQL veritabanı örneğinde Merhaba tablonun adını gösterir. Merhaba tableName büyük/küçük harf duyarlıdır. |Hayır (varsa **sorgu** , **RelationalSource** belirtilir) |

#### <a name="example"></a>Örnek
```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
Daha fazla bilgi için bkz: [PostgreSQL bağlayıcı](data-factory-onprem-postgresql-connector.md#dataset-properties) makalesi.

### <a name="relational-source-in-copy-activity"></a>Kopyalama etkinliği ilişkisel kaynağında
Bir PostgreSQL veritabanından veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**RelationalSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak**bölümü:


| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| sorgu |Merhaba özel sorgu tooread verileri kullanın. |SQL sorgu dizesi. Örneğin: "sorgu": "seçin * gelen \"MySchema\".\" MyTable\"". |Hayır (varsa **tableName** , **dataset** belirtilir) |

#### <a name="example"></a>Örnek

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"public\".\"usstates\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "PostgreSqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobPostgreSqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "PostgreSqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Daha fazla bilgi için bkz: [PostgreSQL bağlayıcı](data-factory-onprem-postgresql-connector.md#copy-activity-properties) makalesi.

## <a name="sap-business-warehouse"></a>SAP Business Warehouse


### <a name="linked-service"></a>Bağlı hizmet
toodefine SAP Business Warehouse (BW) bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**SapBw**ve hello özelliklerinde aşağıdaki belirtin **typeProperties**bölümü:  

Özellik | Açıklama | İzin verilen değerler | Gerekli
-------- | ----------- | -------------- | --------
sunucu | Hangi hello SAP BW örneği bulunduğu hello sunucusunun adı. | Dize | Evet
systemNumber | SAP BW sistem hello sistem sayısı. | Bir dize olarak gösterilen iki basamaklı ondalık sayı. | Evet
istemci kimliği | Merhaba SAP W sistem hello istemcisinde istemci kimliği. | Bir dize olarak gösterilen üç basamaklı ondalık sayı. | Evet
kullanıcı adı | Erişim toohello SAP sunucusuna sahip hello kullanıcı adı | Dize | Evet
password | Merhaba kullanıcının parolası. | Dize | Evet
gatewayName | Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi SAP BW örneğini kullanmanız gerekir. | Dize | Evet
encryptedCredential | şifrelenmiş hello kimlik dizesi. | Dize | Hayır

#### <a name="example"></a>Örnek

```json
{
    "name": "SapBwLinkedService",
    "properties": {
        "type": "SapBw",
        "typeProperties": {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Daha fazla bilgi için bkz: [SAP Business Warehouse Bağlayıcısı](data-factory-sap-business-warehouse-connector.md#linked-service-properties) makalesi. 

### <a name="dataset"></a>Veri kümesi
toodefine bir SAP BW veri kümesi hello **türü** hello kümesinin çok**RelationalTable**. Merhaba SAP BW veri kümesi türü için desteklenen türüne özgü özellikler yok **RelationalTable**.  

#### <a name="example"></a>Örnek

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
Daha fazla bilgi için bkz: [SAP Business Warehouse Bağlayıcısı](data-factory-sap-business-warehouse-connector.md#dataset-properties) makalesi. 

### <a name="relational-source-in-copy-activity"></a>Kopyalama etkinliği ilişkisel kaynağında
SAP Business Warehouse veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**RelationalSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak**bölümü:


| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| sorgu | Merhaba MDX Sorgusu tooread veri hello SAP BW örneğinden belirtir. | MDX Sorgusu. | Evet |

#### <a name="example"></a>Örnek

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<MDX query for SAP BW>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapBwDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapBwToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

Daha fazla bilgi için bkz: [SAP Business Warehouse Bağlayıcısı](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) makalesi. 

## <a name="sap-hana"></a>SAP HANA

### <a name="linked-service"></a>Bağlı hizmet
SAP HANA toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**SapHana**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** bölümü:  

Özellik | Açıklama | İzin verilen değerler | Gerekli
-------- | ----------- | -------------- | --------
sunucu | Hangi hello SAP HANA örneği bulunduğu hello sunucusunun adı. Sunucunuz özelleştirilmiş bir bağlantı noktası kullanıyorsa belirtin `server:port`. | Dize | Evet
authenticationType | Kimlik doğrulama türü. | Dize. "Temel" veya "Windows" | Evet 
kullanıcı adı | Erişim toohello SAP sunucusuna sahip hello kullanıcı adı | Dize | Evet
password | Merhaba kullanıcının parolası. | Dize | Evet
gatewayName | Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi SAP HANA örneğini kullanmanız gerekir. | Dize | Evet
encryptedCredential | şifrelenmiş hello kimlik dizesi. | Dize | Hayır

#### <a name="example"></a>Örnek

```json
{
    "name": "SapHanaLinkedService",
    "properties": {
        "type": "SapHana",
        "typeProperties": {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```
Daha fazla bilgi için bkz: [SAP HANA bağlayıcı](data-factory-sap-hana-connector.md#linked-service-properties) makalesi.
 
### <a name="dataset"></a>Veri kümesi
toodefine bir SAP HANA veri kümesi hello **türü** hello kümesinin çok**RelationalTable**. Merhaba SAP HANA dataset türü için desteklenen türüne özgü özellikler yok **RelationalTable**. 

#### <a name="example"></a>Örnek

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
Daha fazla bilgi için bkz: [SAP HANA bağlayıcı](data-factory-sap-hana-connector.md#dataset-properties) makalesi. 

### <a name="relational-source-in-copy-activity"></a>Kopyalama etkinliği ilişkisel kaynağında
SAP HANA veri deposundan veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**RelationalSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak**bölümü:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| sorgu | Merhaba SQL sorgu tooread veri hello SAP HANA örneğinden belirtir. | SQL sorgusu. | Evet |


#### <a name="example"></a>Örnek


```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<SQL Query for HANA>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapHanaDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapHanaToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

Daha fazla bilgi için bkz: [SAP HANA bağlayıcı](data-factory-sap-hana-connector.md#copy-activity-properties) makalesi.


## <a name="sql-server"></a>SQL Server

### <a name="linked-service"></a>Bağlı hizmet
Bağlı hizmet türü oluşturma **OnPremisesSqlServer** toolink bir şirket içi SQL Server veritabanı tooa data factory. Aşağıdaki tablonun hello JSON öğeleri belirli tooon şirket içi SQL Server bağlantılı hizmet açıklamasını sağlar.

Aşağıdaki tablonun hello JSON öğeleri belirli tooSQL Server bağlantılı hizmeti için bir açıklama sağlar.

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| type |Merhaba type özelliği ayarlanmalıdır: **OnPremisesSqlServer**. |Evet |
| connectionString |SQL kimlik doğrulaması veya Windows kimlik doğrulaması kullanarak tooconnect toohello şirket içi SQL Server veritabanı gerekli connectionString bilgiler belirtin. |Evet |
| gatewayName |Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi SQL Server veritabanını kullanmanız gerekir. |Evet |
| kullanıcı adı |Windows kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin. Örnek: **domainname\\kullanıcıadı**. |Hayır |
| password |Merhaba username için belirtilen hello kullanıcı hesabı için parola belirtin. |Hayır |

Hello kullanarak kimlik bilgilerini şifrelemek **yeni AzureRmDataFactoryEncryptValue** cmdlet'i ve bunları hello aşağıdaki örnekte gösterildiği gibi hello bağlantı dizesinde kullanabilirsiniz (**EncryptedCredential** özellik):  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a>Örnek: SQL kimlik doğrulaması kullanmak için JSON

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a>Örnek: JSON'ı Windows kimlik doğrulaması kullanma

Kullanıcı adı ve parolası belirtilmişse, ağ geçidi bunları tooimpersonate hello kullanır belirtilen kullanıcı hesabı tooconnect toohello şirket içi SQL Server veritabanı. Aksi takdirde, ağ geçidi toohello SQL Server doğrudan hello güvenlik bağlamında ağ geçidi (kendi başlangıç hesabı) ile bağlanır.

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Daha fazla bilgi için bkz: [SQL Server Bağlayıcısı](data-factory-sqlserver-connector.md#linked-service-properties) makalesi. 

### <a name="dataset"></a>Veri kümesi
toodefine bir SQL Server veri kümesi hello **türü** hello kümesinin çok**SqlServerTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü: 

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| tableName |Merhaba tablo veya Görünüm hizmeti bağlı hello SQL Server veritabanı örneğinde başvurduğu adı. |Evet |

#### <a name="example"></a>Örnek
```json
{
    "name": "SqlServerInput",
    "properties": {
        "type": "SqlServerTable",
        "linkedServiceName": "SqlServerLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Daha fazla bilgi için bkz: [SQL Server Bağlayıcısı](data-factory-sqlserver-connector.md#dataset-properties) makalesi. 

### <a name="sql-source-in-copy-activity"></a>Kopyalama etkinliğinde SQL kaynağı
Bir SQL Server veritabanından veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**SqlSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** Bölüm:


| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| sqlReaderQuery |Merhaba özel sorgu tooread verileri kullanın. |SQL sorgu dizesi. Örneğin: `select * from MyTable`. Birden çok tablo hello girdi veri kümesi tarafından başvurulan hello veritabanından başvurabilir. Belirtilmezse, yürütülen SQL deyimini hello: MyTable arasından seçin. |Hayır |
| sqlReaderStoredProcedureName |Merhaba adını hello kaynak tablodan veri okuyan yordamı depolanır. |Saklı yordam hello adı. |Hayır |
| storedProcedureParameters |Saklı yordam hello için parametreler. |Ad/değer çiftleri. Adları ve büyük/küçük harf parametrelerinin hello adları ve büyük küçük harf kullanımını hello saklı yordam parametreleri eşleşmelidir. |Hayır |

Merhaba, **sqlReaderQuery** Merhaba SqlSource, hello kopyalama etkinliği çalıştıran bu sorguyu hello SQL Server veritabanı kaynak tooget hello verileri karşı belirtilir.

Alternatif olarak, bir saklı yordam hello belirterek belirleyebileceğiniz **sqlReaderStoredProcedureName** ve **storedProcedureParameters** (Merhaba saklı yordam parametreleri alır).

SqlReaderQuery veya sqlReaderStoredProcedureName belirtmezseniz hello yapısı bölümünde tanımlanan hello sütunlar kullanılan toobuild seçme sorgusu toorun hello SQL Server veritabanına karşı'dır. Merhaba veri kümesi tanımı hello yapısına sahip değil, tüm sütunlar hello tablosundan seçilir.

> [!NOTE]
> Kullandığınızda, **sqlReaderStoredProcedureName**, hala toospecify bir değer hello için gereksinim duyduğunuz **tableName** JSON hello kümesindeki özelliği. Yine de bu tabloya karşı gerçekleştirilen başka doğrulama vardır.


#### <a name="example"></a>Örnek
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Bu örnekte, **sqlReaderQuery** SqlSource hello için belirtilir. Merhaba kopyalama etkinliği bu sorguyu SQL Server veritabanı kaynak tooget hello verileri hello karşı çalışır. Alternatif olarak, bir saklı yordam hello belirterek belirleyebileceğiniz **sqlReaderStoredProcedureName** ve **storedProcedureParameters** (Merhaba saklı yordam parametreleri alır). Merhaba sqlReaderQuery hello girdi veri kümesi tarafından başvurulan hello veritabanı içinde birden çok tablo başvuruda bulunabilir. Bu veri kümesi'nin tableName typeProperty hello olarak ayarlanmış sınırlı tooonly hello tablosu değil.

SqlReaderQuery veya sqlReaderStoredProcedureName belirtmezseniz hello yapısı bölümünde tanımlanan hello sütunlar kullanılan toobuild seçme sorgusu toorun hello SQL Server veritabanına karşı'dır. Merhaba veri kümesi tanımı hello yapısına sahip değil, tüm sütunlar hello tablosundan seçilir.

Daha fazla bilgi için bkz: [SQL Server Bağlayıcısı](data-factory-sqlserver-connector.md#copy-activity-properties) makalesi. 

### <a name="sql-sink-in-copy-activity"></a>Kopyalama etkinliği SQL havuzunda
Veri tooa SQL Server veritabanı kopyalıyorsanız hello ayarlamak **Havuz türü** Merhaba kopya etkinliği çok**SqlSink**ve hello özelliklerinde aşağıdaki belirtin **havuz** bölümü:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| writeBatchTimeout |Zaman aşımına uğramadan önce hello toplu ekleme işlemi toocomplete bir süre bekleyin. |TimeSpan<br/><br/> Örnek: "00: 30:00" (30 dakika). |Hayır |
| writeBatchSize |Merhaba arabellek boyutu writeBatchSize ulaştığında veri hello SQL tablosuna ekler. |Tamsayı (satır sayısı) |Hayır (varsayılan: 10000) |
| sqlWriterCleanupScript |Belirli bir dilimle verilerinin temizlenmesini gibi kopyalama etkinliği tooexecute için sorgu belirtin. Daha fazla bilgi için bkz: [Yinelenebilirlik](#repeatability-during-copy) bölümü. |Sorgu bildirimi. |Hayır |
| Sliceıdentifiercolumnname |Kopyalama etkinliği toofill sütun adı, ne zaman yeniden çalıştırılacağını belirli bir dilim verilerini kullanılan tooclean olduğu otomatik dilim tanımlayıcı ile belirtin. Daha fazla bilgi için bkz: [Yinelenebilirlik](#repeatability-during-copy) bölümü. |Binary(32) veri türüne sahip bir sütunun sütun adı. |Hayır |
| sqlWriterStoredProcedureName |Merhaba adını upserts (güncelleştirmeler/ekler) verileri hello hedef tabloya saklı yordamı. |Saklı yordam hello adı. |Hayır |
| storedProcedureParameters |Saklı yordam hello için parametreler. |Ad/değer çiftleri. Adları ve büyük/küçük harf parametrelerinin hello adları ve büyük küçük harf kullanımını hello saklı yordam parametreleri eşleşmelidir. |Hayır |
| sqlWriterTableType |Merhaba saklı yordamda kullanılan tablo türü adı toobe belirtin. Kopyalama etkinliği taşınan hello veri geçici bir tablo bu tablo türü ile kullanılabilir hale getirir. Saklı yordam kodu sonra varolan verilerin kopyalanmasını hello verileri birleştirebilirsiniz. |Bir tablo türü adı. |Hayır |

#### <a name="example"></a>Örnek
Merhaba ardışık düzen içeren bir kopyalama etkinliği, yapılandırılmış toouse bu girdi ve çıktı veri kümeleri ve zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**BlobSource** ve **havuz** türü olarak ayarlanmış çok**SqlSink**.

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": " SqlServerOutput "
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Daha fazla bilgi için bkz: [SQL Server Bağlayıcısı](data-factory-sqlserver-connector.md#copy-activity-properties) makalesi. 

## <a name="sybase"></a>Sybase

### <a name="linked-service"></a>Bağlı hizmet
bir Sybase toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**OnPremisesSybase**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** Bölüm:  

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| sunucu |Merhaba Sybase sunucunun adıdır. |Evet |
| Veritabanı |Merhaba Sybase veritabanının adı. |Evet |
| Şema |Merhaba veritabanındaki hello şema adı. |Hayır |
| authenticationType |Kimlik doğrulama türü tooconnect toohello Sybase veritabanına kullanılır. Olası değerler şunlardır: Anonim, temel ve Windows. |Evet |
| kullanıcı adı |Temel veya Windows kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin. |Hayır |
| password |Merhaba username için belirtilen hello kullanıcı hesabı için parola belirtin. |Hayır |
| gatewayName |Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi Sybase veritabanına kullanmanız gerekir. |Evet |

#### <a name="example"></a>Örnek
```json
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

Daha fazla bilgi için bkz: [Sybase bağlayıcı](data-factory-onprem-sybase-connector.md#linked-service-properties) makalesi. 

### <a name="dataset"></a>Veri kümesi
toodefine bir Sybase veri kümesi hello **türü** hello kümesinin çok**RelationalTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü: 

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| tableName |Merhaba bağlı Sybase veritabanı örneğinde Merhaba tablonun adını gösterir. |Hayır (varsa **sorgu** , **RelationalSource** belirtilir) |

#### <a name="example"></a>Örnek

```json
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Daha fazla bilgi için bkz: [Sybase bağlayıcı](data-factory-onprem-sybase-connector.md#dataset-properties) makalesi. 

### <a name="relational-source-in-copy-activity"></a>Kopyalama etkinliği ilişkisel kaynağında
Bir Sybase veritabanından veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**RelationalSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** Bölüm:


| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| sorgu |Merhaba özel sorgu tooread verileri kullanın. |SQL sorgu dizesi. Örneğin: `select * from MyTable`. |Hayır (varsa **tableName** , **dataset** belirtilir) |

#### <a name="example"></a>Örnek

```json
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from DBA.Orders"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "SybaseDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobSybaseDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SybaseToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Daha fazla bilgi için bkz: [Sybase bağlayıcı](data-factory-onprem-sybase-connector.md#copy-activity-properties) makalesi.

## <a name="teradata"></a>Teradata

### <a name="linked-service"></a>Bağlı hizmet
bir Teradata toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**OnPremisesTeradata**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** Bölüm:  

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| sunucu |Merhaba Teradata sunucunun adıdır. |Evet |
| authenticationType |Kimlik doğrulama türü tooconnect toohello Teradata veritabanına kullanılır. Olası değerler şunlardır: Anonim, temel ve Windows. |Evet |
| kullanıcı adı |Temel veya Windows kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin. |Hayır |
| password |Merhaba username için belirtilen hello kullanıcı hesabı için parola belirtin. |Hayır |
| gatewayName |Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi Teradata veritabanına kullanmanız gerekir. |Evet |

#### <a name="example"></a>Örnek
```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

Daha fazla bilgi için bkz: [Teradata bağlayıcı](data-factory-onprem-teradata-connector.md#linked-service-properties) makalesi.

### <a name="dataset"></a>Veri kümesi
toodefine bir Teradata Blob veri kümesi hello **türü** hello kümesinin çok**RelationalTable**. Şu anda hello Teradata veri kümesi için desteklenen tür özellik yok. 

#### <a name="example"></a>Örnek
```json
{
    "name": "TeradataDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Daha fazla bilgi için bkz: [Teradata bağlayıcı](data-factory-onprem-teradata-connector.md#dataset-properties) makalesi.

### <a name="relational-source-in-copy-activity"></a>Kopyalama etkinliği ilişkisel kaynağında
Bir Teradata veritabanından veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**RelationalSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak**bölümü:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| sorgu |Merhaba özel sorgu tooread verileri kullanın. |SQL sorgu dizesi. Örneğin: `select * from MyTable`. |Evet |

#### <a name="example"></a>Örnek

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "TeradataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobTeradataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "TeradataToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "isPaused": false
    }
}
```

Daha fazla bilgi için bkz: [Teradata bağlayıcı](data-factory-onprem-teradata-connector.md#copy-activity-properties) makalesi.

## <a name="cassandra"></a>Cassandra


### <a name="linked-service"></a>Bağlı hizmet
toodefine bir Cassandra bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**OnPremisesCassandra**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** Bölüm:  

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| ana bilgisayar |Bir veya daha fazla IP adresleri veya ana bilgisayar adlarını Cassandra sunucuları.<br/><br/>IP adresi veya ana bilgisayar adları tooconnect tooall sunucuları virgülle ayrılmış listesini eşzamanlı olarak belirtin. |Evet |
| port |Merhaba Cassandra sunucu hello TCP bağlantı noktası toolisten istemci bağlantıları için kullanır. |Hayır, varsayılan değer: 9042 |
| authenticationType |Basic veya Anonymous |Evet |
| kullanıcı adı |Merhaba kullanıcı hesabının kullanıcı adını belirtin. |Evet, authenticationType tooBasic ayarlarsanız. |
| password |Merhaba kullanıcı hesabı için parola belirtin. |Evet, authenticationType tooBasic ayarlarsanız. |
| gatewayName |kullanılan tooconnect toohello şirket içi Cassandra veritabanı hello ağ geçidi Hello adı. |Evet |
| encryptedCredential |Merhaba ağ geçidi tarafından şifrelenmiş kimlik bilgileri. |Hayır |

#### <a name="example"></a>Örnek

```json
{
    "name": "CassandraLinkedService",
    "properties": {
        "type": "OnPremisesCassandra",
        "typeProperties": {
            "authenticationType": "Basic",
            "host": "<cassandra server name or IP address>",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Daha fazla bilgi için bkz: [Cassandra bağlayıcı](data-factory-onprem-cassandra-connector.md#linked-service-properties) makalesi. 

### <a name="dataset"></a>Veri kümesi
toodefine bir Cassandra veri kümesi hello **türü** hello kümesinin çok**CassandraTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü: 

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| keyspace |Merhaba keyspace veya Cassandra veritabanındaki şema adı. |Evet (varsa **sorgu** için **CassandraSource** tanımlı değil). |
| tableName |Cassandra veritabanındaki Merhaba tablonun adı. |Evet (varsa **sorgu** için **CassandraSource** tanımlı değil). |

#### <a name="example"></a>Örnek

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "<key space>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Daha fazla bilgi için bkz: [Cassandra bağlayıcı](data-factory-onprem-cassandra-connector.md#dataset-properties) makalesi. 

### <a name="cassandra-source-in-copy-activity"></a>Kopyalama etkinliği Cassandra kaynağında
Cassandra veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**CassandraSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** bölümü :

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| sorgu |Merhaba özel sorgu tooread verileri kullanın. |SQL-92 sorgusu veya CQL sorgusu. Bkz: [CQL başvuru](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html). <br/><br/>SQL sorgusu kullanırken belirtin **keyspace name.table adı** tooquery istediğiniz toorepresent hello tablo. |Hayır (tableName ve veri kümesi üzerinde keyspace tanımlanmışsa). |
| consistencyLevel |kaç tane çoğaltmaları veri toohello istemci uygulaması döndürmeden önce tooa Okuma isteği yanıtlamalısınız Hello tutarlılık düzeyi belirtir. İstek veri toosatisfy hello okumak için Cassandra denetimleri çoğaltmaları belirtilen sayıda hello. |BİR, İKİ, ÜÇ, ÇEKİRDEK, TÜMÜ, LOCAL_QUORUM EACH_QUORUM, LOCAL_ONE. Bkz: [veri tutarlılığını yapılandırma](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) Ayrıntılar için. |Hayır. Varsayılan değer biridir. |

#### <a name="example"></a>Örnek
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "CassandraInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Daha fazla bilgi için bkz: [Cassandra bağlayıcı](data-factory-onprem-cassandra-connector.md#copy-activity-properties) makalesi.

## <a name="mongodb"></a>MongoDB

### <a name="linked-service"></a>Bağlı hizmet
toodefine bir MongoDB bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**OnPremisesMongoDB**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** Bölüm:  

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| sunucu |IP adresi veya ana bilgisayar hello MongoDB sunucunun adıdır. |Evet |
| port |MongoDB sunucusuna hello TCP bağlantı noktası toolisten istemci bağlantıları için kullanır. |İsteğe bağlı, varsayılan değer: 27017 |
| authenticationType |Basic veya Anonymous. |Evet |
| kullanıcı adı |Kullanıcı hesabı tooaccess MongoDB. |Evet (Temel kimlik doğrulaması kullanılıyorsa). |
| password |Merhaba kullanıcının parolası. |Evet (Temel kimlik doğrulaması kullanılıyorsa). |
| authSource |Kimlik doğrulaması için kimlik bilgilerinizi toouse toocheck istediğiniz hello MongoDB veritabanı adı. |(Temel kimlik doğrulaması kullanılıyorsa) isteğe bağlı. Varsayılan: Merhaba yönetici hesabı ve databaseName özelliği kullanılarak belirtilen hello veritabanı kullanır. |
| databaseName |Tooaccess istediğiniz hello MongoDB veritabanı adı. |Evet |
| gatewayName |Merhaba veri deposu erişen hello ağ geçidi adı. |Evet |
| encryptedCredential |Ağ Geçidi tarafından şifrelenmiş kimlik bilgileri. |İsteğe bağlı |

#### <a name="example"></a>Örnek

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Daha fazla bilgi için bkz: [MongoDB bağlayıcı makale](data-factory-on-premises-mongodb-connector.md#linked-service-properties)

### <a name="dataset"></a>Veri kümesi
toodefine bir MongoDB veri kümesi hello **türü** hello kümesinin çok**MongoDbCollection**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü: 

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| collectionName |MongoDB veritabanı hello koleksiyonunda adı. |Evet |

#### <a name="example"></a>Örnek

```json
{
    "name": "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

Daha fazla bilgi için bkz: [MongoDB bağlayıcı makale](data-factory-on-premises-mongodb-connector.md#dataset-properties)

#### <a name="mongodb-source-in-copy-activity"></a>Kopyalama etkinliği MongoDB kaynağında
Veri adresinden kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**MongoDbSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** bölümü:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| sorgu |Merhaba özel sorgu tooread verileri kullanın. |SQL-92 sorgu dizesi. Örneğin: `select * from MyTable`. |Hayır (varsa **collectionName** , **dataset** belirtilir) |

#### <a name="example"></a>Örnek

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "MongoDbSource",
                    "query": "select * from MyTable"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MongoDbInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MongoDBToAzureBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Daha fazla bilgi için bkz: [MongoDB bağlayıcı makale](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)

## <a name="amazon-s3"></a>Amazon S3


### <a name="linked-service"></a>Bağlı hizmet
toodefine bir Amazon S3 bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**AwsAccessKey**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** bölümü :  

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| accessKeyID |Merhaba gizli erişim anahtarı kimliği. |Dize |Evet |
| secretAccessKey |Merhaba gizli erişim anahtarı kendisi. |Şifrelenmiş gizli dize |Evet |

#### <a name="example"></a>Örnek
```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

Daha fazla bilgi için bkz: [Amazon S3 bağlayıcı makale](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).

### <a name="dataset"></a>Veri kümesi
toodefine bir Amazon S3 dataset, kümesi hello **türü** hello kümesinin çok**AmazonS3**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü: 

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| bucketName |Merhaba S3 demetini adı. |Dize |Evet |
| anahtar |Merhaba S3 nesne anahtarı. |Dize |Hayır |
| önek |Merhaba S3 nesne anahtarı için önek. Seçilen nesneler, anahtarları Bu önek ile başlatın. Yalnızca anahtar boş olduğunda geçerlidir. |Dize |Hayır |
| Sürüm |S3 sürüm etkinleştirilirse S3 nesne Hello sürümü. |Dize |Hayır |
| Biçimi | şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set hello **türü** biçimi tooone şu değerlerden biri altında özellik. Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler. <br><br> Çok istiyorsanız**olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında hello Biçim bölümü atlayın. |Hayır | |
| Sıkıştırma | Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin. Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**. desteklenen hello düzeyleri şunlardır: **Optimal** ve **en hızlı**. Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support). |Hayır | |


> [!NOTE]
> bucketName + anahtarı burada demet hello S3 nesneleri için kök kapsayıcı ve anahtar hello tam yol tooS3 nesnesini hello S3 nesnesinin hello konumunu belirtir.

#### <a name="example-sample-dataset-with-prefix"></a>Örnek: Örnek veri kümesi önekiyle

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "<S3 bucket name>",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
#### <a name="example-sample-data-set-with-version"></a>Örnek: Örnek veri kümesiyle (sürüm)

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "<S3 bucket name>",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

#### <a name="example-dynamic-paths-for-s3"></a>Örnek: S3 dinamik yollar
Merhaba örnek hello Amazon S3 dataset içindeki anahtar ve bucketName özellikler için sabit değerleri kullanın.

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

Veri Fabrikası hello anahtar ve çalışma zamanında dinamik olarak bucketName SliceStart gibi sistem değişkenleri kullanarak hesaplar olabilir.

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

Yapabileceğiniz aynı hello önek özelliği bir Amazon S3 dataset için hello. Bkz: [Data Factory işlevler ve sistem değişkenleri](data-factory-functions-variables.md) desteklenen işlevleri ve değişkenler listesi.

Daha fazla bilgi için bkz: [Amazon S3 bağlayıcı makale](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).

### <a name="file-system-source-in-copy-activity"></a>Dosya sistem kaynağını kopyalama etkinliği
Verileri Amazon S3'ten kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**FileSystemSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** bölümü :


| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| Özyinelemeli |Toorecursively listesi S3 hello dizini altında nesneleri olup olmadığını belirtir. |true/false |Hayır |


#### <a name="example"></a>Örnek


```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource",
                    "recursive": true
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonS3InputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonS3ToBlob"
        }],
        "start": "2016-08-08T18:00:00",
        "end": "2016-08-08T19:00:00"
    }
}
```

Daha fazla bilgi için bkz: [Amazon S3 bağlayıcı makale](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).

## <a name="file-system"></a>Dosya Sistemi


### <a name="linked-service"></a>Bağlı hizmet
Bir şirket içi dosya sistemi tooan Azure data factory hello ile bağlayabilirsiniz **şirket içi dosya sunucusu** bağlı hizmeti. Aşağıdaki tablonun hello belirli toohello şirket içi dosya sunucusuna bağlı hizmeti olan JSON öğeleri için açıklamalar sağlanır.

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| type |Merhaba type özelliği çok ayarlandığından emin olun**OnPremisesFileServer**. |Evet |
| ana bilgisayar |Toocopy istediğiniz hello klasörü Hello kök yolunu belirtir. Merhaba kaçış karakteri kullanmak ' \ ' hello dize özel karakter. Bkz: [örnek bağlantılı hizmeti ve veri kümesi tanımları](#sample-linked-service-and-dataset-definitions) örnekleri için. |Evet |
| Kullanıcı Kimliği |Merhaba erişim toohello sunucusuna sahip hello kullanıcı Kimliğini belirtin. |Hayır (encryptedCredential seçerseniz) |
| password |Merhaba kullanıcı (UserID) Hello parolasını belirtin. |Hayır (encryptedCredential seçerseniz |
| encryptedCredential |Merhaba yeni AzureRmDataFactoryEncryptValue cmdlet'ini çalıştırarak alabilirsiniz hello şifreli kimlik bilgilerini belirtin. |Hayır (toospecify kullanıcı kimliği ve parola düz metin olarak seçerseniz) |
| gatewayName |Veri Fabrikası tooconnect toohello şirket içi dosya sunucusu kullanmalısınız hello ağ geçidi Hello adını belirtir. |Evet |

#### <a name="sample-folder-path-definitions"></a>Örnek klasör yolu tanımları 
| Senaryo | Bağlantılı hizmet tanımında ana bilgisayar | veri kümesi tanımında folderPath |
| --- | --- | --- |
| Veri Yönetimi ağ geçidi makine üzerinde yerel klasör: <br/><br/>Örnekler: D:\\ \* veya D:\folder\subfolder\\* |D:\\ \\ (için veri yönetimi ağ geçidi 2.0 ve sonraki sürümler) <br/><br/> localhost (daha önceki sürümler için veri yönetimi ağ geçidi 2. 0) |. \\ \\ veya klasör\\\\alt klasör (için veri yönetimi ağ geçidi 2.0 ve sonraki sürümler) <br/><br/>D:\\ \\ veya D:\\\\klasörü\\\\alt klasör (için ağ geçidi sürüm 2.0 altında) |
| Uzak paylaşılan klasör: <br/><br/>Örnekler: \\ \\myserver\\paylaşmak\\ \* veya \\ \\myserver\\paylaşmak\\klasörü\\alt klasör\\* |\\\\\\\\myserver\\\\paylaşma |. \\ \\ veya klasör\\\\alt klasör |


#### <a name="example-using-username-and-password-in-plain-text"></a>Örnek: kullanıcı adı ve parola düz metin olarak kullanma

```json
{
    "Name": "OnPremisesFileServerLinkedService",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "\\\\Contosogame-Asia",
            "userid": "Admin",
            "password": "123456",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-encryptedcredential"></a>Örnek: encryptedcredential kullanma

```json
{
    "Name": " OnPremisesFileServerLinkedService ",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "D:\\",
            "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Daha fazla bilgi için bkz: [dosya sistemi bağlayıcı makale](data-factory-onprem-file-system-connector.md#linked-service-properties).

### <a name="dataset"></a>Veri kümesi
toodefine bir dosya sistemi veri kümesi hello **türü** hello kümesinin çok**FileShare**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü: 

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| folderPath |Merhaba alt toohello klasörü belirtir. Merhaba kaçış karakteri kullanmak ' \' hello dize özel karakter. Bkz: [örnek bağlantılı hizmeti ve veri kümesi tanımları](#sample-linked-service-and-dataset-definitions) örnekleri için.<br/><br/>Bu özellik ile birleştirebilirsiniz **partitionBy** toohave klasör yolları dilimine göre başlangıç/bitiş tarih saatleri. |Evet |
| fileName |Hello Hello hello dosyasının adını belirtin **folderPath** hello tablo toorefer tooa belirli dosya hello klasöründeki istiyorsanız. Bu özellik için herhangi bir değer belirtmezseniz, hello tablo hello klasöründeki tooall dosyaları işaret eder.<br/><br/>Dosya adı bir çıkış veri kümesi için belirtilmediğinde hello oluşturulan hello dosya biçimini izleyen hello adıdır: <br/><br/>`Data.<Guid>.txt`(Örnek: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |Hayır |
| fileFilter |Tüm dosyalar yerine hello folderPath dosyaları kümesini filtre toobe tooselect kullanılan belirtin. <br/><br/>İzin verilen değerler: `*` (birden çok karakter) ve `?` (tek bir karakter).<br/><br/>Örnek 1: "fileFilter": "* .log"<br/>Örnek 2: "fileFilter": 2016 - 1-? txt"<br/><br/>Bu fileFilter bir giriş FileShare veri kümesi için geçerli olduğunu unutmayın. |Hayır |
| partitionedBy |Zaman serisi veri partitionedBy toospecify dinamik folderPath/fileName kullanabilirsiniz. İçin verileri saatte parametreli folderPath örneğidir. |Hayır |
| Biçimi | şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set hello **türü** biçimi tooone şu değerlerden biri altında özellik. Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler. <br><br> Çok istiyorsanız**olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında hello Biçim bölümü atlayın. |Hayır |
| Sıkıştırma | Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin. Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**; ve desteklenen düzeyler: **Optimal** ve **en hızlı**. bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support). |Hayır |

> [!NOTE]
> Dosya adı ve fileFilter aynı anda kullanamazsınız.

#### <a name="example"></a>Örnek

```json
{
    "name": "OnpremisesFileSystemInput",
    "properties": {
        "type": " FileShare",
        "linkedServiceName": " OnPremisesFileServerLinkedService ",
        "typeProperties": {
            "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
            "fileName": "{Hour}.csv",
            "partitionedBy": [{
                "name": "Year",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                        "format": "yyyy"
                }
            }, {
                "name": "Month",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "MM"
                }
            }, {
                "name": "Day",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "dd"
                }
            }, {
                "name": "Hour",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "HH"
                }
            }]
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Daha fazla bilgi için bkz: [dosya sistemi bağlayıcı makale](data-factory-onprem-file-system-connector.md#dataset-properties).

### <a name="file-system-source-in-copy-activity"></a>Dosya sistem kaynağını kopyalama etkinliği
Dosya sisteminden veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**FileSystemSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** Bölüm:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| Özyinelemeli |Merhaba klasörlerdeki veya yalnızca klasörden hello belirtilen Hello veri yinelemeli olarak okunur olup olmadığını gösterir. |TRUE, False (varsayılan) |Hayır |

#### <a name="example"></a>Örnek

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T19:00:00",
        "description": "Pipeline for copy activity",
        "activities": [{
            "name": "OnpremisesFileSystemtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "OnpremisesFileSystemInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
Daha fazla bilgi için bkz: [dosya sistemi bağlayıcı makale](data-factory-onprem-file-system-connector.md#copy-activity-properties).

### <a name="file-system-sink-in-copy-activity"></a>Dosya sistemi havuzu kopyalama etkinliği
Veri tooFile sistem kopyalıyorsanız hello ayarlamak **Havuz türü** Merhaba kopya etkinliği çok**FileSystemSink**ve hello özelliklerinde aşağıdaki belirtin **havuz** bölümü:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| copyBehavior |Merhaba kaynağı BlobSource veya dosya sistemi olduğunda hello kopyalama davranışını tanımlar. |**PreserveHierarchy:** hello dosya hiyerarşisi hello hedef klasörde korur. Diğer bir deyişle, hello kaynak dosya toohello kaynak klasörün hello göreli yol olduğundan hello hello hedef dosya toohello hedef klasörü hello göreli yolu ile aynı.<br/><br/>**FlattenHierarchy:** hello kaynak klasördeki tüm dosyaları hedef klasörün hello ilk düzeyi oluşturulur. Merhaba hedef dosyaları otomatik olarak oluşturulur adıyla oluşturulur.<br/><br/>**MergeFiles:** hello kaynak klasör tooone dosyasından tüm dosyaları birleştirir. Merhaba dosya adı/blob adı belirtilirse, hello belirtilen ad hello birleştirilmiş dosya adı değil. Aksi halde, bir otomatik olarak oluşturulan dosya adı değil. |Hayır |
otomatik-

#### <a name="example"></a>Örnek

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T20:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoOnPremisesFile",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "OnpremisesFileSystemOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "FileSystemSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 3,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Daha fazla bilgi için bkz: [dosya sistemi bağlayıcı makale](data-factory-onprem-file-system-connector.md#copy-activity-properties).

## <a name="ftp"></a>FTP

### <a name="linked-service"></a>Bağlı hizmet
toodefine FTP bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**Ftp_sunucusu**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** bölümü:  

| Özellik | Açıklama | Gerekli | Varsayılan |
| --- | --- | --- | --- |
| ana bilgisayar |Hello FTP sunucusu adı veya IP adresi |Evet |&nbsp; |
| authenticationType |Kimlik doğrulama türünü belirtin |Evet |Temel, anonim |
| kullanıcı adı |Erişim toohello FTP sunucusu olan kullanıcı |Hayır |&nbsp; |
| password |Parola hello kullanıcının (kullanıcı adı) |Hayır |&nbsp; |
| encryptedCredential |Şifrelenmiş kimlik bilgileri tooaccess hello FTP sunucusu |Hayır |&nbsp; |
| gatewayName |Merhaba veri yönetimi ağ geçidi ağ geçidi tooconnect tooan adını içi FTP sunucusu |Hayır |&nbsp; |
| port |Hangi hello FTP sunucusunun dinleme yaptığı bağlantı noktası |Hayır |21 |
| enableSsl |Toouse SSL/TLS kanalı üzerinden FTP olup olmadığını belirtin |Hayır |TRUE |
| enableServerCertificateValidation |Tooenable sunucu SSL FTP SSL/TLS kanalı üzerinden kullanırken doğrulama sertifikası olup olmadığını belirtin |Hayır |TRUE |

#### <a name="example-using-anonymous-authentication"></a>Örnek: Anonim kimlik doğrulamasını kullanma

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
            "typeProperties": {
            "authenticationType": "Anonymous",
            "host": "myftpserver.com"
        }
    }
}
```

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a>Örnek: kullanıcı adı ve parola düz metin olarak temel kimlik doğrulaması kullanma

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
    }
}
```

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a>Örnek: Bağlantı noktası, enableSsl, enableServerCertificateValidation kullanma

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a>Örnek: kimlik doğrulama ve ağ geçidi encryptedCredential kullanma

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
      }
}
```

Daha fazla bilgi için bkz: [FTP Bağlayıcısı](data-factory-ftp-connector.md#linked-service-properties) makalesi.

### <a name="dataset"></a>Veri kümesi
toodefine FTP veri kümesi, kümesi hello **türü** hello kümesinin çok**FileShare**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü: 

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| folderPath |Alt yolu toohello klasörü. Kaçış karakteri kullanmak ' \ ' hello dize özel karakter. Bkz: [örnek bağlantılı hizmeti ve veri kümesi tanımları](#sample-linked-service-and-dataset-definitions) örnekleri için.<br/><br/>Bu özellik ile birleştirebilirsiniz **partitionBy** toohave klasör yolları dilimine göre başlangıç/bitiş tarih saatleri. |Evet 
| fileName |Hello Hello hello dosyasının adını belirtin **folderPath** hello tablo toorefer tooa belirli dosya hello klasöründeki istiyorsanız. Bu özellik için herhangi bir değer belirtmezseniz, hello tablo hello klasöründeki tooall dosyaları işaret eder.<br/><br/>FileName bir çıkış veri kümesi için belirtilmediğinde oluşturulan hello dosyasının hello adı Bu biçim aşağıdaki hello olacaktır: <br/><br/>Veriler. <Guid>.txt (örnek: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Hayır |
| fileFilter |Tüm dosyalar yerine hello folderPath dosyaları kümesini filtre toobe tooselect kullanılan belirtin.<br/><br/>İzin verilen değerler: `*` (birden çok karakter) ve `?` (tek bir karakter).<br/><br/>Örnek 1:`"fileFilter": "*.log"`<br/>Örnek 2:`"fileFilter": 2016-1-?.txt"`<br/><br/> fileFilter bir giriş FileShare veri kümesi için geçerlidir. Bu özellik ile HDFS desteklenmiyor. |Hayır |
| partitionedBy |partitionedBy kullanılan toospecify dinamik folderPath zaman serisi veri için dosya adı olabilir. Örneğin, her veri saat için parametreli folderPath. |Hayır |
| Biçimi | şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set hello **türü** biçimi tooone şu değerlerden biri altında özellik. Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler. <br><br> Çok istiyorsanız**olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında hello Biçim bölümü atlayın. |Hayır |
| Sıkıştırma | Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin. Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**; ve desteklenen düzeyler: **Optimal** ve **en hızlı**. Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support). |Hayır |
| useBinaryTransfer |Belirtin olup ikili aktarım modunu kullanın. İkili mod ve false ASCII için true. Varsayılan değer: True. İlişkili bağlantılı hizmet türü türü olduğunda bu özellik yalnızca kullanılabilir: Ftp_sunucusu. |Hayır |

> [!NOTE]
> Dosya adı ve fileFilter aynı anda kullanılamaz.

#### <a name="example"></a>Örnek

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
            "fileName": "test.csv",
            "useBinaryTransfer": true
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Daha fazla bilgi için bkz: [FTP Bağlayıcısı](data-factory-ftp-connector.md#dataset-properties) makalesi.

### <a name="file-system-source-in-copy-activity"></a>Dosya sistem kaynağını kopyalama etkinliği
Bir FTP sunucusundan veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**FileSystemSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** Bölüm:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| Özyinelemeli |Merhaba alt klasörler veya yalnızca hello belirtilen klasör Hello veri yinelemeli olarak okunur olup olmadığını gösterir. |TRUE, False (varsayılan) |Hayır |

#### <a name="example"></a>Örnek

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00",
        "end": "2016-08-24T19:00:00"
    }
}
```

Daha fazla bilgi için bkz: [FTP Bağlayıcısı](data-factory-ftp-connector.md#copy-activity-properties) makalesi.


## <a name="hdfs"></a>HDFS

### <a name="linked-service"></a>Bağlı hizmet
toodefine bir HDFS bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**Hdfs**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** bölümü:  

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| type |Merhaba type özelliği ayarlanmalıdır: **Hdfs** |Evet |
| Url |URL toohello HDFS |Evet |
| authenticationType |Anonim veya Windows. <br><br> toouse **Kerberos kimlik doğrulaması** HDFS bağlayıcı için çok başvuran[Bu bölümde](#use-kerberos-authentication-for-hdfs-connector) tooset şirket içi ortamınızı uygun şekilde. |Evet |
| Kullanıcı adı |Kullanıcı adı için Windows kimlik doğrulaması. |Evet (Windows kimlik doğrulaması için) |
| password |Windows kimlik doğrulaması için parola. |Evet (Windows kimlik doğrulaması için) |
| gatewayName |Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello HDFS kullanmanız gerekir. |Evet |
| encryptedCredential |[AzureRMDataFactoryEncryptValue yeni](https://msdn.microsoft.com/library/mt603802.aspx) hello erişim kimlik bilgisi çıktısı. |Hayır |

#### <a name="example-using-anonymous-authentication"></a>Örnek: Anonim kimlik doğrulamasını kullanma

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-windows-authentication"></a>Örnek: Windows kimlik doğrulaması kullanma

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Daha fazla bilgi için bkz: [HDFS bağlayıcı](#data-factory-hdfs-connector.md#linked-service-properties) makalesi. 

### <a name="dataset"></a>Veri kümesi
toodefine bir HDFS veri kümesi hello **türü** hello kümesinin çok**FileShare**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü: 

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| folderPath |Yol toohello klasör. Örnek:`myfolder`<br/><br/>Kaçış karakteri kullanmak ' \ ' hello dize özel karakter. Örneğin: folder\subfolder için klasör belirtin\\\\alt ve d:\samplefolder için d: belirtin\\\\ÖrnekKlasör.<br/><br/>Bu özellik ile birleştirebilirsiniz **partitionBy** toohave klasör yolları dilimine göre başlangıç/bitiş tarih saatleri. |Evet |
| fileName |Hello Hello hello dosyasının adını belirtin **folderPath** hello tablo toorefer tooa belirli dosya hello klasöründeki istiyorsanız. Bu özellik için herhangi bir değer belirtmezseniz, hello tablo hello klasöründeki tooall dosyaları işaret eder.<br/><br/>FileName bir çıkış veri kümesi için belirtilmediğinde oluşturulan hello dosyasının hello adı Bu biçim aşağıdaki hello olacaktır: <br/><br/>Veriler. <Guid>.txt (örnek:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Hayır |
| partitionedBy |partitionedBy kullanılan toospecify dinamik folderPath zaman serisi veri için dosya adı olabilir. Örnek: veri her saat için parametreli folderPath. |Hayır |
| Biçimi | şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set hello **türü** biçimi tooone şu değerlerden biri altında özellik. Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler. <br><br> Çok istiyorsanız**olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında hello Biçim bölümü atlayın. |Hayır |
| Sıkıştırma | Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin. Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**. Desteklenen düzeyler: **Optimal** ve **en hızlı**. Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support). |Hayır |

> [!NOTE]
> Dosya adı ve fileFilter aynı anda kullanılamaz.

#### <a name="example"></a>Örnek

```json
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Daha fazla bilgi için bkz: [HDFS bağlayıcı](#data-factory-hdfs-connector.md#dataset-properties) makalesi. 

### <a name="file-system-source-in-copy-activity"></a>Dosya sistem kaynağını kopyalama etkinliği
HDFS veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**FileSystemSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** bölümü:

**FileSystemSource** aşağıdaki özelliklere hello destekler:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| Özyinelemeli |Merhaba alt klasörler veya yalnızca hello belirtilen klasör Hello veri yinelemeli olarak okunur olup olmadığını gösterir. |TRUE, False (varsayılan) |Hayır |

#### <a name="example"></a>Örnek

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "HdfsToBlobCopy",
            "inputs": [{
                "name": "InputDataset"
            }],
            "outputs": [{
                "name": "OutputDataset"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Daha fazla bilgi için bkz: [HDFS bağlayıcı](#data-factory-hdfs-connector.md#copy-activity-properties) makalesi.

## <a name="sftp"></a>SFTP


### <a name="linked-service"></a>Bağlı hizmet
toodefine bir SFTP bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**Sftp**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** bölümü:  

| Özellik | Açıklama | Gerekli |
| --- | --- | --- | --- |
| ana bilgisayar | Merhaba SFTP sunucu adı veya IP adresi. |Evet |
| port |Hangi hello SFTP sunucusunun dinleme yaptığı bağlantı noktası. Merhaba varsayılan değer: 21 |Hayır |
| authenticationType |Kimlik doğrulama türü belirtin. İzin verilen değerler: **temel**, **SshPublicKey**. <br><br> Çok başvuran[kullanarak temel kimlik doğrulaması](#using-basic-authentication) ve [kullanarak SSH ortak anahtar kimlik doğrulaması](#using-ssh-public-key-authentication) daha fazla özellikleri ve JSON örnekleri sırasıyla bölümler. |Evet |
| skipHostKeyValidation | Tooskip anahtar doğrulama konak olup olmadığını belirtin. | Hayır. Merhaba varsayılan değeri: false |
| hostKeyFingerprint | Merhaba parmak izi hello ana bilgisayar anahtarı belirtin. | Merhaba, Evet `skipHostKeyValidation` toofalse ayarlanır.  |
| gatewayName |Merhaba veri yönetimi ağ geçidi tooconnect tooan adını SFTP sunucu şirket içi. | Bir şirket içi SFTP sunucusundan veri kopyalama, Evet. |
| encryptedCredential | Şifrelenmiş kimlik bilgileri tooaccess hello SFTP sunucusu. Otomatik olarak oluşturulan, temel kimlik doğrulaması (kullanıcı adı + parola) veya SshPublicKey kimlik (kullanıcı adı + özel anahtar yolu veya içerik) Kopyalama Sihirbazı'nı veya hello ClickOnce açılan iletişim kutusunda belirttiğiniz zaman. | Hayır. Yalnızca bir şirket içi SFTP sunucusundan veri kopyalama işlemi sırasında uygulanır. |

#### <a name="example-using-basic-authentication"></a>Örnek: temel kimlik doğrulaması kullanma

toouse temel kimlik doğrulamasını ayarlamak `authenticationType` olarak `Basic`ve bunun yanında, SFTP bağlayıcı hello son bölümde sunulan genel olanları hello aşağıdaki özelliklere hello belirtin:

| Özellik | Açıklama | Gerekli |
| --- | --- | --- | --- |
| kullanıcı adı | Erişim toohello SFTP sunucusu olan kullanıcı. |Evet |
| password | Merhaba kullanıcının (kullanıcı adı) parolası. | Evet |

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<SFTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a>Örnek: Temel kimlik doğrulaması ile şifrelenmiş kimlik bilgileri **

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="using-ssh-public-key-authentication"></a>SSH ortak anahtar kimlik doğrulaması kullanarak: **

toouse temel kimlik doğrulamasını ayarlamak `authenticationType` olarak `SshPublicKey`ve bunun yanında, SFTP bağlayıcı hello son bölümde sunulan genel olanları hello aşağıdaki özelliklere hello belirtin:

| Özellik | Açıklama | Gerekli |
| --- | --- | --- | --- |
| kullanıcı adı |Erişim toohello SFTP sunucusu olan kullanıcı |Evet |
| privateKeyPath | Mutlak yol toohello belirtin özel anahtar dosyası bu ağ geçidi erişebilir. | Her iki hello belirtin `privateKeyPath` veya `privateKeyContent`. <br><br> Yalnızca bir şirket içi SFTP sunucusundan veri kopyalama işlemi sırasında uygulanır. |
| privateKeyContent | Merhaba özel anahtar içeriğinin seri hale getirilmiş bir dize. Merhaba Kopyalama Sihirbazı'nı hello özel anahtar dosyası okuma ve hello özel anahtar içeriği otomatik olarak ayıklar. Tüm diğer aracı/SDK kullanıyorsanız, bunun yerine hello privateKeyPath özelliğini kullanın. | Her iki hello belirtin `privateKeyPath` veya `privateKeyContent`. |
| Parola | Merhaba anahtar dosyası bir parola deyimi tarafından korunuyorsa hello geçişi tümcecik/parola toodecrypt hello özel anahtarı belirtin. | Merhaba özel anahtar dosyası bir parola deyimi tarafından korunuyorsa, Evet. |

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a>Örnek: kullanarak özel anahtar içerik ** SshPublicKey kimlik doğrulaması

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

Daha fazla bilgi için bkz: [SFTP bağlayıcı](data-factory-sftp-connector.md#linked-service-properties) makalesi. 

### <a name="dataset"></a>Veri kümesi
toodefine SFTP dataset kümesi hello **türü** hello kümesinin çok**FileShare**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü: 

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| folderPath |Alt yolu toohello klasörü. Kaçış karakteri kullanmak ' \ ' hello dize özel karakter. Bkz: [örnek bağlantılı hizmeti ve veri kümesi tanımları](#sample-linked-service-and-dataset-definitions) örnekleri için.<br/><br/>Bu özellik ile birleştirebilirsiniz **partitionBy** toohave klasör yolları dilimine göre başlangıç/bitiş tarih saatleri. |Evet |
| fileName |Hello Hello hello dosyasının adını belirtin **folderPath** hello tablo toorefer tooa belirli dosya hello klasöründeki istiyorsanız. Bu özellik için herhangi bir değer belirtmezseniz, hello tablo hello klasöründeki tooall dosyaları işaret eder.<br/><br/>FileName bir çıkış veri kümesi için belirtilmediğinde oluşturulan hello dosyasının hello adı Bu biçim aşağıdaki hello olacaktır: <br/><br/>Veriler. <Guid>.txt (örnek: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Hayır |
| fileFilter |Tüm dosyalar yerine hello folderPath dosyaları kümesini filtre toobe tooselect kullanılan belirtin.<br/><br/>İzin verilen değerler: `*` (birden çok karakter) ve `?` (tek bir karakter).<br/><br/>Örnek 1:`"fileFilter": "*.log"`<br/>Örnek 2:`"fileFilter": 2016-1-?.txt"`<br/><br/> fileFilter bir giriş FileShare veri kümesi için geçerlidir. Bu özellik ile HDFS desteklenmiyor. |Hayır |
| partitionedBy |partitionedBy kullanılan toospecify dinamik folderPath zaman serisi veri için dosya adı olabilir. Örneğin, her veri saat için parametreli folderPath. |Hayır |
| Biçimi | şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set hello **türü** biçimi tooone şu değerlerden biri altında özellik. Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler. <br><br> Çok istiyorsanız**olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında hello Biçim bölümü atlayın. |Hayır |
| Sıkıştırma | Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin. Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**. Desteklenen düzeyler: **Optimal** ve **en hızlı**. Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support). |Hayır |
| useBinaryTransfer |Belirtin olup ikili aktarım modunu kullanın. İkili mod ve false ASCII için true. Varsayılan değer: True. İlişkili bağlantılı hizmet türü türü olduğunda bu özellik yalnızca kullanılabilir: Ftp_sunucusu. |Hayır |

> [!NOTE]
> Dosya adı ve fileFilter aynı anda kullanılamaz.

#### <a name="example"></a>Örnek

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
            "fileName": "test.csv"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Daha fazla bilgi için bkz: [SFTP bağlayıcı](data-factory-sftp-connector.md#dataset-properties) makalesi. 

### <a name="file-system-source-in-copy-activity"></a>Dosya sistem kaynağını kopyalama etkinliği
SFTP kaynaktan veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**FileSystemSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** Bölüm:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| Özyinelemeli |Merhaba alt klasörler veya yalnızca hello belirtilen klasör Hello veri yinelemeli olarak okunur olup olmadığını gösterir. |TRUE, False (varsayılan) |Hayır |



#### <a name="example"></a>Örnek

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2017-02-20T18:00:00",
        "end": "2017-02-20T19:00:00"
    }
}
```

Daha fazla bilgi için bkz: [SFTP bağlayıcı](data-factory-sftp-connector.md#copy-activity-properties) makalesi.


## <a name="http"></a>HTTP

### <a name="linked-service"></a>Bağlı hizmet
bir HTTP toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**Http**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** bölümü:  

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| URL | Temel URL toohello Web sunucusu | Evet |
| authenticationType | Merhaba kimlik doğrulama türünü belirtir. İzin verilen değerler: **anonim**, **temel**, **Özet**, **Windows**, **ClientCertificate**. <br><br> Daha fazla özellikleri ve JSON örnekleri bu tablonun altındaki toosections bu kimlik doğrulama türleri için sırasıyla bakın. | Evet |
| enableServerCertificateValidation | Kaynak HTTPS Web sunucusu ise tooenable sunucu SSL sertifikası doğrulaması olup olmadığını belirtin | Hayır, varsayılan değer true şeklindedir |
| gatewayName | Merhaba veri yönetimi ağ geçidi tooconnect tooan adını HTTP kaynağı şirket içi. | Bir şirket içi HTTP kaynaktan veri kopyalama, Evet. |
| encryptedCredential | Şifrelenmiş kimlik bilgileri tooaccess hello HTTP uç noktası. Otomatik olarak oluşturulan Kopyalama Sihirbazı'nı veya hello ClickOnce açılan iletişim kutusunda hello kimlik doğrulama bilgilerini yapılandırın. | Hayır. Yalnızca bir şirket içi HTTP sunucusundan veri kopyalama işlemi sırasında uygulanır. |

#### <a name="example-using-basic-digest-or-windows-authentication"></a>Örnek: Temel, Özet veya Windows kimlik doğrulaması kullanma
Ayarlama `authenticationType` olarak `Basic`, `Digest`, veya `Windows`ve bunun yanında, HTTP Bağlayıcısı genel olanları sunulan yukarıda hello aşağıdaki özelliklere hello belirtin:

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| kullanıcı adı | Kullanıcı adı tooaccess hello HTTP uç noktası. | Evet |
| password | Merhaba kullanıcının (kullanıcı adı) parolası. | Evet |

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "basic",
            "url": "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

#### <a name="example-using-clientcertificate-authentication"></a>Örnek: ClientCertificate kimlik doğrulaması kullanma

toouse temel kimlik doğrulamasını ayarlamak `authenticationType` olarak `ClientCertificate`ve bunun yanında, HTTP Bağlayıcısı genel olanları sunulan yukarıda hello aşağıdaki özelliklere hello belirtin:

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| embeddedCertData | Merhaba Base64 ile kodlanmış içeriğini ikili veri hello kişisel bilgi değişimi (PFX) dosyası. | Her iki hello belirtin `embeddedCertData` veya `certThumbprint`. |
| Certthumbprınt | ağ geçidi makinenizin sertifika deposunda yüklü hello sertifikanın parmak izini hello. Yalnızca bir şirket içi HTTP kaynaktan veri kopyalama işlemi sırasında uygulanır. | Her iki hello belirtin `embeddedCertData` veya `certThumbprint`. |
| password | Merhaba sertifikayla ilişkili parola. | Hayır |

Kullanırsanız `certThumbprint` kimlik doğrulaması ve hello sertifika hello kişisel hello yerel bilgisayar deposunda yüklü için toogrant hello okuma izni toohello ağ geçidi hizmeti gerekir:

1. Microsoft Yönetim Konsolu (MMC) başlatın. Merhaba eklemek **sertifikaları** bu hedefleri hello eklentisi **yerel bilgisayar**.
2. Genişletme **sertifikaları**, **kişisel**, tıklatıp **Sertifikalar**.
3. Merhaba kişisel deposundan Hello sertifikayı sağ tıklatın ve seçin **tüm görevler**->**özel anahtarları Yönet...**
3. Merhaba üzerinde **güvenlik** sekmesinde, altında veri yönetimi ağ geçidi ana bilgisayar hizmeti çalıştığı hello okuma erişimi toohello sertifikasıyla hello kullanıcı hesabını ekleyin.  

**Örnek: istemci sertifikası kullanarak:** bu hizmeti, veri fabrikası tooan şirket içi HTTP web sunucunuzun bağlı. Veri Yönetimi yüklü ağ geçidi ile Merhaba makinede yüklü bir istemci sertifikası kullanır.

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"
        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a>Örnek: istemci sertifikası bir dosyada kullanma
Bu hizmet bağlantılar, veri fabrikası tooan şirket içi HTTP web sunucunuzun bağlı. Veri Yönetimi yüklü ağ geçidi ile bir istemci sertifika dosyası hello makinede kullanır.

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

Daha fazla bilgi için bkz: [HTTP Bağlayıcısı](data-factory-http-connector.md#linked-service-properties) makalesi.

### <a name="dataset"></a>Veri kümesi
bir HTTP toodefine veri kümesi, kümesi hello **türü** hello kümesinin çok**Http**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü: 

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| relativeUrl | Merhaba verileri içeren bir göreli URL toohello kaynağıdır. Yol belirtilmediğinde hello bağlantılı hizmet tanımında belirtilen yalnızca hello URL'si kullanılır. <br><br> kullanabileceğiniz tooconstruct dinamik URL [Data Factory işlevler ve sistem değişkenleri](data-factory-functions-variables.md), örneğin: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`. | Hayır |
| requestMethod | HTTP yöntemi. İzin verilen değerler **almak** veya **POST**. | Hayır. Varsayılan değer `GET`. |
| additionalHeaders | Ek HTTP isteği üstbilgileri. | Hayır |
| RequestBody | HTTP istek gövdesi. | Hayır |
| Biçimi | Toosimply istiyorsanız **HTTP uç noktası olarak hello veri almak-olduğu** ayrıştırma olmadan, bu biçim ayarlarını atla. <br><br> Kopyalama sırasında tooparse hello HTTP yanıt içerik isterseniz şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**. Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler. |Hayır |
| Sıkıştırma | Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin. Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**. Desteklenen düzeyler: **Optimal** ve **en hızlı**. Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support). |Hayır |

#### <a name="example-using-hello-get-default-method"></a>Örnek: hello (varsayılan) GET yöntemini kullanma

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

#### <a name="example-using-hello-post-method"></a>Örnek: Merhaba POST yöntemini kullanma

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
            "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
Daha fazla bilgi için bkz: [HTTP Bağlayıcısı](data-factory-http-connector.md#dataset-properties) makalesi.

### <a name="http-source-in-copy-activity"></a>Kopyalama etkinliğinde HTTP kaynağı
Bir HTTP kaynaktan veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**HttpSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** bölümü:

| Özellik | Açıklama | Gerekli |
| -------- | ----------- | -------- |
| httpRequestTimeout | Merhaba HTTP isteği tooget yanıt için zaman aşımı (TimeSpan) hello. Merhaba zaman aşımı tooget bir yanıt hello zaman aşımı tooread yanıt verileri değil olur. | Hayır. Varsayılan değer: 00:01:40 |


#### <a name="example"></a>Örnek

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "HttpSourceDataInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "HttpSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Daha fazla bilgi için bkz: [HTTP Bağlayıcısı](data-factory-http-connector.md#copy-activity-properties) makalesi.

## <a name="odata"></a>OData

### <a name="linked-service"></a>Bağlı hizmet
bir OData toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**OData**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** bölümü:  

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| URL |Merhaba OData hizmeti URL'si. |Evet |
| authenticationType |Kimlik doğrulama türü tooconnect toohello OData kaynağı kullanılır. <br/><br/> OData bulut için olası değerler şunlardır anonim, temel ve OAuth (Not OAuth Azure Active Directory tabanlı şu anda yalnızca Azure Data Factory destek). <br/><br/> Anonim, temel ve Windows, şirket içi OData için olası değerler şunlardır. |Evet |
| kullanıcı adı |Temel kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin. |Evet (yalnızca temel kimlik doğrulaması kullanıyorsanız) |
| password |Merhaba username için belirtilen hello kullanıcı hesabı için parola belirtin. |Evet (yalnızca temel kimlik doğrulaması kullanıyorsanız) |
| authorizedCredential |OAuth kullanıyorsanız **Authorize** hello Data Factory Kopyalama Sihirbazı veya Düzenleyicisi'nde düğmesine tıklayın ve sonra bu özellik başlangıç değeri otomatik olarak oluşturulan kimlik bilgilerinizi girin. |Evet (yalnızca OAuth kimlik doğrulaması kullanıyorsanız) |
| gatewayName |Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi OData hizmeti kullanmanız gerekir. Yalnızca şirket içi OData kaynak sunucudan kopyaladığınız verileri belirtin. |Hayır |

#### <a name="example---using-basic-authentication"></a>Temel kimlik doğrulaması kullanan örnek-
```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

#### <a name="example---using-anonymous-authentication"></a>Anonim kimlik doğrulaması kullanan örnek-

```json
{
    "name": "ODataLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a>Örnek - kullanan Windows kimlik doğrulaması erişme OData kaynağı şirket içi

```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "<endpoint of on-premises OData source, for example, Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a>Örnek - bulut OData kaynağı erişme OAuth kimlik doğrulaması kullanma
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source, for example, https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

Daha fazla bilgi için bkz: [OData bağlayıcı](data-factory-odata-connector.md#linked-service-properties) makalesi.

### <a name="dataset"></a>Veri kümesi
toodefine bir OData veri kümesini kümesi hello **türü** hello kümesinin çok**ODataResource**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü: 

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| Yol |Yol toohello OData kaynak |Hayır |

#### <a name="example"></a>Örnek

```json
{
    "name": "ODataDataset",
    "properties": {
        "type": "ODataResource",
        "typeProperties": {
            "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
        }
    }
}
```

Daha fazla bilgi için bkz: [OData bağlayıcı](data-factory-odata-connector.md#dataset-properties) makalesi.

### <a name="relational-source-in-copy-activity"></a>Kopyalama etkinliği ilişkisel kaynağında
Bir OData kaynaktan veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**RelationalSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** Bölüm:

| Özellik | Açıklama | Örnek | Gerekli |
| --- | --- | --- | --- |
| sorgu |Merhaba özel sorgu tooread verileri kullanın. |"? $select adı, açıklama ve $top = 5 =" |Hayır |

#### <a name="example"></a>Örnek

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "?$select=Name, Description&$top=5"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "ODataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobODataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "ODataToBlob"
        }],
        "start": "2017-02-01T18:00:00",
        "end": "2017-02-03T19:00:00"
    }
}
```

Daha fazla bilgi için bkz: [OData bağlayıcı](data-factory-odata-connector.md#copy-activity-properties) makalesi.


## <a name="odbc"></a>ODBC


### <a name="linked-service"></a>Bağlı hizmet
toodefine bir ODBC bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**OnPremisesOdbc**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** bölümü:  

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| connectionString |Merhaba olmayan erişim kimlik bilgisi kısmı hello bağlantı dizesini ve isteğe bağlı bir kimlik bilgisi şifrelenir. Aşağıdaki bölümlerde hello örneklere bakın. |Evet |
| kimlik bilgisi |Merhaba erişim kimlik bilgisi bölümü sürücüye özgü özellik değer biçiminde belirtilen hello bağlantı dizesi. Örnek: "Uid =<user ID>; PWD =<password>; RefreshToken =<secret refresh token>; ". |Hayır |
| authenticationType |Kimlik doğrulama türü tooconnect toohello ODBC veri deposu kullanılır. Olası değerler şunlardır: anonim ve temel. |Evet |
| kullanıcı adı |Temel kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin. |Hayır |
| password |Merhaba username için belirtilen hello kullanıcı hesabı için parola belirtin. |Hayır |
| gatewayName |Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello ODBC veri deposu kullanmanız gerekir. |Evet |

#### <a name="example---using-basic-authentication"></a>Temel kimlik doğrulaması kullanan örnek-

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a>Temel kimlik doğrulaması ile şifrelenmiş kimlik bilgileri kullanılarak örnek-
Merhaba kimlik hello kullanarak şifreleyebilirsiniz [yeni AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (Azure PowerShell 1.0 sürümü) cmdlet'ini veya [yeni AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 veya önceki bir sürümü hello Azure PowerShell).  

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-anonymous-authentication"></a>Örnek: Anonim kimlik doğrulamasını kullanma

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Daha fazla bilgi için bkz: [ODBC bağlayıcı](data-factory-odbc-connector.md#linked-service-properties) makalesi. 

### <a name="dataset"></a>Veri kümesi
toodefine bir ODBC veri kümesini kümesi hello **türü** hello kümesinin çok**RelationalTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü: 

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| tableName |Merhaba ODBC veri deposundaki Merhaba tablonun adı. |Evet |


#### <a name="example"></a>Örnek

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "ODBCLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Daha fazla bilgi için bkz: [ODBC bağlayıcı](data-factory-odbc-connector.md#dataset-properties) makalesi. 

### <a name="relational-source-in-copy-activity"></a>Kopyalama etkinliği ilişkisel kaynağında
Bir ODBC veri deposundan veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**RelationalSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** Bölüm:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| sorgu |Merhaba özel sorgu tooread verileri kullanın. |SQL sorgu dizesi. Örneğin: `select * from MyTable`. |Evet |

#### <a name="example"></a>Örnek

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "OdbcDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobOdbcDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "OdbcToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
``` 

Daha fazla bilgi için bkz: [ODBC bağlayıcı](data-factory-odbc-connector.md#copy-activity-properties) makalesi.

## <a name="salesforce"></a>Salesforce


### <a name="linked-service"></a>Bağlı hizmet
bir Salesforce toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**Salesforce**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** bölümü:  

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| environmentUrl | Merhaba, URL Salesforce örneği belirtin. <br><br> -Varsayılan değer "https://login.salesforce.com" dir. <br> -Korumalı alan, toocopy verileri "https://test.salesforce.com" belirtin. <br> -toocopy verileri özel bir etki alanından belirtin, örneğin, "https://[domain].my.salesforce.com". |Hayır |
| kullanıcı adı |Merhaba kullanıcı hesabı için bir kullanıcı adı belirtin. |Evet |
| password |Merhaba kullanıcı hesabı için bir parola belirtin. |Evet |
| securityToken |Merhaba kullanıcı hesabı için bir güvenlik belirteci belirtin. Bkz: [güvenlik belirteci alma getirin](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) yönelik yönergeler tooreset/get bir güvenlik belirteci. Genel olarak, toolearn güvenlik belirteçleri hakkında bkz [güvenlik ve hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm). |Evet |

#### <a name="example"></a>Örnek

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```

Daha fazla bilgi için bkz: [Salesforce bağlayıcı](data-factory-salesforce-connector.md#linked-service-properties) makalesi. 

### <a name="dataset"></a>Veri kümesi
toodefine bir Salesforce veri kümesi hello **türü** hello kümesinin çok**RelationalTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü: 

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| tableName |Salesforce Merhaba tablonun adı. |Hayır (varsa bir **sorgu** , **RelationalSource** belirtilir) |

#### <a name="example"></a>Örnek

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Daha fazla bilgi için bkz: [Salesforce bağlayıcı](data-factory-salesforce-connector.md#dataset-properties) makalesi. 

### <a name="relational-source-in-copy-activity"></a>Kopyalama etkinliği ilişkisel kaynağında
Salesforce veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**RelationalSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** Bölüm:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| sorgu |Merhaba özel sorgu tooread verileri kullanın. |Bir SQL-92 sorgu veya [Salesforce nesnesi sorgu dili (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) sorgu. Örneğin:  `select * from MyTable__c`. |Hayır (Merhaba, **tableName** Merhaba, **dataset** belirtilir) |

#### <a name="example"></a>Örnek  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "SalesforceInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

> [!IMPORTANT]
> Merhaba "__c" Merhaba API adı parçası herhangi bir özel nesnesi için gereklidir.

Daha fazla bilgi için bkz: [Salesforce bağlayıcı](data-factory-salesforce-connector.md#copy-activity-properties) makalesi. 

## <a name="web-data"></a>Web verileri 

### <a name="linked-service"></a>Bağlı hizmet
toodefine Web bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**Web**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** bölümü:  

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| Url |URL toohello Web kaynağı |Evet |
| authenticationType |Anonim. |Evet |
 

#### <a name="example"></a>Örnek


```json
{
    "name": "web",
    "properties": {
        "type": "Web",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "url": "https://en.wikipedia.org/wiki/"
        }
    }
}
```

Daha fazla bilgi için bkz: [Web tablo bağlayıcı](data-factory-web-table-connector.md#linked-service-properties) makalesi. 

### <a name="dataset"></a>Veri kümesi
toodefine bir Web veri kümesi hello **türü** hello kümesinin çok**WebTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü: 

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| type |Merhaba veri kümesi türü. çok ayarlanmalıdır**WebTable** |Evet |
| Yol |Merhaba tablo içeren bir göreli URL toohello kaynağıdır. |Hayır. Yol belirtilmediğinde hello bağlantılı hizmet tanımında belirtilen yalnızca hello URL'si kullanılır. |
| Dizin |hello kaynak hello tabloda başlangıç dizini. Bkz: [bir HTML sayfasında tablosunun Get dizini](#get-index-of-a-table-in-an-html-page) HTML sayfası bir tablodaki adımları toogetting dizini için bölüm. |Evet |

#### <a name="example"></a>Örnek

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Daha fazla bilgi için bkz: [Web tablo bağlayıcı](data-factory-web-table-connector.md#dataset-properties) makalesi. 

### <a name="web-source-in-copy-activity"></a>Kopyalama etkinliğinde Web kaynağı
Bir web tablodan veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**WebSource**. Şu anda kopyalama etkinliği hello kaynağında olduğunda türü **WebSource**, hiçbir ek özellikler desteklenir.

#### <a name="example"></a>Örnek

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "WebTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "WebSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Daha fazla bilgi için bkz: [Web tablo bağlayıcı](data-factory-web-table-connector.md#copy-activity-properties) makalesi. 

## <a name="compute-environments"></a>ORTAMLAR İŞLEM
Merhaba aşağıdaki tabloda, bunlar üzerinde çalışan Data Factory ve hello dönüştürme etkinlikleri tarafından desteklenen hello işlem ortamları listeler. Merhaba işlem olduğunuz Hello bağlantısına tıklayın toosee hello JSON şemalarında bağlantılı hizmet toolink için tooa veri fabrikası ilgileniyor. 

| İşlem ortamı | Etkinlikler |
| --- | --- |
| [İsteğe bağlı Hdınsight kümesi](#on-demand-azure-hdinsight-cluster) veya [kendi Hdınsight kümenizi](#existing-azure-hdinsight-cluster) |[.NET özel etkinlik](#net-custom-activity), [Hive etkinliğini](#hdinsight-hive-activity), [Pig etkinlik] (#hdinsight-pig-etkinliği [MapReduce etkinliği](#hdinsight-mapreduce-activity), [Hadoop etkinlik akış](#hdinsight-streaming-activityd), [Spark etkinliği](#hdinsight-spark-activity) |
| [Azure toplu işlem](#azure-batch) |[.NET özel etkinliği](#net-custom-activity) |
| [Azure Machine Learning](#azure-machine-learning) | [Toplu iş yürütme etkinliği makine](#machine-learning-batch-execution-activity), [kaynak güncelleştirme etkinliği makine](#machine-learning-update-resource-activity) |
| [Azure Data Lake Analytics](#azure-data-lake-analytics) |[Data Lake Analytics U-SQL](#data-lake-analytics-u-sql-activity) |
| [Azure SQL veritabanı](#azure-sql-database-1), [Azure SQL veri ambarı](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1) |[Saklı Yordam](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a>İsteğe bağlı Azure Hdınsight kümesi
Hello Azure Data Factory hizmetine otomatik olarak bir Windows/Linux tabanlı isteğe bağlı Hdınsight küme tooprocess veriler oluşturabilir. Merhaba küme hello depolama hesabı (Merhaba JSON özelliğinde linkedServiceName) ile aynı bölgeye hello kümesi ile ilişkili hello oluşturulur. Bu bağlı hizmete dönüştürme etkinlikleri izleyerek hello çalıştırabilirsiniz: [.NET özel etkinlik](#net-custom-activity), [Hive etkinliğini](#hdinsight-hive-activity), [Pig etkinlik] (#hdinsight-pig-etkinliği [MapReduce etkinliği ](#hdinsight-mapreduce-activity), [Hadoop etkinlik akış](#hdinsight-streaming-activityd), [Spark etkinlik](#hdinsight-spark-activity). 

### <a name="linked-service"></a>Bağlı hizmet 
Aşağıdaki tablonun hello hello Azure JSON tanımında bir isteğe bağlı Hdınsight bağlı hizmeti kullanılan hello özellikleri için açıklamalar sağlanır.

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| type |Merhaba type özelliği çok ayarlanmalıdır**HDInsightOnDemand**. |Evet |
| ClusterSize |Merhaba kümede çalışan/veri düğüm sayısı. Merhaba Hdınsight kümesi hello için bu özelliği belirtmeniz çalışan düğüm sayısı ile birlikte 2 baş düğümler ile oluşturulur. Merhaba düğümleri olan 24 çekirdek 4 çalışan düğümlü bir küme alır, böylece 4 çekirdeğe sahip Standard_D3 boyutunu (4\*4 = 16 çekirdek çalışan düğümleri artı 2\*4 = 8 çekirdek baş düğümler için). Bkz: [Hdınsight oluşturma Linux tabanlı Hadoop kümeleri](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) hello Standard_D3 katmanı hakkında ayrıntılı bilgi için. |Evet |
| TimeToLive |Merhaba boşta kalma süresi hello isteğe bağlı Hdınsight kümesi için izin verilen. Ne kadar süreyle hello isteğe bağlı Hdınsight kümesi hello kümedeki diğer etkin iş yok varsa bir etkinlik tamamlandıktan sonra canlı kalır belirtir.<br/><br/>Bir etkinlik 6 dakika ve timetolive sürerse Örneğin, too5 dakika, 5 dakika sonra hello için Canlı hello küme kalır hello etkinlik işleme 6 dakika ayarlandı. Başka bir etkinlik hello 6 dakika penceresiyle yürütülürse, hello tarafından işlenir aynı küme.<br/><br/>İsteğe bağlı Hdınsight kümesi oluşturma (biraz sürebilir), pahalı bir işlem olduğundan bu ayar isteğe bağlı Hdınsight kümesi yeniden kullanarak bir veri fabrikası gerekli tooimprove performansını kullanın.<br/><br/>Timetolive değeri too0 ayarlarsanız, hello etkinliği çalıştırmak hemen işlenen hello küme silinir. Yüksek bir değer ayarlarsanız hello diğer yandan hello küme gereksiz yere yüksek maliyetlerini kaynaklanan boşta kalır. Bu nedenle, gereksinimlerinize göre hello uygun değere ayarlamak önemlidir.<br/><br/>Birden çok ardışık düzen paylaşabilirsiniz hello timetolive özellik değerini uygun şekilde ayarlanmışsa, hello hello isteğe bağlı Hdınsight kümesinin aynı örneği |Evet |
| Sürüm |Merhaba Hdınsight küme sürümü. Ayrıntılar için bkz [desteklenen Azure Data Factory'de Hdınsight sürümleri](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory). |Hayır |
| linkedServiceName |Azure depolama bağlı hizmeti toobe depolamak ve veri işleme için Hello isteğe bağlı küme tarafından kullanılan. <p>Şu anda bir Azure Data Lake Store hello depolama alanı olarak kullanan bir isteğe bağlı Hdınsight kümesi oluşturulamıyor. Bir Azure Data Lake Store'da işleme Hdınsight toostore hello sonuç verileri istiyorsanız hello Azure Blob Storage toohello Azure Data Lake Store kopyalama etkinliği toocopy hello verilerden kullanın.</p>  | Evet |
| additionalLinkedServiceNames |Böylece Hello Data Factory hizmetinin bunları sizin adınıza kaydedebilirsiniz hello Hdınsight için ek depolama hesapları hizmeti bağlı belirtir. |Hayır |
| osType |İşletim sistemi türü. İzin verilen değerler: (varsayılan) Windows ve Linux |Hayır |
| hcatalogLinkedServiceName |Azure SQL bağlı Hello adını noktası toohello HCatalog veritabanı hizmeti. Merhaba isteğe bağlı Hdınsight kümesi hello meta depo hello Azure SQL veritabanı kullanılarak oluşturulur. |Hayır |

### <a name="json-example"></a>JSON örneği
JSON aşağıdaki hello Linux tabanlı isteğe bağlı Hdınsight bağlı hizmeti tanımlar. Merhaba Data Factory hizmetinin otomatik olarak oluşturur bir **Linux tabanlı** veri dilimi işlerken Hdınsight kümesi. 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

Daha fazla bilgi için bkz: [işlem bağlı Hizmetleri](data-factory-compute-linked-services.md) makalesi. 

## <a name="existing-azure-hdinsight-cluster"></a>Var olan Azure Hdınsight kümesi
Data Factory ile kendi Hdınsight kümenizi Azure Hdınsight bağlı hizmeti tooregister oluşturabilirsiniz. Bu bağlı hizmete veri dönüştürme etkinlikleri izleyerek hello çalıştırabilirsiniz: [.NET özel etkinlik](#net-custom-activity), [Hive etkinliğini](#hdinsight-hive-activity), [Pig etkinlik] (#hdinsight-pig-etkinliği [MapReduce Etkinlik](#hdinsight-mapreduce-activity), [Hadoop etkinlik akış](#hdinsight-streaming-activityd), [Spark etkinlik](#hdinsight-spark-activity). 

### <a name="linked-service"></a>Bağlı hizmet
Aşağıdaki tablonun hello hello Azure JSON tanımında Azure Hdınsight bağlı hizmeti kullanılan hello özellikleri için açıklamalar sağlanır.

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| type |Merhaba type özelliği çok ayarlanmalıdır**Hdınsight**. |Evet |
| clusterUri |Merhaba hello Hdınsight kümesinin URI. |Evet |
| kullanıcı adı |Tooconnect tooan olan bir Hdınsight kümesine kullanılan hello kullanıcı toobe Hello adı belirtin. |Evet |
| password |Merhaba kullanıcı hesabı için parola belirtin. |Evet |
| linkedServiceName | Hdınsight kümesi hello tarafından kullanılan hello toohello Azure blob depolama başvuruyor Azure Storage bağlı hizmeti adı. <p>Şu anda bu özellik için bir Azure Data Lake Store bağlı belirtemezsiniz. Merhaba Hdınsight kümesine erişim toohello Data Lake Store varsa Hive/Pig komut dosyalarından hello Azure Data Lake Store verilerde erişebilir. </p>  |Evet |

Hdınsight kümeleri desteklenen sürümleri için bkz: [desteklenen Hdınsight sürümleri](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory). 

#### <a name="json-example"></a>JSON örneği

```json
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
            "userName": "admin",
            "password": "<password>",
            "linkedServiceName": "MyHDInsightStoragelinkedService"
        }
    }
}
```

## <a name="azure-batch"></a>Azure Batch
Bir Azure Batch bağlantılı hizmet tooregister data factory ile sanal makineleri (VM'ler) Batch havuzu oluşturabilirsiniz. .NET özel etkinlikler Azure Batch ya da Azure Hdınsight kullanarak çalıştırabilirsiniz. Çalıştırabilirsiniz bir [.NET özel etkinlik](#net-custom-activity) bu hizmeti bağlı. 

### <a name="linked-service"></a>Bağlı hizmet
Aşağıdaki tablonun hello hello Azure JSON tanımında bağlı Azure Batch hizmetinin kullanılan hello özellikleri için açıklamalar sağlanır.

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| type |Merhaba type özelliği çok ayarlanmalıdır**AzureBatch**. |Evet |
| accountName |Hello Azure Batch hesabı adı. |Evet |
| accessKey |Hello Azure Batch hesabı için erişim anahtarı. |Evet |
| poolName |Sanal makinelerin hello havuzunun adı. |Evet |
| linkedServiceName |Hello Azure Storage bağlı hizmeti Azure bağlı Batch hizmeti ile ilişkili adı. Bu bağlı hizmetin dosyaları hazırlama için kullanılan toorun hello etkinliği ve hello Etkinlik yürütme günlüklerini depolamak gerekli. |Evet |


#### <a name="json-example"></a>JSON örneği

```json
{
    "name": "AzureBatchLinkedService",
    "properties": {
        "type": "AzureBatch",
        "typeProperties": {
            "accountName": "<Azure Batch account name>",
            "accessKey": "<Azure Batch account key>",
            "poolName": "<Azure Batch pool name>",
            "linkedServiceName": "<Specify associated storage linked service reference here>"
        }
    }
}
```

## <a name="azure-machine-learning"></a>Azure Machine Learning
Bir Machine Learning toplu Puanlama uç noktası data factory ile bir Azure Machine Learning bağlantılı hizmet tooregister oluşturun. Bu bilgisayarda çalıştırabilir iki veri dönüştürme etkinlikleri bağlantılı hizmeti: [Machine Learning toplu iş yürütme etkinliği](#machine-learning-batch-execution-activity), [Machine Learning kaynak güncelleştirme etkinliği](#machine-learning-update-resource-activity). 

### <a name="linked-service"></a>Bağlı hizmet
Aşağıdaki tablonun hello hello Azure JSON tanımında bağlı Azure Machine Learning hizmetinin kullanılan hello özellikleri için açıklamalar sağlanır.

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| Tür |Merhaba type özelliği ayarlanmalıdır: **AzureML**. |Evet |
| mlEndpoint |Merhaba toplu işlem Puanlama URL'sini. |Evet |
| apikey ile yapılan |Merhaba, çalışma alanı modelinin API yayımladı. |Evet |

#### <a name="json-example"></a>JSON örneği

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://[batch scoring endpoint]/jobs",
            "apiKey": "<apikey>"
        }
    }
}
```

## <a name="azure-data-lake-analytics"></a>Azure Data Lake Analytics
Oluşturduğunuz bir **Azure Data Lake Analytics** bağlantılı hizmet toolink bir Azure Data Lake Analytics işlem hizmeti tooan Azure data factory hello kullanmadan önce [Data Lake Analytics U-SQL etkinliği](data-factory-usql-activity.md) ardışık düzeninde .

### <a name="linked-service"></a>Bağlı hizmet

Aşağıdaki tablonun hello hello JSON tanımında bir Azure Data Lake Analytics bağlantılı hizmetinin kullanılan hello özellikleri için açıklamalar sağlanır. 

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| Tür |Merhaba type özelliği ayarlanmalıdır: **AzureDataLakeAnalytics**. |Evet |
| accountName |Azure Data Lake Analytics hesap adı. |Evet |
| dataLakeAnalyticsUri |Azure Data Lake Analytics URI. |Hayır |
| Yetkilendirme |Yetkilendirme kodu, tıkladıktan sonra otomatik olarak alınır **Authorize** hello Data Factory düzenleyici ve Tamamlanıyor hello OAuth oturum açma düğmesi. |Evet |
| subscriptionId |Azure abonelik kimliği |Hayır (belirtilmezse, veri fabrikası kullanılan hello abonelik). |
| resourceGroupName |Azure kaynak grubu adı |Hayır (belirtilmezse, veri fabrikası kullanılan hello kaynak grubu). |
| SessionID |Merhaba OAuth yetkilendirme oturumundan oturum kimliği. Her oturum kimliği benzersiz olup yalnızca bir kez kullanılabilir. Merhaba Data Factory Düzenleyici kullandığınızda, bu otomatik olarak oluşturulan kimliğidir. |Evet |


#### <a name="json-example"></a>JSON örneği
Aşağıdaki örneğine hello JSON tanımı için bir Azure Data Lake Analytics bağlı hizmet sağlar.

```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "<account name>",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>",
            "subscriptionId": "<subscription id>",
            "resourceGroupName": "<resource group name>"
        }
    }
}
```

## <a name="azure-sql-database"></a>Azure SQL Database
Azure SQL bağlı hizmeti oluşturma ve hello ile kullanma [saklı yordam etkinliği](#stored-procedure-activity) tooinvoke Data Factory işlem hattı bir saklı yordam. 

### <a name="linked-service"></a>Bağlı hizmet
bir Azure SQL veritabanı toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**AzureSqlDatabase**ve hello özelliklerinde aşağıdaki belirtin **typeProperties**bölümü:  

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| connectionString |Tooconnect toohello Azure SQL veritabanı örneğinde hello connectionString özelliği için gerekli bilgiler belirtin. |Evet |

#### <a name="json-example"></a>JSON örneği

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Bkz: [Azure SQL Bağlayıcısı](data-factory-azure-sql-connector.md#linked-service-properties) makale bu bağlı hizmetin hakkında ayrıntılı bilgi için.

## <a name="azure-sql-data-warehouse"></a>Azure SQL Veri Ambarı
Bir Azure SQL Data Warehouse bağlı hizmet oluşturma ve hello ile kullanma [saklı yordam etkinliği](data-factory-stored-proc-activity.md) tooinvoke Data Factory işlem hattı bir saklı yordam. 

### <a name="linked-service"></a>Bağlı hizmet
Azure SQL Data Warehouse toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**AzureSqlDW**ve hello özelliklerinde aşağıdaki belirtin **typeProperties**bölümü:  

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| connectionString |Tooconnect toohello Azure SQL Data Warehouse örneğine hello connectionString özelliği için gerekli bilgiler belirtin. |Evet |

#### <a name="json-example"></a>JSON örneği

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Daha fazla bilgi için bkz: [Azure SQL Data Warehouse Bağlayıcısı](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) makalesi. 

## <a name="sql-server"></a>SQL Server 
Bir SQL Server bağlantılı hizmet oluşturma ve hello ile kullanma [saklı yordam etkinliği](data-factory-stored-proc-activity.md) tooinvoke Data Factory işlem hattı bir saklı yordam. 

### <a name="linked-service"></a>Bağlı hizmet
Bağlı hizmet türü oluşturma **OnPremisesSqlServer** toolink bir şirket içi SQL Server veritabanı tooa data factory. Aşağıdaki tablonun hello JSON öğeleri belirli tooon şirket içi SQL Server bağlantılı hizmet açıklamasını sağlar.

Aşağıdaki tablonun hello JSON öğeleri belirli tooSQL Server bağlantılı hizmeti için bir açıklama sağlar.

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| type |Merhaba type özelliği ayarlanmalıdır: **OnPremisesSqlServer**. |Evet |
| connectionString |SQL kimlik doğrulaması veya Windows kimlik doğrulaması kullanarak tooconnect toohello şirket içi SQL Server veritabanı gerekli connectionString bilgiler belirtin. |Evet |
| gatewayName |Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi SQL Server veritabanını kullanmanız gerekir. |Evet |
| kullanıcı adı |Windows kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin. Örnek: **domainname\\kullanıcıadı**. |Hayır |
| password |Merhaba username için belirtilen hello kullanıcı hesabı için parola belirtin. |Hayır |

Hello kullanarak kimlik bilgilerini şifrelemek **yeni AzureRmDataFactoryEncryptValue** cmdlet'i ve bunları hello aşağıdaki örnekte gösterildiği gibi hello bağlantı dizesinde kullanabilirsiniz (**EncryptedCredential** özellik):  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a>Örnek: SQL kimlik doğrulaması kullanmak için JSON

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a>Örnek: JSON'ı Windows kimlik doğrulaması kullanma

Kullanıcı adı ve parolası belirtilmişse, ağ geçidi bunları tooimpersonate hello kullanır belirtilen kullanıcı hesabı tooconnect toohello şirket içi SQL Server veritabanı. Aksi takdirde, ağ geçidi toohello SQL Server doğrudan hello güvenlik bağlamında ağ geçidi (kendi başlangıç hesabı) ile bağlanır.

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Daha fazla bilgi için bkz: [SQL Server Bağlayıcısı](data-factory-sqlserver-connector.md#linked-service-properties) makalesi.

## <a name="data-transformation-activities"></a>VERİ DÖNÜŞTÜRME ETKİNLİKLERİ

Etkinlik | Açıklama
-------- | -----------
[Hdınsight Hive etkinliği](#hdinsight-hive-activity) | Merhaba Data Factory işlem hattı Hdınsight Hive etkinliğiyle kendi Hive sorguları ya da isteğe bağlı Windows/Linux tabanlı Hdınsight kümesi yürütür. 
[Hdınsight Pig etkinliği](#hdinsight-pig-activity) | Merhaba Data Factory işlem hattı Hdınsight Pig etkinlik kendi Pig sorgular veya isteğe bağlı Windows/Linux tabanlı Hdınsight kümesi yürütür.
[HDInsight MapReduce Etkinliği](#hdinsight-mapreduce-activity) | Merhaba Data Factory işlem hattı Hdınsight MapReduce etkinlik kendi MapReduce programları veya isteğe bağlı Windows/Linux tabanlı Hdınsight kümesi yürütür.
[HDInsight Akış Etkinliği](#hdinsight-streaming-activity) | Data Factory işlem hattı Hello Hdınsight akış etkinliği Hadoop akış programlar kendi veya isteğe bağlı Windows/Linux tabanlı Hdınsight kümesi yürütür.
[HDInsight Spark Etkinliği](#hdinsight-spark-activity) | Merhaba Data Factory işlem hattı Hdınsight Spark etkinliğinde Spark programlar kendi Hdınsight kümesinde yürütür. 
[Machine Learning Batch Yürütme Etkinliği](#machine-learning-batch-execution-activity) | Web hizmeti Tahmine dayalı analiz için azure Data Factory etkinleştirir, tooeasily yayımlanan bir Azure Machine Learning kullanan komut zincirleri oluşturun. Bir Azure Data Factory işlem hattı toplu iş yürütme etkinliği Hello kullanarak, Machine Learning web hizmeti toomake tahminleri toplu hello veriler üzerinde çağırabilirsiniz. 
[Machine Learning Kaynak Güncelleştirme Etkinliği](#machine-learning-update-resource-activity) | Zaman içinde veri kümeleri hello Machine Learning Puanlama denemeler retrained toobe yeni kullanarak gereken Tahmine dayalı modelleri hello girin. Yeniden eğitme ile tamamladıktan sonra web hizmeti ile Merhaba Puanlama tooupdate hello Machine Learning modelini retrained istiyor. Merhaba kaynak güncelleştirme etkinliği tooupdate hello web hizmeti ile Merhaba yeni eğitilmiş model kullanabilirsiniz.
[Saklı Yordam Etkinliği](#stored-procedure-activity) | Data Factory işlem hattı tooinvoke bir saklı yordam veri depolarına aşağıdaki hello birinde hello saklı yordam etkinliği kullanabilirsiniz: Azure SQL Database, Azure SQL Data Warehouse, SQL Server veritabanı kuruluşunuzdaki veya bir Azure VM. 
[Data Lake Analytics U-SQL etkinliği](#data-lake-analytics-u-sql-activity) | Data Lake Analytics U-SQL etkinliği Azure Data Lake Analytics kümede bir U-SQL komut dosyasını çalıştırır.  
[.NET özel etkinliği](#net-custom-activity) | Tootransform verileri Data Factory tarafından desteklenmeyen bir şekilde ihtiyacınız varsa, kendi veri işleme mantığı ile özel bir etkinlik oluşturmak ve hello ardışık düzeninde hello etkinliği kullanın. Bir Azure Batch hizmeti ya da Azure Hdınsight kümesi kullanarak hello özel .NET etkinliği toorun yapılandırabilirsiniz. 

     
## <a name="hdinsight-hive-activity"></a>HDInsight Hive Etkinliği
Aşağıdaki özelliklere Hive etkinliği JSON tanımında hello belirtebilirsiniz. Merhaba type özelliği hello etkinliğinin olmalıdır: **Hdınsighthive**. Hdınsight bağlı hizmeti ilk oluşturun ve hello için bir değer olarak hello adını belirtmeniz gerekir **linkedServiceName** özelliği. Merhaba aşağıdaki özellikleri hello desteklenir **typeProperties** bölümünde etkinlik tooHDInsightHive hello türü ayarladığınızda:

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| Komut dosyası |Merhaba Hive betiği satır içi belirtin |Hayır |
| komut dosyası yolu |Mağaza hello Hive betiği bir Azure blob depolama alanındaki ve hello yol toohello dosyası sağlayın. 'Komut dosyası' veya 'scriptPath' özelliğini kullanın. Her ikisi birlikte kullanılamaz. Merhaba dosya adı büyük/küçük harf duyarlıdır. |Hayır |
| tanımlar |İçinde hello Hive betiği 'hiveconf' kullanarak başvurmak için anahtar/değer çiftleri olarak parametrelerini belirtin |Hayır |

Bu tür belirli toohello Hive etkinliği özellikleridir. Diğer özellikleri (Merhaba typeProperties bölüm dışında) tüm etkinlikler için desteklenir.   

### <a name="json-example"></a>JSON örneği
JSON aşağıdaki hello Hdınsight Hive etkinliği ardışık düzeninde tanımlar.  

```json
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
    "inputs": [
      {
        "name": "input tables"
      }
    ],
    "outputs": [
      {
        "name": "output tables"
      }
    ],
    "linkedServiceName": "MyHDInsightLinkedService",
    "typeProperties": {
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```

Daha fazla bilgi için bkz: [Hive etkinliği](data-factory-hive-activity.md) makalesi. 

## <a name="hdinsight-pig-activity"></a>HDInsight Pig Etkinliği
Aşağıdaki özelliklere Pig etkinlik JSON tanımında hello belirtebilirsiniz. Merhaba type özelliği hello etkinliğinin olmalıdır: **HDInsightPig**. Hdınsight bağlı hizmeti ilk oluşturun ve hello için bir değer olarak hello adını belirtmeniz gerekir **linkedServiceName** özelliği. Merhaba aşağıdaki özellikleri hello desteklenir **typeProperties** bölümünde etkinlik tooHDInsightPig hello türü ayarladığınızda: 

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| Komut dosyası |Merhaba Pig betiği satır içi belirtin |Hayır |
| komut dosyası yolu |Bir Azure blob depolama alanına Hello Pig betiği depolar ve hello yol toohello dosyası sağlayın. 'Komut dosyası' veya 'scriptPath' özelliğini kullanın. Her ikisi birlikte kullanılamaz. Merhaba dosya adı büyük/küçük harf duyarlıdır. |Hayır |
| tanımlar |Pig betiği hello içinde başvurmak için anahtar/değer çiftleri olarak parametrelerini belirtin |Hayır |

Bu tür belirli toohello Pig etkinlik özellikleridir. Diğer özellikleri (Merhaba typeProperties bölüm dışında) tüm etkinlikler için desteklenir.   

### <a name="json-example"></a>JSON örneği

```json
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
            "inputs": [
                  {
                    "name": "input tables"
                  }
            ],
            "outputs": [
                  {
                    "name": "output tables"
                  }
            ],
            "linkedServiceName": "MyHDInsightLinkedService",
            "typeProperties": {
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```

Daha fazla bilgi için bkz: [Pig etkinlik](#data-factory-pig-activity.md) makalesi. 

## <a name="hdinsight-mapreduce-activity"></a>HDInsight MapReduce Etkinliği
Aşağıdaki özelliklere MapReduce etkinliği JSON tanımında hello belirtebilirsiniz. Merhaba type özelliği hello etkinliğinin olmalıdır: **HDInsightMapReduce**. Hdınsight bağlı hizmeti ilk oluşturun ve hello için bir değer olarak hello adını belirtmeniz gerekir **linkedServiceName** özelliği. Merhaba aşağıdaki özellikleri hello desteklenir **typeProperties** bölümünde etkinlik tooHDInsightMapReduce hello türü ayarladığınızda: 

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| jarLinkedService | Merhaba adını hizmeti hello hello JAR dosyasını içeren Azure Storage için bağlı. | Evet |
| jarFilePath | Yol toohello JAR dosyasını hello Azure depolama. | Evet | 
| className | Merhaba JAR dosyasına hello Ana sınıfın adı. | Evet | 
| Bağımsız değişkenler | Bağımsız değişkenleri hello MapReduce program virgülle ayrılmış listesi. Çalışma zamanında gördüğünüz birkaç ek bağımsız değişkenler (örneğin: mapreduce.job.tags) hello MapReduce çerçeveden. toodifferentiate, hello MapReduce bağımsız değişkenleriyle seçeneği ve değer bağımsız değişken olarak hello aşağıdaki örnekte gösterildiği gibi kullanmayı düşünün (- s,--giriş,--çıkış vb. olan göre bunların değerleri hemen ardından seçenekleri) | Hayır | 

### <a name="json-example"></a>JSON örneği

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix toodetermine hello similarity between two items",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                    "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": ["-s", "SIMILARITY_LOGLIKELIHOOD", "--input", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input", "--output", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/", "--maxSimilaritiesPerItem", "500", "--tempDir", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"]
                },
                "inputs": [
                    {
                        "name": "MahoutInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "MahoutOutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "MahoutActivity",
                "description": "Custom Map Reduce toogenerate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

Daha fazla bilgi için bkz: [MapReduce etkinliği](data-factory-map-reduce.md) makalesi. 

## <a name="hdinsight-streaming-activity"></a>HDInsight Akış Etkinliği
Aşağıdaki özelliklere Hadoop akış etkinliği JSON tanımında hello belirtebilirsiniz. Merhaba type özelliği hello etkinliğinin olmalıdır: **HDInsightStreaming**. Hdınsight bağlı hizmeti ilk oluşturun ve hello için bir değer olarak hello adını belirtmeniz gerekir **linkedServiceName** özelliği. Merhaba aşağıdaki özellikleri hello desteklenir **typeProperties** bölümünde etkinlik tooHDInsightStreaming hello türü ayarladığınızda: 

| Özellik | Açıklama | 
| --- | --- |
| Eşleyici | Merhaba Eşleyici yürütülebilir adı. Merhaba örnekte cat.exe hello Eşleyici yürütülebilir ' dir.| 
| reducer | Merhaba reducer yürütülebilir adı. Merhaba örnekte wc.exe hello reducer yürütülebilir ' dir. | 
| Giriş | Merhaba Eşleyici için giriş dosyası (konum dahil). Merhaba örnekte: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample hello blob kapsayıcısı, veri/örnek/Gutenberg hello klasördür ve davinci.txt hello blob. |
| Çıktı | Merhaba reducer için (konum dahil) çıktı dosyası. Merhaba çıktısı hello Hadoop akış işi, bu özelliği için belirtilen toohello konumu yazılır. |
| filePaths | Merhaba Eşleyici ve reducer yürütülebilir dosyalar için yollar. Merhaba örnekte: "adfsample/example/apps/wc.exe" adfsample hello blob kapsayıcısı, örnek/uygulamaları hello klasördür ve wc.exe hello çalıştırılabilir. | 
| fileLinkedService | Merhaba hello filePaths bölümünde belirtilen hello dosyaları içeren Azure depolama temsil eden azure depolama bağlı hizmeti. | 
| Bağımsız değişkenler | Bağımsız değişkenleri hello MapReduce program virgülle ayrılmış listesi. Çalışma zamanında gördüğünüz birkaç ek bağımsız değişkenler (örneğin: mapreduce.job.tags) hello MapReduce çerçeveden. toodifferentiate, hello MapReduce bağımsız değişkenleriyle seçeneği ve değer bağımsız değişken olarak hello aşağıdaki örnekte gösterildiği gibi kullanmayı düşünün (- s,--giriş,--çıkış vb. olan göre bunların değerleri hemen ardından seçenekleri) | 
| Getdebugınfo | İsteğe bağlı bir öğe. TooFailure ayarlandığında hello günlükleri yalnızca hatada indirilir. TooAll ayarlandığında, günlükleri hello yürütme durumu bağımsız olarak daima yüklenir. | 

> [!NOTE]
> Bir çıkış veri kümesi için Hadoop akış etkinliği Merhaba hello belirtmelisiniz **çıkarır** özelliği. Bu veri kümesi yalnızca gerekli toodrive hello ardışık düzen zamanlaması (saatlik, günlük, vs.) bir kukla dataset olabilir. Merhaba etkinliği bir girdi almazsa hello hello etkinliği bir girdi veri kümesi belirtme atlayabilirsiniz **girişleri** özelliği.  

## <a name="json-example"></a>JSON örneği

```json
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": ["<nameofthecluster>/example/apps/wc.exe","<nameofthecluster>/example/apps/cat.exe"],
                    "fileLinkedService": "StorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00",
        "end": "2014-01-05T00:00:00"
    }
}
```

Daha fazla bilgi için bkz: [Hadoop akış etkinliği](data-factory-hadoop-streaming-activity.md) makalesi. 

## <a name="hdinsight-spark-activity"></a>HDInsight Spark Etkinliği
Aşağıdaki özelliklere Spark etkinlik JSON tanımında hello belirtebilirsiniz. Merhaba type özelliği hello etkinliğinin olmalıdır: **HDInsightSpark**. Hdınsight bağlı hizmeti ilk oluşturun ve hello için bir değer olarak hello adını belirtmeniz gerekir **linkedServiceName** özelliği. Merhaba aşağıdaki özellikleri hello desteklenir **typeProperties** bölümünde etkinlik tooHDInsightSpark hello türü ayarladığınızda: 

| Özellik | Açıklama | Gerekli |
| -------- | ----------- | -------- |
| rootPath | Hello Azure Blob kapsayıcısı ve hello Spark dosyasını içeren klasör. Merhaba dosya adı büyük/küçük harf duyarlıdır. | Evet |
| entryFilePath | Göreli yol toohello kök klasöründe hello Spark kod/paketi. | Evet |
| className | Uygulamanın Java/Spark ana sınıfı | Hayır | 
| Bağımsız değişkenler | Komut satırı bağımsız değişkenleri toohello Spark program listesi. | Hayır | 
| proxyUser | Merhaba kullanıcı hesabı tooimpersonate tooexecute hello Spark programı | Hayır | 
| sparkConfig | Spark yapılandırma özellikleri. | Hayır | 
| Getdebugınfo | Merhaba Spark günlük dosyalarını kopyalanan toohello Hdınsight küme tarafından kullanılan Azure depolama olduğunda belirtir (veya) sparkJobLinkedService tarafından belirtilen. İzin verilen değerler: None, her zaman veya hata. Varsayılan değer: yok. | Hayır | 
| sparkJobLinkedService | Merhaba hello Spark iş dosyası, bağımlılıklar ve günlükleri tutan Azure Storage bağlı hizmeti.  Bu özellik için bir değer belirtmezseniz, Hdınsight kümesi ile ilişkili hello depolama kullanılır. | Hayır |

### <a name="json-example"></a>JSON örneği

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-05T00:00:00",
        "end": "2017-02-06T00:00:00"
    }
}
```
Hello aşağıdaki noktaları göz önünde bulundurun: 

- Merhaba **türü** özelliği çok ayarlanmış**HDInsightSpark**.
- Merhaba **rootPath** çok ayarlanır**adfspark\\pyFiles** adfspark hello Azure Blob kapsayıcısı ve pyFiles olduğu ince kapsayıcıdaki klasörüdür. Bu örnekte, hello Azure Blob Storage hello hello Spark kümesi ile ilişkili olan bir ' dir. Merhaba dosya tooa yükleyebilirsiniz farklı Azure depolama. Bunu yaparsanız, bir Azure Storage bağlı hizmeti toolink bu depolama hesabı toohello veri fabrikası oluşturun. Ardından, hello için bir değer olarak hello hello bağlı hizmetin adını belirtin **sparkJobLinkedService** özelliği. Bkz: [Spark etkinlik özellikleri](#spark-activity-properties) bu özellik ve Spark etkinlik hello tarafından desteklenen diğer özellikleri hakkında ayrıntılı bilgi için.
- Merhaba **entryFilePath** toohello ayarlamak **test.py**, hello python dosyası değil. 
- Merhaba **Getdebugınfo** özelliği çok ayarlanmış**her zaman**, yani hello günlük dosyaları her zaman oluşturulan (başarılı veya başarısız).  

    > [!IMPORTANT]
    > Bir sorun giderme amacıyla sürece bu özellik tooAlways'ı bir üretim ortamında ayarlamayın öneririz. 
- Merhaba **çıkarır** bölümü bir çıkış veri kümesi yok. Merhaba spark program herhangi bir çıktı üretmez olsa bile bir çıkış veri kümesi belirtmeniz gerekir. Merhaba çıkış veri kümesi sürücüleri hello zamanlama hello ardışık düzen (saatlik, günlük, vs.).

Merhaba etkinliği hakkında daha fazla bilgi için bkz: [Spark etkinlik](data-factory-spark.md) makalesi.  

## <a name="machine-learning-batch-execution-activity"></a>Machine Learning Batch Yürütme Etkinliği
Aşağıdaki özelliklere Azure ML toplu iş yürütme etkinliği JSON tanımında hello belirtebilirsiniz. Merhaba type özelliği hello etkinliğinin olmalıdır: **AzureMLBatchExecution**. Bağlantılı hizmet ilk öğrenme Azure bir makine oluşturma ve hello için bir değer olarak hello adını belirtmeniz gerekir **linkedServiceName** özelliği. Merhaba aşağıdaki özellikleri hello desteklenir **typeProperties** bölümünde etkinlik tooAzureMLBatchExecution hello türü ayarladığınızda:

Özellik | Açıklama | Gerekli 
-------- | ----------- | --------
WebServiceInput etkinliğine | hello Azure ML web hizmeti için bir giriş olarak Hello dataset toobe geçirildi. Bu veri kümesi de hello girişleri hello etkinliğinin bulunması gerekir. |WebServiceInput etkinliğine veya webServiceInputs kullanın. | 
webServiceInputs | Veri kümeleri toobe hello Azure ML web hizmeti için girdi olarak geçirilen belirtin. Merhaba web hizmeti birden fazla girdi aldığı durumlarda hello WebServiceInput etkinliğine özelliğini kullanmak yerine hello webServiceInputs özelliğini kullanın. Merhaba tarafından başvurulan veri kümeleri **webServiceInputs** hello etkinliği de dahil edilmesi **girişleri**. | WebServiceInput etkinliğine veya webServiceInputs kullanın. | 
webServiceOutputs | Çıktı hello Azure ML web hizmeti olarak atanan hello veri kümesi. Hello web hizmeti, bu veri kümesini çıktı verilerini döndürür. | Evet | 
globalParameters | Bu bölümde hello web hizmeti parametreleri için değerleri belirtin. | Hayır | 

### <a name="json-example"></a>JSON örneği
Bu örnekte, hello etkinlik hello dataset sahip **MLSqlInput** giriş olarak ve **MLSqlOutput** hello çıktı olarak. Merhaba **MLSqlInput** hello kullanılarak geçirilen bir giriş toohello web hizmeti tarafından olarak **WebServiceInput etkinliğine** JSON özelliği. Merhaba **MLSqlOutput** hello kullanılarak geçirilen bir çıktı toohello Web hizmeti tarafından olarak **webServiceOutputs** JSON özelliği. 

```json
{
   "name": "MLWithSqlReaderSqlWriter",
   "properties": {
      "description": "Azure ML model with sql azure reader/writer",
      "activities": [{
         "name": "MLSqlReaderSqlWriterActivity",
         "type": "AzureMLBatchExecution",
         "description": "test",
         "inputs": [ { "name": "MLSqlInput" }],
         "outputs": [ { "name": "MLSqlOutput" } ],
         "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
         "typeProperties":
         {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
               "output1": "MLSqlOutput"
            },
            "globalParameters": {
               "Database server name": "<myserver>.database.windows.net",
               "Database name": "<database>",
               "Server user account name": "<user name>",
               "Server user account password": "<password>"
            }              
         },
         "policy": {
            "concurrency": 1,
            "executionPriorityOrder": "NewestFirst",
            "retry": 1,
            "timeout": "02:00:00"
         }
      }],
      "start": "2016-02-13T00:00:00",
       "end": "2016-02-14T00:00:00"
   }
}
```

Merhaba JSON örnekte hello Azure Machine Learning hizmetinin kullandığı bir okuyucu ve yazıcı modülü tooread/yazma verilerden Web dağıtılan / tooan Azure SQL veritabanı. Bu Web hizmetini şu dört parametreler hello sunar: veritabanı sunucu adı, veritabanı adı, sunucu kullanıcı hesabı adı ve sunucu kullanıcı hesabı parolası.

> [!NOTE]
> Yalnızca girişleri ve çıkışları hello AzureMLBatchExecution etkinlik parametreleri toohello Web hizmeti geçirilebilir. Örneğin, yukarıdaki JSON parçacığı hello MLSqlInput bir giriş toohello WebServiceInput etkinliğine parametresi ile bir giriş toohello Web hizmeti geçirilen AzureMLBatchExecution etkinlik ' dir.

## <a name="machine-learning-update-resource-activity"></a>Machine Learning Kaynak Güncelleştirme Etkinliği
Aşağıdaki özelliklere Azure ML güncelleştirme kaynak etkinliği JSON tanımında hello belirtebilirsiniz. Merhaba type özelliği hello etkinliğinin olmalıdır: **AzureMLUpdateResource**. Bağlantılı hizmet ilk öğrenme Azure bir makine oluşturma ve hello için bir değer olarak hello adını belirtmeniz gerekir **linkedServiceName** özelliği. Merhaba aşağıdaki özellikleri hello desteklenir **typeProperties** bölümünde etkinlik tooAzureMLUpdateResource hello türü ayarladığınızda:

Özellik | Açıklama | Gerekli 
-------- | ----------- | --------
trainedModelName | Merhaba adını modeli retrained. | Evet |  
trainedModelDatasetName | İşlemi yeniden eğitme hello tarafından döndürülen veri kümesi işaret toohello iLearner dosya. | Evet | 

### <a name="json-example"></a>JSON örneği
Merhaba işlem hattına sahip iki etkinlik: **AzureMLBatchExecution** ve **AzureMLUpdateResource**. Hello Azure ML toplu iş yürütme etkinliği hello eğitim veri giriş olarak alır ve bir iLearner dosya bir çıktı olarak üretir. Merhaba etkinlik verileri eğitim hello girişle hello eğitim web hizmeti (web hizmeti olarak sunulan eğitim denemenizi) çağırır ve hello webservice hello ilearner dosya alır. Merhaba placeholderBlob hello Azure Data Factory hizmeti toorun hello ardışık düzen tarafından gerekli olan yalnızca bir kukla çıktı veri kümesi ' dir.


```json
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "trained model",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [{ "name": "trainedModelBlob" }],
                "outputs": [{ "name": "placeholderBlob" }],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00",
        "end": "2016-02-14T00:00:00"
    }
}
```

## <a name="data-lake-analytics-u-sql-activity"></a>Data Lake Analytics U-SQL Etkinliği
Aşağıdaki U-SQL etkinliği JSON tanımında özelliklere hello belirtebilirsiniz. Merhaba type özelliği hello etkinliğinin olmalıdır: **DataLakeAnalyticsU SQL**. Bir Azure Data Lake Analytics bağlı hizmeti oluşturma ve hello için bir değer olarak hello adını belirtmeniz gerekir **linkedServiceName** özelliği. Merhaba aşağıdaki özellikleri hello desteklenir **typeProperties** bölümünde etkinlik tooDataLakeAnalyticsU-SQL hello türü ayarladığınızda: 

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| scriptPath |Merhaba U-SQL betiğini içeren yolu toofolder. Merhaba dosyasının adı büyük/küçük harf duyarlıdır. |Hayır (komut dosyası kullanırsanız) |
| scriptLinkedService |Merhaba betik toohello veri fabrikası içeren hello depolamayı bağlı hizmet |Hayır (komut dosyası kullanırsanız) |
| Komut dosyası |ScriptPath ve scriptLinkedService belirtme yerine satır içi betiği belirtin. Örneğin: "komut dosyası": "Veritabanı oluştur test". |Hayır (scriptPath ve scriptLinkedService kullanıyorsanız) |
| degreeOfParallelism |Merhaba en fazla düğüm sayısını toorun hello işi aynı anda kullanılır. |Hayır |
| Öncelik |Sıraya alınan tüm işlerden seçili toorun olması gereken ilk belirler. Merhaba alt hello numarası hello yüksek hello önceliği. |Hayır |
| parametreler |Merhaba U-SQL komut dosyası için parametreler |Hayır |

### <a name="json-example"></a>JSON örneği

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This pipeline computes events for en-gb locale and date less than Feb 19, 2012.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00",
        "end": "2015-08-08T01:00:00",
        "isPaused": false
    }
}
```

Daha fazla bilgi için bkz: [Data Lake Analytics U-SQL etkinliği](data-factory-usql-activity.md). 

## <a name="stored-procedure-activity"></a>Saklı Yordam Etkinliği
Aşağıdaki özelliklere saklı yordam etkinliği JSON tanımında hello belirtebilirsiniz. Merhaba type özelliği hello etkinliğinin olmalıdır: **SqlServerStoredProcedure**. Bir bağlı hizmetler aşağıdaki hello birini oluşturun ve hello için bir değer olarak hello hello bağlı hizmet adını belirtmeniz gerekir **linkedServiceName** özelliği:

- SQL Server 
- Azure SQL Database
- Azure SQL Veri Ambarı

Merhaba aşağıdaki özellikleri hello desteklenir **typeProperties** bölümünde etkinlik tooSqlServerStoredProcedure hello türü ayarladığınızda:

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| storedProcedureName |Hello Azure SQL veritabanı veya çıktı tablosu kullanır hello hello bağlantılı hizmeti tarafından temsil edilen Azure SQL Data Warehouse hello saklı yordamı Hello adını belirtin. |Evet |
| storedProcedureParameters |Saklı yordam parametreleri için değerleri belirtin. Toopass parametresi için null ihtiyacınız varsa, hello sözdizimini kullanın: "param1": null (tüm küçük harf). Bu özellik kullanma hakkında örnek toolearn aşağıdaki hello bakın. |Hayır |

Bir giriş veri kümesi belirtirseniz, ('Hazır' durumunda) kullanılabilir olmalıdır Merhaba depolanan yordam etkinliği toorun. Merhaba girdi veri kümesi hello saklı yordama parametre olarak kullanılamaz. Başlangıç hello saklı yordam etkinliği önce yalnızca kullanılan toocheck hello bağımlılık vardır. Bir çıkış veri kümesi için bir saklı yordam etkinliği belirtmeniz gerekir. 

Çıktı veri kümesi belirtir hello **zamanlama** hello için saklı yordam etkinliği (saatlik, haftalık, aylık, vb.). Merhaba çıktı veri kümesi kullanmalısınız bir **bağlantılı hizmeti** tooan Azure SQL Database veya bir Azure SQL Data Warehouse veya SQL Server veritabanı istediğiniz saklı yordam toorun hello başvuruyor. Merhaba çıktı veri kümesi hello saklı yordamın sonraki işleme biçimini toopass hello sonuç olarak başka bir etkinlik tarafından kullanılabileceği ([etkinlikleri zincirleme](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) hello ardışık düzeninde. Ancak, veri fabrikası otomatik olarak bir saklı yordam toothis dataset hello çıktısını yazmaz. Bu, çıktı veri kümesi noktalarına hello o yazma tooa SQL tablosu hello saklı yordamı olur. Bazı durumlarda, hello çıktı veri kümesi olabilir bir **kukla dataset**, toospecify hello zamanlama hello çalıştırmak için depolanan yordam etkinliği yalnızca kullanılır.  

### <a name="json-example"></a>JSON örneği

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
                "outputs": [{ "name": "sprocsampleout" }],
                "name": "SprocActivitySample"
            }
        ],
         "start": "2016-08-02T00:00:00",
         "end": "2016-08-02T05:00:00",
        "isPaused": false
    }
}
```

Daha fazla bilgi için bkz: [saklı yordam etkinliği](data-factory-stored-proc-activity.md) makalesi. 

## <a name="net-custom-activity"></a>.NET özel etkinliği
.NET özel etkinlik JSON tanımını özelliklerinde aşağıdaki hello belirtebilirsiniz. Merhaba type özelliği hello etkinliğinin olmalıdır: **DotNetActivity**. Azure Hdınsight bağlı hizmeti oluşturmak veya bağlı bir Azure Batch hizmeti ve hello için bir değer olarak hello hello bağlı hizmet adını belirtin **linkedServiceName** özelliği. Merhaba aşağıdaki özellikleri hello desteklenir **typeProperties** bölümünde etkinlik tooDotNetActivity hello türü ayarladığınızda:
 
| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| AssemblyName | Merhaba derlemesinin adı. Merhaba örnek,: **MyDotnetActivity.dll**. | Evet |
| EntryPoint |Merhaba IDotNetActivity arabirimini uygulayan hello sınıfının adı. Merhaba örnek,: **MyDotNetActivityNS.MyDotNetActivity** burada MyDotNetActivityNS hello ad alanı ve MyDotNetActivity hello sınıfı.  | Evet | 
| PackageLinkedService | Merhaba hello özel etkinlik zip dosyasını içeren toohello blob depolama işaret Azure Storage bağlı hizmeti adı. Merhaba örnek,: **AzureStorageLinkedService**.| Evet |
| PackageFile | Merhaba ZIP dosyasının adı. Merhaba örnek,: **customactivitycontainer/MyDotNetActivity.zip**. | Evet |
| extendedProperties | Tanımlayın ve toohello .NET kodu geçirin genişletilmiş özellikler. Bu örnekte, hello **SliceStart** değişkeni hello SliceStart system değişkenine göre tooa değere ayarlanır. | Hayır | 

### <a name="json-example"></a>JSON örneği

```json
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "AzureBatchLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00",
    "end": "2016-11-16T05:00:00",
    "isPaused": false
  }
}
```

Ayrıntılı bilgi için bkz: [veri fabrikasında özel etkinlikleri kullanmak](data-factory-use-custom-activities.md) makalesi. 

## <a name="next-steps"></a>Sonraki Adımlar
Eğitim aşağıdaki hello bakın: 

- [Öğretici: kopyalama etkinliği ile işlem hattı oluşturma](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [Öğretici: hive etkinliği ile işlem hattı oluşturma](data-factory-build-your-first-pipeline-using-editor.md)