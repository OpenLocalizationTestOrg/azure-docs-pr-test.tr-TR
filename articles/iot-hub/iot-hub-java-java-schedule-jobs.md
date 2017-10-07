---
title: "Azure IOT hub'ı (Java) aaaSchedule işleriyle | Microsoft Docs"
description: "Nasıl tooschedule Azure IOT Hub tooinvoke doğrudan bir yöntem iş ve birden fazla cihazda istenen bir özellik Ayarla. Java tooimplement benzetimli hello cihaz uygulamaları ve hello Java tooimplement bir hizmeti uygulama toorun hello işi için Azure IOT hizmeti SDK'sı için hello Azure IOT cihaz SDK'sını kullanın."
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
ms.date: 07/10/2017
ms.author: dobett
ms.openlocfilehash: b1b05fa56c3ce96af0b33d4cca0dd54da0f4e927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-java"></a>Zamanlama ve yayın işleri (Java)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

Milyonlarca cihaza güncelleştirme Azure IOT Hub tooschedule ve izleme işlemlerini kullanın. İşlerini kullanın:

* İstenen özellikleri güncelleştirme
* Güncelleştirme etiketleri
* Doğrudan yöntemleri çağırma

Bir işi şu eylemlerden birini sarmalar ve bir cihaz kümesi karşı yürütme parçaları hello. Cihaz çifti sorgu karşı hello iş yürütür aygıtları hello kümesini tanımlar. Örneğin, bir arka uç uygulaması iş tooinvoke doğrudan bir yöntem hello aygıtları yeniden 10.000 cihazlarda kullanabilirsiniz. Cihaz hello kümesini içeren bir cihaz çifti sorgu belirtin ve gelecek bir zamanda hello iş toorun zamanlayın. Merhaba parçaları ilerleyişini her hello aygıtların almak ve hello yeniden başlatma doğrudan yöntemi yürütün.

Bu özelliklerin her biri hakkında daha fazla toolearn bakın:

* Cihaz çifti ve özellikleri: [cihaz çiftlerini ile çalışmaya başlama](iot-hub-java-java-twin-getstarted.md)
* Doğrudan yöntemleri: [IOT Hub Geliştirici Kılavuzu - doğrudan yöntemleri](iot-hub-devguide-direct-methods.md) ve [Öğreticisi: doğrudan yöntemleri kullanın](iot-hub-java-java-direct-methods.md)

Bu öğretici şunların nasıl yapıldığını gösterir:

* Adlı doğrudan bir yöntem uygulayan bir cihaz uygulaması oluşturma **lockDoor**. Merhaba cihaz uygulaması istenen özellik değişikliklerini hello arka uç uygulamasını da alır.
* Bir iş toocall hello oluşturan bir arka uç uygulaması oluşturma **lockDoor** birden fazla cihazda yöntemi doğrudan. Başka bir iş, istenen özelliği toomultiple aygıtları güncelleştirir gönderir.

Bu öğreticinin Hello sonunda, bir java konsol cihaz uygulaması ve bir java konsol arka uç uygulaması sahiptir:

**simulated-device** tooyour IOT hub'a bağlandığında, uygulayan hello **lockDoor** yöntemi ve tanıtıcıları istenen özellik değişikliklerini doğrudan.

**İşleri Zamanla** işleri toocall hello kullan **lockDoor** doğrudan yöntemi ve güncelleştirme hello cihaz çifti istenen birden çok cihazı özellikleri.

> [!NOTE]
> Merhaba makale [Azure IOT SDK'ları](iot-hub-devguide-sdks.md) toobuild kullanabileceğiniz hello Azure IOT SDK'ları hakkında bilgi sağlayan cihaz ve arka uç uygulamalar.

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu öğretici, gerekir:

* Merhaba son [Java SE Geliştirme Seti 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Etkin bir Azure hesabı. (Bir hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz bir hesap](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Program aracılığıyla toocreate hello cihaz kimliği tercih ederseniz, hello hello ilgili bölümünü okuyun [Java kullanarak aygıt tooyour IOT hub'ınıza bağlanmak](iot-hub-java-java-getstarted.md#create-a-device-identity) makalesi. Merhaba de kullanabilirsiniz [iothub-explorer](https://github.com/Azure/iothub-explorer) aracı tooadd bir aygıt tooyour IOT hub'ı.

## <a name="create-hello-service-app"></a>Merhaba service uygulaması oluşturma

Bu bölümde, işleri kullanan bir Java konsol uygulaması oluşturun:

* Merhaba çağrısı **lockDoor** birden fazla cihazda yöntemi doğrudan.
* İstenen özelliklerde toomultiple aygıtları gönderin.

toocreate hello uygulama:

1. Geliştirme makinenizde adlı boş bir klasör oluşturun `iot-java-schedule-jobs`.

1. Merhaba, `iot-java-schedule-jobs` klasörünü adlı bir Maven projesi oluşturun **işleri zamanla** komutu, komut isteminde aşağıdaki hello kullanarak. Bunun tek ve uzun bir komut olduğunu unutmayın:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=schedule-jobs -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Komut isteminizde toohello gidin `schedule-jobs` klasör.

1. Bir metin düzenleyicisi kullanarak hello açın `pom.xml` hello dosyasında `schedule-jobs` klasörü ve bağımlılık toohello aşağıdaki hello ekleyin **bağımlılıkları** düğümü. Bu bağımlılık toouse hello etkinleştirir **IOT hizmeti istemcisi** , uygulama toocommunicate IOT hub'ınızı ile paketinde:

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

1. Bir metin düzenleyicisi kullanarak hello açın `schedule-jobs\src\main\java\com\mycompany\app\App.java` dosya.

1. Merhaba aşağıdakileri ekleyin **alma** deyimleri toohello dosyası:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;
    import com.microsoft.azure.sdk.iot.service.devicetwin.Pair;
    import com.microsoft.azure.sdk.iot.service.devicetwin.Query;
    import com.microsoft.azure.sdk.iot.service.devicetwin.SqlQuery;
    import com.microsoft.azure.sdk.iot.service.jobs.JobClient;
    import com.microsoft.azure.sdk.iot.service.jobs.JobResult;
    import com.microsoft.azure.sdk.iot.service.jobs.JobStatus;

    import java.util.Date;
    import java.time.Instant;
    import java.util.HashSet;
    import java.util.Set;
    import java.util.UUID;
    ```

1. Aşağıdaki sınıf düzeyi değişkenleri toohello hello eklemek **uygulama** sınıfı. Değiştir `{youriothubconnectionstring}` hello ettiğiniz, IOT hub bağlantı dizesine sahip *IOT Hub oluşturma* bölümü:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    // How long hello job is permitted toorun without
    // completing its work on hello set of devices
    private static final long maxExecutionTimeInSeconds = 30;
    ```

1. Yöntem toohello aşağıdaki hello eklemek **uygulama** sınıfı tooschedule iş tooupdate hello **yapı** ve **kat** hello cihaz çifti özelliklerinde istenen:

    ```java
    private static JobResult scheduleJobSetDesiredProperties(JobClient jobClient, String jobId) {
      DeviceTwinDevice twin = new DeviceTwinDevice(deviceId);
      Set<Pair> desiredProperties = new HashSet<Pair>();
      desiredProperties.add(new Pair("Building", 43));
      desiredProperties.add(new Pair("Floor", 3));
      twin.setDesiredProperties(desiredProperties);
      // Optimistic concurrency control
      twin.setETag("*");

      // Schedule hello update twin job toorun now
      // against a single device
      System.out.println("Schedule job " + jobId + " for device " + deviceId);
      try {
        JobResult jobResult = jobClient.scheduleUpdateTwin(jobId, 
          "deviceId='" + deviceId + "'",
          twin,
          new Date(),
          maxExecutionTimeInSeconds);
        return jobResult;
      } catch (Exception e) {
        System.out.println("Exception scheduling desired properties job: " + jobId);
        System.out.println(e.getMessage());
        return null;
      }
    }
    ```

1. tooschedule iş toocall hello **lockDoor** yöntemi, yöntem toohello aşağıdaki hello eklemek **uygulama** sınıfı:

    ```java
    private static JobResult scheduleJobCallDirectMethod(JobClient jobClient, String jobId) {
      // Schedule a job now toocall hello lockDoor direct method
      // against a single device. Response and connection
      // timeouts are set too5 seconds.
      System.out.println("Schedule job " + jobId + " for device " + deviceId);
      try {
        JobResult jobResult = jobClient.scheduleDeviceMethod(jobId,
          "deviceId='" + deviceId + "'",
          "lockDoor",
          5L, 5L, null,
          new Date(),
          maxExecutionTimeInSeconds);
        return jobResult;
      } catch (Exception e) {
        System.out.println("Exception scheduling direct method job: " + jobId);
        System.out.println(e.getMessage());
        return null;
      }
    };
    ```

1. toomonitor bir işi ekleme yöntemi toohello aşağıdaki hello **uygulama** sınıfı:

    ```java
    private static void monitorJob(JobClient jobClient, String jobId) {
      try {
        JobResult jobResult = jobClient.getJob(jobId);
        if(jobResult == null)
        {
          System.out.println("No JobResult for: " + jobId);
          return;
        }
        // Check hello job result until it's completed
        while(jobResult.getJobStatus() != JobStatus.completed)
        {
          Thread.sleep(100);
          jobResult = jobClient.getJob(jobId);
          System.out.println("Status " + jobResult.getJobStatus() + " for job " + jobId);
        }
        System.out.println("Final status " + jobResult.getJobStatus() + " for job " + jobId);
      } catch (Exception e) {
        System.out.println("Exception monitoring job: " + jobId);
        System.out.println(e.getMessage());
        return;
      }
    }
    ```

1. çalıştırdığınız, hello işlerinin hello ayrıntılarını tooquery yöntemi aşağıdaki hello ekleyin:

    ```java
    private static void queryDeviceJobs(JobClient jobClient, String start) throws Exception {
      System.out.println("\nQuery device jobs since " + start);

      // Create a jobs query using hello time hello jobs started
      Query deviceJobQuery = jobClient
          .queryDeviceJob(SqlQuery.createSqlQuery("*", SqlQuery.FromType.JOBS, "devices.jobs.startTimeUtc > '" + start + "'", null).getQuery());

      // Iterate over hello list of jobs and print hello details
      while (jobClient.hasNextJob(deviceJobQuery)) {
        System.out.println(jobClient.getNextJob(deviceJobQuery));
      }
    }
    ```

1. Güncelleştirme hello **ana** yöntemi imza tooinclude hello aşağıdaki `throws` yan tümcesi:

    ```java
    public static void main( String[] args ) throws Exception
    ```

1. toorun ve İzleyici iki işler sırayla, kod toohello aşağıdaki hello eklemek **ana** yöntemi:

    ```java
    // Record hello start time
    String start = Instant.now().toString();

    // Create JobClient
    JobClient jobClient = JobClient.createFromConnectionString(iotHubConnectionString);
    System.out.println("JobClient created with success");

    // Schedule twin job desired properties
    // Maximum concurrent jobs is 1 for Free and S1 tiers
    String desiredPropertiesJobId = "DPCMD" + UUID.randomUUID();
    scheduleJobSetDesiredProperties(jobClient, desiredPropertiesJobId);
    monitorJob(jobClient, desiredPropertiesJobId);

    // Schedule twin job direct method
    String directMethodJobId = "DMCMD" + UUID.randomUUID();
    scheduleJobCallDirectMethod(jobClient, directMethodJobId);
    monitorJob(jobClient, directMethodJobId);

    // Run a query tooshow hello job detail
    queryDeviceJobs(jobClient, start);

    System.out.println("Shutting down schedule-jobs app");
    ```

1. Kaydet ve Kapat hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` dosyası

1. Merhaba yapı **işleri zamanla** uygulama ve olan hataları düzeltin. Komut isteminizde toohello gidin `schedule-jobs` klasörü ve aşağıdaki komutu çalıştırın hello:

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a>Cihaz uygulaması oluşturma

Bu bölümde IOT Hub ve Implements hello doğrudan yöntem çağrısının gönderilen istenen özellikleri tanıtıcıları hello bir Java konsol uygulaması oluşturun.

1. Merhaba, `iot-java-schedule-jobs` klasörünü adlı bir Maven projesi oluşturun **simulated-device** komutu, komut isteminde aşağıdaki hello kullanarak. Bunun tek ve uzun bir komut olduğunu unutmayın:

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
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    Bu örnek uygulama hello kullanan **Protokolü** değişkenini bir **DeviceClient** nesnesi. Merhaba MQTT protokol kullanmanız gereken şu anda toouse cihaz çifti özellikleri.

1. tooprint cihaz çifti bildirimleri toohello konsolunda, hello aşağıdakileri ekleyin iç içe geçmiş sınıf toohello **uygulama** sınıfı:

    ```java
    // Handler for device twin operation notifications from IoT Hub
    protected static class DeviceTwinStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
      }
    }
    ```

1. tooprint doğrudan yöntemi bildirimleri toohello konsolunda, hello aşağıdakileri ekleyin iç içe geçmiş sınıf toohello **uygulama** sınıfı:

    ```java
    // Handler for direct method notifications from IoT Hub
    protected static class DirectMethodStatusCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodirect method operation with status " + status.name());
      }
    }
    ```

1. IOT hub'ı gelen toohandle doğrudan yöntem çağrıları ekleme hello aşağıdaki iç içe geçmiş sınıf toohello **uygulama** sınıfı:

    ```java
    // Handler for direct method calls from IoT Hub
    protected static class DirectMethodCallback
        implements DeviceMethodCallback {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context) {
        DeviceMethodData deviceMethodData;
        switch (methodName) {
          case "lockDoor": {
            System.out.println("Executing direct method: " + methodName);
            deviceMethodData = new DeviceMethodData(METHOD_SUCCESS, "Executed direct method " + methodName);
            break;
          }
          default: {
            deviceMethodData = new DeviceMethodData(METHOD_NOT_DEFINED, "Not defined direct method " + methodName);
          }
        }
        // Notify IoT Hub of result
        return deviceMethodData;
      }
    }
    ```

1. Güncelleştirme hello **ana** yöntemi imza tooinclude hello aşağıdaki `throws` yan tümcesi:

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException
    ```

1. Aşağıdaki kodu toohello hello eklemek **ana** yöntemi için:
    * Aygıt istemci toocommunicate IOT Hub ile oluşturun.
    * Oluşturma bir **aygıt** nesne toostore hello cihaz çifti özellikleri.

    ```java
    // Create a device client
    DeviceClient client = new DeviceClient(connString, protocol);

    // An object toomanage device twin desired and reported properties
    Device dataCollector = new Device() {
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context)
      {
        System.out.println("Received desired property change: " + propertyKey + " " + propertyValue);
      }
    };
    ```

1. toostart hello aygıt istemci hizmetlerini ekleme kodu toohello aşağıdaki hello **ana** yöntemi:

    ```java
    try {
      // Open hello DeviceClient
      // Start hello device twin services
      // Subscribe toodirect method calls
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
    } catch (Exception e) {
      System.out.println("Exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.closeNow();
      System.out.println("Shutting down...");
    }
    ```

1. Merhaba kullanıcı toopress hello toowait **Enter** anahtar kapatmadan önce kod toohello hello sonuna aşağıdaki hello eklemek **ana** yöntemi:

    ```java
    // Close hello app
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    dataCollector.clean();
    client.closeNow();
    scanner.close();
    ```

1. Kaydet ve Kapat hello `simulated-device\src\main\java\com\mycompany\app\App.java` dosya.

1. Merhaba yapı **simulated-device** uygulama ve olan hataları düzeltin. Komut isteminizde toohello gidin `simulated-device` klasörü ve aşağıdaki komutu çalıştırın hello:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Merhaba uygulamaları çalıştırma

Hazır toorun hello konsol uygulamaları sunulmuştur.

1. Bir komut isteminde hello `simulated-device` klasörü, istenen özellik değişikliklerini ve doğrudan yöntem çağrıları için dinleme komutu toostart hello cihaz uygulaması aşağıdaki hello çalıştırın:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Merhaba aygıt istemcisi başlatır](media/iot-hub-java-java-schedule-jobs/device-app-1.png)

1. Bir komut isteminde hello `schedule-jobs` klasörüne komutu toorun hello aşağıdaki Merhaba, **işleri zamanla** uygulama toorun iki işleri hizmet. Merhaba ilk istenen hello özellik değerlerini ayarlar, doğrudan yöntemi hello ikinci çağrıları hello:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IOT Hub hizmeti uygulaması iki işleri oluşturur](media/iot-hub-java-java-schedule-jobs/service-app-1.png)

1. Merhaba cihaz uygulaması istenen hello özellik değişikliği ve hello doğrudan yöntem çağrısı işler:

    ![Merhaba aygıt istemcisi toohello değişiklikleri yanıt veriyor](media/iot-hub-java-java-schedule-jobs/device-app-2.png)

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide hello Azure portalında yeni bir IOT hub yapılandırılmış ve ardından hello IOT hub'ın kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz. Bir arka uç uygulaması toorun iki işi oluşturuldu. İstenen özellik değerlerini ve doğrudan bir yöntem olarak adlandırılan hello ikinci işi Hello ilk iş ayarlayın.

Kaynakları toolearn nasıl aşağıdaki kullanım hello için:

* Merhaba aygıtlarla telemetri gönderen [IOT Hub ile çalışmaya başlama](iot-hub-java-java-getstarted.md) Öğreticisi.
* Merhaba ile etkileşimli olarak (örneğin, kullanıcı tarafından denetlenen bir uygulamadan fan etkinleştirdikten) cihazları denetleme [doğrudan yöntemleri kullanın](iot-hub-java-java-direct-methods.md) Öğreticisi.
