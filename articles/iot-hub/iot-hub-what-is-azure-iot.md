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

## <a name="next-steps"></a>Sonraki adımlar

Azure IoT Hub, çözümünüzün arka ucu ile milyonlarca cihaz arasında düzgün ve güvenli çift yönlü iletişimler sağlayan bir Azure hizmetidir. Merhaba çözüm arka ucuna sağlar:

* Cihazlarınızdan ölçekleyerek telemetri alma.
* Aygıtları tooa akış etkinliği işlemcisine rota verileri.
* Cihazlardan dosya yüklemeleri alma.
* Bulut-cihaz iletilerini toospecific aygıtları gönderin.

Kendi çözüm arka ucu IOT hub'ı tooimplement kullanabilirsiniz. Ayrıca, IOT hub'ı bir kimlik kullanılan kayıt defteri tooprovision cihazları, kendi güvenlik kimlik bilgileri ve bunların haklarını tooconnect toohello IOT hub'ı içerir. IOT hub'ı hakkında daha fazla toolearn bkz [IOT Hub nedir?] [lnk-iot-hub].

Azure IOT Hub, tooremotely yönetmek, yapılandırmak ve aygıtlarınızın güncelleştirmek için standartlara dayalı aygıt yönetimi sağlar nasıl toolearn bkz [cihaz yönetimine genel bakış IOT Hub ile][lnk-device-management].

çok çeşitli cihaz donanım platformları ve işletim sistemleri tooimplement istemci uygulamaları, hello Azure IOT cihaz SDK'ları kullanabilirsiniz. Merhaba cihaz SDK'ları telemetri tooan IOT hub ve alma bulut cihaza iletileri gönderme kolaylaştırmak kitaplıkları içerir. Merhaba cihaz SDK'ları kullandığınızda IOT Hub ile çeşitli ağ protokolleri toocommunicate seçebilirsiniz. toolearn daha, hello fazla [cihaz SDK'ları hakkında bilgi][lnk-device-sdks].

biraz kod yazmaya ve bazı örnekler çalıştıran başlatılan tooget bkz hello [IOT Hub ile çalışmaya başlama] [ lnk-getstarted] Öğreticisi.

Önceden yapılandırılmış çözümler koleksiyonu olan [Azure IoT Paketi][lnk-iot-suite] de ilginizi çekebilir. IOT paketi IOT projelerini tooaddress ortak IOT senaryolarını Uzaktan izleme, varlık yönetimi ve Tahmine dayalı bakım gibi ölçeklendirme ve daha hızlı şekilde kullanmaya tooget sağlar.

[lnk-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-iot-hub]: iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-device-management-overview.md
