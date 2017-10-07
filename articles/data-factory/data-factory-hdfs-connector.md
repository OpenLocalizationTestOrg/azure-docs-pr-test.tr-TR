---
title: "Şirket içi HDFS aaaMove verilerden | Microsoft Docs"
description: "Nasıl toomove verileri HDFS Azure Data Factory kullanarak şirket içi hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3215b82d-291a-46db-8478-eac1a3219614
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 96387e5dd089099fc2e983ab26d67c2044b973b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a>Azure Data Factory kullanarak şirket içi HDFS taşıma verileri
Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove verileri bir şirket içi HDFS de açıklanmaktadır. Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.

Verileri HDFS desteklenen tooany havuz veri deposundan kopyalayabilirsiniz. Verileri bir listesi için desteklenen depoları hello kopyalama etkinliği tarafından havuzlarını hello görür [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo. Veri Fabrikası şu anda bir şirket içi HDFS tooother veri depolarına yalnızca taşıma verilerden destekler, ancak verileri diğer veriler taşıma değil için depoları tooan HDFS şirket.

> [!NOTE]
> Başarıyla kopyalanan toohello hedef tamamlandıktan sonra kopyalama etkinliği hello kaynak dosyayı silmez. Sonra başarılı bir kopyasını toodelete hello kaynak dosyası gerekiyorsa, bir özel etkinlik toodelete hello dosyası oluşturun ve hello ardışık düzeninde hello etkinliği kullanın. 

## <a name="enabling-connectivity"></a>Bağlantıyı etkinleştirme
Data Factory Hizmeti'ne hello veri yönetimi ağ geçidi kullanarak bağlanan tooon içi HDFS destekler. Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale toolearn veri yönetimi ağ geçidi ve hello ağ geçidi kurun ayarlama hakkında adım adım yönergeleri hakkında. Bir Azure Iaas sanal barındırılan olsa bile hello ağ geçidi tooconnect tooHDFS kullanın.

> [!NOTE]
> Veri Yönetimi ağ geçidi çok erişebilir yapma emin hello**tüm** hello [ad düğümü sunucusu]: [name düğümü bağlantı noktası] ve [veri düğümü sunucuları]: [veri düğümü bağlantı noktası] hello Hadoop kümesi. [Adı düğümü bağlantı noktası] 50070 varsayılandır ve [veri düğümü bağlantı noktası] 50075 varsayılandır.

Ağ geçidi üzerinde hello yükleyebilirsiniz sırasında aynı makine ya da hello Azure VM HDFS hello gibi şirket içi, bir ayrı makine/Azure Iaas VM hello ağ geçidi yüklemenizi öneririz. Ağ geçidi ayrı bir makinede sahip kaynak çekişmesini azaltır ve performansı artırır. Merhaba ağ geçidi ayrı bir makineye yüklediğinizde hello makine mümkün tooaccess hello hello HDFS makineyle olmalıdır.

## <a name="getting-started"></a>Başlarken
Farklı araçlar/API'lerini kullanarak verileri HDFS kaynağından taşır kopyalama etkinliği ile işlem hattı oluşturun.

Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**. Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.

Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**. Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.

Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:

1. Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.
2. Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.
3. Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.

Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur. Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.  HDFS veri deposundan kullanılan toocopy verileri Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: şirket içi HDFS tooAzure Blob veri kopyalama](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) bu makalenin.

Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooHDFS olan JSON özellikleri hakkında ayrıntılı bilgi sağlar:

## <a name="linked-service-properties"></a>Bağlantılı hizmet özellikleri
Bağlı hizmet, bir veri deposu tooa veri fabrikası bağlar. Bağlı hizmet türü oluşturma **Hdfs** toolink bir şirket içi HDFS tooyour data factory. Aşağıdaki tablonun hello JSON öğeleri belirli tooHDFS bağlantılı hizmeti için bir açıklama sağlar.

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| type |Merhaba type özelliği ayarlanmalıdır: **Hdfs** |Evet |
| Url |URL toohello HDFS |Evet |
| authenticationType |Anonim veya Windows. <br><br> toouse **Kerberos kimlik doğrulaması** HDFS bağlayıcı için çok başvuran[Bu bölümde](#use-kerberos-authentication-for-hdfs-connector) tooset şirket içi ortamınızı uygun şekilde. |Evet |
| Kullanıcı adı |Kullanıcı adı için Windows kimlik doğrulaması. |Evet (Windows kimlik doğrulaması için) |
| password |Windows kimlik doğrulaması için parola. |Evet (Windows kimlik doğrulaması için) |
| gatewayName |Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello HDFS kullanmanız gerekir. |Evet |
| encryptedCredential |[AzureRMDataFactoryEncryptValue yeni](https://msdn.microsoft.com/library/mt603802.aspx) hello erişim kimlik bilgisi çıktısı. |Hayır |

### <a name="using-anonymous-authentication"></a>Anonim kimlik doğrulamasını kullanma

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-windows-authentication"></a>Windows kimlik doğrulaması kullanma

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```
## <a name="dataset-properties"></a>Veri kümesi özellikleri
Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi. Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.

Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar. Merhaba typeProperties bölüm türü veri kümesi için **FileShare** hello aşağıdaki özelliklere sahip (HDFS dataset içerir)

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| folderPath |Yol toohello klasör. Örnek:`myfolder`<br/><br/>Kaçış karakteri kullanmak ' \ ' hello dize özel karakter. Örneğin: folder\subfolder için klasör belirtin\\\\alt ve d:\samplefolder için d: belirtin\\\\ÖrnekKlasör.<br/><br/>Bu özellik ile birleştirebilirsiniz **partitionBy** toohave klasör yolları dilimine göre başlangıç/bitiş tarih saatleri. |Evet |
| fileName |Hello Hello hello dosyasının adını belirtin **folderPath** hello tablo toorefer tooa belirli dosya hello klasöründeki istiyorsanız. Bu özellik için herhangi bir değer belirtmezseniz, hello tablo hello klasöründeki tooall dosyaları işaret eder.<br/><br/>FileName bir çıkış veri kümesi için belirtilmediğinde oluşturulan hello dosyasının hello adı Bu biçim aşağıdaki hello olacaktır: <br/><br/>Veriler. <Guid>.txt (örnek:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Hayır |
| partitionedBy |partitionedBy kullanılan toospecify dinamik folderPath zaman serisi veri için dosya adı olabilir. Örnek: veri her saat için parametreli folderPath. |Hayır |
| Biçimi | şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set hello **türü** biçimi tooone şu değerlerden biri altında özellik. Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler. <br><br> Çok istiyorsanız**olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında hello Biçim bölümü atlayın. |Hayır |
| Sıkıştırma | Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin. Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**. Desteklenen düzeyler: **Optimal** ve **en hızlı**. Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support). |Hayır |

> [!NOTE]
> Dosya adı ve fileFilter aynı anda kullanılamaz.

### <a name="using-partionedby-property"></a>PartionedBy özelliğini kullanma
Merhaba önceki bölümünde belirtildiği gibi bir dinamik folderPath ve zaman serisi verileri için dosya adı ile Merhaba belirtebilirsiniz **partitionedBy** özelliği, [Data Factory işlevler ve hello sistem değişkenleri](data-factory-functions-variables.md).

Zaman serisi veri kümeleri, zamanlama ve dilimleri hakkında daha fazla toolearn bkz [veri kümeleri oluşturma](data-factory-create-datasets.md), [zamanlama ve yürütme](data-factory-scheduling-and-execution.md), ve [oluşturma ardışık düzen](data-factory-create-pipelines.md) makaleleri.

#### <a name="sample-1"></a>Örnek 1:

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
Bu örnekte {dilim} belirtilen hello Data Factory sistem değişkenin değerini SliceStart hello biçiminde (YYYYMMDDHH) ile değiştirilir. Merhaba SliceStart hello dilim toostart süresini ifade eder. Merhaba folderPath her dilim için farklıdır. Örneğin: wikidatagateway/wikisampledataout/2014100103 veya wikidatagateway/wikisampledataout/2014100104.

#### <a name="sample-2"></a>Örnek 2:

```JSON
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

Oysa hello typeProperties bölümünde hello etkinlik özellikleri her etkinlik türü ile farklılık gösterir. Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.

Kopyalama kaynağı türü olduğunda etkinliği için **FileSystemSource** aşağıdaki özelliklere hello typeProperties bölümünde bulunur:

**FileSystemSource** aşağıdaki özelliklere hello destekler:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| Özyinelemeli |Merhaba alt klasörler veya yalnızca hello belirtilen klasör Hello veri yinelemeli olarak okunur olup olmadığını gösterir. |TRUE, False (varsayılan) |Hayır |

## <a name="supported-file-and-compression-formats"></a>Desteklenen dosya ve sıkıştırma biçimleri
Bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md) makale ayrıntıları.

## <a name="json-example-copy-data-from-on-premises-hdfs-tooazure-blob"></a>JSON örnek: şirket içi HDFS tooAzure Blob veri kopyalama
Bu örnek göstermektedir nasıl bir şirket içi HDFS tooAzure Blob Storage toocopy verileri. Ancak, veriler kopyalanabilir **doğrudan** belirtildiği hello havuzlarını tooany [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.  

Merhaba örnek Data Factory varlıklarını aşağıdaki hello için JSON tanımları sağlar. Bu tanımları toocreate bir ardışık düzen toocopy verileri HDFS tooAzure Blob Storage kullanarak kullanabileceğiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).

1. Bağlı hizmet türü [OnPremisesHdfs](#linked-service-properties).
2. Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Bir giriş [dataset](data-factory-create-datasets.md) türü [FileShare](#dataset-properties).
4. Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [FileSystemSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Merhaba örnek verileri saatte bir şirket içi HDFS tooan Azure blob kopyalar. Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.

İlk adım olarak, hello veri yönetimi ağ geçidi ayarlayın. Merhaba hello'ndaki yönergeleri [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.

**HDFS bağlantılı hizmeti:** kullandığı hello Windows kimlik doğrulaması Bu örnek. Bkz: [HDFS bağlantılı hizmeti](#linked-service-properties) bölümü için farklı tür kimlik doğrulaması kullanabilirsiniz.

```JSON
{
    "name": "HDFSLinkedService",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

**Azure Storage bağlı hizmeti:**

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

**HDFS giriş veri kümesi:** toohello HDFS klasörü DataTransfer/UnitTest bu veri kümesine başvuruyor /. Hello ardışık tüm hello dosyalarını bu klasöre toohello hedef kopyalar.

"Dış" ayarı: "true" bildirir hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.

```JSON
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

**Azure Blob dataset çıktı:**

Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1). hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir. Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.

```JSON
{
    "name": "OutputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/hdfs/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Dosya sistemi kaynak ve Blob havuz sahip işlem hattı kopyalama etkinliğinde:**

Merhaba ardışık düzen içeren bir kopyalama etkinliği, yapılandırılmış toouse bu girdi ve çıktı veri kümeleri ve zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**FileSystemSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**. Merhaba belirtilen hello SQL sorgusu **sorgu** özelliği saat toocopy geçmiş hello hello veri seçer.

```JSON
{
    "name": "pipeline",
    "properties":
    {
        "activities":
        [
            {
                "name": "HdfsToBlobCopy",
                "inputs": [ {"name": "InputDataset"} ],
                "outputs": [ {"name": "OutputDataset"} ],
                "type": "Copy",
                "typeProperties":
                {
                    "source":
                    {
                        "type": "FileSystemSource"
                    },
                    "sink":
                    {
                        "type": "BlobSink"
                    }
                },
                "policy":
                {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "00:05:00"
                }
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="use-kerberos-authentication-for-hdfs-connector"></a>HDFS Bağlayıcısı için Kerberos kimlik doğrulamasını kullan
HDFS Bağlayıcısı toouse Kerberos kimlik doğrulaması olarak şekilde hello şirket içi çevresi iki seçenekleri tooset vardır. Merhaba bir durumunuz daha iyi uyduğunu seçebilirsiniz.
* Seçenek 1: [birleştirme ağ geçidi makinesiyle Kerberos alanı](#kerberos-join-realm)
* Seçenek 2: [Windows etki alanı Kerberos alanı arasında karşılıklı güven etkinleştir](#kerberos-mutual-trust)

### <a name="kerberos-join-realm"></a>Seçenek 1: ağ geçidi makinesi Kerberos bölgesinde katılın.

#### <a name="requirement"></a>Gereksinim:

* Merhaba ağ geçidi makinesi toojoin hello Kerberos alanı gerektiriyor ve herhangi bir Windows etki alanına katılamıyor.

#### <a name="how-tooconfigure"></a>Nasıl tooconfigure:

**Ağ geçidi makinede:**

1.  Merhaba çalıştırmak **Ksetup** yardımcı programı tooconfigure hello Kerberos KDC sunucu ve bölge.

    Kerberos alanı bir Windows etki alanından farklı olduğundan hello makine bir çalışma grubunun bir üyesi yapılandırılmalıdır. Bu işlem, hello Kerberos alanı ayarlama ve şu şekilde bir KDC sunucusu eklemeyi de yararlanılabilir. Değiştir *REALM.COM* gerektiği gibi ilgili kendi bölge ile.

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    **Yeniden** hello makineyi 2 Bu komutları yürütülürken sonra.

2.  Merhaba yapılandırmayla doğrulayın **Ksetup** komutu. Merhaba çıktısı gibi olmalıdır:

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

**Azure Data Factory'de:**

* Merhaba HDFS Bağlayıcısı'nı kullanarak yapılandırma **Windows kimlik doğrulaması** Kerberos asıl adı ve parola tooconnect toohello HDFS veri kaynağınız ile birlikte. Denetleme [HDFS bağlantılı hizmet özellikleri](#linked-service-properties) yapılandırma ayrıntıları bölümü.

### <a name="kerberos-mutual-trust"></a>Seçenek 2: Windows etki alanı Kerberos alanı arasında karşılıklı güven etkinleştirme

#### <a name="requirement"></a>Gereksinim:
*   Merhaba ağ geçidi makinesi bir Windows etki alanına katılması gerekir.
*   İzni tooupdate hello etki alanı denetleyicisinin ayarlarının gerekir.

#### <a name="how-tooconfigure"></a>Nasıl tooconfigure:

> [!NOTE]
> REALM.COM ve AD.COM gerektiği gibi ilgili kendi bölge ve etki alanı denetleyicisi bu öğreticiyi izleyerek hello değiştirin.

**KDC sunucusunda:**

1.  Merhaba KDC yapılandırmasında Düzenle **krb5.conf** dosya toolet KDC Windows yapılandırma şablonu aşağıdaki toohello başvuran etki alanı güven. Varsayılan olarak, hello yapılandırması bulunur **/etc/krb5.conf**.

            [logging]
             default = FILE:/var/log/krb5libs.log
             kdc = FILE:/var/log/krb5kdc.log
             admin_server = FILE:/var/log/kadmind.log

            [libdefaults]
             default_realm = REALM.COM
             dns_lookup_realm = false
             dns_lookup_kdc = false
             ticket_lifetime = 24h
             renew_lifetime = 7d
             forwardable = true

            [realms]
             REALM.COM = {
              kdc = node.REALM.COM
              admin_server = node.REALM.COM
             }
            AD.COM = {
             kdc = windc.ad.com
             admin_server = windc.ad.com
            }

            [domain_realm]
             .REALM.COM = REALM.COM
             REALM.COM = REALM.COM
             .ad.com = AD.COM
             ad.com = AD.COM

            [capaths]
             AD.COM = {
              REALM.COM = .
             }

  **Yeniden** hello KDC Hizmeti yapılandırmasından sonra.

2.  Adlı bir asıl hazırlama  **krbtgt/REALM.COM@AD.COM**  komutu aşağıdaki hello ile KDC Server'daki:

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  İçinde **hadoop.security.auth_to_local** HDFS hizmet yapılandırma dosyası, ekleme `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.

**Etki alanı denetleyicisinde:**

1.  Merhaba aşağıdaki komutu çalıştırarak **Ksetup** tooadd bir bölge girişi komutlar:

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  Windows etki alanı tooKerberos bölge gelen güven oluşturun. [paroladır] hello asıl hello parolasını  **krbtgt/REALM.COM@AD.COM** .

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  İçinde Kerberos kullanılan şifreleme algoritmasını seçin.

    1. TooServer Yöneticisi Git > Grup İlkesi Yönetimi > etki alanı > Grup İlkesi nesneleri > Varsayılan veya etkin etki alanı ilkesi ve düzenleyin.

    2. Merhaba, **Grup İlkesi Yönetimi Düzenleyicisi** açılan pencerede, Git tooComputer yapılandırma > ilkeler > Windows Ayarları > Güvenlik Ayarları > yerel ilkeler > güvenlik seçenekleri ve yapılandırma **ağ Güvenlik: Kerberos için izin verilen şifreleme türleri yapılandırma**.

    3. Select hello şifreleme algoritması toouse istediğiniz tooKDC bağladığınızda. Genellikle, yalnızca tüm hello seçeneklerini belirleyebilirsiniz.

        ![Kerberos için yapılandırma şifreleme türleri](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. Kullanım **Ksetup** komutu toospecify hello şifreleme algoritması toobe hello üzerinde kullanılan belirli bölgesi.

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  Merhaba etki alanı hesabını ve Kerberos arasında Hello eşleme sipariş toouse Windows etki alanında Kerberos asıl asıl oluşturun.

    1. Merhaba yönetimsel araçları başlatmak > **Active Directory Kullanıcıları ve Bilgisayarları**.

    2. Tıklayarak Gelişmiş özellikleri yapılandırma **Görünüm** > **Gelişmiş Özellikler**.

    3. Toocreate eşlemeleri istediğiniz ve tooview sağ hello hesap toowhich bulun **adı eşlemeleri** > tıklatın **Kerberos adları** sekmesi.

    4. Sorumlu hello Bölgesi ' ekleyin.

        ![Güvenlik kimliğine eşleyin](media/data-factory-hdfs-connector/map-security-identity.png)

**Ağ geçidi makinede:**

* Merhaba aşağıdaki komutu çalıştırarak **Ksetup** tooadd bir bölge girişi komutları.

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

**Azure Data Factory'de:**

* Merhaba HDFS Bağlayıcısı'nı kullanarak yapılandırma **Windows kimlik doğrulaması** etki alanı hesabı veya Kerberos asıl tooconnect toohello HDFS veri kaynağı ile birlikte. Denetleme [HDFS bağlantılı hizmet özellikleri](#linked-service-properties) yapılandırma ayrıntıları bölümü.

> [!NOTE]
> Kaynak veri kümesi toocolumns havuz kümesinden toomap sütunlarından bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).


## <a name="performance-and-tuning"></a>Performans ve ayarlama
Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.
