---
title: "Tetikleyicileri ve bağlamaları Azure işlevlerinde ile aaaWork | Microsoft Docs"
description: "Nasıl toouse tetikler ve Azure işlevleri tooconnect bağlama kod yürütme tooonline olayları ve bulut tabanlı hizmetleri öğrenin."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure işlevleri, işlevler, olay işleme, web kancaları, dinamik işlem, sunucusuz mimari"
ms.assetid: cbc7460a-4d8a-423f-a63e-1cd33fef7252
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: donnam
ms.openlocfilehash: eb2ebfca172fcc8c0f479adbcfec99e90fc33615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a>Azure işlevleri Tetikleyicileri ve bağlamaları kavramları
Azure işlevleri sağlar, Azure ve diğer hizmetleri yanıt tooevents toowrite kodda aracılığıyla *Tetikleyicileri* ve *bağlamaları*. Bu makalede Tetikleyicileri kavramsal genel bakış olduğundan ve tüm bağlamaları desteklenen programlama dilleri. Ortak tooall bağlamaları özellikleri burada açıklanmıştır.

## <a name="overview"></a>Genel Bakış

Tetikleyicileri ve bağlamaları olan bir bildirim temelli yolu toodefine nasıl bir işlev çağrılır ve hangi verilerin, ile birlikte çalışır. A *tetikleyici* bir işlev nasıl çağrıldığını tanımlar. Bir işlev tam olarak bir tetikleyici olması gerekir. Tetikleyiciler genellikle hello işlevi tetiklenen hello yükü olduğu veri ilişkilendirdiniz. 

Giriş ve çıkış *bağlamaları* kodunuzu içinde bildirim temelli yolu tooconnect toodata gelen sağlayın. Benzer tootriggers işlevi yapılandırmanızda bağlantı dizeleri ve diğer özellikleri belirtin. Bağlamaları isteğe bağlıdır ve bir işlev birden fazla giriş varsa ve bağlamaları çıktı. 

Tetikleyicileri ve bağlamaları kullanarak, daha genel olan ve olmayan stillerinizin hello ayrıntılarını hello Hizmetleri ile etkileşime giren mu kod yazabilirsiniz. İşlevi kodunuz için giriş değerleri Hizmetleri yalnızca haline gelen veri. (örneğin, yeni bir satır Azure tablo Depolama'da oluşturma), toooutput veri tooanother hizmeti hello hello yönteminin dönüş değeri kullanın. Veya birden çok değer toooutput gerekiyorsa, bir yardımcı nesnesi kullanın. Tetikleyicileri ve bağlamaları sahip bir **adı** kod tooaccess hello bağlamasında kullandığınız bir tanımlayıcıdır özelliği.

Hello Tetikleyicileri ve bağlamaları yapılandırabilirsiniz **tümleştir** hello Azure işlevleri portalına sekmesindedir. Merhaba perde arkasında hello UI adlı bir dosya değiştirir *function.json* hello işlevi dizindeki dosyayı. Bu dosyayı toohello değiştirerek düzenleyebilirsiniz **Gelişmiş Düzenleyici**.

Merhaba aşağıdaki tabloda hello tetikleyiciler ve Azure işlevleri ile desteklenen bağlamaları gösterilmektedir. 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a>Örnek: bağlama sırası tetikleyici ve tablo çıktısı

Her Azure kuyruk depolamada yeni bir ileti görüntülendiğinde toowrite yeni bir satır tooAzure Table Storage istediğinizi varsayalım. Bu senaryo, bir Azure kuyruk kullanarak uygulanabilir tetikleyici ve bir tablo çıktısı bağlama. 

Bir kuyruk tetikleyici hello bilgileri aşağıdaki hello gerektirir **tümleştir** sekmesi:

* Merhaba depolama hesabı bağlantı dizesi hello sıranın içeren hello uygulama ayarı Hello adı
* Merhaba kuyruk adı
* Merhaba kuyruk iletisi, kod tooread hello içeriğini tanımlayıcı gibi hello `order`.

toowrite tooAzure Table Storage, aşağıdaki ayrıntılara hello ile bir çıktı bağlama kullanın:

* Merhaba tablonun hello depolama hesabı bağlantı dizesi içeren hello uygulama ayarı Hello adı
* Merhaba tablo adı
* kod toocreate Hello tanımlayıcıda öğeler veya hello dönüş değeri hello işlevden çıktı.

Bağlantı dizeleri tooenforce hello en iyi uygulama için bağlamaları kullanma uygulaması ayarları *function.json* hizmet gizli içermiyor.

Sonra kodunuzu Azure Storage ile toointegrate sağlanan hello tanımlayıcılar kullanın.

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello method return value creates a new row in Table Storage
public static Person Run(JObject order, TraceWriter log)
{
    return new Person() { 
            PartitionKey = "Orders", 
            RowKey = Guid.NewGuid().ToString(),  
            Name = order["Name"].ToString(),
            MobileNumber = order["MobileNumber"].ToString() };  
}
 
public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
    public string MobileNumber { get; set; }
}
```

```javascript
// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello second parameter toocontext.done is used as hello value for hello new row
module.exports = function (context, order) {
    order.PartitionKey = "Orders";
    order.RowKey = generateRandomId(); 

    context.done(null, order);
};

function generateRandomId() {
    return Math.random().toString(36).substring(2, 15) +
        Math.random().toString(36).substring(2, 15);
}
```

Merhaba işte *function.json* kod önceki toohello karşılık gelir. Merhaba işlev uygulama hello dilinden bağımsız olarak aynı yapılandırmayı kullanılabilir o hello unutmayın.

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```
tooview ve düzenleme Merhaba içeriğine *function.json* hello hello Azure portal'ı tıklatın **Gelişmiş Düzenleyici** hello seçeneği **tümleştir** işlevinizi sekmesinde.

Daha fazla kod örnekleri ve Azure Storage ile tümleştirme hakkında bilgi için bkz: [Azure işlevleri Tetikleyicileri ve bağlamaları Azure Storage için](functions-bindings-storage.md).

### <a name="binding-direction"></a>Bağlama yönü

Tüm Tetikleyicileri ve bağlamaları sahip bir `direction` özelliği:

- Tetikleyiciler için her zaman hello yönü olur`in`
- Giriş ve çıkış bağlamaları kullanmak `in` ve`out`
- Özel bir yön bazı bağlamaları Destek `inout`. Kullanırsanız `inout`, yalnızca hello **Gelişmiş Düzenleyici** hello kullanılabilir **tümleştir** sekmesi.

## <a name="using-hello-function-return-type-tooreturn-a-single-output"></a>Merhaba işlevi dönüş türü tooreturn tek bir çıktı kullanma

Merhaba önceki örnekte nasıl toouse hello işlevi dönüş değeri tooprovide hello özel name parametresi kullanılarak elde edilir tooa bağlama çıktısını gösterir `$return`. (Bu yalnızca C#, JavaScript ve F # gibi bir dönüş değerine sahip dillerde desteklenir.) Bir işlev birden çok çıktı bağlaması içeriyorsa `$return` hello çıkış bağlamaları yalnızca biri için. 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

C#, JavaScript ve F # çıkış bağlamalarla türleri kullanılır Hello örnekleri Göster aşağıda nasıl döndür.

```cs
// C# example: use method return value for output binding
public static string Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```cs
// C# example: async method, using return value for output binding
public static Task<string> Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```javascript
// JavaScript: return a value in hello second parameter toocontext.done
module.exports = function (context, input) {
    var json = JSON.stringify(input);
    context.log('Node.js script processed queue message', json);
    context.done(null, json);
}
```

```fsharp
// F# example: use return value for output binding
let Run(input: WorkItem, log: TraceWriter) =
    let json = String.Format("{{ \"id\": \"{0}\" }}", input.Id)   
    log.Info(sprintf "F# script processed queue message '%s'" json)
    json
```

## <a name="binding-datatype-property"></a>DataType özelliği için bağlama

.NET ile Merhaba türleri toodefine hello veri türü için giriş verileri kullanın. Örneğin, kullanın `string` toobind toohello metnin bir sıra tetikleyici ve bir bayt dizisi tooread ikili olarak.

JavaScript gibi dinamik olarak yazılan diller için hello kullan `dataType` hello bağlama tanımında özelliği. Örneğin, tooread ikili biçimde bir HTTP isteğinin içerik Merhaba, hello türünü kullanmak `binary`:

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

Diğer seçenekler için `dataType` olan `stream` ve `string`.

## <a name="resolving-app-settings"></a>Uygulama ayarlarını çözümleme
En iyi uygulama, parolaları ve bağlantı dizeleri yapılandırma dosyalarını yerine uygulama ayarları kullanılarak yönetilmelidir. Bu sınırlar erişim toothese gizli ve güvenli toostore kolaylaştırır *function.json* ortak kaynak denetimi havuzunda.

Uygulama ayarları da hello ortamına bağlı toochange yapılandırma istediğinizde kullanışlıdır. Örneğin, bir test ortamında toomonitor farklı bir sıra veya blob depolama kapsayıcısı isteyebilirsiniz.

Uygulama ayarları, yüzde işaretleri gibi içine alınmış bir değer her çözümlendirinden `%MyAppSetting%`. Bu hello Not `connection` Tetikleyicileri ve bağlamaları özelliği özel bir durumdur ve uygulama ayarlarının değerleri otomatik olarak çözer. 

Merhaba aşağıdaki örnekte olduğu bir uygulama ayarını kullanan bir sıra tetikleyici `%input-queue-name%` toodefine hello sıra tootrigger üzerinde.

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "%input-queue-name%",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```

## <a name="trigger-metadata-properties"></a>Tetikleyici meta veri özellikleri

Toohello veri yükü tetikleyici (örneğin, bir işlev tetiklenen hello kuyruk iletisi) tarafından sağlanan ek birçok Tetikleyicileri ek meta veri değerleri sağlayın. Bu değerler, C# ve F # veya hello özellikleri giriş parametresi olarak kullanılabilir `context.bindings` JavaScript nesne. 

Örneğin, bir sıra tetikleyici aşağıdaki özelliklere hello destekler:

* QueueTrigger - geçerli bir dize, ileti içeriği tetikleme
* DequeueCount
* expirationTime
* Kimlik
* InsertionTime
* NextVisibleTime
* PopReceipt

Her tetikleyici için meta veri özelliklerini ayrıntılarını hello karşılık gelen başvuru konusunda açıklanmıştır. Belgeleri kullanılabilir ayrıca hello **tümleştir** hello portalında hello sekmesinde **belgelerine** hello bağlama yapılandırma alanı aşağıdaki bölümüne.  

Bazı gecikmeler BLOB Tetikleyicileri sahip olduğundan, örneğin, bir sıra tetikleyici toorun işlevinizi kullanabilirsiniz (bkz [Blob Depolama tetikleyici](functions-bindings-storage-blob.md#storage-blob-trigger). Merhaba kuyruk iletisi üzerinde hello blob filename tootrigger içerecektir. Hello kullanarak `queueTrigger` meta veri özelliği, tüm yapılandırmanızı yerine kodunuzu bu davranış belirtebilirsiniz.

```json
  "bindings": [
    {
      "name": "myQueueItem",
      "type": "queueTrigger",
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "direction": "in",
      "connection": "MyStorageConnection"
    }
  ]
```

Bir tetikleyiciden meta veri özelliklerini de kullanılabilir bir *ifade bağlama* bölümden açıklandığı hello olarak başka bir bağlama için.

## <a name="binding-expressions-and-patterns"></a>İfadeler ve desenler bağlama

Tetikleyicileri ve bağlamaları hello en güçlü özelliklerden biridir *ifadeleri bağlama*. İçinde bağlama, diğer bağlamaları veya kodunuzu daha sonra kullanılabilir düzeni ifadeler tanımlayabilirsiniz. Tetikleyici meta veri bölümü önceki hello hello örnek Göster olarak ifadeleri, bağlama de kullanılabilir.

Örneğin, belirli bir blob depolama kapsayıcısını, benzer toohello tooresize görüntülerinde istediğinizi varsayalım **görüntü Boyutlandır** hello şablonunda **yeni işlev** sayfası. Çok Git**yeni işlev** dil -> **C#** senaryo -> **örnekleri** -> **ImageResizer CSharp**. 

Merhaba işte *function.json* tanımı:

```json
{
  "bindings": [
    {
      "name": "image",
      "type": "blobTrigger",
      "path": "sample-images/{filename}",
      "direction": "in",
      "connection": "MyStorageConnection"
    },
    {
      "name": "imageSmall",
      "type": "blob",
      "path": "sample-images-sm/{filename}",
      "direction": "out",
      "connection": "MyStorageConnection"
    }
  ],
}
```

Bu hello fark `filename` parametresi hem hello blob tetikleyicinizin tanımını yanı sıra hello blobu kullanılır bağlama çıktı. Bu parametre, işlev kodu de kullanılabilir.

```csharp
// C# example of binding too{filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a>Rastgele GUID'leri
Azure işlevleri hello aracılığıyla, bağlamalarda GUID'ler oluşturmak için bir kolaylık sözdizimi sağlar `{rand-guid}` ifade bağlama. Merhaba aşağıdaki örnekte bu toogenerate benzersiz blob adı kullanır: 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a>Geçerli saat

Merhaba bağlama deyimi kullanabilirsiniz `DateTime`, hangi çözümler çok`DateTime.UtcNow`.

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-toocustom-input-properties-in-a-binding-expression"></a>Bir bağlama ifadesinde toocustom giriş özellikleri bağlama

İfadeler bağlama hello tetikleyici yükünde kendisini tanımlanan özellikler başvuruda bulunabilir. Örneğin, bir Web kancası sağlanan bir dosya adı toodynamically bağlama tooa blob depolama dosyası isteyebilirsiniz.

Örneğin, aşağıdaki hello *function.json* adlı bir özellik kullanır `BlobName` hello tetikleyici yükü gelen:

```json
{
  "bindings": [
    {
      "name": "info",
      "type": "httpTrigger",
      "direction": "in",
      "webHookType": "genericJson",
    },
    {
      "name": "blobContents",
      "type": "blob",
      "direction": "in",
      "path": "strings/{BlobName}",
      "connection": "AzureWebJobsStorage"
    },
    {
      "name": "res",
      "type": "http",
      "direction": "out"
    }
  ]
}
```

tooaccomplish bu C# ve F # ' hello tetikleyici yükünde seri durumdan hello alanlarını tanımlayan bir POCO tanımlamanız gerekir.

```csharp
using System.Net;

public class BlobInfo
{
    public string BlobName { get; set; }
}
  
public static HttpResponseMessage Run(HttpRequestMessage req, BlobInfo info, string blobContents)
{
    if (blobContents == null) {
        return req.CreateResponse(HttpStatusCode.NotFound);
    } 

    return req.CreateResponse(HttpStatusCode.OK, new {
        data = $"{blobContents}"
    });
}
```

JavaScript, JSON seri durumundan çıkarma otomatik olarak gerçekleştirilir ve doğrudan hello özelliklerini kullanabilirsiniz.

```javascript
module.exports = function (context, info) {
    if ('BlobName' in info) {
        context.res = {
            body: { 'data': context.bindings.blobContents }
        }
    }
    else {
        context.res = {
            status: 404
        };
    }
    context.done();
}
```

## <a name="configuring-binding-data-at-runtime"></a>Çalışma zamanında veri bağlama yapılandırma

C# ve diğer .NET dilleri karşılıklı toohello bildirim temelli bağlama olarak kesinlik temelli bağlama düzeni kullanabilirsiniz *function.json*. Kesinlik temelli bağlama bağlama parametreleri tasarım yerine çalışma zamanında hesaplanan toobe gerektiğinde kullanışlıdır. toolearn daha, fazla [kesinlik temelli bağlamaları aracılığıyla çalışma zamanında bağlama](functions-reference-csharp.md#imperative-bindings) hello C# Geliştirici Başvurusu.

## <a name="next-steps"></a>Sonraki adımlar
Belirli bir bağlama hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın:

- [HTTP ve web kancaları](functions-bindings-http-webhook.md)
- [Zamanlayıcı](functions-bindings-timer.md)
- [Kuyruk depolama](functions-bindings-storage-queue.md)
- [Blob depolama](functions-bindings-storage-blob.md)
- [Tablo depolama](functions-bindings-storage-table.md)
- [Olay Hub’ı](functions-bindings-event-hubs.md)
- [Service Bus](functions-bindings-service-bus.md)
- [Cosmos DB](functions-bindings-documentdb.md)
- [SendGrid](functions-bindings-sendgrid.md)
- [Twilio](functions-bindings-twilio.md)
- [Notification Hubs](functions-bindings-notification-hubs.md)
- [Mobile Apps](functions-bindings-mobile-apps.md)
- [Dış dosya](functions-bindings-external-file.md)
