---
title: "SensorTag cihaz & Azure IOT ağ geçidi - Ders 2: Get Araçlar (macOS) | Microsoft Docs"
description: "Araçlar Mac bilgisayarınıza yüklemek, IOT hub'ı oluşturun ve hello IOT hub'da Cihazınızı kaydedin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IOT geliştirme, IOT yazılım, IOT bulut hizmeti, Internet şeyler yazılım, azure CLI yükleme python mac, mac, çalıştırmak, yükleme düğümü js mac gulp Git'i yükleyin"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 94e538ef-9857-4023-9c3c-e92a0be7c395
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 44bce452690e18e6c803df564fdafcdda7f41c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos"></a>Merhaba Araçları (MacOS) alın
> [!div class="op_single_selector"]
> * [Windows 7 veya üzeri](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Ne yapacağını

- Git, Node.js, Gulp, Python yükleyin.
- Hello Azure komut satırı arabirimi (Azure CLI) yükleyin. 

Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).

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
- OS X Yosemite (10.10) veya sonraki sürümü çalıştıran bir Mac bilgisayar.

## <a name="install-git-and-nodejs"></a>Git ve Node.js yükleyin

tooinstall Git ve Node.js, aşağıdaki adımları izleyerek hello Homebrew paket yönetimi yardımcı programı kullanın:

1. [Karşıdan](http://brew.sh/) ve Homebrew yükleyin. Homebrew zaten yüklediyseniz, toostep 2 gidin.
   1. Tuşuna `Cmd + Space` ve girin `Terminal` tooopen bir terminal.
   2. Merhaba aşağıdaki komutu çalıştırın:

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. Git ve Node.js hello aşağıdaki komutu çalıştırarak yükleyin:

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a>Node.js geliştirme araçlarını yükleme

Kullandığınız [gulp.js](http://gulpjs.com/) tooautomate dağıtım ve komut dosyası yürütme.

tooinstall gulp, komut hello terminalde aşağıdaki hello çalıştırın:

```bash
npm install -g gulp
```

Merhaba yükleme sorunlarıyla karşılaşırsanız, hello bkz [sorun giderme kılavuzu](iot-hub-gateway-kit-c-troubleshooting.md) çözümleri toocommon sorunları.

> [!Note]
> Düğüm, NPM ve Gulp Node.js içinde geliştirilen gerekli toorun Otomasyon betikleri vardır.

## <a name="install-python"></a>Python yüklemek

Mac OS X ile Python 2.7 gelse Homebrew aracılığıyla Python yüklemenizi öneririz. Bkz: [Python Mac OS X yükleme](http://docs.python-guide.org/en/latest/starting/install/osx/).

Python ve PIP hello aşağıdaki komutu çalıştırarak yükleyin:

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a>Hello Azure CLI yükleme

tooinstall hello Azure CLI, şu adımları izleyin:

1. Komutları hello terminalde aşağıdaki hello çalıştırın:
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   Merhaba yükleme 5 dakika sürebilir.

2. Merhaba aşağıdaki komutu çalıştırarak Hello yüklemeyi doğrulayın:
   ```bash
   az iot -h
   ```
   Merhaba yükleme başarılı olup olmadığını hello aşağıdaki çıktı görmeniz gerekir.

   ![Azure CLI yükleme doğrulayın](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a>Visual Studio Kodu'nu yükle

Visual Studio Code daha sonra hello öğretici tooedit yapılandırma dosyalarını kullanın.

[Karşıdan](https://code.visualstudio.com/docs/setup/osx) ve Visual Studio Code yükleyin.

## <a name="summary"></a>Özet

Mac bilgisayarda tüm gerekli hello araçları ve yazılımı yüklediğiniz. Sonraki görev toouse hello Azure CLI toocreate IOT hub'ı ve IOT hub'ınıza Cihazınızı kaydedin.

## <a name="next-steps"></a>Sonraki adımlar
[IOT hub'ı oluşturma ve cihaz kaydetme](iot-hub-gateway-kit-c-lesson2-register-device.md)
