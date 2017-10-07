---
title: "Connect Arduino (C) tooAzure IOT - Ders 3: şablon dağıtımı | Microsoft Docs"
description: "Hello Azure işlev uygulaması tooAzure IOT hub olayları dinler, gelen iletileri işleme ve tooAzure Table storage yazar."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Merhaba bulutta, bulutta depolanan veriler veri depolama IOT bulut hizmeti
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
ms.openlocfilehash: 6a84a6d3c5263a85c8997cf69fe446d73ab7a5fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a>Bir Azure işlevi uygulama ve Azure depolama hesabı oluştur
[Azure işlevleri](../../articles/azure-functions/functions-overview.md) kolayca çalıştırmak için bir çözüm *işlevleri* (küçük kod parçalarını) hello bulutta. Azure'da işlevlerinizin yürütülmesini hello Azure işlev uygulaması barındırır.

## <a name="what-will-you-do"></a>Ne
Bir Azure Resource Manager şablonu toocreate bir Azure işlevi uygulama ve bir Azure depolama hesabı kullanın. Hello Azure işlev uygulaması tooAzure IOT hub olayları dinler, gelen iletileri işleme ve tooAzure Table storage yazar.

Herhangi bir sorun varsa, hello çözümlerini arayın [sayfa Adafruit yumuşatma M0 WiFi Arduino panonuz için sorun giderme](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).

## <a name="what-will-you-learn"></a>Ne size bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:
* Nasıl toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure kaynakları.
* Nasıl toouse Azure app tooprocess IOT hub iletileri işlev ve bunları Azure Table storage ' tooa tablo yazar.

## <a name="what-do-you-need"></a>Ne ihtiyacınız var
Başarılı bir şekilde tamamladınız gerekir:
- [Arduino panonuzu ile çalışmaya başlama][get-started]
- [Azure IOT hub'ınızı oluşturma][create-iot-hub]

## <a name="open-hello-sample-app"></a>Açık hello örnek uygulaması
Merhaba aşağıdaki komutları çalıştırarak örnek proje Visual Studio Code açık hello:

```bash
cd Lesson3
code .
```

![Depodaki yapısı][repo-structure]

* Merhaba `app.ino` hello dosyasında `app` alt dosyasıdır hello anahtarı kaynağı. Bu kaynak dosya hello kod toosend gönderir 20 kez tooyour IOT hub ve blink hello LED her ileti için ileti içerir.
* Merhaba `config.json` gerekli yapılandırma ayarlarını içerir.
* Merhaba `arm-template.json` bir Azure işlevi uygulama ve Azure storage hesabı içeren hello Azure Resource Manager şablonu bir dosyadır.
* Merhaba `arm-template-param.json` hello Azure Resource Manager şablonu tarafından kullanılan hello yapılandırma dosyası bir dosyadır.
* Merhaba `ReceiveDeviceMessages` alt hello Azure işlevi için hello Node.js kodunu içerir.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Azure Resource Manager şablonları yapılandırmak ve kaynakları oluşturma
Güncelleştirme hello `arm-template-param.json` Visual Studio Code dosyasında.

![Azure Resource Manager şablonu parametreleri][arm-template-params]

* Değiştir **[IOT Hub adınız]** ile **{hub adımın}** ne zaman belirtilen, [IOT hub'ınızı oluşturulur ve Arduino panonuzu kayıtlı] [ created-iot-hub-and-registered-arduino-board].
* Değiştir **[önek dizesi yeni kaynaklar için]** istediğiniz tüm ön ekine sahip. Merhaba önek bu hello kaynak adı genel olarak benzersiz tooavoid çakışma sağlar. Bir çizgi ya da rakamla hello önekini ilk kullanmayın.

Merhaba güncelleştirdikten sonra `arm-template-param.json` dosya, komutu aşağıdaki hello çalıştırarak hello kaynakları tooAzure dağıtma:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

Bu kaynakları toocreate yaklaşık beş dakika sürer. Merhaba kaynak oluşturma işlemi devam ederken, toohello sonraki makalede taşıyabilirsiniz.

## <a name="summary"></a>Özet
IOT hub iletileri Azure işlevi uygulama tooprocess oluşturduğunuz ve bir Azure depolama hesabı toostore bu iletiler. Şimdi, dağıtın ve hello örnek toosend cihaz bulut iletilerini Arduino Panonuzda çalıştırın.

## <a name="next-steps"></a>Sonraki adımlar
[Örnek uygulama toosend cihaz bulut iletilerini Arduino Panonuzda çalıştırın.][send-device-to-cloud-messages]

<!-- Images and links -->

[get-started]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[create-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/repo_structure_c.png
[arm-template-params]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/arm_para_arduino.png
[created-iot-hub-and-registered-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md