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
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub"></a><span data-ttu-id="9297b-104">IOT Hub ile cihaz toohello buluttan dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="9297b-104">Upload files from your device toohello cloud with IoT Hub</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="9297b-105">Bu öğretici hello hello kodda inşa edilmiştir [IOT Hub ile bulut cihaza ileti gönderme](iot-hub-java-java-c2d.md) öğretici tooshow, nasıl toouse hello [dosya karşıya yükleme özellikleri IOT Hub'ın](iot-hub-devguide-file-upload.md) tooupload bir dosya çok[ Azure blob depolama](../storage/index.md).</span><span class="sxs-lookup"><span data-stu-id="9297b-105">This tutorial builds on hello code in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorial tooshow you how toouse hello [file upload capabilities of IoT Hub](iot-hub-devguide-file-upload.md) tooupload a file too[Azure blob storage](../storage/index.md).</span></span> <span data-ttu-id="9297b-106">Merhaba öğretici gösterir, nasıl için:</span><span class="sxs-lookup"><span data-stu-id="9297b-106">hello tutorial shows you how to:</span></span>

- <span data-ttu-id="9297b-107">Güvenli bir şekilde bir aygıt ile Azure sağlayan bir dosya yüklemek için URI blob.</span><span class="sxs-lookup"><span data-stu-id="9297b-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="9297b-108">Merhaba, uygulama arka ucu IOT hub'ı dosya karşıya yükleme bildirimleri tootrigger işleme hello dosyasında kullanın.</span><span class="sxs-lookup"><span data-stu-id="9297b-108">Use hello IoT Hub file upload notifications tootrigger processing hello file in your app back end.</span></span>

<span data-ttu-id="9297b-109">Merhaba [IOT Hub ile çalışmaya başlama](iot-hub-java-java-getstarted.md) ve [IOT Hub ile bulut cihaza ileti gönderme](iot-hub-java-java-c2d.md) öğreticiler hello temel cihaz Bulut ve bulut-cihaz Mesajlaşma işlevlerini IOT hub'ı gösterir.</span><span class="sxs-lookup"><span data-stu-id="9297b-109">hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorials show hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="9297b-110">Merhaba [işlem cihaz-bulut iletileri](iot-hub-java-java-process-d2c.md) öğretici bir şekilde tooreliably store cihaz bulut iletilerini Azure blob depolama alanındaki açıklar.</span><span class="sxs-lookup"><span data-stu-id="9297b-110">hello [Process Device-to-Cloud messages](iot-hub-java-java-process-d2c.md) tutorial describes a way tooreliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="9297b-111">Ancak, bazı senaryolarda hello veri cihazlarınızı IOT hub'ı kabul eden hello görece küçük cihaz bulut iletilere Gönder kolayca eşlenemiyor.</span><span class="sxs-lookup"><span data-stu-id="9297b-111">However, in some scenarios you cannot easily map hello data your devices send into hello relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="9297b-112">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="9297b-112">For example:</span></span>

* <span data-ttu-id="9297b-113">Görüntüleri içeren büyük dosyaları</span><span class="sxs-lookup"><span data-stu-id="9297b-113">Large files that contain images</span></span>
* <span data-ttu-id="9297b-114">Videolar</span><span class="sxs-lookup"><span data-stu-id="9297b-114">Videos</span></span>
* <span data-ttu-id="9297b-115">Yüksek sıklıkta örneklenen titreşimi veri</span><span class="sxs-lookup"><span data-stu-id="9297b-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="9297b-116">Önceden işlenmiş veri çeşit.</span><span class="sxs-lookup"><span data-stu-id="9297b-116">Some form of preprocessed data.</span></span>

<span data-ttu-id="9297b-117">Bu dosyalar genellikle gibi araçları kullanılarak hello bulutta işlenen toplu olan [Azure Data Factory](../data-factory/index.md) veya hello [Hadoop](../hdinsight/index.md) yığını.</span><span class="sxs-lookup"><span data-stu-id="9297b-117">These files are typically batch processed in hello cloud using tools such as [Azure Data Factory](../data-factory/index.md) or hello [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="9297b-118">Bir aygıt tooupland dosyalarından gerektiğinde, hello güvenliği ve güvenilirliği için IOT hub'ı kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9297b-118">When you need tooupland files from a device, you can still use hello security and reliability of IoT Hub.</span></span>

<span data-ttu-id="9297b-119">Merhaba Bu öğreticinin sonunda iki Java konsol uygulamaları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9297b-119">At hello end of this tutorial you run two Java console apps:</span></span>

* <span data-ttu-id="9297b-120">**simulated-device**, hello [IOT Hub ile gönderme bulut-cihaz iletilerini] öğreticide oluşturulan hello uygulaması değiştirilmiş bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="9297b-120">**simulated-device**, a modified version of hello app created in hello [Send Cloud-to-Device messages with IoT Hub] tutorial.</span></span> <span data-ttu-id="9297b-121">Bu uygulama, IOT hub tarafından sağlanan bir SAS URI'sini kullanarak bir dosya toostorage yükler.</span><span class="sxs-lookup"><span data-stu-id="9297b-121">This app uploads a file toostorage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="9297b-122">**dosya karşıya yükleme bildirimi okuma**, IOT hub'ından dosya karşıya yükleme bildirimlerini alır.</span><span class="sxs-lookup"><span data-stu-id="9297b-122">**read-file-upload-notification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="9297b-123">IOT hub'ı Azure IOT cihaz SDK'ları çok sayıda cihaz platformları ve (C, .NET ve Javascript dahil) dilleri destekler.</span><span class="sxs-lookup"><span data-stu-id="9297b-123">IoT Hub supports many device platforms and languages (including C, .NET, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="9297b-124">Toohello başvuran [Azure IOT Geliştirme Merkezi] hakkında adım adım yönergeler için tooconnect, IOT Hub cihaz tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9297b-124">Refer toohello [Azure IoT Developer Center] for step-by-step instructions on how tooconnect your device tooAzure IoT Hub.</span></span>

<span data-ttu-id="9297b-125">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="9297b-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="9297b-126">Merhaba son [Java SE Geliştirme Seti 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="9297b-126">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="9297b-127">Maven 3</span><span class="sxs-lookup"><span data-stu-id="9297b-127">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="9297b-128">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="9297b-128">An active Azure account.</span></span> <span data-ttu-id="9297b-129">(Bir hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz bir hesap](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.)</span><span class="sxs-lookup"><span data-stu-id="9297b-129">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="9297b-130">Bir aygıt uygulamasından bir dosyayı karşıya yüklemek</span><span class="sxs-lookup"><span data-stu-id="9297b-130">Upload a file from a device app</span></span>

<span data-ttu-id="9297b-131">Bu bölümde, oluşturduğunuz hello cihaz uygulamayı değiştirmek [IOT Hub ile bulut cihaza ileti gönderme](iot-hub-java-java-c2d.md) tooupload dosya tooIoT hub.</span><span class="sxs-lookup"><span data-stu-id="9297b-131">In this section, you modify hello device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tooupload a file tooIoT hub.</span></span>

1. <span data-ttu-id="9297b-132">Bir görüntü dosyası toohello kopyalama `simulated-device` klasörü ve yeniden adlandırmak `myimage.png`.</span><span class="sxs-lookup"><span data-stu-id="9297b-132">Copy an image file toohello `simulated-device` folder and rename it `myimage.png`.</span></span>

1. <span data-ttu-id="9297b-133">Bir metin düzenleyicisi kullanarak hello açın `simulated-device\src\main\java\com\mycompany\app\App.java` dosya.</span><span class="sxs-lookup"><span data-stu-id="9297b-133">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="9297b-134">Merhaba değişken bildirimi toohello ekleme **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="9297b-134">Add hello variable declaration toohello **App** class:</span></span>

    ```java
    private static String fileName = "myimage.png";
    ```

1. <span data-ttu-id="9297b-135">tooprocess karşıya yükleme durumu geri çağırma iletileri dosya, hello aşağıdakileri ekleyin iç içe geçmiş sınıf toohello **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="9297b-135">tooprocess file upload status callback messages, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Define a callback method tooprint status codes from IoT Hub.
    protected static class FileUploadStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toofile upload for " + fileName
            + " operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="9297b-136">tooupload görüntüleri tooIoT Hub'ı ekleme yöntemi toohello aşağıdaki hello **uygulama** sınıfı tooupload tooIoT Hub görüntüler:</span><span class="sxs-lookup"><span data-stu-id="9297b-136">tooupload images tooIoT Hub, add hello following method toohello **App** class tooupload images tooIoT Hub:</span></span>

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

1. <span data-ttu-id="9297b-137">Merhaba değiştirme **ana** yöntemi toocall hello **uploadFile** hello aşağıdaki kod parçacığında gösterildiği gibi yöntemi:</span><span class="sxs-lookup"><span data-stu-id="9297b-137">Modify hello **main** method toocall hello **uploadFile** method as shown in hello following snippet:</span></span>

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

1. <span data-ttu-id="9297b-138">Kullanım hello şu komutu toobuild hello **simulated-device** uygulama ve hataları denetleyin:</span><span class="sxs-lookup"><span data-stu-id="9297b-138">Use hello following command toobuild hello **simulated-device** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="9297b-139">Dosya karşıya yükleme bildirimi</span><span class="sxs-lookup"><span data-stu-id="9297b-139">Receive a file upload notification</span></span>

<span data-ttu-id="9297b-140">Bu bölümde IOT hub'dan dosya karşıya yükleme bildirim iletileri alan bir Java konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9297b-140">In this section, you create a Java console app that receives file upload notification messages from IoT Hub.</span></span>

<span data-ttu-id="9297b-141">Merhaba gereksinim **iothubowner** bağlantı dizesi, IOT hub'ı toocomplete için bu bölümü.</span><span class="sxs-lookup"><span data-stu-id="9297b-141">You need hello **iothubowner** connection string for your IoT Hub toocomplete this section.</span></span> <span data-ttu-id="9297b-142">Hello hello bağlantı dizesi bulabilirsiniz [Azure portal](https://portal.azure.com/) hello üzerinde **paylaşılan erişim ilkesi** dikey.</span><span class="sxs-lookup"><span data-stu-id="9297b-142">You can find hello connection string in hello [Azure portal](https://portal.azure.com/) on hello **Shared access policy** blade.</span></span>

1. <span data-ttu-id="9297b-143">Adlı bir Maven projesi oluşturun **dosya karşıya yükleme bildirimi okuma** komutu, komut isteminde aşağıdaki hello kullanarak.</span><span class="sxs-lookup"><span data-stu-id="9297b-143">Create a Maven project called **read-file-upload-notification** using hello following command at your command prompt.</span></span> <span data-ttu-id="9297b-144">Bu komut tek ve uzun bir komut olduğuna dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="9297b-144">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-file-upload-notification -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

1. <span data-ttu-id="9297b-145">Komut isteminizde yeni toohello gidin `read-file-upload-notification` klasör.</span><span class="sxs-lookup"><span data-stu-id="9297b-145">At your command prompt, navigate toohello new `read-file-upload-notification` folder.</span></span>

1. <span data-ttu-id="9297b-146">Bir metin düzenleyicisi kullanarak hello açın `pom.xml` hello dosyasında `read-file-upload-notification` klasörü ve bağımlılık toohello aşağıdaki hello ekleyin **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="9297b-146">Using a text editor, open hello `pom.xml` file in hello `read-file-upload-notification` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="9297b-147">Merhaba bağımlılık ekleme sağlar toouse hello **iothub-java-service-client** , uygulama toocommunicate IOT hub hizmetinizle paketinde:</span><span class="sxs-lookup"><span data-stu-id="9297b-147">Adding hello dependency enables you toouse hello **iothub-java-service-client** package in your application toocommunicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="9297b-148">Hello için en son sürümünü denetleyebilir **IOT hizmeti istemcisi** kullanarak [Maven arama](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="9297b-148">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="9297b-149">Kaydet ve Kapat hello `pom.xml` dosya.</span><span class="sxs-lookup"><span data-stu-id="9297b-149">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="9297b-150">Bir metin düzenleyicisi kullanarak hello açın `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` dosya.</span><span class="sxs-lookup"><span data-stu-id="9297b-150">Using a text editor, open hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="9297b-151">Merhaba aşağıdakileri ekleyin **alma** deyimleri toohello dosyası:</span><span class="sxs-lookup"><span data-stu-id="9297b-151">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;
    ```

1. <span data-ttu-id="9297b-152">Aşağıdaki sınıf düzeyi değişkenleri toohello hello eklemek **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="9297b-152">Add hello following class-level variables toohello **App** class:</span></span>

    ```java
    private static final String connectionString = "{Your IoT Hub connection string}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    private static FileUploadNotificationReceiver fileUploadNotificationReceiver = null;
    ```

1. <span data-ttu-id="9297b-153">Merhaba dosya karşıya yükleme toohello Konsolu hakkında tooprint bilgi eklemek hello aşağıdaki iç içe geçmiş sınıf toohello **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="9297b-153">tooprint information about hello file upload toohello console, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="9297b-154">dosya karşıya yükleme bildirimleri için dinler toostart hello iş parçacığı ekleme kodu toohello aşağıdaki hello **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="9297b-154">toostart hello thread that listens for file upload notifications, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="9297b-155">Kaydet ve Kapat hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` dosya.</span><span class="sxs-lookup"><span data-stu-id="9297b-155">Save and close hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="9297b-156">Kullanım hello şu komutu toobuild hello **dosya karşıya yükleme bildirimi okuma** uygulama ve hataları denetleyin:</span><span class="sxs-lookup"><span data-stu-id="9297b-156">Use hello following command toobuild hello **read-file-upload-notification** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="9297b-157">Merhaba uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9297b-157">Run hello applications</span></span>

<span data-ttu-id="9297b-158">Hazır toorun hello uygulamaları sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="9297b-158">Now you are ready toorun hello applications.</span></span>

<span data-ttu-id="9297b-159">Bir komut isteminde hello `read-file-upload-notification` klasörü, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9297b-159">At a command prompt in hello `read-file-upload-notification` folder, run hello following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="9297b-160">Bir komut isteminde hello `simulated-device` klasörü, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9297b-160">At a command prompt in hello `simulated-device` folder, run hello following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="9297b-161">Merhaba aşağıdaki ekran görüntüsünde hello çıktısını hello gösterir **simulated-device** uygulama:</span><span class="sxs-lookup"><span data-stu-id="9297b-161">hello following screenshot shows hello output from hello **simulated-device** app:</span></span>

![Simulated-device uygulamadan çıktı](media/iot-hub-java-java-upload/simulated-device.png)

<span data-ttu-id="9297b-163">Merhaba aşağıdaki ekran görüntüsünde hello çıktısını hello gösterir **dosya karşıya yükleme bildirimi okuma** uygulama:</span><span class="sxs-lookup"><span data-stu-id="9297b-163">hello following screenshot shows hello output from hello **read-file-upload-notification** app:</span></span>

![Dosya karşıya yükleme bildirimi okuma uygulamadan çıktı](media/iot-hub-java-java-upload/read-file-upload-notification.png)

<span data-ttu-id="9297b-165">Merhaba portal tooview karşıya hello yapılandırdığınız hello depolama kapsayıcısı dosyasında kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9297b-165">You can use hello portal tooview hello uploaded file in hello storage container you configured:</span></span>

![Yüklenen dosya](media/iot-hub-java-java-upload/uploaded-file.png)

## <a name="next-steps"></a><span data-ttu-id="9297b-167">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9297b-167">Next steps</span></span>

<span data-ttu-id="9297b-168">Bu öğreticide, nasıl toouse hello dosyayı karşıya IOT Hub'ın cihazlardan toosimplify dosya yüklemeleri yeteneklerini öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="9297b-168">In this tutorial, you learned how toouse hello file upload capabilities of IoT Hub toosimplify file uploads from devices.</span></span> <span data-ttu-id="9297b-169">Aşağıdaki makaleleri hello ile tooexplore IOT hub özellikleri ve senaryoları devam edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9297b-169">You can continue tooexplore IoT hub features and scenarios with hello following articles:</span></span>

* <span data-ttu-id="9297b-170">[IOT hub'ı program aracılığıyla oluşturma][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="9297b-170">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="9297b-171">[Giriş tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="9297b-171">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="9297b-172">[Azure IOT SDK'ları][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="9297b-172">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="9297b-173">toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:</span><span class="sxs-lookup"><span data-stu-id="9297b-173">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="9297b-174">[Bir cihaz IOT Edge benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="9297b-174">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

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


