---
title: "App Service API uygulaması Tetikleyicileri | Microsoft Docs"
description: "Azure App Service'deki bir API uygulamasında Tetikleyicileri gerçekleştirme"
services: logic-apps
documentationcenter: .net
author: guangyang
manager: erikre
editor: jimbe
ms.assetid: 493c3703-786d-4434-9dca-8f77744b2f5d
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/25/2016
ms.author: rachelap
ms.openlocfilehash: 3ddfb142e7f1a47e2a8564387da785acf36fa61f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-api-app-triggers"></a><span data-ttu-id="af5a9-103">Azure App Service API uygulaması tetikleyicileri</span><span class="sxs-lookup"><span data-stu-id="af5a9-103">Azure App Service API app triggers</span></span>
> [!NOTE]
> <span data-ttu-id="af5a9-104">Makalenin bu sürümü, API apps 2014-12-01-Önizleme şema sürümü için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="af5a9-104">This version of the article applies to API apps 2014-12-01-preview schema version.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="af5a9-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="af5a9-105">Overview</span></span>
<span data-ttu-id="af5a9-106">Bu makalede, API uygulaması Tetikleyicileri uygulamak ve bir mantıksal uygulama kullanma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="af5a9-106">This article explains how to implement API app triggers and consume them from a Logic app.</span></span>

<span data-ttu-id="af5a9-107">Bu konudaki kod parçacıkları tümünün kopyalandığı [FileWatcher API uygulaması kod örneği](http://go.microsoft.com/fwlink/?LinkId=534802).</span><span class="sxs-lookup"><span data-stu-id="af5a9-107">All of the code snippets in this topic are copied from the [FileWatcher API App code sample](http://go.microsoft.com/fwlink/?LinkId=534802).</span></span>

<span data-ttu-id="af5a9-108">Kodu derlemek ve çalıştırmak için bu makaledeki için aşağıdaki nuget paketini karşıdan yüklemek için gereken Not: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span><span class="sxs-lookup"><span data-stu-id="af5a9-108">Note that you'll need to download the following nuget package for the code in this article to build and run: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span></span>

## <a name="what-are-api-app-triggers"></a><span data-ttu-id="af5a9-109">API uygulaması Tetikleyicileri nelerdir?</span><span class="sxs-lookup"><span data-stu-id="af5a9-109">What are API app triggers?</span></span>
<span data-ttu-id="af5a9-110">Böylece istemciler API uygulamasının olaya yanıt olarak uygun eylemi gerçekleştirin bir olay tetikleyin için API uygulaması için ortak bir senaryodur.</span><span class="sxs-lookup"><span data-stu-id="af5a9-110">It's a common scenario for an API app to fire an event so that clients of the API app can take the appropriate action in response to the event.</span></span> <span data-ttu-id="af5a9-111">Bu senaryoyu destekler REST API'si mekanizması bir API uygulaması Tetikleyici adı verilir.</span><span class="sxs-lookup"><span data-stu-id="af5a9-111">The REST API based mechanism that supports this scenario is called an API app trigger.</span></span>

<span data-ttu-id="af5a9-112">Örneğin, istemci kodunuzun kullandığını varsayalım [Twitter Bağlayıcısı API uygulaması](../connectors/connectors-create-api-twitter.md) ve belirli sözcükleri içeren yeni tweet'leri üzerinde dayalı bir eylemi gerçekleştirmek kodunuzu gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="af5a9-112">For example, let's say your client code is using the [Twitter Connector API app](../connectors/connectors-create-api-twitter.md) and your code needs to perform an action based on new tweets that contain specific words.</span></span> <span data-ttu-id="af5a9-113">Bu durumda, bu gereksinimi kolaylaştırmak için yoklama veya itme tetikleyicisi ayarlayabilir.</span><span class="sxs-lookup"><span data-stu-id="af5a9-113">In this case, you might set up a poll or push trigger to facilitate this need.</span></span>

## <a name="poll-trigger-versus-push-trigger"></a><span data-ttu-id="af5a9-114">Yoklama tetikleyici itme tetikleyici karşılaştırması</span><span class="sxs-lookup"><span data-stu-id="af5a9-114">Poll trigger versus push trigger</span></span>
<span data-ttu-id="af5a9-115">İki tür tetikleyici sunucusu şu anda desteklenir:</span><span class="sxs-lookup"><span data-stu-id="af5a9-115">Currently, two types of triggers are supported:</span></span>

* <span data-ttu-id="af5a9-116">Yoklama tetikleyici - istemci bildirimi harekete bir olay için API uygulaması yoklar.</span><span class="sxs-lookup"><span data-stu-id="af5a9-116">Poll trigger - Client polls the API app for notification of an event having been fired</span></span>
* <span data-ttu-id="af5a9-117">Bir olay başlatıldığında itme tetikleyici - istemci API uygulaması tarafından bildirilir</span><span class="sxs-lookup"><span data-stu-id="af5a9-117">Push trigger - Client is notified by the API app when an event fires</span></span>

### <a name="poll-trigger"></a><span data-ttu-id="af5a9-118">Yoklama tetikleyici</span><span class="sxs-lookup"><span data-stu-id="af5a9-118">Poll trigger</span></span>
<span data-ttu-id="af5a9-119">Yoklama tetikleyici normal bir REST API uygulanır ve istemcilerine (örneğin, bir mantıksal uygulama) bildirim almak için yoklamak için bekliyor.</span><span class="sxs-lookup"><span data-stu-id="af5a9-119">A poll trigger is implemented as a regular REST API and expects its clients (such as a Logic app) to poll it in order to get notification.</span></span> <span data-ttu-id="af5a9-120">İstemci durumunu korumak, ancak yoklama tetikleyici durum bilgisiz.</span><span class="sxs-lookup"><span data-stu-id="af5a9-120">While the client may maintain state, the poll trigger itself is stateless.</span></span>

<span data-ttu-id="af5a9-121">İstek ve yanıt paketleri ilgili aşağıdaki bilgileri yoklama tetikleyici sözleşme anahtar bazı yönleri gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="af5a9-121">The following information regarding the request and response packets illustrate some key aspects of the poll trigger contract:</span></span>

* <span data-ttu-id="af5a9-122">İstek</span><span class="sxs-lookup"><span data-stu-id="af5a9-122">Request</span></span>
  * <span data-ttu-id="af5a9-123">HTTP yöntemini: Al</span><span class="sxs-lookup"><span data-stu-id="af5a9-123">HTTP method: GET</span></span>
  * <span data-ttu-id="af5a9-124">Parametreler</span><span class="sxs-lookup"><span data-stu-id="af5a9-124">Parameters</span></span>
    * <span data-ttu-id="af5a9-125">triggerState - yoklama tetikleyici düzgün veya bildirim döndürülecek karar verebilir böylece durumlarına belirtilen durumuna bağlı belirtmek istemcilerin bu isteğe bağlı parametre sağlar.</span><span class="sxs-lookup"><span data-stu-id="af5a9-125">triggerState - This optional parameter allows clients to specify their state so that the poll trigger can properly decide whether to return notification or not based on the specified state.</span></span>
    * <span data-ttu-id="af5a9-126">API özel parametreler</span><span class="sxs-lookup"><span data-stu-id="af5a9-126">API-specific parameters</span></span>
* <span data-ttu-id="af5a9-127">Yanıt</span><span class="sxs-lookup"><span data-stu-id="af5a9-127">Response</span></span>
  * <span data-ttu-id="af5a9-128">Durum kodu **200** - istek geçerli ve tetikleyici bildirimden yoktur.</span><span class="sxs-lookup"><span data-stu-id="af5a9-128">Status code **200** - Request is valid and there is a notification from the trigger.</span></span> <span data-ttu-id="af5a9-129">Bildirim içeriğini yanıt gövdesi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="af5a9-129">The content of the notification will be the response body.</span></span> <span data-ttu-id="af5a9-130">Ek bildirim verileri bir sonraki istek çağrısı ile alınması gereken bir "Yeniden deneme-sonra" üstbilgisi yanıt gösterir.</span><span class="sxs-lookup"><span data-stu-id="af5a9-130">A "Retry-After" header in the response indicates that additional notification data must be retrieved with a subsequent request call.</span></span>
  * <span data-ttu-id="af5a9-131">Durum kodu **202** - istek geçerlidir, ancak tetikleyici öğesinden yeni bildirim yoktur.</span><span class="sxs-lookup"><span data-stu-id="af5a9-131">Status code **202** - Request is valid, but there is no new notification from the trigger.</span></span>
  * <span data-ttu-id="af5a9-132">Durum kodu **4xx** -isteği geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="af5a9-132">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="af5a9-133">İstemci isteği yeniden.</span><span class="sxs-lookup"><span data-stu-id="af5a9-133">The client should not retry the request.</span></span>
  * <span data-ttu-id="af5a9-134">Durum kodu **5xx** -isteği bir iç sunucu hatası ve/veya geçici bir sorun içinde sonuçlandı.</span><span class="sxs-lookup"><span data-stu-id="af5a9-134">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="af5a9-135">İstemci isteği yeniden denemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="af5a9-135">The client should retry the request.</span></span>

<span data-ttu-id="af5a9-136">Aşağıdaki kod parçacığını bir yoklama Tetik uygulamak nasıl bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="af5a9-136">The following code snippet is an example of how to implement a poll trigger.</span></span>

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check to see whether there is any file touched after the timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after the timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by the AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after the timestamp, tell the caller to poll again after 1 mintue.
        else
        {
            // Extension method provided by the AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

<span data-ttu-id="af5a9-137">Bu yoklama tetikleyici sınamak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="af5a9-137">To test this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="af5a9-138">Bir kimlik doğrulama ayarı olan API uygulaması dağıtma **ortak anonim**.</span><span class="sxs-lookup"><span data-stu-id="af5a9-138">Deploy the API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="af5a9-139">Çağrı **touch** bir dosya touch işlemi.</span><span class="sxs-lookup"><span data-stu-id="af5a9-139">Call the **touch** operation to touch a file.</span></span> <span data-ttu-id="af5a9-140">Aşağıdaki resimde bir örnek istek Postman aracılığıyla gösterir.</span><span class="sxs-lookup"><span data-stu-id="af5a9-140">The following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="af5a9-141">![Postman aracılığıyla dokunma işlem çağırma](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="af5a9-141">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
3. <span data-ttu-id="af5a9-142">Yoklama tetikleyiciyle çağrısı **triggerState** #2. adım önce bir zaman damgası parametresini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="af5a9-142">Call the poll trigger with the **triggerState** parameter set to a time stamp prior to Step #2.</span></span> <span data-ttu-id="af5a9-143">Aşağıdaki resimde Postman aracılığıyla örnek isteğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="af5a9-143">The following image shows the sample request via Postman.</span></span>
   <span data-ttu-id="af5a9-144">![Postman aracılığıyla çağrı yoklama tetikleyici](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="af5a9-144">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span></span>

### <a name="push-trigger"></a><span data-ttu-id="af5a9-145">Tetikleyici bildirme</span><span class="sxs-lookup"><span data-stu-id="af5a9-145">Push trigger</span></span>
<span data-ttu-id="af5a9-146">Anında iletme tetikleyicinin belirli olay tetiklendiğinde bildirim almak için kaydettiniz istemciler için bildirimler iter normal bir REST API olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="af5a9-146">A push trigger is implemented as a regular REST API that pushes notifications to clients who have registered to be notified when specific events fire.</span></span>

<span data-ttu-id="af5a9-147">İstek ve yanıt paketleri ilgili aşağıdaki bilgileri anında tetikleyici sözleşme anahtar bazı yönleri gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="af5a9-147">The following information regarding the request and response packets illustrate some key aspects of the push trigger contract.</span></span>

* <span data-ttu-id="af5a9-148">İstek</span><span class="sxs-lookup"><span data-stu-id="af5a9-148">Request</span></span>
  * <span data-ttu-id="af5a9-149">HTTP yöntemini: YERLEŞTİRME</span><span class="sxs-lookup"><span data-stu-id="af5a9-149">HTTP method: PUT</span></span>
  * <span data-ttu-id="af5a9-150">Parametreler</span><span class="sxs-lookup"><span data-stu-id="af5a9-150">Parameters</span></span>
    * <span data-ttu-id="af5a9-151">Tetikleyici No: gerekli - itme tetikleyici kaydını temsil eden donuk dizesini (örneğin, bir GUID).</span><span class="sxs-lookup"><span data-stu-id="af5a9-151">triggerId: required - Opaque string (such as a GUID) that represents the registration of a push trigger.</span></span>
    * <span data-ttu-id="af5a9-152">callbackUrl: gerekli - olay başlatıldığında çağırmak geri çağırma URL'si.</span><span class="sxs-lookup"><span data-stu-id="af5a9-152">callbackUrl: required - URL of the callback to invoke when the event fires.</span></span> <span data-ttu-id="af5a9-153">Basit bir POST HTTP çağrısıyla çağrıdır.</span><span class="sxs-lookup"><span data-stu-id="af5a9-153">The invocation is a simple POST HTTP call.</span></span>
    * <span data-ttu-id="af5a9-154">API özel parametreler</span><span class="sxs-lookup"><span data-stu-id="af5a9-154">API-specific parameters</span></span>
* <span data-ttu-id="af5a9-155">Yanıt</span><span class="sxs-lookup"><span data-stu-id="af5a9-155">Response</span></span>
  * <span data-ttu-id="af5a9-156">Durum kodu **200** -istemci başarılı kaydetmek için istek.</span><span class="sxs-lookup"><span data-stu-id="af5a9-156">Status code **200** - Request to register client successful.</span></span>
  * <span data-ttu-id="af5a9-157">Durum kodu **4xx** -isteği geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="af5a9-157">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="af5a9-158">İstemci isteği yeniden.</span><span class="sxs-lookup"><span data-stu-id="af5a9-158">The client should not retry the request.</span></span>
  * <span data-ttu-id="af5a9-159">Durum kodu **5xx** -isteği bir iç sunucu hatası ve/veya geçici bir sorun içinde sonuçlandı.</span><span class="sxs-lookup"><span data-stu-id="af5a9-159">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="af5a9-160">İstemci isteği yeniden denemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="af5a9-160">The client should retry the request.</span></span>
* <span data-ttu-id="af5a9-161">Geri çağırma</span><span class="sxs-lookup"><span data-stu-id="af5a9-161">Callback</span></span>
  * <span data-ttu-id="af5a9-162">HTTP yöntemini: POST</span><span class="sxs-lookup"><span data-stu-id="af5a9-162">HTTP method: POST</span></span>
  * <span data-ttu-id="af5a9-163">İstek gövdesindeki: bildirim içeriği.</span><span class="sxs-lookup"><span data-stu-id="af5a9-163">Request body: Notification content.</span></span>

<span data-ttu-id="af5a9-164">Aşağıdaki kod parçacığını nasıl anında iletme tetikleyici uygulanacağı örneğidir:</span><span class="sxs-lookup"><span data-stu-id="af5a9-164">The following code snippet is an example of how to implement a push trigger:</span></span>

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by the AppService service SDK.
        // Here it defines the input of the push trigger is a string and the output to the callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register the trigger to some trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by the AppService service SDK indicating the registration is completed.
        return this.Request.PushTriggerRegistered(triggerInput.GetCallback());
    }

    // A simple in-memory trigger store.
    public class InMemoryTriggerStore
    {
        private static InMemoryTriggerStore instance;

        private IDictionary<string, FileSystemWatcher> _store;

        private InMemoryTriggerStore()
        {
            _store = new Dictionary<string, FileSystemWatcher>();
        }

        public static InMemoryTriggerStore Instance
        {
            get
            {
                if (instance == null)
                {
                    instance = new InMemoryTriggerStore();
                }
                return instance;
            }
        }

        // Register a push trigger.
        public void RegisterTrigger(string triggerId, string rootPath,
            TriggerInput<string, FileInfoWrapper> triggerInput)
        {
            // Use FileSystemWatcher to listen to file change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire the push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate the FileSystemWatcher object with the triggerId.
            _store[triggerId] = watcher;

        }

        // Fire the assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed to invoke the callback.
            Runtime runtime,
            // The callback to invoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK to invoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

<span data-ttu-id="af5a9-165">Bu yoklama tetikleyici sınamak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="af5a9-165">To test this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="af5a9-166">Bir kimlik doğrulama ayarı olan API uygulaması dağıtma **ortak anonim**.</span><span class="sxs-lookup"><span data-stu-id="af5a9-166">Deploy the API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="af5a9-167">Gözat [http://requestb.in/](http://requestb.in/) geri çağırma URL'si olarak davranacak bir RequestBin oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="af5a9-167">Browse to [http://requestb.in/](http://requestb.in/) to create a RequestBin which will serve as your callback URL.</span></span>
3. <span data-ttu-id="af5a9-168">Bir GUID olarak itme tetikleyiciyle çağrısı **Tetikleyici No** ve RequestBin URL'si olarak **callbackUrl**.</span><span class="sxs-lookup"><span data-stu-id="af5a9-168">Call the push trigger with a GUID as **triggerId** and the RequestBin URL as **callbackUrl**.</span></span>
   <span data-ttu-id="af5a9-169">![Postman aracılığıyla gönderme tetikleyici çağırın](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="af5a9-169">![Call Push Trigger via Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span></span>
4. <span data-ttu-id="af5a9-170">Çağrı **touch** bir dosya touch işlemi.</span><span class="sxs-lookup"><span data-stu-id="af5a9-170">Call the **touch** operation to touch a file.</span></span> <span data-ttu-id="af5a9-171">Aşağıdaki resimde bir örnek istek Postman aracılığıyla gösterir.</span><span class="sxs-lookup"><span data-stu-id="af5a9-171">The following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="af5a9-172">![Postman aracılığıyla dokunma işlem çağırma](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="af5a9-172">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
5. <span data-ttu-id="af5a9-173">Anında iletme tetikleyici geri çağırma özelliği çıkışıyla çağrılır onaylamak için RequestBin denetleyin.</span><span class="sxs-lookup"><span data-stu-id="af5a9-173">Check the RequestBin to confirm that the push trigger callback is invoked with property output.</span></span>
   <span data-ttu-id="af5a9-174">![Postman aracılığıyla çağrı yoklama tetikleyici](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span><span class="sxs-lookup"><span data-stu-id="af5a9-174">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span></span>

### <a name="describe-triggers-in-api-definition"></a><span data-ttu-id="af5a9-175">API tanımı Tetikleyicileri açıklayın</span><span class="sxs-lookup"><span data-stu-id="af5a9-175">Describe triggers in API definition</span></span>
<span data-ttu-id="af5a9-176">Tetikleyiciler uygulama ve API uygulamanızı Azure'a dağıtan sonra gidin **API tanımı** dikey Azure Önizleme portalını ve Tetikleyicileri Swagger tarafından yönetilen kullanıcı arabiriminde otomatik olarak tanınır göreceksiniz 2.0 API uygulaması API tanımı.</span><span class="sxs-lookup"><span data-stu-id="af5a9-176">After implementing the triggers and deploying your API app to Azure, navigate to the **API Definition** blade in the Azure preview portal and you'll see that triggers are automatically recognized in the UI, which is driven by the Swagger 2.0 API definition of the API app.</span></span>

![API tanımı dikey penceresi](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

<span data-ttu-id="af5a9-178">Tıklatırsanız **karşıdan Swagger** düğmesini tıklatın ve JSON dosyasını açın, aşağıdakine benzer sonuçlar görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="af5a9-178">If you click the **Download Swagger** button and open the JSON file, you'll see results similar to the following:</span></span>

    "/api/files/poll/TouchedFiles": {
      "get": {
        "operationId": "Files_TouchedFilesPollTrigger",
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    },
    "/api/files/push/TouchedFiles/{triggerId}": {
      "put": {
        "operationId": "Files_TouchedFilesPushTrigger",
        ...
        "x-ms-scheduler-trigger": "push"
      }
    }

<span data-ttu-id="af5a9-179">Uzantı özelliği **x-ms-schedular-tetikleyici** nasıl Tetikleyicileri API tanımı'nda açıklanan olduğu ve varsa ağ geçidi üzerinden API tanımı istediğinde API uygulama ağ geçidi tarafından otomatik olarak eklenen birini isteği aşağıdaki ölçütleri.</span><span class="sxs-lookup"><span data-stu-id="af5a9-179">The extension property **x-ms-schedular-trigger** is how triggers are described in API definition, and is automatically added by the API app gateway when you request the API definition via the gateway if the request to one of the following criteria.</span></span> <span data-ttu-id="af5a9-180">(, Bu özellik el ile de ekleyebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="af5a9-180">(You can also add this property manually.)</span></span>

* <span data-ttu-id="af5a9-181">Yoklama tetikleyici</span><span class="sxs-lookup"><span data-stu-id="af5a9-181">Poll trigger</span></span>
  * <span data-ttu-id="af5a9-182">HTTP yöntemi ise **almak**.</span><span class="sxs-lookup"><span data-stu-id="af5a9-182">If the HTTP method is **GET**.</span></span>
  * <span data-ttu-id="af5a9-183">Varsa **Operationıd** özelliği içeren dize **tetikleyici**.</span><span class="sxs-lookup"><span data-stu-id="af5a9-183">If the **operationId** property contains the string **trigger**.</span></span>
  * <span data-ttu-id="af5a9-184">Varsa **parametreleri** özelliği içeren bir parametre ile bir **adı** özelliğini **triggerState**.</span><span class="sxs-lookup"><span data-stu-id="af5a9-184">If the **parameters** property includes a parameter with a **name** property set to **triggerState**.</span></span>
* <span data-ttu-id="af5a9-185">Tetikleyici bildirme</span><span class="sxs-lookup"><span data-stu-id="af5a9-185">Push trigger</span></span>
  * <span data-ttu-id="af5a9-186">HTTP yöntemi ise **PUT**.</span><span class="sxs-lookup"><span data-stu-id="af5a9-186">If the HTTP method is **PUT**.</span></span>
  * <span data-ttu-id="af5a9-187">Varsa **Operationıd** özelliği içeren dize **tetikleyici**.</span><span class="sxs-lookup"><span data-stu-id="af5a9-187">If the **operationId** property contains the string **trigger**.</span></span>
  * <span data-ttu-id="af5a9-188">Varsa **parametreleri** özelliği içeren bir parametre ile bir **adı** özelliğini **Tetikleyici No**.</span><span class="sxs-lookup"><span data-stu-id="af5a9-188">If the **parameters** property includes a parameter with a **name** property set to **triggerId**.</span></span>

## <a name="use-api-app-triggers-in-logic-apps"></a><span data-ttu-id="af5a9-189">Logic apps içinde API uygulaması Tetikleyicileri kullanın</span><span class="sxs-lookup"><span data-stu-id="af5a9-189">Use API app triggers in Logic apps</span></span>
### <a name="list-and-configure-api-app-triggers-in-the-logic-apps-designer"></a><span data-ttu-id="af5a9-190">Liste ve API uygulaması Tetikleyicileri Logic apps Tasarımcısı'nda yapılandırma</span><span class="sxs-lookup"><span data-stu-id="af5a9-190">List and configure API app triggers in the Logic apps designer</span></span>
<span data-ttu-id="af5a9-191">API uygulaması ile aynı kaynak grubunda bir mantıksal uygulama oluşturursanız, yalnızca tıklayarak Tasarımcı tuvaline eklemek mümkün olacaktır.</span><span class="sxs-lookup"><span data-stu-id="af5a9-191">If you create a Logic app in the same resource group as the API app, you will be able to add it to the designer canvas simply by clicking it.</span></span> <span data-ttu-id="af5a9-192">Aşağıdaki görüntüler bu gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="af5a9-192">The following images illustrate this:</span></span>

![Mantıksal Uygulama Tasarımcısı'nda tetikleyicileri](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Yoklama tetikleyici mantığı Uygulama Tasarımcısı'nda yapılandırma](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Anında iletme tetikleyici mantığı Uygulama Tasarımcısı'nda yapılandırma](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a><span data-ttu-id="af5a9-196">API uygulaması Tetikleyicileri mantıksal uygulamalar için en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="af5a9-196">Optimize API app triggers for Logic apps</span></span>
<span data-ttu-id="af5a9-197">Bir API uygulaması Tetikleyicileri ekledikten sonra API uygulaması bir mantıksal uygulama kullanırken deneyimini iyileştirmek için yapabileceğiniz birkaç işlem vardır.</span><span class="sxs-lookup"><span data-stu-id="af5a9-197">After you add triggers to an API app, there are a few things you can do to improve the experience when using the API app in a Logic app.</span></span>

<span data-ttu-id="af5a9-198">Örneğin, **triggerState** parametresi için yoklama Tetikleyicileri mantıksal uygulama aşağıdaki ifadesinde ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="af5a9-198">For instance, the **triggerState** parameter for poll triggers should be set to the following expression in the Logic app.</span></span> <span data-ttu-id="af5a9-199">Bu ifade mantıksal uygulama tetikleyiciyle son çağrılmasını değerlendirmek ve bu değer döndürmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="af5a9-199">This expression should evaluate the last invocation of the trigger from the Logic app, and return that value.</span></span>  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

<span data-ttu-id="af5a9-200">Not: Yukarıdaki ifadeyi kullanılan işlevler açıklaması için üzerinde belgelere bakın [mantığı uygulama iş akışı tanımlama dili](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span><span class="sxs-lookup"><span data-stu-id="af5a9-200">NOTE: For an explanation of the functions used in the expression above, refer to the documentation on [Logic App Workflow Definition Language](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span></span>

<span data-ttu-id="af5a9-201">Mantıksal uygulama kullanıcılarınızın yukarıda ifadesi sağlamak gerekir **triggerState** tetikleyici kullanırken parametresi.</span><span class="sxs-lookup"><span data-stu-id="af5a9-201">Logic app users would need to provide the expression above for the **triggerState** parameter while using the trigger.</span></span> <span data-ttu-id="af5a9-202">Uzantı özelliği aracılığıyla mantığı Uygulama Tasarımcısı tarafından önceden bu değeri olması mümkündür **x-ms-Zamanlayıcı-öneri**.</span><span class="sxs-lookup"><span data-stu-id="af5a9-202">It is possible to have this value preset by the Logic app designer through the extension property **x-ms-scheduler-recommendation**.</span></span>  <span data-ttu-id="af5a9-203">**X-ms-görünürlük** uzantı özelliği için bir değer ayarlanabilir *iç* böylece parametre designer'ı gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="af5a9-203">The **x-ms-visibility** extension property can be set to a value of *internal* so that the parameter itself is not shown on the designer.</span></span>  <span data-ttu-id="af5a9-204">Aşağıdaki kod parçacığında, gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="af5a9-204">The following snippet illustrates that.</span></span>

    "/api/Messages/poll": {
      "get": {
        "operationId": "Messages_NewMessageTrigger",
        "parameters": [
          {
            "name": "triggerState",
            "in": "query",
            "required": true,
            "x-ms-visibility": "internal",
            "x-ms-scheduler-recommendation": "@coalesce(triggers()?.outputs?.body?['triggerState'], '')",
            "type": "string"
          }
        ]
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    }

<span data-ttu-id="af5a9-205">Anında iletme Tetikleyicileri **Tetikleyici No** parametresi mantıksal uygulama benzersiz şekilde tanımlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="af5a9-205">For push triggers, the **triggerId** parameter must uniquely identify the Logic app.</span></span> <span data-ttu-id="af5a9-206">Aşağıdaki ifade kullanarak iş akışının adı için bu özelliği ayarlamak için önerilen en iyi yöntem değil:</span><span class="sxs-lookup"><span data-stu-id="af5a9-206">A recommended best practice is to set this property to the name of the workflow by using the following expression:</span></span>

    @workflow().name

<span data-ttu-id="af5a9-207">Kullanarak **x-ms-Zamanlayıcı-öneri** ve **x-ms-görünürlük** API uygulaması kendi API tanımı uzantısı özellikleri iletmek için bu deyim için otomatik olarak ayarlamak için mantığı Uygulama Tasarımcısı Kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="af5a9-207">Using the **x-ms-scheduler-recommendation** and **x-ms-visibility** extension properties in its API definiton, the API app can convey to the Logic app designer to automatically set this expression for the user.</span></span>

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a><span data-ttu-id="af5a9-208">API tanımı uzantısı özellikleri ekleyin</span><span class="sxs-lookup"><span data-stu-id="af5a9-208">Add extension properties in API defintion</span></span>
<span data-ttu-id="af5a9-209">-Uzantısı özellikleri gibi ek meta veri bilgileri **x-ms-Zamanlayıcı-öneri** ve **x-ms-görünürlük** -iki yoldan biriyle API tanımı eklenebilir: statik veya dinamik.</span><span class="sxs-lookup"><span data-stu-id="af5a9-209">Additional metadata information - such as the extension properties **x-ms-scheduler-recommendation** and **x-ms-visibility** - can be added in the API defintion in one of two ways: static or dynamic.</span></span>

<span data-ttu-id="af5a9-210">Statik meta verileri için doğrudan düzenleyebilirsiniz */metadata/apiDefinition.swagger.json* dosya projenizde ve özellikleri el ile ekleyin.</span><span class="sxs-lookup"><span data-stu-id="af5a9-210">For static metadata, you can directly edit the */metadata/apiDefinition.swagger.json* file in your project and add the properties manually.</span></span>

<span data-ttu-id="af5a9-211">Dinamik meta verileri kullanarak API uygulamaları için bu uzantılar ekleyebilirsiniz bir işlemi filtre eklemek için SwaggerConfig.cs dosyasını düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af5a9-211">For API apps using dynamic metadata, you can edit the SwaggerConfig.cs file to add an operation filter which can add these extensions.</span></span>

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


<span data-ttu-id="af5a9-212">Bu sınıf dinamik meta verileri senaryo kolaylaştırmak için nasıl uygulanabileceği bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="af5a9-212">The following is an example of how this class can be implemented to facilitate the dynamic metadata scenario.</span></span>

    // Add extension properties on the triggerState parameter
    public class TriggerStateFilter : IOperationFilter
    {

        public void Apply(Operation operation, SchemaRegistry schemaRegistry, System.Web.Http.Description.ApiDescription apiDescription)
        {
            if (operation.operationId.IndexOf("Trigger", StringComparison.InvariantCultureIgnoreCase) >= 0)
            {
                // this is a possible trigger
                var triggerStateParam = operation.parameters.FirstOrDefault(x => x.name.Equals("triggerState"));
                if (triggerStateParam != null)
                {
                    if (triggerStateParam.vendorExtensions == null)
                    {
                        triggerStateParam.vendorExtensions = new Dictionary<string, object>();
                    }

                    // add 2 vendor extensions
                    // x-ms-visibility: set to 'internal' to signify this is an internal field
                    // x-ms-scheduler-recommendation: set to a value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }
