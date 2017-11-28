---
title: "Fiziksel aygıtların tooAzure IOT hub'ı bağlanma kullanmaya başlama | Microsoft Docs"
description: "Bilgi nasıl tooconnect fiziksel cihazlar ve panoları tooAzure IOT hub'ı. Aygıtlarınızı telemetri tooIoT hub'ı ve IOT hub'ı izlemek ve cihazlarınızı yönetin gönderebilirsiniz."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: "Azure IOT hub Öğreticisi"
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: 47ce289c438b2f495d499d724c38ddc4b3307425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-with-physical-devices-tutorials"></a><span data-ttu-id="cac10-105">Azure IOT Hub, fiziksel cihazların öğreticileri ile Başlarken</span><span class="sxs-lookup"><span data-stu-id="cac10-105">Azure IoT Hub get started with physical devices tutorials</span></span>

<span data-ttu-id="cac10-106">Bu öğreticiler IOT hub'ı tooAzure ve hello cihaz SDK'ları sunar.</span><span class="sxs-lookup"><span data-stu-id="cac10-106">These tutorials introduce you tooAzure IoT Hub and hello device SDKs.</span></span> <span data-ttu-id="cac10-107">Merhaba öğreticileri ortak IOT senaryolarını toodemonstrate hello özellikleri IOT Hub'ının kapsar.</span><span class="sxs-lookup"><span data-stu-id="cac10-107">hello tutorials cover common IoT scenarios toodemonstrate hello capabilities of IoT Hub.</span></span> <span data-ttu-id="cac10-108">Merhaba öğreticileri de nasıl toocombine IOT Hub ile diğer Azure hizmetlerini ve toobuild daha araçları göstermeye güçlü IOT çözümleri.</span><span class="sxs-lookup"><span data-stu-id="cac10-108">hello tutorials also illustrate how toocombine IoT Hub with other Azure services and tools toobuild more powerful IoT solutions.</span></span> <span data-ttu-id="cac10-109">Merhaba listelenen öğreticileri aşağıdaki tabloda Göster, nasıl hello toocreate fiziksel IOT cihazları.</span><span class="sxs-lookup"><span data-stu-id="cac10-109">hello tutorials listed in hello following table show you how toocreate physical IoT devices.</span></span>

| <span data-ttu-id="cac10-110">IOT cihaz</span><span class="sxs-lookup"><span data-stu-id="cac10-110">IoT device</span></span>                       | <span data-ttu-id="cac10-111">Programlama dili</span><span class="sxs-lookup"><span data-stu-id="cac10-111">Programming language</span></span> |
|---------------------------------|----------------------|
| <span data-ttu-id="cac10-112">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="cac10-112">Raspberry Pi</span></span>                    | <span data-ttu-id="cac10-113">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="cac10-113">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="cac10-114">IOT DevKit</span><span class="sxs-lookup"><span data-stu-id="cac10-114">IoT DevKit</span></span>                      | <span data-ttu-id="cac10-115">[VSCode Arduino][DevKit]</span><span class="sxs-lookup"><span data-stu-id="cac10-115">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="cac10-116">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="cac10-116">Intel Edison</span></span>                    | <span data-ttu-id="cac10-117">[Node.js][Ed_Nd], [C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="cac10-117">[Node.js][Ed_Nd], [C][Ed_C]</span></span>           |
| <span data-ttu-id="cac10-118">Adafruit yumuşatma HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="cac10-118">Adafruit Feather HUZZAH ESP8266</span></span> | <span data-ttu-id="cac10-119">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="cac10-119">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="cac10-120">Sparkfun ESP8266 şey geliştirme</span><span class="sxs-lookup"><span data-stu-id="cac10-120">Sparkfun ESP8266 Thing Dev</span></span>      | <span data-ttu-id="cac10-121">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="cac10-121">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="cac10-122">Adafruit yumuşatma M0</span><span class="sxs-lookup"><span data-stu-id="cac10-122">Adafruit Feather M0</span></span>             | <span data-ttu-id="cac10-123">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="cac10-123">[Arduino][M0_Ard]</span></span>              |

<span data-ttu-id="cac10-124">Ayrıca, IOT sınır ağ geçidi tooenable aygıtları tooconnect tooyour IOT hub'ı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cac10-124">In addition, you can use an IoT Edge gateway tooenable devices tooconnect tooyour IoT hub.</span></span>

| <span data-ttu-id="cac10-125">Ağ geçidi aygıtı</span><span class="sxs-lookup"><span data-stu-id="cac10-125">Gateway device</span></span>               | <span data-ttu-id="cac10-126">Programlama dili</span><span class="sxs-lookup"><span data-stu-id="cac10-126">Programming language</span></span> | <span data-ttu-id="cac10-127">Platform</span><span class="sxs-lookup"><span data-stu-id="cac10-127">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="cac10-128">Intel NUC (modeli DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="cac10-128">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="cac10-129">C</span><span class="sxs-lookup"><span data-stu-id="cac10-129">C</span></span>                    | <span data-ttu-id="cac10-130">[Rüzgar Akarsu Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="cac10-130">[Wind River Linux][NUC_Lnx]</span></span> |

[!INCLUDE [iot-hub-get-started-extended](../../includes/iot-hub-get-started-extended.md)]


[Pi_Nd]: iot-hub-raspberry-pi-kit-node-get-started.md
[Pi_C]: iot-hub-raspberry-pi-kit-c-get-started.md
[Pi_Py]: iot-hub-raspberry-pi-kit-python-get-started.md
[DevKit]: iot-hub-arduino-iot-devkit-az3166-get-started.md
[Ed_Nd]: iot-hub-intel-edison-kit-node-get-started.md
[Ed_C]: iot-hub-intel-edison-kit-c-get-started.md
[Hu_Ard]: iot-hub-arduino-huzzah-esp8266-get-started.md
[Th_Ard]: iot-hub-sparkfun-esp8266-thing-dev-get-started.md
[M0_Ard]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
