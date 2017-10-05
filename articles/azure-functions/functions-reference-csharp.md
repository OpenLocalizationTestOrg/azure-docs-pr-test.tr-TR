---
title: "Azure işlevleri C# betik Geliştirici Başvurusu | Microsoft Docs"
description: "C# kullanarak Azure işlevleri geliştirmek nasıl anlayın."
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
ms.openlocfilehash: 83a351ce0279ada8ce7fe0513497349471334a86
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-c-script-developer-reference"></a><span data-ttu-id="fb012-104">Azure işlevleri C# betik Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="fb012-104">Azure Functions C# script developer reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fb012-105">C# betiği</span><span class="sxs-lookup"><span data-stu-id="fb012-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="fb012-106">F # betiği</span><span class="sxs-lookup"><span data-stu-id="fb012-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="fb012-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="fb012-107">Node.js</span></span>](functions-reference-node.md)
>
>

<span data-ttu-id="fb012-108">Azure işlevleri için C# betik deneyimi üzerinde Azure WebJobs SDK'sı temel alır.</span><span class="sxs-lookup"><span data-stu-id="fb012-108">The C# script experience for Azure Functions is based on the Azure WebJobs SDK.</span></span> <span data-ttu-id="fb012-109">C# işlevinizi yöntem bağımsız değişkenleri ile verileri akar.</span><span class="sxs-lookup"><span data-stu-id="fb012-109">Data flows into your C# function via method arguments.</span></span> <span data-ttu-id="fb012-110">Bağımsız değişken adları belirtilir `function.json`, ve işlevi Günlükçü ve iptal belirteçleri gibi şeyleri erişmek için önceden tanımlanmış adları vardır.</span><span class="sxs-lookup"><span data-stu-id="fb012-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like the function logger and cancellation tokens.</span></span>

<span data-ttu-id="fb012-111">Bu makalede, zaten okuduğunuz varsayılır [Azure işlevleri Geliştirici Başvurusu](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="fb012-111">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

<span data-ttu-id="fb012-112">Sınıf kitaplıkları C# kullanma hakkında bilgi için bkz: [Azure işlevlerini kullanarak .NET sınıf kitaplıkları](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="fb012-112">For information on using C# class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span>

## <a name="how-csx-works"></a><span data-ttu-id="fb012-113">.Csx nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="fb012-113">How .csx works</span></span>
<span data-ttu-id="fb012-114">`.csx` Biçimi daha az "ortak" yazın ve yalnızca bir C# işlevi yazma odaklanmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="fb012-114">The `.csx` format allows you to write less "boilerplate" and focus on writing just a C# function.</span></span> <span data-ttu-id="fb012-115">Her zamanki gibi tüm derleme başvurularını ve dosya başına ad alanları içerir.</span><span class="sxs-lookup"><span data-stu-id="fb012-115">Include any assembly references and namespaces at the beginning of the file as usual.</span></span> <span data-ttu-id="fb012-116">Her şeyi bir ad alanı ve sınıf kaydırma yerine, yalnızca tanımlayan bir `Run` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="fb012-116">Instead of wrapping everything in a namespace and class, just define a `Run` method.</span></span> <span data-ttu-id="fb012-117">Tüm sınıflar, örneğin dahil gerekiyorsa düz eski CLR nesnesi (POCO) nesneleri tanımlamak için bir sınıf aynı dosyanın içine dahil edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fb012-117">If you need to include any classes, for instance to define Plain Old CLR Object (POCO) objects, you can include a class inside the same file.</span></span>   

## <a name="binding-to-arguments"></a><span data-ttu-id="fb012-118">Bağımsız değişkenler bağlama</span><span class="sxs-lookup"><span data-stu-id="fb012-118">Binding to arguments</span></span>
<span data-ttu-id="fb012-119">Çeşitli bağlamaları bir C# işlevi bağlı `name` özelliğinde *function.json* yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="fb012-119">The various bindings are bound to a C# function via the `name` property in the *function.json* configuration.</span></span> <span data-ttu-id="fb012-120">Her bağlama desteklenen türlerinden; yine de sahip istiyor musunuz? Örneğin, bir blob tetikleyici bir dize, bir POCO veya bir CloudBlockBlob destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="fb012-120">Each binding has its own supported types; for instance, a blob trigger can support a string, a POCO, or a CloudBlockBlob.</span></span> <span data-ttu-id="fb012-121">Desteklenen türler her bağlama başvurusunu belgelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="fb012-121">The supported types are documented in the reference for each binding.</span></span> <span data-ttu-id="fb012-122">Bir POCO nesnesi bir'Set ' yordamı her bir özellik için tanımlanmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fb012-122">A POCO object must have a getter and setter defined for each property.</span></span>

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

## <a name="using-method-return-value-for-output-binding"></a><span data-ttu-id="fb012-123">Yöntemin dönüş değeri için çıktı bağlama işlemini kullanma</span><span class="sxs-lookup"><span data-stu-id="fb012-123">Using method return value for output binding</span></span>

<span data-ttu-id="fb012-124">Adını kullanarak bir yöntemin dönüş değeri bir çıktı bağlaması için kullanabileceğiniz `$return` içinde *function.json*:</span><span class="sxs-lookup"><span data-stu-id="fb012-124">You can use a method return value for an output binding, by using the name `$return` in *function.json*:</span></span>

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

## <a name="writing-multiple-output-values"></a><span data-ttu-id="fb012-125">Birden çok çıktı değerleri yazılıyor</span><span class="sxs-lookup"><span data-stu-id="fb012-125">Writing multiple output values</span></span>

<span data-ttu-id="fb012-126">Bir çıkış bağlaması birden çok değeri yazmak için kullanın [ `ICollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) veya [ `IAsyncCollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) türleri.</span><span class="sxs-lookup"><span data-stu-id="fb012-126">To write multiple values to an output binding, use the [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) types.</span></span> <span data-ttu-id="fb012-127">Bu tür yöntemi tamamlandığında, çıkış bağlama yazılan salt yazılır koleksiyonlarıdır.</span><span class="sxs-lookup"><span data-stu-id="fb012-127">These types are write-only collections that are written to the output binding when the method completes.</span></span>

<span data-ttu-id="fb012-128">Bu örnek kullanarak birden çok sıra iletileri Yazar `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="fb012-128">This example writes multiple queue messages using `ICollector`:</span></span>

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a><span data-ttu-id="fb012-129">Günlüğe kaydetme</span><span class="sxs-lookup"><span data-stu-id="fb012-129">Logging</span></span>
<span data-ttu-id="fb012-130">Çıkış akış günlüklerinizi C# oturum açmak için türünde bir bağımsız değişken dahil `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="fb012-130">To log output to your streaming logs in C#, include an argument of type `TraceWriter`.</span></span> <span data-ttu-id="fb012-131">Bu ad öneririz `log`.</span><span class="sxs-lookup"><span data-stu-id="fb012-131">We recommend that you name it `log`.</span></span> <span data-ttu-id="fb012-132">Kullanmaktan kaçının `Console.Write` Azure işlevlerinde.</span><span class="sxs-lookup"><span data-stu-id="fb012-132">Avoid using `Console.Write` in Azure Functions.</span></span> 

<span data-ttu-id="fb012-133">`TraceWriter`tanımlanan [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span><span class="sxs-lookup"><span data-stu-id="fb012-133">`TraceWriter` is defined in the [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span></span> <span data-ttu-id="fb012-134">Günlük düzeyi için `TraceWriter` yapılandırılabilir [konak\.json].</span><span class="sxs-lookup"><span data-stu-id="fb012-134">The log level for `TraceWriter` can be configured in [host\.json].</span></span>

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a><span data-ttu-id="fb012-135">Zaman uyumsuz</span><span class="sxs-lookup"><span data-stu-id="fb012-135">Async</span></span>
<span data-ttu-id="fb012-136">Bir işlev zaman uyumsuz hale getirmek için kullanmak `async` anahtar sözcüğü ve return bir `Task` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="fb012-136">To make a function asynchronous, use the `async` keyword and return a `Task` object.</span></span>

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a><span data-ttu-id="fb012-137">İptal belirteci</span><span class="sxs-lookup"><span data-stu-id="fb012-137">Cancellation Token</span></span>
<span data-ttu-id="fb012-138">Bazı işlemler normal şekilde kapatılmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="fb012-138">Some operations require graceful shutdown.</span></span> <span data-ttu-id="fb012-139">Her zaman kilitlenen işleyebilir kod yazmak en iyi olmakla birlikte, istediğiniz durumlarda istekleri normal şekilde kapatılmasını işlemek için tanımladığınız bir [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) bağımsız değişken belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="fb012-139">While it's always best to write code that can handle crashing,  in cases where you want to handle graceful shutdown requests, you define a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) typed argument.</span></span>  <span data-ttu-id="fb012-140">A `CancellationToken` bir ana bilgisayar kapatma tetiklenir göstermek için sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="fb012-140">A `CancellationToken` is provided to signal that a host shutdown is triggered.</span></span>

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

## <a name="importing-namespaces"></a><span data-ttu-id="fb012-141">Ad alanlarını alma</span><span class="sxs-lookup"><span data-stu-id="fb012-141">Importing namespaces</span></span>
<span data-ttu-id="fb012-142">Ad alanları almanız gerekiyorsa, bu nedenle olarak normal, ile yapabileceğiniz `using` yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="fb012-142">If you need to import namespaces, you can do so as usual, with the `using` clause.</span></span>

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="fb012-143">Şu ad alanlarından otomatik olarak içe aktarılır ve bu nedenle isteğe bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="fb012-143">The following namespaces are automatically imported and are therefore optional:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a><span data-ttu-id="fb012-144">Dış derlemelere başvurma</span><span class="sxs-lookup"><span data-stu-id="fb012-144">Referencing External Assemblies</span></span>
<span data-ttu-id="fb012-145">Kullanarak Framework derlemeler için başvurular ekleyin `#r "AssemblyName"` yönergesi.</span><span class="sxs-lookup"><span data-stu-id="fb012-145">For framework assemblies, add references by using the `#r "AssemblyName"` directive.</span></span>

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="fb012-146">Aşağıdaki derlemeler barındırma ortamı Azure işlevleri tarafından otomatik olarak eklenir:</span><span class="sxs-lookup"><span data-stu-id="fb012-146">The following assemblies are automatically added by the Azure Functions hosting environment:</span></span>

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

<span data-ttu-id="fb012-147">Aşağıdaki derlemeler basit adıyla başvurulabilir (örneğin, `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="fb012-147">The following assemblies may be referenced by simple-name (for example, `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a><span data-ttu-id="fb012-148">Özel derlemelere başvurma</span><span class="sxs-lookup"><span data-stu-id="fb012-148">Referencing custom assemblies</span></span>

<span data-ttu-id="fb012-149">Özel bir derlemeyi başvurmak için ya da kullanabilirsiniz bir *paylaşılan* derleme veya *özel* derleme:</span><span class="sxs-lookup"><span data-stu-id="fb012-149">To reference a custom assembly, you can use either a *shared* assembly or a *private* assembly:</span></span>
- <span data-ttu-id="fb012-150">Paylaşılan derlemeler işlevi uygulamasında tüm işlevleri arasında paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="fb012-150">Shared assemblies are shared across all functions within a function app.</span></span> <span data-ttu-id="fb012-151">Özel bir derlemeyi başvurmak için işlevi uygulamanızı derlemeye gibi yüklemeniz bir `bin` işlevi uygulama kök klasöründe.</span><span class="sxs-lookup"><span data-stu-id="fb012-151">To reference a custom assembly, upload the assembly to your function app, such as in a `bin` folder in the function app root.</span></span> 
- <span data-ttu-id="fb012-152">Özel derlemeler verilen işlevin bağlam parçası olan ve dışarıdan farklı sürümlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="fb012-152">Private assemblies are part of a given function's context, and support side-loading of different versions.</span></span> <span data-ttu-id="fb012-153">Özel derlemeler karşıya yüklenebilir içinde bir `bin` işlevi dizin klasöründe.</span><span class="sxs-lookup"><span data-stu-id="fb012-153">Private assemblies should be uploaded in a `bin` folder in the function directory.</span></span> <span data-ttu-id="fb012-154">Dosya adı gibi kullanarak başvuru `#r "MyAssembly.dll"`.</span><span class="sxs-lookup"><span data-stu-id="fb012-154">Reference using the file name, such as  `#r "MyAssembly.dll"`.</span></span> 

<span data-ttu-id="fb012-155">İşlev klasörünüze dosyaları karşıya yükleme hakkında daha fazla bilgi için paket yönetimi hakkında aşağıdaki bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="fb012-155">For information on how to upload files to your function folder, see the following section on package management.</span></span>

### <a name="watched-directories"></a><span data-ttu-id="fb012-156">İzlenen dizinleri</span><span class="sxs-lookup"><span data-stu-id="fb012-156">Watched directories</span></span>

<span data-ttu-id="fb012-157">İşlev komut dosyasını içeren dizine değişiklikler derlemeler için otomatik olarak izlenen.</span><span class="sxs-lookup"><span data-stu-id="fb012-157">The directory that contains the function script file is automatically watched for changes to assemblies.</span></span> <span data-ttu-id="fb012-158">Diğer dizinlerde derleme değişiklikleri izlemek için bunları Ekle `watchDirectories` listesinde [konak\.json].</span><span class="sxs-lookup"><span data-stu-id="fb012-158">To watch for assembly changes in other directories, add them to the `watchDirectories` list in [host\.json].</span></span>

## <a name="using-nuget-packages"></a><span data-ttu-id="fb012-159">NuGet paketlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="fb012-159">Using NuGet packages</span></span>
<span data-ttu-id="fb012-160">C# işlevinde NuGet paketlerini kullanmak için karşıya bir *project.json* dosyasını işlevin klasöre işlevi uygulamanın dosya sistemi.</span><span class="sxs-lookup"><span data-stu-id="fb012-160">To use NuGet packages in a C# function, upload a *project.json* file to the function's folder in the function app's file system.</span></span> <span data-ttu-id="fb012-161">İşte bir örnek *project.json* Microsoft.ProjectOxford.Face sürüm 1.1.0 bir başvuru ekler dosyası:</span><span class="sxs-lookup"><span data-stu-id="fb012-161">Here is an example *project.json* file that adds a reference to Microsoft.ProjectOxford.Face version 1.1.0:</span></span>

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

<span data-ttu-id="fb012-162">Yalnızca .NET Framework 4.6 desteklenmez, bu nedenle olduğundan emin olun, *project.json* dosyayı belirtir `net46` aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="fb012-162">Only the .NET Framework 4.6 is supported, so make sure that your *project.json* file specifies `net46` as shown here.</span></span>

<span data-ttu-id="fb012-163">Karşıya yüklediğiniz zaman bir *project.json* dosya, çalışma zamanı paketleri alır ve paketi derleme başvuruları otomatik olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="fb012-163">When you upload a *project.json* file, the runtime gets the packages and automatically adds references to the package assemblies.</span></span> <span data-ttu-id="fb012-164">Eklemeniz gerekmez `#r "AssemblyName"` yönergeleri.</span><span class="sxs-lookup"><span data-stu-id="fb012-164">You don't need to add `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="fb012-165">NuGet paketlerinde tanımlanan türlerin kullanmak için gerekli eklemek `using` deyimleri için *run.csx* dosyası</span><span class="sxs-lookup"><span data-stu-id="fb012-165">To use the types defined in the NuGet packages, add the required `using` statements to your *run.csx* file</span></span> 

<span data-ttu-id="fb012-166">NuGet restore işlevleri çalışma zamanı'nda çalışır karşılaştırarak `project.json` ve `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="fb012-166">In the Functions runtime, NuGet restore works by comparing `project.json` and `project.lock.json`.</span></span> <span data-ttu-id="fb012-167">Varsa dosyaların tarih ve saat Damgalar **sağlamadığı** eşleşme NuGet geri yükleme çalıştırır ve NuGet yüklemeleri paketler güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="fb012-167">If the date and time stamps of the files **do not** match, a NuGet restore runs and NuGet downloads updated packages.</span></span> <span data-ttu-id="fb012-168">Ancak, dosyaların tarih ve saat Damgalar **yapmak** eşleşme, NuGet, bir geri yükleme gerçekleştirmez.</span><span class="sxs-lookup"><span data-stu-id="fb012-168">However, if the date and time stamps of the files **do** match, NuGet does not perform a restore.</span></span> <span data-ttu-id="fb012-169">Bu nedenle, `project.lock.json` NuGet paket geri yüklemesi atlamak neden olarak kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="fb012-169">Therefore, `project.lock.json` should not be deployed as it causes NuGet to skip package restore.</span></span> <span data-ttu-id="fb012-170">Kilit dosyası dağıtma önlemek için add `project.lock.json` için `.gitignore` dosya.</span><span class="sxs-lookup"><span data-stu-id="fb012-170">To avoid deploying the lock file, add the `project.lock.json` to the `.gitignore` file.</span></span>

<span data-ttu-id="fb012-171">Akış özel bir NuGet kullanmak için akışta belirtin bir *Nuget.Config* işlev uygulaması kök dosyasında.</span><span class="sxs-lookup"><span data-stu-id="fb012-171">To use a custom NuGet feed, specify the feed in a *Nuget.Config* file in the Function App root.</span></span> <span data-ttu-id="fb012-172">Daha fazla bilgi için bkz: [NuGet yapılandırma davranışı](/nuget/consume-packages/configuring-nuget-behavior).</span><span class="sxs-lookup"><span data-stu-id="fb012-172">For more information, see [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior).</span></span>

### <a name="using-a-projectjson-file"></a><span data-ttu-id="fb012-173">Project.json dosyası kullanma</span><span class="sxs-lookup"><span data-stu-id="fb012-173">Using a project.json file</span></span>
1. <span data-ttu-id="fb012-174">Azure portalında açma işlevi.</span><span class="sxs-lookup"><span data-stu-id="fb012-174">Open the function in the Azure portal.</span></span> <span data-ttu-id="fb012-175">Günlükleri sekmesinde paket yükleme çıktısını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="fb012-175">The logs tab displays the package installation output.</span></span>
2. <span data-ttu-id="fb012-176">Project.json dosyası karşıya yüklemek için açıklanan yöntemlerden birini kullanın [işlevi uygulama dosyaları güncelleştirmek nasıl](functions-reference.md#fileupdate) Azure işlevleri Geliştirici Başvurusu konu başlığı.</span><span class="sxs-lookup"><span data-stu-id="fb012-176">To upload a project.json file, use one of the methods described in the [How to update function app files](functions-reference.md#fileupdate) in the Azure Functions developer reference topic.</span></span>
3. <span data-ttu-id="fb012-177">Sonra *project.json* dosyasının yüklendiği, işlevinizi aşağıdaki örnekte gibi bir çıktı günlük akış bakın:</span><span class="sxs-lookup"><span data-stu-id="fb012-177">After the *project.json* file is uploaded, you see output like the following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="fb012-178">Ortam değişkenleri</span><span class="sxs-lookup"><span data-stu-id="fb012-178">Environment variables</span></span>
<span data-ttu-id="fb012-179">Bir ortam değişkeni veya ayar değeri bir uygulamayı almak için `System.Environment.GetEnvironmentVariable`aşağıdaki kod örneğinde gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="fb012-179">To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, as shown in the following code example:</span></span>

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

## <a name="reusing-csx-code"></a><span data-ttu-id="fb012-180">.Csx kodu yeniden kullanma</span><span class="sxs-lookup"><span data-stu-id="fb012-180">Reusing .csx code</span></span>
<span data-ttu-id="fb012-181">Sınıfları ve diğer tanımlanan yöntemler kullanabilirsiniz *.csx* dosyalar, *run.csx* dosya.</span><span class="sxs-lookup"><span data-stu-id="fb012-181">You can use classes and methods defined in other *.csx* files in your *run.csx* file.</span></span> <span data-ttu-id="fb012-182">Bunu yapmak için kullanmak `#load` yönergeleri, *run.csx* dosya.</span><span class="sxs-lookup"><span data-stu-id="fb012-182">To do that, use `#load` directives in your *run.csx* file.</span></span> <span data-ttu-id="fb012-183">Aşağıdaki örnekte, bir günlük yordam adlı `MyLogger` içinde paylaşılan *myLogger.csx* ve içine yüklenen *run.csx* kullanarak `#load` yönergesi:</span><span class="sxs-lookup"><span data-stu-id="fb012-183">In the following example, a logging routine named `MyLogger` is shared in *myLogger.csx* and loaded into *run.csx* using the `#load` directive:</span></span>

<span data-ttu-id="fb012-184">Örnek *run.csx*:</span><span class="sxs-lookup"><span data-stu-id="fb012-184">Example *run.csx*:</span></span>

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

<span data-ttu-id="fb012-185">Örnek *mylogger.csx*:</span><span class="sxs-lookup"><span data-stu-id="fb012-185">Example *mylogger.csx*:</span></span>

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

<span data-ttu-id="fb012-186">Paylaşılan kullanarak *.csx* kesinlikle türü, bağımsız değişkenleri bir POCO nesnesi kullanılarak işlevleri arasındaki istediğinizde genel bir desen sağlar.</span><span class="sxs-lookup"><span data-stu-id="fb012-186">Using a shared *.csx* is a common pattern when you want to strongly type your arguments between functions using a POCO object.</span></span> <span data-ttu-id="fb012-187">Aşağıdaki basit örnekte, bir HTTP tetikleyicisi ve sıra tetikleyici adlı bir POCO nesne paylaşmak `Order` kesinlikle sipariş veri türü için:</span><span class="sxs-lookup"><span data-stu-id="fb012-187">In the following simplified example, an HTTP trigger and queue trigger share a POCO object named `Order` to strongly type the order data:</span></span>

<span data-ttu-id="fb012-188">Örnek *run.csx* HTTP tetikleyicisi için:</span><span class="sxs-lookup"><span data-stu-id="fb012-188">Example *run.csx* for HTTP trigger:</span></span>

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

<span data-ttu-id="fb012-189">Örnek *run.csx* sıra tetikleyici için:</span><span class="sxs-lookup"><span data-stu-id="fb012-189">Example *run.csx* for queue trigger:</span></span>

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

<span data-ttu-id="fb012-190">Örnek *order.csx*:</span><span class="sxs-lookup"><span data-stu-id="fb012-190">Example *order.csx*:</span></span>

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

<span data-ttu-id="fb012-191">Göreli bir yol ile kullanabileceğiniz `#load` yönergesi:</span><span class="sxs-lookup"><span data-stu-id="fb012-191">You can use a relative path with the `#load` directive:</span></span>

* <span data-ttu-id="fb012-192">`#load "mylogger.csx"`işlev klasöründe bir dosya yükler.</span><span class="sxs-lookup"><span data-stu-id="fb012-192">`#load "mylogger.csx"` loads a file located in the function folder.</span></span>
* <span data-ttu-id="fb012-193">`#load "loadedfiles\mylogger.csx"`işlev klasöründe bulunan bir dosya yükler.</span><span class="sxs-lookup"><span data-stu-id="fb012-193">`#load "loadedfiles\mylogger.csx"` loads a file located in a folder in the function folder.</span></span>
* <span data-ttu-id="fb012-194">`#load "..\shared\mylogger.csx"`diğer bir deyişle, işlevi klasör ile aynı düzeyde bir klasörde bulunan bir dosya yükler doğrudan altında *wwwroot*.</span><span class="sxs-lookup"><span data-stu-id="fb012-194">`#load "..\shared\mylogger.csx"` loads a file located in a folder at the same level as the function folder, that is, directly under *wwwroot*.</span></span>

<span data-ttu-id="fb012-195">`#load` Yönergesi çalışır yalnızca *.csx* (C# betik) dosyaları değil *.cs* dosyaları.</span><span class="sxs-lookup"><span data-stu-id="fb012-195">The `#load` directive works only with *.csx* (C# script) files, not with *.cs* files.</span></span>

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a><span data-ttu-id="fb012-196">Kesinlik temelli bağlamaları aracılığıyla çalışma zamanında bağlama</span><span class="sxs-lookup"><span data-stu-id="fb012-196">Binding at runtime via imperative bindings</span></span>

<span data-ttu-id="fb012-197">C# ve diğer .NET dilleri kullanabileceğiniz bir [kesinlik temelli](https://en.wikipedia.org/wiki/Imperative_programming) tersine düzeni, bağlama [ *bildirim temelli* ](https://en.wikipedia.org/wiki/Declarative_programming) bağlama *function.json*.</span><span class="sxs-lookup"><span data-stu-id="fb012-197">In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed to the [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) bindings in *function.json*.</span></span> <span data-ttu-id="fb012-198">Kesinlik temelli bağlama bağlama parametreleri tasarım yerine çalışma zamanında hesaplanması gerektiğinde kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="fb012-198">Imperative binding is useful when binding parameters need to be computed at runtime rather than design time.</span></span> <span data-ttu-id="fb012-199">Bu desen ile desteklenen girişine bağlamak ve bağlama üzerinde-çalışma sırasında işlevi kodunuzda çıktı.</span><span class="sxs-lookup"><span data-stu-id="fb012-199">With this pattern, you can bind to supported input and output binding on-the-fly in your function code.</span></span>

<span data-ttu-id="fb012-200">Aşağıdaki gibi bağlama kesinliği tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="fb012-200">Define an imperative binding as follows:</span></span>

- <span data-ttu-id="fb012-201">**Sağlamadığı** bir girişe dahil *function.json* , istenen kesinlik temelli bağlamaları için.</span><span class="sxs-lookup"><span data-stu-id="fb012-201">**Do not** include an entry in *function.json* for your desired imperative bindings.</span></span>
- <span data-ttu-id="fb012-202">Giriş parametresi geçişinde [ `Binder binder` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) veya [ `IBinder binder` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span><span class="sxs-lookup"><span data-stu-id="fb012-202">Pass in an input parameter [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) or [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span></span>
- <span data-ttu-id="fb012-203">Veri bağlama gerçekleştirmek için aşağıdaki C# düzeni kullanın.</span><span class="sxs-lookup"><span data-stu-id="fb012-203">Use the following C# pattern to perform the data binding.</span></span>

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

<span data-ttu-id="fb012-204">Burada `BindingTypeAttribute` , bağlama tanımlayan bir .NET özniteliktir ve `T` , bağlama türü tarafından desteklenen giriş veya çıkış türü.</span><span class="sxs-lookup"><span data-stu-id="fb012-204">where `BindingTypeAttribute` is the .NET attribute that defines your binding and `T` is the input or output type that's supported by that binding type.</span></span> <span data-ttu-id="fb012-205">`T`Ayrıca olamaz bir `out` parametre türü (gibi `out JObject`).</span><span class="sxs-lookup"><span data-stu-id="fb012-205">`T` also cannot be an `out` parameter type (such as `out JObject`).</span></span> <span data-ttu-id="fb012-206">Örneğin, Mobile Apps Tablo Bağlama destekler çıktı [altı türleri çıktı](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), ancak yalnızca kullanabilirsiniz [ICollector<T> ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) veya [IAsyncCollector<T> ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs)için `T`.</span><span class="sxs-lookup"><span data-stu-id="fb012-206">For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) for `T`.</span></span>

<span data-ttu-id="fb012-207">Aşağıdaki kod örneği oluşturur bir [depolama blobu çıktı bağlama](functions-bindings-storage-blob.md#using-a-blob-output-binding) blob ile çalışma zamanında tanımlanan yol sonra Yazar bir dize için blob.</span><span class="sxs-lookup"><span data-stu-id="fb012-207">The following example code creates a [Storage blob output binding](functions-bindings-storage-blob.md#using-a-blob-output-binding) with blob path that's defined at run time, then writes a string to the blob.</span></span>

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

<span data-ttu-id="fb012-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) tanımlar [depolama blobu](functions-bindings-storage-blob.md) giriş veya çıkış bağlamayı ve [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) desteklenen çıktı bağlama türü.</span><span class="sxs-lookup"><span data-stu-id="fb012-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) defines the [Storage blob](functions-bindings-storage-blob.md) input or output binding, and [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is a supported output binding type.</span></span>
<span data-ttu-id="fb012-209">Olduğu gibi varsayılan uygulama ayarı depolama hesabı bağlantı dizesi için kodu alır (olduğu `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="fb012-209">As is, the code gets the default app setting for the Storage account connection string (which is `AzureWebJobsStorage`).</span></span> <span data-ttu-id="fb012-210">Ekleyerek kullanmak için bir özel uygulama ayarı belirtebilirsiniz [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) ve öznitelik diziye geçirme `BindAsync<T>()`.</span><span class="sxs-lookup"><span data-stu-id="fb012-210">You can specify a custom app setting to use by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing the attribute array into `BindAsync<T>()`.</span></span> <span data-ttu-id="fb012-211">Örneğin,</span><span class="sxs-lookup"><span data-stu-id="fb012-211">For example,</span></span>

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

<span data-ttu-id="fb012-212">Aşağıdaki tabloda her bağlama türü ve tanımlanmış paketler için .NET öznitelikleri listeler.</span><span class="sxs-lookup"><span data-stu-id="fb012-212">The following table lists the .NET attributes for each binding type and the packages in which they are defined.</span></span>

> [!div class="mx-codeBreakAll"]
| <span data-ttu-id="fb012-213">Bağlama</span><span class="sxs-lookup"><span data-stu-id="fb012-213">Binding</span></span> | <span data-ttu-id="fb012-214">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="fb012-214">Attribute</span></span> | <span data-ttu-id="fb012-215">Başvuru ekleme</span><span class="sxs-lookup"><span data-stu-id="fb012-215">Add reference</span></span> |
|------|------|------|
| <span data-ttu-id="fb012-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fb012-216">Cosmos DB</span></span> | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| <span data-ttu-id="fb012-217">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="fb012-217">Event Hubs</span></span> | <span data-ttu-id="fb012-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="fb012-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| <span data-ttu-id="fb012-219">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="fb012-219">Mobile Apps</span></span> | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| <span data-ttu-id="fb012-220">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="fb012-220">Notification Hubs</span></span> | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| <span data-ttu-id="fb012-221">Service Bus</span><span class="sxs-lookup"><span data-stu-id="fb012-221">Service Bus</span></span> | <span data-ttu-id="fb012-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="fb012-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| <span data-ttu-id="fb012-223">Depolama sırası</span><span class="sxs-lookup"><span data-stu-id="fb012-223">Storage queue</span></span> | <span data-ttu-id="fb012-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="fb012-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="fb012-225">Depolama blobu</span><span class="sxs-lookup"><span data-stu-id="fb012-225">Storage blob</span></span> | <span data-ttu-id="fb012-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="fb012-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="fb012-227">Depolama tablosu</span><span class="sxs-lookup"><span data-stu-id="fb012-227">Storage table</span></span> | <span data-ttu-id="fb012-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="fb012-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="fb012-229">Twilio</span><span class="sxs-lookup"><span data-stu-id="fb012-229">Twilio</span></span> | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a><span data-ttu-id="fb012-230">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fb012-230">Next steps</span></span>
<span data-ttu-id="fb012-231">Daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="fb012-231">For more information, see the following resources:</span></span>

* [<span data-ttu-id="fb012-232">Azure İşlevleri için En İyi Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="fb012-232">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="fb012-233">Azure İşlevleri geliştirici başvurusu</span><span class="sxs-lookup"><span data-stu-id="fb012-233">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="fb012-234">Azure işlevleri F # Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="fb012-234">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="fb012-235">Azure işlevleri NodeJS Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="fb012-235">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="fb012-236">Azure işlevleri Tetikleyicileri ve bağlamaları</span><span class="sxs-lookup"><span data-stu-id="fb012-236">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

[ana bilgisayar\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
