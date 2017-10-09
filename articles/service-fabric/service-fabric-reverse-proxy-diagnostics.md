---
title: "Service Fabric aaaAzure ters proxy tanılama | Microsoft Docs"
description: "Bilgi nasıl toomonitor ve istek işleme hello ters proxy tanılayın."
services: service-fabric
documentationcenter: .net
author: kavyako
manager: vipulm
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: kavyako
ms.openlocfilehash: 9687b9688dc26ba619cbdfab1b1f49a3035345c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-request-processing-at-hello-reverse-proxy"></a><span data-ttu-id="ff5ff-103">İzleme ve istek işleme hello ters proxy tanılama</span><span class="sxs-lookup"><span data-stu-id="ff5ff-103">Monitor and diagnose request processing at hello reverse proxy</span></span>

<span data-ttu-id="ff5ff-104">Service Fabric Hello 5.7 sürümünden başlayarak, ters proxy olayları koleksiyonu için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-104">Starting with hello 5.7 release of Service Fabric, reverse proxy events are available for collection.</span></span> <span data-ttu-id="ff5ff-105">Merhaba olayları iki kanallarında kullanılabilir yalnızca hata olayları ile ilgili hello ters proxy ve girişleri hem başarılı hem başarısız istekler için ayrıntılı olaylarla içeren ikinci kanal toorequest işleme hatası.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-105">hello events are available in two channels, one with only error events related toorequest processing failure at hello reverse proxy and second channel containing verbose events with entries for both successful and failed requests.</span></span>

<span data-ttu-id="ff5ff-106">Çok başvuran[ters proxy olayları toplamak](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) bu kanalları yerel ve Azure Service Fabric kümeleri gelen olay toplama tooenable.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-106">Refer too[Collect reverse proxy events](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) tooenable collecting events from these channels in local and Azure Service Fabric clusters.</span></span>

## <a name="troubleshoot-using-diagnostics-logs"></a><span data-ttu-id="ff5ff-107">Tanılama günlükleri kullanarak sorun giderme</span><span class="sxs-lookup"><span data-stu-id="ff5ff-107">Troubleshoot using diagnostics logs</span></span>
<span data-ttu-id="ff5ff-108">İşte bazı örnekler toointerpret hello ortak hata günlükleri bir nasıl karşılaşabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ff5ff-108">Here are some examples on how toointerpret hello common failure logs that one can encounter:</span></span>

1. <span data-ttu-id="ff5ff-109">Ters proxy yanıt durum kodu 504 (zaman aşımı) döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-109">Reverse proxy returns response status code 504 (Timeout).</span></span>

    <span data-ttu-id="ff5ff-110">Nedenlerinden biri toohello hizmetinin başarısız olmasıyla tooreply hello isteği zaman aşımı süresi içinde olabilir.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-110">One reason could be due toohello service failing tooreply within hello request timeout period.</span></span>
<span data-ttu-id="ff5ff-111">Merhaba ilk olay aşağıdaki hello ters proxy alınan hello isteği hello ayrıntılarını kaydeder.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-111">hello first event below logs hello details of hello request received at hello reverse proxy.</span></span> <span data-ttu-id="ff5ff-112">Merhaba ikinci olay bu hello isteği başarısız iletme tooservice sırasında son çok gösterir "İç hata ERROR_WINHTTP_TIMEOUT ="</span><span class="sxs-lookup"><span data-stu-id="ff5ff-112">hello second event indicates that hello request failed while forwarding tooservice, due too"internal error = ERROR_WINHTTP_TIMEOUT"</span></span> 

    <span data-ttu-id="ff5ff-113">Merhaba yükü içerir:</span><span class="sxs-lookup"><span data-stu-id="ff5ff-113">hello payload includes:</span></span>

    *  <span data-ttu-id="ff5ff-114">**traceId**: Bu GUID olabilir tooa tek isteğine karşılık gelen tüm hello olayları toocorrelate kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-114">**traceId**: This GUID can be used toocorrelate all hello events corresponding tooa single request.</span></span> <span data-ttu-id="ff5ff-115">İki olay aşağıda Hello traceId hello = **2f87b722-e254-4ac2-a802-fd315c1a0271**, ait oldukları toohello olduğunu belirtmek aynı isteği.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-115">In hello below two events, hello traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**, implying they belong toohello same request.</span></span>
    *  <span data-ttu-id="ff5ff-116">**requestUrl**: hello URL (ters proxy URL) toowhich hello isteği gönderildi.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-116">**requestUrl**: hello URL (Reverse proxy URL) toowhich hello request was sent.</span></span>
    *  <span data-ttu-id="ff5ff-117">**Fiili**: HTTP fiili.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-117">**verb**: HTTP verb.</span></span>
    *  <span data-ttu-id="ff5ff-118">**remoteAddress**: hello isteği göndererek istemci adresidir.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-118">**remoteAddress**: Address of client sending hello request.</span></span>
    *  <span data-ttu-id="ff5ff-119">**resolvedServiceUrl**: hizmet uç noktası URL'si toowhich hello gelen isteği çözülmüş.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-119">**resolvedServiceUrl**: Service endpoint URL toowhich hello incoming request was resolved.</span></span> 
    *  <span data-ttu-id="ff5ff-120">**errorDetails**: hello hatayla ilgili ek bilgiler.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-120">**errorDetails**: Additional information about hello failure.</span></span>

    ```
    {
      "Timestamp": "2017-07-20T15:57:59.9871163-07:00",
      "ProviderName": "Microsoft-ServiceFabric",
      "Id": 51477,
      "Message": "2f87b722-e254-4ac2-a802-fd315c1a0271 Request url = https://localhost:19081/LocationApp/LocationFEService?zipcode=98052, verb = GET, remote (client) address = ::1, resolved service url = Https://localhost:8491/LocationApp/?zipcode=98052, request processing start time =     15:58:00.074114 (745,608.196 MSec) ",
      "ProcessId": 57696,
      "Level": "Informational",
      "Keywords": "0x1000000000000021",
      "EventName": "ReverseProxy",
      "ActivityID": null,
      "RelatedActivityID": null,
      "Payload": {
        "traceId": "2f87b722-e254-4ac2-a802-fd315c1a0271",
        "requestUrl": "https://localhost:19081/LocationApp/LocationFEService?zipcode=98052",
        "verb": "GET",
        "remoteAddress": "::1",
        "resolvedServiceUrl": "Https://localhost:8491/LocationApp/?zipcode=98052",
        "requestStartTime": "2017-07-20T15:58:00.0741142-07:00"
      }
    }

    {
      "Timestamp": "2017-07-20T16:00:01.3173605-07:00",
      ...
      "Message": "2f87b722-e254-4ac2-a802-fd315c1a0271 Error while forwarding request tooservice: response status code = 504, description = Reverse proxy Timeout, phase = FinishSendRequest, internal error = ERROR_WINHTTP_TIMEOUT ",
      ...
      "Payload": {
        "traceId": "2f87b722-e254-4ac2-a802-fd315c1a0271",
        "statusCode": 504,
        "description": "Reverse Proxy Timeout",
        "sendRequestPhase": "FinishSendRequest",
        "errorDetails": "internal error = ERROR_WINHTTP_TIMEOUT"
      }
    }
    ```

2. <span data-ttu-id="ff5ff-121">Ters proxy yanıt durum kodu 404 (bulunamadı) döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-121">Reverse proxy returns response status code 404 (Not Found).</span></span> 
    
    <span data-ttu-id="ff5ff-122">Hizmet uç noktası eşleşen toofind hello başarısız olduğundan ters proxy 404 döndüğü bir örnek olay aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-122">Here is an example event where reverse proxy returns 404 since it failed toofind hello matching service endpoint.</span></span>
    <span data-ttu-id="ff5ff-123">Burada ilgi Hello yükü girişleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ff5ff-123">hello payload  entries of interest here are:</span></span>
    *  <span data-ttu-id="ff5ff-124">**processRequestPhase**: hello başarısız oldu, isteği işleme sırasında hello aşamasını gösterir ***TryGetEndpoint*** yani</span><span class="sxs-lookup"><span data-stu-id="ff5ff-124">**processRequestPhase**: Indicates hello phase during request processing when hello failure occurred, ***TryGetEndpoint*** i.e</span></span> <span data-ttu-id="ff5ff-125">çalışırken toofetch hello hizmet uç noktası tooforward için.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-125">while trying toofetch hello service endpoint tooforward to.</span></span> 
    *  <span data-ttu-id="ff5ff-126">**errorDetails**: hello uç noktası arama ölçütlerini listeler.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-126">**errorDetails**: Lists hello endpoint search criteria.</span></span> <span data-ttu-id="ff5ff-127">Burada belirtilen bu hello listenerName görebilirsiniz = **FrontEndListener** içerirken hello çoğaltma uç nokta listesi yalnızca hello adıyla bir dinleyici **OldListener**.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-127">Here you can see that hello listenerName specified = **FrontEndListener** whereas hello replica endpoint list only contains a listener with hello name **OldListener**.</span></span>
    
    ```
    {
      ...
      "Message": "c1cca3b7-f85d-4fef-a162-88af23604343 Error while processing request, cannot forward tooservice: request url = https://localhost:19081/LocationApp/LocationFEService?ListenerName=FrontEndListener&zipcode=98052, verb = GET, remote (client) address = ::1, request processing start time = 16:43:02.686271 (3,448,220.353 MSec), error = FABRIC_E_ENDPOINT_NOT_FOUND, message = , phase = TryGetEndoint, SecureOnlyMode = false, gateway protocol = https, listenerName = FrontEndListener, replica endpoint = {\"Endpoints\":{\"\":\"Https:\/\/localhost:8491\/LocationApp\/\"}} ",
      "ProcessId": 57696,
      "Level": "Warning",
      "EventName": "ReverseProxy",
      "Payload": {
        "traceId": "c1cca3b7-f85d-4fef-a162-88af23604343",
        "requestUrl": "https://localhost:19081/LocationApp/LocationFEService?ListenerName=NewListener&zipcode=98052",
        ...
        "processRequestPhase": "TryGetEndoint",
        "errorDetails": "SecureOnlyMode = false, gateway protocol = https, listenerName = FrontEndListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Https:\/\/localhost:8491\/LocationApp\/\"}}"
      }
    }
    ```
    <span data-ttu-id="ff5ff-128">Başka bir örneği burada ters proxy dönebilirsiniz 404 bulunamıyorsa: ApplicationGateway\Http yapılandırma parametresi **SecureOnlyMode** tootrue dinlemede hello ters proxy ile ayarlanır **HTTPS**, ancak hello yineleme bitiş noktalarının tümü güvenli olmayan (HTTP dinleme).</span><span class="sxs-lookup"><span data-stu-id="ff5ff-128">Another example where reverse proxy can return 404 Not Found is: ApplicationGateway\Http configuration parameter **SecureOnlyMode** is set tootrue with hello reverse proxy listening on **HTTPS**, however all of hello replica endpoints are unsecure (listening on HTTP).</span></span>
    <span data-ttu-id="ff5ff-129">HTTPS tooforward hello isteğine dinleyen bir uç nokta bulunamadı bu yana proxy döndürür 404 ters çevrilir.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-129">Reverse proxy returns 404 since it cannot find an endpoint listening on HTTPS tooforward hello request.</span></span> <span data-ttu-id="ff5ff-130">Merhaba olay yükü Hello parametrelerinde çözümleme hello sorunu aşağı toonarrow yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="ff5ff-130">Analyzing hello parameters in hello event payload helps toonarrow down hello issue:</span></span>
    
    ```
        "errorDetails": "SecureOnlyMode = true, gateway protocol = https, listenerName = NewListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Http:\/\/localhost:8491\/LocationApp\/\", \"NewListener\":\"Http:\/\/localhost:8492\/LocationApp\/\"}}"
    ```

3. <span data-ttu-id="ff5ff-131">İstek toohello ters proxy zaman aşımı hatasıyla başarısız oluyor.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-131">Request toohello reverse proxy fails with a timeout error.</span></span> 
    <span data-ttu-id="ff5ff-132">Merhaba olay günlüklerini Olay hello alınan istek ayrıntıları (burada gösterilmiyor) içerir.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-132">hello event logs contain an event with hello received request details (not shown here).</span></span>
    <span data-ttu-id="ff5ff-133">Merhaba sonraki olay hello hizmeti 404 durum koduyla yanıt verdi ve yeniden çözümlemek ters proxy başlatır gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-133">hello next event shows that hello service responded with a 404 status code and reverse proxy initiates a re-resolve.</span></span> 

    ```
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Request tooservice returned: status code = 404, status description = , Reresolving ",
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "statusCode": 404,
        "statusDescription": ""
      }
    }
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Re-resolved service url = Https://localhost:8491/LocationApp/?zipcode=98052 ",
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "requestUrl": "Https://localhost:8491/LocationApp/?zipcode=98052"
      }
    }
    ```
    <span data-ttu-id="ff5ff-134">Tüm hello olaylarını toplarken, her çözümleyin ve iletme girişimi gösteren olayların tren görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-134">When collecting all hello events, you see a train of events showing every resolve and forward attempt.</span></span>
    <span data-ttu-id="ff5ff-135">Merhaba serideki son olay Hello hello istek işleme başarılı çözümleme denemesi sayısı hello yanı sıra zaman aşımı ile başarısız oldu gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-135">hello last event in hello series shows hello request processing has failed with a timeout, along with hello number of successful resolve attempts.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="ff5ff-136">Varsayılan olarak devre dışı tookeep hello ayrıntılı kanal olay toplama önerilir ve bir gereksinim temelinde sorun giderme için etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-136">It is recommended tookeep hello  verbose channel event collection disabled by default and enable it for troubleshooting on a need basis.</span></span>

    ```
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Error while processing request: number of successful resolve attempts = 12, error = FABRIC_E_TIMEOUT, message = , phase = ResolveServicePartition,  ",
      "EventName": "ReverseProxy",
      ...
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "resolveCount": 12,
        "errorval": -2147017729,
        "errorMessage": "",
        "processRequestPhase": "ResolveServicePartition",
        "errorDetails": ""
      }
    }
    ```
    
    <span data-ttu-id="ff5ff-137">Koleksiyon yalnızca kritik/hata olayları etkinleştirilirse, hello zaman aşımı ve çözümleme denemesi sayısı hello ilişkin ayrıntıları içeren bir olay bakın.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-137">If collection is enabled for critical/error events only, you see one event with details about hello timeout and hello number of resolve attempts.</span></span> 
    
    <span data-ttu-id="ff5ff-138">Merhaba hizmet toosend 404 durum kodu geri toohello kullanıcı çalışırsa, bir "X-ServiceFabric" başlığına göre eşlik etmelidir.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-138">If hello service intends toosend a 404 status code back toohello user, it should be accompanied by an "X-ServiceFabric" header.</span></span> <span data-ttu-id="ff5ff-139">Bu düzelttikten sonra ters proxy ileten hello durum kodu geri toohello istemci görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-139">After fixing this, you will see that reverse proxy forwards hello status code back toohello client.</span></span>  

4. <span data-ttu-id="ff5ff-140">Merhaba istemci hello isteği kesildiğinde durumları.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-140">Cases when hello client has disconnected hello request.</span></span>

    <span data-ttu-id="ff5ff-141">Olay aşağıda Hello ters proxy hello yanıt tooclient iletme ancak hello istemci bağlantısını keser kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="ff5ff-141">hello below event is recorded when reverse proxy is forwarding hello response tooclient but hello client disconnects:</span></span>

    ```
    {
      ...
      "Message": "6e2571a3-14a8-4fc7-93bb-c202c23b50b8 Unable toosend response tooclient: phase = SendResponseHeaders, error = -805306367, internal error = ERROR_SUCCESS ",
      "ProcessId": 57696,
      "Level": "Warning",
      ...
      "EventName": "ReverseProxy",
      "Payload": {
        "traceId": "6e2571a3-14a8-4fc7-93bb-c202c23b50b8",
        "sendResponsePhase": "SendResponseHeaders",
        "errorval": -805306367,
        "winHttpError": "ERROR_SUCCESS"
      }
    }
    ```

> [!NOTE]
> <span data-ttu-id="ff5ff-142">Olaylar ilgili toowebsocket isteği işleme şu anda günlüğe kaydedilmez.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-142">Events related toowebsocket request processing are not currently logged.</span></span> <span data-ttu-id="ff5ff-143">Bu hello sonraki sürümde eklenecek.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-143">This will be added in hello next release.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff5ff-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ff5ff-144">Next steps</span></span>
* <span data-ttu-id="ff5ff-145">[Olay toplama ve Windows Azure Tanılama'yı kullanarak koleksiyon](service-fabric-diagnostics-event-aggregation-wad.md) günlük toplama Azure kümelerinde etkinleştirme.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-145">[Event aggregation and collection using Windows Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md) for enabling log collection in Azure clusters.</span></span>
* <span data-ttu-id="ff5ff-146">Visual Studio'da tooview Service Fabric olaylara bakın [İzleyici ve yerel olarak tanılamak](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="ff5ff-146">tooview Service Fabric events in Visual Studio, see [Monitor and diagnose locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>
* <span data-ttu-id="ff5ff-147">Çok başvuran[ters proxy tooconnect toosecure hizmetlerini yapılandırma](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) için Azure Resource Manager şablonu güvenli ters proxy hello farklı hizmet sertifika doğrulama seçeneklerini tooconfigure örnekleri.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-147">Refer too[Configure reverse proxy tooconnect toosecure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples tooconfigure secure reverse proxy with hello different service certificate validation options.</span></span>
* <span data-ttu-id="ff5ff-148">Okuma [Service Fabric ters proxy](service-fabric-reverseproxy.md) toolearn daha fazla.</span><span class="sxs-lookup"><span data-stu-id="ff5ff-148">Read [Service Fabric reverse proxy](service-fabric-reverseproxy.md) toolearn more.</span></span>
