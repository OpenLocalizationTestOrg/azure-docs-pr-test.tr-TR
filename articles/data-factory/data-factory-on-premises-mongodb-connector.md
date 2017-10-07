---
title: Data Factory kullanarak MongoDB aaaMove verilerden | Microsoft Docs
description: "Azure Data Factory kullanarak MongoDB toomove verileri nasıl veritabanı hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 10ca7d9a-7715-4446-bf59-2d2876584550
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 154e85712f27b978976c7499c43dde9429f124c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a>Azure Data Factory kullanarak MongoDB gelen veri taşıma
Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove veri bir şirket içi MongoDB veritabanından açıklanmaktadır. Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.

Bir şirket içi MongoDB veri deposu desteklenen tooany havuz veri deposundan verileri kopyalayabilirsiniz. Verileri bir listesi için desteklenen depoları hello kopyalama etkinliği tarafından havuzlarını hello görür [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo. Veri Fabrikası şu anda verileri MongoDB verilerinden tooother veri depolarına depolamak taşıma yalnızca, ancak diğer veri depoları tooan MongoDB deposundan veri taşıma değil destekler. 

## <a name="prerequisites"></a>Ön koşullar
Hello Azure Data Factory hizmeti toobe mümkün tooconnect tooyour şirket içi MongoDB veritabanı için aşağıdaki bileşenleri hello yüklemeniz gerekir:

- Desteklenmeyen MongoDB sürümler: 2.4, 2.6, 3.0 ve 3.2.
- Veri Yönetimi ağ geçidi ana hello veritabanının aynı makine hello veya hello veritabanıyla kaynakları için rekabete ayrı makine tooavoid. Veri Yönetimi ağ geçidi, şirket içi veri kaynakları toocloud Hizmetleri güvenli ve yönetilen bir şekilde birbirine bağlayan bir yazılımdır. Bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) makale veri yönetimi ağ geçidi hakkında ayrıntılı bilgi için. Bkz: [şirket içi toocloud veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale hello ağ geçidi veri ardışık düzen toomove veri ayarlama hakkında adım adım yönergeler için.

    Merhaba ağ geçidi yüklediğinizde, bir Microsoft MongoDB ODBC sürücüsü kullanılan tooconnect tooMongoDB otomatik olarak yükler.

    > [!NOTE]
    > Azure Iaas Vm'lerde barındırılan olsa bile toouse hello ağ geçidi tooconnect tooMongoDB gerekir. Bulutta barındırılan MongoDB tooconnect tooan örneğini çalışıyorsanız, hello ağ geçidi örneği hello Iaas VM yükleyebilirsiniz.

## <a name="getting-started"></a>Başlarken
Farklı araçlar/API'lerini kullanarak bir şirket içi MongoDB veri deposundan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.

Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**. Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.

Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**. Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için. 

Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin: 

1. Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.
2. Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi. 
3. Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile. 

Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur. Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.  Bir şirket içi MongoDB veri deposundaki kullanılan toocopy verileri Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: MongoDB tooAzure Blob veri kopyalama](#json-example-copy-data-from-mongodb-to-azure-blob) bu makalenin. 

Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooMongoDB kaynağı JSON özellikleri hakkında ayrıntılı bilgi sağlar:

## <a name="linked-service-properties"></a>Bağlantılı hizmet özellikleri
Merhaba aşağıdaki tabloda JSON öğeleri belirli açıklamasını çok sağlar**OnPremisesMongoDB** bağlı hizmeti.

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| type |Merhaba type özelliği ayarlanmalıdır: **OnPremisesMongoDb** |Evet |
| sunucu |IP adresi veya ana bilgisayar hello MongoDB sunucunun adıdır. |Evet |
| port |MongoDB sunucusuna hello TCP bağlantı noktası toolisten istemci bağlantıları için kullanır. |İsteğe bağlı, varsayılan değer: 27017 |
| authenticationType |Basic veya Anonymous. |Evet |
| kullanıcı adı |Kullanıcı hesabı tooaccess MongoDB. |Evet (Temel kimlik doğrulaması kullanılıyorsa). |
| password |Merhaba kullanıcının parolası. |Evet (Temel kimlik doğrulaması kullanılıyorsa). |
| authSource |Kimlik doğrulaması için kimlik bilgilerinizi toouse toocheck istediğiniz hello MongoDB veritabanı adı. |(Temel kimlik doğrulaması kullanılıyorsa) isteğe bağlı. Varsayılan: Merhaba yönetici hesabı ve databaseName özelliği kullanılarak belirtilen hello veritabanı kullanır. |
| databaseName |Tooaccess istediğiniz hello MongoDB veritabanı adı. |Evet |
| gatewayName |Merhaba veri deposu erişen hello ağ geçidi adı. |Evet |
| encryptedCredential |Ağ Geçidi tarafından şifrelenmiş kimlik bilgileri. |İsteğe bağlı |

## <a name="dataset-properties"></a>Veri kümesi özellikleri
Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi. Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.

Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar. Merhaba typeProperties bölüm türü veri kümesi için **MongoDbCollection** hello aşağıdaki özelliklere sahiptir:

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| collectionName |MongoDB veritabanı hello koleksiyonunda adı. |Evet |

## <a name="copy-activity-properties"></a>Etkinlik özellikleri Kopyala
Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi. Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.

Hello kullanılabilen özellikleri **typeProperties** bölüm diğer yandan hello hello faaliyete, her etkinlik türü ile farklılık gösterir. Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.

Merhaba kaynak türü olduğunda **MongoDbSource** aşağıdaki özelliklere hello typeProperties bölümünde bulunur:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| sorgu |Merhaba özel sorgu tooread verileri kullanın. |SQL-92 sorgu dizesi. Örneğin: seçin * from MyTable. |Hayır (varsa **collectionName** , **dataset** belirtilir) |



## <a name="json-example-copy-data-from-mongodb-tooazure-blob"></a>JSON örnek: MongoDB tooAzure Blob veri kopyalama
Bu örnek örnek JSON tanımları sağlar, toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Bunu gösterir nasıl bir şirket içi MongoDB tooan Azure Blob Storage toocopy verileri. Ancak, veri belirtildiği hello havuzlarını, kopyalanan tooany olabilir [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.

Merhaba örnek data factory varlıklarını aşağıdaki hello sahiptir:

1. Bağlı hizmet türü [OnPremisesMongoDb](#linked-service-properties).
2. Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Bir giriş [dataset](data-factory-create-datasets.md) türü [MongoDbCollection](#dataset-properties).
4. Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [MongoDbSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Merhaba örnek veri MongoDB veritabanı tooa blob bir sorgu sonucunda her saat kopyalar. Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.

Merhaba veri yönetimi ağ geçidi hello hello yönergeleri göredir ilk adım olarak, Kurulum [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) makalesi.

**MongoDB bağlantılı hizmeti:**

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",  
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
        }
    }
}
```

**Azure Storage bağlı hizmeti:**

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

**MongoDB girdi veri kümesi:** "dış" ayarı: "true" bildirir hello Data Factory hizmetinin bu hello tablosu dış toohello veri fabrikası ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.

```json
{
     "name":  "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"    
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

**Azure Blob dataset çıktı:**

Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1). hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir. Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/frommongodb/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**MongoDB kaynak ve Blob havuz ile ardışık düzeninde etkinlik kopyalayın:**

Merhaba ardışık düzen giriş ve çıkış veri kümeleri yukarıda yapılandırılan toouse hello ve zamanlanmış toorun her saatte birdir kopyalama etkinliği içerir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**MongoDbSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**. Merhaba belirtilen hello SQL sorgusu **sorgu** özelliği saat toocopy geçmiş hello hello veri seçer.

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "MongoDbSource",
                        "query": "$$Text.Format('select * from  MyTable where LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "MongoDbInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
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
                "name": "MongoDBToAzureBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```


## <a name="schema-by-data-factory"></a>Şema tarafından veri fabrikası
Azure Data Factory hizmeti hello koleksiyonunda hello son 100 belgeleri kullanarak MongoDB koleksiyonundan şema oluşturur. Bu 100 belgeleri tam şema içermiyorsa, bazı sütunları hello kopyalama işlemi sırasında yoksayılabilir.

## <a name="type-mapping-for-mongodb"></a>MongoDB için tür eşlemesi
Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopyalama etkinliği gerçekleştiren kaynak türleri toosink türlerinden otomatik tür dönüşümleri 2 adımlı yaklaşımı izleyerek hello ile:

1. Yerel kaynak türleri too.NET türünden Dönüştür
2. .NET türü toonative havuz türünden Dönüştür

Aşağıdaki veri tooMongoDB hello taşırken eşlemeleri MongoDB türleri too.NET türlerinden kullanılır.

| MongoDB türü | .NET framework türü |
| --- | --- |
| İkili |Byte] |
| Boole değeri |Boole değeri |
| Tarih |Tarih saat |
| NumberDouble |Çift |
| NumberInt |Int32 |
| NumberLong |Int64 |
| ObjectID |Dize |
| Dize |Dize |
| UUID |GUID |
| Nesne |Renormalized içine iç içe geçmiş ayırıcı olarak "_" sütunlarla düzleştirme |

> [!NOTE]
> Sanal tablolar kullanarak dizileri desteği hakkında toolearn başvurmak çok[sanal tablolar kullanarak karmaşık türleri için destek](#support-for-complex-types-using-virtual-tables) bölümüne bakın.

Şu anda, şu MongoDB veri türlerini hello desteklenmiyor: DBPointer, JavaScript, en fazla/dak anahtar, normal ifade, simge, zaman damgası, tanımlanmamış

## <a name="support-for-complex-types-using-virtual-tables"></a>Sanal tablolar kullanarak karmaşık türleri için destek
Azure Data Factory bir yerleşik ODBC sürücüsü tooconnect tooand kopyalama veritabanınızdaki verileri MongoDB kullanır. Merhaba belgeler arasında farklı türleriyle dizileri veya nesneleri gibi karmaşık türler için hello sürücü veri karşılık gelen sanal tablolara yeniden normalleştirir. Özellikle, bir tablo bu tür sütunlar içeriyorsa, hello sürücü sanal tablolar aşağıdaki hello oluşturur:

* A **temel tablo**, içeren hello hello gerçek tablo hello karmaşık tür sütunları dışında aynı verileri. Merhaba temel tablo aynı adı hello temsil ettiği hello gerçek tablo olarak kullanır.
* A **sanal tablo** her karmaşık tür sütun için hangi genişletir hello iç içe geçmiş verileri. Merhaba sanal tablolar hello gerçek tablonun hello adı, bir ayırıcı "_" ve hello hello dizi veya nesne adını kullanarak adlandırılır.

Sanal tablolar hello gerçek tablosunda toohello veri bakın, etkinleştirme hello sürücü tooaccess Normalleştirilmemiş veri hello. Ayrıntılar aşağıda örnek bölümüne bakın. Sorgulamak ve hello sanal tabloları birleştirme MongoDB dizi hello içeriğe erişebilir.

Merhaba kullanabilirsiniz [Kopyalama Sihirbazı'nı](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively görünümü hello hello sanal tablolar dahil olmak üzere MongoDB veritabanı tablolarında listesi ve önizleme içindeki hello verileri. Ayrıca, hello Kopyalama Sihirbazı, bir sorgu oluşturun ve toosee hello sonucu doğrulayın.

### <a name="example"></a>Örnek
Örneğin, aşağıda "ExampleTable" her hücresinde – faturaları ve bir dizi skaler türler – derecelendirmeleri bir sütunla nesnelerinin bir dizisi ile bir sütunu bulunan bir MongoDB tablodur.

| _ıd | Müşteri adı | Faturalar | Hizmet düzeyi | Derecelendirme |
| --- | --- | --- | --- | --- |
| 1111 |ABC |[{invoice_id: "123" öğesi: "toaster", fiyat: "456", indirim: "0.2"}, {invoice_id: "124" öğesi: "fırın", fiyat: "1235" indirim: "0.2"}] |Gümüş |[5,6] |
| 2222 |XYZ |[{invoice_id: "135" öğesi: "fridge", fiyat: "12543", indirim: "0,0"}] |Altın |[1,2] |

Merhaba sürücüsü birden çok sanal tablolar toorepresent bu tek tablo oluşturur. Merhaba ilk sanal hello temel tablo "aşağıda gösterilen ExampleTable" adlı bir tablodur. Hello temel tablo hello orijinal tablonun tüm hello verileri içerir, ancak hello diziler hello verilerden çıkarıldı ve hello sanal tablolarda genişletilir.

| _ıd | Müşteri adı | Hizmet düzeyi |
| --- | --- | --- |
| 1111 |ABC |Gümüş |
| 2222 |XYZ |Altın |

Merhaba aşağıdaki tablolarda hello hello özgün diziler hello örnekte temsil eden sanal tablolar gösterilmektedir. Bu tablolar hello aşağıdakileri içerir:

* Bir başvuru geri toohello özgün birincil anahtar sütunu karşılık gelen toohello satır hello özgün dizinin (aracılığıyla hello _ıd sütun)
* Merhaba konumunu hello özgün dizi hello verilerini bir göstergesi
* Merhaba veri hello dizi her öğe için genişletilmiş

Tablo "ExampleTable_Invoices":

| _ıd | ExampleTable_Invoices_dim1_idx | invoice_id | Öğesi | price | İndirim |
| --- | --- | --- | --- | --- | --- |
| 1111 |0 |123 |toaster |456 |0.2 |
| 1111 |1 |124 |Fırın |1235 |0.2 |
| 2222 |0 |135 |fridge |12543 |0.0 |

Tablo "ExampleTable_Ratings":

| _ıd | ExampleTable_Ratings_dim1_idx | ExampleTable_Ratings |
| --- | --- | --- |
| 1111 |0 |5 |
| 1111 |1 |6 |
| 2222 |0 |1 |
| 2222 |1 |2 |

## <a name="map-source-toosink-columns"></a>Kaynak toosink sütunları eşleme
Kaynak veri kümesi toocolumns havuz kümesindeki eşleme sütunlarında hakkında toolearn bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>İlişkisel kaynaklardan yinelenebilir okuma
İlişkisel veri depoları veri kopyalama işlemi sırasında Yinelenebilirlik göz tooavoid tutmak istenmeyen sonuçları. Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz. Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz. Bir dilim iki yolla yeniden zaman, aynı veri hello emin toomake nasıl geçtiğinden bağımsız okuma gerekir dilim birçok kez çalıştırın. Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Performans ve ayarlama
Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.

## <a name="next-steps"></a>Sonraki Adımlar
Bkz: [şirket içi ve bulut arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) veri ardışık oluşturma verileri şirket verilerinden depolamak tooan Azure veri deposu taşır için adım adım yönergeler için makalesi.
