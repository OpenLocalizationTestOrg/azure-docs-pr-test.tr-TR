---
title: "Raspberry Pi'yi (düğüm) tooAzure IOT - Ders 3 bağlanın: şablon dağıtımı | Microsoft Docs"
description: "Hello Azure işlev uygulaması tooAzure IOT hub olayları dinler, gelen iletileri işleme ve tooAzure Table storage yazar."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Merhaba bulutta, bulutta depolanan veriler veri depolama IOT bulut hizmeti
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6c58de85-c5c4-4989-bb5e-08c45c549966
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b6c0a9530cb80e3f78c0e96037f6f3942b602aea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a>Bir Azure işlevi uygulama ve Azure depolama hesabı oluştur
[Azure işlevleri](../azure-functions/functions-overview.md) kolayca çalıştırmak için bir çözüm *işlevleri* (küçük kod parçalarını) hello bulutta. Azure'da işlevlerinizin yürütülmesini hello Azure işlev uygulaması barındırır.

## <a name="what-you-will-do"></a>Ne yapacağını
Bir Azure Resource Manager şablonu toocreate bir Azure işlevi uygulama ve bir Azure depolama hesabı kullanın. Hello Azure işlev uygulaması tooAzure IOT hub olayları dinler, gelen iletileri işleme ve tooAzure Table storage yazar. Herhangi bir sorun varsa, hello çözümlerini arama [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:

* Nasıl toouse [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) toodeploy Azure kaynakları.
* Nasıl toouse Azure app tooprocess IOT hub iletileri işlev ve bunları Azure Table storage ' tooa tablo yazar.

## <a name="what-you-need"></a>Ne gerekiyor
Başarılı bir şekilde tamamladınız gerekir:
* [Raspberry Pi 3 ile çalışmaya başlama](iot-hub-raspberry-pi-kit-node-get-started.md)
* [Azure IOT hub'ınızı oluşturma](iot-hub-raspberry-pi-kit-node-get-started.md)

## <a name="open-hello-sample-app"></a>Açık hello örnek uygulaması
Merhaba aşağıdaki komutları çalıştırarak örnek proje Visual Studio Code açık hello:

```bash
cd Lesson3
code .
```

![Depodaki yapısı](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure.png)

* Merhaba `app.js` hello dosyasında `app` alt dosyasıdır hello anahtarı kaynağı. Bu kaynak dosya hello kod toosend gönderir 20 kez tooyour IOT hub ve blink hello LED her ileti için ileti içerir.
* Merhaba `arm-template.json` bir Azure işlevi uygulama ve Azure storage hesabı içeren hello Azure Resource Manager şablonu bir dosyadır.
* Merhaba `arm-template-param.json` hello Azure Resource Manager şablonu tarafından kullanılan hello yapılandırma dosyası bir dosyadır.
* Merhaba `ReceiveDeviceMessages` alt hello Azure işlevi için hello Node.js kodunu içerir.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Azure Resource Manager şablonları yapılandırmak ve kaynakları oluşturma
Güncelleştirme hello `arm-template-param.json` Visual Studio Code dosyasında.

![Azure Resource Manager şablonu parametreleri](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para.png)

* Değiştir **[IOT Hub adınız]** ile **{hub adımın}** ne zaman belirtilen, [IOT hub'ınızı oluşturulur ve Raspberry Pi 3 kayıtlı](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).
* Değiştir **[önek dizesi yeni kaynaklar için]** istediğiniz tüm ön ekine sahip. Merhaba önek bu hello kaynak adı genel olarak benzersiz tooavoid çakışma sağlar. Bir çizgi ya da rakamla hello önekini ilk kullanmayın.

Merhaba güncelleştirdikten sonra `arm-template-param.json` dosya, komutu aşağıdaki hello çalıştırarak hello kaynakları tooAzure dağıtma:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

Bu kaynakları toocreate yaklaşık beş dakika sürer. Merhaba kaynak oluşturma işlemi devam ederken, toohello sonraki makalede taşıyabilirsiniz.

## <a name="summary"></a>Özet
IOT hub iletileri Azure işlevi uygulama tooprocess oluşturduğunuz ve bir Azure depolama hesabı toostore bu iletiler. Şimdi, dağıtın ve hello örnek toosend cihaz bulut iletilerini Pi üzerinde çalıştırın.

## <a name="next-steps"></a>Sonraki adımlar
[Örnek uygulama toosend cihaz bulut iletilerini Raspberry Pi 3'te çalıştırın.](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md)

