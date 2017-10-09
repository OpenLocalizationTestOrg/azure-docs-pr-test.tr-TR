---
title: "Raspberry Pi'yi (düğüm) tooAzure IOT - Ders 1 bağlanın: alma araçlarını (Windows) | Microsoft Docs"
description: "İndirin ve Windows 7 ve sonraki sürümlerde hello gerekli araçları ve Merhaba ilk örnek uygulaması pi yazılımı yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IOT geliştirme IOT yazılım, şeyler yazılımların internet windows Git'i yükleyin, çalışma gulp, düğüm js Windows'u yüklemek, windows npm yükleme, Windows'da python yüklemek"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b3d88e17-97cc-4f23-85fd-a688fc228eb8
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ea7f77cc79c70c8c7952b63462b926471fcf71cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a>(Windows 7 veya üzeri) Hello araçları edinin

> [!div class="op_single_selector"]
> * [Windows 7 veya üzeri](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a>Ne yapacağını
Merhaba geliştirme araçları ve hello ilk örnek bir uygulama için Raspberry Pi 3 hello yazılımı yükleyin. Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

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
Bağlantılar toodownload aşağıdaki hello'ı tıklatın ve Git ve Windows için Node.js LTS yükleyin.

* [Windows için Git Al](https://git-scm.com/download/win/)
* [Windows için node.js LTS Al](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a>Ek Node.js geliştirme araçlarını yükleme
Kullanım [gulp.js](http://gulpjs.com) hello örnek uygulama tooPi tooautomate hello dağıtımı. Merhaba de [aygıt bulma CLI](https://github.com/Azure/device-discovery-cli) IOT aygıtlarınızla ilgili tooretrieve ağ bilgileri.

Bir komut istemini yönetici olarak başlatın. Yükleme `gulp` ve `device-discovery-cli` hello aşağıdaki komutu çalıştırarak:

```bash
npm install -g device-discovery-cli gulp
```

Node.js ve bu ek Node.js geliştirme araçları bilgisayarınızda yüklerken sorunlarla karşılaşırsanız, hello bkz [sorun giderme kılavuzu](iot-hub-raspberry-pi-kit-node-troubleshooting.md) çözümleri toocommon sorunları.

## <a name="install-visual-studio-code"></a>Visual Studio Kodu'nu yükle
[Karşıdan](https://code.visualstudio.com/docs/setup/windows) ve Visual Studio Code yükleyin. Visual Studio Code, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisidir. Daha sonra hello öğretici tooedit hello örnek kodda bu Düzenleyicisi'ni kullanın.

## <a name="summary"></a>Özet
Gerekli hello geliştirme araçları ve hello ilk örnek uygulama için yazılım yüklediniz. Merhaba sonraki toocreate bir görevdir, dağıtmak ve üzerinde Pi hello örnek uygulamayı çalıştırın.

## <a name="next-steps"></a>Sonraki adımlar
[Merhaba blink örnek uygulama oluşturun ve dağıtın](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

