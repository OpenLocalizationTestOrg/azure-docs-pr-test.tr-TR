---
featureFlags: usabilla
title: "Raspberry Pi'yi (düğüm) tooAzure IOT - Ders 3 bağlanın: Tablo depolama | Microsoft Docs"
description: "Azure Table storage'ı tooyour yazıldığı şekilde hello cihaz bulut iletilerini izleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: verileri buluttan, IOT bulut hizmeti
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 9965bd54-61da-479b-aaad-5604850a2be5
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d3c2c8086d3561b7603e18ed00492fcaa0593b87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>İletileri okuma Azure Depolama'da kalıcı
## <a name="what-you-will-do"></a>Ne yapacağını
Merhaba iletileri olarak Raspberry Pi 3 tooyour IOT hub'ından gönderilen İzleyicisi Merhaba cihaz bulut iletilerini tooyour Azure Table depolama yazılır. Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, Azure Table storage ' nasıl toouse Merhaba gulp okuma ileti görevi tooread iletileri kalıcı öğreneceksiniz.

## <a name="what-you-need"></a>Ne gerekiyor
Bu işlem başlamadan önce başarılı bir şekilde tamamladınız gerekir [Raspberry Pi 3'te hello Azure blink örnek uygulamayı çalıştırın](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md).

## <a name="read-new-messages-from-your-storage-account"></a>Depolama hesabınızdan yeni iletiler okuma
Merhaba önceki makalede örnek bir uygulama üzerinde Pi verdi. Merhaba örnek uygulaması tooyour Azure IOT hub'ı iletileri gönderilir. tooyour IOT hub'a gönderilen Merhaba iletileri hello Azure işlev uygulaması aracılığıyla, Azure Table depolama alanına depolanır. Azure Table storage'hello Azure depolama bağlantı dizesi tooread iletileri gerekir.

Azure Table depolama biriminde, depolanan tooread iletiler şu adımları izleyin:

1. Hello bağlantı dizesi hello aşağıdaki komutları çalıştırarak alın:

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   Merhaba ilk komut alır hello `storage name` hello ikinci komutu tooget hello bağlantı dizesi olarak kullanılır. Kullanım `iot-sample` hello değeri olarak `{resource group name}` hello değeri değiştirirseniz alamadık.
2. Açık hello yapılandırma dosyası `config-raspberrypi.json` hello aşağıdaki komutu çalıştırarak Visual Studio Code:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
3. Değiştir `[Azure storage connection string]` 1. adımda aldığınız hello bağlantı dizesine sahip.
4. Merhaba Kaydet `config-raspberrypi.json` dosya.
5. İletileri yeniden göndermek ve bunları hello aşağıdaki komutu çalıştırarak, Azure Table depolama alanından okuyun:
   
   ```bash
   gulp run --read-storage
   ```
   
   Hello Azure Table depolama veri okuma için mantığı olan hello `azure-table.js` dosya.
   
    ![çalıştırma--gulp okuma depolama](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_read_message.png)

## <a name="summary"></a>Özet
Başarıyla Pi tooyour IOT hub'hello bulutta bağlı ve hello blink örnek uygulama toosend cihaz bulut iletilerini kullanılır. Ayrıca, hello Azure işlevi uygulama toostore gelen IOT hub iletileri tooyour Azure Table depolama de kullanılır. Şimdi, IOT hub tooPi bulut-cihaz iletilerini gönderebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
[Merhaba örnek uygulama tooreceive bulut-cihaz iletilerini çalıştırın](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md)

