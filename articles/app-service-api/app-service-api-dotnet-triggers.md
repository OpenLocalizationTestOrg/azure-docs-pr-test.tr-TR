---
title: "aaaApp Service API uygulaması Tetikleyicileri | Microsoft Docs"
description: "Azure App Service'deki bir API uygulamasında tooimplement nasıl tetikler"
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
ms.openlocfilehash: 2d6b6a942a23c0a93987e9c48b69ecc739bfd814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-api-app-triggers"></a><span data-ttu-id="5dac2-103">Azure App Service API uygulaması tetikleyicileri</span><span class="sxs-lookup"><span data-stu-id="5dac2-103">Azure App Service API app triggers</span></span>
> [!NOTE]
> <span data-ttu-id="5dac2-104">Merhaba makalenin bu sürümü tooAPI apps 2014-12-01-Önizleme şema sürümü geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="5dac2-104">This version of hello article applies tooAPI apps 2014-12-01-preview schema version.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="5dac2-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="5dac2-105">Overview</span></span>
<span data-ttu-id="5dac2-106">Bu makalede nasıl tooimplement API uygulaması tetikler ve mantığı uygulamadan tüketen açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5dac2-106">This article explains how tooimplement API app triggers and consume them from a Logic app.</span></span>

<span data-ttu-id="5dac2-107">Bu konudaki hello kod parçacıkları tümünün hello kopyalanır [FileWatcher API uygulaması kod örneği](http://go.microsoft.com/fwlink/?LinkId=534802).</span><span class="sxs-lookup"><span data-stu-id="5dac2-107">All of hello code snippets in this topic are copied from hello [FileWatcher API App code sample](http://go.microsoft.com/fwlink/?LinkId=534802).</span></span>

<span data-ttu-id="5dac2-108">Bu makale toobuild hello kodda için nuget paketi aşağıdaki ve çalıştırma toodownload hello gerekir Not: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span><span class="sxs-lookup"><span data-stu-id="5dac2-108">Note that you'll need toodownload hello following nuget package for hello code in this article toobuild and run: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span></span>

## <a name="what-are-api-app-triggers"></a><span data-ttu-id="5dac2-109">API uygulaması Tetikleyicileri nelerdir?</span><span class="sxs-lookup"><span data-stu-id="5dac2-109">What are API app triggers?</span></span>
<span data-ttu-id="5dac2-110">Bir API uygulaması toofire bir olay için yaygın bir senaryo, böylelikle istemcilerin hello API uygulamasının yanıt toohello olayında hello uygun eylemi alabilir.</span><span class="sxs-lookup"><span data-stu-id="5dac2-110">It's a common scenario for an API app toofire an event so that clients of hello API app can take hello appropriate action in response toohello event.</span></span> <span data-ttu-id="5dac2-111">Merhaba, bu senaryoyu destekler REST API'si mekanizması bir API uygulaması Tetikleyici adı verilir.</span><span class="sxs-lookup"><span data-stu-id="5dac2-111">hello REST API based mechanism that supports this scenario is called an API app trigger.</span></span>

<span data-ttu-id="5dac2-112">Örneğin, istemci kodunuzun hello kullanarak diyelim ki [Twitter Bağlayıcısı API uygulaması](../connectors/connectors-create-api-twitter.md) ve kodunuzu bir eylem dayalı belirli sözcükleri içeren yeni tweet'leri üzerinde tooperform gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="5dac2-112">For example, let's say your client code is using hello [Twitter Connector API app](../connectors/connectors-create-api-twitter.md) and your code needs tooperform an action based on new tweets that contain specific words.</span></span> <span data-ttu-id="5dac2-113">Bu durumda, bir yoklama ya da anında iletme tetikleyici toofacilitate bu gereksinimi ayarlayabilir.</span><span class="sxs-lookup"><span data-stu-id="5dac2-113">In this case, you might set up a poll or push trigger toofacilitate this need.</span></span>

## <a name="poll-trigger-versus-push-trigger"></a><span data-ttu-id="5dac2-114">Yoklama tetikleyici itme tetikleyici karşılaştırması</span><span class="sxs-lookup"><span data-stu-id="5dac2-114">Poll trigger versus push trigger</span></span>
<span data-ttu-id="5dac2-115">İki tür tetikleyici sunucusu şu anda desteklenir:</span><span class="sxs-lookup"><span data-stu-id="5dac2-115">Currently, two types of triggers are supported:</span></span>

* <span data-ttu-id="5dac2-116">Yoklama tetikleyici - istemci hello API uygulaması harekete bir olay bildirim için yoklar.</span><span class="sxs-lookup"><span data-stu-id="5dac2-116">Poll trigger - Client polls hello API app for notification of an event having been fired</span></span>
* <span data-ttu-id="5dac2-117">Bir olay başlatıldığında itme tetikleyici - istemci hello API uygulaması tarafından bildirilir</span><span class="sxs-lookup"><span data-stu-id="5dac2-117">Push trigger - Client is notified by hello API app when an event fires</span></span>

### <a name="poll-trigger"></a><span data-ttu-id="5dac2-118">Yoklama tetikleyici</span><span class="sxs-lookup"><span data-stu-id="5dac2-118">Poll trigger</span></span>
<span data-ttu-id="5dac2-119">Yoklama tetikleyici normal bir REST API uygulanır ve kendi istemcilerinin (örneğin, bir mantıksal uygulama) toopoll bekliyor sipariş tooget bildirimi içinde.</span><span class="sxs-lookup"><span data-stu-id="5dac2-119">A poll trigger is implemented as a regular REST API and expects its clients (such as a Logic app) toopoll it in order tooget notification.</span></span> <span data-ttu-id="5dac2-120">Merhaba istemci durumunu korumak, ancak hello yoklama tetikleyici kendisini durum bilgisiz.</span><span class="sxs-lookup"><span data-stu-id="5dac2-120">While hello client may maintain state, hello poll trigger itself is stateless.</span></span>

<span data-ttu-id="5dac2-121">Karşılama istek ve yanıt paketleri ile ilgili bilgiler aşağıdaki hello hello yoklama tetikleyici sözleşme anahtar bazı yönleri gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="5dac2-121">hello following information regarding hello request and response packets illustrate some key aspects of hello poll trigger contract:</span></span>

* <span data-ttu-id="5dac2-122">İstek</span><span class="sxs-lookup"><span data-stu-id="5dac2-122">Request</span></span>
  * <span data-ttu-id="5dac2-123">HTTP yöntemini: Al</span><span class="sxs-lookup"><span data-stu-id="5dac2-123">HTTP method: GET</span></span>
  * <span data-ttu-id="5dac2-124">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5dac2-124">Parameters</span></span>
    * <span data-ttu-id="5dac2-125">triggerState - Bu isteğe bağlı parametre istemcilerinin sağlar durumlarına yoklama tetikleyici hello şekilde yapabilirsiniz düzgün toospecify karar tooreturn bildirim veya temel alınarak hello durumu belirtilen.</span><span class="sxs-lookup"><span data-stu-id="5dac2-125">triggerState - This optional parameter allows clients toospecify their state so that hello poll trigger can properly decide whether tooreturn notification or not based on hello specified state.</span></span>
    * <span data-ttu-id="5dac2-126">API özel parametreler</span><span class="sxs-lookup"><span data-stu-id="5dac2-126">API-specific parameters</span></span>
* <span data-ttu-id="5dac2-127">Yanıt</span><span class="sxs-lookup"><span data-stu-id="5dac2-127">Response</span></span>
  * <span data-ttu-id="5dac2-128">Durum kodu **200** - istek geçerli ve hello tetikleyici bildirimden yoktur.</span><span class="sxs-lookup"><span data-stu-id="5dac2-128">Status code **200** - Request is valid and there is a notification from hello trigger.</span></span> <span data-ttu-id="5dac2-129">Merhaba bildirim Merhaba içeriğine hello yanıt gövdesi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5dac2-129">hello content of hello notification will be hello response body.</span></span> <span data-ttu-id="5dac2-130">Ek bildirim verileri bir sonraki istek çağrısı ile alınması gereken bir "Yeniden deneme-sonra" üstbilgisi hello yanıt gösterir.</span><span class="sxs-lookup"><span data-stu-id="5dac2-130">A "Retry-After" header in hello response indicates that additional notification data must be retrieved with a subsequent request call.</span></span>
  * <span data-ttu-id="5dac2-131">Durum kodu **202** - istek geçerlidir, ancak hello tetikleyici öğesinden yeni bildirim yoktur.</span><span class="sxs-lookup"><span data-stu-id="5dac2-131">Status code **202** - Request is valid, but there is no new notification from hello trigger.</span></span>
  * <span data-ttu-id="5dac2-132">Durum kodu **4xx** -isteği geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="5dac2-132">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="5dac2-133">Merhaba istemci hello isteği yeniden.</span><span class="sxs-lookup"><span data-stu-id="5dac2-133">hello client should not retry hello request.</span></span>
  * <span data-ttu-id="5dac2-134">Durum kodu **5xx** -isteği bir iç sunucu hatası ve/veya geçici bir sorun içinde sonuçlandı.</span><span class="sxs-lookup"><span data-stu-id="5dac2-134">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="5dac2-135">Merhaba istemci hello isteği yeniden denemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5dac2-135">hello client should retry hello request.</span></span>

<span data-ttu-id="5dac2-136">Aşağıdaki kod parçacığını hello nasıl tooimplement bir yoklama tetikleyen bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="5dac2-136">hello following code snippet is an example of how tooimplement a poll trigger.</span></span>

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check toosee whether there is any file touched after hello timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after hello timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after hello timestamp, tell hello caller toopoll again after 1 mintue.
        else
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

<span data-ttu-id="5dac2-137">tootest bu yoklama tetiklemek, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="5dac2-137">tootest this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="5dac2-138">Merhaba API uygulaması bir kimlik doğrulama ayarı ile dağıtmak **ortak anonim**.</span><span class="sxs-lookup"><span data-stu-id="5dac2-138">Deploy hello API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="5dac2-139">Merhaba çağrısı **touch** işlemi tootouch bir dosya.</span><span class="sxs-lookup"><span data-stu-id="5dac2-139">Call hello **touch** operation tootouch a file.</span></span> <span data-ttu-id="5dac2-140">Görüntü aşağıdaki hello örnek istek Postman aracılığıyla gösterir.</span><span class="sxs-lookup"><span data-stu-id="5dac2-140">hello following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="5dac2-141">![Postman aracılığıyla dokunma işlem çağırma](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="5dac2-141">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
3. <span data-ttu-id="5dac2-142">Merhaba yoklama hello tetikleyiciyle çağrısı **triggerState** parametre tooa zaman damgası önceki tooStep #2.</span><span class="sxs-lookup"><span data-stu-id="5dac2-142">Call hello poll trigger with hello **triggerState** parameter set tooa time stamp prior tooStep #2.</span></span> <span data-ttu-id="5dac2-143">Merhaba aşağıdaki görüntüde hello örnek istek Postman aracılığıyla gösterir.</span><span class="sxs-lookup"><span data-stu-id="5dac2-143">hello following image shows hello sample request via Postman.</span></span>
   <span data-ttu-id="5dac2-144">![Postman aracılığıyla çağrı yoklama tetikleyici](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="5dac2-144">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span></span>

### <a name="push-trigger"></a><span data-ttu-id="5dac2-145">Tetikleyici bildirme</span><span class="sxs-lookup"><span data-stu-id="5dac2-145">Push trigger</span></span>
<span data-ttu-id="5dac2-146">Anında iletme tetikleyicinin belirli olay tetiklendiğinde bildirim toobe kaydolan bildirimleri tooclients iter normal bir REST API uygulanır.</span><span class="sxs-lookup"><span data-stu-id="5dac2-146">A push trigger is implemented as a regular REST API that pushes notifications tooclients who have registered toobe notified when specific events fire.</span></span>

<span data-ttu-id="5dac2-147">Karşılama istek ve yanıt paketleri ile ilgili bilgiler aşağıdaki hello hello itme tetikleyici sözleşme anahtar bazı yönleri gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="5dac2-147">hello following information regarding hello request and response packets illustrate some key aspects of hello push trigger contract.</span></span>

* <span data-ttu-id="5dac2-148">İstek</span><span class="sxs-lookup"><span data-stu-id="5dac2-148">Request</span></span>
  * <span data-ttu-id="5dac2-149">HTTP yöntemini: YERLEŞTİRME</span><span class="sxs-lookup"><span data-stu-id="5dac2-149">HTTP method: PUT</span></span>
  * <span data-ttu-id="5dac2-150">Parametreler</span><span class="sxs-lookup"><span data-stu-id="5dac2-150">Parameters</span></span>
    * <span data-ttu-id="5dac2-151">Tetikleyici No: gerekli - opak dize (GUID gibi) gösteren bir itme tetikleyici kaydını hello.</span><span class="sxs-lookup"><span data-stu-id="5dac2-151">triggerId: required - Opaque string (such as a GUID) that represents hello registration of a push trigger.</span></span>
    * <span data-ttu-id="5dac2-152">callbackUrl: gerekli - hello olay başlatıldığında hello geri çağırma tooinvoke URL'si.</span><span class="sxs-lookup"><span data-stu-id="5dac2-152">callbackUrl: required - URL of hello callback tooinvoke when hello event fires.</span></span> <span data-ttu-id="5dac2-153">Merhaba, basit bir POST HTTP çağrısıyla çağrıdır.</span><span class="sxs-lookup"><span data-stu-id="5dac2-153">hello invocation is a simple POST HTTP call.</span></span>
    * <span data-ttu-id="5dac2-154">API özel parametreler</span><span class="sxs-lookup"><span data-stu-id="5dac2-154">API-specific parameters</span></span>
* <span data-ttu-id="5dac2-155">Yanıt</span><span class="sxs-lookup"><span data-stu-id="5dac2-155">Response</span></span>
  * <span data-ttu-id="5dac2-156">Durum kodu **200** -istek tooregister istemci başarılı.</span><span class="sxs-lookup"><span data-stu-id="5dac2-156">Status code **200** - Request tooregister client successful.</span></span>
  * <span data-ttu-id="5dac2-157">Durum kodu **4xx** -isteği geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="5dac2-157">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="5dac2-158">Merhaba istemci hello isteği yeniden.</span><span class="sxs-lookup"><span data-stu-id="5dac2-158">hello client should not retry hello request.</span></span>
  * <span data-ttu-id="5dac2-159">Durum kodu **5xx** -isteği bir iç sunucu hatası ve/veya geçici bir sorun içinde sonuçlandı.</span><span class="sxs-lookup"><span data-stu-id="5dac2-159">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="5dac2-160">Merhaba istemci hello isteği yeniden denemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5dac2-160">hello client should retry hello request.</span></span>
* <span data-ttu-id="5dac2-161">Geri çağırma</span><span class="sxs-lookup"><span data-stu-id="5dac2-161">Callback</span></span>
  * <span data-ttu-id="5dac2-162">HTTP yöntemini: POST</span><span class="sxs-lookup"><span data-stu-id="5dac2-162">HTTP method: POST</span></span>
  * <span data-ttu-id="5dac2-163">İstek gövdesindeki: bildirim içeriği.</span><span class="sxs-lookup"><span data-stu-id="5dac2-163">Request body: Notification content.</span></span>

<span data-ttu-id="5dac2-164">Aşağıdaki kod parçacığını hello nasıl tooimplement push tetikleyen bir örnektir:</span><span class="sxs-lookup"><span data-stu-id="5dac2-164">hello following code snippet is an example of how tooimplement a push trigger:</span></span>

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by hello AppService service SDK.
        // Here it defines hello input of hello push trigger is a string and hello output toohello callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register hello trigger toosome trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by hello AppService service SDK indicating hello registration is completed.
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
            // Use FileSystemWatcher toolisten toofile change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire hello push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate hello FileSystemWatcher object with hello triggerId.
            _store[triggerId] = watcher;

        }

        // Fire hello assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed tooinvoke hello callback.
            Runtime runtime,
            // hello callback tooinvoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK tooinvoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

<span data-ttu-id="5dac2-165">tootest bu yoklama tetiklemek, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="5dac2-165">tootest this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="5dac2-166">Merhaba API uygulaması bir kimlik doğrulama ayarı ile dağıtmak **ortak anonim**.</span><span class="sxs-lookup"><span data-stu-id="5dac2-166">Deploy hello API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="5dac2-167">Çok Gözat[http://requestb.in/](http://requestb.in/) toocreate geri çağırma URL'si olarak davranacak bir RequestBin.</span><span class="sxs-lookup"><span data-stu-id="5dac2-167">Browse too[http://requestb.in/](http://requestb.in/) toocreate a RequestBin which will serve as your callback URL.</span></span>
3. <span data-ttu-id="5dac2-168">Merhaba itme tetikleyicisi bir GUID olarak ile çağrı **Tetikleyici No** ve RequestBin URL'si olarak hello **callbackUrl**.</span><span class="sxs-lookup"><span data-stu-id="5dac2-168">Call hello push trigger with a GUID as **triggerId** and hello RequestBin URL as **callbackUrl**.</span></span>
   <span data-ttu-id="5dac2-169">![Postman aracılığıyla gönderme tetikleyici çağırın](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="5dac2-169">![Call Push Trigger via Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span></span>
4. <span data-ttu-id="5dac2-170">Merhaba çağrısı **touch** işlemi tootouch bir dosya.</span><span class="sxs-lookup"><span data-stu-id="5dac2-170">Call hello **touch** operation tootouch a file.</span></span> <span data-ttu-id="5dac2-171">Görüntü aşağıdaki hello örnek istek Postman aracılığıyla gösterir.</span><span class="sxs-lookup"><span data-stu-id="5dac2-171">hello following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="5dac2-172">![Postman aracılığıyla dokunma işlem çağırma](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="5dac2-172">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
5. <span data-ttu-id="5dac2-173">Anında iletme tetikleyici geri çağırma hello onay hello RequestBin tooconfirm özelliği çıkışıyla çağrılır.</span><span class="sxs-lookup"><span data-stu-id="5dac2-173">Check hello RequestBin tooconfirm that hello push trigger callback is invoked with property output.</span></span>
   <span data-ttu-id="5dac2-174">![Postman aracılığıyla çağrı yoklama tetikleyici](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span><span class="sxs-lookup"><span data-stu-id="5dac2-174">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span></span>

### <a name="describe-triggers-in-api-definition"></a><span data-ttu-id="5dac2-175">API tanımı Tetikleyicileri açıklayın</span><span class="sxs-lookup"><span data-stu-id="5dac2-175">Describe triggers in API definition</span></span>
<span data-ttu-id="5dac2-176">Merhaba Tetikleyicileri uygulama ve API uygulaması tooAzure dağıtma sonra toohello gidin **API tanımı** dikey penceresinde hello Azure Önizleme portalı ve Tetikleyicileri hello tarafından yönlendirilen UI içinde otomatik olarak tanınır göreceksiniz Merhaba hello API uygulamasının Swagger 2.0 API tanımı.</span><span class="sxs-lookup"><span data-stu-id="5dac2-176">After implementing hello triggers and deploying your API app tooAzure, navigate toohello **API Definition** blade in hello Azure preview portal and you'll see that triggers are automatically recognized in hello UI, which is driven by hello Swagger 2.0 API definition of hello API app.</span></span>

![API tanımı dikey penceresi](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

<span data-ttu-id="5dac2-178">Merhaba tıklatırsanız **karşıdan Swagger** düğmesi ve açık hello JSON dosyası, aşağıdaki sonuçları benzer toohello göreceksiniz:</span><span class="sxs-lookup"><span data-stu-id="5dac2-178">If you click hello **Download Swagger** button and open hello JSON file, you'll see results similar toohello following:</span></span>

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

<span data-ttu-id="5dac2-179">Merhaba uzantı özelliği **x-ms-schedular-tetikleyici** nasıl Tetikleyicileri API tanımı'nda açıklanan olan ve hello tooone, isterse hello API tanımı hello ağ geçidi aracılığıyla istediğinde hello API uygulama ağ geçidi tarafından otomatik olarak eklenir Ölçüt aşağıdaki hello.</span><span class="sxs-lookup"><span data-stu-id="5dac2-179">hello extension property **x-ms-schedular-trigger** is how triggers are described in API definition, and is automatically added by hello API app gateway when you request hello API definition via hello gateway if hello request tooone of hello following criteria.</span></span> <span data-ttu-id="5dac2-180">(, Bu özellik el ile de ekleyebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="5dac2-180">(You can also add this property manually.)</span></span>

* <span data-ttu-id="5dac2-181">Yoklama tetikleyici</span><span class="sxs-lookup"><span data-stu-id="5dac2-181">Poll trigger</span></span>
  * <span data-ttu-id="5dac2-182">Merhaba HTTP yöntemini ise **almak**.</span><span class="sxs-lookup"><span data-stu-id="5dac2-182">If hello HTTP method is **GET**.</span></span>
  * <span data-ttu-id="5dac2-183">Merhaba, **Operationıd** özelliği içeren hello dize **tetikleyici**.</span><span class="sxs-lookup"><span data-stu-id="5dac2-183">If hello **operationId** property contains hello string **trigger**.</span></span>
  * <span data-ttu-id="5dac2-184">Merhaba, **parametreleri** özelliği içeren bir parametre ile bir **adı** çok ayarlanan özelliği**triggerState**.</span><span class="sxs-lookup"><span data-stu-id="5dac2-184">If hello **parameters** property includes a parameter with a **name** property set too**triggerState**.</span></span>
* <span data-ttu-id="5dac2-185">Tetikleyici bildirme</span><span class="sxs-lookup"><span data-stu-id="5dac2-185">Push trigger</span></span>
  * <span data-ttu-id="5dac2-186">Merhaba HTTP yöntemini ise **PUT**.</span><span class="sxs-lookup"><span data-stu-id="5dac2-186">If hello HTTP method is **PUT**.</span></span>
  * <span data-ttu-id="5dac2-187">Merhaba, **Operationıd** özelliği içeren hello dize **tetikleyici**.</span><span class="sxs-lookup"><span data-stu-id="5dac2-187">If hello **operationId** property contains hello string **trigger**.</span></span>
  * <span data-ttu-id="5dac2-188">Merhaba, **parametreleri** özelliği içeren bir parametre ile bir **adı** çok ayarlanan özelliği**Tetikleyici No**.</span><span class="sxs-lookup"><span data-stu-id="5dac2-188">If hello **parameters** property includes a parameter with a **name** property set too**triggerId**.</span></span>

## <a name="use-api-app-triggers-in-logic-apps"></a><span data-ttu-id="5dac2-189">Logic apps içinde API uygulaması Tetikleyicileri kullanın</span><span class="sxs-lookup"><span data-stu-id="5dac2-189">Use API app triggers in Logic apps</span></span>
### <a name="list-and-configure-api-app-triggers-in-hello-logic-apps-designer"></a><span data-ttu-id="5dac2-190">Liste ve API uygulaması Tetikleyicileri hello Logic apps Tasarımcısı'nda yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5dac2-190">List and configure API app triggers in hello Logic apps designer</span></span>
<span data-ttu-id="5dac2-191">Bir mantıksal uygulama hello oluşturursanız, aynı kaynak grubunda Merhaba API uygulaması, mümkün tooadd olacaktır, yalnızca tıklatarak Tasarımcı tuvaline toohello.</span><span class="sxs-lookup"><span data-stu-id="5dac2-191">If you create a Logic app in hello same resource group as hello API app, you will be able tooadd it toohello designer canvas simply by clicking it.</span></span> <span data-ttu-id="5dac2-192">görüntüleri aşağıdaki hello bu gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="5dac2-192">hello following images illustrate this:</span></span>

![Mantıksal Uygulama Tasarımcısı'nda tetikleyicileri](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Yoklama tetikleyici mantığı Uygulama Tasarımcısı'nda yapılandırma](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Anında iletme tetikleyici mantığı Uygulama Tasarımcısı'nda yapılandırma](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a><span data-ttu-id="5dac2-196">API uygulaması Tetikleyicileri mantıksal uygulamalar için en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="5dac2-196">Optimize API app triggers for Logic apps</span></span>
<span data-ttu-id="5dac2-197">Tetikleyiciler tooan API uygulama ekledikten sonra bir mantıksal uygulama hello API uygulamasını kullanırken tooimprove hello deneyimi yapabileceğiniz birkaç şey vardır.</span><span class="sxs-lookup"><span data-stu-id="5dac2-197">After you add triggers tooan API app, there are a few things you can do tooimprove hello experience when using hello API app in a Logic app.</span></span>

<span data-ttu-id="5dac2-198">Örneğin, hello **triggerState** parametresi için yoklama Tetikleyicileri hello mantıksal uygulama ifadesinde aşağıdaki toohello ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5dac2-198">For instance, hello **triggerState** parameter for poll triggers should be set toohello following expression in hello Logic app.</span></span> <span data-ttu-id="5dac2-199">Bu ifade hello son hello mantıksal uygulama hello tetikleyiciyle çalıştırılışı değerlendirmek ve bu değer döndürmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5dac2-199">This expression should evaluate hello last invocation of hello trigger from hello Logic app, and return that value.</span></span>  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

<span data-ttu-id="5dac2-200">Not: Yukarıdaki hello ifadeyi kullanılan hello işlevleri açıklaması için üzerinde toohello belgelerine başvurun [mantığı uygulama iş akışı tanımlama dili](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span><span class="sxs-lookup"><span data-stu-id="5dac2-200">NOTE: For an explanation of hello functions used in hello expression above, refer toohello documentation on [Logic App Workflow Definition Language](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span></span>

<span data-ttu-id="5dac2-201">Mantığı uygulama kullanıcıların Merhaba tooprovide hello ifade yukarıda gereksinim **triggerState** hello tetikleyici kullanırken parametresi.</span><span class="sxs-lookup"><span data-stu-id="5dac2-201">Logic app users would need tooprovide hello expression above for hello **triggerState** parameter while using hello trigger.</span></span> <span data-ttu-id="5dac2-202">Bu değer önceden olası toohave hello uzantısı özelliği aracılığıyla hello mantığı Uygulama Tasarımcısı tarafından olduğu **x-ms-Zamanlayıcı-öneri**.</span><span class="sxs-lookup"><span data-stu-id="5dac2-202">It is possible toohave this value preset by hello Logic app designer through hello extension property **x-ms-scheduler-recommendation**.</span></span>  <span data-ttu-id="5dac2-203">Merhaba **x-ms-görünürlük** uzantısı özelliği tooa değerini ayarlanabilir *iç* böylece hello parametrenin kendisinin hello designer'ı gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="5dac2-203">hello **x-ms-visibility** extension property can be set tooa value of *internal* so that hello parameter itself is not shown on hello designer.</span></span>  <span data-ttu-id="5dac2-204">Aşağıdaki kod parçacığında Merhaba, gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5dac2-204">hello following snippet illustrates that.</span></span>

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

<span data-ttu-id="5dac2-205">Anında iletme Tetikleyicileri hello **Tetikleyici No** parametresi hello mantıksal uygulama benzersiz şekilde tanımlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="5dac2-205">For push triggers, hello **triggerId** parameter must uniquely identify hello Logic app.</span></span> <span data-ttu-id="5dac2-206">Önerilen en iyi uygulama bu özellik toohello adını kullanarak hello iş akışı hello ifade aşağıdaki tooset şöyledir:</span><span class="sxs-lookup"><span data-stu-id="5dac2-206">A recommended best practice is tooset this property toohello name of hello workflow by using hello following expression:</span></span>

    @workflow().name

<span data-ttu-id="5dac2-207">Hello kullanarak **x-ms-Zamanlayıcı-öneri** ve **x-ms-görünürlük** hello API uygulaması kendi API tanımı uzantısı özellikleri iletmek toohello mantığı Uygulama Tasarımcısı tooautomatically bu ayarı Merhaba kullanıcı ifadesi.</span><span class="sxs-lookup"><span data-stu-id="5dac2-207">Using hello **x-ms-scheduler-recommendation** and **x-ms-visibility** extension properties in its API definiton, hello API app can convey toohello Logic app designer tooautomatically set this expression for hello user.</span></span>

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a><span data-ttu-id="5dac2-208">API tanımı uzantısı özellikleri ekleyin</span><span class="sxs-lookup"><span data-stu-id="5dac2-208">Add extension properties in API defintion</span></span>
<span data-ttu-id="5dac2-209">-Hello uzantısı özellikleri gibi ek meta veri bilgileri **x-ms-Zamanlayıcı-öneri** ve **x-ms-görünürlük** -iki yoldan biriyle hello API tanımı eklenebilir: statik veya dinamik.</span><span class="sxs-lookup"><span data-stu-id="5dac2-209">Additional metadata information - such as hello extension properties **x-ms-scheduler-recommendation** and **x-ms-visibility** - can be added in hello API defintion in one of two ways: static or dynamic.</span></span>

<span data-ttu-id="5dac2-210">Statik meta verilerini hello doğrudan düzenleyebilirsiniz */metadata/apiDefinition.swagger.json* dosya projenizde ve hello özellikleri el ile ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5dac2-210">For static metadata, you can directly edit hello */metadata/apiDefinition.swagger.json* file in your project and add hello properties manually.</span></span>

<span data-ttu-id="5dac2-211">Dinamik meta verileri kullanarak API uygulamaları için hello SwaggerConfig.cs dosya tooadd bu uzantılar ekleyebilirsiniz bir işlemi filtresini düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5dac2-211">For API apps using dynamic metadata, you can edit hello SwaggerConfig.cs file tooadd an operation filter which can add these extensions.</span></span>

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


<span data-ttu-id="5dac2-212">Merhaba, bu sınıf uygulanan toofacilitate hello dinamik meta verileri senaryo nasıl olabilir örneği aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="5dac2-212">hello following is an example of how this class can be implemented toofacilitate hello dynamic metadata scenario.</span></span>

    // Add extension properties on hello triggerState parameter
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
                    // x-ms-visibility: set too'internal' toosignify this is an internal field
                    // x-ms-scheduler-recommendation: set tooa value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }
