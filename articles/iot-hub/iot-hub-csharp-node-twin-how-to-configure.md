---
title: "aaaUse Azure IOT Hub cihaz çifti özellikleri (.NET/düğümü) | Microsoft Docs"
description: "Nasıl toouse Azure IOT Hub cihaz tooconfigure cihaz çiftlerini. Node.js tooimplement sanal cihaz uygulaması için hello Azure IOT cihaz SDK'sı ve hello .NET tooimplement cihaz çifti kullanarak bir aygıt yapılandırmasını değiştirir bir hizmet uygulaması için Azure IOT hizmeti SDK'sını kullanın."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: elioda
ms.openlocfilehash: 840a1b2e45f4763131299577583aa89015dcdd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a><span data-ttu-id="debbe-104">İstenen özelliklerde tooconfigure aygıtları'nı kullanın</span><span class="sxs-lookup"><span data-stu-id="debbe-104">Use desired properties tooconfigure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="debbe-105">Bu öğreticinin Hello sonunda, iki konsol uygulamaları olacaktır:</span><span class="sxs-lookup"><span data-stu-id="debbe-105">At hello end of this tutorial, you will have two console apps:</span></span>

* <span data-ttu-id="debbe-106">**SimulateDeviceConfiguration.js**, istenen yapılandırma güncelleştirmesi bekler ve benzetimli yapılandırma güncellemeyi hello durumunu raporlar sanal cihaz uygulaması.</span><span class="sxs-lookup"><span data-stu-id="debbe-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="debbe-107">**SetDesiredConfigurationAndQuery**hello ayarlar .NET arka uç uygulaması istenen bir cihazda yapılandırma ve sorguları hello yapılandırma güncelleştirme işlemi.</span><span class="sxs-lookup"><span data-stu-id="debbe-107">**SetDesiredConfigurationAndQuery**, a .NET back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="debbe-108">Merhaba makale [Azure IOT SDK'ları] [ lnk-hub-sdks] toobuild kullanabileceğiniz hello Azure IOT SDK'ları hakkında bilgi sağlayan cihaz ve arka uç uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="debbe-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="debbe-109">toocomplete hello aşağıdaki gereksinim Bu öğretici:</span><span class="sxs-lookup"><span data-stu-id="debbe-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="debbe-110">Visual Studio 2015 veya Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="debbe-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="debbe-111">Node.js 0.10.x sürümü veya sonraki bir sürüm.</span><span class="sxs-lookup"><span data-stu-id="debbe-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="debbe-112">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="debbe-112">An active Azure account.</span></span> <span data-ttu-id="debbe-113">Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="debbe-113">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="debbe-114">Merhaba izlediyseniz [cihaz çiftlerini ile çalışmaya başlama] [ lnk-twin-tutorial] öğretici, zaten sahip olduğunuz bir IOT hub ve adlı bir cihaz kimliği **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="debbe-114">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="debbe-115">Bu durumda, toohello atlayabilirsiniz [oluşturma hello sanal cihaz uygulamasının] [ lnk-how-to-configure-createapp] bölümü.</span><span class="sxs-lookup"><span data-stu-id="debbe-115">In that case, you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="debbe-116">Merhaba sanal cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="debbe-116">Create hello simulated device app</span></span>
<span data-ttu-id="debbe-117">Bu bölümde, tooyour hub olarak bağlanan bir Node.js konsol uygulaması oluşturma **myDeviceId**, istenen yapılandırma güncelleştirmesi bekler ve daha sonra güncelleştirmeleri benzetimli hello yapılandırmasını güncelleştirme işlemi raporlar.</span><span class="sxs-lookup"><span data-stu-id="debbe-117">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="debbe-118">Adlı yeni bir boş klasör oluşturun **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="debbe-118">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="debbe-119">Merhaba, **simulatedeviceconfiguration** klasörü, komut, komut isteminde aşağıdaki hello kullanarak yeni bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="debbe-119">In hello **simulatedeviceconfiguration** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="debbe-120">Tüm hello Varsayılanları kabul edin.</span><span class="sxs-lookup"><span data-stu-id="debbe-120">Accept all hello defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="debbe-121">Merhaba, komut isteminde **simulatedeviceconfiguration** klasörüne, komut tooinstall hello aşağıdaki hello **azure IOT cihaz** ve **azure-IOT-cihaz-mqtt**paketler:</span><span class="sxs-lookup"><span data-stu-id="debbe-121">At your command prompt in hello **simulatedeviceconfiguration** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="debbe-122">Bir metin düzenleyicisi kullanarak yeni bir oluşturma **SimulateDeviceConfiguration.js** hello dosyasında **simulatedeviceconfiguration** klasör.</span><span class="sxs-lookup"><span data-stu-id="debbe-122">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in hello **simulatedeviceconfiguration** folder.</span></span>
1. <span data-ttu-id="debbe-123">Kod toohello aşağıdaki hello eklemek **SimulateDeviceConfiguration.js** dosya ve hello yerine **{cihaz bağlantı dizesi}** ne zaman kopyaladığınız hello cihaz bağlantı dizesiyle yer tutucu, Merhaba oluşturulan **myDeviceId** cihaz kimliği:</span><span class="sxs-lookup"><span data-stu-id="debbe-123">Add hello following code toohello **SimulateDeviceConfiguration.js** file, and substitute hello **{device connection string}** placeholder with hello device connection string you copied when you created hello **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="debbe-124">Merhaba **istemci** nesne cihaz çiftlerini hello aygıttan ile tüm hello yöntemleri gerekli toointeract kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="debbe-124">hello **Client** object exposes all hello methods required toointeract with device twins from hello device.</span></span> <span data-ttu-id="debbe-125">Bu kod hello başlatır **istemci** nesnesi alır, cihaz çiftinin hello **myDeviceId**ve üzerinde hello güncelleştirme için bir işleyici ekler *özelliklerini istenen*.</span><span class="sxs-lookup"><span data-stu-id="debbe-125">This code initializes hello **Client** object, retrieves hello device twin for **myDeviceId**, and then attaches a handler for hello update on *desired properties*.</span></span> <span data-ttu-id="debbe-126">Merhaba işleyici olmadığını hello configIds karşılaştırarak bir gerçek yapılandırma değişikliği isteği olup, ardından hello yapılandırmasında değişiklik başlatan bir yöntemi çağırır doğrular.</span><span class="sxs-lookup"><span data-stu-id="debbe-126">hello handler verifies that there is an actual configuration change request by comparing hello configIds, then invokes a method that starts hello configuration change.</span></span>
   
    <span data-ttu-id="debbe-127">Basitlik Hello artırmak amacıyla için bu kodu sabit kodlanmış bir varsayılan hello ilk yapılandırmasını kullandığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="debbe-127">Note that for hello sake of simplicity, this code uses a hard-coded default for hello initial configuration.</span></span> <span data-ttu-id="debbe-128">Gerçek bir uygulama büyük olasılıkla bu yapılandırma yerel depolama biriminden yüklenir.</span><span class="sxs-lookup"><span data-stu-id="debbe-128">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="debbe-129">İstenen özellik değiştirme olayları her zaman bir kez aygıt bağlantıdaki gösterilen.</span><span class="sxs-lookup"><span data-stu-id="debbe-129">Desired property change events are always emitted once at device connection.</span></span> <span data-ttu-id="debbe-130">Herhangi bir işlem gerçekleştirmeden önce özellikleri hello gerçek bir değişiklik olduğunu toocheck istenen emin olun.</span><span class="sxs-lookup"><span data-stu-id="debbe-130">Make sure toocheck that there is an actual change in hello desired properties before performing any action.</span></span>
   > 
   > 
1. <span data-ttu-id="debbe-131">Merhaba önce yöntemler aşağıdaki hello eklemek `client.open()` çağırma:</span><span class="sxs-lookup"><span data-stu-id="debbe-131">Add hello following methods before hello `client.open()` invocation:</span></span>
   
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
   
    <span data-ttu-id="debbe-132">Merhaba **initConfigChange** yöntemi güncelleştirmeleri hello bildirilen nesnesindeki özellikleri hello yerel cihaz çifti hello yapılandırmasıyla güncelleştirme isteği ve kümelerini hello durumu çok**bekleyen**, sonra güncelleştirmeleri hello cihaz çifti hello hizmeti.</span><span class="sxs-lookup"><span data-stu-id="debbe-132">hello **initConfigChange** method updates hello reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="debbe-133">Merhaba cihaz çifti başarıyla güncelleştirdikten sonra içinde hello yürütülmesi sonlandırır uzun süre çalışan bir işlem benzetim **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="debbe-133">After successfully updating hello device twin, it simulates a long running process that terminates in hello execution of **completeConfigChange**.</span></span> <span data-ttu-id="debbe-134">Bu yöntem hello yerel bildirilen özellikleri hello durumu çok ayarlanırken güncelleştirmeleri**başarı** ve hello kaldırma **pendingConfig** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="debbe-134">This method updates hello local reported properties setting hello status too**Success** and removing hello **pendingConfig** object.</span></span> <span data-ttu-id="debbe-135">Ardından, hello cihaz çifti hello hizmetinde güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="debbe-135">It then updates hello device twin on hello service.</span></span>
   
    <span data-ttu-id="debbe-136">Toosave bant genişliği, rapor özelliklerini yalnızca hello özellikleri toobe değiştiren belirterek güncelleştirilir unutmayın (adlı **düzeltme eki** kodu yukarıdaki hello içinde), hello tüm belgeyi değiştirme yerine.</span><span class="sxs-lookup"><span data-stu-id="debbe-136">Note that, toosave bandwidth, reported properties are updated by specifying only hello properties toobe modified (named **patch** in hello above code), instead of replacing hello whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="debbe-137">Bu öğretici herhangi davranışı eşzamanlı yapılandırma güncelleştirmelerini benzetimini değil.</span><span class="sxs-lookup"><span data-stu-id="debbe-137">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="debbe-138">Merhaba güncelleştirme çalışırken bazı yapılandırma güncelleştirme işlemleri hedef yapılandırmasının mümkün tooaccommodate değişiklikler olabilir, bazı ve bazı bunları bir hata durumu reddedebilirsiniz tooqueue olabilir.</span><span class="sxs-lookup"><span data-stu-id="debbe-138">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, some might have tooqueue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="debbe-139">Belirli bir yapılandırma işlemi için istenen davranışı hello ve hello yapılandırma değişikliği başlatmadan önce hello uygun mantığı ekleyin emin tooconsider olun.</span><span class="sxs-lookup"><span data-stu-id="debbe-139">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="debbe-140">Merhaba cihaz uygulaması çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="debbe-140">Run hello device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="debbe-141">Merhaba iletiyi görmeniz gerekir `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="debbe-141">You should see hello message `retrieved device twin`.</span></span> <span data-ttu-id="debbe-142">Çalışan hello uygulama tutun.</span><span class="sxs-lookup"><span data-stu-id="debbe-142">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="debbe-143">Merhaba service uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="debbe-143">Create hello service app</span></span>
<span data-ttu-id="debbe-144">Bu bölümde, bu güncelleştirmeleri hello bir .NET konsol uygulaması oluşturacak *özelliklerini istenen* hello cihaz çifti ile ilişkili üzerinde **myDeviceId** ile yeni bir telemetri yapılandırma nesnesi.</span><span class="sxs-lookup"><span data-stu-id="debbe-144">In this section, you will create a .NET console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="debbe-145">Ardından hello IOT hub'da depolanan hello cihaz çiftlerini sorgular ve hello hello birbirinden istenen ve hello cihaz yapılandırmalarını bildirilen gösterir.</span><span class="sxs-lookup"><span data-stu-id="debbe-145">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="debbe-146">Visual Studio'da hello kullanarak bir Visual C# Windows Klasik Masaüstü projesi toohello geçerli çözüme ekleyin **konsol uygulaması** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="debbe-146">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="debbe-147">Ad hello proje **SetDesiredConfigurationAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="debbe-147">Name hello project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![Yeni Visual C# Windows Klasik Masaüstü projesi][img-createapp]
1. <span data-ttu-id="debbe-149">Çözüm Gezgini'nde hello sağ **SetDesiredConfigurationAndQuery** proje ve ardından **NuGet paketlerini Yönet...** .</span><span class="sxs-lookup"><span data-stu-id="debbe-149">In Solution Explorer, right-click hello **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="debbe-150">Merhaba, **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat**, arama **microsoft.azure.devices**seçin **yükleme** tooinstall Merhaba **Microsoft.Azure.Devices** paketini ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="debbe-150">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="debbe-151">Bu yordam indirir, yükler ve başvuru toohello ekler [Azure IOT hizmeti SDK'sını] [ lnk-nuget-service-sdk] NuGet paketi ve bağımlılıklarını.</span><span class="sxs-lookup"><span data-stu-id="debbe-151">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet Paket Yöneticisi penceresi][img-servicenuget]
1. <span data-ttu-id="debbe-153">Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:</span><span class="sxs-lookup"><span data-stu-id="debbe-153">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="debbe-154">Aşağıdaki alanları toohello hello eklemek **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="debbe-154">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="debbe-155">Merhaba hello önceki bölümde oluşturduğunuz hello hub'ın IOT Hub bağlantı dizesine sahip Hello yer tutucu değerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="debbe-155">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="debbe-156">Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="debbe-156">Add hello following method toohello **Program** class:</span></span>
   
        static private async Task SetDesiredConfigurationAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch = new {
                    properties = new {
                        desired = new {
                            telemetryConfig = new {
                                configId = Guid.NewGuid().ToString(),
                                sendFrequency = "5m"
                            }
                        }
                    }
                };
   
            await registryManager.UpdateTwinAsync(twin.DeviceId, JsonConvert.SerializeObject(patch), twin.ETag);
            Console.WriteLine("Updated desired configuration");
   
            try
            {
                while (true)
                {
                    var query = registryManager.CreateQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'");
                    var results = await query.GetNextAsTwinAsync();
                    foreach (var result in results)
                    {
                        Console.WriteLine("Config report for: {0}", result.DeviceId);
                        Console.WriteLine("Desired telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Desired["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine("Reported telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Reported["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine();
                    }
                    Thread.Sleep(10000);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Exception: {ex.Message}");
            }
        }
   
    <span data-ttu-id="debbe-157">Merhaba **kayıt defteri** nesne cihaz çiftlerini hello hizmetinden ile tüm hello yöntemleri gerekli toointeract kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="debbe-157">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="debbe-158">Bu kod hello başlatır **kayıt defteri** nesnesi alır, cihaz çiftinin hello **myDeviceId**ve ardından yeni bir telemetri yapılandırma nesnesi ile istenen özelliklerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="debbe-158">This code initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="debbe-159">Bundan sonra 10 saniyede hello IOT hub'da depolanan hello cihaz çiftlerini sorgular ve baskı siparişi hello istenen ve telemetri yapılandırmaları bildirdi.</span><span class="sxs-lookup"><span data-stu-id="debbe-159">After that, it queries hello device twins stored in hello IoT hub every 10 seconds, and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="debbe-160">Toohello başvuran [IOT hub'ı sorgu dili] [ lnk-query] nasıl toogenerate zengin raporları, tüm aygıtlarda toolearn.</span><span class="sxs-lookup"><span data-stu-id="debbe-160">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="debbe-161">Bu uygulama yalnızca tanım amaçlıdır her 10 saniye IOT hub'ı sorgular.</span><span class="sxs-lookup"><span data-stu-id="debbe-161">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="debbe-162">Kullanım toogenerate kullanıcı dönük raporları birçok cihaz ve toodetect değişiklikleri arasında sorgular.</span><span class="sxs-lookup"><span data-stu-id="debbe-162">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="debbe-163">Çözümünüz cihaz olayların gerçek zamanlı bildirimler gerektiriyorsa, kullanın [twin bildirimleri][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="debbe-163">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="debbe-164">Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="debbe-164">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery().Wait();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. <span data-ttu-id="debbe-165">Merhaba Hello Çözüm Gezgini, açık **başlangıç projelerini Ayarla...**  ve emin hello **eylem** için **SetDesiredConfigurationAndQuery** projedir **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="debbe-165">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="debbe-166">Merhaba çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="debbe-166">Build hello solution.</span></span>
1. <span data-ttu-id="debbe-167">İle **SimulateDeviceConfiguration.js** , Merhaba .NET uygulaması Visual Studio kullanarak çalıştırma **F5** ve hello bildirilen yapılandırma çıkarılıp görmelisiniz. **başarı** çok**bekleyen** çok**başarı** hello yeni etkin ile 24 saat yerine beş dakikalık sıklığı yeniden gönderin.</span><span class="sxs-lookup"><span data-stu-id="debbe-167">With **SimulateDeviceConfiguration.js** running, run hello .NET application from Visual Studio using **F5** and you should see hello reported configuration change from **Success** too**Pending** too**Success** again with hello new active send frequency of five minutes instead of 24 hours.</span></span>

 ![Cihaz başarıyla yapılandırıldı][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="debbe-169">Merhaba aygıt rapor işlemi hello sorgu sonucu arasındaki tooa minute yukarı bir gecikme yoktur.</span><span class="sxs-lookup"><span data-stu-id="debbe-169">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="debbe-170">Çok yüksek ölçekli tooenable hello sorgu altyapısı toowork budur.</span><span class="sxs-lookup"><span data-stu-id="debbe-170">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="debbe-171">tooretrieve tutarlı bir tek cihaz çifti görünümlerini kullanın hello **getDeviceTwin** hello yönteminde **kayıt defteri** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="debbe-171">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="debbe-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="debbe-172">Next steps</span></span>
<span data-ttu-id="debbe-173">Bu öğreticide, istenen yapılandırma olarak kümesi *özellikleri istenen* hello çözümden arka uç ve değiştirebilir ve durumunu bildirilen hello aracılığıyla raporlama çok adımlı güncelleştirme işleminin benzetimini cihaz uygulama toodetect yazıldı Özellikler.</span><span class="sxs-lookup"><span data-stu-id="debbe-173">In this tutorial, you set a desired configuration as *desired properties* from hello solution back end, and wrote a device app toodetect that change and simulate a multi-step update process reporting its status through hello reported properties.</span></span>

<span data-ttu-id="debbe-174">Kaynakları toolearn nasıl aşağıdaki kullanım hello için:</span><span class="sxs-lookup"><span data-stu-id="debbe-174">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="debbe-175">Merhaba aygıtlarla telemetri gönderen [IOT Hub ile çalışmaya başlama] [ lnk-iothub-getstarted] öğretici</span><span class="sxs-lookup"><span data-stu-id="debbe-175">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="debbe-176">zamanlama veya gerçekleştirmek aygıtların büyük kümeleri üzerinde işlemler bkz hello [zamanlama ve yayın işleri] [ lnk-schedule-jobs] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="debbe-176">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="debbe-177">Merhaba ile etkileşimli olarak (örneğin, kullanıcı tarafından denetlenen bir uygulamadan fan etkinleştirdikten), cihazları denetleme [doğrudan yöntemleri kullanın] [ lnk-methods-tutorial] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="debbe-177">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-node-twin-how-to-configure/deviceconfigured.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

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
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-csharp-node-twin-how-to-configure.md#create-the-simulated-device-app
