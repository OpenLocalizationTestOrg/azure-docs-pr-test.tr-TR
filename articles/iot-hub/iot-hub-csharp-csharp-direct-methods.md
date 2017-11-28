---
title: "Azure IOT Hub aaaUse doğrudan yöntemleri (.NET/.NET) | Microsoft Docs"
description: "Nasıl toouse Azure IOT Hub yöntemleri doğrudan. .NET tooimplement doğrudan yöntemi ve hello .NET tooimplement hello doğrudan yöntemini çağıran bir hizmet uygulaması için Azure IOT hizmeti SDK'sını içeren sanal cihaz uygulaması için hello Azure IOT cihaz SDK'sını kullanın."
services: iot-hub
documentationcenter: 
author: dsk-2015
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: dkshir
ms.openlocfilehash: d4fa093a99558ec6faf294c2583a14a722b9ac03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnet"></a><span data-ttu-id="08c05-104">Doğrudan yöntemleri (.NET/.NET) kullanın</span><span class="sxs-lookup"><span data-stu-id="08c05-104">Use direct methods (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="08c05-105">Bu öğreticide, devam eden toodevelop iki .NET konsol uygulamaları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="08c05-105">In this tutorial, we are going toodevelop two .NET console apps:</span></span>

* <span data-ttu-id="08c05-106">**CallMethodOnDevice**, hello sanal cihaz uygulamasının bir yöntemi çağırır ve hello yanıt görüntüler bir arka uç uygulaması.</span><span class="sxs-lookup"><span data-stu-id="08c05-106">**CallMethodOnDevice**, a back-end app, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="08c05-107">**SimulateDeviceMethods**, tooyour IOT hub'ı daha önce oluşturulan hello cihaz kimliğiyle bağlanan bir cihaza benzetim ve hello bulut tarafından adlı toohello yöntemi yanıt bir konsol uygulaması.</span><span class="sxs-lookup"><span data-stu-id="08c05-107">**SimulateDeviceMethods**, a console app which simulates a device connecting tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="08c05-108">Merhaba makale [Azure IOT SDK'ları] [ lnk-hub-sdks] aygıtlar ve çözüm arka ucunuz hem uygulamalar toorun toobuild kullanabileceğiniz hello Azure IOT SDK'ları hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="08c05-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="08c05-109">toocomplete Bu öğretici, gerekir:</span><span class="sxs-lookup"><span data-stu-id="08c05-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="08c05-110">Visual Studio 2015 veya Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="08c05-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="08c05-111">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="08c05-111">An active Azure account.</span></span> <span data-ttu-id="08c05-112">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="08c05-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="08c05-113">Toocreate hello cihaz kimliği programlı olarak bunun yerine isterseniz, hello hello ilgili bölümünü okuyun [.NET kullanarak sanal cihaz tooyour IOT hub'ınıza bağlanmak] [ lnk-device-identity-csharp] makalesi.</span><span class="sxs-lookup"><span data-stu-id="08c05-113">If you want toocreate hello device identity programmatically instead, read hello corresponding section in hello [Connect your simulated device tooyour IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="08c05-114">Sanal cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="08c05-114">Create a simulated device app</span></span>
<span data-ttu-id="08c05-115">Bu bölümde, hello çözüm tarafından arka uç adlı tooa yöntemi yanıt veren bir .NET konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="08c05-115">In this section, you create a .NET console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="08c05-116">Visual Studio'da hello kullanarak bir Visual C# Windows Klasik Masaüstü projesi toohello geçerli çözüme ekleyin **konsol uygulaması** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="08c05-116">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="08c05-117">Ad hello proje **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="08c05-117">Name hello project **SimulateDeviceMethods**.</span></span>
   
    ![Yeni Visual C# Klasik Windows cihaz uygulaması][img-createdeviceapp]
    
1. <span data-ttu-id="08c05-119">Çözüm Gezgini'nde hello sağ **SimulateDeviceMethods** proje ve ardından **NuGet paketlerini Yönet...** .</span><span class="sxs-lookup"><span data-stu-id="08c05-119">In Solution Explorer, right-click hello **SimulateDeviceMethods** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="08c05-120">Merhaba, **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat** arayın ve **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="08c05-120">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="08c05-121">Seçin **yükleme** tooinstall hello **Microsoft.Azure.Devices.Client** paketini ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="08c05-121">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="08c05-122">Bu yordam indirir, yükler ve başvuru toohello ekler [Azure IOT cihaz SDK'sı] [ lnk-nuget-client-sdk] NuGet paketi ve bağımlılıklarını.</span><span class="sxs-lookup"><span data-stu-id="08c05-122">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet Paket Yöneticisi penceresi istemci uygulaması][img-clientnuget]
1. <span data-ttu-id="08c05-124">Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:</span><span class="sxs-lookup"><span data-stu-id="08c05-124">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. <span data-ttu-id="08c05-125">Aşağıdaki alanları toohello hello eklemek **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="08c05-125">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="08c05-126">Merhaba yer tutucu değerini hello önceki bölümünde belirtildiği hello cihaz bağlantı dizesini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="08c05-126">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="08c05-127">Merhaba aygıtta tooimplement hello doğrudan yöntemi aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="08c05-127">Add hello following tooimplement hello direct method on hello device:</span></span>

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written toolog.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. <span data-ttu-id="08c05-128">Son olarak, aşağıdaki kod toohello hello eklemek **ana** yöntemi tooopen hello bağlantı tooyour IOT hub ve başlatma hello yöntemi dinleyicisi:</span><span class="sxs-lookup"><span data-stu-id="08c05-128">Finally, add hello following code toohello **Main** method tooopen hello connection tooyour IoT hub and initialize hello method listener:</span></span>
   
        try
        {
            Console.WriteLine("Connecting toohub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);

            // setup callback for "writeLine" method
            Client.SetMethodHandlerAsync("writeLine", WriteLineToConsole, null).Wait();
            Console.WriteLine("Waiting for direct method call\n Press enter tooexit.");
            Console.ReadLine();

            Console.WriteLine("Exiting...");

            // as a good practice, remove hello "writeLine" handler
            Client.SetMethodHandlerAsync("writeLine", null, null).Wait();
            Client.CloseAsync().Wait();
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
        
1. <span data-ttu-id="08c05-129">Buna Visual Studio Çözüm Gezgini Merhaba, çözümünüze sağ tıklayın ve ardından **başlangıç projelerini Ayarla...** . Seçin **tek başlangıç projesi**ve ardından hello **SimulateDeviceMethods** hello açılır menüsünde projesinde.</span><span class="sxs-lookup"><span data-stu-id="08c05-129">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **SimulateDeviceMethods** project in hello dropdown menu.</span></span>        

> [!NOTE]
> <span data-ttu-id="08c05-130">tookeep şeyler basit, Bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="08c05-130">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="08c05-131">Üretim kodunda yeniden deneme ilkelerini (bağlantı yeniden deneme), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="08c05-131">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="08c05-132">Bir cihazda doğrudan bir yöntem çağrısı</span><span class="sxs-lookup"><span data-stu-id="08c05-132">Call a direct method on a device</span></span>
<span data-ttu-id="08c05-133">Bu bölümde, hello sanal cihaz uygulamasının bir yöntemi çağırır ve hello yanıt görüntüleyen bir .NET konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="08c05-133">In this section, you create a .NET console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="08c05-134">Visual Studio'da hello kullanarak bir Visual C# Windows Klasik Masaüstü projesi toohello geçerli çözüme ekleyin **konsol uygulaması** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="08c05-134">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="08c05-135">Merhaba .NET Framework sürümünün 4.5.1 olduğundan emin olun veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="08c05-135">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="08c05-136">Ad hello proje **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="08c05-136">Name hello project **CallMethodOnDevice**.</span></span>
   
    ![Yeni Visual C# Windows Klasik Masaüstü projesi][img-createserviceapp]
2. <span data-ttu-id="08c05-138">Çözüm Gezgini'nde hello sağ **CallMethodOnDevice** proje ve ardından **NuGet paketlerini Yönet...** .</span><span class="sxs-lookup"><span data-stu-id="08c05-138">In Solution Explorer, right-click hello **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="08c05-139">Merhaba, **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat**, arama **microsoft.azure.devices**seçin **yükleme** tooinstall Merhaba **Microsoft.Azure.Devices** paketini ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="08c05-139">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="08c05-140">Bu yordam indirir, yükler ve başvuru toohello ekler [Azure IOT hizmeti SDK'sını] [ lnk-nuget-service-sdk] NuGet paketi ve bağımlılıklarını.</span><span class="sxs-lookup"><span data-stu-id="08c05-140">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet Paket Yöneticisi penceresi][img-servicenuget]

4. <span data-ttu-id="08c05-142">Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:</span><span class="sxs-lookup"><span data-stu-id="08c05-142">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="08c05-143">Aşağıdaki alanları toohello hello eklemek **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="08c05-143">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="08c05-144">Merhaba hello önceki bölümde oluşturduğunuz hello hub'ın IOT Hub bağlantı dizesine sahip Hello yer tutucu değerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="08c05-144">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="08c05-145">Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="08c05-145">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="08c05-146">Bu yöntem adı ile doğrudan bir yöntem çağırır `writeLine` hello üzerinde `myDeviceId` aygıt.</span><span class="sxs-lookup"><span data-stu-id="08c05-146">This method invokes a direct method with name `writeLine` on hello `myDeviceId` device.</span></span> <span data-ttu-id="08c05-147">Ardından, hello konsolunda hello aygıt tarafından sağlanan hello yanıt yazar.</span><span class="sxs-lookup"><span data-stu-id="08c05-147">Then, it writes hello response provided by hello device on hello console.</span></span> <span data-ttu-id="08c05-148">Nasıl olası toospecify hello aygıt toorespond için zaman aşımı değeri olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="08c05-148">Note how it is possible toospecify a timeout value for hello device toorespond.</span></span>
7. <span data-ttu-id="08c05-149">Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="08c05-149">Finally, add hello following lines toohello **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="08c05-150">Buna Visual Studio Çözüm Gezgini Merhaba, çözümünüze sağ tıklayın ve ardından **başlangıç projelerini Ayarla...** . Seçin **tek başlangıç projesi**ve ardından hello **CallMethodOnDevice** hello açılır menüsünde projesinde.</span><span class="sxs-lookup"><span data-stu-id="08c05-150">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **CallMethodOnDevice** project in hello dropdown menu.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="08c05-151">Merhaba uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="08c05-151">Run hello applications</span></span>
<span data-ttu-id="08c05-152">Hazır toorun hello uygulamaları sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="08c05-152">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="08c05-153">Merhaba .NET cihaz uygulamayı çalıştırma **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="08c05-153">Run hello .NET device app **SimulateDeviceMethods**.</span></span> <span data-ttu-id="08c05-154">IOT Hub'ınızı gelen yöntem çağrıları için dinleme başlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="08c05-154">It should start listening for method calls from your IoT Hub:</span></span> 

    ![Cihaz uygulaması çalıştırın][img-deviceapprun]
1. <span data-ttu-id="08c05-156">Şimdi bu hello cihaz bağlı ve hello .NET çalıştırmak için yöntem çağrılarına bekleniyor, **CallMethodOnDevice** hello sanal cihaz uygulamasının uygulama tooinvoke hello yöntemi.</span><span class="sxs-lookup"><span data-stu-id="08c05-156">Now that hello device is connected and waiting for method invocations, run hello .NET **CallMethodOnDevice** app tooinvoke hello method in hello simulated device app.</span></span> <span data-ttu-id="08c05-157">Merhaba konsolunda yazılmış hello aygıt yanıtı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="08c05-157">You should see hello device response written in hello console.</span></span>
   
    ![Hizmet uygulaması çalıştırın][img-serviceapprun]
1. <span data-ttu-id="08c05-159">Hello aygıt sonra bu iletiyi yazdırma tarafından toohello yöntemi tepki verir:</span><span class="sxs-lookup"><span data-stu-id="08c05-159">hello device then reacts toohello method by printing this message:</span></span>
   
    ![Merhaba aygıtta çağrılan doğrudan yöntemi][img-directmethodinvoked]

## <a name="next-steps"></a><span data-ttu-id="08c05-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="08c05-161">Next steps</span></span>
<span data-ttu-id="08c05-162">Bu öğreticide hello Azure portalında yeni bir IOT hub yapılandırılmış ve ardından hello IOT hub'ın kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="08c05-162">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="08c05-163">Merhaba bulut tarafından çağrılan bu cihaz kimliğini tooenable benzetimli hello aygıt uygulama tooreact toomethods kullanılır.</span><span class="sxs-lookup"><span data-stu-id="08c05-163">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="08c05-164">Merhaba aygıtta yöntemleri çağırır ve hello yanıt hello aygıttan görüntüleyen bir uygulama da oluşturmuş.</span><span class="sxs-lookup"><span data-stu-id="08c05-164">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="08c05-165">Başlarken toocontinue IOT Hub ve tooexplore diğer IOT senaryolarını bakın:</span><span class="sxs-lookup"><span data-stu-id="08c05-165">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="08c05-166">[IOT Hub ile çalışmaya başlama]</span><span class="sxs-lookup"><span data-stu-id="08c05-166">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="08c05-167">[Birden çok aygıta işleri zamanla][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="08c05-167">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="08c05-168">toolearn tooextend birden fazla cihazda IOT çözümü ve zamanlama yöntemi çağırır nasıl hello bkz [zamanlama ve yayın işleri] [ lnk-tutorial-jobs] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="08c05-168">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[img-createdeviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-device-app.png
[img-clientnuget]: ./media/iot-hub-csharp-csharp-direct-methods/device-app-nuget.png
[img-createserviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-service-app.png
[img-servicenuget]: ./media/iot-hub-csharp-csharp-direct-methods/service-app-nuget.png
[img-deviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-device-app.png
[img-serviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-service-app.png
[img-directmethodinvoked]: ./media/iot-hub-csharp-csharp-direct-methods/direct-method-invoked.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[IOT Hub ile çalışmaya başlama]: iot-hub-node-node-getstarted.md
