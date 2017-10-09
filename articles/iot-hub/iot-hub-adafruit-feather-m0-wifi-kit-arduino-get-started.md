---
title: "M0 toocloud: yumuşatma M0 WiFi tooAzure IOT hub'ı bağlanma | Microsoft Docs"
description: "Bilgi nasıl tooset yukarı ve Bu öğreticide Adafruit yumuşatma M0 WiFi tooAzure IOT hub'ı toosend veri toohello Azure bulut platformu bağlanın."
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
ms.openlocfilehash: 6aabeb961a50ba5d3934f77eb1ccda4af1bf64c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-m0-wifi-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="8d9b2-103">Adafruit yumuşatma M0 WiFi tooAzure IOT Hub'hello bulutta Bağlan</span><span class="sxs-lookup"><span data-stu-id="8d9b2-103">Connect Adafruit Feather M0 WiFi tooAzure IoT Hub in hello cloud</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![BME280, yumuşatma M0 WiFi ve IOT hub'ı arasında bir bağlantı](media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

<span data-ttu-id="8d9b2-105">Bu öğreticide, Arduino panonuzu ile çalışmanın hello temelleri öğrenerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-105">In this tutorial, you begin by learning hello basics of working with your Arduino board.</span></span> <span data-ttu-id="8d9b2-106">Daha sonra nasıl tooseamlessly bağlanacağını aygıtları toohello bulutunuzu kullanarak öğrenin [Azure IOT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="8d9b2-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="8d9b2-107">Neler</span><span class="sxs-lookup"><span data-stu-id="8d9b2-107">What you do</span></span>

<span data-ttu-id="8d9b2-108">Oluşturduğunuz Adafruit yumuşatma M0 WiFi tooan IOT hub bağlayın.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-108">Connect Adafruit Feather M0 WiFi tooan IoT hub that you create.</span></span> <span data-ttu-id="8d9b2-109">Daha sonra örnek bir uygulama BME280 sıcaklık ve nem M0 WiFi toocollect hello verileri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-109">Then you run a sample application on M0 WiFi toocollect hello temperature and humidity data from a BME280.</span></span> <span data-ttu-id="8d9b2-110">Son olarak, hello algılayıcı verileri tooyour IOT hub'ı gönderin.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-110">Finally, you send hello sensor data tooyour IoT hub.</span></span>


## <a name="what-you-learn"></a><span data-ttu-id="8d9b2-111">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="8d9b2-111">What you learn</span></span>

* <span data-ttu-id="8d9b2-112">Nasıl toocreate IOT hub'ı ve yumuşatma M0 WiFi için bir cihaz kaydetme</span><span class="sxs-lookup"><span data-stu-id="8d9b2-112">How toocreate an IoT hub and register a device for Feather M0 WiFi</span></span>
* <span data-ttu-id="8d9b2-113">Nasıl tooconnect yumuşatma M0 WiFi hello algılayıcı ve bilgisayarınız</span><span class="sxs-lookup"><span data-stu-id="8d9b2-113">How tooconnect Feather M0 WiFi with hello sensor and your computer</span></span>
* <span data-ttu-id="8d9b2-114">Nasıl yumuşatma M0 WiFi üzerinde bir örnek uygulamayı çalıştırarak toocollect algılayıcı verileri</span><span class="sxs-lookup"><span data-stu-id="8d9b2-114">How toocollect sensor data by running a sample application on Feather M0 WiFi</span></span>
* <span data-ttu-id="8d9b2-115">Nasıl toosend hello algılayıcı verileri tooyour IOT hub'ı</span><span class="sxs-lookup"><span data-stu-id="8d9b2-115">How toosend hello sensor data tooyour IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8d9b2-116">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="8d9b2-116">What you need</span></span>

![Merhaba öğretici için gerekli bölümleri](media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="8d9b2-118">toocomplete bu işlemi yumuşatma M0 WiFi Starter Seti'nden bölümleri aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="8d9b2-118">toocomplete this operation, you need hello following parts from your Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="8d9b2-119">Merhaba yumuşatma M0 WiFi Panosu</span><span class="sxs-lookup"><span data-stu-id="8d9b2-119">hello Feather M0 WiFi board</span></span>
* <span data-ttu-id="8d9b2-120">Mikro USB tooType bir USB kablosu</span><span class="sxs-lookup"><span data-stu-id="8d9b2-120">A Micro USB tooType A USB cable</span></span>

<span data-ttu-id="8d9b2-121">Ayrıca geliştirme ortamınız için öğeleri izleyen hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="8d9b2-121">You also need hello following things for your development environment:</span></span>

* <span data-ttu-id="8d9b2-122">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-122">An active Azure subscription.</span></span> <span data-ttu-id="8d9b2-123">Bir Azure hesabınız yoksa [ücretsiz Azure deneme hesabı oluşturma](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-123">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="8d9b2-124">Mac veya Windows veya Ubuntu çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-124">A Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="8d9b2-125">Kablosuz ağ yumuşatma M0 WiFi tooconnect için.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-125">A wireless network for Feather M0 WiFi tooconnect to.</span></span>
* <span data-ttu-id="8d9b2-126">Bir Internet bağlantısı toodownload hello yapılandırma aracı.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-126">An Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="8d9b2-127">[Arduino IDE](https://www.arduino.cc/en/main/software) sürüm 1.6.8 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-127">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="8d9b2-128">Önceki sürümlerde hello Azure IOT Hub kitaplığı ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-128">Earlier versions don't work with hello Azure IoT Hub library.</span></span>

<span data-ttu-id="8d9b2-129">Algılayıcı yoksa, aşağıdaki öğelerindeki hello isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-129">If you don’t have a sensor, hello following items are optional.</span></span> <span data-ttu-id="8d9b2-130">Benzetimli algılayıcı verilerini kullanarak hello seçeneğiniz de vardır:</span><span class="sxs-lookup"><span data-stu-id="8d9b2-130">You also have hello option of using simulated sensor data:</span></span>

* <span data-ttu-id="8d9b2-131">BME280 sıcaklık ve nem algılayıcı</span><span class="sxs-lookup"><span data-stu-id="8d9b2-131">A BME280 temperature and humidity sensor</span></span>
* <span data-ttu-id="8d9b2-132">Bir breadboard</span><span class="sxs-lookup"><span data-stu-id="8d9b2-132">A breadboard</span></span>
* <span data-ttu-id="8d9b2-133">M/M anahtar kabloları</span><span class="sxs-lookup"><span data-stu-id="8d9b2-133">M/M jumper wires</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-hello-sensor-and-your-computer"></a><span data-ttu-id="8d9b2-134">Merhaba algılayıcı ve bilgisayarınızla yumuşatma M0 WiFi Bağlan</span><span class="sxs-lookup"><span data-stu-id="8d9b2-134">Connect Feather M0 WiFi with hello sensor and your computer</span></span>
<span data-ttu-id="8d9b2-135">Bu bölümde, hello algılayıcılar tooyour Panosu bağlayın.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-135">In this section, you connect hello sensors tooyour board.</span></span> <span data-ttu-id="8d9b2-136">Ardından aygıt tooyour bilgisayarınızdaki başka kullanmak için takın.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-136">Then you plug in your device tooyour computer for further use.</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-m0-wifi"></a><span data-ttu-id="8d9b2-137">Bir DHT22 sıcaklık ve nem algılayıcı tooFeather M0 WiFi Bağlan</span><span class="sxs-lookup"><span data-stu-id="8d9b2-137">Connect a DHT22 temperature and humidity sensor tooFeather M0 WiFi</span></span>

<span data-ttu-id="8d9b2-138">Merhaba breadboard ve anahtar kablolarını toomake hello bağlantısı kullanın.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-138">Use hello breadboard and jumper wires toomake hello connection.</span></span> <span data-ttu-id="8d9b2-139">Algılayıcı yoksa, benzetimli algılayıcı verilerini yerine kullandığından bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-139">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Bağlantı Başvurusu](media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


<span data-ttu-id="8d9b2-141">Algılayıcı PIN'ler için kablolama aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="8d9b2-141">For sensor pins, use hello following wiring:</span></span>


| <span data-ttu-id="8d9b2-142">Başlangıç (algılayıcı)</span><span class="sxs-lookup"><span data-stu-id="8d9b2-142">Start (sensor)</span></span>           | <span data-ttu-id="8d9b2-143">Bitiş (kartı)</span><span class="sxs-lookup"><span data-stu-id="8d9b2-143">End (board)</span></span>            | <span data-ttu-id="8d9b2-144">Kablo rengi</span><span class="sxs-lookup"><span data-stu-id="8d9b2-144">Cable color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="8d9b2-145">VDD (PIN 27A)</span><span class="sxs-lookup"><span data-stu-id="8d9b2-145">VDD (Pin 27A)</span></span>            | <span data-ttu-id="8d9b2-146">3v (PIN 3A)</span><span class="sxs-lookup"><span data-stu-id="8d9b2-146">3V (Pin 3A)</span></span>            | <span data-ttu-id="8d9b2-147">Kırmızı kablosu</span><span class="sxs-lookup"><span data-stu-id="8d9b2-147">Red cable</span></span>     |
| <span data-ttu-id="8d9b2-148">GND (PIN 29A)</span><span class="sxs-lookup"><span data-stu-id="8d9b2-148">GND (Pin 29A)</span></span>            | <span data-ttu-id="8d9b2-149">GND (PIN 6A)</span><span class="sxs-lookup"><span data-stu-id="8d9b2-149">GND (Pin 6A)</span></span>           | <span data-ttu-id="8d9b2-150">Siyah kablosu</span><span class="sxs-lookup"><span data-stu-id="8d9b2-150">Black cable</span></span>   |
| <span data-ttu-id="8d9b2-151">SCK (PIN 30A)</span><span class="sxs-lookup"><span data-stu-id="8d9b2-151">SCK (Pin 30A)</span></span>            | <span data-ttu-id="8d9b2-152">SCK (PIN 12A)</span><span class="sxs-lookup"><span data-stu-id="8d9b2-152">SCK (Pin 12A)</span></span>          | <span data-ttu-id="8d9b2-153">Sarı kablosu</span><span class="sxs-lookup"><span data-stu-id="8d9b2-153">Yellow cable</span></span>  |
| <span data-ttu-id="8d9b2-154">SDO (PIN 31A)</span><span class="sxs-lookup"><span data-stu-id="8d9b2-154">SDO (Pin 31A)</span></span>            | <span data-ttu-id="8d9b2-155">MI (PIN 14A)</span><span class="sxs-lookup"><span data-stu-id="8d9b2-155">MI (Pin 14A)</span></span>           | <span data-ttu-id="8d9b2-156">Beyaz kablosu</span><span class="sxs-lookup"><span data-stu-id="8d9b2-156">White cable</span></span>   |
| <span data-ttu-id="8d9b2-157">SDI (PIN 32A)</span><span class="sxs-lookup"><span data-stu-id="8d9b2-157">SDI (Pin 32A)</span></span>            | <span data-ttu-id="8d9b2-158">M0 (PIN 13A)</span><span class="sxs-lookup"><span data-stu-id="8d9b2-158">M0 (Pin 13A)</span></span>           | <span data-ttu-id="8d9b2-159">Mavi kablosu</span><span class="sxs-lookup"><span data-stu-id="8d9b2-159">Blue cable</span></span>    |
| <span data-ttu-id="8d9b2-160">CS (PIN 33A)</span><span class="sxs-lookup"><span data-stu-id="8d9b2-160">CS (Pin 33A)</span></span>             | <span data-ttu-id="8d9b2-161">GPIO'yu 5 (PIN 15J)</span><span class="sxs-lookup"><span data-stu-id="8d9b2-161">GPIO 5 (Pin 15J)</span></span>       | <span data-ttu-id="8d9b2-162">Turuncu kablosu</span><span class="sxs-lookup"><span data-stu-id="8d9b2-162">Orange cable</span></span>  |

<span data-ttu-id="8d9b2-163">Daha fazla bilgi için bkz: [Adafruit BME280 nem + Barometric baskısı sıcaklık algılayıcısı oturumdan](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) ve [Adafruit yumuşatma M0 WiFi no'lu](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span><span class="sxs-lookup"><span data-stu-id="8d9b2-163">For more information, see [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) and [Adafruit Feather M0 WiFi pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span></span>



<span data-ttu-id="8d9b2-164">Şimdi yumuşatma M0 WiFi ile çalışma algılayıcı bağlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-164">Now your Feather M0 WiFi should be connected with a working sensor.</span></span>

![Yumuşatma Huzzah ile DHT22 Bağlan](media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-tooyour-computer"></a><span data-ttu-id="8d9b2-166">Yumuşatma M0 WiFi tooyour bilgisayara bağlanma</span><span class="sxs-lookup"><span data-stu-id="8d9b2-166">Connect Feather M0 WiFi tooyour computer</span></span>

<span data-ttu-id="8d9b2-167">Merhaba mikro USB tooType bir USB kablosu tooconnect yumuşatma M0 WiFi tooyour bilgisayar, gösterildiği gibi kullanın:</span><span class="sxs-lookup"><span data-stu-id="8d9b2-167">Use hello Micro USB tooType A USB cable tooconnect Feather M0 WiFi tooyour computer, as shown:</span></span>

![Yumuşatma Huzzah tooyour bilgisayara bağlanma](media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="8d9b2-169">Seri bağlantı noktası izinleri (yalnızca Ubuntu) ekleyin</span><span class="sxs-lookup"><span data-stu-id="8d9b2-169">Add serial port permissions (Ubuntu only)</span></span>

<span data-ttu-id="8d9b2-170">Ubuntu kullanırsanız, hello izinleri toooperate hello USB bağlantı noktası, yumuşatma M0 WiFi üzerinde olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-170">If you use Ubuntu, make sure you have hello permissions toooperate on hello USB port of Feather M0 WiFi.</span></span> <span data-ttu-id="8d9b2-171">tooadd seri bağlantı noktası izinleri, aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="8d9b2-171">tooadd serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="8d9b2-172">Bir terminal hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8d9b2-172">At a terminal, run hello following commands:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="8d9b2-173">Çıktı aşağıdaki hello birini alın:</span><span class="sxs-lookup"><span data-stu-id="8d9b2-173">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="8d9b2-174">crw-rw---1 kök uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="8d9b2-174">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="8d9b2-175">crw-rw---1 kök araması xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="8d9b2-175">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="8d9b2-176">Merhaba çıktısında dikkat `uucp` veya `dialout` hello Grup sahibi hello USB bağlantı noktasına adıdır.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-176">In hello output, notice that `uucp` or `dialout` is hello group owner name of hello USB port.</span></span>

2. <span data-ttu-id="8d9b2-177">komutu aşağıdaki hello çalıştırmak tooadd hello kullanıcı toohello grubunun:</span><span class="sxs-lookup"><span data-stu-id="8d9b2-177">tooadd hello user toohello group, run hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="8d9b2-178">Merhaba önceki adımda aldığınız hello Grup sahibi adı `<group-owner-name>`.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-178">In hello previous step, you obtained hello group owner name `<group-owner-name>`.</span></span> <span data-ttu-id="8d9b2-179">Ubuntu kullanıcı adınız `<username>`.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-179">Your Ubuntu user name is `<username>`.</span></span>

3. <span data-ttu-id="8d9b2-180">Merhaba değişiklik tooappear dışında Ubuntu oturum ve yeniden oturum açın.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-180">For hello change tooappear, sign out of Ubuntu and then sign in again.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="8d9b2-181">Algılayıcı verilerini toplamak ve tooyour IOT hub'ı gönderin</span><span class="sxs-lookup"><span data-stu-id="8d9b2-181">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="8d9b2-182">Bu bölümde, dağıtın ve yumuşatma M0 WiFi üzerinde bir örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-182">In this section, you deploy and run a sample application on Feather M0 WiFi.</span></span> <span data-ttu-id="8d9b2-183">Merhaba örnek uygulaması yumuşatma M0 WiFi ışığı yanıp hello yapar.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-183">hello sample application makes hello LED blink on Feather M0 WiFi.</span></span> <span data-ttu-id="8d9b2-184">Ardından hello sıcaklık gönderir ve nem veri hello BME280 algılayıcı tooyour IOT hub'ı toplanmadı.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-184">It then sends hello temperature and humidity data collected from hello BME280 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github-and-prepare-hello-arduino-ide"></a><span data-ttu-id="8d9b2-185">Merhaba örnek uygulaması Github'dan alma ve hello Arduino IDE hazırlama</span><span class="sxs-lookup"><span data-stu-id="8d9b2-185">Get hello sample application from GitHub and prepare hello Arduino IDE</span></span>

<span data-ttu-id="8d9b2-186">Merhaba örnek uygulaması, GitHub üzerinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-186">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="8d9b2-187">Merhaba örnek uygulaması github'dan içeren hello örnek depoyu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-187">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="8d9b2-188">tooclone hello örnek deposu, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="8d9b2-188">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="8d9b2-189">Bir komut istemi veya terminal penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-189">Open a command prompt or a terminal window.</span></span>

2. <span data-ttu-id="8d9b2-190">Depolanan hello örnek uygulama toobe istediğiniz tooa klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-190">Go tooa folder where you want hello sample application toobe stored.</span></span>
3. <span data-ttu-id="8d9b2-191">Merhaba aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8d9b2-191">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

### <a name="install-hello-package-for-feather-m0-wifi-in-hello-arduino-ide"></a><span data-ttu-id="8d9b2-192">Merhaba paketini yumuşatma M0 WiFi hello Arduino IDE yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-192">Install hello package for Feather M0 WiFi in hello Arduino IDE</span></span>

1. <span data-ttu-id="8d9b2-193">Merhaba örnek uygulaması depolandığı hello klasörünü açın.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-193">Open hello folder where hello sample application is stored.</span></span>

2. <span data-ttu-id="8d9b2-194">Merhaba Arduino IDE hello uygulama klasöründe Hello app.ino dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-194">Open hello app.ino file in hello app folder in hello Arduino IDE.</span></span>

   ![Merhaba örnek uygulaması Arduino IDE içinde açın](media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)


1. <span data-ttu-id="8d9b2-196">Tıklatın **dosya** > **Tercihler** (Windows/Linux) veya **Arduino** > **Tercihler** (Mac) kopyalayıp ve Merhaba aşağıda Yapıştır hello bağlantıya **ek panoları yöneticisi URL'leri** Arduino IDE Tercihler hello seçeneği.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-196">Click **File** > **Preferences** (Windows/Linux) or **Arduino** > **Preferences** (Mac) and copy and paste hello link below into hello **Additional Boards Manager URLs** option in hello Arduino IDE preferences.</span></span>
   
   ```
   https://adafruit.github.io/arduino-board-index/package_adafruit_index.json, https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```

1. <span data-ttu-id="8d9b2-197">Tıklatın **Araçları** > **Panosu** > **panoları Yöneticisi**, yükleyip ardından hello `Arduino SAMD Boards` sürüm `1.6.2` veya üstü.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-197">Click **Tools** > **Board** > **Boards Manager**, and then install hello `Arduino SAMD Boards` version `1.6.2` or later.</span></span> 

1. <span data-ttu-id="8d9b2-198">Ardından Merhaba aynı penceresi, yükleme `Adafruit SAMD Boards` paketini tooadd hello Panosu dosya tanımları.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-198">Then in hello same window, install `Adafruit SAMD Boards` package tooadd hello board file definitions.</span></span>

   ![Merhaba esp8266 paketinin yüklü olduğu](media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

4. <span data-ttu-id="8d9b2-200">Tıklatın **Araçları** > **Panosu** > **Adafruit M0 WiFi**.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-200">Click **Tools** > **Board** > **Adafruit M0 WiFi**.</span></span>

5. <span data-ttu-id="8d9b2-201">Sürücüleri (yalnızca Windows için) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-201">Install drivers (for Windows only).</span></span> <span data-ttu-id="8d9b2-202">Yumuşatma M0 WiFi taktığınızda tooinstall bir sürücü gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-202">When you plug in Feather M0 WiFi, you might need tooinstall a driver.</span></span> <span data-ttu-id="8d9b2-203">Tıklatın [hello indirme bağlantısı hello Web sayfasındaki](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) toodownload hello sürücü yükleyicisi.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-203">Click [hello download link on hello webpage](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) toodownload hello driver installer.</span></span> <span data-ttu-id="8d9b2-204">Merhaba adımları tooinstall hello sürücüleri istediğiniz izleyin.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-204">Follow hello steps tooinstall hello drivers you want.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="8d9b2-205">Gerekli kitaplıkları yükleme</span><span class="sxs-lookup"><span data-stu-id="8d9b2-205">Install necessary libraries</span></span>

1. <span data-ttu-id="8d9b2-206">Hello Arduino IDE, tıklatın **taslak** > **dahil Kitaplığı** > **yönetmek kitaplıkları**.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-206">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>

2. <span data-ttu-id="8d9b2-207">Kitaplık adları tek tek aşağıdaki hello arayın.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-207">Search for hello following library names one by one.</span></span> <span data-ttu-id="8d9b2-208">Bulduğunuz her kitaplığını tıklatın **yükleme**:</span><span class="sxs-lookup"><span data-stu-id="8d9b2-208">For each library that you find, click **Install**:</span></span>

   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

3. <span data-ttu-id="8d9b2-209">El ile yüklemeniz `Adafruit_WINC1500`.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-209">Manually install `Adafruit_WINC1500`.</span></span> <span data-ttu-id="8d9b2-210">Çok Git[bu Web sitesi](https://github.com/adafruit/Adafruit_WINC1500) tıklatıp **Kopyala veya indir** > **ZIP'i indir**.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-210">Go too[this website](https://github.com/adafruit/Adafruit_WINC1500) and click **Clone or download** > **Download ZIP**.</span></span> <span data-ttu-id="8d9b2-211">Arduino IDE'yi çok Git**taslak** > **dahil Kitaplığı** > **.zip Kitaplığı eklemek** ve hello zip dosyası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-211">Then in your Arduino IDE, go too**Sketch** > **Include Library** > **Add .zip Library** and add hello zip file.</span></span>

### <a name="use-hello-sample-application-if-you-dont-have-a-real-bme280-sensor"></a><span data-ttu-id="8d9b2-212">Gerçek BME280 algılayıcı yoksa Merhaba örnek uygulaması kullanın</span><span class="sxs-lookup"><span data-stu-id="8d9b2-212">Use hello sample application if you don’t have a real BME280 sensor</span></span>

<span data-ttu-id="8d9b2-213">Gerçek BME280 algılayıcı yoksa, hello örnek uygulama sıcaklık ve nem veri benzetimini yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-213">If you don’t have a real BME280 sensor, hello sample application can simulate temperature and humidity data.</span></span> <span data-ttu-id="8d9b2-214">tooset hello örnek uygulama benzetimli toouse verileri, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="8d9b2-214">tooset up hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="8d9b2-215">Açık hello `config.h` hello dosyasında `app` klasör.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-215">Open hello `config.h` file in hello `app` folder.</span></span>

2. <span data-ttu-id="8d9b2-216">Aşağıdaki kod hello bulun ve hello değerinden değiştirmek `false` çok`true`:</span><span class="sxs-lookup"><span data-stu-id="8d9b2-216">Locate hello following line of code and change hello value from `false` too`true`:</span></span>

   ```c
   define SIMULATED_DATA true
   ```
   ![Merhaba örnek uygulama benzetimli toouse verileri yapılandırma](media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

3. <span data-ttu-id="8d9b2-218">Merhaba dosyayla Kaydet `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-218">Save hello file with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toofeather-m0-wifi"></a><span data-ttu-id="8d9b2-219">Merhaba örnek uygulama tooFeather M0 WiFi dağıtma</span><span class="sxs-lookup"><span data-stu-id="8d9b2-219">Deploy hello sample application tooFeather M0 WiFi</span></span>

1. <span data-ttu-id="8d9b2-220">Hello Arduino IDE, tıklatın **aracı** > **bağlantı noktası**ve yumuşatma M0 WiFi hello seri bağlantı noktası'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-220">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Feather M0 WiFi.</span></span>

2. <span data-ttu-id="8d9b2-221">Tıklatın **taslak** > **karşıya** toobuild ve hello örnek uygulama tooFeather M0 WiFi dağıtın.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-221">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooFeather M0 WiFi.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="8d9b2-222">Kimlik bilgilerinizi girin</span><span class="sxs-lookup"><span data-stu-id="8d9b2-222">Enter your credentials</span></span>

<span data-ttu-id="8d9b2-223">Merhaba karşıya yükleme başarıyla tamamlandıktan sonra bu adımları tooenter kimlik bilgilerinizi izleyin:</span><span class="sxs-lookup"><span data-stu-id="8d9b2-223">After hello upload completes successfully, follow these steps tooenter your credentials:</span></span>

1. <span data-ttu-id="8d9b2-224">Hello Arduino IDE, tıklatın **Araçları** > **seri İzleyici**.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-224">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>

2. <span data-ttu-id="8d9b2-225">Hello sağ alt köşesinde hello seri İzleyicisi penceresinde, seçin **hiçbir satır bitiş** hello soldaki hello aşağı açılan listesinde.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-225">In hello lower-right corner of hello serial monitor window, select **No line ending** in hello drop-down list on hello left.</span></span>
3. <span data-ttu-id="8d9b2-226">Seçin **115200 baud** hello sağ hello aşağı açılan listesinde.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-226">Select **115200 baud** in hello drop-down list on hello right.</span></span>
4. <span data-ttu-id="8d9b2-227">Merhaba giriş kutusuna hello üstünde kullanıcısıysanız bilgisinden hello girin ve tıklatın tooprovide sorulan **Gönder**:</span><span class="sxs-lookup"><span data-stu-id="8d9b2-227">In hello input box at hello top, enter hello following information if you're asked tooprovide it, and click **Send**:</span></span>

   * <span data-ttu-id="8d9b2-228">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="8d9b2-228">Wi-Fi SSID</span></span>
   * <span data-ttu-id="8d9b2-229">Wi-Fi parola</span><span class="sxs-lookup"><span data-stu-id="8d9b2-229">Wi-Fi password</span></span>
   * <span data-ttu-id="8d9b2-230">Cihaz bağlantı dizesi</span><span class="sxs-lookup"><span data-stu-id="8d9b2-230">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="8d9b2-231">Merhaba kimlik bilgileri hello yumuşatma M0 WiFi EEPROM depolanır.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-231">hello credential information is stored in hello EEPROM of Feather M0 WiFi.</span></span> <span data-ttu-id="8d9b2-232">Merhaba yumuşatma M0 WiFi Panosu hello Sıfırla düğmesini tıklatın, Merhaba örnek uygulaması tooerase hello bilgi isteyip istemediğinizi sorar.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-232">If you click hello reset button on hello Feather M0 WiFi board, hello sample application asks if you want tooerase hello information.</span></span> <span data-ttu-id="8d9b2-233">Girin `Y` tooerase hello bilgi.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-233">Enter `Y` tooerase hello information.</span></span> <span data-ttu-id="8d9b2-234">Tooprovide hello bilgi ikinci kez sorulur.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-234">You're asked tooprovide hello information a second time.</span></span>

### <a name="verify-that-hello-sample-application-is-running-successfully"></a><span data-ttu-id="8d9b2-235">Merhaba örnek uygulaması başarılı bir şekilde çalıştığını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="8d9b2-235">Verify that hello sample application is running successfully</span></span>

<span data-ttu-id="8d9b2-236">Görürseniz hello seri İzleyicisi penceresinde hello şu çıktıları ve LED yumuşatma M0 WiFi Merhaba örnek uygulaması üzerinde yanıp sönen hello başarıyla çalıştırma:</span><span class="sxs-lookup"><span data-stu-id="8d9b2-236">If you see hello following output from hello serial monitor window and hello blinking LED on Feather M0 WiFi, hello sample application is running successfully:</span></span>

![Arduino IDE içinde son çıktı](media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="8d9b2-238">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8d9b2-238">Next steps</span></span>

<span data-ttu-id="8d9b2-239">Başarıyla tooyour IOT hub'ı yumuşatma M0 WiFi bağlı ve yakalanan hello algılayıcı verileri tooyour IOT hub'ı gönderilir.</span><span class="sxs-lookup"><span data-stu-id="8d9b2-239">You have successfully connected Feather M0 WiFi tooyour IoT hub and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

