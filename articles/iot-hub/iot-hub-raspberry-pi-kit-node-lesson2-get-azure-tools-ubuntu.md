---
title: "Raspberry Pi'yi (düğüm) tooAzure IOT - Ders 2 bağlanın: Get Araçlar (Ubuntu) | Microsoft Docs"
description: "Python yüklemek ve Azure komut satırı arabirimi (Azure CLI) üzerinde Ubuntu hello."
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
ms.openlocfilehash: 0adf91bef41f502e1333fdcc75cfb2fe912364c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a>Azure Araçları (Ubuntu 16.04) alın
> [!div class="op_single_selector"]
> * [Windows 7 ve üzeri](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>Ne yapacağını
Hello Azure komut satırı arabirimi (Azure CLI) yükleyin. Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:
* Nasıl tooinstall Azure CLI hello.
* Nasıl tooadd hello Azure CLI IOT GUID'sinin.

## <a name="what-you-need"></a>Ne gerekiyor
* Bir Internet bağlantısı olan bir Ubuntu bilgisayar.
* Etkin bir Azure aboneliği. Bir hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz deneme sürümü hesabı](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.

## <a name="install-hello-azure-cli"></a>Hello Azure CLI yükleme
Hello Azure CLI, Azure, komut satırı tooprovision doğrudan toowork etkinleştirme için birden çok platformlu bir komut satırı deneyimi sağlar ve kaynakları yönetin.

tooinstall en son Azure CLI Merhaba, şu adımları izleyin:

1. Bir terminal penceresi komutlarda aşağıdaki hello çalıştırın. Beş dakika tooinstall hello Azure CLI alabilir.

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. Merhaba aşağıdaki komutu çalıştırarak Hello yüklemeyi doğrulayın:

   ```bash
   az iot -h
   ```

Merhaba yükleme başarılı olup olmadığını hello aşağıdaki çıktı görmeniz gerekir.

![Başarı belirten bir çıkış](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a>Özet
Hello Azure CLI yüklediniz. Sonraki göreviniz toocreate olan Azure IOT hub ve cihaz kimliğini kullanarak Azure CLI hello.

## <a name="next-steps"></a>Sonraki adımlar
[IOT hub'ınızı oluşturun ve Raspberry Pi 3 kaydedin](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

