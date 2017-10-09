---
title: "Azure IOT Hub aaaUnderstand Mesajlaşma | Microsoft Docs"
description: "Geliştirici Kılavuzu - cihaz Bulut ve bulut-cihaz IOT Hub ile ileti. İleti biçimleri ve desteklenen protokolleri hakkında bilgi içerir."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: a610741e23e243f392f1c042f9ab4a00d42f734f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a><span data-ttu-id="bd8cd-104">Cihaz Bulut ve bulut-cihaz IOT Hub ile Mesajlaşma</span><span class="sxs-lookup"><span data-stu-id="bd8cd-104">Device-to-cloud and cloud-to-device messaging with IoT Hub</span></span>

<span data-ttu-id="bd8cd-105">IOT Hub'ın cihazlar tarafından ile toocommunicate Mesajlaşma kullanın:</span><span class="sxs-lookup"><span data-stu-id="bd8cd-105">Use IoT Hub messaging toocommunicate with your devices by:</span></span>

* <span data-ttu-id="bd8cd-106">Gönderme [cihaz bulut] [ lnk-d2c] aygıtları tooyour çözümünüzü iletilerden son yedekleme.</span><span class="sxs-lookup"><span data-stu-id="bd8cd-106">Sending [device-to-cloud][lnk-d2c] messages from your devices tooyour solution back end.</span></span>
* <span data-ttu-id="bd8cd-107">Gönderme [bulut cihaz] [ lnk-c2d] hello çözüm arka iletilerden bitiş tooyour aygıtlar.</span><span class="sxs-lookup"><span data-stu-id="bd8cd-107">Sending [cloud-to-device][lnk-c2d] messages from hello solution back end tooyour devices.</span></span>

<span data-ttu-id="bd8cd-108">Çekirdek IOT hub'ı Mesajlaşma işlevleri hello güvenilirlik ve dayanıklılık iletilerinin özellikleridir.</span><span class="sxs-lookup"><span data-stu-id="bd8cd-108">Core properties of IoT Hub messaging functionality are hello reliability and durability of messages.</span></span> <span data-ttu-id="bd8cd-109">Bu özellikleri hello cihaz tarafındaki esnekliği toointermittent bağlantıyı etkinleştirmek ve hello bulut tarafında işleme olay tooload ani.</span><span class="sxs-lookup"><span data-stu-id="bd8cd-109">These properties enable resilience toointermittent connectivity on hello device side, and tooload spikes in event processing on hello cloud side.</span></span> <span data-ttu-id="bd8cd-110">IOT hub'ı uygulayan *en az bir kez* teslim cihaz Bulut ve bulut-cihaz Mesajlaşma güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="bd8cd-110">IoT Hub implements *at least once* delivery guarantees for both device-to-cloud and cloud-to-device messaging.</span></span>

<span data-ttu-id="bd8cd-111">İçin bir giriş toohello özellikleri IOT Hub'ının hello makalelerine bakın [Azure ve nesnelerin interneti] [ lnk-azure-iot] ve [hello Azure IOT Hub hizmetine genel bakış] [lnk-iot-hub-overview].</span><span class="sxs-lookup"><span data-stu-id="bd8cd-111">For an introduction toohello capabilities of IoT Hub, see hello articles [Azure and Internet of Things][lnk-azure-iot] and [Overview of hello Azure IoT Hub service][lnk-iot-hub-overview].</span></span>

## <a name="when-toouse-iot-hub-messaging"></a><span data-ttu-id="bd8cd-112">Zaman toouse IOT hub'ı Mesajlaşma</span><span class="sxs-lookup"><span data-stu-id="bd8cd-112">When toouse IoT Hub messaging</span></span>

<span data-ttu-id="bd8cd-113">Zaman serisi telemetri ve uyarılar, cihaz uygulamanızdan göndermek için cihaz bulut iletilerini ve bulut-cihaz iletilerini tek yönlü bildirimleri tooyour aygıt uygulama için kullanın.</span><span class="sxs-lookup"><span data-stu-id="bd8cd-113">Use device-to-cloud messages for sending time series telemetry and alerts from your device app, and cloud-to-device messages for one-way notifications tooyour device app.</span></span>

* <span data-ttu-id="bd8cd-114">Çok başvuran[cihaz bulut iletişimi Kılavuzu] [ lnk-d2c-guidance] IF cihaz bulut iletilerini, bildirilen özellikleri veya karşıya dosya yükleme kullanarak arasında şüpheli.</span><span class="sxs-lookup"><span data-stu-id="bd8cd-114">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using device-to-cloud messages, reported properties, or file upload.</span></span>
* <span data-ttu-id="bd8cd-115">Çok başvuran[bulut-cihaz iletişimi Kılavuzu] [ lnk-c2d-guidance] IF bulut-cihaz iletilerini, istenen özelliklerini veya doğrudan yöntemlerini kullanarak arasında şüpheli.</span><span class="sxs-lookup"><span data-stu-id="bd8cd-115">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using cloud-to-device messages, desired properties, or direct methods.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd8cd-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bd8cd-116">Next steps</span></span>

* <span data-ttu-id="bd8cd-117">IOT Hub hakkında bilgi edinin [cihaz bulut Mesajlaşma][lnk-d2c].</span><span class="sxs-lookup"><span data-stu-id="bd8cd-117">Learn about IoT Hub [device-to-cloud messaging][lnk-d2c].</span></span>
* <span data-ttu-id="bd8cd-118">IOT Hub hakkında bilgi edinin [bulut cihaz Mesajlaşma][lnk-c2d].</span><span class="sxs-lookup"><span data-stu-id="bd8cd-118">Learn about IoT Hub [cloud-to-device messaging][lnk-c2d].</span></span>

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md