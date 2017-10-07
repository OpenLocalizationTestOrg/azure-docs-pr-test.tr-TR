---
title: "Arduino tooAzure IOT - Ders 1 bağlanın: alma araçlarını (Windows) | Microsoft Docs"
description: "İndirin ve Windows 7 ve sonraki sürümlerde hello gerekli araçları ve hello ilk örnek bir uygulama için Adafruit yumuşatma M0 WiFi yazılımı yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino geliştirme araçları, IOT geliştirme, IOT yazılım, Internet şeyler yazılımın, Windows, düğüm js windows yükleme yükleme git"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9cfb8cd2-eafb-4ba2-b23e-d94e114ff3a6
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4dd946da6c84293987e166fd1d17fac117e94e4c
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

Merhaba geliştirme araçları ve hello ilk örnek bir uygulama için Adafruit yumuşatma M0 WiFi Arduino panonuzu hello yazılımını indirin.

Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].

> [!NOTE]
> Programlama dili hello ana mantığı hello Arduino olsa da, Node.js araçları hello dersleri toobuild kullanılır ve örnek uygulamaları dağıtın.

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

Kullanım [gulp.js](http://gulpjs.com) hello örnek uygulama tooyour Arduino Panosu tooautomate hello dağıtımı.

Bir komut istemini yönetici olarak başlatın. Yükleme `gulp`, `device-discovery-cli` komutu hello terminalde aşağıdaki hello çalıştırarak:

```bash
npm install -g gulp device-discovery-cli
```

Node.js ve bu ek Node.js geliştirme araçları bilgisayarınızda yüklerken sorunlarla karşılaşırsanız, hello bkz [sorun giderme kılavuzu] [ troubleshooting] çözümleri toocommon sorunları.

## <a name="install-visual-studio-code"></a>Visual Studio Kodu'nu yükle

[Karşıdan](https://code.visualstudio.com/docs/setup/windows) ve Visual Studio Code yükleyin. Visual Studio Code, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisidir. Daha sonra hello öğretici tooedit hello örnek kodda bu Düzenleyicisi'ni kullanın.

## <a name="summary"></a>Özet

Gerekli hello geliştirme araçları ve hello ilk örnek uygulama için yazılım yüklediniz. Merhaba sonraki toocreate bir görevdir, dağıtmak ve Arduino Panonuzda hello örnek uygulamayı çalıştırın.

## <a name="next-steps"></a>Sonraki adımlar

[Merhaba blink örnek uygulama oluşturun ve dağıtın][create-and-deploy-the-blink-sample-application]
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-sample-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md