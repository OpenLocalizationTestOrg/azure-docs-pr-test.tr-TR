---
title: "aaaGet başlatılan ile Azure IOT Hub cihaz Yönetimi (.NET/düğümü) | Microsoft Docs"
description: "Nasıl toouse Azure IOT Hub cihaz Yönetimi tooinitiate uzaktaki bir aygıtı yeniden başlatın. Node.js tooimplement doğrudan yöntemi ve hello .NET tooimplement hello doğrudan yöntemini çağıran bir hizmet uygulaması için Azure IOT hizmeti SDK'sını içeren sanal cihaz uygulaması için hello Azure IOT cihaz SDK'sını kullanın."
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
ms.openlocfilehash: ea6d50dfac1c222d7836e3bf5503c6c9b8c89dfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-netnode"></a><span data-ttu-id="7cd18-104">Aygıt Yönetimi (.NET/düğümü) ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="7cd18-104">Get started with device management (.NET/Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="7cd18-105">Bu öğretici şunların nasıl yapıldığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="7cd18-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="7cd18-106">IOT hub'ınızda bir cihaz kimliği oluşturma ve Hello Azure portal toocreate IOT hub'ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="7cd18-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="7cd18-107">Bu cihazı yeniden başlatır doğrudan bir yöntem içeren bir sanal cihaz uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="7cd18-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="7cd18-108">Doğrudan yöntemleri hello buluttan çağrılır.</span><span class="sxs-lookup"><span data-stu-id="7cd18-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="7cd18-109">IOT hub'ınız aracılığıyla hello sanal cihaz uygulamasında hello yeniden başlatma doğrudan yöntemini çağıran bir .NET konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7cd18-109">Create a .NET console app that calls hello reboot direct method in hello simulated device app through your IoT hub.</span></span>

<span data-ttu-id="7cd18-110">Bu öğretici Hello sonunda bir Node.js konsol cihaz uygulaması ve bir .NET (C#) konsol arka uç uygulaması sahiptir:</span><span class="sxs-lookup"><span data-stu-id="7cd18-110">At hello end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="7cd18-111">**dmpatterns_getstarted_device.js**, daha önce oluşturduğunuz hello cihaz kimliğiyle IOT hub'ı tooyour bağlayan bir yeniden başlatma doğrudan yöntemi alır fiziksel yeniden başlatma taklit eder ve hello son yeniden başlatma için başlangıç zamanı raporlar.</span><span class="sxs-lookup"><span data-stu-id="7cd18-111">**dmpatterns_getstarted_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports hello time for hello last reboot.</span></span>

<span data-ttu-id="7cd18-112">**TriggerReboot**, doğrudan bir yöntem hello sanal cihaz uygulamada, çağıran hello yanıt görüntüler ve güncelleştirilmiş görüntüler hello rapor özellikleri.</span><span class="sxs-lookup"><span data-stu-id="7cd18-112">**TriggerReboot**, which calls a direct method in hello simulated device app, displays hello response, and displays hello updated reported properties.</span></span>

<span data-ttu-id="7cd18-113">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7cd18-113">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="7cd18-114">Visual Studio 2015 veya Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="7cd18-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="7cd18-115">Node.js sürümünü 0.12.x sürümü veya sonraki bir sürümü</span><span class="sxs-lookup"><span data-stu-id="7cd18-115">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="7cd18-116">[Geliştirme ortamınızı hazırlama] [ lnk-dev-setup] açıklar nasıl tooinstall Node.js Bu öğretici için Windows veya Linux üzerinde.</span><span class="sxs-lookup"><span data-stu-id="7cd18-116">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="7cd18-117">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="7cd18-117">An active Azure account.</span></span> <span data-ttu-id="7cd18-118">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="7cd18-118">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="7cd18-119">Tetikleyici doğrudan bir yöntem kullanarak hello cihazda Uzaktan yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="7cd18-119">Trigger a remote reboot on hello device using a direct method</span></span>
<span data-ttu-id="7cd18-120">Bu bölümde, doğrudan bir yöntem kullanarak bir cihazda Uzaktan yeniden başlatma başlatır (C# kullanarak) bir .NET konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7cd18-120">In this section, you create a .NET console app (using C#) that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="7cd18-121">Merhaba uygulaması bu cihaz için cihaz çifti sorguları toodiscover hello son yeniden başlatma zamanı kullanır.</span><span class="sxs-lookup"><span data-stu-id="7cd18-121">hello app uses device twin queries toodiscover hello last reboot time for that device.</span></span>

1. <span data-ttu-id="7cd18-122">Visual Studio'da hello kullanarak bir Visual C# Windows Klasik Masaüstü projesi tooa yeni çözüm Ekle **konsol uygulaması (.NET Framework)** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="7cd18-122">In Visual Studio, add a Visual C# Windows Classic Desktop project tooa new solution by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="7cd18-123">Merhaba .NET Framework sürümünün 4.5.1 olduğundan emin olun veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="7cd18-123">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="7cd18-124">Ad hello proje **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="7cd18-124">Name hello project **TriggerReboot**.</span></span>

    ![Yeni Visual C# Windows Klasik Masaüstü projesi][img-createapp]

2. <span data-ttu-id="7cd18-126">Çözüm Gezgini'nde hello sağ **TriggerReboot** proje ve ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="7cd18-126">In Solution Explorer, right-click hello **TriggerReboot** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="7cd18-127">Merhaba, **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat**, arama **microsoft.azure.devices**seçin **yükleme** tooinstall Merhaba **Microsoft.Azure.Devices** paketini ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="7cd18-127">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="7cd18-128">Bu yordam indirir, yükler ve başvuru toohello ekler [Azure IOT hizmeti SDK'sını] [ lnk-nuget-service-sdk] NuGet paketi ve bağımlılıklarını.</span><span class="sxs-lookup"><span data-stu-id="7cd18-128">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![NuGet Paket Yöneticisi penceresi][img-servicenuget]
4. <span data-ttu-id="7cd18-130">Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:</span><span class="sxs-lookup"><span data-stu-id="7cd18-130">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
5. <span data-ttu-id="7cd18-131">Aşağıdaki alanları toohello hello eklemek **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="7cd18-131">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="7cd18-132">Merhaba hello önceki bölümde ve hello hedef aygıt oluşturduğunuz hello hub'ın IOT Hub bağlantı dizesine sahip Hello yer tutucu değerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7cd18-132">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section and hello target device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
6. <span data-ttu-id="7cd18-133">Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="7cd18-133">Add hello following method toohello **Program** class.</span></span>  <span data-ttu-id="7cd18-134">Bu kod alır hello cihaz çifti hello cihaz ve çıkışları hello yeniden başlatıldığı için özellikler bildirdi.</span><span class="sxs-lookup"><span data-stu-id="7cd18-134">This code gets hello device twin for hello rebooting device and outputs hello reported properties.</span></span>
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. <span data-ttu-id="7cd18-135">Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="7cd18-135">Add hello following method toohello **Program** class.</span></span>  <span data-ttu-id="7cd18-136">Bu kod, doğrudan bir yöntem kullanarak hello aygıtta hello yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="7cd18-136">This code initiates hello reboot on hello device using a direct method.</span></span>

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. <span data-ttu-id="7cd18-137">Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="7cd18-137">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
8. <span data-ttu-id="7cd18-138">Merhaba çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7cd18-138">Build hello solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="7cd18-139">Sanal cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="7cd18-139">Create a simulated device app</span></span>
<span data-ttu-id="7cd18-140">Bu bölümde şunları yapacaksınız:</span><span class="sxs-lookup"><span data-stu-id="7cd18-140">In this section, you will</span></span>

* <span data-ttu-id="7cd18-141">Merhaba bulut tarafından adlı tooa doğrudan yöntemi yanıt bir Node.js konsol uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="7cd18-141">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="7cd18-142">Tetikleyici sanal cihaz yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="7cd18-142">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="7cd18-143">Özellikler tooenable cihaz çifti sorguları tooidentify aygıtlar ve bunların en son ne zaman yeniden kullanım hello bildirdi</span><span class="sxs-lookup"><span data-stu-id="7cd18-143">Use hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted</span></span>

1. <span data-ttu-id="7cd18-144">Adlı yeni bir boş klasör oluşturun **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="7cd18-144">Create a new empty folder called **manageddevice**.</span></span>  <span data-ttu-id="7cd18-145">Merhaba, **manageddevice** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7cd18-145">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="7cd18-146">Tüm hello Varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="7cd18-146">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="7cd18-147">Merhaba, komut isteminde **manageddevice** klasörüne, komut tooinstall hello aşağıdaki hello **azure IOT cihaz** cihaz SDK'sı paketinin ve **azure-IOT-cihaz-mqtt**paketi:</span><span class="sxs-lookup"><span data-stu-id="7cd18-147">At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="7cd18-148">Bir metin düzenleyicisi kullanarak yeni bir oluşturma **dmpatterns_getstarted_device.js** hello dosyasında **manageddevice** klasör.</span><span class="sxs-lookup"><span data-stu-id="7cd18-148">Using a text editor, create a new **dmpatterns_getstarted_device.js** file in hello **manageddevice** folder.</span></span>
4. <span data-ttu-id="7cd18-149">Merhaba aşağıdaki 'İste' hello hello başlangıç deyimleri ekleme **dmpatterns_getstarted_device.js** dosyası:</span><span class="sxs-lookup"><span data-stu-id="7cd18-149">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="7cd18-150">Ekleme bir **connectionString** değişken ve toocreate kullanan bir **istemci** örneği.</span><span class="sxs-lookup"><span data-stu-id="7cd18-150">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  <span data-ttu-id="7cd18-151">Merhaba bağlantı dizesi, cihaz bağlantı dizesi ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7cd18-151">Replace hello connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="7cd18-152">Merhaba aygıtta işlevi tooimplement hello doğrudan yöntemi aşağıdaki hello ekleme</span><span class="sxs-lookup"><span data-stu-id="7cd18-152">Add hello following function tooimplement hello direct method on hello device</span></span>
   
    ```
    var onReboot = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report hello reboot before hello physical restart
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
7. <span data-ttu-id="7cd18-153">Merhaba aşağıdaki tooopen hello bağlantı tooyour IOT hub'ı kod ve hello doğrudan yöntemi dinleyicisini başlatmak ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7cd18-153">Add hello following code tooopen hello connection tooyour IoT hub and start hello direct method listener:</span></span>
   
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
8. <span data-ttu-id="7cd18-154">Kaydet ve Kapat hello **dmpatterns_getstarted_device.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="7cd18-154">Save and close hello **dmpatterns_getstarted_device.js** file.</span></span>
   
> [!NOTE]
> <span data-ttu-id="7cd18-155">tookeep şeyler basit, Bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="7cd18-155">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="7cd18-156">Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="7cd18-156">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>


## <a name="run-hello-apps"></a><span data-ttu-id="7cd18-157">Merhaba uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7cd18-157">Run hello apps</span></span>
<span data-ttu-id="7cd18-158">Hazır toorun hello uygulamaları sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="7cd18-158">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="7cd18-159">Merhaba hello komut isteminde **manageddevice** klasöründe şunu hello yeniden başlatma doğrudan yöntemi için dinleme komutu toobegin aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7cd18-159">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="7cd18-160">Çalışma hello C# konsol uygulaması **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="7cd18-160">Run hello C# console app **TriggerReboot**.</span></span> <span data-ttu-id="7cd18-161">Sağ hello **TriggerReboot** proje, select **hata ayıklama**ve ardından **başlangıç yeni örnek**.</span><span class="sxs-lookup"><span data-stu-id="7cd18-161">Right-click hello **TriggerReboot** project, select **Debug**, and then select **Start new instance**.</span></span>

3. <span data-ttu-id="7cd18-162">Merhaba aygıt yanıt toohello doğrudan yöntemi hello konsolunda bakın.</span><span class="sxs-lookup"><span data-stu-id="7cd18-162">You see hello device response toohello direct method in hello console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png
[img-servicenuget]: media/iot-hub-csharp-node-device-management-get-started/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-device-management-get-started/createnetapp.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/