---
title: Azure Data Factory kullanarak SAP HANA aaaMove verilerden | Microsoft Docs
description: "Hakkında bilgi edinin Azure Data Factory kullanarak SAP HANA toomove verileri."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 5cefe4c8ed01ea4e86e02496b2f8a9083d0b949c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a>Veri gelen SAP, HANA Azure Data Factory kullanarak Taşı
Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove verileri bir şirket içi SAP HANA de açıklanmaktadır. Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.

Bir şirket içi SAP HANA veri deposu desteklenen tooany havuz veri deposundan verileri kopyalayabilirsiniz. Verileri bir listesi için desteklenen depoları hello kopyalama etkinliği tarafından havuzlarını hello görür [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo. Veri Fabrikası şu anda destekleyen bir SAP HANA tooother verilerden veri depolar, ancak taşıma yalnızca verileri diğer veriler taşıma tooan SAP HANA depolar için.

## <a name="supported-versions-and-installation"></a>Desteklenen sürümleri ve yükleme
Bu bağlayıcı SAP HANA veritabanına herhangi bir sürümünü destekler. HANA bilgi modeli (gibi Analitik ve hesaplama görünümleri) ve SQL sorgularını kullanarak satır/sütun tablolarından veri kopyalamayı destekler.

tooenable hello bağlantı toohello SAP HANA örneği bileşenleri aşağıdaki hello yükleyin:
- **Veri Yönetimi ağ geçidi**: Data Factory hizmeti destekler tooon içi verilere bağlanma (SAP HANA dahil) depoları bir bileşeni kullanılarak veri yönetimi ağ geçidi çağrılır. Veri Yönetimi ağ geçidi ve hello ağ geçidi, kurmak için adım adım yönergeler hakkında toolearn bkz [şirket içi veri arasında taşıma verilerini depolamak toocloud veri deposu](data-factory-move-data-between-onprem-and-cloud.md) makalesi. SAP HANA Hello bir Azure Iaas sanal makine (VM) barındırılan olsa bile ağ geçidi gereklidir. Merhaba ağ geçidi üzerinde aynı VM hello veri olarak depolamak veya hello ağ geçidi olarak aynı uzunlukta farklı bir VM üzerinde toohello veritabanı bağlanabilir hello yükleyebilirsiniz.
- **SAP HANA ODBC sürücüsü** hello gateway makinesinde. Hello hello SAP HANA ODBC sürücüsü indirebilirsiniz [SAP yazılım İndirme Merkezi](https://support.sap.com/swdc). Arama hello anahtar sözcüğü ile **Windows için SAP HANA İSTEMCİSİ**. 

## <a name="getting-started"></a>Başlarken
Farklı araçlar/API'lerini kullanarak bir şirket içi Cassandra veri deposundan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun. 

- Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**. Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz. 
- Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**. Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için. 

Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:

1. Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.
2. Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi. 
3. Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile. 

Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur. Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.  Bir şirket içi SAP HANA kullanılan toocopy veri Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: Blob SAP HANA tooAzure veri kopyalama](#json-example-copy-data-from-sap-hana-to-azure-blob) bu makalenin. 

Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooan SAP HANA veri deposu olan JSON özellikleri hakkında ayrıntılı bilgi sağlar:

## <a name="linked-service-properties"></a>Bağlantılı hizmet özellikleri
Aşağıdaki tablonun hello bağlantılı hizmetinin JSON öğeleri belirli tooSAP HANA açıklamasını sağlar.

Özellik | Açıklama | İzin verilen değerler | Gerekli
-------- | ----------- | -------------- | --------
sunucu | Hangi hello SAP HANA örneği bulunduğu hello sunucusunun adı. Sunucunuz özelleştirilmiş bir bağlantı noktası kullanıyorsa belirtin `server:port`. | Dize | Evet
authenticationType | Kimlik doğrulama türü. | Dize. "Temel" veya "Windows" | Evet 
kullanıcı adı | Erişim toohello SAP sunucusuna sahip hello kullanıcı adı | Dize | Evet
password | Merhaba kullanıcının parolası. | Dize | Evet
gatewayName | Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi SAP HANA örneğini kullanmanız gerekir. | Dize | Evet
encryptedCredential | şifrelenmiş hello kimlik dizesi. | Dize | Hayır

## <a name="dataset-properties"></a>Veri kümesi özellikleri
Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi. Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.

Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar. Merhaba SAP HANA dataset türü için desteklenen türüne özgü özellikler yok **RelationalTable**. 


## <a name="copy-activity-properties"></a>Etkinlik özellikleri Kopyala
Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi. Ad, açıklama, giriş ve çıkış tabloları gibi özellikleri olan ilkeleri etkinlikleri tüm türleri için kullanılabilir.

Oysa hello kullanılabilen özellikleri **typeProperties** hello etkinlik bölümünü her etkinlik türü ile değişir. Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.

Kopyalama etkinliği kaynağında türü olduğunda **RelationalSource** (içeren SAP HANA), aşağıdaki özelliklere hello typeProperties bölümünde bulunur:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| sorgu | Merhaba SQL sorgu tooread veri hello SAP HANA örneğinden belirtir. | SQL sorgusu. | Evet |

## <a name="json-example-copy-data-from-sap-hana-tooazure-blob"></a>JSON örnek: Blob SAP HANA tooAzure veri kopyalama
Merhaba aşağıdaki örnek örnek JSON tanımları sağlar, toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Bu örnek göstermektedir nasıl bir şirket içi SAP HANA tooan Azure Blob Storage toocopy verileri. Ancak, veriler kopyalanabilir **doğrudan** listelenen hello havuzlarını tooany [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.  

> [!IMPORTANT]
> Bu örnek, JSON parçacıklarını sağlar. Merhaba veri fabrikası oluşturma için yönergeler içermez. Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale adım adım yönergeler için.

Merhaba örnek data factory varlıklarını aşağıdaki hello sahiptir:

1. Bağlı hizmet türü [SapHana](#linked-service-properties).
2. Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Bir giriş [dataset](data-factory-create-datasets.md) türü [RelationalTable](#dataset-properties).
4. Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [RelationalSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Merhaba örnek verileri saatte bir SAP HANA örneği tooan Azure blob kopyalar. Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.

İlk adım olarak, hello veri yönetimi ağ geçidi ayarlayın. Merhaba yönergelerdir hello [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.

### <a name="sap-hana-linked-service"></a>SAP HANA bağlı hizmet
Bu hizmet bağlantıları SAP HANA örneği toohello data factory'nizi bağlı. Merhaba type özelliği çok ayarlamak**SapHana**. Merhaba typeProperties bölüm hello SAP HANA örneği için bağlantı bilgilerini sağlar.

```json
{
    "name": "SapHanaLinkedService",
    "properties":
    {
        "type": "SapHana",
        "typeProperties":
        {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```

### <a name="azure-storage-linked-service"></a>Azure Storage bağlı hizmeti
Bu hizmeti Azure Storage hesabı toohello data factory'nizi bağlı. Merhaba type özelliği çok ayarlamak**AzureStorage**. Merhaba typeProperties bölüm hello Azure depolama hesabı bağlantı bilgilerini sağlar.

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

### <a name="sap-hana-input-dataset"></a>SAP HANA giriş veri kümesi

Bu veri kümesi hello SAP HANA veri kümesini tanımlamaktadır. Merhaba Data Factory veri kümesi hello türü çok ayarlamak**RelationalTable**. Şu anda, SAP HANA veri kümesi için herhangi bir türe özgü özelliği belirtmeyin. Merhaba kopyalama etkinliği tanımı Hello sorguda hangi veri tooread hello SAP HANA örneğinden belirtir. 

Dış özellik tootrue ayarı hello Data Factory hizmetinin bu hello tablosu dış toohello veri fabrikası ve hello veri fabrikasında bir etkinlik tarafından üretilen değil bildirir.

Sıklık ve aralığı özelliklerini hello zamanlama tanımlar. Bu durumda, hello veri hello SAP HANA örneğinden saatlik okunur. 

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="azure-blob-output-dataset"></a>Azure Blob çıktı veri kümesi
Bu veri kümesi hello çıktı Azure Blob dataset tanımlar. Merhaba type özelliği tooAzureBlob ayarlanır. Merhaba typeProperties bölüm hello SAP HANA örneğinden kopyalanan hello verilerinin depolandığı sağlar. Merhaba veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1). hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir. Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/saphana/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a>Kopyalama etkinliği ile kanalı

Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**RelationalSource** (SAP HANA kaynağı için) ve **havuz** türü olarak ayarlanmış çok**BlobSink**. Merhaba belirtilen hello SQL sorgusu **sorgu** özelliği saat toocopy geçmiş hello hello veri seçer.

```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<SQL Query for HANA>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapHanaDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDataSet"
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
                "name": "SapHanaToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```


### <a name="type-mapping-for-sap-hana"></a>SAP HANA türü eşlemesi
Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopyalama etkinliği gerçekleştiren kaynak türleri toosink türlerinden otomatik tür dönüşümleri iki aşamalı bir yaklaşım aşağıdaki hello ile:

1. Yerel kaynak türleri too.NET türünden Dönüştür
2. .NET türü toonative havuz türünden Dönüştür

SAP HANA verilerin taşınması, eşlemeleri aşağıdaki hello SAP HANA türleri too.NET türlerinden kullanılır.

SAP HANA türü | .NET türü temelinde
------------- | ---------------
MİNİ TAMSAYI | Bayt
TAMSAYI | Int16
INT | Int32
BIGINT | Int64
GERÇEK | Tek
ÇİFT | Tek
ONDALIK | Ondalık
BOOLE DEĞERİ | Bayt
VARCHAR | Dize
NVARCHAR | Dize
CLOB | Byte]
ALPHANUM | Dize
BLOB | Byte]
TARİH | Tarih saat
SAAT | TimeSpan
ZAMAN DAMGASI | Tarih saat
SECONDDATE | Tarih saat

## <a name="known-limitations"></a>Bilinen sınırlamaları
SAP HANA veri kopyalama işlemi sırasında birkaç bilinen sınırlamalar vardır:

- NVARCHAR dizeler kesilmiş toomaximum uzunluğu 4000 Unicode karakterler şunlardır:
- SMALLDECIMAL desteklenmiyor
- VARBINARY desteklenmiyor
- Geçerli bir tarih olan 12/1899/30 arasında ile 9999/12/31

## <a name="map-source-toosink-columns"></a>Kaynak toosink sütunları eşleme
Kaynak veri kümesi toocolumns havuz kümesindeki eşleme sütunlarında hakkında toolearn bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>İlişkisel kaynaklardan yinelenebilir okuma
İlişkisel veri depoları veri kopyalama işlemi sırasında Yinelenebilirlik göz tooavoid tutmak istenmeyen sonuçları. Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz. Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz. Bir dilim iki yolla yeniden zaman, aynı veri hello emin toomake nasıl geçtiğinden bağımsız okuma gerekir dilim birçok kez çalıştırın. Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)

## <a name="performance-and-tuning"></a>Performans ve ayarlama
Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.
