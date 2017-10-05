---
title: "Cihaz üretici yazılımı güncelleştirme ile Azure IOT hub'ı (.NET/düğümü) | Microsoft Docs"
description: "Cihaz Yönetimi Azure IOT hub'ına aygıt üretici yazılımı güncelleştirmesi başlatmak için nasıl kullanılacağını. Sanal cihaz uygulaması ve Azure IOT hizmeti SDK'sını bellenim güncelleştirme tetikleyen bir hizmet uygulaması uygulamak .NET için uygulamak için Azure IOT cihaz SDK'sı Node.js için kullanın."
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
ms.openlocfilehash: c2192328a152e955d182c4a07b391c98a5960964
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-device-management-to-initiate-a-device-firmware-update-netnode"></a><span data-ttu-id="2c062-104">Bir cihaz üretici yazılımı güncelleştirmesi (.NET/düğümü) başlatmak için cihaz Yönetimi'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="2c062-104">Use device management to initiate a device firmware update (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="2c062-105">Giriş</span><span class="sxs-lookup"><span data-stu-id="2c062-105">Introduction</span></span>
<span data-ttu-id="2c062-106">İçinde [aygıt Management'i kullanmaya başlama] [ lnk-dm-getstarted] Öğreticisi, nasıl kullanılacağını gördüğünüz [cihaz çifti] [ lnk-devtwin] ve [doğrudan yöntemleri ] [ lnk-c2dmethod] temelleri uzaktan bir aygıt yeniden başlatma.</span><span class="sxs-lookup"><span data-stu-id="2c062-106">In the [Get started with device management][lnk-dm-getstarted] tutorial, you saw how to use the [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives to remotely reboot a device.</span></span> <span data-ttu-id="2c062-107">Bu öğretici aynı IOT hub'ı temelleri kullanır ve bir uçtan uca sanal üretici yazılımı güncelleştirme yapmak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="2c062-107">This tutorial uses the same IoT Hub primitives and shows you how to do an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="2c062-108">Bu desen bellenim güncelleştirme uygulaması için kullanılan [Raspberry Pi'yi cihaz uygulaması örnek][lnk-rpi-implementation].</span><span class="sxs-lookup"><span data-stu-id="2c062-108">This pattern is used in the firmware update implementation for the [Raspberry Pi device implementation sample][lnk-rpi-implementation].</span></span>

<span data-ttu-id="2c062-109">Bu öğretici şunların nasıl yapıldığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="2c062-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="2c062-110">IOT hub'ınız aracılığıyla sanal cihaz uygulamasında firmwareUpdate doğrudan yöntemini çağıran bir .NET konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2c062-110">Create a .NET console app that calls the firmwareUpdate direct method in the simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="2c062-111">Arabirimini uygulayan bir sanal cihaz uygulaması oluşturma bir **firmwareUpdate** doğrudan yöntemi.</span><span class="sxs-lookup"><span data-stu-id="2c062-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="2c062-112">Bu yöntem bellenim görüntüsünü karşıdan yüklemek için bekleyeceği, bellenim görüntüyü indirir ve son bellenim görüntü geçerli bir çok aşama işlemi başlatır.</span><span class="sxs-lookup"><span data-stu-id="2c062-112">This method initiates a multi-stage process that waits to download the firmware image, downloads the firmware image, and finally applies the firmware image.</span></span> <span data-ttu-id="2c062-113">Güncelleştirme her aşaması sırasında aygıt ilerlemesini bildirmek için bildirilen özelliklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="2c062-113">During each stage of the update, the device uses the reported properties to report on progress.</span></span>

<span data-ttu-id="2c062-114">Bu öğreticinin sonunda bir Node.js konsol cihaz uygulaması ve bir .NET (C#) konsol arka uç uygulaması sahiptir:</span><span class="sxs-lookup"><span data-stu-id="2c062-114">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="2c062-115">**dmpatterns_fwupdate_service.js**yanıt görüntüler, sanal cihaz uygulamada, doğrudan bir yöntemi çağırır ve düzenli aralıklarla (her 500ms) görüntüler güncelleştirilmiş bildirilen özellikleri.</span><span class="sxs-lookup"><span data-stu-id="2c062-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in the simulated device app, displays the response, and periodically (every 500ms) displays the updated reported properties.</span></span>

<span data-ttu-id="2c062-116">**TriggerFWUpdate**, daha önce oluşturulan cihaz kimliğiyle IOT hub'ınızı bağlayan firmwareUpdate doğrudan bir yöntem alır, bellenim güncelleştirme dahil benzetimini yapmak için çok durumlu bir işlem çalışır: görüntü yükleme bekleniyor Yeni görüntüyü indirme ve son görüntü uygulama.</span><span class="sxs-lookup"><span data-stu-id="2c062-116">**TriggerFWUpdate**, which connects to your IoT hub with the device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process to simulate a firmware update including: waiting for the image download, downloading the new image, and finally applying the image.</span></span>

<span data-ttu-id="2c062-117">Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="2c062-117">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="2c062-118">Visual Studio 2015 veya Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="2c062-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="2c062-119">Node.js sürümünü 0.12.x sürümü veya sonraki bir sürümü</span><span class="sxs-lookup"><span data-stu-id="2c062-119">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="2c062-120">[Geliştirme ortamınızı hazırlama] [ lnk-dev-setup] Node.js Bu öğretici için Windows veya Linux'ta nasıl yükleneceğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="2c062-120">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="2c062-121">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="2c062-121">An active Azure account.</span></span> <span data-ttu-id="2c062-122">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="2c062-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="2c062-123">İzleyin [aygıt Management'i kullanmaya başlama](iot-hub-csharp-node-device-management-get-started.md) IOT hub'ınızı oluşturun ve IOT Hub bağlantı dizenizi almak için makale.</span><span class="sxs-lookup"><span data-stu-id="2c062-123">Follow the [Get started with device management](iot-hub-csharp-node-device-management-get-started.md) article to create your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-the-device-using-a-direct-method"></a><span data-ttu-id="2c062-124">Doğrudan bir yöntem kullanarak aygıt bir uzak bellenim güncelleştirme Tetikle</span><span class="sxs-lookup"><span data-stu-id="2c062-124">Trigger a remote firmware update on the device using a direct method</span></span>
<span data-ttu-id="2c062-125">Bu bölümde, bir cihazda uzaktan yazılımı güncelleştirmesi başlatır (C# kullanarak) bir .NET konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2c062-125">In this section, you create a .NET console app (using C#) that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="2c062-126">Uygulama güncelleştirme başlatmak için doğrudan bir yöntem kullanır ve etkin bellenim güncelleştirme durumunu düzenli aralıklarla almak için cihaz çifti sorgularını kullanır.</span><span class="sxs-lookup"><span data-stu-id="2c062-126">The app uses a direct method to initiate the update and uses device twin queries to periodically get the status of the active firmware update.</span></span>

1. <span data-ttu-id="2c062-127">Visual Studio'da **Konsol Uygulaması** proje şablonunu kullanarak geçerli çözüme bir Visual C# Windows Klasik Masaüstü projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2c062-127">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="2c062-128">Proje adı **TriggerFWUpdate**.</span><span class="sxs-lookup"><span data-stu-id="2c062-128">Name the project **TriggerFWUpdate**.</span></span>

    ![Yeni Visual C# Windows Klasik Masaüstü projesi][img-createapp]

1. <span data-ttu-id="2c062-130">Çözüm Gezgini'nde sağ **TriggerFWUpdate** proje ve ardından **NuGet paketlerini Yönet...** .</span><span class="sxs-lookup"><span data-stu-id="2c062-130">In Solution Explorer, right-click the **TriggerFWUpdate** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="2c062-131">**NuGet Paket Yöneticisi** penceresinde **Gözat**'ı seçin, **microsoft.azure.devices**'ı aratın, **Microsoft.Azure.Devices** paketini yüklemek için **Yükle**'yi seçin ve kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="2c062-131">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="2c062-132">Bu yordam ile [Azure IoT hizmet SDK'sı][lnk-nuget-service-sdk] NuGet paketi ve bağımlılıkları indirilir, yüklenir ve bu pakete bir başvuru eklenir.</span><span class="sxs-lookup"><span data-stu-id="2c062-132">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![NuGet Paket Yöneticisi penceresi][img-servicenuget]
1. <span data-ttu-id="2c062-134">Aşağıdaki `using` deyimlerini **Program.cs** dosyasının üst kısmına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2c062-134">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. <span data-ttu-id="2c062-135">**Program** sınıfına aşağıdaki alanları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2c062-135">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="2c062-136">Birden çok yer tutucu değerlerini önceki bölümde ve Cihazınızı kimliğini oluşturulan hub'ın IOT Hub bağlantı dizesiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2c062-136">Replace the multiple placeholder values with the IoT Hub connection string for the hub that you created in the previous section and the Id of your device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. <span data-ttu-id="2c062-137">**Program** sınıfına aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2c062-137">Add the following method to the **Program** class:</span></span>
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. <span data-ttu-id="2c062-138">**Program** sınıfına aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2c062-138">Add the following method to the **Program** class:</span></span>

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

1. <span data-ttu-id="2c062-139">Son olarak, **Main** yöntemine aşağıdaki satırları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2c062-139">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
        
1. <span data-ttu-id="2c062-140">Çözüm Gezgini'nde açık **başlangıç projelerini Ayarla...**  ve emin olun **eylem** için **TriggerFWUpdate** projedir **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="2c062-140">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **TriggerFWUpdate** project is **Start**.</span></span>

1. <span data-ttu-id="2c062-141">Çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2c062-141">Build the solution.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-the-apps"></a><span data-ttu-id="2c062-142">Uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="2c062-142">Run the apps</span></span>
<span data-ttu-id="2c062-143">Şimdi uygulamaları çalıştırmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="2c062-143">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="2c062-144">Komut isteminde **manageddevice** klasörü, yeniden başlatma doğrudan yöntemi için dinleme başlamak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2c062-144">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="2c062-145">Visual Studio'da sağ **TriggerFWUpdate** C# konsol uygulaması, projectRun seçin **hata ayıklama** ve **başlangıç yeni örnek**.</span><span class="sxs-lookup"><span data-stu-id="2c062-145">In Visual Studio, right-click on the **TriggerFWUpdate** projectRun to the C# console app, select **Debug** and **Start new instance**.</span></span>

3. <span data-ttu-id="2c062-146">Konsolunda doğrudan yöntemi aygıt yanıta bakın.</span><span class="sxs-lookup"><span data-stu-id="2c062-146">You see the device response to the direct method in the console.</span></span>

    ![Bellenim başarıyla güncelleştirildi][img-fwupdate]

## <a name="next-steps"></a><span data-ttu-id="2c062-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2c062-148">Next steps</span></span>
<span data-ttu-id="2c062-149">Bu öğreticide, doğrudan bir yöntem bir cihazda uzaktan Bellenim güncelleştirmesini tetiklemek için bildirilen özellikleri bellenim güncelleştirme durumunu izlemek için kullanılır ve.</span><span class="sxs-lookup"><span data-stu-id="2c062-149">In this tutorial, you used a direct method to trigger a remote firmware update on a device and used the reported properties to follow the progress of the firmware update.</span></span>

<span data-ttu-id="2c062-150">Çözüm ve zamanlama yöntemini çağıran birden fazla cihazda, IOT genişletmek öğrenmek için bkz: [zamanlama ve yayın işleri] [ lnk-tutorial-jobs] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="2c062-150">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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