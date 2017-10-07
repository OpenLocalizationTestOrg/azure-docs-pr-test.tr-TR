---
title: "Azure IOT hub'ı (düğüm) aaaCloud cihaza iletileriyle | Microsoft Docs"
description: "Nasıl toosend bulut-cihaz hello Azure IOT SDK'ları için Node.js kullanarak Azure IOT hub'ı tooa aygıttan iletileri. Bir sanal cihaz uygulaması tooreceive bulut-cihaz iletilerini değiştirmek ve arka uç uygulaması toosend hello bulut-cihaz iletilerini değiştirin."
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
ms.openlocfilehash: 1ccae0cada52193c2abb91504c086cac226e93da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a><span data-ttu-id="d229d-104">IOT hub'ı (düğüm) sahip bulut-cihaz iletilerini gönder</span><span class="sxs-lookup"><span data-stu-id="d229d-104">Send cloud-to-device messages with IoT Hub (Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="d229d-105">Giriş</span><span class="sxs-lookup"><span data-stu-id="d229d-105">Introduction</span></span>
<span data-ttu-id="d229d-106">Azure IOT Hub, milyonlarca cihaza arasında güvenilir ve güvenli çift yönlü iletişimler sağlayan tam olarak yönetilen hizmet etkinleştirin ve bir çözüm arka ucu ' dir.</span><span class="sxs-lookup"><span data-stu-id="d229d-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="d229d-107">Merhaba [IOT Hub ile çalışmaya başlama] öğretici nasıl toocreate IOT hub'ı, bir cihaz kimliği, sağlamak ve cihaz-bulut iletileri gönderen bir sanal cihaz uygulamasının kodu gösterir.</span><span class="sxs-lookup"><span data-stu-id="d229d-107">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="d229d-108">Bu öğretici derlemeler [IOT Hub ile çalışmaya başlama].</span><span class="sxs-lookup"><span data-stu-id="d229d-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="d229d-109">Size bir nasıl gösterir için:</span><span class="sxs-lookup"><span data-stu-id="d229d-109">It shows you how to:</span></span>

* <span data-ttu-id="d229d-110">Çözüm arka ucunuz, bulut-cihaz iletilerini tooa tek cihaz IOT hub'ı aracılığıyla gönderin.</span><span class="sxs-lookup"><span data-stu-id="d229d-110">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="d229d-111">Bir cihazda bulut-cihaz iletilerini alır.</span><span class="sxs-lookup"><span data-stu-id="d229d-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="d229d-112">Çözüm arka ucunuz, teslimat alındısı iste (*geri bildirim*) tooa cihaz IOT Hub'ından gönderilen iletileri için.</span><span class="sxs-lookup"><span data-stu-id="d229d-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="d229d-113">Hello bulut-cihaz iletilerini hakkında daha fazla bilgi bulabilirsiniz [IOT Hub Geliştirici Kılavuzu][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="d229d-113">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="d229d-114">Bu öğreticinin Hello sonunda, iki Node.js konsol uygulamaları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d229d-114">At hello end of this tutorial, you run two Node.js console apps:</span></span>

* <span data-ttu-id="d229d-115">**SimulatedDevice**, oluşturulan hello uygulama değiştirilmiş bir sürümünü [IOT Hub ile çalışmaya başlama], hangi tooyour IOT hub'ı bağlar ve bulut-cihaz iletilerini alır.</span><span class="sxs-lookup"><span data-stu-id="d229d-115">**SimulatedDevice**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="d229d-116">**SendCloudToDeviceMessage**, hangi bulut aygıt iletisi toohello sanal cihaz uygulaması IOT hub'ı üzerinden gönderir ve teslimat alındısı alır.</span><span class="sxs-lookup"><span data-stu-id="d229d-116">**SendCloudToDeviceMessage**, which sends a cloud-to-device message toohello simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="d229d-117">IOT Hub SDK desteği birçok cihaz platformları ve Azure IOT cihaz SDK'ları aracılığıyla dilleri (C, Java ve Javascript dahil) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d229d-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="d229d-118">Adım adım yönergeler nasıl tooconnect aygıt toothis öğreticinin kod ve genellikle tooAzure IOT hub'ı görmek için hello [Azure IOT Geliştirme Merkezi].</span><span class="sxs-lookup"><span data-stu-id="d229d-118">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [Azure IoT Developer Center].</span></span>
> 
> 

<span data-ttu-id="d229d-119">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="d229d-119">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="d229d-120">Node.js 0.10.x sürümü veya sonraki bir sürüm.</span><span class="sxs-lookup"><span data-stu-id="d229d-120">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="d229d-121">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="d229d-121">An active Azure account.</span></span> <span data-ttu-id="d229d-122">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="d229d-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-simulated-device-app"></a><span data-ttu-id="d229d-123">Merhaba sanal cihaz uygulamasının ileti alma</span><span class="sxs-lookup"><span data-stu-id="d229d-123">Receive messages in hello simulated device app</span></span>
<span data-ttu-id="d229d-124">Bu bölümde, oluşturduğunuz hello sanal cihaz uygulamasının değiştirme [IOT Hub ile çalışmaya başlama] tooreceive bulut cihaza iletilerden hello IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="d229d-124">In this section, you modify hello simulated device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="d229d-125">Bir metin düzenleyicisi kullanarak hello SimulatedDevice.js dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="d229d-125">Using a text editor, open hello SimulatedDevice.js file.</span></span>
2. <span data-ttu-id="d229d-126">Merhaba değiştirme **connectCallback** IOT Hub'ından gönderilen toohandle iletileri işlev.</span><span class="sxs-lookup"><span data-stu-id="d229d-126">Modify hello **connectCallback** function toohandle messages sent from IoT Hub.</span></span> <span data-ttu-id="d229d-127">Bu örnekte, hello cihaz her zaman hello çağırır **tam** toonotify IOT Hub'ın selamlama iletisine işlediğinden işlev.</span><span class="sxs-lookup"><span data-stu-id="d229d-127">In this example, hello device always invokes hello **complete** function toonotify IoT Hub that it has processed hello message.</span></span> <span data-ttu-id="d229d-128">Yeni hello sürümünüz **connectCallback** işlevi hello parçacığını aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="d229d-128">Your new version of hello **connectCallback** function looks like hello following snippet:</span></span>
   
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
        // Create a message and send it toohello IoT Hub every second
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
   > <span data-ttu-id="d229d-129">HTTP MQTT veya AMQP yerine hello taşıma olarak kullanırsanız, hello **DeviceClient** seyrek IOT Hub (değerinden 25 dakikada bir) gelen iletileri örneği denetler.</span><span class="sxs-lookup"><span data-stu-id="d229d-129">If you use HTTP instead of MQTT or AMQP as hello transport, hello **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="d229d-130">Merhaba hello farklarını MQTT, AMQP ve HTTP desteği ve IOT hub'ı azaltma hakkında daha fazla bilgi için bkz: [IOT Hub Geliştirici Kılavuzu][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="d229d-130">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="d229d-131">Bulut cihaza ileti gönderme</span><span class="sxs-lookup"><span data-stu-id="d229d-131">Send a cloud-to-device message</span></span>
<span data-ttu-id="d229d-132">Bu bölümde, bulut-cihaz iletilerini toohello sanal cihaz uygulamasının gönderen bir Node.js konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d229d-132">In this section, you create a Node.js console app that sends cloud-to-device messages toohello simulated device app.</span></span> <span data-ttu-id="d229d-133">Hello eklediğiniz hello aygıtın aygıt kimliği hello [IOT Hub ile çalışmaya başlama] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="d229d-133">You need hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="d229d-134">Hello bulabileceğiniz hub'ınız için IOT Hub bağlantı dizesine hello de [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="d229d-134">You also need hello IoT Hub connection string for your hub that you can find in hello [Azure portal].</span></span>

1. <span data-ttu-id="d229d-135">Adlı bir boş klasör oluşturun **sendcloudtodevicemessage**.</span><span class="sxs-lookup"><span data-stu-id="d229d-135">Create an empty folder called **sendcloudtodevicemessage**.</span></span> <span data-ttu-id="d229d-136">Merhaba, **sendcloudtodevicemessage** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d229d-136">In hello **sendcloudtodevicemessage** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="d229d-137">Tüm hello Varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="d229d-137">Accept all hello defaults:</span></span>
   
    ```shell
    npm init
    ```
2. <span data-ttu-id="d229d-138">Merhaba, komut isteminde **sendcloudtodevicemessage** klasörüne, komut tooinstall hello aşağıdaki hello **azure-iothub** paketi:</span><span class="sxs-lookup"><span data-stu-id="d229d-138">At your command prompt in hello **sendcloudtodevicemessage** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```shell
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="d229d-139">Bir metin düzenleyicisi kullanarak oluşturduğunuz bir **SendCloudToDeviceMessage.js** hello dosyasında **sendcloudtodevicemessage** klasör.</span><span class="sxs-lookup"><span data-stu-id="d229d-139">Using a text editor, create a **SendCloudToDeviceMessage.js** file in hello **sendcloudtodevicemessage** folder.</span></span>
4. <span data-ttu-id="d229d-140">Merhaba aşağıdakileri ekleyin `require` hello deyimlerini başlatmak hello **SendCloudToDeviceMessage.js** dosyası:</span><span class="sxs-lookup"><span data-stu-id="d229d-140">Add hello following `require` statements at hello start of hello **SendCloudToDeviceMessage.js** file:</span></span>
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. <span data-ttu-id="d229d-141">Kod çok aşağıdaki hello eklemek**SendCloudToDeviceMessage.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="d229d-141">Add hello following code too**SendCloudToDeviceMessage.js** file.</span></span> <span data-ttu-id="d229d-142">"{IOT hub bağlantı dizesine}" Merhaba yer tutucu değerini hello hello oluşturduğunuz hello hub için IOT Hub bağlantı dizesi ile değiştirin [IOT Hub ile çalışmaya başlama] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="d229d-142">Replace hello "{iot hub connection string}" placeholder value with hello IoT Hub connection string for hello hub you created in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="d229d-143">"{Aygıt id}" Merhaba yer tutucu hello aygıt hello eklediğiniz hello aygıtın Kimliğini değiştirin [IOT Hub ile çalışmaya başlama] Öğreticisi:</span><span class="sxs-lookup"><span data-stu-id="d229d-143">Replace hello "{device id}" placeholder with hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial:</span></span>
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="d229d-144">İşlev tooprint işlemi sonuçları toohello Konsolu aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d229d-144">Add hello following function tooprint operation results toohello console:</span></span>
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="d229d-145">İşlev tooprint teslim geri bildirim iletileri toohello Konsolu aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d229d-145">Add hello following function tooprint delivery feedback messages toohello console:</span></span>
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. <span data-ttu-id="d229d-146">Merhaba aşağıdaki toosend bir ileti tooyour aygıt kod ve hello aygıt hello bulut cihaz iletiyi onayladıktan zaman hello geri bildirim iletisi işlemek ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d229d-146">Add hello following code toosend a message tooyour device and handle hello feedback message when hello device acknowledges hello cloud-to-device message:</span></span>
   
    ```javascript
    serviceClient.open(function (err) {
      if (err) {
        console.error('Could not connect: ' + err.message);
      } else {
        console.log('Service client connected');
        serviceClient.getFeedbackReceiver(receiveFeedback);
        var message = new Message('Cloud toodevice message.');
        message.ack = 'full';
        message.messageId = "My Message ID";
        console.log('Sending message: ' + message.getData());
        serviceClient.send(targetDevice, message, printResultFor('send'));
      }
    });
    ```
9. <span data-ttu-id="d229d-147">Kaydet ve Kapat **SendCloudToDeviceMessage.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="d229d-147">Save and close **SendCloudToDeviceMessage.js** file.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="d229d-148">Merhaba uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="d229d-148">Run hello applications</span></span>
<span data-ttu-id="d229d-149">Hazır toorun hello uygulamaları sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="d229d-149">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="d229d-150">Merhaba hello komut isteminde **simulateddevice** klasörü hello aşağıdaki komutu çalıştırın, komut toosend telemetri tooIoT Hub ve bulut-cihaz iletilerini toolisten:</span><span class="sxs-lookup"><span data-stu-id="d229d-150">At hello command prompt in hello **simulateddevice** folder, run hello following command toosend telemetry tooIoT Hub and toolisten for cloud-to-device messages:</span></span>
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![Merhaba sanal cihaz uygulamasının çalıştırın][img-simulated-device]
2. <span data-ttu-id="d229d-152">Bir komut isteminde hello **sendcloudtodevicemessage** klasörü, bir bulut cihaz ileti komutu toosend aşağıdaki hello çalıştırın ve hello bildirim geri bildirim için bekleyin:</span><span class="sxs-lookup"><span data-stu-id="d229d-152">At a command prompt in hello **sendcloudtodevicemessage** folder, run hello following command toosend a cloud-to-device message and wait for hello acknowledgment feedback:</span></span>
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![Merhaba uygulama toosend hello bulut cihaz komutunu çalıştırın][img-send-command]
   
   > [!NOTE]
   > <span data-ttu-id="d229d-154">Basitlik'ın artırmak amacıyla için bu öğreticiyi herhangi bir yeniden deneme ilkesi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="d229d-154">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="d229d-155">Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme].</span><span class="sxs-lookup"><span data-stu-id="d229d-155">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="d229d-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d229d-156">Next steps</span></span>
<span data-ttu-id="d229d-157">Bu öğreticide, nasıl öğrenilen toosend ve bulut-cihaz iletilerini.</span><span class="sxs-lookup"><span data-stu-id="d229d-157">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="d229d-158">IOT hub'ı kullanan tam uçtan uca çözümler toosee örnekleri bkz [Azure IOT paketi].</span><span class="sxs-lookup"><span data-stu-id="d229d-158">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="d229d-159">IOT Hub ile çözümleri geliştirme hakkında daha fazla toolearn bkz hello [IOT Hub Geliştirici Kılavuzu].</span><span class="sxs-lookup"><span data-stu-id="d229d-159">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-node-node-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-node-node-c2d/sendc2d.png

<!-- Links -->

[IOT Hub ile çalışmaya başlama]: iot-hub-node-node-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[IOT Hub Geliştirici Kılavuzu]: iot-hub-devguide.md
[Azure IoT Geliştirici Merkezi]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[Geçici hata işleme]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure portal]: https://portal.azure.com
[Azure IoT Paketi]: https://azure.microsoft.com/documentation/suites/iot-suite/
