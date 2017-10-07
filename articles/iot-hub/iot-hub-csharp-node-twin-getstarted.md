---
title: "aaaGet başlatılan Azure IOT Hub cihaz çiftlerini (.NET/düğümü) | Microsoft Docs"
description: "Nasıl toouse Azure IOT Hub cihaz çiftlerini tooadd etiketleri ve IOT Hub sorgusuyla kullanın. Node.js tooimplement hello sanal cihaz uygulamasının ve hello .NET tooimplement hello etiketleri ekler ve hello IOT hub'ı sorgu çalışan bir hizmet uygulaması için Azure IOT hizmeti SDK'sı için hello Azure IOT cihaz SDK'sını kullanın."
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
ms.openlocfilehash: 1cec082ebddc19c9b87998a5fd0159d32b07acd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnode"></a><span data-ttu-id="5813e-104">Cihaz çiftlerini (.NET/düğümü) ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="5813e-104">Get started with device twins (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="5813e-105">Bu öğreticinin Hello sonunda, bir .NET ve bir Node.js konsol uygulaması olacaktır:</span><span class="sxs-lookup"><span data-stu-id="5813e-105">At hello end of this tutorial, you will have a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="5813e-106">**AddTagsAndQuery.sln**, etiketleri ekler ve cihaz çiftlerini sorgular .NET arka uç uygulaması.</span><span class="sxs-lookup"><span data-stu-id="5813e-106">**AddTagsAndQuery.sln**, a .NET back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="5813e-107">**TwinSimulatedDevice.js**, bir cihaza benzetim yapan tooyour IOT hub'ı daha önce oluşturduğunuz hello cihaz kimliği bağlanır ve kendi bağlantı koşulu raporları bir Node.js uygulaması.</span><span class="sxs-lookup"><span data-stu-id="5813e-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects tooyour IoT hub with hello device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="5813e-108">Merhaba makale [Azure IOT SDK'ları] [ lnk-hub-sdks] toobuild kullanabileceğiniz hello Azure IOT SDK'ları hakkında bilgi sağlayan cihaz ve arka uç uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="5813e-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="5813e-109">toocomplete hello aşağıdaki gereksinim Bu öğretici:</span><span class="sxs-lookup"><span data-stu-id="5813e-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="5813e-110">Visual Studio 2015 veya Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="5813e-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="5813e-111">Node.js 0.10.x sürümü veya sonraki bir sürüm.</span><span class="sxs-lookup"><span data-stu-id="5813e-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="5813e-112">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="5813e-112">An active Azure account.</span></span> <span data-ttu-id="5813e-113">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="5813e-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a><span data-ttu-id="5813e-114">Merhaba service uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="5813e-114">Create hello service app</span></span>
<span data-ttu-id="5813e-115">Bu bölümde, konum meta veri toohello cihaz çifti ile ilişkili ekler (C# kullanarak) bir .NET konsol uygulaması oluşturma **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="5813e-115">In this section, you create a .NET console app (using C#) that adds location metadata toohello device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="5813e-116">Ardından hello cihaz çiftlerini hello IOT hub'ı hello bulunan hello aygıtları seçerek BİZE depolanır ve bir cep telefonu bağlantı bildirilen olanları hello sorgular.</span><span class="sxs-lookup"><span data-stu-id="5813e-116">It then queries hello device twins stored in hello IoT hub selecting hello devices located in hello US, and then hello ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="5813e-117">Visual Studio'da hello kullanarak bir Visual C# Windows Klasik Masaüstü projesi toohello geçerli çözüme ekleyin **konsol uygulaması** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="5813e-117">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="5813e-118">Ad hello proje **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="5813e-118">Name hello project **AddTagsAndQuery**.</span></span>
   
    ![Yeni Visual C# Windows Klasik Masaüstü projesi][img-createapp]
1. <span data-ttu-id="5813e-120">Çözüm Gezgini'nde hello sağ **AddTagsAndQuery** proje ve ardından **NuGet paketlerini Yönet...** .</span><span class="sxs-lookup"><span data-stu-id="5813e-120">In Solution Explorer, right-click hello **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="5813e-121">Merhaba, **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat** arayın ve **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="5813e-121">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="5813e-122">Seçin **yükleme** tooinstall hello **Microsoft.Azure.Devices** paketini ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="5813e-122">Select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="5813e-123">Bu yordam indirir, yükler ve başvuru toohello ekler [Azure IOT hizmeti SDK'sını] [ lnk-nuget-service-sdk] NuGet paketi ve bağımlılıklarını.</span><span class="sxs-lookup"><span data-stu-id="5813e-123">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet Paket Yöneticisi penceresi][img-servicenuget]
1. <span data-ttu-id="5813e-125">Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:</span><span class="sxs-lookup"><span data-stu-id="5813e-125">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="5813e-126">Aşağıdaki alanları toohello hello eklemek **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="5813e-126">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="5813e-127">Merhaba hello önceki bölümde oluşturduğunuz hello hub'ın IOT Hub bağlantı dizesine sahip Hello yer tutucu değerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5813e-127">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="5813e-128">Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="5813e-128">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="5813e-129">Merhaba **RegistryManager** sınıfı cihaz çiftlerini hello hizmetinden ile tüm hello yöntemleri gerekli toointeract kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="5813e-129">hello **RegistryManager** class exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="5813e-130">Merhaba önceki kod ilk hello başlatır **registryManager** nesnesi alır cihaz çiftinin hello sonra **myDeviceId**ve son olarak, etiketleri istenen hello konumu bilgilerle güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="5813e-130">hello previous code first initializes hello **registryManager** object, then retrieves hello device twin for **myDeviceId**, and finally updates its tags with hello desired location information.</span></span>
   
    <span data-ttu-id="5813e-131">Güncelleştirdikten sonra iki sorguları yürüten: hello ilk yalnızca hello cihaz çiftlerini hello bulunan aygıtların seçer **Redmond43** tesis ve ayrıca üzerinden bağlanan hello ikinci iyileştirir hello sorgu tooselect yalnızca hello cihazları cep telefonu şebekesi.</span><span class="sxs-lookup"><span data-stu-id="5813e-131">After updating, it executes two queries: hello first selects only hello device twins of devices located in hello **Redmond43** plant, and hello second refines hello query tooselect only hello devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="5813e-132">Merhaba oluşturduğunda bu hello önceki kod Not **sorgu** nesne, döndürülen belgelerin en fazla sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5813e-132">Note that hello previous code, when it creates hello **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="5813e-133">Merhaba **sorgu** nesnesini içeren bir **HasMoreResults** tooinvoke hello kullanabileceğiniz boolean özelliği **GetNextAsTwinAsync** yöntemleri birden çok kez tooretrieve tüm sonuçları.</span><span class="sxs-lookup"><span data-stu-id="5813e-133">hello **query** object contains a **HasMoreResults** boolean property that you can use tooinvoke hello **GetNextAsTwinAsync** methods multiple times tooretrieve all results.</span></span> <span data-ttu-id="5813e-134">Bir yöntem olarak adlandırılan **GetNextAsJson** değil cihaz çiftlerini, örneğin, sonuçları için toplama sorguların sonuçlarını kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5813e-134">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="5813e-135">Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="5813e-135">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="5813e-136">Merhaba Hello Çözüm Gezgini, açık **başlangıç projelerini Ayarla...**  ve emin hello **eylem** için **AddTagsAndQuery** projedir **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="5813e-136">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="5813e-137">Merhaba çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5813e-137">Build hello solution.</span></span>
1. <span data-ttu-id="5813e-138">Merhaba üzerinde sağ tıklayarak bu uygulamayı çalıştırmak **AddTagsAndQuery** proje ve seçerek **hata ayıklama**, ardından **başlangıç yeni örnek**.</span><span class="sxs-lookup"><span data-stu-id="5813e-138">Run this application by right-clicking on hello **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="5813e-139">Bulunan tüm cihazlar için sorgu hello soran bir cihazda hello sonuçlarında görmelisiniz **Redmond43** ve hiçbiri hello kısıtlayan hello sorgu için bir cep telefonu şebekesi kullanmak toodevices sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="5813e-139">You should see one device in hello results for hello query asking for all devices located in **Redmond43** and none for hello query that restricts hello results toodevices that use a cellular network.</span></span>
   
    ![Sorgu Sonuçları penceresinde][img-addtagapp]

<span data-ttu-id="5813e-141">Hello sonraki bölümdeki hello bağlantı bilgilerini raporları bir cihaz uygulaması oluşturma ve değişiklikleri hello önceki bölümdeki hello sorgusunun sonucu hello.</span><span class="sxs-lookup"><span data-stu-id="5813e-141">In hello next section, you create a device app that reports hello connectivity information and changes hello result of hello query in hello previous section.</span></span>

## <a name="create-hello-device-app"></a><span data-ttu-id="5813e-142">Merhaba cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="5813e-142">Create hello device app</span></span>
<span data-ttu-id="5813e-143">Bu bölümde, tooyour hub olarak bağlanan bir Node.js konsol uygulaması oluşturma **myDeviceId**ve ardından, bir cep telefonu şebekesi kullanarak bağlı olduğu bildirilen özellikleri toocontain hello bilgilerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="5813e-143">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, and then updates its reported properties toocontain hello information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="5813e-144">Adlı yeni bir boş klasör oluşturun **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="5813e-144">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="5813e-145">Merhaba, **reportconnectivity** klasörü, komut, komut isteminde aşağıdaki hello kullanarak yeni bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5813e-145">In hello **reportconnectivity** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="5813e-146">Tüm hello Varsayılanları kabul edin.</span><span class="sxs-lookup"><span data-stu-id="5813e-146">Accept all hello defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="5813e-147">Merhaba, komut isteminde **reportconnectivity** klasörüne, komut tooinstall hello aşağıdaki hello **azure IOT cihaz**, ve **azure-IOT-cihaz-mqtt** paketi :</span><span class="sxs-lookup"><span data-stu-id="5813e-147">At your command prompt in hello **reportconnectivity** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="5813e-148">Bir metin düzenleyicisi kullanarak yeni bir oluşturma **ReportConnectivity.js** hello dosyasında **reportconnectivity** klasör.</span><span class="sxs-lookup"><span data-stu-id="5813e-148">Using a text editor, create a new **ReportConnectivity.js** file in hello **reportconnectivity** folder.</span></span>
1. <span data-ttu-id="5813e-149">Aşağıdaki kodu toohello hello eklemek **ReportConnectivity.js** dosya ve hello bir hello oluşturduğunuzda kopyaladığınız cihaz bağlantı dizesi için yer tutucu hello yerine **myDeviceId** aygıt Kimlik:</span><span class="sxs-lookup"><span data-stu-id="5813e-149">Add hello following code toohello **ReportConnectivity.js** file, and substitute hello placeholder for device connection string with hello one you copied when you created hello **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="5813e-150">Merhaba **istemci** nesne cihaz çiftlerini hello aygıttan ile toointeract duyduğunuz tüm hello yöntemler sunar.</span><span class="sxs-lookup"><span data-stu-id="5813e-150">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="5813e-151">Merhaba başlatır sonra önceki kod Hello **istemci** nesnesi alır, cihaz çiftinin hello **myDeviceId** ve kendi bildirilen özelliği hello bağlantı bilgileriyle güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="5813e-151">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId** and updates its reported property with hello connectivity information.</span></span>
1. <span data-ttu-id="5813e-152">Merhaba cihaz uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5813e-152">Run hello device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="5813e-153">Merhaba iletiyi görmeniz gerekir `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="5813e-153">You should see hello message `twin state reported`.</span></span>
1. <span data-ttu-id="5813e-154">Merhaba aygıt bildirilen bağlantı bilgilerini, her iki sorgularda görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="5813e-154">Now that hello device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="5813e-155">Merhaba .NET çalıştırmak **AddTagsAndQuery** uygulama toorun hello yeniden sorgular.</span><span class="sxs-lookup"><span data-stu-id="5813e-155">Run hello .NET **AddTagsAndQuery** app toorun hello queries again.</span></span> <span data-ttu-id="5813e-156">Bu süre **myDeviceId** hem sorgu sonuçlarında görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5813e-156">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][img-addtagapp2]

## <a name="next-steps"></a><span data-ttu-id="5813e-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5813e-157">Next steps</span></span>
<span data-ttu-id="5813e-158">Bu öğreticide hello Azure portalında yeni bir IOT hub yapılandırılmış ve ardından hello IOT hub'ın kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="5813e-158">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="5813e-159">Cihaz meta verilerini bir arka uç uygulamadan etiketler eklendi ve bir sanal cihaz uygulaması tooreport aygıt bağlantı bilgilerini hello cihaz çiftine yazıldı.</span><span class="sxs-lookup"><span data-stu-id="5813e-159">You added device metadata as tags from a back-end app, and wrote a simulated device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="5813e-160">Ayrıca nasıl öğrenilen tooquery hello SQL benzeri IOT hub'ı sorgu dili kullanarak bu bilgileri.</span><span class="sxs-lookup"><span data-stu-id="5813e-160">You also learned how tooquery this information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="5813e-161">Kaynakları toolearn nasıl aşağıdaki kullanım hello için:</span><span class="sxs-lookup"><span data-stu-id="5813e-161">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="5813e-162">Merhaba aygıtlarla telemetri gönderen [IOT Hub ile çalışmaya başlama] [ lnk-iothub-getstarted] öğretici</span><span class="sxs-lookup"><span data-stu-id="5813e-162">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="5813e-163">cihaz çifti'nın istenen özellikleri ile hello kullanarak cihazları yapılandırma [kullanım istenen özellikleri tooconfigure aygıtları] [ lnk-twin-how-to-configure] öğretici,</span><span class="sxs-lookup"><span data-stu-id="5813e-163">configure devices using device twin's desired properties with hello [Use desired properties tooconfigure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="5813e-164">Merhaba ile etkileşimli olarak (örneğin, kullanıcı tarafından denetlenen bir uygulamadan fan etkinleştirdikten) cihazları denetleme [doğrudan yöntemleri kullanın] [ lnk-methods-tutorial] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="5813e-164">control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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

