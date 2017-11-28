---
title: "Azure IOT hub'ı (.NET/düğümü) aaaDevice ürün yazılımı güncelleştirmesini | Microsoft Docs"
description: "Azure IOT Hub tooinitiate cihaz üretici yazılımı toouse cihaz yönetimini nasıl güncelleştirin. Node.js tooimplement sanal cihaz uygulaması için hello Azure IOT cihaz SDK'sı ve hello .NET tooimplement hello bellenim güncelleştirme tetikleyen bir hizmet uygulaması için Azure IOT hizmeti SDK'sını kullanın."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/17/2017
ms.author: juanpere
ms.openlocfilehash: d48899651bcd5d67e577c971be0f9453c8f21592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-netnode"></a><span data-ttu-id="83400-104">Aygıt Yönetimi tooinitiate aygıt üretici yazılımı güncelleştirmesi (.NET/düğüm) kullanın</span><span class="sxs-lookup"><span data-stu-id="83400-104">Use device management tooinitiate a device firmware update (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="83400-105">Giriş</span><span class="sxs-lookup"><span data-stu-id="83400-105">Introduction</span></span>
<span data-ttu-id="83400-106">Merhaba, [aygıt Management'i kullanmaya başlama] [ lnk-dm-getstarted] öğretici, gördüğünüz nasıl toouse hello [cihaz çifti] [ lnk-devtwin] ve [doğrudan yöntemleri] [ lnk-c2dmethod] temelleri tooremotely bir aygıtı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="83400-106">In hello [Get started with device management][lnk-dm-getstarted] tutorial, you saw how toouse hello [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives tooremotely reboot a device.</span></span> <span data-ttu-id="83400-107">Bu öğretici kullandığı aynı IOT hub'ı temelleri hello ve nasıl toodo bir uçtan uca bellenim güncelleştirme benzetimli gösterir.</span><span class="sxs-lookup"><span data-stu-id="83400-107">This tutorial uses hello same IoT Hub primitives and shows you how toodo an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="83400-108">Bu desen Merhaba hello bellenim güncelleştirme uygulamasında kullanılan [Raspberry Pi'yi cihaz uygulaması örnek][lnk-rpi-implementation].</span><span class="sxs-lookup"><span data-stu-id="83400-108">This pattern is used in hello firmware update implementation for hello [Raspberry Pi device implementation sample][lnk-rpi-implementation].</span></span>

<span data-ttu-id="83400-109">Bu öğretici şunların nasıl yapıldığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="83400-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="83400-110">IOT hub'ınız aracılığıyla hello sanal cihaz uygulamasında hello firmwareUpdate doğrudan yöntemini çağıran bir .NET konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="83400-110">Create a .NET console app that calls hello firmwareUpdate direct method in hello simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="83400-111">Arabirimini uygulayan bir sanal cihaz uygulaması oluşturma bir **firmwareUpdate** doğrudan yöntemi.</span><span class="sxs-lookup"><span data-stu-id="83400-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="83400-112">Bu yöntem, toodownload hello bellenim görüntü bekler, hello bellenim görüntüyü indirir ve son olarak hello bellenim görüntü geçerlidir bir çok aşama işlemi başlatır.</span><span class="sxs-lookup"><span data-stu-id="83400-112">This method initiates a multi-stage process that waits toodownload hello firmware image, downloads hello firmware image, and finally applies hello firmware image.</span></span> <span data-ttu-id="83400-113">Merhaba güncelleştirme her aşaması sırasında hello aygıt kullanır hello ilerlemeyi özellikleri tooreport bildirdi.</span><span class="sxs-lookup"><span data-stu-id="83400-113">During each stage of hello update, hello device uses hello reported properties tooreport on progress.</span></span>

<span data-ttu-id="83400-114">Bu öğretici Hello sonunda bir Node.js konsol cihaz uygulaması ve bir .NET (C#) konsol arka uç uygulaması sahiptir:</span><span class="sxs-lookup"><span data-stu-id="83400-114">At hello end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="83400-115">**dmpatterns_fwupdate_service.js**hello sanal cihaz uygulamada, doğrudan bir yöntem çağıran görüntüler hello yanıt ve düzenli aralıklarla (her 500ms) güncelleştirilmiş görüntüler hello bildirilen özellikleri.</span><span class="sxs-lookup"><span data-stu-id="83400-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in hello simulated device app, displays hello response, and periodically (every 500ms) displays hello updated reported properties.</span></span>

<span data-ttu-id="83400-116">**TriggerFWUpdate**, daha önce oluşturduğunuz hello cihaz kimliğiyle IOT hub'ı tooyour bağlayan firmwareUpdate doğrudan bir yöntem alır, bellenim güncelleştirme dahil çok durumlu işlem toosimulate çalıştırır: hello görüntü yükleme bekleniyor Merhaba yeni görüntüsü ve son olarak uygulanan hello görüntüsü yükleniyor.</span><span class="sxs-lookup"><span data-stu-id="83400-116">**TriggerFWUpdate**, which connects tooyour IoT hub with hello device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process toosimulate a firmware update including: waiting for hello image download, downloading hello new image, and finally applying hello image.</span></span>

<span data-ttu-id="83400-117">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="83400-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="83400-118">Visual Studio 2015 veya Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="83400-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="83400-119">Node.js sürümünü 0.12.x sürümü veya sonraki bir sürümü</span><span class="sxs-lookup"><span data-stu-id="83400-119">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="83400-120">[Geliştirme ortamınızı hazırlama] [ lnk-dev-setup] açıklar nasıl tooinstall Node.js Bu öğretici için Windows veya Linux üzerinde.</span><span class="sxs-lookup"><span data-stu-id="83400-120">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="83400-121">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="83400-121">An active Azure account.</span></span> <span data-ttu-id="83400-122">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="83400-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="83400-123">Merhaba izleyin [aygıt Management'i kullanmaya başlama](iot-hub-csharp-node-device-management-get-started.md) toocreate IOT hub'ınızı makalesi ve IOT Hub bağlantı dizenizi alın.</span><span class="sxs-lookup"><span data-stu-id="83400-123">Follow hello [Get started with device management](iot-hub-csharp-node-device-management-get-started.md) article toocreate your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a><span data-ttu-id="83400-124">Merhaba cihaz doğrudan bir yöntem kullanarak bir uzak bellenim güncelleştirme Tetikle</span><span class="sxs-lookup"><span data-stu-id="83400-124">Trigger a remote firmware update on hello device using a direct method</span></span>
<span data-ttu-id="83400-125">Bu bölümde, bir cihazda uzaktan yazılımı güncelleştirmesi başlatır (C# kullanarak) bir .NET konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="83400-125">In this section, you create a .NET console app (using C#) that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="83400-126">doğrudan yöntemi tooinitiate hello güncelleştirmesi Hello uygulamanın kullandığı ve kullandığı cihaz çifti sorguları tooperiodically hello hello etkin bellenim güncelleştirme durumunu alın.</span><span class="sxs-lookup"><span data-stu-id="83400-126">hello app uses a direct method tooinitiate hello update and uses device twin queries tooperiodically get hello status of hello active firmware update.</span></span>

1. <span data-ttu-id="83400-127">Visual Studio'da hello kullanarak bir Visual C# Windows Klasik Masaüstü projesi toohello geçerli çözüme ekleyin **konsol uygulaması** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="83400-127">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="83400-128">Ad hello proje **TriggerFWUpdate**.</span><span class="sxs-lookup"><span data-stu-id="83400-128">Name hello project **TriggerFWUpdate**.</span></span>

    ![Yeni Visual C# Windows Klasik Masaüstü projesi][img-createapp]

1. <span data-ttu-id="83400-130">Çözüm Gezgini'nde hello sağ **TriggerFWUpdate** proje ve ardından **NuGet paketlerini Yönet...** .</span><span class="sxs-lookup"><span data-stu-id="83400-130">In Solution Explorer, right-click hello **TriggerFWUpdate** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="83400-131">Merhaba, **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat**, arama **microsoft.azure.devices**seçin **yükleme** tooinstall Merhaba **Microsoft.Azure.Devices** paketini ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="83400-131">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="83400-132">Bu yordam indirir, yükler ve başvuru toohello ekler [Azure IOT hizmeti SDK'sını] [ lnk-nuget-service-sdk] NuGet paketi ve bağımlılıklarını.</span><span class="sxs-lookup"><span data-stu-id="83400-132">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![NuGet Paket Yöneticisi penceresi][img-servicenuget]
1. <span data-ttu-id="83400-134">Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:</span><span class="sxs-lookup"><span data-stu-id="83400-134">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. <span data-ttu-id="83400-135">Aşağıdaki alanları toohello hello eklemek **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="83400-135">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="83400-136">Merhaba önceki bölümde oluşturduğunuz hello hub'ın IOT Hub bağlantı dizesine sahip birden çok yer tutucu değerlerini hello hello ve hello Cihazınızı kimliğini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="83400-136">Replace hello multiple placeholder values with hello IoT Hub connection string for hello hub that you created in hello previous section and hello Id of your device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. <span data-ttu-id="83400-137">Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="83400-137">Add hello following method toohello **Program** class:</span></span>
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. <span data-ttu-id="83400-138">Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="83400-138">Add hello following method toohello **Program** class:</span></span>

        public static async Task StartFirmwareUpdate()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("firmwareUpdate");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);
            method.SetPayloadJson(
                @"{
                    fwPackageUri : 'https://someurl'
                }");

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

1. <span data-ttu-id="83400-139">Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="83400-139">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
1. <span data-ttu-id="83400-140">Merhaba Hello Çözüm Gezgini, açık **başlangıç projelerini Ayarla...**  ve emin hello **eylem** için **TriggerFWUpdate** projedir **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="83400-140">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **TriggerFWUpdate** project is **Start**.</span></span>

1. <span data-ttu-id="83400-141">Merhaba çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="83400-141">Build hello solution.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a><span data-ttu-id="83400-142">Merhaba uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="83400-142">Run hello apps</span></span>
<span data-ttu-id="83400-143">Hazır toorun hello uygulamaları sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="83400-143">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="83400-144">Merhaba hello komut isteminde **manageddevice** klasöründe şunu hello yeniden başlatma doğrudan yöntemi için dinleme komutu toobegin aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="83400-144">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="83400-145">Visual Studio'da hello üzerinde sağ **TriggerFWUpdate** projectRun toohello C# konsol uygulaması, select **hata ayıklama** ve **başlangıç yeni örnek**.</span><span class="sxs-lookup"><span data-stu-id="83400-145">In Visual Studio, right-click on hello **TriggerFWUpdate** projectRun toohello C# console app, select **Debug** and **Start new instance**.</span></span>

3. <span data-ttu-id="83400-146">Merhaba aygıt yanıt toohello doğrudan yöntemi hello konsolunda bakın.</span><span class="sxs-lookup"><span data-stu-id="83400-146">You see hello device response toohello direct method in hello console.</span></span>

    ![Bellenim başarıyla güncelleştirildi][img-fwupdate]

## <a name="next-steps"></a><span data-ttu-id="83400-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="83400-148">Next steps</span></span>
<span data-ttu-id="83400-149">Bu öğreticide kullandığınız doğrudan yöntemi tootrigger uzak bir cihaz ve kullanılan hello bellenim güncelleştirme özellikleri toofollow hello hello bellenim güncelleştirme ilerlemesini bildirdi.</span><span class="sxs-lookup"><span data-stu-id="83400-149">In this tutorial, you used a direct method tootrigger a remote firmware update on a device and used hello reported properties toofollow hello progress of hello firmware update.</span></span>

<span data-ttu-id="83400-150">toolearn tooextend birden fazla cihazda IOT çözümü ve zamanlama yöntemi çağırır nasıl hello bkz [zamanlama ve yayın işleri] [ lnk-tutorial-jobs] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="83400-150">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-firmware-update/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-firmware-update/createnetapp.png
[img-fwupdate]: media/iot-hub-csharp-node-firmware-update/fwupdated.png

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-rpi-implementation]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt_dm/pi_device
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/