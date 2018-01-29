---
title: ".NET ile Media Services iş bildirimleri izlemek için Azure Web Kancalarını kullanın | Microsoft Docs"
description: "Media Services iş bildirimleri izlemek için Azure Web Kancalarını kullanmayı öğrenin. Kod örneği C# dilinde yazılmıştır ve .NET için Media Services SDK'sını kullanır."
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
ms.date: 12/09/2017
ms.author: juliako
ms.openlocfilehash: 9815e01dffb0342979f17974527b559de8146fed
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/11/2017
---
# <a name="use-azure-webhooks-to-monitor-media-services-job-notifications-with-net"></a>.NET ile Media Services iş bildirimleri izlemek için Azure Web'kancaları kullanın
İşlerini çalıştırdığınızda, genellikle iş ilerleme durumunu izlemek için bir yol gerekir. Azure Web Kancalarını kullanarak Media Services iş bildirimleri izleyebilirsiniz veya [Azure kuyruk depolama](media-services-dotnet-check-job-progress-with-queues.md). Bu makalede, Web kancalarını ile çalışmak gösterilmiştir.

Bu makalede gösterilmektedir nasıl

*  Web kancası için yanıtlamak için özelleştirilmiş bir Azure işlevi tanımlayın. 
    
    Bu durumda, kodlama işinin durumu değiştiğinde Web kancası Media Services tarafından tetiklenir. İşlev Web kancası çağrısından geri Media Services bildirimleri dinler ve iş tamamlandığında, çıkış varlığına yayımlar. 
    
    >[!NOTE]
    >Devam etmeden önce anladığınızdan emin olun nasıl [Azure işlevleri HTTP ve Web kancası bağlamaları](../azure-functions/functions-bindings-http-webhook.md) çalışır.
    >
    
* Bir Web kancası kodlama göreviniz ekleyin ve bu Web kancası yanıtlaması gizli anahtar ve Web kancası URL'si belirtin. Bir Web kancası kodlama göreviniz makalenin sonunda ekleyen bir örnek bulabilirsiniz.  

Çeşitli Media Services .NET Azure (Bu makalede gösterilen de dahil olmak üzere) işlevleri tanımlarını bulabilirsiniz [burada](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).

## <a name="prerequisites"></a>Ön koşullar

Öğreticiyi tamamlamak için aşağıdakiler gereklidir:

* Bir Azure hesabı. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).
* Bir Media Services hesabı. Bir Media Services hesabı oluşturmak için bkz. [Media Services hesabı oluşturma](media-services-portal-create-account.md).
* Anlayış [Azure işlevlerinin nasıl kullanılacağı](../azure-functions/functions-overview.md). Ayrıca, gözden [Azure işlevleri HTTP ve Web kancası bağlamaları](../azure-functions/functions-bindings-http-webhook.md).

## <a name="create-a-function-app"></a>İşlev uygulaması oluşturma

1. [Azure portalına](http://portal.azure.com) gidip Azure hesabınızla oturum açın.
2. Açıklandığı gibi işlev uygulaması oluşturma [burada](../azure-functions/functions-create-function-app-portal.md).

## <a name="configure-function-app-settings"></a>İşlev uygulaması ayarlarını yapılandır

Media Services işlevleri geliştirirken işlevlerinizi kullanılan ortam değişkenleri eklemek için kullanışlıdır. Uygulama ayarlarını yapılandırmak için uygulama ayarlarını yapılandır bağlantısına tıklayın. 

[Uygulama ayarları](media-services-dotnet-how-to-use-azure-functions.md#configure-function-app-settings) bölümünde bu makalede tanımlanan Web kancası kullanılan parametreleri tanımlar. Ayrıca aşağıdaki parametreler için uygulama ayarları ekleyin. 

|Ad|Tanım|Örnek| 
|---|---|---|
|SigningKey |İmzalama anahtarı.| j0txf1f8msjytzvpe40nxbpxdcxtqcgxy0nt|
|WebHookEndpoint | Bir Web kancası uç nokta adresi. Web kancası işlevinizi oluşturulduktan sonra URL'yi kopyalayıp **Al işlevi URL** bağlantı. | https://juliakofuncapp.azurewebsites.NET/api/Notification_Webhook_Function?Code=iN2phdrTnCxmvaKExFWOTulfnm4C71mMLIy8tzLr7Zvf6Z22HHIK5g==.|

## <a name="create-a-function"></a>İşlev oluşturma

İşlev Uygulamanız dağıtıldıktan sonra onu arasında bulabilirsiniz **uygulama hizmetleri** Azure işlevleri.

1. İşlev uygulamanızı seçin ve'ı tıklatın **yeni işlev**.
2. Seçin **C#** kod ve **API & Web Kancalarını** senaryo. 
3. Seçin **Genel Web kancası - C#**.
4. Tuşuna basın ve Web kancası adı **oluşturma**.

### <a name="files"></a>Dosyalar

Azure işlevinizi ve bu bölümde açıklanan diğer dosyaları kod dosyaları ile ilişkilidir. Varsayılan olarak, bir işlev ilişkili olduğu **function.json** ve **run.csx** (C#) dosyaları. Eklemek gereken bir **project.json** dosya. Bu bölümün geri kalanında bu dosyaları tanımlarında gösterir.

![Dosyaları](./media/media-services-azure-functions/media-services-azure-functions003.png)

#### <a name="functionjson"></a>Function.JSON

Function.json dosyası, işlev bağlamaları ve diğer yapılandırma ayarlarını tanımlar. Çalışma zamanı izlenecek olaylar belirlemek için bu dosyaya ve verilerini geçirin ve işlev yürütülmesini veri dönmek nasıl kullanır. 

```
{
  "bindings": [
    {
      "type": "httpTrigger",
      "direction": "in",
      "webHookType": "genericJson",
      "name": "req"
    },
    {
      "type": "http",
      "direction": "out",
      "name": "res"
    }
  ],
  "disabled": false
}
```

#### <a name="projectjson"></a>Project.JSON

Project.json dosyası bağımlılıkları içerir. 

```
{
  "frameworks": {
    "net46":{
      "dependencies": {
        "windowsazure.mediaservices": "4.0.0.4",
        "windowsazure.mediaservices.extensions": "4.0.0.4",
        "Microsoft.IdentityModel.Clients.ActiveDirectory": "3.13.1",
        "Microsoft.IdentityModel.Protocol.Extensions": "1.0.2.206221351"
      }
    }
   }
}
```
    
#### <a name="runcsx"></a>Run.csx

Bu bölümdeki kod bir Web kancası olan bir Azure işlevi uygulaması gösterir. Bu örnekte işlevi Web kancası çağrısından geri Media Services bildirimleri dinler ve iş tamamlandığında, çıkış varlığına yayımlar.

Web kancası bildirim bitiş noktası yapılandırdığınızda geçirdiğiniz olanla eşleşecek şekilde bir imzalama anahtarı (kimlik) bekliyor. İmzalama anahtarı korumak ve Azure Media Services, Web Kancalarını geri aramalar güvenli hale getirmek için kullanılan 64 baytlık Base64 ile kodlanmış değerdir. 

Aşağıdaki Web kancası tanımı kodda **VerifyWebHookRequestSignature** yöntemi bildirim iletisinin doğrulama yapar. Bu doğrulamanın amacı ileti Azure Media Services tarafından gönderilen ve oynanmadığını emin olmaktır. İmza içerdiğinden Azure işlevleri için isteğe bağlı olduğu **kod** değeri olarak bir sorgu parametresi üzerinden Aktarım Katmanı Güvenliği (TLS). 

>[!NOTE]
>Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için). Uzun süre boyunca kullanılmak için oluşturulan bulucu ilkeleri gibi aynı günleri / erişim izinlerini sürekli olarak kullanıyorsanız, aynı ilke kimliğini kullanmalısınız (karşıya yükleme olmayan ilkeler için). Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.

```
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
using Microsoft.Azure.WebJobs;
using Microsoft.IdentityModel.Clients.ActiveDirectory;

internal const string SignatureHeaderKey = "sha256";
internal const string SignatureHeaderValueTemplate = SignatureHeaderKey + "={0}";
static string _webHookEndpoint = Environment.GetEnvironmentVariable("WebHookEndpoint");
static string _signingKey = Environment.GetEnvironmentVariable("SigningKey");

static readonly string _AADTenantDomain = Environment.GetEnvironmentVariable("AMSAADTenantDomain");
static readonly string _RESTAPIEndpoint = Environment.GetEnvironmentVariable("AMSRESTAPIEndpoint");

static readonly string _AMSClientId = Environment.GetEnvironmentVariable("AMSClientId");
static readonly string _AMSClientSecret = Environment.GetEnvironmentVariable("AMSClientSecret");

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
                    AzureAdTokenCredentials tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain,
                                new AzureAdClientSymmetricKey(_AMSClientId, _AMSClientSecret),
                                AzureEnvironments.AzureCloudEnvironment);

                    AzureAdTokenProvider tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                    _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                    if(_context!=null)   
                    {                        
                        string urlForClientStreaming = PublishAndBuildStreamingURLs(msg.Properties["JobId"]);
                        log.Info($"URL to the manifest for client streaming using HLS protocol: {urlForClientStreaming}");
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

    // Create a locator to the streaming content on an origin. 
    ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
    policy,
    DateTime.UtcNow.AddMinutes(-5));

    // Get a reference to the streaming manifest file from the  
    // collection of files in the asset. 
    var manifestFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                EndsWith(".ism")).
                FirstOrDefault();

    // Create a full URL to the manifest file. Use this for playback
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
/// Converts a <see cref="T:byte[]"/> to a hex-encoded string.
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
```

Kaydedin ve işlevinizi çalıştırın.

### <a name="function-output"></a>İşlevi çıktı

Web kancası tetiklenir sonra yukarıdaki örnekte şu çıkışı üretir, değerlerinizi farklılık gösterir.

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
    
    URL to the manifest for client streaming using HLS protocol: http://mediapkeewmg5c3peq.streaming.mediaservices.windows.net/0ac98077-2b58-4db7-a8da-789a13ac6167/BigBuckBunny.ism/manifest(format=m3u8-aapl)

## <a name="add-a-webhook-to-your-encoding-task"></a>Bir Web kancası kodlama göreviniz ekleme

Bu bölümde, bir Web kancası bildirim için bir görev ekler ve kod gösterilir. Zincirleme görevler içeren bir iş için daha kullanışlı olurdu bir proje düzeyi bildirim de ekleyebilirsiniz.  

1. Visual Studio’da yeni bir C# Konsol Uygulaması oluşturun. Adını, konumunu ve çözüm adı girin ve Tamam'ı tıklatın.
2. Kullanım [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) Azure Media Services yüklemek için.
3. App.config dosyasını uygun değerlerle güncelleştirin: 
    
    * Azure Media Services bağlantı bilgilerini, 
    * bildirimleri almak için beklediği Web kancası URL'si 
    * Web kancası bekliyor anahtarla eşleşen imzalama anahtarı. İmzalama anahtarı korumak ve Azure Media Services, Web kancalarını geri aramalar güvenli hale getirmek için kullanılan 64 baytlık Base64 ile kodlanmış değerdir. 

            <appSettings>
              <add key="AMSAADTenantDomain" value="domain" />
              <add key="AMSRESTAPIEndpoint" value="endpoint" />

              <add key="AMSClientId" value="clinet id" />
              <add key="AMSClientSecret" value="client secret" />

              <add key="WebhookURL" value="https://yourapp.azurewebsites.net/api/functionname?code=ApiKey" />
              <add key="WebhookSigningKey" value="j0txf1f8msjytzvpe40nxbpxdcxtqcgxy0nt" />
            </appSettings>

4. Program.cs dosyanıza aşağıdaki kod ile güncelleştirin:

        using System;
        using System.Configuration;
        using System.Linq;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace NotificationWebHook
        {
            class Program
            {
            // Read values from the App.config file.
            private static readonly string _AMSAADTenantDomain =
                ConfigurationManager.AppSettings["AMSAADTenantDomain"];
            private static readonly string _AMSRESTAPIEndpoint =
                ConfigurationManager.AppSettings["AMSRESTAPIEndpoint"];

            private static readonly string _AMSClientId =
                ConfigurationManager.AppSettings["AMSClientId"];
            private static readonly string _AMSClientSecret =
                ConfigurationManager.AppSettings["AMSClientSecret"];

            private static readonly string _webHookEndpoint =
                ConfigurationManager.AppSettings["WebhookURL"];
            private static readonly string _signingKey =
                 ConfigurationManager.AppSettings["WebhookSigningKey"];

            // Field for service context.
            private static CloudMediaContext _context = null;

            static void Main(string[] args)
            {
                AzureAdTokenCredentials tokenCredentials = new AzureAdTokenCredentials(_AMSAADTenantDomain,
                    new AzureAdClientSymmetricKey(_AMSClientId, _AMSClientSecret),
                    AzureEnvironments.AzureCloudEnvironment);

                AzureAdTokenProvider tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                _context = new CloudMediaContext(new Uri(_AMSRESTAPIEndpoint), tokenProvider);

                byte[] keyBytes = Convert.FromBase64String(_signingKey);

                IAsset newAsset = _context.Assets.FirstOrDefault();

                // Check for existing Notification Endpoint with the name "FunctionWebHook"

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

                // Declare a new encoding job with the Standard encoder
                IJob job = _context.Jobs.Create("MES Job");

                // Get a media processor reference, and pass to it the name of the 
                // processor to use for the specific task.
                IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

                ITask task = job.Tasks.AddNew("My encoding task",
                processor,
                "Adaptive Streaming",
                TaskOptions.None);

                // Specify the input asset to be encoded.
                task.InputAssets.Add(newAsset);

                // Add an output asset to contain the results of the job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means the output asset is not encrypted. 
                task.OutputAssets.AddNew(newAsset.Name, AssetCreationOptions.None);

                // Add the WebHook notification to this Task and request all notification state changes.
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

                Console.WriteLine("Expect WebHook to be triggered for the Job ID: {0}", job.Id);
                Console.WriteLine("Expect WebHook to be triggered for the Task ID: {0}", task.Id);

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

## <a name="next-steps"></a>Sonraki adımlar

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
