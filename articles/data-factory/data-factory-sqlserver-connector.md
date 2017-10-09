---
title: SQL Server'dan aaaMove veri tooand | Microsoft Docs
description: "Azure Data Factory kullanarak Azure VM'deki veya nasıl/SQL Server toomove verileri şirket içi yani veritabanı hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 864ece28-93b5-4309-9873-b095bbe6fedd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jingwang
ms.openlocfilehash: f0cccf56a670e62ec893d75052a81eb26d562050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a>Azure Data Factory kullanarak veri tooand şirket içi SQL Server veya Iaas (Azure VM) üzerinde taşıma
Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove için/şirket içi SQL Server veritabanındaki verileri de açıklanmaktadır. Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar. 

## <a name="supported-scenarios"></a>Desteklenen senaryolar
Veri kopyalama **bir SQL Server veritabanından** veri depolarına aşağıdaki toohello:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Veri depoları aşağıdaki hello verileri kopyalayabilirsiniz **tooa SQL Server veritabanı**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a>Desteklenen SQL Server sürümleri
Verileri kopyalama bu SQL Server bağlayıcı desteği / toohello aşağıdaki sürümler barındırılan örneği şirket içi veya Azure SQL kimlik doğrulaması ve Windows kimlik doğrulaması kullanarak Iaas: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005

## <a name="enabling-connectivity"></a>Bağlantıyı etkinleştirme
Merhaba kavramlar ve SQL Server barındırılan şirket içi veya Azure Iaas VM'ler (altyapı-bir hizmet olarak) bağlanmak için gereken adımlar şunlardır hello aynı. Her iki durumda da toouse veri yönetimi ağ geçidi bağlantısı için gereklidir.

Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale toolearn veri yönetimi ağ geçidi ve hello ağ geçidi kurun ayarlama hakkında adım adım yönergeleri hakkında. Bir ağ geçidi örneği SQL Server ile bağlanmak için bir önkoşul ayardır.

Ağ geçidi yüklenirken hello üzerinde aynı makine veya Bulut VM örneği daha iyi performans için SQL Server hello gibi şirket içi, bunları farklı makinelere yüklemeniz önerilir. Merhaba ağ geçidi ve SQL Server ayrı makinelerde sahip kaynak çekişmesini azaltır.

## <a name="getting-started"></a>Başlarken
Farklı araçlar/API'lerini kullanarak bir şirket içi SQL Server veritabanından/gelen verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.

Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**. Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.

Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**. Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için. 

Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin: 

1. Oluşturma bir **veri fabrikası**. Veri Fabrikası bir veya daha fazla ardışık düzen içerebilir. 
2. Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası. Bir SQL Server veritabanı tooan Azure blob depolama veri kopyalama, örneğin, iki bağlı hizmet toolink SQL Server veritabanı ve Azure depolama hesabı tooyour veri fabrikası oluşturun. Belirli tooSQL Server veritabanına bağlı hizmet özellikler için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü. 
3. Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi. Merhaba son adımda bahsedilen hello örnekte, SQL Server veritabanınız hello giriş verileri içeren bir veri kümesi toospecify hello SQL tablo oluşturun. Başka bir veri kümesi toospecify hello blob kapsayıcı oluşturun ve hello verilerini tutan hello klasörü hello SQL Server veritabanı kopyalanır. Belirli tooSQL Server veritabanı veri kümesi özellikleri için bkz: [veri kümesi özellikleri](#dataset-properties) bölümü.
4. Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile. Daha önce bahsedilen hello örnekte SqlSource bir kaynak ve BlobSink havuzu olarak hello kopya etkinliği için kullanırsınız. Azure Blob Storage tooSQL sunucu veritabanı kopyalıyorsanız benzer şekilde, BlobSource ve SqlSink hello kopyalama etkinliği kullanırsınız. Belirli tooSQL sunucu veritabanı kopyalama etkinliği özellikler için bkz: [kopyalama etkinliği özellikleri](#copy-activity-properties) bölümü. Nasıl toouse bir veri deposu bir kaynak veya bir havuz olarak hakkında daha fazla bilgi için veri deposu hello önceki bölümdeki hello bağlantısına tıklayın. 

Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur. Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.  Bir şirket içi SQL Server veritabanı/kullanılan toocopy verileri olan Data Factory varlıkları için JSON tanımlarıyla örnekleri için bkz: [JSON örnekler](#json-examples-for-copying-data-from-and-to-sql-server) bu makalenin. 

Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooSQL sunucu olan JSON özellikleri hakkında ayrıntılı bilgi sağlar: 

## <a name="linked-service-properties"></a>Bağlantılı hizmet özellikleri
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

### <a name="samples"></a>Örnekler
**SQL kimlik doğrulaması kullanarak JSON**

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties":
    {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
**Windows kimlik doğrulaması kullanmak için JSON**

Veri Yönetimi ağ geçidi kimliğine bürünmek hello belirtilen kullanıcı hesabı tooconnect toohello şirket içi SQL Server veritabanı. 

```json
{
     "Name": " MyOnPremisesSQLDB",
     "Properties":
     {
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

## <a name="dataset-properties"></a>Veri kümesi özellikleri
Bir veri türünde kullanılan Hello örneklerinde **SqlServerTable** toorepresent bir SQL Server veritabanındaki bir tablo.  

Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi. Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (SQL Server, Azure blob, Azure tablo, vs.) için benzer.

Merhaba typeProperties bölümü veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar. Merhaba **typeProperties** hello veri kümesi için bir bölüm türü **SqlServerTable** hello aşağıdaki özelliklere sahiptir:

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| tableName |Merhaba tablo veya Görünüm hizmeti bağlı hello SQL Server veritabanı örneğinde başvurduğu adı. |Evet |

## <a name="copy-activity-properties"></a>Etkinlik özellikleri Kopyala
Bir SQL Server veritabanından veri taşıyorsanız, hello kaynak türü hello kopyalama etkinliği çok ayarladığınız**SqlSource**. Veri tooa SQL Server veritabanını taşıyorsanız, benzer şekilde, hello Havuz türü hello kopyalama etkinliği çok ayarladığınız**SqlSink**. Bu bölümde SqlSource ve SqlSink tarafından desteklenen özellikler listesini sağlar.

Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi. Ad, açıklama, giriş ve çıkış tabloları ve ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir.

> [!NOTE]
> Merhaba kopyalama etkinliği yalnızca bir girdi alır ve tek bir çıktı üretir.

Oysa hello typeProperties bölümünde hello etkinlik özellikleri her etkinlik türü ile farklılık gösterir. Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.

### <a name="sqlsource"></a>SqlSource
Kopyalama etkinliği kaynağında türü olduğunda **SqlSource**, aşağıdaki özelliklere hello kullanılabilir **typeProperties** bölümü:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| sqlReaderQuery |Merhaba özel sorgu tooread verileri kullanın. |SQL sorgu dizesi. Örneğin: seçin * from MyTable. Birden çok tablo hello girdi veri kümesi tarafından başvurulan hello veritabanından başvurabilir. Belirtilmezse, yürütülen SQL deyimini hello: MyTable arasından seçin. |Hayır |
| sqlReaderStoredProcedureName |Merhaba adını hello kaynak tablodan veri okuyan yordamı depolanır. |Saklı yordam hello adı. Merhaba son SQL deyimi SELECT deyimi hello saklı yordam içinde olmalıdır. |Hayır |
| storedProcedureParameters |Saklı yordam hello için parametreler. |Ad/değer çiftleri. Adları ve büyük/küçük harf parametrelerinin hello adları ve büyük küçük harf kullanımını hello saklı yordam parametreleri eşleşmelidir. |Hayır |

Merhaba, **sqlReaderQuery** Merhaba SqlSource, hello kopyalama etkinliği çalıştıran bu sorguyu hello SQL Server veritabanı kaynak tooget hello verileri karşı belirtilir.

Alternatif olarak, bir saklı yordam hello belirterek belirleyebileceğiniz **sqlReaderStoredProcedureName** ve **storedProcedureParameters** (Merhaba saklı yordam parametreleri alır).

SqlReaderQuery veya sqlReaderStoredProcedureName belirtmezseniz hello yapısı bölümünde tanımlanan hello sütunlar kullanılan toobuild seçme sorgusu toorun hello SQL Server veritabanına karşı'dır. Merhaba veri kümesi tanımı hello yapısına sahip değil, tüm sütunlar hello tablosundan seçilir.

> [!NOTE]
> Kullandığınızda, **sqlReaderStoredProcedureName**, hala toospecify bir değer hello için gereksinim duyduğunuz **tableName** JSON hello kümesindeki özelliği. Yine de bu tabloya karşı gerçekleştirilen başka doğrulama vardır.

### <a name="sqlsink"></a>SqlSink
**SqlSink** aşağıdaki özelliklere hello destekler:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| writeBatchTimeout |Zaman aşımına uğramadan önce hello toplu ekleme işlemi toocomplete bir süre bekleyin. |TimeSpan<br/><br/> Örnek: "00: 30:00" (30 dakika). |Hayır |
| writeBatchSize |Merhaba arabellek boyutu writeBatchSize ulaştığında veri hello SQL tablosuna ekler. |Tamsayı (satır sayısı) |Hayır (varsayılan: 10000) |
| sqlWriterCleanupScript |Belirli bir dilimle verilerinin temizlenmesini gibi kopyalama etkinliği tooexecute için sorgu belirtin. Daha fazla bilgi için bkz: [yinelenebilir kopyalama](#repeatable-copy) bölümü. |Sorgu bildirimi. |Hayır |
| Sliceıdentifiercolumnname |Kopyalama etkinliği toofill sütun adı, ne zaman yeniden çalıştırılacağını belirli bir dilim verilerini kullanılan tooclean olduğu otomatik dilim tanımlayıcı ile belirtin. Daha fazla bilgi için bkz: [yinelenebilir kopyalama](#repeatable-copy) bölümü. |Binary(32) veri türüne sahip bir sütunun sütun adı. |Hayır |
| sqlWriterStoredProcedureName |Merhaba adını upserts (güncelleştirmeler/ekler) verileri hello hedef tabloya saklı yordamı. |Saklı yordam hello adı. |Hayır |
| storedProcedureParameters |Saklı yordam hello için parametreler. |Ad/değer çiftleri. Adları ve büyük/küçük harf parametrelerinin hello adları ve büyük küçük harf kullanımını hello saklı yordam parametreleri eşleşmelidir. |Hayır |
| sqlWriterTableType |Merhaba saklı yordamda kullanılan tablo türü adı toobe belirtin. Kopyalama etkinliği taşınan hello veri geçici bir tablo bu tablo türü ile kullanılabilir hale getirir. Saklı yordam kodu sonra varolan verilerin kopyalanmasını hello verileri birleştirebilirsiniz. |Bir tablo türü adı. |Hayır |


## <a name="json-examples-for-copying-data-from-and-toosql-server"></a>Verileri ve tooSQL sunucu kopyalamak için JSON örnekleri
Merhaba aşağıdaki örneklerde sağlayan örnek JSON tanımları toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Örnekleri göster nasıl aşağıdaki hello toocopy veri tooand SQL Server ve Azure Blob Storage. Ancak, veriler kopyalanabilir **doğrudan** herhangi birinden belirtildiği hello havuzlarını, kaynakları tooany [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.     

## <a name="example-copy-data-from-sql-server-tooazure-blob"></a>Örnek: Verilerini SQL Server tooAzure Blob
Merhaba, aşağıdaki örnek gösterilmektedir:

1. Bağlı hizmet türü [OnPremisesSqlServer](#linked-service-properties).
2. Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Bir giriş [dataset](data-factory-create-datasets.md) türü [SqlServerTable](#dataset-properties).
4. Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Merhaba [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [SqlSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Merhaba örnek time series verilerini bir SQL Server tablo tooan Azure blob saatte kopyalar. Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.

İlk adım olarak, hello veri yönetimi ağ geçidi ayarlayın. Merhaba yönergelerdir hello [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.

**SQL Server bağlantılı hizmeti**
```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
**Azure Blob storage bağlı hizmeti**

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
**SQL Server girdi veri kümesi**

Merhaba örnek SQL Server'da bir tablo "MyTable" oluşturulur ve zaman serisi veri için "timestampcolumn" adlı bir sütun içerdiği varsayar. Tek bir veri kümesi, ancak tek bir tabloyu kullanarak aynı veritabanı hello veri kümesi'nin tableName typeProperty için kullanılması gereken hello içinde birden çok tablo üzerinde sorgulayabilirsiniz.

"Dış" ayarı: "true" bildirir Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.

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
**Azure Blob dataset çıktı**

Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1). hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir. Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
**Kopyalama etkinliği ile kanalı**

Merhaba ardışık düzen içeren bir kopyalama etkinliği, yapılandırılmış toouse bu girdi ve çıktı veri kümeleri ve zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**SqlSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**. Merhaba belirtilen hello SQL sorgusu **SqlReaderQuery** özelliği saat toocopy geçmiş hello hello veri seçer.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2016-06-01T18:00:00",
    "end":"2016-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
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
      }
     ]
   }
}
```
Bu örnekte, **sqlReaderQuery** SqlSource hello için belirtilir. Merhaba kopyalama etkinliği bu sorguyu SQL Server veritabanı kaynak tooget hello verileri hello karşı çalışır. Alternatif olarak, bir saklı yordam hello belirterek belirleyebileceğiniz **sqlReaderStoredProcedureName** ve **storedProcedureParameters** (Merhaba saklı yordam parametreleri alır). Merhaba sqlReaderQuery hello girdi veri kümesi tarafından başvurulan hello veritabanı içinde birden çok tablo başvuruda bulunabilir. Bu veri kümesi'nin tableName typeProperty hello olarak ayarlanmış sınırlı tooonly hello tablosu değil.

SqlReaderQuery veya sqlReaderStoredProcedureName belirtmezseniz hello yapısı bölümünde tanımlanan hello sütunlar kullanılan toobuild seçme sorgusu toorun hello SQL Server veritabanına karşı'dır. Merhaba veri kümesi tanımı hello yapısına sahip değil, tüm sütunlar hello tablosundan seçilir.

Hello bkz [Sql kaynağı](#sqlsource) bölüm ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) SqlSource ve BlobSink tarafından desteklenen özellikler hello listesi.

## <a name="example-copy-data-from-azure-blob-toosql-server"></a>Örnek: Kopyalama verileri Azure Blob tooSQL sunucu
Merhaba, aşağıdaki örnek gösterilmektedir:

1. Merhaba bağlantılı hizmet türü [OnPremisesSqlServer](#linked-service-properties).
2. Merhaba bağlantılı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Bir çıkış [dataset](data-factory-create-datasets.md) türü [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).
5. Merhaba [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) ve [SqlSink](#sql-server-copy-activity-type-properties).

Merhaba örnek time series verilerini her saat bir Azure blob tooa SQL Server tablosundan kopyalar. Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.

**SQL Server bağlantılı hizmeti**

```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
**Azure Blob storage bağlı hizmeti**

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
**Azure Blob girdi veri kümesi**

Veri toplanma yeni blob üzerinden saatte (sıklığı: saat, aralığı: 1). Merhaba klasör yolu ve dosya adını hello blob dinamik olarak değerlendirilir işleniyor hello dilimin hello başlangıç zamanı temel alınarak. Merhaba klasör yolu yıl, ay ve gün kısmını hello başlangıç saati ve dosya adı hello başlangıç saati hello saat bölümünü kullanır. "dış": "true" ayarı bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil hello Data Factory hizmetinin sizi bilgilendirir.

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
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
**SQL Server çıktı veri kümesi**

Merhaba örnek SQL Server'da "MyTable" olarak adlandırılan veri tooa tablosuna kopyalar. SQL Server ile Merhaba tablosunu oluşturan hello Blob CSV dosyası toocontain beklediğiniz gibi hello aynı sayıda sütun. Yeni satırlar toohello tablo saatte eklenir.

```json
{
  "name": "SqlServerOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
**Kopyalama etkinliği ile kanalı**

Merhaba ardışık düzen içeren bir kopyalama etkinliği, yapılandırılmış toouse bu girdi ve çıktı veri kümeleri ve zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**BlobSource** ve **havuz** türü olarak ayarlanmış çok**SqlSink**.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": " SqlServerOutput "
          }
        ],
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
      }
      ]
   }
}
```

## <a name="troubleshooting-connection-issues"></a>Bağlantı sorunlarını giderme
1. SQL Server tooaccept uzak bağlantıları yapılandırın. Başlatma **SQL Server Management Studio**, sağ **server**, tıklatıp **özellikleri**. Seçin **bağlantıları** hello listesi ve onay **izin uzak bağlantıları toohello sunucu**.

    ![Uzak bağlantıları etkinleştir](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    Bkz: [hello uzaktan erişim sunucu yapılandırma seçeneğini yapılandırma](https://msdn.microsoft.com/library/ms191464.aspx) ayrıntılı adımlar için.
2. Başlatma **SQL Server Configuration Manager**. Genişletme **SQL Server Ağ Yapılandırması** Merhaba istediğiniz ' nı seçip örnek **MSSQLSERVER protokolleri**. Protokolleri hello sağ bölmesinde görmeniz gerekir. Sağ tıklayarak TCP/IP'yi etkinleştirin **TCP/IP'yi** tıklatıp **etkinleştirmek**.

    ![TCP/IP'yi etkinleştirin](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    Bkz: [etkinleştirmek veya devre dışı bir sunucu ağ protokolü](https://msdn.microsoft.com/library/ms191294.aspx) ayrıntı ve TCP/IP protokolünün etkinleştirilmesi alternatif yolu.
3. Buna Merhaba aynı penceresi, çift **TCP/IP'yi** toolaunch **TCP/IP özelliklerini** penceresi.
4. Geçiş toohello **IP adreslerini** sekmesi. Toosee aşağı **IPAll** bölümü. Merhaba Not ** TCP bağlantı noktası ** (varsayılan değer **1433**).
5. Oluşturma bir **hello Windows Güvenlik Duvarı Kuralı** hello makine tooallow Bu bağlantı noktası üzerinden gelen trafiği üzerinde.  
6. **Bağlantıyı doğrulama**: tooconnect toohello tam adını kullanarak SQL Server başka bir makineden SQL Server Management Studio kullanın. Örneğin: "<machine>.<domain>. Corp.<company>.com, 1433. "

   > [!IMPORTANT]

   > Bkz: [şirket içi kaynakları ve veri yönetimi ağ geçidi ile Merhaba bulut arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) ayrıntılı bilgi için.
   >
   > Bkz: [ağ geçidi sorunlarını giderme](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) ilgili sorunlar bağlantı/ağ geçidi sorun giderme ipuçları için.
   >
   >


## <a name="identity-columns-in-hello-target-database"></a>Merhaba hedef veritabanında kimlik sütunu
Bu bölümde bir kimlik sütunu sahip bir kimlik sütunu tooa hedef tablo içeren bir kaynak tablo verileri kopyalar bir örnek sağlar.

**Kaynak tablosu:**

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
**Hedef Tablo:**

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

Merhaba hedef tablosunun bir kimlik sütunu olan dikkat edin.

**Kaynak veri kümesi JSON tanımı**

```json
{
    "name": "SampleSource",
    "properties": {
        "published": false,
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
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
**Hedef veri kümesi JSON tanımı**

```json
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

Kaynak ve hedef tablosu farklı şema sahip dikkat edin (hedef kimliğine sahip başka bir sütuna sahip). Bu senaryoda, toospecify gerek **yapısı** hello kimlik sütunu içermeyen hello hedef veri kümesi tanımında özelliği.

## <a name="invoke-stored-procedure-from-sql-sink"></a>SQL havuz depolanan yordamı çağırma
Bkz: [kopyalama etkinliği SQL havuz için saklı yordam çağırma](data-factory-invoke-stored-procedure-from-copy-activity.md) makale SQL havuz ardışık kopyalama etkinliğinde bir saklı yordam çağırma örneği.

## <a name="type-mapping-for-sql-server"></a>Tür eşlemesi için SQL server
Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, hello kopyalama etkinliği gerçekleştiren kaynak türleri toosink türlerinden otomatik tür dönüşümleri 2 adımlı yaklaşımı izleyerek hello ile:

1. Yerel kaynak türleri too.NET türünden Dönüştür
2. .NET türü toonative havuz türünden Dönüştür

Çok & SQL Server'dan veri taşımayı hello olduğunda aşağıdaki eşlemelerini too.NET türü ve bunun tersi de kullanılır.

Merhaba eşleme hello ADO.NET için SQL Server veri türü eşlemesi olarak aynıdır.

| SQL Server veritabanı altyapısı türü | .NET framework türü |
| --- | --- |
| bigint |Int64 |
| İkili |Byte] |
| bit |Boole değeri |
| char |Dize, Char] |
| Tarih |Tarih saat |
| Tarih saat |Tarih saat |
| datetime2 |Tarih saat |
| Datetimeoffset |DateTimeOffset |
| Ondalık |Ondalık |
| FILESTREAM özniteliği (varbinary(max)) |Byte] |
| Kayan nokta |Çift |
| Görüntü |Byte] |
| Int |Int32 |
| para |Ondalık |
| nchar |Dize, Char] |
| ntext |Dize, Char] |
| sayısal |Ondalık |
| nvarchar |Dize, Char] |
| Gerçek |Tek |
| rowVersion |Byte] |
| smalldatetime |Tarih saat |
| tamsayı |Int16 |
| küçük para |Ondalık |
| sql_variant |Nesne * |
| Metin |Dize, Char] |
| time |TimeSpan |
| timestamp |Byte] |
| Mini tamsayı |Bayt |
| benzersiz tanımlayıcı |GUID |
| varbinary |Byte] |
| varchar |Dize, Char] |
| xml |XML |

## <a name="mapping-source-toosink-columns"></a>Kaynak toosink sütunları eşleme
Kaynak veri kümesi toocolumns havuz kümesinden toomap sütunlarından bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).

## <a name="repeatable-copy"></a>Yinelenebilir kopyalama
Veri tooSQL sunucu veritabanı kopyalama işlemi sırasında hello kopyalama etkinliği varsayılan olarak veri toohello havuz tablosuna ekler. Bunun yerine, tooperform bir UPSERT bkz [yinelenebilir yazma tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) makalesi. 

İlişkisel veri depoları veri kopyalama işlemi sırasında Yinelenebilirlik göz tooavoid tutmak istenmeyen sonuçları. Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz. Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz. Bir dilim iki yolla yeniden zaman, aynı veri hello emin toomake nasıl geçtiğinden bağımsız okuma gerekir dilim birçok kez çalıştırın. Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Performans ve ayarlama
Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.
