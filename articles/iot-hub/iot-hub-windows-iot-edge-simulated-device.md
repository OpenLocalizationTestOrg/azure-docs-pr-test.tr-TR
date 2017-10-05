---
title: "Azure IOT kenar (Windows) bir cihazın benzetimini | Microsoft Docs"
description: "Azure IOT kenar Windows üzerinde bir IOT hub'ına bir Azure IOT sınır ağ geçidi üzerinden telemetri gönderen sanal bir cihaz oluşturmak için nasıl kullanılır."
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
ms.openlocfilehash: e7eb2931993daf3f0aecbd4a43d27ebd5adc10b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-iot-edge-to-send-device-to-cloud-messages-with-a-simulated-device-windows"></a><span data-ttu-id="42e30-103">Bir sanal cihaz (Windows) ile cihaz bulut iletilerini göndermek için Azure IOT kenar kullanın</span><span class="sxs-lookup"><span data-stu-id="42e30-103">Use Azure IoT Edge to send device-to-cloud messages with a simulated device (Windows)</span></span>

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-to-run-the-sample"></a><span data-ttu-id="42e30-104">Örneği çalıştırma</span><span class="sxs-lookup"><span data-stu-id="42e30-104">How to run the sample</span></span>

<span data-ttu-id="42e30-105">**Build.cmd** komut dosyası oluşturur, çıktı **yapı** yerel kopyasını klasöründe **IOT kenar** deposu.</span><span class="sxs-lookup"><span data-stu-id="42e30-105">The **build.cmd** script generates its output in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="42e30-106">Bu çıktı, bu örnekte kullanılan dört IOT kenar modüller içerir.</span><span class="sxs-lookup"><span data-stu-id="42e30-106">This output includes the four IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="42e30-107">Yapı betik basamak:</span><span class="sxs-lookup"><span data-stu-id="42e30-107">The build script places the:</span></span>

* <span data-ttu-id="42e30-108">**Logger.dll** içinde **yapı\\modülleri\\Günlükçü\\hata ayıklama** klasör.</span><span class="sxs-lookup"><span data-stu-id="42e30-108">**logger.dll** in the **build\\modules\\logger\\Debug** folder.</span></span>
* <span data-ttu-id="42e30-109">**iothub.dll** içinde **yapı\\modülleri\\ıothub\\hata ayıklama** klasör.</span><span class="sxs-lookup"><span data-stu-id="42e30-109">**iothub.dll** in the **build\\modules\\iothub\\Debug** folder.</span></span>
* <span data-ttu-id="42e30-110">**kimlik\_map.dll** içinde **yapı\\modülleri\\identitymap\\hata ayıklama** klasör.</span><span class="sxs-lookup"><span data-stu-id="42e30-110">**identity\_map.dll** in the **build\\modules\\identitymap\\Debug** folder.</span></span>
* <span data-ttu-id="42e30-111">**Benzetimli\_device.dll** içinde **yapı\\modülleri\\benzetimli\_aygıt\\hata ayıklama** klasör.</span><span class="sxs-lookup"><span data-stu-id="42e30-111">**simulated\_device.dll** in the **build\\modules\\simulated\_device\\Debug** folder.</span></span>

<span data-ttu-id="42e30-112">Bu yolları için kullanma **modül yolu** değerleri aşağıdaki JSON ayarları dosyasında gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="42e30-112">Use these paths for the **module path** values as shown in the following JSON settings file:</span></span>

<span data-ttu-id="42e30-113">Benzetimli\_aygıt\_bulut\_karşıya\_örnek işlemi komut satırı bağımsız değişkeni olarak bir JSON yapılandırma dosyasına yolunu alır.</span><span class="sxs-lookup"><span data-stu-id="42e30-113">The simulated\_device\_cloud\_upload\_sample process takes the path to a JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="42e30-114">Aşağıdaki örnek JSON dosyası SDK deposunda sağlanan **örnekleri\\benzetimli\_aygıt\_bulut\_karşıya\_örnek\\src\\ Benzetimli\_aygıt\_bulut\_karşıya\_örnek\_win.json**.</span><span class="sxs-lookup"><span data-stu-id="42e30-114">The following example JSON file is provided in the SDK repository at **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_win.json**.</span></span> <span data-ttu-id="42e30-115">Bu yapılandırma dosyası IOT kenar modülleri veya örnek yürütülebilir dosyalar varsayılan olmayan konumlara yerleştirmek için yapı betik değiştirmediğiniz sürece olduğu gibi çalışır.</span><span class="sxs-lookup"><span data-stu-id="42e30-115">This configuration file works as is unless you modify the build script to place the IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="42e30-116">Dizine göre modülü yollardır burada benzetimli\_aygıt\_bulut\_karşıya\_sample.exe bulunduğu.</span><span class="sxs-lookup"><span data-stu-id="42e30-116">The module paths are relative to the directory where the simulated\_device\_cloud\_upload\_sample.exe is located.</span></span> <span data-ttu-id="42e30-117">Örnek JSON yapılandırma dosyası, geçerli çalışma dizini içinde 'deviceCloudUploadGatewaylog.log' yazmak için varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="42e30-117">The sample JSON configuration file defaults to writing to 'deviceCloudUploadGatewaylog.log' in your current working directory.</span></span>

<span data-ttu-id="42e30-118">Dosyayı bir metin düzenleyicisinde açın **örnekleri\\benzetimli\_aygıt\_bulut\_karşıya\_örnek\\src\\benzetimli\_aygıt\_bulut\_karşıya\_win.json** yerel kopyasını içinde **IOT kenar** deposu.</span><span class="sxs-lookup"><span data-stu-id="42e30-118">In a text editor, open the file **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_win.json** in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="42e30-119">Bu dosya IOT kenar modüllerini örnek ağ geçidi yapılandırır:</span><span class="sxs-lookup"><span data-stu-id="42e30-119">This file configures the IoT Edge modules in the sample gateway:</span></span>

* <span data-ttu-id="42e30-120">**Iothub** modülü IOT hub'ınıza bağlanır.</span><span class="sxs-lookup"><span data-stu-id="42e30-120">The **IoTHub** module connects to your IoT hub.</span></span> <span data-ttu-id="42e30-121">IOT hub'ınıza veri göndermek için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="42e30-121">You configure it to send data to your IoT hub.</span></span> <span data-ttu-id="42e30-122">Özellikle, ayarlanan **IoTHubName** değerini IOT hub'ınızın adını ve ayarlayın **IoTHubSuffix** değeri **azure devices.net**.</span><span class="sxs-lookup"><span data-stu-id="42e30-122">Specifically, set the **IoTHubName** value to the name of your IoT hub and set the **IoTHubSuffix** value to **azure-devices.net**.</span></span> <span data-ttu-id="42e30-123">Ayarlama **aktarım** değeri birine: **HTTP**, **AMQP**, veya **MQTT**.</span><span class="sxs-lookup"><span data-stu-id="42e30-123">Set the **Transport** value to one of: **HTTP**, **AMQP**, or **MQTT**.</span></span> <span data-ttu-id="42e30-124">Şu anda yalnızca **HTTP** tüm aygıt iletiler için bir TCP bağlantısı paylaşır.</span><span class="sxs-lookup"><span data-stu-id="42e30-124">Currently, only **HTTP** shares one TCP connection for all device messages.</span></span> <span data-ttu-id="42e30-125">Değeri ayarlarsanız verilen **AMQP**, veya **MQTT**, IOT hub'ı her aygıt için ayrı bir TCP bağlantı ağ geçidi korur.</span><span class="sxs-lookup"><span data-stu-id="42e30-125">If you set the value to **AMQP**, or **MQTT**, the gateway maintains a separate TCP connection to IoT Hub for each device.</span></span>
* <span data-ttu-id="42e30-126">**Eşleme** modülü IOT Hub cihaz kimliklerinizi sanal cihazlarınızın MAC adreslerini eşler.</span><span class="sxs-lookup"><span data-stu-id="42e30-126">The **mapping** module maps the MAC addresses of your simulated devices to your IoT Hub device ids.</span></span> <span data-ttu-id="42e30-127">Olduğundan emin olun **DeviceID** değerleriyle eşleşen IOT hub'ınızı ve, eklediğiniz iki aygıtların kimliklerini **deviceKey** değerleri içeren iki aygıtlarınızın anahtarları.</span><span class="sxs-lookup"><span data-stu-id="42e30-127">Make sure that **deviceId** values match the ids of the two devices you added to your IoT hub, and that the **deviceKey** values contain the keys of your two devices.</span></span>
* <span data-ttu-id="42e30-128">**BLE1** ve **BLE2** modüllerdir sanal cihazlar.</span><span class="sxs-lookup"><span data-stu-id="42e30-128">The **BLE1** and **BLE2** modules are the simulated devices.</span></span> <span data-ttu-id="42e30-129">Nasıl modülü MAC adresleri eşleşen Not **eşleme** modülü.</span><span class="sxs-lookup"><span data-stu-id="42e30-129">Note how the module MAC addresses match the addresses in the **mapping** module.</span></span>
* <span data-ttu-id="42e30-130">**Günlükçü** modülü, ağ geçidi etkinliği bir dosyaya kaydeder.</span><span class="sxs-lookup"><span data-stu-id="42e30-130">The **Logger** module logs your gateway activity to a file.</span></span>
* <span data-ttu-id="42e30-131">**Modül yolu** aşağıdaki örnekte gösterilen göre dizin değerlerdir burada benzetimli\_aygıt\_bulut\_karşıya\_sample.exe bulunduğu.</span><span class="sxs-lookup"><span data-stu-id="42e30-131">The **module path** values shown in the following example are relative to the directory where the simulated\_device\_cloud\_upload\_sample.exe is located.</span></span>
* <span data-ttu-id="42e30-132">**Bağlantılar** dizi JSON dosyasının sonuna bağlayan **BLE1** ve **BLE2** modüllerini **eşleme** modülü ve **eşleme** modülüne **Iothub** modülü.</span><span class="sxs-lookup"><span data-stu-id="42e30-132">The **links** array at the bottom of the JSON file connects the **BLE1** and **BLE2** modules to the **mapping** module, and the **mapping** module to the **IoTHub** module.</span></span> <span data-ttu-id="42e30-133">Ayrıca tüm iletileri tarafından kaydedilir sağlar **Günlükçü** modülü.</span><span class="sxs-lookup"><span data-stu-id="42e30-133">It also ensures that all messages are logged by the **Logger** module.</span></span>

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

<span data-ttu-id="42e30-134">Yapılandırma dosyasına yapılan değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="42e30-134">Save the changes you made to the configuration file.</span></span>

<span data-ttu-id="42e30-135">Örneği çalıştırmak için:</span><span class="sxs-lookup"><span data-stu-id="42e30-135">To run the sample:</span></span>

1. <span data-ttu-id="42e30-136">Bir komut isteminde gidin **yapı** yerel kopyasını klasöründe **IOT kenar** deposu.</span><span class="sxs-lookup"><span data-stu-id="42e30-136">At a command prompt, navigate to the **build** folder in your local copy of the **iot-edge** repository.</span></span>
2. <span data-ttu-id="42e30-137">Şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="42e30-137">Run the following command:</span></span>
   
    ```cmd
    samples\simulated_device_cloud_upload\Debug\simulated_device_cloud_upload_sample.exe ..\samples\simulated_device_cloud_upload\src\simulated_device_cloud_upload_win.json
    ```
3. <span data-ttu-id="42e30-138">Kullanabileceğiniz [aygıt explorer] [ lnk-device-explorer] veya [iothub-explorer] [ lnk-iothub-explorer] ağ geçidi'nden IOT hub'ınızın aldığı iletileri izlemek için aracı.</span><span class="sxs-lookup"><span data-stu-id="42e30-138">You can use the [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool to monitor the messages that IoT hub receives from the gateway.</span></span> <span data-ttu-id="42e30-139">Örneğin, ıothub explorer kullanarak aşağıdaki komutu kullanarak cihaz bulut iletilerini izleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="42e30-139">For example, using iothub-explorer you can monitor device-to-cloud messages using the following command:</span></span>

    ```cmd
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a><span data-ttu-id="42e30-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="42e30-140">Next steps</span></span>

<span data-ttu-id="42e30-141">IOT kenar daha gelişmiş anlamak ve bazı kod örnekleri ile denemek için aşağıdaki Geliştirici öğreticiler ve kaynakları ziyaret edin:</span><span class="sxs-lookup"><span data-stu-id="42e30-141">To gain a more advanced understanding of IoT Edge and experiment with some code examples, visit the following developer tutorials and resources:</span></span>

* <span data-ttu-id="42e30-142">[IOT Edge fiziksel CİHAZDAN cihaz bulut iletilerini gönder][lnk-physical-device]</span><span class="sxs-lookup"><span data-stu-id="42e30-142">[Send device-to-cloud messages from a physical device with IoT Edge][lnk-physical-device]</span></span>
* <span data-ttu-id="42e30-143">[Azure IOT kenar][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="42e30-143">[Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="42e30-144">Daha fazla IOT hub'ı özelliklerini keşfetmek için bkz:</span><span class="sxs-lookup"><span data-stu-id="42e30-144">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="42e30-145">[IOT Hub Geliştirici Kılavuzu][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="42e30-145">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="42e30-146">[IOT çözümünüzden zemin oluşturan güvenli][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="42e30-146">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md