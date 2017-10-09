---
title: "Connect Raspberry pi (C) tooAzure IOT - Ders 1: Get Araçlar (Ubuntu) | Microsoft Docs"
description: "İndirin ve Ubuntu üzerinde hello gerekli araçları ve Merhaba ilk örnek uygulaması pi yazılımı yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IOT geliştirme IOT yazılım, şeyler yazılımların internet üzerinde ubuntu Git'i yükleyin, çalışma gulp, düğüm js ubuntu yükleyin"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 32cfea00-c254-4cef-8f6f-bbf807eca6b6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 794928b5da63521cb0a72cb54256f2ad9724ec84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a>Merhaba Araçları (Ubuntu 16.04) alın

> [!div class="op_single_selector"]
> * [Windows 7 veya üzeri](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Ne yapacağını
Merhaba geliştirme araçları ve hello ilk örnek bir uygulama için Raspberry Pi 3 hello yazılımı yükleyin. Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

> [!NOTE]
> Programlama dili hello ana mantığı hello C olsa da, Node.js araçları hello dersleri toodiscover cihazları kullanılır ve yapı ve örnek uygulamaları dağıtın.

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:

* Nasıl tooinstall Git ve Node.js
  * [Git](https://git-scm.com) bir açık kaynak dağıtılmış sürüm denetim sistemidir. Bu makale için Merhaba örnek uygulaması Git üzerinde depolanır.
  * [Node.js](https://nodejs.org/en/) JavaScript çalışma zamanı zengin paket ekosistemi ile.
* Nasıl toouse NPM tooinstall ek Node.js geliştirme araçları.
  * Merhaba gerekli en düşük sürümü Node.js 4.5 LTS ' dir.
  * [NPM](https://www.npmjs.com) hello Node.js paket yöneticilerinden biridir.

## <a name="what-you-need"></a>Ne gerekiyor
toocomplete bu işlem, gerekir:

* Bir Internet bağlantısı toodownload geliştirme araçları hello ve yazılım hello.
* Ubuntu 16.04 veya sonraki sürümünü çalıştıran bir bilgisayar.

## <a name="install-git-nodejs-and-npm"></a>Git, Node.js ve NPM yükleme
Kullanım hello klavye kısayolu `Ctrl + Alt + T` tooopen aşağıdaki terminal ve çalışma hello komutlar:

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a>Ek Node.js geliştirme araçlarını yükleme
Kullanım [gulp.js](http://gulpjs.com) hello örnek uygulama tooPi tooautomate hello dağıtımı. Kullanım hello [aygıt bulma CLI](https://github.com/Azure/device-discovery-cli) IOT aygıtlarınızla ilgili tooretrieve ağ bilgileri.

Yükleme `gulp` ve `device-discovery-cli` komutu hello terminalde aşağıdaki hello çalıştırarak:

```bash
sudo npm install -g device-discovery-cli gulp
```

Node.js ve bu ek geliştirme araçları üzerinde Ubuntu yüklerken sorunlarla karşılaşırsanız, hello bkz [sorun giderme kılavuzu](iot-hub-raspberry-pi-kit-c-troubleshooting.md) çözümleri toocommon sorunları.

## <a name="install-visual-studio-code"></a>Visual Studio Kodu'nu yükle
[Karşıdan](https://code.visualstudio.com/docs/setup/linux) ve Visual Studio Code yükleyin. Visual Studio Code, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisidir. Daha sonra hello öğretici tooedit hello örnek kodda bu Düzenleyicisi'ni kullanın.

## <a name="summary"></a>Özet
Gerekli hello geliştirme araçları ve hello ilk örnek uygulama için yazılım yüklediniz. Merhaba sonraki toocreate bir görevdir, dağıtmak ve üzerinde Pi hello örnek uygulamayı çalıştırın.

## <a name="next-steps"></a>Sonraki adımlar
[Merhaba blink uygulama oluşturun ve dağıtın](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

