---
title: "ağ geçidi tooAzure IOT paketi kullanarak bir Intel NUC aaaConnect | Microsoft Docs"
description: "Merhaba Microsoft IOT ticari ağ geçidi Seti ve hello Uzaktan izleme önceden yapılandırılmış çözümü kullanın. Hello Azure IOT sınır ağ geçidi tooenable bir SensorTag aygıt tooconnect toohello Uzaktan izleme çözümü kullanın, telemetri toohello bulut gönderebilir ve hello çözüm panodan çağrılan toomethods yanıtlayabilir."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: 6f98ee3c1e2311a8644da9d72d40e671e7cbcf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a>Uzaktan izleme çözümü, Azure IOT sınır ağ geçidi toohello bağlanmak ve SensorTag telemetri Gönder

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

Bu öğretici nasıl çözüm toouse SensorTag aygıt toohello Uzaktan izleme Azure IOT kenar toosend sıcaklık ve nem verileri önceden yapılandırılmış gösterir. Merhaba SensorTag toohello Intel NUC ağ geçidi Bluetooth kullanarak bağlanır. Merhaba öğretici kullanır:

- Azure IOT kenar tooimplement bir örnek ağ geçidi.
- Merhaba IOT paketi Uzaktan izleme çözümü hello bulut tabanlı arka uç önceden yapılandırılmış.

## <a name="overview"></a>Genel Bakış

Bu öğreticide, hello aşağıdaki adımları tamamlayın:

- Merhaba Uzaktan izleme önceden yapılandırılmış çözüm tooyour Azure aboneliği örneği dağıtın. Bu adım, otomatik olarak dağıtır ve birden çok Azure hizmetlerini yapılandırır.
- Intel NUC ağ geçidi aygıtı toocommunicate bilgisayarınızın ve hello Uzaktan izleme çözümü ile ayarlayın.
- Intel NUC ağ geçidi tooreceive telemetrinize SensorTag aygıttan ayarlamak ve toohello Uzaktan izleme Panosu gönderebilirsiniz.

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[Texas Instruments bırak SensorTag][lnk-sensortag]. Bu öğretici, hello SensorTag Aygıttan Bluetooth üzerinden telemetri verilerini alır.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Uzaktan izleme çözümü hükümleri Azure aboneliğinizde Azure Hizmetleri kümesi hello. Merhaba dağıtım gerçek Kurumsal Mimarisi yansıtır. tooavoid gereksiz Azure tüketim ücretleri, kendisiyle tamamladığınızda azureiotsuite.com hello önceden yapılandırılmış çözüm örneğiniz silin. Önceden yapılandırılmış çözümü yeniden hello varsa, kolayca yeniden oluşturabilirsiniz. Merhaba Uzaktan izleme çözümü çalıştığında hatayla tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a>Bluetooth bağlantısını yapılandır

Bluetooth hello Intel NUC tooenable hello SensorTag aygıt tooconnect üzerinde yapılandırın ve telemetri gönderebilir.

### <a name="find-hello-mac-address-of-hello-sensortag"></a>Merhaba SensorTag Hello MAC adresini Bul

1. Merhaba Intel NUC üzerinde Hello Kabuğu'nda komut toounblock hello Bluetooth hizmeti aşağıdaki hello çalıştırın:

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. Çalışma hello aşağıdaki toostart hello Bluetooth hello Intel NUC hizmette komutları ve hello Bluetooth Kabuk girin:

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. Komut toopower hello Bluetooth denetleyicisinde aşağıdaki hello çalıştırın:

    ```bash
    power on
    ```

    Merhaba denetleyicisi açık olduğunda, bir ileti görür **güç değiştirme başarılı**.

1. Bluetooth cihazları yakındaki komutu tooscan için aşağıdaki hello çalıştırın:

    ```bash
    scan on
    ```

1. Tuşuna hello güç düğmesine hello SensorTag toomake üzerinde onu bulunabilir. Merhaba yeşil ışığı yanıp sönen.

1. Merhaba Kabuğu'nda bir ileti görüntülendiğinde bu hello denetleyicisi hello SensorTag bulduğunda, hello hello aygıtın MAC adresini not edin. Merhaba MAC adresi arar gibi **A0:E6:F8:B5:F6:00**. Merhaba ağ geçidi yapılandırdığınızda, daha sonra hello öğreticide hello MAC adresi gerekir.

1. Bluetooth tarama kapalı komutu tooturn aşağıdaki hello çalıştırın:

    ```bash
    scan off
    ```

1. Komut tooverify toohello SensorTag cihazın bağlanabilmesi için aşağıdaki hello çalıştırın:

    ```bash
    connect <SensorTag MAC address>
    ```

    Başarıyla bağlanıyorsanız, selamlama iletisine hello Kabuk gösterir **bağlantı başarılı** ve hello SensorTag aygıt hakkındaki bilgileri yazdırır. Bağlanamıyorsanız, SensorTag hala açık olduğundan hello denetleyin.

1. Şimdi SensorTag hello çıkarın ve hello aşağıdaki komutları çalıştırarak hello Bluetooth kabuktan çıkış:

    ```bash
    disconnect
    exit
    ```

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a>Merhaba özel IOT kenar modülü oluşturmak

Şimdi hello ağ geçidi toosend iletileri toohello Uzaktan izleme çözümü sağlayan hello özel IOT kenar modülü oluşturabilirsiniz. Bir ağ geçidi ve IOT kenar modülleri yapılandırma hakkında daha fazla bilgi için bkz: [Azure IOT kenar kavramları][lnk-gateway-concepts].

Merhaba kaynak kodu hello özel IOT kenar modülleri için aşağıdaki komutları hello kullanarak Github'dan indirin:

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

Hello hello aşağıdaki komutları kullanarak özel IOT kenar modülü oluşturun:

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

Merhaba derleme betiğindeki hello libsensor2remotemonitoring.so özel IOT kenar modülü hello yapı klasörüdür.

## <a name="configure-and-run-hello-iot-edge-gateway"></a>Yapılandırma ve hello IOT sınır ağ geçidi çalıştırma

Merhaba IOT sınır ağ geçidi toosend telemetri, SensorTag aygıt tooyour Uzaktan izleme Panosu artık yapılandırabilirsiniz. Bir ağ geçidi ve IOT kenar modülleri yapılandırma hakkında daha fazla bilgi için bkz: [Azure IOT kenar kavramları][lnk-gateway-concepts].

> [!TIP]
> Bu öğreticide kullandığınız hello standart `vi` hello Intel NUC üzerindeki metin düzenleyici. Değil kullandıysanız `vi` önce bir giriş öğretici gibi tamamlanmalıdır [UNIX - VI hello Düzenleyicisi Öğreticisi] [ lnk-vi-tutorial] toofamiliarize kendiniz bu düzenleyici ile. Alternatif olarak, daha kullanıcı dostu hello yükleyebilirsiniz [nano](https://www.nano-editor.org/) hello komutunu kullanarak Düzenleyicisi `smart install nano -y`.

Merhaba açık hello örnek yapılandırma dosyasında **VI** Düzenleyici'yi komutu aşağıdaki hello kullanma:

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
```

Merhaba Iothub modülü hello yapılandırmasında satırlardan hello bulun:

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

Bu öğretici hello oluşturup hello kaydettiğiniz IOT hub'ı bilgi değerlerle Başlat hello yer tutucu değiştirin. IoTHubName Hello değeri arar gibi **yourrmsolution37e08**, ve IoTSuffix hello değeri genellikle **azure devices.net**.

Merhaba eşleme modülü hello yapılandırmasında satırlardan hello bulun:

```json
args": [
  {
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

Hello yerine **macAddress** yer tutucu hello daha önce not ettiğiniz, SensorTag MAC adresine sahip. Hello yerine **DeviceID** ve **deviceKey** hello kimliklerini ve anahtarlarını hello Uzaktan izleme çözümünde daha önce oluşturduğunuz hello iki cihazlar için yer tutucularını.

Merhaba SensorTag modülü hello yapılandırmasında satırlardan hello bulun:

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

Hello yerine **aygıt\_mac\_adresi** yer tutucu hello daha önce not ettiğiniz, SensorTag MAC adresine sahip.

Yaptığınız değişiklikleri kaydedin.

Şimdi hello ağ geçidi hello aşağıdaki komutları kullanarak da çalıştırabilirsiniz:

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

Merhaba IOT sınır ağ geçidi Intel NUC hello üzerinde başlatır ve SensorTag toohello Uzaktan izleme çözümü hello telemetri gönderir:

![IOT sınır ağ geçidi SensorTag hello telemetri gönderir][img-telemetry]

Tuşuna **Ctrl-C** tooexit hello program herhangi bir zamanda.

## <a name="view-hello-telemetry"></a>Görünüm hello telemetri

Merhaba ağ geçidi artık SensorTag aygıt toohello Uzaktan izleme çözümü hello telemetri gönderiyor. Merhaba telemetri hello çözüm panosunda görüntüleyebilirsiniz. Merhaba çözüm panodan komutları tooyour SensorTag aygıt hello ağ geçidi üzerinden de gönderebilirsiniz.

- Toohello çözüm Panosu gidin.
- Select hello aygıt hello hello SensorTag temsil eden hello ağ geçidi olarak yapılandırılmış **aygıt tooView** açılır.
- Merhaba telemetri hello SensorTag aygıttan hello Panoda görüntüler.

![Merhaba SensorTag cihazlarından telemetri görüntüleme][img-telemetry-display]

> [!WARNING]
> Merhaba Uzaktan izleme çözümü Azure hesabınızda çalışan bırakırsanız hello çalıştırıldığında için faturalandırılır. Merhaba Uzaktan izleme çözümü çalıştığında hatayla tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config]. Bunu kullanmayı bitirdikten sonra hello önceden yapılandırılmış çözümü Azure hesabınızdan silin.


## <a name="next-steps"></a>Sonraki adımlar

Merhaba ziyaret [Azure IOT Geliştirme Merkezi](https://azure.microsoft.com/develop/iot/) daha fazla örnekleri ve Azure IOT belgeler.

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started