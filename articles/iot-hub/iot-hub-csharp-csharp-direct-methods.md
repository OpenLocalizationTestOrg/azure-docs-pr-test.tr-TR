---
title: "Azure IOT hub'ı doğrudan yöntemleri (.NET/.NET) | Microsoft Docs"
description: "Azure IOT hub'ı doğrudan yöntemlerinin nasıl kullanılacağını. Doğrudan bir yöntem ve Azure IOT hizmeti SDK'sını doğrudan yöntemini çağıran bir hizmet uygulaması uygulamak .NET için içeren bir sanal cihaz uygulamasının uygulamak için Azure IOT cihaz SDK'sı .NET için kullanın."
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
ms.openlocfilehash: 9ce1fbebb6417c10618aa182e3c1d9ddf8132fb6
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="use-direct-methods-netnet"></a><span data-ttu-id="44d57-104">Doğrudan yöntemleri (.NET/.NET) kullanın</span><span class="sxs-lookup"><span data-stu-id="44d57-104">Use direct methods (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="44d57-105">Bu öğreticide, şu iki .NET konsol uygulamaları geliştirmek için yapacaksınız:</span><span class="sxs-lookup"><span data-stu-id="44d57-105">In this tutorial, we are going to develop two .NET console apps:</span></span>

* <span data-ttu-id="44d57-106">**CallMethodOnDevice**, sanal cihaz uygulamasının bir yöntemi çağırır ve yanıt görüntüler bir arka uç uygulaması.</span><span class="sxs-lookup"><span data-stu-id="44d57-106">**CallMethodOnDevice**, a back-end app, which calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="44d57-107">**SimulateDeviceMethods**, daha önce oluşturulan cihaz kimliğiyle IOT hub'ınıza bağlanan bir cihaza benzetim bir konsol uygulaması ve yöntemi yanıtlar bulut tarafından çağrılır.</span><span class="sxs-lookup"><span data-stu-id="44d57-107">**SimulateDeviceMethods**, a console app which simulates a device connecting to your IoT hub with the device identity created earlier, and responds to the method called by the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="44d57-108">[IoT Hub SDK'ları][lnk-hub-sdks] makalesi, hem cihazlarınızda hem de çözüm arka ucunuzda çalıştırılacak uygulamalar oluşturmak için kullanabileceğiniz Azure IoT SDK’ları hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="44d57-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="44d57-109">Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="44d57-109">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="44d57-110">Visual Studio 2015 veya Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="44d57-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="44d57-111">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="44d57-111">An active Azure account.</span></span> <span data-ttu-id="44d57-112">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="44d57-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="44d57-113">Bunun yerine cihaz kimliğini program aracılığıyla oluşturmak istiyorsanız, ilgili bölümünü okuyun [.NET kullanarak IOT hub'ınıza sanal Cihazınızı bağlamak] [ lnk-device-identity-csharp] makalesi.</span><span class="sxs-lookup"><span data-stu-id="44d57-113">If you want to create the device identity programmatically instead, read the corresponding section in the [Connect your simulated device to your IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="44d57-114">Sanal cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="44d57-114">Create a simulated device app</span></span>
<span data-ttu-id="44d57-115">Bu bölümde, çözüm tarafından arka uç olarak adlandırılan bir yönteme yanıt veren bir .NET konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="44d57-115">In this section, you create a .NET console app that responds to a method called by the solution back end.</span></span>

1. <span data-ttu-id="44d57-116">Visual Studio'da **Konsol Uygulaması** proje şablonunu kullanarak geçerli çözüme bir Visual C# Windows Klasik Masaüstü projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="44d57-116">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="44d57-117">Proje adı **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="44d57-117">Name the project **SimulateDeviceMethods**.</span></span>
   
    ![Yeni Visual C# Klasik Windows cihaz uygulaması][img-createdeviceapp]
    
1. <span data-ttu-id="44d57-119">Çözüm Gezgini'nde sağ **SimulateDeviceMethods** proje ve ardından **NuGet paketlerini Yönet...** .</span><span class="sxs-lookup"><span data-stu-id="44d57-119">In Solution Explorer, right-click the **SimulateDeviceMethods** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="44d57-120">İçinde **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat** arayın ve **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="44d57-120">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="44d57-121">Seçin **yükleme** yüklemek için **Microsoft.Azure.Devices.Client** paketini ve kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="44d57-121">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="44d57-122">Bu yordam indirir, yükler ve bir başvuru ekler [Azure IOT cihaz SDK'sı] [ lnk-nuget-client-sdk] NuGet paketi ve bağımlılıklarını.</span><span class="sxs-lookup"><span data-stu-id="44d57-122">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet Paket Yöneticisi penceresi istemci uygulaması][img-clientnuget]
1. <span data-ttu-id="44d57-124">Aşağıdaki `using` deyimlerini **Program.cs** dosyasının üst kısmına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="44d57-124">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. <span data-ttu-id="44d57-125">**Program** sınıfına aşağıdaki alanları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="44d57-125">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="44d57-126">Yer tutucu değerini önceki bölümünde belirtildiği cihaz bağlantı dizesini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="44d57-126">Replace the placeholder value with the device connection string that you noted in the previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="44d57-127">Cihazda doğrudan yöntemi uygulamak için aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="44d57-127">Add the following to implement the direct method on the device:</span></span>

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written to log.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. <span data-ttu-id="44d57-128">Son olarak, aşağıdaki kodu ekleyin **ana** IOT hub'ınıza bağlantıyı açın ve yöntemi dinleyicisini başlatmak için yöntem:</span><span class="sxs-lookup"><span data-stu-id="44d57-128">Finally, add the following code to the **Main** method to open the connection to your IoT hub and initialize the method listener:</span></span>
   
        try
        {
            Console.WriteLine("Connecting to hub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);

            // setup callback for "writeLine" method
            Client.SetMethodHandlerAsync("writeLine", WriteLineToConsole, null).Wait();
            Console.WriteLine("Waiting for direct method call\n Press enter to exit.");
            Console.ReadLine();

            Console.WriteLine("Exiting...");

            // as a good practice, remove the "writeLine" handler
            Client.SetMethodHandlerAsync("writeLine", null, null).Wait();
            Client.CloseAsync().Wait();
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
        
1. <span data-ttu-id="44d57-129">Visual Studio Çözüm Gezgini'nde Çözümünüze sağ tıklayın ve ardından **başlangıç projelerini Ayarla...** .</span><span class="sxs-lookup"><span data-stu-id="44d57-129">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**.</span></span> <span data-ttu-id="44d57-130">Seçin **tek başlangıç projesi**ve ardından **SimulateDeviceMethods** açılır menüsünde projesinde.</span><span class="sxs-lookup"><span data-stu-id="44d57-130">Select **Single startup project**, and then select the **SimulateDeviceMethods** project in the dropdown menu.</span></span>        

> [!NOTE]
> <span data-ttu-id="44d57-131">Sade ve basit bir anlatım gözetildiği için bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="44d57-131">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="44d57-132">Üretim kodunda yeniden deneme ilkelerini (bağlantı yeniden deneme), önerilen MSDN makalesinde uygulamalıdır [geçici hata işleme][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="44d57-132">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="44d57-133">Bir cihazda doğrudan bir yöntem çağrısı</span><span class="sxs-lookup"><span data-stu-id="44d57-133">Call a direct method on a device</span></span>
<span data-ttu-id="44d57-134">Bu bölümde, sanal cihaz uygulamasının bir yöntemi çağırır ve yanıt görüntüleyen bir .NET konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="44d57-134">In this section, you create a .NET console app that calls a method in the simulated device app and then displays the response.</span></span>

1. <span data-ttu-id="44d57-135">Visual Studio'da **Konsol Uygulaması** proje şablonunu kullanarak geçerli çözüme bir Visual C# Windows Klasik Masaüstü projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="44d57-135">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="44d57-136">.NET Framework sürümünün 4.5.1 veya sonraki bir sürüm olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="44d57-136">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="44d57-137">Proje adı **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="44d57-137">Name the project **CallMethodOnDevice**.</span></span>
   
    ![Yeni Visual C# Windows Klasik Masaüstü projesi][img-createserviceapp]
2. <span data-ttu-id="44d57-139">Çözüm Gezgini'nde sağ **CallMethodOnDevice** proje ve ardından **NuGet paketlerini Yönet...** .</span><span class="sxs-lookup"><span data-stu-id="44d57-139">In Solution Explorer, right-click the **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="44d57-140">**NuGet Paket Yöneticisi** penceresinde **Gözat**'ı seçin, **microsoft.azure.devices**'ı aratın, **Microsoft.Azure.Devices** paketini yüklemek için **Yükle**'yi seçin ve kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="44d57-140">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="44d57-141">Bu yordam ile [Azure IoT hizmet SDK'sı][lnk-nuget-service-sdk] NuGet paketi ve bağımlılıkları indirilir, yüklenir ve bu pakete bir başvuru eklenir.</span><span class="sxs-lookup"><span data-stu-id="44d57-141">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet Paket Yöneticisi penceresi][img-servicenuget]

4. <span data-ttu-id="44d57-143">Aşağıdaki `using` deyimlerini **Program.cs** dosyasının üst kısmına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="44d57-143">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="44d57-144">**Program** sınıfına aşağıdaki alanları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="44d57-144">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="44d57-145">Yer tutucu değerini, önceki bölümde hub için oluşturduğunuz IoT Hub bağlantı dizesiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="44d57-145">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="44d57-146">**Program** sınıfına aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="44d57-146">Add the following method to the **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line to be written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="44d57-147">Bu yöntem adı ile doğrudan bir yöntem çağırır `writeLine` üzerinde `myDeviceId` aygıt.</span><span class="sxs-lookup"><span data-stu-id="44d57-147">This method invokes a direct method with name `writeLine` on the `myDeviceId` device.</span></span> <span data-ttu-id="44d57-148">Ardından, konsol aygıtta tarafından sağlanan yanıt yazar.</span><span class="sxs-lookup"><span data-stu-id="44d57-148">Then, it writes the response provided by the device on the console.</span></span> <span data-ttu-id="44d57-149">Nasıl yanıt aygıta için zaman aşımı değeri belirlemek mümkün olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="44d57-149">Note how it is possible to specify a timeout value for the device to respond.</span></span>
7. <span data-ttu-id="44d57-150">Son olarak, **Main** yöntemine aşağıdaki satırları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="44d57-150">Finally, add the following lines to the **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

1. <span data-ttu-id="44d57-151">Visual Studio Çözüm Gezgini'nde Çözümünüze sağ tıklayın ve ardından **başlangıç projelerini Ayarla...** .</span><span class="sxs-lookup"><span data-stu-id="44d57-151">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**.</span></span> <span data-ttu-id="44d57-152">Seçin **tek başlangıç projesi**ve ardından **CallMethodOnDevice** açılır menüsünde projesinde.</span><span class="sxs-lookup"><span data-stu-id="44d57-152">Select **Single startup project**, and then select the **CallMethodOnDevice** project in the dropdown menu.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="44d57-153">Uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="44d57-153">Run the applications</span></span>
<span data-ttu-id="44d57-154">Şimdi uygulamaları çalıştırmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="44d57-154">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="44d57-155">.NET cihaz uygulama çalıştırma **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="44d57-155">Run the .NET device app **SimulateDeviceMethods**.</span></span> <span data-ttu-id="44d57-156">IOT Hub'ınızı gelen yöntem çağrıları için dinleme başlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="44d57-156">It should start listening for method calls from your IoT Hub:</span></span> 

    ![Cihaz uygulaması çalıştırın][img-deviceapprun]
1. <span data-ttu-id="44d57-158">Artık, cihazın bağlı ve .NET çalıştırmak için yöntem çağrılarına, bekleyen **CallMethodOnDevice** sanal cihaz uygulamasının yöntemi çağırmak için uygulama.</span><span class="sxs-lookup"><span data-stu-id="44d57-158">Now that the device is connected and waiting for method invocations, run the .NET **CallMethodOnDevice** app to invoke the method in the simulated device app.</span></span> <span data-ttu-id="44d57-159">Konsolda yazılmış aygıt yanıtı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="44d57-159">You should see the device response written in the console.</span></span>
   
    ![Hizmet uygulaması çalıştırın][img-serviceapprun]
1. <span data-ttu-id="44d57-161">Cihaz daha sonra bu iletiyi yazdırma tarafından yönteme tepki verdiğini:</span><span class="sxs-lookup"><span data-stu-id="44d57-161">The device then reacts to the method by printing this message:</span></span>
   
    ![Cihazda çağrılan doğrudan yöntemi][img-directmethodinvoked]

## <a name="next-steps"></a><span data-ttu-id="44d57-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="44d57-163">Next steps</span></span>
<span data-ttu-id="44d57-164">Bu öğreticide, Azure portalında yeni bir IoT hub'ı yapılandırdınız ve ardından IoT hub'ının kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="44d57-164">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="44d57-165">Bu cihaz kimliğini bulut tarafından çağrılan yöntemler tepki vermek sanal cihaz uygulamasının sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="44d57-165">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="44d57-166">Ayrıca aygıtta yöntemleri çağırır ve aygıttan yanıt görüntüleyen bir uygulama oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="44d57-166">You also created an app that invokes methods on the device and displays the response from the device.</span></span> 

<span data-ttu-id="44d57-167">IoT Hub’ı kullanmaya başlamak ve diğer IoT senaryolarını keşfetmek için bkz:</span><span class="sxs-lookup"><span data-stu-id="44d57-167">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="44d57-168">[IOT Hub ile çalışmaya başlama]</span><span class="sxs-lookup"><span data-stu-id="44d57-168">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="44d57-169">[Birden çok aygıta işleri zamanla][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="44d57-169">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="44d57-170">Çözüm ve zamanlama yöntemini çağıran birden fazla cihazda, IOT genişletmek öğrenmek için bkz: [zamanlama ve yayın işleri] [ lnk-tutorial-jobs] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="44d57-170">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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

<span data-ttu-id="44d57-171">[IOT Hub ile çalışmaya başlama]: iot-hub-node-node-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="44d57-171">[Get started with IoT Hub]: iot-hub-node-node-getstarted.md</span></span>
