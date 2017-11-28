---
title: "meta verilerde hello Uzaktan izleme çözümü aaaDevice bilgi | Microsoft Docs"
description: "Hello Azure IOT önceden yapılandırılmış çözümü uzaktan izlemenin ve mimarisinin açıklaması."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1b334769-103b-4eb0-a293-184f3d1ba9a3
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 8387b98b8b2ae4934b0c900bc4df37dc17337c60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="device-information-metadata-in-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="ba3ef-103">Cihaz bilgi meta verilerde hello Uzaktan izleme çözümü</span><span class="sxs-lookup"><span data-stu-id="ba3ef-103">Device information metadata in hello remote monitoring preconfigured solution</span></span>

<span data-ttu-id="ba3ef-104">Hello Azure IOT paketi Uzaktan izleme çözümü cihaz meta verilerini yönetmek için bir yaklaşım gösterir.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-104">hello Azure IoT Suite remote monitoring preconfigured solution demonstrates an approach for managing device metadata.</span></span> <span data-ttu-id="ba3ef-105">Bu makalede hello yaklaşım özetlenmektedir Bu çözüm tooenable alır, toounderstand:</span><span class="sxs-lookup"><span data-stu-id="ba3ef-105">This article outlines hello approach this solution takes tooenable you toounderstand:</span></span>

* <span data-ttu-id="ba3ef-106">Hangi cihaz meta verilerini hello çözümü depolar.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-106">What device metadata hello solution stores.</span></span>
* <span data-ttu-id="ba3ef-107">Nasıl hello çözüm hello cihaz meta verilerini yönetir.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-107">How hello solution manages hello device metadata.</span></span>

## <a name="context"></a><span data-ttu-id="ba3ef-108">Bağlam</span><span class="sxs-lookup"><span data-stu-id="ba3ef-108">Context</span></span>

<span data-ttu-id="ba3ef-109">Merhaba çözümü kullanan önceden yapılandırılmış Uzaktan izleme [Azure IOT Hub] [ lnk-iot-hub] tooenable aygıtları toosend veri toohello bulut.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-109">hello remote monitoring preconfigured solution uses [Azure IoT Hub][lnk-iot-hub] tooenable your devices toosend data toohello cloud.</span></span> <span data-ttu-id="ba3ef-110">Merhaba çözümü üç farklı konumlarda cihazlarla ilgili bilgileri depolar:</span><span class="sxs-lookup"><span data-stu-id="ba3ef-110">hello solution stores information about devices in three different locations:</span></span>

| <span data-ttu-id="ba3ef-111">Konum</span><span class="sxs-lookup"><span data-stu-id="ba3ef-111">Location</span></span> | <span data-ttu-id="ba3ef-112">Depolanan bilgileri</span><span class="sxs-lookup"><span data-stu-id="ba3ef-112">Information stored</span></span> | <span data-ttu-id="ba3ef-113">Uygulama</span><span class="sxs-lookup"><span data-stu-id="ba3ef-113">Implementation</span></span> |
| -------- | ------------------ | -------------- |
| <span data-ttu-id="ba3ef-114">Kimlik kayıt defteri</span><span class="sxs-lookup"><span data-stu-id="ba3ef-114">Identity registry</span></span> | <span data-ttu-id="ba3ef-115">Cihaz kimliği, kimlik doğrulaması anahtarları, durumu etkin</span><span class="sxs-lookup"><span data-stu-id="ba3ef-115">Device id, authentication keys, enabled state</span></span> | <span data-ttu-id="ba3ef-116">Yerleşik tooIoT Hub</span><span class="sxs-lookup"><span data-stu-id="ba3ef-116">Built in tooIoT Hub</span></span> |
| <span data-ttu-id="ba3ef-117">Cihaz çiftlerini</span><span class="sxs-lookup"><span data-stu-id="ba3ef-117">Device twins</span></span> | <span data-ttu-id="ba3ef-118">Meta veriler: bildirilen özellikleri, istenen özellikleri, etiketler</span><span class="sxs-lookup"><span data-stu-id="ba3ef-118">Metadata: reported properties, desired properties, tags</span></span> | <span data-ttu-id="ba3ef-119">Yerleşik tooIoT Hub</span><span class="sxs-lookup"><span data-stu-id="ba3ef-119">Built in tooIoT Hub</span></span> |
| <span data-ttu-id="ba3ef-120">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ba3ef-120">Cosmos DB</span></span> | <span data-ttu-id="ba3ef-121">Komut ve yöntemi geçmişi</span><span class="sxs-lookup"><span data-stu-id="ba3ef-121">Command and method history</span></span> | <span data-ttu-id="ba3ef-122">Özel çözüm için</span><span class="sxs-lookup"><span data-stu-id="ba3ef-122">Custom for solution</span></span> |

<span data-ttu-id="ba3ef-123">IOT hub'ında bir [cihaz kimlik kayıt defteri] [ lnk-identity-registry] toomanage erişim tooan IOT hub ve kullandığı [cihaz çiftlerini] [ lnk-device-twin] toomanage cihaz meta veriler .</span><span class="sxs-lookup"><span data-stu-id="ba3ef-123">IoT Hub includes a [device identity registry][lnk-identity-registry] toomanage access tooan IoT hub and uses [device twins][lnk-device-twin] toomanage device metadata.</span></span> <span data-ttu-id="ba3ef-124">Ayrıca bir uzaktan izleme çözümü özgü olan *cihaz kayıt defteri* komutu ve yöntemi geçmişini saklar.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-124">There is also a remote monitoring solution-specific *device registry* that stores command and method history.</span></span> <span data-ttu-id="ba3ef-125">Merhaba Uzaktan izleme çözümü kullanan bir [Cosmos DB] [ lnk-docdb] veritabanı tooimplement komut ve yöntemi geçmişi için özel bir depo.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-125">hello remote monitoring solution uses a [Cosmos DB][lnk-docdb] database tooimplement a custom store for command and method history.</span></span>

> [!NOTE]
> <span data-ttu-id="ba3ef-126">Uzaktan izleme çözümü Hello hello cihaz kimlik kayıt defteri hello Cosmos DB veritabanında hello bilgilerle eşitlenmiş tutar.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-126">hello remote monitoring preconfigured solution keeps hello device identity registry in sync with hello information in hello Cosmos DB database.</span></span> <span data-ttu-id="ba3ef-127">Her ikisi de aynı cihaz kimliği toouniquely tanımlamak hello kullan her aygıt bağlı tooyour IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-127">Both use hello same device id toouniquely identify each device connected tooyour IoT hub.</span></span>

## <a name="device-metadata"></a><span data-ttu-id="ba3ef-128">Cihaz meta veriler</span><span class="sxs-lookup"><span data-stu-id="ba3ef-128">Device metadata</span></span>

<span data-ttu-id="ba3ef-129">IOT hub'ı tutan bir [cihaz çifti] [ lnk-device-twin] tooa Uzaktan izleme çözümü her sanal ve fiziksel cihaz için bağlı.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-129">IoT Hub maintains a [device twin][lnk-device-twin] for each simulated and physical device connected tooa remote monitoring solution.</span></span> <span data-ttu-id="ba3ef-130">Merhaba çözüm cihazlarla ilişkilendirilmiş cihaz çiftlerini toomanage hello meta verilerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-130">hello solution uses device twins toomanage hello metadata associated with devices.</span></span> <span data-ttu-id="ba3ef-131">Cihaz çifti IOT Hub tarafından korunan bir JSON belgesinin ve hello çözüm hello IOT Hub API toointeract ile cihaz çiftlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-131">A device twin is a JSON document maintained by IoT Hub, and hello solution uses hello IoT Hub API toointeract with device twins.</span></span>

<span data-ttu-id="ba3ef-132">Cihaz çifti üç tür meta verileri depolar:</span><span class="sxs-lookup"><span data-stu-id="ba3ef-132">A device twin stores three types of metadata:</span></span>

- <span data-ttu-id="ba3ef-133">*Özellikler bildirilen* tooan IOT hub cihaz tarafından gönderilir.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-133">*Reported properties* are sent tooan IoT hub by a device.</span></span> <span data-ttu-id="ba3ef-134">Hello Uzaktan izleme çözümü, sanal cihazlar bildirilen özellikleri başlatma ve yanıt çok gönderme**cihaz durumunu değiştir** komutlar ve yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-134">In hello remote monitoring solution, simulated devices send reported properties at start-up and in response too**Change device state** commands and methods.</span></span> <span data-ttu-id="ba3ef-135">Hello bildirilen özelliklerini görüntüleyebilirsiniz **cihaz listesi** ve **cihaz ayrıntıları** hello çözüm Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-135">You can view reported properties in hello **Device list** and **Device details** in hello solution portal.</span></span> <span data-ttu-id="ba3ef-136">Bildirilen özellikleri salt okunurdur.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-136">Reported properties are read only.</span></span>
- <span data-ttu-id="ba3ef-137">*Özellikler istenen* hello IOT hub'ından cihazlar tarafından alınır.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-137">*Desired properties* are retrieved from hello IoT hub by devices.</span></span> <span data-ttu-id="ba3ef-138">Bunu hello tüm gerekli yapılandırma değiştirme hello aygıtta hello aygıt toomake sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-138">It is hello responsibility of hello device toomake any necessary configuration change on hello device.</span></span> <span data-ttu-id="ba3ef-139">Bu ayrıca hello hello aygıt tooreport hello değişikliği geri toohello hub'ı bildirilen bir özellik olarak sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-139">It is also hello responsibility of hello device tooreport hello change back toohello hub as a reported property.</span></span> <span data-ttu-id="ba3ef-140">İstenen özellik değeri hello çözüm portalı üzerinden ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-140">You can set a desired property value through hello solution portal.</span></span>
- <span data-ttu-id="ba3ef-141">*Etiketler* yalnızca hello cihaz çiftine mevcut ve hiçbir zaman bir aygıt ile eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-141">*Tags* only exist in hello device twin and are never synchronized with a device.</span></span> <span data-ttu-id="ba3ef-142">Merhaba çözüm portalında etiket değerleri ayarlayın ve cihazların Merhaba listesi filtre bunları kullanın.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-142">You can set tag values in hello solution portal and use them when you filter hello list of devices.</span></span> <span data-ttu-id="ba3ef-143">Merhaba çözüm bir etiket tooidentify hello simgesi toodisplay hello çözüm portalında bir aygıt için de kullanır.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-143">hello solution also uses a tag tooidentify hello icon toodisplay for a device in hello solution portal.</span></span>

<span data-ttu-id="ba3ef-144">Örnek özellikleri benzetimli hello aygıtlardan üreticisini, model numarası, enlem ve boylam dahil bildirdi.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-144">Example reported properties from hello simulated devices include manufacturer, model number, latitude, and longitude.</span></span> <span data-ttu-id="ba3ef-145">Sanal cihazlar, ayrıca bildirilen bir özellik olarak hello desteklenen yöntemlerin listesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-145">Simulated devices also return hello list of supported methods as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="ba3ef-146">Merhaba sanal cihaz kodu yalnızca hello kullanan **Desired.Config.TemperatureMeanValue** ve **Desired.Config.TelemetryInterval** istenen özellikleri tooupdate hello bildirilen geri gönderilen özellikleri tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-146">hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties sent back tooIoT Hub.</span></span> <span data-ttu-id="ba3ef-147">Diğer tüm istenen özelliği değişiklik isteklerini göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-147">All other desired property change requests are ignored.</span></span>

<span data-ttu-id="ba3ef-148">Merhaba aygıt kayıt defteri Cosmos DB veritabanında depolanan bir aygıt bilgileri meta verileri JSON belgesi yapı izlenerek hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="ba3ef-148">A device information metadata JSON document stored in hello device registry Cosmos DB database has hello following structure:</span></span>

```json
{
  "DeviceProperties": {
    "DeviceID": "deviceid1",
    "HubEnabledState": null,
    "CreatedTime": "2016-04-25T23:54:01.313802Z",
    "DeviceState": "normal",
    "UpdatedTime": null
    },
  "SystemProperties": {
    "ICCID": null
  },
  "Commands": [],
  "CommandHistory": [],
  "IsSimulatedDevice": false,
  "id": "fe81a81c-bcbc-4970-81f4-7f12f2d8bda8"
}
```

> [!NOTE]
> <span data-ttu-id="ba3ef-149">Meta veri toodescribe hello telemetri hello aygıt gönderir tooIoT Hub aygıt bilgileri de içerir.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-149">Device information can also include metadata toodescribe hello telemetry hello device sends tooIoT Hub.</span></span> <span data-ttu-id="ba3ef-150">Merhaba Uzaktan izleme çözümü kullanan nasıl hello Pano görüntüler bu telemetri meta veri toocustomize [dinamik telemetri][lnk-dynamic-telemetry].</span><span class="sxs-lookup"><span data-stu-id="ba3ef-150">hello remote monitoring solution uses this telemetry metadata toocustomize how hello dashboard displays [dynamic telemetry][lnk-dynamic-telemetry].</span></span>

## <a name="lifecycle"></a><span data-ttu-id="ba3ef-151">Yaşam döngüsü</span><span class="sxs-lookup"><span data-stu-id="ba3ef-151">Lifecycle</span></span>

<span data-ttu-id="ba3ef-152">Merhaba çözüm portalında bir cihaz ilk oluşturduğunuzda, hello çözüm hello Cosmos DB veritabanı toostore komut girişi ve yöntemi Geçmişi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-152">When you first create a device in hello solution portal, hello solution creates an entry in hello Cosmos DB database toostore command and method history.</span></span> <span data-ttu-id="ba3ef-153">Bu noktada, hello çözüm ayrıca hello aygıtı için bir giriş hello anahtarları hello aygıt kullanır tooauthenticate IOT Hub ile oluşturur hello cihaz kimlik kayıt oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-153">At this point, hello solution also creates an entry for hello device in hello device identity registry, which generates hello keys hello device uses tooauthenticate with IoT Hub.</span></span> <span data-ttu-id="ba3ef-154">Ayrıca, bir cihaz çifti oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-154">It also creates a device twin.</span></span>

<span data-ttu-id="ba3ef-155">Bir cihaz ilk toohello çözüm bağlandığında, bildirilen özellikleri ve bir cihaz bilgi iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-155">When a device first connects toohello solution, it sends reported properties and a device information message.</span></span> <span data-ttu-id="ba3ef-156">Başlangıç özellik değerlerini otomatik olarak hello cihaz çiftine kaydedilir bildirdi.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-156">hello reported property values are automatically saved in hello device twin.</span></span> <span data-ttu-id="ba3ef-157">Merhaba özellikleri hello aygıt üreticisi, model numarası, seri numarası ve desteklenen yöntemlerin listesi dahil bildirdi.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-157">hello reported properties include hello device manufacturer, model number, serial number, and a list of supported methods.</span></span> <span data-ttu-id="ba3ef-158">Hello cihaz bilgi iletisi hello komut parametreleri hakkında bilgiler dahil olmak üzere hello aygıt destekler hello komutların listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-158">hello device information message includes hello list of hello commands hello device supports including information about any command parameters.</span></span> <span data-ttu-id="ba3ef-159">Merhaba çözümü bu ileti aldığında, hello Cosmos DB veritabanındaki hello cihaz bilgilerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-159">When hello solution receives this message, it updates hello device information in hello Cosmos DB database.</span></span>

### <a name="view-and-edit-device-information-in-hello-solution-portal"></a><span data-ttu-id="ba3ef-160">Aygıt bilgileri hello çözüm portalında görüntüleyin ve düzenleyin</span><span class="sxs-lookup"><span data-stu-id="ba3ef-160">View and edit device information in hello solution portal</span></span>

<span data-ttu-id="ba3ef-161">Merhaba hello çözüm portalı aygıt listesinde görüntüler cihaz özellikleri sütunları olarak varsayılan olarak aşağıdaki hello: **durum**, **DeviceID**, **üretici**, **Model numarası**, **seri numarası**, **bellenim**, **Platform**, **İşlemci**ve  **RAM yüklü**.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-161">hello device list in hello solution portal displays hello following device properties as columns by default: **Status**, **DeviceId**, **Manufacturer**, **Model Number**, **Serial Number**, **Firmware**, **Platform**, **Processor**, and **Installed RAM**.</span></span> <span data-ttu-id="ba3ef-162">Tıklayarak hello sütunları özelleştirebilirsiniz **sütun düzenleyicisini**.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-162">You can customize hello columns by clicking **Column editor**.</span></span> <span data-ttu-id="ba3ef-163">cihaz özellikleri Hello **enlem** ve **boylam** hello Bing harita hello konumda hello Panoda sürücü.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-163">hello device properties **Latitude** and **Longitude** drive hello location in hello Bing Map on hello dashboard.</span></span>

![Aygıt listesinde sütun Düzenleyicisi][img-device-list]

<span data-ttu-id="ba3ef-165">Merhaba, **cihaz ayrıntıları** bölmesinde hello çözüm portalında, istenen özelliklerini ve etiketleri düzenleyebilirsiniz (özellikleri salt okunur bildirilen).</span><span class="sxs-lookup"><span data-stu-id="ba3ef-165">In hello **Device Details** pane in hello solution portal, you can edit desired properties and tags (reported properties are read only).</span></span>

![Cihaz ayrıntıları bölmesi][img-device-edit]

<span data-ttu-id="ba3ef-167">Merhaba çözüm portalı tooremove bir aygıtı çözümünüzden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-167">You can use hello solution portal tooremove a device from your solution.</span></span> <span data-ttu-id="ba3ef-168">Bir aygıt kaldırdığınızda, hello çözüm hello aygıt girişi kimlik kayıt defterinden kaldırır ve hello cihaz çifti siler.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-168">When you remove a device, hello solution removes hello device entry from identity registry and then deletes hello device twin.</span></span> <span data-ttu-id="ba3ef-169">Merhaba çözümü, ayrıca bilgi ilgili toohello aygıt hello Cosmos DB veritabanından kaldırır.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-169">hello solution also removes information related toohello device from hello Cosmos DB database.</span></span> <span data-ttu-id="ba3ef-170">Bir aygıt kaldırabilmeniz için önce devre dışı bırakmalısınız.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-170">Before you can remove a device, you must disable it.</span></span>

![Aygıt kaldırma][img-device-remove]

## <a name="device-information-message-processing"></a><span data-ttu-id="ba3ef-172">Cihaz bilgi iletisi işleme</span><span class="sxs-lookup"><span data-stu-id="ba3ef-172">Device information message processing</span></span>

<span data-ttu-id="ba3ef-173">Bir aygıt tarafından gönderilen cihaz bilgileri iletilerini telemetri iletilerini farklıdır.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-173">Device information messages sent by a device are distinct from telemetry messages.</span></span> <span data-ttu-id="ba3ef-174">Cihaz bilgileri iletilerini bir cihazın karşılık verebildiği hello komutları ve komut geçmişini içerir.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-174">Device information messages include hello commands a device can respond to, and any command history.</span></span> <span data-ttu-id="ba3ef-175">IOT Hub kendisini sahip bir aygıt bilgileri iletideki hello meta verileri olanağıyla ve işlemler hello hello iletisinde aynı şekilde herhangi bir cihaz bulut iletisini işler.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-175">IoT Hub itself has no knowledge of hello metadata contained in a device information message and processes hello message in hello same way it processes any device-to-cloud message.</span></span> <span data-ttu-id="ba3ef-176">Merhaba Uzaktan izleme çözümü, içinde bir [Azure akış analizi] [ lnk-stream-analytics] (ASA) işini IOT Hub'ından karışılama iletileri okur.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-176">In hello remote monitoring solution, an [Azure Stream Analytics][lnk-stream-analytics] (ASA) job reads hello messages from IoT Hub.</span></span> <span data-ttu-id="ba3ef-177">Merhaba **Deviceınfo** stream analytics iş filtreleri içeren iletileri için **"ObjectType": "Deviceınfo"** ve toohello iletir **EventProcessorHost** ana bilgisayar bir web işi çalıştıktan örneği.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-177">hello **DeviceInfo** stream analytics job filters for messages that contain **"ObjectType": "DeviceInfo"** and forwards them toohello **EventProcessorHost** host instance that runs in a web job.</span></span> <span data-ttu-id="ba3ef-178">Merhaba mantığında **EventProcessorHost** örneği hello cihaz kimliği toofind hello Cosmos DB kayıt hello belirli cihaz ve güncelleştirme hello kayıt için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-178">Logic in hello **EventProcessorHost** instance uses hello device id toofind hello Cosmos DB record for hello specific device and update hello record.</span></span>

> [!NOTE]
> <span data-ttu-id="ba3ef-179">Cihaz bilgi iletisi, bir standart cihaz bulut iletisidir.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-179">A device information message is a standard device-to-cloud message.</span></span> <span data-ttu-id="ba3ef-180">Merhaba çözüm ASA sorguları kullanarak cihaz bilgileri iletilerini ve telemetri iletilerini arasında ayırır.</span><span class="sxs-lookup"><span data-stu-id="ba3ef-180">hello solution distinguishes between device information messages and telemetry messages by using ASA queries.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba3ef-181">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ba3ef-181">Next steps</span></span>

<span data-ttu-id="ba3ef-182">Merhaba önceden yapılandırılmış çözümleri nasıl özelleştirebileceğiniz öğrenme bitirdikten sonra artık hello bazıları diğer özellikleri ve yetenekleri hello IOT paketi önceden yapılandırılmış çözümleri gözden geçirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ba3ef-182">Now you've finished learning how you can customize hello preconfigured solutions, you can explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="ba3ef-183">[Önceden yapılandırılmış Tahmine dayalı bakım çözümüne genel bakış][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="ba3ef-183">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* <span data-ttu-id="ba3ef-184">[IoT Paketi için sık sorulan sorular][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="ba3ef-184">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="ba3ef-185">[Merhaba IOT güvenlikten plan][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="ba3ef-185">[IoT security from hello ground up][lnk-security-groundup]</span></span>

<!-- Images and links -->
[img-device-list]: media/iot-suite-remote-monitoring-device-info/image1.png
[img-device-edit]: media/iot-suite-remote-monitoring-device-info/image2.png
[img-device-remove]: media/iot-suite-remote-monitoring-device-info/image3.png

[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-docdb]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-stream-analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
