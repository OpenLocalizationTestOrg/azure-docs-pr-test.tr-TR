---
title: "Azure IOT - Ders 2 Connect Intel Edison (C): Azure Araçları (macOS) | Microsoft Docs"
description: "Python ve Azure komut satırı arabirimi (Azure CLI) üzerinde macOS yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure CLI, IOT bulut hizmeti, arduino bulut
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: d561680f-69cc-427a-820d-24f710ba05a8
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 97beb04781f3f9809cdafc945d9499e71cbbd9b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-macos-1010"></a>Azure Araçları (macOS 10.10) alın
> [!div class="op_single_selector"]
> * [Windows 7 ve üzeri][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>Ne yapacağını
Azure komut satırı arabirimi (Azure CLI) yükleyin. Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:
* Azure CLI yükleme.
* Azure CLI IOT GUID'sinin ekleme.

## <a name="what-you-need"></a>Ne gerekiyor
* Internet bağlantısı olan Mac.
* Etkin bir Azure aboneliği. Bir Azure hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz Azure deneme hesabı](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.

## <a name="install-python"></a>Python yüklemek
MacOS kutu dışı Python 2.7 ile veriliyorsa da Homebrew aracılığıyla Python yüklemenizi öneririz. Bkz: [yükleme Python macOS üzerinde](http://docs.python-guide.org/en/latest/starting/install/osx/).

Python ve PIP aşağıdaki komutu çalıştırarak yükleyin:

```bash
brew install python
```

## <a name="install-the-azure-cli"></a>Azure CLI'yı yükleme
Azure CLI, Azure için birden çok platformlu bir komut satırı deneyimi sağlar. Doğrudan komut satırından sağlamak için çalışır ve kaynaklarını yönetme. 

En son Azure CLI yüklemek için aşağıdaki adımları izleyin:

1. Bir terminal penceresi aşağıdaki komutları çalıştırın. Azure CLI yüklemek için beş dakika sürebilir.

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. Aşağıdaki komutu çalıştırarak yüklemeyi doğrulayın:

   ```bash
   az iot -h
   ```

Yükleme başarılı olursa aşağıdaki çıktı görmeniz gerekir.

![Başarı belirten bir çıkış](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a>Özet
Azure CLI yüklediniz. Sonraki göreviniz, Azure CLI kullanarak Azure IOT hub ve cihaz kimliğini oluşturmaktır.

## <a name="next-steps"></a>Sonraki adımlar
[IOT hub'ınızı oluşturun ve Intel Edison'u kaydedin][create-your-iot-hub-and-register-intel-edison]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
