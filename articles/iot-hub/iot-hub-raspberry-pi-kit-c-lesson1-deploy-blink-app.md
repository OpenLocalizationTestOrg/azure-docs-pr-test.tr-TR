---
title: "Connect Raspberry pi (C) tooAzure IOT - Ders 1: uygulama dağıtma | Microsoft Docs"
description: "Merhaba örnek C uygulaması github'dan kopyalayın ve bu uygulama tooyour Raspberry Pi 3 Panosu toodeploy gulp. Bu örnek uygulama hello bağlı LED toohello Panosu her iki saniye yanıp."
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
ms.openlocfilehash: e90c3360c4de1873313db19561c781eb21dbf1d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Merhaba blink uygulama oluşturun ve dağıtın
## <a name="what-you-will-do"></a>Ne yapacağını
Merhaba örnek C uygulaması github'dan kopyalama ve hello gulp aracı toodeploy hello örnek uygulama tooRaspberry Pi 3 kullanın. Merhaba örnek uygulaması, her iki saniye hello bağlı LED toohello Panosu yanıp. Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:

* Nasıl toouse hello `device-discover-cli` aracı tooretrieve PI hakkında bilgi ağ.
* Nasıl toodeploy ve çalışma hello Pi üzerinde örnek uygulama.
* Nasıl uzaktan Pi üzerinde çalışan toodeploy ve hata ayıklama uygulamaları.

## <a name="what-you-need"></a>Ne gerekiyor
Başarıyla işlemleri aşağıdaki hello tamamlamış olmanız gerekir:

* [Cihazınızı yapılandırma](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md)
* [Merhaba araçları edinin](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

## <a name="obtain-hello-ip-address-and-host-name-of-pi"></a>Başlangıç IP adresi ve ana bilgisayar adını Pi alın
Windows veya terminal macOS veya Ubuntu bir komut istemi açın ve ardından hello aşağıdaki komutu çalıştırın:

```bash
devdisco list --eth
```

Toohello aşağıdadır benzer bir çıktı görmeniz gerekir:

![Aygıt Bulma](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

Merhaba not edin `IP address` ve `hostname` pi'nin. Bu bilgiler bu makalenin sonraki bölümlerinde gerekir.

> [!NOTE]
> Pi bağlı toohello aynı bilgisayarınızda olarak ağ olduğundan emin olun. Pi kablolu ağ bağlantılı tooa olsa da, bilgisayarınız bağlı tooa kablosuz ağ ise, örneğin, size hello IP göremeyebilirsiniz hello devdisco çıkış adresi.

## <a name="open-hello-sample-application"></a>Açık Merhaba örnek uygulaması
tooopen hello örnek uygulama, aşağıdaki adımları izleyin:

1. Merhaba örnek depoyu github'dan hello aşağıdaki komutu çalıştırarak kopyalayın:
   
    ```bash
    git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started.git
    ```
2. Merhaba aşağıdaki komutları çalıştırarak örnek uygulama Visual Studio Code açık hello:
   
    ```bash
    cd iot-hub-c-raspberrypi-getting-started
    cd Lesson1
    code .
    ```

![Depodaki yapısı](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-c-mac.png)

Merhaba `main.c` hello dosyasında `app` alt hello kod toocontrol hello LED içeren hello anahtar kaynak dosyası klasörüdür.

### <a name="install-application-dependencies"></a>Uygulama bağımlılıkları yükler
Merhaba kitaplıkları ve hello aşağıdaki komutu çalıştırarak hello örnek bir uygulama için gereken diğer modüller yükleyin:

```bash
npm install
```

## <a name="configure-hello-device-connection"></a>Merhaba aygıt bağlantısını yapılandırın
tooconfigure Merhaba cihaz bağlantısı, şu adımları izleyin:

1. Hello aşağıdaki komutu çalıştırarak Hello aygıt yapılandırma dosyası oluşturun:
   
   ```bash
   gulp init
   ```
   
   Merhaba yapılandırma dosyası `config-raspberrypi.json` içinde tooPi toolog kullanmak hello kullanıcı kimlik bilgilerini içerir. tooavoid hello sızıntısı kullanıcı kimlik bilgilerini, hello yapılandırma dosyası hello alt klasöründe oluşturulur `.iot-hub-getting-started` bilgisayarınızda hello giriş klasörünün.

2. Merhaba aygıt yapılandırma dosyasını Visual Studio kodda hello aşağıdaki komutu çalıştırarak açın:
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```

3. Merhaba yer tutucu Değiştir `[device hostname or IP address]` başlangıç IP adresi ya da daha önce "Elde hello IP adresi ve ana bilgisayar adlarında pi'nin." aldığınız hello ana bilgisayar adına sahip
   
   ![Config.JSON](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> TooRaspberry Pi bağlanırken, kullanıcı adı ve parola yerine SSH anahtarı kullanabilirsiniz. İçinde toodo bu toogenerate hello kullanarak anahtar olacaktır sipariş **ssh-keygen** ve **ssh-kopya-ID pi @\<aygıt adresi\>**.
>
> Bu komutlar Windows üzerinde kullanılabilir olan **Git Bash**.
>
> MacOS üzerinde toorun gereken **brew yükleme ssh-kopya-ID**.
>
> Başarılı bir şekilde hello anahtar toohello Raspberry Pi'yi dosyalarını karşıya yükledikten sonra yerine **device_password** ile **device_key_path** özelliğinde **config raspberrypi.json**.
>
> Güncelleştirilmiş satırları aşağıdaki gibi görünmelidir:
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

Tebrikler! Merhaba ilk örnek uygulaması pi başarıyla oluşturdunuz.

## <a name="deploy-and-run-hello-sample-application"></a>Dağıtma ve hello örnek uygulamayı çalıştırma
### <a name="install-hello-azure-iot-hub-sdk-on-pi"></a>Pi üzerinde Hello Azure IOT Hub SDK'sını yükleyin
Hello Azure IOT Hub SDK'sı üzerinde Pi hello aşağıdaki komutu çalıştırarak yükleyin:

```bash
gulp install-tools
```

Bu görev, birkaç dakika toocomplete hello çalıştırmadan ilk zaman alabilir.

### <a name="deploy-and-run-hello-sample-app"></a>Dağıtma ve hello örnek uygulamayı çalıştırma
Dağıtma ve hello aşağıdaki komutu çalıştırarak hello örnek uygulamayı çalıştırın:

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a>Merhaba uygulama çalıştığını doğrulama
Merhaba örnek uygulama için 20 kez Hello ışığı yanıp sonra otomatik olarak sonlandırır. Merhaba hello ışığı yanıp sönen görmüyorsanız bkz [sorun giderme kılavuzu](iot-hub-raspberry-pi-kit-c-troubleshooting.md) çözümleri toocommon sorunları.
![IŞIĞI yanıp sönen](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)

## <a name="summary"></a>Özet
Pi ile gerekli hello araçları toowork yüklü ve örnek uygulama tooPi tooblink hello LED dağıtılır. Artık oluşturmak, dağıtmak ve Pi tooAzure IOT hub'ı toosend bağlayan başka bir örnek uygulamayı çalıştırın ve iletileri alabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
[Azure Araçları edinin](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)

