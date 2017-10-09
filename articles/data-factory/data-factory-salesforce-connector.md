---
title: "Veri Fabrikası kullanarak aaaMove verilerden Salesforce | Microsoft Docs"
description: "Hakkında bilgi edinin Azure Data Factory kullanarak toomove verilerden Salesforce."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: dbe3bfd6-fa6a-491a-9638-3a9a10d396d1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: c1bde2a333f5a3c0a995eb8c13ecf585132888b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a>Azure Data Factory kullanarak Salesforce taşıma verileri
Bu makalede Azure data factory toocopy veri Salesforce tooany veri deposundan hello havuz hello sütununda altında listelenen kopyalama etkinliği nasıl kullanabileceğiniz özetlenmektedir [desteklenen kaynakları ve havuzlarını](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo. Bu makale üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) desteklenen veri deposu birleşimleri kopyalama etkinliği ile veri taşıma için genel bir bakış sunan makalesi.

Azure Data Factory şu anda destekler verileri Salesforce çok taşıma yalnızca[havuz veri depolarına desteklenen](data-factory-data-movement-activities.md#supported-data-stores-and-formats), ancak diğer veri depoları tooSalesforce gelen veri taşımayı desteklemez.

## <a name="supported-versions"></a>Desteklenen sürümler
Bu bağlayıcı Salesforce sürümleri aşağıdaki hello destekler: Geliştirici sürümü, Professional Edition, Enterprise Edition veya sınırsız sürümü. Ve Salesforce üretim, korumalı alan ve özel etki alanı kopyalama destekler.

## <a name="prerequisites"></a>Ön koşullar
* API izni etkinleştirilmesi gerekir. Bkz: [nasıl Salesforce API erişim izni kümesi tarafından etkinleştirebilirim?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)
* Salesforce tooon içi veri depolarına toocopy verileri, sahip olmanız gerekir en az veri yönetimi ağ geçidi şirket içi ortamınızda yüklü 2.0.

## <a name="salesforce-request-limits"></a>Salesforce istek sınırları
Salesforce toplam API istekleri ve eşzamanlı API istekleri için sınırları vardır. Hello aşağıdaki noktaları göz önünde bulundurun:

- Eşzamanlı istek sayısını Hello hello sınırını aşarsa, azaltma gerçekleşir ve rastgele hatalara görürsünüz.
- Merhaba toplam istek sayısı hello sınırını aşarsa, 24 saat hello Salesforce hesap engellenir.

Ayrıca, her iki senaryoda hello "REQUEST_LIMIT_EXCEEDED" hatası alabilirsiniz. Merhaba Hello "API istek sınırlarını" bölümüne bakın [Salesforce Geliştirici sınırları](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) Ayrıntılar için makale.

## <a name="getting-started"></a>Başlarken
Farklı araçlar/API'lerini kullanarak Salesforce verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.

Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**. Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.

Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**. Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için. 

Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin: 

1. Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.
2. Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi. 
3. Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile. 

Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur. Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.  Salesforce kullanılan toocopy veri Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: Blob Salesforce tooAzure veri kopyalama](#json-example-copy-data-from-salesforce-to-azure-blob) bu makalenin. 

Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooSalesforce olan JSON özellikleri hakkında ayrıntılı bilgi sağlar: 

## <a name="linked-service-properties"></a>Bağlantılı hizmet özellikleri
Aşağıdaki tablonun hello belirli toohello Salesforce bağlantılı hizmet JSON öğeleri için açıklamalar sağlanır.

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| type |Merhaba type özelliği ayarlanmalıdır: **Salesforce**. |Evet |
| environmentUrl | Merhaba, URL Salesforce örneği belirtin. <br><br> -Varsayılan değer "https://login.salesforce.com" dir. <br> -Korumalı alan, toocopy verileri "https://test.salesforce.com" belirtin. <br> -toocopy verileri özel bir etki alanından belirtin, örneğin, "https://[domain].my.salesforce.com". |Hayır |
| kullanıcı adı |Merhaba kullanıcı hesabı için bir kullanıcı adı belirtin. |Evet |
| password |Merhaba kullanıcı hesabı için bir parola belirtin. |Evet |
| securityToken |Merhaba kullanıcı hesabı için bir güvenlik belirteci belirtin. Bkz: [güvenlik belirteci alma getirin](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) yönelik yönergeler tooreset/get bir güvenlik belirteci. Genel olarak, toolearn güvenlik belirteçleri hakkında bkz [güvenlik ve hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm). |Evet |

## <a name="dataset-properties"></a>Veri kümesi özellikleri
Merhaba bölümler ve veri kümelerini tanımlamak için kullanılabilir olan özellikleri tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi. Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri kümesi türleri için (Azure SQL, Azure blob, Azure tablo ve benzeri) benzer.

Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar. Merhaba typeProperties bölümünde hello türü veri kümesi için **RelationalTable** hello aşağıdaki özelliklere sahiptir:

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| tableName |Salesforce Merhaba tablonun adı. |Hayır (varsa bir **sorgu** , **RelationalSource** belirtilir) |

> [!IMPORTANT]
> Merhaba "__c" Merhaba API adı parçası herhangi bir özel nesnesi için gereklidir.

![Veri Fabrikası - Salesforce bağlantı - API adı](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a>Etkinlik özellikleri Kopyala
Merhaba bölümler ve etkinlikleri tanımlamak için kullanılabilir olan özellikleri tam listesi için bkz [ardışık düzen oluşturma](data-factory-create-pipelines.md) makalesi. Ad, açıklama, giriş ve çıkış tabloları özellikler gibi ve çeşitli ilkeleri etkinlikleri tüm türleri için kullanılabilir.

kullanılabilir hello özellikleri hello faaliyete hello typeProperties bölümünü diğer yandan Merhaba, her etkinlik türü ile değişir. Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.

Kopyalama etkinliğinde hello kaynağı hello türü olduğunda **RelationalSource** (içeren Salesforce), aşağıdaki özelliklere hello typeProperties bölümünde bulunur:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| sorgu |Merhaba özel sorgu tooread verileri kullanın. |Bir SQL-92 sorgu veya [Salesforce nesnesi sorgu dili (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) sorgu. Örneğin:  `select * from MyTable__c`. |Hayır (Merhaba, **tableName** Merhaba, **dataset** belirtilir) |

> [!IMPORTANT]
> Merhaba "__c" Merhaba API adı parçası herhangi bir özel nesnesi için gereklidir.

![Veri Fabrikası - Salesforce bağlantı - API adı](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a>Sorgu ipuçları
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a>WHERE kullanarak veri alma DateTime sütun yan tümcesi
Ne zaman hello SOQL veya SQL sorgusu, ödeme dikkat toohello DateTime biçimi fark belirtin. Örneğin:

* **SOQL örnek**:`$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`
* **SQL örneği**:
    * **Kopyalama Sihirbazı'nı toospecify hello sorgu kullanarak:**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`
    * **JSON toospecify hello sorgu düzenlemeye kullanarak (char düzgün kaçış):**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`

### <a name="retrieving-data-from-salesforce-report"></a>Salesforce raporundan veri alma
Sorgu olarak belirterek Salesforce raporlarını veri alabilirsiniz `{call "<report name>"}`, örneğin,. `"query": "{call \"TestReport\"}"`.

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a>Kayıtları Salesforce Geri Dönüşüm Kutusu'ndan silinen alma
Salesforce geri dönüşüm kutusu tooquery hello yumuşak silinmiş kayıtları, belirtebilirsiniz **"IsDeleted = 1"** Sorgunuzdaki. Örneğin,

* tooquery yalnızca hello silinmiş kayıtlar belirtin "seçin * MyTable__c gelen **burada IsDeleted = 1**"
* Tüm hello hello mevcut ve Silinen, hello dahil olmak üzere kayıtları tooquery belirtin "seçin * MyTable__c gelen **burada IsDeleted = 0 ya da IsDeleted = 1**"

## <a name="json-example-copy-data-from-salesforce-tooazure-blob"></a>JSON örnek: Blob Salesforce tooAzure veri kopyalama
Merhaba aşağıdaki örnek örnek JSON tanımları sağlar, toocreate bir ardışık düzen hello kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Bunlar Göster nasıl Salesforce tooAzure Blob Storage toocopy verileri. Ancak, veri belirtildiği hello havuzlarını, kopyalanan tooany olabilir [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.   

Burada, toocreate tooimplement hello senaryo gerekir hello Data Factory yapıtlarının bulunmaktadır. Merhaba listesini izleyen hello bölümler bu adımlar hakkında ayrıntılı bilgi sağlar.

* Merhaba türündeki bağlı hizmetin [Salesforce](#linked-service-properties)
* Merhaba türündeki bağlı hizmetin [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
* Bir giriş [dataset](data-factory-create-datasets.md) hello türü [RelationalTable](#dataset-properties)
* Bir çıkış [dataset](data-factory-create-datasets.md) hello türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
* A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [RelationalSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)

**Salesforce bağlı hizmet**

Bu örnek hello kullanır **Salesforce** bağlı hizmeti. Merhaba bkz [Salesforce bağlantılı hizmeti](#linked-service-properties) bu bağlantılı hizmet tarafından desteklenen hello özellikler bölümü.  Bkz: [güvenlik belirteci alma getirin](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) nasıl tooreset/get hello güvenlik belirteci hakkında yönergeler için.

```json
{
    "name": "SalesforceLinkedService",
    "properties":
    {
        "type": "Salesforce",
        "typeProperties":
        {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```
**Azure Storage bağlı hizmeti**

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
**Salesforce girdi veri kümesi**

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"  
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

Ayarı **dış** çok**true** hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil bildirir.

> [!IMPORTANT]
> Merhaba "__c" Merhaba API adı parçası herhangi bir özel nesnesi için gereklidir.

![Veri Fabrikası - Salesforce bağlantı - API adı](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

**Azure Blob çıktı veri kümesi**

Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/alltypes_c"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Kopyalama etkinliği ile işlem hattı**

Merhaba ardışık düzen içeren yapılandırılmış kopyalama etkinliği toouse girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**RelationalSource**ve hello **havuz** türü olarak ayarlanmış çok**BlobSink**.

Bkz: [RelationalSource türü özellikleri](#copy-activity-properties) hello RelationalSource hello tarafından desteklenen özelliklerin listesi için.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "SalesforceInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"                
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
> [!IMPORTANT]
> Merhaba "__c" Merhaba API adı parçası herhangi bir özel nesnesi için gereklidir.

![Veri Fabrikası - Salesforce bağlantı - API adı](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a>Tür eşlemesi için Salesforce
| Salesforce türü | . NET tabanlı türü |
| --- | --- |
| Otomatik numara |Dize |
| Onay kutusu |Boole değeri |
| Para birimi |Çift |
| Tarih |Tarih saat |
| Tarih/saat |Tarih saat |
| E-posta |Dize |
| Kimlik |Dize |
| Arama ilişkisi |Dize |
| Çoklu seçim seçim listesi |Dize |
| Sayı |Çift |
| Yüzde |Çift |
| Telefon |Dize |
| Seçim listesi |Dize |
| Metin |Dize |
| Metin alanı |Dize |
| Metin alanı (uzun) |Dize |
| Metin alanı (zengin) |Dize |
| Metin (şifrelenmiş) |Dize |
| URL |Dize |

> [!NOTE]
> Kaynak veri kümesi toocolumns havuz kümesinden toomap sütunlarından bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a>Performans ve ayar
Merhaba bkz [kopyalama etkinliği performans ve ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.
