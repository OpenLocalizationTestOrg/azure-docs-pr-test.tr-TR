---
title: "Azure IOT - Ders 3 Connect Raspberry pi (C): şablon dağıtımı | Microsoft Docs"
description: "Azure işlev uygulaması Azure IOT hub olayları dinler, gelen iletileri işler ve bunları Azure Table depolama alanına yazar."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: bulutta depolanan veriler bulutta veri depolama IOT bulut hizmeti
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
ms.openlocfilehash: b8bab31489f2e912b51212cb58cb598a9db9b59d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a>Bir Azure işlevi uygulama ve Azure depolama hesabı oluştur
[Azure işlevleri](../../articles/azure-functions/functions-overview.md) kolayca çalıştırmak için bir çözüm *işlevleri* (küçük kod parçalarını) bulutta. Azure'da işlevlerinizin yürütülmesini bir Azure işlev uygulaması barındırır.

## <a name="what-will-you-do"></a>Ne
Bir Azure işlevi uygulama ve Azure storage hesabı oluşturmak için bir Azure Resource Manager şablonunu kullanın. Azure işlev uygulaması Azure IOT hub olayları dinler, gelen iletileri işler ve bunları Azure Table depolama alanına yazar. Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-will-you-learn"></a>Ne size bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:
* Nasıl kullanılacağını [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) Azure kaynaklarınızı dağıtmak için.
* IOT hub iletileri işlemek ve bunları Azure Table depolama tabloda yazmak için bir Azure işlev uygulaması kullanma

## <a name="what-do-you-need"></a>Ne ihtiyacınız var
* Başarılı bir şekilde tamamladınız gerekir:
- [Raspberry Pi 3 ile çalışmaya başlama](iot-hub-raspberry-pi-kit-c-get-started.md)
- [Azure IOT hub'ınızı oluşturma](iot-hub-raspberry-pi-kit-c-get-started.md)

## <a name="open-the-sample-app"></a>Örnek uygulamayı açın
Örnek Proje aşağıdaki komutları çalıştırarak Visual Studio kodda açın:

```bash
cd Lesson3
code .
```

![Depodaki yapısı](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure_c.png)

* `main.c` Dosyasını `app` alt anahtarı kaynağı dosyasıdır. Bu kaynak dosyası 20 kez IOT hub'ınıza ileti gönderme ve LED, gönderdiği her ileti için blink kodunu içerir.
* `arm-template.json` Bir Azure işlevi uygulama ve Azure storage hesabı içeren Azure Resource Manager şablonu bir dosyadır.
* `arm-template-param.json` Azure Resource Manager şablonu tarafından kullanılan yapılandırma dosyasını bir dosyadır.
* `ReceiveDeviceMessages` Alt Azure işlevi için Node.js kodunu içerir.

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>Azure Resource Manager şablonları yapılandırmak ve kaynakları oluşturma
Güncelleştirme `arm-template-param.json` Visual Studio Code dosyasında.

![Azure Resource Manager şablonu parametreleri](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para_c.png)

* Değiştir **[IOT Hub adınız]** ile **{hub adımın}** ne zaman belirtilen, [IOT hub'ınızı oluşturulur ve Raspberry Pi 3 kayıtlı](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).
* Değiştir **[önek dizesi yeni kaynaklar için]** istediğiniz tüm ön ekine sahip. Önek, kaynak adı çakışmayı önlemek için genel benzersiz olmasını sağlar. Bir çizgi ya da rakamla önekini ilk kullanmayın.

Güncelleştirdikten sonra `arm-template-param.json` dosya, aşağıdaki komutu çalıştırarak kaynakları Azure'a dağıtma:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

Bu kaynakları oluşturmak için yaklaşık beş dakika sürer. Kaynak oluşturma işlemi devam ederken, sonraki makalede hareket ettirebilirsiniz.

## <a name="summary"></a>Özet
IOT hub iletileri ve Azure storage hesabı bu iletileri depolamak için işlemek için Azure işlevi uygulamanızı oluşturdunuz. Şimdi, dağıtın ve üzerinde Pi cihaz bulut iletilerini göndermek için örnek çalıştırın.

## <a name="next-steps"></a>Sonraki adımlar
[Cihaz bulut iletilerini göndermek için bir örnek uygulamayı çalıştırın](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md)

