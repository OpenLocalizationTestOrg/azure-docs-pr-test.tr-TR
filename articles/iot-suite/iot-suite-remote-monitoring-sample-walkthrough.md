---
title: "aaaRemote önceden yapılandırılmış izleme çözümünde gezinme | Microsoft Docs"
description: "Hello Azure IOT önceden yapılandırılmış çözümü uzaktan izlemenin ve mimarisinin açıklaması."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57a336bd94938c2b9ee5d3456ea8e45446cf3d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="remote-monitoring-preconfigured-solution-walkthrough"></a><span data-ttu-id="0a3ad-103">Önceden yapılandırılmış uzaktan izleme çözümünde gezinme</span><span class="sxs-lookup"><span data-stu-id="0a3ad-103">Remote monitoring preconfigured solution walkthrough</span></span>

<span data-ttu-id="0a3ad-104">IOT paketi Uzaktan izleme hello [önceden yapılandırılmış çözüm] [ lnk-preconfigured-solutions] olan bir uygulaması, bir uçtan uca izleme çözümünün uzak konumlarda çalışan birden fazla makine için.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-104">hello IoT Suite remote monitoring [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end monitoring solution for multiple machines running in remote locations.</span></span> <span data-ttu-id="0a3ad-105">Merhaba çözüm temel Azure hizmetlerini tooprovide hello iş senaryosunun genel uygulamasını birleştirir.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-105">hello solution combines key Azure services tooprovide a generic implementation of hello business scenario.</span></span> <span data-ttu-id="0a3ad-106">Merhaba çözüm kendi uygulamanız için bir başlangıç noktası olarak kullanabilirsiniz ve [özelleştirme] [ lnk-customize] , toomeet kendi belirli iş gereksinimlerinizi.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-106">You can use hello solution as a starting point for your own implementation and [customize][lnk-customize] it toomeet your own specific business requirements.</span></span>

<span data-ttu-id="0a3ad-107">Bu makalede bazı temel öğeleri hello Uzaktan izleme çözümü tooenable hello anlatılmaktadır nasıl çalıştığını toounderstand.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-107">This article walks you through some of hello key elements of hello remote monitoring solution tooenable you toounderstand how it works.</span></span> <span data-ttu-id="0a3ad-108">Bu bilgiler şunları yapmanıza yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="0a3ad-108">This knowledge helps you to:</span></span>

* <span data-ttu-id="0a3ad-109">Merhaba çözümde sorunları giderin.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-109">Troubleshoot issues in hello solution.</span></span>
* <span data-ttu-id="0a3ad-110">Plan nasıl toocustomize toohello çözüm toomeet belirli gereksinimlerinizi.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-110">Plan how toocustomize toohello solution toomeet your own specific requirements.</span></span> 
* <span data-ttu-id="0a3ad-111">Azure hizmetlerini kullanan kendi IoT çözümünüzü tasarlama.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-111">Design your own IoT solution that uses Azure services.</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="0a3ad-112">Mantıksal mimari</span><span class="sxs-lookup"><span data-stu-id="0a3ad-112">Logical architecture</span></span>

<span data-ttu-id="0a3ad-113">Diyagram aşağıdaki hello hello hello önceden yapılandırılmış çözümün mantıksal bileşenlerinin ana hatların vermektedir:</span><span class="sxs-lookup"><span data-stu-id="0a3ad-113">hello following diagram outlines hello logical components of hello preconfigured solution:</span></span>

![Mantıksal mimari](media/iot-suite-remote-monitoring-sample-walkthrough/remote-monitoring-architecture.png)

## <a name="simulated-devices"></a><span data-ttu-id="0a3ad-115">Sanal cihazlar</span><span class="sxs-lookup"><span data-stu-id="0a3ad-115">Simulated devices</span></span>

<span data-ttu-id="0a3ad-116">Merhaba önceden yapılandırılmış çözümde hello sanal cihaz bir soğutma aygıtı (örneğin, bir yapının klimaları veya tesisin havalandırma birimi) temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-116">In hello preconfigured solution, hello simulated device represents a cooling device (such as a building air conditioner or facility air handling unit).</span></span> <span data-ttu-id="0a3ad-117">Merhaba önceden yapılandırılmış çözümü dağıttığınızda, Çalıştır dört sanal cihaz da otomatik olarak sağlamak bir [Azure WebJob][lnk-webjobs].</span><span class="sxs-lookup"><span data-stu-id="0a3ad-117">When you deploy hello preconfigured solution, you also automatically provision four simulated devices that run in an [Azure WebJob][lnk-webjobs].</span></span> <span data-ttu-id="0a3ad-118">Benzetimli hello aygıtlar, tooexplore hello davranışı hello gerek toodeploy olmadan hello çözümün herhangi bir fiziksel cihaza kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-118">hello simulated devices make it easy for you tooexplore hello behavior of hello solution without hello need toodeploy any physical devices.</span></span> <span data-ttu-id="0a3ad-119">toodeploy gerçek fiziksel bir aygıtı Bkz hello [Uzaktan izleme çözümü, aygıt toohello bağlanmak] [ lnk-connect-rm] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-119">toodeploy a real physical device, see hello [Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

### <a name="device-to-cloud-messages"></a><span data-ttu-id="0a3ad-120">Cihazdan buluta iletiler</span><span class="sxs-lookup"><span data-stu-id="0a3ad-120">Device-to-cloud messages</span></span>

<span data-ttu-id="0a3ad-121">Her sanal cihaz ileti türleri tooIoT Hub aşağıdaki hello gönderebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0a3ad-121">Each simulated device can send hello following message types tooIoT Hub:</span></span>

| <span data-ttu-id="0a3ad-122">İleti</span><span class="sxs-lookup"><span data-stu-id="0a3ad-122">Message</span></span> | <span data-ttu-id="0a3ad-123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0a3ad-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0a3ad-124">Başlangıç</span><span class="sxs-lookup"><span data-stu-id="0a3ad-124">Startup</span></span> |<span data-ttu-id="0a3ad-125">Merhaba cihaz başlatıldığında, gönderen bir **cihaz bilgileri** toohello arka uç kendi hakkında bilgileri içeren ileti.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-125">When hello device starts, it sends a **device-info** message containing information about itself toohello back end.</span></span> <span data-ttu-id="0a3ad-126">Cihazın desteklediği yöntemleri hello ve bu verileri hello cihaz kimliği ve hello komutların listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-126">This data includes hello device id and a list of hello commands and methods hello device supports.</span></span> |
| <span data-ttu-id="0a3ad-127">Varlık</span><span class="sxs-lookup"><span data-stu-id="0a3ad-127">Presence</span></span> |<span data-ttu-id="0a3ad-128">Bir aygıt düzenli aralıklarla gönderir bir **varlığı** hello aygıt algılayıcı hello varlığını algılayabilir olup olmadığını tooreport iletisi.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-128">A device periodically sends a **presence** message tooreport whether hello device can sense hello presence of a sensor.</span></span> |
| <span data-ttu-id="0a3ad-129">Telemetri</span><span class="sxs-lookup"><span data-stu-id="0a3ad-129">Telemetry</span></span> |<span data-ttu-id="0a3ad-130">Bir aygıt düzenli aralıklarla gönderir bir **telemetri** hello sıcaklık ve nem hello aygıttan toplanan sanal değerlerini bildiren bir ileti algılayıcılar benzetimli.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-130">A device periodically sends a **telemetry** message that reports simulated values for hello temperature and humidity collected from hello device's simulated sensors.</span></span> |

> [!NOTE]
> <span data-ttu-id="0a3ad-131">Merhaba çözüm hello aygıt Cosmos DB veritabanında alan ve hello cihaz çifti tarafından desteklenen komutları hello listesini depolar.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-131">hello solution stores hello list of commands supported by hello device in a Cosmos DB database and not in hello device twin.</span></span>

### <a name="properties-and-device-twins"></a><span data-ttu-id="0a3ad-132">Özellikler ve cihaz ikizleri</span><span class="sxs-lookup"><span data-stu-id="0a3ad-132">Properties and device twins</span></span>

<span data-ttu-id="0a3ad-133">Merhaba sanal cihazlar Gönder cihaz özellikleri toohello aşağıdaki hello [twin] [ lnk-device-twins] hello IOT hub ' *özellikleri bildirilen*.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-133">hello simulated devices send hello following device properties toohello [twin][lnk-device-twins] in hello IoT hub as *reported properties*.</span></span> <span data-ttu-id="0a3ad-134">Merhaba aygıt gönderir bildirilen özellikleri başlangıçta ve yanıt tooa **cihaz durumunu değiştir** komut veya yöntemi.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-134">hello device sends reported properties at startup and in response tooa **Change Device State** command or method.</span></span>

| <span data-ttu-id="0a3ad-135">Özellik</span><span class="sxs-lookup"><span data-stu-id="0a3ad-135">Property</span></span> | <span data-ttu-id="0a3ad-136">Amaç</span><span class="sxs-lookup"><span data-stu-id="0a3ad-136">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="0a3ad-137">Config.TelemetryInterval</span><span class="sxs-lookup"><span data-stu-id="0a3ad-137">Config.TelemetryInterval</span></span> | <span data-ttu-id="0a3ad-138">Sıklık (saniye) hello cihaz telemetri gönderir</span><span class="sxs-lookup"><span data-stu-id="0a3ad-138">Frequency (seconds) hello device sends telemetry</span></span> |
| <span data-ttu-id="0a3ad-139">Config.TemperatureMeanValue</span><span class="sxs-lookup"><span data-stu-id="0a3ad-139">Config.TemperatureMeanValue</span></span> | <span data-ttu-id="0a3ad-140">Merhaba benzetimli sıcaklık telemetri Hello ortalama değerini belirtir</span><span class="sxs-lookup"><span data-stu-id="0a3ad-140">Specifies hello mean value for hello simulated temperature telemetry</span></span> |
| <span data-ttu-id="0a3ad-141">Device.DeviceID</span><span class="sxs-lookup"><span data-stu-id="0a3ad-141">Device.DeviceID</span></span> |<span data-ttu-id="0a3ad-142">Sağlanan veya bir aygıt hello çözümde oluşturulduğunda atanan kimliği</span><span class="sxs-lookup"><span data-stu-id="0a3ad-142">Id that is either provided or assigned when a device is created in hello solution</span></span> |
| <span data-ttu-id="0a3ad-143">Device.DeviceState</span><span class="sxs-lookup"><span data-stu-id="0a3ad-143">Device.DeviceState</span></span> | <span data-ttu-id="0a3ad-144">Merhaba aygıt tarafından bildirilen durum</span><span class="sxs-lookup"><span data-stu-id="0a3ad-144">State reported by hello device</span></span> |
| <span data-ttu-id="0a3ad-145">Device.CreatedTime</span><span class="sxs-lookup"><span data-stu-id="0a3ad-145">Device.CreatedTime</span></span> |<span data-ttu-id="0a3ad-146">Zaman hello aygıt hello çözümde oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="0a3ad-146">Time hello device was created in hello solution</span></span> |
| <span data-ttu-id="0a3ad-147">Device.StartupTime</span><span class="sxs-lookup"><span data-stu-id="0a3ad-147">Device.StartupTime</span></span> |<span data-ttu-id="0a3ad-148">Zaman hello aygıt başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-148">Time hello device was started</span></span> |
| <span data-ttu-id="0a3ad-149">Device.LastDesiredPropertyChange</span><span class="sxs-lookup"><span data-stu-id="0a3ad-149">Device.LastDesiredPropertyChange</span></span> |<span data-ttu-id="0a3ad-150">Merhaba son istenen özelliği Hello sürüm numarasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="0a3ad-150">hello version number of hello last desired property change</span></span> |
| <span data-ttu-id="0a3ad-151">Device.Location.Latitude</span><span class="sxs-lookup"><span data-stu-id="0a3ad-151">Device.Location.Latitude</span></span> |<span data-ttu-id="0a3ad-152">Merhaba cihazın enlem konumu</span><span class="sxs-lookup"><span data-stu-id="0a3ad-152">Latitude location of hello device</span></span> |
| <span data-ttu-id="0a3ad-153">Device.Location.Longitude</span><span class="sxs-lookup"><span data-stu-id="0a3ad-153">Device.Location.Longitude</span></span> |<span data-ttu-id="0a3ad-154">Merhaba cihazın boylam konumu</span><span class="sxs-lookup"><span data-stu-id="0a3ad-154">Longitude location of hello device</span></span> |
| <span data-ttu-id="0a3ad-155">System.Manufacturer</span><span class="sxs-lookup"><span data-stu-id="0a3ad-155">System.Manufacturer</span></span> |<span data-ttu-id="0a3ad-156">Cihaz üreticisi</span><span class="sxs-lookup"><span data-stu-id="0a3ad-156">Device manufacturer</span></span> |
| <span data-ttu-id="0a3ad-157">System.ModelNumber</span><span class="sxs-lookup"><span data-stu-id="0a3ad-157">System.ModelNumber</span></span> |<span data-ttu-id="0a3ad-158">Merhaba cihazın model numarası</span><span class="sxs-lookup"><span data-stu-id="0a3ad-158">Model number of hello device</span></span> |
| <span data-ttu-id="0a3ad-159">System.SerialNumber</span><span class="sxs-lookup"><span data-stu-id="0a3ad-159">System.SerialNumber</span></span> |<span data-ttu-id="0a3ad-160">Merhaba cihaz seri numarası</span><span class="sxs-lookup"><span data-stu-id="0a3ad-160">Serial number of hello device</span></span> |
| <span data-ttu-id="0a3ad-161">System.FirmwareVersion</span><span class="sxs-lookup"><span data-stu-id="0a3ad-161">System.FirmwareVersion</span></span> |<span data-ttu-id="0a3ad-162">Geçerli hello cihazdaki üretici yazılımı sürümü</span><span class="sxs-lookup"><span data-stu-id="0a3ad-162">Current version of firmware on hello device</span></span> |
| <span data-ttu-id="0a3ad-163">System.Platform</span><span class="sxs-lookup"><span data-stu-id="0a3ad-163">System.Platform</span></span> |<span data-ttu-id="0a3ad-164">Merhaba cihazın Platform mimarisi</span><span class="sxs-lookup"><span data-stu-id="0a3ad-164">Platform architecture of hello device</span></span> |
| <span data-ttu-id="0a3ad-165">System.Processor</span><span class="sxs-lookup"><span data-stu-id="0a3ad-165">System.Processor</span></span> |<span data-ttu-id="0a3ad-166">İşlemci çalışan hello aygıtı</span><span class="sxs-lookup"><span data-stu-id="0a3ad-166">Processor running hello device</span></span> |
| <span data-ttu-id="0a3ad-167">System.InstalledRAM</span><span class="sxs-lookup"><span data-stu-id="0a3ad-167">System.InstalledRAM</span></span> |<span data-ttu-id="0a3ad-168">Merhaba cihazda yüklü RAM miktarı</span><span class="sxs-lookup"><span data-stu-id="0a3ad-168">Amount of RAM installed on hello device</span></span> |

<span data-ttu-id="0a3ad-169">Merhaba benzetici, örnek değerlerle sanal cihazlarda bu özelliklerin çekirdeğini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-169">hello simulator seeds these properties in simulated devices with sample values.</span></span> <span data-ttu-id="0a3ad-170">Merhaba simulator başlatır sanal cihaz, hello cihaz her zaman hello önceden tanımlanmış meta verileri tooIoT Hub bildirilen özellikleri olarak bildirir.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-170">Each time hello simulator initializes a simulated device, hello device reports hello pre-defined metadata tooIoT Hub as reported properties.</span></span> <span data-ttu-id="0a3ad-171">Bildirilen özellikleri yalnızca hello aygıt tarafından güncelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-171">Reported properties can only be updated by hello device.</span></span> <span data-ttu-id="0a3ad-172">toochange bildirilen bir özellik, çözüm Portalı'nda istenen bir özellik Ayarla.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-172">toochange a reported property, you set a desired property in solution portal.</span></span> <span data-ttu-id="0a3ad-173">Merhaba cihaza hello sorumluluğunda olan:</span><span class="sxs-lookup"><span data-stu-id="0a3ad-173">It is hello responsibility of hello device to:</span></span>

1. <span data-ttu-id="0a3ad-174">Düzenli aralıklarla istenen hello IOT hub'ından alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-174">Periodically retrieve desired properties from hello IoT hub.</span></span>
2. <span data-ttu-id="0a3ad-175">İstenen başlangıç özellik değeri ile yapılandırmasını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-175">Update its configuration with hello desired property value.</span></span>
3. <span data-ttu-id="0a3ad-176">Merhaba yeni değer geri toohello hub'ı bildirilen bir özellik olarak gönderin.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-176">Send hello new value back toohello hub as a reported property.</span></span>

<span data-ttu-id="0a3ad-177">Merhaba çözüm panodan kullandığınız *özellikleri istenen* tooset özellikleri hello kullanarak bir cihazdaki [cihaz çifti][lnk-device-twins].</span><span class="sxs-lookup"><span data-stu-id="0a3ad-177">From hello solution dashboard, you can use *desired properties* tooset properties on a device by using hello [device twin][lnk-device-twins].</span></span> <span data-ttu-id="0a3ad-178">Genellikle, bir cihaz hello hub tooupdate kendi iç durumu ve rapor hello geri bildirilen bir özellik olarak değiştirmek istediğiniz özellik değeri okur.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-178">Typically, a device reads a desired property value from hello hub tooupdate its internal state and report hello change back as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="0a3ad-179">Merhaba sanal cihaz kodu yalnızca hello kullanan **Desired.Config.TemperatureMeanValue** ve **Desired.Config.TelemetryInterval** istenen özellikleri tooupdate hello bildirilen geri gönderilen özellikleri tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-179">hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties sent back tooIoT Hub.</span></span> <span data-ttu-id="0a3ad-180">Diğer tüm istenen özelliği değişiklik isteklerini hello sanal cihazda göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-180">All other desired property change requests are ignored in hello simulated device.</span></span>

### <a name="methods"></a><span data-ttu-id="0a3ad-181">Yöntemler</span><span class="sxs-lookup"><span data-stu-id="0a3ad-181">Methods</span></span>

<span data-ttu-id="0a3ad-182">Merhaba sanal cihazlar yöntemler aşağıdaki hello işleyebilir ([doğrudan yöntemleri][lnk-direct-methods]) hello çözüm portalı hello IOT hub'ı aracılığıyla çağrılır:</span><span class="sxs-lookup"><span data-stu-id="0a3ad-182">hello simulated devices can handle hello following methods ([direct methods][lnk-direct-methods]) invoked from hello solution portal through hello IoT hub:</span></span>

| <span data-ttu-id="0a3ad-183">Yöntem</span><span class="sxs-lookup"><span data-stu-id="0a3ad-183">Method</span></span> | <span data-ttu-id="0a3ad-184">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0a3ad-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0a3ad-185">InitiateFirmwareUpdate</span><span class="sxs-lookup"><span data-stu-id="0a3ad-185">InitiateFirmwareUpdate</span></span> |<span data-ttu-id="0a3ad-186">Merhaba aygıt tooperform bellenim güncelleştirme yönlendirir</span><span class="sxs-lookup"><span data-stu-id="0a3ad-186">Instructs hello device tooperform a firmware update</span></span> |
| <span data-ttu-id="0a3ad-187">Yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="0a3ad-187">Reboot</span></span> |<span data-ttu-id="0a3ad-188">Merhaba aygıt tooreboot bildirir</span><span class="sxs-lookup"><span data-stu-id="0a3ad-188">Instructs hello device tooreboot</span></span> |
| <span data-ttu-id="0a3ad-189">FactoryReset</span><span class="sxs-lookup"><span data-stu-id="0a3ad-189">FactoryReset</span></span> |<span data-ttu-id="0a3ad-190">Bir fabrika ayarlarına sıfırlayıp hello aygıt tooperform bildirir</span><span class="sxs-lookup"><span data-stu-id="0a3ad-190">Instructs hello device tooperform a factory reset</span></span> |

<span data-ttu-id="0a3ad-191">Bazı yöntemler bildirilen özellikleri tooreport ilerlemeyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-191">Some methods use reported properties tooreport on progress.</span></span> <span data-ttu-id="0a3ad-192">Örneğin, hello **InitiateFirmwareUpdate** yöntemi zaman uyumsuz olarak hello cihazda çalışan hello güncelleştirme benzetimini yapar.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-192">For example, hello **InitiateFirmwareUpdate** method simulates running hello update asynchronously on hello device.</span></span> <span data-ttu-id="0a3ad-193">Merhaba zaman uyumsuz görev geri toosend durum güncelleştirmeleri devam ederken hello yöntemi hemen hello aygıtta döndürür toohello çözüm panosunu kullanma özellikleri bildirdi.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-193">hello method returns immediately on hello device, while hello asynchronous task continues toosend status updates back toohello solution dashboard using reported properties.</span></span>

### <a name="commands"></a><span data-ttu-id="0a3ad-194">Komutlar</span><span class="sxs-lookup"><span data-stu-id="0a3ad-194">Commands</span></span>

<span data-ttu-id="0a3ad-195">Benzetimli hello cihazlar hello çözüm portalı hello IOT hub'ı aracılığıyla gönderilen komutları (bulut-cihaz iletilerini) aşağıdaki hello işleyebilir:</span><span class="sxs-lookup"><span data-stu-id="0a3ad-195">hello simulated devices can handle hello following commands (cloud-to-device messages) sent from hello solution portal through hello IoT hub:</span></span>

| <span data-ttu-id="0a3ad-196">Komut</span><span class="sxs-lookup"><span data-stu-id="0a3ad-196">Command</span></span> | <span data-ttu-id="0a3ad-197">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0a3ad-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0a3ad-198">PingDevice</span><span class="sxs-lookup"><span data-stu-id="0a3ad-198">PingDevice</span></span> |<span data-ttu-id="0a3ad-199">Gönderen bir *ping* Canlı toohello aygıt toocheck</span><span class="sxs-lookup"><span data-stu-id="0a3ad-199">Sends a *ping* toohello device toocheck it is alive</span></span> |
| <span data-ttu-id="0a3ad-200">StartTelemetry</span><span class="sxs-lookup"><span data-stu-id="0a3ad-200">StartTelemetry</span></span> |<span data-ttu-id="0a3ad-201">Telemetri göndermesini başlatır hello cihaz</span><span class="sxs-lookup"><span data-stu-id="0a3ad-201">Starts hello device sending telemetry</span></span> |
| <span data-ttu-id="0a3ad-202">StopTelemetry</span><span class="sxs-lookup"><span data-stu-id="0a3ad-202">StopTelemetry</span></span> |<span data-ttu-id="0a3ad-203">Cihazın telemetri göndermesini durdurur hello</span><span class="sxs-lookup"><span data-stu-id="0a3ad-203">Stops hello device from sending telemetry</span></span> |
| <span data-ttu-id="0a3ad-204">ChangeSetPointTemp</span><span class="sxs-lookup"><span data-stu-id="0a3ad-204">ChangeSetPointTemp</span></span> |<span data-ttu-id="0a3ad-205">Değişiklikleri hello ayar noktası değerini hangi hello rastgele verilerin oluşturulur</span><span class="sxs-lookup"><span data-stu-id="0a3ad-205">Changes hello set point value around which hello random data is generated</span></span> |
| <span data-ttu-id="0a3ad-206">DiagnosticTelemetry</span><span class="sxs-lookup"><span data-stu-id="0a3ad-206">DiagnosticTelemetry</span></span> |<span data-ttu-id="0a3ad-207">Aygıt benzeticisi toosend ek bir telemetri değeri (externalTemp) Tetikleyicileri hello</span><span class="sxs-lookup"><span data-stu-id="0a3ad-207">Triggers hello device simulator toosend an additional telemetry value (externalTemp)</span></span> |
| <span data-ttu-id="0a3ad-208">ChangeDeviceState</span><span class="sxs-lookup"><span data-stu-id="0a3ad-208">ChangeDeviceState</span></span> |<span data-ttu-id="0a3ad-209">Merhaba cihaz için Genişletilmiş durum özelliğini değiştirir ve hello aygıttan hello cihaz bilgi iletisi gönderir</span><span class="sxs-lookup"><span data-stu-id="0a3ad-209">Changes an extended state property for hello device and sends hello device info message from hello device</span></span> |

> [!NOTE]
> <span data-ttu-id="0a3ad-210">Bu komutlar (buluttan cihaza iletiler) ile yöntemlerin (doğrudan yöntemler) bir karşılaştırması için bkz. [Buluttan cihaza iletişim kılavuzu][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="0a3ad-210">For a comparison of these commands (cloud-to-device messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>

## <a name="iot-hub"></a><span data-ttu-id="0a3ad-211">IoT Hub’ı</span><span class="sxs-lookup"><span data-stu-id="0a3ad-211">IoT Hub</span></span>

<span data-ttu-id="0a3ad-212">Merhaba [IOT hub'ı] [ lnk-iothub] hello aygıtlardan hello buluta gönderilen verileri alır ve kullanılabilir toohello Azure Stream Analytics (ASA) işini kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-212">hello [IoT hub][lnk-iothub] ingests data sent from hello devices into hello cloud and makes it available toohello Azure Stream Analytics (ASA) jobs.</span></span> <span data-ttu-id="0a3ad-213">Her akış ASA işi cihazlarınızdan gelen iletileri ayrı IOT Hub tüketici grubu tooread hello akışı kullanır.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-213">Each stream ASA job uses a separate IoT Hub consumer group tooread hello stream of messages from your devices.</span></span>

<span data-ttu-id="0a3ad-214">IOT hub'hello çözümde de hello:</span><span class="sxs-lookup"><span data-stu-id="0a3ad-214">hello IoT hub in hello solution also:</span></span>

- <span data-ttu-id="0a3ad-215">Merhaba kimlikleri ve tooconnect toohello portal izin verilen tüm hello cihazların kimlik doğrulama anahtarlarını depolayan bir kimlik kayıt defteri tutar.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-215">Maintains an identity registry that stores hello ids and authentication keys of all hello devices permitted tooconnect toohello portal.</span></span> <span data-ttu-id="0a3ad-216">Etkinleştirme ve cihazları hello kimlik kayıt defteri aracılığıyla devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-216">You can enable and disable devices through hello identity registry.</span></span>
- <span data-ttu-id="0a3ad-217">Komutları tooyour cihazların Merhaba çözüm portalı adına gönderir.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-217">Sends commands tooyour devices on behalf of hello solution portal.</span></span>
- <span data-ttu-id="0a3ad-218">Merhaba çözüm portalı adına cihazlarınızda yöntemleri çağırır.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-218">Invokes methods on your devices on behalf of hello solution portal.</span></span>
- <span data-ttu-id="0a3ad-219">Tüm kayıtlı cihazlar için cihaz ikizlerini tutar.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-219">Maintains device twins for all registered devices.</span></span> <span data-ttu-id="0a3ad-220">Cihaz çifti bir cihaz tarafından raporlanan hello özellik değerlerini depolar.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-220">A device twin stores hello property values reported by a device.</span></span> <span data-ttu-id="0a3ad-221">Cihaz çifti hello çözüm portalında, sonraki bağlandığında hello aygıt tooretrieve ayarlamak istediğiniz özellikleri de depolar.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-221">A device twin also stores desired properties, set in hello solution portal, for hello device tooretrieve when it next connects.</span></span>
- <span data-ttu-id="0a3ad-222">Zamanlamaları birden çok aygıt tooset özelliklerini işleri veya birden çok aygıta yöntemleri çağırma.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-222">Schedules jobs tooset properties for multiple devices or invoke methods on multiple devices.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="0a3ad-223">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0a3ad-223">Azure Stream Analytics</span></span>

<span data-ttu-id="0a3ad-224">Uzaktan izleme çözümü, hello içinde [Azure akış analizi] [ lnk-asa] (ASA) işleme veya depolama hello IOT hub tooother arka uç bileşenleri tarafından alınan aygıt iletileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-224">In hello remote monitoring solution, [Azure Stream Analytics][lnk-asa] (ASA) dispatches device messages received by hello IoT hub tooother back-end components for processing or storage.</span></span> <span data-ttu-id="0a3ad-225">Farklı ASA işleri Merhaba iletileri Merhaba içeriğine göre belirli işlevler gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-225">Different ASA jobs perform specific functions based on hello content of hello messages.</span></span>

<span data-ttu-id="0a3ad-226">**İş 1: Cihaz bilgileri** hello gelen ileti akışından cihaz bilgileri iletilerine filtre uygular ve bunları tooan olay hub'ı uç gönderir.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-226">**Job 1: Device Info** filters device information messages from hello incoming message stream and sends them tooan Event Hub endpoint.</span></span> <span data-ttu-id="0a3ad-227">Bir aygıt cihaz bilgileri iletilerini başlangıçta ve yanıt tooa gönderir **Senddeviceınfo** komutu.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-227">A device sends device information messages at startup and in response tooa **SendDeviceInfo** command.</span></span> <span data-ttu-id="0a3ad-228">Bu iş şu Sorgu tanımını tooidentify hello kullanır **cihaz bilgileri** iletileri:</span><span class="sxs-lookup"><span data-stu-id="0a3ad-228">This job uses hello following query definition tooidentify **device-info** messages:</span></span>

```
SELECT * FROM DeviceDataStream Partition By PartitionId WHERE  ObjectType = 'DeviceInfo'
```

<span data-ttu-id="0a3ad-229">Bu iş daha ayrıntılı işleme için kendi çıktı tooan olay hub'ı gönderir.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-229">This job sends its output tooan Event Hub for further processing.</span></span>

<span data-ttu-id="0a3ad-230">**İş 2: Kurallar** cihaz başına eşiklere karşılık gelen sıcaklık ve nem telemetrisi değerlerini değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-230">**Job 2: Rules** evaluates incoming temperature and humidity telemetry values against per-device thresholds.</span></span> <span data-ttu-id="0a3ad-231">Eşik değerleri hello çözüm portalında kullanılabilir hello kurallar düzenleyicisinde ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-231">Threshold values are set in hello rules editor available in hello solution portal.</span></span> <span data-ttu-id="0a3ad-232">Her cihaz/değer çifti, Akış Analizi’nin **Başvuru Verileri** olarak okuduğu blob’daki zaman damgası tarafından depolanır.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-232">Each device/value pair is stored by timestamp in a blob which Stream Analytics reads in as **Reference Data**.</span></span> <span data-ttu-id="0a3ad-233">Merhaba iş herhangi boş olmayan değerleri hello hello cihaz için ayarlanan eşikle karşılaştırır.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-233">hello job compares any non-empty value against hello set threshold for hello device.</span></span> <span data-ttu-id="0a3ad-234">Merhaba aşarsa, ' >' koşulunu, hello iş bir **alarm** bu hello eşik gösteren olay aşılırsa ve hello cihaz, değer ve zaman damgası değerlerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-234">If it exceeds hello '>' condition, hello job outputs an **alarm** event that indicates that hello threshold is exceeded and provides hello device, value, and timestamp values.</span></span> <span data-ttu-id="0a3ad-235">Bu iş bir alarm tetiklemesi gereken sorgu tanımı tooidentify telemetri iletilerini aşağıdaki hello kullanır:</span><span class="sxs-lookup"><span data-stu-id="0a3ad-235">This job uses hello following query definition tooidentify telemetry messages that should trigger an alarm:</span></span>

```
WITH AlarmsData AS 
(
SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Temperature' as ReadingType,
     Stream.Temperature as Reading,
     Ref.Temperature as Threshold,
     Ref.TemperatureRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature

UNION ALL

SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Humidity' as ReadingType,
     Stream.Humidity as Reading,
     Ref.Humidity as Threshold,
     Ref.HumidityRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
)

SELECT *
INTO DeviceRulesMonitoring
FROM AlarmsData

SELECT *
INTO DeviceRulesHub
FROM AlarmsData
```

<span data-ttu-id="0a3ad-236">Merhaba iş kendi çıktı tooan olay hub'ı başka bir işleme için gönderir ve hello çözüm portalı hello uyarı bilgilerini nerede okuyabileceği her uyarı tooblob depolama ayrıntılarını kaydeder.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-236">hello job sends its output tooan Event Hub for further processing and saves details of each alert tooblob storage from where hello solution portal can read hello alert information.</span></span>

<span data-ttu-id="0a3ad-237">**Ş 3: Telemetri** hello gelen cihaz telemetrisi akışını iki yolla çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-237">**Job 3: Telemetry** operates on hello incoming device telemetry stream in two ways.</span></span> <span data-ttu-id="0a3ad-238">Merhaba önce hello aygıtları toopersistent blob depolamadan uzun vadeli depolama için tüm telemetri iletilerini gönderir.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-238">hello first sends all telemetry messages from hello devices toopersistent blob storage for long-term storage.</span></span> <span data-ttu-id="0a3ad-239">Merhaba, ortalama, minimum ve Maksimum nem beş dakikalık kayan pencere üzerinde değerleri ve bu verileri tooblob depolama gönderir ikinci hesaplar.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-239">hello second computes average, minimum, and maximum humidity values over a five-minute sliding window and sends this data tooblob storage.</span></span> <span data-ttu-id="0a3ad-240">Merhaba çözüm portalı blob depolama toopopulate hello grafikten hello telemetri verilerini okur.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-240">hello solution portal reads hello telemetry data from blob storage toopopulate hello charts.</span></span> <span data-ttu-id="0a3ad-241">Bu iş hello aşağıdaki sorgu tanımını kullanır:</span><span class="sxs-lookup"><span data-stu-id="0a3ad-241">This job uses hello following query definition:</span></span>

```
WITH 
    [StreamData]
AS (
    SELECT
        *
    FROM [IoTHubStream]
    WHERE
        [ObjectType] IS NULL -- Filter out device info and command responses
) 

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    Temperature,
    Humidity,
    ExternalTemperature,
    EventProcessedUtcTime,
    PartitionId,
    EventEnqueuedUtcTime,
    * 
INTO
    [Telemetry]
FROM
    [StreamData]

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    AVG (Humidity) AS [AverageHumidity],
    MIN(Humidity) AS [MinimumHumidity],
    MAX(Humidity) AS [MaxHumidity],
    5.0 AS TimeframeMinutes 
INTO
    [TelemetrySummary]
FROM [StreamData]
WHERE
    [Humidity] IS NOT NULL
GROUP BY
    IoTHub.ConnectionDeviceId,
    SlidingWindow (mi, 5)
```

## <a name="event-hubs"></a><span data-ttu-id="0a3ad-242">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="0a3ad-242">Event Hubs</span></span>

<span data-ttu-id="0a3ad-243">Merhaba **cihaz bilgileri** ve **kuralları** ASA işleri çıktı kendi veri tooEvent hub tooreliably İleri toohello üzerinde **olay işlemcisi** hello Web işi çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-243">hello **device info** and **rules** ASA jobs output their data tooEvent Hubs tooreliably forward on toohello **Event Processor** running in hello WebJob.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="0a3ad-244">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0a3ad-244">Azure storage</span></span>

<span data-ttu-id="0a3ad-245">Merhaba çözüm Azure blob depolama toopersist hello çözümde hello aygıtlardan tüm hello ham ve Özet telemetri verilerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-245">hello solution uses Azure blob storage toopersist all hello raw and summarized telemetry data from hello devices in hello solution.</span></span> <span data-ttu-id="0a3ad-246">Merhaba portal blob depolama toopopulate hello grafikten hello telemetri verilerini okur.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-246">hello portal reads hello telemetry data from blob storage toopopulate hello charts.</span></span> <span data-ttu-id="0a3ad-247">telemetri aşıldı değerleri hello eşik değerleri yapılandırıldığında toodisplay uyarıları kaydeden blob depolama alanından hello veri hello çözüm portalı okur.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-247">toodisplay alerts, hello solution portal reads hello data from blob storage that records when telemetry values exceeded hello configured threshold values.</span></span> <span data-ttu-id="0a3ad-248">Merhaba çözüm ayrıca hello çözüm portalında ayarladığınız blob depolama toorecord hello eşik değerleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-248">hello solution also uses blob storage toorecord hello threshold values you set in hello solution portal.</span></span>

## <a name="webjobs"></a><span data-ttu-id="0a3ad-249">WebJobs</span><span class="sxs-lookup"><span data-stu-id="0a3ad-249">WebJobs</span></span>

<span data-ttu-id="0a3ad-250">Ayrıca toohosting hello cihaz benzeticilerini hello WebJobs hello çözümde de konak hello **olay işlemcisi** komut yanıtlarını işleyen bir Azure WebJob içinde çalışan.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-250">In addition toohosting hello device simulators, hello WebJobs in hello solution also host hello **Event Processor** running in an Azure WebJob that handles command responses.</span></span> <span data-ttu-id="0a3ad-251">Komut yanıtı iletileri tooupdate hello cihaz komut geçmişini (Merhaba Cosmos DB veritabanında depolanır) kullanır.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-251">It uses command response messages tooupdate hello device command history (stored in hello Cosmos DB database).</span></span>

## <a name="cosmos-db"></a><span data-ttu-id="0a3ad-252">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0a3ad-252">Cosmos DB</span></span>

<span data-ttu-id="0a3ad-253">Merhaba çözüm hello aygıtları bağlı toohello çözüm Cosmos DB veritabanı toostore bilgilerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-253">hello solution uses a Cosmos DB database toostore information about hello devices connected toohello solution.</span></span> <span data-ttu-id="0a3ad-254">Bu bilgiler hello geçmişi hello çözüm Portalı'ndan toodevices gönderilen komutları ve hello çözüm Portalı'ndan çağrılan yöntemler içerir.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-254">This information includes hello history of commands sent toodevices from hello solution portal and of methods invoked from hello solution portal.</span></span>

## <a name="solution-portal"></a><span data-ttu-id="0a3ad-255">Çözüm portalı</span><span class="sxs-lookup"><span data-stu-id="0a3ad-255">Solution portal</span></span>

<span data-ttu-id="0a3ad-256">Merhaba çözüm portalı hello önceden yapılandırılmış çözümün bir parçası dağıtılan bir web uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-256">hello solution portal is a web app deployed as part of hello preconfigured solution.</span></span> <span data-ttu-id="0a3ad-257">Merhaba anahtar hello çözüm portalında hello Pano ve hello cihaz listesi sayfalarıdır.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-257">hello key pages in hello solution portal are hello dashboard and hello device list.</span></span>

### <a name="dashboard"></a><span data-ttu-id="0a3ad-258">Pano</span><span class="sxs-lookup"><span data-stu-id="0a3ad-258">Dashboard</span></span>

<span data-ttu-id="0a3ad-259">Merhaba web uygulamasındaki bu sayfa Powerbı javascript denetimlerini kullanır (bkz [Powerbı-visuals repo](https://www.github.com/Microsoft/PowerBI-visuals)) hello cihazlardan toovisualize hello telemetri verileri.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-259">This page in hello web app uses PowerBI javascript controls (See [PowerBI-visuals repo](https://www.github.com/Microsoft/PowerBI-visuals)) toovisualize hello telemetry data from hello devices.</span></span> <span data-ttu-id="0a3ad-260">Merhaba çözüm hello ASA telemetri işini toowrite hello telemetri verileri tooblob depolama kullanır.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-260">hello solution uses hello ASA telemetry job toowrite hello telemetry data tooblob storage.</span></span>

### <a name="device-list"></a><span data-ttu-id="0a3ad-261">Cihaz listesi</span><span class="sxs-lookup"><span data-stu-id="0a3ad-261">Device list</span></span>

<span data-ttu-id="0a3ad-262">Bu sayfadan hello çözüm portalında şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0a3ad-262">From this page in hello solution portal you can:</span></span>

* <span data-ttu-id="0a3ad-263">Yeni bir cihaz hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-263">Provision a new device.</span></span> <span data-ttu-id="0a3ad-264">Bu eylemin hello benzersiz cihaz kimliğini ayarlar ve hello kimlik doğrulama anahtarı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-264">This action sets hello unique device id and generates hello authentication key.</span></span> <span data-ttu-id="0a3ad-265">Merhaba çözüme özel Cosmos DB veritabanı ve hello aygıt tooboth hello IOT Hub kimlik kayıt defteri hakkında bilgi yazar.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-265">It writes information about hello device tooboth hello IoT Hub identity registry and hello solution-specific Cosmos DB database.</span></span>
* <span data-ttu-id="0a3ad-266">Cihaz özelliklerini yönetin.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-266">Manage device properties.</span></span> <span data-ttu-id="0a3ad-267">Bu eylem, mevcut özellikleri görüntülemeyi ve yeni özelliklerle güncelleştirmeyi kapsar.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-267">This action includes viewing existing properties and updating with new properties.</span></span>
* <span data-ttu-id="0a3ad-268">Komutları tooa aygıt gönderin.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-268">Send commands tooa device.</span></span>
* <span data-ttu-id="0a3ad-269">Bir aygıt için Hello komut geçmişini görüntüleme.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-269">View hello command history for a device.</span></span>
* <span data-ttu-id="0a3ad-270">Cihazları etkinleştirin ve devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="0a3ad-270">Enable and disable devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a3ad-271">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0a3ad-271">Next steps</span></span>

<span data-ttu-id="0a3ad-272">Merhaba aşağıdaki TechNet blog gönderileri hello Uzaktan izleme çözümü hakkında daha ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="0a3ad-272">hello following TechNet blog posts provide more detail about hello remote monitoring preconfigured solution:</span></span>

* [<span data-ttu-id="0a3ad-273">IOT paketi - altında hello başlık - Uzaktan izleme</span><span class="sxs-lookup"><span data-stu-id="0a3ad-273">IoT Suite - Under hello Hood - Remote Monitoring</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32941.iot-suite-under-the-hood-remote-monitoring.aspx)
* [<span data-ttu-id="0a3ad-274">IoT Paketi - Uzaktan İzleme - Canlı ve Sanal Cihaz Ekleme</span><span class="sxs-lookup"><span data-stu-id="0a3ad-274">IoT Suite - Remote Monitoring - Adding Live and Simulated Devices</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/32975.iot-suite-remote-monitoring-adding-live-and-simulated-devices.aspx)

<span data-ttu-id="0a3ad-275">Makaleler hello okuyarak IOT paketi ile çalışmaya başlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0a3ad-275">You can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="0a3ad-276">[Uzaktan izleme çözümü, aygıt toohello Bağlan][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="0a3ad-276">[Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="0a3ad-277">[Merhaba azureiotsuite.com sitesindeki izinler][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="0a3ad-277">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-iothub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-webjobs]: https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twins]:  ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
