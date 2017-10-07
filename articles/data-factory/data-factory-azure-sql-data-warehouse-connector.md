---
title: Azure SQL Data Warehouse/aaaCopy verileri | Microsoft Docs
description: "Bilgi nasıl/Azure Data Factory kullanarak Azure SQL Data Warehouse toocopy verileri"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: d90fa9bd-4b79-458a-8d40-e896835cfd4a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 75bfcf3c99844fc1297ca500107da23cf875e41f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-data-warehouse-using-azure-data-factory"></a>Azure Data Factory kullanarak Azure SQL veri ambarından veri tooand Kopyala
Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove veri öğesine/öğesinden Azure SQL Data Warehouse açıklanmaktadır. Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.  

> [!TIP]
> tooachieve en iyi performans için Azure SQL Data Warehouse'a PolyBase tooload verileri kullanın. Merhaba [kullanım PolyBase tooload verilerin Azure SQL veri ambarında](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) bölümde ayrıntılar bulunur. Kullanım örneği ile bir anlatım için bkz: [1 TB altında 15 dakika Azure Data Factory ile Azure SQL Data Warehouse'a veri yükleme](data-factory-load-sql-data-warehouse.md).

## <a name="supported-scenarios"></a>Desteklenen senaryolar
Veri kopyalama **Azure SQL veri ambarından** veri depolarına aşağıdaki toohello:

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

Veri depoları aşağıdaki hello verileri kopyalayabilirsiniz **tooAzure SQL Data Warehouse**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> SQL Server veya Azure SQL Database tooAzure veri kopyalama işlemi sırasında SQL Data Warehouse hello tablo hello hedef depo, veri fabrikası yoksa, otomatik olarak hello tablo SQL veri ambarı'nda hello kaynağında Merhaba tablonun hello şeması kullanarak oluşturabilirsiniz veri deposu. Bkz: [Otomatik Tablo oluşturma](#auto-table-creation) Ayrıntılar için.

## <a name="supported-authentication-type"></a>Desteklenen kimlik doğrulama türü
Azure SQL Data Warehouse Bağlayıcısı destek temel kimlik doğrulaması.

## <a name="getting-started"></a>Başlarken
Verileri farklı araçlar/API'lerini kullanarak Azure SQL Data Warehouse denetleyicisinden taşır kopyalama etkinliği ile işlem hattı oluşturun.

Merhaba en kolay yolu toocreate öğesine/öğesinden Azure SQL veri ambarı verileri kopyalayan bir işlem hattı toouse hello kopya veri sihirbazıdır. Bkz: [öğretici: Data Factory ile SQL veri ambarına veri yükleme](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.

Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**. Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.

Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:

1. Oluşturma bir **veri fabrikası**. Veri Fabrikası bir veya daha fazla ardışık düzen içerebilir. 
2. Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası. Bir Azure blob depolama tooan Azure SQL veri ambarından veri kopyalama, örneğin, iki bağlı hizmet toolink Azure depolama hesabınız ve Azure SQL veri ambarı tooyour veri fabrikası oluşturun. Belirli tooAzure SQL Data Warehouse bağlantılı hizmet özellikler için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü. 
3. Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi. Merhaba son adımda bahsedilen hello örnekte, bir veri kümesi toospecify hello blob kapsayıcısı ve hello giriş verisi içeren klasörü oluşturun. Ve hello blob depolama biriminden kopyalanan hello verilerini tutan Azure SQL veri ambarı hello başka bir veri kümesi toospecify hello tablo oluşturun. Belirli tooAzure SQL veri ambarı veri kümesi özellikler için bkz: [veri kümesi özellikleri](#dataset-properties) bölümü.
4. Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile. Daha önce bahsedilen hello örnekte BlobSource bir kaynak ve SqlDWSink havuzu olarak hello kopya etkinliği için kullanırsınız. Azure SQL Data Warehouse tooAzure Blob Depolama kopyalıyorsanız benzer şekilde, SqlDWSource ve BlobSink hello kopyalama etkinliği kullanırsınız. Belirli tooAzure SQL Data Warehouse kopyalama etkinliği özellikler için bkz: [kopyalama etkinliği özellikleri](#copy-activity-properties) bölümü. Nasıl toouse bir veri deposu bir kaynak veya bir havuz olarak hakkında daha fazla bilgi için veri deposu hello önceki bölümdeki hello bağlantısına tıklayın.

Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur. Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.  Azure SQL Data Warehouse/kullanılan toocopy verileri olan Data Factory varlıkları için JSON tanımlarıyla örnekleri için bkz: [JSON örnekler](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) bu makalenin.

Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooAzure SQL veri ambarı olan JSON özellikleri hakkında ayrıntılı bilgi sağlar:

## <a name="linked-service-properties"></a>Bağlantılı hizmet özellikleri
Aşağıdaki tablonun hello JSON öğeleri belirli tooAzure SQL veri ambarı bağlantılı hizmeti için bir açıklama sağlar.

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| type |Merhaba type özelliği ayarlanmalıdır: **AzureSqlDW** |Evet |
| connectionString |Tooconnect toohello Azure SQL Data Warehouse örneğine hello connectionString özelliği için gerekli bilgiler belirtin. Yalnızca temel kimlik doğrulama desteklenir. |Evet |

> [!IMPORTANT]
> Yapılandırma [Azure SQL veritabanı Güvenlik Duvarı](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) ve veritabanı sunucusu çok hello[Azure Hizmetleri tooaccess hello sunucusu izin](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure). Ayrıca, dış Azure veri fabrikası ağ geçidi ile şirket içi veri kaynaklarından dahil olmak üzere veri tooAzure SQL Data Warehouse kopyalıyorsanız, veri tooAzure SQL Data Warehouse gönderme hello makine için uygun IP adresi aralığı yapılandırın.

## <a name="dataset-properties"></a>Veri kümesi özellikleri
Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi. Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.

Merhaba typeProperties bölümü veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar. Merhaba **typeProperties** hello veri kümesi için bir bölüm türü **AzureSqlDWTable** hello aşağıdaki özelliklere sahiptir:

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| tableName |Merhaba tablonun veya bağlantılı hizmet hello hello Azure SQL Data Warehouse Veritabanı görünümünde adı ifade eder. |Evet |

## <a name="copy-activity-properties"></a>Etkinlik özellikleri Kopyala
Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi. Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.

> [!NOTE]
> Merhaba kopyalama etkinliği yalnızca bir girdi alır ve tek bir çıktı üretir.

Oysa hello typeProperties bölümünde hello etkinlik özellikleri her etkinlik türü ile farklılık gösterir. Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.

### <a name="sqldwsource"></a>SqlDWSource
Kaynak türü olduğunda **SqlDWSource**, aşağıdaki özelliklere hello kullanılabilir **typeProperties** bölümü:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| sqlReaderQuery |Merhaba özel sorgu tooread verileri kullanın. |SQL sorgu dizesi. Örneğin: seçin * from MyTable. |Hayır |
| sqlReaderStoredProcedureName |Merhaba adını hello kaynak tablodan veri okuyan yordamı depolanır. |Saklı yordam hello adı. Merhaba son SQL deyimi SELECT deyimi hello saklı yordam içinde olmalıdır. |Hayır |
| storedProcedureParameters |Saklı yordam hello için parametreler. |Ad/değer çiftleri. Adları ve büyük/küçük harf parametrelerinin hello adları ve büyük küçük harf kullanımını hello saklı yordam parametreleri eşleşmelidir. |Hayır |

Merhaba, **sqlReaderQuery** Merhaba SqlDWSource, hello kopyalama etkinliği çalıştıran bu sorguyu hello Azure SQL Data Warehouse kaynak tooget hello verileri karşı belirtilir.

Alternatif olarak, bir saklı yordam hello belirterek belirleyebileceğiniz **sqlReaderStoredProcedureName** ve **storedProcedureParameters** (Merhaba saklı yordam parametreleri alır).

SqlReaderQuery veya sqlReaderStoredProcedureName belirtmezseniz hello yapısı bölümünde JSON hello kümesinin tanımlanan hello sütunlar kullanılan toobuild hello Azure SQL veri ambarına karşı sorgu toorun'dır. Örnek: `select column1, column2 from mytable`. Merhaba veri kümesi tanımı hello yapısına sahip değil, tüm sütunlar hello tablosundan seçilir.

#### <a name="sqldwsource-example"></a>SqlDWSource örneği

```JSON
"source": {
    "type": "SqlDWSource",
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

### <a name="sqldwsink"></a>SqlDWSink
**SqlDWSink** aşağıdaki özelliklere hello destekler:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| sqlWriterCleanupScript |Belirli bir dilimle verilerinin temizlenmesini gibi bir sorgu için kopyalama etkinliği tooexecute belirtin. Ayrıntılar için bkz [Yinelenebilirlik bölüm](#repeatability-during-copy). |Sorgu bildirimi. |Hayır |
| Bulunan'allowpolybase |Gösterir olup olmadığını BULKINSERT mekanizması yerine toouse PolyBase (varsa). <br/><br/> **PolyBase kullanarak SQL Data Warehouse'a veri yolu tooload veri önerilen hello değildir.** Bkz: [kullanım PolyBase tooload verilerin Azure SQL veri ambarında](#use-polybase-to-load-data-into-azure-sql-data-warehouse) kısıtlamaları ve ayrıntıları bölümü. |True <br/>False (varsayılan) |Hayır |
| polyBaseSettings |Bir grup hello belirtilebilir özellik **Bulunan'allowpolybase** özelliği çok ayarlanmış**doğru**. |&nbsp; |Hayır |
| rejectValue |Merhaba numarası veya hello sorgu başarısız olmadan önce reddedilemiyor satırları yüzdesini belirtir. <br/><br/>Merhaba seçeneklerinde Reddet hello PolyBase'nın hakkında daha fazla bilgi edinin **bağımsız değişkenleri** bölümünü [CREATE dış TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) konu. |0 (varsayılan), 1, 2... |Hayır |
| rejectType |Merhaba rejectValue seçeneği bir hazır değer veya bir yüzde belirtilen belirtir. |Değer (varsayılan), yüzde |Hayır |
| Havuzu'na ilişkin |Merhaba PolyBase reddedilen satırları hello yüzdesini yeniden hesaplar önce satırları tooretrieve hello sayısını belirler. |1, 2, … |Evet, varsa **rejectType** olan **yüzdesi** |
| useTypeDefault |PolyBase hello metin dosyasından veri aldığında değerlerde eksik toohandle metin dosyaları nasıl ayrılmış belirtir.<br/><br/>Merhaba bağımsız değişkenler bölümünde bu özelliği hakkında daha fazla bilgi [oluşturma EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx). |TRUE, False (varsayılan) |Hayır |
| writeBatchSize |Merhaba arabellek boyutu writeBatchSize ulaştığında veri hello SQL tablosuna ekler. |Tamsayı (satır sayısı) |Hayır (varsayılan: 10000) |
| writeBatchTimeout |Zaman aşımına uğramadan önce hello toplu ekleme işlemi toocomplete bir süre bekleyin. |TimeSpan<br/><br/> Örnek: "00: 30:00" (30 dakika). |Hayır |

#### <a name="sqldwsink-example"></a>SqlDWSink örneği

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-tooload-data-into-azure-sql-data-warehouse"></a>Azure SQL Data Warehouse'a PolyBase tooload verileri kullanma
Kullanarak  **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)**  büyük miktarda veri yüksek işleme ile Azure SQL Data Warehouse'a veri yükleme etkili bir yoldur. Merhaba varsayılan BULKINSERT mekanizmasını yerine PolyBase kullanarak büyük kazanç hello verimliliği de görebilirsiniz. Bkz: [kopyalama performans başvuru numarası](data-factory-copy-activity-performance.md#performance-reference) ayrıntılı karşılaştırması ile. Kullanım örneği ile bir anlatım için bkz: [1 TB altında 15 dakika Azure Data Factory ile Azure SQL Data Warehouse'a veri yükleme](data-factory-load-sql-data-warehouse.md).

* Veri kaynağınızı ise **Azure Blob veya Azure Data Lake Store**ve hello biçimi PolyBase ile uyumlu ise, SQL Data Warehouse Polybase'i kullanarak tooAzure doğrudan kopyalayabilirsiniz. Bkz:  **[Polybase'i kullanarak doğrudan kopyalama](#direct-copy-using-polybase)**  ayrıntılarla.
* Kaynak veri deposu ve biçim başlangıçta desteklenmiyor, PolyBase tarafından hello kullanabilirsiniz  **[Polybase'i kullanarak kopyalama hazırlanan](#staged-copy-using-polybase)**  yerine özelliği. Ayrıca, daha iyi verim otomatik olarak hello veri PolyBase uyumlu biçimine dönüştürmek için kullanılan ve hello verileri Azure Blob storage'da depolamak sağlar. Ardından verileri SQL Data Warehouse'a veri yükler.

Set hello `allowPolyBase` özelliği çok**true** hello Azure SQL Data Warehouse'a örnek Azure Data Factory toouse PolyBase toocopy veri için aşağıdaki gösterildiği gibi. Bulunan'allowpolybase tootrue ayarladığınızda hello kullanarak PolyBase belirli özelliklerini belirtebilirsiniz `polyBaseSettings` özellik grubu. Merhaba bkz [SqlDWSink](#SqlDWSink) polyBaseSettings ile kullanabileceğiniz özellikleri hakkında ayrıntılı bilgi için bölüm.

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true,
    "polyBaseSettings":
    {
        "rejectType": "percentage",
        "rejectValue": 10.0,
        "rejectSampleValue": 100,
        "useTypeDefault": true
    }
}
```

### <a name="direct-copy-using-polybase"></a>Polybase'i kullanarak doğrudan kopyalama
SQL veri ambarı PolyBase doğrudan desteği Azure Blob ve Azure Data Lake Store (hizmet sorumlusu kullanarak) kaynak olarak ve belirli dosya biçimi gereksinimleriyle. Veri kaynağınızı Bu bölümde açıklanan hello ölçütlerini karşılıyorsa, kaynak veri deposu tooAzure PolyBase kullanarak SQL Data Warehouse doğrudan kopyalayabilirsiniz. Aksi takdirde, kullanabileceğiniz [Polybase'i kullanarak kopyalama hazırlanan](#staged-copy-using-polybase).

> [!TIP]
> Data Lake Store tooSQL veri ambarı toocopy verilerden verimli bir şekilde daha fazla bilgi gelen [verilerden daha kolay ve rahat toouncover Öngörüler Data Lake Store ile SQL veri ambarı kullanırken bile Azure Data Factory kılar](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).

Hello gereksinimleri karşılanmadı, Azure Data Factory hello ayarlarını denetler ve otomatik olarak toohello BULKINSERT mekanizması hello veri taşıma için geri döner.

1. **Kaynak bağlantılı hizmeti** türüdür: **AzureStorage** veya **AzureDataLakeStore hizmet asıl kimlik doğrulaması ile**.  
2. Merhaba **girdi veri kümesi** türüdür: **AzureBlob** veya **AzureDataLakeStore**, ve hello biçim türü'nün altında `type` özellikleri **OrcFormat** , veya **TextFormat** yapılandırmaları aşağıdaki hello ile:

   1. `rowDelimiter`olmalıdır  **\n** .
   2. `nullValue`çok ayarlanır**boş dize** (""), veya `treatEmptyAsNull` çok ayarlanır**doğru**.
   3. `encodingName`çok ayarlanır**utf-8**, olduğu **varsayılan** değeri.
   4. `escapeChar`, `quoteChar`, `firstRowAsHeader`, ve `skipLineCount` belirtilmedi.
   5. `compression`olabilir **sıkıştırma yok**, **GZip**, veya **Deflate**.

    ```JSON
    "typeProperties": {
       "folderPath": "<blobpath>",
       "format": {
           "type": "TextFormat",     
           "columnDelimiter": "<any delimiter>",
           "rowDelimiter": "\n",       
           "nullValue": "",           
           "encodingName": "utf-8"    
       },
       "compression": {  
           "type": "GZip",  
           "level": "Optimal"  
       }  
    },
    ```

3. Yoktur hiçbir `skipHeaderLineCount` altında ayarı **BlobSource** veya **AzureDataLakeStore** hello hello ardışık düzeninde kopyalama etkinliği için.
4. Yoktur hiçbir `sliceIdentifierColumnName` altında ayarı **SqlDWSink** hello hello ardışık düzeninde kopyalama etkinliği için. (Tüm veriler güncelleştirilir veya hiçbir şey bir tek çalıştırmada güncelleştirildiğinde PolyBase garanti eder. tooachieve **Yinelenebilirlik**, kullanabileceğinizi `sqlWriterCleanupScript`).
5. Var olan hiçbir `columnMapping` kopyalama etkinliği ilişkili hello kullanılmakta.

### <a name="staged-copy-using-polybase"></a>Polybase'i kullanarak hazırlanmış kopyalama
Veri kaynağınızı hello önceki bölümde sunulan hello ölçütlerle eşleşmeyen, bir geçici hazırlama Azure Blob (Premium depolama olamaz) depolama aracılığıyla veri kopyalamayı etkinleştirebilirsiniz. Bu durumda, Azure Data Factory otomatik olarak hello veri toomeet veri biçimi gereksinimleri PolyBase, daha sonra kullanmak PolyBase tooload verileri SQL Data Warehouse dönüşümleri gerçekleştirir ve en sonunda temp verilerinizi hello Blob depolama biriminden temizleyin. Bkz: [hazırlanan kopyalama](data-factory-copy-activity-performance.md#staged-copy) nasıl hazırlama Azure Blob üzerinden veri kopyalama genel çalıştığı hakkında bilgi.

> [!NOTE]
> Bir şirket içi veri kopyalama verileri Azure SQL Data Polybase'i kullanarak Warehouse'a veri depolamak ve hazırlama, veri yönetimi ağ geçidi sürümü 2.4 ise, JRE (Java Çalışma zamanı ortamı) ağ geçidiniz gerekli olduğunda, makine kullanılan tootransform veri kaynağınızı olduğu doğru biçime. Bu bağımlılık ağ geçidi toohello son tooavoid yükseltme önerir.
>

toouse bu özelliği, oluşturma bir [Azure depolama bağlantılı hizmeti](data-factory-azure-blob-connector.md#azure-storage-linked-service) toohello hello geçici blob depolama alanına sahip bir Azure depolama hesabı anlamına gelir, sonra hello belirtin `enableStaging` ve `stagingSettings` hello kopyalama etkinliği özellikleri hello kod aşağıdaki gösterildiği gibi kullanın:

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server tooSQL Data Warehouse via PolyBase",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDWOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlDwSink",
            "allowPolyBase": true
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob"
        }
    }
}
]
```

## <a name="best-practices-when-using-polybase"></a>PolyBase kullanırken en iyi uygulamalar
Merhaba aşağıdaki bölümlerde ek en iyi yöntemler toohello bölümünde belirtildiği olanları sağlamak [en iyi uygulamalar Azure SQL Data Warehouse için](../sql-data-warehouse/sql-data-warehouse-best-practices.md).

### <a name="required-database-permission"></a>Gerekli veritabanı izni
toouse PolyBase, gerektirdiği SQL Data Warehouse kullanılan tooload verisine sahip hello kullanıcı hello olan ["Denetim" izni](https://msdn.microsoft.com/library/ms191291.aspx) hello hedef veritabanı üzerinde. Tooadd olan tek yönlü tooachieve "db_owner" rolünün bir üyesi olarak o kullanıcı. Bilgi nasıl toodo, izleyerek [Bu bölümde](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).

### <a name="row-size-and-data-type-limitation"></a>Satır boyutu ve verileri sınırlama yazın
Polybase yükleri sınırlı tooloading satırları hem küçük **1 MB** ve tooVARCHR(MAX), yüklenemiyor NVARCHAR(MAX) veya VARBINARY(MAX). Çok başvuran[burada](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).

Satır boyutu 1 MB'tan fazla kaynak verilerle varsa, burada her biri en büyük satır boyutu hello hello sınırını aşmayacak birkaç küçük parçalara toosplit hello kaynak tabloları dikey isteyebilirsiniz. Merhaba küçük tabloları sonra PolyBase kullanarak ve Azure SQL Data Warehouse'da birleştirmeniz yüklenebilir.

### <a name="sql-data-warehouse-resource-class"></a>SQL veri ambarı kaynak sınıfı
tooachieve en iyi olası üretilen işi tooassign büyük kaynak sınıfı toohello kullanıcı olan göz önünde bulundurun PolyBase aracılığıyla SQL veri ambarında kullanılan tooload veri. Bilgi nasıl toodo, izleyerek [kullanıcı kaynak sınıfı örneğini değiştirmek](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).

### <a name="tablename-in-azure-sql-data-warehouse"></a>Azure SQL Data Warehouse tableName
Merhaba aşağıdaki tabloda örnekler hakkında yönergeler verilmektedir toospecify hello **tableName** dataset JSON çeşitli şema ve tablo adı için bir özellik.

| DB şeması | Tablo adı | tableName JSON özelliği |
| --- | --- | --- |
| dbo |MyTable |MyTable ya da dbo. MyTable ya da [dbo]. [MyTable] |
| dbo1 |MyTable |dbo1. MyTable veya [dbo1]. [MyTable] |
| dbo |My.Table |[My.Table] veya [dbo]. [My.Table] |
| dbo1 |My.Table |[dbo1]. [My.Table] |

Aşağıdaki hata hello görürseniz, hello tableName özelliği için belirtilen başlangıç değeri ile ilgili bir sorun olabilir. Merhaba tableName JSON özellik için hello doğru bir şekilde toospecify değerler için Hello tabloya bakın.  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a>Varsayılan değerleri içeren sütun
Şu anda aynı sayıda sütun hello hedef tabloda olduğu gibi hello PolyBase özelliği veri fabrikasında yalnızca kabul eder. Dört sütun içeren bir tablo varsa ve bunlardan birini varsayılan bir değerle tanımlanan söyleyin. Merhaba giriş verisi hala dört sütun içermelidir. 3-sütun girdi veri kümesi sağlayan bir hata benzer toohello iletiden verir:

```
All columns of hello table must be specified in hello INSERT BULK statement.
```
NULL değer, varsayılan değeri özel bir biçimidir. Merhaba sütunu null atanabilir ise, hello giriş verilerini (blob) Bu sütun için boş olabilir (Merhaba giriş kümesinden eksik olamaz). PolyBase, bunlar için NULL hello Azure SQL Data Warehouse ekler.  

## <a name="auto-table-creation"></a>Otomatik Tablo oluşturma
Toohello kaynak tablosunda karşılık gelen Azure SQL veritabanı tooAzure SQL veri ambarı ve hello tablosu hello hedef deposunda mevcut değil veya kopyalama Sihirbazı'nı toocopy verileri SQL Server kullanıyorsanız, veri fabrikası otomatik olarak hello tablo hello oluşturabilirsiniz Merhaba kaynak tablo şemasını kullanarak veri ambarı'nı tıklatın.

Veri Fabrikası hello hedef deposunda hello tablo oluşturur hello ile aynı tablo hello kaynak veri deposundaki adı. Merhaba veri türlerinde sütun türü eşlemesi aşağıdaki hello göre seçilir. Gerekli olursa, kaynak ve hedef depoları arasında uyumsuzlukları türü dönüşümleri toofix gerçekleştirir. Ayrıca, hepsini bir kez Tablo dağıtım kullanır.

| Kaynak SQL veritabanı sütun türü | Hedef SQL DW sütun türü (boyutu kısıtlaması) |
| --- | --- |
| Int | Int |
| BigInt | BigInt |
| Tamsayı | Tamsayı |
| Mini tamsayı | Mini tamsayı |
| bit | bit |
| Ondalık | Ondalık |
| sayısal | Ondalık |
| Kayan nokta | Kayan nokta |
| para | para |
| Real | Real |
| Küçük para | Küçük para |
| İkili | İkili |
| varbinary | Varbinary (yukarı too8000) |
| Tarih | Tarih |
| Tarih saat | Tarih saat |
| DateTime2 | DateTime2 |
| Zaman | Zaman |
| DateTimeOffset | DateTimeOffset |
| SmallDateTime | SmallDateTime |
| Metin | VARCHAR (yukarı too8000) |
| NText | NVarChar (yukarı too4000) |
| Görüntü | VarBinary (yukarı too8000) |
| Benzersiz tanımlayıcı | Benzersiz tanımlayıcı |
| char | char |
| NChar | NChar |
| VarChar | VarChar (yukarı too8000) |
| NVarChar | NVarChar (yukarı too4000) |
| XML | VARCHAR (yukarı too8000) |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a>Tür eşlemesi için Azure SQL veri ambarı
Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopyalama etkinliği gerçekleştiren kaynak türleri toosink türlerinden otomatik tür dönüşümleri 2 adımlı yaklaşımı izleyerek hello ile:

1. Yerel kaynak türleri too.NET türünden Dönüştür
2. .NET türü toonative havuz türünden Dönüştür

Çok & Azure SQL veri ambarından veri taşırken, hello aşağıdaki eşlemelerini too.NET türü ve bunun tersi de kullanılır.

Merhaba eşleme hello aynı [ADO.NET için SQL Server veri türü eşlemesi](https://msdn.microsoft.com/library/cc716729.aspx).

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

Ayrıca, kaynak veri kümesi toocolumns hello kopyalama etkinliği tanımında havuz kümesinden sütunlarından eşleyebilirsiniz. Ayrıntılar için bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).

## <a name="json-examples-for-copying-data-tooand-from-sql-data-warehouse"></a>SQL veri ambarından veri tooand kopyalama için JSON örnekleri
Merhaba aşağıdaki örneklerde sağlayan örnek JSON tanımları toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Bunlar Göster nasıl toocopy veri tooand Azure SQL Data Warehouse ve Azure Blob Storage. Ancak, veriler kopyalanabilir **doğrudan** herhangi birinden belirtildiği hello havuzlarını, kaynakları tooany [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.

### <a name="example-copy-data-from-azure-sql-data-warehouse-tooazure-blob"></a>Örnek: Verilerini Azure SQL Data Warehouse tooAzure Blob
Merhaba örnek Data Factory varlıklarını aşağıdaki hello tanımlar:

1. Bağlı hizmet türü [AzureSqlDW](#linked-service-properties).
2. Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureSqlDWTable](#dataset-properties).
4. Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [SqlDWSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Merhaba örnek zaman serisi (saatlik, günlük, vs.) verileri Azure SQL Data Warehouse veritabanı tooa blob tablosunda her saat kopyalar. Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.

**Azure SQL Data Warehouse bağlantılı hizmeti:**

```JSON
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
**Azure SQL veri ambarı veri kümesi giriş:**

Azure SQL Data Warehouse'da bir tablo "MyTable" oluşturulur ve zaman serisi veri için "timestampcolumn" adlı bir sütun içerdiği Hello örnek varsayar.

"Dış" ayarı: "true" bildirir hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.

```JSON
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
**Azure Blob dataset çıktı:**

Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1). hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir. Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.

```JSON
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

**SqlDWSource ve BlobSink ardışık düzeninde etkinlik kopyalayın:**

Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**SqlDWSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**. Merhaba belirtilen hello SQL sorgusu **SqlReaderQuery** özelliği saat toocopy geçmiş hello hello veri seçer.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLDWtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSqlDWInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
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
      }
     ]
   }
}
```
> [!NOTE]
> Merhaba örnekte **sqlReaderQuery** SqlDWSource hello için belirtilir. Merhaba kopyalama etkinliği hello Azure SQL Data Warehouse kaynak tooget hello verileri karşı bu sorguyu çalıştırır.
>
> Alternatif olarak, bir saklı yordam hello belirterek belirleyebileceğiniz **sqlReaderStoredProcedureName** ve **storedProcedureParameters** (Merhaba saklı yordam parametreleri alır).
>
> SqlReaderQuery veya sqlReaderStoredProcedureName belirtmezseniz, kullanılan toobuild bir sorgu (select column1, column2 mytable gelen) hello yapısı bölümünde JSON hello kümesinin tanımlanan hello sütunlar: hello Azure SQL Data Warehouse karşı toorun. Merhaba veri kümesi tanımı hello yapısına sahip değil, tüm sütunlar hello tablosundan seçilir.
>
>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-data-warehouse"></a>Örnek: Kopyalama verileri Azure Blob tooAzure SQL veri ambarı
Merhaba örnek Data Factory varlıklarını aşağıdaki hello tanımlar:

1. Bağlı hizmet türü [AzureSqlDW](#linked-service-properties).
2. Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureSqlDWTable](#dataset-properties).
5. A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) ve [SqlDWSink](#copy-activity-properties).

Merhaba örnek time series verilerini (saatlik, günlük, vb.) Azure blob tooa Azure SQL Data Warehouse veritabanı tablosunda her saat kopyalar. Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.

**Azure SQL Data Warehouse bağlantılı hizmeti:**

```JSON
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
**Azure Blob girdi veri kümesi:**

Veri toplanma yeni blob üzerinden saatte (sıklığı: saat, aralığı: 1). Merhaba klasör yolu ve dosya adını hello blob dinamik olarak değerlendirilir işleniyor hello dilimin hello başlangıç zamanı temel alınarak. Merhaba klasör yolu yıl, ay ve gün kısmını hello başlangıç saati ve dosya adı hello başlangıç saati hello saat bölümünü kullanır. "dış": "true" ayarı bu tablosu dış toohello veri fabrikası ve hello veri fabrikasında bir etkinlik tarafından üretilen değil hello Data Factory hizmetinin sizi bilgilendirir.

```JSON
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
**Azure SQL veri ambarı veri kümesi çıkışını:**

Merhaba örnek Azure SQL Data Warehouse "MyTable" adlı veri tooa tablosuna kopyalar. Azure SQL Data Warehouse ile Merhaba tablosunu oluşturan hello Blob CSV dosyası toocontain beklediğiniz gibi hello aynı sayıda sütun. Yeni satırlar toohello tablo saatte eklenir.

```JSON
{
  "name": "AzureSqlDWOutput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
**BlobSource ve SqlDWSink ardışık düzeninde etkinlik kopyalayın:**

Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**BlobSource** ve **havuz** türü olarak ayarlanmış çok**SqlDWSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQLDW",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlDWOutput"
          }
        ],
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
      }
      ]
   }
}
```
İçin bkz: hello bkz [1 TB altında 15 dakika Azure Data Factory ile Azure SQL Data Warehouse'a veri yükleme](data-factory-load-sql-data-warehouse.md) ve [Azure Data Factory ile veri yükleme](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) hello Azure SQL Data Warehouse makalesinde belgeler.

## <a name="performance-and-tuning"></a>Performans ve ayarlama
Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.
