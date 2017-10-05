---
title: "Benzetimli cihaz & Azure IOT ağ geçidi - Ders 2: alma araçlarını (Windows) | Microsoft Docs"
description: "Araçlar ve yazılımı Windows çalıştıran ana bilgisayarınıza yüklemek, IOT hub'ı oluşturun ve IOT hub'ı Cihazınızı kaydedin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IOT geliştirme, IOT yazılım IOT bulut hizmeti, şeyler yazılım, azure CLI, Internet Windows Git'i yükleyin, çalışma gulp, düğüm js Windows'u yüklemek, Windows npm yükleme, Windows'da python yüklemek"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: c16eee4c-8756-454b-82bf-3eb0dd51aa5f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ecedf5ef89677c73c5d9a3e5250eb9f45f6bad32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-and-later"></a>(Windows 7 ve üzeri) araçları edinin
> [!div class="op_single_selector"]
> * [Windows 7 veya üzeri](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Ne yapacağını

- Git, Node.js, Gulp, Python yükleyin.
- Azure komut satırı arabirimi (Azure CLI) yükleyin. 

Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz

Bu alıştırmanın ilerisinde şunları öğreneceksiniz:

- Yükleme [Git](https://git-scm.com/) ve [Node.js](https://nodejs.org/en/).
  - Git bir açık kaynak dağıtılmış sürüm denetim sistemidir. Örnek bir uygulama bu ders için Git üzerinde depolanır.
  - Node.js, JavaScript çalışma zamanı zengin paket ekosistemi ile olur.
- Nasıl kullanılacağını [NPM](https://www.npmjs.com/) Node.js geliştirme araçlarını yüklemek için.
  - Node.js, gerekli en düşük sürüm 4.5 LTS ' dir.
  - NPM Node.js paket yöneticilerinden biridir.
- Visual Studio Code yükleme.
  - Visual Studio platformlar arası, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisini kodudur. Hata ayıklama, katıştırılmış Git denetimi, sözdizimi vurgulama, akıllı kod tamamlama, parçacıkları ve kod da yeniden düzenleme için harika desteğe sahiptir.
- Python yükleme.
  - Python yaygın olarak kullanılan üst düzey, genel amaçlı, yorumlanan ve dinamik programlama dilidir.
- Azure CLI yükleme.
  - Azure CLI, Azure için birden çok platformlu bir komut satırı deneyimi sağlar. Doğrudan komut satırından sağlamak için çalışır ve kaynaklarını yönetme.
- IOT hub'ı oluşturmak için Azure CLI kullanma

## <a name="what-you-need"></a>Ne gerekiyor

- Araçlar ve yazılım indirmesi için Internet bağlantısı.
- Bir Windows bilgisayarı.

## <a name="install-git-and-nodejs"></a>Git ve Node.js yükleyin

İndirmek ve Git ve Windows için Node.js LTS yüklemek için aşağıdaki bağlantıları tıklatın.

- [Windows için Git Al](https://git-scm.com/download/win/)
- [Windows için node.js LTS Al](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a>Node.js geliştirme araçlarını yükleme

Kullandığınız [gulp.js](http://gulpjs.com/) dağıtım ve betiklerinin yürütülmesi otomatik hale getirmek için.

Basın `Windows + R`, türü `cmd` ve basın `Enter` bir komut istemi penceresi açın ve ardından aşağıdaki komutu çalıştırın:

```cmd
npm install -g gulp
```

Yükleme sorunlarıyla karşılaşırsanız, bkz: [sorun giderme kılavuzu](iot-hub-gateway-kit-c-sim-troubleshooting.md) yaygın sorunların çözümleri için.

> [!Note]
> Düğüm, NPM ve Gulp Node.js içinde geliştirilen Otomasyon betikleri çalıştırmak için gereklidir.

## <a name="install-python"></a>Python yüklemek

Python 2.7, 3.4 veya 3.5 seçebilirsiniz. Bu öğreticide, Python 2.7 kullanırız. Python'ı zaten yüklediyseniz, sonraki bölüme gidin.

[Python için Windows Al](https://www.python.org/downloads/)

Ayrıca Python.exe'yi ve pip.exe yüklendiği için sistem klasörlerinin yolu eklemek gereken `PATH` ortam değişkeni. Varsayılan olarak, Python.exe'yi yüklü `C:\Python27` ve pip.exe yüklü `C:\Python27\Scripts`.

## <a name="install-the-azure-cli"></a>Azure CLI'yı yükleme

Azure CLI yüklemek için aşağıdaki adımları izleyin:

1. Yönetici olarak bir komut istemi penceresi açın.

2. Azure CLI aşağıdaki komutları çalıştırarak yükleyin:

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   Yükleme 5 dakika sürebilir.

3. Aşağıdaki komutu çalıştırarak yüklemeyi doğrulayın:

   ```cmd
   az iot -h
   ```

   Yükleme başarılı olursa aşağıdaki çıktı görmeniz gerekir.

   ![Azure CLI yükleme doğrulayın](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a>Visual Studio Kodu'nu yükle

Visual Studio Code öğreticide daha sonra yapılandırma dosyalarını düzenlemek için kullanın.

[Karşıdan](https://code.visualstudio.com/docs/setup/windows) ve Visual Studio Code yükleyin.

## <a name="summary"></a>Özet

Tüm gerekli araçlar ve yazılım ana bilgisayara yüklediniz. Sonraki göreviniz IOT hub'ı oluşturun ve IOT hub'ınıza Cihazınızı kaydetmek için Azure CLI kullanmaktır.

## <a name="next-steps"></a>Sonraki adımlar
[IoT hub'ı oluşturma ve cihazınızı kaydetme](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
