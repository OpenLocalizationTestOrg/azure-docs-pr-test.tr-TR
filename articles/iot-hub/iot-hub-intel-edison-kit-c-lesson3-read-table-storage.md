---
title: 'Azure IOT - Ders 3 Connect Intel Edison (C): izleme iletileri | Microsoft Docs'
description: "Azure Table depolama alanına yazılır gibi cihaz bulut iletilerini izleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Bulut, bulut veri koleksiyonu, IOT bulut hizmeti, IOT veri verileri
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: cad545c3-dd88-486c-a663-d587a924ccd4
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 249b5e0e96051fa2adeedfb9befd98fc939b4d40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>İletileri okuma Azure Depolama'da kalıcı
## <a name="what-you-will-do"></a>Ne yapacağını
İletileri Azure Table depolama alanına yazılır gibi Intel Edison'u IOT hub'ına gönderilen cihaz bulut iletilerini izleyin. Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, gulp okuma ileti görevi iletileri, Azure tablo Depolama'da kalıcı okumak için nasıl kullanılacağını öğreneceksiniz.

## <a name="what-you-need"></a>Ne gerekiyor
Bu işlem başlamadan önce başarılı bir şekilde tamamladınız gerekir [Intel Edison'u üzerinde Azure blink örnek uygulamayı çalıştırın][run-the-azure-blink-sample-application-on-intel-edison].

## <a name="read-new-messages-from-your-storage-account"></a>Depolama hesabınızdan yeni iletiler okuma
Önceki makalede örnek bir uygulama üzerinde Edison'u verdi. Azure IOT hub'ınıza örnek uygulama gönderilen iletileri. IOT hub'ına gönderilen iletileri Azure işlev uygulaması aracılığıyla, Azure Table depolama alanına depolanır. Azure Table depolama hesabınızdan iletileri okumak için Azure depolama bağlantı dizesi gerekir.

Azure Table storage'da depolanan iletileri okumak için şu adımları izleyin:

1. Bağlantı dizesi, aşağıdaki komutları çalıştırarak alın:

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   İlk komut alır `storage name` , ikinci komutta bağlantı dizesini almak için kullanılır. Kullanım `iot-sample` değeri olarak `{resource group name}` değeri değiştirirseniz alamadık.
2. Yapılandırma dosyasını açın `config-edison.json` aşağıdaki komutu çalıştırarak Visual Studio Code:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```
3. Değiştir `[Azure storage connection string]` 1. adımda aldığınız bağlantı dizesiyle.
4. Kaydet `config-edison.json` dosya.
5. İletileri yeniden göndermek ve bunları aşağıdaki komutu çalıştırarak, Azure Table depolama alanından okuyun:

   ```bash
   gulp run --read-storage
   ```

   Azure Table depolama veri okuma mantığını bulunduğu `azure-table.js` dosya.

   ![çalıştırma--gulp okuma depolama][gulp run]

## <a name="summary"></a>Özet
Başarılı bir şekilde bulutta IOT hub'ınıza Edison'u bağlı ve cihaz bulut iletilerini göndermek için kullanılan blink örnek uygulama. Azure işlev uygulaması, Azure Table depolama alanına gelen IOT hub iletileri depolamak için de kullanılır. Şimdi, IOT hub'ından Edison'u için bulut cihaz iletileri gönderebilir.

## <a name="next-steps"></a>Sonraki adımlar
[Bulut cihaz iletileri almak için bir örnek uygulamayı çalıştırın][receive-cloud-to-device-messages]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[run-the-azure-blink-sample-application-on-intel-edison]: iot-hub-intel-edison-kit-c-lesson3-run-azure-blink.md
[gulp run]: media/iot-hub-intel-edison-lessons/lesson3/gulp_read_message_c.png
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md