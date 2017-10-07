---
title: "Raspberry Pi'yi (düğüm) tooAzure IOT - Ders 2 bağlanın: Get Araçlar (Ubuntu) | Microsoft Docs"
description: "Python yüklemek ve Azure komut satırı arabirimi (Azure CLI) üzerinde macOS hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: IOT bulut hizmeti, azure CLI
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 1814b703-2d81-45db-aff0-eb338c97f120
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 3f35fae53a360a758bc8f61ed2063f7e2f2dc067
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-macos-1010"></a>Azure Araçları (macOS 10.10) alın
> [!div class="op_single_selector"]
> * [Windows 7 ve üzeri](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>Ne yapacağını
Hello Azure komut satırı arabirimi (Azure CLI) yükleyin. Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:
* Nasıl tooinstall Azure CLI.
* Nasıl tooadd hello Azure CLI IOT GUID'sinin.

## <a name="what-you-need"></a>Ne gerekiyor
* Internet bağlantısı olan Mac.
* Etkin bir Azure aboneliği. Bir Azure hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz Azure deneme hesabı](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.

## <a name="install-python"></a>Python yüklemek
MacOS hello kutu dışı Python 2.7 ile veriliyorsa da Homebrew aracılığıyla Python yüklemenizi öneririz. Bkz: [yükleme Python macOS üzerinde](http://docs.python-guide.org/en/latest/starting/install/osx/).

Python ve PIP hello aşağıdaki komutu çalıştırarak yükleyin:

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a>Hello Azure CLI yükleme
Hello Azure CLI, Azure için birden çok platformlu bir komut satırı deneyimi sağlar. Doğrudan komut satırı, tooprovision çalışma ve kaynaklarını yönetme. 

tooinstall en son Azure CLI Merhaba, şu adımları izleyin:

1. Bir terminal penceresi komutlarda aşağıdaki hello çalıştırın. Beş dakika tooinstall hello Azure CLI alabilir.

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. Merhaba aşağıdaki komutu çalıştırarak Hello yüklemeyi doğrulayın:

   ```bash
   az iot -h
   ```

Merhaba yükleme başarılı olup olmadığını hello aşağıdaki çıktı görmeniz gerekir.

![Başarı belirten bir çıkış](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a>Özet
Hello Azure CLI yüklediniz. Sonraki göreviniz toocreate olan Azure CLI kullanarak Azure IOT hub ve cihaz kimliğinizi hello.

## <a name="next-steps"></a>Sonraki adımlar
[IOT hub'ınızı oluşturun ve Raspberry Pi 3 kaydedin](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

