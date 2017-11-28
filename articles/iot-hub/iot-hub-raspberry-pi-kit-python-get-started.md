---
title: "Buluta (Python) - Azure IOT Hub'ına bağlanmak Raspberry Pi'yi Böğürtlenli Pi | Microsoft Docs"
description: "Kurulum ve Raspberry Pi'yi'nın bu öğreticide Azure bulut platformuna veri göndermek için Azure IOT Hub ile Raspberry Pi'yi bağlanma hakkında bilgi edinin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure IOT Böğürtlenli PI Böğürtlenli PI IOT hub, bulut için Böğürtlenli pi gönderme, verileri buluta Böğürtlenli pi"
ms.service: iot-hub
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/31/2017
ms.author: xshi
ms.openlocfilehash: 1b1a9dc960846cbc15ce09d0fd106e1492937439
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-python"></a><span data-ttu-id="1aa30-104">Azure IOT Hub (Python) Böğürtlenli Pi Bağlan</span><span class="sxs-lookup"><span data-stu-id="1aa30-104">Connect Raspberry Pi to Azure IoT Hub (Python)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="1aa30-105">Bu öğreticide, Raspbian çalıştıran Raspberry Pi'yi ile çalışmanın temelleri öğrenerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="1aa30-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="1aa30-106">Daha sonra sorunsuzca aygıtlarınızı buluta kullanarak bağlanmasına nasıl öğrenin [Azure IOT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="1aa30-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="1aa30-107">Windows 10 IOT Core örnekleri için Git [Windows Geliştirme Merkezi](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="1aa30-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="1aa30-108">Bir pakete henüz yok mu?</span><span class="sxs-lookup"><span data-stu-id="1aa30-108">Don't have a kit yet?</span></span> <span data-ttu-id="1aa30-109">Deneyin [Raspberry Pi'yi çevrimiçi simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1aa30-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="1aa30-110">Veya yeni bir paket satın [burada](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="1aa30-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="1aa30-111">Neler</span><span class="sxs-lookup"><span data-stu-id="1aa30-111">What you do</span></span>

* <span data-ttu-id="1aa30-112">IOT hub'ı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1aa30-112">Create an IoT hub.</span></span>
* <span data-ttu-id="1aa30-113">Bir cihaz IOT hub'ınıza Pi için kaydetme.</span><span class="sxs-lookup"><span data-stu-id="1aa30-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="1aa30-114">Böğürtlenli PI kurulumu.</span><span class="sxs-lookup"><span data-stu-id="1aa30-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="1aa30-115">Pi algılayıcı verilerini IOT hub'ınıza gönderilecek örnek bir uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1aa30-115">Run a sample application on Pi to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="1aa30-116">Raspberry Pi'yi, oluşturduğunuz bir IOT hub'ına bağlanın.</span><span class="sxs-lookup"><span data-stu-id="1aa30-116">Connect Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="1aa30-117">Pi BME280 algılayıcı sıcaklık ve nem verileri toplamak için bir örnek uygulamayı çalıştırın. ardından.</span><span class="sxs-lookup"><span data-stu-id="1aa30-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="1aa30-118">Son olarak, IOT hub'ınıza algılayıcı verileri gönderin.</span><span class="sxs-lookup"><span data-stu-id="1aa30-118">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="1aa30-119">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="1aa30-119">What you learn</span></span>

* <span data-ttu-id="1aa30-120">Azure IOT hub oluşturma ve yeni cihaz bağlantı dizenizi elde etme.</span><span class="sxs-lookup"><span data-stu-id="1aa30-120">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="1aa30-121">Pi BME280 algılayıcı ile bağlanma.</span><span class="sxs-lookup"><span data-stu-id="1aa30-121">How to connect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="1aa30-122">Pi üzerinde bir örnek uygulamayı çalıştırarak algılayıcı verilerini toplamak nasıl.</span><span class="sxs-lookup"><span data-stu-id="1aa30-122">How to collect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="1aa30-123">IOT hub'ınıza algılayıcı verileri göndermek nasıl.</span><span class="sxs-lookup"><span data-stu-id="1aa30-123">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1aa30-124">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="1aa30-124">What you need</span></span>

![Ne gerekiyor](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="1aa30-126">Raspberry Pi 2 veya Raspberry Pi 3 Panosu.</span><span class="sxs-lookup"><span data-stu-id="1aa30-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="1aa30-127">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="1aa30-127">An active Azure subscription.</span></span> <span data-ttu-id="1aa30-128">Bir Azure hesabınız yoksa [ücretsiz Azure deneme hesabı oluşturma](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="1aa30-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="1aa30-129">Bir izleyici, bir USB klavye ve fare Pi bağlanan.</span><span class="sxs-lookup"><span data-stu-id="1aa30-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span></span>
* <span data-ttu-id="1aa30-130">Mac veya Windows veya Linux çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="1aa30-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="1aa30-131">Bir Internet bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="1aa30-131">An Internet connection.</span></span>
* <span data-ttu-id="1aa30-132">16 GB veya üzeri microSD kartı.</span><span class="sxs-lookup"><span data-stu-id="1aa30-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="1aa30-133">İşletim sistemi görüntüsü microSD kartı üzerine yazmak için bir USB SD bağdaştırıcı veya microSD kartı.</span><span class="sxs-lookup"><span data-stu-id="1aa30-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="1aa30-134">5-volt 2 amp güç 6 kaplama alanı mikro USB kablosu ile sağlayın.</span><span class="sxs-lookup"><span data-stu-id="1aa30-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span></span>

<span data-ttu-id="1aa30-135">Aşağıdaki öğeler isteğe bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="1aa30-135">The following items are optional:</span></span>

* <span data-ttu-id="1aa30-136">Bir birleştirilmiş Adafruit BME280 sıcaklık, baskısı ve nem algılayıcı.</span><span class="sxs-lookup"><span data-stu-id="1aa30-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="1aa30-137">Bir breadboard.</span><span class="sxs-lookup"><span data-stu-id="1aa30-137">A breadboard.</span></span>
* <span data-ttu-id="1aa30-138">6 F/M anahtar kablolarını.</span><span class="sxs-lookup"><span data-stu-id="1aa30-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="1aa30-139">Yayılmış 10 mm LED.</span><span class="sxs-lookup"><span data-stu-id="1aa30-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="1aa30-140">Kod örneği desteği algılayıcı verilerini benzetimli çünkü bu öğeler isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="1aa30-140">These items are optional because the code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="set-up-raspberry-pi"></a><span data-ttu-id="1aa30-141">Raspberry Pi'yi ayarlayın</span><span class="sxs-lookup"><span data-stu-id="1aa30-141">Set up Raspberry Pi</span></span>

### <a name="install-the-raspbian-operating-system-for-pi"></a><span data-ttu-id="1aa30-142">Pi için Raspbian işletim sistemini yükleme</span><span class="sxs-lookup"><span data-stu-id="1aa30-142">Install the Raspbian operating system for Pi</span></span>

<span data-ttu-id="1aa30-143">MicroSD kartı Raspbian görüntünün yüklenmesi için hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="1aa30-143">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="1aa30-144">Raspbian indirin.</span><span class="sxs-lookup"><span data-stu-id="1aa30-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="1aa30-145">[Masaüstü ile Raspbian Jessie karşıdan](https://www.raspberrypi.org/downloads/raspbian/) (.zip dosyası).</span><span class="sxs-lookup"><span data-stu-id="1aa30-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span></span>
   1. <span data-ttu-id="1aa30-146">Raspbian görüntünün bilgisayarınızdaki bir klasöre ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="1aa30-146">Extract the Raspbian image to a folder on your computer.</span></span>
1. <span data-ttu-id="1aa30-147">Raspbian microSD kartı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1aa30-147">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="1aa30-148">[Etcher SD kart yazıcı yardımcı programı yükleyip](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="1aa30-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="1aa30-149">Etcher çalıştırın ve 1. adımda ayıkladığınız Raspbian görüntüyü seçin.</span><span class="sxs-lookup"><span data-stu-id="1aa30-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="1aa30-150">MicroSD kartı sürücü seçin.</span><span class="sxs-lookup"><span data-stu-id="1aa30-150">Select the microSD card drive.</span></span> <span data-ttu-id="1aa30-151">Etcher zaten doğru sürücü seçmiş olabilirsiniz olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1aa30-151">Note that Etcher may have already selected the correct drive.</span></span>
   1. <span data-ttu-id="1aa30-152">Raspbian microSD kartı yüklemek için Flash'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1aa30-152">Click Flash to install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="1aa30-153">Yükleme tamamlandığında microSD kartı bilgisayarınızdan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="1aa30-153">Remove the microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="1aa30-154">Etcher otomatik olarak çıkarır veya tamamlanmasından sonra microSD kartı çıkarır çünkü microSD kartı doğrudan kaldırmak güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="1aa30-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   1. <span data-ttu-id="1aa30-155">MicroSD kartı Pi yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="1aa30-155">Insert the microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="1aa30-156">SSH ve I2C etkinleştir</span><span class="sxs-lookup"><span data-stu-id="1aa30-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="1aa30-157">Monitör, klavye ve fare pi bağlanmak, Pi başlatın ve ardından içinde Raspbian kullanarak oturum `pi` kullanıcı adı ve `raspberry` ve parola olarak.</span><span class="sxs-lookup"><span data-stu-id="1aa30-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span></span>
1. <span data-ttu-id="1aa30-158">Böğürtlenli simgesine tıklayın > **Tercihler** > **Raspberry Pi yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="1aa30-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Raspbian Tercihler menüsü](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="1aa30-160">Üzerinde **arabirimleri** sekmesinde, ayarlamak **I2C** ve **SSH** için **etkinleştirmek**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="1aa30-160">On the **Interfaces** tab, set **I2C** and **SSH** to **Enable**, and then click **OK**.</span></span> <span data-ttu-id="1aa30-161">Fiziksel algılayıcılar varsa ve benzetimli algılayıcı verilerini kullanmak istediğiniz yok, bu adım isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="1aa30-161">If you don't have physical sensors and want to use simulated sensor data, this step is optional.</span></span>

   ![I2C ve Böğürtlenli Pi üzerinde SSH etkinleştir](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="1aa30-163">SSH ve I2C etkinleştirmek için daha fazla başvuru belgeleri bulabilirsiniz [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) ve [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span><span class="sxs-lookup"><span data-stu-id="1aa30-163">To enable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="1aa30-164">Pi algılayıcı Bağlan</span><span class="sxs-lookup"><span data-stu-id="1aa30-164">Connect the sensor to Pi</span></span>

<span data-ttu-id="1aa30-165">Bir LED ve bir BME280 Pi şu şekilde bağlanmak için breadboard ve anahtar kablolarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="1aa30-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span></span> <span data-ttu-id="1aa30-166">Algılayıcı yoksa [Bu bölüm atlayın](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="1aa30-166">If you don’t have the sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![Raspberry Pi'yi ve algılayıcı bağlantısı](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="1aa30-168">BME280 algılayıcı sıcaklık ve nem verileri toplayabilir.</span><span class="sxs-lookup"><span data-stu-id="1aa30-168">The BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="1aa30-169">Ve cihaz ve bulut arasındaki iletişimi ise LED blink.</span><span class="sxs-lookup"><span data-stu-id="1aa30-169">And the LED will blink if there is a communication between device and the cloud.</span></span> 

<span data-ttu-id="1aa30-170">Algılayıcı PIN'ler için aşağıdaki kablolama kullanın:</span><span class="sxs-lookup"><span data-stu-id="1aa30-170">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="1aa30-171">Başlangıç (algılayıcı & LED)</span><span class="sxs-lookup"><span data-stu-id="1aa30-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="1aa30-172">Bitiş (kartı)</span><span class="sxs-lookup"><span data-stu-id="1aa30-172">End (Board)</span></span>            | <span data-ttu-id="1aa30-173">Kablo rengi</span><span class="sxs-lookup"><span data-stu-id="1aa30-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="1aa30-174">VDD (PIN 5G)</span><span class="sxs-lookup"><span data-stu-id="1aa30-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="1aa30-175">3, 3v PWR (PIN 1)</span><span class="sxs-lookup"><span data-stu-id="1aa30-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="1aa30-176">Beyaz kablosu</span><span class="sxs-lookup"><span data-stu-id="1aa30-176">White cable</span></span>   |
| <span data-ttu-id="1aa30-177">GND (PIN 7G)</span><span class="sxs-lookup"><span data-stu-id="1aa30-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="1aa30-178">GND (PIN 6)</span><span class="sxs-lookup"><span data-stu-id="1aa30-178">GND (Pin 6)</span></span>            | <span data-ttu-id="1aa30-179">Kahverengi kablosu</span><span class="sxs-lookup"><span data-stu-id="1aa30-179">Brown cable</span></span>   |
| <span data-ttu-id="1aa30-180">SDI (PIN 10G)</span><span class="sxs-lookup"><span data-stu-id="1aa30-180">SDI (Pin 10G)</span></span>            | <span data-ttu-id="1aa30-181">I2C1 SDA (PIN 3)</span><span class="sxs-lookup"><span data-stu-id="1aa30-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="1aa30-182">Kırmızı kablosu</span><span class="sxs-lookup"><span data-stu-id="1aa30-182">Red cable</span></span>     |
| <span data-ttu-id="1aa30-183">SCK (PIN 8G)</span><span class="sxs-lookup"><span data-stu-id="1aa30-183">SCK (Pin 8G)</span></span>             | <span data-ttu-id="1aa30-184">I2C1 SCL (PIN 5)</span><span class="sxs-lookup"><span data-stu-id="1aa30-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="1aa30-185">Turuncu kablosu</span><span class="sxs-lookup"><span data-stu-id="1aa30-185">Orange cable</span></span>  |
| <span data-ttu-id="1aa30-186">LED VDD (PIN 18F)</span><span class="sxs-lookup"><span data-stu-id="1aa30-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="1aa30-187">GPIO'yu 24 (PIN 18)</span><span class="sxs-lookup"><span data-stu-id="1aa30-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="1aa30-188">Beyaz kablosu</span><span class="sxs-lookup"><span data-stu-id="1aa30-188">White cable</span></span>   |
| <span data-ttu-id="1aa30-189">LED GND (PIN 17F)</span><span class="sxs-lookup"><span data-stu-id="1aa30-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="1aa30-190">GND (PIN 20)</span><span class="sxs-lookup"><span data-stu-id="1aa30-190">GND (Pin 20)</span></span>           | <span data-ttu-id="1aa30-191">Siyah kablosu</span><span class="sxs-lookup"><span data-stu-id="1aa30-191">Black cable</span></span>   |

<span data-ttu-id="1aa30-192">Görüntülemek için tıklatın [Raspberry Pi 2 ve 3 PIN eşlemeleri](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) daha sonra başvurmak üzere.</span><span class="sxs-lookup"><span data-stu-id="1aa30-192">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="1aa30-193">Raspberry Pi'yi BME280 başarıyla bağlandıktan sonra görüntü gibi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1aa30-193">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span></span>

![Bağlı Pi ve BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a><span data-ttu-id="1aa30-195">Pi ağa bağlanın</span><span class="sxs-lookup"><span data-stu-id="1aa30-195">Connect Pi to the network</span></span>

<span data-ttu-id="1aa30-196">Pi üzerinde mikro USB kablosu ve güç kaynağı kullanarak açın.</span><span class="sxs-lookup"><span data-stu-id="1aa30-196">Turn on Pi by using the micro USB cable and the power supply.</span></span> <span data-ttu-id="1aa30-197">Pi kablolu ağa bağlanın veya izleyin için Ethernet kablosu kullanın [Raspberry Pi Foundation yönergeleri](https://www.raspberrypi.org/learning/software-guide/wifi/) Pi kablosuz ağınıza bağlanmak için.</span><span class="sxs-lookup"><span data-stu-id="1aa30-197">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span></span> <span data-ttu-id="1aa30-198">Not yapmanıza gerek, Pi ağa başarıyla bağlandı sonra [IP adresi, pi'nin](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="1aa30-198">After your Pi has been successfully connected to the network, you need to take a note of the [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Kablolu ağa bağlı](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="1aa30-200">Pi bilgisayarınızın aynı ağa bağlı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="1aa30-200">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="1aa30-201">Örneğin, pi kablolu bir ağa bağlıyken, bilgisayarınızın kablosuz bir ağa bağlıysa, IP adresi devdisco çıkışı göremeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1aa30-201">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="1aa30-202">Pi üzerinde bir örnek uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="1aa30-202">Run a sample application on Pi</span></span>

### <a name="install-the-prerequisite-packages"></a><span data-ttu-id="1aa30-203">Önkoşul yükleme</span><span class="sxs-lookup"><span data-stu-id="1aa30-203">Install the prerequisite packages</span></span>

<span data-ttu-id="1aa30-204">Raspberry Pi'yi bağlanmak için ana bilgisayarınız aşağıdaki SSH istemcilerden birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="1aa30-204">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span></span>
   
   <span data-ttu-id="1aa30-205">**Windows kullanıcıları**</span><span class="sxs-lookup"><span data-stu-id="1aa30-205">**Windows Users**</span></span>
   1. <span data-ttu-id="1aa30-206">İndirme ve yükleme [PuTTY](http://www.putty.org/) Windows için.</span><span class="sxs-lookup"><span data-stu-id="1aa30-206">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="1aa30-207">Ana bilgisayar adı (veya IP adresi) içine Pi bölümünüzü IP adresini kopyalayın ve SSH bağlantı türü olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="1aa30-207">Copy the IP address of your Pi into the Host name (or IP address) section and select SSH as the connection type.</span></span>
   
   
   <span data-ttu-id="1aa30-208">**Mac ve Ubuntu kullanıcılar**</span><span class="sxs-lookup"><span data-stu-id="1aa30-208">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="1aa30-209">Yerleşik SSH istemcisi Ubuntu veya macOS kullanın.</span><span class="sxs-lookup"><span data-stu-id="1aa30-209">Use the built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="1aa30-210">Çalıştırmanız gerekebilir `ssh pi@<ip address of pi>` Pi SSH aracılığıyla bağlanmak için.</span><span class="sxs-lookup"><span data-stu-id="1aa30-210">You might need to run `ssh pi@<ip address of pi>` to connect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="1aa30-211">Varsayılan kullanıcı adı `pi` , ve parola `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="1aa30-211">The default username is `pi` , and the password is `raspberry`.</span></span>


### <a name="configure-the-sample-application"></a><span data-ttu-id="1aa30-212">Örnek uygulamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1aa30-212">Configure the sample application</span></span>

1. <span data-ttu-id="1aa30-213">Örnek uygulama, aşağıdaki komutu çalıştırarak kopyalama:</span><span class="sxs-lookup"><span data-stu-id="1aa30-213">Clone the sample application by running the following command:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-python-raspberrypi-client-app.git
   ```
1. <span data-ttu-id="1aa30-214">Yapılandırma dosyası, aşağıdaki komutları çalıştırarak açın:</span><span class="sxs-lookup"><span data-stu-id="1aa30-214">Open the config file by running the following commands:</span></span>

   ```bash
   cd iot-hub-python-raspberrypi-client-app
   nano config.py
   ```

   <span data-ttu-id="1aa30-215">5 makroları vardır bu dosyada configurate olabilir.</span><span class="sxs-lookup"><span data-stu-id="1aa30-215">There are 5 macros in this file you can configurate.</span></span> <span data-ttu-id="1aa30-216">İlk sağlayıcıdır `MESSAGE_TIMESPAN`, bulut göndermek iki ileti süre (milisaniye cinsinden) tanımlar.</span><span class="sxs-lookup"><span data-stu-id="1aa30-216">The first one is `MESSAGE_TIMESPAN`, which defines the time interval (in milliseconds) between two messages that send to cloud.</span></span> <span data-ttu-id="1aa30-217">İkincisi `SIMULATED_DATA`, benzetimli algılayıcı verilerini veya kullanıp kullanmayacağınızı için bir Boolean değeri değil.</span><span class="sxs-lookup"><span data-stu-id="1aa30-217">The second one `SIMULATED_DATA`, which is a Boolean value for whether to use simulated sensor data or not.</span></span> <span data-ttu-id="1aa30-218">`I2C_ADDRESS`BME280 algılayıcı bağlı I2C adresidir.</span><span class="sxs-lookup"><span data-stu-id="1aa30-218">`I2C_ADDRESS` is the I2C address which your BME280 sensor is connected.</span></span> <span data-ttu-id="1aa30-219">`GPIO_PIN_ADDRESS`için LED GPIO'yu adresidir.</span><span class="sxs-lookup"><span data-stu-id="1aa30-219">`GPIO_PIN_ADDRESS` is the GPIO address for your LED.</span></span> <span data-ttu-id="1aa30-220">Son sunucudur `BLINK_TIMESPAN`, milisaniye cinsinden, LED açıldığında timespan tanımlı.</span><span class="sxs-lookup"><span data-stu-id="1aa30-220">The last one is `BLINK_TIMESPAN`, which defined the timespan when your LED is turned on in milliseconds.</span></span>

   <span data-ttu-id="1aa30-221">Varsa, **algılayıcı yok**ayarlayın `SIMULATED_DATA` değeri `True` oluşturma ve sanal algılayıcı verilerini kullanma örnek uygulamayı yapmak için.</span><span class="sxs-lookup"><span data-stu-id="1aa30-221">If you **don't have the sensor**, set the `SIMULATED_DATA` value to `True` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="1aa30-222">Kaydedip çıkmak denetimi O tuşlarına basarak > Enter > Denetim X.</span><span class="sxs-lookup"><span data-stu-id="1aa30-222">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-the-sample-application"></a><span data-ttu-id="1aa30-223">Derleme ve örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="1aa30-223">Build and run the sample application</span></span>

1. <span data-ttu-id="1aa30-224">Örnek uygulama, aşağıdaki komutu çalıştırarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1aa30-224">Build the sample application by running the following command.</span></span> <span data-ttu-id="1aa30-225">Python için Azure IOT SDK'ları Azure IOT cihaz C SDK'sı üstünde sarmalayıcıları olduğundan, istediğiniz veya Python kitaplıkları kaynak kodundan üretmek ihtiyacınız varsa C kitaplıkları derlemek gerekir.</span><span class="sxs-lookup"><span data-stu-id="1aa30-225">Because the Azure IoT SDKs for Python are wrappers on top of the Azure IoT Device C SDK, you will need to compile the C libraries if you want or need to generate the Python libraries from source code.</span></span>

   ```bash
   sudo chmod u+x setup.sh
   sudo ./setup.sh
   ```
   > [!NOTE] 
   <span data-ttu-id="1aa30-226">İstediğiniz çalıştırarak sürümü de belirtebilirsiniz `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span><span class="sxs-lookup"><span data-stu-id="1aa30-226">You can also specify the version you want by running `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span></span> <span data-ttu-id="1aa30-227">Betik parametresi olmadan çalıştırırsanız, komut dosyası yüklü python sürümü otomatik olarak algılar (arama sırasını 2.7 -> 3.4 3.5 ->).</span><span class="sxs-lookup"><span data-stu-id="1aa30-227">If you run script without parameter, the script will automatically detect the version of python installed (Search sequence 2.7->3.4->3.5).</span></span> <span data-ttu-id="1aa30-228">Oluşturma ve çalıştırma sırasında Python sürümünüzü tutarlı tutar emin olun.</span><span class="sxs-lookup"><span data-stu-id="1aa30-228">Make sure your Python version keeps consistent during building and running.</span></span> 
   
   > [!NOTE] 
   <span data-ttu-id="1aa30-229">Daha az en az 1 GB RAM içeren Linux cihazlarda oluşturma Python istemci kitaplığına (iothub_client.so) görebilirsiniz %98 aşağıda gösterildiği gibi iothub_client_python.cpp oluşturulurken takılmış derleme `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span><span class="sxs-lookup"><span data-stu-id="1aa30-229">On building the Python client library (iothub_client.so) on Linux devices that have less than 1GB RAM, you may see build getting stuck at 98% while building iothub_client_python.cpp as shown below `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span></span> <span data-ttu-id="1aa30-230">Bu sorunu yaşayıp çalıştırırsanız, kullanarak aygıt bellek tüketimini denetleme `free -m command` bu süre boyunca başka bir terminal penceresi içinde.</span><span class="sxs-lookup"><span data-stu-id="1aa30-230">If you run into this issue, check the memory consumption of the device using `free -m command` in another terminal window during that time.</span></span> <span data-ttu-id="1aa30-231">Bellek yetersiz iothub_client_python.cpp dosyası derlenirken çalıştırıyorsanız, geçici olarak başarıyla Python istemci-tarafı cihaz SDK'sı kitaplığı oluşturmak için daha fazla kullanılabilir bellek almak için takas alanı artırmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="1aa30-231">If you are running out of memory while compiling iothub_client_python.cpp file, you may have to temporarily increase the swap space to get more available memory to successfully build the Python client-side device SDK library.</span></span>
   
1. <span data-ttu-id="1aa30-232">Aşağıdaki komutu çalıştırarak örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="1aa30-232">Run the sample application by running the following command:</span></span>

   ```bash
   python app.py '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="1aa30-233">Kopyalama cihaz bağlantı dizesi tek tırnak yapıştırma emin olun.</span><span class="sxs-lookup"><span data-stu-id="1aa30-233">Make sure you copy-paste the device connection string into the single quotes.</span></span> <span data-ttu-id="1aa30-234">Ve python 3 kullanın, sonra komutu kullanabilirsiniz, `python3 app.py '<your Azure IoT hub device connection string>'`.</span><span class="sxs-lookup"><span data-stu-id="1aa30-234">And if you use the python 3, then you can use the command `python3 app.py '<your Azure IoT hub device connection string>'`.</span></span>


   <span data-ttu-id="1aa30-235">Algılayıcı verilerini ve IOT hub'ına gönderilen iletileri gösterir aşağıdaki çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1aa30-235">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

   ![Çıktı - Raspberry Pi'yi IOT hub'ına gönderilen algılayıcı verileri](media/iot-hub-raspberry-pi-kit-c-get-started/success.png
)

## <a name="next-steps"></a><span data-ttu-id="1aa30-237">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1aa30-237">Next steps</span></span>

<span data-ttu-id="1aa30-238">Algılayıcı verilerini toplamak ve IOT hub'ınıza göndermek için örnek bir uygulamayı çalıştırdıktan.</span><span class="sxs-lookup"><span data-stu-id="1aa30-238">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span> <span data-ttu-id="1aa30-239">Bir komut satırı arabirimi içinde Raspberry Pi'yi, IOT hub'ı veya gönderme iletileri Raspberry Pi'yi tarafından gönderilen iletileri görmek için bkz: [iothub-explorer eğitici Mesajlaşma Yönet bulut cihaz](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="1aa30-239">To see the messages that your Raspberry Pi has sent to your IoT hub or send messages to your Raspberry Pi in a command line interface, see the [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
