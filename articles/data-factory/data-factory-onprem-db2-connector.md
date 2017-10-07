---
title: Azure Data Factory kullanarak aaaMove verilerden DB2 | Microsoft Docs
description: "Azure Data Factory kopyalama etkinliği kullanarak bir şirket içi DB2 toomove verileri nasıl veritabanı öğrenin"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c1644e17-4560-46bb-bf3c-b923126671f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 696ac059be644cb3901c37d2fc746e0682c65a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a>Azure Data Factory kopyalama etkinliği kullanarak DB2 taşıma verileri
Bu makalede Azure Data Factory toocopy veri bir şirket içi DB2 veritabanına tooa veri deposundaki kopyalama etkinliği nasıl kullanabileceğinizi açıklar. Merhaba, desteklenen bir havuz olarak listelenen veri tooany deposuna kopyalayabilirsiniz [Data Factory veri taşıma etkinlikleri](data-factory-data-movement-activities.md#supported-data-stores-and-formats) makalesi. Bu konu, kopyalama etkinliği kullanarak veri taşıma genel bir bakış sunar ve desteklenen hello veri deposu birleşimlerini listeler hello Data Factory makale üzerinde oluşturur. 

Veri Fabrikası şu anda bir DB2 veritabanına tooa yalnızca taşıma verilerden destekler [desteklenen havuz veri deposu](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Verileri diğer veriler taşıma tooa DB2 veritabanına desteklenmiyor depolar.

## <a name="prerequisites"></a>Ön koşullar
Veri Fabrikası hello kullanarak bağlanan tooan şirket içi DB2 veritabanına destekler [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md). Adım adım yönergeler tooset hello ağ geçidi verileri için verilerinizi toomove kanal bkz hello [şirket içi toocloud veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.

Merhaba DB2 Azure Iaas sanal üzerinde barındırılan olsa bile bir ağ geçidi gereklidir. Merhaba ağ geçidi üzerinde hello yükleyebilirsiniz hello veri deposu olarak aynı Iaas VM. Hello ağ geçidi toohello veritabanı bağlanırsanız, farklı bir VM hello ağ geçidi yükleyebilirsiniz.

Yerleşik bir DB2 sürücü Hello veri yönetimi ağ geçidi sağlar, sizin için toomanually sürücü toocopy veri DB2'den yüklemeniz gerekir.

> [!NOTE]
> Merhaba bağlantı ve ağ geçidi sorunları giderme hakkında ipuçları için bkz: [ağ geçidi sorunlarını giderme](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) makalesi.


## <a name="supported-versions"></a>Desteklenen sürümler
Merhaba veri fabrikası DB2 Bağlayıcısı IBM DB2 platformları ve dağıtılmış ilişkisel veritabanı mimarisi (DRDA) SQL Erişim Yöneticisi sürüm 9, 10 ve 11 sürümleriyle aşağıdaki hello destekler:

* IBM DB2 z/OS sürümü 11.1 için
* IBM DB2 z/OS sürümü 10.1 için
* IBM DB2'i (AS400) sürüm 7.2 için
* IBM DB2'i (AS400) sürüm 7.1 için
* IBM DB2 Linux, UNIX ve Windows (LUW) sürüm 11
* IBM DB2 sürüm 10.5 LUW için
* IBM DB2 sürüm 10.1 LUW için

> [!TIP]
> "Hello paket karşılık gelen tooan SQL deyimi yürütme isteği bulunamadı. hello hata iletisi alırsanız SQLSTATE 51002 SQLCODE =-805, = "hello nedeni hello normal kullanıcı hello işletim sistemi için gerekli bir paketi oluşturulmaz. tooresolve Bu sorun, DB2 sunucu türü için aşağıdaki yönergeleri izleyin:
> - DB2 için i (AS400): kopyalama etkinliği çalıştırmadan önce hello toplamalarında hello normal kullanıcı oluşturma power user olanak tanır. toocreate hello koleksiyonu, use hello komutu:`create collection <username>`
> - DB2 için z/OS veya LUW: kullanım yüksek ayrıcalıklı bir hesap--power user veya paket yetkilileri ve bağlama, BINDADD, sahip yönetim toorun hello kez kopya yürütme tooPUBLIC izinleri--verin. Merhaba gerekli paketi hello kopyalama sırasında otomatik olarak oluşturulur. Daha sonra sonraki kopyalama çalışmalarınız için geri toohello normal kullanıcı geçebilirsiniz.

## <a name="getting-started"></a>Başlarken
Farklı araçlar ve API'ler kullanarak kopyalama etkinliği toomove verilerle bir şirket içi DB2 veri deposu bir ardışık düzen oluşturabilirsiniz: 

- Merhaba en kolay yolu toocreate bir ardışık düzen toouse hello Azure Data Factory Kopyalama Sihirbazı ' dir. Hello hızlı bir anlatım hello Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma hakkında bilgi için bkz: [Öğreticisi: hello Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md). 
- Araçlar toocreate hello Azure portal, Visual Studio, Azure PowerShell, bir Azure Resource Manager şablonu, hello .NET API ve hello gibi bir işlem hattı de kullanabilirsiniz REST API. Adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için bkz: Merhaba [kopyalama etkinliği Öğreticisi](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:

1. Bağlı hizmetler toolink girdi ve çıktı veri depoları tooyour veri fabrikası oluşturun.
2. Veri kümeleri toorepresent girişi oluşturun ve çıktı verilerini hello kopyalama işlemi için. 
3. Bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile işlem hattı oluşturacaksınız. 

Merhaba, JSON tanımları hello Data Factory bağlı Hizmetleri, kopyalama Sihirbazı'nı kullandığınızda veri kümelerini ve ardışık düzen varlıklar otomatik olarak sizin için oluşturulur. Araçları veya API'ler (Merhaba dışında .NET API'si) kullandığınızda, hello Data Factory varlıklarını hello JSON biçimi kullanarak tanımlayın. Merhaba [JSON örnek: veri DB2 tooAzure Blob Depolama kopyalama](#json-example-copy-data-from-db2-to-azure-blob) hello JSON tanımlarını hello için bir şirket içi DB2 veri deposundaki kullanılan toocopy verileri Data Factory varlıklarını gösterir.

Aşağıdaki bölümlerde hello belirli tooa DB2 veri deposudur kullanılan toodefine hello Data Factory varlıklarını JSON özellikleri hello hakkında ayrıntılar verilmektedir.

## <a name="db2-linked-service-properties"></a>DB2 bağlantılı hizmet özellikleri
Aşağıdaki tablonun hello belirli tooa DB2 bağlantılı hizmet hello JSON özellikleri listeler.

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| **türü** |Bu özellik çok ayarlanmalıdır**OnPremisesDB2**. |Evet |
| **Sunucu** |Merhaba hello DB2 sunucunun adıdır. |Evet |
| **Veritabanı** |Merhaba DB2 veritabanına Hello adı. |Evet |
| **Şema** |Merhaba şema hello DB2 veritabanında Hello adı. Bu özellik, büyük/küçük harf duyarlıdır. |Hayır |
| **authenticationType** |kullanılan tooconnect toohello DB2 veritabanı kimlik doğrulaması Hello türü. Merhaba olası değerler şunlardır: Anonim, temel ve Windows. |Evet |
| **Kullanıcı adı** |Basic veya Windows kimlik doğrulaması kullanırsanız hello kullanıcı hesabı için Hello adı. |Hayır |
| **Parola** |Merhaba kullanıcı hesabının parolasını Hello. |Hayır |
| **gatewayName** |Data Factory hizmetinin hello hello ağ geçidinin Hello adı tooconnect toohello şirket içi DB2 veritabanına kullanmanız gerekir. |Evet |

## <a name="dataset-properties"></a>Veri kümesi özellikleri
Merhaba hello bölümleri ve veri kümelerini tanımlamak için kullanılabilir özelliklerin listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi. Bölümler, gibi **yapısı**, **kullanılabilirlik**ve hello **İlkesi** bir veri kümesi için JSON, tüm veri türleri (Azure SQL, Azure Blob storage, Azure Table için benzer Depolama vb.).

Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar. Merhaba **typeProperties** bir veri kümesi için bir bölüm türü **RelationalTable**, hello DB2 veri kümesini içeren, özellik aşağıdaki hello vardır:

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| **tableName** |Merhaba bağlantılı hizmet hello hello DB2 veritabanı örneğinde Merhaba tablonun adını gösterir. Bu özellik, büyük/küçük harf duyarlıdır. |Hayır (Merhaba, **sorgu** türü kopyalama etkinliği özelliğinin **RelationalSource** belirtilir) |

## <a name="copy-activity-properties"></a>Etkinlik özellikleri Kopyala
Merhaba hello bölümleri ve kopyalama etkinlikleri tanımlamak için kullanılabilir özelliklerin listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi. Etkinlik özellikleri gibi kopyalamak **adı**, **açıklama**, **girişleri** tablo **çıkarır** tablo ve **İlkesi**, tüm etkinlikler türleri için kullanılabilir. Merhaba hello kullanılabilir özellikler **typeProperties** her etkinlik türü için hello etkinliğin bölümü. Kopya etkinliği için hello özellikleri hello türlerini veri kaynakları ve havuzlarını bağlı olarak farklılık gösterir.

Kopyalama hello kaynak türü olduğunda etkinliği için **RelationalSource** (içeren DB2), aşağıdaki özelliklere hello hello kullanılabilir **typeProperties** bölümü:

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| **Sorgu** |Merhaba özel sorgu tooread hello verileri kullanın. |SQL sorgu dizesi. Örneğin, `"query": "select * from "MySchema"."MyTable""` |Hayır (Merhaba, **tableName** özellik kümesinin belirtilen) |

> [!NOTE]
> Şema ve tablo adları büyük/küçük harfe duyarlıdır. Merhaba sorgu deyimi içinde özellik adları kullanarak alın "" (çift tırnak). Örneğin:
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-tooazure-blob-storage"></a>JSON örnek: DB2 tooAzure Blob Depolama veri kopyalama
Bu örnek örnek JSON tanımları sağlar, toocreate bir ardışık düzen hello kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Merhaba örnek nasıl tooBlob depolama toocopy verilerden bir DB2 veritabanına gösterir. Ancak, veriler çok kopyalanabilir[desteklenen herhangi bir veriyi depolamak Havuz türü](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği.

Merhaba örnek Data Factory varlıklarını aşağıdaki hello sahiptir:

- Bir DB2 bağlantılı hizmet türü [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)
- Bir Azure Blob Depolama bağlantılı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
- Bir giriş [dataset](data-factory-create-datasets.md) türü [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)
- Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
- A [ardışık düzen](data-factory-create-pipelines.md) hello kullanan kopyalama etkinliği ile [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) özellikleri

Merhaba örnek veri DB2 veritabanına tooan Azure blob bir sorgu sonucunda saatlik kopyalar. Merhaba örnekte kullanılan JSON özellikleri hello hello varlık tanımları izleyin hello bölümlerde açıklanmıştır.

İlk adım olarak yükleyin ve bir veri ağ geçidi yapılandırın. Yönergelerdir hello [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.

**DB2 bağlı hizmet**

```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

**Azure Blob storage bağlı hizmeti**

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

**DB2 girdi veri kümesi**

Merhaba örnek DB2 "Merhaba zaman serisi veri için" zaman damgası"etiketli bir sütun sahip MyTable" adlı bir tablo oluşturduğunuzu varsayar.

Merhaba **dış** özelliği true olarak ayarlamak çok "." Bu ayar, bu veri kümesi dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil hello Data Factory hizmetinin bildirir. Bu hello fark **türü** özelliği çok ayarlanmış**RelationalTable**.


```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
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

Veri yazıldığı tooa yeni blob her saat ayarı hello tarafından **sıklığı** özelliği çok "Saat" ve hello **aralığı** özelliği too1. Merhaba **folderPath** özelliği hello blob dinamik olarak değerlendirilmesi için işleniyor hello dilimin hello başlangıç zamanı temel alarak. Merhaba klasör yolu hello yıl, ay, gün ve saat bölümlerini hello başlangıç saatini kullanır.

```json
{
    "name": "AzureBlobDb2DataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/db2/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Ardışık düzeni için başlangıç kopyalama etkinliği**

Merhaba ardışık düzen içeren yapılandırılmış bir kopyalama etkinliği toouse belirtilen giriş ve çıkış veri kümeleri ve saatte zamanlanmış toorun değil. Hello JSON tanımını hello ardışık düzeni için hello **kaynak** türü olarak ayarlanmış çok**RelationalSource** ve hello **havuz** türü olarak ayarlanmış çok**BlobSink**. Merhaba belirtilen hello SQL sorgusu **sorgu** özelliği hello "Siparişler" tablosundan hello veri seçer.

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for hello copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"Orders\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "Db2DataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDb2DataSet"
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
                "name": "Db2ToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-db2"></a>DB2 için tür eşlemesi
Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopyalama etkinliği, iki aşamalı bir yaklaşım aşağıdaki hello kullanarak kaynak türü toosink türünden otomatik tür dönüşümleri gerçekleştirir:

1. Yerel kaynak türü tooa .NET türü Dönüştür
2. .NET türü tooa yerel Havuz türü Dönüştür

Kopya etkinliği bir DB2 türü tooa .NET türünden hello veri dönüştürdüğünde hello aşağıdaki eşlemelerini kullanılır:

| DB2 veritabanı türü | .NET framework türü |
| --- | --- |
| Tamsayı |Int16 |
| Tamsayı |Int32 |
| BigInt |Int64 |
| Real |Tek |
| Çift |Çift |
| Kayan nokta |Çift |
| Ondalık |Ondalık |
| DecimalFloat |Ondalık |
| sayısal |Ondalık |
| Tarih |Tarih saat |
| Zaman |TimeSpan |
| zaman damgası |Tarih saat |
| XML |Byte] |
| char |Dize |
| VarChar |Dize |
| LongVarChar |Dize |
| DB2DynArray |Dize |
| İkili |Byte] |
| VarBinary |Byte] |
| LONGVARBINARY |Byte] |
| Grafiği |Dize |
| VarGraphic |Dize |
| LongVarGraphic |Dize |
| CLOB |Dize |
| Blob |Byte] |
| DbClob |Dize |
| Tamsayı |Int16 |
| Tamsayı |Int32 |
| BigInt |Int64 |
| Real |Tek |
| Çift |Çift |
| Kayan nokta |Çift |
| Ondalık |Ondalık |
| DecimalFloat |Ondalık |
| sayısal |Ondalık |
| Tarih |Tarih saat |
| Zaman |TimeSpan |
| zaman damgası |Tarih saat |
| XML |Byte] |
| char |Dize |

## <a name="map-source-toosink-columns"></a>Kaynak toosink sütunları eşleme
hello kaynak dataset toocolumns hello havuz kümesindeki toomap sütunlarında nasıl görürüm toolearn [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).

## <a name="repeatable-reads-from-relational-sources"></a>İlişkisel kaynaklardan yinelenebilir okuma
İlişkisel veri deposundan verileri kopyaladığınızda, Yinelenebilirlik göz tooavoid tutmak istenmeyen sonuçları. Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz. Merhaba yeniden deneme de yapılandırabilirsiniz **İlkesi** özelliği için bir veri kümesi toorerun bir hata oluştuğunda bir dilim. Merhaba aynı veri nasıl geçtiğinden bağımsız okuma emin olun birçok kez hello dilimi yeniden çalıştırın ve ne olursa olsun, nasıl hello dilimi yeniden çalıştırın. Daha fazla bilgi için bkz: [Repeatable okur ilişkisel kaynaklardan](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Performans ve ayar
Kopyalama etkinliği ve yolları toooptimize performans hello hello performansını etkileyen anahtar Etkenler hakkında bilgi edinin [kopya etkinliği performansının ve ayarlama Kılavuzu](data-factory-copy-activity-performance.md).
