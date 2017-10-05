---
title: "Azure IOT - Ders 1 Intel Edison'u (düğüm) bağlanma: Get Araçlar (macOS) | Microsoft Docs"
description: "Karşıdan yükle ve gerekli araçları ve Edison'u için ilk örnek uygulama için yazılım üzerinde macOS yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino geliştirme araçları, IOT geliştirme, IOT yazılım, Internet şeyler yazılımın, mac, yükleme düğümü js mac üzerinde yükleme git"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: fb6742be-2825-4524-89f7-8ccb7e7f1de1
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a5e406f49379e9f2192ee93334ab1dcf9f3e53d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a>Araçları edinme (macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 veya üzeri][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>Ne yapacağını
Geliştirme araçları ve Intel Edison'u için ilk örnek uygulama için yazılım indirin. Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:

* Git ve Node.js nasıl yüklenir.
  * [Git](https://git-scm.com) bir açık kaynak dağıtılmış sürüm denetim sistemidir. Bu makalede örnek uygulama Git üzerinde depolanır.
  * [Node.js](https://nodejs.org/en/) JavaScript çalışma zamanı zengin paket ekosistemi ile.
* NPM ek Node.js Geliştirme Araçları'nı yüklemek için nasıl kullanılacağını.
  * Node.js, gerekli en düşük sürüm 4.5 LTS ' dir.
  * [NPM](https://www.npmjs.com) Node.js paket yöneticilerinden biridir.

## <a name="what-you-need"></a>Ne gerekiyor
Bu işlemi tamamlamak için gerekir:
* Geliştirme araçları ve yazılım indirmesi için Internet bağlantısı.
* MacOS Yosemite (10.10) çalıştıran bir Mac veya sonraki bir sürümü.

## <a name="install-git-and-nodejs"></a>Git ve Node.js yükleyin
Git ve Node.js yüklemek için kullandığınız [Homebrew](http://brew.sh) paket yönetimi yardımcı programı aşağıdaki adımları izleyerek:

1. Homebrew yükleyin. Homebrew zaten yüklediyseniz, 2. adıma geçin.

   1. Tuşuna `Cmd + Space` ve girin `Terminal` bir Terminali açın.
   2. Şu komutu çalıştırın:

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. Git ve Node.js aşağıdaki komutu çalıştırarak yükleyin:

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a>Ek Node.js geliştirme araçlarını yükleme
Kullanım [gulp.js](http://gulpjs.com) , Edison'u örnek uygulamaya dağıtımını otomatik hale getirmek için.

Yükleme `gulp` terminale aşağıdaki komutu çalıştırarak:

```bash
sudo npm install -g gulp
```

Node.js ve bu ek geliştirme araçları üzerinde macOS yüklerken sorunlarla karşılaşırsanız bkz [sorun giderme kılavuzu] [ troubleshooting] yaygın sorunların çözümleri için.

## <a name="install-visual-studio-code"></a>Visual Studio Kodu'nu yükle
[Karşıdan](https://code.visualstudio.com/docs/setup/osx) ve Visual Studio Code yükleyin. Visual Studio Code, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisidir. Örnek kod düzenlemek için öğreticide daha sonra bu Düzenleyicisi'ni kullanın.

## <a name="summary"></a>Özet
İlk örnek uygulama için yazılım ve gerekli geliştirme araçları yüklediniz. Sonraki oluşturmak, dağıtmak ve örnek uygulama Edison'u üzerinde çalıştırmak için bir görevdir.

## <a name="next-steps"></a>Sonraki adımlar
[Blink uygulama oluşturun ve dağıtın][create-and-deploy-the-blink-application]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
