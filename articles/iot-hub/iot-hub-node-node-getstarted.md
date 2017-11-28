---
title: "aaaGet başlatılan Azure IOT Hub (düğüm) | Microsoft Docs"
description: "Nasıl tooAzure IOT Hub'ın IOT SDK'ları için Node.js kullanarak toosend cihaz-bulut iletileri öğrenin. Sanal cihazı ve hizmet uygulamaları tooregister Cihazınızı oluşturmak, iletileri gönderir ve IOT hub'ından iletileri okur."
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
ms.openlocfilehash: d0747895365f2359a9c38ea1e85a5881d6efec0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-node"></a><span data-ttu-id="fc3f1-104">Düğüm kullanarak sanal cihaz tooyour IOT hub'ınıza bağlanın</span><span class="sxs-lookup"><span data-stu-id="fc3f1-104">Connect your simulated device tooyour IoT hub using Node</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="fc3f1-105">Bu öğretici Hello sonunda üç Node.js konsol uygulamaları vardır:</span><span class="sxs-lookup"><span data-stu-id="fc3f1-105">At hello end of this tutorial, you have three Node.js console apps:</span></span>

* <span data-ttu-id="fc3f1-106">**Createdeviceıdentity.js**ilişkili güvenlik anahtarı tooconnect sanal cihaz uygulamanız ve bir cihaz kimliği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-106">**CreateDeviceIdentity.js**, which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="fc3f1-107">**ReadDeviceToCloudMessages.js**, sanal cihaz uygulamanız tarafından gönderilen hello telemetri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-107">**ReadDeviceToCloudMessages.js**, which displays hello telemetry sent by your simulated device app.</span></span>
* <span data-ttu-id="fc3f1-108">**SimulatedDevice.js**, hangi tooyour IOT hub'ı daha önce oluşturduğunuz hello cihaz kimliği bağlanır ve hello MQTT protokolünü kullanarak her saniye bir telemetri iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-108">**SimulatedDevice.js**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="fc3f1-109">Merhaba makale [Azure IOT SDK'ları] [ lnk-hub-sdks] aygıtlar ve çözüm arka ucunuz hem uygulamalar toorun toobuild kullanabileceğiniz hello Azure IOT SDK'ları hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="fc3f1-110">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="fc3f1-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="fc3f1-111">Node.js 0.10.x sürümü veya sonraki bir sürüm.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="fc3f1-112">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-112">An active Azure account.</span></span> <span data-ttu-id="fc3f1-113">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="fc3f1-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="fc3f1-114">IoT Hub’ınızı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-114">You have now created your IoT hub.</span></span> <span data-ttu-id="fc3f1-115">Merhaba IOT Hub ana bilgisayar adı ve hello IOT Hub bağlantı dizesine toocomplete hello Bu öğreticinin geri kalanını ihtiyacınız var.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-115">You have hello IoT Hub host name and hello IoT Hub connection string that you need toocomplete hello rest of this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="fc3f1-116">Cihaz kimliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="fc3f1-116">Create a device identity</span></span>
<span data-ttu-id="fc3f1-117">Bu bölümde, hello kimlik IOT hub'ınızı kayıt defterinde bir cihaz kimliği oluşturan bir Node.js konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-117">In this section, you create a Node.js console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="fc3f1-118">Bir aygıt tooIoT hub hello kimlik kayıt defterinde girişi olmayan yalnızca bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-118">A device can only connect tooIoT hub if it has an entry in hello identity registry.</span></span> <span data-ttu-id="fc3f1-119">Daha fazla bilgi için bkz: Merhaba **kimlik kayıt defteri** hello bölümünü [IOT Hub Geliştirici Kılavuzu][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="fc3f1-119">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="fc3f1-120">Bu konsol uygulamasını çalıştırdığınızda, benzersiz cihaz kimliği oluşturur ve cihaz bulut gönderdiğinde Cihazınızı tooidentify kendisini kullanabileceğiniz anahtar tooIoT Hub iletileri.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-120">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="fc3f1-121">**createdeviceidentity** adlı yeni bir boş klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-121">Create a new empty folder called **createdeviceidentity**.</span></span> <span data-ttu-id="fc3f1-122">Merhaba, **createdeviceidentity** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-122">In hello **createdeviceidentity** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="fc3f1-123">Tüm hello Varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="fc3f1-123">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="fc3f1-124">Merhaba, komut isteminde **createdeviceidentity** klasörüne, komut tooinstall hello aşağıdaki hello **azure-iothub** hizmet SDK paketi:</span><span class="sxs-lookup"><span data-stu-id="fc3f1-124">At your command prompt in hello **createdeviceidentity** folder, run hello following command tooinstall hello **azure-iothub** Service SDK package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="fc3f1-125">Bir metin düzenleyicisi kullanarak oluşturduğunuz bir **Createdeviceıdentity.js** hello dosyasında **createdeviceidentity** klasör.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-125">Using a text editor, create a **CreateDeviceIdentity.js** file in hello **createdeviceidentity** folder.</span></span>
4. <span data-ttu-id="fc3f1-126">Merhaba aşağıdakileri ekleyin `require` hello hello başlangıç deyiminin **Createdeviceıdentity.js** dosyası:</span><span class="sxs-lookup"><span data-stu-id="fc3f1-126">Add hello following `require` statement at hello start of hello **CreateDeviceIdentity.js** file:</span></span>
   
    ```
    'use strict';
   
    var iothub = require('azure-iothub');
    ```
5. <span data-ttu-id="fc3f1-127">Aşağıdaki kodu toohello hello eklemek **Createdeviceıdentity.js** dosya ve hello yer tutucu değerini hello hello önceki bölümde oluşturduğunuz hello hub için IOT Hub bağlantı dizesi ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="fc3f1-127">Add hello following code toohello **CreateDeviceIdentity.js** file and replace hello placeholder value with hello IoT Hub connection string for hello hub you created in hello previous section:</span></span> 
   
    ```
    var connectionString = '{iothub connection string}';
   
    var registry = iothub.Registry.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="fc3f1-128">Aşağıdaki kod toocreate hello kimlik IOT hub'ınızı kayıt defterinde bir cihaz tanımında hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-128">Add hello following code toocreate a device definition in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="fc3f1-129">Merhaba cihaz kimliği hello kimlik kayıt defterinde yoksa, bu kod bir cihaz oluşturur, aksi takdirde hello mevcut aygıt hello anahtarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="fc3f1-129">This code creates a device if hello device ID does not exist in hello identity registry, otherwise it returns hello key of hello existing device:</span></span>
   
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

7. <span data-ttu-id="fc3f1-130">**CreateDeviceIdentity.js** dosyasını kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-130">Save and close **CreateDeviceIdentity.js** file.</span></span>
8. <span data-ttu-id="fc3f1-131">toorun hello **createdeviceidentity** uygulamayı, komut hello hello createdeviceidentity klasöründeki komut isteminde aşağıdaki hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="fc3f1-131">toorun hello **createdeviceidentity** application, execute hello following command at hello command prompt in hello createdeviceidentity folder:</span></span>
   
    ```
    node CreateDeviceIdentity.js 
    ```
9. <span data-ttu-id="fc3f1-132">Merhaba Not **cihaz kimliği** ve **aygıt anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-132">Make a note of hello **Device ID** and **Device key**.</span></span> <span data-ttu-id="fc3f1-133">TooIoT hub'a bir cihaz olarak bağlanan bir uygulama oluşturduğunuzda, bu değerleri daha sonra gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-133">You need these values later when you create an application that connects tooIoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="fc3f1-134">Merhaba IOT Hub kimlik kayıt defteri, yalnızca cihaz kimlikleri tooenable güvenli erişim toohello IOT hub'ı depolar.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-134">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="fc3f1-135">Cihaz kimliklerini ve anahtarlarını toouse güvenlik kimlik bilgileri ve toodisable erişim için tek bir cihaza kullanabilirsiniz bir etkin/devre dışı bayrağını depolar.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-135">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="fc3f1-136">Uygulamanızın cihaza özgü diğer meta verileri toostore gerekiyorsa, bir uygulamaya özgü depo kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-136">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="fc3f1-137">Daha fazla bilgi için bkz: Merhaba [IOT Hub Geliştirici Kılavuzu][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="fc3f1-137">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<a id="D2C_node"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="fc3f1-138">Cihazdan buluta iletileri alma</span><span class="sxs-lookup"><span data-stu-id="fc3f1-138">Receive device-to-cloud messages</span></span>
<span data-ttu-id="fc3f1-139">Bu bölümde, IoT Hub'dan cihazdan buluta iletiler okuyan bir Node.js konsol uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-139">In this section, you create a Node.js console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="fc3f1-140">IOT hub'ı kullanıma sunan bir [Event Hubs][lnk-event-hubs-overview]-uyumlu bir uç noktasını tooenable, tooread cihaz bulut iletilerini.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-140">An IoT hub exposes an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="fc3f1-141">tookeep şeyler basit, Bu öğretici, bir yüksek işleme dağıtımına uygun olmayan temel bir okuyucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-141">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="fc3f1-142">Merhaba [cihaz-bulut iletileri] [ lnk-process-d2c-tutorial] öğretici gösterir, ölçekli olarak nasıl tooprocess cihaz-bulut iletileri.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-142">hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how tooprocess device-to-cloud messages at scale.</span></span> <span data-ttu-id="fc3f1-143">Merhaba [Event Hubs ile çalışmaya başlama] [ lnk-eventhubs-tutorial] Eğitmeni nasıl tooprocess olay hub'larından iletileri ve geçerli toohello IOT Hub ve Event Hub ile uyumlu uç noktalar hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-143">hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how tooprocess messages from Event Hubs and is applicable toohello IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="fc3f1-144">Merhaba cihaz bulut iletilerini her zaman okumak için Event Hub ile uyumlu uç nokta hello AMQP protokolünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-144">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>
> 
> 

1. <span data-ttu-id="fc3f1-145">**readdevicetocloudmessages** adlı boş bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-145">Create an empty folder called **readdevicetocloudmessages**.</span></span> <span data-ttu-id="fc3f1-146">Merhaba, **readdevicetocloudmessages** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-146">In hello **readdevicetocloudmessages** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="fc3f1-147">Tüm hello Varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="fc3f1-147">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="fc3f1-148">Merhaba, komut isteminde **readdevicetocloudmessages** klasörüne, komut tooinstall hello aşağıdaki hello **azure event hubs** paketi:</span><span class="sxs-lookup"><span data-stu-id="fc3f1-148">At your command prompt in hello **readdevicetocloudmessages** folder, run hello following command tooinstall hello **azure-event-hubs** package:</span></span>
   
    ```
    npm install azure-event-hubs --save
    ```
3. <span data-ttu-id="fc3f1-149">Bir metin düzenleyicisi kullanarak oluşturduğunuz bir **ReadDeviceToCloudMessages.js** hello dosyasında **readdevicetocloudmessages** klasör.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-149">Using a text editor, create a **ReadDeviceToCloudMessages.js** file in hello **readdevicetocloudmessages** folder.</span></span>
4. <span data-ttu-id="fc3f1-150">Merhaba aşağıdakileri ekleyin `require` hello deyimlerini başlatmak hello **ReadDeviceToCloudMessages.js** dosyası:</span><span class="sxs-lookup"><span data-stu-id="fc3f1-150">Add hello following `require` statements at hello start of hello **ReadDeviceToCloudMessages.js** file:</span></span>
   
    ```
    'use strict';
   
    var EventHubClient = require('azure-event-hubs').Client;
    ```
5. <span data-ttu-id="fc3f1-151">Değişken bildirimi aşağıdaki hello ekleyin ve hello hub'ınız için IOT Hub bağlantı dizesine sahip hello yer tutucu değerini değiştirin:</span><span class="sxs-lookup"><span data-stu-id="fc3f1-151">Add hello following variable declaration and replace hello placeholder value with hello IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    ```
6. <span data-ttu-id="fc3f1-152">Yazdırma çıktı toohello Konsolu iki işlevleri aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="fc3f1-152">Add hello following two functions that print output toohello console:</span></span>
   
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
7. <span data-ttu-id="fc3f1-153">Aşağıdaki kod toocreate hello hello eklemek **EventHubClient**hello bağlantı tooyour IOT hub'ı açın ve her bölüm için alıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-153">Add hello following code toocreate hello **EventHubClient**, open hello connection tooyour IoT Hub, and create a receiver for each partition.</span></span> <span data-ttu-id="fc3f1-154">Bu uygulama Hello alıcı çalışmaya başladıktan sonra hello alıcı yalnızca gönderilen iletileri tooIoT Hub okur böylece bir alıcı oluştururken bir filtre kullanır.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-154">This application uses a filter when it creates a receiver so that hello receiver only reads messages sent tooIoT Hub after hello receiver starts running.</span></span> <span data-ttu-id="fc3f1-155">Yalnızca hello geçerli iletiler kümesini görmek için bu filtre bir test ortamında kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-155">This filter is useful in a test environment so you see just hello current set of messages.</span></span> <span data-ttu-id="fc3f1-156">Bir üretim ortamında kodunuzun tüm hello iletileri işlediğinden emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-156">In a production environment, your code should make sure that it processes all hello messages.</span></span> <span data-ttu-id="fc3f1-157">Daha fazla bilgi için bkz: Merhaba [nasıl tooprocess IOT Hub cihaz bulut iletilerini] [ lnk-process-d2c-tutorial] Öğreticisi:</span><span class="sxs-lookup"><span data-stu-id="fc3f1-157">For more information, see hello [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial:</span></span>
   
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
8. <span data-ttu-id="fc3f1-158">Kaydet ve Kapat hello **ReadDeviceToCloudMessages.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-158">Save and close hello **ReadDeviceToCloudMessages.js** file.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="fc3f1-159">Sanal cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="fc3f1-159">Create a simulated device app</span></span>
<span data-ttu-id="fc3f1-160">Bu bölümde, tooan IOT hub'ı cihaz-bulut iletileri gönderen bir cihaza benzetim yapan bir Node.js konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-160">In this section, you create a Node.js console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="fc3f1-161">**simulateddevice** adlı boş bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-161">Create an empty folder called **simulateddevice**.</span></span> <span data-ttu-id="fc3f1-162">Merhaba, **simulateddevice** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-162">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="fc3f1-163">Tüm hello Varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="fc3f1-163">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="fc3f1-164">Merhaba, komut isteminde **simulateddevice** klasörüne, komut tooinstall hello aşağıdaki hello **azure IOT cihaz** cihaz SDK'sı paketinin ve **azure-IOT-cihaz-mqtt**paketi:</span><span class="sxs-lookup"><span data-stu-id="fc3f1-164">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="fc3f1-165">Bir metin düzenleyicisi kullanarak oluşturduğunuz bir **SimulatedDevice.js** hello dosyasında **simulateddevice** klasör.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-165">Using a text editor, create a **SimulatedDevice.js** file in hello **simulateddevice** folder.</span></span>
4. <span data-ttu-id="fc3f1-166">Merhaba aşağıdakileri ekleyin `require` hello deyimlerini başlatmak hello **SimulatedDevice.js** dosyası:</span><span class="sxs-lookup"><span data-stu-id="fc3f1-166">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    ```
5. <span data-ttu-id="fc3f1-167">Ekleme bir **connectionString** değişken ve toocreate kullanan bir **istemci** örneği.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-167">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="fc3f1-168">Değiştir **{youriothostname}** hello IOT hub'ı hello adı ile oluşturduğunuz hello *IOT Hub oluşturma* bölümü.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-168">Replace **{youriothostname}** with hello name of hello IoT hub you created hello *Create an IoT Hub* section.</span></span> <span data-ttu-id="fc3f1-169">Değiştir **{yourdevicekey}** hello oluşturulan hello aygıt anahtarı değerine sahip *bir cihaz kimliği oluşturma* bölümü:</span><span class="sxs-lookup"><span data-stu-id="fc3f1-169">Replace **{yourdevicekey}** with hello device key value you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myFirstNodeDevice;SharedAccessKey={yourdevicekey}';
   
    var client = clientFromConnectionString(connectionString);
    ```
6. <span data-ttu-id="fc3f1-170">Merhaba uygulamadan işlevi toodisplay çıktı aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="fc3f1-170">Add hello following function toodisplay output from hello application:</span></span>
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="fc3f1-171">Bir geri çağırma oluşturun ve hello kullan **setInterval** saniyede bir ileti tooyour IOT hub'ı toosend işlev:</span><span class="sxs-lookup"><span data-stu-id="fc3f1-171">Create a callback and use hello **setInterval** function toosend a message tooyour IoT hub every second:</span></span>
   
    ```
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
   
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
8. <span data-ttu-id="fc3f1-172">Merhaba bağlantı tooyour IOT hub'ı açın ve iletileri göndermeye başlayın:</span><span class="sxs-lookup"><span data-stu-id="fc3f1-172">Open hello connection tooyour IoT Hub and start sending messages:</span></span>
   
    ```
    client.open(connectCallback);
    ```
9. <span data-ttu-id="fc3f1-173">Kaydet ve Kapat hello **SimulatedDevice.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-173">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="fc3f1-174">tookeep şeyler basit, Bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-174">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="fc3f1-175">Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="fc3f1-175">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="run-hello-apps"></a><span data-ttu-id="fc3f1-176">Merhaba uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="fc3f1-176">Run hello apps</span></span>
<span data-ttu-id="fc3f1-177">Hazır toorun hello uygulamaları sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-177">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="fc3f1-178">Bir komut isteminde hello **readdevicetocloudmessages** klasörü, IOT hub'ınızı izleme komut toobegin aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fc3f1-178">At a command prompt in hello **readdevicetocloudmessages** folder, run hello following command toobegin monitoring your IoT hub:</span></span>
   
    ```
    node ReadDeviceToCloudMessages.js 
    ```
   
    ![Node.js IOT Hub hizmeti uygulama toomonitor cihaz-bulut iletileri][7]
2. <span data-ttu-id="fc3f1-180">Bir komut isteminde hello **simulateddevice** klasörü, telemetri verileri tooyour IOT hub'ı gönderme komutu toobegin aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fc3f1-180">At a command prompt in hello **simulateddevice** folder, run hello following command toobegin sending telemetry data tooyour IoT hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![Node.js IOT Hub cihaz uygulaması toosend cihaz bulut iletilerini][8]
3. <span data-ttu-id="fc3f1-182">Merhaba **kullanım** döşeme hello [Azure portal] [ lnk-portal] gösterir hello gönderilen iletileri toohello IOT hub'ı sayısı:</span><span class="sxs-lookup"><span data-stu-id="fc3f1-182">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>
   
    ![Azure portalı kullanım kutucuğu sayısını gösteren gönderilen iletileri tooIoT Hub][43]

## <a name="next-steps"></a><span data-ttu-id="fc3f1-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fc3f1-184">Next steps</span></span>
<span data-ttu-id="fc3f1-185">Bu öğreticide hello Azure portalında yeni bir IOT hub yapılandırılmış ve ardından hello IOT hub'ın kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-185">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="fc3f1-186">Bu cihaz kimliğini tooenable benzetimli hello cihaz uygulama toosend cihaz bulut iletilerini toohello IOT hub kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-186">You used this device identity tooenable hello simulated device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="fc3f1-187">Merhaba hello IOT hub tarafından alınan iletileri görüntüleyen bir uygulama da oluşturmuş.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-187">You also created an app that displays hello messages received by hello IoT hub.</span></span> 

<span data-ttu-id="fc3f1-188">Başlarken toocontinue IOT Hub ve tooexplore diğer IOT senaryolarını bakın:</span><span class="sxs-lookup"><span data-stu-id="fc3f1-188">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="fc3f1-189">[Cihazınızı bağlama][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="fc3f1-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="fc3f1-190">[Cihaz yönetimini kullanmaya başlama][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="fc3f1-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="fc3f1-191">[Azure IoT Edge’i kullanmaya başlama][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="fc3f1-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="fc3f1-192">toolearn tooextend, IOT çözümü ve işlem cihaz bulut iletilerini ölçekli olarak nasıl görürüm hello [cihaz-bulut iletileri] [ lnk-process-d2c-tutorial] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="fc3f1-192">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
