---
title: "Azure IOT hub'ı (Java) aaaCloud cihaza iletileriyle | Microsoft Docs"
description: "Nasıl toosend bulut-cihaz hello Azure IOT SDK'ları için Java kullanarak Azure IOT hub'ı tooa aygıttan iletileri. Bir sanal cihaz uygulaması tooreceive bulut-cihaz iletilerini değiştirmek ve arka uç uygulaması toosend hello bulut-cihaz iletilerini değiştirin."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7f785ea8-e7c2-40c5-87ef-96525e9b9e1e
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: 8721f18428c849ed9a04aa2e45c65605c3e38101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-java"></a><span data-ttu-id="d2ce8-104">IOT hub'ı (Java) sahip bulut-cihaz iletilerini gönder</span><span class="sxs-lookup"><span data-stu-id="d2ce8-104">Send cloud-to-device messages with IoT Hub (Java)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

<span data-ttu-id="d2ce8-105">Azure IOT Hub, milyonlarca cihaza arasında güvenilir ve güvenli çift yönlü iletişimler sağlayan tam olarak yönetilen hizmet etkinleştirin ve bir çözüm arka ucu ' dir.</span><span class="sxs-lookup"><span data-stu-id="d2ce8-105">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="d2ce8-106">Merhaba [IOT Hub ile çalışmaya başlama] öğretici nasıl toocreate IOT hub'ı, bir cihaz kimliği, sağlamak ve cihaz-bulut iletileri gönderen bir sanal cihaz uygulamasının kodu gösterir.</span><span class="sxs-lookup"><span data-stu-id="d2ce8-106">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="d2ce8-107">Bu öğretici derlemeler [IOT Hub ile çalışmaya başlama].</span><span class="sxs-lookup"><span data-stu-id="d2ce8-107">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="d2ce8-108">Size bir nasıl gösterir için:</span><span class="sxs-lookup"><span data-stu-id="d2ce8-108">It shows you how to:</span></span>

* <span data-ttu-id="d2ce8-109">Çözüm arka ucunuz, bulut-cihaz iletilerini tooa tek cihaz IOT hub'ı aracılığıyla gönderin.</span><span class="sxs-lookup"><span data-stu-id="d2ce8-109">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="d2ce8-110">Bir cihazda bulut-cihaz iletilerini alır.</span><span class="sxs-lookup"><span data-stu-id="d2ce8-110">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="d2ce8-111">Çözüm arka ucunuz, teslimat alındısı iste (*geri bildirim*) tooa cihaz IOT Hub'ından gönderilen iletileri için.</span><span class="sxs-lookup"><span data-stu-id="d2ce8-111">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="d2ce8-112">Hello bulut-cihaz iletilerini hakkında daha fazla bilgi bulabilirsiniz [IOT Hub Geliştirici Kılavuzu][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="d2ce8-112">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="d2ce8-113">Bu öğreticinin Hello sonunda, iki Java konsol uygulamaları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d2ce8-113">At hello end of this tutorial, you run two Java console apps:</span></span>

* <span data-ttu-id="d2ce8-114">**simulated-device**, oluşturulan hello uygulama değiştirilmiş bir sürümünü [IOT Hub ile çalışmaya başlama], hangi tooyour IOT hub'ı bağlar ve bulut-cihaz iletilerini alır.</span><span class="sxs-lookup"><span data-stu-id="d2ce8-114">**simulated-device**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="d2ce8-115">**Send-c2d-messages**, hangi bulut aygıt iletisi toohello sanal cihaz uygulaması IOT hub'ı üzerinden gönderir ve teslimat alındısı alır.</span><span class="sxs-lookup"><span data-stu-id="d2ce8-115">**send-c2d-messages**, which sends a cloud-to-device message toohello simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="d2ce8-116">IOT Hub SDK desteği birçok cihaz platformları ve Azure IOT cihaz SDK'ları aracılığıyla dilleri (C, Java ve Javascript dahil) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d2ce8-116">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="d2ce8-117">Adım adım yönergeler nasıl tooconnect aygıt toothis öğreticinin kod ve genellikle tooAzure IOT hub'ı görmek için hello [Azure IOT Geliştirme Merkezi].</span><span class="sxs-lookup"><span data-stu-id="d2ce8-117">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="d2ce8-118">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="d2ce8-118">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="d2ce8-119">Merhaba tam çalışma sürümü [IOT Hub ile çalışmaya başlama](iot-hub-java-java-getstarted.md) veya [işlem IOT Hub cihaz bulut iletilerini](iot-hub-java-java-process-d2c.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="d2ce8-119">A complete working version of hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) or [Process IoT Hub device-to-cloud messages](iot-hub-java-java-process-d2c.md) tutorial.</span></span>
* <span data-ttu-id="d2ce8-120">Merhaba son [Java SE Geliştirme Seti 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="d2ce8-120">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="d2ce8-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="d2ce8-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="d2ce8-122">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="d2ce8-122">An active Azure account.</span></span> <span data-ttu-id="d2ce8-123">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="d2ce8-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-simulated-device-app"></a><span data-ttu-id="d2ce8-124">Merhaba sanal cihaz uygulamasının ileti alma</span><span class="sxs-lookup"><span data-stu-id="d2ce8-124">Receive messages in hello simulated device app</span></span>

<span data-ttu-id="d2ce8-125">Bu bölümde, oluşturduğunuz hello sanal cihaz uygulamasının değiştirme [IOT Hub ile çalışmaya başlama] tooreceive bulut cihaza iletilerden hello IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="d2ce8-125">In this section, you modify hello simulated device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="d2ce8-126">Bir metin düzenleyicisi kullanarak hello simulated-device\src\main\java\com\mycompany\app\App.java dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="d2ce8-126">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

2. <span data-ttu-id="d2ce8-127">Merhaba aşağıdakileri ekleyin **MessageCallback** sınıf hello içinde iç içe bir sınıf olarak **uygulama** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="d2ce8-127">Add hello following **MessageCallback** class as a nested class inside hello **App** class.</span></span> <span data-ttu-id="d2ce8-128">Merhaba **yürütme** yöntemi hello cihaz IOT Hub'ından bir ileti aldığında çağrılır.</span><span class="sxs-lookup"><span data-stu-id="d2ce8-128">hello **execute** method is invoked when hello device receives a message from IoT Hub.</span></span> <span data-ttu-id="d2ce8-129">Bu örnekte, hello cihaz her zaman hello IOT hub'ı selamlama iletisine tamamlandığını bildirir:</span><span class="sxs-lookup"><span data-stu-id="d2ce8-129">In this example, hello device always notifies hello IoT hub that it has completed hello message:</span></span>

    ```java
    private static class AppMessageCallback implements MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));
    
        return IotHubMessageResult.COMPLETE;
      }
    }
    ```
3. <span data-ttu-id="d2ce8-130">Merhaba değiştirme **ana** yöntemi toocreate bir **AppMessageCallback** örneği ve çağrı hello **setMessageCallback** gibi hello istemci açılmadan önce yöntemi:</span><span class="sxs-lookup"><span data-stu-id="d2ce8-130">Modify hello **main** method toocreate an **AppMessageCallback** instance and call hello **setMessageCallback** method before it opens hello client as follows:</span></span>

    ```java
    client = new DeviceClient(connString, protocol);
   
    MessageCallback callback = new AppMessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```

    > [!NOTE]
    > <span data-ttu-id="d2ce8-131">HTTP MQTT veya AMQP yerine hello taşıma olarak kullanırsanız, hello **DeviceClient** seyrek IOT Hub (değerinden 25 dakikada bir) gelen iletileri örneği denetler.</span><span class="sxs-lookup"><span data-stu-id="d2ce8-131">If you use HTTP instead of MQTT or AMQP as hello transport, hello **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="d2ce8-132">Merhaba hello farklarını MQTT, AMQP ve HTTP desteği ve IOT hub'ı azaltma hakkında daha fazla bilgi için bkz: [IOT Hub Geliştirici Kılavuzu][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="d2ce8-132">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

4. <span data-ttu-id="d2ce8-133">toobuild hello **simulated-device** Maven kullanarak uygulama komutu hello hello simulated-device klasöründeki komut isteminde aşağıdaki hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="d2ce8-133">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="d2ce8-134">Bulut cihaza ileti gönderme</span><span class="sxs-lookup"><span data-stu-id="d2ce8-134">Send a cloud-to-device message</span></span>

<span data-ttu-id="d2ce8-135">Bu bölümde, bulut-cihaz iletilerini toohello sanal cihaz uygulamasının gönderen bir Java konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d2ce8-135">In this section, you create a Java console app that sends cloud-to-device messages toohello simulated device app.</span></span> <span data-ttu-id="d2ce8-136">Hello eklediğiniz hello aygıtın aygıt kimliği hello [IOT Hub ile çalışmaya başlama] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="d2ce8-136">You need hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="d2ce8-137">Hello bulabileceğiniz hub'ınız için IOT Hub bağlantı dizesine hello de [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="d2ce8-137">You also need hello IoT Hub connection string for your hub that you can find in hello [Azure portal].</span></span>

1. <span data-ttu-id="d2ce8-138">Adlı bir Maven projesi oluşturun **c2d iletileri gönderme** komutu, komut isteminde aşağıdaki hello kullanarak.</span><span class="sxs-lookup"><span data-stu-id="d2ce8-138">Create a Maven project called **send-c2d-messages** using hello following command at your command prompt.</span></span> <span data-ttu-id="d2ce8-139">Bu komut tek ve uzun bir komut olduğuna dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="d2ce8-139">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="d2ce8-140">Komut isteminizde toohello yeni gönderme-c2d-messages klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="d2ce8-140">At your command prompt, navigate toohello new send-c2d-messages folder.</span></span>

3. <span data-ttu-id="d2ce8-141">Bir metin düzenleyicisi kullanarak hello Gönder-c2d-messages klasöründeki hello pom.xml dosyasını açın ve bağımlılık toohello aşağıdaki hello ekleyin **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="d2ce8-141">Using a text editor, open hello pom.xml file in hello send-c2d-messages folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="d2ce8-142">Merhaba bağımlılık ekleme sağlar toouse hello **iothub-java-service-client** , uygulama toocommunicate IOT hub hizmetinizle paketinde:</span><span class="sxs-lookup"><span data-stu-id="d2ce8-142">Adding hello dependency enables you toouse hello **iothub-java-service-client** package in your application toocommunicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="d2ce8-143">Hello için en son sürümünü denetleyebilir **IOT hizmeti istemcisi** kullanarak [Maven arama][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="d2ce8-143">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="d2ce8-144">Merhaba pom.xml dosyasını kaydedip kapatın.</span><span class="sxs-lookup"><span data-stu-id="d2ce8-144">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="d2ce8-145">Bir metin düzenleyicisi kullanarak hello send-c2d-messages\src\main\java\com\mycompany\app\App.java dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="d2ce8-145">Using a text editor, open hello send-c2d-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="d2ce8-146">Merhaba aşağıdakileri ekleyin **alma** deyimleri toohello dosyası:</span><span class="sxs-lookup"><span data-stu-id="d2ce8-146">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="d2ce8-147">Aşağıdaki sınıf düzeyi değişkenleri toohello hello eklemek **uygulama** sınıfına **{yourhubconnectionstring}** ve **{yourdeviceid}** hello ile daha önce not ettiğiniz değerleri:</span><span class="sxs-lookup"><span data-stu-id="d2ce8-147">Add hello following class-level variables toohello **App** class, replacing **{yourhubconnectionstring}** and **{yourdeviceid}** with hello values your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```

8. <span data-ttu-id="d2ce8-148">Hello yerine **ana** koddan hello yöntemiyle.</span><span class="sxs-lookup"><span data-stu-id="d2ce8-148">Replace hello **main** method with hello following code.</span></span> <span data-ttu-id="d2ce8-149">Bu kod tooyour IOT hub'ı bağlandığında, bir ileti tooyour cihaz gönderir ve sonra o hello aygıt alınan ve işlenen hello iletisi için bir bildirim bekler:</span><span class="sxs-lookup"><span data-stu-id="d2ce8-149">This code connects tooyour IoT hub, sends a message tooyour device, and then waits for an acknowledgment that hello device received and processed hello message:</span></span>
   
    ```java
    public static void main(String[] args) throws IOException,
        URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(
        connectionString, protocol);
   
      if (serviceClient != null) {
        serviceClient.open();
        FeedbackReceiver feedbackReceiver = serviceClient
          .getFeedbackReceiver();
        if (feedbackReceiver != null) feedbackReceiver.open();
   
        Message messageToSend = new Message("Cloud toodevice message.");
        messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);
   
        serviceClient.send(deviceId, messageToSend);
        System.out.println("Message sent toodevice");
   
        FeedbackBatch feedbackBatch = feedbackReceiver.receive(10000);
        if (feedbackBatch != null) {
          System.out.println("Message feedback received, feedback time: "
            + feedbackBatch.getEnqueuedTimeUtc().toString());
        }
   
        if (feedbackReceiver != null) feedbackReceiver.close();
        serviceClient.close();
      }
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="d2ce8-150">Basitlik'ın artırmak amacıyla için bu öğreticiyi herhangi bir yeniden deneme ilkesi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="d2ce8-150">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="d2ce8-151">Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme].</span><span class="sxs-lookup"><span data-stu-id="d2ce8-151">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>


9. <span data-ttu-id="d2ce8-152">toobuild hello **simulated-device** Maven kullanarak uygulama komutu hello hello simulated-device klasöründeki komut isteminde aşağıdaki hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="d2ce8-152">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="d2ce8-153">Merhaba uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="d2ce8-153">Run hello applications</span></span>

<span data-ttu-id="d2ce8-154">Hazır toorun hello uygulamaları sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="d2ce8-154">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="d2ce8-155">Merhaba simulated-device klasöründeki komut isteminde, telemetri tooyour IOT hub ve toolisten, hub'dan gönderilen bulut cihaz iletileri gönderme komutu toobegin aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d2ce8-155">At a command prompt in hello simulated-device folder, run hello following command toobegin sending telemetry tooyour IoT hub and toolisten for cloud-to-device messages sent from your hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Merhaba sanal cihaz uygulamasının çalıştırın][img-simulated-device]

2. <span data-ttu-id="d2ce8-157">Hello Gönder-c2d-messages klasöründeki komut isteminde, bir bulut aygıt iletisi ve geri bildirim bekle komutu toosend aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d2ce8-157">At a command prompt in hello send-c2d-messages folder, run hello following command toosend a cloud-to-device message and wait for a feedback acknowledgment:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Merhaba komutu toosend hello bulut cihaz ileti çalıştırın][img-send-command]

## <a name="next-steps"></a><span data-ttu-id="d2ce8-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d2ce8-159">Next steps</span></span>

<span data-ttu-id="d2ce8-160">Bu öğreticide, nasıl öğrenilen toosend ve bulut-cihaz iletilerini.</span><span class="sxs-lookup"><span data-stu-id="d2ce8-160">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="d2ce8-161">IOT hub'ı kullanan tam uçtan uca çözümler toosee örnekleri bkz [Azure IOT paketi].</span><span class="sxs-lookup"><span data-stu-id="d2ce8-161">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="d2ce8-162">IOT Hub ile çözümleri geliştirme hakkında daha fazla toolearn bkz hello [IOT Hub Geliştirici Kılavuzu].</span><span class="sxs-lookup"><span data-stu-id="d2ce8-162">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-java-java-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-java-java-c2d/sendc2d.png
<!-- Links -->

[IOT Hub ile çalışmaya başlama]: iot-hub-java-java-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[IOT Hub Geliştirici Kılavuzu]: iot-hub-devguide.md
[Azure IOT Geliştirme Merkezi]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java
[geçici hata işleme]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure portal]: https://portal.azure.com
[Azure IOT paketi]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22