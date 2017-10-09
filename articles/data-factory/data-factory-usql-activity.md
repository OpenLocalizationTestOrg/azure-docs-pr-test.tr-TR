---
title: "U-SQL betiği - Azure kullanarak aaaTransform veri | Microsoft Docs"
description: "Üzerinde Azure Data Lake Analytics U-SQL komut dosyaları çalıştırarak tooprocess veya dönüştürme veri hizmeti nasıl işlem öğrenin."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e17c1255-62c2-4e2e-bb60-d25274903e80
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: spelluru
ms.openlocfilehash: 51fdb40334d0c131720f65c3a96b4c5045a98b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a>Üzerinde Azure Data Lake Analytics U-SQL betiklerini çalıştırarak veri dönüştürme 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Hive etkinliği](data-factory-hive-activity.md) 
> * [Pig etkinliği](data-factory-pig-activity.md)
> * [MapReduce etkinliği](data-factory-map-reduce.md)
> * [Hadoop akış etkinliği](data-factory-hadoop-streaming-activity.md)
> * [Spark etkinliği](data-factory-spark.md)
> * [Machine Learning Batch Yürütme Etkinliği](data-factory-azure-ml-batch-execution-activity.md)
> * [Machine Learning Kaynak Güncelleştirme Etkinliği](data-factory-azure-ml-update-resource-activity.md)
> * [Saklı Yordam Etkinliği](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL Etkinliği](data-factory-usql-activity.md)
> * [.NET özel etkinlik](data-factory-use-custom-activities.md)

Bir Azure data factory işlem hattı bağlantılı işlem hizmetlerini kullanarak bağlantılı depolama Hizmetleri'nde verilerini işler. Burada her etkinlik özel işleme işlemi gerçekleştiren etkinlikler dizisini içerir. Bu makalede hello **Data Lake Analytics U-SQL etkinliği** çalıştıran bir **U-SQL** üzerinde komut dosyası bir **Azure Data Lake Analytics** bağlantılı hizmet işlem. 

> [!NOTE]
> Bir Azure Data Lake Analytics hesabı, bir veri Lake Analytics U-SQL etkinliği ile işlem hattı oluşturmadan önce oluşturun. Azure Data Lake Analytics hakkında toolearn bkz [Azure Data Lake Analytics ile çalışmaya başlama](../data-lake-analytics/data-lake-analytics-get-started-portal.md).
> 
> Gözden geçirme hello [ilk ardışık düzen öğreticinizi yapı](data-factory-build-your-first-pipeline.md) ayrıntılı adımlar toocreate veri fabrikası için hizmetler, veri kümeleri ve işlem hattı bağlı. JSON parçacığı, Data Factory Düzenleyici veya Visual Studio ya da Azure PowerShell toocreate Data Factory varlıklarını kullanın.

## <a name="supported-authentication-types"></a>Desteklenen kimlik doğrulama türleri
Data Lake Analytics karşı kimlik doğrulama türleri aşağıdaki U-SQL etkinliği destekler:
* Hizmet sorumlusu kimlik doğrulaması
* Kullanıcı kimlik bilgisi (OAuth) kimlik doğrulaması 

Zamanlanmış U-SQL yürütmesi için özellikle bir hizmet asıl kimlik doğrulaması kullanmanızı öneririz. Belirteç süre sonu davranış kullanıcı kimlik bilgilerinin ile ortaya çıkabilir. Merhaba yapılandırma ayrıntıları için bkz: [bağlantılı hizmet özellikleri](#azure-data-lake-analytics-linked-service) bölümü.

## <a name="azure-data-lake-analytics-linked-service"></a>Azure Data Lake Analytics hizmeti bağlı
Oluşturduğunuz bir **Azure Data Lake Analytics** bağlantılı hizmet toolink bir Azure Data Lake Analytics işlem hizmeti tooan Azure data factory. Merhaba Data Lake Analytics U-SQL etkinliği hello ardışık düzende toothis bağlantılı hizmeti anlamına gelmektedir. 

Merhaba aşağıdaki tabloda Merhaba açıklamalarına hello JSON tanımını kullanılan genel özellikleri sağlar. Daha fazla hizmet sorumlusu ve kullanıcı kimlik bilgileri doğrulaması arasında seçim yapabilirsiniz.

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| **türü** |Merhaba type özelliği ayarlanmalıdır: **AzureDataLakeAnalytics**. |Evet |
| **accountName** |Azure Data Lake Analytics hesap adı. |Evet |
| **dataLakeAnalyticsUri** |Azure Data Lake Analytics URI. |Hayır |
| **Subscriptionıd** |Azure abonelik kimliği |Hayır (belirtilmezse, veri fabrikası kullanılan hello abonelik). |
| **resourceGroupName** |Azure kaynak grubu adı |Hayır (belirtilmezse, veri fabrikası kullanılan hello kaynak grubu). |

### <a name="service-principal-authentication-recommended"></a>(Önerilen) hizmet asıl kimlik doğrulaması
Kayıt, hello Azure Active Directory (Azure AD) ve grant uygulama varlık toouse hizmet asıl kimlik doğrulaması, tooData Lake Store erişin. Ayrıntılı adımlar için bkz: [hizmeti için kimlik doğrulama](../data-lake-store/data-lake-store-authenticate-using-active-directory.md). Kullandığınız değerler aşağıdaki hello Not toodefine hello bağlantılı hizmeti:
* Uygulama Kimliği
* Uygulama anahtarı 
* Kiracı Kimliği

Aşağıdaki özelliklere hello belirterek hizmet asıl kimlik doğrulamasını kullan:

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| **servicePrincipalId** | Merhaba uygulamanın istemci kimliği belirtin. | Evet |
| **servicePrincipalKey** | Merhaba uygulamanın anahtarını belirtin. | Evet |
| **Kiracı** | Uygulamanızın bulunduğu altında Hello Kiracı bilgileri (etki alanı adı veya Kiracı kimliği) belirtin. Vurgulama hello fare hello sağ üst köşesindeki hello Azure portal tarafından alabilir. | Evet |

**Örnek: Hizmet asıl kimlik doğrulaması**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>Kullanıcı kimlik bilgileri doğrulaması
Alternatif olarak, aşağıdaki özelliklere hello belirterek Data Lake Analytics için kullanıcı kimlik bilgilerinin kullanabilirsiniz:

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| **Yetkilendirme** | Merhaba tıklatın **Authorize** hello Data Factory Düzenleyici'düğmesine tıklayın ve hello otomatik olarak oluşturulur yetkilendirme URL'si toothis özelliği atar kimlik bilgilerinizi girin. | Evet |
| **SessionID** | Merhaba OAuth yetkilendirme oturumundan OAuth oturum kimliği. Her oturum kimliği benzersiz olup yalnızca bir kez kullanılabilir. Merhaba Data Factory Düzenleyici kullandığınızda bu ayarı otomatik olarak oluşturulur. | Evet |

**Örnek: Kullanıcı kimlik bilgileri doğrulaması**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a>Belirteç süre sonu
Merhaba oluşturulan hello kullanarak Yetkilendirme kodu **Authorize** düğmesi süre sonra süresi dolar. Farklı türlerdeki kullanıcı hesapları için hello bitiş zamanları için aşağıdaki tablonun hello bakın. Aşağıdaki hata iletisini hello görebilirsiniz zaman kimlik doğrulaması'nı hello **belirtecinin süresi dolmadan**: kimlik bilgisi işlemi hatası: invalid_grant - AADSTS70002: Kimlik doğrulanırken hata oluştu. AADSTS70008: hello erişim izninin süresi doldu veya iptal sağlanan. İzleme kimliği: d18629e8-af88-43c5-88e3-d8419eb1fca1 bağıntı kimliği: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 zaman damgası: 2015-12-15 21:09:31Z

| Kullanıcı türü | Kullanım süresi sonu |
|:--- |:--- |
| Azure Active Directory tarafından yönetilmeyen kullanıcı hesapları (@hotmail.com, @live.comvb..) |12 saat |
| Azure Active Directory (AAD tarafından) yönetilen kullanıcı hesapları |14 gün sonra hello son dilim çalıştırın. <br/><br/>90 OAuth tabanlı bağlantılı hizmette dayanan bir dilim 14 günde bir en az bir kez çalıştırılıyorsa, gün. |

tooavoid/Çöz bu hata, hello kullanarak yeniden yetkilendirin **Authorize** düğmesini hello **belirtecinin süresi dolmadan** ve hello bağlantılı hizmeti yeniden dağıtın. Değerleri de oluşturabilirsiniz **SessionID** ve **yetkilendirme** kullanılarak programlı olarak kod şu şekilde özellikleri:

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

Bkz: [AzureDataLakeStoreLinkedService sınıfı](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService sınıfı](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), ve [AuthorizationSessionGetResponse sınıfı](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) ayrıntıları konuları Merhaba kod içinde kullanılan hello Data Factory sınıfları hakkında. Bir başvuru ekleyin: Merhaba WindowsFormsWebAuthenticationDialog sınıfı için Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll. 

## <a name="data-lake-analytics-u-sql-activity"></a>Data Lake Analytics U-SQL Etkinliği
JSON parçacığı aşağıdaki hello bir Data Lake Analytics U-SQL etkinliği ile işlem hattı tanımlar. Merhaba etkinlik tanımı başvuru toohello daha önce oluşturduğunuz Azure Data Lake Analytics bağlantılı hizmet yok.   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline toocompute events for en-gb locale and date less than 2012/02/19.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00Z",
        "end": "2015-08-08T01:00:00Z",
        "isPaused": false
    }
}
```

Merhaba aşağıdaki tabloda adları ve açıklamaları belirli toothis etkinlik özellikleri açıklanmaktadır. 

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| type |Merhaba type özelliği çok ayarlanmalıdır**DataLakeAnalyticsU SQL**. |Evet |
| scriptPath |Merhaba U-SQL betiğini içeren yolu toofolder. Merhaba dosyasının adı büyük/küçük harf duyarlıdır. |Hayır (komut dosyası kullanırsanız) |
| scriptLinkedService |Merhaba betik toohello veri fabrikası içeren hello depolamayı bağlı hizmet |Hayır (komut dosyası kullanırsanız) |
| Komut dosyası |ScriptPath ve scriptLinkedService belirtme yerine satır içi betiği belirtin. Örneğin: `"script": "CREATE DATABASE test"`. |Hayır (scriptPath ve scriptLinkedService kullanıyorsanız) |
| degreeOfParallelism |Merhaba en fazla düğüm sayısını toorun hello işi aynı anda kullanılır. |Hayır |
| Öncelik |Sıraya alınan tüm işlerden seçili toorun olması gereken ilk belirler. Merhaba alt hello numarası hello yüksek hello önceliği. |Hayır |
| parametreler |Merhaba U-SQL komut dosyası için parametreler |Hayır |
| runtimeVersion | U-SQL hello altyapısı toouse çalışma zamanı sürümü | Hayır | 
| compilationMode | <p>U-SQL derleme modu. Şu değerlerden biri olmalıdır:</p> <ul><li>**Anlam:** yalnızca anlamsal denetler ve gerekli sağlamlık denetimleri gerçekleştirin.</li><li>**Tam:** sözdizimi denetimi, en iyi duruma getirme, kod oluşturma, vb. dahil olmak üzere hello tam derleme gerçekleştirin.</li><li>**SingleBox:** TargetType ayarı tooSingleBox ile Merhaba tam derleme gerçekleştirin.</li></ul><p>Bu özellik için bir değer belirtmezseniz, hello sunucu hello en iyi bir derleme moduna belirler. </p>| Hayır | 

Bkz: [SearchLogProcessing.txt betik tanımı](#sample-u-sql-script) hello betik tanımı. 

## <a name="sample-input-and-output-datasets"></a>Örnek girdi ve çıktı veri kümeleri
### <a name="input-dataset"></a>Girdi veri kümesi
Bu örnekte, bir Azure Data Lake Store (Merhaba datalake/giriş klasörünü dosyasında searchlog.tsv dosyasını) hello giriş verisi bulunur. 

```json
{
    "name": "DataLakeTable",
    "properties": {
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
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}    
```

### <a name="output-dataset"></a>Çıktı veri kümesi
Bu örnekte, U-SQL betiği hello tarafından üretilen hello çıktı verilerini bir Azure Data Lake Store'da (datalake/çıkış klasörü) depolanır. 

```json
{
    "name": "EventsByRegionTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="sample-data-lake-store-linked-service"></a>Bağlantılı hizmetinin örnek veri Gölü deposu
Azure Data Lake Store giriş/çıkış hello veri kümeleri tarafından kullanılan hizmet bağlı hello örnek hello tanımı aşağıda verilmiştir. 

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
        }
    }
}
```

Bkz: [veri tooand Azure Data Lake Deposu'ndan veri taşıma](data-factory-azure-datalake-connector.md) makale açıklamaları JSON özellikleri için. 

## <a name="sample-u-sql-script"></a>Örnek U-SQL betiği

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    too@out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

Merhaba değerlerini  **@in**  ve  **@out**  hello U-SQL betiği parametrelerinde geçirilir dinamik olarak ADF tarafından hello 'parameters' bölümünü kullanarak. Merhaba ardışık düzen tanımı Hello 'parameters' bölümüne bakın.

DegreeOfParallelism ve öncelik gibi diğer özellikleri ardışık düzen tanımınızı hello Azure Data Lake Analytics hizmeti üzerinde çalıştırılan hello işleri için de belirtebilirsiniz.

## <a name="dynamic-parameters"></a>Dinamik parametreler
Merhaba örnek ardışık düzen tanımı'nda giriş ve çıkış parametreleri sabit kodlanmış değerler ile atandı. 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

Bunun yerine olası toouse dinamik parametreleri olur. Örneğin: 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

Bu durumda, giriş dosyaları hala hello /datalake/input klasöründen toplanmış ve çıktı dosyalarını hello /datalake/output klasöründe oluşturulur. Merhaba dosya hello dilim başlangıç zamanı temel alınarak dinamik adlardır.  

