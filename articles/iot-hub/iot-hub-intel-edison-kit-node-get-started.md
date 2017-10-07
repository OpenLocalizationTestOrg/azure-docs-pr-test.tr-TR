---
title: "aaaIntel Edison'u toocloud (Node.js) - bağlanmak Intel Edison'u tooAzure IOT hub'ı | Microsoft Docs"
description: "Bilgi nasıl toosetup ve Intel Edison'u toosend veri toohello Azure bulut platformu için Intel Edison'u tooAzure IOT hub'ı Bu öğreticide bağlanın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure IOT Intel edison'u, Intel edison'u IOT hub, Intel edison'u Gönder veri toocloud, Intel edison'u toocloud"
ms.assetid: a7c9cf2d-c102-41b0-aa45-41285c6877eb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/15/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bfc3387efc532b4b83f0626a9cf61d12c2952af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-intel-edison-tooazure-iot-hub-nodejs"></a>Intel Edison'u tooAzure IOT hub'ı (Node.js) bağlanma

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

Bu öğreticide, Intel Edison'u ile çalışmanın hello temelleri öğrenerek başlayın. Daha sonra nasıl tooseamlessly bağlanacağını aygıtları toohello bulutunuzu kullanarak öğrenin [Azure IOT Hub](iot-hub-what-is-iot-hub.md).

Bir pakete henüz yok mu? Başlat [burada](https://azure.microsoft.com/develop/iot/starter-kits)

## <a name="what-you-do"></a>Neler

* Intel Edison'u Kurulum ve ve Grove modüller.
* IOT hub'ı oluşturun.
* Bir cihaz IOT hub'ınıza Edison'u için kaydetme.
* Örnek bir uygulama Edison'u toosend algılayıcı verileri tooyour IOT hub'ına çalıştırın.

Oluşturduğunuz Intel Edison'u tooan IOT hub bağlayın. Ardından, örnek bir uygulama üzerinde Edison'u toocollect sıcaklık ve nem veri Grove sıcaklık algılayıcısı çalıştırın. Son olarak, hello algılayıcı verileri tooyour IOT hub'ı gönderin.

## <a name="what-you-learn"></a>Öğrenecekleriniz

* Nasıl toocreate Azure IOT hub'ı ve yeni cihaz bağlantı dizenizi alın.
* Nasıl tooconnect Edison'u Grove sıcaklık algılayıcısı ile.
* Nasıl Edison'u üzerinde bir örnek uygulamayı çalıştırarak toocollect algılayıcı verileri.
* Nasıl toosend algılayıcı verileri tooyour IOT hub'ı.

## <a name="what-you-need"></a>Ne gerekiyor

![Ne gerekiyor](media/iot-hub-intel-edison-kit-node-get-started/0_kit.png)

* Merhaba Intel Edison'u Panosu
* Arduino genişletme kartı
* Etkin bir Azure aboneliği. Bir Azure hesabınız yoksa [ücretsiz Azure deneme hesabı oluşturma](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.
* Mac veya Windows veya Linux çalıştıran bir bilgisayar.
* Bir Internet bağlantısı.
* Mikro B tooType bir USB kablosu
* Bir doğrudan geçerli (DC) güç kaynağı. Güç kaynağı gibi derecelendirilmiş:
  - 7 15V DC
  - En az 1500mA
  - Merhaba merkezi/iç PIN hello pozitif kutbu'na hello güç kaynağı, olmalıdır

Aşağıdaki öğelerindeki hello isteğe bağlıdır:

* Grove temel kalkan V2
* Grove - sıcaklık algılayıcısı
* Grove kablosu
* Bir ayırıcı çubukları veya iki Vida toofasten hello modülü toohello genişletme kartı ve vida ve plastik boşluk ekleyiciler dört kümeleri dahil olmak üzere hello paketleme de dahil Vida.

> [!NOTE] 
Merhaba kod örnek desteği algılayıcı verilerini benzetimli çünkü bu öğeler isteğe bağlıdır.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a>Intel Edison'u Kurulumu

### <a name="assemble-your-board"></a>Panonuzu birleştirin

Bu bölümdeki adımları tooattach Intel® Edison'u modülü tooyour genişletme panonuzu içerir.

1. Merhaba Intel® Edison'u modülü hello beyaz anahat içinde hello genişletme panosunda hello Vida ile Merhaba delik hello modül hizalama genişletme panonuzu yerleştirin.

2. Merhaba modül hello sözcükleri hemen altındaki aşağı basın `What will you make?` bir ek düşündüğünüz kadar.

   ![Pano 2 birleştirin](media/iot-hub-intel-edison-kit-node-get-started/1_assemble_board2.jpg)

3. Merhaba iki (Merhaba paketine dahil) onaltılık nasıl toosecure hello modülü toohello genişletme kartı kullanın.

   ![Pano 3 birleştirin](media/iot-hub-intel-edison-kit-node-get-started/2_assemble_board3.jpg)

4. Merhaba dört köşe delik hello genişletme panosunda birinde bir Vidayı ekleyin. Bük ve hello Beyaz Plastik boşluk ekleyiciler hello Vidayı üzerine birini sıkılaştırabilirsiniz.

   ![Pano 4 birleştirin](media/iot-hub-intel-edison-kit-node-get-started/3_assemble_board4.jpg)

5. Diğer üç köşe boşluk ekleyiciler hello için yineleyin.

   ![Pano 5 birleştirin](media/iot-hub-intel-edison-kit-node-get-started/4_assemble_board5.jpg)

Panonuz artık derlenip.

   ![Birleştirilmiş Panosu](media/iot-hub-intel-edison-kit-node-get-started/5_assembled_board.jpg)

### <a name="connect-hello-grove-base-shield-and-hello-temperature-sensor"></a>Merhaba Grove temel kalkan ve hello sıcaklık algılayıcısı

1. Merhaba Grove temel kalkan tooyour panosunda yerleştirin. Tüm PIN'ler panonuzu sıkıca takılı olduğundan emin olun.
   
   ![Grove temel kalkan](media/iot-hub-intel-edison-kit-node-get-started/6_grove_base_sheild.jpg)

2. Kullanım Grove kablo tooconnect Grove sıcaklık algılayıcısı hello Grove temel kalkan üzerine **A0** bağlantı noktası.

   ![Tootemperature algılayıcı Bağlan](media/iot-hub-intel-edison-kit-node-get-started/7_temperature_sensor.jpg)

   ![Edison'u ve algılayıcı bağlantısı](media/iot-hub-intel-edison-kit-node-get-started/16_edion_sensor.png)

Artık, algılayıcı hazırdır.

### <a name="power-up-edison"></a>Güç Edison'u ayarlama

1. Merhaba güç takın.

   ![Güç kaynağı bağlama](media/iot-hub-intel-edison-kit-node-get-started/8_plug_power.jpg)

2. (DS1 hello Arduino * genişletme Panosu üzerinde etiketli) yeşil bir LED açık ve aydınlatılmış olmak gerekir.

3. Başlangıç Panosu toofinish yukarı önyükleme için bir dakika bekleyin.

   > [!NOTE]
   > DC güç kaynağı yoksa, hala bir USB bağlantı noktası üzerinden Güç hello Panosu kullanabilirsiniz. Bkz: `Connect Edison tooyour computer` ayrıntıları bölümü. Özellikle Wi-Fi kullanarak veya yürüten motors zaman Panonuzu bu şekilde destekleyen, karttan beklenmeyen davranışlara neden olabilir.

### <a name="connect-edison-tooyour-computer"></a>Edison'u tooyour bilgisayara bağlanma

1. Böylece Edison'u aygıt modunda hello mikro düğme hello iki mikro USB bağlantı noktası doğru aşağı Değiştir. Cihaz mod ve ana mod arasındaki farklar için lütfen başvuru [burada](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).

   ![Merhaba mikro düğme Değiştir](media/iot-hub-intel-edison-kit-node-get-started/9_toggle_down_microswitch.jpg)

2. Merhaba mikro USB kablosu hello üst mikro USB bağlantı noktasına takın.

   ![Üst mikro USB bağlantı noktası](media/iot-hub-intel-edison-kit-node-get-started/10_top_usbport.jpg)

3. Tak bilgisayarınıza USB kablosu diğer ucundaki hello.

   ![Bilgisayar USB](media/iot-hub-intel-edison-kit-node-get-started/11_computer_usb.jpg)

4. Bilgisayarınızın yeni bir sürücüye (çok SD kart bilgisayarınıza ekleme gibi) bağladığında panonuzu tam olarak başlatılmadan bilirsiniz.

## <a name="download-and-run-hello-configuration-tool"></a>Karşıdan yükle ve hello yapılandırma aracını çalıştırın.
Merhaba en son yapılandırma aracından alma [bu bağlantıyı](https://software.intel.com/en-us/iot/hardware/edison/downloads) hello altında listelenen `Installers` başlığı. Hello aracını Yürüt ve izleyin, ekrandaki yönergeleri, gerektiğinde İleri tıklatıldığında

### <a name="flash-firmware"></a>Bellenim flash
1. Merhaba üzerinde `Set up options` sayfasında, `Flash Firmware`.
2. Merhaba görüntü tooflash panonuzu üzerine hello aşağıdakilerden birini yaparak seçin:
   - toodownload flash panonuzu görüntüsüyle hello en son bellenim Intel'in, kullanılabilir seçip `Download hello latest image version xxxx`.
   - panonuzu, önceden kaydettiğiniz bilgisayarınızdan bir görüntüyle tooflash seçin `Select hello local image`. Tooflash tooyour Panosu tooand select hello görüntü göz atın.
3. Merhaba Kurulum aracı tooflash panonuzu deneyecek. Merhaba tüm yanıp sönen işlem too10 dakika sürebilir.

### <a name="set-password"></a>Parola ayarlama
1. Merhaba üzerinde `Set up options` sayfasında, `Enable Security`.
2. Intel® Edison'u panonuz için bir özel ad ayarlayabilirsiniz. Bu isteğe bağlıdır.
3. Panonuz için bir parola yazın ve ardından `Set password`.
4. Daha sonra kullanılan hello parola işaretleyin.

### <a name="connect-wi-fi"></a>Wi-Fi Bağlan
1. Merhaba üzerinde `Set up options` sayfasında, `Connect Wi-Fi`. Kullanılabilir kablosuz ağlar için bilgisayar taramaları olarak tooone dakika yukarı bekleyin.
2. Merhaba gelen `Detected Networks` aşağı açılan listesinde, ağınızı seçin.
3. Merhaba gelen `Security` aşağı açılan listesinden, select hello ağın güvenlik türü.
4. Oturum açma ve parola bilgilerinizi sağlayın ve ardından `Configure Wi-Fi`.
5. Hello daha sonra kullanılan IP adresi işaretleyin.

> [!NOTE]
> Edison'u bağlı toohello aynı bilgisayarınızda olarak ağ olduğundan emin olun. Bilgisayarınızı tooyour Edison'u hello IP adresini kullanarak bağlanır.

   ![Tootemperature algılayıcı Bağlan](media/iot-hub-intel-edison-kit-node-get-started/12_configuration_tool.png)

Tebrikler! Edison'u başarıyla yapılandırdıktan.

## <a name="run-a-sample-application-on-intel-edison"></a>Intel Edison'u üzerinde bir örnek uygulamayı çalıştırın

### <a name="prepare-hello-azure-iot-device-sdk"></a>Hello Azure IOT cihaz SDK'sı hazırlama

1. SSH istemcilerini, ana bilgisayar tooconnect tooyour Intel Edison'u aşağıdaki hello birini kullanın. Başlangıç IP adresi hello yapılandırma aracından ve hello parola hello biri bu aracında ayarladınız.
    - [PuTTY](http://www.putty.org/) Windows için.
    - Merhaba yerleşik SSH istemcisi Ubuntu veya macOS.

2. Kopya hello örnek istemci uygulaması tooyour aygıt. 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-intel-edison-client-app
   ```

3. Ardından tüm paketler toohello deposu klasör toorun hello komutu tooinstall aşağıdaki gidin, serval dakika toocomplete alabilir.
   
   ```bash
   cd iot-hub-node-intel-edison-client-app
   npm install
   ```


### <a name="configure-and-run-hello-sample-application"></a>Yapılandırma ve hello örnek uygulamayı çalıştırma

1. Merhaba yapılandırma dosyası hello aşağıdaki komutları çalıştırarak açın:

   ```bash
   nano config.json
   ```

   ![Yapılandırma dosyası](media/iot-hub-intel-edison-kit-node-get-started/13_configure_file.png)

   İki makroları vardır bu dosyada configurate olabilir. Merhaba ilk biridir `INTERVAL`, toocloud Gönder iki ileti arasındaki hello zaman aralığını tanımlar. İkinci bir hello `simulatedData`, veya toouse algılayıcı verilerini olup benzetimi için bir Boole değeri değil.

   Varsa, **hello algılayıcı yok**ayarlayın hello `simulatedData` çok değer`true` toomake Merhaba örnek uygulaması oluşturup benzetimli algılayıcı verilerini kullanabilirsiniz.

1. Kaydedip çıkmak denetimi O tuşlarına basarak > Enter > Denetim X.


1. Merhaba aşağıdaki komutu çalıştırarak Hello örnek uygulamayı çalıştırın:

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   Kopyalama hello cihaz bağlantı dizesi hello tek tırnak yapıştırma emin olun.

Gösterir tooyour IOT hub gönderilen algılayıcı verileri ve hello iletileri hello hello aşağıdaki çıktı görmeniz gerekir.

![Çıktı - Intel Edison'u tooyour IOT hub'ından gönderilen algılayıcı verileri](media/iot-hub-intel-edison-kit-node-get-started/15_message_sent.png)

## <a name="next-steps"></a>Sonraki adımlar

Bir örnek uygulama toocollect algılayıcı verilerini çalıştırdıktan ve tooyour IOT hub'ı gönderebilirsiniz.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
