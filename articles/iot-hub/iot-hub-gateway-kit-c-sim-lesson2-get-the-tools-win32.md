---
title: "Benzetimli cihaz & Azure IOT ağ geçidi - Ders 2: alma araçlarını (Windows) | Microsoft Docs"
description: "Merhaba araçları ve hello yazılım Windows çalıştıran ana bilgisayarınıza yüklemek, IOT hub'ı oluşturun ve hello IOT hub'da Cihazınızı kaydedin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IOT geliştirme, IOT yazılım IOT bulut hizmeti, şeyler yazılım, azure CLI, Internet Windows Git'i yükleyin, çalışma gulp, düğüm js Windows'u yüklemek, Windows npm yükleme, Windows'da python yüklemek"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: c16eee4c-8756-454b-82bf-3eb0dd51aa5f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7ca3c9f11eb232f853fc8fd921b0a49ae37d0184
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-and-later"></a>(Windows 7 ve üzeri) Hello araçları edinin
> [!div class="op_single_selector"]
> * [Windows 7 veya üzeri](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Ne yapacağını

- Git, Node.js, Gulp, Python yükleyin.
- Hello Azure komut satırı arabirimi (Azure CLI) yükleyin. 

Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz

Bu alıştırmanın ilerisinde şunları öğreneceksiniz:

- Nasıl tooinstall [Git](https://git-scm.com/) ve [Node.js](https://nodejs.org/en/).
  - Git bir açık kaynak dağıtılmış sürüm denetim sistemidir. Merhaba örnek bir uygulama bu ders için Git üzerinde depolanır.
  - Node.js, JavaScript çalışma zamanı zengin paket ekosistemi ile olur.
- Nasıl toouse [NPM](https://www.npmjs.com/) tooinstall Node.js geliştirme araçları.
  - Merhaba gerekli en düşük sürümü Node.js 4.5 LTS ' dir.
  - NPM hello paket Node.js yöneticilerinden biridir.
- Nasıl tooinstall Visual Studio Code.
  - Visual Studio platformlar arası, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisini kodudur. Hata ayıklama, katıştırılmış Git denetimi, sözdizimi vurgulama, akıllı kod tamamlama, parçacıkları ve kod da yeniden düzenleme için harika desteğe sahiptir.
- Nasıl tooinstall Python.
  - Python yaygın olarak kullanılan üst düzey, genel amaçlı, yorumlanan ve dinamik programlama dilidir.
- Nasıl tooinstall Azure CLI hello.
  - Hello Azure CLI, Azure için birden çok platformlu bir komut satırı deneyimi sağlar. Doğrudan bir komut satırı tooprovision çalışma ve kaynaklarını yönetme.
- Nasıl toouse hello Azure CLI toocreate IOT hub'ı.

## <a name="what-you-need"></a>Ne gerekiyor

- Bir Internet bağlantısı toodownload araçları ve yazılım hello.
- Bir Windows bilgisayarı.

## <a name="install-git-and-nodejs"></a>Git ve Node.js yükleyin

Bağlantılar toodownload aşağıdaki hello'ı tıklatın ve Git ve Windows için Node.js LTS yükleyin.

- [Windows için Git Al](https://git-scm.com/download/win/)
- [Windows için node.js LTS Al](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a>Node.js geliştirme araçlarını yükleme

Kullandığınız [gulp.js](http://gulpjs.com/) tooautomate dağıtım ve komut dosyası yürütme.

Basın `Windows + R`, türü `cmd` ve basın `Enter` tooopen bir komut istemi penceresi ve sonra çalışma hello aşağıdaki komutu:

```cmd
npm install -g gulp
```

Merhaba yükleme sorunlarıyla karşılaşırsanız, hello bkz [sorun giderme kılavuzu](iot-hub-gateway-kit-c-sim-troubleshooting.md) çözümleri toocommon sorunları.

> [!Note]
> Düğüm, NPM ve Gulp Node.js içinde geliştirilen gerekli toorun Otomasyon betikleri vardır.

## <a name="install-python"></a>Python yüklemek

Python 2.7, 3.4 veya 3.5 seçebilirsiniz. Bu öğreticide, Python 2.7 kullanırız. Python'ı zaten yüklediyseniz, toohello sonraki bölümüne gidin.

[Python için Windows Al](https://www.python.org/downloads/)

Tooadd hello yolu Python.exe'yi ve pip.exe nerede yüklü toohello sistem hello klasörlerinin etmeniz `PATH` ortam değişkeni. Varsayılan olarak, Python.exe'yi yüklü `C:\Python27` ve pip.exe yüklü `C:\Python27\Scripts`.

## <a name="install-hello-azure-cli"></a>Hello Azure CLI yükleme

tooinstall hello Azure CLI, şu adımları izleyin:

1. Yönetici olarak bir komut istemi penceresi açın.

2. Hello Azure CLI hello aşağıdaki komutları çalıştırarak yükleyin:

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   Merhaba yükleme 5 dakika sürebilir.

3. Merhaba aşağıdaki komutu çalıştırarak Hello yüklemeyi doğrulayın:

   ```cmd
   az iot -h
   ```

   Merhaba yükleme başarılı olup olmadığını hello aşağıdaki çıktı görmeniz gerekir.

   ![Azure CLI yükleme doğrulayın](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a>Visual Studio Kodu'nu yükle

Visual Studio Code daha sonra hello öğretici tooedit yapılandırma dosyalarını kullanın.

[Karşıdan](https://code.visualstudio.com/docs/setup/windows) ve Visual Studio Code yükleyin.

## <a name="summary"></a>Özet

Tüm gerekli hello araçları ve yazılım ana bilgisayara yüklediniz. Sonraki görev toouse hello Azure CLI toocreate IOT hub'ı ve IOT hub'ınıza Cihazınızı kaydedin.

## <a name="next-steps"></a>Sonraki adımlar
[IoT hub'ı oluşturma ve cihazınızı kaydetme](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
