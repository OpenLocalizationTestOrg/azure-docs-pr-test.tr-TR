---
title: "Benzetimli cihaz & Azure IOT ağ geçidi - Ders 2: Get Araçlar (Ubuntu) | Microsoft Docs"
description: "Merhaba araçları ve hello yazılım Ubuntu çalıştıran ana bilgisayarınıza yüklemek, IOT hub'ı oluşturun ve hello IOT hub'da Cihazınızı kaydedin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IOT geliştirme, IOT yazılım IOT bulut hizmeti, şeyler yazılım, azure CLI, Internet üzerinde ubuntu Git'i yükleyin, çalışma gulp, düğüm js ubuntu yükleyin"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cf673154-ce67-4ed7-a9f7-2440301c6270
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 38c4d5d9cceec47758f0641cc26b631a7b19d37e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a>Merhaba Araçları (Ubuntu 16.04) alın
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

- Nasıl tooinstall Git ve Node.js.
  - Git bir açık kaynak dağıtılmış sürüm denetim sistemidir. Merhaba örnek bir uygulama bu ders için Git üzerinde depolanır.
  - Node.js, JavaScript çalışma zamanı zengin paket ekosistemi ile olur.
- Nasıl toouse NPM tooinstall Node.js geliştirme araçları.
  - Merhaba gerekli en düşük sürümü Node.js 4.5 LTS ' dir.
  - NPM hello paket Node.js yöneticilerinden biridir.
- Nasıl tooinstall Visual Studio Code.
  - Visual Studio platformlar arası, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisini kodudur. Hata ayıklama, katıştırılmış Git denetimi, sözdizimi vurgulama, akıllı kod tamamlama, parçacıkları ve kod da yeniden düzenleme için harika desteğe sahiptir.
- Nasıl tooinstall hello Azure CLI
  - Hello Azure CLI, Azure için birden çok platformlu bir komut satırı deneyimi sağlar. Doğrudan bir komut satırı tooprovision çalışma ve kaynaklarını yönetme.
- Nasıl toouse hello Azure CLI toocreate IOT hub'ı.

## <a name="what-you-need"></a>Ne gerekiyor

- Bir Internet bağlantısı toodownload araçları ve yazılım hello.
- Ubuntu 16.04 veya sonraki sürümünü çalıştıran bir bilgisayar.

## <a name="install-git-and-nodejs"></a>Git ve Node.js yükleyin

tooinstall Git ve Node.js, şu adımları izleyin:

1. Tuşuna `Ctrl + Alt + T` tooopen bir terminal.
2. Merhaba aşağıdaki komutları çalıştırın:

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a>Node.js geliştirme araçlarını yükleme

Kullandığınız [gulp.js](http://gulpjs.com/) tooautomate dağıtım ve komut dosyası yürütme.

tooinstall gulp, komut hello terminalde aşağıdaki hello çalıştırın:

```bash
sudo npm install -g gulp
```

Merhaba yükleme sorunlarıyla karşılaşırsanız, hello bkz [sorun giderme kılavuzu](iot-hub-gateway-kit-c-sim-troubleshooting.md) çözümleri toocommon sorunları.

> [!Note]
> Düğüm, NPM ve Gulp Node.js içinde geliştirilen gerekli toorun Otomasyon betikleri vardır.

## <a name="install-hello-azure-cli"></a>Hello Azure CLI yükleme

tooinstall hello Azure CLI, şu adımları izleyin:

1. Komutları hello terminalde aşağıdaki hello çalıştırın:

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   Merhaba yükleme 5 dakika sürebilir.

2. Merhaba aşağıdaki komutu çalıştırarak Hello yüklemeyi doğrulayın:

   ```bash
   az iot -h
   ```
Merhaba yükleme başarılı olup olmadığını hello aşağıdaki çıktı görmeniz gerekir.
![Azure CLI yükleme doğrulayın](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)

### <a name="install-visual-studio-code"></a>Visual Studio Kodu'nu yükle

Visual Studio Code daha sonra hello öğretici tooedit yapılandırma dosyalarını kullanın.

[Karşıdan](https://code.visualstudio.com/docs/setup/linux) ve Visual Studio Code yükleyin.

## <a name="summary"></a>Özet

Tüm gerekli hello araçları ve yazılım ana bilgisayara yüklediniz. Sonraki görev toouse hello Azure CLI toocreate IOT hub'ı ve IOT hub'ınıza Cihazınızı kaydedin.

## <a name="next-steps"></a>Sonraki adımlar
[IoT hub'ı oluşturma ve cihazınızı kaydetme](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
