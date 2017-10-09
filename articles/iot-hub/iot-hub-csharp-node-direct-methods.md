---
title: "Azure IOT Hub aaaUse doğrudan yöntemleri (.NET/düğümü) | Microsoft Docs"
description: "Nasıl toouse Azure IOT Hub yöntemleri doğrudan. Node.js tooimplement doğrudan yöntemi ve hello .NET tooimplement hello doğrudan yöntemini çağıran bir hizmet uygulaması için Azure IOT hizmeti SDK'sını içeren sanal cihaz uygulaması için hello Azure IOT cihaz SDK'sını kullanın."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: nberdy
ms.openlocfilehash: f566f939be840eb308b00ffa4e05c4e5b3fefb39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnode"></a><span data-ttu-id="b5c85-104">Doğrudan yöntemleri (.NET/düğüm) kullanın</span><span class="sxs-lookup"><span data-stu-id="b5c85-104">Use direct methods (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="b5c85-105">Bu öğreticide, biz toodevelop bir .NET ve bir Node.js konsol uygulaması yapacaksınız:</span><span class="sxs-lookup"><span data-stu-id="b5c85-105">In this tutorial, we are going toodevelop a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="b5c85-106">**CallMethodOnDevice.sln**, hello sanal cihaz uygulamasının bir yöntemi çağırır ve hello yanıt görüntüler .NET arka uç uygulaması.</span><span class="sxs-lookup"><span data-stu-id="b5c85-106">**CallMethodOnDevice.sln**, a .NET back-end app, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="b5c85-107">**SimulatedDevice.js**, tooyour IOT hub'ı daha önce oluşturulan hello cihaz kimliğiyle bağlanan bir cihaza benzetim ve hello bulut tarafından adlı toohello yöntemi yanıt bir Node.js uygulaması.</span><span class="sxs-lookup"><span data-stu-id="b5c85-107">**SimulatedDevice.js**, a Node.js app, which simulates a device connecting tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="b5c85-108">Merhaba makale [Azure IOT SDK'ları] [ lnk-hub-sdks] aygıtlar ve çözüm arka ucunuz hem uygulamalar toorun toobuild kullanabileceğiniz hello Azure IOT SDK'ları hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b5c85-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="b5c85-109">toocomplete Bu öğretici, gerekir:</span><span class="sxs-lookup"><span data-stu-id="b5c85-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="b5c85-110">Visual Studio 2015 veya Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="b5c85-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="b5c85-111">Node.js 0.10.x sürümü veya sonraki bir sürüm.</span><span class="sxs-lookup"><span data-stu-id="b5c85-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="b5c85-112">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="b5c85-112">An active Azure account.</span></span> <span data-ttu-id="b5c85-113">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="b5c85-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="b5c85-114">Sanal cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="b5c85-114">Create a simulated device app</span></span>
<span data-ttu-id="b5c85-115">Bu bölümde, hello çözüm tarafından arka uç adlı tooa yöntemi yanıt bir Node.js konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b5c85-115">In this section, you create a Node.js console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="b5c85-116">**simulateddevice** adlı yeni bir boş klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b5c85-116">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="b5c85-117">Merhaba, **simulateddevice** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b5c85-117">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="b5c85-118">Tüm hello Varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="b5c85-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="b5c85-119">Merhaba, komut isteminde **simulateddevice** klasörüne, komut tooinstall hello aşağıdaki hello **azure IOT cihaz** ve **azure-IOT-cihaz-mqtt** paketler:</span><span class="sxs-lookup"><span data-stu-id="b5c85-119">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="b5c85-120">Bir metin düzenleyicisi kullanarak, bir dosya hello oluşturun **simulateddevice** klasörü ve adlandırın **SimulatedDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="b5c85-120">Using a text editor, create a file in hello **simulateddevice** folder and name it **SimulatedDevice.js**.</span></span>
4. <span data-ttu-id="b5c85-121">Merhaba aşağıdakileri ekleyin `require` hello deyimlerini başlatmak hello **SimulatedDevice.js** dosyası:</span><span class="sxs-lookup"><span data-stu-id="b5c85-121">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="b5c85-122">Ekleme bir **connectionString** değişken ve toocreate kullanan bir **DeviceClient** örneği.</span><span class="sxs-lookup"><span data-stu-id="b5c85-122">Add a **connectionString** variable and use it toocreate a **DeviceClient** instance.</span></span> <span data-ttu-id="b5c85-123">Değiştir **{cihaz bağlantı dizesi}** hello oluşturulan hello cihaz bağlantı dizesiyle *bir cihaz kimliği oluşturma* bölümü:</span><span class="sxs-lookup"><span data-stu-id="b5c85-123">Replace **{device connection string}** with hello device connection string you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="b5c85-124">Merhaba aygıtta işlevi tooimplement hello doğrudan yöntemi aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b5c85-124">Add hello following function tooimplement hello direct method on hello device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="b5c85-125">Merhaba bağlantı tooyour IOT hub'ı açın ve hello yöntemi dinleyicisi başlatılamıyor:</span><span class="sxs-lookup"><span data-stu-id="b5c85-125">Open hello connection tooyour IoT hub and initialize hello method listener:</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. <span data-ttu-id="b5c85-126">Kaydet ve Kapat hello **SimulatedDevice.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="b5c85-126">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="b5c85-127">tookeep şeyler basit, Bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="b5c85-127">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="b5c85-128">Üretim kodunda yeniden deneme ilkelerini (bağlantı yeniden deneme), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="b5c85-128">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="b5c85-129">Bir cihazda doğrudan bir yöntem çağrısı</span><span class="sxs-lookup"><span data-stu-id="b5c85-129">Call a direct method on a device</span></span>
<span data-ttu-id="b5c85-130">Bu bölümde, hello sanal cihaz uygulamasının bir yöntemi çağırır ve hello yanıt görüntüleyen bir .NET konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b5c85-130">In this section, you create a .NET console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="b5c85-131">Visual Studio'da hello kullanarak bir Visual C# Windows Klasik Masaüstü projesi toohello geçerli çözüme ekleyin **konsol uygulaması** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="b5c85-131">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="b5c85-132">Merhaba .NET Framework sürümünün 4.5.1 olduğundan emin olun veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="b5c85-132">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="b5c85-133">Ad hello proje **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="b5c85-133">Name hello project **CallMethodOnDevice**.</span></span>
   
    ![Yeni Visual C# Windows Klasik Masaüstü projesi][10]
2. <span data-ttu-id="b5c85-135">Çözüm Gezgini'nde hello sağ **CallMethodOnDevice** proje ve ardından **NuGet paketlerini Yönet...** .</span><span class="sxs-lookup"><span data-stu-id="b5c85-135">In Solution Explorer, right-click hello **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="b5c85-136">Merhaba, **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat**, arama **microsoft.azure.devices**seçin **yükleme** tooinstall Merhaba **Microsoft.Azure.Devices** paketini ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="b5c85-136">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="b5c85-137">Bu yordam indirir, yükler ve başvuru toohello ekler [Azure IOT hizmeti SDK'sını] [ lnk-nuget-service-sdk] NuGet paketi ve bağımlılıklarını.</span><span class="sxs-lookup"><span data-stu-id="b5c85-137">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet Paket Yöneticisi penceresi][11]

4. <span data-ttu-id="b5c85-139">Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:</span><span class="sxs-lookup"><span data-stu-id="b5c85-139">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="b5c85-140">Aşağıdaki alanları toohello hello eklemek **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="b5c85-140">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="b5c85-141">Merhaba hello önceki bölümde oluşturduğunuz hello hub'ın IOT Hub bağlantı dizesine sahip Hello yer tutucu değerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b5c85-141">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="b5c85-142">Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="b5c85-142">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="b5c85-143">Bu yöntem adı ile doğrudan bir yöntem çağırır `writeLine` hello üzerinde `myDeviceId` aygıt.</span><span class="sxs-lookup"><span data-stu-id="b5c85-143">This method invokes a direct method with name `writeLine` on hello `myDeviceId` device.</span></span> <span data-ttu-id="b5c85-144">Ardından, hello konsolunda hello aygıt tarafından sağlanan hello yanıt yazar.</span><span class="sxs-lookup"><span data-stu-id="b5c85-144">Then, it writes hello response provided by hello device on hello console.</span></span> <span data-ttu-id="b5c85-145">Nasıl olası toospecify hello aygıt toorespond için zaman aşımı değeri olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="b5c85-145">Note how it is possible toospecify a timeout value for hello device toorespond.</span></span>
7. <span data-ttu-id="b5c85-146">Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="b5c85-146">Finally, add hello following lines toohello **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

## <a name="run-hello-applications"></a><span data-ttu-id="b5c85-147">Merhaba uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b5c85-147">Run hello applications</span></span>
<span data-ttu-id="b5c85-148">Hazır toorun hello uygulamaları sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="b5c85-148">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="b5c85-149">Buna Visual Studio Çözüm Gezgini Merhaba, çözümünüze sağ tıklayın ve ardından **başlangıç projelerini Ayarla...** . Seçin **tek başlangıç projesi**ve ardından hello **CallMethodOnDevice** hello açılır menüsünde projesinde.</span><span class="sxs-lookup"><span data-stu-id="b5c85-149">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **CallMethodOnDevice** project in hello dropdown menu.</span></span>

2. <span data-ttu-id="b5c85-150">Bir komut isteminde hello **simulateddevice** klasörü, IOT Hub'ınızı gelen yöntem çağrıları için dinleme komutu toostart aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b5c85-150">At a command prompt in hello **simulateddevice** folder, run hello following command toostart listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   <span data-ttu-id="b5c85-151">Benzetimli hello aygıt tooopen bekler:![][7]</span><span class="sxs-lookup"><span data-stu-id="b5c85-151">Wait for hello simulated device tooopen:  ![][7]</span></span>
3. <span data-ttu-id="b5c85-152">Şimdi bu hello cihaz bağlı ve hello .NET çalıştırmak için yöntem çağrılarına bekleniyor, **CallMethodOnDevice** hello sanal cihaz uygulamasının uygulama tooinvoke hello yöntemi.</span><span class="sxs-lookup"><span data-stu-id="b5c85-152">Now that hello device is connected and waiting for method invocations, run hello .NET **CallMethodOnDevice** app tooinvoke hello method in hello simulated device app.</span></span> <span data-ttu-id="b5c85-153">Merhaba konsolunda yazılmış hello aygıt yanıtı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b5c85-153">You should see hello device response written in hello console.</span></span>
   
    ![][8]
4. <span data-ttu-id="b5c85-154">Hello aygıt sonra bu iletiyi yazdırma tarafından toohello yöntemi tepki verir:</span><span class="sxs-lookup"><span data-stu-id="b5c85-154">hello device then reacts toohello method by printing this message:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="b5c85-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b5c85-155">Next steps</span></span>
<span data-ttu-id="b5c85-156">Bu öğreticide hello Azure portalında yeni bir IOT hub yapılandırılmış ve ardından hello IOT hub'ın kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="b5c85-156">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="b5c85-157">Merhaba bulut tarafından çağrılan bu cihaz kimliğini tooenable benzetimli hello aygıt uygulama tooreact toomethods kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b5c85-157">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="b5c85-158">Merhaba aygıtta yöntemleri çağırır ve hello yanıt hello aygıttan görüntüleyen bir uygulama da oluşturmuş.</span><span class="sxs-lookup"><span data-stu-id="b5c85-158">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="b5c85-159">Başlarken toocontinue IOT Hub ve tooexplore diğer IOT senaryolarını bakın:</span><span class="sxs-lookup"><span data-stu-id="b5c85-159">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="b5c85-160">[IOT Hub ile çalışmaya başlama]</span><span class="sxs-lookup"><span data-stu-id="b5c85-160">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="b5c85-161">[Birden çok aygıta işleri zamanla][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="b5c85-161">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="b5c85-162">toolearn tooextend birden fazla cihazda IOT çözümü ve zamanlama yöntemi çağırır nasıl hello bkz [zamanlama ve yayın işleri] [ lnk-tutorial-jobs] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="b5c85-162">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-csharp-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-csharp-node-direct-methods/netserviceapp.png
[9]: ./media/iot-hub-csharp-node-direct-methods/methods-output.png

[10]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp1.png
[11]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp2.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[IOT Hub ile çalışmaya başlama]: iot-hub-node-node-getstarted.md
