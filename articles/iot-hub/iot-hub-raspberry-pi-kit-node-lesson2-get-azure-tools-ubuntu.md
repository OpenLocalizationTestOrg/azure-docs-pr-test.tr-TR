---
title: "Azure IOT - Ders 2 Raspberry Pi'yi (düğüm) bağlanma: Get Araçlar (Ubuntu) | Microsoft Docs"
description: "Python ve Azure komut satırı arabirimi (Azure CLI) üzerinde Ubuntu yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: IOT bulut hizmeti, azure CLI
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 2f98923a-5274-4220-87d4-77ac8beb4d0f
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 3933ccea992c62da1dd402f651d5b5b4ad43713d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a>Azure Araçları (Ubuntu 16.04) alın
> [!div class="op_single_selector"]
> * [Windows 7 ve üzeri](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>Ne yapacağını
Azure komut satırı arabirimi (Azure CLI) yükleyin. Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:
* Azure CLI yükleme.
* Azure CLI IOT GUID'sinin ekleme.

## <a name="what-you-need"></a>Ne gerekiyor
* Bir Internet bağlantısı olan bir Ubuntu bilgisayar.
* Etkin bir Azure aboneliği. Bir hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz deneme sürümü hesabı](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.

## <a name="install-the-azure-cli"></a>Azure CLI'yı yükleme
Azure CLI çok platformlu bir komut satırı deneyimi, Azure için doğrudan, komut satırından sağlamak için çalışır ve kaynakları yönetmenize olanak sağlar.

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

![Başarı belirten bir çıkış](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a>Özet
Azure CLI yüklediniz. Sonraki göreviniz Azure CLI kullanarak Azure IOT hub ve cihaz kimliğinizi oluşturmaktır.

## <a name="next-steps"></a>Sonraki adımlar
[IOT hub'ınızı oluşturun ve Raspberry Pi 3 kaydedin](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

