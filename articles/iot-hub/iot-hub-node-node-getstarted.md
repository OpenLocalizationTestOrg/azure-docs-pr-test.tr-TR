---
title: "Azure IoT Hub'ı (Node) kullanmaya başlama | Microsoft Docs"
description: "Node.js için IoT SDK’larını kullanarak Azure IoT Hub’a cihazdan buluta ileti göndermeyi öğrenin. IoT hub’a cihazınızı kaydetmek, ileti göndermek ve ileti okumak için sanal cihaz ve hizmet uygulamaları oluşturun."
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 56618522-9a31-42c6-94bf-55e2233b39ac
ms.service: iot-hub
ms.devlang: javascript
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b27a34c0f1f127628912ad68a002e15cc838b4d0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-simulated-device-to-your-iot-hub-using-node"></a><span data-ttu-id="a21f4-104">Node kullanarak sanal cihazınızı IoT hub’ınıza bağlama</span><span class="sxs-lookup"><span data-stu-id="a21f4-104">Connect your simulated device to your IoT hub using Node</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="a21f4-105">Bu öğreticinin sonunda üç Node.js konsol uygulamanız olacak:</span><span class="sxs-lookup"><span data-stu-id="a21f4-105">At the end of this tutorial, you have three Node.js console apps:</span></span>

* <span data-ttu-id="a21f4-106">Bir cihaz kimliği ve sanal cihaz uygulamanızı bağlamak için ilişkili güvenlik anahtarı oluşturan **CreateDeviceIdentity.js**.</span><span class="sxs-lookup"><span data-stu-id="a21f4-106">**CreateDeviceIdentity.js**, which creates a device identity and associated security key to connect your simulated device app.</span></span>
* <span data-ttu-id="a21f4-107">Sanal cihaz uygulamanız tarafından gönderilen telemetriyi gösteren **ReadDeviceToCloudMessages.js**.</span><span class="sxs-lookup"><span data-stu-id="a21f4-107">**ReadDeviceToCloudMessages.js**, which displays the telemetry sent by your simulated device app.</span></span>
* <span data-ttu-id="a21f4-108">Daha önce oluşturulan cihaz kimliğiyle IoT hub'ınıza bağlanan ve MQTT protokolünü kullanarak her saniye bir telemetri iletisi gönderen **SimulatedDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="a21f4-108">**SimulatedDevice.js**, which connects to your IoT hub with the device identity created earlier, and sends a telemetry message every second using the MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="a21f4-109">[IoT Hub SDK'ları][lnk-hub-sdks] makalesi, hem cihazlarınızda hem de çözüm arka ucunuzda çalıştırılacak uygulamalar oluşturmak için kullanabileceğiniz Azure IoT SDK’ları hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="a21f4-109">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="a21f4-110">Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="a21f4-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="a21f4-111">Node.js 0.10.x sürümü veya sonraki bir sürüm.</span><span class="sxs-lookup"><span data-stu-id="a21f4-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="a21f4-112">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="a21f4-112">An active Azure account.</span></span> <span data-ttu-id="a21f4-113">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="a21f4-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="a21f4-114">IoT Hub’ınızı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="a21f4-114">You have now created your IoT hub.</span></span> <span data-ttu-id="a21f4-115">Bu öğreticinin geri kalanını tamamlamak için gereken IoT Hub ana bilgisayar adına ve IoT Hub bağlantı dizesine sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="a21f4-115">You have the IoT Hub host name and the IoT Hub connection string that you need to complete the rest of this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="a21f4-116">Cihaz kimliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="a21f4-116">Create a device identity</span></span>
<span data-ttu-id="a21f4-117">Bu bölümde, IoT hub'ınızdaki kimlik kayıt defterinde bir cihaz kimliği oluşturan bir Node.js konsol uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="a21f4-117">In this section, you create a Node.js console app that creates a device identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="a21f4-118">Yalnızca kimlik kayıt defterinde girişi olan cihazlar IoT hub'ına bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="a21f4-118">A device can only connect to IoT hub if it has an entry in the identity registry.</span></span> <span data-ttu-id="a21f4-119">Daha fazla bilgi için [IoT Hub Geliştirici Kılavuzu][lnk-devguide-identity]'nun **Kimlik Kayıt Defteri** bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="a21f4-119">For more information, see the **Identity Registry** section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="a21f4-120">Bu konsol uygulamasını çalıştırdığınızda, cihazınızın IoT Hub'a cihaz-bulut iletileri gönderdiğinde kendisini tanımlamak için kullanabileceği benzersiz bir cihaz kimliği ve anahtarı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a21f4-120">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span>

1. <span data-ttu-id="a21f4-121">**createdeviceidentity** adlı yeni bir boş klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a21f4-121">Create a new empty folder called **createdeviceidentity**.</span></span> <span data-ttu-id="a21f4-122">Komut isteminizde aşağıdaki komutu kullanarak **createdeviceidentity** klasöründe bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a21f4-122">In the **createdeviceidentity** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="a21f4-123">Tüm varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="a21f4-123">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="a21f4-124">Komut isteminizde **createdeviceidentity** klasöründe **azure-iothub** Hizmet SDK paketini yüklemek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a21f4-124">At your command prompt in the **createdeviceidentity** folder, run the following command to install the **azure-iothub** Service SDK package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="a21f4-125">Bir metin düzenleyicisi kullanarak **createdeviceidentity** klasöründe bir **CreateDeviceIdentity.js** dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a21f4-125">Using a text editor, create a **CreateDeviceIdentity.js** file in the **createdeviceidentity** folder.</span></span>
4. <span data-ttu-id="a21f4-126">Aşağıdaki `require` deyimini **CreateDeviceIdentity.js** dosyasının başlangıcına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a21f4-126">Add the following `require` statement at the start of the **CreateDeviceIdentity.js** file:</span></span>
   
    ```
    'use strict';
   
    var iothub = require('azure-iothub');
    ```
5. <span data-ttu-id="a21f4-127">Aşağıdaki kodu **CreateDeviceIdentity.js** dosyasına ekleyin ve yer tutucu değerini önceki bölümde oluşturduğunuz hub'ın IoT Hub'ı bağlantı dizesiyle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="a21f4-127">Add the following code to the **CreateDeviceIdentity.js** file and replace the placeholder value with the IoT Hub connection string for the hub you created in the previous section:</span></span> 
   
    ```
    var connectionString = '{iothub connection string}';
   
    var registry = iothub.Registry.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="a21f4-128">IoT hub'ınızın kimlik kayıt defterinde bir cihaz tanımı oluşturmak için aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a21f4-128">Add the following code to create a device definition in the identity registry in your IoT hub.</span></span> <span data-ttu-id="a21f4-129">Bu kod, cihaz kimliği kayıt defterinde yoksa bir cihaz oluşturur, aksi halde var olan cihazın anahtarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="a21f4-129">This code creates a device if the device ID does not exist in the identity registry, otherwise it returns the key of the existing device:</span></span>
   
    ```
    var device = {
      deviceId: 'myFirstNodeDevice'
    }
    registry.create(device, function(err, deviceInfo, res) {
      if (err) {
        registry.get(device.deviceId, printDeviceInfo);
      }
      if (deviceInfo) {
        printDeviceInfo(err, deviceInfo, res)
      }
    });
   
    function printDeviceInfo(err, deviceInfo, res) {
      if (deviceInfo) {
        console.log('Device ID: ' + deviceInfo.deviceId);
        console.log('Device key: ' + deviceInfo.authentication.symmetricKey.primaryKey);
      }
    }
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

7. <span data-ttu-id="a21f4-130">**CreateDeviceIdentity.js** dosyasını kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="a21f4-130">Save and close **CreateDeviceIdentity.js** file.</span></span>
8. <span data-ttu-id="a21f4-131">**createdeviceidentity** uygulamasını çalıştırmak için, createdeviceidentity klasöründeki komut isteminde aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="a21f4-131">To run the **createdeviceidentity** application, execute the following command at the command prompt in the createdeviceidentity folder:</span></span>
   
    ```
    node CreateDeviceIdentity.js 
    ```
9. <span data-ttu-id="a21f4-132">**Cihaz kimliği** ve **Cihaz anahtarını** not edin.</span><span class="sxs-lookup"><span data-stu-id="a21f4-132">Make a note of the **Device ID** and **Device key**.</span></span> <span data-ttu-id="a21f4-133">İleride IoT Hub'a bir cihaz olarak bağlanan bir uygulama oluşturduğunuzda bu değerlere ihtiyacınız olur.</span><span class="sxs-lookup"><span data-stu-id="a21f4-133">You need these values later when you create an application that connects to IoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="a21f4-134">IoT Hub kimlik kayıt defteri, yalnızca IoT hub'ına güvenli erişim sağlamak amacıyla cihaz kimliklerini depolar.</span><span class="sxs-lookup"><span data-stu-id="a21f4-134">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="a21f4-135">Güvenlik kimlik bilgileri olarak kullanılmak üzere cihaz kimliklerini ve anahtarlarını ve tek bir cihaza erişimi devre dışı bırakmak için kullanabileceğiniz etkin/devre dışı bayrağını depolar.</span><span class="sxs-lookup"><span data-stu-id="a21f4-135">It stores device IDs and keys to use as security credentials and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="a21f4-136">Uygulamanızın cihaza özgü diğer meta verileri depolaması gerekiyorsa uygulamaya özgü bir depo kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a21f4-136">If your application needs to store other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="a21f4-137">Daha fazla bilgi için bkz. [IoT Hub geliştirici kılavuzu][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="a21f4-137">For more information, see the [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<a id="D2C_node"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="a21f4-138">Cihazdan buluta iletileri alma</span><span class="sxs-lookup"><span data-stu-id="a21f4-138">Receive device-to-cloud messages</span></span>
<span data-ttu-id="a21f4-139">Bu bölümde, IoT Hub'dan cihazdan buluta iletiler okuyan bir Node.js konsol uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="a21f4-139">In this section, you create a Node.js console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="a21f4-140">IoT hub'ı, cihazdan buluta iletilerini okumanızı sağlamak için [Event Hubs][lnk-event-hubs-overview] ile uyumlu bir uç noktasını kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="a21f4-140">An IoT hub exposes an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint to enable you to read device-to-cloud messages.</span></span> <span data-ttu-id="a21f4-141">Sade ve basit bir anlatım gözetildiği için bu öğretici yüksek işleme dağıtımına uygun olmayan temel bir okuyucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a21f4-141">To keep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="a21f4-142">[Cihazdan buluta iletileri işleme][lnk-process-d2c-tutorial] öğreticisi, cihazdan buluta iletilerin ölçekli olarak nasıl işleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="a21f4-142">The [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how to process device-to-cloud messages at scale.</span></span> <span data-ttu-id="a21f4-143">[Event Hubs ile Çalışmaya Başlama][lnk-eventhubs-tutorial] öğreticisi, Event Hubs'dan alınan iletilerin nasıl işleneceği hakkında daha fazla bilgi sağlar; IoT Hub ve Event Hub ile uyumlu uç noktalar için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="a21f4-143">The [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how to process messages from Event Hubs and is applicable to the IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="a21f4-144">Cihazdan buluta iletileri okumak için Event Hub ile uyumlu uç nokta her zaman AMQP protokolünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="a21f4-144">The Event Hub-compatible endpoint for reading device-to-cloud messages always uses the AMQP protocol.</span></span>
> 
> 

1. <span data-ttu-id="a21f4-145">**readdevicetocloudmessages** adlı boş bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a21f4-145">Create an empty folder called **readdevicetocloudmessages**.</span></span> <span data-ttu-id="a21f4-146">Komut isteminizde aşağıdaki komutu kullanarak **readdevicetocloudmessages** klasöründe bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a21f4-146">In the **readdevicetocloudmessages** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="a21f4-147">Tüm varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="a21f4-147">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="a21f4-148">Komut isteminizde **readdevicetocloudmessages** klasöründe **azure-event-hubs** paketini yüklemek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a21f4-148">At your command prompt in the **readdevicetocloudmessages** folder, run the following command to install the **azure-event-hubs** package:</span></span>
   
    ```
    npm install azure-event-hubs --save
    ```
3. <span data-ttu-id="a21f4-149">Bir metin düzenleyicisi kullanarak **readdevicetocloudmessages** klasöründe bir **ReadDeviceToCloudMessages.js** dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a21f4-149">Using a text editor, create a **ReadDeviceToCloudMessages.js** file in the **readdevicetocloudmessages** folder.</span></span>
4. <span data-ttu-id="a21f4-150">Aşağıdaki `require` deyimlerini **ReadDeviceToCloudMessages.js** dosyasının başlangıcına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a21f4-150">Add the following `require` statements at the start of the **ReadDeviceToCloudMessages.js** file:</span></span>
   
    ```
    'use strict';
   
    var EventHubClient = require('azure-event-hubs').Client;
    ```
5. <span data-ttu-id="a21f4-151">Aşağıdaki değişken bildirimini ekleyin ve yer tutucu değerini hub'ınızın IoT Hub'ı bağlantı dizesiyle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="a21f4-151">Add the following variable declaration and replace the placeholder value with the IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    ```
6. <span data-ttu-id="a21f4-152">Konsola çıktı yazdıran aşağıdaki iki işlevi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a21f4-152">Add the following two functions that print output to the console:</span></span>
   
    ```
    var printError = function (err) {
      console.log(err.message);
    };
   
    var printMessage = function (message) {
      console.log('Message received: ');
      console.log(JSON.stringify(message.body));
      console.log('');
    };
    ```
7. <span data-ttu-id="a21f4-153">**EventHubClient** oluşturmak, IoT Hub bağlantısını açmak ve her bölüme yönelik bir alıcı oluşturmak için aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a21f4-153">Add the following code to create the **EventHubClient**, open the connection to your IoT Hub, and create a receiver for each partition.</span></span> <span data-ttu-id="a21f4-154">Bu uygulama alıcı oluştururken bir filtre kullanır, böylece bir alıcı çalışmaya başladıktan sonra IoT Hub'a gönderilen iletileri yalnızca okur.</span><span class="sxs-lookup"><span data-stu-id="a21f4-154">This application uses a filter when it creates a receiver so that the receiver only reads messages sent to IoT Hub after the receiver starts running.</span></span> <span data-ttu-id="a21f4-155">Bu filtre, yalnızca geçerli ileti kümesini görmeniz açısından bir test ortamında kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="a21f4-155">This filter is useful in a test environment so you see just the current set of messages.</span></span> <span data-ttu-id="a21f4-156">Bir üretim ortamında, kodunuzun tüm iletileri işlediğinden emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a21f4-156">In a production environment, your code should make sure that it processes all the messages.</span></span> <span data-ttu-id="a21f4-157">Daha fazla bilgi için [IoT Hub cihazdan buluta iletiler nasıl işlenir?][lnk-process-d2c-tutorial] öğreticisine bakın:</span><span class="sxs-lookup"><span data-stu-id="a21f4-157">For more information, see the [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial:</span></span>
   
    ```
    var client = EventHubClient.fromConnectionString(connectionString);
    client.open()
        .then(client.getPartitionIds.bind(client))
        .then(function (partitionIds) {
            return partitionIds.map(function (partitionId) {
                return client.createReceiver('$Default', partitionId, { 'startAfterTime' : Date.now()}).then(function(receiver) {
                    console.log('Created partition receiver: ' + partitionId)
                    receiver.on('errorReceived', printError);
                    receiver.on('message', printMessage);
                });
            });
        })
        .catch(printError);
    ```
8. <span data-ttu-id="a21f4-158">**ReadDeviceToCloudMessages.js** dosyasını kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="a21f4-158">Save and close the **ReadDeviceToCloudMessages.js** file.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="a21f4-159">Sanal cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="a21f4-159">Create a simulated device app</span></span>
<span data-ttu-id="a21f4-160">Bu bölümde, bir IoT hub'a cihazdan buluta iletiler gönderen bir cihaza benzetim yapan bir Node.js konsol uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="a21f4-160">In this section, you create a Node.js console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span></span>

1. <span data-ttu-id="a21f4-161">**simulateddevice** adlı boş bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a21f4-161">Create an empty folder called **simulateddevice**.</span></span> <span data-ttu-id="a21f4-162">Komut isteminizde aşağıdaki komutu kullanarak **simulateddevice** klasöründe bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a21f4-162">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="a21f4-163">Tüm varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="a21f4-163">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="a21f4-164">Komut isteminizde **simulateddevice** klasöründe **azure-iot-device** Cihaz SDK paketini ve **azure-iot-device-mqtt** paketini yüklemek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a21f4-164">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="a21f4-165">Bir metin düzenleyicisi kullanarak **simulateddevice** klasöründe bir **SimulatedDevice.js** dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a21f4-165">Using a text editor, create a **SimulatedDevice.js** file in the **simulateddevice** folder.</span></span>
4. <span data-ttu-id="a21f4-166">Aşağıdaki `require` deyimlerini **SimulatedDevice.js** dosyasının başlangıcına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a21f4-166">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    ```
5. <span data-ttu-id="a21f4-167">Bir **connectionString** değişkeni ekleyin ve bir **İstemci** örneği oluşturmak için bunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="a21f4-167">Add a **connectionString** variable and use it to create a **Client** instance.</span></span> <span data-ttu-id="a21f4-168">**{youriothostname}** yerine, *IoT Hub oluşturma* bölümünde oluşturduğunuz IoT hub'ın adını girin.</span><span class="sxs-lookup"><span data-stu-id="a21f4-168">Replace **{youriothostname}** with the name of the IoT hub you created the *Create an IoT Hub* section.</span></span> <span data-ttu-id="a21f4-169">**{yourdevicekey}** yerine, *Cihaz kimliği oluşturma* bölümünde oluşturduğunuz cihaz anahtarı değerini girin:</span><span class="sxs-lookup"><span data-stu-id="a21f4-169">Replace **{yourdevicekey}** with the device key value you generated in the *Create a device identity* section:</span></span>
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myFirstNodeDevice;SharedAccessKey={yourdevicekey}';
   
    var client = clientFromConnectionString(connectionString);
    ```
6. <span data-ttu-id="a21f4-170">Uygulamadan çıktı görüntülemek için aşağıdaki işlevi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a21f4-170">Add the following function to display output from the application:</span></span>
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="a21f4-171">Bir geri çağırma oluşturun ve IoT hub'ınıza her saniye bir ileti göndermek için **setInterval** işlevini kullanın:</span><span class="sxs-lookup"><span data-stu-id="a21f4-171">Create a callback and use the **setInterval** function to send a message to your IoT hub every second:</span></span>
   
    ```
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
   
        // Create a message and send it to the IoT Hub every second
        setInterval(function(){
            var temperature = 20 + (Math.random() * 15);
            var humidity = 60 + (Math.random() * 20);            
            var data = JSON.stringify({ deviceId: 'myFirstNodeDevice', temperature: temperature, humidity: humidity });
            var message = new Message(data);
            message.properties.add('temperatureAlert', (temperature > 30) ? 'true' : 'false');
            console.log("Sending message: " + message.getData());
            client.sendEvent(message, printResultFor('send'));
        }, 1000);
      }
    };
    ```
8. <span data-ttu-id="a21f4-172">IoT Hub'ınıza bağlantıyı açın ve iletileri göndermeye başlayın:</span><span class="sxs-lookup"><span data-stu-id="a21f4-172">Open the connection to your IoT Hub and start sending messages:</span></span>
   
    ```
    client.open(connectCallback);
    ```
9. <span data-ttu-id="a21f4-173">**SimulatedDevice.js** dosyasını kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="a21f4-173">Save and close the **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="a21f4-174">Sade ve basit bir anlatım gözetildiği için bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="a21f4-174">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="a21f4-175">[Geçici Hata İşleme][lnk-transient-faults] adlı MSDN makalesinde önerildiği üzere, üretim kodunda yeniden deneme ilkelerini (üstel geri alma gibi) uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a21f4-175">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="run-the-apps"></a><span data-ttu-id="a21f4-176">Uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="a21f4-176">Run the apps</span></span>
<span data-ttu-id="a21f4-177">Şimdi uygulamaları çalıştırmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="a21f4-177">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="a21f4-178">**readdevicetocloudmessages** klasöründeki bir komut isteminde IoT hub'ınızı izlemeye başlamak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a21f4-178">At a command prompt in the **readdevicetocloudmessages** folder, run the following command to begin monitoring your IoT hub:</span></span>
   
    ```
    node ReadDeviceToCloudMessages.js 
    ```
   
    ![Cihazdan buluta iletileri izlemeye yönelik Node.js IoT Hub hizmet uygulaması][7]
2. <span data-ttu-id="a21f4-180">**simulateddevice** klasöründeki bir komut isteminde IoT hub'ınıza telemetri verileri göndermeye başlamak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a21f4-180">At a command prompt in the **simulateddevice** folder, run the following command to begin sending telemetry data to your IoT hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![Cihazdan buluta iletileri göndermeye yönelik Node.js IoT Hub cihaz uygulaması][8]
3. <span data-ttu-id="a21f4-182">[Azure portalındaki][lnk-portal] **Kullanım** kutucuğu, IoT hub'ına gönderilen ileti sayısını gösterir:</span><span class="sxs-lookup"><span data-stu-id="a21f4-182">The **Usage** tile in the [Azure portal][lnk-portal] shows the number of messages sent to the IoT hub:</span></span>
   
    ![IoT Hub’a gönderilen ileti sayısını gösteren Azure portalı Kullanım kutucuğu][43]

## <a name="next-steps"></a><span data-ttu-id="a21f4-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a21f4-184">Next steps</span></span>
<span data-ttu-id="a21f4-185">Bu öğreticide, Azure portalında yeni bir IoT hub'ı yapılandırdınız ve ardından IoT hub'ının kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="a21f4-185">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="a21f4-186">Bu cihaz kimliğini, sanal cihaz uygulamasının, IoT hub'ına cihazdan buluta iletileri göndermesini sağlamak için kullandınız.</span><span class="sxs-lookup"><span data-stu-id="a21f4-186">You used this device identity to enable the simulated device app to send device-to-cloud messages to the IoT hub.</span></span> <span data-ttu-id="a21f4-187">Ayrıca, IoT hub’ı tarafından alınan iletileri görüntüleyen bir uygulama da oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="a21f4-187">You also created an app that displays the messages received by the IoT hub.</span></span> 

<span data-ttu-id="a21f4-188">IoT Hub’ı kullanmaya başlamak ve diğer IoT senaryolarını keşfetmek için bkz:</span><span class="sxs-lookup"><span data-stu-id="a21f4-188">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="a21f4-189">[Cihazınızı bağlama][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="a21f4-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="a21f4-190">[Cihaz yönetimini kullanmaya başlama][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="a21f4-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="a21f4-191">[Azure IoT Edge’i kullanmaya başlama][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="a21f4-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="a21f4-192">IoT çözümünüzün nasıl genişletileceğini ve cihazdan buluta iletilerin doğru ölçekte nasıl işleneceğini öğrenmek için [Cihazdan buluta iletileri işleme][lnk-process-d2c-tutorial] öğreticisine bakın.</span><span class="sxs-lookup"><span data-stu-id="a21f4-192">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]


<!-- Images. -->
[7]: ./media/iot-hub-node-node-getstarted/runapp1.png
[8]: ./media/iot-hub-node-node-getstarted/runapp2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
