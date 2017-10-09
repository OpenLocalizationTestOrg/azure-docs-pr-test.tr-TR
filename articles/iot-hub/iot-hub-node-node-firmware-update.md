---
title: "Azure IOT hub'ı (düğüm) aaaDevice ürün yazılımı güncelleştirmesini | Microsoft Docs"
description: "Azure IOT Hub tooinitiate cihaz üretici yazılımı toouse cihaz yönetimini nasıl güncelleştirin. Sanal cihaz uygulaması ve hello bellenim güncelleştirme tetikleyen bir hizmet uygulaması hello Azure IOT SDK'ları için Node.js tooimplement kullanın."
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
ms.openlocfilehash: 99d4b369e7aba334bf713e0c657e6e5d227fb691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-nodenode"></a><span data-ttu-id="474e4-104">Aygıt Yönetimi tooinitiate aygıt üretici yazılımı güncelleştirmesi (düğümü/düğümü) kullanın</span><span class="sxs-lookup"><span data-stu-id="474e4-104">Use device management tooinitiate a device firmware update (Node/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="474e4-105">Giriş</span><span class="sxs-lookup"><span data-stu-id="474e4-105">Introduction</span></span>
<span data-ttu-id="474e4-106">Merhaba, [aygıt Management'i kullanmaya başlama] [ lnk-dm-getstarted] öğretici, gördüğünüz nasıl toouse hello [cihaz çifti] [ lnk-devtwin] ve [doğrudan yöntemleri] [ lnk-c2dmethod] temelleri tooremotely bir aygıtı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="474e4-106">In hello [Get started with device management][lnk-dm-getstarted] tutorial, you saw how toouse hello [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives tooremotely reboot a device.</span></span> <span data-ttu-id="474e4-107">Bu öğretici kullanır aynı IOT hub'ı temelleri hello ve rehberlik sağlar ve nasıl toodo bir uçtan uca bellenim güncelleştirme benzetimli gösterir.</span><span class="sxs-lookup"><span data-stu-id="474e4-107">This tutorial uses hello same IoT Hub primitives and provides guidance and shows you how toodo an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="474e4-108">Bu desen hello bellenim güncelleştirme uygulamasında hello Intel Edison'u aygıt örnek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="474e4-108">This pattern is used in hello firmware update implementation for hello Intel Edison device sample.</span></span>

<span data-ttu-id="474e4-109">Bu öğretici şunların nasıl yapıldığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="474e4-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="474e4-110">IOT hub'ınız aracılığıyla hello sanal cihaz uygulamasında hello firmwareUpdate doğrudan yöntemini çağıran bir Node.js konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="474e4-110">Create a Node.js console app that calls hello firmwareUpdate direct method in hello simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="474e4-111">Arabirimini uygulayan bir sanal cihaz uygulaması oluşturma bir **firmwareUpdate** doğrudan yöntemi.</span><span class="sxs-lookup"><span data-stu-id="474e4-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="474e4-112">Bu yöntem, toodownload hello bellenim görüntü bekler, hello bellenim görüntüyü indirir ve son olarak hello bellenim görüntü geçerlidir bir çok aşama işlemi başlatır.</span><span class="sxs-lookup"><span data-stu-id="474e4-112">This method initiates a multi-stage process that waits toodownload hello firmware image, downloads hello firmware image, and finally applies hello firmware image.</span></span> <span data-ttu-id="474e4-113">Merhaba güncelleştirme her aşaması sırasında hello aygıt kullanır hello ilerlemeyi özellikleri tooreport bildirdi.</span><span class="sxs-lookup"><span data-stu-id="474e4-113">During each stage of hello update, hello device uses hello reported properties tooreport on progress.</span></span>

<span data-ttu-id="474e4-114">Bu öğreticinin Hello sonunda, iki Node.js konsol uygulamaları vardır:</span><span class="sxs-lookup"><span data-stu-id="474e4-114">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="474e4-115">**dmpatterns_fwupdate_service.js**hello sanal cihaz uygulamada, doğrudan bir yöntem çağıran görüntüler hello yanıt ve düzenli aralıklarla (her 500ms) güncelleştirilmiş görüntüler hello bildirilen özellikleri.</span><span class="sxs-lookup"><span data-stu-id="474e4-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in hello simulated device app, displays hello response, and periodically (every 500ms) displays hello updated reported properties.</span></span>

<span data-ttu-id="474e4-116">**dmpatterns_fwupdate_device.js**, daha önce oluşturduğunuz hello cihaz kimliğiyle IOT hub'ı tooyour bağlayan firmwareUpdate doğrudan bir yöntem alır, bellenim güncelleştirme dahil çok durumlu işlem toosimulate çalıştırır: Merhaba bekleniyor Görüntü, hello yeni görüntüsünü indirerek ve son olarak hello görüntüyü uygulamadan'i yükleyin.</span><span class="sxs-lookup"><span data-stu-id="474e4-116">**dmpatterns_fwupdate_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process toosimulate a firmware update including: waiting for hello image download, downloading hello new image, and finally applying hello image.</span></span>

<span data-ttu-id="474e4-117">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="474e4-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="474e4-118">Node.js sürümünü 0.12.x sürümü veya sonraki bir sürümü</span><span class="sxs-lookup"><span data-stu-id="474e4-118">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="474e4-119">[Geliştirme ortamınızı hazırlama] [ lnk-dev-setup] açıklar nasıl tooinstall Node.js Bu öğretici için Windows veya Linux üzerinde.</span><span class="sxs-lookup"><span data-stu-id="474e4-119">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="474e4-120">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="474e4-120">An active Azure account.</span></span> <span data-ttu-id="474e4-121">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="474e4-121">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="474e4-122">Merhaba izleyin [aygıt Management'i kullanmaya başlama](iot-hub-node-node-device-management-get-started.md) toocreate IOT hub'ınızı makalesi ve IOT Hub bağlantı dizenizi alın.</span><span class="sxs-lookup"><span data-stu-id="474e4-122">Follow hello [Get started with device management](iot-hub-node-node-device-management-get-started.md) article toocreate your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a><span data-ttu-id="474e4-123">Merhaba cihaz doğrudan bir yöntem kullanarak bir uzak bellenim güncelleştirme Tetikle</span><span class="sxs-lookup"><span data-stu-id="474e4-123">Trigger a remote firmware update on hello device using a direct method</span></span>
<span data-ttu-id="474e4-124">Bu bölümde, bir cihazda uzaktan bellenim güncelleştirme başlatan bir Node.js konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="474e4-124">In this section, you create a Node.js console app that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="474e4-125">doğrudan yöntemi tooinitiate hello güncelleştirmesi Hello uygulamanın kullandığı ve kullandığı cihaz çifti sorguları tooperiodically hello hello etkin bellenim güncelleştirme durumunu alın.</span><span class="sxs-lookup"><span data-stu-id="474e4-125">hello app uses a direct method tooinitiate hello update and uses device twin queries tooperiodically get hello status of hello active firmware update.</span></span>

1. <span data-ttu-id="474e4-126">Adlı bir boş klasör oluşturun **triggerfwupdateondevice**.</span><span class="sxs-lookup"><span data-stu-id="474e4-126">Create an empty folder called **triggerfwupdateondevice**.</span></span>  <span data-ttu-id="474e4-127">Merhaba, **triggerfwupdateondevice** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="474e4-127">In hello **triggerfwupdateondevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="474e4-128">Tüm hello Varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="474e4-128">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="474e4-129">Merhaba, komut isteminde **triggerfwupdateondevice** klasörüne, komut tooinstall hello aşağıdaki hello **azure IOT hub** ve **azure-IOT-cihaz-mqtt** aygıt SDK paketler:</span><span class="sxs-lookup"><span data-stu-id="474e4-129">At your command prompt in hello **triggerfwupdateondevice** folder, run hello following command tooinstall hello **azure-iot-hub** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="474e4-130">Bir metin düzenleyicisi kullanarak oluşturduğunuz bir **dmpatterns_getstarted_service.js** hello dosyasında **triggerfwupdateondevice** klasör.</span><span class="sxs-lookup"><span data-stu-id="474e4-130">Using a text editor, create a **dmpatterns_getstarted_service.js** file in hello **triggerfwupdateondevice** folder.</span></span>
4. <span data-ttu-id="474e4-131">Merhaba aşağıdaki 'İste' hello hello başlangıç deyimleri ekleme **dmpatterns_getstarted_service.js** dosyası:</span><span class="sxs-lookup"><span data-stu-id="474e4-131">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="474e4-132">Değişken bildirimleri aşağıdaki hello ekleyin ve hello yer tutucu değerlerini değiştirin:</span><span class="sxs-lookup"><span data-stu-id="474e4-132">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. <span data-ttu-id="474e4-133">Merhaba aşağıdaki toofind işlev ve hello firmwareUpdate hello değerini görüntülemek ekleme özelliği bildirdi.</span><span class="sxs-lookup"><span data-stu-id="474e4-133">Add hello following function toofind and display hello value of hello firmwareUpdate reported property.</span></span>
   
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
7. <span data-ttu-id="474e4-134">İşlev tooinvoke hello firmwareUpdate yöntemi tooreboot hello hedef aygıt aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="474e4-134">Add hello following function tooinvoke hello firmwareUpdate method tooreboot hello target device:</span></span>
   
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
          console.error('Could not start hello firmware update on hello device: ' + err.message)
        } 
      });
    };
    ```
8. <span data-ttu-id="474e4-135">Son olarak, Ekle hello aşağıdaki işlev toocode toostart hello bellenim güncelleştirme sırası ve düzenli aralıklarla gösteren Başlat hello bildirilen özellikleri:</span><span class="sxs-lookup"><span data-stu-id="474e4-135">Finally, Add hello following function toocode toostart hello firmware update sequence and start periodically showing hello reported properties:</span></span>
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. <span data-ttu-id="474e4-136">Kaydet ve Kapat hello **dmpatterns_fwupdate_service.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="474e4-136">Save and close hello **dmpatterns_fwupdate_service.js** file.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a><span data-ttu-id="474e4-137">Merhaba uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="474e4-137">Run hello apps</span></span>
<span data-ttu-id="474e4-138">Hazır toorun hello uygulamaları sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="474e4-138">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="474e4-139">Merhaba hello komut isteminde **manageddevice** klasöründe şunu hello yeniden başlatma doğrudan yöntemi için dinleme komutu toobegin aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="474e4-139">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="474e4-140">Merhaba hello komut isteminde **triggerfwupdateondevice** komutu tootrigger hello uzaktan aşağıdaki hello Çalıştır klasörü yeniden başlatın ve hello cihaz çifti toofind hello en son yeniden başlatma için zaman sorgu.</span><span class="sxs-lookup"><span data-stu-id="474e4-140">At hello command prompt in hello **triggerfwupdateondevice** folder, run hello following command tootrigger hello remote reboot and query for hello device twin toofind hello last reboot time.</span></span>
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. <span data-ttu-id="474e4-141">Merhaba aygıt yanıt toohello doğrudan yöntemi hello konsolunda bakın.</span><span class="sxs-lookup"><span data-stu-id="474e4-141">You see hello device response toohello direct method in hello console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="474e4-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="474e4-142">Next steps</span></span>
<span data-ttu-id="474e4-143">Bu öğreticide kullandığınız doğrudan yöntemi tootrigger uzak bir cihaz ve kullanılan hello bellenim güncelleştirme özellikleri toofollow hello hello bellenim güncelleştirme ilerlemesini bildirdi.</span><span class="sxs-lookup"><span data-stu-id="474e4-143">In this tutorial, you used a direct method tootrigger a remote firmware update on a device and used hello reported properties toofollow hello progress of hello firmware update.</span></span>

<span data-ttu-id="474e4-144">toolearn tooextend birden fazla cihazda IOT çözümü ve zamanlama yöntemi çağırır nasıl hello bkz [zamanlama ve yayın işleri] [ lnk-tutorial-jobs] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="474e4-144">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
