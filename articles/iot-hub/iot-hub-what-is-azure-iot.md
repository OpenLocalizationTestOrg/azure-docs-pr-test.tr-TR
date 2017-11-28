---
title: "aaaAzure çözümleri nesnelerin interneti (IOT paketi) | Microsoft Docs"
description: "Örnek bir IOT çözüm mimarisi ve nasıl toodevices, ilişkili olduğu genel bakış, Azure IOT Hub hizmeti, Azure IOT cihaz SDK'ları, Azure IOT hizmeti SDK'ları ve diğer Azure hizmetleriyle hello."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a859e379-dca7-42fa-bdf6-1125c86ad140
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 2d934e3f988c530de6a242869c021712d2aa1576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="next-steps"></a><span data-ttu-id="6d286-103">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6d286-103">Next steps</span></span>

<span data-ttu-id="6d286-104">Azure IoT Hub, çözümünüzün arka ucu ile milyonlarca cihaz arasında düzgün ve güvenli çift yönlü iletişimler sağlayan bir Azure hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="6d286-104">Azure IoT Hub is an Azure service that enables secure and reliable bi-directional communications between your solution back end and millions of devices.</span></span> <span data-ttu-id="6d286-105">Merhaba çözüm arka ucuna sağlar:</span><span class="sxs-lookup"><span data-stu-id="6d286-105">It enables hello solution back end to:</span></span>

* <span data-ttu-id="6d286-106">Cihazlarınızdan ölçekleyerek telemetri alma.</span><span class="sxs-lookup"><span data-stu-id="6d286-106">Receive telemetry at scale from your devices.</span></span>
* <span data-ttu-id="6d286-107">Aygıtları tooa akış etkinliği işlemcisine rota verileri.</span><span class="sxs-lookup"><span data-stu-id="6d286-107">Route data from your devices tooa stream event processor.</span></span>
* <span data-ttu-id="6d286-108">Cihazlardan dosya yüklemeleri alma.</span><span class="sxs-lookup"><span data-stu-id="6d286-108">Receive file uploads from devices.</span></span>
* <span data-ttu-id="6d286-109">Bulut-cihaz iletilerini toospecific aygıtları gönderin.</span><span class="sxs-lookup"><span data-stu-id="6d286-109">Send cloud-to-device messages toospecific devices.</span></span>

<span data-ttu-id="6d286-110">Kendi çözüm arka ucu IOT hub'ı tooimplement kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d286-110">You can use IoT Hub tooimplement your own solution back end.</span></span> <span data-ttu-id="6d286-111">Ayrıca, IOT hub'ı bir kimlik kullanılan kayıt defteri tooprovision cihazları, kendi güvenlik kimlik bilgileri ve bunların haklarını tooconnect toohello IOT hub'ı içerir.</span><span class="sxs-lookup"><span data-stu-id="6d286-111">In addition, IoT Hub includes an identity registry used tooprovision devices, their security credentials, and their rights tooconnect toohello IoT hub.</span></span> <span data-ttu-id="6d286-112">IOT hub'ı hakkında daha fazla toolearn bkz [IOT Hub nedir?] [lnk-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="6d286-112">toolearn more about IoT Hub, see [What is IoT Hub?][lnk-iot-hub].</span></span>

<span data-ttu-id="6d286-113">Azure IOT Hub, tooremotely yönetmek, yapılandırmak ve aygıtlarınızın güncelleştirmek için standartlara dayalı aygıt yönetimi sağlar nasıl toolearn bkz [cihaz yönetimine genel bakış IOT Hub ile][lnk-device-management].</span><span class="sxs-lookup"><span data-stu-id="6d286-113">toolearn how Azure IoT Hub enables standards-based device management for you tooremotely manage, configure, and update your devices, see [Overview of device management with IoT Hub][lnk-device-management].</span></span>

<span data-ttu-id="6d286-114">çok çeşitli cihaz donanım platformları ve işletim sistemleri tooimplement istemci uygulamaları, hello Azure IOT cihaz SDK'ları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d286-114">tooimplement client applications on a wide variety of device hardware platforms and operating systems, you can use hello Azure IoT device SDKs.</span></span> <span data-ttu-id="6d286-115">Merhaba cihaz SDK'ları telemetri tooan IOT hub ve alma bulut cihaza iletileri gönderme kolaylaştırmak kitaplıkları içerir.</span><span class="sxs-lookup"><span data-stu-id="6d286-115">hello device SDKs include libraries that facilitate sending telemetry tooan IoT hub and receiving cloud-to-device messages.</span></span> <span data-ttu-id="6d286-116">Merhaba cihaz SDK'ları kullandığınızda IOT Hub ile çeşitli ağ protokolleri toocommunicate seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d286-116">When you use hello device SDKs, you can choose from several network protocols toocommunicate with IoT Hub.</span></span> <span data-ttu-id="6d286-117">toolearn daha, hello fazla [cihaz SDK'ları hakkında bilgi][lnk-device-sdks].</span><span class="sxs-lookup"><span data-stu-id="6d286-117">toolearn more, see hello [information about device SDKs][lnk-device-sdks].</span></span>

<span data-ttu-id="6d286-118">biraz kod yazmaya ve bazı örnekler çalıştıran başlatılan tooget bkz hello [IOT Hub ile çalışmaya başlama] [ lnk-getstarted] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="6d286-118">tooget started writing some code and running some samples, see hello [Get started with IoT Hub][lnk-getstarted] tutorial.</span></span>

<span data-ttu-id="6d286-119">Önceden yapılandırılmış çözümler koleksiyonu olan [Azure IoT Paketi][lnk-iot-suite] de ilginizi çekebilir.</span><span class="sxs-lookup"><span data-stu-id="6d286-119">You may also be interested in [Azure IoT Suite][lnk-iot-suite], which is a collection of preconfigured solutions.</span></span> <span data-ttu-id="6d286-120">IOT paketi IOT projelerini tooaddress ortak IOT senaryolarını Uzaktan izleme, varlık yönetimi ve Tahmine dayalı bakım gibi ölçeklendirme ve daha hızlı şekilde kullanmaya tooget sağlar.</span><span class="sxs-lookup"><span data-stu-id="6d286-120">IoT Suite enables you tooget started quickly and scale IoT projects tooaddress common IoT scenarios--such as remote monitoring, asset management, and predictive maintenance.</span></span>

[lnk-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-iot-hub]: iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-device-management-overview.md
