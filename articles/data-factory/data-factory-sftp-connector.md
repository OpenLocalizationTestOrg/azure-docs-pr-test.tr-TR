---
title: Azure Data Factory kullanarak SFTP sunucudan aaaMove veri | Microsoft Docs
description: "Hakkında bilgi edinin şirket içi veya Bulut SFTP sunucusunu Azure Data Factory kullanarak toomove verileri."
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
ms.date: 06/05/2017
ms.author: jingwang
ms.openlocfilehash: b976289e2c1b1899634bb5565b375499077fa554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-sftp-server-using-azure-data-factory"></a>Azure Data Factory kullanarak bir SFTP sunucudan veri taşıma
Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove bir şirket içi/bulut SFTP sunucu tooa verilerden havuz veri deposu desteklenen özetlenmektedir. Bu makale üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale listesiyle kopyalama etkinliği ve hello kaynakları/havuzlarını desteklenen veri depoları veri taşıma genel bir bakış sunar.

Veri Fabrikası şu anda destekleyen bir SFTP server tooother verilerden veri depolar, ancak taşıma yalnızca tooan SFTP sunucuda depolanan verileri diğer veriler taşıma için. Her iki şirket içi destekler ve SFTP sunucuları bulut.

> [!NOTE]
> Başarıyla kopyalanan toohello hedef tamamlandıktan sonra kopyalama etkinliği hello kaynak dosyayı silmez. Sonra başarılı bir kopyasını toodelete hello kaynak dosyası gerekiyorsa, bir özel etkinlik toodelete hello dosyası oluşturun ve hello ardışık düzeninde hello etkinliği kullanın. 

## <a name="supported-scenarios-and-authentication-types"></a>Desteklenen senaryolar ve kimlik doğrulama türleri
Bu SFTP bağlayıcı toocopy verilerden kullanabilirsiniz **SFTP sunucuları ve şirket içi SFTP sunucuları hem de bulut**. **Temel** ve **SshPublicKey** toohello SFTP sunucusuna bağlanırken kimlik doğrulama türleri desteklenir.

Bir şirket içi SFTP sunucusundan veri kopyalama işlemi sırasında veri yönetimi ağ geçidi hello şirket içi ortamına/Azure VM yüklemeniz gerekir. Bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) hello ağ geçidi hakkında ayrıntılı bilgi için. Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale hello ağ geçidi kurun ayarlama ve kullanmaya ilişkin adım adım yönergeler.

## <a name="getting-started"></a>Başlarken
Farklı araçlar/API'lerini kullanarak bir SFTP kaynaktan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.

- Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**. Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.

- Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**. Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için. SFTP sunucu tooAzure Blob Storage toocopy verileri JSON örnekleri için bkz: [JSON örnek: SFTP sunucu tooAzure blobundan veri kopyalama](#json-example-copy-data-from-sftp-server-to-azure-blob) bu makalenin.

## <a name="linked-service-properties"></a>Bağlantılı hizmet özellikleri
Aşağıdaki tablonun hello JSON öğeleri belirli tooFTP bağlantılı hizmeti için bir açıklama sağlar.

| Özellik | Açıklama | Gerekli |
| --- | --- | --- | --- |
| type | Merhaba type özelliği çok ayarlanmalıdır`Sftp`. |Evet |
| ana bilgisayar | Merhaba SFTP sunucu adı veya IP adresi. |Evet |
| port |Hangi hello SFTP sunucusunun dinleme yaptığı bağlantı noktası. Merhaba varsayılan değer: 21 |Hayır |
| authenticationType |Kimlik doğrulama türü belirtin. İzin verilen değerler: **temel**, **SshPublicKey**. <br><br> Çok başvuran[kullanarak temel kimlik doğrulaması](#using-basic-authentication) ve [kullanarak SSH ortak anahtar kimlik doğrulaması](#using-ssh-public-key-authentication) daha fazla özellikleri ve JSON örnekleri sırasıyla bölümler. |Evet |
| skipHostKeyValidation | Tooskip anahtar doğrulama konak olup olmadığını belirtin. | Hayır. Merhaba varsayılan değeri: false |
| hostKeyFingerprint | Merhaba parmak izi hello ana bilgisayar anahtarı belirtin. | Merhaba, Evet `skipHostKeyValidation` toofalse ayarlanır.  |
| gatewayName |Merhaba veri yönetimi ağ geçidi tooconnect tooan adını SFTP sunucu şirket içi. | Bir şirket içi SFTP sunucusundan veri kopyalama, Evet. |
| encryptedCredential | Şifrelenmiş kimlik bilgileri tooaccess hello SFTP sunucusu. Otomatik olarak oluşturulan, temel kimlik doğrulaması (kullanıcı adı + parola) veya SshPublicKey kimlik (kullanıcı adı + özel anahtar yolu veya içerik) Kopyalama Sihirbazı'nı veya hello ClickOnce açılan iletişim kutusunda belirttiğiniz zaman. | Hayır. Yalnızca bir şirket içi SFTP sunucusundan veri kopyalama işlemi sırasında uygulanır. |

### <a name="using-basic-authentication"></a>Temel kimlik doğrulaması kullanma

toouse temel kimlik doğrulamasını ayarlamak `authenticationType` olarak `Basic`ve bunun yanında, SFTP bağlayıcı hello son bölümde sunulan genel olanları hello aşağıdaki özelliklere hello belirtin:

| Özellik | Açıklama | Gerekli |
| --- | --- | --- | --- |
| kullanıcı adı | Erişim toohello SFTP sunucusu olan kullanıcı. |Evet |
| password | Merhaba kullanıcının (kullanıcı adı) parolası. | Evet |

#### <a name="example-basic-authentication"></a>Örnek: Temel kimlik doğrulaması
```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a>Örnek: Temel kimlik doğrulaması ile şifrelenmiş kimlik bilgileri

```JSON
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
      }
}
```

### <a name="using-ssh-public-key-authentication"></a>SSH ortak anahtar kimlik doğrulaması kullanma

toouse SSH ortak anahtar kimlik doğrulaması, ayarlamak `authenticationType` olarak `SshPublicKey`ve bunun yanında, SFTP bağlayıcı hello son bölümde sunulan genel olanları hello aşağıdaki özelliklere hello belirtin:

| Özellik | Açıklama | Gerekli |
| --- | --- | --- | --- |
| kullanıcı adı |Erişim toohello SFTP sunucusu olan kullanıcı |Evet |
| privateKeyPath | Mutlak yol toohello belirtin özel anahtar dosyası bu ağ geçidi erişebilir. | Her iki hello belirtin `privateKeyPath` veya `privateKeyContent`. <br><br> Yalnızca bir şirket içi SFTP sunucusundan veri kopyalama işlemi sırasında uygulanır. |
| privateKeyContent | Merhaba özel anahtar içeriğinin seri hale getirilmiş bir dize. Merhaba Kopyalama Sihirbazı'nı hello özel anahtar dosyası okuma ve hello özel anahtar içeriği otomatik olarak ayıklar. Tüm diğer aracı/SDK kullanıyorsanız, bunun yerine hello privateKeyPath özelliğini kullanın. | Her iki hello belirtin `privateKeyPath` veya `privateKeyContent`. |
| Parola | Merhaba anahtar dosyası bir parola deyimi tarafından korunuyorsa hello geçişi tümcecik/parola toodecrypt hello özel anahtarı belirtin. | Merhaba özel anahtar dosyası bir parola deyimi tarafından korunuyorsa, Evet. |

> [!NOTE]
> SFTP Bağlayıcısı yalnızca OpenSSH anahtarını destekler. Anahtar dosyanızı hello doğru biçimde olduğundan emin olun. Putty aracı tooconvert .ppk tooOpenSSH biçiminden kullanabilirsiniz.

#### <a name="example-sshpublickey-authentication-using-private-key-filepath"></a>Örnek: özel anahtar filePath kullanarak SshPublicKey kimlik doğrulaması

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a>Örnek: özel anahtar içeriği kullanarak SshPublicKey kimlik doğrulaması

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

## <a name="dataset-properties"></a>Veri kümesi özellikleri
Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi. Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri kümesi türleri için benzerdir.

Merhaba **typeProperties** bölümü, her veri kümesi türü için farklıdır. Belirli toohello veri kümesi türü olan bilgiler sağlar. Merhaba typeProperties bölüm türü veri kümesi için **FileShare** veri kümesine hello aşağıdaki özelliklere sahiptir:

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| folderPath |Alt yolu toohello klasörü. Kaçış karakteri kullanmak ' \ ' hello dize özel karakter. Bkz: [örnek bağlantılı hizmeti ve veri kümesi tanımları](#sample-linked-service-and-dataset-definitions) örnekleri için.<br/><br/>Bu özellik ile birleştirebilirsiniz **partitionBy** toohave klasör yolları dilimine göre başlangıç/bitiş tarih saatleri. |Evet |
| fileName |Hello Hello hello dosyasının adını belirtin **folderPath** hello tablo toorefer tooa belirli dosya hello klasöründeki istiyorsanız. Bu özellik için herhangi bir değer belirtmezseniz, hello tablo hello klasöründeki tooall dosyaları işaret eder.<br/><br/>FileName bir çıkış veri kümesi için belirtilmediğinde oluşturulan hello dosyasının hello adı Bu biçim aşağıdaki hello olacaktır: <br/><br/>Veriler. <Guid>.txt (örnek: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Hayır |
| fileFilter |Tüm dosyalar yerine hello folderPath dosyaları kümesini filtre toobe tooselect kullanılan belirtin.<br/><br/>İzin verilen değerler: `*` (birden çok karakter) ve `?` (tek bir karakter).<br/><br/>Örnek 1:`"fileFilter": "*.log"`<br/>Örnek 2:`"fileFilter": 2014-1-?.txt"`<br/><br/> fileFilter bir giriş FileShare veri kümesi için geçerlidir. Bu özellik ile HDFS desteklenmiyor. |Hayır |
| partitionedBy |partitionedBy kullanılan toospecify dinamik folderPath zaman serisi veri için dosya adı olabilir. Örneğin, her veri saat için parametreli folderPath. |Hayır |
| Biçimi | şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set hello **türü** biçimi tooone şu değerlerden biri altında özellik. Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler. <br><br> Çok istiyorsanız**olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında hello Biçim bölümü atlayın. |Hayır |
| Sıkıştırma | Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin. Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**. Desteklenen düzeyler: **Optimal** ve **en hızlı**. Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support). |Hayır |
| useBinaryTransfer |Belirtin olup ikili aktarım modunu kullanın. İkili mod ve false ASCII için true. Varsayılan değer: True. İlişkili bağlantılı hizmet türü türü olduğunda bu özellik yalnızca kullanılabilir: Ftp_sunucusu. |Hayır |

> [!NOTE]
> Dosya adı ve fileFilter aynı anda kullanılamaz.

### <a name="using-partionedby-property"></a>PartionedBy özelliğini kullanma
Merhaba önceki bölümünde belirtildiği gibi dinamik bir folderPath, zaman serisi veri partitionedBy ile dosya adını belirtebilirsiniz. Merhaba Data Factory makroları ve hello sistem değişkeni SliceStart, verilen veri dilimi için mantıksal süre hello belirtmek SliceEnd bunu yapabilirsiniz.

Zaman serisi veri kümeleri, zamanlama ve dilimleri hakkında toolearn bkz [veri kümeleri oluşturma](data-factory-create-datasets.md), [zamanlama ve yürütme](data-factory-scheduling-and-execution.md), ve [oluşturma ardışık düzen](data-factory-create-pipelines.md) makaleleri.

#### <a name="sample-1"></a>Örnek 1:

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
Bu örnekte {dilim} belirtilen hello Data Factory sistem değişkenin değerini SliceStart hello biçiminde (YYYYMMDDHH) ile değiştirilir. Merhaba SliceStart hello dilim toostart süresini ifade eder. Merhaba folderPath her dilim için farklıdır. Örnek: wikidatagateway/wikisampledataout/2014100103 veya wikidatagateway/wikisampledataout/2014100104.

#### <a name="sample-2"></a>Örnek 2:

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
Bu örnekte, folderPath ve fileName özellikleri tarafından kullanılan ayrı değişkenleri içine yıl, ay, gün ve saat SliceStart ayıklanır.

## <a name="copy-activity-properties"></a>Etkinlik özellikleri Kopyala
Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi. Ad, açıklama, giriş ve çıkış tabloları ve ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir.

Oysa Hello özellikler kullanılabilir hello etkinlik hello typeProperties bölümünde her etkinlik türü ile farklılık gösterir. Kopya etkinliği için hello türü özellikleri hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.

[!INCLUDE [data-factory-file-system-source](../../includes/data-factory-file-system-source.md)]

## <a name="supported-file-and-compression-formats"></a>Desteklenen dosya ve sıkıştırma biçimleri
Bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md) makale ayrıntıları.

## <a name="json-example-copy-data-from-sftp-server-tooazure-blob"></a>JSON örnek: Verilerini SFTP sunucu tooAzure blob
Merhaba aşağıdaki örnek örnek JSON tanımları sağlar, toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Bunların nasıl SFTP toocopy verileri tooAzure Blob Depolama kaynağı gösterir. Ancak, veriler kopyalanabilir **doğrudan** herhangi birinden belirtildiği hello havuzlarını, kaynakları tooany [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.

> [!IMPORTANT]
> Bu örnek, JSON parçacıklarını sağlar. Merhaba veri fabrikası oluşturma için yönergeler içermez. Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale adım adım yönergeler için.

Merhaba örnek data factory varlıklarını aşağıdaki hello sahiptir:

* Bağlı hizmet türü [sftp](#linked-service-properties).
* Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Bir giriş [dataset](data-factory-create-datasets.md) türü [FileShare](#dataset-properties).
* Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [FileSystemSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Merhaba örnek verileri saatte bir SFTP server tooan Azure blob kopyalar. Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.

**SFTP bağlı hizmet**

Bu örnekte, kullanıcı adı ve parola düz metin hello temel kimlik doğrulaması kullanır. Aşağıdaki şekilde hello birini de kullanabilirsiniz:

* Şifrelenmiş kimlik bilgileri ile temel kimlik doğrulaması
* SSH ortak anahtar kimlik doğrulaması

Bkz: [FTP bağlantılı hizmeti](#linked-service-properties) bölümü için farklı tür kimlik doğrulaması kullanabilirsiniz.

```JSON

{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "myuser",
            "password": "mypassword",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```
**Azure Storage bağlı hizmeti**

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
**SFTP girdi veri kümesi**

Bu veri kümesi toohello SFTP klasörü işaret ediyor `mysharedfolder` ve dosya `test.csv`. Merhaba ardışık düzen hello dosya toohello hedef kopyalar.

"Dış" ayarı: "true" bildirir hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.

```JSON
{
  "name": "SFTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "SftpLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Azure Blob dataset çıktı**

Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1). hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir. Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Kopyalama etkinliği ile kanalı**

Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**FileSystemSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**.

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
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
        "start": "2017-02-20T18:00:00Z",
        "end": "2017-02-20T19:00:00Z"
    }
}
```

## <a name="performance-and-tuning"></a>Performans ve ayarlama
Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.

## <a name="next-steps"></a>Sonraki Adımlar
Aşağıdaki makaleleri hello bakın:

* [Kopya etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) kopyalama etkinliği ile işlem hattı oluşturmak için adım adım yönergeler için.
