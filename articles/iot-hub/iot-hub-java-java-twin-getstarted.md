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
# <a name="get-started-with-device-twins-java"></a>Cihaz çiftlerini (Java) ile çalışmaya başlama

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

Bu öğreticide, iki Java konsol uygulamaları oluşturun:

* **ekleme-etiketleri-query**, etiketleri ekler ve cihaz çiftlerini sorgular bir Java arka uç uygulaması.
* **simulated-device**, bir Java cihaz uygulaması, bildirilen bir özellik kullanarak kendi bağlantı koşulunun tooyour IOT hub ve raporları bağlanır.

> [!NOTE]
> Merhaba makale [Azure IOT SDK'ları](iot-hub-devguide-sdks.md) toobuild kullanabileceğiniz hello Azure IOT SDK'ları hakkında bilgi sağlayan cihaz ve arka uç uygulamalar.

toocomplete Bu öğretici, gerekir:

* Merhaba son [Java SE Geliştirme Seti 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Etkin bir Azure hesabı. (Bir hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz bir hesap](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Program aracılığıyla toocreate hello cihaz kimliği tercih ederseniz, hello hello ilgili bölümünü okuyun [Java kullanarak aygıt tooyour IOT hub'ınıza bağlanmak](iot-hub-java-java-getstarted.md#create-a-device-identity) makalesi.

## <a name="create-hello-service-app"></a>Merhaba service uygulaması oluşturma

Bu bölümde IOT Hub'ındaki etiketi toohello cihaz çifti ile ilişkili olarak, konum meta veri ekleyen bir Java uygulaması oluşturma **myDeviceId**. Merhaba uygulama ilk IOT hub'ın hello ABD bulunan aygıtları ve ardından bir cep telefonu ağ bağlantısı rapor cihazlar için sorgular.

1. Geliştirme makinenizde adlı boş bir klasör oluşturun `iot-java-twin-getstarted`.

1. Merhaba, `iot-java-twin-getstarted` klasörünü adlı bir Maven projesi oluşturun **ekleme-etiketleri-query** komutu, komut isteminde aşağıdaki hello kullanarak. Bunun tek ve uzun bir komut olduğunu unutmayın:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Komut isteminizde toohello gidin `add-tags-query` klasör.

1. Bir metin düzenleyicisi kullanarak hello açın `pom.xml` hello dosyasında `add-tags-query` klasörü ve bağımlılık toohello aşağıdaki hello ekleyin **bağımlılıkları** düğümü. Bu bağımlılık toouse hello etkinleştirir **IOT hizmeti istemcisi** , uygulama toocommunicate IOT hub'ınızı ile paketinde:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > Hello için en son sürümünü denetleyebilir **IOT hizmeti istemcisi** kullanarak [Maven arama](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).

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

1. Kaydet ve Kapat hello `pom.xml` dosya.

1. Bir metin düzenleyicisi kullanarak hello açın `add-tags-query\src\main\java\com\mycompany\app\App.java` dosya.

1. Merhaba aşağıdakileri ekleyin **alma** deyimleri toohello dosyası:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. Aşağıdaki sınıf düzeyi değişkenleri toohello hello eklemek **uygulama** sınıfı. Değiştir `{youriothubconnectionstring}` hello ettiğiniz, IOT hub bağlantı dizesine sahip *IOT Hub oluşturma* bölümü:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. Güncelleştirme hello **ana** yöntemi imza tooinclude hello aşağıdaki `throws` yan tümcesi:

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. Aşağıdaki kodu toohello hello eklemek **ana** yöntemi toocreate hello **DeviceTwin** ve **DeviceTwinDevice** nesneleri. Merhaba **DeviceTwin** nesne IOT hub'ınızı ile Merhaba iletişim işler. Merhaba **DeviceTwinDevice** nesne özelliklerini ve etiketler ile Merhaba cihaz çifti temsil eder:

    ```java
    // Get hello DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. Merhaba aşağıdakileri ekleyin `try/catch` toohello engelleme **ana** yöntemi:

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. tooupdate hello **bölge** ve **tesis** cihaz çifti etiketler, cihaz çiftine ekleme hello kodda aşağıdaki hello `try` engelle:

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

1. tooquery hello cihaz çiftlerini IOT hub'ındaki ekleme kodu toohello aşağıdaki hello `try` hello önceki adımda eklediğiniz kodun hello bloğu. Merhaba kod iki sorguları çalıştırır. Her sorgu en fazla 100 cihazları döndürür:

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

1. Kaydet ve Kapat hello `add-tags-query\src\main\java\com\mycompany\app\App.java` dosyası

1. Merhaba yapı **ekleme-etiketleri-query** uygulama ve olan hataları düzeltin. Komut isteminizde toohello gidin `add-tags-query` klasörü ve aşağıdaki komutu çalıştırın hello:

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a>Cihaz uygulaması oluşturma

Bu bölümde, tooIoT Hub gönderilen bir bildirilen özelliği değerini ayarlayan bir Java konsol uygulaması oluşturun.

1. Merhaba, `iot-java-twin-getstarted` klasörünü adlı bir Maven projesi oluşturun **simulated-device** komutu, komut isteminde aşağıdaki hello kullanarak. Bunun tek ve uzun bir komut olduğunu unutmayın:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Komut isteminizde toohello gidin `simulated-device` klasör.

1. Bir metin düzenleyicisi kullanarak hello açın `pom.xml` hello dosyasında `simulated-device` klasörü ve bağımlılıkları toohello aşağıdaki hello ekleyin **bağımlılıkları** düğümü. Bu bağımlılık toouse hello etkinleştirir **IOT cihaz istemci** , uygulama toocommunicate IOT hub'ınızı ile paketinde:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > Hello için en son sürümünü denetleyebilir **IOT cihaz istemci** kullanarak [Maven arama](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).

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

1. Kaydet ve Kapat hello `pom.xml` dosya.

1. Bir metin düzenleyicisi kullanarak hello açın `simulated-device\src\main\java\com\mycompany\app\App.java` dosya.

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
    ```

    Bu örnek uygulama hello kullanan **Protokolü** değişkenini bir **DeviceClient** nesnesi. Merhaba MQTT protokol kullanmanız gereken şu anda toouse cihaz çifti özellikleri.

1. Aşağıdaki kodu toohello hello eklemek **ana** yöntemi için:
    * Aygıt istemci toocommunicate IOT Hub ile oluşturun.
    * Oluşturma bir **aygıt** nesne toostore hello cihaz çifti özellikleri.

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

1. Aşağıdaki kodu toohello hello eklemek **ana** yöntemi toocreate bir **connectivityType** özelliği bildirilen ve tooIoT Hub gönderin:

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

1. Kod toohello hello sonuna aşağıdaki hello eklemek **ana** yöntemi. Merhaba bekleyen **Enter** anahtar IOT hub'ı tooreport hello hello aygıt çifti işlemleri durumunu süredir sağlar:

    ```java
    System.out.println("Press any key tooexit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. Kaydet ve Kapat hello `simulated-device\src\main\java\com\mycompany\app\App.java` dosya.

1. Merhaba yapı **simulated-device** uygulama ve olan hataları düzeltin. Komut isteminizde toohello gidin `simulated-device` klasörü ve aşağıdaki komutu çalıştırın hello:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Merhaba uygulamaları çalıştırma

Hazır toorun hello konsol uygulamaları sunulmuştur.

1. Bir komut isteminde hello `add-tags-query` klasörüne komutu toorun hello aşağıdaki Merhaba, **ekleme-etiketleri-query** service uygulaması:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IOT Hub hizmeti uygulama tooupdate değerleri etiketi ve cihaz sorguları çalıştırma](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    Merhaba görebilirsiniz **tesis** ve **bölge** etiketleri toohello cihaz çifti eklendi. Cihazınızı Hello ilk sorgunun döndürdüğü ancak hello ikinci desteklemez.

1. Bir komut isteminde hello `simulated-device` klasörüne komutu tooadd hello aşağıdaki Merhaba, **connectivityType** özelliği toohello cihaz çifti bildirdi:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Merhaba aygıt istemci ekler hello ** connectivityType ** bildirilen özelliği](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. Bir komut isteminde hello `add-tags-query` komutu toorun hello aşağıdaki hello Çalıştır klasörü **ekleme-etiketleri-query** service uygulaması ikinci kez:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IOT Hub hizmeti uygulama tooupdate değerleri etiketi ve cihaz sorguları çalıştırma](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    Cihazınızı hello gönderdi artık **connectivityType** özelliği tooIoT Hub'ı hello ikinci sorguyu Cihazınızı döndürür.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide hello Azure portalında yeni bir IOT hub yapılandırılmış ve ardından hello IOT hub'ın kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz. Cihaz meta verilerini bir arka uç uygulamadan etiketler eklendi ve bir cihaz uygulama tooreport aygıt bağlantı bilgilerini hello cihaz çiftine yazıldı. Ayrıca, nasıl tooquery hello hello SQL benzeri IOT hub'ı sorgu dili kullanarak cihaz çifti bilgileri öğrendiniz.

Kaynakları toolearn nasıl aşağıdaki kullanım hello için:

* Merhaba aygıtlarla telemetri gönderen [IOT Hub ile çalışmaya başlama](iot-hub-java-java-getstarted.md) Öğreticisi.
* Merhaba ile etkileşimli olarak (örneğin, kullanıcı tarafından denetlenen bir uygulamadan fan etkinleştirdikten) cihazları denetleme [doğrudan yöntemleri kullanın](iot-hub-java-java-direct-methods.md) Öğreticisi.

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
