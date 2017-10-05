---
title: "Buluta (Node.js) - Azure IOT Hub'ına bağlanmak Raspberry Pi'yi Böğürtlenli Pi | Microsoft Docs"
description: "Azure bulut veri göndermek Raspberry Pi'yi için Azure IOT Hub ile Raspberry Pi'yi bağlayın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure IOT Böğürtlenli PI Böğürtlenli PI IOT hub, bulut için Böğürtlenli pi gönderme, verileri buluta Böğürtlenli pi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/27/2017
ms.author: xshi
ms.openlocfilehash: 956ed5ab0ed38ddebd978b35eb54bc96567f0d57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-nodejs"></a><span data-ttu-id="64ecf-104">Azure IOT Hub (Node.js) Böğürtlenli Pi Bağlan</span><span class="sxs-lookup"><span data-stu-id="64ecf-104">Connect Raspberry Pi to Azure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="64ecf-105">Bu öğreticide, Raspbian çalıştıran Raspberry Pi'yi ile çalışmanın temelleri öğrenerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="64ecf-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="64ecf-106">Daha sonra sorunsuzca aygıtlarınızı buluta kullanarak bağlanmasına nasıl öğrenin [Azure IOT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="64ecf-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="64ecf-107">Windows 10 IOT Core örnekleri için Git [Windows Geliştirme Merkezi](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="64ecf-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="64ecf-108">Bir pakete henüz yok mu?</span><span class="sxs-lookup"><span data-stu-id="64ecf-108">Don't have a kit yet?</span></span> <span data-ttu-id="64ecf-109">Deneyin [Raspberry Pi 3 öykünücü](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/).</span><span class="sxs-lookup"><span data-stu-id="64ecf-109">Try the [Raspberry Pi 3 emulator](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/).</span></span> <span data-ttu-id="64ecf-110">Veya yeni bir paket satın [burada](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="64ecf-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="64ecf-111">Neler</span><span class="sxs-lookup"><span data-stu-id="64ecf-111">What you do</span></span>

* <span data-ttu-id="64ecf-112">Böğürtlenli PI kurulumu.</span><span class="sxs-lookup"><span data-stu-id="64ecf-112">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="64ecf-113">IOT hub'ı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="64ecf-113">Create an IoT hub.</span></span>
* <span data-ttu-id="64ecf-114">Bir cihaz IOT hub'ınıza Pi için kaydetme.</span><span class="sxs-lookup"><span data-stu-id="64ecf-114">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="64ecf-115">Pi algılayıcı verilerini IOT hub'ınıza gönderilecek örnek bir uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="64ecf-115">Run a sample application on Pi to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="64ecf-116">Raspberry Pi'yi, oluşturduğunuz bir IOT hub'ına bağlanın.</span><span class="sxs-lookup"><span data-stu-id="64ecf-116">Connect Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="64ecf-117">Pi BME280 algılayıcı sıcaklık ve nem verileri toplamak için bir örnek uygulamayı çalıştırın. ardından.</span><span class="sxs-lookup"><span data-stu-id="64ecf-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="64ecf-118">Son olarak, IOT hub'ınıza algılayıcı verileri gönderin.</span><span class="sxs-lookup"><span data-stu-id="64ecf-118">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="64ecf-119">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="64ecf-119">What you learn</span></span>

* <span data-ttu-id="64ecf-120">Azure IOT hub oluşturma ve yeni cihaz bağlantı dizenizi elde etme.</span><span class="sxs-lookup"><span data-stu-id="64ecf-120">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="64ecf-121">Pi BME280 algılayıcı ile bağlanma.</span><span class="sxs-lookup"><span data-stu-id="64ecf-121">How to connect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="64ecf-122">Pi üzerinde bir örnek uygulamayı çalıştırarak algılayıcı verilerini toplamak nasıl.</span><span class="sxs-lookup"><span data-stu-id="64ecf-122">How to collect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="64ecf-123">IOT hub'ınıza algılayıcı verileri göndermek nasıl.</span><span class="sxs-lookup"><span data-stu-id="64ecf-123">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="64ecf-124">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="64ecf-124">What you need</span></span>

![Ne gerekiyor](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* <span data-ttu-id="64ecf-126">Raspberry Pi 2 veya Raspberry Pi 3 Panosu.</span><span class="sxs-lookup"><span data-stu-id="64ecf-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="64ecf-127">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="64ecf-127">An active Azure subscription.</span></span> <span data-ttu-id="64ecf-128">Bir Azure hesabınız yoksa [ücretsiz Azure deneme hesabı oluşturma](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="64ecf-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="64ecf-129">Bir izleyici, bir USB klavye ve fare Pi bağlanan.</span><span class="sxs-lookup"><span data-stu-id="64ecf-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span></span>
* <span data-ttu-id="64ecf-130">Mac veya Windows veya Linux çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="64ecf-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="64ecf-131">Bir Internet bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="64ecf-131">An Internet connection.</span></span>
* <span data-ttu-id="64ecf-132">16 GB veya üzeri microSD kartı.</span><span class="sxs-lookup"><span data-stu-id="64ecf-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="64ecf-133">İşletim sistemi görüntüsü microSD kartı üzerine yazmak için bir USB SD bağdaştırıcı veya microSD kartı.</span><span class="sxs-lookup"><span data-stu-id="64ecf-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="64ecf-134">5-volt 2 amp güç 6 kaplama alanı mikro USB kablosu ile sağlayın.</span><span class="sxs-lookup"><span data-stu-id="64ecf-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span></span>

<span data-ttu-id="64ecf-135">Aşağıdaki öğeler isteğe bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="64ecf-135">The following items are optional:</span></span>

* <span data-ttu-id="64ecf-136">Bir birleştirilmiş Adafruit BME280 sıcaklık, baskısı ve nem algılayıcı.</span><span class="sxs-lookup"><span data-stu-id="64ecf-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="64ecf-137">Bir breadboard.</span><span class="sxs-lookup"><span data-stu-id="64ecf-137">A breadboard.</span></span>
* <span data-ttu-id="64ecf-138">6 F/M anahtar kablolarını.</span><span class="sxs-lookup"><span data-stu-id="64ecf-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="64ecf-139">Yayılmış 10 mm LED.</span><span class="sxs-lookup"><span data-stu-id="64ecf-139">A diffused 10-mm LED.</span></span>

  > [!NOTE] 
  <span data-ttu-id="64ecf-140">Kod örneği desteği algılayıcı verilerini benzetimli çünkü bu öğeler isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="64ecf-140">These items are optional because the code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="64ecf-141">Böğürtlenli PI Kurulumu</span><span class="sxs-lookup"><span data-stu-id="64ecf-141">Setup Raspberry Pi</span></span>

### <a name="install-the-raspbian-operating-system-for-pi"></a><span data-ttu-id="64ecf-142">Pi için Raspbian işletim sistemini yükleme</span><span class="sxs-lookup"><span data-stu-id="64ecf-142">Install the Raspbian operating system for Pi</span></span>

<span data-ttu-id="64ecf-143">MicroSD kartı Raspbian görüntünün yüklenmesi için hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="64ecf-143">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="64ecf-144">Raspbian indirin.</span><span class="sxs-lookup"><span data-stu-id="64ecf-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="64ecf-145">[Piksel ile Raspbian Jessie karşıdan](https://www.raspberrypi.org/downloads/raspbian/) (.zip dosyası).</span><span class="sxs-lookup"><span data-stu-id="64ecf-145">[Download Raspbian Jessie with Pixel](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span></span>
   1. <span data-ttu-id="64ecf-146">Raspbian görüntünün bilgisayarınızdaki bir klasöre ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="64ecf-146">Extract the Raspbian image to a folder on your computer.</span></span>
1. <span data-ttu-id="64ecf-147">Raspbian microSD kartı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="64ecf-147">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="64ecf-148">[Etcher SD kart yazıcı yardımcı programı yükleyip](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="64ecf-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="64ecf-149">Etcher çalıştırın ve 1. adımda ayıkladığınız Raspbian görüntüyü seçin.</span><span class="sxs-lookup"><span data-stu-id="64ecf-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="64ecf-150">MicroSD kartı sürücü seçin.</span><span class="sxs-lookup"><span data-stu-id="64ecf-150">Select the microSD card drive.</span></span> <span data-ttu-id="64ecf-151">Etcher zaten doğru sürücü seçmiş olabilirsiniz olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="64ecf-151">Note that Etcher may have already selected the correct drive.</span></span>
   1. <span data-ttu-id="64ecf-152">Raspbian microSD kartı yüklemek için Flash'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="64ecf-152">Click Flash to install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="64ecf-153">Yükleme tamamlandığında microSD kartı bilgisayarınızdan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="64ecf-153">Remove the microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="64ecf-154">Etcher otomatik olarak çıkarır veya tamamlanmasından sonra microSD kartı çıkarır çünkü microSD kartı doğrudan kaldırmak güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="64ecf-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   1. <span data-ttu-id="64ecf-155">MicroSD kartı Pi yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="64ecf-155">Insert the microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="64ecf-156">SSH ve I2C etkinleştir</span><span class="sxs-lookup"><span data-stu-id="64ecf-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="64ecf-157">Monitör, klavye ve fare pi bağlanmak, Pi başlatın ve ardından içinde Raspbian kullanarak oturum `pi` kullanıcı adı ve `raspberry` ve parola olarak.</span><span class="sxs-lookup"><span data-stu-id="64ecf-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span></span>
1. <span data-ttu-id="64ecf-158">Böğürtlenli simgesine tıklayın > **Tercihler** > **Raspberry Pi yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="64ecf-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Raspbian Tercihler menüsü](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="64ecf-160">Üzerinde **arabirimleri** sekmesinde, ayarlamak **I2C** ve **SSH** için **etkinleştirmek**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="64ecf-160">On the **Interfaces** tab, set **I2C** and **SSH** to **Enable**, and then click **OK**.</span></span> <span data-ttu-id="64ecf-161">Fiziksel algılayıcılar varsa ve benzetimli algılayıcı verilerini kullanmak istediğiniz yok, bu adım isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="64ecf-161">If you don't have physical sensors and want to use simulated sensor data, this step is optional.</span></span>

   ![I2C ve Böğürtlenli Pi üzerinde SSH etkinleştir](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="64ecf-163">SSH ve I2C etkinleştirmek için daha fazla başvuru belgeleri bulabilirsiniz [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) ve [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span><span class="sxs-lookup"><span data-stu-id="64ecf-163">To enable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="64ecf-164">Pi algılayıcı Bağlan</span><span class="sxs-lookup"><span data-stu-id="64ecf-164">Connect the sensor to Pi</span></span>

<span data-ttu-id="64ecf-165">Bir LED ve bir BME280 Pi şu şekilde bağlanmak için breadboard ve anahtar kablolarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="64ecf-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span></span> <span data-ttu-id="64ecf-166">Algılayıcı yoksa bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64ecf-166">If you don’t have the sensor, skip this section.</span></span>

![Raspberry Pi'yi ve algılayıcı bağlantısı](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="64ecf-168">BME280 algılayıcı sıcaklık ve nem verileri toplayabilir.</span><span class="sxs-lookup"><span data-stu-id="64ecf-168">The BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="64ecf-169">Ve cihaz ve bulut arasındaki iletişimi ise LED blink.</span><span class="sxs-lookup"><span data-stu-id="64ecf-169">And the LED will blink if there is a communication between device and the cloud.</span></span> 

<span data-ttu-id="64ecf-170">Algılayıcı PIN'ler için aşağıdaki kablolama kullanın:</span><span class="sxs-lookup"><span data-stu-id="64ecf-170">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="64ecf-171">Başlangıç (algılayıcı & LED)</span><span class="sxs-lookup"><span data-stu-id="64ecf-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="64ecf-172">Bitiş (kartı)</span><span class="sxs-lookup"><span data-stu-id="64ecf-172">End (Board)</span></span>            | <span data-ttu-id="64ecf-173">Kablo rengi</span><span class="sxs-lookup"><span data-stu-id="64ecf-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="64ecf-174">VDD (PIN 5G)</span><span class="sxs-lookup"><span data-stu-id="64ecf-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="64ecf-175">3, 3v PWR (PIN 1)</span><span class="sxs-lookup"><span data-stu-id="64ecf-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="64ecf-176">Beyaz kablosu</span><span class="sxs-lookup"><span data-stu-id="64ecf-176">White cable</span></span>   |
| <span data-ttu-id="64ecf-177">GND (PIN 7G)</span><span class="sxs-lookup"><span data-stu-id="64ecf-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="64ecf-178">GND (PIN 6)</span><span class="sxs-lookup"><span data-stu-id="64ecf-178">GND (Pin 6)</span></span>            | <span data-ttu-id="64ecf-179">Kahverengi kablosu</span><span class="sxs-lookup"><span data-stu-id="64ecf-179">Brown cable</span></span>   |
| <span data-ttu-id="64ecf-180">SCK (PIN 8G)</span><span class="sxs-lookup"><span data-stu-id="64ecf-180">SCK (Pin 8G)</span></span>             | <span data-ttu-id="64ecf-181">I2C1 SDA (PIN 3)</span><span class="sxs-lookup"><span data-stu-id="64ecf-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="64ecf-182">Turuncu kablosu</span><span class="sxs-lookup"><span data-stu-id="64ecf-182">Orange cable</span></span>  |
| <span data-ttu-id="64ecf-183">SDI (PIN 10G)</span><span class="sxs-lookup"><span data-stu-id="64ecf-183">SDI (Pin 10G)</span></span>            | <span data-ttu-id="64ecf-184">I2C1 SCL (PIN 5)</span><span class="sxs-lookup"><span data-stu-id="64ecf-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="64ecf-185">Kırmızı kablosu</span><span class="sxs-lookup"><span data-stu-id="64ecf-185">Red cable</span></span>     |
| <span data-ttu-id="64ecf-186">LED VDD (PIN 18F)</span><span class="sxs-lookup"><span data-stu-id="64ecf-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="64ecf-187">GPIO'yu 24 (PIN 18)</span><span class="sxs-lookup"><span data-stu-id="64ecf-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="64ecf-188">Beyaz kablosu</span><span class="sxs-lookup"><span data-stu-id="64ecf-188">White cable</span></span>   |
| <span data-ttu-id="64ecf-189">LED GND (PIN 17F)</span><span class="sxs-lookup"><span data-stu-id="64ecf-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="64ecf-190">GND (PIN 20)</span><span class="sxs-lookup"><span data-stu-id="64ecf-190">GND (Pin 20)</span></span>           | <span data-ttu-id="64ecf-191">Siyah kablosu</span><span class="sxs-lookup"><span data-stu-id="64ecf-191">Black cable</span></span>   |

<span data-ttu-id="64ecf-192">Görüntülemek için tıklatın [Raspberry Pi 2 ve 3 PIN eşlemeleri](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) daha sonra başvurmak üzere.</span><span class="sxs-lookup"><span data-stu-id="64ecf-192">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="64ecf-193">Raspberry Pi'yi BME280 başarıyla bağlandıktan sonra görüntü gibi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="64ecf-193">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span></span>

![Bağlı Pi ve BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a><span data-ttu-id="64ecf-195">Pi ağa bağlanın</span><span class="sxs-lookup"><span data-stu-id="64ecf-195">Connect Pi to the network</span></span>

<span data-ttu-id="64ecf-196">Pi üzerinde mikro USB kablosu ve güç kaynağı kullanarak açın.</span><span class="sxs-lookup"><span data-stu-id="64ecf-196">Turn on Pi by using the micro USB cable and the power supply.</span></span> <span data-ttu-id="64ecf-197">Pi kablolu ağa bağlanın veya izleyin için Ethernet kablosu kullanın [Raspberry Pi Foundation yönergeleri](https://www.raspberrypi.org/learning/software-guide/wifi/) Pi kablosuz ağınıza bağlanmak için.</span><span class="sxs-lookup"><span data-stu-id="64ecf-197">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span></span> <span data-ttu-id="64ecf-198">Not yapmanıza gerek, Pi ağa başarıyla bağlandı sonra [IP adresi, pi'nin](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="64ecf-198">After your Pi has been successfully connected to the network, you need to take a note of the [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Kablolu ağa bağlı](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="64ecf-200">Pi bilgisayarınızın aynı ağa bağlı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="64ecf-200">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="64ecf-201">Örneğin, pi kablolu bir ağa bağlıyken, bilgisayarınızın kablosuz bir ağa bağlıysa, IP adresi devdisco çıkışı göremeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64ecf-201">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="64ecf-202">Pi üzerinde bir örnek uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="64ecf-202">Run a sample application on Pi</span></span>

### <a name="clone-sample-application-and-install-the-prerequisite-packages"></a><span data-ttu-id="64ecf-203">Örnek uygulama kopyalamak ve önkoşul yükleyin</span><span class="sxs-lookup"><span data-stu-id="64ecf-203">Clone sample application and install the prerequisite packages</span></span>

1. <span data-ttu-id="64ecf-204">Raspberry Pi'yi bağlanmak için ana bilgisayarınız aşağıdaki SSH istemcilerden birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="64ecf-204">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span></span>
    - <span data-ttu-id="64ecf-205">[PuTTY](http://www.putty.org/) Windows için.</span><span class="sxs-lookup"><span data-stu-id="64ecf-205">[PuTTY](http://www.putty.org/) for Windows.</span></span> <span data-ttu-id="64ecf-206">SSH bağlanmak için Pi IP adresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="64ecf-206">You need the IP address of your Pi to connect it via SSH.</span></span>
    - <span data-ttu-id="64ecf-207">Ubuntu veya macOS üzerindeki yerleşik SSH istemcisi.</span><span class="sxs-lookup"><span data-stu-id="64ecf-207">The built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="64ecf-208">Çalıştırma `ssh pi@<ip address of pi>` Pi SSH aracılığıyla bağlanmak için.</span><span class="sxs-lookup"><span data-stu-id="64ecf-208">You might need run `ssh pi@<ip address of pi>` to connect Pi via SSH.</span></span>

   > [!NOTE] 
   <span data-ttu-id="64ecf-209">Varsayılan kullanıcı adı `pi` , ve parola `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="64ecf-209">The default username is `pi` , and the password is `raspberry`.</span></span>

1. <span data-ttu-id="64ecf-210">Node.js ve NPM, Pi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="64ecf-210">Install Node.js and NPM to your Pi.</span></span>
   
   <span data-ttu-id="64ecf-211">Önce aşağıdaki komutu kullanarak, Node.js sürümünü kontrol etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="64ecf-211">First you should check your Node.js version with the following command.</span></span> 
   
   ```bash
   node -v
   ```

   <span data-ttu-id="64ecf-212">Sürüm 4.x düşük olduğu veya, Pi üzerinde hiçbir Node.js yüklemek veya Node.js güncelleştirmek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="64ecf-212">If the version is lower than 4.x or there is no Node.js on your Pi, then run the following command to install or update Node.js.</span></span>

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. <span data-ttu-id="64ecf-213">Örnek uygulama, aşağıdaki komutu çalıştırarak kopyalama:</span><span class="sxs-lookup"><span data-stu-id="64ecf-213">Clone the sample application by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. <span data-ttu-id="64ecf-214">Tüm paketler aşağıdaki komutu tarafından yükleyin.</span><span class="sxs-lookup"><span data-stu-id="64ecf-214">Install all packages by the following command.</span></span> <span data-ttu-id="64ecf-215">Azure IOT cihaz SDK'sı, BME280 algılayıcı kitaplığı ve geriye Pi kitaplığı içerir.</span><span class="sxs-lookup"><span data-stu-id="64ecf-215">It includes Azure IoT device SDK, BME280 Sensor library and Wiring Pi library.</span></span>

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   <span data-ttu-id="64ecf-216">Bu yükleme işlemini denpening ağ bağlantınızdaki tamamlanması birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="64ecf-216">It might take several minutes to finish this installation process denpening on your network connection.</span></span>

### <a name="configure-the-sample-application"></a><span data-ttu-id="64ecf-217">Örnek uygulamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="64ecf-217">Configure the sample application</span></span>

1. <span data-ttu-id="64ecf-218">Yapılandırma dosyası, aşağıdaki komutları çalıştırarak açın:</span><span class="sxs-lookup"><span data-stu-id="64ecf-218">Open the config file by running the following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Yapılandırma dosyası](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   <span data-ttu-id="64ecf-220">İki öğe bu dosyada configurate olabilir.</span><span class="sxs-lookup"><span data-stu-id="64ecf-220">There are two items in this file you can configurate.</span></span> <span data-ttu-id="64ecf-221">İlk sağlayıcıdır `interval`, bulut göndermek iki ileti arasındaki zaman aralığını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="64ecf-221">The first one is `interval`, which defines the time interval between two messages that send to cloud.</span></span> <span data-ttu-id="64ecf-222">İkincisi `simulatedData`, benzetimli algılayıcı verilerini veya kullanıp kullanmayacağınızı için bir Boolean değeri değil.</span><span class="sxs-lookup"><span data-stu-id="64ecf-222">The second one `simulatedData`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="64ecf-223">Varsa, **algılayıcı yok**ayarlayın `simulatedData` değeri `true` oluşturma ve sanal algılayıcı verilerini kullanma örnek uygulamayı yapmak için.</span><span class="sxs-lookup"><span data-stu-id="64ecf-223">If you **don't have the sensor**, set the `simulatedData` value to `true` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="64ecf-224">Kaydedip çıkmak denetimi O tuşlarına basarak > Enter > Denetim X.</span><span class="sxs-lookup"><span data-stu-id="64ecf-224">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="run-the-sample-application"></a><span data-ttu-id="64ecf-225">Örnek uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="64ecf-225">Run the sample application</span></span>

1. <span data-ttu-id="64ecf-226">Aşağıdaki komutu çalıştırarak örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="64ecf-226">Run the sample application by running the following command:</span></span>

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="64ecf-227">Kopyalama cihaz bağlantı dizesi tek tırnak yapıştırma emin olun.</span><span class="sxs-lookup"><span data-stu-id="64ecf-227">Make sure you copy-paste the device connection string into the single quotes.</span></span>


<span data-ttu-id="64ecf-228">Algılayıcı verilerini ve IOT hub'ına gönderilen iletileri gösterir aşağıdaki çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="64ecf-228">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![Çıktı - Raspberry Pi'yi IOT hub'ına gönderilen algılayıcı verileri](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="64ecf-230">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="64ecf-230">Next steps</span></span>

<span data-ttu-id="64ecf-231">Algılayıcı verilerini toplamak ve IOT hub'ınıza göndermek için örnek bir uygulamayı çalıştırdıktan.</span><span class="sxs-lookup"><span data-stu-id="64ecf-231">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]