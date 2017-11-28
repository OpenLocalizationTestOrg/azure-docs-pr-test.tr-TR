---
title: Azure IOT Hub MQTT destek anlama | Microsoft Docs
description: "Geliştirici Kılavuzu - MQTT protokolünü kullanarak bir IOT Hub cihaz'e yönelik uç noktasına bağlanan cihazlar için destek. Yerleşik MQTT destekleyen Azure IOT cihaz SDK'ları hakkında bilgi içerir."
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
ms.openlocfilehash: eab70c1aa9c49a137c2ac1012449d57915fb0d27
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="communicate-with-your-iot-hub-using-the-mqtt-protocol"></a><span data-ttu-id="d8542-104">MQTT protokolünü kullanarak, IOT hub ile iletişim</span><span class="sxs-lookup"><span data-stu-id="d8542-104">Communicate with your IoT hub using the MQTT protocol</span></span>

<span data-ttu-id="d8542-105">IOT hub'ı kullanarak IOT Hub cihaz uç ile iletişim kurmak cihazları etkinleştirir [MQTT v3.1.1] [ lnk-mqtt-org] 8883 bağlantı noktası veya bağlantı noktası 443 üzerinden WebSocket protokolü üzerinden MQTT v3.1.1 protokolü.</span><span class="sxs-lookup"><span data-stu-id="d8542-105">IoT Hub enables devices to communicate with the IoT Hub device endpoints using the [MQTT v3.1.1][lnk-mqtt-org] protocol on port 8883 or MQTT v3.1.1 over WebSocket protocol on port 443.</span></span> <span data-ttu-id="d8542-106">IOT hub'ı TLS/SSL ile korunması için tüm cihaz iletişimi gerektirir (Bu nedenle, IOT hub'ı güvenli olmayan bağlantıları 1883 bağlantı noktası üzerinden olarak desteklemiyor).</span><span class="sxs-lookup"><span data-stu-id="d8542-106">IoT Hub requires all device communication to be secured using TLS/SSL (hence, IoT Hub doesn’t support non-secure connections over port 1883).</span></span>

## <a name="connecting-to-iot-hub"></a><span data-ttu-id="d8542-107">IOT hub'ına bağlama</span><span class="sxs-lookup"><span data-stu-id="d8542-107">Connecting to IoT Hub</span></span>

<span data-ttu-id="d8542-108">Bir aygıt ya da kitaplıkları kullanarak bir IOT hub'ına bağlanmak için MQTT protokolünü kullanabilirsiniz [Azure IOT SDK'ları] [ lnk-device-sdks] veya MQTT kullanarak doğrudan iletişim kuralı.</span><span class="sxs-lookup"><span data-stu-id="d8542-108">A device can use the MQTT protocol to connect to an IoT hub either by using the libraries in the [Azure IoT SDKs][lnk-device-sdks] or by using the MQTT protocol directly.</span></span>

## <a name="using-the-device-sdks"></a><span data-ttu-id="d8542-109">Cihaz SDK'ları kullanma</span><span class="sxs-lookup"><span data-stu-id="d8542-109">Using the device SDKs</span></span>

<span data-ttu-id="d8542-110">[Cihaz SDK'ları] [ lnk-device-sdks] destekleyen MQTT Protokolü Java, Node.js, C, C# ve Python için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d8542-110">[Device SDKs][lnk-device-sdks] that support the MQTT protocol are available for Java, Node.js, C, C#, and Python.</span></span> <span data-ttu-id="d8542-111">Cihaz SDK'ları, bir IOT hub bağlantı kurmak için standart IOT Hub bağlantı dizesine kullanın.</span><span class="sxs-lookup"><span data-stu-id="d8542-111">The device SDKs use the standard IoT Hub connection string to establish a connection to an IoT hub.</span></span> <span data-ttu-id="d8542-112">MQTT protokolünü kullanmak için istemci protokolünü parametresi ayarlanmalıdır **MQTT**.</span><span class="sxs-lookup"><span data-stu-id="d8542-112">To use the MQTT protocol, the client protocol parameter must be set to **MQTT**.</span></span> <span data-ttu-id="d8542-113">Varsayılan olarak, cihaz SDK'ları bir IOT Hub ile bağlanmak **CleanSession** bayrağı ayarlanmış **0** ve **QoS 1** IOT hub ile ileti alışverişi için.</span><span class="sxs-lookup"><span data-stu-id="d8542-113">By default, the device SDKs connect to an IoT Hub with the **CleanSession** flag set to **0** and use **QoS 1** for message exchange with the IoT hub.</span></span>

<span data-ttu-id="d8542-114">Bir cihaz IOT hub'a bağlandığında, cihaz SDK'ları cihazın IOT hub'ından ileti alıp ileti göndermek yöntemleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="d8542-114">When a device is connected to an IoT hub, the device SDKs provide methods that enable the device to send messages to and receive messages from an IoT hub.</span></span>

<span data-ttu-id="d8542-115">Aşağıdaki tabloda, desteklenen her dil için kod örnekleri içerir ve IOT Hub'ın MQTT protokolünü kullanarak bir bağlantı kurmak için kullanılacak parametreyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="d8542-115">The following table contains links to code samples for each supported language and specifies the parameter to use to establish a connection to IoT Hub using the MQTT protocol.</span></span>

| <span data-ttu-id="d8542-116">Dil</span><span class="sxs-lookup"><span data-stu-id="d8542-116">Language</span></span> | <span data-ttu-id="d8542-117">Protokol parametresi</span><span class="sxs-lookup"><span data-stu-id="d8542-117">Protocol parameter</span></span> |
| --- | --- |
| <span data-ttu-id="d8542-118">[Node.js][lnk-sample-node]</span><span class="sxs-lookup"><span data-stu-id="d8542-118">[Node.js][lnk-sample-node]</span></span> |<span data-ttu-id="d8542-119">Azure-IOT-cihaz-mqtt</span><span class="sxs-lookup"><span data-stu-id="d8542-119">azure-iot-device-mqtt</span></span> |
| <span data-ttu-id="d8542-120">[Java][lnk-sample-java]</span><span class="sxs-lookup"><span data-stu-id="d8542-120">[Java][lnk-sample-java]</span></span> |<span data-ttu-id="d8542-121">IotHubClientProtocol.MQTT</span><span class="sxs-lookup"><span data-stu-id="d8542-121">IotHubClientProtocol.MQTT</span></span> |
| <span data-ttu-id="d8542-122">[C][lnk-sample-c]</span><span class="sxs-lookup"><span data-stu-id="d8542-122">[C][lnk-sample-c]</span></span> |<span data-ttu-id="d8542-123">MQTT_Protocol</span><span class="sxs-lookup"><span data-stu-id="d8542-123">MQTT_Protocol</span></span> |
| <span data-ttu-id="d8542-124">[C#][lnk-sample-csharp]</span><span class="sxs-lookup"><span data-stu-id="d8542-124">[C#][lnk-sample-csharp]</span></span> |<span data-ttu-id="d8542-125">TransportType.Mqtt</span><span class="sxs-lookup"><span data-stu-id="d8542-125">TransportType.Mqtt</span></span> |
| <span data-ttu-id="d8542-126">[Python][lnk-sample-python]</span><span class="sxs-lookup"><span data-stu-id="d8542-126">[Python][lnk-sample-python]</span></span> |<span data-ttu-id="d8542-127">IoTHubTransportProvider.MQTT</span><span class="sxs-lookup"><span data-stu-id="d8542-127">IoTHubTransportProvider.MQTT</span></span> |

### <a name="migrating-a-device-app-from-amqp-to-mqtt"></a><span data-ttu-id="d8542-128">Cihaz uygulaması MQTT için AMQP geçirme</span><span class="sxs-lookup"><span data-stu-id="d8542-128">Migrating a device app from AMQP to MQTT</span></span>

<span data-ttu-id="d8542-129">Kullanıyorsanız [cihaz SDK'ları][lnk-device-sdks], MQTT için AMQP kullanarak geçiş gerektirir daha önce belirtildiği gibi istemci başlatması Protokolü parametresinde değiştirme.</span><span class="sxs-lookup"><span data-stu-id="d8542-129">If you are using the [device SDKs][lnk-device-sdks], switching from using AMQP to MQTT requires changing the protocol parameter in the client initialization as stated previously.</span></span>

<span data-ttu-id="d8542-130">Bunu yaparken, aşağıdaki öğeleri olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="d8542-130">When doing so, make sure to check the following items:</span></span>

* <span data-ttu-id="d8542-131">MQTT bağlantıyı sonlandırır sırada AMQP birçok koşulları için hatalar döndürür.</span><span class="sxs-lookup"><span data-stu-id="d8542-131">AMQP returns errors for many conditions, while MQTT terminates the connection.</span></span> <span data-ttu-id="d8542-132">Sonuç olarak, özel durum mantığı işleme bazı değişiklikler gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="d8542-132">As a result your exception handling logic might require some changes.</span></span>
* <span data-ttu-id="d8542-133">MQTT desteklemiyor *Reddet* alırken işlemleri [bulut-cihaz iletilerini][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="d8542-133">MQTT does not support the *reject* operations when receiving [cloud-to-device messages][lnk-messaging].</span></span> <span data-ttu-id="d8542-134">Arka uç uygulamanızı aygıt uygulamasından bir yanıt gerekiyorsa kullanmayı [doğrudan yöntemleri][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="d8542-134">If your back-end app needs to receive a response from the device app, consider using [direct methods][lnk-methods].</span></span>

## <a name="using-the-mqtt-protocol-directly"></a><span data-ttu-id="d8542-135">MQTT protokolü kullanarak doğrudan</span><span class="sxs-lookup"><span data-stu-id="d8542-135">Using the MQTT protocol directly</span></span>
<span data-ttu-id="d8542-136">Bir aygıt cihaz SDK'ları kullanamıyorsanız, bağlantı noktası 8883 MQTT protokolünü kullanarak ortak cihaz Uç noktalara hala bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="d8542-136">If a device cannot use the device SDKs, it can still connect to the public device endpoints using the MQTT protocol on port 8883.</span></span> <span data-ttu-id="d8542-137">İçinde **BAĞLAN** paket aygıt, aşağıdaki değerleri kullanmalıdır:</span><span class="sxs-lookup"><span data-stu-id="d8542-137">In the **CONNECT** packet the device should use the following values:</span></span>

* <span data-ttu-id="d8542-138">İçin **ClientID** alanında, kullanmak **DeviceID**.</span><span class="sxs-lookup"><span data-stu-id="d8542-138">For the **ClientId** field, use the **deviceId**.</span></span>
* <span data-ttu-id="d8542-139">İçin **kullanıcıadı** alanında, kullanmak `{iothubhostname}/{device_id}/api-version=2016-11-14`{iothubhostname} IOT hub'ın tam CName eder.</span><span class="sxs-lookup"><span data-stu-id="d8542-139">For the **Username** field, use `{iothubhostname}/{device_id}/api-version=2016-11-14`, where {iothubhostname} is the full CName of the IoT hub.</span></span>

    <span data-ttu-id="d8542-140">Örneğin, IOT hub'ınızın adını ise **contoso.azure devices.net** ve Cihazınızı adı ise **MyDevice01**, tam **kullanıcıadı** alan içermelidir`contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span><span class="sxs-lookup"><span data-stu-id="d8542-140">For example, if the name of your IoT hub is **contoso.azure-devices.net** and if the name of your device is **MyDevice01**, the full **Username** field should contain `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span></span>
* <span data-ttu-id="d8542-141">İçin **parola** alan, bir SAS belirteci kullanın.</span><span class="sxs-lookup"><span data-stu-id="d8542-141">For the **Password** field, use a SAS token.</span></span> <span data-ttu-id="d8542-142">SAS belirteci biçimi hem HTTP hem de AMQP protokolleri aynıdır:</span><span class="sxs-lookup"><span data-stu-id="d8542-142">The format of the SAS token is the same as for both the HTTP and AMQP protocols:</span></span><br/><span data-ttu-id="d8542-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span><span class="sxs-lookup"><span data-stu-id="d8542-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span></span>

    <span data-ttu-id="d8542-144">SAS belirteci oluşturma hakkında daha fazla bilgi için aygıt bölümüne bakın [IOT Hub'ı kullanarak güvenlik belirteçleri][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="d8542-144">For more information about how to generate SAS tokens, see the device section of [Using IoT Hub security tokens][lnk-sas-tokens].</span></span>

    <span data-ttu-id="d8542-145">Test edilirken de kullanabilirsiniz [aygıt explorer] [ lnk-device-explorer] aracı hızlı bir şekilde kendi koda kopyalayıp bir SAS belirteci oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="d8542-145">When testing, you can also use the [device explorer][lnk-device-explorer] tool to quickly generate a SAS token that you can copy and paste into your own code:</span></span>

  1. <span data-ttu-id="d8542-146">Git **Yönetim** sekmesinde **aygıt Explorer**.</span><span class="sxs-lookup"><span data-stu-id="d8542-146">Go to the **Management** tab in **Device Explorer**.</span></span>
  2. <span data-ttu-id="d8542-147">Tıklatın **SAS belirteci** (sağ üst).</span><span class="sxs-lookup"><span data-stu-id="d8542-147">Click **SAS Token** (top right).</span></span>
  3. <span data-ttu-id="d8542-148">Üzerinde **SASTokenForm**, Cihazınızı seçin **DeviceID** açılır.</span><span class="sxs-lookup"><span data-stu-id="d8542-148">On **SASTokenForm**, select your device in the **DeviceID** drop down.</span></span> <span data-ttu-id="d8542-149">Ayarlama, **TTL**.</span><span class="sxs-lookup"><span data-stu-id="d8542-149">Set your **TTL**.</span></span>
  4. <span data-ttu-id="d8542-150">Tıklatın **Generate** , belirteç oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="d8542-150">Click **Generate** to create your token.</span></span>

     <span data-ttu-id="d8542-151">Bu yapı oluşturulan SAS belirteci sahip: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="d8542-151">The SAS token that's generated has this structure: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

     <span data-ttu-id="d8542-152">Bir parçası olarak kullanmak üzere bu belirteci **parola** MQTT kullanarak bağlanmak için bir alandır: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="d8542-152">The part of this token to use as the **Password** field to connect using MQTT is: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

<span data-ttu-id="d8542-153">İçin MQTT bağlanmak ve paketleri bağlantısını kesmek, IOT hub'ı üzerinde bir olay sorunları **işlemlerini izleme** kanal, bağlantı sorunları gidermenize yardımcı olabilecek ek bilgiler ile.</span><span class="sxs-lookup"><span data-stu-id="d8542-153">For MQTT connect and disconnect packets, IoT Hub issues an event on the **Operations Monitoring** channel with additional information that can help you to troubleshoot connectivity issues.</span></span>

### <a name="sending-device-to-cloud-messages"></a><span data-ttu-id="d8542-154">Cihaz bulut iletilerini gönderme</span><span class="sxs-lookup"><span data-stu-id="d8542-154">Sending device-to-cloud messages</span></span>

<span data-ttu-id="d8542-155">Başarılı bir bağlantı yaptıktan sonra bir cihaz IOT Hub'ına kullanarak iletileri gönderebilirsiniz `devices/{device_id}/messages/events/` veya `devices/{device_id}/messages/events/{property_bag}` olarak bir **konu adı**.</span><span class="sxs-lookup"><span data-stu-id="d8542-155">After making a successful connection, a device can send messages to IoT Hub using `devices/{device_id}/messages/events/` or `devices/{device_id}/messages/events/{property_bag}` as a **Topic Name**.</span></span> <span data-ttu-id="d8542-156">`{property_bag}` Öğesi url kodlanmış bir biçimde ek özelliklerle iletileri göndermek aygıt sağlar.</span><span class="sxs-lookup"><span data-stu-id="d8542-156">The `{property_bag}` element enables the device to send messages with additional properties in a url-encoded format.</span></span> <span data-ttu-id="d8542-157">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="d8542-157">For example:</span></span>

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> <span data-ttu-id="d8542-158">Bu `{property_bag}` öğesini kullanan sorgu dizeleri HTTP protokolü için olduğu gibi aynı kodlama.</span><span class="sxs-lookup"><span data-stu-id="d8542-158">This `{property_bag}` element uses the same encoding as for query strings in the HTTP protocol.</span></span>
>
>

<span data-ttu-id="d8542-159">Cihaz uygulaması de kullanabilirsiniz `devices/{device_id}/messages/events/{property_bag}` olarak **Will konu adı** tanımlamak için *iletilerini* bir telemetri iletisi olarak iletilir.</span><span class="sxs-lookup"><span data-stu-id="d8542-159">The device app can also use `devices/{device_id}/messages/events/{property_bag}` as the **Will topic name** to define *Will messages* to be forwarded as a telemetry message.</span></span>

- <span data-ttu-id="d8542-160">IOT hub'ı QoS 2 iletileri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="d8542-160">IoT Hub does not support QoS 2 messages.</span></span> <span data-ttu-id="d8542-161">Cihaz uygulaması içeren bir ileti yayımlarsa **QoS 2**, IOT hub'ı ağ bağlantıyı kapatır.</span><span class="sxs-lookup"><span data-stu-id="d8542-161">If a device app publishes a message with **QoS 2**, IoT Hub closes the network connection.</span></span>
- <span data-ttu-id="d8542-162">IOT hub'ı tut iletileri kalmaz.</span><span class="sxs-lookup"><span data-stu-id="d8542-162">IoT Hub does not persist Retain messages.</span></span> <span data-ttu-id="d8542-163">Bir cihaz içeren bir ileti gönderirse **TUT** bayrağı, IOT hub'ı ekler 1 olarak ayarlayın **x-opt-korumak** iletisi uygulama özelliği.</span><span class="sxs-lookup"><span data-stu-id="d8542-163">If a device sends a message with the **RETAIN** flag set to 1, IoT Hub adds the **x-opt-retain** application property to the message.</span></span> <span data-ttu-id="d8542-164">Bu durumda, tut ileti kalıcı yerine IOT hub'ı, arka uç uygulamaya geçirir.</span><span class="sxs-lookup"><span data-stu-id="d8542-164">In this case, instead of persisting the retain message, IoT Hub passes it to the backend app.</span></span>
- <span data-ttu-id="d8542-165">IOT Hub, yalnızca cihaz başına bir etkin MQTT bağlantısını destekler.</span><span class="sxs-lookup"><span data-stu-id="d8542-165">IoT Hub only supports one active MQTT connection per device.</span></span> <span data-ttu-id="d8542-166">Yeni bir MQTT bağlantı aynı cihaz kimliği adına, IOT Hub'ın var olan bağlantıyı kesmek neden olur.</span><span class="sxs-lookup"><span data-stu-id="d8542-166">Any new MQTT connection on behalf of the same device ID causes IoT Hub to drop the existing connection.</span></span>

<span data-ttu-id="d8542-167">Daha fazla bilgi için bkz: [Geliştirici Kılavuzu Mesajlaşma][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="d8542-167">For more information, see [Messaging developer's guide][lnk-messaging].</span></span>

### <a name="receiving-cloud-to-device-messages"></a><span data-ttu-id="d8542-168">Bulut-cihaz iletilerini alma</span><span class="sxs-lookup"><span data-stu-id="d8542-168">Receiving cloud-to-device messages</span></span>

<span data-ttu-id="d8542-169">IOT Hub'ından iletileri almak için bir cihaz kullanarak abone olmalısınız `devices/{device_id}/messages/devicebound/#` olarak bir **konu filtre**.</span><span class="sxs-lookup"><span data-stu-id="d8542-169">To receive messages from IoT Hub, a device should subscribe using `devices/{device_id}/messages/devicebound/#` as a **Topic Filter**.</span></span> <span data-ttu-id="d8542-170">Birden çok düzeyli joker  **#**  konu filtresinde yalnızca ek özellikleri'nde konu adı almak cihaz sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d8542-170">The multi-level wildcard **#** in the Topic Filter is used only to allow the device to receive additional properties in the topic name.</span></span> <span data-ttu-id="d8542-171">IOT hub'ı kullanımını izin verme  **#**  veya **?**</span><span class="sxs-lookup"><span data-stu-id="d8542-171">IoT Hub does not allow the usage of the **#** or **?**</span></span> <span data-ttu-id="d8542-172">alt konuları filtrelemek için joker karakter.</span><span class="sxs-lookup"><span data-stu-id="d8542-172">wildcards for filtering of sub-topics.</span></span> <span data-ttu-id="d8542-173">IOT hub'ı genel amaçlı pub-sub Mesajlaşma Aracısı olmadığından, yalnızca belgelenen konu adları ve konu filtreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="d8542-173">Since IoT Hub is not a general purpose pub-sub messaging broker, it only supports the documented topic names and topic filters.</span></span>

<span data-ttu-id="d8542-174">Cihaz herhangi bir ileti almazsa, cihaza özel uç noktasında başarıyla abone kadar IOT Hub'ından tarafından temsil edilen `devices/{device_id}/messages/devicebound/#` konu filtre.</span><span class="sxs-lookup"><span data-stu-id="d8542-174">The device does not receive any messages from IoT Hub, until it has successfully subscribed to its device-specific endpoint, represented by the `devices/{device_id}/messages/devicebound/#` topic filter.</span></span> <span data-ttu-id="d8542-175">Başarılı abonelik kurulduktan sonra cihaz için abonelik süresi sonra gönderilmiş bulut-cihaz iletilerini alma başlatır.</span><span class="sxs-lookup"><span data-stu-id="d8542-175">After successful subscription has been established, the device starts receiving only cloud-to-device messages that have been sent to it after the time of the subscription.</span></span> <span data-ttu-id="d8542-176">Aygıt ile bağlanıyorsa **CleanSession** bayrağı ayarlanmış **0**, abonelik farklı oturumlarında kalıcıdır.</span><span class="sxs-lookup"><span data-stu-id="d8542-176">If the device connects with **CleanSession** flag set to **0**, the subscription is persisted across different sessions.</span></span> <span data-ttu-id="d8542-177">Bu durumda, sonraki bağladığı ile **CleanSession 0** cihaz, bağlı değilken, kendisine gönderilen bekleyen iletileri alır.</span><span class="sxs-lookup"><span data-stu-id="d8542-177">In this case, the next time it connects with **CleanSession 0** the device receives outstanding messages that have been sent to it while it was disconnected.</span></span> <span data-ttu-id="d8542-178">Aygıt kullanıyorsa **CleanSession** bayrağı ayarlanmış **1** kendi cihaz uç noktasına abone kadar yine de, tüm iletileri IOT Hub'ından almaz.</span><span class="sxs-lookup"><span data-stu-id="d8542-178">If the device uses **CleanSession** flag set to **1** though, it does not receive any messages from IoT Hub until it subscribes to its device-endpoint.</span></span>

<span data-ttu-id="d8542-179">IOT hub'ı sunar iletilerle **konu adı** `devices/{device_id}/messages/devicebound/`, veya `devices/{device_id}/messages/devicebound/{property_bag}` tüm ileti özellikleri varsa.</span><span class="sxs-lookup"><span data-stu-id="d8542-179">IoT Hub delivers messages with the **Topic Name** `devices/{device_id}/messages/devicebound/`, or `devices/{device_id}/messages/devicebound/{property_bag}` if there are any message properties.</span></span> <span data-ttu-id="d8542-180">`{property_bag}`İleti özelliklerini URL kodlanmış anahtar/değer çiftleri içerir.</span><span class="sxs-lookup"><span data-stu-id="d8542-180">`{property_bag}` contains url-encoded key/value pairs of message properties.</span></span> <span data-ttu-id="d8542-181">Yalnızca uygulama özellikleri ve kullanıcı ayarlanabilir Sistem Özellikleri (gibi **MessageID** veya **correlationıd değeri**) özellik paketindeki dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="d8542-181">Only application properties and user-settable system properties (such as **messageId** or **correlationId**) are included in the property bag.</span></span> <span data-ttu-id="d8542-182">Sistem özelliği adlara sahip önek  **$** , uygulama özellikleri ile önek özgün özellik adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="d8542-182">System property names have the prefix **$**, application properties use the original property name with no prefix.</span></span>

<span data-ttu-id="d8542-183">Bir konu ile cihaz uygulamasının ne zaman aboneliği **QoS 2**, IOT hub'ı verir maksimum QoS düzey 1 **SUBACK** paket.</span><span class="sxs-lookup"><span data-stu-id="d8542-183">When a device app subscribes to a topic with **QoS 2**, IoT Hub grants maximum QoS level 1 in the **SUBACK** packet.</span></span> <span data-ttu-id="d8542-184">Bundan sonra IOT Hub aygıtına QoS 1 kullanarak iletileri sunar.</span><span class="sxs-lookup"><span data-stu-id="d8542-184">After that, IoT Hub delivers messages to the device using QoS 1.</span></span>

### <a name="retrieving-a-device-twins-properties"></a><span data-ttu-id="d8542-185">Bir cihaz çifti'nın özelliklerini alma</span><span class="sxs-lookup"><span data-stu-id="d8542-185">Retrieving a device twin's properties</span></span>

<span data-ttu-id="d8542-186">Bir cihaz ilk olarak, abone `$iothub/twin/res/#`, işlem yanıtları almak için.</span><span class="sxs-lookup"><span data-stu-id="d8542-186">First, a device subscribes to `$iothub/twin/res/#`, to receive the operation's responses.</span></span> <span data-ttu-id="d8542-187">Ardından, boş bir iletiyi konu başlığına gönderir `$iothub/twin/GET/?$rid={request id}`, için doldurulan bir değerle **istek kimliği**.</span><span class="sxs-lookup"><span data-stu-id="d8542-187">Then, it sends an empty message to topic `$iothub/twin/GET/?$rid={request id}`, with a populated value for **request id**.</span></span> <span data-ttu-id="d8542-188">Hizmeti daha sonra konuda cihaz çifti verileri içeren bir yanıt iletisi gönderir `$iothub/twin/res/{status}/?$rid={request id}`, aynı kullanarak **istek kimliği** istek olarak.</span><span class="sxs-lookup"><span data-stu-id="d8542-188">The service then sends a response message containing the device twin data on topic `$iothub/twin/res/{status}/?$rid={request id}`, using the same **request id** as the request.</span></span>

<span data-ttu-id="d8542-189">İstek Kimliği olarak başına bir ileti özellik değeri için geçerli bir değer olabilir [IOT Hub Geliştirici Kılavuzu Mesajlaşma][lnk-messaging], ve durumunu bir tamsayı olarak doğrulandı.</span><span class="sxs-lookup"><span data-stu-id="d8542-189">Request id can be any valid value for a message property value, as per [IoT Hub messaging developer's guide][lnk-messaging], and status is validated as an integer.</span></span>
<span data-ttu-id="d8542-190">Yanıt gövdesi cihaz çiftinin özellikler bölümü içerir:</span><span class="sxs-lookup"><span data-stu-id="d8542-190">The response body contains the properties section of the device twin:</span></span>

<span data-ttu-id="d8542-191">Örneğin "Özellikler" üyesine sınırlı kimlik kayıt defteri girişi gövdesi:</span><span class="sxs-lookup"><span data-stu-id="d8542-191">The body of the identity registry entry limited to the “properties” member, for example:</span></span>

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

<span data-ttu-id="d8542-192">Olası durum kodları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d8542-192">The possible status codes are:</span></span>

|<span data-ttu-id="d8542-193">Durum</span><span class="sxs-lookup"><span data-stu-id="d8542-193">Status</span></span> | <span data-ttu-id="d8542-194">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d8542-194">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="d8542-195">200</span><span class="sxs-lookup"><span data-stu-id="d8542-195">200</span></span> | <span data-ttu-id="d8542-196">Başarılı</span><span class="sxs-lookup"><span data-stu-id="d8542-196">Success</span></span> |
| <span data-ttu-id="d8542-197">429</span><span class="sxs-lookup"><span data-stu-id="d8542-197">429</span></span> | <span data-ttu-id="d8542-198">(Kısıtlanan) çok sayıda istek, göre [IOT Hub'ın azaltma][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="d8542-198">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="d8542-199">5**</span><span class="sxs-lookup"><span data-stu-id="d8542-199">5**</span></span> | <span data-ttu-id="d8542-200">Sunucu hataları</span><span class="sxs-lookup"><span data-stu-id="d8542-200">Server errors</span></span> |

<span data-ttu-id="d8542-201">Daha fazla bilgi için bkz: [cihaz çiftlerini Geliştirici Kılavuzu][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="d8542-201">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="update-device-twins-reported-properties"></a><span data-ttu-id="d8542-202">Cihaz çifti'nın bildirilen özelliklerini güncelleştir</span><span class="sxs-lookup"><span data-stu-id="d8542-202">Update device twin's reported properties</span></span>

<span data-ttu-id="d8542-203">Aşağıdaki sırada, bir cihaz IOT Hub cihaz çiftine bildirilen özelliklerinde güncelleştirme biçimini açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="d8542-203">The following sequence describes how a device updates the reported properties in the device twin in IoT Hub:</span></span>

1. <span data-ttu-id="d8542-204">Bir cihaz ilk abone olmalısınız `$iothub/twin/res/#` IOT Hub'ından işlem yanıtları almak için konu.</span><span class="sxs-lookup"><span data-stu-id="d8542-204">A device must first subscribe to the `$iothub/twin/res/#` topic to receive the operation's responses from IoT Hub.</span></span>

1. <span data-ttu-id="d8542-205">Bir cihaz için cihaz çifti güncelleştirme içeren bir ileti gönderir `$iothub/twin/PATCH/properties/reported/?$rid={request id}` konu.</span><span class="sxs-lookup"><span data-stu-id="d8542-205">A device sends a message that contains the device twin update to the `$iothub/twin/PATCH/properties/reported/?$rid={request id}` topic.</span></span> <span data-ttu-id="d8542-206">Bu iletiyi içeren bir **istek kimliği** değeri.</span><span class="sxs-lookup"><span data-stu-id="d8542-206">This message includes a **request id** value.</span></span>

1. <span data-ttu-id="d8542-207">Hizmeti daha sonra konuda bildirilen özellikleri koleksiyon için yeni ETag değeri içeren bir yanıt iletisi gönderir `$iothub/twin/res/{status}/?$rid={request id}`.</span><span class="sxs-lookup"><span data-stu-id="d8542-207">The service then sends a response message that contains the new ETag value for the reported properties collection on topic `$iothub/twin/res/{status}/?$rid={request id}`.</span></span> <span data-ttu-id="d8542-208">Bu yanıt iletisiyle aynı kullanan **istek kimliği** istek olarak.</span><span class="sxs-lookup"><span data-stu-id="d8542-208">This response message uses the same **request id** as the request.</span></span>

<span data-ttu-id="d8542-209">İstek ileti gövdesi yeni değerleri bildirilen özelliklerini (değiştirilebilir, başka bir özellik veya meta veri) sağlayan bir JSON belgesi içerir.</span><span class="sxs-lookup"><span data-stu-id="d8542-209">The request message body contains a JSON document, which provides new values for reported properties (no other property or metadata can be modified).</span></span>
<span data-ttu-id="d8542-210">JSON belgesini içindeki her üyenin güncelleştirir veya cihaz çifti'nın belgeye karşılık gelen üye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d8542-210">Each member in the JSON document updates or add the corresponding member in the device twin’s document.</span></span> <span data-ttu-id="d8542-211">Ayarlanmış bir üye `null`, üyeyi içeren nesneyi siler.</span><span class="sxs-lookup"><span data-stu-id="d8542-211">A member set to `null`, deletes the member from the containing object.</span></span> <span data-ttu-id="d8542-212">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="d8542-212">For example:</span></span>

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

<span data-ttu-id="d8542-213">Olası durum kodları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d8542-213">The possible status codes are:</span></span>

|<span data-ttu-id="d8542-214">Durum</span><span class="sxs-lookup"><span data-stu-id="d8542-214">Status</span></span> | <span data-ttu-id="d8542-215">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d8542-215">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="d8542-216">200</span><span class="sxs-lookup"><span data-stu-id="d8542-216">200</span></span> | <span data-ttu-id="d8542-217">Başarılı</span><span class="sxs-lookup"><span data-stu-id="d8542-217">Success</span></span> |
| <span data-ttu-id="d8542-218">400</span><span class="sxs-lookup"><span data-stu-id="d8542-218">400</span></span> | <span data-ttu-id="d8542-219">Hatalı istek.</span><span class="sxs-lookup"><span data-stu-id="d8542-219">Bad Request.</span></span> <span data-ttu-id="d8542-220">Hatalı biçimlendirilmiş JSON</span><span class="sxs-lookup"><span data-stu-id="d8542-220">Malformed JSON</span></span> |
| <span data-ttu-id="d8542-221">429</span><span class="sxs-lookup"><span data-stu-id="d8542-221">429</span></span> | <span data-ttu-id="d8542-222">(Kısıtlanan) çok sayıda istek, göre [IOT Hub'ın azaltma][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="d8542-222">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="d8542-223">5**</span><span class="sxs-lookup"><span data-stu-id="d8542-223">5**</span></span> | <span data-ttu-id="d8542-224">Sunucu hataları</span><span class="sxs-lookup"><span data-stu-id="d8542-224">Server errors</span></span> |

<span data-ttu-id="d8542-225">Daha fazla bilgi için bkz: [cihaz çiftlerini Geliştirici Kılavuzu][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="d8542-225">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="receiving-desired-properties-update-notifications"></a><span data-ttu-id="d8542-226">Alıcı istenen özellikler güncelleştirme bildirimlerini</span><span class="sxs-lookup"><span data-stu-id="d8542-226">Receiving desired properties update notifications</span></span>

<span data-ttu-id="d8542-227">Bir aygıt bağlandığında, IOT hub'ı bildirimleri konu başlığına gönderir. `$iothub/twin/PATCH/properties/desired/?$version={new version}`, çözüm arka ucu tarafından gerçekleştirilen güncelleştirme içeriğini içerir.</span><span class="sxs-lookup"><span data-stu-id="d8542-227">When a device is connected, IoT Hub sends notifications to the topic `$iothub/twin/PATCH/properties/desired/?$version={new version}`, which contain the content of the update performed by the solution back end.</span></span> <span data-ttu-id="d8542-228">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="d8542-228">For example:</span></span>

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

<span data-ttu-id="d8542-229">Özelliği güncelleştirmeleri ettirilmesi `null` değerleri JSON nesnesi üye silinip silinmediğini anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="d8542-229">As for property updates, `null` values means that the JSON object member is being deleted.</span></span>


> [!IMPORTANT] 
> <span data-ttu-id="d8542-230">Yalnızca aygıtları bağlandığınızda IOT hub'ı değişiklik bildirimleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d8542-230">IoT Hub generates change notifications only when devices are connected.</span></span> <span data-ttu-id="d8542-231">Uygulanacak emin olun [aygıt yeniden bağlanmayı akış] [ lnk-devguide-twin-reconnection] IOT Hub ve cihaz uygulaması arasında eşitlenen istenen özellikleri tutmak için.</span><span class="sxs-lookup"><span data-stu-id="d8542-231">Make sure to implement the [device reconnection flow][lnk-devguide-twin-reconnection] to keep the desired properties synchronized between IoT Hub and the device app.</span></span>

<span data-ttu-id="d8542-232">Daha fazla bilgi için bkz: [cihaz çiftlerini Geliştirici Kılavuzu][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="d8542-232">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="respond-to-a-direct-method"></a><span data-ttu-id="d8542-233">Doğrudan bir yönteme yanıt</span><span class="sxs-lookup"><span data-stu-id="d8542-233">Respond to a direct method</span></span>

<span data-ttu-id="d8542-234">İlk olarak, bir abone olmak aygıtın `$iothub/methods/POST/#`.</span><span class="sxs-lookup"><span data-stu-id="d8542-234">First, a device has to subscribe to `$iothub/methods/POST/#`.</span></span> <span data-ttu-id="d8542-235">IOT hub'ı konuya yöntemi istekleri gönderir `$iothub/methods/POST/{method name}/?$rid={request id}`, ya geçerli bir JSON ya da boş bir gövde ile.</span><span class="sxs-lookup"><span data-stu-id="d8542-235">IoT Hub sends method requests to the topic `$iothub/methods/POST/{method name}/?$rid={request id}`, with either a valid JSON or an empty body.</span></span>

<span data-ttu-id="d8542-236">Cihaz yanıt vermek için konu ile geçerli JSON ya da boş gövdesi içeren bir ileti gönderir `$iothub/methods/res/{status}/?$rid={request id}`, burada **istek kimliği** bir istek iletisinde eşleşmelidir ve **durum** bir tamsayı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d8542-236">To respond, the device sends a message with a valid JSON or empty body to the topic `$iothub/methods/res/{status}/?$rid={request id}`, where **request id** has to match the one in the request message, and **status** has to be an integer.</span></span>

<span data-ttu-id="d8542-237">Daha fazla bilgi için bkz: [yöntemi Geliştirici Kılavuzu doğrudan][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="d8542-237">For more information, see [Direct method developer's guide][lnk-methods].</span></span>

### <a name="additional-considerations"></a><span data-ttu-id="d8542-238">Diğer konular</span><span class="sxs-lookup"><span data-stu-id="d8542-238">Additional considerations</span></span>

<span data-ttu-id="d8542-239">Son yaparken, bulut tarafındaki MQTT protokol davranışı özelleştirmeniz gerekiyorsa gözden geçirmeniz gereken [Azure IOT protokolü ağ geçidini] [ lnk-azure-protocol-gateway] yüksek performanslı özel dağıtmanıza olanak tanır doğrudan IOT Hub ile arabirimleri protokol ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="d8542-239">As a final consideration, if you need to customize the MQTT protocol behavior on the cloud side, you should review the [Azure IoT protocol gateway][lnk-azure-protocol-gateway] that enables you to deploy a high-performance custom protocol gateway that interfaces directly with IoT Hub.</span></span> <span data-ttu-id="d8542-240">Azure IOT protokolü ağ geçidini brownfield MQTT dağıtımları uyum sağlayacak şekilde cihaz protokolü veya diğer özel protokoller özelleştirmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="d8542-240">The Azure IoT protocol gateway enables you to customize the device protocol to accommodate brownfield MQTT deployments or other custom protocols.</span></span> <span data-ttu-id="d8542-241">Bu yaklaşım, ancak çalıştırın ve bir özel protokol ağ geçidi çalışmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d8542-241">This approach does require, however, that you run and operate a custom protocol gateway.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8542-242">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d8542-242">Next steps</span></span>

<span data-ttu-id="d8542-243">MQTT protokolü hakkında daha fazla bilgi için bkz: [MQTT belgelerine][lnk-mqtt-docs].</span><span class="sxs-lookup"><span data-stu-id="d8542-243">To learn more about the MQTT protocol, see the [MQTT documentation][lnk-mqtt-docs].</span></span>

<span data-ttu-id="d8542-244">IOT hub'ı dağıtımınızı planlama hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="d8542-244">To learn more about planning your IoT Hub deployment, see:</span></span>

* <span data-ttu-id="d8542-245">[IOT cihaz katalog için Azure Onaylandı][lnk-devices]</span><span class="sxs-lookup"><span data-stu-id="d8542-245">[Azure Certified for IoT device catalog][lnk-devices]</span></span>
* <span data-ttu-id="d8542-246">[Destek ek protokoller][lnk-protocols]</span><span class="sxs-lookup"><span data-stu-id="d8542-246">[Support additional protocols][lnk-protocols]</span></span>
* <span data-ttu-id="d8542-247">[Event Hubs ile karşılaştırın][lnk-compare]</span><span class="sxs-lookup"><span data-stu-id="d8542-247">[Compare with Event Hubs][lnk-compare]</span></span>
* <span data-ttu-id="d8542-248">[Ölçeklendirme, HA ve DR][lnk-scaling]</span><span class="sxs-lookup"><span data-stu-id="d8542-248">[Scaling, HA, and DR][lnk-scaling]</span></span>

<span data-ttu-id="d8542-249">Daha fazla IOT hub'ı özelliklerini keşfetmek için bkz:</span><span class="sxs-lookup"><span data-stu-id="d8542-249">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="d8542-250">[IOT Hub Geliştirici Kılavuzu][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="d8542-250">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="d8542-251">[Bir aygıt ile Azure IOT kenar benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="d8542-251">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
