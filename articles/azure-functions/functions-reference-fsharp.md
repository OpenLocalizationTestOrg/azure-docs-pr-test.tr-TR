---
title: "aaaAzure İşlevler F # Geliştirici Başvurusu | Microsoft Docs"
description: "Anlamak nasıl toodevelop Azure kullanarak F # işlevleri."
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
ms.openlocfilehash: 1ac366ba6f73d191c582dcd9214b688ef719617a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-f-developer-reference"></a><span data-ttu-id="fb565-104">Azure işlevleri F # Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="fb565-104">Azure Functions F# Developer Reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fb565-105">C# betiği</span><span class="sxs-lookup"><span data-stu-id="fb565-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="fb565-106">F # betiği</span><span class="sxs-lookup"><span data-stu-id="fb565-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="fb565-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="fb565-107">Node.js</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="fb565-108">F # için Azure işlevleri kolayca küçük parçalarını kodu veya "işlevleri" Merhaba bulutta çalışan bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="fb565-108">F# for Azure Functions is a solution for easily running small pieces of code, or "functions," in hello cloud.</span></span> <span data-ttu-id="fb565-109">Veri, F # işlevi işlev bağımsız değişkenleri aracılığıyla akar.</span><span class="sxs-lookup"><span data-stu-id="fb565-109">Data flows into your F# function via function arguments.</span></span> <span data-ttu-id="fb565-110">Bağımsız değişken adları belirtilir `function.json`, ve işlevi Günlükçü ve iptal belirteçleri hello gibi işlemler erişmek için önceden tanımlanmış adları vardır.</span><span class="sxs-lookup"><span data-stu-id="fb565-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like hello function logger and cancellation tokens.</span></span>

<span data-ttu-id="fb565-111">Bu makalede, zaten hello okuduğunuz varsayılır [Azure işlevleri Geliştirici Başvurusu](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="fb565-111">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="how-fsx-works"></a><span data-ttu-id="fb565-112">.Fsx nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="fb565-112">How .fsx works</span></span>
<span data-ttu-id="fb565-113">Bir `.fsx` F # betiği bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="fb565-113">An `.fsx` file is an F# script.</span></span> <span data-ttu-id="fb565-114">Bu, tek bir dosyada bulunan F # proje olarak düşünülebilir.</span><span class="sxs-lookup"><span data-stu-id="fb565-114">It can be thought of as an F# project that's contained in a single file.</span></span> <span data-ttu-id="fb565-115">Merhaba dosya iki hello kodunu programınız (Bu durumda, Azure işlevinizi) içerir ve bağımlılıkları yönetmek için yönergeleri.</span><span class="sxs-lookup"><span data-stu-id="fb565-115">hello file contains both hello code for your program (in this case, your Azure Function) and directives for managing dependencies.</span></span>

<span data-ttu-id="fb565-116">Kullandığınızda, bir `.fsx` bir Azure işlevi için yaygın olarak derlemeleri hello "ortak" yerine işlevi kodu toofocus izin vererek sizin için otomatik olarak dahil gereklidir.</span><span class="sxs-lookup"><span data-stu-id="fb565-116">When you use an `.fsx` for an Azure Function, commonly required assemblies are automatically included for you, allowing you toofocus on hello function rather than "boilerplate" code.</span></span>

## <a name="binding-tooarguments"></a><span data-ttu-id="fb565-117">Tooarguments bağlama</span><span class="sxs-lookup"><span data-stu-id="fb565-117">Binding tooarguments</span></span>
<span data-ttu-id="fb565-118">Bazı bağımsız değişkenler, küme içinde ayrıntılı hello olarak her bağlama destekleyen [Azure işlevleri Tetikleyicileri ve bağlamaları Geliştirici Başvurusu](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="fb565-118">Each binding supports some set of arguments, as detailed in hello [Azure Functions triggers and bindings developer reference](functions-triggers-bindings.md).</span></span> <span data-ttu-id="fb565-119">Örneğin, bir blob tetikleyici destekleyen hello bağımsız değişken bağlamaları kullanarak bir F # kayıt ifade bir POCO biridir.</span><span class="sxs-lookup"><span data-stu-id="fb565-119">For example, one of hello argument bindings a blob trigger supports is a POCO, which can be expressed using an F# record.</span></span> <span data-ttu-id="fb565-120">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="fb565-120">For example:</span></span>

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

<span data-ttu-id="fb565-121">F # Azure işlevinizi bağımsız değişkenlerden biri veya daha fazla sürer.</span><span class="sxs-lookup"><span data-stu-id="fb565-121">Your F# Azure Function will take one or more arguments.</span></span> <span data-ttu-id="fb565-122">Biz Azure işlevleri bağımsız değişkenleri hakkında konuşurken biz çok başvuran*giriş* bağımsız değişkenleri ve *çıkış* bağımsız değişkenler.</span><span class="sxs-lookup"><span data-stu-id="fb565-122">When we talk about Azure Functions arguments, we refer too*input* arguments and *output* arguments.</span></span> <span data-ttu-id="fb565-123">Ne gibi ses giriş bağımsız değişkeni tam olduğundan: tooyour F # Azure işlevi giriş.</span><span class="sxs-lookup"><span data-stu-id="fb565-123">An input argument is exactly what it sounds like: input tooyour F# Azure Function.</span></span> <span data-ttu-id="fb565-124">Bir *çıkış* değişkendir değişebilir veri veya `byref<>` şekilde toopass veri geri hizmet bağımsız değişkeni *çıkışı* , işlevin.</span><span class="sxs-lookup"><span data-stu-id="fb565-124">An *output* argument is mutable data or a `byref<>` argument that serves as a way toopass data back *out* of your function.</span></span>

<span data-ttu-id="fb565-125">Yukarıdaki hello örnekte `blob` bir giriş bağımsız değişkeni ve `output` bir çıktı bağımsız değişken.</span><span class="sxs-lookup"><span data-stu-id="fb565-125">In hello example above, `blob` is an input argument, and `output` is an output argument.</span></span> <span data-ttu-id="fb565-126">Kullandık bildirimi `byref<>` için `output` (hiçbir gerek tooadd hello yoktur `[<Out>]` ek açıklama).</span><span class="sxs-lookup"><span data-stu-id="fb565-126">Notice that we used `byref<>` for `output` (there's no need tooadd hello `[<Out>]` annotation).</span></span> <span data-ttu-id="fb565-127">Kullanarak bir `byref<>` türü için hangi kaydı ya da nesne hello bağımsız değişkeni başvuruyor, işlevi toochange sağlar.</span><span class="sxs-lookup"><span data-stu-id="fb565-127">Using a `byref<>` type allows your function toochange which record or object hello argument refers to.</span></span>

<span data-ttu-id="fb565-128">İle bir F # kaydı bir girdi türü olarak kullanıldığında, hello kayıt tanımı işaretlenmelidir `[<CLIMutable>]` içinde hello alanlarını uygun şekilde hello kayıt tooyour işlevi önce geçirme tooallow hello Azure işlevleri framework tooset sipariş.</span><span class="sxs-lookup"><span data-stu-id="fb565-128">When an F# record is used as an input type, hello record definition must be marked with `[<CLIMutable>]` in order tooallow hello Azure Functions framework tooset hello fields appropriately before passing hello record tooyour function.</span></span> <span data-ttu-id="fb565-129">Merhaba başlık altında `[<CLIMutable>]` hello kaydı özellikler için ayarlayıcılar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fb565-129">Under hello hood, `[<CLIMutable>]` generates setters for hello record properties.</span></span> <span data-ttu-id="fb565-130">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="fb565-130">For example:</span></span>

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

<span data-ttu-id="fb565-131">F # sınıfı, giriş ve çıkış bağımsız değişkenler her ikisi için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fb565-131">An F# class can also be used for both in and out arguments.</span></span> <span data-ttu-id="fb565-132">Bir sınıf için özellikleri genellikle alıcılar ve ayarlayıcılar gerekir.</span><span class="sxs-lookup"><span data-stu-id="fb565-132">For a class, properties will usually need getters and setters.</span></span> <span data-ttu-id="fb565-133">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="fb565-133">For example:</span></span>

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a><span data-ttu-id="fb565-134">Günlüğe kaydetme</span><span class="sxs-lookup"><span data-stu-id="fb565-134">Logging</span></span>
<span data-ttu-id="fb565-135">toolog çıkış tooyour [akış günlükleri](../app-service-web/web-sites-streaming-logs-and-console.md) F #'ta işlevinizi türünde bir bağımsız değişken zamanınızı `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="fb565-135">toolog output tooyour [streaming logs](../app-service-web/web-sites-streaming-logs-and-console.md) in F#, your function should take an argument of type `TraceWriter`.</span></span> <span data-ttu-id="fb565-136">Tutarlılık için bu bağımsız değişken adlandırılan olan öneririz `log`.</span><span class="sxs-lookup"><span data-stu-id="fb565-136">For consistency, we recommend this argument is named `log`.</span></span> <span data-ttu-id="fb565-137">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="fb565-137">For example:</span></span>

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a><span data-ttu-id="fb565-138">Zaman uyumsuz</span><span class="sxs-lookup"><span data-stu-id="fb565-138">Async</span></span>
<span data-ttu-id="fb565-139">Merhaba `async` iş akışı kullanılabilir, ancak hello sonuç gerekiyor tooreturn bir `Task`.</span><span class="sxs-lookup"><span data-stu-id="fb565-139">hello `async` workflow can be used, but hello result needs tooreturn a `Task`.</span></span> <span data-ttu-id="fb565-140">Bu, yapılabilir `Async.StartAsTask`, örneğin:</span><span class="sxs-lookup"><span data-stu-id="fb565-140">This can be done with `Async.StartAsTask`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a><span data-ttu-id="fb565-141">İptal belirteci</span><span class="sxs-lookup"><span data-stu-id="fb565-141">Cancellation Token</span></span>
<span data-ttu-id="fb565-142">İşlevinizi toohandle kapatma düzgün biçimde gerekirse, verebilirsiniz bir [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="fb565-142">If your function needs toohandle shutdown gracefully, you can give it a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument.</span></span> <span data-ttu-id="fb565-143">Bu ile birleştirilebilir `async`, örneğin:</span><span class="sxs-lookup"><span data-stu-id="fb565-143">This can be combined with `async`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a><span data-ttu-id="fb565-144">Ad alanlarını alma</span><span class="sxs-lookup"><span data-stu-id="fb565-144">Importing namespaces</span></span>
<span data-ttu-id="fb565-145">Ad alanları hello açılabilir her zamanki gibi:</span><span class="sxs-lookup"><span data-stu-id="fb565-145">Namespaces can be opened in hello usual way:</span></span>

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="fb565-146">ad alanları aşağıdaki hello otomatik olarak açılır:</span><span class="sxs-lookup"><span data-stu-id="fb565-146">hello following namespaces are automatically opened:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* <span data-ttu-id="fb565-147">`Microsoft.Azure.WebJobs.Host`.</span><span class="sxs-lookup"><span data-stu-id="fb565-147">`Microsoft.Azure.WebJobs.Host`.</span></span>

## <a name="referencing-external-assemblies"></a><span data-ttu-id="fb565-148">Dış derlemelere başvurma</span><span class="sxs-lookup"><span data-stu-id="fb565-148">Referencing External Assemblies</span></span>
<span data-ttu-id="fb565-149">Benzer şekilde, framework derleme başvuruları ile Merhaba eklenmesi `#r "AssemblyName"` yönergesi.</span><span class="sxs-lookup"><span data-stu-id="fb565-149">Similarly, framework assembly references be added with hello `#r "AssemblyName"` directive.</span></span>

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="fb565-150">Merhaba aşağıdaki derlemeler otomatik barındırma ortamı hello Azure işlevleri tarafından eklenir:</span><span class="sxs-lookup"><span data-stu-id="fb565-150">hello following assemblies are automatically added by hello Azure Functions hosting environment:</span></span>

* <span data-ttu-id="fb565-151">`mscorlib`,</span><span class="sxs-lookup"><span data-stu-id="fb565-151">`mscorlib`,</span></span>
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* <span data-ttu-id="fb565-152">`System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="fb565-152">`System.Net.Http.Formatting`.</span></span>

<span data-ttu-id="fb565-153">Ayrıca, derlemeleri aşağıdaki hello özel ortası ve simplename tarafından başvurulan (örneğin `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="fb565-153">In addition, hello following assemblies are special cased and may be referenced by simplename (e.g. `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* <span data-ttu-id="fb565-154">`Microsoft.AspNEt.WebHooks.Common`.</span><span class="sxs-lookup"><span data-stu-id="fb565-154">`Microsoft.AspNEt.WebHooks.Common`.</span></span>

<span data-ttu-id="fb565-155">Özel derleme tooreference gerekiyorsa, hello derleme dosyasına karşıya yükleyebilir bir `bin` klasörü göreli tooyour işlevi ve kullanarak hello dosya adı (örneğin başvurusu  `#r "MyAssembly.dll"`).</span><span class="sxs-lookup"><span data-stu-id="fb565-155">If you need tooreference a private assembly, you can upload hello assembly file into a `bin` folder relative tooyour function and reference it by using hello file name (e.g.  `#r "MyAssembly.dll"`).</span></span> <span data-ttu-id="fb565-156">Nasıl tooupload dosyaları tooyour işlevi klasörü hakkında daha fazla bilgi için paket Yönetimi bölümünde aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="fb565-156">For information on how tooupload files tooyour function folder, see hello following section on package management.</span></span>

## <a name="editor-prelude"></a><span data-ttu-id="fb565-157">Düzenleyici Prelude</span><span class="sxs-lookup"><span data-stu-id="fb565-157">Editor Prelude</span></span>
<span data-ttu-id="fb565-158">F # derleyici hizmetlerini destekleyen bir düzenleyici hello ad alanları ve Azure işlevleri otomatik olarak içeren derlemeler haberdar olmaz.</span><span class="sxs-lookup"><span data-stu-id="fb565-158">An editor that supports F# Compiler Services will not be aware of hello namespaces and assemblies that Azure Functions automatically includes.</span></span> <span data-ttu-id="fb565-159">Bu nedenle, yararlı tooinclude kullanmakta olduğunuz hello derlemelerini bulmak hello Düzenleyicisi yardımcı olan bir prelude olabilir ve tooexplicitly ad alanları açın.</span><span class="sxs-lookup"><span data-stu-id="fb565-159">As such, it can be useful tooinclude a prelude that helps hello editor find hello assemblies you are using, and tooexplicitly open namespaces.</span></span> <span data-ttu-id="fb565-160">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="fb565-160">For example:</span></span>

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

<span data-ttu-id="fb565-161">Azure işlevleri, kodunuzu yürütüldüğünde, hello kaynağıyla işler `COMPILED` tanımlanan şekilde hello Düzenleyicisi prelude göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="fb565-161">When Azure Functions executes your code, it processes hello source with `COMPILED` defined, so hello editor prelude will be ignored.</span></span>

<a name="package"></a>

## <a name="package-management"></a><span data-ttu-id="fb565-162">Paket Yönetimi</span><span class="sxs-lookup"><span data-stu-id="fb565-162">Package management</span></span>
<span data-ttu-id="fb565-163">F # işlevinde, toouse NuGet paketleri ekleme bir `project.json` hello işlevi uygulamanın dosya sisteminde dosyası toohello hello işlevin klasörü.</span><span class="sxs-lookup"><span data-stu-id="fb565-163">toouse NuGet packages in an F# function, add a `project.json` file toohello hello function's folder in hello function app's file system.</span></span> <span data-ttu-id="fb565-164">İşte bir örnek `project.json` bir NuGet paketi başvuru çok ekler dosya`Microsoft.ProjectOxford.Face` sürüm 1.1.0:</span><span class="sxs-lookup"><span data-stu-id="fb565-164">Here is an example `project.json` file that adds a NuGet package reference too`Microsoft.ProjectOxford.Face` version 1.1.0:</span></span>

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

<span data-ttu-id="fb565-165">Hello .NET Framework 4.6 desteklenir yalnızca, bu nedenle olduğundan emin olun, `project.json` dosyayı belirtir `net46` aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="fb565-165">Only hello .NET Framework 4.6 is supported, so make sure that your `project.json` file specifies `net46` as shown here.</span></span>

<span data-ttu-id="fb565-166">Karşıya yüklediğiniz zaman bir `project.json` dosya, hello çalışma zamanı hello paketleri alır ve başvurular toohello paket derlemeler otomatik olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="fb565-166">When you upload a `project.json` file, hello runtime gets hello packages and automatically adds references toohello package assemblies.</span></span> <span data-ttu-id="fb565-167">Tooadd gerekmeyen `#r "AssemblyName"` yönergeleri.</span><span class="sxs-lookup"><span data-stu-id="fb565-167">You don't need tooadd `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="fb565-168">Yalnızca gerekli hello Ekle `open` deyimleri tooyour `.fsx` dosya.</span><span class="sxs-lookup"><span data-stu-id="fb565-168">Just add hello required `open` statements tooyour `.fsx` file.</span></span>

<span data-ttu-id="fb565-169">Tooput tooimprove, Düzenleyicisi prelude derlemelerde F # Hizmetleri derlemek etkileşim Düzenleyicisi'nin otomatik olarak başvuruyor. isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="fb565-169">You may wish tooput automatically references assemblies in your editor prelude, tooimprove your editor's interaction with F# Compile Services.</span></span>

### <a name="how-tooadd-a-projectjson-file-tooyour-azure-function"></a><span data-ttu-id="fb565-170">Nasıl tooadd bir `project.json` dosya tooyour Azure işlevi</span><span class="sxs-lookup"><span data-stu-id="fb565-170">How tooadd a `project.json` file tooyour Azure Function</span></span>
1. <span data-ttu-id="fb565-171">Hello Azure portal işlevinizi açarak yapabilirsiniz işlevi uygulamanızı emin yaparak Başlangıç çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="fb565-171">Begin by making sure your function app is running, which you can do by opening your function in hello Azure portal.</span></span> <span data-ttu-id="fb565-172">Bu ayrıca toohello akış günlükleri paket yükleme çıktısı görüntülenir burada erişmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="fb565-172">This also gives access toohello streaming logs where package installation output will be displayed.</span></span>
2. <span data-ttu-id="fb565-173">tooupload bir `project.json` dosya, açıklanan hello yöntemlerden birini kullanın [nasıl tooupdate işlev uygulama dosyaları](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="fb565-173">tooupload a `project.json` file, use one of hello methods described in [how tooupdate function app files](functions-reference.md#fileupdate).</span></span> <span data-ttu-id="fb565-174">Kullanıyorsanız [Azure işlevleri için sürekli dağıtım](functions-continuous-deployment.md), ekleyebileceğiniz bir `project.json` tooyour dağıtım şube eklemeden önce sipariş tooexperiment onunla dalında hazırlama tooyour dosya.</span><span class="sxs-lookup"><span data-stu-id="fb565-174">If you are using [Continuous Deployment for Azure Functions](functions-continuous-deployment.md), you can add a `project.json` file tooyour staging branch in order tooexperiment with it before adding it tooyour deployment branch.</span></span>
3. <span data-ttu-id="fb565-175">Merhaba sonra `project.json` dosya eklenir, çıktı benzer toohello işlevinizi örnekte aşağıdaki günlük akış görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="fb565-175">After hello `project.json` file is added, you will see output similar toohello following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="fb565-176">Ortam değişkenleri</span><span class="sxs-lookup"><span data-stu-id="fb565-176">Environment variables</span></span>
<span data-ttu-id="fb565-177">tooget bir ortam değişkeni veya kullanan bir uygulama ayarı değeri `System.Environment.GetEnvironmentVariable`, örneğin:</span><span class="sxs-lookup"><span data-stu-id="fb565-177">tooget an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, for example:</span></span>

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a><span data-ttu-id="fb565-178">.Fsx kodu yeniden kullanma</span><span class="sxs-lookup"><span data-stu-id="fb565-178">Reusing .fsx code</span></span>
<span data-ttu-id="fb565-179">Diğer kodu kullanabilirsiniz `.fsx` kullanarak dosyaları bir `#load` yönergesi.</span><span class="sxs-lookup"><span data-stu-id="fb565-179">You can use code from other `.fsx` files by using a `#load` directive.</span></span> <span data-ttu-id="fb565-180">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="fb565-180">For example:</span></span>

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

<span data-ttu-id="fb565-181">Yollar sağlar toohello `#load` yönergesi olan göreli toohello konumunu, `.fsx` dosya.</span><span class="sxs-lookup"><span data-stu-id="fb565-181">Paths provides toohello `#load` directive are relative toohello location of your `.fsx` file.</span></span>

* <span data-ttu-id="fb565-182">`#load "logger.fsx"`Merhaba işlevi klasöründe bir dosya yükler.</span><span class="sxs-lookup"><span data-stu-id="fb565-182">`#load "logger.fsx"` loads a file located in hello function folder.</span></span>
* <span data-ttu-id="fb565-183">`#load "package\logger.fsx"`Hello bulunan bir dosya yükler `package` hello işlevi klasöründe.</span><span class="sxs-lookup"><span data-stu-id="fb565-183">`#load "package\logger.fsx"` loads a file located in hello `package` folder in hello function folder.</span></span>
* <span data-ttu-id="fb565-184">`#load "..\shared\mylogger.fsx"`Hello bulunan bir dosya yükler `shared` aynı düzeydeki hello işlevi klasör, başka bir deyişle, hello klasöre doğrudan altında `wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="fb565-184">`#load "..\shared\mylogger.fsx"` loads a file located in hello `shared` folder at hello same level as hello function folder, that is, directly under `wwwroot`.</span></span>

<span data-ttu-id="fb565-185">Merhaba `#load` yönergesi yalnızca çalışır `.fsx` (F # betik) dosyaları ve değil `.fs` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="fb565-185">hello `#load` directive only works with `.fsx` (F# script) files, and not with `.fs` files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb565-186">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fb565-186">Next steps</span></span>
<span data-ttu-id="fb565-187">Daha fazla bilgi için kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="fb565-187">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="fb565-188">F # Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="fb565-188">F# Guide</span></span>](/dotnet/articles/fsharp/index)
* [<span data-ttu-id="fb565-189">Azure İşlevleri için En İyi Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="fb565-189">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="fb565-190">Azure İşlevleri geliştirici başvurusu</span><span class="sxs-lookup"><span data-stu-id="fb565-190">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="fb565-191">Azure işlevleri C# Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="fb565-191">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="fb565-192">Azure işlevleri NodeJS Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="fb565-192">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="fb565-193">Azure işlevleri Tetikleyicileri ve bağlamaları</span><span class="sxs-lookup"><span data-stu-id="fb565-193">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)
* [<span data-ttu-id="fb565-194">Azure işlevlerini test etme</span><span class="sxs-lookup"><span data-stu-id="fb565-194">Azure Functions testing</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="fb565-195">Azure işlevlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="fb565-195">Azure Functions scaling</span></span>](functions-scale.md)

