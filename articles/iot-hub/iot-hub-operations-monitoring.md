---
title: "İzleme aaaAzure IOT hub'ı operations | Microsoft Docs"
description: "Nasıl toomonitor izleme toouse Azure IOT Hub işlemleri gerçek zamanlı IOT hub'ınızı işlemlerinin durumunu hello."
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
ms.openlocfilehash: a0b233ef2d9bd0827e19fa30fdbdd49b2b61b813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="iot-hub-operations-monitoring"></a><span data-ttu-id="7b26a-103">IOT hub'ı işlemlerini izleme</span><span class="sxs-lookup"><span data-stu-id="7b26a-103">IoT Hub operations monitoring</span></span>

<span data-ttu-id="7b26a-104">IOT hub'ı operations izleme toomonitor hello durumunu gerçek zamanlı IOT hub'ınızı işlemlerinin sağlar.</span><span class="sxs-lookup"><span data-stu-id="7b26a-104">IoT Hub operations monitoring enables you toomonitor hello status of operations on your IoT hub in real time.</span></span> <span data-ttu-id="7b26a-105">IOT hub'ı operations birkaç kategoriler arasında olayları izler.</span><span class="sxs-lookup"><span data-stu-id="7b26a-105">IoT Hub tracks events across several categories of operations.</span></span> <span data-ttu-id="7b26a-106">IOT hub'ınızın işlemek için bir veya daha fazla kategorileri tooan uç noktasından olayları göndermeyi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b26a-106">You can opt into sending events from one or more categories tooan endpoint of your IoT hub for processing.</span></span> <span data-ttu-id="7b26a-107">Merhaba veri hataları izleme veya veri düzenlerini esas alarak daha karmaşık işleme ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7b26a-107">You can monitor hello data for errors or set up more complex processing based on data patterns.</span></span>

<span data-ttu-id="7b26a-108">IOT hub'ı olayların altı kategoriye izler:</span><span class="sxs-lookup"><span data-stu-id="7b26a-108">IoT Hub monitors six categories of events:</span></span>

* <span data-ttu-id="7b26a-109">Aygıt Kimliği işlemleri</span><span class="sxs-lookup"><span data-stu-id="7b26a-109">Device identity operations</span></span>
* <span data-ttu-id="7b26a-110">Cihaz telemetrisi</span><span class="sxs-lookup"><span data-stu-id="7b26a-110">Device telemetry</span></span>
* <span data-ttu-id="7b26a-111">Bulut-cihaz iletilerini</span><span class="sxs-lookup"><span data-stu-id="7b26a-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="7b26a-112">Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="7b26a-112">Connections</span></span>
* <span data-ttu-id="7b26a-113">Dosya yüklemeleri</span><span class="sxs-lookup"><span data-stu-id="7b26a-113">File uploads</span></span>
* <span data-ttu-id="7b26a-114">İleti yönlendirme</span><span class="sxs-lookup"><span data-stu-id="7b26a-114">Message routing</span></span>

## <a name="how-tooenable-operations-monitoring"></a><span data-ttu-id="7b26a-115">Nasıl tooenable işlemlerini izleme</span><span class="sxs-lookup"><span data-stu-id="7b26a-115">How tooenable operations monitoring</span></span>

1. <span data-ttu-id="7b26a-116">IOT hub'ı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7b26a-116">Create an IoT hub.</span></span> <span data-ttu-id="7b26a-117">Hakkında yönergeler bulabilirsiniz toocreate bir IOT hub'hello [Get Started] [ lnk-get-started] Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="7b26a-117">You can find instructions on how toocreate an IoT hub in hello [Get Started][lnk-get-started] guide.</span></span>

1. <span data-ttu-id="7b26a-118">IOT hub'ınızı Hello dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="7b26a-118">Open hello blade of your IoT hub.</span></span> <span data-ttu-id="7b26a-119">Buradan, tıklatın **izleme işlemleri**.</span><span class="sxs-lookup"><span data-stu-id="7b26a-119">From there, click **Operations monitoring**.</span></span>

    ![Merhaba portalındaki izleme erişim işlemleri][1]

1. <span data-ttu-id="7b26a-121">Select hello toomonitor ister ve ardından kategorileri izleme **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="7b26a-121">Select hello monitoring categories you wish toomonitor, and then click **Save**.</span></span> <span data-ttu-id="7b26a-122">Merhaba olayları listelenen hello Event Hub ile uyumlu uç noktasından okumak için kullanılabilir **izleme ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="7b26a-122">hello events are available for reading from hello Event Hub-compatible endpoint listed in **Monitoring settings**.</span></span> <span data-ttu-id="7b26a-123">Merhaba IOT hub'ı uç adlandırılır `messages/operationsmonitoringevents`.</span><span class="sxs-lookup"><span data-stu-id="7b26a-123">hello IoT Hub endpoint is called `messages/operationsmonitoringevents`.</span></span>

    ![IOT hub'ınızı üzerinde izleme işlemlerini yapılandırma][2]

> [!NOTE]
> <span data-ttu-id="7b26a-125">Seçme **ayrıntılı** Merhaba izleme **bağlantıları** kategori toogenerate ek tanılama iletilerini IOT Hub neden olur.</span><span class="sxs-lookup"><span data-stu-id="7b26a-125">Selecting **Verbose** monitoring for hello **Connections** category causes IoT Hub toogenerate additional diagnostics messages.</span></span> <span data-ttu-id="7b26a-126">Diğer tüm kategorileri için hello **ayrıntılı** değişiklikleri bilgi IOT hub'ı hello miktarını ayarlama her hata iletisi içerir.</span><span class="sxs-lookup"><span data-stu-id="7b26a-126">For all other categories, hello **Verbose** setting changes hello quantity of information IoT Hub includes in each error message.</span></span>

## <a name="event-categories-and-how-toouse-them"></a><span data-ttu-id="7b26a-127">Olay kategorileri ve nasıl toouse bunları</span><span class="sxs-lookup"><span data-stu-id="7b26a-127">Event categories and how toouse them</span></span>

<span data-ttu-id="7b26a-128">Her kategori parçaları izleme işlemleri farklı türde bir IOT Hub ve her izleme kategorisi etkileşimi bu kategorideki olayları nasıl yapılandırıldığı tanımlayan bir şema sahiptir.</span><span class="sxs-lookup"><span data-stu-id="7b26a-128">Each operations monitoring category tracks a different type of interaction with IoT Hub, and each monitoring category has a schema that defines how events in that category are structured.</span></span>

### <a name="device-identity-operations"></a><span data-ttu-id="7b26a-129">Aygıt Kimliği işlemleri</span><span class="sxs-lookup"><span data-stu-id="7b26a-129">Device identity operations</span></span>

<span data-ttu-id="7b26a-130">Merhaba aygıt kimlik işlemleri kategorisini toocreate çalıştığınızda oluşan hataları izler, güncelleştirmek ya da, IOT hub'ın kimlik kayıt defterinde bir girişi silmek.</span><span class="sxs-lookup"><span data-stu-id="7b26a-130">hello device identity operations category tracks errors that occur when you attempt toocreate, update, or delete an entry in your IoT hub's identity registry.</span></span> <span data-ttu-id="7b26a-131">Bu kategori izleme senaryoları sağlamak için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="7b26a-131">Tracking this category is useful for provisioning scenarios.</span></span>

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

### <a name="device-telemetry"></a><span data-ttu-id="7b26a-132">Cihaz telemetrisi</span><span class="sxs-lookup"><span data-stu-id="7b26a-132">Device telemetry</span></span>

<span data-ttu-id="7b26a-133">Merhaba cihaz telemetri kategorisini hello IOT hub'ına oluşur ve ilgili toohello telemetri ardışık düzen hatalarını izler.</span><span class="sxs-lookup"><span data-stu-id="7b26a-133">hello device telemetry category tracks errors that occur at hello IoT hub and are related toohello telemetry pipeline.</span></span> <span data-ttu-id="7b26a-134">Bu kategori (örneğin, azaltma) telemetri olayları gönderirken oluşan hataları içeren ve telemetri olayları (örneğin, yetkisiz okuyucu) alma.</span><span class="sxs-lookup"><span data-stu-id="7b26a-134">This category includes errors that occur when sending telemetry events (such as throttling) and receiving telemetry events (such as unauthorized reader).</span></span> <span data-ttu-id="7b26a-135">Bu kategori hello cihazının kendisinde çalışan kodu nedeni hatalarını yakalama olamaz.</span><span class="sxs-lookup"><span data-stu-id="7b26a-135">This category cannot catch errors caused by code running on hello device itself.</span></span>

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

### <a name="cloud-to-device-commands"></a><span data-ttu-id="7b26a-136">Bulut cihaz komutları</span><span class="sxs-lookup"><span data-stu-id="7b26a-136">Cloud-to-device commands</span></span>

<span data-ttu-id="7b26a-137">Merhaba bulut-cihaz komutlarını kategori hello IOT hub'ına oluşur ve ilgili toohello bulut cihaz ileti işlem hattını hataları izler.</span><span class="sxs-lookup"><span data-stu-id="7b26a-137">hello cloud-to-device commands category tracks errors that occur at hello IoT hub and are related toohello cloud-to-device message pipeline.</span></span> <span data-ttu-id="7b26a-138">Bu kategori (örneğin, yetkisiz gönderen) bulut cihaza ileti gönderme, (örneğin, teslimat sayısı aşıldı) bulut-cihaz iletilerini alma ve bulut-cihaz ileti geri bildirim (görüş süresi gibi) alırken oluşan hataları içerir.</span><span class="sxs-lookup"><span data-stu-id="7b26a-138">This category includes errors that occur when sending cloud-to-device messages (such as unauthorized sender), receiving cloud-to-device messages (such as delivery count exceeded), and receiving cloud-to-device message feedback (such as feedback expired).</span></span> <span data-ttu-id="7b26a-139">Bu kategori hello bulut aygıt iletisi başarılı bir şekilde teslim, yanlış bir bulut cihaz iletiyi işleyen bir aygıtı hatalarından yakalamaz.</span><span class="sxs-lookup"><span data-stu-id="7b26a-139">This category does not catch errors from a device that improperly handles a cloud-to-device message if hello cloud-to-device message was delivered successfully.</span></span>

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

### <a name="connections"></a><span data-ttu-id="7b26a-140">Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="7b26a-140">Connections</span></span>

<span data-ttu-id="7b26a-141">Merhaba bağlantıları kategorisi cihazlar bağlanmak veya IOT hub'ından bağlantısını oluşan hataları izler.</span><span class="sxs-lookup"><span data-stu-id="7b26a-141">hello connections category tracks errors that occur when devices connect or disconnect from an IoT hub.</span></span> <span data-ttu-id="7b26a-142">Bu kategori izleme, yetkisiz bağlantı denemeleri tanımlamak için ve zamanlar zayıf bağlantıya alanlarında cihazlar için bir bağlantı kesildiğinde izlemek için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="7b26a-142">Tracking this category is useful for identifying unauthorized connection attempts and for tracking when a connection is lost for devices in areas of poor connectivity.</span></span>

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

### <a name="file-uploads"></a><span data-ttu-id="7b26a-143">Dosya yüklemeleri</span><span class="sxs-lookup"><span data-stu-id="7b26a-143">File uploads</span></span>

<span data-ttu-id="7b26a-144">Merhaba dosya karşıya yükleme kategori hello IOT hub'ına oluşur ve ilgili toofile karşıya yükleme işlevselliği olan hataları izler.</span><span class="sxs-lookup"><span data-stu-id="7b26a-144">hello file upload category tracks errors that occur at hello IoT hub and are related toofile upload functionality.</span></span> <span data-ttu-id="7b26a-145">Bu kategori içerir:</span><span class="sxs-lookup"><span data-stu-id="7b26a-145">This category includes:</span></span>

* <span data-ttu-id="7b26a-146">Merhaba hub tamamlanan karşıya yükleme, bir cihaz bildirir önce onu süresi dolduğunda gibi hello SAS URI'si ile oluşan hatalar.</span><span class="sxs-lookup"><span data-stu-id="7b26a-146">Errors that occur with hello SAS URI, such as when it expires before a device notifies hello hub of a completed upload.</span></span>
* <span data-ttu-id="7b26a-147">Merhaba cihaz tarafından raporlanan yüklemeler başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="7b26a-147">Failed uploads reported by hello device.</span></span>
* <span data-ttu-id="7b26a-148">Bir dosya depolama alanına IOT hub'ı bildirim iletisi oluşturma sırasında bulunamadı kullanırken oluşan hatalar.</span><span class="sxs-lookup"><span data-stu-id="7b26a-148">Errors that occur when a file is not found in storage during IoT Hub notification message creation.</span></span>

<span data-ttu-id="7b26a-149">Bu kategori hello aygıt dosya toostorage karşıya doğrudan oluşan hatalar catch olamaz.</span><span class="sxs-lookup"><span data-stu-id="7b26a-149">This category cannot catch errors that directly occur while hello device is uploading a file toostorage.</span></span>

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

### <a name="message-routing"></a><span data-ttu-id="7b26a-150">İleti yönlendirme</span><span class="sxs-lookup"><span data-stu-id="7b26a-150">Message routing</span></span>

<span data-ttu-id="7b26a-151">Merhaba ileti yönlendirme kategorisi ileti rota değerlendirme ve IOT Hub tarafından algılanan gibi uç noktası sistem durumu sırasında oluşan hataları izler.</span><span class="sxs-lookup"><span data-stu-id="7b26a-151">hello message routing category tracks errors that occur during message route evaluation and endpoint health as perceived by IoT Hub.</span></span> <span data-ttu-id="7b26a-152">Bir kural "tanımsız" çok değerlendirildiğinde zaman IOT hub'ı bir uç nokta olarak atılacak ve bir uç noktasından alınan hatalarını işaretler gibi bu kategoriyi olaylarını içerir.</span><span class="sxs-lookup"><span data-stu-id="7b26a-152">This category includes events such as when a rule evaluates too"undefined", when IoT Hub marks an endpoint as dead, and any other errors received from an endpoint.</span></span> <span data-ttu-id="7b26a-153">Bu kategori hello "cihaz telemetrisi" kategorisi altında bildirilen hello iletilerini kendileri (örneğin, aygıt) hataları azaltma hakkında belirli hataları içermez.</span><span class="sxs-lookup"><span data-stu-id="7b26a-153">This category does not include specific errors about hello messages themselves (such as device throttling errors), which are reported under hello "device telemetry" category.</span></span>

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

## <a name="view-events"></a><span data-ttu-id="7b26a-154">Etkinlikleri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="7b26a-154">View events</span></span>

<span data-ttu-id="7b26a-155">Merhaba kullanabilirsiniz *iothub-explorer* aracı tooquickly test IOT hub'ınızı izleme olayı oluşturuyor.</span><span class="sxs-lookup"><span data-stu-id="7b26a-155">You can use hello *iothub-explorer* tool tooquickly test that your IoT hub is generating monitoring events.</span></span> <span data-ttu-id="7b26a-156">tooinstall hello aracı, hello hello yönergelerini görmek [iothub-explorer] [ lnk-iothub-explorer] GitHub depo.</span><span class="sxs-lookup"><span data-stu-id="7b26a-156">tooinstall hello tool, see hello instructions in hello [iothub-explorer][lnk-iothub-explorer] GitHub repository.</span></span>

1. <span data-ttu-id="7b26a-157">Merhaba emin olun **bağlantıları** kategori izleme ayarlanmış çok**ayrıntılı** hello Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="7b26a-157">Make sure hello **Connections** monitoring category is set too**Verbose** in hello portal.</span></span>

1. <span data-ttu-id="7b26a-158">Bir komut isteminde, uç nokta izleme hello komutu tooread aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7b26a-158">At a command-prompt, run hello following command tooread from hello monitoring endpoint:</span></span>

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="7b26a-159">Başka bir komut isteminden komut toosimulate aşağıdaki hello cihaz-bulut iletileri gönderen bir aygıt çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7b26a-159">In another command-prompt, run hello following command toosimulate a device sending device-to-cloud messages:</span></span>

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="7b26a-160">Merhaba sanal cihaz tooyour IOT hub'a bağlandığında hello ilk komut istemi hello izleme olayları gösterir.</span><span class="sxs-lookup"><span data-stu-id="7b26a-160">hello first command-prompt shows hello monitoring events as hello simulated device connects tooyour IoT hub.</span></span>

## <a name="connect-toohello-monitoring-endpoint"></a><span data-ttu-id="7b26a-161">Uç nokta izleme toohello Bağlan</span><span class="sxs-lookup"><span data-stu-id="7b26a-161">Connect toohello monitoring endpoint</span></span>

<span data-ttu-id="7b26a-162">IOT hub'ınızı noktadaki izleme hello bir Event Hub ile uyumlu uç noktadır.</span><span class="sxs-lookup"><span data-stu-id="7b26a-162">hello monitoring endpoint on your IoT hub is an Event Hub-compatible endpoint.</span></span> <span data-ttu-id="7b26a-163">Bu uç noktasından olay hub'ları tooread izleme iletileri ile birlikte çalışan herhangi bir mekanizma kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b26a-163">You can use any mechanism that works with Event Hubs tooread monitoring messages from this endpoint.</span></span> <span data-ttu-id="7b26a-164">Merhaba aşağıdaki örnek, bir yüksek işleme dağıtımına uygun olmayan temel bir okuyucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7b26a-164">hello following sample creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="7b26a-165">Merhaba nasıl tooprocess olay hub'larından iletileri hakkında daha fazla bilgi için bkz: [Event Hubs ile çalışmaya başlama] [ lnk-eventhubs-tutorial] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="7b26a-165">For more information about how tooprocess messages from Event Hubs, see hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span>

<span data-ttu-id="7b26a-166">tooconnect toohello izleme uç noktası, bir bağlantı dizesi ve hello uç nokta adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b26a-166">tooconnect toohello monitoring endpoint, you need a connection string and hello endpoint name.</span></span> <span data-ttu-id="7b26a-167">Aşağıdaki adımları hello nasıl toofind hello hello Portalı'nda gerekli değerleri göster:</span><span class="sxs-lookup"><span data-stu-id="7b26a-167">hello following steps show you how toofind hello necessary values in hello portal:</span></span>

1. <span data-ttu-id="7b26a-168">Merhaba Portalı'nda tooyour IOT hub'ı kaynak dikey penceresine gidin.</span><span class="sxs-lookup"><span data-stu-id="7b26a-168">In hello portal, navigate tooyour IoT Hub resource blade.</span></span>

1. <span data-ttu-id="7b26a-169">Seçin **izleme işlemleri**ve hello Not **Event Hub ile uyumlu adı** ve **Event Hub ile uyumlu uç nokta** değerler:</span><span class="sxs-lookup"><span data-stu-id="7b26a-169">Choose **Operations monitoring**, and make a note of hello **Event Hub-compatible name** and **Event Hub-compatible endpoint** values:</span></span>

    ![Olay Hub ile uyumlu uç nokta değerleri][img-endpoints]

1. <span data-ttu-id="7b26a-171">Seçin **paylaşılan erişim ilkeleri**, ardından **hizmet**.</span><span class="sxs-lookup"><span data-stu-id="7b26a-171">Choose **Shared access policies**, then choose **service**.</span></span> <span data-ttu-id="7b26a-172">Merhaba Not **birincil anahtar** değeri:</span><span class="sxs-lookup"><span data-stu-id="7b26a-172">Make a note of hello **Primary key** value:</span></span>

    ![Hizmet paylaşılan erişim ilkesi birincil anahtarı][img-service-key]

<span data-ttu-id="7b26a-174">Merhaba aşağıdaki C# kod örneği Visual Studio'dan alınır **Windows Klasik Masaüstü** C# konsol uygulaması.</span><span class="sxs-lookup"><span data-stu-id="7b26a-174">hello following C# code sample is taken from a Visual Studio **Windows Classic Desktop** C# console app.</span></span> <span data-ttu-id="7b26a-175">Merhaba proje sahip hello **WindowsAzure.ServiceBus** NuGet paketi yüklü.</span><span class="sxs-lookup"><span data-stu-id="7b26a-175">hello project has hello **WindowsAzure.ServiceBus** NuGet package installed.</span></span>

* <span data-ttu-id="7b26a-176">Merhaba bağlantı dizesi yer tutucusunu hello kullanan bir bağlantı dizesi ile değiştirin **Event Hub ile uyumlu uç nokta** ve hizmet **birincil anahtar** hello aşağıda gösterildiği gibi daha önce not ettiğiniz değerleri Örnek:</span><span class="sxs-lookup"><span data-stu-id="7b26a-176">Replace hello connection string placeholder with a connection string that uses hello **Event Hub-compatible endpoint** and service **Primary key** values you noted previously as shown in hello following example:</span></span>

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* <span data-ttu-id="7b26a-177">Uç nokta ad yer tutucusu hello ile izleme hello yerine **Event Hub ile uyumlu adı** daha önce not ettiğiniz değer.</span><span class="sxs-lookup"><span data-stu-id="7b26a-177">Replace hello monitoring endpoint name placeholder with hello **Event Hub-compatible name** value you noted previously.</span></span>

```cs
class Program
{
    static string connectionString = "{your monitoring endpoint connection string}";
    static string monitoringEndpointName = "{your monitoring endpoint name}";
    static EventHubClient eventHubClient;

    static void Main(string[] args)
    {
        Console.WriteLine("Monitoring. Press Enter key tooexit.\n");

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

## <a name="next-steps"></a><span data-ttu-id="7b26a-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7b26a-178">Next steps</span></span>
<span data-ttu-id="7b26a-179">toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:</span><span class="sxs-lookup"><span data-stu-id="7b26a-179">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="7b26a-180">[IOT Hub Geliştirici Kılavuzu][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="7b26a-180">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="7b26a-181">[Bir aygıt ile Azure IOT kenar benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="7b26a-181">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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