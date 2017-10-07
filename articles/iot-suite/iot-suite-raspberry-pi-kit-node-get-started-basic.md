---
title: "aaaConnect Raspberry Pi'yi tooAzure IOT paketi ile gerçek algılayıcılar Node.js kullanarak | Microsoft Docs"
description: "Microsoft Azure IOT Starter Kit Merhaba hello Raspberry Pi 3 ve Azure IOT paketi kullanır. Uzaktan izleme çözümü, Raspberry Pi'yi toohello node.js tooconnect kullanın, telemetri algılayıcı toohello bulut göndermek ve hello çözüm panodan çağrılan toomethods yanıt."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 7ffb4a7a8c04b424a1f29170f4739d89f39a2429
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-nodejs"></a>Uzaktan izleme çözümü, Raspberry Pi 3 toohello bağlanmak ve Node.js kullanarak gerçek algılayıcı telemetri Gönder

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

Bu öğretici nasıl toouse hello Microsoft Azure IOT Starter Kit Raspberry Pi 3 toodevelop hello bulut ile iletişim kurabilen bir sıcaklık ve nem okuyucu gösterir. Merhaba öğretici kullanır:

- Raspbian OS programlama dili Node.js hello ve Microsoft Azure IOT SDK'sı Node.js tooimplement örnek aygıt hello.
- Merhaba IOT paketi Uzaktan izleme çözümü hello bulut tabanlı arka uç önceden yapılandırılmış.

## <a name="overview"></a>Genel Bakış

Bu öğreticide, hello aşağıdaki adımları tamamlayın:

- Merhaba Uzaktan izleme önceden yapılandırılmış çözüm tooyour Azure aboneliği örneği dağıtın. Bu adım, otomatik olarak dağıtır ve birden çok Azure hizmetlerini yapılandırır.
- Aygıt ve algılayıcılar toocommunicate bilgisayarınızın ve hello ile Uzaktan izleme çözümü ayarlayın.
- Merhaba örnek aygıt kodu tooconnect toohello Uzaktan izleme çözümü güncelleştirin ve hello çözüm panosunda görüntüleyebilirsiniz telemetri gönderebilir.

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Uzaktan izleme çözümü hükümleri Azure aboneliğinizde Azure Hizmetleri kümesi hello. Merhaba dağıtım gerçek Kurumsal Mimarisi yansıtır. tooavoid gereksiz Azure tüketim ücretleri, kendisiyle tamamladığınızda azureiotsuite.com hello önceden yapılandırılmış çözüm örneğiniz silin. Önceden yapılandırılmış çözümü yeniden hello varsa, kolayca yeniden oluşturabilirsiniz. Merhaba Uzaktan izleme çözümü çalıştığında hatayla tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a>İndirme ve hello örnek yapılandırma

Şimdi, indirin ve, Raspberry Pi'yi Merhaba Uzaktan izleme istemci uygulaması yapılandırın.

### <a name="install-nodejs"></a>Node.js yükleme

Node.js, Böğürtlenli Pi üzerinde yükleyin. Merhaba IOT SDK'sı Node.js için 0.11.5 Node.js veya sonraki sürümünü gerektirir. Merhaba aşağıdaki adımlarda size yol gösterecektir tooinstall Node.js v6.10.2 Raspberry Pi'yi üzerinde:

1. Komut tooupdate aşağıdaki hello Raspberry Pi'yi kullanın:

    ```sh
    sudo apt-get update
    ```

1. Komut toodownload hello Node.js ikili dosyaları tooyour Raspberry Pi'yi aşağıdaki hello kullan:

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. Komut tooinstall hello ikili dosyalarını aşağıdaki hello kullan:

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. Node.js v6.10.2 başarıyla yüklediniz komutu tooverify aşağıdaki hello kullan:

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a>Kopya hello depoları

Zaten yapmadıysanız, komutları, Pi üzerinde aşağıdaki çalıştırarak depoları hello kopya hello gerekli:

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git`
```

### <a name="update-hello-device-connection-string"></a>Merhaba cihaz bağlantı dizesi güncelleştir

Açık hello örnek kaynak dosyasına hello **nano** Düzenleyici'yi komutu aşağıdaki hello kullanma:

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

Merhaba satırı bulun:

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

Merhaba cihaz ve oluşturulan ve bu öğreticinin hello başlangıcında kaydedilen IOT Hub bilgileri ile Merhaba yer tutucu değerlerini değiştirin. Değişikliklerinizi kaydetmek (**Ctrl-O**, **Enter**) ve çıkış hello Düzenleyicisi'ni (**Ctrl-X**).

## <a name="run-hello-sample"></a>Merhaba örnek çalıştırın

Çalışma hello aşağıdaki tooinstall hello önkoşul hello örnek komutlar:

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic
npm install
```

Bu gibi durumlarda, hello örnek programı şimdi Raspberry Pi'yi hello üzerinde çalıştırabilirsiniz. Merhaba komutu girin:

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

Merhaba aşağıdaki örnek çıkış hello komut isteminde hello Raspberry Pi'yi gördüğünüz hello çıkış örneğidir:

![Böğürtlenli Pi uygulamadan çıktı][img-raspberry-output]

Tuşuna **Ctrl-C** tooexit hello program herhangi bir zamanda.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a>Sonraki adımlar

Merhaba ziyaret [Azure IOT Geliştirme Merkezi](https://azure.microsoft.com/develop/iot/) daha fazla örnekleri ve Azure IOT belgeler.

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-basic/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
