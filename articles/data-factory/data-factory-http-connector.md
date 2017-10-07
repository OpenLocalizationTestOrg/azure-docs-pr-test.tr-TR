---
title: "bir HTTP kaynağı - Azure aaaMove verilerden | Microsoft Docs"
description: "Azure Data Factory kullanarak şirket içi veya Bulut HTTP toomove verileri nasıl kaynak hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: e39b9cbff870aef4be91938cacff39a2fd12d64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a>Azure Data Factory kullanarak bir HTTP kaynağından veri taşıma
Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove bir şirket içi/bulut HTTP uç noktası tooa verilerden havuz veri deposu desteklenen özetlenmektedir. Bu makale üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale listesiyle kopyalama etkinliği ve hello kaynakları/havuzlarını desteklenen veri depoları veri taşıma genel bir bakış sunar.

Veri Fabrikası şu anda yalnızca bir HTTP veri taşınmasını destekler tooother veri depolarına kaynağı, ancak verileri diğer veriler taşıma değil tooan HTTP hedef depolar.

## <a name="supported-scenarios-and-authentication-types"></a>Desteklenen senaryolar ve kimlik doğrulama türleri
Bu HTTP Bağlayıcısı tooretrieve verilerden kullanabilirsiniz **Bulut ve şirket içi HTTP/s uç nokta** HTTP kullanarak **almak** veya **POST** yöntemi. şu kimlik doğrulama türlerini hello desteklenir: **anonim**, **temel**, **Özet**, **Windows**, ve  **ClientCertificate**. Not hello birbirinden bu bağlayıcı ve hello [Web tablo Bağlayıcısı](data-factory-web-table-connector.md) olduğu: hello ikinci tablodur kullanılan tooextract web HTML sayfasından içerik.

Bir şirket içi HTTP uç noktasından veri kopyalama işlemi sırasında veri yönetimi ağ geçidi hello şirket içi ortamına/Azure VM yüklemeniz gerekir. Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale toolearn veri yönetimi ağ geçidi ve hello ağ geçidi kurun ayarlama hakkında adım adım yönergeleri hakkında.

## <a name="getting-started"></a>Başlarken
Farklı araçlar/API'lerini kullanarak bir HTTP kaynaktan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.

- Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**. Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.

- Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**. Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için. HTTP kaynağı tooAzure Blob Storage toocopy verileri JSON örnekleri için bkz: [JSON örnekler](#json-examples) Bu makaleler bölümü.

## <a name="linked-service-properties"></a>Bağlantılı hizmet özellikleri
Aşağıdaki tablonun hello JSON öğeleri belirli tooHTTP bağlantılı hizmeti için bir açıklama sağlar.

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| type | Merhaba type özelliği ayarlanmalıdır: `Http`. | Evet |
| URL | Temel URL toohello Web sunucusu | Evet |
| authenticationType | Merhaba kimlik doğrulama türünü belirtir. İzin verilen değerler: **anonim**, **temel**, **Özet**, **Windows**, **ClientCertificate**. <br><br> Daha fazla özellikleri ve JSON örnekleri bu tablonun altındaki toosections bu kimlik doğrulama türleri için sırasıyla bakın. | Evet |
| enableServerCertificateValidation | Kaynak HTTPS Web sunucusu ise tooenable sunucu SSL sertifikası doğrulaması olup olmadığını belirtin | Hayır, varsayılan değer true şeklindedir |
| gatewayName | Merhaba veri yönetimi ağ geçidi tooconnect tooan adını HTTP kaynağı şirket içi. | Bir şirket içi HTTP kaynaktan veri kopyalama, Evet. |
| encryptedCredential | Şifrelenmiş kimlik bilgileri tooaccess hello HTTP uç noktası. Otomatik olarak oluşturulan Kopyalama Sihirbazı'nı veya hello ClickOnce açılan iletişim kutusunda hello kimlik doğrulama bilgilerini yapılandırın. | Hayır. Yalnızca bir şirket içi HTTP sunucusundan veri kopyalama işlemi sırasında uygulanır. |

Bkz: [şirket içi kaynakları ve veri yönetimi ağ geçidi ile Merhaba bulut arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) şirket içi HTTP Bağlayıcısı veri kaynağı için kimlik bilgilerini ayarlama hakkında ayrıntılı bilgi için.

### <a name="using-basic-digest-or-windows-authentication"></a>Temel, Özet veya Windows kimlik doğrulaması kullanma

Ayarlama `authenticationType` olarak `Basic`, `Digest`, veya `Windows`ve bunun yanında, HTTP Bağlayıcısı genel olanları sunulan yukarıda hello aşağıdaki özelliklere hello belirtin:

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| kullanıcı adı | Kullanıcı adı tooaccess hello HTTP uç noktası. | Evet |
| password | Merhaba kullanıcının (kullanıcı adı) parolası. | Evet |

#### <a name="example-using-basic-digest-or-windows-authentication"></a>Örnek: Temel, Özet veya Windows kimlik doğrulaması kullanma

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "basic",
            "url" : "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

### <a name="using-clientcertificate-authentication"></a>ClientCertificate kimlik doğrulaması kullanma

toouse temel kimlik doğrulamasını ayarlamak `authenticationType` olarak `ClientCertificate`ve bunun yanında, HTTP Bağlayıcısı genel olanları sunulan yukarıda hello aşağıdaki özelliklere hello belirtin:

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| embeddedCertData | Merhaba Base64 ile kodlanmış içeriğini ikili veri hello kişisel bilgi değişimi (PFX) dosyası. | Her iki hello belirtin `embeddedCertData` veya `certThumbprint`. |
| Certthumbprınt | ağ geçidi makinenizin sertifika deposunda yüklü hello sertifikanın parmak izini hello. Yalnızca bir şirket içi HTTP kaynaktan veri kopyalama işlemi sırasında uygulanır. | Her iki hello belirtin `embeddedCertData` veya `certThumbprint`. |
| password | Merhaba sertifikayla ilişkili parola. | Hayır |

Kullanırsanız `certThumbprint` kimlik doğrulaması ve hello sertifika hello kişisel hello yerel bilgisayar deposunda yüklü için toogrant hello okuma izni toohello ağ geçidi hizmeti gerekir:

1. Microsoft Yönetim Konsolu (MMC) başlatın. Merhaba eklemek **sertifikaları** bu hedefleri hello eklentisi **yerel bilgisayar**.
2. Genişletme **sertifikaları**, **kişisel**, tıklatıp **Sertifikalar**.
3. Merhaba kişisel deposundan Hello sertifikayı sağ tıklatın ve seçin **tüm görevler**->**özel anahtarları Yönet...**
3. Merhaba üzerinde **güvenlik** sekmesinde, altında veri yönetimi ağ geçidi ana bilgisayar hizmeti çalıştığı hello okuma erişimi toohello sertifikasıyla hello kullanıcı hesabını ekleyin.  

#### <a name="example-using-client-certificate"></a>Örnek: istemci sertifikası kullanarak
Bu hizmet bağlantılar, veri fabrikası tooan şirket içi HTTP web sunucunuzun bağlı. Veri Yönetimi yüklü ağ geçidi ile Merhaba makinede yüklü bir istemci sertifikası kullanır.

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"

        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a>Örnek: istemci sertifikası bir dosyada kullanma
Bu hizmet bağlantılar, veri fabrikası tooan şirket içi HTTP web sunucunuzun bağlı. Veri Yönetimi yüklü ağ geçidi ile bir istemci sertifika dosyası hello makinede kullanır.

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

## <a name="dataset-properties"></a>Veri kümesi özellikleri
Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi. Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.

Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar. Merhaba typeProperties bölüm türü veri kümesi için **Http** hello aşağıdaki özelliklere sahip

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| type | Merhaba dataset Hello türü belirttiniz. çok ayarlanmalıdır`Http`. | Evet |
| relativeUrl | Merhaba verileri içeren bir göreli URL toohello kaynağıdır. Yol belirtilmediğinde hello bağlantılı hizmet tanımında belirtilen yalnızca hello URL'si kullanılır. <br><br> kullanabileceğiniz tooconstruct dinamik URL [Data Factory işlevler ve sistem değişkenleri](data-factory-functions-variables.md), örneğin "relativeUrl": "$$Text.Format ('/ my/rapor? ay = {0:yyyy}-{0:MM} & fmt csv =', SliceStart)". | Hayır |
| requestMethod | HTTP yöntemi. İzin verilen değerler **almak** veya **POST**. | Hayır. Varsayılan değer `GET`. |
| additionalHeaders | Ek HTTP isteği üstbilgileri. | Hayır |
| RequestBody | HTTP istek gövdesi. | Hayır |
| Biçimi | Toosimply istiyorsanız **HTTP uç noktası olarak hello veri almak-olduğu** ayrıştırma olmadan, bu biçim ayarlarını atla. <br><br> Kopyalama sırasında tooparse hello HTTP yanıt içerik isterseniz şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**. Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler. |Hayır |
| Sıkıştırma | Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin. Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**. Desteklenen düzeyler: **Optimal** ve **en hızlı**. Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support). |Hayır |

### <a name="example-using-hello-get-default-method"></a>Örnek: hello (varsayılan) GET yöntemini kullanma

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

### <a name="example-using-hello-post-method"></a>Örnek: Merhaba POST yöntemini kullanma

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
           "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a>Etkinlik özellikleri Kopyala
Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi. Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.

Hello kullanılabilen özellikleri **typeProperties** bölüm diğer yandan hello hello faaliyete, her etkinlik türü ile farklılık gösterir. Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.

Şu anda kopyalama etkinliği hello kaynağında olduğunda türü **HttpSource**, aşağıdaki özelliklere hello desteklenir.

| Özellik | Açıklama | Gerekli |
| -------- | ----------- | -------- |
| httpRequestTimeout | Merhaba HTTP isteği tooget yanıt için zaman aşımı (TimeSpan) hello. Merhaba zaman aşımı tooget bir yanıt hello zaman aşımı tooread yanıt verileri değil olur. | Hayır. Varsayılan değer: 00:01:40 |

## <a name="supported-file-and-compression-formats"></a>Desteklenen dosya ve sıkıştırma biçimleri
Bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md) makale ayrıntıları.

## <a name="json-examples"></a>JSON örnekleri
Aşağıdaki örneğine hello sağlayan örnek JSON tanımları toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Bunların nasıl tooAzure Blob Storage HTTP toocopy veri kaynağı gösterir. Ancak, veriler kopyalanabilir **doğrudan** herhangi birinden belirtildiği hello havuzlarını, kaynakları tooany [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.

### <a name="example-copy-data-from-http-source-tooazure-blob-storage"></a>Örnek: HTTP kaynağı tooAzure Blob depolama alanından veri Kopyala
Bu örnek için veri fabrikası çözümü Hello Data Factory varlıklarını aşağıdaki hello içerir:

1. Bağlı hizmet türü [HTTP](#linked-service-properties).
2. Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Bir giriş [dataset](data-factory-create-datasets.md) türü [Http](#dataset-properties).
4. Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [HttpSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Merhaba örnek verileri saatte bir HTTP kaynağı tooan Azure blob kopyalar. Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.

### <a name="http-linked-service"></a>Bağlantılı HTTP hizmeti
HTTP kullanan hello Bu örnek anonim kimlik doğrulaması ile bağlı. Bkz: [HTTP bağlantılı hizmeti](#linked-service-properties) bölümü için farklı tür kimlik doğrulaması kullanabilirsiniz.

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a>Azure Storage bağlı hizmeti

```JSON
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

### <a name="http-input-dataset"></a>HTTP girdi veri kümesi
Ayarı **dış** çok**true** hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil bildirir.

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}

```

### <a name="azure-blob-output-dataset"></a>Azure Blob çıktı veri kümesi

Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).

```JSON
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

### <a name="pipeline-with-copy-activity"></a>Kopyalama etkinliği ile kanalı

Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**HttpSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**.

Bkz: [HttpSource](#copy-activity-properties) HttpSource hello tarafından desteklenen özellikler hello listesi.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "HttpSourceToAzureBlob",
        "description": "Copy from an HTTP source tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "HttpSourceDataInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "HttpSource"
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
> Kaynak veri kümesi toocolumns havuz kümesinden toomap sütunlarından bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Performans ve ayarlama
Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.
