---
title: "Connect Raspberry pi (C) tooAzure IOT - sorunlarını giderme | Microsoft Docs"
description: "Sayfa hello Raspberry Pi Node.js deneyimi için sorun giderme"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IOT sorunları, Internet şeyler sorunları"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 22cf50dc-8206-42a2-a1fc-f75fa85135fa
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8f0807104550e8e53a132f7741564b33f1db17ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Sorun giderme
## <a name="hardware-issues"></a>Donanım sorunları
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a>çalıştırır yanı sıra ancak LED hello Merhaba uygulaması yanıp sönen değil
Bu her zaman ilgili toohardware hattı bağlantı sorunudur. Aşağıdaki adımları tooidentify sorunları hello kullan:

1. Merhaba doğru seçtiğiniz denetleyin **GPIO'yu** panonuzu üzerinde. Merhaba iki bağlantı noktası olmalıdır **GPIO'yu GND (PIN 6)** ve **GPIO'yu 04 (PIN 7)**.
2. Merhaba polarite, LED, doğru olup olmadığını denetleyin. Merhaba uzun leg hello belirtmek **pozitif**, Number PIN.
3. Kullanım hello **3, 3v PIN** ve **GND PIN** Raspberry Pi 3. Pi DC Güç hello kabul eder. Bu hello LED düzgün çalışır denetleyin.

![LED belirtimi](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a>Diğer donanım sorunları
Merhaba Raspberry Pi 3'te sık karşılaşılan sorunları giderme hakkında daha fazla bilgi için bkz: [resmi sorun giderme sayfa](http://elinux.org/R-Pi_Troubleshooting).

## <a name="nodejs-package-issues"></a>Node.js paket sorunları
### <a name="no-response-during-gulp-tasks"></a>Gulp görevler sırasında yanıt yok
Çalışan gulp görevleri sorunlarla karşılaşırsanız, hello ekleyebilirsiniz `--verbose` hata ayıklama seçeneği. Ctrl + C'ı kullanarak tooterminate geçerli gulp görevleri deneyin ve ardından konsol penceresinde toosee hata ayıklama iletileri komutunda aşağıdaki hello çalıştırın. Ayrıntılı hata iletileri, konsol çıktısı görebilirsiniz.

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a>Aygıt Bulma sorunları
İlgili hello ortak sorunları gidermede yardım için `devdisco` komutu, hello denetleyin [Benioku](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).

### <a name="npm-issues"></a>npm sorunları
Tooupdate komutu aşağıdaki hello kullanarak npm paket deneyin:

```bash
npm install -g npm
```

Merhaba sorun devam ederse, bu makalenin hello sonunda yorumlarınızı bırakın veya bir GitHub sorunu oluşturmak bizim [örnek depo](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).

## <a name="remote-debugging"></a>Uzaktan hata ayıklama
### <a name="run-hello-sample-application-in-debug-mode"></a>Hata ayıklama modunda Hello örnek uygulamayı çalıştırın
```bash
gulp run --debug
```

Merhaba hata ayıklama altyapısı hazır olduğunda, görmelisiniz ```Debugger listening on port 5858``` hello konsol çıkışı.

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a>Visual Studio Code tooconnect toohello uzak aygıt yapılandırma
1. Açık hello **hata ayıklama** hello yan sol panelde.
2. Merhaba yeşil tıklatın **hata ayıklamayı Başlat** (F5) düğmesi. Visual Studio Code Launch.json'u dosyasını açar.
3. Merhaba Launch.json'u dosya içeriği aşağıdaki hello ile güncelleştirin. Değiştir `[device hostname or IP address]` Merhaba, gerçek cihaz IP adresi veya ana bilgisayar adı ile.

> [!NOTE]
> Merhaba Visual Studio hata ayıklama, hakkında daha fazla toolearn başvurun çok[Visual Studio kodda hata ayıklama](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).


```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Attach",
            "type": "node",
            "request": "attach",
            "port": 5858,
            "address": "[device hostname or IP address]",
            "restart": false,
            "sourceMaps": false,
            "outDir": null,
            "localRoot": "${workspaceRoot}",
            "remoteRoot": null
        }
    ]
}
```

![Uzaktan hata ayıklama yapılandırması](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a>Toohello uzak uygulama ekleme
Merhaba yeşil tıklatın **hata ayıklamayı Başlat** (F5) düğmesini toostart hata ayıklama.

Okuma [JavaScript VS code'da](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn hello hata ayıklayıcı hakkında daha fazla.

![Uzaktan etkileşimli hata ayıklama](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a>Azure CLI sorunları
Hello Azure komut satırı arabirimi (Azure CLI) önizleme yapıdır. tooseek çözümleri hello kullanabilir [Önizleme Yükleme Kılavuzu](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).

Tüm hatalar hello aracı ile karşılaşırsanız, dosya bir [sorunu](https://github.com/Azure/azure-cli/issues) hello içinde **sorunları** hello GitHub deposuna bölümü.

Sık karşılaşılan sorunları giderme konusunda yardım için hello denetleyin [Benioku](https://github.com/Azure/azure-cli/blob/master/README.rst).

## <a name="python-installation-issues"></a>Python yükleme sorunları
### <a name="legacy-installation-issues-macos"></a>Eski yükleme sorunları (macOS)
PIP yüklüyorsanız, eski paketleri ile yüklendiğinde izin hatası atılır **su** izinleri. Python brew (macOS) kullanarak önceki bir yüklemesini tümüyle kaldırılmamış. Bu durum oluşur. Önceki yüklemeye ait bazı PIP paketler hello izni hatasına neden oluyor kök tarafından oluşturuldu. Merhaba çözüm tooremove bu paketleri kök tarafından yüklü değil. Aşağıdaki adımları toocomplete hello bu görevi kullanın:

1. Gidin: /usr/local/lib/python2.7/site-packages
2. Kök tarafından oluşturulan listesi paketler:`ls -l | grep root`
3. Paketler, adım 2 ' Kaldır:`sudo rm -rf {package name}`
4. Python yeniden yükleyin.

## <a name="azure-iot-hub-issues"></a>Azure IOT hub'ı sorunları
Azure CLI ile Azure IOT hub'ınızı başarıyla kaynak sağlandı ve tooyour IOT hub'a bağlanan bir aracı toomanage hello aygıtları ihtiyacınız varsa araçları aşağıdaki hello deneyin.

### <a name="device-explorer"></a>Cihaz Gezgini
Merhaba [aygıt explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) aracı Windows yerel makinenizde çalıştırır ve azure'da tooyour IOT hub'ı bağlar. Merhaba aşağıdaki ile iletişim kurar [IOT Hub uç noktaları](iot-hub-devguide.md):


* *Cihaz Kimlik Yönetimi* tooprovision ve IOT hub'ınıza kayıtlı cihazları yönetme.
* *Cihaz bulut alma* aygıt tooyour IOT hub'dan gönderilen iletileri izleyebilmek.
* *Bulut cihaz Gönder* IOT hub'ından tooyour aygıtları iletileri gönderebilmesi.

IOT hub bağlantı dizenizi bu aracı toouse içindeki tüm özelliklerini yapılandırın.

### <a name="iothub-explorer"></a>ıothub Gezgini
[ıothub explorer](https://github.com/Azure/iothub-explorer) bir örnek çok platformlu CLI toomanage aygıtları aracıdır. Merhaba kimlik kayıt defterinde hello aracı toomanage hello aygıtları'nı kullanın, cihaz bulut iletilerini izlemek ve bulut-cihaz iletilerini göndermek.

tooinstall hello ıothub explorer aracı, aşağıdaki komut, komut satırı ortamınızdaki hello çalıştırın (ön) en son sürümünü hello:

```bash
npm install -g iothub-explorer@latest
```

Tüm hakkında ek Yardım tooget iothub-explorer komutlar ve bunların parametrelerini hello komutu aşağıdaki hello kullanabilirsiniz:

```bash
iothub-explorer help
```

### <a name="azure-portal"></a>Azure portalına
Tam CLI deneyimi oluşturma ve Azure kaynaklarınızı yönetmenize yardımcı olur. Toouse hello isteyebilirsiniz [Azure portal](../azure-portal-overview.md) toohelp sağlamanıza, yönetmek ve Azure kaynaklarınızı hata ayıklama.

## <a name="azure-storage-issues"></a>Azure depolama sorunları
[Microsoft Azure Storage Gezgini (Önizleme)](http://storageexplorer.com) toowork Windows, macOS ve Linux Azure Storage veri ile kullanabileceğiniz Microsoft tek başına uygulamadır. Bu aracı kullanarak tooyour tablo bağlanabilir ve hello verilerde bakın. Bu aracı tootroubleshoot Azure depolama sorunlarınızı kullanabilirsiniz.

