---
title: ".NET ile aaaUse Azure kuyruk depolama toomonitor Media Services iş bildirimleri | Microsoft Docs"
description: "Nasıl toouse Azure kuyruk depolama toomonitor Media Services iş bildirimlerini öğrenin. Merhaba kod örneği C# dilinde yazılmıştır ve .NET için hello Media Services SDK'sı kullanır."
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
ms.openlocfilehash: e4068621ada00d763133dc0d01cfc666b53f8b1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-queue-storage-toomonitor-media-services-job-notifications-with-net"></a>Azure kuyruk depolama toomonitor Media Services iş bildirimleri .NET ile kullanma
Kodlama işleri çalıştırdığınızda, genellikle bir şekilde tootrack ilerleyişini gerektirir. Media Services toodeliver bildirimleri çok yapılandırabilirsiniz[Azure kuyruk depolama](../storage/storage-dotnet-how-to-use-queues.md). Merhaba kuyruk depolama alma bildirimleri tarafından iş ilerleme durumunu izleyebilirsiniz. 

TooQueue depolama teslim edilen ileti herhangi bir yere hello world erişilebilir. Hello kuyruk depolama Mesajlaşma mimarisi, güvenilir ve ölçeklendirilebilir. Kuyruk depolama iletileri için yoklama diğer yöntemleri kullanmayı üzerinden önerilir.

Bir içerik yönetim sistemi geliştiriyorsanız, tooperform gereken dinleme tooMedia Hizmetleri bildirimler için yaygın bir senaryo biri (örneğin, bir iş akışında veya toopublish tootrigger hello sonraki adım bir kodlama işi sonra bazı ek görevi tamamlandıktan içeriği).

Bu konu, kuyruk depolama biriminden nasıl tooget bildirim iletilerini gösterir.  

## <a name="considerations"></a>Dikkat edilmesi gerekenler
Kuyruk depolama kullanma Media Services uygulamaları geliştirirken Hello aşağıdakileri dikkate alın:

* Kuyruk depolama ilk olarak ilk çıkar garanti sağlamaz (FIFO) sıralı teslim. Daha fazla bilgi için bkz: [Azure kuyrukları ve Azure hizmet veri yolu kuyrukları karşılaştırıldığında ve Contrasted](https://msdn.microsoft.com/library/azure/hh767287.aspx).
* Kuyruk depolama gönderme hizmeti değil. Toopoll hello kuyruk bulunur.
* Herhangi bir sayıda sıralar olabilir. Daha fazla bilgi için bkz: [kuyruk hizmeti REST API'si](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API).
* Kuyruk depolama bazı kısıtlamalar ve özellikleri toobe farkında sahiptir. Bunlar [Azure kuyrukları ve Azure hizmet veri yolu kuyrukları karşılaştırıldığında ve Contrasted](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted).

## <a name="net-code-example"></a>.NET kodu örneği

Bu bölümdeki Hello kod örneği, aşağıdaki hello:

1. Merhaba tanımlar **EncodingJobMessage** toohello bildirim ileti biçimi eşleyen sınıfı. Merhaba kod çıkarır hello nesnelerine hello kuyruğundan alınan iletilerin **EncodingJobMessage** türü.
2. Medya Hizmetleri ve depolama hesabı bilgilerini hello app.config dosyasından yükleri hello. Merhaba kod örneği, bu bilgileri toocreate hello kullanır **CloudMediaContext** ve **CloudQueue** nesneleri.
3. İş kodlama hello hakkında bildirim iletileri alan bir hello sıra oluşturur.
4. Bitiş noktasını toohello sıra eşlenen hello bildirim oluşturur.
5. Merhaba bildirim bitiş noktası toohello işi ekler ve hello kodlama işi gönderir. Birden çok bildirim bitiş noktası bağlı tooa işi olabilir.
6. Geçişleri **NotificationJobState.FinalStatesOnly** toohello **AddNew** yöntemi. (Bu örnekte, yalnızca son hello iş işleme durumlarda ilginizi duyuyoruz.)

        job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly, _notificationEndPoint);
7. Geçirirseniz **NotificationJobState.All**, tüm durum değişikliği bildirimlerini aşağıdaki hello almak: sıraya alınan, zamanlanan, işlem ve tamamlandı. Ancak, daha önce belirtildiği gibi kuyruk depolama sıralı teslim garanti etmez. tooorder iletileri kullanan hello **zaman damgası** özelliği (Merhaba üzerinde tanımlı **EncodingJobMessage** aşağıdaki hello örnek yazın). Yinelenen iletileri mümkündür. çoğaltmaları kullanım hello toocheck **ETag özelliği** (Merhaba üzerinde tanımlı **EncodingJobMessage** türü). Bazı durum değişikliği bildirimlerini atlandı mümkündür.
8. Merhaba iş tooget toohello bekler 10 saniyede hello sıra denetleyerek durumu tamamlandı. Bunlar işlendikten sonra iletileri siler.
9. Hello kuyruk ve hello bildirim bitiş noktasını siler.

> [!NOTE]
> bir işin durumunda dinleme toonotification iletileri göre önerilen yöntem toomonitor hello aşağıdaki örnekte gösterildiği gibi hello.
>
> Alternatif olarak, hello kullanarak bir işin durumuna iade edilemedi **IJob.State** özelliği.  Bir işin tamamlanma hakkında bir uyarı iletisi üzerinde hello durumu önce gelebilir **IJob** çok ayarlanır**tamamlandı**. Merhaba **IJob.State** özellik hello doğru kısa bir gecikme durumuyla gösterir.
>
>

### <a name="create-and-configure-a-visual-studio-project"></a>Visual Studio projesi oluşturup yapılandırma

1. Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md). 
2. Yeni bir klasör oluşturun (klasör herhangi bir yerde olabilir yerel diskinize) ve tooencode ve akış istediğiniz veya aşamalı indirmek bir .mp4 dosyasını kopyalayın. Bu örnekte, hello "C:\Media" yol kullanılır.

### <a name="code"></a>Kod

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

        // Type of hello event. Valid values are
        // JobStateChange and NotificationEndpointRegistration.
        public String EventType { get; set; }

        // ETag is used toohelp hello customer detect if
        // hello message is a duplicate of another message previously sent.
        public String ETag { get; set; }

        // Time of occurrence of hello event.
        public String TimeStamp { get; set; }

        // Collection of values specific toohello event.

        // For hello JobStateChange event hello values are:
        //     JobId - Id of hello Job that triggered hello notification.
        //     NewState- hello new state of hello Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished
        //     OldState- hello old state of hello Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished

        // For hello NotificationEndpointRegistration event hello values are:
        //     NotificationEndpointId- Id of hello NotificationEndpoint
        //          that triggered hello notification.
        //     State- hello state of hello Endpoint.
        //          Valid values are: Registered and Unregistered.

        public IDictionary<string, object> Properties { get; set; }
    }

    class Program
    {

        // Read values from hello App.config file.
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

            // Create hello context.
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Create hello queue that will be receiving hello notification messages.
            _queue = CreateQueue(_StorageConnectionString, endPointAddress);

            // Create hello notification point that is mapped toohello queue.
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

            // Create hello queue client
            CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

            // Retrieve a reference tooa queue
            CloudQueue queue = queueClient.GetQueueReference(endPointAddress);

            // Create hello queue if it doesn't already exist
            queue.CreateIfNotExists();

            return queue;
        }


        public static IJob SubmitEncodingJobWithNotificationEndPoint(string inputMediaFilePath)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("My MP4 tooSmooth Streaming encoding job");

            //Create an encrypted asset and upload hello mp4.
            IAsset asset = CreateAssetAndUploadSingleFile(AssetCreationOptions.StorageEncrypted,
                inputMediaFilePath);

            // Get a media processor reference, and pass tooit hello name of the
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with hello conversion details, using a configuration file.
            ITask task = job.Tasks.AddNew("My encoding Task",
                processor,
                "Adaptive Streaming",
                Microsoft.WindowsAzure.MediaServices.Client.TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("Output asset",
                AssetCreationOptions.None);

            // Add a notification point toohello job. You can add multiple notification points.  
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
                // Specify how often you want tooget messages from hello queue.
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

                        // Display hello message information.
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
                    // Delete hello message after we've read it.
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
Çıktı aşağıdaki önceki örnek üretilen hello hello. Değerlerinizi değişir.

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
        JobName: My MP4 tooSmooth Streaming encoding job
        NewState: Finished
        OldState: Processing
        AccountName: westeuropewamsaccount
    job with Id: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54 reached expected
    State: Finished


## <a name="next-step"></a>Sonraki adım
Media Services öğrenme yollarını gözden geçirin.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
