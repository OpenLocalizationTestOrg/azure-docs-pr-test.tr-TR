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
# <a name="use-azure-webhooks-toomonitor-media-services-job-notifications-with-net"></a><span data-ttu-id="29a9d-104">Azure Web Kancalarını toomonitor Media Services iş bildirimleri .NET ile kullanma</span><span class="sxs-lookup"><span data-stu-id="29a9d-104">Use Azure WebHooks toomonitor Media Services job notifications with .NET</span></span>
<span data-ttu-id="29a9d-105">İşlerini çalıştırdığınızda, genellikle bir şekilde tootrack ilerleyişini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="29a9d-105">When you run jobs, you often require a way tootrack job progress.</span></span> <span data-ttu-id="29a9d-106">Azure Web Kancalarını kullanarak Media Services iş bildirimleri izleyebilirsiniz veya [Azure kuyruk depolama](media-services-dotnet-check-job-progress-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="29a9d-106">You can monitor Media Services job notifications by using Azure Webhooks or [Azure Queue storage](media-services-dotnet-check-job-progress-with-queues.md).</span></span> <span data-ttu-id="29a9d-107">Bu konuda gösterilmektedir nasıl Kancalarını ile toowork.</span><span class="sxs-lookup"><span data-stu-id="29a9d-107">This topic shows how toowork with Webhooks.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29a9d-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="29a9d-108">Prerequisites</span></span>

<span data-ttu-id="29a9d-109">Merhaba, gerekli toocomplete hello öğretici şunlardır:</span><span class="sxs-lookup"><span data-stu-id="29a9d-109">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="29a9d-110">Bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="29a9d-110">An Azure account.</span></span> <span data-ttu-id="29a9d-111">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="29a9d-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="29a9d-112">Bir Media Services hesabı.</span><span class="sxs-lookup"><span data-stu-id="29a9d-112">A Media Services account.</span></span> <span data-ttu-id="29a9d-113">bir Media Services hesabı toocreate bkz [nasıl tooCreate Media Services hesabı](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="29a9d-113">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="29a9d-114">Anlayış [nasıl toouse Azure işlevleri](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="29a9d-114">Understanding of [how toouse Azure functions](../azure-functions/functions-overview.md).</span></span> <span data-ttu-id="29a9d-115">Ayrıca, gözden [Azure işlevleri HTTP ve Web kancası bağlamaları](../azure-functions/functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="29a9d-115">Also, review [Azure functions HTTP and webhook bindings](../azure-functions/functions-bindings-http-webhook.md).</span></span>

<span data-ttu-id="29a9d-116">Bu konuda gösterilmektedir nasıl</span><span class="sxs-lookup"><span data-stu-id="29a9d-116">This topic shows how to</span></span>

*  <span data-ttu-id="29a9d-117">Özelleştirilmiş toorespond toowebhooks olan bir Azure işlevi tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="29a9d-117">Define an Azure Function that is customized toorespond toowebhooks.</span></span> 
    
    <span data-ttu-id="29a9d-118">Bu durumda, kodlama işinin durumu değiştiğinde hello Web kancası Media Services tarafından tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="29a9d-118">In this case, hello webhook is triggered by Media Services when your encoding job changes status.</span></span> <span data-ttu-id="29a9d-119">Merhaba işlevi hello Web kancası çağrısından geri Media Services bildirimleri dinler ve hello işi tamamlandıktan sonra hello çıkış varlığına yayımlar.</span><span class="sxs-lookup"><span data-stu-id="29a9d-119">hello function listens for hello webhook call back from Media Services notifications and publishes hello output asset once hello job finishes.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="29a9d-120">Devam etmeden önce anladığınızdan emin olun nasıl [Azure işlevleri HTTP ve Web kancası bağlamaları](../azure-functions/functions-bindings-http-webhook.md) çalışır.</span><span class="sxs-lookup"><span data-stu-id="29a9d-120">Before continuing, make sure you understand how [Azure Functions HTTP and webhook bindings](../azure-functions/functions-bindings-http-webhook.md) work.</span></span>
    >
    
* <span data-ttu-id="29a9d-121">Bir Web kancası tooyour kodlama görev ekleyin ve bu Web kancası yanıtlaması gizli anahtar ve hello Web kancası URL'si belirtin.</span><span class="sxs-lookup"><span data-stu-id="29a9d-121">Add a webhook tooyour encoding task and specify hello webhook URL and secret key that this webhook responds to.</span></span> <span data-ttu-id="29a9d-122">Burada gösterilen hello örnekte görev kodlama hello oluşturan hello bir konsol uygulaması kodudur.</span><span class="sxs-lookup"><span data-stu-id="29a9d-122">In hello example shown here, hello code that creates hello encoding task is a console app.</span></span>

## <a name="setting-up-webhook-notification-azure-functions"></a><span data-ttu-id="29a9d-123">Azure işlevleri "Web kancası bildirimi" ayarlama</span><span class="sxs-lookup"><span data-stu-id="29a9d-123">Setting up "webhook notification" Azure functions</span></span>

<span data-ttu-id="29a9d-124">Bu bölümdeki Hello kodu bir Web kancası olan bir Azure işlevi uygulaması gösterilir.</span><span class="sxs-lookup"><span data-stu-id="29a9d-124">hello code in this section shows an implementation of an Azure function that is a webhook.</span></span> <span data-ttu-id="29a9d-125">Bu örnek hello işlevi hello Web kancası çağrısından geri Media Services bildirimleri dinler ve hello işi tamamlandıktan sonra hello çıkış varlığına yayımlar.</span><span class="sxs-lookup"><span data-stu-id="29a9d-125">In this sample, hello function listens for hello webhook call back from Media Services notifications and publishes hello output asset once hello job finishes.</span></span>

<span data-ttu-id="29a9d-126">Merhaba Web kancası bekliyor imzalama anahtarı (kimlik) toomatch bir hello bildirim bitiş noktası yapılandırdığınızda geçirdiğiniz hello.</span><span class="sxs-lookup"><span data-stu-id="29a9d-126">hello webhook expects a signing key (credential) toomatch hello one you pass when you configure hello notification endpoint.</span></span> <span data-ttu-id="29a9d-127">imzalama anahtarı hello kullanılan tooprotect ve Azure Media Services, Web Kancalarını geri aramalar güvenli hello 64 baytlık Base64 ile kodlanmış değerdir.</span><span class="sxs-lookup"><span data-stu-id="29a9d-127">hello signing key is hello 64-byte Base64 encoded value that is used tooprotect and secure your WebHooks callbacks from Azure Media Services.</span></span> 

<span data-ttu-id="29a9d-128">Koddan hello hello **VerifyWebHookRequestSignature** yöntemi hello bildirim iletisi doğrulamayı hello.</span><span class="sxs-lookup"><span data-stu-id="29a9d-128">In hello following code, hello **VerifyWebHookRequestSignature** method does hello verification on hello notification message.</span></span> <span data-ttu-id="29a9d-129">Merhaba amacı, bu doğrulama ileti hello tooensure Azure Media Services tarafından gönderilen ve oynanmadığını ' dir.</span><span class="sxs-lookup"><span data-stu-id="29a9d-129">hello purpose of this validation is tooensure that hello message was sent by Azure Media Services and hasn’t been tampered with.</span></span> <span data-ttu-id="29a9d-130">Merhaba olduğu gibi Hello imza Azure işlevleri için isteğe bağlı **kod** değeri olarak bir sorgu parametresi üzerinden Aktarım Katmanı Güvenliği (TLS).</span><span class="sxs-lookup"><span data-stu-id="29a9d-130">hello signature is optional for Azure functions as it has hello **Code** value as a query parameter over Transport Layer Security (TLS).</span></span> 

<span data-ttu-id="29a9d-131">Çeşitli Media Services .NET Azure işlevleri (Merhaba biri bu konuda gösterilen dahil) hello tanımını bulabilirsiniz [burada](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="29a9d-131">You can find hello definition of various Media Services .NET Azure functions (including hello one shown in this topic) [here](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span>

<span data-ttu-id="29a9d-132">Merhaba aşağıdaki kod listesi gösterir Azure işlev parametrelerini ve hello Azure işlevi ile ilişkili olan üç dosyaları hello tanımları: function.json, project.json ve run.csx.</span><span class="sxs-lookup"><span data-stu-id="29a9d-132">hello following code listing shows hello definitions of Azure function parameters and three files that are associated with hello Azure function: function.json, project.json, and run.csx.</span></span>

### <a name="application-settings"></a><span data-ttu-id="29a9d-133">Uygulama ayarları</span><span class="sxs-lookup"><span data-stu-id="29a9d-133">Application settings</span></span> 

<span data-ttu-id="29a9d-134">Merhaba aşağıdaki tabloda hello bu bölümünde tanımlanan Azure işlevi tarafından kullanılan hello parametrelerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="29a9d-134">hello following table shows hello parameters that are used by hello Azure function defined in this section.</span></span> 

|<span data-ttu-id="29a9d-135">Ad</span><span class="sxs-lookup"><span data-stu-id="29a9d-135">Name</span></span>|<span data-ttu-id="29a9d-136">Tanım</span><span class="sxs-lookup"><span data-stu-id="29a9d-136">Definition</span></span>|<span data-ttu-id="29a9d-137">Örnek</span><span class="sxs-lookup"><span data-stu-id="29a9d-137">Example</span></span>| 
|---|---|---|
|<span data-ttu-id="29a9d-138">AMSAccount</span><span class="sxs-lookup"><span data-stu-id="29a9d-138">AMSAccount</span></span>|<span data-ttu-id="29a9d-139">AMS hesabının adı.</span><span class="sxs-lookup"><span data-stu-id="29a9d-139">Your AMS account name.</span></span> |<span data-ttu-id="29a9d-140">juliakomediaservices</span><span class="sxs-lookup"><span data-stu-id="29a9d-140">juliakomediaservices</span></span>|
|<span data-ttu-id="29a9d-141">AMSKey</span><span class="sxs-lookup"><span data-stu-id="29a9d-141">AMSKey</span></span> |<span data-ttu-id="29a9d-142">AMS hesap anahtarınızı.</span><span class="sxs-lookup"><span data-stu-id="29a9d-142">Your AMS account key.</span></span> | <span data-ttu-id="29a9d-143">JUWJdDaOHQQqsZeiXZuE76eDt2SO + YMJk25Lghgy2nY =</span><span class="sxs-lookup"><span data-stu-id="29a9d-143">JUWJdDaOHQQqsZeiXZuE76eDt2SO+YMJk25Lghgy2nY=</span></span>|
|<span data-ttu-id="29a9d-144">MediaServicesStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="29a9d-144">MediaServicesStorageAccountName</span></span> |<span data-ttu-id="29a9d-145">AMS hesabınızla ilişkili hello depolama hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="29a9d-145">A name of hello storage account that is associated with your AMS account.</span></span>| <span data-ttu-id="29a9d-146">storagepkeewmg5c3peq</span><span class="sxs-lookup"><span data-stu-id="29a9d-146">storagepkeewmg5c3peq</span></span>|
|<span data-ttu-id="29a9d-147">MediaServicesStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="29a9d-147">MediaServicesStorageAccountKey</span></span> |<span data-ttu-id="29a9d-148">AMS hesabınızla ilişkili hello depolama hesabı anahtarı.</span><span class="sxs-lookup"><span data-stu-id="29a9d-148">A key of hello storage account that is associated with your AMS account.</span></span>|
|<span data-ttu-id="29a9d-149">SigningKey</span><span class="sxs-lookup"><span data-stu-id="29a9d-149">SigningKey</span></span> |<span data-ttu-id="29a9d-150">İmzalama anahtarı.</span><span class="sxs-lookup"><span data-stu-id="29a9d-150">A signing key.</span></span>| <span data-ttu-id="29a9d-151">j0txf1f8msjytzvpe40nxbpxdcxtqcgxy0nt</span><span class="sxs-lookup"><span data-stu-id="29a9d-151">j0txf1f8msjytzvpe40nxbpxdcxtqcgxy0nt</span></span>|
|<span data-ttu-id="29a9d-152">WebHookEndpoint</span><span class="sxs-lookup"><span data-stu-id="29a9d-152">WebHookEndpoint</span></span> | <span data-ttu-id="29a9d-153">Bir Web kancası uç nokta adresi.</span><span class="sxs-lookup"><span data-stu-id="29a9d-153">A webhook endpoint address.</span></span> | <span data-ttu-id="29a9d-154">https://juliakofuncapp.azurewebsites.NET/api/Notification_Webhook_Function?Code=iN2phdrTnCxmvaKExFWOTulfnm4C71mMLIy8tzLr7Zvf6Z22HHIK5g==.</span><span class="sxs-lookup"><span data-stu-id="29a9d-154">https://juliakofuncapp.azurewebsites.net/api/Notification_Webhook_Function?code=iN2phdrTnCxmvaKExFWOTulfnm4C71mMLIy8tzLr7Zvf6Z22HHIK5g==.</span></span>|

### <a name="functionjson"></a><span data-ttu-id="29a9d-155">Function.JSON</span><span class="sxs-lookup"><span data-stu-id="29a9d-155">function.json</span></span>

<span data-ttu-id="29a9d-156">Merhaba function.json dosyası hello işlev bağlamaları ve diğer yapılandırma ayarlarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="29a9d-156">hello function.json file defines hello function bindings and other configuration settings.</span></span> <span data-ttu-id="29a9d-157">Bu dosya toodetermine hello olayları toomonitor ve yürütme toopass verisine ve dönüş verileri nasıl işlev Hello çalışma zamanı kullanır.</span><span class="sxs-lookup"><span data-stu-id="29a9d-157">hello runtime uses this file toodetermine hello events toomonitor and how toopass data into and return data from function execution.</span></span> 

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
    
### <a name="projectjson"></a><span data-ttu-id="29a9d-158">Project.JSON</span><span class="sxs-lookup"><span data-stu-id="29a9d-158">project.json</span></span>

<span data-ttu-id="29a9d-159">Merhaba project.json dosyası bağımlılıkları içerir.</span><span class="sxs-lookup"><span data-stu-id="29a9d-159">hello project.json file contains dependencies.</span></span> 

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
    
### <a name="runcsx"></a><span data-ttu-id="29a9d-160">Run.csx</span><span class="sxs-lookup"><span data-stu-id="29a9d-160">run.csx</span></span>

<span data-ttu-id="29a9d-161">Merhaba aşağıdaki C# kodu bir Web kancası olan bir Azure işlevi tanımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="29a9d-161">hello following C# code shows a definition of an Azure function that is a webhook.</span></span> <span data-ttu-id="29a9d-162">Merhaba işlevi hello Web kancası çağrısından geri Media Services bildirimleri dinler ve hello işi tamamlandıktan sonra hello çıkış varlığına yayımlar.</span><span class="sxs-lookup"><span data-stu-id="29a9d-162">hello function listens for hello webhook call back from Media Services notifications and publishes hello output asset once hello job finishes.</span></span> 


>[!NOTE]
><span data-ttu-id="29a9d-163">Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için).</span><span class="sxs-lookup"><span data-stu-id="29a9d-163">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="29a9d-164">Merhaba kullanması gereken her zaman kullanıyorsanız, aynı ilke kimliği hello aynı gün / erişim izinlerini, örneğin, uzun bir süre (karşıya yükleme olmayan ilkeleri) yerinde hedeflenen tooremain olan bulucular ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="29a9d-164">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="29a9d-165">Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="29a9d-165">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

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

### <a name="function-output"></a><span data-ttu-id="29a9d-166">İşlevi çıktı</span><span class="sxs-lookup"><span data-stu-id="29a9d-166">Function output</span></span>

<span data-ttu-id="29a9d-167">Yukarıdaki Hello örnek çıktı aşağıdaki hello üretilen, değerlerinizi farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="29a9d-167">hello example above produced hello following output, your values will vary.</span></span>

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

## <a name="adding-webhook-tooyour-encoding-task"></a><span data-ttu-id="29a9d-168">Web kancası tooyour kodlama görev ekleme</span><span class="sxs-lookup"><span data-stu-id="29a9d-168">Adding Webhook tooyour encoding task</span></span>

<span data-ttu-id="29a9d-169">Bu bölümde, bir Web kancası bildirim tooa görev ekler hello kodu gösterilir.</span><span class="sxs-lookup"><span data-stu-id="29a9d-169">In this section, hello code that adds a webhook notification tooa Task is shown.</span></span> <span data-ttu-id="29a9d-170">Zincirleme görevler içeren bir iş için daha kullanışlı olurdu bir proje düzeyi bildirim de ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29a9d-170">You can also add a job level notification, which would be more useful for a job with chained tasks.</span></span>  

1. <span data-ttu-id="29a9d-171">Visual Studio’da yeni bir C# Konsol Uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="29a9d-171">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="29a9d-172">Merhaba adını, konumunu ve çözüm adı girin ve Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="29a9d-172">Enter hello Name, Location, and Solution name, and then click OK.</span></span>
2. <span data-ttu-id="29a9d-173">Kullanım [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) tooinstall Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="29a9d-173">Use [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) tooinstall Azure Media Services.</span></span>
3. <span data-ttu-id="29a9d-174">App.config dosyasını uygun değerlerle güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="29a9d-174">Update App.config file with appropriate values:</span></span> 
    
    * <span data-ttu-id="29a9d-175">Azure Media Services adını ve bildirimleri gönderme anahtarı</span><span class="sxs-lookup"><span data-stu-id="29a9d-175">Azure Media Services name and key that will be sending notifications,</span></span> 
    * <span data-ttu-id="29a9d-176">tooget hello bildirimleri beklediği Web kancası URL'si</span><span class="sxs-lookup"><span data-stu-id="29a9d-176">webhook URL that expects tooget hello notifications,</span></span> 
    * <span data-ttu-id="29a9d-177">Merhaba, Web kancası bekliyor hello anahtarla eşleşen anahtara imzalama.</span><span class="sxs-lookup"><span data-stu-id="29a9d-177">hello signing key that matches hello key that your webhook expects.</span></span> <span data-ttu-id="29a9d-178">imzalama anahtarı hello kullanılan tooprotect ve Azure Media Services, Web Kancalarını geri aramalar güvenli hello 64 baytlık Base64 ile kodlanmış değerdir.</span><span class="sxs-lookup"><span data-stu-id="29a9d-178">hello signing key is hello 64-byte Base64 encoded value that is used tooprotect and secure your WebHooks callbacks from Azure Media Services.</span></span> 

            <appSettings>
              <add key="MediaServicesAccountName" value="AMSAcctName" />
              <add key="MediaServicesAccountKey" value="AMSAcctKey" />
              <add key="WebhookURL" value="https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>" />
              <add key="WebhookSigningKey" value="j0txf1f8msjytzvpe40nxbpxdcxtqcgxy0nt" />
            </appSettings>
            
4. <span data-ttu-id="29a9d-179">Program.cs dosyanızdaki koddan hello ile güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="29a9d-179">Update your Program.cs file with hello following code:</span></span>

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

## <a name="next-step"></a><span data-ttu-id="29a9d-180">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="29a9d-180">Next step</span></span>
<span data-ttu-id="29a9d-181">Gözden geçirme Media Services'i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="29a9d-181">Review Media Services learning paths</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="29a9d-182">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="29a9d-182">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
