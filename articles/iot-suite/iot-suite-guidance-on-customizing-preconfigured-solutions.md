---
title: "aaaCustomizing önceden yapılandırılmış çözümleri | Microsoft Docs"
description: "Nasıl toocustomize hello Azure IOT paketi önceden yapılandırılmış çözümler hakkında rehberlik sağlar."
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
ms.openlocfilehash: 1a8573f5ac6ed944c44459df495446f15174d513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-a-preconfigured-solution"></a><span data-ttu-id="3509d-103">Önceden yapılandırılmış bir çözümü özelleştirme</span><span class="sxs-lookup"><span data-stu-id="3509d-103">Customize a preconfigured solution</span></span>

<span data-ttu-id="3509d-104">Azure IOT paketi Hello ile sağlanan hello önceden yapılandırılmış çözüm hello suite çalışma birlikte toodeliver bir uçtan uca çözüm içinde hello hizmetlerini gösterme.</span><span class="sxs-lookup"><span data-stu-id="3509d-104">hello preconfigured solutions provided with hello Azure IoT Suite demonstrate hello services within hello suite working together toodeliver an end-to-end solution.</span></span> <span data-ttu-id="3509d-105">Bu başlangıç noktasından genişletmek ve belirli senaryolar için hello çözümü özelleştirme çeşitli yerlerde vardır.</span><span class="sxs-lookup"><span data-stu-id="3509d-105">From this starting point, there are various places in which you can extend and customize hello solution for specific scenarios.</span></span> <span data-ttu-id="3509d-106">Aşağıdaki bölümlerde hello bu ortak özelleştirme noktaları açıklar.</span><span class="sxs-lookup"><span data-stu-id="3509d-106">hello following sections describe these common customization points.</span></span>

## <a name="find-hello-source-code"></a><span data-ttu-id="3509d-107">Merhaba kaynak kod Bul</span><span class="sxs-lookup"><span data-stu-id="3509d-107">Find hello source code</span></span>

<span data-ttu-id="3509d-108">depoları aşağıdaki hello Github'da Hello kaynak kodu hello önceden yapılandırılmış çözümleri için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="3509d-108">hello source code for hello preconfigured solutions is available on GitHub in hello following repositories:</span></span>

* <span data-ttu-id="3509d-109">Uzaktan izleme: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span><span class="sxs-lookup"><span data-stu-id="3509d-109">Remote Monitoring: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)</span></span>
* <span data-ttu-id="3509d-110">Tahmine dayalı Bakım: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span><span class="sxs-lookup"><span data-stu-id="3509d-110">Predictive Maintenance: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)</span></span>
* <span data-ttu-id="3509d-111">Bağlı Fabrika: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span><span class="sxs-lookup"><span data-stu-id="3509d-111">Connected factory: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)</span></span>

<span data-ttu-id="3509d-112">toodemonstrate hello desenleri ve uygulamalar tooimplement hello uçtan uca Azure IOT paketi kullanarak bir IOT çözüm işlevselliğini kullanılan hello önceden yapılandırılmış çözümleri için hello kaynak kodu sağlanır.</span><span class="sxs-lookup"><span data-stu-id="3509d-112">hello source code for hello preconfigured solutions is provided toodemonstrate hello patterns and practices used tooimplement hello end-to-end functionality of an IoT solution using Azure IoT Suite.</span></span> <span data-ttu-id="3509d-113">Hakkında daha fazla bilgi bulabilirsiniz toobuild ve hello GitHub depolarının hello çözümlerinde dağıtın.</span><span class="sxs-lookup"><span data-stu-id="3509d-113">You can find more information about how toobuild and deploy hello solutions in hello GitHub repositories.</span></span>

## <a name="change-hello-preconfigured-rules"></a><span data-ttu-id="3509d-114">Önceden yapılandırılmış hello kuralları Değiştir</span><span class="sxs-lookup"><span data-stu-id="3509d-114">Change hello preconfigured rules</span></span>

<span data-ttu-id="3509d-115">Merhaba Uzaktan izleme çözümü üç içeren [Azure akış analizi](https://azure.microsoft.com/services/stream-analytics/) toohandle cihaz bilgilerini, telemetri ve hello çözümde kuralları mantığı işler.</span><span class="sxs-lookup"><span data-stu-id="3509d-115">hello remote monitoring solution includes three [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) jobs toohandle device information, telemetry, and rules logic in hello solution.</span></span>

<span data-ttu-id="3509d-116">Merhaba üç analytics iş akışı ve bunların söz dizimi hello derinlemesine açıklanmıştır [Uzaktan izleme çözümünde gezinme önceden yapılandırılmış](iot-suite-remote-monitoring-sample-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="3509d-116">hello three stream analytics jobs and their syntax are described in depth in hello [Remote monitoring preconfigured solution walkthrough](iot-suite-remote-monitoring-sample-walkthrough.md).</span></span> 

<span data-ttu-id="3509d-117">Tooalter mantığı hello veya mantığı belirli tooyour senaryo Ekle doğrudan bu işleri düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3509d-117">You can edit these jobs directly tooalter hello logic, or add logic specific tooyour scenario.</span></span> <span data-ttu-id="3509d-118">Akış analizi işleri gibi hello bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3509d-118">You can find hello Stream Analytics jobs as follows:</span></span>

1. <span data-ttu-id="3509d-119">Çok Git[Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3509d-119">Go too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3509d-120">Toohello kaynak grubuyla aynı IOT çözümü olarak ad hello gidin.</span><span class="sxs-lookup"><span data-stu-id="3509d-120">Navigate toohello resource group with hello same name as your IoT solution.</span></span> 
3. <span data-ttu-id="3509d-121">Toomodify istediğiniz hello Azure akış analizi işi seçin.</span><span class="sxs-lookup"><span data-stu-id="3509d-121">Select hello Azure Stream Analytics job you'd like toomodify.</span></span> 
4. <span data-ttu-id="3509d-122">Seçerek durdurma hello işi **durdurmak** , komutları hello kümesi.</span><span class="sxs-lookup"><span data-stu-id="3509d-122">Stop hello job by selecting **Stop** in hello set of commands.</span></span> 
5. <span data-ttu-id="3509d-123">Merhaba giriş, sorgu ve çıkışlarla düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="3509d-123">Edit hello inputs, query, and outputs.</span></span>
   
    <span data-ttu-id="3509d-124">Basit bir değişiklikle toochange hello hello için sorgudur **kuralları** iş toouse bir **"<"** yerine bir **">"**.</span><span class="sxs-lookup"><span data-stu-id="3509d-124">A simple modification is toochange hello query for hello **Rules** job toouse a **"<"** instead of a **">"**.</span></span> <span data-ttu-id="3509d-125">Merhaba çözüm portalı görüntülenmeye **">"** kullandığınızda, kural düzenleme, ancak iş temel hello toohello değişikliği nedeniyle hello davranışı nasıl çevrilmiş dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="3509d-125">hello solution portal still shows **">"** when you edit a rule, but notice how hello behavior is flipped due toohello change in hello underlying job.</span></span>
6. <span data-ttu-id="3509d-126">Merhaba işi Başlat</span><span class="sxs-lookup"><span data-stu-id="3509d-126">Start hello job</span></span>

> [!NOTE]
> <span data-ttu-id="3509d-127">Merhaba işleri değiştirme hello Pano toofail neden şekilde hello Uzaktan izleme Panosu belirli verilere, bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="3509d-127">hello remote monitoring dashboard depends on specific data, so altering hello jobs can cause hello dashboard toofail.</span></span>

## <a name="add-your-own-rules"></a><span data-ttu-id="3509d-128">Kendi kurallarınızı ekleme</span><span class="sxs-lookup"><span data-stu-id="3509d-128">Add your own rules</span></span>

<span data-ttu-id="3509d-129">Ayrıca Azure akış analizi işi toochanging hello önceden yapılandırılmış, hello Azure portal tooadd yeni işleri kullanın veya yeni sorgular tooexisting işleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3509d-129">In addition toochanging hello preconfigured Azure Stream Analytics jobs, you can use hello Azure portal tooadd new jobs or add new queries tooexisting jobs.</span></span>

## <a name="customize-devices"></a><span data-ttu-id="3509d-130">Aygıtları özelleştirme</span><span class="sxs-lookup"><span data-stu-id="3509d-130">Customize devices</span></span>

<span data-ttu-id="3509d-131">Merhaba en yaygın uzantısı etkinliklerden birini aygıtları belirli tooyour senaryoyla çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3509d-131">One of hello most common extension activities is working with devices specific tooyour scenario.</span></span> <span data-ttu-id="3509d-132">Cihazları ile çalışmak için birkaç yöntem vardır.</span><span class="sxs-lookup"><span data-stu-id="3509d-132">There are several methods for working with devices.</span></span> <span data-ttu-id="3509d-133">Bir sanal cihaz toomatch senaryonuz değiştirilmesine veya hello kullanarak bu yöntemleri dahil [IOT cihaz SDK'sı] [ IoT Device SDK] tooconnect fiziksel cihaz toohello çözümünüzü.</span><span class="sxs-lookup"><span data-stu-id="3509d-133">These methods include altering a simulated device toomatch your scenario, or using hello [IoT Device SDK][IoT Device SDK] tooconnect your physical device toohello solution.</span></span>

<span data-ttu-id="3509d-134">Merhaba adım adım kılavuzu tooadding cihazlar için bkz [IOT paketi bağlanan cihazları](iot-suite-connecting-devices.md) makale ve hello [C SDK'sı örneği izleme uzaktan](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span><span class="sxs-lookup"><span data-stu-id="3509d-134">For a step-by-step guide tooadding devices, see hello [Iot Suite Connecting Devices](iot-suite-connecting-devices.md) article and hello [remote monitoring C SDK Sample](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring).</span></span> <span data-ttu-id="3509d-135">Merhaba Uzaktan izleme çözümü ile tasarlanmış toowork örnektir.</span><span class="sxs-lookup"><span data-stu-id="3509d-135">This sample is designed toowork with hello remote monitoring preconfigured solution.</span></span>

### <a name="create-your-own-simulated-device"></a><span data-ttu-id="3509d-136">Sanal cihazınız oluşturma</span><span class="sxs-lookup"><span data-stu-id="3509d-136">Create your own simulated device</span></span>

<span data-ttu-id="3509d-137">Hello dahil [Uzaktan izleme çözümünün kaynak kodu](https://github.com/Azure/azure-iot-remote-monitoring), .NET simulator değil.</span><span class="sxs-lookup"><span data-stu-id="3509d-137">Included in hello [remote monitoring solution source code](https://github.com/Azure/azure-iot-remote-monitoring), is a .NET simulator.</span></span> <span data-ttu-id="3509d-138">Bu simulator hello bir hello çözüm ve parçası toosend farklı meta veriler, telemetri, alter ve toodifferent komutları ve yöntemleri yanıt olarak sağlanan ' dir.</span><span class="sxs-lookup"><span data-stu-id="3509d-138">This simulator is hello one provisioned as part of hello solution and you can alter it toosend different metadata, telemetry, and respond toodifferent commands and methods.</span></span>

<span data-ttu-id="3509d-139">Merhaba önceden yapılandırılmış Uzaktan izleme çözümü hello benzeticisinde sıcaklık ve nem telemetri yayan için bir cihazın benzetimini yapar.</span><span class="sxs-lookup"><span data-stu-id="3509d-139">hello preconfigured simulator in hello remote monitoring preconfigured solution simulates a cooler device that emits temperature and humidity telemetry.</span></span> <span data-ttu-id="3509d-140">Merhaba hello benzeticisinde değiştirebileceğiniz [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) proje hello GitHub deposunu çatallanmış zaman.</span><span class="sxs-lookup"><span data-stu-id="3509d-140">You can modify hello simulator in hello [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) project when you've forked hello GitHub repository.</span></span>

### <a name="available-locations-for-simulated-devices"></a><span data-ttu-id="3509d-141">Sanal cihazlar için kullanılabilir konumları</span><span class="sxs-lookup"><span data-stu-id="3509d-141">Available locations for simulated devices</span></span>

<span data-ttu-id="3509d-142">Merhaba varsayılan konumları kümesidir Seattle/Redmond, Washington, Amerika Birleşik Devletleri.</span><span class="sxs-lookup"><span data-stu-id="3509d-142">hello default set of locations is in Seattle/Redmond, Washington, United States of America.</span></span> <span data-ttu-id="3509d-143">Bu konumları değiştirebilirsiniz [SampleDeviceFactory.cs][lnk-sample-device-factory].</span><span class="sxs-lookup"><span data-stu-id="3509d-143">You can change these locations in [SampleDeviceFactory.cs][lnk-sample-device-factory].</span></span>

### <a name="add-a-desired-property-update-handler-toohello-simulator"></a><span data-ttu-id="3509d-144">İstenen özellik güncelleştirme işleyicisi toohello simulator ekleme</span><span class="sxs-lookup"><span data-stu-id="3509d-144">Add a desired property update handler toohello simulator</span></span>

<span data-ttu-id="3509d-145">Merhaba çözüm portalında bir aygıt için istenen bir özellik için bir değer ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3509d-145">You can set a value for a desired property for a device in hello solution portal.</span></span> <span data-ttu-id="3509d-146">Merhaba aygıt istenen hello özellik değeri aldığında bu hello hello aygıt toohandle hello özellik değişikliği isteğini sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="3509d-146">It is hello responsibility of hello device toohandle hello property change request when hello device retrieves hello desired property value.</span></span> <span data-ttu-id="3509d-147">bir özellik değeri değişikliği tooadd desteği istenen bir özelliği üzerinden tooadd işleyici toohello simulator gerekir.</span><span class="sxs-lookup"><span data-stu-id="3509d-147">tooadd support for a property value change through a desired property, you need tooadd a handler toohello simulator.</span></span>

<span data-ttu-id="3509d-148">Merhaba simulator içeren hello için işleyiciler **SetPointTemp** ve **TelemetryInterval** ayarlayarak güncelleştirebilirsiniz özellikleri istenen hello çözüm portalı değerleri.</span><span class="sxs-lookup"><span data-stu-id="3509d-148">hello simulator contains handlers for hello **SetPointTemp** and **TelemetryInterval** properties that you can update by setting desired values in hello solution portal.</span></span>

<span data-ttu-id="3509d-149">Merhaba aşağıdaki örnekte gösterilir hello hello işleyicisi **SetPointTemp** hello özelliğinde istenen **CoolerDevice** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="3509d-149">hello following example shows hello handler for hello **SetPointTemp** desired property in hello **CoolerDevice** class:</span></span>

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

<span data-ttu-id="3509d-150">Bu yöntem sıcaklık ve raporları hello geri tooIoT Hub bildirilen özelliği ayarlanarak değiştirmek hello telemetri noktası güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="3509d-150">This method updates hello telemetry point temperature and then reports hello change back tooIoT Hub by setting a reported property.</span></span>

<span data-ttu-id="3509d-151">Örnek önceki hello aşağıdaki hello desende tarafından kendi özelliklerinizi için kendi işleyicilerinizi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3509d-151">You can add your own handlers for your own properties by following hello pattern in hello preceding example.</span></span>

<span data-ttu-id="3509d-152">Ayrıca hello istenen özellik toohello işleyicisi hello hello örnekten aşağıdaki gösterildiği gibi bağlamanız gerekir **CoolerDevice** Oluşturucusu:</span><span class="sxs-lookup"><span data-stu-id="3509d-152">You must also bind hello desired property toohello handler as shown in hello following example from hello **CoolerDevice** constructor:</span></span>

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

<span data-ttu-id="3509d-153">Unutmayın **SetPointTempPropertyName** olan "Config.SetPointTemp" tanımlanan bir sabit.</span><span class="sxs-lookup"><span data-stu-id="3509d-153">Note that **SetPointTempPropertyName** is a constant defined as "Config.SetPointTemp".</span></span>

### <a name="add-support-for-a-new-method-toohello-simulator"></a><span data-ttu-id="3509d-154">Yeni bir yöntem toohello simulator desteği ekleme</span><span class="sxs-lookup"><span data-stu-id="3509d-154">Add support for a new method toohello simulator</span></span>

<span data-ttu-id="3509d-155">Merhaba simulator tooadd desteği için yeni bir özelleştirebilirsiniz [yöntemi (doğrudan yöntemi)][lnk-direct-methods].</span><span class="sxs-lookup"><span data-stu-id="3509d-155">You can customize hello simulator tooadd support for a new [method (direct method)][lnk-direct-methods].</span></span> <span data-ttu-id="3509d-156">Gereken iki temel adımlar verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="3509d-156">There are two key steps required:</span></span>

- <span data-ttu-id="3509d-157">Merhaba simulator hello IOT hub'hello yönteminin ayrıntılarla hello önceden yapılandırılmış çözümde bildirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3509d-157">hello simulator must notify hello IoT hub in hello preconfigured solution with details of hello method.</span></span>
- <span data-ttu-id="3509d-158">Merhaba simulator, kod toohandle hello yöntem çağrısı içermelidir, hello çağırdığınızda **cihaz ayrıntıları** Masası hello Çözüm Gezgini'nde ya da bir iş.</span><span class="sxs-lookup"><span data-stu-id="3509d-158">hello simulator must include code toohandle hello method call when you invoke it from hello **Device details** panel in hello solution explorer or through a job.</span></span>

<span data-ttu-id="3509d-159">Merhaba çözümü kullanan önceden yapılandırılmış Uzaktan izleme *özellikleri bildirilen* desteklenen yöntemleri tooIoT hub toosend ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="3509d-159">hello remote monitoring preconfigured solution uses *reported properties* toosend details of supported methods tooIoT hub.</span></span> <span data-ttu-id="3509d-160">Merhaba çözüm arka ucu yöntem çağrılarına geçmişini yanı sıra her bir cihaz tarafından desteklenen tüm hello yöntemlerinin listesini tutar.</span><span class="sxs-lookup"><span data-stu-id="3509d-160">hello solution back end maintains a list of all hello methods supported by each device along with a history of method invocations.</span></span> <span data-ttu-id="3509d-161">Bu cihazlar hakkındaki bilgileri görüntülemek ve hello çözüm portalı yöntemleri çağırır.</span><span class="sxs-lookup"><span data-stu-id="3509d-161">You can view this information about devices and invoke methods in hello solution portal.</span></span>

<span data-ttu-id="3509d-162">toonotify hello IOT hub, bir aygıt bir yöntem desteklediğini hello aygıt hello yöntemi toohello ayrıntılarını eklemelisiniz **SupportedMethods** hello düğümünde bildirilen özellikleri:</span><span class="sxs-lookup"><span data-stu-id="3509d-162">toonotify hello IoT hub that a device supports a method, hello device must add details of hello method toohello **SupportedMethods** node in hello reported properties:</span></span>

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

<span data-ttu-id="3509d-163">Merhaba yöntemi imzası olan biçimini izleyen hello: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span><span class="sxs-lookup"><span data-stu-id="3509d-163">hello method signature has hello following format: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`.</span></span> <span data-ttu-id="3509d-164">Örneğin, toospecify hello **InitiateFirmwareUpdate** yöntemi bekliyor adlı bir dize parametresi **FwPackageURI**, yöntem imzası aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="3509d-164">For example, toospecify hello **InitiateFirmwareUpdate** method expects a string parameter named **FwPackageURI**, use hello following method signature:</span></span>

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

<span data-ttu-id="3509d-165">Merhaba desteklenen parametre türleri listesi için bkz: **CommandTypes** hello altyapısı projesi sınıfta.</span><span class="sxs-lookup"><span data-stu-id="3509d-165">For a list of supported parameter types, see hello **CommandTypes** class in hello Infrastructure project.</span></span>

<span data-ttu-id="3509d-166">toodelete bir yöntem hello yöntemi imza çok ayarlama`null` özellikleri hello bildirdi.</span><span class="sxs-lookup"><span data-stu-id="3509d-166">toodelete a method, set hello method signature too`null` in hello reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="3509d-167">aldığında hello çözüm arka ucu yalnızca desteklenen yöntemleri hakkında bilgi güncelleştirmeleri bir *aygıt bilgileri* hello aygıttan ileti.</span><span class="sxs-lookup"><span data-stu-id="3509d-167">hello solution back end only updates information about supported methods when it receives a *device information* message from hello device.</span></span>

<span data-ttu-id="3509d-168">Merhaba hello kod örnekten aşağıdaki **SampleDeviceFactory** hello ortak sınıfında proje gösterir nasıl tooadd yöntemi toohello listesini, **SupportedMethods** hello hello tarafından gönderilen özellikleri bildirdi aygıt:</span><span class="sxs-lookup"><span data-stu-id="3509d-168">hello following code sample from hello **SampleDeviceFactory** class in hello Common project shows how tooadd a method toohello list of **SupportedMethods** in hello reported properties sent by hello device:</span></span>

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' toospecifiy hello URI of hello firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

<span data-ttu-id="3509d-169">Bu kod parçacığını hello ayrıntılarını ekler **InitiateFirmwareUpdate** metin toodisplay hello çözüm portalı ve hello ayrıntılarını dahil yöntemi gereken yöntem parametreleri.</span><span class="sxs-lookup"><span data-stu-id="3509d-169">This code snippet adds details of hello **InitiateFirmwareUpdate** method including text toodisplay in hello solution portal and details of hello required method parameters.</span></span>

<span data-ttu-id="3509d-170">Merhaba simulator hello desteklenen yöntemlerin listesi tooIoT hello simulator başladığında Hub içeren bildirilen özelliklerini gönderir.</span><span class="sxs-lookup"><span data-stu-id="3509d-170">hello simulator sends reported properties, including hello list of supported methods, tooIoT Hub when hello simulator starts.</span></span>

<span data-ttu-id="3509d-171">Onu destekleyen her bir yöntemi için bir işleyici toohello simulator kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3509d-171">Add a handler toohello simulator code for each method it supports.</span></span> <span data-ttu-id="3509d-172">Merhaba varolan işleyicileri hello görebilirsiniz **CoolerDevice** hello Simulator.WebJob projesinde sınıfı.</span><span class="sxs-lookup"><span data-stu-id="3509d-172">You can see hello existing handlers in hello **CoolerDevice** class in hello Simulator.WebJob project.</span></span> <span data-ttu-id="3509d-173">Merhaba aşağıdaki örnekte gösterilir hello işleyicisi **InitiateFirmwareUpdate** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="3509d-173">hello following example shows hello handler for **InitiateFirmwareUpdate** method:</span></span>

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

<span data-ttu-id="3509d-174">Yöntem işleyici adları ile başlamalı `On` ardından hello yöntemi hello adı.</span><span class="sxs-lookup"><span data-stu-id="3509d-174">Method handler names must start with `On` followed by hello name of hello method.</span></span> <span data-ttu-id="3509d-175">Merhaba **methodRequest** parametresi ile Merhaba yöntemi çağırma hello çözüm arka uçtan geçirilen herhangi bir parametre içeriyor.</span><span class="sxs-lookup"><span data-stu-id="3509d-175">hello **methodRequest** parameter contains any parameters passed with hello method invocation from hello solution back end.</span></span> <span data-ttu-id="3509d-176">Merhaba dönüş değeri türü olmalıdır **görev&lt;MethodResponse&gt;**.</span><span class="sxs-lookup"><span data-stu-id="3509d-176">hello return value must be of type **Task&lt;MethodResponse&gt;**.</span></span> <span data-ttu-id="3509d-177">Merhaba **BuildMethodResponse** yardımcı program yöntemi hello dönüş değeri oluşturmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="3509d-177">hello **BuildMethodResponse** utility method helps you create hello return value.</span></span>

<span data-ttu-id="3509d-178">Merhaba yöntemi işleyicisinin içinden, olabilir:</span><span class="sxs-lookup"><span data-stu-id="3509d-178">Inside hello method handler, you could:</span></span>

- <span data-ttu-id="3509d-179">Zaman uyumsuz bir görevi başlatın.</span><span class="sxs-lookup"><span data-stu-id="3509d-179">Start an asynchronous task.</span></span>
- <span data-ttu-id="3509d-180">İstenen özelliklerini hello almak *cihaz çifti* IOT hub.</span><span class="sxs-lookup"><span data-stu-id="3509d-180">Retrieve desired properties from hello *device twin* in IoT Hub.</span></span>
- <span data-ttu-id="3509d-181">Merhaba kullanan tek bildirilen bir özellik güncelleştirme **SetReportedPropertyAsync** hello yönteminde **CoolerDevice** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="3509d-181">Update a single reported property using hello **SetReportedPropertyAsync** method in hello **CoolerDevice** class.</span></span>
- <span data-ttu-id="3509d-182">Birden çok bildirilen özellikleri oluşturarak güncelleştirmek bir **TwinCollection** örneği ve arama hello **Transport.UpdateReportedPropertiesAsync** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="3509d-182">Update multiple reported properties by creating a **TwinCollection** instance and calling hello **Transport.UpdateReportedPropertiesAsync** method.</span></span>

<span data-ttu-id="3509d-183">Merhaba bellenim güncelleştirme sabitlerini hello aşağıdaki adımları gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="3509d-183">hello preceding firmware update example performs hello following steps:</span></span>

- <span data-ttu-id="3509d-184">Denetimleri hello mümkün tooaccept hello bellenim güncelleştirme isteği aygıttır.</span><span class="sxs-lookup"><span data-stu-id="3509d-184">Checks hello device is able tooaccept hello firmware update request.</span></span>
- <span data-ttu-id="3509d-185">Zaman uyumsuz olarak hello bellenim güncelleştirme işlemi başlatır ve hello işlemi tamamlandığında hello telemetri sıfırlar.</span><span class="sxs-lookup"><span data-stu-id="3509d-185">Asynchronously initiates hello firmware update operation and resets hello telemetry when hello operation is complete.</span></span>
- <span data-ttu-id="3509d-186">"Kabul FirmwareUpdate" döndürür hello hemen ileti tooindicate hello isteği hello aygıt tarafından kabul edildi.</span><span class="sxs-lookup"><span data-stu-id="3509d-186">Immediately returns hello "FirmwareUpdate accepted" message tooindicate hello request was accepted by hello device.</span></span>

### <a name="build-and-use-your-own-physical-device"></a><span data-ttu-id="3509d-187">Derleme ve (fiziksel) aygıtınızı kullanın</span><span class="sxs-lookup"><span data-stu-id="3509d-187">Build and use your own (physical) device</span></span>

<span data-ttu-id="3509d-188">Merhaba [Azure IOT SDK'ları](https://github.com/Azure/azure-iot-sdks) kitaplıkları çok sayıda aygıt türleri (diller ve işletim sistemleri) bağlamak için IOT çözümleriyle sağlar.</span><span class="sxs-lookup"><span data-stu-id="3509d-188">hello [Azure IoT SDKs](https://github.com/Azure/azure-iot-sdks) provide libraries for connecting numerous device types (languages and operating systems) into IoT solutions.</span></span>

## <a name="modify-dashboard-limits"></a><span data-ttu-id="3509d-189">Pano sınırları değiştirme</span><span class="sxs-lookup"><span data-stu-id="3509d-189">Modify dashboard limits</span></span>

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a><span data-ttu-id="3509d-190">Pano açılır listede görüntülenen aygıt sayısı</span><span class="sxs-lookup"><span data-stu-id="3509d-190">Number of devices displayed in dashboard dropdown</span></span>

<span data-ttu-id="3509d-191">Merhaba, 200 varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="3509d-191">hello default is 200.</span></span> <span data-ttu-id="3509d-192">Bu sayıyı değiştirin [DashboardController.cs][lnk-dashboard-controller].</span><span class="sxs-lookup"><span data-stu-id="3509d-192">You can change this number in [DashboardController.cs][lnk-dashboard-controller].</span></span>

### <a name="number-of-pins-toodisplay-in-bing-map-control"></a><span data-ttu-id="3509d-193">Bing harita denetimindeki PIN'ler toodisplay sayısı</span><span class="sxs-lookup"><span data-stu-id="3509d-193">Number of pins toodisplay in Bing Map control</span></span>

<span data-ttu-id="3509d-194">Merhaba, 200 varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="3509d-194">hello default is 200.</span></span> <span data-ttu-id="3509d-195">Bu sayıyı değiştirin [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span><span class="sxs-lookup"><span data-stu-id="3509d-195">You can change this number in [TelemetryApiController.cs][lnk-telemetry-api-controller-01].</span></span>

### <a name="time-period-of-telemetry-graph"></a><span data-ttu-id="3509d-196">Süre telemetri grafik</span><span class="sxs-lookup"><span data-stu-id="3509d-196">Time period of telemetry graph</span></span>

<span data-ttu-id="3509d-197">Merhaba varsayılan değer 10 dakikadır.</span><span class="sxs-lookup"><span data-stu-id="3509d-197">hello default is 10 minutes.</span></span> <span data-ttu-id="3509d-198">Bu değeri değiştirebilirsiniz [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span><span class="sxs-lookup"><span data-stu-id="3509d-198">You can change this value in [TelmetryApiController.cs][lnk-telemetry-api-controller-02].</span></span>

## <a name="manually-set-up-application-roles"></a><span data-ttu-id="3509d-199">Uygulama rolleri el ile ayarlamanız</span><span class="sxs-lookup"><span data-stu-id="3509d-199">Manually set up application roles</span></span>

<span data-ttu-id="3509d-200">Merhaba aşağıdaki yordamda açıklanmıştır nasıl tooadd **yönetici** ve **ReadOnly** uygulama rolleri tooa önceden yapılandırılmış çözümü.</span><span class="sxs-lookup"><span data-stu-id="3509d-200">hello following procedure describes how tooadd **Admin** and **ReadOnly** application roles tooa preconfigured solution.</span></span> <span data-ttu-id="3509d-201">Merhaba azureiotsuite.com sitesinden zaten sağlanan önceden yapılandırılmış çözümler hello içerdiğini **yönetici** ve **ReadOnly** rolleri.</span><span class="sxs-lookup"><span data-stu-id="3509d-201">Note that preconfigured solutions provisioned from hello azureiotsuite.com site already include hello **Admin** and **ReadOnly** roles.</span></span>

<span data-ttu-id="3509d-202">Merhaba üyeleri **ReadOnly** rolü hello Pano ve hello cihaz listesini görebilirsiniz ancak tooadd cihazları, cihaz öznitelikleri Değiştir veya gönderme komutlar izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="3509d-202">Members of hello **ReadOnly** role can see hello dashboard and hello device list, but are not allowed tooadd devices, change device attributes, or send commands.</span></span>  <span data-ttu-id="3509d-203">Merhaba üyeleri **yönetici** rolüne sahip tam erişim tooall hello işlevselliği hello çözümde.</span><span class="sxs-lookup"><span data-stu-id="3509d-203">Members of hello **Admin** role have full access tooall hello functionality in hello solution.</span></span>

1. <span data-ttu-id="3509d-204">Toohello Git [Klasik Azure portalı][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="3509d-204">Go toohello [Azure classic portal][lnk-classic-portal].</span></span>
2. <span data-ttu-id="3509d-205">**Active Directory**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="3509d-205">Select **Active Directory**.</span></span>
3. <span data-ttu-id="3509d-206">Çözümünüzü sağlarken, kullanılan hello AAD kiracısını Hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3509d-206">Click hello name of hello AAD tenant you used when you provisioned your solution.</span></span>
4. <span data-ttu-id="3509d-207">**Uygulamalar**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3509d-207">Click **Applications**.</span></span>
5. <span data-ttu-id="3509d-208">Merhaba, önceden yapılandırılmış çözümünüzün adıyla eşleşen hello uygulamanın adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="3509d-208">Click hello name of hello application that matches your preconfigured solution name.</span></span> <span data-ttu-id="3509d-209">Uygulamanızı hello listesinde görmüyorsanız seçin **Şirketimin sahip olduğu uygulamalar** hello içinde **Göster** tıklayın ve açılan hello onay işareti.</span><span class="sxs-lookup"><span data-stu-id="3509d-209">If you don't see your application in hello list, select **Applications my company owns** in hello **Show** dropdown and click hello check mark.</span></span>
6. <span data-ttu-id="3509d-210">Merhaba sayfasının Hello altında tıklatın **yönetmek bildirim** ve ardından **karşıdan bildirim**.</span><span class="sxs-lookup"><span data-stu-id="3509d-210">At hello bottom of hello page, click **Manage Manifest** and then **Download Manifest**.</span></span>
7. <span data-ttu-id="3509d-211">Bu yordam bir .json dosyası tooyour yerel makine indirir.</span><span class="sxs-lookup"><span data-stu-id="3509d-211">This procedure downloads a .json file tooyour local machine.</span></span> <span data-ttu-id="3509d-212">Tercih ettiğiniz bir metin düzenleyicisinde düzenlemek için bu dosyayı açın.</span><span class="sxs-lookup"><span data-stu-id="3509d-212">Open this file for editing in a text editor of your choice.</span></span>
8. <span data-ttu-id="3509d-213">Merhaba üçüncü satıra hello .json dosyası, görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3509d-213">On hello third line of hello .json file, you can see:</span></span>

   ```json
   "appRoles" : [],
   ```
   <span data-ttu-id="3509d-214">Bu satırı koddan hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="3509d-214">Replace this line with hello following code:</span></span>

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access toohello application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access toodevice information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. <span data-ttu-id="3509d-215">Merhaba güncelleştirilmiş .json dosyası (Merhaba varolan dosyanın üzerine) kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3509d-215">Save hello updated .json file (you can overwrite hello existing file).</span></span>
10. <span data-ttu-id="3509d-216">Merhaba hello sayfanın hello sonundaki Klasik Azure portalı seçin **yönetmek bildirim** sonra **karşıya bildirim** hello önceki adımda kaydettiğiniz tooupload hello .json dosyası.</span><span class="sxs-lookup"><span data-stu-id="3509d-216">In hello Azure classic portal, at hello bottom of hello page, select **Manage Manifest** then **Upload Manifest** tooupload hello .json file you saved in hello previous step.</span></span>
11. <span data-ttu-id="3509d-217">Merhaba şimdi eklediğiniz **yönetici** ve **ReadOnly** rolleri tooyour uygulama.</span><span class="sxs-lookup"><span data-stu-id="3509d-217">You have now added hello **Admin** and **ReadOnly** roles tooyour application.</span></span>
12. <span data-ttu-id="3509d-218">tooassign, dizininizdeki bu rolleri tooa kullanıcı birini bkz [hello azureiotsuite.com sitesindeki izinler][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="3509d-218">tooassign one of these roles tooa user in your directory, see [Permissions on hello azureiotsuite.com site][lnk-permissions].</span></span>

## <a name="feedback"></a><span data-ttu-id="3509d-219">Geri Bildirim</span><span class="sxs-lookup"><span data-stu-id="3509d-219">Feedback</span></span>

<span data-ttu-id="3509d-220">Bu belgede ele alınan toosee istediğiniz özelleştirme var mı?</span><span class="sxs-lookup"><span data-stu-id="3509d-220">Do you have a customization you'd like toosee covered in this document?</span></span> <span data-ttu-id="3509d-221">Özellik önerileri çok eklemek[kullanıcı sesi](https://feedback.azure.com/forums/321918-azure-iot), ya da bu makaleye yorum.</span><span class="sxs-lookup"><span data-stu-id="3509d-221">Add feature suggestions too[User Voice](https://feedback.azure.com/forums/321918-azure-iot), or comment on this article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3509d-222">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3509d-222">Next steps</span></span>

<span data-ttu-id="3509d-223">Daha fazla hello seçenekleri hello önceden yapılandırılmış çözümleri özelleştirme hakkında toolearn bakın:</span><span class="sxs-lookup"><span data-stu-id="3509d-223">toolearn more about hello options for customizing hello preconfigured solutions, see:</span></span>

* <span data-ttu-id="3509d-224">[Mantıksal uygulama tooyour Azure IOT paketi uzaktan önceden yapılandırılmış izleme çözümü bağlantı][lnk-logicapp]</span><span class="sxs-lookup"><span data-stu-id="3509d-224">[Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapp]</span></span>
* <span data-ttu-id="3509d-225">[Dinamik telemetri hello Uzaktan izleme çözümü ile kullanma][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="3509d-225">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="3509d-226">[Cihaz bilgi meta verilerde hello Uzaktan izleme çözümü][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="3509d-226">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo]</span></span>
* <span data-ttu-id="3509d-227">[Merhaba Fabrika çözüm görüntüler veri OPC UA sunucularınızdan nasıl bağlanacağını özelleştirme][lnk-cf-customize]</span><span class="sxs-lookup"><span data-stu-id="3509d-227">[Customize how hello connected factory solution displays data from your OPC UA servers][lnk-cf-customize]</span></span>

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