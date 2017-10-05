---
title: "Azure IOT - Ders 1 Connect Raspberry pi (C): Get Araçlar (macOS) | Microsoft Docs"
description: "Karşıdan yükle ve gerekli araçları ve pi ilk örnek uygulama için yazılım üzerinde macOS yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IOT geliştirme, IOT yazılım, Internet şeyler yazılımın, Mac, çalıştırmak, yükleme düğümü js mac gulp yükleme git"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fc6bd2c8-a847-4bf5-818f-6f7f9a6835ee
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 64db77040ef3482f213bd622320fdb5df243fa93
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a>Araçları edinme (macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 veya üzeri](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Ne yapacağını
Geliştirme araçları ve ilk uygulama Raspberry Pi 3 için yazılımı yükleyin. Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

> [!NOTE]
> Asıl mantığı programlama dili C olsa da, Node.js araçları dersleri aygıtları bulmak ve yapı ve örnek uygulamaları dağıtmak için kullanılır.

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
Kullanım [gulp.js](http://gulpjs.com) , Pi örnek uygulamaya dağıtımını otomatik hale getirmek için. Kullanım [aygıt bulma CLI](https://github.com/Azure/device-discovery-cli) IOT aygıtlarınızla ilgili ağ bilgileri alınamadı.

Yükleme `gulp` ve `device-discovery-cli` terminale aşağıdaki komutu çalıştırarak:

```bash
sudo npm install -g device-discovery-cli gulp
```

Node.js ve bu ek geliştirme araçları üzerinde macOS yüklerken sorunlarla karşılaşırsanız bkz [sorun giderme kılavuzu](iot-hub-raspberry-pi-kit-c-troubleshooting.md) yaygın sorunların çözümleri için.

## <a name="install-visual-studio-code"></a>Visual Studio Kodu'nu yükle
[Karşıdan](https://code.visualstudio.com/docs/setup/osx) ve Visual Studio Code yükleyin. Visual Studio Code, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisidir. Örnek kod düzenlemek için öğreticide daha sonra bu Düzenleyicisi'ni kullanın.

## <a name="summary"></a>Özet
İlk örnek uygulama için yazılım ve gerekli geliştirme araçları yüklediniz. Sonraki oluşturmak, dağıtmak ve örnek uygulama Pi üzerinde çalıştırmak için bir görevdir.

## <a name="next-steps"></a>Sonraki adımlar
[Blink uygulaması oluşturma ve dağıtma](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

