---
title: "IOT hub'ı nasıl aaaAzure çok | Microsoft Docs"
description: "Bir geliştirici olarak nasıl hello kullanabilirim çeşitli IOT Hub özellikleri?"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: d9c6e25bb332704dee4327bcdc361a299c064130
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-iot-hub"></a>Nasıl toouse Azure IOT Hub

Nasıl toodevelop hello IOT Hub için hizmet çeşitli seçenekler toolearn vardır:

* IOT hub'ı hello özellikleri ayrıntılı açıklamaktadır hello kavramsal makaleleri okuyun.
* IOT Hub'ın çeşitli özellikleri hello kapak hello öğreticileri birini izleyin.

## <a name="developer-guide"></a>Geliştirici kılavuzu

Bir geliştirici olarak hello IOT Hub ile ilgili ayrıntılı kavramsal Kılavuzu okuyabilirsiniz [Geliştirici Kılavuzu][lnk-devguide]. Bu kılavuz içerir:

* Ayrıntılı toolearn nasıl yardımcı tüm IOT hub'ı özelliklerin açıklamaları toouse bunları.
* Nasıl hakkında yönergeler birden çok seçenek kullanılabilir olduğunda toochoose.

## <a name="tutorials"></a>Öğreticiler

Uygulama alıştırmalarını aracılığıyla çalışarak IOT Hub, belirli özelliklerle ilgili toolearn tercih ederseniz, gelen birkaç öğreticileri toochoose vardır. Bu öğreticileri birçoğu, birden fazla programlama dillerinde kullanılabilir. Bu öğreticiler şunları içerir:

- [IOT Hub cihaz-bulut iletileri yolları kullanma][lnk-routes-tutorial]. Bu öğreticide nasıl toouse IOT hub'ı yönlendirme toodispatch cihaz bulut iletilerini bir kolay, yapılandırma tabanlı şekilde kurallar gösterilmiştir.

- [IOT Hub ile bulut-cihaz iletilerini göndermek][lnk-c2d-tutorial]. Bu öğretici ve bulut-cihaz iletilerini bir cihazda nasıl toosend bulut-cihaz IOT hub'ı aracılığıyla iletileri gösterir.

- [IOT Hub ile cihazları toohello buluttan dosyaları karşıya yükleme][lnk-upload-tutorial]. Bu öğretici nasıl toouse hello dosyayı karşıya IOT hub'ı özelliklerini gösterir.

- [Cihaz çiftlerini ile çalışmaya başlama][lnk-twin-tutorial]. Bu öğretici toodevice çiftlerini, bildirilen özellikleri, istenen özellikleri ve etiketleri tanıtır. Cihazlarınızı cihaz çiftlerini toosynchronize değerlerini kullanın.

- [Doğrudan yöntemleri kullanın][lnk-methods-tutorial]. Bu öğretici nasıl toouse doğrudan yöntemleri gösterir. Sanal cihazınız doğrudan bir yöntem için bir işleyici ekleyin ve IOT hub'dan hello doğrudan yöntemi çağırır.

- [Aygıt Management'i kullanmaya başlama][lnk-dm-tutorial]. Bu öğretici nasıl toouse anahtar aygıt yönetimi çiftlerini ve doğrudan yöntemleri gibi özellikleri gösterir. Sanal cihazınız bu özellikleri tooremotely yeniden kullanın.

- [İstenen özelliklerde tooconfigure aygıtları kullanan][lnk-properties-tutorial]. Bu öğretici, nasıl toouse hello cihaz çifti'nın istenen ve Özellikler bildirilen gösterir, tooremotely Cihazınızı yapılandırın.

- [Kullanım Cihaz işleri tooinitiate aygıt üretici yazılımı güncelleştirmesi][lnk-jobs-tutorial]. Bu öğretici nasıl toouse anahtar aygıt yönetimi çiftlerini ve doğrudan yöntemleri gibi özellikleri gösterir. Hakkında bilgi edineceksiniz nasıl toouse bu özellikleri tooremotely aygıtınızın bellenim güncelleştirme.

- [Zamanlama ve yayın işleri][lnk-schedule-tutorial]. Bu öğretici nasıl toouse özellikleri ve doğrudan yöntemleri toointeract ile birden çok cihazda zamanlanmış bir saatte istenen gösterir.

## <a name="next-steps"></a>Sonraki adımlar

toolearn hello IOT Hub hizmeti hakkında daha fazla bilgi görmek hello [Geliştirici Kılavuzu][lnk-devguide].

[lnk-devguide]: ./iot-hub-devguide.md
[lnk-routes-tutorial]: ./iot-hub-csharp-csharp-process-d2c.md
[lnk-c2d-tutorial]: ./iot-hub-csharp-csharp-c2d.md
[lnk-upload-tutorial]: ./iot-hub-csharp-csharp-file-upload.md
[lnk-twin-tutorial]: ./iot-hub-node-node-twin-getstarted.md
[lnk-methods-tutorial]: ./iot-hub-node-node-direct-methods.md
[lnk-dm-tutorial]: ./iot-hub-node-node-device-management-get-started.md
[lnk-properties-tutorial]: ./iot-hub-node-node-twin-how-to-configure.md
[lnk-jobs-tutorial]: ./iot-hub-node-node-firmware-update.md
[lnk-schedule-tutorial]: ./iot-hub-node-node-schedule-jobs.md