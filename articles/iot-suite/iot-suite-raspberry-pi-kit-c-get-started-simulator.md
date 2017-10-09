---
title: aaaConnect Raspberry Pi'yi tooAzure IOT paketi C ile sanal telemetriyi kullanarak | Microsoft Docs
description: "Microsoft Azure IOT Starter Kit Merhaba hello Raspberry Pi 3 ve Azure IOT paketi kullanır. Uzaktan izleme çözümü, Raspberry Pi'yi toohello C tooconnect kullanmak, sanal telemetriyi toohello bulut gönderebilir ve hello çözüm panodan çağrılan toomethods yanıtlayabilir."
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
ms.openlocfilehash: 3c4fa43b381385d1a7896cada34aa3aa0b8e5fb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-simulated-telemetry-using-c"></a>Uzaktan izleme çözümü, Raspberry Pi 3 toohello bağlanmak ve C kullanarak sanal telemetriyi Gönder

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

Bu öğretici nasıl toouse hello Raspberry Pi 3 toosimulate sıcaklık ve nem veri toosend toohello bulut gösterir. Merhaba öğretici kullanır:

- Raspbian işletim sistemi, hello C programlama dili ve C tooimplement örnek cihaz için Microsoft Azure IOT SDK'sı hello.
- Merhaba IOT paketi Uzaktan izleme çözümü hello bulut tabanlı arka uç önceden yapılandırılmış.

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Uzaktan izleme çözümü hükümleri Azure aboneliğinizde Azure Hizmetleri kümesi hello. Merhaba dağıtım gerçek Kurumsal Mimarisi yansıtır. tooavoid gereksiz Azure tüketim ücretleri, kendisiyle tamamladığınızda azureiotsuite.com hello önceden yapılandırılmış çözüm örneğiniz silin. Önceden yapılandırılmış çözümü yeniden hello varsa, kolayca yeniden oluşturabilirsiniz. Merhaba Uzaktan izleme çözümü çalıştığında hatayla tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-hello-sample"></a>İndirme ve hello örnek yapılandırma

Şimdi, indirin ve, Raspberry Pi'yi Merhaba Uzaktan izleme istemci uygulaması yapılandırın.

### <a name="clone-hello-repositories"></a>Kopya hello depoları

Zaten yapmadıysanız, bir terminal komutlarda, Pi üzerinde aşağıdaki çalıştırarak depoları hello kopya hello gerekli:

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a>Merhaba cihaz bağlantı dizesi güncelleştir

Açık hello örnek kaynak dosyasına hello **nano** Düzenleyici'yi komutu aşağıdaki hello kullanma:

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/remote_monitoring/remote_monitoring.c
```

Satırlardan hello bulun:

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

Merhaba cihaz ve oluşturulan ve bu öğreticinin hello başlangıcında kaydedilen IOT Hub bilgileri ile Merhaba yer tutucu değerlerini değiştirin. Değişikliklerinizi kaydetmek (**Ctrl-O**, **Enter**) ve çıkış hello Düzenleyicisi'ni (**Ctrl-X**).

## <a name="build-hello-sample"></a>Merhaba örnek oluşturma

Hello önkoşul hello Microsoft Azure IOT cihaz SDK'sı için bir terminal komutlarda Raspberry Pi'yi hello üzerinde aşağıdaki hello çalıştırarak için C yükleyin:

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

Bu gibi durumlarda, güncelleştirilmiş hello örnek çözümü şimdi Raspberry Pi'yi hello üzerinde oluşturabilirsiniz:

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
```

Bu gibi durumlarda, hello örnek programı şimdi Raspberry Pi'yi hello üzerinde çalıştırabilirsiniz. Merhaba komutu girin:

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

Merhaba aşağıdaki örnek çıkış hello komut isteminde hello Raspberry Pi'yi gördüğünüz hello çıkış örneğidir:

![Böğürtlenli Pi uygulamadan çıktı][img-raspberry-output]

Tuşuna **Ctrl-C** tooexit hello program herhangi bir zamanda.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a>Sonraki adımlar

Merhaba ziyaret [Azure IOT Geliştirme Merkezi](https://azure.microsoft.com/develop/iot/) daha fazla örnekleri ve Azure IOT belgeler.

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-simulator/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
