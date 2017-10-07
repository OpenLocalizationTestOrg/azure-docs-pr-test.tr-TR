---
title: "aaaIoT DevKit toocloud - bağlanmak IOT DevKit AZ3166 tooAzure IOT hub'ı | Microsoft Docs"
description: "Bilgi nasıl toosetup ve onun için IOT DevKit AZ3166 tooAzure IOT hub'ı Bu öğreticide toosend veri toohello Azure bulut platformu bağlanın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: xshi
ms.openlocfilehash: fd36abaed1fd9f73028b84312bca9e900fb9c004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-iot-devkit-az3166-tooazure-iot-hub-in-hello-cloud"></a>IOT DevKit AZ3166 tooAzure IOT Hub'hello bulutta Bağlan

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

Merhaba [MXChip IOT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) kullanılan toodevelop ve prototip Microsoft Azure hizmetlerini yararlanarak nesnelerin interneti (IOT) çözümleri olabilir. Zengin çevre algılayıcılar, bir açık kaynak tablosu paketi ve bir büyüyen bir Arduino uyumlu panosuna içeren [projeleri katalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).

## <a name="what-you-do"></a>Neler
Bağlantı [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) tooan Azure IOT hub oluşturma, toplama hello sıcaklık ve nem verilerden algılayıcılar ve hello veri tooIoT hub gönderin.

Bir DevKit henüz yok mu? Yeni bir tane almak [burada](https://aka.ms/iot-devkit-purchase).

## <a name="what-you-learn"></a>Öğrenecekleriniz

* Nasıl tooconnect IOT DevKit tooWireless erişim noktası ve geliştirme ortamınızı hazırlayın.
* Nasıl toocreate IOT hub'ı ve MXChip IOT DevKit için kaydedilecek.
* Nasıl MXChip IOT DevKit üzerinde bir örnek uygulamayı çalıştırarak toocollect algılayıcı verileri.
* Nasıl toosend algılayıcı verileri tooyour IOT hub'ı hello.

## <a name="what-you-need"></a>Ne gerekiyor

* MXChip IOT DevKit kartı mikro USB kablosu ile. [Şimdi alın](https://aka.ms/iot-devkit-purchase)
* Windows 10 veya macOS 10.10 + çalıştıran bir bilgisayar
* Etkin bir Azure aboneliği
  * Etkinleştirme bir [Ücretsiz 30 günlük deneme Microsoft Azure hesabı](https://azureinfo.microsoft.com/us-freetrial.html)

## <a name="prepare-your-hardware"></a>Donanımınızın hazırlama

Merhaba donanım tooyour bilgisayarı takma.

### <a name="hardware-you-need"></a>Gereksinim duyduğunuz donanım

* DevKit Panosu
* Mikro USB kablosu

![alma başlatıldı-donanım](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

### <a name="connect-devkit-tooyour-computer"></a>DevKit tooyour bilgisayara bağlanma

1. USB son tooyour PC Bağlan
2. Mikro USB son toohello DevKit Bağlan
3. bağlantı Hello yeşil LED sonraki toopower onaylar

![alma-başlatıldı-Bağlan](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wifi"></a>WiFi yapılandırın

IOT projelerinin Internet bağlantısı kullanır. Aşağıdaki yönergeler tooconfigure hello DevKit tooconnect tooWiFi hello kullanın.

### <a name="enter-ap-mode"></a>AP modu girin

B düğmesini basılı tutun, ardından itme ve yayın hello düğmesine, ardından yayın düğmesi b sıfırlama DevKit WiFi yapılandırmak için AP moduna girer. Merhaba ekranında hello hizmet ayarlamak Identifier(SSID) hello DevKit, ve bunun yanı sıra hello yapılandırma portalı IP adresini görüntüler:

![alma-başlatıldı-wifi-ap](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-toodevkit-ap"></a>TooDevKit AP Bağlan

Şimdi, başka bir etkin WiFi aygıt (PC veya cep telefonu) tooconnect toohello DevKit (yukarıdaki hello ekran görüntüsünde vurgulanan) SSID kullanın, hello parola boş bırakın.

![alma-başlatıldı-SSID](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wifi-for-devkit"></a>WiFi DevKit için yapılandırma

PC veya cep telefonu tarayıcı hello DevKit ekranda gösterilen açık hello IP adresi hello DevKit tooconnect istediğiniz hello WiFi ağı seçin ve ardından hello parolayı yazın. Tıklatın **Bağlan** toocomplete:

![alma başlatıldı-wifi-portal](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

Merhaba DevKit Hello bağlantı başarılı olduktan sonra birkaç saniye içinde yeniden başlatılır. Başarılı olursa Merhaba ekranında hello WiFi adı ve IP adresi görürsünüz:

![alma başlatıldı-wifi-IP](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
Merhaba fotoğraf görüntülenen başlangıç IP adresi atanır ve hello DevKit ekranda görüntülenen hello gerçek IP eşleşmeyebilir. Bu DHCP toodynamically atamak IP'leri WiFi kullandıkça normaldir.

WiFi yapılandırıldıktan sonra kimlik bilgilerinizi hello cihazda Bu bağlantı için takılı olsa bile kalıcı. Merhaba DevKit evinizde WiFi için yapılandırılmış ve hello DevKit toohello office sürdü, örneğin, tooreconfigure AP modu gerekir (adım başlangıç **girin AP modu**) tooconnect hello DevKit tooyour office WiFi. 

## <a name="start-using-devkit"></a>DevKit kullanmaya başlama

DevKit üzerinde çalışan hello varsayılan uygulama hello son hello bellenim sürümünü denetleyin ve sizin için bazı algılayıcı tanılama verilerini görüntüler.

### <a name="upgrade-toohello-latest-firmware"></a>Toohello en son bellenim yükseltme

Gerekli bir yükseltme ise her ikisi de geçerli ve en son bellenim sürümünü hello Merhaba ekranında istenir. İzleyin [yükseltme bellenim](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) Kılavuzu tooupgrade onu.

![alma-başlatıldı-üretici yazılımı](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
Bu DevKit hello üzerinde geliştirme başladıktan sonra bir kerelik çaba ve uygulamanızı karşıya yükleme, uygulamanız ile gelen hello son üretici yazılımına sahip olur.

### <a name="test-various-sensors"></a>Çeşitli algılayıcılar test

Düğmesi B tootest algılayıcılar tuşlarına basın, tuşuna basarak ve her algılayıcı hello B düğmesi toocycle serbest devam eder.

![alma-başlatıldı-algılayıcılar](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-development-environment"></a>Geliştirme ortamını hazırlayın

Şimdi zaman tooset hello geliştirme ortamını ayarlama: araçlar ve IOT uygulamaları şaşırtıcı toobuild paketleri. Windows veya macOS sürüm tooyour işletim sistemine göre seçebilirsiniz.


### <a name="windows"></a>Windows

Toouse hello yükleme paketini tooprepare hello geliştirme ortamı öneririz. Herhangi bir sorunla karşılaşırsanız, hello izleyebilirsiniz [el ile yapılacak adımlar](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget bu yapılır.

#### <a name="download-latest-package"></a>Son paketini indirin

Merhaba `.zip` karşıdan dosya tüm gerekli araçları ve DevKit geliştirme için gerekli paketleri içerir.

> [!div class="button"]
[İndir](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


> [!NOTE] 
> Merhaba `.zip` dosyasını içeren hello aşağıdaki araçları ve paketleri. Bazı bileşenleri yüklü zaten varsa, hello betik algılamak ve onları atlayın.
> * Node.js ve Yarn: hello Kurulum komut dosyası ve otomatik görevler için çalışma zamanı
> * [Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) -Azure kaynaklarını, hello MSI yönetmek için platformlar arası komut satırı deneyimi bağımlı Python ve PIP içerir.
> * [Visual Studio Code](https://code.visualstudio.com/): DevKit geliştirme için basit Kod Düzenleyicisi
> * [Visual Studio Code uzantısı Arduino için](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): VS code'da sağlayan Arduino geliştirme
> * [Arduino IDE](https://www.arduino.cc/en/Main/Software): hello uzantısı Arduino için bu aracı üzerinde kullanır
> * DevKit Panosu paketi: zincirleri, kitaplıklar ve hello DevKit projelerde aracı
> * ST bağlantı yardımcı programı: Gerekli yardımcı programları ve sürücüleri

#### <a name="run-installation-script"></a>Yükleme komut dosyasını çalıştır

Windows dosya Gezgini'nde hello bulun `.zip` ve ayıklayın, Bul `install.cmd`seçin ve sağ tıklatıp **"Yönetici olarak çalıştır"** toostart.

![alma başlatıldı-Çalıştır-yönetici](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

Yükleme sırasında her aracı veya paket hello ilerlemesini görürsünüz.

![alma başlatıldı-yükleme](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="confirm-tooinstall-drivers"></a>Tooinstall sürücüleri onaylayın

Merhaba VS Code Arduino uzantısı hello Arduino IDE üzerinde kullanır. Bu hello hello Arduino IDE yüklediğiniz ilk kez kullanıyorsanız, istendiğinde tooinstall ilgili sürücüleri olacaktır:

![alma başlatıldı-sürücü](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

Internet hızınıza bağlı olarak toofinish yükleme yaklaşık 10 dakika sürer. Merhaba yüklemesi tamamlandıktan sonra masaüstünüzde Visual Studio Code ve Arduino IDE kısayolları görmeniz gerekir.

> [!NOTE] 
Bazen, VS Code'u başlatın, Arduino IDE veya ilgili Panosu paketi bulamıyor bir hata ile istenir. Kapat VS Code'u başlatın Arduino IDE kez toosolve ve VS Code Arduino IDE yolu doğru bulun.


### <a name="macos-preview"></a>macOS (Önizleme)

Bu adımları tooprepare geliştirme ortamı macOS üzerinde izleyin.

#### <a name="install-azure-cli-20"></a>Azure CLI 2.0’ı yükleme

Merhaba izleyin [resmi Kılavuzu](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall Azure CLI 2.0:

Azure CLI 2.0 yüklemek `curl` komutu:

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

Ve değişiklikleri tootake etkisi, komut kabuğu yeniden başlatın:

```bash
exec -l $SHELL
```

#### <a name="install-arduino-ide"></a>Arduino IDE yükleyin

Visual Studio kod Arduino uzantısı Hello hello Arduino IDE üzerinde kullanır. Merhaba yükleyip [macOS Arduino IDE](https://www.arduino.cc/en/Main/Software).

#### <a name="install-visual-studio-code"></a>Visual Studio Kodu'nu yükle

İndirme ve yükleme [macOS için Visual Studio Code](https://code.visualstudio.com/). Bu DevKit IOT uygulamaları oluşturmak için hello birincil geliştirme aracı olacaktır.

####  <a name="download-latest-package"></a>Son paketini indirin

1. Node.js yükleyin. Popüler macOS Paket Yöneticisi'ni kullanabilirsiniz [Homebrew](https://brew.sh/) veya [yükleyici önceden oluşturulmuş](https://nodejs.org/en/download/) tooinstall onu.

2. Karşıdan `.zip` VS Code DevKit geliştirme için gerekli görev komut dosyalarını içeren dosya.

   > [!div class="button"]
   [İndir](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

   Merhaba bulun `.zip` ve ayıklayın. Ardından başlatma **Terminal** uygulama ve komutları tooconfigure aşağıdaki çalışma hello:

   Ayıklanan klasörü tooyour macOS kullanıcı klasörü Taşı:
   ```bash
   mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
   ```
  
   Yükleme `npm` paketler:
   ```
   npm install
   ```

#### <a name="install-vs-code-extension-for-arduino"></a>VS Code uzantısını Arduino için yükleyin

Visual Studio Code verir tooinstall Market uzantıları doğrudan hello aracında, yalnızca hello soldaki menüden bölmesinde hello uzantıları simgesine tıklayın ve ardından arama `Arduino` tooinstall:

![Uzantıları Yükleme](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-devkit-board-package"></a>DevKit Panosu paketini yükle

Visual Studio kodda hello Panosu Yöneticisi'ni kullanarak tooadd hello DevKit Panosu gerekir.

1. Kullanım `Cmd+Shift+P` tooinvoke komutu paleti ve türü **Arduino** ardından bulmak ve seçmek **Arduino: Panosu Yöneticisi**.

2. Tıklatın **'Ek URL'ler'** sağ hello altındaki.
   ![Yükleme ek-URL'leri](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)

3. Merhaba, `settings.json` dosya, hello alt kısmında bir satır ekleyin `USER SETTINGS` bölmesi ve kaydedin.
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![yükleme ayarları json](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. Şimdi 'az3166 için' hello Panosu Yöneticisi'ni arayın ve hello en son sürümünü yükleyin.
   ![Yükleme az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)

Artık tüm hello gereken araçları ve macOS için yüklü olan paketleri vardır.


## <a name="open-project-folder"></a>Proje Aç klasörü

### <a name="launch-vs-code"></a>VS Code’u başlatın

DevKit bağlı emin olun. İlk VS Code'u başlatın ve hello DevKit tooyour bilgisayara bağlanın. VS Code otomatik olarak bulmak ve ayarlama giriş sayfası açılır:

![Mini solution vscode](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
Bazen, VS Code'u başlatın, Arduino IDE veya ilgili Panosu paketi bulunamadı hatasıyla istenir. Kapat VS Code'u başlatın Arduino IDE yeniden toosolve ve VS Code Arduino IDE yolu doğru bulun.

### <a name="open-arduino-examples-folder"></a>Arduino örnekler Klasör Aç

Çok geçiş**'Arduino örnekler'** sekmesinde, çok gidin`Examples for MXCHIP AZ3166 > AzureIoT` ve tıklayın `GetStarted`.

![Mini solution örnekleri](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

Tooclose hello bölmesini görülüyorsa tooreload, kullanım `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke komutu paleti ve türü **Arduino** toofind seçip **Arduino: örnekler**.

## <a name="provision-azure-services"></a>Azure hizmetlerini hazırlamanız

Görevinizi Hello çözüm penceresinde çalıştırın `Ctrl+P` (macOS: `Cmd+P`) 'bulut sağlama görev' yazarak:

Hello VS Code etkileşimli bir komut satırı sağlama hello yönlendirecek terminal Azure Hizmetleri gereklidir:

![Mini-solution-bulut-sağlama](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-arduino-sketch"></a>Derleme ve Arduino taslak karşıya yükle

### <a name="install-required-library"></a>Gerekli kitaplığını yükle

1. Tuşuna `F1` veya `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke komutu paleti ve türü **Arduino** ardından bulmak ve seçmek **Arduino: Kitaplığı Yöneticisi**.

2. Arama `ArduinoJson` kitaplığı ve tıklatın **yükleyin**

### <a name="build-and-upload-hello-device-code"></a>Derleme ve hello aygıt kodu karşıya yükle

Kullanım `Ctrl+P` (macOS: `Cmd+P`) toorun 'görev aygıt-karşıya yükleme'. Merhaba terminal, tooenter yapılandırma modu ister. toodo, bu nedenle, A düğmesini basılı tutun, ardından itme ve yayın hello Sıfırla düğmesi. 'Configuration' Başlangıç ekranı görüntüler. 'Görev bulut-provision' adımından alır tooset hello bağlantı dizesi budur.

Ardından doğrulama ve hello Arduino taslak karşıya yükleme başlar:

![Mini-solution aygıt-karşıya yükleme](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

Merhaba DevKit yeniden başlatın ve hello kodu çalıştırma başlatın.

## <a name="test-hello-project"></a>Test hello projesi

VS Code'da hello durum çubuğu tooopen hello seri İzleyicisi Merhaba güç Tak simgesine tıklayın.

sonuçları aşağıdaki hello gördüğünüzde hello örnek uygulama başarıyla çalıştırma:

* Merhaba seri İzleyici görüntüler hello ekran görüntüsü hello içeriği aynı bilgileri hello.
* Merhaba LED MXChip IOT DevKit üzerinde yanıp sönen.

![VS code'da son çıktı](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a>Sorunları ve geri bildirim

Bulabileceğiniz [SSS](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) sorunlarla ya da kanalları hello aşağıdaki toous ulaşın.

## <a name="next-steps"></a>Sonraki adımlar

MXChip IOT DevKit tooyour IOT hub'ı başarıyla bağlandı ve gönderilen hello algılayıcı verileri tooyour IOT hub'ı yakalanan.

Başlarken toocontinue IOT Hub ve tooexplore diğer IOT senaryolarını bakın:

- [iothub-explorer ile bulut cihaz mesajlaşmasını yönetme](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [IOT hub'ı iletileri tooAzure veri depolama Kaydet](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [Power BI toovisualize gerçek zamanlı algılayıcı verileri Azure IOT hub'ı kullanın](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [Azure Web Apps toovisualize gerçek zamanlı algılayıcı verileri Azure IOT hub'ı kullanın](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [IOT hub'ınızı hello algılayıcı verilerini Azure Machine Learning kullanarak hava durumu tahmini](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [iothub-explorer ile cihaz yönetimi](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- [Logic Apps ile uzaktan izleme ve bildirimler](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps)