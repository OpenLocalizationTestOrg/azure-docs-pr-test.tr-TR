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
# <a name="schedule-and-broadcast-jobs-java"></a><span data-ttu-id="186cb-104">Zamanlama ve yayın işleri (Java)</span><span class="sxs-lookup"><span data-stu-id="186cb-104">Schedule and broadcast jobs (Java)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="186cb-105">Milyonlarca cihaza güncelleştirme Azure IOT Hub tooschedule ve izleme işlemlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="186cb-105">Use Azure IoT Hub tooschedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="186cb-106">İşlerini kullanın:</span><span class="sxs-lookup"><span data-stu-id="186cb-106">Use jobs to:</span></span>

* <span data-ttu-id="186cb-107">İstenen özellikleri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="186cb-107">Update desired properties</span></span>
* <span data-ttu-id="186cb-108">Güncelleştirme etiketleri</span><span class="sxs-lookup"><span data-stu-id="186cb-108">Update tags</span></span>
* <span data-ttu-id="186cb-109">Doğrudan yöntemleri çağırma</span><span class="sxs-lookup"><span data-stu-id="186cb-109">Invoke direct methods</span></span>

<span data-ttu-id="186cb-110">Bir işi şu eylemlerden birini sarmalar ve bir cihaz kümesi karşı yürütme parçaları hello.</span><span class="sxs-lookup"><span data-stu-id="186cb-110">A job wraps one of these actions and tracks hello execution against a set of devices.</span></span> <span data-ttu-id="186cb-111">Cihaz çifti sorgu karşı hello iş yürütür aygıtları hello kümesini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="186cb-111">A device twin query defines hello set of devices hello job executes against.</span></span> <span data-ttu-id="186cb-112">Örneğin, bir arka uç uygulaması iş tooinvoke doğrudan bir yöntem hello aygıtları yeniden 10.000 cihazlarda kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="186cb-112">For example, a back-end app can use a job tooinvoke a direct method on 10,000 devices that reboots hello devices.</span></span> <span data-ttu-id="186cb-113">Cihaz hello kümesini içeren bir cihaz çifti sorgu belirtin ve gelecek bir zamanda hello iş toorun zamanlayın.</span><span class="sxs-lookup"><span data-stu-id="186cb-113">You specify hello set of devices with a device twin query and schedule hello job toorun at a future time.</span></span> <span data-ttu-id="186cb-114">Merhaba parçaları ilerleyişini her hello aygıtların almak ve hello yeniden başlatma doğrudan yöntemi yürütün.</span><span class="sxs-lookup"><span data-stu-id="186cb-114">hello job tracks progress as each of hello devices receive and execute hello reboot direct method.</span></span>

<span data-ttu-id="186cb-115">Bu özelliklerin her biri hakkında daha fazla toolearn bakın:</span><span class="sxs-lookup"><span data-stu-id="186cb-115">toolearn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="186cb-116">Cihaz çifti ve özellikleri: [cihaz çiftlerini ile çalışmaya başlama](iot-hub-java-java-twin-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="186cb-116">Device twin and properties: [Get started with device twins](iot-hub-java-java-twin-getstarted.md)</span></span>
* <span data-ttu-id="186cb-117">Doğrudan yöntemleri: [IOT Hub Geliştirici Kılavuzu - doğrudan yöntemleri](iot-hub-devguide-direct-methods.md) ve [Öğreticisi: doğrudan yöntemleri kullanın](iot-hub-java-java-direct-methods.md)</span><span class="sxs-lookup"><span data-stu-id="186cb-117">Direct methods: [IoT Hub developer guide - direct methods](iot-hub-devguide-direct-methods.md) and [Tutorial: Use direct methods](iot-hub-java-java-direct-methods.md)</span></span>

<span data-ttu-id="186cb-118">Bu öğretici şunların nasıl yapıldığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="186cb-118">This tutorial shows you how to:</span></span>

* <span data-ttu-id="186cb-119">Adlı doğrudan bir yöntem uygulayan bir cihaz uygulaması oluşturma **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="186cb-119">Create a device app that implements a direct method called **lockDoor**.</span></span> <span data-ttu-id="186cb-120">Merhaba cihaz uygulaması istenen özellik değişikliklerini hello arka uç uygulamasını da alır.</span><span class="sxs-lookup"><span data-stu-id="186cb-120">hello device app also receives desired property changes from hello back-end app.</span></span>
* <span data-ttu-id="186cb-121">Bir iş toocall hello oluşturan bir arka uç uygulaması oluşturma **lockDoor** birden fazla cihazda yöntemi doğrudan.</span><span class="sxs-lookup"><span data-stu-id="186cb-121">Create a back-end app that creates a job toocall hello **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="186cb-122">Başka bir iş, istenen özelliği toomultiple aygıtları güncelleştirir gönderir.</span><span class="sxs-lookup"><span data-stu-id="186cb-122">Another job sends desired property updates toomultiple devices.</span></span>

<span data-ttu-id="186cb-123">Bu öğreticinin Hello sonunda, bir java konsol cihaz uygulaması ve bir java konsol arka uç uygulaması sahiptir:</span><span class="sxs-lookup"><span data-stu-id="186cb-123">At hello end of this tutorial, you have a java console device app and a java console back-end app:</span></span>

<span data-ttu-id="186cb-124">**simulated-device** tooyour IOT hub'a bağlandığında, uygulayan hello **lockDoor** yöntemi ve tanıtıcıları istenen özellik değişikliklerini doğrudan.</span><span class="sxs-lookup"><span data-stu-id="186cb-124">**simulated-device** that connects tooyour IoT hub, implements hello **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="186cb-125">**İşleri Zamanla** işleri toocall hello kullan **lockDoor** doğrudan yöntemi ve güncelleştirme hello cihaz çifti istenen birden çok cihazı özellikleri.</span><span class="sxs-lookup"><span data-stu-id="186cb-125">**schedule-jobs** that use jobs toocall hello **lockDoor** direct method and update hello device twin desired properties on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="186cb-126">Merhaba makale [Azure IOT SDK'ları](iot-hub-devguide-sdks.md) toobuild kullanabileceğiniz hello Azure IOT SDK'ları hakkında bilgi sağlayan cihaz ve arka uç uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="186cb-126">hello article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="186cb-127">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="186cb-127">Prerequisites</span></span>

<span data-ttu-id="186cb-128">toocomplete Bu öğretici, gerekir:</span><span class="sxs-lookup"><span data-stu-id="186cb-128">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="186cb-129">Merhaba son [Java SE Geliştirme Seti 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="186cb-129">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="186cb-130">Maven 3</span><span class="sxs-lookup"><span data-stu-id="186cb-130">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="186cb-131">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="186cb-131">An active Azure account.</span></span> <span data-ttu-id="186cb-132">(Bir hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz bir hesap](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.)</span><span class="sxs-lookup"><span data-stu-id="186cb-132">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="186cb-133">Program aracılığıyla toocreate hello cihaz kimliği tercih ederseniz, hello hello ilgili bölümünü okuyun [Java kullanarak aygıt tooyour IOT hub'ınıza bağlanmak](iot-hub-java-java-getstarted.md#create-a-device-identity) makalesi.</span><span class="sxs-lookup"><span data-stu-id="186cb-133">If you prefer toocreate hello device identity programmatically, read hello corresponding section in hello [Connect your device tooyour IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span> <span data-ttu-id="186cb-134">Merhaba de kullanabilirsiniz [iothub-explorer](https://github.com/Azure/iothub-explorer) aracı tooadd bir aygıt tooyour IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="186cb-134">You can also use hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool tooadd a device tooyour IoT hub.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="186cb-135">Merhaba service uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="186cb-135">Create hello service app</span></span>

<span data-ttu-id="186cb-136">Bu bölümde, işleri kullanan bir Java konsol uygulaması oluşturun:</span><span class="sxs-lookup"><span data-stu-id="186cb-136">In this section, you create a Java console app that uses jobs to:</span></span>

* <span data-ttu-id="186cb-137">Merhaba çağrısı **lockDoor** birden fazla cihazda yöntemi doğrudan.</span><span class="sxs-lookup"><span data-stu-id="186cb-137">Call hello **lockDoor** direct method on multiple devices.</span></span>
* <span data-ttu-id="186cb-138">İstenen özelliklerde toomultiple aygıtları gönderin.</span><span class="sxs-lookup"><span data-stu-id="186cb-138">Send desired properties toomultiple devices.</span></span>

<span data-ttu-id="186cb-139">toocreate hello uygulama:</span><span class="sxs-lookup"><span data-stu-id="186cb-139">toocreate hello app:</span></span>

1. <span data-ttu-id="186cb-140">Geliştirme makinenizde adlı boş bir klasör oluşturun `iot-java-schedule-jobs`.</span><span class="sxs-lookup"><span data-stu-id="186cb-140">On your development machine, create an empty folder called `iot-java-schedule-jobs`.</span></span>

1. <span data-ttu-id="186cb-141">Merhaba, `iot-java-schedule-jobs` klasörünü adlı bir Maven projesi oluşturun **işleri zamanla** komutu, komut isteminde aşağıdaki hello kullanarak.</span><span class="sxs-lookup"><span data-stu-id="186cb-141">In hello `iot-java-schedule-jobs` folder, create a Maven project called **schedule-jobs** using hello following command at your command prompt.</span></span> <span data-ttu-id="186cb-142">Bunun tek ve uzun bir komut olduğunu unutmayın:</span><span class="sxs-lookup"><span data-stu-id="186cb-142">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=schedule-jobs -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="186cb-143">Komut isteminizde toohello gidin `schedule-jobs` klasör.</span><span class="sxs-lookup"><span data-stu-id="186cb-143">At your command prompt, navigate toohello `schedule-jobs` folder.</span></span>

1. <span data-ttu-id="186cb-144">Bir metin düzenleyicisi kullanarak hello açın `pom.xml` hello dosyasında `schedule-jobs` klasörü ve bağımlılık toohello aşağıdaki hello ekleyin **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="186cb-144">Using a text editor, open hello `pom.xml` file in hello `schedule-jobs` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="186cb-145">Bu bağımlılık toouse hello etkinleştirir **IOT hizmeti istemcisi** , uygulama toocommunicate IOT hub'ınızı ile paketinde:</span><span class="sxs-lookup"><span data-stu-id="186cb-145">This dependency enables you toouse hello **iot-service-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="186cb-146">Hello için en son sürümünü denetleyebilir **IOT hizmeti istemcisi** kullanarak [Maven arama](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="186cb-146">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="186cb-147">Merhaba aşağıdakileri ekleyin **yapı** düğümünden hello sonraki **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="186cb-147">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="186cb-148">Bu yapılandırma, Maven toouse Java 1.8 toobuild hello uygulaması bildirir:</span><span class="sxs-lookup"><span data-stu-id="186cb-148">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="186cb-149">Kaydet ve Kapat hello `pom.xml` dosya.</span><span class="sxs-lookup"><span data-stu-id="186cb-149">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="186cb-150">Bir metin düzenleyicisi kullanarak hello açın `schedule-jobs\src\main\java\com\mycompany\app\App.java` dosya.</span><span class="sxs-lookup"><span data-stu-id="186cb-150">Using a text editor, open hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="186cb-151">Merhaba aşağıdakileri ekleyin **alma** deyimleri toohello dosyası:</span><span class="sxs-lookup"><span data-stu-id="186cb-151">Add hello following **import** statements toohello file:</span></span>

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

1. <span data-ttu-id="186cb-152">Aşağıdaki sınıf düzeyi değişkenleri toohello hello eklemek **uygulama** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="186cb-152">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="186cb-153">Değiştir `{youriothubconnectionstring}` hello ettiğiniz, IOT hub bağlantı dizesine sahip *IOT Hub oluşturma* bölümü:</span><span class="sxs-lookup"><span data-stu-id="186cb-153">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    // How long hello job is permitted toorun without
    // completing its work on hello set of devices
    private static final long maxExecutionTimeInSeconds = 30;
    ```

1. <span data-ttu-id="186cb-154">Yöntem toohello aşağıdaki hello eklemek **uygulama** sınıfı tooschedule iş tooupdate hello **yapı** ve **kat** hello cihaz çifti özelliklerinde istenen:</span><span class="sxs-lookup"><span data-stu-id="186cb-154">Add hello following method toohello **App** class tooschedule a job tooupdate hello **Building** and **Floor** desired properties in hello device twin:</span></span>

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

1. <span data-ttu-id="186cb-155">tooschedule iş toocall hello **lockDoor** yöntemi, yöntem toohello aşağıdaki hello eklemek **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="186cb-155">tooschedule a job toocall hello **lockDoor** method, add hello following method toohello **App** class:</span></span>

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

1. <span data-ttu-id="186cb-156">toomonitor bir işi ekleme yöntemi toohello aşağıdaki hello **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="186cb-156">toomonitor a job, add hello following method toohello **App** class:</span></span>

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

1. <span data-ttu-id="186cb-157">çalıştırdığınız, hello işlerinin hello ayrıntılarını tooquery yöntemi aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="186cb-157">tooquery for hello details of hello jobs you ran, add hello following method:</span></span>

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

1. <span data-ttu-id="186cb-158">Güncelleştirme hello **ana** yöntemi imza tooinclude hello aşağıdaki `throws` yan tümcesi:</span><span class="sxs-lookup"><span data-stu-id="186cb-158">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws Exception
    ```

1. <span data-ttu-id="186cb-159">toorun ve İzleyici iki işler sırayla, kod toohello aşağıdaki hello eklemek **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="186cb-159">toorun and monitor two jobs sequentially, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="186cb-160">Kaydet ve Kapat hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` dosyası</span><span class="sxs-lookup"><span data-stu-id="186cb-160">Save and close hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="186cb-161">Merhaba yapı **işleri zamanla** uygulama ve olan hataları düzeltin.</span><span class="sxs-lookup"><span data-stu-id="186cb-161">Build hello **schedule-jobs** app and correct any errors.</span></span> <span data-ttu-id="186cb-162">Komut isteminizde toohello gidin `schedule-jobs` klasörü ve aşağıdaki komutu çalıştırın hello:</span><span class="sxs-lookup"><span data-stu-id="186cb-162">At your command prompt, navigate toohello `schedule-jobs` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="186cb-163">Cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="186cb-163">Create a device app</span></span>

<span data-ttu-id="186cb-164">Bu bölümde IOT Hub ve Implements hello doğrudan yöntem çağrısının gönderilen istenen özellikleri tanıtıcıları hello bir Java konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="186cb-164">In this section, you create a Java console app that handles hello desired properties sent from IoT Hub and implements hello direct method call.</span></span>

1. <span data-ttu-id="186cb-165">Merhaba, `iot-java-schedule-jobs` klasörünü adlı bir Maven projesi oluşturun **simulated-device** komutu, komut isteminde aşağıdaki hello kullanarak.</span><span class="sxs-lookup"><span data-stu-id="186cb-165">In hello `iot-java-schedule-jobs` folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="186cb-166">Bunun tek ve uzun bir komut olduğunu unutmayın:</span><span class="sxs-lookup"><span data-stu-id="186cb-166">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="186cb-167">Komut isteminizde toohello gidin `simulated-device` klasör.</span><span class="sxs-lookup"><span data-stu-id="186cb-167">At your command prompt, navigate toohello `simulated-device` folder.</span></span>

1. <span data-ttu-id="186cb-168">Bir metin düzenleyicisi kullanarak hello açın `pom.xml` hello dosyasında `simulated-device` klasörü ve bağımlılıkları toohello aşağıdaki hello ekleyin **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="186cb-168">Using a text editor, open hello `pom.xml` file in hello `simulated-device` folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="186cb-169">Bu bağımlılık toouse hello etkinleştirir **IOT cihaz istemci** , uygulama toocommunicate IOT hub'ınızı ile paketinde:</span><span class="sxs-lookup"><span data-stu-id="186cb-169">This dependency enables you toouse hello **iot-device-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="186cb-170">Hello için en son sürümünü denetleyebilir **IOT cihaz istemci** kullanarak [Maven arama](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="186cb-170">You can check for hello latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="186cb-171">Merhaba aşağıdakileri ekleyin **yapı** düğümünden hello sonraki **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="186cb-171">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="186cb-172">Bu yapılandırma, Maven toouse Java 1.8 toobuild hello uygulaması bildirir:</span><span class="sxs-lookup"><span data-stu-id="186cb-172">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="186cb-173">Kaydet ve Kapat hello `pom.xml` dosya.</span><span class="sxs-lookup"><span data-stu-id="186cb-173">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="186cb-174">Bir metin düzenleyicisi kullanarak hello açın `simulated-device\src\main\java\com\mycompany\app\App.java` dosya.</span><span class="sxs-lookup"><span data-stu-id="186cb-174">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="186cb-175">Merhaba aşağıdakileri ekleyin **alma** deyimleri toohello dosyası:</span><span class="sxs-lookup"><span data-stu-id="186cb-175">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="186cb-176">Aşağıdaki sınıf düzeyi değişkenleri toohello hello eklemek **uygulama** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="186cb-176">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="186cb-177">Değiştirme `{youriothubname}` , IOT hub'ı adıyla ve `{yourdevicekey}` hello oluşturulan hello aygıt anahtarı değerine sahip *bir cihaz kimliği oluşturma* bölümü:</span><span class="sxs-lookup"><span data-stu-id="186cb-177">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="186cb-178">Bu örnek uygulama hello kullanan **Protokolü** değişkenini bir **DeviceClient** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="186cb-178">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="186cb-179">Merhaba MQTT protokol kullanmanız gereken şu anda toouse cihaz çifti özellikleri.</span><span class="sxs-lookup"><span data-stu-id="186cb-179">Currently, toouse device twin features you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="186cb-180">tooprint cihaz çifti bildirimleri toohello konsolunda, hello aşağıdakileri ekleyin iç içe geçmiş sınıf toohello **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="186cb-180">tooprint device twin notifications toohello console, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Handler for device twin operation notifications from IoT Hub
    protected static class DeviceTwinStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="186cb-181">tooprint doğrudan yöntemi bildirimleri toohello konsolunda, hello aşağıdakileri ekleyin iç içe geçmiş sınıf toohello **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="186cb-181">tooprint direct method notifications toohello console, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Handler for direct method notifications from IoT Hub
    protected static class DirectMethodStatusCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodirect method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="186cb-182">IOT hub'ı gelen toohandle doğrudan yöntem çağrıları ekleme hello aşağıdaki iç içe geçmiş sınıf toohello **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="186cb-182">toohandle direct method calls from IoT Hub, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="186cb-183">Güncelleştirme hello **ana** yöntemi imza tooinclude hello aşağıdaki `throws` yan tümcesi:</span><span class="sxs-lookup"><span data-stu-id="186cb-183">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="186cb-184">Aşağıdaki kodu toohello hello eklemek **ana** yöntemi için:</span><span class="sxs-lookup"><span data-stu-id="186cb-184">Add hello following code toohello **main** method to:</span></span>
    * <span data-ttu-id="186cb-185">Aygıt istemci toocommunicate IOT Hub ile oluşturun.</span><span class="sxs-lookup"><span data-stu-id="186cb-185">Create a device client toocommunicate with IoT Hub.</span></span>
    * <span data-ttu-id="186cb-186">Oluşturma bir **aygıt** nesne toostore hello cihaz çifti özellikleri.</span><span class="sxs-lookup"><span data-stu-id="186cb-186">Create a **Device** object toostore hello device twin properties.</span></span>

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

1. <span data-ttu-id="186cb-187">toostart hello aygıt istemci hizmetlerini ekleme kodu toohello aşağıdaki hello **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="186cb-187">toostart hello device client services, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="186cb-188">Merhaba kullanıcı toopress hello toowait **Enter** anahtar kapatmadan önce kod toohello hello sonuna aşağıdaki hello eklemek **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="186cb-188">toowait for hello user toopress hello **Enter** key before shutting down, add hello following code toohello end of hello **main** method:</span></span>

    ```java
    // Close hello app
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    dataCollector.clean();
    client.closeNow();
    scanner.close();
    ```

1. <span data-ttu-id="186cb-189">Kaydet ve Kapat hello `simulated-device\src\main\java\com\mycompany\app\App.java` dosya.</span><span class="sxs-lookup"><span data-stu-id="186cb-189">Save and close hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="186cb-190">Merhaba yapı **simulated-device** uygulama ve olan hataları düzeltin.</span><span class="sxs-lookup"><span data-stu-id="186cb-190">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="186cb-191">Komut isteminizde toohello gidin `simulated-device` klasörü ve aşağıdaki komutu çalıştırın hello:</span><span class="sxs-lookup"><span data-stu-id="186cb-191">At your command prompt, navigate toohello `simulated-device` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="186cb-192">Merhaba uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="186cb-192">Run hello apps</span></span>

<span data-ttu-id="186cb-193">Hazır toorun hello konsol uygulamaları sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="186cb-193">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="186cb-194">Bir komut isteminde hello `simulated-device` klasörü, istenen özellik değişikliklerini ve doğrudan yöntem çağrıları için dinleme komutu toostart hello cihaz uygulaması aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="186cb-194">At a command prompt in hello `simulated-device` folder, run hello following command toostart hello device app listening for desired property changes and direct method calls:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Merhaba aygıt istemcisi başlatır](media/iot-hub-java-java-schedule-jobs/device-app-1.png)

1. <span data-ttu-id="186cb-196">Bir komut isteminde hello `schedule-jobs` klasörüne komutu toorun hello aşağıdaki Merhaba, **işleri zamanla** uygulama toorun iki işleri hizmet.</span><span class="sxs-lookup"><span data-stu-id="186cb-196">At a command prompt in hello `schedule-jobs` folder, run hello following command toorun hello **schedule-jobs** service app toorun two jobs.</span></span> <span data-ttu-id="186cb-197">Merhaba ilk istenen hello özellik değerlerini ayarlar, doğrudan yöntemi hello ikinci çağrıları hello:</span><span class="sxs-lookup"><span data-stu-id="186cb-197">hello first sets hello desired property values, hello second calls hello direct method:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IOT Hub hizmeti uygulaması iki işleri oluşturur](media/iot-hub-java-java-schedule-jobs/service-app-1.png)

1. <span data-ttu-id="186cb-199">Merhaba cihaz uygulaması istenen hello özellik değişikliği ve hello doğrudan yöntem çağrısı işler:</span><span class="sxs-lookup"><span data-stu-id="186cb-199">hello device app handles hello desired property change and hello direct method call:</span></span>

    ![Merhaba aygıt istemcisi toohello değişiklikleri yanıt veriyor](media/iot-hub-java-java-schedule-jobs/device-app-2.png)

## <a name="next-steps"></a><span data-ttu-id="186cb-201">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="186cb-201">Next steps</span></span>

<span data-ttu-id="186cb-202">Bu öğreticide hello Azure portalında yeni bir IOT hub yapılandırılmış ve ardından hello IOT hub'ın kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="186cb-202">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="186cb-203">Bir arka uç uygulaması toorun iki işi oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="186cb-203">You created a back-end app toorun two jobs.</span></span> <span data-ttu-id="186cb-204">İstenen özellik değerlerini ve doğrudan bir yöntem olarak adlandırılan hello ikinci işi Hello ilk iş ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="186cb-204">hello first job set desired property values, and hello second job called a direct method.</span></span>

<span data-ttu-id="186cb-205">Kaynakları toolearn nasıl aşağıdaki kullanım hello için:</span><span class="sxs-lookup"><span data-stu-id="186cb-205">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="186cb-206">Merhaba aygıtlarla telemetri gönderen [IOT Hub ile çalışmaya başlama](iot-hub-java-java-getstarted.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="186cb-206">Send telemetry from devices with hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="186cb-207">Merhaba ile etkileşimli olarak (örneğin, kullanıcı tarafından denetlenen bir uygulamadan fan etkinleştirdikten) cihazları denetleme [doğrudan yöntemleri kullanın](iot-hub-java-java-direct-methods.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="186cb-207">Control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>
