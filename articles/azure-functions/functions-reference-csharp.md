---
title: "Azure işlevleri C# betik Geliştirici Başvurusu"
description: "C# betik kullanarak Azure işlevleri geliştirmek nasıl anlayın."
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
editor: 
tags: 
keywords: "azure işlevleri, işlevler, olay işleme, web kancaları, dinamik işlem, sunucusuz mimari"
ms.service: functions
ms.devlang: dotnet
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 12/12/2017
ms.author: glenga
ms.openlocfilehash: b6b18f79b0ef50c30335218ef45ba6ed932cb586
ms.sourcegitcommit: 99d29d0aa8ec15ec96b3b057629d00c70d30cfec
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="azure-functions-c-script-csx-developer-reference"></a>Azure işlevleri C# betik (.csx) Geliştirici Başvurusu

<!-- When updating this article, make corresponding changes to any duplicate content in functions-dotnet-class-library.md -->

Bu makalede Azure işlevleri C# kod kullanarak geliştirme için bir giriş olduğunu (*.csx*).

Azure işlevleri, C# ve programlama dilleri C# betik destekler. Yönergeler için arıyorsanız [C# kullanarak bir Visual Studio sınıf kitaplığı projesinde](functions-develop-vs.md), bkz: [C# Geliştirici Başvurusu](functions-dotnet-class-library.md).

Bu makalede, zaten okuduğunuz varsayılır [Azure işlevleri Geliştirici Kılavuzu](functions-reference.md).

## <a name="how-csx-works"></a>.Csx nasıl çalışır?

Azure işlevleri için C# betik deneyimi dayanır [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/wiki/Introduction). C# işlevinizi yöntem bağımsız değişkenleri ile verileri akar. Bağımsız değişken adları içinde belirtilen bir `function.json` dosya ve orada önceden tanımlanmış şey erişmek için adları işlevi Günlükçü ve iptal belirteçleri ister.

*.Csx* biçimi daha az "ortak" yazın ve yalnızca bir C# işlevi yazma odaklanmanıza olanak tanır. Her şeyi bir ad alanı ve sınıf kaydırma yerine, yalnızca tanımlayan bir `Run` yöntemi. Her zamanki gibi tüm derleme başvurularını ve dosya başına ad alanları içerir.

Bir işlev uygulamanın *.csx* dosyaları örneği başlatıldığında derlenir. Bu derleme adımı soğuk başlangıç betiği C# sınıfı kitaplıklar karşılaştırıldığında C# işlevleri için uzun sürebilir gibi işlemler anlamına gelir. Bu derleme ayrıca C# sınıfı kitaplıklar değildir; ancak C# betik işlevleri neden Azure Portalı'nda düzenlenebilir bir adımdır.

## <a name="binding-to-arguments"></a>Bağımsız değişkenler bağlama

Giriş veya çıkış verisi C# betik işlevi parametresi bağlı `name` özelliğinde *function.json* yapılandırma dosyası. Aşağıdaki örnekte gösterildiği bir *function.json* dosya ve *run.csx* dosya sırası tetiklenen bir işlev. Sıra iletiden verileri alan parametresi adlı `myQueueItem` değeri olduğu için `name` özelliği.

```json
{
    "disabled": false,
    "bindings": [
        {
            "type": "queueTrigger",
            "direction": "in",
            "name": "myQueueItem",
            "queueName": "myqueue-items",
            "connection":"MyStorageConnectionAppSetting"
        }
    ]
}
```

```csharp
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Queue;
using System;

public static void Run(CloudQueueMessage myQueueItem, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem.AsString}");
}
```

`#r` Deyimi açıklanmıştır [bu makalenin ilerisinde yer](#referencing-external-assemblies).

## <a name="supported-types-for-bindings"></a>Bağlamaları için desteklenen türler

Her bağlama desteklenen türlerinden; yine de sahip istiyor musunuz? Örneğin, bir blob tetikleyici bir POCO parametresi bir dize parametresi ile kullanılabilir bir `CloudBlockBlob` parametresi ya da birkaç diğer hiçbirini desteklenen türler. [Blob bağlamaları için bağlama başvurusu makalesinde](functions-bindings-storage-blob.md#trigger---usage) blob Tetikleyiciler için desteklenen tüm listeleri parametre türleri. Daha fazla bilgi için bkz: [Tetikleyicileri ve bağlamaları](functions-triggers-bindings.md) ve [bağlama başvuru belgeleri her bağlama türü için](functions-triggers-bindings.md#next-steps).

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="referencing-custom-classes"></a>Başvuruda bulunan özel sınıflar

Özel bir düz eski CLR nesnesi (POCO) sınıf kullanmanız gerekiyorsa, aynı dosya içinde sınıf tanımını dahil edebilir veya ayrı bir dosyaya yerleştirin.

Aşağıdaki örnekte gösterildiği bir *run.csx* POCO sınıf tanımını içeren örnek.

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

POCO sınıfı, bir'Set ' yordamı her bir özellik için tanımlanmış olması gerekir.

## <a name="reusing-csx-code"></a>.Csx kodu yeniden kullanma

Sınıfları ve diğer tanımlanan yöntemler kullanabilirsiniz *.csx* dosyalar, *run.csx* dosya. Bunu yapmak için kullanmak `#load` yönergeleri, *run.csx* dosya. Aşağıdaki örnekte, bir günlük yordam adlı `MyLogger` içinde paylaşılan *myLogger.csx* ve içine yüklenen *run.csx* kullanarak `#load` yönergesi:

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

Paylaşılan kullanarak *.csx* dosyasıdır genel bir desen kesinlikle işlevleri tarafından arasında bir POCO nesnesi kullanılarak iletilen thet veri türü istediğinizde. Aşağıdaki basit örnekte, bir HTTP tetikleyicisi ve sıra tetikleyici adlı bir POCO nesne paylaşmak `Order` kesinlikle sipariş veri türü için:

Örnek *run.csx* HTTP tetikleyicisi için:

```cs
#load "..\shared\order.csx"

using System.Net;

public static async Task<HttpResponseMessage> Run(Order req, IAsyncCollector<Order> outputQueueItem, TraceWriter log)
{
    log.Info("C# HTTP trigger function received an order.");
    log.Info(req.ToString());
    log.Info("Submitting to processing queue.");

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

Göreli bir yol ile kullanabileceğiniz `#load` yönergesi:

* `#load "mylogger.csx"`işlev klasöründe bir dosya yükler.
* `#load "loadedfiles\mylogger.csx"`işlev klasöründe bulunan bir dosya yükler.
* `#load "..\shared\mylogger.csx"`diğer bir deyişle, işlevi klasör ile aynı düzeyde bir klasörde bulunan bir dosya yükler doğrudan altında *wwwroot*.

`#load` Yönergesi çalışır yalnızca *.csx* dosyaları değil *.cs* dosyaları.

## <a name="binding-to-method-return-value"></a>Bağlama yöntemini dönüş değeri

Adını kullanarak bir yöntemin dönüş değeri bir çıktı bağlaması için kullanabileceğiniz `$return` içinde *function.json*:

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

Bir çıkış bağlaması birden çok değeri yazmak için kullanın [ `ICollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) veya [ `IAsyncCollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) türleri. Bu tür yöntemi tamamlandığında, çıkış bağlama yazılan salt yazılır koleksiyonlarıdır.

Bu örnek, aynı kullanarak sıra birden çok sıraya ileti yazar `ICollector`:

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a>Günlüğe kaydetme

Çıkış akış günlüklerinizi C# oturum açmak için türünde bir bağımsız değişken dahil `TraceWriter`. Bu ad öneririz `log`. Kullanmaktan kaçının `Console.Write` Azure işlevlerinde. 

`TraceWriter`tanımlanan [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs). Günlük düzeyi için `TraceWriter` yapılandırılabilir [host.json](functions-host-json.md).

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

> [!NOTE]
> Yerine kullanabileceğiniz yeni bir günlük framework hakkında bilgi için `TraceWriter`, bkz: [yazma günlüklerini C# işlevlerde](functions-monitoring.md#write-logs-in-c-functions) içinde **İzleyici Azure işlevleri** makale.

## <a name="async"></a>Async

Bir işlev zaman uyumsuz hale getirmek için kullanmak `async` anahtar sözcüğü ve return bir `Task` nesnesi.

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096);
}
```

## <a name="cancellation-tokens"></a>İptal belirteçleri

Bazı işlemler normal şekilde kapatılmasını gerektirir. Her zaman kilitlenen işleyebilir kod yazmak en iyi olmakla birlikte, kapatma isteklerini işlemek istediğiniz durumlarda tanımlayan bir [CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) bağımsız değişken belirtilmiş.  A `CancellationToken` bir ana bilgisayar kapatma tetiklenir göstermek için sağlanmıştır.

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

Ad alanları almanız gerekiyorsa, bu nedenle olarak normal, ile yapabileceğiniz `using` yan tümcesi.

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

Şu ad alanlarından otomatik olarak içe aktarılır ve bu nedenle isteğe bağlıdır:

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a>Dış derlemelere başvurma

Kullanarak Framework derlemeler için başvurular ekleyin `#r "AssemblyName"` yönergesi.

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

Aşağıdaki derlemeler barındırma ortamı Azure işlevleri tarafından otomatik olarak eklenir:

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

Aşağıdaki derlemeler basit adıyla başvurulabilir (örneğin, `#r "AssemblyName"`):

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a>Özel derlemelere başvurma

Özel bir derlemeyi başvurmak için ya da kullanabilirsiniz bir *paylaşılan* derleme veya *özel* derleme:
- Paylaşılan derlemeler işlevi uygulamasında tüm işlevleri arasında paylaşılır. Özel bir derlemeyi başvurmak için işlevi uygulamanızı derlemeye gibi yüklemeniz bir `bin` işlevi uygulama kök klasöründe. 
- Özel derlemeler verilen işlevin bağlam parçası olan ve dışarıdan farklı sürümlerini destekler. Özel derlemeler karşıya yüklenebilir içinde bir `bin` işlevi dizin klasöründe. Dosya adı gibi kullanarak derlemeler başvuru `#r "MyAssembly.dll"`. 

Bölümüne bakarak işlevi klasörünüze dosyaları karşıya yükleme hakkında daha fazla bilgi için [Yönetim paketini](#using-nuget-packages).

### <a name="watched-directories"></a>İzlenen dizinleri

İşlev komut dosyasını içeren dizine değişiklikler derlemeler için otomatik olarak izlenen. Diğer dizinlerde derleme değişiklikleri izlemek için bunları Ekle `watchDirectories` listesinde [host.json](functions-host-json.md).

## <a name="using-nuget-packages"></a>NuGet paketlerini kullanma

C# işlevinde NuGet paketlerini kullanmak için karşıya bir *project.json* dosyasını işlevin klasöre işlevi uygulamanın dosya sistemi. İşte bir örnek *project.json* Microsoft.ProjectOxford.Face sürüm 1.1.0 bir başvuru ekler dosyası:

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

Azure'da 1.x İşlevler, yalnızca .NET Framework 4.6 desteklenir, dolayısıyla olduğundan emin olun, *project.json* dosyayı belirtir `net46` aşağıda gösterildiği gibi.

Karşıya yüklediğiniz zaman bir *project.json* dosya, çalışma zamanı paketleri alır ve paketi derleme başvuruları otomatik olarak ekler. Eklemeniz gerekmez `#r "AssemblyName"` yönergeleri. NuGet paketlerinde tanımlanan türlerin kullanmak için; yalnızca gerekli Ekle `using` deyimleri için *run.csx* dosya. 

NuGet restore işlevleri çalışma zamanı'nda çalışır karşılaştırarak `project.json` ve `project.lock.json`. Varsa dosyaların tarih ve saat Damgalar **sağlamadığı** eşleşme NuGet geri yükleme çalıştırır ve NuGet yüklemeleri paketler güncelleştirilir. Ancak, dosyaların tarih ve saat Damgalar **yapmak** eşleşme, NuGet, bir geri yükleme gerçekleştirmez. Bu nedenle, `project.lock.json` NuGet paket geri yüklemesi atlamak neden olur, dağıtılmalıdır değil. Kilit dosyası dağıtma önlemek için add `project.lock.json` için `.gitignore` dosya.

Akış özel bir NuGet kullanmak için akışta belirtin bir *Nuget.Config* işlev uygulaması kök dosyasında. Daha fazla bilgi için bkz: [NuGet yapılandırma davranışı](/nuget/consume-packages/configuring-nuget-behavior).

### <a name="using-a-projectjson-file"></a>Project.json dosyası kullanma

1. Azure portalında açma işlevi. Günlükleri sekmesinde paket yükleme çıktısını görüntüler.
2. Project.json dosyası karşıya yüklemek için açıklanan yöntemlerden birini kullanın [işlevi uygulama dosyaları güncelleştirmek nasıl](functions-reference.md#fileupdate) Azure işlevleri Geliştirici Başvurusu konu başlığı.
3. Sonra *project.json* dosyasının yüklendiği, işlevinizi aşağıdaki örnekte gibi bir çıktı günlük akış bakın:

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

Bir ortam değişkeni veya ayar değeri bir uygulamayı almak için `System.Environment.GetEnvironmentVariable`aşağıdaki kod örneğinde gösterildiği gibi:

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

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime"></a>Çalışma zamanında bağlama

C# ve diğer .NET dilleri kullanabileceğiniz bir [kesinlik temelli](https://en.wikipedia.org/wiki/Imperative_programming) tersine düzeni, bağlama [ *bildirim temelli* ](https://en.wikipedia.org/wiki/Declarative_programming) bağlama *function.json*. Kesinlik temelli bağlama bağlama parametreleri tasarım yerine çalışma zamanında hesaplanması gerektiğinde kullanışlıdır. Bu desen ile desteklenen giriş ve çıkış bağlamaları üzerinde-çalışma sırasında işlevi kodunuzda bağlayabilirsiniz.

Aşağıdaki gibi bağlama kesinliği tanımlayın:

- **Sağlamadığı** bir girişe dahil *function.json* , istenen kesinlik temelli bağlamaları için.
- Giriş parametresi geçişinde [ `Binder binder` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) veya [ `IBinder binder` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).
- Veri bağlama gerçekleştirmek için aşağıdaki C# düzeni kullanın.

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

`BindingTypeAttribute`bağlama tanımlayan bir .NET özniteliktir ve `T` , bağlama türü tarafından desteklenen bir giriş veya çıkış türü. `T`olamaz bir `out` parametre türü (gibi `out JObject`). Örneğin, Mobile Apps Tablo Bağlama destekler çıktı [altı türleri çıktı](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), ancak yalnızca kullanabilirsiniz [ICollector<T> ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) veya [IAsyncCollector<T> ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs)için `T`.

### <a name="single-attribute-example"></a>Tek öznitelik örneği

Aşağıdaki kod örneği oluşturur bir [depolama blobu çıktı bağlama](functions-bindings-storage-blob.md#output) blob ile çalışma zamanında tanımlanan yol sonra Yazar bir dize için blob.

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

[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) tanımlar [depolama blobu](functions-bindings-storage-blob.md) giriş veya çıkış bağlamayı ve [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) desteklenen çıktı bağlama türü.

### <a name="multiple-attribute-example"></a>Birden çok öznitelik örneği

Önceki örnekte işlevi uygulamanın ana depolama hesabı bağlantı dizesi için uygulama ayarı alır (olduğu `AzureWebJobsStorage`). Ekleyerek depolama hesabı için kullanılacak bir özel uygulama ayarını belirtebilirsiniz [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) ve öznitelik diziye geçirme `BindAsync<T>()`. Kullanım bir `Binder` parametresi olmayan `IBinder`.  Örneğin:

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

Aşağıdaki tabloda her bağlama türü ve tanımlanmış paketler için .NET öznitelikleri listeler.

> [!div class="mx-codeBreakAll"]
| Bağlama | Öznitelik | Başvuru ekleme |
|------|------|------|
| Cosmos DB | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.CosmosDB/CosmosDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.CosmosDB"` |
| Event Hubs | [`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs) | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| Mobile Apps | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| Notification Hubs | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| Service Bus | [`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs) | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| Depolama kuyruğu | [`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Depolama blobu | [`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Depolama tablosu | [`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Twilio | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |

## <a name="next-steps"></a>Sonraki adımlar

> [!div class="nextstepaction"]
> [Tetikleyicileri ve bağlamaları hakkında daha fazla bilgi edinin](functions-triggers-bindings.md)

> [!div class="nextstepaction"]
> [Azure işlevleri için en iyi uygulamalar hakkında daha fazla bilgi edinin](functions-best-practices.md)
