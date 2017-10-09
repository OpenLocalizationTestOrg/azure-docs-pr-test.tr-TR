---
title: Azure Blob Storage/aaaCopy verileri | Microsoft Docs
description: "Nasıl toocopy blob Azure Data Factory veri öğrenin. Bizim örnek kullanın: nasıl toocopy veri tooand Azure Blob Storage ve Azure SQL veritabanı."
keywords: BLOB verilerini, azure blob kopyalama
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: bec8160f-5e07-47e4-8ee1-ebb14cfb805d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 8428c64e8e8b1084b3f2f680c4e1819559e4ffa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooor-from-azure-blob-storage-using-azure-data-factory"></a>Azure Data Factory kullanarak Azure Blob depolama alanından veri tooor kopyalama
Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toocopy veri tooand Azure Blob depolama biriminden de açıklanmaktadır. Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.

## <a name="overview"></a>Genel Bakış
Veri depolamak tooAzure Blob Storage veya Azure Blob Storage desteklenen tooany havuz verileri depolamak herhangi desteklenen bir kaynaktan veri kopyalayabilirsiniz. Merhaba aşağıdaki tabloda kaynakları olarak desteklenen veri depoları listesini sağlar veya tarafından hello kopyalama etkinliği iç havuzlar. Örneğin, veri taşıyabilirsiniz **gelen** bir SQL Server veritabanı veya bir Azure SQL veritabanı **için** Azure blob depolama. Ve veri kopyalayabilirsiniz **gelen** Azure blob depolama **için** Azure SQL Data Warehouse veya bir Azure Cosmos DB koleksiyonu. 

## <a name="supported-scenarios"></a>Desteklenen senaryolar
Veri kopyalama **Azure Blob depolama biriminden** veri depolarına aşağıdaki toohello:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Veri depoları aşağıdaki hello verileri kopyalayabilirsiniz **tooAzure Blob Storage**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> Kopyalama etkinliği destekleyen kopyalama verilerden / tooboth genel amaçlı Azure depolama hesapları ve sık erişimli/seyrek erişimli Blob Depolama. Merhaba etkinlik destekler **bloğundan okuma, ekleme veya sayfa blobları**, ancak destekleyen **tooonly blok blobları yazma**. Sayfa blobları tarafından yedeklenen olduğundan azure Premium depolama havuzu olarak desteklenmiyor.
> 
> Veri başarıyla olduğundan hello toohello hedef kopyalandıktan sonra kopyalama etkinliği hello kaynaktan verileri silmez. Sonra başarılı bir kopyasını toodelete kaynak verilere ihtiyacınız varsa oluşturma bir [özel etkinlik](data-factory-use-custom-activities.md) toodelete hello veri ve hello ardışık düzeninde hello etkinliği kullanın. Merhaba bir örnek için bkz: [Delete blob veya klasör örneği github'daki](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity). 

## <a name="get-started"></a>başlarken
Farklı araçlar/API'lerini kullanarak verileri Azure Blob Storage/gruptan taşır kopyalama etkinliği ile işlem hattı oluşturun.

Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**. Bu makalede sahip bir [izlenecek](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) bir Azure Blob Depolama konumu tooanother Azure Blob depolama konumunu bir ardışık düzen toocopy verileri oluşturmak için. Ardışık Düzen toocopy veri bir Azure Blob Storage tooAzure SQL veritabanı oluşturma, Öğretici için bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md).

Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**. Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.

Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:

1. Oluşturma bir **veri fabrikası**. Veri Fabrikası bir veya daha fazla ardışık düzen içerebilir. 
2. Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası. Bir Azure blob depolama tooan Azure SQL veritabanından veri kopyalama, örneğin, iki bağlı hizmet toolink Azure depolama hesabınız ve Azure SQL veritabanı tooyour veri fabrikası oluşturun. Belirli tooAzure Blob Storage bağlı hizmeti özellikler için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü. 
2. Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi. Merhaba son adımda bahsedilen hello örnekte, bir veri kümesi toospecify hello blob kapsayıcısı ve hello giriş verisi içeren klasörü oluşturun. Ve hello blob depolama biriminden kopyalanan hello verilerini tutan hello Azure SQL veritabanında başka bir veri kümesi toospecify hello SQL tablo oluşturun. Belirli tooAzure Blob Storage veri kümesi özellikler için bkz: [veri kümesi özellikleri](#dataset-properties) bölümü.
3. Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile. Daha önce bahsedilen hello örnekte BlobSource bir kaynak ve SqlSink havuzu olarak hello kopya etkinliği için kullanırsınız. Azure SQL veritabanı tooAzure Blob Depolama kopyalıyorsanız benzer şekilde, SqlSource ve BlobSink hello kopyalama etkinliği kullanırsınız. Belirli tooAzure Blob Storage kopyalama etkinliği özellikler için bkz: [kopyalama etkinliği özellikleri](#copy-activity-properties) bölümü. Nasıl toouse bir veri deposu bir kaynak veya bir havuz olarak hakkında daha fazla bilgi için veri deposu hello önceki bölümdeki hello bağlantısına tıklayın.  

Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur. Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.  Kullanılan toocopy verileri Azure Blob Storage/Data Factory varlıkları için JSON tanımlarıyla örnekleri için bkz: [JSON örnekler](#json-examples-for-copying-data-to-and-from-blob-storage  ) bu makalenin.

Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooAzure Blob Storage JSON özellikleri hakkında ayrıntılı bilgiler sağlar.

## <a name="linked-service-properties"></a>Bağlantılı hizmet özellikleri
İki tür vardır bağlı hizmetler Azure Storage tooan Azure data factory toolink kullanabilirsiniz. Bunlar: **AzureStorage** bağlantılı hizmeti ve **AzureStorageSas** bağlı hizmeti. Hello Azure Storage bağlı hizmeti hello data factory genel erişim toohello Azure Storage ile sağlar. Hello Azure depolama SAS (paylaşılan erişim imzası) bağlı ise hello data factory ile sınırlı/zaman sınırlı erişim toohello Azure depolama hizmeti sağlar. Bu iki bağlı hizmet arasındaki herhangi bir fark vardır. Gereksinimlerinize uygun hello bağlı hizmeti seçin. Merhaba aşağıdaki bölümlerde daha fazla ayrıntı bu iki bağlı hizmet sağlar.

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a>Veri kümesi özellikleri
toospecify dataset toorepresent giriş veya çıkış verileri Azure Blob Depolama hello türü özelliği için hello kümesinin ayarlayın: **AzureBlob**. Set hello **linkedServiceName** özelliği hello dataset toohello adının hello Azure Storage veya Azure depolama SAS bağlantılı hizmeti.  Merhaba kümesinin Hello türü özellikleri belirtin hello **blob kapsayıcısı** ve hello **klasörü** hello blob depolama.

Merhaba JSON bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi. Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.

Veri Fabrikası yapısındaki"" şema üzerinde okuma veri kaynakları için Azure blob gibi türü bilgileri sağlamak için temel CLS uyumlu .NET türü değerleri aşağıdaki hello destekler: Int16, Int32, Int64, tek, Double, Decimal, Byte [], Bool, dize, GUID, Datetime, Datetimeoffset, Timespan. Veri Fabrikası otomatik olarak veri kaynağına veri dosyaları tooa havuz veri deposunu taşırken tür dönüşümleri gerçekleştirir.

Merhaba **typeProperties** bölüm bilgileri sağlar ve her veri kümesi türü için farklı hello konumu hakkında hello veri hello veri deposundaki vb., biçimlendirme. Merhaba typeProperties bölüm türü veri kümesi için **AzureBlob** veri kümesine hello aşağıdaki özelliklere sahiptir:

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| folderPath |Yol toohello kapsayıcı ve klasöre hello blob depolama. Örnek: myblobcontainer\myblobfolder\ |Evet |
| fileName |Merhaba blob adı. isteğe bağlıdır ve büyük küçük harfe duyarlı dosya adıdır.<br/><br/>Üzerinde bir dosya adı, hello (kopyalama dahil) etkinlik works belirtirseniz, belirli Blob hello.<br/><br/>FileName belirtilmediğinde kopyalama tüm BLOB'lar girdi veri kümesi için hello folderPath içerir.<br/><br/>Zaman **fileName** bir çıkış veri kümesi için belirtilmemiş ve **preserveHierarchy** belirtilmedi etkinlik havuzunda oluşturulan hello dosyasının hello adı, bu biçim aşağıdaki hello olacaktır: veri.<Guid>. txt (örneğin:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Hayır |
| partitionedBy |partitionedBy isteğe bağlı bir özelliktir. Bunu toospecify dinamik folderPath ve dosya adı için zaman serisi veri kullanabilirsiniz. Örneğin, folderPath için verileri saatte parametreli olabilir. Merhaba bkz [partitionedBy özellik bölümünü kullanarak](#using-partitionedBy-property) ayrıntı ve örnekler için. |Hayır |
| Biçimi | şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set hello **türü** biçimi tooone şu değerlerden biri altında özellik. Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler. <br><br> Çok istiyorsanız**olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında hello Biçim bölümü atlayın. |Hayır |
| Sıkıştırma | Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin. Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**. Desteklenen düzeyler: **Optimal** ve **en hızlı**. Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support). |Hayır |

### <a name="using-partitionedby-property"></a>PartitionedBy özelliğini kullanma
Merhaba önceki bölümünde belirtildiği gibi bir dinamik folderPath ve zaman serisi verileri için dosya adı ile Merhaba belirtebilirsiniz **partitionedBy** özelliği, [Data Factory işlevler ve hello sistem değişkenleri](data-factory-functions-variables.md).

Zaman serisi veri kümeleri, zamanlama ve dilimleri hakkında daha fazla bilgi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md) ve [zamanlama ve yürütme](data-factory-scheduling-and-execution.md) makaleleri.

#### <a name="sample-1"></a>Örnek 1

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

Bu örnekte, {dilim} belirtilen hello Data Factory sistem değişkenin değerini SliceStart hello biçiminde (YYYYMMDDHH) ile değiştirilir. Merhaba SliceStart hello dilim toostart süresini ifade eder. Merhaba folderPath her dilim için farklıdır. Örneğin: wikidatagateway/wikisampledataout/2014100103 veya wikidatagateway/wikisampledataout/2014100104

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

Bu örnekte, folderPath ve fileName özellikleri tarafından kullanılan ayrı değişkenleri içine yıl, ay, gün ve saat SliceStart ayıklanır.

## <a name="copy-activity-properties"></a>Etkinlik özellikleri Kopyala
Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi. Ad, açıklama, giriş ve çıkış veri kümeleri ve ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir. Oysa hello kullanılabilen özellikleri **typeProperties** hello etkinlik bölümünü her etkinlik türü ile değişir. Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir. Bir Azure Blob depolama alanından veri taşıyorsanız, hello kaynak türü hello kopyalama etkinliği çok ayarladığınız**BlobSource**. Veri tooan Azure Blob Storage taşıyorsanız, benzer şekilde, hello Havuz türü hello kopyalama etkinliği çok ayarladığınız**BlobSink**. Bu bölümde BlobSource ve BlobSink tarafından desteklenen özellikler listesini sağlar.

**BlobSource** hello özelliklerinde aşağıdaki hello destekleyen **typeProperties** bölümü:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| Özyinelemeli |Merhaba alt klasörler veya yalnızca hello belirtilen klasör Hello veri yinelemeli olarak okunur olup olmadığını gösterir. |(Varsayılan değer) false değerini true |Hayır |

**BlobSink** aşağıdaki özelliklere hello destekleyen **typeProperties** bölümü:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| copyBehavior |Merhaba kaynağı BlobSource veya dosya sistemi olduğunda hello kopyalama davranışını tanımlar. |<b>PreserveHierarchy</b>: korur hello hello hedef klasörü içinde dosya hiyerarşisi. Kaynak dosya toosource klasörünün göreli yolu Hello aynı toohello göreli hedef dosya tootarget klasör yoludur.<br/><br/><b>FlattenHierarchy</b>: hello kaynak klasördeki tüm dosyaları hello ilk hedef klasörü düzeyi. Merhaba hedef dosyalara otomatik adına sahip. <br/><br/><b>MergeFiles</b>: hello kaynak klasör tooone dosyasından tüm dosyaları birleştirir. Merhaba dosya/Blob adı belirtilirse, hello birleştirilmiş dosya adı hello belirtilen adı olur; Aksi takdirde otomatik olarak oluşturulan dosya adı olacaktır. |Hayır |

**BlobSource** geriye dönük uyumluluk için bu iki özellik de destekler.

* **treatEmptyAsNull**: belirtir olup olmadığını tootreat null veya boş dize olarak null değer.
* **skipHeaderLineCount** -kaç satır atlandı belirtir. Yalnızca girdi veri kümesi TextFormat kullandığında geçerli olduğu.

Benzer şekilde, **BlobSink** özelliği geriye dönük uyumluluk için aşağıdaki hello destekler.

* **blobWriterAddHeader**: tooadd tooan yazılırken sütun tanımları üstbilgisinin veri kümesini çıktı olup olmadığını belirtir.

Veri kümeleri şimdi destek hello aşağıdaki uygulamak özelliklere hello aynı işlevselliği: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.

Merhaba aşağıdaki tabloda bu blob kaynak/havuz özellikleri yerine hello yeni veri kümesi özellikleri kullanma hakkında yönergeler sunmaktadır.

| Kopya etkinliği özelliği | Veri kümesi özelliği |
|:--- |:--- |
| BlobSource üzerinde skipHeaderLineCount |skipLineCount ve firstRowAsHeader. Satırlar ilk atlanır ve hello ilk satırın üstbilgi olarak sonra okuyun. |
| BlobSource üzerinde treatEmptyAsNull |girdi veri kümesi üzerinde treatEmptyAsNull |
| BlobSink üzerinde blobWriterAddHeader |Çıktı veri kümesi üzerinde firstRowAsHeader |

Bkz: [belirtme TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) bu özellikleri hakkında ayrıntılı bilgi için bölüm.    

### <a name="recursive-and-copybehavior-examples"></a>özyinelemeli ve copyBehavior örnekleri
Bu bölümde hello kopyalama işlemi farklı bir özyinelemeli ve copyBehavior değerleri kombinasyonu için sonuçta elde edilen davranışını hello açıklanmaktadır.

| Özyinelemeli | copyBehavior | Bunun sonucunda oluşan davranışı |
| --- | --- | --- |
| TRUE |preserveHierarchy |Bir kaynak klasörü için Klasör1 yapı izlenerek hello ile: <br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Merhaba hedef klasör Klasör1 aynı hello kaynağı olarak yapısı hello oluşturulur<br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5. |
| TRUE |flattenHierarchy |Bir kaynak klasörü için Klasör1 yapı izlenerek hello ile: <br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Merhaba hedef Klasör1 yapı izlenerek hello ile oluşturulur: <br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;dosya1 için otomatik olarak oluşturulan adı<br/>&nbsp;&nbsp;&nbsp;&nbsp;dosya2 için otomatik olarak oluşturulan adı<br/>&nbsp;&nbsp;&nbsp;&nbsp;dosya3 için otomatik olarak oluşturulan adı<br/>&nbsp;&nbsp;&nbsp;&nbsp;File4 için otomatik olarak oluşturulan adı<br/>&nbsp;&nbsp;&nbsp;&nbsp;File5 için otomatik olarak oluşturulan adı |
| TRUE |mergeFiles |Bir kaynak klasörü için Klasör1 yapı izlenerek hello ile: <br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Merhaba hedef Klasör1 yapı izlenerek hello ile oluşturulur: <br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya1 + dosya2 + dosya3 + File4 + 5 dosyası içeriği otomatik olarak oluşturulan dosya adında bir dosya halinde birleştirilir |
| False |preserveHierarchy |Bir kaynak klasörü için Klasör1 yapı izlenerek hello ile: <br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Merhaba hedef klasör Klasör1 yapı izlenerek hello ile oluşturulur<br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya2<br/><br/><br/>Dosya3, File4 ve File5 Subfolder1 değil toplanma. |
| False |flattenHierarchy |Bir kaynak klasörü için Klasör1 yapı izlenerek hello ile:<br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Merhaba hedef klasör Klasör1 yapı izlenerek hello ile oluşturulur<br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;dosya1 için otomatik olarak oluşturulan adı<br/>&nbsp;&nbsp;&nbsp;&nbsp;dosya2 için otomatik olarak oluşturulan adı<br/><br/><br/>Dosya3, File4 ve File5 Subfolder1 değil toplanma. |
| False |mergeFiles |Bir kaynak klasörü için Klasör1 yapı izlenerek hello ile:<br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Merhaba hedef klasör Klasör1 yapı izlenerek hello ile oluşturulur<br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya1 + dosya2 içeriği otomatik olarak oluşturulan dosya adında bir dosya halinde birleştirilir. dosya1 için otomatik olarak oluşturulan adı<br/><br/>Dosya3, File4 ve File5 Subfolder1 değil toplanma. |

## <a name="walkthrough-use-copy-wizard-toocopy-data-tofrom-blob-storage"></a>İzlenecek yol: Kopyalama Sihirbazı'nı kullan toocopy veri/Blob depolama biriminden
Nasıl tooquickly kopya verileri için/Azure blob depolama konumunda bakalım. Bu kılavuzda, hem kaynak hem de hedef veri türünü depolar: Azure Blob Storage. Merhaba ardışık düzen bu kılavuzda veri bir tooanother klasörü hello kopyalar aynı blob kapsayıcısı. Bu kılavuzda kasıtlı olarak basit tooshow olan ayarları veya Blob Depolama kaynağı veya havuz olarak kullanırken özellikleri. 

### <a name="prerequisites"></a>Ön koşullar
1. Bir genel amaçlı oluşturma **Azure depolama hesabı** zaten yoksa. Her iki biçimde hello blob storage kullanma **kaynak** ve **hedef** verileri depolamak bu kılavuzda. bir Azure depolama hesabınız yoksa, hello bkz [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) adımları toocreate bir makale.
2. Adlı bir blob kapsayıcı oluşturun **adfblobconnector** hello depolama hesabındaki. 
4. Adlı bir klasör oluşturun **giriş** hello içinde **adfblobconnector** kapsayıcı.
5. Adlı bir dosya oluşturun **emp.txt** aşağıdaki hello ile içerik ve toohello karşıya **giriş** gibi araçları kullanarak klasör [Azure Storage Gezgini](https://azurestorageexplorer.codeplex.com/)
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-hello-data-factory"></a>Merhaba veri fabrikası oluşturma
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Tıklatın **+ yeni** hello sol üst köşeden tıklatın **Intelligence + analiz**, tıklatıp **Data Factory**.
3. Merhaba, **yeni data factory** dikey penceresinde:   
    1. Girin **ADFBlobConnectorDF** hello için **adı**. Merhaba hello Azure veri fabrikasının adı genel olarak benzersiz olması gerekir. Merhaba hatayı alırsanız: `*Data factory name “ADFBlobConnectorDF” is not available`, hello veri fabrikası (örneğin, yournameADFBlobConnectorDF) hello adını değiştirin ve oluşturmayı yeniden deneyin. Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.
    2. Azure **aboneliğinizi** seçin.
    3. Kaynak grubu için seçin **kullanım varolan** tooselect bir var olan kaynak grubunu (veya) seçin **Yeni Oluştur** tooenter bir kaynak grubu için bir ad.
    4. Seçin bir **konumu** hello veri fabrikası için.
    5. Seçin **PIN toodashboard** hello dikey penceresinde hello altındaki onay kutusu.
    6. **Oluştur**'a tıklayın.
3. Merhaba oluşturma işlemi tamamlandıktan sonra hello bkz **Data Factory** hello görüntü aşağıdaki gösterildiği gibi dikey: ![Data factory giriş sayfası](./media/data-factory-azure-blob-connector/data-factory-home-page.png)

### <a name="copy-wizard"></a>Kopyalama Sihirbazı
1. Merhaba Hello Data Factory giriş sayfasında, tıklatın **kopyalama [Önizleme] verileri** toolaunch döşeme **kopyalama veri Sihirbazı** ayrı bir sekmede.    
    
    > [!NOTE]
    >    Bu hello web tarayıcısının "Yetkilendiriliyor..." takılmış görürseniz, devre dışı bırakın/işaretini kaldırın **üçüncü taraf tanımlama bilgilerini engelleyebilir ve site verileri** ayarlama (veya) etkin ve oluşturmak için bir özel durum **login.microsoftonline.com**ve hello Sihirbazı yeniden başlatmayı deneyin.
2. Merhaba, **özellikleri** sayfa:
    1. Girin **CopyPipeline** için **görev adı**. Merhaba görev adı, veri fabrikasında ardışık düzeni hello hello adıdır.
    2. Girin bir **açıklama** hello görevin (isteğe bağlı).
    3. İçin **görev tempoyla veya görev zamanlama**, hello tutmak **düzenli olarak zamanında** seçeneği. Bu görevi yalnızca bir kez yerine çalıştırmak sürekli bir zamanlamaya göre toorun istiyorsanız seçin **kez Şimdi Çalıştır**. Öğesini seçerseniz, **kez Şimdi Çalıştır** seçeneği, bir [tek seferlik ardışık düzen](data-factory-create-pipelines.md#onetime-pipeline) oluşturulur. 
    4. Hello ayarlarını koruyabilirsiniz **yinelenen desen**. Her gün çalışır hello arasında başlangıç ve bitiş, bu görev hello sonraki adımda belirtin.
    5. Değişiklik hello **başlangıç tarihi ve saati** çok**21/04/2017**. 
    6. Değişiklik hello **bitiş tarihi ve saati** çok**25/04/2017**. Merhaba takvimi aracılığıyla gözatma yerine tootype hello tarih isteyebilirsiniz.     
    8. **İleri**’ye tıklayın.
      ![Kopyalama aracı - Özellikler sayfası](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png) 
3. Merhaba üzerinde **kaynak veri deposu** sayfasında, **Azure Blob Storage** döşeme. Bu sayfa toospecify hello kaynak veri deposu hello kopyalama görevi için kullanın. Yeni bir veri deposu belirtmek için mevcut bir veri deposu bağlı hizmetini kullanabilirsiniz (veya) yeni bir veri deposu belirtebilirsiniz. var olan toouse bağlantılı hizmeti, seçtiğiniz **mevcut bağlı hizmetlerden** ve hello doğru bağlı hizmeti seçin. 
    ![Kopyalama aracı - kaynak veri deposu sayfası](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)
4. Merhaba üzerinde **hello Azure Blob Depolama hesabı belirtin** sayfa:
   1. İçin Hello otomatik olarak oluşturulan adı bırakın **bağlantı adı**. Merhaba bağlantı adı adıdır hello hello bağlantılı hizmet türü: Azure depolama. 
   2. **Hesap seçme yöntemi** için **Azure aboneliklerinden** seçeneğinin belirlendiğini onaylayın.
   3. Azure aboneliğinizi seçin ya da koruma **Tümünü Seç** için **Azure aboneliği**.   
   4. Seçin bir **Azure depolama hesabı** hello hesaplarına Azure depolama listesi hello seçili abonelikte kullanılabilir. Ayrıca tooenter depolama hesabı ayarlarını el ile seçerek seçebilirsiniz **el ile girmeniz** hello seçeneği **hesap seçme yöntemi**.
   5. **İleri**’ye tıklayın. 
      ![Kopyalama aracı - hello Azure Blob Depolama hesabı belirtin](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)
5. Üzerinde **Seç hello girdi dosyası veya klasörü** sayfa:
   1. Çift **adfblobcontainer**.
   2. Seçin **giriş**, tıklatıp **Seç**. Bu kılavuzda, hello giriş klasörü seçin. Merhaba emp.txt dosya hello klasöründe bunun yerine seçeneğini de. 
      ![Kopyalama aracı - hello girdi dosyası veya klasörü seçin](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)
6. Merhaba üzerinde **Seç hello girdi dosyası veya klasörü** sayfa:
    1. Bu hello onaylayın **dosya veya klasör** çok ayarlanır**adfblobconnector/giriş**. Merhaba dosyaları alt klasörlerde, örneğin, 04/2017/01, 04/2017/02 ve vb. adfblobconnector/giriş girin / {year} / {month} / {day} dosya veya klasör için. Merhaba metin kutusu dışında SEKME tuşuna bastığınızda (yyyy) yıl, ay (MM) ve gün (dd) için üç açılan listeleri tooselect biçimleri bakın. 
    2. Ayarlamayın **kopyalayın dosyayı yinelemeli olarak**. Bu seçenek toorecursively çapraz dosyaları toobe kopyalanan toohello hedefine klasörlerde seçin. 
    3. Değil hello **ikili kopyalama** seçeneği. Bu seçenek tooperform kaynak dosya toohello hedef ikili bir kopyasını seçin. Daha fazla seçenek hello sonraki sayfalarda görebilmeniz için bu kılavuzda seçmeyin. 
    4. Bu hello onaylayın **sıkıştırma türünü** çok ayarlanır**hiçbiri**. Kaynak dosyalar hello desteklenen biçimlerden birinde sıkıştırılmış bu seçenek için bir değer seçin. 
    5. **İleri**’ye tıklayın.
    ![Kopyalama aracı - hello girdi dosyası veya klasörü seçin](./media/data-factory-azure-blob-connector/chose-input-file-folder.png) 
7. Merhaba üzerinde **dosya biçimi ayarları** sayfasında, gördüğünüz hello sınırlayıcıları ve hello dosyası ayrıştırılırken hello Sihirbazı tarafından otomatik olarak algılanır hello şema. 
    1. Seçenekler aşağıdaki hello onaylayın: bir. Merhaba **dosya biçimi** çok ayarlanır**metin biçimi**. Tüm desteklenen hello biçimleri hello aşağı açılan listesinde görebilirsiniz. Örneğin: JSON, Avro, ORC, Parquet.
        b. Merhaba **sütun sınırlayıcı** çok ayarlanır`Comma (,)`. Gördüğünüz hello aşağı açılan listesinde Data Factory ile desteklenen diğer sütun sınırlayıcıları hello. Özel bir sınırlayıcı de belirtebilirsiniz.
        c. Merhaba **satır ayırıcı** çok ayarlanır`Carriage Return + Line feed (\r\n)`. Gördüğünüz hello aşağı açılan listesinde Data Factory ile desteklenen diğer satır sınırlayıcıları hello. Özel bir sınırlayıcı de belirtebilirsiniz.
        d. Merhaba **satır sayısı atla** çok ayarlanır**0**. Merhaba dosya hello üstünde atlandı birkaç satırları toobe istiyorsanız hello numarasını buraya girin.
        e.  Merhaba **ilk veri satırı sütun adları içeren** ayarlı değil. Merhaba ilk satırı sütun adları Hello kaynak dosyaları içeriyorsa, bu seçeneği belirleyin.
        f. Merhaba **boş sütun değeri null olarak davran** seçeneği ayarlanmış.
    2. Genişletme **Gelişmiş ayarları** toosee Gelişmiş seçeneği kullanılabilir.
    3. Merhaba sayfasının Hello altında hello bkz **Önizleme** hello emp.txt dosya verileri.
    4. Tıklatın **şema** hello kaynak dosyasında hello veri bakarak çıkarımı yapılan bu hello Kopyalama Sihirbazı hello alt toosee hello şema sekmesi.
    5. Tıklatın **sonraki** hello sınırlayıcıları gözden geçirin ve Önizleme veri sonra.
    ![Kopyalama aracı - dosya biçimi ayarları](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)  
8. Merhaba üzerinde **hedef veri deposu sayfası**seçin **Azure Blob Storage**, tıklatıp **sonraki**. Her iki hello kaynak ve hedef veri depolarına bu kılavuzda olarak hello Azure Blob Storage kullanıyor.    
    ![Kopyalama aracı - select hedef veri deposu](media/data-factory-azure-blob-connector/select-destination-data-store.png)
9. Üzerinde **hello Azure Blob Depolama hesabı belirtin** sayfa:
   1. Girin **AzureStorageLinkedService** hello için **bağlantı adı** alan.
   2. **Hesap seçme yöntemi** için **Azure aboneliklerinden** seçeneğinin belirlendiğini onaylayın.
   3. Azure **aboneliğinizi** seçin.  
   4. Azure depolama hesabınızı seçin. 
   5. **İleri**’ye tıklayın.     
10. Merhaba üzerinde **Seç hello çıktı dosya veya klasör** sayfa: 
    6. belirtin **klasör yolu** olarak **adfblobconnector/çıkış / {year} / {month} / {day}**. Girin **sekmesini**.
    7. Hello için **yıl**seçin **yyyy**.
    8. Hello için **ay**, çok ayarlandığından emin olun**MM**.
    9. Hello için **gün**, çok ayarlandığından emin olun**GG**.
    10. Bu hello onaylayın **sıkıştırma türünü** çok ayarlanır**hiçbiri**.
    11. Bu hello onaylayın **kopyalama davranışı** çok ayarlanır**dosyaları Birleştir**. Hello çıkış dosyası ile aynı adı zaten var. Merhaba, hello yeni içerik eklendi toohello hello sonunda dosya aynı olur.
    12. **İleri**’ye tıklayın.
    ![Kopyalama aracı - çıktı dosyası veya klasörü seçin](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)
11. Merhaba üzerinde **dosya biçimi ayarları** sayfasında hello ayarlarını gözden geçirin ve tıklayın **sonraki**. Burada ek seçenekler hello tooadd üstbilgi toohello çıktı dosyası biridir. Bu seçeneği belirlerseniz, bir başlık satırı hello kaynak hello şemadan hello sütunların adlarıyla eklenir. Merhaba varsayılan sütun adları hello kaynak hello şemasını görüntülerken yeniden adlandırabilirsiniz. Örneğin, hello ilk sütun tooFirst adı ve ikinci sütun tooLast adını değiştirebilirsiniz. Ardından, hello çıktı dosyası bu adları içeren bir başlık sütun adları olarak üretilir. 
    ![Kopyalama aracı - hedef için dosya biçimi ayarları](media/data-factory-azure-blob-connector/file-format-destination.png)
12. Merhaba üzerinde **performans ayarlarını** sayfasında, onaylayın **bulut birimleri** ve **paralel kopyaları** çok ayarlanır**otomatik**, İleri'yi tıklatın. Bu ayarlar hakkında daha fazla ayrıntı için bkz: [kopyalama etkinliği performans ve ayarlama Kılavuzu](data-factory-copy-activity-performance.md#parallel-copy).
    ![Kopyalama aracı - performans ayarları](media/data-factory-azure-blob-connector/copy-performance-settings.png) 
14. Merhaba üzerinde **Özet** sayfasında (görev özellikleri, kaynak ve hedef ayarları ve kopya ayarlarını) tüm ayarları gözden geçirin ve tıklayın **sonraki**.
    ![Kopyalama aracı - Özet sayfası](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)
15. Merhaba bilgileri gözden **Özet** sayfasında ve tıklayın **son**. Başlangıç Sihirbazı'nı (Başlangıç burada hello Kopyalama Sihirbazı'nı başlatılan) hello veri fabrikasında iki bağlı hizmet, iki veri kümesi (girdi ve çıktı) ve bir işlem hattı oluşturur.
    ![Kopyalama aracı - dağıtım sayfası](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)

### <a name="monitor-hello-pipeline-copy-task"></a>İzleyici hello ardışık düzen (kopyalama görevi)

1. Merhaba bağlantısına tıklayın `Click here toomonitor copy pipeline` hello üzerinde **dağıtım** sayfası. 
2. Merhaba görmelisiniz **izleme ve yönetme uygulaması** ayrı bir sekmede.  ![İzleme ve uygulama yönetme](media/data-factory-azure-blob-connector/monitor-manage-app.png)
3. Değişiklik hello **Başlat** hello üstünde çok zaman`04/19/2017` ve **son** çok zaman`04/27/2017`ve ardından **Uygula**. 
4. Beş etkinlik windows hello görmelisiniz **etkinlik WINDOWS** listesi. Merhaba **WindowStart** kez ardışık düzen başlangıç toopipeline bitiş zamanları tüm gün kapak. 
5. Tıklatın **yenileme** hello düğmesi **etkinlik WINDOWS** birkaç kez tüm hello etkinlik windows hello durumunu görene kadar listesini tooReady ayarlayın. 
6. Şimdi, adfblobconnector kapsayıcısının çıkış klasörüne hello oluşturulan hello çıktı dosyaları doğrulayın. Klasör yapısı hello çıkış klasöründe aşağıdaki hello görmeniz gerekir: 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
İzleme ve veri fabrikaları yönetme hakkında ayrıntılı bilgi için bkz: [İzleyici ve Data Factory işlem hattı yönetmek](data-factory-monitor-manage-app.md) makalesi. 
 
### <a name="data-factory-entities"></a>Data Factory varlıklarını
Şimdi, hello Data Factory giriş sayfasına geri toohello sekmesiyle geçin. İki bağlı hizmet, iki veri kümesi ve bir ardışık düzeni, veri fabrikası'nda artık dikkat edin. 

![Varlıklarla Data Factory giriş sayfası](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

Tıklatın **yazar ve dağıtma** toolaunch Data Factory Düzenleyici. 

![Data Factory Düzenleyicisi](media/data-factory-azure-blob-connector/data-factory-editor.png)

Data Factory varlıklarını, veri fabrikası'nda aşağıdaki hello görmeniz gerekir: 

 - İki bağlı hizmet. Biri hello kaynak ve hello diğeri hello hedef için. İki bağlı hello hizmet toohello başvurmak bu kılavuzda aynı Azure depolama hesabı. 
 - İki veri kümesi. Bir giriş veri kümesi ve bir çıkış veri kümesi. Bu kılavuzda, her ikisini de hello kullanmanız aynı blob kapsayıcısı ancak toodifferent klasörleri (girdi ve çıktı) ifade eder.
 - Ardışık Düzen. Merhaba ardışık düzen blob kaynağı ve Azure blob konumu tooanother Azure blob konumu blob havuz toocopy verilerden kullanan kopyalama etkinliği içerir. 

Merhaba aşağıdaki bölümler bu varlıkları hakkında daha fazla bilgi sağlar. 

#### <a name="linked-services"></a>Bağlı hizmetler
İki bağlı hizmet görmeniz gerekir. Biri hello kaynak ve hello diğeri hello hedef için. Bu kılavuzda, her iki tanımları görünüm hello aynı dışında hello adları. Merhaba **türü** Merhaba bağlantılı hizmet olarak ayarlanmış çok**AzureStorage**. En önemli hello bağlantılı hizmet tanımı özelliğidir hello **connectionString**, veri fabrikası tooconnect tooyour çalışma zamanında Azure depolama hesabı tarafından kullanılıyor. Merhaba hubName özelliği hello tanımında yoksay. 

##### <a name="source-blob-storage-linked-service"></a>Kaynak blob storage bağlı hizmeti
```json
{
    "name": "Source-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

##### <a name="destination-blob-storage-linked-service"></a>Hedef blob depolama bağlı hizmeti

```json
{
    "name": "Destination-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

Azure Storage bağlı hizmeti hakkında daha fazla bilgi için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü. 

#### <a name="datasets"></a>Veri kümeleri
İki veri kümesi vardır: bir giriş veri kümesi ve bir çıkış veri kümesi. Merhaba dataset Hello türü çok ayarlamak**AzureBlob** her ikisi için de. 

Merhaba girdi veri kümesi işaret toohello **giriş** hello klasörünü **adfblobconnector** blob kapsayıcısı. Merhaba **dış** özelliği çok ayarlanmış**true** hello olarak bu veri kümesi için veri hello ardışık düzen tarafından bu veri kümesine bir girdi olarak alır hello kopyalama etkinliği ile oluşturulmuyor. 

Çıktı veri kümesi noktaları toohello hello **çıkış** hello klasörü aynı blob kapsayıcısı. Merhaba çıktı veri kümesi de hello yıl, ay ve gün Merhaba, kullanır **SliceStart** sistem değişken toodynamically hello çıktı dosyası için hello yol değerlendirin. İşlevler ve Data Factory ile desteklenen sistem değişkenleri listesi için bkz: [Data Factory işlevler ve sistem değişkenleri](data-factory-functions-variables.md). Merhaba **dış** özelliği çok ayarlanmış**false** (varsayılan değer) bu veri kümesi hello ardışık düzen tarafından üretilen olduğundan. 

Azure Blob veri kümesi tarafından desteklenen özellikler hakkında daha fazla bilgi için bkz: [veri kümesi özellikleri](#dataset-properties) bölümü.

##### <a name="input-dataset"></a>Girdi veri kümesi

```json
{
    "name": "InputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Source-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/input/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

##### <a name="output-dataset"></a>Çıktı veri kümesi

```json
{
    "name": "OutputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Destination-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/output/{year}/{month}/{day}",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
            "partitionedBy": [
                { "name": "year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } }
            ]
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

#### <a name="pipeline"></a>İşlem hattı
Merhaba ardışık yalnızca bir etkinlik vardır. Merhaba **türü** Merhaba, etkinlik çok ayarlanır**kopya**.  Merhaba etkinliğinin Hello tür özellikleri kaynak ve hello başka bir havuz için iki bölümü vardır. Merhaba kaynak türü çok ayarlamak**BlobSource** hello etkinliği bir blob depolama alanından veri kopyalama gibi. Merhaba Havuz türü çok ayarlanmış**BlobSink** veri tooa blob depolama kopyalama hello etkinlik olarak. Merhaba kopyalama etkinliği InputDataset z4y hello giriş ve OutputDataset z4y hello çıktı olarak alır. 

BlobSource ve BlobSink tarafından desteklenen özellikler hakkında daha fazla bilgi için bkz: [kopyalama etkinliği özellikleri](#copy-activity-properties) bölümü. 

```json
{
    "name": "CopyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "MergeFiles",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-z4y"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-z4y"
                    }
                ],
                "policy": {
                    "timeout": "1.00:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "style": "StartOfInterval",
                    "retry": 3,
                    "longRetry": 0,
                    "longRetryInterval": "00:00:00"
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "Activity-0-Blob path_ adfblobconnector_input_->OutputDataset-z4y"
            }
        ],
        "start": "2017-04-21T22:34:00Z",
        "end": "2017-04-25T05:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-blob-storage"></a>Blob depolama alanından veri tooand kopyalama için JSON örnekleri  
Merhaba aşağıdaki örneklerde sağlayan örnek JSON tanımları toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Bunlar Göster nasıl toocopy veri tooand Azure Blob Storage ve Azure SQL veritabanı. Ancak, veriler kopyalanabilir **doğrudan** herhangi birinden belirtildiği hello havuzlarını, kaynakları tooany [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.

### <a name="json-example-copy-data-from-blob-storage-toosql-database"></a>JSON örnek: Verilerini Blob Storage tooSQL veritabanı
Merhaba, aşağıdaki örnek gösterilmektedir:

1. Bağlı hizmet türü [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).
2. Bağlı hizmet türü [AzureStorage](#linked-service-properties).
3. Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureBlob](#dataset-properties).
4. Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).
5. A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [BlobSource](#copy-activity-properties) ve [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).

Merhaba örnek time series verilerini saatlik bir Azure blob tooan Azure SQL tablosundan kopyalar. Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.

**Azure SQL bağlı hizmeti:**

```json
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
**Azure Storage bağlı hizmeti:**

```json
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

Veri toplanma yeni blob üzerinden saatte (sıklığı: saat, aralığı: 1). Merhaba klasör yolu ve dosya adını hello blob dinamik olarak değerlendirilir işleniyor hello dilimin hello başlangıç zamanı temel alınarak. Merhaba klasör yolu yıl, ay ve gün kısmını hello başlangıç saati ve dosya adı hello başlangıç saati hello saat bölümünü kullanır. "dış": "true" ayarı bu hello tablosu dış toohello veri fabrikası ve hello veri fabrikasında bir etkinlik tarafından üretilen değil veri fabrikası sizi bilgilendirir.

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
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
**Azure SQL çıktı veri kümesi:**

Merhaba örnek bir Azure SQL veritabanında "MyTable" adlı veri tooa tablosuna kopyalar. Azure SQL veritabanınızda Hello tablo oluşturma hello Blob CSV dosyası toocontain beklediğiniz gibi hello aynı sayıda sütun. Yeni satırlar toohello tablo saatte eklenir.

```json
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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
**Blob kaynağı ve SQL havuz sahip işlem hattı kopyalama etkinliğinde:**

Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**BlobSource** ve **havuz** türü olarak ayarlanmış çok**SqlSink**.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink"
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
### <a name="json-example-copy-data-from-azure-sql-tooazure-blob"></a>JSON örnek: Verilerini Azure SQL tooAzure Blob
Merhaba, aşağıdaki örnek gösterilmektedir:

1. Bağlı hizmet türü [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).
2. Bağlı hizmet türü [AzureStorage](#linked-service-properties).
3. Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).
4. Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](#dataset-properties).
5. A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) ve [BlobSink](#copy-activity-properties).

Merhaba örnek time series verilerini saatlik bir Azure SQL tablosu tooan Azure blob kopyalar. Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.

**Azure SQL bağlı hizmeti:**

```json
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
**Azure Storage bağlı hizmeti:**

```json
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

**Azure SQL girdi veri kümesi:**

Merhaba örnek "MyTable" Azure SQL tablosu oluşturdunuz ve zaman serisi veri için "timestampcolumn" adlı bir sütun içerdiği varsayar.

"Dış" ayarı: "true" bildirir Data Factory hizmetinin bu hello tablosu dış toohello veri fabrikası ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.

```json
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
      "partitionedBy": [
        {
          "name": "Year",
          "value": { "type": "DateTime",  "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
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

**SQL kaynak ve Blob havuz sahip işlem hattı kopyalama etkinliğinde:**

Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**SqlSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**. Merhaba belirtilen hello SQL sorgusu **SqlReaderQuery** özelliği saat toocopy geçmiş hello hello veri seçer.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureSQLInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
