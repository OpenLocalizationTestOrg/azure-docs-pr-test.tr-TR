---
title: "Azure IOT - Ders 2 Intel Edison'u (düğüm) bağlanma: Azure araçlarını (Windows) | Microsoft Docs"
description: "Python ve Azure komut satırı arabirimi (Azure CLI) Windows 7 ve sonraki sürümlerde yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure CLI, IOT bulut hizmeti, arduino bulut
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 60631b54-6d2e-4e8a-88bf-7c2f8e7e1f29
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7257fe98fa1075456de620ca46b4e10c34e06574
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a>Azure araçlarını (Windows 7 ve üzeri) Al
> [!div class="op_single_selector"]
> * [Windows 7 ve üzeri][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>Ne yapacağını
Python ve Azure komut satırı arabirimi (Azure CLI) yükleyin. Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:
* Python yükleme.
* Azure CLI yükleme.

## <a name="what-you-need"></a>Ne gerekiyor
* Bir Internet bağlantısı olan bir Windows bilgisayar.
* Etkin bir Azure aboneliği. Bir Azure hesabınız yoksa, oluşturma bir [ücretsiz Azure deneme hesabı](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.

## <a name="install-python"></a>Python yüklemek
[Python yüklemek](https://www.python.org/downloads/) Windows bilgisayarınızda. Python 2.7, 3.4 veya 3.5 yükleyebilirsiniz. Bu öğretici, Python 2.7 temel alır. Python'ı zaten yüklediyseniz, sonraki bölüme gidin ve Azure CLI yükleme.

Ayrıca Python.exe'yi ve pip.exe yüklendiği için sistem klasörlerinin yolu eklemek gereken `PATH` ortam değişkeni. Varsayılan olarak, Python.exe'yi yüklü `C:\Python27` ve pip.exe yüklü `C:\Python27\Scripts`.

## <a name="install-the-azure-cli"></a>Azure CLI'yı yükleme
Azure CLI, Azure için birden çok platformlu bir komut satırı deneyimi sağlar. Doğrudan komut satırından sağlamak için çalışır ve kaynaklarını yönetme.

Azure CLI yüklemek için aşağıdaki adımları izleyin:

1. Yönetici olarak bir komut istemi penceresi açın.
2. Aşağıdaki komutları çalıştırın:

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. Aşağıdaki komutu çalıştırarak yüklemeyi doğrulayın:

   ```cmd
   az iot -h
   ```

Yükleme başarılı olursa, aşağıdaki çıkış görürsünüz.

![Başarı belirten bir çıkış](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a>Özet
Azure CLI yüklediniz. Azure CLI kullanarak Azure IOT hub ve cihaz kimliğini oluşturmak için sonraki göreviniz.

## <a name="next-steps"></a>Sonraki adımlar
[IOT hub'ınızı oluşturun ve Intel Edison'u kaydedin][create-your-iot-hub-and-register-intel-edison]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-mac.md
