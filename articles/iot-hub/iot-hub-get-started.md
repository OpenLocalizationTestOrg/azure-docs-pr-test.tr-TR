---
title: "Azure IOT Hub - IOT cihazları toohello bulut bağlanma Başlarken | Microsoft Docs"
description: "Bilgi nasıl tooconnect IOT panoları ve Başlatıcı Setleri tooAzure IOT hub'ı. Aygıtlarınızı telemetri tooIoT hub'ı ve IOT hub'ı izlemek ve cihazlarınızı yönetin gönderebilirsiniz."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: "Azure IOT hub Öğreticisi"
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: 6dc956308009091532019ff84aec881f042f0104
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-tutorials"></a><span data-ttu-id="dd655-105">Azure IOT hub'ı öğreticileri ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="dd655-105">Azure IoT Hub get started tutorials</span></span>

<span data-ttu-id="dd655-106">Azure IOT Hub ve hello Azure IOT cihaz SDK'ları toobuild nesnelerin interneti (IOT) çözümleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="dd655-106">You can use Azure IoT Hub and hello Azure IoT device SDKs toobuild Internet of Things (IoT) solutions:</span></span>

* <span data-ttu-id="dd655-107">Azure IOT Hub, güvenli bir şekilde bağlandığında, izler ve IOT cihazları yöneten hello bulutta tam olarak yönetilen bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="dd655-107">Azure IoT Hub is a fully managed service in hello cloud that securely connects, monitors, and manages your IoT devices.</span></span> <span data-ttu-id="dd655-108">Hello Azure IOT cihaz SDK'ları tooimplement IOT cihazlarınızı kullanın.</span><span class="sxs-lookup"><span data-stu-id="dd655-108">Use hello Azure IoT Device SDKs tooimplement your IoT devices.</span></span>
* <span data-ttu-id="dd655-109">Bir IOT ağ geçidi daha karmaşık IOT senaryolarda kullanın.</span><span class="sxs-lookup"><span data-stu-id="dd655-109">Use an IoT gateway in more complex IoT scenarios.</span></span> <span data-ttu-id="dd655-110">Örneğin, burada, eski aygıtlar, bant genişliği maliyetlerini, güvenlik ve gizlilik ilkeleri veya edge veri işleme gibi tooconsider faktörlere gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd655-110">For example, where you need tooconsider factors such as legacy devices, bandwidth costs, security and privacy policies, or edge data processing.</span></span> <span data-ttu-id="dd655-111">Bu senaryolarda, Azure IOT kenar tooimplement tooyour IOT hub'ı aygıtları bağlayan bir ağ geçidi kullanın.</span><span class="sxs-lookup"><span data-stu-id="dd655-111">In these scenarios, you use Azure IoT Edge tooimplement a gateway that connects devices tooyour IoT hub.</span></span>

## <a name="what-hello-tutorials-cover"></a><span data-ttu-id="dd655-112">Hangi hello öğreticileri kapsar</span><span class="sxs-lookup"><span data-stu-id="dd655-112">What hello tutorials cover</span></span>

<span data-ttu-id="dd655-113">Bu öğreticiler IOT hub'ı tooAzure ve hello cihaz SDK'ları sunar.</span><span class="sxs-lookup"><span data-stu-id="dd655-113">These tutorials introduce you tooAzure IoT Hub and hello device SDKs.</span></span> <span data-ttu-id="dd655-114">Merhaba öğreticileri ortak IOT senaryolarını toodemonstrate hello özellikleri IOT Hub'ının kapsar.</span><span class="sxs-lookup"><span data-stu-id="dd655-114">hello tutorials cover common IoT scenarios toodemonstrate hello capabilities of IoT Hub.</span></span> <span data-ttu-id="dd655-115">Merhaba öğreticileri de nasıl toocombine IOT Hub ile diğer Azure hizmetlerini ve toobuild daha araçları göstermeye güçlü IOT çözümleri.</span><span class="sxs-lookup"><span data-stu-id="dd655-115">hello tutorials also illustrate how toocombine IoT Hub with other Azure services and tools toobuild more powerful IoT solutions.</span></span> <span data-ttu-id="dd655-116">Merhaba eğitimlerine benzetimli ya da gerçek IOT cihazları toouse seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd655-116">In hello tutorials, you can choose toouse either simulated or real IoT devices.</span></span> <span data-ttu-id="dd655-117">Ayrıca, öğrenebilirsiniz nasıl toouse bir ağ geçidi tooenable aygıtları tooconnect tooyour IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="dd655-117">In addition, you can learn how toouse a gateway tooenable devices tooconnect tooyour IoT hub.</span></span>

## <a name="set-up-your-device"></a><span data-ttu-id="dd655-118">Cihazınızı kurma</span><span class="sxs-lookup"><span data-stu-id="dd655-118">Set up your device</span></span>

<span data-ttu-id="dd655-119">Bir IOT cihaz veya ağ geçidi tooAzure IOT hub'ı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="dd655-119">Connect an IoT device or gateway tooAzure IoT Hub.</span></span> <span data-ttu-id="dd655-120">Başlatılan bir fiziksel veya sanal aygıt tooget birini seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="dd655-120">You can choose a physical or simulated device tooget started:</span></span>

| <span data-ttu-id="dd655-121">IOT cihaz</span><span class="sxs-lookup"><span data-stu-id="dd655-121">IoT device</span></span>                       | <span data-ttu-id="dd655-122">Programlama dili</span><span class="sxs-lookup"><span data-stu-id="dd655-122">Programming language</span></span> |
|----------------------------------|----------------------|
| <span data-ttu-id="dd655-123">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="dd655-123">Raspberry Pi</span></span>                     | <span data-ttu-id="dd655-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="dd655-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="dd655-125">IOT DevKit</span><span class="sxs-lookup"><span data-stu-id="dd655-125">IoT DevKit</span></span>                       | <span data-ttu-id="dd655-126">[VSCode Arduino][DevKit]</span><span class="sxs-lookup"><span data-stu-id="dd655-126">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="dd655-127">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="dd655-127">Intel Edison</span></span>                     | <span data-ttu-id="dd655-128">[Node.js][Ed_Nd], [C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="dd655-128">[Node.js][Ed_Nd], [C][Ed_C]</span></span>    |
| <span data-ttu-id="dd655-129">Adafruit yumuşatma HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="dd655-129">Adafruit Feather HUZZAH ESP8266</span></span>  | <span data-ttu-id="dd655-130">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="dd655-130">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="dd655-131">Sparkfun ESP8266 şey geliştirme</span><span class="sxs-lookup"><span data-stu-id="dd655-131">Sparkfun ESP8266 Thing Dev</span></span>       | <span data-ttu-id="dd655-132">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="dd655-132">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="dd655-133">Adafruit yumuşatma M0</span><span class="sxs-lookup"><span data-stu-id="dd655-133">Adafruit Feather M0</span></span>              | <span data-ttu-id="dd655-134">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="dd655-134">[Arduino][M0_Ard]</span></span>              |
| <span data-ttu-id="dd655-135">Sanal cihaz PC'de</span><span class="sxs-lookup"><span data-stu-id="dd655-135">Simulated device on PC</span></span>           | <span data-ttu-id="dd655-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth]</span><span class="sxs-lookup"><span data-stu-id="dd655-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth]</span></span> |
| <span data-ttu-id="dd655-137">Çevrimiçi aygıt benzeticisi</span><span class="sxs-lookup"><span data-stu-id="dd655-137">Online device simulator</span></span>         | <span data-ttu-id="dd655-138">[Böğürtlenli Pi (Node.js)][Ol_Sim]</span><span class="sxs-lookup"><span data-stu-id="dd655-138">[Raspberry Pi (Node.js)][Ol_Sim]</span></span> |

<span data-ttu-id="dd655-139">Ayrıca, IOT sınır ağ geçidi tooenable aygıtları tooconnect tooyour IOT hub'ı kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="dd655-139">In addition, you can use an IoT Edge gateway tooenable devices tooconnect tooyour IoT hub:</span></span>

| <span data-ttu-id="dd655-140">Ağ geçidi aygıtı</span><span class="sxs-lookup"><span data-stu-id="dd655-140">Gateway device</span></span>               | <span data-ttu-id="dd655-141">Programlama dili</span><span class="sxs-lookup"><span data-stu-id="dd655-141">Programming language</span></span> | <span data-ttu-id="dd655-142">Platform</span><span class="sxs-lookup"><span data-stu-id="dd655-142">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="dd655-143">Intel NUC (modeli DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="dd655-143">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="dd655-144">C</span><span class="sxs-lookup"><span data-stu-id="dd655-144">C</span></span>                    | <span data-ttu-id="dd655-145">[Rüzgar Akarsu Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="dd655-145">[Wind River Linux][NUC_Lnx]</span></span> |
| <span data-ttu-id="dd655-146">Sanal ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="dd655-146">Simulated gateway</span></span>            | <span data-ttu-id="dd655-147">C</span><span class="sxs-lookup"><span data-stu-id="dd655-147">C</span></span>                    | <span data-ttu-id="dd655-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span><span class="sxs-lookup"><span data-stu-id="dd655-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span></span> |

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
[Sim_NET]: iot-hub-csharp-csharp-getstarted.md
[Sim_Jav]: iot-hub-java-java-getstarted.md
[Sim_Nd]: iot-hub-node-node-getstarted.md
[Sim_Pyth]: iot-hub-python-getstarted.md
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
[Sim_Lnx]: iot-hub-linux-iot-edge-get-started.md
[Sim_Win]: iot-hub-windows-iot-edge-get-started.md
[Ol_Sim]: iot-hub-raspberry-pi-web-simulator-get-started.md
