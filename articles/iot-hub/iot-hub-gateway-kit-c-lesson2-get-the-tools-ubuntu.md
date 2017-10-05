---
title: "SensorTag cihaz & Azure IOT ağ geçidi - Ders 2: Get Araçlar (Ubuntu) | Microsoft Docs"
description: "Araçlar ve yazılım Ubuntu çalıştıran ana bilgisayarınıza yüklemek, IOT hub'ı oluşturun ve IOT hub'ı Cihazınızı kaydedin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IOT geliştirme, IOT yazılım IOT bulut hizmeti, şeyler yazılım, azure CLI, Internet üzerinde ubuntu Git'i yükleyin, çalışma gulp, düğüm js ubuntu yükleyin"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0bac1412-385b-4255-a33f-9d44c35feb3e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 234b60e1f8eaff52ce07f54d4d12de2421cc1a52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a>Araçları edinme (Ubuntu 16.04)
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

- Git ve Node.js nasıl yüklenir.
  - Git bir açık kaynak dağıtılmış sürüm denetim sistemidir. Örnek bir uygulama bu ders için Git üzerinde depolanır.
  - Node.js, JavaScript çalışma zamanı zengin paket ekosistemi ile olur.
- NPM Node.js Geliştirme Araçları'nı yüklemek için nasıl kullanılacağını.
  - Node.js, gerekli en düşük sürüm 4.5 LTS ' dir.
  - NPM Node.js paket yöneticilerinden biridir.
- Visual Studio Code yükleme.
  - Visual Studio platformlar arası, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisini kodudur. Hata ayıklama, katıştırılmış Git denetimi, sözdizimi vurgulama, akıllı kod tamamlama, parçacıkları ve kod da yeniden düzenleme için harika desteğe sahiptir.
- Azure CLI yükleme
  - Azure CLI, Azure için birden çok platformlu bir komut satırı deneyimi sağlar. Doğrudan komut satırından sağlamak için çalışır ve kaynaklarını yönetme.
- IOT hub'ı oluşturmak için Azure CLI kullanma

## <a name="what-you-need"></a>Ne gerekiyor

- Araçlar ve yazılım indirmesi için Internet bağlantısı.
- Ubuntu 16.04 veya sonraki sürümünü çalıştıran bir bilgisayar.

## <a name="install-git-and-nodejs"></a>Git ve Node.js yükleyin

Git ve Node.js yüklemek için aşağıdaki adımları izleyin:

1. Tuşuna `Ctrl + Alt + T` bir Terminali açın.
2. Aşağıdaki komutları çalıştırın:

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a>Node.js geliştirme araçlarını yükleme

Kullandığınız [gulp.js](http://gulpjs.com/) dağıtım ve betiklerinin yürütülmesi otomatik hale getirmek için.

Gulp yüklemek için terminal aşağıdaki komutu çalıştırın:

```bash
sudo npm install -g gulp
```

Yükleme sorunlarıyla karşılaşırsanız, bkz: [sorun giderme kılavuzu](iot-hub-gateway-kit-c-troubleshooting.md) yaygın sorunların çözümleri için.

> [!Note]
> Düğüm, NPM ve Gulp Node.js içinde geliştirilen Otomasyon betikleri çalıştırmak için gereklidir.

## <a name="install-the-azure-cli"></a>Azure CLI'yı yükleme

Azure CLI yüklemek için aşağıdaki adımları izleyin:

1. Terminale aşağıdaki komutları çalıştırın:

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   Yükleme 5 dakika sürebilir.

2. Aşağıdaki komutu çalıştırarak yüklemeyi doğrulayın:

   ```bash
   az iot -h
   ```
Yükleme başarılı olursa aşağıdaki çıktı görmeniz gerekir.
![Azure CLI yükleme doğrulayın](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)

### <a name="install-visual-studio-code"></a>Visual Studio Kodu'nu yükle

Visual Studio Code öğreticide daha sonra yapılandırma dosyalarını düzenlemek için kullanın.

[Karşıdan](https://code.visualstudio.com/docs/setup/linux) ve Visual Studio Code yükleyin.

## <a name="summary"></a>Özet

Tüm gerekli araçlar ve yazılım ana bilgisayara yüklediniz. Sonraki göreviniz IOT hub'ı oluşturun ve IOT hub'ınıza Cihazınızı kaydetmek için Azure CLI kullanmaktır.

## <a name="next-steps"></a>Sonraki adımlar
[IoT hub'ı oluşturma ve cihazınızı kaydetme](iot-hub-gateway-kit-c-lesson2-register-device.md)
