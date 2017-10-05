---
title: "SensorTag cihaz & Azure IOT ağ geçidi - Ders 2: Get Araçlar (macOS) | Microsoft Docs"
description: "Mac bilgisayarda araçlarını yükleme, IOT hub'ı oluşturun ve IOT hub'ı Cihazınızı kaydedin."
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
ms.openlocfilehash: 07bc5f2cf6542273c334371b77520c674c5d2f00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos"></a>(MacOS) araçları edinin
> [!div class="op_single_selector"]
> * [Windows 7 veya üzeri](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Ne yapacağını

- Git, Node.js, Gulp, Python yükleyin.
- Azure komut satırı arabirimi (Azure CLI) yükleyin. 

Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz

Bu alıştırmanın ilerisinde şunları öğreneceksiniz:

- Yükleme [Git](https://git-scm.com/) ve [Node.js](https://nodejs.org/en/).
  - Git bir açık kaynak dağıtılmış sürüm denetim sistemidir. Örnek bir uygulama bu ders için Git üzerinde depolanır.
  - Node.js, JavaScript çalışma zamanı zengin paket ekosistemi ile olur.
- Nasıl kullanılacağını [NPM](https://www.npmjs.com/) Node.js geliştirme araçlarını yüklemek için.
  - Node.js, gerekli en düşük sürüm 4.5 LTS ' dir.
  - NPM Node.js paket yöneticilerinden biridir.
- Visual Studio Code yükleme.
  - Visual Studio platformlar arası, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisini kodudur. Hata ayıklama, katıştırılmış Git denetimi, sözdizimi vurgulama, akıllı kod tamamlama, parçacıkları ve kod da yeniden düzenleme için harika desteğe sahiptir.
- Python yükleme.
  - Python yaygın olarak kullanılan üst düzey, genel amaçlı, yorumlanan ve dinamik programlama dilidir.
- Azure CLI yükleme.
  - Azure CLI, Azure için birden çok platformlu bir komut satırı deneyimi sağlar. Doğrudan komut satırından sağlamak için çalışır ve kaynaklarını yönetme.
- IOT hub'ı oluşturmak için Azure CLI kullanma

## <a name="what-you-need"></a>Ne gerekiyor

- Araçlar ve yazılım indirmesi için Internet bağlantısı.
- OS X Yosemite (10.10) veya sonraki sürümü çalıştıran bir Mac bilgisayar.

## <a name="install-git-and-nodejs"></a>Git ve Node.js yükleyin

Git ve Node.js yüklemek için aşağıdaki adımları izleyerek Homebrew paket yönetimi yardımcı programı'nı kullanın:

1. [Karşıdan](http://brew.sh/) ve Homebrew yükleyin. Homebrew zaten yüklediyseniz, 2. adıma geçin.
   1. Tuşuna `Cmd + Space` ve girin `Terminal` bir Terminali açın.
   2. Şu komutu çalıştırın:

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. Git ve Node.js aşağıdaki komutu çalıştırarak yükleyin:

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a>Node.js geliştirme araçlarını yükleme

Kullandığınız [gulp.js](http://gulpjs.com/) dağıtım ve betiklerinin yürütülmesi otomatik hale getirmek için.

Gulp yüklemek için terminal aşağıdaki komutu çalıştırın:

```bash
npm install -g gulp
```

Yükleme sorunlarıyla karşılaşırsanız, bkz: [sorun giderme kılavuzu](iot-hub-gateway-kit-c-troubleshooting.md) yaygın sorunların çözümleri için.

> [!Note]
> Düğüm, NPM ve Gulp Node.js içinde geliştirilen Otomasyon betikleri çalıştırmak için gereklidir.

## <a name="install-python"></a>Python yüklemek

Mac OS X ile Python 2.7 gelse Homebrew aracılığıyla Python yüklemenizi öneririz. Bkz: [Python Mac OS X yükleme](http://docs.python-guide.org/en/latest/starting/install/osx/).

Python ve PIP aşağıdaki komutu çalıştırarak yükleyin:

```bash
brew install python
```

## <a name="install-the-azure-cli"></a>Azure CLI'yı yükleme

Azure CLI yüklemek için aşağıdaki adımları izleyin:

1. Terminale aşağıdaki komutları çalıştırın:
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   Yükleme 5 dakika sürebilir.

2. Aşağıdaki komutu çalıştırarak yüklemeyi doğrulayın:
   ```bash
   az iot -h
   ```
   Yükleme başarılı olursa aşağıdaki çıktı görmeniz gerekir.

   ![Azure CLI yükleme doğrulayın](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a>Visual Studio Kodu'nu yükle

Visual Studio Code öğreticide daha sonra yapılandırma dosyalarını düzenlemek için kullanın.

[Karşıdan](https://code.visualstudio.com/docs/setup/osx) ve Visual Studio Code yükleyin.

## <a name="summary"></a>Özet

Mac bilgisayarda tüm gerekli araçlar ve yazılımı yüklediğiniz. Sonraki göreviniz IOT hub'ı oluşturun ve IOT hub'ınıza Cihazınızı kaydetmek için Azure CLI kullanmaktır.

## <a name="next-steps"></a>Sonraki adımlar
[IOT hub'ı oluşturma ve cihaz kaydetme](iot-hub-gateway-kit-c-lesson2-register-device.md)
