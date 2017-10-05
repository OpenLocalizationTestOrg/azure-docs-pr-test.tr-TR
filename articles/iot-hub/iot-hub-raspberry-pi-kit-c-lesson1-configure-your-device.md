---
title: "Azure IOT - Ders 1 Connect Raspberry pi (C): cihaz yapılandırma | Microsoft Docs"
description: "Raspberry Pi 3'ü ilk kez kullanmak için yapılandırmak ve Raspberry Pi'yi donanım için en iyi duruma getirilmiş boş bir işletim sistemi Raspbian işletim sistemi yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Yükleme raspbian, raspbian indirme raspbian, raspbian Kurulum, Böğürtlenli pi yükleme raspbian, Böğürtlenli pi yükleme işletim sistemi, Böğürtlenli pi sd kart yükleme, raspberry yüklemek için pi bağlantı kurma Böğürtlenli pi, Böğürtlenli pi bağlantı bağlanma"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8ee9b23c-93f7-43ff-8ea1-e7761eb87a6f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 2a380f78d67db47a0dcab5b90843404921510528
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-device"></a>Cihazınızı yapılandırma
## <a name="what-you-will-do"></a>Ne yapacağını
Pi ilk kez kullanmak için yapılandırmak ve Raspbian işletim sistemini yükleyin. Raspbian Raspberry Pi'yi donanım için en iyi duruma getirilmiş boş bir işletim sistemi ' dir. Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:

* Raspbian Pi üzerinde yükleme.
* Bir USB kablosu kullanarak pi güç yapma.
* Pi ağa bir Ethernet kablolu veya kablosuz ağ kullanarak bağlanma.
* Nasıl bir LED breadboard ekleyin ve Pi bağlanın.

## <a name="what-you-need"></a>Ne gerekiyor
Bu işlemi tamamlamak için aşağıdaki bölümleri Raspberry Pi 3 Starter Seti'nden gerekir:

* Raspberry Pi 3 Panosu
* 16 GB microSD kartı
* 5-volt 2 amp güç kaynağı ile 6 kaplama alanı mikro USB kablosu
* Breadboard
* Bağlayıcı kabloları
* 560 ohm Direnç
* Yayılmış 10 mm LED
* Ethernet kablosu

![Starter Kit şeyler](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

Şunları da yapmanız gerekir:

* Pi bağlanmak için bir kablolu veya kablosuz bağlantı.
* İşletim sistemi görüntüsü microSD kartı üzerine yazmak için bir USB SD bağdaştırıcı veya mini SD kart.
* Windows, Mac veya Linux çalıştıran bir bilgisayar. Bilgisayar üzerinde microSD kartı Raspbian yüklemek için kullanılır.
* Gerekli araçları ve yazılım indirmesi için Internet bağlantısı.

## <a name="install-raspbian-on-the-microsd-card"></a>Raspbian MicroSD kartı yükleyin
MicroSD kartı Raspbian görüntünün yüklenmesi için hazırlayın.

1. Raspbian indirin.
   1. [Karşıdan](https://www.raspberrypi.org/downloads/raspbian/) Raspbian Jessie piksel ile .zip dosyası.
   2. Raspbian görüntünün bilgisayarınızdaki bir klasöre ayıklayın.
2. Raspbian microSD kartı yükleyin.
   1. [Karşıdan](https://www.etcher.io) ve Etcher SD kart yazıcı yardımcı programını yükleyin.
   2. Etcher çalıştırın ve 1. adımda ayıkladığınız Raspbian görüntüyü seçin.
   3. MicroSD kartı sürücü seçin.
      Etcher zaten doğru sürücü seçmiş olabilirsiniz olduğunu unutmayın.
   4. Tıklatın **Flash** Raspbian microSD kartı yüklemek için.
   5. Yükleme tamamlandığında microSD kartı bilgisayarınızdan kaldırın.
      Etcher otomatik olarak çıkarır veya tamamlanmasından sonra microSD kartı çıkarır çünkü microSD kartı doğrudan kaldırmak güvenlidir.
   6. MicroSD kartı, Pi yerleştirin.

![SD kart Ekle](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a>Pi üzerinde Aç
Pi üzerinde mikro USB kablosu ve güç kaynağı kullanarak açın.

![Aç](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> En az Seti'nde güç kaynağı kullanmak önemlidir 2A, Raspberry düzgün çalışması için yeterli güç olduğundan emin olun.

## <a name="enable-ssh"></a>SSH etkinleştir
Kasım 2016 güncelleştirmesinden itibaren Raspbian varsayılan olarak devre dışı SSH sunucusu vardır. El ile etkinleştirmeniz gerekir. Başvurabilirsiniz [resmi yönergeleri](https://www.raspberrypi.org/documentation/remote-access/ssh/) veya bir izleyici bağlanmak ve Git **Tercihler Raspberry Pi yapılandırma ->** SSH etkinleştirmek için.

## <a name="connect-raspberry-pi-3-to-the-network"></a>Raspberry Pi 3 ağa bağlanın
Pi kablolu veya kablosuz ağa bağlanabilir. Pi bilgisayarınızın aynı ağa bağlı olduğundan emin olun. Örneğin, Pi, bilgisayarın bağlı olduğu aynı anahtara bağlanabilir.

### <a name="connect-to-a-wired-network"></a>Kablolu bir ağa bağlan
Pi kablolu ağa bağlamak için Ethernet kablosu kullanın. Bağlantı kurulamazsa Pi üzerinde iki LED'leri etkinleştirin.

![Ethernet kablosu kullanarak bağlanma](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-to-a-wireless-network"></a>Kablosuz bir ağa bağlan
İzleyin [yönergeleri](https://www.raspberrypi.org/learning/software-guide/wifi/) Pi kablosuz ağınıza bağlanmak için Raspberry Pi Foundation gelen. Bu yönergeleri Pi bir izleyici ve klavye ilk bağlanmanızı gerektirir.

## <a name="connect-the-led-to-pi"></a>Pi LED Bağlan
Bu görevi tamamlamak için kullanmak [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), bağlayıcı kablo, LED ve Direnci. Kendilerine bağlanması [genel amaçlı giriş/çıkış](https://www.raspberrypi.org/documentation/usage/gpio/) Pi (GPIO'yu) bağlantı noktaları.

![Breadboard, LED ve Direnç](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. Daha kısa Bacak LED için bağlanmak **GPIO'yu GND (PIN 6)**.
2. LED uzun bacaktaki Direnci bir bacağı için bağlayın.
3. Diğer Bacak Direnci için bağlanmak **GPIO'yu 4 (PIN 7)**.

LED polarite önemli olduğunu unutmayın. Bu polarite ayarı etkin düşük yaygın olarak bilinir.

![Bağlantı](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

Tebrikler! Pi başarıyla yapılandırdıktan.

## <a name="summary"></a>Özet
Bu makalede, Raspbian yükleyerek, Pi ağa bağlanma ve bir LED Pi bağlanma Pi yapılandırma öğrendiniz. LED henüz açık değil yukarı unutmayın. Sonraki hazırlık Pi üzerinde örnek bir uygulamayı çalıştırmak için gerekli araçları ve yazılım yüklemek için bir görevdir.

![Donanım hazır.](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a>Sonraki adımlar
[Araçları edinin](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

