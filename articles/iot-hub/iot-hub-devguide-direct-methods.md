---
title: "Azure IOT hub'ı doğrudan yöntemlerini anlama | Microsoft Docs"
description: "Geliştirici Kılavuzu - kod cihazlarınızda service uygulamasından çağırmak için doğrudan yöntemlerini kullanın."
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
ms.openlocfilehash: 77e788a32097edbcb1cd4faaa45f35812eabd94a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a><span data-ttu-id="29695-103">Anlama ve IOT hub'ı doğrudan yöntemleri çağırma</span><span class="sxs-lookup"><span data-stu-id="29695-103">Understand and invoke direct methods from IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="29695-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="29695-104">Overview</span></span>
<span data-ttu-id="29695-105">IOT Hub, bulutta cihazlarda doğrudan yöntemlerini çağırmasına olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="29695-105">IoT Hub gives you ability to invoke direct methods on devices from the cloud.</span></span> <span data-ttu-id="29695-106">Başarılı veya başarısız hemen (bir kullanıcı tarafından belirtilen zaman aşımından sonra), bir HTTP çağrısıyla benzer bir cihaz istek-yanıt etkileşim doğrudan yöntemleri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="29695-106">Direct methods represent a request-reply interaction with a device similar to an HTTP call in that they succeed or fail immediately (after a user-specified timeout).</span></span> <span data-ttu-id="29695-107">Acil eylem seyri aygıt bir aygıtı (çevrimdışı SMS yöntem çağrısı daha pahalı olması) ise, bir SMS Uyandırma bir cihaza gönderme gibi yanıt verebilmesini olmasına bağlı olarak farklı olduğu senaryolar için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="29695-107">This is useful for scenarios where the course of immediate action is different depending on whether the device was able to respond, such as sending an SMS wake-up to a device if a device is offline (SMS being more expensive than a method call).</span></span>

<span data-ttu-id="29695-108">Her cihaz yöntemi tek bir cihazı hedefler.</span><span class="sxs-lookup"><span data-stu-id="29695-108">Each device method targets a single device.</span></span> <span data-ttu-id="29695-109">[İşlerini] [ lnk-devguide-jobs] doğrudan yöntemlerini birden çok aygıta çağırmak için bir yol sağlar ve zamanlama yöntem çağırma bağlantısı kesilmiş aygıtları için.</span><span class="sxs-lookup"><span data-stu-id="29695-109">[Jobs][lnk-devguide-jobs] provide a way to invoke direct methods on multiple devices, and schedule method invocation for disconnected devices.</span></span>

<span data-ttu-id="29695-110">Herkesle **service bağlanma** IOT Hub üzerindeki izinleri bir aygıtta bir yöntemi çağırma.</span><span class="sxs-lookup"><span data-stu-id="29695-110">Anyone with **service connect** permissions on IoT Hub may invoke a method on a device.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="29695-111">Kullanılması gereken durumlar</span><span class="sxs-lookup"><span data-stu-id="29695-111">When to use</span></span>
<span data-ttu-id="29695-112">Doğrudan yöntemleri istek-yanıt desenler izleyen ve örneğin fan üzerinde etkinleştirmek aygıtın genellikle etkileşimli denetimini kendi sonucunun hemen onay gerektiren iletişimleri için yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="29695-112">Direct methods follow a request-response pattern and are meant for communications that require immediate confirmation of their result, usually interactive control of the device, for example to turn on a fan.</span></span>

<span data-ttu-id="29695-113">Başvurmak [bulut-cihaz iletişimi Kılavuzu] [ lnk-c2d-guidance] istenen özelliklerini kullanarak arasında emin değilseniz, yöntemler veya Bulut-cihaz iletilerini doğrudan.</span><span class="sxs-lookup"><span data-stu-id="29695-113">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="method-lifecycle"></a><span data-ttu-id="29695-114">Yöntem yaşam döngüsü</span><span class="sxs-lookup"><span data-stu-id="29695-114">Method lifecycle</span></span>
<span data-ttu-id="29695-115">Doğrudan yöntemleri cihazda uygulanır ve doğru örneği oluşturmak için yöntem yükte sıfır veya daha fazla girdi gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="29695-115">Direct methods are implemented on the device and may require zero or more inputs in the method payload to correctly instantiate.</span></span> <span data-ttu-id="29695-116">Bir hizmet dönük URI üzerinden doğrudan bir yöntemi çağırma (`{iot hub}/twins/{device id}/methods/`).</span><span class="sxs-lookup"><span data-stu-id="29695-116">You invoke a direct method through a service-facing URI (`{iot hub}/twins/{device id}/methods/`).</span></span> <span data-ttu-id="29695-117">Bir aygıt bir aygıta özgü MQTT konu aracılığıyla doğrudan yöntemleri alır (`$iothub/methods/POST/{method name}/`).</span><span class="sxs-lookup"><span data-stu-id="29695-117">A device receives direct methods through a device-specific MQTT topic (`$iothub/methods/POST/{method name}/`).</span></span> <span data-ttu-id="29695-118">Doğrudan yöntemleri ek cihaz tarafındaki ağ protokollerini temel gelecekte destekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="29695-118">We may support direct methods on additional device-side networking protocols in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="29695-119">Bir cihazda doğrudan bir yöntemini çağırdığınızda, özellik adları ve değerleri yalnızca US-ASCII yazdırılabilir içerebilir herhangi aşağıdaki kümesindeki dışında alfasayısal: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="29695-119">When you invoke a direct method on a device, property names and values can only contain US-ASCII printable alphanumeric, except any in the following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

<span data-ttu-id="29695-120">Zaman uyumlu yöntemleri ve ya da başarılı doğrudan veya zaman aşımı süresinden sonra başarısız (varsayılan: 30 saniye, 3600 saniye olarak ayarlanabilir kurma).</span><span class="sxs-lookup"><span data-stu-id="29695-120">Direct methods are synchronous and either succeed or fail after the timeout period (default: 30 seconds, settable up to 3600 seconds).</span></span> <span data-ttu-id="29695-121">Doğrudan yöntemler, bir Phone ışığı kapatma gibi çevrimiçi ve alıcı komutları, cihaz, yalnızca ve yalnızca, görev yapması için bir aygıt istediğiniz etkileşimli senaryolarda kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="29695-121">Direct methods are useful in interactive scenarios where you want a device to act if and only if the device is online and receiving commands, such as turning on a light from a phone.</span></span> <span data-ttu-id="29695-122">Bu senaryolarda, bulut hizmeti sonucuna mümkün olan en kısa sürede hareket etmesini sağlamak bir hemen başarı veya başarısızlık görmek istediğinizi açıklayın.</span><span class="sxs-lookup"><span data-stu-id="29695-122">In these scenarios, you want to see an immediate success or failure so the cloud service can act on the result as soon as possible.</span></span> <span data-ttu-id="29695-123">Cihaz bazı ileti gövdesi yöntemi sonucunda döndürebilir ancak yöntemi bunu yapmak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="29695-123">The device may return some message body as a result of the method, but it isn't required for the method to do so.</span></span> <span data-ttu-id="29695-124">Garanti sıralama üzerinde veya tüm eşzamanlılık semantiği yöntem çağrılarını üzerinde yok.</span><span class="sxs-lookup"><span data-stu-id="29695-124">There is no guarantee on ordering or any concurrency semantics on method calls.</span></span>

<span data-ttu-id="29695-125">Doğrudan yöntemini yalnızca HTTP bulut taraftaki ve yalnızca MQTT aygıt taraftaki.</span><span class="sxs-lookup"><span data-stu-id="29695-125">Direct method are HTTP-only from the cloud side, and MQTT-only from the device side.</span></span>

<span data-ttu-id="29695-126">Yöntem istekleri ve yanıtları için yükü, bir JSON belgesi en fazla 8 KB ' dir.</span><span class="sxs-lookup"><span data-stu-id="29695-126">The payload for method requests and responses is a JSON document up to 8KB.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="29695-127">Başvuru konuları:</span><span class="sxs-lookup"><span data-stu-id="29695-127">Reference topics:</span></span>
<span data-ttu-id="29695-128">Aşağıdaki başvuru konuları doğrudan yöntemler kullanma hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="29695-128">The following reference topics provide you with more information about using direct methods.</span></span>

## <a name="invoke-a-direct-method-from-a-back-end-app"></a><span data-ttu-id="29695-129">Bir arka uç uygulamasından doğrudan bir yöntem çağırma</span><span class="sxs-lookup"><span data-stu-id="29695-129">Invoke a direct method from a back-end app</span></span>
### <a name="method-invocation"></a><span data-ttu-id="29695-130">Yöntem çağırma</span><span class="sxs-lookup"><span data-stu-id="29695-130">Method invocation</span></span>
<span data-ttu-id="29695-131">Bir cihazda doğrudan yöntem çağrılarını oluşturan HTTP çağrıları vardır:</span><span class="sxs-lookup"><span data-stu-id="29695-131">Direct method invocations on a device are HTTP calls which comprise:</span></span>

* <span data-ttu-id="29695-132">*URI* aygıta belirli (`{iot hub}/twins/{device id}/methods/`)</span><span class="sxs-lookup"><span data-stu-id="29695-132">The *URI* specific to the device (`{iot hub}/twins/{device id}/methods/`)</span></span>
* <span data-ttu-id="29695-133">POST *yöntemi*</span><span class="sxs-lookup"><span data-stu-id="29695-133">The POST *method*</span></span>
* <span data-ttu-id="29695-134">*Üstbilgileri* yetkilendirme içeren, istek kimliği, içerik türü ve içerik kodlaması</span><span class="sxs-lookup"><span data-stu-id="29695-134">*Headers* which contain the authorization, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="29695-135">Saydam JSON *gövde* şu biçimde:</span><span class="sxs-lookup"><span data-stu-id="29695-135">A transparent JSON *body* in the following format:</span></span>

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

<span data-ttu-id="29695-136">Zaman aşımı saniye cinsindendir.</span><span class="sxs-lookup"><span data-stu-id="29695-136">Timeout is in seconds.</span></span> <span data-ttu-id="29695-137">Zaman aşımı ayarlanmamışsa 30 saniye olarak varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="29695-137">If timeout is not set, it defaults to 30 seconds.</span></span>

### <a name="response"></a><span data-ttu-id="29695-138">Yanıt</span><span class="sxs-lookup"><span data-stu-id="29695-138">Response</span></span>
<span data-ttu-id="29695-139">Arka uç uygulama içeren bir yanıt alır:</span><span class="sxs-lookup"><span data-stu-id="29695-139">The back-end app receives a response which comprises:</span></span>

* <span data-ttu-id="29695-140">*HTTP durum kodu*, IOT Hub'ından gelen hatalara kullanıldığı, 404 hatası cihazlar için şu anda da dahil olmak üzere bağlı</span><span class="sxs-lookup"><span data-stu-id="29695-140">*HTTP status code*, which is used for errors coming from the IoT Hub, including a 404 error for devices not currently connected</span></span>
* <span data-ttu-id="29695-141">*Üstbilgileri* ETag içeren, istek kimliği, içerik türü ve içerik kodlaması</span><span class="sxs-lookup"><span data-stu-id="29695-141">*Headers* which contain the ETag, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="29695-142">JSON *gövde* şu biçimde:</span><span class="sxs-lookup"><span data-stu-id="29695-142">A JSON *body* in the following format:</span></span>

```
{
    "status" : 201,
    "payload" : {...}
}
```

   <span data-ttu-id="29695-143">Her ikisi de `status` ve `body` cihaz tarafından sağlanan ve cihazın kendi durum kodu ve/veya açıklama ile yanıtlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="29695-143">Both `status` and `body` are provided by the device and used to respond with the device's own status code and/or description.</span></span>

## <a name="handle-a-direct-method-on-a-device"></a><span data-ttu-id="29695-144">Bir cihazda doğrudan bir yöntem işleme</span><span class="sxs-lookup"><span data-stu-id="29695-144">Handle a direct method on a device</span></span>
### <a name="method-invocation"></a><span data-ttu-id="29695-145">Yöntem çağırma</span><span class="sxs-lookup"><span data-stu-id="29695-145">Method invocation</span></span>
<span data-ttu-id="29695-146">Cihazlar, MQTT konusunda doğrudan yöntem isteği alır:`$iothub/methods/POST/{method name}/?$rid={request id}`</span><span class="sxs-lookup"><span data-stu-id="29695-146">Devices receive direct method requests on the MQTT topic: `$iothub/methods/POST/{method name}/?$rid={request id}`</span></span>

<span data-ttu-id="29695-147">Cihaz alan gövdesi aşağıdaki biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="29695-147">The body which the device receives is in the following format:</span></span>

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

<span data-ttu-id="29695-148">Yöntemi, QoS 0 isteklerdir.</span><span class="sxs-lookup"><span data-stu-id="29695-148">Method requests are QoS 0.</span></span>

### <a name="response"></a><span data-ttu-id="29695-149">Yanıt</span><span class="sxs-lookup"><span data-stu-id="29695-149">Response</span></span>
<span data-ttu-id="29695-150">Cihaz yanıtlarını gönderir `$iothub/methods/res/{status}/?$rid={request id}`, burada:</span><span class="sxs-lookup"><span data-stu-id="29695-150">The device sends responses to `$iothub/methods/res/{status}/?$rid={request id}`, where:</span></span>

* <span data-ttu-id="29695-151">`status` Yöntemi yürütme aygıt tarafından sağlanan durumunu bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="29695-151">The `status` property is the device-supplied status of method execution.</span></span>
* <span data-ttu-id="29695-152">`$rid` IOT Hub'ından alınan yöntemi çağırma isteği Kimliğinden bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="29695-152">The `$rid` property is the request ID from the method invocation received from IoT Hub.</span></span>

<span data-ttu-id="29695-153">Gövde aygıt tarafından ayarlanır ve herhangi bir durum olabilir.</span><span class="sxs-lookup"><span data-stu-id="29695-153">The body is set by the device and can be any status.</span></span>

## <a name="additional-reference-material"></a><span data-ttu-id="29695-154">Ek başvuru bilgileri</span><span class="sxs-lookup"><span data-stu-id="29695-154">Additional reference material</span></span>
<span data-ttu-id="29695-155">IOT Hub Geliştirici Kılavuzu'ndaki diğer başvuru konuları içerir:</span><span class="sxs-lookup"><span data-stu-id="29695-155">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="29695-156">[IOT Hub uç noktaları] [ lnk-endpoints] her IOT hub'ı çalışma zamanı ve yönetim işlemleri için kullanıma sunan çeşitli uç noktaları açıklar.</span><span class="sxs-lookup"><span data-stu-id="29695-156">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="29695-157">[Azaltma ve kotaları] [ lnk-quotas] IOT Hub hizmeti ve azaltma davranışı hizmetini kullandığınızda beklediğiniz uygulama kotaları açıklar.</span><span class="sxs-lookup"><span data-stu-id="29695-157">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="29695-158">[Azure IOT cihaz ve hizmet SDK'ları] [ lnk-sdks] çeşitli dil IOT Hub ile etkileşim hem cihaz hem de hizmet uygulamaları geliştirirken kullanabilir SDK'ları listeler.</span><span class="sxs-lookup"><span data-stu-id="29695-158">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="29695-159">[IOT Hub cihaz çiftlerini, işler ve ileti yönlendirme için sorgu dili] [ lnk-query] IOT Hub'ından, cihaz çiftlerini ve işleri hakkında bilgi almak için kullanabileceğiniz IOT hub'ı sorgu dili açıklar.</span><span class="sxs-lookup"><span data-stu-id="29695-159">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="29695-160">[IOT Hub MQTT Destek] [ lnk-devguide-mqtt] IOT hub'ı desteği hakkında daha fazla bilgi için MQTT Protokolü sağlar.</span><span class="sxs-lookup"><span data-stu-id="29695-160">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29695-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="29695-161">Next steps</span></span>
<span data-ttu-id="29695-162">Doğrudan yöntemlerini kullanmayı öğrendiniz artık aşağıdaki IOT Hub Geliştirici Kılavuzu konusundaki ilgi olabilir:</span><span class="sxs-lookup"><span data-stu-id="29695-162">Now you have learned how to use direct methods, you may be interested in the following IoT Hub developer guide topic:</span></span>

* <span data-ttu-id="29695-163">[Birden çok aygıta işleri zamanla][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="29695-163">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="29695-164">Bu makalede açıklanan kavramları bazıları denemek istiyorsanız, aşağıdaki IOT hub'ı öğreticide ilgilenen olabilir:</span><span class="sxs-lookup"><span data-stu-id="29695-164">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="29695-165">[Doğrudan yöntemleri kullanın][lnk-methods-tutorial]</span><span class="sxs-lookup"><span data-stu-id="29695-165">[Use direct methods][lnk-methods-tutorial]</span></span>

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
