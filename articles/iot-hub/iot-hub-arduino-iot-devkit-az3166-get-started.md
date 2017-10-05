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
# <a name="connect-iot-devkit-az3166-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="829ec-103">Bulutta Azure IOT Hub'ına IOT DevKit AZ3166 Bağlan</span><span class="sxs-lookup"><span data-stu-id="829ec-103">Connect IoT DevKit AZ3166 to Azure IoT Hub in the cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="829ec-104">[MXChip IOT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) geliştirmek için kullanılan ve Microsoft Azure hizmetlerini yararlanarak prototip nesnelerin interneti (IOT) çözümler.</span><span class="sxs-lookup"><span data-stu-id="829ec-104">The [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) can be used to develop and prototype Internet of Things (IoT) solutions leveraging Microsoft Azure services.</span></span> <span data-ttu-id="829ec-105">Zengin çevre algılayıcılar, bir açık kaynak tablosu paketi ve bir büyüyen bir Arduino uyumlu panosuna içeren [projeleri katalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).</span><span class="sxs-lookup"><span data-stu-id="829ec-105">It includes an Arduino compatible board with rich peripherals and sensors, an open-source board package and a growing [projects catalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="829ec-106">Neler</span><span class="sxs-lookup"><span data-stu-id="829ec-106">What you do</span></span>
<span data-ttu-id="829ec-107">Bağlantı [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) , oluşturduğunuz bir Azure IOT hub'ına sıcaklık ve nem veri algılayıcı verilerini toplar ve IOT hub'ına gönderir.</span><span class="sxs-lookup"><span data-stu-id="829ec-107">Connect [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) to an Azure IoT hub that you create, collect the temperature and humidity data from sensors and send the data to IoT hub.</span></span>

<span data-ttu-id="829ec-108">Bir DevKit henüz yok mu?</span><span class="sxs-lookup"><span data-stu-id="829ec-108">Don't have a DevKit yet?</span></span> <span data-ttu-id="829ec-109">Yeni bir tane almak [burada](https://aka.ms/iot-devkit-purchase).</span><span class="sxs-lookup"><span data-stu-id="829ec-109">Get a new one [here](https://aka.ms/iot-devkit-purchase).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="829ec-110">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="829ec-110">What you learn</span></span>

* <span data-ttu-id="829ec-111">Nasıl IOT DevKit kablosuz erişim noktasına bağlanmak ve geliştirme ortamınızı hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="829ec-111">How to connect IoT DevKit to Wireless access point and prepare your development environment.</span></span>
* <span data-ttu-id="829ec-112">IOT hub'ı oluşturma ve MXChip IOT DevKit için bir cihaz kaydetme hakkında.</span><span class="sxs-lookup"><span data-stu-id="829ec-112">How to create an IoT hub and register a device for MXChip IoT DevKit.</span></span>
* <span data-ttu-id="829ec-113">Örnek bir uygulama üzerinde MXChip IOT DevKit çalıştırarak algılayıcı verilerini toplamak nasıl.</span><span class="sxs-lookup"><span data-stu-id="829ec-113">How to collect sensor data by running a sample application on MXChip IoT DevKit.</span></span>
* <span data-ttu-id="829ec-114">IOT hub'ınıza algılayıcı verileri göndermek nasıl.</span><span class="sxs-lookup"><span data-stu-id="829ec-114">How to send the sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="829ec-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="829ec-115">What you need</span></span>

* <span data-ttu-id="829ec-116">MXChip IOT DevKit kartı mikro USB kablosu ile.</span><span class="sxs-lookup"><span data-stu-id="829ec-116">An MXChip IoT DevKit board with a micro USB cable.</span></span> [<span data-ttu-id="829ec-117">Şimdi alın</span><span class="sxs-lookup"><span data-stu-id="829ec-117">Get it now</span></span>](https://aka.ms/iot-devkit-purchase)
* <span data-ttu-id="829ec-118">Windows 10 veya macOS 10.10 + çalıştıran bir bilgisayar</span><span class="sxs-lookup"><span data-stu-id="829ec-118">A computer running Windows 10 or macOS 10.10+</span></span>
* <span data-ttu-id="829ec-119">Etkin bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="829ec-119">An active Azure subscription</span></span>
  * <span data-ttu-id="829ec-120">Etkinleştirme bir [Ücretsiz 30 günlük deneme Microsoft Azure hesabı](https://azureinfo.microsoft.com/us-freetrial.html)</span><span class="sxs-lookup"><span data-stu-id="829ec-120">Activate a [free 30-day trial Microsoft Azure account](https://azureinfo.microsoft.com/us-freetrial.html)</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="829ec-121">Donanımınızın hazırlama</span><span class="sxs-lookup"><span data-stu-id="829ec-121">Prepare your hardware</span></span>

<span data-ttu-id="829ec-122">Donanım bilgisayarınıza bağlayın.</span><span class="sxs-lookup"><span data-stu-id="829ec-122">Hook up the hardware to your computer.</span></span>

### <a name="hardware-you-need"></a><span data-ttu-id="829ec-123">Gereksinim duyduğunuz donanım</span><span class="sxs-lookup"><span data-stu-id="829ec-123">Hardware you need</span></span>

* <span data-ttu-id="829ec-124">DevKit Panosu</span><span class="sxs-lookup"><span data-stu-id="829ec-124">DevKit board</span></span>
* <span data-ttu-id="829ec-125">Mikro USB kablosu</span><span class="sxs-lookup"><span data-stu-id="829ec-125">Micro USB cable</span></span>

![alma başlatıldı-donanım](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

### <a name="connect-devkit-to-your-computer"></a><span data-ttu-id="829ec-127">DevKit bilgisayarınıza bağlayın</span><span class="sxs-lookup"><span data-stu-id="829ec-127">Connect DevKit to your computer</span></span>

1. <span data-ttu-id="829ec-128">USB son PC'nize bağlayın</span><span class="sxs-lookup"><span data-stu-id="829ec-128">Connect USB end to your PC</span></span>
2. <span data-ttu-id="829ec-129">Mikro USB son DevKit Bağlan</span><span class="sxs-lookup"><span data-stu-id="829ec-129">Connect Micro USB end to the DevKit</span></span>
3. <span data-ttu-id="829ec-130">Bağlantı Güç yanındaki yeşil LED onaylar</span><span class="sxs-lookup"><span data-stu-id="829ec-130">The green LED next to power confirms connection</span></span>

![alma-başlatıldı-Bağlan](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wifi"></a><span data-ttu-id="829ec-132">WiFi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="829ec-132">Configure WiFi</span></span>

<span data-ttu-id="829ec-133">IOT projelerinin Internet bağlantısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="829ec-133">IoT projects rely on Internet connectivity.</span></span> <span data-ttu-id="829ec-134">WiFi için bağlanmak için DevKit yapılandırmak için aşağıdaki yönergeleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="829ec-134">Use the following instructions to configure the DevKit to connect to WiFi.</span></span>

### <a name="enter-ap-mode"></a><span data-ttu-id="829ec-135">AP modu girin</span><span class="sxs-lookup"><span data-stu-id="829ec-135">Enter AP Mode</span></span>

<span data-ttu-id="829ec-136">B düğmesini basılı tutun itme ve Sıfırla düğmesini bırakın, sonra düğmesini B. bırakın DevKit WiFi yapılandırmak için AP moduna girer.</span><span class="sxs-lookup"><span data-stu-id="829ec-136">Hold down button B, then push and release the reset button, then release button B. Your DevKit will enter AP Mode for configuring WiFi.</span></span> <span data-ttu-id="829ec-137">Ekran hizmet ayarlamak Identifier(SSID) DevKit yanı sıra yapılandırma portalı IP adresini görüntüler:</span><span class="sxs-lookup"><span data-stu-id="829ec-137">The screen will display the Service Set Identifier(SSID) of the DevKit as well as the configuration portal IP address:</span></span>

![alma-başlatıldı-wifi-ap](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-to-devkit-ap"></a><span data-ttu-id="829ec-139">DevKit AP Bağlan</span><span class="sxs-lookup"><span data-stu-id="829ec-139">Connect to DevKit AP</span></span>

<span data-ttu-id="829ec-140">Şimdi, başka bir WiFi Etkin aygıt (PC veya cep telefonu) (yukarıdaki ekran görüntüsünde vurgulanan) DevKit SSID bağlanmak için parolayı boş bırakın kullanın.</span><span class="sxs-lookup"><span data-stu-id="829ec-140">Now, use another WiFi enabled device (PC or mobile phone) to connect to the DevKit SSID (highlighted in the screenshot above), leave the password empty.</span></span>

![alma-başlatıldı-SSID](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wifi-for-devkit"></a><span data-ttu-id="829ec-142">WiFi DevKit için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="829ec-142">Configure WiFi for DevKit</span></span>

<span data-ttu-id="829ec-143">PC veya cep telefonu tarayıcınız DevKit ekranda gösterilen IP adresini açın, bağlanmak için DevKit WiFi ağı seçin ve sonra parolayı yazın.</span><span class="sxs-lookup"><span data-stu-id="829ec-143">Open the IP address shown on the DevKit screen on your PC or mobile phone browser, select the WiFi network you want the DevKit to connect to, then type the password.</span></span> <span data-ttu-id="829ec-144">Tıklatın **Bağlan** tamamlamak için:</span><span class="sxs-lookup"><span data-stu-id="829ec-144">Click **Connect** to complete:</span></span>

![alma başlatıldı-wifi-portal](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

<span data-ttu-id="829ec-146">Bağlantı başarılı olduktan sonra DevKit birkaç saniye içinde yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="829ec-146">Once the connection succeeds, the DevKit will reboot in a few seconds.</span></span> <span data-ttu-id="829ec-147">Başarılı olursa WiFi adı ve IP adresi ekranda görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="829ec-147">If succeeded, you will see the WiFi name and IP address on the screen:</span></span>

![alma başlatıldı-wifi-IP](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
<span data-ttu-id="829ec-149">Fotoğrafın görüntülenen IP adresi atanır ve DevKit ekranda görüntülenen gerçek IP eşleşmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="829ec-149">The IP address displayed in the photo may not match the actual IP assigned and displayed on the DevKit screen.</span></span> <span data-ttu-id="829ec-150">WiFi IP'leri dinamik olarak atamak için DHCP kullanır, bu normaldir.</span><span class="sxs-lookup"><span data-stu-id="829ec-150">This is normal as WiFi uses DHCP to dynamically assign IPs.</span></span>

<span data-ttu-id="829ec-151">WiFi yapılandırıldıktan sonra kimlik bilgilerinizi bu bağlantı için cihazda takılı olsa bile kalıcı.</span><span class="sxs-lookup"><span data-stu-id="829ec-151">After WiFi is configured, your credentials will be persisted on the device for that connection, even if unplugged.</span></span> <span data-ttu-id="829ec-152">Örneğin, DevKit evinizde WiFi için yapılandırılmış ve ardından DevKit ofise sürdü, AP modu yeniden yapılandırmanız gerekecektir (adımda başlangıç **girin AP modu**), office WiFi DevKit bağlanmak için.</span><span class="sxs-lookup"><span data-stu-id="829ec-152">For example, if you configured the DevKit for WiFi in your home and then took the DevKit to the office, you will need to reconfigure AP mode (starting at step **Enter AP Mode**) to connect the DevKit to your office WiFi.</span></span> 

## <a name="start-using-devkit"></a><span data-ttu-id="829ec-153">DevKit kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="829ec-153">Start using DevKit</span></span>

<span data-ttu-id="829ec-154">DevKit üzerinde çalışan varsayılan uygulama en son bellenim sürümünü denetleyin ve sizin için bazı algılayıcı tanılama verilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="829ec-154">The default app running on DevKit will check the latest version of the firmware and display some sensor diagnosis data for you.</span></span>

### <a name="upgrade-to-the-latest-firmware"></a><span data-ttu-id="829ec-155">En son bellenim yükseltme</span><span class="sxs-lookup"><span data-stu-id="829ec-155">Upgrade to the latest firmware</span></span>

<span data-ttu-id="829ec-156">Bir yükseltme ise hem geçerli ve en son bellenim sürümünü gerekli ekranda istenir.</span><span class="sxs-lookup"><span data-stu-id="829ec-156">You will be prompted on the screen both the current and latest firmware version if there is an upgrade needed.</span></span> <span data-ttu-id="829ec-157">İzleyin [yükseltme bellenim](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) Yükseltme Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="829ec-157">Follow [Upgrade firmware](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) guide to upgrade it.</span></span>

![alma-başlatıldı-üretici yazılımı](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
<span data-ttu-id="829ec-159">Bu DevKit üzerinde geliştirme başladıktan sonra bir kerelik çaba ve uygulamanızı karşıya yükleme, uygulamanızla gelen en son üretici yazılımına sahip olur.</span><span class="sxs-lookup"><span data-stu-id="829ec-159">This is a one-time effort, once you start developing on the DevKit and upload your app, you will have the latest firmware come with your app.</span></span>

### <a name="test-various-sensors"></a><span data-ttu-id="829ec-160">Çeşitli algılayıcılar test</span><span class="sxs-lookup"><span data-stu-id="829ec-160">Test various sensors</span></span>

<span data-ttu-id="829ec-161">Algılayıcılar test, tuşuna basarak ve her algılayıcı arasında geçiş yapmak için B düğmesini bırakmadan devam etmek için B düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="829ec-161">Press button B to test sensors, continue pressing and releasing the B button to cycle through each sensor.</span></span>

![alma-başlatıldı-algılayıcılar](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-development-environment"></a><span data-ttu-id="829ec-163">Geliştirme ortamını hazırlayın</span><span class="sxs-lookup"><span data-stu-id="829ec-163">Prepare development environment</span></span>

<span data-ttu-id="829ec-164">Geliştirme ortamını ayarlama şimdi: araçlar ve etkileyici IOT uygulamalar oluşturmanızı paketleri.</span><span class="sxs-lookup"><span data-stu-id="829ec-164">Now it's time to set up the development environment: tools and packages for you to build stunning IoT applications.</span></span> <span data-ttu-id="829ec-165">Windows veya macOS sürüm işletim sisteminize göre seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="829ec-165">You can choose Windows or macOS version according to your operating system.</span></span>


### <a name="windows"></a><span data-ttu-id="829ec-166">Windows</span><span class="sxs-lookup"><span data-stu-id="829ec-166">Windows</span></span>

<span data-ttu-id="829ec-167">Geliştirme ortamı hazırlamak için yükleme paketi kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="829ec-167">We encourage you to use the installation package to prepare the development environment.</span></span> <span data-ttu-id="829ec-168">Herhangi bir sorunla karşılaşırsanız, takip edebilirsiniz [el ile yapılacak adımlar](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) bitti elde edin.</span><span class="sxs-lookup"><span data-stu-id="829ec-168">If you encounter any issues, you can follow the [manual steps](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) to get it done.</span></span>

#### <a name="download-latest-package"></a><span data-ttu-id="829ec-169">Son paketini indirin</span><span class="sxs-lookup"><span data-stu-id="829ec-169">Download latest package</span></span>

<span data-ttu-id="829ec-170">`.zip` Karşıdan dosya tüm gerekli araçları ve DevKit geliştirme için gerekli paketleri içerir.</span><span class="sxs-lookup"><span data-stu-id="829ec-170">The `.zip` file you download contains all necessary tools and packages required for DevKit development.</span></span>

> [!div class="button"]
[<span data-ttu-id="829ec-171">İndir</span><span class="sxs-lookup"><span data-stu-id="829ec-171">Download</span></span>](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


> [!NOTE] 
> <span data-ttu-id="829ec-172">`.zip` Dosyası aşağıdaki araçları ve paketleri içerir.</span><span class="sxs-lookup"><span data-stu-id="829ec-172">The `.zip` file contains the following tools and packages.</span></span> <span data-ttu-id="829ec-173">Bazı bileşenleri yüklü zaten varsa, betik algılamak ve onları atlayın.</span><span class="sxs-lookup"><span data-stu-id="829ec-173">If you already have some components installed, the script will detect and skip them.</span></span>
> * <span data-ttu-id="829ec-174">Node.js ve Yarn: otomatik görevler ve Kurulum komut dosyası için çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="829ec-174">Node.js and Yarn: Runtime for the setup script and automated tasks</span></span>
> * <span data-ttu-id="829ec-175">[Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) -platformlar arası komut satırı deneyimi Azure kaynaklarını yönetmek için MSI bağımlı Python ve PIP içerir.</span><span class="sxs-lookup"><span data-stu-id="829ec-175">[Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) - Cross-platform command-line experience for managing Azure resources, the MSI contains dependent Python and pip.</span></span>
> * <span data-ttu-id="829ec-176">[Visual Studio Code](https://code.visualstudio.com/): DevKit geliştirme için basit Kod Düzenleyicisi</span><span class="sxs-lookup"><span data-stu-id="829ec-176">[Visual Studio Code](https://code.visualstudio.com/): Lightweight code editor for DevKit development</span></span>
> * <span data-ttu-id="829ec-177">[Visual Studio Code uzantısı Arduino için](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): VS code'da sağlayan Arduino geliştirme</span><span class="sxs-lookup"><span data-stu-id="829ec-177">[Visual Studio Code extension for Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): Enables Arduino development in VS Code</span></span>
> * <span data-ttu-id="829ec-178">[Arduino IDE](https://www.arduino.cc/en/Main/Software): Bu araç hakkında Arduino uzantısı kullanır</span><span class="sxs-lookup"><span data-stu-id="829ec-178">[Arduino IDE](https://www.arduino.cc/en/Main/Software): The extension for Arduino relies on this tool</span></span>
> * <span data-ttu-id="829ec-179">DevKit Panosu paketi: Aracı zincirleri, kitaplıklar ve DevKit projeleri</span><span class="sxs-lookup"><span data-stu-id="829ec-179">DevKit Board Package: Tool chains, libraries and projects for the DevKit</span></span>
> * <span data-ttu-id="829ec-180">ST bağlantı yardımcı programı: Gerekli yardımcı programları ve sürücüleri</span><span class="sxs-lookup"><span data-stu-id="829ec-180">ST-Link Utility: Essential utilities and drivers</span></span>

#### <a name="run-installation-script"></a><span data-ttu-id="829ec-181">Yükleme komut dosyasını çalıştır</span><span class="sxs-lookup"><span data-stu-id="829ec-181">Run installation script</span></span>

<span data-ttu-id="829ec-182">Windows dosya Gezgini'nde bulun `.zip` ve ayıklayın, Bul `install.cmd`seçin ve sağ tıklatıp **"Yönetici olarak çalıştır"** başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="829ec-182">In Windows File Explorer, locate the `.zip` and extract it, find `install.cmd`, right-click and select **"Run as administrator"** to start.</span></span>

![alma başlatıldı-Çalıştır-yönetici](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

<span data-ttu-id="829ec-184">Yükleme sırasında her aracı veya paket ilerlemesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="829ec-184">During installation, you will see the progress of each tool or package.</span></span>

![alma başlatıldı-yükleme](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="confirm-to-install-drivers"></a><span data-ttu-id="829ec-186">Sürücüleri yüklemek için Onayla</span><span class="sxs-lookup"><span data-stu-id="829ec-186">Confirm to install drivers</span></span>

<span data-ttu-id="829ec-187">VS Code'da Arduino uzantısı Arduino IDE üzerinde kullanır.</span><span class="sxs-lookup"><span data-stu-id="829ec-187">The VS Code for Arduino extension relies on the Arduino IDE.</span></span> <span data-ttu-id="829ec-188">Arduino IDE yüklediğiniz ilk kez kullanıyorsanız, ilgili sürücüleri yüklemeniz istenir:</span><span class="sxs-lookup"><span data-stu-id="829ec-188">If this is the first time you are installing the Arduino IDE, you will be prompted to install relevant drivers:</span></span>

![alma başlatıldı-sürücü](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

<span data-ttu-id="829ec-190">Internet hızınıza bağlı olarak yüklemeyi tamamlamak için yaklaşık 10 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="829ec-190">It should take around 10 minutes to finish installation depending on your Internet speed.</span></span> <span data-ttu-id="829ec-191">Yükleme tamamlandıktan sonra masaüstünüzde Visual Studio Code ve Arduino IDE kısayolları görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="829ec-191">Once the installation is complete, you should see Visual Studio Code and Arduino IDE shortcuts on your desktop.</span></span>

> [!NOTE] 
<span data-ttu-id="829ec-192">Bazen, VS Code'u başlatın, Arduino IDE veya ilgili Panosu paketi bulamıyor bir hata ile istenir.</span><span class="sxs-lookup"><span data-stu-id="829ec-192">Occasionally, when you launch VS Code, you will be prompted with an error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="829ec-193">Çözmek VS Code kapatmak için bir kez Arduino IDE başlatma ve VS Code Arduino IDE yolu doğru bulun.</span><span class="sxs-lookup"><span data-stu-id="829ec-193">To solve it, close VS Code, launch Arduino IDE once and VS Code should locate Arduino IDE path correctly.</span></span>


### <a name="macos-preview"></a><span data-ttu-id="829ec-194">macOS (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="829ec-194">macOS (Preview)</span></span>

<span data-ttu-id="829ec-195">MacOS geliştirme ortamında hazırlamak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="829ec-195">Follow these steps to prepare development environment on macOS.</span></span>

#### <a name="install-azure-cli-20"></a><span data-ttu-id="829ec-196">Azure CLI 2.0’ı yükleme</span><span class="sxs-lookup"><span data-stu-id="829ec-196">Install Azure CLI 2.0</span></span>

<span data-ttu-id="829ec-197">İzleyin [resmi Kılavuzu](https://docs.microsoft.com//cli/azure/install-azure-cli) Azure CLI 2.0 yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="829ec-197">Follow the [official guide](https://docs.microsoft.com//cli/azure/install-azure-cli) to install Azure CLI 2.0:</span></span>

<span data-ttu-id="829ec-198">Azure CLI 2.0 yüklemek `curl` komutu:</span><span class="sxs-lookup"><span data-stu-id="829ec-198">Install Azure CLI 2.0 with one `curl` command:</span></span>

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="829ec-199">Ve değişikliklerin etkili olması, komut kabuğu yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="829ec-199">And restart your command shell for changes to take effect:</span></span>

```bash
exec -l $SHELL
```

#### <a name="install-arduino-ide"></a><span data-ttu-id="829ec-200">Arduino IDE yükleyin</span><span class="sxs-lookup"><span data-stu-id="829ec-200">Install Arduino IDE</span></span>

<span data-ttu-id="829ec-201">Visual Studio kod Arduino uzantısı Arduino IDE üzerinde kullanır.</span><span class="sxs-lookup"><span data-stu-id="829ec-201">The Visual Studio Code Arduino extension relies on the Arduino IDE.</span></span> <span data-ttu-id="829ec-202">İndirme ve yükleme [macOS Arduino IDE](https://www.arduino.cc/en/Main/Software).</span><span class="sxs-lookup"><span data-stu-id="829ec-202">Download and install the [Arduino IDE for macOS](https://www.arduino.cc/en/Main/Software).</span></span>

#### <a name="install-visual-studio-code"></a><span data-ttu-id="829ec-203">Visual Studio Kodu'nu yükle</span><span class="sxs-lookup"><span data-stu-id="829ec-203">Install Visual Studio Code</span></span>

<span data-ttu-id="829ec-204">İndirme ve yükleme [macOS için Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="829ec-204">Download and install [Visual Studio Code for macOS](https://code.visualstudio.com/).</span></span> <span data-ttu-id="829ec-205">Bu DevKit IOT uygulamaları oluşturmak için birincil geliştirme aracı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="829ec-205">This will be the primary development tool for building DevKit IoT applications.</span></span>

####  <a name="download-latest-package"></a><span data-ttu-id="829ec-206">Son paketini indirin</span><span class="sxs-lookup"><span data-stu-id="829ec-206">Download latest package</span></span>

1. <span data-ttu-id="829ec-207">Node.js yükleyin.</span><span class="sxs-lookup"><span data-stu-id="829ec-207">Install Node.js.</span></span> <span data-ttu-id="829ec-208">Popüler macOS Paket Yöneticisi'ni kullanabilirsiniz [Homebrew](https://brew.sh/) veya [yükleyici önceden oluşturulmuş](https://nodejs.org/en/download/) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="829ec-208">You can use popular macOS package manager [Homebrew](https://brew.sh/) or [pre-built installer](https://nodejs.org/en/download/) to install it.</span></span>

2. <span data-ttu-id="829ec-209">Karşıdan `.zip` VS Code DevKit geliştirme için gerekli görev komut dosyalarını içeren dosya.</span><span class="sxs-lookup"><span data-stu-id="829ec-209">Download `.zip` file containing task scripts required for DevKit development in VS Code.</span></span>

   > [!div class="button"]
   [<span data-ttu-id="829ec-210">İndir</span><span class="sxs-lookup"><span data-stu-id="829ec-210">Download</span></span>](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

   <span data-ttu-id="829ec-211">Bulun `.zip` ve ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="829ec-211">Locate the `.zip` and extract it.</span></span> <span data-ttu-id="829ec-212">Ardından başlatma **Terminal** uygulama ve yapılandırmak için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="829ec-212">Then launch **Terminal** app and run the following commands to configure:</span></span>

   <span data-ttu-id="829ec-213">MacOS kullanıcı klasörünüze ayıklanan klasörü Taşı:</span><span class="sxs-lookup"><span data-stu-id="829ec-213">Move extracted folder to your macOS user folder:</span></span>
   ```bash
   mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
   ```
  
   <span data-ttu-id="829ec-214">Yükleme `npm` paketler:</span><span class="sxs-lookup"><span data-stu-id="829ec-214">Install `npm` packages:</span></span>
   ```
   npm install
   ```

#### <a name="install-vs-code-extension-for-arduino"></a><span data-ttu-id="829ec-215">VS Code uzantısını Arduino için yükleyin</span><span class="sxs-lookup"><span data-stu-id="829ec-215">Install VS Code extension for Arduino</span></span>

<span data-ttu-id="829ec-216">Visual Studio Code Market uzantılar doğrudan aracı yükleme, soldaki menüden bölmesinde uzantıları simgesine tıklamanız yeterlidir ve ardından arama olanak tanır `Arduino` yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="829ec-216">Visual Studio Code allows you to install Marketplace extensions directly in the tool, simply click the extensions icon in the left menu pane and then search `Arduino` to install:</span></span>

![Uzantıları Yükleme](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-devkit-board-package"></a><span data-ttu-id="829ec-218">DevKit Panosu paketini yükle</span><span class="sxs-lookup"><span data-stu-id="829ec-218">Install DevKit board package</span></span>

<span data-ttu-id="829ec-219">Visual Studio kodda Panosu Yöneticisi'ni kullanarak DevKit Panosu eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="829ec-219">You will need to add the DevKit board using the Board Manager in Visual Studio Code.</span></span>

1. <span data-ttu-id="829ec-220">Kullanım `Cmd+Shift+P` komutu paleti ve türü çağrılacak **Arduino** ardından bulmak ve seçmek **Arduino: Panosu Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="829ec-220">Use `Cmd+Shift+P` to invoke command palette and type **Arduino** then find and select **Arduino: Board Manager**.</span></span>

2. <span data-ttu-id="829ec-221">Tıklatın **'Ek URL'ler'** sağ alt köşede.</span><span class="sxs-lookup"><span data-stu-id="829ec-221">Click **'Additional URLs'** at the bottom right.</span></span>
   <span data-ttu-id="829ec-222">![Yükleme ek-URL'leri](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span><span class="sxs-lookup"><span data-stu-id="829ec-222">![installation-additional-urls](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span></span>

3. <span data-ttu-id="829ec-223">İçinde `settings.json` dosya, alt kısmında bir satır ekleyin `USER SETTINGS` bölmesi ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="829ec-223">In the `settings.json` file, add a line at the bottom of `USER SETTINGS` pane and save.</span></span>
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![yükleme ayarları json](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. <span data-ttu-id="829ec-225">Şimdi 'az3166 için' Panosu Yöneticisi'nde arayın ve en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="829ec-225">Now in the Board Manager search for 'az3166' and install the latest version.</span></span>
   <span data-ttu-id="829ec-226">![Yükleme az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span><span class="sxs-lookup"><span data-stu-id="829ec-226">![installation-az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span></span>

<span data-ttu-id="829ec-227">Artık tüm gerekli araçları ve macOS için yüklü olan paketleri vardır.</span><span class="sxs-lookup"><span data-stu-id="829ec-227">You now have all the necessary tools and packages installed for macOS.</span></span>


## <a name="open-project-folder"></a><span data-ttu-id="829ec-228">Proje Aç klasörü</span><span class="sxs-lookup"><span data-stu-id="829ec-228">Open project folder</span></span>

### <a name="launch-vs-code"></a><span data-ttu-id="829ec-229">VS Code’u başlatın</span><span class="sxs-lookup"><span data-stu-id="829ec-229">Launch VS Code</span></span>

<span data-ttu-id="829ec-230">DevKit bağlı emin olun.</span><span class="sxs-lookup"><span data-stu-id="829ec-230">Make sure your DevKit is not connected.</span></span> <span data-ttu-id="829ec-231">İlk VS Code'u başlatın ve DevKit bilgisayarınıza bağlayın.</span><span class="sxs-lookup"><span data-stu-id="829ec-231">Launch VS Code first and connect the DevKit to your computer.</span></span> <span data-ttu-id="829ec-232">VS Code otomatik olarak bulmak ve ayarlama giriş sayfası açılır:</span><span class="sxs-lookup"><span data-stu-id="829ec-232">VS Code will automatically find it and pop up an introduction page:</span></span>

![Mini solution vscode](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
<span data-ttu-id="829ec-234">Bazen, VS Code'u başlatın, Arduino IDE veya ilgili Panosu paketi bulunamadı hatasıyla istenir.</span><span class="sxs-lookup"><span data-stu-id="829ec-234">Occasionally, when you launch VS Code, you will be prompted with error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="829ec-235">Çözmek VS Code kapatmak için bir kez yeniden başlatma Arduino IDE ve VS Code Arduino IDE yolu doğru bulun.</span><span class="sxs-lookup"><span data-stu-id="829ec-235">To solve it, close VS Code, launch Arduino IDE once again and VS Code should locate Arduino IDE path correctly.</span></span>

### <a name="open-arduino-examples-folder"></a><span data-ttu-id="829ec-236">Arduino örnekler Klasör Aç</span><span class="sxs-lookup"><span data-stu-id="829ec-236">Open Arduino Examples folder</span></span>

<span data-ttu-id="829ec-237">Geçiş **'Arduino örnekler'** sekmesinde, gitmek `Examples for MXCHIP AZ3166 > AzureIoT` ve tıklayın `GetStarted`.</span><span class="sxs-lookup"><span data-stu-id="829ec-237">Switch to **'Arduino Examples'** tab, navigate to `Examples for MXCHIP AZ3166 > AzureIoT` and click on `GetStarted`.</span></span>

![Mini solution örnekleri](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

<span data-ttu-id="829ec-239">Bölmesini kapatmak için görülüyorsa, yeniden yüklemek için kullanmak `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) komutu paleti ve türü çağrılacak **Arduino** bulmak ve seçmek için **Arduino: örnekler**.</span><span class="sxs-lookup"><span data-stu-id="829ec-239">If you happen to close the pane, to reload it, use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) to invoke command palette and type **Arduino** to find and select **Arduino: Examples**.</span></span>

## <a name="provision-azure-services"></a><span data-ttu-id="829ec-240">Azure hizmetlerini hazırlamanız</span><span class="sxs-lookup"><span data-stu-id="829ec-240">Provision Azure services</span></span>

<span data-ttu-id="829ec-241">Çözüm penceresinde göreviniz çalıştırın `Ctrl+P` (macOS: `Cmd+P`) 'bulut sağlama görev' yazarak:</span><span class="sxs-lookup"><span data-stu-id="829ec-241">In the solution window, run your task through `Ctrl+P` (macOS: `Cmd+P`) by typing 'task cloud-provision':</span></span>

<span data-ttu-id="829ec-242">Terminal VS kodu'nda etkileşimli bir komut satırı, gerekli Azure hizmetleri sağlama aracılığıyla yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="829ec-242">In the VS Code terminal, an interactive command line will guide you through provisioning the required Azure services:</span></span>

![Mini-solution-bulut-sağlama](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-arduino-sketch"></a><span data-ttu-id="829ec-244">Derleme ve Arduino taslak karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="829ec-244">Build and upload Arduino sketch</span></span>

### <a name="install-required-library"></a><span data-ttu-id="829ec-245">Gerekli kitaplığını yükle</span><span class="sxs-lookup"><span data-stu-id="829ec-245">Install required library</span></span>

1. <span data-ttu-id="829ec-246">Tuşuna `F1` veya `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) komutu paleti ve türü çağrılacak **Arduino** ardından bulmak ve seçmek **Arduino: Kitaplığı Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="829ec-246">Press `F1` or `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) to invoke command palette and type **Arduino** then find and select **Arduino: Library Manager**.</span></span>

2. <span data-ttu-id="829ec-247">Arama `ArduinoJson` kitaplığı ve tıklatın **yükleyin**</span><span class="sxs-lookup"><span data-stu-id="829ec-247">Search for `ArduinoJson` library and click **Install**</span></span>

### <a name="build-and-upload-the-device-code"></a><span data-ttu-id="829ec-248">Derleme ve aygıt kodu karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="829ec-248">Build and upload the device code</span></span>

<span data-ttu-id="829ec-249">Kullanım `Ctrl+P` (macOS: `Cmd+P`) 'aygıt karşıya yükleme görev' çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="829ec-249">Use `Ctrl+P` (macOS: `Cmd+P`) to run 'task device-upload'.</span></span> <span data-ttu-id="829ec-250">Terminal yapılandırma modu girmenizi ister.</span><span class="sxs-lookup"><span data-stu-id="829ec-250">The terminal will prompt you to enter configuration mode.</span></span> <span data-ttu-id="829ec-251">Bunu yapmak için A düğmesini basılı tutun sonra push ve Sıfırla düğmesini bırakın.</span><span class="sxs-lookup"><span data-stu-id="829ec-251">To do so, hold down button A, then push and release the reset button.</span></span> <span data-ttu-id="829ec-252">'Configuration' ekranı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="829ec-252">The screen will display 'Configuration'.</span></span> <span data-ttu-id="829ec-253">'Görev bulut-provision' adımından alır bağlantı dizesini ayarlamak için budur.</span><span class="sxs-lookup"><span data-stu-id="829ec-253">This is to set the connection string that retrieves from 'task cloud-provision' step.</span></span>

<span data-ttu-id="829ec-254">Ardından doğrulama ve Arduino taslak karşıya yükleme başlar:</span><span class="sxs-lookup"><span data-stu-id="829ec-254">Then it will start verifying and uploading the Arduino sketch:</span></span>

![Mini-solution aygıt-karşıya yükleme](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

<span data-ttu-id="829ec-256">DevKit yeniden başlatın ve kodu çalıştırma başlatın.</span><span class="sxs-lookup"><span data-stu-id="829ec-256">The DevKit will reboot and start running the code.</span></span>

## <a name="test-the-project"></a><span data-ttu-id="829ec-257">Projeyi test</span><span class="sxs-lookup"><span data-stu-id="829ec-257">Test the project</span></span>

<span data-ttu-id="829ec-258">VS Code'da seri İzleyicisi'ni açmak için durum çubuğunda güç Tak simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="829ec-258">In VS Code, click the power plug icon on the status bar to open the Serial Monitor.</span></span>

<span data-ttu-id="829ec-259">Aşağıdaki sonuçları gördüğünüzde örnek uygulama başarıyla çalıştırma:</span><span class="sxs-lookup"><span data-stu-id="829ec-259">The sample application is running successfully when you see the following results:</span></span>

* <span data-ttu-id="829ec-260">Seri İzleyicisi, aşağıdaki ekran görüntüsünde içerik olarak aynı bilgiyi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="829ec-260">The Serial Monitor displays the same information as the content in the screenshot below.</span></span>
* <span data-ttu-id="829ec-261">LED MXChip IOT DevKit üzerinde yanıp sönen.</span><span class="sxs-lookup"><span data-stu-id="829ec-261">The LED on MXChip IoT DevKit is blinking.</span></span>

![VS code'da son çıktı](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a><span data-ttu-id="829ec-263">Sorunları ve geri bildirim</span><span class="sxs-lookup"><span data-stu-id="829ec-263">Problems and feedback</span></span>

<span data-ttu-id="829ec-264">Bulabileceğiniz [SSS](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) sorunlarla ya da kanaldan bize ulaşın.</span><span class="sxs-lookup"><span data-stu-id="829ec-264">You can find [FAQs](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) if you encounter problems or reach out to us from the channels below.</span></span>

## <a name="next-steps"></a><span data-ttu-id="829ec-265">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="829ec-265">Next steps</span></span>

<span data-ttu-id="829ec-266">Başarıyla MXChip IOT DevKit IOT Hub'ına bağlı ve yakalanan algılayıcı verilerini IOT hub'ına gönderilen.</span><span class="sxs-lookup"><span data-stu-id="829ec-266">You have successfully connected an MXChip IoT DevKit to your IoT Hub, and sent the captured sensor data to your IoT hub.</span></span>

<span data-ttu-id="829ec-267">IoT Hub’ı kullanmaya başlamak ve diğer IoT senaryolarını keşfetmek için bkz:</span><span class="sxs-lookup"><span data-stu-id="829ec-267">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

- [<span data-ttu-id="829ec-268">iothub-explorer ile bulut cihaz mesajlaşmasını yönetme</span><span class="sxs-lookup"><span data-stu-id="829ec-268">Manage cloud device messaging with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [<span data-ttu-id="829ec-269">IoT Hub iletilerini Azure veri depolamaya kaydetme</span><span class="sxs-lookup"><span data-stu-id="829ec-269">Save IoT Hub messages to Azure data storage</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [<span data-ttu-id="829ec-270">Azure IOT hub'ı gerçek zamanlı algılayıcı verilerini görselleştirmek için Power BI kullanın</span><span class="sxs-lookup"><span data-stu-id="829ec-270">Use Power BI to visualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [<span data-ttu-id="829ec-271">Azure IOT hub'ı gerçek zamanlı algılayıcı verilerini görselleştirmek için Azure Web uygulamaları kullanma</span><span class="sxs-lookup"><span data-stu-id="829ec-271">Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [<span data-ttu-id="829ec-272">IOT hub'ınızı algılayıcı verilerini Azure Machine Learning kullanarak tahmin hava durumu</span><span class="sxs-lookup"><span data-stu-id="829ec-272">Weather forecast using the sensor data from your IoT hub in Azure Machine Learning</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [<span data-ttu-id="829ec-273">iothub-explorer ile cihaz yönetimi</span><span class="sxs-lookup"><span data-stu-id="829ec-273">Device management with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- [<span data-ttu-id="829ec-274">Logic Apps ile uzaktan izleme ve bildirimler</span><span class="sxs-lookup"><span data-stu-id="829ec-274">Remote monitoring and notifications with Logic Apps</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps)