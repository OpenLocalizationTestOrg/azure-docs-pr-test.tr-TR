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
# <a name="monitor-and-diagnose-request-processing-at-hello-reverse-proxy"></a>İzleme ve istek işleme hello ters proxy tanılama

Service Fabric Hello 5.7 sürümünden başlayarak, ters proxy olayları koleksiyonu için kullanılabilir. Merhaba olayları iki kanallarında kullanılabilir yalnızca hata olayları ile ilgili hello ters proxy ve girişleri hem başarılı hem başarısız istekler için ayrıntılı olaylarla içeren ikinci kanal toorequest işleme hatası.

Çok başvuran[ters proxy olayları toplamak](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) bu kanalları yerel ve Azure Service Fabric kümeleri gelen olay toplama tooenable.

## <a name="troubleshoot-using-diagnostics-logs"></a>Tanılama günlükleri kullanarak sorun giderme
İşte bazı örnekler toointerpret hello ortak hata günlükleri bir nasıl karşılaşabilirsiniz:

1. Ters proxy yanıt durum kodu 504 (zaman aşımı) döndürür.

    Nedenlerinden biri toohello hizmetinin başarısız olmasıyla tooreply hello isteği zaman aşımı süresi içinde olabilir.
Merhaba ilk olay aşağıdaki hello ters proxy alınan hello isteği hello ayrıntılarını kaydeder. Merhaba ikinci olay bu hello isteği başarısız iletme tooservice sırasında son çok gösterir "İç hata ERROR_WINHTTP_TIMEOUT =" 

    Merhaba yükü içerir:

    *  **traceId**: Bu GUID olabilir tooa tek isteğine karşılık gelen tüm hello olayları toocorrelate kullanılır. İki olay aşağıda Hello traceId hello = **2f87b722-e254-4ac2-a802-fd315c1a0271**, ait oldukları toohello olduğunu belirtmek aynı isteği.
    *  **requestUrl**: hello URL (ters proxy URL) toowhich hello isteği gönderildi.
    *  **Fiili**: HTTP fiili.
    *  **remoteAddress**: hello isteği göndererek istemci adresidir.
    *  **resolvedServiceUrl**: hizmet uç noktası URL'si toowhich hello gelen isteği çözülmüş. 
    *  **errorDetails**: hello hatayla ilgili ek bilgiler.

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

2. Ters proxy yanıt durum kodu 404 (bulunamadı) döndürür. 
    
    Hizmet uç noktası eşleşen toofind hello başarısız olduğundan ters proxy 404 döndüğü bir örnek olay aşağıdadır.
    Burada ilgi Hello yükü girişleri şunlardır:
    *  **processRequestPhase**: hello başarısız oldu, isteği işleme sırasında hello aşamasını gösterir ***TryGetEndpoint*** yani çalışırken toofetch hello hizmet uç noktası tooforward için. 
    *  **errorDetails**: hello uç noktası arama ölçütlerini listeler. Burada belirtilen bu hello listenerName görebilirsiniz = **FrontEndListener** içerirken hello çoğaltma uç nokta listesi yalnızca hello adıyla bir dinleyici **OldListener**.
    
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
    Başka bir örneği burada ters proxy dönebilirsiniz 404 bulunamıyorsa: ApplicationGateway\Http yapılandırma parametresi **SecureOnlyMode** tootrue dinlemede hello ters proxy ile ayarlanır **HTTPS**, ancak hello yineleme bitiş noktalarının tümü güvenli olmayan (HTTP dinleme).
    HTTPS tooforward hello isteğine dinleyen bir uç nokta bulunamadı bu yana proxy döndürür 404 ters çevrilir. Merhaba olay yükü Hello parametrelerinde çözümleme hello sorunu aşağı toonarrow yardımcı olur:
    
    ```
        "errorDetails": "SecureOnlyMode = true, gateway protocol = https, listenerName = NewListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Http:\/\/localhost:8491\/LocationApp\/\", \"NewListener\":\"Http:\/\/localhost:8492\/LocationApp\/\"}}"
    ```

3. İstek toohello ters proxy zaman aşımı hatasıyla başarısız oluyor. 
    Merhaba olay günlüklerini Olay hello alınan istek ayrıntıları (burada gösterilmiyor) içerir.
    Merhaba sonraki olay hello hizmeti 404 durum koduyla yanıt verdi ve yeniden çözümlemek ters proxy başlatır gösterir. 

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
    Tüm hello olaylarını toplarken, her çözümleyin ve iletme girişimi gösteren olayların tren görürsünüz.
    Merhaba serideki son olay Hello hello istek işleme başarılı çözümleme denemesi sayısı hello yanı sıra zaman aşımı ile başarısız oldu gösterir.
    
    > [!NOTE]
    > Varsayılan olarak devre dışı tookeep hello ayrıntılı kanal olay toplama önerilir ve bir gereksinim temelinde sorun giderme için etkinleştirin.

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
    
    Koleksiyon yalnızca kritik/hata olayları etkinleştirilirse, hello zaman aşımı ve çözümleme denemesi sayısı hello ilişkin ayrıntıları içeren bir olay bakın. 
    
    Merhaba hizmet toosend 404 durum kodu geri toohello kullanıcı çalışırsa, bir "X-ServiceFabric" başlığına göre eşlik etmelidir. Bu düzelttikten sonra ters proxy ileten hello durum kodu geri toohello istemci görürsünüz.  

4. Merhaba istemci hello isteği kesildiğinde durumları.

    Olay aşağıda Hello ters proxy hello yanıt tooclient iletme ancak hello istemci bağlantısını keser kaydedilir:

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
> Olaylar ilgili toowebsocket isteği işleme şu anda günlüğe kaydedilmez. Bu hello sonraki sürümde eklenecek.

## <a name="next-steps"></a>Sonraki adımlar
* [Olay toplama ve Windows Azure Tanılama'yı kullanarak koleksiyon](service-fabric-diagnostics-event-aggregation-wad.md) günlük toplama Azure kümelerinde etkinleştirme.
* Visual Studio'da tooview Service Fabric olaylara bakın [İzleyici ve yerel olarak tanılamak](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).
* Çok başvuran[ters proxy tooconnect toosecure hizmetlerini yapılandırma](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) için Azure Resource Manager şablonu güvenli ters proxy hello farklı hizmet sertifika doğrulama seçeneklerini tooconfigure örnekleri.
* Okuma [Service Fabric ters proxy](service-fabric-reverseproxy.md) toolearn daha fazla.
