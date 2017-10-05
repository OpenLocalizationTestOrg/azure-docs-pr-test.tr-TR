---
title: "Azure IOT - Ders 1 Böğürtlenli Pi (C) bağlanın: uygulama dağıtma | Microsoft Docs"
description: "Örnek C uygulama github'dan kopyalayın ve bu uygulamayı Raspberry Pi 3 panonuzu dağıtmak için gulp. Bu örnek uygulama panosuna her iki saniye bağlı ışığı yanıp."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Böğürtlenli pi öncülük blink, blink neden Böğürtlenli pi ile"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f601d1e1-2bc3-4cc5-a6b1-0467e5304dcf
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 2ae409c6a39521711777ec329d2507a2801cc985
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a>Blink uygulaması oluşturma ve dağıtma
## <a name="what-you-will-do"></a>Ne yapacağını
Örnek C uygulama github'dan kopyalama ve Raspberry Pi 3 örnek uygulamayı dağıtmak için gulp aracını kullanın. Örnek uygulama panosuna her iki saniye bağlı ışığı yanıp. Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:

* Nasıl kullanılacağını `device-discover-cli` PI hakkında ağ bilgilerini almak için aracı.
* Nasıl dağıtmak ve Pi üzerinde örnek uygulamayı çalıştırın.
* Dağıtma ve hata ayıklama uygulamaları uzaktan Pi üzerinde çalışan.

## <a name="what-you-need"></a>Ne gerekiyor
Aşağıdaki işlemleri başarıyla tamamlandı gerekir:

* [Cihazınızı yapılandırma](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md)
* [Araçları edinin](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

## <a name="obtain-the-ip-address-and-host-name-of-pi"></a>Pi IP adresi ve ana bilgisayar adını alın
Windows veya terminal macOS veya Ubuntu bir komut istemi açın ve aşağıdaki komutu çalıştırın:

```bash
devdisco list --eth
```

Aşağıdakine benzer bir çıktı görmeniz gerekir:

![Aygıt Bulma](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

Not edin `IP address` ve `hostname` pi'nin. Bu bilgiler bu makalenin sonraki bölümlerinde gerekir.

> [!NOTE]
> Pi bilgisayarınızın aynı ağa bağlı olduğundan emin olun. Örneğin, pi kablolu bir ağa bağlıyken, bilgisayarınızın kablosuz bir ağa bağlıysa, IP adresi devdisco çıkışı göremeyebilirsiniz.

## <a name="open-the-sample-application"></a>Örnek uygulamayı Aç
Örnek uygulamayı açmak için şu adımları izleyin:

1. Aşağıdaki komutu çalıştırarak github'dan örnek depoyu kopyalayın:
   
    ```bash
    git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started.git
    ```
2. Örnek uygulama, aşağıdaki komutları çalıştırarak Visual Studio kodda açın:
   
    ```bash
    cd iot-hub-c-raspberrypi-getting-started
    cd Lesson1
    code .
    ```

![Depodaki yapısı](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-c-mac.png)

`main.c` Dosyasını `app` alt denetim LED koda içeren anahtar kaynak dosyası klasörüdür.

### <a name="install-application-dependencies"></a>Uygulama bağımlılıkları yükler
Kitaplıklar ve örnek uygulama için aşağıdaki komutu çalıştırarak gereken diğer modüller yükleyin:

```bash
npm install
```

## <a name="configure-the-device-connection"></a>Aygıt bağlantısını yapılandırın
Aygıt bağlantısını yapılandırmak için aşağıdaki adımları izleyin:

1. Aşağıdaki komutu çalıştırarak aygıt yapılandırma dosyası oluşturun:
   
   ```bash
   gulp init
   ```
   
   Yapılandırma dosyası `config-raspberrypi.json` Pi oturum açmak için kullandığınız kullanıcı kimlik bilgilerini içerir. Kullanıcı kimlik bilgilerini sızıntısını önlemek için yapılandırma dosyası alt klasöründe oluşturulur `.iot-hub-getting-started` bilgisayarınızda giriş klasörünün.

2. Aygıt yapılandırma dosyası, aşağıdaki komutu çalıştırarak Visual Studio kodda açın:
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```

3. Yer tutucu Değiştir `[device hostname or IP address]` IP adresini ya da daha önce alındı ana bilgisayar adına sahip "Pi IP adresi ve ana bilgisayar adını alın."
   
   ![Config.JSON](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> Raspberry Pi'yi bağlanırken, kullanıcı adı ve parola yerine SSH anahtarı kullanabilirsiniz. Bunu kullanarak anahtar oluşturmak için olacaktır yapmak için **ssh-keygen** ve **ssh-kopya-ID pi @\<aygıt adresi\>**.
>
> Bu komutlar Windows üzerinde kullanılabilir olan **Git Bash**.
>
> MacOS üzerinde çalıştırmanız gerekir. **brew yükleme ssh-kopya-ID**.
>
> Başarılı bir şekilde anahtar Raspberry Pi'yi dosyalarını karşıya yükledikten sonra yerine **device_password** ile **device_key_path** özelliğinde **config raspberrypi.json**.
>
> Güncelleştirilmiş satırları aşağıdaki gibi görünmelidir:
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

Tebrikler! Pi ilk örnek uygulama başarıyla oluşturdunuz.

## <a name="deploy-and-run-the-sample-application"></a>Dağıtma ve örnek uygulamayı çalıştırma
### <a name="install-the-azure-iot-hub-sdk-on-pi"></a>Pi üzerinde Azure IOT Hub SDK'sını yükleyin
Azure IOT Hub SDK'sı, aşağıdaki komutu çalıştırarak üzerinde Pi yükleyin:

```bash
gulp install-tools
```

Bu görev, ilk çalıştırdığınızda tamamlanması birkaç dakika sürebilir.

### <a name="deploy-and-run-the-sample-app"></a>Dağıtma ve örnek uygulamayı çalıştırma
Dağıtma ve aşağıdaki komutu çalıştırarak örnek uygulamayı çalıştırın:

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a>Uygulama çalıştığını doğrulama
Örnek uygulama için 20 kez ışığı yanıp sonra otomatik olarak sonlandırır. IŞIĞI yanıp sönen görmüyorsanız bkz [sorun giderme kılavuzu](iot-hub-raspberry-pi-kit-c-troubleshooting.md) yaygın sorunların çözümleri için.
![IŞIĞI yanıp sönen](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)

## <a name="summary"></a>Özet
Pi ile çalışmak için gerekli araçları yüklü ve bir örnek uygulama ile Pi LED blink dağıtılır. Şimdi oluşturmanıza, dağıtmanıza ve Pi ileti gönderme ve alma için Azure IOT hub'a bağlanan başka bir örnek uygulamayı çalıştırın.

## <a name="next-steps"></a>Sonraki adımlar
[Azure Araçları edinin](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)

