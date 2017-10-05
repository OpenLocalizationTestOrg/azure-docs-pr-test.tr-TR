---
title: "Önceden yapılandırılmış çözümleri özelleştirme | Microsoft Docs"
description: "Azure IOT paketi önceden yapılandırılmış çözümleri Özelleştirme Kılavuzu verilmektedir."
services: 
suite: iot-suite
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4653ae53-4110-4a10-bd6c-7dc034c293a8
ms.service: iot-suite
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: bdf4cd89d5ad0392337dfe761108608d506adf18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="customize-a-preconfigured-solution"></a><span data-ttu-id="9def7-103">Önceden yapılandırılmış bir çözümü özelleştirme</span><span class="sxs-lookup"><span data-stu-id="9def7-103">Customize a preconfigured solution</span></span>

<span data-ttu-id="9def7-104">Azure IOT paketi ile sağlanan önceden yapılandırılmış çözümler bir uçtan uca çözümü sunmak için birlikte çalışan suite içinde hizmetlerini gösterme.</span><span class="sxs-lookup"><span data-stu-id="9def7-104">The preconfigured solutions provided with the Azure IoT Suite demonstrate the services within the suite working together to deliver an end-to-end solution.</span></span> <span data-ttu-id="9def7-105">Bu başlangıç noktasından genişletmek ve belirli senaryolar için çözümü özelleştirme çeşitli yerlerde vardır.</span><span class="sxs-lookup"><span data-stu-id="9def7-105">From this starting point, there are various places in which you can extend and customize the solution for specific scenarios.</span></span> <span data-ttu-id="9def7-106">Aşağıdaki bölümlerde bu ortak özelleştirme noktalarını açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9def7-106">The following sections describe these common customization points.</span></span>

## <a name="find-the-source-code"></a><span data-ttu-id="9def7-107">Kaynak kodu bulun</span><span class="sxs-lookup"><span data-stu-id="9def7-107">Find the source code</span></span>

<span data-ttu-id="9def7-108">Önceden yapılandırılmış çözümler için kaynak kodunu şu depoları Github'da kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="9def7-108">The source code for the preconfigured solutions is available on GitHub in the following repositories:</span></span>

* <span data-ttu-id="9def7-109">Uzaktan izleme: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span><span class="sxs-lookup"><span data-stu-id="9def7-109">Remote Monitoring: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span></span>
* <span data-ttu-id="9def7-110">Tahmine dayalı Bakım: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span><span class="sxs-lookup"><span data-stu-id="9def7-110">Predictive Maintenance: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span></span>
* <span data-ttu-id="9def7-111">Bağlı Fabrika: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span><span class="sxs-lookup"><span data-stu-id="9def7-111">Connected factory: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span></span>

<span data-ttu-id="9def7-112">Önceden yapılandırılmış çözümler için kaynak kodunu desenleri ve Azure IOT paketi kullanarak bir IOT çözüm uçtan uca işlevselliğini uygulamak için kullanılan yöntemler göstermek için sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9def7-112">The source code for the preconfigured solutions is provided to demonstrate the patterns and practices used to implement the end-to-end functionality of an IoT solution using Azure IoT Suite.</span></span> <span data-ttu-id="9def7-113">Derleme ve GitHub depolarının çözümlerinde dağıtma hakkında daha fazla bilgi bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9def7-113">You can find more information about how to build and deploy the solutions in the GitHub repositories.</span></span>

## <a name="change-the-preconfigured-rules"></a><span data-ttu-id="9def7-114">Önceden yapılandırılmış kurallarını değiştirin</span><span class="sxs-lookup"><span data-stu-id="9def7-114">Change the preconfigured rules</span></span>

<span data-ttu-id="9def7-115">Uzaktan izleme çözümü üç içeren [Azure akış analizi](https://azure.microsoft.com/services/stream-analytics/) cihaz bilgilerini, telemetri ve çözümdeki kuralları mantığı işlemek için işler.</span><span class="sxs-lookup"><span data-stu-id="9def7-115">The remote monitoring solution includes three [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) jobs to handle device information, telemetry, and rules logic in the solution.</span></span>

<span data-ttu-id="9def7-116">Üç akış analizi işleri ve bunların söz dizimi ayrıntılı olarak açıklanmıştır [Uzaktan izleme çözümünde gezinme önceden yapılandırılmış](iot-suite-remote-monitoring-sample-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="9def7-116">The three stream analytics jobs and their syntax are described in depth in the [Remote monitoring preconfigured solution walkthrough](iot-suite-remote-monitoring-sample-walkthrough.md).</span></span> 

<span data-ttu-id="9def7-117">Bu işleri doğrudan mantığı alter düzenleyin veya senaryonuz için belirli mantığı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9def7-117">You can edit these jobs directly to alter the logic, or add logic specific to your scenario.</span></span> <span data-ttu-id="9def7-118">Akış analizi işleri şu şekilde bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9def7-118">You can find the Stream Analytics jobs as follows:</span></span>

1. <span data-ttu-id="9def7-119">Git [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9def7-119">Go to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9def7-120">IOT çözümünüzü aynı ada sahip kaynak grubuna gidin.</span><span class="sxs-lookup"><span data-stu-id="9def7-120">Navigate to the resource group with the same name as your IoT solution.</span></span> 
3. <span data-ttu-id="9def7-121">Değiştirmek istediğiniz Azure akış analizi işi seçin.</span><span class="sxs-lookup"><span data-stu-id="9def7-121">Select the Azure Stream Analytics job you'd like to modify.</span></span> 
4. <span data-ttu-id="9def7-122">Seçerek işini durdurma **durdurmak** , komutları kümesi.</span><span class="sxs-lookup"><span data-stu-id="9def7-122">Stop the job by selecting **Stop** in the set of commands.</span></span> 
5. <span data-ttu-id="9def7-123">Giriş, sorgu ve çıkış düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="9def7-123">Edit the inputs, query, and outputs.</span></span>
   
    <span data-ttu-id="9def7-124">Basit bir değişiklikle için sorgu değiştirmektir **kuralları** kullanmak için iş bir **"<"** yerine bir **">"**.</span><span class="sxs-lookup"><span data-stu-id="9def7-124">A simple modification is to change the query for the **Rules** job to use a **"<"** instead of a **">"**.</span></span> <span data-ttu-id="9def7-125">Çözüm portalı görüntülenmeye **">"** kullandığınızda, kural düzenleme, ancak temel alınan iş değişikliği nedeniyle davranışı nasıl çevrilmiş dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="9def7-125">The solution portal still shows **">"** when you edit a rule, but notice how the behavior is flipped due to the change in the underlying job.</span></span>
6. <span data-ttu-id="9def7-126">İşi Başlat</span><span class="sxs-lookup"><span data-stu-id="9def7-126">Start the job</span></span>

> [!NOTE]
> <span data-ttu-id="9def7-127">İşlerini değiştirilmesine Pano başarısız olmasına neden olabilir şekilde Uzaktan izleme Panosu belirli verilere, bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="9def7-127">The remote monitoring dashboard depends on specific data, so altering the jobs can cause the dashboard to fail.</span></span>

## <a name="add-your-own-rules"></a><span data-ttu-id="9def7-128">Kendi kurallarınızı ekleme</span><span class="sxs-lookup"><span data-stu-id="9def7-128">Add your own rules</span></span>

<span data-ttu-id="9def7-129">Önceden yapılandırılmış Azure akış analizi işi değiştirmenin yanı sıra, yeni işleri ekleyin veya yeni sorgular için var olan işler eklemek için Azure portalını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9def7-129">In addition to changing the preconfigured Azure Stream Analytics jobs, you can use the Azure portal to add new jobs or add new queries to existing jobs.</span></span>

## <a name="customize-devices"></a><span data-ttu-id="9def7-130">Aygıtları özelleştirme</span><span class="sxs-lookup"><span data-stu-id="9def7-130">Customize devices</span></span>

<span data-ttu-id="9def7-131">En yaygın uzantısı etkinlikler senaryonuz için belirli cihazlar ile çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9def7-131">One of the most common extension activities is working with devices specific to your scenario.</span></span> <span data-ttu-id="9def7-132">Cihazları ile çalışmak için birkaç yöntem vardır.</span><span class="sxs-lookup"><span data-stu-id="9def7-132">There are several methods for working with devices.</span></span> <span data-ttu-id="9def7-133">Senaryonuz eşleşecek şekilde bir sanal cihaz değiştirilmesine veya kullanarak bu yöntemleri dahil [IOT cihaz SDK'sı] [ IoT Device SDK] çözüme fiziksel Cihazınızı bağlamak için.</span><span class="sxs-lookup"><span data-stu-id="9def7-133">These methods include altering a simulated device to match your scenario, or using the [IoT Device SDK][IoT Device SDK] to connect your physical device to the solution.</span></span>

<span data-ttu-id="9def7-134">Cihaz ekleme için adım adım yönergeler için bkz: [IOT paketi bağlanan cihazları](iot-suite-connecting-devices.md) makale ve [C SDK'sı örneği izleme uzaktan](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span><span class="sxs-lookup"><span data-stu-id="9def7-134">For a step-by-step guide to adding devices, see the [Iot Suite Connecting Devices](iot-suite-connecting-devices.md) article and the [remote monitoring C SDK Sample](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span></span> <span data-ttu-id="9def7-135">Bu örnek, Uzaktan izleme önceden yapılandırılmış çözümü ile çalışmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9def7-135">This sample is designed to work with the remote monitoring preconfigured solution.</span></span>

### <a name="create-your-own-simulated-device"></a><span data-ttu-id="9def7-136">Sanal cihazınız oluşturma</span><span class="sxs-lookup"><span data-stu-id="9def7-136">Create your own simulated device</span></span>

<span data-ttu-id="9def7-137">Dahil [Uzaktan izleme çözümünün kaynak kodu](https://github.com/Azure/azure-iot-remote-monitoring), .NET simulator değil.</span><span class="sxs-lookup"><span data-stu-id="9def7-137">Included in the [remote monitoring solution source code](https://github.com/Azure/azure-iot-remote-monitoring), is a .NET simulator.</span></span> <span data-ttu-id="9def7-138">Bu simulator çözümün bir parçası sağlanan olur ve farklı meta veriler, telemetri, Gönder ve farklı komutları ve yöntemleri yanıt şekilde değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9def7-138">This simulator is the one provisioned as part of the solution and you can alter it to send different metadata, telemetry, and respond to different commands and methods.</span></span>

<span data-ttu-id="9def7-139">Önceden yapılandırılmış Uzaktan izleme çözümü önceden yapılandırılmış benzeticisinde sıcaklık ve nem telemetri yayan için bir cihazın benzetimini yapar.</span><span class="sxs-lookup"><span data-stu-id="9def7-139">The preconfigured simulator in the remote monitoring preconfigured solution simulates a cooler device that emits temperature and humidity telemetry.</span></span> <span data-ttu-id="9def7-140">Benzetici değiştirebileceğiniz [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) proje GitHub deposuna çatallanmış zaman.</span><span class="sxs-lookup"><span data-stu-id="9def7-140">You can modify the simulator in the [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) project when you've forked the GitHub repository.</span></span>

### <a name="available-locations-for-simulated-devices"></a><span data-ttu-id="9def7-141">Sanal cihazlar için kullanılabilir konumları</span><span class="sxs-lookup"><span data-stu-id="9def7-141">Available locations for simulated devices</span></span>

<span data-ttu-id="9def7-142">Varsayılan konumlar kümesidir Seattle/Redmond, Washington, Amerika Birleşik Devletleri.</span><span class="sxs-lookup"><span data-stu-id="9def7-142">The default set of locations is in Seattle/Redmond, Washington, United States of America.</span></span> <span data-ttu-id="9def7-143">Bu konumları değiştirebilirsiniz [SampleDeviceFactory.cs][lnk-sample-device-factory].</span><span class="sxs-lookup"><span data-stu-id="9def7-143">You can change these locations in [SampleDeviceFactory.cs][lnk-sample-device-factory].</span></span>

### <a name="add-a-desired-property-update-handler-to-the-simulator"></a><span data-ttu-id="9def7-144">İstenen özellik güncelleştirme işleyicisi simulator ekleyin</span><span class="sxs-lookup"><span data-stu-id="9def7-144">Add a desired property update handler to the simulator</span></span>

<span data-ttu-id="9def7-145">Çözüm Portalı'nda bir aygıt için istenen bir özellik için bir değer ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9def7-145">You can set a value for a desired property for a device in the solution portal.</span></span> <span data-ttu-id="9def7-146">Bu özelliği işlemek için cihaz sorumluluğunda değiştirme isteği cihaz istenen özellik değeri aldığında olur.</span><span class="sxs-lookup"><span data-stu-id="9def7-146">It is the responsibility of the device to handle the property change request when the device retrieves the desired property value.</span></span> <span data-ttu-id="9def7-147">Özellik değeri değişikliği istenen özelliği aracılığıyla desteği eklemek için bir işleyici simulator eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9def7-147">To add support for a property value change through a desired property, you need to add a handler to the simulator.</span></span>

<span data-ttu-id="9def7-148">Simulator işleyicilerini içeren **SetPointTemp** ve **TelemetryInterval** ayarlayarak güncelleştirebilirsiniz özellikleri istenen çözüm portalı değerleri.</span><span class="sxs-lookup"><span data-stu-id="9def7-148">The simulator contains handlers for the **SetPointTemp** and **TelemetryInterval** properties that you can update by setting desired values in the solution portal.</span></span>

<span data-ttu-id="9def7-149">Aşağıdaki örnek, işleyicisi gösterir **SetPointTemp** özelliğinde istenen **CoolerDevice** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="9def7-149">The following example shows the handler for the **SetPointTemp** desired property in the **CoolerDevice** class:</span></span>

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

<span data-ttu-id="9def7-150">Bu yöntem telemetri noktası sıcaklık güncelleştirir ve değişikliği geri IOT Hub'ına bildirilen özelliği ayarlanarak bildirir.</span><span class="sxs-lookup"><span data-stu-id="9def7-150">This method updates the telemetry point temperature and then reports the change back to IoT Hub by setting a reported property.</span></span>

<span data-ttu-id="9def7-151">Önceki örnekte düzeni izleyerek kendi özelliklerinizi için kendi işleyicilerinizi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9def7-151">You can add your own handlers for your own properties by following the pattern in the preceding example.</span></span>

<span data-ttu-id="9def7-152">Ayrıca istenen özelliği işleyicisine aşağıdaki örnekte gösterildiği gibi bağlamanız gerekir **CoolerDevice** Oluşturucusu:</span><span class="sxs-lookup"><span data-stu-id="9def7-152">You must also bind the desired property to the handler as shown in the following example from the **CoolerDevice** constructor:</span></span>

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

<span data-ttu-id="9def7-153">Unutmayın **SetPointTempPropertyName** olan "Config.SetPointTemp" tanımlanan bir sabit.</span><span class="sxs-lookup"><span data-stu-id="9def7-153">Note that **SetPointTempPropertyName** is a constant defined as "Config.SetPointTemp".</span></span>

### <a name="add-support-for-a-new-method-to-the-simulator"></a><span data-ttu-id="9def7-154">Yeni bir yöntem için destek simulator Ekle</span><span class="sxs-lookup"><span data-stu-id="9def7-154">Add support for a new method to the simulator</span></span>

<span data-ttu-id="9def7-155">Yeni bir desteği eklemek için simulator özelleştirebilirsiniz [yöntemi (doğrudan yöntemi)][lnk-direct-methods].</span><span class="sxs-lookup"><span data-stu-id="9def7-155">You can customize the simulator to add support for a new [method (direct method)][lnk-direct-methods].</span></span> <span data-ttu-id="9def7-156">Gereken iki temel adımlar verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="9def7-156">There are two key steps required:</span></span>

- <span data-ttu-id="9def7-157">Benzetici, IOT hub yönteminin ayrıntılarla önceden yapılandırılmış çözümde bildirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9def7-157">The simulator must notify the IoT hub in the preconfigured solution with details of the method.</span></span>
- <span data-ttu-id="9def7-158">Simulator çağırdığınızda, ondan yöntem çağrısının işlemek için kod içermelidir **cihaz ayrıntıları** Masası Çözüm Gezgini'nde ya da bir iş.</span><span class="sxs-lookup"><span data-stu-id="9def7-158">The simulator must include code to handle the method call when you invoke it from the **Device details** panel in the solution explorer or through a job.</span></span>

<span data-ttu-id="9def7-159">Çözüm kullanan önceden yapılandırılmış Uzaktan izleme *özellikleri bildirilen* IOT hub'ına desteklenen yöntemlerden ayrıntılarını göndermek için.</span><span class="sxs-lookup"><span data-stu-id="9def7-159">The remote monitoring preconfigured solution uses *reported properties* to send details of supported methods to IoT hub.</span></span> <span data-ttu-id="9def7-160">Çözüm arka ucu yöntem çağrılarına geçmişini yanı sıra her bir cihaz tarafından desteklenen tüm yöntemleri listesini tutar.</span><span class="sxs-lookup"><span data-stu-id="9def7-160">The solution back end maintains a list of all the methods supported by each device along with a history of method invocations.</span></span> <span data-ttu-id="9def7-161">Bu cihazlar hakkındaki bilgileri görüntülemek ve çözüm portalında yöntemleri çağırma.</span><span class="sxs-lookup"><span data-stu-id="9def7-161">You can view this information about devices and invoke methods in the solution portal.</span></span>

<span data-ttu-id="9def7-162">Bir aygıt bir yöntem destekler, cihaz yönteme ayrıntılarını eklemeniz gerekir IOT hub'ı bildirmek için **SupportedMethods** bildirilen özellikleri düğümünde:</span><span class="sxs-lookup"><span data-stu-id="9def7-162">To notify the IoT hub that a device supports a method, the device must add details of the method to the **SupportedMethods** node in the reported properties:</span></span>

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

<span data-ttu-id="9def7-163">Yöntem imzası aşağıdaki biçime sahiptir: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span><span class="sxs-lookup"><span data-stu-id="9def7-163">The method signature has the following format: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span></span> <span data-ttu-id="9def7-164">Örneğin, belirtmek için **InitiateFirmwareUpdate** yöntemi bekliyor adlı bir dize parametresi **FwPackageURI**, aşağıdaki yöntemi imzası kullanın:</span><span class="sxs-lookup"><span data-stu-id="9def7-164">For example, to specify the **InitiateFirmwareUpdate** method expects a string parameter named **FwPackageURI**, use the following method signature:</span></span>

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

<span data-ttu-id="9def7-165">Desteklenen parametre türleri listesi için bkz: **CommandTypes** altyapısı projesi sınıfta.</span><span class="sxs-lookup"><span data-stu-id="9def7-165">For a list of supported parameter types, see the **CommandTypes** class in the Infrastructure project.</span></span>

<span data-ttu-id="9def7-166">Bir yöntem silmek için yöntem imzası ayarlamak `null` bildirilen özellikleri.</span><span class="sxs-lookup"><span data-stu-id="9def7-166">To delete a method, set the method signature to `null` in the reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="9def7-167">Çözüm arka ucu, aldığında, yalnızca desteklenen yöntemleri hakkında bilgi güncelleştirmeleri bir *aygıt bilgileri* aygıttan ileti.</span><span class="sxs-lookup"><span data-stu-id="9def7-167">The solution back end only updates information about supported methods when it receives a *device information* message from the device.</span></span>

<span data-ttu-id="9def7-168">Aşağıdaki kod örnek alarak **SampleDeviceFactory** ortak proje sınıfında bir yöntem listesine eklemek nasıl gösterir **SupportedMethods** aygıt tarafından gönderilen bildirilen özellikleri:</span><span class="sxs-lookup"><span data-stu-id="9def7-168">The following code sample from the **SampleDeviceFactory** class in the Common project shows how to add a method to the list of **SupportedMethods** in the reported properties sent by the device:</span></span>

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' to specifiy the URI of the firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

<span data-ttu-id="9def7-169">Bu kod parçacığını ayrıntılarını ekler **InitiateFirmwareUpdate** çözüm portalı ve gerekli yöntem parametreleri ayrıntılarını görüntülemek için metin dahil yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9def7-169">This code snippet adds details of the **InitiateFirmwareUpdate** method including text to display in the solution portal and details of the required method parameters.</span></span>

<span data-ttu-id="9def7-170">Simulator bildirilen özellikleri, IOT hub'ına simulator başladığında desteklenen yöntemlerin listesi dahil olmak üzere gönderir.</span><span class="sxs-lookup"><span data-stu-id="9def7-170">The simulator sends reported properties, including the list of supported methods, to IoT Hub when the simulator starts.</span></span>

<span data-ttu-id="9def7-171">Simulator koduna desteklediği her bir yöntemi için bir işleyici ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9def7-171">Add a handler to the simulator code for each method it supports.</span></span> <span data-ttu-id="9def7-172">Varolan işleyiciler görebilirsiniz **CoolerDevice** Simulator.WebJob projesinde sınıfı.</span><span class="sxs-lookup"><span data-stu-id="9def7-172">You can see the existing handlers in the **CoolerDevice** class in the Simulator.WebJob project.</span></span> <span data-ttu-id="9def7-173">Aşağıdaki örnek, işleyicisi gösterir **InitiateFirmwareUpdate** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="9def7-173">The following example shows the handler for **InitiateFirmwareUpdate** method:</span></span>

```csharp
public async Task<MethodResponse> OnInitiateFirmwareUpdate(MethodRequest methodRequest, object userContext)
{
    if (_deviceManagementTask != null && !_deviceManagementTask.IsCompleted)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "Device is busy"
        }, 409));
    }

    try
    {
        var operation = new FirmwareUpdate(methodRequest);
        _deviceManagementTask = operation.Run(Transport).ContinueWith(async task =>
        {
            // after firmware completed, we reset telemetry
            var telemetry = _telemetryController as ITelemetryWithTemperatureMeanValue;
            if (telemetry != null)
            {
                telemetry.TemperatureMeanValue = 34.5;
            }

            await UpdateReportedTemperatureMeanValue();
        });

        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "FirmwareUpdate accepted",
            Uri = operation.Uri
        }));
    }
    catch (Exception ex)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = ex.Message
        }, 400));
    }
}
```

<span data-ttu-id="9def7-174">Yöntem işleyici adları ile başlamalı `On` ardından yöntemin adı.</span><span class="sxs-lookup"><span data-stu-id="9def7-174">Method handler names must start with `On` followed by the name of the method.</span></span> <span data-ttu-id="9def7-175">**MethodRequest** parametresi çözüm arka ucu ile yöntemi çağırma geçirilen herhangi bir parametre içeriyor.</span><span class="sxs-lookup"><span data-stu-id="9def7-175">The **methodRequest** parameter contains any parameters passed with the method invocation from the solution back end.</span></span> <span data-ttu-id="9def7-176">Dönüş değeri türü olmalıdır **görev&lt;MethodResponse&gt;**.</span><span class="sxs-lookup"><span data-stu-id="9def7-176">The return value must be of type **Task&lt;MethodResponse&gt;**.</span></span> <span data-ttu-id="9def7-177">**BuildMethodResponse** yardımcı program yöntemi, dönüş değeri oluşturmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="9def7-177">The **BuildMethodResponse** utility method helps you create the return value.</span></span>

<span data-ttu-id="9def7-178">Yöntem işleyicisinin içinden, olabilir:</span><span class="sxs-lookup"><span data-stu-id="9def7-178">Inside the method handler, you could:</span></span>

- <span data-ttu-id="9def7-179">Zaman uyumsuz bir görevi başlatın.</span><span class="sxs-lookup"><span data-stu-id="9def7-179">Start an asynchronous task.</span></span>
- <span data-ttu-id="9def7-180">İstenen özelliklerinden almak *cihaz çifti* IOT hub.</span><span class="sxs-lookup"><span data-stu-id="9def7-180">Retrieve desired properties from the *device twin* in IoT Hub.</span></span>
- <span data-ttu-id="9def7-181">Bir tek bildirilen özelliğini kullanarak güncelleştirme **SetReportedPropertyAsync** yönteminde **CoolerDevice** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="9def7-181">Update a single reported property using the **SetReportedPropertyAsync** method in the **CoolerDevice** class.</span></span>
- <span data-ttu-id="9def7-182">Birden çok bildirilen özellikleri oluşturarak güncelleştirmek bir **TwinCollection** örneği ve arama **Transport.UpdateReportedPropertiesAsync** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9def7-182">Update multiple reported properties by creating a **TwinCollection** instance and calling the **Transport.UpdateReportedPropertiesAsync** method.</span></span>

<span data-ttu-id="9def7-183">Bellenim güncelleştirme sabitlerini aşağıdaki adımları gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="9def7-183">The preceding firmware update example performs the following steps:</span></span>

- <span data-ttu-id="9def7-184">Cihazın üretici yazılımı güncelleştirme isteğini kabul edemiyor denetler.</span><span class="sxs-lookup"><span data-stu-id="9def7-184">Checks the device is able to accept the firmware update request.</span></span>
- <span data-ttu-id="9def7-185">Zaman uyumsuz olarak bellenim güncelleştirme işlemi başlatır ve işlem tamamlandığında, telemetri sıfırlar.</span><span class="sxs-lookup"><span data-stu-id="9def7-185">Asynchronously initiates the firmware update operation and resets the telemetry when the operation is complete.</span></span>
- <span data-ttu-id="9def7-186">Hemen istek aygıt tarafından kabul belirtmek için "FirmwareUpdate kabul" iletisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="9def7-186">Immediately returns the "FirmwareUpdate accepted" message to indicate the request was accepted by the device.</span></span>

### <a name="build-and-use-your-own-physical-device"></a><span data-ttu-id="9def7-187">Derleme ve (fiziksel) aygıtınızı kullanın</span><span class="sxs-lookup"><span data-stu-id="9def7-187">Build and use your own (physical) device</span></span>

<span data-ttu-id="9def7-188">[Azure IOT SDK'ları](https://github.com/Azure/azure-iot-sdks) kitaplıkları çok sayıda aygıt türleri (diller ve işletim sistemleri) bağlamak için IOT çözümleriyle sağlar.</span><span class="sxs-lookup"><span data-stu-id="9def7-188">The [Azure IoT SDKs](https://github.com/Azure/azure-iot-sdks) provide libraries for connecting numerous device types (languages and operating systems) into IoT solutions.</span></span>

## <a name="modify-dashboard-limits"></a><span data-ttu-id="9def7-189">Pano sınırları değiştirme</span><span class="sxs-lookup"><span data-stu-id="9def7-189">Modify dashboard limits</span></span>

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a><span data-ttu-id="9def7-190">Pano açılır listede görüntülenen aygıt sayısı</span><span class="sxs-lookup"><span data-stu-id="9def7-190">Number of devices displayed in dashboard dropdown</span></span>

<span data-ttu-id="9def7-191">200 varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="9def7-191">The default is 200.</span></span> <span data-ttu-id="9def7-192">Bu sayıyı değiştirin [DashboardController.cs][lnk-dashboard-controller].</span><span class="sxs-lookup"><span data-stu-id="9def7-192">You can change this number in [DashboardController.cs][lnk-dashboard-controller].</span></span>

### <a name="number-of-pins-to-display-in-bing-map-control"></a><span data-ttu-id="9def7-193">Sayısını Bing harita denetiminde görüntüleme</span><span class="sxs-lookup"><span data-stu-id="9def7-193">Number of pins to display in Bing Map control</span></span>

<span data-ttu-id="9def7-194">200 varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="9def7-194">The default is 200.</span></span> <span data-ttu-id="9def7-195">Bu sayıyı değiştirin [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span><span class="sxs-lookup"><span data-stu-id="9def7-195">You can change this number in [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span></span>

### <a name="time-period-of-telemetry-graph"></a><span data-ttu-id="9def7-196">Süre telemetri grafik</span><span class="sxs-lookup"><span data-stu-id="9def7-196">Time period of telemetry graph</span></span>

<span data-ttu-id="9def7-197">Varsayılan değer 10 dakikadır.</span><span class="sxs-lookup"><span data-stu-id="9def7-197">The default is 10 minutes.</span></span> <span data-ttu-id="9def7-198">Bu değeri değiştirebilirsiniz [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span><span class="sxs-lookup"><span data-stu-id="9def7-198">You can change this value in [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span></span>

## <a name="manually-set-up-application-roles"></a><span data-ttu-id="9def7-199">Uygulama rolleri el ile ayarlamanız</span><span class="sxs-lookup"><span data-stu-id="9def7-199">Manually set up application roles</span></span>

<span data-ttu-id="9def7-200">Aşağıdaki yordam nasıl ekleneceğini açıklar **yönetici** ve **ReadOnly** uygulama rolleri önceden yapılandırılmış bir çözüm için.</span><span class="sxs-lookup"><span data-stu-id="9def7-200">The following procedure describes how to add **Admin** and **ReadOnly** application roles to a preconfigured solution.</span></span> <span data-ttu-id="9def7-201">Azureiotsuite.com sitesinden zaten sağlanan önceden yapılandırılmış çözümler içerdiğini unutmayın **yönetici** ve **ReadOnly** rolleri.</span><span class="sxs-lookup"><span data-stu-id="9def7-201">Note that preconfigured solutions provisioned from the azureiotsuite.com site already include the **Admin** and **ReadOnly** roles.</span></span>

<span data-ttu-id="9def7-202">Üyeleri **ReadOnly** rolü Pano ve cihaz listesini görebilirsiniz ancak cihazları eklemek, cihaz özniteliklerine değiştirmek veya komutlarını göndermek için izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="9def7-202">Members of the **ReadOnly** role can see the dashboard and the device list, but are not allowed to add devices, change device attributes, or send commands.</span></span>  <span data-ttu-id="9def7-203">Üyeleri **yönetici** rol Çözümdeki tüm işlevlere tam erişimi vardır.</span><span class="sxs-lookup"><span data-stu-id="9def7-203">Members of the **Admin** role have full access to all the functionality in the solution.</span></span>

1. <span data-ttu-id="9def7-204">Git [Klasik Azure portalı][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="9def7-204">Go to the [Azure classic portal][lnk-classic-portal].</span></span>
2. <span data-ttu-id="9def7-205">**Active Directory**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="9def7-205">Select **Active Directory**.</span></span>
3. <span data-ttu-id="9def7-206">Çözümünüzü sağlarken kullandığınız AAD Kiracı adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9def7-206">Click the name of the AAD tenant you used when you provisioned your solution.</span></span>
4. <span data-ttu-id="9def7-207">**Uygulamalar**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9def7-207">Click **Applications**.</span></span>
5. <span data-ttu-id="9def7-208">Önceden yapılandırılmış çözümünüzün adıyla eşleşen uygulamanın adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9def7-208">Click the name of the application that matches your preconfigured solution name.</span></span> <span data-ttu-id="9def7-209">Uygulamanızı listede görmüyorsanız, seçin **Şirketimin sahip olduğu uygulamalar** içinde **Göster** onay işareti açılır ve'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="9def7-209">If you don't see your application in the list, select **Applications my company owns** in the **Show** dropdown and click the check mark.</span></span>
6. <span data-ttu-id="9def7-210">Sayfanın alt kısmındaki tıklatın **yönetmek bildirim** ve ardından **karşıdan bildirim**.</span><span class="sxs-lookup"><span data-stu-id="9def7-210">At the bottom of the page, click **Manage Manifest** and then **Download Manifest**.</span></span>
7. <span data-ttu-id="9def7-211">Bu yordam bir .json dosyası yerel makinenize indirir.</span><span class="sxs-lookup"><span data-stu-id="9def7-211">This procedure downloads a .json file to your local machine.</span></span> <span data-ttu-id="9def7-212">Tercih ettiğiniz bir metin düzenleyicisinde düzenlemek için bu dosyayı açın.</span><span class="sxs-lookup"><span data-stu-id="9def7-212">Open this file for editing in a text editor of your choice.</span></span>
8. <span data-ttu-id="9def7-213">.Json dosyası üçüncü satırında, görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9def7-213">On the third line of the .json file, you can see:</span></span>

   ```json
   "appRoles" : [],
   ```
   <span data-ttu-id="9def7-214">Bu satırı aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="9def7-214">Replace this line with the following code:</span></span>

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access to the application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access to device information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. <span data-ttu-id="9def7-215">(Mevcut dosyanın üzerine yazabilirsiniz) güncelleştirilmiş .json dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9def7-215">Save the updated .json file (you can overwrite the existing file).</span></span>
10. <span data-ttu-id="9def7-216">Klasik Azure portalı, sayfanın sonundaki seçin **yönetmek bildirim** sonra **karşıya bildirim** önceki adımda kaydettiğiniz .json dosyası karşıya yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="9def7-216">In the Azure classic portal, at the bottom of the page, select **Manage Manifest** then **Upload Manifest** to upload the .json file you saved in the previous step.</span></span>
11. <span data-ttu-id="9def7-217">Artık eklemiş olduğunuz **yönetici** ve **ReadOnly** uygulamanız için rolleri.</span><span class="sxs-lookup"><span data-stu-id="9def7-217">You have now added the **Admin** and **ReadOnly** roles to your application.</span></span>
12. <span data-ttu-id="9def7-218">Bu rollerden birinin dizininizdeki bir kullanıcı atamak için bkz: [azureiotsuite.com sitesindeki izinler][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="9def7-218">To assign one of these roles to a user in your directory, see [Permissions on the azureiotsuite.com site][lnk-permissions].</span></span>

## <a name="feedback"></a><span data-ttu-id="9def7-219">Geri Bildirim</span><span class="sxs-lookup"><span data-stu-id="9def7-219">Feedback</span></span>

<span data-ttu-id="9def7-220">Bir özelleştirme zorunda görmek bu belgedeki kapsanan istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="9def7-220">Do you have a customization you'd like to see covered in this document?</span></span> <span data-ttu-id="9def7-221">Özellik önerileri eklemek [kullanıcı sesi](https://feedback.azure.com/forums/321918-azure-iot), ya da bu makaleye yorum.</span><span class="sxs-lookup"><span data-stu-id="9def7-221">Add feature suggestions to [User Voice](https://feedback.azure.com/forums/321918-azure-iot), or comment on this article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9def7-222">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9def7-222">Next steps</span></span>

<span data-ttu-id="9def7-223">Önceden yapılandırılmış çözümleri özelleştirme seçenekleri hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="9def7-223">To learn more about the options for customizing the preconfigured solutions, see:</span></span>

* <span data-ttu-id="9def7-224">[Mantıksal uygulama, Azure IOT paketi uzaktan önceden yapılandırılmış izleme çözümüne bağlama][lnk-logicapp]</span><span class="sxs-lookup"><span data-stu-id="9def7-224">[Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapp]</span></span>
* <span data-ttu-id="9def7-225">[Önceden yapılandırılmış Uzaktan izleme çözümü ile dinamik telemetri kullanın][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="9def7-225">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="9def7-226">[Önceden yapılandırılmış Uzaktan izleme çözümü cihaz bilgileri meta veriler][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="9def7-226">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo]</span></span>
* <span data-ttu-id="9def7-227">[Bağlı Fabrika çözüm OPC UA sunucularınızdan veri biçimini Özelleştir][lnk-cf-customize]</span><span class="sxs-lookup"><span data-stu-id="9def7-227">[Customize how the connected factory solution displays data from your OPC UA servers][lnk-cf-customize]</span></span>

[lnk-logicapp]: iot-suite-logic-apps-tutorial.md
[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[IoT Device SDK]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-permissions]: iot-suite-permissions.md
[lnk-dashboard-controller]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/Controllers/DashboardController.cs#L27
[lnk-telemetry-api-controller-01]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L27
[lnk-telemetry-api-controller-02]: https://github.com/Azure/azure-iot-remote-monitoring/blob/e7003339f73e21d3930f71ceba1e74fb5c0d9ea0/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L25 
[lnk-sample-device-factory]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Common/Factory/SampleDeviceFactory.cs#L40
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-cf-customize]: iot-suite-connected-factory-customize.md