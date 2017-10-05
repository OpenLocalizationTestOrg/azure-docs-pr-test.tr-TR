---
title: "Benzetimli cihaz & Azure IOT ağ geçidi - Ders 4: iletileri kaydetme | Microsoft Docs"
description: "IOT hub'ınıza Intel NUC iletileri kaydetmek için bunları Azure Table depolama alanına yazmak ve bunları buluttan okuyun."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: bulutta depolanan veriler bulutta veri depolama IOT bulut hizmeti
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: ffed0c2e-b092-40e1-9113-8196ec057d67
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c7fc47b07acede28ffe790debca7e38521726011
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a>Azure işlev uygulaması ve depolama hesabı oluşturma

Azure işlevleri; kolayca çalıştırmak için bir çözüm _işlevleri_ (küçük kod parçalarını) bulutta. Azure'da işlevlerinizin yürütülmesini bir Azure işlev uygulaması barındırır. 

## <a name="what-you-will-do"></a>Ne yapacağını

- Bir Azure işlevi uygulama ve Azure storage hesabı oluşturmak için bir Azure Resource Manager şablonunu kullanın. Azure işlev uygulaması Azure IOT hub olayları dinler, gelen iletileri işler ve bunları Azure Table depolama alanına yazar.

Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-gateway-kit-c-sim-troubleshooting.md).


## <a name="what-you-will-learn"></a>Bilgi edineceksiniz

Bu alıştırmanın ilerisinde şunları öğreneceksiniz:

- Azure Resource Manager Azure kaynaklarınızı dağıtmak için nasıl kullanılacağını.
- IOT hub'ı iletileri işlemek ve bunları Azure Table depolama tabloda yazmak için bir Azure işlev uygulaması kullanma

## <a name="what-you-need"></a>Ne gerekiyor

Başarıyla önceki dersleri tamamlamış olmanız gerekir:

- [Ders 1:, Intel NUC IOT ağ geçidi olarak ayarlama](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)
- [Ders 2: ana bilgisayar ve Azure IOT hub'ı hazırlanın](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
- [Ders 3: sanal cihaz iletileri almak ve IOT hub'ından iletileri okur](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

## <a name="open-a-sample-app"></a>Bir örnek uygulamasını açın

Gidin, `iot-hub-c-intel-nuc-gateway-getting-started` deposu klasör, yapılandırma dosyalarını başlatın ve aşağıdaki komutu çalıştırarak bu örnek proje Visual Studio kodda açın:

```bash
cd Lesson4
npm install
gulp init
code .
```

![Depodaki yapısı](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- `arm-template.json` Bir Azure işlevi uygulama ve Azure storage hesabı içeren Azure Resource Manager şablonu bir dosyadır.
- `arm-template-param.json` Azure Resource Manager şablonu tarafından kullanılan yapılandırma dosyasını bir dosyadır.
- `ReceiveDeviceMessages` Alt Azure işlevi için Node.js kodunu içerir.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Azure Resource Manager şablonları yapılandırmak ve kaynakları oluşturma

Güncelleştirme `arm-template-param.json` Visual Studio Code dosyasında.

![ARM şablonu json](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- Değiştir `[your IoT Hub name]` ile `{my hub name}` Ders 2'de belirtilen.

Güncelleştirdikten sonra `arm-template-param.json` dosya, aşağıdaki komutu çalıştırarak kaynakları Azure'a dağıtma:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

Kullanım `iot-gateway` değeri olarak `{resource group name}` Ders 2 değerinde değiştirilmediyse.

## <a name="summary"></a>Özet

IOT hub iletileri ve Azure storage hesabı bu iletileri depolamak için işlemek için Azure işlevi uygulamanızı oluşturdunuz. Şimdi, ağ geçidi IOT hub'ınıza gönderdiği iletileri okuyabilir.

## <a name="next-steps"></a>Sonraki adımlar
[İletileri okuma Azure Depolama'da kalıcı](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).
