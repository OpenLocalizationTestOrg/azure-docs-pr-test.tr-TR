---
title: "Azure IOT hub'ı işlemleri izleme | Microsoft Docs"
description: "Azure IOT Hub işlemleri gerçek zamanlı IOT hub'ınızı işlemlerinin durumunu izlemek için izleme kullanma"
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: a299f3a5-b14d-4586-9c3b-44aea14ed013
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.openlocfilehash: b6de5c5df5f9401a41be152bfa06eb994594e83d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="iot-hub-operations-monitoring"></a><span data-ttu-id="b0dfa-103">IOT hub'ı işlemlerini izleme</span><span class="sxs-lookup"><span data-stu-id="b0dfa-103">IoT Hub operations monitoring</span></span>

<span data-ttu-id="b0dfa-104">IOT hub'ı işlemlerini izleme işlemleri gerçek zamanlı IOT hub'ınızı durumunu izlemenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-104">IoT Hub operations monitoring enables you to monitor the status of operations on your IoT hub in real time.</span></span> <span data-ttu-id="b0dfa-105">IOT hub'ı operations birkaç kategoriler arasında olayları izler.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-105">IoT Hub tracks events across several categories of operations.</span></span> <span data-ttu-id="b0dfa-106">İşleme için IOT hub'ınızın bir uç nokta için bir veya daha fazla kategorilerden olayları göndermeyi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-106">You can opt into sending events from one or more categories to an endpoint of your IoT hub for processing.</span></span> <span data-ttu-id="b0dfa-107">Hatalar için verileri izlemek veya veri düzenlerini esas alarak daha karmaşık işleme ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-107">You can monitor the data for errors or set up more complex processing based on data patterns.</span></span>

<span data-ttu-id="b0dfa-108">IOT hub'ı olayların altı kategoriye izler:</span><span class="sxs-lookup"><span data-stu-id="b0dfa-108">IoT Hub monitors six categories of events:</span></span>

* <span data-ttu-id="b0dfa-109">Aygıt Kimliği işlemleri</span><span class="sxs-lookup"><span data-stu-id="b0dfa-109">Device identity operations</span></span>
* <span data-ttu-id="b0dfa-110">Cihaz telemetrisi</span><span class="sxs-lookup"><span data-stu-id="b0dfa-110">Device telemetry</span></span>
* <span data-ttu-id="b0dfa-111">Bulut-cihaz iletilerini</span><span class="sxs-lookup"><span data-stu-id="b0dfa-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="b0dfa-112">Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="b0dfa-112">Connections</span></span>
* <span data-ttu-id="b0dfa-113">Dosya yüklemeleri</span><span class="sxs-lookup"><span data-stu-id="b0dfa-113">File uploads</span></span>
* <span data-ttu-id="b0dfa-114">İleti yönlendirme</span><span class="sxs-lookup"><span data-stu-id="b0dfa-114">Message routing</span></span>

## <a name="how-to-enable-operations-monitoring"></a><span data-ttu-id="b0dfa-115">İzleme işlemlerini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="b0dfa-115">How to enable operations monitoring</span></span>

1. <span data-ttu-id="b0dfa-116">IOT hub'ı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-116">Create an IoT hub.</span></span> <span data-ttu-id="b0dfa-117">Bir IOT hub oluşturma hakkında yönergeler bulabilirsiniz [Get Started] [ lnk-get-started] Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-117">You can find instructions on how to create an IoT hub in the [Get Started][lnk-get-started] guide.</span></span>

1. <span data-ttu-id="b0dfa-118">IOT hub'ınızı dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-118">Open the blade of your IoT hub.</span></span> <span data-ttu-id="b0dfa-119">Buradan, tıklatın **izleme işlemleri**.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-119">From there, click **Operations monitoring**.</span></span>

    ![Yapılandırma portalında izleme erişim işlemleri][1]

1. <span data-ttu-id="b0dfa-121">İzleme ve ardından istediğiniz izleme kategorileri seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-121">Select the monitoring categories you wish to monitor, and then click **Save**.</span></span> <span data-ttu-id="b0dfa-122">Olaylar listelenen Event Hub ile uyumlu uç noktasından okumak için kullanılabilir **izleme ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-122">The events are available for reading from the Event Hub-compatible endpoint listed in **Monitoring settings**.</span></span> <span data-ttu-id="b0dfa-123">IOT hub'ı uç adlı `messages/operationsmonitoringevents`.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-123">The IoT Hub endpoint is called `messages/operationsmonitoringevents`.</span></span>

    ![IOT hub'ınızı üzerinde izleme işlemlerini yapılandırma][2]

> [!NOTE]
> <span data-ttu-id="b0dfa-125">Seçme **ayrıntılı** için izleme **bağlantıları** kategori ek tanılama iletilerini oluşturmak için IOT Hub neden olur.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-125">Selecting **Verbose** monitoring for the **Connections** category causes IoT Hub to generate additional diagnostics messages.</span></span> <span data-ttu-id="b0dfa-126">Diğer tüm kategorileri için **ayrıntılı** değişiklikleri IOT hub'ı bilgi miktarını ayarlama her hata iletisi içerir.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-126">For all other categories, the **Verbose** setting changes the quantity of information IoT Hub includes in each error message.</span></span>

## <a name="event-categories-and-how-to-use-them"></a><span data-ttu-id="b0dfa-127">Olay kategorilerini ve bunların nasıl kullanılacağını</span><span class="sxs-lookup"><span data-stu-id="b0dfa-127">Event categories and how to use them</span></span>

<span data-ttu-id="b0dfa-128">Her kategori parçaları izleme işlemleri farklı türde bir IOT Hub ve her izleme kategorisi etkileşimi bu kategorideki olayları nasıl yapılandırıldığı tanımlayan bir şema sahiptir.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-128">Each operations monitoring category tracks a different type of interaction with IoT Hub, and each monitoring category has a schema that defines how events in that category are structured.</span></span>

### <a name="device-identity-operations"></a><span data-ttu-id="b0dfa-129">Aygıt Kimliği işlemleri</span><span class="sxs-lookup"><span data-stu-id="b0dfa-129">Device identity operations</span></span>

<span data-ttu-id="b0dfa-130">Cihaz kimliği işlemleri kategorisi oluşturmak, güncelleştirmek ya da bir giriş, IOT hub'ın kimlik kayıt defterinde silme girişimi sırasında oluşan hataları izler.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-130">The device identity operations category tracks errors that occur when you attempt to create, update, or delete an entry in your IoT hub's identity registry.</span></span> <span data-ttu-id="b0dfa-131">Bu kategori izleme senaryoları sağlamak için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-131">Tracking this category is useful for provisioning scenarios.</span></span>

```json
{
    "time": "UTC timestamp",
        "operationName": "create",
        "category": "DeviceIdentityOperations",
        "level": "Error",
        "statusCode": 4XX,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "durationMs": 1234,
        "userAgent": "userAgent",
        "sharedAccessPolicy": "accessPolicy"
}
```

### <a name="device-telemetry"></a><span data-ttu-id="b0dfa-132">Cihaz telemetrisi</span><span class="sxs-lookup"><span data-stu-id="b0dfa-132">Device telemetry</span></span>

<span data-ttu-id="b0dfa-133">Cihaz telemetri kategorisini IOT hub'ına oluşur ve telemetri ardışık düzene ilgili hatalar izler.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-133">The device telemetry category tracks errors that occur at the IoT hub and are related to the telemetry pipeline.</span></span> <span data-ttu-id="b0dfa-134">Bu kategori (örneğin, azaltma) telemetri olayları gönderirken oluşan hataları içeren ve telemetri olayları (örneğin, yetkisiz okuyucu) alma.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-134">This category includes errors that occur when sending telemetry events (such as throttling) and receiving telemetry events (such as unauthorized reader).</span></span> <span data-ttu-id="b0dfa-135">Bu kategori cihazda çalışan kod nedeni hatalarını yakalama olamaz.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-135">This category cannot catch errors caused by code running on the device itself.</span></span>

```json
{
        "messageSizeInBytes": 1234,
        "batching": 0,
        "protocol": "Amqp",
        "authType": "{\"scope\":\"device\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
        "time": "UTC timestamp",
        "operationName": "ingress",
        "category": "DeviceTelemetry",
        "level": "Error",
        "statusCode": 4XX,
        "statusType": 4XX001,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "EventProcessedUtcTime": "UTC timestamp",
        "PartitionId": 1,
        "EventEnqueuedUtcTime": "UTC timestamp"
}
```

### <a name="cloud-to-device-commands"></a><span data-ttu-id="b0dfa-136">Bulut cihaz komutları</span><span class="sxs-lookup"><span data-stu-id="b0dfa-136">Cloud-to-device commands</span></span>

<span data-ttu-id="b0dfa-137">Bulut-cihaz komutlarını kategori IOT hub'ına oluşur ve bulut-cihaz ileti ardışık düzene ilgili hatalar izler.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-137">The cloud-to-device commands category tracks errors that occur at the IoT hub and are related to the cloud-to-device message pipeline.</span></span> <span data-ttu-id="b0dfa-138">Bu kategori (örneğin, yetkisiz gönderen) bulut cihaza ileti gönderme, (örneğin, teslimat sayısı aşıldı) bulut-cihaz iletilerini alma ve bulut-cihaz ileti geri bildirim (görüş süresi gibi) alırken oluşan hataları içerir.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-138">This category includes errors that occur when sending cloud-to-device messages (such as unauthorized sender), receiving cloud-to-device messages (such as delivery count exceeded), and receiving cloud-to-device message feedback (such as feedback expired).</span></span> <span data-ttu-id="b0dfa-139">Bu kategori, bulut cihaz iletisi başarılı bir şekilde teslim, yanlış bir bulut cihaz iletiyi işleyen bir aygıtı hatalarından yakalamaz.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-139">This category does not catch errors from a device that improperly handles a cloud-to-device message if the cloud-to-device message was delivered successfully.</span></span>

```json
{
    "messageSizeInBytes": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "deliveryAcknowledgement": 0,
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "C2DCommands",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "EventProcessedUtcTime": "UTC timestamp",
    "PartitionId": 1,
    "EventEnqueuedUtcTime": “UTC timestamp"
}
```

### <a name="connections"></a><span data-ttu-id="b0dfa-140">Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="b0dfa-140">Connections</span></span>

<span data-ttu-id="b0dfa-141">Bağlantıları kategorisi cihazlar bağlanmak veya IOT hub'ından bağlantısını oluşan hataları izler.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-141">The connections category tracks errors that occur when devices connect or disconnect from an IoT hub.</span></span> <span data-ttu-id="b0dfa-142">Bu kategori izleme, yetkisiz bağlantı denemeleri tanımlamak için ve zamanlar zayıf bağlantıya alanlarında cihazlar için bir bağlantı kesildiğinde izlemek için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-142">Tracking this category is useful for identifying unauthorized connection attempts and for tracking when a connection is lost for devices in areas of poor connectivity.</span></span>

```json
{
    "durationMs": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "deviceConnect",
    "category": "Connections",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID"
}
```

### <a name="file-uploads"></a><span data-ttu-id="b0dfa-143">Dosya yüklemeleri</span><span class="sxs-lookup"><span data-stu-id="b0dfa-143">File uploads</span></span>

<span data-ttu-id="b0dfa-144">Dosya karşıya yükleme kategori IOT hub'ına oluşur ve dosya karşıya yükleme işlevselliği için ilgili hatalar izler.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-144">The file upload category tracks errors that occur at the IoT hub and are related to file upload functionality.</span></span> <span data-ttu-id="b0dfa-145">Bu kategori içerir:</span><span class="sxs-lookup"><span data-stu-id="b0dfa-145">This category includes:</span></span>

* <span data-ttu-id="b0dfa-146">Bir aygıt tamamlanan karşıya yükleme hub'ını bildirir önce onu süresi dolduğunda gibi SAS URI'si ile oluşan hatalar.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-146">Errors that occur with the SAS URI, such as when it expires before a device notifies the hub of a completed upload.</span></span>
* <span data-ttu-id="b0dfa-147">Cihaz tarafından raporlanan yüklemeler başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-147">Failed uploads reported by the device.</span></span>
* <span data-ttu-id="b0dfa-148">Bir dosya depolama alanına IOT hub'ı bildirim iletisi oluşturma sırasında bulunamadı kullanırken oluşan hatalar.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-148">Errors that occur when a file is not found in storage during IoT Hub notification message creation.</span></span>

<span data-ttu-id="b0dfa-149">Bu kategori, cihaz bir dosya depolama alanına yükleme doğrudan oluşan hatalar catch olamaz.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-149">This category cannot catch errors that directly occur while the device is uploading a file to storage.</span></span>

```json
{
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "HTTP",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "fileUpload",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "blobUri": "http//bloburi.com",
    "durationMs": 1234
}
```

### <a name="message-routing"></a><span data-ttu-id="b0dfa-150">İleti yönlendirme</span><span class="sxs-lookup"><span data-stu-id="b0dfa-150">Message routing</span></span>

<span data-ttu-id="b0dfa-151">İleti yönlendirme kategorisi ileti rota değerlendirme ve IOT Hub tarafından algılanan gibi uç noktası sistem durumu sırasında oluşan hataları izler.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-151">The message routing category tracks errors that occur during message route evaluation and endpoint health as perceived by IoT Hub.</span></span> <span data-ttu-id="b0dfa-152">Bir kural "tanımsız" değerlendirildiğinde zaman IOT hub'ı bir uç nokta olarak atılacak ve bir uç noktasından alınan hatalarını işaretler gibi bu kategoriyi olaylarını içerir.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-152">This category includes events such as when a rule evaluates to "undefined", when IoT Hub marks an endpoint as dead, and any other errors received from an endpoint.</span></span> <span data-ttu-id="b0dfa-153">Bu kategori "cihaz telemetrisi" kategorisi altında bildirilen iletilerini kendileri (örneğin, aygıt) hataları azaltma hakkında belirli hataları içermez.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-153">This category does not include specific errors about the messages themselves (such as device throttling errors), which are reported under the "device telemetry" category.</span></span>

```json
{
    "messageSizeInBytes": 1234,
    "time": "UTC timestamp",
    "operationName": "ingress",
    "category": "routes",
    "level": "Error",
    "deviceId": "device-ID",
    "messageId": "ID of message",
    "routeName": "myroute",
    "endpointName": "myendpoint",
    "details": "ExternalEndpointDisabled"
}
```

## <a name="view-events"></a><span data-ttu-id="b0dfa-154">Etkinlikleri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="b0dfa-154">View events</span></span>

<span data-ttu-id="b0dfa-155">Kullanabileceğiniz *iothub-explorer* hızla IOT hub'ınızı izleme olayları oluşturmak, sınamak için aracı.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-155">You can use the *iothub-explorer* tool to quickly test that your IoT hub is generating monitoring events.</span></span> <span data-ttu-id="b0dfa-156">Aracı yüklemek için yönergeleri görmek [iothub-explorer] [ lnk-iothub-explorer] GitHub depo.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-156">To install the tool, see the instructions in the [iothub-explorer][lnk-iothub-explorer] GitHub repository.</span></span>

1. <span data-ttu-id="b0dfa-157">Emin olun **bağlantıları** kategori izleme ayarlanmış **ayrıntılı** Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-157">Make sure the **Connections** monitoring category is set to **Verbose** in the portal.</span></span>

1. <span data-ttu-id="b0dfa-158">Bir komut isteminde, izleme uç noktasından okumak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b0dfa-158">At a command-prompt, run the following command to read from the monitoring endpoint:</span></span>

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="b0dfa-159">Başka bir komut isteminden, cihaz-bulut iletileri gönderen bir cihazın benzetimini yapmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b0dfa-159">In another command-prompt, run the following command to simulate a device sending device-to-cloud messages:</span></span>

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="b0dfa-160">Sanal cihaz IOT hub'ına bağlandığında ilk komut istemi izleme olayları gösterir.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-160">The first command-prompt shows the monitoring events as the simulated device connects to your IoT hub.</span></span>

## <a name="connect-to-the-monitoring-endpoint"></a><span data-ttu-id="b0dfa-161">İzleme uç noktasına bağlanın</span><span class="sxs-lookup"><span data-stu-id="b0dfa-161">Connect to the monitoring endpoint</span></span>

<span data-ttu-id="b0dfa-162">IOT hub'ınızı izleme uç noktada bir Event Hub ile uyumlu uç noktadır.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-162">The monitoring endpoint on your IoT hub is an Event Hub-compatible endpoint.</span></span> <span data-ttu-id="b0dfa-163">İzleme iletileri Bu uç noktasından okumak için Event Hubs ile çalışan herhangi bir mekanizma kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-163">You can use any mechanism that works with Event Hubs to read monitoring messages from this endpoint.</span></span> <span data-ttu-id="b0dfa-164">Aşağıdaki örnek, bir yüksek işleme dağıtımına uygun olmayan temel bir okuyucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-164">The following sample creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="b0dfa-165">Event Hubs'dan iletilerin nasıl işleneceği hakkında daha fazla bilgi için [Event Hubs ile Çalışmaya Başlama][lnk-eventhubs-tutorial] öğreticisine bakın.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-165">For more information about how to process messages from Event Hubs, see the [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span>

<span data-ttu-id="b0dfa-166">İzleme uç noktasına bağlanmak için bir bağlantı dizesi ve uç nokta adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-166">To connect to the monitoring endpoint, you need a connection string and the endpoint name.</span></span> <span data-ttu-id="b0dfa-167">Aşağıdaki adımlar Portalı'nda gerekli değerleri bulmaya nasıl gösterir:</span><span class="sxs-lookup"><span data-stu-id="b0dfa-167">The following steps show you how to find the necessary values in the portal:</span></span>

1. <span data-ttu-id="b0dfa-168">Portalda, IOT Hub kaynağı dikey penceresine gidin.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-168">In the portal, navigate to your IoT Hub resource blade.</span></span>

1. <span data-ttu-id="b0dfa-169">Seçin **izleme işlemleri**ve Not **Event Hub ile uyumlu adı** ve **Event Hub ile uyumlu uç nokta** değerler:</span><span class="sxs-lookup"><span data-stu-id="b0dfa-169">Choose **Operations monitoring**, and make a note of the **Event Hub-compatible name** and **Event Hub-compatible endpoint** values:</span></span>

    ![Olay Hub ile uyumlu uç nokta değerleri][img-endpoints]

1. <span data-ttu-id="b0dfa-171">Seçin **paylaşılan erişim ilkeleri**, ardından **hizmet**.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-171">Choose **Shared access policies**, then choose **service**.</span></span> <span data-ttu-id="b0dfa-172">Not **birincil anahtar** değeri:</span><span class="sxs-lookup"><span data-stu-id="b0dfa-172">Make a note of the **Primary key** value:</span></span>

    ![Hizmet paylaşılan erişim ilkesi birincil anahtarı][img-service-key]

<span data-ttu-id="b0dfa-174">Aşağıdaki C# kod örneği, Visual Studio'dan alınır **Windows Klasik Masaüstü** C# konsol uygulaması.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-174">The following C# code sample is taken from a Visual Studio **Windows Classic Desktop** C# console app.</span></span> <span data-ttu-id="b0dfa-175">Proje **WindowsAzure.ServiceBus** NuGet paketi yüklü.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-175">The project has the **WindowsAzure.ServiceBus** NuGet package installed.</span></span>

* <span data-ttu-id="b0dfa-176">Bağlantı dizesi yer tutucusunu kullanan bir bağlantı dizesi ile değiştirin **Event Hub ile uyumlu uç nokta** ve hizmet **birincil anahtar** aşağıdaki örnekte gösterildiği gibi daha önce not ettiğiniz değerleri:</span><span class="sxs-lookup"><span data-stu-id="b0dfa-176">Replace the connection string placeholder with a connection string that uses the **Event Hub-compatible endpoint** and service **Primary key** values you noted previously as shown in the following example:</span></span>

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* <span data-ttu-id="b0dfa-177">İzleme uç nokta ad yer tutucusu ile Değiştir **Event Hub ile uyumlu adı** daha önce not ettiğiniz değer.</span><span class="sxs-lookup"><span data-stu-id="b0dfa-177">Replace the monitoring endpoint name placeholder with the **Event Hub-compatible name** value you noted previously.</span></span>

```cs
class Program
{
    static string connectionString = "{your monitoring endpoint connection string}";
    static string monitoringEndpointName = "{your monitoring endpoint name}";
    static EventHubClient eventHubClient;

    static void Main(string[] args)
    {
        Console.WriteLine("Monitoring. Press Enter key to exit.\n");

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, monitoringEndpointName);
        var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;
        CancellationTokenSource cts = new CancellationTokenSource();
        var tasks = new List<Task>();

        foreach (string partition in d2cPartitions)
        {
            tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
        }

        Console.ReadLine();
        Console.WriteLine("Exiting...");
        cts.Cancel();
        Task.WaitAll(tasks.ToArray());
    }

    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested)
            {
                await eventHubReceiver.CloseAsync();
                break;
            }

            EventData eventData = await eventHubReceiver.ReceiveAsync(new TimeSpan(0,0,10));

            if (eventData != null)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
            }
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="b0dfa-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b0dfa-178">Next steps</span></span>
<span data-ttu-id="b0dfa-179">Daha fazla IOT hub'ı özelliklerini keşfetmek için bkz:</span><span class="sxs-lookup"><span data-stu-id="b0dfa-179">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="b0dfa-180">[IOT Hub Geliştirici Kılavuzu][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="b0dfa-180">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="b0dfa-181">[Bir aygıt ile Azure IOT kenar benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="b0dfa-181">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links and images -->
[1]: media/iot-hub-operations-monitoring/enable-OM-1.png
[2]: media/iot-hub-operations-monitoring/enable-OM-2.png
[img-endpoints]: media/iot-hub-operations-monitoring/monitoring-endpoint.png
[img-service-key]: media/iot-hub-operations-monitoring/service-key.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[lnk-diagnostic-metrics]: iot-hub-metrics.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-dr]: iot-hub-ha-dr.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer
[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md