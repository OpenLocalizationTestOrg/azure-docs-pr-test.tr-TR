---
title: "ODBC veri depolarına aaaMove verilerden | Microsoft Docs"
description: "Azure Data Factory kullanarak ODBC veri toomove verileri nasıl depolar hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ad70a598-c031-4339-a883-c6125403cb76
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: bf96e71da449313b6144bb194205c572d2ca2030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a>Azure Data Factory kullanarak veri öğesinden ODBC veri depolarını taşıma
Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove verileri bir şirket içi ODBC veri depolamak açıklanmaktadır. Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.

Bir ODBC veri deposu desteklenen tooany havuz veri deposundan verileri kopyalayabilirsiniz. Verileri bir listesi için desteklenen depoları hello kopyalama etkinliği tarafından havuzlarını hello görür [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo. Veri Fabrikası şu anda bir ODBC veri verilerden tooother veri depolarına depolamak taşıma yalnızca, ancak diğer veri depoları tooan ODBC veri deposundan veri taşıma değil destekler. 

## <a name="enabling-connectivity"></a>Bağlantıyı etkinleştirme
Data Factory Hizmeti'ne hello veri yönetimi ağ geçidi kullanarak bağlanan tooon içi ODBC kaynakları destekler. Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale toolearn veri yönetimi ağ geçidi ve hello ağ geçidi kurun ayarlama hakkında adım adım yönergeleri hakkında. Bir Azure Iaas sanal barındırılan olsa bile hello ağ geçidi tooconnect tooan ODBC veri deposunu kullan.

Merhaba ağ geçidi içi aynı makine veya hello ODBC veri deposu olarak Azure VM hello hello yükleyebilirsiniz. Ancak, bir ayrı makine/Azure Iaas VM hello ağ geçidi yüklemenizi öneririz tooavoid kaynak çekişmesini ve daha iyi performans için. Merhaba ağ geçidi ayrı bir makineye yüklediğinizde hello makine hello ODBC veri deposu ile mümkün tooaccess hello makine olmalıdır.

Veri Yönetimi ağ geçidi Hello dışında ayrıca tooinstall hello ODBC sürücüsü hello veri deposu hello gateway makinesinde gerekir.

> [!NOTE]
> Bkz: [ağ geçidi sorunlarını giderme](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) ilgili sorunlar bağlantı/ağ geçidi sorun giderme ipuçları için.

## <a name="getting-started"></a>Başlarken
Farklı araçlar/API'lerini kullanarak bir ODBC veri deposundan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.

Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**. Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.

Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu **, **.NET API**, ve **REST API**. Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için. 

Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin: 

1. Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.
2. Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi. 
3. Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile. 

Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur. Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.  Bir ODBC veri deposundaki kullanılan toocopy verileri Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: ODBC veri verilerini depolamak tooAzure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) bu makalenin. 

Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooODBC veri deposu olan JSON özellikleri hakkında ayrıntılı bilgi sağlar:

## <a name="linked-service-properties"></a>Bağlantılı hizmet özellikleri
Aşağıdaki tablonun hello JSON öğeleri belirli tooODBC bağlantılı hizmeti için bir açıklama sağlar.

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| type |Merhaba type özelliği ayarlanmalıdır: **OnPremisesOdbc** |Evet |
| connectionString |Merhaba olmayan erişim kimlik bilgisi kısmı hello bağlantı dizesini ve isteğe bağlı bir kimlik bilgisi şifrelenir. Aşağıdaki bölümlerde hello örneklere bakın. |Evet |
| kimlik bilgisi |Merhaba erişim kimlik bilgisi bölümü sürücüye özgü özellik değer biçiminde belirtilen hello bağlantı dizesi. Örnek: "Uid =<user ID>; PWD =<password>; RefreshToken =<secret refresh token>; ". |Hayır |
| authenticationType |Kimlik doğrulama türü tooconnect toohello ODBC veri deposu kullanılır. Olası değerler şunlardır: anonim ve temel. |Evet |
| kullanıcı adı |Temel kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin. |Hayır |
| password |Merhaba username için belirtilen hello kullanıcı hesabı için parola belirtin. |Hayır |
| gatewayName |Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello ODBC veri deposu kullanmanız gerekir. |Evet |

### <a name="using-basic-authentication"></a>Temel kimlik doğrulaması kullanma

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```
### <a name="using-basic-authentication-with-encrypted-credentials"></a>Temel kimlik doğrulaması ile şifrelenmiş kimlik bilgileri kullanma
Merhaba kimlik hello kullanarak şifreleyebilirsiniz [yeni AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (Azure PowerShell 1.0 sürümü) cmdlet'ini veya [yeni AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 veya önceki bir sürümü hello Azure PowerShell).  

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a>Anonim kimlik doğrulamasını kullanma

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "mygateway"
        }
    }
}
```


## <a name="dataset-properties"></a>Veri kümesi özellikleri
Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi. Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.

Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar. Merhaba typeProperties bölüm türü veri kümesi için **RelationalTable** hello aşağıdaki özelliklere sahip (ODBC veri kümesi içerir)

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| tableName |Merhaba ODBC veri deposundaki Merhaba tablonun adı. |Evet |

## <a name="copy-activity-properties"></a>Etkinlik özellikleri Kopyala
Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi. Ad, açıklama, giriş ve çıkış tabloları ve ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir.

Hello kullanılabilen özellikleri **typeProperties** bölüm diğer yandan hello hello faaliyete, her etkinlik türü ile farklılık gösterir. Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.

Kopyalama etkinliğinde kaynak türü olduğunda **RelationalSource** (içeren ODBC), aşağıdaki özelliklere hello typeProperties bölümünde bulunur:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| sorgu |Merhaba özel sorgu tooread verileri kullanın. |SQL sorgu dizesi. Örneğin: seçin * from MyTable. |Evet |


## <a name="json-example-copy-data-from-odbc-data-store-tooazure-blob"></a>JSON örnek: ODBC veri verilerini depolamak tooAzure Blob
Bu örnek JSON tanımları sağlar, toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Bunu nasıl tooan Azure Blob Storage toocopy bir ODBC veri kaynağı gösterir. Ancak, veri belirtildiği hello havuzlarını, kopyalanan tooany olabilir [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.

Merhaba örnek data factory varlıklarını aşağıdaki hello sahiptir:

1. Bağlı hizmet türü [OnPremisesOdbc](#linked-service-properties).
2. Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Bir giriş [dataset](data-factory-create-datasets.md) türü [RelationalTable](#dataset-properties).
4. Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [RelationalSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Merhaba örnek verileri bir ODBC veri deposu tooa blob bir sorgu sonucunda her saat kopyalar. Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.

İlk adım olarak, hello veri yönetimi ağ geçidi ayarlayın. Merhaba yönergelerdir hello [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.

**ODBC bağlantılı hizmeti** kullandığı hello temel kimlik doğrulaması Bu örnek. Bkz: [ODBC bağlantılı hizmeti](#linked-service-properties) bölümü için farklı tür kimlik doğrulaması kullanabilirsiniz.

```json
{
    "name": "OnPremOdbcLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
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

**ODBC girdi veri kümesi**

Merhaba örnek bir ODBC veritabanında bir tablo "MyTable" oluşturdunuz ve zaman serisi veri için "timestampcolumn" adlı bir sütun içerdiği varsayar.

"Dış" ayarı: "true" bildirir hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremOdbcLinkedService",
        "typeProperties": {},
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

**Azure Blob dataset çıktı**

Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1). hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir. Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.

```json
{
    "name": "AzureBlobOdbcDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odbc/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


**ODBC kaynak (RelationalSource) ve Blob havuz (BlobSink) sahip işlem hattı kopyalama etkinliği**

Merhaba ardışık düzen içeren bir kopyalama etkinliği, yapılandırılmış toouse bu girdi ve çıktı veri kümeleri ve zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**RelationalSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**. Merhaba belirtilen hello SQL sorgusu **sorgu** özelliği saat toocopy geçmiş hello hello veri seçer.

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "OdbcDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOdbcDataSet"
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
                "name": "OdbcToBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-odbc"></a>Tür eşlemesi için ODBC
Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopyalama etkinliği gerçekleştiren kaynak türleri toosink türlerinden otomatik tür dönüşümleri iki aşamalı bir yaklaşım aşağıdaki hello ile:

1. Yerel kaynak türleri too.NET türünden Dönüştür
2. .NET türü toonative havuz türünden Dönüştür

ODBC veri depolarına verilerin taşınması, ODBC veri türleri eşlenen too.NET hello belirtildiği gibi türleridir [ODBC veri türü eşlemeleri](https://msdn.microsoft.com/library/cc668763.aspx) konu.

## <a name="map-source-toosink-columns"></a>Kaynak toosink sütunları eşleme
Kaynak veri kümesi toocolumns havuz kümesindeki eşleme sütunlarında hakkında toolearn bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>İlişkisel kaynaklardan yinelenebilir okuma
İlişkisel veri depoları veri kopyalama işlemi sırasında Yinelenebilirlik göz tooavoid tutmak istenmeyen sonuçları. Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz. Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz. Bir dilim iki yolla yeniden zaman, aynı veri hello emin toomake nasıl geçtiğinden bağımsız okuma gerekir dilim birçok kez çalıştırın. Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="ge-historian-store"></a>GE Historian deposu
Bir ODBC bağlantılı hizmet toolink oluşturduğunuz bir [GE Proficy Historian (şimdi GE Historian)](http://www.geautomation.com/products/proficy-historian) hello aşağıdaki örnekte gösterildiği gibi verileri depolamak tooan Azure veri fabrikası:

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of hello GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

Bir şirket içi veri yönetimi ağ geçidi yükleyin ve hello portalıyla hello ağ geçidini kaydedin. Şirket içi bilgisayarınıza yüklü hello ağ geçidi hello ODBC sürücüsü GE Historian tooconnect toohello GE Historian veri deposu kullanır. Merhaba ağ geçidi makinede zaten yüklü değilse, bu nedenle, hello sürücüsünü yükleyin. Bkz: [bağlantıyı etkinleştirme](#enabling-connectivity) ayrıntıları bölümü.

GE Historian depolamak bir veri fabrikası çözümde hello kullanmadan önce hello ağ geçidi toohello veri deposu hello sonraki bölümde yönergeleri kullanarak bağlandığını doğrulayın.

ODBC veri kullanımının hello makale okuma ayrıntılı bir genel bakış için hello başından bir kopyalama işleminde kaynak veri depoları olarak depolar.  

## <a name="troubleshoot-connectivity-issues"></a>Bağlantı sorunlarını giderme
tootroubleshoot bağlantı sorunlarını kullanmak hello **tanılama** sekmesinde **veri yönetimi ağ geçidi Yapılandırma Yöneticisi**.

1. Başlatma **veri yönetimi ağ geçidi Yapılandırma Yöneticisi**. İçin "C:\Program Files\Microsoft veri yönetimi Gateway\1.0\Shared\ConfigManager.exe" doğrudan (veya) arama ya da çalıştırabilirsiniz **ağ geçidi** toofind bağlantı çok**Microsoft Veri Yönetimi ağ geçidi** Görüntü aşağıdaki hello gösterildiği gibi uygulama.

    ![Arama ağ geçidi](./media/data-factory-odbc-connector/search-gateway.png)
2. Geçiş toohello **tanılama** sekmesi.

    ![Ağ geçidi tanılama](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. Select hello **türü** (bağlantılı hizmeti) verilerini depolar.
4. Belirtin **kimlik doğrulaması** ve girin **kimlik bilgileri** (veya) girin **bağlantı dizesi** , kullanılan tooconnect toohello veri deposudur.
5. Tıklatın **Bağlantıyı Sına** tootest hello bağlantı toohello veri deposu.

## <a name="performance-and-tuning"></a>Performans ve ayarlama
Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.
