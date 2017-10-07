---
title: Data Factory kullanarak Cassandra aaaMove verilerden | Microsoft Docs
description: "Azure Data Factory kullanarak bir şirket içi Cassandra toomove verileri nasıl veritabanı hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 085cc312-42ca-4f43-aa35-535b35a102d5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 0e265d3a8439d0a2cb2a5c32e5ea8348a1617621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a>Azure Data Factory kullanarak bir şirket içi Cassandra veritabanından veri taşıma
Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove veri bir şirket içi Cassandra veritabanından açıklanmaktadır. Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.

Bir şirket içi Cassandra veri deposu desteklenen tooany havuz veri deposundan verileri kopyalayabilirsiniz. Verileri bir listesi için desteklenen depoları hello kopyalama etkinliği tarafından havuzlarını hello görür [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo. Veri Fabrikası şu anda verileri Cassandra verilerinden tooother veri depolarına depolamak taşıma yalnızca, ancak diğer veri depoları tooa Cassandra veri deposundan veri taşıma değil destekler. 

## <a name="supported-versions"></a>Desteklenen sürümler
Merhaba Cassandra bağlayıcı Cassandra sürümleri aşağıdaki hello destekler: 2.X.

## <a name="prerequisites"></a>Ön koşullar
Hello Azure Data Factory hizmeti toobe mümkün tooconnect tooyour şirket içi Cassandra veritabanı için veri yönetimi ağ geçidi yüklemeniz gerekir hello üzerinde aynı ana bilgisayar hello veritabanının makine veya hello kaynaklarla için rekabet ayrı makine tooavoid Veritabanı. Veri Yönetimi ağ geçidi, şirket içi veri kaynakları toocloud Hizmetleri güvenli ve yönetilen bir şekilde birbirine bağlayan bir bileşenidir. Bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) makale veri yönetimi ağ geçidi hakkında ayrıntılı bilgi için. Bkz: [şirket içi toocloud veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale hello ağ geçidi veri ardışık düzen toomove veri ayarlama hakkında adım adım yönergeler için.

Merhaba veritabanı hello bulutta, örneğin, bir Azure Iaas sanal bile barındırılıyorsa hello ağ geçidi tooconnect tooa Cassandra veritabanı kullanmanız gerekir. Y hello ağ geçidine sahip ana hello veritabanının aynı VM hello veya hello ağ geçidi olarak uzunluğunda ayrı bir VM'de toohello veritabanı bağlanabilirsiniz.  

Merhaba ağ geçidi yüklediğinizde, bir Microsoft Cassandra ODBC sürücüsü kullanılan tooconnect tooCassandra veritabanı otomatik olarak yükler. Bu nedenle, gerekmeyen toomanually hello Cassandra veritabanından veri kopyalama işlemi sırasında bu herhangi bir sürücüsü hello ağ geçidi makineye yükleyin. 

> [!NOTE]
> Bkz: [ağ geçidi sorunlarını giderme](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) ilgili sorunlar bağlantı/ağ geçidi sorun giderme ipuçları için.

## <a name="getting-started"></a>Başlarken
Farklı araçlar/API'lerini kullanarak bir şirket içi Cassandra veri deposundan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun. 

- Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**. Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz. 
- Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**. Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için. 

Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:

1. Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.
2. Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi. 
3. Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile. 

Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur. Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.  Bir şirket içi Cassandra veri deposundaki kullanılan toocopy verileri Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: Cassandra tooAzure Blob veri kopyalama](#json-example-copy-data-from-cassandra-to-azure-blob) bu makalenin. 

Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooa Cassandra veri deposu olan JSON özellikleri hakkında ayrıntılı bilgi sağlar:

## <a name="linked-service-properties"></a>Bağlantılı hizmet özellikleri
Aşağıdaki tablonun hello JSON öğeleri belirli tooCassandra bağlantılı hizmeti için bir açıklama sağlar.

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| type |Merhaba type özelliği ayarlanmalıdır: **OnPremisesCassandra** |Evet |
| ana bilgisayar |Bir veya daha fazla IP adresleri veya ana bilgisayar adlarını Cassandra sunucuları.<br/><br/>IP adresi veya ana bilgisayar adları tooconnect tooall sunucuları virgülle ayrılmış listesini eşzamanlı olarak belirtin. |Evet |
| port |Merhaba Cassandra sunucu hello TCP bağlantı noktası toolisten istemci bağlantıları için kullanır. |Hayır, varsayılan değer: 9042 |
| authenticationType |Basic veya Anonymous |Evet |
| kullanıcı adı |Merhaba kullanıcı hesabının kullanıcı adını belirtin. |Evet, authenticationType tooBasic ayarlarsanız. |
| password |Merhaba kullanıcı hesabı için parola belirtin. |Evet, authenticationType tooBasic ayarlarsanız. |
| gatewayName |kullanılan tooconnect toohello şirket içi Cassandra veritabanı hello ağ geçidi Hello adı. |Evet |
| encryptedCredential |Merhaba ağ geçidi tarafından şifrelenmiş kimlik bilgileri. |Hayır |

## <a name="dataset-properties"></a>Veri kümesi özellikleri
Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi. Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.

Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar. Merhaba typeProperties bölüm türü veri kümesi için **CassandraTable** hello aşağıdaki özelliklere sahip

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| keyspace |Merhaba keyspace veya Cassandra veritabanındaki şema adı. |Evet (varsa **sorgu** için **CassandraSource** tanımlı değil). |
| tableName |Cassandra veritabanındaki Merhaba tablonun adı. |Evet (varsa **sorgu** için **CassandraSource** tanımlı değil). |

## <a name="copy-activity-properties"></a>Etkinlik özellikleri Kopyala
Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi. Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.

Oysa hello typeProperties bölümünde hello etkinlik özellikleri her etkinlik türü ile farklılık gösterir. Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.

Kaynak türü olduğunda **CassandraSource**, aşağıdaki özelliklere hello typeProperties bölümünde bulunur:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| sorgu |Merhaba özel sorgu tooread verileri kullanın. |SQL-92 sorgusu veya CQL sorgusu. Bkz: [CQL başvuru](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html). <br/><br/>SQL sorgusu kullanırken belirtin **keyspace name.table adı** tooquery istediğiniz toorepresent hello tablo. |Hayır (tableName ve veri kümesi üzerinde keyspace tanımlanmışsa). |
| consistencyLevel |kaç tane çoğaltmaları veri toohello istemci uygulaması döndürmeden önce tooa Okuma isteği yanıtlamalısınız Hello tutarlılık düzeyi belirtir. İstek veri toosatisfy hello okumak için Cassandra denetimleri çoğaltmaları belirtilen sayıda hello. |BİR, İKİ, ÜÇ, ÇEKİRDEK, TÜMÜ, LOCAL_QUORUM EACH_QUORUM, LOCAL_ONE. Bkz: [veri tutarlılığını yapılandırma](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) Ayrıntılar için. |Hayır. Varsayılan değer biridir. |

## <a name="json-example-copy-data-from-cassandra-tooazure-blob"></a>JSON örnek: Cassandra tooAzure Blob veri kopyalama
Bu örnek örnek JSON tanımları sağlar, toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Bu, nasıl bir şirket içi Cassandra toocopy verileri Azure Blob Storage tooan veritabanı gösterir. Ancak, veri belirtildiği hello havuzlarını, kopyalanan tooany olabilir [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.

> [!IMPORTANT]
> Bu örnek, JSON parçacıklarını sağlar. Merhaba veri fabrikası oluşturma için yönergeler içermez. Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale adım adım yönergeler için.

Merhaba örnek data factory varlıklarını aşağıdaki hello sahiptir:

* Bağlı hizmet türü [OnPremisesCassandra](#linked-service-properties).
* Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Bir giriş [dataset](data-factory-create-datasets.md) türü [CassandraTable](#dataset-properties).
* Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [CassandraSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

**Bağlantılı Cassandra hizmeti:**

Bu örnek hello kullanır **Cassandra** bağlı hizmeti. Bkz: [Cassandra bağlantılı hizmeti](#linked-service-properties) bu bağlantılı hizmet tarafından desteklenen hello özellikler bölümü.  

```json
{
    "name": "CassandraLinkedService",
    "properties":
    {
        "type": "OnPremisesCassandra",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "host": "mycassandraserver",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "mygateway"
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

**Cassandra girdi veri kümesi:**

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "mykeyspace"
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

**Azure Blob dataset çıktı:**

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
            "folderPath": "adfgetstarted/fromcassandra"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Etkinlik Cassandra kaynak ve Blob havuz sahip işlem hattı kopyalayın:**

Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir. JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**CassandraSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**.

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
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "CassandraInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"

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

### <a name="type-mapping-for-cassandra"></a>Tür eşlemesi için Cassandra
| Cassandra türü | .NET türü temelinde |
| --- | --- |
| ASCII |Dize |
| BIGINT |Int64 |
| BLOB |Byte] |
| BOOLE DEĞERİ |Boole değeri |
| ONDALIK |Ondalık |
| ÇİFT |Çift |
| KAYAN NOKTA |Tek |
| INET |Dize |
| INT |Int32 |
| METİN |Dize |
| ZAMAN DAMGASI |Tarih saat |
| TIMEUUID |GUID |
| UUID |GUID |
| VARCHAR |Dize |
| VARINT |Ondalık |

> [!NOTE]
> Koleksiyon için türlerini (harita, kümesi, liste, vb.), çok başvurun[iş Cassandra koleksiyon türlerini sanal tablosunu kullanarak](#work-with-collections-using-virtual-table) bölümü.
>
> Kullanıcı tanımlı türler desteklenmez.
>
> İkili sütun ve dize sütunu uzunluklarını Hello uzunluğu 4000'den büyük olamaz.
>
>

## <a name="work-with-collections-using-virtual-table"></a>Sanal tablosunu kullanarak koleksiyonları ile çalışma
Azure Data Factory yerleşik ODBC sürücüsü tooconnect tooand kopya veri Cassandra veritabanınızdan kullanır. Harita, kümesi ve listesi dahil olmak üzere koleksiyon türü için karşılık gelen sanal tablolara hello veri hello sürücü renormalizes. Bir tablo tüm koleksiyon sütunları içeriyorsa, özellikle hello sürücü sanal tablolar aşağıdaki hello oluşturur:

* A **temel tablo**, içeren hello hello gerçek tablo hello koleksiyonu sütunları dışında aynı verileri. Merhaba temel tablo aynı adı hello temsil ettiği hello gerçek tablo olarak kullanır.
* A **sanal tablo** her koleksiyon sütun için hangi genişletir hello iç içe geçmiş verileri. koleksiyonları temsil eden hello sanal tablolar Merhaba tablonun adı hello gerçek, ayırıcı kullanılarak adlandırılması "*vt*" ve hello sütunun hello adı.

Sanal tablolar hello gerçek tablosunda toohello veri bakın, etkinleştirme hello sürücü tooaccess Normalleştirilmemiş veri hello. Ayrıntılar için örnek bölümüne bakın. Sorgulamak ve hello sanal tabloları birleştirme Cassandra koleksiyonların hello içeriğe erişebilir.

Merhaba kullanabilirsiniz [Kopyalama Sihirbazı'nı](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively görünümü hello hello sanal tablolar dahil olmak üzere Cassandra veritabanındaki tabloların listesi ve önizleme içindeki hello verileri. Ayrıca, hello Kopyalama Sihirbazı, bir sorgu oluşturun ve toosee hello sonucu doğrulayın.

### <a name="example"></a>Örnek
Örneğin, hello aşağıdaki "ExampleTable" "pk_int", değer adlı bir text sütunu, bir liste sütunu, sütun eşleme ve ("StringSet" olarak adlandırılır) bir sütunu Ayarla adlı bir tamsayı birincil anahtar sütunu içeren bir Cassandra veritabanı tablosu verilmiştir.

| pk_int | Değer | Liste | eşleme | StringSet |
| --- | --- | --- | --- | --- |
| 1 |"örnek değeri 1" |["1", "2", "3"] |{"S1": "a", "S2": "b"} |{"A", "B", "C"} |
| 3 |"örnek value 3" |["100", "101", "102", "105"] |{"S1": "t"} |{"A", "E"} |

Merhaba sürücüsü birden çok sanal tablolar toorepresent bu tek tablo oluşturur. Merhaba hello Sanal tablolardaki yabancı anahtar sütunları hello gerçek tablosundaki birincil anahtar sütunlarının hello başvuru ve hangi gerçek belirtmek tablo hello sanal tablosuna satır karşılık gelir.

Aşağıdaki tablonun hello "ExampleTable" adlı hello temel tabloda gösterilen Hello ilk sanal tablosu değil. Merhaba temel tablo içeren hello hello özgün veritabanı tablosu bu tablodan atlanmış ve diğer sanal tablolarda genişletilmiş hello koleksiyonları dışında aynı verileri.

| pk_int | Değer |
| --- | --- |
| 1 |"örnek değeri 1" |
| 3 |"örnek value 3" |

Merhaba aşağıdaki tablolarda hello listesi, eşleme ve StringSet sütunları hello verilerden renormalize hello sanal tablolar gösterilmektedir. yalnızca "_index" veya "_anahtar" ile biten adlarını Hello sütunlarla hello asıl liste veya eşlemesi içinde hello veri hello konumunu belirtin. yalnızca "_value" ile biten adlarını Hello sütunlarla hello koleksiyonundan hello genişletilmiş verileri içerir.

#### <a name="table-exampletablevtlist"></a>Tablo "ExampleTable_vt_List":
| pk_int | List_index | List_value |
| --- | --- | --- |
| 1 |0 |1 |
| 1 |1 |2 |
| 1 |2 |3 |
| 3 |0 |100 |
| 3 |1 |101 |
| 3 |2 |102 |
| 3 |3 |103 |

#### <a name="table-exampletablevtmap"></a>Tablo "ExampleTable_vt_Map":
| pk_int | Map_key | Map_value |
| --- | --- | --- |
| 1 |S1 |A |
| 1 |S2 |B |
| 3 |S1 |T |

#### <a name="table-exampletablevtstringset"></a>Tablo "ExampleTable_vt_StringSet":
| pk_int | StringSet_value |
| --- | --- |
| 1 |A |
| 1 |B |
| 1 |C |
| 3 |A |
| 3 |E |

## <a name="map-source-toosink-columns"></a>Kaynak toosink sütunları eşleme
Kaynak veri kümesi toocolumns havuz kümesindeki eşleme sütunlarında hakkında toolearn bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>İlişkisel kaynaklardan yinelenebilir okuma
İlişkisel veri depoları veri kopyalama işlemi sırasında Yinelenebilirlik göz tooavoid tutmak istenmeyen sonuçları. Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz. Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz. Bir dilim iki yolla yeniden zaman, aynı veri hello emin toomake nasıl geçtiğinden bağımsız okuma gerekir dilim birçok kez çalıştırın. Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Performans ve ayarlama
Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.
