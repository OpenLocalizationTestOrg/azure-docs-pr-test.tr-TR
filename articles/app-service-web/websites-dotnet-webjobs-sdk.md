---
title: Azure WebJobs SDK nedir?
description: "Azure WebJobs SDK Giriş. SDK nedir, yararlıdır ve kod örnekleri tipik senaryolar açıklanmaktadır."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 8281267b-572b-4b14-a328-6704493ea682
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 8eb05b7cbfb4505f2e94c5b8e6d367ec63a2f033
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-the-azure-webjobs-sdk"></a><span data-ttu-id="88676-104">Azure WebJobs SDK nedir?</span><span class="sxs-lookup"><span data-stu-id="88676-104">What is the Azure WebJobs SDK</span></span>
## <span data-ttu-id="88676-105"><a id="overview"></a>Genel bakış</span><span class="sxs-lookup"><span data-stu-id="88676-105"><a id="overview"></a>Overview</span></span>
<span data-ttu-id="88676-106">Bu makalede WebJobs SDK nedir açıklanmakta, bazı ortak senaryolar için faydalı olur ve kodunuzda kullanma hakkında genel bir bakış sunar inceler.</span><span class="sxs-lookup"><span data-stu-id="88676-106">This article explains what the WebJobs SDK is, reviews some common scenarios it is useful for, and gives an overview of how you use it in your code.</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="88676-107">[Web işleri](websites-webjobs-resources.md) bir web uygulaması, API uygulaması veya mobil uygulama olarak aynı bağlamda bir program veya komut dosyasını çalıştırmanıza olanak sağlayan bir Azure uygulama hizmeti özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="88676-107">[WebJobs](websites-webjobs-resources.md) is a feature of Azure App Service that enables you to run a program or script in the same context as a web app, API app, or mobile app.</span></span> <span data-ttu-id="88676-108">Amacı [WebJobs SDK](websites-webjobs-resources.md) bir Web işi gerçekleştirebilirsiniz, görüntü işleme, sıra işleme, RSS toplama, dosya bakımı gibi ortak görevler için yazdığınız kodları kolaylaştırmaktır ve e-postaları gönderme.</span><span class="sxs-lookup"><span data-stu-id="88676-108">The purpose of the [WebJobs SDK](websites-webjobs-resources.md) is to simplify the code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span></span> <span data-ttu-id="88676-109">Web işleri SDK'si, Azure Storage ve Service Bus ile çalışmak için görev zamanlama ve hataları işleme ve diğer birçok yaygın senaryolar için yerleşik özellikler vardır.</span><span class="sxs-lookup"><span data-stu-id="88676-109">The WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span></span> <span data-ttu-id="88676-110">Ayrıca, Genişletilebilir olmak için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="88676-110">In addition, it's designed to be extensible.</span></span> <span data-ttu-id="88676-111">[Web işleri SDK'si açık kaynak olan](https://github.com/Azure/azure-webjobs-sdk/)ve bir [uzantıları için açık kaynak deposu](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span><span class="sxs-lookup"><span data-stu-id="88676-111">The [WebJobs SDK is open source](https://github.com/Azure/azure-webjobs-sdk/), and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span></span>

<span data-ttu-id="88676-112">WebJobs SDK aşağıdaki bileşenleri içerir:</span><span class="sxs-lookup"><span data-stu-id="88676-112">The WebJobs SDK includes the following components:</span></span>

* <span data-ttu-id="88676-113">**NuGet paketlerini**.</span><span class="sxs-lookup"><span data-stu-id="88676-113">**NuGet packages**.</span></span> <span data-ttu-id="88676-114">Visual Studio konsol uygulaması projesine ekleyin NuGet paketlerini yöntemlerinizi Web işleri SDK'si özniteliklerle tasarlayarak kodunuzun kullandığı bir çerçeve sağlar.</span><span class="sxs-lookup"><span data-stu-id="88676-114">NuGet packages that you add to a Visual Studio Console Application project provide a framework that your code uses by decorating your methods with WebJobs SDK attributes.</span></span>
* <span data-ttu-id="88676-115">**Pano**.</span><span class="sxs-lookup"><span data-stu-id="88676-115">**Dashboard**.</span></span> <span data-ttu-id="88676-116">WebJobs SDK parçası Azure App Service içinde bulunur ve zengin izleme ve tanılama NuGet paketlerini kullanan programlar için sağlar.</span><span class="sxs-lookup"><span data-stu-id="88676-116">Part of the WebJobs SDK is included in Azure App Service and provides rich monitoring and diagnostics for programs that use the NuGet packages.</span></span> <span data-ttu-id="88676-117">Bu izleme ve tanılama özellikleri kullanmak için kod yazmak zorunda değilsiniz.</span><span class="sxs-lookup"><span data-stu-id="88676-117">You don't have to write code to use these monitoring and diagnostics features.</span></span>

## <span data-ttu-id="88676-118"><a id="scenarios"></a>Senaryoları</span><span class="sxs-lookup"><span data-stu-id="88676-118"><a id="scenarios"></a>Scenarios</span></span>
<span data-ttu-id="88676-119">Azure WebJobs SDK ile daha kolay işleyebilir bazı tipik senaryolar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="88676-119">Here are some typical scenarios you can handle more easily with the Azure WebJobs SDK:</span></span>

* <span data-ttu-id="88676-120">İşlem ya da diğer CPU yoğunluklu iş görüntü.</span><span class="sxs-lookup"><span data-stu-id="88676-120">Image processing or other CPU-intensive work.</span></span> <span data-ttu-id="88676-121">Bir ortak Web siteleri görüntüler veya videoları karşıya yükleme olanağı özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="88676-121">A common feature of websites is the ability to upload images or videos.</span></span> <span data-ttu-id="88676-122">Genellikle, karşıya ancak bunu bekleyin kullanıcı yapmak istemiyorsanız sonra içeriği işlemek istersiniz.</span><span class="sxs-lookup"><span data-stu-id="88676-122">Often you want to manipulate the content after it's uploaded, but you don't want to make the user wait while you do that.</span></span>
* <span data-ttu-id="88676-123">Sıranın işleme.</span><span class="sxs-lookup"><span data-stu-id="88676-123">Queue processing.</span></span> <span data-ttu-id="88676-124">Arka uç hizmeti ile iletişim kurmak web ön uç için yaygın bir yolu sıraları kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="88676-124">A common way for a web frontend to communicate with a backend service is to use queues.</span></span> <span data-ttu-id="88676-125">Web sitesi işlerini halletmek ihtiyaç duyduğunda üzerine bir sıraya bir ileti iter.</span><span class="sxs-lookup"><span data-stu-id="88676-125">When the website needs to get work done, it pushes a message onto a queue.</span></span> <span data-ttu-id="88676-126">Arka uç hizmeti sırasından ileti çeker ve çalışır.</span><span class="sxs-lookup"><span data-stu-id="88676-126">A backend service pulls messages from the queue and does the work.</span></span> <span data-ttu-id="88676-127">Görüntü işleme için kuyrukları kullanabilirsiniz: kullanıcı dosya sayısı gönderildikten sonra Örneğin, dosya adları bir kuyruk iletisi işleme için arka uç tarafından çekilmesi yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="88676-127">You could use queues for image processing: for example, after the user uploads a number of files, put the file names in a queue message to be picked up by the backend for processing.</span></span> <span data-ttu-id="88676-128">Veya site yanıt hızını artırmak için kuyrukları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88676-128">Or you could use queues to improve site responsiveness.</span></span> <span data-ttu-id="88676-129">Örneğin, bir SQL veritabanına doğrudan yazmak yerine, bir kuyruğa işiniz bittiğinde, kullanıcıya bildir yazma ve iş arka uç hizmeti tanıtıcı Yüksek gecikmeli ilişkisel veritabanı izin verin.</span><span class="sxs-lookup"><span data-stu-id="88676-129">For example, instead of writing directly to a SQL database, write to a queue, tell the user you're done, and let the backend service handle high-latency relational database work.</span></span> <span data-ttu-id="88676-130">Görüntü işlemine işleme sırası örneği için bkz: [WebJobs SDK Başlarken Öğreticisi](websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="88676-130">For an example of queue processing with image process, see the [WebJobs SDK Get Started tutorial](websites-dotnet-webjobs-sdk-get-started.md).</span></span>
* <span data-ttu-id="88676-131">RSS toplama.</span><span class="sxs-lookup"><span data-stu-id="88676-131">RSS aggregation.</span></span> <span data-ttu-id="88676-132">RSS akışları listesini tutar bir siteniz varsa, tüm arka plan işlemi akışlarında makalelerinden çekme.</span><span class="sxs-lookup"><span data-stu-id="88676-132">If you have a site that maintains a list of RSS feeds, you could pull in all of the articles from the feeds in a background process.</span></span>
* <span data-ttu-id="88676-133">Dosya bakımı, toplama veya günlük dosyalarını temizleme gibi.</span><span class="sxs-lookup"><span data-stu-id="88676-133">File maintenance, such as aggregating or cleaning up log files.</span></span>  <span data-ttu-id="88676-134">Bazı siteler tarafından veya bunlar üzerinde analiz işlerini çalıştırmak için birleştirmek istediğiniz ayrı zaman aralıkları için oluşturulan günlük dosyalarını olabilir.</span><span class="sxs-lookup"><span data-stu-id="88676-134">You might have log files being created by several sites or for separate time spans which you want to combine in order to run analysis jobs on them.</span></span> <span data-ttu-id="88676-135">Veya, eski günlük dosyaları temizlemek için haftalık çalıştırmak için bir görev zamanlama isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88676-135">Or you might want to schedule a task to run weekly to clean up old log files.</span></span>
* <span data-ttu-id="88676-136">Giriş Azure tablolara.</span><span class="sxs-lookup"><span data-stu-id="88676-136">Ingress into Azure Tables.</span></span> <span data-ttu-id="88676-137">Depolanan dosyaların ve blobları sahip ve bunları ayrıştırma ve tablolarındaki verileri depolamak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="88676-137">You might have files stored and blobs and want to parse them and store the data in tables.</span></span> <span data-ttu-id="88676-138">Giriş işlevi çok sayıda satır (bazı durumlarda milyonlarca) yazmak ve Web işleri SDK'si, bu işlev kolayca uygulamak mümkün kılar.</span><span class="sxs-lookup"><span data-stu-id="88676-138">The ingress function could be writing lots of rows (millions in some cases), and the WebJobs SDK makes it possible to implement this functionality easily.</span></span> <span data-ttu-id="88676-139">SDK, ayrıca İlerleme göstergesi tabloda yazılmış satır sayısı gibi gerçek zamanlı izlenmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="88676-139">The SDK also provides real-time monitoring of progress indicators such as the number of rows written in the table.</span></span>
* <span data-ttu-id="88676-140">Arka plan iş parçacığında, çalıştırmak istediğiniz diğer uzun süre çalışan görevler [e-postaları gönderme](https://github.com/victorhurdugaci/AzureWebJobsSamples/tree/master/SendEmailOnFailure).</span><span class="sxs-lookup"><span data-stu-id="88676-140">Other long-running tasks that you want to run in a background thread, such as [sending emails](https://github.com/victorhurdugaci/AzureWebJobsSamples/tree/master/SendEmailOnFailure).</span></span> 
* <span data-ttu-id="88676-141">Yedekleme işlemi her gece gerçekleştirme gibi bir zamanlamaya göre çalıştırmak istediğiniz herhangi bir görevi.</span><span class="sxs-lookup"><span data-stu-id="88676-141">Any tasks that you want to run on a schedule, such as performing a back-up operation every night.</span></span>

<span data-ttu-id="88676-142">Bu senaryolar çoğunu birden çok Web işleri aynı anda çalıştırırsınız: birden çok VM çalıştırmak için bir web uygulaması ölçeklendirme isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88676-142">In many of these scenarios you may want to scale a web app to run on multiple VMs, which would run multiple WebJobs simultaneously.</span></span> <span data-ttu-id="88676-143">Bazı senaryolarda bu birden çok kez işlenen aynı veri kaybına neden, ancak yerleşik sırası, blob ve WebJobs SDK, Service Bus Tetikleyicileri kullandığınızda bu bir sorun değildir.</span><span class="sxs-lookup"><span data-stu-id="88676-143">In some scenarios this could result in the same data getting processed multiple times, but this is not a problem when you use the built-in queue, blob, and Service Bus triggers of the WebJobs SDK.</span></span> <span data-ttu-id="88676-144">SDK işlevlerinizi yalnızca bir kez her ileti veya blob işleneceğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="88676-144">The SDK ensures that your functions will be processed only once for each message or blob.</span></span>

<span data-ttu-id="88676-145">WebJobs SDK Ayrıca ortak hata senaryoları işleme işlemek kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="88676-145">The WebJobs SDK also makes it easy to handle common error handling scenarios.</span></span> <span data-ttu-id="88676-146">Bir işlev işlemi başarısız olur ve zaman aşımları belirtilen süre sınırı içinde tamamlanmazsa bir işlev otomatik olarak iptal ayarlayabilirsiniz bildirimleri göndermek için uyarıları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="88676-146">You can set up alerts to send notifications when a function fails, and you can set timeouts so that a function is automatically canceled if it doesn't complete within a specified time limit.</span></span>

## <span data-ttu-id="88676-147"><a id="code"></a>Kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="88676-147"><a id="code"></a> Code samples</span></span>
<span data-ttu-id="88676-148">Azure Storage ile çalışma genel görevler işlemek için kod basittir.</span><span class="sxs-lookup"><span data-stu-id="88676-148">The code for handling typical tasks that work with Azure Storage is simple.</span></span> <span data-ttu-id="88676-149">Konsol uygulamanızın içinde `Main` yöntemi, oluşturduğunuz bir `JobHost` yazma yöntemleri çağrıları koordine eden nesne.</span><span class="sxs-lookup"><span data-stu-id="88676-149">In your Console Application's `Main` method you create a `JobHost` object that coordinates the calls to methods you write.</span></span> <span data-ttu-id="88676-150">Web işleri SDK'si framework yöntemlerinizi çağrısının ne zaman ve ne kullanılacak parametre değerlerini bunları kullandığınız Web işleri SDK'si özniteliklerini temel alarak bilir.</span><span class="sxs-lookup"><span data-stu-id="88676-150">The WebJobs SDK framework knows when to call your methods and what parameter values to use based on the WebJobs SDK attributes you use in them.</span></span> <span data-ttu-id="88676-151">SDK sağlar *Tetikleyicileri* belirten çağrılacak, işlev hangi koşullar neden ve *bağlayıcıları* bilgilerin içine ve dışına yöntem parametreleri nasıl alınacağını belirtin.</span><span class="sxs-lookup"><span data-stu-id="88676-151">The SDK provides *triggers* that specify what conditions cause the function to be called, and *binders* that specify how to get information into and out of method parameters.</span></span>

<span data-ttu-id="88676-152">Örneğin, [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md) özniteliği neden olan bir sırada bir ileti aldı ve ileti biçimi JSON bir bayt dizisi veya özel bir tür için ileti otomatik olarak seri durumdan çıkarılmış ise, çağrılacak işlev.</span><span class="sxs-lookup"><span data-stu-id="88676-152">For example, the [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md) attribute causes a function to be called when a message is received on a queue, and if the message format is JSON for a byte array or a custom type, the message is automatically deserialized.</span></span> <span data-ttu-id="88676-153">[BlobTrigger](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) özniteliği, yeni blob Azure depolama hesabınız oluşturulduğunda bir işlem tetikler.</span><span class="sxs-lookup"><span data-stu-id="88676-153">The [BlobTrigger](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) attribute triggers a process whenever a new blob is created in an Azure Storage account.</span></span>

<span data-ttu-id="88676-154">Bir kuyruk yoklar ve alınan her kuyruk iletisi için bir blob oluşturan basit bir program şöyledir:</span><span class="sxs-lookup"><span data-stu-id="88676-154">Here is a simple program that polls a queue and creates a blob for each queue message received:</span></span>

        public static void Main()
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)
        {
            writer.WriteLine(inputText);
        }

<span data-ttu-id="88676-155">`JobHost` Nesnesi bir arka plan işlevler kümesi için bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="88676-155">The `JobHost` object is a container for a set of background functions.</span></span> <span data-ttu-id="88676-156">`JobHost` Nesne İşlevler, Gözcü bunları tetikleyen olayları izler ve tetikleyici olaylar meydana geldiğinde işlevleri yürütür.</span><span class="sxs-lookup"><span data-stu-id="88676-156">The `JobHost` object monitors the functions, watches for events that trigger them, and executes the functions when trigger events occur.</span></span> <span data-ttu-id="88676-157">Çağırmanız bir `JobHost` yöntemi geçerli iş parçacığının veya bir arka plan iş parçacığı çalışmaya kapsayıcı işlem isteyip istemediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="88676-157">You call a `JobHost` method to indicate whether you want the container process to run on the current thread or a background thread.</span></span> <span data-ttu-id="88676-158">Örnekte, `RunAndBlock` yöntemi çalışan işlemi sürekli olarak geçerli iş parçacığı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="88676-158">In the example, the `RunAndBlock` method runs the process continuously on the current thread.</span></span>

<span data-ttu-id="88676-159">Çünkü `ProcessQueueMessage` yöntemi bu örnekte sahip bir `QueueTrigger` özniteliği, tetikleyici bu işlevi yeni bir kuyruk iletisi alınması için.</span><span class="sxs-lookup"><span data-stu-id="88676-159">Because the `ProcessQueueMessage` method in this example has a `QueueTrigger` attribute, the trigger for that function is the reception of a new queue message.</span></span> <span data-ttu-id="88676-160">`JobHost` Nesne izleyen yeni bir kuyruk iletisi belirtilen sırada (Bu örnekte "webjobsqueue") için ve biri bulunduğunda, çağıran `ProcessQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="88676-160">The `JobHost` object watches for new queue messages on the specified queue ("webjobsqueue" in this sample) and when one is found, it calls `ProcessQueueMessage`.</span></span> 

<span data-ttu-id="88676-161">`QueueTrigger` Özniteliği bağlamalar `inputText` kuyruk iletisini değeri parametresi.</span><span class="sxs-lookup"><span data-stu-id="88676-161">The `QueueTrigger` attribute binds the `inputText` parameter to the value of the queue message.</span></span> <span data-ttu-id="88676-162">Ve `Blob` özniteliği bağlamalar bir `TextWriter` "containername" adlı bir kapsayıcı "blobname" adlı bir blob nesnesi.</span><span class="sxs-lookup"><span data-stu-id="88676-162">And the `Blob` attribute binds a `TextWriter` object to a blob named "blobname" in a container named "containername".</span></span>  

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")]] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)

<span data-ttu-id="88676-163">İşlevi bu parametreler için blob kuyruk iletisini değerini yazmak için sonra kullanır:</span><span class="sxs-lookup"><span data-stu-id="88676-163">The function then uses these parameters to write the value of the queue message to the blob:</span></span>

        writer.WriteLine(inputText);

<span data-ttu-id="88676-164">WebJobs SDK tetikleyici ve bağlayıcı özelliklerini yazmak zorunda kod büyük ölçüde basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="88676-164">The trigger and binder features of the WebJobs SDK greatly simplify the code you have to write.</span></span> <span data-ttu-id="88676-165">Kuyruklar, BLOB'lar veya dosyalarını işlemek için veya zamanlanmış görevler başlatmak için gereken alt düzey kodu sizin için Web işleri SDK'si çerçevesi tarafından yapılır.</span><span class="sxs-lookup"><span data-stu-id="88676-165">The low-level code required to process queues, blobs, or files, or to initiate scheduled tasks, is done for you by the WebJobs SDK framework.</span></span> <span data-ttu-id="88676-166">Örneğin, framework açılır henüz yoksa sıraları kuyruk oluşturur, iletileri okuma kuyruk, işleme tamamlandı, yoksa blob kapsayıcıları oluşturur henüz BLOB'lar vb. için yazar zaman siler iletileri kuyruğa.</span><span class="sxs-lookup"><span data-stu-id="88676-166">For example, the framework creates queues that don't exist yet, opens the queue, reads queue messages, deletes queue messages when processing is completed, creates blob containers that don't exist yet, writes to blobs, and so on.</span></span>

<span data-ttu-id="88676-167">Aşağıdaki kod örneğinde bir WebJob içinde Tetikleyicileri çeşitli gösterir: `QueueTrigger`, `FileTrigger`, `WebHookTrigger`, ve `ErrorTrigger`.</span><span class="sxs-lookup"><span data-stu-id="88676-167">The following code example shows a variety of triggers in one WebJob: `QueueTrigger`, `FileTrigger`, `WebHookTrigger`, and `ErrorTrigger`.</span></span> 

```
    public class Functions
    {
        public static void ProcessQueueMessage([QueueTrigger("queue")] string message,
        TextWriter log)
        {
            log.WriteLine(message);
        }

        public static void ProcessFileAndUploadToBlob(
            [FileTrigger(@"import\{name}", "*.*", autoDelete: true)] Stream file,
            [Blob(@"processed/{name}", FileAccess.Write)] Stream output,
            string name,
            TextWriter log)
        {
            output = file;
            file.Close();
            log.WriteLine(string.Format("Processed input file '{0}'!", name));
        }

        [Singleton]
        public static void ProcessWebHookA([WebHookTrigger] string body, TextWriter log)
        {
            log.WriteLine(string.Format("WebHookA invoked! Body: {0}", body));
        }

        public static void ProcessGitHubWebHook([WebHookTrigger] string body, TextWriter log)
        {
            dynamic issueEvent = JObject.Parse(body);
            log.WriteLine(string.Format("GitHub WebHook invoked! ('{0}', '{1}')",
                issueEvent.issue.title, issueEvent.action));
        }

        public static void ErrorMonitor(
        [ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
        [SendGrid(
            To = "admin@emailaddress.com",
            Subject = "Error!")]
         SendGridMessage message)
        {
            // log last 5 detailed errors to the Dashboard
            log.WriteLine(filter.GetDetailedMessage(5));
            message.Text = filter.GetDetailedMessage(1);
        }
    }
```

## <span data-ttu-id="88676-168"><a id="schedule"></a>Zamanlama</span><span class="sxs-lookup"><span data-stu-id="88676-168"><a id="schedule"></a> Scheduling</span></span>
<span data-ttu-id="88676-169">`TimerTrigger` Özniteliği imkanı sunar, tetikleyici işlevlere bir zamanlamaya göre çalıştır.</span><span class="sxs-lookup"><span data-stu-id="88676-169">The `TimerTrigger` attribute gives you the ability to trigger functions to run on a schedule.</span></span> <span data-ttu-id="88676-170">WebJobs SDK'yı kullanarak bir Web işinin Azure veya zamanlama tekil işlevler aracılığıyla bir bütün olarak bir Web işi zamanlama `TimerTrigger`.</span><span class="sxs-lookup"><span data-stu-id="88676-170">You can schedule a WebJob as a whole through Azure or schedule individual functions of a WebJob using the WebJobs SDK `TimerTrigger`.</span></span> <span data-ttu-id="88676-171">Kod örneği aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="88676-171">Here's a code sample.</span></span>

```
public class Functions
{
    public static void ProcessTimer([TimerTrigger("*/15 * * * * *", RunOnStartup = true)]
    TimerInfo info, [Queue("queue")] out string message)
    {
        message = info.FormatNextOccurrences(1);
    }
}
```

<span data-ttu-id="88676-172">Daha fazla örnek kod için bkz: [TimerSamples.cs](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/ExtensionsSample/Samples/TimerSamples.cs) Github.com'u üzerinde azure webjobs sdk uzantıları deposunda.</span><span class="sxs-lookup"><span data-stu-id="88676-172">For more sample code, see [TimerSamples.cs](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/ExtensionsSample/Samples/TimerSamples.cs) in the azure-webjobs-sdk-extensions repository on GitHub.com.</span></span>

## <a name="extensibility"></a><span data-ttu-id="88676-173">Genişletilebilirlik</span><span class="sxs-lookup"><span data-stu-id="88676-173">Extensibility</span></span>
<span data-ttu-id="88676-174">Yerleşik işlevselliği--sınırlı değil WebJobs SDK özel tetikleyiciler ve bağlayıcıları yazmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="88676-174">You're not limited to built-in functionality -- the WebJobs SDK allows you to write custom triggers and binders.</span></span>  <span data-ttu-id="88676-175">Örneğin, önbellek olayları ve düzenli zamanlamaları Tetikleyicileri yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88676-175">For example, you can write triggers for cache events and periodic schedules.</span></span> <span data-ttu-id="88676-176">Bir [açık kaynak deposu](https://github.com/Azure/azure-webjobs-sdk-extensions) içeren bir [WebJobs SDK genişletilebilirlik hakkında ayrıntılı kılavuz](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) ve yardımcı olması için örnek kod başlatılan kendi Tetikleyicileri ve bağlayıcıları yazma.</span><span class="sxs-lookup"><span data-stu-id="88676-176">An [open source repository](https://github.com/Azure/azure-webjobs-sdk-extensions) contains a [detailed guide on WebJobs SDK extensibility](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) and sample code to help get you started writing your own triggers and binders.</span></span>

## <span data-ttu-id="88676-177"><a id="workerrole"></a>Web işleri dışında WebJobs SDK'sını kullanarak</span><span class="sxs-lookup"><span data-stu-id="88676-177"><a id="workerrole"></a>Using the WebJobs SDK outside of WebJobs</span></span>
<span data-ttu-id="88676-178">Kullanan bir programı Web işleri SDK'si standart bir konsol uygulamasıdır ve her yerden çalıştırabilirsiniz--Web işi çalıştırmak sahip değil.</span><span class="sxs-lookup"><span data-stu-id="88676-178">A program that uses the the WebJobs SDK is a standard Console Application and can run anywhere -- it doesn't have to run as a WebJob.</span></span> <span data-ttu-id="88676-179">Program geliştirme bilgisayarınızda yerel olarak sınayabilirsiniz ve bu ortamlarda birini tercih ederseniz üretimde bir bulut hizmeti çalışan rolü veya bir Windows hizmeti çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88676-179">You can test the program locally on your development computer, and in production you can run it in a Cloud Service worker role or a Windows service if you prefer one of those environments.</span></span> 

<span data-ttu-id="88676-180">Ancak, Pano yalnızca bir Azure App Service web uygulaması için bir uzantı olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="88676-180">However, the dashboard is only available as an extension for an Azure App Service web app.</span></span> <span data-ttu-id="88676-181">Bir Web işi dışında çalıştırın ve panoyu kullanmaya devam istiyorsanız, WebJobs SDK Pano bağlantı dizenizi başvurduğu ve web uygulamanızın Web işleri Panosu'nu sonra işlevi yürütme hakkındaki verileri gösterecek aynı depolama hesabı kullanmak için bir web uygulaması yapılandırabilirsiniz programınızdan, başka bir yere çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="88676-181">If you want to run outside of a WebJob and still use the Dashboard, you can configure a web app to use the same storage account that your WebJobs SDK Dashboard connection string refers to, and that web app's WebJobs Dashboard will then show data about function execution from your program that is running somewhere else.</span></span> <span data-ttu-id="88676-182">URL https:// kullanarak panoya alabilirsiniz*{webappname}*.scm.azurewebsites.net/azurejobs/#/functions.</span><span class="sxs-lookup"><span data-stu-id="88676-182">You can get to the Dashboard by using the URL https://*{webappname}*.scm.azurewebsites.net/azurejobs/#/functions.</span></span> <span data-ttu-id="88676-183">Daha fazla bilgi için bkz: [WebJobs SDK ile yerel geliştirme için bir Pano alma](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), ancak blog postası eski bir bağlantı dizesi adı gösterdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="88676-183">For more information, see [Getting a dashboard for local development with the WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that the blog post shows an old connection string name.</span></span> 

## <span data-ttu-id="88676-184"><a id="nostorage"></a>Pano özellikleri</span><span class="sxs-lookup"><span data-stu-id="88676-184"><a id="nostorage"></a>Dashboard features</span></span>
<span data-ttu-id="88676-185">Web işleri SDK'si Tetikleyicileri veya bağlayıcıları kullanmayın olsa bile WebJobs SDK çeşitli avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="88676-185">The WebJobs SDK provides several advantages even if you don't use WebJobs SDK triggers or binders:</span></span>

* <span data-ttu-id="88676-186">Panodan işlevleri çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="88676-186">You can invoke functions from the Dashboard.</span></span>
* <span data-ttu-id="88676-187">Panodan işlevleri oynatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88676-187">You can replay functions from the Dashboard.</span></span>
* <span data-ttu-id="88676-188">Belirli Web işi (Console.Out, Console.Error, izleme, vb. kullanılarak yazılmış uygulama günlükleri) ile bağlantılı ya da bunları oluşturulan belirli işlevi çağırma bağlı panosundaki günlüklerini görüntüleyebilirsiniz (günlükleri kullanılarak yazılmış bir `TextWriter` nesnesi SDK işlevi için parametre olarak geçtiğini).</span><span class="sxs-lookup"><span data-stu-id="88676-188">You can view logs in the Dashboard, linked to the particular WebJob (application logs, written by using Console.Out, Console.Error, Trace, etc.) or linked to the particular function invocation that generated them (logs written by using a `TextWriter` object that the SDK passes to the function as a parameter).</span></span> 

<span data-ttu-id="88676-189">Daha fazla bilgi için bkz: [el ile bir işlevi çağırmak nasıl](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual) ve [nasıl günlüklerini yazma](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)</span><span class="sxs-lookup"><span data-stu-id="88676-189">For more information, see [How to manually invoke a function](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual) and [How to write logs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)</span></span> 

## <span data-ttu-id="88676-190"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="88676-190"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="88676-191">WebJobs SDK'sı hakkında daha fazla bilgi için bkz: [Azure Web işleri önerilen kaynakları](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="88676-191">For more information about the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

<span data-ttu-id="88676-192">WebJobs SDK'sının en son geliştirmeleri hakkında daha fazla bilgi için bkz: [sürüm notları](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes).</span><span class="sxs-lookup"><span data-stu-id="88676-192">For information about the latest enhancements to the WebJobs SDK, see the [Release Notes](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes).</span></span>

