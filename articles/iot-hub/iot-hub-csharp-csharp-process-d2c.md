---
title: "Azure IOT Hub cihaz-bulut iletileri yolları (.Net) kullanma | Microsoft Docs"
description: "Diğer arka uç hizmetlerine iletilerinin gönderilmesi için yönlendirme kurallarını ve özel uç noktaları kullanarak IOT Hub cihaz bulut iletilerini işlemek nasıl."
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
ms.openlocfilehash: 1d2b52ea005ab520bf294efa603512c00a92ee63
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a><span data-ttu-id="736aa-103">Yollar (.NET) kullanılarak IOT Hub cihaz bulut iletilerini işleme</span><span class="sxs-lookup"><span data-stu-id="736aa-103">Process IoT Hub device-to-cloud messages using routes (.NET)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="736aa-104">Bu öğretici derlemeler [IOT Hub ile çalışmaya başlama] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="736aa-104">This tutorial builds on the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="736aa-105">Öğretici:</span><span class="sxs-lookup"><span data-stu-id="736aa-105">The tutorial:</span></span>

* <span data-ttu-id="736aa-106">Cihaz bulut iletilerini kolay, yapılandırma tabanlı bir şekilde gönderilmesi için yönlendirme kurallarını kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="736aa-106">Shows you how to use routing rules to dispatch device-to-cloud messages in an easy, configuration-based way.</span></span>
* <span data-ttu-id="736aa-107">Daha ayrıntılı işleme için çözüm arka uçtan Acil eylem gerekli etkileşimli iletilerin yalıtmak nasıl gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="736aa-107">Illustrates how to isolate interactive messages that require immediate action from the solution back end for further processing.</span></span> <span data-ttu-id="736aa-108">Örneğin, bir aygıt bir bilet bir CRM sistemine ekleme tetikleyen bir uyarı iletisi gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="736aa-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="736aa-109">Buna karşılık, sıcaklık telemetri gibi veri noktası iletileri analytics motoruna akış.</span><span class="sxs-lookup"><span data-stu-id="736aa-109">In contrast, data-point messages, such as temperature telemetry, feed into an analytics engine.</span></span>

<span data-ttu-id="736aa-110">Bu öğreticinin sonunda üç .NET konsol uygulamaları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="736aa-110">At the end of this tutorial, you run three .NET console apps:</span></span>

* <span data-ttu-id="736aa-111">**SimulatedDevice**, oluşturduğunuz uygulama değiştirilmiş bir sürümünü [IOT Hub ile çalışmaya başlama] öğretici saniyede veri noktası cihaz bulut iletilerini gönderir ve etkileşimli cihaz bulut iletilerini her 10 saniye.</span><span class="sxs-lookup"><span data-stu-id="736aa-111">**SimulatedDevice**, a modified version of the app created in the [Get started with IoT Hub] tutorial sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span>
* <span data-ttu-id="736aa-112">**ReadDeviceToCloudMessages** cihaz uygulamanız tarafından gönderilen kritik olmayan telemetriyi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="736aa-112">**ReadDeviceToCloudMessages** that displays the non-critical telemetry sent by your device app.</span></span>
* <span data-ttu-id="736aa-113">**ReadCriticalQueue** Service Bus kuyruğundaki iletileri cihaz uygulamanız tarafından gönderilen kritik iletileri çıkarır.</span><span class="sxs-lookup"><span data-stu-id="736aa-113">**ReadCriticalQueue** de-queues the critical messages sent by your device app from a Service Bus queue.</span></span> <span data-ttu-id="736aa-114">Bu sıra IOT hub'ına bağlı.</span><span class="sxs-lookup"><span data-stu-id="736aa-114">This queue is attached to the IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="736aa-115">IOT hub'ı birçok cihaz platformları ve C, Java ve JavaScript gibi diller için SDK desteğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="736aa-115">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="736aa-116">Sanal cihaz Bu öğreticide bir fiziksel aygıt ile değiştirmek öğrenmek için bkz: [Azure IOT Geliştirme Merkezi].</span><span class="sxs-lookup"><span data-stu-id="736aa-116">To learn how to replace the simulated device in this tutorial with a physical device, see the [Azure IoT Developer Center].</span></span>

<span data-ttu-id="736aa-117">Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="736aa-117">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="736aa-118">Visual Studio 2015 veya Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="736aa-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="736aa-119">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="736aa-119">An active Azure account.</span></span> <br/><span data-ttu-id="736aa-120">Bir hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="736aa-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="736aa-121">Bazı temel bilgiye sahip [Azure Storage] ve [Azure Service Bus].</span><span class="sxs-lookup"><span data-stu-id="736aa-121">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages"></a><span data-ttu-id="736aa-122">Etkileşimli iletileri gönder</span><span class="sxs-lookup"><span data-stu-id="736aa-122">Send interactive messages</span></span>

<span data-ttu-id="736aa-123">Oluşturduğunuz cihaz uygulamayı değiştirmek [IOT Hub ile çalışmaya başlama] bazen etkileşimli iletileri göndermek için öğretici.</span><span class="sxs-lookup"><span data-stu-id="736aa-123">Modify the device app you created in the [Get started with IoT Hub] tutorial to occasionally send interactive messages.</span></span>

<span data-ttu-id="736aa-124">Visual Studio içinde **SimulatedDevice** proje, yerine `SendDeviceToCloudMessagesAsync` aşağıdaki kod ile yöntemi:</span><span class="sxs-lookup"><span data-stu-id="736aa-124">In Visual Studio, in the **SimulatedDevice** project, replace the `SendDeviceToCloudMessagesAsync` method with the following code:</span></span>

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

<span data-ttu-id="736aa-125">Bu yöntem rastgele özelliği ekler `"level": "critical"` aygıt tarafından gönderilen iletiler için hangi benzetim çözüm arka ucu tarafından Acil eylem gerektiren bir ileti.</span><span class="sxs-lookup"><span data-stu-id="736aa-125">This method randomly adds the property `"level": "critical"` to messages sent by the device, which simulates a message that requires immediate action by the solution back-end.</span></span> <span data-ttu-id="736aa-126">Bu IOT hub'ın uygun mesajı hedefe ileti yönlendirmek için cihaz uygulaması bu bilgileri ileti özelliklerinde yerine ileti gövdesinde geçirir.</span><span class="sxs-lookup"><span data-stu-id="736aa-126">The device app passes this information in the message properties, instead of in the message body, so that IoT Hub can route the message to the proper message destination.</span></span>

> [!NOTE]
> <span data-ttu-id="736aa-127">Burada gösterilen hot yolu örnek yanı sıra soğuk yolu işleme dahil olmak üzere çeşitli senaryoları için ileti özellikleri iletileri yönlendirmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="736aa-127">You can use message properties to route messages for various scenarios including cold-path processing, in addition to the hot-path example shown here.</span></span>

> [!NOTE]
> <span data-ttu-id="736aa-128">Basitleştirmek amacıyla, Bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="736aa-128">For the sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="736aa-129">Üretim kodunda MSDN makalesinde önerilen üstel geri alma gibi bir yeniden deneme ilkesi uygulamalıdır [geçici hata işleme].</span><span class="sxs-lookup"><span data-stu-id="736aa-129">In production code, you should implement a retry policy such as exponential backoff, as suggested in the MSDN article [Transient Fault Handling].</span></span>

## <a name="route-messages-to-a-queue-in-your-iot-hub"></a><span data-ttu-id="736aa-130">IOT hub'ınızdaki kuyruğuna iletileri yönlendirmek</span><span class="sxs-lookup"><span data-stu-id="736aa-130">Route messages to a queue in your IoT hub</span></span>

<span data-ttu-id="736aa-131">Bu bölümde şunları yapacaksınız:</span><span class="sxs-lookup"><span data-stu-id="736aa-131">In this section, you:</span></span>

* <span data-ttu-id="736aa-132">Service Bus kuyruğuna oluşturun.</span><span class="sxs-lookup"><span data-stu-id="736aa-132">Create a Service Bus queue.</span></span>
* <span data-ttu-id="736aa-133">IOT hub'ınıza bağlanın.</span><span class="sxs-lookup"><span data-stu-id="736aa-133">Connect it to your IoT hub.</span></span>
* <span data-ttu-id="736aa-134">İleti bir özellik varlığına dayalı kuyruğa ileti göndermek için IOT hub'ınızı yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="736aa-134">Configure your IoT hub to send messages to the queue based on the presence of a property on the message.</span></span>

<span data-ttu-id="736aa-135">Hizmet veri yolu sıralardan işlem iletileri hakkında daha fazla bilgi için bkz: [kuyruklarla çalışmaya başlama][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="736aa-135">For more information about how to process messages from Service Bus queues, see [Get started with queues][Service Bus queue].</span></span>

1. <span data-ttu-id="736aa-136">Service Bus kuyruğuna açıklandığı gibi oluşturmak [kuyruklarla çalışmaya başlama][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="736aa-136">Create a Service Bus queue as described in [Get started with queues][Service Bus queue].</span></span> <span data-ttu-id="736aa-137">Sıranın IOT hub'ınızı aynı abonelikte ve bölgede olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="736aa-137">The queue must be in the same subscription and region as your IoT hub.</span></span> <span data-ttu-id="736aa-138">Ad alanı ve sıra adını not edin.</span><span class="sxs-lookup"><span data-stu-id="736aa-138">Make a note of the namespace and queue name.</span></span>

    > [!NOTE]
    > <span data-ttu-id="736aa-139">Service Bus kuyrukları ve konularından IOT Hub uç noktaları değil olarak kullanılan **oturumları** veya **yinelenen saptama** etkin.</span><span class="sxs-lookup"><span data-stu-id="736aa-139">Service Bus queues and topics used as IoT Hub endpoints must not have **Sessions** or **Duplicate Detection** enabled.</span></span> <span data-ttu-id="736aa-140">Bu seçeneklerden birini etkinleştirilmişse, uç nokta olarak görünür **ulaşılamıyor** Azure portalında.</span><span class="sxs-lookup"><span data-stu-id="736aa-140">If either of those options are enabled, the endpoint appears as **Unreachable** in the Azure portal.</span></span>

2. <span data-ttu-id="736aa-141">Azure portalında, IOT hub'ınızı açın ve **uç noktaları**.</span><span class="sxs-lookup"><span data-stu-id="736aa-141">In the Azure portal, open your IoT hub and click **Endpoints**.</span></span>
    
    ![IOT hub uç noktaları][30]

3. <span data-ttu-id="736aa-143">İçinde **uç noktaları** dikey penceresinde tıklatın **Ekle** sıranız IOT hub'ınıza eklemek için üst.</span><span class="sxs-lookup"><span data-stu-id="736aa-143">In the **Endpoints** blade, click **Add** at the top to add your queue to your IoT hub.</span></span> <span data-ttu-id="736aa-144">Uç nokta adı **CriticalQueue** ve seçmek için açılır listeleri kullanın **Service Bus kuyruğuna**, sıranız bulunduğu hizmet veri yolu ad alanı ve sıranız adı.</span><span class="sxs-lookup"><span data-stu-id="736aa-144">Name the endpoint **CriticalQueue** and use the drop-downs to select **Service Bus queue**, the Service Bus namespace in which your queue resides, and the name of your queue.</span></span> <span data-ttu-id="736aa-145">İşiniz bittiğinde tıklatın **kaydetmek** altındaki.</span><span class="sxs-lookup"><span data-stu-id="736aa-145">When you are done, click **Save** at the bottom.</span></span>
    
    ![Bir uç nokta ekleme][31]
    
4. <span data-ttu-id="736aa-147">Şimdi **yollar** IOT hub'ınızdaki.</span><span class="sxs-lookup"><span data-stu-id="736aa-147">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="736aa-148">Tıklatın **Ekle** iletileri kuyruğa yönlendiren bir yönlendirme kuralı oluşturmak için dikey pencerenin üstündeki eklediğiniz.</span><span class="sxs-lookup"><span data-stu-id="736aa-148">Click **Add** at the top of the blade to create a routing rule that routes messages to the queue you just added.</span></span> <span data-ttu-id="736aa-149">Seçin **DeviceTelemetry** veri kaynağı olarak.</span><span class="sxs-lookup"><span data-stu-id="736aa-149">Select **DeviceTelemetry** as the source of data.</span></span> <span data-ttu-id="736aa-150">Girin `level="critical"` koşulu olarak ve yeni eklediğiniz yönlendirme kuralı uç noktası olarak özel bir uç noktası olarak sıra'yı seçin.</span><span class="sxs-lookup"><span data-stu-id="736aa-150">Enter `level="critical"` as the condition, and choose the queue you just added as a custom endpoint as the routing rule endpoint.</span></span> <span data-ttu-id="736aa-151">İşiniz bittiğinde tıklatın **kaydetmek** altındaki.</span><span class="sxs-lookup"><span data-stu-id="736aa-151">When you are done, click **Save** at the bottom.</span></span>
    
    ![Bir yol ekleme][32]
    
    <span data-ttu-id="736aa-153">Emin olun geri dönüş rota ayarlanmış **ON**.</span><span class="sxs-lookup"><span data-stu-id="736aa-153">Make sure the fallback route is set to **ON**.</span></span> <span data-ttu-id="736aa-154">Bu değer, bir IOT hub'ın varsayılan yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="736aa-154">This value is the default configuration for an IoT hub.</span></span>
    
    ![Geri dönüş yolu][33]

## <a name="read-from-the-queue-endpoint"></a><span data-ttu-id="736aa-156">Sıra uç noktasından okumak</span><span class="sxs-lookup"><span data-stu-id="736aa-156">Read from the queue endpoint</span></span>

<span data-ttu-id="736aa-157">Bu bölümde, sıra uç noktasından iletilerini okuyun.</span><span class="sxs-lookup"><span data-stu-id="736aa-157">In this section, you read the messages from the queue endpoint.</span></span>

1. <span data-ttu-id="736aa-158">Visual Studio’da **Konsol Uygulaması (.NET Framework)** proje şablonunu kullanarak geçerli çözüme bir Visual C# Windows Klasik Masaüstü projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="736aa-158">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="736aa-159">Proje adı **ReadCriticalQueue**.</span><span class="sxs-lookup"><span data-stu-id="736aa-159">Name the project **ReadCriticalQueue**.</span></span>

2. <span data-ttu-id="736aa-160">Çözüm Gezgini'nde sağ **ReadCriticalQueue** proje ve ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="736aa-160">In Solution Explorer, right-click the **ReadCriticalQueue** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="736aa-161">Bu işlem görüntüler **NuGet Paket Yöneticisi** penceresi.</span><span class="sxs-lookup"><span data-stu-id="736aa-161">This operation displays the **NuGet Package Manager** window.</span></span>

3. <span data-ttu-id="736aa-162">Arama **WindowsAzure.ServiceBus**, tıklatın **yükleme**ve kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="736aa-162">Search for **WindowsAzure.ServiceBus**, click **Install**, and accept the terms of use.</span></span> <span data-ttu-id="736aa-163">Bu işlem indirir, yükler ve Azure hizmet veri yolu, tüm bağımlılıklarıyla birlikte bir başvuru eklenir.</span><span class="sxs-lookup"><span data-stu-id="736aa-163">This operation downloads, installs, and adds a reference to the Azure Service Bus, with all its dependencies.</span></span>

4. <span data-ttu-id="736aa-164">Aşağıdakileri ekleyin **kullanarak** deyimleri en üstündeki **Program.cs** dosyası:</span><span class="sxs-lookup"><span data-stu-id="736aa-164">Add the following **using** statements at the top of the **Program.cs** file:</span></span>
   
    ```csharp
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. <span data-ttu-id="736aa-165">Son olarak aşağıdaki satırları ekleyin **ana** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="736aa-165">Finally, add the following lines to the **Main** method.</span></span> <span data-ttu-id="736aa-166">Bağlantı dizesi ile değiştirin **dinleme** sıra için izinleri:</span><span class="sxs-lookup"><span data-stu-id="736aa-166">Substitute the connection string with **Listen** permissions for the queue:</span></span>
   
    ```csharp
    Console.WriteLine("Receive critical messages. Ctrl-C to exit.\n");
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

## <a name="run-the-applications"></a><span data-ttu-id="736aa-167">Uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="736aa-167">Run the applications</span></span>
<span data-ttu-id="736aa-168">Şimdi uygulamaları çalıştırmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="736aa-168">Now you are ready to run the applications.</span></span>

1. <span data-ttu-id="736aa-169">Visual Studio'da, Çözüm Gezgini'nde Çözümünüze sağ tıklayın ve seçin **başlangıç projelerini Ayarla**.</span><span class="sxs-lookup"><span data-stu-id="736aa-169">In Visual Studio, in Solution Explorer, right-click your solution and select **Set StartUp Projects**.</span></span> <span data-ttu-id="736aa-170">Seçin **birden fazla başlangıç projesi**seçeneğini belirleyip **Başlat** için eylem olarak **ReadDeviceToCloudMessages**, **SimulatedDevice**, ve **ReadCriticalQueue** projeleri.</span><span class="sxs-lookup"><span data-stu-id="736aa-170">Select **Multiple startup projects**, then select **Start** as the action for the **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **ReadCriticalQueue** projects.</span></span>
2. <span data-ttu-id="736aa-171">Tuşuna **F5** üç konsol uygulamaları başlatın.</span><span class="sxs-lookup"><span data-stu-id="736aa-171">Press **F5** to start the three console apps.</span></span> <span data-ttu-id="736aa-172">**ReadDeviceToCloudMessages** uygulama tarafından gönderilen yalnızca kritik olmayan iletileri sahip **SimulatedDevice** uygulama ve **ReadCriticalQueue** uygulamanın yalnızca kritik iletileri yok.</span><span class="sxs-lookup"><span data-stu-id="736aa-172">The **ReadDeviceToCloudMessages** app has only non-critical messages sent from the **SimulatedDevice** application, and the **ReadCriticalQueue** app has only critical messages.</span></span>
   
   ![Üç konsol uygulamaları][50]

## <a name="next-steps"></a><span data-ttu-id="736aa-174">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="736aa-174">Next steps</span></span>
<span data-ttu-id="736aa-175">Bu öğreticide, IOT Hub'ının ileti yönlendirme işlevini kullanarak cihaz bulut iletilerini güvenilir bir şekilde gönderme öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="736aa-175">In this tutorial, you learned how to reliably dispatch device-to-cloud messages by using the message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="736aa-176">[IOT Hub ile bulut-cihaz iletilerini göndermek nasıl] [ lnk-c2d] aygıtlarınıza çözüm arka ucu iletileri göndermek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="736aa-176">The [How to send cloud-to-device messages with IoT Hub][lnk-c2d] shows you how to send messages to your devices from your solution back end.</span></span>

<span data-ttu-id="736aa-177">IOT hub'ı kullanan tam uçtan uca çözümler örnekleri görmek için bkz: [Azure IOT paketi][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="736aa-177">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="736aa-178">IOT Hub ile çözümleri geliştirme hakkında daha fazla bilgi için bkz: [IOT Hub Geliştirici Kılavuzu].</span><span class="sxs-lookup"><span data-stu-id="736aa-178">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<span data-ttu-id="736aa-179">IOT Hub içinde ileti yönlendirme hakkında daha fazla bilgi için bkz: [IOT Hub ile iletileri almasına ve göndermesine][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="736aa-179">To learn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
[50]: ./media/iot-hub-csharp-csharp-process-d2c/run1.png
[30]: ./media/iot-hub-csharp-csharp-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-csharp-csharp-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-csharp-csharp-process-d2c/route-creation.png
[33]: ./media/iot-hub-csharp-csharp-process-d2c/fallback-route.png

<!-- Links -->
[Service Bus queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
<span data-ttu-id="736aa-180">[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/</span><span class="sxs-lookup"><span data-stu-id="736aa-180">[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/</span></span>
<span data-ttu-id="736aa-181">[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/</span><span class="sxs-lookup"><span data-stu-id="736aa-181">[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/</span></span>
<span data-ttu-id="736aa-182">[IOT Hub Geliştirici Kılavuzu]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="736aa-182">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
<span data-ttu-id="736aa-183">[IOT Hub ile çalışmaya başlama]: iot-hub-csharp-csharp-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="736aa-183">[Get started with IoT Hub]: iot-hub-csharp-csharp-getstarted.md</span></span>
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
<span data-ttu-id="736aa-184">[Azure IOT Geliştirme Merkezi]: https://azure.microsoft.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="736aa-184">[Azure IoT Developer Center]: https://azure.microsoft.com/develop/iot</span></span>
<span data-ttu-id="736aa-185">[geçici hata işleme]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="736aa-185">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
[lnk-c2d]: iot-hub-csharp-csharp-process-d2c.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
