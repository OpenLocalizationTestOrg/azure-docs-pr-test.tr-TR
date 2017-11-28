---
title: "aaaUsing .NET sınıf kitaplıkları Azure işlevleriyle | Microsoft Docs"
description: "Tooauthor .NET sınıf kitaplıkları için Azure işlevleri nasıl bilgi edinin"
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "Azure işlevleri, İşlevler, olay işleme dinamik işlem sunucusuz mimarisi"
ms.assetid: 9f5db0c2-a88e-4fa8-9b59-37a7096fc828
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/09/2017
ms.author: donnam
ms.openlocfilehash: 4e0fd954b554006ba1d8ecc47403a9fb1c67c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-net-class-libraries-with-azure-functions"></a><span data-ttu-id="7e249-104">Azure işlevleriyle .NET sınıf kitaplıkları kullanma</span><span class="sxs-lookup"><span data-stu-id="7e249-104">Using .NET class libraries with Azure Functions</span></span>

<span data-ttu-id="7e249-105">Ayrıca tooscript dosyaları, Azure işlevleri destekler hello uygulama bir veya daha fazla işlevler için farklı bir sınıf kitaplığı yayımlama.</span><span class="sxs-lookup"><span data-stu-id="7e249-105">In addition tooscript files, Azure Functions supports publishing a class library as hello implementation for one or more functions.</span></span> <span data-ttu-id="7e249-106">Merhaba kullanmanızı öneririz [Azure işlevleri Visual Studio 2017 Araçları](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="7e249-106">We recommend that you use hello [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e249-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7e249-107">Prerequisites</span></span> 

<span data-ttu-id="7e249-108">Bu makalede aşağıdaki önkoşullar hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="7e249-108">This article has hello following prerequisites:</span></span>

- <span data-ttu-id="7e249-109">[Visual Studio 2017 15.3 Önizleme](https://www.visualstudio.com/vs/preview/).</span><span class="sxs-lookup"><span data-stu-id="7e249-109">[Visual Studio 2017 15.3 Preview](https://www.visualstudio.com/vs/preview/).</span></span> <span data-ttu-id="7e249-110">Merhaba iş yükleri yüklemek **ASP.NET ve web geliştirme** ve **Azure geliştirme**.</span><span class="sxs-lookup"><span data-stu-id="7e249-110">Install hello workloads **ASP.NET and web development** and **Azure development**.</span></span>
- [<span data-ttu-id="7e249-111">Visual Studio 2017 için Azure işlevi araçları</span><span class="sxs-lookup"><span data-stu-id="7e249-111">Azure Function Tools for Visual Studio 2017</span></span>](https://marketplace.visualstudio.com/items?itemName=AndrewBHall-MSFT.AzureFunctionToolsforVisualStudio2017)

## <a name="functions-class-library-project"></a><span data-ttu-id="7e249-112">İşlevler sınıf kitaplığı proje</span><span class="sxs-lookup"><span data-stu-id="7e249-112">Functions class library project</span></span>

<span data-ttu-id="7e249-113">Visual Studio'da yeni bir Azure işlevleri projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7e249-113">From Visual Studio, create a new Azure Functions project.</span></span> <span data-ttu-id="7e249-114">Merhaba yeni proje şablonu oluşturur hello dosyaları *host.json* ve *local.settings.json*.</span><span class="sxs-lookup"><span data-stu-id="7e249-114">hello new project template creates hello files *host.json* and *local.settings.json*.</span></span> <span data-ttu-id="7e249-115">Yapabilecekleriniz [host.json Azure işlevleri çalışma zamanı ayarlarınızı özelleştirme](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="7e249-115">You can [customize Azure Functions runtime settings in host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span> 

<span data-ttu-id="7e249-116">Merhaba dosya *local.settings.json* uygulama ayarları, bağlantı dizeleri ve Azure işlevleri çekirdek araçları ayarlarını saklar.</span><span class="sxs-lookup"><span data-stu-id="7e249-116">hello file *local.settings.json* stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="7e249-117">toolearn kendi yapısı hakkında daha fazla bilgi görmek [kod ve yerel olarak Azure işlevlerini test](functions-run-local.md#local-settings).</span><span class="sxs-lookup"><span data-stu-id="7e249-117">toolearn more about its structure, see [Code and test Azure functions locally](functions-run-local.md#local-settings).</span></span>

### <a name="functionname-attribute"></a><span data-ttu-id="7e249-118">FunctionName özniteliği</span><span class="sxs-lookup"><span data-stu-id="7e249-118">FunctionName attribute</span></span>

<span data-ttu-id="7e249-119">Merhaba özniteliği [ `FunctionNameAttribute` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) yöntemi bir işlev giriş noktası olarak işaretler.</span><span class="sxs-lookup"><span data-stu-id="7e249-119">hello attribute [`FunctionNameAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) marks a method as a function entry point.</span></span> <span data-ttu-id="7e249-120">Tam olarak bir tetikleyiciyle kullanılmalıdır ve 0 veya daha fazla giriş ve bağlamaları çıkış.</span><span class="sxs-lookup"><span data-stu-id="7e249-120">It must be used with exactly one trigger and 0 or more input and output bindings.</span></span>

### <a name="conversion-toofunctionjson"></a><span data-ttu-id="7e249-121">Dönüştürme toofunction.json</span><span class="sxs-lookup"><span data-stu-id="7e249-121">Conversion toofunction.json</span></span>

<span data-ttu-id="7e249-122">Azure işlevleri projesinde yapılandırıldığında, bir dosya oluşturur `function.json` tarafından hello işlevi adıyla eşleşen hello dizinde tanımlanan `[FunctionName]`.</span><span class="sxs-lookup"><span data-stu-id="7e249-122">When an Azure Functions project is built, it produces a file `function.json` in hello directory matching hello function name defined by `[FunctionName]`.</span></span> <span data-ttu-id="7e249-123">Tetikleyicileri ve bağlamaları ve noktaları toohello proje derleme dosyası belirtir.</span><span class="sxs-lookup"><span data-stu-id="7e249-123">It specifies triggers and bindings and points toohello project assembly file.</span></span>

<span data-ttu-id="7e249-124">Bu dönüştürme hello NuGet paketi tarafından gerçekleştirilen [Microsoft\.NET\.Sdk\.işlevler](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span><span class="sxs-lookup"><span data-stu-id="7e249-124">This conversion is performed by hello NuGet package [Microsoft\.NET\.Sdk\.Functions](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span></span> <span data-ttu-id="7e249-125">Merhaba kaynak hello GitHub deposuna kullanılabilir [azure\-işlevleri\-vs\-yapı\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span><span class="sxs-lookup"><span data-stu-id="7e249-125">hello source is available in hello GitHub repo [azure\-functions\-vs\-build\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span></span>

## <a name="triggers-and-bindings"></a><span data-ttu-id="7e249-126">Tetikleyiciler ve bağlamalar</span><span class="sxs-lookup"><span data-stu-id="7e249-126">Triggers and bindings</span></span>

<span data-ttu-id="7e249-127">Merhaba aşağıdaki tabloda hello tetikleyiciler ve bir Azure işlevleri sınıf kitaplığında kullanılabilir bağlamaları listeler.</span><span class="sxs-lookup"><span data-stu-id="7e249-127">hello following table lists hello triggers and bindings that are available in an Azure Functions class library project.</span></span> <span data-ttu-id="7e249-128">Tüm öznitelikleri hello ad alanında bulunan `Microsoft.Azure.WebJobs`.</span><span class="sxs-lookup"><span data-stu-id="7e249-128">All attributes are in hello namespace `Microsoft.Azure.WebJobs`.</span></span>

| <span data-ttu-id="7e249-129">Bağlama</span><span class="sxs-lookup"><span data-stu-id="7e249-129">Binding</span></span> | <span data-ttu-id="7e249-130">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="7e249-130">Attribute</span></span> | <span data-ttu-id="7e249-131">NuGet paketi</span><span class="sxs-lookup"><span data-stu-id="7e249-131">NuGet package</span></span> |
|------   | ------    | ------        |
| [<span data-ttu-id="7e249-132">BLOB Depolama tetikleyici, giriş, çıkış</span><span class="sxs-lookup"><span data-stu-id="7e249-132">Blob storage trigger, input, output</span></span>](#blob-storage) | <span data-ttu-id="7e249-133">[BlobAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="7e249-133">[BlobAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="7e249-134">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="7e249-134">[Microsoft.Azure.WebJobs]</span></span> | <span data-ttu-id="7e249-135">[Blob depolama]</span><span class="sxs-lookup"><span data-stu-id="7e249-135">[Blob storage]</span></span> |
| [<span data-ttu-id="7e249-136">Cosmos DB giriş ve çıkış bağlama</span><span class="sxs-lookup"><span data-stu-id="7e249-136">Cosmos DB input and output binding</span></span>](#cosmos-db) | <span data-ttu-id="7e249-137">[DocumentDBAttribute]</span><span class="sxs-lookup"><span data-stu-id="7e249-137">[DocumentDBAttribute]</span></span> | <span data-ttu-id="7e249-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span><span class="sxs-lookup"><span data-stu-id="7e249-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span></span> | 
| [<span data-ttu-id="7e249-139">Olay hub'ları tetikleyici ve çıkış</span><span class="sxs-lookup"><span data-stu-id="7e249-139">Event Hubs trigger and output</span></span>](#event-hub) | <span data-ttu-id="7e249-140">[EventHubTriggerAttribute], [EventHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="7e249-140">[EventHubTriggerAttribute], [EventHubAttribute]</span></span> | <span data-ttu-id="7e249-141">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="7e249-141">[Microsoft.Azure.WebJobs.ServiceBus]</span></span> |
| [<span data-ttu-id="7e249-142">Dış dosya giriş ve çıkış</span><span class="sxs-lookup"><span data-stu-id="7e249-142">External file input and output</span></span>](#api-hub) | <span data-ttu-id="7e249-143">[ApiHubFileAttribute]</span><span class="sxs-lookup"><span data-stu-id="7e249-143">[ApiHubFileAttribute]</span></span> | <span data-ttu-id="7e249-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span><span class="sxs-lookup"><span data-stu-id="7e249-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span></span> |
| [<span data-ttu-id="7e249-145">HTTP ve Web kancası tetikleyici</span><span class="sxs-lookup"><span data-stu-id="7e249-145">HTTP and webhook trigger</span></span>](#http) | <span data-ttu-id="7e249-146">[HttpTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="7e249-146">[HttpTriggerAttribute]</span></span> | <span data-ttu-id="7e249-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span><span class="sxs-lookup"><span data-stu-id="7e249-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span></span> |
| [<span data-ttu-id="7e249-148">Mobile Apps giriş ve çıkış</span><span class="sxs-lookup"><span data-stu-id="7e249-148">Mobile Apps input and output</span></span>](#mobile-apps) | <span data-ttu-id="7e249-149">[MobileTableAttribute]</span><span class="sxs-lookup"><span data-stu-id="7e249-149">[MobileTableAttribute]</span></span> | <span data-ttu-id="7e249-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span><span class="sxs-lookup"><span data-stu-id="7e249-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span></span> | 
| [<span data-ttu-id="7e249-151">Bildirim hub'ları çıktı</span><span class="sxs-lookup"><span data-stu-id="7e249-151">Notification Hubs output</span></span>](#nh) | <span data-ttu-id="7e249-152">[NotificationHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="7e249-152">[NotificationHubAttribute]</span></span> | <span data-ttu-id="7e249-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span><span class="sxs-lookup"><span data-stu-id="7e249-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span></span> | 
| [<span data-ttu-id="7e249-154">Kuyruk depolama tetikleyici ve çıkış</span><span class="sxs-lookup"><span data-stu-id="7e249-154">Queue storage trigger and output</span></span>](#queue) | <span data-ttu-id="7e249-155">[QueueAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="7e249-155">[QueueAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="7e249-156">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="7e249-156">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="7e249-157">SendGrid çıkış</span><span class="sxs-lookup"><span data-stu-id="7e249-157">SendGrid output</span></span>](#sendgrid) | <span data-ttu-id="7e249-158">[SendGridAttribute]</span><span class="sxs-lookup"><span data-stu-id="7e249-158">[SendGridAttribute]</span></span> | <span data-ttu-id="7e249-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span><span class="sxs-lookup"><span data-stu-id="7e249-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span></span> | 
| [<span data-ttu-id="7e249-160">Hizmet veri yolu tetikleyici ve çıkış</span><span class="sxs-lookup"><span data-stu-id="7e249-160">Service Bus trigger and output</span></span>](#service-bus) | <span data-ttu-id="7e249-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="7e249-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span></span> | <span data-ttu-id="7e249-162">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="7e249-162">[Microsoft.Azure.WebJobs.ServiceBus]</span></span>
| [<span data-ttu-id="7e249-163">Tablo depolama giriş ve çıkış</span><span class="sxs-lookup"><span data-stu-id="7e249-163">Table storage input and output</span></span>](#table) | <span data-ttu-id="7e249-164">[TableAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="7e249-164">[TableAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="7e249-165">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="7e249-165">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="7e249-166">Zamanlayıcı tetikleyicisi</span><span class="sxs-lookup"><span data-stu-id="7e249-166">Timer trigger</span></span>](#timer) | <span data-ttu-id="7e249-167">[TimerTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="7e249-167">[TimerTriggerAttribute]</span></span> | <span data-ttu-id="7e249-168">[Microsoft.Azure.WebJobs.Extensions]</span><span class="sxs-lookup"><span data-stu-id="7e249-168">[Microsoft.Azure.WebJobs.Extensions]</span></span> | 
| [<span data-ttu-id="7e249-169">Twilio çıkış</span><span class="sxs-lookup"><span data-stu-id="7e249-169">Twilio output</span></span>](#twilio) | <span data-ttu-id="7e249-170">[TwilioSmsAttribute]</span><span class="sxs-lookup"><span data-stu-id="7e249-170">[TwilioSmsAttribute]</span></span> | <span data-ttu-id="7e249-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span><span class="sxs-lookup"><span data-stu-id="7e249-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span></span> | 

<a name="blob-storage"></a>

### <a name="blob-storage-trigger-input-and-output-bindings"></a><span data-ttu-id="7e249-172">BLOB Depolama tetikleyici, giriş ve çıkış bağlamaları</span><span class="sxs-lookup"><span data-stu-id="7e249-172">Blob storage trigger, input, and output bindings</span></span>

<span data-ttu-id="7e249-173">Azure işlevleri destekler tetikleyici, giriş ve Azure Blob Depolama bağlantılarında çıkış.</span><span class="sxs-lookup"><span data-stu-id="7e249-173">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="7e249-174">Bağlama ifadeleri ve meta verileri hakkında daha fazla bilgi için bkz: [Azure işlevleri Blob Depolama bağlamaları](functions-bindings-storage-blob.md).</span><span class="sxs-lookup"><span data-stu-id="7e249-174">For more information on binding expressions and metadata, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>

<span data-ttu-id="7e249-175">Blob tetikleyici ile Merhaba tanımlı `[BlobTrigger]` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="7e249-175">A blob trigger is defined with hello `[BlobTrigger]` attribute.</span></span> <span data-ttu-id="7e249-176">Merhaba özniteliğini kullanabilirsiniz `[StorageAccount]` bir tüm işlev veya sınıf tarafından kullanılan toodefine hello depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="7e249-176">You can use hello attribute `[StorageAccount]` toodefine hello storage account that is used by an entire function or class.</span></span>

```csharp
[StorageAccount("AzureWebJobsStorage")]
[FunctionName("BlobTriggerCSharp")]        
public static void Run([BlobTrigger("samples-workitems/{name}")] Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

<span data-ttu-id="7e249-177">Blob giriş ve çıkış tanımlanmış hello kullanarak `[Blob]` , bunların ile öznitelik bir `FileAccess` parametresi belirten okuma veya yazma.</span><span class="sxs-lookup"><span data-stu-id="7e249-177">Blob input and output are defined using hello `[Blob]` attribute, along with a `FileAccess` parameter indicating read or write.</span></span> <span data-ttu-id="7e249-178">Örnek kullanan bir blob tetikleyici hello ve çıktı bağlama blob.</span><span class="sxs-lookup"><span data-stu-id="7e249-178">hello following example uses a blob trigger and blob output binding.</span></span>

```csharp
[FunctionName("ResizeImage")]
[StorageAccount("AzureWebJobsStorage")]
public static void Run(
    [BlobTrigger("sample-images/{name}")] Stream image, 
    [Blob("sample-images-sm/{name}", FileAccess.Write)] Stream imageSmall, 
    [Blob("sample-images-md/{name}", FileAccess.Write)] Stream imageMedium)
{
    var imageBuilder = ImageResizer.ImageBuilder.Current;
    var size = imageDimensionsTable[ImageSize.Small];

    imageBuilder.Build(image, imageSmall,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);

    image.Position = 0;
    size = imageDimensionsTable[ImageSize.Medium];

    imageBuilder.Build(image, imageMedium,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);
}

public enum ImageSize { ExtraSmall, Small, Medium }

private static Dictionary<ImageSize, (int, int)> imageDimensionsTable = new Dictionary<ImageSize, (int, int)>() {
    { ImageSize.ExtraSmall, (320, 200) },
    { ImageSize.Small,      (640, 400) },
    { ImageSize.Medium,     (800, 600) }
};
```        

<a name="cosmos-db"></a>

### <a name="cosmos-db-input-and-output-bindings"></a><span data-ttu-id="7e249-179">Cosmos DB giriş ve çıkış bağlamaları</span><span class="sxs-lookup"><span data-stu-id="7e249-179">Cosmos DB input and output bindings</span></span>

<span data-ttu-id="7e249-180">Giriş ve Cosmos DB bağlantılarında çıktı Azure işlevleri destekler.</span><span class="sxs-lookup"><span data-stu-id="7e249-180">Azure Functions supports input and output bindings for Cosmos DB.</span></span> <span data-ttu-id="7e249-181">toolearn hello Cosmos DB bağlamanın hello özellikleri hakkında daha fazla bilgi görmek [Azure işlevleri Cosmos DB bağlamaları](functions-bindings-documentdb.md).</span><span class="sxs-lookup"><span data-stu-id="7e249-181">toolearn more about hello features of hello Cosmos DB binding, see [Azure Functions Cosmos DB bindings](functions-bindings-documentdb.md).</span></span>

<span data-ttu-id="7e249-182">toobind tooa Cosmos DB belge kullanmak hello özniteliği `[DocumentDB]` hello NuGet paketi [Microsoft.Azure.WebJobs.Extensions.DocumentDB].</span><span class="sxs-lookup"><span data-stu-id="7e249-182">toobind tooa Cosmos DB document, use hello attribute `[DocumentDB]` in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.DocumentDB].</span></span> <span data-ttu-id="7e249-183">Aşağıdaki örneğine hello sıra tetikleyici ve bir DocumentDB bağlama çıktısı API vardır:</span><span class="sxs-lookup"><span data-stu-id="7e249-183">hello following example has a queue trigger and a DocumentDB API output binding:</span></span>

```csharp
[FunctionName("QueueToDocDB")]        
public static void Run(
    [QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, 
    [DocumentDB("ToDoList", "Items", ConnectionStringSetting = "DocDBConnection")] out dynamic document)
{
    document = new { Text = myQueueItem, id = Guid.NewGuid() };
}

```

<a name="event-hub"></a>

### <a name="event-hubs-trigger-and-output"></a><span data-ttu-id="7e249-184">Olay hub'ları tetikleyici ve çıkış</span><span class="sxs-lookup"><span data-stu-id="7e249-184">Event Hubs trigger and output</span></span>

<span data-ttu-id="7e249-185">Tetikler ve olay hub'ları için bağlamaları çıktı Azure işlevleri destekler.</span><span class="sxs-lookup"><span data-stu-id="7e249-185">Azure Functions supports trigger and output bindings for Event Hubs.</span></span> <span data-ttu-id="7e249-186">Daha fazla bilgi için bkz: [Azure işlevleri olay hub'ı bağlamaları](functions-bindings-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="7e249-186">For more information, see  [Azure Functions Event Hub bindings](functions-bindings-event-hubs.md).</span></span>

<span data-ttu-id="7e249-187">Merhaba türleri `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` ve `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` hello NuGet paketi tanımlanan [Microsoft.Azure.WebJobs.ServiceBus].</span><span class="sxs-lookup"><span data-stu-id="7e249-187">hello types `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` and `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` are defined in hello NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="7e249-188">Merhaba aşağıdaki örnekte bir olay hub'ı tetikleyicisi kullanır:</span><span class="sxs-lookup"><span data-stu-id="7e249-188">hello following example uses an Event Hub trigger:</span></span>

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="7e249-189">Merhaba aşağıdaki örnekte bir olay çıkışı, hello yönteminin dönüş değeri hello çıkış olarak kullanan Hub sahiptir:</span><span class="sxs-lookup"><span data-stu-id="7e249-189">hello following example has an Event Hub output, using hello method return value as hello output:</span></span>

```csharp
[FunctionName("EventHubOutput")]
[return: EventHub("outputEventHubMessage", Connection = "EventHubConnection")]
public static string Run([TimerTrigger("0 */5 * * * *")] TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    return $"{DateTime.Now}";
}
```

<a name="api-hub"></a>

### <a name="external-file-input-and-output"></a><span data-ttu-id="7e249-190">Dış dosya giriş ve çıkış</span><span class="sxs-lookup"><span data-stu-id="7e249-190">External file input and output</span></span>

<span data-ttu-id="7e249-191">Azure işlevlerini destekleyen tetikleyici, giriş ve çıkış bağlamaları Google sürücü, Dropbox ve OneDrive gibi harici dosyalar için.</span><span class="sxs-lookup"><span data-stu-id="7e249-191">Azure Functions supports trigger, input, and output bindings for external files, such as Google Drive, Dropbox, and OneDrive.</span></span> <span data-ttu-id="7e249-192">toolearn daha, fazla [Azure işlevleri dış dosya bağlamalarını](functions-bindings-external-file.md).</span><span class="sxs-lookup"><span data-stu-id="7e249-192">toolearn more, see [Azure Functions External File bindings](functions-bindings-external-file.md).</span></span> <span data-ttu-id="7e249-193">Merhaba öznitelikleri `[ExternalFileTrigger]` ve `[ExternalFile]` hello NuGet paketi tanımlanan [Microsoft.Azure.WebJobs.Extensions.ApiHub].</span><span class="sxs-lookup"><span data-stu-id="7e249-193">hello attributes `[ExternalFileTrigger]` and `[ExternalFile]` are defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.ApiHub].</span></span>

<span data-ttu-id="7e249-194">Aşağıdaki C# örneğine hello dış dosyası giriş ve bağlama çıkış gösterir.</span><span class="sxs-lookup"><span data-stu-id="7e249-194">hello following C# example demonstrates an external file input and output binding.</span></span> <span data-ttu-id="7e249-195">Merhaba kod kopyaları giriş toohello çıktı dosyası hello.</span><span class="sxs-lookup"><span data-stu-id="7e249-195">hello code copies hello input file toohello output file.</span></span>

```csharp
[StorageAccount("MyStorageConnection")]
[FunctionName("ExternalFile")]
[return: ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}-Copy", FileAccess.Write)]
public static string Run([QueueTrigger("myqueue-items")] string myQueueItem, 
    [ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}", FileAccess.Read)] string myInputFile, 
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    return myInputFile;
}
```

<a name="http"></a>

### <a name="http-and-webhooks"></a><span data-ttu-id="7e249-196">HTTP ve web kancaları</span><span class="sxs-lookup"><span data-stu-id="7e249-196">HTTP and webhooks</span></span>

<span data-ttu-id="7e249-197">Kullanım hello `HttpTrigger` özniteliği toodefine bir HTTP tetikleyicisi veya Web kancası.</span><span class="sxs-lookup"><span data-stu-id="7e249-197">Use hello `HttpTrigger` attribute toodefine an HTTP trigger or webhook.</span></span> <span data-ttu-id="7e249-198">Bu öznitelik hello NuGet paketi tanımlanan [Microsoft.Azure.WebJobs.Extensions.Http].</span><span class="sxs-lookup"><span data-stu-id="7e249-198">This attribute is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.Http].</span></span> <span data-ttu-id="7e249-199">Merhaba yetki düzeyini, Web kancası türü, yol ve yöntemleri özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e249-199">You can customize hello authorization level, webhook type, route, and methods.</span></span> <span data-ttu-id="7e249-200">Merhaba aşağıdaki örnek tanımlayan bir HTTP tetikleyicisi anonim kimlik doğrulaması ile ve _genericJson_ Web kancası türü.</span><span class="sxs-lookup"><span data-stu-id="7e249-200">hello following example defines an HTTP trigger with anonymous authentication and _genericJson_ webhook type.</span></span>

```csharp
[FunctionName("HttpTriggerCSharp")]
public static HttpResponseMessage Run([HttpTrigger(AuthorizationLevel.Anonymous, WebHookType = "genericJson")] HttpRequestMessage req)
{
    return req.CreateResponse(HttpStatusCode.OK);
}
```

<a name="mobile-apps"></a>

### <a name="mobile-apps-input-and-output"></a><span data-ttu-id="7e249-201">Mobile Apps giriş ve çıkış</span><span class="sxs-lookup"><span data-stu-id="7e249-201">Mobile Apps input and output</span></span>

<span data-ttu-id="7e249-202">Giriş ve Mobile Apps için bağlamaları çıktı Azure işlevleri destekler.</span><span class="sxs-lookup"><span data-stu-id="7e249-202">Azure Functions supports input and output bindings for Mobile Apps.</span></span> <span data-ttu-id="7e249-203">toolearn daha, fazla [Azure işlevleri Mobile Apps bağlamaları](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="7e249-203">toolearn more, see [Azure Functions Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span> <span data-ttu-id="7e249-204">Merhaba özniteliği `[MobileTable]` hello NuGet paketi tanımlanan [Microsoft.Azure.WebJobs.Extensions.MobileApps].</span><span class="sxs-lookup"><span data-stu-id="7e249-204">hello attribute `[MobileTable]` is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.MobileApps].</span></span>

<span data-ttu-id="7e249-205">Merhaba aşağıdaki örnekte gösterilmiştir Mobile Apps bağlama çıktı:</span><span class="sxs-lookup"><span data-stu-id="7e249-205">hello following example demonstrates a Mobile Apps output binding:</span></span>

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, TraceWriter log)
{
    return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```

<a name="nh"></a>

### <a name="notification-hubs-output"></a><span data-ttu-id="7e249-206">Bildirim hub'ları çıktı</span><span class="sxs-lookup"><span data-stu-id="7e249-206">Notification Hubs output</span></span>

<span data-ttu-id="7e249-207">Azure işlevleri, bildirim hub'ları için bir çıktı bağlama destekler.</span><span class="sxs-lookup"><span data-stu-id="7e249-207">Azure Functions supports an output binding for Notification Hubs.</span></span> <span data-ttu-id="7e249-208">toolearn daha, fazla [Azure işlevleri bildirim hub'ı çıktı bağlama](functions-bindings-notification-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="7e249-208">toolearn more, see [Azure Functions Notification Hub output binding](functions-bindings-notification-hubs.md).</span></span> <span data-ttu-id="7e249-209">Merhaba özniteliği `[NotificationHub]` hello NuGet paketi tanımlanan [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].</span><span class="sxs-lookup"><span data-stu-id="7e249-209">hello attribute `[NotificationHub]` is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].</span></span>

<a name="queue"></a>

### <a name="queue-storage-trigger-and-output"></a><span data-ttu-id="7e249-210">Kuyruk depolama tetikleyici ve çıkış</span><span class="sxs-lookup"><span data-stu-id="7e249-210">Queue storage trigger and output</span></span>

<span data-ttu-id="7e249-211">Tetikler ve Azure sıralar bağlamaları çıktı Azure işlevleri destekler.</span><span class="sxs-lookup"><span data-stu-id="7e249-211">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="7e249-212">Daha fazla bilgi için bkz: [Azure işlevleri kuyruk depolama bağlamaları](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="7e249-212">For more information, see [Azure Functions Queue Storage bindings](functions-bindings-storage-queue.md).</span></span>

<span data-ttu-id="7e249-213">Merhaba aşağıdaki örnekte nasıl toouse hello işlevi dönüş türü bağlama, hello kullanarak bir sıra çıktıyla gösterir `[Queue]` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="7e249-213">hello following example shows how toouse hello function return type with a queue output binding, using hello `[Queue]` attribute.</span></span> <span data-ttu-id="7e249-214">toodefine bir sıra tetikleyici kullanmak hello `[QueueTrigger]` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="7e249-214">toodefine a queue trigger, use hello `[QueueTrigger]` attribute.</span></span>

```csharp
[StorageAccount("AzureWebJobsStorage")]
public static class QueueFunctions
{
    // HTTP trigger with queue output binding
    [FunctionName("QueueOutput")]
    [return: Queue("myqueue-items")]
    public static string QueueOutput([HttpTrigger] dynamic input,  TraceWriter log)
    {
        log.Info($"C# function processed: {input.Text}");
        return input.Text;
    }

    // Queue trigger
    [FunctionName("QueueTrigger")]
    [StorageAccount("AzureWebJobsStorage")]
    public static void QueueTrigger([QueueTrigger("myqueue-items")] string myQueueItem, TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
    }
}

```

<a name="sendgrid"></a>

### <a name="sendgrid-output"></a><span data-ttu-id="7e249-215">SendGrid çıkış</span><span class="sxs-lookup"><span data-stu-id="7e249-215">SendGrid output</span></span>

<span data-ttu-id="7e249-216">Azure işlevleri program aracılığıyla e-posta göndermek için bağlama SendGrid çıkış destekler.</span><span class="sxs-lookup"><span data-stu-id="7e249-216">Azure Functions supports a SendGrid output binding for sending email programmatically.</span></span> <span data-ttu-id="7e249-217">toolearn daha, fazla [Azure işlevleri SendGrid bağlamaları](functions-bindings-sendgrid.md).</span><span class="sxs-lookup"><span data-stu-id="7e249-217">toolearn more, see [Azure Functions SendGrid bindings](functions-bindings-sendgrid.md).</span></span>

<span data-ttu-id="7e249-218">Merhaba özniteliği `[SendGrid]` hello NuGet paketi tanımlanan [Microsoft.Azure.WebJobs.Extensions.SendGrid].</span><span class="sxs-lookup"><span data-stu-id="7e249-218">hello attribute `[SendGrid]` is defined in hello NuGet package [Microsoft.Azure.WebJobs.Extensions.SendGrid].</span></span>

<span data-ttu-id="7e249-219">Merhaba aşağıdaki hizmet veri yolu kuyruğu tetikleyici kullanılarak ve SendGrid çıktı kullanarak bir bağlama örneğidir `SendGridMessage`:</span><span class="sxs-lookup"><span data-stu-id="7e249-219">hello following is an example of using a Service Bus queue trigger and a SendGrid output binding using `SendGridMessage`:</span></span>

```csharp
[FunctionName("SendEmail")]
public static void Run(
    [ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] OutgoingEmail email,
    [SendGrid] out SendGridMessage message)
{
    message = new SendGridMessage();
    message.AddTo(email.To);
    message.AddContent("text/html", email.Body);
    message.SetFrom(new EmailAddress(email.From));
    message.SetSubject(email.Subject);
}

public class OutgoingEmail
{
    public string too{ get; set; }
    public string From { get; set; }
    public string Subject { get; set; }
    public string Body { get; set; }
}
```

<a name="service-bus"></a>

### <a name="service-bus-trigger-and-output"></a><span data-ttu-id="7e249-220">Hizmet veri yolu tetikleyici ve çıkış</span><span class="sxs-lookup"><span data-stu-id="7e249-220">Service Bus trigger and output</span></span>

<span data-ttu-id="7e249-221">Tetikler ve Service Bus kuyrukları ve konuları için bağlamaları çıktı Azure işlevleri destekler.</span><span class="sxs-lookup"><span data-stu-id="7e249-221">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span> <span data-ttu-id="7e249-222">Bağlamaları yapılandırma hakkında daha fazla bilgi için bkz: [Azure işlevleri Service Bus bağlamaları](functions-bindings-service-bus.md).</span><span class="sxs-lookup"><span data-stu-id="7e249-222">For more information on configuring bindings, see [Azure Functions Service Bus bindings](functions-bindings-service-bus.md).</span></span>

<span data-ttu-id="7e249-223">Merhaba öznitelikleri `[ServiceBusTrigger]` ve `[ServiceBus]` hello NuGet paketi tanımlanan [Microsoft.Azure.WebJobs.ServiceBus].</span><span class="sxs-lookup"><span data-stu-id="7e249-223">hello attributes `[ServiceBusTrigger]` and `[ServiceBus]` are defined in hello NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="7e249-224">Merhaba, hizmet veri yolu kuyruğu tetikleyici örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="7e249-224">hello following is an example of a Service Bus queue trigger:</span></span>

```csharp
[FunctionName("ServiceBusQueueTriggerCSharp")]                    
public static void Run([ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<span data-ttu-id="7e249-225">Merhaba, bağlama, hello yönteminin dönüş türü hello çıkış olarak kullanan bir hizmet veri yolu çıktısı örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="7e249-225">hello following is an example of a Service Bus output binding, using hello method return type as hello output:</span></span>

```csharp
[FunctionName("ServiceBusOutput")]
[return: ServiceBus("myqueue", Connection = "ServiceBusConnection")]
public static string ServiceBusOutput([HttpTrigger] dynamic input, TraceWriter log)
{
    log.Info($"C# function processed: {input.Text}");
    return input.Text;
}
```        

<a name="table"></a>

### <a name="table-storage-input-and-output"></a><span data-ttu-id="7e249-226">Tablo depolama giriş ve çıkış</span><span class="sxs-lookup"><span data-stu-id="7e249-226">Table storage input and output</span></span>

<span data-ttu-id="7e249-227">Giriş ve Azure tablo depolaması için bağlamaları çıktı Azure işlevleri destekler.</span><span class="sxs-lookup"><span data-stu-id="7e249-227">Azure Functions supports input and output bindings for Azure Table storage.</span></span> <span data-ttu-id="7e249-228">toolearn daha, fazla [Azure işlevleri tablo depolama bağlamaları](functions-bindings-storage-table.md).</span><span class="sxs-lookup"><span data-stu-id="7e249-228">toolearn more, see [Azure Functions Table storage bindings](functions-bindings-storage-table.md).</span></span>

<span data-ttu-id="7e249-229">Merhaba aşağıdaki örnekte bir tablo depolama çıkış ve giriş bağlamaları gösteren iki işlevlerle sınıftır.</span><span class="sxs-lookup"><span data-stu-id="7e249-229">hello following example is a class with two functions, demonstrating table storage output and input bindings.</span></span> 

```csharp
[StorageAccount("AzureWebJobsStorage")]
public class TableStorage
{
    public class MyPoco
    {
        public string PartitionKey { get; set; }
        public string RowKey { get; set; }
        public string Text { get; set; }
    }

    [FunctionName("TableOutput")]
    [return: Table("MyTable")]
    public static MyPoco TableOutput([HttpTrigger] dynamic input, TraceWriter log)
    {
        log.Info($"C# http trigger function processed: {input.Text}");
        return new MyPoco { PartitionKey = "Http", RowKey = Guid.NewGuid().ToString(), Text = input.Text };
    }

    // use hello metadata parameter "queueTrigger" toobind hello queue payload
    [FunctionName("TableInput")]
    public static void TableInput([QueueTrigger("table-items")] string input, [Table("MyTable", "Http", "{queueTrigger}")] MyPoco poco, TraceWriter log)
    {
        log.Info($"C# function processed: {poco.Text}");
    }
}

```

<a name="timer"></a>

### <a name="timer-trigger"></a><span data-ttu-id="7e249-230">Zamanlayıcı tetikleyicisi</span><span class="sxs-lookup"><span data-stu-id="7e249-230">Timer trigger</span></span>

<span data-ttu-id="7e249-231">Azure işlevleri tanımlanmış bir zamanlamaya göre işlevi kodunuzu çalıştırmak olanak sağlayan zamanlayıcı tetikleyicisi bağlama sahiptir.</span><span class="sxs-lookup"><span data-stu-id="7e249-231">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> <span data-ttu-id="7e249-232">toolearn hello bağlama hello özellikleri hakkında daha fazla bilgi görmek [zamanlama kod yürütmeyi Azure işlevleriyle](functions-bindings-timer.md).</span><span class="sxs-lookup"><span data-stu-id="7e249-232">toolearn more about hello features of hello binding, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>

<span data-ttu-id="7e249-233">Merhaba tüketim plan üzerinde zamanlamalarla tanımlayabilirsiniz bir [CRON ifade](http://en.wikipedia.org/wiki/Cron#CRON_expression).</span><span class="sxs-lookup"><span data-stu-id="7e249-233">On hello Consumption plan, you can define schedules with a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression).</span></span> <span data-ttu-id="7e249-234">Bir uygulama hizmeti planı kullanıyorsanız, bir TimeSpan dize de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e249-234">If you're using an App Service Plan, you can also use a TimeSpan string.</span></span> 

<span data-ttu-id="7e249-235">Aşağıdaki örnek hello her 5 dakikada bir zamanlayıcı tetikleyicisi tanımlar:</span><span class="sxs-lookup"><span data-stu-id="7e249-235">hello following example defines a timer trigger that runs every 5 minutes:</span></span>

```csharp
[FunctionName("TimerTriggerCSharp")]
public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
}
```

<a name="twilio"></a>

### <a name="twilio-output"></a><span data-ttu-id="7e249-236">Twilio çıkış</span><span class="sxs-lookup"><span data-stu-id="7e249-236">Twilio output</span></span>

<span data-ttu-id="7e249-237">Azure işlevleri destekler Twilio bağlamaları tooenable işlevleri toosend SMS metin iletileri çıktı.</span><span class="sxs-lookup"><span data-stu-id="7e249-237">Azure Functions supports Twilio output bindings tooenable your functions toosend SMS text messages.</span></span> <span data-ttu-id="7e249-238">toolearn daha, fazla [hello Twilio kullanarak Azure işlevlerden SMS gönder İleti çıkışı bağlama](functions-bindings-twilio.md).</span><span class="sxs-lookup"><span data-stu-id="7e249-238">toolearn more, see [Send SMS messages from Azure Functions using hello Twilio output binding](functions-bindings-twilio.md).</span></span> 

<span data-ttu-id="7e249-239">Merhaba özniteliği `[TwilioSms]` hello paketinde tanımlanan [Microsoft.Azure.WebJobs.Extensions.Twilio].</span><span class="sxs-lookup"><span data-stu-id="7e249-239">hello attribute `[TwilioSms]` is defined in hello package [Microsoft.Azure.WebJobs.Extensions.Twilio].</span></span>

<span data-ttu-id="7e249-240">Merhaba aşağıdaki C# örnek kullanan bir sıra tetikleyici ve bir Twilio çıkış bağlama:</span><span class="sxs-lookup"><span data-stu-id="7e249-240">hello following C# example uses a queue trigger and a Twilio output binding:</span></span>

```csharp
[FunctionName("QueueTwilio")]
[return: TwilioSms(AccountSidSetting = "TwilioAccountSid", AuthTokenSetting = "TwilioAuthToken", From = "+1425XXXXXXX" )]
public static SMSMessage Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] JObject order, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {order}");

    var message = new SMSMessage()
    {
        Body = $"Hello {order["name"]}, thanks for your order!",
        too= order["mobileNumber"].ToString()
    };

    return message;
}
```

## <a name="next-steps"></a><span data-ttu-id="7e249-241">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7e249-241">Next steps</span></span>

<span data-ttu-id="7e249-242">C# betik yazımı Azure işlevleri kullanma hakkında daha fazla bilgi için bkz: [Azure işlevleri C\# komut Geliştirici Başvurusu](functions-reference-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="7e249-242">For more information on using Azure Functions in C# scripting, see [Azure Functions C\# script developer reference](functions-reference-csharp.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


<!-- NuGet packages --> 
[Microsoft.Azure.WebJobs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.DocumentDB]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB/1.1.0-beta1
[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.MobileApps]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps/1.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs/1.1.0-beta1
[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.SendGrid]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.Http]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http/1.0.0-beta1
[Microsoft.Azure.WebJobs.Extensions.BotFramework]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.BotFramework/1.0.15-beta
[Microsoft.Azure.WebJobs.Extensions.ApiHub]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ApiHub/1.0.0-beta4
[Microsoft.Azure.WebJobs.Extensions.Twilio]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio/1.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions/2.1.0-beta1


<!-- Links toosource --> 
[DocumentDBAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs
[EventHubAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs
[EventHubTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs
[MobileTableAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs
[NotificationHubAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs 
[ServiceBusAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs
[ServiceBusAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs
[QueueAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs
[StorageAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs
[BlobAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs
[TableAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs
[TwilioSmsAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs
[SendGridAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs
[HttpTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs
[ApiHubFileAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.ApiHub/ApiHubFileAttribute.cs
[TimerTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs
