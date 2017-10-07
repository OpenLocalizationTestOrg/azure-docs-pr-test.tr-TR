---
title: "aaaUnderstand Azure IOT Hub işleri | Microsoft Docs"
description: "Geliştirici Kılavuzu - birden çok aygıta işleri toorun zamanlama tooyour IOT hub'ı bağlı. İşler, etiketler ve istenen özelliklerini güncelleştirmek ve birden çok aygıta doğrudan yöntemleri çağırma."
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
ms.openlocfilehash: 8be134e6c379feae5087df8f562a74505c57afee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a>Birden fazla cihazda işleri zamanlama
## <a name="overview"></a>Genel Bakış
Önceki makaleleri tarafından açıklandığı gibi Azure IOT hub'ı birkaç yapı taşlarını sağlar ([cihaz çifti özellikleri ve etiketleri] [ lnk-twin-devguide] ve [doğrudan yöntemleri][lnk-dev-methods]).  Genellikle, arka uç uygulamalar aygıt Yöneticiler ve İşletmenleri tooupdate etkinleştirin ve IOT cihazları toplu ve zamanlanan saatte etkileşim.  İşlerini zamanlama zaman hello yürütme cihaz çifti güncelleştirmeleri ve bir cihaz kümesi karşı doğrudan yöntemlerin kapsüller.  Örneğin, bir işleç başlatmak ve iş tooreboot 43 ve 3 kat hello oluşturma işlemlerini kesintiye uğratan toohello olmayacaktır aynı anda oluşturmanın cihazlar izleyen bir arka uç uygulaması kullanırsınız.

### <a name="when-toouse"></a>Zaman toouse
Göz önünde bulundurun kullanarak, işlerin ne zaman: bir çözüm arka ucu gereksinimlerini tooschedule ve izleme herhangi bir cihaz kümesine etkinlikleri izleyerek hello ilerleme:

* İstenen özellikleri güncelleştirme
* Güncelleştirme etiketleri
* Doğrudan yöntemleri çağırma

## <a name="job-lifecycle"></a>İş yaşam döngüsü
İşlerini hello çözüm arka ucu tarafından başlatılan ve IOT Hub tarafından korunur.  Bir hizmet dönük URI ile bir işi başlatabilirsiniz (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) ve bir hizmet dönük URI aracılığıyla yürütülen bir işin ilerleme için sorgu (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).  Bir iş başlatıldıktan sonra işleri sorgulama çalışan işi hello arka uç uygulama toorefresh hello durumu sağlar.

> [!NOTE]
> Bir işi başlattığınızda özellik adları ve değerleri yalnızca US-ASCII yazdırılabilir içerebilir kümesi aşağıdaki hello birinde dışında alfasayısal: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.
> 
> 

## <a name="reference-topics"></a>Başvuru konuları:
başvuru konuları aşağıdaki hello işleri kullanma hakkında daha fazla bilgi sağlar.

## <a name="jobs-tooexecute-direct-methods"></a>İşlerini tooexecute doğrudan yöntemleri
Merhaba yürütmek hello HTTP 1.1 İstek Ayrıntıları aşağıdadır bir [doğrudan yöntemi] [ lnk-dev-methods] bir işi kullanarak cihazları bir dizi:

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
Merhaba sorgu koşulu da tek bir cihaz kimliği veya aygıt kimliklerinin bir listesi aşağıda gösterildiği gibi olabilir

**Örnekler**
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
[IOT Hub sorgu dili] [ lnk-query] IOT hub'ı sorgu dili ek ayrıntılı kapsar.

## <a name="jobs-tooupdate-device-twin-properties"></a>İşlerini tooupdate cihaz çifti özellikleri
Merhaba, bir iş kullanarak cihaz çifti özelliklerini güncelleştirmek için HTTP 1.1 hello İstek Ayrıntıları aşağıdadır:

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
Merhaba hello için HTTP 1.1 İstek Ayrıntıları aşağıdadır [işleri sorgulama][lnk-query]:

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

Merhaba continuationToken hello yanıttan sağlanır.  

## <a name="jobs-properties"></a>İşlerini özellikleri
Merhaba, özellikleri ve sorgulanırken işleri veya iş sonuçları için kullanılabilir karşılık gelen açıklamaları listesi aşağıdadır.

| Özellik | Açıklama |
| --- | --- |
| **iş kimliği** |Uygulama Kimliği hello işi için sağlanan. |
| **startTime** |Merhaba işi için sağlanan uygulama başlangıç saati (ISO 8601). |
| **endTime** |Merhaba işi tamamlandığında IOT hub'ı tarih (ISO 8601) için sağlanan. Yalnızca 'Tamamlandı' hello durumu hello iş ulaştıktan sonra geçerli. |
| **türü** |İşlerini türleri: |
| **scheduledUpdateTwin**: kullanılan iş tooupdate istenen özellikleri veya etiketleri kümesi. | |
| **scheduledDeviceMethod**: kullanılan iş tooinvoke bir dizi cihaz çiftlerini cihaz yöntemi. | |
| **durumu** |Merhaba işin geçerli durumu. Durum için olası değerler: |
| **Bekleyen** : Zamanlanmış ve bekleme toobe hello iş hizmeti tarafından toplanma. | |
| **Zamanlanmış** : hello gelecekteki bir süre için zamanlanan. | |
| **çalışan** : şu anda etkin iş. | |
| **İptal** : işi iptal edildi. | |
| **başarısız** : işi başarısız oldu. | |
| **Tamamlanan** : işi tamamlandı. | |
| **deviceJobStatistics** |Merhaba işin yürütme hakkındaki istatistiklerdir. |

**deviceJobStatistics** özellikleri.

| Özellik | Açıklama |
| --- | --- |
| **deviceJobStatistics.deviceCount** |Cihazların Merhaba işi sayısı. |
| **deviceJobStatistics.failedCount** |Merhaba iş başarısız olduğu cihazlar sayısı. |
| **deviceJobStatistics.succeededCount** |Burada hello iş başarılı cihaz sayısı. |
| **deviceJobStatistics.runningCount** |Merhaba işi çalışmakta olan aygıt sayısı. |
| **deviceJobStatistics.pendingCount** |Toorun hello işi olan aygıt sayısı. |

### <a name="additional-reference-material"></a>Ek başvuru bilgileri
Merhaba IOT Hub Geliştirici Kılavuzu diğer başvuru konularına şunları içerir:

* [IOT Hub uç noktaları] [ lnk-endpoints] açıklar çalışma zamanı ve yönetim işlemleri için her IOT hub'ı sunan çeşitli uç noktaları hello.
* [Azaltma ve kotaları] [ lnk-quotas] toohello IOT Hub hizmetine uygulamak ve hello hizmetini kullandığınızda azaltma davranışı tooexpect hello hello kotaları açıklar.
* [Azure IOT cihaz ve hizmet SDK'ları] [ lnk-sdks] listeleri hello çeşitli dil SDK'ları, IOT Hub ile etkileşim hem cihaz hem de hizmet uygulamaları geliştirirken kullanın.
* [IOT Hub cihaz çiftlerini, işler ve ileti yönlendirme için sorgu dili] [ lnk-query] hello tooretrieve bilgilerini IOT hub'dan cihaz çiftlerini ve işleri kullanabileceğiniz IOT hub'ı sorgu dili açıklar.
* [IOT Hub MQTT Destek] [ lnk-devguide-mqtt] hello MQTT protokolü için IOT hub'ı desteği hakkında daha fazla bilgi sağlar.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede açıklanan hello kavramların bazıları çıkışı tootry isterseniz, IOT hub'ı öğreticiyi izleyerek hello ilgilenen olabilir:

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
