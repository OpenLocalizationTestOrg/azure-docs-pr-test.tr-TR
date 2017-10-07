---
title: "SensorTag cihaz & Azure IOT ağ geçidi - Ders 4: işlev uygulaması oluşturma | Microsoft Docs"
description: "Intel NUC tooyour IOT hub'ından iletileri kaydetmek için tooAzure tablo depolama yazma ve bunları hello buluttan okuyun."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Merhaba bulutta, bulutta depolanan veriler veri depolama IOT bulut hizmeti
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f84f9a85-e2c4-4a92-8969-f65eb34c194e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: efee3bdc15ced104651f4a500311a5fe614267c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a>Azure işlev uygulaması ve depolama hesabı oluşturma

Azure işlevleri; kolayca çalıştırmak için bir çözüm _işlevleri_ (küçük kod parçalarını) hello bulutta. Azure'da işlevlerinizin yürütülmesini hello Azure işlev uygulaması barındırır. 

## <a name="what-you-will-do"></a>Ne yapacağını

- Bir Azure Resource Manager şablonu toocreate bir Azure işlevi uygulama ve bir Azure depolama hesabı kullanın. Hello Azure işlev uygulaması tooAzure IOT hub olayları dinler, gelen iletileri işleme ve tooAzure Table storage yazar.

Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).


## <a name="what-you-will-learn"></a>Bilgi edineceksiniz

Bu alıştırmanın ilerisinde şunları öğreneceksiniz:

- Nasıl toouse Azure Resource Manager toodeploy Azure kaynakları.
- Nasıl toouse Azure app tooprocess IOT hub'ı iletileri işlev ve bunları Azure Table storage ' tooa tablo yazar.

## <a name="what-you-need"></a>Ne gerekiyor

Başarılı bir şekilde hello önceki dersleri tamamlamış olmanız gerekir:

- [Ders 1:, Intel NUC IOT ağ geçidi olarak ayarlama](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
- [Ders 2: ana bilgisayar ve Azure IOT hub'ı hazırlanın](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
- [Ders 3: SensorTag iletileri almasına ve IOT hub'ından iletileri okur](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

## <a name="open-a-sample-app"></a>Bir örnek uygulamasını açın

Tooyour Git `iot-hub-c-intel-nuc-gateway-getting-started` depodaki klasörü, başlatma hello yapılandırma dosyalarını ve Visual Studio Code sonra açık hello örnek proje hello aşağıdaki komutu çalıştırarak:

```bash
cd Lesson4
npm install
gulp init
code .
```

![Depodaki yapısı](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- Merhaba `arm-template.json` bir Azure işlevi uygulama ve Azure storage hesabı içeren hello Azure Resource Manager şablonu bir dosyadır.
- Merhaba `arm-template-param.json` hello Azure Resource Manager şablonu tarafından kullanılan hello yapılandırma dosyası bir dosyadır.
- Merhaba `ReceiveDeviceMessages` alt hello Azure işlevi için hello Node.js kodunu içerir.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Azure Resource Manager şablonları yapılandırmak ve kaynakları oluşturma

Güncelleştirme hello `arm-template-param.json` Visual Studio Code dosyasında.

![ARM şablonu json](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- Değiştir `[your IoT Hub name]` ile `{my hub name}` Ders 2'de belirtilen.

Merhaba güncelleştirdikten sonra `arm-template-param.json` dosya, komutu aşağıdaki hello çalıştırarak hello kaynakları tooAzure dağıtma:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

Kullanım `iot-gateway` hello değeri olarak `{resource group name}` Ders 2 hello değerinde değiştirilmediyse.

## <a name="summary"></a>Özet

IOT hub iletileri Azure işlevi uygulama tooprocess oluşturduğunuz ve bir Azure depolama hesabı toostore bu iletiler. Şimdi, ağ geçidi tooyour IOT hub tarafından gönderilen iletileri okuyabilir.

## <a name="next-steps"></a>Sonraki adımlar
[İletileri okuma Azure Depolama'da kalıcı](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).
