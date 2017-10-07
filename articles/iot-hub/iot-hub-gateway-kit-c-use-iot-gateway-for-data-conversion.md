---
title: "Azure IOT kenarıyla IOT ağ geçidi aaaData dönüştürme | Microsoft Docs"
description: "Azure IOT kenarından özelleştirilmiş bir modül üzerinden algılayıcı veri IOT ağ geçidi tooconvert hello biçimini kullanın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IOT ağ geçidi veri dönüştürme, IOT ağ geçidi veri dönüştürme"
ms.assetid: 75f2573d-500b-4405-bff7-61021c4c3500
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: ae94b1f96f36dfcb4f77fadc0ece3cff3d0bba91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-edge"></a>Azure IOT kenarıyla algılayıcı veri dönüştürme için IOT ağ geçidi kullan

> [!NOTE]
> Bu öğretici başlamadan önce sırayla dersleri aşağıdaki tamamlanmış hello olduğunuz emin olun:
> * [Intel NUC cihazını IoT ağ geçidi olarak ayarlama](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
> * [IOT ağ geçidi tooconnect şeyler toohello bulut - SensorTag tooAzure IOT hub'ı kullanın](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

Tek bir IOT ağ geçidinin amacı, toplanan tooprocess toohello bulut göndermeden önce verilerdir. Azure IOT kenar oluşturulan ve birleştirilmiş tooform hello veri işleme iş akışı olabilen modülleri tanıtır. Bir modül bir ileti alır, üzerinde bazı eylemleri gerçekleştirir ve sonra taşıyın diğer modüller tooprocess için.

## <a name="what-you-learn"></a>Öğrenecekleriniz

Nasıl toocreate modülü tooconvert hello SensorTag farklı bir biçime gelen iletileri öğrenin.

## <a name="what-you-do"></a>Neler

* Bir modül tooconvert hello .json biçimine alınan bir ileti oluşturun.
* Merhaba modülü derleyin.
* Merhaba modülü toohello bırak örnek uygulaması, Azure IOT kenarından ekleyin.
* Merhaba örnek uygulamayı çalıştırın.

## <a name="what-you-need"></a>Ne gerekiyor

* aşağıdaki sırayla tamamlandı öğreticileri hello:
  * [Intel NUC cihazını IoT ağ geçidi olarak ayarlama](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
  * [IOT ağ geçidi tooconnect şeyler toohello bulut - SensorTag tooAzure IOT hub'ı kullanın](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
* Ana bilgisayar üzerinde çalışan bir SSH istemcisi. Putty'yi Windows önerilir. Linux ve macOS zaten bir SSH istemcisi ile gelir.
* Başlangıç IP adresi ve hello kullanıcı adı ve parola tooaccess hello ağ geçidi'nden hello SSH istemcisi.
* Bir Internet bağlantısı.

## <a name="create-a-module"></a>Bir modül oluşturma

1. Merhaba ana bilgisayarda hello SSH istemcisi çalıştırın ve toohello IOT ağ geçidi bağlanın.
1. Hello aşağıdaki komutları çalıştırarak hello dönüştürme GitHub toohello giriş dizinine hello IOT ağ geçidi modülünden Hello kaynak dosyalarını kopyalayın:

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   Merhaba C programlama dili yazılmış yerel bir Azure kenar modül budur. Merhaba modülü bir aşağıdaki hello alınan iletilerin hello biçime dönüştürür:

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-hello-module"></a>Merhaba modülü derleme

toocompile hello modülü, hello aşağıdaki komutları çalıştırın:

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module/my_module
# change hello build script runnable
chmod 777 build.sh
# remove hello invalid windows character
sed -i -e "s/\r$//" build.sh
# run hello build shell script
./build.sh
```

Size bir `libmy_module.so` hello derleme tamamlandıktan sonra dosya. Bu dosyanın hello mutlak yolu not edin.

## <a name="add-hello-module-toohello-ble-sample-application"></a>Merhaba modülü toohello bırak örnek uygulaması ekleyin

1. Hello aşağıdaki komutu çalıştırarak toohello örnekleri klasöre gidin:

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. Merhaba aşağıdaki komutu çalıştırarak Hello yapılandırma dosyasını açın:

   ```bash
   vi ble_gateway.json
   ```

1. Aşağıdaki kod toohello hello ekleyerek bir modül ekleyin `modules` bölümü.

   ```json
   {
       "name": "MyModule",
       "loader": {
           "name": "native",
           "entrypoint":{
               "module.path": "[Your libmy_module.so path]"
               }
            },
        "args": null
    },
    ```

1. Değiştir `[Your libmy_module.so path]` hello libmy_module.so hello mutlak yolu ile Merhaba kodda ' dosyası.
1. Merhaba Hello kodla `links` bir aşağıdaki hello bölümle:

   ```json
   {
       "source": "SensorTag",
       "sink": "MyModule"
   },
   {
       "source": "MyModule",
       "sink": "mapping"
   }
   ```

1. Tuşuna `ESC`ve ardından `:wq` toosave hello dosya.

## <a name="run-hello-sample-application"></a>Merhaba örnek uygulamayı çalıştırın

1. Merhaba SensorTag açma.
1. Merhaba SSL_CERT_FILE ortam değişkeni hello aşağıdaki komutu çalıştırarak ayarlayın:

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. Merhaba aşağıdaki komutu çalıştırarak hello eklenen modülüyle Hello örnek uygulamayı çalıştırın:

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a>Sonraki adımlar

Kullanım hello IOT ağ geçidi tooconvert hello iletiden SensorTag hello .json biçime başarıyla seçtiğiniz.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
