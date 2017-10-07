---
title: "Azure Data Factory aaaFile ve sıkıştırma biçimlerde | Microsoft Docs"
description: "Azure Data Factory ile desteklenen hello dosya biçimleri hakkında bilgi edinin."
keywords: BLOB verilerini, azure blob kopyalama
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 9d40517b059fc533776bcc088db8c531ee5b003d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="file-and-compression-formats-supported-by-azure-data-factory"></a>Azure Data Factory tarafından desteklenen dosya ve sıkıştırma biçimleri
*Bu konu, bağlayıcıları aşağıdaki toohello geçerlidir: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [dosya sistemi](data-factory-onprem-file-system-connector.md), [ FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), ve [SFTP](data-factory-sftp-connector.md).*

Azure Data Factory hello şu dosya biçimi türlerini destekler:

* [Metin biçimi](#text-format)
* [JSON biçimi](#json-format)
* [Avro biçimi](#avro-format)
* [ORC biçimi](#orc-format)
* [Parquet biçimi](#parquet-format)

## <a name="text-format"></a>Metin biçimi
Bir metin dosyasından tooread istediğiniz veya tooa metin dosyasına yazma, hello ayarlayın `type` hello özelliğinde `format` hello dataset bölümü çok**TextFormat**. Merhaba aşağıdakileri de belirtebilirsiniz **isteğe bağlı** hello özelliklerinde `format` bölümü. Bkz: [TextFormat örnek](#textformat-example) nasıl bölüm tooconfigure.

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| columnDelimiter |Merhaba karakter tooseparate sütunları bir dosyada kullanılır. Verilerinizi değil olasılıkla olabilir nadir bir yazdırılamayan karakter var. toouse düşünebilirsiniz. Örneğin, Başlat, başlık (SOH) temsil eder "\u0001" belirtin. |Yalnızca bir karaktere izin verilir. Merhaba **varsayılan** değer **virgül (',')**. <br/><br/>toouse bir Unicode karakter başvurmak çok[Unicode karakterler](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello ilgili kod için. |Hayır |
| rowDelimiter |Merhaba karakter tooseparate satır bir dosyada kullanılır. |Yalnızca bir karaktere izin verilir. Merhaba **varsayılan** değerdir herhangi biri üzerinde okuma değerleri aşağıdaki hello: **["\r\n", "\r", "\n"]** ve **"\r\n"** yazma üzerinde. |Hayır |
| escapeChar |Merhaba özel karakter tooescape bir sütun ayırıcısı giriş dosyası hello içeriğinde kullanılır. <br/><br/>Bir tablo için hem escapeChar hem de quoteChar parametrelerini aynı anda belirtemezsiniz. |Yalnızca bir karaktere izin verilir. Varsayılan değer yoktur. <br/><br/>Örnek: virgül varsa (', ') hello sütun sınırlayıcı ancak toohave hello virgül karakteri hello metin istediğiniz şekilde (örnek: "Hello, world"), '$' hello kaçış karakteri olarak tanımlamak ve dizesi kullanın "$Hello, world" Merhaba kaynağındaki. |Hayır |
| quoteChar |Merhaba karakter tooquote bir dize değeri kullanılır. Hello sütun ve satır sınırlayıcıları hello tırnak karakterleri içine hello dize değeri bir parçası olarak değerlendirilmesi. Bu özellik geçerli tooboth girdidir ve çıkış veri kümeleri.<br/><br/>Bir tablo için hem escapeChar hem de quoteChar parametrelerini aynı anda belirtemezsiniz. |Yalnızca bir karaktere izin verilir. Varsayılan değer yoktur. <br/><br/>Virgül varsa, örneğin, (', ') hello sütun sınırlayıcı ancak toohave virgül karakteri hello metin istediğiniz gibi (örnek: < Hello, world >), tanımlayabileceğiniz "(tırnak) tırnak işareti karakteri hello ve hello dizesini kullanın"Hello, world"Merhaba kaynağındaki. |Hayır |
| nullValue |Bir veya daha fazla karakter toorepresent bir null değer kullanılır. |Bir veya daha fazla karakter olabilir. Merhaba **varsayılan** değerler **"\N" ve "NULL"** okunur ve **"\N"** yazma üzerinde. |Hayır |
| encodingName |Merhaba kodlama adı belirtin. |Geçerli bir kodlama adı. Bkz. [Encoding.EncodingName Özelliği](https://msdn.microsoft.com/library/system.text.encoding.aspx). Örnek: windows-1250 veya shift_jis. Merhaba **varsayılan** değer **UTF-8**. |Hayır |
| firstRowAsHeader |Tooconsider ilk satır bir başlık olarak hello olup olmadığını belirtir. Giriş veri kümesinde Data Factory ilk satırı üst bilgi olarak okur. Çıkış veri kümesinde Data Factory ilk satırı üst bilgi olarak yazar. <br/><br/>Örnek senaryolar için bkz. [`firstRowAsHeader` ve `skipLineCount` kullanım senaryoları](#scenarios-for-using-firstrowasheader-and-skiplinecount). |True<br/><b>False (varsayılan)</b> |Hayır |
| skipLineCount |Giriş dosyaları veri okuma satırları tooskip Hello sayısını gösterir. SkipLineCount ve firstRowAsHeader belirtilirse, hello satırlar ilk atlanır ve hello üst bilgileri hello giriş dosyasından sonra okuyun. <br/><br/>Örnek senaryolar için bkz. [`firstRowAsHeader` ve `skipLineCount` kullanım senaryoları](#scenarios-for-using-firstrowasheader-and-skiplinecount). |Tamsayı |Hayır |
| treatEmptyAsNull |Bir null olarak tootreat null veya boş dize değeri olup olmadığını belirten bir giriş dosyasından veri okuma. |**True (varsayılan)**<br/>False |Hayır |

### <a name="textformat-example"></a>TextFormat örneği
Bir veri kümesi için JSON tanımını izleyen hello hello isteğe bağlı özelliklerin bazıları belirtilir.

```json
"typeProperties":
{
    "folderPath": "mycontainer/myfolder",
    "fileName": "myblobname",
    "format":
    {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";",
        "quoteChar": "\"",
        "NullValue": "NaN",
        "firstRowAsHeader": true,
        "skipLineCount": 0,
        "treatEmptyAsNull": true
    }
},
```

toouse bir `escapeChar` yerine `quoteChar`, hello satırla değiştirin `quoteChar` escapeChar aşağıdaki hello ile:

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a>firstRowAsHeader ve skipLineCount kullanım senaryoları
* Dosya olmayan kaynak tooa metin dosyasından kopyalama ve tooadd hello şema meta verileri içeren bir başlık satırı istiyor musunuz (örneğin: SQL Şeması). Belirtin `firstRowAsHeader` hello çıkış DataSet Bu senaryo için true.
* Bir üst bilgi satırı tooa dosya olmayan havuz içeren bir metin dosyasından kopyalama ve satır toodrop istersiniz. Belirtin `firstRowAsHeader` hello girdi veri kümesi olarak true.
* Bir metin dosyasından kopyalama ve hiçbir veri veya üstbilgi bilgileri içeren birkaç satır hello başında tooskip istiyor. Belirtin `skipLineCount` tooindicate hello satırları toobe sayısı atlandı. Merhaba rest hello dosyasının bir başlık satırı içeriyorsa, ayrıca belirtebilirsiniz `firstRowAsHeader`. Her iki `skipLineCount` ve `firstRowAsHeader` belirtilirse, hello satırları ilk atlanır ve hello üstbilgi bilgileri hello giriş dosyasından sonra okuyun

## <a name="json-format"></a>JSON biçimi
çok**bir JSON dosyası olarak içeri/dışarı aktarma-olduğu içine/Azure Cosmos DB'den**, hello bakın [içeri/dışarı aktarma JSON belgeleri](data-factory-azure-documentdb-connector.md#importexport-json-documents) bölümüne [/Azure Cosmos DB'den veri taşıma](data-factory-azure-documentdb-connector.md) makalesi.

Merhaba, tooparse hello JSON dosyaları veya JSON biçiminde hello veri yazmak istiyorsanız ayarlayın `type` hello özelliğinde `format` çok bölümünde**JsonFormat**. Merhaba aşağıdakileri de belirtebilirsiniz **isteğe bağlı** hello özelliklerinde `format` bölümü. Bkz: [JsonFormat örnek](#jsonformat-example) nasıl bölüm tooconfigure.

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| filePattern |Her JSON dosyasında depolanan verilerin Hello desen belirtin. İzin verilen değerler: **setOfObjects** ve **arrayOfObjects**. Merhaba **varsayılan** değer **setOfObjects**. Bu desenler hakkında ayrıntılı bilgi için bkz. [JSON dosyası desenleri](#json-file-patterns). |Hayır |
| jsonNodeReference | Bir dizinin içindeki hello nesnelerinden verileri ayıklamak ve tooiterate isterseniz hello ile aynı alan desen, bu dizinin hello JSON yolu belirtin. Bu özellik yalnızca JSON dosyalarından veri kopyalarken desteklenir. | Hayır |
| jsonPathDefinition | Merhaba JSON yol ifadesi her sütun eşlemesi için özelleştirilmiş sütun adıyla (küçük başlayın) belirtin. Bu özellik yalnızca JSON dosyalarından veri kopyalarken desteklenir. Verileri nesne veya diziden ayıklayabilirsiniz. <br/><br/> Kök nesnede altında alanlar için kök $ ile Başlat; tarafından seçilen hello dizinin içindeki alanlar için `jsonNodeReference` özelliği, hello dizi öğesinin başından. Bkz: [JsonFormat örnek](#jsonformat-example) nasıl bölüm tooconfigure. | Hayır |
| encodingName |Merhaba kodlama adı belirtin. Geçerli kodlama adlar Hello listesi için bkz: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) özelliği. Örneğin: windows-1250 veya shift_jis. Merhaba **varsayılan** değer: **UTF-8**. |Hayır |
| nestingSeparator |Kullanılan tooseparate iç içe geçme düzeyi karakter. Merhaba varsayılan değer '.' (nokta). |Hayır |

### <a name="json-file-patterns"></a>JSON dosyası desenleri

Kopyalama etkinliği, JSON dosyalarınızın desenler izleyen hello ayrıştırma yapabilir:

- **1. Tür: setOfObjects**

    Her dosya tek bir nesne veya satırlara ayrılmış/bitiştirilmiş birden fazla nesne içerir. Bu seçenek bir çıkış veri kümesinde belirlendiğinde, kopyalama etkinliği her satırda bir nesnenin bulunduğu (satırlara ayrılmış) tek bir JSON dosyası üretir.

    * **tek nesne JSON örneği**

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        ```

    * **satırlara ayrılmış JSON örneği**

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * **bitiştirilmiş JSON örneği**

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        }
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
        ```

- **2. Tür: arrayOfObjects**

    Her dosya bir nesne dizisi içerir.

    ```json
    [
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        },
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        },
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
    ]
    ```

### <a name="jsonformat-example"></a>JsonFormat örneği

**Örnek Durum 1: JSON dosyalarından veri kopyalama**

İki örnek verileri JSON dosyaları kopyalarken aşağıdaki hello bakın. Merhaba genel toonote noktaları:

**Örnek 1: nesne ve diziden veri ayıklama**

Bu örnekte, bir kök JSON nesnesi toosingle kaydı tablo sonuç eşler bekler. İçeriği aşağıdaki hello ile bir JSON dosyası varsa:  

```json
{
    "id": "ed0e4960-d9c5-11e6-85dc-d7996816aad3",
    "context": {
        "device": {
            "type": "PC"
        },
        "custom": {
            "dimensions": [
                {
                    "TargetResourceType": "Microsoft.Compute/virtualMachines"
                },
                {
                    "ResourceManagmentProcessRunId": "827f8aaa-ab72-437c-ba48-d8917a7336a3"
                },
                {
                    "OccurrenceTime": "1/13/2017 11:24:37 AM"
                }
            ]
        }
    }
}
```
ve bunu bir Azure SQL tablosuna hello aşağıdaki biçimi, veri nesneleri hem dizi çıkartarak toocopy istiyor:

| id | deviceType | targetResourceType | resourceManagmentProcessRunId | occurrenceTime |
| --- | --- | --- | --- | --- |
| ed0e4960-d9c5-11e6-85dc-d7996816aad3 | PC | Microsoft.Compute/virtualMachines | 827f8aaa-ab72-437c-ba48-d8917a7336a3 | 1/13/2017 11:24:37 AM |

Merhaba girdi veri kümesi ile **JsonFormat** türü şu şekilde tanımlanır: (yalnızca hello ilgili bölümleri kısmi tanımıyla). Daha ayrıntılı belirtmek gerekirse:

- `structure`Bölüm tootabular veri dönüştürülürken özelleştirilmiş hello sütun adları ve hello karşılık gelen veri türünü tanımlar. Bu bölüm **isteğe bağlı** toodo sütun eşlemesi gerekmedikçe. Bkz: [kaynak veri kümesi sütunları toodestination dataset sütunlara](data-factory-map-columns.md) daha fazla ayrıntı için bölüm.
- `jsonPathDefinition`Burada tooextract hello verilerden belirten her sütun için Hello JSON yolu belirtir. kullanabileceğiniz toocopy veri dizisinden **array [x] .property** özelliği hello un x. nesne veya size verilen hello tooextract değerini kullanabilir  **dizisi [*] .property** toofind Böyle bir özellik içeren herhangi bir nesneden Hello değeri.

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "deviceType",
            "type": "String"
        },
        {
            "name": "targetResourceType",
            "type": "String"
        },
        {
            "name": "resourceManagmentProcessRunId",
            "type": "String"
        },
        {
            "name": "occurrenceTime",
            "type": "DateTime"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonPathDefinition": {"id": "$.id", "deviceType": "$.context.device.type", "targetResourceType": "$.context.custom.dimensions[0].TargetResourceType", "resourceManagmentProcessRunId": "$.context.custom.dimensions[1].ResourceManagmentProcessRunId", "occurrenceTime": " $.context.custom.dimensions[2].OccurrenceTime"}      
        }
    }
}
```

**Örnek 2: çapraz hello aynı diziden desen ile birden çok nesne uygulayın.**

Bu örnekte, tablo sonuç içinde birden çok kayıt içine tootransform bir kök JSON nesnesi bekler. İçeriği aşağıdaki hello ile bir JSON dosyası varsa:  

```json
{
    "ordernumber": "01",
    "orderdate": "20170122",
    "orderlines": [
        {
            "prod": "p1",
            "price": 23
        },
        {
            "prod": "p2",
            "price": 13
        },
        {
            "prod": "p3",
            "price": 231
        }
    ],
    "city": [ { "sanmateo": "No 1" } ]
}
```
ve bunu bir Azure SQL tablosuna hello aşağıdaki biçiminde hello veri hello dizinin içindeki düzleştirme tarafından toocopy istediğiniz ve çapraz birleştirme hello ortak kök bilgileri ile:

| ordernumber | orderdate | order_pd | order_price | city |
| --- | --- | --- | --- | --- |
| 01 | 20170122 | P1 | 23 | [{"sanmateo":"No 1"}] |
| 01 | 20170122 | P2 | 13 | [{"sanmateo":"No 1"}] |
| 01 | 20170122 | P3 | 231 | [{"sanmateo":"No 1"}] |

Merhaba girdi veri kümesi ile **JsonFormat** türü şu şekilde tanımlanır: (yalnızca hello ilgili bölümleri kısmi tanımıyla). Daha ayrıntılı belirtmek gerekirse:

- `structure`Bölüm tootabular veri dönüştürülürken özelleştirilmiş hello sütun adları ve hello karşılık gelen veri türünü tanımlar. Bu bölüm **isteğe bağlı** toodo sütun eşlemesi gerekmedikçe. Bkz: [kaynak veri kümesi sütunları toodestination dataset sütunlara](data-factory-map-columns.md) daha fazla ayrıntı için bölüm.
- `jsonNodeReference`aynı desen altında hello hello nesneleriyle tooiterate ve ayıklama verilerini gösteren **dizi** orderlines.
- `jsonPathDefinition`Burada tooextract hello verilerden belirten her sütun için Hello JSON yolu belirtir. Bu örnekte "$.", "order_pd" ve "order_price" "$" olmadan hello array öğesinden türetilen yoluyla tanımlı başlangıç JSON yolu ile kök nesnesi altında "ordernumber", "orderdate" ve "Şehir" olur.

```json
"properties": {
    "structure": [
        {
            "name": "ordernumber",
            "type": "String"
        },
        {
            "name": "orderdate",
            "type": "String"
        },
        {
            "name": "order_pd",
            "type": "String"
        },
        {
            "name": "order_price",
            "type": "Int64"
        },
        {
            "name": "city",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonNodeReference": "$.orderlines",
            "jsonPathDefinition": {"ordernumber": "$.ordernumber", "orderdate": "$.orderdate", "order_pd": "prod", "order_price": "price", "city": " $.city"}         
        }
    }
}
```

**Hello aşağıdaki noktaları göz önünde bulundurun:**

* Merhaba, `structure` ve `jsonPathDefinition` hello Data Factory veri kümesi içinde hello tanımlanmayan kopyalama etkinliği hello hello ilk nesne şemadan ve nesnenin tamamı hello düzleştirmek algılar.
* Merhaba JSON girişi bir dizi varsa, varsayılan olarak hello kopyalama etkinliği hello tüm dizi değeri bir dizeye dönüştürür. Tooextract verileri kullanarak ondan seçebilirsiniz `jsonNodeReference` ve/veya `jsonPathDefinition`, veya içinde belirterek değil atlayabilirsiniz `jsonPathDefinition`.
* Varsa yinelenen adları, aynı düzeydeki Merhaba, hello kopyalama etkinliği hello sonuncu seçer.
* Özellik adları büyük/küçük harfe duyarlıdır. Aynı ada ancak farklı büyük/küçük harf düzenine sahip iki özellik, iki ayrı özellik olarak kabul edilir.

**Durum 2: veri tooJSON dosyası yazılıyor**

SQL veritabanı tablosunda aşağıdaki hello varsa:

| id | order_date | order_price | order_by |
| --- | --- | --- | --- |
| 1 | 20170119 | 2000 | David |
| 2 | 20170120 | 3500 | Patrick |
| 3 | 20170121 | 4000 | Jason |

ve her bir kaydı toowrite tooa JSON nesnesi biçimini izleyen hello beklediğiniz:
```json
{
    "id": "1",
    "order": {
        "date": "20170119",
        "price": 2000,
        "customer": "David"
    }
}
```

Merhaba çıkış veri kümesi ile **JsonFormat** türü şu şekilde tanımlanır: (yalnızca hello ilgili bölümleri kısmi tanımıyla). Daha belirgin olarak `structure` bölüm hedef dosyasında özelleştirilmiş hello özellik adlarını tanımlar `nestingSeparator` (varsayılan değer ".") hello adından kullanılan tooidentify hello iç içe katmandır. Bu bölüm **isteğe bağlı** toochange hello özellik adı kaynak sütun adı ile karşılaştırmak istediğiniz ya da hello özelliklerden bazıları iç içe sürece.

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "order.date",
            "type": "String"
        },
        {
            "name": "order.price",
            "type": "Int64"
        },
        {
            "name": "order.customer",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat"
        }
    }
}
```

## <a name="avro-format"></a>AVRO biçimi
Tooparse hello Avro dosyalarının istediğiniz veya Avro biçiminde hello veri yazmak istiyorsanız, hello ayarlayın `format` `type` özelliği çok**AvroFormat**. Merhaba typeProperties bölüm içindeki hello biçimi bölümünde herhangi bir özellik toospecify gerekmez. Örnek:

```json
"format":
{
    "type": "AvroFormat",
}
```

bir Hive tablosu toouse Avro biçimi, başvurabilirsiniz çok[Apache Hive'nın Öğreticisi](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).

Hello aşağıdaki noktaları göz önünde bulundurun:  

* [Karmaşık veri türlerini](http://avro.apache.org/docs/current/spec.html#schema_complex) desteklenmez (kaydeder, numaralandırmalar, dizileri, haritalar, birleşimler ve sabit).

## <a name="orc-format"></a>ORC biçimi
Merhaba, tooparse hello ORC dosyaları veya ORC biçiminde hello veri yazmak istiyorsanız ayarlayın `format` `type` özelliği çok**OrcFormat**. Merhaba typeProperties bölüm içindeki hello biçimi bölümünde herhangi bir özellik toospecify gerekmez. Örnek:

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> ORC dosyaları kopyalıyorsanız değil, **olarak-olduğu** şirket içi ve bulut arasında veri depolarına, ağ geçidi makinenizde tooinstall hello JRE 8 (Java Çalışma zamanı ortamı) gerekir. 64 bit ağ geçidi için 64 bit JRE, 32 bit ağ geçidi için de 32 bit JRE gerekir. İki sürüme de [buradan](http://go.microsoft.com/fwlink/?LinkId=808605) ulaşabilirsiniz. Merhaba uygun olanı seçin.
>
>

Hello aşağıdaki noktaları göz önünde bulundurun:

* Karmaşık veri türleri desteklenmez (STRUCT, MAP, LIST, UNION)
* ORC dosyası [sıkıştırmayla ilgili üç seçeneğe sahiptir](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY. Data Factory, bu sıkıştırma biçimlerinin herhangi birine sahip ORC dosyalarını okuyabilir. Merhaba sıkıştırma kullanır codec olduğu hello meta veri tooread hello verileri. Ancak, tooan ORC dosyasına yazarken, veri fabrikası ZLIB, ORC için hello varsayılan olduğu seçer. Şu anda bu davranış hiçbir seçeneği toooverride yoktur.

## <a name="parquet-format"></a>Parquet biçimi
Tooparse hello Parquet dosyalarının istediğiniz veya Parquet biçiminde hello veri yazmak istiyorsanız, hello ayarlayın `format` `type` özelliği çok**ParquetFormat**. Merhaba typeProperties bölüm içindeki hello biçimi bölümünde herhangi bir özellik toospecify gerekmez. Örnek:

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> Parquet dosyaları kopyalıyorsanız değil, **olarak-olduğu** şirket içi ve bulut arasında veri depolarına, ağ geçidi makinenizde tooinstall hello JRE 8 (Java Çalışma zamanı ortamı) gerekir. 64 bit ağ geçidi için 64 bit JRE, 32 bit ağ geçidi için de 32 bit JRE gerekir. İki sürüme de [buradan](http://go.microsoft.com/fwlink/?LinkId=808605) ulaşabilirsiniz. Merhaba uygun olanı seçin.
>
>

Hello aşağıdaki noktaları göz önünde bulundurun:

* Karmaşık veri türleri desteklenmez (MAP, LIST)
* Parquet dosya sıkıştırma ilgili seçenekleri aşağıdaki hello vardır: NONE, SNAPPY, GZIP ve LZO. Data Factory, bu sıkıştırma biçimlerinin herhangi birine sahip ORC dosyalarını okuyabilir. Merhaba sıkıştırma codec hello meta veri tooread hello verileri kullanır. Ancak, tooa Parquet dosyasına yazarken, veri fabrikası SNAPPY, Parquet biçiminde hello varsayılan olduğu seçer. Şu anda bu davranış hiçbir seçeneği toooverride yoktur.

## <a name="compression-support"></a>Sıkıştırma desteği
Büyük veri kümeleri işleme g/ç ve ağ performans sorunlarına neden. Bu nedenle, sıkıştırılmış veri depolarında yazabilir yalnızca hello ağ üzerinden veri aktarımı hızı ve disk alanından tasarruf, ancak ayrıca büyük veri işlerken önemli performans geliştirmeleri getirin. Şu anda sıkıştırma, Azure Blob veya şirket içi dosya sistemi gibi dosya tabanlı veri depoları için desteklenir.  

bir veri kümesi, kullanım hello toospecify sıkıştırma **sıkıştırma** aşağıdaki örneğine hello olduğu gibi JSON hello kümesindeki özelliği:   

```json
{  
    "name": "AzureBlobDataSet",  
    "properties": {  
        "availability": {  
            "frequency": "Day",  
              "interval": 1  
        },  
        "type": "AzureBlob",  
        "linkedServiceName": "StorageLinkedService",  
        "typeProperties": {  
            "fileName": "pagecounts.csv.gz",  
            "folderPath": "compression/file/",  
            "compression": {  
                "type": "GZip",  
                "level": "Optimal"  
            }  
        }  
    }  
}  
```

Merhaba örnek veri kümesi kopyalama etkinliği hello çıkış olarak kullanılan varsayalım hello kopyalama etkinliği sıkıştırır hello GZIP codec ile en iyi oranını kullanarak çıktı verilerini ve hello Azure Blob Storage pagecounts.csv.gz adlı bir dosyaya sıkıştırılmış hello veri yazma.

> [!NOTE]
> Merhaba veri sıkıştırma ayarları desteklenmez **AvroFormat**, **OrcFormat**, veya **ParquetFormat**. Bu biçimler dosyalarında okurken, veri fabrikası algılar ve hello sıkıştırma codec hello meta verilerde kullanır. Toofiles aşağıdaki biçimlerde yazarken, veri fabrikası hello varsayılan sıkıştırma codec Bu biçim seçer. Örneğin, ZLIB OrcFormat ve ParquetFormat SNAPPY.   

Merhaba **sıkıştırma** bölüm iki özellik vardır:  

* **Tür:** olabilir hello sıkıştırma codec **GZIP**, **Deflate**, **bzıp2**, veya **ZipDeflate**.  
* **Düzeyi:** olabilir hello sıkıştırma oranı **Optimal** veya **en hızlı**.

  * **Hızlı:** hello sıkıştırma işlemini tamamlamanız gereken mümkün olan en kısa sürede hello elde edilen dosyası en iyi şekilde sıkıştırılmaz olsa bile.
  * **En iyi**: hello sıkıştırma işlemi en iyi şekilde sıkıştırılmış, dahi hello işlemi daha uzun bir süre toocomplete alır.

    Daha fazla bilgi için bkz: [sıkıştırma düzeyi](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) konu.

Belirttiğinizde `compression` bir girdi veri kümesi JSON özelliğinde hello ardışık düzen hello kaynağından; sıkıştırılmış verileri okuyabilir ve bir çıkış dataset JSON hello özelliğini belirttiğinizde hello kopyalama etkinliği sıkıştırılmış veri toohello hedef yazabilirsiniz. Bazı örnek senaryolar verilmiştir:

* GZIP sıkıştırılmış verileri Azure blob'tan okuma, iptal ve sonuç verileri tooan Azure SQL veritabanı yazma. Merhaba giriş Azure Blob kümesiyle hello tanımladığınız `compression` `type` JSON özellik GZIP olarak.
* Şirket içi dosya sistemi düz metin dosyasından veri okunamıyor, GZip biçimi kullanarak Sıkıştır ve sıkıştırılmış hello veri tooan Azure blob yazma. Merhaba çıktı Azure Blob kümesiyle tanımladığınız `compression` `type` JSON özellik GZip olarak.
* FTP sunucusu, .zip dosyasından okuma içindeki tooget hello dosyaları sıkıştırılmış ve bu dosyaların Azure Data Lake Store güden. Girdi bir FTP veri kümesi'hello ile tanımladığınız `compression` `type` JSON özelliği ZipDeflate olarak.
* GZIP sıkıştırılmış verileri Azure blob'tan okuma, iptal, bzıp2 kullanarak Sıkıştır ve sonuç verileri tooan Azure blob yazma. Merhaba giriş Azure Blob kümesiyle tanımladığınız `compression` `type` tooGZIP ayarlayın ve çıktı veri kümesi ile Merhaba `compression` `type` tooBZIP2 bu durumda ayarlayın.   


## <a name="next-steps"></a>Sonraki adımlar
Aşağıdaki makaleler Azure Data Factory ile desteklenen dosya tabanlı veri depoları için hello bakın:

- [Azure Blob Depolama](data-factory-azure-blob-connector.md)
- [Azure Data Lake Store](data-factory-azure-datalake-connector.md)
- [FTP](data-factory-ftp-connector.md)
- [HDFS](data-factory-hdfs-connector.md)
- [Dosya Sistemi](data-factory-onprem-file-system-connector.md)
- [Amazon S3](data-factory-amazon-simple-storage-service-connector.md)
