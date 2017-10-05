---
title: "Buluta (C) - Azure IOT Hub'ına bağlanmak Raspberry Pi'yi Böğürtlenli Pi | Microsoft Docs"
description: "Kurulum ve Raspberry Pi'yi'nın bu öğreticide Azure bulut platformuna veri göndermek için Azure IOT Hub ile Raspberry Pi'yi bağlanma hakkında bilgi edinin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure IOT Böğürtlenli PI Böğürtlenli PI IOT hub, bulut için Böğürtlenli pi gönderme, verileri buluta Böğürtlenli pi"
ms.assetid: 68c0e730-1dc8-4e26-ac6b-573b217b302d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/12/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8b8fda17a8d1d1796d5299e3aba4b0fd5e719a4c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-c"></a><span data-ttu-id="87afc-104">Azure IoT Hub (C) Böğürtlenli Pi Bağlan</span><span class="sxs-lookup"><span data-stu-id="87afc-104">Connect Raspberry Pi to Azure IoT Hub (C)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="87afc-105">Bu öğreticide, Raspbian çalıştıran Raspberry Pi'yi ile çalışmanın temelleri öğrenerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="87afc-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="87afc-106">Daha sonra sorunsuzca aygıtlarınızı buluta kullanarak bağlanmasına nasıl öğrenin [Azure IOT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="87afc-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="87afc-107">Windows 10 IOT Core örnekleri için Git [Windows Geliştirme Merkezi](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="87afc-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="87afc-108">Bir pakete henüz yok mu?</span><span class="sxs-lookup"><span data-stu-id="87afc-108">Don't have a kit yet?</span></span> <span data-ttu-id="87afc-109">Deneyin [Raspberry Pi'yi çevrimiçi simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="87afc-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="87afc-110">Veya yeni bir paket satın [burada](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="87afc-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="87afc-111">Neler</span><span class="sxs-lookup"><span data-stu-id="87afc-111">What you do</span></span>

* <span data-ttu-id="87afc-112">IOT hub'ı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="87afc-112">Create an IoT hub.</span></span>
* <span data-ttu-id="87afc-113">Bir cihaz IOT hub'ınıza Pi için kaydetme.</span><span class="sxs-lookup"><span data-stu-id="87afc-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="87afc-114">Böğürtlenli PI kurulumu.</span><span class="sxs-lookup"><span data-stu-id="87afc-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="87afc-115">Pi algılayıcı verilerini IOT hub'ınıza gönderilecek örnek bir uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="87afc-115">Run a sample application on Pi to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="87afc-116">Raspberry Pi'yi, oluşturduğunuz bir IOT hub'ına bağlanın.</span><span class="sxs-lookup"><span data-stu-id="87afc-116">Connect Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="87afc-117">Pi BME280 algılayıcı sıcaklık ve nem verileri toplamak için bir örnek uygulamayı çalıştırın. ardından.</span><span class="sxs-lookup"><span data-stu-id="87afc-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="87afc-118">Son olarak, IOT hub'ınıza algılayıcı verileri gönderin.</span><span class="sxs-lookup"><span data-stu-id="87afc-118">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="87afc-119">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="87afc-119">What you learn</span></span>

* <span data-ttu-id="87afc-120">Azure IOT hub oluşturma ve yeni cihaz bağlantı dizenizi elde etme.</span><span class="sxs-lookup"><span data-stu-id="87afc-120">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="87afc-121">Pi BME280 algılayıcı ile bağlanma.</span><span class="sxs-lookup"><span data-stu-id="87afc-121">How to connect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="87afc-122">Pi üzerinde bir örnek uygulamayı çalıştırarak algılayıcı verilerini toplamak nasıl.</span><span class="sxs-lookup"><span data-stu-id="87afc-122">How to collect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="87afc-123">IOT hub'ınıza algılayıcı verileri göndermek nasıl.</span><span class="sxs-lookup"><span data-stu-id="87afc-123">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="87afc-124">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="87afc-124">What you need</span></span>

![Ne gerekiyor](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="87afc-126">Raspberry Pi 2 veya Raspberry Pi 3 Panosu.</span><span class="sxs-lookup"><span data-stu-id="87afc-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="87afc-127">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="87afc-127">An active Azure subscription.</span></span> <span data-ttu-id="87afc-128">Bir Azure hesabınız yoksa [ücretsiz Azure deneme hesabı oluşturma](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="87afc-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="87afc-129">Bir izleyici, bir USB klavye ve fare Pi bağlanan.</span><span class="sxs-lookup"><span data-stu-id="87afc-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span></span>
* <span data-ttu-id="87afc-130">Mac veya Windows veya Linux çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="87afc-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="87afc-131">Bir Internet bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="87afc-131">An Internet connection.</span></span>
* <span data-ttu-id="87afc-132">16 GB veya üzeri microSD kartı.</span><span class="sxs-lookup"><span data-stu-id="87afc-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="87afc-133">İşletim sistemi görüntüsü microSD kartı üzerine yazmak için bir USB SD bağdaştırıcı veya microSD kartı.</span><span class="sxs-lookup"><span data-stu-id="87afc-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="87afc-134">5-volt 2 amp güç 6 kaplama alanı mikro USB kablosu ile sağlayın.</span><span class="sxs-lookup"><span data-stu-id="87afc-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span></span>

<span data-ttu-id="87afc-135">Aşağıdaki öğeler isteğe bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="87afc-135">The following items are optional:</span></span>

* <span data-ttu-id="87afc-136">Bir birleştirilmiş Adafruit BME280 sıcaklık, baskısı ve nem algılayıcı.</span><span class="sxs-lookup"><span data-stu-id="87afc-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="87afc-137">Bir breadboard.</span><span class="sxs-lookup"><span data-stu-id="87afc-137">A breadboard.</span></span>
* <span data-ttu-id="87afc-138">6 F/M anahtar kablolarını.</span><span class="sxs-lookup"><span data-stu-id="87afc-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="87afc-139">Yayılmış 10 mm LED.</span><span class="sxs-lookup"><span data-stu-id="87afc-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="87afc-140">Kod örneği desteği algılayıcı verilerini benzetimli çünkü bu öğeler isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="87afc-140">These items are optional because the code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="87afc-141">Böğürtlenli PI Kurulumu</span><span class="sxs-lookup"><span data-stu-id="87afc-141">Setup Raspberry Pi</span></span>

### <a name="install-the-raspbian-operating-system-for-pi"></a><span data-ttu-id="87afc-142">Pi için Raspbian işletim sistemini yükleme</span><span class="sxs-lookup"><span data-stu-id="87afc-142">Install the Raspbian operating system for Pi</span></span>

<span data-ttu-id="87afc-143">MicroSD kartı Raspbian görüntünün yüklenmesi için hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="87afc-143">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="87afc-144">Raspbian indirin.</span><span class="sxs-lookup"><span data-stu-id="87afc-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="87afc-145">[Masaüstü ile Raspbian Jessie karşıdan](https://www.raspberrypi.org/downloads/raspbian/) (.zip dosyası).</span><span class="sxs-lookup"><span data-stu-id="87afc-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span></span>
   1. <span data-ttu-id="87afc-146">Raspbian görüntünün bilgisayarınızdaki bir klasöre ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="87afc-146">Extract the Raspbian image to a folder on your computer.</span></span>
1. <span data-ttu-id="87afc-147">Raspbian microSD kartı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="87afc-147">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="87afc-148">[Etcher SD kart yazıcı yardımcı programı yükleyip](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="87afc-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="87afc-149">Etcher çalıştırın ve 1. adımda ayıkladığınız Raspbian görüntüyü seçin.</span><span class="sxs-lookup"><span data-stu-id="87afc-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="87afc-150">MicroSD kartı sürücü seçin.</span><span class="sxs-lookup"><span data-stu-id="87afc-150">Select the microSD card drive.</span></span> <span data-ttu-id="87afc-151">Etcher zaten doğru sürücü seçmiş olabilirsiniz olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="87afc-151">Note that Etcher may have already selected the correct drive.</span></span>
   1. <span data-ttu-id="87afc-152">Raspbian microSD kartı yüklemek için Flash'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="87afc-152">Click Flash to install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="87afc-153">Yükleme tamamlandığında microSD kartı bilgisayarınızdan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="87afc-153">Remove the microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="87afc-154">Etcher otomatik olarak çıkarır veya tamamlanmasından sonra microSD kartı çıkarır çünkü microSD kartı doğrudan kaldırmak güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="87afc-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   1. <span data-ttu-id="87afc-155">MicroSD kartı Pi yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="87afc-155">Insert the microSD card into Pi.</span></span>

### <a name="enable-ssh-and-spi"></a><span data-ttu-id="87afc-156">SSH ve SPI etkinleştir</span><span class="sxs-lookup"><span data-stu-id="87afc-156">Enable SSH and SPI</span></span>

1. <span data-ttu-id="87afc-157">Monitör, klavye ve fare pi bağlanmak, Pi başlatın ve ardından içinde Raspbian kullanarak oturum `pi` kullanıcı adı ve `raspberry` ve parola olarak.</span><span class="sxs-lookup"><span data-stu-id="87afc-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span></span>
1. <span data-ttu-id="87afc-158">Böğürtlenli simgesine tıklayın > **Tercihler** > **Raspberry Pi yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="87afc-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Raspbian Tercihler menüsü](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="87afc-160">Üzerinde **arabirimleri** sekmesinde, ayarlamak **SPI** ve **SSH** için **etkinleştirmek**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="87afc-160">On the **Interfaces** tab, set **SPI** and **SSH** to **Enable**, and then click **OK**.</span></span> <span data-ttu-id="87afc-161">Fiziksel algılayıcılar varsa ve benzetimli algılayıcı verilerini kullanmak istediğiniz yok, bu adım isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="87afc-161">If you don't have physical sensors and want to use simulated sensor data, this step is optional.</span></span>

   ![SPI ve Böğürtlenli Pi üzerinde SSH etkinleştir](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="87afc-163">SSH ve SPI etkinleştirmek için daha fazla başvuru belgeleri bulabilirsiniz [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) ve [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span><span class="sxs-lookup"><span data-stu-id="87afc-163">To enable SSH and SPI, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="87afc-164">Pi algılayıcı Bağlan</span><span class="sxs-lookup"><span data-stu-id="87afc-164">Connect the sensor to Pi</span></span>

<span data-ttu-id="87afc-165">Bir LED ve bir BME280 Pi şu şekilde bağlanmak için breadboard ve anahtar kablolarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="87afc-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span></span> <span data-ttu-id="87afc-166">Algılayıcı yoksa [Bu bölüm atlayın](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="87afc-166">If you don’t have the sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![Raspberry Pi'yi ve algılayıcı bağlantısı](media/iot-hub-raspberry-pi-kit-c-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="87afc-168">BME280 algılayıcı sıcaklık ve nem verileri toplayabilir.</span><span class="sxs-lookup"><span data-stu-id="87afc-168">The BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="87afc-169">Ve cihaz ve bulut arasındaki iletişimi ise LED blink.</span><span class="sxs-lookup"><span data-stu-id="87afc-169">And the LED will blink if there is a communication between device and the cloud.</span></span> 

<span data-ttu-id="87afc-170">Algılayıcı PIN'ler için aşağıdaki kablolama kullanın:</span><span class="sxs-lookup"><span data-stu-id="87afc-170">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="87afc-171">Başlangıç (algılayıcı & LED)</span><span class="sxs-lookup"><span data-stu-id="87afc-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="87afc-172">Bitiş (kartı)</span><span class="sxs-lookup"><span data-stu-id="87afc-172">End (Board)</span></span>            | <span data-ttu-id="87afc-173">Kablo rengi</span><span class="sxs-lookup"><span data-stu-id="87afc-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="87afc-174">LED VDD (PIN 5G)</span><span class="sxs-lookup"><span data-stu-id="87afc-174">LED VDD (Pin 5G)</span></span>         | <span data-ttu-id="87afc-175">GPIO'yu 4 (PIN 7)</span><span class="sxs-lookup"><span data-stu-id="87afc-175">GPIO 4 (Pin 7)</span></span>         | <span data-ttu-id="87afc-176">Beyaz kablosu</span><span class="sxs-lookup"><span data-stu-id="87afc-176">White cable</span></span>   |
| <span data-ttu-id="87afc-177">LED GND (PIN 6G)</span><span class="sxs-lookup"><span data-stu-id="87afc-177">LED GND (Pin 6G)</span></span>         | <span data-ttu-id="87afc-178">GND (PIN 6)</span><span class="sxs-lookup"><span data-stu-id="87afc-178">GND (Pin 6)</span></span>            | <span data-ttu-id="87afc-179">Siyah kablosu</span><span class="sxs-lookup"><span data-stu-id="87afc-179">Black cable</span></span>   |
| <span data-ttu-id="87afc-180">VDD (PIN 18F)</span><span class="sxs-lookup"><span data-stu-id="87afc-180">VDD (Pin 18F)</span></span>            | <span data-ttu-id="87afc-181">3, 3v PWR (PIN 17)</span><span class="sxs-lookup"><span data-stu-id="87afc-181">3.3V PWR (Pin 17)</span></span>      | <span data-ttu-id="87afc-182">Beyaz kablosu</span><span class="sxs-lookup"><span data-stu-id="87afc-182">White cable</span></span>   |
| <span data-ttu-id="87afc-183">GND (PIN 20F)</span><span class="sxs-lookup"><span data-stu-id="87afc-183">GND (Pin 20F)</span></span>            | <span data-ttu-id="87afc-184">GND (PIN 20)</span><span class="sxs-lookup"><span data-stu-id="87afc-184">GND (Pin 20)</span></span>           | <span data-ttu-id="87afc-185">Siyah kablosu</span><span class="sxs-lookup"><span data-stu-id="87afc-185">Black cable</span></span>   |
| <span data-ttu-id="87afc-186">SCK (PIN 21F)</span><span class="sxs-lookup"><span data-stu-id="87afc-186">SCK (Pin 21F)</span></span>            | <span data-ttu-id="87afc-187">SPI0 SCLK (PIN 23)</span><span class="sxs-lookup"><span data-stu-id="87afc-187">SPI0 SCLK (Pin 23)</span></span>     | <span data-ttu-id="87afc-188">Turuncu kablosu</span><span class="sxs-lookup"><span data-stu-id="87afc-188">Orange cable</span></span>  |
| <span data-ttu-id="87afc-189">SDO (PIN 22F)</span><span class="sxs-lookup"><span data-stu-id="87afc-189">SDO (Pin 22F)</span></span>            | <span data-ttu-id="87afc-190">SPI0 MISO (PIN 21)</span><span class="sxs-lookup"><span data-stu-id="87afc-190">SPI0 MISO (Pin 21)</span></span>     | <span data-ttu-id="87afc-191">Sarı kablosu</span><span class="sxs-lookup"><span data-stu-id="87afc-191">Yellow cable</span></span>  |
| <span data-ttu-id="87afc-192">SDI (PIN 23F)</span><span class="sxs-lookup"><span data-stu-id="87afc-192">SDI (Pin 23F)</span></span>            | <span data-ttu-id="87afc-193">SPI0 MOSI (PIN 19)</span><span class="sxs-lookup"><span data-stu-id="87afc-193">SPI0 MOSI (Pin 19)</span></span>     | <span data-ttu-id="87afc-194">Yeşil kablosu</span><span class="sxs-lookup"><span data-stu-id="87afc-194">Green cable</span></span>   |
| <span data-ttu-id="87afc-195">CS (PIN 24F)</span><span class="sxs-lookup"><span data-stu-id="87afc-195">CS (Pin 24F)</span></span>             | <span data-ttu-id="87afc-196">SPI0 CS (PIN 24)</span><span class="sxs-lookup"><span data-stu-id="87afc-196">SPI0 CS (Pin 24)</span></span>       | <span data-ttu-id="87afc-197">Mavi kablosu</span><span class="sxs-lookup"><span data-stu-id="87afc-197">Blue cable</span></span>    |

<span data-ttu-id="87afc-198">Görüntülemek için tıklatın [Raspberry Pi 2 ve 3 PIN eşlemeleri](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) daha sonra başvurmak üzere.</span><span class="sxs-lookup"><span data-stu-id="87afc-198">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="87afc-199">Raspberry Pi'yi BME280 başarıyla bağlandıktan sonra görüntü gibi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="87afc-199">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span></span>

![Bağlı Pi ve BME280](media/iot-hub-raspberry-pi-kit-c-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a><span data-ttu-id="87afc-201">Pi ağa bağlanın</span><span class="sxs-lookup"><span data-stu-id="87afc-201">Connect Pi to the network</span></span>

<span data-ttu-id="87afc-202">Pi üzerinde mikro USB kablosu ve güç kaynağı kullanarak açın.</span><span class="sxs-lookup"><span data-stu-id="87afc-202">Turn on Pi by using the micro USB cable and the power supply.</span></span> <span data-ttu-id="87afc-203">Pi kablolu ağa bağlanın veya izleyin için Ethernet kablosu kullanın [Raspberry Pi Foundation yönergeleri](https://www.raspberrypi.org/learning/software-guide/wifi/) Pi kablosuz ağınıza bağlanmak için.</span><span class="sxs-lookup"><span data-stu-id="87afc-203">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span></span> <span data-ttu-id="87afc-204">Not yapmanıza gerek, Pi ağa başarıyla bağlandı sonra [IP adresi, pi'nin](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="87afc-204">After your Pi has been successfully connected to the network, you need to take a note of the [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Kablolu ağa bağlı](media/iot-hub-raspberry-pi-kit-c-get-started/5_power-on-pi.jpg)


## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="87afc-206">Pi üzerinde bir örnek uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="87afc-206">Run a sample application on Pi</span></span>

### <a name="install-the-prerequisite-packages"></a><span data-ttu-id="87afc-207">Önkoşul yükleme</span><span class="sxs-lookup"><span data-stu-id="87afc-207">Install the prerequisite packages</span></span>

1. <span data-ttu-id="87afc-208">Raspberry Pi'yi bağlanmak için ana bilgisayarınız aşağıdaki SSH istemcilerden birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="87afc-208">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span></span>
   
   <span data-ttu-id="87afc-209">**Windows kullanıcıları**</span><span class="sxs-lookup"><span data-stu-id="87afc-209">**Windows Users**</span></span>
   1. <span data-ttu-id="87afc-210">İndirme ve yükleme [PuTTY](http://www.putty.org/) Windows için.</span><span class="sxs-lookup"><span data-stu-id="87afc-210">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="87afc-211">Ana bilgisayar adı (veya IP adresi) içine Pi bölümünüzü IP adresini kopyalayın ve SSH bağlantı türü olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="87afc-211">Copy the IP address of your Pi into the Host name (or IP address) section and select SSH as the connection type.</span></span>
   
   ![PuTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   <span data-ttu-id="87afc-213">**Mac ve Ubuntu kullanıcılar**</span><span class="sxs-lookup"><span data-stu-id="87afc-213">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="87afc-214">Yerleşik SSH istemcisi Ubuntu veya macOS kullanın.</span><span class="sxs-lookup"><span data-stu-id="87afc-214">Use the built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="87afc-215">Çalıştırmanız gerekebilir `ssh pi@<ip address of pi>` Pi SSH aracılığıyla bağlanmak için.</span><span class="sxs-lookup"><span data-stu-id="87afc-215">You might need to run `ssh pi@<ip address of pi>` to connect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="87afc-216">Varsayılan kullanıcı adı `pi` , ve parola `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="87afc-216">The default username is `pi` , and the password is `raspberry`.</span></span>

1. <span data-ttu-id="87afc-217">Önkoşul aşağıdaki komutları çalıştırarak C ve Cmake için Microsoft Azure IOT cihaz SDK yükleyin:</span><span class="sxs-lookup"><span data-stu-id="87afc-217">Install the prerequisite packages for the Microsoft Azure IoT Device SDK for C and Cmake by running the following commands:</span></span>

   ```bash
   grep -q -F 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   grep -q -F 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys FDA6A393E4C2257F
   sudo apt-get update
   sudo apt-get install -y azure-iot-sdk-c-dev cmake libcurl4-openssl-dev git-core
   git clone git://git.drogon.net/wiringPi
   cd ./wiringPi
   ./build
   ```


### <a name="configure-the-sample-application"></a><span data-ttu-id="87afc-218">Örnek uygulamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="87afc-218">Configure the sample application</span></span>

1. <span data-ttu-id="87afc-219">Örnek uygulama, aşağıdaki komutu çalıştırarak kopyalama:</span><span class="sxs-lookup"><span data-stu-id="87afc-219">Clone the sample application by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-client-app
   ```
1. <span data-ttu-id="87afc-220">Yapılandırma dosyası, aşağıdaki komutları çalıştırarak açın:</span><span class="sxs-lookup"><span data-stu-id="87afc-220">Open the config file by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-raspberrypi-client-app
   nano config.h
   ```

   ![Yapılandırma dosyası](media/iot-hub-raspberry-pi-kit-c-get-started/6_config-file.png)

   <span data-ttu-id="87afc-222">İki makroları vardır bu dosyada configurate olabilir.</span><span class="sxs-lookup"><span data-stu-id="87afc-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="87afc-223">İlk sağlayıcıdır `INTERVAL`, bulut göndermek iki ileti süre (milisaniye cinsinden) tanımlar.</span><span class="sxs-lookup"><span data-stu-id="87afc-223">The first one is `INTERVAL`, which defines the time interval (in milliseconds) between two messages that send to cloud.</span></span> <span data-ttu-id="87afc-224">İkincisi `SIMULATED_DATA`, benzetimli algılayıcı verilerini veya kullanıp kullanmayacağınızı için bir Boolean değeri değil.</span><span class="sxs-lookup"><span data-stu-id="87afc-224">The second one `SIMULATED_DATA`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="87afc-225">Varsa, **algılayıcı yok**ayarlayın `SIMULATED_DATA` değeri `1` oluşturma ve sanal algılayıcı verilerini kullanma örnek uygulamayı yapmak için.</span><span class="sxs-lookup"><span data-stu-id="87afc-225">If you **don't have the sensor**, set the `SIMULATED_DATA` value to `1` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="87afc-226">Kaydedip çıkmak denetimi O tuşlarına basarak > Enter > Denetim X.</span><span class="sxs-lookup"><span data-stu-id="87afc-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-the-sample-application"></a><span data-ttu-id="87afc-227">Derleme ve örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="87afc-227">Build and run the sample application</span></span>

1. <span data-ttu-id="87afc-228">Örnek uygulama, aşağıdaki komutu çalıştırarak oluşturun:</span><span class="sxs-lookup"><span data-stu-id="87afc-228">Build the sample application by running the following command:</span></span>

   ```bash
   cmake . && make
   ```
   ![Çıktı derleme](media/iot-hub-raspberry-pi-kit-c-get-started/7_build-output.png)

1. <span data-ttu-id="87afc-230">Aşağıdaki komutu çalıştırarak örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="87afc-230">Run the sample application by running the following command:</span></span>

   ```bash
   sudo ./app '<DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   <span data-ttu-id="87afc-231">Kopyalama cihaz bağlantı dizesi tek tırnak yapıştırma emin olun.</span><span class="sxs-lookup"><span data-stu-id="87afc-231">Make sure you copy-paste the device connection string into the single quotes.</span></span>


<span data-ttu-id="87afc-232">Algılayıcı verilerini ve IOT hub'ına gönderilen iletileri gösterir aşağıdaki çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="87afc-232">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![Çıktı - Raspberry Pi'yi IOT hub'ına gönderilen algılayıcı verileri](media/iot-hub-raspberry-pi-kit-c-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="87afc-234">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="87afc-234">Next steps</span></span>

<span data-ttu-id="87afc-235">Algılayıcı verilerini toplamak ve IOT hub'ınıza göndermek için örnek bir uygulamayı çalıştırdıktan.</span><span class="sxs-lookup"><span data-stu-id="87afc-235">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span> <span data-ttu-id="87afc-236">Bir komut satırı arabirimi içinde Raspberry Pi'yi, IOT hub'ı veya gönderme iletileri Raspberry Pi'yi tarafından gönderilen iletileri görmek için bkz: [iothub-explorer eğitici Mesajlaşma Yönet bulut cihaz](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="87afc-236">To see the messages that your Raspberry Pi has sent to your IoT hub or send messages to your Raspberry Pi in a command line interface, see the [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
