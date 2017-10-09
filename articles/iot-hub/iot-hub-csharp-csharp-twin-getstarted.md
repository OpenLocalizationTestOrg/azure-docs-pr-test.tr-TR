---
title: "aaaGet başlatılan Azure IOT Hub cihaz çiftlerini (.NET/.NET) | Microsoft Docs"
description: "Nasıl toouse Azure IOT Hub cihaz çiftlerini tooadd etiketleri ve IOT Hub sorgusuyla kullanın. .NET tooimplement hello sanal cihaz uygulamasının ve hello .NET tooimplement hello etiketleri ekler ve hello IOT hub'ı sorgu çalışan bir hizmet uygulaması için Azure IOT hizmeti SDK'sı için hello Azure IOT cihaz SDK'sını kullanın."
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
ms.openlocfilehash: 7fa73ac896c44e79c6522d252cd1515bd6e7bb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnet"></a><span data-ttu-id="dcd3c-104">Cihaz çiftlerini (.NET/.NET) ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="dcd3c-104">Get started with device twins (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="dcd3c-105">Bu öğreticinin Hello sonunda, bu .NET konsol uygulamaları olacaktır:</span><span class="sxs-lookup"><span data-stu-id="dcd3c-105">At hello end of this tutorial, you will have these .NET console apps:</span></span>

* <span data-ttu-id="dcd3c-106">**CreateDeviceIdentity**, bir cihaz kimliği ve ilişkili güvenlik oluşturan bir .NET uygulaması, sanal cihaz uygulamasının tooconnect anahtar.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-106">**CreateDeviceIdentity**, a .NET app which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="dcd3c-107">**AddTagsAndQuery**, etiketleri ekler ve cihaz çiftlerini sorgular .NET arka uç uygulaması.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-107">**AddTagsAndQuery**, a .NET back-end app which adds tags and queries device twins.</span></span>
* <span data-ttu-id="dcd3c-108">**ReportConnectivity**, bir cihaza benzetim yapan tooyour IOT hub'ı daha önce oluşturduğunuz hello cihaz kimliği bağlanır ve kendi bağlantı koşulu raporları .NET cihaz uygulaması.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-108">**ReportConnectivity**, a .NET device app which simulates a device that connects tooyour IoT hub with hello device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="dcd3c-109">Merhaba makale [Azure IOT SDK'ları] [ lnk-hub-sdks] toobuild kullanabileceğiniz hello Azure IOT SDK'ları hakkında bilgi sağlayan cihaz ve arka uç uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="dcd3c-110">toocomplete hello aşağıdaki gereksinim Bu öğretici:</span><span class="sxs-lookup"><span data-stu-id="dcd3c-110">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="dcd3c-111">Visual Studio 2015 veya Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-111">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="dcd3c-112">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-112">An active Azure account.</span></span> <span data-ttu-id="dcd3c-113">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="dcd3c-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="dcd3c-114">Toocreate hello cihaz kimliği programlı olarak bunun yerine isterseniz, hello hello ilgili bölümünü okuyun [.NET kullanarak sanal cihaz tooyour IOT hub'ınıza bağlanmak] [ lnk-device-identity-csharp] makalesi.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-114">If you want toocreate hello device identity programmatically instead, read hello corresponding section in hello [Connect your simulated device tooyour IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="dcd3c-115">Merhaba service uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="dcd3c-115">Create hello service app</span></span>
<span data-ttu-id="dcd3c-116">Bu bölümde, konum meta veri toohello cihaz çifti ile ilişkili ekler (C# kullanarak) bir .NET konsol uygulaması oluşturma **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-116">In this section, you create a .NET console app (using C#) that adds location metadata toohello device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="dcd3c-117">Ardından hello cihaz çiftlerini hello IOT hub'ı hello bulunan hello aygıtları seçerek BİZE depolanır ve bir cep telefonu bağlantı bildirilen olanları hello sorgular.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-117">It then queries hello device twins stored in hello IoT hub selecting hello devices located in hello US, and then hello ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="dcd3c-118">Visual Studio'da hello kullanarak bir Visual C# Windows Klasik Masaüstü projesi toohello geçerli çözüme ekleyin **konsol uygulaması** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-118">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="dcd3c-119">Ad hello proje **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-119">Name hello project **AddTagsAndQuery**.</span></span>
   
    ![Yeni Visual C# Windows Klasik Masaüstü projesi][img-createapp]
1. <span data-ttu-id="dcd3c-121">Çözüm Gezgini'nde hello sağ **AddTagsAndQuery** proje ve ardından **NuGet paketlerini Yönet...** .</span><span class="sxs-lookup"><span data-stu-id="dcd3c-121">In Solution Explorer, right-click hello **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="dcd3c-122">Merhaba, **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat** arayın ve **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-122">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="dcd3c-123">Seçin **yükleme** tooinstall hello **Microsoft.Azure.Devices** paketini ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-123">Select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="dcd3c-124">Bu yordam indirir, yükler ve başvuru toohello ekler [Azure IOT hizmeti SDK'sını] [ lnk-nuget-service-sdk] NuGet paketi ve bağımlılıklarını.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-124">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet Paket Yöneticisi penceresi][img-servicenuget]
1. <span data-ttu-id="dcd3c-126">Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:</span><span class="sxs-lookup"><span data-stu-id="dcd3c-126">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="dcd3c-127">Aşağıdaki alanları toohello hello eklemek **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-127">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="dcd3c-128">Merhaba hello önceki bölümde oluşturduğunuz hello hub'ın IOT Hub bağlantı dizesine sahip Hello yer tutucu değerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-128">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="dcd3c-129">Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="dcd3c-129">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="dcd3c-130">Merhaba **RegistryManager** sınıfı cihaz çiftlerini hello hizmetinden ile tüm hello yöntemleri gerekli toointeract kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-130">hello **RegistryManager** class exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="dcd3c-131">Merhaba önceki kod ilk hello başlatır **registryManager** nesnesi alır cihaz çiftinin hello sonra **myDeviceId**ve son olarak, etiketleri istenen hello konumu bilgilerle güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-131">hello previous code first initializes hello **registryManager** object, then retrieves hello device twin for **myDeviceId**, and finally updates its tags with hello desired location information.</span></span>
   
    <span data-ttu-id="dcd3c-132">Güncelleştirdikten sonra iki sorguları yürüten: hello ilk yalnızca hello cihaz çiftlerini hello bulunan aygıtların seçer **Redmond43** tesis ve ayrıca üzerinden bağlanan hello ikinci iyileştirir hello sorgu tooselect yalnızca hello cihazları cep telefonu şebekesi.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-132">After updating, it executes two queries: hello first selects only hello device twins of devices located in hello **Redmond43** plant, and hello second refines hello query tooselect only hello devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="dcd3c-133">Merhaba oluşturduğunda bu hello önceki kod Not **sorgu** nesne, döndürülen belgelerin en fazla sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-133">Note that hello previous code, when it creates hello **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="dcd3c-134">Merhaba **sorgu** nesnesini içeren bir **HasMoreResults** tooinvoke hello kullanabileceğiniz boolean özelliği **GetNextAsTwinAsync** yöntemleri birden çok kez tooretrieve tüm sonuçları.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-134">hello **query** object contains a **HasMoreResults** boolean property that you can use tooinvoke hello **GetNextAsTwinAsync** methods multiple times tooretrieve all results.</span></span> <span data-ttu-id="dcd3c-135">Bir yöntem olarak adlandırılan **GetNextAsJson** değil cihaz çiftlerini, örneğin, sonuçları için toplama sorguların sonuçlarını kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-135">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="dcd3c-136">Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="dcd3c-136">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="dcd3c-137">Merhaba Hello Çözüm Gezgini, açık **başlangıç projelerini Ayarla...**  ve emin hello **eylem** için **AddTagsAndQuery** projedir **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-137">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="dcd3c-138">Merhaba çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-138">Build hello solution.</span></span>
1. <span data-ttu-id="dcd3c-139">Merhaba üzerinde sağ tıklayarak bu uygulamayı çalıştırmak **AddTagsAndQuery** proje ve seçerek **hata ayıklama**, ardından **başlangıç yeni örnek**.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-139">Run this application by right-clicking on hello **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="dcd3c-140">Bulunan tüm cihazlar için sorgu hello soran bir cihazda hello sonuçlarında görmelisiniz **Redmond43** ve hiçbiri hello kısıtlayan hello sorgu için bir cep telefonu şebekesi kullanmak toodevices sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-140">You should see one device in hello results for hello query asking for all devices located in **Redmond43** and none for hello query that restricts hello results toodevices that use a cellular network.</span></span>
   
    ![Sorgu Sonuçları penceresinde][img-addtagapp]

<span data-ttu-id="dcd3c-142">Hello sonraki bölümdeki hello bağlantı bilgilerini raporları bir cihaz uygulaması oluşturma ve değişiklikleri hello önceki bölümdeki hello sorgusunun sonucu hello.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-142">In hello next section, you create a device app that reports hello connectivity information and changes hello result of hello query in hello previous section.</span></span>

## <a name="create-hello-device-app"></a><span data-ttu-id="dcd3c-143">Merhaba cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="dcd3c-143">Create hello device app</span></span>
<span data-ttu-id="dcd3c-144">Bu bölümde, tooyour hub olarak bağlanan bir .NET konsol uygulaması oluşturma **myDeviceId**ve ardından, bir cep telefonu şebekesi kullanarak bağlı olduğu bildirilen özellikleri toocontain hello bilgilerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-144">In this section, you create a .NET console app that connects tooyour hub as **myDeviceId**, and then updates its reported properties toocontain hello information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="dcd3c-145">Visual Studio'da hello kullanarak bir Visual C# Windows Klasik Masaüstü projesi toohello geçerli çözüme ekleyin **konsol uygulaması** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-145">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="dcd3c-146">Ad hello proje **ReportConnectivity**.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-146">Name hello project **ReportConnectivity**.</span></span>
   
    ![Yeni Visual C# Klasik Windows cihaz uygulaması][img-createdeviceapp]
    
1. <span data-ttu-id="dcd3c-148">Çözüm Gezgini'nde hello sağ **ReportConnectivity** proje ve ardından **NuGet paketlerini Yönet...** .</span><span class="sxs-lookup"><span data-stu-id="dcd3c-148">In Solution Explorer, right-click hello **ReportConnectivity** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="dcd3c-149">Merhaba, **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat** arayın ve **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-149">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="dcd3c-150">Seçin **yükleme** tooinstall hello **Microsoft.Azure.Devices.Client** paketini ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-150">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="dcd3c-151">Bu yordam indirir, yükler ve başvuru toohello ekler [Azure IOT cihaz SDK'sı] [ lnk-nuget-client-sdk] NuGet paketi ve bağımlılıklarını.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-151">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet Paket Yöneticisi penceresi istemci uygulaması][img-clientnuget]
1. <span data-ttu-id="dcd3c-153">Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:</span><span class="sxs-lookup"><span data-stu-id="dcd3c-153">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="dcd3c-154">Aşağıdaki alanları toohello hello eklemek **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-154">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="dcd3c-155">Merhaba yer tutucu değerini hello önceki bölümünde belirtildiği hello cihaz bağlantı dizesini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-155">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="dcd3c-156">Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="dcd3c-156">Add hello following method toohello **Program** class:</span></span>

       public static async void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
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

    <span data-ttu-id="dcd3c-157">Merhaba **istemci** nesne cihaz çiftlerini hello aygıttan ile toointeract duyduğunuz tüm hello yöntemler sunar.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-157">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="dcd3c-158">Merhaba, yukarıda gösterilen kodu başlatır hello **istemci** nesne ve alır hello cihaz çiftinin **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-158">hello code shown above, initializes hello **Client** object, and then retrieves hello device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="dcd3c-159">Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="dcd3c-159">Add hello following method toohello **Program** class:</span></span>
   
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

   <span data-ttu-id="dcd3c-160">Merhaba güncelleştirmeleri yukarıdaki kodu **myDeviceId**hello bağlantı bilgilerini özelliğiyle bildirilen.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-160">hello code above updates **myDeviceId**'s reported property with hello connectivity information.</span></span>

1. <span data-ttu-id="dcd3c-161">Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="dcd3c-161">Finally, add hello following lines toohello **Main** method:</span></span>
   
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
       Console.WriteLine("Press Enter tooexit.");
       Console.ReadLine();

1. <span data-ttu-id="dcd3c-162">Merhaba Hello Çözüm Gezgini, açık **başlangıç projelerini Ayarla...**  ve emin hello **eylem** için **ReportConnectivity** projedir **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-162">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **ReportConnectivity** project is **Start**.</span></span> <span data-ttu-id="dcd3c-163">Merhaba çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-163">Build hello solution.</span></span>
1. <span data-ttu-id="dcd3c-164">Merhaba üzerinde sağ tıklayarak bu uygulamayı çalıştırmak **ReportConnectivity** proje ve seçerek **hata ayıklama**, ardından **başlangıç yeni örnek**.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-164">Run this application by right-clicking on hello **ReportConnectivity** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="dcd3c-165">Merhaba twin bilgi alma ve bağlantı olarak gönderme görmelisiniz bir *özelliği bildirilen*.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-165">You should see it getting hello twin information, and then sending connectivity as a *reported property*.</span></span>
   
    ![Cihaz uygulama tooreport bağlantısı çalıştırın][img-rundeviceapp]
    
    
1. <span data-ttu-id="dcd3c-167">Merhaba aygıt bildirilen bağlantı bilgilerini, her iki sorgularda görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-167">Now that hello device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="dcd3c-168">Merhaba .NET çalıştırmak **AddTagsAndQuery** uygulama toorun hello yeniden sorgular.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-168">Run hello .NET **AddTagsAndQuery** app toorun hello queries again.</span></span> <span data-ttu-id="dcd3c-169">Bu süre **myDeviceId** hem sorgu sonuçlarında görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-169">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![Başarıyla bildirilen cihaz bağlantısı][img-tagappsuccess]

## <a name="next-steps"></a><span data-ttu-id="dcd3c-171">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dcd3c-171">Next steps</span></span>
<span data-ttu-id="dcd3c-172">Bu öğreticide hello Azure portalında yeni bir IOT hub yapılandırılmış ve ardından hello IOT hub'ın kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-172">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="dcd3c-173">Cihaz meta verilerini bir arka uç uygulamadan etiketler eklendi ve bir sanal cihaz uygulaması tooreport aygıt bağlantı bilgilerini hello cihaz çiftine yazıldı.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-173">You added device metadata as tags from a back-end app, and wrote a simulated device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="dcd3c-174">Ayrıca nasıl öğrenilen tooquery hello SQL benzeri IOT hub'ı sorgu dili kullanarak bu bilgileri.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-174">You also learned how tooquery this information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="dcd3c-175">Kaynakları toolearn nasıl aşağıdaki kullanım hello için:</span><span class="sxs-lookup"><span data-stu-id="dcd3c-175">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="dcd3c-176">Merhaba aygıtlarla telemetri gönderen [IOT Hub ile çalışmaya başlama] [ lnk-iothub-getstarted] öğretici</span><span class="sxs-lookup"><span data-stu-id="dcd3c-176">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="dcd3c-177">cihaz çifti'nın istenen özellikleri ile hello kullanarak cihazları yapılandırma [kullanım istenen özellikleri tooconfigure aygıtları] [ lnk-twin-how-to-configure] öğretici,</span><span class="sxs-lookup"><span data-stu-id="dcd3c-177">configure devices using device twin's desired properties with hello [Use desired properties tooconfigure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="dcd3c-178">Merhaba ile etkileşimli olarak (örneğin, kullanıcı tarafından denetlenen bir uygulamadan fan etkinleştirdikten) cihazları denetleme [doğrudan yöntemleri kullanın] [ lnk-methods-tutorial] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="dcd3c-178">control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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

