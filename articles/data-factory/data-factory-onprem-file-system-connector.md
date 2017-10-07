---
title: Azure Data Factory kullanarak bir dosya sistemi/aaaCopy verileri | Microsoft Docs
description: "Bilgi nasıl toocopy veri tooand Azure Data Factory kullanarak bir şirket içi dosya sisteminden."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ce19f1ae-358e-4ffc-8a80-d802505c9c84
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 201b8bc3ffa639df781443aa0c3f95c975d280be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-an-on-premises-file-system-by-using-azure-data-factory"></a>Azure Data Factory kullanarak veri tooand bir şirket içi dosya sisteminden kopyalama
Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toocopy veri grafikten bir şirket içi dosya sistemi açıklanmaktadır. Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.

## <a name="supported-scenarios"></a>Desteklenen senaryolar
Veri kopyalama **bir şirket içi dosya sisteminden** veri depolarına aşağıdaki toohello:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Veri depoları aşağıdaki hello verileri kopyalayabilirsiniz **tooan şirket içi dosya sistemi**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> Başarıyla kopyalanan toohello hedef tamamlandıktan sonra kopyalama etkinliği hello kaynak dosyayı silmez. Sonra başarılı bir kopyasını toodelete hello kaynak dosyası gerekiyorsa, bir özel etkinlik toodelete hello dosyası oluşturun ve hello ardışık düzeninde hello etkinliği kullanın. 

## <a name="enabling-connectivity"></a>Bağlantıyı etkinleştirme
Veri Fabrikası destekleyen bir şirket içi dosya sisteminden bağlanan tooand **veri yönetimi ağ geçidi**. Dosya sistemi dahil olmak üzere hello Data Factory hizmeti tooconnect tooany desteklenen şirket içi veri depolama için şirket içi ortamınızda hello veri yönetimi ağ geçidi yüklemeniz gerekir. toolearn veri yönetimi ağ geçidi hakkında ve hello ağ geçidi, ayarlama hakkında adım adım yönergeler için bkz: [şirket içi kaynakları ve veri yönetimi ağ geçidi ile Merhaba bulut arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md). Veri Yönetimi ağ geçidi dışında herhangi bir ikili dosyaları yüklü toobe toocommunicate tooand bir şirket içi dosya sisteminden gerekir. Yüklemeniz ve Azure Iaas sanal hello dosya sistemi olsa bile, hello veri yönetimi ağ geçidi kullanmanız gerekir. Merhaba ağ geçidi hakkında ayrıntılı bilgi için bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md).

toouse Linux dosya paylaşımı yükleme [Samba](https://www.samba.org/) Linux sunucusu ve Windows Server yükleme veri yönetimi ağ geçidi. Veri Yönetimi ağ geçidi Linux sunucusu üzerinde yüklenmesi desteklenmez.

## <a name="getting-started"></a>Başlarken
Farklı araçlar/API'lerini kullanarak verileri öğesine/öğesinden bir dosya sistemi taşır kopyalama etkinliği ile işlem hattı oluşturun.

Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**. Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.

Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**. Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.

Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:

1. Oluşturma bir **veri fabrikası**. Veri Fabrikası bir veya daha fazla ardışık düzen içerebilir. 
2. Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası. Bir Azure blob depolama tooan şirket içi dosya sisteminden veri kopyalama, örneğin, iki bağlı hizmet toolink şirket içi dosya sistemi ve Azure depolama hesabı tooyour veri fabrikası oluşturun. Belirli tooan şirket içi dosya sistemi bağlantılı hizmet özellikler için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü.
3. Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi. Merhaba son adımda bahsedilen hello örnekte, bir veri kümesi toospecify hello blob kapsayıcısı ve hello giriş verisi içeren klasörü oluşturun. Ve başka bir veri kümesi toospecify hello klasör ve dosya adı (isteğe bağlı) dosya sisteminizi oluşturun. Belirli tooon içi veri kümesi özellikleri dosya sistemi için bkz: [veri kümesi özellikleri](#dataset-properties) bölümü.
4. Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile. Daha önce bahsedilen hello örnekte BlobSource bir kaynak ve FileSystemSink havuzu olarak hello kopya etkinliği için kullanırsınız. Şirket içi dosya sistemi tooAzure Blob Depolama kopyalıyorsanız benzer şekilde, FileSystemSource ve BlobSink hello kopyalama etkinliği kullanırsınız. Belirli tooon içi kopyalama etkinliği özellikleri dosya sistemi için bkz: [kopyalama etkinliği özellikleri](#copy-activity-properties) bölümü. Nasıl toouse bir veri deposu bir kaynak veya bir havuz olarak hakkında daha fazla bilgi için veri deposu hello önceki bölümdeki hello bağlantısına tıklayın.

Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur. Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.  Bir dosya sistemi/kullanılan toocopy verileri olan Data Factory varlıkları için JSON tanımlarıyla örnekleri için bkz: [JSON örnekler](#json-examples-for-copying-data-to-and-from-file-system) bu makalenin.

Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli toofile sistem JSON özellikleri hakkında ayrıntılı bilgi sağlar:

## <a name="linked-service-properties"></a>Bağlantılı hizmet özellikleri
Bir şirket içi dosya sistemi tooan Azure data factory hello ile bağlayabilirsiniz **şirket içi dosya sunucusu** bağlı hizmeti. Aşağıdaki tablonun hello belirli toohello şirket içi dosya sunucusuna bağlı hizmeti olan JSON öğeleri için açıklamalar sağlanır.

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| type |Merhaba type özelliği çok ayarlandığından emin olun**OnPremisesFileServer**. |Evet |
| ana bilgisayar |Toocopy istediğiniz hello klasörü Hello kök yolunu belirtir. Merhaba kaçış karakteri kullanmak ' \ ' hello dize özel karakter. Bkz: [örnek bağlantılı hizmeti ve veri kümesi tanımları](#sample-linked-service-and-dataset-definitions) örnekleri için. |Evet |
| Kullanıcı Kimliği |Merhaba erişim toohello sunucusuna sahip hello kullanıcı Kimliğini belirtin. |Hayır (encryptedCredential seçerseniz) |
| password |Merhaba kullanıcı (UserID) Hello parolasını belirtin. |Hayır (encryptedCredential seçerseniz |
| encryptedCredential |Merhaba yeni AzureRmDataFactoryEncryptValue cmdlet'ini çalıştırarak alabilirsiniz hello şifreli kimlik bilgilerini belirtin. |Hayır (toospecify kullanıcı kimliği ve parola düz metin olarak seçerseniz) |
| gatewayName |Veri Fabrikası tooconnect toohello şirket içi dosya sunucusu kullanmalısınız hello ağ geçidi Hello adını belirtir. |Evet |


### <a name="sample-linked-service-and-dataset-definitions"></a>Örnek bağlantılı hizmet ve veri kümesi tanımları
| Senaryo | Bağlantılı hizmet tanımında ana bilgisayar | veri kümesi tanımında folderPath |
| --- | --- | --- |
| Veri Yönetimi ağ geçidi makine üzerinde yerel klasör: <br/><br/>Örnekler: D:\\ \* veya D:\folder\subfolder\\* |D:\\ \\ (için veri yönetimi ağ geçidi 2.0 ve sonraki sürümler) <br/><br/> localhost (daha önceki sürümler için veri yönetimi ağ geçidi 2. 0) |. \\ \\ veya klasör\\\\alt klasör (için veri yönetimi ağ geçidi 2.0 ve sonraki sürümler) <br/><br/>D:\\ \\ veya D:\\\\klasörü\\\\alt klasör (için ağ geçidi sürüm 2.0 altında) |
| Uzak paylaşılan klasör: <br/><br/>Örnekler: \\ \\myserver\\paylaşmak\\ \* veya \\ \\myserver\\paylaşmak\\klasörü\\alt klasör\\* |\\\\\\\\myserver\\\\paylaşma |. \\ \\ veya klasör\\\\alt klasör |


### <a name="example-using-username-and-password-in-plain-text"></a>Örnek: kullanıcı adı ve parola düz metin olarak kullanma

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

### <a name="example-using-encryptedcredential"></a>Örnek: encryptedcredential kullanma

```JSON
{
  "Name": " OnPremisesFileServerLinkedService ",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "D:\\",
      "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
      "gatewayName": "mygateway"
    }
  }
}
```

## <a name="dataset-properties"></a>Veri kümesi özellikleri
Bölümleri ve veri kümelerini tanımlamak için kullanılabilir olan özellikleri tam listesi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md). Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri kümesi türleri için benzerdir.

Merhaba typeProperties bölüm veri kümesi her tür için farklıdır. Başlangıç konumu ve hello veri deposundaki hello veri biçimi gibi bilgiler sağlar. Merhaba typeProperties bölüm türü hello veri kümesi için **FileShare** hello aşağıdaki özelliklere sahiptir:

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| folderPath |Merhaba alt toohello klasörü belirtir. Merhaba kaçış karakteri kullanmak ' \' hello dize özel karakter. Bkz: [örnek bağlantılı hizmeti ve veri kümesi tanımları](#sample-linked-service-and-dataset-definitions) örnekleri için.<br/><br/>Bu özellik ile birleştirebilirsiniz **partitionBy** toohave klasör yolları dilimine göre başlangıç/bitiş tarih saatleri. |Evet |
| fileName |Hello Hello hello dosyasının adını belirtin **folderPath** hello tablo toorefer tooa belirli dosya hello klasöründeki istiyorsanız. Bu özellik için herhangi bir değer belirtmezseniz, hello tablo hello klasöründeki tooall dosyaları işaret eder.<br/><br/>Zaman **fileName** bir çıkış veri kümesi için belirtilmemiş ve **preserveHierarchy** belirtilmedi etkinlik havuzunda hello oluşturulan hello dosyasının adıdır biçimini izleyen hello: <br/><br/>`Data.<Guid>.txt`(Örnek: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |Hayır |
| fileFilter |Tüm dosyalar yerine hello folderPath dosyaları kümesini filtre toobe tooselect kullanılan belirtin. <br/><br/>İzin verilen değerler: `*` (birden çok karakter) ve `?` (tek bir karakter).<br/><br/>Örnek 1: "fileFilter": "* .log"<br/>Örnek 2: "fileFilter": 2014 - 1-? txt"<br/><br/>Bu fileFilter bir giriş FileShare veri kümesi için geçerli olduğunu unutmayın. |Hayır |
| partitionedBy |Zaman serisi veri partitionedBy toospecify dinamik folderPath/fileName kullanabilirsiniz. İçin verileri saatte parametreli folderPath örneğidir. |Hayır |
| Biçimi | şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set hello **türü** biçimi tooone şu değerlerden biri altında özellik. Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler. <br><br> Çok istiyorsanız**olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında hello Biçim bölümü atlayın. |Hayır |
| Sıkıştırma | Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin. Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**. Desteklenen düzeyler: **Optimal** ve **en hızlı**. bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support). |Hayır |

> [!NOTE]
> Dosya adı ve fileFilter aynı anda kullanamazsınız.

### <a name="using-partitionedby-property"></a>PartitionedBy özelliğini kullanma
Merhaba önceki bölümünde belirtildiği gibi bir dinamik folderPath ve zaman serisi verileri için dosya adı ile Merhaba belirtebilirsiniz **partitionedBy** özelliği, [Data Factory işlevler ve hello sistem değişkenleri](data-factory-functions-variables.md).

toounderstand zaman serisi veri kümeleri, zamanlama ve dilimleri hakkında daha fazla ayrıntı görmek [veri kümeleri oluşturma](data-factory-create-datasets.md), [zamanlama ve yürütme](data-factory-scheduling-and-execution.md), ve [ardışık düzen oluşturma](data-factory-create-pipelines.md).

#### <a name="sample-1"></a>Örnek 1:

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

Bu örnekte, {dilim} hello değişkeninin değeri hello Data Factory sistem SliceStart hello biçiminde (YYYYMMDDHH) ile değiştirilir. SliceStart toostart süresi hello dilimin başvurur. Merhaba folderPath her dilim için farklıdır. Örneğin: wikidatagateway/wikisampledataout/2014100103 veya wikidatagateway/wikisampledataout/2014100104.

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

Bu örnekte, yıl, ay, gün ve saat SliceStart hello folderPath ve dosya adı özellikleri kullanan ayrı değişkenlere ayıklanır.

## <a name="copy-activity-properties"></a>Etkinlik özellikleri Kopyala
Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi. Ad, açıklama, giriş ve çıkış veri kümeleri ve ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir. Oysa hello kullanılabilen özellikleri **typeProperties** hello etkinlik bölümünü her etkinlik türü ile değişir.

Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir. Bir şirket içi dosya sisteminden veri taşıyorsanız, hello kaynak türü hello kopyalama etkinliği çok ayarladığınız**FileSystemSource**. Benzer şekilde, veri tooan taşıyorsanız, şirket içi dosya sistemi, hello Havuz türü hello kopyalama etkinliği çok ayarladığınız**FileSystemSink**. Bu bölümde FileSystemSource ve FileSystemSink tarafından desteklenen özellikler listesini sağlar.

**FileSystemSource** aşağıdaki özelliklere hello destekler:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| Özyinelemeli |Merhaba klasörlerdeki veya yalnızca klasörden hello belirtilen Hello veri yinelemeli olarak okunur olup olmadığını gösterir. |TRUE, False (varsayılan) |Hayır |

**FileSystemSink** aşağıdaki özelliklere hello destekler:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| copyBehavior |Merhaba kaynağı BlobSource veya dosya sistemi olduğunda hello kopyalama davranışını tanımlar. |**PreserveHierarchy:** hello dosya hiyerarşisi hello hedef klasörde korur. Diğer bir deyişle, hello kaynak dosya toohello kaynak klasörün hello göreli yol olduğundan hello hello hedef dosya toohello hedef klasörü hello göreli yolu ile aynı.<br/><br/>**FlattenHierarchy:** hello kaynak klasördeki tüm dosyaları hedef klasörün hello ilk düzeyi oluşturulur. Merhaba hedef dosyaları otomatik olarak oluşturulur adıyla oluşturulur.<br/><br/>**MergeFiles:** hello kaynak klasör tooone dosyasından tüm dosyaları birleştirir. Merhaba dosya adı/blob adı belirtilirse, hello belirtilen ad hello birleştirilmiş dosya adı değil. Aksi halde, bir otomatik olarak oluşturulan dosya adı değil. |Hayır |

### <a name="recursive-and-copybehavior-examples"></a>özyinelemeli ve copyBehavior örnekleri
Bu bölümde hello kopyalama işlemi farklı birleşimlerini hello özyinelemeli ve copyBehavior özelliklerine ilişkin değerleri için sonuçta elde edilen davranışını hello açıklanmaktadır.

| özyinelemeli değeri | copyBehavior değeri | Bunun sonucunda oluşan davranışı |
| --- | --- | --- |
| TRUE |preserveHierarchy |Kaynak klasör Klasör1 yapı izlenerek hello ile<br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Merhaba hedef klasör Klasör1 aynı hello kaynağı olarak yapısı hello oluşturulur:<br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5 |
| TRUE |flattenHierarchy |Kaynak klasör Klasör1 yapı izlenerek hello ile<br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Merhaba hedef Klasör1 yapı izlenerek hello ile oluşturulur: <br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;dosya1 için otomatik olarak oluşturulan adı<br/>&nbsp;&nbsp;&nbsp;&nbsp;dosya2 için otomatik olarak oluşturulan adı<br/>&nbsp;&nbsp;&nbsp;&nbsp;dosya3 için otomatik olarak oluşturulan adı<br/>&nbsp;&nbsp;&nbsp;&nbsp;File4 için otomatik olarak oluşturulan adı<br/>&nbsp;&nbsp;&nbsp;&nbsp;File5 için otomatik olarak oluşturulan adı |
| TRUE |mergeFiles |Kaynak klasör Klasör1 yapı izlenerek hello ile<br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Merhaba hedef Klasör1 yapı izlenerek hello ile oluşturulur: <br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya1 + dosya2 + dosya3 + File4 + 5 dosyası içeriği otomatik olarak oluşturulan dosya adına sahip bir dosya halinde birleştirilir. |
| False |preserveHierarchy |Kaynak klasör Klasör1 yapı izlenerek hello ile<br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Merhaba hedef klasör Klasör1 yapı izlenerek hello ile oluşturulur:<br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya2<br/><br/>Dosya3, File4 ve File5 Subfolder1 toplanma değil. |
| False |flattenHierarchy |Kaynak klasör Klasör1 yapı izlenerek hello ile<br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Merhaba hedef klasör Klasör1 yapı izlenerek hello ile oluşturulur:<br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;dosya1 için otomatik olarak oluşturulan adı<br/>&nbsp;&nbsp;&nbsp;&nbsp;dosya2 için otomatik olarak oluşturulan adı<br/><br/>Dosya3, File4 ve File5 Subfolder1 toplanma değil. |
| False |mergeFiles |Kaynak klasör Klasör1 yapı izlenerek hello ile<br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Merhaba hedef klasör Klasör1 yapı izlenerek hello ile oluşturulur:<br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya1 + dosya2 içeriği otomatik olarak oluşturulan dosya adına sahip bir dosya halinde birleştirilir.<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya1 için otomatik olarak oluşturulan adı<br/><br/>Dosya3, File4 ve File5 Subfolder1 toplanma değil. |

## <a name="supported-file-and-compression-formats"></a>Desteklenen dosya ve sıkıştırma biçimleri
Bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md) makale ayrıntıları.

## <a name="json-examples-for-copying-data-tooand-from-file-system"></a>Veri tooand dosya sisteminden kopyalama için JSON örnekleri
Merhaba aşağıdaki örneklerde sağlayan örnek JSON tanımları toocreate bir ardışık düzen hello kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Bunlar Göster nasıl toocopy veri tooand bir şirket içi dosya sistemi ve Azure Blob Depolama. Ancak, veri kopyalayabilirsiniz *doğrudan* herhangi birinden hello kaynakları tooany listelenen hello havuzlarını, [desteklenen kaynakları ve havuzlarını](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kopya etkinliği Azure Data Factory kullanarak.

### <a name="example-copy-data-from-an-on-premises-file-system-tooazure-blob-storage"></a>Örnek: bir şirket içi dosya sistemi tooAzure Blob depolama alanına veri kopyalama
Bu örnek göstermektedir nasıl bir şirket içi dosya sistemi tooAzure Blob Depolama toocopy verileri. Merhaba örnek Data Factory varlıklarını aşağıdaki hello sahiptir:

* Bağlı hizmet türü [OnPremisesFileServer](#linked-service-properties).
* Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Bir giriş [dataset](data-factory-create-datasets.md) türü [FileShare](#dataset-properties).
* Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [FileSystemSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Aşağıdaki örnek hello time series verilerini her saat bir şirket içi dosya sistemi tooAzure Blob Depolama kopyalar. Bu örnekler kullanılan JSON özellikleri hello hello örnekleri sonra hello bölümlerde açıklanmıştır.

İlk adım olarak, veri yönetimi ağ geçidi kurun hello yönergelerini uygun şekilde ayarlayın. [şirket içi kaynakları ve veri yönetimi ağ geçidi ile Merhaba bulut arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md).

**Şirket içi dosya sunucusu hizmeti bağlı:**

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

Merhaba kullanmanızı öneririz **encryptedCredential** özelliği yerine hello **UserID** ve **parola** özellikleri. Bkz: [dosya sunucusuna bağlı hizmetinin](#linked-service-properties) bu hakkındaki ayrıntılar için bağlantılı hizmeti.

**Azure Storage bağlı hizmeti:**

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

**Şirket içi sistem girdi veri kümesi dosya:**

Verileri yeni bir dosyadan saatte kayıt. folderPath hello ve fileName özellikleri hello dilimin hello başlangıç zamanı temel alınarak belirlenir.  

Ayar `"external": "true"` bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil veri fabrikası bildirir.

```JSON
{
  "name": "OnpremisesFileSystemInput",
  "properties": {
    "type": " FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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

**Azure Blob Depolama çıktı veri kümesi:**

Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1). hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir. Merhaba klasör yolu hello yıl, ay, gün ve saat bölümlerini hello başlangıç saatini kullanır.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Dosya sistemi kaynak ve Blob havuz sahip işlem hattı kopyalama etkinliğinde:**

Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**FileSystemSource**, ve **havuz** türü olarak ayarlanmış çok**BlobSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T19:00:00",
    "description":"Pipeline for copy activity",
    "activities":[  
      {
        "name": "OnpremisesFileSystemtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "OnpremisesFileSystemInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
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
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```

### <a name="example-copy-data-from-azure-sql-database-tooan-on-premises-file-system"></a>Örnek: verileri Azure SQL veritabanı tooan şirket içi dosya sisteminden kopyalama
Merhaba, aşağıdaki örnek gösterilmektedir:

* Bağlı hizmet türü [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)
* Bağlı hizmet türü [OnPremisesFileServer](#linked-service-properties).
* Bir giriş veri kümesi türü [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).
* Bir çıkış veri kümesi türü [FileShare](#dataset-properties).
* Kullanan kopyalama etkinliği ile işlem hattı [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) ve [FileSystemSink](#copy-activity-properties).

Merhaba örnek time series verilerini her saat bir Azure SQL tablosu tooan şirket içi dosya sisteminden kopyalar. Bu örnekler kullanılan JSON özellikleri hello hello örnekleri sonra bölümlerde açıklanmıştır.

**Azure SQL Database hizmeti bağlı:**

```JSON
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

**Şirket içi dosya sunucusu hizmeti bağlı:**

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

Merhaba kullanmanızı öneririz **encryptedCredential** hello yerine özelliği **UserID** ve **parola** özellikleri. Bkz: [dosya sistemi bağlantılı hizmet](#linked-service-properties) bu hakkındaki ayrıntılar için bağlı hizmeti.

**Azure SQL girdi veri kümesi:**

Merhaba örnek bir tablo "MyTable" Azure SQL oluşturduğunuz ve için zaman serisi veri "timestampcolumn" adlı bir sütun içerdiği varsayar.

Ayar ``“external”: ”true”`` bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil veri fabrikası bildirir.

```JSON
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

**Şirket içi sistem çıktı veri kümesi dosya:**

Veri kopyalanan tooa yeni saatte dosyasıdır. Merhaba folderPath ve hello blob fileName hello dilimin hello başlangıç zamanı temel alınarak belirlenir.

```JSON
{
  "name": "OnpremisesFileSystemOutput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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

**SQL kaynak ve dosya sistemi havuz sahip işlem hattı kopyalama etkinliğinde:**

Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**SqlSource**ve hello **havuz** türü olarak ayarlanmış çok**FileSystemSink**. Merhaba belirtilen hello SQL sorgusu **SqlReaderQuery** özelliği saat toocopy geçmiş hello hello veri seçer.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T20:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoOnPremisesFile",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "OnpremisesFileSystemOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "FileSystemSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 3,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```


Ayrıca, kaynak veri kümesi toocolumns hello kopyalama etkinliği tanımında havuz kümesinden sütunlarından eşleyebilirsiniz. Ayrıntılar için bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Performans ve ayar
 anahtarı hakkında toolearn Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi hello performansını, hello bkz [kopyalama etkinliği performans ve ayarlama Kılavuzu](data-factory-copy-activity-performance.md).
