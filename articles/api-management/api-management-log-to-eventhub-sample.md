---
title: "Azure API Management, olay hub'ları ve Runscope API izleme | Microsoft Docs"
description: "Bağlanan Azure API Management, Azure olay hub'ları ve günlüğe kaydetme ve izleme HTTP Runscope günlük eventhub ilkeyle gösteren örnek uygulama"
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
ms.openlocfilehash: 70ee752c5639c90f77dde104ce85eec0a1062300
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a><span data-ttu-id="943a2-103">Azure API Management, olay hub'ları ve Runscope Apı'lerinizi izleme</span><span class="sxs-lookup"><span data-stu-id="943a2-103">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>
<span data-ttu-id="943a2-104">[API Management hizmeti](api-management-key-concepts.md) HTTP API'nizi gönderilen HTTP isteklerinin işlenmesini geliştirmek için çok sayıda özellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="943a2-104">The [API Management service](api-management-key-concepts.md) provides many capabilities to enhance the processing of HTTP requests sent to your HTTP API.</span></span> <span data-ttu-id="943a2-105">Ancak, isteklerin ve yanıtların varlığını geçici.</span><span class="sxs-lookup"><span data-stu-id="943a2-105">However, the existence of the requests and responses are transient.</span></span> <span data-ttu-id="943a2-106">İstek yapıldığında ve arka uç API'niz için API Management hizmeti aracılığıyla akar.</span><span class="sxs-lookup"><span data-stu-id="943a2-106">The request is made and it flows through the API Management service to your backend API.</span></span> <span data-ttu-id="943a2-107">API'nizi isteği işler ve bir yanıt API tüketiciye geriye doğru akar.</span><span class="sxs-lookup"><span data-stu-id="943a2-107">Your API processes the request and a response flows back through to the API consumer.</span></span> <span data-ttu-id="943a2-108">API Management hizmeti bazı önemli istatistik görüntü API'leri hakkında Publisher portal panosunda, ancak ötesine ayrıntıları kayboldu, tutar.</span><span class="sxs-lookup"><span data-stu-id="943a2-108">The API Management service keeps some important statistics about the APIs for display in the Publisher portal dashboard, but beyond that, the details are gone.</span></span>

<span data-ttu-id="943a2-109">Kullanarak [günlük eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [İlkesi](api-management-howto-policies.md) API Management hizmeti, herhangi bir ayrıntıyı istek ve yanıt olarak gönderebileceğiniz bir [Azure olay hub'ı](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="943a2-109">By using the [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [policy](api-management-howto-policies.md) in the API Management service you can send any details from the request and response to an [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span> <span data-ttu-id="943a2-110">Çeşitli nedenlerle neden HTTP iletileri için Apı'lerinizi gönderilen olaylar oluşturmak isteyebilirsiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="943a2-110">There are a variety of reasons why you may want to generate events from HTTP messages being sent to your APIs.</span></span> <span data-ttu-id="943a2-111">Denetim izi güncelleştirmeler, kullanım analizi, özel durum uyarı ve 3 taraf tümleştirmeler bazı örnekler.</span><span class="sxs-lookup"><span data-stu-id="943a2-111">Some examples include audit trail of updates, usage analytics, exception alerting and 3rd party integrations.</span></span>   

<span data-ttu-id="943a2-112">Bu makalede, tüm HTTP istek ve yanıt iletisi yakalamak, olay Hub'ına göndermek ve HTTP günlüğe kaydetme ve izleme hizmetleri sağlayan hizmet üçüncü bir tarafa ileti geçiş gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="943a2-112">This article demonstrates how to capture the entire HTTP request and response message, send it to an Event Hub and then relay that message to a third party service that provides HTTP logging and monitoring services.</span></span>

## <a name="why-send-from-api-management-service"></a><span data-ttu-id="943a2-113">API Management hizmetinden neden gönderilsin mi?</span><span class="sxs-lookup"><span data-stu-id="943a2-113">Why Send From API Management Service?</span></span>
<span data-ttu-id="943a2-114">HTTP istekleri ve yanıtları yakalamak ve günlüğe kaydetme ve izleme sistemleri içine akış için HTTP API çerçeveleri takın HTTP Ara yazmanız mümkündür.</span><span class="sxs-lookup"><span data-stu-id="943a2-114">It is possible to write HTTP middleware that can plug into HTTP API frameworks to capture HTTP requests and responses and feed them into logging and monitoring systems.</span></span> <span data-ttu-id="943a2-115">Bu yaklaşımın dezavantajı, HTTP ara yazılımı API'si arka uç tümleştirilmesi gerekir ve platform API eşleşmelidir ' dir.</span><span class="sxs-lookup"><span data-stu-id="943a2-115">The downside to this approach is the HTTP middleware needs to be integrated into the backend API and must match the platform of the API.</span></span> <span data-ttu-id="943a2-116">Birden çok API'leri varsa her bir ara yazılım dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="943a2-116">If there are multiple APIs then each one must deploy the middleware.</span></span> <span data-ttu-id="943a2-117">Genellikle arka uç API'leri neden güncelleştirilemiyor nedenleri vardır.</span><span class="sxs-lookup"><span data-stu-id="943a2-117">Often there are reasons why backend APIs cannot be updated.</span></span>

<span data-ttu-id="943a2-118">Günlüğe kaydetme altyapısı ile tümleştirmek için Azure API Management hizmeti kullanarak merkezi ve platformdan bağımsız bir çözüm sağlar.</span><span class="sxs-lookup"><span data-stu-id="943a2-118">Using the Azure API Management service to integrate with logging infrastructure provides a centralized and platform-independent solution.</span></span> <span data-ttu-id="943a2-119">Ayrıca, kısmen son biçimde ölçeklendirilebilir [coğrafi çoğaltma](api-management-howto-deploy-multi-region.md) Azure API yönetimi özellikleri.</span><span class="sxs-lookup"><span data-stu-id="943a2-119">It is also scalable, in part due to the [geo-replication](api-management-howto-deploy-multi-region.md) capabilities of Azure API Management.</span></span>

## <a name="why-send-to-an-azure-event-hub"></a><span data-ttu-id="943a2-120">Neden Azure olay Hub'ına gönderilsin mi?</span><span class="sxs-lookup"><span data-stu-id="943a2-120">Why send to an Azure Event Hub?</span></span>
<span data-ttu-id="943a2-121">Bu sorun, neden Azure Event Hubs için özel bir ilke oluşturmak makul mi?</span><span class="sxs-lookup"><span data-stu-id="943a2-121">It is a reasonable to ask, why create a policy that is specific to Azure Event Hubs?</span></span> <span data-ttu-id="943a2-122">Burada isteklerim oturum isteyebilirsiniz pek çok farklı yerde vardır.</span><span class="sxs-lookup"><span data-stu-id="943a2-122">There are many different places where I might want to log my requests.</span></span> <span data-ttu-id="943a2-123">Neden yalnızca isteklerini doğrudan son hedefe gönderilsin mi?</span><span class="sxs-lookup"><span data-stu-id="943a2-123">Why not just send the requests directly to the final destination?</span></span>  <span data-ttu-id="943a2-124">Bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="943a2-124">That is an option.</span></span> <span data-ttu-id="943a2-125">Ancak, bir API management hizmeti günlük kaydı isteklerinden yaparken günlük iletilerini API performansını nasıl etkiler dikkate alınması gereken gereklidir.</span><span class="sxs-lookup"><span data-stu-id="943a2-125">However, when making logging requests from an API management service, it is necessary to consider how logging messages will impact the performance of the API.</span></span> <span data-ttu-id="943a2-126">Aşamalı yükleme artışlar sistem bileşenleri kullanılabilir örneklerini artırarak veya coğrafi çoğaltma yararlanarak işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="943a2-126">Gradual increases in load can be handled by increasing available instances of system components or by taking advantage of geo-replication.</span></span> <span data-ttu-id="943a2-127">Ancak, kısa ani trafiğinin yük altında yavaş istekleri günlüğe kaydetme altyapısına başlatırsanız, önemli ölçüde Gecikmeli isteklerine neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="943a2-127">However, short spikes in traffic can cause requests to be significantly delayed if requests to logging infrastructure start to slow under load.</span></span>

<span data-ttu-id="943a2-128">Azure Event Hubs, HTTP çoğu API işlem isteklerinin sayısı daha için olayların ne kadar daha yüksek bir sayı ile ilgilenen kapasiteli giriş çok büyük miktarda veri için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="943a2-128">The Azure Event Hubs is designed to ingress huge volumes of data, with capacity for dealing with a far higher number of events than the number of HTTP requests most APIs process.</span></span> <span data-ttu-id="943a2-129">Olay hub'ı Gelişmiş arabellek API management hizmetiniz depolamak ve iletileri işleme altyapısı arasındaki bir tür olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="943a2-129">The Event Hub acts as a kind of sophisticated buffer between your API management service and the infrastructure that will store and process the messages.</span></span> <span data-ttu-id="943a2-130">Bu API performansınızı nedeniyle günlük altyapısı görmeyecektir sağlar.</span><span class="sxs-lookup"><span data-stu-id="943a2-130">This ensures that your API performance will not suffer due to the logging infrastructure.</span></span>  

<span data-ttu-id="943a2-131">Verileri bir olay Hub kalıcıdır ve işlemek olay hub'ı Tüketiciler için bekleyeceği geçtikten sonra.</span><span class="sxs-lookup"><span data-stu-id="943a2-131">Once the data has been passed to an Event Hub it is persisted and will wait for Event Hub consumers to process it.</span></span> <span data-ttu-id="943a2-132">Olay hub'ı nasıl işlenir ilgilenmez, yalnızca ileti başarıyla teslim emin olmanızı hedefler cares.</span><span class="sxs-lookup"><span data-stu-id="943a2-132">The Event Hub does not care how it will be processed, it just cares about making sure the message will be successfully delivered.</span></span>     

<span data-ttu-id="943a2-133">Olay hub'ları birden çok tüketici grupları akış olayları yeteneğine sahip.</span><span class="sxs-lookup"><span data-stu-id="943a2-133">Event Hubs have the ability to stream events to multiple consumer groups.</span></span> <span data-ttu-id="943a2-134">Bu, tamamen farklı sistemleri tarafından işlenecek olayların sağlar.</span><span class="sxs-lookup"><span data-stu-id="943a2-134">This allows events to be processed by completely different systems.</span></span> <span data-ttu-id="943a2-135">Bu, yalnızca bir olay oluşturulması gereken şekilde ek gecikmeler API Management hizmeti içinde API isteğinin işlenmesi üzerinde koymadan birçok tümleştirme senaryolarına destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="943a2-135">This enables supporting many integration scenarios without putting addition delays on the processing of the API request within the API Management service as only one event needs to be generated.</span></span>

## <a name="a-policy-to-send-applicationhttp-messages"></a><span data-ttu-id="943a2-136">Uygulama/http iletileri göndermek için bir ilke</span><span class="sxs-lookup"><span data-stu-id="943a2-136">A policy to send application/http messages</span></span>
<span data-ttu-id="943a2-137">Bir olay hub'ı olay verisi basit bir dize olarak kabul eder.</span><span class="sxs-lookup"><span data-stu-id="943a2-137">An Event Hub accepts event data as a simple string.</span></span> <span data-ttu-id="943a2-138">Bu dizeyi içeriğini tamamen size bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="943a2-138">The contents of that string are completely up to you.</span></span> <span data-ttu-id="943a2-139">Bir HTTP isteğini oluşturan paketini ve Event Hubs'a gönderme için kimliğinizi biçim dizesi istek veya yanıt bilgilerle gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="943a2-139">To be able to package up an HTTP request and send it off to Event Hubs we need to format the string with the request or response information.</span></span> <span data-ttu-id="943a2-140">Bu gibi durumlarda varolan bir biçim ise yeniden kullanabilirsiniz, sonra biz kendi kod ayrıştırma yazmak olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="943a2-140">In situations like this, if there is an existing format we can reuse, then we may not have to write our own parsing code.</span></span> <span data-ttu-id="943a2-141">Başlangıçta t kullanarak kabul [HAR](http://www.softwareishard.com/blog/har-12-spec/) HTTP istekleri ve yanıtları göndermek için.</span><span class="sxs-lookup"><span data-stu-id="943a2-141">Initially I considered using the [HAR](http://www.softwareishard.com/blog/har-12-spec/) for sending HTTP requests and responses.</span></span> <span data-ttu-id="943a2-142">Ancak, bu biçim HTTP istekleri dizisi tabanlı JSON biçiminde depolamak için optimize edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="943a2-142">However, this format is optimized for storing a sequence of HTTP requests in a JSON based format.</span></span> <span data-ttu-id="943a2-143">Kablo üzerinden HTTP ileti iletme senaryosu için gereksiz karmaşıklık eklenen zorunlu öğelerin sayısını içeriyor.</span><span class="sxs-lookup"><span data-stu-id="943a2-143">It contained a number of mandatory elements that added unnecessary complexity for the scenario of passing the HTTP message over the wire.</span></span>  

<span data-ttu-id="943a2-144">Alternatif bir seçenek kullanılmasıydır `application/http` medya türü HTTP belirtiminde açıklandığı gibi [RFC 7230](http://tools.ietf.org/html/rfc7230).</span><span class="sxs-lookup"><span data-stu-id="943a2-144">An alternative option was to use the `application/http` media type as described in the HTTP specification [RFC 7230](http://tools.ietf.org/html/rfc7230).</span></span> <span data-ttu-id="943a2-145">Bu ortam türünü gerçekte HTTP ileti kablo üzerinden göndermek için kullanılan tam aynı biçimi kullanır, ancak tüm ileti başka bir HTTP istek gövdesinde put olabilir.</span><span class="sxs-lookup"><span data-stu-id="943a2-145">This media type uses the exact same format that is used to actually send HTTP messages over the wire, but the entire message can be put in the body of another HTTP request.</span></span> <span data-ttu-id="943a2-146">Örneğimizde biz yalnızca gövde bizim iletisi olarak Event Hubs'a göndermek için kullanacağınız.</span><span class="sxs-lookup"><span data-stu-id="943a2-146">In our case we are just going to use the body as our message to send to Event Hubs.</span></span> <span data-ttu-id="943a2-147">Rahat, var. bir çözümleyici yok [Microsoft ASP.NET Web API 2.2 istemci](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) Bu biçim ayrıştırabilir ve yerel Dönüştür kitaplıkları `HttpRequestMessage` ve `HttpResponseMessage` nesneleri.</span><span class="sxs-lookup"><span data-stu-id="943a2-147">Conveniently, there is a parser that exists in [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) libraries that can parse this format and convert it into the native `HttpRequestMessage` and `HttpResponseMessage` objects.</span></span>

<span data-ttu-id="943a2-148">C# dayalı yararlanmak ihtiyacımız bu iletiyi oluşturmak için [ilke ifadelerini](https://msdn.microsoft.com/library/azure/dn910913.aspx) Azure API Management'te.</span><span class="sxs-lookup"><span data-stu-id="943a2-148">To be able to create this message we need to take advantage of C# based [Policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx) in Azure API Management.</span></span> <span data-ttu-id="943a2-149">Azure Event Hubs'a bir HTTP istek iletisini gönderen İlkesi aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="943a2-149">Here is the policy which sends a HTTP request message to Azure Event Hubs.</span></span>

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

### <a name="policy-declaration"></a><span data-ttu-id="943a2-150">İlke bildirimi</span><span class="sxs-lookup"><span data-stu-id="943a2-150">Policy declaration</span></span>
<span data-ttu-id="943a2-151">Var. Bu ilke ifadesi hakkında söz değerinde belirli birkaç.</span><span class="sxs-lookup"><span data-stu-id="943a2-151">There a few particular things worth mentioning about this policy expression.</span></span> <span data-ttu-id="943a2-152">Günlük eventhub İlkesi API Management hizmet içinde oluşturulan Günlükçü adına başvuran Günlükçü kimliği adlı bir öznitelik içeriyor.</span><span class="sxs-lookup"><span data-stu-id="943a2-152">The log-to-eventhub policy has an attribute called logger-id which refers to the name of logger that has been created within the API Management service.</span></span> <span data-ttu-id="943a2-153">Bir olay hub'ı Günlükçü API Management hizmet Kurulum nasıl ayrıntılarını belgesinde bulunabilir [Azure Event hubs'a Azure API Management olaylarını günlüğe kaydedecek şekilde nasıl](api-management-howto-log-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="943a2-153">The details of how to setup an Event Hub logger in the API Management service can be found in the document [How to log events to Azure Event Hubs in Azure API Management](api-management-howto-log-event-hubs.md).</span></span> <span data-ttu-id="943a2-154">İkinci öznitelik, iletide depolamak için bölüm Event Hubs yönlendiren isteğe bağlı bir parametredir.</span><span class="sxs-lookup"><span data-stu-id="943a2-154">The second attribute is an optional parameter that instructs Event Hubs which partition to store the message in.</span></span> <span data-ttu-id="943a2-155">Olay hub'ları, en az iki gerekli ve scalabilty için bölümleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="943a2-155">Event Hubs use partitions to enable scalabilty and require a minimum of two.</span></span> <span data-ttu-id="943a2-156">İletilerin sıralı teslimini yalnızca bir bölüm içinde sağlanır.</span><span class="sxs-lookup"><span data-stu-id="943a2-156">The ordered delivery of messages is only guaranteed within a partition.</span></span> <span data-ttu-id="943a2-157">Biz olay hub'ı ileti yerleştirmek için hangi bölümünde istemeniz değil, yükü dağıtmak için hepsini algoritması kullanır.</span><span class="sxs-lookup"><span data-stu-id="943a2-157">If we do not instruct Event Hub in which partition to place the message, it will use a round-robin algorithm to distribute the load.</span></span> <span data-ttu-id="943a2-158">Ancak, bazı bozuk işlenecek bizim iletilerinin neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="943a2-158">However, that may cause some of our messages to be processed out of order.</span></span>  

### <a name="partitions"></a><span data-ttu-id="943a2-159">Bölümler</span><span class="sxs-lookup"><span data-stu-id="943a2-159">Partitions</span></span>
<span data-ttu-id="943a2-160">Bizim iletileri tüketiciye sırayla teslim edilir ve bölümlerinin yük dağıtım özellikten yararlanabilir emin olmak için bir bölüm ve HTTP yanıt iletilerini ikinci bir bölüm için HTTP isteği iletilerini göndermek seçtiğim.</span><span class="sxs-lookup"><span data-stu-id="943a2-160">To ensure our messages are delivered to consumers in order and take advantage of the load distribution capability of partitions, I chose to send HTTP request messages to one partition and HTTP response messages to a second partition.</span></span> <span data-ttu-id="943a2-161">Bu durum, hatta yük dağıtımı güvence altına alır ve tüm isteklerin sırada kullanılır ve tüm yanıtları sırayla tüketilebilir garanti ediyoruz.</span><span class="sxs-lookup"><span data-stu-id="943a2-161">This will ensure an even load distribution and we can guarantee that all requests will be consumed in order and all responses will be consumed in order.</span></span> <span data-ttu-id="943a2-162">Karşılık gelen isteği önce kullanılması için bir yanıt mümkündür, ancak sahibiz gibi bir sorun olmadığı yanıtları ilişkilendirme için farklı bir mekanizma ister ve istekleri her zaman yanıtları önce gelen biliyoruz.</span><span class="sxs-lookup"><span data-stu-id="943a2-162">It is possible for a response to be consumed before the corresponding request, but as that is not a problem as we have a different mechanism for correlating requests to responses and we know that requests always come before responses.</span></span>

### <a name="http-payloads"></a><span data-ttu-id="943a2-163">HTTP yükü</span><span class="sxs-lookup"><span data-stu-id="943a2-163">HTTP payloads</span></span>
<span data-ttu-id="943a2-164">Yapı sonra `requestLine` biz istek gövdesi kesilmiş denetleyin.</span><span class="sxs-lookup"><span data-stu-id="943a2-164">After building the `requestLine` we check to see if the request body should be truncated.</span></span> <span data-ttu-id="943a2-165">İstek gövdesi için yalnızca 1024 kesilir.</span><span class="sxs-lookup"><span data-stu-id="943a2-165">The request body is truncated to only 1024.</span></span> <span data-ttu-id="943a2-166">Tek bir olay hub'ı ileti 256 KB ile sınırlı ancak bu, artırılacak bazı HTTP iletisi tek iletiye sığmayacak değil gövdeleri, büyük olasılıkla gelir.</span><span class="sxs-lookup"><span data-stu-id="943a2-166">This could be increased, however individual Event Hub messages are limited to 256KB, so it is likely that some HTTP message bodies will not fit in a single message.</span></span> <span data-ttu-id="943a2-167">Günlüğe kaydetme ve analiz yaparken önemli miktarda bilgi yalnızca HTTP isteği çizgi ve üst bilgileri elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="943a2-167">When doing logging and analytics a significant amount of information can be derived from just the HTTP request line and headers.</span></span> <span data-ttu-id="943a2-168">Ayrıca, birçok API istekleri yalnızca küçük gövdeleri dönün ve böylece büyük gövdeleri kesilmesiyle tarafından bilgi değeri kaybı oldukça tüm gövdesi içeriği korumak için Aktarım, işleme ve depolama maliyetlerini azaltma kıyasla en alt düzeydedir.</span><span class="sxs-lookup"><span data-stu-id="943a2-168">Also, many API requests only return small bodies and so the loss of information value by truncating large bodies is fairly minimal in comparison to the reduction in transfer, processing and storage costs to keep all body contents.</span></span> <span data-ttu-id="943a2-169">Gövde işleme hakkında son OneNote olduğu geçirmek ihtiyacımız `true` AS<string>() yönteminin gövdesi içeriği okumakta olduğunuz nedeni ancak, aynı zamanda arka uç gövdesi okuyabilir API istiyor.</span><span class="sxs-lookup"><span data-stu-id="943a2-169">One final note about processing the body is that we need to pass `true` to the As<string>() method because we are reading the body contents, but was also want the backend API to be able to read the body.</span></span> <span data-ttu-id="943a2-170">Bu yöntem true geçirerek biz böylece ikinci kez okunabilecek arabellekli için gövdesini neden.</span><span class="sxs-lookup"><span data-stu-id="943a2-170">By passing true to this method we cause the body to be buffered so that it can be read a second time.</span></span> <span data-ttu-id="943a2-171">Bu çok büyük dosyaları karşıya yükleme veya uzun yoklama kullanan bir API varsa bilincinde olmak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="943a2-171">This is important to be aware of if you have an API that does uploading of very large files or uses long polling.</span></span> <span data-ttu-id="943a2-172">Bu durumlarda gövde hiç okuma önlemek en iyi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="943a2-172">In these cases it would be best to avoid reading the body at all.</span></span>   

### <a name="http-headers"></a><span data-ttu-id="943a2-173">HTTP üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="943a2-173">HTTP headers</span></span>
<span data-ttu-id="943a2-174">HTTP üstbilgileri yalnızca üzerinden basit anahtar/değer çifti biçiminde ileti biçimi içine aktarılabilir.</span><span class="sxs-lookup"><span data-stu-id="943a2-174">HTTP Headers can be simply transferred over into the message format in a simple key/value pair format.</span></span> <span data-ttu-id="943a2-175">Kimlik bilgileri gereksiz yere sızmasını önlemek için belirli güvenlik duyarlı alanları, Şerit seçtiniz.</span><span class="sxs-lookup"><span data-stu-id="943a2-175">We have chosen to strip out certain security sensitive fields, to avoid unnecessarily leaking credential information.</span></span> <span data-ttu-id="943a2-176">API anahtarları ve diğer kimlik bilgilerini analiz amaçlı kullanılacak düşüktür.</span><span class="sxs-lookup"><span data-stu-id="943a2-176">It is unlikely that API keys and other credentials would be used for analytics purposes.</span></span> <span data-ttu-id="943a2-177">Biz kullanıcı ve belirli ürün çözümleme yapmak isterseniz, kullandıkları sonra biz değerinden alabilir `context` nesne ve iletiye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="943a2-177">If we wish to do analysis on the user and the particular product they are using then we could get that from the `context` object and add that to the message.</span></span>     

### <a name="message-metadata"></a><span data-ttu-id="943a2-178">İleti meta verileri</span><span class="sxs-lookup"><span data-stu-id="943a2-178">Message Metadata</span></span>
<span data-ttu-id="943a2-179">Olay hub'ına göndermek için tam iletiyi oluştururken, ilk satırı değil gerçekte parçası `application/http` ileti.</span><span class="sxs-lookup"><span data-stu-id="943a2-179">When building the complete message to send to the event hub, the first line is not actually part of the `application/http` message.</span></span> <span data-ttu-id="943a2-180">İlk satırı ileti bir istek veya yanıt iletisi ve yanıtları isteklerine ilişkilendirmek için kullanılan bir ileti kimliği olduğundan oluşan ek meta verilerdir.</span><span class="sxs-lookup"><span data-stu-id="943a2-180">The first line is additional metadata consisting of whether the message is a request or response message and a message id which is used to correlate requests to responses.</span></span> <span data-ttu-id="943a2-181">İleti kimliği, şuna benzer başka bir ilke kullanılarak oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="943a2-181">The message id is created by using another policy that looks like this:</span></span>

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

<span data-ttu-id="943a2-182">Biz istek iletisi oluşturulan, bir değişkende depolanan kadar yanıtta döndürülen ve sonra yalnızca istek ve yanıt tek bir ileti gönderilir.</span><span class="sxs-lookup"><span data-stu-id="943a2-182">We could have created the request message, stored that in a variable until the response was returned and then simply sent the request and response as a single message.</span></span> <span data-ttu-id="943a2-183">Ancak, istek ve yanıt bağımsız olarak gönderme ve iki ilişkilendirmek için bir ileti kimliği kullanılarak, biz biraz daha fazla esneklik ileti boyutu, ileti sırası ve istek koruyarak görünür yaparken birden çok bölüm yararlanmak olanağı Al Bizim günlük panosunda daha erken.</span><span class="sxs-lookup"><span data-stu-id="943a2-183">However, by sending the request and response independently and using a message id to correlate the two, we get a bit more flexibility in the message size, the ability to take advantage of multiple partitions whilst maintaining message order and the request will appear in our logging dashboard sooner.</span></span> <span data-ttu-id="943a2-184">Ayrıca burada geçerli bir yanıt hiçbir zaman muhtemelen bir API Management hizmeti önemli isteği hatası nedeniyle olay hub'ına gönderilen ancak biz yine isteğin bir kayda sahip olacaksınız bazı senaryolar olabilir.</span><span class="sxs-lookup"><span data-stu-id="943a2-184">There also may be some scenarios where a valid response is never sent to the event hub, possibly due to a fatal request error in the API Management service, but we still will have a record of the request.</span></span>

<span data-ttu-id="943a2-185">Yanıt HTTP iletisi göndermek için ilke isteği çok benzer ve bu nedenle tam ilke yapılandırması şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="943a2-185">The policy to send the response HTTP message looks very similar to the request and so the complete policy configuration looks like this:</span></span>

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

<span data-ttu-id="943a2-186">`set-variable` İlke, her ikisi için de erişilebilir olan bir değer oluşturur `log-to-eventhub` ilkesinde `<inbound>` bölüm ve `<outbound>` bölümü.</span><span class="sxs-lookup"><span data-stu-id="943a2-186">The `set-variable` policy creates a value that is accessible by both the `log-to-eventhub` policy in the `<inbound>` section and the `<outbound>` section.</span></span>  

## <a name="receiving-events-from-event-hubs"></a><span data-ttu-id="943a2-187">Event Hubs'a ait alma olaylarını</span><span class="sxs-lookup"><span data-stu-id="943a2-187">Receiving events from Event Hubs</span></span>
<span data-ttu-id="943a2-188">Azure Event Hub olaylarından kullanarak alınan [AMQP protokolünü](http://www.amqp.org/).</span><span class="sxs-lookup"><span data-stu-id="943a2-188">Events from Azure Event Hub are received using the [AMQP protocol](http://www.amqp.org/).</span></span> <span data-ttu-id="943a2-189">Microsoft Service Bus ekibine istemci kitaplıkları Süren olayları kolaylaştırmak kullanılabilir yaptınız.</span><span class="sxs-lookup"><span data-stu-id="943a2-189">The Microsoft Service Bus team have made client libraries available to make the consuming events easier.</span></span> <span data-ttu-id="943a2-190">Desteklenen iki farklı yaklaşım vardır, biri yükleniyor bir *doğrudan tüketici* ve diğer kullanarak `EventProcessorHost` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="943a2-190">There are two different approaches supported, one is being a *Direct Consumer* and the other is using the `EventProcessorHost` class.</span></span> <span data-ttu-id="943a2-191">Bu iki yaklaşım örnekleri bulunabilir [Event Hubs Programlama Kılavuzu](../event-hubs/event-hubs-programming-guide.md).</span><span class="sxs-lookup"><span data-stu-id="943a2-191">Examples of these two approaches can be found in the [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).</span></span> <span data-ttu-id="943a2-192">Kısa farklar sürümüdür, `Direct Consumer` tam denetim verir ve `EventProcessorHost` ancak bu olayları nasıl işleyecek hakkında bazı varsayımlarda bulunur tesisat iş bazıları desteklemez.</span><span class="sxs-lookup"><span data-stu-id="943a2-192">The short version of the differences is, `Direct Consumer` gives you complete control and the `EventProcessorHost` does some of the plumbing work for you but makes certain assumptions about how you will process those events.</span></span>  

### <a name="eventprocessorhost"></a><span data-ttu-id="943a2-193">EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="943a2-193">EventProcessorHost</span></span>
<span data-ttu-id="943a2-194">Bu örnekte, kullanacağız `EventProcessorHost` kolaylık sağlamak için ancak bunu olabilir en iyi seçenek belirli bu senaryo için değil.</span><span class="sxs-lookup"><span data-stu-id="943a2-194">In this sample, we will use the `EventProcessorHost` for simplicity, however it may not the best choice for this particular scenario.</span></span> <span data-ttu-id="943a2-195">`EventProcessorHost`iş parçacığı oluşturma sorunları belirli olay işlemcisi sınıfı içinde hakkında endişelenmeniz gerekmez emin olmak zor bir iş yapar.</span><span class="sxs-lookup"><span data-stu-id="943a2-195">`EventProcessorHost` does the hard work of making sure you don't have to worry about threading issues within a particular event processor class.</span></span> <span data-ttu-id="943a2-196">Ancak, Senaryomuzda biz yalnızca ileti başka bir biçime dönüştürme ve onu boyunca bir zaman uyumsuz yöntem kullanarak başka bir hizmete geçirmeden.</span><span class="sxs-lookup"><span data-stu-id="943a2-196">However, in our scenario, we are simply converting the message to another format and passing it along to another service using an async method.</span></span> <span data-ttu-id="943a2-197">Paylaşılan durum ve iş parçacığı oluşturma sorunları, bu nedenle hiçbir risk güncelleştirmek için gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="943a2-197">There is no need for updating shared state and therefore no risk of threading issues.</span></span> <span data-ttu-id="943a2-198">Çoğu senaryo için `EventProcessorHost` büyük olasılıkla en iyi seçenek, kesinlikle daha kolay seçeneği ise.</span><span class="sxs-lookup"><span data-stu-id="943a2-198">For most scenarios, `EventProcessorHost` is probably the best choice and it is certainly the easier option.</span></span>     

### <a name="ieventprocessor"></a><span data-ttu-id="943a2-199">Ieventprocessor</span><span class="sxs-lookup"><span data-stu-id="943a2-199">IEventProcessor</span></span>
<span data-ttu-id="943a2-200">Kullanırken merkezi kavram `EventProcessorHost` oluşturmaktır bir uygulaması `IEventProcessor` yöntemi içeren arabirimi `ProcessEventAsync`.</span><span class="sxs-lookup"><span data-stu-id="943a2-200">The central concept when using `EventProcessorHost` is to create a an implementation of the `IEventProcessor` interface which contains the method `ProcessEventAsync`.</span></span> <span data-ttu-id="943a2-201">Bu yöntem özünü burada gösterilir:</span><span class="sxs-lookup"><span data-stu-id="943a2-201">The essence of that method is shown here:</span></span>

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

<span data-ttu-id="943a2-202">EventData nesnelerin bir listesini, yönteme geçirilir ve biz bu liste yineleme.</span><span class="sxs-lookup"><span data-stu-id="943a2-202">A list of EventData objects are passed into the method and we iterate over that list.</span></span> <span data-ttu-id="943a2-203">Her yöntem bayt HttpMessage nesnesine Ayrıştırılan ve söz konusu nesne IHttpMessageProcessor örneğine geçirilir.</span><span class="sxs-lookup"><span data-stu-id="943a2-203">The bytes of each method are parsed into a HttpMessage object and that object is passed to an instance of IHttpMessageProcessor.</span></span>

### <a name="httpmessage"></a><span data-ttu-id="943a2-204">HttpMessage</span><span class="sxs-lookup"><span data-stu-id="943a2-204">HttpMessage</span></span>
<span data-ttu-id="943a2-205">`HttpMessage` Örnek veri üç parçalarını içerir:</span><span class="sxs-lookup"><span data-stu-id="943a2-205">The `HttpMessage` instance contains three pieces of data:</span></span>

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

<span data-ttu-id="943a2-206">`HttpMessage` Örneğini içeren bir `MessageId` bize karşılık gelen HTTP yanıtı ve nesne örneğini bir HttpRequestMessage ve httpresponsemessage öğesini içeriyorsa tanımlayan bir Boole değeri HTTP isteği bağlanmasını sağlayan GUID.</span><span class="sxs-lookup"><span data-stu-id="943a2-206">The `HttpMessage` instance contains a `MessageId` GUID that allows us to connect the HTTP request to the corresponding HTTP response and a boolean value that identifies if the object contains an instance of a HttpRequestMessage and HttpResponseMessage.</span></span> <span data-ttu-id="943a2-207">HTTP sınıflardan yerleşik kullanılarak `System.Net.Http`, ı yararlanmak kurtararak `application/http` dahil kod ayrıştırma `System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="943a2-207">By using the built in HTTP classes from `System.Net.Http`, I was able to take advantage of the `application/http` parsing code that is included in `System.Net.Http.Formatting`.</span></span>  

### <a name="ihttpmessageprocessor"></a><span data-ttu-id="943a2-208">IHttpMessageProcessor</span><span class="sxs-lookup"><span data-stu-id="943a2-208">IHttpMessageProcessor</span></span>
<span data-ttu-id="943a2-209">`HttpMessage` Örnek uygulaması için sonra iletilen `IHttpMessageProcessor` oluşturduğum alma ve Azure olay hub'ı olayından yorumu ve gerçek işlenmesini aynı şekilde bir arabirim olduğu.</span><span class="sxs-lookup"><span data-stu-id="943a2-209">The `HttpMessage` instance is then forwarded to implementation of `IHttpMessageProcessor` which is an interface I created to decouple the receiving and interpretation of the event from Azure Event Hub and the actual processing of it.</span></span>

## <a name="forwarding-the-http-message"></a><span data-ttu-id="943a2-210">HTTP ileti iletme</span><span class="sxs-lookup"><span data-stu-id="943a2-210">Forwarding the HTTP message</span></span>
<span data-ttu-id="943a2-211">Bu örnek için onu olacaktır için üzerinden HTTP isteği göndermek ilginç ı karar [Runscope](http://www.runscope.com).</span><span class="sxs-lookup"><span data-stu-id="943a2-211">For this sample, I decided it would be interesting to push the HTTP Request over to [Runscope](http://www.runscope.com).</span></span> <span data-ttu-id="943a2-212">Runscope hata ayıklama, günlüğe kaydetme ve izleme HTTP uzmanlaşmış bulut tabanlı bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="943a2-212">Runscope is a cloud based service that specializes in HTTP debugging, logging and monitoring.</span></span> <span data-ttu-id="943a2-213">Deneyin kolaydır ve gerçek zamanlı bizim API Management hizmeti aracılığıyla akan HTTP istek bkz kurmamızı sağlayan ücretsiz bir katman sahiptirler.</span><span class="sxs-lookup"><span data-stu-id="943a2-213">They have a free tier, so it is easy to try and it allows us to see the HTTP requests in real-time flowing through our API Management service.</span></span>

<span data-ttu-id="943a2-214">`IHttpMessageProcessor` Uygulaması şu şekilde görünür</span><span class="sxs-lookup"><span data-stu-id="943a2-214">The `IHttpMessageProcessor` implementation looks like this,</span></span>

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
       _Logger.LogDebug("Request sent to Runscope");
   }
}
```

<span data-ttu-id="943a2-215">I yararlanmak için bir [Runscope için var olan istemci Kitaplığı](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) , anında iletme kolaylaştırır `HttpRequestMessage` ve `HttpResponseMessage` kendi hizmetinde örnekleri ayarlama.</span><span class="sxs-lookup"><span data-stu-id="943a2-215">I was able to take advantage of an [existing client library for Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) that makes it easy to push `HttpRequestMessage` and `HttpResponseMessage` instances up into their service.</span></span> <span data-ttu-id="943a2-216">Runscope API erişmek için bir hesap ve bir API anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="943a2-216">In order to access the Runscope API you will need an account and an API Key.</span></span> <span data-ttu-id="943a2-217">Bir API anahtarı alma yönergeleri bulunabilir [erişim Runscope API uygulamaları oluşturma](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) ekran kaydı.</span><span class="sxs-lookup"><span data-stu-id="943a2-217">Instructions for getting an API key can be found in the [Creating Applications to Access Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.</span></span>

## <a name="complete-sample"></a><span data-ttu-id="943a2-218">Tam örnek</span><span class="sxs-lookup"><span data-stu-id="943a2-218">Complete sample</span></span>
<span data-ttu-id="943a2-219">[Kaynak kodu](https://github.com/darrelmiller/ApimEventProcessor) ve testleri örnek için GitHub üzerinde.</span><span class="sxs-lookup"><span data-stu-id="943a2-219">The [source code](https://github.com/darrelmiller/ApimEventProcessor) and tests for the sample are on GitHub.</span></span> <span data-ttu-id="943a2-220">İhtiyacınız olacak bir [API Management hizmeti](api-management-get-started.md), [bağlı bir olay hub '](api-management-howto-log-event-hubs.md)ve bir [depolama hesabı](../storage/common/storage-create-storage-account.md) örneği kendiniz çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="943a2-220">You will need an [API Management Service](api-management-get-started.md), [a connected Event Hub](api-management-howto-log-event-hubs.md), and a [Storage Account](../storage/common/storage-create-storage-account.md) to run the sample for yourself.</span></span>   

<span data-ttu-id="943a2-221">Örnek olay Hub'ından gelen olayların dönüştürür için bunlara dinler yalnızca basit bir konsol uygulaması olan bir `HttpRequestMessage` ve `HttpResponseMessage` nesneleri ve bunları açın Runscope API iletir.</span><span class="sxs-lookup"><span data-stu-id="943a2-221">The sample is just a simple Console application that listens for events coming from Event Hub, converts them into a `HttpRequestMessage` and `HttpResponseMessage` objects and then forwards them on to the Runscope API.</span></span>

<span data-ttu-id="943a2-222">Animasyonlu aşağıdaki görüntüde, işlenen iletilen ve alınan ileti gösteren konsol uygulaması ve ardından istek ve yanıt Runscope trafiği Denetçisi'nde gösteren Geliştirici Portalı'nda bir API için yapılan bir istek görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="943a2-222">In the following animated image, you can see a request being made to an API in the Developer Portal, the Console application showing the message being received, processed and forwarded and then the request and response showing up in the Runscope Traffic inspector.</span></span>

![İstek için Runscope iletilen Tanıtımı](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a><span data-ttu-id="943a2-224">Özet</span><span class="sxs-lookup"><span data-stu-id="943a2-224">Summary</span></span>
<span data-ttu-id="943a2-225">Azure API Management hizmeti, Apı'lerinizi gelen ve giden seyahatte HTTP trafiğini yakalamak için ideal bir yer sağlar.</span><span class="sxs-lookup"><span data-stu-id="943a2-225">Azure API Management service provides an ideal place to capture the HTTP traffic travelling to and from your APIs.</span></span> <span data-ttu-id="943a2-226">Azure Event Hubs bu trafiği yakalamak için bir yüksek oranda ölçeklenebilir ve düşük maliyetli çözümdür ve günlüğe kaydetme için ikincil işleme sistemleri içine besleme, izleme ve diğer gelişmiş analiz.</span><span class="sxs-lookup"><span data-stu-id="943a2-226">Azure Event Hubs is a highly scalable, low cost solution for capturing that traffic and feeding it into secondary processing systems for logging, monitoring and other sophisticated analytics.</span></span> <span data-ttu-id="943a2-227">Runscope basit bir düzine birkaç kod olduğu gibi sistemleri izleme 3 taraf trafiği bağlanılıyor.</span><span class="sxs-lookup"><span data-stu-id="943a2-227">Connecting to 3rd party traffic monitoring systems like Runscope is a simple as a few dozen lines of code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="943a2-228">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="943a2-228">Next steps</span></span>
* <span data-ttu-id="943a2-229">Azure Event Hubs hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="943a2-229">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="943a2-230">Azure Event Hubs ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="943a2-230">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="943a2-231">EventProcessorHost bulunan iletiler alma</span><span class="sxs-lookup"><span data-stu-id="943a2-231">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="943a2-232">Event Hubs programlama kılavuzu</span><span class="sxs-lookup"><span data-stu-id="943a2-232">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="943a2-233">API Management ve Event Hubs ile tümleştirme hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="943a2-233">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="943a2-234">Azure Event hubs'a Azure API Management'te olayları günlüğe kaydetme hakkında</span><span class="sxs-lookup"><span data-stu-id="943a2-234">How to log events to Azure Event Hubs in Azure API Management</span></span>](api-management-howto-log-event-hubs.md)
  * [<span data-ttu-id="943a2-235">Günlükçü varlık başvurusu</span><span class="sxs-lookup"><span data-stu-id="943a2-235">Logger entity reference</span></span>](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [<span data-ttu-id="943a2-236">Günlük eventhub ilke başvurusu</span><span class="sxs-lookup"><span data-stu-id="943a2-236">log-to-eventhub policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
