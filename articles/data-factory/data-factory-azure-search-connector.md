---
title: "Veri Fabrikası kullanarak aaaPush veri tooSearch dizini | Microsoft Docs"
description: "Hakkında bilgi edinin Azure Data Factory kullanarak toopush veri tooAzure arama dizini."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f8d46e1e-5c37-4408-80fb-c54be532a4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: f2d973d0a2c24d6448e2d59e37e24503aa433018
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="push-data-tooan-azure-search-index-by-using-azure-data-factory"></a>Azure Data Factory kullanarak veri tooan Azure Search dizini bildirme
Bu makalede nasıl toouse hello kopyalama etkinliği toopush verileri bir desteklenen kaynak verilerinden tooAzure arama dizini depolamak açıklanmaktadır. Desteklenen kaynak veri depolarına hello Kaynak sütununda hello listelenen [desteklenen kaynakları ve havuzlarını](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo. Bu makale üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) desteklenen veri deposu birleşimleri kopyalama etkinliği ile veri taşıma için genel bir bakış sunan makalesi.

## <a name="enabling-connectivity"></a>Bağlantıyı etkinleştirme
tooallow Data Factory hizmetine bağlanmak tooan şirket içi veri depolama, veri yönetimi ağ geçidi, şirket içi ortamınızda yükleyin. Ağ geçidi üzerinde hello kaynak verilerini barındıran aynı makine depolamak ya da hello veri kaynakları için rekabete ayrı makine tooavoid depolamak hello yükleyebilirsiniz.

Veri Yönetimi ağ geçidi şirket içi veri kaynakları toocloud Hizmetleri güvenli ve yönetilen bir şekilde birbirine bağlayan. Bkz: [şirket içi ve bulut arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale veri yönetimi ağ geçidi hakkında ayrıntılı bilgi için.

## <a name="getting-started"></a>Başlarken
Farklı araçlar/API'lerini kullanarak bir kaynak veri deposu tooAzure arama dizinden veri iter kopyalama etkinliği ile işlem hattı oluşturun.

Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**. Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.

Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**. Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için. 

Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin: 

1. Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.
2. Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi. 
3. Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile. 

Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur. Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.  Kullanılan toocopy veri tooAzure arama dizini olan Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: şirket içi SQL Server tooAzure arama dizinden veri kopyalama](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) bu makalenin. 

Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooAzure arama dizini olan JSON özellikleri hakkında ayrıntılı bilgi sağlar:

## <a name="linked-service-properties"></a>Bağlantılı hizmet özellikleri

Aşağıdaki tablonun hello belirli toohello bağlı Azure Search Hizmeti JSON öğeleri için açıklamalar sağlanır.

| Özellik | Açıklama | Gerekli |
| -------- | ----------- | -------- |
| type | Merhaba type özelliği ayarlanmalıdır: **AzureSearch**. | Evet |
| URL | Hello Azure Search hizmeti için URL. | Evet |
| anahtar | Hello Azure Search hizmeti için yönetici anahtarı. | Evet |

## <a name="dataset-properties"></a>Veri kümesi özellikleri

Merhaba bölümler ve veri kümelerini tanımlamak için kullanılabilir olan özellikleri tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi. Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri kümesi türleri için benzerdir. Merhaba **typeProperties** bölümü, her veri kümesi türü için farklıdır. Merhaba typeProperties bölümünde hello türü veri kümesi için **AzureSearchIndex** hello aşağıdaki özelliklere sahiptir:

| Özellik | Açıklama | Gerekli |
| -------- | ----------- | -------- |
| type | Merhaba type özelliği çok ayarlanmalıdır**AzureSearchIndex**.| Evet |
| indexName | Hello Azure Search dizini adı. Veri Fabrikası hello dizin oluşturmaz. Başlangıç dizini, Azure Search'te mevcut olması gerekir. | Evet |


## <a name="copy-activity-properties"></a>Etkinlik özellikleri Kopyala
Merhaba bölümler ve etkinlikleri tanımlamak için kullanılabilir olan özellikleri tam listesi için bkz [ardışık düzen oluşturma](data-factory-create-pipelines.md) makalesi. Ad, açıklama, giriş ve çıkış tabloları ve çeşitli ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir. Oysa her etkinlik türü ile Merhaba typeProperties bölümündeki özellikler değişir. Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.

Kopyalama hello havuz hello türü olduğunda etkinliği için **AzureSearchIndexSink**, aşağıdaki özelliklere hello typeProperties bölümünde bulunur:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| -------- | ----------- | -------------- | -------- |
| WriteBehavior | Toomerge veya Değiştir bir belgeyi açtığında hello dizinde zaten olup olmadığını belirtir. Merhaba bkz [WriteBehavior özelliği](#writebehavior-property).| Merge (varsayılan)<br/>Karşıya Yükle| Hayır |
| writeBatchSize | Hello arabellek boyutu writeBatchSize ulaştığında hello Azure Search dizinine veri yükler. Merhaba bkz [WriteBatchSize özelliği](#writebatchsize-property) Ayrıntılar için. | 1 too1, 000. Varsayılan değer 1000'dir. | Hayır |

### <a name="writebehavior-property"></a>WriteBehavior özelliği
Verileri yazarken AzureSearchSink upserts. Diğer bir deyişle, hello belge anahtarını hello Azure Search dizini zaten varsa bir belge yazarken, Azure Search çakışma özel durum atma yerine hello var olan bir belgeyi güncelleştirir.

Merhaba AzureSearchSink (AzureSearch SDK kullanılarak) iki upsert davranışları aşağıdaki hello sağlar:

- **Birleştirme**: hello yeni belgedeki tüm hello sütunları bir varolan hello ile birleştirin. Null değer hello yeni belge bulunan sütunlar için var olan bir hello hello değeri korunur.
- **Karşıya yükleme**: hello varolan bir hello yeni belge değiştirir. Bulunup bulunmadığını değeri null olmayan hello mevcut belgede veya hello yeni belgede belirtilmeyen sütunlar için toonull hello değer ayarlanır.

Merhaba varsayılan davranışı **birleştirme**.

### <a name="writebatchsize-property"></a>WriteBatchSize özelliği
Azure Search Hizmeti yazma belgeleri toplu iş olarak destekler. Bir toplu 1 too1, 000 eylemler içerebilir. Bir eylem, bir belge tooperform hello karşıya yükleme/birleştirme işlemi gerçekleştirir.

### <a name="data-type-support"></a>Veri türü desteği
Merhaba aşağıdaki tabloda bir Azure Search veri türü veya desteklenip desteklenmediğini belirtir.

| Azure arama veri türü | Azure arama havuzunda desteklenir |
| ---------------------- | ------------------------------ |
| Dize | E |
| Int32 | E |
| Int64 | E |
| Çift | E |
| Boole değeri | E |
| DataTimeOffset | E |
| Dize dizisi | N |
| GeographyPoint | N |

## <a name="json-example-copy-data-from-on-premises-sql-server-tooazure-search-index"></a>JSON örnek: şirket içi SQL Server tooAzure arama dizinden veri kopyalama

Merhaba, aşağıdaki örnek gösterilmektedir:

1.  Bağlı hizmet türü [AzureSearch](#linked-service-properties).
2.  Bağlı hizmet türü [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).
3.  Bir giriş [dataset](data-factory-create-datasets.md) türü [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).
4.  Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureSearchIndex](#dataset-properties).
4.  A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) ve [AzureSearchIndexSink](#copy-activity-properties).

Merhaba örnek time series verilerini saatlik bir şirket içi SQL Server veritabanı tooan Azure Search dizini kopyalar. Bu örnekte kullanılan JSON özellikleri hello hello örnekleri aşağıdaki bölümlerde açıklanmıştır.

İlk adım olarak, şirket içi makinenizde hello veri yönetimi ağ geçidi ayarlayın. Merhaba yönergelerdir hello [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.

**Azure arama bağlantılı hizmeti:**

```JSON
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

**SQL Server bağlantılı hizmeti**

```JSON
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

**SQL Server girdi veri kümesi**

Merhaba örnek SQL Server'da bir tablo "MyTable" oluşturulur ve zaman serisi veri için "timestampcolumn" adlı bir sütun içerdiği varsayar. Tek bir veri kümesi, ancak tek bir tabloyu kullanarak aynı veritabanı hello veri kümesi'nin tableName typeProperty için kullanılması gereken hello içinde birden çok tablo üzerinde sorgulayabilirsiniz.

"Dış" ayarı: "true" bildirir Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.

```JSON
{
  "name": "SqlServerDataset",
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

**Azure Search'te veri kümesini çıktı:**

Merhaba örnek kopya veri tooan Azure Search dizini adlı **ürünleri**. Veri Fabrikası hello dizin oluşturmaz. tootest hello örnek, bu ada sahip bir dizin oluşturun. Hello Azure Search dizini oluşturma hello ile aynı sayıda sütun olduğu gibi hello girdi veri kümesi. Yeni girişler toohello Azure Search dizini saatte eklenir.

```JSON
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties" : {
            "indexName": "products",
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
   }
}
```

**SQL kaynak ve Azure Search dizini havuz ile ardışık düzeninde etkinlik kopyalayın:**

Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**SqlSource** ve **havuz** türü olarak ayarlanmış çok**AzureSearchIndexSink**. Merhaba belirtilen hello SQL sorgusu **SqlReaderQuery** özelliği saat toocopy geçmiş hello hello veri seçer.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoAzureSearchIndex",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSearchIndexDataset"
          }
        ],
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
      }
     ]
   }
}
```

Azure Search bir bulut veri deposundan veri kopyalıyorsanız `executionLocation` özelliği gereklidir. Merhaba aşağıdaki JSON parçacığı gösterir kopyalama etkinliği altında gerekli hello değişiklik `typeProperties` bir örnek olarak. Denetleme [bulut veri depoları arasında veri kopyalama](data-factory-data-movement-activities.md#global) desteklenen değerler ve daha fazla ayrıntı için bölüm.

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```


## <a name="copy-from-a-cloud-source"></a>Bir bulut kaynaktan kopyalama
Azure Search bir bulut veri deposundan veri kopyalıyorsanız `executionLocation` özelliği gereklidir. Merhaba aşağıdaki JSON parçacığı gösterir kopyalama etkinliği altında gerekli hello değişiklik `typeProperties` bir örnek olarak. Denetleme [bulut veri depoları arasında veri kopyalama](data-factory-data-movement-activities.md#global) desteklenen değerler ve daha fazla ayrıntı için bölüm.

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```

Ayrıca, kaynak veri kümesi toocolumns hello kopyalama etkinliği tanımında havuz kümesinden sütunlarından eşleyebilirsiniz. Ayrıntılar için bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Performans ve ayar  
Merhaba bkz [kopyalama etkinliği performans ve ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler veri taşıma (kopyalama etkinliği), o etki performansını ve çeşitli yolları toooptimize onu.

## <a name="next-steps"></a>Sonraki adımlar
Aşağıdaki makaleleri hello bakın:

* [Kopya etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) kopyalama etkinliği ile işlem hattı oluşturmak için adım adım yönergeler için.
