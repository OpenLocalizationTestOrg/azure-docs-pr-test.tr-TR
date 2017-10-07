---
title: Azure tablo/aaaMove verileri | Microsoft Docs
description: "Bilgi nasıl/Azure Data Factory kullanarak Azure Table Storage toomove verileri."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 07b046b1-7884-4e57-a613-337292416319
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 3dc3da6d88854674a9108b600534bc5d07575f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-table-using-azure-data-factory"></a>Azure Data Factory kullanarak Azure tablodan veri tooand taşıma
Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove veri öğesine/öğesinden Azure Table Storage açıklanmaktadır. Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar. 

Veri depolamak tooAzure Table Storage veya Azure Table Storage desteklenen tooany havuz verileri depolamak herhangi desteklenen bir kaynaktan veri kopyalayabilirsiniz. Merhaba kaynakları veya havuzlarını olarak hello kopyalama etkinliği tarafından desteklenen veri depoları listesi için bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo. 

## <a name="getting-started"></a>Başlarken
Farklı araçlar/API'lerini kullanarak Azure Table Storage/gruptan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.

Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**. Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.

Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**. Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için. 

Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin: 

1. Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.
2. Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi. 
3. Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile. 

Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur. Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.  Bir Azure Table Storage/kullanılan toocopy verileri olan Data Factory varlıkları için JSON tanımlarıyla örnekleri için bkz: [JSON örnekler](#json-examples) bu makalenin. 

Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooAzure Table Storage olan JSON özellikleri hakkında ayrıntılı bilgi sağlar: 

## <a name="linked-service-properties"></a>Bağlantılı hizmet özellikleri
İki tür vardır bağlı hizmetler toolink Azure blob depolama tooan Azure data factory kullanabilirsiniz. Bunlar: **AzureStorage** bağlantılı hizmeti ve **AzureStorageSas** bağlı hizmeti. Hello Azure Storage bağlı hizmeti hello data factory genel erişim toohello Azure Storage ile sağlar. Hello Azure depolama SAS (paylaşılan erişim imzası) bağlı ise hello data factory ile sınırlı/zaman sınırlı erişim toohello Azure depolama hizmeti sağlar. Bu iki bağlı hizmet arasındaki herhangi bir fark vardır. Gereksinimlerinize uygun hello bağlı hizmeti seçin. Merhaba aşağıdaki bölümlerde daha fazla ayrıntı bu iki bağlı hizmet sağlar.

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a>Veri kümesi özellikleri
Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi. Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.

Merhaba typeProperties bölümü veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar. Merhaba **typeProperties** hello veri kümesi için bir bölüm türü **AzureTable** hello aşağıdaki özelliklere sahiptir.

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| tableName |Bağlantılı hizmetinin hello Azure tablo veritabanı örneğinde Merhaba tablonun adını gösterir. |Evet. Bir tableName bir azureTableSourceQuery belirtildiğinde, tüm hello tablosundan kopyalanan toohello hedef kayıtlarıdır. Bir azureTableSourceQuery de belirtilirse hello sorguyu karşılayan hello tablosundan kopyalanan toohello hedef kayıtlarıdır. |

### <a name="schema-by-data-factory"></a>Şema tarafından veri fabrikası
Azure Table gibi şemasız veri depoları için hello Data Factory hizmetinin yolları aşağıdaki hello birinde hello şema oluşturur:

1. Hello kullanarak verilerin hello yapısını belirtirseniz **yapısı** hello veri kümesi tanımında hello Data Factory hizmeti özelliği bu yapısı hello şema olarak geliştirir. Bu durumda, bir satır bir sütun için bir değer içermiyorsa, bir null değer için sağlanır.
2. Hello kullanarak verilerin hello yapısını belirtmezseniz **yapısı** hello veri kümesi tanımı, veri fabrikası özelliğinde hello verilerde hello ilk satırını kullanarak hello şema oluşturur. Bu durumda, Hello ilk satır hello tam şema içermiyorsa, bazı sütunları hello kopyalama işlemi sonucunda eksik.

Bu nedenle, şemasız veri kaynakları için hello en iyi uygulama toospecify hello hello kullanarak veri yapısıdır **yapısı** özelliği.

## <a name="copy-activity-properties"></a>Etkinlik özellikleri Kopyala
Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi. Ad, açıklama, giriş ve çıkış veri kümeleri ve ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir.

Özellikler hello hello faaliyete hello typeProperties bölümünde kullanılabilir diğer yandan farklılık ile her etkinlik türü. Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.

**AzureTableSource** aşağıdaki özelliklere typeProperties bölümdeki hello destekler:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| azureTableSourceQuery |Merhaba özel sorgu tooread verileri kullanın. |Azure tablo sorgu dizesi. Merhaba sonraki bölümdeki örneklere bakın. |Hayır. Bir tableName bir azureTableSourceQuery belirtildiğinde, tüm hello tablosundan kopyalanan toohello hedef kayıtlarıdır. Bir azureTableSourceQuery de belirtilirse hello sorguyu karşılayan hello tablosundan kopyalanan toohello hedef kayıtlarıdır. |
| azureTableSourceIgnoreTableNotFound |Tablonun swallow hello özel durum var olup olmadığını gösterir. |TRUE<br/>FALSE |Hayır |

### <a name="azuretablesourcequery-examples"></a>azureTableSourceQuery örnekleri
Azure tablo sütunu dize türü ise:

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

Azure tablo sütunu datetime türü ise:

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

**AzureTableSink** aşağıdaki özelliklere typeProperties bölümdeki hello destekler:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| azureTableDefaultPartitionKeyValue |Merhaba havuzu tarafından kullanılan varsayılan bölüm anahtar değeri. |Bir dize değeri. |Hayır |
| azureTablePartitionKeyName |Değerleri bölüm anahtarları olarak kullanılan hello sütunun adını belirtin. Belirtilmezse, AzureTableDefaultPartitionKeyValue hello bölüm anahtarı olarak kullanılır. |Sütun adı. |Hayır |
| azureTableRowKeyName |Sütun değerleri satır anahtarı olarak kullanılan hello sütunun adını belirtin. Belirtilmezse, her satır için bir GUID kullanın. |Sütun adı. |Hayır |
| azureTableInsertType |başlangıç modu tooinsert verileri Azure tablosuna.<br/><br/>Bu özellik, varolan satırlardan eşleşen bölüm ve satır anahtarlarla hello çıkış tablodaki birleştirilmiş veya değiştirilmesi değerlerine sahip olup olmadığını denetler. <br/><br/>Bu ayarların (birleştirme ve değiştirme) nasıl çalıştığını, ilgili toolearn bkz [ekleme veya birleştirme varlık](https://msdn.microsoft.com/library/azure/hh452241.aspx) ve [ekleme veya değiştirme varlık](https://msdn.microsoft.com/library/azure/hh452242.aspx) konuları. <br/><br> Hello satır düzeyinde, hello tablo düzeyinde değil, bu ayar uygulanır ve her iki seçenek hello giriş yok hello çıkış tablosundaki satırları siler. |Merge (varsayılan)<br/>Değiştir |Hayır |
| writeBatchSize |Merhaba writeBatchSize veya writeBatchTimeout gelindiğinde veri hello Azure tablo ekler. |Tamsayı (satır sayısı) |Hayır (varsayılan: 10000) |
| writeBatchTimeout |Merhaba writeBatchSize veya writeBatchTimeout gelindiğinde veri hello Azure tablo ekler. |TimeSpan<br/><br/>Örnek: "00: 20:00" (20 dakika) |Hayır (varsayılan toostorage istemci varsayılan zaman aşımı değeri 90 saniye) |

### <a name="azuretablepartitionkeyname"></a>azureTablePartitionKeyName
Merhaba hedef sütun azureTablePartitionKeyName hello olarak kullanabilmeniz için önce hello Çeviricisi JSON özelliğini kullanarak bir kaynak sütun tooa hedef sütun eşleyin.

Aşağıdaki örneğine hello kaynak sütunu DivisionID eşlenen toohello hedef sütundur: DivisionID.  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
Merhaba DivisionID hello bölüm anahtarı olarak belirtilir.

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a>JSON örnekleri
Merhaba aşağıdaki örneklerde sağlayan örnek JSON tanımları toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Bunlar Göster nasıl toocopy veri tooand Azure Table Storage ve Azure Blob veritabanı. Ancak, veriler kopyalanabilir **doğrudan** herhangi birinden hello kaynakları tooany desteklenen hello havuzlarını biri. Daha fazla bilgi için hello "desteklenen veri depoları ve biçimleri" bölümüne bakın [Kopyala etkinliğini kullanarak veri taşıma](data-factory-data-movement-activities.md).

## <a name="example-copy-data-from-azure-table-tooazure-blob"></a>Örnek: Verilerini Azure Table tooAzure Blob
Merhaba, aşağıdaki örnek gösterilmektedir:

1. Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (Tablo & blob için kullanılır).
2. Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureTable](#dataset-properties).
3. Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Merhaba [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [AzureTableSource](#activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Merhaba örnek bir Azure Table tooa blob toohello varsayılan bölümünde saatte ait verileri kopyalar. Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.

**Azure depolama bağlı hizmeti:**

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
Azure Data Factory iki tür Azure Storage bağlı hizmeti destekler: **AzureStorage** ve **AzureStorageSas**. İçin birinci Merhaba, hello hesap anahtarı içeren hello bağlantı dizesini belirtin ve hello daha ileri bir hello paylaşılan erişim imzası (SAS) URI belirtin. Bkz: [bağlı hizmetler](#linked-service-properties) ayrıntıları bölümü.  

**Azure Tablo girdi veri kümesi:**

Merhaba örnek Azure tablosunda tablo "MyTable" oluşturdunuz varsayılır.

"Dış" ayarı: "true" bildirir hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.

```JSON
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

**AzureTableSource ve BlobSink ardışık düzeninde etkinlik kopyalayın:**

Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**AzureTableSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**. Merhaba SQL sorgusu ile belirtilen **AzureTableSourceQuery** özelliği her saat toocopy hello varsayılan bölümünden hello veri seçer.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "AzureTabletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                      {
                        "name": "AzureTableInput"
                    }
                ],
                "outputs": [
                      {
                            "name": "AzureBlobOutput"
                      }
                ],
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
            }
         ]    
    }
}
```

## <a name="example-copy-data-from-azure-blob-tooazure-table"></a>Örnek: Kopyalama verileri Azure Blob tooAzure tablosu
Merhaba, aşağıdaki örnek gösterilmektedir:

1. Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (Tablo & blob için kullanılır)
2. Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
3. Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureTable](#dataset-properties).
4. Merhaba [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) ve [AzureTableSink](#copy-activity-properties).

Merhaba örnek time series verilerini saatlik bir Azure blob tooan Azure tablosuna kopyalar. Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.

**(İçin Azure Table & Blob) azure depolama bağlı hizmeti:**

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

Azure Data Factory iki tür Azure Storage bağlı hizmeti destekler: **AzureStorage** ve **AzureStorageSas**. İçin birinci Merhaba, hello hesap anahtarı içeren hello bağlantı dizesini belirtin ve hello daha ileri bir hello paylaşılan erişim imzası (SAS) URI belirtin. Bkz: [bağlı hizmetler](#linked-service-properties) ayrıntıları bölümü.

**Azure Blob girdi veri kümesi:**

Veri toplanma yeni blob üzerinden saatte (sıklığı: saat, aralığı: 1). Merhaba klasör yolu ve dosya adını hello blob dinamik olarak değerlendirilir işleniyor hello dilimin hello başlangıç zamanı temel alınarak. Merhaba klasör yolu yıl, ay ve gün kısmını hello başlangıç saati ve dosya adı hello başlangıç saati hello saat bölümünü kullanır. "dış": "true" ayarı bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil hello Data Factory hizmetinin sizi bilgilendirir.

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

**Azure tablo çıkış dataset:**

Merhaba örnek Azure tablosunda "MyTable" olarak adlandırılan veri tooa tablosuna kopyalar. Bir Azure tablosu ile oluşturma hello Blob CSV dosyası toocontain beklediğiniz gibi hello aynı sayıda sütun. Yeni satırlar toohello tablo saatte eklenir.

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
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

**BlobSource ve AzureTableSink ardışık düzeninde etkinlik kopyalayın:**

Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**BlobSource** ve **havuz** türü olarak ayarlanmış çok**AzureTableSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoTable",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureTableOutput"
          }
        ],
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
      }
      ]
   }
}
```
## <a name="type-mapping-for-azure-table"></a>Tür eşlemesi için Azure tablo
Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopyalama etkinliği gerçekleştiren kaynak türleri toosink türlerinden otomatik tür dönüşümleri iki aşamalı bir yaklaşım aşağıdaki hello ile.

1. Yerel kaynak türleri too.NET türünden Dönüştür
2. .NET türü toonative havuz türünden Dönüştür

Çok & Azure tablodan veri taşırken, aşağıdaki hello [Azure tablo hizmeti tarafından tanımlanan eşlemeler](https://msdn.microsoft.com/library/azure/dd179338.aspx) Azure tablo OData türlerini too.NET türünden ve kullanılır.

| OData veri türü | .NET türü | Ayrıntılar |
| --- | --- | --- |
| Edm.Binary |Byte] |Too64 KB oluşturan bir bayt dizisi. |
| Edm.Boolean |bool |Bir Boole değeri. |
| Edm.DateTime |Tarih saat |Eşgüdümlü Evrensel Saat (UTC) olarak ifade edilen bir 64-bit değeri. Aralık 1 Ocak 1601 gece 12:00 gece ' başlayan DateTime Hello desteklenir (C.E.) UTC. Merhaba Aralık 9999 31 Aralık sona erer. |
| Edm.Double |Çift |Bir 64-bit kayan noktalı değeri. |
| Edm.Guid |GUID |128-bit bir genel benzersiz tanımlayıcısı. |
| Edm.Int32 |Int32 |Bir 32 bit tamsayı. |
| Edm.Int64 |Int64 |64 bitlik bir tamsayı. |
| Edm.String |Dize |UTF-16 kodlu değer. Dize değerlerini too64 KB olabilir. |

### <a name="type-conversion-sample"></a>Tür dönüştürme örnek
veri türü dönüşümleri ile Azure Blob tooAzure Tablo kopyalama için örnek aşağıdaki hello olur.

Merhaba Blob dataset CSV biçiminde olduğunu ve üç sütun içeren varsayalım. Bunlardan biri, hello haftanın günü için kısaltılmış Fransızca adları kullanarak bir özel datetime biçimiyle datetime bir sütundur.

Merhaba Blob kaynağı dataset hello sütunlar için tür tanımları birlikte aşağıdaki gibi tanımlayın.

```JSON
{
    "name": " AzureBlobInput",
    "properties":
    {
         "structure":
          [
                { "name": "userid", "type": "Int64"},
                { "name": "name", "type": "String"},
                { "name": "lastlogindate", "type": "Datetime", "culture": "fr-fr", "format": "ddd-MM-YYYY"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "external": true,
        "availability":
        {
            "frequency": "Hour",
            "interval": 1,
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
Merhaba türü eşlemesi Azure tablo OData türü too.NET türünden verildiğinde, şema aşağıdaki hello ile Azure tablosunda hello tablo tanımlarsınız.

**Azure tablo şemasını:**

| Sütun adı | Tür |
| --- | --- |
| Kullanıcı Kimliği |Edm.Int64 |
| ad |Edm.String |
| lastlogindate |Edm.DateTime |

Ardından, hello Azure Table dataset aşağıdaki gibi tanımlayın. Veri deposu temel hello Hello türü bilgileri önceden belirtildiği toospecify "yapısı" Merhaba türü bilgileri bölümle gerekmez.

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
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

Bu durumda, veri fabrikası dönüşümleri hello Datetime alan verileri Blob tooAzure tablo taşırken hello "fr-fr" kültürü kullanarak hello özel datetime biçimine de dahil olmak üzere otomatik olarak yazın.

> [!NOTE]
> Kaynak veri kümesi toocolumns havuz kümesinden toomap sütunlarından bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Performans ve ayarlama
anahtarı hakkında toolearn Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını, bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md).
