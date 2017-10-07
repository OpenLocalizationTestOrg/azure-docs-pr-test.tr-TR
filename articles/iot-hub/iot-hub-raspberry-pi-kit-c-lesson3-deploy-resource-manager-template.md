---
title: "Connect Raspberry pi (C) tooAzure IOT - Ders 3: şablon dağıtımı | Microsoft Docs"
description: "Hello Azure işlev uygulaması tooAzure IOT hub olayları dinler, gelen iletileri işleme ve tooAzure Table storage yazar."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Merhaba bulutta, bulutta depolanan veriler veri depolama IOT bulut hizmeti
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 4bcfb071-b3ae-48cc-8ea5-7e7434732287
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 11aaad4935681d8b3d338779eec1b19d77cb11e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a>Bir Azure işlevi uygulama ve Azure depolama hesabı oluştur
[Azure işlevleri](../../articles/azure-functions/functions-overview.md) kolayca çalıştırmak için bir çözüm *işlevleri* (küçük kod parçalarını) hello bulutta. Azure'da işlevlerinizin yürütülmesini hello Azure işlev uygulaması barındırır.

## <a name="what-will-you-do"></a>Ne
Bir Azure Resource Manager şablonu toocreate bir Azure işlevi uygulama ve bir Azure depolama hesabı kullanın. Hello Azure işlev uygulaması tooAzure IOT hub olayları dinler, gelen iletileri işleme ve tooAzure Table storage yazar. Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-will-you-learn"></a>Ne size bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:
* Nasıl toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure kaynakları.
* Nasıl toouse Azure app tooprocess IOT hub iletileri işlev ve bunları Azure Table storage ' tooa tablo yazar.

## <a name="what-do-you-need"></a>Ne ihtiyacınız var
* Başarılı bir şekilde tamamladınız gerekir:
- [Raspberry Pi 3 ile çalışmaya başlama](iot-hub-raspberry-pi-kit-c-get-started.md)
- [Azure IOT hub'ınızı oluşturma](iot-hub-raspberry-pi-kit-c-get-started.md)

## <a name="open-hello-sample-app"></a>Açık hello örnek uygulaması
Merhaba aşağıdaki komutları çalıştırarak örnek proje Visual Studio Code açık hello:

```bash
cd Lesson3
code .
```

![Depodaki yapısı](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure_c.png)

* Merhaba `main.c` hello dosyasında `app` alt dosyasıdır hello anahtarı kaynağı. Bu kaynak dosya hello kod toosend gönderir 20 kez tooyour IOT hub ve blink hello LED her ileti için ileti içerir.
* Merhaba `arm-template.json` bir Azure işlevi uygulama ve Azure storage hesabı içeren hello Azure Resource Manager şablonu bir dosyadır.
* Merhaba `arm-template-param.json` hello Azure Resource Manager şablonu tarafından kullanılan hello yapılandırma dosyası bir dosyadır.
* Merhaba `ReceiveDeviceMessages` alt hello Azure işlevi için hello Node.js kodunu içerir.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Azure Resource Manager şablonları yapılandırmak ve kaynakları oluşturma
Güncelleştirme hello `arm-template-param.json` Visual Studio Code dosyasında.

![Azure Resource Manager şablonu parametreleri](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para_c.png)

* Değiştir **[IOT Hub adınız]** ile **{hub adımın}** ne zaman belirtilen, [IOT hub'ınızı oluşturulur ve Raspberry Pi 3 kayıtlı](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).
* Değiştir **[önek dizesi yeni kaynaklar için]** istediğiniz tüm ön ekine sahip. Merhaba önek bu hello kaynak adı genel olarak benzersiz tooavoid çakışma sağlar. Bir çizgi ya da rakamla hello önekini ilk kullanmayın.

Merhaba güncelleştirdikten sonra `arm-template-param.json` dosya, komutu aşağıdaki hello çalıştırarak hello kaynakları tooAzure dağıtma:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

Bu kaynakları toocreate yaklaşık beş dakika sürer. Merhaba kaynak oluşturma işlemi devam ederken, toohello sonraki makalede taşıyabilirsiniz.

## <a name="summary"></a>Özet
IOT hub iletileri Azure işlevi uygulama tooprocess oluşturduğunuz ve bir Azure depolama hesabı toostore bu iletiler. Şimdi, dağıtın ve hello örnek toosend cihaz bulut iletilerini Pi üzerinde çalıştırın.

## <a name="next-steps"></a>Sonraki adımlar
[Örnek uygulama toosend cihaz bulut iletilerini çalıştırın](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md)

