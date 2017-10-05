---
title: "Zamanlama işlerini ile Azure IOT hub'ı (Java) | Microsoft Docs"
description: "Doğrudan bir yöntem çağırma ve birden fazla cihazda istenen özelliği ayarlamak için bir Azure IOT Hub işini zamanlamak nasıl. Sanal cihaz uygulamaları ve Azure IOT hizmeti işi çalıştırmak için bir hizmet uygulaması uygulamak için Java SDK'sını uygulamak için Azure IOT cihaz SDK'sı Java için kullanın."
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
ms.openlocfilehash: 003a548ef2da2921a699df1aa9f7aee366d341ab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="schedule-and-broadcast-jobs-java"></a><span data-ttu-id="7c179-104">Zamanlama ve yayın işleri (Java)</span><span class="sxs-lookup"><span data-stu-id="7c179-104">Schedule and broadcast jobs (Java)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="7c179-105">Zamanlama ve milyonlarca cihaza güncelleştirme işleri izlemek için Azure IOT hub'ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="7c179-105">Use Azure IoT Hub to schedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="7c179-106">İşlerini kullanın:</span><span class="sxs-lookup"><span data-stu-id="7c179-106">Use jobs to:</span></span>

* <span data-ttu-id="7c179-107">İstenen özellikleri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="7c179-107">Update desired properties</span></span>
* <span data-ttu-id="7c179-108">Güncelleştirme etiketleri</span><span class="sxs-lookup"><span data-stu-id="7c179-108">Update tags</span></span>
* <span data-ttu-id="7c179-109">Doğrudan yöntemleri çağırma</span><span class="sxs-lookup"><span data-stu-id="7c179-109">Invoke direct methods</span></span>

<span data-ttu-id="7c179-110">Bir işi şu eylemlerden birini sarmalar ve bir cihaz kümesi karşı yürütme izler.</span><span class="sxs-lookup"><span data-stu-id="7c179-110">A job wraps one of these actions and tracks the execution against a set of devices.</span></span> <span data-ttu-id="7c179-111">Cihaz çifti sorgu karşı iş yürütür cihaz kümesini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7c179-111">A device twin query defines the set of devices the job executes against.</span></span> <span data-ttu-id="7c179-112">Örneğin, bir arka uç uygulaması, aygıtların yeniden 10.000 cihazlarda doğrudan yöntemini çağırmak için bir iş kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c179-112">For example, a back-end app can use a job to invoke a direct method on 10,000 devices that reboots the devices.</span></span> <span data-ttu-id="7c179-113">Cihaz kümesini içeren bir cihaz çifti sorgu belirtin ve gelecek bir zamanda çalıştırmak için iş zamanlama.</span><span class="sxs-lookup"><span data-stu-id="7c179-113">You specify the set of devices with a device twin query and schedule the job to run at a future time.</span></span> <span data-ttu-id="7c179-114">Her aygıt olarak ilerleyişini izler almak ve yeniden başlatma doğrudan yöntemi yürütün.</span><span class="sxs-lookup"><span data-stu-id="7c179-114">The job tracks progress as each of the devices receive and execute the reboot direct method.</span></span>

<span data-ttu-id="7c179-115">Bu özelliklerin her biri hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="7c179-115">To learn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="7c179-116">Cihaz çifti ve özellikleri: [cihaz çiftlerini ile çalışmaya başlama](iot-hub-java-java-twin-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="7c179-116">Device twin and properties: [Get started with device twins](iot-hub-java-java-twin-getstarted.md)</span></span>
* <span data-ttu-id="7c179-117">Doğrudan yöntemleri: [IOT Hub Geliştirici Kılavuzu - doğrudan yöntemleri](iot-hub-devguide-direct-methods.md) ve [Öğreticisi: doğrudan yöntemleri kullanın](iot-hub-java-java-direct-methods.md)</span><span class="sxs-lookup"><span data-stu-id="7c179-117">Direct methods: [IoT Hub developer guide - direct methods](iot-hub-devguide-direct-methods.md) and [Tutorial: Use direct methods](iot-hub-java-java-direct-methods.md)</span></span>

<span data-ttu-id="7c179-118">Bu öğretici şunların nasıl yapıldığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="7c179-118">This tutorial shows you how to:</span></span>

* <span data-ttu-id="7c179-119">Adlı doğrudan bir yöntem uygulayan bir cihaz uygulaması oluşturma **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="7c179-119">Create a device app that implements a direct method called **lockDoor**.</span></span> <span data-ttu-id="7c179-120">Cihaz uygulaması Ayrıca, arka uç uygulama istenen özellik değişiklikleri alır.</span><span class="sxs-lookup"><span data-stu-id="7c179-120">The device app also receives desired property changes from the back-end app.</span></span>
* <span data-ttu-id="7c179-121">Aranacak bir işi oluşturan bir arka uç uygulaması oluşturma **lockDoor** birden fazla cihazda yöntemi doğrudan.</span><span class="sxs-lookup"><span data-stu-id="7c179-121">Create a back-end app that creates a job to call the **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="7c179-122">Başka bir iş birden çok aygıta istenen özelliği güncelleştirmeleri gönderir.</span><span class="sxs-lookup"><span data-stu-id="7c179-122">Another job sends desired property updates to multiple devices.</span></span>

<span data-ttu-id="7c179-123">Bu öğreticinin sonunda bir java konsol cihaz uygulaması ve bir java konsol arka uç uygulaması sahiptir:</span><span class="sxs-lookup"><span data-stu-id="7c179-123">At the end of this tutorial, you have a java console device app and a java console back-end app:</span></span>

<span data-ttu-id="7c179-124">**simulated-device** uygular, IOT hub'ına bağlanan **lockDoor** yöntemi ve tanıtıcıları istenen özellik değişikliklerini doğrudan.</span><span class="sxs-lookup"><span data-stu-id="7c179-124">**simulated-device** that connects to your IoT hub, implements the **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="7c179-125">**İşleri Zamanla** çağırmak için işleri kullanan **lockDoor** doğrudan yöntemi ve birden çok aygıta cihaz çifti istenen özelliklerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="7c179-125">**schedule-jobs** that use jobs to call the **lockDoor** direct method and update the device twin desired properties on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="7c179-126">Makaleyi [Azure IOT SDK'ları](iot-hub-devguide-sdks.md) hem cihaz hem de arka uç uygulamalar oluşturmak için kullanabileceğiniz Azure IOT SDK'ları hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c179-126">The article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c179-127">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7c179-127">Prerequisites</span></span>

<span data-ttu-id="7c179-128">Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="7c179-128">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="7c179-129">En güncel [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="7c179-129">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="7c179-130">Maven 3</span><span class="sxs-lookup"><span data-stu-id="7c179-130">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="7c179-131">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="7c179-131">An active Azure account.</span></span> <span data-ttu-id="7c179-132">(Bir hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz bir hesap](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.)</span><span class="sxs-lookup"><span data-stu-id="7c179-132">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="7c179-133">Cihaz kimliği programlı olarak oluşturmayı tercih ederseniz karşılık gelen bölümünde okuma [Cihazınızı Java kullanarak IOT hub'ınıza bağlanmak](iot-hub-java-java-getstarted.md#create-a-device-identity) makalesi.</span><span class="sxs-lookup"><span data-stu-id="7c179-133">If you prefer to create the device identity programmatically, read the corresponding section in the [Connect your device to your IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span> <span data-ttu-id="7c179-134">Aynı zamanda [iothub-explorer](https://github.com/Azure/iothub-explorer) bir cihaz IOT hub'ınıza eklemek için aracı.</span><span class="sxs-lookup"><span data-stu-id="7c179-134">You can also use the [iothub-explorer](https://github.com/Azure/iothub-explorer) tool to add a device to your IoT hub.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="7c179-135">Hizmet Uygulaması Oluştur</span><span class="sxs-lookup"><span data-stu-id="7c179-135">Create the service app</span></span>

<span data-ttu-id="7c179-136">Bu bölümde, işleri kullanan bir Java konsol uygulaması oluşturun:</span><span class="sxs-lookup"><span data-stu-id="7c179-136">In this section, you create a Java console app that uses jobs to:</span></span>

* <span data-ttu-id="7c179-137">Çağrı **lockDoor** birden fazla cihazda yöntemi doğrudan.</span><span class="sxs-lookup"><span data-stu-id="7c179-137">Call the **lockDoor** direct method on multiple devices.</span></span>
* <span data-ttu-id="7c179-138">İstenen özelliklerde birden fazla cihaza Gönder.</span><span class="sxs-lookup"><span data-stu-id="7c179-138">Send desired properties to multiple devices.</span></span>

<span data-ttu-id="7c179-139">Uygulama oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="7c179-139">To create the app:</span></span>

1. <span data-ttu-id="7c179-140">Geliştirme makinenizde adlı boş bir klasör oluşturun `iot-java-schedule-jobs`.</span><span class="sxs-lookup"><span data-stu-id="7c179-140">On your development machine, create an empty folder called `iot-java-schedule-jobs`.</span></span>

1. <span data-ttu-id="7c179-141">İçinde `iot-java-schedule-jobs` klasörünü adlı bir Maven projesi oluşturun **işleri zamanla** , komut isteminde aşağıdaki komutu kullanarak.</span><span class="sxs-lookup"><span data-stu-id="7c179-141">In the `iot-java-schedule-jobs` folder, create a Maven project called **schedule-jobs** using the following command at your command prompt.</span></span> <span data-ttu-id="7c179-142">Bunun tek ve uzun bir komut olduğunu unutmayın:</span><span class="sxs-lookup"><span data-stu-id="7c179-142">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=schedule-jobs -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="7c179-143">Komut isteminizde gidin `schedule-jobs` klasör.</span><span class="sxs-lookup"><span data-stu-id="7c179-143">At your command prompt, navigate to the `schedule-jobs` folder.</span></span>

1. <span data-ttu-id="7c179-144">Bir metin düzenleyicisi kullanarak açın `pom.xml` dosyasını `schedule-jobs` klasörü ve aşağıdaki bağımlılığı eklemek **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="7c179-144">Using a text editor, open the `pom.xml` file in the `schedule-jobs` folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="7c179-145">Bu bağımlılık kullanmanıza olanak tanır **IOT hizmeti istemcisi** IOT hub ile iletişim kurmak için uygulamanızda paketi:</span><span class="sxs-lookup"><span data-stu-id="7c179-145">This dependency enables you to use the **iot-service-client** package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="7c179-146">En son sürümü için kontrol edebilirsiniz **IOT hizmeti istemcisi** kullanarak [Maven arama](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="7c179-146">You can check for the latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="7c179-147">Aşağıdakileri ekleyin **yapı** düğümünden sonraki **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="7c179-147">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="7c179-148">Bu yapılandırma, uygulamanızı oluşturmak için Java 1.8 kullanmak için Maven bildirir:</span><span class="sxs-lookup"><span data-stu-id="7c179-148">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="7c179-149">Kaydet ve Kapat `pom.xml` dosya.</span><span class="sxs-lookup"><span data-stu-id="7c179-149">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="7c179-150">Bir metin düzenleyicisi kullanarak açın `schedule-jobs\src\main\java\com\mycompany\app\App.java` dosya.</span><span class="sxs-lookup"><span data-stu-id="7c179-150">Using a text editor, open the `schedule-jobs\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="7c179-151">Aşağıdaki **içeri aktarma** deyimlerini dosyaya ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7c179-151">Add the following **import** statements to the file:</span></span>

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

1. <span data-ttu-id="7c179-152">Aşağıdaki sınıf düzeyi değişkenleri **App** sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7c179-152">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="7c179-153">Değiştir `{youriothubconnectionstring}` , not ettiğiniz, IOT hub bağlantı dizesine sahip *IOT Hub oluşturma* bölümü:</span><span class="sxs-lookup"><span data-stu-id="7c179-153">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    // How long the job is permitted to run without
    // completing its work on the set of devices
    private static final long maxExecutionTimeInSeconds = 30;
    ```

1. <span data-ttu-id="7c179-154">Aşağıdaki yöntemi ekleyin **uygulama** güncelleştirmek için bir iş zamanlamak için sınıf **yapı** ve **kat** özellikler cihaz çiftine istenen:</span><span class="sxs-lookup"><span data-stu-id="7c179-154">Add the following method to the **App** class to schedule a job to update the **Building** and **Floor** desired properties in the device twin:</span></span>

    ```java
    private static JobResult scheduleJobSetDesiredProperties(JobClient jobClient, String jobId) {
      DeviceTwinDevice twin = new DeviceTwinDevice(deviceId);
      Set<Pair> desiredProperties = new HashSet<Pair>();
      desiredProperties.add(new Pair("Building", 43));
      desiredProperties.add(new Pair("Floor", 3));
      twin.setDesiredProperties(desiredProperties);
      // Optimistic concurrency control
      twin.setETag("*");

      // Schedule the update twin job to run now
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

1. <span data-ttu-id="7c179-155">Çağrılacak işini zamanlamak için **lockDoor** yöntemi, aşağıdaki yöntemi ekleyin **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="7c179-155">To schedule a job to call the **lockDoor** method, add the following method to the **App** class:</span></span>

    ```java
    private static JobResult scheduleJobCallDirectMethod(JobClient jobClient, String jobId) {
      // Schedule a job now to call the lockDoor direct method
      // against a single device. Response and connection
      // timeouts are set to 5 seconds.
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

1. <span data-ttu-id="7c179-156">Bir işi izlemek için aşağıdaki yöntemi ekleyin **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="7c179-156">To monitor a job, add the following method to the **App** class:</span></span>

    ```java
    private static void monitorJob(JobClient jobClient, String jobId) {
      try {
        JobResult jobResult = jobClient.getJob(jobId);
        if(jobResult == null)
        {
          System.out.println("No JobResult for: " + jobId);
          return;
        }
        // Check the job result until it's completed
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

1. <span data-ttu-id="7c179-157">Çalıştırdığınız iş ayrıntılarını sorgulamak için aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7c179-157">To query for the details of the jobs you ran, add the following method:</span></span>

    ```java
    private static void queryDeviceJobs(JobClient jobClient, String start) throws Exception {
      System.out.println("\nQuery device jobs since " + start);

      // Create a jobs query using the time the jobs started
      Query deviceJobQuery = jobClient
          .queryDeviceJob(SqlQuery.createSqlQuery("*", SqlQuery.FromType.JOBS, "devices.jobs.startTimeUtc > '" + start + "'", null).getQuery());

      // Iterate over the list of jobs and print the details
      while (jobClient.hasNextJob(deviceJobQuery)) {
        System.out.println(jobClient.getNextJob(deviceJobQuery));
      }
    }
    ```

1. <span data-ttu-id="7c179-158">Güncelleştirme **ana** şunlar için yöntem imzası `throws` yan tümcesi:</span><span class="sxs-lookup"><span data-stu-id="7c179-158">Update the **main** method signature to include the following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws Exception
    ```

1. <span data-ttu-id="7c179-159">Çalıştırmak ve iki işler sırayla izlemek için aşağıdaki kodu ekleyin **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="7c179-159">To run and monitor two jobs sequentially, add the following code to the **main** method:</span></span>

    ```java
    // Record the start time
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

    // Run a query to show the job detail
    queryDeviceJobs(jobClient, start);

    System.out.println("Shutting down schedule-jobs app");
    ```

1. <span data-ttu-id="7c179-160">Kaydet ve Kapat `schedule-jobs\src\main\java\com\mycompany\app\App.java` dosyası</span><span class="sxs-lookup"><span data-stu-id="7c179-160">Save and close the `schedule-jobs\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="7c179-161">Yapı **işleri zamanla** uygulama ve olan hataları düzeltin.</span><span class="sxs-lookup"><span data-stu-id="7c179-161">Build the **schedule-jobs** app and correct any errors.</span></span> <span data-ttu-id="7c179-162">Komut isteminizde gidin `schedule-jobs` klasörü ve aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7c179-162">At your command prompt, navigate to the `schedule-jobs` folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="7c179-163">Cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c179-163">Create a device app</span></span>

<span data-ttu-id="7c179-164">Bu bölümde IOT Hub'ından gönderilen istenen özellikleri işler ve doğrudan yöntem çağrısının uygulayan bir Java konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7c179-164">In this section, you create a Java console app that handles the desired properties sent from IoT Hub and implements the direct method call.</span></span>

1. <span data-ttu-id="7c179-165">İçinde `iot-java-schedule-jobs` klasörünü adlı bir Maven projesi oluşturun **simulated-device** , komut isteminde aşağıdaki komutu kullanarak.</span><span class="sxs-lookup"><span data-stu-id="7c179-165">In the `iot-java-schedule-jobs` folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="7c179-166">Bunun tek ve uzun bir komut olduğunu unutmayın:</span><span class="sxs-lookup"><span data-stu-id="7c179-166">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="7c179-167">Komut isteminizde gidin `simulated-device` klasör.</span><span class="sxs-lookup"><span data-stu-id="7c179-167">At your command prompt, navigate to the `simulated-device` folder.</span></span>

1. <span data-ttu-id="7c179-168">Bir metin düzenleyicisi kullanarak açın `pom.xml` dosyasını `simulated-device` klasörü ve aşağıdaki bağımlılıkları ekleyin **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="7c179-168">Using a text editor, open the `pom.xml` file in the `simulated-device` folder and add the following dependencies to the **dependencies** node.</span></span> <span data-ttu-id="7c179-169">Bu bağımlılık kullanmanıza olanak tanır **IOT cihaz istemci** IOT hub ile iletişim kurmak için uygulamanızda paketi:</span><span class="sxs-lookup"><span data-stu-id="7c179-169">This dependency enables you to use the **iot-device-client** package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="7c179-170">En son sürümü için kontrol edebilirsiniz **IOT cihaz istemci** kullanarak [Maven arama](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="7c179-170">You can check for the latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="7c179-171">Aşağıdakileri ekleyin **yapı** düğümünden sonraki **bağımlılıkları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="7c179-171">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="7c179-172">Bu yapılandırma, uygulamanızı oluşturmak için Java 1.8 kullanmak için Maven bildirir:</span><span class="sxs-lookup"><span data-stu-id="7c179-172">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="7c179-173">Kaydet ve Kapat `pom.xml` dosya.</span><span class="sxs-lookup"><span data-stu-id="7c179-173">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="7c179-174">Bir metin düzenleyicisi kullanarak açın `simulated-device\src\main\java\com\mycompany\app\App.java` dosya.</span><span class="sxs-lookup"><span data-stu-id="7c179-174">Using a text editor, open the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="7c179-175">Aşağıdaki **içeri aktarma** deyimlerini dosyaya ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7c179-175">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="7c179-176">Aşağıdaki sınıf düzeyi değişkenleri **App** sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7c179-176">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="7c179-177">Değiştirme `{youriothubname}` , IOT hub'ı adıyla ve `{yourdevicekey}` içinde oluşturulan cihaz anahtarla değeri *bir cihaz kimliği oluşturma* bölümü:</span><span class="sxs-lookup"><span data-stu-id="7c179-177">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with the device key value you generated in the *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="7c179-178">Bu örnek uygulama, bir **DeviceClient** nesnesi örneğini oluşturduğunda **prokotol** değişkenini kullanır.</span><span class="sxs-lookup"><span data-stu-id="7c179-178">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="7c179-179">Şu anda, cihaz çifti özelliklerini kullanmak için MQTT Protokolü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c179-179">Currently, to use device twin features you must use the MQTT protocol.</span></span>

1. <span data-ttu-id="7c179-180">Cihaz çifti bildirimleri konsoluna yazdırmak için aşağıdaki iç içe geçmiş sınıf ekleme **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="7c179-180">To print device twin notifications to the console, add the following nested class to the **App** class:</span></span>

    ```java
    // Handler for device twin operation notifications from IoT Hub
    protected static class DeviceTwinStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to device twin operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="7c179-181">Konsola doğrudan yöntem bildirimleri yazdırmak için aşağıdaki iç içe geçmiş sınıf ekleme **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="7c179-181">To print direct method notifications to the console, add the following nested class to the **App** class:</span></span>

    ```java
    // Handler for direct method notifications from IoT Hub
    protected static class DirectMethodStatusCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to direct method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="7c179-182">IOT hub'dan doğrudan yöntem çağrıları işlemek için aşağıdaki iç içe geçmiş sınıf ekleme **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="7c179-182">To handle direct method calls from IoT Hub, add the following nested class to the **App** class:</span></span>

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

1. <span data-ttu-id="7c179-183">Güncelleştirme **ana** şunlar için yöntem imzası `throws` yan tümcesi:</span><span class="sxs-lookup"><span data-stu-id="7c179-183">Update the **main** method signature to include the following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="7c179-184">Aşağıdaki kodu ekleyin **ana** yöntemi için:</span><span class="sxs-lookup"><span data-stu-id="7c179-184">Add the following code to the **main** method to:</span></span>
    * <span data-ttu-id="7c179-185">IOT Hub ile iletişim kurmak için bir cihaz istemcisi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7c179-185">Create a device client to communicate with IoT Hub.</span></span>
    * <span data-ttu-id="7c179-186">Oluşturma bir **aygıt** cihaz çifti özelliklerini depolamak için nesne.</span><span class="sxs-lookup"><span data-stu-id="7c179-186">Create a **Device** object to store the device twin properties.</span></span>

    ```java
    // Create a device client
    DeviceClient client = new DeviceClient(connString, protocol);

    // An object to manage device twin desired and reported properties
    Device dataCollector = new Device() {
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context)
      {
        System.out.println("Received desired property change: " + propertyKey + " " + propertyValue);
      }
    };
    ```

1. <span data-ttu-id="7c179-187">Aygıt istemci hizmetlerini başlatmak için aşağıdaki kodu ekleyin **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="7c179-187">To start the device client services, add the following code to the **main** method:</span></span>

    ```java
    try {
      // Open the DeviceClient
      // Start the device twin services
      // Subscribe to direct method calls
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

1. <span data-ttu-id="7c179-188">Kullanıcı basmak beklenecek **Enter** anahtar kapatmadan önce sonuna aşağıdaki kodu ekleyin **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="7c179-188">To wait for the user to press the **Enter** key before shutting down, add the following code to the end of the **main** method:</span></span>

    ```java
    // Close the app
    System.out.println("Press any key to exit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    dataCollector.clean();
    client.closeNow();
    scanner.close();
    ```

1. <span data-ttu-id="7c179-189">Kaydet ve Kapat `simulated-device\src\main\java\com\mycompany\app\App.java` dosya.</span><span class="sxs-lookup"><span data-stu-id="7c179-189">Save and close the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="7c179-190">Yapı **simulated-device** uygulama ve olan hataları düzeltin.</span><span class="sxs-lookup"><span data-stu-id="7c179-190">Build the **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="7c179-191">Komut isteminizde gidin `simulated-device` klasörü ve aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7c179-191">At your command prompt, navigate to the `simulated-device` folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-the-apps"></a><span data-ttu-id="7c179-192">Uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7c179-192">Run the apps</span></span>

<span data-ttu-id="7c179-193">Şimdi konsol uygulamaları çalıştırmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="7c179-193">You are now ready to run the console apps.</span></span>

1. <span data-ttu-id="7c179-194">Bir komut isteminde `simulated-device` klasörü, istenen özellik değişikliklerini ve doğrudan yöntem çağrıları için dinleme aygıt uygulamasını başlatmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7c179-194">At a command prompt in the `simulated-device` folder, run the following command to start the device app listening for desired property changes and direct method calls:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Aygıt istemcisi başlatır](media/iot-hub-java-java-schedule-jobs/device-app-1.png)

1. <span data-ttu-id="7c179-196">Bir komut isteminde `schedule-jobs` klasörü çalıştırmak için aşağıdaki komutu çalıştırın, **işleri zamanla** iki işlerini çalıştırmak için hizmeti uygulaması.</span><span class="sxs-lookup"><span data-stu-id="7c179-196">At a command prompt in the `schedule-jobs` folder, run the following command to run the **schedule-jobs** service app to run two jobs.</span></span> <span data-ttu-id="7c179-197">İlk istenen özellik değerlerini ayarlar, ikinci doğrudan yöntemini çağırır:</span><span class="sxs-lookup"><span data-stu-id="7c179-197">The first sets the desired property values, the second calls the direct method:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IOT Hub hizmeti uygulaması iki işleri oluşturur](media/iot-hub-java-java-schedule-jobs/service-app-1.png)

1. <span data-ttu-id="7c179-199">Cihaz uygulaması istenen özellik değişikliği ve doğrudan yöntem çağrısının işler:</span><span class="sxs-lookup"><span data-stu-id="7c179-199">The device app handles the desired property change and the direct method call:</span></span>

    ![Aygıt istemcisi değişiklikleri yanıt veriyor](media/iot-hub-java-java-schedule-jobs/device-app-2.png)

## <a name="next-steps"></a><span data-ttu-id="7c179-201">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7c179-201">Next steps</span></span>

<span data-ttu-id="7c179-202">Bu öğreticide, Azure portalında yeni bir IoT hub'ı yapılandırdınız ve ardından IoT hub'ının kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="7c179-202">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="7c179-203">İki işlerini çalıştırmak için bir arka uç uygulaması oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="7c179-203">You created a back-end app to run two jobs.</span></span> <span data-ttu-id="7c179-204">İlk iş istenen özellik değerlerini ayarlayın ve ikinci işi doğrudan bir yöntem çağrılır.</span><span class="sxs-lookup"><span data-stu-id="7c179-204">The first job set desired property values, and the second job called a direct method.</span></span>

<span data-ttu-id="7c179-205">Bilgi edinmek için aşağıdaki kaynakları kullanın nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="7c179-205">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="7c179-206">Aygıtlarla telemetri gönderen [IOT Hub ile çalışmaya başlama](iot-hub-java-java-getstarted.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="7c179-206">Send telemetry from devices with the [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="7c179-207">Aygıtlarını etkileşimli olarak (örneğin, kullanıcı tarafından denetlenen bir uygulamadan fan etkinleştirdikten) ile [doğrudan yöntemleri kullanın](iot-hub-java-java-direct-methods.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="7c179-207">Control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>
