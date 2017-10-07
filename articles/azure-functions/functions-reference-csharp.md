---
title: "aaaAzure işlevleri C# betik Geliştirici Başvurusu | Microsoft Docs"
description: "Anlamak nasıl toodevelop C# kullanarak Azure işlevleri."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure işlevleri, işlevler, olay işleme, web kancaları, dinamik işlem, sunucusuz mimari"
ms.assetid: f28cda01-15f3-4047-83f3-e89d5728301c
ms.service: functions
ms.devlang: dotnet
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/07/2017
ms.author: donnam
ms.openlocfilehash: 27a8f4eb77497a373ff4031539e2e930585e48e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-c-script-developer-reference"></a>Azure işlevleri C# betik Geliştirici Başvurusu
> [!div class="op_single_selector"]
> * [C# betiği](functions-reference-csharp.md)
> * [F # betiği](functions-reference-fsharp.md)
> * [Node.js](functions-reference-node.md)
>
>

Merhaba C# betik deneyimi Azure işlevleri için Azure WebJobs SDK hello üzerinde temel alır. C# işlevinizi yöntem bağımsız değişkenleri ile verileri akar. Bağımsız değişken adları belirtilir `function.json`, ve işlevi Günlükçü ve iptal belirteçleri hello gibi işlemler erişmek için önceden tanımlanmış adları vardır.

Bu makalede, zaten hello okuduğunuz varsayılır [Azure işlevleri Geliştirici Başvurusu](functions-reference.md).

Sınıf kitaplıkları C# kullanma hakkında bilgi için bkz: [Azure işlevlerini kullanarak .NET sınıf kitaplıkları](functions-dotnet-class-library.md).

## <a name="how-csx-works"></a>.Csx nasıl çalışır?
Merhaba `.csx` biçimi toowrite daha az "ortak" ve yalnızca bir C# işlevi yazma odağı sağlar. Tüm derleme başvurularını ve ad alanları hello dosya hello başında her zamanki gibi içerir. Her şeyi bir ad alanı ve sınıf kaydırma yerine, yalnızca tanımlayan bir `Run` yöntemi. Tooinclude gerekiyorsa tüm sınıflar örneği toodefine eski CLR nesnesi (POCO) nesneleri, bir sınıf içinde içerebilir düz için aynı dosyayı hello.   

## <a name="binding-tooarguments"></a>Tooarguments bağlama
Merhaba çeşitli bağlamaları olan ilişkili tooa C# işlevi hello aracılığıyla `name` hello özelliğinde *function.json* yapılandırma. Her bağlama desteklenen türlerinden; yine de sahip istiyor musunuz? Örneğin, bir blob tetikleyici bir dize, bir POCO veya bir CloudBlockBlob destekleyebilir. desteklenen hello türleri her bağlama hello başvurusunu belgelenmiştir. Bir POCO nesnesi bir'Set ' yordamı her bir özellik için tanımlanmış olması gerekir.

```csharp
public static void Run(string myBlob, out MyClass myQueueItem)
{
    log.Verbose($"C# Blob trigger function processed: {myBlob}");
    myQueueItem = new MyClass() { Id = "myid" };
}

public class MyClass
{
    public string Id { get; set; }
}
```

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="using-method-return-value-for-output-binding"></a>Yöntemin dönüş değeri için çıktı bağlama işlemini kullanma

Merhaba adını kullanarak bir yöntemin dönüş değeri bir çıktı bağlaması için kullanabileceğiniz `$return` içinde *function.json*:

```json
{
    "type": "queue",
    "direction": "out",
    "name": "$return",
    "queueName": "outqueue",
    "connection": "MyStorageConnectionString",
}
```

```csharp
public static string Run(string input, TraceWriter log)
{
    return input;
}
```

## <a name="writing-multiple-output-values"></a>Birden çok çıktı değerleri yazılıyor

birden çok değer tooan toowrite çıkış bağlama, hello kullan [ `ICollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) veya [ `IAsyncCollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) türleri. Bu tür hello yöntemi tamamlandığında, çıkış yazılı toohello bağlama olan salt yazılır koleksiyonlarıdır.

Bu örnek kullanarak birden çok sıra iletileri Yazar `ICollector`:

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a>Günlüğe kaydetme
türünde bir bağımsız değişken içeriyor, toolog C# tooyour akışlı günlükleri çıkış `TraceWriter`. Bu ad öneririz `log`. Kullanmaktan kaçının `Console.Write` Azure işlevlerinde. 

`TraceWriter`Hello tanımlanan [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs). Merhaba günlük düzeyi için `TraceWriter` yapılandırılabilir [konak\.json].

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a>Zaman uyumsuz
toomake zaman uyumsuz, bir işlev kullanmak hello `async` anahtar sözcüğü ve return bir `Task` nesnesi.

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a>İptal belirteci
Bazı işlemler normal şekilde kapatılmasını gerektirir. Her zaman, toohandle kapama istekleri, istediğiniz durumlarda kilitlenen işleyebileceği en iyi toowrite kod olsa tanımladığınız bir [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) bağımsız değişken belirtilmiş.  A `CancellationToken` bir ana bilgisayar kapatma tetiklenir toosignal sağlanır.

```csharp
public async static Task ProcessQueueMessageAsyncCancellationToken(
        string blobName,
        Stream blobInput,
        Stream blobOutput,
        CancellationToken token)
    {
        await blobInput.CopyToAsync(blobOutput, 4096, token);
    }
```

## <a name="importing-namespaces"></a>Ad alanlarını alma
Tooimport ad alanları ihtiyacınız varsa, her zamanki gibi hello ile bunu yapabilirsiniz `using` yan tümcesi.

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

Merhaba şu ad alanlarından otomatik olarak içe aktarılır ve bu nedenle isteğe bağlıdır:

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a>Dış derlemelere başvurma
Hello kullanarak Framework derlemeler için başvurular ekleyin `#r "AssemblyName"` yönergesi.

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

Merhaba aşağıdaki derlemeler otomatik barındırma ortamı hello Azure işlevleri tarafından eklenir:

* `mscorlib`
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* `System.Net.Http.Formatting`

Merhaba aşağıdaki derlemeler basit adıyla başvurulabilir (örneğin, `#r "AssemblyName"`):

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a>Özel derlemelere başvurma

özel bir derlemeyi tooreference, kullanma ya da bir *paylaşılan* derleme veya *özel* derleme:
- Paylaşılan derlemeler işlevi uygulamasında tüm işlevleri arasında paylaşılır. tooreference özel bir derlemeyi karşıya yükleme hello derleme tooyour işlev uygulaması gibi bir `bin` hello işlevi uygulama kök klasöründe. 
- Özel derlemeler verilen işlevin bağlam parçası olan ve dışarıdan farklı sürümlerini destekler. Özel derlemeler karşıya yüklenebilir içinde bir `bin` hello işlevi dizin klasöründe. Merhaba dosya adı gibi kullanarak başvuru `#r "MyAssembly.dll"`. 

Nasıl tooupload dosyaları tooyour işlevi klasörü hakkında daha fazla bilgi için paket Yönetimi bölümünde aşağıdaki hello bakın.

### <a name="watched-directories"></a>İzlenen dizinleri

Merhaba işlevi komut dosyasını içeren hello dizini otomatik olarak değişiklikleri tooassemblies için izlenen. derleme değişiklikleri diğer dizinlerde toowatch eklemek bunları toohello `watchDirectories` listesinde [konak\.json].

## <a name="using-nuget-packages"></a>NuGet paketlerini kullanma
bir C# işlevinde toouse NuGet paketlerini yüklemek bir *project.json* toohello işlevin klasörü hello işlevi uygulamanın dosya sisteminde dosya. İşte bir örnek *project.json* bir başvuru tooMicrosoft.ProjectOxford.Face sürüm 1.1.0 ekler dosyası:

```json
{
  "frameworks": {
    "net46":{
      "dependencies": {
        "Microsoft.ProjectOxford.Face": "1.1.0"
      }
    }
   }
}
```

Hello .NET Framework 4.6 desteklenir yalnızca, bu nedenle olduğundan emin olun, *project.json* dosyayı belirtir `net46` aşağıda gösterildiği gibi.

Karşıya yüklediğiniz zaman bir *project.json* dosya, hello çalışma zamanı hello paketleri alır ve başvurular toohello paket derlemeler otomatik olarak ekler. Tooadd gerekmeyen `#r "AssemblyName"` yönergeleri. Merhaba NuGet paketlerini içinde tanımlanan toouse hello türleri eklemek gerekli hello `using` deyimleri tooyour *run.csx* dosyası 

Merhaba işlevleri çalışma zamanında NuGet restore çalışır karşılaştırarak `project.json` ve `project.lock.json`. Varsa hello dosyaların tarih ve saat damgaları hello **sağlamadığı** eşleşme NuGet geri yükleme çalıştırır ve NuGet yüklemeleri paketler güncelleştirilir. Ancak, Merhaba, tarih ve saat damgaları hello dosyaların **yapmak** eşleşme, NuGet, bir geri yükleme gerçekleştirmez. Bu nedenle, `project.lock.json` NuGet tooskip paket geri yüklemesi neden olarak kullanılmamalıdır. Merhaba kilit dağıtma tooavoid dosya, hello eklemek `project.lock.json` toohello `.gitignore` dosya.

toouse özel bir NuGet akışı belirtin, akış hello bir *Nuget.Config* hello işlev uygulaması kök dosyasında. Daha fazla bilgi için bkz: [NuGet yapılandırma davranışı](/nuget/consume-packages/configuring-nuget-behavior).

### <a name="using-a-projectjson-file"></a>Project.json dosyası kullanma
1. Merhaba işlevi hello Azure portalını açın. Merhaba sekmesini görüntüler hello paket yükleme çıktı günlüğe kaydeder.
2. tooupload project.json dosyası hello açıklanan hello yöntemlerden birini kullanın [nasıl tooupdate işlev uygulama dosyaları](functions-reference.md#fileupdate) hello Azure işlevleri Geliştirici Başvurusu konu başlığı.
3. Merhaba sonra *project.json* dosyasının yüklendiği, işlevinizi örnekte aşağıdaki hello gibi bir çıktı günlük akış bakın:

```
2016-04-04T19:02:48.745 Restoring packages.
2016-04-04T19:02:48.745 Starting NuGet restore
2016-04-04T19:02:50.183 MSBuild auto-detection: using msbuild version '14.0' from 'D:\Program Files (x86)\MSBuild\14.0\bin'.
2016-04-04T19:02:50.261 Feeds used:
2016-04-04T19:02:50.261 C:\DWASFiles\Sites\facavalfunctest\LocalAppData\NuGet\Cache
2016-04-04T19:02:50.261 https://api.nuget.org/v3/index.json
2016-04-04T19:02:50.261
2016-04-04T19:02:50.511 Restoring packages for D:\home\site\wwwroot\HttpTriggerCSharp1\Project.json...
2016-04-04T19:02:52.800 Installing Newtonsoft.Json 6.0.8.
2016-04-04T19:02:52.800 Installing Microsoft.ProjectOxford.Face 1.1.0.
2016-04-04T19:02:57.095 All packages are compatible with .NETFramework,Version=v4.6.
2016-04-04T19:02:57.189
2016-04-04T19:02:57.189
2016-04-04T19:02:57.455 Packages restored.
```

## <a name="environment-variables"></a>Ortam değişkenleri
tooget bir ortam değişkeni veya kullanan bir uygulama ayarı değeri `System.Environment.GetEnvironmentVariable`, aşağıdaki kod örneğine hello gösterildiği gibi:

```csharp
public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    log.Info(GetEnvironmentVariable("AzureWebJobsStorage"));
    log.Info(GetEnvironmentVariable("WEBSITE_SITE_NAME"));
}

public static string GetEnvironmentVariable(string name)
{
    return name + ": " +
        System.Environment.GetEnvironmentVariable(name, EnvironmentVariableTarget.Process);
}
```

## <a name="reusing-csx-code"></a>.Csx kodu yeniden kullanma
Sınıfları ve diğer tanımlanan yöntemler kullanabilirsiniz *.csx* dosyalar, *run.csx* dosya. kullanan, toodo `#load` yönergeleri, *run.csx* dosya. Günlüğe kaydetme yordamını aşağıdaki örneğine hello adlı `MyLogger` içinde paylaşılan *myLogger.csx* ve içine yüklenen *run.csx* hello kullanarak `#load` yönergesi:

Örnek *run.csx*:

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

Örnek *mylogger.csx*:

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

Paylaşılan kullanarak *.csx* toostrongly istediğinizde genel bir desen, bağımsız değişkenleri arasında bir POCO nesnesi kullanarak işlevleri yazın. Aşağıdaki Basitleştirilmiş örneğine hello adlı bir POCO nesnesi bir HTTP tetikleyicisi ve sıra tetikleyici paylaşmak `Order` toostrongly türü hello sipariş verileri:

Örnek *run.csx* HTTP tetikleyicisi için:

```cs
#load "..\shared\order.csx"

using System.Net;

public static async Task<HttpResponseMessage> Run(Order req, IAsyncCollector<Order> outputQueueItem, TraceWriter log)
{
    log.Info("C# HTTP trigger function received an order.");
    log.Info(req.ToString());
    log.Info("Submitting tooprocessing queue.");

    if (req.orderId == null)
    {
        return new HttpResponseMessage(HttpStatusCode.BadRequest);
    }
    else
    {
        await outputQueueItem.AddAsync(req);
        return new HttpResponseMessage(HttpStatusCode.OK);
    }
}
```

Örnek *run.csx* sıra tetikleyici için:

```cs
#load "..\shared\order.csx"

using System;

public static void Run(Order myQueueItem, out Order outputQueueItem,TraceWriter log)
{
    log.Info($"C# Queue trigger function processed order...");
    log.Info(myQueueItem.ToString());

    outputQueueItem = myQueueItem;
}
```

Örnek *order.csx*:

```cs
public class Order
{
    public string orderId {get; set; }
    public string custName {get; set;}
    public string custAddress {get; set;}
    public string custEmail {get; set;}
    public string cartId {get; set; }

    public override String ToString()
    {
        return "\n{\n\torderId : " + orderId +
                  "\n\tcustName : " + custName +             
                  "\n\tcustAddress : " + custAddress +             
                  "\n\tcustEmail : " + custEmail +             
                  "\n\tcartId : " + cartId + "\n}";             
    }
}
```

Göreli bir yol ile Merhaba kullanabilirsiniz `#load` yönergesi:

* `#load "mylogger.csx"`Merhaba işlevi klasöründe bir dosya yükler.
* `#load "loadedfiles\mylogger.csx"`Merhaba işlevi klasöründe bulunan bir dosya yükler.
* `#load "..\shared\mylogger.csx"`aynı düzeydeki hello işlevi klasör, başka bir deyişle, hello bir klasörde bulunan bir dosya yükler doğrudan altında *wwwroot*.

Merhaba `#load` yönergesi çalışır yalnızca *.csx* (C# betik) dosyaları değil *.cs* dosyaları.

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a>Kesinlik temelli bağlamaları aracılığıyla çalışma zamanında bağlama

C# ve diğer .NET dilleri kullanabileceğiniz bir [kesinlik temelli](https://en.wikipedia.org/wiki/Imperative_programming) karşılıklı toohello olarak bağlama düzeni [ *bildirim temelli* ](https://en.wikipedia.org/wiki/Declarative_programming) bağlama *function.json*. Kesinlik temelli bağlama bağlama parametreleri tasarım yerine çalışma zamanında hesaplanan toobe gerektiğinde kullanışlıdır. Bu desen ile toosupported giriş bağlamak ve bağlama üzerinde-çalışma sırasında işlevi kodunuzda çıktı.

Aşağıdaki gibi bağlama kesinliği tanımlayın:

- **Sağlamadığı** bir girişe dahil *function.json* , istenen kesinlik temelli bağlamaları için.
- Giriş parametresi geçişinde [ `Binder binder` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) veya [ `IBinder binder` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).
- C# düzeni tooperform hello veri bağlama aşağıdaki hello kullanın.

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

Burada `BindingTypeAttribute` , bağlama tanımlar hello .NET özniteliği ve `T` Merhaba, bağlama türü tarafından desteklenen giriş veya çıkış türü değil. `T`Ayrıca olamaz bir `out` parametre türü (gibi `out JObject`). Örneğin, Mobile Apps Tablo Bağlama destekler çıktı [altı türleri çıktı](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), ancak yalnızca kullanabilirsiniz [ICollector<T> ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) veya [IAsyncCollector<T> ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs)için `T`.

Aşağıdaki örnek kod hello oluşturur bir [depolama blobu çıktı bağlama](functions-bindings-storage-blob.md#using-a-blob-output-binding) blob ile çalışma zamanında tanımlanan yol sonra bir dize toohello blob yazar.

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;

public static async Task Run(string input, Binder binder)
{
    using (var writer = await binder.BindAsync<TextWriter>(new BlobAttribute("samples-output/path")))
    {
        writer.Write("Hello World!!");
    }
}
```

[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) hello tanımlar [depolama blobu](functions-bindings-storage-blob.md) giriş veya çıkış bağlamayı ve [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) desteklenen çıktı bağlama türü.
Olduğu şekilde hello kodu hello depolama hesabı bağlantı dizesi için hello varsayılan uygulama ayarı alır (olduğu `AzureWebJobsStorage`). Bir özel uygulama ayarı toouse ekleyerek belirtebilirsiniz [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) ve hello özniteliği diziye geçirme `BindAsync<T>()`. Örneğin,

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;

public static async Task Run(string input, Binder binder)
{
    var attributes = new Attribute[]
    {    
        new BlobAttribute("samples-output/path"),
        new StorageAccountAttribute("MyStorageAccount")
    };

    using (var writer = await binder.BindAsync<TextWriter>(attributes))
    {
        writer.Write("Hello World!");
    }
}
```

Merhaba aşağıdaki tabloda her bağlama türü ve hello tanımlı paketler için hello .NET öznitelikleri listeler.

> [!div class="mx-codeBreakAll"]
| Bağlama | Öznitelik | Başvuru ekleme |
|------|------|------|
| Cosmos DB | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| Event Hubs | [`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs) | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| Mobile Apps | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| Notification Hubs | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| Service Bus | [`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs) | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| Depolama sırası | [`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Depolama blobu | [`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Depolama tablosu | [`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Twilio | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için kaynakları aşağıdaki hello bakın:

* [Azure İşlevleri için En İyi Uygulamalar](functions-best-practices.md)
* [Azure İşlevleri geliştirici başvurusu](functions-reference.md)
* [Azure işlevleri F # Geliştirici Başvurusu](functions-reference-fsharp.md)
* [Azure işlevleri NodeJS Geliştirici Başvurusu](functions-reference-node.md)
* [Azure işlevleri Tetikleyicileri ve bağlamaları](functions-triggers-bindings.md)

[ana bilgisayar\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
