---
title: "aaaESP8266 toocloud - bağlanmak yumuşatma HUZZAH ESP8266 tooAzure IOT hub'ı | Microsoft Docs"
description: "Bilgi nasıl toosetup ve onun için Adafruit yumuşatma HUZZAH ESP8266 tooAzure IOT hub'ı Bu öğreticide toosend veri toohello Azure bulut platformu bağlanın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: c505aacf-89a8-40ed-a853-493b75bec524
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: xshi
ms.openlocfilehash: 44fd47232488948d21c7aa71bdd865397e41e63e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-tooazure-iot-hub-in-hello-cloud"></a>Adafruit yumuşatma HUZZAH ESP8266 tooAzure IOT Hub'hello bulutta Bağlan

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![DHT22, yumuşatma HUZZAH ESP8266 ve IOT hub'ı arasında bir bağlantı](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a>Neler


Oluşturduğunuz Adafruit yumuşatma HUZZAH ESP8266 tooan IOT hub bağlayın. Daha sonra örnek bir uygulama DHT22 algılayıcı sıcaklık ve nem ESP8266 toocollect hello verileri çalıştırın. Son olarak, hello algılayıcı verileri tooyour IOT hub'ı gönderin.

> [!NOTE]
> Diğer ESP8266 panoları kullanıyorsanız, bu adımları tooconnect hala izleyebilirsiniz, tooyour IOT hub'ı. Kullanmakta olduğunuz hello ESP8266 Panosu bağlı olarak, tooreconfigure hello gerekebilecek `LED_PIN`. AI Thinker gelen ESP8266 kullanıyorsanız, örneğin, ondan değişebilir `0` çok`2`. Bir pakete henüz yok mu? Hello alma [Azure Web sitesi](http://azure.com/iotstarterkits).




## <a name="what-you-learn"></a>Öğrenecekleriniz

* Nasıl toocreate IOT hub'ı ve yumuşatma HUZZAH ESP8266 için bir cihaz kaydetme
* Nasıl tooconnect yumuşatma HUZZAH ESP8266 hello algılayıcı ve bilgisayarınız
* Nasıl yumuşatma HUZZAH ESP8266 üzerinde bir örnek uygulamayı çalıştırarak toocollect algılayıcı verileri
* Nasıl toosend hello algılayıcı verileri tooyour IOT hub'ı

## <a name="what-you-need"></a>Ne gerekiyor

![Merhaba öğretici için gerekli bölümleri](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete bu işlemi yumuşatma HUZZAH ESP8266 Starter Seti'nden bölümleri aşağıdaki hello gerekir:

* Merhaba yumuşatma HUZZAH ESP8266 Panosu
* Mikro USB tooType bir USB kablosu

Ayrıca geliştirme ortamınız için öğeleri izleyen hello gerekir:

* Etkin bir Azure aboneliği. Bir Azure hesabınız yoksa [ücretsiz Azure deneme hesabı oluşturma](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.
* Mac veya Windows veya Ubuntu çalıştıran bir bilgisayar.
* Kablosuz ağ yumuşatma HUZZAH ESP8266 tooconnect için.
* Internet bağlantısı toodownload hello yapılandırma aracı.
* [Arduino IDE](https://www.arduino.cc/en/main/software) sürüm 1.6.8 veya sonraki bir sürümü. Önceki sürümlerde hello AzureIoT kitaplığı ile çalışmaz.

Algılayıcı olmayan olasılığına hello aşağıdaki öğeler isteğe bağlıdır. Benzetimli algılayıcı verilerini kullanmanın hello seçeneğiniz de vardır.

* Adafruit DHT22 sıcaklık ve nem algılayıcısı
* Bir breadboard
* M/M anahtar kabloları


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-hello-sensor-and-your-computer"></a>Merhaba algılayıcı ve bilgisayarınızla yumuşatma HUZZAH ESP8266 Bağlan
Bu bölümde, hello algılayıcılar tooyour Panosu bağlayın. Ardından aygıt tooyour bilgisayarınızdaki başka kullanmak için takın.
### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-huzzah-esp8266"></a>Bir DHT22 sıcaklık ve nem algılayıcı tooFeather HUZZAH ESP8266 Bağlan

Merhaba breadboard ve anahtar kablolarını toomake hello bağlantısı aşağıdaki şekilde kullanın. Algılayıcı yoksa, benzetimli algılayıcı verilerini yerine kullandığından bu bölümü atlayabilirsiniz.

![Bağlantı Başvurusu](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


Algılayıcı PIN'ler için kablolama aşağıdaki hello kullan:


| Başlangıç (algılayıcı)           | Bitiş (kartı)           | Kablo rengi   |
| -----------------------  | ---------------------- | ------------: |
| VDD (PIN 31F)            | 3v (PIN 58H)           | Kırmızı kablosu     |
| Veri (PIN 32F)           | GPIO'yu 2 (PIN 46A)       | Mavi kablosu    |
| GND (PIN 34F)            | GND (PIN 56I)          | Siyah kablosu   |

Daha fazla bilgi için bkz: [Adafruit DHT22 algılayıcı Kurulum](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) ve [Adafruit yumuşatma HUZZAH Esp8266 no'lu](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).



Şimdi yumuşatma Huzzah ESP8266 ile çalışma algılayıcı bağlı olması gerekir.

![Yumuşatma Huzzah ile DHT22 Bağlan](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-tooyour-computer"></a>Yumuşatma HUZZAH ESP8266 tooyour bilgisayara bağlanma

Sonraki gösterildiği gibi hello mikro USB tooType bir USB kablosu tooconnect yumuşatma HUZZAH ESP8266 tooyour bilgisayar kullanın.

![Yumuşatma Huzzah tooyour bilgisayara bağlanma](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a>Seri bağlantı noktası izinleri (yalnızca Ubuntu) ekleyin


Ubuntu kullanırsanız, hello izinleri toooperate hello USB bağlantı noktası, yumuşatma HUZZAH ESP8266 üzerinde olduğundan emin olun. tooadd seri bağlantı noktası izinleri, aşağıdaki adımları uygulayın:


1. Bir terminal komutları aşağıdaki hello çalıştırın:

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   Çıktı aşağıdaki hello birini alın:

   * crw-rw---1 kök uucp xxxxxxxx
   * crw-rw---1 kök araması xxxxxxxx

   Merhaba çıktısında dikkat `uucp` veya `dialout` hello Grup sahibi hello USB bağlantı noktasına adıdır.

1. Merhaba kullanıcı toohello grubu hello aşağıdaki komutu çalıştırarak ekleyin:

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   `<group-owner-name>`elde ettiğiniz hello Grup sahibi hello önceki adımda adıdır. `<username>`Ubuntu kullanıcı adınızdır.

1. Ubuntu dışında oturum açın ve yeniden hello değişiklik tooappear için oturum açın.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>Algılayıcı verilerini toplamak ve tooyour IOT hub'ı gönderin

Bu bölümde, dağıtın ve yumuşatma HUZZAH ESP8266 üzerinde bir örnek uygulamayı çalıştırın. Merhaba örnek uygulaması hello LED yumuşatma HUZZAH ESP8266 üzerinde yanıp ve hello sıcaklık gönderir ve nem veri hello DHT22 algılayıcı tooyour IOT hub'ı toplanır.

### <a name="get-hello-sample-application-from-github"></a>Merhaba örnek uygulaması Github'dan alma

Merhaba örnek uygulaması, GitHub üzerinde barındırılır. Merhaba örnek uygulaması github'dan içeren hello örnek depoyu kopyalayın. tooclone hello örnek deposu, şu adımları izleyin:

1. Bir komut istemi veya terminal penceresi açın.
1. Depolanan hello örnek uygulama toobe istediğiniz tooa klasörüne gidin.
1. Merhaba aşağıdaki komutu çalıştırın:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

Merhaba paket yumuşatma HUZZAH ESP8266 hello Arduino IDE yükleyin:

1. Merhaba örnek uygulaması depolandığı hello klasörünü açın.
1. Merhaba Arduino IDE hello uygulama klasöründe Hello app.ino dosyasını açın.

   ![Merhaba örnek uygulaması Arduino IDE içinde açın](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. Hello Arduino IDE, tıklatın **dosya** > **Tercihler**.
1. Merhaba, **Tercihler** iletişim kutusunda, hello simgesi sonraki toohello tıklayın **ek panoları yöneticisi URL'leri** kutusunu.
1. URL aşağıdaki hello Hello açılır pencerede girin ve ardından **Tamam**.

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Arduino IDE içinde tooa paket URL'sini noktası](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. Merhaba, **tercih** iletişim kutusu, tıklatın **Tamam**.
1. Tıklatın **Araçları** > **Panosu** > **panoları Yöneticisi**ve esp8266 için arama yapın.

   Panoları Yöneticisi ESP8266 2.2.0 veya sonraki bir sürümü ile yüklü olduğunu gösterir.

   ![Merhaba esp8266 paketinin yüklü olduğu](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. Tıklatın **Araçları** > **Panosu** > **Adafruit HUZZAH ESP8266**.

### <a name="install-necessary-libraries"></a>Gerekli kitaplıkları yükleme

1. Hello Arduino IDE, tıklatın **taslak** > **dahil Kitaplığı** > **yönetmek kitaplıkları**.
1. Kitaplık adları tek tek aşağıdaki hello arayın. Bulduğunuz her kitaplığını tıklatın **yükleme**.
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a>Gerçek DHT22 algılayıcı yok mu?

Gerçek DHT22 algılayıcı olmayan olasılığına Merhaba örnek uygulaması sıcaklık ve nem veri benzetimini yapabilirsiniz. tooset hello örnek uygulama benzetimli toouse verileri, şu adımları izleyin:

1. Açık hello `config.h` hello dosyasında `app` klasör.
1. Aşağıdaki kod hello bulun ve hello değerinden değiştirmek `false` çok`true`:
   ```c
   define SIMULATED_DATA true
   ```
   ![Merhaba örnek uygulama benzetimli toouse verileri yapılandırma](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. Merhaba dosyayla Kaydet `Control-s`.

### <a name="deploy-hello-sample-application-toofeather-huzzah-esp8266"></a>Merhaba örnek uygulama tooFeather HUZZAH ESP8266 dağıtma

1. Hello Arduino IDE, tıklatın **aracı** > **bağlantı noktası**, yumuşatma HUZZAH ESP8266 hello seri bağlantı noktası'a tıklayın.
1. Tıklatın **taslak** > **karşıya** toobuild ve hello örnek uygulama tooFeather HUZZAH ESP8266 dağıtın.

### <a name="enter-your-credentials"></a>Kimlik bilgilerinizi girin

Merhaba karşıya yükleme başarıyla tamamlandıktan sonra bu adımları tooenter kimlik bilgilerinizi izleyin:

1. Hello Arduino IDE, tıklatın **Araçları** > **seri İzleyici**.
1. Merhaba seri İzleyicisi penceresinde hello iki açılan listeleri hello sağ alt köşedeki dikkat edin.
1. Seçin **hiçbir satır bitiş** hello sol aşağı açılan listesi.
1. Seçin **115200 baud** hello sağda açılan listesi.
1. Merhaba seri İzleyicisi penceresinde Hello üstünde bulunan hello giriş tooprovide sorulursa bilgisinden hello kutusuna ve ardından **Gönder**.
   * Wi-Fi SSID
   * Wi-Fi parola
   * Cihaz bağlantı dizesi

> [!Note]
> Merhaba kimlik bilgileri hello yumuşatma HUZZAH ESP8266 EEPROM depolanır. Merhaba yumuşatma HUZZAH ESP8266 Panosu hello Sıfırla düğmesini tıklatın, Merhaba örnek uygulaması tooerase hello bilgi isteyip istemediğinizi sorar. Girin `Y` toohave hello bilgileri silinir. Tooprovide hello bilgi ikinci kez istenir.

### <a name="verify-hello-sample-application-is-running-successfully"></a>Merhaba örnek uygulaması başarılı bir şekilde çalıştığını doğrulayın

Görürseniz hello seri İzleyicisi penceresinde hello şu çıktıları ve LED yumuşatma HUZZAH ESP8266, Merhaba örnek uygulaması üzerinde yanıp sönen hello başarılı bir şekilde çalışıyor.

![Arduino IDE içinde son çıktı](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a>Sonraki adımlar

Başarıyla bir yumuşatma HUZZAH ESP8266 tooyour IOT hub'ı bağlı ve yakalanan hello algılayıcı verileri tooyour IOT hub gönderilen. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

