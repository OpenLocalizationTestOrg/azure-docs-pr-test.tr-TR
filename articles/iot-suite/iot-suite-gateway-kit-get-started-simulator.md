---
title: "ağ geçidi tooAzure IOT paketi kullanarak bir Intel NUC aaaConnect | Microsoft Docs"
description: "Merhaba Microsoft IOT ticari ağ geçidi Seti ve hello Uzaktan izleme önceden yapılandırılmış çözümü kullanın. Kullanım hello Azure IOT sınır ağ geçidi tooconnect toohello Uzaktan izleme çözümü, sanal telemetriyi toohello bulut gönderebilir ve toomethods hello çözüm panodan çağrılan yanıtlayabilir."
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
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 46b545fc21b054191c8f78ace20fc628f839a819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a>Uzaktan izleme çözümü, Azure IOT sınır ağ geçidi toohello bağlanmak ve sanal telemetriyi Gönder

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

Bu öğretici nasıl çözüm toouse Azure IOT kenar toosimulate sıcaklık ve nem toosend toohello Uzaktan izleme verilerini önceden yapılandırılmış gösterir. Merhaba öğretici kullanır:

- Azure IOT kenar tooimplement bir örnek ağ geçidi.
- Merhaba IOT paketi Uzaktan izleme çözümü hello bulut tabanlı arka uç önceden yapılandırılmış.

## <a name="overview"></a>Genel Bakış

Bu öğreticide, hello aşağıdaki adımları tamamlayın:

- Merhaba Uzaktan izleme önceden yapılandırılmış çözüm tooyour Azure aboneliği örneği dağıtın. Bu adım, otomatik olarak dağıtır ve birden çok Azure hizmetlerini yapılandırır.
- Intel NUC ağ geçidi aygıtı toocommunicate bilgisayarınızın ve hello Uzaktan izleme çözümü ile ayarlayın.
- IOT sınır ağ geçidi toosend hello çözüm panosunda görüntüleyebilirsiniz telemetri benzetimli hello yapılandırın.

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Uzaktan izleme çözümü hükümleri Azure aboneliğinizde Azure Hizmetleri kümesi hello. Merhaba dağıtım gerçek Kurumsal Mimarisi yansıtır. tooavoid gereksiz Azure tüketim ücretleri, kendisiyle tamamladığınızda azureiotsuite.com hello önceden yapılandırılmış çözüm örneğiniz silin. Önceden yapılandırılmış çözümü yeniden hello varsa, kolayca yeniden oluşturabilirsiniz. Merhaba Uzaktan izleme çözümü çalıştığında hatayla tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

Bir cihaz kimliği gibi kullanarak ikinci bir cihaz Hello önceki adımları tooadd yineleyin **device02**. Merhaba örnek verileri iki sanal aygıtlardan hello ağ geçidi toohello Uzaktan izleme çözümünde gönderir.

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

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
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

Merhaba derleme betiğindeki hello libsimulator.so özel IOT kenar modülü hello yapı klasörüdür.

## <a name="configure-and-run-hello-iot-edge-gateway"></a>Yapılandırma ve hello IOT sınır ağ geçidi çalıştırma

Merhaba IOT sınır ağ geçidi toosend sanal telemetriyi tooyour Uzaktan izleme Panosu artık yapılandırabilirsiniz. Bir ağ geçidi ve IOT kenar modülleri yapılandırma hakkında daha fazla bilgi için bkz: [Azure IOT kenar kavramları][lnk-gateway-concepts].

> [!TIP]
> Bu öğreticide kullandığınız hello standart `vi` hello Intel NUC üzerindeki metin düzenleyici. Değil kullandıysanız `vi` önce bir giriş öğretici gibi tamamlanmalıdır [UNIX - VI hello Düzenleyicisi Öğreticisi] [ lnk-vi-tutorial] toofamiliarize kendiniz bu düzenleyici ile. Alternatif olarak, daha kullanıcı dostu hello yükleyebilirsiniz [nano](https://www.nano-editor.org/) hello komutunu kullanarak Düzenleyicisi `smart install nano -y`.

Merhaba açık hello örnek yapılandırma dosyasında **VI** Düzenleyici'yi komutu aşağıdaki hello kullanma:

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
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
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  },
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

Hello yerine **DeviceID** ve **deviceKey** hello kimliklerini ve anahtarlarını hello Uzaktan izleme çözümünde daha önce oluşturduğunuz hello iki cihazlar için yer tutucularını.

Yaptığınız değişiklikleri kaydedin.

Şimdi hello aşağıdaki hello kullanarak IOT sınır ağ geçidi komutları çalıştırabilirsiniz:

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

Merhaba ağ geçidi Intel NUC hello üzerinde başlatır ve sanal telemetriyi toohello Uzaktan izleme çözümü gönderir:

![IOT sınır ağ geçidi sanal telemetriyi oluşturur][img-simulated telemetry]

Tuşuna **Ctrl-C** tooexit hello program herhangi bir zamanda.

## <a name="view-hello-telemetry"></a>Görünüm hello telemetri

Merhaba IOT sınır ağ geçidi artık sanal telemetriyi toohello Uzaktan izleme çözümü gönderiyor. Merhaba telemetri hello çözüm panosunda görüntüleyebilirsiniz.

- Toohello çözüm Panosu gidin.
- Hello hello ağ geçidi olarak yapılandırılmış hello iki cihazlar birini **aygıt tooView** açılır.
- Merhaba telemetri hello ağ geçidi aygıtlardan hello panosunda görüntülenir.

![Telemetri benzetimli hello ağ geçidi aygıtlardan görüntüle][img-telemetry-display]

> [!WARNING]
> Merhaba Uzaktan izleme çözümü Azure hesabınızda çalışan bırakırsanız hello çalıştırıldığında için faturalandırılır. Merhaba Uzaktan izleme çözümü çalıştığında hatayla tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config]. Bunu kullanmayı bitirdikten sonra hello önceden yapılandırılmış çözümü Azure hesabınızdan silin.

## <a name="next-steps"></a>Sonraki adımlar

Merhaba ziyaret [Azure IOT Geliştirme Merkezi](https://azure.microsoft.com/develop/iot/) daha fazla örnekleri ve Azure IOT belgeler.

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started