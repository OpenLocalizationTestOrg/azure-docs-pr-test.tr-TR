---
title: "aaaUse IOT ağ geçidi tooconnect aygıt tooAzure IOT hub'ı | Microsoft Docs"
description: "Toouse IOT ağ geçidi tooconnect tı SensorTag olarak Intel NUC ve gönderme algılayıcı verileri tooAzure IOT hub'ı hello nasıl bulut öğrenin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IOT ağ geçidi aygıtı toocloud Bağlan"
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 418af34bf29992d46b76ae59ef548744808664c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-tooconnect-things-toohello-cloud---sensortag-tooazure-iot-hub"></a>IOT ağ geçidi tooconnect şeyler toohello bulut - SensorTag tooAzure IOT hub'ı kullanın

> [!NOTE]
> Bu öğretici başlamadan önce tamamlandı emin olun [Intel NUC IOT ağ geçidi olarak ayarlama](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md). İçinde [Intel NUC IOT ağ geçidi olarak ayarlamak](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), hello Intel NUC cihazı IOT ağ geçidi olarak ayarlayın.

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz

Hakkında bilgi edineceksiniz nasıl toouse IOT ağ geçidi tooconnect Texas Instruments SensorTag (CC2650STK) tooAzure IOT hub'ı. Merhaba IOT ağ geçidi sıcaklık gönderir ve hello SensorTag tooAzure IOT hub'ı toplanan nem veriler.

## <a name="what-you-will-do"></a>Ne yapacağını

- IOT hub'ı oluşturun.
- Merhaba IOT hub'hello SensorTag için bir cihaz kaydetme.
- Merhaba IOT ağ geçidi hello SensorTag arasında Hello bağlantı etkinleştirin.
- Bir bırak örnek uygulama toosend SensorTag veri tooyour IOT hub'ı çalıştırın.

## <a name="what-you-need"></a>Ne gerekiyor

- Öğretici [Intel NUC IOT ağ geçidi olarak ayarlama](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) tamamlandı, Intel NUC IOT ağ geçidi olarak ayarlamanız içinde.
- * Etkin bir Azure aboneliği. Bir Azure hesabınız yoksa [ücretsiz Azure deneme hesabı oluşturma](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.
- Ana bilgisayar üzerinde çalışan bir SSH istemcisi. Putty'yi Windows önerilir. Linux ve macOS zaten bir SSH istemcisi ile gelir.
- Başlangıç IP adresi ve hello kullanıcı adı ve parola tooaccess hello ağ geçidi'nden hello SSH istemcisi.
- Bir Internet bağlantısı.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> Burada, SensorTag için bu yeni cihaz kaydedilir

## <a name="enable-hello-connection-between-hello-iot-gateway-and-hello-sensortag"></a>Merhaba IOT ağ geçidi hello SensorTag arasındaki Hello bağlantıyı etkinleştir

Bu bölümde, hello aşağıdaki görevleri gerçekleştirin:

- Bluetooth bağlantısı için hello SensorTag Hello MAC adresini alın.
- Merhaba IOT ağ geçidi toohello SensorTag bir Bluetooth bağlantısını başlatma.

### <a name="get-hello-mac-address-of-hello-sensortag-for-bluetooth-connection"></a>Merhaba SensorTag Hello MAC adresi için Bluetooth bağlantısını Al

1. Merhaba ana bilgisayarda hello SSH istemcisi çalıştırın ve toohello IOT ağ geçidi bağlanın.
1. Bluetooth hello aşağıdaki komutu çalıştırarak Engellemeyi Kaldır:

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. Merhaba IOT ağ geçidi'nde Hello Bluetooth hizmetini başlatın ve aşağıdaki komutları çalıştırarak Bluetooth hello Bluetooth Kabuk tooconfigure girin:

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. Güç çalıştırarak hello Bluetooth denetleyicisinde hello hello Bluetooth Kabuk komut aşağıdaki:

   ```bash
   power on
   ```

   ![Merhaba IOT bluetoothctl ağ geçidiyle hello Bluetooth denetleyicide güç](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. Yakındaki Bluetooth aygıtlar hello aşağıdaki komutu çalıştırarak Taramayı Başlat:

   ```bash
   scan on
   ```

   ![Bluetoothctl ile Bluetooth cihazları yakındaki tarama](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. Merhaba SensorTag düğmesinde eşleştirme hello tuşuna basın. Merhaba yeşil hello SensorTag yanıp sönen üzerinde GEREKTİRİYORDU.
1. Merhaba Bluetooth Kabuk SensorTag bulunan hello görmeniz gerekir. Merhaba hello SensorTag MAC adresini not edin. Bu örnekte, hello hello SensorTag MAC adresi olan `24:71:89:C0:7F:82`.
1. Merhaba aşağıdaki komutu çalıştırarak Hello tarama devre dışı bırakın:

   ```bash
   scan off
   ```

   ![Bluetoothctl ile Bluetooth cihazları yakındaki Taramayı Durdur](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-hello-iot-gateway-toohello-sensortag"></a>Merhaba IOT ağ geçidi toohello SensorTag bir Bluetooth bağlantısını başlatma

1. Toohello SensorTag hello aşağıdaki komutu çalıştırarak Bağlan:

   ```bash
   connect <MAC address>
   ```

   ![Toohello SensorTag bluetoothctl ile bağlanma](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. Merhaba SensorTag çıkarın ve hello aşağıdaki komutları çalıştırarak hello Bluetooth kabuktan çıkış:

   ```bash
   disconnect
   exit
   ```

   ![Merhaba SensorTag bluetoothctl ile bağlantısını kesin](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

Merhaba SensorTag hello IOT ağ geçidi arasında hello bağlantısı başarıyla etkinleştirdikten.

## <a name="run-a-ble-sample-application-toosend-sensortag-data-tooyour-iot-hub"></a>Bir bırak örnek uygulama toosend SensorTag veri tooyour IOT hub çalıştırın

Merhaba Bluetooth düşük enerji (bırak) örnek uygulaması, Azure IOT kenar tarafından sağlanır. Merhaba örnek uygulaması bırak bağlantısından veri toplar ve hello veri tooyou IOT hub'ı gönderin. toorun Merhaba örnek uygulaması, şunları yapmanız gerekir:

1. Merhaba örnek uygulaması yapılandırın.
1. Merhaba IOT ağ geçidi'nde Hello örnek uygulamayı çalıştırın.

### <a name="configure-hello-sample-application"></a>Merhaba örnek uygulamayı yapılandırma

1. Merhaba aşağıdaki komutu çalıştırarak Merhaba örnek uygulaması toohello klasörüne gidin:

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. Merhaba aşağıdaki komutu çalıştırarak Hello yapılandırma dosyasını açın:

   ```bash
   vi ble_gateway.json
   ```

1. Merhaba yapılandırma dosyasında aşağıdaki değerleri hello doldurun:

   **IoTHubName**: IOT hub'ınızı hello adı.

   **IoTHubSuffix**: Get IoTHubSuffix aşağı not ettiğiniz hello birincil anahtarı hello cihaz bağlantı dizesi. Merhaba birincil anahtarı hello cihaz bağlantı dizesi alma, IOT hub bağlantı dizenizi birincil anahtarı hello değil emin olun. Merhaba birincil hello cihaz bağlantı dizesi anahtarıdır hello biçiminde `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.

   **Aktarım**: hello varsayılan değer `amqp`. Bu değer hello protokolü sırasında transpotation gösterir. Olabilir `http`, `amqp`, veya `mqtt`.

   **macAddress**: hello aşağı ettiğiniz SensorTag MAC adresini hello.

   **DeviceID**: IOT hub'ınıza oluşturulan hello aygıtın kimliği.

   **deviceKey**: hello birincil anahtar hello cihaz bağlantı dizesi.

   ![Merhaba bırak örnek uygulaması, tam hello yapılandırma dosyası](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. Tuşuna `ESC` ve türü `:wq` toosave hello dosya.

### <a name="run-hello-sample-application"></a>Merhaba örnek uygulamayı çalıştırın

1. SensorTag açık olduğundan emin hello olun.
1. Merhaba aşağıdaki komutu çalıştırın:

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a>Sonraki adımlar

[Azure IOT kenarıyla algılayıcı veri dönüştürme için IOT ağ geçidi kullan](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
