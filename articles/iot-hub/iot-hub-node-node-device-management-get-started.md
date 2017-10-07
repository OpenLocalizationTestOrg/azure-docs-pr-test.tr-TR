---
title: "aaaGet başlatılan ile Azure IOT Hub cihaz Yönetimi (düğüm) | Microsoft Docs"
description: "Nasıl toouse IOT Hub cihaz Yönetimi tooinitiate uzaktaki bir aygıtı yeniden başlatın. Doğrudan bir yöntem içeren bir sanal cihaz uygulamasının ve hello doğrudan yöntemini çağıran bir hizmet uygulaması için Node.js tooimplement hello Azure IOT SDK'sını kullanın."
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
ms.date: 08/25/2017
ms.author: juanpere
ms.openlocfilehash: 5dd1878e71231850fb95f4170b823f1e86c3ee83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-node"></a><span data-ttu-id="b7734-104">Aygıt Yönetimi (düğüm) ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="b7734-104">Get started with device management (Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="b7734-105">Bu öğretici şunların nasıl yapıldığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="b7734-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="b7734-106">IOT hub'ınızda bir cihaz kimliği oluşturma ve Hello Azure portal toocreate IOT hub'ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7734-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="b7734-107">Bu cihazı yeniden başlatır doğrudan bir yöntem içeren bir sanal cihaz uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="b7734-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="b7734-108">Doğrudan yöntemleri hello buluttan çağrılır.</span><span class="sxs-lookup"><span data-stu-id="b7734-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="b7734-109">IOT hub'ınız aracılığıyla hello sanal cihaz uygulamasında hello yeniden başlatma doğrudan yöntemini çağıran bir Node.js konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b7734-109">Create a Node.js console app that calls hello reboot direct method in hello simulated device app through your IoT hub.</span></span>

<span data-ttu-id="b7734-110">Bu öğreticinin Hello sonunda, iki Node.js konsol uygulamaları vardır:</span><span class="sxs-lookup"><span data-stu-id="b7734-110">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="b7734-111">**dmpatterns_getstarted_device.js**, daha önce oluşturduğunuz hello cihaz kimliğiyle IOT hub'ı tooyour bağlayan bir yeniden başlatma doğrudan yöntemi alır fiziksel yeniden başlatma taklit eder ve hello son yeniden başlatma için başlangıç zamanı raporlar.</span><span class="sxs-lookup"><span data-stu-id="b7734-111">**dmpatterns_getstarted_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports hello time for hello last reboot.</span></span>

<span data-ttu-id="b7734-112">**dmpatterns_getstarted_service.js**, doğrudan bir yöntem hello sanal cihaz uygulamada, çağıran hello yanıt görüntüler ve güncelleştirilmiş görüntüler hello rapor özellikleri.</span><span class="sxs-lookup"><span data-stu-id="b7734-112">**dmpatterns_getstarted_service.js**, which calls a direct method in hello simulated device app, displays hello response, and displays hello updated reported properties.</span></span>

<span data-ttu-id="b7734-113">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="b7734-113">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="b7734-114">Node.js sürümünü 0.12.x sürümü veya sonraki bir sürümü</span><span class="sxs-lookup"><span data-stu-id="b7734-114">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="b7734-115">[Geliştirme ortamınızı hazırlama] [ lnk-dev-setup] açıklar nasıl tooinstall Node.js Bu öğretici için Windows veya Linux üzerinde.</span><span class="sxs-lookup"><span data-stu-id="b7734-115">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="b7734-116">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="b7734-116">An active Azure account.</span></span> <span data-ttu-id="b7734-117">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="b7734-117">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="b7734-118">Sanal cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="b7734-118">Create a simulated device app</span></span>
<span data-ttu-id="b7734-119">Bu bölümde şunları yapacaksınız:</span><span class="sxs-lookup"><span data-stu-id="b7734-119">In this section, you will</span></span>

* <span data-ttu-id="b7734-120">Merhaba bulut tarafından adlı tooa doğrudan yöntemi yanıt bir Node.js konsol uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="b7734-120">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="b7734-121">Tetikleyici sanal cihaz yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="b7734-121">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="b7734-122">Özellikler tooenable cihaz çifti sorguları tooidentify aygıtlar ve bunların en son ne zaman yeniden kullanım hello bildirdi</span><span class="sxs-lookup"><span data-stu-id="b7734-122">Use hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted</span></span>

1. <span data-ttu-id="b7734-123">**manageddevice** adlı boş bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b7734-123">Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="b7734-124">Merhaba, **manageddevice** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b7734-124">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="b7734-125">Tüm hello Varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="b7734-125">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="b7734-126">Merhaba, komut isteminde **manageddevice** klasörüne, komut tooinstall hello aşağıdaki hello **azure IOT cihaz** cihaz SDK'sı paketinin ve **azure-IOT-cihaz-mqtt**paketi:</span><span class="sxs-lookup"><span data-stu-id="b7734-126">At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="b7734-127">Bir metin düzenleyicisi kullanarak oluşturduğunuz bir **dmpatterns_getstarted_device.js** hello dosyasında **manageddevice** klasör.</span><span class="sxs-lookup"><span data-stu-id="b7734-127">Using a text editor, create a **dmpatterns_getstarted_device.js** file in hello **manageddevice** folder.</span></span>
4. <span data-ttu-id="b7734-128">Merhaba aşağıdaki 'İste' hello hello başlangıç deyimleri ekleme **dmpatterns_getstarted_device.js** dosyası:</span><span class="sxs-lookup"><span data-stu-id="b7734-128">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="b7734-129">Ekleme bir **connectionString** değişken ve toocreate kullanan bir **istemci** örneği.</span><span class="sxs-lookup"><span data-stu-id="b7734-129">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  <span data-ttu-id="b7734-130">Merhaba bağlantı dizesi, cihaz bağlantı dizesi ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b7734-130">Replace hello connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="b7734-131">Merhaba aygıtta işlevi tooimplement hello doğrudan yöntemi aşağıdaki hello ekleme</span><span class="sxs-lookup"><span data-stu-id="b7734-131">Add hello following function tooimplement hello direct method on hello device</span></span>
   
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
7. <span data-ttu-id="b7734-132">Merhaba bağlantı tooyour IOT hub'ı açın ve hello doğrudan yöntemi dinleyicisi başlayın:</span><span class="sxs-lookup"><span data-stu-id="b7734-132">Open hello connection tooyour IoT hub and start hello direct method listener:</span></span>
   
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
8. <span data-ttu-id="b7734-133">Kaydet ve Kapat hello **dmpatterns_getstarted_device.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="b7734-133">Save and close hello **dmpatterns_getstarted_device.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="b7734-134">tookeep şeyler basit, Bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="b7734-134">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="b7734-135">Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="b7734-135">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="b7734-136">Tetikleyici doğrudan bir yöntem kullanarak hello cihazda Uzaktan yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="b7734-136">Trigger a remote reboot on hello device using a direct method</span></span>
<span data-ttu-id="b7734-137">Bu bölümde, doğrudan bir yöntem kullanarak bir cihazda Uzaktan yeniden başlatma başlatan bir Node.js konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b7734-137">In this section, you create a Node.js console app that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="b7734-138">Merhaba uygulaması bu cihaz için cihaz çifti sorguları toodiscover hello son yeniden başlatma zamanı kullanır.</span><span class="sxs-lookup"><span data-stu-id="b7734-138">hello app uses device twin queries toodiscover hello last reboot time for that device.</span></span>

1. <span data-ttu-id="b7734-139">Adlı bir boş klasör oluşturun **triggerrebootondevice**.</span><span class="sxs-lookup"><span data-stu-id="b7734-139">Create an empty folder called **triggerrebootondevice**.</span></span>  <span data-ttu-id="b7734-140">Merhaba, **triggerrebootondevice** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b7734-140">In hello **triggerrebootondevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="b7734-141">Tüm hello Varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="b7734-141">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="b7734-142">Merhaba, komut isteminde **triggerrebootondevice** klasörüne, komut tooinstall hello aşağıdaki hello **azure-iothub** cihaz SDK'sı paketinin ve **azure-IOT-cihaz-mqtt** paketi:</span><span class="sxs-lookup"><span data-stu-id="b7734-142">At your command prompt in hello **triggerrebootondevice** folder, run hello following command tooinstall hello **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="b7734-143">Bir metin düzenleyicisi kullanarak oluşturduğunuz bir **dmpatterns_getstarted_service.js** hello dosyasında **triggerrebootondevice** klasör.</span><span class="sxs-lookup"><span data-stu-id="b7734-143">Using a text editor, create a **dmpatterns_getstarted_service.js** file in hello **triggerrebootondevice** folder.</span></span>
4. <span data-ttu-id="b7734-144">Merhaba aşağıdaki 'İste' hello hello başlangıç deyimleri ekleme **dmpatterns_getstarted_service.js** dosyası:</span><span class="sxs-lookup"><span data-stu-id="b7734-144">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="b7734-145">Değişken bildirimleri aşağıdaki hello ekleyin ve hello yer tutucu değerlerini değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b7734-145">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. <span data-ttu-id="b7734-146">İşlev tooinvoke hello aygıt yöntemi tooreboot hello hedef aygıt aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b7734-146">Add hello following function tooinvoke hello device method tooreboot hello target device:</span></span>
   
    ```
    var startRebootDevice = function(twin) {
   
        var methodName = "reboot";
   
        var methodParams = {
            methodName: methodName,
            payload: null,
            timeoutInSeconds: 30
        };
   
        client.invokeDeviceMethod(deviceToReboot, methodParams, function(err, result) {
            if (err) { 
                console.error("Direct method error: "+err.message);
            } else {
                console.log("Successfully invoked hello device tooreboot.");  
            }
        });
    };
    ```
7. <span data-ttu-id="b7734-147">Merhaba aşağıdaki tooquery hello cihaz için işlev ve hello son yeniden başlatma zamanı alma ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b7734-147">Add hello following function tooquery for hello device and get hello last reboot time:</span></span>
   
    ```
    var queryTwinLastReboot = function() {
   
        registry.getTwin(deviceToReboot, function(err, twin){
   
            if (twin.properties.reported.iothubDM != null)
            {
                if (err) {
                    console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
                } else {
                    var lastRebootTime = twin.properties.reported.iothubDM.reboot.lastReboot;
                    console.log('Last reboot time: ' + JSON.stringify(lastRebootTime, null, 2));
                }
            } else 
                console.log('Waiting for device tooreport last reboot time.');
        });
    };
    ```
8. <span data-ttu-id="b7734-148">Merhaba tetiklemek kod toocall hello işlevleri aşağıdaki hello doğrudan yöntemi yeniden başlatın ve sorgu hello için son zaman yeniden ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b7734-148">Add hello following code toocall hello functions that trigger hello reboot direct method and query for hello last reboot time:</span></span>
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. <span data-ttu-id="b7734-149">Kaydet ve Kapat hello **dmpatterns_getstarted_service.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="b7734-149">Save and close hello **dmpatterns_getstarted_service.js** file.</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="b7734-150">Merhaba uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b7734-150">Run hello apps</span></span>
<span data-ttu-id="b7734-151">Hazır toorun hello uygulamaları sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="b7734-151">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="b7734-152">Merhaba hello komut isteminde **manageddevice** klasöründe şunu hello yeniden başlatma doğrudan yöntemi için dinleme komutu toobegin aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b7734-152">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="b7734-153">Merhaba hello komut isteminde **triggerrebootondevice** komutu tootrigger hello uzaktan aşağıdaki hello Çalıştır klasörü yeniden başlatın ve hello cihaz çifti toofind hello en son yeniden başlatma için zaman sorgu.</span><span class="sxs-lookup"><span data-stu-id="b7734-153">At hello command prompt in hello **triggerrebootondevice** folder, run hello following command tootrigger hello remote reboot and query for hello device twin toofind hello last reboot time.</span></span>
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. <span data-ttu-id="b7734-154">Merhaba aygıt yanıt toohello doğrudan yöntemi hello konsolunda bakın.</span><span class="sxs-lookup"><span data-stu-id="b7734-154">You see hello device response toohello direct method in hello console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
