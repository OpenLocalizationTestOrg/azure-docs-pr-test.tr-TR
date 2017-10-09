---
title: "Arduino tooAzure IOT - Ders 2 bağlanın: Azure araçlarını (Windows) | Microsoft Docs"
description: "Python ve hello Azure komut satırı arabirimi (Azure CLI) Windows 7 ve sonraki sürümlerde yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure CLI, IOT bulut hizmeti, arduino bulut
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 70dfff14-4be1-468d-9919-e40f4bead308
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f9b891224ff3974d9ce5382eb983470d5d41bcc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a>Azure araçlarını (Windows 7 ve üzeri) Al

> [!div class="op_single_selector"]
> * [Windows 7 veya üzeri][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>Ne yapacağını

Python yüklemek ve Azure komut satırı arabirimi (Azure CLI) hello. Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) Adafruit yumuşatma M0 WiFi Arduino panonuz için.

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:
* Nasıl tooinstall Python.
* Nasıl tooinstall Azure CLI hello.

## <a name="what-you-need"></a>Ne gerekiyor
* Bir Internet bağlantısı olan bir Windows bilgisayar.
* Etkin bir Azure aboneliği. Bir Azure hesabınız yoksa, oluşturma bir [ücretsiz Azure deneme hesabı](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.

## <a name="install-python"></a>Python yüklemek
[Python yüklemek](https://www.python.org/downloads/) Windows bilgisayarınızda. Python 2.7, 3.4 veya 3.5 yükleyebilirsiniz. Bu öğretici, Python 2.7 temel alır. Python'ı zaten yüklediyseniz, toohello sonraki bölümüne gidin ve hello Azure CLI yükleyin.

Tooadd hello yolu Python.exe'yi ve pip.exe nerede yüklü toohello sistem hello klasörlerinin etmeniz `PATH` ortam değişkeni. Varsayılan olarak, Python.exe'yi yüklü `C:\Python27` ve pip.exe yüklü `C:\Python27\Scripts`.

## <a name="install-hello-azure-cli"></a>Hello Azure CLI yükleme
Hello Azure CLI, Azure için birden çok platformlu bir komut satırı deneyimi sağlar. Doğrudan, komut satırı tooprovision çalışma ve kaynaklarını yönetme.

tooinstall hello Azure CLI, şu adımları izleyin:

1. Yönetici olarak bir komut istemi penceresi açın.
2. Merhaba aşağıdaki komutları çalıştırın:

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. Merhaba aşağıdaki komutu çalıştırarak Hello yüklemeyi doğrulayın:

   ```bash
   az iot -h
   ```

Merhaba yükleme başarılı olup olmadığını hello aşağıdaki çıktı görürsünüz.

![Başarı belirten bir çıkış][output]

## <a name="summary"></a>Özet
Hello Azure CLI yüklediniz. Sonraki görev toocreate Azure IOT hub ve cihaz kimliğini hello Azure CLI kullanarak.

## <a name="next-steps"></a>Sonraki adımlar
[IOT hub'ınızı oluşturun ve Arduino panonuzu kaydedin][create-your-iot-hub-and-register-your-arduino-board]


<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_win.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md