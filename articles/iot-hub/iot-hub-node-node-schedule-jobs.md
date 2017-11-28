---
title: "Azure IOT hub'ı (düğüm) aaaSchedule işleriyle | Microsoft Docs"
description: "Nasıl tooschedule Azure IOT hub'ı işi tooinvoke birden çok aygıta doğrudan bir yöntem. Node.js tooimplement benzetimli hello cihaz uygulamaları ve hizmet uygulaması toorun hello işi için hello Azure IOT SDK'ları kullanın."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: be293362447fbcddaa3433b66f208f22545fe0c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-node"></a><span data-ttu-id="82b4d-104">Zamanlama ve yayın işleri (düğüm)</span><span class="sxs-lookup"><span data-stu-id="82b4d-104">Schedule and broadcast jobs (Node)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="82b4d-105">Azure IOT hub'ı, arka uç uygulama toocreate sağlayan tam olarak yönetilen bir hizmet ve zamanlama ve milyonlarca cihaza güncelleştirme izleme işleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="82b4d-105">Azure IoT Hub is a fully managed service that enables a back-end app toocreate and track jobs that schedule and update millions of devices.</span></span>  <span data-ttu-id="82b4d-106">İşlerini Merhaba aşağıdaki eylemler kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="82b4d-106">Jobs can be used for hello following actions:</span></span>

* <span data-ttu-id="82b4d-107">İstenen özellikleri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="82b4d-107">Update desired properties</span></span>
* <span data-ttu-id="82b4d-108">Güncelleştirme etiketleri</span><span class="sxs-lookup"><span data-stu-id="82b4d-108">Update tags</span></span>
* <span data-ttu-id="82b4d-109">Doğrudan yöntemleri çağırma</span><span class="sxs-lookup"><span data-stu-id="82b4d-109">Invoke direct methods</span></span>

<span data-ttu-id="82b4d-110">Kavramsal olarak, bir işi şu eylemlerden birini sarmalar ve bir cihaz çifti sorgu tarafından tanımlanan bir dizi aygıtlar, yürütme ilerlemesini parçaları hello.</span><span class="sxs-lookup"><span data-stu-id="82b4d-110">Conceptually, a job wraps one of these actions and tracks hello progress of execution against a set of devices, which is defined by a device twin query.</span></span>  <span data-ttu-id="82b4d-111">Örneğin, bir cihaz çifti sorgu tarafından belirtilen ve gelecek bir zamanda zamanlanmış 10.000 cihaz üzerinde bir arka uç uygulaması iş tooinvoke yeniden başlatma yöntemini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82b4d-111">For example, a back-end app can use a job tooinvoke a reboot method on 10,000 devices, specified by a device twin query and scheduled at a future time.</span></span>  <span data-ttu-id="82b4d-112">Bu cihazların her biri almak ve execute hello yeniden başlatma yöntemi olarak bu uygulama daha sonra ilerleme durumunu izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82b4d-112">That application can then track progress as each of those devices receive and execute hello reboot method.</span></span>

<span data-ttu-id="82b4d-113">Bu makaleler, bu özelliklerin her biri hakkında daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="82b4d-113">Learn more about each of these capabilities in these articles:</span></span>

* <span data-ttu-id="82b4d-114">Cihaz çifti ve özellikleri: [cihaz çiftlerini ile çalışmaya başlama] [ lnk-get-started-twin] ve [Öğreticisi: nasıl toouse cihaz çifti özellikleri][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="82b4d-114">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How toouse device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="82b4d-115">doğrudan yöntemleri: [IOT Hub Geliştirici Kılavuzu - doğrudan yöntemleri] [ lnk-dev-methods] ve [Öğreticisi: doğrudan yöntemleri][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="82b4d-115">direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="82b4d-116">Bu öğretici şunların nasıl yapıldığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="82b4d-116">This tutorial shows you how to:</span></span>

* <span data-ttu-id="82b4d-117">Sağlayan doğrudan bir yönteme sahip bir sanal cihaz uygulaması oluşturma **lockDoor** hangi çağrılabilir hello çözüm arka ucu tarafından.</span><span class="sxs-lookup"><span data-stu-id="82b4d-117">Create a simulated device app that has a direct method which enables **lockDoor** which can be called by hello solution back end.</span></span>
* <span data-ttu-id="82b4d-118">Bu çağrı hello bir Node.js konsol uygulaması oluşturmak **lockDoor** hello sanal cihaz uygulamasının iş ve güncelleştirmeleri hello kullanarak doğrudan yönteminde istenen cihaz işi kullanarak özellikleri.</span><span class="sxs-lookup"><span data-stu-id="82b4d-118">Create a Node.js console app that calls hello **lockDoor** direct method in hello simulated device app using a job and updates hello desired properties using a device job.</span></span>

<span data-ttu-id="82b4d-119">Bu öğreticinin Hello sonunda, iki Node.js konsol uygulamaları vardır:</span><span class="sxs-lookup"><span data-stu-id="82b4d-119">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="82b4d-120">**simDevice.js**, tooyour IOT hub'ı hello cihaz kimliği bağlanır ve alan bir **lockDoor** doğrudan yöntemi.</span><span class="sxs-lookup"><span data-stu-id="82b4d-120">**simDevice.js**, which connects tooyour IoT hub with hello device identity and receives a **lockDoor** direct method.</span></span>

<span data-ttu-id="82b4d-121">**scheduleJobService.js**, çağıran doğrudan bir yöntem hello sanal cihaz uygulama ve güncelleştirme hello aygıt bir iş kullanarak twin'ın istenen özellikleri.</span><span class="sxs-lookup"><span data-stu-id="82b4d-121">**scheduleJobService.js**, which calls a direct method in hello simulated device app and update hello device twin's desired properties using a job.</span></span>

<span data-ttu-id="82b4d-122">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="82b4d-122">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="82b4d-123">Node.js sürümünü 0.12.x sürümü veya sonraki bir sürümü</span><span class="sxs-lookup"><span data-stu-id="82b4d-123">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="82b4d-124">[Geliştirme ortamınızı hazırlama] [ lnk-dev-setup] açıklar nasıl tooinstall Node.js Bu öğretici için Windows veya Linux üzerinde.</span><span class="sxs-lookup"><span data-stu-id="82b4d-124">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="82b4d-125">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="82b4d-125">An active Azure account.</span></span> <span data-ttu-id="82b4d-126">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="82b4d-126">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="82b4d-127">Sanal cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="82b4d-127">Create a simulated device app</span></span>
<span data-ttu-id="82b4d-128">Bu bölümde, sanal cihaz yeniden başlatma tetikler hello bulut tarafından adlı tooa doğrudan yöntemi yanıt bir Node.js konsol uygulaması oluşturun ve Özellikler tooenable cihaz çifti sorguları tooidentify aygıtlar ve bunların en son ne zaman yeniden kullandığı hello rapor.</span><span class="sxs-lookup"><span data-stu-id="82b4d-128">In this section, you create a Node.js console app that responds tooa direct method called by hello cloud, which triggers a simulated device reboot and uses hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="82b4d-129">Adlı yeni bir boş klasör oluşturun **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="82b4d-129">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="82b4d-130">Merhaba, **simDevice** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="82b4d-130">In hello **simDevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="82b4d-131">Tüm hello Varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="82b4d-131">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="82b4d-132">Merhaba, komut isteminde **simDevice** klasörüne, komut tooinstall hello aşağıdaki hello **azure IOT cihaz** cihaz SDK'sı paketinin ve **azure-IOT-cihaz-mqtt** paketi:</span><span class="sxs-lookup"><span data-stu-id="82b4d-132">At your command prompt in hello **simDevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="82b4d-133">Bir metin düzenleyicisi kullanarak yeni bir oluşturma **simDevice.js** hello dosyasında **simDevice** klasör.</span><span class="sxs-lookup"><span data-stu-id="82b4d-133">Using a text editor, create a new **simDevice.js** file in hello **simDevice** folder.</span></span>
4. <span data-ttu-id="82b4d-134">Merhaba aşağıdaki 'İste' hello hello başlangıç deyimleri ekleme **simDevice.js** dosyası:</span><span class="sxs-lookup"><span data-stu-id="82b4d-134">Add hello following 'require' statements at hello start of hello **simDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="82b4d-135">Ekleme bir **connectionString** değişken ve toocreate kullanan bir **istemci** örneği.</span><span class="sxs-lookup"><span data-stu-id="82b4d-135">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="82b4d-136">İşlev toohandle hello aşağıdaki hello eklemek **lockDoor** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="82b4d-136">Add hello following function toohandle hello **lockDoor** method.</span></span>
   
    ```
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```
7. <span data-ttu-id="82b4d-137">Kod tooregister hello işleyici hello için aşağıdaki hello eklemek **lockDoor** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="82b4d-137">Add hello following code tooregister hello handler for hello **lockDoor** method.</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub. Register handler for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```
8. <span data-ttu-id="82b4d-138">Kaydet ve Kapat hello **simDevice.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="82b4d-138">Save and close hello **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="82b4d-139">tookeep şeyler basit, Bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="82b4d-139">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="82b4d-140">Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="82b4d-140">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a><span data-ttu-id="82b4d-141">İşlerini doğrudan bir yöntemi çağırmak ve bir cihaz çifti'nın özelliklerini güncelleştirmek için zamanla</span><span class="sxs-lookup"><span data-stu-id="82b4d-141">Schedule jobs for calling a direct method and updating a device twin's properties</span></span>
<span data-ttu-id="82b4d-142">Bu bölümde, bir uzak başlatan bir Node.js konsol uygulaması oluşturma **lockDoor** bir doğrudan yöntemi ve güncelleştirme hello cihaz çifti'nın özelliklerini kullanarak bir cihazdaki.</span><span class="sxs-lookup"><span data-stu-id="82b4d-142">In this section, you create a Node.js console app that initiates a remote **lockDoor** on a device using a direct method and update hello device twin's properties.</span></span>

1. <span data-ttu-id="82b4d-143">Adlı yeni bir boş klasör oluşturun **scheduleJobService**.</span><span class="sxs-lookup"><span data-stu-id="82b4d-143">Create a new empty folder called **scheduleJobService**.</span></span>  <span data-ttu-id="82b4d-144">Merhaba, **scheduleJobService** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="82b4d-144">In hello **scheduleJobService** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="82b4d-145">Tüm hello Varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="82b4d-145">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="82b4d-146">Merhaba, komut isteminde **scheduleJobService** klasörüne, komut tooinstall hello aşağıdaki hello **azure-iothub** cihaz SDK'sı paketinin ve **azure-IOT-cihaz-mqtt**paketi:</span><span class="sxs-lookup"><span data-stu-id="82b4d-146">At your command prompt in hello **scheduleJobService** folder, run hello following command tooinstall hello **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub uuid --save
    ```
3. <span data-ttu-id="82b4d-147">Bir metin düzenleyicisi kullanarak yeni bir oluşturma **scheduleJobService.js** hello dosyasında **scheduleJobService** klasör.</span><span class="sxs-lookup"><span data-stu-id="82b4d-147">Using a text editor, create a new **scheduleJobService.js** file in hello **scheduleJobService** folder.</span></span>
4. <span data-ttu-id="82b4d-148">Merhaba aşağıdaki 'İste' hello hello başlangıç deyimleri ekleme **dmpatterns_gscheduleJobServiceetstarted_service.js** dosyası:</span><span class="sxs-lookup"><span data-stu-id="82b4d-148">Add hello following 'require' statements at hello start of hello **dmpatterns_gscheduleJobServiceetstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var uuid = require('uuid');
    var JobClient = require('azure-iothub').JobClient;
    ```
5. <span data-ttu-id="82b4d-149">Değişken bildirimleri aşağıdaki hello ekleyin ve hello yer tutucu değerlerini değiştirin:</span><span class="sxs-lookup"><span data-stu-id="82b4d-149">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var queryCondition = "deviceId IN ['myDeviceId']";
    var startTime = new Date();
    var maxExecutionTimeInSeconds =  3600;
    var jobClient = JobClient.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="82b4d-150">Kullanılan toomonitor hello hello işinin yürütülmesi olacaktır işlevi aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="82b4d-150">Add hello following function that will be used toomonitor hello execution of hello job:</span></span>
   
    ```
    function monitorJob (jobId, callback) {
        var jobMonitorInterval = setInterval(function() {
            jobClient.getJob(jobId, function(err, result) {
            if (err) {
                console.error('Could not get job status: ' + err.message);
            } else {
                console.log('Job: ' + jobId + ' - status: ' + result.status);
                if (result.status === 'completed' || result.status === 'failed' || result.status === 'cancelled') {
                clearInterval(jobMonitorInterval);
                callback(null, result);
                }
            }
            });
        }, 5000);
    }
    ```
7. <span data-ttu-id="82b4d-151">Hello aygıt yöntemini çağıran kodu tooschedule hello işi aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="82b4d-151">Add hello following code tooschedule hello job that calls hello device method:</span></span>
   
    ```
    var methodParams = {
        methodName: 'lockDoor',
        payload: null,
        responseTimeoutInSeconds: 15 // Timeout after 15 seconds if device is unable tooprocess method
    };
   
    var methodJobId = uuid.v4();
    console.log('scheduling Device Method job with id: ' + methodJobId);
    jobClient.scheduleDeviceMethod(methodJobId,
                                queryCondition,
                                methodParams,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule device method job: ' + err.message);
        } else {
            monitorJob(methodJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor device method job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
8. <span data-ttu-id="82b4d-152">Kod tooschedule hello iş tooupdate hello cihaz çifti aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="82b4d-152">Add hello following code tooschedule hello job tooupdate hello device twin:</span></span>
   
    ```
    var twinPatch = {
        etag: '*',
        desired: {
            building: '43',
            floor: 3
        }
    };
   
    var twinJobId = uuid.v4();
   
    console.log('scheduling Twin Update job with id: ' + twinJobId);
    jobClient.scheduleTwinUpdate(twinJobId,
                                queryCondition,
                                twinPatch,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule twin update job: ' + err.message);
        } else {
            monitorJob(twinJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor twin update job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
9. <span data-ttu-id="82b4d-153">Kaydet ve Kapat hello **scheduleJobService.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="82b4d-153">Save and close hello **scheduleJobService.js** file.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="82b4d-154">Merhaba uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="82b4d-154">Run hello applications</span></span>
<span data-ttu-id="82b4d-155">Hazır toorun hello uygulamaları sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="82b4d-155">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="82b4d-156">Merhaba hello komut isteminde **simDevice** klasöründe şunu hello yeniden başlatma doğrudan yöntemi için dinleme komutu toobegin aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="82b4d-156">At hello command prompt in hello **simDevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node simDevice.js
    ```
2. <span data-ttu-id="82b4d-157">Merhaba hello komut isteminde **scheduleJobService** klasörü, komut tootrigger hello işleri toolock hello kapı ve güncelleştirme hello çifti aşağıdaki hello çalıştırın</span><span class="sxs-lookup"><span data-stu-id="82b4d-157">At hello command prompt in hello **scheduleJobService** folder, run hello following command tootrigger hello jobs toolock hello door and update hello twin</span></span>
   
    ```
    node scheduleJobService.js
    ```
3. <span data-ttu-id="82b4d-158">Merhaba aygıt yanıt toohello doğrudan yöntemi hello konsolunda bakın.</span><span class="sxs-lookup"><span data-stu-id="82b4d-158">You see hello device response toohello direct method in hello console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82b4d-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="82b4d-159">Next steps</span></span>
<span data-ttu-id="82b4d-160">Bu öğreticide, bir iş tooschedule doğrudan yöntemi tooa cihaz ve hello güncelleştirme hello cihaz çifti'nın özelliklerinin kullanılır.</span><span class="sxs-lookup"><span data-stu-id="82b4d-160">In this tutorial, you used a job tooschedule a direct method tooa device and hello update of hello device twin's properties.</span></span>

<span data-ttu-id="82b4d-161">IOT Hub ve cihaz yönetim desenleri uzaktan gibi hello hava bellenim güncelleştirme kullanmaya Başlarken toocontinue bakın:</span><span class="sxs-lookup"><span data-stu-id="82b4d-161">toocontinue getting started with IoT Hub and device management patterns such as remote over hello air firmware update, see:</span></span>

<span data-ttu-id="82b4d-162">[Öğretici: Toodo üretici yazılımı nasıl güncelleştirin.][lnk-fwupdate]</span><span class="sxs-lookup"><span data-stu-id="82b4d-162">[Tutorial: How toodo a firmware update][lnk-fwupdate]</span></span>

<span data-ttu-id="82b4d-163">IOT Hub ile çalışmaya başlama toocontinue bkz [Azure IOT Edge ile çalışmaya başlama][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="82b4d-163">toocontinue getting started with IoT Hub, see [Getting started with Azure IoT Edge][lnk-iot-edge].</span></span>

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
