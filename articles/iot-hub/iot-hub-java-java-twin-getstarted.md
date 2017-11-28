---
title: "aaaGet başlatılan Azure IOT Hub cihaz çiftlerini (Java) | Microsoft Docs"
description: "Nasıl toouse Azure IOT Hub cihaz çiftlerini tooadd etiketleri ve IOT Hub sorgusuyla kullanın. Hello Azure IOT cihaz SDK Java tooimplement hello cihaz uygulamasının ve Java tooimplement hello etiketleri ekler ve hello IOT hub'ı sorgu çalışan bir hizmet uygulaması için Azure IOT hizmeti SDK'sını hello için kullanın."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/04/2017
ms.author: dobett
ms.openlocfilehash: 25f6fc81471d59c62bcdc3766bb5c33f5733c930
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-java"></a><span data-ttu-id="2654c-104">Cihaz çiftlerini (Java) ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="2654c-104">Get started with device twins (Java)</span></span>

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="2654c-105">Bu öğreticide, iki Java konsol uygulamaları oluşturun:</span><span class="sxs-lookup"><span data-stu-id="2654c-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="2654c-106">**ekleme-etiketleri-query**, etiketleri ekler ve cihaz çiftlerini sorgular bir Java arka uç uygulaması.</span><span class="sxs-lookup"><span data-stu-id="2654c-106">**add-tags-query**, a Java back-end app that adds tags and queries device twins.</span></span>
* <span data-ttu-id="2654c-107">**simulated-device**, bir Java cihaz uygulaması, bildirilen bir özellik kullanarak kendi bağlantı koşulunun tooyour IOT hub ve raporları bağlanır.</span><span class="sxs-lookup"><span data-stu-id="2654c-107">**simulated-device**, a Java device app that that connects tooyour IoT hub and reports its connectivity condition using a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="2654c-108">Merhaba makale [Azure IOT SDK'ları](iot-hub-devguide-sdks.md) toobuild kullanabileceğiniz hello Azure IOT SDK'ları hakkında bilgi sağlayan cihaz ve arka uç uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="2654c-108">hello article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>

<span data-ttu-id="2654c-109">toocomplete Bu öğretici, gerekir:</span><span class="sxs-lookup"><span data-stu-id="2654c-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="2654c-110">Merhaba son [Java SE Geliştirme Seti 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="2654c-110">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="2654c-111">Maven 3</span><span class="sxs-lookup"><span data-stu-id="2654c-111">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="2654c-112">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="2654c-112">An active Azure account.</span></span> <span data-ttu-id="2654c-113">(Bir hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz bir hesap](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.)</span><span class="sxs-lookup"><span data-stu-id="2654c-113">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="2654c-114">Program aracılığıyla toocreate hello cihaz kimliği tercih ederseniz, hello hello ilgili bölümünü okuyun [Java kullanarak aygıt tooyour IOT hub'ınıza bağlanmak](iot-hub-java-java-getstarted.md#create-a-device-identity) makalesi.</span><span class="sxs-lookup"><span data-stu-id="2654c-114">If you prefer toocreate hello device identity programmatically, read hello corresponding section in hello [Connect your device tooyour IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="2654c-115">Merhaba service uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="2654c-115">Create hello service app</span></span>

<span data-ttu-id="2654c-116">Bu bölümde IOT Hub'ındaki etiketi toohello cihaz çifti ile ilişkili olarak, konum meta veri ekleyen bir Java uygulaması oluşturma **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="2654c-116">In this section, you create a Java app that adds location metadata as a tag toohello device twin in IoT Hub associated with **myDeviceId**.</span></span> <span data-ttu-id="2654c-117">Merhaba uygulama ilk IOT hub'ın hello ABD bulunan aygıtları ve ardından bir cep telefonu ağ bağlantısı rapor cihazlar için sorgular.</span><span class="sxs-lookup"><span data-stu-id="2654c-117">hello app first queries IoT hub for devices located in hello US, and then for devices that report a cellular network connection.</span></span>

1. <span data-ttu-id="2654c-118">Geliştirme makinenizde adlı boş bir klasör oluşturun `iot-java-twin-getstarted`.</span><span class="sxs-lookup"><span data-stu-id="2654c-118">On your development machine, create an empty folder called `iot-java-twin-getstarted`.</span></span>

1. <span data-ttu-id="2654c-119">Merhaba, `iot-java-twin-getstarted` klasörünü adlı bir Maven projesi oluşturun **ekleme-etiketleri-query** komutu, komut isteminde aşağıdaki hello kullanarak.</span><span class="sxs-lookup"><span data-stu-id="2654c-119">In hello `iot-java-twin-getstarted` folder, create a Maven project called **add-tags-query** using hello following command at your command prompt.</span></span> <span data-ttu-id="2654c-120">Bunun tek ve uzun bir komut olduğunu unutmayın:</span><span class="sxs-lookup"><span data-stu-id="2654c-120">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="2654c-121">Komut isteminizde toohello gidin `add-tags-query` klasör.</span><span class="sxs-lookup"><span data-stu-id="2654c-121">At your command prompt, navigate toohello `add-tags-query` folder.</span></span>

1. <span data-ttu-id="2654c-122">Bir metin düzenleyicisi kullanarak hello açın `pom.xml` hello dosyasında `add-tags-query` klasörü ve bağımlılık toohello aşağıdaki hello ekleyin **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="2654c-122">Using a text editor, open hello `pom.xml` file in hello `add-tags-query` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="2654c-123">Bu bağımlılık toouse hello etkinleştirir **IOT hizmeti istemcisi** , uygulama toocommunicate IOT hub'ınızı ile paketinde:</span><span class="sxs-lookup"><span data-stu-id="2654c-123">This dependency enables you toouse hello **iot-service-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="2654c-124">Hello için en son sürümünü denetleyebilir **IOT hizmeti istemcisi** kullanarak [Maven arama](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="2654c-124">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="2654c-125">Merhaba aşağıdakileri ekleyin **yapı** düğümünden hello sonraki **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="2654c-125">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="2654c-126">Bu yapılandırma, Maven toouse Java 1.8 toobuild hello uygulaması bildirir:</span><span class="sxs-lookup"><span data-stu-id="2654c-126">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. <span data-ttu-id="2654c-127">Kaydet ve Kapat hello `pom.xml` dosya.</span><span class="sxs-lookup"><span data-stu-id="2654c-127">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="2654c-128">Bir metin düzenleyicisi kullanarak hello açın `add-tags-query\src\main\java\com\mycompany\app\App.java` dosya.</span><span class="sxs-lookup"><span data-stu-id="2654c-128">Using a text editor, open hello `add-tags-query\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="2654c-129">Merhaba aşağıdakileri ekleyin **alma** deyimleri toohello dosyası:</span><span class="sxs-lookup"><span data-stu-id="2654c-129">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. <span data-ttu-id="2654c-130">Aşağıdaki sınıf düzeyi değişkenleri toohello hello eklemek **uygulama** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="2654c-130">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="2654c-131">Değiştir `{youriothubconnectionstring}` hello ettiğiniz, IOT hub bağlantı dizesine sahip *IOT Hub oluşturma* bölümü:</span><span class="sxs-lookup"><span data-stu-id="2654c-131">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. <span data-ttu-id="2654c-132">Güncelleştirme hello **ana** yöntemi imza tooinclude hello aşağıdaki `throws` yan tümcesi:</span><span class="sxs-lookup"><span data-stu-id="2654c-132">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. <span data-ttu-id="2654c-133">Aşağıdaki kodu toohello hello eklemek **ana** yöntemi toocreate hello **DeviceTwin** ve **DeviceTwinDevice** nesneleri.</span><span class="sxs-lookup"><span data-stu-id="2654c-133">Add hello following code toohello **main** method toocreate hello **DeviceTwin** and **DeviceTwinDevice** objects.</span></span> <span data-ttu-id="2654c-134">Merhaba **DeviceTwin** nesne IOT hub'ınızı ile Merhaba iletişim işler.</span><span class="sxs-lookup"><span data-stu-id="2654c-134">hello **DeviceTwin** object handles hello communication with your IoT hub.</span></span> <span data-ttu-id="2654c-135">Merhaba **DeviceTwinDevice** nesne özelliklerini ve etiketler ile Merhaba cihaz çifti temsil eder:</span><span class="sxs-lookup"><span data-stu-id="2654c-135">hello **DeviceTwinDevice** object represents hello device twin with its properties and tags:</span></span>

    ```java
    // Get hello DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. <span data-ttu-id="2654c-136">Merhaba aşağıdakileri ekleyin `try/catch` toohello engelleme **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="2654c-136">Add hello following `try/catch` block toohello **main** method:</span></span>

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. <span data-ttu-id="2654c-137">tooupdate hello **bölge** ve **tesis** cihaz çifti etiketler, cihaz çiftine ekleme hello kodda aşağıdaki hello `try` engelle:</span><span class="sxs-lookup"><span data-stu-id="2654c-137">tooupdate hello **region** and **plant** device twin tags in your device twin, add hello following code in hello `try` block:</span></span>

    ```java
    // Get hello device twin from IoT Hub
    System.out.println("Device twin before update:");
    twinClient.getTwin(device);
    System.out.println(device);

    // Update device twin tags if they are different
    // from hello existing values
    String currentTags = device.tagsToString();
    if ((!currentTags.contains("region=" + region) && !currentTags.contains("plant=" + plant))) {
      // Create hello tags and attach them toohello DeviceTwinDevice object
      Set<Pair> tags = new HashSet<Pair>();
      tags.add(new Pair("region", region));
      tags.add(new Pair("plant", plant));
      device.setTags(tags);

      // Update hello device twin in IoT Hub
      System.out.println("Updating device twin");
      twinClient.updateTwin(device);
    }

    // Retrieve hello device twin with hello tag values from IoT Hub
    System.out.println("Device twin after update:");
    twinClient.getTwin(device);
    System.out.println(device);
    ```

1. <span data-ttu-id="2654c-138">tooquery hello cihaz çiftlerini IOT hub'ındaki ekleme kodu toohello aşağıdaki hello `try` hello önceki adımda eklediğiniz kodun hello bloğu.</span><span class="sxs-lookup"><span data-stu-id="2654c-138">tooquery hello device twins in IoT hub, add hello following code toohello `try` block after hello code you added in hello previous step.</span></span> <span data-ttu-id="2654c-139">Merhaba kod iki sorguları çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="2654c-139">hello code runs two queries.</span></span> <span data-ttu-id="2654c-140">Her sorgu en fazla 100 cihazları döndürür:</span><span class="sxs-lookup"><span data-stu-id="2654c-140">Each query returns a maximum of 100 devices:</span></span>

    ```java
    // Query hello device twins in IoT Hub
    System.out.println("Devices in Redmond:");

    // Construct hello query
    SqlQuery sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43'", null);

    // Run hello query, returning a maximum of 100 devices
    Query twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 100);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }

    System.out.println("Devices in Redmond using a cellular network:");

    // Construct hello query
    sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43' AND properties.reported.connectivityType = 'cellular'", null);

    // Run hello query, returning a maximum of 100 devices
    twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 3);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }
    ```

1. <span data-ttu-id="2654c-141">Kaydet ve Kapat hello `add-tags-query\src\main\java\com\mycompany\app\App.java` dosyası</span><span class="sxs-lookup"><span data-stu-id="2654c-141">Save and close hello `add-tags-query\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="2654c-142">Merhaba yapı **ekleme-etiketleri-query** uygulama ve olan hataları düzeltin.</span><span class="sxs-lookup"><span data-stu-id="2654c-142">Build hello **add-tags-query** app and correct any errors.</span></span> <span data-ttu-id="2654c-143">Komut isteminizde toohello gidin `add-tags-query` klasörü ve aşağıdaki komutu çalıştırın hello:</span><span class="sxs-lookup"><span data-stu-id="2654c-143">At your command prompt, navigate toohello `add-tags-query` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="2654c-144">Cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="2654c-144">Create a device app</span></span>

<span data-ttu-id="2654c-145">Bu bölümde, tooIoT Hub gönderilen bir bildirilen özelliği değerini ayarlayan bir Java konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2654c-145">In this section, you create a Java console app that sets a reported property value that is sent tooIoT Hub.</span></span>

1. <span data-ttu-id="2654c-146">Merhaba, `iot-java-twin-getstarted` klasörünü adlı bir Maven projesi oluşturun **simulated-device** komutu, komut isteminde aşağıdaki hello kullanarak.</span><span class="sxs-lookup"><span data-stu-id="2654c-146">In hello `iot-java-twin-getstarted` folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="2654c-147">Bunun tek ve uzun bir komut olduğunu unutmayın:</span><span class="sxs-lookup"><span data-stu-id="2654c-147">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="2654c-148">Komut isteminizde toohello gidin `simulated-device` klasör.</span><span class="sxs-lookup"><span data-stu-id="2654c-148">At your command prompt, navigate toohello `simulated-device` folder.</span></span>

1. <span data-ttu-id="2654c-149">Bir metin düzenleyicisi kullanarak hello açın `pom.xml` hello dosyasında `simulated-device` klasörü ve bağımlılıkları toohello aşağıdaki hello ekleyin **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="2654c-149">Using a text editor, open hello `pom.xml` file in hello `simulated-device` folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="2654c-150">Bu bağımlılık toouse hello etkinleştirir **IOT cihaz istemci** , uygulama toocommunicate IOT hub'ınızı ile paketinde:</span><span class="sxs-lookup"><span data-stu-id="2654c-150">This dependency enables you toouse hello **iot-device-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="2654c-151">Hello için en son sürümünü denetleyebilir **IOT cihaz istemci** kullanarak [Maven arama](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="2654c-151">You can check for hello latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="2654c-152">Merhaba aşağıdakileri ekleyin **yapı** düğümünden hello sonraki **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="2654c-152">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="2654c-153">Bu yapılandırma, Maven toouse Java 1.8 toobuild hello uygulaması bildirir:</span><span class="sxs-lookup"><span data-stu-id="2654c-153">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. <span data-ttu-id="2654c-154">Kaydet ve Kapat hello `pom.xml` dosya.</span><span class="sxs-lookup"><span data-stu-id="2654c-154">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="2654c-155">Bir metin düzenleyicisi kullanarak hello açın `simulated-device\src\main\java\com\mycompany\app\App.java` dosya.</span><span class="sxs-lookup"><span data-stu-id="2654c-155">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="2654c-156">Merhaba aşağıdakileri ekleyin **alma** deyimleri toohello dosyası:</span><span class="sxs-lookup"><span data-stu-id="2654c-156">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="2654c-157">Aşağıdaki sınıf düzeyi değişkenleri toohello hello eklemek **uygulama** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="2654c-157">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="2654c-158">Değiştirme `{youriothubname}` , IOT hub'ı adıyla ve `{yourdevicekey}` hello oluşturulan hello aygıt anahtarı değerine sahip *bir cihaz kimliği oluşturma* bölümü:</span><span class="sxs-lookup"><span data-stu-id="2654c-158">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    ```

    <span data-ttu-id="2654c-159">Bu örnek uygulama hello kullanan **Protokolü** değişkenini bir **DeviceClient** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="2654c-159">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="2654c-160">Merhaba MQTT protokol kullanmanız gereken şu anda toouse cihaz çifti özellikleri.</span><span class="sxs-lookup"><span data-stu-id="2654c-160">Currently, toouse device twin features you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="2654c-161">Aşağıdaki kodu toohello hello eklemek **ana** yöntemi için:</span><span class="sxs-lookup"><span data-stu-id="2654c-161">Add hello following code toohello **main** method to:</span></span>
    * <span data-ttu-id="2654c-162">Aygıt istemci toocommunicate IOT Hub ile oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2654c-162">Create a device client toocommunicate with IoT Hub.</span></span>
    * <span data-ttu-id="2654c-163">Oluşturma bir **aygıt** nesne toostore hello cihaz çifti özellikleri.</span><span class="sxs-lookup"><span data-stu-id="2654c-163">Create a **Device** object toostore hello device twin properties.</span></span>

    ```java
    DeviceClient client = new DeviceClient(connString, protocol);

    // Create a Device object toostore hello device twin properties
    Device dataCollector = new Device() {
      // Print details when a property value changes
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context) {
        System.out.println(propertyKey + " changed too" + propertyValue);
      }
    };
    ```

1. <span data-ttu-id="2654c-164">Aşağıdaki kodu toohello hello eklemek **ana** yöntemi toocreate bir **connectivityType** özelliği bildirilen ve tooIoT Hub gönderin:</span><span class="sxs-lookup"><span data-stu-id="2654c-164">Add hello following code toohello **main** method toocreate a **connectivityType** reported property and send it tooIoT Hub:</span></span>

    ```java
    try {
      // Open hello DeviceClient and start hello device twin services.
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);

      // Create a reported property and send it tooyour IoT hub.
      dataCollector.setReportedProp(new Property("connectivityType", "cellular"));
      client.sendReportedProperties(dataCollector.getReportedProp());
    }
    catch (Exception e) {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="2654c-165">Kod toohello hello sonuna aşağıdaki hello eklemek **ana** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="2654c-165">Add hello following code toohello end of hello **main** method.</span></span> <span data-ttu-id="2654c-166">Merhaba bekleyen **Enter** anahtar IOT hub'ı tooreport hello hello aygıt çifti işlemleri durumunu süredir sağlar:</span><span class="sxs-lookup"><span data-stu-id="2654c-166">Waiting for hello **Enter** key allows time for IoT Hub tooreport hello status of hello device twin operations:</span></span>

    ```java
    System.out.println("Press any key tooexit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. <span data-ttu-id="2654c-167">Kaydet ve Kapat hello `simulated-device\src\main\java\com\mycompany\app\App.java` dosya.</span><span class="sxs-lookup"><span data-stu-id="2654c-167">Save and close hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="2654c-168">Merhaba yapı **simulated-device** uygulama ve olan hataları düzeltin.</span><span class="sxs-lookup"><span data-stu-id="2654c-168">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="2654c-169">Komut isteminizde toohello gidin `simulated-device` klasörü ve aşağıdaki komutu çalıştırın hello:</span><span class="sxs-lookup"><span data-stu-id="2654c-169">At your command prompt, navigate toohello `simulated-device` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="2654c-170">Merhaba uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="2654c-170">Run hello apps</span></span>

<span data-ttu-id="2654c-171">Hazır toorun hello konsol uygulamaları sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="2654c-171">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="2654c-172">Bir komut isteminde hello `add-tags-query` klasörüne komutu toorun hello aşağıdaki Merhaba, **ekleme-etiketleri-query** service uygulaması:</span><span class="sxs-lookup"><span data-stu-id="2654c-172">At a command prompt in hello `add-tags-query` folder, run hello following command toorun hello **add-tags-query** service app:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IOT Hub hizmeti uygulama tooupdate değerleri etiketi ve cihaz sorguları çalıştırma](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    <span data-ttu-id="2654c-174">Merhaba görebilirsiniz **tesis** ve **bölge** etiketleri toohello cihaz çifti eklendi.</span><span class="sxs-lookup"><span data-stu-id="2654c-174">You can see hello **plant** and **region** tags added toohello device twin.</span></span> <span data-ttu-id="2654c-175">Cihazınızı Hello ilk sorgunun döndürdüğü ancak hello ikinci desteklemez.</span><span class="sxs-lookup"><span data-stu-id="2654c-175">hello first query returns your device, but hello second does not.</span></span>

1. <span data-ttu-id="2654c-176">Bir komut isteminde hello `simulated-device` klasörüne komutu tooadd hello aşağıdaki Merhaba, **connectivityType** özelliği toohello cihaz çifti bildirdi:</span><span class="sxs-lookup"><span data-stu-id="2654c-176">At a command prompt in hello `simulated-device` folder, run hello following command tooadd hello **connectivityType** reported property toohello device twin:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Merhaba aygıt istemci ekler hello ** connectivityType ** bildirilen özelliği](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. <span data-ttu-id="2654c-178">Bir komut isteminde hello `add-tags-query` komutu toorun hello aşağıdaki hello Çalıştır klasörü **ekleme-etiketleri-query** service uygulaması ikinci kez:</span><span class="sxs-lookup"><span data-stu-id="2654c-178">At a command prompt in hello `add-tags-query` folder, run hello following command toorun hello **add-tags-query** service app a second time:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IOT Hub hizmeti uygulama tooupdate değerleri etiketi ve cihaz sorguları çalıştırma](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    <span data-ttu-id="2654c-180">Cihazınızı hello gönderdi artık **connectivityType** özelliği tooIoT Hub'ı hello ikinci sorguyu Cihazınızı döndürür.</span><span class="sxs-lookup"><span data-stu-id="2654c-180">Now your device has sent hello **connectivityType** property tooIoT Hub, hello second query returns your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2654c-181">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2654c-181">Next steps</span></span>

<span data-ttu-id="2654c-182">Bu öğreticide hello Azure portalında yeni bir IOT hub yapılandırılmış ve ardından hello IOT hub'ın kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="2654c-182">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="2654c-183">Cihaz meta verilerini bir arka uç uygulamadan etiketler eklendi ve bir cihaz uygulama tooreport aygıt bağlantı bilgilerini hello cihaz çiftine yazıldı.</span><span class="sxs-lookup"><span data-stu-id="2654c-183">You added device metadata as tags from a back-end app, and wrote a device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="2654c-184">Ayrıca, nasıl tooquery hello hello SQL benzeri IOT hub'ı sorgu dili kullanarak cihaz çifti bilgileri öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="2654c-184">You also learned how tooquery hello device twin information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="2654c-185">Kaynakları toolearn nasıl aşağıdaki kullanım hello için:</span><span class="sxs-lookup"><span data-stu-id="2654c-185">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="2654c-186">Merhaba aygıtlarla telemetri gönderen [IOT Hub ile çalışmaya başlama](iot-hub-java-java-getstarted.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="2654c-186">Send telemetry from devices with hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="2654c-187">Merhaba ile etkileşimli olarak (örneğin, kullanıcı tarafından denetlenen bir uygulamadan fan etkinleştirdikten) cihazları denetleme [doğrudan yöntemleri kullanın](iot-hub-java-java-direct-methods.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="2654c-187">Control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
