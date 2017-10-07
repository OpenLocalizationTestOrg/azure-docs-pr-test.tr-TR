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
# <a name="azure-iot-hub-get-started-with-physical-devices-tutorials"></a>Azure IOT Hub, fiziksel cihazların öğreticileri ile Başlarken

Bu öğreticiler IOT hub'ı tooAzure ve hello cihaz SDK'ları sunar. Merhaba öğreticileri ortak IOT senaryolarını toodemonstrate hello özellikleri IOT Hub'ının kapsar. Merhaba öğreticileri de nasıl toocombine IOT Hub ile diğer Azure hizmetlerini ve toobuild daha araçları göstermeye güçlü IOT çözümleri. Merhaba listelenen öğreticileri aşağıdaki tabloda Göster, nasıl hello toocreate fiziksel IOT cihazları.

| IOT cihaz                       | Programlama dili |
|---------------------------------|----------------------|
| Raspberry Pi                    | [Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]  |
| IOT DevKit                      | [VSCode Arduino][DevKit]     |
| Intel Edison                    | [Node.js][Ed_Nd], [C][Ed_C]           |
| Adafruit yumuşatma HUZZAH ESP8266 | [Arduino][Hu_Ard]              |
| Sparkfun ESP8266 şey geliştirme      | [Arduino][Th_Ard]              |
| Adafruit yumuşatma M0             | [Arduino][M0_Ard]              |

Ayrıca, IOT sınır ağ geçidi tooenable aygıtları tooconnect tooyour IOT hub'ı kullanabilirsiniz.

| Ağ geçidi aygıtı               | Programlama dili | Platform         |
|------------------------------|----------------------|------------------|
| Intel NUC (modeli DE3815TYKE) | C                    | [Rüzgar Akarsu Linux][NUC_Lnx] |

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
