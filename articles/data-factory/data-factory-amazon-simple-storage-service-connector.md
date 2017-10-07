---
title: "Veri Fabrikası kullanarak aaaMove verilerden Amazon basit depolama hizmeti | Microsoft Docs"
description: "Hakkında bilgi edinin Azure Data Factory kullanarak toomove verilerden Amazon Basit Depolama Birimi Hizmeti (S3)."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 636d3179-eba8-4841-bcb4-3563f6822a26
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8a8cd2845fd1de74413bd0372f3aabfb4817549b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a>Azure Data Factory kullanarak Amazon Basit Depolama hizmetinden veri taşıma
Bu makalede nasıl toouse hello kopyalama etkinliği Azure Data Factory toomove verileri Amazon Basit Depolama hizmetinden (S3) açıklanmaktadır. Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.

Verileri Amazon S3 desteklenen tooany havuz veri deposundan kopyalayabilirsiniz. Verileri bir listesi için desteklenen depoları hello kopyalama etkinliği tarafından havuzlarını hello görür [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo. Veri Fabrikası şu anda yalnızca taşıma verileri Amazon S3 tooother veri depolarını destekler, ancak verileri diğer veriler taşıma değil tooAmazon S3 depolar.

## <a name="required-permissions"></a>Gerekli izinler
Amazon S3 toocopy verilerden hello aşağıdaki izinleri verilmiş olan emin olun:

* `s3:GetObject`ve `s3:GetObjectVersion` Amazon S3 nesne işlemleri için.
* `s3:ListBucket`Amazon S3 Demetini işlemleri için. Merhaba Data Factory Kopyalama Sihirbazı, kullanıyorsanız `s3:ListAllMyBuckets` de gereklidir.

Amazon S3 izinleri hello tam listesi hakkında daha fazla ayrıntı için bkz: [belirleyen izinleri bir ilke](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).

## <a name="getting-started"></a>Başlarken
Farklı araçlar veya API'lerini kullanarak bir Amazon S3 kaynaktan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.

Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**. Hızlı bir kılavuz için bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md).

Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**. Adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için bkz: Merhaba [kopyalama etkinliği Öğreticisi](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

Araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:

1. Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.
2. Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.
3. Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.

Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur. Araçları veya API'ler (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın. Merhaba kullanılan toocopy verileri Amazon S3 veri deposundan Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz [JSON örnek: Blob Amazon S3 tooAzure veri kopyalama](#json-example-copy-data-from-amazon-s3-to-azure-blob) bu makalenin.

> [!NOTE]
> Kopyalama etkinliği için desteklenen dosya ve sıkıştırma biçimleri hakkında daha fazla ayrıntı için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md).

Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooAmazon S3 JSON özellikleri hakkında ayrıntılı bilgiler sağlar.

## <a name="linked-service-properties"></a>Bağlantılı hizmet özellikleri
Bağlı hizmet, bir veri deposu tooa veri fabrikası bağlar. Bağlı hizmet türü oluşturma **AwsAccessKey** toolink Amazon S3 verilerinizi depolamak tooyour veri fabrikası. Aşağıdaki tablonun hello bağlı açıklamasını JSON öğeleri belirli tooAmazon S3 (AwsAccessKey) hizmeti sağlar.

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| accessKeyID |Merhaba gizli erişim anahtarı kimliği. |Dize |Evet |
| secretAccessKey |Merhaba gizli erişim anahtarı kendisi. |Şifrelenmiş gizli dize |Evet |

Örnek aşağıda verilmiştir:

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

## <a name="dataset-properties"></a>Veri kümesi özellikleri
toospecify dataset toorepresent giriş verileri Azure Blob storage'da kümesi hello type özelliği hello kümesinin çok**AmazonS3**. Set hello **linkedServiceName** hello dataset toohello adının hello Amazon S3 özelliği bağlı hizmeti. Bölümleri ve veri kümelerini tanımlamak için kullanılabilen özellikleri tam listesi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md). 

Bölümler yapısı, kullanılabilirlik ve ilke gibi tüm veri türleri (örneğin, SQL database, Azure blob ve Azure tablo) benzer. Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar. Merhaba **typeProperties** bir veri kümesi için bir bölüm türü **AmazonS3** (Merhaba Amazon S3 dataset içerir) hello aşağıdaki özelliklere sahiptir:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| bucketName |Merhaba S3 demetini adı. |Dize |Evet |
| anahtar |Merhaba S3 nesne anahtarı. |Dize |Hayır |
| önek |Merhaba S3 nesne anahtarı için önek. Seçilen nesneler, anahtarları Bu önek ile başlatın. Yalnızca anahtar boş olduğunda geçerlidir. |Dize |Hayır |
| Sürüm |Merhaba S3 nesnesinin S3 sürüm etkinleştirilirse Hello sürümü. |Dize |Hayır |
| Biçimi | şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set hello **türü** biçimi tooone şu değerlerden biri altında özellik. Merhaba daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [JSON biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi ](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler. <br><br> Toocopy dosyaları olarak istiyorsanız-dosya tabanlı depolar (ikili kopya), her iki girdi ve çıktı veri kümesi tanımları Atla hello biçimi bölümünde arasındadır. |Hayır | |
| Sıkıştırma | Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin. desteklenen hello türleri şunlardır: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**. desteklenen hello düzeyleri şunlardır: **Optimal** ve **en hızlı**. Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support). |Hayır | |


> [!NOTE]
> **bucketName + tuşu** hello S3 nesnesinin burada demet hello S3 nesneleri için kök kapsayıcı ve anahtarıdır hello tam yol toohello S3 nesnesini hello konumunu belirtir.

### <a name="sample-dataset-with-prefix"></a>Örnek veri kümesi önekiyle

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "testbucket",
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
### <a name="sample-dataset-with-version"></a>Örnek veri kümesi (sürümüyle)

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "testbucket",
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

### <a name="dynamic-paths-for-s3"></a>S3 için dinamik yollar
Merhaba önceki örnek sabit değerleri Merhaba kullanır **anahtar** ve **bucketName** hello Amazon S3 dataset özelliklerinde.

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

Veri Fabrikası SliceStart gibi sistem değişkenleri kullanarak çalışma zamanında dinamik olarak bu özellikleri hesaplama olabilir.

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

Yapabileceğiniz aynı Merhaba hello **önek** bir Amazon S3 dataset özelliğinin. Desteklenen işlevleri ve değişkenler listesi için bkz: [Data Factory işlevler ve sistem değişkenleri](data-factory-functions-variables.md).

## <a name="copy-activity-properties"></a>Etkinlik özellikleri Kopyala
Bölümleri ve etkinlikleri tanımlamak için kullanılabilen özellikleri tam listesi için bkz: [ardışık düzen oluşturma](data-factory-create-pipelines.md). Ad, açıklama, giriş ve çıkış tabloları ve ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir. Hello kullanılabilen özellikleri **typeProperties** hello etkinlik bölümünü her etkinlik türü ile değişir. Merhaba kopya etkinliği için özellikler hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir. Merhaba kopyalama etkinliğinde bir kaynak türü olduğunda **FileSystemSource** (içeren Amazon S3), özellik aşağıdaki hello sağlanmıştır **typeProperties** bölümü:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| Özyinelemeli |Toorecursively listesi S3 hello dizini altında nesneleri olup olmadığını belirtir. |true/false |Hayır |

## <a name="json-example-copy-data-from-amazon-s3-tooazure-blob-storage"></a>JSON örnek: Amazon S3 tooAzure Blob Depolama veri kopyalama
Bu örnek göstermektedir nasıl toocopy verileri Amazon S3 tooan Azure Blob Depolama. Ancak, verileri doğrudan çok kopyalanabilir[desteklenen hello havuzlarını hiçbirini](data-factory-data-movement-activities.md#supported-data-stores-and-formats) veri fabrikasında hello kopyalama etkinliği kullanarak.

Merhaba örnek Data Factory varlıklarını aşağıdaki hello için JSON tanımları sağlar. Hello kullanarak bu tanımları toocreate Amazon S3 tooBlob depolama, ardışık düzen toocopy verilerden kullanabileceğiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), veya [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).   

* Bağlı hizmet türü [AwsAccessKey](#linked-service-properties).
* Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Bir giriş [dataset](data-factory-create-datasets.md) türü [AmazonS3](#dataset-properties).
* Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [FileSystemSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Merhaba örnek verileri Amazon S3 tooan Azure blob ' saatte kopyalar. Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.

### <a name="amazon-s3-linked-service"></a>Amazon S3 bağlı hizmet

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

### <a name="azure-storage-linked-service"></a>Azure Storage bağlı hizmeti

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

### <a name="amazon-s3-input-dataset"></a>Amazon S3 girdi veri kümesi

Ayarı **"dış": true** hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olduğunu bildirir. Bu özellik tootrue hello ardışık düzeninde bir etkinlik tarafından üretilen olmayan bir girdi veri kümesi ayarlayın.

```json
    {
        "name": "AmazonS3InputDataset",
        "properties": {
            "type": "AmazonS3",
            "linkedServiceName": "AmazonS3LinkedService",
            "typeProperties": {
                "key": "testFolder/test.orc",
                "bucketName": "testbucket",
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


### <a name="azure-blob-output-dataset"></a>Azure Blob çıktı veri kümesi

Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1). hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir. Merhaba klasör yolu hello yıl, ay, gün ve saat bölümlerini hello başlangıç saatini kullanır.

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazons3/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a>Bir Amazon S3 kaynak ve blob havuz sahip işlem hattı kopyalama etkinliği

Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**FileSystemSource**, ve **havuz** türü olarak ayarlanmış çok**BlobSink**.

```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
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
                "inputs": [
                    {
                        "name": "AmazonS3InputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AmazonS3ToBlob"
            }
        ],
        "start": "2014-08-08T18:00:00Z",
        "end": "2014-08-08T19:00:00Z"
    }
}
```
> [!NOTE]
> Kaynak veri kümesi toocolumns bir havuz veri kümesinden toomap sütunlarından bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).


## <a name="next-steps"></a>Sonraki adımlar
Aşağıdaki makaleleri hello bakın:

* anahtarı hakkında toolearn Etkenler etkisi performans veri fabrikasında (kopyalama etkinliği) veri hareketlerini ve çeşitli yolları toooptimize, hello bkz [kopyalama etkinliği performans ve ayarlama Kılavuzu](data-factory-copy-activity-performance.md).

* Kopyalama etkinliği ile işlem hattı oluşturmak için adım adım yönergeler için bkz: Merhaba [kopyalama etkinliği Öğreticisi](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
