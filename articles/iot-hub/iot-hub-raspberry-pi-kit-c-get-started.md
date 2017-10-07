---
title: "aaaRaspberry Pi toocloud (C) - bağlanmak Raspberry Pi'yi tooAzure IOT hub'ı | Microsoft Docs"
description: "Bilgi nasıl toosetup ve Bu öğreticide Raspberry Pi'yi toosend veri toohello Azure bulut platformu için Raspberry Pi'yi tooAzure IOT hub'ı bağlanın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure IOT Böğürtlenli Böğürtlenli pi pi IOT hub'ı Böğürtlenli pi gönderme veri toocloud, Böğürtlenli PI toocloud"
ms.assetid: 68c0e730-1dc8-4e26-ac6b-573b217b302d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/12/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 05086890458e196d7fdc87a53fcabb9386245d6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-c"></a>Raspberry Pi'yi tooAzure IoT Hub (C) Bağlan

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

Bu öğreticide, Raspberry Pi'yi ile Raspbian çalıştıran çalışmanın hello temelleri öğrenerek başlayın. Daha sonra nasıl tooseamlessly bağlanacağını aygıtları toohello bulutunuzu kullanarak öğrenin [Azure IOT Hub](iot-hub-what-is-iot-hub.md). Windows 10 IOT Core örnekleri için toohello Git [Windows Geliştirme Merkezi](http://www.windowsondevices.com/).

Bir pakete henüz yok mu? Deneyin [Raspberry Pi'yi çevrimiçi simulator](iot-hub-raspberry-pi-web-simulator-get-started.md). Veya yeni bir paket satın [burada](https://azure.microsoft.com/develop/iot/starter-kits).

## <a name="what-you-do"></a>Neler

* IOT hub'ı oluşturun.
* Bir cihaz IOT hub'ınıza Pi için kaydetme.
* Böğürtlenli PI kurulumu.
* Pi toosend algılayıcı verileri tooyour IOT hub'ına bir örnek uygulamayı çalıştırın.

Oluşturduğunuz Raspberry Pi'yi tooan IOT hub bağlayın. Daha sonra örnek bir uygulama BME280 algılayıcının Pi toocollect sıcaklık ve nem veri üzerinde çalıştırın. Son olarak, hello algılayıcı verileri tooyour IOT hub'ı gönderin.

## <a name="what-you-learn"></a>Öğrenecekleriniz

* Nasıl toocreate Azure IOT hub'ı ve yeni cihaz bağlantı dizenizi alın.
* Nasıl tooconnect ile BME280 algılayıcı Pi.
* Nasıl Pi üzerinde bir örnek uygulamayı çalıştırarak toocollect algılayıcı verileri.
* Nasıl toosend algılayıcı verileri tooyour IOT hub'ı.

## <a name="what-you-need"></a>Ne gerekiyor

![Ne gerekiyor](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

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
   1. [Masaüstü ile Raspbian Jessie karşıdan](https://www.raspberrypi.org/downloads/raspbian/) (Merhaba .zip dosyası).
   1. Bilgisayarınızdaki Hello Raspbian görüntü tooa klasöre ayıklayın.
1. Raspbian toohello microSD kartı yükleyin.
   1. [Merhaba Etcher SD kart yazıcı yardımcı programı yükleyip](https://etcher.io/).
   1. Etcher çalıştırın ve 1. adımda ayıkladığınız hello Raspbian görüntüsünü seçin.
   1. Merhaba microSD kartı sürücü seçin. Etcher zaten hello doğru sürücü seçmiş olabilirsiniz olduğunu unutmayın.
   1. Flash tooinstall Raspbian toohello microSD kartı tıklatın.
   1. Yükleme tamamlandığında hello microSD kartı bilgisayarınızdan kaldırın. Etcher otomatik olarak çıkarır veya hello microSD kartı tamamlanmasından sonra çıkarır güvenli tooremove hello microSD kartı doğrudan demektir.
   1. Merhaba microSD kartı Pi yerleştirin.

### <a name="enable-ssh-and-spi"></a>SSH ve SPI etkinleştir

1. Pi toohello monitör, klavye ve fare bağlanmak, Pi başlatın ve ardından içinde Raspbian kullanarak oturum `pi` hello kullanıcı adı ve `raspberry` hello parola olarak.
1. Merhaba Böğürtlenli simgesine tıklayın > **Tercihler** > **Raspberry Pi yapılandırma**.

   ![Merhaba Raspbian Tercihler menüsü](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. Merhaba üzerinde **arabirimleri** sekmesinde, ayarlamak **SPI** ve **SSH** çok**etkinleştirmek**ve ardından **Tamam**. Fiziksel algılayıcılar varsa ve benzetimli toouse algılayıcı verilerini istediğiniz yok, bu adım isteğe bağlıdır.

   ![SPI ve Böğürtlenli Pi üzerinde SSH etkinleştir](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
tooenable SSH ve SPI bulabilirsiniz daha fazla başvuru belgeleri üzerinde [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) ve [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).

### <a name="connect-hello-sensor-toopi"></a>Merhaba algılayıcı tooPi Bağlan

Merhaba breadboard ve anahtar kablolarını tooconnect bir LED ve BME280 tooPi aşağıdaki şekilde kullanın. Merhaba algılayıcı yoksa [Bu bölüm atlayın](#connect-pi-to-the-network).

![Merhaba Raspberry Pi'yi ve algılayıcı bağlantısı](media/iot-hub-raspberry-pi-kit-c-get-started/3_raspberry-pi-sensor-connection.png)

Merhaba BME280 algılayıcı sıcaklık ve nem verileri toplayabilir. Ve cihaz ve hello bulut arasındaki iletişimi ise hello LED blink. 

Algılayıcı PIN'ler için kablolama aşağıdaki hello kullan:

| Başlangıç (algılayıcı & LED)     | Bitiş (kartı)            | Kablo rengi   |
| -----------------------  | ---------------------- | ------------: |
| LED VDD (PIN 5G)         | GPIO'yu 4 (PIN 7)         | Beyaz kablosu   |
| LED GND (PIN 6G)         | GND (PIN 6)            | Siyah kablosu   |
| VDD (PIN 18F)            | 3, 3v PWR (PIN 17)      | Beyaz kablosu   |
| GND (PIN 20F)            | GND (PIN 20)           | Siyah kablosu   |
| SCK (PIN 21F)            | SPI0 SCLK (PIN 23)     | Turuncu kablosu  |
| SDO (PIN 22F)            | SPI0 MISO (PIN 21)     | Sarı kablosu  |
| SDI (PIN 23F)            | SPI0 MOSI (PIN 19)     | Yeşil kablosu   |
| CS (PIN 24F)             | SPI0 CS (PIN 24)       | Mavi kablosu    |

Tooview tıklatın [Raspberry Pi 2 ve 3 PIN eşlemeleri](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) daha sonra başvurmak üzere.

BME280 tooyour Raspberry Pi'yi başarıyla bağlandıktan sonra görüntü gibi olmalıdır.

![Bağlı Pi ve BME280](media/iot-hub-raspberry-pi-kit-c-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a>Pi toohello ağa bağlan

Pi üzerinde hello mikro USB kablosu ve hello güç kaynağı kullanarak açın. Kullanım hello Ethernet kablo tooconnect PI tooyour kablolu ağ veya hello izleyin [hello Raspberry Pi Foundation yönergeleri](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect PI tooyour kablosuz ağ. Pi başarıyla bağlı toohello ağ sağlandıktan sonra tootake hello Not gereksinim [IP adresi, pi'nin](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).

![Bağlı toowired ağ](media/iot-hub-raspberry-pi-kit-c-get-started/5_power-on-pi.jpg)


## <a name="run-a-sample-application-on-pi"></a>Pi üzerinde bir örnek uygulamayı çalıştırın

### <a name="install-hello-prerequisite-packages"></a>Merhaba önkoşul yükleyin

1. SSH istemcilerini, ana bilgisayar tooconnect tooyour Raspberry Pi'yi aşağıdaki hello birini kullanın.
   
   **Windows kullanıcıları**
   1. İndirme ve yükleme [PuTTY](http://www.putty.org/) Windows için. 
   1. Pi hello ana bilgisayar adı (veya IP adresi) içine bölümünüzü Hello IP adresini kopyalayın ve SSH hello bağlantı türü olarak seçin.
   
   ![PuTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   **Mac ve Ubuntu kullanıcılar**
   
   Ubuntu veya macOS Hello yerleşik SSH İstemcisi'ni kullanın. Toorun gerekebilecek `ssh pi@<ip address of pi>` tooconnect Pi SSH aracılığıyla.
   > [!NOTE] 
   Merhaba varsayılan kullanıcı adı `pi` , ve hello parola `raspberry`.

1. Merhaba önkoşul hello Microsoft Azure IOT cihaz SDK'sı için C ve Cmake hello aşağıdaki komutları çalıştırarak yükleyin:

   ```bash
   grep -q -F 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   grep -q -F 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys FDA6A393E4C2257F
   sudo apt-get update
   sudo apt-get install -y azure-iot-sdk-c-dev cmake libcurl4-openssl-dev git-core
   git clone git://git.drogon.net/wiringPi
   cd ./wiringPi
   ./build
   ```


### <a name="configure-hello-sample-application"></a>Merhaba örnek uygulamayı yapılandırma

1. Merhaba örnek uygulaması hello aşağıdaki komutu çalıştırarak kopyalama:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-client-app
   ```
1. Merhaba yapılandırma dosyası hello aşağıdaki komutları çalıştırarak açın:

   ```bash
   cd iot-hub-c-raspberrypi-client-app
   nano config.h
   ```

   ![Yapılandırma dosyası](media/iot-hub-raspberry-pi-kit-c-get-started/6_config-file.png)

   İki makroları vardır bu dosyada configurate olabilir. Merhaba ilk biridir `INTERVAL`, toocloud Gönder arasında iki iletileri hello zaman aralığı (milisaniye cinsinden) tanımlar. İkinci bir hello `SIMULATED_DATA`, veya toouse algılayıcı verilerini olup benzetimi için bir Boole değeri değil.

   Varsa, **hello algılayıcı yok**ayarlayın hello `SIMULATED_DATA` çok değer`1` toomake Merhaba örnek uygulaması oluşturup benzetimli algılayıcı verilerini kullanabilirsiniz.

1. Kaydedip çıkmak denetimi O tuşlarına basarak > Enter > Denetim X.

### <a name="build-and-run-hello-sample-application"></a>Derleme ve hello örnek uygulamayı çalıştırma

1. Merhaba örnek uygulaması hello aşağıdaki komutu çalıştırarak oluşturun:

   ```bash
   cmake . && make
   ```
   ![Çıktı derleme](media/iot-hub-raspberry-pi-kit-c-get-started/7_build-output.png)

1. Merhaba aşağıdaki komutu çalıştırarak Hello örnek uygulamayı çalıştırın:

   ```bash
   sudo ./app '<DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   Kopyalama hello cihaz bağlantı dizesi hello tek tırnak yapıştırma emin olun.


Gösterir tooyour IOT hub gönderilen algılayıcı verileri ve hello iletileri hello hello aşağıdaki çıktı görmeniz gerekir.

![Çıktı - Raspberry Pi'yi tooyour IOT hub'ından gönderilen algılayıcı verileri](media/iot-hub-raspberry-pi-kit-c-get-started/8_run-output.png)

## <a name="next-steps"></a>Sonraki adımlar

Bir örnek uygulama toocollect algılayıcı verilerini çalıştırdıktan ve tooyour IOT hub'ı gönderebilirsiniz. bkz: Merhaba Raspberry Pi'yi tooyour IOT hub'ı veya gönderme iletileri tooyour Raspberry Pi'yi bir komut satırı arabirimi gönderdiğini toosee hello iletileri [iothub-explorer eğitici Mesajlaşma Yönet bulut cihaz](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
