---
title: OData kaynaklardan aaaMove veri | Microsoft Docs
description: "Azure Data Factory kullanarak OData toomove verileri nasıl kaynakları hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: de28fa56-3204-4546-a4df-21a21de43ed7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 328efe4fd274fb3e54c1d2f209e4614c77c1ff37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-odata-source-using-azure-data-factory"></a>Verileri Azure Data Factory kullanarak gelen bir OData kaynağı taşıma
Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove veri bir OData kaynaktan açıklanmaktadır. Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.

Bir OData kaynağı desteklenen tooany havuz veri deposundan verileri kopyalayabilirsiniz. Verileri bir listesi için desteklenen depoları hello kopyalama etkinliği tarafından havuzlarını hello görür [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo. Veri Fabrikası şu anda destekleyen bir OData kaynak tooother verilerden veri depolar, ancak taşıma yalnızca verileri diğer veriler taşıma tooan OData kaynağı depolar için. 

## <a name="supported-versions-and-authentication-types"></a>Desteklenen sürümler ve kimlik doğrulama türleri
Bu OData bağlayıcısını destekleyen OData sürüm 3.0 ve 4.0 ve hem bulut OData verilerden ve şirket içi OData kaynaklarına kopyalayabilirsiniz. İkinci Hello için tooinstall hello veri yönetimi ağ geçidi gerekir. Bkz: [şirket içi ve bulut arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale veri yönetimi ağ geçidi hakkında ayrıntılı bilgi için.

Kimlik doğrulama türleri desteklenir:

* tooaccess **bulut** OData akışı, kullanabileceğiniz anonim, temel (kullanıcı adı ve parola) veya Azure Active Directory tabanlı OAuth kimlik doğrulaması.
* tooaccess **şirket içi** OData akışı, kullanabileceğiniz anonim, temel (kullanıcı adı ve parola) veya Windows kimlik doğrulaması.

## <a name="getting-started"></a>Başlarken
Farklı araçlar/API'lerini kullanarak bir OData kaynaktan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.

Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**. Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.

Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**. Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için. 

Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin: 

1. Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.
2. Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi. 
3. Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile. 

Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur. Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.  Bir OData kaynaktan kullanılan toocopy verileri Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: OData kaynak tooAzure Blob veri kopyalama](#json-example-copy-data-from-odata-source-to-azure-blob) bu makalenin. 

Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooOData kaynağı JSON özellikleri hakkında ayrıntılı bilgi sağlar:

## <a name="linked-service-properties"></a>Bağlantılı hizmet özellikleri
Aşağıdaki tablonun hello JSON öğeleri belirli tooOData bağlantılı hizmeti için bir açıklama sağlar.

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| type |Merhaba type özelliği ayarlanmalıdır: **OData** |Evet |
| URL |Merhaba OData hizmeti URL'si. |Evet |
| authenticationType |Kimlik doğrulama türü tooconnect toohello OData kaynağı kullanılır. <br/><br/> OData bulut için olası değerler şunlardır anonim, temel ve OAuth (Not OAuth Azure Active Directory tabanlı şu anda yalnızca Azure Data Factory destek). <br/><br/> Anonim, temel ve Windows, şirket içi OData için olası değerler şunlardır. |Evet |
| kullanıcı adı |Temel kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin. |Evet (yalnızca temel kimlik doğrulaması kullanıyorsanız) |
| password |Merhaba username için belirtilen hello kullanıcı hesabı için parola belirtin. |Evet (yalnızca temel kimlik doğrulaması kullanıyorsanız) |
| authorizedCredential |OAuth kullanıyorsanız **Authorize** hello Data Factory Kopyalama Sihirbazı veya Düzenleyicisi'nde düğmesine tıklayın ve sonra bu özellik başlangıç değeri otomatik olarak oluşturulan kimlik bilgilerinizi girin. |Evet (yalnızca OAuth kimlik doğrulaması kullanıyorsanız) |
| gatewayName |Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi OData hizmeti kullanmanız gerekir. Yalnızca şirket içi OData kaynak sunucudan kopyaladığınız verileri belirtin. |Hayır |

### <a name="using-basic-authentication"></a>Temel kimlik doğrulaması kullanma
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a>Anonim kimlik doğrulamasını kullanma
```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
        "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

### <a name="using-windows-authentication-accessing-on-premises-odata-source"></a>Şirket içi OData kaynağına erişme Windows kimlik doğrulaması kullanma
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of on-premises OData source e.g. Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-oauth-authentication-accessing-cloud-odata-source"></a>OAuth kimlik doğrulaması erişen bulut OData kaynağı kullanma
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source e.g. https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

## <a name="dataset-properties"></a>Veri kümesi özellikleri
Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi. Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.

Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar. Merhaba typeProperties bölüm türü veri kümesi için **ODataResource** hello aşağıdaki özelliklere sahip (OData veri kümesi içerir)

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| Yol |Yol toohello OData kaynak |Hayır |

## <a name="copy-activity-properties"></a>Etkinlik özellikleri Kopyala
Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi. Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.

Özellikler hello hello faaliyete hello typeProperties bölümünde kullanılabilir diğer yandan farklılık ile her etkinlik türü. Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.

Kaynak türü olduğunda **RelationalSource** (OData içerir) aşağıdaki özelliklere hello typeProperties bölümünde bulunur:

| Özellik | Açıklama | Örnek | Gerekli |
| --- | --- | --- | --- |
| sorgu |Merhaba özel sorgu tooread verileri kullanın. |"? $select adı, açıklama ve $top = 5 =" |Hayır |

## <a name="type-mapping-for-odata"></a>Tür eşlemesi için OData
Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopyalama etkinliği gerçekleştiren kaynak türleri toosink türlerinden otomatik tür dönüşümleri iki aşamalı bir yaklaşım aşağıdaki hello ile.

1. Yerel kaynak türleri too.NET türünden Dönüştür
2. .NET türü toonative havuz türünden Dönüştür

Veri OData taşırken hello aşağıdaki eşlemelerini OData türlerini too.NET türünden kullanılır.

| OData veri türü | .NET türü |
| --- | --- |
| Edm.Binary |Byte] |
| Edm.Boolean |bool |
| Edm.Byte |Byte] |
| Edm.DateTime |Tarih saat |
| Edm.Decimal |Ondalık |
| Edm.Double |Çift |
| Edm.Single |Tek |
| Edm.Guid |GUID |
| Edm.Int16 |Int16 |
| Edm.Int32 |Int32 |
| Edm.Int64 |Int64 |
| Edm.SByte |Int16 |
| Edm.String |Dize |
| Edm.Time |TimeSpan |
| Edm.DateTimeOffset |DateTimeOffset |

> [!Note]
> OData karmaşık veri türleri örneğin nesnesi desteklenmez.

## <a name="json-example-copy-data-from-odata-source-tooazure-blob"></a>JSON örnek: OData kaynak tooAzure Blob veri kopyalama
Bu örnek örnek JSON tanımları sağlar, toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Bunlar, nasıl bir OData toocopy verileri tooan Azure Blob Depolama kaynağı gösterir. Ancak, veri belirtildiği hello havuzlarını, kopyalanan tooany olabilir [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello. Merhaba örnek Data Factory varlıklarını aşağıdaki hello sahiptir:

1. Bağlı hizmet türü [OData](#linked-service-properties).
2. Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Bir giriş [dataset](data-factory-create-datasets.md) türü [ODataResource](#dataset-properties).
4. Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [RelationalSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Merhaba örnek verileri bir OData kaynak tooan karşı Azure blob saatte sorgulamasını kopyalar. Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.

**OData bağlantılı hizmeti:** kullandığı hello anonim kimlik doğrulaması Bu örnek. Bkz: [OData bağlantılı hizmeti](#linked-service-properties) bölümü için farklı tür kimlik doğrulaması kullanabilirsiniz.

```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
            }
        }
}
```

**Azure Storage bağlı hizmeti:**

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

**OData giriş veri kümesi:**

"Dış" ayarı: "true" bildirir hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.

```json
{
    "name": "ODataDataset",
    "properties":
    {
        "type": "ODataResource",
        "typeProperties":
        {
                "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3                
        }
    }
}
```

Belirtme **yolu** hello kümesinde tanımı isteğe bağlıdır.

**Azure Blob dataset çıktı:**

Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1). hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir. Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.

```json
{
    "name": "AzureBlobODataDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


**OData kaynağı ve Blob havuz ile ardışık düzeninde etkinlik kopyalayın:**

Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**RelationalSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**. Merhaba belirtilen hello SQL sorgusu **sorgu** özelliği hello OData kaynağından hello en son (yeni) verileri seçer.

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "?$select=Name, Description&$top=5",
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "ODataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobODataDataSet"
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
                "name": "ODataToBlob"
            }
        ],
        "start": "2017-02-01T18:00:00Z",
        "end": "2017-02-03T19:00:00Z"
    }
}
```

Belirtme **sorgu** hello ardışık düzeninde tanımı isteğe bağlıdır. Merhaba **URL** hello Data Factory hizmetinin tooretrieve veri kullanır: Merhaba bağlantılı hizmeti (gerekli) + (isteğe bağlı) hello dataset belirtilen yolu + sorgu (isteğe bağlı) hello ardışık düzeninde URL belirtilmiş.


### <a name="type-mapping-for-odata"></a>Tür eşlemesi için OData
Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopyalama etkinliği gerçekleştiren kaynak türleri toosink türlerinden otomatik tür dönüşümleri 2 adımlı yaklaşımı izleyerek hello ile:

1. Yerel kaynak türleri too.NET türünden Dönüştür
2. .NET türü toonative havuz türünden Dönüştür

OData veri depolarına verilerin taşınması, OData veri türleri eşlenen too.NET türleridir.

## <a name="map-source-toosink-columns"></a>Kaynak toosink sütunları eşleme
Kaynak veri kümesi toocolumns havuz kümesindeki eşleme sütunlarında hakkında toolearn bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>İlişkisel kaynaklardan yinelenebilir okuma
İlişkisel veri depoları veri kopyalama işlemi sırasında Yinelenebilirlik göz tooavoid tutmak istenmeyen sonuçları. Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz. Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz. Bir dilim iki yolla yeniden zaman, aynı veri hello emin toomake nasıl geçtiğinden bağımsız okuma gerekir dilim birçok kez çalıştırın. Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Performans ve ayarlama
Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.
