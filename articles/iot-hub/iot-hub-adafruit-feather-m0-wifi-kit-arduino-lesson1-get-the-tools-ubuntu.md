---
title: "Azure IOT - Ders 1 Arduino bağlanın: Get Araçlar (Ubuntu) | Microsoft Docs"
description: "Karşıdan yükle ve gerekli araçları ve Adafruit yumuşatma M0 WiFi için ilk örnek uygulama için yazılım üzerinde Ubuntu yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino geliştirme araçları, IOT geliştirme, IOT yazılım, Internet şeyler yazılımın, ubuntu, yükleme düğümü js ubuntu üzerinde yükleme git"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 7572f191-420d-41f0-923b-7ea86c0bfa73
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 90b1c12659c33517142e2048d8f5f629f6d6b4c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a>Araçları edinme (Ubuntu 16.04)

> [!div class="op_single_selector"]
> * [Windows 7 veya üzeri][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>Ne yapacağını

Geliştirme araçları ve ilk uygulama Adafruit yumuşatma M0 WiFi Arduino panonuz için yazılımı yükleyin. 

Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].

> [!NOTE]
> Asıl mantığı programlama dili Arduino olsa da, Node.js araçları dersleri örnek uygulamaları geliştirmek ve dağıtmak için kullanılır.

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:

* Git ve Node.js nasıl yüklenir
  * [Git](https://git-scm.com) bir açık kaynak dağıtılmış sürüm denetim sistemidir. Bu makalede örnek uygulama Git üzerinde depolanır.
  * [Node.js](https://nodejs.org/en/) JavaScript çalışma zamanı zengin paket ekosistemi ile.
* NPM ek Node.js Geliştirme Araçları'nı yüklemek için nasıl kullanılacağını.
  * Node.js, gerekli en düşük sürüm 4.5 LTS ' dir.
  * [NPM](https://www.npmjs.com) Node.js paket yöneticilerinden biridir.

## <a name="what-you-need"></a>Ne gerekiyor
Bu işlemi tamamlamak için gerekir:
* Geliştirme araçları ve yazılım indirmesi için Internet bağlantısı.
* Ubuntu 16.04 veya sonraki sürümünü çalıştıran bir bilgisayar.

## <a name="install-git-nodejs-and-npm"></a>Git, Node.js ve NPM yükleme
Klavye kısayolunu kullanın `Ctrl + Alt + T` bir Terminali açın ve aşağıdaki komutları çalıştırın:

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a>Ek Node.js geliştirme araçlarını yükleme
Kullanım [gulp.js](http://gulpjs.com) Arduino panonuz için örnek uygulama dağıtımını otomatik hale getirmek için.

Yükleme `gulp`, `device-discovery-cli` terminale aşağıdaki komutu çalıştırarak:

```bash
sudo npm install -g gulp device-discovery-cli
```

Node.js ve bu ek geliştirme araçları üzerinde Ubuntu yüklerken sorunlarla karşılaşırsanız bkz [sorun giderme kılavuzu] [ troubleshooting] yaygın sorunların çözümleri için.

## <a name="install-visual-studio-code"></a>Visual Studio Kodu'nu yükle
[Karşıdan](https://code.visualstudio.com/docs/setup/linux) ve Visual Studio Code yükleyin. Visual Studio Code, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisidir. Örnek kod düzenlemek için öğreticide daha sonra bu Düzenleyicisi'ni kullanın.

## <a name="summary"></a>Özet
İlk örnek uygulama için yazılım ve gerekli geliştirme araçları yüklediniz. Sonraki oluşturmak, dağıtmak ve Arduino Panonuzda örnek uygulamayı çalıştırmak için bir görevdir.

## <a name="next-steps"></a>Sonraki adımlar
[Blink örnek uygulama oluşturun ve dağıtın][create-and-deploy-the-blink-sample-application]

<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-sample-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md