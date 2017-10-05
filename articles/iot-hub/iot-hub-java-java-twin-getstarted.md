---
title: "Azure IOT Hub cihaz çiftlerini (Java) ile çalışmaya başlama | Microsoft Docs"
description: "Azure IOT Hub cihaz çiftlerini etiket ekleyebilir ve IOT Hub sorgusuyla kullanmak için nasıl kullanılacağını. Cihaz uygulaması ve Azure IOT hizmeti etiketleri ekler ve IOT hub'ı sorgu çalışan bir hizmet uygulaması uygulamak için Java SDK'sını uygulamak için Azure IOT cihaz SDK'sı Java için kullanın."
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
ms.openlocfilehash: 583cfcb9442c7be0a41aa1bc0f743bf8cf863665
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-device-twins-java"></a><span data-ttu-id="ea9da-104">Cihaz çiftlerini (Java) ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ea9da-104">Get started with device twins (Java)</span></span>

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="ea9da-105">Bu öğreticide, iki Java konsol uygulamaları oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ea9da-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="ea9da-106">**ekleme-etiketleri-query**, etiketleri ekler ve cihaz çiftlerini sorgular bir Java arka uç uygulaması.</span><span class="sxs-lookup"><span data-stu-id="ea9da-106">**add-tags-query**, a Java back-end app that adds tags and queries device twins.</span></span>
* <span data-ttu-id="ea9da-107">**simulated-device**, IOT hub'ınızı bağlayan ve bağlantısını raporları bildirilen bir özellik kullanarak koşul bir Java cihaz uygulaması.</span><span class="sxs-lookup"><span data-stu-id="ea9da-107">**simulated-device**, a Java device app that that connects to your IoT hub and reports its connectivity condition using a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="ea9da-108">Makaleyi [Azure IOT SDK'ları](iot-hub-devguide-sdks.md) hem cihaz hem de arka uç uygulamalar oluşturmak için kullanabileceğiniz Azure IOT SDK'ları hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ea9da-108">The article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>

<span data-ttu-id="ea9da-109">Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="ea9da-109">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="ea9da-110">En güncel [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="ea9da-110">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="ea9da-111">Maven 3</span><span class="sxs-lookup"><span data-stu-id="ea9da-111">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="ea9da-112">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="ea9da-112">An active Azure account.</span></span> <span data-ttu-id="ea9da-113">(Bir hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz bir hesap](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.)</span><span class="sxs-lookup"><span data-stu-id="ea9da-113">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="ea9da-114">Cihaz kimliği programlı olarak oluşturmayı tercih ederseniz karşılık gelen bölümünde okuma [Cihazınızı Java kullanarak IOT hub'ınıza bağlanmak](iot-hub-java-java-getstarted.md#create-a-device-identity) makalesi.</span><span class="sxs-lookup"><span data-stu-id="ea9da-114">If you prefer to create the device identity programmatically, read the corresponding section in the [Connect your device to your IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="ea9da-115">Hizmet Uygulaması Oluştur</span><span class="sxs-lookup"><span data-stu-id="ea9da-115">Create the service app</span></span>

<span data-ttu-id="ea9da-116">Bu bölümde IOT Hub cihaz çiftine etiket ilişkili olarak, konum meta veri ekleyen bir Java uygulaması oluşturma **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="ea9da-116">In this section, you create a Java app that adds location metadata as a tag to the device twin in IoT Hub associated with **myDeviceId**.</span></span> <span data-ttu-id="ea9da-117">Uygulamayı ilk IOT hub'ın ABD'de bulunan aygıtları ve ardından bir cep telefonu ağ bağlantısı rapor cihazlar için sorgular.</span><span class="sxs-lookup"><span data-stu-id="ea9da-117">The app first queries IoT hub for devices located in the US, and then for devices that report a cellular network connection.</span></span>

1. <span data-ttu-id="ea9da-118">Geliştirme makinenizde adlı boş bir klasör oluşturun `iot-java-twin-getstarted`.</span><span class="sxs-lookup"><span data-stu-id="ea9da-118">On your development machine, create an empty folder called `iot-java-twin-getstarted`.</span></span>

1. <span data-ttu-id="ea9da-119">İçinde `iot-java-twin-getstarted` klasörünü adlı bir Maven projesi oluşturun **ekleme-etiketleri-query** , komut isteminde aşağıdaki komutu kullanarak.</span><span class="sxs-lookup"><span data-stu-id="ea9da-119">In the `iot-java-twin-getstarted` folder, create a Maven project called **add-tags-query** using the following command at your command prompt.</span></span> <span data-ttu-id="ea9da-120">Bunun tek ve uzun bir komut olduğunu unutmayın:</span><span class="sxs-lookup"><span data-stu-id="ea9da-120">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="ea9da-121">Komut isteminizde gidin `add-tags-query` klasör.</span><span class="sxs-lookup"><span data-stu-id="ea9da-121">At your command prompt, navigate to the `add-tags-query` folder.</span></span>

1. <span data-ttu-id="ea9da-122">Bir metin düzenleyicisi kullanarak açın `pom.xml` dosyasını `add-tags-query` klasörü ve aşağıdaki bağımlılığı eklemek **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="ea9da-122">Using a text editor, open the `pom.xml` file in the `add-tags-query` folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="ea9da-123">Bu bağımlılık kullanmanıza olanak tanır **IOT hizmeti istemcisi** IOT hub ile iletişim kurmak için uygulamanızda paketi:</span><span class="sxs-lookup"><span data-stu-id="ea9da-123">This dependency enables you to use the **iot-service-client** package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="ea9da-124">En son sürümü için kontrol edebilirsiniz **IOT hizmeti istemcisi** kullanarak [Maven arama](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="ea9da-124">You can check for the latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="ea9da-125">Aşağıdakileri ekleyin **yapı** düğümünden sonraki **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="ea9da-125">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="ea9da-126">Bu yapılandırma, uygulamanızı oluşturmak için Java 1.8 kullanmak için Maven bildirir:</span><span class="sxs-lookup"><span data-stu-id="ea9da-126">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="ea9da-127">Kaydet ve Kapat `pom.xml` dosya.</span><span class="sxs-lookup"><span data-stu-id="ea9da-127">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="ea9da-128">Bir metin düzenleyicisi kullanarak açın `add-tags-query\src\main\java\com\mycompany\app\App.java` dosya.</span><span class="sxs-lookup"><span data-stu-id="ea9da-128">Using a text editor, open the `add-tags-query\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="ea9da-129">Aşağıdaki **içeri aktarma** deyimlerini dosyaya ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ea9da-129">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. <span data-ttu-id="ea9da-130">Aşağıdaki sınıf düzeyi değişkenleri **App** sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ea9da-130">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="ea9da-131">Değiştir `{youriothubconnectionstring}` , not ettiğiniz, IOT hub bağlantı dizesine sahip *IOT Hub oluşturma* bölümü:</span><span class="sxs-lookup"><span data-stu-id="ea9da-131">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. <span data-ttu-id="ea9da-132">Güncelleştirme **ana** şunlar için yöntem imzası `throws` yan tümcesi:</span><span class="sxs-lookup"><span data-stu-id="ea9da-132">Update the **main** method signature to include the following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. <span data-ttu-id="ea9da-133">Aşağıdaki kodu ekleyin **ana** oluşturmak için yöntemi **DeviceTwin** ve **DeviceTwinDevice** nesneleri.</span><span class="sxs-lookup"><span data-stu-id="ea9da-133">Add the following code to the **main** method to create the **DeviceTwin** and **DeviceTwinDevice** objects.</span></span> <span data-ttu-id="ea9da-134">**DeviceTwin** nesnesini işleme IOT hub ile iletişim.</span><span class="sxs-lookup"><span data-stu-id="ea9da-134">The **DeviceTwin** object handles the communication with your IoT hub.</span></span> <span data-ttu-id="ea9da-135">**DeviceTwinDevice** nesne özelliklerini ve etiketler ile cihaz çifti temsil eder:</span><span class="sxs-lookup"><span data-stu-id="ea9da-135">The **DeviceTwinDevice** object represents the device twin with its properties and tags:</span></span>

    ```java
    // Get the DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. <span data-ttu-id="ea9da-136">Aşağıdakileri ekleyin `try/catch` için engelleyin **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="ea9da-136">Add the following `try/catch` block to the **main** method:</span></span>

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. <span data-ttu-id="ea9da-137">Güncelleştirilecek **bölge** ve **tesis** cihaz çifti etiketler, cihaz çiftine aşağıdaki kodu ekleyin `try` engelle:</span><span class="sxs-lookup"><span data-stu-id="ea9da-137">To update the **region** and **plant** device twin tags in your device twin, add the following code in the `try` block:</span></span>

    ```java
    // Get the device twin from IoT Hub
    System.out.println("Device twin before update:");
    twinClient.getTwin(device);
    System.out.println(device);

    // Update device twin tags if they are different
    // from the existing values
    String currentTags = device.tagsToString();
    if ((!currentTags.contains("region=" + region) && !currentTags.contains("plant=" + plant))) {
      // Create the tags and attach them to the DeviceTwinDevice object
      Set<Pair> tags = new HashSet<Pair>();
      tags.add(new Pair("region", region));
      tags.add(new Pair("plant", plant));
      device.setTags(tags);

      // Update the device twin in IoT Hub
      System.out.println("Updating device twin");
      twinClient.updateTwin(device);
    }

    // Retrieve the device twin with the tag values from IoT Hub
    System.out.println("Device twin after update:");
    twinClient.getTwin(device);
    System.out.println(device);
    ```

1. <span data-ttu-id="ea9da-138">IOT hub cihaz çiftlerini sorgulamak için aşağıdaki kodu ekleyin `try` önceki adımda eklediğiniz koddan sonra bloğu.</span><span class="sxs-lookup"><span data-stu-id="ea9da-138">To query the device twins in IoT hub, add the following code to the `try` block after the code you added in the previous step.</span></span> <span data-ttu-id="ea9da-139">Kod iki sorguları çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="ea9da-139">The code runs two queries.</span></span> <span data-ttu-id="ea9da-140">Her sorgu en fazla 100 cihazları döndürür:</span><span class="sxs-lookup"><span data-stu-id="ea9da-140">Each query returns a maximum of 100 devices:</span></span>

    ```java
    // Query the device twins in IoT Hub
    System.out.println("Devices in Redmond:");

    // Construct the query
    SqlQuery sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43'", null);

    // Run the query, returning a maximum of 100 devices
    Query twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 100);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }

    System.out.println("Devices in Redmond using a cellular network:");

    // Construct the query
    sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43' AND properties.reported.connectivityType = 'cellular'", null);

    // Run the query, returning a maximum of 100 devices
    twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 3);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }
    ```

1. <span data-ttu-id="ea9da-141">Kaydet ve Kapat `add-tags-query\src\main\java\com\mycompany\app\App.java` dosyası</span><span class="sxs-lookup"><span data-stu-id="ea9da-141">Save and close the `add-tags-query\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="ea9da-142">Yapı **ekleme-etiketleri-query** uygulama ve olan hataları düzeltin.</span><span class="sxs-lookup"><span data-stu-id="ea9da-142">Build the **add-tags-query** app and correct any errors.</span></span> <span data-ttu-id="ea9da-143">Komut isteminizde gidin `add-tags-query` klasörü ve aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ea9da-143">At your command prompt, navigate to the `add-tags-query` folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="ea9da-144">Cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea9da-144">Create a device app</span></span>

<span data-ttu-id="ea9da-145">Bu bölümde IOT hub'a gönderilen bir bildirilen özelliği değerini ayarlayan bir Java konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ea9da-145">In this section, you create a Java console app that sets a reported property value that is sent to IoT Hub.</span></span>

1. <span data-ttu-id="ea9da-146">İçinde `iot-java-twin-getstarted` klasörünü adlı bir Maven projesi oluşturun **simulated-device** , komut isteminde aşağıdaki komutu kullanarak.</span><span class="sxs-lookup"><span data-stu-id="ea9da-146">In the `iot-java-twin-getstarted` folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="ea9da-147">Bunun tek ve uzun bir komut olduğunu unutmayın:</span><span class="sxs-lookup"><span data-stu-id="ea9da-147">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="ea9da-148">Komut isteminizde gidin `simulated-device` klasör.</span><span class="sxs-lookup"><span data-stu-id="ea9da-148">At your command prompt, navigate to the `simulated-device` folder.</span></span>

1. <span data-ttu-id="ea9da-149">Bir metin düzenleyicisi kullanarak açın `pom.xml` dosyasını `simulated-device` klasörü ve aşağıdaki bağımlılıkları ekleyin **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="ea9da-149">Using a text editor, open the `pom.xml` file in the `simulated-device` folder and add the following dependencies to the **dependencies** node.</span></span> <span data-ttu-id="ea9da-150">Bu bağımlılık kullanmanıza olanak tanır **IOT cihaz istemci** IOT hub ile iletişim kurmak için uygulamanızda paketi:</span><span class="sxs-lookup"><span data-stu-id="ea9da-150">This dependency enables you to use the **iot-device-client** package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="ea9da-151">En son sürümü için kontrol edebilirsiniz **IOT cihaz istemci** kullanarak [Maven arama](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="ea9da-151">You can check for the latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="ea9da-152">Aşağıdakileri ekleyin **yapı** düğümünden sonraki **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="ea9da-152">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="ea9da-153">Bu yapılandırma, uygulamanızı oluşturmak için Java 1.8 kullanmak için Maven bildirir:</span><span class="sxs-lookup"><span data-stu-id="ea9da-153">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="ea9da-154">Kaydet ve Kapat `pom.xml` dosya.</span><span class="sxs-lookup"><span data-stu-id="ea9da-154">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="ea9da-155">Bir metin düzenleyicisi kullanarak açın `simulated-device\src\main\java\com\mycompany\app\App.java` dosya.</span><span class="sxs-lookup"><span data-stu-id="ea9da-155">Using a text editor, open the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="ea9da-156">Aşağıdaki **içeri aktarma** deyimlerini dosyaya ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ea9da-156">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="ea9da-157">Aşağıdaki sınıf düzeyi değişkenleri **App** sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ea9da-157">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="ea9da-158">Değiştirme `{youriothubname}` , IOT hub'ı adıyla ve `{yourdevicekey}` içinde oluşturulan cihaz anahtarla değeri *bir cihaz kimliği oluşturma* bölümü:</span><span class="sxs-lookup"><span data-stu-id="ea9da-158">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with the device key value you generated in the *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    ```

    <span data-ttu-id="ea9da-159">Bu örnek uygulama, bir **DeviceClient** nesnesi örneğini oluşturduğunda **prokotol** değişkenini kullanır.</span><span class="sxs-lookup"><span data-stu-id="ea9da-159">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="ea9da-160">Şu anda, cihaz çifti özelliklerini kullanmak için MQTT Protokolü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea9da-160">Currently, to use device twin features you must use the MQTT protocol.</span></span>

1. <span data-ttu-id="ea9da-161">Aşağıdaki kodu ekleyin **ana** yöntemi için:</span><span class="sxs-lookup"><span data-stu-id="ea9da-161">Add the following code to the **main** method to:</span></span>
    * <span data-ttu-id="ea9da-162">IOT Hub ile iletişim kurmak için bir cihaz istemcisi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ea9da-162">Create a device client to communicate with IoT Hub.</span></span>
    * <span data-ttu-id="ea9da-163">Oluşturma bir **aygıt** cihaz çifti özelliklerini depolamak için nesne.</span><span class="sxs-lookup"><span data-stu-id="ea9da-163">Create a **Device** object to store the device twin properties.</span></span>

    ```java
    DeviceClient client = new DeviceClient(connString, protocol);

    // Create a Device object to store the device twin properties
    Device dataCollector = new Device() {
      // Print details when a property value changes
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context) {
        System.out.println(propertyKey + " changed to " + propertyValue);
      }
    };
    ```

1. <span data-ttu-id="ea9da-164">Aşağıdaki kodu ekleyin **ana** yöntemi oluşturmak için bir **connectivityType** özelliği bildirilen ve IOT Hub'ına gönderebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ea9da-164">Add the following code to the **main** method to create a **connectivityType** reported property and send it to IoT Hub:</span></span>

    ```java
    try {
      // Open the DeviceClient and start the device twin services.
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);

      // Create a reported property and send it to your IoT hub.
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

1. <span data-ttu-id="ea9da-165">Sonuna aşağıdaki kodu ekleyin **ana** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ea9da-165">Add the following code to the end of the **main** method.</span></span> <span data-ttu-id="ea9da-166">Bekleyen **Enter** anahtar IOT Hub'ın cihaz çifti işlemlerinin durumunu raporlamak için zaman sağlar:</span><span class="sxs-lookup"><span data-stu-id="ea9da-166">Waiting for the **Enter** key allows time for IoT Hub to report the status of the device twin operations:</span></span>

    ```java
    System.out.println("Press any key to exit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. <span data-ttu-id="ea9da-167">Kaydet ve Kapat `simulated-device\src\main\java\com\mycompany\app\App.java` dosya.</span><span class="sxs-lookup"><span data-stu-id="ea9da-167">Save and close the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="ea9da-168">Yapı **simulated-device** uygulama ve olan hataları düzeltin.</span><span class="sxs-lookup"><span data-stu-id="ea9da-168">Build the **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="ea9da-169">Komut isteminizde gidin `simulated-device` klasörü ve aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ea9da-169">At your command prompt, navigate to the `simulated-device` folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-the-apps"></a><span data-ttu-id="ea9da-170">Uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="ea9da-170">Run the apps</span></span>

<span data-ttu-id="ea9da-171">Şimdi konsol uygulamaları çalıştırmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="ea9da-171">You are now ready to run the console apps.</span></span>

1. <span data-ttu-id="ea9da-172">Bir komut isteminde `add-tags-query` klasörü çalıştırmak için aşağıdaki komutu çalıştırın, **ekleme-etiketleri-query** service uygulaması:</span><span class="sxs-lookup"><span data-stu-id="ea9da-172">At a command prompt in the `add-tags-query` folder, run the following command to run the **add-tags-query** service app:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Etiket değerleri güncelleştirmek ve cihaz sorguları çalıştırmak için Java IOT Hub hizmeti uygulaması](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    <span data-ttu-id="ea9da-174">Gördüğünüz **tesis** ve **bölge** cihaz çifti eklenen etiketler.</span><span class="sxs-lookup"><span data-stu-id="ea9da-174">You can see the **plant** and **region** tags added to the device twin.</span></span> <span data-ttu-id="ea9da-175">İlk sorguyu Cihazınızı döndürür, ancak ikinci desteklemez.</span><span class="sxs-lookup"><span data-stu-id="ea9da-175">The first query returns your device, but the second does not.</span></span>

1. <span data-ttu-id="ea9da-176">Bir komut isteminde `simulated-device` klasörü eklemek için aşağıdaki komutu çalıştırın, **connectivityType** özelliği cihaz çifti bildirdi:</span><span class="sxs-lookup"><span data-stu-id="ea9da-176">At a command prompt in the `simulated-device` folder, run the following command to add the **connectivityType** reported property to the device twin:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Aygıt istemcisi ekler ** connectivityType ** bildirilen özelliği](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. <span data-ttu-id="ea9da-178">Bir komut isteminde `add-tags-query` klasörü çalıştırmak için aşağıdaki komutu çalıştırın, **ekleme-etiketleri-query** service uygulaması ikinci kez:</span><span class="sxs-lookup"><span data-stu-id="ea9da-178">At a command prompt in the `add-tags-query` folder, run the following command to run the **add-tags-query** service app a second time:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Etiket değerleri güncelleştirmek ve cihaz sorguları çalıştırmak için Java IOT Hub hizmeti uygulaması](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    <span data-ttu-id="ea9da-180">Cihazınızı gönderdi artık **connectivityType** özelliği IOT Hub'ına ikinci sorguyu Cihazınızı döndürür.</span><span class="sxs-lookup"><span data-stu-id="ea9da-180">Now your device has sent the **connectivityType** property to IoT Hub, the second query returns your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea9da-181">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ea9da-181">Next steps</span></span>

<span data-ttu-id="ea9da-182">Bu öğreticide, Azure portalında yeni bir IoT hub'ı yapılandırdınız ve ardından IoT hub'ının kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="ea9da-182">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="ea9da-183">Cihaz meta verilerini etiketi gibi bir arka uç uygulamadan eklenen ve cihaz uygulaması rapor cihaz bağlantı bilgilerini cihaz çiftine yazıldı.</span><span class="sxs-lookup"><span data-stu-id="ea9da-183">You added device metadata as tags from a back-end app, and wrote a device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="ea9da-184">Ayrıca SQL benzeri IOT hub'ı sorgu dili kullanarak cihaz çifti bilgileri sorgulamak öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="ea9da-184">You also learned how to query the device twin information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="ea9da-185">Bilgi edinmek için aşağıdaki kaynakları kullanın nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="ea9da-185">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="ea9da-186">Aygıtlarla telemetri gönderen [IOT Hub ile çalışmaya başlama](iot-hub-java-java-getstarted.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="ea9da-186">Send telemetry from devices with the [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="ea9da-187">Aygıtlarını etkileşimli olarak (örneğin, kullanıcı tarafından denetlenen bir uygulamadan fan etkinleştirdikten) ile [doğrudan yöntemleri kullanın](iot-hub-java-java-direct-methods.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="ea9da-187">Control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
