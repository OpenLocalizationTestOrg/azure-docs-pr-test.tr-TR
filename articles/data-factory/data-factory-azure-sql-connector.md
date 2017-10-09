---
title: "Azure SQL veritabanı/aaaCopy verileri | Microsoft Docs"
description: "Bilgi nasıl/Azure Data Factory kullanarak Azure SQL veritabanı toocopy verileri."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 484f735b-8464-40ba-a9fc-820e6553159e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: d2ff16191afb028da75699c5e4d0bb310538db0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-database-using-azure-data-factory"></a>Azure SQL Azure Data Factory kullanarak veritabanından veri tooand kopyalama
Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove veri tooand Azure SQL veritabanından de açıklanmaktadır. Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.  

## <a name="supported-scenarios"></a>Desteklenen senaryolar
Veri kopyalama **Azure SQL veritabanından** veri depolarına aşağıdaki toohello:

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

Veri depoları aşağıdaki hello verileri kopyalayabilirsiniz **tooAzure SQL veritabanı**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a>Desteklenen kimlik doğrulama türü
Azure SQL Veritabanı Bağlayıcısı temel kimlik doğrulamasını destekler.

## <a name="getting-started"></a>Başlarken
Farklı araçlar/API'lerini kullanarak bir Azure SQL veritabanından/gelen verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.

Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**. Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.

Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**. Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için. 

Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin: 

1. Oluşturma bir **veri fabrikası**. Veri Fabrikası bir veya daha fazla ardışık düzen içerebilir. 
2. Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası. Bir Azure blob depolama tooan Azure SQL veritabanından veri kopyalama, örneğin, iki bağlı hizmet toolink Azure depolama hesabınız ve Azure SQL veritabanı tooyour veri fabrikası oluşturun. Belirli tooAzure SQL veritabanı bağlantılı hizmet özellikler için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü. 
3. Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi. Merhaba son adımda bahsedilen hello örnekte, bir veri kümesi toospecify hello blob kapsayıcısı ve hello giriş verisi içeren klasörü oluşturun. Ve hello blob depolama biriminden kopyalanan hello verilerini tutan hello Azure SQL veritabanında başka bir veri kümesi toospecify hello SQL tablo oluşturun. Belirli tooAzure Data Lake Store dataset özellikler için bkz: [veri kümesi özellikleri](#dataset-properties) bölümü.
4. Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile. Daha önce bahsedilen hello örnekte BlobSource bir kaynak ve SqlSink havuzu olarak hello kopya etkinliği için kullanırsınız. Azure SQL veritabanı tooAzure Blob Depolama kopyalıyorsanız benzer şekilde, SqlSource ve BlobSink hello kopyalama etkinliği kullanırsınız. Belirli tooAzure SQL veritabanını kopyalama etkinliği özellikler için bkz: [kopyalama etkinliği özellikleri](#copy-activity-properties) bölümü. Nasıl toouse bir veri deposu bir kaynak veya bir havuz olarak hakkında daha fazla bilgi için veri deposu hello önceki bölümdeki hello bağlantısına tıklayın.

Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur. Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.  Bir Azure SQL veritabanı/kullanılan toocopy verileri olan Data Factory varlıkları için JSON tanımlarıyla örnekleri için bkz: [JSON örnekler](#json-examples-for-copying-data-to-and-from-sql-database) bu makalenin. 

Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooAzure SQL veritabanı olan JSON özellikleri hakkında ayrıntılı bilgi sağlar: 

## <a name="linked-service-properties"></a>Bağlantılı hizmet özellikleri
Bir Azure SQL hizmeti bir Azure SQL veritabanı tooyour data factory bağlantılı. Aşağıdaki tablonun hello JSON öğeleri belirli tooAzure SQL açıklamasını bağlantılı hizmetinin sağlar.

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| type |Merhaba type özelliği ayarlanmalıdır: **AzureSqlDatabase** |Evet |
| connectionString |Tooconnect toohello Azure SQL veritabanı örneğinde hello connectionString özelliği için gerekli bilgiler belirtin. Yalnızca temel kimlik doğrulama desteklenir. |Evet |

> [!IMPORTANT]
> Yapılandırma [Azure SQL veritabanı Güvenlik Duvarı](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) veritabanı sunucusu çok hello[Azure Hizmetleri tooaccess hello sunucusu izin](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure). Ayrıca, dış Azure veri fabrikası ağ geçidi ile şirket içi veri kaynaklarından dahil olmak üzere veri tooAzure SQL veritabanı kopyalıyorsanız, veri tooAzure SQL veritabanı gönderme hello makine için uygun IP adresi aralığı yapılandırın.

## <a name="dataset-properties"></a>Veri kümesi özellikleri
toospecify dataset toorepresent giriş veya çıkış verisi bir Azure SQL veritabanında hello türü özelliği için hello kümesinin ayarlayın: **AzureSqlTable**. Set hello **linkedServiceName** özelliği hello dataset toohello adının hello Azure SQL bağlı hizmeti.  

Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi. Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.

Merhaba typeProperties bölümü veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar. Merhaba **typeProperties** hello veri kümesi için bir bölüm türü **AzureSqlTable** hello aşağıdaki özelliklere sahiptir:

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| tableName |Merhaba tablo veya Görünüm hizmeti bağlı hello Azure SQL veritabanı örneğinde başvurduğu adı. |Evet |

## <a name="copy-activity-properties"></a>Etkinlik özellikleri Kopyala
Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi. Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.

> [!NOTE]
> Merhaba kopyalama etkinliği yalnızca bir girdi alır ve tek bir çıktı üretir.

Oysa hello kullanılabilen özellikleri **typeProperties** hello etkinlik bölümünü her etkinlik türü ile değişir. Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.

Bir Azure SQL veritabanından veri taşıyorsanız, hello kaynak türü hello kopyalama etkinliği çok ayarladığınız**SqlSource**. Veri tooan Azure SQL veritabanını taşıyorsanız, benzer şekilde, hello Havuz türü hello kopyalama etkinliği çok ayarladığınız**SqlSink**. Bu bölümde SqlSource ve SqlSink tarafından desteklenen özellikler listesini sağlar.

### <a name="sqlsource"></a>SqlSource
Kopyalama etkinliğinde hello kaynak türü olduğunda **SqlSource**, aşağıdaki özelliklere hello kullanılabilir **typeProperties** bölümü:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| sqlReaderQuery |Merhaba özel sorgu tooread verileri kullanın. |SQL sorgu dizesi. Örnek: `select * from MyTable`. |Hayır |
| sqlReaderStoredProcedureName |Merhaba adını hello kaynak tablodan veri okuyan yordamı depolanır. |Saklı yordam hello adı. Merhaba son SQL deyimi SELECT deyimi hello saklı yordam içinde olmalıdır. |Hayır |
| storedProcedureParameters |Saklı yordam hello için parametreler. |Ad/değer çiftleri. Adları ve büyük/küçük harf parametrelerinin hello adları ve büyük küçük harf kullanımını hello saklı yordam parametreleri eşleşmelidir. |Hayır |

Merhaba, **sqlReaderQuery** Merhaba SqlSource, hello kopyalama etkinliği çalıştıran bu sorguyu hello Azure SQL veritabanı kaynak tooget hello verileri karşı belirtilir. Alternatif olarak, bir saklı yordam hello belirterek belirleyebileceğiniz **sqlReaderStoredProcedureName** ve **storedProcedureParameters** (Merhaba saklı yordam parametreleri alır).

SqlReaderQuery veya sqlReaderStoredProcedureName belirtmezseniz, kullanılan toobuild bir sorgu hello yapısı bölümünde JSON hello kümesinin tanımlanan hello sütunlar: (`select column1, column2 from mytable`) hello Azure SQL veritabanına karşı toorun. Merhaba veri kümesi tanımı hello yapısına sahip değil, tüm sütunlar hello tablosundan seçilir.

> [!NOTE]
> Kullandığınızda, **sqlReaderStoredProcedureName**, hala toospecify bir değer hello için gereksinim duyduğunuz **tableName** JSON hello kümesindeki özelliği. Yine de bu tabloya karşı gerçekleştirilen başka doğrulama vardır.
>
>

### <a name="sqlsource-example"></a>SqlSource örneği

```JSON
"source": {
    "type": "SqlSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```

**Merhaba saklı yordamı tanımı:**

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqlsink"></a>SqlSink
**SqlSink** aşağıdaki özelliklere hello destekler:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| writeBatchTimeout |Zaman aşımına uğramadan önce hello toplu ekleme işlemi toocomplete bir süre bekleyin. |TimeSpan<br/><br/> Örnek: "00: 30:00" (30 dakika). |Hayır |
| writeBatchSize |Merhaba arabellek boyutu writeBatchSize ulaştığında veri hello SQL tablosuna ekler. |Tamsayı (satır sayısı) |Hayır (varsayılan: 10000) |
| sqlWriterCleanupScript |Belirli bir dilimle verilerinin temizlenmesini gibi bir sorgu için kopyalama etkinliği tooexecute belirtin. Daha fazla bilgi için bkz: [yinelenebilir kopyalama](#repeatable-copy). |Sorgu bildirimi. |Hayır |
| Sliceıdentifiercolumnname |Kopyalama etkinliği toofill bir sütun adı, ne zaman yeniden çalıştırılacağını belirli bir dilim verilerini kullanılan tooclean olduğu otomatik dilim tanımlayıcı ile belirtin. Daha fazla bilgi için bkz: [yinelenebilir kopyalama](#repeatable-copy). |Binary(32) veri türüne sahip bir sütunun sütun adı. |Hayır |
| sqlWriterStoredProcedureName |Merhaba adını upserts (güncelleştirmeler/ekler) verileri hello hedef tabloya saklı yordamı. |Saklı yordam hello adı. |Hayır |
| storedProcedureParameters |Saklı yordam hello için parametreler. |Ad/değer çiftleri. Adları ve büyük/küçük harf parametrelerinin hello adları ve büyük küçük harf kullanımını hello saklı yordam parametreleri eşleşmelidir. |Hayır |
| sqlWriterTableType |Merhaba saklı yordamda kullanılan bir tablo türü adı toobe belirtin. Kopyalama etkinliği taşınan hello veri geçici bir tablo bu tablo türü ile kullanılabilir hale getirir. Saklı yordam kodu sonra varolan verilerin kopyalanmasını hello verileri birleştirebilirsiniz. |Bir tablo türü adı. |Hayır |

#### <a name="sqlsink-example"></a>SqlSink örneği

```JSON
"sink": {
    "type": "SqlSink",
    "writeBatchSize": 1000000,
    "writeBatchTimeout": "00:05:00",
    "sqlWriterStoredProcedureName": "CopyTestStoredProcedureWithParameters",
    "sqlWriterTableType": "CopyTestTableType",
    "storedProcedureParameters": {
        "identifier": { "value": "1", "type": "Int" },
        "stringData": { "value": "str1" },
        "decimalData": { "value": "1", "type": "Decimal" }
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-sql-database"></a>SQL veritabanından veri tooand kopyalamak için JSON örnekleri
Merhaba aşağıdaki örneklerde sağlayan örnek JSON tanımları toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Bunlar Göster nasıl toocopy veri tooand Azure SQL Database ve Azure Blob depolama alanından. Ancak, veriler kopyalanabilir **doğrudan** herhangi birinden belirtildiği hello havuzlarını, kaynakları tooany [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.

### <a name="example-copy-data-from-azure-sql-database-tooazure-blob"></a>Örnek: Verilerini Azure SQL veritabanı tooAzure Blob
Merhaba aynı Data Factory varlıklarını aşağıdaki hello tanımlar:

1. Bağlı hizmet türü [AzureSqlDatabase](#linked-service-properties).
2. Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureSqlTable](#dataset-properties).
4. Bir çıkış [dataset](data-factory-create-datasets.md) türü [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).
5. A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [SqlSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Merhaba örnek time series verilerini (saatlik, günlük, vb.) Azure SQL veritabanı tooa blob tablosunda her saat kopyalar. Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.  

**Azure SQL Database hizmeti bağlı:**

```JSON
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
Merhaba bkz [Azure SQL bağlı hizmeti](#linked-service) hello listesi için bu bağlantılı hizmet tarafından desteklenen özellikler bölümü.

**Azure Blob storage bağlı hizmeti:**

```JSON
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
Merhaba bkz [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) bu bağlantılı hizmet tarafından desteklenen özellikler hello listesi için makale.


**Azure SQL girdi veri kümesi:**

Merhaba örnek "MyTable" Azure SQL tablosu oluşturdunuz ve zaman serisi veri için "timestampcolumn" adlı bir sütun içerdiği varsayar.

"Dış" ayarı: "true" bildirir hello Azure Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.

```JSON
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

Merhaba bkz [Azure SQL veri kümesi türü özellikleri](#dataset) hello listesi için bu veri kümesi türü tarafından desteklenen özellikler bölümü.  

**Azure Blob dataset çıktı:**

Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1). hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir. Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
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
Merhaba bkz [Azure Blob veri kümesi türü özellikleri](data-factory-azure-blob-connector.md#dataset-properties) hello listesi için bu veri kümesi türü tarafından desteklenen özellikler bölümü.  

**SQL kaynak ve Blob havuz sahip işlem hattı kopyalama etkinliğinde:**

Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**SqlSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**. Merhaba belirtilen hello SQL sorgusu **SqlReaderQuery** özelliği saat toocopy geçmiş hello hello veri seçer.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoBlob",
        "description": "copy activity",
        "type": "Copy",
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
Merhaba örnekte **sqlReaderQuery** SqlSource hello için belirtilir. Merhaba kopyalama etkinliği hello Azure SQL veritabanı kaynak tooget hello verilerine karşı bu sorguyu çalıştırır. Alternatif olarak, bir saklı yordam hello belirterek belirleyebileceğiniz **sqlReaderStoredProcedureName** ve **storedProcedureParameters** (Merhaba saklı yordam parametreleri alır).

SqlReaderQuery veya sqlReaderStoredProcedureName belirtmezseniz hello yapısı bölümünde JSON hello kümesinin tanımlanan hello sütunlar kullanılan toobuild hello Azure SQL veritabanına karşı sorgu toorun'dır. Örneğin: `select column1, column2 from mytable`. Merhaba veri kümesi tanımı hello yapısına sahip değil, tüm sütunlar hello tablosundan seçilir.

Hello bkz [Sql kaynağı](#sqlsource) bölüm ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) SqlSource ve BlobSink tarafından desteklenen özellikler hello listesi.

### <a name="example-copy-data-from-azure-blob-tooazure-sql-database"></a>Örnek: Kopyalama verileri Azure Blob tooAzure SQL veritabanı
Merhaba örnek Data Factory varlıklarını aşağıdaki hello tanımlar:  

1. Bağlı hizmet türü [AzureSqlDatabase](#linked-service-properties).
2. Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureSqlTable](#dataset-properties).
5. A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) ve [SqlSink](#copy-activity-properties).

Merhaba örnek time series verilerini (saatlik, günlük, vb.) Azure blob tooa Azure SQL veritabanı tablosunda her saat kopyalar. Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.

**Azure SQL bağlı hizmeti:**

```JSON
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
Merhaba bkz [Azure SQL bağlı hizmeti](#linked-service) hello listesi için bu bağlantılı hizmet tarafından desteklenen özellikler bölümü.

**Azure Blob storage bağlı hizmeti:**

```JSON
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
Merhaba bkz [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) bu bağlantılı hizmet tarafından desteklenen özellikler hello listesi için makale.


**Azure Blob girdi veri kümesi:**

Veri toplanma yeni blob üzerinden saatte (sıklığı: saat, aralığı: 1). Merhaba klasör yolu ve dosya adını hello blob dinamik olarak değerlendirilir işleniyor hello dilimin hello başlangıç zamanı temel alınarak. Merhaba klasör yolu yıl, ay ve gün kısmını hello başlangıç saati ve dosya adı hello başlangıç saati hello saat bölümünü kullanır. "dış": "true" ayarı bu tablosu dış toohello veri fabrikası ve hello veri fabrikasında bir etkinlik tarafından üretilen değil hello Data Factory hizmetinin sizi bilgilendirir.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
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
Merhaba bkz [Azure Blob veri kümesi türü özellikleri](data-factory-azure-blob-connector.md#dataset-properties) hello listesi için bu veri kümesi türü tarafından desteklenen özellikler bölümü.

**Azure SQL veritabanı veri kümesini çıktı:**

Merhaba örnek Azure SQL "MyTable" olarak adlandırılan veri tooa tablosuna kopyalar. Azure SQL ile Merhaba tablo oluşturmak hello Blob CSV dosyası toocontain beklediğiniz gibi hello aynı sayıda sütun. Yeni satırlar toohello tablo saatte eklenir.

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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
Merhaba bkz [Azure SQL veri kümesi türü özellikleri](#dataset) hello listesi için bu veri kümesi türü tarafından desteklenen özellikler bölümü.

**Blob kaynağı ve SQL havuz sahip işlem hattı kopyalama etkinliğinde:**

Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**BlobSource** ve **havuz** türü olarak ayarlanmış çok**SqlSink**.

```JSON
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
            "name": "AzureSqlOutput"
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
Hello bkz [Sql havuz](#sqlsink) bölüm ve [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) SqlSink ve BlobSource tarafından desteklenen özellikler hello listesi.

## <a name="identity-columns-in-hello-target-database"></a>Merhaba hedef veritabanında kimlik sütunu
Bu bölümde, bir kimlik sütunu tooa hedef tabloyla bir kimlik sütunu olmayan bir kaynak tablodan veri kopyalamak için bir örnek sağlar.

**Kaynak tablosu:**

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
**Hedef Tablo:**

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
Merhaba hedef tablosunun bir kimlik sütunu olan dikkat edin.

**Kaynak veri kümesi JSON tanımı**

```JSON
{
    "name": "SampleSource",
    "properties": {
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

```JSON
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
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
Kopyalama etkinliği ardışık SQL havuzunda bir saklı yordam çağırma bir örnek için bkz: [kopyalama etkinliği SQL havuz için saklı yordam çağırma](data-factory-invoke-stored-procedure-from-copy-activity.md) makalesi. 

## <a name="type-mapping-for-azure-sql-database"></a>Tür eşlemesi için Azure SQL veritabanı
Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale kopyalama etkinliği ile 2 adımlı yaklaşımı izleyerek hello kaynak türleri toosink türlerinden otomatik tür dönüşümleri gerçekleştirir:

1. Yerel kaynak türleri too.NET türünden Dönüştür
2. .NET türü toonative havuz türünden Dönüştür

Azure SQL veritabanından veri tooand taşırken, hello aşağıdaki eşlemelerini too.NET türü ve bunun tersi de kullanılır. Merhaba eşleme hello ADO.NET için SQL Server veri türü eşlemesi olarak aynıdır.

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

## <a name="map-source-toosink-columns"></a>Kaynak toosink sütunları eşleme
Kaynak veri kümesi toocolumns havuz kümesindeki eşleme sütunlarında hakkında toolearn bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).

## <a name="repeatable-copy"></a>Yinelenebilir kopyalama
Veri tooSQL sunucu veritabanı kopyalama işlemi sırasında hello kopyalama etkinliği varsayılan olarak veri toohello havuz tablosuna ekler. Bunun yerine, tooperform bir UPSERT bkz [yinelenebilir yazma tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) makalesi. 

İlişkisel veri depoları veri kopyalama işlemi sırasında Yinelenebilirlik göz tooavoid tutmak istenmeyen sonuçları. Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz. Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz. Bir dilim iki yolla yeniden zaman, aynı veri hello emin toomake nasıl geçtiğinden bağımsız okuma gerekir dilim birçok kez çalıştırın. Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Performans ve ayarlama
Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.
