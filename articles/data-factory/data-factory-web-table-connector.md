---
title: Azure Data Factory kullanarak Web tablodan aaaMove veri | Microsoft Docs
description: "Azure Data Factory kullanarak bir Web tablosunda toomove verileri nasıl sayfa hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f54a26a4-baa4-4255-9791-5a8f935898e2
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e52216305583ebbe71ed896522f361bb22f01278
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a>Azure Data Factory kullanarak bir Web tablo kaynağından veri taşıma
Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove verileri bir Web sayfası tooa tabloda havuz veri deposu desteklenen özetlenmektedir. Bu makale üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale listesiyle kopyalama etkinliği ve hello kaynakları/havuzlarını desteklenen veri depoları veri taşıma genel bir bakış sunar.

Veri Fabrikası şu anda yalnızca bir Web tablo tooother verilerden veri taşımayı depolar, ancak verileri diğer veriler taşıma değil tooa Web tablosu hedef depolar destekler.

> [!IMPORTANT]
> Bu Web bağlayıcı şu anda bir HTML sayfasından yalnızca ayıklanan tablo içeriği destekler. bir HTTP/s uç noktası tooretrieve verileri kullan [HTTP Bağlayıcısı](data-factory-http-connector.md) yerine.

## <a name="getting-started"></a>Başlarken
Farklı araçlar/API'lerini kullanarak bir şirket içi Cassandra veri deposundan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun. 

- Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**. Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz. 
- Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**. Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için. 

Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:

1. Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.
2. Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi. 
3. Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile. 

Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur. Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.  Bir web tablodan kullanılan toocopy verileri Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: Web tablo tooAzure Blob veri kopyalama](#json-example-copy-data-from-web-table-to-azure-blob) bu makalenin. 

Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooa Web tablosunun JSON özellikleri hakkında ayrıntılı bilgi sağlar:

## <a name="linked-service-properties"></a>Bağlantılı hizmet özellikleri
Aşağıdaki tablonun hello JSON öğeleri belirli tooWeb bağlantılı hizmeti için bir açıklama sağlar.

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| type |Merhaba type özelliği ayarlanmalıdır: **Web** |Evet |
| Url |URL toohello Web kaynağı |Evet |
| authenticationType |Anonim. |Evet |

### <a name="using-anonymous-authentication"></a>Anonim kimlik doğrulamasını kullanma

```json
{
    "name": "web",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

## <a name="dataset-properties"></a>Veri kümesi özellikleri
Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi. Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.

Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar. Merhaba typeProperties bölüm türü veri kümesi için **WebTable** hello aşağıdaki özelliklere sahip

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| type |Merhaba veri kümesi türü. çok ayarlanmalıdır**WebTable** |Evet |
| Yol |Merhaba tablo içeren bir göreli URL toohello kaynağıdır. |Hayır. Yol belirtilmediğinde hello bağlantılı hizmet tanımında belirtilen yalnızca hello URL'si kullanılır. |
| Dizin |hello kaynak hello tabloda başlangıç dizini. Bkz: [bir HTML sayfasında tablosunun Get dizini](#get-index-of-a-table-in-an-html-page) HTML sayfası bir tablodaki adımları toogetting dizini için bölüm. |Evet |

**Örnek:**

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
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

Oysa hello typeProperties bölümünde hello etkinlik özellikleri her etkinlik türü ile farklılık gösterir. Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.

Şu anda kopyalama etkinliği hello kaynağında olduğunda türü **WebSource**, hiçbir ek özellikler desteklenir.


## <a name="json-example-copy-data-from-web-table-tooazure-blob"></a>JSON örnek: Web tablo tooAzure Blob veri kopyalama
Merhaba, aşağıdaki örnek gösterilmektedir:

1. Bağlı hizmet türü [Web](#linked-service-properties).
2. Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Bir giriş [dataset](data-factory-create-datasets.md) türü [WebTable](#dataset-properties).
4. Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [WebSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Merhaba örnek verileri saatte bir Web tablo tooan Azure blob kopyalar. Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.

Aşağıdaki örnek hello nasıl toocopy verileri bir Web tablo tooan Azure blob'tan gösterir. İçinde belirtilen hello hello tooany havuzlarını doğrudan veri ancak kopyalanabilir [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) hello kopya etkinliği Azure Data Factory kullanarak makale.

**Web hizmeti bağlı** kullanan Web hello Bu örnek anonim kimlik doğrulaması ile bağlı. Bkz: [Web bağlantılı hizmeti](#linked-service-properties) bölümü için farklı tür kimlik doğrulaması kullanabilirsiniz.

```json
{
    "name": "WebLinkedService",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
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

**WebTable girdi veri kümesi** ayarı **dış** çok**true** hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello bir etkinlik tarafından üretilen değil bildirir Veri Fabrikası.

> [!NOTE]
> Bkz: [bir HTML sayfasında tablosunun Get dizini](#get-index-of-a-table-in-an-html-page) HTML sayfası bir tablodaki adımları toogetting dizini için bölüm.  
>
>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```


**Azure Blob dataset çıktı**

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



**Kopyalama etkinliği ile kanalı**

Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**WebSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**.

Bkz: [WebSource türü özellikleri](#copy-activity-type-properties) hello WebSource hello tarafından desteklenen özelliklerin listesi için.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "WebTableToAzureBlob",
        "description": "Copy from a Web table tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "WebTableInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "WebSource"
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

## <a name="get-index-of-a-table-in-an-html-page"></a>Bir HTML sayfasında bir tablonun dizini alma
1. Başlatma **Excel 2016** ve toohello anahtar **veri** sekmesi.  
2. Tıklatın **yeni sorgu** hello araç çubuğunda, çok noktası**diğer kaynaklardan** tıklatıp **Web'den**.

    ![Power Query menüsü](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. Merhaba, **Web'den** iletişim kutusunda, girin **URL** bağlantılı hizmeti JSON içinde kullanırsınız (örneğin: https://en.wikipedia.org/wiki/) yolu belirtin hello veri kümesi için birlikte (örneğin: AFI % 27s_100_Years... 100_Movies) tıklatıp **Tamam**.

    ![Web iletişim kutusundan](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    Bu örnekte kullanılan URL: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies
4. Görürseniz **erişim Web içeriği** iletişim kutusu, select hello sağ **URL**, **kimlik doğrulaması**, tıklatıp **Bağlan**.

   ![Web içerik iletişim kutusuna erişin](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. Tıklatın bir **tablo** öğesi hello ağaç görünümü toosee içerik hello tablosundan ve ardından **Düzenle** hello altındaki düğmesi.  

   ![Gezgin iletişim](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. Merhaba, **sorgu Düzenleyicisi'ni** penceresinde tıklatın **Gelişmiş Düzenleyici** hello araç çubuğunda.

    ![Gelişmiş Düzenleyici düğmesi](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. Sayı Hello Gelişmiş Düzenleyicisi iletişim kutusunda hello sonraki çok "Kaynak" Merhaba dizinidir.

    ![Düzenleyicisi - Gelişmiş dizin](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

Excel 2013 kullanıyorsanız, [Excel için Microsoft Power Query](https://www.microsoft.com/download/details.aspx?id=39379) tooget başlangıç dizini. Bkz: [Bağlan tooa web sayfası](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) Ayrıntılar için makale. Merhaba adımlardır kullanıyorsanız benzer [Masaüstü için Microsoft Power BI](https://powerbi.microsoft.com/desktop/).

> [!NOTE]
> Kaynak veri kümesi toocolumns havuz kümesinden toomap sütunlarından bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Performans ve ayarlama
Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.
