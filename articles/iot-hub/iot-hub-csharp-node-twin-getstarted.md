---
title: "Azure IOT Hub cihaz çiftlerini (.NET/düğümü) ile çalışmaya başlama | Microsoft Docs"
description: "Azure IOT Hub cihaz çiftlerini etiket ekleyebilir ve IOT Hub sorgusuyla kullanmak için nasıl kullanılacağını. Sanal cihaz uygulamasının ve Azure IOT hizmeti SDK'sını etiketleri ekler ve IOT hub'ı sorgu çalışan bir hizmet uygulaması uygulamak .NET için uygulamak için Azure IOT cihaz SDK'sı Node.js için kullanın."
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: elioda
ms.openlocfilehash: 07797b9159c9b926e9eb47d8864c63048951931a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-device-twins-netnode"></a><span data-ttu-id="c8d10-104">Cihaz çiftlerini (.NET/düğümü) ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="c8d10-104">Get started with device twins (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="c8d10-105">Bu öğreticinin sonunda bir .NET ve bir Node.js konsol uygulaması olacaktır:</span><span class="sxs-lookup"><span data-stu-id="c8d10-105">At the end of this tutorial, you will have a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="c8d10-106">**AddTagsAndQuery.sln**, etiketleri ekler ve cihaz çiftlerini sorgular .NET arka uç uygulaması.</span><span class="sxs-lookup"><span data-stu-id="c8d10-106">**AddTagsAndQuery.sln**, a .NET back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="c8d10-107">**TwinSimulatedDevice.js**, bir cihaza benzetim yapan daha önce oluşturulan cihaz kimliğiyle IOT hub'ınıza bağlanır ve kendi bağlantı koşulu raporları bir Node.js uygulaması.</span><span class="sxs-lookup"><span data-stu-id="c8d10-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="c8d10-108">Makaleyi [Azure IOT SDK'ları] [ lnk-hub-sdks] hem cihaz hem de arka uç uygulamalar oluşturmak için kullanabileceğiniz Azure IOT SDK'ları hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="c8d10-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="c8d10-109">Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="c8d10-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="c8d10-110">Visual Studio 2015 veya Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="c8d10-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="c8d10-111">Node.js 0.10.x sürümü veya sonraki bir sürüm.</span><span class="sxs-lookup"><span data-stu-id="c8d10-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="c8d10-112">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="c8d10-112">An active Azure account.</span></span> <span data-ttu-id="c8d10-113">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="c8d10-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-service-app"></a><span data-ttu-id="c8d10-114">Hizmet Uygulaması Oluştur</span><span class="sxs-lookup"><span data-stu-id="c8d10-114">Create the service app</span></span>
<span data-ttu-id="c8d10-115">Bu bölümde, konum meta verileri ile ilişkili cihaz çifti ekler (C# kullanarak) bir .NET konsol uygulaması oluşturma **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="c8d10-115">In this section, you create a .NET console app (using C#) that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="c8d10-116">Ardından, IOT hub'ı ABD, ardından bir cep telefonu bağlantı bildirilen olanları içinde bulunan aygıtları seçerek depolanan cihaz çiftlerini sorgular.</span><span class="sxs-lookup"><span data-stu-id="c8d10-116">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="c8d10-117">Visual Studio'da **Konsol Uygulaması** proje şablonunu kullanarak geçerli çözüme bir Visual C# Windows Klasik Masaüstü projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c8d10-117">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="c8d10-118">Proje adı **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="c8d10-118">Name the project **AddTagsAndQuery**.</span></span>
   
    ![Yeni Visual C# Windows Klasik Masaüstü projesi][img-createapp]
1. <span data-ttu-id="c8d10-120">Çözüm Gezgini'nde sağ **AddTagsAndQuery** proje ve ardından **NuGet paketlerini Yönet...** .</span><span class="sxs-lookup"><span data-stu-id="c8d10-120">In Solution Explorer, right-click the **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="c8d10-121">İçinde **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat** arayın ve **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="c8d10-121">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="c8d10-122">Seçin **yükleme** yüklemek için **Microsoft.Azure.Devices** paketini ve kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="c8d10-122">Select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="c8d10-123">Bu yordam ile [Azure IoT hizmet SDK'sı][lnk-nuget-service-sdk] NuGet paketi ve bağımlılıkları indirilir, yüklenir ve bu pakete bir başvuru eklenir.</span><span class="sxs-lookup"><span data-stu-id="c8d10-123">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet Paket Yöneticisi penceresi][img-servicenuget]
1. <span data-ttu-id="c8d10-125">Aşağıdaki `using` deyimlerini **Program.cs** dosyasının üst kısmına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c8d10-125">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="c8d10-126">**Program** sınıfına aşağıdaki alanları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c8d10-126">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="c8d10-127">Yer tutucu değerini, önceki bölümde hub için oluşturduğunuz IoT Hub bağlantı dizesiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c8d10-127">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="c8d10-128">**Program** sınıfına aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c8d10-128">Add the following method to the **Program** class:</span></span>
   
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
   
    <span data-ttu-id="c8d10-129">**RegistryManager** sınıfı cihaz çiftlerini hizmet ile etkileşim kurmak için gereken tüm yöntemleri sunar.</span><span class="sxs-lookup"><span data-stu-id="c8d10-129">The **RegistryManager** class exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="c8d10-130">Önceki kod ilk başlatır **registryManager** nesnesi, ardından cihaz çiftinin alır **myDeviceId**ve son olarak, etiketleri istenen konumu bilgilerle güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="c8d10-130">The previous code first initializes the **registryManager** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="c8d10-131">Güncelleştirdikten sonra iki sorguları yürüten: yalnızca cihaz çiftlerini bulunan aygıtların ilk seçer **Redmond43** tesis ve ikinci da cep telefonu şebekesi bağlı aygıtlar seçmek için sorgu iyileştirir.</span><span class="sxs-lookup"><span data-stu-id="c8d10-131">After updating, it executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="c8d10-132">Unutmayın, oluşturduğunda, önceki kod **sorgu** nesne, döndürülen belgelerin en fazla sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8d10-132">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="c8d10-133">**Sorgu** nesnesini içeren bir **HasMoreResults** çağırmak için kullanabileceğiniz boolean özelliği **GetNextAsTwinAsync** birden çok kez tüm sonuçları almak için yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="c8d10-133">The **query** object contains a **HasMoreResults** boolean property that you can use to invoke the **GetNextAsTwinAsync** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="c8d10-134">Bir yöntem olarak adlandırılan **GetNextAsJson** değil cihaz çiftlerini, örneğin, sonuçları için toplama sorguların sonuçlarını kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c8d10-134">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="c8d10-135">Son olarak, **Main** yöntemine aşağıdaki satırları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c8d10-135">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

1. <span data-ttu-id="c8d10-136">Çözüm Gezgini'nde açık **başlangıç projelerini Ayarla...**  ve emin olun **eylem** için **AddTagsAndQuery** projedir **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="c8d10-136">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="c8d10-137">Çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c8d10-137">Build the solution.</span></span>
1. <span data-ttu-id="c8d10-138">Üzerinde sağ tıklayarak bu uygulamayı çalıştırmak **AddTagsAndQuery** proje ve seçerek **hata ayıklama**, ardından **başlangıç yeni örnek**.</span><span class="sxs-lookup"><span data-stu-id="c8d10-138">Run this application by right-clicking on the **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="c8d10-139">Bulunan tüm cihazlar için sorgu soran bir cihazda sonuçlarında görmelisiniz **Redmond43** ve sonuçları bir cep telefonu şebekesi kullanan cihazlar için sınırlar sorgu için yok.</span><span class="sxs-lookup"><span data-stu-id="c8d10-139">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![Sorgu Sonuçları penceresinde][img-addtagapp]

<span data-ttu-id="c8d10-141">Sonraki bölümde, önceki bölümde sorgusunun sonucu değiştirir ve bağlantı bilgilerini raporlar bir cihaz uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="c8d10-141">In the next section, you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="c8d10-142">Cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="c8d10-142">Create the device app</span></span>
<span data-ttu-id="c8d10-143">Bu bölümde, hub'ınıza bağlanan bir Node.js konsol uygulaması oluşturma **myDeviceId**ve ardından bir cep telefonu şebekesi kullanarak bağlı bilgileri içerecek şekilde bildirilen özelliklerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="c8d10-143">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, and then updates its reported properties to contain the information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="c8d10-144">Adlı yeni bir boş klasör oluşturun **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="c8d10-144">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="c8d10-145">İçinde **reportconnectivity** klasörü, komut isteminde aşağıdaki komutu kullanarak yeni bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c8d10-145">In the **reportconnectivity** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="c8d10-146">Tüm Varsayılanları kabul edin.</span><span class="sxs-lookup"><span data-stu-id="c8d10-146">Accept all the defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="c8d10-147">Komut isteminizde **reportconnectivity** klasörü yüklemek için aşağıdaki komutu çalıştırın, **azure IOT cihaz**, ve **azure-IOT-cihaz-mqtt** paketi:</span><span class="sxs-lookup"><span data-stu-id="c8d10-147">At your command prompt in the **reportconnectivity** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="c8d10-148">Bir metin düzenleyicisi kullanarak yeni bir oluşturma **ReportConnectivity.js** dosyasını **reportconnectivity** klasör.</span><span class="sxs-lookup"><span data-stu-id="c8d10-148">Using a text editor, create a new **ReportConnectivity.js** file in the **reportconnectivity** folder.</span></span>
1. <span data-ttu-id="c8d10-149">Aşağıdaki kodu ekleyin **ReportConnectivity.js** dosya ve oluştururken kopyaladığınız bir aygıt bağlantı dizesi için yer tutucu yerine **myDeviceId** cihaz kimliği:</span><span class="sxs-lookup"><span data-stu-id="c8d10-149">Add the following code to the **ReportConnectivity.js** file, and substitute the placeholder for device connection string with the one you copied when you created the **myDeviceId** device identity:</span></span>
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
   
            client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                var patch = {
                    connectivity: {
                        type: 'cellular'
                    }
                };
   
                twin.properties.reported.update(patch, function(err) {
                    if (err) {
                        console.error('could not update twin');
                    } else {
                        console.log('twin state reported');
                        process.exit();
                    }
                });
            }
            });
        }
        });
   
    <span data-ttu-id="c8d10-150">**İstemci** nesne ihtiyaç duyduğunuz etkileşim kurmak için cihaz çiftlerini aygıttan ile tüm yöntemleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="c8d10-150">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="c8d10-151">Bunu başlatır sonra önceki kod **istemci** nesnesi, cihaz çiftinin alır **myDeviceId** ve kendi bildirilen özelliği ile bağlantı bilgilerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="c8d10-151">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId** and updates its reported property with the connectivity information.</span></span>
1. <span data-ttu-id="c8d10-152">Cihaz uygulama çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c8d10-152">Run the device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="c8d10-153">Şu iletiyi görürsünüz `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="c8d10-153">You should see the message `twin state reported`.</span></span>
1. <span data-ttu-id="c8d10-154">Aygıt bağlantısı bilgilerini bildirdi, her iki sorgularda görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="c8d10-154">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="c8d10-155">.NET çalıştırmak **AddTagsAndQuery** uygulama sorguları yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c8d10-155">Run the .NET **AddTagsAndQuery** app to run the queries again.</span></span> <span data-ttu-id="c8d10-156">Bu süre **myDeviceId** hem sorgu sonuçlarında görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8d10-156">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][img-addtagapp2]

## <a name="next-steps"></a><span data-ttu-id="c8d10-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c8d10-157">Next steps</span></span>
<span data-ttu-id="c8d10-158">Bu öğreticide, Azure portalında yeni bir IoT hub'ı yapılandırdınız ve ardından IoT hub'ının kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="c8d10-158">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="c8d10-159">Cihaz meta verilerini bir arka uç uygulamadan etiketler eklendi ve sanal cihaz uygulaması rapor cihaz bağlantı bilgilerini cihaz çiftine yazıldı.</span><span class="sxs-lookup"><span data-stu-id="c8d10-159">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="c8d10-160">Ayrıca SQL benzeri IOT hub'ı sorgu dili kullanarak bu bilgileri sorgulamak öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="c8d10-160">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="c8d10-161">Bilgi edinmek için aşağıdaki kaynakları kullanın nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="c8d10-161">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="c8d10-162">aygıtlarla telemetri gönderen [IOT Hub ile çalışmaya başlama] [ lnk-iothub-getstarted] öğretici</span><span class="sxs-lookup"><span data-stu-id="c8d10-162">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="c8d10-163">cihaz çifti'nın istenen özelliklere sahip kullanarak cihazları yapılandırma [kullanmak istediğiniz cihazları yapılandırmak için Özellikler] [ lnk-twin-how-to-configure] öğretici</span><span class="sxs-lookup"><span data-stu-id="c8d10-163">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="c8d10-164">aygıtlarını etkileşimli olarak (örneğin, kullanıcı tarafından denetlenen bir uygulamadan fan etkinleştirdikten) ile [doğrudan yöntemleri kullanın] [ lnk-methods-tutorial] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="c8d10-164">control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-node-twin-getstarted/addtagapp.png
[img-addtagapp2]: media/iot-hub-csharp-node-twin-getstarted/addtagapp2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

