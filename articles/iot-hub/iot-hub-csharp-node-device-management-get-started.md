---
title: "Azure IOT Hub cihaz Yönetimi (.NET/düğümü) ile çalışmaya başlama | Microsoft Docs"
description: "Uzak aygıt yeniden başlatma işlemi başlatmak için Azure IOT Hub cihaz yönetimini kullanma Doğrudan bir yöntem ve Azure IOT hizmeti SDK'sını doğrudan yöntemini çağıran bir hizmet uygulaması uygulamak .NET için içeren bir sanal cihaz uygulamasının uygulamak için Azure IOT cihaz SDK'sı Node.js için kullanın."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: e044006d-ffd6-469b-bc63-c182ad066e31
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/17/2016
ms.author: juanpere
ms.openlocfilehash: d97fc5493570985f94c23032c870628d6a089dcd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-device-management-netnode"></a><span data-ttu-id="b7daa-104">Aygıt Yönetimi (.NET/düğümü) ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="b7daa-104">Get started with device management (.NET/Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="b7daa-105">Bu öğretici şunların nasıl yapıldığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="b7daa-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="b7daa-106">IOT hub'ı oluşturun ve IOT hub'ınızda bir cihaz kimliği oluşturma için Azure Portalı'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7daa-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="b7daa-107">Bu cihazı yeniden başlatır doğrudan bir yöntem içeren bir sanal cihaz uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="b7daa-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="b7daa-108">Doğrudan yöntemleri buluttan çağrılır.</span><span class="sxs-lookup"><span data-stu-id="b7daa-108">Direct methods are invoked from the cloud.</span></span>
* <span data-ttu-id="b7daa-109">IOT hub'ınız aracılığıyla sanal cihaz uygulama yeniden başlatma doğrudan yöntemini çağıran bir .NET konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b7daa-109">Create a .NET console app that calls the reboot direct method in the simulated device app through your IoT hub.</span></span>

<span data-ttu-id="b7daa-110">Bu öğreticinin sonunda bir Node.js konsol cihaz uygulaması ve bir .NET (C#) konsol arka uç uygulaması sahiptir:</span><span class="sxs-lookup"><span data-stu-id="b7daa-110">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="b7daa-111">**dmpatterns_getstarted_device.js**, daha önce oluşturulan cihaz kimliğiyle IOT hub'ınızı bağlayan bir yeniden başlatma doğrudan yöntemi alır fiziksel yeniden başlatma taklit eder ve son yeniden başlatma zamanı raporlar.</span><span class="sxs-lookup"><span data-stu-id="b7daa-111">**dmpatterns_getstarted_device.js**, which connects to your IoT hub with the device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports the time for the last reboot.</span></span>

<span data-ttu-id="b7daa-112">**TriggerReboot**, yanıt görüntüler, sanal cihaz uygulamada, doğrudan bir yöntemi çağırır ve görüntüler güncelleştirilmiş rapor özellikleri.</span><span class="sxs-lookup"><span data-stu-id="b7daa-112">**TriggerReboot**, which calls a direct method in the simulated device app, displays the response, and displays the updated reported properties.</span></span>

<span data-ttu-id="b7daa-113">Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="b7daa-113">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="b7daa-114">Visual Studio 2015 veya Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="b7daa-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="b7daa-115">Node.js sürümünü 0.12.x sürümü veya sonraki bir sürümü</span><span class="sxs-lookup"><span data-stu-id="b7daa-115">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="b7daa-116">[Geliştirme ortamınızı hazırlama] [ lnk-dev-setup] Node.js Bu öğretici için Windows veya Linux'ta nasıl yükleneceğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="b7daa-116">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="b7daa-117">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="b7daa-117">An active Azure account.</span></span> <span data-ttu-id="b7daa-118">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="b7daa-118">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a><span data-ttu-id="b7daa-119">Tetikleyici doğrudan bir yöntem kullanarak cihaz üzerinde Uzaktan yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="b7daa-119">Trigger a remote reboot on the device using a direct method</span></span>
<span data-ttu-id="b7daa-120">Bu bölümde, doğrudan bir yöntem kullanarak bir cihazda Uzaktan yeniden başlatma başlatır (C# kullanarak) bir .NET konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b7daa-120">In this section, you create a .NET console app (using C#) that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="b7daa-121">Uygulama cihaz çifti sorguları bu aygıtın son yeniden başlatma zamanını bulmak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="b7daa-121">The app uses device twin queries to discover the last reboot time for that device.</span></span>

1. <span data-ttu-id="b7daa-122">Visual Studio’da **Konsol Uygulaması (.NET Framework)** proje şablonunu kullanarak yeni bir çözüme bir Visual C# Windows Klasik Masaüstü projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b7daa-122">In Visual Studio, add a Visual C# Windows Classic Desktop project to a new solution by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="b7daa-123">.NET Framework sürümünün 4.5.1 veya sonraki bir sürüm olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="b7daa-123">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="b7daa-124">Proje adı **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="b7daa-124">Name the project **TriggerReboot**.</span></span>

    ![Yeni Visual C# Windows Klasik Masaüstü projesi][img-createapp]

2. <span data-ttu-id="b7daa-126">Çözüm Gezgini'nde sağ **TriggerReboot** proje ve ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="b7daa-126">In Solution Explorer, right-click the **TriggerReboot** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="b7daa-127">**NuGet Paket Yöneticisi** penceresinde **Gözat**'ı seçin, **microsoft.azure.devices**'ı aratın, **Microsoft.Azure.Devices** paketini yüklemek için **Yükle**'yi seçin ve kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="b7daa-127">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="b7daa-128">Bu yordam ile [Azure IoT hizmet SDK'sı][lnk-nuget-service-sdk] NuGet paketi ve bağımlılıkları indirilir, yüklenir ve bu pakete bir başvuru eklenir.</span><span class="sxs-lookup"><span data-stu-id="b7daa-128">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![NuGet Paket Yöneticisi penceresi][img-servicenuget]
4. <span data-ttu-id="b7daa-130">Aşağıdaki `using` deyimlerini **Program.cs** dosyasının üst kısmına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b7daa-130">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
5. <span data-ttu-id="b7daa-131">**Program** sınıfına aşağıdaki alanları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b7daa-131">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="b7daa-132">Yer tutucu değerini önceki bölümde ile hedef aygıt oluşturulan hub'ın IOT Hub bağlantı dizesiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b7daa-132">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section and the target device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
6. <span data-ttu-id="b7daa-133">Aşağıdaki yöntemi ekleyin **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="b7daa-133">Add the following method to the **Program** class.</span></span>  <span data-ttu-id="b7daa-134">Bu kod yeniden başlatılan cihaz için cihaz çifti alır ve bildirilen özellikleri çıkarır.</span><span class="sxs-lookup"><span data-stu-id="b7daa-134">This code gets the device twin for the rebooting device and outputs the reported properties.</span></span>
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. <span data-ttu-id="b7daa-135">Aşağıdaki yöntemi ekleyin **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="b7daa-135">Add the following method to the **Program** class.</span></span>  <span data-ttu-id="b7daa-136">Bu kod, doğrudan bir yöntem kullanarak cihazı önyüklemede başlatır.</span><span class="sxs-lookup"><span data-stu-id="b7daa-136">This code initiates the reboot on the device using a direct method.</span></span>

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. <span data-ttu-id="b7daa-137">Son olarak, **Main** yöntemine aşağıdaki satırları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b7daa-137">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
        
8. <span data-ttu-id="b7daa-138">Çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b7daa-138">Build the solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="b7daa-139">Sanal cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="b7daa-139">Create a simulated device app</span></span>
<span data-ttu-id="b7daa-140">Bu bölümde şunları yapacaksınız:</span><span class="sxs-lookup"><span data-stu-id="b7daa-140">In this section, you will</span></span>

* <span data-ttu-id="b7daa-141">Bulut tarafından çağrılan doğrudan bir yönteme yanıt veren bir Node.js konsol uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="b7daa-141">Create a Node.js console app that responds to a direct method called by the cloud</span></span>
* <span data-ttu-id="b7daa-142">Tetikleyici sanal cihaz yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="b7daa-142">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="b7daa-143">Aygıtları ve bunların en son ne zaman yeniden tanımlamak için cihaz çifti sorgular etkinleştirmek için bildirilen özelliklerini kullanın</span><span class="sxs-lookup"><span data-stu-id="b7daa-143">Use the reported properties to enable device twin queries to identify devices and when they last rebooted</span></span>

1. <span data-ttu-id="b7daa-144">Adlı yeni bir boş klasör oluşturun **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="b7daa-144">Create a new empty folder called **manageddevice**.</span></span>  <span data-ttu-id="b7daa-145">Komut isteminizde aşağıdaki komutu kullanarak **manageddevice** klasöründe bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b7daa-145">In the **manageddevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="b7daa-146">Tüm varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="b7daa-146">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="b7daa-147">Komut isteminizde **manageddevice** klasörü yüklemek için aşağıdaki komutu çalıştırın, **azure IOT cihaz** cihaz SDK'sı paketinin ve **azure-IOT-cihaz-mqtt** paketi:</span><span class="sxs-lookup"><span data-stu-id="b7daa-147">At your command prompt in the **manageddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="b7daa-148">Bir metin düzenleyicisi kullanarak yeni bir oluşturma **dmpatterns_getstarted_device.js** dosyasını **manageddevice** klasör.</span><span class="sxs-lookup"><span data-stu-id="b7daa-148">Using a text editor, create a new **dmpatterns_getstarted_device.js** file in the **manageddevice** folder.</span></span>
4. <span data-ttu-id="b7daa-149">Aşağıdaki 'İste' deyimleri başlangıcında eklemek **dmpatterns_getstarted_device.js** dosyası:</span><span class="sxs-lookup"><span data-stu-id="b7daa-149">Add the following 'require' statements at the start of the **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="b7daa-150">Bir **connectionString** değişkeni ekleyin ve bir **İstemci** örneği oluşturmak için bunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7daa-150">Add a **connectionString** variable and use it to create a **Client** instance.</span></span>  <span data-ttu-id="b7daa-151">Bağlantı dizesi, cihaz bağlantı dizesi ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b7daa-151">Replace the connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="b7daa-152">Cihazda doğrudan yöntemi uygulamak için aşağıdaki işlevi ekleyin</span><span class="sxs-lookup"><span data-stu-id="b7daa-152">Add the following function to implement the direct method on the device</span></span>
   
    ```
    var onReboot = function(request, response) {
   
        // Respond the cloud app for the direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report the reboot before the physical restart
        var date = new Date();
        var patch = {
            iothubDM : {
                reboot : {
                    lastReboot : date.toISOString(),
                }
            }
        };
   
        // Get device Twin
        client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                console.log('twin acquired');
                twin.properties.reported.update(patch, function(err) {
                    if (err) throw err;
                    console.log('Device reboot twin state reported')
                });  
            }
        });
   
        // Add your device's reboot API for physical restart.
        console.log('Rebooting!');
    };
    ```
7. <span data-ttu-id="b7daa-153">IOT hub'ınıza bağlantıyı açın ve doğrudan yöntemi dinleyicisini başlatmak için aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b7daa-153">Add the following code to open the connection to your IoT hub and start the direct method listener:</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not open IotHub client');
        }  else {
            console.log('Client opened.  Waiting for reboot method.');
            client.onDeviceMethod('reboot', onReboot);
        }
    });
    ```
8. <span data-ttu-id="b7daa-154">Kaydet ve Kapat **dmpatterns_getstarted_device.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="b7daa-154">Save and close the **dmpatterns_getstarted_device.js** file.</span></span>
   
> [!NOTE]
> <span data-ttu-id="b7daa-155">Sade ve basit bir anlatım gözetildiği için bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="b7daa-155">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="b7daa-156">[Geçici Hata İşleme][lnk-transient-faults] adlı MSDN makalesinde önerildiği üzere, üretim kodunda yeniden deneme ilkelerini (üstel geri alma gibi) uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7daa-156">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>


## <a name="run-the-apps"></a><span data-ttu-id="b7daa-157">Uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b7daa-157">Run the apps</span></span>
<span data-ttu-id="b7daa-158">Şimdi uygulamaları çalıştırmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="b7daa-158">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="b7daa-159">Komut isteminde **manageddevice** klasörü, yeniden başlatma doğrudan yöntemi için dinleme başlamak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b7daa-159">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="b7daa-160">C# konsol uygulaması çalıştırmak **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="b7daa-160">Run the C# console app **TriggerReboot**.</span></span> <span data-ttu-id="b7daa-161">Sağ **TriggerReboot** proje, select **hata ayıklama**ve ardından **başlangıç yeni örnek**.</span><span class="sxs-lookup"><span data-stu-id="b7daa-161">Right-click the **TriggerReboot** project, select **Debug**, and then select **Start new instance**.</span></span>

3. <span data-ttu-id="b7daa-162">Konsolunda doğrudan yöntemi aygıt yanıta bakın.</span><span class="sxs-lookup"><span data-stu-id="b7daa-162">You see the device response to the direct method in the console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png
[img-servicenuget]: media/iot-hub-csharp-node-device-management-get-started/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-device-management-get-started/createnetapp.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups to manage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/