---
title: "yollar (.Net) kullanılarak aaaProcess Azure IOT Hub cihaz bulut iletilerini | Microsoft Docs"
description: "Nasıl tooprocess yönlendirme kuralları ve özel uç noktaları toodispatch kullanarak IOT Hub cihaz bulut iletilerini tooother arka uç hizmetlerini iletileri."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 5177bac9-722f-47ef-8a14-b201142ba4bc
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: c1dd5be04ca30c65af2be466ba6c8c1858333154
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a><span data-ttu-id="5388e-103">Yollar (.NET) kullanılarak IOT Hub cihaz bulut iletilerini işleme</span><span class="sxs-lookup"><span data-stu-id="5388e-103">Process IoT Hub device-to-cloud messages using routes (.NET)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="5388e-104">Bu öğretici üzerinde hello derlemeler [IOT Hub ile çalışmaya başlama] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="5388e-104">This tutorial builds on hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="5388e-105">Başlangıç Öğreticisi:</span><span class="sxs-lookup"><span data-stu-id="5388e-105">hello tutorial:</span></span>

* <span data-ttu-id="5388e-106">Nasıl toouse yönlendirme toodispatch cihaz bulut iletilerini bir kolay, yapılandırma tabanlı şekilde kuralları gösterir.</span><span class="sxs-lookup"><span data-stu-id="5388e-106">Shows you how toouse routing rules toodispatch device-to-cloud messages in an easy, configuration-based way.</span></span>
* <span data-ttu-id="5388e-107">Nasıl hello çözümden Acil eylem gerektiren tooisolate etkileşimli iletilerin arka uç başka bir işleme için gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5388e-107">Illustrates how tooisolate interactive messages that require immediate action from hello solution back end for further processing.</span></span> <span data-ttu-id="5388e-108">Örneğin, bir aygıt bir bilet bir CRM sistemine ekleme tetikleyen bir uyarı iletisi gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="5388e-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="5388e-109">Buna karşılık, sıcaklık telemetri gibi veri noktası iletileri analytics motoruna akış.</span><span class="sxs-lookup"><span data-stu-id="5388e-109">In contrast, data-point messages, such as temperature telemetry, feed into an analytics engine.</span></span>

<span data-ttu-id="5388e-110">Bu öğretici Hello sonunda üç .NET konsol uygulamaları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="5388e-110">At hello end of this tutorial, you run three .NET console apps:</span></span>

* <span data-ttu-id="5388e-111">**SimulatedDevice**, hello oluşturulan hello uygulaması değiştirilmiş bir sürümünü [IOT Hub ile çalışmaya başlama] öğretici saniyede veri noktası cihaz bulut iletilerini gönderir ve etkileşimli cihaz bulut iletilerini her 10 saniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="5388e-111">**SimulatedDevice**, a modified version of hello app created in hello [Get started with IoT Hub] tutorial sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span>
* <span data-ttu-id="5388e-112">**ReadDeviceToCloudMessages** görüntüler cihaz uygulamanız tarafından gönderilen kritik olmayan telemetri hello.</span><span class="sxs-lookup"><span data-stu-id="5388e-112">**ReadDeviceToCloudMessages** that displays hello non-critical telemetry sent by your device app.</span></span>
* <span data-ttu-id="5388e-113">**ReadCriticalQueue** Service Bus kuyruğundaki iletileri cihaz uygulamanız tarafından gönderilen Merhaba kritik iletileri çıkarır.</span><span class="sxs-lookup"><span data-stu-id="5388e-113">**ReadCriticalQueue** de-queues hello critical messages sent by your device app from a Service Bus queue.</span></span> <span data-ttu-id="5388e-114">Bu sıra ekli toohello IOT hub ' dir.</span><span class="sxs-lookup"><span data-stu-id="5388e-114">This queue is attached toohello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="5388e-115">IOT hub'ı birçok cihaz platformları ve C, Java ve JavaScript gibi diller için SDK desteğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="5388e-115">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="5388e-116">toolearn Bu öğreticide bir fiziksel cihaz ile sanal cihaz tooreplace hello nasıl hello bkz [Azure IOT Geliştirme Merkezi].</span><span class="sxs-lookup"><span data-stu-id="5388e-116">toolearn how tooreplace hello simulated device in this tutorial with a physical device, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="5388e-117">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="5388e-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="5388e-118">Visual Studio 2015 veya Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="5388e-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="5388e-119">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="5388e-119">An active Azure account.</span></span> <br/><span data-ttu-id="5388e-120">Bir hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="5388e-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="5388e-121">Bazı temel bilgiye sahip [Azure Storage] ve [Azure Service Bus].</span><span class="sxs-lookup"><span data-stu-id="5388e-121">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages"></a><span data-ttu-id="5388e-122">Etkileşimli iletileri gönder</span><span class="sxs-lookup"><span data-stu-id="5388e-122">Send interactive messages</span></span>

<span data-ttu-id="5388e-123">Hello oluşturduğunuz hello cihaz uygulamayı değiştirmek [IOT Hub ile çalışmaya başlama] öğretici toooccasionally etkileşimli ileti gönderme.</span><span class="sxs-lookup"><span data-stu-id="5388e-123">Modify hello device app you created in hello [Get started with IoT Hub] tutorial toooccasionally send interactive messages.</span></span>

<span data-ttu-id="5388e-124">Visual Studio'da, hello **SimulatedDevice** proje, hello yerine `SendDeviceToCloudMessagesAsync` koddan hello yöntemiyle:</span><span class="sxs-lookup"><span data-stu-id="5388e-124">In Visual Studio, in hello **SimulatedDevice** project, replace hello `SendDeviceToCloudMessagesAsync` method with hello following code:</span></span>

```csharp
private static async void SendDeviceToCloudMessagesAsync()
{
    double minTemperature = 20;
    double minHumidity = 60;
    Random rand = new Random();

    while (true)
    {
        double currentTemperature = minTemperature + rand.NextDouble() * 15;
        double currentHumidity = minHumidity + rand.NextDouble() * 20;

        var telemetryDataPoint = new
        {
            deviceId = "myFirstDevice",
            temperature = currentTemperature,
            humidity = currentHumidity
        };
        var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
        string levelValue;

        if (rand.NextDouble() > 0.7)
        {
            messageString = "This is a critical message";
            levelValue = "critical";
        }
        else
        {
            levelValue = "normal";
        }
        
        var message = new Message(Encoding.ASCII.GetBytes(messageString));
        message.Properties.Add("level", levelValue);
        
        await deviceClient.SendEventAsync(message);
        Console.WriteLine("{0} > Sent message: {1}", DateTime.Now, messageString);

        await Task.Delay(1000);
    }
}
```

<span data-ttu-id="5388e-125">Bu yöntem rastgele hello özelliği ekler `"level": "critical"` hello çözüm arka uç tarafından Acil eylem gerektiren bir ileti taklit eden bir hello aygıt tarafından gönderilen toomessages.</span><span class="sxs-lookup"><span data-stu-id="5388e-125">This method randomly adds hello property `"level": "critical"` toomessages sent by hello device, which simulates a message that requires immediate action by hello solution back-end.</span></span> <span data-ttu-id="5388e-126">Bu IOT hub'ın hello ileti toohello uygun mesajı hedef yönlendirebilir şekilde hello cihaz uygulaması bu bilgileri hello ileti özelliklerinde yerine hello ileti gövdesinde geçirir.</span><span class="sxs-lookup"><span data-stu-id="5388e-126">hello device app passes this information in hello message properties, instead of in hello message body, so that IoT Hub can route hello message toohello proper message destination.</span></span>

> [!NOTE]
> <span data-ttu-id="5388e-127">Özellikler tooroute ileti işleme, ayrıca burada gösterilen toohello hot yolu örnek soğuk yolu da dahil olmak üzere çeşitli senaryolar için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5388e-127">You can use message properties tooroute messages for various scenarios including cold-path processing, in addition toohello hot-path example shown here.</span></span>

> [!NOTE]
> <span data-ttu-id="5388e-128">Basitlik Hello artırmak amacıyla için bu öğreticiyi herhangi bir yeniden deneme ilkesi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="5388e-128">For hello sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="5388e-129">Üretim kodunda hello MSDN makalesinde önerilen üstel geri alma gibi bir yeniden deneme ilkesi uygulamalıdır [geçici hata işleme].</span><span class="sxs-lookup"><span data-stu-id="5388e-129">In production code, you should implement a retry policy such as exponential backoff, as suggested in hello MSDN article [Transient Fault Handling].</span></span>

## <a name="route-messages-tooa-queue-in-your-iot-hub"></a><span data-ttu-id="5388e-130">IOT hub'ınızdaki rota iletileri tooa sırası</span><span class="sxs-lookup"><span data-stu-id="5388e-130">Route messages tooa queue in your IoT hub</span></span>

<span data-ttu-id="5388e-131">Bu bölümde şunları yapacaksınız:</span><span class="sxs-lookup"><span data-stu-id="5388e-131">In this section, you:</span></span>

* <span data-ttu-id="5388e-132">Service Bus kuyruğuna oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5388e-132">Create a Service Bus queue.</span></span>
* <span data-ttu-id="5388e-133">Tooyour IOT hub bağlayın.</span><span class="sxs-lookup"><span data-stu-id="5388e-133">Connect it tooyour IoT hub.</span></span>
* <span data-ttu-id="5388e-134">Bir özellik selamlama iletisine hello varlığını temel IOT hub toosend iletileri toohello sıranız yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5388e-134">Configure your IoT hub toosend messages toohello queue based on hello presence of a property on hello message.</span></span>

<span data-ttu-id="5388e-135">Service Bus sıralarından tooprocess nasıl iletileri hakkında daha fazla bilgi için bkz: [kuyruklarla çalışmaya başlama][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="5388e-135">For more information about how tooprocess messages from Service Bus queues, see [Get started with queues][Service Bus queue].</span></span>

1. <span data-ttu-id="5388e-136">Service Bus kuyruğuna açıklandığı gibi oluşturmak [kuyruklarla çalışmaya başlama][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="5388e-136">Create a Service Bus queue as described in [Get started with queues][Service Bus queue].</span></span> <span data-ttu-id="5388e-137">Merhaba sıra hello olmalıdır aynı abonelikte ve bölgede IOT hub'ınızı.</span><span class="sxs-lookup"><span data-stu-id="5388e-137">hello queue must be in hello same subscription and region as your IoT hub.</span></span> <span data-ttu-id="5388e-138">Merhaba ad alanı ve sıra adını not edin.</span><span class="sxs-lookup"><span data-stu-id="5388e-138">Make a note of hello namespace and queue name.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5388e-139">Service Bus kuyrukları ve konularından IOT Hub uç noktaları değil olarak kullanılan **oturumları** veya **yinelenen saptama** etkin.</span><span class="sxs-lookup"><span data-stu-id="5388e-139">Service Bus queues and topics used as IoT Hub endpoints must not have **Sessions** or **Duplicate Detection** enabled.</span></span> <span data-ttu-id="5388e-140">Bu seçeneklerden birini etkinleştirilirse hello uç noktası olarak görünür **ulaşılamıyor** hello Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="5388e-140">If either of those options are enabled, hello endpoint appears as **Unreachable** in hello Azure portal.</span></span>

2. <span data-ttu-id="5388e-141">Azure portal Merhaba, IOT hub'ınızı açın ve'ı tıklatın **uç noktaları**.</span><span class="sxs-lookup"><span data-stu-id="5388e-141">In hello Azure portal, open your IoT hub and click **Endpoints**.</span></span>
    
    ![IOT hub uç noktaları][30]

3. <span data-ttu-id="5388e-143">Merhaba, **uç noktaları** dikey penceresinde tıklatın **Ekle** en üst tooadd sıra tooyour IOT hub'ınızı hello.</span><span class="sxs-lookup"><span data-stu-id="5388e-143">In hello **Endpoints** blade, click **Add** at hello top tooadd your queue tooyour IoT hub.</span></span> <span data-ttu-id="5388e-144">Ad hello endpoint **CriticalQueue** ve hello aşağı açılan listeler tooselect kullanmak **Service Bus kuyruğuna**, hizmet veri yolu ad alanı, sıra içinde bulunduğu hello ve Merhaba, kuyruk adı.</span><span class="sxs-lookup"><span data-stu-id="5388e-144">Name hello endpoint **CriticalQueue** and use hello drop-downs tooselect **Service Bus queue**, hello Service Bus namespace in which your queue resides, and hello name of your queue.</span></span> <span data-ttu-id="5388e-145">İşiniz bittiğinde tıklatın **kaydetmek** hello altındaki.</span><span class="sxs-lookup"><span data-stu-id="5388e-145">When you are done, click **Save** at hello bottom.</span></span>
    
    ![Bir uç nokta ekleme][31]
    
4. <span data-ttu-id="5388e-147">Şimdi **yollar** IOT hub'ınızdaki.</span><span class="sxs-lookup"><span data-stu-id="5388e-147">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="5388e-148">Tıklatın **Ekle** hello üstünde hello dikey toocreate toohello sıra, yalnızca iletileri yönlendiren bir yönlendirme kuralı eklendi.</span><span class="sxs-lookup"><span data-stu-id="5388e-148">Click **Add** at hello top of hello blade toocreate a routing rule that routes messages toohello queue you just added.</span></span> <span data-ttu-id="5388e-149">Seçin **DeviceTelemetry** hello veri kaynağı olarak.</span><span class="sxs-lookup"><span data-stu-id="5388e-149">Select **DeviceTelemetry** as hello source of data.</span></span> <span data-ttu-id="5388e-150">Girin `level="critical"` hello koşulu olarak ve hello sıra yeni eklenen kural endpoint yönlendirme hello olarak özel bir uç noktası olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="5388e-150">Enter `level="critical"` as hello condition, and choose hello queue you just added as a custom endpoint as hello routing rule endpoint.</span></span> <span data-ttu-id="5388e-151">İşiniz bittiğinde tıklatın **kaydetmek** hello altındaki.</span><span class="sxs-lookup"><span data-stu-id="5388e-151">When you are done, click **Save** at hello bottom.</span></span>
    
    ![Bir yol ekleme][32]
    
    <span data-ttu-id="5388e-153">Merhaba geri dönüş rota çok ayarlandığından emin olun**ON**.</span><span class="sxs-lookup"><span data-stu-id="5388e-153">Make sure hello fallback route is set too**ON**.</span></span> <span data-ttu-id="5388e-154">Bu değer hello için varsayılan bir IOT hub yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="5388e-154">This value is hello default configuration for an IoT hub.</span></span>
    
    ![Geri dönüş yolu][33]

## <a name="read-from-hello-queue-endpoint"></a><span data-ttu-id="5388e-156">Merhaba sıra uç noktasından okumak</span><span class="sxs-lookup"><span data-stu-id="5388e-156">Read from hello queue endpoint</span></span>

<span data-ttu-id="5388e-157">Bu bölümde, hello sıra uç noktasından Merhaba iletileri okuyun.</span><span class="sxs-lookup"><span data-stu-id="5388e-157">In this section, you read hello messages from hello queue endpoint.</span></span>

1. <span data-ttu-id="5388e-158">Visual Studio'da bir Visual C# Windows Klasik Masaüstü projesi toohello geçerli çözüme, hello kullanarak ekleyin **konsol uygulaması (.NET Framework)** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="5388e-158">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="5388e-159">Ad hello proje **ReadCriticalQueue**.</span><span class="sxs-lookup"><span data-stu-id="5388e-159">Name hello project **ReadCriticalQueue**.</span></span>

2. <span data-ttu-id="5388e-160">Çözüm Gezgini'nde hello sağ **ReadCriticalQueue** proje ve ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="5388e-160">In Solution Explorer, right-click hello **ReadCriticalQueue** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="5388e-161">Bu işlem hello görüntüler **NuGet Paket Yöneticisi** penceresi.</span><span class="sxs-lookup"><span data-stu-id="5388e-161">This operation displays hello **NuGet Package Manager** window.</span></span>

3. <span data-ttu-id="5388e-162">Arama **WindowsAzure.ServiceBus**, tıklatın **yüklemek**ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="5388e-162">Search for **WindowsAzure.ServiceBus**, click **Install**, and accept hello terms of use.</span></span> <span data-ttu-id="5388e-163">Bu işlem indirir, yükler ve başvuru toohello Azure Service Bus, tüm bağımlılıklarıyla birlikte ekler.</span><span class="sxs-lookup"><span data-stu-id="5388e-163">This operation downloads, installs, and adds a reference toohello Azure Service Bus, with all its dependencies.</span></span>

4. <span data-ttu-id="5388e-164">Merhaba aşağıdakileri ekleyin **kullanarak** deyimleri hello hello üstündeki **Program.cs** dosyası:</span><span class="sxs-lookup"><span data-stu-id="5388e-164">Add hello following **using** statements at hello top of hello **Program.cs** file:</span></span>
   
    ```csharp
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. <span data-ttu-id="5388e-165">Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="5388e-165">Finally, add hello following lines toohello **Main** method.</span></span> <span data-ttu-id="5388e-166">Yedek hello bağlantı dizesiyle **dinleme** hello sırası izinlerini:</span><span class="sxs-lookup"><span data-stu-id="5388e-166">Substitute hello connection string with **Listen** permissions for hello queue:</span></span>
   
    ```csharp
    Console.WriteLine("Receive critical messages. Ctrl-C tooexit.\n");
    var connectionString = "{service bus listen string}";
    var queueName = "{queue name}";
    
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);

    client.OnMessage(message =>
        {
            Stream stream = message.GetBody<Stream>();
            StreamReader reader = new StreamReader(stream, Encoding.ASCII);
            string s = reader.ReadToEnd();
            Console.WriteLine(String.Format("Message body: {0}", s));
        });
        
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="5388e-167">Merhaba uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5388e-167">Run hello applications</span></span>
<span data-ttu-id="5388e-168">Hazır toorun hello uygulamaları sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="5388e-168">Now you are ready toorun hello applications.</span></span>

1. <span data-ttu-id="5388e-169">Visual Studio'da, Çözüm Gezgini'nde Çözümünüze sağ tıklayın ve seçin **başlangıç projelerini Ayarla**.</span><span class="sxs-lookup"><span data-stu-id="5388e-169">In Visual Studio, in Solution Explorer, right-click your solution and select **Set StartUp Projects**.</span></span> <span data-ttu-id="5388e-170">Seçin **birden fazla başlangıç projesi**seçeneğini belirleyip **Başlat** hello hello eylem olarak **ReadDeviceToCloudMessages**, **SimulatedDevice**, ve **ReadCriticalQueue** projeleri.</span><span class="sxs-lookup"><span data-stu-id="5388e-170">Select **Multiple startup projects**, then select **Start** as hello action for hello **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **ReadCriticalQueue** projects.</span></span>
2. <span data-ttu-id="5388e-171">Tuşuna **F5** toostart hello üç konsol uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="5388e-171">Press **F5** toostart hello three console apps.</span></span> <span data-ttu-id="5388e-172">Merhaba **ReadDeviceToCloudMessages** uygulama sahip yalnızca hello gönderilen kritik olmayan iletiler **SimulatedDevice** uygulama ve hello **ReadCriticalQueue** uygulama sahip yalnızca Kritik iletileri.</span><span class="sxs-lookup"><span data-stu-id="5388e-172">hello **ReadDeviceToCloudMessages** app has only non-critical messages sent from hello **SimulatedDevice** application, and hello **ReadCriticalQueue** app has only critical messages.</span></span>
   
   ![Üç konsol uygulamaları][50]

## <a name="next-steps"></a><span data-ttu-id="5388e-174">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5388e-174">Next steps</span></span>
<span data-ttu-id="5388e-175">Bu öğreticide, nasıl tooreliably gönderme cihaz bulut iletilerini IOT Hub'ının hello ileti yönlendirme işlevini kullanarak öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="5388e-175">In this tutorial, you learned how tooreliably dispatch device-to-cloud messages by using hello message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="5388e-176">Merhaba [toosend bulut-cihaz IOT Hub ile nasıl iletileri] [ lnk-c2d] nasıl toosend çözüm arka ucunuz tooyour aygıtlardan iletileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="5388e-176">hello [How toosend cloud-to-device messages with IoT Hub][lnk-c2d] shows you how toosend messages tooyour devices from your solution back end.</span></span>

<span data-ttu-id="5388e-177">IOT hub'ı kullanan tam uçtan uca çözümler toosee örnekleri bkz [Azure IOT paketi][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="5388e-177">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="5388e-178">IOT Hub ile çözümleri geliştirme hakkında daha fazla toolearn bkz hello [IOT Hub Geliştirici Kılavuzu].</span><span class="sxs-lookup"><span data-stu-id="5388e-178">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<span data-ttu-id="5388e-179">IOT Hub içinde ileti yönlendirme hakkında daha fazla toolearn bkz [IOT Hub ile iletileri almasına ve göndermesine][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="5388e-179">toolearn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
[50]: ./media/iot-hub-csharp-csharp-process-d2c/run1.png
[30]: ./media/iot-hub-csharp-csharp-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-csharp-csharp-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-csharp-csharp-process-d2c/route-creation.png
[33]: ./media/iot-hub-csharp-csharp-process-d2c/fallback-route.png

<!-- Links -->
[Service Bus queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/
[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/
[IOT Hub Geliştirici Kılavuzu]: iot-hub-devguide.md
[IOT Hub ile çalışmaya başlama]: iot-hub-csharp-csharp-getstarted.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[Azure IOT Geliştirme Merkezi]: https://azure.microsoft.com/develop/iot
[geçici hata işleme]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-c2d]: iot-hub-csharp-csharp-process-d2c.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
