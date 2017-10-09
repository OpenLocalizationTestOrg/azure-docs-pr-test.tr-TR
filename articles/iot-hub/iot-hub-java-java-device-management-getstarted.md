---
title: "aaaGet başlatılan ile Azure IOT Hub cihaz Yönetimi (Java) | Microsoft Docs"
description: "Nasıl toouse Azure IOT Hub cihaz Yönetimi tooinitiate uzaktaki bir aygıtı yeniden başlatın. Java tooimplement doğrudan yöntemi ve hello Java tooimplement hello doğrudan yöntemini çağıran bir hizmet uygulaması için Azure IOT hizmeti SDK'sını içeren sanal cihaz uygulaması için hello Azure IOT cihaz SDK'sını kullanın."
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
ms.openlocfilehash: 7aaeda9d4ff7002e5c66adfd61e2dfd5bcea964f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-java"></a><span data-ttu-id="2fb90-104">Aygıt Yönetimi (Java) ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="2fb90-104">Get started with device management (Java)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="2fb90-105">Bu öğretici şunların nasıl yapıldığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="2fb90-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="2fb90-106">IOT hub'ınızda bir cihaz kimliği oluşturma ve Hello Azure portal toocreate IOT hub'ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="2fb90-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="2fb90-107">Bir doğrudan yöntemi tooreboot hello aygıtı uygulayan bir sanal cihaz uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="2fb90-107">Create a simulated device app that implements a direct method tooreboot hello device.</span></span> <span data-ttu-id="2fb90-108">Doğrudan yöntemleri hello buluttan çağrılır.</span><span class="sxs-lookup"><span data-stu-id="2fb90-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="2fb90-109">IOT hub'ınız aracılığıyla hello sanal cihaz uygulamasında hello yeniden başlatma doğrudan yöntemini çağıran bir uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2fb90-109">Create an app that invokes hello reboot direct method in hello simulated device app through your IoT hub.</span></span> <span data-ttu-id="2fb90-110">Bu uygulama daha sonra hello yeniden başlatma işlemi tamamlandığında hello aygıt toosee bildirilen özelliklerinden hello izleyiciler.</span><span class="sxs-lookup"><span data-stu-id="2fb90-110">This app then monitors hello reported properties from hello device toosee when hello reboot operation is complete.</span></span>

<span data-ttu-id="2fb90-111">Bu öğreticinin Hello sonunda, iki Java konsol uygulamaları vardır:</span><span class="sxs-lookup"><span data-stu-id="2fb90-111">At hello end of this tutorial, you have two Java console apps:</span></span>

<span data-ttu-id="2fb90-112">**simulated-device**.</span><span class="sxs-lookup"><span data-stu-id="2fb90-112">**simulated-device**.</span></span> <span data-ttu-id="2fb90-113">Bu uygulama:</span><span class="sxs-lookup"><span data-stu-id="2fb90-113">This app:</span></span>

* <span data-ttu-id="2fb90-114">Tooyour IOT hub'ı daha önce oluşturduğunuz hello cihaz kimliği bağlanır.</span><span class="sxs-lookup"><span data-stu-id="2fb90-114">Connects tooyour IoT hub with hello device identity created earlier.</span></span>
* <span data-ttu-id="2fb90-115">Yeniden başlatma doğrudan yöntem çağrısı alır.</span><span class="sxs-lookup"><span data-stu-id="2fb90-115">Receives a reboot direct method call.</span></span>
* <span data-ttu-id="2fb90-116">Fiziksel bir yeniden başlatma benzetimini yapar.</span><span class="sxs-lookup"><span data-stu-id="2fb90-116">Simulates a physical reboot.</span></span>
* <span data-ttu-id="2fb90-117">Merhaba son yeniden başlatmadan bildirilen bir özellik aracılığıyla raporları hello zamanı.</span><span class="sxs-lookup"><span data-stu-id="2fb90-117">Reports hello time of hello last reboot through a reported property.</span></span>

<span data-ttu-id="2fb90-118">**Tetikleyici yeniden başlatma**.</span><span class="sxs-lookup"><span data-stu-id="2fb90-118">**trigger-reboot**.</span></span> <span data-ttu-id="2fb90-119">Bu uygulama:</span><span class="sxs-lookup"><span data-stu-id="2fb90-119">This app:</span></span>

* <span data-ttu-id="2fb90-120">Merhaba sanal cihaz uygulamasının doğrudan bir yöntem çağırır.</span><span class="sxs-lookup"><span data-stu-id="2fb90-120">Calls a direct method in hello simulated device app.</span></span>
* <span data-ttu-id="2fb90-121">Merhaba yanıt toohello doğrudan yöntem çağrısı Hello sanal aygıt tarafından gönderilen görüntüler</span><span class="sxs-lookup"><span data-stu-id="2fb90-121">Displays hello response toohello direct method call sent by hello simulated device</span></span>
* <span data-ttu-id="2fb90-122">Güncelleştirilmiş görüntüler hello özellikleri bildirdi.</span><span class="sxs-lookup"><span data-stu-id="2fb90-122">Displays hello updated reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="2fb90-123">Cihazları ve çözüm arka ucunuz toobuild uygulamaları toorun kullanabileceği hello SDK'ları hakkında bilgi için bkz [Azure IOT SDK'ları][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="2fb90-123">For information about hello SDKs that you can use toobuild applications toorun on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="2fb90-124">toocomplete Bu öğretici, gerekir:</span><span class="sxs-lookup"><span data-stu-id="2fb90-124">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="2fb90-125">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="2fb90-125">Java SE 8.</span></span> <br/> <span data-ttu-id="2fb90-126">[Geliştirme ortamınızı hazırlama] [ lnk-dev-setup] açıklar nasıl tooinstall Java Bu öğretici için Windows veya Linux üzerinde.</span><span class="sxs-lookup"><span data-stu-id="2fb90-126">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="2fb90-127">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="2fb90-127">Maven 3.</span></span>  <br/> <span data-ttu-id="2fb90-128">[Geliştirme ortamınızı hazırlama] [ lnk-dev-setup] açıklar nasıl tooinstall [Maven] [ lnk-maven] Windows veya Linux üzerinde Bu öğretici için.</span><span class="sxs-lookup"><span data-stu-id="2fb90-128">[Prepare your development environment][lnk-dev-setup] describes how tooinstall [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="2fb90-129">[Node.js sürümünü 0.10.0 veya üzeri](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="2fb90-129">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="2fb90-130">Tetikleyici doğrudan bir yöntem kullanarak hello cihazda Uzaktan yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="2fb90-130">Trigger a remote reboot on hello device using a direct method</span></span>

<span data-ttu-id="2fb90-131">Bu bölümde, bir Java konsol uygulaması, oluşturun:</span><span class="sxs-lookup"><span data-stu-id="2fb90-131">In this section, you create a Java console app that:</span></span>

1. <span data-ttu-id="2fb90-132">Merhaba sanal cihaz uygulamasında Hello yeniden başlatma doğrudan yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="2fb90-132">Invokes hello reboot direct method in hello simulated device app.</span></span>
1. <span data-ttu-id="2fb90-133">Merhaba yanıt görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2fb90-133">Displays hello response.</span></span>
1. <span data-ttu-id="2fb90-134">Anketler hello hello yeniden başlatma tamamlandıktan sonra hello aygıt toodetermine gönderilen özellikleri bildirdi.</span><span class="sxs-lookup"><span data-stu-id="2fb90-134">Polls hello reported properties sent from hello device toodetermine when hello reboot is complete.</span></span>

<span data-ttu-id="2fb90-135">Bu konsol uygulamasını tooyour IOT hub'a bağlanan tooinvoke hello doğrudan yöntemi ve okuma hello bildirilen özellikleri.</span><span class="sxs-lookup"><span data-stu-id="2fb90-135">This console app connects tooyour IoT Hub tooinvoke hello direct method and read hello reported properties.</span></span>

1. <span data-ttu-id="2fb90-136">DM-get-started adlı boş bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2fb90-136">Create an empty folder called dm-get-started.</span></span>

1. <span data-ttu-id="2fb90-137">Merhaba dm-get-started klasöründe adlı bir Maven projesi oluşturun **tetikleyici yeniden başlatma** komutu, komut isteminde aşağıdaki hello kullanarak.</span><span class="sxs-lookup"><span data-stu-id="2fb90-137">In hello dm-get-started folder, create a Maven project called **trigger-reboot** using hello following command at your command prompt.</span></span> <span data-ttu-id="2fb90-138">Merhaba aşağıdaki tek ve uzun bir komut gösterir:</span><span class="sxs-lookup"><span data-stu-id="2fb90-138">hello following shows a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="2fb90-139">Komut isteminizde toohello tetikleyici yeniden başlatma klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="2fb90-139">At your command prompt, navigate toohello trigger-reboot folder.</span></span>

1. <span data-ttu-id="2fb90-140">Bir metin düzenleyicisi kullanarak hello tetikleyici yeniden başlatma klasöründe hello pom.xml dosyasını açın ve bağımlılık toohello aşağıdaki hello ekleyin **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="2fb90-140">Using a text editor, open hello pom.xml file in hello trigger-reboot folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="2fb90-141">Bu bağımlılık, toouse hello IOT hizmeti istemci paketi, uygulama toocommunicate IOT hub'ınızı ile sağlar:</span><span class="sxs-lookup"><span data-stu-id="2fb90-141">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="2fb90-142">Hello için en son sürümünü denetleyebilir **IOT hizmeti istemcisi** kullanarak [Maven arama][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="2fb90-142">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="2fb90-143">Merhaba aşağıdakileri ekleyin **yapı** düğümünden hello sonraki **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="2fb90-143">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="2fb90-144">Bu yapılandırma, Maven toouse Java 1.8 toobuild hello uygulaması bildirir:</span><span class="sxs-lookup"><span data-stu-id="2fb90-144">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="2fb90-145">Merhaba pom.xml dosyasını kaydedip kapatın.</span><span class="sxs-lookup"><span data-stu-id="2fb90-145">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="2fb90-146">Bir metin düzenleyicisi kullanarak hello trigger-reboot\src\main\java\com\mycompany\app\App.java kaynak dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="2fb90-146">Using a text editor, open hello trigger-reboot\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="2fb90-147">Merhaba aşağıdakileri ekleyin **alma** deyimleri toohello dosyası:</span><span class="sxs-lookup"><span data-stu-id="2fb90-147">Add hello following **import** statements toohello file:</span></span>

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

1. <span data-ttu-id="2fb90-148">Aşağıdaki sınıf düzeyi değişkenleri toohello hello eklemek **uygulama** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="2fb90-148">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="2fb90-149">Değiştir `{youriothubconnectionstring}` hello ettiğiniz, IOT hub bağlantı dizesine sahip *IOT Hub oluşturma* bölümü:</span><span class="sxs-lookup"><span data-stu-id="2fb90-149">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. <span data-ttu-id="2fb90-150">tooimplement hello okuyan bir iş parçacığı özellikleri bildirilen hello cihaz çifti 10 saniyede hello aşağıdakileri ekleyin. iç içe geçmiş sınıf toohello **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="2fb90-150">tooimplement a thread that reads hello reported properties from hello device twin every 10 seconds, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="2fb90-151">tooinvoke hello yeniden başlatma doğrudan yöntemi hello sanal cihazda ekleme kodu toohello aşağıdaki hello **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="2fb90-151">tooinvoke hello reboot direct method on hello simulated device, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="2fb90-152">toostart hello iş parçacığı toopoll Merhaba hello sanal cihaz bildirilen özelliklerinden, kod toohello aşağıdaki hello eklemek **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="2fb90-152">toostart hello thread toopoll hello reported properties from hello simulated device, add hello following code toohello **main** method:</span></span>

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. <span data-ttu-id="2fb90-153">tooenable, toostop hello uygulama kodu toohello aşağıdaki hello eklemek **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="2fb90-153">tooenable you toostop hello app, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. <span data-ttu-id="2fb90-154">Merhaba trigger-reboot\src\main\java\com\mycompany\app\App.java dosyasını kaydedip kapatın.</span><span class="sxs-lookup"><span data-stu-id="2fb90-154">Save and close hello trigger-reboot\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="2fb90-155">Merhaba yapı **tetikleyici yeniden başlatma** arka uç uygulama ve olan hataları düzeltin.</span><span class="sxs-lookup"><span data-stu-id="2fb90-155">Build hello **trigger-reboot** back-end app and correct any errors.</span></span> <span data-ttu-id="2fb90-156">Komut isteminizde toohello tetikleyici yeniden başlatma klasörü ve aşağıdaki komutu çalıştırın hello gidin:</span><span class="sxs-lookup"><span data-stu-id="2fb90-156">At your command prompt, navigate toohello trigger-reboot folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="2fb90-157">Sanal cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="2fb90-157">Create a simulated device app</span></span>

<span data-ttu-id="2fb90-158">Bu bölümde, bir cihaza benzetim bir Java konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2fb90-158">In this section, you create a Java console app that simulates a device.</span></span> <span data-ttu-id="2fb90-159">Merhaba uygulama hello yeniden başlatma doğrudan yöntemi, IOT hub çağrısından dinler ve hemen toothat çağrısı yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="2fb90-159">hello app listens for hello reboot direct method call from your IoT hub and immediately responds toothat call.</span></span> <span data-ttu-id="2fb90-160">Merhaba uygulama sonra uykuya geçme bir süre için bildirilen özelliği toonotify hello kullanmadan önce toosimulate hello yeniden başlatma işlemi **tetikleyici yeniden başlatma** yeniden başlatma hello arka uç uygulama tamamlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="2fb90-160">hello app then sleeps for a while toosimulate hello reboot process before it uses a reported property toonotify hello **trigger-reboot** back-end app that hello reboot is complete.</span></span>

1. <span data-ttu-id="2fb90-161">Merhaba dm-get-started klasöründe adlı bir Maven projesi oluşturun **simulated-device** komutu, komut isteminde aşağıdaki hello kullanarak.</span><span class="sxs-lookup"><span data-stu-id="2fb90-161">In hello dm-get-started folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="2fb90-162">Merhaba, tek ve uzun bir komut verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="2fb90-162">hello following is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="2fb90-163">Komut isteminizde toohello simulated-device klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="2fb90-163">At your command prompt, navigate toohello simulated-device folder.</span></span>

1. <span data-ttu-id="2fb90-164">Bir metin düzenleyicisi kullanarak hello simulated-device klasöründeki hello pom.xml dosyasını açın ve bağımlılık toohello aşağıdaki hello ekleyin **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="2fb90-164">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="2fb90-165">Bu bağımlılık, toouse hello IOT hizmeti istemci paketi, uygulama toocommunicate IOT hub'ınızı ile sağlar:</span><span class="sxs-lookup"><span data-stu-id="2fb90-165">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="2fb90-166">Hello için en son sürümünü denetleyebilir **IOT cihaz istemci** kullanarak [Maven arama][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="2fb90-166">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="2fb90-167">Merhaba aşağıdakileri ekleyin **yapı** düğümünden hello sonraki **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="2fb90-167">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="2fb90-168">Bu yapılandırma, Maven toouse Java 1.8 toobuild hello uygulaması bildirir:</span><span class="sxs-lookup"><span data-stu-id="2fb90-168">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="2fb90-169">Merhaba pom.xml dosyasını kaydedip kapatın.</span><span class="sxs-lookup"><span data-stu-id="2fb90-169">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="2fb90-170">Bir metin düzenleyicisi kullanarak hello simulated-device\src\main\java\com\mycompany\app\App.java kaynak dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="2fb90-170">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="2fb90-171">Merhaba aşağıdakileri ekleyin **alma** deyimleri toohello dosyası:</span><span class="sxs-lookup"><span data-stu-id="2fb90-171">Add hello following **import** statements toohello file:</span></span>

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

1. <span data-ttu-id="2fb90-172">Aşağıdaki sınıf düzeyi değişkenleri toohello hello eklemek **uygulama** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="2fb90-172">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="2fb90-173">Değiştir `{yourdeviceconnectionstring}` hello ettiğiniz hello cihaz bağlantı dizesiyle *bir cihaz kimliği oluşturma* bölümü:</span><span class="sxs-lookup"><span data-stu-id="2fb90-173">Replace `{yourdeviceconnectionstring}` with hello device connection string you noted in hello *Create a device identity* section:</span></span>

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. <span data-ttu-id="2fb90-174">tooimplement doğrudan yöntem durum olayları için bir geri çağırma işleyici ekleme hello aşağıdaki iç içe geçmiş sınıf toohello **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="2fb90-174">tooimplement a callback handler for direct method status events, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="2fb90-175">tooimplement cihaz çifti durum olayları için bir geri çağırma işleyici ekleme hello aşağıdaki iç içe geçmiş sınıf toohello **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="2fb90-175">tooimplement a callback handler for device twin status events, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
        }
    }
    ```

1. <span data-ttu-id="2fb90-176">tooimplement özellik olayları için bir geri çağırma işleyici ekleme hello aşağıdaki iç içe geçmiş sınıf toohello **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="2fb90-176">tooimplement a callback handler for property events, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="2fb90-177">tooimplement iş parçacığı toosimulate hello aygıt yeniden başlatma, ekleme hello aşağıdaki iç içe geçmiş sınıf toohello **uygulama** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="2fb90-177">tooimplement a thread toosimulate hello device reboot, add hello following nested class toohello **App** class.</span></span> <span data-ttu-id="2fb90-178">Merhaba iş parçacığı beş saniye için uyku moduna geçer ve ardından ayarlar hello **lastReboot** özelliği bildirdi:</span><span class="sxs-lookup"><span data-stu-id="2fb90-178">hello thread sleeps for five seconds and then sets hello **lastReboot** reported property:</span></span>

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

1. <span data-ttu-id="2fb90-179">tooimplement hello hello aygıtta doğrudan bir yöntem ekleyin hello aşağıdaki iç içe geçmiş sınıf toohello **uygulama** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="2fb90-179">tooimplement hello direct method on hello device, add hello following nested class toohello **App** class.</span></span> <span data-ttu-id="2fb90-180">Ne zaman hello sanal uygulama alan bir çağrı toohello **yeniden** doğrudan yöntemi, bir bildirim toohello çağıran döndürür ve ardından bir iş parçacığı tooprocess hello başlatır yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="2fb90-180">When hello simulated app receives a call toohello **reboot** direct method, it returns an acknowledgement toohello caller and then starts a thread tooprocess hello reboot:</span></span>

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

1. <span data-ttu-id="2fb90-181">Merhaba Hello imzası değiştirme **ana** yöntemi toothrow hello aşağıdaki özel durumlar:</span><span class="sxs-lookup"><span data-stu-id="2fb90-181">Modify hello signature of hello **main** method toothrow hello following exceptions:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="2fb90-182">tooinstantiate bir **DeviceClient**, kod toohello aşağıdaki hello eklemek **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="2fb90-182">tooinstantiate a **DeviceClient**, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. <span data-ttu-id="2fb90-183">doğrudan yöntem çağrıları için dinleme toostart ekleme kodu toohello aşağıdaki hello **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="2fb90-183">toostart listening for direct method calls, add hello following code toohello **main** method:</span></span>

    ```java
    try
    {
      client.open();
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
      client.startDeviceTwin(new DeviceTwinStatusCallback(), null, new PropertyCallback(), null);
      System.out.println("Subscribed toodirect methods and polling for reported properties. Waiting...");
    }
    catch (Exception e)
    {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="2fb90-184">Merhaba aygıt benzeticisi aşağı tooshut ekleme kodu toohello aşağıdaki hello **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="2fb90-184">tooshut down hello device simulator, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. <span data-ttu-id="2fb90-185">Merhaba simulated-device\src\main\java\com\mycompany\app\App.java dosyasını kaydedip kapatın.</span><span class="sxs-lookup"><span data-stu-id="2fb90-185">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="2fb90-186">Merhaba yapı **simulated-device** arka uç uygulama ve olan hataları düzeltin.</span><span class="sxs-lookup"><span data-stu-id="2fb90-186">Build hello **simulated-device** back-end app and correct any errors.</span></span> <span data-ttu-id="2fb90-187">Komut isteminizde toohello simulated-device klasörüne ve aşağıdaki komutu çalıştırın hello gidin:</span><span class="sxs-lookup"><span data-stu-id="2fb90-187">At your command prompt, navigate toohello simulated-device folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="2fb90-188">Merhaba uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="2fb90-188">Run hello apps</span></span>

<span data-ttu-id="2fb90-189">Hazır toorun hello uygulamaları sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="2fb90-189">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="2fb90-190">Merhaba simulated-device klasöründeki komut isteminde IOT hub'ınızı gelen yeniden başlatma yöntemi çağrıları için dinleme komutu toobegin aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2fb90-190">At a command prompt in hello simulated-device folder, run hello following command toobegin listening for reboot method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IOT Hub'ın benzetimli cihaz uygulama toolisten için yeniden başlatma doğrudan yöntem çağrıları][1]

1. <span data-ttu-id="2fb90-192">Merhaba tetikleyici yeniden başlatma klasöründeki bir komut isteminde komutu toocall hello yeniden başlatma yöntemini sanal Cihazınızı IOT hub'ından aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2fb90-192">At a command prompt in hello trigger-reboot folder, run hello following command toocall hello reboot method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IOT Hub hizmeti uygulama toocall hello yeniden doğrudan yöntemi][2]

1. <span data-ttu-id="2fb90-194">Merhaba sanal cihaz toohello yeniden başlatma doğrudan yöntem çağrısı yanıt verir:</span><span class="sxs-lookup"><span data-stu-id="2fb90-194">hello simulated device responds toohello reboot direct method call:</span></span>

    ![Java IOT hub'ı sanal cihaz uygulamasının toohello doğrudan yöntem çağrısı yanıt verir.][3]

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