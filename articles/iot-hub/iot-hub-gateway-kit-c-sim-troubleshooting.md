---
title: "Benzetimli cihaz & Azure IOT ağ geçidi - sorunlarını giderme | Microsoft Docs"
description: "Sayfa Intel NUC ağ geçidi için sorun giderme"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IOT sorunları, Internet şeyler sorunları"
ROBOTS: NOINDEX
ms.assetid: 3ee8f4b0-5799-40a3-8cf0-8d5aa44dbc2b
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: cc7add6273e66aadeca9a4915a44f5edf61a0a59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Sorun giderme

## <a name="hardware-issues"></a>Donanım sorunları

### <a name="ti-sensortag-cannot-be-connected"></a>TI SensorTag bağlı

tootroubleshoot SensorTag bağlantı sorunları, hello kullan [SensorTag uygulama](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).

### <a name="have-an-issue-with-intel-nuc"></a>Intel NUC ile ilgili bir sorun olması

tootroubleshoot önyükleme sorunlarını başvurmak çok[Intel NUC üzerinde Hayır önyükleme sorunlarını giderme](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).

tootroubleshoot işletim sistemi sorunları başvurmak çok[Intel NUC üzerinde işletim sistemi sorunlarını giderme](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).

tootroubleshoot diğer sorunlar başvurmak çok[Blink kodları ve Intel NUC kodları bip sesi](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).

## <a name="nodejs-package-issues"></a>Node.js paket sorunları

### <a name="no-response-during-gulp-tasks"></a>Gulp görevler sırasında yanıt yok

Çalışan gulp görevleri sorunlarla karşılaşırsanız, hello ekleyebilirsiniz `--verbose` hata ayıklama seçeneği. Tooterminate geçerli gulp görevleri kullanarak deneyin `Ctrl + C`, ve ardından çalışma hello aşağıdaki konsol penceresi toosee hata ayıklama iletileri komutu. Ayrıntılı hata iletileri, konsol çıktısı görebilirsiniz.

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a>Aygıt Bulma sorunları

İlgili hello ortak sorunları gidermede yardım için `discover-sensortag` komutu, hello denetleyin [wiki sayfa](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).

### <a name="npm-issues"></a>npm sorunları

Tooupdate hello aşağıdaki komutu çalıştırarak npm paket deneyin:

```bash
npm install -g npm
```

Merhaba sorun devam ederse, bu makalenin hello sonunda yorumlarınızı bırakın veya bir GitHub sorunu oluşturmak bizim [örnek depo](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).

## <a name="remote-debugging"></a>Uzaktan hata ayıklama
> Bu öğreticide kullanılan node.js komut hata ayıklama için aşağıdaki yönergeleri yöneliktir.
### <a name="run-hello-sample-application-in-debug-mode"></a>Hata ayıklama modunda Hello örnek uygulamayı çalıştırın

Merhaba örnek uygulaması hello aşağıdaki komutu çalıştırarak hata ayıklama modunda çalıştırın:

```bash
gulp run --debug
```

Merhaba hata ayıklama altyapısı hazır olduğunda, görmelisiniz `Debugger listening on port 5858` hello konsol çıkışı.

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a>Visual Studio Code tooconnect toohello uzak aygıt yapılandırma

1. Açık hello **hata ayıklama** hello yan sol panelde.
2. Merhaba yeşil tıklatın **hata ayıklamayı Başlat** (F5) düğmesi. Visual Studio Code açılır bir `launch.json` dosyası.
3. Güncelleştirme hello `launch.json` içeriği aşağıdaki hello dosyasıyla. Değiştir `[device hostname or IP address]` Merhaba, gerçek cihaz IP adresi veya ana bilgisayar adı ile.

   ``` json
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
            "remoteRoot": "~/ble_sample"
        }
     ]
   }
   ```

![Uzaktan hata ayıklama yapılandırması](./media/iot-hub-gateway-kit-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a>Toohello uzak uygulama ekleme

Merhaba yeşil tıklatın **hata ayıklamayı Başlat** (F5) düğmesini toostart hata ayıklama.

Okuma [JavaScript VS code'da](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn hello hata ayıklayıcı hakkında daha fazla.

![Hata ayıklama bırak örnek](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a>Azure CLI sorunları

Hello Azure komut satırı arabirimi (Azure CLI) önizleme yapıdır. tooseek çözümleri hello kullanabilir [Önizleme Yükleme Kılavuzu](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).

Tüm hatalar hello aracı ile karşılaşırsanız, dosya bir [sorunu](https://github.com/Azure/azure-cli/issues) hello içinde **sorunları** hello GitHub deposuna bölümü.

Sık karşılaşılan sorunları giderme konusunda yardım için hello denetleyin [Benioku](https://github.com/Azure/azure-cli/blob/master/README.rst).

"Merhaba gereksinimini karşılayan bir sürüm bulunamadı", lütfen karşılıyorsa çalışma hello aşağıdaki tooupgrade PIP toolastest sürüm komutu.

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a>Python yükleme sorunları

### <a name="legacy-installation-issues-macos"></a>Eski yükleme sorunları (macOS)

PIP yüklüyorsanız, eski paketleri ile yüklendiğinde izin hatası atılır **su** izinleri. Python brew (macOS) kullanarak önceki bir yüklemesini tümüyle kaldırılmamış. Bu durum oluşur. Önceki yüklemeye ait bazı PIP paketler hello izni hatasına neden oluyor kök tarafından oluşturuldu. Merhaba çözüm tooremove bu paketleri kök tarafından yüklü değil. Aşağıdaki adımları toocomplete hello bu görevi kullanın:

1. Çok gidin`/usr/local/lib/python2.7/site-packages`
2. Kök tarafından oluşturulan listesi paketler:`ls -l | grep root`
3. Paketler, adım 2 ' Kaldır:`sudo rm -rf {package name}`
4. Python yeniden yükleyin.

## <a name="azure-iot-hub-issues"></a>Azure IOT hub'ı sorunları

Hello Azure CLI ile Azure IOT hub'ınızı başarıyla kaynak sağlandı ve tooyour IOT hub'a bağlanan bir aracı toomanage hello aygıtları ihtiyacınız varsa araçları aşağıdaki hello deneyin.

### <a name="device-explorer"></a>Cihaz Gezgini

[Cihaz Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) Windows yerel makinenizde çalıştırır ve azure'da tooyour IOT hub'ı bağlar. Merhaba aşağıdaki ile iletişim kurar [IOT Hub uç noktaları](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):

- Cihaz Kimlik Yönetimi tooprovision ve IOT hub'ınıza kayıtlı cihazları yönetme.
- Cihaz bulut alır, böylece cihaz tooyour IOT hub'dan gönderilen iletileri izleyebilirsiniz.
- IOT hub'ından tooyour aygıtları iletileri gönderebilmesi bulut cihaz gönderin.

IOT hub bağlantı dizenizi bu aracı toouse içindeki tüm özelliklerini yapılandırın.

### <a name="iothub-explorer"></a>ıothub Gezgini

[ıothub explorer](https://github.com/Azure/iothub-explorer) bir örnek çok platformlu CLI toomanage aygıt istemcileri aracıdır. Merhaba kimlik kayıt defterinde hello aracı toomanage hello aygıtları'nı kullanın, cihaz bulut iletilerini izlemek ve bulut cihaza komut gönderme.

(tooinstall hello en son ön) sürümünü hello ıothub explorer aracı, hello aşağıdaki komutu çalıştırın:

```bash
npm install -g iothub-explorer@latest
```

Tüm hakkında ek Yardım tooget iothub-explorer komutlar ve bunların parametrelerini Merhaba, hello aşağıdaki komutu çalıştırın:

```bash
iothub-explorer help
```

### <a name="hello-azure-portal"></a>Hello Azure portalı

Tam CLI deneyimi oluşturma ve Azure kaynaklarınızı yönetmenize yardımcı olur. Toouse hello isteyebilirsiniz [Azure portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp sağlamanıza, yönetmek ve Azure kaynaklarınızı hata ayıklama.

## <a name="azure-storage-issues"></a>Azure depolama sorunları

[Microsoft Azure Storage Gezgini (Önizleme)](http://storageexplorer.com/) toowork Windows, macOS ve Linux Azure Storage veri ile kullanabileceğiniz Microsoft tek başına uygulamadır. Bu aracı kullanarak tooyour tablo bağlanabilir ve hello verilerde bakın. Bu aracı tootroubleshoot Azure depolama sorunlarınızı kullanabilirsiniz.
