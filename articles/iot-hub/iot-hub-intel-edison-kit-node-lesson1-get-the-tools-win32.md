---
title: "Azure IOT - Ders 1 Intel Edison'u (düğüm) bağlanma: alma araçlarını (Windows) | Microsoft Docs"
description: "İndirin ve Windows 7 ve sonraki sürümleri gerekli araçları ve Edison'u için ilk örnek uygulama için yazılım yüklemek."
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
ms.openlocfilehash: 35b7ae24f8616848eaa6affccb96630603b823b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-or-later"></a>(Windows 7 veya üzeri) araçları edinin
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
  * Node.js en düşük sürüm gereksinimini 4.5 LTS ' dir.
  * [NPM](https://www.npmjs.com) Node.js paket yöneticilerinden biridir.

## <a name="what-you-need"></a>Ne gerekiyor

Bu işlemi tamamlamak için gerekir:

* Geliştirme araçları ve yazılım indirmesi için Internet bağlantısı.
* Windows çalıştıran bir bilgisayar.

## <a name="install-git-and-nodejs"></a>Git ve Node.js yükleyin

İndirmek ve Git ve Windows için Node.js LTS yüklemek için aşağıdaki bağlantıları tıklatın.

* [Windows için Git Al](https://git-scm.com/download/win/)
* [Windows için node.js LTS Al](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a>Ek Node.js geliştirme araçlarını yükleme

Kullanım [gulp.js](http://gulpjs.com) Edison'u için örnek uygulama dağıtımını otomatik hale getirmek için.

Bir komut istemini yönetici olarak başlatın. Yükleme `gulp` aşağıdaki komutu çalıştırarak:

```cmd
npm install -g gulp
```

Node.js ve bu ek Node.js geliştirme araçları bilgisayarınızda yüklerken sorunlarla karşılaşırsanız bkz [sorun giderme kılavuzu] [ troubleshooting] yaygın sorunların çözümleri için.

## <a name="install-visual-studio-code"></a>Visual Studio Kodu'nu yükle

[Karşıdan](https://code.visualstudio.com/docs/setup/windows) ve Visual Studio Code yükleyin. Visual Studio Code, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisidir. Örnek kod düzenlemek için öğreticide daha sonra bu Düzenleyicisi'ni kullanın.

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
