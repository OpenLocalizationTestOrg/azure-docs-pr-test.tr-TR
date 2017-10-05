---
title: "Bulut M0: yumuşatma M0 WiFi Azure IOT Hub'ına bağlanmak | Microsoft Docs"
description: "Ayarlama ve Bu öğreticide Azure bulut platformuna veri göndermek için Azure IOT Hub Adafruit yumuşatma M0 WiFi bağlanmak öğrenin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 51befcdb-332b-416f-a6a1-8aabdb67f283
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/16/2017
ms.author: xshi
ms.openlocfilehash: 0dcf6b46a4c6c743c713d24ce7844e801b278dcf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-adafruit-feather-m0-wifi-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="d120a-103">Bulutta Azure IOT Hub'ına Adafruit yumuşatma M0 WiFi Bağlan</span><span class="sxs-lookup"><span data-stu-id="d120a-103">Connect Adafruit Feather M0 WiFi to Azure IoT Hub in the cloud</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![BME280, yumuşatma M0 WiFi ve IOT hub'ı arasında bir bağlantı](media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

<span data-ttu-id="d120a-105">Bu öğreticide, Arduino panonuzu ile çalışmanın temelleri öğrenerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="d120a-105">In this tutorial, you begin by learning the basics of working with your Arduino board.</span></span> <span data-ttu-id="d120a-106">Daha sonra sorunsuzca aygıtlarınızı buluta kullanarak bağlanmasına nasıl öğrenin [Azure IOT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="d120a-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="d120a-107">Neler</span><span class="sxs-lookup"><span data-stu-id="d120a-107">What you do</span></span>

<span data-ttu-id="d120a-108">Adafruit yumuşatma M0 WiFi oluşturduğunuz bir IOT hub'ına bağlanın.</span><span class="sxs-lookup"><span data-stu-id="d120a-108">Connect Adafruit Feather M0 WiFi to an IoT hub that you create.</span></span> <span data-ttu-id="d120a-109">Sonra M0 BME280 sıcaklık ve nem veri toplamak üzere WiFi üzerinde bir örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d120a-109">Then you run a sample application on M0 WiFi to collect the temperature and humidity data from a BME280.</span></span> <span data-ttu-id="d120a-110">Son olarak, IOT hub'ınıza algılayıcı verileri gönderin.</span><span class="sxs-lookup"><span data-stu-id="d120a-110">Finally, you send the sensor data to your IoT hub.</span></span>


## <a name="what-you-learn"></a><span data-ttu-id="d120a-111">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="d120a-111">What you learn</span></span>

* <span data-ttu-id="d120a-112">IOT hub'ı oluşturma ve yumuşatma M0 WiFi için bir cihaz kaydetme</span><span class="sxs-lookup"><span data-stu-id="d120a-112">How to create an IoT hub and register a device for Feather M0 WiFi</span></span>
* <span data-ttu-id="d120a-113">Algılayıcı ve bilgisayarınızla yumuşatma M0 WiFi bağlanma</span><span class="sxs-lookup"><span data-stu-id="d120a-113">How to connect Feather M0 WiFi with the sensor and your computer</span></span>
* <span data-ttu-id="d120a-114">Yumuşatma M0 WiFi üzerinde bir örnek uygulamayı çalıştırarak algılayıcı verilerini toplamak nasıl</span><span class="sxs-lookup"><span data-stu-id="d120a-114">How to collect sensor data by running a sample application on Feather M0 WiFi</span></span>
* <span data-ttu-id="d120a-115">IOT hub'ınıza algılayıcı verileri gönderme</span><span class="sxs-lookup"><span data-stu-id="d120a-115">How to send the sensor data to your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d120a-116">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="d120a-116">What you need</span></span>

![Öğretici için gerekli bölümleri](media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="d120a-118">Bu işlemi tamamlamak için aşağıdaki bölümleri yumuşatma M0 WiFi Starter Seti'nden gerekir:</span><span class="sxs-lookup"><span data-stu-id="d120a-118">To complete this operation, you need the following parts from your Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="d120a-119">Yumuşatma M0 WiFi Panosu</span><span class="sxs-lookup"><span data-stu-id="d120a-119">The Feather M0 WiFi board</span></span>
* <span data-ttu-id="d120a-120">Mikro USB tipi A USB kablosu</span><span class="sxs-lookup"><span data-stu-id="d120a-120">A Micro USB to Type A USB cable</span></span>

<span data-ttu-id="d120a-121">Ayrıca, geliştirme ortamınız için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="d120a-121">You also need the following things for your development environment:</span></span>

* <span data-ttu-id="d120a-122">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="d120a-122">An active Azure subscription.</span></span> <span data-ttu-id="d120a-123">Bir Azure hesabınız yoksa [ücretsiz Azure deneme hesabı oluşturma](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="d120a-123">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="d120a-124">Mac veya Windows veya Ubuntu çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="d120a-124">A Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="d120a-125">Kablosuz ağ yumuşatma M0 WiFi bağlanmak için.</span><span class="sxs-lookup"><span data-stu-id="d120a-125">A wireless network for Feather M0 WiFi to connect to.</span></span>
* <span data-ttu-id="d120a-126">Yapılandırma Aracı indirmek için Internet bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="d120a-126">An Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="d120a-127">[Arduino IDE](https://www.arduino.cc/en/main/software) sürüm 1.6.8 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="d120a-127">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="d120a-128">Önceki sürümleri Azure IOT Hub kitaplığı ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="d120a-128">Earlier versions don't work with the Azure IoT Hub library.</span></span>

<span data-ttu-id="d120a-129">Algılayıcı yoksa, aşağıdaki öğeler isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="d120a-129">If you don’t have a sensor, the following items are optional.</span></span> <span data-ttu-id="d120a-130">Ayrıca sanal algılayıcı verilerini kullanma seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="d120a-130">You also have the option of using simulated sensor data:</span></span>

* <span data-ttu-id="d120a-131">BME280 sıcaklık ve nem algılayıcı</span><span class="sxs-lookup"><span data-stu-id="d120a-131">A BME280 temperature and humidity sensor</span></span>
* <span data-ttu-id="d120a-132">Bir breadboard</span><span class="sxs-lookup"><span data-stu-id="d120a-132">A breadboard</span></span>
* <span data-ttu-id="d120a-133">M/M anahtar kabloları</span><span class="sxs-lookup"><span data-stu-id="d120a-133">M/M jumper wires</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-the-sensor-and-your-computer"></a><span data-ttu-id="d120a-134">Algılayıcı ve bilgisayarınızla yumuşatma M0 WiFi Bağlan</span><span class="sxs-lookup"><span data-stu-id="d120a-134">Connect Feather M0 WiFi with the sensor and your computer</span></span>
<span data-ttu-id="d120a-135">Bu bölümde, algılayıcılar panonuz için bağlayın.</span><span class="sxs-lookup"><span data-stu-id="d120a-135">In this section, you connect the sensors to your board.</span></span> <span data-ttu-id="d120a-136">Daha sonra Cihazınızı başka kullanmak için bilgisayarınıza takın.</span><span class="sxs-lookup"><span data-stu-id="d120a-136">Then you plug in your device to your computer for further use.</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-feather-m0-wifi"></a><span data-ttu-id="d120a-137">Yumuşatma M0 WiFi DHT22 sıcaklık ve nem algılayıcı Bağlan</span><span class="sxs-lookup"><span data-stu-id="d120a-137">Connect a DHT22 temperature and humidity sensor to Feather M0 WiFi</span></span>

<span data-ttu-id="d120a-138">Bağlantıyı kurmak için breadboard ve anahtar kablolarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="d120a-138">Use the breadboard and jumper wires to make the connection.</span></span> <span data-ttu-id="d120a-139">Algılayıcı yoksa, benzetimli algılayıcı verilerini yerine kullandığından bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d120a-139">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Bağlantı Başvurusu](media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


<span data-ttu-id="d120a-141">Algılayıcı PIN'ler için aşağıdaki kablolama kullanın:</span><span class="sxs-lookup"><span data-stu-id="d120a-141">For sensor pins, use the following wiring:</span></span>


| <span data-ttu-id="d120a-142">Başlangıç (algılayıcı)</span><span class="sxs-lookup"><span data-stu-id="d120a-142">Start (sensor)</span></span>           | <span data-ttu-id="d120a-143">Bitiş (kartı)</span><span class="sxs-lookup"><span data-stu-id="d120a-143">End (board)</span></span>            | <span data-ttu-id="d120a-144">Kablo rengi</span><span class="sxs-lookup"><span data-stu-id="d120a-144">Cable color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="d120a-145">VDD (PIN 27A)</span><span class="sxs-lookup"><span data-stu-id="d120a-145">VDD (Pin 27A)</span></span>            | <span data-ttu-id="d120a-146">3v (PIN 3A)</span><span class="sxs-lookup"><span data-stu-id="d120a-146">3V (Pin 3A)</span></span>            | <span data-ttu-id="d120a-147">Kırmızı kablosu</span><span class="sxs-lookup"><span data-stu-id="d120a-147">Red cable</span></span>     |
| <span data-ttu-id="d120a-148">GND (PIN 29A)</span><span class="sxs-lookup"><span data-stu-id="d120a-148">GND (Pin 29A)</span></span>            | <span data-ttu-id="d120a-149">GND (PIN 6A)</span><span class="sxs-lookup"><span data-stu-id="d120a-149">GND (Pin 6A)</span></span>           | <span data-ttu-id="d120a-150">Siyah kablosu</span><span class="sxs-lookup"><span data-stu-id="d120a-150">Black cable</span></span>   |
| <span data-ttu-id="d120a-151">SCK (PIN 30A)</span><span class="sxs-lookup"><span data-stu-id="d120a-151">SCK (Pin 30A)</span></span>            | <span data-ttu-id="d120a-152">SCK (PIN 12A)</span><span class="sxs-lookup"><span data-stu-id="d120a-152">SCK (Pin 12A)</span></span>          | <span data-ttu-id="d120a-153">Sarı kablosu</span><span class="sxs-lookup"><span data-stu-id="d120a-153">Yellow cable</span></span>  |
| <span data-ttu-id="d120a-154">SDO (PIN 31A)</span><span class="sxs-lookup"><span data-stu-id="d120a-154">SDO (Pin 31A)</span></span>            | <span data-ttu-id="d120a-155">MI (PIN 14A)</span><span class="sxs-lookup"><span data-stu-id="d120a-155">MI (Pin 14A)</span></span>           | <span data-ttu-id="d120a-156">Beyaz kablosu</span><span class="sxs-lookup"><span data-stu-id="d120a-156">White cable</span></span>   |
| <span data-ttu-id="d120a-157">SDI (PIN 32A)</span><span class="sxs-lookup"><span data-stu-id="d120a-157">SDI (Pin 32A)</span></span>            | <span data-ttu-id="d120a-158">M0 (PIN 13A)</span><span class="sxs-lookup"><span data-stu-id="d120a-158">M0 (Pin 13A)</span></span>           | <span data-ttu-id="d120a-159">Mavi kablosu</span><span class="sxs-lookup"><span data-stu-id="d120a-159">Blue cable</span></span>    |
| <span data-ttu-id="d120a-160">CS (PIN 33A)</span><span class="sxs-lookup"><span data-stu-id="d120a-160">CS (Pin 33A)</span></span>             | <span data-ttu-id="d120a-161">GPIO'yu 5 (PIN 15J)</span><span class="sxs-lookup"><span data-stu-id="d120a-161">GPIO 5 (Pin 15J)</span></span>       | <span data-ttu-id="d120a-162">Turuncu kablosu</span><span class="sxs-lookup"><span data-stu-id="d120a-162">Orange cable</span></span>  |

<span data-ttu-id="d120a-163">Daha fazla bilgi için bkz: [Adafruit BME280 nem + Barometric baskısı sıcaklık algılayıcısı oturumdan](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) ve [Adafruit yumuşatma M0 WiFi no'lu](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span><span class="sxs-lookup"><span data-stu-id="d120a-163">For more information, see [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) and [Adafruit Feather M0 WiFi pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span></span>



<span data-ttu-id="d120a-164">Şimdi yumuşatma M0 WiFi ile çalışma algılayıcı bağlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d120a-164">Now your Feather M0 WiFi should be connected with a working sensor.</span></span>

![Yumuşatma Huzzah ile DHT22 Bağlan](media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-to-your-computer"></a><span data-ttu-id="d120a-166">Yumuşatma M0 WiFi bilgisayarınıza bağlayın</span><span class="sxs-lookup"><span data-stu-id="d120a-166">Connect Feather M0 WiFi to your computer</span></span>

<span data-ttu-id="d120a-167">Gösterildiği gibi bilgisayarınıza yumuşatma M0 WiFi bağlanmak için mikro USB tipi A USB kablosu kullanın:</span><span class="sxs-lookup"><span data-stu-id="d120a-167">Use the Micro USB to Type A USB cable to connect Feather M0 WiFi to your computer, as shown:</span></span>

![Yumuşatma Huzzah bilgisayarınıza bağlayın](media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="d120a-169">Seri bağlantı noktası izinleri (yalnızca Ubuntu) ekleyin</span><span class="sxs-lookup"><span data-stu-id="d120a-169">Add serial port permissions (Ubuntu only)</span></span>

<span data-ttu-id="d120a-170">Ubuntu kullanırsanız, USB bağlantı noktası, yumuşatma M0 WiFi üzerinde çalışması için izinlere sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d120a-170">If you use Ubuntu, make sure you have the permissions to operate on the USB port of Feather M0 WiFi.</span></span> <span data-ttu-id="d120a-171">Seri bağlantı noktası izinleri eklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d120a-171">To add serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="d120a-172">Bir terminal aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d120a-172">At a terminal, run the following commands:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="d120a-173">Aşağıdaki çıktıları birini alın:</span><span class="sxs-lookup"><span data-stu-id="d120a-173">You get one of the following outputs:</span></span>

   * <span data-ttu-id="d120a-174">crw-rw---1 kök uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="d120a-174">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="d120a-175">crw-rw---1 kök araması xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="d120a-175">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="d120a-176">Çıktıda dikkat `uucp` veya `dialout` USB bağlantı noktasına Grup sahibi adıdır.</span><span class="sxs-lookup"><span data-stu-id="d120a-176">In the output, notice that `uucp` or `dialout` is the group owner name of the USB port.</span></span>

2. <span data-ttu-id="d120a-177">Gruba kullanıcı eklemek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d120a-177">To add the user to the group, run the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="d120a-178">Önceki adımda aldığınız Grup sahibi adı `<group-owner-name>`.</span><span class="sxs-lookup"><span data-stu-id="d120a-178">In the previous step, you obtained the group owner name `<group-owner-name>`.</span></span> <span data-ttu-id="d120a-179">Ubuntu kullanıcı adınız `<username>`.</span><span class="sxs-lookup"><span data-stu-id="d120a-179">Your Ubuntu user name is `<username>`.</span></span>

3. <span data-ttu-id="d120a-180">Değişiklik görünür, Ubuntu dışında oturum açın ve yeniden oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d120a-180">For the change to appear, sign out of Ubuntu and then sign in again.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="d120a-181">Algılayıcı verilerini toplamak ve IOT hub'ınıza gönderin</span><span class="sxs-lookup"><span data-stu-id="d120a-181">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="d120a-182">Bu bölümde, dağıtın ve yumuşatma M0 WiFi üzerinde bir örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d120a-182">In this section, you deploy and run a sample application on Feather M0 WiFi.</span></span> <span data-ttu-id="d120a-183">Örnek uygulama LED blink yumuşatma M0 WiFi üzerinde yapar.</span><span class="sxs-lookup"><span data-stu-id="d120a-183">The sample application makes the LED blink on Feather M0 WiFi.</span></span> <span data-ttu-id="d120a-184">Ardından, IOT hub'ınıza BME280 algılayıcı toplanan sıcaklık ve nem verileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="d120a-184">It then sends the temperature and humidity data collected from the BME280 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github-and-prepare-the-arduino-ide"></a><span data-ttu-id="d120a-185">Örnek uygulama Github'dan alma ve Arduino IDE hazırlama</span><span class="sxs-lookup"><span data-stu-id="d120a-185">Get the sample application from GitHub and prepare the Arduino IDE</span></span>

<span data-ttu-id="d120a-186">Örnek uygulama, GitHub üzerinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="d120a-186">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="d120a-187">Github'dan örnek uygulamayı içeren örnek depoyu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d120a-187">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="d120a-188">Örnek deposuna kopyalamak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d120a-188">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="d120a-189">Bir komut istemi veya terminal penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="d120a-189">Open a command prompt or a terminal window.</span></span>

2. <span data-ttu-id="d120a-190">Depolanması için örnek uygulama istediğiniz bir klasöre gidin.</span><span class="sxs-lookup"><span data-stu-id="d120a-190">Go to a folder where you want the sample application to be stored.</span></span>
3. <span data-ttu-id="d120a-191">Şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d120a-191">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

### <a name="install-the-package-for-feather-m0-wifi-in-the-arduino-ide"></a><span data-ttu-id="d120a-192">Yumuşatma M0 WiFi Arduino IDE'de paketi yükle</span><span class="sxs-lookup"><span data-stu-id="d120a-192">Install the package for Feather M0 WiFi in the Arduino IDE</span></span>

1. <span data-ttu-id="d120a-193">Örnek uygulama depolandığı klasörü açın.</span><span class="sxs-lookup"><span data-stu-id="d120a-193">Open the folder where the sample application is stored.</span></span>

2. <span data-ttu-id="d120a-194">Arduino IDE uygulama klasöründe app.ino dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="d120a-194">Open the app.ino file in the app folder in the Arduino IDE.</span></span>

   ![Örnek uygulamayı Arduino IDE içinde Aç](media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)


1. <span data-ttu-id="d120a-196">Tıklatın **dosya** > **Tercihler** (Windows/Linux) veya **Arduino** > **Tercihler** (Mac) kopyalayıp ve Aşağıdaki bağlantıda içine yapıştırma **ek panoları yöneticisi URL'leri** Arduino IDE tercihlerinde seçeneği.</span><span class="sxs-lookup"><span data-stu-id="d120a-196">Click **File** > **Preferences** (Windows/Linux) or **Arduino** > **Preferences** (Mac) and copy and paste the link below into the **Additional Boards Manager URLs** option in the Arduino IDE preferences.</span></span>
   
   ```
   https://adafruit.github.io/arduino-board-index/package_adafruit_index.json, https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```

1. <span data-ttu-id="d120a-197">' I tıklatın **Araçları** > **Panosu** > **panoları Yöneticisi**ve ardından yükleyin `Arduino SAMD Boards` sürüm `1.6.2` veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="d120a-197">Click **Tools** > **Board** > **Boards Manager**, and then install the `Arduino SAMD Boards` version `1.6.2` or later.</span></span> 

1. <span data-ttu-id="d120a-198">Aynı pencerede yüklemek `Adafruit SAMD Boards` Panosu dosya tanımları eklemek için paket.</span><span class="sxs-lookup"><span data-stu-id="d120a-198">Then in the same window, install `Adafruit SAMD Boards` package to add the board file definitions.</span></span>

   ![esp8266 paketi yüklü](media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

4. <span data-ttu-id="d120a-200">Tıklatın **Araçları** > **Panosu** > **Adafruit M0 WiFi**.</span><span class="sxs-lookup"><span data-stu-id="d120a-200">Click **Tools** > **Board** > **Adafruit M0 WiFi**.</span></span>

5. <span data-ttu-id="d120a-201">Sürücüleri (yalnızca Windows için) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d120a-201">Install drivers (for Windows only).</span></span> <span data-ttu-id="d120a-202">Yumuşatma M0 WiFi bağladığınızda, bir sürücü yüklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="d120a-202">When you plug in Feather M0 WiFi, you might need to install a driver.</span></span> <span data-ttu-id="d120a-203">Tıklatın [sayfasındaki indirme bağlantısı](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) sürücü yükleyici indirmek için.</span><span class="sxs-lookup"><span data-stu-id="d120a-203">Click [the download link on the webpage](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) to download the driver installer.</span></span> <span data-ttu-id="d120a-204">İstediğiniz sürücüleri yüklemek için adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="d120a-204">Follow the steps to install the drivers you want.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="d120a-205">Gerekli kitaplıkları yükleme</span><span class="sxs-lookup"><span data-stu-id="d120a-205">Install necessary libraries</span></span>

1. <span data-ttu-id="d120a-206">Arduino IDE'de tıklatın **taslak** > **dahil Kitaplığı** > **yönetmek kitaplıkları**.</span><span class="sxs-lookup"><span data-stu-id="d120a-206">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>

2. <span data-ttu-id="d120a-207">Aşağıdaki Kitaplığı Ara tek tek adları.</span><span class="sxs-lookup"><span data-stu-id="d120a-207">Search for the following library names one by one.</span></span> <span data-ttu-id="d120a-208">Bulduğunuz her kitaplığını tıklatın **yükleme**:</span><span class="sxs-lookup"><span data-stu-id="d120a-208">For each library that you find, click **Install**:</span></span>

   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

3. <span data-ttu-id="d120a-209">El ile yüklemeniz `Adafruit_WINC1500`.</span><span class="sxs-lookup"><span data-stu-id="d120a-209">Manually install `Adafruit_WINC1500`.</span></span> <span data-ttu-id="d120a-210">Git [bu Web sitesi](https://github.com/adafruit/Adafruit_WINC1500) tıklatıp **Kopyala veya indir** > **ZIP'i indir**.</span><span class="sxs-lookup"><span data-stu-id="d120a-210">Go to [this website](https://github.com/adafruit/Adafruit_WINC1500) and click **Clone or download** > **Download ZIP**.</span></span> <span data-ttu-id="d120a-211">Arduino IDE'yi geçin **taslak** > **dahil Kitaplığı** > **.zip Kitaplığı eklemek** ve zip dosyası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d120a-211">Then in your Arduino IDE, go to **Sketch** > **Include Library** > **Add .zip Library** and add the zip file.</span></span>

### <a name="use-the-sample-application-if-you-dont-have-a-real-bme280-sensor"></a><span data-ttu-id="d120a-212">Örnek uygulamayı gerçek BME280 algılayıcı yoksa kullanın</span><span class="sxs-lookup"><span data-stu-id="d120a-212">Use the sample application if you don’t have a real BME280 sensor</span></span>

<span data-ttu-id="d120a-213">Gerçek BME280 algılayıcı yoksa, örnek uygulamayı sıcaklık ve nem veri benzetimini yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d120a-213">If you don’t have a real BME280 sensor, the sample application can simulate temperature and humidity data.</span></span> <span data-ttu-id="d120a-214">Örnek uygulamayı benzetimli veri kullanacak şekilde ayarlamak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d120a-214">To set up the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="d120a-215">Açık `config.h` dosyasını `app` klasör.</span><span class="sxs-lookup"><span data-stu-id="d120a-215">Open the `config.h` file in the `app` folder.</span></span>

2. <span data-ttu-id="d120a-216">Aşağıdaki kod satırını bulun ve değeri değiştirin `false` için `true`:</span><span class="sxs-lookup"><span data-stu-id="d120a-216">Locate the following line of code and change the value from `false` to `true`:</span></span>

   ```c
   define SIMULATED_DATA true
   ```
   ![Örnek uygulamayı benzetimli veri kullanacak şekilde yapılandırma](media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

3. <span data-ttu-id="d120a-218">Dosyayı kaydetmek `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="d120a-218">Save the file with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-feather-m0-wifi"></a><span data-ttu-id="d120a-219">Yumuşatma M0 WiFi örnek uygulamayı dağıtmak</span><span class="sxs-lookup"><span data-stu-id="d120a-219">Deploy the sample application to Feather M0 WiFi</span></span>

1. <span data-ttu-id="d120a-220">Arduino IDE'de tıklatın **aracı** > **bağlantı noktası**ve yumuşatma M0 WiFi için seri bağlantı noktası'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d120a-220">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Feather M0 WiFi.</span></span>

2. <span data-ttu-id="d120a-221">' I tıklatın **taslak** > **karşıya** oluşturup yumuşatma M0 WiFi örnek uygulamayı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="d120a-221">Click **Sketch** > **Upload** to build and deploy the sample application to Feather M0 WiFi.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="d120a-222">Kimlik bilgilerinizi girin</span><span class="sxs-lookup"><span data-stu-id="d120a-222">Enter your credentials</span></span>

<span data-ttu-id="d120a-223">Karşıya yükleme başarıyla tamamlandıktan sonra kimlik bilgilerinizi girmeniz için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d120a-223">After the upload completes successfully, follow these steps to enter your credentials:</span></span>

1. <span data-ttu-id="d120a-224">Arduino IDE'de tıklatın **Araçları** > **seri İzleyici**.</span><span class="sxs-lookup"><span data-stu-id="d120a-224">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>

2. <span data-ttu-id="d120a-225">Seri İzleyici penceresinin sağ alt köşesinde seçin **hiçbir satır bitiş** sol aşağı açılan listesinde.</span><span class="sxs-lookup"><span data-stu-id="d120a-225">In the lower-right corner of the serial monitor window, select **No line ending** in the drop-down list on the left.</span></span>
3. <span data-ttu-id="d120a-226">Seçin **115200 baud** sağdaki aşağı açılan listesinde.</span><span class="sxs-lookup"><span data-stu-id="d120a-226">Select **115200 baud** in the drop-down list on the right.</span></span>
4. <span data-ttu-id="d120a-227">' A tıklayın ve bunu sağlamak için sorulursa üst giriş kutusuna aşağıdaki bilgileri girin **Gönder**:</span><span class="sxs-lookup"><span data-stu-id="d120a-227">In the input box at the top, enter the following information if you're asked to provide it, and click **Send**:</span></span>

   * <span data-ttu-id="d120a-228">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="d120a-228">Wi-Fi SSID</span></span>
   * <span data-ttu-id="d120a-229">Wi-Fi parola</span><span class="sxs-lookup"><span data-stu-id="d120a-229">Wi-Fi password</span></span>
   * <span data-ttu-id="d120a-230">Cihaz bağlantı dizesi</span><span class="sxs-lookup"><span data-stu-id="d120a-230">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="d120a-231">Kimlik bilgisi EEPROM, yumuşatma M0 WiFi içinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="d120a-231">The credential information is stored in the EEPROM of Feather M0 WiFi.</span></span> <span data-ttu-id="d120a-232">Yumuşatma M0 WiFi panosunda Sıfırla düğmesini tıklatın, örnek uygulamayı bilgileri silmek isteyip istemediğinizi sorar.</span><span class="sxs-lookup"><span data-stu-id="d120a-232">If you click the reset button on the Feather M0 WiFi board, the sample application asks if you want to erase the information.</span></span> <span data-ttu-id="d120a-233">Girin `Y` bilgileri silmek için.</span><span class="sxs-lookup"><span data-stu-id="d120a-233">Enter `Y` to erase the information.</span></span> <span data-ttu-id="d120a-234">İkinci kez bilgileri vermeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="d120a-234">You're asked to provide the information a second time.</span></span>

### <a name="verify-that-the-sample-application-is-running-successfully"></a><span data-ttu-id="d120a-235">Örnek Uygulama başarıyla çalıştığını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="d120a-235">Verify that the sample application is running successfully</span></span>

<span data-ttu-id="d120a-236">Yumuşatma M0 WiFi üzerinde seri İzleyici penceresinin ve yanıp sönen LED aşağıdaki çıkışı görürseniz örnek uygulama başarıyla çalıştırma:</span><span class="sxs-lookup"><span data-stu-id="d120a-236">If you see the following output from the serial monitor window and the blinking LED on Feather M0 WiFi, the sample application is running successfully:</span></span>

![Arduino IDE içinde son çıktı](media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="d120a-238">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d120a-238">Next steps</span></span>

<span data-ttu-id="d120a-239">Başarıyla yumuşatma M0 WiFi IOT hub'ına bağlı ve IOT hub'ınıza yakalanan algılayıcı verilerini gönderilir.</span><span class="sxs-lookup"><span data-stu-id="d120a-239">You have successfully connected Feather M0 WiFi to your IoT hub and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

