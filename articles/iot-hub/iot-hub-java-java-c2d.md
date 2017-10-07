---
title: "Azure IOT hub'ı (Java) aaaCloud cihaza iletileriyle | Microsoft Docs"
description: "Nasıl toosend bulut-cihaz hello Azure IOT SDK'ları için Java kullanarak Azure IOT hub'ı tooa aygıttan iletileri. Bir sanal cihaz uygulaması tooreceive bulut-cihaz iletilerini değiştirmek ve arka uç uygulaması toosend hello bulut-cihaz iletilerini değiştirin."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7f785ea8-e7c2-40c5-87ef-96525e9b9e1e
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: 8721f18428c849ed9a04aa2e45c65605c3e38101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-java"></a>IOT hub'ı (Java) sahip bulut-cihaz iletilerini gönder
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

Azure IOT Hub, milyonlarca cihaza arasında güvenilir ve güvenli çift yönlü iletişimler sağlayan tam olarak yönetilen hizmet etkinleştirin ve bir çözüm arka ucu ' dir. Merhaba [IOT Hub ile çalışmaya başlama] öğretici nasıl toocreate IOT hub'ı, bir cihaz kimliği, sağlamak ve cihaz-bulut iletileri gönderen bir sanal cihaz uygulamasının kodu gösterir.

Bu öğretici derlemeler [IOT Hub ile çalışmaya başlama]. Size bir nasıl gösterir için:

* Çözüm arka ucunuz, bulut-cihaz iletilerini tooa tek cihaz IOT hub'ı aracılığıyla gönderin.
* Bir cihazda bulut-cihaz iletilerini alır.
* Çözüm arka ucunuz, teslimat alındısı iste (*geri bildirim*) tooa cihaz IOT Hub'ından gönderilen iletileri için.

Hello bulut-cihaz iletilerini hakkında daha fazla bilgi bulabilirsiniz [IOT Hub Geliştirici Kılavuzu][IoT Hub developer guide - C2D].

Bu öğreticinin Hello sonunda, iki Java konsol uygulamaları çalıştırın:

* **simulated-device**, oluşturulan hello uygulama değiştirilmiş bir sürümünü [IOT Hub ile çalışmaya başlama], hangi tooyour IOT hub'ı bağlar ve bulut-cihaz iletilerini alır.
* **Send-c2d-messages**, hangi bulut aygıt iletisi toohello sanal cihaz uygulaması IOT hub'ı üzerinden gönderir ve teslimat alındısı alır.

> [!NOTE]
> IOT Hub SDK desteği birçok cihaz platformları ve Azure IOT cihaz SDK'ları aracılığıyla dilleri (C, Java ve Javascript dahil) sahiptir. Adım adım yönergeler nasıl tooconnect aygıt toothis öğreticinin kod ve genellikle tooAzure IOT hub'ı görmek için hello [Azure IOT Geliştirme Merkezi].

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Merhaba tam çalışma sürümü [IOT Hub ile çalışmaya başlama](iot-hub-java-java-getstarted.md) veya [işlem IOT Hub cihaz bulut iletilerini](iot-hub-java-java-process-d2c.md) Öğreticisi.
* Merhaba son [Java SE Geliştirme Seti 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Etkin bir Azure hesabı. (Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)

## <a name="receive-messages-in-hello-simulated-device-app"></a>Merhaba sanal cihaz uygulamasının ileti alma

Bu bölümde, oluşturduğunuz hello sanal cihaz uygulamasının değiştirme [IOT Hub ile çalışmaya başlama] tooreceive bulut cihaza iletilerden hello IOT hub'ı.

1. Bir metin düzenleyicisi kullanarak hello simulated-device\src\main\java\com\mycompany\app\App.java dosyasını açın.

2. Merhaba aşağıdakileri ekleyin **MessageCallback** sınıf hello içinde iç içe bir sınıf olarak **uygulama** sınıfı. Merhaba **yürütme** yöntemi hello cihaz IOT Hub'ından bir ileti aldığında çağrılır. Bu örnekte, hello cihaz her zaman hello IOT hub'ı selamlama iletisine tamamlandığını bildirir:

    ```java
    private static class AppMessageCallback implements MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));
    
        return IotHubMessageResult.COMPLETE;
      }
    }
    ```
3. Merhaba değiştirme **ana** yöntemi toocreate bir **AppMessageCallback** örneği ve çağrı hello **setMessageCallback** gibi hello istemci açılmadan önce yöntemi:

    ```java
    client = new DeviceClient(connString, protocol);
   
    MessageCallback callback = new AppMessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```

    > [!NOTE]
    > HTTP MQTT veya AMQP yerine hello taşıma olarak kullanırsanız, hello **DeviceClient** seyrek IOT Hub (değerinden 25 dakikada bir) gelen iletileri örneği denetler. Merhaba hello farklarını MQTT, AMQP ve HTTP desteği ve IOT hub'ı azaltma hakkında daha fazla bilgi için bkz: [IOT Hub Geliştirici Kılavuzu][IoT Hub developer guide - C2D].

4. toobuild hello **simulated-device** Maven kullanarak uygulama komutu hello hello simulated-device klasöründeki komut isteminde aşağıdaki hello yürütün:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="send-a-cloud-to-device-message"></a>Bulut cihaza ileti gönderme

Bu bölümde, bulut-cihaz iletilerini toohello sanal cihaz uygulamasının gönderen bir Java konsol uygulaması oluşturun. Hello eklediğiniz hello aygıtın aygıt kimliği hello [IOT Hub ile çalışmaya başlama] Öğreticisi. Hello bulabileceğiniz hub'ınız için IOT Hub bağlantı dizesine hello de [Azure portal].

1. Adlı bir Maven projesi oluşturun **c2d iletileri gönderme** komutu, komut isteminde aşağıdaki hello kullanarak. Bu komut tek ve uzun bir komut olduğuna dikkat edin:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. Komut isteminizde toohello yeni gönderme-c2d-messages klasörüne gidin.

3. Bir metin düzenleyicisi kullanarak hello Gönder-c2d-messages klasöründeki hello pom.xml dosyasını açın ve bağımlılık toohello aşağıdaki hello ekleyin **bağımlılıkları** düğümü. Merhaba bağımlılık ekleme sağlar toouse hello **iothub-java-service-client** , uygulama toocommunicate IOT hub hizmetinizle paketinde:

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

5. Bir metin düzenleyicisi kullanarak hello send-c2d-messages\src\main\java\com\mycompany\app\App.java dosyasını açın.

6. Merhaba aşağıdakileri ekleyin **alma** deyimleri toohello dosyası:

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. Aşağıdaki sınıf düzeyi değişkenleri toohello hello eklemek **uygulama** sınıfına **{yourhubconnectionstring}** ve **{yourdeviceid}** hello ile daha önce not ettiğiniz değerleri:

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```

8. Hello yerine **ana** koddan hello yöntemiyle. Bu kod tooyour IOT hub'ı bağlandığında, bir ileti tooyour cihaz gönderir ve sonra o hello aygıt alınan ve işlenen hello iletisi için bir bildirim bekler:
   
    ```java
    public static void main(String[] args) throws IOException,
        URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(
        connectionString, protocol);
   
      if (serviceClient != null) {
        serviceClient.open();
        FeedbackReceiver feedbackReceiver = serviceClient
          .getFeedbackReceiver();
        if (feedbackReceiver != null) feedbackReceiver.open();
   
        Message messageToSend = new Message("Cloud toodevice message.");
        messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);
   
        serviceClient.send(deviceId, messageToSend);
        System.out.println("Message sent toodevice");
   
        FeedbackBatch feedbackBatch = feedbackReceiver.receive(10000);
        if (feedbackBatch != null) {
          System.out.println("Message feedback received, feedback time: "
            + feedbackBatch.getEnqueuedTimeUtc().toString());
        }
   
        if (feedbackReceiver != null) feedbackReceiver.close();
        serviceClient.close();
      }
    }
    ```

    > [!NOTE]
    > Basitlik'ın artırmak amacıyla için bu öğreticiyi herhangi bir yeniden deneme ilkesi uygulamaz. Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme].


9. toobuild hello **simulated-device** Maven kullanarak uygulama komutu hello hello simulated-device klasöründeki komut isteminde aşağıdaki hello yürütün:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a>Merhaba uygulamaları çalıştırma

Hazır toorun hello uygulamaları sunulmuştur.

1. Merhaba simulated-device klasöründeki komut isteminde, telemetri tooyour IOT hub ve toolisten, hub'dan gönderilen bulut cihaz iletileri gönderme komutu toobegin aşağıdaki hello çalıştırın:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Merhaba sanal cihaz uygulamasının çalıştırın][img-simulated-device]

2. Hello Gönder-c2d-messages klasöründeki komut isteminde, bir bulut aygıt iletisi ve geri bildirim bekle komutu toosend aşağıdaki hello çalıştırın:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Merhaba komutu toosend hello bulut cihaz ileti çalıştırın][img-send-command]

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, nasıl öğrenilen toosend ve bulut-cihaz iletilerini. 

IOT hub'ı kullanan tam uçtan uca çözümler toosee örnekleri bkz [Azure IOT paketi].

IOT Hub ile çözümleri geliştirme hakkında daha fazla toolearn bkz hello [IOT Hub Geliştirici Kılavuzu].

<!-- Images -->
[img-simulated-device]: media/iot-hub-java-java-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-java-java-c2d/sendc2d.png
<!-- Links -->

[IOT Hub ile çalışmaya başlama]: iot-hub-java-java-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[IOT Hub Geliştirici Kılavuzu]: iot-hub-devguide.md
[Azure IOT Geliştirme Merkezi]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java
[geçici hata işleme]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure portal]: https://portal.azure.com
[Azure IOT paketi]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22