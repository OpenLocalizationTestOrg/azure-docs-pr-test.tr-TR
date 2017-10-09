---
title: "Azure API Management, olay hub'ları ve Runscope API'leri aaaMonitor | Microsoft Docs"
description: "Merhaba günlük eventhub ilkeyle bağlanan Azure API Management, Azure olay hub'ları ve günlüğe kaydetme ve izleme HTTP Runscope gösteren örnek uygulama"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: c528cf6f-5f16-4a06-beea-fa1207541a47
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 7456a2436f3a2d7b815b70b65fca9481d39c5fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a><span data-ttu-id="d85c5-103">Azure API Management, olay hub'ları ve Runscope Apı'lerinizi izleme</span><span class="sxs-lookup"><span data-stu-id="d85c5-103">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>
<span data-ttu-id="d85c5-104">Merhaba [API Management hizmeti](api-management-key-concepts.md) birçok yetenekleri tooenhance hello işlenmesini HTTP gönderilen istekleri tooyour HTTP API sağlar.</span><span class="sxs-lookup"><span data-stu-id="d85c5-104">hello [API Management service](api-management-key-concepts.md) provides many capabilities tooenhance hello processing of HTTP requests sent tooyour HTTP API.</span></span> <span data-ttu-id="d85c5-105">Ancak, hello istekleri varlığını hello ve yanıtları geçicidir.</span><span class="sxs-lookup"><span data-stu-id="d85c5-105">However, hello existence of hello requests and responses are transient.</span></span> <span data-ttu-id="d85c5-106">Merhaba istek yapıldığında ve hello API Management hizmeti tooyour arka API akar.</span><span class="sxs-lookup"><span data-stu-id="d85c5-106">hello request is made and it flows through hello API Management service tooyour backend API.</span></span> <span data-ttu-id="d85c5-107">API'nizi hello isteği işler ve bir yanıtı geri toohello API tüketici akar.</span><span class="sxs-lookup"><span data-stu-id="d85c5-107">Your API processes hello request and a response flows back through toohello API consumer.</span></span> <span data-ttu-id="d85c5-108">Merhaba yayımcı portal panosunda, ancak ötesinde Hello API Management hizmeti bazı önemli istatistik hello API'leri görüntülenmek hakkında tutar, hello ayrıntıları kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="d85c5-108">hello API Management service keeps some important statistics about hello APIs for display in hello Publisher portal dashboard, but beyond that, hello details are gone.</span></span>

<span data-ttu-id="d85c5-109">Hello kullanarak [günlük eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [İlkesi](api-management-howto-policies.md) hello API Management hizmeti, herhangi bir ayrıntıyı hello istek ve yanıt tooan gönderebilirsiniz [Azure olay hub'ı](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="d85c5-109">By using hello [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [policy](api-management-howto-policies.md) in hello API Management service you can send any details from hello request and response tooan [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span> <span data-ttu-id="d85c5-110">Çeşitli nedenlerle tooyour API'leri gönderilen HTTP iletileri toogenerate olaylarından neden isteyebilirsiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="d85c5-110">There are a variety of reasons why you may want toogenerate events from HTTP messages being sent tooyour APIs.</span></span> <span data-ttu-id="d85c5-111">Denetim izi güncelleştirmeler, kullanım analizi, özel durum uyarı ve 3 taraf tümleştirmeler bazı örnekler.</span><span class="sxs-lookup"><span data-stu-id="d85c5-111">Some examples include audit trail of updates, usage analytics, exception alerting and 3rd party integrations.</span></span>   

<span data-ttu-id="d85c5-112">Bu makalede nasıl toocapture hello tüm HTTP istek ve yanıt iletisi, olay hub'ı tooan göndermek ve günlüğe kaydetme ve Hizmetleri izleme HTTP sağlar, ileti tooa üçüncü taraf hizmeti geçiş gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="d85c5-112">This article demonstrates how toocapture hello entire HTTP request and response message, send it tooan Event Hub and then relay that message tooa third party service that provides HTTP logging and monitoring services.</span></span>

## <a name="why-send-from-api-management-service"></a><span data-ttu-id="d85c5-113">API Management hizmetinden neden gönderilsin mi?</span><span class="sxs-lookup"><span data-stu-id="d85c5-113">Why Send From API Management Service?</span></span>
<span data-ttu-id="d85c5-114">Bu, HTTP API çerçeveler toocapture HTTP istekleri ve yanıtları takın ve günlüğe kaydetme ve izleme sistemleri içine akış olası toowrite HTTP Ara yazılımıdır.</span><span class="sxs-lookup"><span data-stu-id="d85c5-114">It is possible toowrite HTTP middleware that can plug into HTTP API frameworks toocapture HTTP requests and responses and feed them into logging and monitoring systems.</span></span> <span data-ttu-id="d85c5-115">Merhaba dezavantajı toothis hello HTTP Ara hello arka uç API tümleşik toobe gerekir ve hello API hello platformunu eşleşmelidir yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="d85c5-115">hello downside toothis approach is hello HTTP middleware needs toobe integrated into hello backend API and must match hello platform of hello API.</span></span> <span data-ttu-id="d85c5-116">Birden çok API'leri varsa her biri hello Ara dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d85c5-116">If there are multiple APIs then each one must deploy hello middleware.</span></span> <span data-ttu-id="d85c5-117">Genellikle arka uç API'leri neden güncelleştirilemiyor nedenleri vardır.</span><span class="sxs-lookup"><span data-stu-id="d85c5-117">Often there are reasons why backend APIs cannot be updated.</span></span>

<span data-ttu-id="d85c5-118">Günlüğe kaydetme altyapısıyla Hello Azure API Management hizmeti toointegrate kullanarak merkezi ve platformdan bağımsız bir çözüm sağlar.</span><span class="sxs-lookup"><span data-stu-id="d85c5-118">Using hello Azure API Management service toointegrate with logging infrastructure provides a centralized and platform-independent solution.</span></span> <span data-ttu-id="d85c5-119">Ayrıca ölçeklenebilir, kısmen son toohello [coğrafi çoğaltma](api-management-howto-deploy-multi-region.md) Azure API yönetimi özellikleri.</span><span class="sxs-lookup"><span data-stu-id="d85c5-119">It is also scalable, in part due toohello [geo-replication](api-management-howto-deploy-multi-region.md) capabilities of Azure API Management.</span></span>

## <a name="why-send-tooan-azure-event-hub"></a><span data-ttu-id="d85c5-120">Neden Azure olay hub'ı tooan gönderilsin mi?</span><span class="sxs-lookup"><span data-stu-id="d85c5-120">Why send tooan Azure Event Hub?</span></span>
<span data-ttu-id="d85c5-121">Makul tooask olduğundan, neden belirli tooAzure Event hubs bir ilke oluşturun?</span><span class="sxs-lookup"><span data-stu-id="d85c5-121">It is a reasonable tooask, why create a policy that is specific tooAzure Event Hubs?</span></span> <span data-ttu-id="d85c5-122">Burada toolog isteklerim istiyorum pek çok farklı yerde vardır.</span><span class="sxs-lookup"><span data-stu-id="d85c5-122">There are many different places where I might want toolog my requests.</span></span> <span data-ttu-id="d85c5-123">Neden hello doğrudan toohello son hedefi istekleri yalnızca gönderilsin mi?</span><span class="sxs-lookup"><span data-stu-id="d85c5-123">Why not just send hello requests directly toohello final destination?</span></span>  <span data-ttu-id="d85c5-124">Bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="d85c5-124">That is an option.</span></span> <span data-ttu-id="d85c5-125">Ancak, bir API management hizmeti günlük kaydı isteklerinden yaparken gerekli tooconsider olmasından günlük iletilerini hello API hello performansını nasıl etkiler.</span><span class="sxs-lookup"><span data-stu-id="d85c5-125">However, when making logging requests from an API management service, it is necessary tooconsider how logging messages will impact hello performance of hello API.</span></span> <span data-ttu-id="d85c5-126">Aşamalı yükleme artışlar sistem bileşenleri kullanılabilir örneklerini artırarak veya coğrafi çoğaltma yararlanarak işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="d85c5-126">Gradual increases in load can be handled by increasing available instances of system components or by taking advantage of geo-replication.</span></span> <span data-ttu-id="d85c5-127">Ancak, trafiğin kısa ani istekleri toologging altyapı yük altında tooslow başlatırsanız önemli ölçüde Gecikmeli istekleri toobe neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="d85c5-127">However, short spikes in traffic can cause requests toobe significantly delayed if requests toologging infrastructure start tooslow under load.</span></span>

<span data-ttu-id="d85c5-128">Hello Azure Event Hubs tasarlanmış tooingress çok büyük miktarda veriyi, olayların ne kadar daha yüksek bir sayı HTTP hello sayısından ilgilenmek için kapasiteli çoğu API işlem istekleri.</span><span class="sxs-lookup"><span data-stu-id="d85c5-128">hello Azure Event Hubs is designed tooingress huge volumes of data, with capacity for dealing with a far higher number of events than hello number of HTTP requests most APIs process.</span></span> <span data-ttu-id="d85c5-129">Merhaba olay hub'ı Gelişmiş arabellek depolamak ve hello iletileri işlemek API management hizmeti ve hello altyapınızı arasındaki bir tür olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="d85c5-129">hello Event Hub acts as a kind of sophisticated buffer between your API management service and hello infrastructure that will store and process hello messages.</span></span> <span data-ttu-id="d85c5-130">Bu API performansınızı toohello günlük altyapısı görmeyecektir sağlar.</span><span class="sxs-lookup"><span data-stu-id="d85c5-130">This ensures that your API performance will not suffer due toohello logging infrastructure.</span></span>  

<span data-ttu-id="d85c5-131">Hello veri tooan olay hub'ı geçtikten sonra kalıcıdır ve bekleyecek olay hub'ı tüketicileri tooprocess için bunu.</span><span class="sxs-lookup"><span data-stu-id="d85c5-131">Once hello data has been passed tooan Event Hub it is persisted and will wait for Event Hub consumers tooprocess it.</span></span> <span data-ttu-id="d85c5-132">Merhaba olay hub'ı nasıl işlenir ilgilenmez, yalnızca selamlama iletisine başarıyla teslim edilecek emin olmanızı hedefler cares.</span><span class="sxs-lookup"><span data-stu-id="d85c5-132">hello Event Hub does not care how it will be processed, it just cares about making sure hello message will be successfully delivered.</span></span>     

<span data-ttu-id="d85c5-133">Olay hub'ları hello özelliği toostream olayları toomultiple tüketici grupları vardır.</span><span class="sxs-lookup"><span data-stu-id="d85c5-133">Event Hubs have hello ability toostream events toomultiple consumer groups.</span></span> <span data-ttu-id="d85c5-134">Bu, tamamen farklı sistemleri tarafından işlenen olayların toobe sağlar.</span><span class="sxs-lookup"><span data-stu-id="d85c5-134">This allows events toobe processed by completely different systems.</span></span> <span data-ttu-id="d85c5-135">Bu, yalnızca bir olay oluşturulan toobe gerektiği hello hello API isteğinin hello API Management hizmeti içinde işleme ek gecikmeler koymadan birçok tümleştirme senaryolarına destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="d85c5-135">This enables supporting many integration scenarios without putting addition delays on hello processing of hello API request within hello API Management service as only one event needs toobe generated.</span></span>

## <a name="a-policy-toosend-applicationhttp-messages"></a><span data-ttu-id="d85c5-136">Bir ilke toosend uygulama/http iletileri</span><span class="sxs-lookup"><span data-stu-id="d85c5-136">A policy toosend application/http messages</span></span>
<span data-ttu-id="d85c5-137">Bir olay hub'ı olay verisi basit bir dize olarak kabul eder.</span><span class="sxs-lookup"><span data-stu-id="d85c5-137">An Event Hub accepts event data as a simple string.</span></span> <span data-ttu-id="d85c5-138">Bu dizeyi Merhaba içeriğine tooyou tamamen var.</span><span class="sxs-lookup"><span data-stu-id="d85c5-138">hello contents of that string are completely up tooyou.</span></span> <span data-ttu-id="d85c5-139">toobe mümkün toopackage bir HTTP isteği yukarı ve tooEvent tooformat hello dize hello istek veya yanıt bilgilerle ihtiyacımız hub kapalı gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d85c5-139">toobe able toopackage up an HTTP request and send it off tooEvent Hubs we need tooformat hello string with hello request or response information.</span></span> <span data-ttu-id="d85c5-140">Biz yeniden kullanabilir, varolan bir biçim ise bu gibi durumlarda, ardından biz toowrite kendi ayrıştırma kodu olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="d85c5-140">In situations like this, if there is an existing format we can reuse, then we may not have toowrite our own parsing code.</span></span> <span data-ttu-id="d85c5-141">Başlangıçta ı hello kullanarak kabul [HAR](http://www.softwareishard.com/blog/har-12-spec/) HTTP istekleri ve yanıtları göndermek için.</span><span class="sxs-lookup"><span data-stu-id="d85c5-141">Initially I considered using hello [HAR](http://www.softwareishard.com/blog/har-12-spec/) for sending HTTP requests and responses.</span></span> <span data-ttu-id="d85c5-142">Ancak, bu biçim HTTP istekleri dizisi tabanlı JSON biçiminde depolamak için optimize edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d85c5-142">However, this format is optimized for storing a sequence of HTTP requests in a JSON based format.</span></span> <span data-ttu-id="d85c5-143">Gereksiz karmaşıklık hello kablo üzerinden hello HTTP ileti geçirme hello senaryosu için eklenen zorunlu öğelerin sayısını içeriyor.</span><span class="sxs-lookup"><span data-stu-id="d85c5-143">It contained a number of mandatory elements that added unnecessary complexity for hello scenario of passing hello HTTP message over hello wire.</span></span>  

<span data-ttu-id="d85c5-144">Alternatif bir seçenek toouse hello edildi `application/http` medya türü hello HTTP belirtiminde açıklandığı gibi [RFC 7230](http://tools.ietf.org/html/rfc7230).</span><span class="sxs-lookup"><span data-stu-id="d85c5-144">An alternative option was toouse hello `application/http` media type as described in hello HTTP specification [RFC 7230](http://tools.ietf.org/html/rfc7230).</span></span> <span data-ttu-id="d85c5-145">Bu ortam türünü hello aynı diğer bir deyişle kullanılan tooactually HTTP iletileri gönderme hello kablo üzerinden biçimi, ancak hello tüm ileti hello başka bir HTTP istek gövdesinde yerleştirilebileceği tam kullanır.</span><span class="sxs-lookup"><span data-stu-id="d85c5-145">This media type uses hello exact same format that is used tooactually send HTTP messages over hello wire, but hello entire message can be put in hello body of another HTTP request.</span></span> <span data-ttu-id="d85c5-146">Örneğimizde biz yalnızca toouse hello gövde bizim ileti toosend tooEvent hub adımıdır.</span><span class="sxs-lookup"><span data-stu-id="d85c5-146">In our case we are just going toouse hello body as our message toosend tooEvent Hubs.</span></span> <span data-ttu-id="d85c5-147">Rahat, var. bir çözümleyici yok [Microsoft ASP.NET Web API 2.2 istemci](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) Bu biçim ayrıştırabilir ve hello yerel Dönüştür kitaplıkları `HttpRequestMessage` ve `HttpResponseMessage` nesneleri.</span><span class="sxs-lookup"><span data-stu-id="d85c5-147">Conveniently, there is a parser that exists in [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) libraries that can parse this format and convert it into hello native `HttpRequestMessage` and `HttpResponseMessage` objects.</span></span>

<span data-ttu-id="d85c5-148">toobe mümkün toocreate tootake avantajı, C# dayalı ihtiyacımız bu iletiyi [ilke ifadelerini](https://msdn.microsoft.com/library/azure/dn910913.aspx) Azure API Management'te.</span><span class="sxs-lookup"><span data-stu-id="d85c5-148">toobe able toocreate this message we need tootake advantage of C# based [Policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx) in Azure API Management.</span></span> <span data-ttu-id="d85c5-149">Bir HTTP istek iletisi tooAzure olay hub'ları gönderen hello İlkesi aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="d85c5-149">Here is hello policy which sends a HTTP request message tooAzure Event Hubs.</span></span>

```xml
<log-to-eventhub logger-id="conferencelogger" partition-id="0">
@{
   var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                               context.Request.Method,
                                               context.Request.Url.Path + context.Request.Url.QueryString);

   var body = context.Request.Body?.As<string>(true);
   if (body != null && body.Length > 1024)
   {
       body = body.Substring(0, 1024);
   }

   var headers = context.Request.Headers
                          .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                          .ToArray<string>();

   var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

   return "request:"   + context.Variables["message-id"] + "\n"
                       + requestLine + headerString + "\r\n" + body;
}
</log-to-eventhub>
```

### <a name="policy-declaration"></a><span data-ttu-id="d85c5-150">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="d85c5-150">Policy declaration</span></span>
<span data-ttu-id="d85c5-151">Var. Bu ilke ifadesi hakkında söz değerinde belirli birkaç.</span><span class="sxs-lookup"><span data-stu-id="d85c5-151">There a few particular things worth mentioning about this policy expression.</span></span> <span data-ttu-id="d85c5-152">Merhaba günlük eventhub İlkesi API Management hizmeti hello içinde oluşturulan Günlükçü toohello adını başvuran Günlükçü kimliği adlı bir öznitelik içeriyor.</span><span class="sxs-lookup"><span data-stu-id="d85c5-152">hello log-to-eventhub policy has an attribute called logger-id which refers toohello name of logger that has been created within hello API Management service.</span></span> <span data-ttu-id="d85c5-153">Merhaba hello belgede nasıl toosetup hello API Management hizmeti, bir olay hub'ı Günlükçü bulunabilir ayrıntılarını [nasıl toolog olayları tooAzure olay hub'ları Azure API Management'te](api-management-howto-log-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="d85c5-153">hello details of how toosetup an Event Hub logger in hello API Management service can be found in hello document [How toolog events tooAzure Event Hubs in Azure API Management](api-management-howto-log-event-hubs.md).</span></span> <span data-ttu-id="d85c5-154">Merhaba ikinci öznitelik olay hub'ları hangi bölüm toostore hello iletisinde yönlendiren isteğe bağlı bir parametredir.</span><span class="sxs-lookup"><span data-stu-id="d85c5-154">hello second attribute is an optional parameter that instructs Event Hubs which partition toostore hello message in.</span></span> <span data-ttu-id="d85c5-155">Olay hub'ları bölümleri tooenable scalabilty kullanın ve en az iki gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d85c5-155">Event Hubs use partitions tooenable scalabilty and require a minimum of two.</span></span> <span data-ttu-id="d85c5-156">iletilerin teslimini sıralı hello yalnızca bir bölüm içinde sağlanır.</span><span class="sxs-lookup"><span data-stu-id="d85c5-156">hello ordered delivery of messages is only guaranteed within a partition.</span></span> <span data-ttu-id="d85c5-157">Biz olay hub'ı hangi bölüm tooplace hello iletisinde istemeniz değil, hepsini algoritması toodistribute hello Yük kullanır.</span><span class="sxs-lookup"><span data-stu-id="d85c5-157">If we do not instruct Event Hub in which partition tooplace hello message, it will use a round-robin algorithm toodistribute hello load.</span></span> <span data-ttu-id="d85c5-158">Ancak, bazı sıralama dışında işlenen bizim iletileri toobe neden.</span><span class="sxs-lookup"><span data-stu-id="d85c5-158">However, that may cause some of our messages toobe processed out of order.</span></span>  

### <a name="partitions"></a><span data-ttu-id="d85c5-159">Bölümler</span><span class="sxs-lookup"><span data-stu-id="d85c5-159">Partitions</span></span>
<span data-ttu-id="d85c5-160">Bizim iletileri tooconsumers sırayla teslim edilir ve bölümlerinin hello yük dağıtım özellikten yararlanabilir tooensure toosend HTTP isteği iletilerini tooone bölüm ve HTTP yanıt iletilerini tooa İkinci bölüm seçtiniz.</span><span class="sxs-lookup"><span data-stu-id="d85c5-160">tooensure our messages are delivered tooconsumers in order and take advantage of hello load distribution capability of partitions, I chose toosend HTTP request messages tooone partition and HTTP response messages tooa second partition.</span></span> <span data-ttu-id="d85c5-161">Bu durum, hatta yük dağıtımı güvence altına alır ve tüm isteklerin sırada kullanılır ve tüm yanıtları sırayla tüketilebilir garanti ediyoruz.</span><span class="sxs-lookup"><span data-stu-id="d85c5-161">This will ensure an even load distribution and we can guarantee that all requests will be consumed in order and all responses will be consumed in order.</span></span> <span data-ttu-id="d85c5-162">Hello karşılık gelen isteği önce tüketilen yanıt toobe mümkündür, ancak sahibiz gibi bir sorun olmadığı ilişkilendirme için farklı bir mekanizma tooresponses ister ve istekleri her zaman yanıtları önce gelen biliyoruz.</span><span class="sxs-lookup"><span data-stu-id="d85c5-162">It is possible for a response toobe consumed before hello corresponding request, but as that is not a problem as we have a different mechanism for correlating requests tooresponses and we know that requests always come before responses.</span></span>

### <a name="http-payloads"></a><span data-ttu-id="d85c5-163">HTTP yükü</span><span class="sxs-lookup"><span data-stu-id="d85c5-163">HTTP payloads</span></span>
<span data-ttu-id="d85c5-164">Merhaba oluşturduktan sonra `requestLine` hello istek gövdesi kesiliyor biz toosee kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="d85c5-164">After building hello `requestLine` we check toosee if hello request body should be truncated.</span></span> <span data-ttu-id="d85c5-165">Merhaba istek gövdesi kesilmiş tooonly 1024 ' dir.</span><span class="sxs-lookup"><span data-stu-id="d85c5-165">hello request body is truncated tooonly 1024.</span></span> <span data-ttu-id="d85c5-166">Bu artan, ancak tek bir olay hub'ı ileti sınırlı too256KB; dolayısıyla bazı HTTP ileti tek bir iletiye sığmayacak değil gövdeleri olduğunu olasıdır.</span><span class="sxs-lookup"><span data-stu-id="d85c5-166">This could be increased, however individual Event Hub messages are limited too256KB, so it is likely that some HTTP message bodies will not fit in a single message.</span></span> <span data-ttu-id="d85c5-167">Günlüğe kaydetme ve analiz önemli miktarda bilgi yaparken yalnızca hello HTTP isteği satır ve üstbilgileri elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="d85c5-167">When doing logging and analytics a significant amount of information can be derived from just hello HTTP request line and headers.</span></span> <span data-ttu-id="d85c5-168">Ayrıca, birçok API istekleri yalnızca küçük gövdeleri dönün ve büyük gövdeleri kesilmesiyle tarafından bilgi değeri hello kaybı karşılaştırma toohello azalma aktarımı oldukça az olacak şekilde işleme ve depolama maliyetlerini tookeep tüm gövdesi içeriği.</span><span class="sxs-lookup"><span data-stu-id="d85c5-168">Also, many API requests only return small bodies and so hello loss of information value by truncating large bodies is fairly minimal in comparison toohello reduction in transfer, processing and storage costs tookeep all body contents.</span></span> <span data-ttu-id="d85c5-169">Merhaba gövdesinin işlenmesi hakkında son OneNote olduğu toopass ihtiyacımız `true` toohello olarak<string>() yönteminin hello gövdesi içeriği okumakta olduğunuz nedeni ancak, aynı zamanda istediğiniz hello arka uç API'si toobe mümkün tooread hello gövdesi.</span><span class="sxs-lookup"><span data-stu-id="d85c5-169">One final note about processing hello body is that we need toopass `true` toohello As<string>() method because we are reading hello body contents, but was also want hello backend API toobe able tooread hello body.</span></span> <span data-ttu-id="d85c5-170">TRUE toothis yöntemi geçirerek biz böylece ikinci kez okunabilecek arabellekli hello gövde toobe neden.</span><span class="sxs-lookup"><span data-stu-id="d85c5-170">By passing true toothis method we cause hello body toobe buffered so that it can be read a second time.</span></span> <span data-ttu-id="d85c5-171">Bu önemli toobe çok büyük dosyaları karşıya yükleme veya uzun yoklama kullanan bir API varsa farkında değildir.</span><span class="sxs-lookup"><span data-stu-id="d85c5-171">This is important toobe aware of if you have an API that does uploading of very large files or uses long polling.</span></span> <span data-ttu-id="d85c5-172">Bu durumlarda hello gövde hiç okuma en iyi tooavoid olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d85c5-172">In these cases it would be best tooavoid reading hello body at all.</span></span>   

### <a name="http-headers"></a><span data-ttu-id="d85c5-173">HTTP üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="d85c5-173">HTTP headers</span></span>
<span data-ttu-id="d85c5-174">HTTP üstbilgileri yalnızca üzerinden basit anahtar/değer çifti biçiminde hello ileti biçimi içine aktarılabilir.</span><span class="sxs-lookup"><span data-stu-id="d85c5-174">HTTP Headers can be simply transferred over into hello message format in a simple key/value pair format.</span></span> <span data-ttu-id="d85c5-175">Biz toostrip belirli güvenlik çıkışı gizli alanlar, kimlik bilgileri gereksiz yere sızmasını tooavoid seçtiniz.</span><span class="sxs-lookup"><span data-stu-id="d85c5-175">We have chosen toostrip out certain security sensitive fields, tooavoid unnecessarily leaking credential information.</span></span> <span data-ttu-id="d85c5-176">API anahtarları ve diğer kimlik bilgilerini analiz amaçlı kullanılacak düşüktür.</span><span class="sxs-lookup"><span data-stu-id="d85c5-176">It is unlikely that API keys and other credentials would be used for analytics purposes.</span></span> <span data-ttu-id="d85c5-177">Merhaba kullanıcı ve hello belirli ürün toodo analiz isterseniz, kullandıkları sonra biz, hello alabilir `context` nesne ve toohello ileti ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d85c5-177">If we wish toodo analysis on hello user and hello particular product they are using then we could get that from hello `context` object and add that toohello message.</span></span>     

### <a name="message-metadata"></a><span data-ttu-id="d85c5-178">İleti meta verileri</span><span class="sxs-lookup"><span data-stu-id="d85c5-178">Message Metadata</span></span>
<span data-ttu-id="d85c5-179">Merhaba tamamlandı iletisini toosend toohello olay hub'ı oluştururken hello ilk satırı hello gerçekte bir parçası değil `application/http` ileti.</span><span class="sxs-lookup"><span data-stu-id="d85c5-179">When building hello complete message toosend toohello event hub, hello first line is not actually part of hello `application/http` message.</span></span> <span data-ttu-id="d85c5-180">ek meta veri selamlama iletisine bir istek veya yanıt iletisi olup oluşan Hello ilk satırı olan ve kullanılan toocorrelate olan bir ileti kimliği tooresponses ister.</span><span class="sxs-lookup"><span data-stu-id="d85c5-180">hello first line is additional metadata consisting of whether hello message is a request or response message and a message id which is used toocorrelate requests tooresponses.</span></span> <span data-ttu-id="d85c5-181">Merhaba ileti kimliği, şuna benzer başka bir ilke kullanılarak oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="d85c5-181">hello message id is created by using another policy that looks like this:</span></span>

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

<span data-ttu-id="d85c5-182">Bir değişkende hello kadar yanıt döndürdü ve sonra yalnızca hello istek ve yanıt tek bir ileti gönderilir, depolanan hello istek iletisi oluşturduk.</span><span class="sxs-lookup"><span data-stu-id="d85c5-182">We could have created hello request message, stored that in a variable until hello response was returned and then simply sent hello request and response as a single message.</span></span> <span data-ttu-id="d85c5-183">İki ancak hello istek ve yanıt bağımsız olarak gönderme ve bir ileti kimliği toocorrelate kullanarak Merhaba, biz biraz daha fazla esneklik hello ileti boyutu, birden çok bölüm hello özelliği tootake avantajlarından ileti sırası ve hello koruyarak adımında Al İstek er bizim günlük panosunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d85c5-183">However, by sending hello request and response independently and using a message id toocorrelate hello two, we get a bit more flexibility in hello message size, hello ability tootake advantage of multiple partitions whilst maintaining message order and hello request will appear in our logging dashboard sooner.</span></span> <span data-ttu-id="d85c5-184">Ayrıca, geçerli bir yanıt hiçbir zaman toohello olay hub'ı, büyük olasılıkla hello API Management hizmeti, tooa önemli isteği hatası nedeniyle gönderilir ancak biz yine hello isteğinin bir kayda sahip olacaksınız bazı senaryolar olabilir.</span><span class="sxs-lookup"><span data-stu-id="d85c5-184">There also may be some scenarios where a valid response is never sent toohello event hub, possibly due tooa fatal request error in hello API Management service, but we still will have a record of hello request.</span></span>

<span data-ttu-id="d85c5-185">Hello İlkesi toosend hello yanıt HTTP iletisi çok benzer toohello isteği arar ve hello tamamlamak için ilke yapılandırması şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="d85c5-185">hello policy toosend hello response HTTP message looks very similar toohello request and so hello complete policy configuration looks like this:</span></span>

```xml
<policies>
  <inbound>
      <set-variable name="message-id" value="@(Guid.NewGuid())" />
      <log-to-eventhub logger-id="conferencelogger" partition-id="0">
      @{
          var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                                      context.Request.Method,
                                                      context.Request.Url.Path + context.Request.Url.QueryString);

          var body = context.Request.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Request.Headers
                               .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                               .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                               .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "request:"   + context.Variables["message-id"] + "\n"
                              + requestLine + headerString + "\r\n" + body;
      }
  </log-to-eventhub>
  </inbound>
  <backend>
      <forward-request follow-redirects="true" />
  </backend>
  <outbound>
      <log-to-eventhub logger-id="conferencelogger" partition-id="1">
      @{
          var statusLine = string.Format("HTTP/1.1 {0} {1}\r\n",
                                              context.Response.StatusCode,
                                              context.Response.StatusReason);

          var body = context.Response.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Response.Headers
                                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                                          .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "response:"  + context.Variables["message-id"] + "\n"
                              + statusLine + headerString + "\r\n" + body;
     }
  </log-to-eventhub>
  </outbound>
</policies>
```

<span data-ttu-id="d85c5-186">Merhaba `set-variable` ilkesi oluşturur hem hello tarafından erişilebilir olan bir değer `log-to-eventhub` hello ilkesinde `<inbound>` bölümü ve hello `<outbound>` bölümü.</span><span class="sxs-lookup"><span data-stu-id="d85c5-186">hello `set-variable` policy creates a value that is accessible by both hello `log-to-eventhub` policy in hello `<inbound>` section and hello `<outbound>` section.</span></span>  

## <a name="receiving-events-from-event-hubs"></a><span data-ttu-id="d85c5-187">Event Hubs'a ait alma olaylarını</span><span class="sxs-lookup"><span data-stu-id="d85c5-187">Receiving events from Event Hubs</span></span>
<span data-ttu-id="d85c5-188">Azure Event Hub olaylarından hello kullanarak alınan [AMQP protokolünü](http://www.amqp.org/).</span><span class="sxs-lookup"><span data-stu-id="d85c5-188">Events from Azure Event Hub are received using hello [AMQP protocol](http://www.amqp.org/).</span></span> <span data-ttu-id="d85c5-189">Merhaba Microsoft Service Bus ekibine, istemci kitaplıkları kullanılabilir toomake hello olayları daha kolay tüketen yapmış.</span><span class="sxs-lookup"><span data-stu-id="d85c5-189">hello Microsoft Service Bus team have made client libraries available toomake hello consuming events easier.</span></span> <span data-ttu-id="d85c5-190">Desteklenen iki farklı yaklaşım vardır, biri yükleniyor bir *doğrudan tüketici* ve hello diğer hello kullanarak `EventProcessorHost` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="d85c5-190">There are two different approaches supported, one is being a *Direct Consumer* and hello other is using hello `EventProcessorHost` class.</span></span> <span data-ttu-id="d85c5-191">Bu iki yaklaşım örnekleri hello bulunabilir [Event Hubs Programlama Kılavuzu](../event-hubs/event-hubs-programming-guide.md).</span><span class="sxs-lookup"><span data-stu-id="d85c5-191">Examples of these two approaches can be found in hello [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).</span></span> <span data-ttu-id="d85c5-192">Merhaba kısa hello farklar sürümüdür, `Direct Consumer` tam denetim ve hello sağlar `EventProcessorHost` ancak bu olayları nasıl işleyecek hakkında bazı varsayımlarda bulunur hello tesisat iş bazıları desteklemez.</span><span class="sxs-lookup"><span data-stu-id="d85c5-192">hello short version of hello differences is, `Direct Consumer` gives you complete control and hello `EventProcessorHost` does some of hello plumbing work for you but makes certain assumptions about how you will process those events.</span></span>  

### <a name="eventprocessorhost"></a><span data-ttu-id="d85c5-193">EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="d85c5-193">EventProcessorHost</span></span>
<span data-ttu-id="d85c5-194">Bu örnekte, hello kullanacağız `EventProcessorHost` kolaylık sağlamak için ancak bunu değil hello belirli bu senaryo için en iyi seçimdir.</span><span class="sxs-lookup"><span data-stu-id="d85c5-194">In this sample, we will use hello `EventProcessorHost` for simplicity, however it may not hello best choice for this particular scenario.</span></span> <span data-ttu-id="d85c5-195">`EventProcessorHost`iş parçacığı oluşturma sorunları belirli olay işlemcisi sınıfı içinde hakkında tooworry yok emin sabit iş hello.</span><span class="sxs-lookup"><span data-stu-id="d85c5-195">`EventProcessorHost` does hello hard work of making sure you don't have tooworry about threading issues within a particular event processor class.</span></span> <span data-ttu-id="d85c5-196">Ancak, Senaryomuzda, biz yalnızca hello ileti tooanother biçimine dönüştürme ve bir zaman uyumsuz yöntem kullanarak tooanother hizmet geçirme.</span><span class="sxs-lookup"><span data-stu-id="d85c5-196">However, in our scenario, we are simply converting hello message tooanother format and passing it along tooanother service using an async method.</span></span> <span data-ttu-id="d85c5-197">Paylaşılan durum ve iş parçacığı oluşturma sorunları, bu nedenle hiçbir risk güncelleştirmek için gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="d85c5-197">There is no need for updating shared state and therefore no risk of threading issues.</span></span> <span data-ttu-id="d85c5-198">Çoğu senaryo için `EventProcessorHost` büyük olasılıkla hello en iyi seçenek, kesinlikle hello daha kolay seçeneği ise.</span><span class="sxs-lookup"><span data-stu-id="d85c5-198">For most scenarios, `EventProcessorHost` is probably hello best choice and it is certainly hello easier option.</span></span>     

### <a name="ieventprocessor"></a><span data-ttu-id="d85c5-199">Ieventprocessor</span><span class="sxs-lookup"><span data-stu-id="d85c5-199">IEventProcessor</span></span>
<span data-ttu-id="d85c5-200">kullanırken hello merkezi kavram `EventProcessorHost` toocreate olan bir başlangıç uygulaması `IEventProcessor` hello yöntemi içeren arabirimi `ProcessEventAsync`.</span><span class="sxs-lookup"><span data-stu-id="d85c5-200">hello central concept when using `EventProcessorHost` is toocreate a an implementation of hello `IEventProcessor` interface which contains hello method `ProcessEventAsync`.</span></span> <span data-ttu-id="d85c5-201">Bu yöntem Hello özünü burada gösterilir:</span><span class="sxs-lookup"><span data-stu-id="d85c5-201">hello essence of that method is shown here:</span></span>

```c#
async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
{

   foreach (EventData eventData in messages)
   {
       _Logger.LogInfo(string.Format("Event received from partition: {0} - {1}", context.Lease.PartitionId,eventData.PartitionKey));

       try
       {
           var httpMessage = HttpMessage.Parse(eventData.GetBodyStream());
           await _MessageContentProcessor.ProcessHttpMessage(httpMessage);
       }
       catch (Exception ex)
       {
           _Logger.LogError(ex.Message);
       }
   }
    ... checkpointing code snipped ...
}
```

<span data-ttu-id="d85c5-202">EventData nesnelerin bir listesini hello yönteme geçirilen ve biz bu liste yineleme.</span><span class="sxs-lookup"><span data-stu-id="d85c5-202">A list of EventData objects are passed into hello method and we iterate over that list.</span></span> <span data-ttu-id="d85c5-203">Her yöntemin Hello bayt HttpMessage nesnesine Ayrıştırılan ve söz konusu nesne IHttpMessageProcessor tooan örneğini geçirilir.</span><span class="sxs-lookup"><span data-stu-id="d85c5-203">hello bytes of each method are parsed into a HttpMessage object and that object is passed tooan instance of IHttpMessageProcessor.</span></span>

### <a name="httpmessage"></a><span data-ttu-id="d85c5-204">HttpMessage</span><span class="sxs-lookup"><span data-stu-id="d85c5-204">HttpMessage</span></span>
<span data-ttu-id="d85c5-205">Merhaba `HttpMessage` örnek veri üç parçalarını içerir:</span><span class="sxs-lookup"><span data-stu-id="d85c5-205">hello `HttpMessage` instance contains three pieces of data:</span></span>

```c#
public class HttpMessage
{
   public Guid MessageId { get; set; }
   public bool IsRequest { get; set; }
   public HttpRequestMessage HttpRequestMessage { get; set; }
   public HttpResponseMessage HttpResponseMessage { get; set; }

... parsing code snipped ...

}
```

<span data-ttu-id="d85c5-206">Merhaba `HttpMessage` örneğini içeren bir `MessageId` bize toohello karşılık gelen HTTP yanıtı ve bir Boole değeri, tooconnect hello HTTP isteğinin olanak GUID tanımlayan hello nesnesi bir HttpRequestMessage örneği içeriyorsa ve Bilgisayarın HttpResponseMessage.</span><span class="sxs-lookup"><span data-stu-id="d85c5-206">hello `HttpMessage` instance contains a `MessageId` GUID that allows us tooconnect hello HTTP request toohello corresponding HTTP response and a boolean value that identifies if hello object contains an instance of a HttpRequestMessage and HttpResponseMessage.</span></span> <span data-ttu-id="d85c5-207">HTTP sınıflardan yerleşik hello kullanarak `System.Net.Http`, hello mümkün tootake avantajlarından edildi `application/http` dahil kod ayrıştırma `System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="d85c5-207">By using hello built in HTTP classes from `System.Net.Http`, I was able tootake advantage of hello `application/http` parsing code that is included in `System.Net.Http.Formatting`.</span></span>  

### <a name="ihttpmessageprocessor"></a><span data-ttu-id="d85c5-208">IHttpMessageProcessor</span><span class="sxs-lookup"><span data-stu-id="d85c5-208">IHttpMessageProcessor</span></span>
<span data-ttu-id="d85c5-209">Merhaba `HttpMessage` örneği tooimplementation, ardından iletilen `IHttpMessageProcessor` oluşturduğum toodecouple hello alma ve hello olay yorumu Azure olay hub'ı ve hello gerçek bu işleme bir arabirim olduğu.</span><span class="sxs-lookup"><span data-stu-id="d85c5-209">hello `HttpMessage` instance is then forwarded tooimplementation of `IHttpMessageProcessor` which is an interface I created toodecouple hello receiving and interpretation of hello event from Azure Event Hub and hello actual processing of it.</span></span>

## <a name="forwarding-hello-http-message"></a><span data-ttu-id="d85c5-210">Merhaba HTTP ileti iletme</span><span class="sxs-lookup"><span data-stu-id="d85c5-210">Forwarding hello HTTP message</span></span>
<span data-ttu-id="d85c5-211">Bu örnek için onu olacaktır ilginç toopush hello HTTP isteği üzerinden çok ı karar[Runscope](http://www.runscope.com).</span><span class="sxs-lookup"><span data-stu-id="d85c5-211">For this sample, I decided it would be interesting toopush hello HTTP Request over too[Runscope](http://www.runscope.com).</span></span> <span data-ttu-id="d85c5-212">Runscope hata ayıklama, günlüğe kaydetme ve izleme HTTP uzmanlaşmış bulut tabanlı bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="d85c5-212">Runscope is a cloud based service that specializes in HTTP debugging, logging and monitoring.</span></span> <span data-ttu-id="d85c5-213">Kolay tootry olduğu ve gerçek zamanlı bizim API Management hizmeti aracılığıyla akan toosee hello HTTP istek bize sağlayan ücretsiz bir katman sahiptirler.</span><span class="sxs-lookup"><span data-stu-id="d85c5-213">They have a free tier, so it is easy tootry and it allows us toosee hello HTTP requests in real-time flowing through our API Management service.</span></span>

<span data-ttu-id="d85c5-214">Merhaba `IHttpMessageProcessor` uygulaması şu şekilde görünür</span><span class="sxs-lookup"><span data-stu-id="d85c5-214">hello `IHttpMessageProcessor` implementation looks like this,</span></span>

```c#
public class RunscopeHttpMessageProcessor : IHttpMessageProcessor
{
   private HttpClient _HttpClient;
   private ILogger _Logger;
   private string _BucketKey;
   public RunscopeHttpMessageProcessor(HttpClient httpClient, ILogger logger)
   {
       _HttpClient = httpClient;
       var key = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-KEY", EnvironmentVariableTarget.User);
       _HttpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("bearer", key);
       _HttpClient.BaseAddress = new Uri("https://api.runscope.com");
       _BucketKey = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-BUCKET", EnvironmentVariableTarget.User);
       _Logger = logger;
   }

   public async Task ProcessHttpMessage(HttpMessage message)
   {
       var runscopeMessage = new RunscopeMessage()
       {
           UniqueIdentifier = message.MessageId
       };

       if (message.IsRequest)
       {
           _Logger.LogInfo("Sending HTTP request " + message.MessageId.ToString());
           runscopeMessage.Request = await RunscopeRequest.CreateFromAsync(message.HttpRequestMessage);
       }
       else
       {
           _Logger.LogInfo("Sending HTTP response " + message.MessageId.ToString());
           runscopeMessage.Response = await RunscopeResponse.CreateFromAsync(message.HttpResponseMessage);
       }

       var messagesLink = new MessagesLink() { Method = HttpMethod.Post };
       messagesLink.BucketKey = _BucketKey;
       messagesLink.RunscopeMessage = runscopeMessage;
       var runscopeResponse = await _HttpClient.SendAsync(messagesLink.CreateRequest());
       _Logger.LogDebug("Request sent tooRunscope");
   }
}
```

<span data-ttu-id="d85c5-215">Mümkün tootake avantajlarından olan bir [Runscope için var olan istemci Kitaplığı](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) , kolay toopush yapar `HttpRequestMessage` ve `HttpResponseMessage` kendi hizmetinde örnekleri ayarlama.</span><span class="sxs-lookup"><span data-stu-id="d85c5-215">I was able tootake advantage of an [existing client library for Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) that makes it easy toopush `HttpRequestMessage` and `HttpResponseMessage` instances up into their service.</span></span> <span data-ttu-id="d85c5-216">Sırayla tooaccess Runscope bir hesap ve bir API anahtarı gerekir API hello.</span><span class="sxs-lookup"><span data-stu-id="d85c5-216">In order tooaccess hello Runscope API you will need an account and an API Key.</span></span> <span data-ttu-id="d85c5-217">Bir API anahtarı alma yönergeleri hello bulunabilir [uygulamaları oluşturma tooAccess Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) ekran kaydı.</span><span class="sxs-lookup"><span data-stu-id="d85c5-217">Instructions for getting an API key can be found in hello [Creating Applications tooAccess Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.</span></span>

## <a name="complete-sample"></a><span data-ttu-id="d85c5-218">Tam örnek</span><span class="sxs-lookup"><span data-stu-id="d85c5-218">Complete sample</span></span>
<span data-ttu-id="d85c5-219">Merhaba [kaynak kodu](https://github.com/darrelmiller/ApimEventProcessor) ve testleri hello örnek için GitHub üzerinde.</span><span class="sxs-lookup"><span data-stu-id="d85c5-219">hello [source code](https://github.com/darrelmiller/ApimEventProcessor) and tests for hello sample are on GitHub.</span></span> <span data-ttu-id="d85c5-220">İhtiyacınız olacak bir [API Management hizmeti](api-management-get-started.md), [bağlı bir olay hub '](api-management-howto-log-event-hubs.md)ve bir [depolama hesabı](../storage/common/storage-create-storage-account.md) toorun hello örnek kendiniz için.</span><span class="sxs-lookup"><span data-stu-id="d85c5-220">You will need an [API Management Service](api-management-get-started.md), [a connected Event Hub](api-management-howto-log-event-hubs.md), and a [Storage Account](../storage/common/storage-create-storage-account.md) toorun hello sample for yourself.</span></span>   

<span data-ttu-id="d85c5-221">Merhaba olay Hub'ından gelen olayların dönüştürür için bunlara dinler yalnızca basit bir konsol uygulaması örnektir bir `HttpRequestMessage` ve `HttpResponseMessage` nesneleri ve bunları Runscope API toohello üzerinde iletir.</span><span class="sxs-lookup"><span data-stu-id="d85c5-221">hello sample is just a simple Console application that listens for events coming from Event Hub, converts them into a `HttpRequestMessage` and `HttpResponseMessage` objects and then forwards them on toohello Runscope API.</span></span>

<span data-ttu-id="d85c5-222">Animasyonlu resmi aşağıdaki hello tooan API hello Geliştirici Portalı, alınan, hello konsol uygulaması gösteren hello iletisi yapılan bir istek işlenen ve iletilen ve istek ve yanıt hello Runscope trafiği gösteren hello görebilirsiniz Denetleyici.</span><span class="sxs-lookup"><span data-stu-id="d85c5-222">In hello following animated image, you can see a request being made tooan API in hello Developer Portal, hello Console application showing hello message being received, processed and forwarded and then hello request and response showing up in hello Runscope Traffic inspector.</span></span>

![İstek tooRunscope iletilen Tanıtımı](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a><span data-ttu-id="d85c5-224">Özet</span><span class="sxs-lookup"><span data-stu-id="d85c5-224">Summary</span></span>
<span data-ttu-id="d85c5-225">Azure API Management hizmeti, API'lerden tooand seyahatte bir ideal yer toocapture hello HTTP trafiği sağlar.</span><span class="sxs-lookup"><span data-stu-id="d85c5-225">Azure API Management service provides an ideal place toocapture hello HTTP traffic travelling tooand from your APIs.</span></span> <span data-ttu-id="d85c5-226">Azure Event Hubs bu trafiği yakalamak için bir yüksek oranda ölçeklenebilir ve düşük maliyetli çözümdür ve günlüğe kaydetme için ikincil işleme sistemleri içine besleme, izleme ve diğer gelişmiş analiz.</span><span class="sxs-lookup"><span data-stu-id="d85c5-226">Azure Event Hubs is a highly scalable, low cost solution for capturing that traffic and feeding it into secondary processing systems for logging, monitoring and other sophisticated analytics.</span></span> <span data-ttu-id="d85c5-227">Runscope basit bir düzine birkaç kod olduğu gibi sistemleri izleme too3rd taraf trafiği bağlanılıyor.</span><span class="sxs-lookup"><span data-stu-id="d85c5-227">Connecting too3rd party traffic monitoring systems like Runscope is a simple as a few dozen lines of code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d85c5-228">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d85c5-228">Next steps</span></span>
* <span data-ttu-id="d85c5-229">Azure Event Hubs hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="d85c5-229">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="d85c5-230">Azure Event Hubs ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="d85c5-230">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="d85c5-231">EventProcessorHost bulunan iletiler alma</span><span class="sxs-lookup"><span data-stu-id="d85c5-231">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="d85c5-232">Event Hubs programlama kılavuzu</span><span class="sxs-lookup"><span data-stu-id="d85c5-232">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="d85c5-233">API Management ve Event Hubs ile tümleştirme hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="d85c5-233">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="d85c5-234">Nasıl toolog olayları tooAzure Azure API Management olay hub'ları</span><span class="sxs-lookup"><span data-stu-id="d85c5-234">How toolog events tooAzure Event Hubs in Azure API Management</span></span>](api-management-howto-log-event-hubs.md)
  * [<span data-ttu-id="d85c5-235">Günlükçü varlık başvurusu</span><span class="sxs-lookup"><span data-stu-id="d85c5-235">Logger entity reference</span></span>](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [<span data-ttu-id="d85c5-236">Günlük eventhub ilke başvurusu</span><span class="sxs-lookup"><span data-stu-id="d85c5-236">log-to-eventhub policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
