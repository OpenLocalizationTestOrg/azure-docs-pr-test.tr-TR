---
title: aaaProcess Azure IOT Hub cihaz bulut iletilerini (Java) | Microsoft Docs
description: "Nasıl tooprocess yönlendirme kuralları ve özel uç noktaları toodispatch kullanarak IOT Hub cihaz bulut iletilerini tooother arka uç hizmetlerini iletileri."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: bd9af5f9-a740-4780-a2a6-8c0e2752cf48
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.openlocfilehash: 084e84e721ca4297c4d7d6cb06a43b0bed9bce85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-java"></a><span data-ttu-id="b14a7-103">İşlem IOT hub'a cihaz-bulut iletileri (Java)</span><span class="sxs-lookup"><span data-stu-id="b14a7-103">Process IoT Hub device-to-cloud messages (Java)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="b14a7-104">Azure IOT Hub güvenilir sağlayan tam olarak yönetilen bir hizmettir ve arka uç milyonlarca cihaza ve çözüm arasında güvenli çift yönlü iletişim.</span><span class="sxs-lookup"><span data-stu-id="b14a7-104">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="b14a7-105">Diğer öğreticiler ([IOT Hub ile çalışmaya başlama] ve [IOT Hub ile bulut cihaza ileti gönderme][lnk-c2d]) toouse nasıl hello temel cihaz Bulut ve bulut-cihaz Göster IOT hub'ı işlevselliğini Mesajlaşma.</span><span class="sxs-lookup"><span data-stu-id="b14a7-105">Other tutorials ([Get started with IoT Hub] and [Send cloud-to-device messages with IoT Hub][lnk-c2d]) show you how toouse hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span>

<span data-ttu-id="b14a7-106">Bu öğretici hello gösterilen hello kod inşa edilmiştir [IOT Hub ile çalışmaya başlama] öğretici ve nasıl toouse ileti yönlendirme tooprocess cihaz bulut ölçeklenebilir bir şekilde gösterir.</span><span class="sxs-lookup"><span data-stu-id="b14a7-106">This tutorial builds on hello code shown in hello [Get started with IoT Hub] tutorial, and shows you how toouse message routing tooprocess device-to-cloud messages in a scalable way.</span></span> <span data-ttu-id="b14a7-107">Başlangıç Öğreticisi nasıl hello çözümden Acil eylem gerekli tooprocess iletileri arka uç gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b14a7-107">hello tutorial illustrates how tooprocess messages that require immediate action from hello solution back end.</span></span> <span data-ttu-id="b14a7-108">Örneğin, bir aygıt bir bilet bir CRM sistemine ekleme tetikleyen bir uyarı iletisi gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="b14a7-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="b14a7-109">Bunun aksine, veri noktası iletileri yalnızca bir analytics motoruna akış.</span><span class="sxs-lookup"><span data-stu-id="b14a7-109">By contrast, data-point messages simply feed into an analytics engine.</span></span> <span data-ttu-id="b14a7-110">Örneğin, sıcaklık telemetri toobe sonra analiz etmek için depolanmış olan bir CİHAZDAN bir veri noktası iletisidir.</span><span class="sxs-lookup"><span data-stu-id="b14a7-110">For example, temperature telemetry from a device that is toobe stored for later analysis is a data-point message.</span></span>

<span data-ttu-id="b14a7-111">Bu öğretici Hello sonunda üç Java konsol uygulamaları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b14a7-111">At hello end of this tutorial, you run three Java console apps:</span></span>

* <span data-ttu-id="b14a7-112">**simulated-device**, hello oluşturulan hello uygulaması değiştirilmiş bir sürümünü [IOT Hub ile çalışmaya başlama] öğretici, saniyede veri noktası cihaz bulut iletilerini gönderir ve etkileşimli cihaz bulut iletilerini her 10 saniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="b14a7-112">**simulated-device**, a modified version of hello app created in hello [Get started with IoT Hub] tutorial, sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span> <span data-ttu-id="b14a7-113">Bu uygulama, IOT Hub ile Merhaba AMQP protokolünü toocommunicate kullanır.</span><span class="sxs-lookup"><span data-stu-id="b14a7-113">This app uses hello AMQP protocol toocommunicate with IoT Hub.</span></span>
* <span data-ttu-id="b14a7-114">**Read-d2c-messages** cihaz uygulamanız tarafından gönderilen hello telemetri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="b14a7-114">**read-d2c-messages** displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="b14a7-115">**Okuma kritik-sıra** hello Service Bus kuyruğu bağlı toohello IOT hub'ı kritik iletileri hello çıkarır.</span><span class="sxs-lookup"><span data-stu-id="b14a7-115">**read-critical-queue** de-queues hello critical messages from hello Service Bus queue attached toohello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="b14a7-116">IOT hub'ı birçok cihaz platformları ve C, Java ve JavaScript gibi diller için SDK desteğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="b14a7-116">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="b14a7-117">Nasıl tooreplace hello cihaz Bu öğreticide bir fiziksel cihaz ile ilgili yönergeler için ve nasıl tooconnect aygıtları tooan IOT hub'ına bakın hello [Azure IOT Geliştirme Merkezi].</span><span class="sxs-lookup"><span data-stu-id="b14a7-117">For instructions on how tooreplace hello device in this tutorial with a physical device, and how tooconnect devices tooan IoT Hub, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="b14a7-118">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="b14a7-118">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="b14a7-119">Merhaba tam çalışma sürümü [IOT Hub ile çalışmaya başlama] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="b14a7-119">A complete working version of hello [Get started with IoT Hub] tutorial.</span></span>
* <span data-ttu-id="b14a7-120">Merhaba son [Java SE Geliştirme Seti 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="b14a7-120">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="b14a7-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="b14a7-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="b14a7-122">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="b14a7-122">An active Azure account.</span></span> <span data-ttu-id="b14a7-123">(Bir hesabınız yoksa, [ücretsiz bir hesap] oluşturabilirsiniz [lnk-free-trial] yalnızca birkaç dakika içinde.)</span><span class="sxs-lookup"><span data-stu-id="b14a7-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="b14a7-124">Bazı temel bilgiye sahip [Azure Storage] ve [Azure Service Bus].</span><span class="sxs-lookup"><span data-stu-id="b14a7-124">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages-from-a-device-app"></a><span data-ttu-id="b14a7-125">Bir aygıt uygulamadan etkileşimli ileti gönderme</span><span class="sxs-lookup"><span data-stu-id="b14a7-125">Send interactive messages from a device app</span></span>
<span data-ttu-id="b14a7-126">Bu bölümde, hello oluşturduğunuz hello cihaz uygulamayı değiştirmek [IOT Hub ile çalışmaya başlama] öğretici toooccasionally hemen işleme gerektiren ileti gönderme.</span><span class="sxs-lookup"><span data-stu-id="b14a7-126">In this section, you modify hello device app you created in hello [Get started with IoT Hub] tutorial toooccasionally send messages that require immediate processing.</span></span>

1. <span data-ttu-id="b14a7-127">Bir metin düzenleyicisi tooopen hello simulated-device\src\main\java\com\mycompany\app\App.java dosyasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="b14a7-127">Use a text editor tooopen hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span> <span data-ttu-id="b14a7-128">Bu dosya hello hello kodunu içerir **simulated-device** hello oluşturduğunuz uygulama [IOT Hub ile çalışmaya başlama] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="b14a7-128">This file contains hello code for hello **simulated-device** app you created in hello [Get started with IoT Hub] tutorial.</span></span>

2. <span data-ttu-id="b14a7-129">Hello yerine **MessageSender** koddan hello sınıfıyla:</span><span class="sxs-lookup"><span data-stu-id="b14a7-129">Replace hello **MessageSender** class with hello following code:</span></span>

    ```java
    private static class MessageSender implements Runnable {

        public void run()  {
            try {
                double minTemperature = 20;
                double minHumidity = 60;
                Random rand = new Random();

                while (true) {
                    String msgStr;
                    Message msg;
                    if (new Random().nextDouble() > 0.7) {
                        msgStr = "This is a critical message.";
                        msg = new Message(msgStr);
                        msg.setProperty("level", "critical");
                    } else {
                        double currentTemperature = minTemperature + rand.nextDouble() * 15;
                        double currentHumidity = minHumidity + rand.nextDouble() * 20; 
                        TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
                        telemetryDataPoint.deviceId = deviceId;
                        telemetryDataPoint.temperature = currentTemperature;
                        telemetryDataPoint.humidity = currentHumidity;

                        msgStr = telemetryDataPoint.serialize();
                        msg = new Message(msgStr);
                    }
                    
                    System.out.println("Sending: " + msgStr);

                    Object lockobj = new Object();
                    EventCallback callback = new EventCallback();
                    client.sendEventAsync(msg, callback, lockobj);

                    synchronized (lockobj) {
                        lockobj.wait();
                    }
                    Thread.sleep(1000);
                }
            } catch (InterruptedException e) {
                System.out.println("Finished.");
            }
        }
    }
    ```
   
    <span data-ttu-id="b14a7-130">Bu yöntem rastgele hello özelliği ekler `"level": "critical"` hello uygulama arka uç tarafından Acil eylem gerektiren bir ileti taklit eden bir hello aygıt tarafından gönderilen toomessages.</span><span class="sxs-lookup"><span data-stu-id="b14a7-130">This method randomly adds hello property `"level": "critical"` toomessages sent by hello device, which simulates a message that requires immediate action by hello application back-end.</span></span> <span data-ttu-id="b14a7-131">Bu IOT hub'ın hello ileti toohello uygun mesajı hedef yönlendirebilir şekilde hello uygulama bu bilgileri hello ileti özelliklerinde yerine hello ileti gövdesinde geçirir.</span><span class="sxs-lookup"><span data-stu-id="b14a7-131">hello application passes this information in hello message properties, instead of in hello message body, so that IoT Hub can route hello message toohello proper message destination.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b14a7-132">Özellikler tooroute ileti işleme, ayrıca burada gösterilen toohello etkin yolunuzda örnek soğuk yolu da dahil olmak üzere çeşitli senaryolar için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b14a7-132">You can use message properties tooroute messages for various scenarios including cold-path processing, in addition toohello hot path example shown here.</span></span>

2. <span data-ttu-id="b14a7-133">Merhaba simulated-device\src\main\java\com\mycompany\app\App.java dosyasını kaydedip kapatın.</span><span class="sxs-lookup"><span data-stu-id="b14a7-133">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b14a7-134">Basitlik Hello artırmak amacıyla için bu öğreticiyi herhangi bir yeniden deneme ilkesi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="b14a7-134">For hello sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="b14a7-135">Üretim kodunda hello MSDN makalesinde önerilen üstel geri alma gibi bir yeniden deneme ilkesi uygulamalıdır [geçici hata işleme].</span><span class="sxs-lookup"><span data-stu-id="b14a7-135">In production code, you should implement a retry policy such as exponential backoff, as suggested in hello MSDN article [Transient Fault Handling].</span></span>

3. <span data-ttu-id="b14a7-136">toobuild hello **simulated-device** Maven kullanarak uygulama komutu hello hello simulated-device klasöründeki komut isteminde aşağıdaki hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="b14a7-136">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-tooyour-iot-hub-and-route-messages-tooit"></a><span data-ttu-id="b14a7-137">Bir kuyruk tooyour IOT hub ve rota iletileri tooit Ekle</span><span class="sxs-lookup"><span data-stu-id="b14a7-137">Add a queue tooyour IoT hub and route messages tooit</span></span>

<span data-ttu-id="b14a7-138">Bu bölümde, hizmet veri yolu kuyruğu oluşturma, tooyour IOT hub'ı bağlanmak ve selamlama iletisine özellikte hello varlığına göre IOT hub toosend iletileri toohello sırası yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b14a7-138">In this section, you create a Service Bus queue, connect it tooyour IoT hub, and configure your IoT hub toosend messages toohello queue based on hello presence of a property on hello message.</span></span> <span data-ttu-id="b14a7-139">Service Bus sıralarından tooprocess nasıl iletileri hakkında daha fazla bilgi için bkz: [kuyruklarla çalışmaya başlama][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="b14a7-139">For more information about how tooprocess messages from Service Bus queues, see [Get started with queues][lnk-sb-queues-java].</span></span>

1. <span data-ttu-id="b14a7-140">Service Bus kuyruğuna açıklandığı gibi oluşturmak [kuyruklarla çalışmaya başlama][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="b14a7-140">Create a Service Bus queue as described in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="b14a7-141">Merhaba ad alanı ve sıra adını not edin.</span><span class="sxs-lookup"><span data-stu-id="b14a7-141">Make a note of hello namespace and queue name.</span></span>

2. <span data-ttu-id="b14a7-142">Azure portal Merhaba, IOT hub'ınızı açın ve'ı tıklatın **uç noktaları**.</span><span class="sxs-lookup"><span data-stu-id="b14a7-142">In hello Azure portal, open your IoT hub and click **Endpoints**.</span></span>

    ![IOT hub uç noktaları][30]

3. <span data-ttu-id="b14a7-144">Merhaba, **uç noktaları** dikey penceresinde tıklatın **Ekle** en üst tooadd sıra tooyour IOT hub'ınızı hello.</span><span class="sxs-lookup"><span data-stu-id="b14a7-144">In hello **Endpoints** blade, click **Add** at hello top tooadd your queue tooyour IoT hub.</span></span> <span data-ttu-id="b14a7-145">Ad hello endpoint **CriticalQueue** ve hello aşağı açılan listeler tooselect kullanmak **Service Bus kuyruğuna**, hizmet veri yolu ad alanı, sıra içinde bulunduğu hello ve Merhaba, kuyruk adı.</span><span class="sxs-lookup"><span data-stu-id="b14a7-145">Name hello endpoint **CriticalQueue** and use hello drop-downs tooselect **Service Bus queue**, hello Service Bus namespace in which your queue resides, and hello name of your queue.</span></span> <span data-ttu-id="b14a7-146">İşiniz bittiğinde tıklatın **kaydetmek** hello altındaki.</span><span class="sxs-lookup"><span data-stu-id="b14a7-146">When you are done, click **Save** at hello bottom.</span></span>

    ![Bir uç nokta ekleme][31]

4. <span data-ttu-id="b14a7-148">Şimdi **yollar** IOT hub'ınızdaki.</span><span class="sxs-lookup"><span data-stu-id="b14a7-148">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="b14a7-149">Tıklatın **Ekle** hello üstünde hello dikey toocreate toohello sıra, yalnızca iletileri yönlendiren bir yönlendirme kuralı eklendi.</span><span class="sxs-lookup"><span data-stu-id="b14a7-149">Click **Add** at hello top of hello blade toocreate a routing rule that routes messages toohello queue you just added.</span></span> <span data-ttu-id="b14a7-150">Seçin **DeviceTelemetry** hello veri kaynağı olarak.</span><span class="sxs-lookup"><span data-stu-id="b14a7-150">Select **DeviceTelemetry** as hello source of data.</span></span> <span data-ttu-id="b14a7-151">Girin `level="critical"` hello koşulu olarak ve hello sıra yeni eklenen kural endpoint yönlendirme hello olarak özel bir uç noktası olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="b14a7-151">Enter `level="critical"` as hello condition, and choose hello queue you just added as a custom endpoint as hello routing rule endpoint.</span></span> <span data-ttu-id="b14a7-152">İşiniz bittiğinde tıklatın **kaydetmek** hello altındaki.</span><span class="sxs-lookup"><span data-stu-id="b14a7-152">When you are done, click **Save** at hello bottom.</span></span>

    ![Bir yol ekleme][32]

    <span data-ttu-id="b14a7-154">Merhaba geri dönüş rota çok ayarlandığından emin olun**ON**.</span><span class="sxs-lookup"><span data-stu-id="b14a7-154">Make sure hello fallback route is set too**ON**.</span></span> <span data-ttu-id="b14a7-155">Bu ayar hello varsayılan bir IOT hub'ının yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="b14a7-155">This setting is hello default configuration of an IoT hub.</span></span>

    ![Geri dönüş yolu][33]

## <a name="optional-read-from-hello-queue-endpoint"></a><span data-ttu-id="b14a7-157">(İsteğe bağlı) Merhaba sıra uç noktasından okumak</span><span class="sxs-lookup"><span data-stu-id="b14a7-157">(Optional) Read from hello queue endpoint</span></span>

<span data-ttu-id="b14a7-158">Merhaba yönergeleri takip ederek Merhaba iletileri hello sıra uç noktasından isteğe bağlı olarak okuyabilirsiniz [kuyruklarla çalışmaya başlama][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="b14a7-158">You can optionally read hello messages from hello queue endpoint by following hello instructions in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="b14a7-159">Ad hello uygulama **okuma kritik-sıra**.</span><span class="sxs-lookup"><span data-stu-id="b14a7-159">Name hello app **read-critical-queue**.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="b14a7-160">Merhaba uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b14a7-160">Run hello applications</span></span>

<span data-ttu-id="b14a7-161">Hazır toorun hello üç uygulama sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="b14a7-161">Now you are ready toorun hello three applications.</span></span>

1. <span data-ttu-id="b14a7-162">toorun hello **read-d2c-messages** uygulamasında, bir komut istemi veya kabuk toohello read-d2c klasörüne gidin ve hello aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="b14a7-162">toorun hello **read-d2c-messages** application, in a command prompt or shell navigate toohello read-d2c folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![Read-d2c-messages çalıştırın][readd2c]

2. <span data-ttu-id="b14a7-164">toorun hello **okuma kritik-sıra** uygulamasında, bir komut istemi veya kabuk toohello okuma kritik-sıra klasörüne gidin ve hello aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="b14a7-164">toorun hello **read-critical-queue** application, in a command prompt or shell navigate toohello read-critical-queue folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Read-kritik-messages çalıştırın][readqueue]

3. <span data-ttu-id="b14a7-166">toorun hello **simulated-device** uygulamasında, bir komut istemi veya kabuk toohello simulated-device klasörüne gidin ve hello aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="b14a7-166">toorun hello **simulated-device** app, in a command prompt or shell navigate toohello simulated-device folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Simulated-device çalıştırın][simulateddevice]

## <a name="next-steps"></a><span data-ttu-id="b14a7-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b14a7-168">Next steps</span></span>

<span data-ttu-id="b14a7-169">Bu öğreticide, nasıl tooreliably gönderme cihaz bulut iletilerini IOT Hub'ının hello ileti yönlendirme işlevini kullanarak öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="b14a7-169">In this tutorial, you learned how tooreliably dispatch device-to-cloud messages by using hello message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="b14a7-170">Merhaba [toosend bulut-cihaz IOT Hub ile nasıl iletileri] [ lnk-c2d] nasıl toosend çözüm arka ucunuz tooyour aygıtlardan iletileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="b14a7-170">hello [How toosend cloud-to-device messages with IoT Hub][lnk-c2d] shows you how toosend messages tooyour devices from your solution back end.</span></span>

<span data-ttu-id="b14a7-171">IOT hub'ı kullanan tam uçtan uca çözümler toosee örnekleri bkz [Azure IOT paketi][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="b14a7-171">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="b14a7-172">IOT Hub ile çözümleri geliştirme hakkında daha fazla toolearn bkz hello [IOT Hub Geliştirici Kılavuzu].</span><span class="sxs-lookup"><span data-stu-id="b14a7-172">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<span data-ttu-id="b14a7-173">IOT Hub içinde ileti yönlendirme hakkında daha fazla toolearn bkz [IOT Hub ile iletileri almasına ve göndermesine][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="b14a7-173">toolearn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
<!-- TODO: UPDATE PICTURES -->
[simulateddevice]: ./media/iot-hub-java-java-process-d2c/runsimulateddevice.png
[readd2c]: ./media/iot-hub-java-java-process-d2c/runprocessinteractive.png
[readqueue]: ./media/iot-hub-java-java-process-d2c/runprocessd2c.png

[30]: ./media/iot-hub-java-java-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-java-java-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-java-java-process-d2c/route-creation.png
[33]: ./media/iot-hub-java-java-process-d2c/fallback-route.png

<!-- Links -->

[lnk-sb-queues-java]: ../service-bus-messaging/service-bus-java-how-to-use-queues.md

[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/
[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/

[IOT Hub Geliştirici Kılavuzu]: iot-hub-devguide.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[IOT Hub ile çalışmaya başlama]: iot-hub-java-java-getstarted.md
[Azure IOT Geliştirme Merkezi]: https://azure.microsoft.com/develop/iot
[geçici hata işleme]: https://msdn.microsoft.com/library/hh675232.aspx

<!-- Links -->
[Geçici hata işleme]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-c2d]: iot-hub-java-java-c2d.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
