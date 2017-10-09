---
title: "aygıtları tooAzure IOT Hub .NET ile aaaUpload dosyalarından | Microsoft Docs"
description: ".NET için Azure IOT cihaz SDK'sını kullanarak bir aygıtı toohello buluttan nasıl tooupload dosyaları. Karşıya yüklenen dosyaların bir Azure depolama blob kapsayıcısında depolanır."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 4759d229-f856-4526-abda-414f8b00a56d
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/04/2017
ms.author: elioda
ms.openlocfilehash: 07d555f6ba8b067bbd3233bc8eebaa220ad2388b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub-using-net"></a><span data-ttu-id="2712b-104">.NET kullanarak IOT Hub ile cihaz toohello bulut dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="2712b-104">Upload files from your device toohello cloud with IoT Hub using .NET</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="2712b-105">Bu öğretici hello hello kodda inşa edilmiştir [IOT Hub ile bulut cihaza ileti gönderme](iot-hub-csharp-csharp-c2d.md) öğretici tooshow, nasıl toouse hello IOT Hub'ın dosya karşıya yükleme özellikleri.</span><span class="sxs-lookup"><span data-stu-id="2712b-105">This tutorial builds on hello code in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial tooshow you how toouse hello file upload capabilities of IoT Hub.</span></span> <span data-ttu-id="2712b-106">Size bir nasıl gösterir için:</span><span class="sxs-lookup"><span data-stu-id="2712b-106">It shows you how to:</span></span>

- <span data-ttu-id="2712b-107">Güvenli bir şekilde bir aygıt ile Azure sağlayan bir dosya yüklemek için URI blob.</span><span class="sxs-lookup"><span data-stu-id="2712b-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="2712b-108">Merhaba, uygulama arka ucu IOT hub'ı dosya karşıya yükleme bildirimleri tootrigger işleme hello dosyasında kullanın.</span><span class="sxs-lookup"><span data-stu-id="2712b-108">Use hello IoT Hub file upload notifications tootrigger processing hello file in your app back end.</span></span>

<span data-ttu-id="2712b-109">Merhaba [IOT Hub ile çalışmaya başlama](iot-hub-csharp-csharp-getstarted.md) ve [IOT Hub ile bulut cihaza ileti gönderme](iot-hub-csharp-csharp-c2d.md) öğreticiler hello temel cihaz Bulut ve bulut-cihaz Mesajlaşma işlevlerini IOT hub'ı gösterir.</span><span class="sxs-lookup"><span data-stu-id="2712b-109">hello [Get started with IoT Hub](iot-hub-csharp-csharp-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorials show hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="2712b-110">Merhaba [işlem cihaz-bulut iletileri](iot-hub-csharp-csharp-process-d2c.md) öğretici bir şekilde tooreliably store cihaz bulut iletilerini Azure blob depolama alanındaki açıklar.</span><span class="sxs-lookup"><span data-stu-id="2712b-110">hello [Process Device-to-Cloud messages](iot-hub-csharp-csharp-process-d2c.md) tutorial describes a way tooreliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="2712b-111">Ancak, bazı senaryolarda hello veri cihazlarınızı IOT hub'ı kabul eden hello görece küçük cihaz bulut iletilere Gönder kolayca eşlenemiyor.</span><span class="sxs-lookup"><span data-stu-id="2712b-111">However, in some scenarios you cannot easily map hello data your devices send into hello relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="2712b-112">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="2712b-112">For example:</span></span>

* <span data-ttu-id="2712b-113">Görüntüleri içeren büyük dosyaları</span><span class="sxs-lookup"><span data-stu-id="2712b-113">Large files that contain images</span></span>
* <span data-ttu-id="2712b-114">Videolar</span><span class="sxs-lookup"><span data-stu-id="2712b-114">Videos</span></span>
* <span data-ttu-id="2712b-115">Yüksek sıklıkta örneklenen titreşimi veri</span><span class="sxs-lookup"><span data-stu-id="2712b-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="2712b-116">Önceden işlenmiş veri çeşit</span><span class="sxs-lookup"><span data-stu-id="2712b-116">Some form of preprocessed data</span></span>

<span data-ttu-id="2712b-117">Bu dosyalar genellikle gibi araçları kullanılarak hello bulutta işlenen toplu olan [Azure Data Factory](../data-factory/index.md) veya hello [Hadoop](../hdinsight/index.md) yığını.</span><span class="sxs-lookup"><span data-stu-id="2712b-117">These files are typically batch processed in hello cloud using tools such as [Azure Data Factory](../data-factory/index.md) or hello [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="2712b-118">Bir aygıt tooupload dosyalarından gerektiğinde, hello güvenliği ve güvenilirliği için IOT hub'ı kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2712b-118">When you need tooupload files from a device, you can still use hello security and reliability of IoT Hub.</span></span>

<span data-ttu-id="2712b-119">Merhaba Bu öğreticinin sonunda iki .NET konsol uygulamaları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2712b-119">At hello end of this tutorial you run two .NET console apps:</span></span>

* <span data-ttu-id="2712b-120">**SimulatedDevice**, hello oluşturulan hello uygulaması değiştirilmiş bir sürümünü [IOT Hub ile bulut cihaza ileti gönderme](iot-hub-csharp-csharp-c2d.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="2712b-120">**SimulatedDevice**, a modified version of hello app created in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial.</span></span> <span data-ttu-id="2712b-121">Bu uygulama, IOT hub tarafından sağlanan bir SAS URI'sini kullanarak bir dosya toostorage yükler.</span><span class="sxs-lookup"><span data-stu-id="2712b-121">This app uploads a file toostorage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="2712b-122">**ReadFileUploadNotification**, IOT hub'ından dosya karşıya yükleme bildirimlerini alır.</span><span class="sxs-lookup"><span data-stu-id="2712b-122">**ReadFileUploadNotification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="2712b-123">IOT hub'ı Azure IOT cihaz SDK'ları çok sayıda cihaz platformları ve (C, Java ve Javascript gibi) dilleri destekler.</span><span class="sxs-lookup"><span data-stu-id="2712b-123">IoT Hub supports many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="2712b-124">Toohello başvuran [Azure IOT Geliştirme Merkezi] hakkında adım adım yönergeler için tooconnect, IOT Hub cihaz tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2712b-124">Refer toohello [Azure IoT Developer Center] for step-by-step instructions on how tooconnect your device tooAzure IoT Hub.</span></span>

<span data-ttu-id="2712b-125">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2712b-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="2712b-126">Visual Studio 2015 veya Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="2712b-126">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="2712b-127">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="2712b-127">An active Azure account.</span></span> <span data-ttu-id="2712b-128">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="2712b-128">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="2712b-129">Bir aygıt uygulamasından bir dosyayı karşıya yüklemek</span><span class="sxs-lookup"><span data-stu-id="2712b-129">Upload a file from a device app</span></span>

<span data-ttu-id="2712b-130">Bu bölümde, oluşturduğunuz hello cihaz uygulamayı değiştirmek [IOT Hub ile bulut cihaza ileti gönderme](iot-hub-csharp-csharp-c2d.md) tooreceive bulut cihaza iletilerden hello IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="2712b-130">In this section, you modify hello device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="2712b-131">Visual Studio'da hello sağ **SimulatedDevice** proje, tıklatın **Ekle**ve ardından **varolan öğeyi**.</span><span class="sxs-lookup"><span data-stu-id="2712b-131">In Visual Studio, right-click hello **SimulatedDevice** project, click **Add**, and then click **Existing Item**.</span></span> <span data-ttu-id="2712b-132">Tooan görüntü dosyasına gidin ve projenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2712b-132">Navigate tooan image file and include it in your project.</span></span> <span data-ttu-id="2712b-133">Bu öğretici hello görüntü adlandırılan varsayar `image.jpg`.</span><span class="sxs-lookup"><span data-stu-id="2712b-133">This tutorial assumes hello image is named `image.jpg`.</span></span>

1. <span data-ttu-id="2712b-134">Merhaba görüntüde sağ tıklayın ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="2712b-134">Right-click on hello image, and then click **Properties**.</span></span> <span data-ttu-id="2712b-135">Olduğundan emin olun **tooOutput dizin kopyalama** çok ayarlanır**her zaman Kopyala**.</span><span class="sxs-lookup"><span data-stu-id="2712b-135">Make sure that **Copy tooOutput Directory** is set too**Copy always**.</span></span>

    ![][1]

1. <span data-ttu-id="2712b-136">Merhaba, **Program.cs** dosya, aşağıdaki deyimleri hello dosyanın üst kısmındaki hello hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2712b-136">In hello **Program.cs** file, add hello following statements at hello top of hello file:</span></span>

    ```csharp
    using System.IO;
    ```

1. <span data-ttu-id="2712b-137">Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="2712b-137">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    private static async void SendToBlobAsync()
    {
        string fileName = "image.jpg";
        Console.WriteLine("Uploading file: {0}", fileName);
        var watch = System.Diagnostics.Stopwatch.StartNew();

        using (var sourceData = new FileStream(@"image.jpg", FileMode.Open))
        {
            await deviceClient.UploadToBlobAsync(fileName, sourceData);
        }

        watch.Stop();
        Console.WriteLine("Time tooupload file: {0}ms\n", watch.ElapsedMilliseconds);
    }
    ```

    <span data-ttu-id="2712b-138">Merhaba `UploadToBlobAsync` yöntemi hello dosya adını alır ve hello dosya toobe akış kaynağı karşıya ve hello karşıya yükleme toostorage işler.</span><span class="sxs-lookup"><span data-stu-id="2712b-138">hello `UploadToBlobAsync` method takes in hello file name and stream source of hello file toobe uploaded and handles hello upload toostorage.</span></span> <span data-ttu-id="2712b-139">Merhaba konsol uygulaması hello süresini tooupload hello dosya görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2712b-139">hello console app displays hello time it takes tooupload hello file.</span></span>

1. <span data-ttu-id="2712b-140">Merhaba yönteminde aşağıdaki hello eklemek **ana** hello önceki yöntemi `Console.ReadLine()` satır:</span><span class="sxs-lookup"><span data-stu-id="2712b-140">Add hello following method in hello **Main** method, right before hello `Console.ReadLine()` line:</span></span>

    ```csharp
    SendToBlobAsync();
    ```

> [!NOTE]
> <span data-ttu-id="2712b-141">Basitlik'ın artırmak amacıyla için bu öğreticiyi herhangi bir yeniden deneme ilkesi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="2712b-141">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="2712b-142">Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme].</span><span class="sxs-lookup"><span data-stu-id="2712b-142">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="2712b-143">Dosya karşıya yükleme bildirimi</span><span class="sxs-lookup"><span data-stu-id="2712b-143">Receive a file upload notification</span></span>

<span data-ttu-id="2712b-144">Bu bölümde IOT hub'dan dosya karşıya yükleme bildirim iletileri alan bir .NET konsol uygulaması yazma.</span><span class="sxs-lookup"><span data-stu-id="2712b-144">In this section, you write a .NET console app that receives file upload notification messages from IoT Hub.</span></span>

1. <span data-ttu-id="2712b-145">Merhaba geçerli Visual Studio çözümünde hello kullanarak bir Visual C# Windows projesi oluşturma **konsol uygulaması** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="2712b-145">In hello current Visual Studio solution, create a Visual C# Windows project by using hello **Console Application** project template.</span></span> <span data-ttu-id="2712b-146">Ad hello proje **ReadFileUploadNotification**.</span><span class="sxs-lookup"><span data-stu-id="2712b-146">Name hello project **ReadFileUploadNotification**.</span></span>

    ![Visual Studio'da yeni proje][2]

1. <span data-ttu-id="2712b-148">Çözüm Gezgini'nde hello sağ **ReadFileUploadNotification** proje ve ardından **NuGet paketlerini Yönet...** .</span><span class="sxs-lookup"><span data-stu-id="2712b-148">In Solution Explorer, right-click hello **ReadFileUploadNotification** project, and then click **Manage NuGet Packages...**.</span></span>

1. <span data-ttu-id="2712b-149">Merhaba, **NuGet Paket Yöneticisi** penceresinde, arama **Microsoft.Azure.Devices**, tıklatın **yüklemek**ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="2712b-149">In hello **NuGet Package Manager** window, search for **Microsoft.Azure.Devices**, click **Install**, and accept hello terms of use.</span></span>

    <span data-ttu-id="2712b-150">Bu eylem indirir, yükler ve başvuru toohello ekler [Azure IOT hizmeti SDK'sı NuGet paketi] hello içinde **ReadFileUploadNotification** projesi.</span><span class="sxs-lookup"><span data-stu-id="2712b-150">This action downloads, installs, and adds a reference toohello [Azure IoT service SDK NuGet package] in hello **ReadFileUploadNotification** project.</span></span>

1. <span data-ttu-id="2712b-151">Merhaba, **Program.cs** dosya, aşağıdaki deyimleri hello dosyanın üst kısmındaki hello hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2712b-151">In hello **Program.cs** file, add hello following statements at hello top of hello file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices;
    ```

1. <span data-ttu-id="2712b-152">Aşağıdaki alanları toohello hello eklemek **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="2712b-152">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="2712b-153">Yedek hello IOT hub bağlantı dizesinden ile Merhaba yer tutucu değerini [IOT Hub ile çalışmaya başlama]:</span><span class="sxs-lookup"><span data-stu-id="2712b-153">Substitute hello placeholder value with hello IoT hub connection string from [Get started with IoT Hub]:</span></span>

    ```csharp
    static ServiceClient serviceClient;
    static string connectionString = "{iot hub connection string}";
    ```

1. <span data-ttu-id="2712b-154">Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="2712b-154">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    private async static void ReceiveFileUploadNotificationAsync()
    {
        var notificationReceiver = serviceClient.GetFileNotificationReceiver();

        Console.WriteLine("\nReceiving file upload notification from service");
        while (true)
        {
            var fileUploadNotification = await notificationReceiver.ReceiveAsync();
            if (fileUploadNotification == null) continue;

            Console.ForegroundColor = ConsoleColor.Yellow;
            Console.WriteLine("Received file upload noticiation: {0}", string.Join(", ", fileUploadNotification.BlobName));
            Console.ResetColor();

            await notificationReceiver.CompleteAsync(fileUploadNotification);
        }
    }
    ```

    <span data-ttu-id="2712b-155">Bu alma düzeni aynı bir kullanılan tooreceive bulut-cihaz iletilerini hello aygıt uygulamadan hello unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2712b-155">Note this receive pattern is hello same one used tooreceive cloud-to-device messages from hello device app.</span></span>

1. <span data-ttu-id="2712b-156">Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="2712b-156">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive file upload notifications\n");
    serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
    ReceiveFileUploadNotificationAsync();
    Console.WriteLine("Press Enter tooexit\n");
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="2712b-157">Merhaba uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="2712b-157">Run hello applications</span></span>

<span data-ttu-id="2712b-158">Hazır toorun hello uygulamaları sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="2712b-158">Now you are ready toorun hello applications.</span></span>

1. <span data-ttu-id="2712b-159">Visual Studio'da Çözümünüze sağ tıklayın ve seçin **başlangıç projelerini Ayarla**.</span><span class="sxs-lookup"><span data-stu-id="2712b-159">In Visual Studio, right-click your solution, and select **Set StartUp projects**.</span></span> <span data-ttu-id="2712b-160">Seçin **birden fazla başlangıç projesi**seçeneğini belirleyip hello **Başlat** eylemi için **ReadFileUploadNotification** ve **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="2712b-160">Select **Multiple startup projects**, then select hello **Start** action for **ReadFileUploadNotification** and **SimulatedDevice**.</span></span>

1. <span data-ttu-id="2712b-161">Tuşuna **F5**.</span><span class="sxs-lookup"><span data-stu-id="2712b-161">Press **F5**.</span></span> <span data-ttu-id="2712b-162">Her iki uygulamayı başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2712b-162">Both applications should start.</span></span> <span data-ttu-id="2712b-163">Bir konsol uygulamasında hello karşıya yükleme tamamlandı ve diğer konsol uygulaması tarafından alınan hello karşıya yükleme bildirim iletisi hello görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2712b-163">You should see hello upload completed in one console app and hello upload notification message received by hello other console app.</span></span> <span data-ttu-id="2712b-164">Merhaba kullanabilirsiniz [Azure portal] veya hello hello varlığını için Visual Studio Sunucu Gezgini toocheck karşıya dosya Azure depolama hesabınızdaki.</span><span class="sxs-lookup"><span data-stu-id="2712b-164">You can use hello [Azure portal] or Visual Studio Server Explorer toocheck for hello presence of hello uploaded file in your Azure Storage account.</span></span>

    ![][50]

## <a name="next-steps"></a><span data-ttu-id="2712b-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2712b-165">Next steps</span></span>

<span data-ttu-id="2712b-166">Bu öğreticide, nasıl toouse hello dosyayı karşıya IOT Hub'ın cihazlardan toosimplify dosya yüklemeleri yeteneklerini öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="2712b-166">In this tutorial, you learned how toouse hello file upload capabilities of IoT Hub toosimplify file uploads from devices.</span></span> <span data-ttu-id="2712b-167">Aşağıdaki makaleleri hello ile tooexplore IOT hub özellikleri ve senaryoları devam edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2712b-167">You can continue tooexplore IoT hub features and scenarios with hello following articles:</span></span>

* <span data-ttu-id="2712b-168">[IOT hub'ı program aracılığıyla oluşturma][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="2712b-168">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="2712b-169">[Giriş tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="2712b-169">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="2712b-170">[Azure IOT SDK'ları][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="2712b-170">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="2712b-171">toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:</span><span class="sxs-lookup"><span data-stu-id="2712b-171">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="2712b-172">[Bir cihaz IOT Edge benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="2712b-172">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png

<!-- Links -->

[Azure portal]: https://portal.azure.com/

[Azure IOT Geliştirme Merkezi]: http://www.azure.com/develop/iot

[geçici hata işleme]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure IOT hizmeti SDK'sı NuGet paketi]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md
