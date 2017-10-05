---
title: "Azure işlevleri F # Geliştirici Başvurusu | Microsoft Docs"
description: "F # kullanarak Azure işlevleri geliştirmek nasıl anlayın."
services: functions
documentationcenter: fsharp
author: sylvanc
manager: jbronsk
editor: 
tags: 
keywords: "Azure işlevleri, İşlevler, olay işleme, Web kancalarını, dinamik işlem, sunucusuz mimarisi, F #"
ms.assetid: e60226e5-2630-41d7-9e5b-9f9e5acc8e50
ms.service: functions
ms.devlang: fsharp
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/09/2016
ms.author: syclebsc
ms.openlocfilehash: 1691d378263f6b4ce5072f5c621d8db02f774b5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-f-developer-reference"></a><span data-ttu-id="32d59-104">Azure işlevleri F # Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="32d59-104">Azure Functions F# Developer Reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="32d59-105">C# betiği</span><span class="sxs-lookup"><span data-stu-id="32d59-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="32d59-106">F # betiği</span><span class="sxs-lookup"><span data-stu-id="32d59-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="32d59-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="32d59-107">Node.js</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="32d59-108">F # için Azure işlevleri küçük parçalarını kodu veya "işlevleri" bulutta kolayca çalıştırmak için bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="32d59-108">F# for Azure Functions is a solution for easily running small pieces of code, or "functions," in the cloud.</span></span> <span data-ttu-id="32d59-109">Veri, F # işlevi işlev bağımsız değişkenleri aracılığıyla akar.</span><span class="sxs-lookup"><span data-stu-id="32d59-109">Data flows into your F# function via function arguments.</span></span> <span data-ttu-id="32d59-110">Bağımsız değişken adları belirtilir `function.json`, ve işlevi Günlükçü ve iptal belirteçleri gibi şeyleri erişmek için önceden tanımlanmış adları vardır.</span><span class="sxs-lookup"><span data-stu-id="32d59-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like the function logger and cancellation tokens.</span></span>

<span data-ttu-id="32d59-111">Bu makalede, zaten okuduğunuz varsayılır [Azure işlevleri Geliştirici Başvurusu](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="32d59-111">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="how-fsx-works"></a><span data-ttu-id="32d59-112">.Fsx nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="32d59-112">How .fsx works</span></span>
<span data-ttu-id="32d59-113">Bir `.fsx` F # betiği bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="32d59-113">An `.fsx` file is an F# script.</span></span> <span data-ttu-id="32d59-114">Bu, tek bir dosyada bulunan F # proje olarak düşünülebilir.</span><span class="sxs-lookup"><span data-stu-id="32d59-114">It can be thought of as an F# project that's contained in a single file.</span></span> <span data-ttu-id="32d59-115">Dosyası kodu programınızın (Bu durumda, Azure işlevinizi) içerir ve bağımlılıkları yönetmek için yönergeleri.</span><span class="sxs-lookup"><span data-stu-id="32d59-115">The file contains both the code for your program (in this case, your Azure Function) and directives for managing dependencies.</span></span>

<span data-ttu-id="32d59-116">Kullandığınızda, bir `.fsx` bir Azure işlevi için yaygın olarak derlemeler "ortak" yerine işlevi kodlarına odaklanmasını olanak tanıyan sizin için otomatik olarak dahil gereklidir.</span><span class="sxs-lookup"><span data-stu-id="32d59-116">When you use an `.fsx` for an Azure Function, commonly required assemblies are automatically included for you, allowing you to focus on the function rather than "boilerplate" code.</span></span>

## <a name="binding-to-arguments"></a><span data-ttu-id="32d59-117">Bağımsız değişkenler bağlama</span><span class="sxs-lookup"><span data-stu-id="32d59-117">Binding to arguments</span></span>
<span data-ttu-id="32d59-118">Her bağlama bağımsız değişkenler, içinde ayrıntılı olarak bazı kümesini destekler [Azure işlevleri Tetikleyicileri ve bağlamaları Geliştirici Başvurusu](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="32d59-118">Each binding supports some set of arguments, as detailed in the [Azure Functions triggers and bindings developer reference](functions-triggers-bindings.md).</span></span> <span data-ttu-id="32d59-119">Örneğin, bir blob tetikleyici destekleyen bağımsız değişken bağlamaları kullanarak bir F # kayıt ifade bir POCO biridir.</span><span class="sxs-lookup"><span data-stu-id="32d59-119">For example, one of the argument bindings a blob trigger supports is a POCO, which can be expressed using an F# record.</span></span> <span data-ttu-id="32d59-120">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="32d59-120">For example:</span></span>

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

<span data-ttu-id="32d59-121">F # Azure işlevinizi bağımsız değişkenlerden biri veya daha fazla sürer.</span><span class="sxs-lookup"><span data-stu-id="32d59-121">Your F# Azure Function will take one or more arguments.</span></span> <span data-ttu-id="32d59-122">Biz Azure işlevleri bağımsız değişkenleri hakkında konuşurken biz başvurmak *giriş* bağımsız değişkenleri ve *çıkış* bağımsız değişkenler.</span><span class="sxs-lookup"><span data-stu-id="32d59-122">When we talk about Azure Functions arguments, we refer to *input* arguments and *output* arguments.</span></span> <span data-ttu-id="32d59-123">Ne gibi ses giriş bağımsız değişkeni tam olduğundan: F # Azure işlevinizi için giriş.</span><span class="sxs-lookup"><span data-stu-id="32d59-123">An input argument is exactly what it sounds like: input to your F# Azure Function.</span></span> <span data-ttu-id="32d59-124">Bir *çıkış* değişkendir değişebilir veri veya `byref<>` geri veri iletmek için bir yol olarak hizmet veren bir bağımsız değişken *çıkışı* , işlevin.</span><span class="sxs-lookup"><span data-stu-id="32d59-124">An *output* argument is mutable data or a `byref<>` argument that serves as a way to pass data back *out* of your function.</span></span>

<span data-ttu-id="32d59-125">Yukarıdaki örnekte `blob` bir giriş bağımsız değişkeni ve `output` bir çıktı bağımsız değişken.</span><span class="sxs-lookup"><span data-stu-id="32d59-125">In the example above, `blob` is an input argument, and `output` is an output argument.</span></span> <span data-ttu-id="32d59-126">Kullandık bildirimi `byref<>` için `output` (eklemeye gerek yoktur `[<Out>]` ek açıklama).</span><span class="sxs-lookup"><span data-stu-id="32d59-126">Notice that we used `byref<>` for `output` (there's no need to add the `[<Out>]` annotation).</span></span> <span data-ttu-id="32d59-127">Kullanarak bir `byref<>` türü hangi kaydı veya bağımsız değişkeni başvuruda bulunduğu nesne değiştirmek, işlevi sağlar.</span><span class="sxs-lookup"><span data-stu-id="32d59-127">Using a `byref<>` type allows your function to change which record or object the argument refers to.</span></span>

<span data-ttu-id="32d59-128">İle bir F # kaydı bir girdi türü olarak kullanıldığında, kayıt tanımı işaretlenmelidir `[<CLIMutable>]` işlevinizi için kayıt geçirmeden önce alanlarını uygun şekilde ayarlamak Azure işlevleri framework izin vermek üzere.</span><span class="sxs-lookup"><span data-stu-id="32d59-128">When an F# record is used as an input type, the record definition must be marked with `[<CLIMutable>]` in order to allow the Azure Functions framework to set the fields appropriately before passing the record to your function.</span></span> <span data-ttu-id="32d59-129">Başlık altında `[<CLIMutable>]` kaydı özellikler için ayarlayıcılar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="32d59-129">Under the hood, `[<CLIMutable>]` generates setters for the record properties.</span></span> <span data-ttu-id="32d59-130">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="32d59-130">For example:</span></span>

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

<span data-ttu-id="32d59-131">F # sınıfı, giriş ve çıkış bağımsız değişkenler her ikisi için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="32d59-131">An F# class can also be used for both in and out arguments.</span></span> <span data-ttu-id="32d59-132">Bir sınıf için özellikleri genellikle alıcılar ve ayarlayıcılar gerekir.</span><span class="sxs-lookup"><span data-stu-id="32d59-132">For a class, properties will usually need getters and setters.</span></span> <span data-ttu-id="32d59-133">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="32d59-133">For example:</span></span>

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a><span data-ttu-id="32d59-134">Günlüğe kaydetme</span><span class="sxs-lookup"><span data-stu-id="32d59-134">Logging</span></span>
<span data-ttu-id="32d59-135">Çıktıyı oturum, [akış günlükleri](../app-service-web/web-sites-streaming-logs-and-console.md) F #'ta işlevinizi türünde bir bağımsız değişken zamanınızı `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="32d59-135">To log output to your [streaming logs](../app-service-web/web-sites-streaming-logs-and-console.md) in F#, your function should take an argument of type `TraceWriter`.</span></span> <span data-ttu-id="32d59-136">Tutarlılık için bu bağımsız değişken adlandırılan olan öneririz `log`.</span><span class="sxs-lookup"><span data-stu-id="32d59-136">For consistency, we recommend this argument is named `log`.</span></span> <span data-ttu-id="32d59-137">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="32d59-137">For example:</span></span>

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a><span data-ttu-id="32d59-138">Zaman uyumsuz</span><span class="sxs-lookup"><span data-stu-id="32d59-138">Async</span></span>
<span data-ttu-id="32d59-139">`async` İş akışı kullanılabilir, ancak sonuç döndürmesi gerekir bir `Task`.</span><span class="sxs-lookup"><span data-stu-id="32d59-139">The `async` workflow can be used, but the result needs to return a `Task`.</span></span> <span data-ttu-id="32d59-140">Bu, yapılabilir `Async.StartAsTask`, örneğin:</span><span class="sxs-lookup"><span data-stu-id="32d59-140">This can be done with `Async.StartAsTask`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a><span data-ttu-id="32d59-141">İptal belirteci</span><span class="sxs-lookup"><span data-stu-id="32d59-141">Cancellation Token</span></span>
<span data-ttu-id="32d59-142">İşlevinizi kapatma işleyebilmesini gerekiyorsa verebilirsiniz bir [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="32d59-142">If your function needs to handle shutdown gracefully, you can give it a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument.</span></span> <span data-ttu-id="32d59-143">Bu ile birleştirilebilir `async`, örneğin:</span><span class="sxs-lookup"><span data-stu-id="32d59-143">This can be combined with `async`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a><span data-ttu-id="32d59-144">Ad alanlarını alma</span><span class="sxs-lookup"><span data-stu-id="32d59-144">Importing namespaces</span></span>
<span data-ttu-id="32d59-145">Ad alanları normal şekilde açılabilir:</span><span class="sxs-lookup"><span data-stu-id="32d59-145">Namespaces can be opened in the usual way:</span></span>

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="32d59-146">Şu ad alanlarından otomatik olarak açılır:</span><span class="sxs-lookup"><span data-stu-id="32d59-146">The following namespaces are automatically opened:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* <span data-ttu-id="32d59-147">`Microsoft.Azure.WebJobs.Host`.</span><span class="sxs-lookup"><span data-stu-id="32d59-147">`Microsoft.Azure.WebJobs.Host`.</span></span>

## <a name="referencing-external-assemblies"></a><span data-ttu-id="32d59-148">Dış derlemelere başvurma</span><span class="sxs-lookup"><span data-stu-id="32d59-148">Referencing External Assemblies</span></span>
<span data-ttu-id="32d59-149">Benzer şekilde, framework derleme başvuruları ile eklenmesi `#r "AssemblyName"` yönergesi.</span><span class="sxs-lookup"><span data-stu-id="32d59-149">Similarly, framework assembly references be added with the `#r "AssemblyName"` directive.</span></span>

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="32d59-150">Aşağıdaki derlemeler barındırma ortamı Azure işlevleri tarafından otomatik olarak eklenir:</span><span class="sxs-lookup"><span data-stu-id="32d59-150">The following assemblies are automatically added by the Azure Functions hosting environment:</span></span>

* <span data-ttu-id="32d59-151">`mscorlib`,</span><span class="sxs-lookup"><span data-stu-id="32d59-151">`mscorlib`,</span></span>
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* <span data-ttu-id="32d59-152">`System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="32d59-152">`System.Net.Http.Formatting`.</span></span>

<span data-ttu-id="32d59-153">Ayrıca, aşağıdaki derlemeler özel ortası ve simplename tarafından başvurulan (örneğin `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="32d59-153">In addition, the following assemblies are special cased and may be referenced by simplename (e.g. `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* <span data-ttu-id="32d59-154">`Microsoft.AspNEt.WebHooks.Common`.</span><span class="sxs-lookup"><span data-stu-id="32d59-154">`Microsoft.AspNEt.WebHooks.Common`.</span></span>

<span data-ttu-id="32d59-155">Özel derleme başvurusu ihtiyacınız varsa, derleme dosyasına yükleyebilirsiniz bir `bin` klasörüne görelidir dosyasını kullanarak adlandırın (örneğin, işlev ve başvurusu  `#r "MyAssembly.dll"`).</span><span class="sxs-lookup"><span data-stu-id="32d59-155">If you need to reference a private assembly, you can upload the assembly file into a `bin` folder relative to your function and reference it by using the file name (e.g.  `#r "MyAssembly.dll"`).</span></span> <span data-ttu-id="32d59-156">İşlev klasörünüze dosyaları karşıya yükleme hakkında daha fazla bilgi için paket yönetimi hakkında aşağıdaki bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="32d59-156">For information on how to upload files to your function folder, see the following section on package management.</span></span>

## <a name="editor-prelude"></a><span data-ttu-id="32d59-157">Düzenleyici Prelude</span><span class="sxs-lookup"><span data-stu-id="32d59-157">Editor Prelude</span></span>
<span data-ttu-id="32d59-158">F # derleyici hizmetlerini destekleyen bir düzenleyici ad alanları ve Azure işlevleri otomatik olarak içeren derlemeler haberdar olmaz.</span><span class="sxs-lookup"><span data-stu-id="32d59-158">An editor that supports F# Compiler Services will not be aware of the namespaces and assemblies that Azure Functions automatically includes.</span></span> <span data-ttu-id="32d59-159">Bu nedenle, kullandığınız derlemelerini bulmak Düzenleyicisi yardımcı olan bir prelude dahil edilecek ve ad alanları açıkça açmak için yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="32d59-159">As such, it can be useful to include a prelude that helps the editor find the assemblies you are using, and to explicitly open namespaces.</span></span> <span data-ttu-id="32d59-160">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="32d59-160">For example:</span></span>

```fsharp
#if !COMPILED
#I "../../bin/Binaries/WebJobs.Script.Host"
#r "Microsoft.Azure.WebJobs.Host.dll"
#endif

open Sytem
open Microsoft.Azure.WebJobs.Host

let Run(blob: string, output: byref<string>, log: TraceWriter) =
    ...
```

<span data-ttu-id="32d59-161">Azure işlevleri, kodunuzu yürütüldüğünde, kaynağıyla işler `COMPILED` tanımlı, bu nedenle Düzenleyicisi prelude yoksayıldı.</span><span class="sxs-lookup"><span data-stu-id="32d59-161">When Azure Functions executes your code, it processes the source with `COMPILED` defined, so the editor prelude will be ignored.</span></span>

<a name="package"></a>

## <a name="package-management"></a><span data-ttu-id="32d59-162">Paket Yönetimi</span><span class="sxs-lookup"><span data-stu-id="32d59-162">Package management</span></span>
<span data-ttu-id="32d59-163">NuGet paketlerini bir F # işlevi kullanmak için ekleyin bir `project.json` dosya işlevi uygulamanın dosya sistemi işlevin klasöründe.</span><span class="sxs-lookup"><span data-stu-id="32d59-163">To use NuGet packages in an F# function, add a `project.json` file to the the function's folder in the function app's file system.</span></span> <span data-ttu-id="32d59-164">İşte bir örnek `project.json` NuGet paketi başvuru ekler dosya `Microsoft.ProjectOxford.Face` sürüm 1.1.0:</span><span class="sxs-lookup"><span data-stu-id="32d59-164">Here is an example `project.json` file that adds a NuGet package reference to `Microsoft.ProjectOxford.Face` version 1.1.0:</span></span>

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

<span data-ttu-id="32d59-165">Yalnızca .NET Framework 4.6 desteklenmez, bu nedenle olduğundan emin olun, `project.json` dosyayı belirtir `net46` aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="32d59-165">Only the .NET Framework 4.6 is supported, so make sure that your `project.json` file specifies `net46` as shown here.</span></span>

<span data-ttu-id="32d59-166">Karşıya yüklediğiniz zaman bir `project.json` dosya, çalışma zamanı paketleri alır ve paketi derleme başvuruları otomatik olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="32d59-166">When you upload a `project.json` file, the runtime gets the packages and automatically adds references to the package assemblies.</span></span> <span data-ttu-id="32d59-167">Eklemeniz gerekmez `#r "AssemblyName"` yönergeleri.</span><span class="sxs-lookup"><span data-stu-id="32d59-167">You don't need to add `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="32d59-168">Yalnızca gerekli Ekle `open` deyimleri için `.fsx` dosya.</span><span class="sxs-lookup"><span data-stu-id="32d59-168">Just add the required `open` statements to your `.fsx` file.</span></span>

<span data-ttu-id="32d59-169">F # Hizmetleri derlemek Düzenleyicisi'nin etkileşim artırmak için Düzenleyicisi prelude otomatik olarak başvuru derlemeleri koymak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32d59-169">You may wish to put automatically references assemblies in your editor prelude, to improve your editor's interaction with F# Compile Services.</span></span>

### <a name="how-to-add-a-projectjson-file-to-your-azure-function"></a><span data-ttu-id="32d59-170">Nasıl ekleneceği bir `project.json` Azure işlevinizi dosyasına</span><span class="sxs-lookup"><span data-stu-id="32d59-170">How to add a `project.json` file to your Azure Function</span></span>
1. <span data-ttu-id="32d59-171">Azure portalında işlevinizi açarak yapabilirsiniz işlevi uygulamanızı emin yaparak Başlangıç çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="32d59-171">Begin by making sure your function app is running, which you can do by opening your function in the Azure portal.</span></span> <span data-ttu-id="32d59-172">Bu ayrıca akış günlüklerine paket yükleme çıktısı görüntülenir burada erişmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="32d59-172">This also gives access to the streaming logs where package installation output will be displayed.</span></span>
2. <span data-ttu-id="32d59-173">Karşıya yüklemek için bir `project.json` dosya, açıklanan yöntemlerden birini kullanın [işlevi uygulama dosyaları güncelleştirmek nasıl](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="32d59-173">To upload a `project.json` file, use one of the methods described in [how to update function app files](functions-reference.md#fileupdate).</span></span> <span data-ttu-id="32d59-174">Kullanıyorsanız [Azure işlevleri için sürekli dağıtım](functions-continuous-deployment.md), ekleyebileceğiniz bir `project.json` ile dağıtım dalınızdaki eklemeden önce denemek için hazırlama dalı dosyasına.</span><span class="sxs-lookup"><span data-stu-id="32d59-174">If you are using [Continuous Deployment for Azure Functions](functions-continuous-deployment.md), you can add a `project.json` file to your staging branch in order to experiment with it before adding it to your deployment branch.</span></span>
3. <span data-ttu-id="32d59-175">Sonra `project.json` dosya eklenir, işlevinizi aşağıdaki örneğe benzer bir çıktı günlük akış görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="32d59-175">After the `project.json` file is added, you will see output similar to the following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="32d59-176">Ortam değişkenleri</span><span class="sxs-lookup"><span data-stu-id="32d59-176">Environment variables</span></span>
<span data-ttu-id="32d59-177">Bir ortam değişkeni veya ayar değeri bir uygulamayı almak için `System.Environment.GetEnvironmentVariable`, örneğin:</span><span class="sxs-lookup"><span data-stu-id="32d59-177">To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, for example:</span></span>

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a><span data-ttu-id="32d59-178">.Fsx kodu yeniden kullanma</span><span class="sxs-lookup"><span data-stu-id="32d59-178">Reusing .fsx code</span></span>
<span data-ttu-id="32d59-179">Diğer kodu kullanabilirsiniz `.fsx` kullanarak dosyaları bir `#load` yönergesi.</span><span class="sxs-lookup"><span data-stu-id="32d59-179">You can use code from other `.fsx` files by using a `#load` directive.</span></span> <span data-ttu-id="32d59-180">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="32d59-180">For example:</span></span>

`run.fsx`

```fsharp
#load "logger.fsx"

let Run(timer: TimerInfo, log: TraceWriter) =
    mylog log (sprintf "Timer: %s" DateTime.Now.ToString())
```

`logger.fsx`

```fsharp
let mylog(log: TraceWriter, text: string) =
    log.Verbose(text);
```

<span data-ttu-id="32d59-181">Yollar sağlar için `#load` göreli konumunu yönerge olan, `.fsx` dosya.</span><span class="sxs-lookup"><span data-stu-id="32d59-181">Paths provides to the `#load` directive are relative to the location of your `.fsx` file.</span></span>

* <span data-ttu-id="32d59-182">`#load "logger.fsx"`işlev klasöründe bir dosya yükler.</span><span class="sxs-lookup"><span data-stu-id="32d59-182">`#load "logger.fsx"` loads a file located in the function folder.</span></span>
* <span data-ttu-id="32d59-183">`#load "package\logger.fsx"`bulunan bir dosya yükler `package` işlevi klasöründe.</span><span class="sxs-lookup"><span data-stu-id="32d59-183">`#load "package\logger.fsx"` loads a file located in the `package` folder in the function folder.</span></span>
* <span data-ttu-id="32d59-184">`#load "..\shared\mylogger.fsx"`bulunan bir dosya yükler `shared` klasör başka bir deyişle, işlevi klasör ile aynı düzeyde doğrudan altında `wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="32d59-184">`#load "..\shared\mylogger.fsx"` loads a file located in the `shared` folder at the same level as the function folder, that is, directly under `wwwroot`.</span></span>

<span data-ttu-id="32d59-185">`#load` Yönergesi yalnızca çalışır `.fsx` (F # betik) dosyaları ve değil `.fs` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="32d59-185">The `#load` directive only works with `.fsx` (F# script) files, and not with `.fs` files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32d59-186">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="32d59-186">Next steps</span></span>
<span data-ttu-id="32d59-187">Daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="32d59-187">For more information, see the following resources:</span></span>

* [<span data-ttu-id="32d59-188">F # Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="32d59-188">F# Guide</span></span>](/dotnet/articles/fsharp/index)
* [<span data-ttu-id="32d59-189">Azure İşlevleri için En İyi Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="32d59-189">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="32d59-190">Azure İşlevleri geliştirici başvurusu</span><span class="sxs-lookup"><span data-stu-id="32d59-190">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="32d59-191">Azure işlevleri C# Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="32d59-191">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="32d59-192">Azure işlevleri NodeJS Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="32d59-192">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="32d59-193">Azure işlevleri Tetikleyicileri ve bağlamaları</span><span class="sxs-lookup"><span data-stu-id="32d59-193">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)
* [<span data-ttu-id="32d59-194">Azure işlevlerini test etme</span><span class="sxs-lookup"><span data-stu-id="32d59-194">Azure Functions testing</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="32d59-195">Azure işlevlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="32d59-195">Azure Functions scaling</span></span>](functions-scale.md)

