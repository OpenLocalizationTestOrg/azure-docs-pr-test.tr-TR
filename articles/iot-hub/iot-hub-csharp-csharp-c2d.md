---
title: "aaaCloud aygıt iletileri ile Azure IOT hub'ı (.NET) | Microsoft Docs"
description: "Nasıl toosend bulut-cihaz hello Azure IOT SDK'ları için .NET kullanarak Azure IOT hub'ı tooa aygıttan iletileri. Bir aygıt uygulama tooreceive bulut-cihaz iletilerini değiştirmek ve bir arka uç uygulaması toosend hello bulut-cihaz iletilerini değiştirin."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: a31c05ed-6ec0-40f3-99ab-8fdd28b1a89a
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: f6a7618b164d95c8ddaf28943f244aeeb568217f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="send-messages-from-hello-cloud-tooyour-device-with-iot-hub-net"></a><span data-ttu-id="4a704-104">İletileri hello bulut tooyour cihaz IOT hub'ı (.NET) ile gönderin.</span><span class="sxs-lookup"><span data-stu-id="4a704-104">Send messages from hello cloud tooyour device with IoT Hub (.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="4a704-105">Giriş</span><span class="sxs-lookup"><span data-stu-id="4a704-105">Introduction</span></span>
<span data-ttu-id="4a704-106">Azure IOT Hub, milyonlarca cihaza arasında güvenilir ve güvenli çift yönlü iletişimler sağlayan tam olarak yönetilen hizmet etkinleştirin ve bir çözüm arka ucu ' dir.</span><span class="sxs-lookup"><span data-stu-id="4a704-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="4a704-107">Merhaba [IOT Hub ile çalışmaya başlama] öğretici nasıl toocreate IOT hub'ı, bir cihaz kimliği, sağlamak ve cihaz-bulut iletileri gönderen bir aygıt uygulama kodu gösterir.</span><span class="sxs-lookup"><span data-stu-id="4a704-107">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="4a704-108">Bu öğretici derlemeler [IOT Hub ile çalışmaya başlama].</span><span class="sxs-lookup"><span data-stu-id="4a704-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="4a704-109">Size bir nasıl gösterir için:</span><span class="sxs-lookup"><span data-stu-id="4a704-109">It shows you how to:</span></span>

* <span data-ttu-id="4a704-110">Çözüm arka ucunuz, bulut-cihaz iletilerini tooa tek cihaz IOT hub'ı aracılığıyla gönderin.</span><span class="sxs-lookup"><span data-stu-id="4a704-110">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="4a704-111">Bir cihazda bulut-cihaz iletilerini alır.</span><span class="sxs-lookup"><span data-stu-id="4a704-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="4a704-112">Çözüm arka ucunuz, teslimat alındısı iste (*geri bildirim*) tooa cihaz IOT Hub'ından gönderilen iletileri için.</span><span class="sxs-lookup"><span data-stu-id="4a704-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="4a704-113">Hello bulut-cihaz iletilerini hakkında daha fazla bilgi bulabilirsiniz [IOT Hub Geliştirici Kılavuzu][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="4a704-113">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="4a704-114">Bu öğreticinin Hello sonunda, iki .NET konsol uygulamaları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4a704-114">At hello end of this tutorial, you run two .NET console apps:</span></span>

* <span data-ttu-id="4a704-115">**SimulatedDevice**, oluşturulan hello uygulama değiştirilmiş bir sürümünü [IOT Hub ile çalışmaya başlama], hangi tooyour IOT hub'ı bağlar ve bulut-cihaz iletilerini alır.</span><span class="sxs-lookup"><span data-stu-id="4a704-115">**SimulatedDevice**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="4a704-116">**SendCloudToDevice**, hangi bulut aygıt iletisi toohello cihaz uygulaması IOT hub'ı üzerinden gönderir ve teslimat alındısı alır.</span><span class="sxs-lookup"><span data-stu-id="4a704-116">**SendCloudToDevice**, which sends a cloud-to-device message toohello device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="4a704-117">IOT hub'ı aracılığıyla birçok cihaz platformları ve (C, Java ve Javascript dahil) dillerin SDK desteği olan [Azure IOT cihaz SDK'ları].</span><span class="sxs-lookup"><span data-stu-id="4a704-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through [Azure IoT device SDKs].</span></span> <span data-ttu-id="4a704-118">Adım adım yönergeler nasıl tooconnect aygıt toothis öğreticinin kod ve genellikle tooAzure IOT hub'ı görmek için hello [IOT Hub Geliştirici Kılavuzu].</span><span class="sxs-lookup"><span data-stu-id="4a704-118">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [IoT Hub developer guide].</span></span>
> 
> 

<span data-ttu-id="4a704-119">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="4a704-119">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="4a704-120">Visual Studio 2015 veya Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="4a704-120">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="4a704-121">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="4a704-121">An active Azure account.</span></span> <span data-ttu-id="4a704-122">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="4a704-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-device-app"></a><span data-ttu-id="4a704-123">Merhaba aygıt uygulamada ileti alma</span><span class="sxs-lookup"><span data-stu-id="4a704-123">Receive messages in hello device app</span></span>
<span data-ttu-id="4a704-124">Bu bölümde, oluşturduğunuz hello cihaz uygulaması değiştireceksiniz [IOT Hub ile çalışmaya başlama] tooreceive bulut cihaza iletilerden hello IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="4a704-124">In this section, you'll modify hello device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="4a704-125">Visual Studio'da, hello **SimulatedDevice** projesi, yöntem toohello aşağıdaki hello eklemek **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="4a704-125">In Visual Studio, in hello **SimulatedDevice** project, add hello following method toohello **Program** class.</span></span>
   
        private static async void ReceiveC2dAsync()
        {
            Console.WriteLine("\nReceiving cloud toodevice messages from service");
            while (true)
            {
                Message receivedMessage = await deviceClient.ReceiveAsync();
                if (receivedMessage == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received message: {0}", Encoding.ASCII.GetString(receivedMessage.GetBytes()));
                Console.ResetColor();
   
                await deviceClient.CompleteAsync(receivedMessage);
            }
        }
   
    <span data-ttu-id="4a704-126">Merhaba `ReceiveAsync` yöntemi zaman uyumsuz olarak döndürür alınan selamlama iletisine hello aygıt tarafından alınan hello zaman.</span><span class="sxs-lookup"><span data-stu-id="4a704-126">hello `ReceiveAsync` method asynchronously returns hello received message at hello time that it is received by hello device.</span></span> <span data-ttu-id="4a704-127">Döndürdüğü *null* specifiable zaman aşımı süresinden sonra (Bu durumda, bir dakika hello varsayılan kullanılır).</span><span class="sxs-lookup"><span data-stu-id="4a704-127">It returns *null* after a specifiable timeout period (in this case, hello default of one minute is used).</span></span> <span data-ttu-id="4a704-128">Merhaba uygulama zaman alan bir *null*, yeni iletiler için toowait devam etmelidir.</span><span class="sxs-lookup"><span data-stu-id="4a704-128">When hello app receives a *null*, it should continue toowait for new messages.</span></span> <span data-ttu-id="4a704-129">Bu gereksinim hello hello nedeni `if (receivedMessage == null) continue` satır.</span><span class="sxs-lookup"><span data-stu-id="4a704-129">This requirement is hello reason for hello `if (receivedMessage == null) continue` line.</span></span>
   
    <span data-ttu-id="4a704-130">Çağrı çok hello`CompleteAsync()` IOT Hub, selamlama iletisine başarıyla işlendiğinden bildirir.</span><span class="sxs-lookup"><span data-stu-id="4a704-130">hello call too`CompleteAsync()` notifies IoT Hub that hello message has been successfully processed.</span></span> <span data-ttu-id="4a704-131">Merhaba ileti güvenli bir şekilde hello aygıt sıradan kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="4a704-131">hello message can be safely removed from hello device queue.</span></span> <span data-ttu-id="4a704-132">Bir şey selamlama iletisine hello işlenmesini tamamlanmasını o önlenmiş hello cihaz uygulaması oluştuysa, IOT Hub tarafından tekrar teslim edilir.</span><span class="sxs-lookup"><span data-stu-id="4a704-132">If something happened that prevented hello device app from completing hello processing of hello message, IoT Hub delivers it again.</span></span> <span data-ttu-id="4a704-133">Ardından hello cihaz uygulama mantığını işleme o iletisi önemli *ıdempotent*, aynı iletiyi birden çok kez üreten hello alma hello aynı sonucu.</span><span class="sxs-lookup"><span data-stu-id="4a704-133">It is then important that message processing logic in hello device app is *idempotent*, so that receiving hello same message multiple times produces hello same result.</span></span> <span data-ttu-id="4a704-134">Bir uygulama geçici olarak IOT hub'ı gelecekteki tüketimi için hello sırasındaki selamlama iletisine koruma sonuçları bir ileti iptal.</span><span class="sxs-lookup"><span data-stu-id="4a704-134">An application can also temporarily abandon a message, which results in IoT hub retaining hello message in hello queue for future consumption.</span></span> <span data-ttu-id="4a704-135">Veya Merhaba uygulaması kalıcı olarak selamlama iletisine hello kuyruktan kaldırır bir ileti reddedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a704-135">Or, hello application can reject a message, which permanently removes hello message from hello queue.</span></span> <span data-ttu-id="4a704-136">Merhaba hello bulut cihaz ileti yaşam döngüsü hakkında daha fazla bilgi için bkz: [IOT Hub Geliştirici Kılavuzu][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="4a704-136">For more information about hello cloud-to-device message lifecycle, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4a704-137">HTTP MQTT veya AMQP yerine bir taşıma olarak kullanırken, hello `ReceiveAsync` yöntemi hemen döndürür.</span><span class="sxs-lookup"><span data-stu-id="4a704-137">When using HTTP instead of MQTT or AMQP as a transport, hello `ReceiveAsync` method returns immediately.</span></span> <span data-ttu-id="4a704-138">desteklenen hello düzeni için HTTP ile bulut-cihaz iletilerini denetleyen aralıklı bağlı seyrek iletileri (değerinden 25 dakikada bir) cihazlar içindir.</span><span class="sxs-lookup"><span data-stu-id="4a704-138">hello supported pattern for cloud-to-device messages with HTTP is intermittently connected devices that check for messages infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="4a704-139">Daha fazla HTTP veren sonuçları IOT hub'ı azaltma hello isteklerini alır.</span><span class="sxs-lookup"><span data-stu-id="4a704-139">Issuing more HTTP receives results in IoT Hub throttling hello requests.</span></span> <span data-ttu-id="4a704-140">Merhaba hello farklarını MQTT, AMQP ve HTTP desteği ve IOT hub'ı azaltma hakkında daha fazla bilgi için bkz: [IOT Hub Geliştirici Kılavuzu][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="4a704-140">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 
2. <span data-ttu-id="4a704-141">Merhaba yönteminde aşağıdaki hello eklemek **ana** hello önceki yöntemi `Console.ReadLine()` satır:</span><span class="sxs-lookup"><span data-stu-id="4a704-141">Add hello following method in hello **Main** method, right before hello `Console.ReadLine()` line:</span></span>
   
        ReceiveC2dAsync();

> [!NOTE]
> <span data-ttu-id="4a704-142">Basitlik'ın artırmak amacıyla için bu öğreticiyi herhangi bir yeniden deneme ilkesi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="4a704-142">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="4a704-143">Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme].</span><span class="sxs-lookup"><span data-stu-id="4a704-143">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="4a704-144">Bulut cihaza ileti gönderme</span><span class="sxs-lookup"><span data-stu-id="4a704-144">Send a cloud-to-device message</span></span>
<span data-ttu-id="4a704-145">Bu bölümde, bulut-cihaz iletilerini toohello cihaz uygulaması gönderir bir .NET konsol uygulaması yazma.</span><span class="sxs-lookup"><span data-stu-id="4a704-145">In this section, you write a .NET console app that sends cloud-to-device messages toohello device app.</span></span>

1. <span data-ttu-id="4a704-146">Merhaba geçerli Visual Studio çözümünde hello kullanarak bir Visual C# masaüstü uygulaması projesi oluşturma **konsol uygulaması** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="4a704-146">In hello current Visual Studio solution, create a Visual C# Desktop App project by using hello **Console Application** project template.</span></span> <span data-ttu-id="4a704-147">Ad hello proje **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="4a704-147">Name hello project **SendCloudToDevice**.</span></span>
   
    ![Visual Studio'da yeni proje][20]
2. <span data-ttu-id="4a704-149">Çözüm Gezgini'nde, hello çözüme sağ tıklayın ve ardından **çözüm için NuGet paketlerini Yönet...** .</span><span class="sxs-lookup"><span data-stu-id="4a704-149">In Solution Explorer, right-click hello solution, and then click **Manage NuGet Packages for Solution...**.</span></span> 
   
    <span data-ttu-id="4a704-150">Bu eylemin hello açılır **NuGet paketlerini Yönet** penceresi.</span><span class="sxs-lookup"><span data-stu-id="4a704-150">This action opens hello **Manage NuGet Packages** window.</span></span>
3. <span data-ttu-id="4a704-151">Arama **Microsoft.Azure.Devices**, tıklatın **yüklemek**ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="4a704-151">Search for **Microsoft.Azure.Devices**, click **Install**, and accept hello terms of use.</span></span> 
   
    <span data-ttu-id="4a704-152">Bu indirir, yükler ve başvuru toohello ekler [Azure IOT hizmeti SDK'sı NuGet paketi].</span><span class="sxs-lookup"><span data-stu-id="4a704-152">This downloads, installs, and adds a reference toohello [Azure IoT service SDK NuGet package].</span></span>

4. <span data-ttu-id="4a704-153">Merhaba aşağıdakileri ekleyin `using` deyimi hello hello üstündeki **Program.cs** dosyası:</span><span class="sxs-lookup"><span data-stu-id="4a704-153">Add hello following `using` statement at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="4a704-154">Aşağıdaki alanları toohello hello eklemek **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="4a704-154">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="4a704-155">Yedek hello yer tutucu değerini hello IOT hub bağlantı dizesinden ile [IOT Hub ile çalışmaya başlama]:</span><span class="sxs-lookup"><span data-stu-id="4a704-155">Substitute hello placeholder value with hello IoT hub connection string from [Get started with IoT Hub]:</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="4a704-156">Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="4a704-156">Add hello following method toohello **Program** class:</span></span>
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud toodevice message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    <span data-ttu-id="4a704-157">Bu yöntem, yeni bir bulut aygıt iletisi toohello aygıt hello kimlikli gönderir `myFirstDevice`.</span><span class="sxs-lookup"><span data-stu-id="4a704-157">This method sends a new cloud-to-device message toohello device with hello ID, `myFirstDevice`.</span></span> <span data-ttu-id="4a704-158">Bu parametre yalnızca bir kullanılan hello gelen değişiklik tıklarsanız [IOT Hub ile çalışmaya başlama].</span><span class="sxs-lookup"><span data-stu-id="4a704-158">Change this parameter only if you modified it from hello one used in [Get started with IoT Hub].</span></span>
7. <span data-ttu-id="4a704-159">Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="4a704-159">Finally, add hello following lines toohello **Main** method:</span></span>
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key toosend a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="4a704-160">Visual Studio'dan Çözümünüze sağ tıklayın ve seçin **başlangıç projelerini Ayarla...** . Seçin **birden fazla başlangıç projesi**seçeneğini belirleyip hello **Başlat** eylemi için **ReadDeviceToCloudMessages**, **SimulatedDevice**, ve **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="4a704-160">From within Visual Studio, right-click your solution, and select **Set StartUp projects...**. Select **Multiple startup projects**, then select hello **Start** action for **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **SendCloudToDevice**.</span></span>
9. <span data-ttu-id="4a704-161">Tuşuna **F5**.</span><span class="sxs-lookup"><span data-stu-id="4a704-161">Press **F5**.</span></span> <span data-ttu-id="4a704-162">Üç uygulama başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4a704-162">All three applications should start.</span></span> <span data-ttu-id="4a704-163">Select hello **SendCloudToDevice** windows ve tuşuna **Enter**.</span><span class="sxs-lookup"><span data-stu-id="4a704-163">Select hello **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="4a704-164">Merhaba cihaz uygulaması tarafından alınan hello iletiyi görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4a704-164">You should see hello message being received by hello device app.</span></span>
   
   ![Uygulama alma iletisi][21]

## <a name="receive-delivery-feedback"></a><span data-ttu-id="4a704-166">Teslim geri alma</span><span class="sxs-lookup"><span data-stu-id="4a704-166">Receive delivery feedback</span></span>
<span data-ttu-id="4a704-167">Bu, olası toorequest teslim (veya sona erme) IOT hub'dan ilişkin bildirimleri her bulut cihaz ileti olur.</span><span class="sxs-lookup"><span data-stu-id="4a704-167">It is possible toorequest delivery (or expiration) acknowledgements from IoT Hub for each cloud-to-device message.</span></span> <span data-ttu-id="4a704-168">Bu seçeneği etkinleştirir hello çözüm arka ucu tooeasily Yeniden Dene'yi tıklatın veya maaş mantığı bildirin.</span><span class="sxs-lookup"><span data-stu-id="4a704-168">This option enables hello solution back end tooeasily inform retry or compensation logic.</span></span> <span data-ttu-id="4a704-169">Merhaba bulut cihaz geri bildirim hakkında daha fazla bilgi için bkz: [IOT Hub Geliştirici Kılavuzu][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="4a704-169">For more information about cloud-to-device feedback, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="4a704-170">Bu bölümde, hello değiştirme **SendCloudToDevice** uygulama toorequest geri bildirim ve IOT Hub'ından alırsınız.</span><span class="sxs-lookup"><span data-stu-id="4a704-170">In this section, you modify hello **SendCloudToDevice** app toorequest feedback, and receive it from IoT Hub.</span></span>

1. <span data-ttu-id="4a704-171">Visual Studio'da, hello **SendCloudToDevice** projesi, yöntem toohello aşağıdaki hello eklemek **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="4a704-171">In Visual Studio, in hello **SendCloudToDevice** project, add hello following method toohello **Program** class.</span></span>
   
        private async static void ReceiveFeedbackAsync()
        {
            var feedbackReceiver = serviceClient.GetFeedbackReceiver();
   
            Console.WriteLine("\nReceiving c2d feedback from service");
            while (true)
            {
                var feedbackBatch = await feedbackReceiver.ReceiveAsync();
                if (feedbackBatch == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received feedback: {0}", string.Join(", ", feedbackBatch.Records.Select(f => f.StatusCode)));
                Console.ResetColor();
   
                await feedbackReceiver.CompleteAsync(feedbackBatch);
            }
        }
   
    <span data-ttu-id="4a704-172">Bu alma düzeni aynı bir kullanılan tooreceive bulut-cihaz iletilerini hello aygıt uygulamadan hello unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4a704-172">Note this receive pattern is hello same one used tooreceive cloud-to-device messages from hello device app.</span></span>
2. <span data-ttu-id="4a704-173">Merhaba yönteminde aşağıdaki hello eklemek **ana** hello hemen sonra yöntemi `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` satır:</span><span class="sxs-lookup"><span data-stu-id="4a704-173">Add hello following method in hello **Main** method, right after hello `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` line:</span></span>
   
        ReceiveFeedbackAsync();
3. <span data-ttu-id="4a704-174">toorequest geribildirim bulut cihaz iletinizin hello teslimi için toospecify bir özelliğe sahip hello **SendCloudToDeviceMessageAsync** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="4a704-174">toorequest feedback for hello delivery of your cloud-to-device message, you have toospecify a property in hello **SendCloudToDeviceMessageAsync** method.</span></span> <span data-ttu-id="4a704-175">Satır, hemen sonra hello aşağıdaki hello eklemek `var commandMessage = new Message(...);` satır:</span><span class="sxs-lookup"><span data-stu-id="4a704-175">Add hello following line, right after hello `var commandMessage = new Message(...);` line:</span></span>
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. <span data-ttu-id="4a704-176">Basarak Hello uygulamaları çalıştırmak **F5**.</span><span class="sxs-lookup"><span data-stu-id="4a704-176">Run hello apps by pressing **F5**.</span></span> <span data-ttu-id="4a704-177">Başlangıç üç uygulama görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4a704-177">You should see all three applications start.</span></span> <span data-ttu-id="4a704-178">Select hello **SendCloudToDevice** windows ve tuşuna **Enter**.</span><span class="sxs-lookup"><span data-stu-id="4a704-178">Select hello **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="4a704-179">İleti hello cihaz uygulaması tarafından ve birkaç saniye sonra alınan, hello tarafından alınan geri bildirim iletisi hello görmeniz gerekir, **SendCloudToDevice** uygulama.</span><span class="sxs-lookup"><span data-stu-id="4a704-179">You should see hello message being received by hello device app, and after a few seconds, hello feedback message being received by your **SendCloudToDevice** application.</span></span>
   
   ![Uygulama alma iletisi][22]

> [!NOTE]
> <span data-ttu-id="4a704-181">Basitlik'ın artırmak amacıyla için bu öğreticiyi herhangi bir yeniden deneme ilkesi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="4a704-181">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="4a704-182">Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme].</span><span class="sxs-lookup"><span data-stu-id="4a704-182">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4a704-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4a704-183">Next steps</span></span>
<span data-ttu-id="4a704-184">Bu öğreticide, nasıl öğrenilen toosend ve bulut-cihaz iletilerini.</span><span class="sxs-lookup"><span data-stu-id="4a704-184">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="4a704-185">IOT hub'ı kullanan tam uçtan uca çözümler toosee örnekleri bkz [Azure IOT paketi].</span><span class="sxs-lookup"><span data-stu-id="4a704-185">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="4a704-186">IOT Hub ile çözümleri geliştirme hakkında daha fazla toolearn bkz hello [IOT Hub Geliştirici Kılavuzu].</span><span class="sxs-lookup"><span data-stu-id="4a704-186">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<!-- Images -->
[20]: ./media/iot-hub-csharp-csharp-c2d/create-identity-csharp1.png
[21]: ./media/iot-hub-csharp-csharp-c2d/sendc2d1.png
[22]: ./media/iot-hub-csharp-csharp-c2d/sendc2d2.png

<!-- Links -->

[Azure IOT hizmeti SDK'sı NuGet paketi]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[geçici hata işleme]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md

[IOT Hub Geliştirici Kılavuzu]: iot-hub-devguide.md
[IOT Hub ile çalışmaya başlama]: iot-hub-csharp-csharp-getstarted.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure IOT paketi]: https://docs.microsoft.com/en-us/azure/iot-suite/
[Azure IOT cihaz SDK'ları]: iot-hub-devguide-sdks.md