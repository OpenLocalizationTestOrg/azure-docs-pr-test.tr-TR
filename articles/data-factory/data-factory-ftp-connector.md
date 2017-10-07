---
title: Azure Data Factory kullanarak bir FTP sunucusu aaaMove verilerden | Microsoft Docs
description: "Hakkında bilgi edinin Azure Data Factory kullanarak bir FTP sunucusunu toomove verileri."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: eea3bab0-a6e4-4045-ad44-9ce06229c718
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jingwang
ms.openlocfilehash: c707e29532b2a8a870603948cb6150ab857bd6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a>Azure Data Factory kullanarak bir FTP sunucusundan veri taşıma
Bu makalede nasıl toouse hello kopyalama etkinliği Azure Data Factory toomove verileri bir FTP sunucusundan açıklanmaktadır. Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.

Bir FTP sunucusu desteklenen tooany havuz veri deposundan verileri kopyalayabilirsiniz. Verileri bir listesi için desteklenen depoları hello kopyalama etkinliği tarafından havuzlarını hello görür [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo. Veri Fabrikası şu anda yalnızca bir FTP sunucusu tooother verilerden veri taşımayı depolar, ancak verileri diğer veriler taşıma değil tooan FTP sunucusu depolar destekler. Her iki şirket içi destekler ve FTP sunucuları bulut.

> [!NOTE]
> başarıyla kopyalanan toohello hedef sonra hello kopyalama etkinliği hello kaynak dosya silinmez. Sonra başarılı bir kopyasını toodelete hello kaynak dosyası gerekiyorsa, bir özel etkinlik toodelete hello dosyası oluşturun ve hello ardışık düzeninde hello etkinliği kullanın. 

## <a name="enable-connectivity"></a>Bağlantıyı etkinleştirmek
Veri geçiş yapıyorsanız, bir **şirket içi** FTP sunucusu tooa bulut veri deposu (örneğin, tooAzure Blob Depolama), yükleme ve veri yönetimi ağ geçidi kullanın. Merhaba veri yönetimi ağ geçidi, şirket içi makinenizde yüklü bir istemci aracısıdır ve bulut Hizmetleri tooconnect tooan şirket içi kaynak sağlar. Ayrıntılar için bkz [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md). Merhaba ağ geçidi kurun ayarlama ve kullanılarak adım adım yönergeler için bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md). Merhaba sunucu üzerinde bir Azure altyapı (ıaas) sanal makine (VM) olarak olsa bile, hello ağ geçidi tooconnect tooan FTP sunucusu kullanın.

Olası tooinstall hello ağ geçidi olduğu hello üzerinde aynı makine ya da Iaas VM FTP sunucusu hello gibi şirket içi. Ancak, ayrı makinede veya Iaas VM tooavoid kaynak çekişmesini ve daha iyi performans için hello ağ geçidi yüklemenizi öneririz. Merhaba ağ geçidi ayrı bir makineye yüklediğinizde hello makine mümkün tooaccess hello FTP sunucusu olmalıdır.

## <a name="get-started"></a>başlarken
Farklı araçlar veya API'lerini kullanarak bir FTP kaynaktan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.

Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Data Factory Kopyalama Sihirbazı**. Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hızlı kılavuz.

Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager şablonu**, **.NET API**, ve **REST API**. Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.

Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:

1. Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.
2. Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.
3. Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.

Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur. Araçları veya API'ler (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın. Merhaba bir FTP veri deposundaki kullanılan toocopy verileri Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz [JSON örnek: FTP sunucusu tooAzure blobundan veri kopyalama](#json-example-copy-data-from-ftp-server-to-azure-blob) bu makalenin.

> [!NOTE]
> Desteklenen dosya ve sıkıştırma biçimleri toouse hakkında daha fazla ayrıntı için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md).

Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooFTP olan JSON özellikleri hakkında ayrıntılı bilgi sağlar.

## <a name="linked-service-properties"></a>Bağlantılı hizmet özellikleri
Aşağıdaki tablonun hello JSON öğeleri belirli tooan bağlı FTP hizmeti açıklar.

| Özellik | Açıklama | Gerekli | Varsayılan |
| --- | --- | --- | --- |
| type |Bu tooFtpServer ayarlayın. |Evet |&nbsp; |
| ana bilgisayar |Merhaba adını veya hello FTP sunucusunun IP adresini belirtin. |Evet |&nbsp; |
| authenticationType |Merhaba kimlik doğrulama türü belirtin. |Evet |Temel, anonim |
| kullanıcı adı |Erişim toohello FTP sunucusu olan hello kullanıcı belirtin. |Hayır |&nbsp; |
| password |Merhaba kullanıcının (kullanıcı adı) Hello parolasını belirtin. |Hayır |&nbsp; |
| encryptedCredential |Şifrelenmiş hello kimlik bilgisi tooaccess hello FTP sunucusunu belirtin. |Hayır |&nbsp; |
| gatewayName |Veri Yönetimi ağ geçidi tooconnect tooan şirket içi FTP sunucusunda hello ağ geçidinin Hello adı belirtin. |Hayır |&nbsp; |
| port |Hangi hello FTP sunucusunun dinleme hello bağlantı noktasını belirtin. |Hayır |21 |
| enableSsl |Toouse SSL/TLS kanalı üzerinden FTP olup olmadığını belirtin. |Hayır |TRUE |
| enableServerCertificateValidation |FTP SSL/TLS kanalı üzerinden kullanırken tooenable sunucu SSL sertifikası doğrulaması olup olmadığını belirtin. |Hayır |TRUE |

### <a name="use-anonymous-authentication"></a>Anonim kimlik doğrulamasını kullan

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {        
            "authenticationType": "Anonymous",
              "host": "myftpserver.com"
        }
    }
}
```

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a>Kullanıcı adı ve parola düz metin olarak temel kimlik doğrulaması için kullanın.

```JSON
{
    "name": "FTPLinkedService",
      "properties": {
    "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
      }
}
```

### <a name="use-port-enablessl-enableservercertificatevalidation"></a>Bağlantı noktası, enableSsl, enableServerCertificateValidation kullanın

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a>Kimlik doğrulama ve ağ geçidi için encryptedCredential kullanın

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "mygateway"
        }
      }
}
```

## <a name="dataset-properties"></a>Veri kümesi özellikleri
Bölümleri ve veri kümelerini tanımlamak için kullanılabilen özellikleri tam listesi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md). Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri kümesi türleri için benzerdir.

Merhaba **typeProperties** bölümü, her veri kümesi türü için farklıdır. Belirli toohello veri kümesi türü olan bilgiler sağlar. Merhaba **typeProperties** bir veri kümesi için bir bölüm türü **FileShare** hello aşağıdaki özelliklere sahiptir:

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| folderPath |Alt toohello klasör. Kaçış karakteri kullanmak ' \ ' hello dize özel karakter. Bkz: [örnek bağlantılı hizmeti ve veri kümesi tanımları](#sample-linked-service-and-dataset-definitions) örnekleri için.<br/><br/>Bu özellik ile birleştirebilirsiniz **partitionBy** toohave klasör yolları dilimine göre başlangıç ve bitiş tarih saatleri. |Evet |
| fileName |Hello Hello hello dosyasının adını belirtin **folderPath** hello tablo toorefer tooa belirli dosya hello klasöründeki istiyorsanız. Bu özellik için herhangi bir değer belirtmezseniz, hello tablo hello klasöründeki tooall dosyaları işaret eder.<br/><br/>Zaman **fileName** belirtilmemiş bir çıkış veri kümesi için oluşturulan hello dosyasının hello adı biçimini izleyen hello: <br/><br/>Veriler. <Guid>.txt (örnek: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |Hayır |
| fileFilter |Bir filtre kullanılan toobe tooselect dosya alt kümesine hello belirtin **folderPath**, tüm dosyalar yerine.<br/><br/>İzin verilen değerler: `*` (birden çok karakter) ve `?` (tek bir karakter).<br/><br/>Örnek 1:`"fileFilter": "*.log"`<br/>Örnek 2:`"fileFilter": 2014-1-?.txt"`<br/><br/> **fileFilter** bir giriş FileShare veri kümesi için geçerlidir. Bu özellik, Hadoop dağıtılmış dosya sistemi (HDFS ile) desteklenmiyor. |Hayır |
| partitionedBy |Toospecify dinamik kullanılan **folderPath** ve **fileName** zaman serisi veriler için. Örneğin, belirleyebileceğiniz bir **folderPath** için verileri saatte parametreli. |Hayır |
| Biçimi | şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set hello **türü** biçimi tooone şu değerlerden biri altında özellik. Merhaba daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi ](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler. <br><br> Depoları arasında (ikili kopya), dosya tabanlı oldukları gibi toocopy dosyaları istiyorsanız, her iki girdi ve çıktı veri kümesi tanımlarında hello Biçim bölümü atlayın. |Hayır |
| Sıkıştırma | Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin. Desteklenen türler **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**, ve desteklenen düzeyler **Optimal** ve **en hızlı**. Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support). |Hayır |
| useBinaryTransfer |Toouse hello ikili aktarım modu olup olmadığını belirtin. Merhaba değerleri (Bu, hello varsayılan değer) ikili mod için true ve false ASCII için. Merhaba ilişkili bağlantılı hizmet türü türü olduğunda bu özellik yalnızca kullanılabilir: Ftp_sunucusu. |Hayır |

> [!NOTE]
> **Dosya adı** ve **fileFilter** eşzamanlı olarak kullanılamaz.

### <a name="use-hello-partionedby-property"></a>Merhaba partionedBy özelliğini kullanın
Merhaba önceki bölümünde belirtildiği gibi bir dinamik belirtebilirsiniz **folderPath** ve **fileName** zaman serisi veri hello ile **partitionedBy** özelliği.

Zaman serisi veri kümeleri, zamanlama ve dilimleri hakkında toolearn bkz [veri kümeleri oluşturma](data-factory-create-datasets.md), [zamanlama ve yürütme](data-factory-scheduling-and-execution.md), ve [ardışık düzen oluşturma](data-factory-create-pipelines.md).

#### <a name="sample-1"></a>Örnek 1

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
Bu örnekte, {dilim} hello Data Factory sistem değişkeni SliceStart değeriyle değiştirilir, belirtilen (YYYYMMDDHH) hello biçimlendirin. Merhaba SliceStart hello dilim toostart süresini ifade eder. Merhaba klasör yolu, her dilim için farklıdır. (Örneğin, wikidatagateway/wikisampledataout/2014100103 veya wikidatagateway/wikisampledataout/2014100104.)

#### <a name="sample-2"></a>Örnek 2

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
Bu örnekte, hello tarafından kullanılan ayrı değişkenleri içine ayıklanır hello yıl, ay, gün ve saat SliceStart **folderPath** ve **fileName** özellikleri.

## <a name="copy-activity-properties"></a>Etkinlik özellikleri Kopyala
Bölümleri ve etkinlikleri tanımlamak için kullanılabilen özellikleri tam listesi için bkz: [ardışık düzen oluşturma](data-factory-create-pipelines.md). Ad, açıklama, giriş ve çıkış tabloları ve ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir.

Hello kullanılabilen özellikleri **typeProperties** bölümünü diğer yandan faaliyete hello Merhaba, her etkinlik türü ile değişir. Merhaba kopya etkinliği için hello türü özellikleri hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.

Kopyalama etkinliğinde hello kaynak türü olduğunda **FileSystemSource**, özellik aşağıdaki hello sağlanmıştır **typeProperties** bölümü:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| Özyinelemeli |Merhaba klasörlerdeki ya da yalnızca klasöründen hello belirtilen Hello veri yinelemeli olarak okunur olup olmadığını gösterir. |TRUE, False (varsayılan) |Hayır |

## <a name="json-example-copy-data-from-ftp-server-tooazure-blob"></a>JSON örnek: FTP sunucusu tooAzure Blob veri kopyalama
Bu örnek göstermektedir nasıl bir FTP sunucusu tooAzure Blob Depolama toocopy verileri. İçinde belirtilen hello hello tooany havuzlarını doğrudan veri ancak kopyalanabilir [desteklenen veri depoları ve biçimleri](data-factory-data-movement-activities.md#supported-data-stores-and-formats), veri fabrikasında hello kopyalama etkinliği kullanarak.  

Merhaba aşağıdaki örneklerde sağlayan örnek JSON tanımları toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), veya [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):

* Bağlı hizmet türü [Ftp_sunucusu](#linked-service-properties)
* Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
* Bir giriş [dataset](data-factory-create-datasets.md) türü [dosya paylaşımı](#dataset-properties)
* Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
* A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [FileSystemSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)

Merhaba örnek verileri saatte bir FTP sunucusu tooan Azure blob kopyalar. Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.

### <a name="ftp-linked-service"></a>Bağlı FTP hizmeti

Bu örnek, hello kullanıcı adı ve parola düz metin ile temel kimlik doğrulaması kullanır. Aşağıdaki şekilde hello birini de kullanabilirsiniz:

* Anonim kimlik doğrulaması
* Şifrelenmiş kimlik bilgileri ile temel kimlik doğrulaması
* SSL/TLS (FTPS) üzerinden FTP

Merhaba bkz [FTP bağlantılı hizmeti](#linked-service-properties) bölümü için farklı tür kimlik doğrulaması kullanabilirsiniz.

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
    "type": "FtpServer",
    "typeProperties": {
        "host": "myftpserver.com",           
        "authenticationType": "Basic",
        "username": "Admin",
        "password": "123456"
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
### <a name="ftp-input-dataset"></a>FTP giriş veri kümesi

Bu veri kümesi toohello FTP klasörü işaret ediyor `mysharedfolder` ve dosya `test.csv`. Merhaba ardışık düzen hello dosya toohello hedef kopyalar.

Ayarı **dış** çok**true** hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil bildirir.

```JSON
{
  "name": "FTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "FTPLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv",
      "useBinaryTransfer": true
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

### <a name="azure-blob-output-dataset"></a>Azure Blob çıktı veri kümesi

Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1). Merhaba klasör yolu hello blob için dinamik olarak değerlendirilen işleniyor hello dilimin hello başlangıç zamanı temel alınarak. Merhaba klasör yolu hello yıl, ay, gün ve saat bölümlerini hello başlangıç saatini kullanır.

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/ftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a>Dosya sistemi kaynak ve blob havuz sahip işlem hattı kopyalama etkinliği

Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**FileSystemSource**ve hello **havuz** türü olarak ayarlanmış çok**BlobSink**.

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
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
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00Z",
        "end": "2016-08-24T19:00:00Z"
    }
}
```
> [!NOTE]
> Kaynak veri kümesi toocolumns havuz kümesinden toomap sütunlarından bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).

## <a name="next-steps"></a>Sonraki adımlar
Aşağıdaki makaleleri hello bakın:

* anahtarı hakkında toolearn Etkenler etkisi performans veri fabrikasında (kopyalama etkinliği) veri hareketlerini ve çeşitli yolları toooptimize, hello bkz [kopyalama etkinliği performans ve ayarlama Kılavuzu](data-factory-copy-activity-performance.md).

* Kopyalama etkinliği ile işlem hattı oluşturmak için adım adım yönergeler için bkz: Merhaba [kopyalama etkinliği Öğreticisi](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
