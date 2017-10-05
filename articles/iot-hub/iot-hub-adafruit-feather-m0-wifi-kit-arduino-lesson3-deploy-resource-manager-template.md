---
title: "Azure IOT - Ders 3 Connect Arduino (C): şablon dağıtımı | Microsoft Docs"
description: "Azure işlev uygulaması Azure IOT hub olayları dinler, gelen iletileri işler ve bunları Azure Table depolama alanına yazar."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: bulutta depolanan veriler bulutta veri depolama IOT bulut hizmeti
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9c8f4cd1-9511-4601-ad7e-51761a986753
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: be6105927645ae2ec56f6885c61dbcb6faf5b11f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a>Bir Azure işlevi uygulama ve Azure depolama hesabı oluştur
[Azure işlevleri](../../articles/azure-functions/functions-overview.md) kolayca çalıştırmak için bir çözüm *işlevleri* (küçük kod parçalarını) bulutta. Azure'da işlevlerinizin yürütülmesini bir Azure işlev uygulaması barındırır.

## <a name="what-will-you-do"></a>Ne
Bir Azure işlevi uygulama ve Azure storage hesabı oluşturmak için bir Azure Resource Manager şablonunu kullanın. Azure işlev uygulaması Azure IOT hub olayları dinler, gelen iletileri işler ve bunları Azure Table depolama alanına yazar.

Herhangi bir sorun varsa, çözümleri için Ara [sayfa Adafruit yumuşatma M0 WiFi Arduino panonuz için sorun giderme](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).

## <a name="what-will-you-learn"></a>Ne size bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:
* Nasıl kullanılacağını [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) Azure kaynaklarınızı dağıtmak için.
* IOT hub iletileri işlemek ve bunları Azure Table depolama tabloda yazmak için bir Azure işlev uygulaması kullanma

## <a name="what-do-you-need"></a>Ne ihtiyacınız var
Başarılı bir şekilde tamamladınız gerekir:
- [Arduino panonuzu ile çalışmaya başlama][get-started]
- [Azure IOT hub'ınızı oluşturma][create-iot-hub]

## <a name="open-the-sample-app"></a>Örnek uygulamayı açın
Örnek Proje aşağıdaki komutları çalıştırarak Visual Studio kodda açın:

```bash
cd Lesson3
code .
```

![Depodaki yapısı][repo-structure]

* `app.ino` Dosyasını `app` alt anahtarı kaynağı dosyasıdır. Bu kaynak dosyası 20 kez IOT hub'ınıza ileti gönderme ve LED, gönderdiği her ileti için blink kodunu içerir.
* `config.json` Gerekli yapılandırma ayarlarını içerir.
* `arm-template.json` Bir Azure işlevi uygulama ve Azure storage hesabı içeren Azure Resource Manager şablonu bir dosyadır.
* `arm-template-param.json` Azure Resource Manager şablonu tarafından kullanılan yapılandırma dosyasını bir dosyadır.
* `ReceiveDeviceMessages` Alt Azure işlevi için Node.js kodunu içerir.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Azure Resource Manager şablonları yapılandırmak ve kaynakları oluşturma
Güncelleştirme `arm-template-param.json` Visual Studio Code dosyasında.

![Azure Resource Manager şablonu parametreleri][arm-template-params]

* Değiştir **[IOT Hub adınız]** ile **{hub adımın}** ne zaman belirtilen, [IOT hub'ınızı oluşturulur ve Arduino panonuzu kayıtlı] [ created-iot-hub-and-registered-arduino-board].
* Değiştir **[önek dizesi yeni kaynaklar için]** istediğiniz tüm ön ekine sahip. Önek, kaynak adı çakışmayı önlemek için genel benzersiz olmasını sağlar. Bir çizgi ya da rakamla önekini ilk kullanmayın.

Güncelleştirdikten sonra `arm-template-param.json` dosya, aşağıdaki komutu çalıştırarak kaynakları Azure'a dağıtma:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

Bu kaynakları oluşturmak için yaklaşık beş dakika sürer. Kaynak oluşturma işlemi devam ederken, sonraki makalede hareket ettirebilirsiniz.

## <a name="summary"></a>Özet
IOT hub iletileri ve Azure storage hesabı bu iletileri depolamak için işlemek için Azure işlevi uygulamanızı oluşturdunuz. Şimdi, dağıtın ve Arduino Panonuzda cihaz bulut iletilerini göndermek için örnek çalıştırın.

## <a name="next-steps"></a>Sonraki adımlar
[Arduino Panonuzda cihaz bulut iletilerini göndermek için bir örnek uygulamayı çalıştırın][send-device-to-cloud-messages]

<!-- Images and links -->

[get-started]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[create-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/repo_structure_c.png
[arm-template-params]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/arm_para_arduino.png
[created-iot-hub-and-registered-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md