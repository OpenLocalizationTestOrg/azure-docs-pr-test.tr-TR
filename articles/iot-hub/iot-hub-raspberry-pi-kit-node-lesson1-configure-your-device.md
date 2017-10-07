---
title: "Raspberry Pi'yi (düğüm) tooAzure IOT - Ders 1 bağlanın: cihaz yapılandırma | Microsoft Docs"
description: "Raspberry Pi 3'ü ilk kez kullanmak için yapılandırmak ve hello Raspbian işletim sistemi, Raspberry Pi'yi donanım hello için en iyi duruma getirilmiş boş bir işletim sistemi yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Yükleme raspbian, raspbian indirme tooinstall raspbian raspbian Kurulum Böğürtlenli pi yükleme raspbian, Böğürtlenli pi yükleme işletim sistemi, Böğürtlenli pi sd kart yükleme, Böğürtlenli pi bağlantı kurma tooraspberry pi Böğürtlenli pi bağlantı bağlanma"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 43f7c2cf-f1a5-4dd5-93f0-7e546c6dc91e
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 504a4d2a3f29717f955530812442cce2a78a6448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a>Cihazınızı yapılandırma
## <a name="what-you-will-do"></a>Ne yapacağını
Pi ilk kez kullanmak için yapılandırmak ve hello Raspbian işletim sistemini yükleyin. Raspbian Raspberry Pi'yi donanım hello için en iyi duruma getirilmiş boş bir işletim sistemi ' dir. Herhangi bir sorun varsa, hello çözümlerini arama [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:

* Nasıl tooinstall Raspbian Pi üzerinde.
* Nasıl bir USB kablosu kullanarak toopower Pi ayarlama.
* Nasıl tooconnect PI toohello ağ bir Ethernet kablolu veya kablosuz ağ kullanarak.
* Nasıl tooadd LED toohello breadboard ve tooPi bağlanın.

## <a name="what-you-will-need"></a>İhtiyacınız olacak
toocomplete bu işlemi Raspberry Pi 3 Starter Seti'nden bölümleri aşağıdaki hello gerekir:

* Merhaba Raspberry Pi 3 Panosu
* Merhaba 16 GB microSD kartı
* Merhaba 6 kaplama alanı mikro USB kablosu ile Merhaba 5-volt 2 amp güç kaynağı
* Merhaba breadboard
* Bağlayıcı kabloları
* 560 ohm Direnç
* Yayılmış 10 mm LED
* Merhaba Ethernet kablosu

![Starter Kit şeyler](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

Şunları da yapmanız gerekir:

* Pi tooconnect için kablolu veya kablosuz bağlantı.
* Bir USB SD bağdaştırıcı veya miniSD kartı tooburn hello işletim sistemi görüntüsünü hello microSD kartı.
* Windows, Mac veya Linux çalıştıran bir bilgisayar. Merhaba, kullanılan tooinstall Raspbian hello microSD kartı bilgisayardır.
* Bir Internet bağlantısı toodownload gerekli araçları ve yazılım hello.

## <a name="install-raspbian-on-hello-microsd-card"></a>Merhaba microSD kartı Raspbian yükleyin
Merhaba microSD kartı hello Raspbian görüntü yüklemesi için hazırlayın.

1. Raspbian indirin.
   1. [Karşıdan](https://www.raspberrypi.org/downloads/raspbian/) Raspbian Jessie piksel ile için hello .zip dosyası.
   2. Bilgisayarınızdaki Hello Raspbian görüntü tooa klasöre ayıklayın.
2. Raspbian toohello microSD kartı yükleyin.
   1. [Karşıdan](https://www.etcher.io) ve hello Etcher SD kart yazıcı yardımcı programını yükleyin.
   2. Etcher çalıştırın ve 1. adımda ayıkladığınız hello Raspbian görüntüsünü seçin.
   3. Merhaba microSD kartı sürücü seçin.
      Etcher zaten hello doğru sürücü seçmiş olabilirsiniz olduğunu unutmayın.
   4. Tıklatın **Flash** tooinstall Raspbian toohello microSD kartı.
   5. Yükleme tamamlandığında hello microSD kartı bilgisayarınızdan kaldırın.
      Etcher otomatik olarak çıkarır veya hello microSD kartı tamamlanmasından sonra çıkarır güvenli tooremove hello microSD kartı doğrudan demektir.
   6. Merhaba microSD kartı Pi yerleştirin.

![Merhaba SD kart Ekle](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a>Pi üzerinde Aç
Pi üzerinde hello mikro USB kablosu ve hello güç kaynağı kullanarak açın.

![Aç](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> En az hello Seti'nde önemli toouse hello güç kaynağı olan 2A toomake, Raspberry yeterli güç toowork doğru olduğundan emin.

## <a name="enable-ssh"></a>SSH etkinleştir
Kasım 2016 sürüm Hello itibariyle hello SSH sunucusu varsayılan olarak devre dışı Raspbian sahiptir. Tooenable gerekir, el ile. Toohello başvurabilir [resmi yönergeleri](https://www.raspberrypi.org/documentation/remote-access/ssh/) veya bir izleyici bağlanmak ve çok Git**Tercihler Raspberry Pi yapılandırma ->** tooenable SSH.

## <a name="connect-raspberry-pi-3-toohello-network"></a>Raspberry Pi 3 toohello ağa bağlan
Pi tooa kablolu ağ veya tooa kablosuz ağa bağlanabilir. Pi bağlı toohello aynı bilgisayarınızda olarak ağ olduğundan emin olun. Örneğin, aynı, bilgisayarın bağlı olduğu anahtar Pi toohello bağlanabilir.

### <a name="connect-tooa-wired-network"></a>Kablolu ağ tooa Bağlan
Merhaba Ethernet kablo tooconnect PI tooyour kablolu ağ kullanın. Merhaba bağlantı kurulamazsa hello Pi üzerinde iki LED'leri etkinleştirin.

![Ethernet kablosu kullanarak bağlanma](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-tooa-wireless-network"></a>Tooa kablosuz ağa bağlan
Merhaba izleyin [yönergeleri](https://www.raspberrypi.org/learning/software-guide/wifi/) hello Raspberry Pi Foundation tooconnect PI tooyour kablosuz ağ üzerinden. Bu yönergeleri gerektiren bir izleyici ve klavye tooPi toofirst bağlanın.

## <a name="connect-hello-led-toopi"></a>Merhaba LED tooPi Bağlan
toocomplete bu görev, kullanım hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard)hello bağlayıcı kablo, LED hello ve hello Direnci. Toohello bağlanmak [genel amaçlı giriş/çıkış](https://www.raspberrypi.org/documentation/usage/gpio/) Pi (GPIO'yu) bağlantı noktaları.

![Breadboard, LED ve Direnç](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. Merhaba kısa Bacak hello LED için çok bağlanmak**GPIO'yu GND (PIN 6)**.
2. Merhaba uzun Bacak hello LED tooone Bacak hello Direnci için için bağlayın.
3. Bağlantı diğer Bacak hello Direnci için çok hello**GPIO'yu 4 (PIN 7)**.

Merhaba LED polarite önemli olduğunu unutmayın. Bu polarite ayarı etkin düşük yaygın olarak bilinir.

![Bağlantı](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

Tebrikler! Pi başarıyla yapılandırdıktan.

## <a name="summary"></a>Özet
Bu makalede, öğrendiğinize tooconfigure nasıl Pi Raspbian, bağlanan Pi tooa ağ, yükleme ve LED tooPi bağlanma. LED henüz açık değil yukarı bu hello unutmayın. Merhaba sonraki tooinstall hello gerekli araçları ve yazılım üzerinde Pi örnek bir uygulamayı çalıştırmak için hazırlanırken bir görevdir.

![Donanım hazır.](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a>Sonraki adımlar
[Merhaba araçları edinin](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

