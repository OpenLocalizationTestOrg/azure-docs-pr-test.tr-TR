---
title: "Intel Edison'u (düğüm) tooAzure IOT - Ders 1 bağlanın: alma araçlarını (Windows) | Microsoft Docs"
description: "İndirin ve Windows 7 ve sonraki sürümlerde hello gerekli araçları ve hello ilk örnek bir uygulama için Edison'u yazılımı yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino geliştirme araçları, IOT geliştirme, IOT yazılım, Internet şeyler yazılımın, Windows, düğüm js windows yükleme yükleme git"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 4164b5a1-5a42-4d8a-9ff6-441e79fcc936
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 933cc585d1b8b0236d76452f5c449ae9f2f3987b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a>(Windows 7 veya üzeri) Hello araçları edinin
> [!div class="op_single_selector"]
> * [Windows 7 veya üzeri][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>Ne yapacağını
Merhaba geliştirme araçları ve hello ilk örnek bir uygulama için Intel Edison'u hello yazılımını indirin. Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:

* Nasıl tooinstall Git ve Node.js.
  * [Git](https://git-scm.com) bir açık kaynak dağıtılmış sürüm denetim sistemidir. Bu makale için Merhaba örnek uygulaması Git üzerinde depolanır.
  * [Node.js](https://nodejs.org/en/) JavaScript çalışma zamanı zengin paket ekosistemi ile.
* Nasıl toouse NPM tooinstall ek Node.js geliştirme araçları.
  * Node.js Hello en düşük sürüm gereksinimini 4.5 LTS ' dir.
  * [NPM](https://www.npmjs.com) hello Node.js paket yöneticilerinden biridir.

## <a name="what-you-need"></a>Ne gerekiyor

toocomplete bu işlem, gerekir:

* Bir Internet bağlantısı toodownload geliştirme araçları hello ve yazılım hello.
* Windows çalıştıran bir bilgisayar.

## <a name="install-git-and-nodejs"></a>Git ve Node.js yükleyin

Toodownload aşağıda Hello Bağlantılar'ı tıklatın ve Git ve Windows için Node.js LTS yükleyin.

* [Windows için Git Al](https://git-scm.com/download/win/)
* [Windows için node.js LTS Al](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a>Ek Node.js geliştirme araçlarını yükleme

Kullanım [gulp.js](http://gulpjs.com) hello örnek uygulama tooEdison tooautomate hello dağıtımı.

Bir komut istemini yönetici olarak başlatın. Yükleme `gulp` hello aşağıdaki komutu çalıştırarak:

```cmd
npm install -g gulp
```

Node.js ve bu ek Node.js geliştirme araçları bilgisayarınızda yüklerken sorunlarla karşılaşırsanız, hello bkz [sorun giderme kılavuzu] [ troubleshooting] çözümleri toocommon sorunları.

## <a name="install-visual-studio-code"></a>Visual Studio Kodu'nu yükle

[Karşıdan](https://code.visualstudio.com/docs/setup/windows) ve Visual Studio Code yükleyin. Visual Studio Code, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisidir. Daha sonra hello öğretici tooedit hello örnek kodda bu Düzenleyicisi'ni kullanın.

## <a name="summary"></a>Özet

Gerekli hello geliştirme araçları ve hello ilk örnek uygulama için yazılım yüklediniz. Merhaba sonraki toocreate bir görevdir, dağıtmak ve üzerinde Edison'u hello örnek uygulamayı çalıştırın.

## <a name="next-steps"></a>Sonraki adımlar

[Merhaba blink uygulama oluşturun ve dağıtın][create-and-deploy-the-blink-application]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
