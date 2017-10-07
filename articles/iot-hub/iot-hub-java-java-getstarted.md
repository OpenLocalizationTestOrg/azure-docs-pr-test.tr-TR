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
# <a name="connect-your-device-tooyour-iot-hub-using-java"></a>Java kullanarak aygıt tooyour IOT hub'ınıza bağlanın
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

Bu öğretici Hello sonunda üç Java konsol uygulamaları vardır:

* **Create-device-identity**ilişkili güvenlik anahtarı tooconnect cihaz uygulamanız ve bir cihaz kimliği oluşturur.
* **Read-d2c-messages**, cihaz uygulamanız tarafından gönderilen hello telemetri görüntüler.
* **simulated-device**, hangi tooyour IOT hub'ı daha önce oluşturduğunuz hello cihaz kimliği bağlanır ve hello MQTT protokolünü kullanarak her saniye bir telemetri iletisi gönderir.

> [!NOTE]
> Merhaba makale [Azure IOT SDK'ları] [ lnk-hub-sdks] aygıtlar ve çözüm arka ucunuz hem uygulamalar toorun toobuild kullanabileceğiniz hello Azure IOT SDK'ları hakkında bilgi sağlar.

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Merhaba son [Java SE Geliştirme Seti 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) 
* [Maven 3](https://maven.apache.org/install.html) 
* Etkin bir Azure hesabı. (Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

Son adım olarak, hello Not **birincil anahtar** değeri. Ardından **uç noktaları** ve hello **olayları** yerleşik uç noktası. Merhaba üzerinde **özellikleri** dikey penceresinde hello Not **Event Hub ile uyumlu adı** ve hello **Event Hub ile uyumlu uç nokta** adresi. **read-d2c-messages** uygulamanızı oluştururken bu üç değere sahip olmanız gerekir.

![Azure portalı IoT Hub Mesajlaşma dikey penceresi][6]

IoT Hub’ınızı oluşturdunuz. Merhaba IOT Hub ana bilgisayar adı, IOT Hub bağlantı dizesine, IOT hub'ı birincil anahtar, Event Hub ile uyumlu ada ve Event Hub ile uyumlu uç noktası Bu öğretici toocomplete ihtiyacınız var.

## <a name="create-a-device-identity"></a>Cihaz kimliği oluşturma
Bu bölümde, hello kimlik IOT hub'ınızı kayıt defterinde bir cihaz kimliği oluşturan bir Java konsol uygulaması oluşturun. Merhaba kimlik kayıt defterinde girişi olmayan sürece bir aygıt tooIoT hub bağlanamıyor. Daha fazla bilgi için bkz: Merhaba **kimlik kayıt defteri** hello bölümünü [IOT Hub Geliştirici Kılavuzu][lnk-devguide-identity]. Bu konsol uygulamasını çalıştırdığınızda, benzersiz cihaz kimliği oluşturur ve cihaz bulut gönderdiğinde Cihazınızı tooidentify kendisini kullanabileceğiniz anahtar tooIoT Hub iletileri.

1. iot-java-get-started adlı bir boş klasör oluşturun. Merhaba iot-java-get-started klasöründe adlı bir Maven projesi oluşturun **create-device-identity** komutu, komut isteminde aşağıdaki hello kullanarak. Bunun tek ve uzun bir komut olduğunu unutmayın:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. Komut isteminizde toohello create-device-identity klasörüne gidin.

3. Bir metin düzenleyicisi kullanarak hello create-device-identity klasörüne hello pom.xml dosyasını açın ve bağımlılık toohello aşağıdaki hello ekleyin **bağımlılıkları** düğümü. Bu bağımlılık, toouse hello IOT hizmeti istemci paketi uygulamanızda sağlar:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > Hello için en son sürümünü denetleyebilir **IOT hizmeti istemcisi** kullanarak [Maven arama][lnk-maven-service-search].

4. Merhaba pom.xml dosyasını kaydedip kapatın.

5. Bir metin düzenleyicisi kullanarak hello create-device-identity\src\main\java\com\mycompany\app\App.java dosyasını açın.

6. Merhaba aşağıdakileri ekleyin **alma** deyimleri toohello dosyası:

    ```java
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.Device;
    import com.microsoft.azure.sdk.iot.service.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. Aşağıdaki sınıf düzeyi değişkenleri toohello hello eklemek **uygulama** sınıfına **{yourhubconnectionstring}** hello ile daha önce not ettiğiniz değer:

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
    ```
[!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

8. Merhaba Hello imzası değiştirme **ana** yöntemi tooinclude özel durumlar gibi hello:

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```

9. Merhaba hello gövdesi olarak koddan hello eklemek **ana** yöntemi. Bu kod, IoT Hub kimlik kayıt defterinizde zaten yoksa *javadevice* adlı bir cihaz oluşturur. Ardından hello cihaz Kimliğini ve daha sonra ihtiyacınız anahtarını görüntüler:

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

10. Merhaba App.java dosyasını kaydedip kapatın.

11. toobuild hello **create-device-identity** Maven kullanarak uygulama komutu hello hello create-device-identity klasöründeki komut isteminde aşağıdaki hello yürütün:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

12. toorun hello **create-device-identity** Maven kullanarak uygulama komutu hello hello create-device-identity klasöründeki komut isteminde aşağıdaki hello yürütün:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

13. Merhaba Not **cihaz kimliği** ve **aygıt anahtarı**. TooIoT hub'a bir cihaz olarak bağlanan bir uygulama oluşturduğunuzda, bu değerleri daha sonra gerekir.

> [!NOTE]
> Merhaba IOT Hub kimlik kayıt defteri, yalnızca cihaz kimlikleri tooenable güvenli erişim toohello IOT hub'ı depolar. Cihaz kimliklerini ve anahtarlarını toouse güvenlik kimlik bilgileri ve toodisable erişim için tek bir cihaza kullanabilirsiniz bir etkin/devre dışı bayrağını depolar. Uygulamanızın cihaza özgü diğer meta verileri toostore gerekiyorsa, bir uygulamaya özgü depo kullanması gerekir. Daha fazla bilgi için bkz: Merhaba [IOT Hub Geliştirici Kılavuzu][lnk-devguide-identity].

## <a name="receive-device-to-cloud-messages"></a>Cihazdan buluta iletileri alma

Bu bölümde IoT Hub'dan cihaz-bulut iletilerini okuyan bir Java konsol uygulaması oluşturursunuz. IOT hub'ı kullanıma sunan bir [olay hub'ı][lnk-event-hubs-overview]-uyumlu bir uç noktasını tooenable, tooread cihaz bulut iletilerini. tookeep şeyler basit, Bu öğretici, bir yüksek işleme dağıtımına uygun olmayan temel bir okuyucu oluşturur. Merhaba [cihaz-bulut iletileri] [ lnk-process-d2c-tutorial] öğretici gösterir, ölçekli olarak nasıl tooprocess cihaz-bulut iletileri. Merhaba [Event Hubs ile çalışmaya başlama] [ lnk-eventhubs-tutorial] Eğitmeni nasıl tooprocess olay hub'larından iletileri ve geçerli toohello IOT Hub ve Event Hub ile uyumlu uç noktalar hakkında daha fazla bilgi sağlar.

> [!NOTE]
> Merhaba cihaz bulut iletilerini her zaman okumak için Event Hub ile uyumlu uç nokta hello AMQP protokolünü kullanır.

1. Merhaba iot-java-get-started klasöründe oluşturduğunuz hello *bir cihaz kimliği oluşturma* bölümünde, adlı bir Maven projesi oluşturun **read-d2c-messages** komutu, komut isteminde aşağıdaki hello kullanarak. Bunun tek ve uzun bir komut olduğunu unutmayın:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. Komut isteminizde toohello read-d2c-messages klasörüne gidin.

3. Bir metin düzenleyicisi kullanarak hello read-d2c-messages klasörüne hello pom.xml dosyasını açın ve bağımlılık toohello aşağıdaki hello ekleyin **bağımlılıkları** düğümü. Bu bağımlılık toouse hello eventhubs-client paketini, uygulama tooread hello Event Hub ile uyumlu uç noktasından içinde sağlar:

    ```xml
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.13.0</version> 
    </dependency>
    ```

4. Merhaba pom.xml dosyasını kaydedip kapatın.

5. Bir metin düzenleyicisi kullanarak hello read-d2c-messages\src\main\java\com\mycompany\app\App.java dosyasını açın.

6. Merhaba aşağıdakileri ekleyin **alma** deyimleri toohello dosyası:

    ```java
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;
    import com.microsoft.azure.servicebus.*;

    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.function.*;
    ```

7. Aşağıdaki sınıf düzeyi değişken toohello hello eklemek **uygulama** sınıfı. Değiştir **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, ve **{youreventhubcompatiblename}** daha önce not ettiğiniz hello değerlerle:

    ```java
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```

8. Merhaba aşağıdakileri ekleyin **receiveMessages** yöntemi toohello **uygulama** sınıfı. Bu yöntem oluşturur bir **EventHubClient** örnek tooconnect toohello Event Hub ile uyumlu uç nokta ve zaman uyumsuz olarak oluşturan bir **PartitionReceiver** Event Hub'ındaki örneği tooread bölüm. Sürekli döngüye girer ve hello uygulama sonlanana kadar hello ileti ayrıntılarını yazdırır.

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
   > Bu yöntem, böylece Hello alıcı çalışmaya başladıktan sonra hello alıcı yalnızca gönderilen iletileri tooIoT Hub okur hello alıcı oluştururken bir filtre kullanır. Merhaba geçerli iletiler kümesini görebileceğiniz için bu tekniği bir test ortamında kullanışlıdır. Bir üretim ortamında kodunuzun - daha fazla bilgi için tüm karışılama iletileri işlediğinden emin olmak için bkz hello [nasıl tooprocess IOT Hub cihaz bulut iletilerini] [ lnk-process-d2c-tutorial] Öğreticisi.

9. Merhaba Hello imzası değiştirme **ana** yöntemi tooinclude özel durumu aşağıdaki gibi hello:

    ```java
    public static void main( String[] args ) throws IOException
    ```

10. Aşağıdaki kodu toohello hello eklemek **ana** hello yönteminde **uygulama** sınıfı. Bu kod hello iki oluşturur **EventHubClient** ve **PartitionReceiver** örnekleri ve iletilerini işleme bittiğinde tooclose hello uygulama sağlar:

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
    > Bu kod, IOT hub'ınızı hello F1 (ücretsiz) katmanında oluşturduğunuzu varsayar. Ücretsiz IoT hub'ının "0" ve "1" adlı iki bölümü vardır.

11. Merhaba App.java dosyasını kaydedip kapatın.

12. toobuild hello **read-d2c-messages** Maven kullanarak uygulama komutu hello hello read-d2c-messages klasöründeki komut isteminde aşağıdaki hello yürütün:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="create-a-device-app"></a>Cihaz uygulaması oluşturma
Bu bölümde, tooan IOT hub'ı cihaz-bulut iletileri gönderen bir cihaza benzetim yapan bir Java konsol uygulaması oluşturun.

1. Merhaba iot-java-get-started klasöründe oluşturduğunuz hello *bir cihaz kimliği oluşturma* bölümünde, adlı bir Maven projesi oluşturun **simulated-device** komutu, komut isteminde aşağıdaki hello kullanarak. Bunun tek ve uzun bir komut olduğunu unutmayın:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. Komut isteminizde toohello simulated-device klasörüne gidin.

3. Bir metin düzenleyicisi kullanarak, hello simulated-device klasöründeki hello pom.xml dosyasını açın ve aşağıdaki bağımlılıkları toohello hello ekleyin **bağımlılıkları** düğümü. Bu bağımlılık, toouse hello iothub-java-client paketinde, uygulama toocommunicate IOT hub ve Java nesnelerini tooJSON tooserialize sağlar:

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
    > Hello için en son sürümünü denetleyebilir **IOT cihaz istemci** kullanarak [Maven arama][lnk-maven-device-search].

4. Merhaba pom.xml dosyasını kaydedip kapatın.

5. Bir metin düzenleyicisi kullanarak hello simulated-device\src\main\java\com\mycompany\app\App.java dosyasını açın.

6. Merhaba aşağıdakileri ekleyin **alma** deyimleri toohello dosyası:

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.google.gson.Gson;

    import java.io.*;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

7. Aşağıdaki sınıf düzeyi değişkenleri toohello hello eklemek **uygulama** sınıfı. Değiştirme **{youriothubname}** , IOT hub'ı adıyla ve **{yourdevicekey}** hello oluşturulan hello aygıt anahtarı değerine sahip *bir cihaz kimliği oluşturma* bölümü:

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    Bu örnek uygulama hello kullanan **Protokolü** değişkenini bir **DeviceClient** nesnesi. IOT Hub ile ya da hello MQTT, AMQP veya HTTP protokolü toocommunicate kullanabilirsiniz.

8. Ekleme hello aşağıdaki iç içe geçmiş **TelemetryDataPoint** hello sınıfında **uygulama** sınıf toospecify hello telemetri verilerini Cihazınızı tooyour IOT hub'ı gönderir:

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
9. Ekleme hello aşağıdaki iç içe geçmiş **EventCallback** hello sınıfında **uygulama** hello aygıt uygulamadan bir ileti işlediğinde IOT hub'ı hello sınıfı toodisplay hello onay durumunu döndürür. Merhaba ileti işlendiğinde bu yöntem aynı zamanda hello hello uygulamadaki ana iş parçacığı bildirir:
   
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

10. Ekleme hello aşağıdaki iç içe geçmiş **MessageSender** hello sınıfında **uygulama** sınıfı. Merhaba **çalıştırmak** bu sınıftaki yöntemi örnek telemetri verileri toosend tooyour IOT hub'ı oluşturur ve hello sonraki iletiyi göndermeden önce onay bekler:

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

    Bu yöntem bir hello IOT hub'ı hello önceki iletiyi onayladıktan bir saniye sonra yeni bir cihaz bulut iletisi gönderir. Selamlama iletisine JSON serileştirilmiş nesne hello DeviceID içeren ve rastgele sayılar toosimulate sıcaklık algılayıcısı ve nem algılayıcı oluşturulur.

11. Hello yerine **ana** yöntemi ile bir iş parçacığı toosend cihaz bulut iletilerini tooyour IOT hub'ı oluşturan koddan hello:

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

12. Merhaba App.java dosyasını kaydedip kapatın.

13. toobuild hello **simulated-device** Maven kullanarak uygulama komutu hello hello simulated-device klasöründeki komut isteminde aşağıdaki hello yürütün:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

> [!NOTE]
> tookeep şeyler basit, Bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz. Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme][lnk-transient-faults].

## <a name="run-hello-apps"></a>Merhaba uygulamaları çalıştırma

Hazır toorun hello uygulamaları sunulmuştur.

1. Hello read-d2c klasöründeki bir komut isteminde IOT hub'ınızı hello ilk bölümü izlemeye komutu toobegin aşağıdaki hello çalıştırın:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Java IOT Hub hizmeti uygulama toomonitor cihaz-bulut iletileri][7]

2. Telemetri veri tooyour IOT hub'ı gönderme komutu toobegin aşağıdaki hello hello simulated-device klasöründeki komut isteminde çalıştırın:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Java IOT Hub cihaz uygulaması toosend cihaz bulut iletilerini][8]

3. Merhaba **kullanım** döşeme hello [Azure portal] [ lnk-portal] gösterir hello gönderilen iletileri toohello IOT hub'ı sayısı:

    ![Azure portalı kullanım kutucuğu sayısını gösteren gönderilen iletileri tooIoT Hub][43]

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide hello Azure portalında yeni bir IOT hub yapılandırılmış ve ardından hello IOT hub'ın kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz. Bu cihaz kimliğini tooenable hello cihaz uygulama toosend cihaz bulut iletilerini toohello IOT hub kullanılır. Merhaba hello IOT hub tarafından alınan iletileri görüntüleyen bir uygulama da oluşturmuş.

Başlarken toocontinue IOT Hub ve tooexplore diğer IOT senaryolarını bakın:

* [Cihazınızı bağlama][lnk-connect-device]
* [Cihaz yönetimini kullanmaya başlama][lnk-device-management]
* [Azure IoT Edge’i kullanmaya başlama][lnk-iot-edge]

toolearn tooextend, IOT çözümü ve işlem cihaz bulut iletilerini ölçekli olarak nasıl görürüm hello [cihaz-bulut iletileri] [ lnk-process-d2c-tutorial] Öğreticisi.
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
