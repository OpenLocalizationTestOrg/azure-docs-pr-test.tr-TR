---
title: "aaaAzure IOT hub'ı doğrudan yöntemleri (düğüm) | Microsoft Docs"
description: "Nasıl toouse Azure IOT Hub yöntemleri doğrudan. Doğrudan bir yöntem içeren bir sanal cihaz uygulamasının ve hello doğrudan yöntemini çağıran bir hizmet uygulaması için Node.js tooimplement hello Azure IOT SDK'ları kullanın."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ea9c73ca-7778-4e38-a8f1-0bee9d142f04
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 12300ba451816fec1f80163b633f6b6e411d9e5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a><span data-ttu-id="ca017-104">IOT cihazınızla Node.js doğrudan yöntemleri kullan</span><span class="sxs-lookup"><span data-stu-id="ca017-104">Use direct methods on your IoT device with Node.js</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="ca017-105">Bu öğreticinin Hello sonunda, iki Node.js konsol uygulamaları vardır:</span><span class="sxs-lookup"><span data-stu-id="ca017-105">At hello end of this tutorial, you have two Node.js console apps:</span></span>

* <span data-ttu-id="ca017-106">**CallMethodOnDevice.js**, hello sanal cihaz uygulamasının bir yöntemi çağırır ve hello yanıt görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ca017-106">**CallMethodOnDevice.js**, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="ca017-107">**SimulatedDevice.js**, hangi tooyour IOT hub'ı daha önce oluşturduğunuz hello cihaz kimliği bağlanır ve hello bulut tarafından adlı toohello yöntemi yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="ca017-107">**SimulatedDevice.js**, which connects tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="ca017-108">Merhaba makale [Azure IOT SDK'ları] [ lnk-hub-sdks] aygıtlar ve çözüm arka ucunuz hem uygulamalar toorun toobuild kullanabileceğiniz hello Azure IOT SDK'ları hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca017-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="ca017-109">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="ca017-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="ca017-110">Node.js 0.10.x sürümü veya sonraki bir sürüm.</span><span class="sxs-lookup"><span data-stu-id="ca017-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="ca017-111">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="ca017-111">An active Azure account.</span></span> <span data-ttu-id="ca017-112">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="ca017-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="ca017-113">Sanal cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="ca017-113">Create a simulated device app</span></span>
<span data-ttu-id="ca017-114">Bu bölümde, hello bulut tarafından adlı tooa yöntemi yanıt bir Node.js konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ca017-114">In this section, you create a Node.js console app that responds tooa method called by hello cloud.</span></span>

1. <span data-ttu-id="ca017-115">**simulateddevice** adlı yeni bir boş klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ca017-115">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="ca017-116">Merhaba, **simulateddevice** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ca017-116">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="ca017-117">Tüm hello Varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="ca017-117">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="ca017-118">Merhaba, komut isteminde **simulateddevice** klasörüne, komut tooinstall hello aşağıdaki hello **azure IOT cihaz** cihaz SDK'sı paketinin ve **azure-IOT-cihaz-mqtt**paketi:</span><span class="sxs-lookup"><span data-stu-id="ca017-118">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="ca017-119">Bir metin düzenleyicisi kullanarak yeni bir oluşturma **SimulatedDevice.js** hello dosyasında **simulateddevice** klasör.</span><span class="sxs-lookup"><span data-stu-id="ca017-119">Using a text editor, create a new **SimulatedDevice.js** file in hello **simulateddevice** folder.</span></span>
4. <span data-ttu-id="ca017-120">Merhaba aşağıdakileri ekleyin `require` hello deyimlerini başlatmak hello **SimulatedDevice.js** dosyası:</span><span class="sxs-lookup"><span data-stu-id="ca017-120">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="ca017-121">Ekleme bir **connectionString** değişken ve toocreate kullanan bir **DeviceClient** örneği.</span><span class="sxs-lookup"><span data-stu-id="ca017-121">Add a **connectionString** variable and use it toocreate a **DeviceClient** instance.</span></span> <span data-ttu-id="ca017-122">Değiştir **{cihaz bağlantı dizesi}** hello oluşturulan hello cihaz bağlantı dizesiyle *bir cihaz kimliği oluşturma* bölümü:</span><span class="sxs-lookup"><span data-stu-id="ca017-122">Replace **{device connection string}** with hello device connection string you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="ca017-123">Merhaba aygıtta işlevi tooimplement hello yöntemi aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ca017-123">Add hello following function tooimplement hello method on hello device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="ca017-124">Merhaba bağlantı tooyour IOT hub'ı açın ve başlatma hello yöntemi dinleyicisini başlatmak:</span><span class="sxs-lookup"><span data-stu-id="ca017-124">Open hello connection tooyour IoT hub and start initialize hello method listener:</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. <span data-ttu-id="ca017-125">Kaydet ve Kapat hello **SimulatedDevice.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="ca017-125">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="ca017-126">tookeep şeyler basit, Bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="ca017-126">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="ca017-127">Üretim kodunda yeniden deneme ilkelerini (bağlantı yeniden deneme), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="ca017-127">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-method-on-a-device"></a><span data-ttu-id="ca017-128">Bir cihazda bir yöntemini çağırın</span><span class="sxs-lookup"><span data-stu-id="ca017-128">Call a method on a device</span></span>
<span data-ttu-id="ca017-129">Bu bölümde, hello sanal cihaz uygulamasının bir yöntemi çağırır ve hello yanıt görüntüleyen bir Node.js konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ca017-129">In this section, you create a Node.js console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="ca017-130">Adlı yeni bir boş klasör oluşturun **callmethodondevice**.</span><span class="sxs-lookup"><span data-stu-id="ca017-130">Create a new empty folder called **callmethodondevice**.</span></span> <span data-ttu-id="ca017-131">Merhaba, **callmethodondevice** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ca017-131">In hello **callmethodondevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="ca017-132">Tüm hello Varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="ca017-132">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="ca017-133">Merhaba, komut isteminde **callmethodondevice** klasörüne, komut tooinstall hello aşağıdaki hello **azure-iothub** paketi:</span><span class="sxs-lookup"><span data-stu-id="ca017-133">At your command prompt in hello **callmethodondevice** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="ca017-134">Bir metin düzenleyicisi kullanarak oluşturduğunuz bir **CallMethodOnDevice.js** hello dosyasında **callmethodondevice** klasör.</span><span class="sxs-lookup"><span data-stu-id="ca017-134">Using a text editor, create a **CallMethodOnDevice.js** file in hello **callmethodondevice** folder.</span></span>
4. <span data-ttu-id="ca017-135">Merhaba aşağıdakileri ekleyin `require` hello deyimlerini başlatmak hello **CallMethodOnDevice.js** dosyası:</span><span class="sxs-lookup"><span data-stu-id="ca017-135">Add hello following `require` statements at hello start of hello **CallMethodOnDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="ca017-136">Değişken bildirimi aşağıdaki hello ekleyin ve hello hub'ınız için IOT Hub bağlantı dizesine sahip hello yer tutucu değerini değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ca017-136">Add hello following variable declaration and replace hello placeholder value with hello IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. <span data-ttu-id="ca017-137">Merhaba istemci tooopen hello bağlantı tooyour IOT hub'ı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ca017-137">Create hello client tooopen hello connection tooyour IoT hub.</span></span>
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. <span data-ttu-id="ca017-138">İşlevi tooinvoke hello aygıt yöntemi ve yazdırma hello aygıt yanıt toohello Konsolu aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ca017-138">Add hello following function tooinvoke hello device method and print hello device response toohello console:</span></span>
   
    ```
    var methodParams = {
        methodName: methodName,
        payload: 'hello world',
        timeoutInSeconds: 30
    };
   
    client.invokeDeviceMethod(deviceId, methodParams, function (err, result) {
        if (err) {
            console.error('Failed tooinvoke method \'' + methodName + '\': ' + err.message);
        } else {
            console.log(methodName + ' on ' + deviceId + ':');
            console.log(JSON.stringify(result, null, 2));
        }
    });
    ```
8. <span data-ttu-id="ca017-139">Kaydet ve Kapat hello **CallMethodOnDevice.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="ca017-139">Save and close hello **CallMethodOnDevice.js** file.</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="ca017-140">Merhaba uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="ca017-140">Run hello apps</span></span>
<span data-ttu-id="ca017-141">Hazır toorun hello uygulamaları sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="ca017-141">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="ca017-142">Bir komut isteminde hello **simulateddevice** klasörü, IOT Hub'ınızı gelen yöntem çağrıları için dinleme komutu toostart aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ca017-142">At a command prompt in hello **simulateddevice** folder, run hello following command toostart listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. <span data-ttu-id="ca017-143">Bir komut isteminde hello **callmethodondevice** klasörü, IOT hub'ınızı izleme komut toobegin aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ca017-143">At a command prompt in hello **callmethodondevice** folder, run hello following command toobegin monitoring your IoT hub:</span></span>
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. <span data-ttu-id="ca017-144">Merhaba aygıt selamlama iletisine ve hello aygıttan hello yöntemi görüntü hello yanıt olarak adlandırılan Merhaba uygulaması yazdırma tarafından toohello yöntemi tepki görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="ca017-144">You will see hello device react toohello method by printing out hello message and hello application which called hello method display hello response from hello device:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="ca017-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ca017-145">Next steps</span></span>
<span data-ttu-id="ca017-146">Bu öğreticide hello Azure portalında yeni bir IOT hub yapılandırılmış ve ardından hello IOT hub'ın kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="ca017-146">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="ca017-147">Merhaba bulut tarafından çağrılan bu cihaz kimliğini tooenable benzetimli hello aygıt uygulama tooreact toomethods kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ca017-147">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="ca017-148">Merhaba aygıtta yöntemleri çağırır ve hello yanıt hello aygıttan görüntüleyen bir uygulama da oluşturmuş.</span><span class="sxs-lookup"><span data-stu-id="ca017-148">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="ca017-149">Başlarken toocontinue IOT Hub ve tooexplore diğer IOT senaryolarını bakın:</span><span class="sxs-lookup"><span data-stu-id="ca017-149">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="ca017-150">[IOT Hub ile çalışmaya başlama]</span><span class="sxs-lookup"><span data-stu-id="ca017-150">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="ca017-151">[Birden çok aygıta işleri zamanla][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="ca017-151">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="ca017-152">toolearn tooextend birden fazla cihazda IOT çözümü ve zamanlama yöntemi çağırır nasıl hello bkz [zamanlama ve yayın işleri] [ lnk-tutorial-jobs] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="ca017-152">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-node-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-node-node-direct-methods/run-callmethodondevice.png
[9]: ./media/iot-hub-node-node-direct-methods/methods-output.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[IOT Hub ile çalışmaya başlama]: iot-hub-node-node-getstarted.md
