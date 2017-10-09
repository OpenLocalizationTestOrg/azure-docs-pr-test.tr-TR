---
title: "aaaCreate/zamanlama ardışık düzen, veri fabrikası'nda zinciri etkinlikler | Microsoft Docs"
description: "Veri dönüştürme ve toocreate bir veri ardışık düzeninde Azure Data Factory toomove öğrenin. Bir veri akışı tooproduce hazır toouse bilgileri tabanlı oluşturun."
keywords: "Veri ardışık düzeni, veri akışı tabanlı"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 13b137c7-1033-406f-aea7-b66f25b313c0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/12/2017
ms.author: shlo
ms.openlocfilehash: 4a0fc20f98ce6453c16955e97fddb891926c173a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="pipelines-and-activities-in-azure-data-factory"></a>İşlem hatlarının ve etkinliklerin Azure veri fabrikası
Bu makalede, işlem hatlarının ve etkinliklerin Azure Data Factory anlamak ve bunları tooconstruct uçtan uca veri odaklı iş akışlarının veri işleme senaryolarını ve veri taşıma için yardımcı olur.  

> [!NOTE]
> Bu makalede, ilerlemiş olduğunu varsayar [giriş tooAzure Data Factory](data-factory-introduction.md). Hands-on-data Factory oluşturma konusunda deneyim yoksa oluşturulmak [veri dönüştürme öğretici](data-factory-build-your-first-pipeline.md) ve/veya [veri taşıma öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) , bu makalede daha iyi anlamanıza yardımcı.  

## <a name="overview"></a>Genel Bakış
Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir. İşlem hattı, bir araya geldiğinde bir görev gerçekleştiren mantıksal etkinlik grubudur. bir ardışık düzende Hello etkinlik Eylemler tooperform verilerinizde tanımlayın. Örneğin, bir şirket içi SQL Server tooan Azure Blob Storage kopyalama etkinliği toocopy verilerden kullanabilir. Ardından, hello blob depolama tooproduce çıktı verilerini Azure Hdınsight küme tooprocess/dönüştürme verileri üzerinde bir Hive betiği çalıştıran bir Hive etkinliği kullanın. Son olarak, ikinci kopyalama etkinliği toocopy hello çıkış veri tooan Azure SQL veri hangi iş zekası (BI) üzerinde raporlama çözümleri yerleşiktir ambarı kullanın. 

Bir etkinliğin sıfır veya sıfırdan çok giriş [veri kümesi](data-factory-create-datasets.md) olabilir ve her etkinlik bir veya birden çok çıkış [veri kümesi](data-factory-create-datasets.md) oluşturabilir. Merhaba Aşağıdaki diyagramda hello arasındaki ilişkiyi ardışık düzen, etkinlik ve veri kümesi veri fabrikasında gösterir: 

![Ardışık düzen, etkinlik ve veri kümesi arasındaki ilişki](media/data-factory-create-pipelines/relationship-pipeline-activity-dataset.png)

İşlem hattı toomanage etkinliklerin her biri yerine bir küme olarak ayrı ayrı sağlar. Örneğin, dağıtma, zamanlama, askıya alma ve hello ardışık düzendeki etkinlik ile bağımsız olarak ilgilenme yerine bir ardışık düzen Sürdür.

Data Factory iki tür etkinliği destekler: veri taşıma etkinlikleri ve veri dönüştürme etkinlikleri. Her etkinlik sıfır veya daha fazla giriş olabilir [veri kümeleri](data-factory-create-datasets.md) ve bir veya daha fazla çıkış veri kümeleri oluşturma.

Bir giriş veri kümesi hello giriş hello ardışık düzeninde bir etkinliğin temsil eder ve bir çıkış veri kümesi hello çıktı hello etkinliği temsil eder. Veri kümeleri tablolar, dosyalar, klasörler ve belgeler gibi farklı veri depolarındaki verileri tanımlar. Bir veri kümesi oluşturduktan sonra, bu kümeyi bir işlem hattındaki etkinliklerle birlikte kullanabilirsiniz. Örneğin, veri kümesi bir Kopyalama Etkinliğinin veya HDInsightHive Etkinliğinin giriş/çıkış veri kümesi olabilir. Veri kümeleri hakkında daha fazla bilgi için [Azure Data Factory'de Veri Kümeleri](data-factory-create-datasets.md) makalesine bakın.

### <a name="data-movement-activities"></a>Veri taşıma etkinlikleri
Data Factory kopyalama etkinliği, bir kaynak veri deposu tooa havuz veri deposundan verileri kopyalar. Data Factory veri depolarına aşağıdaki hello destekler. Herhangi bir kaynaktan veri tooany havuz yazılabilir. Bir veri deposu toolearn nasıl tıklatın toocopy veri tooand o depolama alanından.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Veri depolar ile * şirket içi olabilir veya Azure Iaas ve tooinstall gerektiren [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) , şirket içi/Azure Iaas makinede.

Daha fazla bilgi için [Veri Taşıma Etkinlikleri](data-factory-data-movement-activities.md) makalesine bakın.

### <a name="data-transformation-activities"></a>Veri dönüştürme etkinlikleri
[!INCLUDE [data-factory-transformation-activities](../../includes/data-factory-transformation-activities.md)]

Daha fazla bilgi için [Veri Dönüştürme Etkinlikleri](data-factory-data-transformation-activities.md) makalesine bakın.

### <a name="custom-net-activities"></a>Özel .NET etkinlikleri 
Toomove verilere ihtiyacınız/bir veri kopyalama etkinliği hello deposu değil desteği veya kendi mantığı kullanarak verileri, oluşturmak, bir **özel .NET etkinlik**. Özel bir etkinlik oluşturma ve kullanma hakkında ayrıntılı bilgi için bkz. [Azure Data Factory işlem hattında özel etkinlikler kullanma](data-factory-use-custom-activities.md).

## <a name="schedule-pipelines"></a>Zamanlama komut zincirleri
İşlem hattı yalnızca arasında etkin olduğu kendi **Başlat** zaman ve **son** saat. Bunu hello başlangıç saatinden önce veya sonra hello bitiş saati yürütülmedi. Hello ardışık düzen duraklatıldığında, kendi başlangıç ve bitiş zamanı yedeklemiş yürütülmedi. Ardışık Düzen toorun için bunu duraklatılması değil. Bkz: [zamanlama ve yürütme](data-factory-scheduling-and-execution.md) zamanlama ve yürütme şeklini Azure Data Factory'de toounderstand.

## <a name="pipeline-json"></a>İşlem Hattı JSON
Bir işlem hattının JSON biçiminde nasıl tanımlandığına daha yakından bakalım. Merhaba genel yapısı bir ardışık düzeni için şu şekilde görünür:

```json
{
    "name": "PipelineName",
    "properties": 
    {
        "description" : "pipeline description",
        "activities":
        [

        ],
        "start": "<start date-time>",
        "end": "<end date-time>",
        "isPaused": true/false,
        "pipelineMode": "scheduled/onetime",
        "expirationTime": "15.00:00:00",
        "datasets": 
        [
        ]
    }
}
```

| Etiket | Açıklama | Gerekli |
| --- | --- | --- |
| ad |Merhaba ardışık düzen adı. Ardışık Düzen hello hello eylemi temsil eden adını gerçekleştirir belirtin. <br/><ul><li>En fazla karakter sayısı: 260</li><li>Bir harf, sayı veya alt çizgi (_) ile başlamalıdır</li><li>Şu karakterler kullanılamaz: ".", "+","?", "/", "<",">", "*", "%", "&", ":","\\"</li></ul> |Evet |
| açıklama | Hangi hello ardışık düzeni için kullanılan açıklayan hello metni belirtin. |Evet |
| etkinlikler | Merhaba **etkinlikleri** bölüm içinde tanımlanan bir veya daha fazla etkinlik olabilir. Merhaba hello etkinlikleri JSON öğesi hakkında ayrıntılı bilgi için sonraki bölüme bakın. | Evet |  
| start | Merhaba ardışık düzeni için başlangıç tarihi / saati. Olmalıdır [ISO biçiminde](http://en.wikipedia.org/wiki/ISO_8601). Örneğin: `2016-10-14T16:32:41Z`. <br/><br/>Olası toospecify yerel saat örneğin bir EST zamanı. Örnek aşağıda verilmiştir: `2016-02-27T06:00:00-05:00`", 6'da tahmini olduğu<br/><br/>Merhaba başlangıç ve bitiş özellikleri birlikte hello ardışık düzen etkin süresini belirtin. Çıktı dilimler yalnızca ile etkin bu dönemde üretilir. |Hayır<br/><br/>Merhaba end özelliği için bir değer belirtirseniz, hello başlangıç özelliği için değer belirtmeniz gerekir.<br/><br/>Merhaba başlangıç ve bitiş zamanlarını hem de boş toocreate işlem hattı olabilir. Her iki değeri de belirtilmelisiniz tooset etkin dönem hello ardışık düzen toorun için bir. Başlangıç ve bitiş zamanlarını belirtmezseniz, bir işlem hattı oluştururken, bunları ayarlayabilirsiniz daha sonra hello kümesi AzureRmDataFactoryPipelineActivePeriod cmdlet'ini kullanarak. |
| Bitiş | Merhaba ardışık düzeni için bitiş tarihi / saati. Belirtilen ISO biçiminde olmalıdır. Örneğin, `2016-10-14T17:32:41Z` <br/><br/>Olası toospecify yerel saat örneğin bir EST zamanı. Örnek aşağıda verilmiştir: `2016-02-27T06:00:00-05:00`, 6'da tahmini olduğu<br/><br/>toorun hello ardışık kalıcı olarak belirtin 9999-09-09 hello end özelliği hello değeri olarak. <br/><br/> Yalnızca kendi başlangıç ve bitiş zamanı arasında bir ardışık düzen etkindir. Bunu hello başlangıç saatinden önce veya sonra hello bitiş saati yürütülmedi. Hello ardışık düzen duraklatıldığında, kendi başlangıç ve bitiş zamanı yedeklemiş yürütülmedi. Ardışık Düzen toorun için bunu duraklatılması değil. Bkz: [zamanlama ve yürütme](data-factory-scheduling-and-execution.md) zamanlama ve yürütme şeklini Azure Data Factory'de toounderstand. |Hayır <br/><br/>Merhaba başlangıç özelliği için bir değer belirtirseniz, hello end özelliği için değer belirtmeniz gerekir.<br/><br/>Hello için notlarına bakın **Başlat** özelliği. |
| isPaused | Set tootrue, hello ardışık düzen çalışmazsa. Bu durum hello duraklatıldı. Varsayılan değer = false. Bu özellik tooenable kullanın veya bir işlem hattı devre dışı bırakabilirsiniz. |Hayır |
| pipelineMode | zamanlama için başlangıç yöntemi hello ardışık düzeni için çalışır. İzin verilen değerler: (varsayılan), zamanlanmış kez.<br/><br/>'Zamanlanmış' Bu hello ardışık düzen tooits etkin dönemi (başlangıç ve bitiş saati) göre belirli bir zaman aralığında çalışır gösterir. 'Kez' Bu hello ardışık düzen yalnızca bir kez çalışır gösterir. Oluşturulduktan sonra kez ardışık düzen şu anda değiştiren/güncelleştirilemiyor. Bkz: [Onetime ardışık düzen](#onetime-pipeline) kez ayar hakkındaki ayrıntılar için. |Hayır |
| expirationTime | Hangi hello için oluşturulduktan sonra süre [tek seferlik ardışık düzen](#onetime-pipeline) geçerli olduğunu ve sağlanan kalmalıdır. Her etkin başarısız oldu, yok veya çalıştığında, hello ardışık düzen otomatik olarak bir kez silinmiş onu hello süre sonu zamanı ulaşır. Merhaba varsayılan değer:`"expirationTime": "3.00:00:00"`|Hayır |
| Veri kümeleri |Merhaba ardışık düzeninde tanımlanan etkinlikleri tarafından kullanılan veri kümeleri toobe listesi. Bu özellik belirli toothis ardışık düzen ve hello veri fabrikası içinde tanımlı değil kullanılan toodefine veri kümeleri olabilir. Bu ardışık düzen içinde tanımlanan veri kümeleri yalnızca bu ardışık düzen tarafından kullanılabilir ve paylaşılamaz. Bkz: [veri kümeleri kapsamlı](data-factory-create-datasets.md#scoped-datasets) Ayrıntılar için. |Hayır |

## <a name="activity-json"></a>Etkinlik JSON
Merhaba **etkinlikleri** bölüm içinde tanımlanan bir veya daha fazla etkinlik olabilir. Her etkinlik en üst düzey yapı izlenerek hello sahiptir:

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
    },
    "scheduler":
    {
    }
}
```

Aşağıdaki tabloda, JSON tanımını hello etkinliğinde özelliklerini açıklamaktadır:

| Etiket | Açıklama | Gerekli |
| --- | --- | --- |
| ad | Merhaba etkinlik adı. Merhaba etkinliği gerçekleştiren hello eylemi temsil eden bir ad belirtin. <br/><ul><li>En fazla karakter sayısı: 260</li><li>Bir harf, sayı veya alt çizgi (_) ile başlamalıdır</li><li>Şu karakterler kullanılamaz: ".", "+","?", "/", "<",">", "*", "%", "&", ":","\\"</li></ul> |Evet |
| açıklama | Hangi etkinlik hello veya için kullanılan açıklayan metin |Evet |
| type | Merhaba etkinlik türü. Merhaba bkz [veri taşıma etkinlikleri](#data-movement-activities) ve [veri dönüştürme etkinlikleri](#data-transformation-activities) bölümleri etkinlikler farklı türde. |Evet |
| Girişleri |Merhaba etkinlik tarafından kullanılan giriş tabloları<br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |Evet |
| Çıkışları |Merhaba etkinlik tarafından kullanılan çıkış tabloları.<br/><br/>`// one output table`<br/>`"outputs":  [ { "name": "outputtable1" } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": "outputtable1" }, { "name": "outputtable2" }  ],` |Evet |
| linkedServiceName |Merhaba etkinlik tarafından kullanılan hello bağlı hizmetin adı. <br/><br/>Bir etkinlik toohello gerekli hesaplama ortamı bağlantılar hello bağlantılı hizmeti belirtin gerektirebilir. |Hdınsight etkinliği ve Azure Machine Learning toplu iş Puanlama etkinliği için Evet <br/><br/>Diğer tümü için hayır |
| typeProperties |Merhaba özelliklerinde **typeProperties** bölüm hello etkinlik türüne bağlıdır. bir etkinliğin toosee türü özellikleri hello önceki bölümdeki bağlantılar toohello etkinliği tıklatın. | Hayır |
| ilke |Merhaba etkinlik hello çalışma zamanı davranışını etkileyen ilkeleri. Belirtilmezse, varsayılan ilkeler kullanılır. |Hayır |
| Zamanlayıcı | "Zamanlayıcı" Merhaba etkinliği için zamanlama kullanılan toodefine istenen özelliğidir. Onun alt olanları hello içinde hello aynı hello olan [dataset kullanılabilirliği özelliğinde](data-factory-create-datasets.md#dataset-availability). |Hayır |


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

## <a name="sample-copy-pipeline"></a>Örnek kopyalama işlem hattı
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
    "start": "2016-07-12T00:00:00Z",
    "end": "2016-07-13T00:00:00Z"
  }
} 
```

Hello aşağıdaki noktaları göz önünde bulundurun:

* Merhaba etkinlikler bölümünde, yalnızca bir etkinlik olduğundan, **türü** çok ayarlanır**kopya**.
* Merhaba etkinlik çok kümesi için giriş**InputDataset** ve hello etkinlik çok kümesi için çıkış**OutputDataset**. JSON biçiminde veri kümeleri tanımlamak için [Veri Kümeleri](data-factory-create-datasets.md) makalesine bakın. 
* Merhaba, **typeProperties** bölümünde **BlobSource** hello kaynak türü olarak belirtilir ve **SqlSink** hello Havuz türü olarak belirtilir. Merhaba, [veri taşıma etkinlikleri](#data-movement-activities) bölümünde, veri depolama, veri deposundan için/veri taşıma hakkında daha fazla kaynak veya havuz toolearn olarak toouse istediğiniz hello'ı tıklatın. 

Bu ardışık düzen oluşturma izlenecek tam yol için bkz: [Öğreticisi: Blob Storage tooSQL veritabanı ' veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

## <a name="sample-transformation-pipeline"></a>Örnek dönüştürme işlem hattı
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
        "start": "2016-04-01T00:00:00Z",
        "end": "2016-04-02T00:00:00Z",
        "isPaused": false
    }
}
```

Hello aşağıdaki noktaları göz önünde bulundurun: 

* Merhaba etkinlikler bölümünde, yalnızca bir etkinlik olduğundan, **türü** çok ayarlanır**Hdınsighthive**.
* Merhaba Hive betik dosyası **partitionweblogs.hql**, hello Azure depolama hesabı depolanır (adlı hello scriptLinkedService tarafından belirtilen **AzureStorageLinkedService**) ve  **komut dosyası** hello kapsayıcı klasöründe **adfgetstarted**.
* Merhaba `defines` bölümdür toohello hive betiğini Hive yapılandırma değerleri olarak geçirilir kullanılan toospecify hello çalışma zamanı ayarları (örneğin `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).

Merhaba **typeProperties** bölümü, her bir dönüşüm etkinlik için farklıdır. toolearn dönüştürme etkinliğine için desteklenen tür özellikleri hakkında tıklatın hello dönüştürme hello etkinliğinde [veri dönüştürme etkinlikleri](#data-transformation-activities) tablo. 

Bu ardışık düzen oluşturma izlenecek tam yol için bkz: [Öğreticisi: Hadoop kümesi kullanarak ilk ardışık düzen tooprocess verilerinizi yapı](data-factory-build-your-first-pipeline.md). 

## <a name="multiple-activities-in-a-pipeline"></a>Bir işlem hattında birden çok etkinlik
Merhaba önceki iki örnek ardışık düzen yalnızca bir etkinlik olması. Bir işlem hattında birden fazla etkinliğiniz olabilir.  

Merhaba etkinlikler için giriş veri dilimi hazır olup olmadığını hello etkinlikleri bir ardışık düzende birden çok etkinliği varsa ve bir etkinlik çıktısını başka bir etkinliğin bir giriş değil, paralel olarak çalışabilir. 

İki etkinlik hello çıkış veri kümesi bir etkinlik hello Merhaba, girdi veri kümesi olarak sağlayarak diğer etkinliklerin zincir. yalnızca hello önce bir başarıyla tamamlandığında hello ikinci etkinlik yürütür.

![Merhaba aktivitelerde zincirleme aynı kanalı](./media/data-factory-create-pipelines/chaining-one-pipeline.png)

Bu örnekte, iki etkinlik hello ardışık düzen vardır: Activity1 ve Activity2. Merhaba Activity1 Dataset1 bir girdi olarak alır ve bir çıktı üretir Dataset2. Merhaba etkinlik Dataset2 bir girdi olarak alır ve bir çıktı üretir Dataset3. Activity1 hello çıktısını bu yana (Dataset2) olan Activity2 hello girişi, hello Activity2 etkinliği başarıyla tamamlandığında hello sonra çalıştırır ve üretir hello Dataset2 dilim. Merhaba Activity1 herhangi bir nedenden dolayı başarısız olursa ve hello Dataset2 dilim üretmez hello etkinlik 2, dilim için çalışmaz (örneğin: 9 AM too10 'M). 

Ayrıca, farklı ardışık düzenlerinde etkinlikleri zincir.

![İki ardışık düzende zincirleme etkinlikleri](./media/data-factory-create-pipelines/chaining-two-pipelines.png)

Bu örnekte, Pipeline1 Dataset1 bir girdi olarak alır ve Dataset2 bir çıktı olarak üretir yalnızca bir etkinlik vardır. Merhaba Pipeline2 de girdi ve çıktı olarak Dataset3 Dataset2 alır yalnızca bir etkinlik vardır. 

Daha fazla bilgi için bkz: [zamanlama ve yürütme](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

## <a name="create-and-monitor-pipelines"></a>Oluşturma ve işlem hatlarını izleme
Ardışık Düzen Bu araçlar ya da SDK'ları birini kullanarak oluşturabilirsiniz. 

- Kopyalama Sihirbazı. 
- Azure portalına
- Visual Studio
- Azure PowerShell
- Azure Resource Manager şablonu
- REST API
- .NET API’si

Bu araçlar ya da SDK'ları biri kullanılarak işlem hatlarını oluşturmak için öğreticileri adım adım yönergeler için aşağıdaki hello bakın.
 
- [Veri dönüştürme etkinliğine sahip işlem hattı oluşturma](data-factory-build-your-first-pipeline.md)
- [Veri taşıma etkinliği ile işlem hattı oluşturma](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

Oluşturulan ve dağıtılan bir ardışık düzen olduktan sonra izlemek ve yönetebilirsiniz Azure portal dikey penceresi veya izleme ve yönetme uygulaması kullanılarak işlem hatlarınızı hello. Merhaba aşağıdaki konularda adım adım yönergeler için bkz. 

- [İzleme ve Azure portal dikey penceresi kullanılarak işlem hatlarını yönetme](data-factory-monitor-manage-pipelines.md).
- [İzleme ve işlem hatlarını izleme ve yönetme uygulaması'nı kullanarak yönetme](data-factory-monitor-manage-app.md)


## <a name="onetime-pipeline"></a>Kez ardışık düzen
Oluşturma ve bir ardışık düzen toorun düzenli aralıklarla zamanlama (örneğin: saatlik veya günlük) içinde hello başlangıç ve bitiş zamanları hello ardışık düzen tanımında belirtin. Bkz: [etkinlikleri zamanlama](#scheduling-and-execution) Ayrıntılar için. Yalnızca bir kez çalışır bir ardışık düzen de oluşturabilirsiniz. toodo Merhaba, ayarladığınız **pipelineMode** hello özelliğinde tanımı çok potansiyel satış**kez** hello JSON örnek aşağıdaki gösterildiği gibi. Bu özellik için varsayılan değer Hello **zamanlanmış**.

```json
{
    "name": "CopyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ]
                "name": "CopyActivity-0"
            }
        ]
        "pipelineMode": "OneTime"
    }
}
```

Merhaba aşağıdakileri göz önünde bulundurun:

* **Başlat** ve **son** kez hello ardışık düzeni için belirtilmemiş.
* **Kullanılabilirlik** giriş ve çıkış veri kümeleri belirtilir (**sıklığı** ve **aralığı**), veri fabrikası hello değerleri kullanmıyor olsa bile.  
* Diyagram görünümü tek seferlik ardışık düzen göstermez. Bu davranış tasarım gereğidir.
* Tek seferlik ardışık düzen güncelleştirilemiyor. Tek seferlik Ardışık düzenin kopyalama, yeniden adlandırmak, güncelleştirme özellikleri ve toocreate dağıtmak başka bir.


## <a name="next-steps"></a>Sonraki Adımlar
- Veri kümeleri hakkında daha fazla bilgi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi. 
- Ardışık Düzen nasıl zamanlanmış ve yürütülen hakkında daha fazla bilgi için bkz: [zamanlama ve yürütme Azure veri fabrikası'nda](data-factory-scheduling-and-execution.md) makalesi. 
  

