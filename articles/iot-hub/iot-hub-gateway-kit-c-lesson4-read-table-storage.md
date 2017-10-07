---
title: "SensorTag cihaz & Azure IOT ağ geçidi - Ders 4: Tablo depolama | Microsoft Docs"
description: "Intel NUC tooyour IOT hub'ından iletileri kaydetmek için tooAzure tablo depolama yazma ve bunları hello buluttan okuyun."
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
ms.openlocfilehash: 29525b084eb4d6e6dfcb16d9b34f78f075d30b7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a>İletileri okuma Azure tablo Depolama'da kalıcı

## <a name="what-you-will-do"></a>Ne yapacağını

- Merhaba ağ geçidi örnek uygulaması tooyour IOT hub'ı iletileri gönderir, ağ geçidi üzerinde çalıştırın.
- Ardından örnek kod, Azure Table depolama ana bilgisayar tooread hello ileti çalıştırın. 

Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz

Nasıl toouse hello aracı toorun hello örnek kodu tooread iletilerinde Azure Table depolama alanınızın gulp.

## <a name="what-you-need"></a>Ne gerekiyor

Başarıyla sahip görevlerin ardından hello:

- [Oluşturulan Hello Azure işlev uygulaması ve hello Azure depolama hesabı](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md).
- [Merhaba ağ geçidi örnek uygulamayı çalıştırın](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md).
- [IOT hub'ından iletileri okumak](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md).

## <a name="get-your-azure-storage-connection-strings"></a>Azure depolama bağlantı dizelerinizi Al

Bu ders erken bir Azure depolama hesabı başarıyla oluşturuldu. tooget hello bağlantı dizesi hello Azure depolama hesabı, hello aşağıdaki komutları çalıştırın:

* Tüm depolama hesaplarının listesi.

```bash
az storage account list -g iot-gateway --query [].name
```

* Azure depolama bağlantı dizesi alın.

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

IOT ağ geçidi hello değeri olarak kullanın `{resource group name}` Ders 2 hello değerinde değiştirilmediyse.

## <a name="configure-hello-device-connection"></a>Merhaba aygıt bağlantısını yapılandırın

Güncelleştirme hello `config-azure.json` hello ana bilgisayarda çalışan hello örnek kod, Azure Table depolama iletisinde okuyabilmeniz için dosya. tooconfigure Merhaba cihaz bağlantısı, şu adımları izleyin:

1. Açık hello aygıt yapılandırma dosyası `config-azure.json` hello aşağıdaki komutları çalıştırarak:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![yapılandırma](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. Değiştir `[Azure storage connection string]` hello aldığınız Azure depolama bağlantı dizesi ile.

   `[IoT hub connection string]`bölümünde değiştirilmesi gereken [Azure IOT Hub'ından iletileri okumak](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) Lesson3 içinde.

## <a name="read-messages-in-your-azure-table-storage"></a>Azure Table depolama alanınızın iletileri

Merhaba ağ geçidi örnek uygulamayı çalıştırın ve Azure Table depolama iletileri komutu aşağıdaki hello tarafından okuyun:

```bash
gulp run --table-storage
```

Yeni ileti geldiğinde IOT hub'ınızı Azure işlevi uygulama toosave iletinizi Azure Table depolama alanına tetikler.
Merhaba `gulp run` komutu tooyour IOT hub'ı iletileri gönderir ağ geçidi örnek uygulamayı çalıştırır. İle `table-storage` parametresi, bu da olarak çoğaltılır ileti Azure Table storage ' kayıtlı bir alt işlem tooreceive hello.

gönderilen ve alınan tüm hizmetlerde Anında hello aynı konsol penceresinde hello iletileri ana makine hello. Merhaba örnek uygulama örneği 40 saniye içinde otomatik olarak sona erdirir.

   ![gulp okuma](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table.png)


## <a name="summary"></a>Özet

Azure işlevi uygulamanız tarafından kaydedilen, Azure Table depolama hello örnek kodu tooread karışılama iletileri çalıştırdıysanız.
