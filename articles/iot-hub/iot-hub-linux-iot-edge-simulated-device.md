---
title: "Azure IOT kenar (Linux) bir cihazın benzetimini | Microsoft Docs"
description: "Azure IOT kenar Linux'ta bir IOT hub'ına bir IOT sınır ağ geçidi üzerinden telemetri gönderen sanal bir cihaz oluşturma için nasıl kullanılacağını."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 11e7bf28-ee3d-48d6-a386-eb506c7a31cf
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: andbuc
ms.openlocfilehash: 5349960373ae6815862c5f79a69dd6d5d9d624ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-iot-edge-to-send-device-to-cloud-messages-with-a-simulated-device-linux"></a><span data-ttu-id="53ee3-103">Bir sanal cihaz (Linux) ile cihaz bulut iletilerini göndermek için Azure IOT kenar kullanın</span><span class="sxs-lookup"><span data-stu-id="53ee3-103">Use Azure IoT Edge to send device-to-cloud messages with a simulated device (Linux)</span></span>

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-to-run-the-sample"></a><span data-ttu-id="53ee3-104">Örneği çalıştırma</span><span class="sxs-lookup"><span data-stu-id="53ee3-104">How to run the sample</span></span>

<span data-ttu-id="53ee3-105">**build.sh** betiği, çıktısını **iot-edge** deposu yerel kopyasının **build** klasöründe oluşturur.</span><span class="sxs-lookup"><span data-stu-id="53ee3-105">The **build.sh** script generates its output in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="53ee3-106">Bu çıktı, bu örnekte kullanılan dört IOT kenar modüller içerir.</span><span class="sxs-lookup"><span data-stu-id="53ee3-106">This output includes the four IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="53ee3-107">Yapı betik basamak:</span><span class="sxs-lookup"><span data-stu-id="53ee3-107">The build script places the:</span></span>

* <span data-ttu-id="53ee3-108">**liblogger.SO** içinde **modülleri/yapı/Günlükçü** klasör.</span><span class="sxs-lookup"><span data-stu-id="53ee3-108">**liblogger.so** in the **build/modules/logger** folder.</span></span>
* <span data-ttu-id="53ee3-109">**libiothub.SO** içinde **modülleri/yapı/ıothub** klasör.</span><span class="sxs-lookup"><span data-stu-id="53ee3-109">**libiothub.so** in the **build/modules/iothub** folder.</span></span>
* <span data-ttu-id="53ee3-110">**LIB\_kimlik\_map.so** içinde **modülleri/yapı/identitymap** klasör.</span><span class="sxs-lookup"><span data-stu-id="53ee3-110">**lib\_identity\_map.so** in the **build/modules/identitymap** folder.</span></span>
* <span data-ttu-id="53ee3-111">**libsimulated\_device.so** içinde **yapı/modülleri/benzetimli\_aygıt** klasör.</span><span class="sxs-lookup"><span data-stu-id="53ee3-111">**libsimulated\_device.so** in the **build/modules/simulated\_device** folder.</span></span>

<span data-ttu-id="53ee3-112">Bu yolları için kullanma **modül yolu** değerleri aşağıdaki JSON ayarları dosyasında gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="53ee3-112">Use these paths for the **module path** values as shown in the following JSON settings file:</span></span>

<span data-ttu-id="53ee3-113">Benzetimli\_aygıt\_bulut\_karşıya\_örnek işlemi komut satırı bağımsız değişkeni olarak bir JSON yapılandırma dosyasına yolunu alır.</span><span class="sxs-lookup"><span data-stu-id="53ee3-113">The simulated\_device\_cloud\_upload\_sample process takes the path to a JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="53ee3-114">Aşağıdaki örnek JSON dosyası SDK deposunda sağlanan **örnekleri\\benzetimli\_aygıt\_bulut\_karşıya\_örnek\\src\\ Benzetimli\_aygıt\_bulut\_karşıya\_örnek\_lin.json**.</span><span class="sxs-lookup"><span data-stu-id="53ee3-114">The following example JSON file is provided in the SDK repository at **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_lin.json**.</span></span> <span data-ttu-id="53ee3-115">Bu yapılandırma dosyası IOT kenar modülleri veya örnek yürütülebilir dosyalar varsayılan olmayan konumlara yerleştirmek için yapı betik değiştirmediğiniz sürece olduğu gibi çalışır.</span><span class="sxs-lookup"><span data-stu-id="53ee3-115">This configuration file works as is unless you modify the build script to place the IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="53ee3-116">Modül benzetimli çalıştırdığınız gelen dizine göreli yollardır\_aygıt\_bulut\_karşıya\_örnek yürütülebilir, yürütülebilir dosyanın bulunduğu dizin değil.</span><span class="sxs-lookup"><span data-stu-id="53ee3-116">The module paths are relative to the directory from where you run the simulated\_device\_cloud\_upload\_sample executable, not the directory where the executable is located.</span></span> <span data-ttu-id="53ee3-117">Örnek JSON yapılandırma dosyası, geçerli çalışma dizini içinde 'deviceCloudUploadGatewaylog.log' yazmak için varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="53ee3-117">The sample JSON configuration file defaults to writing to 'deviceCloudUploadGatewaylog.log' in your current working directory.</span></span>

<span data-ttu-id="53ee3-118">Dosyayı bir metin düzenleyicisinde açın **örnekleri ve benzetimli\_aygıt\_bulut\_karşıya\_örnek/src/benzetimli\_aygıt\_bulut\_KarşıyaYükle\_lin.json** yerel kopyasını içinde **IOT kenar** deposu.</span><span class="sxs-lookup"><span data-stu-id="53ee3-118">In a text editor, open the file **samples/simulated\_device\_cloud\_upload\_sample/src/simulated\_device\_cloud\_upload\_lin.json** in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="53ee3-119">Bu dosya IOT kenar modüllerini örnek ağ geçidi yapılandırır:</span><span class="sxs-lookup"><span data-stu-id="53ee3-119">This file configures the IoT Edge modules in the sample gateway:</span></span>

* <span data-ttu-id="53ee3-120">**Iothub** modülü IOT hub'ınıza bağlanır.</span><span class="sxs-lookup"><span data-stu-id="53ee3-120">The **IoTHub** module connects to your IoT hub.</span></span> <span data-ttu-id="53ee3-121">IOT hub'ınıza veri göndermek için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="53ee3-121">You configure it to send data to your IoT hub.</span></span> <span data-ttu-id="53ee3-122">Özellikle, ayarlanan **IoTHubName** değerini IOT hub'ınızın adını ve ayarlayın **IoTHubSuffix** değeri **azure devices.net**.</span><span class="sxs-lookup"><span data-stu-id="53ee3-122">Specifically, set the **IoTHubName** value to the name of your IoT hub and set the **IoTHubSuffix** value to **azure-devices.net**.</span></span> <span data-ttu-id="53ee3-123">Ayarlama **aktarım** değeri birine: **HTTP**, **AMQP**, veya **MQTT**.</span><span class="sxs-lookup"><span data-stu-id="53ee3-123">Set the **Transport** value to one of: **HTTP**, **AMQP**, or **MQTT**.</span></span> <span data-ttu-id="53ee3-124">Şu anda yalnızca **HTTP** tüm aygıt iletiler için bir TCP bağlantısı paylaşır.</span><span class="sxs-lookup"><span data-stu-id="53ee3-124">Currently, only **HTTP** shares one TCP connection for all device messages.</span></span> <span data-ttu-id="53ee3-125">Değeri ayarlarsanız verilen **AMQP**, veya **MQTT**, IOT hub'ı her aygıt için ayrı bir TCP bağlantı ağ geçidi korur.</span><span class="sxs-lookup"><span data-stu-id="53ee3-125">If you set the value to **AMQP**, or **MQTT**, the gateway maintains a separate TCP connection to IoT Hub for each device.</span></span>
* <span data-ttu-id="53ee3-126">**Eşleme** modülü IOT Hub cihaz kimliklerinizi sanal cihazlarınızın MAC adreslerini eşler.</span><span class="sxs-lookup"><span data-stu-id="53ee3-126">The **mapping** module maps the MAC addresses of your simulated devices to your IoT Hub device ids.</span></span> <span data-ttu-id="53ee3-127">Olduğundan emin olun **DeviceID** değerleriyle eşleşen IOT hub'ınızı ve, eklediğiniz iki aygıtların kimliklerini **deviceKey** değerleri içeren iki aygıtlarınızın anahtarları.</span><span class="sxs-lookup"><span data-stu-id="53ee3-127">Make sure that **deviceId** values match the ids of the two devices you added to your IoT hub, and that the **deviceKey** values contain the keys of your two devices.</span></span>
* <span data-ttu-id="53ee3-128">**BLE1** ve **BLE2** modüllerdir sanal cihazlar.</span><span class="sxs-lookup"><span data-stu-id="53ee3-128">The **BLE1** and **BLE2** modules are the simulated devices.</span></span> <span data-ttu-id="53ee3-129">Nasıl MAC adreslerini eşleşen Not **eşleme** modülü.</span><span class="sxs-lookup"><span data-stu-id="53ee3-129">Note how their MAC addresses match the addresses in the **mapping** module.</span></span>
* <span data-ttu-id="53ee3-130">**Günlükçü** modülü, ağ geçidi etkinliği bir dosyaya kaydeder.</span><span class="sxs-lookup"><span data-stu-id="53ee3-130">The **Logger** module logs your gateway activity to a file.</span></span>
* <span data-ttu-id="53ee3-131">**Modül yolu** örnekte gösterilen değerleri varsayın örnek alarak çalıştırın **yapı** yerel kopyasını klasöründe **IOT kenar** deposu.</span><span class="sxs-lookup"><span data-stu-id="53ee3-131">The **module path** values shown in the example assume that you run the sample from the **build** folder in your local copy of the **iot-edge** repository.</span></span>
* <span data-ttu-id="53ee3-132">**Bağlantılar** dizi JSON dosyasının sonuna bağlayan **BLE1** ve **BLE2** modüllerini **eşleme** modülü ve **eşleme** modülüne **Iothub** modülü.</span><span class="sxs-lookup"><span data-stu-id="53ee3-132">The **links** array at the bottom of the JSON file connects the **BLE1** and **BLE2** modules to the **mapping** module, and the **mapping** module to the **IoTHub** module.</span></span> <span data-ttu-id="53ee3-133">Ayrıca tüm iletileri tarafından kaydedilir sağlar **Günlükçü** modülü.</span><span class="sxs-lookup"><span data-stu-id="53ee3-133">It also ensures that all messages are logged by the **Logger** module.</span></span>

```json
{
    "modules": [
        {
            "name": "IotHub",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/iothub/libiothub.so"
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
              "module.path": "./modules/identitymap/libidentity_map.so"
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
              "module.path": "./modules/simulated_device/libsimulated_device.so"
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
              "module.path": "./modules/simulated_device/libsimulated_device.so"
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
              "module.path": "./modules/logger/liblogger.so"
            }
            },
            "args": {
              "filename": "deviceCloudUploadGatewaylog.log"
            }
          }
    ],
    "links": [
        {
            "source": "*",
            "sink": "Logger"
        },
        {
            "source": "BLE1",
            "sink": "mapping"
        },
        {
            "source": "BLE2",
            "sink": "mapping"
        },
        {
            "source": "mapping",
            "sink": "IotHub"
        }
    ]
}
```

<span data-ttu-id="53ee3-134">Yapılandırma dosyasına yapılan değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="53ee3-134">Save the changes you made to the configuration file.</span></span>

<span data-ttu-id="53ee3-135">Örneği çalıştırmak için:</span><span class="sxs-lookup"><span data-stu-id="53ee3-135">To run the sample:</span></span>

1. <span data-ttu-id="53ee3-136">Kabuğunda gidin **IOT-edge/yapı** klasör.</span><span class="sxs-lookup"><span data-stu-id="53ee3-136">In your shell, navigate to the **iot-edge/build** folder.</span></span>
2. <span data-ttu-id="53ee3-137">Şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="53ee3-137">Run the following command:</span></span>
   
    ```sh
    ./samples/simulated_device_cloud_upload/simulated_device_cloud_upload_sample ../samples/simulated_device_cloud_upload/src/simulated_device_cloud_upload_lin.json
    ```
3. <span data-ttu-id="53ee3-138">Kullanabileceğiniz [aygıt explorer] [ lnk-device-explorer] veya [iothub-explorer] [ lnk-iothub-explorer] ağ geçidi'nden IOT hub'ınızın aldığı iletileri izlemek için aracı.</span><span class="sxs-lookup"><span data-stu-id="53ee3-138">You can use the [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool to monitor the messages that IoT hub receives from the gateway.</span></span> <span data-ttu-id="53ee3-139">Örneğin, ıothub explorer kullanarak aşağıdaki komutu kullanarak cihaz bulut iletilerini izleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="53ee3-139">For example, using iothub-explorer you can monitor device-to-cloud messages using the following command:</span></span>

    ```sh
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a><span data-ttu-id="53ee3-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="53ee3-140">Next steps</span></span>

<span data-ttu-id="53ee3-141">Azure IOT kenar daha gelişmiş anlamak ve bazı kod örnekleri ile denemek için aşağıdaki Geliştirici öğreticiler ve kaynakları ziyaret edin:</span><span class="sxs-lookup"><span data-stu-id="53ee3-141">To gain a more advanced understanding of Azure IoT Edge and experiment with some code examples, visit the following developer tutorials and resources:</span></span>

* <span data-ttu-id="53ee3-142">[Azure IOT Edge fiziksel CİHAZDAN cihaz bulut iletilerini gönder][lnk-physical-device]</span><span class="sxs-lookup"><span data-stu-id="53ee3-142">[Send device-to-cloud messages from a physical device with Azure IoT Edge][lnk-physical-device]</span></span>
* <span data-ttu-id="53ee3-143">[Azure IOT kenar][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="53ee3-143">[Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="53ee3-144">Daha fazla IOT hub'ı özelliklerini keşfetmek için bkz:</span><span class="sxs-lookup"><span data-stu-id="53ee3-144">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="53ee3-145">[IOT Hub Geliştirici Kılavuzu][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="53ee3-145">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="53ee3-146">[IOT çözümünüzden zemin oluşturan güvenli][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="53ee3-146">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
