---
title: "Azure IOT Hub cihaz çiftlerini (.NET/.NET) ile çalışmaya başlama | Microsoft Docs"
description: "Azure IOT Hub cihaz çiftlerini etiket ekleyebilir ve IOT Hub sorgusuyla kullanmak için nasıl kullanılacağını. Sanal cihaz uygulamasının ve Azure IOT hizmeti SDK'sını etiketleri ekler ve IOT hub'ı sorgu çalışan bir hizmet uygulaması uygulamak .NET için uygulamak için Azure IOT cihaz SDK'sı .NET için kullanın."
services: iot-hub
documentationcenter: node
author: dsk-2015
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: dkshir
ms.openlocfilehash: 6073d594117e69676b753a1e3af25fffa3583a2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-device-twins-netnet"></a><span data-ttu-id="a8e1c-104">Cihaz çiftlerini (.NET/.NET) ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a8e1c-104">Get started with device twins (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="a8e1c-105">Bu öğreticinin sonunda bu .NET konsol uygulamaları olacaktır:</span><span class="sxs-lookup"><span data-stu-id="a8e1c-105">At the end of this tutorial, you will have these .NET console apps:</span></span>

* <span data-ttu-id="a8e1c-106">**CreateDeviceIdentity**, bir cihaz kimliği ve sanal cihaz uygulamanızı bağlamak için ilişkili güvenlik anahtarı oluşturan bir .NET uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-106">**CreateDeviceIdentity**, a .NET app which creates a device identity and associated security key to connect your simulated device app.</span></span>
* <span data-ttu-id="a8e1c-107">**AddTagsAndQuery**, etiketleri ekler ve cihaz çiftlerini sorgular .NET arka uç uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-107">**AddTagsAndQuery**, a .NET back-end app which adds tags and queries device twins.</span></span>
* <span data-ttu-id="a8e1c-108">**ReportConnectivity**, bir cihaza benzetim yapan daha önce oluşturulan cihaz kimliğiyle IOT hub'ınıza bağlanır ve kendi bağlantı koşulu raporları .NET cihaz uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-108">**ReportConnectivity**, a .NET device app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="a8e1c-109">Makaleyi [Azure IOT SDK'ları] [ lnk-hub-sdks] hem cihaz hem de arka uç uygulamalar oluşturmak için kullanabileceğiniz Azure IOT SDK'ları hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-109">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="a8e1c-110">Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="a8e1c-110">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="a8e1c-111">Visual Studio 2015 veya Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-111">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="a8e1c-112">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-112">An active Azure account.</span></span> <span data-ttu-id="a8e1c-113">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="a8e1c-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="a8e1c-114">Bunun yerine cihaz kimliğini program aracılığıyla oluşturmak istiyorsanız, ilgili bölümünü okuyun [.NET kullanarak IOT hub'ınıza sanal Cihazınızı bağlamak] [ lnk-device-identity-csharp] makalesi.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-114">If you want to create the device identity programmatically instead, read the corresponding section in the [Connect your simulated device to your IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="a8e1c-115">Hizmet Uygulaması Oluştur</span><span class="sxs-lookup"><span data-stu-id="a8e1c-115">Create the service app</span></span>
<span data-ttu-id="a8e1c-116">Bu bölümde, konum meta verileri ile ilişkili cihaz çifti ekler (C# kullanarak) bir .NET konsol uygulaması oluşturma **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-116">In this section, you create a .NET console app (using C#) that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="a8e1c-117">Ardından, IOT hub'ı ABD, ardından bir cep telefonu bağlantı bildirilen olanları içinde bulunan aygıtları seçerek depolanan cihaz çiftlerini sorgular.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-117">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="a8e1c-118">Visual Studio'da **Konsol Uygulaması** proje şablonunu kullanarak geçerli çözüme bir Visual C# Windows Klasik Masaüstü projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-118">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="a8e1c-119">Proje adı **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-119">Name the project **AddTagsAndQuery**.</span></span>
   
    ![Yeni Visual C# Windows Klasik Masaüstü projesi][img-createapp]
1. <span data-ttu-id="a8e1c-121">Çözüm Gezgini'nde sağ **AddTagsAndQuery** proje ve ardından **NuGet paketlerini Yönet...** .</span><span class="sxs-lookup"><span data-stu-id="a8e1c-121">In Solution Explorer, right-click the **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="a8e1c-122">İçinde **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat** arayın ve **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-122">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="a8e1c-123">Seçin **yükleme** yüklemek için **Microsoft.Azure.Devices** paketini ve kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-123">Select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="a8e1c-124">Bu yordam ile [Azure IoT hizmet SDK'sı][lnk-nuget-service-sdk] NuGet paketi ve bağımlılıkları indirilir, yüklenir ve bu pakete bir başvuru eklenir.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-124">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet Paket Yöneticisi penceresi][img-servicenuget]
1. <span data-ttu-id="a8e1c-126">Aşağıdaki `using` deyimlerini **Program.cs** dosyasının üst kısmına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a8e1c-126">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="a8e1c-127">**Program** sınıfına aşağıdaki alanları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-127">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="a8e1c-128">Yer tutucu değerini, önceki bölümde hub için oluşturduğunuz IoT Hub bağlantı dizesiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-128">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="a8e1c-129">**Program** sınıfına aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a8e1c-129">Add the following method to the **Program** class:</span></span>
   
        public static async Task AddTagsAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch =
                @"{
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                        }
                    }
                }";
            await registryManager.UpdateTwinAsync(twin.DeviceId, patch, twin.ETag);
   
            var query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            var twinsInRedmond43 = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43: {0}", string.Join(", ", twinsInRedmond43.Select(t => t.DeviceId)));
   
            query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            var twinsInRedmond43UsingCellular = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43 using cellular network: {0}", string.Join(", ", twinsInRedmond43UsingCellular.Select(t => t.DeviceId)));
        }
   
    <span data-ttu-id="a8e1c-130">**RegistryManager** sınıfı cihaz çiftlerini hizmet ile etkileşim kurmak için gereken tüm yöntemleri sunar.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-130">The **RegistryManager** class exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="a8e1c-131">Önceki kod ilk başlatır **registryManager** nesnesi, ardından cihaz çiftinin alır **myDeviceId**ve son olarak, etiketleri istenen konumu bilgilerle güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-131">The previous code first initializes the **registryManager** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="a8e1c-132">Güncelleştirdikten sonra iki sorguları yürüten: yalnızca cihaz çiftlerini bulunan aygıtların ilk seçer **Redmond43** tesis ve ikinci da cep telefonu şebekesi bağlı aygıtlar seçmek için sorgu iyileştirir.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-132">After updating, it executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="a8e1c-133">Unutmayın, oluşturduğunda, önceki kod **sorgu** nesne, döndürülen belgelerin en fazla sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-133">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="a8e1c-134">**Sorgu** nesnesini içeren bir **HasMoreResults** çağırmak için kullanabileceğiniz boolean özelliği **GetNextAsTwinAsync** birden çok kez tüm sonuçları almak için yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-134">The **query** object contains a **HasMoreResults** boolean property that you can use to invoke the **GetNextAsTwinAsync** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="a8e1c-135">Bir yöntem olarak adlandırılan **GetNextAsJson** değil cihaz çiftlerini, örneğin, sonuçları için toplama sorguların sonuçlarını kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-135">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="a8e1c-136">Son olarak, **Main** yöntemine aşağıdaki satırları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a8e1c-136">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

1. <span data-ttu-id="a8e1c-137">Çözüm Gezgini'nde açık **başlangıç projelerini Ayarla...**  ve emin olun **eylem** için **AddTagsAndQuery** projedir **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-137">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="a8e1c-138">Çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-138">Build the solution.</span></span>
1. <span data-ttu-id="a8e1c-139">Üzerinde sağ tıklayarak bu uygulamayı çalıştırmak **AddTagsAndQuery** proje ve seçerek **hata ayıklama**, ardından **başlangıç yeni örnek**.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-139">Run this application by right-clicking on the **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="a8e1c-140">Bulunan tüm cihazlar için sorgu soran bir cihazda sonuçlarında görmelisiniz **Redmond43** ve sonuçları bir cep telefonu şebekesi kullanan cihazlar için sınırlar sorgu için yok.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-140">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![Sorgu Sonuçları penceresinde][img-addtagapp]

<span data-ttu-id="a8e1c-142">Sonraki bölümde, önceki bölümde sorgusunun sonucu değiştirir ve bağlantı bilgilerini raporlar bir cihaz uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-142">In the next section, you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="a8e1c-143">Cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="a8e1c-143">Create the device app</span></span>
<span data-ttu-id="a8e1c-144">Bu bölümde, hub'ınıza bağlanan bir .NET konsol uygulaması oluşturma **myDeviceId**ve ardından bir cep telefonu şebekesi kullanarak bağlı bilgileri içerecek şekilde bildirilen özelliklerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-144">In this section, you create a .NET console app that connects to your hub as **myDeviceId**, and then updates its reported properties to contain the information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="a8e1c-145">Visual Studio'da **Konsol Uygulaması** proje şablonunu kullanarak geçerli çözüme bir Visual C# Windows Klasik Masaüstü projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-145">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="a8e1c-146">Proje adı **ReportConnectivity**.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-146">Name the project **ReportConnectivity**.</span></span>
   
    ![Yeni Visual C# Klasik Windows cihaz uygulaması][img-createdeviceapp]
    
1. <span data-ttu-id="a8e1c-148">Çözüm Gezgini'nde sağ **ReportConnectivity** proje ve ardından **NuGet paketlerini Yönet...** .</span><span class="sxs-lookup"><span data-stu-id="a8e1c-148">In Solution Explorer, right-click the **ReportConnectivity** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="a8e1c-149">İçinde **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat** arayın ve **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-149">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="a8e1c-150">Seçin **yükleme** yüklemek için **Microsoft.Azure.Devices.Client** paketini ve kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-150">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="a8e1c-151">Bu yordam indirir, yükler ve bir başvuru ekler [Azure IOT cihaz SDK'sı] [ lnk-nuget-client-sdk] NuGet paketi ve bağımlılıklarını.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-151">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet Paket Yöneticisi penceresi istemci uygulaması][img-clientnuget]
1. <span data-ttu-id="a8e1c-153">Aşağıdaki `using` deyimlerini **Program.cs** dosyasının üst kısmına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a8e1c-153">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="a8e1c-154">**Program** sınıfına aşağıdaki alanları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-154">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="a8e1c-155">Yer tutucu değerini önceki bölümünde belirtildiği cihaz bağlantı dizesini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-155">Replace the placeholder value with the device connection string that you noted in the previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="a8e1c-156">**Program** sınıfına aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a8e1c-156">Add the following method to the **Program** class:</span></span>

       public static async void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting to hub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
                Console.WriteLine("Retrieving twin");
                await Client.GetTwinAsync();
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    <span data-ttu-id="a8e1c-157">**İstemci** nesne ihtiyaç duyduğunuz etkileşim kurmak için cihaz çiftlerini aygıttan ile tüm yöntemleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-157">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="a8e1c-158">Yukarıda gösterilen koddan başlatır **istemci** nesne ve cihaz çiftinin alır **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-158">The code shown above, initializes the **Client** object, and then retrieves the device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="a8e1c-159">**Program** sınıfına aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a8e1c-159">Add the following method to the **Program** class:</span></span>
   
        public static async void ReportConnectivity()
        {
            try
            {
                Console.WriteLine("Sending connectivity data as reported property");
                
                TwinCollection reportedProperties, connectivity;
                reportedProperties = new TwinCollection();
                connectivity = new TwinCollection();
                connectivity["type"] = "cellular";
                reportedProperties["connectivity"] = connectivity;
                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

   <span data-ttu-id="a8e1c-160">Güncelleştirmeleri yukarıdaki kodu **myDeviceId**bağlantı bilgilerini özelliğiyle bildirilen.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-160">The code above updates **myDeviceId**'s reported property with the connectivity information.</span></span>

1. <span data-ttu-id="a8e1c-161">Son olarak, **Main** yöntemine aşağıdaki satırları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a8e1c-161">Finally, add the following lines to the **Main** method:</span></span>
   
       try
       {
            InitClient();
            ReportConnectivity();
       }
       catch (Exception ex)
       {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
       }
       Console.WriteLine("Press Enter to exit.");
       Console.ReadLine();

1. <span data-ttu-id="a8e1c-162">Çözüm Gezgini'nde açık **başlangıç projelerini Ayarla...**  ve emin olun **eylem** için **ReportConnectivity** projedir **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-162">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **ReportConnectivity** project is **Start**.</span></span> <span data-ttu-id="a8e1c-163">Çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-163">Build the solution.</span></span>
1. <span data-ttu-id="a8e1c-164">Üzerinde sağ tıklayarak bu uygulamayı çalıştırmak **ReportConnectivity** proje ve seçerek **hata ayıklama**, ardından **başlangıç yeni örnek**.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-164">Run this application by right-clicking on the **ReportConnectivity** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="a8e1c-165">Twin bilgi alma ve sonra bağlantı olarak gönderme görmelisiniz bir *özelliği bildirilen*.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-165">You should see it getting the twin information, and then sending connectivity as a *reported property*.</span></span>
   
    ![Rapor bağlantısı cihaz uygulamayı çalıştırma][img-rundeviceapp]
    
    
1. <span data-ttu-id="a8e1c-167">Aygıt bağlantısı bilgilerini bildirdi, her iki sorgularda görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-167">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="a8e1c-168">.NET çalıştırmak **AddTagsAndQuery** uygulama sorguları yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-168">Run the .NET **AddTagsAndQuery** app to run the queries again.</span></span> <span data-ttu-id="a8e1c-169">Bu süre **myDeviceId** hem sorgu sonuçlarında görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-169">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![Başarıyla bildirilen cihaz bağlantısı][img-tagappsuccess]

## <a name="next-steps"></a><span data-ttu-id="a8e1c-171">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a8e1c-171">Next steps</span></span>
<span data-ttu-id="a8e1c-172">Bu öğreticide, Azure portalında yeni bir IoT hub'ı yapılandırdınız ve ardından IoT hub'ının kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-172">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="a8e1c-173">Cihaz meta verilerini bir arka uç uygulamadan etiketler eklendi ve sanal cihaz uygulaması rapor cihaz bağlantı bilgilerini cihaz çiftine yazıldı.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-173">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="a8e1c-174">Ayrıca SQL benzeri IOT hub'ı sorgu dili kullanarak bu bilgileri sorgulamak öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-174">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="a8e1c-175">Bilgi edinmek için aşağıdaki kaynakları kullanın nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="a8e1c-175">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="a8e1c-176">aygıtlarla telemetri gönderen [IOT Hub ile çalışmaya başlama] [ lnk-iothub-getstarted] öğretici</span><span class="sxs-lookup"><span data-stu-id="a8e1c-176">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="a8e1c-177">cihaz çifti'nın istenen özelliklere sahip kullanarak cihazları yapılandırma [kullanmak istediğiniz cihazları yapılandırmak için Özellikler] [ lnk-twin-how-to-configure] öğretici</span><span class="sxs-lookup"><span data-stu-id="a8e1c-177">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="a8e1c-178">aygıtlarını etkileşimli olarak (örneğin, kullanıcı tarafından denetlenen bir uygulamadan fan etkinleştirdikten) ile [doğrudan yöntemleri kullanın] [ lnk-methods-tutorial] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-178">control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-csharp-twin-getstarted/addtagapp.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-getstarted/clientsdknuget.png
[img-rundeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/rundeviceapp.png
[img-tagappsuccess]: media/iot-hub-csharp-csharp-twin-getstarted/tagappsuccess.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp
[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

