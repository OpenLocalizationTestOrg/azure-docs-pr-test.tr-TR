---
title: ".NET ile aaaUse Azure Web Kancalarını toomonitor Media Services iş bildirimleri | Microsoft Docs"
description: "Nasıl toouse Azure Web Kancalarını toomonitor Media Services iş bildirimlerini öğrenin. Merhaba kod örneği C# dilinde yazılmıştır ve .NET için hello Media Services SDK'sı kullanır."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: a61fe157-81b1-45c1-89f2-224b7ef55869
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/06/2017
ms.author: juliako
ms.openlocfilehash: b7df597da20e551cb2a02cd21c96c7bddf9e1a66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-webhooks-toomonitor-media-services-job-notifications-with-net"></a>Azure Web Kancalarını toomonitor Media Services iş bildirimleri .NET ile kullanma
İşlerini çalıştırdığınızda, genellikle bir şekilde tootrack ilerleyişini gerektirir. Azure Web Kancalarını kullanarak Media Services iş bildirimleri izleyebilirsiniz veya [Azure kuyruk depolama](media-services-dotnet-check-job-progress-with-queues.md). Bu konuda gösterilmektedir nasıl Kancalarını ile toowork.

## <a name="prerequisites"></a>Ön koşullar

Merhaba, gerekli toocomplete hello öğretici şunlardır:

* Bir Azure hesabı. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).
* Bir Media Services hesabı. bir Media Services hesabı toocreate bkz [nasıl tooCreate Media Services hesabı](media-services-portal-create-account.md).
* Anlayış [nasıl toouse Azure işlevleri](../azure-functions/functions-overview.md). Ayrıca, gözden [Azure işlevleri HTTP ve Web kancası bağlamaları](../azure-functions/functions-bindings-http-webhook.md).

Bu konuda gösterilmektedir nasıl

*  Özelleştirilmiş toorespond toowebhooks olan bir Azure işlevi tanımlayın. 
    
    Bu durumda, kodlama işinin durumu değiştiğinde hello Web kancası Media Services tarafından tetiklenir. Merhaba işlevi hello Web kancası çağrısından geri Media Services bildirimleri dinler ve hello işi tamamlandıktan sonra hello çıkış varlığına yayımlar. 
    
    >[!NOTE]
    >Devam etmeden önce anladığınızdan emin olun nasıl [Azure işlevleri HTTP ve Web kancası bağlamaları](../azure-functions/functions-bindings-http-webhook.md) çalışır.
    >
    
* Bir Web kancası tooyour kodlama görev ekleyin ve bu Web kancası yanıtlaması gizli anahtar ve hello Web kancası URL'si belirtin. Burada gösterilen hello örnekte görev kodlama hello oluşturan hello bir konsol uygulaması kodudur.

## <a name="setting-up-webhook-notification-azure-functions"></a>Azure işlevleri "Web kancası bildirimi" ayarlama

Bu bölümdeki Hello kodu bir Web kancası olan bir Azure işlevi uygulaması gösterilir. Bu örnek hello işlevi hello Web kancası çağrısından geri Media Services bildirimleri dinler ve hello işi tamamlandıktan sonra hello çıkış varlığına yayımlar.

Merhaba Web kancası bekliyor imzalama anahtarı (kimlik) toomatch bir hello bildirim bitiş noktası yapılandırdığınızda geçirdiğiniz hello. imzalama anahtarı hello kullanılan tooprotect ve Azure Media Services, Web Kancalarını geri aramalar güvenli hello 64 baytlık Base64 ile kodlanmış değerdir. 

Koddan hello hello **VerifyWebHookRequestSignature** yöntemi hello bildirim iletisi doğrulamayı hello. Merhaba amacı, bu doğrulama ileti hello tooensure Azure Media Services tarafından gönderilen ve oynanmadığını ' dir. Merhaba olduğu gibi Hello imza Azure işlevleri için isteğe bağlı **kod** değeri olarak bir sorgu parametresi üzerinden Aktarım Katmanı Güvenliği (TLS). 

Çeşitli Media Services .NET Azure işlevleri (Merhaba biri bu konuda gösterilen dahil) hello tanımını bulabilirsiniz [burada](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).

Merhaba aşağıdaki kod listesi gösterir Azure işlev parametrelerini ve hello Azure işlevi ile ilişkili olan üç dosyaları hello tanımları: function.json, project.json ve run.csx.

### <a name="application-settings"></a>Uygulama ayarları 

Merhaba aşağıdaki tabloda hello bu bölümünde tanımlanan Azure işlevi tarafından kullanılan hello parametrelerini gösterir. 

|Ad|Tanım|Örnek| 
|---|---|---|
|AMSAccount|AMS hesabının adı. |juliakomediaservices|
|AMSKey |AMS hesap anahtarınızı. | JUWJdDaOHQQqsZeiXZuE76eDt2SO + YMJk25Lghgy2nY =|
|MediaServicesStorageAccountName |AMS hesabınızla ilişkili hello depolama hesabı adı.| storagepkeewmg5c3peq|
|MediaServicesStorageAccountKey |AMS hesabınızla ilişkili hello depolama hesabı anahtarı.|
|SigningKey |İmzalama anahtarı.| j0txf1f8msjytzvpe40nxbpxdcxtqcgxy0nt|
|WebHookEndpoint | Bir Web kancası uç nokta adresi. | https://juliakofuncapp.azurewebsites.NET/api/Notification_Webhook_Function?Code=iN2phdrTnCxmvaKExFWOTulfnm4C71mMLIy8tzLr7Zvf6Z22HHIK5g==.|

### <a name="functionjson"></a>Function.JSON

Merhaba function.json dosyası hello işlev bağlamaları ve diğer yapılandırma ayarlarını tanımlar. Bu dosya toodetermine hello olayları toomonitor ve yürütme toopass verisine ve dönüş verileri nasıl işlev Hello çalışma zamanı kullanır. 

    {
      "bindings": [
        {
          "type": "httpTrigger",
          "name": "req",
          "direction": "in",
          "methods": [
        "post",
        "get",
        "put",
        "update",
        "patch"
          ]
        },
        {
          "type": "http",
          "name": "res",
          "direction": "out"
        }
      ]
    }
    
### <a name="projectjson"></a>Project.JSON

Merhaba project.json dosyası bağımlılıkları içerir. 

    {
      "frameworks": {
        "net46":{
          "dependencies": {
        "windowsazure.mediaservices": "3.8.0.5",
        "windowsazure.mediaservices.extensions": "3.8.0.3"
          }
        }
       }
    }
    
### <a name="runcsx"></a>Run.csx

Merhaba aşağıdaki C# kodu bir Web kancası olan bir Azure işlevi tanımını gösterir. Merhaba işlevi hello Web kancası çağrısından geri Media Services bildirimleri dinler ve hello işi tamamlandıktan sonra hello çıkış varlığına yayımlar. 


>[!NOTE]
>Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için). Merhaba kullanması gereken her zaman kullanıyorsanız, aynı ilke kimliği hello aynı gün / erişim izinlerini, örneğin, uzun bir süre (karşıya yükleme olmayan ilkeleri) yerinde hedeflenen tooremain olan bulucular ilkeleri. Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.

    ///////////////////////////////////////////////////
    #r "Newtonsoft.Json"

    using System;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using System.IO;
    using System.Globalization;
    using Newtonsoft.Json;
    using Microsoft.Azure;
    using System.Net;
    using System.Security.Cryptography;

    internal const string SignatureHeaderKey = "sha256";
    internal const string SignatureHeaderValueTemplate = SignatureHeaderKey + "={0}";
    static string _webHookEndpoint = Environment.GetEnvironmentVariable("WebHookEndpoint");
    static string _signingKey = Environment.GetEnvironmentVariable("SigningKey");
    static string _mediaServicesAccountName = Environment.GetEnvironmentVariable("AMSAccount");
    static string _mediaServicesAccountKey = Environment.GetEnvironmentVariable("AMSKey");

    static CloudMediaContext _context = null;

    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        log.Info($"C# HTTP trigger function processed a request. RequestUri={req.RequestUri}");

        Task<byte[]> taskForRequestBody = req.Content.ReadAsByteArrayAsync();
        byte[] requestBody = await taskForRequestBody;

        string jsonContent = await req.Content.ReadAsStringAsync();
        log.Info($"Request Body = {jsonContent}");

        IEnumerable<string> values = null;
        if (req.Headers.TryGetValues("ms-signature", out values))
        {
        byte[] signingKey = Convert.FromBase64String(_signingKey);
        string signatureFromHeader = values.FirstOrDefault();

        if (VerifyWebHookRequestSignature(requestBody, signatureFromHeader, signingKey))
        {
            string requestMessageContents = Encoding.UTF8.GetString(requestBody);

            NotificationMessage msg = JsonConvert.DeserializeObject<NotificationMessage>(requestMessageContents);

            if (VerifyHeaders(req, msg, log))
            { 
            string newJobStateStr = (string)msg.Properties.Where(j => j.Key == "NewState").FirstOrDefault().Value;
            if (newJobStateStr == "Finished")
            {
                _context = new CloudMediaContext(new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey));

                if(_context!=null)   
                {                        
                string urlForClientStreaming = PublishAndBuildStreamingURLs(msg.Properties["JobId"]);
                log.Info($"URL toohello manifest for client streaming using HLS protocol: {urlForClientStreaming}");
                }
            }

            return req.CreateResponse(HttpStatusCode.OK, string.Empty);
            }
            else
            {
            log.Info($"VerifyHeaders failed.");
            return req.CreateResponse(HttpStatusCode.BadRequest, "VerifyHeaders failed.");
            }
        }
        else
        {
            log.Info($"VerifyWebHookRequestSignature failed.");
            return req.CreateResponse(HttpStatusCode.BadRequest, "VerifyWebHookRequestSignature failed.");
        }
        }

        return req.CreateResponse(HttpStatusCode.BadRequest, "Generic Error.");
    }

    private static string PublishAndBuildStreamingURLs(String jobID)
    {
        IJob job = _context.Jobs.Where(j => j.Id == jobID).FirstOrDefault();
        IAsset asset = job.OutputMediaAssets.FirstOrDefault();

        // Create a 30-day readonly access policy. 
        // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
        TimeSpan.FromDays(30),
        AccessPermissions.Read);

        // Create a locator toohello streaming content on an origin. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
        policy,
        DateTime.UtcNow.AddMinutes(-5));


        // Get a reference toohello streaming manifest file from hello  
        // collection of files in hello asset. 
        var manifestFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                    EndsWith(".ism")).
                    FirstOrDefault();

        // Create a full URL toohello manifest file. Use this for playback
        // in streaming media clients. 
        string urlForClientStreaming = originLocator.Path + manifestFile.Name + "/manifest" +  "(format=m3u8-aapl)";
        return urlForClientStreaming;

    }

    private static bool VerifyWebHookRequestSignature(byte[] data, string actualValue, byte[] verificationKey)
    {
        using (var hasher = new HMACSHA256(verificationKey))
        {
        byte[] sha256 = hasher.ComputeHash(data);
        string expectedValue = string.Format(CultureInfo.InvariantCulture, SignatureHeaderValueTemplate, ToHex(sha256));

        return (0 == String.Compare(actualValue, expectedValue, System.StringComparison.Ordinal));
        }
    }

    private static bool VerifyHeaders(HttpRequestMessage req, NotificationMessage msg, TraceWriter log)
    {
        bool headersVerified = false;

        try
        {
        IEnumerable<string> values = null;
        if (req.Headers.TryGetValues("ms-mediaservices-accountid", out values))
        {
            string accountIdHeader = values.FirstOrDefault();
            string accountIdFromMessage = msg.Properties["AccountId"];

            if (0 == string.Compare(accountIdHeader, accountIdFromMessage, StringComparison.OrdinalIgnoreCase))
            {
            headersVerified = true;
            }
            else
            {
            log.Info($"accountIdHeader={accountIdHeader} does not match accountIdFromMessage={accountIdFromMessage}");
            }
        }
        else
        {
            log.Info($"Header ms-mediaservices-accountid not found.");
        }
        }
        catch (Exception e)
        {
        log.Info($"VerifyHeaders hit exception {e}");
        headersVerified = false;
        }

        return headersVerified;
    }

    private static readonly char[] HexLookup = new char[] { '0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'A', 'B', 'C', 'D', 'E', 'F' };

    /// <summary>
    /// Converts a <see cref="T:byte[]"/> tooa hex-encoded string.
    /// </summary>
    private static string ToHex(byte[] data)
    {
        if (data == null)
        {
        return string.Empty;
        }

        char[] content = new char[data.Length * 2];
        int output = 0;
        byte d;
        for (int input = 0; input < data.Length; input++)
        {
        d = data[input];
        content[output++] = HexLookup[d / 0x10];
        content[output++] = HexLookup[d % 0x10];
        }
        return new string(content);
    }

    internal enum NotificationEventType
    {
        None = 0,
        JobStateChange = 1,
        NotificationEndPointRegistration = 2,
        NotificationEndPointUnregistration = 3,
        TaskStateChange = 4,
        TaskProgress = 5
    }
    
    internal sealed class NotificationMessage
    {
        public string MessageVersion { get; set; }
        public string ETag { get; set; }
        public NotificationEventType EventType { get; set; }
        public DateTime TimeStamp { get; set; }
        public IDictionary<string, string> Properties { get; set; }
    }

### <a name="function-output"></a>İşlevi çıktı

Yukarıdaki Hello örnek çıktı aşağıdaki hello üretilen, değerlerinizi farklılık gösterir.

    C# HTTP trigger function processed a request. RequestUri=https://juliako001-functions.azurewebsites.net/api/Notification_Webhook_Function?code=9376d69kygoy49oft81nel8frty5cme8hb9xsjslxjhalwhfrqd79awz8ic4ieku74dvkdfgvi
    Request Body = {
      "MessageVersion": "1.1",
      "ETag": "b8977308f48858a8f224708bc963e1a09ff917ce730316b4e7ae9137f78f3b20",
      "EventType": 4,
      "TimeStamp": "2017-02-16T03:59:53.3041122Z",
      "Properties": {
        "JobId": "nb:jid:UUID:badd996c-8d7c-4ae0-9bc1-bd7f1902dbdd",
        "TaskId": "nb:tid:UUID:80e26fb9-ee04-4739-abd8-2555dc24639f",
        "NewState": "Finished",
        "OldState": "Processing",
        "AccountName": "mediapkeewmg5c3peq",
        "AccountId": "301912b0-659e-47e0-9bc4-6973f2be3424",
        "NotificationEndPointId": "nb:nepid:UUID:cb5d707b-4db8-45fe-a558-19f8d3306093"
      }
    }
    
    URL toohello manifest for client streaming using HLS protocol: http://mediapkeewmg5c3peq.streaming.mediaservices.windows.net/0ac98077-2b58-4db7-a8da-789a13ac6167/BigBuckBunny.ism/manifest(format=m3u8-aapl)

## <a name="adding-webhook-tooyour-encoding-task"></a>Web kancası tooyour kodlama görev ekleme

Bu bölümde, bir Web kancası bildirim tooa görev ekler hello kodu gösterilir. Zincirleme görevler içeren bir iş için daha kullanışlı olurdu bir proje düzeyi bildirim de ekleyebilirsiniz.  

1. Visual Studio’da yeni bir C# Konsol Uygulaması oluşturun. Merhaba adını, konumunu ve çözüm adı girin ve Tamam'ı tıklatın.
2. Kullanım [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) tooinstall Azure Media Services.
3. App.config dosyasını uygun değerlerle güncelleştirin: 
    
    * Azure Media Services adını ve bildirimleri gönderme anahtarı 
    * tooget hello bildirimleri beklediği Web kancası URL'si 
    * Merhaba, Web kancası bekliyor hello anahtarla eşleşen anahtara imzalama. imzalama anahtarı hello kullanılan tooprotect ve Azure Media Services, Web Kancalarını geri aramalar güvenli hello 64 baytlık Base64 ile kodlanmış değerdir. 

            <appSettings>
              <add key="MediaServicesAccountName" value="AMSAcctName" />
              <add key="MediaServicesAccountKey" value="AMSAcctKey" />
              <add key="WebhookURL" value="https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>" />
              <add key="WebhookSigningKey" value="j0txf1f8msjytzvpe40nxbpxdcxtqcgxy0nt" />
            </appSettings>
            
4. Program.cs dosyanızdaki koddan hello ile güncelleştirin:

        using System;
        using System.Configuration;
        using System.Linq;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace NotificationWebHook
        {
            class Program
            {
            // Read values from hello App.config file.
            private static readonly string _mediaServicesAccountName =
                ConfigurationManager.AppSettings["MediaServicesAccountName"];
            private static readonly string _mediaServicesAccountKey =
                ConfigurationManager.AppSettings["MediaServicesAccountKey"];
            private static readonly string _webHookEndpoint =
                ConfigurationManager.AppSettings["WebhookURL"];
            private static readonly string _signingKey =
                 ConfigurationManager.AppSettings["WebhookSigningKey"];

            // Field for service context.
            private static CloudMediaContext _context = null;

            static void Main(string[] args)
            {

                // Used hello cached credentials toocreate CloudMediaContext.
                _context = new CloudMediaContext(new MediaServicesCredentials(
                        _mediaServicesAccountName,
                        _mediaServicesAccountKey));

                byte[] keyBytes = Convert.FromBase64String(_signingKey);

                IAsset newAsset = _context.Assets.FirstOrDefault();

                // Check for existing Notification Endpoint with hello name "FunctionWebHook"

                var existingEndpoint = _context.NotificationEndPoints.Where(e => e.Name == "FunctionWebHook").FirstOrDefault();
                INotificationEndPoint endpoint = null;

                if (existingEndpoint != null)
                {
                Console.WriteLine("webhook endpoint already exists");
                endpoint = (INotificationEndPoint)existingEndpoint;
                }
                else
                {
                endpoint = _context.NotificationEndPoints.Create("FunctionWebHook",
                    NotificationEndPointType.WebHook, _webHookEndpoint, keyBytes);
                Console.WriteLine("Notification Endpoint Created with Key : {0}", keyBytes.ToString());
                }

                // Declare a new encoding job with hello Standard encoder
                IJob job = _context.Jobs.Create("MES Job");

                // Get a media processor reference, and pass tooit hello name of hello 
                // processor toouse for hello specific task.
                IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

                ITask task = job.Tasks.AddNew("My encoding task",
                processor,
                "Adaptive Streaming",
                TaskOptions.None);

                // Specify hello input asset toobe encoded.
                task.InputAssets.Add(newAsset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is not encrypted. 
                task.OutputAssets.AddNew(newAsset.Name, AssetCreationOptions.None);

                // Add hello WebHook notification toothis Task and request all notification state changes.
                // Note that you can also add a job level notification
                // which would be more useful for a job with chained tasks.  
                if (endpoint != null)
                {
                task.TaskNotificationSubscriptions.AddNew(NotificationJobState.All, endpoint, true);
                Console.WriteLine("Created Notification Subscription for endpoint: {0}", _webHookEndpoint);
                }
                else
                {
                Console.WriteLine("No Notification Endpoint is being used");
                }

                job.Submit();

                Console.WriteLine("Expect WebHook toobe triggered for hello Job ID: {0}", job.Id);
                Console.WriteLine("Expect WebHook toobe triggered for hello Task ID: {0}", task.Id);

                Console.WriteLine("Job Submitted");

            }
            private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
            {
                var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

                if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

                return processor;
            }

            }
        }

## <a name="next-step"></a>Sonraki adım
Gözden geçirme Media Services'i öğrenme yolları

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
