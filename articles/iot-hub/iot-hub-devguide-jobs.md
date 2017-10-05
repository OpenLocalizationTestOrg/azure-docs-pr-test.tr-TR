---
title: "Azure IOT Hub işleri anlama | Microsoft Docs"
description: "Geliştirici Kılavuzu - birden çok cihaz üzerinde çalışmasına işlerini zamanlama IOT hub'ına bağlı. İşler, etiketler ve istenen özelliklerini güncelleştirmek ve birden çok aygıta doğrudan yöntemleri çağırma."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: fe78458f-4f14-4358-ac83-4f7bd14ee8da
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: abb7f80662650efa8f158f32125ebc5350cb4f62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a>Birden fazla cihazda işleri zamanlama
## <a name="overview"></a>Genel Bakış
Önceki makaleleri tarafından açıklandığı gibi Azure IOT hub'ı birkaç yapı taşlarını sağlar ([cihaz çifti özellikleri ve etiketleri] [ lnk-twin-devguide] ve [doğrudan yöntemleri][lnk-dev-methods]).  Genellikle, arka uç uygulamaları cihaz yöneticileri ve işleçleri güncelleştirmek ve IOT cihazları toplu ve zamanlanan saatte etkileşim etkinleştirir.  İşlerini cihaz çifti güncelleştirmeler ve bir cihaz kümesi karşı doğrudan yöntemleri yürütme zamanlama zaman kapsüller.  Örneğin, bir işleç başlatmak ve bir grup oluşturma işlemlerini kesintiye uğratan olmayacaktır zaman 43 ve 3 kat oluşturmanın cihazı yeniden başlatmak için bir iş izleyen bir arka uç uygulaması kullanırsınız.

### <a name="when-to-use"></a>Kullanılması gereken durumlar
Göz önünde bulundurun kullanarak, işlerin ne zaman: bir çözüm arka uç gereksinimlerini zamanlamak ve ilerleme durumunu izlemek için herhangi bir cihaz kümesi üzerinde şu etkinlikler:

* İstenen özellikleri güncelleştirme
* Güncelleştirme etiketleri
* Doğrudan yöntemleri çağırma

## <a name="job-lifecycle"></a>İş yaşam döngüsü
İşlerini çözüm arka ucu tarafından başlatılan ve IOT Hub tarafından korunur.  Bir hizmet dönük URI ile bir işi başlatabilirsiniz (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) ve bir hizmet dönük URI aracılığıyla yürütülen bir işin ilerleme için sorgu (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).  Bir iş başlatıldıktan sonra işleri sorgulama işlerin durumunu yenilemek arka uç uygulama sağlar.

> [!NOTE]
> Bir işi başlattığınızda özellik adları ve değerleri yalnızca US-ASCII yazdırılabilir içerebilir herhangi aşağıdaki kümesindeki dışında alfasayısal: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.
> 
> 

## <a name="reference-topics"></a>Başvuru konuları:
Aşağıdaki başvuru konuları işleri kullanma hakkında daha fazla bilgi sağlar.

## <a name="jobs-to-execute-direct-methods"></a>İşlerini doğrudan bir yöntem yürütülemez
Yürütme için HTTP 1.1 istek ayrıntıları verilmiştir bir [doğrudan yöntemi] [ lnk-dev-methods] bir işi kullanarak cihazları bir dizi:

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleDirectRequest', 
        cloudToDeviceMethod: {
            methodName: '<methodName>',
            payload: <payload>,                 
            responseTimeoutInSeconds: methodTimeoutInSeconds 
        },
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        
    }
    ```
Sorgu koşulu da tek bir cihaz kimliği veya aygıt aşağıda gösterildiği gibi kimlikleri listesini olabilir

**Örnekler**
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
[IOT Hub sorgu dili] [ lnk-query] IOT hub'ı sorgu dili ek ayrıntılı kapsar.

## <a name="jobs-to-update-device-twin-properties"></a>Cihaz çifti özelliklerini güncelleştirmek için işlemler
Bir iş kullanarak cihaz çifti özelliklerini güncelleştirmek için HTTP 1.1 istek ayrıntıları verilmiştir:

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14
    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleTwinUpdate', 
        updateTwin: <patch>                 // Valid JSON object
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        // format TBD
    }
    ```

## <a name="querying-for-progress-on-jobs"></a>İşlerini ilerleme sorgulama
HTTP 1.1 istek ayrıntıları verilmiştir [işleri sorgulama][lnk-query]:

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

ContinuationToken yanıttan sağlanır.  

## <a name="jobs-properties"></a>İşlerini özellikleri
Özellikler ve sorgulanırken işleri veya iş sonuçları için kullanılabilir karşılık gelen açıklamaları listesi verilmiştir.

| Özellik | Açıklama |
| --- | --- |
| **iş kimliği** |Uygulama Kimliği iş için sağlanan. |
| **startTime** |Uygulama için iş başlangıç zamanı (ISO 8601) sağlanan. |
| **endTime** |IOT hub'ı zaman iş tamamlandı (ISO 8601) tarihi sağlanır. Yalnızca iş 'Tamamlandı' durumuna ulaştıktan sonra geçerli. |
| **türü** |İşlerini türleri: |
| **scheduledUpdateTwin**: İstenen özellikleri veya etiketleri kümesi güncelleştirmek için kullanılan bir işi. | |
| **scheduledDeviceMethod**: cihaz çiftlerini kümesi üzerinde bir aygıt yöntemi çağırmak için kullanılan bir işi. | |
| **durumu** |İşin geçerli durumu. Durum için olası değerler: |
| **Bekleyen** : Zamanlanmış ve iş hizmeti tarafından çekilmesi bekleniyor. | |
| **Zamanlanmış** : gelecekteki bir zamanı için zamanlanan. | |
| **çalışan** : şu anda etkin iş. | |
| **İptal** : işi iptal edildi. | |
| **başarısız** : işi başarısız oldu. | |
| **Tamamlanan** : işi tamamlandı. | |
| **deviceJobStatistics** |İş yürütme hakkındaki istatistiklerdir. |

**deviceJobStatistics** özellikleri.

| Özellik | Açıklama |
| --- | --- |
| **deviceJobStatistics.deviceCount** |İşte cihaz sayısı. |
| **deviceJobStatistics.failedCount** |İş başarısız olduğu cihazlar sayısı. |
| **deviceJobStatistics.succeededCount** |İş yeri başarılı cihaz sayısı. |
| **deviceJobStatistics.runningCount** |İşi çalışmakta olan aygıt sayısı. |
| **deviceJobStatistics.pendingCount** |İşi çalıştırmak için beklemede olan aygıt sayısı. |

### <a name="additional-reference-material"></a>Ek başvuru bilgileri
IOT Hub Geliştirici Kılavuzu'ndaki diğer başvuru konuları içerir:

* [IOT Hub uç noktaları] [ lnk-endpoints] her IOT hub'ı çalışma zamanı ve yönetim işlemleri için kullanıma sunan çeşitli uç noktaları açıklar.
* [Azaltma ve kotaları] [ lnk-quotas] IOT Hub hizmeti ve azaltma davranışı hizmetini kullandığınızda beklediğiniz uygulama kotaları açıklar.
* [Azure IOT cihaz ve hizmet SDK'ları] [ lnk-sdks] çeşitli dil SDK'ları listeler, IOT Hub ile etkileşim hem cihaz hem de hizmet uygulamaları geliştirirken kullanın.
* [IOT Hub cihaz çiftlerini, işler ve ileti yönlendirme için sorgu dili] [ lnk-query] IOT Hub'ından, cihaz çiftlerini ve işleri hakkında bilgi almak için kullanabileceğiniz IOT hub'ı sorgu dili açıklar.
* [IOT Hub MQTT Destek] [ lnk-devguide-mqtt] IOT hub'ı desteği hakkında daha fazla bilgi için MQTT Protokolü sağlar.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede açıklanan kavramları bazıları denemek istiyorsanız, aşağıdaki IOT hub'ı öğreticide ilgilenen olabilir:

* [Zamanlama ve yayın işleri][lnk-jobs-tutorial]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-jobs-tutorial]: iot-hub-node-node-schedule-jobs.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-devguide]: iot-hub-devguide-device-twins.md
