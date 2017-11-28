---
title: "aaaGet başlatılan Azure IOT hub'ı (.NET) | Microsoft Docs"
description: "Nasıl tooAzure IOT Hub'ın IOT SDK'ları için .NET kullanarak toosend cihaz-bulut iletileri öğrenin. Sanal cihazı ve hizmet uygulamaları tooregister Cihazınızı oluşturmak, iletileri gönderir ve IOT hub'ından iletileri okur."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: f40604ff-8fd6-4969-9e99-8574fbcf036c
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56cf14687411898ea0fa4ebb1782e18b3930809c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-net"></a><span data-ttu-id="ebab3-104">.NET kullanarak aygıt tooyour IOT hub'ınıza bağlanın</span><span class="sxs-lookup"><span data-stu-id="ebab3-104">Connect your device tooyour IoT hub using .NET</span></span>

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="ebab3-105">Bu öğretici Hello sonunda üç .NET konsol uygulamaları vardır:</span><span class="sxs-lookup"><span data-stu-id="ebab3-105">At hello end of this tutorial, you have three .NET console apps:</span></span>

* <span data-ttu-id="ebab3-106">**CreateDeviceIdentity**ilişkili güvenlik anahtarı tooconnect cihaz uygulamanız ve bir cihaz kimliği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ebab3-106">**CreateDeviceIdentity**, which creates a device identity and associated security key tooconnect your device app.</span></span>
* <span data-ttu-id="ebab3-107">**ReadDeviceToCloudMessages**, cihaz uygulamanız tarafından gönderilen hello telemetri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ebab3-107">**ReadDeviceToCloudMessages**, which displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="ebab3-108">**SimulatedDevice**, hangi tooyour IOT hub'ı daha önce oluşturduğunuz hello cihaz kimliği bağlanır ve hello MQTT protokolünü kullanarak her saniye bir telemetri iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="ebab3-108">**SimulatedDevice**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second by using hello MQTT protocol.</span></span>

<span data-ttu-id="ebab3-109">Github'dan hello üç uygulamaları içeren hello Visual Studio çözümü kopyalama veya indirilir.</span><span class="sxs-lookup"><span data-stu-id="ebab3-109">You can download or clone hello Visual Studio solution, which contains hello three apps from Github.</span></span>

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> <span data-ttu-id="ebab3-110">Cihazlardaki uygulamalar toorun hem, çözüm arka ucu hello Azure IOT SDK'ları hakkında toobuild kullanabileceğiniz bilgi için bkz [Azure IOT SDK'ları][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="ebab3-110">For information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices, and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="ebab3-111">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="ebab3-111">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="ebab3-112">Visual Studio 2015 veya Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="ebab3-112">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="ebab3-113">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="ebab3-113">An active Azure account.</span></span> <span data-ttu-id="ebab3-114">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="ebab3-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="ebab3-115">IOT hub'ınızı oluşturdunuz ve hello ana bilgisayar adı ve IOT Hub bağlantı dizesine toocomplete hello Bu öğreticinin geri kalanını gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="ebab3-115">You have now created your IoT hub, and you have hello host name and IoT Hub connection string that you need toocomplete hello rest of this tutorial.</span></span>

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="ebab3-116">Cihazdan buluta iletileri alma</span><span class="sxs-lookup"><span data-stu-id="ebab3-116">Receive device-to-cloud messages</span></span>
<span data-ttu-id="ebab3-117">Bu bölümde IoT Hub'dan cihaz-bulut iletilerini okuyan bir .NET konsol uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="ebab3-117">In this section, you create a .NET console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="ebab3-118">IOT hub'ı kullanıma sunan bir [Azure Event Hubs][lnk-event-hubs-overview]-uyumlu bir uç noktasını tooenable, tooread cihaz bulut iletilerini.</span><span class="sxs-lookup"><span data-stu-id="ebab3-118">An IoT hub exposes an [Azure Event Hubs][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="ebab3-119">tookeep şeyler basit, Bu öğretici, bir yüksek işleme dağıtımına uygun olmayan temel bir okuyucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ebab3-119">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="ebab3-120">tooprocess cihaz-bulut iletileri ölçekli olarak nasıl toolearn bakın hello [cihaz-bulut iletileri] [ lnk-process-d2c-tutorial] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="ebab3-120">toolearn how tooprocess device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span> <span data-ttu-id="ebab3-121">Merhaba nasıl tooprocess olay hub'larından iletileri hakkında daha fazla bilgi için bkz: [Event Hubs ile çalışmaya başlama] [ lnk-eventhubs-tutorial] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="ebab3-121">For more information about how tooprocess messages from Event Hubs, see hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span> <span data-ttu-id="ebab3-122">(Bu öğretici geçerli toohello IOT Hub ve Event Hub ile uyumlu uç noktaları olur.)</span><span class="sxs-lookup"><span data-stu-id="ebab3-122">(This tutorial is applicable toohello IoT Hub Event Hub-compatible endpoints.)</span></span>

> [!NOTE]
> <span data-ttu-id="ebab3-123">Merhaba cihaz bulut iletilerini her zaman okumak için Event Hub ile uyumlu uç nokta hello AMQP protokolünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="ebab3-123">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>

1. <span data-ttu-id="ebab3-124">Visual Studio'da bir Visual C# Windows Klasik Masaüstü projesi toohello geçerli çözüme, hello kullanarak ekleyin **konsol uygulaması (.NET Framework)** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="ebab3-124">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="ebab3-125">Merhaba .NET Framework sürümünün 4.5.1 olduğundan emin olun veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="ebab3-125">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="ebab3-126">Ad hello proje **ReadDeviceToCloudMessages**.</span><span class="sxs-lookup"><span data-stu-id="ebab3-126">Name hello project **ReadDeviceToCloudMessages**.</span></span>

    ![Yeni Visual C# Windows Klasik Masaüstü projesi][10a]

2. <span data-ttu-id="ebab3-128">Çözüm Gezgini'nde hello sağ **ReadDeviceToCloudMessages** proje ve ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="ebab3-128">In Solution Explorer, right-click hello **ReadDeviceToCloudMessages** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="ebab3-129">Merhaba, **NuGet Paket Yöneticisi** penceresinde, arama **WindowsAzure.ServiceBus**seçin **yükleme**ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="ebab3-129">In hello **NuGet Package Manager** window, search for **WindowsAzure.ServiceBus**, select **Install**, and accept hello terms of use.</span></span> <span data-ttu-id="ebab3-130">Bu yordam indirir, yükler ve bir başvuru çok ekler[Azure Service Bus][lnk-servicebus-nuget], tüm bağımlılıklarıyla birlikte.</span><span class="sxs-lookup"><span data-stu-id="ebab3-130">This procedure downloads, installs, and adds a reference too[Azure Service Bus][lnk-servicebus-nuget], with all its dependencies.</span></span> <span data-ttu-id="ebab3-131">Bu paket hello uygulama tooconnect toohello Event Hub ile uyumlu uç IOT hub'ınızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="ebab3-131">This package enables hello application tooconnect toohello Event Hub-compatible endpoint on your IoT hub.</span></span>

4. <span data-ttu-id="ebab3-132">Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:</span><span class="sxs-lookup"><span data-stu-id="ebab3-132">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. <span data-ttu-id="ebab3-133">Aşağıdaki alanları toohello hello eklemek **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="ebab3-133">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="ebab3-134">Merhaba hello "IOT hub oluşturma" bölümünde oluşturduğunuz hello hub'ın IOT Hub bağlantı dizesine sahip Hello yer tutucu değerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ebab3-134">Replace hello placeholder value with hello IoT Hub connection string for hello hub you created in hello "Create an IoT hub" section.</span></span>

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. <span data-ttu-id="ebab3-135">Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="ebab3-135">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested) break;
            EventData eventData = await eventHubReceiver.ReceiveAsync();
            if (eventData == null) continue;

            string data = Encoding.UTF8.GetString(eventData.GetBytes());
            Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
        }
    }
    ```

    <span data-ttu-id="ebab3-136">Bu yöntem bir **EventHubReceiver** örneği tooreceive tüm hello IOT hub'a cihaz-bulut iletileri alma bölümlerinden.</span><span class="sxs-lookup"><span data-stu-id="ebab3-136">This method uses an **EventHubReceiver** instance tooreceive messages from all hello IoT hub device-to-cloud receive partitions.</span></span> <span data-ttu-id="ebab3-137">Nasıl geçirdiğinize dikkat edin bir `DateTime.Now` hello oluşturduğunuzda parametresi **EventHubReceiver** yalnızca başladıktan sonra gönderilen iletileri alması nesne.</span><span class="sxs-lookup"><span data-stu-id="ebab3-137">Notice how you pass a `DateTime.Now` parameter when you create hello **EventHubReceiver** object, so that it only receives messages sent after it starts.</span></span> <span data-ttu-id="ebab3-138">Merhaba geçerli iletiler kümesini görebileceğiniz için bu filtre bir test ortamında kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="ebab3-138">This filter is useful in a test environment so you can see hello current set of messages.</span></span> <span data-ttu-id="ebab3-139">Bir üretim ortamında kodunuzun tüm hello iletileri işlediğinden emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ebab3-139">In a production environment, your code should make sure that it processes all hello messages.</span></span> <span data-ttu-id="ebab3-140">Merhaba öğretici daha fazla bilgi için bkz [nasıl tooprocess IOT Hub cihaz bulut iletilerini][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="ebab3-140">For more information, see hello tutorial [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial].</span></span>

7. <span data-ttu-id="ebab3-141">Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="ebab3-141">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive messages. Ctrl-C tooexit.\n");
    eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, iotHubD2cEndpoint);

    var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;

    CancellationTokenSource cts = new CancellationTokenSource();

    System.Console.CancelKeyPress += (s, e) =>
    {
        e.Cancel = true;
        cts.Cancel();
        Console.WriteLine("Exiting...");
    };

    var tasks = new List<Task>();
    foreach (string partition in d2cPartitions)
    {
        tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
    }  
    Task.WaitAll(tasks.ToArray());
    ```

## <a name="create-a-device-app"></a><span data-ttu-id="ebab3-142">Cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="ebab3-142">Create a device app</span></span>

<span data-ttu-id="ebab3-143">Bu bölümde, tooan IOT hub'ı cihaz-bulut iletileri gönderen bir cihaza benzetim yapan bir .NET konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ebab3-143">In this section, you create a .NET console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="ebab3-144">Visual Studio'da bir Visual C# Windows Klasik Masaüstü projesi toohello geçerli çözüme, hello kullanarak ekleyin **konsol uygulaması (.NET Framework)** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="ebab3-144">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="ebab3-145">Merhaba .NET Framework sürümünün 4.5.1 olduğundan emin olun veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="ebab3-145">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="ebab3-146">Ad hello proje **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="ebab3-146">Name hello project **SimulatedDevice**.</span></span>

    ![Yeni Visual C# Windows Klasik Masaüstü projesi][10b]

2. <span data-ttu-id="ebab3-148">Çözüm Gezgini'nde hello sağ **SimulatedDevice** proje ve ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="ebab3-148">In Solution Explorer, right-click hello **SimulatedDevice** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="ebab3-149">Merhaba, **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat**, arama **Microsoft.Azure.Devices.Client**seçin **yükleme** tooinstall hello **Microsoft.Azure.Devices.Client** paketini ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="ebab3-149">In hello **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices.Client**, select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="ebab3-150">Bu yordam indirir, yükler ve başvuru toohello ekler [Azure IOT cihaz SDK'sı NuGet paketi] [ lnk-device-nuget] ve bağımlılıklarını.</span><span class="sxs-lookup"><span data-stu-id="ebab3-150">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK NuGet package][lnk-device-nuget] and its dependencies.</span></span>

4. <span data-ttu-id="ebab3-151">Merhaba aşağıdakileri ekleyin `using` deyimi hello hello üstündeki **Program.cs** dosyası:</span><span class="sxs-lookup"><span data-stu-id="ebab3-151">Add hello following `using` statement at hello top of hello **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. <span data-ttu-id="ebab3-152">Aşağıdaki alanları toohello hello eklemek **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="ebab3-152">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="ebab3-153">Yedek `{iot hub hostname}` hello IOT hub ana bilgisayar adıyla hello "IOT hub oluşturma" bölümünde alınır.</span><span class="sxs-lookup"><span data-stu-id="ebab3-153">Substitute `{iot hub hostname}` with hello IoT hub host name you retrieved in hello "Create an IoT hub" section.</span></span> <span data-ttu-id="ebab3-154">Yedek `{device key}` hello aygıt anahtarı ile hello "bir cihaz kimliği oluşturma" bölümünde aldığınız.</span><span class="sxs-lookup"><span data-stu-id="ebab3-154">Substitute `{device key}` with hello device key you retrieved in hello "Create a device identity" section.</span></span>

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. <span data-ttu-id="ebab3-155">Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="ebab3-155">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    private static async void SendDeviceToCloudMessagesAsync()
    {
        double minTemperature = 20;
        double minHumidity = 60;
        int messageId = 1;
        Random rand = new Random();

        while (true)
        {
            double currentTemperature = minTemperature + rand.NextDouble() * 15;
            double currentHumidity = minHumidity + rand.NextDouble() * 20;

            var telemetryDataPoint = new
            {
                messageId = messageId++,
                deviceId = "myFirstDevice",
                temperature = currentTemperature,
                humidity = currentHumidity
            };
            var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
            var message = new Message(Encoding.ASCII.GetBytes(messageString));
            message.Properties.Add("temperatureAlert", (currentTemperature > 30) ? "true" : "false");

            await deviceClient.SendEventAsync(message);
            Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, messageString);

            await Task.Delay(1000);
        }
    }
    ```

    <span data-ttu-id="ebab3-156">Bu yöntem, her saniye yeni bir cihazdan buluta iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="ebab3-156">This method sends a new device-to-cloud message every second.</span></span> <span data-ttu-id="ebab3-157">Selamlama iletisine ve rastgele sayılar toosimulate sıcaklık algılayıcısı ve nem algılayıcı oluşturulan hello cihaz kimliği ile JSON seri hale getirilmiş bir nesneyi içerir.</span><span class="sxs-lookup"><span data-stu-id="ebab3-157">hello message contains a JSON-serialized object, with hello device ID and randomly generated numbers toosimulate a temperature sensor, and a humidity sensor.</span></span>

7. <span data-ttu-id="ebab3-158">Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="ebab3-158">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    <span data-ttu-id="ebab3-159">Varsayılan olarak, hello **oluşturma** yöntemi bir .NET Framework uygulamasında oluşturur bir **DeviceClient** IOT Hub ile Merhaba AMQP protokolünü toocommunicate kullanan örneği.</span><span class="sxs-lookup"><span data-stu-id="ebab3-159">By default, hello **Create** method in a .NET Framework app creates a **DeviceClient** instance that uses hello AMQP protocol toocommunicate with IoT Hub.</span></span> <span data-ttu-id="ebab3-160">toouse hello MQTT veya HTTP protokolünü kullanmak hello hello geçersiz kılma **oluşturma** toospecify hello Protokolü sağlar yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ebab3-160">toouse hello MQTT or HTTP protocol, use hello override of hello **Create** method that enables you toospecify hello protocol.</span></span> <span data-ttu-id="ebab3-161">UWP ve PCL istemcileri varsayılan olarak hello HTTP protokolünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="ebab3-161">UWP and PCL clients use hello HTTP protocol by default.</span></span> <span data-ttu-id="ebab3-162">Merhaba HTTP protokolü kullanırsanız, hello de eklemeniz gerekir **Microsoft.AspNet.WebApi.Client** NuGet paketi tooyour proje tooinclude hello **Microsoft.ASPNET.webapi.Client** ad alanı.</span><span class="sxs-lookup"><span data-stu-id="ebab3-162">If you use hello HTTP protocol, you should also add hello **Microsoft.AspNet.WebApi.Client** NuGet package tooyour project tooinclude hello **System.Net.Http.Formatting** namespace.</span></span>

<span data-ttu-id="ebab3-163">Bu öğretici hello adımları toocreate IOT hub'ı cihaz uygulaması gösterir.</span><span class="sxs-lookup"><span data-stu-id="ebab3-163">This tutorial takes you through hello steps toocreate an IoT Hub device app.</span></span> <span data-ttu-id="ebab3-164">Merhaba de kullanabilirsiniz [Azure IOT Hub için bağlı hizmet] [ lnk-connected-service] Visual Studio uzantısı tooadd hello gerekli kodu tooyour cihaz uygulaması.</span><span class="sxs-lookup"><span data-stu-id="ebab3-164">You can also use hello [Connected Service for Azure IoT Hub][lnk-connected-service] Visual Studio extension tooadd hello necessary code tooyour device app.</span></span>

> [!NOTE]
> <span data-ttu-id="ebab3-165">tookeep şeyler basit, Bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="ebab3-165">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="ebab3-166">Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="ebab3-166">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="ebab3-167">Merhaba uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="ebab3-167">Run hello apps</span></span>

<span data-ttu-id="ebab3-168">Hazır toorun hello uygulamaları sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="ebab3-168">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="ebab3-169">Visual Studio'daki Çözüm Gezgini'nde çözümünüze sağ tıklayın ve ardından **Başlangıç projelerini ayarla**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ebab3-169">In Visual Studio, in Solution Explorer, right-click your solution, and then click **Set StartUp projects**.</span></span> <span data-ttu-id="ebab3-170">Seçin **birden fazla başlangıç projesi**ve ardından **Başlat** hem hello hello eylem olarak **ReadDeviceToCloudMessages** ve **SimulatedDevice** projeleri.</span><span class="sxs-lookup"><span data-stu-id="ebab3-170">Select **Multiple startup projects**, and then select **Start** as hello action for both hello **ReadDeviceToCloudMessages** and **SimulatedDevice** projects.</span></span>

    ![Başlangıç projesinin özellikleri][41]

2. <span data-ttu-id="ebab3-172">Tuşuna **F5** toostart çalışan her iki uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="ebab3-172">Press **F5** toostart both apps running.</span></span> <span data-ttu-id="ebab3-173">Merhaba hello konsol çıktısı **SimulatedDevice** uygulama gösterir Merhaba iletileri tooyour IOT hub cihaz uygulamanız gönderir.</span><span class="sxs-lookup"><span data-stu-id="ebab3-173">hello console output from hello **SimulatedDevice** app shows hello messages your device app sends tooyour IoT hub.</span></span> <span data-ttu-id="ebab3-174">Merhaba hello konsol çıktısı **ReadDeviceToCloudMessages** uygulama IOT hub'ınızın aldığı hello iletileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="ebab3-174">hello console output from hello **ReadDeviceToCloudMessages** app shows hello messages that your IoT hub receives.</span></span>

    ![Uygulamalardan konsol çıktısı][42]

3. <span data-ttu-id="ebab3-176">Merhaba **kullanım** döşeme hello [Azure portal] [ lnk-portal] gösterir hello gönderilen iletileri toohello IOT hub'ı sayısı:</span><span class="sxs-lookup"><span data-stu-id="ebab3-176">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>

    ![Azure portalı Kullanım kutucuğu][43]

## <a name="next-steps"></a><span data-ttu-id="ebab3-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ebab3-178">Next steps</span></span>

<span data-ttu-id="ebab3-179">Bu öğreticide, bir IOT hub'hello Azure portal yapılandırılmış ve ardından hello IOT hub'ın kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="ebab3-179">In this tutorial, you configured an IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="ebab3-180">Bu cihaz kimliğini tooenable hello cihaz uygulama toosend cihaz bulut iletilerini toohello IOT hub kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ebab3-180">You used this device identity tooenable hello device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="ebab3-181">Merhaba hello IOT hub tarafından alınan iletileri görüntüleyen bir uygulama da oluşturmuş.</span><span class="sxs-lookup"><span data-stu-id="ebab3-181">You also created an app that displays hello messages received by hello IoT hub.</span></span>

<span data-ttu-id="ebab3-182">Başlarken toocontinue IOT Hub ve tooexplore diğer IOT senaryolarını bakın:</span><span class="sxs-lookup"><span data-stu-id="ebab3-182">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="ebab3-183">[Cihazınızı bağlama][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="ebab3-183">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="ebab3-184">[Cihaz yönetimini kullanmaya başlama][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="ebab3-184">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="ebab3-185">[IoT Edge ile çalışmaya başlama][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="ebab3-185">[Getting started with IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="ebab3-186">toolearn tooextend, IOT çözümü ve işlem cihaz bulut iletilerini ölçekli olarak nasıl görürüm hello [cihaz-bulut iletileri] [ lnk-process-d2c-tutorial] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="ebab3-186">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[41]: ./media/iot-hub-csharp-csharp-getstarted/run-apps1.png
[42]: ./media/iot-hub-csharp-csharp-getstarted/run-apps2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png
[10a]: ./media/iot-hub-csharp-csharp-getstarted/create-receive-csharp1.png
[10b]: ./media/iot-hub-csharp-csharp-getstarted/create-device-csharp1.png


<!-- Links -->
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-servicebus-nuget]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-device-nuget]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-connected-service]: https://visualstudiogallery.msdn.microsoft.com/e254a3a5-d72e-488e-9bd3-8fee8e0cd1d6
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
