---
title: "aaaESP8266 toocloud - Sparkfun ESP8266 şey geliştirme bağlanmak tooAzure IOT hub'ı | Microsoft Docs"
description: "Bilgi nasıl toosetup ve onun için Sparkfun ESP8266 şey geliştirme tooAzure IOT hub'ı Bu öğreticide toosend veri toohello Azure bulut platformu bağlanın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 587fe292-9602-45b4-95ee-f39bba10e716
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 19b249df23b6df516634853521c6d532f51014da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-tooazure-iot-hub-in-hello-cloud"></a>Sparkfun ESP8266 şey geliştirme tooAzure IOT Hub'hello bulutta Bağlan

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![DHT22, şey geliştirme ve IOT hub'ı arasında bir bağlantı](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a>Ne yapacağını

Oluşturacağınız Sparkfun ESP8266 şey geliştirme tooan IOT hub bağlayın. Daha sonra örnek bir uygulama üzerinde ESP8266 toocollect sıcaklık ve nem veri DHT22 algılayıcının çalıştırın. Son olarak, hello algılayıcı verileri tooyour IOT hub'ı gönderin.

> [!NOTE]
> Diğer ESP8266 panoları kullanıyorsanız, bu adımları tooconnect hala izleyebilirsiniz, tooyour IOT hub'ı. Kullanmakta olduğunuz hello ESP8266 Panosu bağlı olarak, tooreconfigure hello gerekebilir `LED_PIN`. AI Thinker gelen ESP8266 kullanıyorsanız, örneğin, ondan değişebilir `0` çok`2`. Bir pakete henüz yok mu?: tıklatın [burada](http://azure.com/iotstarterkits)

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz

* Nasıl toocreate IOT hub'ı ve şey istisnası için bir cihaz kaydetme
* Nasıl tooconnect şey geliştirme hello algılayıcı ve bilgisayarınızı.
* Nasıl şey istisnası üzerinde bir örnek uygulamayı çalıştırarak toocollect algılayıcı verileri
* Nasıl toosend algılayıcı verileri tooyour IOT hub'ı hello.

## <a name="what-you-will-need"></a>İhtiyacınız olacak

![Merhaba öğretici için gerekli bölümleri](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete bu işlemi şey geliştirme Starter Seti'nden bölümleri aşağıdaki hello gerekir:

* Merhaba Sparkfun ESP8266 şey geliştirme Panosu.
* Mikro USB tooType bir USB kablosu.

Ayrıca, geliştirme ortamınız için hello aşağıdaki gerekir:

* Etkin bir Azure aboneliği. Bir Azure hesabınız yoksa [ücretsiz Azure deneme hesabı oluşturma](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.
* Mac veya Windows veya Ubuntu çalıştıran bir bilgisayar.
* Kablosuz ağ Sparkfun ESP8266 şey geliştirme tooconnect için.
* Internet bağlantısı toodownload hello yapılandırma aracı.
* [Arduino IDE](https://www.arduino.cc/en/main/software) sürüm 1.6.8 (veya daha yeni), önceki sürümlerinde hello AzureIoT kitaplığı ile çalışmaz.

Algılayıcı olmayan olasılığına hello aşağıdaki öğeler isteğe bağlıdır. Benzetimli algılayıcı verilerini kullanmanın hello seçeneğiniz de vardır.

* Bir Adafruit DHT22 sıcaklık ve nem algılayıcı.
* Bir breadboard.
* M/M anahtar kablolarını.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-hello-sensor-and-your-computer"></a>Merhaba algılayıcı ve bilgisayarınızla ESP8266 şey geliştirme Bağlan

### <a name="connect-a-dht22-temperature-and-humidity-sensor-tooesp8266-thing-dev"></a>DHT22 sıcaklık ve nem algılayıcı bağlanmak tooESP8266 şey geliştirme

Merhaba breadboard ve anahtar kablolarını toomake hello bağlantısı aşağıdaki şekilde kullanın. Algılayıcı yoksa, benzetimli algılayıcı verilerini yerine kullandığından bu bölümü atlayabilirsiniz.

![Bağlantı Başvurusu](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

Kablolama aşağıdaki hello algılayıcı PIN'ler için kullanırız:

| Başlangıç (algılayıcı)           | Bitiş (kartı)           | Kablo rengi   |
| -----------------------  | ---------------------- | ------------: |
| VDD (PIN 27F)            | 3v (PIN 8A)           | Kırmızı kablosu     |
| Veri (PIN 28F)           | GPIO'yu 2 (PIN 9A)       | Beyaz kablosu    |
| GND (PIN 30F)            | GND (PIN 7J)          | Siyah kablosu   |


- Daha fazla bilgi için bkz: [DHT22 algılayıcı Kurulum](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) ve [Sparkfun ESP8266 şey geliştirme belirtimi](https://www.sparkfun.com/products/13711)

Şimdi, Sparkfun ESP8266 şey geliştirme ile çalışma algılayıcı bağlı olması gerekir.

![dht22 ESP8266 şey geliştirme ile bağlanma](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-tooyour-computer"></a>Sparkfun ESP8266 şey geliştirme tooyour bilgisayara bağlanma

Merhaba mikro USB tooType bir USB kablosu tooconnect Sparkfun ESP8266 şey geliştirme tooyour bilgisayar aşağıdaki şekilde kullanın.

![yumuşatma huzzah tooyour bilgisayara bağlanma](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a>Seri bağlantı noktası izinleri – yalnızca Ubuntu ekleyin

Ubuntu kullanıyorsanız, normal bir kullanıcı hello izinleri toooperate hello USB bağlantı noktası, Sparkfun ESP8266 şey istisnası üzerinde sahip olduğundan emin olun tooadd seri bağlantı noktası izinleri normal bir kullanıcı için aşağıdaki adımları uygulayın:

1. Bir terminal komutları aşağıdaki hello çalıştırın:

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   Çıktı aşağıdaki hello birini alın:

   * crw-rw---1 kök uucp xxxxxxxx
   * crw-rw---1 kök araması xxxxxxxx

   Merhaba çıktısında fark `uucp` veya `dialout` diğer bir deyişle hello Grup sahibi adını hello USB bağlantı noktası.

1. Merhaba kullanıcı toohello grubu hello aşağıdaki komutu çalıştırarak ekleyin:

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   `<group-owner-name>`elde ettiğiniz hello Grup sahibi hello önceki adımda adıdır. `<username>`Ubuntu kullanıcı adınızdır.

1. Ubuntu ve yeniden oturum içinde hello tootake değişikliğin için.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>Algılayıcı verilerini toplamak ve tooyour IOT hub'ı gönderin

Bu bölümde, dağıtma ve Sparkfun ESP8266 şey istisnası üzerinde örnek uygulamayı çalıştırma Merhaba örnek uygulaması hello LED Sparkfun ESP8266 şey geliştirme üzerinde yanıp ve hello sıcaklık gönderir ve nem veri hello DHT22 algılayıcı tooyour IOT hub'ı toplanır.

### <a name="get-hello-sample-application-from-github"></a>Merhaba örnek uygulaması Github'dan alma

Merhaba örnek uygulaması, GitHub üzerinde barındırılır. Merhaba örnek uygulaması github'dan içeren hello örnek depoyu kopyalayın. tooclone hello örnek deposu, şu adımları izleyin:

1. Bir komut istemi veya terminal penceresi açın.
1. Depolanan hello örnek uygulama toobe istediğiniz tooa klasörüne gidin.
1. Merhaba aşağıdaki komutu çalıştırın:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

Sparkfun ESP8266 şey geliştirme Arduino IDE'de Hello paketi yükle:

1. Merhaba örnek uygulaması depolandığı hello klasörünü açın.
1. Merhaba uygulama klasöründe Arduino IDE Hello app.ino dosyasını açın.

   ![Merhaba örnek uygulaması arduino IDE içinde açın](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. Hello Arduino IDE, tıklatın **dosya** > **Tercihler**.
1. Merhaba, **Tercihler** iletişim kutusunda, hello simgesi sonraki toohello tıklayın **ek panoları yöneticisi URL'leri** metin kutusu.
1. URL aşağıdaki hello Hello açılır pencerede girin ve ardından **Tamam**.

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![arduino IDE içinde tooa paket URL'sini noktası](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. Merhaba, **tercih** iletişim kutusu, tıklatın **Tamam**.
1. Tıklatın **Araçları** > **Panosu** > **panoları Yöneticisi**ve esp8266 için arama yapın.
   ESP8266 2.2.0 veya sonraki bir sürümüyle yüklenmesi gerekir.

   ![Merhaba esp8266 paketinin yüklü olduğu](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. Tıklatın **Araçları** > **Panosu** > **Sparkfun ESP8266 şey geliştirme**.

### <a name="install-necessary-libraries"></a>Gerekli kitaplıkları yükleme

1. Hello Arduino IDE, tıklatın **taslak** > **dahil Kitaplığı** > **yönetmek kitaplıkları**.
1. Kitaplık adları tek tek aşağıdaki hello arayın. Her bulduğunuz hello kitaplığının tıklatın **yükleme**.
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a>Gerçek DHT22 algılayıcı yok mu?

Gerçek DHT22 algılayıcı olmayan olasılığına Merhaba örnek uygulaması sıcaklık ve nem veri benzetimini yapabilirsiniz. tooenable hello örnek uygulama benzetimli toouse verileri, şu adımları izleyin:

1. Açık hello `config.h` hello dosyasında `app` klasör.
1. Aşağıdaki kod hello bulun ve hello değerinden değiştirmek `false` çok`true`:
   ```c
   define SIMULATED_DATA true
   ```
   ![Merhaba örnek uygulama benzetimli toouse verileri yapılandırma](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. İle Kaydet `Control-s`.

### <a name="deploy-hello-sample-application-toosparkfun-esp8266-thing-dev"></a>Merhaba örnek uygulama tooSparkfun ESP8266 şey geliştirme dağıtma

1. Hello Arduino IDE, tıklatın **aracı** > **bağlantı noktası**ve Sparkfun ESP8266 şey istisnası hello seri bağlantı noktası'ı tıklatın
1. Tıklatın **taslak** > **karşıya** toobuild ve hello örnek uygulama tooSparkfun ESP8266 şey istisnası dağıtma

> [!Note]
> MacOS kullanıyorsanız büyük olasılıkla karşıya yükleme sırasında iletileri aşağıdaki hello görebilir. `warning: espcomm_sync failed`,`error: espcomm_open failed`. Lütfen ternimal penceresini açın ve bu sorun Eylemler toosolve son.
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a>Kimlik bilgilerinizi girin

Merhaba karşıya yükleme başarıyla tamamlandıktan sonra kimlik bilgilerinizi hello adımları tooenter izleyin:

1. Hello Arduino IDE, tıklatın **Araçları** > **seri İzleyici**.
1. Merhaba seri İzleyicisi penceresinde hello sağ alt köşesindeki hello iki açılan listelerde dikkat edin.
1. Seçin **hiçbir satır bitiş** hello sol aşağı açılan listesi.
1. Seçin **115200 baud** hello sağda açılan listesi.
1. Merhaba seri İzleyicisi penceresinde Hello üstünde bulunan hello giriş tooprovide sorulursa bilgisinden hello kutusuna ve ardından **Gönder**.
   * Wi-Fi SSID
   * Wi-Fi parola
   * Cihaz bağlantı dizesi

> [!Note]
> Merhaba kimlik bilgileri hello EEPROM Sparkfun ESP8266 şey istisnası depolanır Merhaba Sparkfun ESP8266 şey geliştirme Panosu hello Sıfırla düğmesini tıklatın, Merhaba örnek uygulaması tooerase hello bilgi isteyip istemediğinizi sorar. Girin `Y` toohave hello bilgi silinmesi ve yeniden tooprovide hello bilgi istendi.

### <a name="verify-hello-sample-application-is-running-successfully"></a>Merhaba örnek uygulaması başarılı bir şekilde çalıştığını doğrulayın

Görürseniz hello seri İzleyicisi penceresinde hello şu çıktıları ve LED Sparkfun ESP8266 şey geliştirme, Merhaba örnek uygulaması üzerinde yanıp sönen hello başarılı bir şekilde çalışıyor.

![arduino IDE içinde son çıktı](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a>Sonraki adımlar

Başarıyla bir Sparkfun ESP8266 şey geliştirme tooyour IOT hub'ı bağlı ve yakalanan hello algılayıcı verileri tooyour IOT hub'ı gönderilir. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
