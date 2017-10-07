---
title: / Azure Cosmos DB aaaMove verileri | Microsoft Docs
description: "Bilgi nasıl veri taşıma/Azure Data Factory kullanarak Azure Cosmos DB koleksiyonundan"
services: data-factory, cosmosdb
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c9297b71-1bb4-4b29-ba3c-4cf1f5575fac
ms.service: multiple
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: bd23ce4e004a972ce6f3e4165cfdea4f0c18fecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-cosmos-db-using-azure-data-factory"></a>Azure Cosmos Azure Data Factory kullanarak Veritabanından veri tooand Taşı
Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove veri öğesine/öğesinden Azure Cosmos DB (DocumentDB API) açıklanmaktadır. Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar. 

Veri tooAzure Cosmos DB depolamak veya Azure Cosmos DB desteklenen tooany havuz verileri depolamak istediğiniz desteklenen kaynağından veri kopyalayabilirsiniz. Merhaba kaynakları veya havuzlarını olarak hello kopyalama etkinliği tarafından desteklenen veri depoları listesi için bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo. 

> [!IMPORTANT]
> Azure Cosmos DB Bağlayıcısı yalnızca DocumentDB API destekler.

toocopy verileri olarak-olduğu için/JSON dosyalarında veya başka bir Cosmos DB koleksiyonu bkz [içeri/dışarı aktarma JSON belgeleri](#importexport-json-documents).

## <a name="getting-started"></a>Başlarken
Farklı araçlar/API'lerini kullanarak verileri öğesine/öğesinden Azure Cosmos DB taşır kopyalama etkinliği ile işlem hattı oluşturun.

Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**. Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.

Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**. Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için. 

Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin: 

1. Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.
2. Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi. 
3. Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile. 

Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur. Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.  / Cosmos DB kullanılan toocopy verileri olan Data Factory varlıkları için JSON tanımlarıyla örnekleri için bkz: [JSON örnekler](#json-examples) bu makalenin. 

Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooCosmos DB olan JSON özellikleri hakkında ayrıntılı bilgi sağlar: 

## <a name="linked-service-properties"></a>Bağlantılı hizmet özellikleri
Aşağıdaki tablonun hello JSON öğeleri belirli tooAzure Cosmos DB bağlantılı hizmeti için bir açıklama sağlar.

| **Özellik** | **Açıklama** | **Gerekli** |
| --- | --- | --- |
| type |Merhaba type özelliği ayarlanmalıdır: **DocumentDb** |Evet |
| connectionString |Gerekli bilgiler tooconnect tooAzure Cosmos DB veritabanı belirtin. |Evet |

Örnek:

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```

## <a name="dataset-properties"></a>Veri kümesi özellikleri
Bölümler & özellikleri veri kümeleri tanımlamak için kullanılabilir tam bir listesi için lütfen toohello bakın [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi. Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.

Merhaba typeProperties bölümü veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar. Merhaba typeProperties bölüm türü hello veri kümesi için **DocumentDbCollection** hello aşağıdaki özelliklere sahiptir.

| **Özellik** | **Açıklama** | **Gerekli** |
| --- | --- | --- |
| collectionName |Merhaba Cosmos DB belge koleksiyonu adı. |Evet |

Örnek:

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
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
### <a name="schema-by-data-factory"></a>Şema tarafından veri fabrikası
Azure Cosmos DB gibi şemasız veri depoları için hello Data Factory hizmetinin yolları aşağıdaki hello birinde hello şema oluşturur:  

1. Hello kullanarak verilerin hello yapısını belirtirseniz **yapısı** hello veri kümesi tanımında hello Data Factory hizmeti özelliği bu yapısı hello şema olarak geliştirir. Bir satır bir sütun için bir değer içermiyorsa, bu durumda, boş bir değer için sağlanır.
2. Hello kullanarak verilerin hello yapısını belirtmezseniz, **yapısı** hello veri kümesi tanımında hello Data Factory hizmeti özellik hello verilerde hello ilk satırını kullanarak hello şema oluşturur. Merhaba ilk satır hello tam şema içermiyorsa, bu durumda, bazı sütunları hello kopyalama işlemi sonucunda eksilir.

Bu nedenle, şemasız veri kaynakları için hello en iyi uygulama toospecify hello hello kullanarak veri yapısıdır **yapısı** özelliği.

## <a name="copy-activity-properties"></a>Etkinlik özellikleri Kopyala
Bölümler & özellikleri etkinlikleri tanımlamak için kullanılabilir tam bir listesi için lütfen toohello bakın [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi. Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.

> [!NOTE]
> Merhaba kopyalama etkinliği yalnızca bir girdi alır ve tek bir çıktı üretir.

Özellikler hello hello faaliyete hello typeProperties bölümünde kullanılabilir diğer yandan farklılık hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık kopyalama etkinliği durumunda her etkinlik türü ile.

Kaynak türü olduğunda kopyalama etkinliği durumunda **DocumentDbCollectionSource** aşağıdaki özelliklere hello kullanılabilir **typeProperties** bölümü:

| **Özellik** | **Açıklama** | **İzin verilen değerler** | **Gerekli** |
| --- | --- | --- | --- |
| sorgu |Merhaba sorgu tooread verileri belirtin. |Sorgu dizesindeki Azure Cosmos DB tarafından desteklenir. <br/><br/>Örnek:`SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"` |Hayır <br/><br/>Belirtilmezse, yürütülen SQL deyimini hello:`select <columns defined in structure> from mycollection` |
| nestingSeparator |Belge hello özel karakter tooindicate iç içe geçmiş |Herhangi bir karakter. <br/><br/>Azure Cosmos DB iç içe geçmiş yapılar burada izin verilen bir NoSQL JSON belgeleri için deposudur. Azure Data Factory sağlayan kullanıcı toodenote hiyerarşisi olan nestingSeparator aracılığıyla "." Yukarıdaki örneklerde Hello. Merhaba ayırıcı ile üç alt öğeleri olan hello "Ad" nesne hello kopyalama etkinliği oluşturacaktır ilk, Orta ve son, according too"Name.First", "Name.Middle" ve "Name.Last" hello, tablo tanımı. |Hayır |

**DocumentDbCollectionSink** aşağıdaki özelliklere hello destekler:

| **Özellik** | **Açıklama** | **İzin verilen değerler** | **Gerekli** |
| --- | --- | --- | --- |
| nestingSeparator |Bir özel karakter belge iç içe geçmiş hello kaynak sütun adı tooindicate gereklidir. <br/><br/>Örneğin yukarıdaki: `Name.First` hello çıktısında JSON yapısındaki hello Cosmos DB belgede aşağıdaki hello tablo oluşturur:<br/><br/>"Name": {<br/>    "İlk": "John"<br/>}, |Kullanılan tooseparate iç içe geçme düzeyi karakter.<br/><br/>Varsayılan değer `.` (nokta). |Kullanılan tooseparate iç içe geçme düzeyi karakter. <br/><br/>Varsayılan değer `.` (nokta). |
| writeBatchSize |TooAzure Cosmos DB hizmet toocreate belgeleri istekleri paralel sayısı.<br/><br/>Bu özelliği kullanarak verileri için/Cosmos DB kopyalama işlemi sırasında hello performans ince ayar yapabilirsiniz. Daha fazla paralel istekler tooCosmos DB gönderildiğinden writeBatchSize artırdığınızda daha iyi bir performans düşüklüğü görebilir. Ancak, azaltma tooavoid gerekir hello hata iletisi atabilirsiniz: "oranıdır büyük istek".<br/><br/>Azaltmayı bir dizi etkene, belgeler, belgeleri koşullarını sayısı boyutunu dahil olmak üzere, hedef koleksiyon, vb. İlkesi dizin tarafından belirlenir. Kopyalama işlemleri için daha iyi bir koleksiyon (ör S3) toohave hello çoğu üretilen iş kullanabilirsiniz (2.500 istek birimleri/saniye). |Tamsayı |Hayır (varsayılan: 5) |
| writeBatchTimeout |Zaman aşımına uğramadan önce hello işlemi toocomplete bir süre bekleyin. |TimeSpan<br/><br/> Örnek: "00: 30:00" (30 dakika). |Hayır |

## <a name="importexport-json-documents"></a>İçeri/dışarı aktarma JSON belgeleri
Bu Cosmos DB Bağlayıcısı'nı kullanarak kolayca yapabilecekleriniz

* JSON belgeleri Cosmos DB, Azure Blob, Azure Data Lake, şirket içi dosya sistemi veya Azure Data Factory ile desteklenen diğer dosya tabanlı depoları gibi çeşitli kaynaklardan aktarın.
* JSON belgeleri Cosmos DB collecton çeşitli dosya tabanlı depoları verin.
* İki Cosmos DB koleksiyon olarak arasında veri geçirme-değil.

Bu tür şema belirsiz tooachieve kopyalama 
* Kopyalama Sihirbazı'nı kullanırken hello denetleyin **"dışa-tooJSON dosyaları ya da Cosmos DB koleksiyonu"** seçeneği.
* Ne zaman, JSON düzenleme kullanarak belirlemezseniz hello "yapısı" bölümü Cosmos DB veri kümeleri içinde ya da "nestingSeparator" özelliği Cosmos DB kaynak/havuz kopyalama etkinliği. gelen tooimport / tooJSON dosyaları dışarı aktarma, hello dosya depolama kümesinde "JsonFormat", yapılandırma "filePattern" biçim türünü belirtin ve hello rest biçim ayarlarını Atla bkz [JSON biçimine](data-factory-supported-file-and-compression-formats.md#json-format) ayrıntıları bölümü.

## <a name="json-examples"></a>JSON örnekleri
Merhaba aşağıdaki örneklerde sağlayan örnek JSON tanımları toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Bunlar Göster nasıl toocopy veri tooand Azure Cosmos DB ve Azure Blob Storage. Ancak, veriler kopyalanabilir **doğrudan** herhangi birinden hello kaynakları tooany belirtildiği hello havuzlarını, [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.

## <a name="example-copy-data-from-azure-cosmos-db-tooazure-blob"></a>Örnek: Verilerini Azure Cosmos DB tooAzure Blob
Aşağıdaki Hello örneği gösterilmektedir:

1. Bağlı hizmet türü [DocumentDb](#linked-service-properties).
2. Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Bir giriş [dataset](data-factory-create-datasets.md) türü [DocumentDbCollection](#dataset-properties).
4. Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [DocumentDbCollectionSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Merhaba örnek verileri Azure Cosmos DB tooAzure Blob kopyalar. Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.

**Azure Cosmos bağlı DB hizmeti:**

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
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
**Azure belge DB girdi veri kümesi:**

Merhaba örnek varsayar adlı bir koleksiyon sahip **kişi** Azure Cosmos DB veritabanında.

"Dış" ayarı: "true" ve externalData belirtme hello Azure Data Factory hizmeti hello tablosunun ilkesi bilgileri dış toohello veri fabrikası ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
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

**Azure Blob dataset çıktı:**

Kopyalanan tooa yeni blob hello yoluyla her saat için saat ayrıntı hello belirli datetime yansıtma hello blob verilerdir.

```JSON
{
  "name": "PersonBlobTableOut",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
JSON belgesinde hello Cosmos DB veritabanı kişi koleksiyonunda örnek:

```JSON
{
  "PersonId": 2,
  "Name": {
    "First": "Jane",
    "Middle": "",
    "Last": "Doe"
  }
}
```
Cosmos DB SQL söz dizimi gibi hiyerarşik JSON belgelerini kullanarak belgelerin sorgulanmasını destekler.

Örnek: 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

Merhaba aşağıdaki hello hello Azure Cosmos DB veritabanı tooan Azure blob kişi koleksiyonunda kopya veri kanalı. Merhaba kopyalama etkinliği hello bir parçası olarak giriş ve çıkış veri kümeleri belirtilmedi.  

```JSON
{
  "name": "DocDbToBlobPipeline",
  "properties": {
    "activities": [
      {
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
        "inputs": [
          {
            "name": "PersonCosmosDbTable"
          }
        ],
        "outputs": [
          {
            "name": "PersonBlobTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromDocDbToBlob"
      }
    ],
    "start": "2015-04-01T00:00:00Z",
    "end": "2015-04-02T00:00:00Z"
  }
}
```
## <a name="example-copy-data-from-azure-blob-tooazure-cosmos-db"></a>Örnek: Kopyalama verileri Azure Blob tooAzure Cosmos DB 
Aşağıdaki Hello örneği gösterilmektedir:

1. Bağlı hizmet türü [DocumentDb](#azure-documentdb-linked-service-properties).
2. Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Bir çıkış [dataset](data-factory-create-datasets.md) türü [DocumentDbCollection](#azure-documentdb-dataset-type-properties).
5. A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) ve [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).

Merhaba örnek verileri Azure blob tooAzure Cosmos DB kopyalar. Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.

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
**Azure Cosmos bağlı DB hizmeti:**

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
**Azure Blob girdi veri kümesi:**

```JSON
{
  "name": "PersonBlobTableIn",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "MiddleName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "fileName": "input.csv",
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
**Azure Cosmos DB çıkış dataset:**

Merhaba örnek "Kişi" adlı veri tooa koleksiyon kopyalar.

```JSON
{
  "name": "PersonCosmosDbTableOut",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "Name.First",
        "type": "String"
      },
      {
        "name": "Name.Middle",
        "type": "String"
      },
      {
        "name": "Name.Last",
        "type": "String"
      }
    ],
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
Merhaba aşağıdaki kopya verileri Azure Blob toohello kişi hello Cosmos DB koleksiyonunda kanalı. Merhaba kopyalama etkinliği hello bir parçası olarak giriş ve çıkış veri kümeleri belirtilmedi.

```JSON
{
  "name": "BlobToDocDbPipeline",
  "properties": {
    "activities": [
      {
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
          }
          "translator": {
              "type": "TabularTranslator",
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
          }
        },
        "inputs": [
          {
            "name": "PersonBlobTableIn"
          }
        ],
        "outputs": [
          {
            "name": "PersonCosmosDbTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromBlobToDocDb"
      }
    ],
    "start": "2015-04-14T00:00:00Z",
    "end": "2015-04-15T00:00:00Z"
  }
}
```
Merhaba örnek blob giriş olarak ise

```
1,John,,Doe
```
Ardından hello çıktı Cosmos DB'de JSON olarak olacaktır:

```JSON
{
  "Id": 1,
  "Name": {
    "First": "John",
    "Middle": null,
    "Last": "Doe"
  },
  "id": "a5e8595c-62ec-4554-a118-3940f4ff70b6"
}
```
Azure Cosmos DB iç içe geçmiş yapılar burada izin verilen bir NoSQL JSON belgeleri için deposudur. Azure Data Factory sağlayan kullanıcı toodenote hiyerarşisi aracılığıyla **nestingSeparator**, olduğu "." Bu örnekte. Merhaba ayırıcı ile üç alt öğeleri olan hello "Ad" nesne hello kopyalama etkinliği oluşturacaktır ilk, Orta ve son, according too"Name.First", "Name.Middle" ve "Name.Last" hello, tablo tanımı.

## <a name="appendix"></a>Ek
1. **Soru:** kopyalama etkinliği desteği güncelleştirmesi mevcut kayıtların hello?

    **Yanıt:** No
2. **Soru:** kayıtları kopyalanan nasıl bir kopya tooAzure Cosmos DB anlaşma ile yeniden denemek zaten mu?

    **Yanıt:** kayıtları "ID" alanına sahipseniz ve hello kopyalama işlemi çalışırsa tooinsert hello bir kayıtla aynı kimliği, başlangıç kopyalama işlemi bir hata oluşturur.  
3. **Soru:** Data Factory desteklemiyor [aralığı veya karma tabanlı veri bölümlendirme](../documentdb/documentdb-partition-data.md)?

    **Yanıt:** No
4. **Soru:** bir tablo için birden fazla Azure Cosmos DB koleksiyonu belirtin?

    **Yanıt:** No Şu anda yalnızca bir koleksiyon belirtilebilir.

## <a name="performance-and-tuning"></a>Performans ve ayarlama
Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.
