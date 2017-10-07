---
title: "Intel Edison'u (düğüm) tooAzure IOT - Ders 4 bağlanın: sorun giderme | Microsoft Docs"
description: "Sayfa Intel Edison'u Node.js deneyimi için sorun giderme"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino sorunlarını giderme"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: f11c5521-8a36-44c0-baad-f5ec26ab4618
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9502300f7f372255572b49bea45dd3e1fdaeeb37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Sorun giderme
## <a name="hardware-issues"></a>Donanım sorunları
Merhaba Intel Edison'u ortak sorunlarını çözme hakkında daha fazla bilgi için bkz [resmi sorun giderme sayfa](https://software.intel.com/en-us/node/637974).

## <a name="nodejs-package-issues"></a>Node.js paket sorunları
### <a name="no-response-during-gulp-tasks"></a>Gulp görevler sırasında yanıt yok
Çalışan gulp görevleri sorunlarla karşılaşırsanız, hello ekleyebilirsiniz `--verbose` hata ayıklama seçeneği. Tooterminate geçerli gulp görevleri kullanarak deneyin `Ctrl + C`, ve ardından çalışma hello aşağıdaki konsol penceresi toosee hata ayıklama iletileri komutu. Ayrıntılı hata iletileri, konsol çıktısı görebilirsiniz. 

```bash
gulp --verbose
```

### <a name="npm-issues"></a>NPM sorunları
Tooupdate NPM paket komutu aşağıdaki hello ile deneyin:

```bash
npm install -g npm
```

Merhaba sorun devam ederse, bu makalenin hello sonunda yorumlarınızı bırakın veya bir GitHub sorunu oluşturmak bizim [örnek depo][sample-repository].

## <a name="remote-debugging"></a>Uzaktan hata ayıklama

### <a name="run-hello-sample-application-in-debug-mode"></a>Hata ayıklama modunda Hello örnek uygulamayı çalıştırın

```bash
gulp run --debug
```

Merhaba hata ayıklama altyapı hazır olduktan sonra mümkün toosee olmalıdır ```Debugger listening on port 5858``` hello konsol çıktısından.

### <a name="configure-vs-code-tooconnect-toohello-remote-device"></a>VS Code'da tooconnect toohello uzak aygıt yapılandırma

Açık hello **hata ayıklama** hello yan sol panelden.

Merhaba yeşil tıklatın **hata ayıklamayı Başlat** (F5) düğmesi. VS Code açmak bir **Launch.json'u** dosyası, hangi tooupdate gerekir.

Güncelleştirme hello **Launch.json'u** aşağıdaki hello ile içerik dosya getirin, yerine `[device hostname or IP address]` hello gerçek cihazı IP adresi veya ana bilgisayar adı.  

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

![Uzaktan hata ayıklama yapılandırması](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a>Toohello uzak uygulama ekleme

Merhaba yeşil tıklatın **hata ayıklamayı Başlat** (F5) düğmesine tıklayın ve hata ayıklama keyfini çıkarın.

Okuyabilirsiniz [JavaScript VS code'da](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn hello hata ayıklayıcı hakkında daha fazla.

![Uzaktan etkileşimli hata ayıklama](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a>Azure CLI sorunları
Hello Azure komut satırı arabirimi (Azure CLI) önizleme yapıdır. Merhaba çözümde arayın [Önizleme Yükleme Kılavuzu](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek çözümler. Komutları beklendiği gibi çalışmıyor olduğunda tooupgrade Azure CLI toolatest sürümünü deneyin.

Tüm hatalar hello aracı ile karşılaşırsanız, dosya bir [sorunu](https://github.com/Azure/azure-cli/issues) hello içinde **sorunları** hello GitHub deposuna bölümü.

Sık karşılaşılan sorunları gidermede yardım için hello denetleyin [Benioku](https://github.com/Azure/azure-cli/blob/master/README.rst).

"Merhaba gereksinimini karşılayan bir sürüm bulunamadı", lütfen karşılıyorsa çalışma hello aşağıdaki tooupgrade PIP toolastest sürüm komutu.

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a>Python yükleme sorunları
### <a name="legacy-installation-issues-macos"></a>Eski yükleme sorunları (macOS)
Ne zaman yüklüyorsanız **PIP**, eski paketleri olduğunda izin hatası atılır ile birlikte yüklenen **su** izinleri. Python brew (macOS) kullanarak önceki bir yüklemesini tümüyle kaldırılmamış. Bu durum oluşur. Bazı **PIP** önceki bir yükleme paketi hello izni hatasına neden oluyor kök tarafından oluşturulmuş. Merhaba çözüm tooremove bu paketleri kök tarafından yüklü değil. Aşağıdaki adımları toocomplete hello bu görevi kullanın:

1. Gidin: /usr/local/lib/python2.7/site-packages
2. Liste paketleri kök tarafından oluşturun:`ls -l | grep root`
3. Paketler, adım 2 ' Kaldır:`sudo rm -rf {package name}`
4. Python yeniden yükleyin.

## <a name="azure-iot-hub-issues"></a>Azure IOT hub'ı sorunları
Başarılı bir şekilde Azure IOT hub'ınıza sağladığınız varsa `azure-cli`, ve tooyour IOT hub'ı deneyin hello araçları aşağıdaki bağlanan bir aracı toomanage hello aygıtlarının gerekir:

### <a name="device-explorer"></a>Cihaz Gezgini
[Cihaz Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) Windows yerel makinenizde çalıştırır ve azure'da tooyour IOT hub'ı bağlar. Merhaba aşağıdaki ile iletişim kurar [IOT Hub uç noktaları](iot-hub-devguide.md):

- _Cihaz Kimlik Yönetimi_ tooprovision ve IOT hub'ınıza kayıtlı cihazları yönetme.
- _Cihaz bulut alma_ aygıt tooyour IOT hub'dan gönderilen iletileri izleyebilmek.
- _Bulut cihaz Gönder_ IOT hub'ından tooyour aygıtları iletileri gönderebilmesi.

Yapılandırma, `IoT hub connection string` bu aracı toouse içindeki tüm özellikleri.

### <a name="iot-hub-explorer"></a>IOT hub'ı Gezgini
[IOT hub'ı Explorer](https://github.com/Azure/iothub-explorer) bir örnek çok platformlu CLI toomanage aygıt istemcileri aracıdır. Merhaba kimlik kayıt defterinde hello aracı toomanage hello aygıtları'nı kullanın, cihaz bulut iletilerini izlemek ve bulut cihaza komut gönderme.

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
[Microsoft Azure Storage Gezgini (Önizleme)](http://storageexplorer.com) toowork ile kullanabileceğiniz Microsoft tek başına uygulamadır [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) Windows, macOS ve Linux veri. Bu aracı kullanarak tooyour tablo bağlanabilir ve hello verilerde bakın. Bu aracı tootroubleshoot Azure depolama sorunlarınızı kullanabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
Bu sayfa yalnızca Intel Edison'u Seti'nin hello en yaygın sorunları içerir. Bu gibi durumlarda, alt açıklamaları da daha fazla sorun giderme için tooreport sorunları bırakabilirsiniz.

Çok dön[Intel Edison'u (Node.js) ile çalışmaya başlama](iot-hub-intel-edison-kit-node-get-started.md)

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-node-edison-getting-started