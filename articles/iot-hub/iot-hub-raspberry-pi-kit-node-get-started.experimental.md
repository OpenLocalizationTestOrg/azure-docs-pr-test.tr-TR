---
title: "Buluta (Node.js) - Azure IOT Hub'ına bağlanmak Raspberry Pi'yi Böğürtlenli Pi | Microsoft Docs"
description: "Azure bulut veri göndermek Raspberry Pi'yi için Azure IOT Hub ile Raspberry Pi'yi bağlayın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure IOT Böğürtlenli PI Böğürtlenli PI IOT hub, bulut için Böğürtlenli pi gönderme, verileri buluta Böğürtlenli pi"
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
ms.openlocfilehash: 956ed5ab0ed38ddebd978b35eb54bc96567f0d57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-nodejs"></a>Azure IOT Hub (Node.js) Böğürtlenli Pi Bağlan

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

Bu öğreticide, Raspbian çalıştıran Raspberry Pi'yi ile çalışmanın temelleri öğrenerek başlayın. Daha sonra sorunsuzca aygıtlarınızı buluta kullanarak bağlanmasına nasıl öğrenin [Azure IOT Hub](iot-hub-what-is-iot-hub.md). Windows 10 IOT Core örnekleri için Git [Windows Geliştirme Merkezi](http://www.windowsondevices.com/).

Bir pakete henüz yok mu? Deneyin [Raspberry Pi 3 öykünücü](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/). Veya yeni bir paket satın [burada](https://azure.microsoft.com/develop/iot/starter-kits).

## <a name="what-you-do"></a>Neler

* Böğürtlenli PI kurulumu.
* IOT hub'ı oluşturun.
* Bir cihaz IOT hub'ınıza Pi için kaydetme.
* Pi algılayıcı verilerini IOT hub'ınıza gönderilecek örnek bir uygulamayı çalıştırın.

Raspberry Pi'yi, oluşturduğunuz bir IOT hub'ına bağlanın. Pi BME280 algılayıcı sıcaklık ve nem verileri toplamak için bir örnek uygulamayı çalıştırın. ardından. Son olarak, IOT hub'ınıza algılayıcı verileri gönderin.

## <a name="what-you-learn"></a>Öğrenecekleriniz

* Azure IOT hub oluşturma ve yeni cihaz bağlantı dizenizi elde etme.
* Pi BME280 algılayıcı ile bağlanma.
* Pi üzerinde bir örnek uygulamayı çalıştırarak algılayıcı verilerini toplamak nasıl.
* IOT hub'ınıza algılayıcı verileri göndermek nasıl.

## <a name="what-you-need"></a>Ne gerekiyor

![Ne gerekiyor](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* Raspberry Pi 2 veya Raspberry Pi 3 Panosu.
* Etkin bir Azure aboneliği. Bir Azure hesabınız yoksa [ücretsiz Azure deneme hesabı oluşturma](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.
* Bir izleyici, bir USB klavye ve fare Pi bağlanan.
* Mac veya Windows veya Linux çalıştıran bir bilgisayar.
* Bir Internet bağlantısı.
* 16 GB veya üzeri microSD kartı.
* İşletim sistemi görüntüsü microSD kartı üzerine yazmak için bir USB SD bağdaştırıcı veya microSD kartı.
* 5-volt 2 amp güç 6 kaplama alanı mikro USB kablosu ile sağlayın.

Aşağıdaki öğeler isteğe bağlıdır:

* Bir birleştirilmiş Adafruit BME280 sıcaklık, baskısı ve nem algılayıcı.
* Bir breadboard.
* 6 F/M anahtar kablolarını.
* Yayılmış 10 mm LED.

  > [!NOTE] 
  Kod örneği desteği algılayıcı verilerini benzetimli çünkü bu öğeler isteğe bağlıdır.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a>Böğürtlenli PI Kurulumu

### <a name="install-the-raspbian-operating-system-for-pi"></a>Pi için Raspbian işletim sistemini yükleme

MicroSD kartı Raspbian görüntünün yüklenmesi için hazırlayın.

1. Raspbian indirin.
   1. [Piksel ile Raspbian Jessie karşıdan](https://www.raspberrypi.org/downloads/raspbian/) (.zip dosyası).
   1. Raspbian görüntünün bilgisayarınızdaki bir klasöre ayıklayın.
1. Raspbian microSD kartı yükleyin.
   1. [Etcher SD kart yazıcı yardımcı programı yükleyip](https://etcher.io/).
   1. Etcher çalıştırın ve 1. adımda ayıkladığınız Raspbian görüntüyü seçin.
   1. MicroSD kartı sürücü seçin. Etcher zaten doğru sürücü seçmiş olabilirsiniz olduğunu unutmayın.
   1. Raspbian microSD kartı yüklemek için Flash'ı tıklatın.
   1. Yükleme tamamlandığında microSD kartı bilgisayarınızdan kaldırın. Etcher otomatik olarak çıkarır veya tamamlanmasından sonra microSD kartı çıkarır çünkü microSD kartı doğrudan kaldırmak güvenlidir.
   1. MicroSD kartı Pi yerleştirin.

### <a name="enable-ssh-and-i2c"></a>SSH ve I2C etkinleştir

1. Monitör, klavye ve fare pi bağlanmak, Pi başlatın ve ardından içinde Raspbian kullanarak oturum `pi` kullanıcı adı ve `raspberry` ve parola olarak.
1. Böğürtlenli simgesine tıklayın > **Tercihler** > **Raspberry Pi yapılandırma**.

   ![Raspbian Tercihler menüsü](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. Üzerinde **arabirimleri** sekmesinde, ayarlamak **I2C** ve **SSH** için **etkinleştirmek**ve ardından **Tamam**. Fiziksel algılayıcılar varsa ve benzetimli algılayıcı verilerini kullanmak istediğiniz yok, bu adım isteğe bağlıdır.

   ![I2C ve Böğürtlenli Pi üzerinde SSH etkinleştir](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
SSH ve I2C etkinleştirmek için daha fazla başvuru belgeleri bulabilirsiniz [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) ve [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).

### <a name="connect-the-sensor-to-pi"></a>Pi algılayıcı Bağlan

Bir LED ve bir BME280 Pi şu şekilde bağlanmak için breadboard ve anahtar kablolarını kullanır. Algılayıcı yoksa bu bölümü atlayabilirsiniz.

![Raspberry Pi'yi ve algılayıcı bağlantısı](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

BME280 algılayıcı sıcaklık ve nem verileri toplayabilir. Ve cihaz ve bulut arasındaki iletişimi ise LED blink. 

Algılayıcı PIN'ler için aşağıdaki kablolama kullanın:

| Başlangıç (algılayıcı & LED)     | Bitiş (kartı)            | Kablo rengi   |
| -----------------------  | ---------------------- | ------------: |
| VDD (PIN 5G)             | 3, 3v PWR (PIN 1)       | Beyaz kablosu   |
| GND (PIN 7G)             | GND (PIN 6)            | Kahverengi kablosu   |
| SCK (PIN 8G)             | I2C1 SDA (PIN 3)       | Turuncu kablosu  |
| SDI (PIN 10G)            | I2C1 SCL (PIN 5)       | Kırmızı kablosu     |
| LED VDD (PIN 18F)        | GPIO'yu 24 (PIN 18)       | Beyaz kablosu   |
| LED GND (PIN 17F)        | GND (PIN 20)           | Siyah kablosu   |

Görüntülemek için tıklatın [Raspberry Pi 2 ve 3 PIN eşlemeleri](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) daha sonra başvurmak üzere.

Raspberry Pi'yi BME280 başarıyla bağlandıktan sonra görüntü gibi olmalıdır.

![Bağlı Pi ve BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a>Pi ağa bağlanın

Pi üzerinde mikro USB kablosu ve güç kaynağı kullanarak açın. Pi kablolu ağa bağlanın veya izleyin için Ethernet kablosu kullanın [Raspberry Pi Foundation yönergeleri](https://www.raspberrypi.org/learning/software-guide/wifi/) Pi kablosuz ağınıza bağlanmak için. Not yapmanıza gerek, Pi ağa başarıyla bağlandı sonra [IP adresi, pi'nin](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).

![Kablolu ağa bağlı](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> Pi bilgisayarınızın aynı ağa bağlı olduğundan emin olun. Örneğin, pi kablolu bir ağa bağlıyken, bilgisayarınızın kablosuz bir ağa bağlıysa, IP adresi devdisco çıkışı göremeyebilirsiniz.

## <a name="run-a-sample-application-on-pi"></a>Pi üzerinde bir örnek uygulamayı çalıştırın

### <a name="clone-sample-application-and-install-the-prerequisite-packages"></a>Örnek uygulama kopyalamak ve önkoşul yükleyin

1. Raspberry Pi'yi bağlanmak için ana bilgisayarınız aşağıdaki SSH istemcilerden birini kullanın.
    - [PuTTY](http://www.putty.org/) Windows için. SSH bağlanmak için Pi IP adresi gerekir.
    - Ubuntu veya macOS üzerindeki yerleşik SSH istemcisi. Çalıştırma `ssh pi@<ip address of pi>` Pi SSH aracılığıyla bağlanmak için.

   > [!NOTE] 
   Varsayılan kullanıcı adı `pi` , ve parola `raspberry`.

1. Node.js ve NPM, Pi yükleyin.
   
   Önce aşağıdaki komutu kullanarak, Node.js sürümünü kontrol etmeniz gerekir. 
   
   ```bash
   node -v
   ```

   Sürüm 4.x düşük olduğu veya, Pi üzerinde hiçbir Node.js yüklemek veya Node.js güncelleştirmek için aşağıdaki komutu çalıştırın.

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. Örnek uygulama, aşağıdaki komutu çalıştırarak kopyalama:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. Tüm paketler aşağıdaki komutu tarafından yükleyin. Azure IOT cihaz SDK'sı, BME280 algılayıcı kitaplığı ve geriye Pi kitaplığı içerir.

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   Bu yükleme işlemini denpening ağ bağlantınızdaki tamamlanması birkaç dakika sürebilir.

### <a name="configure-the-sample-application"></a>Örnek uygulamayı yapılandırma

1. Yapılandırma dosyası, aşağıdaki komutları çalıştırarak açın:

   ```bash
   nano config.json
   ```

   ![Yapılandırma dosyası](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   İki öğe bu dosyada configurate olabilir. İlk sağlayıcıdır `interval`, bulut göndermek iki ileti arasındaki zaman aralığını tanımlar. İkincisi `simulatedData`, benzetimli algılayıcı verilerini veya kullanıp kullanmayacağınızı için bir Boolean değeri değil.

   Varsa, **algılayıcı yok**ayarlayın `simulatedData` değeri `true` oluşturma ve sanal algılayıcı verilerini kullanma örnek uygulamayı yapmak için.

1. Kaydedip çıkmak denetimi O tuşlarına basarak > Enter > Denetim X.

### <a name="run-the-sample-application"></a>Örnek uygulamayı çalıştırın

1. Aşağıdaki komutu çalıştırarak örnek uygulamayı çalıştırın:

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   Kopyalama cihaz bağlantı dizesi tek tırnak yapıştırma emin olun.


Algılayıcı verilerini ve IOT hub'ına gönderilen iletileri gösterir aşağıdaki çıktı görmeniz gerekir.

![Çıktı - Raspberry Pi'yi IOT hub'ına gönderilen algılayıcı verileri](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a>Sonraki adımlar

Algılayıcı verilerini toplamak ve IOT hub'ınıza göndermek için örnek bir uygulamayı çalıştırdıktan.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]