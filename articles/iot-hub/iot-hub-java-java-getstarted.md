---
title: "aaaGet başlatılan Azure IOT Hub (Java) | Microsoft Docs"
description: "Nasıl tooAzure IOT Hub'ın IOT SDK'ları için Java kullanarak toosend cihaz-bulut iletileri öğrenin. Sanal cihazı ve hizmet uygulamaları tooregister Cihazınızı oluşturmak, iletileri gönderir ve IOT hub'ından iletileri okur."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 70dae4a8-0e98-4c53-b5a5-9d6963abb245
ms.service: iot-hub
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac954f0522b46ed2a5b4a819bc611c13be0b9a9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-java"></a><span data-ttu-id="7027f-104">Java kullanarak aygıt tooyour IOT hub'ınıza bağlanın</span><span class="sxs-lookup"><span data-stu-id="7027f-104">Connect your device tooyour IoT hub using Java</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="7027f-105">Bu öğretici Hello sonunda üç Java konsol uygulamaları vardır:</span><span class="sxs-lookup"><span data-stu-id="7027f-105">At hello end of this tutorial, you have three Java console apps:</span></span>

* <span data-ttu-id="7027f-106">**Create-device-identity**ilişkili güvenlik anahtarı tooconnect cihaz uygulamanız ve bir cihaz kimliği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7027f-106">**create-device-identity**, which creates a device identity and associated security key tooconnect your device app.</span></span>
* <span data-ttu-id="7027f-107">**Read-d2c-messages**, cihaz uygulamanız tarafından gönderilen hello telemetri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7027f-107">**read-d2c-messages**, which displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="7027f-108">**simulated-device**, hangi tooyour IOT hub'ı daha önce oluşturduğunuz hello cihaz kimliği bağlanır ve hello MQTT protokolünü kullanarak her saniye bir telemetri iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="7027f-108">**simulated-device**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="7027f-109">Merhaba makale [Azure IOT SDK'ları] [ lnk-hub-sdks] aygıtlar ve çözüm arka ucunuz hem uygulamalar toorun toobuild kullanabileceğiniz hello Azure IOT SDK'ları hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7027f-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both apps toorun on devices and your solution back end.</span></span>

<span data-ttu-id="7027f-110">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7027f-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="7027f-111">Merhaba son [Java SE Geliştirme Seti 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="7027f-111">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span> 
* [<span data-ttu-id="7027f-112">Maven 3</span><span class="sxs-lookup"><span data-stu-id="7027f-112">Maven 3</span></span>](https://maven.apache.org/install.html) 
* <span data-ttu-id="7027f-113">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="7027f-113">An active Azure account.</span></span> <span data-ttu-id="7027f-114">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="7027f-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="7027f-115">Son adım olarak, hello Not **birincil anahtar** değeri.</span><span class="sxs-lookup"><span data-stu-id="7027f-115">As a final step, make a note of hello **Primary key** value.</span></span> <span data-ttu-id="7027f-116">Ardından **uç noktaları** ve hello **olayları** yerleşik uç noktası.</span><span class="sxs-lookup"><span data-stu-id="7027f-116">Then click **Endpoints** and hello **Events** built-in endpoint.</span></span> <span data-ttu-id="7027f-117">Merhaba üzerinde **özellikleri** dikey penceresinde hello Not **Event Hub ile uyumlu adı** ve hello **Event Hub ile uyumlu uç nokta** adresi.</span><span class="sxs-lookup"><span data-stu-id="7027f-117">On hello **Properties** blade, make a note of hello **Event Hub-compatible name** and hello **Event Hub-compatible endpoint** address.</span></span> <span data-ttu-id="7027f-118">**read-d2c-messages** uygulamanızı oluştururken bu üç değere sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7027f-118">You need these three values when you create your **read-d2c-messages** app.</span></span>

![Azure portalı IoT Hub Mesajlaşma dikey penceresi][6]

<span data-ttu-id="7027f-120">IoT Hub’ınızı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="7027f-120">You have now created your IoT hub.</span></span> <span data-ttu-id="7027f-121">Merhaba IOT Hub ana bilgisayar adı, IOT Hub bağlantı dizesine, IOT hub'ı birincil anahtar, Event Hub ile uyumlu ada ve Event Hub ile uyumlu uç noktası Bu öğretici toocomplete ihtiyacınız var.</span><span class="sxs-lookup"><span data-stu-id="7027f-121">You have hello IoT Hub host name, IoT Hub connection string, IoT Hub Primary Key, Event Hub-compatible name, and Event Hub-compatible endpoint you need toocomplete this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="7027f-122">Cihaz kimliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="7027f-122">Create a device identity</span></span>
<span data-ttu-id="7027f-123">Bu bölümde, hello kimlik IOT hub'ınızı kayıt defterinde bir cihaz kimliği oluşturan bir Java konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7027f-123">In this section, you create a Java console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="7027f-124">Merhaba kimlik kayıt defterinde girişi olmayan sürece bir aygıt tooIoT hub bağlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="7027f-124">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="7027f-125">Daha fazla bilgi için bkz: Merhaba **kimlik kayıt defteri** hello bölümünü [IOT Hub Geliştirici Kılavuzu][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="7027f-125">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="7027f-126">Bu konsol uygulamasını çalıştırdığınızda, benzersiz cihaz kimliği oluşturur ve cihaz bulut gönderdiğinde Cihazınızı tooidentify kendisini kullanabileceğiniz anahtar tooIoT Hub iletileri.</span><span class="sxs-lookup"><span data-stu-id="7027f-126">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="7027f-127">iot-java-get-started adlı bir boş klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7027f-127">Create an empty folder called iot-java-get-started.</span></span> <span data-ttu-id="7027f-128">Merhaba iot-java-get-started klasöründe adlı bir Maven projesi oluşturun **create-device-identity** komutu, komut isteminde aşağıdaki hello kullanarak.</span><span class="sxs-lookup"><span data-stu-id="7027f-128">In hello iot-java-get-started folder, create a Maven project called **create-device-identity** using hello following command at your command prompt.</span></span> <span data-ttu-id="7027f-129">Bunun tek ve uzun bir komut olduğunu unutmayın:</span><span class="sxs-lookup"><span data-stu-id="7027f-129">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="7027f-130">Komut isteminizde toohello create-device-identity klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="7027f-130">At your command prompt, navigate toohello create-device-identity folder.</span></span>

3. <span data-ttu-id="7027f-131">Bir metin düzenleyicisi kullanarak hello create-device-identity klasörüne hello pom.xml dosyasını açın ve bağımlılık toohello aşağıdaki hello ekleyin **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="7027f-131">Using a text editor, open hello pom.xml file in hello create-device-identity folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="7027f-132">Bu bağımlılık, toouse hello IOT hizmeti istemci paketi uygulamanızda sağlar:</span><span class="sxs-lookup"><span data-stu-id="7027f-132">This dependency enables you toouse hello iot-service-client package in your app:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="7027f-133">Hello için en son sürümünü denetleyebilir **IOT hizmeti istemcisi** kullanarak [Maven arama][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="7027f-133">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="7027f-134">Merhaba pom.xml dosyasını kaydedip kapatın.</span><span class="sxs-lookup"><span data-stu-id="7027f-134">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="7027f-135">Bir metin düzenleyicisi kullanarak hello create-device-identity\src\main\java\com\mycompany\app\App.java dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="7027f-135">Using a text editor, open hello create-device-identity\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="7027f-136">Merhaba aşağıdakileri ekleyin **alma** deyimleri toohello dosyası:</span><span class="sxs-lookup"><span data-stu-id="7027f-136">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.Device;
    import com.microsoft.azure.sdk.iot.service.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="7027f-137">Aşağıdaki sınıf düzeyi değişkenleri toohello hello eklemek **uygulama** sınıfına **{yourhubconnectionstring}** hello ile daha önce not ettiğiniz değer:</span><span class="sxs-lookup"><span data-stu-id="7027f-137">Add hello following class-level variables toohello **App** class, replacing **{yourhubconnectionstring}** with hello value your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
    ```
[!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

8. <span data-ttu-id="7027f-138">Merhaba Hello imzası değiştirme **ana** yöntemi tooinclude özel durumlar gibi hello:</span><span class="sxs-lookup"><span data-stu-id="7027f-138">Modify hello signature of hello **main** method tooinclude hello exceptions as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```

9. <span data-ttu-id="7027f-139">Merhaba hello gövdesi olarak koddan hello eklemek **ana** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7027f-139">Add hello following code as hello body of hello **main** method.</span></span> <span data-ttu-id="7027f-140">Bu kod, IoT Hub kimlik kayıt defterinizde zaten yoksa *javadevice* adlı bir cihaz oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7027f-140">This code creates a device called *javadevice* in your IoT Hub identity registry if doesn't already exist.</span></span> <span data-ttu-id="7027f-141">Ardından hello cihaz Kimliğini ve daha sonra ihtiyacınız anahtarını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="7027f-141">It then displays hello device ID and key that you need later:</span></span>

    ```java
    RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);
RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);

    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    ```

10. <span data-ttu-id="7027f-142">Merhaba App.java dosyasını kaydedip kapatın.</span><span class="sxs-lookup"><span data-stu-id="7027f-142">Save and close hello App.java file.</span></span>

11. <span data-ttu-id="7027f-143">toobuild hello **create-device-identity** Maven kullanarak uygulama komutu hello hello create-device-identity klasöründeki komut isteminde aşağıdaki hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="7027f-143">toobuild hello **create-device-identity** app using Maven, execute hello following command at hello command prompt in hello create-device-identity folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

12. <span data-ttu-id="7027f-144">toorun hello **create-device-identity** Maven kullanarak uygulama komutu hello hello create-device-identity klasöründeki komut isteminde aşağıdaki hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="7027f-144">toorun hello **create-device-identity** app using Maven, execute hello following command at hello command prompt in hello create-device-identity folder:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

13. <span data-ttu-id="7027f-145">Merhaba Not **cihaz kimliği** ve **aygıt anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="7027f-145">Make a note of hello **Device ID** and **Device key**.</span></span> <span data-ttu-id="7027f-146">TooIoT hub'a bir cihaz olarak bağlanan bir uygulama oluşturduğunuzda, bu değerleri daha sonra gerekir.</span><span class="sxs-lookup"><span data-stu-id="7027f-146">You need these values later when you create an app that connects tooIoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="7027f-147">Merhaba IOT Hub kimlik kayıt defteri, yalnızca cihaz kimlikleri tooenable güvenli erişim toohello IOT hub'ı depolar.</span><span class="sxs-lookup"><span data-stu-id="7027f-147">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="7027f-148">Cihaz kimliklerini ve anahtarlarını toouse güvenlik kimlik bilgileri ve toodisable erişim için tek bir cihaza kullanabilirsiniz bir etkin/devre dışı bayrağını depolar.</span><span class="sxs-lookup"><span data-stu-id="7027f-148">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="7027f-149">Uygulamanızın cihaza özgü diğer meta verileri toostore gerekiyorsa, bir uygulamaya özgü depo kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7027f-149">If your app needs toostore other device-specific metadata, it should use an app-specific store.</span></span> <span data-ttu-id="7027f-150">Daha fazla bilgi için bkz: Merhaba [IOT Hub Geliştirici Kılavuzu][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="7027f-150">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>

## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="7027f-151">Cihazdan buluta iletileri alma</span><span class="sxs-lookup"><span data-stu-id="7027f-151">Receive device-to-cloud messages</span></span>

<span data-ttu-id="7027f-152">Bu bölümde IoT Hub'dan cihaz-bulut iletilerini okuyan bir Java konsol uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="7027f-152">In this section, you create a Java console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="7027f-153">IOT hub'ı kullanıma sunan bir [olay hub'ı][lnk-event-hubs-overview]-uyumlu bir uç noktasını tooenable, tooread cihaz bulut iletilerini.</span><span class="sxs-lookup"><span data-stu-id="7027f-153">An IoT hub exposes an [Event Hub][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="7027f-154">tookeep şeyler basit, Bu öğretici, bir yüksek işleme dağıtımına uygun olmayan temel bir okuyucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7027f-154">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="7027f-155">Merhaba [cihaz-bulut iletileri] [ lnk-process-d2c-tutorial] öğretici gösterir, ölçekli olarak nasıl tooprocess cihaz-bulut iletileri.</span><span class="sxs-lookup"><span data-stu-id="7027f-155">hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how tooprocess device-to-cloud messages at scale.</span></span> <span data-ttu-id="7027f-156">Merhaba [Event Hubs ile çalışmaya başlama] [ lnk-eventhubs-tutorial] Eğitmeni nasıl tooprocess olay hub'larından iletileri ve geçerli toohello IOT Hub ve Event Hub ile uyumlu uç noktalar hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7027f-156">hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how tooprocess messages from Event Hubs and is applicable toohello IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="7027f-157">Merhaba cihaz bulut iletilerini her zaman okumak için Event Hub ile uyumlu uç nokta hello AMQP protokolünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="7027f-157">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>

1. <span data-ttu-id="7027f-158">Merhaba iot-java-get-started klasöründe oluşturduğunuz hello *bir cihaz kimliği oluşturma* bölümünde, adlı bir Maven projesi oluşturun **read-d2c-messages** komutu, komut isteminde aşağıdaki hello kullanarak.</span><span class="sxs-lookup"><span data-stu-id="7027f-158">In hello iot-java-get-started folder you created in hello *Create a device identity* section, create a Maven project called **read-d2c-messages** using hello following command at your command prompt.</span></span> <span data-ttu-id="7027f-159">Bunun tek ve uzun bir komut olduğunu unutmayın:</span><span class="sxs-lookup"><span data-stu-id="7027f-159">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="7027f-160">Komut isteminizde toohello read-d2c-messages klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="7027f-160">At your command prompt, navigate toohello read-d2c-messages folder.</span></span>

3. <span data-ttu-id="7027f-161">Bir metin düzenleyicisi kullanarak hello read-d2c-messages klasörüne hello pom.xml dosyasını açın ve bağımlılık toohello aşağıdaki hello ekleyin **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="7027f-161">Using a text editor, open hello pom.xml file in hello read-d2c-messages folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="7027f-162">Bu bağımlılık toouse hello eventhubs-client paketini, uygulama tooread hello Event Hub ile uyumlu uç noktasından içinde sağlar:</span><span class="sxs-lookup"><span data-stu-id="7027f-162">This dependency enables you toouse hello eventhubs-client package in your app tooread from hello Event Hub-compatible endpoint:</span></span>

    ```xml
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.13.0</version> 
    </dependency>
    ```

4. <span data-ttu-id="7027f-163">Merhaba pom.xml dosyasını kaydedip kapatın.</span><span class="sxs-lookup"><span data-stu-id="7027f-163">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="7027f-164">Bir metin düzenleyicisi kullanarak hello read-d2c-messages\src\main\java\com\mycompany\app\App.java dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="7027f-164">Using a text editor, open hello read-d2c-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="7027f-165">Merhaba aşağıdakileri ekleyin **alma** deyimleri toohello dosyası:</span><span class="sxs-lookup"><span data-stu-id="7027f-165">Add hello following **import** statements toohello file:</span></span>

    ```java
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;
    import com.microsoft.azure.servicebus.*;

    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.function.*;
    ```

7. <span data-ttu-id="7027f-166">Aşağıdaki sınıf düzeyi değişken toohello hello eklemek **uygulama** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="7027f-166">Add hello following class-level variable toohello **App** class.</span></span> <span data-ttu-id="7027f-167">Değiştir **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, ve **{youreventhubcompatiblename}** daha önce not ettiğiniz hello değerlerle:</span><span class="sxs-lookup"><span data-stu-id="7027f-167">Replace **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, and **{youreventhubcompatiblename}** with hello values you noted previously:</span></span>

    ```java
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```

8. <span data-ttu-id="7027f-168">Merhaba aşağıdakileri ekleyin **receiveMessages** yöntemi toohello **uygulama** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="7027f-168">Add hello following **receiveMessages** method toohello **App** class.</span></span> <span data-ttu-id="7027f-169">Bu yöntem oluşturur bir **EventHubClient** örnek tooconnect toohello Event Hub ile uyumlu uç nokta ve zaman uyumsuz olarak oluşturan bir **PartitionReceiver** Event Hub'ındaki örneği tooread bölüm.</span><span class="sxs-lookup"><span data-stu-id="7027f-169">This method creates an **EventHubClient** instance tooconnect toohello Event Hub-compatible endpoint and then asynchronously creates a **PartitionReceiver** instance tooread from an Event Hub partition.</span></span> <span data-ttu-id="7027f-170">Sürekli döngüye girer ve hello uygulama sonlanana kadar hello ileti ayrıntılarını yazdırır.</span><span class="sxs-lookup"><span data-stu-id="7027f-170">It loops continuously and prints hello message details until hello app terminates.</span></span>

    ```java
    // Create a receiver on a partition.
    private static EventHubClient receiveMessages(final String partitionId) {
      EventHubClient client = null;
      try {
        client = EventHubClient.createFromConnectionStringSync(connStr);
      } catch (Exception e) {
        System.out.println("Failed toocreate client: " + e.getMessage());
        System.exit(1);
      }
      try {
        // Create a receiver using the
        // default Event Hubs consumer group
        // that listens for messages from now on.
        client.createReceiver(EventHubClient.DEFAULT_CONSUMER_GROUP_NAME, partitionId, Instant.now())
          .thenAccept(new Consumer<PartitionReceiver>() {
            public void accept(PartitionReceiver receiver) {
              System.out.println("** Created receiver on partition " + partitionId);
              try {
                while (true) {
                  Iterable<EventData> receivedEvents = receiver.receive(100).get();
                  int batchSize = 0;
                  if (receivedEvents != null) {
                    System.out.println("Got some evenst");
                    for (EventData receivedEvent : receivedEvents) {
                      System.out.println(String.format("Offset: %s, SeqNo: %s, EnqueueTime: %s",
                        receivedEvent.getSystemProperties().getOffset(),
                        receivedEvent.getSystemProperties().getSequenceNumber(),
                        receivedEvent.getSystemProperties().getEnqueuedTime()));
                      System.out.println(String.format("| Device ID: %s",
                        receivedEvent.getSystemProperties().get("iothub-connection-device-id")));
                      System.out.println(String.format("| Message Payload: %s",
                        new String(receivedEvent.getBytes(), Charset.defaultCharset())));
                      batchSize++;
                    }
                  }
                  System.out.println(String.format("Partition: %s, ReceivedBatch Size: %s", partitionId, batchSize));
                }
              } catch (Exception e) {
                System.out.println("Failed tooreceive messages: " + e.getMessage());
              }
            }
          });
        } catch (Exception e) {
          System.out.println("Failed toocreate receiver: " + e.getMessage());
      }
      return client;
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="7027f-171">Bu yöntem, böylece Hello alıcı çalışmaya başladıktan sonra hello alıcı yalnızca gönderilen iletileri tooIoT Hub okur hello alıcı oluştururken bir filtre kullanır.</span><span class="sxs-lookup"><span data-stu-id="7027f-171">This method uses a filter when it creates hello receiver so that hello receiver only reads messages sent tooIoT Hub after hello receiver starts running.</span></span> <span data-ttu-id="7027f-172">Merhaba geçerli iletiler kümesini görebileceğiniz için bu tekniği bir test ortamında kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="7027f-172">This technique is useful in a test environment so you can see hello current set of messages.</span></span> <span data-ttu-id="7027f-173">Bir üretim ortamında kodunuzun - daha fazla bilgi için tüm karışılama iletileri işlediğinden emin olmak için bkz hello [nasıl tooprocess IOT Hub cihaz bulut iletilerini] [ lnk-process-d2c-tutorial] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="7027f-173">In a production environment, your code should make sure that it processes all hello messages - for more information, see hello [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

9. <span data-ttu-id="7027f-174">Merhaba Hello imzası değiştirme **ana** yöntemi tooinclude özel durumu aşağıdaki gibi hello:</span><span class="sxs-lookup"><span data-stu-id="7027f-174">Modify hello signature of hello **main** method tooinclude hello exception as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

10. <span data-ttu-id="7027f-175">Aşağıdaki kodu toohello hello eklemek **ana** hello yönteminde **uygulama** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="7027f-175">Add hello following code toohello **main** method in hello **App** class.</span></span> <span data-ttu-id="7027f-176">Bu kod hello iki oluşturur **EventHubClient** ve **PartitionReceiver** örnekleri ve iletilerini işleme bittiğinde tooclose hello uygulama sağlar:</span><span class="sxs-lookup"><span data-stu-id="7027f-176">This code creates hello two **EventHubClient** and **PartitionReceiver** instances and enables you tooclose hello app when you have finished processing messages:</span></span>

    ```java
    // Create receivers for partitions 0 and 1.
    EventHubClient client0 = receiveMessages("0");
    EventHubClient client1 = receiveMessages("1");
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    try {
      client0.closeSync();
      client1.closeSync();
      System.exit(0);
    } catch (ServiceBusException sbe) {
      System.exit(1);
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="7027f-177">Bu kod, IOT hub'ınızı hello F1 (ücretsiz) katmanında oluşturduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="7027f-177">This code assumes you created your IoT hub in hello F1 (free) tier.</span></span> <span data-ttu-id="7027f-178">Ücretsiz IoT hub'ının "0" ve "1" adlı iki bölümü vardır.</span><span class="sxs-lookup"><span data-stu-id="7027f-178">A free IoT hub has two partitions named "0" and "1".</span></span>

11. <span data-ttu-id="7027f-179">Merhaba App.java dosyasını kaydedip kapatın.</span><span class="sxs-lookup"><span data-stu-id="7027f-179">Save and close hello App.java file.</span></span>

12. <span data-ttu-id="7027f-180">toobuild hello **read-d2c-messages** Maven kullanarak uygulama komutu hello hello read-d2c-messages klasöründeki komut isteminde aşağıdaki hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="7027f-180">toobuild hello **read-d2c-messages** app using Maven, execute hello following command at hello command prompt in hello read-d2c-messages folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="create-a-device-app"></a><span data-ttu-id="7027f-181">Cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="7027f-181">Create a device app</span></span>
<span data-ttu-id="7027f-182">Bu bölümde, tooan IOT hub'ı cihaz-bulut iletileri gönderen bir cihaza benzetim yapan bir Java konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7027f-182">In this section, you create a Java console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="7027f-183">Merhaba iot-java-get-started klasöründe oluşturduğunuz hello *bir cihaz kimliği oluşturma* bölümünde, adlı bir Maven projesi oluşturun **simulated-device** komutu, komut isteminde aşağıdaki hello kullanarak.</span><span class="sxs-lookup"><span data-stu-id="7027f-183">In hello iot-java-get-started folder you created in hello *Create a device identity* section, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="7027f-184">Bunun tek ve uzun bir komut olduğunu unutmayın:</span><span class="sxs-lookup"><span data-stu-id="7027f-184">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="7027f-185">Komut isteminizde toohello simulated-device klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="7027f-185">At your command prompt, navigate toohello simulated-device folder.</span></span>

3. <span data-ttu-id="7027f-186">Bir metin düzenleyicisi kullanarak, hello simulated-device klasöründeki hello pom.xml dosyasını açın ve aşağıdaki bağımlılıkları toohello hello ekleyin **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="7027f-186">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="7027f-187">Bu bağımlılık, toouse hello iothub-java-client paketinde, uygulama toocommunicate IOT hub ve Java nesnelerini tooJSON tooserialize sağlar:</span><span class="sxs-lookup"><span data-stu-id="7027f-187">This dependency enables you toouse hello iothub-java-client package in your app toocommunicate with your IoT hub and tooserialize Java objects tooJSON:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    <dependency>
      <groupId>com.google.code.gson</groupId>
      <artifactId>gson</artifactId>
      <version>2.3.1</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="7027f-188">Hello için en son sürümünü denetleyebilir **IOT cihaz istemci** kullanarak [Maven arama][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="7027f-188">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

4. <span data-ttu-id="7027f-189">Merhaba pom.xml dosyasını kaydedip kapatın.</span><span class="sxs-lookup"><span data-stu-id="7027f-189">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="7027f-190">Bir metin düzenleyicisi kullanarak hello simulated-device\src\main\java\com\mycompany\app\App.java dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="7027f-190">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="7027f-191">Merhaba aşağıdakileri ekleyin **alma** deyimleri toohello dosyası:</span><span class="sxs-lookup"><span data-stu-id="7027f-191">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.google.gson.Gson;

    import java.io.*;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

7. <span data-ttu-id="7027f-192">Aşağıdaki sınıf düzeyi değişkenleri toohello hello eklemek **uygulama** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="7027f-192">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="7027f-193">Değiştirme **{youriothubname}** , IOT hub'ı adıyla ve **{yourdevicekey}** hello oluşturulan hello aygıt anahtarı değerine sahip *bir cihaz kimliği oluşturma* bölümü:</span><span class="sxs-lookup"><span data-stu-id="7027f-193">Replacing **{youriothubname}** with your IoT hub name, and **{yourdevicekey}** with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    <span data-ttu-id="7027f-194">Bu örnek uygulama hello kullanan **Protokolü** değişkenini bir **DeviceClient** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="7027f-194">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="7027f-195">IOT Hub ile ya da hello MQTT, AMQP veya HTTP protokolü toocommunicate kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7027f-195">You can use either hello MQTT, AMQP, or HTTP protocol toocommunicate with IoT Hub.</span></span>

8. <span data-ttu-id="7027f-196">Ekleme hello aşağıdaki iç içe geçmiş **TelemetryDataPoint** hello sınıfında **uygulama** sınıf toospecify hello telemetri verilerini Cihazınızı tooyour IOT hub'ı gönderir:</span><span class="sxs-lookup"><span data-stu-id="7027f-196">Add hello following nested **TelemetryDataPoint** class inside hello **App** class toospecify hello telemetry data your device sends tooyour IoT hub:</span></span>

    ```java
    private static class TelemetryDataPoint {
      public String deviceId;
      public double temperature;
      public double humidity;
   
      public String serialize() {
        Gson gson = new Gson();
        return gson.toJson(this);
      }
    }
    ```
9. <span data-ttu-id="7027f-197">Ekleme hello aşağıdaki iç içe geçmiş **EventCallback** hello sınıfında **uygulama** hello aygıt uygulamadan bir ileti işlediğinde IOT hub'ı hello sınıfı toodisplay hello onay durumunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="7027f-197">Add hello following nested **EventCallback** class inside hello **App** class toodisplay hello acknowledgement status that hello IoT hub returns when it processes a message from hello device app.</span></span> <span data-ttu-id="7027f-198">Merhaba ileti işlendiğinde bu yöntem aynı zamanda hello hello uygulamadaki ana iş parçacığı bildirir:</span><span class="sxs-lookup"><span data-stu-id="7027f-198">This method also notifies hello main thread in hello app when hello message has been processed:</span></span>
   
    ```java
    private static class EventCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toomessage with status: " + status.name());
   
        if (context != null) {
          synchronized (context) {
            context.notify();
          }
        }
      }
    }
    ```

10. <span data-ttu-id="7027f-199">Ekleme hello aşağıdaki iç içe geçmiş **MessageSender** hello sınıfında **uygulama** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="7027f-199">Add hello following nested **MessageSender** class inside hello **App** class.</span></span> <span data-ttu-id="7027f-200">Merhaba **çalıştırmak** bu sınıftaki yöntemi örnek telemetri verileri toosend tooyour IOT hub'ı oluşturur ve hello sonraki iletiyi göndermeden önce onay bekler:</span><span class="sxs-lookup"><span data-stu-id="7027f-200">hello **run** method in this class generates sample telemetry data toosend tooyour IoT hub and waits for an acknowledgement before sending hello next message:</span></span>

    ```java
    private static class MessageSender implements Runnable {
      public void run()  {
        try {
          double minTemperature = 20;
          double minHumidity = 60;
          Random rand = new Random();
    
          while (true) {
            double currentTemperature = minTemperature + rand.nextDouble() * 15;
            double currentHumidity = minHumidity + rand.nextDouble() * 20;
            TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
            telemetryDataPoint.deviceId = deviceId;
            telemetryDataPoint.temperature = currentTemperature;
            telemetryDataPoint.humidity = currentHumidity;
    
            String msgStr = telemetryDataPoint.serialize();
            Message msg = new Message(msgStr);
            msg.setProperty("temperatureAlert", (currentTemperature > 30) ? "true" : "false");
            msg.setMessageId(java.util.UUID.randomUUID().toString()); 
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

    <span data-ttu-id="7027f-201">Bu yöntem bir hello IOT hub'ı hello önceki iletiyi onayladıktan bir saniye sonra yeni bir cihaz bulut iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="7027f-201">This method sends a new device-to-cloud message one second after hello IoT hub acknowledges hello previous message.</span></span> <span data-ttu-id="7027f-202">Selamlama iletisine JSON serileştirilmiş nesne hello DeviceID içeren ve rastgele sayılar toosimulate sıcaklık algılayıcısı ve nem algılayıcı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7027f-202">hello message contains a JSON-serialized object with hello deviceId and randomly generated numbers toosimulate a temperature sensor, and a humidity sensor.</span></span>

11. <span data-ttu-id="7027f-203">Hello yerine **ana** yöntemi ile bir iş parçacığı toosend cihaz bulut iletilerini tooyour IOT hub'ı oluşturan koddan hello:</span><span class="sxs-lookup"><span data-stu-id="7027f-203">Replace hello **main** method with hello following code that creates a thread toosend device-to-cloud messages tooyour IoT hub:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException {
      client = new DeviceClient(connString, protocol);
      client.open();
    
      MessageSender sender = new MessageSender();
    
      ExecutorService executor = Executors.newFixedThreadPool(1);
      executor.execute(sender);
    
      System.out.println("Press ENTER tooexit.");
      System.in.read();
      executor.shutdownNow();
      client.closeNow();
    }
    ```

12. <span data-ttu-id="7027f-204">Merhaba App.java dosyasını kaydedip kapatın.</span><span class="sxs-lookup"><span data-stu-id="7027f-204">Save and close hello App.java file.</span></span>

13. <span data-ttu-id="7027f-205">toobuild hello **simulated-device** Maven kullanarak uygulama komutu hello hello simulated-device klasöründeki komut isteminde aşağıdaki hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="7027f-205">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

> [!NOTE]
> <span data-ttu-id="7027f-206">tookeep şeyler basit, Bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="7027f-206">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="7027f-207">Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="7027f-207">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="7027f-208">Merhaba uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7027f-208">Run hello apps</span></span>

<span data-ttu-id="7027f-209">Hazır toorun hello uygulamaları sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="7027f-209">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="7027f-210">Hello read-d2c klasöründeki bir komut isteminde IOT hub'ınızı hello ilk bölümü izlemeye komutu toobegin aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7027f-210">At a command prompt in hello read-d2c folder, run hello following command toobegin monitoring hello first partition in your IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Java IOT Hub hizmeti uygulama toomonitor cihaz-bulut iletileri][7]

2. <span data-ttu-id="7027f-212">Telemetri veri tooyour IOT hub'ı gönderme komutu toobegin aşağıdaki hello hello simulated-device klasöründeki komut isteminde çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7027f-212">At a command prompt in hello simulated-device folder, run hello following command toobegin sending telemetry data tooyour IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Java IOT Hub cihaz uygulaması toosend cihaz bulut iletilerini][8]

3. <span data-ttu-id="7027f-214">Merhaba **kullanım** döşeme hello [Azure portal] [ lnk-portal] gösterir hello gönderilen iletileri toohello IOT hub'ı sayısı:</span><span class="sxs-lookup"><span data-stu-id="7027f-214">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>

    ![Azure portalı kullanım kutucuğu sayısını gösteren gönderilen iletileri tooIoT Hub][43]

## <a name="next-steps"></a><span data-ttu-id="7027f-216">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7027f-216">Next steps</span></span>
<span data-ttu-id="7027f-217">Bu öğreticide hello Azure portalında yeni bir IOT hub yapılandırılmış ve ardından hello IOT hub'ın kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="7027f-217">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="7027f-218">Bu cihaz kimliğini tooenable hello cihaz uygulama toosend cihaz bulut iletilerini toohello IOT hub kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7027f-218">You used this device identity tooenable hello device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="7027f-219">Merhaba hello IOT hub tarafından alınan iletileri görüntüleyen bir uygulama da oluşturmuş.</span><span class="sxs-lookup"><span data-stu-id="7027f-219">You also created an app that displays hello messages received by hello IoT hub.</span></span>

<span data-ttu-id="7027f-220">Başlarken toocontinue IOT Hub ve tooexplore diğer IOT senaryolarını bakın:</span><span class="sxs-lookup"><span data-stu-id="7027f-220">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="7027f-221">[Cihazınızı bağlama][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="7027f-221">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="7027f-222">[Cihaz yönetimini kullanmaya başlama][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="7027f-222">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="7027f-223">[Azure IoT Edge’i kullanmaya başlama][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="7027f-223">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="7027f-224">toolearn tooextend, IOT çözümü ve işlem cihaz bulut iletilerini ölçekli olarak nasıl görürüm hello [cihaz-bulut iletileri] [ lnk-process-d2c-tutorial] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="7027f-224">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[6]: ./media/iot-hub-java-java-getstarted/create-iot-hub6.png
[7]: ./media/iot-hub-java-java-getstarted/runapp1.png
[8]: ./media/iot-hub-java-java-getstarted/runapp2.png
[43]: ./media/iot-hub-java-java-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-eventhubs-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22
