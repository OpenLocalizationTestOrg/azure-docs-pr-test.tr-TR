---
title: "M0 toocloud: yumuşatma M0 WiFi tooAzure IOT hub'ı bağlanma | Microsoft Docs"
description: "Bilgi nasıl tooset yukarı ve Bu öğreticide Adafruit yumuşatma M0 WiFi tooAzure IOT hub'ı toosend veri toohello Azure bulut platformu bağlanın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 51befcdb-332b-416f-a6a1-8aabdb67f283
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/16/2017
ms.author: xshi
ms.openlocfilehash: 6aabeb961a50ba5d3934f77eb1ccda4af1bf64c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-m0-wifi-tooazure-iot-hub-in-hello-cloud"></a>Adafruit yumuşatma M0 WiFi tooAzure IOT Hub'hello bulutta Bağlan
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![BME280, yumuşatma M0 WiFi ve IOT hub'ı arasında bir bağlantı](media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

Bu öğreticide, Arduino panonuzu ile çalışmanın hello temelleri öğrenerek başlayın. Daha sonra nasıl tooseamlessly bağlanacağını aygıtları toohello bulutunuzu kullanarak öğrenin [Azure IOT Hub](iot-hub-what-is-iot-hub.md).

## <a name="what-you-do"></a>Neler

Oluşturduğunuz Adafruit yumuşatma M0 WiFi tooan IOT hub bağlayın. Daha sonra örnek bir uygulama BME280 sıcaklık ve nem M0 WiFi toocollect hello verileri çalıştırın. Son olarak, hello algılayıcı verileri tooyour IOT hub'ı gönderin.


## <a name="what-you-learn"></a>Öğrenecekleriniz

* Nasıl toocreate IOT hub'ı ve yumuşatma M0 WiFi için bir cihaz kaydetme
* Nasıl tooconnect yumuşatma M0 WiFi hello algılayıcı ve bilgisayarınız
* Nasıl yumuşatma M0 WiFi üzerinde bir örnek uygulamayı çalıştırarak toocollect algılayıcı verileri
* Nasıl toosend hello algılayıcı verileri tooyour IOT hub'ı

## <a name="what-you-need"></a>Ne gerekiyor

![Merhaba öğretici için gerekli bölümleri](media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete bu işlemi yumuşatma M0 WiFi Starter Seti'nden bölümleri aşağıdaki hello gerekir:

* Merhaba yumuşatma M0 WiFi Panosu
* Mikro USB tooType bir USB kablosu

Ayrıca geliştirme ortamınız için öğeleri izleyen hello gerekir:

* Etkin bir Azure aboneliği. Bir Azure hesabınız yoksa [ücretsiz Azure deneme hesabı oluşturma](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.
* Mac veya Windows veya Ubuntu çalıştıran bir bilgisayar.
* Kablosuz ağ yumuşatma M0 WiFi tooconnect için.
* Bir Internet bağlantısı toodownload hello yapılandırma aracı.
* [Arduino IDE](https://www.arduino.cc/en/main/software) sürüm 1.6.8 veya sonraki bir sürümü. Önceki sürümlerde hello Azure IOT Hub kitaplığı ile çalışmaz.

Algılayıcı yoksa, aşağıdaki öğelerindeki hello isteğe bağlıdır. Benzetimli algılayıcı verilerini kullanarak hello seçeneğiniz de vardır:

* BME280 sıcaklık ve nem algılayıcı
* Bir breadboard
* M/M anahtar kabloları

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-hello-sensor-and-your-computer"></a>Merhaba algılayıcı ve bilgisayarınızla yumuşatma M0 WiFi Bağlan
Bu bölümde, hello algılayıcılar tooyour Panosu bağlayın. Ardından aygıt tooyour bilgisayarınızdaki başka kullanmak için takın.

### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-m0-wifi"></a>Bir DHT22 sıcaklık ve nem algılayıcı tooFeather M0 WiFi Bağlan

Merhaba breadboard ve anahtar kablolarını toomake hello bağlantısı kullanın. Algılayıcı yoksa, benzetimli algılayıcı verilerini yerine kullandığından bu bölümü atlayabilirsiniz.

![Bağlantı Başvurusu](media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


Algılayıcı PIN'ler için kablolama aşağıdaki hello kullan:


| Başlangıç (algılayıcı)           | Bitiş (kartı)            | Kablo rengi   |
| -----------------------  | ---------------------- | ------------: |
| VDD (PIN 27A)            | 3v (PIN 3A)            | Kırmızı kablosu     |
| GND (PIN 29A)            | GND (PIN 6A)           | Siyah kablosu   |
| SCK (PIN 30A)            | SCK (PIN 12A)          | Sarı kablosu  |
| SDO (PIN 31A)            | MI (PIN 14A)           | Beyaz kablosu   |
| SDI (PIN 32A)            | M0 (PIN 13A)           | Mavi kablosu    |
| CS (PIN 33A)             | GPIO'yu 5 (PIN 15J)       | Turuncu kablosu  |

Daha fazla bilgi için bkz: [Adafruit BME280 nem + Barometric baskısı sıcaklık algılayıcısı oturumdan](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) ve [Adafruit yumuşatma M0 WiFi no'lu](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).



Şimdi yumuşatma M0 WiFi ile çalışma algılayıcı bağlı olması gerekir.

![Yumuşatma Huzzah ile DHT22 Bağlan](media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-tooyour-computer"></a>Yumuşatma M0 WiFi tooyour bilgisayara bağlanma

Merhaba mikro USB tooType bir USB kablosu tooconnect yumuşatma M0 WiFi tooyour bilgisayar, gösterildiği gibi kullanın:

![Yumuşatma Huzzah tooyour bilgisayara bağlanma](media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a>Seri bağlantı noktası izinleri (yalnızca Ubuntu) ekleyin

Ubuntu kullanırsanız, hello izinleri toooperate hello USB bağlantı noktası, yumuşatma M0 WiFi üzerinde olduğundan emin olun. tooadd seri bağlantı noktası izinleri, aşağıdaki adımları uygulayın:


1. Bir terminal hello aşağıdaki komutları çalıştırın:

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   Çıktı aşağıdaki hello birini alın:

   * crw-rw---1 kök uucp xxxxxxxx
   * crw-rw---1 kök araması xxxxxxxx

   Merhaba çıktısında dikkat `uucp` veya `dialout` hello Grup sahibi hello USB bağlantı noktasına adıdır.

2. komutu aşağıdaki hello çalıştırmak tooadd hello kullanıcı toohello grubunun:

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   Merhaba önceki adımda aldığınız hello Grup sahibi adı `<group-owner-name>`. Ubuntu kullanıcı adınız `<username>`.

3. Merhaba değişiklik tooappear dışında Ubuntu oturum ve yeniden oturum açın.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>Algılayıcı verilerini toplamak ve tooyour IOT hub'ı gönderin

Bu bölümde, dağıtın ve yumuşatma M0 WiFi üzerinde bir örnek uygulamayı çalıştırın. Merhaba örnek uygulaması yumuşatma M0 WiFi ışığı yanıp hello yapar. Ardından hello sıcaklık gönderir ve nem veri hello BME280 algılayıcı tooyour IOT hub'ı toplanmadı.

### <a name="get-hello-sample-application-from-github-and-prepare-hello-arduino-ide"></a>Merhaba örnek uygulaması Github'dan alma ve hello Arduino IDE hazırlama

Merhaba örnek uygulaması, GitHub üzerinde barındırılır. Merhaba örnek uygulaması github'dan içeren hello örnek depoyu kopyalayın. tooclone hello örnek deposu, şu adımları izleyin:

1. Bir komut istemi veya terminal penceresi açın.

2. Depolanan hello örnek uygulama toobe istediğiniz tooa klasörüne gidin.
3. Merhaba aşağıdaki komutu çalıştırın:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

### <a name="install-hello-package-for-feather-m0-wifi-in-hello-arduino-ide"></a>Merhaba paketini yumuşatma M0 WiFi hello Arduino IDE yükleyin.

1. Merhaba örnek uygulaması depolandığı hello klasörünü açın.

2. Merhaba Arduino IDE hello uygulama klasöründe Hello app.ino dosyasını açın.

   ![Merhaba örnek uygulaması Arduino IDE içinde açın](media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)


1. Tıklatın **dosya** > **Tercihler** (Windows/Linux) veya **Arduino** > **Tercihler** (Mac) kopyalayıp ve Merhaba aşağıda Yapıştır hello bağlantıya **ek panoları yöneticisi URL'leri** Arduino IDE Tercihler hello seçeneği.
   
   ```
   https://adafruit.github.io/arduino-board-index/package_adafruit_index.json, https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```

1. Tıklatın **Araçları** > **Panosu** > **panoları Yöneticisi**, yükleyip ardından hello `Arduino SAMD Boards` sürüm `1.6.2` veya üstü. 

1. Ardından Merhaba aynı penceresi, yükleme `Adafruit SAMD Boards` paketini tooadd hello Panosu dosya tanımları.

   ![Merhaba esp8266 paketinin yüklü olduğu](media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

4. Tıklatın **Araçları** > **Panosu** > **Adafruit M0 WiFi**.

5. Sürücüleri (yalnızca Windows için) yükleyin. Yumuşatma M0 WiFi taktığınızda tooinstall bir sürücü gerekebilir. Tıklatın [hello indirme bağlantısı hello Web sayfasındaki](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) toodownload hello sürücü yükleyicisi. Merhaba adımları tooinstall hello sürücüleri istediğiniz izleyin.

### <a name="install-necessary-libraries"></a>Gerekli kitaplıkları yükleme

1. Hello Arduino IDE, tıklatın **taslak** > **dahil Kitaplığı** > **yönetmek kitaplıkları**.

2. Kitaplık adları tek tek aşağıdaki hello arayın. Bulduğunuz her kitaplığını tıklatın **yükleme**:

   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

3. El ile yüklemeniz `Adafruit_WINC1500`. Çok Git[bu Web sitesi](https://github.com/adafruit/Adafruit_WINC1500) tıklatıp **Kopyala veya indir** > **ZIP'i indir**. Arduino IDE'yi çok Git**taslak** > **dahil Kitaplığı** > **.zip Kitaplığı eklemek** ve hello zip dosyası ekleyin.

### <a name="use-hello-sample-application-if-you-dont-have-a-real-bme280-sensor"></a>Gerçek BME280 algılayıcı yoksa Merhaba örnek uygulaması kullanın

Gerçek BME280 algılayıcı yoksa, hello örnek uygulama sıcaklık ve nem veri benzetimini yapabilirsiniz. tooset hello örnek uygulama benzetimli toouse verileri, şu adımları izleyin:

1. Açık hello `config.h` hello dosyasında `app` klasör.

2. Aşağıdaki kod hello bulun ve hello değerinden değiştirmek `false` çok`true`:

   ```c
   define SIMULATED_DATA true
   ```
   ![Merhaba örnek uygulama benzetimli toouse verileri yapılandırma](media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

3. Merhaba dosyayla Kaydet `Control-s`.

### <a name="deploy-hello-sample-application-toofeather-m0-wifi"></a>Merhaba örnek uygulama tooFeather M0 WiFi dağıtma

1. Hello Arduino IDE, tıklatın **aracı** > **bağlantı noktası**ve yumuşatma M0 WiFi hello seri bağlantı noktası'ı tıklatın.

2. Tıklatın **taslak** > **karşıya** toobuild ve hello örnek uygulama tooFeather M0 WiFi dağıtın.

### <a name="enter-your-credentials"></a>Kimlik bilgilerinizi girin

Merhaba karşıya yükleme başarıyla tamamlandıktan sonra bu adımları tooenter kimlik bilgilerinizi izleyin:

1. Hello Arduino IDE, tıklatın **Araçları** > **seri İzleyici**.

2. Hello sağ alt köşesinde hello seri İzleyicisi penceresinde, seçin **hiçbir satır bitiş** hello soldaki hello aşağı açılan listesinde.
3. Seçin **115200 baud** hello sağ hello aşağı açılan listesinde.
4. Merhaba giriş kutusuna hello üstünde kullanıcısıysanız bilgisinden hello girin ve tıklatın tooprovide sorulan **Gönder**:

   * Wi-Fi SSID
   * Wi-Fi parola
   * Cihaz bağlantı dizesi

> [!Note]
> Merhaba kimlik bilgileri hello yumuşatma M0 WiFi EEPROM depolanır. Merhaba yumuşatma M0 WiFi Panosu hello Sıfırla düğmesini tıklatın, Merhaba örnek uygulaması tooerase hello bilgi isteyip istemediğinizi sorar. Girin `Y` tooerase hello bilgi. Tooprovide hello bilgi ikinci kez sorulur.

### <a name="verify-that-hello-sample-application-is-running-successfully"></a>Merhaba örnek uygulaması başarılı bir şekilde çalıştığını doğrulayın

Görürseniz hello seri İzleyicisi penceresinde hello şu çıktıları ve LED yumuşatma M0 WiFi Merhaba örnek uygulaması üzerinde yanıp sönen hello başarıyla çalıştırma:

![Arduino IDE içinde son çıktı](media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a>Sonraki adımlar

Başarıyla tooyour IOT hub'ı yumuşatma M0 WiFi bağlı ve yakalanan hello algılayıcı verileri tooyour IOT hub'ı gönderilir. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

