---
title: "Böğürtlenli Pi (C) bağlanmak için Azure IOT - sorunlarını giderme | Microsoft Docs"
description: "Sayfa Raspberry Pi Node.js deneyimi için sorun giderme"
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
ms.openlocfilehash: f9058068972ddbb674d3cd159948835dc88c4451
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a>Sorun giderme
## <a name="hardware-issues"></a>Donanım sorunları
### <a name="the-application-runs-well-but-the-led-is-not-blinking"></a>Uygulama iyi çalışır ancak ışığı yanıp sönen değil
Bu sorun, her zaman donanım hattı bağlantı ilişkilidir. Sorunları belirlemek için aşağıdaki adımları kullanın:

1. Doğru seçtiğiniz denetleyin **GPIO'yu** panonuzu üzerinde. İki bağlantı noktası olmalıdır **GPIO'yu GND (PIN 6)** ve **GPIO'yu 04 (PIN 7)**.
2. LED polarite doğru olduğunu denetleyin. Uzun leg belirtmelidir **pozitif**, Number PIN.
3. Kullanım **3, 3v PIN** ve **GND PIN** üzerinde Raspberry 3 ila Pi. Pi DC Güç kabul eder. LED düzgün çalışıp çalışmadığını denetleyin.

![LED belirtimi](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a>Diğer donanım sorunları
Raspberry Pi 3'te sık karşılaşılan sorunları giderme hakkında daha fazla bilgi için bkz: [resmi sorun giderme sayfa](http://elinux.org/R-Pi_Troubleshooting).

## <a name="nodejs-package-issues"></a>Node.js paket sorunları
### <a name="no-response-during-gulp-tasks"></a>Gulp görevler sırasında yanıt yok
Ekleyebileceğiniz gulp görevleri çalıştırma sorunlarla karşılaşmanız halinde, `--verbose` hata ayıklama seçeneği. Ctrl + C'ı kullanarak geçerli gulp görevleri sonlandırmak deneyin ve ardından görmek için konsol penceresinde aşağıdaki komutu çalıştırın hata ayıklama iletilerini. Ayrıntılı hata iletileri, konsol çıktısı görebilirsiniz.

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a>Aygıt Bulma sorunları
İlgili genel sorunları gidermede yardım için `devdisco` komutu, onay [Benioku](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).

### <a name="npm-issues"></a>npm sorunları
Aşağıdaki komutu kullanarak npm paket güncelleştirmeyi deneyin:

```bash
npm install -g npm
```

Sorun devam ederse, bu makalenin sonunda yorumlarınızı bırakın veya bir GitHub sorunu oluşturmak bizim [örnek depo](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).

## <a name="remote-debugging"></a>Uzaktan hata ayıklama
### <a name="run-the-sample-application-in-debug-mode"></a>Örnek uygulamayı hata ayıklama modunda çalıştırın
```bash
gulp run --debug
```

Hata ayıklama altyapısı hazır olduğunda, görmelisiniz ```Debugger listening on port 5858``` konsol çıkışı.

### <a name="configure-visual-studio-code-to-connect-to-the-remote-device"></a>Visual Studio Code uzak cihaza bağlanmak için yapılandırın
1. Açık **hata ayıklama** sol tarafındaki paneli.
2. Yeşil tıklatın **hata ayıklamayı Başlat** (F5) düğmesi. Visual Studio Code Launch.json'u dosyasını açar.
3. Launch.json'u dosyasını aşağıdaki içerik ile güncelleştirin. Değiştir `[device hostname or IP address]` gerçek aygıt IP adresi veya ana bilgisayar adı.

> [!NOTE]
> Visual Studio hata ayıklama hakkında daha fazla bilgi için lütfen [Visual Studio kodda hata ayıklama](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).


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

### <a name="attach-to-the-remote-application"></a>Uzak uygulamasına ekleme
Yeşil tıklatın **hata ayıklamayı Başlat** hata ayıklamayı başlatmak için (F5) düğmesini.

Okuma [JavaScript VS code'da](https://code.visualstudio.com/docs/languages/javascript#_debugging) hata ayıklayıcı hakkında daha fazla bilgi için.

![Uzaktan etkileşimli hata ayıklama](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a>Azure CLI sorunları
Azure komut satırı arabirimi (Azure CLI) önizleme yapıdır. Çözümleri aramak için kullanabileceğiniz [Önizleme Yükleme Kılavuzu](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).

Tüm hatalar aracı ile karşılaşırsanız, dosya bir [sorunu](https://github.com/Azure/azure-cli/issues) içinde **sorunları** GitHub depo bölümü.

Sık karşılaşılan sorunları giderme konusunda yardım için kontrol [Benioku](https://github.com/Azure/azure-cli/blob/master/README.rst).

## <a name="python-installation-issues"></a>Python yükleme sorunları
### <a name="legacy-installation-issues-macos"></a>Eski yükleme sorunları (macOS)
PIP yüklüyorsanız, eski paketleri ile yüklendiğinde izin hatası atılır **su** izinleri. Python brew (macOS) kullanarak önceki bir yüklemesini tümüyle kaldırılmamış. Bu durum oluşur. Önceki yüklemeye ait bazı PIP paketler izni hataya neden olan kök tarafından oluşturuldu. Kök tarafından yüklenen bu paketleri kaldırmak için çözümüdür. Bu görevi tamamlamak için aşağıdaki adımları kullanın:

1. Gidin: /usr/local/lib/python2.7/site-packages
2. Kök tarafından oluşturulan listesi paketler:`ls -l | grep root`
3. Paketler, adım 2 ' Kaldır:`sudo rm -rf {package name}`
4. Python yeniden yükleyin.

## <a name="azure-iot-hub-issues"></a>Azure IOT hub'ı sorunları
Azure CLI ile Azure IOT hub'ınızı başarıyla kaynak sağlandı ve IOT hub'ınıza bağlanan cihazları yönetmek için bir aracı ihtiyacınız varsa aşağıdaki araçları deneyin.

### <a name="device-explorer"></a>Cihaz Gezgini
[Aygıt explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) aracı Windows yerel makinenizde çalıştırır ve Azure IOT hub'ınıza bağlanır. Aşağıdaki ile iletişim kurar [IOT Hub uç noktaları](iot-hub-devguide.md):


* *Cihaz Kimlik Yönetimi* sağlamak ve IOT hub'ınıza kayıtlı cihazları yönetmek için.
* *Cihaz bulut alma* cihazınızın IOT hub'ına gönderilen iletileri izleyebilmek.
* *Bulut cihaz Gönder* IOT hub'ından aygıtlarınıza iletileri gönderebilmesi.

IOT hub bağlantı dizenizi tüm özellikleri kullanmak için bu aracı içinde yapılandırın.

### <a name="iothub-explorer"></a>ıothub Gezgini
[ıothub explorer](https://github.com/Azure/iothub-explorer) cihazları yönetmek için bir örnek çok platformlu CLI aracıdır. Cihaz kimlik kayıt defterinde yönetmek, cihaz bulut iletilerini izlemek ve bulut-cihaz iletilerini göndermek için aracını kullanabilirsiniz.

Iothub explorer Aracı (ön) en son sürümünü yüklemek için komut satırı ortamınızda aşağıdaki komutu çalıştırın:

```bash
npm install -g iothub-explorer@latest
```

Tüm ıothub explorer komutları ve bunların parametreleri hakkında ek Yardım almak için aşağıdaki komutu kullanın:

```bash
iothub-explorer help
```

### <a name="azure-portal"></a>Azure portalına
Tam CLI deneyimi oluşturma ve Azure kaynaklarınızı yönetmenize yardımcı olur. Kullanmak isteyebilirsiniz [Azure portal](../azure-portal-overview.md) sağlama Yardım, yönetmek ve Azure kaynaklarınızı hata ayıklamak için.

## <a name="azure-storage-issues"></a>Azure depolama sorunları
[Microsoft Azure Storage Gezgini (Önizleme)](http://storageexplorer.com) Windows, macOS ve Linux Azure Storage verilerle çalışmak için kullanabileceğiniz bir Microsoft tek başına uygulamadır. Bu aracı kullanarak tablonuza bağlanabilir ve içindeki verilerin bakın. Azure Storage sorunlarını gidermek için bu aracı kullanabilirsiniz.

