---
title: "Connect Arduino (C) tooAzure IOT - Ders 1: cihaz yapılandırma | Microsoft Docs"
description: "Adafruit yumuşatma M0 WiFi ilk kez kullanmak için yapılandırın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "ayarlama, arduino bağlanmak arduino toopc, Kurulum arduino, arduino Panosu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: f5b334f0-a148-41aa-b374-ce7b9f5b305a
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 30b764e8ff6221995456283a226e79f064b2d74e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a>Cihazınızı yapılandırma
## <a name="what-you-will-do"></a>Ne yapacağını
Merhaba Panosu, Yukarı başlatırken birleştirerek Adafruit yumuşatma M0 WiFi Arduino panonuzu ilk kez kullanmak için yapılandırın. Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).

## <a name="what-you-need"></a>Ne gerekiyor
toocomplete bu işlem, Adafruit yumuşatma M0 WiFi Starter Kit için bölümleri aşağıdaki hello gerekir:

* Merhaba Adafruit yumuşatma M0 WiFi Panosu
* Mikro B tooType bir USB kablosu

![Seti][kit]

Şunları da yapmanız gerekir:

* Windows, Mac veya Linux çalıştıran bir bilgisayar.
* Kablosuz bağlantı, Arduino Panosu tooconnect için.
* Bir Internet bağlantısı toodownload yapılandırma aracı.

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:

* Nasıl tooassemble Arduino kurulu ve güç, aşağıdaki hello kaydınızı dersler.
* Nasıl Ubuntu tooadd seri bağlantı noktası izinleri.

## <a name="connect-your-arduino-board-tooyour-computer"></a>Arduino tablosu tooyour bilgisayarınızı bağlayın

1. Merhaba mikro USB kablosu hello üst mikro USB bağlantı noktasına takın.

   ![Üst mikro USB bağlantı noktası][top-micro-usb-port]

2. Tak bilgisayarınıza USB kablosu diğer ucundaki hello.

   ![Bilgisayar USB][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a>Seri bağlantı noktası izinleri üzerinde Ubuntu ekleyin

Windows veya macOS kullanırsanız, bu bölümü atlayabilirsiniz. Ubuntu için aşağıdaki adımları toomake hello normal linux kullanıcı hello izinleri toooperate Arduino panosunun hello USB bağlantı noktasına sahip olduğundan emin hello gerekir.

1. Terminal artık normal olarak kullanıcıdan:

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   Aşağıdakine benzer alırsınız:

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   "0" Merhaba farklı bir numara olabilir veya birden çok giriş döndürdü. İhtiyacımız hello ilk örneği hello verilerde `uucp`, hello ikinci olan `dialout`, hello dosyanın hello Grup sahibi olduğu.

2. Kullanıcı toohello toohello grubu Ekle:

   ```bash
   sudo usermod -a -G group-name username
   ```

   Burada `group-name` hello veri hello ilk adımda bulundu ve `username` linux kullanıcı adınızdır.

3. Bu değişikliğin tootake ve tam hello kurulumu için toolog oturumunuzu kapatıp tekrar gerekir.

## <a name="summary"></a>Özet
Bu makalede, öğrendiğinize nasıl tooconfigure Arduino panonuz. Merhaba sonraki tooinstall hello gerekli araçları ve yazılım Arduino Panonuzda örnek bir uygulamayı çalıştırmak için hazırlanırken bir görevdir.

![Donanım hazır.][hardware-is-ready]

## <a name="next-steps"></a>Sonraki adımlar
[Merhaba araçları edinin][get-the-tools]
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md