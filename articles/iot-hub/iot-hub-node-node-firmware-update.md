---
title: "Azure IOT hub'ı (düğüm) aaaDevice ürün yazılımı güncelleştirmesini | Microsoft Docs"
description: "Azure IOT Hub tooinitiate cihaz üretici yazılımı toouse cihaz yönetimini nasıl güncelleştirin. Sanal cihaz uygulaması ve hello bellenim güncelleştirme tetikleyen bir hizmet uygulaması hello Azure IOT SDK'ları için Node.js tooimplement kullanın."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/06/2017
ms.author: juanpere
ms.openlocfilehash: 99d4b369e7aba334bf713e0c657e6e5d227fb691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-nodenode"></a>Aygıt Yönetimi tooinitiate aygıt üretici yazılımı güncelleştirmesi (düğümü/düğümü) kullanın
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a>Giriş
Merhaba, [aygıt Management'i kullanmaya başlama] [ lnk-dm-getstarted] öğretici, gördüğünüz nasıl toouse hello [cihaz çifti] [ lnk-devtwin] ve [doğrudan yöntemleri] [ lnk-c2dmethod] temelleri tooremotely bir aygıtı yeniden başlatın. Bu öğretici kullanır aynı IOT hub'ı temelleri hello ve rehberlik sağlar ve nasıl toodo bir uçtan uca bellenim güncelleştirme benzetimli gösterir.  Bu desen hello bellenim güncelleştirme uygulamasında hello Intel Edison'u aygıt örnek için kullanılır.

Bu öğretici şunların nasıl yapıldığını gösterir:

* IOT hub'ınız aracılığıyla hello sanal cihaz uygulamasında hello firmwareUpdate doğrudan yöntemini çağıran bir Node.js konsol uygulaması oluşturun.
* Arabirimini uygulayan bir sanal cihaz uygulaması oluşturma bir **firmwareUpdate** doğrudan yöntemi. Bu yöntem, toodownload hello bellenim görüntü bekler, hello bellenim görüntüyü indirir ve son olarak hello bellenim görüntü geçerlidir bir çok aşama işlemi başlatır. Merhaba güncelleştirme her aşaması sırasında hello aygıt kullanır hello ilerlemeyi özellikleri tooreport bildirdi.

Bu öğreticinin Hello sonunda, iki Node.js konsol uygulamaları vardır:

**dmpatterns_fwupdate_service.js**hello sanal cihaz uygulamada, doğrudan bir yöntem çağıran görüntüler hello yanıt ve düzenli aralıklarla (her 500ms) güncelleştirilmiş görüntüler hello bildirilen özellikleri.

**dmpatterns_fwupdate_device.js**, daha önce oluşturduğunuz hello cihaz kimliğiyle IOT hub'ı tooyour bağlayan firmwareUpdate doğrudan bir yöntem alır, bellenim güncelleştirme dahil çok durumlu işlem toosimulate çalıştırır: Merhaba bekleniyor Görüntü, hello yeni görüntüsünü indirerek ve son olarak hello görüntüyü uygulamadan'i yükleyin.

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Node.js sürümünü 0.12.x sürümü veya sonraki bir sürümü <br/>  [Geliştirme ortamınızı hazırlama] [ lnk-dev-setup] açıklar nasıl tooinstall Node.js Bu öğretici için Windows veya Linux üzerinde.
* Etkin bir Azure hesabı. (Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)

Merhaba izleyin [aygıt Management'i kullanmaya başlama](iot-hub-node-node-device-management-get-started.md) toocreate IOT hub'ınızı makalesi ve IOT Hub bağlantı dizenizi alın.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a>Merhaba cihaz doğrudan bir yöntem kullanarak bir uzak bellenim güncelleştirme Tetikle
Bu bölümde, bir cihazda uzaktan bellenim güncelleştirme başlatan bir Node.js konsol uygulaması oluşturun. doğrudan yöntemi tooinitiate hello güncelleştirmesi Hello uygulamanın kullandığı ve kullandığı cihaz çifti sorguları tooperiodically hello hello etkin bellenim güncelleştirme durumunu alın.

1. Adlı bir boş klasör oluşturun **triggerfwupdateondevice**.  Merhaba, **triggerfwupdateondevice** klasörü, komut, komut isteminde aşağıdaki hello kullanarak bir package.json dosyası oluşturun.  Tüm hello Varsayılanları kabul edin:
   
    ```
    npm init
    ```
2. Merhaba, komut isteminde **triggerfwupdateondevice** klasörüne, komut tooinstall hello aşağıdaki hello **azure IOT hub** ve **azure-IOT-cihaz-mqtt** aygıt SDK paketler:
   
    ```
    npm install azure-iothub --save
    ```
3. Bir metin düzenleyicisi kullanarak oluşturduğunuz bir **dmpatterns_getstarted_service.js** hello dosyasında **triggerfwupdateondevice** klasör.
4. Merhaba aşağıdaki 'İste' hello hello başlangıç deyimleri ekleme **dmpatterns_getstarted_service.js** dosyası:
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. Değişken bildirimleri aşağıdaki hello ekleyin ve hello yer tutucu değerlerini değiştirin:
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. Merhaba aşağıdaki toofind işlev ve hello firmwareUpdate hello değerini görüntülemek ekleme özelliği bildirdi.
   
    ```
    var queryTwinFWUpdateReported = function() {
        registry.getTwin(deviceToUpdate, function(err, twin){
            if (err) {
              console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
            } else {
              console.log((JSON.stringify(twin.properties.reported.iothubDM.firmwareUpdate)) + "\n");
            }
        });
    };
    ```
7. İşlev tooinvoke hello firmwareUpdate yöntemi tooreboot hello hedef aygıt aşağıdaki hello ekleyin:
   
    ```
    var startFirmwareUpdateDevice = function() {
      var params = {
          fwPackageUri: 'https://secureurl'
      };
   
      var methodName = "firmwareUpdate";
      var payloadData =  JSON.stringify(params);
   
      var methodParams = {
        methodName: methodName,
        payload: payloadData,
        timeoutInSeconds: 30
      };
   
      client.invokeDeviceMethod(deviceToUpdate, methodParams, function(err, result) {
        if (err) {
          console.error('Could not start hello firmware update on hello device: ' + err.message)
        } 
      });
    };
    ```
8. Son olarak, Ekle hello aşağıdaki işlev toocode toostart hello bellenim güncelleştirme sırası ve düzenli aralıklarla gösteren Başlat hello bildirilen özellikleri:
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. Kaydet ve Kapat hello **dmpatterns_fwupdate_service.js** dosya.

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a>Merhaba uygulamaları çalıştırma
Hazır toorun hello uygulamaları sunulmuştur.

1. Merhaba hello komut isteminde **manageddevice** klasöründe şunu hello yeniden başlatma doğrudan yöntemi için dinleme komutu toobegin aşağıdaki hello çalıştırın.
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. Merhaba hello komut isteminde **triggerfwupdateondevice** komutu tootrigger hello uzaktan aşağıdaki hello Çalıştır klasörü yeniden başlatın ve hello cihaz çifti toofind hello en son yeniden başlatma için zaman sorgu.
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. Merhaba aygıt yanıt toohello doğrudan yöntemi hello konsolunda bakın.

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide kullandığınız doğrudan yöntemi tootrigger uzak bir cihaz ve kullanılan hello bellenim güncelleştirme özellikleri toofollow hello hello bellenim güncelleştirme ilerlemesini bildirdi.

toolearn tooextend birden fazla cihazda IOT çözümü ve zamanlama yöntemi çağırır nasıl hello bkz [zamanlama ve yayın işleri] [ lnk-tutorial-jobs] Öğreticisi.

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
