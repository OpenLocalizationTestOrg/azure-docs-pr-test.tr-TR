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
# <a name="use-direct-methods-java"></a>Doğrudan yöntemleri (Java) kullanın

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

Bu öğreticide, iki Java konsol uygulamaları oluşturun:

* **Invoke-doğrudan-method**, hello sanal cihaz uygulamasının bir yöntemi çağırır ve hello yanıt görüntüleyen bir Java arka uç uygulaması.
* **simulated-device**, tooyour IOT hub'ı oluşturduğunuz hello cihaz kimliği ile bağlanan bir cihaza benzetim bir Java uygulaması. Bu uygulamayı doğrudan hello arka uçtan çağrılan toohello yanıt verir.

> [!NOTE]
> Cihazları ve çözüm arka ucunuz toobuild uygulamaları toorun kullanabileceği hello SDK'ları hakkında bilgi için bkz [Azure IOT SDK'ları][lnk-hub-sdks].

toocomplete Bu öğretici, gerekir:

* Java SE 8. <br/> [Geliştirme ortamınızı hazırlama] [ lnk-dev-setup] açıklar nasıl tooinstall Java Bu öğretici için Windows veya Linux üzerinde.
* Maven 3.  <br/> [Geliştirme ortamınızı hazırlama] [ lnk-dev-setup] açıklar nasıl tooinstall [Maven] [ lnk-maven] Windows veya Linux üzerinde Bu öğretici için.
* [Node.js sürümünü 0.10.0 veya üzeri](http://nodejs.org).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Sanal cihaz uygulaması oluşturma

Bu bölümde, hello çözüm tarafından arka uç adlı tooa yöntemi yanıt bir Java konsol uygulaması oluşturun.

1. İot-java-doğrudan-method adlı boş bir klasör oluşturun.

1. Merhaba iot-java-doğrudan-method klasöründe adlı bir Maven projesi oluşturun **simulated-device** komutu, komut isteminde aşağıdaki hello kullanarak. komutu aşağıdaki hello tek ve uzun bir komut şöyledir:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Komut isteminizde toohello simulated-device klasörüne gidin.

1. Bir metin düzenleyicisi kullanarak, hello simulated-device klasöründeki hello pom.xml dosyasını açın ve aşağıdaki bağımlılıkları toohello hello ekleyin **bağımlılıkları** düğümü. Bu bağımlılık, toouse hello IOT cihaz istemci paketi, uygulama toocommunicate IOT hub'ınızı ile sağlar:

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

1. Bir metin düzenleyicisi kullanarak hello simulated-device\src\main\java\com\mycompany\app\App.java dosyasını açın.

1. Merhaba aşağıdakileri ekleyin **alma** deyimleri toohello dosyası:

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. Aşağıdaki sınıf düzeyi değişkenleri toohello hello eklemek **uygulama** sınıfı. Değiştirme `{youriothubname}` , IOT hub'ı adıyla ve `{yourdevicekey}` hello oluşturulan hello aygıt anahtarı değerine sahip *bir cihaz kimliği oluşturma* bölümü:

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    Bu örnek uygulama hello kullanan **Protokolü** değişkenini bir **DeviceClient** nesnesi. Şu anda toouse doğrudan yöntemleri hello MQTT Protokolü kullanmanız gerekir.

1. tooreturn bir durum kodu tooyour IOT hub eklemek hello aşağıdaki iç içe geçmiş sınıf toohello **uygulama** sınıfı:

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. toohandle hello doğrudan yöntem çağrılarını hello çözüm arka ucu, gelen ekleme hello aşağıdaki iç içe geçmiş sınıf toohello **uygulama** sınıfı:

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

1. toocreate bir **DeviceClient** ve için doğrudan yöntem çağrılarına dinleme, eklemeniz bir **ana** yöntemi toohello **uygulama** sınıfı:

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

1. Merhaba simulated-device\src\main\java\com\mycompany\app\App.java dosyasını kaydedin ve kapatın

1. Merhaba yapı **simulated-device** uygulama ve olan hataları düzeltin. Komut isteminizde toohello simulated-device klasörüne ve aşağıdaki komutu çalıştırın hello gidin:

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a>Bir cihazda doğrudan bir yöntem çağrısı

Bu bölümde, doğrudan bir yöntemi çağırır ve hello yanıt görüntüleyen bir Java konsol uygulaması oluşturun. Bu konsol uygulamasını tooyour IOT hub'ı tooinvoke hello doğrudan yöntemi bağlanır.

1. Merhaba iot-java-doğrudan-method klasöründe adlı bir Maven projesi oluşturun **Invoke-doğrudan-method** komutu, komut isteminde aşağıdaki hello kullanarak. komutu aşağıdaki hello tek ve uzun bir komut şöyledir:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Komut isteminizde toohello Invoke-doğrudan-method klasörüne gidin.

1. Bir metin düzenleyicisi kullanarak hello Invoke-doğrudan-method klasöründe hello pom.xml dosyasını açın ve bağımlılık toohello aşağıdaki hello ekleyin **bağımlılıkları** düğümü. Bu bağımlılık, toouse hello IOT hizmeti istemci paketi, uygulama toocommunicate IOT hub'ınızı ile sağlar:

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

1. Bir metin düzenleyicisi kullanarak hello invoke-direct-method\src\main\java\com\mycompany\app\App.java dosyasını açın.

1. Merhaba aşağıdakileri ekleyin **alma** deyimleri toohello dosyası:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. Aşağıdaki sınıf düzeyi değişkenleri toohello hello eklemek **uygulama** sınıfı. Değiştir `{youriothubconnectionstring}` hello ettiğiniz, IOT hub bağlantı dizesine sahip *IOT Hub oluşturma* bölümü:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line toobe written";
    ```

1. Merhaba sanal cihazda tooinvoke hello yöntemi ekleme kodu toohello aşağıdaki hello **ana** yöntemi:

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

1. Merhaba invoke-direct-method\src\main\java\com\mycompany\app\App.java dosyasını kaydedin ve kapatın

1. Merhaba yapı **Invoke-doğrudan-method** uygulama ve olan hataları düzeltin. Komut isteminizde toohello Invoke-doğrudan-method klasörü ve aşağıdaki komutu çalıştırın hello gidin:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Merhaba uygulamaları çalıştırma

Hazır toorun hello konsol uygulamaları sunulmuştur.

1. Merhaba simulated-device klasöründeki komut isteminde IOT hub'ınızı gelen yöntem çağrıları için dinleme komutu toobegin aşağıdaki hello çalıştırın:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IOT Hub cihaz uygulama toolisten doğrudan yöntem çağrıları için benzetimli][8]

1. Hello Invoke-doğrudan-method klasöründeki bir komut isteminde IOT hub'ından sanal Cihazınızda bir yöntem komutu toocall aşağıdaki hello çalıştırın:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IOT Hub hizmeti uygulama toocall doğrudan yöntemi][7]

1. Merhaba sanal cihaz toohello doğrudan yöntem çağrısı yanıt verir:

    ![Java IOT hub'ı sanal cihaz uygulamasının toohello doğrudan yöntem çağrısı yanıt verir.][9]

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide hello Azure portalında yeni bir IOT hub yapılandırılmış ve ardından hello IOT hub'ın kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz. Merhaba bulut tarafından çağrılan bu cihaz kimliğini tooenable benzetimli hello aygıt uygulama tooreact toomethods kullanılır. Merhaba aygıtta yöntemleri çağırır ve hello yanıt hello aygıttan görüntüleyen bir uygulama da oluşturmuş.

tooexplore diğer IOT senaryolarını bkz [zamanlama işlerini birden çok aygıta][lnk-devguide-jobs].

toolearn tooextend birden fazla cihazda IOT çözümü ve zamanlama yöntemi çağırır nasıl hello bkz [zamanlama ve yayın işleri] [ lnk-tutorial-jobs] Öğreticisi.

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
