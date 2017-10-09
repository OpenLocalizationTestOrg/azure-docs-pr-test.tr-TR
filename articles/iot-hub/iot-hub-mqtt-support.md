---
title: Azure IOT Hub MQTT destek aaaUnderstand | Microsoft Docs
description: "Geliştirici Kılavuzu - IOT Hub cihaz dönük kullanan uç noktasını tooan bağlanan cihazları MQTT Protokolü hello desteği. Hello Azure IOT cihaz SDK'ları yerleşik MQTT desteği hakkında bilgi içerir."
services: iot-hub
documentationcenter: .net
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 1d71c27c-b466-4a40-b95b-d6550cf85144
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e461687963138987acdf1f4e0e34c453744ea191
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="communicate-with-your-iot-hub-using-hello-mqtt-protocol"></a><span data-ttu-id="62947-104">Merhaba MQTT protokolünü kullanarak, IOT hub ile iletişim</span><span class="sxs-lookup"><span data-stu-id="62947-104">Communicate with your IoT hub using hello MQTT protocol</span></span>

<span data-ttu-id="62947-105">IOT hub'ı etkinleştirir aygıtları toocommunicate hello IOT Hub cihaz uç hello kullanarak ile [MQTT v3.1.1] [ lnk-mqtt-org] 8883 bağlantı noktası veya bağlantı noktası 443 üzerinden WebSocket protokolü üzerinden MQTT v3.1.1 protokolü.</span><span class="sxs-lookup"><span data-stu-id="62947-105">IoT Hub enables devices toocommunicate with hello IoT Hub device endpoints using hello [MQTT v3.1.1][lnk-mqtt-org] protocol on port 8883 or MQTT v3.1.1 over WebSocket protocol on port 443.</span></span> <span data-ttu-id="62947-106">IOT hub'ı TLS/SSL kullanılarak güvenlik altına tüm cihaz iletişimi toobe gerektirir (Bu nedenle, IOT hub'ı güvenli olmayan bağlantıları 1883 bağlantı noktası üzerinden olarak desteklemiyor).</span><span class="sxs-lookup"><span data-stu-id="62947-106">IoT Hub requires all device communication toobe secured using TLS/SSL (hence, IoT Hub doesn’t support non-secure connections over port 1883).</span></span>

## <a name="connecting-tooiot-hub"></a><span data-ttu-id="62947-107">TooIoT Hub bağlanma</span><span class="sxs-lookup"><span data-stu-id="62947-107">Connecting tooIoT Hub</span></span>

<span data-ttu-id="62947-108">Bir cihazı hello hello kitaplıklarında kullanarak ya da hello MQTT Protokolü tooconnect tooan IOT hub'ı kullanmak [Azure IOT SDK'ları] [ lnk-device-sdks] veya doğrudan hello MQTT protokolünü kullanarak.</span><span class="sxs-lookup"><span data-stu-id="62947-108">A device can use hello MQTT protocol tooconnect tooan IoT hub either by using hello libraries in hello [Azure IoT SDKs][lnk-device-sdks] or by using hello MQTT protocol directly.</span></span>

## <a name="using-hello-device-sdks"></a><span data-ttu-id="62947-109">Merhaba cihaz SDK'ları kullanma</span><span class="sxs-lookup"><span data-stu-id="62947-109">Using hello device SDKs</span></span>

<span data-ttu-id="62947-110">[Cihaz SDK'ları] [ lnk-device-sdks] Bu destek hello MQTT Protokolü Java, Node.js, C, C# ve Python için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="62947-110">[Device SDKs][lnk-device-sdks] that support hello MQTT protocol are available for Java, Node.js, C, C#, and Python.</span></span> <span data-ttu-id="62947-111">Merhaba cihaz SDK'ları hello standart IOT Hub bağlantı dizesi tooestablish bir bağlantı tooan IOT hub'ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="62947-111">hello device SDKs use hello standard IoT Hub connection string tooestablish a connection tooan IoT hub.</span></span> <span data-ttu-id="62947-112">toouse hello MQTT Protokolü hello istemci protokolü parametresi ayarlanmalıdır çok**MQTT**.</span><span class="sxs-lookup"><span data-stu-id="62947-112">toouse hello MQTT protocol, hello client protocol parameter must be set too**MQTT**.</span></span> <span data-ttu-id="62947-113">Varsayılan olarak, hello cihaz SDK'ları bağlamak tooan IOT Hub ile Merhaba **CleanSession** bayrağı ayarlanmış çok**0** ve **QoS 1** hello IOT hub ile ileti alışverişi için.</span><span class="sxs-lookup"><span data-stu-id="62947-113">By default, hello device SDKs connect tooan IoT Hub with hello **CleanSession** flag set too**0** and use **QoS 1** for message exchange with hello IoT hub.</span></span>

<span data-ttu-id="62947-114">Bir aygıt bağlı tooan IOT hub'ı olduğunda hello cihaz SDK'ları hello aygıt toosend iletileri tooand IOT hub'ından iletileri Al sağlayan yöntemler sağlar.</span><span class="sxs-lookup"><span data-stu-id="62947-114">When a device is connected tooan IoT hub, hello device SDKs provide methods that enable hello device toosend messages tooand receive messages from an IoT hub.</span></span>

<span data-ttu-id="62947-115">Her desteklenen dil ve hello parametresi toouse tooestablish bağlantı tooIoT Hub belirtir hello aşağıdaki tabloda bağlantıları toocode örnekleri içeren hello MQTT protokolünü kullanarak.</span><span class="sxs-lookup"><span data-stu-id="62947-115">hello following table contains links toocode samples for each supported language and specifies hello parameter toouse tooestablish a connection tooIoT Hub using hello MQTT protocol.</span></span>

| <span data-ttu-id="62947-116">Dil</span><span class="sxs-lookup"><span data-stu-id="62947-116">Language</span></span> | <span data-ttu-id="62947-117">Protokol parametresi</span><span class="sxs-lookup"><span data-stu-id="62947-117">Protocol parameter</span></span> |
| --- | --- |
| <span data-ttu-id="62947-118">[Node.js][lnk-sample-node]</span><span class="sxs-lookup"><span data-stu-id="62947-118">[Node.js][lnk-sample-node]</span></span> |<span data-ttu-id="62947-119">Azure-IOT-cihaz-mqtt</span><span class="sxs-lookup"><span data-stu-id="62947-119">azure-iot-device-mqtt</span></span> |
| <span data-ttu-id="62947-120">[Java][lnk-sample-java]</span><span class="sxs-lookup"><span data-stu-id="62947-120">[Java][lnk-sample-java]</span></span> |<span data-ttu-id="62947-121">IotHubClientProtocol.MQTT</span><span class="sxs-lookup"><span data-stu-id="62947-121">IotHubClientProtocol.MQTT</span></span> |
| <span data-ttu-id="62947-122">[C][lnk-sample-c]</span><span class="sxs-lookup"><span data-stu-id="62947-122">[C][lnk-sample-c]</span></span> |<span data-ttu-id="62947-123">MQTT_Protocol</span><span class="sxs-lookup"><span data-stu-id="62947-123">MQTT_Protocol</span></span> |
| <span data-ttu-id="62947-124">[C#][lnk-sample-csharp]</span><span class="sxs-lookup"><span data-stu-id="62947-124">[C#][lnk-sample-csharp]</span></span> |<span data-ttu-id="62947-125">TransportType.Mqtt</span><span class="sxs-lookup"><span data-stu-id="62947-125">TransportType.Mqtt</span></span> |
| <span data-ttu-id="62947-126">[Python][lnk-sample-python]</span><span class="sxs-lookup"><span data-stu-id="62947-126">[Python][lnk-sample-python]</span></span> |<span data-ttu-id="62947-127">IoTHubTransportProvider.MQTT</span><span class="sxs-lookup"><span data-stu-id="62947-127">IoTHubTransportProvider.MQTT</span></span> |

### <a name="migrating-a-device-app-from-amqp-toomqtt"></a><span data-ttu-id="62947-128">Cihaz uygulaması AMQP tooMQTT ' geçiş</span><span class="sxs-lookup"><span data-stu-id="62947-128">Migrating a device app from AMQP tooMQTT</span></span>

<span data-ttu-id="62947-129">Merhaba kullanıyorsanız [cihaz SDK'ları][lnk-device-sdks], AMQP kullanarak geçiş tooMQTT daha önce belirtildiği gibi hello Protokolü hello İstemci başlatması parametresinde değiştirilmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="62947-129">If you are using hello [device SDKs][lnk-device-sdks], switching from using AMQP tooMQTT requires changing hello protocol parameter in hello client initialization as stated previously.</span></span>

<span data-ttu-id="62947-130">Bunu yaparken aşağıdaki öğelerindeki emin toocheck hello olun:</span><span class="sxs-lookup"><span data-stu-id="62947-130">When doing so, make sure toocheck hello following items:</span></span>

* <span data-ttu-id="62947-131">MQTT hello bağlantıyı sonlandırır sırada AMQP birçok koşulları için hatalar döndürür.</span><span class="sxs-lookup"><span data-stu-id="62947-131">AMQP returns errors for many conditions, while MQTT terminates hello connection.</span></span> <span data-ttu-id="62947-132">Sonuç olarak, özel durum mantığı işleme bazı değişiklikler gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="62947-132">As a result your exception handling logic might require some changes.</span></span>
* <span data-ttu-id="62947-133">MQTT hello desteklemediği *Reddet* alırken işlemleri [bulut-cihaz iletilerini][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="62947-133">MQTT does not support hello *reject* operations when receiving [cloud-to-device messages][lnk-messaging].</span></span> <span data-ttu-id="62947-134">Arka uç uygulamanızı tooreceive hello aygıt uygulamasından bir yanıt gerekirse, kullanmayı [doğrudan yöntemleri][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="62947-134">If your back-end app needs tooreceive a response from hello device app, consider using [direct methods][lnk-methods].</span></span>

## <a name="using-hello-mqtt-protocol-directly"></a><span data-ttu-id="62947-135">Merhaba MQTT protokolü kullanarak doğrudan</span><span class="sxs-lookup"><span data-stu-id="62947-135">Using hello MQTT protocol directly</span></span>
<span data-ttu-id="62947-136">Bir aygıt hello cihaz SDK'ları kullanamıyorsanız, hala toohello ortak cihaz uç noktaları 8883 bağlantı noktasında hello MQTT protokolünü kullanarak bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="62947-136">If a device cannot use hello device SDKs, it can still connect toohello public device endpoints using hello MQTT protocol on port 8883.</span></span> <span data-ttu-id="62947-137">Merhaba, **BAĞLAN** paket hello aygıt değerleri aşağıdaki hello kullanmalıdır:</span><span class="sxs-lookup"><span data-stu-id="62947-137">In hello **CONNECT** packet hello device should use hello following values:</span></span>

* <span data-ttu-id="62947-138">Hello için **ClientID** alanında, hello kullanın **DeviceID**.</span><span class="sxs-lookup"><span data-stu-id="62947-138">For hello **ClientId** field, use hello **deviceId**.</span></span>
* <span data-ttu-id="62947-139">Hello için **kullanıcıadı** alanında, kullanmak `{iothubhostname}/{device_id}/api-version=2016-11-14`, {iothubhostname} olan hello burada hello IOT hub'ın tam CName.</span><span class="sxs-lookup"><span data-stu-id="62947-139">For hello **Username** field, use `{iothubhostname}/{device_id}/api-version=2016-11-14`, where {iothubhostname} is hello full CName of hello IoT hub.</span></span>

    <span data-ttu-id="62947-140">Örneğin, hello IOT hub'ınızın adını ise **contoso.azure devices.net** ve Cihazınızı hello adı ise **MyDevice01**, hello tam **kullanıcıadı** alan içermelidir `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span><span class="sxs-lookup"><span data-stu-id="62947-140">For example, if hello name of your IoT hub is **contoso.azure-devices.net** and if hello name of your device is **MyDevice01**, hello full **Username** field should contain `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span></span>
* <span data-ttu-id="62947-141">Hello için **parola** alan, bir SAS belirteci kullanın.</span><span class="sxs-lookup"><span data-stu-id="62947-141">For hello **Password** field, use a SAS token.</span></span> <span data-ttu-id="62947-142">SAS belirteci hello Hello biçimi hello aynı hello HTTP ve AMQP protokolleri için:</span><span class="sxs-lookup"><span data-stu-id="62947-142">hello format of hello SAS token is hello same as for both hello HTTP and AMQP protocols:</span></span><br/><span data-ttu-id="62947-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span><span class="sxs-lookup"><span data-stu-id="62947-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span></span>

    <span data-ttu-id="62947-144">Hakkında daha fazla bilgi için toogenerate SAS belirteci hello aygıt bölümüne bakın [IOT Hub'ı kullanarak güvenlik belirteçleri][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="62947-144">For more information about how toogenerate SAS tokens, see hello device section of [Using IoT Hub security tokens][lnk-sas-tokens].</span></span>

    <span data-ttu-id="62947-145">Test ederken hello de kullanabilirsiniz [aygıt explorer] [ lnk-device-explorer] aracı tooquickly kendi koda kopyalayıp bir SAS belirteci oluştur:</span><span class="sxs-lookup"><span data-stu-id="62947-145">When testing, you can also use hello [device explorer][lnk-device-explorer] tool tooquickly generate a SAS token that you can copy and paste into your own code:</span></span>

  1. <span data-ttu-id="62947-146">Toohello Git **Yönetim** sekmesinde **aygıt Explorer**.</span><span class="sxs-lookup"><span data-stu-id="62947-146">Go toohello **Management** tab in **Device Explorer**.</span></span>
  2. <span data-ttu-id="62947-147">Tıklatın **SAS belirteci** (sağ üst).</span><span class="sxs-lookup"><span data-stu-id="62947-147">Click **SAS Token** (top right).</span></span>
  3. <span data-ttu-id="62947-148">Üzerinde **SASTokenForm**, aygıtınızı hello seçin **DeviceID** açılır.</span><span class="sxs-lookup"><span data-stu-id="62947-148">On **SASTokenForm**, select your device in hello **DeviceID** drop down.</span></span> <span data-ttu-id="62947-149">Ayarlama, **TTL**.</span><span class="sxs-lookup"><span data-stu-id="62947-149">Set your **TTL**.</span></span>
  4. <span data-ttu-id="62947-150">Tıklatın **Generate** toocreate belirtecinizi.</span><span class="sxs-lookup"><span data-stu-id="62947-150">Click **Generate** toocreate your token.</span></span>

     <span data-ttu-id="62947-151">Merhaba oluşturulan SAS belirteci bu yapısının: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="62947-151">hello SAS token that's generated has this structure: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

     <span data-ttu-id="62947-152">Merhaba Bu belirteci toouse hello olarak parçası **parola** MQTT kullanarak alan tooconnect olduğu: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="62947-152">hello part of this token toouse as hello **Password** field tooconnect using MQTT is: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

<span data-ttu-id="62947-153">İçin MQTT bağlanmak ve paketleri kesmek, IOT hub'ı sorunları olay hello olarak **işlemlerini izleme** kanal tootroubleshoot bağlantı sorunları yardımcı olabilecek ek bilgiler ile.</span><span class="sxs-lookup"><span data-stu-id="62947-153">For MQTT connect and disconnect packets, IoT Hub issues an event on hello **Operations Monitoring** channel with additional information that can help you tootroubleshoot connectivity issues.</span></span>

### <a name="sending-device-to-cloud-messages"></a><span data-ttu-id="62947-154">Cihaz bulut iletilerini gönderme</span><span class="sxs-lookup"><span data-stu-id="62947-154">Sending device-to-cloud messages</span></span>

<span data-ttu-id="62947-155">Başarılı bir bağlantı yaptıktan sonra bir cihaz iletileri tooIoT hub'ı kullanarak gönderebilirsiniz `devices/{device_id}/messages/events/` veya `devices/{device_id}/messages/events/{property_bag}` olarak bir **konu adı**.</span><span class="sxs-lookup"><span data-stu-id="62947-155">After making a successful connection, a device can send messages tooIoT Hub using `devices/{device_id}/messages/events/` or `devices/{device_id}/messages/events/{property_bag}` as a **Topic Name**.</span></span> <span data-ttu-id="62947-156">Merhaba `{property_bag}` öğesi Merhaba aygıt toosend iletileri url kodlanmış bir biçimde ek özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="62947-156">hello `{property_bag}` element enables hello device toosend messages with additional properties in a url-encoded format.</span></span> <span data-ttu-id="62947-157">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="62947-157">For example:</span></span>

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> <span data-ttu-id="62947-158">Bu `{property_bag}` öğesi kullanır hello sorgu dizeleri hello HTTP protokolü için olduğu gibi aynı kodlama.</span><span class="sxs-lookup"><span data-stu-id="62947-158">This `{property_bag}` element uses hello same encoding as for query strings in hello HTTP protocol.</span></span>
>
>

<span data-ttu-id="62947-159">Merhaba cihaz uygulaması de kullanabilir `devices/{device_id}/messages/events/{property_bag}` hello olarak **Will konu adı** toodefine *iletilerini* toobe bir telemetri iletisi olarak iletilir.</span><span class="sxs-lookup"><span data-stu-id="62947-159">hello device app can also use `devices/{device_id}/messages/events/{property_bag}` as hello **Will topic name** toodefine *Will messages* toobe forwarded as a telemetry message.</span></span>

- <span data-ttu-id="62947-160">IOT hub'ı QoS 2 iletileri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="62947-160">IoT Hub does not support QoS 2 messages.</span></span> <span data-ttu-id="62947-161">Cihaz uygulaması içeren bir ileti yayımlarsa **QoS 2**, IOT hub'ı hello ağ bağlantısı kapatır.</span><span class="sxs-lookup"><span data-stu-id="62947-161">If a device app publishes a message with **QoS 2**, IoT Hub closes hello network connection.</span></span>
- <span data-ttu-id="62947-162">IOT hub'ı tut iletileri kalmaz.</span><span class="sxs-lookup"><span data-stu-id="62947-162">IoT Hub does not persist Retain messages.</span></span> <span data-ttu-id="62947-163">Bir aygıt hello içeren bir ileti gönderirse **TUT** bayrağı ayarlanmış too1, IOT hub'ı ekler hello **x-opt-korumak** uygulama özelliği toohello iletisi.</span><span class="sxs-lookup"><span data-stu-id="62947-163">If a device sends a message with hello **RETAIN** flag set too1, IoT Hub adds hello **x-opt-retain** application property toohello message.</span></span> <span data-ttu-id="62947-164">Bu durumda, ileti kalıcı hello yerine korumak, isteğe bağlı olarak IOT hub'ı toohello arka uç uygulama geçirir.</span><span class="sxs-lookup"><span data-stu-id="62947-164">In this case, instead of persisting hello retain message, IoT Hub passes it toohello backend app.</span></span>
- <span data-ttu-id="62947-165">IOT Hub, yalnızca cihaz başına bir etkin MQTT bağlantısını destekler.</span><span class="sxs-lookup"><span data-stu-id="62947-165">IoT Hub only supports one active MQTT connection per device.</span></span> <span data-ttu-id="62947-166">Yeni bir MQTT bağlantı adına hello aynı cihaz kimliği IOT hub'ı toodrop hello var olan bağlantının kesilmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="62947-166">Any new MQTT connection on behalf of hello same device ID causes IoT Hub toodrop hello existing connection.</span></span>

<span data-ttu-id="62947-167">Daha fazla bilgi için bkz: [Geliştirici Kılavuzu Mesajlaşma][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="62947-167">For more information, see [Messaging developer's guide][lnk-messaging].</span></span>

### <a name="receiving-cloud-to-device-messages"></a><span data-ttu-id="62947-168">Bulut-cihaz iletilerini alma</span><span class="sxs-lookup"><span data-stu-id="62947-168">Receiving cloud-to-device messages</span></span>

<span data-ttu-id="62947-169">bir cihaz IOT hub'ı iletilerden tooreceive, abone kullanarak `devices/{device_id}/messages/devicebound/#` olarak bir **konu filtre**.</span><span class="sxs-lookup"><span data-stu-id="62947-169">tooreceive messages from IoT Hub, a device should subscribe using `devices/{device_id}/messages/devicebound/#` as a **Topic Filter**.</span></span> <span data-ttu-id="62947-170">birden çok düzeyli joker hello  **#**  tooallow hello yalnızca aygıt tooreceive ek özelliklerinde hello konu adı hello konu filtresi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="62947-170">hello multi-level wildcard **#** in hello Topic Filter is used only tooallow hello device tooreceive additional properties in hello topic name.</span></span> <span data-ttu-id="62947-171">IOT hub'ı hello hello kullanımını izin verme  **#**  veya **?**</span><span class="sxs-lookup"><span data-stu-id="62947-171">IoT Hub does not allow hello usage of hello **#** or **?**</span></span> <span data-ttu-id="62947-172">alt konuları filtrelemek için joker karakter.</span><span class="sxs-lookup"><span data-stu-id="62947-172">wildcards for filtering of sub-topics.</span></span> <span data-ttu-id="62947-173">IOT hub'ı genel amaçlı pub-sub Mesajlaşma Aracısı olmadığından, yalnızca belgelenen hello konu adları ve konu filtreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="62947-173">Since IoT Hub is not a general purpose pub-sub messaging broker, it only supports hello documented topic names and topic filters.</span></span>

<span data-ttu-id="62947-174">Merhaba tarafından temsil edilen tooits cihaza özel uç noktası başarıyla abone kadar hello cihaz tüm iletileri IOT Hub'ından almaz `devices/{device_id}/messages/devicebound/#` konu filtre.</span><span class="sxs-lookup"><span data-stu-id="62947-174">hello device does not receive any messages from IoT Hub, until it has successfully subscribed tooits device-specific endpoint, represented by hello `devices/{device_id}/messages/devicebound/#` topic filter.</span></span> <span data-ttu-id="62947-175">Başarılı abonelik kurulduktan sonra hello aygıtı tooit hello Abonelik başlangıç zamanından sonra gönderilen yalnızca bulut-cihaz iletilerini alma başlatır.</span><span class="sxs-lookup"><span data-stu-id="62947-175">After successful subscription has been established, hello device starts receiving only cloud-to-device messages that have been sent tooit after hello time of hello subscription.</span></span> <span data-ttu-id="62947-176">Merhaba aygıt ile bağlanıyorsa **CleanSession** bayrağı ayarlanmış çok**0**, hello abonelik, farklı oturumlarında kalıcıdır.</span><span class="sxs-lookup"><span data-stu-id="62947-176">If hello device connects with **CleanSession** flag set too**0**, hello subscription is persisted across different sessions.</span></span> <span data-ttu-id="62947-177">Bu durumda, ile sonraki bağlanışında hello **CleanSession 0** hello cihaz, bağlı değilken tooit gönderilen bekleyen iletileri alır.</span><span class="sxs-lookup"><span data-stu-id="62947-177">In this case, hello next time it connects with **CleanSession 0** hello device receives outstanding messages that have been sent tooit while it was disconnected.</span></span> <span data-ttu-id="62947-178">Merhaba aygıt kullanıyorsa **CleanSession** bayrağı ayarlanmış çok**1** tooits aygıt uç noktası abone kadar yine de, tüm iletileri IOT Hub'ından almaz.</span><span class="sxs-lookup"><span data-stu-id="62947-178">If hello device uses **CleanSession** flag set too**1** though, it does not receive any messages from IoT Hub until it subscribes tooits device-endpoint.</span></span>

<span data-ttu-id="62947-179">IOT hub'ı sunar hello iletilerle **konu adı** `devices/{device_id}/messages/devicebound/`, veya `devices/{device_id}/messages/devicebound/{property_bag}` tüm ileti özellikleri varsa.</span><span class="sxs-lookup"><span data-stu-id="62947-179">IoT Hub delivers messages with hello **Topic Name** `devices/{device_id}/messages/devicebound/`, or `devices/{device_id}/messages/devicebound/{property_bag}` if there are any message properties.</span></span> <span data-ttu-id="62947-180">`{property_bag}`İleti özelliklerini URL kodlanmış anahtar/değer çiftleri içerir.</span><span class="sxs-lookup"><span data-stu-id="62947-180">`{property_bag}` contains url-encoded key/value pairs of message properties.</span></span> <span data-ttu-id="62947-181">Yalnızca uygulama özellikleri ve kullanıcı ayarlanabilir Sistem Özellikleri (gibi **MessageID** veya **correlationıd değeri**) hello özellik paketindeki dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="62947-181">Only application properties and user-settable system properties (such as **messageId** or **correlationId**) are included in hello property bag.</span></span> <span data-ttu-id="62947-182">Sistem özelliği adlara sahip hello önek  **$** , uygulama özellikleri ile önek hello özgün özellik adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="62947-182">System property names have hello prefix **$**, application properties use hello original property name with no prefix.</span></span>

<span data-ttu-id="62947-183">Cihaz uygulaması tooa konuyla zaman abone olan **QoS 2**, IOT hub'ı verir hello maksimum QoS düzey 1 **SUBACK** paket.</span><span class="sxs-lookup"><span data-stu-id="62947-183">When a device app subscribes tooa topic with **QoS 2**, IoT Hub grants maximum QoS level 1 in hello **SUBACK** packet.</span></span> <span data-ttu-id="62947-184">Bundan sonra QoS 1'i kullanarak iletileri toohello cihaz IOT hub'ı sunar.</span><span class="sxs-lookup"><span data-stu-id="62947-184">After that, IoT Hub delivers messages toohello device using QoS 1.</span></span>

### <a name="retrieving-a-device-twins-properties"></a><span data-ttu-id="62947-185">Bir cihaz çifti'nın özelliklerini alma</span><span class="sxs-lookup"><span data-stu-id="62947-185">Retrieving a device twin's properties</span></span>

<span data-ttu-id="62947-186">İlk olarak, bir cihaz çok abone`$iothub/twin/res/#`, tooreceive hello işlemin yanıtlar.</span><span class="sxs-lookup"><span data-stu-id="62947-186">First, a device subscribes too`$iothub/twin/res/#`, tooreceive hello operation's responses.</span></span> <span data-ttu-id="62947-187">Ardından, bir boş ileti tootopic gönderir `$iothub/twin/GET/?$rid={request id}`, için doldurulan bir değerle **istek kimliği**. hello hizmeti sonra konuda hello cihaz çifti verileri içeren bir yanıt iletisi gönderir `$iothub/twin/res/{status}/?$rid={request id}`, kullanma, hello aynı  **İstek Kimliği** hello istek olarak.</span><span class="sxs-lookup"><span data-stu-id="62947-187">Then, it sends an empty message tootopic `$iothub/twin/GET/?$rid={request id}`, with a populated value for **request id**. hello service then sends a response message containing hello device twin data on topic `$iothub/twin/res/{status}/?$rid={request id}`, using hello same **request id** as hello request.</span></span>

<span data-ttu-id="62947-188">İstek Kimliği olarak başına bir ileti özellik değeri için geçerli bir değer olabilir [IOT Hub Geliştirici Kılavuzu Mesajlaşma][lnk-messaging], ve durumunu bir tamsayı olarak doğrulandı.</span><span class="sxs-lookup"><span data-stu-id="62947-188">Request id can be any valid value for a message property value, as per [IoT Hub messaging developer's guide][lnk-messaging], and status is validated as an integer.</span></span>
<span data-ttu-id="62947-189">Merhaba yanıt gövdesi hello cihaz çifti hello özellikler bölümü içerir:</span><span class="sxs-lookup"><span data-stu-id="62947-189">hello response body contains hello properties section of hello device twin:</span></span>

<span data-ttu-id="62947-190">Merhaba kimlik kayıt defteri girişi Hello gövdesi toohello "Özellikler" üye, örneğin sınırlıdır:</span><span class="sxs-lookup"><span data-stu-id="62947-190">hello body of hello identity registry entry limited toohello “properties” member, for example:</span></span>

        {
            "properties": {
                "desired": {
                    "telemetrySendFrequency": "5m",
                    "$version": 12
                },
                "reported": {
                    "telemetrySendFrequency": "5m",
                    "batteryLevel": 55,
                    "$version": 123
                }
            }
        }

<span data-ttu-id="62947-191">Merhaba olası durum kodları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="62947-191">hello possible status codes are:</span></span>

|<span data-ttu-id="62947-192">Durum</span><span class="sxs-lookup"><span data-stu-id="62947-192">Status</span></span> | <span data-ttu-id="62947-193">Açıklama</span><span class="sxs-lookup"><span data-stu-id="62947-193">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="62947-194">200</span><span class="sxs-lookup"><span data-stu-id="62947-194">200</span></span> | <span data-ttu-id="62947-195">Başarılı</span><span class="sxs-lookup"><span data-stu-id="62947-195">Success</span></span> |
| <span data-ttu-id="62947-196">429</span><span class="sxs-lookup"><span data-stu-id="62947-196">429</span></span> | <span data-ttu-id="62947-197">(Kısıtlanan) çok sayıda istek, göre [IOT Hub'ın azaltma][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="62947-197">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="62947-198">5**</span><span class="sxs-lookup"><span data-stu-id="62947-198">5**</span></span> | <span data-ttu-id="62947-199">Sunucu hataları</span><span class="sxs-lookup"><span data-stu-id="62947-199">Server errors</span></span> |

<span data-ttu-id="62947-200">Daha fazla bilgi için bkz: [cihaz çiftlerini Geliştirici Kılavuzu][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="62947-200">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="update-device-twins-reported-properties"></a><span data-ttu-id="62947-201">Cihaz çifti'nın bildirilen özelliklerini güncelleştir</span><span class="sxs-lookup"><span data-stu-id="62947-201">Update device twin's reported properties</span></span>

<span data-ttu-id="62947-202">Merhaba aşağıdaki sırayı bir aygıtı hello güncelleştirme biçimini açıklar IOT Hub cihaz çiftine hello özelliklerinde bildirdi:</span><span class="sxs-lookup"><span data-stu-id="62947-202">hello following sequence describes how a device updates hello reported properties in hello device twin in IoT Hub:</span></span>

1. <span data-ttu-id="62947-203">Bir cihaz ilk toohello abone olmalısınız `$iothub/twin/res/#` IOT hub'dan konu tooreceive hello işlemin yanıtlar.</span><span class="sxs-lookup"><span data-stu-id="62947-203">A device must first subscribe toohello `$iothub/twin/res/#` topic tooreceive hello operation's responses from IoT Hub.</span></span>

1. <span data-ttu-id="62947-204">Bir aygıt hello cihaz çifti güncelleştirme toohello içeren bir ileti gönderir `$iothub/twin/PATCH/properties/reported/?$rid={request id}` konu.</span><span class="sxs-lookup"><span data-stu-id="62947-204">A device sends a message that contains hello device twin update toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` topic.</span></span> <span data-ttu-id="62947-205">Bu iletiyi içeren bir **istek kimliği** değeri.</span><span class="sxs-lookup"><span data-stu-id="62947-205">This message includes a **request id** value.</span></span>

1. <span data-ttu-id="62947-206">Konu bildirilen özellikler koleksiyonunda içeren bir yanıt iletisi için yeni ETag değeri hello gönderir hello sonra hizmet Hello `$iothub/twin/res/{status}/?$rid={request id}`.</span><span class="sxs-lookup"><span data-stu-id="62947-206">hello service then sends a response message that contains hello new ETag value for hello reported properties collection on topic `$iothub/twin/res/{status}/?$rid={request id}`.</span></span> <span data-ttu-id="62947-207">Bu yanıt iletisiyle kullandığı aynı hello **istek kimliği** hello istek olarak.</span><span class="sxs-lookup"><span data-stu-id="62947-207">This response message uses hello same **request id** as hello request.</span></span>

<span data-ttu-id="62947-208">Merhaba istek ileti gövdesi yeni değerleri bildirilen özelliklerini (değiştirilebilir, başka bir özellik veya meta veri) sağlayan bir JSON belgesi içerir.</span><span class="sxs-lookup"><span data-stu-id="62947-208">hello request message body contains a JSON document, which provides new values for reported properties (no other property or metadata can be modified).</span></span>
<span data-ttu-id="62947-209">Merhaba JSON belgesi içindeki her üyenin güncelleştirir veya hello cihaz çifti'nın belgede hello karşılık gelen üye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="62947-209">Each member in hello JSON document updates or add hello corresponding member in hello device twin’s document.</span></span> <span data-ttu-id="62947-210">Bir üye kümesi çok`null`, hello nesnesini içeren hello üyeden siler.</span><span class="sxs-lookup"><span data-stu-id="62947-210">A member set too`null`, deletes hello member from hello containing object.</span></span> <span data-ttu-id="62947-211">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="62947-211">For example:</span></span>

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

<span data-ttu-id="62947-212">Merhaba olası durum kodları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="62947-212">hello possible status codes are:</span></span>

|<span data-ttu-id="62947-213">Durum</span><span class="sxs-lookup"><span data-stu-id="62947-213">Status</span></span> | <span data-ttu-id="62947-214">Açıklama</span><span class="sxs-lookup"><span data-stu-id="62947-214">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="62947-215">200</span><span class="sxs-lookup"><span data-stu-id="62947-215">200</span></span> | <span data-ttu-id="62947-216">Başarılı</span><span class="sxs-lookup"><span data-stu-id="62947-216">Success</span></span> |
| <span data-ttu-id="62947-217">400</span><span class="sxs-lookup"><span data-stu-id="62947-217">400</span></span> | <span data-ttu-id="62947-218">Hatalı istek.</span><span class="sxs-lookup"><span data-stu-id="62947-218">Bad Request.</span></span> <span data-ttu-id="62947-219">Hatalı biçimlendirilmiş JSON</span><span class="sxs-lookup"><span data-stu-id="62947-219">Malformed JSON</span></span> |
| <span data-ttu-id="62947-220">429</span><span class="sxs-lookup"><span data-stu-id="62947-220">429</span></span> | <span data-ttu-id="62947-221">(Kısıtlanan) çok sayıda istek, göre [IOT Hub'ın azaltma][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="62947-221">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="62947-222">5**</span><span class="sxs-lookup"><span data-stu-id="62947-222">5**</span></span> | <span data-ttu-id="62947-223">Sunucu hataları</span><span class="sxs-lookup"><span data-stu-id="62947-223">Server errors</span></span> |

<span data-ttu-id="62947-224">Daha fazla bilgi için bkz: [cihaz çiftlerini Geliştirici Kılavuzu][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="62947-224">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="receiving-desired-properties-update-notifications"></a><span data-ttu-id="62947-225">Alıcı istenen özellikler güncelleştirme bildirimlerini</span><span class="sxs-lookup"><span data-stu-id="62947-225">Receiving desired properties update notifications</span></span>

<span data-ttu-id="62947-226">Bir aygıt bağlandığında, IOT hub'ı bildirimleri toohello konu gönderir `$iothub/twin/PATCH/properties/desired/?$version={new version}`, hello çözüm arka ucu tarafından gerçekleştirilen hello güncelleştirme Merhaba içeriğine içerir.</span><span class="sxs-lookup"><span data-stu-id="62947-226">When a device is connected, IoT Hub sends notifications toohello topic `$iothub/twin/PATCH/properties/desired/?$version={new version}`, which contain hello content of hello update performed by hello solution back end.</span></span> <span data-ttu-id="62947-227">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="62947-227">For example:</span></span>

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

<span data-ttu-id="62947-228">Özelliği güncelleştirmeleri ettirilmesi `null` JSON hello değerleri anlamına gelir nesne üyesi siliniyor.</span><span class="sxs-lookup"><span data-stu-id="62947-228">As for property updates, `null` values means that hello JSON object member is being deleted.</span></span>


> [!IMPORTANT] 
> <span data-ttu-id="62947-229">Yalnızca aygıtları bağlandığınızda IOT hub'ı değişiklik bildirimleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="62947-229">IoT Hub generates change notifications only when devices are connected.</span></span> <span data-ttu-id="62947-230">Tooimplement hello emin olun [aygıt yeniden bağlanmayı akış] [ lnk-devguide-twin-reconnection] tookeep hello istenen özellikleri IOT Hub ve hello cihaz uygulaması arasında eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="62947-230">Make sure tooimplement hello [device reconnection flow][lnk-devguide-twin-reconnection] tookeep hello desired properties synchronized between IoT Hub and hello device app.</span></span>

<span data-ttu-id="62947-231">Daha fazla bilgi için bkz: [cihaz çiftlerini Geliştirici Kılavuzu][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="62947-231">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="respond-tooa-direct-method"></a><span data-ttu-id="62947-232">Yanıt tooa doğrudan yöntemi</span><span class="sxs-lookup"><span data-stu-id="62947-232">Respond tooa direct method</span></span>

<span data-ttu-id="62947-233">İlk olarak, bir aygıt toosubscribe çok sahip`$iothub/methods/POST/#`.</span><span class="sxs-lookup"><span data-stu-id="62947-233">First, a device has toosubscribe too`$iothub/methods/POST/#`.</span></span> <span data-ttu-id="62947-234">IOT Hub yöntemi istekleri toohello konu gönderir `$iothub/methods/POST/{method name}/?$rid={request id}`, ya geçerli bir JSON ya da boş bir gövde ile.</span><span class="sxs-lookup"><span data-stu-id="62947-234">IoT Hub sends method requests toohello topic `$iothub/methods/POST/{method name}/?$rid={request id}`, with either a valid JSON or an empty body.</span></span>

<span data-ttu-id="62947-235">toorespond, hello aygıt, geçerli bir JSON ya da boş gövde toohello konu içeren bir ileti gönderir `$iothub/methods/res/{status}/?$rid={request id}`, burada **istek kimliği** bir hello istek iletisinde hello toomatch sahiptir ve **durum** tamsayı toobe sahip .</span><span class="sxs-lookup"><span data-stu-id="62947-235">toorespond, hello device sends a message with a valid JSON or empty body toohello topic `$iothub/methods/res/{status}/?$rid={request id}`, where **request id** has toomatch hello one in hello request message, and **status** has toobe an integer.</span></span>

<span data-ttu-id="62947-236">Daha fazla bilgi için bkz: [yöntemi Geliştirici Kılavuzu doğrudan][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="62947-236">For more information, see [Direct method developer's guide][lnk-methods].</span></span>

### <a name="additional-considerations"></a><span data-ttu-id="62947-237">Diğer konular</span><span class="sxs-lookup"><span data-stu-id="62947-237">Additional considerations</span></span>

<span data-ttu-id="62947-238">Son yaparken, toocustomize hello MQTT protokol davranışı hello bulut tarafındaki gerekiyorsa hello gözden geçirmelidir [Azure IOT protokolü ağ geçidini] [ lnk-azure-protocol-gateway] toodeploy yüksek performans sağlayan doğrudan IOT Hub ile arabirimleri özel protokol ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="62947-238">As a final consideration, if you need toocustomize hello MQTT protocol behavior on hello cloud side, you should review hello [Azure IoT protocol gateway][lnk-azure-protocol-gateway] that enables you toodeploy a high-performance custom protocol gateway that interfaces directly with IoT Hub.</span></span> <span data-ttu-id="62947-239">Hello Azure IOT protokolü ağ geçidini, toocustomize hello aygıt Protokolü tooaccommodate brownfield MQTT dağıtımları veya diğer özel protokoller sağlar.</span><span class="sxs-lookup"><span data-stu-id="62947-239">hello Azure IoT protocol gateway enables you toocustomize hello device protocol tooaccommodate brownfield MQTT deployments or other custom protocols.</span></span> <span data-ttu-id="62947-240">Bu yaklaşım, ancak çalıştırın ve bir özel protokol ağ geçidi çalışmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="62947-240">This approach does require, however, that you run and operate a custom protocol gateway.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62947-241">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="62947-241">Next steps</span></span>

<span data-ttu-id="62947-242">toolearn hello MQTT protokolü hakkında daha fazla bilgi görmek hello [MQTT belgelerine][lnk-mqtt-docs].</span><span class="sxs-lookup"><span data-stu-id="62947-242">toolearn more about hello MQTT protocol, see hello [MQTT documentation][lnk-mqtt-docs].</span></span>

<span data-ttu-id="62947-243">IOT hub'ı dağıtımınızı planlama hakkında daha fazla toolearn bakın:</span><span class="sxs-lookup"><span data-stu-id="62947-243">toolearn more about planning your IoT Hub deployment, see:</span></span>

* <span data-ttu-id="62947-244">[IOT cihaz katalog için Azure Onaylandı][lnk-devices]</span><span class="sxs-lookup"><span data-stu-id="62947-244">[Azure Certified for IoT device catalog][lnk-devices]</span></span>
* <span data-ttu-id="62947-245">[Destek ek protokoller][lnk-protocols]</span><span class="sxs-lookup"><span data-stu-id="62947-245">[Support additional protocols][lnk-protocols]</span></span>
* <span data-ttu-id="62947-246">[Event Hubs ile karşılaştırın][lnk-compare]</span><span class="sxs-lookup"><span data-stu-id="62947-246">[Compare with Event Hubs][lnk-compare]</span></span>
* <span data-ttu-id="62947-247">[Ölçeklendirme, HA ve DR][lnk-scaling]</span><span class="sxs-lookup"><span data-stu-id="62947-247">[Scaling, HA, and DR][lnk-scaling]</span></span>

<span data-ttu-id="62947-248">toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:</span><span class="sxs-lookup"><span data-stu-id="62947-248">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="62947-249">[IOT Hub Geliştirici Kılavuzu][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="62947-249">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="62947-250">[Bir aygıt ile Azure IOT kenar benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="62947-250">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-mqtt-org]: http://mqtt.org/
[lnk-mqtt-docs]: http://mqtt.org/documentation
[lnk-sample-node]: https://github.com/Azure/azure-iot-sdk-node/blob/master/device/samples/simple_sample_device.js
[lnk-sample-java]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device/samples/send-receive-sample/src/main/java/samples/com/microsoft/azure/iothub/SendReceive.java
[lnk-sample-c]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt
[lnk-sample-csharp]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device/samples
[lnk-sample-python]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device/samples
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-sas-tokens]: iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-devices]: https://catalog.azureiotsuite.com/
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-messaging]: iot-hub-devguide-messaging.md

[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-twin-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow
[lnk-devguide-twin]: iot-hub-devguide-device-twins.md
