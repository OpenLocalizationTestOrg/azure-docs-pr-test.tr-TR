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
# <a name="get-started-with-device-management-java"></a>Aygıt Yönetimi (Java) ile çalışmaya başlama

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

Bu öğretici şunların nasıl yapıldığını gösterir:

* IOT hub'ınızda bir cihaz kimliği oluşturma ve Hello Azure portal toocreate IOT hub'ı kullanın.
* Bir doğrudan yöntemi tooreboot hello aygıtı uygulayan bir sanal cihaz uygulaması oluşturursunuz. Doğrudan yöntemleri hello buluttan çağrılır.
* IOT hub'ınız aracılığıyla hello sanal cihaz uygulamasında hello yeniden başlatma doğrudan yöntemini çağıran bir uygulama oluşturun. Bu uygulama daha sonra hello yeniden başlatma işlemi tamamlandığında hello aygıt toosee bildirilen özelliklerinden hello izleyiciler.

Bu öğreticinin Hello sonunda, iki Java konsol uygulamaları vardır:

**simulated-device**. Bu uygulama:

* Tooyour IOT hub'ı daha önce oluşturduğunuz hello cihaz kimliği bağlanır.
* Yeniden başlatma doğrudan yöntem çağrısı alır.
* Fiziksel bir yeniden başlatma benzetimini yapar.
* Merhaba son yeniden başlatmadan bildirilen bir özellik aracılığıyla raporları hello zamanı.

**Tetikleyici yeniden başlatma**. Bu uygulama:

* Merhaba sanal cihaz uygulamasının doğrudan bir yöntem çağırır.
* Merhaba yanıt toohello doğrudan yöntem çağrısı Hello sanal aygıt tarafından gönderilen görüntüler
* Güncelleştirilmiş görüntüler hello özellikleri bildirdi.

> [!NOTE]
> Cihazları ve çözüm arka ucunuz toobuild uygulamaları toorun kullanabileceği hello SDK'ları hakkında bilgi için bkz [Azure IOT SDK'ları][lnk-hub-sdks].

toocomplete Bu öğretici, gerekir:

* Java SE 8. <br/> [Geliştirme ortamınızı hazırlama] [ lnk-dev-setup] açıklar nasıl tooinstall Java Bu öğretici için Windows veya Linux üzerinde.
* Maven 3.  <br/> [Geliştirme ortamınızı hazırlama] [ lnk-dev-setup] açıklar nasıl tooinstall [Maven] [ lnk-maven] Windows veya Linux üzerinde Bu öğretici için.
* [Node.js sürümünü 0.10.0 veya üzeri](http://nodejs.org).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>Tetikleyici doğrudan bir yöntem kullanarak hello cihazda Uzaktan yeniden başlatma

Bu bölümde, bir Java konsol uygulaması, oluşturun:

1. Merhaba sanal cihaz uygulamasında Hello yeniden başlatma doğrudan yöntemini çağırır.
1. Merhaba yanıt görüntüler.
1. Anketler hello hello yeniden başlatma tamamlandıktan sonra hello aygıt toodetermine gönderilen özellikleri bildirdi.

Bu konsol uygulamasını tooyour IOT hub'a bağlanan tooinvoke hello doğrudan yöntemi ve okuma hello bildirilen özellikleri.

1. DM-get-started adlı boş bir klasör oluşturun.

1. Merhaba dm-get-started klasöründe adlı bir Maven projesi oluşturun **tetikleyici yeniden başlatma** komutu, komut isteminde aşağıdaki hello kullanarak. Merhaba aşağıdaki tek ve uzun bir komut gösterir:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Komut isteminizde toohello tetikleyici yeniden başlatma klasörüne gidin.

1. Bir metin düzenleyicisi kullanarak hello tetikleyici yeniden başlatma klasöründe hello pom.xml dosyasını açın ve bağımlılık toohello aşağıdaki hello ekleyin **bağımlılıkları** düğümü. Bu bağımlılık, toouse hello IOT hizmeti istemci paketi, uygulama toocommunicate IOT hub'ınızı ile sağlar:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > Hello için en son sürümünü denetleyebilir **IOT hizmeti istemcisi** kullanarak [Maven arama][lnk-maven-service-search].

1. Merhaba aşağıdakileri ekleyin **yapı** düğümünden hello sonraki **bağımlılıkları** düğümü. Bu yapılandırma, Maven toouse Java 1.8 toobuild hello uygulaması bildirir:

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

1. Merhaba pom.xml dosyasını kaydedip kapatın.

1. Bir metin düzenleyicisi kullanarak hello trigger-reboot\src\main\java\com\mycompany\app\App.java kaynak dosyasını açın.

1. Merhaba aşağıdakileri ekleyin **alma** deyimleri toohello dosyası:

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

1. Aşağıdaki sınıf düzeyi değişkenleri toohello hello eklemek **uygulama** sınıfı. Değiştir `{youriothubconnectionstring}` hello ettiğiniz, IOT hub bağlantı dizesine sahip *IOT Hub oluşturma* bölümü:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. tooimplement hello okuyan bir iş parçacığı özellikleri bildirilen hello cihaz çifti 10 saniyede hello aşağıdakileri ekleyin. iç içe geçmiş sınıf toohello **uygulama** sınıfı:

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

1. tooinvoke hello yeniden başlatma doğrudan yöntemi hello sanal cihazda ekleme kodu toohello aşağıdaki hello **ana** yöntemi:

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

1. toostart hello iş parçacığı toopoll Merhaba hello sanal cihaz bildirilen özelliklerinden, kod toohello aşağıdaki hello eklemek **ana** yöntemi:

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. tooenable, toostop hello uygulama kodu toohello aşağıdaki hello eklemek **ana** yöntemi:

    ```java
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. Merhaba trigger-reboot\src\main\java\com\mycompany\app\App.java dosyasını kaydedip kapatın.

1. Merhaba yapı **tetikleyici yeniden başlatma** arka uç uygulama ve olan hataları düzeltin. Komut isteminizde toohello tetikleyici yeniden başlatma klasörü ve aşağıdaki komutu çalıştırın hello gidin:

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a>Sanal cihaz uygulaması oluşturma

Bu bölümde, bir cihaza benzetim bir Java konsol uygulaması oluşturun. Merhaba uygulama hello yeniden başlatma doğrudan yöntemi, IOT hub çağrısından dinler ve hemen toothat çağrısı yanıt verir. Merhaba uygulama sonra uykuya geçme bir süre için bildirilen özelliği toonotify hello kullanmadan önce toosimulate hello yeniden başlatma işlemi **tetikleyici yeniden başlatma** yeniden başlatma hello arka uç uygulama tamamlanmıştır.

1. Merhaba dm-get-started klasöründe adlı bir Maven projesi oluşturun **simulated-device** komutu, komut isteminde aşağıdaki hello kullanarak. Merhaba, tek ve uzun bir komut verilmiştir:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Komut isteminizde toohello simulated-device klasörüne gidin.

1. Bir metin düzenleyicisi kullanarak hello simulated-device klasöründeki hello pom.xml dosyasını açın ve bağımlılık toohello aşağıdaki hello ekleyin **bağımlılıkları** düğümü. Bu bağımlılık, toouse hello IOT hizmeti istemci paketi, uygulama toocommunicate IOT hub'ınızı ile sağlar:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > Hello için en son sürümünü denetleyebilir **IOT cihaz istemci** kullanarak [Maven arama][lnk-maven-device-search].

1. Merhaba aşağıdakileri ekleyin **yapı** düğümünden hello sonraki **bağımlılıkları** düğümü. Bu yapılandırma, Maven toouse Java 1.8 toobuild hello uygulaması bildirir:

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

1. Merhaba pom.xml dosyasını kaydedip kapatın.

1. Bir metin düzenleyicisi kullanarak hello simulated-device\src\main\java\com\mycompany\app\App.java kaynak dosyasını açın.

1. Merhaba aşağıdakileri ekleyin **alma** deyimleri toohello dosyası:

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

1. Aşağıdaki sınıf düzeyi değişkenleri toohello hello eklemek **uygulama** sınıfı. Değiştir `{yourdeviceconnectionstring}` hello ettiğiniz hello cihaz bağlantı dizesiyle *bir cihaz kimliği oluşturma* bölümü:

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. tooimplement doğrudan yöntem durum olayları için bir geri çağırma işleyici ekleme hello aşağıdaki iç içe geçmiş sınıf toohello **uygulama** sınıfı:

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. tooimplement cihaz çifti durum olayları için bir geri çağırma işleyici ekleme hello aşağıdaki iç içe geçmiş sınıf toohello **uygulama** sınıfı:

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
        }
    }
    ```

1. tooimplement özellik olayları için bir geri çağırma işleyici ekleme hello aşağıdaki iç içe geçmiş sınıf toohello **uygulama** sınıfı:

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

1. tooimplement iş parçacığı toosimulate hello aygıt yeniden başlatma, ekleme hello aşağıdaki iç içe geçmiş sınıf toohello **uygulama** sınıfı. Merhaba iş parçacığı beş saniye için uyku moduna geçer ve ardından ayarlar hello **lastReboot** özelliği bildirdi:

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

1. tooimplement hello hello aygıtta doğrudan bir yöntem ekleyin hello aşağıdaki iç içe geçmiş sınıf toohello **uygulama** sınıfı. Ne zaman hello sanal uygulama alan bir çağrı toohello **yeniden** doğrudan yöntemi, bir bildirim toohello çağıran döndürür ve ardından bir iş parçacığı tooprocess hello başlatır yeniden başlatın:

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

1. Merhaba Hello imzası değiştirme **ana** yöntemi toothrow hello aşağıdaki özel durumlar:

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. tooinstantiate bir **DeviceClient**, kod toohello aşağıdaki hello eklemek **ana** yöntemi:

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. doğrudan yöntem çağrıları için dinleme toostart ekleme kodu toohello aşağıdaki hello **ana** yöntemi:

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

1. Merhaba aygıt benzeticisi aşağı tooshut ekleme kodu toohello aşağıdaki hello **ana** yöntemi:

    ```java
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. Merhaba simulated-device\src\main\java\com\mycompany\app\App.java dosyasını kaydedip kapatın.

1. Merhaba yapı **simulated-device** arka uç uygulama ve olan hataları düzeltin. Komut isteminizde toohello simulated-device klasörüne ve aşağıdaki komutu çalıştırın hello gidin:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Merhaba uygulamaları çalıştırma

Hazır toorun hello uygulamaları sunulmuştur.

1. Merhaba simulated-device klasöründeki komut isteminde IOT hub'ınızı gelen yeniden başlatma yöntemi çağrıları için dinleme komutu toobegin aşağıdaki hello çalıştırın:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IOT Hub'ın benzetimli cihaz uygulama toolisten için yeniden başlatma doğrudan yöntem çağrıları][1]

1. Merhaba tetikleyici yeniden başlatma klasöründeki bir komut isteminde komutu toocall hello yeniden başlatma yöntemini sanal Cihazınızı IOT hub'ından aşağıdaki hello çalıştırın:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IOT Hub hizmeti uygulama toocall hello yeniden doğrudan yöntemi][2]

1. Merhaba sanal cihaz toohello yeniden başlatma doğrudan yöntem çağrısı yanıt verir:

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