---
title: "Azure IOT Hub cihaz Yönetimi (Java) ile çalışmaya başlama | Microsoft Docs"
description: "Uzak aygıt yeniden başlatma işlemi başlatmak için Azure IOT Hub cihaz yönetimini kullanma Doğrudan bir yöntem ve Azure IOT hizmeti doğrudan yöntemini çağıran bir hizmet uygulaması uygulamak için Java SDK'sını içeren bir sanal cihaz uygulamasının uygulamak için Azure IOT cihaz SDK'sı Java için kullanın."
services: iot-hub
documentationcenter: .java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: c75635f366f5ced4bf91792d1a905dd6aab8ed79
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-device-management-java"></a><span data-ttu-id="b5dad-104">Aygıt Yönetimi (Java) ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="b5dad-104">Get started with device management (Java)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="b5dad-105">Bu öğretici şunların nasıl yapıldığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="b5dad-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="b5dad-106">IOT hub'ı oluşturun ve IOT hub'ınızda bir cihaz kimliği oluşturma için Azure Portalı'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="b5dad-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="b5dad-107">Cihaz yeniden başlatmak için doğrudan bir yöntem uygulayan bir sanal cihaz uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="b5dad-107">Create a simulated device app that implements a direct method to reboot the device.</span></span> <span data-ttu-id="b5dad-108">Doğrudan yöntemleri buluttan çağrılır.</span><span class="sxs-lookup"><span data-stu-id="b5dad-108">Direct methods are invoked from the cloud.</span></span>
* <span data-ttu-id="b5dad-109">IOT hub'ınız aracılığıyla sanal cihaz uygulama yeniden başlatma doğrudan yöntemini çağıran bir uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b5dad-109">Create an app that invokes the reboot direct method in the simulated device app through your IoT hub.</span></span> <span data-ttu-id="b5dad-110">Bu uygulama daha sonra yeniden başlatma işlemi tamamlandığında görmek için aygıt bildirilen özelliklerinden izler.</span><span class="sxs-lookup"><span data-stu-id="b5dad-110">This app then monitors the reported properties from the device to see when the reboot operation is complete.</span></span>

<span data-ttu-id="b5dad-111">Bu öğreticinin sonunda iki Java konsol uygulamaları vardır:</span><span class="sxs-lookup"><span data-stu-id="b5dad-111">At the end of this tutorial, you have two Java console apps:</span></span>

<span data-ttu-id="b5dad-112">**simulated-device**.</span><span class="sxs-lookup"><span data-stu-id="b5dad-112">**simulated-device**.</span></span> <span data-ttu-id="b5dad-113">Bu uygulama:</span><span class="sxs-lookup"><span data-stu-id="b5dad-113">This app:</span></span>

* <span data-ttu-id="b5dad-114">Daha önce oluşturulan cihaz kimliğiyle IOT hub'ınıza bağlanır.</span><span class="sxs-lookup"><span data-stu-id="b5dad-114">Connects to your IoT hub with the device identity created earlier.</span></span>
* <span data-ttu-id="b5dad-115">Yeniden başlatma doğrudan yöntem çağrısı alır.</span><span class="sxs-lookup"><span data-stu-id="b5dad-115">Receives a reboot direct method call.</span></span>
* <span data-ttu-id="b5dad-116">Fiziksel bir yeniden başlatma benzetimini yapar.</span><span class="sxs-lookup"><span data-stu-id="b5dad-116">Simulates a physical reboot.</span></span>
* <span data-ttu-id="b5dad-117">Bildirilen bir özellik aracılığıyla son yeniden başlatma zamanı raporlar.</span><span class="sxs-lookup"><span data-stu-id="b5dad-117">Reports the time of the last reboot through a reported property.</span></span>

<span data-ttu-id="b5dad-118">**Tetikleyici yeniden başlatma**.</span><span class="sxs-lookup"><span data-stu-id="b5dad-118">**trigger-reboot**.</span></span> <span data-ttu-id="b5dad-119">Bu uygulama:</span><span class="sxs-lookup"><span data-stu-id="b5dad-119">This app:</span></span>

* <span data-ttu-id="b5dad-120">Sanal cihaz uygulamasının doğrudan bir yöntem çağırır.</span><span class="sxs-lookup"><span data-stu-id="b5dad-120">Calls a direct method in the simulated device app.</span></span>
* <span data-ttu-id="b5dad-121">Sanal aygıt tarafından gönderilen doğrudan yöntem çağrısının yanıtı görüntüler</span><span class="sxs-lookup"><span data-stu-id="b5dad-121">Displays the response to the direct method call sent by the simulated device</span></span>
* <span data-ttu-id="b5dad-122">Güncelleştirilmiş görüntüler özellikleri bildirdi.</span><span class="sxs-lookup"><span data-stu-id="b5dad-122">Displays the updated reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="b5dad-123">Aygıtları ve çözüm arka ucunuz çalıştırmak için uygulamalar oluşturmak için kullanabileceğiniz SDK'ları hakkında daha fazla bilgi için bkz: [Azure IOT SDK'ları][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="b5dad-123">For information about the SDKs that you can use to build applications to run on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="b5dad-124">Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="b5dad-124">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="b5dad-125">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="b5dad-125">Java SE 8.</span></span> <br/> <span data-ttu-id="b5dad-126">[Geliştirme ortamınızı hazırlama][lnk-dev-setup], bu öğretici için Java'nın Windows veya Linux'ta nasıl yükleneceğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="b5dad-126">[Prepare your development environment][lnk-dev-setup] describes how to install Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="b5dad-127">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="b5dad-127">Maven 3.</span></span>  <br/> <span data-ttu-id="b5dad-128">[Geliştirme ortamınızı hazırlama][lnk-dev-setup], bu öğretici için [Maven][lnk-maven]'ın Windows veya Linux'ta nasıl yükleneceğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="b5dad-128">[Prepare your development environment][lnk-dev-setup] describes how to install [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="b5dad-129">[Node.js sürümünü 0.10.0 veya üzeri](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="b5dad-129">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a><span data-ttu-id="b5dad-130">Tetikleyici doğrudan bir yöntem kullanarak cihaz üzerinde Uzaktan yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="b5dad-130">Trigger a remote reboot on the device using a direct method</span></span>

<span data-ttu-id="b5dad-131">Bu bölümde, bir Java konsol uygulaması, oluşturun:</span><span class="sxs-lookup"><span data-stu-id="b5dad-131">In this section, you create a Java console app that:</span></span>

1. <span data-ttu-id="b5dad-132">Sanal cihaz uygulamasının yeniden başlatma doğrudan yöntemi çağırır.</span><span class="sxs-lookup"><span data-stu-id="b5dad-132">Invokes the reboot direct method in the simulated device app.</span></span>
1. <span data-ttu-id="b5dad-133">Yanıt görüntüler.</span><span class="sxs-lookup"><span data-stu-id="b5dad-133">Displays the response.</span></span>
1. <span data-ttu-id="b5dad-134">Anketler yeniden başlatmanın ne zaman tamamlandığını belirlemek için cihazın gönderilen bildirilen özellikleri.</span><span class="sxs-lookup"><span data-stu-id="b5dad-134">Polls the reported properties sent from the device to determine when the reboot is complete.</span></span>

<span data-ttu-id="b5dad-135">Bu konsol uygulamasını IOT doğrudan yöntemini çağırmak ve bildirilen özellikleri okumak için Hub'ınıza bağlanır.</span><span class="sxs-lookup"><span data-stu-id="b5dad-135">This console app connects to your IoT Hub to invoke the direct method and read the reported properties.</span></span>

1. <span data-ttu-id="b5dad-136">DM-get-started adlı boş bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b5dad-136">Create an empty folder called dm-get-started.</span></span>

1. <span data-ttu-id="b5dad-137">Dm-get-started klasöründe adlı bir Maven projesi oluşturun **tetikleyici yeniden başlatma** , komut isteminde aşağıdaki komutu kullanarak.</span><span class="sxs-lookup"><span data-stu-id="b5dad-137">In the dm-get-started folder, create a Maven project called **trigger-reboot** using the following command at your command prompt.</span></span> <span data-ttu-id="b5dad-138">Tek ve uzun bir komut gösterir:</span><span class="sxs-lookup"><span data-stu-id="b5dad-138">The following shows a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="b5dad-139">Komut isteminizde tetikleyici yeniden başlatma klasöre gidin.</span><span class="sxs-lookup"><span data-stu-id="b5dad-139">At your command prompt, navigate to the trigger-reboot folder.</span></span>

1. <span data-ttu-id="b5dad-140">Bir metin düzenleyicisi kullanarak, tetikleyici yeniden başlatma klasöründeki pom.xml dosyasını açın ve aşağıdaki bağımlılığı eklemek **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="b5dad-140">Using a text editor, open the pom.xml file in the trigger-reboot folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="b5dad-141">Bu bağımlılık, IOT hub ile iletişim kurmak için uygulamanızda IOT-service-client paketini kullanmanıza olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="b5dad-141">This dependency enables you to use the iot-service-client package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="b5dad-142">[Maven arama][lnk-maven-service-search] kullanarak en yeni **iot-service-client** sürümünü kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b5dad-142">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="b5dad-143">Aşağıdakileri ekleyin **yapı** düğümünden sonraki **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="b5dad-143">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="b5dad-144">Bu yapılandırma, uygulamanızı oluşturmak için Java 1.8 kullanmak için Maven bildirir:</span><span class="sxs-lookup"><span data-stu-id="b5dad-144">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="b5dad-145">pom.xml dosyasını kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="b5dad-145">Save and close the pom.xml file.</span></span>

1. <span data-ttu-id="b5dad-146">Bir metin düzenleyicisi kullanarak trigger-reboot\src\main\java\com\mycompany\app\App.java kaynak dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="b5dad-146">Using a text editor, open the trigger-reboot\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="b5dad-147">Aşağıdaki **içeri aktarma** deyimlerini dosyaya ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b5dad-147">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwin;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

1. <span data-ttu-id="b5dad-148">Aşağıdaki sınıf düzeyi değişkenleri **App** sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b5dad-148">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="b5dad-149">Değiştir `{youriothubconnectionstring}` , not ettiğiniz, IOT hub bağlantı dizesine sahip *IOT Hub oluşturma* bölümü:</span><span class="sxs-lookup"><span data-stu-id="b5dad-149">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. <span data-ttu-id="b5dad-150">Bildirilen özellikleri cihaz çifti 10 saniyede okuyan bir iş parçacığı uygulamak için aşağıdaki iç içe geçmiş sınıf ekleme **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="b5dad-150">To implement a thread that reads the reported properties from the device twin every 10 seconds, add the following nested class to the **App** class:</span></span>

    ```java
    private static class ShowReportedProperties implements Runnable {
      public void run() {
        try {
          DeviceTwin deviceTwins = DeviceTwin.createFromConnectionString(iotHubConnectionString);
          DeviceTwinDevice twinDevice = new DeviceTwinDevice(deviceId);
          while (true) {
            System.out.println("Get reported properties from device twin");
            deviceTwins.getTwin(twinDevice);
            System.out.println(twinDevice.reportedPropertiesToString());
            Thread.sleep(10000);
          }
        } catch (Exception ex) {
          System.out.println("Exception reading reported properties: " + ex.getMessage());
        }
      }
    }
    ```

1. <span data-ttu-id="b5dad-151">Sanal cihaz için yeniden başlatma doğrudan yöntemini çağırmak için aşağıdaki kodu ekleyin **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="b5dad-151">To invoke the reboot direct method on the simulated device, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
      System.out.println("Invoke reboot direct method");
      MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, null);

      if(result == null)
      {
        throw new IOException("Invoke direct method reboot returns null");
      }
      System.out.println("Invoked reboot on device");
      System.out.println("Status for device:   " + result.getStatus());
      System.out.println("Message from device: " + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }
    ```

1. <span data-ttu-id="b5dad-152">Sanal cihaz bildirilen özelliklerinden yoklamak için iş parçacığı başlatmak için aşağıdaki kodu ekleyin **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="b5dad-152">To start the thread to poll the reported properties from the simulated device, add the following code to the **main** method:</span></span>

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. <span data-ttu-id="b5dad-153">Uygulamayı durdurun sağlamak için aşağıdaki kodu ekleyin **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="b5dad-153">To enable you to stop the app, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Press ENTER to exit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. <span data-ttu-id="b5dad-154">Trigger-reboot\src\main\java\com\mycompany\app\App.java dosyasını kaydedip kapatın.</span><span class="sxs-lookup"><span data-stu-id="b5dad-154">Save and close the trigger-reboot\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="b5dad-155">Yapı **tetikleyici yeniden başlatma** arka uç uygulama ve olan hataları düzeltin.</span><span class="sxs-lookup"><span data-stu-id="b5dad-155">Build the **trigger-reboot** back-end app and correct any errors.</span></span> <span data-ttu-id="b5dad-156">Komut isteminde, tetikleyici yeniden başlatma klasörüne gidin ve aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b5dad-156">At your command prompt, navigate to the trigger-reboot folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="b5dad-157">Sanal cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="b5dad-157">Create a simulated device app</span></span>

<span data-ttu-id="b5dad-158">Bu bölümde, bir cihaza benzetim bir Java konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b5dad-158">In this section, you create a Java console app that simulates a device.</span></span> <span data-ttu-id="b5dad-159">Yeniden başlatma uygulama dinler yöntem çağrısı IOT hub'ınızı ve hemen o aramayı yanıtlar doğrudan.</span><span class="sxs-lookup"><span data-stu-id="b5dad-159">The app listens for the reboot direct method call from your IoT hub and immediately responds to that call.</span></span> <span data-ttu-id="b5dad-160">Uygulama sonra uykuya geçme bildirmek için bildirilen bir özellik kullanmadan önce yeniden başlatma işleminin benzetimini yapmak bir süre için **tetikleyici yeniden başlatma** yeniden başlatma tamamlandıktan arka uç uygulama.</span><span class="sxs-lookup"><span data-stu-id="b5dad-160">The app then sleeps for a while to simulate the reboot process before it uses a reported property to notify the **trigger-reboot** back-end app that the reboot is complete.</span></span>

1. <span data-ttu-id="b5dad-161">Dm-get-started klasöründe adlı bir Maven projesi oluşturun **simulated-device** , komut isteminde aşağıdaki komutu kullanarak.</span><span class="sxs-lookup"><span data-stu-id="b5dad-161">In the dm-get-started folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="b5dad-162">Tek ve uzun bir komut verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b5dad-162">The following is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="b5dad-163">Komut isteminizde simulated-device klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="b5dad-163">At your command prompt, navigate to the simulated-device folder.</span></span>

1. <span data-ttu-id="b5dad-164">Bir metin düzenleyicisi kullanarak simulated-device klasöründeki pom.xml dosyasını açın ve aşağıdaki bağımlılığı eklemek **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="b5dad-164">Using a text editor, open the pom.xml file in the simulated-device folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="b5dad-165">Bu bağımlılık, IOT hub ile iletişim kurmak için uygulamanızda IOT-service-client paketini kullanmanıza olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="b5dad-165">This dependency enables you to use the iot-service-client package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="b5dad-166">[Maven arama][lnk-maven-device-search] kullanarak en yeni **iot-device-client** sürümünü kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b5dad-166">You can check for the latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="b5dad-167">Aşağıdakileri ekleyin **yapı** düğümünden sonraki **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="b5dad-167">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="b5dad-168">Bu yapılandırma, uygulamanızı oluşturmak için Java 1.8 kullanmak için Maven bildirir:</span><span class="sxs-lookup"><span data-stu-id="b5dad-168">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="b5dad-169">pom.xml dosyasını kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="b5dad-169">Save and close the pom.xml file.</span></span>

1. <span data-ttu-id="b5dad-170">Bir metin düzenleyicisi kullanarak simulated-device\src\main\java\com\mycompany\app\App.java kaynak dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="b5dad-170">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="b5dad-171">Aşağıdaki **içeri aktarma** deyimlerini dosyaya ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b5dad-171">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.time.LocalDateTime;
    import java.util.Scanner;
    import java.util.Set;
    import java.util.HashSet;
    ```

1. <span data-ttu-id="b5dad-172">Aşağıdaki sınıf düzeyi değişkenleri **App** sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b5dad-172">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="b5dad-173">Değiştir `{yourdeviceconnectionstring}` , not ettiğiniz aygıt bağlantı dizesiyle *bir cihaz kimliği oluşturma* bölümü:</span><span class="sxs-lookup"><span data-stu-id="b5dad-173">Replace `{yourdeviceconnectionstring}` with the device connection string you noted in the *Create a device identity* section:</span></span>

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. <span data-ttu-id="b5dad-174">Doğrudan yöntem durum olayları için bir geri çağırma işleyici uygulamak için aşağıdaki iç içe geçmiş sınıf ekleme **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="b5dad-174">To implement a callback handler for direct method status events, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded to device method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="b5dad-175">Cihaz çifti durum olayları için bir geri çağırma işleyici uygulamak için aşağıdaki iç içe geçmiş sınıf ekleme **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="b5dad-175">To implement a callback handler for device twin status events, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded to device twin operation with status " + status.name());
        }
    }
    ```

1. <span data-ttu-id="b5dad-176">Özellik olayları için bir geri çağırma işleyici uygulamak için aşağıdaki iç içe geçmiş sınıf ekleme **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="b5dad-176">To implement a callback handler for property events, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class PropertyCallback implements PropertyCallBack<String, String>
    {
      public void PropertyCall(String propertyKey, String propertyValue, Object context)
      {
        System.out.println("PropertyKey:     " + propertyKey);
        System.out.println("PropertyKvalue:  " + propertyKey);
      }
    }
    ```

1. <span data-ttu-id="b5dad-177">Aygıt yeniden başlatma benzetimini yapmak için bir iş parçacığı uygulamak için aşağıdaki iç içe geçmiş sınıf ekleme **uygulama** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="b5dad-177">To implement a thread to simulate the device reboot, add the following nested class to the **App** class.</span></span> <span data-ttu-id="b5dad-178">İş parçacığı beş saniye için uyku moduna geçer ve ardından ayarlar **lastReboot** özelliği bildirdi:</span><span class="sxs-lookup"><span data-stu-id="b5dad-178">The thread sleeps for five seconds and then sets the **lastReboot** reported property:</span></span>

    ```java
    protected static class RebootDeviceThread implements Runnable {
      public void run() {
        try {
          System.out.println("Rebooting...");
          Thread.sleep(5000);
          Property property = new Property("lastReboot", LocalDateTime.now());
          Set<Property> properties = new HashSet<Property>();
          properties.add(property);
          client.sendReportedProperties(properties);
          System.out.println("Rebooted");
        }
        catch (Exception ex) {
          System.out.println("Exception in reboot thread: " + ex.getMessage());
        }
      }
    }
    ```

1. <span data-ttu-id="b5dad-179">Cihazda doğrudan yöntemi uygulamak için aşağıdaki iç içe geçmiş sınıf ekleme **uygulama** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="b5dad-179">To implement the direct method on the device, add the following nested class to the **App** class.</span></span> <span data-ttu-id="b5dad-180">Ne zaman sanal uygulama alan bir çağrı **yeniden** doğrudan yöntemi, bir bildirim çağırana döndürür ve ardından yeniden işlemek için bir iş parçacığı başlatır:</span><span class="sxs-lookup"><span data-stu-id="b5dad-180">When the simulated app receives a call to the **reboot** direct method, it returns an acknowledgement to the caller and then starts a thread to process the reboot:</span></span>

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "reboot" :
          {
            int status = METHOD_SUCCESS;
            System.out.println("Received reboot request");
            deviceMethodData = new DeviceMethodData(status, "Started reboot");
            RebootDeviceThread rebootThread = new RebootDeviceThread();
            Thread t = new Thread(rebootThread);
            t.start();
            break;
          }
          default:
          {
            int status = METHOD_NOT_DEFINED;
            deviceMethodData = new DeviceMethodData(status, "Not defined direct method " + methodName);
          }
        }
        return deviceMethodData;
      }
    }
    ```

1. <span data-ttu-id="b5dad-181">İmzası değiştirme **ana** aşağıdaki özel durumlar oluşturma yöntemi:</span><span class="sxs-lookup"><span data-stu-id="b5dad-181">Modify the signature of the **main** method to throw the following exceptions:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="b5dad-182">Örneği oluşturmak için bir **DeviceClient**, aşağıdaki kodu ekleyin **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="b5dad-182">To instantiate a **DeviceClient**, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. <span data-ttu-id="b5dad-183">Doğrudan yöntem çağrıları için dinleme başlatmak için aşağıdaki kodu ekleyin **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="b5dad-183">To start listening for direct method calls, add the following code to the **main** method:</span></span>

    ```java
    try
    {
      client.open();
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
      client.startDeviceTwin(new DeviceTwinStatusCallback(), null, new PropertyCallback(), null);
      System.out.println("Subscribed to direct methods and polling for reported properties. Waiting...");
    }
    catch (Exception e)
    {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="b5dad-184">Aygıt benzeticisi kapatmak için aşağıdaki kodu ekleyin **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="b5dad-184">To shut down the device simulator, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Press any key to exit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. <span data-ttu-id="b5dad-185">Simulated-device\src\main\java\com\mycompany\app\App.java dosyasını kaydedip kapatın.</span><span class="sxs-lookup"><span data-stu-id="b5dad-185">Save and close the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="b5dad-186">Yapı **simulated-device** arka uç uygulama ve olan hataları düzeltin.</span><span class="sxs-lookup"><span data-stu-id="b5dad-186">Build the **simulated-device** back-end app and correct any errors.</span></span> <span data-ttu-id="b5dad-187">Komut isteminde, simulated-device klasörüne gidin ve aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b5dad-187">At your command prompt, navigate to the simulated-device folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-the-apps"></a><span data-ttu-id="b5dad-188">Uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b5dad-188">Run the apps</span></span>

<span data-ttu-id="b5dad-189">Şimdi uygulamaları çalıştırmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="b5dad-189">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="b5dad-190">Simulated-device klasöründeki bir komut isteminde IOT hub'ınızı gelen yeniden başlatma yöntemi çağrıları dinleme yapmaya başlamak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b5dad-190">At a command prompt in the simulated-device folder, run the following command to begin listening for reboot method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Dinlemek için Java IOT hub'ı sanal cihaz uygulamasının yeniden doğrudan yöntem çağrıları][1]

1. <span data-ttu-id="b5dad-192">Tetikleyici yeniden başlatma klasöründeki bir komut isteminde IOT hub'ından sanal cihazınız üzerinde yeniden başlatma yöntemini çağırmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b5dad-192">At a command prompt in the trigger-reboot folder, run the following command to call the reboot method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Yeniden başlatma doğrudan yöntemini çağırmak için Java IOT Hub hizmeti uygulaması][2]

1. <span data-ttu-id="b5dad-194">Sanal cihaz yeniden başlatma doğrudan yöntem çağrısı yanıt verir:</span><span class="sxs-lookup"><span data-stu-id="b5dad-194">The simulated device responds to the reboot direct method call:</span></span>

    ![Java IOT hub'ı sanal cihaz uygulamasının doğrudan yöntem çağrısı yanıt verir.][3]

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[1]: ./media/iot-hub-java-java-device-management-getstarted/launchsimulator.png
[2]: ./media/iot-hub-java-java-device-management-getstarted/triggerreboot.png
[3]: ./media/iot-hub-java-java-device-management-getstarted/respondtoreboot.png
<!-- Links -->

[lnk-maven]: https://maven.apache.org/what-is-maven.html

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22