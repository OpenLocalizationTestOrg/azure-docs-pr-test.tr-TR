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
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a>Azure API Management, olay hub'ları ve Runscope Apı'lerinizi izleme
Merhaba [API Management hizmeti](api-management-key-concepts.md) birçok yetenekleri tooenhance hello işlenmesini HTTP gönderilen istekleri tooyour HTTP API sağlar. Ancak, hello istekleri varlığını hello ve yanıtları geçicidir. Merhaba istek yapıldığında ve hello API Management hizmeti tooyour arka API akar. API'nizi hello isteği işler ve bir yanıtı geri toohello API tüketici akar. Merhaba yayımcı portal panosunda, ancak ötesinde Hello API Management hizmeti bazı önemli istatistik hello API'leri görüntülenmek hakkında tutar, hello ayrıntıları kaldırılmıştır.

Hello kullanarak [günlük eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [İlkesi](api-management-howto-policies.md) hello API Management hizmeti, herhangi bir ayrıntıyı hello istek ve yanıt tooan gönderebilirsiniz [Azure olay hub'ı](../event-hubs/event-hubs-what-is-event-hubs.md). Çeşitli nedenlerle tooyour API'leri gönderilen HTTP iletileri toogenerate olaylarından neden isteyebilirsiniz vardır. Denetim izi güncelleştirmeler, kullanım analizi, özel durum uyarı ve 3 taraf tümleştirmeler bazı örnekler.   

Bu makalede nasıl toocapture hello tüm HTTP istek ve yanıt iletisi, olay hub'ı tooan göndermek ve günlüğe kaydetme ve Hizmetleri izleme HTTP sağlar, ileti tooa üçüncü taraf hizmeti geçiş gösterilmektedir.

## <a name="why-send-from-api-management-service"></a>API Management hizmetinden neden gönderilsin mi?
Bu, HTTP API çerçeveler toocapture HTTP istekleri ve yanıtları takın ve günlüğe kaydetme ve izleme sistemleri içine akış olası toowrite HTTP Ara yazılımıdır. Merhaba dezavantajı toothis hello HTTP Ara hello arka uç API tümleşik toobe gerekir ve hello API hello platformunu eşleşmelidir yaklaşımdır. Birden çok API'leri varsa her biri hello Ara dağıtmanız gerekir. Genellikle arka uç API'leri neden güncelleştirilemiyor nedenleri vardır.

Günlüğe kaydetme altyapısıyla Hello Azure API Management hizmeti toointegrate kullanarak merkezi ve platformdan bağımsız bir çözüm sağlar. Ayrıca ölçeklenebilir, kısmen son toohello [coğrafi çoğaltma](api-management-howto-deploy-multi-region.md) Azure API yönetimi özellikleri.

## <a name="why-send-tooan-azure-event-hub"></a>Neden Azure olay hub'ı tooan gönderilsin mi?
Makul tooask olduğundan, neden belirli tooAzure Event hubs bir ilke oluşturun? Burada toolog isteklerim istiyorum pek çok farklı yerde vardır. Neden hello doğrudan toohello son hedefi istekleri yalnızca gönderilsin mi?  Bir seçenektir. Ancak, bir API management hizmeti günlük kaydı isteklerinden yaparken gerekli tooconsider olmasından günlük iletilerini hello API hello performansını nasıl etkiler. Aşamalı yükleme artışlar sistem bileşenleri kullanılabilir örneklerini artırarak veya coğrafi çoğaltma yararlanarak işlenebilir. Ancak, trafiğin kısa ani istekleri toologging altyapı yük altında tooslow başlatırsanız önemli ölçüde Gecikmeli istekleri toobe neden olabilir.

Hello Azure Event Hubs tasarlanmış tooingress çok büyük miktarda veriyi, olayların ne kadar daha yüksek bir sayı HTTP hello sayısından ilgilenmek için kapasiteli çoğu API işlem istekleri. Merhaba olay hub'ı Gelişmiş arabellek depolamak ve hello iletileri işlemek API management hizmeti ve hello altyapınızı arasındaki bir tür olarak görev yapar. Bu API performansınızı toohello günlük altyapısı görmeyecektir sağlar.  

Hello veri tooan olay hub'ı geçtikten sonra kalıcıdır ve bekleyecek olay hub'ı tüketicileri tooprocess için bunu. Merhaba olay hub'ı nasıl işlenir ilgilenmez, yalnızca selamlama iletisine başarıyla teslim edilecek emin olmanızı hedefler cares.     

Olay hub'ları hello özelliği toostream olayları toomultiple tüketici grupları vardır. Bu, tamamen farklı sistemleri tarafından işlenen olayların toobe sağlar. Bu, yalnızca bir olay oluşturulan toobe gerektiği hello hello API isteğinin hello API Management hizmeti içinde işleme ek gecikmeler koymadan birçok tümleştirme senaryolarına destek sağlar.

## <a name="a-policy-toosend-applicationhttp-messages"></a>Bir ilke toosend uygulama/http iletileri
Bir olay hub'ı olay verisi basit bir dize olarak kabul eder. Bu dizeyi Merhaba içeriğine tooyou tamamen var. toobe mümkün toopackage bir HTTP isteği yukarı ve tooEvent tooformat hello dize hello istek veya yanıt bilgilerle ihtiyacımız hub kapalı gönderebilirsiniz. Biz yeniden kullanabilir, varolan bir biçim ise bu gibi durumlarda, ardından biz toowrite kendi ayrıştırma kodu olmayabilir. Başlangıçta ı hello kullanarak kabul [HAR](http://www.softwareishard.com/blog/har-12-spec/) HTTP istekleri ve yanıtları göndermek için. Ancak, bu biçim HTTP istekleri dizisi tabanlı JSON biçiminde depolamak için optimize edilmiştir. Gereksiz karmaşıklık hello kablo üzerinden hello HTTP ileti geçirme hello senaryosu için eklenen zorunlu öğelerin sayısını içeriyor.  

Alternatif bir seçenek toouse hello edildi `application/http` medya türü hello HTTP belirtiminde açıklandığı gibi [RFC 7230](http://tools.ietf.org/html/rfc7230). Bu ortam türünü hello aynı diğer bir deyişle kullanılan tooactually HTTP iletileri gönderme hello kablo üzerinden biçimi, ancak hello tüm ileti hello başka bir HTTP istek gövdesinde yerleştirilebileceği tam kullanır. Örneğimizde biz yalnızca toouse hello gövde bizim ileti toosend tooEvent hub adımıdır. Rahat, var. bir çözümleyici yok [Microsoft ASP.NET Web API 2.2 istemci](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) Bu biçim ayrıştırabilir ve hello yerel Dönüştür kitaplıkları `HttpRequestMessage` ve `HttpResponseMessage` nesneleri.

toobe mümkün toocreate tootake avantajı, C# dayalı ihtiyacımız bu iletiyi [ilke ifadelerini](https://msdn.microsoft.com/library/azure/dn910913.aspx) Azure API Management'te. Bir HTTP istek iletisi tooAzure olay hub'ları gönderen hello İlkesi aşağıdadır.

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

### <a name="policy-declaration"></a>İlke bildirimi
Var. Bu ilke ifadesi hakkında söz değerinde belirli birkaç. Merhaba günlük eventhub İlkesi API Management hizmeti hello içinde oluşturulan Günlükçü toohello adını başvuran Günlükçü kimliği adlı bir öznitelik içeriyor. Merhaba hello belgede nasıl toosetup hello API Management hizmeti, bir olay hub'ı Günlükçü bulunabilir ayrıntılarını [nasıl toolog olayları tooAzure olay hub'ları Azure API Management'te](api-management-howto-log-event-hubs.md). Merhaba ikinci öznitelik olay hub'ları hangi bölüm toostore hello iletisinde yönlendiren isteğe bağlı bir parametredir. Olay hub'ları bölümleri tooenable scalabilty kullanın ve en az iki gerektirir. iletilerin teslimini sıralı hello yalnızca bir bölüm içinde sağlanır. Biz olay hub'ı hangi bölüm tooplace hello iletisinde istemeniz değil, hepsini algoritması toodistribute hello Yük kullanır. Ancak, bazı sıralama dışında işlenen bizim iletileri toobe neden.  

### <a name="partitions"></a>Bölümler
Bizim iletileri tooconsumers sırayla teslim edilir ve bölümlerinin hello yük dağıtım özellikten yararlanabilir tooensure toosend HTTP isteği iletilerini tooone bölüm ve HTTP yanıt iletilerini tooa İkinci bölüm seçtiniz. Bu durum, hatta yük dağıtımı güvence altına alır ve tüm isteklerin sırada kullanılır ve tüm yanıtları sırayla tüketilebilir garanti ediyoruz. Hello karşılık gelen isteği önce tüketilen yanıt toobe mümkündür, ancak sahibiz gibi bir sorun olmadığı ilişkilendirme için farklı bir mekanizma tooresponses ister ve istekleri her zaman yanıtları önce gelen biliyoruz.

### <a name="http-payloads"></a>HTTP yükü
Merhaba oluşturduktan sonra `requestLine` hello istek gövdesi kesiliyor biz toosee kontrol edin. Merhaba istek gövdesi kesilmiş tooonly 1024 ' dir. Bu artan, ancak tek bir olay hub'ı ileti sınırlı too256KB; dolayısıyla bazı HTTP ileti tek bir iletiye sığmayacak değil gövdeleri olduğunu olasıdır. Günlüğe kaydetme ve analiz önemli miktarda bilgi yaparken yalnızca hello HTTP isteği satır ve üstbilgileri elde edilebilir. Ayrıca, birçok API istekleri yalnızca küçük gövdeleri dönün ve büyük gövdeleri kesilmesiyle tarafından bilgi değeri hello kaybı karşılaştırma toohello azalma aktarımı oldukça az olacak şekilde işleme ve depolama maliyetlerini tookeep tüm gövdesi içeriği. Merhaba gövdesinin işlenmesi hakkında son OneNote olduğu toopass ihtiyacımız `true` toohello olarak<string>() yönteminin hello gövdesi içeriği okumakta olduğunuz nedeni ancak, aynı zamanda istediğiniz hello arka uç API'si toobe mümkün tooread hello gövdesi. TRUE toothis yöntemi geçirerek biz böylece ikinci kez okunabilecek arabellekli hello gövde toobe neden. Bu önemli toobe çok büyük dosyaları karşıya yükleme veya uzun yoklama kullanan bir API varsa farkında değildir. Bu durumlarda hello gövde hiç okuma en iyi tooavoid olacaktır.   

### <a name="http-headers"></a>HTTP üstbilgileri
HTTP üstbilgileri yalnızca üzerinden basit anahtar/değer çifti biçiminde hello ileti biçimi içine aktarılabilir. Biz toostrip belirli güvenlik çıkışı gizli alanlar, kimlik bilgileri gereksiz yere sızmasını tooavoid seçtiniz. API anahtarları ve diğer kimlik bilgilerini analiz amaçlı kullanılacak düşüktür. Merhaba kullanıcı ve hello belirli ürün toodo analiz isterseniz, kullandıkları sonra biz, hello alabilir `context` nesne ve toohello ileti ekleyin.     

### <a name="message-metadata"></a>İleti meta verileri
Merhaba tamamlandı iletisini toosend toohello olay hub'ı oluştururken hello ilk satırı hello gerçekte bir parçası değil `application/http` ileti. ek meta veri selamlama iletisine bir istek veya yanıt iletisi olup oluşan Hello ilk satırı olan ve kullanılan toocorrelate olan bir ileti kimliği tooresponses ister. Merhaba ileti kimliği, şuna benzer başka bir ilke kullanılarak oluşturulur:

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

Bir değişkende hello kadar yanıt döndürdü ve sonra yalnızca hello istek ve yanıt tek bir ileti gönderilir, depolanan hello istek iletisi oluşturduk. İki ancak hello istek ve yanıt bağımsız olarak gönderme ve bir ileti kimliği toocorrelate kullanarak Merhaba, biz biraz daha fazla esneklik hello ileti boyutu, birden çok bölüm hello özelliği tootake avantajlarından ileti sırası ve hello koruyarak adımında Al İstek er bizim günlük panosunda görüntülenir. Ayrıca, geçerli bir yanıt hiçbir zaman toohello olay hub'ı, büyük olasılıkla hello API Management hizmeti, tooa önemli isteği hatası nedeniyle gönderilir ancak biz yine hello isteğinin bir kayda sahip olacaksınız bazı senaryolar olabilir.

Hello İlkesi toosend hello yanıt HTTP iletisi çok benzer toohello isteği arar ve hello tamamlamak için ilke yapılandırması şöyle görünür:

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

Merhaba `set-variable` ilkesi oluşturur hem hello tarafından erişilebilir olan bir değer `log-to-eventhub` hello ilkesinde `<inbound>` bölümü ve hello `<outbound>` bölümü.  

## <a name="receiving-events-from-event-hubs"></a>Event Hubs'a ait alma olaylarını
Azure Event Hub olaylarından hello kullanarak alınan [AMQP protokolünü](http://www.amqp.org/). Merhaba Microsoft Service Bus ekibine, istemci kitaplıkları kullanılabilir toomake hello olayları daha kolay tüketen yapmış. Desteklenen iki farklı yaklaşım vardır, biri yükleniyor bir *doğrudan tüketici* ve hello diğer hello kullanarak `EventProcessorHost` sınıfı. Bu iki yaklaşım örnekleri hello bulunabilir [Event Hubs Programlama Kılavuzu](../event-hubs/event-hubs-programming-guide.md). Merhaba kısa hello farklar sürümüdür, `Direct Consumer` tam denetim ve hello sağlar `EventProcessorHost` ancak bu olayları nasıl işleyecek hakkında bazı varsayımlarda bulunur hello tesisat iş bazıları desteklemez.  

### <a name="eventprocessorhost"></a>EventProcessorHost
Bu örnekte, hello kullanacağız `EventProcessorHost` kolaylık sağlamak için ancak bunu değil hello belirli bu senaryo için en iyi seçimdir. `EventProcessorHost`iş parçacığı oluşturma sorunları belirli olay işlemcisi sınıfı içinde hakkında tooworry yok emin sabit iş hello. Ancak, Senaryomuzda, biz yalnızca hello ileti tooanother biçimine dönüştürme ve bir zaman uyumsuz yöntem kullanarak tooanother hizmet geçirme. Paylaşılan durum ve iş parçacığı oluşturma sorunları, bu nedenle hiçbir risk güncelleştirmek için gerek yoktur. Çoğu senaryo için `EventProcessorHost` büyük olasılıkla hello en iyi seçenek, kesinlikle hello daha kolay seçeneği ise.     

### <a name="ieventprocessor"></a>Ieventprocessor
kullanırken hello merkezi kavram `EventProcessorHost` toocreate olan bir başlangıç uygulaması `IEventProcessor` hello yöntemi içeren arabirimi `ProcessEventAsync`. Bu yöntem Hello özünü burada gösterilir:

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

EventData nesnelerin bir listesini hello yönteme geçirilen ve biz bu liste yineleme. Her yöntemin Hello bayt HttpMessage nesnesine Ayrıştırılan ve söz konusu nesne IHttpMessageProcessor tooan örneğini geçirilir.

### <a name="httpmessage"></a>HttpMessage
Merhaba `HttpMessage` örnek veri üç parçalarını içerir:

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

Merhaba `HttpMessage` örneğini içeren bir `MessageId` bize toohello karşılık gelen HTTP yanıtı ve bir Boole değeri, tooconnect hello HTTP isteğinin olanak GUID tanımlayan hello nesnesi bir HttpRequestMessage örneği içeriyorsa ve Bilgisayarın HttpResponseMessage. HTTP sınıflardan yerleşik hello kullanarak `System.Net.Http`, hello mümkün tootake avantajlarından edildi `application/http` dahil kod ayrıştırma `System.Net.Http.Formatting`.  

### <a name="ihttpmessageprocessor"></a>IHttpMessageProcessor
Merhaba `HttpMessage` örneği tooimplementation, ardından iletilen `IHttpMessageProcessor` oluşturduğum toodecouple hello alma ve hello olay yorumu Azure olay hub'ı ve hello gerçek bu işleme bir arabirim olduğu.

## <a name="forwarding-hello-http-message"></a>Merhaba HTTP ileti iletme
Bu örnek için onu olacaktır ilginç toopush hello HTTP isteği üzerinden çok ı karar[Runscope](http://www.runscope.com). Runscope hata ayıklama, günlüğe kaydetme ve izleme HTTP uzmanlaşmış bulut tabanlı bir hizmettir. Kolay tootry olduğu ve gerçek zamanlı bizim API Management hizmeti aracılığıyla akan toosee hello HTTP istek bize sağlayan ücretsiz bir katman sahiptirler.

Merhaba `IHttpMessageProcessor` uygulaması şu şekilde görünür

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

Mümkün tootake avantajlarından olan bir [Runscope için var olan istemci Kitaplığı](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) , kolay toopush yapar `HttpRequestMessage` ve `HttpResponseMessage` kendi hizmetinde örnekleri ayarlama. Sırayla tooaccess Runscope bir hesap ve bir API anahtarı gerekir API hello. Bir API anahtarı alma yönergeleri hello bulunabilir [uygulamaları oluşturma tooAccess Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) ekran kaydı.

## <a name="complete-sample"></a>Tam örnek
Merhaba [kaynak kodu](https://github.com/darrelmiller/ApimEventProcessor) ve testleri hello örnek için GitHub üzerinde. İhtiyacınız olacak bir [API Management hizmeti](api-management-get-started.md), [bağlı bir olay hub '](api-management-howto-log-event-hubs.md)ve bir [depolama hesabı](../storage/common/storage-create-storage-account.md) toorun hello örnek kendiniz için.   

Merhaba olay Hub'ından gelen olayların dönüştürür için bunlara dinler yalnızca basit bir konsol uygulaması örnektir bir `HttpRequestMessage` ve `HttpResponseMessage` nesneleri ve bunları Runscope API toohello üzerinde iletir.

Animasyonlu resmi aşağıdaki hello tooan API hello Geliştirici Portalı, alınan, hello konsol uygulaması gösteren hello iletisi yapılan bir istek işlenen ve iletilen ve istek ve yanıt hello Runscope trafiği gösteren hello görebilirsiniz Denetleyici.

![İstek tooRunscope iletilen Tanıtımı](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a>Özet
Azure API Management hizmeti, API'lerden tooand seyahatte bir ideal yer toocapture hello HTTP trafiği sağlar. Azure Event Hubs bu trafiği yakalamak için bir yüksek oranda ölçeklenebilir ve düşük maliyetli çözümdür ve günlüğe kaydetme için ikincil işleme sistemleri içine besleme, izleme ve diğer gelişmiş analiz. Runscope basit bir düzine birkaç kod olduğu gibi sistemleri izleme too3rd taraf trafiği bağlanılıyor.

## <a name="next-steps"></a>Sonraki adımlar
* Azure Event Hubs hakkında daha fazla bilgi edinin
  * [Azure Event Hubs ile çalışmaya başlama](../event-hubs/event-hubs-c-getstarted-send.md)
  * [EventProcessorHost bulunan iletiler alma](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [Event Hubs programlama kılavuzu](../event-hubs/event-hubs-programming-guide.md)
* API Management ve Event Hubs ile tümleştirme hakkında daha fazla bilgi edinin
  * [Nasıl toolog olayları tooAzure Azure API Management olay hub'ları](api-management-howto-log-event-hubs.md)
  * [Günlükçü varlık başvurusu](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [Günlük eventhub ilke başvurusu](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
