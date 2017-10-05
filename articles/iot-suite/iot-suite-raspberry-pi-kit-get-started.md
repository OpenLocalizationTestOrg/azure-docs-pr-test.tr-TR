---
title: "Azure IOT paketi Böğürtlenli Pi bağlanma | Microsoft Docs"
description: "Öğreticiler Raspberry Pi 3 ve IOT paketi Uzaktan izleme çözümü için Microsoft Azure IOT Starter Kit kullanmayı öğrenmenize yardımcı olmak için node.js veya C kullanma. Telemetri, benzetim veya gerçek algılayıcılar kullanan ya da uzak Bellenim güncelleştirmeleri sağlayan bir öğretici seçebilirsiniz."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: eaa6a21a08bd9068b5335a8167f54c2aa387e0e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-microsoft-azure-iot-raspberry-pi-3-starter-kit-to-the-remote-monitoring-solution"></a><span data-ttu-id="e577b-104">Microsoft Azure IOT Raspberry Pi 3 Starter Kit Uzaktan izleme çözümüne bağlama</span><span class="sxs-lookup"><span data-stu-id="e577b-104">Connect your Microsoft Azure IoT Raspberry Pi 3 Starter Kit to the remote monitoring solution</span></span>

<span data-ttu-id="e577b-105">Bu bölümdeki öğreticileri Raspberry Pi 3 aygıtı Uzaktan izleme çözümüne bağlama öğrenin yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="e577b-105">The tutorials in this section help you learn how to connect a Raspberry Pi 3 device to the remote monitoring solution.</span></span> <span data-ttu-id="e577b-106">Tercih edilen programlama diline uygun öğretici seçin ve algılayıcı donanım, Raspberry Pi'yi ile kullanmak için kullanılabilir olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="e577b-106">Choose the tutorial appropriate to your preferred programming language and the whether you have the sensor hardware available to use with your Raspberry Pi.</span></span>

## <a name="the-tutorials"></a><span data-ttu-id="e577b-107">Öğreticiler</span><span class="sxs-lookup"><span data-stu-id="e577b-107">The tutorials</span></span>

| <span data-ttu-id="e577b-108">Öğretici</span><span class="sxs-lookup"><span data-stu-id="e577b-108">Tutorial</span></span> | <span data-ttu-id="e577b-109">Notlar</span><span class="sxs-lookup"><span data-stu-id="e577b-109">Notes</span></span> | <span data-ttu-id="e577b-110">Diller</span><span class="sxs-lookup"><span data-stu-id="e577b-110">Languages</span></span> |
| -------- | ----- | --------- |
| <span data-ttu-id="e577b-111">Sanal telemetriyi (Temel)</span><span class="sxs-lookup"><span data-stu-id="e577b-111">Simulated telemetry (Basic)</span></span>| <span data-ttu-id="e577b-112">Algılayıcı verilerini benzetimini yapar.</span><span class="sxs-lookup"><span data-stu-id="e577b-112">Simulates sensor data.</span></span> <span data-ttu-id="e577b-113">Tek başına Raspberry Pi'yi kullanır.</span><span class="sxs-lookup"><span data-stu-id="e577b-113">Uses a standalone Raspberry Pi.</span></span> | <span data-ttu-id="e577b-114">[C][lnk-c-simulator], [Node.js][lnk-node-simulator]</span><span class="sxs-lookup"><span data-stu-id="e577b-114">[C][lnk-c-simulator], [Node.js][lnk-node-simulator]</span></span> |
| <span data-ttu-id="e577b-115">Gerçek algılayıcısı (Orta)</span><span class="sxs-lookup"><span data-stu-id="e577b-115">Real sensor (Intermediate)</span></span> | <span data-ttu-id="e577b-116">Raspberry Pi'yi bağlı BME280 algılayıcı verilerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="e577b-116">Uses data from a BME280 sensor connected to your Raspberry Pi.</span></span> | <span data-ttu-id="e577b-117">[C][lnk-c-basic], [Node.js][lnk-node-basic]</span><span class="sxs-lookup"><span data-stu-id="e577b-117">[C][lnk-c-basic], [Node.js][lnk-node-basic]</span></span> |
| <span data-ttu-id="e577b-118">Uygulama yazılımı güncelleştirmesi (Gelişmiş)</span><span class="sxs-lookup"><span data-stu-id="e577b-118">Implement firmware update (Advanced)</span></span>| <span data-ttu-id="e577b-119">Raspberry Pi'yi bağlı BME280 algılayıcı verilerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="e577b-119">Uses data from a BME280 sensor connected to your Raspberry Pi.</span></span> <span data-ttu-id="e577b-120">Raspberry Pi'yi uzak Bellenim güncelleştirmeleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="e577b-120">Enables remote firmware updates on your Raspberry Pi.</span></span> | <span data-ttu-id="e577b-121">[C][lnk-c-advanced], [Node.js][lnk-node-advanced]</span><span class="sxs-lookup"><span data-stu-id="e577b-121">[C][lnk-c-advanced], [Node.js][lnk-node-advanced]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e577b-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e577b-122">Next steps</span></span>

<span data-ttu-id="e577b-123">Ziyaret [Azure IOT Geliştirme Merkezi](https://azure.microsoft.com/develop/iot/) daha fazla örnekleri ve Azure IOT belgeler.</span><span class="sxs-lookup"><span data-stu-id="e577b-123">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[lnk-node-simulator]: iot-suite-raspberry-pi-kit-node-get-started-simulator.md
[lnk-node-basic]: iot-suite-raspberry-pi-kit-node-get-started-basic.md
[lnk-node-advanced]: iot-suite-raspberry-pi-kit-node-get-started-advanced.md
[lnk-c-simulator]: iot-suite-raspberry-pi-kit-c-get-started-simulator.md
[lnk-c-basic]: iot-suite-raspberry-pi-kit-c-get-started-basic.md
[lnk-c-advanced]: iot-suite-raspberry-pi-kit-c-get-started-advanced.md