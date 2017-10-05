---
title: "Azure IOT - Ders 1 Raspberry Pi'yi (düğüm) bağlanma: Get Araçlar (macOS) | Microsoft Docs"
description: "Karşıdan yükle ve gerekli araçları ve pi ilk örnek uygulama için yazılım üzerinde macOS yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IOT geliştirme IOT yazılım, Internet şeyler yazılımların python mac yükleyin, mac Git'i yükleyin, çalışma gulp, düğüm js mac yükleyin"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 2ea6d211-c0e8-4ade-ac69-d1c2261d78c4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 6c2338baa8e88bab4c4be64568220f53178943cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a>Araçları edinme (macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 veya üzeri](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Ne yapacağını
Geliştirme araçları ve ilk uygulama Raspberry Pi 3 için yazılımı yükleyin. Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

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
Kullanım [gulp.js](http://gulpjs.com) Pi örnek uygulamaya dağıtımını otomatik hale getirmek için. Kullanım [aygıt bulma CLI](https://github.com/Azure/device-discovery-cli) IOT aygıtlarınızla ilgili ağ bilgileri alınamadı.

Yükleme `gulp` ve `device-discovery-cli` terminale aşağıdaki komutu çalıştırarak:

```bash
npm install -g device-discovery-cli gulp
```

Node.js ve bu ek geliştirme araçları üzerinde macOS yüklerken sorunlarla karşılaşırsanız bkz [sorun giderme kılavuzu](iot-hub-raspberry-pi-kit-node-troubleshooting.md) yaygın sorunların çözümleri için.

## <a name="install-visual-studio-code"></a>Visual Studio Kodu'nu yükle
[Karşıdan](https://code.visualstudio.com/docs/setup/osx) ve Visual Studio Code yükleyin. Visual Studio Code, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisidir. Örnek kod düzenlemek için öğreticide daha sonra bu Düzenleyicisi'ni kullanın.

## <a name="summary"></a>Özet
İlk örnek uygulama için yazılım ve gerekli geliştirme araçları yüklediniz. Sonraki oluşturmak, dağıtmak ve örnek uygulama Pi üzerinde çalıştırmak için bir görevdir.

## <a name="next-steps"></a>Sonraki adımlar
[Blink örnek uygulama oluşturun ve dağıtın](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

