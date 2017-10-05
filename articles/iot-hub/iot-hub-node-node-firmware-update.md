---
title: "Cihaz üretici yazılımı güncelleştirme ile Azure IOT hub'ı (düğüm) | Microsoft Docs"
description: "Cihaz Yönetimi Azure IOT hub'ına aygıt üretici yazılımı güncelleştirmesi başlatmak için nasıl kullanılacağını. Sanal cihaz uygulaması ve bellenim güncelleştirme tetikleyen bir hizmet uygulaması uygulamak için Node.js için Azure IOT SDK'ları kullanın."
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
ms.date: 02/06/2017
ms.author: juanpere
ms.openlocfilehash: 350cf1cbec8847d1bbf29814435502af6f098e54
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-device-management-to-initiate-a-device-firmware-update-nodenode"></a><span data-ttu-id="feb6d-104">Bir cihaz üretici yazılımı güncelleştirmesi (düğümü/düğümü) başlatmak için cihaz Yönetimi'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="feb6d-104">Use device management to initiate a device firmware update (Node/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="feb6d-105">Giriş</span><span class="sxs-lookup"><span data-stu-id="feb6d-105">Introduction</span></span>
<span data-ttu-id="feb6d-106">İçinde [aygıt Management'i kullanmaya başlama] [ lnk-dm-getstarted] Öğreticisi, nasıl kullanılacağını gördüğünüz [cihaz çifti] [ lnk-devtwin] ve [doğrudan yöntemleri ] [ lnk-c2dmethod] temelleri uzaktan bir aygıt yeniden başlatma.</span><span class="sxs-lookup"><span data-stu-id="feb6d-106">In the [Get started with device management][lnk-dm-getstarted] tutorial, you saw how to use the [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives to remotely reboot a device.</span></span> <span data-ttu-id="feb6d-107">Bu öğretici aynı IOT hub'ı temelleri kullanır ve rehberlik sağlar ve bir uçtan uca sanal üretici yazılımı güncelleştirme yapmak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="feb6d-107">This tutorial uses the same IoT Hub primitives and provides guidance and shows you how to do an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="feb6d-108">Bu deseni bellenim güncelleştirme uygulamasında Intel Edison'u aygıt örnek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="feb6d-108">This pattern is used in the firmware update implementation for the Intel Edison device sample.</span></span>

<span data-ttu-id="feb6d-109">Bu öğretici şunların nasıl yapıldığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="feb6d-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="feb6d-110">IOT hub'ınız aracılığıyla sanal cihaz uygulamasında firmwareUpdate doğrudan yöntemini çağıran bir Node.js konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="feb6d-110">Create a Node.js console app that calls the firmwareUpdate direct method in the simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="feb6d-111">Arabirimini uygulayan bir sanal cihaz uygulaması oluşturma bir **firmwareUpdate** doğrudan yöntemi.</span><span class="sxs-lookup"><span data-stu-id="feb6d-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="feb6d-112">Bu yöntem bellenim görüntüsünü karşıdan yüklemek için bekleyeceği, bellenim görüntüyü indirir ve son bellenim görüntü geçerli bir çok aşama işlemi başlatır.</span><span class="sxs-lookup"><span data-stu-id="feb6d-112">This method initiates a multi-stage process that waits to download the firmware image, downloads the firmware image, and finally applies the firmware image.</span></span> <span data-ttu-id="feb6d-113">Güncelleştirme her aşaması sırasında aygıt ilerlemesini bildirmek için bildirilen özelliklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="feb6d-113">During each stage of the update, the device uses the reported properties to report on progress.</span></span>

<span data-ttu-id="feb6d-114">Bu öğreticinin sonunda iki Node.js konsol uygulamaları vardır:</span><span class="sxs-lookup"><span data-stu-id="feb6d-114">At the end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="feb6d-115">**dmpatterns_fwupdate_service.js**yanıt görüntüler, sanal cihaz uygulamada, doğrudan bir yöntemi çağırır ve düzenli aralıklarla (her 500ms) görüntüler güncelleştirilmiş bildirilen özellikleri.</span><span class="sxs-lookup"><span data-stu-id="feb6d-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in the simulated device app, displays the response, and periodically (every 500ms) displays the updated reported properties.</span></span>

<span data-ttu-id="feb6d-116">**dmpatterns_fwupdate_device.js**, daha önce oluşturulan cihaz kimliğiyle IOT hub'ınızı bağlayan firmwareUpdate doğrudan bir yöntem alır, bellenim güncelleştirme dahil benzetimini yapmak için çok durumlu bir işlem çalışır: görüntü için bekleniyor , yeni görüntüyü indirme ve son olarak görüntüyü uygulamadan indirin.</span><span class="sxs-lookup"><span data-stu-id="feb6d-116">**dmpatterns_fwupdate_device.js**, which connects to your IoT hub with the device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process to simulate a firmware update including: waiting for the image download, downloading the new image, and finally applying the image.</span></span>

<span data-ttu-id="feb6d-117">Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="feb6d-117">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="feb6d-118">Node.js sürümünü 0.12.x sürümü veya sonraki bir sürümü</span><span class="sxs-lookup"><span data-stu-id="feb6d-118">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="feb6d-119">[Geliştirme ortamınızı hazırlama] [ lnk-dev-setup] Node.js Bu öğretici için Windows veya Linux'ta nasıl yükleneceğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="feb6d-119">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="feb6d-120">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="feb6d-120">An active Azure account.</span></span> <span data-ttu-id="feb6d-121">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="feb6d-121">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="feb6d-122">İzleyin [aygıt Management'i kullanmaya başlama](iot-hub-node-node-device-management-get-started.md) IOT hub'ınızı oluşturun ve IOT Hub bağlantı dizenizi almak için makale.</span><span class="sxs-lookup"><span data-stu-id="feb6d-122">Follow the [Get started with device management](iot-hub-node-node-device-management-get-started.md) article to create your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-the-device-using-a-direct-method"></a><span data-ttu-id="feb6d-123">Doğrudan bir yöntem kullanarak aygıt bir uzak bellenim güncelleştirme Tetikle</span><span class="sxs-lookup"><span data-stu-id="feb6d-123">Trigger a remote firmware update on the device using a direct method</span></span>
<span data-ttu-id="feb6d-124">Bu bölümde, bir cihazda uzaktan bellenim güncelleştirme başlatan bir Node.js konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="feb6d-124">In this section, you create a Node.js console app that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="feb6d-125">Uygulama güncelleştirme başlatmak için doğrudan bir yöntem kullanır ve etkin bellenim güncelleştirme durumunu düzenli aralıklarla almak için cihaz çifti sorgularını kullanır.</span><span class="sxs-lookup"><span data-stu-id="feb6d-125">The app uses a direct method to initiate the update and uses device twin queries to periodically get the status of the active firmware update.</span></span>

1. <span data-ttu-id="feb6d-126">Adlı bir boş klasör oluşturun **triggerfwupdateondevice**.</span><span class="sxs-lookup"><span data-stu-id="feb6d-126">Create an empty folder called **triggerfwupdateondevice**.</span></span>  <span data-ttu-id="feb6d-127">İçinde **triggerfwupdateondevice** klasörü, komut isteminde aşağıdaki komutu kullanarak bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="feb6d-127">In the **triggerfwupdateondevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="feb6d-128">Tüm varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="feb6d-128">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="feb6d-129">Komut isteminizde **triggerfwupdateondevice** klasörü yüklemek için aşağıdaki komutu çalıştırın, **azure IOT hub** ve **azure-IOT-cihaz-mqtt** cihaz SDK'sı paketler:</span><span class="sxs-lookup"><span data-stu-id="feb6d-129">At your command prompt in the **triggerfwupdateondevice** folder, run the following command to install the **azure-iot-hub** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="feb6d-130">Bir metin düzenleyicisi kullanarak oluşturduğunuz bir **dmpatterns_getstarted_service.js** dosyasını **triggerfwupdateondevice** klasör.</span><span class="sxs-lookup"><span data-stu-id="feb6d-130">Using a text editor, create a **dmpatterns_getstarted_service.js** file in the **triggerfwupdateondevice** folder.</span></span>
4. <span data-ttu-id="feb6d-131">Aşağıdaki 'İste' deyimleri başlangıcında eklemek **dmpatterns_getstarted_service.js** dosyası:</span><span class="sxs-lookup"><span data-stu-id="feb6d-131">Add the following 'require' statements at the start of the **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="feb6d-132">Aşağıdaki değişken bildirimlerini ekleme ve yer tutucu değerlerini değiştirin:</span><span class="sxs-lookup"><span data-stu-id="feb6d-132">Add the following variable declarations and replace the placeholder values:</span></span>
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. <span data-ttu-id="feb6d-133">Bulmak için aşağıdaki işlevi ekleyin ve özellik görüntü firmwareUpdate değerini bildirdi.</span><span class="sxs-lookup"><span data-stu-id="feb6d-133">Add the following function to find and display the value of the firmwareUpdate reported property.</span></span>
   
    ```
    var queryTwinFWUpdateReported = function() {
        registry.getTwin(deviceToUpdate, function(err, twin){
            if (err) {
              console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
            } else {
              console.log((JSON.stringify(twin.properties.reported.iothubDM.firmwareUpdate)) + "\n");
            }
        });
    };
    ```
7. <span data-ttu-id="feb6d-134">Hedef aygıt yeniden firmwareUpdate yöntemini çağırmak için aşağıdaki işlevi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="feb6d-134">Add the following function to invoke the firmwareUpdate method to reboot the target device:</span></span>
   
    ```
    var startFirmwareUpdateDevice = function() {
      var params = {
          fwPackageUri: 'https://secureurl'
      };
   
      var methodName = "firmwareUpdate";
      var payloadData =  JSON.stringify(params);
   
      var methodParams = {
        methodName: methodName,
        payload: payloadData,
        timeoutInSeconds: 30
      };
   
      client.invokeDeviceMethod(deviceToUpdate, methodParams, function(err, result) {
        if (err) {
          console.error('Could not start the firmware update on the device: ' + err.message)
        } 
      });
    };
    ```
8. <span data-ttu-id="feb6d-135">Son olarak, aşağıdaki işlev bellenim güncelleştirme sırası ve düzenli olarak bildirilen özelliklerini gösteren başlatmak için kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="feb6d-135">Finally, Add the following function to code to start the firmware update sequence and start periodically showing the reported properties:</span></span>
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. <span data-ttu-id="feb6d-136">Kaydet ve Kapat **dmpatterns_fwupdate_service.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="feb6d-136">Save and close the **dmpatterns_fwupdate_service.js** file.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-the-apps"></a><span data-ttu-id="feb6d-137">Uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="feb6d-137">Run the apps</span></span>
<span data-ttu-id="feb6d-138">Şimdi uygulamaları çalıştırmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="feb6d-138">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="feb6d-139">Komut isteminde **manageddevice** klasörü, yeniden başlatma doğrudan yöntemi için dinleme başlamak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="feb6d-139">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="feb6d-140">Komut isteminde **triggerfwupdateondevice** klasörü, Uzaktan yeniden başlatma ve sorgu son bulmak cihaz çifti için yeniden başlatma zamanı tetikleyicisi için şu komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="feb6d-140">At the command prompt in the **triggerfwupdateondevice** folder, run the following command to trigger the remote reboot and query for the device twin to find the last reboot time.</span></span>
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. <span data-ttu-id="feb6d-141">Konsolunda doğrudan yöntemi aygıt yanıta bakın.</span><span class="sxs-lookup"><span data-stu-id="feb6d-141">You see the device response to the direct method in the console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="feb6d-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="feb6d-142">Next steps</span></span>
<span data-ttu-id="feb6d-143">Bu öğreticide, doğrudan bir yöntem bir cihazda uzaktan Bellenim güncelleştirmesini tetiklemek için bildirilen özellikleri bellenim güncelleştirme durumunu izlemek için kullanılır ve.</span><span class="sxs-lookup"><span data-stu-id="feb6d-143">In this tutorial, you used a direct method to trigger a remote firmware update on a device and used the reported properties to follow the progress of the firmware update.</span></span>

<span data-ttu-id="feb6d-144">Çözüm ve zamanlama yöntemini çağıran birden fazla cihazda, IOT genişletmek öğrenmek için bkz: [zamanlama ve yayın işleri] [ lnk-tutorial-jobs] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="feb6d-144">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
