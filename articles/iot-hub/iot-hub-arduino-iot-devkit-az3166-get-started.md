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
# <a name="connect-iot-devkit-az3166-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="0a7b5-103">IOT DevKit AZ3166 tooAzure IOT Hub'hello bulutta Bağlan</span><span class="sxs-lookup"><span data-stu-id="0a7b5-103">Connect IoT DevKit AZ3166 tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="0a7b5-104">Merhaba [MXChip IOT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) kullanılan toodevelop ve prototip Microsoft Azure hizmetlerini yararlanarak nesnelerin interneti (IOT) çözümleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-104">hello [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) can be used toodevelop and prototype Internet of Things (IoT) solutions leveraging Microsoft Azure services.</span></span> <span data-ttu-id="0a7b5-105">Zengin çevre algılayıcılar, bir açık kaynak tablosu paketi ve bir büyüyen bir Arduino uyumlu panosuna içeren [projeleri katalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).</span><span class="sxs-lookup"><span data-stu-id="0a7b5-105">It includes an Arduino compatible board with rich peripherals and sensors, an open-source board package and a growing [projects catalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="0a7b5-106">Neler</span><span class="sxs-lookup"><span data-stu-id="0a7b5-106">What you do</span></span>
<span data-ttu-id="0a7b5-107">Bağlantı [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) tooan Azure IOT hub oluşturma, toplama hello sıcaklık ve nem verilerden algılayıcılar ve hello veri tooIoT hub gönderin.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-107">Connect [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) tooan Azure IoT hub that you create, collect hello temperature and humidity data from sensors and send hello data tooIoT hub.</span></span>

<span data-ttu-id="0a7b5-108">Bir DevKit henüz yok mu?</span><span class="sxs-lookup"><span data-stu-id="0a7b5-108">Don't have a DevKit yet?</span></span> <span data-ttu-id="0a7b5-109">Yeni bir tane almak [burada](https://aka.ms/iot-devkit-purchase).</span><span class="sxs-lookup"><span data-stu-id="0a7b5-109">Get a new one [here](https://aka.ms/iot-devkit-purchase).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="0a7b5-110">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="0a7b5-110">What you learn</span></span>

* <span data-ttu-id="0a7b5-111">Nasıl tooconnect IOT DevKit tooWireless erişim noktası ve geliştirme ortamınızı hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-111">How tooconnect IoT DevKit tooWireless access point and prepare your development environment.</span></span>
* <span data-ttu-id="0a7b5-112">Nasıl toocreate IOT hub'ı ve MXChip IOT DevKit için kaydedilecek.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-112">How toocreate an IoT hub and register a device for MXChip IoT DevKit.</span></span>
* <span data-ttu-id="0a7b5-113">Nasıl MXChip IOT DevKit üzerinde bir örnek uygulamayı çalıştırarak toocollect algılayıcı verileri.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-113">How toocollect sensor data by running a sample application on MXChip IoT DevKit.</span></span>
* <span data-ttu-id="0a7b5-114">Nasıl toosend algılayıcı verileri tooyour IOT hub'ı hello.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-114">How toosend hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0a7b5-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="0a7b5-115">What you need</span></span>

* <span data-ttu-id="0a7b5-116">MXChip IOT DevKit kartı mikro USB kablosu ile.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-116">An MXChip IoT DevKit board with a micro USB cable.</span></span> [<span data-ttu-id="0a7b5-117">Şimdi alın</span><span class="sxs-lookup"><span data-stu-id="0a7b5-117">Get it now</span></span>](https://aka.ms/iot-devkit-purchase)
* <span data-ttu-id="0a7b5-118">Windows 10 veya macOS 10.10 + çalıştıran bir bilgisayar</span><span class="sxs-lookup"><span data-stu-id="0a7b5-118">A computer running Windows 10 or macOS 10.10+</span></span>
* <span data-ttu-id="0a7b5-119">Etkin bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="0a7b5-119">An active Azure subscription</span></span>
  * <span data-ttu-id="0a7b5-120">Etkinleştirme bir [Ücretsiz 30 günlük deneme Microsoft Azure hesabı](https://azureinfo.microsoft.com/us-freetrial.html)</span><span class="sxs-lookup"><span data-stu-id="0a7b5-120">Activate a [free 30-day trial Microsoft Azure account](https://azureinfo.microsoft.com/us-freetrial.html)</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="0a7b5-121">Donanımınızın hazırlama</span><span class="sxs-lookup"><span data-stu-id="0a7b5-121">Prepare your hardware</span></span>

<span data-ttu-id="0a7b5-122">Merhaba donanım tooyour bilgisayarı takma.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-122">Hook up hello hardware tooyour computer.</span></span>

### <a name="hardware-you-need"></a><span data-ttu-id="0a7b5-123">Gereksinim duyduğunuz donanım</span><span class="sxs-lookup"><span data-stu-id="0a7b5-123">Hardware you need</span></span>

* <span data-ttu-id="0a7b5-124">DevKit Panosu</span><span class="sxs-lookup"><span data-stu-id="0a7b5-124">DevKit board</span></span>
* <span data-ttu-id="0a7b5-125">Mikro USB kablosu</span><span class="sxs-lookup"><span data-stu-id="0a7b5-125">Micro USB cable</span></span>

![alma başlatıldı-donanım](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

### <a name="connect-devkit-tooyour-computer"></a><span data-ttu-id="0a7b5-127">DevKit tooyour bilgisayara bağlanma</span><span class="sxs-lookup"><span data-stu-id="0a7b5-127">Connect DevKit tooyour computer</span></span>

1. <span data-ttu-id="0a7b5-128">USB son tooyour PC Bağlan</span><span class="sxs-lookup"><span data-stu-id="0a7b5-128">Connect USB end tooyour PC</span></span>
2. <span data-ttu-id="0a7b5-129">Mikro USB son toohello DevKit Bağlan</span><span class="sxs-lookup"><span data-stu-id="0a7b5-129">Connect Micro USB end toohello DevKit</span></span>
3. <span data-ttu-id="0a7b5-130">bağlantı Hello yeşil LED sonraki toopower onaylar</span><span class="sxs-lookup"><span data-stu-id="0a7b5-130">hello green LED next toopower confirms connection</span></span>

![alma-başlatıldı-Bağlan](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wifi"></a><span data-ttu-id="0a7b5-132">WiFi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0a7b5-132">Configure WiFi</span></span>

<span data-ttu-id="0a7b5-133">IOT projelerinin Internet bağlantısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-133">IoT projects rely on Internet connectivity.</span></span> <span data-ttu-id="0a7b5-134">Aşağıdaki yönergeler tooconfigure hello DevKit tooconnect tooWiFi hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-134">Use hello following instructions tooconfigure hello DevKit tooconnect tooWiFi.</span></span>

### <a name="enter-ap-mode"></a><span data-ttu-id="0a7b5-135">AP modu girin</span><span class="sxs-lookup"><span data-stu-id="0a7b5-135">Enter AP Mode</span></span>

<span data-ttu-id="0a7b5-136">B düğmesini basılı tutun, ardından itme ve yayın hello düğmesine, ardından yayın düğmesi b sıfırlama DevKit WiFi yapılandırmak için AP moduna girer.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-136">Hold down button B, then push and release hello reset button, then release button B. Your DevKit will enter AP Mode for configuring WiFi.</span></span> <span data-ttu-id="0a7b5-137">Merhaba ekranında hello hizmet ayarlamak Identifier(SSID) hello DevKit, ve bunun yanı sıra hello yapılandırma portalı IP adresini görüntüler:</span><span class="sxs-lookup"><span data-stu-id="0a7b5-137">hello screen will display hello Service Set Identifier(SSID) of hello DevKit as well as hello configuration portal IP address:</span></span>

![alma-başlatıldı-wifi-ap](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-toodevkit-ap"></a><span data-ttu-id="0a7b5-139">TooDevKit AP Bağlan</span><span class="sxs-lookup"><span data-stu-id="0a7b5-139">Connect tooDevKit AP</span></span>

<span data-ttu-id="0a7b5-140">Şimdi, başka bir etkin WiFi aygıt (PC veya cep telefonu) tooconnect toohello DevKit (yukarıdaki hello ekran görüntüsünde vurgulanan) SSID kullanın, hello parola boş bırakın.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-140">Now, use another WiFi enabled device (PC or mobile phone) tooconnect toohello DevKit SSID (highlighted in hello screenshot above), leave hello password empty.</span></span>

![alma-başlatıldı-SSID](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wifi-for-devkit"></a><span data-ttu-id="0a7b5-142">WiFi DevKit için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0a7b5-142">Configure WiFi for DevKit</span></span>

<span data-ttu-id="0a7b5-143">PC veya cep telefonu tarayıcı hello DevKit ekranda gösterilen açık hello IP adresi hello DevKit tooconnect istediğiniz hello WiFi ağı seçin ve ardından hello parolayı yazın.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-143">Open hello IP address shown on hello DevKit screen on your PC or mobile phone browser, select hello WiFi network you want hello DevKit tooconnect to, then type hello password.</span></span> <span data-ttu-id="0a7b5-144">Tıklatın **Bağlan** toocomplete:</span><span class="sxs-lookup"><span data-stu-id="0a7b5-144">Click **Connect** toocomplete:</span></span>

![alma başlatıldı-wifi-portal](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

<span data-ttu-id="0a7b5-146">Merhaba DevKit Hello bağlantı başarılı olduktan sonra birkaç saniye içinde yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-146">Once hello connection succeeds, hello DevKit will reboot in a few seconds.</span></span> <span data-ttu-id="0a7b5-147">Başarılı olursa Merhaba ekranında hello WiFi adı ve IP adresi görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="0a7b5-147">If succeeded, you will see hello WiFi name and IP address on hello screen:</span></span>

![alma başlatıldı-wifi-IP](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
<span data-ttu-id="0a7b5-149">Merhaba fotoğraf görüntülenen başlangıç IP adresi atanır ve hello DevKit ekranda görüntülenen hello gerçek IP eşleşmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-149">hello IP address displayed in hello photo may not match hello actual IP assigned and displayed on hello DevKit screen.</span></span> <span data-ttu-id="0a7b5-150">Bu DHCP toodynamically atamak IP'leri WiFi kullandıkça normaldir.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-150">This is normal as WiFi uses DHCP toodynamically assign IPs.</span></span>

<span data-ttu-id="0a7b5-151">WiFi yapılandırıldıktan sonra kimlik bilgilerinizi hello cihazda Bu bağlantı için takılı olsa bile kalıcı.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-151">After WiFi is configured, your credentials will be persisted on hello device for that connection, even if unplugged.</span></span> <span data-ttu-id="0a7b5-152">Merhaba DevKit evinizde WiFi için yapılandırılmış ve hello DevKit toohello office sürdü, örneğin, tooreconfigure AP modu gerekir (adım başlangıç **girin AP modu**) tooconnect hello DevKit tooyour office WiFi.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-152">For example, if you configured hello DevKit for WiFi in your home and then took hello DevKit toohello office, you will need tooreconfigure AP mode (starting at step **Enter AP Mode**) tooconnect hello DevKit tooyour office WiFi.</span></span> 

## <a name="start-using-devkit"></a><span data-ttu-id="0a7b5-153">DevKit kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="0a7b5-153">Start using DevKit</span></span>

<span data-ttu-id="0a7b5-154">DevKit üzerinde çalışan hello varsayılan uygulama hello son hello bellenim sürümünü denetleyin ve sizin için bazı algılayıcı tanılama verilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-154">hello default app running on DevKit will check hello latest version of hello firmware and display some sensor diagnosis data for you.</span></span>

### <a name="upgrade-toohello-latest-firmware"></a><span data-ttu-id="0a7b5-155">Toohello en son bellenim yükseltme</span><span class="sxs-lookup"><span data-stu-id="0a7b5-155">Upgrade toohello latest firmware</span></span>

<span data-ttu-id="0a7b5-156">Gerekli bir yükseltme ise her ikisi de geçerli ve en son bellenim sürümünü hello Merhaba ekranında istenir.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-156">You will be prompted on hello screen both hello current and latest firmware version if there is an upgrade needed.</span></span> <span data-ttu-id="0a7b5-157">İzleyin [yükseltme bellenim](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) Kılavuzu tooupgrade onu.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-157">Follow [Upgrade firmware](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) guide tooupgrade it.</span></span>

![alma-başlatıldı-üretici yazılımı](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
<span data-ttu-id="0a7b5-159">Bu DevKit hello üzerinde geliştirme başladıktan sonra bir kerelik çaba ve uygulamanızı karşıya yükleme, uygulamanız ile gelen hello son üretici yazılımına sahip olur.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-159">This is a one-time effort, once you start developing on hello DevKit and upload your app, you will have hello latest firmware come with your app.</span></span>

### <a name="test-various-sensors"></a><span data-ttu-id="0a7b5-160">Çeşitli algılayıcılar test</span><span class="sxs-lookup"><span data-stu-id="0a7b5-160">Test various sensors</span></span>

<span data-ttu-id="0a7b5-161">Düğmesi B tootest algılayıcılar tuşlarına basın, tuşuna basarak ve her algılayıcı hello B düğmesi toocycle serbest devam eder.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-161">Press button B tootest sensors, continue pressing and releasing hello B button toocycle through each sensor.</span></span>

![alma-başlatıldı-algılayıcılar](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-development-environment"></a><span data-ttu-id="0a7b5-163">Geliştirme ortamını hazırlayın</span><span class="sxs-lookup"><span data-stu-id="0a7b5-163">Prepare development environment</span></span>

<span data-ttu-id="0a7b5-164">Şimdi zaman tooset hello geliştirme ortamını ayarlama: araçlar ve IOT uygulamaları şaşırtıcı toobuild paketleri.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-164">Now it's time tooset up hello development environment: tools and packages for you toobuild stunning IoT applications.</span></span> <span data-ttu-id="0a7b5-165">Windows veya macOS sürüm tooyour işletim sistemine göre seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-165">You can choose Windows or macOS version according tooyour operating system.</span></span>


### <a name="windows"></a><span data-ttu-id="0a7b5-166">Windows</span><span class="sxs-lookup"><span data-stu-id="0a7b5-166">Windows</span></span>

<span data-ttu-id="0a7b5-167">Toouse hello yükleme paketini tooprepare hello geliştirme ortamı öneririz.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-167">We encourage you toouse hello installation package tooprepare hello development environment.</span></span> <span data-ttu-id="0a7b5-168">Herhangi bir sorunla karşılaşırsanız, hello izleyebilirsiniz [el ile yapılacak adımlar](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget bu yapılır.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-168">If you encounter any issues, you can follow hello [manual steps](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget it done.</span></span>

#### <a name="download-latest-package"></a><span data-ttu-id="0a7b5-169">Son paketini indirin</span><span class="sxs-lookup"><span data-stu-id="0a7b5-169">Download latest package</span></span>

<span data-ttu-id="0a7b5-170">Merhaba `.zip` karşıdan dosya tüm gerekli araçları ve DevKit geliştirme için gerekli paketleri içerir.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-170">hello `.zip` file you download contains all necessary tools and packages required for DevKit development.</span></span>

> [!div class="button"]
[<span data-ttu-id="0a7b5-171">İndir</span><span class="sxs-lookup"><span data-stu-id="0a7b5-171">Download</span></span>](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


> [!NOTE] 
> <span data-ttu-id="0a7b5-172">Merhaba `.zip` dosyasını içeren hello aşağıdaki araçları ve paketleri.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-172">hello `.zip` file contains hello following tools and packages.</span></span> <span data-ttu-id="0a7b5-173">Bazı bileşenleri yüklü zaten varsa, hello betik algılamak ve onları atlayın.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-173">If you already have some components installed, hello script will detect and skip them.</span></span>
> * <span data-ttu-id="0a7b5-174">Node.js ve Yarn: hello Kurulum komut dosyası ve otomatik görevler için çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="0a7b5-174">Node.js and Yarn: Runtime for hello setup script and automated tasks</span></span>
> * <span data-ttu-id="0a7b5-175">[Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) -Azure kaynaklarını, hello MSI yönetmek için platformlar arası komut satırı deneyimi bağımlı Python ve PIP içerir.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-175">[Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) - Cross-platform command-line experience for managing Azure resources, hello MSI contains dependent Python and pip.</span></span>
> * <span data-ttu-id="0a7b5-176">[Visual Studio Code](https://code.visualstudio.com/): DevKit geliştirme için basit Kod Düzenleyicisi</span><span class="sxs-lookup"><span data-stu-id="0a7b5-176">[Visual Studio Code](https://code.visualstudio.com/): Lightweight code editor for DevKit development</span></span>
> * <span data-ttu-id="0a7b5-177">[Visual Studio Code uzantısı Arduino için](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): VS code'da sağlayan Arduino geliştirme</span><span class="sxs-lookup"><span data-stu-id="0a7b5-177">[Visual Studio Code extension for Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): Enables Arduino development in VS Code</span></span>
> * <span data-ttu-id="0a7b5-178">[Arduino IDE](https://www.arduino.cc/en/Main/Software): hello uzantısı Arduino için bu aracı üzerinde kullanır</span><span class="sxs-lookup"><span data-stu-id="0a7b5-178">[Arduino IDE](https://www.arduino.cc/en/Main/Software): hello extension for Arduino relies on this tool</span></span>
> * <span data-ttu-id="0a7b5-179">DevKit Panosu paketi: zincirleri, kitaplıklar ve hello DevKit projelerde aracı</span><span class="sxs-lookup"><span data-stu-id="0a7b5-179">DevKit Board Package: Tool chains, libraries and projects for hello DevKit</span></span>
> * <span data-ttu-id="0a7b5-180">ST bağlantı yardımcı programı: Gerekli yardımcı programları ve sürücüleri</span><span class="sxs-lookup"><span data-stu-id="0a7b5-180">ST-Link Utility: Essential utilities and drivers</span></span>

#### <a name="run-installation-script"></a><span data-ttu-id="0a7b5-181">Yükleme komut dosyasını çalıştır</span><span class="sxs-lookup"><span data-stu-id="0a7b5-181">Run installation script</span></span>

<span data-ttu-id="0a7b5-182">Windows dosya Gezgini'nde hello bulun `.zip` ve ayıklayın, Bul `install.cmd`seçin ve sağ tıklatıp **"Yönetici olarak çalıştır"** toostart.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-182">In Windows File Explorer, locate hello `.zip` and extract it, find `install.cmd`, right-click and select **"Run as administrator"** toostart.</span></span>

![alma başlatıldı-Çalıştır-yönetici](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

<span data-ttu-id="0a7b5-184">Yükleme sırasında her aracı veya paket hello ilerlemesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-184">During installation, you will see hello progress of each tool or package.</span></span>

![alma başlatıldı-yükleme](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="confirm-tooinstall-drivers"></a><span data-ttu-id="0a7b5-186">Tooinstall sürücüleri onaylayın</span><span class="sxs-lookup"><span data-stu-id="0a7b5-186">Confirm tooinstall drivers</span></span>

<span data-ttu-id="0a7b5-187">Merhaba VS Code Arduino uzantısı hello Arduino IDE üzerinde kullanır.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-187">hello VS Code for Arduino extension relies on hello Arduino IDE.</span></span> <span data-ttu-id="0a7b5-188">Bu hello hello Arduino IDE yüklediğiniz ilk kez kullanıyorsanız, istendiğinde tooinstall ilgili sürücüleri olacaktır:</span><span class="sxs-lookup"><span data-stu-id="0a7b5-188">If this is hello first time you are installing hello Arduino IDE, you will be prompted tooinstall relevant drivers:</span></span>

![alma başlatıldı-sürücü](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

<span data-ttu-id="0a7b5-190">Internet hızınıza bağlı olarak toofinish yükleme yaklaşık 10 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-190">It should take around 10 minutes toofinish installation depending on your Internet speed.</span></span> <span data-ttu-id="0a7b5-191">Merhaba yüklemesi tamamlandıktan sonra masaüstünüzde Visual Studio Code ve Arduino IDE kısayolları görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-191">Once hello installation is complete, you should see Visual Studio Code and Arduino IDE shortcuts on your desktop.</span></span>

> [!NOTE] 
<span data-ttu-id="0a7b5-192">Bazen, VS Code'u başlatın, Arduino IDE veya ilgili Panosu paketi bulamıyor bir hata ile istenir.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-192">Occasionally, when you launch VS Code, you will be prompted with an error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="0a7b5-193">Kapat VS Code'u başlatın Arduino IDE kez toosolve ve VS Code Arduino IDE yolu doğru bulun.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-193">toosolve it, close VS Code, launch Arduino IDE once and VS Code should locate Arduino IDE path correctly.</span></span>


### <a name="macos-preview"></a><span data-ttu-id="0a7b5-194">macOS (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="0a7b5-194">macOS (Preview)</span></span>

<span data-ttu-id="0a7b5-195">Bu adımları tooprepare geliştirme ortamı macOS üzerinde izleyin.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-195">Follow these steps tooprepare development environment on macOS.</span></span>

#### <a name="install-azure-cli-20"></a><span data-ttu-id="0a7b5-196">Azure CLI 2.0’ı yükleme</span><span class="sxs-lookup"><span data-stu-id="0a7b5-196">Install Azure CLI 2.0</span></span>

<span data-ttu-id="0a7b5-197">Merhaba izleyin [resmi Kılavuzu](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall Azure CLI 2.0:</span><span class="sxs-lookup"><span data-stu-id="0a7b5-197">Follow hello [official guide](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall Azure CLI 2.0:</span></span>

<span data-ttu-id="0a7b5-198">Azure CLI 2.0 yüklemek `curl` komutu:</span><span class="sxs-lookup"><span data-stu-id="0a7b5-198">Install Azure CLI 2.0 with one `curl` command:</span></span>

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="0a7b5-199">Ve değişiklikleri tootake etkisi, komut kabuğu yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="0a7b5-199">And restart your command shell for changes tootake effect:</span></span>

```bash
exec -l $SHELL
```

#### <a name="install-arduino-ide"></a><span data-ttu-id="0a7b5-200">Arduino IDE yükleyin</span><span class="sxs-lookup"><span data-stu-id="0a7b5-200">Install Arduino IDE</span></span>

<span data-ttu-id="0a7b5-201">Visual Studio kod Arduino uzantısı Hello hello Arduino IDE üzerinde kullanır.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-201">hello Visual Studio Code Arduino extension relies on hello Arduino IDE.</span></span> <span data-ttu-id="0a7b5-202">Merhaba yükleyip [macOS Arduino IDE](https://www.arduino.cc/en/Main/Software).</span><span class="sxs-lookup"><span data-stu-id="0a7b5-202">Download and install hello [Arduino IDE for macOS](https://www.arduino.cc/en/Main/Software).</span></span>

#### <a name="install-visual-studio-code"></a><span data-ttu-id="0a7b5-203">Visual Studio Kodu'nu yükle</span><span class="sxs-lookup"><span data-stu-id="0a7b5-203">Install Visual Studio Code</span></span>

<span data-ttu-id="0a7b5-204">İndirme ve yükleme [macOS için Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="0a7b5-204">Download and install [Visual Studio Code for macOS](https://code.visualstudio.com/).</span></span> <span data-ttu-id="0a7b5-205">Bu DevKit IOT uygulamaları oluşturmak için hello birincil geliştirme aracı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-205">This will be hello primary development tool for building DevKit IoT applications.</span></span>

####  <a name="download-latest-package"></a><span data-ttu-id="0a7b5-206">Son paketini indirin</span><span class="sxs-lookup"><span data-stu-id="0a7b5-206">Download latest package</span></span>

1. <span data-ttu-id="0a7b5-207">Node.js yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-207">Install Node.js.</span></span> <span data-ttu-id="0a7b5-208">Popüler macOS Paket Yöneticisi'ni kullanabilirsiniz [Homebrew](https://brew.sh/) veya [yükleyici önceden oluşturulmuş](https://nodejs.org/en/download/) tooinstall onu.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-208">You can use popular macOS package manager [Homebrew](https://brew.sh/) or [pre-built installer](https://nodejs.org/en/download/) tooinstall it.</span></span>

2. <span data-ttu-id="0a7b5-209">Karşıdan `.zip` VS Code DevKit geliştirme için gerekli görev komut dosyalarını içeren dosya.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-209">Download `.zip` file containing task scripts required for DevKit development in VS Code.</span></span>

   > [!div class="button"]
   [<span data-ttu-id="0a7b5-210">İndir</span><span class="sxs-lookup"><span data-stu-id="0a7b5-210">Download</span></span>](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

   <span data-ttu-id="0a7b5-211">Merhaba bulun `.zip` ve ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-211">Locate hello `.zip` and extract it.</span></span> <span data-ttu-id="0a7b5-212">Ardından başlatma **Terminal** uygulama ve komutları tooconfigure aşağıdaki çalışma hello:</span><span class="sxs-lookup"><span data-stu-id="0a7b5-212">Then launch **Terminal** app and run hello following commands tooconfigure:</span></span>

   <span data-ttu-id="0a7b5-213">Ayıklanan klasörü tooyour macOS kullanıcı klasörü Taşı:</span><span class="sxs-lookup"><span data-stu-id="0a7b5-213">Move extracted folder tooyour macOS user folder:</span></span>
   ```bash
   mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
   ```
  
   <span data-ttu-id="0a7b5-214">Yükleme `npm` paketler:</span><span class="sxs-lookup"><span data-stu-id="0a7b5-214">Install `npm` packages:</span></span>
   ```
   npm install
   ```

#### <a name="install-vs-code-extension-for-arduino"></a><span data-ttu-id="0a7b5-215">VS Code uzantısını Arduino için yükleyin</span><span class="sxs-lookup"><span data-stu-id="0a7b5-215">Install VS Code extension for Arduino</span></span>

<span data-ttu-id="0a7b5-216">Visual Studio Code verir tooinstall Market uzantıları doğrudan hello aracında, yalnızca hello soldaki menüden bölmesinde hello uzantıları simgesine tıklayın ve ardından arama `Arduino` tooinstall:</span><span class="sxs-lookup"><span data-stu-id="0a7b5-216">Visual Studio Code allows you tooinstall Marketplace extensions directly in hello tool, simply click hello extensions icon in hello left menu pane and then search `Arduino` tooinstall:</span></span>

![Uzantıları Yükleme](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-devkit-board-package"></a><span data-ttu-id="0a7b5-218">DevKit Panosu paketini yükle</span><span class="sxs-lookup"><span data-stu-id="0a7b5-218">Install DevKit board package</span></span>

<span data-ttu-id="0a7b5-219">Visual Studio kodda hello Panosu Yöneticisi'ni kullanarak tooadd hello DevKit Panosu gerekir.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-219">You will need tooadd hello DevKit board using hello Board Manager in Visual Studio Code.</span></span>

1. <span data-ttu-id="0a7b5-220">Kullanım `Cmd+Shift+P` tooinvoke komutu paleti ve türü **Arduino** ardından bulmak ve seçmek **Arduino: Panosu Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-220">Use `Cmd+Shift+P` tooinvoke command palette and type **Arduino** then find and select **Arduino: Board Manager**.</span></span>

2. <span data-ttu-id="0a7b5-221">Tıklatın **'Ek URL'ler'** sağ hello altındaki.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-221">Click **'Additional URLs'** at hello bottom right.</span></span>
   <span data-ttu-id="0a7b5-222">![Yükleme ek-URL'leri](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span><span class="sxs-lookup"><span data-stu-id="0a7b5-222">![installation-additional-urls](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span></span>

3. <span data-ttu-id="0a7b5-223">Merhaba, `settings.json` dosya, hello alt kısmında bir satır ekleyin `USER SETTINGS` bölmesi ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-223">In hello `settings.json` file, add a line at hello bottom of `USER SETTINGS` pane and save.</span></span>
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![yükleme ayarları json](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. <span data-ttu-id="0a7b5-225">Şimdi 'az3166 için' hello Panosu Yöneticisi'ni arayın ve hello en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-225">Now in hello Board Manager search for 'az3166' and install hello latest version.</span></span>
   <span data-ttu-id="0a7b5-226">![Yükleme az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span><span class="sxs-lookup"><span data-stu-id="0a7b5-226">![installation-az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span></span>

<span data-ttu-id="0a7b5-227">Artık tüm hello gereken araçları ve macOS için yüklü olan paketleri vardır.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-227">You now have all hello necessary tools and packages installed for macOS.</span></span>


## <a name="open-project-folder"></a><span data-ttu-id="0a7b5-228">Proje Aç klasörü</span><span class="sxs-lookup"><span data-stu-id="0a7b5-228">Open project folder</span></span>

### <a name="launch-vs-code"></a><span data-ttu-id="0a7b5-229">VS Code’u başlatın</span><span class="sxs-lookup"><span data-stu-id="0a7b5-229">Launch VS Code</span></span>

<span data-ttu-id="0a7b5-230">DevKit bağlı emin olun.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-230">Make sure your DevKit is not connected.</span></span> <span data-ttu-id="0a7b5-231">İlk VS Code'u başlatın ve hello DevKit tooyour bilgisayara bağlanın.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-231">Launch VS Code first and connect hello DevKit tooyour computer.</span></span> <span data-ttu-id="0a7b5-232">VS Code otomatik olarak bulmak ve ayarlama giriş sayfası açılır:</span><span class="sxs-lookup"><span data-stu-id="0a7b5-232">VS Code will automatically find it and pop up an introduction page:</span></span>

![Mini solution vscode](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
<span data-ttu-id="0a7b5-234">Bazen, VS Code'u başlatın, Arduino IDE veya ilgili Panosu paketi bulunamadı hatasıyla istenir.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-234">Occasionally, when you launch VS Code, you will be prompted with error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="0a7b5-235">Kapat VS Code'u başlatın Arduino IDE yeniden toosolve ve VS Code Arduino IDE yolu doğru bulun.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-235">toosolve it, close VS Code, launch Arduino IDE once again and VS Code should locate Arduino IDE path correctly.</span></span>

### <a name="open-arduino-examples-folder"></a><span data-ttu-id="0a7b5-236">Arduino örnekler Klasör Aç</span><span class="sxs-lookup"><span data-stu-id="0a7b5-236">Open Arduino Examples folder</span></span>

<span data-ttu-id="0a7b5-237">Çok geçiş**'Arduino örnekler'** sekmesinde, çok gidin`Examples for MXCHIP AZ3166 > AzureIoT` ve tıklayın `GetStarted`.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-237">Switch too**'Arduino Examples'** tab, navigate too`Examples for MXCHIP AZ3166 > AzureIoT` and click on `GetStarted`.</span></span>

![Mini solution örnekleri](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

<span data-ttu-id="0a7b5-239">Tooclose hello bölmesini görülüyorsa tooreload, kullanım `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke komutu paleti ve türü **Arduino** toofind seçip **Arduino: örnekler**.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-239">If you happen tooclose hello pane, tooreload it, use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke command palette and type **Arduino** toofind and select **Arduino: Examples**.</span></span>

## <a name="provision-azure-services"></a><span data-ttu-id="0a7b5-240">Azure hizmetlerini hazırlamanız</span><span class="sxs-lookup"><span data-stu-id="0a7b5-240">Provision Azure services</span></span>

<span data-ttu-id="0a7b5-241">Görevinizi Hello çözüm penceresinde çalıştırın `Ctrl+P` (macOS: `Cmd+P`) 'bulut sağlama görev' yazarak:</span><span class="sxs-lookup"><span data-stu-id="0a7b5-241">In hello solution window, run your task through `Ctrl+P` (macOS: `Cmd+P`) by typing 'task cloud-provision':</span></span>

<span data-ttu-id="0a7b5-242">Hello VS Code etkileşimli bir komut satırı sağlama hello yönlendirecek terminal Azure Hizmetleri gereklidir:</span><span class="sxs-lookup"><span data-stu-id="0a7b5-242">In hello VS Code terminal, an interactive command line will guide you through provisioning hello required Azure services:</span></span>

![Mini-solution-bulut-sağlama](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-arduino-sketch"></a><span data-ttu-id="0a7b5-244">Derleme ve Arduino taslak karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="0a7b5-244">Build and upload Arduino sketch</span></span>

### <a name="install-required-library"></a><span data-ttu-id="0a7b5-245">Gerekli kitaplığını yükle</span><span class="sxs-lookup"><span data-stu-id="0a7b5-245">Install required library</span></span>

1. <span data-ttu-id="0a7b5-246">Tuşuna `F1` veya `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke komutu paleti ve türü **Arduino** ardından bulmak ve seçmek **Arduino: Kitaplığı Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-246">Press `F1` or `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke command palette and type **Arduino** then find and select **Arduino: Library Manager**.</span></span>

2. <span data-ttu-id="0a7b5-247">Arama `ArduinoJson` kitaplığı ve tıklatın **yükleyin**</span><span class="sxs-lookup"><span data-stu-id="0a7b5-247">Search for `ArduinoJson` library and click **Install**</span></span>

### <a name="build-and-upload-hello-device-code"></a><span data-ttu-id="0a7b5-248">Derleme ve hello aygıt kodu karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="0a7b5-248">Build and upload hello device code</span></span>

<span data-ttu-id="0a7b5-249">Kullanım `Ctrl+P` (macOS: `Cmd+P`) toorun 'görev aygıt-karşıya yükleme'.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-249">Use `Ctrl+P` (macOS: `Cmd+P`) toorun 'task device-upload'.</span></span> <span data-ttu-id="0a7b5-250">Merhaba terminal, tooenter yapılandırma modu ister.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-250">hello terminal will prompt you tooenter configuration mode.</span></span> <span data-ttu-id="0a7b5-251">toodo, bu nedenle, A düğmesini basılı tutun, ardından itme ve yayın hello Sıfırla düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-251">toodo so, hold down button A, then push and release hello reset button.</span></span> <span data-ttu-id="0a7b5-252">'Configuration' Başlangıç ekranı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-252">hello screen will display 'Configuration'.</span></span> <span data-ttu-id="0a7b5-253">'Görev bulut-provision' adımından alır tooset hello bağlantı dizesi budur.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-253">This is tooset hello connection string that retrieves from 'task cloud-provision' step.</span></span>

<span data-ttu-id="0a7b5-254">Ardından doğrulama ve hello Arduino taslak karşıya yükleme başlar:</span><span class="sxs-lookup"><span data-stu-id="0a7b5-254">Then it will start verifying and uploading hello Arduino sketch:</span></span>

![Mini-solution aygıt-karşıya yükleme](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

<span data-ttu-id="0a7b5-256">Merhaba DevKit yeniden başlatın ve hello kodu çalıştırma başlatın.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-256">hello DevKit will reboot and start running hello code.</span></span>

## <a name="test-hello-project"></a><span data-ttu-id="0a7b5-257">Test hello projesi</span><span class="sxs-lookup"><span data-stu-id="0a7b5-257">Test hello project</span></span>

<span data-ttu-id="0a7b5-258">VS Code'da hello durum çubuğu tooopen hello seri İzleyicisi Merhaba güç Tak simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-258">In VS Code, click hello power plug icon on hello status bar tooopen hello Serial Monitor.</span></span>

<span data-ttu-id="0a7b5-259">sonuçları aşağıdaki hello gördüğünüzde hello örnek uygulama başarıyla çalıştırma:</span><span class="sxs-lookup"><span data-stu-id="0a7b5-259">hello sample application is running successfully when you see hello following results:</span></span>

* <span data-ttu-id="0a7b5-260">Merhaba seri İzleyici görüntüler hello ekran görüntüsü hello içeriği aynı bilgileri hello.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-260">hello Serial Monitor displays hello same information as hello content in hello screenshot below.</span></span>
* <span data-ttu-id="0a7b5-261">Merhaba LED MXChip IOT DevKit üzerinde yanıp sönen.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-261">hello LED on MXChip IoT DevKit is blinking.</span></span>

![VS code'da son çıktı](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a><span data-ttu-id="0a7b5-263">Sorunları ve geri bildirim</span><span class="sxs-lookup"><span data-stu-id="0a7b5-263">Problems and feedback</span></span>

<span data-ttu-id="0a7b5-264">Bulabileceğiniz [SSS](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) sorunlarla ya da kanalları hello aşağıdaki toous ulaşın.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-264">You can find [FAQs](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) if you encounter problems or reach out toous from hello channels below.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a7b5-265">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0a7b5-265">Next steps</span></span>

<span data-ttu-id="0a7b5-266">MXChip IOT DevKit tooyour IOT hub'ı başarıyla bağlandı ve gönderilen hello algılayıcı verileri tooyour IOT hub'ı yakalanan.</span><span class="sxs-lookup"><span data-stu-id="0a7b5-266">You have successfully connected an MXChip IoT DevKit tooyour IoT Hub, and sent hello captured sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="0a7b5-267">Başlarken toocontinue IOT Hub ve tooexplore diğer IOT senaryolarını bakın:</span><span class="sxs-lookup"><span data-stu-id="0a7b5-267">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

- [<span data-ttu-id="0a7b5-268">iothub-explorer ile bulut cihaz mesajlaşmasını yönetme</span><span class="sxs-lookup"><span data-stu-id="0a7b5-268">Manage cloud device messaging with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [<span data-ttu-id="0a7b5-269">IOT hub'ı iletileri tooAzure veri depolama Kaydet</span><span class="sxs-lookup"><span data-stu-id="0a7b5-269">Save IoT Hub messages tooAzure data storage</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [<span data-ttu-id="0a7b5-270">Power BI toovisualize gerçek zamanlı algılayıcı verileri Azure IOT hub'ı kullanın</span><span class="sxs-lookup"><span data-stu-id="0a7b5-270">Use Power BI toovisualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [<span data-ttu-id="0a7b5-271">Azure Web Apps toovisualize gerçek zamanlı algılayıcı verileri Azure IOT hub'ı kullanın</span><span class="sxs-lookup"><span data-stu-id="0a7b5-271">Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [<span data-ttu-id="0a7b5-272">IOT hub'ınızı hello algılayıcı verilerini Azure Machine Learning kullanarak hava durumu tahmini</span><span class="sxs-lookup"><span data-stu-id="0a7b5-272">Weather forecast using hello sensor data from your IoT hub in Azure Machine Learning</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [<span data-ttu-id="0a7b5-273">iothub-explorer ile cihaz yönetimi</span><span class="sxs-lookup"><span data-stu-id="0a7b5-273">Device management with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- [<span data-ttu-id="0a7b5-274">Logic Apps ile uzaktan izleme ve bildirimler</span><span class="sxs-lookup"><span data-stu-id="0a7b5-274">Remote monitoring and notifications with Logic Apps</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps)