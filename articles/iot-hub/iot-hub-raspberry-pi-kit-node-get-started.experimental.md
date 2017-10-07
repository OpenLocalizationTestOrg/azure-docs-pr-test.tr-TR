---
title: "aaaRaspberry Pi toocloud (Node.js) - bağlanmak Raspberry Pi'yi tooAzure IOT hub'ı | Microsoft Docs"
description: "Raspberry Pi'yi toosend veri toohello Azure bulut için Raspberry Pi'yi tooAzure IOT hub'ı bağlayın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure IOT Böğürtlenli Böğürtlenli pi pi IOT hub'ı Böğürtlenli pi gönderme veri toocloud, Böğürtlenli PI toocloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/27/2017
ms.author: xshi
ms.openlocfilehash: 07bc66983c427eab8118be18d91abb25deb03ad3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-nodejs"></a>Raspberry Pi'yi tooAzure IOT hub'ı (Node.js) bağlanma

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

Bu öğreticide, Raspberry Pi'yi ile Raspbian çalıştıran çalışmanın hello temelleri öğrenerek başlayın. Daha sonra nasıl tooseamlessly bağlanacağını aygıtları toohello bulutunuzu kullanarak öğrenin [Azure IOT Hub](iot-hub-what-is-iot-hub.md). Windows 10 IOT Core örnekleri için toohello Git [Windows Geliştirme Merkezi](http://www.windowsondevices.com/).

Bir pakete henüz yok mu? Merhaba deneyin [Raspberry Pi 3 öykünücü](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/). Veya yeni bir paket satın [burada](https://azure.microsoft.com/develop/iot/starter-kits).

## <a name="what-you-do"></a>Neler

* Böğürtlenli PI kurulumu.
* IOT hub'ı oluşturun.
* Bir cihaz IOT hub'ınıza Pi için kaydetme.
* Pi toosend algılayıcı verileri tooyour IOT hub'ına bir örnek uygulamayı çalıştırın.

Oluşturduğunuz Raspberry Pi'yi tooan IOT hub bağlayın. Daha sonra örnek bir uygulama BME280 algılayıcının Pi toocollect sıcaklık ve nem veri üzerinde çalıştırın. Son olarak, hello algılayıcı verileri tooyour IOT hub'ı gönderin.

## <a name="what-you-learn"></a>Öğrenecekleriniz

* Nasıl toocreate Azure IOT hub'ı ve yeni cihaz bağlantı dizenizi alın.
* Nasıl tooconnect ile BME280 algılayıcı Pi.
* Nasıl Pi üzerinde bir örnek uygulamayı çalıştırarak toocollect algılayıcı verileri.
* Nasıl toosend algılayıcı verileri tooyour IOT hub'ı.

## <a name="what-you-need"></a>Ne gerekiyor

![Ne gerekiyor](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* Merhaba Raspberry Pi 2 veya Raspberry Pi 3 Panosu.
* Etkin bir Azure aboneliği. Bir Azure hesabınız yoksa [ücretsiz Azure deneme hesabı oluşturma](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.
* Bir izleyici, bir USB klavye ve fare tooPi bağlanan.
* Mac veya Windows veya Linux çalıştıran bir bilgisayar.
* Bir Internet bağlantısı.
* 16 GB veya üzeri microSD kartı.
* Bir USB SD bağdaştırıcı veya microSD kartı tooburn hello işletim sistemi görüntüsünü hello microSD kartı.
* 5-volt 2 amp güç hello 6 kaplama alanı mikro USB kablosu ile sağlayın.

Aşağıdaki öğelerindeki hello isteğe bağlıdır:

* Bir birleştirilmiş Adafruit BME280 sıcaklık, baskısı ve nem algılayıcı.
* Bir breadboard.
* 6 F/M anahtar kablolarını.
* Yayılmış 10 mm LED.

  > [!NOTE] 
  Merhaba kod örnek desteği algılayıcı verilerini benzetimli çünkü bu öğeler isteğe bağlıdır.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a>Böğürtlenli PI Kurulumu

### <a name="install-hello-raspbian-operating-system-for-pi"></a>Pi için Hello Raspbian işletim sistemini yükleme

Merhaba microSD kartı hello Raspbian görüntü yüklemesi için hazırlayın.

1. Raspbian indirin.
   1. [Piksel ile Raspbian Jessie karşıdan](https://www.raspberrypi.org/downloads/raspbian/) (Merhaba .zip dosyası).
   1. Bilgisayarınızdaki Hello Raspbian görüntü tooa klasöre ayıklayın.
1. Raspbian toohello microSD kartı yükleyin.
   1. [Merhaba Etcher SD kart yazıcı yardımcı programı yükleyip](https://etcher.io/).
   1. Etcher çalıştırın ve 1. adımda ayıkladığınız hello Raspbian görüntüsünü seçin.
   1. Merhaba microSD kartı sürücü seçin. Etcher zaten hello doğru sürücü seçmiş olabilirsiniz olduğunu unutmayın.
   1. Flash tooinstall Raspbian toohello microSD kartı tıklatın.
   1. Yükleme tamamlandığında hello microSD kartı bilgisayarınızdan kaldırın. Etcher otomatik olarak çıkarır veya hello microSD kartı tamamlanmasından sonra çıkarır güvenli tooremove hello microSD kartı doğrudan demektir.
   1. Merhaba microSD kartı Pi yerleştirin.

### <a name="enable-ssh-and-i2c"></a>SSH ve I2C etkinleştir

1. Pi toohello monitör, klavye ve fare bağlanmak, Pi başlatın ve ardından içinde Raspbian kullanarak oturum `pi` hello kullanıcı adı ve `raspberry` hello parola olarak.
1. Merhaba Böğürtlenli simgesine tıklayın > **Tercihler** > **Raspberry Pi yapılandırma**.

   ![Merhaba Raspbian Tercihler menüsü](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. Merhaba üzerinde **arabirimleri** sekmesinde, ayarlamak **I2C** ve **SSH** çok**etkinleştirmek**ve ardından **Tamam**. Fiziksel algılayıcılar varsa ve benzetimli toouse algılayıcı verilerini istediğiniz yok, bu adım isteğe bağlıdır.

   ![I2C ve Böğürtlenli Pi üzerinde SSH etkinleştir](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
tooenable SSH ve I2C bulabilirsiniz daha fazla başvuru belgeleri üzerinde [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) ve [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).

### <a name="connect-hello-sensor-toopi"></a>Merhaba algılayıcı tooPi Bağlan

Merhaba breadboard ve anahtar kablolarını tooconnect bir LED ve BME280 tooPi aşağıdaki şekilde kullanın. Merhaba algılayıcı yoksa bu bölümü atlayabilirsiniz.

![Merhaba Raspberry Pi'yi ve algılayıcı bağlantısı](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

Merhaba BME280 algılayıcı sıcaklık ve nem verileri toplayabilir. Ve cihaz ve hello bulut arasındaki iletişimi ise hello LED blink. 

Algılayıcı PIN'ler için kablolama aşağıdaki hello kullan:

| Başlangıç (algılayıcı & LED)     | Bitiş (kartı)            | Kablo rengi   |
| -----------------------  | ---------------------- | ------------: |
| VDD (PIN 5G)             | 3, 3v PWR (PIN 1)       | Beyaz kablosu   |
| GND (PIN 7G)             | GND (PIN 6)            | Kahverengi kablosu   |
| SCK (PIN 8G)             | I2C1 SDA (PIN 3)       | Turuncu kablosu  |
| SDI (PIN 10G)            | I2C1 SCL (PIN 5)       | Kırmızı kablosu     |
| LED VDD (PIN 18F)        | GPIO'yu 24 (PIN 18)       | Beyaz kablosu   |
| LED GND (PIN 17F)        | GND (PIN 20)           | Siyah kablosu   |

Tooview tıklatın [Raspberry Pi 2 ve 3 PIN eşlemeleri](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) daha sonra başvurmak üzere.

BME280 tooyour Raspberry Pi'yi başarıyla bağlandıktan sonra görüntü gibi olmalıdır.

![Bağlı Pi ve BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a>Pi toohello ağa bağlan

Pi üzerinde hello mikro USB kablosu ve hello güç kaynağı kullanarak açın. Kullanım hello Ethernet kablo tooconnect PI tooyour kablolu ağ veya hello izleyin [hello Raspberry Pi Foundation yönergeleri](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect PI tooyour kablosuz ağ. Pi başarıyla bağlı toohello ağ sağlandıktan sonra tootake hello Not gereksinim [IP adresi, pi'nin](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).

![Bağlı toowired ağ](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> Pi bağlı toohello aynı bilgisayarınızda olarak ağ olduğundan emin olun. Pi kablolu ağ bağlantılı tooa olsa da, bilgisayarınız bağlı tooa kablosuz ağ ise, örneğin, size hello IP göremeyebilirsiniz hello devdisco çıkış adresi.

## <a name="run-a-sample-application-on-pi"></a>Pi üzerinde bir örnek uygulamayı çalıştırın

### <a name="clone-sample-application-and-install-hello-prerequisite-packages"></a>Örnek uygulama kopyalamak ve hello önkoşul yükleyin

1. SSH istemcilerini, ana bilgisayar tooconnect tooyour Raspberry Pi'yi aşağıdaki hello birini kullanın.
    - [PuTTY](http://www.putty.org/) Windows için. Pi tooconnect hello IP adresine ihtiyacınız, SSH aracılığıyla.
    - Merhaba yerleşik SSH istemcisi Ubuntu veya macOS. Çalıştırma `ssh pi@<ip address of pi>` tooconnect Pi SSH aracılığıyla.

   > [!NOTE] 
   Merhaba varsayılan kullanıcı adı `pi` , ve hello parola `raspberry`.

1. Node.js ve NPM tooyour Pi yükleyin.
   
   İlk komut aşağıdaki hello ile Node.js sürümünüzü kontrol etmeniz gerekir. 
   
   ```bash
   node -v
   ```

   Merhaba sürüm 4.x düşük olduğu veya, Pi üzerinde hiçbir Node.js komut tooinstall aşağıdaki hello çalıştırmak veya Node.js güncelleştirin.

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. Merhaba örnek uygulaması hello aşağıdaki komutu çalıştırarak kopyalama:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. Tüm paketler komutu aşağıdaki hello tarafından yükleyin. Azure IOT cihaz SDK'sı, BME280 algılayıcı kitaplığı ve geriye Pi kitaplığı içerir.

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   Bu işlem, ağ bağlantısı üzerinde bu yükleme işlemini denpening birkaç dakika toofinish sürebilir.

### <a name="configure-hello-sample-application"></a>Merhaba örnek uygulamayı yapılandırma

1. Merhaba yapılandırma dosyası hello aşağıdaki komutları çalıştırarak açın:

   ```bash
   nano config.json
   ```

   ![Yapılandırma dosyası](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   İki öğe bu dosyada configurate olabilir. Merhaba ilk biridir `interval`, toocloud Gönder iki ileti arasındaki hello zaman aralığını tanımlar. İkinci bir hello `simulatedData`, veya toouse algılayıcı verilerini olup benzetimi için bir Boole değeri değil.

   Varsa, **hello algılayıcı yok**ayarlayın hello `simulatedData` çok değer`true` toomake Merhaba örnek uygulaması oluşturup benzetimli algılayıcı verilerini kullanabilirsiniz.

1. Kaydedip çıkmak denetimi O tuşlarına basarak > Enter > Denetim X.

### <a name="run-hello-sample-application"></a>Merhaba örnek uygulamayı çalıştırın

1. Merhaba aşağıdaki komutu çalıştırarak Hello örnek uygulamayı çalıştırın:

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   Kopyalama hello cihaz bağlantı dizesi hello tek tırnak yapıştırma emin olun.


Gösterir tooyour IOT hub gönderilen algılayıcı verileri ve hello iletileri hello hello aşağıdaki çıktı görmeniz gerekir.

![Çıktı - Raspberry Pi'yi tooyour IOT hub'ından gönderilen algılayıcı verileri](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a>Sonraki adımlar

Bir örnek uygulama toocollect algılayıcı verilerini çalıştırdıktan ve tooyour IOT hub'ı gönderebilirsiniz.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]