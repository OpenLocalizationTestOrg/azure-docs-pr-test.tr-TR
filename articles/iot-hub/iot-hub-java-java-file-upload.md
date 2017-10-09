---
title: "aygıtları tooAzure IOT Hub Java ile aaaUpload dosyalarından | Microsoft Docs"
description: "Java için Azure IOT cihaz SDK'sını kullanarak bir aygıtı toohello buluttan nasıl tooupload dosyaları. Karşıya yüklenen dosyaların bir Azure depolama blob kapsayıcısında depolanır."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4759d229-f856-4526-abda-414f8b00a56d
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: e305fe61bf7ca0aeb2c092bc2c7efebdc78d4f68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub"></a>IOT Hub ile cihaz toohello buluttan dosyaları karşıya yükleme

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

Bu öğretici hello hello kodda inşa edilmiştir [IOT Hub ile bulut cihaza ileti gönderme](iot-hub-java-java-c2d.md) öğretici tooshow, nasıl toouse hello [dosya karşıya yükleme özellikleri IOT Hub'ın](iot-hub-devguide-file-upload.md) tooupload bir dosya çok[ Azure blob depolama](../storage/index.md). Merhaba öğretici gösterir, nasıl için:

- Güvenli bir şekilde bir aygıt ile Azure sağlayan bir dosya yüklemek için URI blob.
- Merhaba, uygulama arka ucu IOT hub'ı dosya karşıya yükleme bildirimleri tootrigger işleme hello dosyasında kullanın.

Merhaba [IOT Hub ile çalışmaya başlama](iot-hub-java-java-getstarted.md) ve [IOT Hub ile bulut cihaza ileti gönderme](iot-hub-java-java-c2d.md) öğreticiler hello temel cihaz Bulut ve bulut-cihaz Mesajlaşma işlevlerini IOT hub'ı gösterir. Merhaba [işlem cihaz-bulut iletileri](iot-hub-java-java-process-d2c.md) öğretici bir şekilde tooreliably store cihaz bulut iletilerini Azure blob depolama alanındaki açıklar. Ancak, bazı senaryolarda hello veri cihazlarınızı IOT hub'ı kabul eden hello görece küçük cihaz bulut iletilere Gönder kolayca eşlenemiyor. Örneğin:

* Görüntüleri içeren büyük dosyaları
* Videolar
* Yüksek sıklıkta örneklenen titreşimi veri
* Önceden işlenmiş veri çeşit.

Bu dosyalar genellikle gibi araçları kullanılarak hello bulutta işlenen toplu olan [Azure Data Factory](../data-factory/index.md) veya hello [Hadoop](../hdinsight/index.md) yığını. Bir aygıt tooupland dosyalarından gerektiğinde, hello güvenliği ve güvenilirliği için IOT hub'ı kullanmaya devam edebilirsiniz.

Merhaba Bu öğreticinin sonunda iki Java konsol uygulamaları çalıştırın:

* **simulated-device**, hello [IOT Hub ile gönderme bulut-cihaz iletilerini] öğreticide oluşturulan hello uygulaması değiştirilmiş bir sürümü. Bu uygulama, IOT hub tarafından sağlanan bir SAS URI'sini kullanarak bir dosya toostorage yükler.
* **dosya karşıya yükleme bildirimi okuma**, IOT hub'ından dosya karşıya yükleme bildirimlerini alır.

> [!NOTE]
> IOT hub'ı Azure IOT cihaz SDK'ları çok sayıda cihaz platformları ve (C, .NET ve Javascript dahil) dilleri destekler. Toohello başvuran [Azure IOT Geliştirme Merkezi] hakkında adım adım yönergeler için tooconnect, IOT Hub cihaz tooAzure.

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Merhaba son [Java SE Geliştirme Seti 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Etkin bir Azure hesabı. (Bir hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz bir hesap](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.)

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a>Bir aygıt uygulamasından bir dosyayı karşıya yüklemek

Bu bölümde, oluşturduğunuz hello cihaz uygulamayı değiştirmek [IOT Hub ile bulut cihaza ileti gönderme](iot-hub-java-java-c2d.md) tooupload dosya tooIoT hub.

1. Bir görüntü dosyası toohello kopyalama `simulated-device` klasörü ve yeniden adlandırmak `myimage.png`.

1. Bir metin düzenleyicisi kullanarak hello açın `simulated-device\src\main\java\com\mycompany\app\App.java` dosya.

1. Merhaba değişken bildirimi toohello ekleme **uygulama** sınıfı:

    ```java
    private static String fileName = "myimage.png";
    ```

1. tooprocess karşıya yükleme durumu geri çağırma iletileri dosya, hello aşağıdakileri ekleyin iç içe geçmiş sınıf toohello **uygulama** sınıfı:

    ```java
    // Define a callback method tooprint status codes from IoT Hub.
    protected static class FileUploadStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toofile upload for " + fileName
            + " operation with status " + status.name());
      }
    }
    ```

1. tooupload görüntüleri tooIoT Hub'ı ekleme yöntemi toohello aşağıdaki hello **uygulama** sınıfı tooupload tooIoT Hub görüntüler:

    ```java
    // Use IoT Hub tooupload a file asynchronously tooAzure blob storage.
    private static void uploadFile(String fullFileName) throws FileNotFoundException, IOException
    {
      File file = new File(fullFileName);
      InputStream inputStream = new FileInputStream(file);
      long streamLength = file.length();

      client.uploadToBlobAsync(fileName, inputStream, streamLength, new FileUploadStatusCallBack(), null);
    }
    ```

1. Merhaba değiştirme **ana** yöntemi toocall hello **uploadFile** hello aşağıdaki kod parçacığında gösterildiği gibi yöntemi:

    ```java
    client.open();

    try
    {
      // Get hello filename and start hello upload.
      String fullFileName = System.getProperty("user.dir") + File.separator + fileName;
      uploadFile(fullFileName);
      System.out.println("File upload started with success");
    }
    catch (Exception e)
    {
      System.out.println("Exception uploading file: " + e.getCause() + " \nERROR: " + e.getMessage());
    }

    MessageSender sender = new MessageSender();
    ```

1. Kullanım hello şu komutu toobuild hello **simulated-device** uygulama ve hataları denetleyin:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="receive-a-file-upload-notification"></a>Dosya karşıya yükleme bildirimi

Bu bölümde IOT hub'dan dosya karşıya yükleme bildirim iletileri alan bir Java konsol uygulaması oluşturun.

Merhaba gereksinim **iothubowner** bağlantı dizesi, IOT hub'ı toocomplete için bu bölümü. Hello hello bağlantı dizesi bulabilirsiniz [Azure portal](https://portal.azure.com/) hello üzerinde **paylaşılan erişim ilkesi** dikey.

1. Adlı bir Maven projesi oluşturun **dosya karşıya yükleme bildirimi okuma** komutu, komut isteminde aşağıdaki hello kullanarak. Bu komut tek ve uzun bir komut olduğuna dikkat edin:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-file-upload-notification -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

1. Komut isteminizde yeni toohello gidin `read-file-upload-notification` klasör.

1. Bir metin düzenleyicisi kullanarak hello açın `pom.xml` hello dosyasında `read-file-upload-notification` klasörü ve bağımlılık toohello aşağıdaki hello ekleyin **bağımlılıkları** düğümü. Merhaba bağımlılık ekleme sağlar toouse hello **iothub-java-service-client** , uygulama toocommunicate IOT hub hizmetinizle paketinde:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > Hello için en son sürümünü denetleyebilir **IOT hizmeti istemcisi** kullanarak [Maven arama](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).

1. Kaydet ve Kapat hello `pom.xml` dosya.

1. Bir metin düzenleyicisi kullanarak hello açın `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` dosya.

1. Merhaba aşağıdakileri ekleyin **alma** deyimleri toohello dosyası:

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;
    ```

1. Aşağıdaki sınıf düzeyi değişkenleri toohello hello eklemek **uygulama** sınıfı:

    ```java
    private static final String connectionString = "{Your IoT Hub connection string}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    private static FileUploadNotificationReceiver fileUploadNotificationReceiver = null;
    ```

1. Merhaba dosya karşıya yükleme toohello Konsolu hakkında tooprint bilgi eklemek hello aşağıdaki iç içe geçmiş sınıf toohello **uygulama** sınıfı:

    ```java
    // Create a thread tooreceive file upload notifications.
    private static class ShowFileUploadNotifications implements Runnable {
      public void run() {
        try {
          while (true) {
            System.out.println("Recieve file upload notifications...");
            FileUploadNotification fileUploadNotification = fileUploadNotificationReceiver.receive();
            if (fileUploadNotification != null) {
              System.out.println("File Upload notification received");
              System.out.println("Device Id : " + fileUploadNotification.getDeviceId());
              System.out.println("Blob Uri: " + fileUploadNotification.getBlobUri());
              System.out.println("Blob Name: " + fileUploadNotification.getBlobName());
              System.out.println("Last Updated : " + fileUploadNotification.getLastUpdatedTimeDate());
              System.out.println("Blob Size (Bytes): " + fileUploadNotification.getBlobSizeInBytes());
              System.out.println("Enqueued Time: " + fileUploadNotification.getEnqueuedTimeUtcDate());
            }
          }
        } catch (Exception ex) {
          System.out.println("Exception reading reported properties: " + ex.getMessage());
        }
      }
    }
    ```

1. dosya karşıya yükleme bildirimleri için dinler toostart hello iş parçacığı ekleme kodu toohello aşağıdaki hello **ana** yöntemi:

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(connectionString, protocol);

      if (serviceClient != null) {
        serviceClient.open();

        // Get a file upload notification receiver from hello ServiceClient.
        fileUploadNotificationReceiver = serviceClient.getFileUploadNotificationReceiver();
        fileUploadNotificationReceiver.open();

        // Start hello thread tooreceive file upload notifications.
        ShowFileUploadNotifications showFileUploadNotifications = new ShowFileUploadNotifications();
        ExecutorService executor = Executors.newFixedThreadPool(1);
        executor.execute(showFileUploadNotifications);

        System.out.println("Press ENTER tooexit.");
        System.in.read();
        executor.shutdownNow();
        System.out.println("Shutting down sample...");
        fileUploadNotificationReceiver.close();
        serviceClient.close();
      }
    }
    ```

1. Kaydet ve Kapat hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` dosya.

1. Kullanım hello şu komutu toobuild hello **dosya karşıya yükleme bildirimi okuma** uygulama ve hataları denetleyin:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a>Merhaba uygulamaları çalıştırma

Hazır toorun hello uygulamaları sunulmuştur.

Bir komut isteminde hello `read-file-upload-notification` klasörü, hello aşağıdaki komutu çalıştırın:

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

Bir komut isteminde hello `simulated-device` klasörü, hello aşağıdaki komutu çalıştırın:

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

Merhaba aşağıdaki ekran görüntüsünde hello çıktısını hello gösterir **simulated-device** uygulama:

![Simulated-device uygulamadan çıktı](media/iot-hub-java-java-upload/simulated-device.png)

Merhaba aşağıdaki ekran görüntüsünde hello çıktısını hello gösterir **dosya karşıya yükleme bildirimi okuma** uygulama:

![Dosya karşıya yükleme bildirimi okuma uygulamadan çıktı](media/iot-hub-java-java-upload/read-file-upload-notification.png)

Merhaba portal tooview karşıya hello yapılandırdığınız hello depolama kapsayıcısı dosyasında kullanabilirsiniz:

![Yüklenen dosya](media/iot-hub-java-java-upload/uploaded-file.png)

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, nasıl toouse hello dosyayı karşıya IOT Hub'ın cihazlardan toosimplify dosya yüklemeleri yeteneklerini öğrendiniz. Aşağıdaki makaleleri hello ile tooexplore IOT hub özellikleri ve senaryoları devam edebilirsiniz:

* [IOT hub'ı program aracılığıyla oluşturma][lnk-create-hub]
* [Giriş tooC SDK][lnk-c-sdk]
* [Azure IOT SDK'ları][lnk-sdks]

toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:

* [Bir cihaz IOT Edge benzetimini yapma][lnk-iotedge]

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png
[3]: ./media/iot-hub-csharp-csharp-file-upload/enable-file-notifications.png

<!-- Links -->



[Azure IOT Geliştirme Merkezi]: http://www.azure.com/develop/iot

[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure Storage]:../storage/common/storage-create-storage-account.md#create-a-storage-account
[lnk-configure-upload]: iot-hub-configure-file-upload.md
[Azure IoT service SDK NuGet package]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md


