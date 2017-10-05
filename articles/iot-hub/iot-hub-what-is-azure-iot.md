---
title: "Nesnelerin İnterneti (IoT Paketi) için Azure çözümleri | Microsoft Docs"
description: "Örnek bir IoT çözümü mimarisi ile cihazlar, Azure IoT Hub hizmeti, Azure IoT cihaz SDK'ları, Azure IoT hizmeti SDK'ları ve diğer Azure hizmetleriyle olan ilişkisi."
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
ms.openlocfilehash: 1d54f090a0e07cd5102cb48cd70a1377845d6654
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="next-steps"></a><span data-ttu-id="23c90-103">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="23c90-103">Next steps</span></span>

<span data-ttu-id="23c90-104">Azure IoT Hub, çözümünüzün arka ucu ile milyonlarca cihaz arasında düzgün ve güvenli çift yönlü iletişimler sağlayan bir Azure hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="23c90-104">Azure IoT Hub is an Azure service that enables secure and reliable bi-directional communications between your solution back end and millions of devices.</span></span> <span data-ttu-id="23c90-105">Şunları yapmak için çözüm arka ucu sağlar:</span><span class="sxs-lookup"><span data-stu-id="23c90-105">It enables the solution back end to:</span></span>

* <span data-ttu-id="23c90-106">Cihazlarınızdan ölçekleyerek telemetri alma.</span><span class="sxs-lookup"><span data-stu-id="23c90-106">Receive telemetry at scale from your devices.</span></span>
* <span data-ttu-id="23c90-107">Verileri cihazlarınızdan akış olayı işlemcisine yönlendirme.</span><span class="sxs-lookup"><span data-stu-id="23c90-107">Route data from your devices to a stream event processor.</span></span>
* <span data-ttu-id="23c90-108">Cihazlardan dosya yüklemeleri alma.</span><span class="sxs-lookup"><span data-stu-id="23c90-108">Receive file uploads from devices.</span></span>
* <span data-ttu-id="23c90-109">Belirli cihazlara, buluttan cihaza iletileri gönderme.</span><span class="sxs-lookup"><span data-stu-id="23c90-109">Send cloud-to-device messages to specific devices.</span></span>

<span data-ttu-id="23c90-110">Kendi çözüm arka ucunuzu uygulamak için IoT Hub'ınızı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23c90-110">You can use IoT Hub to implement your own solution back end.</span></span> <span data-ttu-id="23c90-111">Buna ek olarak IoT Hub; cihazları, güvenlik kimlik bilgilerini ve IoT hub'ına bağlanma haklarını sağlamak için kullanılan bir kimlik kayıt defterini içerir.</span><span class="sxs-lookup"><span data-stu-id="23c90-111">In addition, IoT Hub includes an identity registry used to provision devices, their security credentials, and their rights to connect to the IoT hub.</span></span> <span data-ttu-id="23c90-112">IoT Hub hakkında daha fazla bilgi almak için bkz. [IoT Hub nedir?][lnk-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="23c90-112">To learn more about IoT Hub, see [What is IoT Hub?][lnk-iot-hub].</span></span>

<span data-ttu-id="23c90-113">Cihazlarınızı uzaktan yönetmeniz, yapılandırmanız ve güncelleştirmeniz için Azure IoT Hub’ın standartlara dayalı cihaz yönetimini nasıl etkinleştirdiği hakkında bilgi almak üzere bkz. [IoT Hub’ı ile cihaz yönetimine genel bakış][lnk-device-management].</span><span class="sxs-lookup"><span data-stu-id="23c90-113">To learn how Azure IoT Hub enables standards-based device management for you to remotely manage, configure, and update your devices, see [Overview of device management with IoT Hub][lnk-device-management].</span></span>

<span data-ttu-id="23c90-114">İstemci uygulamalarını çok sayıda cihaz donanımı platformunda ve işletim sisteminde uygulamak için Azure IoT cihaz SDK'larını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23c90-114">To implement client applications on a wide variety of device hardware platforms and operating systems, you can use the Azure IoT device SDKs.</span></span> <span data-ttu-id="23c90-115">Cihaz SDK'ları, bir IoT hub'ına telemetri gönderme ve buluttan cihaza iletilerini alma işlemlerini gerçekleştiren kitaplıkları içerir.</span><span class="sxs-lookup"><span data-stu-id="23c90-115">The device SDKs include libraries that facilitate sending telemetry to an IoT hub and receiving cloud-to-device messages.</span></span> <span data-ttu-id="23c90-116">Cihaz SDK'larını kullandığınızda IoT Hub ile iletişim kurmak için birçok ağ protokolü arasından seçim yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23c90-116">When you use the device SDKs, you can choose from several network protocols to communicate with IoT Hub.</span></span> <span data-ttu-id="23c90-117">Daha fazla bilgi için bkz. [Cihaz SDK'ları hakkında bilgi][lnk-device-sdks].</span><span class="sxs-lookup"><span data-stu-id="23c90-117">To learn more, see the [information about device SDKs][lnk-device-sdks].</span></span>

<span data-ttu-id="23c90-118">Bazı kodları yazmaya ve bazı örnekleri çalıştırmaya başlamak için [IoT Hub ile çalışmaya başlama][lnk-getstarted] öğreticisine bakın.</span><span class="sxs-lookup"><span data-stu-id="23c90-118">To get started writing some code and running some samples, see the [Get started with IoT Hub][lnk-getstarted] tutorial.</span></span>

<span data-ttu-id="23c90-119">Önceden yapılandırılmış çözümler koleksiyonu olan [Azure IoT Paketi][lnk-iot-suite] de ilginizi çekebilir.</span><span class="sxs-lookup"><span data-stu-id="23c90-119">You may also be interested in [Azure IoT Suite][lnk-iot-suite], which is a collection of preconfigured solutions.</span></span> <span data-ttu-id="23c90-120">IoT Paketi, hızlı bir şekilde kullanmaya başlamanızı ve uzaktan izleme, varlık yönetimi ve tahmine dayalı bakım gibi ortak IoT senaryolarını ele almak üzere IoT projelerini ölçeklendirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="23c90-120">IoT Suite enables you to get started quickly and scale IoT projects to address common IoT scenarios--such as remote monitoring, asset management, and predictive maintenance.</span></span>

[lnk-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-iot-hub]: iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-device-management-overview.md
