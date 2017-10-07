---
title: / Data Factory kullanarak Oracle aaaCopy verileri | Microsoft Docs
description: "Nasıl toocopy veri için/olan Oracle veritabanından Azure Data Factory kullanarak şirket içi öğrenin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3c20aa95-a8a1-4aae-9180-a6a16d64a109
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: adb6d5fbe38e18791616ac77e8179970bbea37fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a>Öğesine/öğesinden Azure Data Factory kullanarak şirket içi Oracle veri kopyalama
Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove veri grafikten bir şirket içi Oracle veritabanına açıklanmaktadır. Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.

## <a name="supported-scenarios"></a>Desteklenen senaryolar
Veri kopyalama **bir Oracle veritabanından** veri depolarına aşağıdaki toohello:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Veri depoları aşağıdaki hello verileri kopyalayabilirsiniz **tooan Oracle veritabanı**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a>Ön koşullar
Veri Fabrikası hello veri yönetimi ağ geçidi kullanarak bağlanan tooon içi Oracle kaynakları destekler. Bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) makale toolearn veri yönetimi ağ geçidi hakkında ve [şirket içi toocloud veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale hello ağ geçidi kurun veri ardışık ayarlama hakkında adım adım yönergeler için toomove verileri.

Merhaba Oracle bir Azure Iaas sanal barındırılan olsa bile ağ geçidi gereklidir. Merhaba ağ geçidi üzerinde aynı Iaas VM hello veri olarak depolamak veya hello ağ geçidi olarak aynı uzunlukta farklı bir VM üzerinde toohello veritabanı bağlanabilir hello yükleyebilirsiniz.

> [!NOTE]
> Bkz: [ağ geçidi sorunlarını giderme](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) ilgili sorunlar bağlantı/ağ geçidi sorun giderme ipuçları için.

## <a name="supported-versions-and-installation"></a>Desteklenen sürümleri ve yükleme
Bu Oracle bağlayıcı sürücülerin iki sürümlerini destekler:

- **(Önerilen) Oracle için Microsoft sürücüsü**: Oracle hello ağ geçidi ile birlikte otomatik olarak yüklenen için veri yönetimi ağ geçidi'nden sürüm 2.7, Microsoft sürücüsü başlayarak, bu nedenle yapmanıza gerek yoktur sırayla tooadditionally tanıtıcı hello sürücüsü Ayrıca tooestablish bağlantı tooOracle ve bu sürücü kullanarak daha iyi kopyalama performansını yaşayabilirsiniz. Oracle sürümleri veritabanları desteklenir:
    - Oracle 12c R1 (12,1)
    - Oracle 11g R1, R2 (11.1, 11.2)
    - Oracle 10g R1, R2 (10,1, 10.2)
    - Oracle 9i R1, R2 (9.0.1, 9.2)
    - Oracle 8i R3 (8.1.7)

> [!IMPORTANT]
> Şu anda Oracle için Microsoft sürücüsü yalnızca Oracle ancak tooOracle yazılamıyor veri kopyalamayı destekler. Ve Not hello test bağlantısı özelliği veri yönetimi ağ geçidi tanılama sekmesinde bu sürücüyü desteklemiyor. Alternatif olarak, hello Kopyalama Sihirbazı'nı toovalidate hello bağlantısını kullanabilirsiniz.
>

- **.NET için Oracle veri sağlayıcısı:** toouse Oracle veri sağlayıcısı toocopy verileri de seçebilirsiniz / tooOracle. Bu bileşen dahil [için Oracle veri erişim bileşenleri Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/). Merhaba uygun sürüm (32/64 bit) hello ağ geçidi yüklendiği hello makineye yükleyin. [Oracle veri sağlayıcısı .NET 12,1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) tooOracle veritabanı 10 g sürüm 2 veya sonrasını erişebilirsiniz.

    "XCopy yükleme" seçerseniz, hello readme.htm adımları izleyin. Kullanıcı Arabirimi (olmayan-XCopy biri) ile Merhaba yükleyici seçtiğiniz öneririz.

    Merhaba sağlayıcı yükledikten sonra **yeniden** hello Hizmetleri uygulaması (veya) veri yönetimi ağ geçidi Yapılandırma Yöneticisi kullanarak makinenizde veri yönetimi ağ geçidi ana bilgisayar hizmeti.  

Kopyalama Sihirbazı'nı tooauthor hello kopyalama işlem hattını kullanırsanız, otomatik olarak belirlenen hello sürücü türü olacaktır. Microsoft sürücüsü, ağ geçidi sürümü 2.7 düşük olduğu veya Oracle havuz olarak seçtiğiniz sürece varsayılan olarak kullanılır.

## <a name="getting-started"></a>Başlarken
Farklı araçlar/API'lerini kullanarak bir şirket içi Oracle veritabanından/gelen verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.

Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**. Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.

Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**. Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.

Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:

1. Oluşturma bir **veri fabrikası**. Veri Fabrikası bir veya daha fazla ardışık düzen içerebilir. 
2. Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası. Bir Oralce veritabanı tooan Azure blob depolama veri kopyalama, örneğin, iki bağlı hizmet toolink Oracle veritabanı ve Azure depolama hesabı tooyour veri fabrikası oluşturun. Belirli tooOracle bağlantılı hizmet özellikler için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü.
3. Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi. Merhaba son adımda bahsedilen hello örnekte, Oracle veritabanınız hello giriş verileri içeren bir veri kümesi toospecify hello tablo oluşturun. Başka bir veri kümesi toospecify hello blob kapsayıcı oluşturun ve hello verilerini tutan hello klasörü hello Oracle veritabanı kopyalanır. Belirli tooOracle dataset özellikler için bkz: [veri kümesi özellikleri](#dataset-properties) bölümü.
4. Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile. Daha önce bahsedilen hello örnekte OracleSource bir kaynak ve BlobSink havuzu olarak hello kopya etkinliği için kullanırsınız. Azure Blob Storage tooOracle veritabanı ' kopyalıyorsanız benzer şekilde, BlobSource ve OracleSink hello kopyalama etkinliği kullanırsınız. Belirli tooOracle veritabanı kopyalama etkinliği özellikler için bkz: [kopyalama etkinliği özellikleri](#copy-activity-properties) bölümü. Nasıl toouse bir veri deposu bir kaynak veya bir havuz olarak hakkında daha fazla bilgi için veri deposu hello önceki bölümdeki hello bağlantısına tıklayın. 

Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur. Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.  Şirket içi Oracle veritabanına/kullanılan toocopy verileri olan Data Factory varlıkları için JSON tanımlarıyla örnekleri için bkz: [JSON örnekler](#json-examples-for-copying-data-to-and-from-oracle-database) bu makalenin.

Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıklarını olan JSON özellikleri hakkında ayrıntılı bilgi sağlar:

## <a name="linked-service-properties"></a>Bağlantılı hizmet özellikleri
Aşağıdaki tablonun hello JSON öğeleri belirli tooOracle bağlantılı hizmeti için bir açıklama sağlar.

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| type |Merhaba type özelliği ayarlanmalıdır: **OnPremisesOracle** |Evet |
| driverType | Hangi sürücü toouse toocopy verilerden belirtin / tooOracle veritabanı. İzin verilen değerler **Microsoft** veya **ODP** (varsayılan). Bkz: [desteklenen sürümü ve yükleme](#supported-versions-and-installation) sürücü ayrıntıları bölümü. | Hayır |
| connectionString | Tooconnect toohello Oracle veritabanı örneği hello connectionString özelliği için gerekli bilgiler belirtin. | Evet |
| gatewayName | Kullanılan tooconnect toohello olan şirket içi Oracle Sunucusu hello ağ geçidi adı |Evet |

**Örnek: Microsoft sürücüsü kullanma:**
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**Örnek: ODP sürücü kullanma**

Çok başvuran[bu site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) biçimleri hello için.

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

## <a name="dataset-properties"></a>Veri kümesi özellikleri
Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi. Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Oracle, Azure blob, Azure tablo, vs.) için benzer.

Merhaba typeProperties bölümü veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar. türü OracleTable hello veri kümesi için Hello typeProperties bölümü hello aşağıdaki özelliklere sahip:

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| tableName |Merhaba bağlantılı hizmet hello Oracle veritabanı Merhaba tablonun adını gösterir. |Hayır (varsa **oracleReaderQuery** , **OracleSource** belirtilir) |

## <a name="copy-activity-properties"></a>Etkinlik özellikleri Kopyala
Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi. Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.

> [!NOTE]
> Merhaba kopyalama etkinliği yalnızca bir girdi alır ve tek bir çıktı üretir.

Oysa hello typeProperties bölümünde hello etkinlik özellikleri her etkinlik türü ile farklılık gösterir. Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.

### <a name="oraclesource"></a>OracleSource
Kopyalama etkinliğinde hello kaynak türü olduğunda **OracleSource** aşağıdaki özelliklere hello kullanılabilir **typeProperties** bölümü:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| oracleReaderQuery |Merhaba özel sorgu tooread verileri kullanın. |SQL sorgu dizesi. Örneğin: seçin * from MyTable <br/><br/>Belirtilmezse, yürütülen SQL deyimini hello: seçin * from MyTable |Hayır (varsa **tableName** , **dataset** belirtilir) |

### <a name="oraclesink"></a>OracleSink
**OracleSink** aşağıdaki özelliklere hello destekler:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| writeBatchTimeout |Zaman aşımına uğramadan önce hello toplu ekleme işlemi toocomplete bir süre bekleyin. |TimeSpan<br/><br/> Örnek: 00:30:00 (30 dakika). |Hayır |
| writeBatchSize |Merhaba arabellek boyutu writeBatchSize ulaştığında veri hello SQL tablosuna ekler. |Tamsayı (satır sayısı) |Hayır (varsayılan: 100) |
| sqlWriterCleanupScript |Belirli bir dilimle verilerinin temizlenmesini gibi bir sorgu için kopyalama etkinliği tooexecute belirtin. |Sorgu bildirimi. |Hayır |
| Sliceıdentifiercolumnname |Kopyalama etkinliği toofill sütun adı, ne zaman yeniden çalıştırılacağını belirli bir dilim verilerini kullanılan tooclean olduğu otomatik dilim tanımlayıcı ile belirtin. |Binary(32) veri türüne sahip bir sütunun sütun adı. |Hayır |

## <a name="json-examples-for-copying-data-tooand-from-oracle-database"></a>Oracle veritabanından veri tooand kopyalamak için JSON örnekleri
Merhaba aşağıdaki örnek örnek JSON tanımları sağlar, toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Bunlar Göster nasıl toocopy verilerden / tooan Oracle veritabanı/Azure Blob depolama biriminden. Ancak, veri belirtildiği hello havuzlarını, kopyalanan tooany olabilir [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.   

## <a name="example-copy-data-from-oracle-tooazure-blob"></a>Örnek: Verilerini Oracle tooAzure Blob

Merhaba örnek data factory varlıklarını aşağıdaki hello sahiptir:

1. Bağlı hizmet türü [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).
2. Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Bir giriş [dataset](data-factory-create-datasets.md) türü [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).
4. Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) kaynağı olarak ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) havuz olarak.

Merhaba örnek verileri bir tabloda bir şirket içi Oracle veritabanı tooa blob saatlik kopyalar. Merhaba örnekte kullanılan çeşitli özellikler hakkında daha fazla bilgi için hello örnekleri aşağıdaki bölümlerde belgelerine bakın.

**Oracle bağlantılı hizmeti:**

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**Azure Blob storage bağlı hizmeti:**

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

**Oracle girdi veri kümesi:**

Merhaba örnek Oracle tablo "MyTable" oluşturulur ve zaman serisi veri için "timestampcolumn" adlı bir sütun içerdiği varsayar.

"Dış" ayarı: "true" bildirir hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.

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
            "anchorDateTime": "2014-02-27T12:00:00",
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

**Azure Blob dataset çıktı:**

Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1). Merhaba klasör yolu ve dosya adını hello blob dinamik olarak değerlendirilir işleniyor hello dilimin hello başlangıç zamanı temel alınarak. Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.

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

**Kopyalama etkinliği ile kanal:**

Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun saatlik ise. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**OracleSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**.  Merhaba SQL sorgusu ile belirtilen **oracleReaderQuery** özelliği saat toocopy geçmiş hello hello veri seçer.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "OracletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": " OracleInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
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
            }
        ]
    }
}
```

## <a name="example-copy-data-from-azure-blob-toooracle"></a>Örnek: Verilerini Azure Blob tooOracle
Bu örnek nasıl toocopy verileri Azure Blob Storage tooan Oracle veritabanı şirket içi gösterir. Ancak, veriler kopyalanabilir **doğrudan** herhangi belirtildiği hello kaynakları [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.  

Merhaba örnek data factory varlıklarını aşağıdaki hello sahiptir:

1. Bağlı hizmet türü [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).
2. Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Bir çıkış [dataset](data-factory-create-datasets.md) türü [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).
5. A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) kaynağı olarak [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) havuz olarak.

Merhaba örnek verileri saatte bir şirket içi Oracle veritabanına bir blob tooa tablodaki kopyalar. Merhaba örnekte kullanılan çeşitli özellikler hakkında daha fazla bilgi için hello örnekleri aşağıdaki bölümlerde belgelerine bakın.

**Oracle bağlantılı hizmeti:**
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
            User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**Azure Blob storage bağlı hizmeti:**
```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

**Azure Blob girdi veri kümesi**

Veri toplanma yeni blob üzerinden saatte (sıklığı: saat, aralığı: 1). Merhaba klasör yolu ve dosya adını hello blob dinamik olarak değerlendirilir işleniyor hello dilimin hello başlangıç zamanı temel alınarak. Merhaba klasör yolu yıl, ay ve gün kısmını hello başlangıç saati ve dosya adı hello başlangıç saati hello saat bölümünü kullanır. "dış": "true" ayarı bu tablosu dış toohello veri fabrikası ve hello veri fabrikasında bir etkinlik tarafından üretilen değil hello Data Factory hizmetinin sizi bilgilendirir.

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
            "frequency": "Day",
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

**Oracle çıktı veri kümesi:**

Hello örnek Oracle tablo "MyTable" oluşturdunuz varsayılır. Oracle ile Merhaba tablosunu oluşturan hello Blob CSV dosyası toocontain beklediğiniz gibi hello aynı sayıda sütun. Yeni satırlar toohello tablo saatte eklenir.

```json
{
    "name": "OracleOutput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Day",
            "interval": "1"
        }
    }
}
```

**Kopyalama etkinliği ile kanal:**

Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**BlobSource** ve hello **havuz** türü olarak ayarlanmış çok**OracleSink**.  

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-05T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
            {
                "name": "AzureBlobtoOracle",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "OracleOutput"
                    }
                ],
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
            }
        ]
    }
}
```


## <a name="troubleshooting-tips"></a>Sorun giderme ipuçları
### <a name="problem-1-net-framework-data-provider"></a>Sorun 1: .NET Framework veri sağlayıcısı

Merhaba aşağıdakilere bakın **hata iletisi**:

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable toofind hello requested .Net Framework Data Provider. It may not be installed”.  

**Olası nedenler:**

1. Merhaba Oracle için .NET Framework veri sağlayıcısı yüklü değil.
2. Merhaba Oracle için .NET Framework veri sağlayıcısı yüklü too.NET Framework 2.0 ve .NET Framework 4.0 hello klasörlerde bulunamadı.

**Çözümleme/geçici çözüm:**

1. Merhaba, Oracle için .NET sağlayıcısı yüklemediyseniz [yüklemek](http://www.oracle.com/technetwork/topics/dotnet/downloads/) ve hello senaryo yeniden deneyin.
2. Merhaba sağlayıcı yükledikten sonra bile hello hata iletisi alırsanız, adımları hello:
   1. Makine yapılandırma .NET 2.0 hello klasöründen açın: <system disk>: \Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.
   2. Arama **.NET için Oracle veri sağlayıcısı**, ve hello örnek altında aşağıdaki gösterildiği gibi mümkün toofind bir giriş olmalıdır **system.data** -> **DbProviderFactories**: "<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description=".NET için oracle veri sağlayıcısı" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" />”
3. Bu giriş toohello machine.config dosyasının v4.0 klasörü aşağıdaki hello kopyalayın: <system disk>: \Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config ve değişiklik hello sürüm too4.xxx.x.x.
4. "< ODP.NET yüklü yolu > \11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll" Merhaba Genel Derleme Önbelleği'ne (GAC) çalıştırarak yükleyin `gacutil /i [provider path]`. ## sorun giderme ipuçları

### <a name="problem-2-datetime-formatting"></a>Sorun 2: datetime biçimlendirme

Merhaba aşağıdakilere bakın **hata iletisi**:

    Message=Operation failed in Oracle Database with hello following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

**Çözümleme/geçici çözüm:**

Merhaba aşağıda gösterildiği gibi tarihleri, Oracle veritabanınızı nasıl yapılandırıldığına göre kopyalama etkinliğinde tooadjust hello sorgu dizesi gerekebilir (Merhaba to_date işlevi kullanılarak) örnek:

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a>Oracle için tür eşlemesi
Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale kopyalama etkinliği ile 2 adımlı yaklaşımı izleyerek hello kaynak türleri toosink türlerinden otomatik tür dönüşümleri gerçekleştirir:

1. Yerel kaynak türleri too.NET türünden Dönüştür
2. .NET türü toonative havuz türünden Dönüştür

Verileri Oracle'dan taşırken, eşlemeleri aşağıdaki hello Oracle veri türü too.NET türünden ve kullanılır.

| Oracle veri türü | .NET framework veri türü |
| --- | --- |
| BDOSYA |Byte] |
| BLOB |Byte] |
| CHAR |Dize |
| CLOB |Dize |
| TARİH |Tarih saat |
| KAYAN NOKTA |Ondalık, dize (varsa precision > 28) |
| TAMSAYI |Ondalık, dize (varsa precision > 28) |
| ARALIĞI yıl tooMONTH |Int32 |
| Aralık gün tooSECOND |TimeSpan |
| UZUN |Dize |
| UZUN HAM |Byte] |
| NCHAR |Dize |
| NCLOB |Dize |
| SAYI |Ondalık, dize (varsa precision > 28) |
| NVARCHAR2 |Dize |
| HAM |Byte] |
| SATIR KİMLİĞİ |Dize |
| ZAMAN DAMGASI |Tarih saat |
| YEREL SAAT DİLİMİ ZAMAN DAMGASI |Tarih saat |
| SAAT DİLİMİ ZAMAN DAMGASI |Tarih saat |
| İŞARETSİZ TAMSAYI |Sayı |
| VARCHAR2 |Dize |
| XML |Dize |

> [!NOTE]
> Veri türü **ARALIĞI yıl tooMONTH** ve **ARALIĞI gün tooSECOND** Microsoft sürücüsü kullanılırken desteklenmez.

## <a name="map-source-toosink-columns"></a>Kaynak toosink sütunları eşleme
Kaynak veri kümesi toocolumns havuz kümesindeki eşleme sütunlarında hakkında toolearn bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>İlişkisel kaynaklardan yinelenebilir okuma
İlişkisel veri depoları veri kopyalama işlemi sırasında Yinelenebilirlik göz tooavoid tutmak istenmeyen sonuçları. Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz. Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz. Bir dilim iki yolla yeniden zaman, aynı veri hello emin toomake nasıl geçtiğinden bağımsız okuma gerekir dilim birçok kez çalıştırın. Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Performans ve ayarlama
Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.
