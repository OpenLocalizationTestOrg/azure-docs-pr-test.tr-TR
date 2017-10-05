---
title: "SensorTag cihaz & Azure IOT ağ geçidi - Ders 4: Tablo depolama | Microsoft Docs"
description: "IOT hub'ınıza Intel NUC iletileri kaydetmek için bunları Azure Table depolama alanına yazmak ve bunları buluttan okuyun."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: verileri buluttan, IOT bulut hizmeti
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 8ca78045-ad92-4a6a-90f1-05f9668e6f0e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 72659ef3a7fd2f6011590d37176fd05503269aff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a>İletileri okuma Azure tablo Depolama'da kalıcı

## <a name="what-you-will-do"></a>Ne yapacağını

- IOT hub'ına iletileri gönderir, ağ geçidi üzerinde ağ geçidi örnek uygulamayı çalıştırın.
- Daha sonra ana bilgisayarınızda Azure Table depolama alanınızın iletileri okumak için örnek kod çalıştırın. 

Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz

Gulp aracı, Azure Table depolama iletileri okumak için örnek kod çalıştırmak için nasıl kullanılır.

## <a name="what-you-need"></a>Ne gerekiyor

Başarıyla sahip aşağıdaki görevleri yapılır:

- [Oluşturulan Azure işlev uygulaması ve Azure depolama hesabı](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md).
- [Ağ geçidi örnek uygulamayı çalıştırın](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md).
- [IOT hub'ından iletileri okumak](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md).

## <a name="get-your-azure-storage-connection-strings"></a>Azure depolama bağlantı dizelerinizi Al

Bu ders erken bir Azure depolama hesabı başarıyla oluşturuldu. Azure depolama hesabı bağlantı dizesini almak için aşağıdaki komutları çalıştırın:

* Tüm depolama hesaplarının listesi.

```bash
az storage account list -g iot-gateway --query [].name
```

* Azure depolama bağlantı dizesi alın.

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

IOT ağ geçidi değeri olarak kullanın `{resource group name}` Ders 2 değerinde değiştirilmediyse.

## <a name="configure-the-device-connection"></a>Aygıt bağlantısını yapılandırın

Güncelleştirme `config-azure.json` ana bilgisayarda çalışan örnek kod, Azure Table depolama iletisinde okuyabilmeniz için dosya. Aygıt bağlantısını yapılandırmak için aşağıdaki adımları izleyin:

1. Aygıt yapılandırma dosyasını açın `config-azure.json` aşağıdaki komutları çalıştırarak:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![yapılandırma](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. Değiştir `[Azure storage connection string]` aldığınız Azure depolama bağlantı dizesi ile.

   `[IoT hub connection string]`bölümünde değiştirilmesi gereken [Azure IOT Hub'ından iletileri okumak](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) Lesson3 içinde.

## <a name="read-messages-in-your-azure-table-storage"></a>Azure Table depolama alanınızın iletileri

Ağ geçidi örnek uygulamayı çalıştırın ve aşağıdaki komutu tarafından Azure Table depolama iletilerini okuyun:

```bash
gulp run --table-storage
```

IOT hub'ınıza ileti yeni ileti geldiğinde, Azure Table depolama alanına kaydetmek için Azure işlevi uygulamanızı tetikler.
`gulp run` Komutu IOT hub'ına iletileri gönderen ağ geçidi örnek uygulamayı çalıştırır. İle `table-storage` parametresi, bu da olarak çoğaltılır, Azure Table storage ' kaydedilmiş ileti almak için bir alt işlem.

Gönderilen ve alınan tüm iletileri anında üzerinde aynı ana bilgisayar makinesi konsol penceresinde görüntülenir. Örnek uygulama örneği 40 saniye içinde otomatik olarak sona erdirir.

   ![gulp okuma](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table.png)


## <a name="summary"></a>Özet

Azure işlevi uygulamanız tarafından kaydedilen, Azure Table depolama iletileri okumak için örnek kod çalıştırdıysanız.