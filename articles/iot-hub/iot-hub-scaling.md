---
title: "Azure IOT Hub ile ölçeklendirme | Microsoft Docs"
description: "Beklenen ileti işleme desteklemek için IOT hub'ını ölçeklendirmek nasıl. Her katman için desteklenen işleme ve parçalama seçeneklerini özetini içerir."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: e7bd4968-db46-46cf-865d-9c944f683832
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2cb263103da05b10c24aab71d81c43eb25987565
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="scale-your-iot-hub-solution"></a><span data-ttu-id="bc5cb-104">IOT hub çözümünüzü ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="bc5cb-104">Scale your IoT hub solution</span></span>
<span data-ttu-id="bc5cb-105">Azure IOT Hub, en çok bir milyon eş zamanlı cihazı destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="bc5cb-105">Azure IoT Hub can support up to a million simultaneously connected devices.</span></span> <span data-ttu-id="bc5cb-106">Daha fazla bilgi için bkz: [IOT Hub'ın fiyatlandırma][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="bc5cb-106">For more information, see [IoT Hub pricing][lnk-pricing].</span></span> <span data-ttu-id="bc5cb-107">Her IOT hub'ı birimi belirli sayıda günlük iletileri izin verir.</span><span class="sxs-lookup"><span data-stu-id="bc5cb-107">Each IoT Hub unit allows a certain number of daily messages.</span></span>

<span data-ttu-id="bc5cb-108">Çözümünüzü düzgün ölçeklendirmek için belirli IOT hub'ı kullanımınızı göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="bc5cb-108">To properly scale your solution, consider your particular use of IoT Hub.</span></span> <span data-ttu-id="bc5cb-109">Özellikle, gerekli en yüksek verimlilik işlemlerinin Aşağıdaki kategorilerde göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="bc5cb-109">In particular, consider the required peak throughput for the following categories of operations:</span></span>

* <span data-ttu-id="bc5cb-110">Cihazdan buluta iletiler</span><span class="sxs-lookup"><span data-stu-id="bc5cb-110">Device-to-cloud messages</span></span>
* <span data-ttu-id="bc5cb-111">Bulut-cihaz iletilerini</span><span class="sxs-lookup"><span data-stu-id="bc5cb-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="bc5cb-112">Kimlik kayıt defteri işlemleri</span><span class="sxs-lookup"><span data-stu-id="bc5cb-112">Identity registry operations</span></span>

<span data-ttu-id="bc5cb-113">Bu işleme ek bilgi [IOT hub'ı kotaları ve kısıtlamaları] [ IoT Hub quotas and throttles] ve çözümünüzün uygun şekilde tasarlayın.</span><span class="sxs-lookup"><span data-stu-id="bc5cb-113">In addition to this throughput information, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles] and design your solution accordingly.</span></span>

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a><span data-ttu-id="bc5cb-114">Cihaz Bulut ve bulut-cihaz ileti işleme</span><span class="sxs-lookup"><span data-stu-id="bc5cb-114">Device-to-cloud and cloud-to-device message throughput</span></span>
<span data-ttu-id="bc5cb-115">IOT hub'ı çözümünü boyutu için en iyi birim başına temelinde trafiği değerlendirmek için yoludur.</span><span class="sxs-lookup"><span data-stu-id="bc5cb-115">The best way to size an IoT Hub solution is to evaluate the traffic on a per-unit basis.</span></span>

<span data-ttu-id="bc5cb-116">Cihaz bulut iletilerini bu aralıksız üretilen yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="bc5cb-116">Device-to-cloud messages follow these sustained throughput guidelines.</span></span>

| <span data-ttu-id="bc5cb-117">Katman</span><span class="sxs-lookup"><span data-stu-id="bc5cb-117">Tier</span></span> | <span data-ttu-id="bc5cb-118">Aralıksız üretilen</span><span class="sxs-lookup"><span data-stu-id="bc5cb-118">Sustained throughput</span></span> | <span data-ttu-id="bc5cb-119">Sürdürülen gönderme oranı</span><span class="sxs-lookup"><span data-stu-id="bc5cb-119">Sustained send rate</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc5cb-120">S1</span><span class="sxs-lookup"><span data-stu-id="bc5cb-120">S1</span></span> |<span data-ttu-id="bc5cb-121">Birim başına 1111 KB/dakika kadar</span><span class="sxs-lookup"><span data-stu-id="bc5cb-121">Up to 1111 KB/minute per unit</span></span><br/><span data-ttu-id="bc5cb-122">(1,5 GB/gün/birim)</span><span class="sxs-lookup"><span data-stu-id="bc5cb-122">(1.5 GB/day/unit)</span></span> |<span data-ttu-id="bc5cb-123">278 iletileri dakikada birim başına ortalama</span><span class="sxs-lookup"><span data-stu-id="bc5cb-123">Average of 278 messages/minute per unit</span></span><br/><span data-ttu-id="bc5cb-124">(400.000 iletileri/gün birim başına)</span><span class="sxs-lookup"><span data-stu-id="bc5cb-124">(400,000 messages/day per unit)</span></span> |
| <span data-ttu-id="bc5cb-125">S2</span><span class="sxs-lookup"><span data-stu-id="bc5cb-125">S2</span></span> |<span data-ttu-id="bc5cb-126">Birim başına 16 MB/dakika kadar</span><span class="sxs-lookup"><span data-stu-id="bc5cb-126">Up to 16 MB/minute per unit</span></span><br/><span data-ttu-id="bc5cb-127">(22.8 GB/gün/birim)</span><span class="sxs-lookup"><span data-stu-id="bc5cb-127">(22.8 GB/day/unit)</span></span> |<span data-ttu-id="bc5cb-128">4,167 iletileri dakikada birim başına ortalama</span><span class="sxs-lookup"><span data-stu-id="bc5cb-128">Average of 4,167 messages/minute per unit</span></span><br/><span data-ttu-id="bc5cb-129">(6 milyon iletileri/gün birim başına)</span><span class="sxs-lookup"><span data-stu-id="bc5cb-129">(6 million messages/day per unit)</span></span> |
| <span data-ttu-id="bc5cb-130">S3</span><span class="sxs-lookup"><span data-stu-id="bc5cb-130">S3</span></span> |<span data-ttu-id="bc5cb-131">Birim başına 814 MB/dakika kadar</span><span class="sxs-lookup"><span data-stu-id="bc5cb-131">Up to 814 MB/minute per unit</span></span><br/><span data-ttu-id="bc5cb-132">(1144.4 GB/gün/birim)</span><span class="sxs-lookup"><span data-stu-id="bc5cb-132">(1144.4 GB/day/unit)</span></span> |<span data-ttu-id="bc5cb-133">208,333 iletileri dakikada birim başına ortalama</span><span class="sxs-lookup"><span data-stu-id="bc5cb-133">Average of 208,333 messages/minute per unit</span></span><br/><span data-ttu-id="bc5cb-134">(300 milyon iletileri/gün birim başına)</span><span class="sxs-lookup"><span data-stu-id="bc5cb-134">(300 million messages/day per unit)</span></span> |

## <a name="identity-registry-operation-throughput"></a><span data-ttu-id="bc5cb-135">Kimlik kayıt defteri işlemi işleme</span><span class="sxs-lookup"><span data-stu-id="bc5cb-135">Identity registry operation throughput</span></span>
<span data-ttu-id="bc5cb-136">Cihaz sağlamak için çoğunlukla ilişkili oldukları gibi IOT Hub kimlik kayıt defteri işlemlerini çalıştırma işlemleri olması gereken değil.</span><span class="sxs-lookup"><span data-stu-id="bc5cb-136">IoT Hub identity registry operations are not supposed to be run-time operations, as they are mostly related to device provisioning.</span></span>

<span data-ttu-id="bc5cb-137">Belirli veri bloğu performans numaraları için bkz: [IOT hub'ı kotaları ve kısıtlamaları][IoT Hub quotas and throttles].</span><span class="sxs-lookup"><span data-stu-id="bc5cb-137">For specific burst performance numbers, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles].</span></span>

## <a name="sharding"></a><span data-ttu-id="bc5cb-138">Parçalama</span><span class="sxs-lookup"><span data-stu-id="bc5cb-138">Sharding</span></span>
<span data-ttu-id="bc5cb-139">Bazen tek bir IOT hub, milyonlarca cihaza için ölçeklendirebilirsiniz olmakla birlikte, çözümünüzü tek bir IOT hub garanti edemez özel performans özellikleri gerektirir.</span><span class="sxs-lookup"><span data-stu-id="bc5cb-139">While a single IoT hub can scale to millions of devices, sometimes your solution requires specific performance characteristics that a single IoT hub cannot guarantee.</span></span> <span data-ttu-id="bc5cb-140">Bu durumda, birden çok IOT hub'ları aygıtlarınızı bölüm önerilir.</span><span class="sxs-lookup"><span data-stu-id="bc5cb-140">In that case, it is recommended that you partition your devices into multiple IoT hubs.</span></span> <span data-ttu-id="bc5cb-141">Birden çok IOT hub'ları trafiği WINS'e kesintisiz ve gerekli işlem hızları ve gerekli verimlilik elde edin.</span><span class="sxs-lookup"><span data-stu-id="bc5cb-141">Multiple IoT hubs smooth traffic bursts and obtain the required throughput or operation rates that are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc5cb-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bc5cb-142">Next steps</span></span>
<span data-ttu-id="bc5cb-143">Daha fazla IOT hub'ı özelliklerini keşfetmek için bkz:</span><span class="sxs-lookup"><span data-stu-id="bc5cb-143">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="bc5cb-144">[IOT Hub Geliştirici Kılavuzu][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="bc5cb-144">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="bc5cb-145">[Bir aygıt ile Azure IOT kenar benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="bc5cb-145">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
