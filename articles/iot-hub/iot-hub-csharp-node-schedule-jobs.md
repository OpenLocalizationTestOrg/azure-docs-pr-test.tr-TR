---
title: "Azure IOT hub'ı (.NET/düğümü) aaaSchedule işleriyle | Microsoft Docs"
description: "Nasıl tooschedule Azure IOT hub'ı işi tooinvoke birden çok aygıta doğrudan bir yöntem. Node.js tooimplement benzetimli hello cihaz uygulamaları ve hello .NET tooimplement bir hizmeti uygulama toorun hello işi için Azure IOT hizmeti SDK'sı için hello Azure IOT cihaz SDK'sını kullanın."
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
ms.date: 07/10/2017
ms.author: juanpere
ms.openlocfilehash: f6148b67129dde4580bfe9ccceafd6400fbc5976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-netnodejs"></a><span data-ttu-id="a4ab7-104">Zamanlama ve yayın işleri (.NET/Node.js)</span><span class="sxs-lookup"><span data-stu-id="a4ab7-104">Schedule and broadcast jobs (.NET/Node.js)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="a4ab7-105">Milyonlarca cihaza güncelleştirme Azure IOT Hub tooschedule ve izleme işlemlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-105">Use Azure IoT Hub tooschedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="a4ab7-106">İşlerini kullanın:</span><span class="sxs-lookup"><span data-stu-id="a4ab7-106">Use jobs to:</span></span>

* <span data-ttu-id="a4ab7-107">İstenen özellikleri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="a4ab7-107">Update desired properties</span></span>
* <span data-ttu-id="a4ab7-108">Güncelleştirme etiketleri</span><span class="sxs-lookup"><span data-stu-id="a4ab7-108">Update tags</span></span>
* <span data-ttu-id="a4ab7-109">Doğrudan yöntemleri çağırma</span><span class="sxs-lookup"><span data-stu-id="a4ab7-109">Invoke direct methods</span></span>

<span data-ttu-id="a4ab7-110">Bir işi şu eylemlerden birini sarmalar ve cihaz çifti sorgu tarafından tanımlanan bir dizi cihazların yürütmeyi parçaları hello.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-110">A job wraps one of these actions and tracks hello execution against a set of devices that is defined by a device twin query.</span></span> <span data-ttu-id="a4ab7-111">Örneğin, bir arka uç uygulaması iş tooinvoke doğrudan bir yöntem hello aygıtları yeniden 10.000 cihazlarda kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-111">For example, a back-end app can use a job tooinvoke a direct method on 10,000 devices that reboots hello devices.</span></span> <span data-ttu-id="a4ab7-112">Cihaz hello kümesini içeren bir cihaz çifti sorgu belirtin ve gelecek bir zamanda hello iş toorun zamanlayın.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-112">You specify hello set of devices with a device twin query and schedule hello job toorun at a future time.</span></span> <span data-ttu-id="a4ab7-113">Merhaba parçaları ilerleyişini her hello aygıtların almak ve hello yeniden başlatma doğrudan yöntemi yürütün.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-113">hello job tracks progress as each of hello devices receive and execute hello reboot direct method.</span></span>

<span data-ttu-id="a4ab7-114">Bu özelliklerin her biri hakkında daha fazla toolearn bakın:</span><span class="sxs-lookup"><span data-stu-id="a4ab7-114">toolearn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="a4ab7-115">Cihaz çifti ve özellikleri: [cihaz çiftlerini ile çalışmaya başlama] [ lnk-get-started-twin] ve [Öğreticisi: nasıl toouse cihaz çifti özellikleri][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="a4ab7-115">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How toouse device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="a4ab7-116">Doğrudan yöntemleri: [IOT Hub Geliştirici Kılavuzu - doğrudan yöntemleri] [ lnk-dev-methods] ve [Öğreticisi: doğrudan yöntemleri kullanın][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="a4ab7-116">Direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: Use direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="a4ab7-117">Bu öğretici şunların nasıl yapıldığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="a4ab7-117">This tutorial shows you how to:</span></span>

* <span data-ttu-id="a4ab7-118">Adlı doğrudan bir yöntem uygulayan bir cihaz uygulaması oluşturma **lockDoor** hello arka uç uygulama tarafından çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-118">Create a device app that implements a direct method called **lockDoor** that can be called by hello back-end app.</span></span> <span data-ttu-id="a4ab7-119">Merhaba cihaz uygulaması istenen özellik değişikliklerini hello arka uç uygulamasını da alır.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-119">hello device app also receives desired property changes from hello back-end app.</span></span>
* <span data-ttu-id="a4ab7-120">Bir iş toocall hello oluşturan bir arka uç uygulaması oluşturma **lockDoor** birden fazla cihazda yöntemi doğrudan.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-120">Create a back-end app that creates a job toocall hello **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="a4ab7-121">Başka bir iş, istenen özelliği toomultiple aygıtları güncelleştirir gönderir.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-121">Another job sends desired property updates toomultiple devices.</span></span>

<span data-ttu-id="a4ab7-122">Bu öğretici Hello sonunda bir Node.js konsol cihaz uygulaması ve bir .NET (C#) konsol arka uç uygulaması sahiptir:</span><span class="sxs-lookup"><span data-stu-id="a4ab7-122">At hello end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="a4ab7-123">**simDevice.js** tooyour IOT hub'a bağlandığında, uygulayan hello **lockDoor** yöntemi ve tanıtıcıları istenen özellik değişikliklerini doğrudan.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-123">**simDevice.js** that connects tooyour IoT hub, implements hello **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="a4ab7-124">**ScheduleJob** işleri toocall hello kullanan **lockDoor** doğrudan yöntemi ve güncelleştirme hello cihaz çifti istenen birden çok cihazı özellikleri.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-124">**ScheduleJob** that uses jobs toocall hello **lockDoor** direct method and update hello device twin desired properties on multiple devices.</span></span>

<span data-ttu-id="a4ab7-125">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="a4ab7-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="a4ab7-126">Visual Studio 2015 veya Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-126">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="a4ab7-127">Node.js 0.12.x sürümü veya sonraki bir sürüm.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-127">Node.js version 0.12.x or later.</span></span> <span data-ttu-id="a4ab7-128">Merhaba makale [geliştirme ortamınızı hazırlama] [ lnk-dev-setup] açıklar nasıl tooinstall Node.js Bu öğretici için Windows veya Linux üzerinde.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-128">hello article [Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="a4ab7-129">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-129">An active Azure account.</span></span> <span data-ttu-id="a4ab7-130">Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-130">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-sending-device-twin-updates"></a><span data-ttu-id="a4ab7-131">Doğrudan bir yöntem çağırma ve cihaz çifti güncelleştirmeleri göndermek için zamanlama işleri</span><span class="sxs-lookup"><span data-stu-id="a4ab7-131">Schedule jobs for calling a direct method and sending device twin updates</span></span>

<span data-ttu-id="a4ab7-132">Bu bölümde, işleri toocall hello kullanır (C# kullanarak) bir .NET konsol uygulaması oluşturma **lockDoor** doğrudan yöntemi ve istenen özelliği güncelleştirmeleri toomultiple aygıtları gönderin.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-132">In this section, you create a .NET console app (using C#) that uses jobs toocall hello **lockDoor** direct method and send desired property updates toomultiple devices.</span></span>

1. <span data-ttu-id="a4ab7-133">Visual Studio'da hello kullanarak bir Visual C# Windows Klasik Masaüstü projesi toohello geçerli çözüme ekleyin **konsol uygulaması** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-133">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="a4ab7-134">Ad hello proje **ScheduleJob**.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-134">Name hello project **ScheduleJob**.</span></span>

    ![Yeni Visual C# Windows Klasik Masaüstü projesi][img-createapp]

1. <span data-ttu-id="a4ab7-136">Çözüm Gezgini'nde hello sağ **ScheduleJob** proje ve ardından **NuGet paketlerini Yönet...** .</span><span class="sxs-lookup"><span data-stu-id="a4ab7-136">In Solution Explorer, right-click hello **ScheduleJob** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="a4ab7-137">Merhaba, **NuGet Paket Yöneticisi** penceresinde, seçin **Gözat**, arama **microsoft.azure.devices**seçin **yükleme** tooinstall Merhaba **Microsoft.Azure.Devices** paketini ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-137">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="a4ab7-138">Bu adım indirir, yükler ve başvuru toohello ekler [Azure IOT hizmeti SDK'sını] [ lnk-nuget-service-sdk] NuGet paketi ve bağımlılıklarını.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-138">This step downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![NuGet Paket Yöneticisi penceresi][img-servicenuget]
1. <span data-ttu-id="a4ab7-140">Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **Program.cs** dosyası:</span><span class="sxs-lookup"><span data-stu-id="a4ab7-140">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
    
    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Shared;
    ```

1. <span data-ttu-id="a4ab7-141">Merhaba aşağıdakileri ekleyin `using` deyimi yoksa hello varsayılan deyimlerinde.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-141">Add hello following `using` statement if not already present in hello default statements.</span></span>

    ```csharp
    using System.Threading.Tasks;
    ```

1. <span data-ttu-id="a4ab7-142">Aşağıdaki alanları toohello hello eklemek **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-142">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="a4ab7-143">Merhaba yer tutucu hello hello önceki bölümde oluşturduğunuz hello hub için IOT Hub bağlantı dizesini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-143">Replace hello placeholder with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>

    ```csharp
    static string connString = "{iot hub connection string}";
    static ServiceClient client;
    static JobClient jobClient;
    ```

1. <span data-ttu-id="a4ab7-144">Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="a4ab7-144">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    public static async Task MonitorJob(string jobId)
    {
        JobResponse result;
        do
        {
            result = await jobClient.GetJobAsync(jobId);
            Console.WriteLine("Job Status : " + result.Status.ToString());
            Thread.Sleep(2000);
        } while ((result.Status != JobStatus.Completed) && (result.Status != JobStatus.Failed));
    }
    ```

1. <span data-ttu-id="a4ab7-145">Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="a4ab7-145">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    public static async Task StartMethodJob(string jobId)
    {
        CloudToDeviceMethod directMethod = new CloudToDeviceMethod("lockDoor", TimeSpan.FromSeconds(5), TimeSpan.FromSeconds(5));

        JobResponse result = await jobClient.ScheduleDeviceMethodAsync(jobId,
            "deviceId='myDeviceId'",
            directMethod,
            DateTime.Now,
            10);

        Console.WriteLine("Started Method Job");
    }
    ```

1. <span data-ttu-id="a4ab7-146">Yöntem toohello aşağıdaki hello eklemek **Program** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="a4ab7-146">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    public static async Task StartTwinUpdateJob(string jobId)
    {
        var twin = new Twin();
        twin.Properties.Desired["Building"] = "43";
        twin.Properties.Desired["Floor"] = "3";
        twin.ETag = "*";

        JobResponse result = await jobClient.ScheduleTwinUpdateAsync(jobId,
            "deviceId='myDeviceId'",
            twin,
            DateTime.Now,
            10);

        Console.WriteLine("Started Twin Update Job");
    }
    ```

1. <span data-ttu-id="a4ab7-147">Son olarak, aşağıdaki satırları toohello hello eklemek **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="a4ab7-147">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    jobClient = JobClient.CreateFromConnectionString(connString);

    string methodJobId = Guid.NewGuid().ToString();

    StartMethodJob(methodJobId);
    MonitorJob(methodJobId).Wait();
    Console.WriteLine("Press ENTER toorun hello next job.");
    Console.ReadLine();

    string twinUpdateJobId = Guid.NewGuid().ToString();

    StartTwinUpdateJob(twinUpdateJobId);
    MonitorJob(twinUpdateJobId).Wait();
    Console.WriteLine("Press ENTER tooexit.");
    Console.ReadLine();
    ```

1. <span data-ttu-id="a4ab7-148">Merhaba Hello Çözüm Gezgini, açık **başlangıç projelerini Ayarla...**  ve emin hello **eylem** için **ScheduleJob** projedir **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-148">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **ScheduleJob** project is **Start**.</span></span> <span data-ttu-id="a4ab7-149">Merhaba çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-149">Build hello solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="a4ab7-150">Sanal cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4ab7-150">Create a simulated device app</span></span>

<span data-ttu-id="a4ab7-151">Bu bölümde, sanal cihaz yeniden başlatma tetikler hello bulut tarafından adlı tooa doğrudan yöntemi yanıt bir Node.js konsol uygulaması oluşturun ve Özellikler tooenable cihaz çifti sorguları tooidentify aygıtlar ve bunların en son ne zaman yeniden kullandığı hello rapor.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-151">In this section, you create a Node.js console app that responds tooa direct method called by hello cloud, which triggers a simulated device reboot and uses hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="a4ab7-152">Adlı yeni bir boş klasör oluşturun **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-152">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="a4ab7-153">Merhaba, **simDevice** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-153">In hello **simDevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="a4ab7-154">Tüm hello Varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="a4ab7-154">Accept all hello defaults:</span></span>

    ```cmd/sh
    npm init
    ```

1. <span data-ttu-id="a4ab7-155">Merhaba, komut isteminde **simDevice** klasörüne, komut tooinstall hello aşağıdaki hello **azure IOT cihaz** ve **azure-IOT-cihaz-mqtt** paketler:</span><span class="sxs-lookup"><span data-stu-id="a4ab7-155">At your command prompt in hello **simDevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>

    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="a4ab7-156">Bir metin düzenleyicisi kullanarak yeni bir oluşturma **simDevice.js** hello dosyasında **simDevice** klasör.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-156">Using a text editor, create a new **simDevice.js** file in hello **simDevice** folder.</span></span>

1. <span data-ttu-id="a4ab7-157">Merhaba aşağıdaki 'İste' hello hello başlangıç deyimleri ekleme **simDevice.js** dosyası:</span><span class="sxs-lookup"><span data-stu-id="a4ab7-157">Add hello following 'require' statements at hello start of hello **simDevice.js** file:</span></span>

    ```nodejs
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```

1. <span data-ttu-id="a4ab7-158">Ekleme bir **connectionString** değişken ve toocreate kullanan bir **istemci** örneği.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-158">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="a4ab7-159">Değerleri uygun tooyour Kurulum emin tooreplace hello yer tutucularını olun.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-159">Make sure tooreplace hello placeholders with values appropriate tooyour setup.</span></span>

    ```nodejs
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="a4ab7-160">İşlev toohandle hello aşağıdaki hello eklemek **lockDoor** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-160">Add hello following function toohandle hello **lockDoor** method.</span></span>

    ```nodejs
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

1. <span data-ttu-id="a4ab7-161">Kod tooregister hello işleyici hello için aşağıdaki hello eklemek **lockDoor** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-161">Add hello following code tooregister hello handler for hello **lockDoor** method.</span></span>

    ```nodejs
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub.  Waiting for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```

1. <span data-ttu-id="a4ab7-162">Kaydet ve Kapat hello **simDevice.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-162">Save and close hello **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="a4ab7-163">tookeep şeyler basit, Bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-163">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="a4ab7-164">Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="a4ab7-164">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="a4ab7-165">Merhaba uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="a4ab7-165">Run hello apps</span></span>

<span data-ttu-id="a4ab7-166">Hazır toorun hello uygulamaları sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-166">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="a4ab7-167">Merhaba hello komut isteminde **simDevice** klasöründe şunu hello yeniden başlatma doğrudan yöntemi için dinleme komutu toobegin aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-167">At hello command prompt in hello **simDevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>

    ```cmd/sh
    node simDevice.js
    ```

1. <span data-ttu-id="a4ab7-168">Çalışma hello C# konsol uygulaması **ScheduleJob** hello üzerinde sağ tıklanarak **ScheduleJob** sonra seçerek proje **hata ayıklama** ve **başlangıç yeni örnek**.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-168">Run hello C# console app **ScheduleJob** by right-clicking on hello **ScheduleJob** project, then selecting **Debug** and **Start new instance**.</span></span>

1. <span data-ttu-id="a4ab7-169">Cihaz ve arka uç uygulamaları hello çıktısını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-169">You see hello output from both device and back-end apps.</span></span>

    ![Merhaba uygulamaları tooschedule işleri çalıştırma][img-schedulejobs]

## <a name="next-steps"></a><span data-ttu-id="a4ab7-171">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a4ab7-171">Next steps</span></span>

<span data-ttu-id="a4ab7-172">Bu öğreticide, bir iş tooschedule doğrudan yöntemi tooa cihaz ve hello güncelleştirme hello cihaz çifti'nın özelliklerinin kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-172">In this tutorial, you used a job tooschedule a direct method tooa device and hello update of hello device twin's properties.</span></span>

<span data-ttu-id="a4ab7-173">Uzaktan gibi IOT Hub ve cihaz yönetim düzenleri hava bellenim güncelleştirme okuma hello kullanmaya Başlarken toocontinue [Öğreticisi: toodo üretici yazılımı güncelleştirme nasıl][lnk-fwupdate].</span><span class="sxs-lookup"><span data-stu-id="a4ab7-173">toocontinue getting started with IoT Hub and device management patterns such as remote over hello air firmware update, read [Tutorial: How toodo a firmware update][lnk-fwupdate].</span></span>

<span data-ttu-id="a4ab7-174">IOT Hub ile çalışmaya başlama toocontinue bkz [IOT Edge ile çalışmaya başlama][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="a4ab7-174">toocontinue getting started with IoT Hub, see [Getting started with IoT Edge][lnk-iot-edge].</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-schedule-jobs/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-schedule-jobs/createnetapp.png
[img-schedulejobs]: media/iot-hub-csharp-node-schedule-jobs/schedulejobs.png

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
