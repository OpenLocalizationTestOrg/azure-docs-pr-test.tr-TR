---
title: 'Azure IOT - Ders 3 Connect Raspberry pi (C): Tablo depolama | Microsoft Docs'
description: "Azure Table depolama alanına yazılır gibi cihaz bulut iletilerini izleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: verileri buluttan, IOT bulut hizmeti
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8c5558bb-3c31-4445-90e6-b1a978738545
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 16b7f2e38bfe3b40d199cb6e07976433aa54ea32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>İletileri okuma Azure Depolama'da kalıcı
## <a name="what-you-will-do"></a>Ne yapacağını
İletileri Azure Table depolama alanına yazılır gibi Raspberry Pi 3 veya IOT hub'ına gönderilen cihaz bulut iletilerini izleyin. Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, gulp okuma ileti görevi iletileri, Azure tablo Depolama'da kalıcı okumak için nasıl kullanılacağını öğreneceksiniz.

## <a name="what-you-need"></a>Ne gerekiyor
Bu işlem başlamadan önce başarılı bir şekilde tamamladınız gerekir [Raspberry Pi 3'te Azure blink örnek uygulamayı çalıştırın](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md).

## <a name="read-new-messages-from-your-storage-account"></a>Depolama hesabınızdan yeni iletiler okuma
Önceki makalede örnek bir uygulama üzerinde Pi verdi. Azure IOT hub'ınıza örnek uygulama gönderilen iletileri. IOT hub'ına gönderilen iletileri Azure işlev uygulaması aracılığıyla, Azure Table depolama alanına depolanır. Azure Table depolama hesabınızdan iletileri okumak için Azure depolama bağlantı dizesi gerekir.

Azure Table storage'da depolanan iletileri okumak için şu adımları izleyin:

1. Bağlantı dizesi, aşağıdaki komutları çalıştırarak alın:

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   İlk komut alır `storage name` , ikinci komutta bağlantı dizesini almak için kullanılır. Kullanım `iot-sample` değeri olarak `{resource group name}` değeri değiştirirseniz alamadık.
2. Yapılandırma dosyasını açın `config-raspberrypi.json` aşağıdaki komutu çalıştırarak Visual Studio Code:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
3. Değiştir `[Azure storage connection string]` 1. adımda aldığınız bağlantı dizesiyle.
4. Kaydet `config-raspberrypi.json` dosya.
5. İletileri yeniden göndermek ve bunları aşağıdaki komutu çalıştırarak, Azure Table depolama alanından okuyun:
   
   ```bash
   gulp run --read-storage
   ```
   
   Azure Table depolama veri okuma mantığını bulunduğu `azure-table.js` dosya.
   
   ![çalıştırma--gulp okuma depolama](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_read_message_c.png)

## <a name="summary"></a>Özet
Başarılı bir şekilde bulutta IOT hub'ınıza Pi bağlı ve cihaz bulut iletilerini göndermek için kullanılan blink örnek uygulama. Azure işlev uygulaması, Azure Table depolama alanına gelen IOT hub iletileri depolamak için de kullanılır. Şimdi, IOT hub'ından Pi bulut cihaz iletileri gönderebilir.

## <a name="next-steps"></a>Sonraki adımlar
[Bulut cihaz iletileri almak için bir örnek uygulamayı çalıştırın](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md)

