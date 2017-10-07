---
title: "IOT paketi C toosupport bellenim kullanarak aaaConnect Raspberry Pi'yi tooAzure güncelleştirmeleri | Microsoft Docs"
description: "Microsoft Azure IOT Starter Kit Merhaba hello Raspberry Pi 3 ve Azure IOT paketi kullanır. Uzaktan izleme çözümü, Raspberry Pi'yi toohello C tooconnect kullanın, telemetri algılayıcı toohello bulut göndermek ve uzak bellenim güncelleştirme gerçekleştirin."
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
ms.openlocfilehash: 36d39c6d754ddb025fd3f6b74d7795ed907b754c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-enable-remote-firmware-updates-using-c"></a>Uzaktan izleme çözümü, Raspberry Pi 3 toohello bağlanmak ve C kullanarak uzak Bellenim güncelleştirmeleri etkinleştir

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

Bu öğretici nasıl toouse hello Microsoft Azure IOT Starter Kit Raspberry Pi 3 gösterir:

* Merhaba bulut ile iletişim kurabilen bir sıcaklık ve nem okuyucu geliştirin.
* Etkinleştirmek ve bir uzak bellenim güncelleştirme tooupdate hello istemci uygulaması Raspberry Pi'yi hello üzerinde gerçekleştirin.

Merhaba öğretici kullanır:

* Raspbian işletim sistemi, hello C programlama dili ve C tooimplement örnek cihaz için Microsoft Azure IOT SDK'sı hello.
* Merhaba IOT paketi Uzaktan izleme çözümü hello bulut tabanlı arka uç önceden yapılandırılmış.

## <a name="overview"></a>Genel Bakış

Bu öğreticide, hello aşağıdaki adımları tamamlayın:

* Merhaba Uzaktan izleme önceden yapılandırılmış çözüm tooyour Azure aboneliği örneği dağıtın. Bu adım, otomatik olarak dağıtır ve birden çok Azure hizmetlerini yapılandırır.
* Aygıt ve algılayıcılar toocommunicate bilgisayarınızın ve hello ile Uzaktan izleme çözümü ayarlayın.
* Merhaba örnek aygıt kodu tooconnect toohello Uzaktan izleme çözümü güncelleştirin ve hello çözüm panosunda görüntüleyebilirsiniz telemetri gönderebilir.
* Merhaba örnek aygıt kodu tooupdate hello istemci uygulaması kullanın.

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Uzaktan izleme çözümü hükümleri Azure aboneliğinizde Azure Hizmetleri kümesi hello. Merhaba dağıtım gerçek Kurumsal Mimarisi yansıtır. tooavoid gereksiz Azure tüketim ücretleri, kendisiyle tamamladığınızda azureiotsuite.com hello önceden yapılandırılmış çözüm örneğiniz silin. Önceden yapılandırılmış çözümü yeniden hello varsa, kolayca yeniden oluşturabilirsiniz. Merhaba Uzaktan izleme çözümü çalıştığında hatayla tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config].

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a>İndirme ve hello örnek yapılandırma

Şimdi, indirin ve, Raspberry Pi'yi Merhaba Uzaktan izleme istemci uygulaması yapılandırın.

### <a name="clone-hello-repositories"></a>Kopya hello depoları

Henüz yapmadıysanız, komutları, Pi üzerinde aşağıdaki çalıştırarak depoları hello kopya hello gerekli:

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a>Merhaba cihaz bağlantı dizesi güncelleştir

Merhaba açık hello örnek yapılandırma dosyasında **nano** Düzenleyici'yi komutu aşağıdaki hello kullanma:

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

Bilgilerle oluşturulur ve bu öğreticinin hello başlangıcında kaydedilmiş hello cihaz kimliği ve IOT hub'ı Hello yer tutucu değerlerini değiştirin.

İşiniz bittiğinde, hello deviceınfo dosyasının Merhaba içeriğine hello örnek aşağıdaki gibi görünmelidir:

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

Değişikliklerinizi kaydetmek (**Ctrl-O**, **Enter**) ve çıkış hello Düzenleyicisi'ni (**Ctrl-X**).

## <a name="build-hello-sample"></a>Merhaba örnek oluşturma

Zaten yapmadıysanız, hello önkoşul hello Microsoft Azure IOT cihaz SDK'sı için C Raspberry Pi'yi hello üzerinde komutları bir terminalde aşağıdaki hello çalıştırarak yükleyin:

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

Merhaba örnek çözümü Raspberry Pi'yi hello üzerinde şimdi oluşturabilirsiniz:

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
```

Bu gibi durumlarda, hello örnek programı şimdi Raspberry Pi'yi hello üzerinde çalıştırabilirsiniz. Merhaba komutu girin:

  ```sh
  sudo ~/cmake/remote_monitoring/remote_monitoring
  ```

Merhaba aşağıdaki örnek çıkış hello komut isteminde hello Raspberry Pi'yi gördüğünüz hello çıkış örneğidir:

![Böğürtlenli Pi uygulamadan çıktı][img-raspberry-output]

Tuşuna **Ctrl-C** tooexit hello program herhangi bir zamanda.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. Merhaba çözüm panosunda tıklatın **aygıtları** toovisit hello **aygıtları** sayfası. Hello Raspberry Pi'yi seçin **cihaz listesi**. Ardından **yöntemleri**:

    ![Panoda aygıtları listele][img-list-devices]

1. Merhaba üzerinde **yöntemi çağırma** sayfasında, **InitiateFirmwareUpdate** hello içinde **yöntemi** açılır.

1. Merhaba, **FWPackageURI** alanına, **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**. Bu Arşiv hello uygulamasını hello bellenim 2.0 sürümünü içerir.

1. Seçin **InvokeMethod**. Merhaba Raspberry Pi'yi Hello uygulamasına bir bildirim geri toohello çözüm Panosu gönderir. Ardından, hello bellenim güncelleştirme işlemi'nin hello yeni hello bellenim sürümünü indirerek başlar:

    ![Yöntem geçmişini göster][img-method-history]

## <a name="observe-hello-firmware-update-process"></a>Merhaba bellenim güncelleştirme işlemini inceleyin

Merhaba cihazda çalışan gibi hello bellenim güncelleştirme işlemi görebilirsiniz ve hello görüntüleyerek hello çözüm Panosu özelliklerinde bildirdi:

1. Merhaba güncelleştirme işleminin hello ediyor Raspberry Pi'yi hello üzerinde görüntüleyebilirsiniz:

    ![Güncelleştirme ilerlemesini Göster][img-update-progress]

    > [!NOTE]
    > Merhaba güncelleştirme tamamlandığında hello Uzaktan izleme uygulama sessizce yeniden başlatır. Merhaba komutunu `ps -ef` çalıştığından tooverify. Tooterminate hello işlem istiyorsanız hello kullanın `kill` hello işlem kimlikli komutu.

1. Merhaba çözüm portalında hello aygıt tarafından bildirilen şekilde hello bellenim güncelleştirme hello durumunu görüntüleyebilirsiniz. Merhaba aşağıdaki ekran görüntüsü hello durumu ve her aşamanın hello güncelleştirme işlemini hello yeni üretici yazılımı sürümüne ve süresini gösterir:

    ![İş durumunu göster][img-job-status]

    Geri toohello Pano giderseniz, hello aygıt hala hello bellenim güncelleştirme aşağıdaki telemetri gönderiyor doğrulayabilirsiniz.

> [!WARNING]
> Merhaba Uzaktan izleme çözümü Azure hesabınızda çalışan bırakırsanız hello çalıştırıldığında için faturalandırılır. Merhaba Uzaktan izleme çözümü çalıştığında hatayla tüketiminin azaltılması hakkında daha fazla bilgi için bkz: [yapılandırma Azure IOT paketi önceden yapılandırılmış çözümleri tanıtım amacıyla][lnk-demo-config]. Bunu kullanmayı bitirdikten sonra hello önceden yapılandırılmış çözümü Azure hesabınızdan silin.

## <a name="next-steps"></a>Sonraki adımlar

Merhaba ziyaret [Azure IOT Geliştirme Merkezi](https://azure.microsoft.com/develop/iot/) daha fazla örnekleri ve Azure IOT belgeler.


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md