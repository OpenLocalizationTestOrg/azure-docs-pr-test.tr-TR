---
title: "Bulut için - IOT DevKit IOT DevKit AZ3166 Azure IOT Hub'ına bağlanmak | Microsoft Docs"
description: "Kurulum ve Bu öğreticide Azure bulut platformuna veri göndermek için Azure IOT Hub için bu IOT DevKit AZ3166 bağlanma hakkında bilgi edinin."
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
ms.openlocfilehash: 122fac584ac5b954ef7b33a3121bee2c502ebc63
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-iot-devkit-az3166-to-azure-iot-hub-in-the-cloud"></a>Bulutta Azure IOT Hub'ına IOT DevKit AZ3166 Bağlan

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

[MXChip IOT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) geliştirmek için kullanılan ve Microsoft Azure hizmetlerini yararlanarak prototip nesnelerin interneti (IOT) çözümler. Zengin çevre algılayıcılar, bir açık kaynak tablosu paketi ve bir büyüyen bir Arduino uyumlu panosuna içeren [projeleri katalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).

## <a name="what-you-do"></a>Neler
Bağlantı [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) , oluşturduğunuz bir Azure IOT hub'ına sıcaklık ve nem veri algılayıcı verilerini toplar ve IOT hub'ına gönderir.

Bir DevKit henüz yok mu? Yeni bir tane almak [burada](https://aka.ms/iot-devkit-purchase).

## <a name="what-you-learn"></a>Öğrenecekleriniz

* Nasıl IOT DevKit kablosuz erişim noktasına bağlanmak ve geliştirme ortamınızı hazırlayın.
* IOT hub'ı oluşturma ve MXChip IOT DevKit için bir cihaz kaydetme hakkında.
* Örnek bir uygulama üzerinde MXChip IOT DevKit çalıştırarak algılayıcı verilerini toplamak nasıl.
* IOT hub'ınıza algılayıcı verileri göndermek nasıl.

## <a name="what-you-need"></a>Ne gerekiyor

* MXChip IOT DevKit kartı mikro USB kablosu ile. [Şimdi alın](https://aka.ms/iot-devkit-purchase)
* Windows 10 veya macOS 10.10 + çalıştıran bir bilgisayar
* Etkin bir Azure aboneliği
  * Etkinleştirme bir [Ücretsiz 30 günlük deneme Microsoft Azure hesabı](https://azureinfo.microsoft.com/us-freetrial.html)

## <a name="prepare-your-hardware"></a>Donanımınızın hazırlama

Donanım bilgisayarınıza bağlayın.

### <a name="hardware-you-need"></a>Gereksinim duyduğunuz donanım

* DevKit Panosu
* Mikro USB kablosu

![alma başlatıldı-donanım](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

### <a name="connect-devkit-to-your-computer"></a>DevKit bilgisayarınıza bağlayın

1. USB son PC'nize bağlayın
2. Mikro USB son DevKit Bağlan
3. Bağlantı Güç yanındaki yeşil LED onaylar

![alma-başlatıldı-Bağlan](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wifi"></a>WiFi yapılandırın

IOT projelerinin Internet bağlantısı kullanır. WiFi için bağlanmak için DevKit yapılandırmak için aşağıdaki yönergeleri kullanın.

### <a name="enter-ap-mode"></a>AP modu girin

B düğmesini basılı tutun itme ve Sıfırla düğmesini bırakın, sonra düğmesini B. bırakın DevKit WiFi yapılandırmak için AP moduna girer. Ekran hizmet ayarlamak Identifier(SSID) DevKit yanı sıra yapılandırma portalı IP adresini görüntüler:

![alma-başlatıldı-wifi-ap](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-to-devkit-ap"></a>DevKit AP Bağlan

Şimdi, başka bir WiFi Etkin aygıt (PC veya cep telefonu) (yukarıdaki ekran görüntüsünde vurgulanan) DevKit SSID bağlanmak için parolayı boş bırakın kullanın.

![alma-başlatıldı-SSID](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wifi-for-devkit"></a>WiFi DevKit için yapılandırma

PC veya cep telefonu tarayıcınız DevKit ekranda gösterilen IP adresini açın, bağlanmak için DevKit WiFi ağı seçin ve sonra parolayı yazın. Tıklatın **Bağlan** tamamlamak için:

![alma başlatıldı-wifi-portal](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

Bağlantı başarılı olduktan sonra DevKit birkaç saniye içinde yeniden başlatılır. Başarılı olursa WiFi adı ve IP adresi ekranda görürsünüz:

![alma başlatıldı-wifi-IP](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
Fotoğrafın görüntülenen IP adresi atanır ve DevKit ekranda görüntülenen gerçek IP eşleşmeyebilir. WiFi IP'leri dinamik olarak atamak için DHCP kullanır, bu normaldir.

WiFi yapılandırıldıktan sonra kimlik bilgilerinizi bu bağlantı için cihazda takılı olsa bile kalıcı. Örneğin, DevKit evinizde WiFi için yapılandırılmış ve ardından DevKit ofise sürdü, AP modu yeniden yapılandırmanız gerekecektir (adımda başlangıç **girin AP modu**), office WiFi DevKit bağlanmak için. 

## <a name="start-using-devkit"></a>DevKit kullanmaya başlama

DevKit üzerinde çalışan varsayılan uygulama en son bellenim sürümünü denetleyin ve sizin için bazı algılayıcı tanılama verilerini görüntüler.

### <a name="upgrade-to-the-latest-firmware"></a>En son bellenim yükseltme

Bir yükseltme ise hem geçerli ve en son bellenim sürümünü gerekli ekranda istenir. İzleyin [yükseltme bellenim](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) Yükseltme Kılavuzu.

![alma-başlatıldı-üretici yazılımı](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
Bu DevKit üzerinde geliştirme başladıktan sonra bir kerelik çaba ve uygulamanızı karşıya yükleme, uygulamanızla gelen en son üretici yazılımına sahip olur.

### <a name="test-various-sensors"></a>Çeşitli algılayıcılar test

Algılayıcılar test, tuşuna basarak ve her algılayıcı arasında geçiş yapmak için B düğmesini bırakmadan devam etmek için B düğmesine basın.

![alma-başlatıldı-algılayıcılar](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-development-environment"></a>Geliştirme ortamını hazırlayın

Geliştirme ortamını ayarlama şimdi: araçlar ve etkileyici IOT uygulamalar oluşturmanızı paketleri. Windows veya macOS sürüm işletim sisteminize göre seçebilirsiniz.


### <a name="windows"></a>Windows

Geliştirme ortamı hazırlamak için yükleme paketi kullanmanızı öneririz. Herhangi bir sorunla karşılaşırsanız, takip edebilirsiniz [el ile yapılacak adımlar](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) bitti elde edin.

#### <a name="download-latest-package"></a>Son paketini indirin

`.zip` Karşıdan dosya tüm gerekli araçları ve DevKit geliştirme için gerekli paketleri içerir.

> [!div class="button"]
[İndir](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


> [!NOTE] 
> `.zip` Dosyası aşağıdaki araçları ve paketleri içerir. Bazı bileşenleri yüklü zaten varsa, betik algılamak ve onları atlayın.
> * Node.js ve Yarn: otomatik görevler ve Kurulum komut dosyası için çalışma zamanı
> * [Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) -platformlar arası komut satırı deneyimi Azure kaynaklarını yönetmek için MSI bağımlı Python ve PIP içerir.
> * [Visual Studio Code](https://code.visualstudio.com/): DevKit geliştirme için basit Kod Düzenleyicisi
> * [Visual Studio Code uzantısı Arduino için](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): VS code'da sağlayan Arduino geliştirme
> * [Arduino IDE](https://www.arduino.cc/en/Main/Software): Bu araç hakkında Arduino uzantısı kullanır
> * DevKit Panosu paketi: Aracı zincirleri, kitaplıklar ve DevKit projeleri
> * ST bağlantı yardımcı programı: Gerekli yardımcı programları ve sürücüleri

#### <a name="run-installation-script"></a>Yükleme komut dosyasını çalıştır

Windows dosya Gezgini'nde bulun `.zip` ve ayıklayın, Bul `install.cmd`seçin ve sağ tıklatıp **"Yönetici olarak çalıştır"** başlatmak için.

![alma başlatıldı-Çalıştır-yönetici](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

Yükleme sırasında her aracı veya paket ilerlemesini görürsünüz.

![alma başlatıldı-yükleme](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="confirm-to-install-drivers"></a>Sürücüleri yüklemek için Onayla

VS Code'da Arduino uzantısı Arduino IDE üzerinde kullanır. Arduino IDE yüklediğiniz ilk kez kullanıyorsanız, ilgili sürücüleri yüklemeniz istenir:

![alma başlatıldı-sürücü](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

Internet hızınıza bağlı olarak yüklemeyi tamamlamak için yaklaşık 10 dakika sürer. Yükleme tamamlandıktan sonra masaüstünüzde Visual Studio Code ve Arduino IDE kısayolları görmeniz gerekir.

> [!NOTE] 
Bazen, VS Code'u başlatın, Arduino IDE veya ilgili Panosu paketi bulamıyor bir hata ile istenir. Çözmek VS Code kapatmak için bir kez Arduino IDE başlatma ve VS Code Arduino IDE yolu doğru bulun.


### <a name="macos-preview"></a>macOS (Önizleme)

MacOS geliştirme ortamında hazırlamak için aşağıdaki adımları izleyin.

#### <a name="install-azure-cli-20"></a>Azure CLI 2.0’ı yükleme

İzleyin [resmi Kılavuzu](https://docs.microsoft.com//cli/azure/install-azure-cli) Azure CLI 2.0 yüklemek için:

Azure CLI 2.0 yüklemek `curl` komutu:

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

Ve değişikliklerin etkili olması, komut kabuğu yeniden başlatın:

```bash
exec -l $SHELL
```

#### <a name="install-arduino-ide"></a>Arduino IDE yükleyin

Visual Studio kod Arduino uzantısı Arduino IDE üzerinde kullanır. İndirme ve yükleme [macOS Arduino IDE](https://www.arduino.cc/en/Main/Software).

#### <a name="install-visual-studio-code"></a>Visual Studio Kodu'nu yükle

İndirme ve yükleme [macOS için Visual Studio Code](https://code.visualstudio.com/). Bu DevKit IOT uygulamaları oluşturmak için birincil geliştirme aracı olacaktır.

####  <a name="download-latest-package"></a>Son paketini indirin

1. Node.js yükleyin. Popüler macOS Paket Yöneticisi'ni kullanabilirsiniz [Homebrew](https://brew.sh/) veya [yükleyici önceden oluşturulmuş](https://nodejs.org/en/download/) yükleyin.

2. Karşıdan `.zip` VS Code DevKit geliştirme için gerekli görev komut dosyalarını içeren dosya.

   > [!div class="button"]
   [İndir](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

   Bulun `.zip` ve ayıklayın. Ardından başlatma **Terminal** uygulama ve yapılandırmak için aşağıdaki komutları çalıştırın:

   MacOS kullanıcı klasörünüze ayıklanan klasörü Taşı:
   ```bash
   mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
   ```
  
   Yükleme `npm` paketler:
   ```
   npm install
   ```

#### <a name="install-vs-code-extension-for-arduino"></a>VS Code uzantısını Arduino için yükleyin

Visual Studio Code Market uzantılar doğrudan aracı yükleme, soldaki menüden bölmesinde uzantıları simgesine tıklamanız yeterlidir ve ardından arama olanak tanır `Arduino` yüklemek için:

![Uzantıları Yükleme](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-devkit-board-package"></a>DevKit Panosu paketini yükle

Visual Studio kodda Panosu Yöneticisi'ni kullanarak DevKit Panosu eklemeniz gerekir.

1. Kullanım `Cmd+Shift+P` komutu paleti ve türü çağrılacak **Arduino** ardından bulmak ve seçmek **Arduino: Panosu Yöneticisi**.

2. Tıklatın **'Ek URL'ler'** sağ alt köşede.
   ![Yükleme ek-URL'leri](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)

3. İçinde `settings.json` dosya, alt kısmında bir satır ekleyin `USER SETTINGS` bölmesi ve kaydedin.
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![yükleme ayarları json](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. Şimdi 'az3166 için' Panosu Yöneticisi'nde arayın ve en son sürümünü yükleyin.
   ![Yükleme az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)

Artık tüm gerekli araçları ve macOS için yüklü olan paketleri vardır.


## <a name="open-project-folder"></a>Proje Aç klasörü

### <a name="launch-vs-code"></a>VS Code’u başlatın

DevKit bağlı emin olun. İlk VS Code'u başlatın ve DevKit bilgisayarınıza bağlayın. VS Code otomatik olarak bulmak ve ayarlama giriş sayfası açılır:

![Mini solution vscode](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
Bazen, VS Code'u başlatın, Arduino IDE veya ilgili Panosu paketi bulunamadı hatasıyla istenir. Çözmek VS Code kapatmak için bir kez yeniden başlatma Arduino IDE ve VS Code Arduino IDE yolu doğru bulun.

### <a name="open-arduino-examples-folder"></a>Arduino örnekler Klasör Aç

Geçiş **'Arduino örnekler'** sekmesinde, gitmek `Examples for MXCHIP AZ3166 > AzureIoT` ve tıklayın `GetStarted`.

![Mini solution örnekleri](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

Bölmesini kapatmak için görülüyorsa, yeniden yüklemek için kullanmak `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) komutu paleti ve türü çağrılacak **Arduino** bulmak ve seçmek için **Arduino: örnekler**.

## <a name="provision-azure-services"></a>Azure hizmetlerini hazırlamanız

Çözüm penceresinde göreviniz çalıştırın `Ctrl+P` (macOS: `Cmd+P`) 'bulut sağlama görev' yazarak:

Terminal VS kodu'nda etkileşimli bir komut satırı, gerekli Azure hizmetleri sağlama aracılığıyla yardımcı olur:

![Mini-solution-bulut-sağlama](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-arduino-sketch"></a>Derleme ve Arduino taslak karşıya yükle

### <a name="install-required-library"></a>Gerekli kitaplığını yükle

1. Tuşuna `F1` veya `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) komutu paleti ve türü çağrılacak **Arduino** ardından bulmak ve seçmek **Arduino: Kitaplığı Yöneticisi**.

2. Arama `ArduinoJson` kitaplığı ve tıklatın **yükleyin**

### <a name="build-and-upload-the-device-code"></a>Derleme ve aygıt kodu karşıya yükle

Kullanım `Ctrl+P` (macOS: `Cmd+P`) 'aygıt karşıya yükleme görev' çalıştırmak için. Terminal yapılandırma modu girmenizi ister. Bunu yapmak için A düğmesini basılı tutun sonra push ve Sıfırla düğmesini bırakın. 'Configuration' ekranı görüntüler. 'Görev bulut-provision' adımından alır bağlantı dizesini ayarlamak için budur.

Ardından doğrulama ve Arduino taslak karşıya yükleme başlar:

![Mini-solution aygıt-karşıya yükleme](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

DevKit yeniden başlatın ve kodu çalıştırma başlatın.

## <a name="test-the-project"></a>Projeyi test

VS Code'da seri İzleyicisi'ni açmak için durum çubuğunda güç Tak simgesine tıklayın.

Aşağıdaki sonuçları gördüğünüzde örnek uygulama başarıyla çalıştırma:

* Seri İzleyicisi, aşağıdaki ekran görüntüsünde içerik olarak aynı bilgiyi görüntüler.
* LED MXChip IOT DevKit üzerinde yanıp sönen.

![VS code'da son çıktı](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a>Sorunları ve geri bildirim

Bulabileceğiniz [SSS](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) sorunlarla ya da kanaldan bize ulaşın.

## <a name="next-steps"></a>Sonraki adımlar

Başarıyla MXChip IOT DevKit IOT Hub'ına bağlı ve yakalanan algılayıcı verilerini IOT hub'ına gönderilen.

IoT Hub’ı kullanmaya başlamak ve diğer IoT senaryolarını keşfetmek için bkz:

- [iothub-explorer ile bulut cihaz mesajlaşmasını yönetme](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [IoT Hub iletilerini Azure veri depolamaya kaydetme](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [Azure IOT hub'ı gerçek zamanlı algılayıcı verilerini görselleştirmek için Power BI kullanın](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [Azure IOT hub'ı gerçek zamanlı algılayıcı verilerini görselleştirmek için Azure Web uygulamaları kullanma](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [IOT hub'ınızı algılayıcı verilerini Azure Machine Learning kullanarak tahmin hava durumu](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [iothub-explorer ile cihaz yönetimi](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- [Logic Apps ile uzaktan izleme ve bildirimler](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps)