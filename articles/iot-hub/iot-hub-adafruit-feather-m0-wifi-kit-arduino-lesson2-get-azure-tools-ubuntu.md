---
title: "Azure IOT - Ders 2 Arduino bağlanın: Azure Araçları (Ubuntu) | Microsoft Docs"
description: "Python ve Azure komut satırı arabirimi (Azure CLI) üzerinde Ubuntu yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure CLI, IOT bulut hizmeti, arduino bulut
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: bb5cb602-7292-4772-ac90-c0b52ebc8340
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a2f83e59a37abc3f44e770b22ac089b88481a6a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a>Azure Araçları (Ubuntu 16.04) alın

> [!div class="op_single_selector"]
> * [Windows 7 veya üzeri][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>Ne yapacağını

Azure komut satırı arabirimi (Azure CLI) yükleyin. Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) Adafruit yumuşatma M0 WiFi Arduino panonuz için.

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:
* Azure CLI yükleme.
* Azure CLI IOT GUID'sinin ekleme.

## <a name="what-you-need"></a>Ne gerekiyor
* Bir Internet bağlantısı olan bir Ubuntu bilgisayar.
* Etkin bir Azure aboneliği. Bir hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz deneme sürümü hesabı](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.

## <a name="install-the-azure-cli"></a>Azure CLI'yı yükleme
Azure CLI çok platformlu bir komut satırı deneyimi, Azure için doğrudan komut satırından sağlamak için çalışma ve kaynakları yönetmenize olanak sağlar.

En son Azure CLI yüklemek için aşağıdaki adımları izleyin:

1. Bir terminal penceresi aşağıdaki komutları çalıştırın. Azure CLI yüklemek için beş dakika sürebilir.

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. Aşağıdaki komutu çalıştırarak yüklemeyi doğrulayın:

   ```bash
   az iot -h
   ```

Yükleme başarılı olursa aşağıdaki çıktı görmeniz gerekir.

![Başarı belirten bir çıkış][output]

## <a name="summary"></a>Özet
Azure CLI yüklediniz. Sonraki göreviniz Azure CLI kullanarak Azure IOT hub ve cihaz kimliğinizi oluşturmaktır.

## <a name="next-steps"></a>Sonraki adımlar
[IOT hub'ınızı oluşturun ve Arduino panonuzu kaydedin][create-your-iot-hub-and-register-your-arduino-board]
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_ubuntu.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md