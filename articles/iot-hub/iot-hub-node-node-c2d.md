---
title: "Azure IOT hub'ı (düğüm) sahip bulut-cihaz iletilerini | Microsoft Docs"
description: "Node.js için Azure IOT SDK'ları kullanarak bir Azure IOT hub'dan bir aygıta bulut-cihaz iletilerini göndermek nasıl. Bulut-cihaz iletilerini ve bulut-cihaz iletilerini göndermek için bir arka uç uygulaması değiştirmek için bir sanal cihaz uygulamasının değiştirin."
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3ca8a78f-ade2-46e8-8a49-d5d599cdf1f1
ms.service: iot-hub
ms.devlang: javascript
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 4580bda5633f84a7c7af0dc85f3cea4951024836
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a><span data-ttu-id="b9d91-104">IOT hub'ı (düğüm) sahip bulut-cihaz iletilerini gönder</span><span class="sxs-lookup"><span data-stu-id="b9d91-104">Send cloud-to-device messages with IoT Hub (Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="b9d91-105">Giriş</span><span class="sxs-lookup"><span data-stu-id="b9d91-105">Introduction</span></span>
<span data-ttu-id="b9d91-106">Azure IOT Hub, milyonlarca cihaza arasında güvenilir ve güvenli çift yönlü iletişimler sağlayan tam olarak yönetilen hizmet etkinleştirin ve bir çözüm arka ucu ' dir.</span><span class="sxs-lookup"><span data-stu-id="b9d91-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="b9d91-107">[IOT Hub ile çalışmaya başlama] öğretici, IOT hub'ı oluşturma, bir cihaz kimliği, sağlama ve cihaz-bulut iletileri gönderen bir sanal cihaz uygulamasının kodu gösterir.</span><span class="sxs-lookup"><span data-stu-id="b9d91-107">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="b9d91-108">Bu öğretici derlemeler [IOT Hub ile çalışmaya başlama].</span><span class="sxs-lookup"><span data-stu-id="b9d91-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="b9d91-109">Size bir nasıl gösterir için:</span><span class="sxs-lookup"><span data-stu-id="b9d91-109">It shows you how to:</span></span>

* <span data-ttu-id="b9d91-110">Çözüm arka ucunuz, tek bir cihaz IOT hub'ı aracılığıyla bulut cihaz ileti gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="b9d91-110">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span></span>
* <span data-ttu-id="b9d91-111">Bir cihazda bulut-cihaz iletilerini alır.</span><span class="sxs-lookup"><span data-stu-id="b9d91-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="b9d91-112">Çözüm arka ucunuz, teslimat alındısı iste (*geri bildirim*) için bir cihaz IOT Hub'ından gönderilen iletiler için.</span><span class="sxs-lookup"><span data-stu-id="b9d91-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span></span>

<span data-ttu-id="b9d91-113">Bulut cihaz iletileri hakkında daha fazla bilgi bulabilirsiniz [IOT Hub Geliştirici Kılavuzu][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="b9d91-113">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="b9d91-114">Bu öğreticinin sonunda iki Node.js konsol uygulamaları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b9d91-114">At the end of this tutorial, you run two Node.js console apps:</span></span>

* <span data-ttu-id="b9d91-115">**SimulatedDevice**, oluşturduğunuz uygulama değiştirilmiş bir sürümünü [IOT Hub ile çalışmaya başlama], IOT hub'ınıza bağlanır ve bulut-cihaz iletilerini alır.</span><span class="sxs-lookup"><span data-stu-id="b9d91-115">**SimulatedDevice**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="b9d91-116">**SendCloudToDeviceMessage**, IOT hub'ı aracılığıyla sanal cihaz uygulamasının bir bulut cihaz ileti gönderir ve teslimat alındısı alır.</span><span class="sxs-lookup"><span data-stu-id="b9d91-116">**SendCloudToDeviceMessage**, which sends a cloud-to-device message to the simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="b9d91-117">IOT Hub SDK desteği birçok cihaz platformları ve Azure IOT cihaz SDK'ları aracılığıyla dilleri (C, Java ve Javascript dahil) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="b9d91-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="b9d91-118">Bu öğreticinin kod ve genellikle Azure IOT Hub Cihazınızı bağlamak hakkında adım adım yönergeler için bkz: [Azure IOT Geliştirme Merkezi].</span><span class="sxs-lookup"><span data-stu-id="b9d91-118">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [Azure IoT Developer Center].</span></span>
> 
> 

<span data-ttu-id="b9d91-119">Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="b9d91-119">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="b9d91-120">Node.js 0.10.x sürümü veya sonraki bir sürüm.</span><span class="sxs-lookup"><span data-stu-id="b9d91-120">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="b9d91-121">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="b9d91-121">An active Azure account.</span></span> <span data-ttu-id="b9d91-122">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="b9d91-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-the-simulated-device-app"></a><span data-ttu-id="b9d91-123">Sanal cihaz uygulamasının ileti alma</span><span class="sxs-lookup"><span data-stu-id="b9d91-123">Receive messages in the simulated device app</span></span>
<span data-ttu-id="b9d91-124">Bu bölümde, oluşturduğunuz sanal cihaz uygulamasının değiştirme [IOT Hub ile çalışmaya başlama] IOT hub'ından bulut cihaz iletileri almak için.</span><span class="sxs-lookup"><span data-stu-id="b9d91-124">In this section, you modify the simulated device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="b9d91-125">Bir metin düzenleyicisi kullanarak SimulatedDevice.js dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="b9d91-125">Using a text editor, open the SimulatedDevice.js file.</span></span>
2. <span data-ttu-id="b9d91-126">Değiştirme **connectCallback** IOT hub'dan gönderilen iletileri işlemek için işlev.</span><span class="sxs-lookup"><span data-stu-id="b9d91-126">Modify the **connectCallback** function to handle messages sent from IoT Hub.</span></span> <span data-ttu-id="b9d91-127">Bu örnekte, cihazın her zaman çağırır **tam** iletiyi işledi IOT hub'ı bildirmek için işlevi.</span><span class="sxs-lookup"><span data-stu-id="b9d91-127">In this example, the device always invokes the **complete** function to notify IoT Hub that it has processed the message.</span></span> <span data-ttu-id="b9d91-128">Yeni sürümünüz **connectCallback** işlevi aşağıdaki kod parçacığını gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="b9d91-128">Your new version of the **connectCallback** function looks like the following snippet:</span></span>
   
    ```javascript
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
        client.on('message', function (msg) {
          console.log('Id: ' + msg.messageId + ' Body: ' + msg.data);
          client.complete(msg, printResultFor('completed'));
        });
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
   
   > [!NOTE]
   > <span data-ttu-id="b9d91-129">HTTP MQTT veya AMQP yerine taşıma olarak kullanırsanız **DeviceClient** seyrek IOT Hub (değerinden 25 dakikada bir) gelen iletileri örneği denetler.</span><span class="sxs-lookup"><span data-stu-id="b9d91-129">If you use HTTP instead of MQTT or AMQP as the transport, the **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="b9d91-130">MQTT, AMQP ve HTTP desteği ve IOT hub'ı azaltma arasındaki farklar hakkında daha fazla bilgi için bkz: [IOT Hub Geliştirici Kılavuzu][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="b9d91-130">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="b9d91-131">Bulut cihaza ileti gönderme</span><span class="sxs-lookup"><span data-stu-id="b9d91-131">Send a cloud-to-device message</span></span>
<span data-ttu-id="b9d91-132">Bu bölümde, sanal cihaz uygulamasının bulut cihaz iletileri gönderen bir Node.js konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b9d91-132">In this section, you create a Node.js console app that sends cloud-to-device messages to the simulated device app.</span></span> <span data-ttu-id="b9d91-133">Eklediğiniz aygıt cihaz Kimliğini gereksinim [IOT Hub ile çalışmaya başlama] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="b9d91-133">You need the device ID of the device you added in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="b9d91-134">Ayrıca bulabilirsiniz, hub'ın IOT Hub bağlantı dizesine gerekir [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="b9d91-134">You also need the IoT Hub connection string for your hub that you can find in the [Azure portal].</span></span>

1. <span data-ttu-id="b9d91-135">Adlı bir boş klasör oluşturun **sendcloudtodevicemessage**.</span><span class="sxs-lookup"><span data-stu-id="b9d91-135">Create an empty folder called **sendcloudtodevicemessage**.</span></span> <span data-ttu-id="b9d91-136">İçinde **sendcloudtodevicemessage** klasörü, komut isteminde aşağıdaki komutu kullanarak bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b9d91-136">In the **sendcloudtodevicemessage** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="b9d91-137">Tüm varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="b9d91-137">Accept all the defaults:</span></span>
   
    ```shell
    npm init
    ```
2. <span data-ttu-id="b9d91-138">Komut isteminizde **sendcloudtodevicemessage** klasörü yüklemek için aşağıdaki komutu çalıştırın, **azure-iothub** paketi:</span><span class="sxs-lookup"><span data-stu-id="b9d91-138">At your command prompt in the **sendcloudtodevicemessage** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```shell
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="b9d91-139">Bir metin düzenleyicisi kullanarak oluşturduğunuz bir **SendCloudToDeviceMessage.js** dosyasını **sendcloudtodevicemessage** klasör.</span><span class="sxs-lookup"><span data-stu-id="b9d91-139">Using a text editor, create a **SendCloudToDeviceMessage.js** file in the **sendcloudtodevicemessage** folder.</span></span>
4. <span data-ttu-id="b9d91-140">Aşağıdakileri ekleyin `require` deyimleri başlangıcında **SendCloudToDeviceMessage.js** dosyası:</span><span class="sxs-lookup"><span data-stu-id="b9d91-140">Add the following `require` statements at the start of the **SendCloudToDeviceMessage.js** file:</span></span>
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. <span data-ttu-id="b9d91-141">Aşağıdaki kodu ekleyin **SendCloudToDeviceMessage.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="b9d91-141">Add the following code to **SendCloudToDeviceMessage.js** file.</span></span> <span data-ttu-id="b9d91-142">"{IOT hub bağlantı dizesine}" yer tutucu değerini, oluşturduğunuz hub'ın IOT Hub bağlantı dizesiyle değiştirin [IOT Hub ile çalışmaya başlama] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="b9d91-142">Replace the "{iot hub connection string}" placeholder value with the IoT Hub connection string for the hub you created in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="b9d91-143">"{Aygıt id}" yer tutucusunu, eklediğiniz aygıt cihaz Kimliğini değiştirin [IOT Hub ile çalışmaya başlama] Öğreticisi:</span><span class="sxs-lookup"><span data-stu-id="b9d91-143">Replace the "{device id}" placeholder with the device ID of the device you added in the [Get started with IoT Hub] tutorial:</span></span>
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="b9d91-144">İşlem sonuçları konsoluna yazdırmak için aşağıdaki işlevi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b9d91-144">Add the following function to print operation results to the console:</span></span>
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="b9d91-145">Teslim geri bildirim iletilerini konsola yazdırmak için aşağıdaki işlevi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b9d91-145">Add the following function to print delivery feedback messages to the console:</span></span>
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. <span data-ttu-id="b9d91-146">Aygıtınıza ileti gönderme ve cihaz bulut cihaz iletiyi onayladıktan zaman geri bildirim iletisi işlemek için aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b9d91-146">Add the following code to send a message to your device and handle the feedback message when the device acknowledges the cloud-to-device message:</span></span>
   
    ```javascript
    serviceClient.open(function (err) {
      if (err) {
        console.error('Could not connect: ' + err.message);
      } else {
        console.log('Service client connected');
        serviceClient.getFeedbackReceiver(receiveFeedback);
        var message = new Message('Cloud to device message.');
        message.ack = 'full';
        message.messageId = "My Message ID";
        console.log('Sending message: ' + message.getData());
        serviceClient.send(targetDevice, message, printResultFor('send'));
      }
    });
    ```
9. <span data-ttu-id="b9d91-147">Kaydet ve Kapat **SendCloudToDeviceMessage.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="b9d91-147">Save and close **SendCloudToDeviceMessage.js** file.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="b9d91-148">Uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b9d91-148">Run the applications</span></span>
<span data-ttu-id="b9d91-149">Şimdi uygulamaları çalıştırmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="b9d91-149">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="b9d91-150">Komut isteminde **simulateddevice** klasörü, IOT Hub'ına telemetri göndermeyi ve bulut-cihaz iletilerini dinlemek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b9d91-150">At the command prompt in the **simulateddevice** folder, run the following command to send telemetry to IoT Hub and to listen for cloud-to-device messages:</span></span>
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![Sanal cihaz uygulamasının çalıştırın][img-simulated-device]
2. <span data-ttu-id="b9d91-152">Bir komut isteminde **sendcloudtodevicemessage** klasörü, bulut cihaza ileti gönderme ve onayı geri bildirim için beklemek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b9d91-152">At a command prompt in the **sendcloudtodevicemessage** folder, run the following command to send a cloud-to-device message and wait for the acknowledgment feedback:</span></span>
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![Bulut cihaz komut göndermek için uygulamayı çalıştırın][img-send-command]
   
   > [!NOTE]
   > <span data-ttu-id="b9d91-154">Basitlik'ın artırmak amacıyla için bu öğreticiyi herhangi bir yeniden deneme ilkesi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="b9d91-154">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="b9d91-155">Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen MSDN makalesinde uygulamalıdır [geçici hata işleme].</span><span class="sxs-lookup"><span data-stu-id="b9d91-155">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="b9d91-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b9d91-156">Next steps</span></span>
<span data-ttu-id="b9d91-157">Bu öğretici kapsamında, bulut cihaza ileti gönderme ve alma öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="b9d91-157">In this tutorial, you learned how to send and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="b9d91-158">IOT hub'ı kullanan tam uçtan uca çözümler örnekleri görmek için bkz: [Azure IOT paketi].</span><span class="sxs-lookup"><span data-stu-id="b9d91-158">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="b9d91-159">IOT Hub ile çözümleri geliştirme hakkında daha fazla bilgi için bkz: [IOT Hub Geliştirici Kılavuzu].</span><span class="sxs-lookup"><span data-stu-id="b9d91-159">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-node-node-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-node-node-c2d/sendc2d.png

<!-- Links -->

<span data-ttu-id="b9d91-160">[IOT Hub ile çalışmaya başlama]: iot-hub-node-node-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="b9d91-160">[Get started with IoT Hub]: iot-hub-node-node-getstarted.md</span></span>
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
<span data-ttu-id="b9d91-161">[IOT Hub Geliştirici Kılavuzu]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="b9d91-161">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
<span data-ttu-id="b9d91-162">[Azure IOT Geliştirme Merkezi]: http://www.azure.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="b9d91-162">[Azure IoT Developer Center]: http://www.azure.com/develop/iot</span></span>
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
<span data-ttu-id="b9d91-163">[geçici hata işleme]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="b9d91-163">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
<span data-ttu-id="b9d91-164">[Azure portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="b9d91-164">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="b9d91-165">[Azure IOT paketi]: https://azure.microsoft.com/documentation/suites/iot-suite/</span><span class="sxs-lookup"><span data-stu-id="b9d91-165">[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/</span></span>
