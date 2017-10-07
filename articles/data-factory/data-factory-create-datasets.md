---
title: "Azure Data Factory'deki veri kümelerini aaaCreate | Microsoft Docs"
description: "Azure Data Factory toocreate kümelerinde gibi özellikleri kullanma örnekleri içeren nasıl uzaklığı ve anchorDateTime öğrenin."
keywords: "veri kümesi, veri kümesi örnek oluşturma, örnek uzaklığı"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 0614cd24-2ff0-49d3-9301-06052fd4f92a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: shlo
ms.openlocfilehash: 181859ed250595d756df73e9ebcac08d9e7184c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="datasets-in-azure-data-factory"></a>Azure Data Factory'deki veri kümelerini
Bu makalede hangi veri kümeleri, JSON biçiminde nasıl tanımlanan açıklanmıştır ve Azure Data Factory içinde kullanılan nasıl ardışık düzenleri. Bu, hello dataset JSON tanımında her bölüm (örneğin, yapısı, kullanılabilirlik ve ilke) hakkında ayrıntılar sağlar. Merhaba makale ayrıca hello kullanmak için örnekler **uzaklık**, **anchorDateTime**, ve **stili** dataset JSON tanımında özellikleri.

> [!NOTE]
> Yeni tooData Fabrika olup olmadığını görmek [giriş tooAzure Data Factory](data-factory-introduction.md) bir genel bakış. Veri fabrikaları oluşturma ile uygulamalı deneyim yoksa daha iyi anlamak okuma hello tarafından kazanmadan [veri dönüştürme öğretici](data-factory-build-your-first-pipeline.md) ve hello [veri taşıma Öğreticisi](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

## <a name="overview"></a>Genel Bakış
Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir. A **ardışık düzen** mantıksal bir gruplandırmasıdır **etkinlikleri** görev birlikte gerçekleştirin. bir ardışık düzende Hello etkinlik Eylemler tooperform verilerinizde tanımlayın. Örneğin, bir şirket içi SQL Server tooAzure Blob depolama alanına kopyalama etkinliği toocopy verilerden kullanabilirsiniz. Ardından, Blob Depolama tooproduce çıktı verilerini Azure Hdınsight küme tooprocess verileri üzerinde bir Hive betiği çalıştıran bir Hive etkinliği kullanabilir. Son olarak, bir ikinci kopya etkinliği toocopy hello çıkış veri tooAzure SQL Data Warehouse, çözümleri yerleşik raporlama hangi iş zekası (BI) üstünde kullanabilir. Ardışık Düzen ve etkinlikleri hakkında daha fazla bilgi için bkz: [işlem hatlarının ve etkinliklerin Azure Data Factory](data-factory-create-pipelines.md).

Bir etkinlik sıfır veya daha fazla giriş alabilir **veri kümeleri**ve bir veya daha fazla çıkış veri kümeleri oluşturma. Bir giriş veri kümesi hello ardışık düzeninde bir etkinliğin hello giriş ve bir çıkış veri kümesi hello çıktı hello etkinliği temsil eder. Veri kümeleri tablolar, dosyalar, klasörler ve belgeler gibi farklı veri depoları içindeki verileri tanımlamak. Örneğin, bir Azure Blob dataset hello blob kapsayıcısı ve klasör hangi hello ardışık düzen hello veri okumalısınız Blob depolama alanına belirtir. 

Bir veri kümesi oluşturmadan önce oluşturun bir **bağlantılı hizmeti** toolink verilerinizi depolamak toohello veri fabrikası. Bağlı hizmetler Data Factory tooconnect tooexternal kaynakları için gerekli hello bağlantı bilgilerini tanımlayın bağlantı dizeleri çok gibidir. Veri kümelerini SQL tablolarının, dosyalar, klasörler ve belgeler gibi hello bağlı veri depoları içindeki verileri tanımlamak. Örneğin, bir Azure depolama hizmeti depolama hesabı toohello data factory bağlantılı. Bir Azure Blob dataset hello blob kapsayıcısı ve işlenen hello giriş BLOB'ları toobe içeren hello klasörü temsil eder. 

Bir örnek senaryo aşağıda verilmiştir. Blob Depolama tooa SQL veritabanından veri toocopy, iki bağlı hizmet oluşturma: Azure Storage ve Azure SQL veritabanı. Ardından, iki veri kümesi oluşturun: (toohello Azure Storage bağlı hizmeti ifade eder) Azure Blob veri kümesi ve (toohello bağlı Azure SQL veritabanı hizmetinin atıfta bulunmaktadır) Azure SQL tablosu veri kümesi. Azure Storage ve Azure SQL bağlantılı Hizmetleri çalışma zamanı tooconnect tooyour Azure Storage ve Azure SQL Database, veri fabrikası sırasıyla kullandığı bağlantı dizelerini içeren veritabanı hello. Hello Azure Blob dataset hello blob kapsayıcısı ve Blob Depolama alanınızın hello giriş blobları içeren blob klasörü belirtir. Hello Azure SQL tablosu veri kümesi, SQL veritabanı toowhich hello verilerinizi hello SQL tablosuna kopyalanan toobe belirtir.

Merhaba Aşağıdaki diyagramda hello arasındaki ilişkiler ardışık düzen, etkinlik, veri kümesi ve bağlantılı hizmet veri fabrikasında gösterilmektedir: 

![Ardışık düzen, etkinlik, veri kümesi, bağlı hizmetler arasındaki ilişki](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a>JSON veri kümesi
Veri fabrikasında bir veri kümesini JSON biçiminde şu şekilde tanımlanır:

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
| ad |Merhaba DataSet'in adı. Bkz: [Azure Data Factory - adlandırma kuralları](data-factory-naming-rules.md) adlandırma kuralları. |Evet |NA |
| type |Merhaba veri kümesi türü. Data Factory ile desteklenen hello türlerinden birini belirtin (örneğin: AzureBlob, AzureSqlTable). <br/><br/>Ayrıntılar için bkz [veri kümesi türü](#Type). |Evet |NA |
| yapısı |Merhaba dataset şema.<br/><br/>Ayrıntılar için bkz [veri kümesi yapısı](#Structure). |Hayır |NA |
| typeProperties | Merhaba türü özellikleri her türü için farklı (örneğin: Azure Blob, Azure SQL tablosu). Desteklenen hello türleri ve özellikleri hakkında daha fazla bilgi için bkz: [veri kümesi türü](#Type). |Evet |NA |
| external | Boole veya bir veri kümesi açıkça data factory işlem hattı tarafından üretilir olup olmadığını toospecify bayrağı. Merhaba giriş veri kümesi bir etkinlik için hello geçerli ardışık düzen tarafından üretilen değil, bu bayrağı tootrue ayarlayın. Bu bayrak tootrue hello hello ilk etkinliğin girdi veri kümesi için hello ardışık düzeninde ayarlayın.  |Hayır |False |
| availability | (Örneğin, saatlik veya günlük) işlemi penceresini hello veya model hello dataset üretim için dilimleme hello tanımlar. Her veri birimi, tüketilen ve etkinlik çalışması tarafından üretilen veri dilimi adı verilir. Bir çıkış veri kümesi Hello kullanılabilirliğini kümesi toodaily (sıklığı - Day, aralığı - 1) ise, bir dilim günlük oluşturulur. <br/><br/>Ayrıntılar için bkz [Dataset kullanılabilirliği](#Availability). <br/><br/>Merhaba dataset hakkında ayrıntılı bilgi için modeli dilimleme bkz hello [zamanlama ve yürütme](data-factory-scheduling-and-execution.md) makalesi. |Evet |NA |
| İlke |Merhaba ölçütleri veya hello dataset dilimler karşılamanız gerekmektedir hello koşulu tanımlar. <br/><br/>Merhaba Ayrıntılar için bkz [Dataset İlkesi](#Policy) bölümü. |Hayır |NA |

## <a name="dataset-example"></a>Veri kümesi örneği
Aşağıdaki örneğine hello hello dataset adlı bir tablo temsil **MyTable** bir SQL veritabanında.

```json
{
    "name": "DatasetSample",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties":
        {
            "tableName": "MyTable"
        },
        "availability":
        {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

Hello aşağıdaki noktaları göz önünde bulundurun:

* **tür** tooAzureSqlTable ayarlanır.
* **tableName** type özelliği (belirli tooAzureSqlTable türü), tooMyTable ayarlanır.
* **linkedServiceName** tooa bağlantılı hizmet türü hello sonraki JSON parçacığında tanımlanan AzureSqlDatabase başvuruyor. 
* **Kullanılabilirlik sıklığı** tooDay, ayarlayın ve **aralığı** too1 ayarlanır. Bu, o hello dataset dilim günlük üretilen anlamına gelir.  

**AzureSqlLinkedService** şu şekilde tanımlanır:

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>@<servername>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

JSON parçacığı önceki hello:

* **tür** tooAzureSqlDatabase ayarlanır.
* **connectionString** type özelliği bilgi tooconnect tooa SQL veritabanını belirtir.  

Gördüğünüz gibi hello bağlantılı hizmet tanımlar nasıl tooconnect tooa SQL veritabanı. Merhaba dataset hangi tablo girdi olarak kullanılır ve ardışık düzeninde hello etkinliğinin çıkış tanımlar.   

> [!IMPORTANT]
> Bir veri kümesi hello ardışık düzen tarafından üretilen sürece bunu olarak işaretlenmelidir **dış**. Bu ayar genellikle bir ardışık düzendeki ilk etkinliğin tooinputs uygulanır.   


## <a name="Type"></a>Veri kümesi türü
kullandığınız hello veri deposunda hello dataset Hello türüne bağlıdır. Merhaba aşağıdaki tablonun Data Factory ile desteklenen veri depoları listesi için bkz. Bir veri deposu toolearn tıklatın nasıl toocreate bağlı hizmet ve bu veriler için bir veri kümesi depolar.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Veri depolar ile * şirket içi olabilir veya hizmet (Iaas) olarak Azure altyapısı. Bu veri depolarına tooinstall gerektiren [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md).

Merhaba önceki bölümdeki Hello örnekte hello dataset hello türü çok ayarlanır**AzureSqlTable**. Benzer şekilde, Azure Blob veri kümesi için hello türü hello veri kümesi çok ayarlıdır**AzureBlob**hello JSON aşağıdaki gösterildiği gibi:

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

## <a name="Structure"></a>Veri kümesi yapısı
Merhaba **yapısı** bölümdür isteğe bağlıdır. Merhaba kümesinin hello şema, tarafından içeren bir koleksiyon adları ve sütunların veri türlerini tanımlar. Kullanılan tooconvert türleri ve hello kaynak toohello hedef harita sütunlarından hello yapısı bölüm tooprovide türü bilgileri kullanın. Aşağıdaki örneğine hello hello dataset üç sütun vardır: `slicetimestamp`, `projectname`, ve `pageviews`. Bunlar dize, dize ve ondalık, sırasıyla türüdür.

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

Her sütun hello yapısında aşağıdaki özelliklere hello içerir:

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| ad |Merhaba sütunun adı. |Evet |
| type |Merhaba sütununun veri türü.  |Hayır |
| Kültür |. Merhaba türü .NET türü olduğunda kullanılan NET tabanlı kültürü toobe: `Datetime` veya `Datetimeoffset`. Merhaba varsayılan `en-us`. |Hayır |
| Biçimi |Biçimlendirme dizesi toobe hello türü .NET türü olduğunda kullanılan: `Datetime` veya `Datetimeoffset`. |Hayır |

Merhaba aşağıdaki yönergeleri tooinclude yapısı bilgileri ne zaman ve hangi tooinclude hello içinde belirlemenize yardımcı **yapısı** bölümü.

* **Yapılandırılmış veri kaynakları için**, yalnızca kaynak sütunları toosink sütunları eşlemek istediğiniz ve adları olan değil hello aynı hello yapısı bölümünde belirtin. Bu tür bir yapılandırılmış veri kaynağı hello verilerin kendisini veri şeması ve tür bilgileri depolar. SQL Server, Oracle ve Azure tablo yapılandırılmış veri kaynakları örneklerindendir. 
  
    Tür bilgileri zaten yapılandırılmış veri kaynakları için kullanılabilir olduğu gibi hello yapısı bölüm eklediğinizde türü bilgileri içermemelidir.
* **Şema okuma veri kaynaklarında (özellikle Blob Depolama) için**, herhangi bir şema veya türü bilgi hello verilerle depolamadan toostore veri seçebilirsiniz. Toomap kaynak sütunları toosink sütunları istediğinizde bu tür veri kaynağı yapısı içerir. Ayrıca yapısı hello veri kümesi kopyalama etkinliği için bir giriş, kaynak veri kümesinin veri türleri dönüştürülmüş toonative türleri hello havuz için kullanılabilir olmalı ve zaman içerir. 
    
    Veri Fabrikası yapısındaki türü bilgileri sağlamak için değerleri aşağıdaki hello destekler: **Int16, Int32, Int64, tek, Double, Decimal, bayt [], Boolean, dize, GUID, Datetime, Datetimeoffset ve Timespan**. Ortak dil belirtimi (CLS) bu değerler-uyumlu. NET tabanlı türü değerleri.

Veri Fabrikası otomatik olarak veri kaynağına veri dosyaları tooa havuz veri deposunu taşırken tür dönüşümleri gerçekleştirir. 
  

## <a name="dataset-availability"></a>DataSet kullanılabilirliği
Merhaba **kullanılabilirlik** hello işleme penceresi (örneğin, saatlik, günlük veya haftalık) hello veri kümesi için bir veri kümesi bölümünde tanımlar. Etkinlik pencereleri hakkında daha fazla bilgi için bkz: [zamanlama ve yürütme](data-factory-scheduling-and-execution.md).

Kullanılabilirlik bölümden hello hello çıktı veri kümesi ya da saatlik üretilen veya hello girdi veri kümesi saatlik kullanılabilir belirtir:

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

Merhaba ardışık düzen başlangıç ve bitiş zamanlarını aşağıdaki hello varsa:  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

Merhaba çıktı veri kümesi üretilen saatlik içinde hello ardışık düzeni başlangıç ve bitiş zamanları. Bu nedenle, bu ardışık düzen, her etkinlik penceresinin (00: 00-1 AM, 1 AM - 2 AM, 2: 00 - 3 AM, 3 AM - 4 AM, 4 AM - 5 AM) için bir tane tarafından üretilen beş veri kümesi dilimler vardır. 

Merhaba aşağıdaki tabloda hello Kullanılabilirliği bölümünde kullanabileceğiniz özellikleri açıklanmaktadır:

| Özellik | Açıklama | Gerekli | Varsayılan |
| --- | --- | --- | --- |
| frequency |Veri kümesi dilim üretim Hello zaman birimini belirtir.<br/><br/><b>Sıklık desteklenen</b>: dakika, saat, gün, hafta, ay |Evet |NA |
| interval |Sıklığı çarpanı belirtir.<br/><br/>"X sıklığı aralığını" ne sıklıkta hello dilim üretilen belirler. Örneğin, dilimlenebilir saatlik olarak başka bir veri kümesi toobe hello varsa, ayarladığınız <b>sıklığı</b> çok<b>saat</b>, ve <b>aralığı</b> çok<b>1</b>.<br/><br/>Belirtirseniz unutmayın **sıklığı** olarak **Minute**, 15'den küçük hello aralığı toono ayarlamanız gerekir. |Evet |NA |
| stili |Merhaba dilim hello başlangıç veya bitiş hello aralığının olarak üretilen belirtir.<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul>Varsa **sıklığı** çok ayarlanır**ay**, ve **stili** çok ayarlanır**EndOfInterval**, hello dilim ayın son günü hello üzerinde oluşturulur. Varsa **stili** çok ayarlanır**StartOfInterval**, hello dilim ayın ilk günü hello üzerinde oluşturulur.<br/><br/>Varsa **sıklığı** çok ayarlanır**gün**, ve **stili** çok ayarlanır**EndOfInterval**, hello dilim hello hello günün son bir saat oluşturulur.<br/><br/>Varsa **sıklığı** çok ayarlanır**saat**, ve **stili** çok ayarlanır**EndOfInterval**, hello dilim hello hello saat sonunda oluşturulur. Örneğin, hello 1 PM - 2 PM dönem için bir dilim için 2 saat hello dilim oluşturulur. |Hayır |EndOfInterval |
| anchorDateTime |Merhaba Zamanlayıcı toocompute dataset dilim sınırları tarafından kullanılan süre içinde mutlak konum Hello tanımlar. <br/><br/>Bu propoerty hello sıklığı belirtilenden daha ayrıntılı tarih kısımlarını varsa daha ayrıntılı bölümleri hello unutmayın göz ardı edilir. Örneğin, hello **aralığı** olan **saatlik** (sıklığı: saat ve aralığı: 1) ve hello **anchorDateTime** içeren **dakika ve saniyeleri**, dakika ve saniyeleri bölümlerini hello **anchorDateTime** göz ardı edilir. |Hayır |01/01/0001 |
| uzaklık |Tarafından hangi hello başlangıç ve bitiş tüm veri kümesi dilim gölgeye Timespan. <br/><br/>Her iki unutmayın **anchorDateTime** ve **uzaklık** belirtilirse, hello sonucudur birleştirilmiş hello shift. |Hayır |NA |

### <a name="offset-example"></a>uzaklık örneği
Varsayılan olarak, her gün (`"frequency": "Day", "interval": 1`) dilimler 00: 00 (gece yarısı) Eşgüdümlü Evrensel Saat (UTC) başlatın. Merhaba başlangıç saati toobe 6'da UTC saati bunun yerine isterseniz, hello aşağıdaki kod parçacığında gösterildiği gibi uzaklığı hello ayarlayın: 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a>anchorDateTime örneği
Aşağıdaki örneğine hello hello dataset 23 saatte bir kez oluşturulur. Merhaba ilk dilim tarafından belirtilen başlangıç saati başlar **anchorDateTime**, ayarlanmış çok`2017-04-19T08:00:00` (UTC).

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a>uzaklık/stil örneği
Merhaba aşağıdaki veri kümesi olan aylık ve 8: 00'da her ayın 3 hello üzerinde üretilen (`3.08:00:00`):

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <a name="Policy"></a>Veri kümesi İlkesi
Merhaba **İlkesi** gerekir dataset dilimler hello hello koşulu karşılayan veya hello veri kümesi tanımı bölümünde hello ölçütleri tanımlar.

### <a name="validation-policies"></a>Doğrulama ilkeleri
| İlke adı | Açıklama | Çok uygulanan| Gerekli | Varsayılan |
| --- | --- | --- | --- | --- |
| minimumSizeMB |Merhaba verilerin doğrular **Azure Blob Depolama** karşılıyor hello minimum boyut gereksinimlerini (megabayt cinsinden). |Azure Blob depolama |Hayır |NA |
| minimumRows |Merhaba verilerin doğrulayan bir **Azure SQL veritabanı** veya bir **Azure tablo** hello en az satır sayısını içerir. |<ul><li>Azure SQL veritabanı</li><li>Azure tablo</li></ul> |Hayır |NA |

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

**minimumRows:**

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a>Dış veri kümeleri
Dış veri kümeleri hello hello veri fabrikası'nda çalışan bir ardışık düzen tarafından üretilmeyen olanları ' dir. Merhaba veri kümesi olarak işaretlenmişse **dış**, hello **ExternalData** ilkesi tanımlı tooinfluence hello hello dataset dilim kullanılabilirlik davranışını olabilir.

Bir veri kümesi Data Factory tarafından üretilen sürece bunu olarak işaretlenmelidir **dış**. Etkinlik veya ardışık düzen zincirleme kullanılmadığı sürece bu ayar genellikle ardışık düzendeki, ilk etkinliğin toohello girişleri uygulanır.

| Ad | Açıklama | Gerekli | Varsayılan değer |
| --- | --- | --- | --- |
| dataDelay |toodelay hello denetleyin hello için dış veri hello hello kullanılabilirliğine hello saat dilimi verilir. Örneğin, bu ayarı kullanarak bir saatlik onay geciktirebilir.<br/><br/>Merhaba ayar, yalnızca geçerli zaman toohello uygulanır.  Örneğin, 1:00 PM şimdi ise ve bu değer 10 dakikadır hello doğrulama 13: 10'te başlatır.<br/><br/>Bu ayar hello geçmiş dilimleri etkilemez unutmayın. İle dilimler **dilim bitiş saati** + **dataDelay** < **şimdi** herhangi bir gecikme işlenir.<br/><br/>23:59 büyük saatleri saat hello kullanarak belirtilmelidir `day.hours:minutes:seconds` biçimi. Örneğin, toospecify 24 saat 24:00:00 kullanmayın. Bunun yerine, 1.00:00:00 kullanın. 24:00:00 kullanırsanız, 24 gün (24.00:00:00) kabul edilir. 1 gün ve 4 saat için 1:04:00:00 belirtin. |Hayır |0 |
| Retryınterval |Merhaba hatası ve hello bir sonraki denemesi arasındaki süre bekleyin. Bu ayar toopresent zaman geçerlidir. Merhaba önceki deneme başarısız olursa hello sonraki deneyin sonra hello olan **Retryınterval** süresi. <br/><br/>1:00 PM şimdi ise, biz hello ilk denemede başlayın. Merhaba süresi toocomplete hello ilk doğrulama denetimi hello işlemi başarısız oldu ve 1 dakikalık hello sonraki yeniden deneme ise, 1:00 1 dak (süresi) + 1 dak (yeniden deneme aralığı) = 1:02 PM. <br/><br/>Merhaba son dilim için gecikme yoktur. Merhaba yeniden deneme hemen gerçekleşir. |Hayır |00:01:00 (1 dakika) |
| retryTimeout |yeniden deneme girişimleri için Hello zaman aşımı.<br/><br/>Bu özellik ayarlanırsa too10 dakika hello doğrulama 10 dakika içinde tamamlanması. 10 dakika tooperform hello doğrulama uzun sürerse hello zaman aşımına yeniden deneyin.<br/><br/>Tüm denemeleri hello doğrulama zaman aşımı için Merhaba, dilim olarak işaretlenmiş **süresi sona erdi**. |Hayır |00:10:00 (10 dakika) |
| maximumRetry |Merhaba sayısı toocheck hello dış veri hello kullanılabilirlik için zaman. değer izin verilen hello en fazla 10'dur. |Hayır |3 |


## <a name="create-datasets"></a>Veri kümeleri oluşturma
Bu araçlar ya da SDK'ları birini kullanarak veri kümeleri oluşturabilirsiniz: 

- Kopyalama Sihirbazı 
- Azure portalı
- Visual Studio
- PowerShell
- Azure Resource Manager şablonu
- REST API
- .NET API’si

Bu araçlar ya da SDK'ları birini kullanarak ardışık düzen ve veri kümeleri oluşturmak için öğreticileri adım adım yönergeler için aşağıdaki hello bakın:
 
- [Veri dönüştürme etkinliğine sahip işlem hattı oluşturma](data-factory-build-your-first-pipeline.md)
- [Veri taşıma etkinliği ile işlem hattı oluşturma](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

Ardışık düzenin oluşturulan ve dağıtılan sonra izlemek yönetmek ve Azure portal dikey penceresi veya hello izleme ve yönetim uygulaması kullanılarak işlem hatlarınızı hello. Merhaba aşağıdaki konularda adım adım yönergeler için bkz: 

- [İzleme ve Azure portal dikey penceresi kullanılarak işlem hatlarını yönetme](data-factory-monitor-manage-pipelines.md)
- [İzleme ve hello izleme ve yönetim uygulaması kullanılarak işlem hatlarını yönetme](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a>Kapsamlı veri kümeleri
Hello kullanarak kapsamlı tooa ardışık düzen olan veri kümeleri oluşturabilirsiniz **veri kümeleri** özelliği. Bu veri kümeleri yalnızca kullanılabilir etkinlikler içinde bu ardışık düzen tarafından diğer ardışık etkinlikler tarafından değil. Aşağıdaki örneğine hello içinde hello ardışık düzeni kullanılan iki veri kümesi (InputDataset rdc ve OutputDataset rdc) toobe ile işlem hattı tanımlar.  

> [!IMPORTANT]
> Kapsamlı veri kümeleri, yalnızca tek seferlik ardışık düzen ile desteklenir (burada **pipelineMode** çok ayarlanır**OneTime**). Bkz: [Onetime ardışık düzen](data-factory-create-pipelines.md#onetime-pipeline) Ayrıntılar için.
>
>

```json
{
    "name": "CopyPipeline-rdc",
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
                        "name": "InputDataset-rdc"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-rdc"
                    }
                ],
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1,
                    "style": "StartOfInterval"
                },
                "name": "CopyActivity-0"
            }
        ],
        "start": "2016-02-28T00:00:00Z",
        "end": "2016-02-28T00:00:00Z",
        "isPaused": false,
        "pipelineMode": "OneTime",
        "expirationTime": "15.00:00:00",
        "datasets": [
            {
                "name": "InputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "InputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/input",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": true,
                    "policy": {}
                }
            },
            {
                "name": "OutputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "OutputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/output",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": false,
                    "policy": {}
                }
            }
        ]
    }
}
```

## <a name="next-steps"></a>Sonraki adımlar
- Ardışık Düzen hakkında daha fazla bilgi için bkz: [oluşturma ardışık düzen](data-factory-create-pipelines.md). 
- Ardışık Düzen nasıl zamanlanmış ve yürütülen hakkında daha fazla bilgi için bkz: [zamanlama ve yürütme Azure Data factory'de](data-factory-scheduling-and-execution.md). 
