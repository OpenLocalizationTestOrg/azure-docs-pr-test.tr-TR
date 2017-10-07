---
title: Azure Data Lake Store gelen aaaCopy veri tooand | Microsoft Docs
description: "Bilgi nasıl Azure Data Factory kullanarak Data Lake Store gelen toocopy veri tooand"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 25b1ff3c-b2fd-48e5-b759-bb2112122e30
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 2e78f75f3821738332dacf70f6bf2c16f0136408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-data-lake-store-by-using-data-factory"></a>Veri Fabrikası kullanarak veri tooand Data Lake Deposu'ndan veri kopyalama
Bu makalede açıklanır nasıl toouse kopya etkinliği Azure Data Factory toomove veri tooand Azure Data Lake Store gelen içinde. Merhaba üzerinde derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalesi, veri taşıma kopyalama etkinliği ile bir genel bakış.

## <a name="supported-scenarios"></a>Desteklenen senaryolar
Veri kopyalama **Azure Data Lake Store gelen** veri depolarına aşağıdaki toohello:

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

Veri depoları aşağıdaki hello verileri kopyalayabilirsiniz **tooAzure Data Lake Store**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> Kopyalama etkinliği ile işlem hattı oluşturmadan önce bir Data Lake Store hesabı oluşturun. Daha fazla bilgi için bkz: [Azure Data Lake Store ile çalışmaya başlama](../data-lake-store/data-lake-store-get-started-portal.md).

## <a name="supported-authentication-types"></a>Desteklenen kimlik doğrulama türleri
Merhaba Data Lake Store bağlayıcı, bu kimlik doğrulama türlerini destekler:
* Hizmet sorumlusu kimlik doğrulaması
* Kullanıcı kimlik bilgisi (OAuth) kimlik doğrulaması 

Hizmet asıl kimlik doğrulaması, özellikle bir zamanlanmış veri kopyalama için kullanmanızı öneririz. Belirteç süre sonu davranış kullanıcı kimlik bilgilerinin ile ortaya çıkabilir. Merhaba yapılandırma ayrıntıları için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü.

## <a name="get-started"></a>başlarken
Verileri farklı araçlar/API'lerini kullanarak Azure Data Lake Store denetleyicisinden taşır kopyalama etkinliği ile işlem hattı oluşturun.

Merhaba en kolay yolu toocreate bir ardışık düzen toocopy veri olduğu toouse hello **Kopyalama Sihirbazı'nı**. Merhaba Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma, Öğretici için bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md).

Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**. Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.

Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:

1. Oluşturma bir **veri fabrikası**. Veri Fabrikası bir veya daha fazla ardışık düzen içerebilir. 
2. Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası. Bir Azure blob depolama tooan Azure Data Lake Store veri kopyalama, örneğin, iki bağlı hizmet toolink Azure depolama hesabınız ve Azure Data Lake deposu tooyour veri fabrikası oluşturun. Belirli tooAzure Data Lake Store bağlantılı hizmet özellikler için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü. 
2. Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi. Merhaba son adımda bahsedilen hello örnekte, bir veri kümesi toospecify hello blob kapsayıcısı ve hello giriş verisi içeren klasörü oluşturun. Ve hello blob depolama biriminden kopyalanan hello verilerini tutan hello Data Lake deposu başka bir veri kümesi toospecify hello klasör ve dosya yolu oluşturun. Belirli tooAzure Data Lake Store dataset özellikler için bkz: [veri kümesi özellikleri](#dataset-properties) bölümü.
3. Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile. Daha önce bahsedilen hello örnekte BlobSource bir kaynak ve AzureDataLakeStoreSink havuzu olarak hello kopya etkinliği için kullanırsınız. Azure Data Lake Store tooAzure Blob Depolama kopyalıyorsanız benzer şekilde, AzureDataLakeStoreSource ve BlobSink hello kopyalama etkinliği kullanırsınız. Belirli tooAzure Data Lake Store kopyalama etkinliği özellikler için bkz: [kopyalama etkinliği özellikleri](#copy-activity-properties) bölümü. Nasıl toouse bir veri deposu bir kaynak veya bir havuz olarak hakkında daha fazla bilgi için veri deposu hello önceki bölümdeki hello bağlantısına tıklayın.  

Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur. Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.  Bir Azure Data Lake Store/kullanılan toocopy verileri olan Data Factory varlıkları için JSON tanımlarıyla örnekleri için bkz: [JSON örnekler](#json-examples-for-copying-data-to-and-from-data-lake-store) bu makalenin.

Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooData Lake deposu JSON özellikleri hakkında ayrıntılı bilgiler sağlar.

## <a name="linked-service-properties"></a>Bağlantılı hizmet özellikleri
Bağlı hizmet, bir veri deposu tooa veri fabrikası bağlar. Bağlı hizmet türü oluşturma **AzureDataLakeStore** toolink Data Lake Store veri tooyour data factory'nizi. Aşağıdaki tablonun hello JSON öğeleri belirli tooData Lake deposu bağlı Hizmetleri açıklar. Hizmet sorumlusu ve kullanıcı kimlik bilgileri doğrulaması arasında seçim yapabilirsiniz.

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| **türü** | Merhaba type özelliği çok ayarlanmalıdır**AzureDataLakeStore**. | Evet |
| **dataLakeStoreUri** | Hello Azure Data Lake Store hesabı hakkında bilgi sağlar. Bu bilgiler biçimleri aşağıdaki hello birini alır: `https://[accountname].azuredatalakestore.net/webhdfs/v1` veya `adl://[accountname].azuredatalakestore.net/`. | Evet |
| **Subscriptionıd** | Azure abonelik kimliği toowhich hello Data Lake Store hesabına ait. | Havuz için gerekli |
| **resourceGroupName** | Azure kaynak grubu adı toowhich hello Data Lake Store hesabına ait. | Havuz için gerekli |

### <a name="service-principal-authentication-recommended"></a>(Önerilen) hizmet asıl kimlik doğrulaması
Kayıt, hello Azure Active Directory (Azure AD) ve grant uygulama varlık toouse hizmet asıl kimlik doğrulaması, tooData Lake Store erişin. Ayrıntılı adımlar için bkz: [hizmeti için kimlik doğrulama](../data-lake-store/data-lake-store-authenticate-using-active-directory.md). Kullandığınız değerler aşağıdaki hello Not toodefine hello bağlantılı hizmeti:
* Uygulama Kimliği
* Uygulama anahtarı 
* Kiracı Kimliği

> [!IMPORTANT]
> Merhaba Kopyalama Sihirbazı'nı tooauthor veri ardışık kullanıyorsanız, hello hizmet sorumlusu vermek emin olun. en az bir **okuyucu** hello Data Lake Store hesabı için erişim denetimi (kimlik ve erişim yönetimi) rolü. Ayrıca, hello hizmet asıl en az izni **okuma + yürütme** izin tooyour Data Lake Store kök ("/") ve alt öğelerini. Aksi takdirde, selamlama iletisine "hello girilen kimlik bilgileri geçersiz." görebilirsiniz<br/><br/>
Oluşturma veya Azure AD içinde bir hizmet sorumlusu güncelleştirdikten sonra hello değişiklikleri tootake etkisi birkaç dakika sürebilir. Merhaba hizmet sorumlusu ve Data Lake Store erişim denetimi listesi (ACL) yapılandırmalarını denetleyin. Hala selamlama iletisine "geçersiz kimlik bilgileri sağlanan hello" görürseniz, bir süre bekleyin ve yeniden deneyin.

Aşağıdaki özelliklere hello belirterek hizmet asıl kimlik doğrulamasını kullan:

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| **servicePrincipalId** | Merhaba uygulamanın istemci kimliği belirtin. | Evet |
| **servicePrincipalKey** | Merhaba uygulamanın anahtarını belirtin. | Evet |
| **Kiracı** | Uygulamanızın bulunduğu altında Hello Kiracı bilgileri (etki alanı adı veya Kiracı kimliği) belirtin. Vurgulama hello fare hello sağ üst köşesindeki hello Azure portal tarafından alabilir. | Evet |

**Örnek: Hizmet asıl kimlik doğrulaması**
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>Kullanıcı kimlik bilgileri doğrulaması
Alternatif olarak, aşağıdaki özelliklere hello belirterek kullanıcı kimlik bilgileri kimlik doğrulaması toocopy gelen veya tooData Lake Store kullanabilirsiniz:

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| **Yetkilendirme** | Merhaba tıklatın **Authorize** hello Data Factory Düzenleyici'düğmesine tıklayın ve hello otomatik olarak oluşturulur yetkilendirme URL'si toothis özelliği atar kimlik bilgilerinizi girin. | Evet |
| **SessionID** | Merhaba OAuth yetkilendirme oturumundan OAuth oturum kimliği. Her oturum kimliği benzersiz olup yalnızca bir kez kullanılabilir. Merhaba Data Factory Düzenleyici kullandığınızda bu ayarı otomatik olarak oluşturulur. | Evet |

**Örnek: Kullanıcı kimlik bilgileri doğrulaması**
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

#### <a name="token-expiration"></a>Belirteç süre sonu
Merhaba hello kullanarak oluşturmak yetkilendirme kodu **Authorize** düğmesi belirli bir miktar süre sonra süresi dolar. iletiden hello hello kimlik doğrulama belirtecini süresi doldu anlamına gelir:

Kimlik bilgisi işlemi hatası: invalid_grant - AADSTS70002: Kimlik doğrulanırken hata oluştu. AADSTS70008: hello erişim izninin süresi doldu veya iptal sağlanan. İzleme kimliği: d18629e8-af88-43c5-88e3-d8419eb1fca1 bağıntı kimliği: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 zaman damgası: 2015-12-15 21 09 31Z.

Merhaba aşağıdaki tabloda farklı türlerdeki kullanıcı hesapları hello sona erme sürelerini gösterilmektedir:


| Kullanıcı türü | Kullanım süresi sonu |
|:--- |:--- |
| Kullanıcı hesaplarını *değil* Azure Active Directory tarafından yönetilen (örneğin, @hotmail.com veya @live.com) |12 saat |
| Azure Active Directory tarafından yönetilen kullanıcılar hesapları |14 gün sonra hello son dilim çalıştırın <br/><br/>90 OAuth tabanlı bir bağlantılı hizmette dayanan bir dilim 14 günde bir en az bir kez çalıştırıyorsa gün |

Merhaba belirteci süre sonu önce parolanızı değiştirirseniz, hello belirteci hemen süresi dolar. Bu bölümde daha önce bahsedilen hello iletisi görürsünüz.

Hello kullanarak hello hesabı yeniden yetkilendirmek **Authorize** tooredeploy hello hello belirtecinin süresi dolduğunda düğmesi bağlı hizmeti. Merhaba değerlerini de oluşturabilirsiniz **SessionID** ve **yetkilendirme** kullanarak program aracılığıyla özellikleri hello kodu:


```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```
Merhaba hello kod içinde kullanılan hello Data Factory sınıfları hakkında daha fazla bilgi için bkz [AzureDataLakeStoreLinkedService sınıfı](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService sınıfı](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), ve [ AuthorizationSessionGetResponse sınıfı](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) Konular. Bir başvuru tooversion ekleme `2.9.10826.1824` , `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` hello için `WindowsFormsWebAuthenticationDialog` hello kod içinde kullanılan bir sınıftır.

## <a name="dataset-properties"></a>Veri kümesi özellikleri
toospecify bir veri kümesi toorepresent girdi verileri Data Lake Store, ayarladığınız hello **türü** hello dataset özelliğinin çok**AzureDataLakeStore**. Set hello **linkedServiceName** hello dataset toohello hello Data Lake Store adını özelliğinin bağlı hizmeti. Merhaba JSON bölümler ve veri kümelerini tanımlamak için kullanılabilen özellikler tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi. JSON, bir veri kümesini bölümlerini gibi **yapısı**, **kullanılabilirlik**, ve **İlkesi**, tüm veri kümesi türleri için benzerdir (Azure SQL database, Azure blob ve Azure tablo için Örnek). Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve konum ve hello veri deposundaki hello veri biçimi gibi bilgiler sağlar. 

Merhaba **typeProperties** bir veri kümesi için bir bölüm türü **AzureDataLakeStore** aşağıdaki özelliklere hello içerir:

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| **folderPath** |Yol toohello kapsayıcı ve Data Lake Store klasörü. |Evet |
| **Dosya adı** |Azure Data Lake Store'da hello dosyasının adı. Merhaba **fileName** özelliği isteğe bağlıdır ve büyük küçük harfe duyarlı. <br/><br/>Belirtirseniz **fileName**, (kopyalama dahil) hello etkinlik hello belirli dosya üzerinde çalışır.<br/><br/>Zaman **fileName** belirtilmezse, kopyalama içeren tüm dosyaları **folderPath** hello girdi veri kümesi içinde.<br/><br/>Zaman **fileName** bir çıkış veri kümesi için belirtilmemiş ve **preserveHierarchy** belirtilmedi etkinlik havuzunda hello oluşturulan hello dosyasının adıdır veri hello biçiminde. _GUID_.txt'. Örnek: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt. |Hayır |
| **partitionedBy** |Merhaba **partitionedBy** özelliği isteğe bağlıdır. Toospecify dinamik bir yol ve dosya adını time series verilerini kullanabilirsiniz. Örneğin, **folderPath** için verileri saatte parametreli olabilir. Ayrıntılı bilgi ve örnekler için bkz: [hello partitionedBy özelliği](#using-partitionedby-property). |Hayır |
| **biçimi** | şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, ve  **ParquetFormat**. Set hello **türü** altında özellik **biçimi** tooone bu değerleri. Merhaba daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [JSON biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi ](data-factory-supported-file-and-compression-formats.md#parquet-format) hello bölümlerde [Azure Data Factory tarafından desteklenen dosya ve sıkıştırma biçimleri](data-factory-supported-file-and-compression-formats.md) makalesi. <br><br> Toocopy dosyaları isterseniz "olarak-olan" Merhaba dosya tabanlı depoları arasında (ikili kopya), atla `format` iki girdi ve çıktı veri kümesi tanımları bölümünde. |Hayır |
| **sıkıştırma** | Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin. Desteklenen türler **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**. Desteklenen düzeyler **Optimal** ve **en hızlı**. Daha fazla bilgi için bkz: [Azure Data Factory tarafından desteklenen dosya ve sıkıştırma biçimleri](data-factory-supported-file-and-compression-formats.md#compression-support). |Hayır |

### <a name="hello-partitionedby-property"></a>Merhaba partitionedBy özelliği
Dinamik belirtebilirsiniz **folderPath** ve **fileName** hello zaman serisi verilerle özelliklerini **partitionedBy** özelliği, veri fabrikası işlevleri ve sistem değişkenleri. Merhaba Ayrıntılar için bkz [Azure Data Factory - işlevler ve sistem değişkenleri](data-factory-functions-variables.md) makalesi.


Örneğin, aşağıdaki hello içinde `{Slice}` hello hello Data Factory sistem değişkeninin değeriyle değiştirilir `SliceStart` belirtilen hello biçiminde (`yyyyMMddHH`). Merhaba adı `SliceStart` toohello hello dilimin başlangıç zamanı gösterir. Merhaba `folderPath` özelliktir giriş olarak her dilim için farklı `wikidatagateway/wikisampledataout/2014100103` veya `wikidatagateway/wikisampledataout/2014100104`.

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

Aşağıdaki örnek, hello yıl, ay, gün ve saat hello içinde `SliceStart` hello tarafından kullanılan ayrı değişkenleri içine ayıklanan `folderPath` ve `fileName` özellikleri:
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
Zaman serisi veri kümeleri hakkında daha fazla ayrıntı için zamanlama ve dilim hello bkz [Azure Data Factory'deki veri kümelerini](data-factory-create-datasets.md) ve [Data Factory zamanlama ve yürütme](data-factory-scheduling-and-execution.md) makaleleri. 


## <a name="copy-activity-properties"></a>Etkinlik özellikleri Kopyala
Merhaba bölümler ve etkinlikleri tanımlamak için kullanılabilen özellikler tam listesi için bkz [ardışık düzen oluşturma](data-factory-create-pipelines.md) makalesi. Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.

Merhaba hello kullanılabilen özellikleri **typeProperties** bölüm etkinliğin her etkinlik türü ile değişir. Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.

**AzureDataLakeStoreSource** hello özelliğinde aşağıdaki hello destekleyen **typeProperties** bölümü:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| **özyinelemeli** |Merhaba klasörlerdeki veya yalnızca klasörden hello belirtilen Hello veri yinelemeli olarak okunur olup olmadığını gösterir. |(Varsayılan değer) false değerini true |Hayır |


**AzureDataLakeStoreSink** hello özelliklerinde aşağıdaki hello destekleyen **typeProperties** bölümü:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| **copyBehavior** |Merhaba kopyalama davranışını belirtir. |<b>PreserveHierarchy</b>: hello dosya hiyerarşisi hello hedef klasörde korur. Kaynak dosya toosource klasörünün göreli yolu Hello aynı toohello göreli hedef dosya tootarget klasör yoludur.<br/><br/><b>FlattenHierarchy</b>: hello kaynak klasördeki tüm dosyaları hello ilk düzeyi hello hedef klasörü içinde oluşturulur. Merhaba hedef dosyaları otomatik olarak oluşturulur adlarıyla oluşturulur.<br/><br/><b>MergeFiles</b>: hello kaynak klasör tooone dosyasından tüm dosyaları birleştirir. Merhaba dosya veya blob adı belirtilirse, hello belirtilen ad hello birleştirilmiş dosya adı değil. Aksi takdirde hello dosya adı oluşturulur. |Hayır |

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

## <a name="supported-file-and-compression-formats"></a>Desteklenen dosya ve sıkıştırma biçimleri
Merhaba Ayrıntılar için bkz [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md) makalesi.

## <a name="json-examples-for-copying-data-tooand-from-data-lake-store"></a>Veri tooand Data Lake Deposu'ndan veri kopyalamak için JSON örnekleri
Merhaba örnekleri aşağıdaki örnek JSON tanımları sağlar. Bu örnek tanımları toocreate bir ardışık düzen hello kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). örneklerde nasıl hello toocopy veri tooand Data Lake Store ve Azure Blob depolama biriminden. Ancak, veriler kopyalanabilir _doğrudan_ herhangi birinden hello kaynakları tooany desteklenen hello havuzlarını biri. Daha fazla bilgi için "desteklenen veri depoları ve biçimleri" Merhaba bölümüne hello bkz [Kopyala etkinliğini kullanarak veri taşıma](data-factory-data-movement-activities.md) makalesi.  

### <a name="example-copy-data-from-azure-blob-storage-tooazure-data-lake-store"></a>Örnek: verileri Azure Blob Storage tooAzure Data Lake Store kopyalayın.
Bu bölümdeki kod Hello örneği gösterilmektedir:

* Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Bağlı hizmet türü [AzureDataLakeStore](#linked-service-properties).
* Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureDataLakeStore](#dataset-properties).
* A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) ve [AzureDataLakeStoreSink](#copy-activity-properties).

Merhaba örnekler ne zaman serisi verileri Azure Blob depolama biriminden göstermek tooData Lake Store saatte kopyalanır. 

**Azure Storage bağlı hizmeti**

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

**Azure Data Lake Store hizmeti bağlı**

```JSON
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

> [!NOTE]
> Merhaba yapılandırma ayrıntıları için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü.
>

**Azure Blob girdi veri kümesi**

Aşağıdaki örneğine hello veri yeni blob üzerinden saatte kayıt (`"frequency": "Hour", "interval": 1`). Merhaba klasör yolu ve dosya adını hello blob dinamik olarak değerlendirilir işleniyor hello dilimin hello başlangıç zamanı temel alınarak. Merhaba klasör yolu hello yıl, ay ve gün kısmı hello başlangıç saati kullanır. Merhaba dosya adı hello saat hello kısmı başlangıç saati kullanır. Merhaba `"external": true` ayarı bildirir hello Data Factory hizmetinin bu hello tablosu dış toohello veri fabrikası ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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

**Azure Data Lake Store çıkış dataset**

Aşağıdaki örnek kopya veri tooData Lake deposu hello. Yeni veri kopyalanır tooData Lake Store her saat.

```JSON
{
    "name": "AzureDataLakeStoreOutput",
      "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
              "frequency": "Hour",
              "interval": 1
        }
      }
}
```


**Bir blob kaynağı ve Data Lake Store havuz sahip işlem hattı kopyalama etkinliği**

Aşağıdaki örneğine hello hello ardışık düzen yapılandırılmış bir kopyalama etkinliği içeren toouse hello girdi ve çıktı veri kümeleri. Merhaba kopyalama etkinliği zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello `source` türü olarak ayarlanmış çok`BlobSource`ve hello `sink` türü olarak ayarlanmış çok`AzureDataLakeStoreSink`.

```json
{  
    "name":"SamplePipeline",
    "properties":
    {  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":
        [  
              {
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureBlobInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureDataLakeStoreOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                      },
                      "sink": {
                        "type": "AzureDataLakeStoreSink"
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

### <a name="example-copy-data-from-azure-data-lake-store-tooan-azure-blob"></a>Örnek: Verilerini Azure Data Lake Store tooan Azure blob
Bu bölümdeki kod Hello örneği gösterilmektedir:

* Bağlı hizmet türü [AzureDataLakeStore](#linked-service-properties).
* Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureDataLakeStore](#dataset-properties).
* Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [AzureDataLakeStoreSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Merhaba kodu time series verilerini her saat Data Lake Store tooan Azure blob ' kopyalar. 

**Azure Data Lake Store hizmeti bağlı**

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>"
        }
    }
}
```

> [!NOTE]
> Merhaba yapılandırma ayrıntıları için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü.
>

**Azure Storage bağlı hizmeti**

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
**Azure Data Lake girdi veri kümesi**

Bu örnekte, ayarı `"external"` çok`true` hello Data Factory hizmetinin bu hello tablosu dış toohello veri fabrikası ve hello veri fabrikasında bir etkinlik tarafından üretilen değil bildirir.

```json
{
    "name": "AzureDataLakeStoreInput",
      "properties":
    {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
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
**Azure Blob çıktı veri kümesi**

Aşağıdaki örneğine hello veriler her saat tooa yeni blob yazılır (`"frequency": "Hour", "interval": 1`). hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir. Merhaba klasör yolu hello yıl, ay, gün ve saat bölümünü hello başlangıç saati kullanır.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Bir Azure Data Lake Store kaynak ve blob havuz sahip işlem hattı kopyalama etkinliği**

Aşağıdaki örneğine hello hello ardışık düzen yapılandırılmış bir kopyalama etkinliği içeren toouse hello girdi ve çıktı veri kümeleri. Merhaba kopyalama etkinliği zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello `source` türü olarak ayarlanmış çok`AzureDataLakeStoreSource`ve hello `sink` türü olarak ayarlanmış çok`BlobSink`.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureDakeLaketoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureDataLakeStoreInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "AzureDataLakeStoreSource",
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

Merhaba kopyalama etkinlik tanımında hello kaynak dataset toocolumns hello havuz kümesindeki sütunlarından eşleyebilirsiniz. Ayrıntılar için bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Performans ve ayar
Kopyalama etkinliği performansı etkileyen hello Etkenler hakkında toolearn ve nasıl toooptimize, hello bkz [kopyalama etkinliği performans ve ayarlama Kılavuzu](data-factory-copy-activity-performance.md) makalesi.
