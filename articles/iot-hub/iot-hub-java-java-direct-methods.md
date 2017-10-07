---
title: "Azure IOT Hub aaaUse doğrudan yöntemleri (Java) | Microsoft Docs"
description: "Nasıl toouse Azure IOT Hub yöntemleri doğrudan. Java tooimplement doğrudan yöntemi ve hello Java tooimplement hello doğrudan yöntemini çağıran bir hizmet uygulaması için Azure IOT hizmeti SDK'sını içeren sanal cihaz uygulaması için hello Azure IOT cihaz SDK'sını kullanın."
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
ms.openlocfilehash: b6f2f4a64535ab649a3965cd9c5a19bebaf88eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-java"></a><span data-ttu-id="ca417-104">Doğrudan yöntemleri (Java) kullanın</span><span class="sxs-lookup"><span data-stu-id="ca417-104">Use direct methods (Java)</span></span>

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="ca417-105">Bu öğreticide, iki Java konsol uygulamaları oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ca417-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="ca417-106">**Invoke-doğrudan-method**, hello sanal cihaz uygulamasının bir yöntemi çağırır ve hello yanıt görüntüleyen bir Java arka uç uygulaması.</span><span class="sxs-lookup"><span data-stu-id="ca417-106">**invoke-direct-method**, a Java back-end app that calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="ca417-107">**simulated-device**, tooyour IOT hub'ı oluşturduğunuz hello cihaz kimliği ile bağlanan bir cihaza benzetim bir Java uygulaması.</span><span class="sxs-lookup"><span data-stu-id="ca417-107">**simulated-device**, a Java app that simulates a device connecting tooyour IoT hub with hello device identity you create.</span></span> <span data-ttu-id="ca417-108">Bu uygulamayı doğrudan hello arka uçtan çağrılan toohello yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="ca417-108">This app responds toohello direct invoked from hello back end.</span></span>

> [!NOTE]
> <span data-ttu-id="ca417-109">Cihazları ve çözüm arka ucunuz toobuild uygulamaları toorun kullanabileceği hello SDK'ları hakkında bilgi için bkz [Azure IOT SDK'ları][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="ca417-109">For information about hello SDKs that you can use toobuild applications toorun on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="ca417-110">toocomplete Bu öğretici, gerekir:</span><span class="sxs-lookup"><span data-stu-id="ca417-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="ca417-111">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="ca417-111">Java SE 8.</span></span> <br/> <span data-ttu-id="ca417-112">[Geliştirme ortamınızı hazırlama] [ lnk-dev-setup] açıklar nasıl tooinstall Java Bu öğretici için Windows veya Linux üzerinde.</span><span class="sxs-lookup"><span data-stu-id="ca417-112">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="ca417-113">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="ca417-113">Maven 3.</span></span>  <br/> <span data-ttu-id="ca417-114">[Geliştirme ortamınızı hazırlama] [ lnk-dev-setup] açıklar nasıl tooinstall [Maven] [ lnk-maven] Windows veya Linux üzerinde Bu öğretici için.</span><span class="sxs-lookup"><span data-stu-id="ca417-114">[Prepare your development environment][lnk-dev-setup] describes how tooinstall [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="ca417-115">[Node.js sürümünü 0.10.0 veya üzeri](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="ca417-115">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="ca417-116">Sanal cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="ca417-116">Create a simulated device app</span></span>

<span data-ttu-id="ca417-117">Bu bölümde, hello çözüm tarafından arka uç adlı tooa yöntemi yanıt bir Java konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ca417-117">In this section, you create a Java console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="ca417-118">İot-java-doğrudan-method adlı boş bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ca417-118">Create an empty folder called iot-java-direct-method.</span></span>

1. <span data-ttu-id="ca417-119">Merhaba iot-java-doğrudan-method klasöründe adlı bir Maven projesi oluşturun **simulated-device** komutu, komut isteminde aşağıdaki hello kullanarak.</span><span class="sxs-lookup"><span data-stu-id="ca417-119">In hello iot-java-direct-method folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="ca417-120">komutu aşağıdaki hello tek ve uzun bir komut şöyledir:</span><span class="sxs-lookup"><span data-stu-id="ca417-120">hello following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="ca417-121">Komut isteminizde toohello simulated-device klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="ca417-121">At your command prompt, navigate toohello simulated-device folder.</span></span>

1. <span data-ttu-id="ca417-122">Bir metin düzenleyicisi kullanarak, hello simulated-device klasöründeki hello pom.xml dosyasını açın ve aşağıdaki bağımlılıkları toohello hello ekleyin **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="ca417-122">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="ca417-123">Bu bağımlılık, toouse hello IOT cihaz istemci paketi, uygulama toocommunicate IOT hub'ınızı ile sağlar:</span><span class="sxs-lookup"><span data-stu-id="ca417-123">This dependency enables you toouse hello iot-device-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="ca417-124">Hello için en son sürümünü denetleyebilir **IOT cihaz istemci** kullanarak [Maven arama][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="ca417-124">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="ca417-125">Merhaba aşağıdakileri ekleyin **yapı** düğümünden hello sonraki **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="ca417-125">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="ca417-126">Bu yapılandırma, Maven toouse Java 1.8 toobuild hello uygulaması bildirir:</span><span class="sxs-lookup"><span data-stu-id="ca417-126">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="ca417-127">Merhaba pom.xml dosyasını kaydedip kapatın.</span><span class="sxs-lookup"><span data-stu-id="ca417-127">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="ca417-128">Bir metin düzenleyicisi kullanarak hello simulated-device\src\main\java\com\mycompany\app\App.java dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="ca417-128">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="ca417-129">Merhaba aşağıdakileri ekleyin **alma** deyimleri toohello dosyası:</span><span class="sxs-lookup"><span data-stu-id="ca417-129">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="ca417-130">Aşağıdaki sınıf düzeyi değişkenleri toohello hello eklemek **uygulama** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="ca417-130">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="ca417-131">Değiştirme `{youriothubname}` , IOT hub'ı adıyla ve `{yourdevicekey}` hello oluşturulan hello aygıt anahtarı değerine sahip *bir cihaz kimliği oluşturma* bölümü:</span><span class="sxs-lookup"><span data-stu-id="ca417-131">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="ca417-132">Bu örnek uygulama hello kullanan **Protokolü** değişkenini bir **DeviceClient** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="ca417-132">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="ca417-133">Şu anda toouse doğrudan yöntemleri hello MQTT Protokolü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca417-133">Currently, toouse direct methods you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="ca417-134">tooreturn bir durum kodu tooyour IOT hub eklemek hello aşağıdaki iç içe geçmiş sınıf toohello **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="ca417-134">tooreturn a status code tooyour IoT hub, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="ca417-135">toohandle hello doğrudan yöntem çağrılarını hello çözüm arka ucu, gelen ekleme hello aşağıdaki iç içe geçmiş sınıf toohello **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="ca417-135">toohandle hello direct method invocations from hello solution back end, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="ca417-136">toocreate bir **DeviceClient** ve için doğrudan yöntem çağrılarına dinleme, eklemeniz bir **ana** yöntemi toohello **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="ca417-136">toocreate a **DeviceClient** and listen for direct method invocations, add a **main** method toohello **App** class:</span></span>

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
        System.out.println("Subscribed toodirect methods. Waiting...");
      }
      catch (Exception e)
      {
        System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
        client.close();
        System.out.println("Shutting down...");
      }

      System.out.println("Press any key tooexit...");
      Scanner scanner = new Scanner(System.in);
      scanner.nextLine();
      scanner.close();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="ca417-137">Merhaba simulated-device\src\main\java\com\mycompany\app\App.java dosyasını kaydedin ve kapatın</span><span class="sxs-lookup"><span data-stu-id="ca417-137">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="ca417-138">Merhaba yapı **simulated-device** uygulama ve olan hataları düzeltin.</span><span class="sxs-lookup"><span data-stu-id="ca417-138">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="ca417-139">Komut isteminizde toohello simulated-device klasörüne ve aşağıdaki komutu çalıştırın hello gidin:</span><span class="sxs-lookup"><span data-stu-id="ca417-139">At your command prompt, navigate toohello simulated-device folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="ca417-140">Bir cihazda doğrudan bir yöntem çağrısı</span><span class="sxs-lookup"><span data-stu-id="ca417-140">Call a direct method on a device</span></span>

<span data-ttu-id="ca417-141">Bu bölümde, doğrudan bir yöntemi çağırır ve hello yanıt görüntüleyen bir Java konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ca417-141">In this section, you create a Java console app that invokes a direct method and then displays hello response.</span></span> <span data-ttu-id="ca417-142">Bu konsol uygulamasını tooyour IOT hub'ı tooinvoke hello doğrudan yöntemi bağlanır.</span><span class="sxs-lookup"><span data-stu-id="ca417-142">This console app connects tooyour IoT Hub tooinvoke hello direct method.</span></span>

1. <span data-ttu-id="ca417-143">Merhaba iot-java-doğrudan-method klasöründe adlı bir Maven projesi oluşturun **Invoke-doğrudan-method** komutu, komut isteminde aşağıdaki hello kullanarak.</span><span class="sxs-lookup"><span data-stu-id="ca417-143">In hello iot-java-direct-method folder, create a Maven project called **invoke-direct-method** using hello following command at your command prompt.</span></span> <span data-ttu-id="ca417-144">komutu aşağıdaki hello tek ve uzun bir komut şöyledir:</span><span class="sxs-lookup"><span data-stu-id="ca417-144">hello following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="ca417-145">Komut isteminizde toohello Invoke-doğrudan-method klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="ca417-145">At your command prompt, navigate toohello invoke-direct-method folder.</span></span>

1. <span data-ttu-id="ca417-146">Bir metin düzenleyicisi kullanarak hello Invoke-doğrudan-method klasöründe hello pom.xml dosyasını açın ve bağımlılık toohello aşağıdaki hello ekleyin **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="ca417-146">Using a text editor, open hello pom.xml file in hello invoke-direct-method folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="ca417-147">Bu bağımlılık, toouse hello IOT hizmeti istemci paketi, uygulama toocommunicate IOT hub'ınızı ile sağlar:</span><span class="sxs-lookup"><span data-stu-id="ca417-147">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="ca417-148">Hello için en son sürümünü denetleyebilir **IOT hizmeti istemcisi** kullanarak [Maven arama][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="ca417-148">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="ca417-149">Merhaba aşağıdakileri ekleyin **yapı** düğümünden hello sonraki **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="ca417-149">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="ca417-150">Bu yapılandırma, Maven toouse Java 1.8 toobuild hello uygulaması bildirir:</span><span class="sxs-lookup"><span data-stu-id="ca417-150">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="ca417-151">Merhaba pom.xml dosyasını kaydedip kapatın.</span><span class="sxs-lookup"><span data-stu-id="ca417-151">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="ca417-152">Bir metin düzenleyicisi kullanarak hello invoke-direct-method\src\main\java\com\mycompany\app\App.java dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="ca417-152">Using a text editor, open hello invoke-direct-method\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="ca417-153">Merhaba aşağıdakileri ekleyin **alma** deyimleri toohello dosyası:</span><span class="sxs-lookup"><span data-stu-id="ca417-153">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. <span data-ttu-id="ca417-154">Aşağıdaki sınıf düzeyi değişkenleri toohello hello eklemek **uygulama** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="ca417-154">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="ca417-155">Değiştir `{youriothubconnectionstring}` hello ettiğiniz, IOT hub bağlantı dizesine sahip *IOT Hub oluşturma* bölümü:</span><span class="sxs-lookup"><span data-stu-id="ca417-155">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line toobe written";
    ```

1. <span data-ttu-id="ca417-156">Merhaba sanal cihazda tooinvoke hello yöntemi ekleme kodu toohello aşağıdaki hello **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="ca417-156">tooinvoke hello method on hello simulated device, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="ca417-157">Merhaba invoke-direct-method\src\main\java\com\mycompany\app\App.java dosyasını kaydedin ve kapatın</span><span class="sxs-lookup"><span data-stu-id="ca417-157">Save and close hello invoke-direct-method\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="ca417-158">Merhaba yapı **Invoke-doğrudan-method** uygulama ve olan hataları düzeltin.</span><span class="sxs-lookup"><span data-stu-id="ca417-158">Build hello **invoke-direct-method** app and correct any errors.</span></span> <span data-ttu-id="ca417-159">Komut isteminizde toohello Invoke-doğrudan-method klasörü ve aşağıdaki komutu çalıştırın hello gidin:</span><span class="sxs-lookup"><span data-stu-id="ca417-159">At your command prompt, navigate toohello invoke-direct-method folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="ca417-160">Merhaba uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="ca417-160">Run hello apps</span></span>

<span data-ttu-id="ca417-161">Hazır toorun hello konsol uygulamaları sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="ca417-161">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="ca417-162">Merhaba simulated-device klasöründeki komut isteminde IOT hub'ınızı gelen yöntem çağrıları için dinleme komutu toobegin aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ca417-162">At a command prompt in hello simulated-device folder, run hello following command toobegin listening for method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IOT Hub cihaz uygulama toolisten doğrudan yöntem çağrıları için benzetimli][8]

1. <span data-ttu-id="ca417-164">Hello Invoke-doğrudan-method klasöründeki bir komut isteminde IOT hub'ından sanal Cihazınızda bir yöntem komutu toocall aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ca417-164">At a command prompt in hello invoke-direct-method folder, run hello following command toocall a method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IOT Hub hizmeti uygulama toocall doğrudan yöntemi][7]

1. <span data-ttu-id="ca417-166">Merhaba sanal cihaz toohello doğrudan yöntem çağrısı yanıt verir:</span><span class="sxs-lookup"><span data-stu-id="ca417-166">hello simulated device responds toohello direct method call:</span></span>

    ![Java IOT hub'ı sanal cihaz uygulamasının toohello doğrudan yöntem çağrısı yanıt verir.][9]

## <a name="next-steps"></a><span data-ttu-id="ca417-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ca417-168">Next steps</span></span>

<span data-ttu-id="ca417-169">Bu öğreticide hello Azure portalında yeni bir IOT hub yapılandırılmış ve ardından hello IOT hub'ın kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="ca417-169">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="ca417-170">Merhaba bulut tarafından çağrılan bu cihaz kimliğini tooenable benzetimli hello aygıt uygulama tooreact toomethods kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ca417-170">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="ca417-171">Merhaba aygıtta yöntemleri çağırır ve hello yanıt hello aygıttan görüntüleyen bir uygulama da oluşturmuş.</span><span class="sxs-lookup"><span data-stu-id="ca417-171">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span>

<span data-ttu-id="ca417-172">tooexplore diğer IOT senaryolarını bkz [zamanlama işlerini birden çok aygıta][lnk-devguide-jobs].</span><span class="sxs-lookup"><span data-stu-id="ca417-172">tooexplore other IoT scenarios, see [Schedule jobs on multiple devices][lnk-devguide-jobs].</span></span>

<span data-ttu-id="ca417-173">toolearn tooextend birden fazla cihazda IOT çözümü ve zamanlama yöntemi çağırır nasıl hello bkz [zamanlama ve yayın işleri] [ lnk-tutorial-jobs] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="ca417-173">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
