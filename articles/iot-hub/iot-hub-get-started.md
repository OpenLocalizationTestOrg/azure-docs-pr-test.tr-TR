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
# <a name="azure-iot-hub-get-started-tutorials"></a>Azure IOT hub'ı öğreticileri ile çalışmaya başlama

Azure IOT Hub ve hello Azure IOT cihaz SDK'ları toobuild nesnelerin interneti (IOT) çözümleri kullanabilirsiniz:

* Azure IOT Hub, güvenli bir şekilde bağlandığında, izler ve IOT cihazları yöneten hello bulutta tam olarak yönetilen bir hizmettir. Hello Azure IOT cihaz SDK'ları tooimplement IOT cihazlarınızı kullanın.
* Bir IOT ağ geçidi daha karmaşık IOT senaryolarda kullanın. Örneğin, burada, eski aygıtlar, bant genişliği maliyetlerini, güvenlik ve gizlilik ilkeleri veya edge veri işleme gibi tooconsider faktörlere gerekir. Bu senaryolarda, Azure IOT kenar tooimplement tooyour IOT hub'ı aygıtları bağlayan bir ağ geçidi kullanın.

## <a name="what-hello-tutorials-cover"></a>Hangi hello öğreticileri kapsar

Bu öğreticiler IOT hub'ı tooAzure ve hello cihaz SDK'ları sunar. Merhaba öğreticileri ortak IOT senaryolarını toodemonstrate hello özellikleri IOT Hub'ının kapsar. Merhaba öğreticileri de nasıl toocombine IOT Hub ile diğer Azure hizmetlerini ve toobuild daha araçları göstermeye güçlü IOT çözümleri. Merhaba eğitimlerine benzetimli ya da gerçek IOT cihazları toouse seçebilirsiniz. Ayrıca, öğrenebilirsiniz nasıl toouse bir ağ geçidi tooenable aygıtları tooconnect tooyour IOT hub'ı.

## <a name="set-up-your-device"></a>Cihazınızı kurma

Bir IOT cihaz veya ağ geçidi tooAzure IOT hub'ı bağlayın. Başlatılan bir fiziksel veya sanal aygıt tooget birini seçebilirsiniz:

| IOT cihaz                       | Programlama dili |
|----------------------------------|----------------------|
| Raspberry Pi                     | [Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]  |
| IOT DevKit                       | [VSCode Arduino][DevKit]     |
| Intel Edison                     | [Node.js][Ed_Nd], [C][Ed_C]    |
| Adafruit yumuşatma HUZZAH ESP8266  | [Arduino][Hu_Ard]              |
| Sparkfun ESP8266 şey geliştirme       | [Arduino][Th_Ard]              |
| Adafruit yumuşatma M0              | [Arduino][M0_Ard]              |
| Sanal cihaz PC'de           | [.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth] |
| Çevrimiçi aygıt benzeticisi         | [Böğürtlenli Pi (Node.js)][Ol_Sim] |

Ayrıca, IOT sınır ağ geçidi tooenable aygıtları tooconnect tooyour IOT hub'ı kullanabilirsiniz:

| Ağ geçidi aygıtı               | Programlama dili | Platform         |
|------------------------------|----------------------|------------------|
| Intel NUC (modeli DE3815TYKE) | C                    | [Rüzgar Akarsu Linux][NUC_Lnx] |
| Sanal ağ geçidi            | C                    | [Linux][Sim_Lnx], [Windows][Sim_Win] |

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
