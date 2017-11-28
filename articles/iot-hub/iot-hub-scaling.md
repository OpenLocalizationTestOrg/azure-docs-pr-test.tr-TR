---
title: "IOT hub'ı aaaAzure ölçeklendirme | Microsoft Docs"
description: "Nasıl tooscale IOT hub toosupport beklenen ileti işleme. Her katman için desteklenen hello verimliliği ve parçalama seçeneklerini özetini içerir."
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
ms.openlocfilehash: 3b8bf6c44631c65b34b69752d9043c21db24bb01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-iot-hub-solution"></a><span data-ttu-id="5530f-104">IOT hub çözümünüzü ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="5530f-104">Scale your IoT hub solution</span></span>
<span data-ttu-id="5530f-105">Azure IOT Hub tooa milyon aynı anda bağlı cihazları destekler.</span><span class="sxs-lookup"><span data-stu-id="5530f-105">Azure IoT Hub can support up tooa million simultaneously connected devices.</span></span> <span data-ttu-id="5530f-106">Daha fazla bilgi için bkz: [IOT Hub'ın fiyatlandırma][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="5530f-106">For more information, see [IoT Hub pricing][lnk-pricing].</span></span> <span data-ttu-id="5530f-107">Her IOT hub'ı birimi belirli sayıda günlük iletileri izin verir.</span><span class="sxs-lookup"><span data-stu-id="5530f-107">Each IoT Hub unit allows a certain number of daily messages.</span></span>

<span data-ttu-id="5530f-108">tooproperly çözümünüzü ölçeklendirme, belirli IOT hub'ı kullanımınızı göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="5530f-108">tooproperly scale your solution, consider your particular use of IoT Hub.</span></span> <span data-ttu-id="5530f-109">Özellikle, kategoriler işlemlerinin aşağıdaki hello için gerekli hello en yüksek işleme göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="5530f-109">In particular, consider hello required peak throughput for hello following categories of operations:</span></span>

* <span data-ttu-id="5530f-110">Cihazdan buluta iletiler</span><span class="sxs-lookup"><span data-stu-id="5530f-110">Device-to-cloud messages</span></span>
* <span data-ttu-id="5530f-111">Bulut-cihaz iletilerini</span><span class="sxs-lookup"><span data-stu-id="5530f-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="5530f-112">Kimlik kayıt defteri işlemleri</span><span class="sxs-lookup"><span data-stu-id="5530f-112">Identity registry operations</span></span>

<span data-ttu-id="5530f-113">Toplama toothis üretilen iş bilgilerine bakın [IOT hub'ı kotaları ve kısıtlamaları] [ IoT Hub quotas and throttles] ve çözümünüzün uygun şekilde tasarlayın.</span><span class="sxs-lookup"><span data-stu-id="5530f-113">In addition toothis throughput information, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles] and design your solution accordingly.</span></span>

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a><span data-ttu-id="5530f-114">Cihaz Bulut ve bulut-cihaz ileti işleme</span><span class="sxs-lookup"><span data-stu-id="5530f-114">Device-to-cloud and cloud-to-device message throughput</span></span>
<span data-ttu-id="5530f-115">Merhaba en iyi şekilde toosize IOT hub'ı çözümünü tooevaluate hello birim başına temelinde trafiğidir.</span><span class="sxs-lookup"><span data-stu-id="5530f-115">hello best way toosize an IoT Hub solution is tooevaluate hello traffic on a per-unit basis.</span></span>

<span data-ttu-id="5530f-116">Cihaz bulut iletilerini bu aralıksız üretilen yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="5530f-116">Device-to-cloud messages follow these sustained throughput guidelines.</span></span>

| <span data-ttu-id="5530f-117">Katman</span><span class="sxs-lookup"><span data-stu-id="5530f-117">Tier</span></span> | <span data-ttu-id="5530f-118">Aralıksız üretilen</span><span class="sxs-lookup"><span data-stu-id="5530f-118">Sustained throughput</span></span> | <span data-ttu-id="5530f-119">Sürdürülen gönderme oranı</span><span class="sxs-lookup"><span data-stu-id="5530f-119">Sustained send rate</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5530f-120">S1</span><span class="sxs-lookup"><span data-stu-id="5530f-120">S1</span></span> |<span data-ttu-id="5530f-121">Too1111 KB dakikada birim başına</span><span class="sxs-lookup"><span data-stu-id="5530f-121">Up too1111 KB/minute per unit</span></span><br/><span data-ttu-id="5530f-122">(1,5 GB/gün/birim)</span><span class="sxs-lookup"><span data-stu-id="5530f-122">(1.5 GB/day/unit)</span></span> |<span data-ttu-id="5530f-123">278 iletileri dakikada birim başına ortalama</span><span class="sxs-lookup"><span data-stu-id="5530f-123">Average of 278 messages/minute per unit</span></span><br/><span data-ttu-id="5530f-124">(400.000 iletileri/gün birim başına)</span><span class="sxs-lookup"><span data-stu-id="5530f-124">(400,000 messages/day per unit)</span></span> |
| <span data-ttu-id="5530f-125">S2</span><span class="sxs-lookup"><span data-stu-id="5530f-125">S2</span></span> |<span data-ttu-id="5530f-126">Too16 MB dakikada birim başına</span><span class="sxs-lookup"><span data-stu-id="5530f-126">Up too16 MB/minute per unit</span></span><br/><span data-ttu-id="5530f-127">(22.8 GB/gün/birim)</span><span class="sxs-lookup"><span data-stu-id="5530f-127">(22.8 GB/day/unit)</span></span> |<span data-ttu-id="5530f-128">4,167 iletileri dakikada birim başına ortalama</span><span class="sxs-lookup"><span data-stu-id="5530f-128">Average of 4,167 messages/minute per unit</span></span><br/><span data-ttu-id="5530f-129">(6 milyon iletileri/gün birim başına)</span><span class="sxs-lookup"><span data-stu-id="5530f-129">(6 million messages/day per unit)</span></span> |
| <span data-ttu-id="5530f-130">S3</span><span class="sxs-lookup"><span data-stu-id="5530f-130">S3</span></span> |<span data-ttu-id="5530f-131">Too814 MB dakikada birim başına</span><span class="sxs-lookup"><span data-stu-id="5530f-131">Up too814 MB/minute per unit</span></span><br/><span data-ttu-id="5530f-132">(1144.4 GB/gün/birim)</span><span class="sxs-lookup"><span data-stu-id="5530f-132">(1144.4 GB/day/unit)</span></span> |<span data-ttu-id="5530f-133">208,333 iletileri dakikada birim başına ortalama</span><span class="sxs-lookup"><span data-stu-id="5530f-133">Average of 208,333 messages/minute per unit</span></span><br/><span data-ttu-id="5530f-134">(300 milyon iletileri/gün birim başına)</span><span class="sxs-lookup"><span data-stu-id="5530f-134">(300 million messages/day per unit)</span></span> |

## <a name="identity-registry-operation-throughput"></a><span data-ttu-id="5530f-135">Kimlik kayıt defteri işlemi işleme</span><span class="sxs-lookup"><span data-stu-id="5530f-135">Identity registry operation throughput</span></span>
<span data-ttu-id="5530f-136">Bunlar çoğunlukla ilgili toodevice sağlama olduğu IOT Hub kimlik kayıt defteri işlemlerini toobe çalıştırma işlemleri, beklenen değil.</span><span class="sxs-lookup"><span data-stu-id="5530f-136">IoT Hub identity registry operations are not supposed toobe run-time operations, as they are mostly related toodevice provisioning.</span></span>

<span data-ttu-id="5530f-137">Belirli veri bloğu performans numaraları için bkz: [IOT hub'ı kotaları ve kısıtlamaları][IoT Hub quotas and throttles].</span><span class="sxs-lookup"><span data-stu-id="5530f-137">For specific burst performance numbers, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles].</span></span>

## <a name="sharding"></a><span data-ttu-id="5530f-138">Parçalama</span><span class="sxs-lookup"><span data-stu-id="5530f-138">Sharding</span></span>
<span data-ttu-id="5530f-139">Bazen tek bir IOT hub cihaz toomillions ölçeklendirebilirsiniz olmakla birlikte, çözümünüzü tek bir IOT hub garanti edemez özel performans özellikleri gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5530f-139">While a single IoT hub can scale toomillions of devices, sometimes your solution requires specific performance characteristics that a single IoT hub cannot guarantee.</span></span> <span data-ttu-id="5530f-140">Bu durumda, birden çok IOT hub'ları aygıtlarınızı bölüm önerilir.</span><span class="sxs-lookup"><span data-stu-id="5530f-140">In that case, it is recommended that you partition your devices into multiple IoT hubs.</span></span> <span data-ttu-id="5530f-141">Birden çok IOT hub'ları trafiği WINS'e kesintisiz ve hello gerekli işleme veya gerekli işlem hızları elde edin.</span><span class="sxs-lookup"><span data-stu-id="5530f-141">Multiple IoT hubs smooth traffic bursts and obtain hello required throughput or operation rates that are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5530f-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5530f-142">Next steps</span></span>
<span data-ttu-id="5530f-143">toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:</span><span class="sxs-lookup"><span data-stu-id="5530f-143">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="5530f-144">[IOT Hub Geliştirici Kılavuzu][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="5530f-144">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="5530f-145">[Bir aygıt ile Azure IOT kenar benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="5530f-145">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
