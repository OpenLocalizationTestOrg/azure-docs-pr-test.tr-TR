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
# <a name="azure-functions-f-developer-reference"></a>Azure işlevleri F # Geliştirici Başvurusu
> [!div class="op_single_selector"]
> * [C# betiği](functions-reference-csharp.md)
> * [F # betiği](functions-reference-fsharp.md)
> * [Node.js](functions-reference-node.md)
> 
> 

F # için Azure işlevleri kolayca küçük parçalarını kodu veya "işlevleri" Merhaba bulutta çalışan bir çözümdür. Veri, F # işlevi işlev bağımsız değişkenleri aracılığıyla akar. Bağımsız değişken adları belirtilir `function.json`, ve işlevi Günlükçü ve iptal belirteçleri hello gibi işlemler erişmek için önceden tanımlanmış adları vardır.

Bu makalede, zaten hello okuduğunuz varsayılır [Azure işlevleri Geliştirici Başvurusu](functions-reference.md).

## <a name="how-fsx-works"></a>.Fsx nasıl çalışır?
Bir `.fsx` F # betiği bir dosyadır. Bu, tek bir dosyada bulunan F # proje olarak düşünülebilir. Merhaba dosya iki hello kodunu programınız (Bu durumda, Azure işlevinizi) içerir ve bağımlılıkları yönetmek için yönergeleri.

Kullandığınızda, bir `.fsx` bir Azure işlevi için yaygın olarak derlemeleri hello "ortak" yerine işlevi kodu toofocus izin vererek sizin için otomatik olarak dahil gereklidir.

## <a name="binding-tooarguments"></a>Tooarguments bağlama
Bazı bağımsız değişkenler, küme içinde ayrıntılı hello olarak her bağlama destekleyen [Azure işlevleri Tetikleyicileri ve bağlamaları Geliştirici Başvurusu](functions-triggers-bindings.md). Örneğin, bir blob tetikleyici destekleyen hello bağımsız değişken bağlamaları kullanarak bir F # kayıt ifade bir POCO biridir. Örneğin:

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

F # Azure işlevinizi bağımsız değişkenlerden biri veya daha fazla sürer. Biz Azure işlevleri bağımsız değişkenleri hakkında konuşurken biz çok başvuran*giriş* bağımsız değişkenleri ve *çıkış* bağımsız değişkenler. Ne gibi ses giriş bağımsız değişkeni tam olduğundan: tooyour F # Azure işlevi giriş. Bir *çıkış* değişkendir değişebilir veri veya `byref<>` şekilde toopass veri geri hizmet bağımsız değişkeni *çıkışı* , işlevin.

Yukarıdaki hello örnekte `blob` bir giriş bağımsız değişkeni ve `output` bir çıktı bağımsız değişken. Kullandık bildirimi `byref<>` için `output` (hiçbir gerek tooadd hello yoktur `[<Out>]` ek açıklama). Kullanarak bir `byref<>` türü için hangi kaydı ya da nesne hello bağımsız değişkeni başvuruyor, işlevi toochange sağlar.

İle bir F # kaydı bir girdi türü olarak kullanıldığında, hello kayıt tanımı işaretlenmelidir `[<CLIMutable>]` içinde hello alanlarını uygun şekilde hello kayıt tooyour işlevi önce geçirme tooallow hello Azure işlevleri framework tooset sipariş. Merhaba başlık altında `[<CLIMutable>]` hello kaydı özellikler için ayarlayıcılar oluşturur. Örneğin:

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

F # sınıfı, giriş ve çıkış bağımsız değişkenler her ikisi için de kullanılabilir. Bir sınıf için özellikleri genellikle alıcılar ve ayarlayıcılar gerekir. Örneğin:

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a>Günlüğe kaydetme
toolog çıkış tooyour [akış günlükleri](../app-service-web/web-sites-streaming-logs-and-console.md) F #'ta işlevinizi türünde bir bağımsız değişken zamanınızı `TraceWriter`. Tutarlılık için bu bağımsız değişken adlandırılan olan öneririz `log`. Örneğin:

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a>Zaman uyumsuz
Merhaba `async` iş akışı kullanılabilir, ancak hello sonuç gerekiyor tooreturn bir `Task`. Bu, yapılabilir `Async.StartAsTask`, örneğin:

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a>İptal belirteci
İşlevinizi toohandle kapatma düzgün biçimde gerekirse, verebilirsiniz bir [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) bağımsız değişkeni. Bu ile birleştirilebilir `async`, örneğin:

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a>Ad alanlarını alma
Ad alanları hello açılabilir her zamanki gibi:

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

ad alanları aşağıdaki hello otomatik olarak açılır:

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`.

## <a name="referencing-external-assemblies"></a>Dış derlemelere başvurma
Benzer şekilde, framework derleme başvuruları ile Merhaba eklenmesi `#r "AssemblyName"` yönergesi.

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

Merhaba aşağıdaki derlemeler otomatik barındırma ortamı hello Azure işlevleri tarafından eklenir:

* `mscorlib`,
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* `System.Net.Http.Formatting`.

Ayrıca, derlemeleri aşağıdaki hello özel ortası ve simplename tarafından başvurulan (örneğin `#r "AssemblyName"`):

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNEt.WebHooks.Common`.

Özel derleme tooreference gerekiyorsa, hello derleme dosyasına karşıya yükleyebilir bir `bin` klasörü göreli tooyour işlevi ve kullanarak hello dosya adı (örneğin başvurusu  `#r "MyAssembly.dll"`). Nasıl tooupload dosyaları tooyour işlevi klasörü hakkında daha fazla bilgi için paket Yönetimi bölümünde aşağıdaki hello bakın.

## <a name="editor-prelude"></a>Düzenleyici Prelude
F # derleyici hizmetlerini destekleyen bir düzenleyici hello ad alanları ve Azure işlevleri otomatik olarak içeren derlemeler haberdar olmaz. Bu nedenle, yararlı tooinclude kullanmakta olduğunuz hello derlemelerini bulmak hello Düzenleyicisi yardımcı olan bir prelude olabilir ve tooexplicitly ad alanları açın. Örneğin:

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

Azure işlevleri, kodunuzu yürütüldüğünde, hello kaynağıyla işler `COMPILED` tanımlanan şekilde hello Düzenleyicisi prelude göz ardı edilir.

<a name="package"></a>

## <a name="package-management"></a>Paket Yönetimi
F # işlevinde, toouse NuGet paketleri ekleme bir `project.json` hello işlevi uygulamanın dosya sisteminde dosyası toohello hello işlevin klasörü. İşte bir örnek `project.json` bir NuGet paketi başvuru çok ekler dosya`Microsoft.ProjectOxford.Face` sürüm 1.1.0:

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

Hello .NET Framework 4.6 desteklenir yalnızca, bu nedenle olduğundan emin olun, `project.json` dosyayı belirtir `net46` aşağıda gösterildiği gibi.

Karşıya yüklediğiniz zaman bir `project.json` dosya, hello çalışma zamanı hello paketleri alır ve başvurular toohello paket derlemeler otomatik olarak ekler. Tooadd gerekmeyen `#r "AssemblyName"` yönergeleri. Yalnızca gerekli hello Ekle `open` deyimleri tooyour `.fsx` dosya.

Tooput tooimprove, Düzenleyicisi prelude derlemelerde F # Hizmetleri derlemek etkileşim Düzenleyicisi'nin otomatik olarak başvuruyor. isteyebilir.

### <a name="how-tooadd-a-projectjson-file-tooyour-azure-function"></a>Nasıl tooadd bir `project.json` dosya tooyour Azure işlevi
1. Hello Azure portal işlevinizi açarak yapabilirsiniz işlevi uygulamanızı emin yaparak Başlangıç çalışıyor. Bu ayrıca toohello akış günlükleri paket yükleme çıktısı görüntülenir burada erişmenizi sağlar.
2. tooupload bir `project.json` dosya, açıklanan hello yöntemlerden birini kullanın [nasıl tooupdate işlev uygulama dosyaları](functions-reference.md#fileupdate). Kullanıyorsanız [Azure işlevleri için sürekli dağıtım](functions-continuous-deployment.md), ekleyebileceğiniz bir `project.json` tooyour dağıtım şube eklemeden önce sipariş tooexperiment onunla dalında hazırlama tooyour dosya.
3. Merhaba sonra `project.json` dosya eklenir, çıktı benzer toohello işlevinizi örnekte aşağıdaki günlük akış görürsünüz:

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
tooget bir ortam değişkeni veya kullanan bir uygulama ayarı değeri `System.Environment.GetEnvironmentVariable`, örneğin:

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a>.Fsx kodu yeniden kullanma
Diğer kodu kullanabilirsiniz `.fsx` kullanarak dosyaları bir `#load` yönergesi. Örneğin:

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

Yollar sağlar toohello `#load` yönergesi olan göreli toohello konumunu, `.fsx` dosya.

* `#load "logger.fsx"`Merhaba işlevi klasöründe bir dosya yükler.
* `#load "package\logger.fsx"`Hello bulunan bir dosya yükler `package` hello işlevi klasöründe.
* `#load "..\shared\mylogger.fsx"`Hello bulunan bir dosya yükler `shared` aynı düzeydeki hello işlevi klasör, başka bir deyişle, hello klasöre doğrudan altında `wwwroot`.

Merhaba `#load` yönergesi yalnızca çalışır `.fsx` (F # betik) dosyaları ve değil `.fs` dosyaları.

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için kaynakları aşağıdaki hello bakın:

* [F # Kılavuzu](/dotnet/articles/fsharp/index)
* [Azure İşlevleri için En İyi Uygulamalar](functions-best-practices.md)
* [Azure İşlevleri geliştirici başvurusu](functions-reference.md)
* [Azure işlevleri C# Geliştirici Başvurusu](functions-reference-csharp.md)
* [Azure işlevleri NodeJS Geliştirici Başvurusu](functions-reference-node.md)
* [Azure işlevleri Tetikleyicileri ve bağlamaları](functions-triggers-bindings.md)
* [Azure işlevlerini test etme](functions-test-a-function.md)
* [Azure işlevlerini ölçeklendirme](functions-scale.md)

