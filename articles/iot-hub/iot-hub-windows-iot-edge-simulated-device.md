---
title: "Azure IOT kenar (Windows) aygıtıyla aaaSimulate | Microsoft Docs"
description: "Nasıl toouse Azure IOT kenar Windows toocreate sanal bir cihaz üzerinde bir Azure IOT sınır ağ geçidi tooan IOT hub'ı aracılığıyla telemetri gönderir."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 6a2aeda0-696a-4732-90e1-595d2e2fadc6
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: andbuc
ms.openlocfilehash: ddbe85eb956e9934e80e2e80e09f77b24cf54856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-toosend-device-to-cloud-messages-with-a-simulated-device-windows"></a><span data-ttu-id="5c002-103">Bir sanal cihaz (Windows) ile Azure IOT kenar toosend cihaz bulut iletilerini kullanın</span><span class="sxs-lookup"><span data-stu-id="5c002-103">Use Azure IoT Edge toosend device-to-cloud messages with a simulated device (Windows)</span></span>

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="5c002-104">Nasıl toorun hello örnek</span><span class="sxs-lookup"><span data-stu-id="5c002-104">How toorun hello sample</span></span>

<span data-ttu-id="5c002-105">Merhaba **build.cmd** betik hello çıktısını oluşturur **yapı** hello yerel kopyasını klasöründe **IOT kenar** deposu.</span><span class="sxs-lookup"><span data-stu-id="5c002-105">hello **build.cmd** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="5c002-106">Bu çıktı, bu örnekte kullanılan hello dört IOT kenar modüller içerir.</span><span class="sxs-lookup"><span data-stu-id="5c002-106">This output includes hello four IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="5c002-107">Merhaba yapı betik basamak:</span><span class="sxs-lookup"><span data-stu-id="5c002-107">hello build script places the:</span></span>

* <span data-ttu-id="5c002-108">**Logger.dll** hello içinde **yapı\\modülleri\\Günlükçü\\hata ayıklama** klasör.</span><span class="sxs-lookup"><span data-stu-id="5c002-108">**logger.dll** in hello **build\\modules\\logger\\Debug** folder.</span></span>
* <span data-ttu-id="5c002-109">**iothub.dll** hello içinde **yapı\\modülleri\\ıothub\\hata ayıklama** klasör.</span><span class="sxs-lookup"><span data-stu-id="5c002-109">**iothub.dll** in hello **build\\modules\\iothub\\Debug** folder.</span></span>
* <span data-ttu-id="5c002-110">**kimlik\_map.dll** hello içinde **yapı\\modülleri\\identitymap\\hata ayıklama** klasör.</span><span class="sxs-lookup"><span data-stu-id="5c002-110">**identity\_map.dll** in hello **build\\modules\\identitymap\\Debug** folder.</span></span>
* <span data-ttu-id="5c002-111">**Benzetimli\_device.dll** hello içinde **yapı\\modülleri\\benzetimli\_aygıt\\hata ayıklama** klasör.</span><span class="sxs-lookup"><span data-stu-id="5c002-111">**simulated\_device.dll** in hello **build\\modules\\simulated\_device\\Debug** folder.</span></span>

<span data-ttu-id="5c002-112">Bu yolları Merhaba kullanma **modül yolu** değerleri aşağıdaki JSON ayarları dosyasına hello gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="5c002-112">Use these paths for hello **module path** values as shown in hello following JSON settings file:</span></span>

<span data-ttu-id="5c002-113">Benzetimli hello\_aygıt\_bulut\_karşıya\_örnek işlemi hello yol tooa JSON yapılandırma dosyası komut satırı bağımsız değişkeni olarak alır.</span><span class="sxs-lookup"><span data-stu-id="5c002-113">hello simulated\_device\_cloud\_upload\_sample process takes hello path tooa JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="5c002-114">Merhaba aşağıdaki örnek JSON dosyası hello SDK deposu sırasında sağlanan **örnekleri\\benzetimli\_aygıt\_bulut\_karşıya\_örnek\\src\\ Benzetimli\_aygıt\_bulut\_karşıya\_örnek\_win.json**.</span><span class="sxs-lookup"><span data-stu-id="5c002-114">hello following example JSON file is provided in hello SDK repository at **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_win.json**.</span></span> <span data-ttu-id="5c002-115">Merhaba değiştirmediğiniz sürece olduğundan bu yapılandırma dosyası works betik tooplace hello IOT kenar modülleri oluşturabilir veya yürütülebilir dosyalar varsayılan olmayan konumlarda örnek.</span><span class="sxs-lookup"><span data-stu-id="5c002-115">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="5c002-116">Merhaba modülü burada hello benzetimli göreli toohello dizin yollardır\_aygıt\_bulut\_karşıya\_sample.exe bulunduğu.</span><span class="sxs-lookup"><span data-stu-id="5c002-116">hello module paths are relative toohello directory where hello simulated\_device\_cloud\_upload\_sample.exe is located.</span></span> <span data-ttu-id="5c002-117">Merhaba örnek JSON yapılandırma dosyası varsayılan olarak toowriting too'deviceCloudUploadGatewaylog.log', geçerli çalışma dizininde.</span><span class="sxs-lookup"><span data-stu-id="5c002-117">hello sample JSON configuration file defaults toowriting too'deviceCloudUploadGatewaylog.log' in your current working directory.</span></span>

<span data-ttu-id="5c002-118">Merhaba dosyasını bir metin düzenleyicisinde açın **örnekleri\\benzetimli\_aygıt\_bulut\_karşıya\_örnek\\src\\benzetimli\_aygıt \_bulut\_karşıya\_win.json** hello yerel kopyasını içinde **IOT kenar** deposu.</span><span class="sxs-lookup"><span data-stu-id="5c002-118">In a text editor, open hello file **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_win.json** in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="5c002-119">Bu dosya hello IOT kenar modüllerini hello örnek ağ geçidi yapılandırır:</span><span class="sxs-lookup"><span data-stu-id="5c002-119">This file configures hello IoT Edge modules in hello sample gateway:</span></span>

* <span data-ttu-id="5c002-120">Merhaba **Iothub** modülü tooyour IOT hub'ı bağlar.</span><span class="sxs-lookup"><span data-stu-id="5c002-120">hello **IoTHub** module connects tooyour IoT hub.</span></span> <span data-ttu-id="5c002-121">Bu toosend veri tooyour IOT hub'ı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5c002-121">You configure it toosend data tooyour IoT hub.</span></span> <span data-ttu-id="5c002-122">Özellikle, kümesi hello **IoTHubName** değer toohello adı IOT hub'ınızın ve ayarlayın hello **IoTHubSuffix** çok değer**azure devices.net**.</span><span class="sxs-lookup"><span data-stu-id="5c002-122">Specifically, set hello **IoTHubName** value toohello name of your IoT hub and set hello **IoTHubSuffix** value too**azure-devices.net**.</span></span> <span data-ttu-id="5c002-123">Set hello **aktarım** , değer tooone: **HTTP**, **AMQP**, veya **MQTT**.</span><span class="sxs-lookup"><span data-stu-id="5c002-123">Set hello **Transport** value tooone of: **HTTP**, **AMQP**, or **MQTT**.</span></span> <span data-ttu-id="5c002-124">Şu anda yalnızca **HTTP** tüm aygıt iletiler için bir TCP bağlantısı paylaşır.</span><span class="sxs-lookup"><span data-stu-id="5c002-124">Currently, only **HTTP** shares one TCP connection for all device messages.</span></span> <span data-ttu-id="5c002-125">Merhaba değeri çok ayarlarsanız**AMQP**, veya **MQTT**, hello ağ geçidi bir ayrı TCP bağlantısı tooIoT Hub her aygıt için korur.</span><span class="sxs-lookup"><span data-stu-id="5c002-125">If you set hello value too**AMQP**, or **MQTT**, hello gateway maintains a separate TCP connection tooIoT Hub for each device.</span></span>
* <span data-ttu-id="5c002-126">Merhaba **eşleme** modülü sanal cihazlar tooyour IOT Hub cihaz kimliklerinizi hello MAC adreslerini eşler.</span><span class="sxs-lookup"><span data-stu-id="5c002-126">hello **mapping** module maps hello MAC addresses of your simulated devices tooyour IoT Hub device ids.</span></span> <span data-ttu-id="5c002-127">Olduğundan emin olun **DeviceID** değerleri Eşleştir hello kimliklerini hello tooyour IOT hub ve o hello eklediğiniz iki aygıtları **deviceKey** değerleri içeren iki aygıtlarınızın hello anahtarları.</span><span class="sxs-lookup"><span data-stu-id="5c002-127">Make sure that **deviceId** values match hello ids of hello two devices you added tooyour IoT hub, and that hello **deviceKey** values contain hello keys of your two devices.</span></span>
* <span data-ttu-id="5c002-128">Merhaba **BLE1** ve **BLE2** modüllerdir benzetimli hello aygıtlar.</span><span class="sxs-lookup"><span data-stu-id="5c002-128">hello **BLE1** and **BLE2** modules are hello simulated devices.</span></span> <span data-ttu-id="5c002-129">Nasıl hello modülü MAC adresleri hello hello eşleşen Not **eşleme** modülü.</span><span class="sxs-lookup"><span data-stu-id="5c002-129">Note how hello module MAC addresses match hello addresses in hello **mapping** module.</span></span>
* <span data-ttu-id="5c002-130">Merhaba **Günlükçü** modülü, ağ geçidi etkinliği tooa dosyanızı günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="5c002-130">hello **Logger** module logs your gateway activity tooa file.</span></span>
* <span data-ttu-id="5c002-131">Merhaba **modül yolu** aşağıdaki örneğine hello gösterilen burada hello benzetimli göreli toohello dizin değerlerdir\_aygıt\_bulut\_karşıya\_sample.exe bulunduğu.</span><span class="sxs-lookup"><span data-stu-id="5c002-131">hello **module path** values shown in hello following example are relative toohello directory where hello simulated\_device\_cloud\_upload\_sample.exe is located.</span></span>
* <span data-ttu-id="5c002-132">Merhaba **bağlantılar** dizi hello JSON dosyasının hello altındaki bağlayan hello **BLE1** ve **BLE2** modülleri toohello **eşleme** modülü ve hello **eşleme** modülü toohello **Iothub** modülü.</span><span class="sxs-lookup"><span data-stu-id="5c002-132">hello **links** array at hello bottom of hello JSON file connects hello **BLE1** and **BLE2** modules toohello **mapping** module, and hello **mapping** module toohello **IoTHub** module.</span></span> <span data-ttu-id="5c002-133">Ayrıca tüm iletileri hello tarafından günlüğe kaydedilen sağlar **Günlükçü** modülü.</span><span class="sxs-lookup"><span data-stu-id="5c002-133">It also ensures that all messages are logged by hello **Logger** module.</span></span>

```json
{
    "modules" :
    [
      {
        "name": "IotHub",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\iothub\\Debug\\iothub.dll"
          }
          },
          "args": {
            "IoTHubName": "<<insert here IoTHubName>>",
            "IoTHubSuffix": "<<insert here IoTHubSuffix>>",
            "Transport": "HTTP"
          }
        },
      {
        "name": "mapping",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\identitymap\\Debug\\identity_map.dll"
          }
          },
          "args": [
            {
              "macAddress": "01:01:01:01:01:01",
              "deviceId": "<<insert here deviceId>>",
              "deviceKey": "<<insert here deviceKey>>"
            },
            {
              "macAddress": "02:02:02:02:02:02",
              "deviceId": "<<insert here deviceId>>",
              "deviceKey": "<<insert here deviceKey>>"
            }
          ]
        },
      {
        "name": "BLE1",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\simulated_device\\Debug\\simulated_device.dll"
          }
          },
          "args": {
            "macAddress": "01:01:01:01:01:01"
          }
        },
      {
        "name": "BLE2",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\simulated_device\\Debug\\simulated_device.dll"
          }
          },
          "args": {
            "macAddress": "02:02:02:02:02:02"
          }
        },
      {
        "name": "Logger",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\logger\\Debug\\logger.dll"
          }
        },
        "args": {
          "filename": "deviceCloudUploadGatewaylog.log"
        }
      }
    ],
    "links" : [
        { "source" : "*", "sink" : "Logger" },
        { "source" : "BLE1", "sink" : "mapping" },
        { "source" : "BLE2", "sink" : "mapping" },
        { "source" : "mapping", "sink" : "IotHub" }
    ]
}
```

<span data-ttu-id="5c002-134">Toohello yapılandırma dosyası yaptığınız Hello Değişiklikleri Kaydet.</span><span class="sxs-lookup"><span data-stu-id="5c002-134">Save hello changes you made toohello configuration file.</span></span>

<span data-ttu-id="5c002-135">toorun hello örneği:</span><span class="sxs-lookup"><span data-stu-id="5c002-135">toorun hello sample:</span></span>

1. <span data-ttu-id="5c002-136">Bir komut isteminde toohello gidin **yapı** hello yerel kopyasını klasöründe **IOT kenar** deposu.</span><span class="sxs-lookup"><span data-stu-id="5c002-136">At a command prompt, navigate toohello **build** folder in your local copy of hello **iot-edge** repository.</span></span>
2. <span data-ttu-id="5c002-137">Merhaba aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="5c002-137">Run hello following command:</span></span>
   
    ```cmd
    samples\simulated_device_cloud_upload\Debug\simulated_device_cloud_upload_sample.exe ..\samples\simulated_device_cloud_upload\src\simulated_device_cloud_upload_win.json
    ```
3. <span data-ttu-id="5c002-138">Merhaba kullanabilirsiniz [aygıt explorer] [ lnk-device-explorer] veya [iothub-explorer] [ lnk-iothub-explorer] aracı hello IOT hub'ınızın aldığı toomonitor karışılama iletileri ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="5c002-138">You can use hello [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool toomonitor hello messages that IoT hub receives from hello gateway.</span></span> <span data-ttu-id="5c002-139">Örneğin, ıothub explorer kullanarak cihaz bulut iletilerini komutu aşağıdaki hello kullanarak izleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5c002-139">For example, using iothub-explorer you can monitor device-to-cloud messages using hello following command:</span></span>

    ```cmd
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a><span data-ttu-id="5c002-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5c002-140">Next steps</span></span>

<span data-ttu-id="5c002-141">toogain IOT kenarı ve deneme daha gelişmiş bir anlayış bazı kod örnekleri ile ziyaret hello aşağıdaki Geliştirici öğreticiler ve kaynaklar:</span><span class="sxs-lookup"><span data-stu-id="5c002-141">toogain a more advanced understanding of IoT Edge and experiment with some code examples, visit hello following developer tutorials and resources:</span></span>

* <span data-ttu-id="5c002-142">[IOT Edge fiziksel CİHAZDAN cihaz bulut iletilerini gönder][lnk-physical-device]</span><span class="sxs-lookup"><span data-stu-id="5c002-142">[Send device-to-cloud messages from a physical device with IoT Edge][lnk-physical-device]</span></span>
* <span data-ttu-id="5c002-143">[Azure IOT kenar][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="5c002-143">[Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="5c002-144">toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:</span><span class="sxs-lookup"><span data-stu-id="5c002-144">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="5c002-145">[IOT Hub Geliştirici Kılavuzu][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="5c002-145">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="5c002-146">[IOT çözümünüzden plan hello güvenli][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="5c002-146">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md