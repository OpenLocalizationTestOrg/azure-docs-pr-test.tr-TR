---
title: "Uzaktan izleme çözümü cihaz bilgileri meta verilerde | Microsoft Docs"
description: "Azure IOT önceden yapılandırılmış çözümü uzaktan izlemenin ve mimarisinin açıklaması."
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
ms.openlocfilehash: f8fd452806a0a0b98cf8e434c9bd55700083a6c5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="device-information-metadata-in-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="86a5e-103">Önceden yapılandırılmış Uzaktan izleme çözümü cihaz bilgileri meta veriler</span><span class="sxs-lookup"><span data-stu-id="86a5e-103">Device information metadata in the remote monitoring preconfigured solution</span></span>

<span data-ttu-id="86a5e-104">Azure IOT paketi Uzaktan izleme çözümü cihaz meta verilerini yönetmek için bir yaklaşım gösterir.</span><span class="sxs-lookup"><span data-stu-id="86a5e-104">The Azure IoT Suite remote monitoring preconfigured solution demonstrates an approach for managing device metadata.</span></span> <span data-ttu-id="86a5e-105">Bu makalede, bu çözüm anlamak etkinleştirmeniz için gereken bir yaklaşım özetlenmektedir:</span><span class="sxs-lookup"><span data-stu-id="86a5e-105">This article outlines the approach this solution takes to enable you to understand:</span></span>

* <span data-ttu-id="86a5e-106">Çözüm hangi cihaz meta verilerini depolar.</span><span class="sxs-lookup"><span data-stu-id="86a5e-106">What device metadata the solution stores.</span></span>
* <span data-ttu-id="86a5e-107">Nasıl çözüm cihaz meta verilerini yönetir.</span><span class="sxs-lookup"><span data-stu-id="86a5e-107">How the solution manages the device metadata.</span></span>

## <a name="context"></a><span data-ttu-id="86a5e-108">Bağlam</span><span class="sxs-lookup"><span data-stu-id="86a5e-108">Context</span></span>

<span data-ttu-id="86a5e-109">Çözüm kullanan önceden yapılandırılmış Uzaktan izleme [Azure IOT Hub] [ lnk-iot-hub] aygıtlarınızı buluta veri göndermesini sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="86a5e-109">The remote monitoring preconfigured solution uses [Azure IoT Hub][lnk-iot-hub] to enable your devices to send data to the cloud.</span></span> <span data-ttu-id="86a5e-110">Çözümü üç farklı konumlarda cihazlarla ilgili bilgileri depolar:</span><span class="sxs-lookup"><span data-stu-id="86a5e-110">The solution stores information about devices in three different locations:</span></span>

| <span data-ttu-id="86a5e-111">Konum</span><span class="sxs-lookup"><span data-stu-id="86a5e-111">Location</span></span> | <span data-ttu-id="86a5e-112">Depolanan bilgileri</span><span class="sxs-lookup"><span data-stu-id="86a5e-112">Information stored</span></span> | <span data-ttu-id="86a5e-113">Uygulama</span><span class="sxs-lookup"><span data-stu-id="86a5e-113">Implementation</span></span> |
| -------- | ------------------ | -------------- |
| <span data-ttu-id="86a5e-114">Kimlik kayıt defteri</span><span class="sxs-lookup"><span data-stu-id="86a5e-114">Identity registry</span></span> | <span data-ttu-id="86a5e-115">Cihaz kimliği, kimlik doğrulaması anahtarları, durumu etkin</span><span class="sxs-lookup"><span data-stu-id="86a5e-115">Device id, authentication keys, enabled state</span></span> | <span data-ttu-id="86a5e-116">IOT Hub'ına yerleşik</span><span class="sxs-lookup"><span data-stu-id="86a5e-116">Built in to IoT Hub</span></span> |
| <span data-ttu-id="86a5e-117">Cihaz çiftlerini</span><span class="sxs-lookup"><span data-stu-id="86a5e-117">Device twins</span></span> | <span data-ttu-id="86a5e-118">Meta veriler: bildirilen özellikleri, istenen özellikleri, etiketler</span><span class="sxs-lookup"><span data-stu-id="86a5e-118">Metadata: reported properties, desired properties, tags</span></span> | <span data-ttu-id="86a5e-119">IOT Hub'ına yerleşik</span><span class="sxs-lookup"><span data-stu-id="86a5e-119">Built in to IoT Hub</span></span> |
| <span data-ttu-id="86a5e-120">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="86a5e-120">Cosmos DB</span></span> | <span data-ttu-id="86a5e-121">Komut ve yöntemi geçmişi</span><span class="sxs-lookup"><span data-stu-id="86a5e-121">Command and method history</span></span> | <span data-ttu-id="86a5e-122">Özel çözüm için</span><span class="sxs-lookup"><span data-stu-id="86a5e-122">Custom for solution</span></span> |

<span data-ttu-id="86a5e-123">IOT hub'ında bir [cihaz kimlik kayıt defteri] [ lnk-identity-registry] IOT hub'ı ve kullanım erişimini yönetmek için [cihaz çiftlerini] [ lnk-device-twin] cihaz meta verilerini yönetmek için.</span><span class="sxs-lookup"><span data-stu-id="86a5e-123">IoT Hub includes a [device identity registry][lnk-identity-registry] to manage access to an IoT hub and uses [device twins][lnk-device-twin] to manage device metadata.</span></span> <span data-ttu-id="86a5e-124">Ayrıca bir uzaktan izleme çözümü özgü olan *cihaz kayıt defteri* komutu ve yöntemi geçmişini saklar.</span><span class="sxs-lookup"><span data-stu-id="86a5e-124">There is also a remote monitoring solution-specific *device registry* that stores command and method history.</span></span> <span data-ttu-id="86a5e-125">Uzaktan izleme çözümü kullanan bir [Cosmos DB] [ lnk-docdb] komut ve yöntemi geçmişi için özel bir depo uygulamak için veritabanı.</span><span class="sxs-lookup"><span data-stu-id="86a5e-125">The remote monitoring solution uses a [Cosmos DB][lnk-docdb] database to implement a custom store for command and method history.</span></span>

> [!NOTE]
> <span data-ttu-id="86a5e-126">Önceden yapılandırılmış Uzaktan izleme çözümü cihaz kimlik kayıt defteri Cosmos DB veritabanında bilgilerle eşitlenmiş tutar.</span><span class="sxs-lookup"><span data-stu-id="86a5e-126">The remote monitoring preconfigured solution keeps the device identity registry in sync with the information in the Cosmos DB database.</span></span> <span data-ttu-id="86a5e-127">Her ikisi de aynı cihaz kimliği IOT hub'ına bağlı her cihazın benzersiz şekilde tanımlamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="86a5e-127">Both use the same device id to uniquely identify each device connected to your IoT hub.</span></span>

## <a name="device-metadata"></a><span data-ttu-id="86a5e-128">Cihaz meta veriler</span><span class="sxs-lookup"><span data-stu-id="86a5e-128">Device metadata</span></span>

<span data-ttu-id="86a5e-129">IOT hub'ı tutan bir [cihaz çifti] [ lnk-device-twin] her sanal ve fiziksel cihaz için bir uzaktan izleme çözümüne bağlı.</span><span class="sxs-lookup"><span data-stu-id="86a5e-129">IoT Hub maintains a [device twin][lnk-device-twin] for each simulated and physical device connected to a remote monitoring solution.</span></span> <span data-ttu-id="86a5e-130">Çözüm, aygıtlar ile ilişkili meta verileri yönetmek için cihaz çiftlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="86a5e-130">The solution uses device twins to manage the metadata associated with devices.</span></span> <span data-ttu-id="86a5e-131">Cihaz çifti IOT Hub tarafından korunan bir JSON belgesinin ve çözüm cihaz çiftlerini ile etkileşim kurmak için IOT Hub API kullanır.</span><span class="sxs-lookup"><span data-stu-id="86a5e-131">A device twin is a JSON document maintained by IoT Hub, and the solution uses the IoT Hub API to interact with device twins.</span></span>

<span data-ttu-id="86a5e-132">Cihaz çifti üç tür meta verileri depolar:</span><span class="sxs-lookup"><span data-stu-id="86a5e-132">A device twin stores three types of metadata:</span></span>

- <span data-ttu-id="86a5e-133">*Özellikler bildirilen* IOT hub'a bir cihaz tarafından gönderilir.</span><span class="sxs-lookup"><span data-stu-id="86a5e-133">*Reported properties* are sent to an IoT hub by a device.</span></span> <span data-ttu-id="86a5e-134">Uzaktan izleme çözümünde başlatma ve yanıt olarak bildirilen özellikleri sanal cihazlar Gönder **cihaz durumunu değiştir** komutlar ve yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="86a5e-134">In the remote monitoring solution, simulated devices send reported properties at start-up and in response to **Change device state** commands and methods.</span></span> <span data-ttu-id="86a5e-135">Bildirilen özelliklerinde görüntüleyebilirsiniz **cihaz listesi** ve **cihaz ayrıntıları** çözüm Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="86a5e-135">You can view reported properties in the **Device list** and **Device details** in the solution portal.</span></span> <span data-ttu-id="86a5e-136">Bildirilen özellikleri salt okunurdur.</span><span class="sxs-lookup"><span data-stu-id="86a5e-136">Reported properties are read only.</span></span>
- <span data-ttu-id="86a5e-137">*Özellikler istenen* IOT hub'ından cihazlar tarafından alınır.</span><span class="sxs-lookup"><span data-stu-id="86a5e-137">*Desired properties* are retrieved from the IoT hub by devices.</span></span> <span data-ttu-id="86a5e-138">Tüm gerekli yapılandırma cihazda değişikliği yapmak için cihaz sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="86a5e-138">It is the responsibility of the device to make any necessary configuration change on the device.</span></span> <span data-ttu-id="86a5e-139">Bu ayrıca değişikliği geri hub'ı bildirilen bir özellik olarak rapor aygıta sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="86a5e-139">It is also the responsibility of the device to report the change back to the hub as a reported property.</span></span> <span data-ttu-id="86a5e-140">İstenen özellik değeri çözüm Portalı aracılığıyla ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86a5e-140">You can set a desired property value through the solution portal.</span></span>
- <span data-ttu-id="86a5e-141">*Etiketler* yalnızca cihaz çiftine mevcut ve hiçbir zaman bir aygıt ile eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="86a5e-141">*Tags* only exist in the device twin and are never synchronized with a device.</span></span> <span data-ttu-id="86a5e-142">Çözüm portalında etiket değerleri ayarlamak ve cihaz listesini filtre bunları kullanın.</span><span class="sxs-lookup"><span data-stu-id="86a5e-142">You can set tag values in the solution portal and use them when you filter the list of devices.</span></span> <span data-ttu-id="86a5e-143">Çözüm bir etiket çözüm portalında bir aygıt için görüntülemek için bu simgeyi tanımlamak için de kullanır.</span><span class="sxs-lookup"><span data-stu-id="86a5e-143">The solution also uses a tag to identify the icon to display for a device in the solution portal.</span></span>

<span data-ttu-id="86a5e-144">Sanal cihazlar özelliklerinden üreticisini, model numarası, enlem ve boylam dahil örnek bildirdi.</span><span class="sxs-lookup"><span data-stu-id="86a5e-144">Example reported properties from the simulated devices include manufacturer, model number, latitude, and longitude.</span></span> <span data-ttu-id="86a5e-145">Sanal cihazlar, ayrıca bildirilen bir özellik olarak desteklenen yöntemlerin listesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="86a5e-145">Simulated devices also return the list of supported methods as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="86a5e-146">Sanal cihaz kodu, IoT Hub’ına geri gönderilen bildirilen özellikleri güncelleştirmek üzere yalnızca istenen **Desired.Config.TemperatureMeanValue** ve **Desired.Config.TelemetryInterval** özelliklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="86a5e-146">The simulated device code only uses the **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties to update the reported properties sent back to IoT Hub.</span></span> <span data-ttu-id="86a5e-147">Diğer tüm istenen özelliği değişiklik isteklerini göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="86a5e-147">All other desired property change requests are ignored.</span></span>

<span data-ttu-id="86a5e-148">Cihaz kayıt defteri Cosmos DB veritabanında depolanan bir aygıt bilgileri meta verileri JSON belgesi aşağıdaki yapıya sahiptir:</span><span class="sxs-lookup"><span data-stu-id="86a5e-148">A device information metadata JSON document stored in the device registry Cosmos DB database has the following structure:</span></span>

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
> <span data-ttu-id="86a5e-149">Aygıt bilgileri aygıt IOT Hub'ına gönderir telemetri açıklamak için meta verileri de içerir.</span><span class="sxs-lookup"><span data-stu-id="86a5e-149">Device information can also include metadata to describe the telemetry the device sends to IoT Hub.</span></span> <span data-ttu-id="86a5e-150">Uzaktan izleme çözümü, Pano biçimini özelleştirmek için bu telemetri meta veri kullanan [dinamik telemetri][lnk-dynamic-telemetry].</span><span class="sxs-lookup"><span data-stu-id="86a5e-150">The remote monitoring solution uses this telemetry metadata to customize how the dashboard displays [dynamic telemetry][lnk-dynamic-telemetry].</span></span>

## <a name="lifecycle"></a><span data-ttu-id="86a5e-151">Yaşam döngüsü</span><span class="sxs-lookup"><span data-stu-id="86a5e-151">Lifecycle</span></span>

<span data-ttu-id="86a5e-152">Çözüm Portalı'nda bir cihaz ilk oluşturduğunuzda, çözüm komut ve yöntemi geçmişini depolamak için Cosmos DB veritabanında bir giriş oluşturur.</span><span class="sxs-lookup"><span data-stu-id="86a5e-152">When you first create a device in the solution portal, the solution creates an entry in the Cosmos DB database to store command and method history.</span></span> <span data-ttu-id="86a5e-153">Bu noktada, çözüm Ayrıca aygıtı için bir giriş aygıtın IOT Hub ile kimlik doğrulaması için kullandığı anahtarları oluşturur cihaz kimliği kayıt oluşturur.</span><span class="sxs-lookup"><span data-stu-id="86a5e-153">At this point, the solution also creates an entry for the device in the device identity registry, which generates the keys the device uses to authenticate with IoT Hub.</span></span> <span data-ttu-id="86a5e-154">Ayrıca, bir cihaz çifti oluşturur.</span><span class="sxs-lookup"><span data-stu-id="86a5e-154">It also creates a device twin.</span></span>

<span data-ttu-id="86a5e-155">Bir cihaz ilk çözüme bağlandığında, bildirilen özellikleri ve bir cihaz bilgi iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="86a5e-155">When a device first connects to the solution, it sends reported properties and a device information message.</span></span> <span data-ttu-id="86a5e-156">Bildirilen özellik değerlerini otomatik olarak cihaz çiftine kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="86a5e-156">The reported property values are automatically saved in the device twin.</span></span> <span data-ttu-id="86a5e-157">Bildirilen özellikleri aygıt üreticisi, model numarası, seri numarası ve desteklenen yöntemlerin listesi içerir.</span><span class="sxs-lookup"><span data-stu-id="86a5e-157">The reported properties include the device manufacturer, model number, serial number, and a list of supported methods.</span></span> <span data-ttu-id="86a5e-158">Cihaz bilgi iletisi komut parametreleri hakkında bilgiler dahil olmak üzere cihaz destekler komutların listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="86a5e-158">The device information message includes the list of the commands the device supports including information about any command parameters.</span></span> <span data-ttu-id="86a5e-159">Bu iletiyi çözümünün aldığında, aygıt bilgileri Cosmos DB veritabanında güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="86a5e-159">When the solution receives this message, it updates the device information in the Cosmos DB database.</span></span>

### <a name="view-and-edit-device-information-in-the-solution-portal"></a><span data-ttu-id="86a5e-160">Çözüm portalında aygıt bilgileri görüntüleyin ve düzenleyin</span><span class="sxs-lookup"><span data-stu-id="86a5e-160">View and edit device information in the solution portal</span></span>

<span data-ttu-id="86a5e-161">Çözüm portalı aygıt listesinde aşağıdaki cihaz özelliklerini sütunları olarak varsayılan olarak görüntüler: **durum**, **DeviceID**, **üretici**, **modeli Sayı**, **seri numarası**, **bellenim**, **Platform**, **İşlemci**, ve  **RAM yüklü**.</span><span class="sxs-lookup"><span data-stu-id="86a5e-161">The device list in the solution portal displays the following device properties as columns by default: **Status**, **DeviceId**, **Manufacturer**, **Model Number**, **Serial Number**, **Firmware**, **Platform**, **Processor**, and **Installed RAM**.</span></span> <span data-ttu-id="86a5e-162">Tıklayarak sütunları özelleştirebilirsiniz **sütun düzenleyicisini**.</span><span class="sxs-lookup"><span data-stu-id="86a5e-162">You can customize the columns by clicking **Column editor**.</span></span> <span data-ttu-id="86a5e-163">Cihaz özellikleri **enlem** ve **boylam** Bing harita konumda Panoda sürücü.</span><span class="sxs-lookup"><span data-stu-id="86a5e-163">The device properties **Latitude** and **Longitude** drive the location in the Bing Map on the dashboard.</span></span>

![Aygıt listesinde sütun Düzenleyicisi][img-device-list]

<span data-ttu-id="86a5e-165">İçinde **cihaz ayrıntıları** bölmesi çözüm Portalı'nda, istenen özelliklerini ve etiketleri düzenleyebilirsiniz (özellikleri salt okunur bildirilen).</span><span class="sxs-lookup"><span data-stu-id="86a5e-165">In the **Device Details** pane in the solution portal, you can edit desired properties and tags (reported properties are read only).</span></span>

![Cihaz ayrıntıları bölmesi][img-device-edit]

<span data-ttu-id="86a5e-167">Bir aygıtı çözümünüzden kaldırmak için çözüm Portalı'nı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86a5e-167">You can use the solution portal to remove a device from your solution.</span></span> <span data-ttu-id="86a5e-168">Bir aygıt kaldırdığınızda, çözüm aygıt girişi kimlik kayıt defterinden kaldırır ve cihaz çifti siler.</span><span class="sxs-lookup"><span data-stu-id="86a5e-168">When you remove a device, the solution removes the device entry from identity registry and then deletes the device twin.</span></span> <span data-ttu-id="86a5e-169">Çözüm Cosmos DB veritabanından cihaza ilgili bilgileri de kaldırır.</span><span class="sxs-lookup"><span data-stu-id="86a5e-169">The solution also removes information related to the device from the Cosmos DB database.</span></span> <span data-ttu-id="86a5e-170">Bir aygıt kaldırabilmeniz için önce devre dışı bırakmalısınız.</span><span class="sxs-lookup"><span data-stu-id="86a5e-170">Before you can remove a device, you must disable it.</span></span>

![Aygıt kaldırma][img-device-remove]

## <a name="device-information-message-processing"></a><span data-ttu-id="86a5e-172">Cihaz bilgi iletisi işleme</span><span class="sxs-lookup"><span data-stu-id="86a5e-172">Device information message processing</span></span>

<span data-ttu-id="86a5e-173">Bir aygıt tarafından gönderilen cihaz bilgileri iletilerini telemetri iletilerini farklıdır.</span><span class="sxs-lookup"><span data-stu-id="86a5e-173">Device information messages sent by a device are distinct from telemetry messages.</span></span> <span data-ttu-id="86a5e-174">Cihaz bilgileri iletilerini bir aygıtı yanıt verebileceği komutları ve komut geçmişini içerir.</span><span class="sxs-lookup"><span data-stu-id="86a5e-174">Device information messages include the commands a device can respond to, and any command history.</span></span> <span data-ttu-id="86a5e-175">IOT Hub kendisini bir cihaz bilgi iletisi bulunan meta veriler olanağıyla sahiptir ve iletiyi herhangi bir cihaz bulut iletisini işler aynı şekilde işler.</span><span class="sxs-lookup"><span data-stu-id="86a5e-175">IoT Hub itself has no knowledge of the metadata contained in a device information message and processes the message in the same way it processes any device-to-cloud message.</span></span> <span data-ttu-id="86a5e-176">Uzaktan izleme çözümünde bir [Azure akış analizi] [ lnk-stream-analytics] (ASA) işini IOT Hub'ından iletileri okur.</span><span class="sxs-lookup"><span data-stu-id="86a5e-176">In the remote monitoring solution, an [Azure Stream Analytics][lnk-stream-analytics] (ASA) job reads the messages from IoT Hub.</span></span> <span data-ttu-id="86a5e-177">**Deviceınfo** stream analytics iş filtreleri içeren iletileri için **"ObjectType": "Deviceınfo"** ve bunlara iletir **EventProcessorHost** ana bilgisayar örneği bir web işi çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="86a5e-177">The **DeviceInfo** stream analytics job filters for messages that contain **"ObjectType": "DeviceInfo"** and forwards them to the **EventProcessorHost** host instance that runs in a web job.</span></span> <span data-ttu-id="86a5e-178">Mantık **EventProcessorHost** örneği için belirli bir aygıtı Cosmos DB kayıt bulmak ve kaydı güncelleştirmek için cihaz kimliği kullanır.</span><span class="sxs-lookup"><span data-stu-id="86a5e-178">Logic in the **EventProcessorHost** instance uses the device id to find the Cosmos DB record for the specific device and update the record.</span></span>

> [!NOTE]
> <span data-ttu-id="86a5e-179">Cihaz bilgi iletisi, bir standart cihaz bulut iletisidir.</span><span class="sxs-lookup"><span data-stu-id="86a5e-179">A device information message is a standard device-to-cloud message.</span></span> <span data-ttu-id="86a5e-180">Çözüm, ASA sorguları kullanarak cihaz bilgileri iletilerini ve telemetri iletilerini arasında ayırır.</span><span class="sxs-lookup"><span data-stu-id="86a5e-180">The solution distinguishes between device information messages and telemetry messages by using ASA queries.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86a5e-181">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="86a5e-181">Next steps</span></span>

<span data-ttu-id="86a5e-182">Önceden yapılandırılmış çözümler nasıl özelleştirebileceğiniz öğrenme bitirdikten sonra artık, bazı diğer özellikler ve yetenekler IOT paketi önceden yapılandırılmış çözümleri gözden geçirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="86a5e-182">Now you've finished learning how you can customize the preconfigured solutions, you can explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="86a5e-183">[Önceden yapılandırılmış Tahmine dayalı bakım çözümüne genel bakış][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="86a5e-183">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* <span data-ttu-id="86a5e-184">[IoT Paketi için sık sorulan sorular][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="86a5e-184">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="86a5e-185">[Baştan sona IoT güvenliği][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="86a5e-185">[IoT security from the ground up][lnk-security-groundup]</span></span>

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
