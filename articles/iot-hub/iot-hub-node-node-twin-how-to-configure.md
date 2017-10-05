---
title: "Azure IOT Hub cihaz çifti özellikleri (düğüm) kullanın | Microsoft Docs"
description: "Azure IOT Hub cihaz çiftlerini cihazları yapılandırmak için nasıl kullanılacağını. Sanal cihaz uygulaması ve cihaz çifti kullanarak bir aygıt yapılandırmasını değiştirir bir hizmet uygulaması uygulamak için Node.js için Azure IOT SDK'ları kullanın."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: d0bcec50-26e6-40f0-8096-733b2f3071ec
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: elioda
ms.openlocfilehash: 771106ce7b00a5231d9929e4b5ea34aefe693597
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-desired-properties-to-configure-devices-node"></a><span data-ttu-id="b4db8-104">İstenen özelliklerde cihazları (düğüm) yapılandırmak için kullanın</span><span class="sxs-lookup"><span data-stu-id="b4db8-104">Use desired properties to configure devices (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="b4db8-105">Bu öğreticinin sonunda iki Node.js konsol uygulamaları olacaktır:</span><span class="sxs-lookup"><span data-stu-id="b4db8-105">At the end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="b4db8-106">**SimulateDeviceConfiguration.js**, istenen yapılandırma güncelleştirmesi bekler ve benzetimli yapılandırmasını güncelleştirme işleminin durumunu raporlar bir sanal cihaz uygulaması.</span><span class="sxs-lookup"><span data-stu-id="b4db8-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports the status of a simulated configuration update process.</span></span>
* <span data-ttu-id="b4db8-107">**SetDesiredConfigurationAndQuery.js**, istenen yapılandırma bir cihazda ayarlar ve yapılandırmayı güncelleştirme işlemini sorgular bir Node.js arka uç uygulaması.</span><span class="sxs-lookup"><span data-stu-id="b4db8-107">**SetDesiredConfigurationAndQuery.js**, a Node.js back-end app, which sets the desired configuration on a device and queries the configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="b4db8-108">Makaleyi [Azure IOT SDK'ları] [ lnk-hub-sdks] hem cihaz hem de arka uç uygulamalar oluşturmak için kullanabileceğiniz Azure IOT SDK'ları hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b4db8-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="b4db8-109">Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="b4db8-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="b4db8-110">Node.js 0.10.x sürümü veya sonraki bir sürüm.</span><span class="sxs-lookup"><span data-stu-id="b4db8-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="b4db8-111">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="b4db8-111">An active Azure account.</span></span> <span data-ttu-id="b4db8-112">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="b4db8-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="b4db8-113">İzlediyseniz [cihaz çiftlerini ile çalışmaya başlama] [ lnk-twin-tutorial] öğretici, zaten sahip olduğunuz bir IOT hub ve adlı bir cihaz kimliği **myDeviceId**; ve atlayabilirsiniz[Sanal cihaz uygulaması oluşturma] [ lnk-how-to-configure-createapp] bölümü.</span><span class="sxs-lookup"><span data-stu-id="b4db8-113">If you followed the [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**; and you can skip to the [Create the simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-simulated-device-app"></a><span data-ttu-id="b4db8-114">Sanal cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="b4db8-114">Create the simulated device app</span></span>
<span data-ttu-id="b4db8-115">Bu bölümde, hub'ınıza bağlanan bir Node.js konsol uygulaması oluşturma **myDeviceId**, istenen yapılandırma güncelleştirmesi bekler ve daha sonra güncelleştirmeleri benzetimli yapılandırmasını güncelleştirme işlemini raporlar.</span><span class="sxs-lookup"><span data-stu-id="b4db8-115">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, waits for a desired configuration update and then reports updates on the simulated configuration update process.</span></span>

1. <span data-ttu-id="b4db8-116">Adlı yeni bir boş klasör oluşturun **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="b4db8-116">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="b4db8-117">İçinde **simulatedeviceconfiguration** klasörü, komut isteminde aşağıdaki komutu kullanarak yeni bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b4db8-117">In the **simulatedeviceconfiguration** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="b4db8-118">Tüm varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="b4db8-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="b4db8-119">Komut isteminizde **simulatedeviceconfiguration** klasörü yüklemek için aşağıdaki komutu çalıştırın, **azure IOT cihaz**, ve **azure-IOT-cihaz-mqtt** paketi:</span><span class="sxs-lookup"><span data-stu-id="b4db8-119">At your command prompt in the **simulatedeviceconfiguration** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="b4db8-120">Bir metin düzenleyicisi kullanarak yeni bir oluşturma **SimulateDeviceConfiguration.js** dosyasını **simulatedeviceconfiguration** klasör.</span><span class="sxs-lookup"><span data-stu-id="b4db8-120">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in the **simulatedeviceconfiguration** folder.</span></span>
4. <span data-ttu-id="b4db8-121">Aşağıdaki kodu ekleyin **SimulateDeviceConfiguration.js** dosya ve yerine **{cihaz bağlantı dizesi}** yer tutucu oluştururken kopyaladığınız cihaz bağlantı dizesiyle **myDeviceId** cihaz kimliği:</span><span class="sxs-lookup"><span data-stu-id="b4db8-121">Add the following code to the **SimulateDeviceConfiguration.js** file, and substitute the **{device connection string}** placeholder with the device connection string you copied when you created the **myDeviceId** device identity:</span></span>
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
            if (err) {
                console.error('could not open IotHub client');
            } else {
                client.getTwin(function(err, twin) {
                    if (err) {
                        console.error('could not get twin');
                    } else {
                        console.log('retrieved device twin');
                        twin.properties.reported.telemetryConfig = {
                            configId: "0",
                            sendFrequency: "24h"
                        }
                        twin.on('properties.desired', function(desiredChange) {
                            console.log("received change: "+JSON.stringify(desiredChange));
                            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
                            if (desiredChange.telemetryConfig &&desiredChange.telemetryConfig.configId !== currentTelemetryConfig.configId) {
                                initConfigChange(twin);
                            }
                        });
                    }
                });
            }
        });
   
    <span data-ttu-id="b4db8-122">**İstemci** nesne cihaz çiftlerini aygıttan ile etkileşim kurmak için gereken tüm yöntemleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="b4db8-122">The **Client** object exposes all the methods required to interact with device twins from the device.</span></span> <span data-ttu-id="b4db8-123">Bunu başlatır sonra önceki kod **istemci** nesnesi, cihaz çiftinin alır **myDeviceId**ve istenen özellikler güncelleştirme için bir işleyici ekler.</span><span class="sxs-lookup"><span data-stu-id="b4db8-123">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId**, and attaches a handler for the update on desired properties.</span></span> <span data-ttu-id="b4db8-124">İşleyici olmadığını configIds karşılaştırarak bir gerçek yapılandırma değişikliği isteği olup, ardından yapılandırma değişikliği başlatan bir yöntemi çağırır doğrular.</span><span class="sxs-lookup"><span data-stu-id="b4db8-124">The handler verifies that there is an actual configuration change request by comparing the configIds, then invokes a method that starts the configuration change.</span></span>
   
    <span data-ttu-id="b4db8-125">Basitleştirmek amacıyla, sabit kodlanmış varsayılan bir önceki kod ilk yapılandırmasını kullandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b4db8-125">Note that for the sake of simplicity, the previous code uses a hard-coded default for the inital configuration.</span></span> <span data-ttu-id="b4db8-126">Gerçek bir uygulama büyük olasılıkla bu yapılandırma yerel depolama biriminden yüklenir.</span><span class="sxs-lookup"><span data-stu-id="b4db8-126">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="b4db8-127">İstenen özellik değiştirme olayları her zaman bir kez aygıt bağlantıdaki gösterilen, herhangi bir işlem gerçekleştirmeden önce İstenen özelliklerde gerçek bir değişiklik olup olmadığını denetlemek emin olun.</span><span class="sxs-lookup"><span data-stu-id="b4db8-127">Desired property change events are always emitted once at device connection, make sure to check that there is an actual change in the desired properties before performing any action.</span></span>
   > 
   > 
5. <span data-ttu-id="b4db8-128">Önce aşağıdaki yöntemleri ekleyin `client.open()` çağırma:</span><span class="sxs-lookup"><span data-stu-id="b4db8-128">Add the following methods before the `client.open()` invocation:</span></span>
   
        var initConfigChange = function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.pendingConfig = twin.properties.desired.telemetryConfig;
            currentTelemetryConfig.status = "Pending";
   
            var patch = {
            telemetryConfig: currentTelemetryConfig
            };
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.log('Could not report properties');
                } else {
                    console.log('Reported pending config change: ' + JSON.stringify(patch));
                    setTimeout(function() {completeConfigChange(twin);}, 60000);
                }
            });
        }
   
        var completeConfigChange =  function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.configId = currentTelemetryConfig.pendingConfig.configId;
            currentTelemetryConfig.sendFrequency = currentTelemetryConfig.pendingConfig.sendFrequency;
            currentTelemetryConfig.status = "Success";
            delete currentTelemetryConfig.pendingConfig;
   
            var patch = {
                telemetryConfig: currentTelemetryConfig
            };
            patch.telemetryConfig.pendingConfig = null;
   
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.error('Error reporting properties: ' + err);
                } else {
                    console.log('Reported completed config change: ' + JSON.stringify(patch));
                }
            });
        };
   
    <span data-ttu-id="b4db8-129">**İnitConfigChange** yöntemi yerel cihaz çifti nesnesindeki bildirilen özellikleri yapılandırma güncelleştirme isteği ile güncelleştirir ve durumunu ayarlar **bekleyen**, cihaz çifti sonra güncelleştirir hizmet.</span><span class="sxs-lookup"><span data-stu-id="b4db8-129">The **initConfigChange** method updates reported properties on the local device twin object with the configuration update request and sets the status to **Pending**, then updates the device twin on the service.</span></span> <span data-ttu-id="b4db8-130">Cihaz çifti başarıyla güncelleştirdikten sonra yürütme işlemi sona erer uzun süre çalışan bir işlem benzetim **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="b4db8-130">After successfully updating the device twin, it simulates a long running process that terminates in the execution of **completeConfigChange**.</span></span> <span data-ttu-id="b4db8-131">Bu yöntem yerel cihaz çifti'nın bildirilen özellikleri durumu ayarını güncelleştirmeleri **başarı** ve kaldırma **pendingConfig** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="b4db8-131">This method updates the local device twin's reported properties setting the status to **Success** and removing the **pendingConfig** object.</span></span> <span data-ttu-id="b4db8-132">Ardından, cihaz çifti hizmette güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="b4db8-132">It then updates the device twin on the service.</span></span>
   
    <span data-ttu-id="b4db8-133">Bant genişliğini korumak için bildirilen özellikler, yalnızca değiştirilecek özelliklerini belirterek güncelleştirilir unutmayın (adlı **düzeltme eki** Yukarıdaki koddaki), tüm belgeyi değiştirme yerine.</span><span class="sxs-lookup"><span data-stu-id="b4db8-133">Note that, to save bandwidth, reported properties are updated by specifying only the properties to be modified (named **patch** in the above code), instead of replacing the whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b4db8-134">Bu öğretici herhangi davranışı eşzamanlı yapılandırma güncelleştirmelerini benzetimini değil.</span><span class="sxs-lookup"><span data-stu-id="b4db8-134">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="b4db8-135">Bazı yapılandırma güncelleştirme işlemleri hedef yapılandırma değişiklikleri güncelleştirme çalışan, diğerleri bunları kuyruğuna olabilir ve diğerleri ile bir hata koşulu reddedebilirsiniz sırada karşılamak mümkün olabilir.</span><span class="sxs-lookup"><span data-stu-id="b4db8-135">Some configuration update processes might be able to accommodate changes of target configuration while the update is running, others might have to queue them, and others could reject them with an error condition.</span></span> <span data-ttu-id="b4db8-136">Belirli bir yapılandırma işlemi için istenen davranışı dikkate aldığınızdan emin olun ve yapılandırma değişikliğini başlatmadan önce uygun mantığı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b4db8-136">Make sure to consider the desired behavior for your specific configuration process, and add the appropriate logic before initiating the configuration change.</span></span>
   > 
   > 
6. <span data-ttu-id="b4db8-137">Cihaz uygulaması çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b4db8-137">Run the device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="b4db8-138">Şu iletiyi görürsünüz `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="b4db8-138">You should see the message `retrieved device twin`.</span></span> <span data-ttu-id="b4db8-139">Uygulamayı çalıştıran tutun.</span><span class="sxs-lookup"><span data-stu-id="b4db8-139">Keep the app running.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="b4db8-140">Hizmet Uygulaması Oluştur</span><span class="sxs-lookup"><span data-stu-id="b4db8-140">Create the service app</span></span>
<span data-ttu-id="b4db8-141">Bu bölümde, güncelleştirmeleri bir Node.js konsol uygulaması oluşturacak *özelliklerini istenen* ilişkili cihaz çifti üzerinde **myDeviceId** ile yeni bir telemetri yapılandırma nesnesi.</span><span class="sxs-lookup"><span data-stu-id="b4db8-141">In this section, you will create a Node.js console app that updates the *desired properties* on the device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="b4db8-142">IOT hub'ı depolanan cihaz çiftlerini sorgular ve cihazın istenen ve bildirilen yapılandırmaları arasındaki farkı gösterir.</span><span class="sxs-lookup"><span data-stu-id="b4db8-142">It then queries the device twins stored in the IoT hub and shows the difference between the desired and reported configurations of the device.</span></span>

1. <span data-ttu-id="b4db8-143">Adlı yeni bir boş klasör oluşturun **setdesiredandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="b4db8-143">Create a new empty folder called **setdesiredandqueryapp**.</span></span> <span data-ttu-id="b4db8-144">İçinde **setdesiredandqueryapp** klasörü, komut isteminde aşağıdaki komutu kullanarak yeni bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b4db8-144">In the **setdesiredandqueryapp** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="b4db8-145">Tüm varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="b4db8-145">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="b4db8-146">Komut isteminizde **setdesiredandqueryapp** klasörü yüklemek için aşağıdaki komutu çalıştırın, **azure-iothub** paketi:</span><span class="sxs-lookup"><span data-stu-id="b4db8-146">At your command prompt in the **setdesiredandqueryapp** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. <span data-ttu-id="b4db8-147">Bir metin düzenleyicisi kullanarak yeni bir oluşturma **SetDesiredAndQuery.js** dosyasını **addtagsandqueryapp** klasör.</span><span class="sxs-lookup"><span data-stu-id="b4db8-147">Using a text editor, create a new **SetDesiredAndQuery.js** file in the **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="b4db8-148">Aşağıdaki kodu ekleyin **SetDesiredAndQuery.js** dosya ve yerine **{IOT hub bağlantı dizesine}** yer tutucu hub'ınızı oluşturduğunuzda kopyaladığınız IOT Hub bağlantı dizesine sahip:</span><span class="sxs-lookup"><span data-stu-id="b4db8-148">Add the following code to the **SetDesiredAndQuery.js** file, and substitute the **{iot hub connection string}** placeholder with the IoT Hub connection string you copied when you created your hub:</span></span>
   
        'use strict';
        var iothub = require('azure-iothub');
        var uuid = require('node-uuid');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var newConfigId = uuid.v4();
                var newFrequency = process.argv[2] || "5m";
                var patch = {
                    properties: {
                        desired: {
                            telemetryConfig: {
                                configId: newConfigId,
                                sendFrequency: newFrequency
                            }
                        }
                    }
                }
                twin.update(patch, function(err) {
                    if (err) {
                        console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                    } else {
                        console.log(twin.deviceId + ' twin updated successfully');
                    }
                });
                setInterval(queryTwins, 10000);
            }
        });

    <span data-ttu-id="b4db8-149">**Kayıt defteri** nesne cihaz çiftlerini hizmet ile etkileşim kurmak için gereken tüm yöntemleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="b4db8-149">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="b4db8-150">Bunu başlatır sonra önceki kod **kayıt defteri** nesnesi, cihaz çiftinin alır **myDeviceId**ve yeni bir telemetri yapılandırma nesnesi ile istenen özelliklerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="b4db8-150">The previous code, after it initializes the **Registry** object, retrieves the device twin for **myDeviceId**, and updates its desired properties with a new telemetry configuration object.</span></span> <span data-ttu-id="b4db8-151">Bundan sonra çağırır **queryTwins** 10 saniye olay işlev.</span><span class="sxs-lookup"><span data-stu-id="b4db8-151">After that, it calls the **queryTwins** function event 10 seconds.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b4db8-152">Bu uygulama yalnızca tanım amaçlıdır her 10 saniye IOT hub'ı sorgular.</span><span class="sxs-lookup"><span data-stu-id="b4db8-152">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="b4db8-153">Sorguları birçok cihaz arasında kullanıcı dönük raporları oluşturmak ve değil değişikliklerini algılamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="b4db8-153">Use queries to generate user-facing reports across many devices, and not to detect changes.</span></span> <span data-ttu-id="b4db8-154">Çözümünüz cihaz olayların gerçek zamanlı bildirimler gerektiriyorsa, kullanın [twin bildirimleri][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="b4db8-154">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
    > 
    ><span data-ttu-id="b4db8-155">.</span><span class="sxs-lookup"><span data-stu-id="b4db8-155">.</span></span>

1. <span data-ttu-id="b4db8-156">Aşağıdaki kod hemen önce eklemek `registry.getDeviceTwin()` uygulamak için çağırma **queryTwins** işlevi:</span><span class="sxs-lookup"><span data-stu-id="b4db8-156">Add the following code right before the `registry.getDeviceTwin()` invocation to implement the **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed to fetch the results: ' + err.message);
                } else {
                    console.log();
                    results.forEach(function(twin) {
                        var desiredConfig = twin.properties.desired.telemetryConfig;
                        var reportedConfig = twin.properties.reported.telemetryConfig;
                        console.log("Config report for: " + twin.deviceId);
                        console.log("Desired: ");
                        console.log(JSON.stringify(desiredConfig, null, 2));
                        console.log("Reported: ");
                        console.log(JSON.stringify(reportedConfig, null, 2));
                    });
                }
            });
        };
   
    <span data-ttu-id="b4db8-157">Önceki kod sorguları cihaz çiftlerini IOT hub'ı depolanan ve istenen ve bildirilen telemetri yapılandırmaları yazdırır.</span><span class="sxs-lookup"><span data-stu-id="b4db8-157">The previous code queries the device twins stored in the IoT hub and prints the desired and reported telemetry configurations.</span></span> <span data-ttu-id="b4db8-158">Başvurmak [IOT hub'ı sorgu dili] [ lnk-query] tüm cihazlarınızda zengin raporlar üretmek hakkında bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="b4db8-158">Refer to the [IoT Hub query language][lnk-query] to learn how to generate rich reports across all your devices.</span></span>
2. <span data-ttu-id="b4db8-159">İle **SimulateDeviceConfiguration.js** , uygulama ile çalıştırma:</span><span class="sxs-lookup"><span data-stu-id="b4db8-159">With **SimulateDeviceConfiguration.js** running, run the application with:</span></span>
   
        node SetDesiredAndQuery.js 5m
   
    <span data-ttu-id="b4db8-160">Bildirilen yapılandırma öğesinden değişikliği görmelisiniz **başarı** için **bekleyen** için **başarı** yeni etkin 24 saat yerine beş dakikalık sıklığı yeniden gönderin.</span><span class="sxs-lookup"><span data-stu-id="b4db8-160">You should see the reported configuration change from **Success** to **Pending** to **Success** again with the new active send frequency of five minutes instead of 24 hours.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="b4db8-161">Cihaz rapor işlemi ve sorgu sonucu arasında bir dakika kadar bir gecikme yoktur.</span><span class="sxs-lookup"><span data-stu-id="b4db8-161">There is a delay of up to a minute between the device report operation and the query result.</span></span> <span data-ttu-id="b4db8-162">Bu, çok yüksek ölçekli olarak çalışmak sorgu altyapısı olanak sağlamasıdır.</span><span class="sxs-lookup"><span data-stu-id="b4db8-162">This is to enable the query infrastructure to work at very high scale.</span></span> <span data-ttu-id="b4db8-163">Bir tek cihaz çifti kullanımı tutarlı görünümleri almak için **getDeviceTwin** yönteminde **kayıt defteri** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="b4db8-163">To retrieve consistent views of a single device twin use the **getDeviceTwin** method in the **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="b4db8-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b4db8-164">Next steps</span></span>
<span data-ttu-id="b4db8-165">Bu öğreticide, istenen yapılandırma olarak ayarlamak *özelliklerini istenen* bir arka uç uygulamasından ve bu değişikliği algılar ve durumunu olarak raporlama çok adımlı güncelleştirme işleminin benzetimini yapmak için bir sanal cihaz uygulaması yazdı  *Özellikler bildirilen* cihaz çifti için.</span><span class="sxs-lookup"><span data-stu-id="b4db8-165">In this tutorial, you set a desired configuration as *desired properties* from a back-end app, and wrote a simulated device app to detect that change and simulate a multi-step update process reporting its status as *reported properties* to the device twin.</span></span>

<span data-ttu-id="b4db8-166">Bilgi edinmek için aşağıdaki kaynakları kullanın nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="b4db8-166">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="b4db8-167">aygıtlarla telemetri gönderen [IOT Hub ile çalışmaya başlama] [ lnk-iothub-getstarted] öğretici</span><span class="sxs-lookup"><span data-stu-id="b4db8-167">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="b4db8-168">zamanlama veya aygıtları bakın büyük kümeleri işlemleri [zamanlama ve yayın işleri] [ lnk-schedule-jobs] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="b4db8-168">schedule or perform operations on large sets of devices see the [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="b4db8-169">ile etkileşimli olarak (örneğin, kullanıcı tarafından denetlenen bir uygulamadan fan etkinleştirdikten), cihazları denetleme [doğrudan yöntemleri kullanın] [ lnk-methods-tutorial] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="b4db8-169">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: iot-hub-device-management-overview.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-node-node-twin-how-to-configure.md#create-the-simulated-device-app
