---
title: "Azure IOT Hub cihaz çifti özellikleri (.NET/.NET) kullanın | Microsoft Docs"
description: "Azure IOT Hub cihaz çiftlerini cihazları yapılandırmak için nasıl kullanılacağını. Sanal cihaz uygulaması ve Azure IOT hizmeti SDK'sını cihaz çifti kullanarak bir aygıt yapılandırmasını değiştirir bir hizmet uygulaması uygulamak .NET için uygulamak için Azure IOT cihaz SDK'sı .NET için kullanın."
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
ms.openlocfilehash: 679cda28bf3ce9fb207fe3693a3453b355f1de15
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="use-desired-properties-to-configure-devices"></a><span data-ttu-id="3d444-104">İstenen özelliklerde cihazları yapılandırmak için kullanın</span><span class="sxs-lookup"><span data-stu-id="3d444-104">Use desired properties to configure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="3d444-105">Bu öğreticinin sonunda iki .NET konsol uygulamaları olacaktır:</span><span class="sxs-lookup"><span data-stu-id="3d444-105">At the end of this tutorial, you will have two .NET console apps:</span></span>

* <span data-ttu-id="3d444-106">**SimulateDeviceConfiguration**, istenen yapılandırma güncelleştirmesi bekler ve benzetimli yapılandırmasını güncelleştirme işleminin durumunu raporlar bir sanal cihaz uygulaması.</span><span class="sxs-lookup"><span data-stu-id="3d444-106">**SimulateDeviceConfiguration**, a simulated device app that waits for a desired configuration update and reports the status of a simulated configuration update process.</span></span>
* <span data-ttu-id="3d444-107">**SetDesiredConfigurationAndQuery**, istenen yapılandırma bir cihazda ayarlar ve yapılandırmayı güncelleştirme işlemini sorgular bir arka uç uygulaması.</span><span class="sxs-lookup"><span data-stu-id="3d444-107">**SetDesiredConfigurationAndQuery**, a back-end app, which sets the desired configuration on a device and queries the configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="3d444-108">Makaleyi [Azure IOT SDK'ları] [ lnk-hub-sdks] hem cihaz hem de arka uç uygulamalar oluşturmak için kullanabileceğiniz Azure IOT SDK'ları hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="3d444-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="3d444-109">Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="3d444-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="3d444-110">Visual Studio 2015 veya Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="3d444-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="3d444-111">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="3d444-111">An active Azure account.</span></span> <span data-ttu-id="3d444-112">Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d444-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="3d444-113">İzlediyseniz [cihaz çiftlerini ile çalışmaya başlama] [ lnk-twin-tutorial] öğretici, zaten sahip olduğunuz bir IOT hub ve adlı bir cihaz kimliği **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="3d444-113">If you followed the [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="3d444-114">Bu durumda, atlayabilirsiniz [sanal cihaz uygulaması oluşturma] [ lnk-how-to-configure-createapp] bölümü.</span><span class="sxs-lookup"><span data-stu-id="3d444-114">In that case, you can skip to the [Create the simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-the-simulated-device-app"></a><span data-ttu-id="3d444-115">Sanal cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="3d444-115">Create the simulated device app</span></span>
<span data-ttu-id="3d444-116">Bu bölümde, hub'ınıza bağlanan bir .NET konsol uygulaması oluşturma **myDeviceId**, istenen yapılandırma güncelleştirmesi bekler ve daha sonra güncelleştirmeleri benzetimli yapılandırmasını güncelleştirme işlemini raporlar.</span><span class="sxs-lookup"><span data-stu-id="3d444-116">In this section, you create a .NET console app that connects to your hub as **myDeviceId**, waits for a desired configuration update and then reports updates on the simulated configuration update process.</span></span>

1. <span data-ttu-id="3d444-117">Visual Studio kullanarak yeni bir Visual C# Windows Klasik Masaüstü projesi oluşturma **konsol uygulaması** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="3d444-117">In Visual Studio, create a new Visual C# Windows Classic Desktop project by using the **Console Application** project template.</span></span> <span data-ttu-id="3d444-118">Proje adı **SimulateDeviceConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="3d444-118">Name the project **SimulateDeviceConfiguration**.</span></span>
   
    ![Yeni Visual C# Klasik Windows cihaz uygulaması][img-createdeviceapp]

1. <span data-ttu-id="3d444-120">Çözüm Gezgini'nde sağ **SimulateDeviceConfiguration** proje ve ardından **NuGet paketlerini Yönet...** .</span><span class="sxs-lookup"><span data-stu-id="3d444-120">In Solution Explorer, right-click the **SimulateDeviceConfiguration** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="3d444-121">İçinde **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat** arayın ve **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="3d444-121">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="3d444-122">Seçin **yükleme** yüklemek için **Microsoft.Azure.Devices.Client** paketini ve kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="3d444-122">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="3d444-123">Bu yordam indirir, yükler ve bir başvuru ekler [Azure IOT cihaz SDK'sı] [ lnk-nuget-client-sdk] NuGet paketi ve bağımlılıklarını.</span><span class="sxs-lookup"><span data-stu-id="3d444-123">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet Paket Yöneticisi penceresi istemci uygulaması][img-clientnuget]
1. <span data-ttu-id="3d444-125">Aşağıdaki `using` deyimlerini **Program.cs** dosyasının üst kısmına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3d444-125">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="3d444-126">**Program** sınıfına aşağıdaki alanları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3d444-126">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="3d444-127">Yer tutucu değerini önceki bölümünde belirtildiği cihaz bağlantı dizesini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3d444-127">Replace the placeholder value with the device connection string that you noted in the previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;
        static TwinCollection reportedProperties = new TwinCollection();

1. <span data-ttu-id="3d444-128">**Program** sınıfına aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3d444-128">Add the following method to the **Program** class:</span></span>
 
        public static void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting to hub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }
    <span data-ttu-id="3d444-129">**İstemci** nesne ihtiyaç duyduğunuz etkileşim kurmak için cihaz çiftlerini aygıttan ile tüm yöntemleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="3d444-129">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="3d444-130">Yukarıda gösterilen koddan başlatır **istemci** nesne ve cihaz çiftinin alır **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="3d444-130">The code shown above, initializes the **Client** object, and then retrieves the device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="3d444-131">Aşağıdaki yöntemi ekleyin **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="3d444-131">Add the following method to the **Program** class.</span></span> <span data-ttu-id="3d444-132">Bu yöntem yerel cihazda telemetri ilk değerlerini ayarlar ve cihaz çifti güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="3d444-132">This method sets the initial values of telemetry on the local device and then updates the device twin.</span></span>

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

1. <span data-ttu-id="3d444-133">Aşağıdaki yöntemi ekleyin **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="3d444-133">Add the following method to the **Program** class.</span></span> <span data-ttu-id="3d444-134">Bu değişikliği algılar bir geri çağırma olduğu *özelliklerini istenen* cihaz çiftine.</span><span class="sxs-lookup"><span data-stu-id="3d444-134">This is a callback which will detect a change in *desired properties* in the device twin.</span></span>

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

    <span data-ttu-id="3d444-135">Bu yöntem yerel cihaz çifti nesnesindeki bildirilen özellikleri yapılandırma güncelleştirme isteği ile güncelleştirir ve durumunu ayarlar **bekleyen**, hizmette cihaz çifti güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="3d444-135">This method updates the reported properties on the local device twin object with the configuration update request and sets the status to **Pending**, then updates the device twin on the service.</span></span> <span data-ttu-id="3d444-136">Cihaz çifti başarıyla güncelleştirdikten sonra yapılandırma değişikliği yöntemini çağırarak tamamlanmadan `CompleteConfigChange` sonraki noktasında açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3d444-136">After successfully updating the device twin, it completes the config change by calling the method `CompleteConfigChange` described in the next point.</span></span>

1. <span data-ttu-id="3d444-137">Aşağıdaki yöntemi ekleyin **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="3d444-137">Add the following method to the **Program** class.</span></span> <span data-ttu-id="3d444-138">Bu yöntem bir cihaz sıfırlama benzetimini yapar, sonra güncelleştirmeleri yerel bildirilen durum ayarını özellikleri **başarı** ve kaldırır **pendingConfig** öğesi.</span><span class="sxs-lookup"><span data-stu-id="3d444-138">This method simulates a device reset, then updates the local reported properties setting the status to **Success** and removes the **pendingConfig** element.</span></span> <span data-ttu-id="3d444-139">Ardından, cihaz çifti hizmette güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="3d444-139">It then updates the device twin on the service.</span></span> 

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
                Console.WriteLine("Config change complete \nPress any key to exit.");
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

1. <span data-ttu-id="3d444-140">Son olarak aşağıdaki satırları ekleyin **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="3d444-140">Finally add the following lines to the **Main** method:</span></span>

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
   > <span data-ttu-id="3d444-141">Bu öğretici herhangi davranışı eşzamanlı yapılandırma güncelleştirmelerini benzetimini değil.</span><span class="sxs-lookup"><span data-stu-id="3d444-141">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="3d444-142">Bazı yapılandırma güncelleştirme işlemleri hedef yapılandırma değişiklikleri güncelleştirme çalışan bazı bunları kuyruğuna olabilir ve bazı bir hata durumu reddedebilirsiniz sırada karşılamak mümkün olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d444-142">Some configuration update processes might be able to accommodate changes of target configuration while the update is running, some might have to queue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="3d444-143">Belirli bir yapılandırma işlemi için istenen davranışı dikkate aldığınızdan emin olun ve yapılandırma değişikliğini başlatmadan önce uygun mantığı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3d444-143">Make sure to consider the desired behavior for your specific configuration process, and add the appropriate logic before initiating the configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="3d444-144">Çözümü derlemek ve tıklayarak bu cihaz uygulaması Visual Studio'dan çalıştırma **F5**.</span><span class="sxs-lookup"><span data-stu-id="3d444-144">Build the solution and then run the device app from Visual Studio by clicking **F5**.</span></span> <span data-ttu-id="3d444-145">Çıktı konsolda sanal cihazınız cihaz çifti alıyor belirten, telemetri ayarlama ve istenen özellik değişikliği için bekleyen iletileri görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3d444-145">On the output console, you should see the messages indicating that your simulated device is retrieving the device twin, setting up the telemetry, and waiting for desired property change.</span></span> <span data-ttu-id="3d444-146">Uygulamayı çalıştıran tutun.</span><span class="sxs-lookup"><span data-stu-id="3d444-146">Keep the app running.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="3d444-147">Hizmet Uygulaması Oluştur</span><span class="sxs-lookup"><span data-stu-id="3d444-147">Create the service app</span></span>
<span data-ttu-id="3d444-148">Bu bölümde, güncelleştirmeleri bir .NET konsol uygulaması oluşturacak *özelliklerini istenen* ilişkili cihaz çifti üzerinde **myDeviceId** ile yeni bir telemetri yapılandırma nesnesi.</span><span class="sxs-lookup"><span data-stu-id="3d444-148">In this section, you will create a .NET console app that updates the *desired properties* on the device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="3d444-149">IOT hub'ı depolanan cihaz çiftlerini sorgular ve cihazın istenen ve bildirilen yapılandırmaları arasındaki farkı gösterir.</span><span class="sxs-lookup"><span data-stu-id="3d444-149">It then queries the device twins stored in the IoT hub and shows the difference between the desired and reported configurations of the device.</span></span>

1. <span data-ttu-id="3d444-150">Visual Studio'da **Konsol Uygulaması** proje şablonunu kullanarak geçerli çözüme bir Visual C# Windows Klasik Masaüstü projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3d444-150">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="3d444-151">Proje adı **SetDesiredConfigurationAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="3d444-151">Name the project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![Yeni Visual C# Windows Klasik Masaüstü projesi][img-createapp]
1. <span data-ttu-id="3d444-153">Çözüm Gezgini'nde sağ **SetDesiredConfigurationAndQuery** proje ve ardından **NuGet paketlerini Yönet...** .</span><span class="sxs-lookup"><span data-stu-id="3d444-153">In Solution Explorer, right-click the **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="3d444-154">**NuGet Paket Yöneticisi** penceresinde **Gözat**'ı seçin, **microsoft.azure.devices**'ı aratın, **Microsoft.Azure.Devices** paketini yüklemek için **Yükle**'yi seçin ve kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="3d444-154">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="3d444-155">Bu yordam ile [Azure IoT hizmet SDK'sı][lnk-nuget-service-sdk] NuGet paketi ve bağımlılıkları indirilir, yüklenir ve bu pakete bir başvuru eklenir.</span><span class="sxs-lookup"><span data-stu-id="3d444-155">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet Paket Yöneticisi penceresi][img-servicenuget]
1. <span data-ttu-id="3d444-157">Aşağıdaki `using` deyimlerini **Program.cs** dosyasının üst kısmına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3d444-157">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="3d444-158">**Program** sınıfına aşağıdaki alanları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3d444-158">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="3d444-159">Yer tutucu değerini, önceki bölümde hub için oluşturduğunuz IoT Hub bağlantı dizesiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3d444-159">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="3d444-160">**Program** sınıfına aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3d444-160">Add the following method to the **Program** class:</span></span>
   
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
   
    <span data-ttu-id="3d444-161">**Kayıt defteri** nesne cihaz çiftlerini hizmet ile etkileşim kurmak için gereken tüm yöntemleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="3d444-161">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="3d444-162">Bu kod başlatır **kayıt defteri** nesnesi, cihaz çiftinin alır **myDeviceId**ve ardından yeni bir telemetri yapılandırma nesnesi ile istenen özelliklerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="3d444-162">This code initializes the **Registry** object, retrieves the device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="3d444-163">Bundan sonra IOT hub'ı 10 saniyede depolanan cihaz çiftlerini sorgular ve istenen ve bildirilen telemetri yapılandırmaları yazdırır.</span><span class="sxs-lookup"><span data-stu-id="3d444-163">After that, it queries the device twins stored in the IoT hub every 10 seconds, and prints the desired and reported telemetry configurations.</span></span> <span data-ttu-id="3d444-164">Başvurmak [IOT hub'ı sorgu dili] [ lnk-query] tüm cihazlarınızda zengin raporlar üretmek hakkında bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="3d444-164">Refer to the [IoT Hub query language][lnk-query] to learn how to generate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="3d444-165">Bu uygulama yalnızca tanım amaçlıdır her 10 saniye IOT hub'ı sorgular.</span><span class="sxs-lookup"><span data-stu-id="3d444-165">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="3d444-166">Sorguları birçok cihaz arasında kullanıcı dönük raporları oluşturmak ve değil değişikliklerini algılamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="3d444-166">Use queries to generate user-facing reports across many devices, and not to detect changes.</span></span> <span data-ttu-id="3d444-167">Çözümünüz cihaz olayların gerçek zamanlı bildirimler gerektiriyorsa, kullanın [twin bildirimleri][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="3d444-167">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="3d444-168">Son olarak, **Main** yöntemine aşağıdaki satırları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3d444-168">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery();
        Console.WriteLine("Press any key to quit.");
        Console.ReadLine();
1. <span data-ttu-id="3d444-169">Çözüm Gezgini'nde açık **başlangıç projelerini Ayarla...**  ve emin olun **eylem** için **SetDesiredConfigurationAndQuery** projedir **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="3d444-169">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="3d444-170">Çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3d444-170">Build the solution.</span></span>
1. <span data-ttu-id="3d444-171">İle **SimulateDeviceConfiguration** cihaz uygulamasının çalışıyor, Visual Studio kullanarak hizmet uygulama çalıştırma **F5**.</span><span class="sxs-lookup"><span data-stu-id="3d444-171">With **SimulateDeviceConfiguration** device app running, run the service app from Visual Studio using **F5**.</span></span> <span data-ttu-id="3d444-172">Çıkarılıp bildirilen yapılandırma görmelisiniz **bekleyen** için **başarı** 24 saat yerine beş dakikalık sıklığı yeni etkin gönderin.</span><span class="sxs-lookup"><span data-stu-id="3d444-172">You should see the reported configuration change from **Pending** to **Success** with the new active send frequency of five minutes instead of 24 hours.</span></span>

 ![Cihaz başarıyla yapılandırıldı][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="3d444-174">Cihaz rapor işlemi ve sorgu sonucu arasında bir dakika kadar bir gecikme yoktur.</span><span class="sxs-lookup"><span data-stu-id="3d444-174">There is a delay of up to a minute between the device report operation and the query result.</span></span> <span data-ttu-id="3d444-175">Bu, çok yüksek ölçekli olarak çalışmak sorgu altyapısı olanak sağlamasıdır.</span><span class="sxs-lookup"><span data-stu-id="3d444-175">This is to enable the query infrastructure to work at very high scale.</span></span> <span data-ttu-id="3d444-176">Bir tek cihaz çifti kullanımı tutarlı görünümleri almak için **getDeviceTwin** yönteminde **kayıt defteri** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="3d444-176">To retrieve consistent views of a single device twin use the **getDeviceTwin** method in the **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="3d444-177">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3d444-177">Next steps</span></span>
<span data-ttu-id="3d444-178">Bu öğreticide, istenen yapılandırma olarak kümesi *özellikleri istenen* çözümden arka uç ve bu değişikliği algılar ve durumunu bildirilen özellikleri aracılığıyla raporlama çok adımlı güncelleştirme işleminin benzetimini yapmak için bir cihaz uygulaması yazıldı.</span><span class="sxs-lookup"><span data-stu-id="3d444-178">In this tutorial, you set a desired configuration as *desired properties* from the solution back end, and wrote a device app to detect that change and simulate a multi-step update process reporting its status through the reported properties.</span></span>

<span data-ttu-id="3d444-179">Bilgi edinmek için aşağıdaki kaynakları kullanın nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="3d444-179">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="3d444-180">aygıtlarla telemetri gönderen [IOT Hub ile çalışmaya başlama] [ lnk-iothub-getstarted] öğretici</span><span class="sxs-lookup"><span data-stu-id="3d444-180">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="3d444-181">zamanlama veya aygıtları bakın büyük kümeleri işlemleri [zamanlama ve yayın işleri] [ lnk-schedule-jobs] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="3d444-181">schedule or perform operations on large sets of devices see the [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="3d444-182">ile etkileşimli olarak (örneğin, kullanıcı tarafından denetlenen bir uygulamadan fan etkinleştirdikten), cihazları denetleme [doğrudan yöntemleri kullanın] [ lnk-methods-tutorial] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="3d444-182">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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
