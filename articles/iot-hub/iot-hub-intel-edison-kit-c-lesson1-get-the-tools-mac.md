---
title: "Connect Intel Edison (C) tooAzure IOT - Ders 1: Get Araçlar (macOS) | Microsoft Docs"
description: "Karşıdan yükleyip hello gerekli araçları ve yazılım için Edison'u hello ilk örnek uygulaması macOS üzerinde."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino geliştirme araçları, IOT geliştirme, IOT yazılım, Internet şeyler yazılımın, mac, yükleme düğümü js mac üzerinde yükleme git"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 3f764f2e-25fa-4dde-9e8d-d278453fccfd
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4a53331b0dce73c3dd51de91f07df86e28cbb6b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a>Merhaba Araçları (macOS 10.10) alın
> [!div class="op_single_selector"]
> * [Windows 7 veya üzeri][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>Ne yapacağını
Merhaba geliştirme araçları ve hello ilk örnek bir uygulama için Intel Edison'u hello yazılımını indirin. Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].

> [!NOTE]
> Programlama dili hello ana mantığı hello C olsa da, Node.js araçları hello dersleri toobuild kullanılır ve örnek uygulamaları dağıtın.

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:

* Nasıl tooinstall Git ve Node.js.
  * [Git](https://git-scm.com) bir açık kaynak dağıtılmış sürüm denetim sistemidir. Bu makale için Merhaba örnek uygulaması Git üzerinde depolanır.
  * [Node.js](https://nodejs.org/en/) JavaScript çalışma zamanı zengin paket ekosistemi ile.
* Nasıl toouse NPM tooinstall ek Node.js geliştirme araçları.
  * Merhaba gerekli en düşük sürümü Node.js 4.5 LTS ' dir.
  * [NPM](https://www.npmjs.com) hello Node.js paket yöneticilerinden biridir.

## <a name="what-you-need"></a>Ne gerekiyor
toocomplete bu işlem, gerekir:
* Bir Internet bağlantısı toodownload geliştirme araçları hello ve yazılım hello.
* MacOS Yosemite (10.10) çalıştıran bir Mac veya sonraki bir sürümü.

## <a name="install-git-and-nodejs"></a>Git ve Node.js yükleyin
tooinstall Git ve Node.js kullanın hello [Homebrew](http://brew.sh) paket yönetimi yardımcı programı aşağıdaki adımları izleyerek:

1. Homebrew yükleyin. Homebrew zaten yüklediyseniz, toostep 2 gidin.

   1. Tuşuna `Cmd + Space` ve girin `Terminal` tooopen bir terminal.
   2. Merhaba aşağıdaki komutu çalıştırın:

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. Git ve Node.js hello aşağıdaki komutu çalıştırarak yükleyin:

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a>Ek Node.js geliştirme araçlarını yükleme
Kullanım [gulp.js](http://gulpjs.com) hello örnek uygulama tooyour Edison'u tooautomate hello dağıtımı.

Yükleme `gulp` komutu hello terminalde aşağıdaki hello çalıştırarak:

```bash
sudo npm install -g gulp
```

Node.js ve bu ek geliştirme araçları üzerinde macOS yüklerken sorunlarla karşılaşırsanız, hello bkz [sorun giderme kılavuzu] [ troubleshooting] çözümleri toocommon sorunları.

## <a name="install-visual-studio-code"></a>Visual Studio Kodu'nu yükle
[Karşıdan](https://code.visualstudio.com/docs/setup/osx) ve Visual Studio Code yükleyin. Visual Studio Code, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisidir. Daha sonra hello öğretici tooedit hello örnek kodda bu Düzenleyicisi'ni kullanın.

## <a name="summary"></a>Özet
Gerekli hello geliştirme araçları ve hello ilk örnek uygulama için yazılım yüklediniz. Merhaba sonraki toocreate bir görevdir, dağıtmak ve üzerinde Edison'u hello örnek uygulamayı çalıştırın.

## <a name="next-steps"></a>Sonraki adımlar
[Merhaba blink uygulama oluşturun ve dağıtın][create-and-deploy-the-blink-application]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-c-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-mac.md
