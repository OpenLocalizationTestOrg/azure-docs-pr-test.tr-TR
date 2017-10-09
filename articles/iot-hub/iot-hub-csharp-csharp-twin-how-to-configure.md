---
title: "aaaUse Azure IOT Hub cihaz çifti özellikleri (.NET/.NET) | Microsoft Docs"
description: "Nasıl toouse Azure IOT Hub cihaz tooconfigure cihaz çiftlerini. .NET tooimplement sanal cihaz uygulaması için hello Azure IOT cihaz SDK'sı ve hello .NET tooimplement cihaz çifti kullanarak bir aygıt yapılandırmasını değiştirir bir hizmet uygulaması için Azure IOT hizmeti SDK'sını kullanın."
services: iot-hub
documentationcenter: .net
author: dsk-2015
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: dkshir
ms.openlocfilehash: 486436d29abfd5158c253adc5abf5935e0e1fdba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a><span data-ttu-id="fa35b-104">İstenen özelliklerde tooconfigure aygıtları'nı kullanın</span><span class="sxs-lookup"><span data-stu-id="fa35b-104">Use desired properties tooconfigure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="fa35b-105">Bu öğreticinin Hello sonunda, iki .NET konsol uygulamaları olacaktır:</span><span class="sxs-lookup"><span data-stu-id="fa35b-105">At hello end of this tutorial, you will have two .NET console apps:</span></span>

* <span data-ttu-id="fa35b-106">**SimulateDeviceConfiguration**, istenen yapılandırma güncelleştirmesi bekler ve benzetimli yapılandırma güncellemeyi hello durumunu raporlar sanal cihaz uygulaması.</span><span class="sxs-lookup"><span data-stu-id="fa35b-106">**SimulateDeviceConfiguration**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="fa35b-107">**SetDesiredConfigurationAndQuery**hello ayarlar bir arka uç uygulaması istenen bir cihazda yapılandırma ve sorguları hello yapılandırma güncelleştirme işlemi.</span><span class="sxs-lookup"><span data-stu-id="fa35b-107">**SetDesiredConfigurationAndQuery**, a back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="fa35b-108">Merhaba makale [Azure IOT SDK'ları] [ lnk-hub-sdks] toobuild kullanabileceğiniz hello Azure IOT SDK'ları hakkında bilgi sağlayan cihaz ve arka uç uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="fa35b-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="fa35b-109">toocomplete hello aşağıdaki gereksinim Bu öğretici:</span><span class="sxs-lookup"><span data-stu-id="fa35b-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="fa35b-110">Visual Studio 2015 veya Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="fa35b-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="fa35b-111">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="fa35b-111">An active Azure account.</span></span> <span data-ttu-id="fa35b-112">Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa35b-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="fa35b-113">Merhaba izlediyseniz [cihaz çiftlerini ile çalışmaya başlama] [ lnk-twin-tutorial] öğretici, zaten sahip olduğunuz bir IOT hub ve adlı bir cihaz kimliği **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="fa35b-113">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="fa35b-114">Bu durumda, toohello atlayabilirsiniz [oluşturma hello sanal cihaz uygulamasının] [ lnk-how-to-configure-createapp] bölümü.</span><span class="sxs-lookup"><span data-stu-id="fa35b-114">In that case, you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="fa35b-115">Merhaba sanal cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa35b-115">Create hello simulated device app</span></span>
<span data-ttu-id="fa35b-116">Bu bölümde, tooyour hub olarak bağlanan bir .NET konsol uygulaması oluşturma **myDeviceId**, istenen yapılandırma güncelleştirmesi bekler ve daha sonra güncelleştirmeleri benzetimli hello yapılandırmasını güncelleştirme işlemi raporlar.</span><span class="sxs-lookup"><span data-stu-id="fa35b-116">In this section, you create a .NET console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="fa35b-117">Visual Studio'da hello kullanarak yeni bir Visual C# Windows Klasik Masaüstü projesi oluşturma **konsol uygulaması** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="fa35b-117">In Visual Studio, create a new Visual C# Windows Classic Desktop project by using hello **Console Application** project template.</span></span> <span data-ttu-id="fa35b-118">Ad hello proje **SimulateDeviceConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="fa35b-118">Name hello project **SimulateDeviceConfiguration**.</span></span>
   
    ![Yeni Visual C# Klasik Windows cihaz uygulaması][img-createdeviceapp]

1. <span data-ttu-id="fa35b-120">Çözüm Gezgini'nde hello sağ **SimulateDeviceConfiguration** proje ve ardından **NuGet paketlerini Yönet...** .</span><span class="sxs-lookup"><span data-stu-id="fa35b-120">In Solution Explorer, right-click hello **SimulateDeviceConfiguration** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="fa35b-121">Merhaba, **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat** arayın ve **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="fa35b-121">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="fa35b-122">Seçin **yükleme** tooinstall hello **Microsoft.Azure.Devices.Client** paketini ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="fa35b-122">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="fa35b-123">Bu yordam indirir, yükler ve başvuru toohello ekler [Azure IOT cihaz SDK'sı] [ lnk-nuget-client-sdk] NuGet paketi ve bağımlılıklarını.</span><span class="sxs-lookup"><span data-stu-id="fa35b-123">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet Paket Yöneticisi penceresi istemci uygulaması][img-clientnuget]
1. <span data-ttu-id="fa35b-125">Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:</span><span class="sxs-lookup"><span data-stu-id="fa35b-125">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="fa35b-126">Aşağıdaki alanları toohello hello eklemek **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="fa35b-126">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="fa35b-127">Merhaba yer tutucu değerini hello önceki bölümünde belirtildiği hello cihaz bağlantı dizesini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="fa35b-127">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;
        static TwinCollection reportedProperties = new TwinCollection();

1. <span data-ttu-id="fa35b-128">Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="fa35b-128">Add hello following method toohello **Program** class:</span></span>
 
        public static void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }
    <span data-ttu-id="fa35b-129">Merhaba **istemci** nesne cihaz çiftlerini hello aygıttan ile toointeract duyduğunuz tüm hello yöntemler sunar.</span><span class="sxs-lookup"><span data-stu-id="fa35b-129">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="fa35b-130">Merhaba, yukarıda gösterilen kodu başlatır hello **istemci** nesne ve alır hello cihaz çiftinin **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="fa35b-130">hello code shown above, initializes hello **Client** object, and then retrieves hello device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="fa35b-131">Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="fa35b-131">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="fa35b-132">Bu yöntem hello başlangıç değerleri telemetri hello yerel cihazda ayarlar ve ardından güncelleştirmeleri cihaz çifti hello.</span><span class="sxs-lookup"><span data-stu-id="fa35b-132">This method sets hello initial values of telemetry on hello local device and then updates hello device twin.</span></span>

        public static async void InitTelemetry()
        {
            try
            {
                Console.WriteLine("Report initial telemetry config:");
                TwinCollection telemetryConfig = new TwinCollection();
                
                telemetryConfig["configId"] = "0";
                telemetryConfig["sendFrequency"] = "24h";
                reportedProperties["telemetryConfig"] = telemetryConfig;
                Console.WriteLine(JsonConvert.SerializeObject(reportedProperties));

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. <span data-ttu-id="fa35b-133">Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="fa35b-133">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="fa35b-134">Bu değişikliği algılar bir geri çağırma olduğu *özelliklerini istenen* hello cihaz çiftine.</span><span class="sxs-lookup"><span data-stu-id="fa35b-134">This is a callback which will detect a change in *desired properties* in hello device twin.</span></span>

        private static async Task OnDesiredPropertyChanged(TwinCollection desiredProperties, object userContext)
        {
            try
            {
                Console.WriteLine("Desired property change:");
                Console.WriteLine(JsonConvert.SerializeObject(desiredProperties));

                var currentTelemetryConfig = reportedProperties["telemetryConfig"];
                var desiredTelemetryConfig = desiredProperties["telemetryConfig"];

                if ((desiredTelemetryConfig != null) && (desiredTelemetryConfig["configId"] != currentTelemetryConfig["configId"]))
                {
                    Console.WriteLine("\nInitiating config change");
                    currentTelemetryConfig["status"] = "Pending";
                    currentTelemetryConfig["pendingConfig"] = desiredTelemetryConfig;

                    await Client.UpdateReportedPropertiesAsync(reportedProperties);

                    CompleteConfigChange();
                }
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    <span data-ttu-id="fa35b-135">Bu yöntem güncelleştirmeleri hello bildirilen nesnesindeki özellikleri hello yerel cihaz çifti hello yapılandırmasıyla güncelleştirme isteği ve kümelerini hello durumu çok**bekleyen**, cihaz çifti hello hizmetinde güncelleştirmeleri hello sonra.</span><span class="sxs-lookup"><span data-stu-id="fa35b-135">This method updates hello reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="fa35b-136">Merhaba cihaz çifti başarıyla güncelleştirdikten sonra hello yapılandırma değişikliği hello yöntemini çağırarak tamamlanmadan `CompleteConfigChange` hello sonraki noktasında açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="fa35b-136">After successfully updating hello device twin, it completes hello config change by calling hello method `CompleteConfigChange` described in hello next point.</span></span>

1. <span data-ttu-id="fa35b-137">Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="fa35b-137">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="fa35b-138">Bu yöntem bir cihaz sıfırlama benzetimini yapar, sonra güncelleştirmeleri hello hello durumu çok ayarı yerel bildirilen özellikleri**başarı** ve kaldırır hello **pendingConfig** öğesi.</span><span class="sxs-lookup"><span data-stu-id="fa35b-138">This method simulates a device reset, then updates hello local reported properties setting hello status too**Success** and removes hello **pendingConfig** element.</span></span> <span data-ttu-id="fa35b-139">Ardından, hello cihaz çifti hello hizmetinde güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="fa35b-139">It then updates hello device twin on hello service.</span></span> 

        public static async void CompleteConfigChange()
        {
            try
            {
                var currentTelemetryConfig = reportedProperties["telemetryConfig"];

                Console.WriteLine("\nSimulating device reset");
                await Task.Delay(30000); 

                Console.WriteLine("\nCompleting config change");
                currentTelemetryConfig["configId"] = currentTelemetryConfig["pendingConfig"]["configId"];
                currentTelemetryConfig["sendFrequency"] = currentTelemetryConfig["pendingConfig"]["sendFrequency"];
                currentTelemetryConfig["status"] = "Success";
                currentTelemetryConfig["pendingConfig"] = null;

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
                Console.WriteLine("Config change complete \nPress any key tooexit.");
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. <span data-ttu-id="fa35b-140">Son satırları toohello aşağıdaki hello ekleyin **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="fa35b-140">Finally add hello following lines toohello **Main** method:</span></span>

        try
        {
            InitClient();
            InitTelemetry();

            Console.WriteLine("Wait for desired telemetry...");
            Client.SetDesiredPropertyUpdateCallback(OnDesiredPropertyChanged, null).Wait();
            Console.ReadKey();
        }
        catch (AggregateException ex)
        {
            foreach (Exception exception in ex.InnerExceptions)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", exception);
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }

   > [!NOTE]
   > <span data-ttu-id="fa35b-141">Bu öğretici herhangi davranışı eşzamanlı yapılandırma güncelleştirmelerini benzetimini değil.</span><span class="sxs-lookup"><span data-stu-id="fa35b-141">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="fa35b-142">Merhaba güncelleştirme çalışırken bazı yapılandırma güncelleştirme işlemleri hedef yapılandırmasının mümkün tooaccommodate değişiklikler olabilir, bazı ve bazı bunları bir hata durumu reddedebilirsiniz tooqueue olabilir.</span><span class="sxs-lookup"><span data-stu-id="fa35b-142">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, some might have tooqueue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="fa35b-143">Belirli bir yapılandırma işlemi için istenen davranışı hello ve hello yapılandırma değişikliği başlatmadan önce hello uygun mantığı ekleyin emin tooconsider olun.</span><span class="sxs-lookup"><span data-stu-id="fa35b-143">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="fa35b-144">Hello çözümü oluşturmak ve ardından hello cihaz uygulaması tıklayarak Visual Studio'dan çalıştırma **F5**.</span><span class="sxs-lookup"><span data-stu-id="fa35b-144">Build hello solution and then run hello device app from Visual Studio by clicking **F5**.</span></span> <span data-ttu-id="fa35b-145">Merhaba çıkış konsolda sanal cihazınız hello cihaz çifti alma, hello telemetri ayarlama ve istenen özellik değişikliği için bekleyen belirten Merhaba iletileri görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa35b-145">On hello output console, you should see hello messages indicating that your simulated device is retrieving hello device twin, setting up hello telemetry, and waiting for desired property change.</span></span> <span data-ttu-id="fa35b-146">Çalışan hello uygulama tutun.</span><span class="sxs-lookup"><span data-stu-id="fa35b-146">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="fa35b-147">Merhaba service uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa35b-147">Create hello service app</span></span>
<span data-ttu-id="fa35b-148">Bu bölümde, bu güncelleştirmeleri hello bir .NET konsol uygulaması oluşturacak *özelliklerini istenen* hello cihaz çifti ile ilişkili üzerinde **myDeviceId** ile yeni bir telemetri yapılandırma nesnesi.</span><span class="sxs-lookup"><span data-stu-id="fa35b-148">In this section, you will create a .NET console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="fa35b-149">Ardından hello IOT hub'da depolanan hello cihaz çiftlerini sorgular ve hello hello birbirinden istenen ve hello cihaz yapılandırmalarını bildirilen gösterir.</span><span class="sxs-lookup"><span data-stu-id="fa35b-149">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="fa35b-150">Visual Studio'da hello kullanarak bir Visual C# Windows Klasik Masaüstü projesi toohello geçerli çözüme ekleyin **konsol uygulaması** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="fa35b-150">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="fa35b-151">Ad hello proje **SetDesiredConfigurationAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="fa35b-151">Name hello project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![Yeni Visual C# Windows Klasik Masaüstü projesi][img-createapp]
1. <span data-ttu-id="fa35b-153">Çözüm Gezgini'nde hello sağ **SetDesiredConfigurationAndQuery** proje ve ardından **NuGet paketlerini Yönet...** .</span><span class="sxs-lookup"><span data-stu-id="fa35b-153">In Solution Explorer, right-click hello **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="fa35b-154">Merhaba, **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat**, arama **microsoft.azure.devices**seçin **yükleme** tooinstall Merhaba **Microsoft.Azure.Devices** paketini ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="fa35b-154">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="fa35b-155">Bu yordam indirir, yükler ve başvuru toohello ekler [Azure IOT hizmeti SDK'sını] [ lnk-nuget-service-sdk] NuGet paketi ve bağımlılıklarını.</span><span class="sxs-lookup"><span data-stu-id="fa35b-155">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet Paket Yöneticisi penceresi][img-servicenuget]
1. <span data-ttu-id="fa35b-157">Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:</span><span class="sxs-lookup"><span data-stu-id="fa35b-157">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="fa35b-158">Aşağıdaki alanları toohello hello eklemek **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="fa35b-158">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="fa35b-159">Merhaba hello önceki bölümde oluşturduğunuz hello hub'ın IOT Hub bağlantı dizesine sahip Hello yer tutucu değerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="fa35b-159">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="fa35b-160">Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="fa35b-160">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="fa35b-161">Merhaba **kayıt defteri** nesne cihaz çiftlerini hello hizmetinden ile tüm hello yöntemleri gerekli toointeract kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="fa35b-161">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="fa35b-162">Bu kod hello başlatır **kayıt defteri** nesnesi alır, cihaz çiftinin hello **myDeviceId**ve ardından yeni bir telemetri yapılandırma nesnesi ile istenen özelliklerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="fa35b-162">This code initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="fa35b-163">Bundan sonra 10 saniyede hello IOT hub'da depolanan hello cihaz çiftlerini sorgular ve baskı siparişi hello istenen ve telemetri yapılandırmaları bildirdi.</span><span class="sxs-lookup"><span data-stu-id="fa35b-163">After that, it queries hello device twins stored in hello IoT hub every 10 seconds, and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="fa35b-164">Toohello başvuran [IOT hub'ı sorgu dili] [ lnk-query] nasıl toogenerate zengin raporları, tüm aygıtlarda toolearn.</span><span class="sxs-lookup"><span data-stu-id="fa35b-164">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="fa35b-165">Bu uygulama yalnızca tanım amaçlıdır her 10 saniye IOT hub'ı sorgular.</span><span class="sxs-lookup"><span data-stu-id="fa35b-165">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="fa35b-166">Kullanım toogenerate kullanıcı dönük raporları birçok cihaz ve toodetect değişiklikleri arasında sorgular.</span><span class="sxs-lookup"><span data-stu-id="fa35b-166">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="fa35b-167">Çözümünüz cihaz olayların gerçek zamanlı bildirimler gerektiriyorsa, kullanın [twin bildirimleri][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="fa35b-167">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="fa35b-168">Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="fa35b-168">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. <span data-ttu-id="fa35b-169">Merhaba Hello Çözüm Gezgini, açık **başlangıç projelerini Ayarla...**  ve emin hello **eylem** için **SetDesiredConfigurationAndQuery** projedir **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="fa35b-169">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="fa35b-170">Merhaba çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fa35b-170">Build hello solution.</span></span>
1. <span data-ttu-id="fa35b-171">İle **SimulateDeviceConfiguration** cihaz uygulamasının çalışıyor, Visual Studio kullanarak çalışma hello service uygulaması **F5**.</span><span class="sxs-lookup"><span data-stu-id="fa35b-171">With **SimulateDeviceConfiguration** device app running, run hello service app from Visual Studio using **F5**.</span></span> <span data-ttu-id="fa35b-172">Merhaba bildirilen yapılandırma çıkarılıp görmelisiniz **bekleyen** çok**başarı** hello yeni etkin ile 24 saat yerine beş dakikalık sıklığı Gönder.</span><span class="sxs-lookup"><span data-stu-id="fa35b-172">You should see hello reported configuration change from **Pending** too**Success** with hello new active send frequency of five minutes instead of 24 hours.</span></span>

 ![Cihaz başarıyla yapılandırıldı][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="fa35b-174">Merhaba aygıt rapor işlemi hello sorgu sonucu arasındaki tooa minute yukarı bir gecikme yoktur.</span><span class="sxs-lookup"><span data-stu-id="fa35b-174">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="fa35b-175">Çok yüksek ölçekli tooenable hello sorgu altyapısı toowork budur.</span><span class="sxs-lookup"><span data-stu-id="fa35b-175">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="fa35b-176">tooretrieve tutarlı bir tek cihaz çifti görünümlerini kullanın hello **getDeviceTwin** hello yönteminde **kayıt defteri** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="fa35b-176">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="fa35b-177">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fa35b-177">Next steps</span></span>
<span data-ttu-id="fa35b-178">Bu öğreticide, istenen yapılandırma olarak kümesi *özellikleri istenen* hello çözümden arka uç ve değiştirebilir ve durumunu bildirilen hello aracılığıyla raporlama çok adımlı güncelleştirme işleminin benzetimini cihaz uygulama toodetect yazıldı Özellikler.</span><span class="sxs-lookup"><span data-stu-id="fa35b-178">In this tutorial, you set a desired configuration as *desired properties* from hello solution back end, and wrote a device app toodetect that change and simulate a multi-step update process reporting its status through hello reported properties.</span></span>

<span data-ttu-id="fa35b-179">Kaynakları toolearn nasıl aşağıdaki kullanım hello için:</span><span class="sxs-lookup"><span data-stu-id="fa35b-179">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="fa35b-180">Merhaba aygıtlarla telemetri gönderen [IOT Hub ile çalışmaya başlama] [ lnk-iothub-getstarted] öğretici</span><span class="sxs-lookup"><span data-stu-id="fa35b-180">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="fa35b-181">zamanlama veya gerçekleştirmek aygıtların büyük kümeleri üzerinde işlemler bkz hello [zamanlama ve yayın işleri] [ lnk-schedule-jobs] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="fa35b-181">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="fa35b-182">Merhaba ile etkileşimli olarak (örneğin, kullanıcı tarafından denetlenen bir uygulamadan fan etkinleştirdikten), cihazları denetleme [doğrudan yöntemleri kullanın] [ lnk-methods-tutorial] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="fa35b-182">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/devicesdknuget.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png


<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-twin-tutorial]: iot-hub-csharp-csharp-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-how-to-configure-createapp]: iot-hub-csharp-csharp-twin-how-to-configure.md#create-the-simulated-device-app
