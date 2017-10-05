---
title: "Azure IOT hub'ı doğrudan yöntemleri (Java) kullanın | Microsoft Docs"
description: "Azure IOT hub'ı doğrudan yöntemlerinin nasıl kullanılacağını. Doğrudan bir yöntem ve Azure IOT hizmeti doğrudan yöntemini çağıran bir hizmet uygulaması uygulamak için Java SDK'sını içeren bir sanal cihaz uygulamasının uygulamak için Azure IOT cihaz SDK'sı Java için kullanın."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 6243a1a8cc971c53c797182b2beb6f594d2ac5f7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="use-direct-methods-java"></a><span data-ttu-id="8f2a7-104">Doğrudan yöntemleri (Java) kullanın</span><span class="sxs-lookup"><span data-stu-id="8f2a7-104">Use direct methods (Java)</span></span>

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="8f2a7-105">Bu öğreticide, iki Java konsol uygulamaları oluşturun:</span><span class="sxs-lookup"><span data-stu-id="8f2a7-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="8f2a7-106">**Invoke-doğrudan-method**, sanal cihaz uygulamasının bir yöntemi çağırır ve yanıt görüntüleyen bir Java arka uç uygulaması.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-106">**invoke-direct-method**, a Java back-end app that calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="8f2a7-107">**simulated-device**, oluşturduğunuz cihaz kimliğiyle IOT hub'ınıza bağlanan bir cihaza benzetim bir Java uygulaması.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-107">**simulated-device**, a Java app that simulates a device connecting to your IoT hub with the device identity you create.</span></span> <span data-ttu-id="8f2a7-108">Bu uygulama arka uçtan çağrılan doğrudan yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-108">This app responds to the direct invoked from the back end.</span></span>

> [!NOTE]
> <span data-ttu-id="8f2a7-109">Aygıtları ve çözüm arka ucunuz çalıştırmak için uygulamalar oluşturmak için kullanabileceğiniz SDK'ları hakkında daha fazla bilgi için bkz: [Azure IOT SDK'ları][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="8f2a7-109">For information about the SDKs that you can use to build applications to run on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="8f2a7-110">Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="8f2a7-110">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="8f2a7-111">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-111">Java SE 8.</span></span> <br/> <span data-ttu-id="8f2a7-112">[Geliştirme ortamınızı hazırlama][lnk-dev-setup], bu öğretici için Java'nın Windows veya Linux'ta nasıl yükleneceğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-112">[Prepare your development environment][lnk-dev-setup] describes how to install Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="8f2a7-113">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-113">Maven 3.</span></span>  <br/> <span data-ttu-id="8f2a7-114">[Geliştirme ortamınızı hazırlama][lnk-dev-setup], bu öğretici için [Maven][lnk-maven]'ın Windows veya Linux'ta nasıl yükleneceğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-114">[Prepare your development environment][lnk-dev-setup] describes how to install [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="8f2a7-115">[Node.js sürümünü 0.10.0 veya üzeri](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="8f2a7-115">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="8f2a7-116">Sanal cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="8f2a7-116">Create a simulated device app</span></span>

<span data-ttu-id="8f2a7-117">Bu bölümde, çözüm tarafından arka uç olarak adlandırılan bir yönteme yanıt bir Java konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-117">In this section, you create a Java console app that responds to a method called by the solution back end.</span></span>

1. <span data-ttu-id="8f2a7-118">İot-java-doğrudan-method adlı boş bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-118">Create an empty folder called iot-java-direct-method.</span></span>

1. <span data-ttu-id="8f2a7-119">İot-java-doğrudan-method klasöründe adlı bir Maven projesi oluşturun **simulated-device** , komut isteminde aşağıdaki komutu kullanarak.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-119">In the iot-java-direct-method folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="8f2a7-120">Aşağıdaki komut tek ve uzun bir komut şöyledir:</span><span class="sxs-lookup"><span data-stu-id="8f2a7-120">The following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="8f2a7-121">Komut isteminizde simulated-device klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-121">At your command prompt, navigate to the simulated-device folder.</span></span>

1. <span data-ttu-id="8f2a7-122">Bir metin düzenleyicisi kullanarak simulated-device klasöründeki pom.xml dosyasını açın ve aşağıdaki bağımlılıkları **bağımlılıklar** düğümüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-122">Using a text editor, open the pom.xml file in the simulated-device folder and add the following dependencies to the **dependencies** node.</span></span> <span data-ttu-id="8f2a7-123">Bu bağımlılık, IOT hub ile iletişim kurmak için uygulamanızda IOT cihaz istemci paketini kullanmanıza olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="8f2a7-123">This dependency enables you to use the iot-device-client package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="8f2a7-124">[Maven arama][lnk-maven-device-search] kullanarak en yeni **iot-device-client** sürümünü kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-124">You can check for the latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="8f2a7-125">Aşağıdakileri ekleyin **yapı** düğümünden sonraki **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-125">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="8f2a7-126">Bu yapılandırma, uygulamanızı oluşturmak için Java 1.8 kullanmak için Maven bildirir:</span><span class="sxs-lookup"><span data-stu-id="8f2a7-126">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="8f2a7-127">pom.xml dosyasını kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-127">Save and close the pom.xml file.</span></span>

1. <span data-ttu-id="8f2a7-128">Bir metin düzenleyicisi kullanarak simulated-device\src\main\java\com\mycompany\app\App.java dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-128">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="8f2a7-129">Aşağıdaki **içeri aktarma** deyimlerini dosyaya ekleyin:</span><span class="sxs-lookup"><span data-stu-id="8f2a7-129">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="8f2a7-130">Aşağıdaki sınıf düzeyi değişkenleri **App** sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-130">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="8f2a7-131">Değiştirme `{youriothubname}` , IOT hub'ı adıyla ve `{yourdevicekey}` içinde oluşturulan cihaz anahtarla değeri *bir cihaz kimliği oluşturma* bölümü:</span><span class="sxs-lookup"><span data-stu-id="8f2a7-131">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with the device key value you generated in the *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="8f2a7-132">Bu örnek uygulama, bir **DeviceClient** nesnesi örneğini oluşturduğunda **prokotol** değişkenini kullanır.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-132">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="8f2a7-133">Şu anda, doğrudan yöntemlerini kullanmayı MQTT Protokolü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-133">Currently, to use direct methods you must use the MQTT protocol.</span></span>

1. <span data-ttu-id="8f2a7-134">Bir durum kodu IOT hub'ınıza döndürmek için aşağıdaki iç içe geçmiş sınıf ekleme **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="8f2a7-134">To return a status code to your IoT hub, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded to device method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="8f2a7-135">Çözüm arka uçtan doğrudan yöntem çağrılarını işlemek için aşağıdaki iç içe geçmiş sınıf ekleme **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="8f2a7-135">To handle the direct method invocations from the solution back end, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "writeLine" :
          {
            int status = METHOD_SUCCESS;
            System.out.println(new String((byte[])methodData));
            deviceMethodData = new DeviceMethodData(status, "Executed direct method " + methodName);
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

1. <span data-ttu-id="8f2a7-136">Oluşturmak için bir **DeviceClient** ve için doğrudan yöntem çağrılarına dinleme, eklemeniz bir **ana** yönteme **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="8f2a7-136">To create a **DeviceClient** and listen for direct method invocations, add a **main** method to the **App** class:</span></span>

    ```java
    public static void main(String[] args)
      throws IOException, URISyntaxException
    {
      System.out.println("Starting device sample...");

      DeviceClient client = new DeviceClient(connString, protocol);

      try
      {
        client.open();
        client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
        System.out.println("Subscribed to direct methods. Waiting...");
      }
      catch (Exception e)
      {
        System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
        client.close();
        System.out.println("Shutting down...");
      }

      System.out.println("Press any key to exit...");
      Scanner scanner = new Scanner(System.in);
      scanner.nextLine();
      scanner.close();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="8f2a7-137">Simulated-device\src\main\java\com\mycompany\app\App.java dosyasını kaydedin ve kapatın</span><span class="sxs-lookup"><span data-stu-id="8f2a7-137">Save and close the simulated-device\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="8f2a7-138">Yapı **simulated-device** uygulama ve olan hataları düzeltin.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-138">Build the **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="8f2a7-139">Komut isteminde, simulated-device klasörüne gidin ve aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8f2a7-139">At your command prompt, navigate to the simulated-device folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="8f2a7-140">Bir cihazda doğrudan bir yöntem çağrısı</span><span class="sxs-lookup"><span data-stu-id="8f2a7-140">Call a direct method on a device</span></span>

<span data-ttu-id="8f2a7-141">Bu bölümde, doğrudan bir yöntemi çağırır ve yanıt görüntüleyen bir Java konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-141">In this section, you create a Java console app that invokes a direct method and then displays the response.</span></span> <span data-ttu-id="8f2a7-142">Bu konsol uygulamasını IOT doğrudan yöntemini çağırmak için Hub'ınıza bağlanır.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-142">This console app connects to your IoT Hub to invoke the direct method.</span></span>

1. <span data-ttu-id="8f2a7-143">İot-java-doğrudan-method klasöründe adlı bir Maven projesi oluşturun **Invoke-doğrudan-method** , komut isteminde aşağıdaki komutu kullanarak.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-143">In the iot-java-direct-method folder, create a Maven project called **invoke-direct-method** using the following command at your command prompt.</span></span> <span data-ttu-id="8f2a7-144">Aşağıdaki komut tek ve uzun bir komut şöyledir:</span><span class="sxs-lookup"><span data-stu-id="8f2a7-144">The following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="8f2a7-145">Komut isteminizde Invoke doğrudan yöntemi klasöre gidin.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-145">At your command prompt, navigate to the invoke-direct-method folder.</span></span>

1. <span data-ttu-id="8f2a7-146">Bir metin düzenleyicisi kullanarak Invoke doğrudan yöntemi klasöründeki pom.xml dosyasını açın ve aşağıdaki bağımlılığı eklemek **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-146">Using a text editor, open the pom.xml file in the invoke-direct-method folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="8f2a7-147">Bu bağımlılık, IOT hub ile iletişim kurmak için uygulamanızda IOT-service-client paketini kullanmanıza olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="8f2a7-147">This dependency enables you to use the iot-service-client package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="8f2a7-148">[Maven arama][lnk-maven-service-search] kullanarak en yeni **iot-service-client** sürümünü kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-148">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="8f2a7-149">Aşağıdakileri ekleyin **yapı** düğümünden sonraki **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-149">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="8f2a7-150">Bu yapılandırma, uygulamanızı oluşturmak için Java 1.8 kullanmak için Maven bildirir:</span><span class="sxs-lookup"><span data-stu-id="8f2a7-150">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="8f2a7-151">pom.xml dosyasını kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-151">Save and close the pom.xml file.</span></span>

1. <span data-ttu-id="8f2a7-152">Bir metin düzenleyicisi kullanarak invoke-direct-method\src\main\java\com\mycompany\app\App.java dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-152">Using a text editor, open the invoke-direct-method\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="8f2a7-153">Aşağıdaki **içeri aktarma** deyimlerini dosyaya ekleyin:</span><span class="sxs-lookup"><span data-stu-id="8f2a7-153">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. <span data-ttu-id="8f2a7-154">Aşağıdaki sınıf düzeyi değişkenleri **App** sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-154">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="8f2a7-155">Değiştir `{youriothubconnectionstring}` , not ettiğiniz, IOT hub bağlantı dizesine sahip *IOT Hub oluşturma* bölümü:</span><span class="sxs-lookup"><span data-stu-id="8f2a7-155">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line to be written";
    ```

1. <span data-ttu-id="8f2a7-156">Sanal cihaz için yöntemini çağırmak için aşağıdaki kodu ekleyin **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="8f2a7-156">To invoke the method on the simulated device, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
        System.out.println("Invoke direct method");
        MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, payload);

        if(result == null)
        {
            throw new IOException("Direct method invoke returns null");
        }
        System.out.println("Status=" + result.getStatus());
        System.out.println("Payload=" + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }

    System.out.println("Shutting down sample...");
    ```

1. <span data-ttu-id="8f2a7-157">İnvoke-direct-method\src\main\java\com\mycompany\app\App.java dosyasını kaydedin ve kapatın</span><span class="sxs-lookup"><span data-stu-id="8f2a7-157">Save and close the invoke-direct-method\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="8f2a7-158">Yapı **Invoke-doğrudan-method** uygulama ve olan hataları düzeltin.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-158">Build the **invoke-direct-method** app and correct any errors.</span></span> <span data-ttu-id="8f2a7-159">Komut isteminde, Invoke doğrudan yöntemi klasöre gidin ve aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8f2a7-159">At your command prompt, navigate to the invoke-direct-method folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-the-apps"></a><span data-ttu-id="8f2a7-160">Uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="8f2a7-160">Run the apps</span></span>

<span data-ttu-id="8f2a7-161">Şimdi konsol uygulamaları çalıştırmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-161">You are now ready to run the console apps.</span></span>

1. <span data-ttu-id="8f2a7-162">Simulated-device klasöründeki bir komut isteminde IOT hub'ınızı gelen yöntem çağrıları için dinleme başlamak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8f2a7-162">At a command prompt in the simulated-device folder, run the following command to begin listening for method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IOT hub'ı sanal cihaz uygulamasının doğrudan yöntem çağrılarını dinlemek üzere][8]

1. <span data-ttu-id="8f2a7-164">Invoke doğrudan yöntemi klasöründeki bir komut isteminde IOT hub'ından sanal Cihazınızda bir yöntemi çağırmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8f2a7-164">At a command prompt in the invoke-direct-method folder, run the following command to call a method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Doğrudan bir yöntemi çağırmak için Java IOT Hub hizmeti uygulaması][7]

1. <span data-ttu-id="8f2a7-166">Sanal cihaz doğrudan yöntem çağrısı yanıt verir:</span><span class="sxs-lookup"><span data-stu-id="8f2a7-166">The simulated device responds to the direct method call:</span></span>

    ![Java IOT hub'ı sanal cihaz uygulamasının doğrudan yöntem çağrısı yanıt verir.][9]

## <a name="next-steps"></a><span data-ttu-id="8f2a7-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8f2a7-168">Next steps</span></span>

<span data-ttu-id="8f2a7-169">Bu öğreticide, Azure portalında yeni bir IoT hub'ı yapılandırdınız ve ardından IoT hub'ının kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-169">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="8f2a7-170">Bu cihaz kimliğini bulut tarafından çağrılan yöntemler tepki vermek sanal cihaz uygulamasının sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-170">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="8f2a7-171">Ayrıca aygıtta yöntemleri çağırır ve aygıttan yanıt görüntüleyen bir uygulama oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-171">You also created an app that invokes methods on the device and displays the response from the device.</span></span>

<span data-ttu-id="8f2a7-172">Diğer IOT senaryolarını keşfetmeye bkz [zamanlama işlerini birden çok aygıta][lnk-devguide-jobs].</span><span class="sxs-lookup"><span data-stu-id="8f2a7-172">To explore other IoT scenarios, see [Schedule jobs on multiple devices][lnk-devguide-jobs].</span></span>

<span data-ttu-id="8f2a7-173">Çözüm ve zamanlama yöntemini çağıran birden fazla cihazda, IOT genişletmek öğrenmek için bkz: [zamanlama ve yayın işleri] [ lnk-tutorial-jobs] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="8f2a7-173">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-java-java-direct-methods/invoke-method.png
[8]: ./media/iot-hub-java-java-direct-methods/device-listen.png
[9]: ./media/iot-hub-java-java-direct-methods/device-respond.png

<!-- Links -->
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md
[lnk-maven]: https://maven.apache.org/what-is-maven.html
[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
