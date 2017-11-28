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
# <a name="azure-functions-c-script-developer-reference"></a><span data-ttu-id="421d2-104">Azure işlevleri C# betik Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="421d2-104">Azure Functions C# script developer reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="421d2-105">C# betiği</span><span class="sxs-lookup"><span data-stu-id="421d2-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="421d2-106">F # betiği</span><span class="sxs-lookup"><span data-stu-id="421d2-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="421d2-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="421d2-107">Node.js</span></span>](functions-reference-node.md)
>
>

<span data-ttu-id="421d2-108">Merhaba C# betik deneyimi Azure işlevleri için Azure WebJobs SDK hello üzerinde temel alır.</span><span class="sxs-lookup"><span data-stu-id="421d2-108">hello C# script experience for Azure Functions is based on hello Azure WebJobs SDK.</span></span> <span data-ttu-id="421d2-109">C# işlevinizi yöntem bağımsız değişkenleri ile verileri akar.</span><span class="sxs-lookup"><span data-stu-id="421d2-109">Data flows into your C# function via method arguments.</span></span> <span data-ttu-id="421d2-110">Bağımsız değişken adları belirtilir `function.json`, ve işlevi Günlükçü ve iptal belirteçleri hello gibi işlemler erişmek için önceden tanımlanmış adları vardır.</span><span class="sxs-lookup"><span data-stu-id="421d2-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like hello function logger and cancellation tokens.</span></span>

<span data-ttu-id="421d2-111">Bu makalede, zaten hello okuduğunuz varsayılır [Azure işlevleri Geliştirici Başvurusu](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="421d2-111">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

<span data-ttu-id="421d2-112">Sınıf kitaplıkları C# kullanma hakkında bilgi için bkz: [Azure işlevlerini kullanarak .NET sınıf kitaplıkları](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="421d2-112">For information on using C# class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span>

## <a name="how-csx-works"></a><span data-ttu-id="421d2-113">.Csx nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="421d2-113">How .csx works</span></span>
<span data-ttu-id="421d2-114">Merhaba `.csx` biçimi toowrite daha az "ortak" ve yalnızca bir C# işlevi yazma odağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="421d2-114">hello `.csx` format allows you toowrite less "boilerplate" and focus on writing just a C# function.</span></span> <span data-ttu-id="421d2-115">Tüm derleme başvurularını ve ad alanları hello dosya hello başında her zamanki gibi içerir.</span><span class="sxs-lookup"><span data-stu-id="421d2-115">Include any assembly references and namespaces at hello beginning of hello file as usual.</span></span> <span data-ttu-id="421d2-116">Her şeyi bir ad alanı ve sınıf kaydırma yerine, yalnızca tanımlayan bir `Run` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="421d2-116">Instead of wrapping everything in a namespace and class, just define a `Run` method.</span></span> <span data-ttu-id="421d2-117">Tooinclude gerekiyorsa tüm sınıflar örneği toodefine eski CLR nesnesi (POCO) nesneleri, bir sınıf içinde içerebilir düz için aynı dosyayı hello.</span><span class="sxs-lookup"><span data-stu-id="421d2-117">If you need tooinclude any classes, for instance toodefine Plain Old CLR Object (POCO) objects, you can include a class inside hello same file.</span></span>   

## <a name="binding-tooarguments"></a><span data-ttu-id="421d2-118">Tooarguments bağlama</span><span class="sxs-lookup"><span data-stu-id="421d2-118">Binding tooarguments</span></span>
<span data-ttu-id="421d2-119">Merhaba çeşitli bağlamaları olan ilişkili tooa C# işlevi hello aracılığıyla `name` hello özelliğinde *function.json* yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="421d2-119">hello various bindings are bound tooa C# function via hello `name` property in hello *function.json* configuration.</span></span> <span data-ttu-id="421d2-120">Her bağlama desteklenen türlerinden; yine de sahip istiyor musunuz? Örneğin, bir blob tetikleyici bir dize, bir POCO veya bir CloudBlockBlob destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="421d2-120">Each binding has its own supported types; for instance, a blob trigger can support a string, a POCO, or a CloudBlockBlob.</span></span> <span data-ttu-id="421d2-121">desteklenen hello türleri her bağlama hello başvurusunu belgelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="421d2-121">hello supported types are documented in hello reference for each binding.</span></span> <span data-ttu-id="421d2-122">Bir POCO nesnesi bir'Set ' yordamı her bir özellik için tanımlanmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="421d2-122">A POCO object must have a getter and setter defined for each property.</span></span>

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

## <a name="using-method-return-value-for-output-binding"></a><span data-ttu-id="421d2-123">Yöntemin dönüş değeri için çıktı bağlama işlemini kullanma</span><span class="sxs-lookup"><span data-stu-id="421d2-123">Using method return value for output binding</span></span>

<span data-ttu-id="421d2-124">Merhaba adını kullanarak bir yöntemin dönüş değeri bir çıktı bağlaması için kullanabileceğiniz `$return` içinde *function.json*:</span><span class="sxs-lookup"><span data-stu-id="421d2-124">You can use a method return value for an output binding, by using hello name `$return` in *function.json*:</span></span>

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

## <a name="writing-multiple-output-values"></a><span data-ttu-id="421d2-125">Birden çok çıktı değerleri yazılıyor</span><span class="sxs-lookup"><span data-stu-id="421d2-125">Writing multiple output values</span></span>

<span data-ttu-id="421d2-126">birden çok değer tooan toowrite çıkış bağlama, hello kullan [ `ICollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) veya [ `IAsyncCollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) türleri.</span><span class="sxs-lookup"><span data-stu-id="421d2-126">toowrite multiple values tooan output binding, use hello [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) types.</span></span> <span data-ttu-id="421d2-127">Bu tür hello yöntemi tamamlandığında, çıkış yazılı toohello bağlama olan salt yazılır koleksiyonlarıdır.</span><span class="sxs-lookup"><span data-stu-id="421d2-127">These types are write-only collections that are written toohello output binding when hello method completes.</span></span>

<span data-ttu-id="421d2-128">Bu örnek kullanarak birden çok sıra iletileri Yazar `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="421d2-128">This example writes multiple queue messages using `ICollector`:</span></span>

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a><span data-ttu-id="421d2-129">Günlüğe kaydetme</span><span class="sxs-lookup"><span data-stu-id="421d2-129">Logging</span></span>
<span data-ttu-id="421d2-130">türünde bir bağımsız değişken içeriyor, toolog C# tooyour akışlı günlükleri çıkış `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="421d2-130">toolog output tooyour streaming logs in C#, include an argument of type `TraceWriter`.</span></span> <span data-ttu-id="421d2-131">Bu ad öneririz `log`.</span><span class="sxs-lookup"><span data-stu-id="421d2-131">We recommend that you name it `log`.</span></span> <span data-ttu-id="421d2-132">Kullanmaktan kaçının `Console.Write` Azure işlevlerinde.</span><span class="sxs-lookup"><span data-stu-id="421d2-132">Avoid using `Console.Write` in Azure Functions.</span></span> 

<span data-ttu-id="421d2-133">`TraceWriter`Hello tanımlanan [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span><span class="sxs-lookup"><span data-stu-id="421d2-133">`TraceWriter` is defined in hello [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span></span> <span data-ttu-id="421d2-134">Merhaba günlük düzeyi için `TraceWriter` yapılandırılabilir [konak\.json].</span><span class="sxs-lookup"><span data-stu-id="421d2-134">hello log level for `TraceWriter` can be configured in [host\.json].</span></span>

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a><span data-ttu-id="421d2-135">Zaman uyumsuz</span><span class="sxs-lookup"><span data-stu-id="421d2-135">Async</span></span>
<span data-ttu-id="421d2-136">toomake zaman uyumsuz, bir işlev kullanmak hello `async` anahtar sözcüğü ve return bir `Task` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="421d2-136">toomake a function asynchronous, use hello `async` keyword and return a `Task` object.</span></span>

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a><span data-ttu-id="421d2-137">İptal belirteci</span><span class="sxs-lookup"><span data-stu-id="421d2-137">Cancellation Token</span></span>
<span data-ttu-id="421d2-138">Bazı işlemler normal şekilde kapatılmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="421d2-138">Some operations require graceful shutdown.</span></span> <span data-ttu-id="421d2-139">Her zaman, toohandle kapama istekleri, istediğiniz durumlarda kilitlenen işleyebileceği en iyi toowrite kod olsa tanımladığınız bir [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) bağımsız değişken belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="421d2-139">While it's always best toowrite code that can handle crashing,  in cases where you want toohandle graceful shutdown requests, you define a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) typed argument.</span></span>  <span data-ttu-id="421d2-140">A `CancellationToken` bir ana bilgisayar kapatma tetiklenir toosignal sağlanır.</span><span class="sxs-lookup"><span data-stu-id="421d2-140">A `CancellationToken` is provided toosignal that a host shutdown is triggered.</span></span>

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

## <a name="importing-namespaces"></a><span data-ttu-id="421d2-141">Ad alanlarını alma</span><span class="sxs-lookup"><span data-stu-id="421d2-141">Importing namespaces</span></span>
<span data-ttu-id="421d2-142">Tooimport ad alanları ihtiyacınız varsa, her zamanki gibi hello ile bunu yapabilirsiniz `using` yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="421d2-142">If you need tooimport namespaces, you can do so as usual, with hello `using` clause.</span></span>

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="421d2-143">Merhaba şu ad alanlarından otomatik olarak içe aktarılır ve bu nedenle isteğe bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="421d2-143">hello following namespaces are automatically imported and are therefore optional:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a><span data-ttu-id="421d2-144">Dış derlemelere başvurma</span><span class="sxs-lookup"><span data-stu-id="421d2-144">Referencing External Assemblies</span></span>
<span data-ttu-id="421d2-145">Hello kullanarak Framework derlemeler için başvurular ekleyin `#r "AssemblyName"` yönergesi.</span><span class="sxs-lookup"><span data-stu-id="421d2-145">For framework assemblies, add references by using hello `#r "AssemblyName"` directive.</span></span>

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="421d2-146">Merhaba aşağıdaki derlemeler otomatik barındırma ortamı hello Azure işlevleri tarafından eklenir:</span><span class="sxs-lookup"><span data-stu-id="421d2-146">hello following assemblies are automatically added by hello Azure Functions hosting environment:</span></span>

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

<span data-ttu-id="421d2-147">Merhaba aşağıdaki derlemeler basit adıyla başvurulabilir (örneğin, `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="421d2-147">hello following assemblies may be referenced by simple-name (for example, `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a><span data-ttu-id="421d2-148">Özel derlemelere başvurma</span><span class="sxs-lookup"><span data-stu-id="421d2-148">Referencing custom assemblies</span></span>

<span data-ttu-id="421d2-149">özel bir derlemeyi tooreference, kullanma ya da bir *paylaşılan* derleme veya *özel* derleme:</span><span class="sxs-lookup"><span data-stu-id="421d2-149">tooreference a custom assembly, you can use either a *shared* assembly or a *private* assembly:</span></span>
- <span data-ttu-id="421d2-150">Paylaşılan derlemeler işlevi uygulamasında tüm işlevleri arasında paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="421d2-150">Shared assemblies are shared across all functions within a function app.</span></span> <span data-ttu-id="421d2-151">tooreference özel bir derlemeyi karşıya yükleme hello derleme tooyour işlev uygulaması gibi bir `bin` hello işlevi uygulama kök klasöründe.</span><span class="sxs-lookup"><span data-stu-id="421d2-151">tooreference a custom assembly, upload hello assembly tooyour function app, such as in a `bin` folder in hello function app root.</span></span> 
- <span data-ttu-id="421d2-152">Özel derlemeler verilen işlevin bağlam parçası olan ve dışarıdan farklı sürümlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="421d2-152">Private assemblies are part of a given function's context, and support side-loading of different versions.</span></span> <span data-ttu-id="421d2-153">Özel derlemeler karşıya yüklenebilir içinde bir `bin` hello işlevi dizin klasöründe.</span><span class="sxs-lookup"><span data-stu-id="421d2-153">Private assemblies should be uploaded in a `bin` folder in hello function directory.</span></span> <span data-ttu-id="421d2-154">Merhaba dosya adı gibi kullanarak başvuru `#r "MyAssembly.dll"`.</span><span class="sxs-lookup"><span data-stu-id="421d2-154">Reference using hello file name, such as  `#r "MyAssembly.dll"`.</span></span> 

<span data-ttu-id="421d2-155">Nasıl tooupload dosyaları tooyour işlevi klasörü hakkında daha fazla bilgi için paket Yönetimi bölümünde aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="421d2-155">For information on how tooupload files tooyour function folder, see hello following section on package management.</span></span>

### <a name="watched-directories"></a><span data-ttu-id="421d2-156">İzlenen dizinleri</span><span class="sxs-lookup"><span data-stu-id="421d2-156">Watched directories</span></span>

<span data-ttu-id="421d2-157">Merhaba işlevi komut dosyasını içeren hello dizini otomatik olarak değişiklikleri tooassemblies için izlenen.</span><span class="sxs-lookup"><span data-stu-id="421d2-157">hello directory that contains hello function script file is automatically watched for changes tooassemblies.</span></span> <span data-ttu-id="421d2-158">derleme değişiklikleri diğer dizinlerde toowatch eklemek bunları toohello `watchDirectories` listesinde [konak\.json].</span><span class="sxs-lookup"><span data-stu-id="421d2-158">toowatch for assembly changes in other directories, add them toohello `watchDirectories` list in [host\.json].</span></span>

## <a name="using-nuget-packages"></a><span data-ttu-id="421d2-159">NuGet paketlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="421d2-159">Using NuGet packages</span></span>
<span data-ttu-id="421d2-160">bir C# işlevinde toouse NuGet paketlerini yüklemek bir *project.json* toohello işlevin klasörü hello işlevi uygulamanın dosya sisteminde dosya.</span><span class="sxs-lookup"><span data-stu-id="421d2-160">toouse NuGet packages in a C# function, upload a *project.json* file toohello function's folder in hello function app's file system.</span></span> <span data-ttu-id="421d2-161">İşte bir örnek *project.json* bir başvuru tooMicrosoft.ProjectOxford.Face sürüm 1.1.0 ekler dosyası:</span><span class="sxs-lookup"><span data-stu-id="421d2-161">Here is an example *project.json* file that adds a reference tooMicrosoft.ProjectOxford.Face version 1.1.0:</span></span>

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

<span data-ttu-id="421d2-162">Hello .NET Framework 4.6 desteklenir yalnızca, bu nedenle olduğundan emin olun, *project.json* dosyayı belirtir `net46` aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="421d2-162">Only hello .NET Framework 4.6 is supported, so make sure that your *project.json* file specifies `net46` as shown here.</span></span>

<span data-ttu-id="421d2-163">Karşıya yüklediğiniz zaman bir *project.json* dosya, hello çalışma zamanı hello paketleri alır ve başvurular toohello paket derlemeler otomatik olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="421d2-163">When you upload a *project.json* file, hello runtime gets hello packages and automatically adds references toohello package assemblies.</span></span> <span data-ttu-id="421d2-164">Tooadd gerekmeyen `#r "AssemblyName"` yönergeleri.</span><span class="sxs-lookup"><span data-stu-id="421d2-164">You don't need tooadd `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="421d2-165">Merhaba NuGet paketlerini içinde tanımlanan toouse hello türleri eklemek gerekli hello `using` deyimleri tooyour *run.csx* dosyası</span><span class="sxs-lookup"><span data-stu-id="421d2-165">toouse hello types defined in hello NuGet packages, add hello required `using` statements tooyour *run.csx* file</span></span> 

<span data-ttu-id="421d2-166">Merhaba işlevleri çalışma zamanında NuGet restore çalışır karşılaştırarak `project.json` ve `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="421d2-166">In hello Functions runtime, NuGet restore works by comparing `project.json` and `project.lock.json`.</span></span> <span data-ttu-id="421d2-167">Varsa hello dosyaların tarih ve saat damgaları hello **sağlamadığı** eşleşme NuGet geri yükleme çalıştırır ve NuGet yüklemeleri paketler güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="421d2-167">If hello date and time stamps of hello files **do not** match, a NuGet restore runs and NuGet downloads updated packages.</span></span> <span data-ttu-id="421d2-168">Ancak, Merhaba, tarih ve saat damgaları hello dosyaların **yapmak** eşleşme, NuGet, bir geri yükleme gerçekleştirmez.</span><span class="sxs-lookup"><span data-stu-id="421d2-168">However, if hello date and time stamps of hello files **do** match, NuGet does not perform a restore.</span></span> <span data-ttu-id="421d2-169">Bu nedenle, `project.lock.json` NuGet tooskip paket geri yüklemesi neden olarak kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="421d2-169">Therefore, `project.lock.json` should not be deployed as it causes NuGet tooskip package restore.</span></span> <span data-ttu-id="421d2-170">Merhaba kilit dağıtma tooavoid dosya, hello eklemek `project.lock.json` toohello `.gitignore` dosya.</span><span class="sxs-lookup"><span data-stu-id="421d2-170">tooavoid deploying hello lock file, add hello `project.lock.json` toohello `.gitignore` file.</span></span>

<span data-ttu-id="421d2-171">toouse özel bir NuGet akışı belirtin, akış hello bir *Nuget.Config* hello işlev uygulaması kök dosyasında.</span><span class="sxs-lookup"><span data-stu-id="421d2-171">toouse a custom NuGet feed, specify hello feed in a *Nuget.Config* file in hello Function App root.</span></span> <span data-ttu-id="421d2-172">Daha fazla bilgi için bkz: [NuGet yapılandırma davranışı](/nuget/consume-packages/configuring-nuget-behavior).</span><span class="sxs-lookup"><span data-stu-id="421d2-172">For more information, see [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior).</span></span>

### <a name="using-a-projectjson-file"></a><span data-ttu-id="421d2-173">Project.json dosyası kullanma</span><span class="sxs-lookup"><span data-stu-id="421d2-173">Using a project.json file</span></span>
1. <span data-ttu-id="421d2-174">Merhaba işlevi hello Azure portalını açın.</span><span class="sxs-lookup"><span data-stu-id="421d2-174">Open hello function in hello Azure portal.</span></span> <span data-ttu-id="421d2-175">Merhaba sekmesini görüntüler hello paket yükleme çıktı günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="421d2-175">hello logs tab displays hello package installation output.</span></span>
2. <span data-ttu-id="421d2-176">tooupload project.json dosyası hello açıklanan hello yöntemlerden birini kullanın [nasıl tooupdate işlev uygulama dosyaları](functions-reference.md#fileupdate) hello Azure işlevleri Geliştirici Başvurusu konu başlığı.</span><span class="sxs-lookup"><span data-stu-id="421d2-176">tooupload a project.json file, use one of hello methods described in hello [How tooupdate function app files](functions-reference.md#fileupdate) in hello Azure Functions developer reference topic.</span></span>
3. <span data-ttu-id="421d2-177">Merhaba sonra *project.json* dosyasının yüklendiği, işlevinizi örnekte aşağıdaki hello gibi bir çıktı günlük akış bakın:</span><span class="sxs-lookup"><span data-stu-id="421d2-177">After hello *project.json* file is uploaded, you see output like hello following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="421d2-178">Ortam değişkenleri</span><span class="sxs-lookup"><span data-stu-id="421d2-178">Environment variables</span></span>
<span data-ttu-id="421d2-179">tooget bir ortam değişkeni veya kullanan bir uygulama ayarı değeri `System.Environment.GetEnvironmentVariable`, aşağıdaki kod örneğine hello gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="421d2-179">tooget an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, as shown in hello following code example:</span></span>

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

## <a name="reusing-csx-code"></a><span data-ttu-id="421d2-180">.Csx kodu yeniden kullanma</span><span class="sxs-lookup"><span data-stu-id="421d2-180">Reusing .csx code</span></span>
<span data-ttu-id="421d2-181">Sınıfları ve diğer tanımlanan yöntemler kullanabilirsiniz *.csx* dosyalar, *run.csx* dosya.</span><span class="sxs-lookup"><span data-stu-id="421d2-181">You can use classes and methods defined in other *.csx* files in your *run.csx* file.</span></span> <span data-ttu-id="421d2-182">kullanan, toodo `#load` yönergeleri, *run.csx* dosya.</span><span class="sxs-lookup"><span data-stu-id="421d2-182">toodo that, use `#load` directives in your *run.csx* file.</span></span> <span data-ttu-id="421d2-183">Günlüğe kaydetme yordamını aşağıdaki örneğine hello adlı `MyLogger` içinde paylaşılan *myLogger.csx* ve içine yüklenen *run.csx* hello kullanarak `#load` yönergesi:</span><span class="sxs-lookup"><span data-stu-id="421d2-183">In hello following example, a logging routine named `MyLogger` is shared in *myLogger.csx* and loaded into *run.csx* using hello `#load` directive:</span></span>

<span data-ttu-id="421d2-184">Örnek *run.csx*:</span><span class="sxs-lookup"><span data-stu-id="421d2-184">Example *run.csx*:</span></span>

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

<span data-ttu-id="421d2-185">Örnek *mylogger.csx*:</span><span class="sxs-lookup"><span data-stu-id="421d2-185">Example *mylogger.csx*:</span></span>

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

<span data-ttu-id="421d2-186">Paylaşılan kullanarak *.csx* toostrongly istediğinizde genel bir desen, bağımsız değişkenleri arasında bir POCO nesnesi kullanarak işlevleri yazın.</span><span class="sxs-lookup"><span data-stu-id="421d2-186">Using a shared *.csx* is a common pattern when you want toostrongly type your arguments between functions using a POCO object.</span></span> <span data-ttu-id="421d2-187">Aşağıdaki Basitleştirilmiş örneğine hello adlı bir POCO nesnesi bir HTTP tetikleyicisi ve sıra tetikleyici paylaşmak `Order` toostrongly türü hello sipariş verileri:</span><span class="sxs-lookup"><span data-stu-id="421d2-187">In hello following simplified example, an HTTP trigger and queue trigger share a POCO object named `Order` toostrongly type hello order data:</span></span>

<span data-ttu-id="421d2-188">Örnek *run.csx* HTTP tetikleyicisi için:</span><span class="sxs-lookup"><span data-stu-id="421d2-188">Example *run.csx* for HTTP trigger:</span></span>

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

<span data-ttu-id="421d2-189">Örnek *run.csx* sıra tetikleyici için:</span><span class="sxs-lookup"><span data-stu-id="421d2-189">Example *run.csx* for queue trigger:</span></span>

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

<span data-ttu-id="421d2-190">Örnek *order.csx*:</span><span class="sxs-lookup"><span data-stu-id="421d2-190">Example *order.csx*:</span></span>

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

<span data-ttu-id="421d2-191">Göreli bir yol ile Merhaba kullanabilirsiniz `#load` yönergesi:</span><span class="sxs-lookup"><span data-stu-id="421d2-191">You can use a relative path with hello `#load` directive:</span></span>

* <span data-ttu-id="421d2-192">`#load "mylogger.csx"`Merhaba işlevi klasöründe bir dosya yükler.</span><span class="sxs-lookup"><span data-stu-id="421d2-192">`#load "mylogger.csx"` loads a file located in hello function folder.</span></span>
* <span data-ttu-id="421d2-193">`#load "loadedfiles\mylogger.csx"`Merhaba işlevi klasöründe bulunan bir dosya yükler.</span><span class="sxs-lookup"><span data-stu-id="421d2-193">`#load "loadedfiles\mylogger.csx"` loads a file located in a folder in hello function folder.</span></span>
* <span data-ttu-id="421d2-194">`#load "..\shared\mylogger.csx"`aynı düzeydeki hello işlevi klasör, başka bir deyişle, hello bir klasörde bulunan bir dosya yükler doğrudan altında *wwwroot*.</span><span class="sxs-lookup"><span data-stu-id="421d2-194">`#load "..\shared\mylogger.csx"` loads a file located in a folder at hello same level as hello function folder, that is, directly under *wwwroot*.</span></span>

<span data-ttu-id="421d2-195">Merhaba `#load` yönergesi çalışır yalnızca *.csx* (C# betik) dosyaları değil *.cs* dosyaları.</span><span class="sxs-lookup"><span data-stu-id="421d2-195">hello `#load` directive works only with *.csx* (C# script) files, not with *.cs* files.</span></span>

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a><span data-ttu-id="421d2-196">Kesinlik temelli bağlamaları aracılığıyla çalışma zamanında bağlama</span><span class="sxs-lookup"><span data-stu-id="421d2-196">Binding at runtime via imperative bindings</span></span>

<span data-ttu-id="421d2-197">C# ve diğer .NET dilleri kullanabileceğiniz bir [kesinlik temelli](https://en.wikipedia.org/wiki/Imperative_programming) karşılıklı toohello olarak bağlama düzeni [ *bildirim temelli* ](https://en.wikipedia.org/wiki/Declarative_programming) bağlama *function.json*.</span><span class="sxs-lookup"><span data-stu-id="421d2-197">In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed toohello [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) bindings in *function.json*.</span></span> <span data-ttu-id="421d2-198">Kesinlik temelli bağlama bağlama parametreleri tasarım yerine çalışma zamanında hesaplanan toobe gerektiğinde kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="421d2-198">Imperative binding is useful when binding parameters need toobe computed at runtime rather than design time.</span></span> <span data-ttu-id="421d2-199">Bu desen ile toosupported giriş bağlamak ve bağlama üzerinde-çalışma sırasında işlevi kodunuzda çıktı.</span><span class="sxs-lookup"><span data-stu-id="421d2-199">With this pattern, you can bind toosupported input and output binding on-the-fly in your function code.</span></span>

<span data-ttu-id="421d2-200">Aşağıdaki gibi bağlama kesinliği tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="421d2-200">Define an imperative binding as follows:</span></span>

- <span data-ttu-id="421d2-201">**Sağlamadığı** bir girişe dahil *function.json* , istenen kesinlik temelli bağlamaları için.</span><span class="sxs-lookup"><span data-stu-id="421d2-201">**Do not** include an entry in *function.json* for your desired imperative bindings.</span></span>
- <span data-ttu-id="421d2-202">Giriş parametresi geçişinde [ `Binder binder` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) veya [ `IBinder binder` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span><span class="sxs-lookup"><span data-stu-id="421d2-202">Pass in an input parameter [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) or [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span></span>
- <span data-ttu-id="421d2-203">C# düzeni tooperform hello veri bağlama aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="421d2-203">Use hello following C# pattern tooperform hello data binding.</span></span>

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

<span data-ttu-id="421d2-204">Burada `BindingTypeAttribute` , bağlama tanımlar hello .NET özniteliği ve `T` Merhaba, bağlama türü tarafından desteklenen giriş veya çıkış türü değil.</span><span class="sxs-lookup"><span data-stu-id="421d2-204">where `BindingTypeAttribute` is hello .NET attribute that defines your binding and `T` is hello input or output type that's supported by that binding type.</span></span> <span data-ttu-id="421d2-205">`T`Ayrıca olamaz bir `out` parametre türü (gibi `out JObject`).</span><span class="sxs-lookup"><span data-stu-id="421d2-205">`T` also cannot be an `out` parameter type (such as `out JObject`).</span></span> <span data-ttu-id="421d2-206">Örneğin, Mobile Apps Tablo Bağlama destekler çıktı [altı türleri çıktı](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), ancak yalnızca kullanabilirsiniz [ICollector<T> ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) veya [IAsyncCollector<T> ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs)için `T`.</span><span class="sxs-lookup"><span data-stu-id="421d2-206">For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) for `T`.</span></span>

<span data-ttu-id="421d2-207">Aşağıdaki örnek kod hello oluşturur bir [depolama blobu çıktı bağlama](functions-bindings-storage-blob.md#using-a-blob-output-binding) blob ile çalışma zamanında tanımlanan yol sonra bir dize toohello blob yazar.</span><span class="sxs-lookup"><span data-stu-id="421d2-207">hello following example code creates a [Storage blob output binding](functions-bindings-storage-blob.md#using-a-blob-output-binding) with blob path that's defined at run time, then writes a string toohello blob.</span></span>

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

<span data-ttu-id="421d2-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) hello tanımlar [depolama blobu](functions-bindings-storage-blob.md) giriş veya çıkış bağlamayı ve [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) desteklenen çıktı bağlama türü.</span><span class="sxs-lookup"><span data-stu-id="421d2-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) defines hello [Storage blob](functions-bindings-storage-blob.md) input or output binding, and [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is a supported output binding type.</span></span>
<span data-ttu-id="421d2-209">Olduğu şekilde hello kodu hello depolama hesabı bağlantı dizesi için hello varsayılan uygulama ayarı alır (olduğu `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="421d2-209">As is, hello code gets hello default app setting for hello Storage account connection string (which is `AzureWebJobsStorage`).</span></span> <span data-ttu-id="421d2-210">Bir özel uygulama ayarı toouse ekleyerek belirtebilirsiniz [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) ve hello özniteliği diziye geçirme `BindAsync<T>()`.</span><span class="sxs-lookup"><span data-stu-id="421d2-210">You can specify a custom app setting toouse by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing hello attribute array into `BindAsync<T>()`.</span></span> <span data-ttu-id="421d2-211">Örneğin,</span><span class="sxs-lookup"><span data-stu-id="421d2-211">For example,</span></span>

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

<span data-ttu-id="421d2-212">Merhaba aşağıdaki tabloda her bağlama türü ve hello tanımlı paketler için hello .NET öznitelikleri listeler.</span><span class="sxs-lookup"><span data-stu-id="421d2-212">hello following table lists hello .NET attributes for each binding type and hello packages in which they are defined.</span></span>

> [!div class="mx-codeBreakAll"]
| <span data-ttu-id="421d2-213">Bağlama</span><span class="sxs-lookup"><span data-stu-id="421d2-213">Binding</span></span> | <span data-ttu-id="421d2-214">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="421d2-214">Attribute</span></span> | <span data-ttu-id="421d2-215">Başvuru ekleme</span><span class="sxs-lookup"><span data-stu-id="421d2-215">Add reference</span></span> |
|------|------|------|
| <span data-ttu-id="421d2-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="421d2-216">Cosmos DB</span></span> | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| <span data-ttu-id="421d2-217">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="421d2-217">Event Hubs</span></span> | <span data-ttu-id="421d2-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="421d2-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| <span data-ttu-id="421d2-219">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="421d2-219">Mobile Apps</span></span> | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| <span data-ttu-id="421d2-220">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="421d2-220">Notification Hubs</span></span> | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| <span data-ttu-id="421d2-221">Service Bus</span><span class="sxs-lookup"><span data-stu-id="421d2-221">Service Bus</span></span> | <span data-ttu-id="421d2-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="421d2-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| <span data-ttu-id="421d2-223">Depolama sırası</span><span class="sxs-lookup"><span data-stu-id="421d2-223">Storage queue</span></span> | <span data-ttu-id="421d2-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="421d2-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="421d2-225">Depolama blobu</span><span class="sxs-lookup"><span data-stu-id="421d2-225">Storage blob</span></span> | <span data-ttu-id="421d2-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="421d2-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="421d2-227">Depolama tablosu</span><span class="sxs-lookup"><span data-stu-id="421d2-227">Storage table</span></span> | <span data-ttu-id="421d2-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="421d2-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="421d2-229">Twilio</span><span class="sxs-lookup"><span data-stu-id="421d2-229">Twilio</span></span> | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a><span data-ttu-id="421d2-230">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="421d2-230">Next steps</span></span>
<span data-ttu-id="421d2-231">Daha fazla bilgi için kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="421d2-231">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="421d2-232">Azure İşlevleri için En İyi Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="421d2-232">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="421d2-233">Azure İşlevleri geliştirici başvurusu</span><span class="sxs-lookup"><span data-stu-id="421d2-233">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="421d2-234">Azure işlevleri F # Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="421d2-234">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="421d2-235">Azure işlevleri NodeJS Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="421d2-235">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="421d2-236">Azure işlevleri Tetikleyicileri ve bağlamaları</span><span class="sxs-lookup"><span data-stu-id="421d2-236">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

[ana bilgisayar\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
