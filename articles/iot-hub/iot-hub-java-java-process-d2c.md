---
title: aaaProcess Azure IOT Hub cihaz bulut iletilerini (Java) | Microsoft Docs
description: "Nasıl tooprocess yönlendirme kuralları ve özel uç noktaları toodispatch kullanarak IOT Hub cihaz bulut iletilerini tooother arka uç hizmetlerini iletileri."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: bd9af5f9-a740-4780-a2a6-8c0e2752cf48
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.openlocfilehash: 084e84e721ca4297c4d7d6cb06a43b0bed9bce85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-java"></a>İşlem IOT hub'a cihaz-bulut iletileri (Java)

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

Azure IOT Hub güvenilir sağlayan tam olarak yönetilen bir hizmettir ve arka uç milyonlarca cihaza ve çözüm arasında güvenli çift yönlü iletişim. Diğer öğreticiler ([IOT Hub ile çalışmaya başlama] ve [IOT Hub ile bulut cihaza ileti gönderme][lnk-c2d]) toouse nasıl hello temel cihaz Bulut ve bulut-cihaz Göster IOT hub'ı işlevselliğini Mesajlaşma.

Bu öğretici hello gösterilen hello kod inşa edilmiştir [IOT Hub ile çalışmaya başlama] öğretici ve nasıl toouse ileti yönlendirme tooprocess cihaz bulut ölçeklenebilir bir şekilde gösterir. Başlangıç Öğreticisi nasıl hello çözümden Acil eylem gerekli tooprocess iletileri arka uç gösterilmektedir. Örneğin, bir aygıt bir bilet bir CRM sistemine ekleme tetikleyen bir uyarı iletisi gönderebilir. Bunun aksine, veri noktası iletileri yalnızca bir analytics motoruna akış. Örneğin, sıcaklık telemetri toobe sonra analiz etmek için depolanmış olan bir CİHAZDAN bir veri noktası iletisidir.

Bu öğretici Hello sonunda üç Java konsol uygulamaları çalıştırın:

* **simulated-device**, hello oluşturulan hello uygulaması değiştirilmiş bir sürümünü [IOT Hub ile çalışmaya başlama] öğretici, saniyede veri noktası cihaz bulut iletilerini gönderir ve etkileşimli cihaz bulut iletilerini her 10 saniye sayısı. Bu uygulama, IOT Hub ile Merhaba AMQP protokolünü toocommunicate kullanır.
* **Read-d2c-messages** cihaz uygulamanız tarafından gönderilen hello telemetri görüntüler.
* **Okuma kritik-sıra** hello Service Bus kuyruğu bağlı toohello IOT hub'ı kritik iletileri hello çıkarır.

> [!NOTE]
> IOT hub'ı birçok cihaz platformları ve C, Java ve JavaScript gibi diller için SDK desteğe sahiptir. Nasıl tooreplace hello cihaz Bu öğreticide bir fiziksel cihaz ile ilgili yönergeler için ve nasıl tooconnect aygıtları tooan IOT hub'ına bakın hello [Azure IOT Geliştirme Merkezi].

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Merhaba tam çalışma sürümü [IOT Hub ile çalışmaya başlama] Öğreticisi.
* Merhaba son [Java SE Geliştirme Seti 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Etkin bir Azure hesabı. (Bir hesabınız yoksa, [ücretsiz bir hesap] oluşturabilirsiniz [lnk-free-trial] yalnızca birkaç dakika içinde.)

Bazı temel bilgiye sahip [Azure Storage] ve [Azure Service Bus].

## <a name="send-interactive-messages-from-a-device-app"></a>Bir aygıt uygulamadan etkileşimli ileti gönderme
Bu bölümde, hello oluşturduğunuz hello cihaz uygulamayı değiştirmek [IOT Hub ile çalışmaya başlama] öğretici toooccasionally hemen işleme gerektiren ileti gönderme.

1. Bir metin düzenleyicisi tooopen hello simulated-device\src\main\java\com\mycompany\app\App.java dosyasını kullanın. Bu dosya hello hello kodunu içerir **simulated-device** hello oluşturduğunuz uygulama [IOT Hub ile çalışmaya başlama] Öğreticisi.

2. Hello yerine **MessageSender** koddan hello sınıfıyla:

    ```java
    private static class MessageSender implements Runnable {

        public void run()  {
            try {
                double minTemperature = 20;
                double minHumidity = 60;
                Random rand = new Random();

                while (true) {
                    String msgStr;
                    Message msg;
                    if (new Random().nextDouble() > 0.7) {
                        msgStr = "This is a critical message.";
                        msg = new Message(msgStr);
                        msg.setProperty("level", "critical");
                    } else {
                        double currentTemperature = minTemperature + rand.nextDouble() * 15;
                        double currentHumidity = minHumidity + rand.nextDouble() * 20; 
                        TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
                        telemetryDataPoint.deviceId = deviceId;
                        telemetryDataPoint.temperature = currentTemperature;
                        telemetryDataPoint.humidity = currentHumidity;

                        msgStr = telemetryDataPoint.serialize();
                        msg = new Message(msgStr);
                    }
                    
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
   
    Bu yöntem rastgele hello özelliği ekler `"level": "critical"` hello uygulama arka uç tarafından Acil eylem gerektiren bir ileti taklit eden bir hello aygıt tarafından gönderilen toomessages. Bu IOT hub'ın hello ileti toohello uygun mesajı hedef yönlendirebilir şekilde hello uygulama bu bilgileri hello ileti özelliklerinde yerine hello ileti gövdesinde geçirir.
   
   > [!NOTE]
   > Özellikler tooroute ileti işleme, ayrıca burada gösterilen toohello etkin yolunuzda örnek soğuk yolu da dahil olmak üzere çeşitli senaryolar için kullanabilirsiniz.

2. Merhaba simulated-device\src\main\java\com\mycompany\app\App.java dosyasını kaydedip kapatın.

    > [!NOTE]
    > Basitlik Hello artırmak amacıyla için bu öğreticiyi herhangi bir yeniden deneme ilkesi uygulamaz. Üretim kodunda hello MSDN makalesinde önerilen üstel geri alma gibi bir yeniden deneme ilkesi uygulamalıdır [geçici hata işleme].

3. toobuild hello **simulated-device** Maven kullanarak uygulama komutu hello hello simulated-device klasöründeki komut isteminde aşağıdaki hello yürütün:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-tooyour-iot-hub-and-route-messages-tooit"></a>Bir kuyruk tooyour IOT hub ve rota iletileri tooit Ekle

Bu bölümde, hizmet veri yolu kuyruğu oluşturma, tooyour IOT hub'ı bağlanmak ve selamlama iletisine özellikte hello varlığına göre IOT hub toosend iletileri toohello sırası yapılandırın. Service Bus sıralarından tooprocess nasıl iletileri hakkında daha fazla bilgi için bkz: [kuyruklarla çalışmaya başlama][lnk-sb-queues-java].

1. Service Bus kuyruğuna açıklandığı gibi oluşturmak [kuyruklarla çalışmaya başlama][lnk-sb-queues-java]. Merhaba ad alanı ve sıra adını not edin.

2. Azure portal Merhaba, IOT hub'ınızı açın ve'ı tıklatın **uç noktaları**.

    ![IOT hub uç noktaları][30]

3. Merhaba, **uç noktaları** dikey penceresinde tıklatın **Ekle** en üst tooadd sıra tooyour IOT hub'ınızı hello. Ad hello endpoint **CriticalQueue** ve hello aşağı açılan listeler tooselect kullanmak **Service Bus kuyruğuna**, hizmet veri yolu ad alanı, sıra içinde bulunduğu hello ve Merhaba, kuyruk adı. İşiniz bittiğinde tıklatın **kaydetmek** hello altındaki.

    ![Bir uç nokta ekleme][31]

4. Şimdi **yollar** IOT hub'ınızdaki. Tıklatın **Ekle** hello üstünde hello dikey toocreate toohello sıra, yalnızca iletileri yönlendiren bir yönlendirme kuralı eklendi. Seçin **DeviceTelemetry** hello veri kaynağı olarak. Girin `level="critical"` hello koşulu olarak ve hello sıra yeni eklenen kural endpoint yönlendirme hello olarak özel bir uç noktası olarak seçin. İşiniz bittiğinde tıklatın **kaydetmek** hello altındaki.

    ![Bir yol ekleme][32]

    Merhaba geri dönüş rota çok ayarlandığından emin olun**ON**. Bu ayar hello varsayılan bir IOT hub'ının yapılandırmadır.

    ![Geri dönüş yolu][33]

## <a name="optional-read-from-hello-queue-endpoint"></a>(İsteğe bağlı) Merhaba sıra uç noktasından okumak

Merhaba yönergeleri takip ederek Merhaba iletileri hello sıra uç noktasından isteğe bağlı olarak okuyabilirsiniz [kuyruklarla çalışmaya başlama][lnk-sb-queues-java]. Ad hello uygulama **okuma kritik-sıra**.

## <a name="run-hello-applications"></a>Merhaba uygulamaları çalıştırma

Hazır toorun hello üç uygulama sunulmuştur.

1. toorun hello **read-d2c-messages** uygulamasında, bir komut istemi veya kabuk toohello read-d2c klasörüne gidin ve hello aşağıdaki komutu yürütün:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![Read-d2c-messages çalıştırın][readd2c]

2. toorun hello **okuma kritik-sıra** uygulamasında, bir komut istemi veya kabuk toohello okuma kritik-sıra klasörüne gidin ve hello aşağıdaki komutu yürütün:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Read-kritik-messages çalıştırın][readqueue]

3. toorun hello **simulated-device** uygulamasında, bir komut istemi veya kabuk toohello simulated-device klasörüne gidin ve hello aşağıdaki komutu yürütün:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Simulated-device çalıştırın][simulateddevice]

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, nasıl tooreliably gönderme cihaz bulut iletilerini IOT Hub'ının hello ileti yönlendirme işlevini kullanarak öğrendiniz.

Merhaba [toosend bulut-cihaz IOT Hub ile nasıl iletileri] [ lnk-c2d] nasıl toosend çözüm arka ucunuz tooyour aygıtlardan iletileri gösterir.

IOT hub'ı kullanan tam uçtan uca çözümler toosee örnekleri bkz [Azure IOT paketi][lnk-suite].

IOT Hub ile çözümleri geliştirme hakkında daha fazla toolearn bkz hello [IOT Hub Geliştirici Kılavuzu].

IOT Hub içinde ileti yönlendirme hakkında daha fazla toolearn bkz [IOT Hub ile iletileri almasına ve göndermesine][lnk-devguide-messaging].

<!-- Images. -->
<!-- TODO: UPDATE PICTURES -->
[simulateddevice]: ./media/iot-hub-java-java-process-d2c/runsimulateddevice.png
[readd2c]: ./media/iot-hub-java-java-process-d2c/runprocessinteractive.png
[readqueue]: ./media/iot-hub-java-java-process-d2c/runprocessd2c.png

[30]: ./media/iot-hub-java-java-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-java-java-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-java-java-process-d2c/route-creation.png
[33]: ./media/iot-hub-java-java-process-d2c/fallback-route.png

<!-- Links -->

[lnk-sb-queues-java]: ../service-bus-messaging/service-bus-java-how-to-use-queues.md

[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/
[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/

[IOT Hub Geliştirici Kılavuzu]: iot-hub-devguide.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[IOT Hub ile çalışmaya başlama]: iot-hub-java-java-getstarted.md
[Azure IOT Geliştirme Merkezi]: https://azure.microsoft.com/develop/iot
[geçici hata işleme]: https://msdn.microsoft.com/library/hh675232.aspx

<!-- Links -->
[Geçici hata işleme]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-c2d]: iot-hub-java-java-c2d.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
