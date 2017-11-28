---
title: ".NET ile Media Services iş bildirimleri izlemek için Azure kuyruk depolama kullanma | Microsoft Docs"
description: "Media Services iş bildirimleri izlemek için Azure kuyruk depolama kullanmayı öğrenin. Kod örneği C# dilinde yazılmıştır ve .NET için Media Services SDK'sını kullanır."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: f535d0b5-f86c-465f-81c6-177f4f490987
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/14/2017
ms.author: juliako
ms.openlocfilehash: 5ee89d0ae4c3c56d164aff4e321ee99f015ba4fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-queue-storage-to-monitor-media-services-job-notifications-with-net"></a><span data-ttu-id="a20e3-104">.NET ile Media Services iş bildirimleri izlemek için Azure kuyruk depolama kullanma</span><span class="sxs-lookup"><span data-stu-id="a20e3-104">Use Azure Queue storage to monitor Media Services job notifications with .NET</span></span>
<span data-ttu-id="a20e3-105">Kodlama işleri çalıştırdığınızda, genellikle iş ilerleme durumunu izlemek için bir yol gerekir.</span><span class="sxs-lookup"><span data-stu-id="a20e3-105">When you run encoding jobs, you often require a way to track job progress.</span></span> <span data-ttu-id="a20e3-106">Media Services'ı için bildirimleri göndermeyi yapılandırabilirsiniz [Azure kuyruk depolama](../storage/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="a20e3-106">You can configure Media Services to deliver notifications to [Azure Queue storage](../storage/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="a20e3-107">Kuyruk depolama biriminden bildirimleri alarak iş ilerleme durumunu izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a20e3-107">You can monitor job progress by getting notifications from the Queue storage.</span></span> 

<span data-ttu-id="a20e3-108">Kuyruk depolama için teslim edilen ileti herhangi bir yere dünyada erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="a20e3-108">Messages delivered to Queue storage can be accessed from anywhere in the world.</span></span> <span data-ttu-id="a20e3-109">Kuyruk depolama Mesajlaşma mimarisi, güvenilir ve yüksek oranda ölçeklenebilir.</span><span class="sxs-lookup"><span data-stu-id="a20e3-109">The Queue storage messaging architecture is reliable and highly scalable.</span></span> <span data-ttu-id="a20e3-110">Kuyruk depolama iletileri için yoklama diğer yöntemleri kullanmayı üzerinden önerilir.</span><span class="sxs-lookup"><span data-stu-id="a20e3-110">Polling Queue storage for messages is recommended over using other methods.</span></span>

<span data-ttu-id="a20e3-111">Media Services bildirimleri göndermek için dinleme yaygın bir senaryo, bazı ek görevi gerçekleştirmek için gereken bir içerik yönetim sistemi geliştiriyorsanız (örneğin, bir iş akışı bir sonraki adımda tetiklemek için ya da içerik yayımlamak için) bir kodlama işi tamamlar ' dir.</span><span class="sxs-lookup"><span data-stu-id="a20e3-111">One common scenario for listening to Media Services notifications is if you are developing a content management system that needs to perform some additional task after an encoding job completes (for example, to trigger the next step in a workflow, or to publish content).</span></span>

<span data-ttu-id="a20e3-112">Bu konu, kuyruk depolama biriminden bildirim iletilerini alma gösterir.</span><span class="sxs-lookup"><span data-stu-id="a20e3-112">This topic shows how to get notification messages from Queue storage.</span></span>  

## <a name="considerations"></a><span data-ttu-id="a20e3-113">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="a20e3-113">Considerations</span></span>
<span data-ttu-id="a20e3-114">Kuyruk depolama kullanma Media Services uygulamaları geliştirirken, aşağıdakileri dikkate alın:</span><span class="sxs-lookup"><span data-stu-id="a20e3-114">Consider the following when developing Media Services applications that use Queue storage:</span></span>

* <span data-ttu-id="a20e3-115">Kuyruk depolama ilk olarak ilk çıkar garanti sağlamaz (FIFO) sıralı teslim.</span><span class="sxs-lookup"><span data-stu-id="a20e3-115">Queue storage does not provide a guarantee of first-in-first-out (FIFO) ordered delivery.</span></span> <span data-ttu-id="a20e3-116">Daha fazla bilgi için bkz: [Azure kuyrukları ve Azure hizmet veri yolu kuyrukları karşılaştırıldığında ve Contrasted](https://msdn.microsoft.com/library/azure/hh767287.aspx).</span><span class="sxs-lookup"><span data-stu-id="a20e3-116">For more information, see [Azure Queues and Azure Service Bus Queues Compared and Contrasted](https://msdn.microsoft.com/library/azure/hh767287.aspx).</span></span>
* <span data-ttu-id="a20e3-117">Kuyruk depolama gönderme hizmeti değil.</span><span class="sxs-lookup"><span data-stu-id="a20e3-117">Queue storage is not a push service.</span></span> <span data-ttu-id="a20e3-118">Sıranın yoklaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a20e3-118">You have to poll the queue.</span></span>
* <span data-ttu-id="a20e3-119">Herhangi bir sayıda sıralar olabilir.</span><span class="sxs-lookup"><span data-stu-id="a20e3-119">You can have any number of queues.</span></span> <span data-ttu-id="a20e3-120">Daha fazla bilgi için bkz: [kuyruk hizmeti REST API'si](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="a20e3-120">For more information, see [Queue Service REST API](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API).</span></span>
* <span data-ttu-id="a20e3-121">Kuyruk depolama bazı kısıtlamalar ve dikkat edilmesi gereken özellikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="a20e3-121">Queue storage has some limitations and specifics to be aware of.</span></span> <span data-ttu-id="a20e3-122">Bunlar [Azure kuyrukları ve Azure hizmet veri yolu kuyrukları karşılaştırıldığında ve Contrasted](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted).</span><span class="sxs-lookup"><span data-stu-id="a20e3-122">These are described in [Azure Queues and Azure Service Bus Queues Compared and Contrasted](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted).</span></span>

## <a name="net-code-example"></a><span data-ttu-id="a20e3-123">.NET kodu örneği</span><span class="sxs-lookup"><span data-stu-id="a20e3-123">.NET code example</span></span>

<span data-ttu-id="a20e3-124">Bu bölümde aşağıdaki kod örneğinde şunları yapar:</span><span class="sxs-lookup"><span data-stu-id="a20e3-124">The code example in this section does the following:</span></span>

1. <span data-ttu-id="a20e3-125">Tanımlar **EncodingJobMessage** bildirim iletisi biçimine eşleyen sınıfı.</span><span class="sxs-lookup"><span data-stu-id="a20e3-125">Defines the **EncodingJobMessage** class that maps to the notification message format.</span></span> <span data-ttu-id="a20e3-126">Kod nesnelerin sıradan alınan iletilerin çıkarır **EncodingJobMessage** türü.</span><span class="sxs-lookup"><span data-stu-id="a20e3-126">The code deserializes messages received from the queue into objects of the **EncodingJobMessage** type.</span></span>
2. <span data-ttu-id="a20e3-127">Medya Hizmetleri ve depolama hesabı bilgilerini app.config dosyasından yükler.</span><span class="sxs-lookup"><span data-stu-id="a20e3-127">Loads the Media Services and Storage account information from the app.config file.</span></span> <span data-ttu-id="a20e3-128">Kod örneği, oluşturmak için bu bilgileri kullanır. **CloudMediaContext** ve **CloudQueue** nesneleri.</span><span class="sxs-lookup"><span data-stu-id="a20e3-128">The code example uses this information to create the **CloudMediaContext** and **CloudQueue** objects.</span></span>
3. <span data-ttu-id="a20e3-129">Kodlama işinin hakkında bildirim iletileri alan bir sıra oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a20e3-129">Creates the queue that receives notification messages about the encoding job.</span></span>
4. <span data-ttu-id="a20e3-130">Sıraya eşlenen bildirim bitiş noktası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a20e3-130">Creates the notification end point that is mapped to the queue.</span></span>
5. <span data-ttu-id="a20e3-131">Bildirim bitiş noktası projeye ekler ve kodlama işi gönderir.</span><span class="sxs-lookup"><span data-stu-id="a20e3-131">Attaches the notification end point to the job and submits the encoding job.</span></span> <span data-ttu-id="a20e3-132">Bir projeye bağlı birden çok bildirim uç noktaları olabilir.</span><span class="sxs-lookup"><span data-stu-id="a20e3-132">You can have multiple notification end points attached to a job.</span></span>
6. <span data-ttu-id="a20e3-133">Geçişleri **NotificationJobState.FinalStatesOnly** için **AddNew** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a20e3-133">Passes **NotificationJobState.FinalStatesOnly** to the **AddNew** method.</span></span> <span data-ttu-id="a20e3-134">(Bu örnekte, biz yalnızca iş işleme son Devletleri'nde ilgilendiğiniz.)</span><span class="sxs-lookup"><span data-stu-id="a20e3-134">(In this example, we are only interested in final states of the job processing.)</span></span>

        job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly, _notificationEndPoint);
7. <span data-ttu-id="a20e3-135">Geçirirseniz **NotificationJobState.All**, tüm aşağıdaki durum değişikliği bildirimlerini almak: sıraya alınan, zamanlanan, işlem ve tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="a20e3-135">If you pass **NotificationJobState.All**, you get all of the following state change notifications: queued, scheduled, processing, and finished.</span></span> <span data-ttu-id="a20e3-136">Ancak, daha önce belirtildiği gibi kuyruk depolama sıralı teslim garanti etmez.</span><span class="sxs-lookup"><span data-stu-id="a20e3-136">However, as noted earlier, Queue storage does not guarantee ordered delivery.</span></span> <span data-ttu-id="a20e3-137">İletileri sipariş, kullanmak için **zaman damgası** özelliği (tanımlanan **EncodingJobMessage** aşağıdaki örnekte türü).</span><span class="sxs-lookup"><span data-stu-id="a20e3-137">To order messages, use the **Timestamp** property (defined on the **EncodingJobMessage** type in the example below).</span></span> <span data-ttu-id="a20e3-138">Yinelenen iletileri mümkündür.</span><span class="sxs-lookup"><span data-stu-id="a20e3-138">Duplicate messages are possible.</span></span> <span data-ttu-id="a20e3-139">Çoğaltmaları denetlemek için kullanın **ETag özelliği** (tanımlanan **EncodingJobMessage** türü).</span><span class="sxs-lookup"><span data-stu-id="a20e3-139">To check for duplicates, use the **ETag property** (defined on the **EncodingJobMessage** type).</span></span> <span data-ttu-id="a20e3-140">Bazı durum değişikliği bildirimlerini atlandı mümkündür.</span><span class="sxs-lookup"><span data-stu-id="a20e3-140">It is also possible that some state change notifications get skipped.</span></span>
8. <span data-ttu-id="a20e3-141">10 saniyede sıraya denetleyerek tamamlanmış durumuna almak iş bekler.</span><span class="sxs-lookup"><span data-stu-id="a20e3-141">Waits for the job to get to the finished state by checking the queue every 10 seconds.</span></span> <span data-ttu-id="a20e3-142">Bunlar işlendikten sonra iletileri siler.</span><span class="sxs-lookup"><span data-stu-id="a20e3-142">Deletes messages after they have been processed.</span></span>
9. <span data-ttu-id="a20e3-143">Sıranın ve bildirim bitiş noktasını siler.</span><span class="sxs-lookup"><span data-stu-id="a20e3-143">Deletes the queue and the notification end point.</span></span>

> [!NOTE]
> <span data-ttu-id="a20e3-144">Bir işin durumunu izlemek için önerilen bildirim iletileri için dinleyerek aşağıdaki örnekte gösterildiği gibi bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="a20e3-144">The recommended way to monitor a job’s state is by listening to notification messages, as shown in the following example.</span></span>
>
> <span data-ttu-id="a20e3-145">Alternatif olarak, kullanarak bir işin durumuna iade edilemedi **IJob.State** özelliği.</span><span class="sxs-lookup"><span data-stu-id="a20e3-145">Alternatively, you could check on a job’s state by using the **IJob.State** property.</span></span>  <span data-ttu-id="a20e3-146">Bir işin tamamlanma hakkında bir uyarı iletisi üzerinde duruma gelebilir **IJob** ayarlanır **tamamlandı**.</span><span class="sxs-lookup"><span data-stu-id="a20e3-146">A notification message about a job’s completion may arrive before the state on **IJob** is set to **Finished**.</span></span> <span data-ttu-id="a20e3-147">**IJob.State** özelliği kısa bir gecikmeyle doğru durumunu yansıtır.</span><span class="sxs-lookup"><span data-stu-id="a20e3-147">The **IJob.State**  property reflects the accurate state with a slight delay.</span></span>
>
>

### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="a20e3-148">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a20e3-148">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="a20e3-149">Geliştirme ortamınızı kurun ve app.config dosyanızı [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md) bölümünde açıklandığı gibi bağlantı bilgileriyle doldurun.</span><span class="sxs-lookup"><span data-stu-id="a20e3-149">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="a20e3-150">Yeni bir klasör oluşturun (yerel sürücünüzün herhangi bir yerinde) ve kodlayıp akışla aktarmak veya aşamalı indirmek istediğiniz bir .mp4 dosyasını buraya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="a20e3-150">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want to encode and stream or progressively download.</span></span> <span data-ttu-id="a20e3-151">Bu örnekte, "C:\Media" yol kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a20e3-151">In this example, the "C:\Media" path is used.</span></span>

### <a name="code"></a><span data-ttu-id="a20e3-152">Kod</span><span class="sxs-lookup"><span data-stu-id="a20e3-152">Code</span></span>

```
using System;
using System.Linq;
using System.Configuration;
using System.IO;
using System.Threading;
using System.Collections.Generic;
using Microsoft.WindowsAzure.MediaServices.Client;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Queue;
using System.Runtime.Serialization.Json;

namespace JobNotification
{
    public class EncodingJobMessage
    {
        // MessageVersion is used for version control.
        public String MessageVersion { get; set; }

        // Type of the event. Valid values are
        // JobStateChange and NotificationEndpointRegistration.
        public String EventType { get; set; }

        // ETag is used to help the customer detect if
        // the message is a duplicate of another message previously sent.
        public String ETag { get; set; }

        // Time of occurrence of the event.
        public String TimeStamp { get; set; }

        // Collection of values specific to the event.

        // For the JobStateChange event the values are:
        //     JobId - Id of the Job that triggered the notification.
        //     NewState- The new state of the Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished
        //     OldState- The old state of the Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished

        // For the NotificationEndpointRegistration event the values are:
        //     NotificationEndpointId- Id of the NotificationEndpoint
        //          that triggered the notification.
        //     State- The state of the Endpoint.
        //          Valid values are: Registered and Unregistered.

        public IDictionary<string, object> Properties { get; set; }
    }

    class Program
    {

        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
        private static readonly string _StorageConnectionString = 
            ConfigurationManager.AppSettings["StorageConnectionString"];

        private static CloudMediaContext _context = null;
        private static CloudQueue _queue = null;
        private static INotificationEndPoint _notificationEndPoint = null;

        private static readonly string _singleInputMp4Path =
            Path.GetFullPath(@"C:\Media\BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            string endPointAddress = Guid.NewGuid().ToString();

            // Create the context.
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Create the queue that will be receiving the notification messages.
            _queue = CreateQueue(_StorageConnectionString, endPointAddress);

            // Create the notification point that is mapped to the queue.
            _notificationEndPoint =
                    _context.NotificationEndPoints.Create(
                    Guid.NewGuid().ToString(), NotificationEndPointType.AzureQueue, endPointAddress);


            if (_notificationEndPoint != null)
            {
                IJob job = SubmitEncodingJobWithNotificationEndPoint(_singleInputMp4Path);
                WaitForJobToReachedFinishedState(job.Id);
            }

            // Clean up.
            _queue.Delete();
            _notificationEndPoint.Delete();
        }


        static public CloudQueue CreateQueue(string storageAccountConnectionString, string endPointAddress)
        {
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageAccountConnectionString);

            // Create the queue client
            CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

            // Retrieve a reference to a queue
            CloudQueue queue = queueClient.GetQueueReference(endPointAddress);

            // Create the queue if it doesn't already exist
            queue.CreateIfNotExists();

            return queue;
        }


        public static IJob SubmitEncodingJobWithNotificationEndPoint(string inputMediaFilePath)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("My MP4 to Smooth Streaming encoding job");

            //Create an encrypted asset and upload the mp4.
            IAsset asset = CreateAssetAndUploadSingleFile(AssetCreationOptions.StorageEncrypted,
                inputMediaFilePath);

            // Get a media processor reference, and pass to it the name of the
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with the conversion details, using a configuration file.
            ITask task = job.Tasks.AddNew("My encoding Task",
                processor,
                "Adaptive Streaming",
                Microsoft.WindowsAzure.MediaServices.Client.TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);

            // Add an output asset to contain the results of the job.
            task.OutputAssets.AddNew("Output asset",
                AssetCreationOptions.None);

            // Add a notification point to the job. You can add multiple notification points.  
            job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly,
                _notificationEndPoint);

            job.Submit();

            return job;
        }

        public static void WaitForJobToReachedFinishedState(string jobId)
        {
            int expectedState = (int)JobState.Finished;
            int timeOutInSeconds = 600;

            bool jobReachedExpectedState = false;
            DateTime startTime = DateTime.Now;
            int jobState = -1;

            while (!jobReachedExpectedState)
            {
                // Specify how often you want to get messages from the queue.
                Thread.Sleep(TimeSpan.FromSeconds(10));

                foreach (var message in _queue.GetMessages(10))
                {
                    using (Stream stream = new MemoryStream(message.AsBytes))
                    {
                        DataContractJsonSerializerSettings settings = new DataContractJsonSerializerSettings();
                        settings.UseSimpleDictionaryFormat = true;
                        DataContractJsonSerializer ser = new DataContractJsonSerializer(typeof(EncodingJobMessage), settings);
                        EncodingJobMessage encodingJobMsg = (EncodingJobMessage)ser.ReadObject(stream);

                        Console.WriteLine();

                        // Display the message information.
                        Console.WriteLine("EventType: {0}", encodingJobMsg.EventType);
                        Console.WriteLine("MessageVersion: {0}", encodingJobMsg.MessageVersion);
                        Console.WriteLine("ETag: {0}", encodingJobMsg.ETag);
                        Console.WriteLine("TimeStamp: {0}", encodingJobMsg.TimeStamp);
                        foreach (var property in encodingJobMsg.Properties)
                        {
                            Console.WriteLine("    {0}: {1}", property.Key, property.Value);
                        }

                        // We are only interested in messages
                        // where EventType is "JobStateChange".
                        if (encodingJobMsg.EventType == "JobStateChange")
                        {
                            string JobId = (String)encodingJobMsg.Properties.Where(j => j.Key == "JobId").FirstOrDefault().Value;
                            if (JobId == jobId)
                            {
                                string oldJobStateStr = (String)encodingJobMsg.Properties.
                                                            Where(j => j.Key == "OldState").FirstOrDefault().Value;
                                string newJobStateStr = (String)encodingJobMsg.Properties.
                                                            Where(j => j.Key == "NewState").FirstOrDefault().Value;

                                JobState oldJobState = (JobState)Enum.Parse(typeof(JobState), oldJobStateStr);
                                JobState newJobState = (JobState)Enum.Parse(typeof(JobState), newJobStateStr);

                                if (newJobState == (JobState)expectedState)
                                {
                                    Console.WriteLine("job with Id: {0} reached expected state: {1}",
                                        jobId, newJobState);
                                    jobReachedExpectedState = true;
                                    break;
                                }
                            }
                        }
                    }
                    // Delete the message after we've read it.
                    _queue.DeleteMessage(message);
                }

                // Wait until timeout
                TimeSpan timeDiff = DateTime.Now - startTime;
                bool timedOut = (timeDiff.TotalSeconds > timeOutInSeconds);
                if (timedOut)
                {
                    Console.WriteLine(@"Timeout for checking job notification messages,
                                        latest found state ='{0}', wait time = {1} secs",
                        jobState,
                        timeDiff.TotalSeconds);

                    throw new TimeoutException();
                }
            }
        }

        static private IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
        {
            var asset = _context.Assets.Create("UploadSingleFile_" + DateTime.UtcNow.ToString(),
                assetCreationOptions);

            var fileName = Path.GetFileName(singleFilePath);

            var assetFile = asset.AssetFiles.Create(fileName);

            Console.WriteLine("Created assetFile {0}", assetFile.Name);
            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading of {0}", assetFile.Name);

            return asset;
        }

        static private IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }
    }
}
```
<span data-ttu-id="a20e3-153">Önceki örnekte, aşağıdaki çıkış üretti.</span><span class="sxs-lookup"><span data-stu-id="a20e3-153">The preceding example produced the following output.</span></span> <span data-ttu-id="a20e3-154">Değerlerinizi değişir.</span><span class="sxs-lookup"><span data-stu-id="a20e3-154">Your values will vary.</span></span>

    Created assetFile BigBuckBunny.mp4
    Upload BigBuckBunny.mp4
    Done uploading of BigBuckBunny.mp4

    EventType: NotificationEndPointRegistration
    MessageVersion: 1.0
    ETag: e0238957a9b25bdf3351a88e57978d6a81a84527fad03bc23861dbe28ab293f6
    TimeStamp: 2013-05-14T20:22:37
        NotificationEndPointId: nb:nepid:UUID:d6af9412-2488-45b2-ba1f-6e0ade6dbc27
        State: Registered
        Name: dde957b2-006e-41f2-9869-a978870ac620
        Created: 2013-05-14T20:22:35

    EventType: JobStateChange
    MessageVersion: 1.0
    ETag: 4e381f37c2d844bde06ace650310284d6928b1e50101d82d1b56220cfcb6076c
    TimeStamp: 2013-05-14T20:24:40
        JobId: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54
        JobName: My MP4 to Smooth Streaming encoding job
        NewState: Finished
        OldState: Processing
        AccountName: westeuropewamsaccount
    job with Id: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54 reached expected
    State: Finished


## <a name="next-step"></a><span data-ttu-id="a20e3-155">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="a20e3-155">Next step</span></span>
<span data-ttu-id="a20e3-156">Media Services öğrenme yollarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="a20e3-156">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a20e3-157">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="a20e3-157">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
