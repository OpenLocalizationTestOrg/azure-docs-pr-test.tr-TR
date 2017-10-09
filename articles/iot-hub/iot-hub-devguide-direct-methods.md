---
title: "Azure IOT Hub aaaUnderstand doğrudan yöntemleri | Microsoft Docs"
description: "Geliştirici Kılavuzu - cihazlarınızda service uygulamasından doğrudan yöntemleri tooinvoke kod kullanın."
services: iot-hub
documentationcenter: .net
author: nberdy
manager: timlt
editor: 
ms.assetid: 9f0535f1-02e6-467a-9fc4-c0950702102d
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d15d44a0c3e1d1cda1669c1ed011c2f932e3d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a><span data-ttu-id="868fa-103">Anlama ve IOT hub'ı doğrudan yöntemleri çağırma</span><span class="sxs-lookup"><span data-stu-id="868fa-103">Understand and invoke direct methods from IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="868fa-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="868fa-104">Overview</span></span>
<span data-ttu-id="868fa-105">IOT hub'ı hello buluta cihazlarda özelliği tooinvoke doğrudan yöntemleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="868fa-105">IoT Hub gives you ability tooinvoke direct methods on devices from hello cloud.</span></span> <span data-ttu-id="868fa-106">Doğrudan yöntemleri HTTP çağrı başarılı veya başarısız hemen (bir kullanıcı tarafından belirtilen zaman aşımından sonra), bir cihaz benzer tooan istek-yanıt etkileşim temsil eder.</span><span class="sxs-lookup"><span data-stu-id="868fa-106">Direct methods represent a request-reply interaction with a device similar tooan HTTP call in that they succeed or fail immediately (after a user-specified timeout).</span></span> <span data-ttu-id="868fa-107">Acil eylem hello seyri hello aygıt bir aygıtı (çevrimdışı SMS yöntem çağrısı daha pahalı olması) ise bir SMS Uyandırma tooa aygıt gönderme gibi mümkün toorespond olmasına bağlı olarak farklı olduğu senaryolar için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="868fa-107">This is useful for scenarios where hello course of immediate action is different depending on whether hello device was able toorespond, such as sending an SMS wake-up tooa device if a device is offline (SMS being more expensive than a method call).</span></span>

<span data-ttu-id="868fa-108">Her cihaz yöntemi tek bir cihazı hedefler.</span><span class="sxs-lookup"><span data-stu-id="868fa-108">Each device method targets a single device.</span></span> <span data-ttu-id="868fa-109">[İşlerini] [ lnk-devguide-jobs] şekilde tooinvoke birden fazla cihazda doğrudan yöntemleri sağlar ve zamanlama yöntem çağırma bağlantısı kesilmiş aygıtları için.</span><span class="sxs-lookup"><span data-stu-id="868fa-109">[Jobs][lnk-devguide-jobs] provide a way tooinvoke direct methods on multiple devices, and schedule method invocation for disconnected devices.</span></span>

<span data-ttu-id="868fa-110">Herkesle **service bağlanma** IOT Hub üzerindeki izinleri bir aygıtta bir yöntemi çağırma.</span><span class="sxs-lookup"><span data-stu-id="868fa-110">Anyone with **service connect** permissions on IoT Hub may invoke a method on a device.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="868fa-111">Zaman toouse</span><span class="sxs-lookup"><span data-stu-id="868fa-111">When toouse</span></span>
<span data-ttu-id="868fa-112">Doğrudan yöntemleri bir istek-yanıt desen izleyin ve kendi sonucunun hello aygıtın, örneğin tooturn fan üzerinde genellikle etkileşimli denetimini hemen onay gerektiren iletişimleri için yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="868fa-112">Direct methods follow a request-response pattern and are meant for communications that require immediate confirmation of their result, usually interactive control of hello device, for example tooturn on a fan.</span></span>

<span data-ttu-id="868fa-113">Çok başvuran[bulut-cihaz iletişimi Kılavuzu] [ lnk-c2d-guidance] istenen özelliklerini kullanarak arasında emin değilseniz, yöntemler veya Bulut-cihaz iletilerini doğrudan.</span><span class="sxs-lookup"><span data-stu-id="868fa-113">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="method-lifecycle"></a><span data-ttu-id="868fa-114">Yöntem yaşam döngüsü</span><span class="sxs-lookup"><span data-stu-id="868fa-114">Method lifecycle</span></span>
<span data-ttu-id="868fa-115">Doğrudan yöntemleri hello aygıtta uygulanır ve sıfır gerektirebilir veya hello yöntemi yükü toocorrectly içinde daha fazla giriş örneği.</span><span class="sxs-lookup"><span data-stu-id="868fa-115">Direct methods are implemented on hello device and may require zero or more inputs in hello method payload toocorrectly instantiate.</span></span> <span data-ttu-id="868fa-116">Bir hizmet dönük URI üzerinden doğrudan bir yöntemi çağırma (`{iot hub}/twins/{device id}/methods/`).</span><span class="sxs-lookup"><span data-stu-id="868fa-116">You invoke a direct method through a service-facing URI (`{iot hub}/twins/{device id}/methods/`).</span></span> <span data-ttu-id="868fa-117">Bir aygıt bir aygıta özgü MQTT konu aracılığıyla doğrudan yöntemleri alır (`$iothub/methods/POST/{method name}/`).</span><span class="sxs-lookup"><span data-stu-id="868fa-117">A device receives direct methods through a device-specific MQTT topic (`$iothub/methods/POST/{method name}/`).</span></span> <span data-ttu-id="868fa-118">Doğrudan yöntemleri protokollerine ek cihaz tarafındaki ağ hello gelecekteki destekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="868fa-118">We may support direct methods on additional device-side networking protocols in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="868fa-119">Bir cihazda doğrudan bir yöntemini çağırdığınızda, özellik adları ve değerleri yalnızca US-ASCII yazdırılabilir içerebilir kümesi aşağıdaki hello birinde dışında alfasayısal: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="868fa-119">When you invoke a direct method on a device, property names and values can only contain US-ASCII printable alphanumeric, except any in hello following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

<span data-ttu-id="868fa-120">Doğrudan yöntemleri zaman uyumlu ve ya da başarılı veya başarısız hello zaman aşımı süresinden sonra (varsayılan: 30 saniye, too3600 saniyeleri ayarlanabilir).</span><span class="sxs-lookup"><span data-stu-id="868fa-120">Direct methods are synchronous and either succeed or fail after hello timeout period (default: 30 seconds, settable up too3600 seconds).</span></span> <span data-ttu-id="868fa-121">Doğrudan yöntemler, bir Phone ışığı kapatma gibi çevrimiçi ve alıcı komutları hello aygıttır ve yalnızca, bir aygıt tooact istediğiniz etkileşimli senaryolarda kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="868fa-121">Direct methods are useful in interactive scenarios where you want a device tooact if and only if hello device is online and receiving commands, such as turning on a light from a phone.</span></span> <span data-ttu-id="868fa-122">Merhaba bulut hizmeti hello sonucuna mümkün olan en kısa sürede hareket etmesini sağlamak bu senaryolarda, toosee bir hemen başarı veya başarısızlık istiyor.</span><span class="sxs-lookup"><span data-stu-id="868fa-122">In these scenarios, you want toosee an immediate success or failure so hello cloud service can act on hello result as soon as possible.</span></span> <span data-ttu-id="868fa-123">Merhaba aygıt hello yöntemi sonucunda bazı ileti gövdesi döndürebilir ancak hello yöntemi toodo için gerekli değildir şekilde.</span><span class="sxs-lookup"><span data-stu-id="868fa-123">hello device may return some message body as a result of hello method, but it isn't required for hello method toodo so.</span></span> <span data-ttu-id="868fa-124">Garanti sıralama üzerinde veya tüm eşzamanlılık semantiği yöntem çağrılarını üzerinde yok.</span><span class="sxs-lookup"><span data-stu-id="868fa-124">There is no guarantee on ordering or any concurrency semantics on method calls.</span></span>

<span data-ttu-id="868fa-125">Doğrudan yöntemini yalnızca HTTP hello bulut taraftaki ve yalnızca MQTT hello aygıt taraftaki.</span><span class="sxs-lookup"><span data-stu-id="868fa-125">Direct method are HTTP-only from hello cloud side, and MQTT-only from hello device side.</span></span>

<span data-ttu-id="868fa-126">yöntem istekleri ve yanıtları için Hello yükü too8KB yukarı JSON belgedir.</span><span class="sxs-lookup"><span data-stu-id="868fa-126">hello payload for method requests and responses is a JSON document up too8KB.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="868fa-127">Başvuru konuları:</span><span class="sxs-lookup"><span data-stu-id="868fa-127">Reference topics:</span></span>
<span data-ttu-id="868fa-128">Merhaba aşağıdaki başvuru konuları doğrudan yöntemler kullanma hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="868fa-128">hello following reference topics provide you with more information about using direct methods.</span></span>

## <a name="invoke-a-direct-method-from-a-back-end-app"></a><span data-ttu-id="868fa-129">Bir arka uç uygulamasından doğrudan bir yöntem çağırma</span><span class="sxs-lookup"><span data-stu-id="868fa-129">Invoke a direct method from a back-end app</span></span>
### <a name="method-invocation"></a><span data-ttu-id="868fa-130">Yöntem çağırma</span><span class="sxs-lookup"><span data-stu-id="868fa-130">Method invocation</span></span>
<span data-ttu-id="868fa-131">Bir cihazda doğrudan yöntem çağrılarını oluşturan HTTP çağrıları vardır:</span><span class="sxs-lookup"><span data-stu-id="868fa-131">Direct method invocations on a device are HTTP calls which comprise:</span></span>

* <span data-ttu-id="868fa-132">Merhaba *URI* belirli toohello aygıt (`{iot hub}/twins/{device id}/methods/`)</span><span class="sxs-lookup"><span data-stu-id="868fa-132">hello *URI* specific toohello device (`{iot hub}/twins/{device id}/methods/`)</span></span>
* <span data-ttu-id="868fa-133">Merhaba POST *yöntemi*</span><span class="sxs-lookup"><span data-stu-id="868fa-133">hello POST *method*</span></span>
* <span data-ttu-id="868fa-134">*Üstbilgileri* hello yetkilendirme içeren, istek kimliği, içerik türü ve içerik kodlaması</span><span class="sxs-lookup"><span data-stu-id="868fa-134">*Headers* which contain hello authorization, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="868fa-135">Saydam JSON *gövde* biçimini izleyen hello içinde:</span><span class="sxs-lookup"><span data-stu-id="868fa-135">A transparent JSON *body* in hello following format:</span></span>

```
{
    "methodName": "reboot",
    "responseTimeoutInSeconds": 200,
    "payload": {
        "input1": "someInput",
        "input2": "anotherInput"
    }
}
```

<span data-ttu-id="868fa-136">Zaman aşımı saniye cinsindendir.</span><span class="sxs-lookup"><span data-stu-id="868fa-136">Timeout is in seconds.</span></span> <span data-ttu-id="868fa-137">Zaman aşımı ayarlanmamışsa too30 varsayılan olarak saniye.</span><span class="sxs-lookup"><span data-stu-id="868fa-137">If timeout is not set, it defaults too30 seconds.</span></span>

### <a name="response"></a><span data-ttu-id="868fa-138">Yanıt</span><span class="sxs-lookup"><span data-stu-id="868fa-138">Response</span></span>
<span data-ttu-id="868fa-139">Merhaba arka uç uygulama içeren bir yanıt alır:</span><span class="sxs-lookup"><span data-stu-id="868fa-139">hello back-end app receives a response which comprises:</span></span>

* <span data-ttu-id="868fa-140">*HTTP durum kodu*, IOT hub'ı hello gelen hatalara kullanıldığı, 404 hatası cihazlar için şu anda da dahil olmak üzere bağlı</span><span class="sxs-lookup"><span data-stu-id="868fa-140">*HTTP status code*, which is used for errors coming from hello IoT Hub, including a 404 error for devices not currently connected</span></span>
* <span data-ttu-id="868fa-141">*Üstbilgileri* hello ETag içeren, istek kimliği, içerik türü ve içerik kodlaması</span><span class="sxs-lookup"><span data-stu-id="868fa-141">*Headers* which contain hello ETag, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="868fa-142">JSON *gövde* biçimini izleyen hello içinde:</span><span class="sxs-lookup"><span data-stu-id="868fa-142">A JSON *body* in hello following format:</span></span>

```
{
    "status" : 201,
    "payload" : {...}
}
```

   <span data-ttu-id="868fa-143">Her ikisi de `status` ve `body` hello aygıt tarafından sağlanan ve toorespond hello cihazın kendi durum kodu ve/veya açıklama ile kullanılır.</span><span class="sxs-lookup"><span data-stu-id="868fa-143">Both `status` and `body` are provided by hello device and used toorespond with hello device's own status code and/or description.</span></span>

## <a name="handle-a-direct-method-on-a-device"></a><span data-ttu-id="868fa-144">Bir cihazda doğrudan bir yöntem işleme</span><span class="sxs-lookup"><span data-stu-id="868fa-144">Handle a direct method on a device</span></span>
### <a name="method-invocation"></a><span data-ttu-id="868fa-145">Yöntem çağırma</span><span class="sxs-lookup"><span data-stu-id="868fa-145">Method invocation</span></span>
<span data-ttu-id="868fa-146">Cihazlar hello MQTT konuda doğrudan yöntem isteği alır:`$iothub/methods/POST/{method name}/?$rid={request id}`</span><span class="sxs-lookup"><span data-stu-id="868fa-146">Devices receive direct method requests on hello MQTT topic: `$iothub/methods/POST/{method name}/?$rid={request id}`</span></span>

<span data-ttu-id="868fa-147">hangi hello aygıtından alan hello gövde biçimi aşağıdaki hello şöyledir:</span><span class="sxs-lookup"><span data-stu-id="868fa-147">hello body which hello device receives is in hello following format:</span></span>

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

<span data-ttu-id="868fa-148">Yöntemi, QoS 0 isteklerdir.</span><span class="sxs-lookup"><span data-stu-id="868fa-148">Method requests are QoS 0.</span></span>

### <a name="response"></a><span data-ttu-id="868fa-149">Yanıt</span><span class="sxs-lookup"><span data-stu-id="868fa-149">Response</span></span>
<span data-ttu-id="868fa-150">Merhaba cihaz gönderir yanıtları çok`$iothub/methods/res/{status}/?$rid={request id}`, burada:</span><span class="sxs-lookup"><span data-stu-id="868fa-150">hello device sends responses too`$iothub/methods/res/{status}/?$rid={request id}`, where:</span></span>

* <span data-ttu-id="868fa-151">Merhaba `status` hello aygıt tarafından sağlanan durumunu yöntemi yürütme bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="868fa-151">hello `status` property is hello device-supplied status of method execution.</span></span>
* <span data-ttu-id="868fa-152">Merhaba `$rid` hello isteği IOT Hub'ından alınan hello yöntemi çağırma Kimliğinden bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="868fa-152">hello `$rid` property is hello request ID from hello method invocation received from IoT Hub.</span></span>

<span data-ttu-id="868fa-153">Merhaba gövde hello aygıt tarafından ayarlanır ve herhangi bir durum olabilir.</span><span class="sxs-lookup"><span data-stu-id="868fa-153">hello body is set by hello device and can be any status.</span></span>

## <a name="additional-reference-material"></a><span data-ttu-id="868fa-154">Ek başvuru bilgileri</span><span class="sxs-lookup"><span data-stu-id="868fa-154">Additional reference material</span></span>
<span data-ttu-id="868fa-155">Merhaba IOT Hub Geliştirici Kılavuzu diğer başvuru konularına şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="868fa-155">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="868fa-156">[IOT Hub uç noktaları] [ lnk-endpoints] açıklar çalışma zamanı ve yönetim işlemleri için her IOT hub'ı sunan çeşitli uç noktaları hello.</span><span class="sxs-lookup"><span data-stu-id="868fa-156">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="868fa-157">[Azaltma ve kotaları] [ lnk-quotas] toohello IOT Hub hizmetine uygulamak ve hello hizmetini kullandığınızda azaltma davranışı tooexpect hello hello kotaları açıklar.</span><span class="sxs-lookup"><span data-stu-id="868fa-157">[Throttling and quotas][lnk-quotas] describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="868fa-158">[Azure IOT cihaz ve hizmet SDK'ları] [ lnk-sdks] listeleri hello çeşitli dil SDK'ları, IOT Hub ile etkileşim hem cihaz hem de hizmet uygulamaları geliştirdiğinizde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="868fa-158">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="868fa-159">[IOT Hub cihaz çiftlerini, işler ve ileti yönlendirme için sorgu dili] [ lnk-query] hello tooretrieve bilgilerini IOT hub'dan cihaz çiftlerini ve işleri kullanabileceğiniz IOT hub'ı sorgu dili açıklar.</span><span class="sxs-lookup"><span data-stu-id="868fa-159">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="868fa-160">[IOT Hub MQTT Destek] [ lnk-devguide-mqtt] hello MQTT protokolü için IOT hub'ı desteği hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="868fa-160">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="868fa-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="868fa-161">Next steps</span></span>
<span data-ttu-id="868fa-162">Şimdi nasıl toouse doğrudan yöntemleri, IOT Hub Geliştirici Kılavuzu konusundaki aşağıdaki hello ilgilenebilirsiniz öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="868fa-162">Now you have learned how toouse direct methods, you may be interested in hello following IoT Hub developer guide topic:</span></span>

* <span data-ttu-id="868fa-163">[Birden çok aygıta işleri zamanla][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="868fa-163">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="868fa-164">Bu makalede açıklanan hello kavramların bazıları çıkışı tootry isterseniz, IOT hub'ı öğreticiyi izleyerek hello ilgilenen olabilir:</span><span class="sxs-lookup"><span data-stu-id="868fa-164">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="868fa-165">[Doğrudan yöntemleri kullanın][lnk-methods-tutorial]</span><span class="sxs-lookup"><span data-stu-id="868fa-165">[Use direct methods][lnk-methods-tutorial]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-messages]: iot-hub-devguide-messaging.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
