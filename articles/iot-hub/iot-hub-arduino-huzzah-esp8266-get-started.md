---
title: "Bulut için - ESP8266 yumuşatma HUZZAH ESP8266 Azure IOT Hub'ına bağlanmak | Microsoft Docs"
description: "Kurulum ve Bu öğreticide Azure bulut platformuna veri göndermek için Azure IOT Hub için bu Adafruit yumuşatma HUZZAH ESP8266 bağlanma hakkında bilgi edinin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: c505aacf-89a8-40ed-a853-493b75bec524
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: xshi
ms.openlocfilehash: 6a450579c848fe6030a328ddf410f139baae2324
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="b6ac6-103">Bulutta Azure IOT Hub'ına Adafruit yumuşatma HUZZAH ESP8266 Bağlan</span><span class="sxs-lookup"><span data-stu-id="b6ac6-103">Connect Adafruit Feather HUZZAH ESP8266 to Azure IoT Hub in the cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![DHT22, yumuşatma HUZZAH ESP8266 ve IOT hub'ı arasında bir bağlantı](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a><span data-ttu-id="b6ac6-105">Neler</span><span class="sxs-lookup"><span data-stu-id="b6ac6-105">What you do</span></span>


<span data-ttu-id="b6ac6-106">Adafruit yumuşatma HUZZAH ESP8266, oluşturduğunuz bir IOT hub'ına bağlanın.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-106">Connect Adafruit Feather HUZZAH ESP8266 to an IoT hub that you create.</span></span> <span data-ttu-id="b6ac6-107">Sonra DHT22 algılayıcı sıcaklık ve nem veri toplamak üzere ESP8266 üzerinde bir örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-107">Then you run a sample application on ESP8266 to collect the temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="b6ac6-108">Son olarak, IOT hub'ınıza algılayıcı verileri gönderin.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-108">Finally, you send the sensor data to your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="b6ac6-109">Diğer ESP8266 panoları kullanıyorsanız, yine IOT hub'ınıza bağlanmak için aşağıdaki adımları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-109">If you're using other ESP8266 boards, you can still follow these steps to connect it to your IoT hub.</span></span> <span data-ttu-id="b6ac6-110">Kullanmakta olduğunuz ESP8266 Panosu bağlı olarak, yeniden yapılandırmanız gerekebilir `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-110">Depending on the ESP8266 board you're using, you might need to reconfigure the `LED_PIN`.</span></span> <span data-ttu-id="b6ac6-111">AI Thinker gelen ESP8266 kullanıyorsanız, örneğin, ondan değişebilir `0` için `2`.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-111">For example, if you're using ESP8266 from AI-Thinker, you might change it from `0` to `2`.</span></span> <span data-ttu-id="b6ac6-112">Bir pakete henüz yok mu?</span><span class="sxs-lookup"><span data-stu-id="b6ac6-112">Don't have a kit yet?</span></span> <span data-ttu-id="b6ac6-113">Elde [Azure Web sitesi](http://azure.com/iotstarterkits).</span><span class="sxs-lookup"><span data-stu-id="b6ac6-113">Get it from the [Azure website](http://azure.com/iotstarterkits).</span></span>




## <a name="what-you-learn"></a><span data-ttu-id="b6ac6-114">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="b6ac6-114">What you learn</span></span>

* <span data-ttu-id="b6ac6-115">IOT hub'ı oluşturma ve yumuşatma HUZZAH ESP8266 için bir cihaz kaydetme</span><span class="sxs-lookup"><span data-stu-id="b6ac6-115">How to create an IoT hub and register a device for Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="b6ac6-116">Algılayıcı ve bilgisayarınızla yumuşatma HUZZAH ESP8266 bağlanma</span><span class="sxs-lookup"><span data-stu-id="b6ac6-116">How to connect Feather HUZZAH ESP8266 with the sensor and your computer</span></span>
* <span data-ttu-id="b6ac6-117">Yumuşatma HUZZAH ESP8266 üzerinde bir örnek uygulamayı çalıştırarak algılayıcı verilerini toplamak nasıl</span><span class="sxs-lookup"><span data-stu-id="b6ac6-117">How to collect sensor data by running a sample application on Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="b6ac6-118">IOT hub'ınıza algılayıcı verileri gönderme</span><span class="sxs-lookup"><span data-stu-id="b6ac6-118">How to send the sensor data to your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b6ac6-119">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="b6ac6-119">What you need</span></span>

![Öğretici için gerekli bölümleri](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="b6ac6-121">Bu işlemi tamamlamak için aşağıdaki bölümleri yumuşatma HUZZAH ESP8266 Starter Seti'nden gerekir:</span><span class="sxs-lookup"><span data-stu-id="b6ac6-121">To complete this operation, you need the following parts from your Feather HUZZAH ESP8266 Starter Kit:</span></span>

* <span data-ttu-id="b6ac6-122">Yumuşatma HUZZAH ESP8266 Panosu</span><span class="sxs-lookup"><span data-stu-id="b6ac6-122">The Feather HUZZAH ESP8266 board</span></span>
* <span data-ttu-id="b6ac6-123">Mikro USB tipi A USB kablosu</span><span class="sxs-lookup"><span data-stu-id="b6ac6-123">A Micro USB to Type A USB cable</span></span>

<span data-ttu-id="b6ac6-124">Ayrıca, geliştirme ortamınız için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="b6ac6-124">You also need the following things for your development environment:</span></span>

* <span data-ttu-id="b6ac6-125">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-125">An active Azure subscription.</span></span> <span data-ttu-id="b6ac6-126">Bir Azure hesabınız yoksa [ücretsiz Azure deneme hesabı oluşturma](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-126">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="b6ac6-127">Mac veya Windows veya Ubuntu çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-127">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="b6ac6-128">Yumuşatma HUZZAH ESP8266 bağlanmak için kablosuz ağ.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-128">Wireless network for Feather HUZZAH ESP8266 to connect to.</span></span>
* <span data-ttu-id="b6ac6-129">Yapılandırma Aracı indirmek için Internet bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-129">Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="b6ac6-130">[Arduino IDE](https://www.arduino.cc/en/main/software) sürüm 1.6.8 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-130">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="b6ac6-131">Önceki sürümlerde AzureIoT kitaplığı ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-131">Earlier versions don't work with the AzureIoT library.</span></span>

<span data-ttu-id="b6ac6-132">Algılayıcı olmayan olasılığına aşağıdaki öğeler isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-132">The following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="b6ac6-133">Ayrıca sanal algılayıcı verilerini kullanma seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-133">You also have the option of using simulated sensor data.</span></span>

* <span data-ttu-id="b6ac6-134">Adafruit DHT22 sıcaklık ve nem algılayıcısı</span><span class="sxs-lookup"><span data-stu-id="b6ac6-134">An Adafruit DHT22 temperature and humidity sensor</span></span>
* <span data-ttu-id="b6ac6-135">Bir breadboard</span><span class="sxs-lookup"><span data-stu-id="b6ac6-135">A breadboard</span></span>
* <span data-ttu-id="b6ac6-136">M/M anahtar kabloları</span><span class="sxs-lookup"><span data-stu-id="b6ac6-136">M/M jumper wires</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-the-sensor-and-your-computer"></a><span data-ttu-id="b6ac6-137">Algılayıcı ve bilgisayarınızla yumuşatma HUZZAH ESP8266 Bağlan</span><span class="sxs-lookup"><span data-stu-id="b6ac6-137">Connect Feather HUZZAH ESP8266 with the sensor and your computer</span></span>
<span data-ttu-id="b6ac6-138">Bu bölümde, algılayıcılar panonuz için bağlayın.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-138">In this section, you connect the sensors to your board.</span></span> <span data-ttu-id="b6ac6-139">Daha sonra Cihazınızı başka kullanmak için bilgisayarınıza takın.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-139">Then you plug in your device to your computer for further use.</span></span>
### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-feather-huzzah-esp8266"></a><span data-ttu-id="b6ac6-140">Yumuşatma HUZZAH ESP8266 DHT22 sıcaklık ve nem algılayıcı Bağlan</span><span class="sxs-lookup"><span data-stu-id="b6ac6-140">Connect a DHT22 temperature and humidity sensor to Feather HUZZAH ESP8266</span></span>

<span data-ttu-id="b6ac6-141">Şu şekilde bağlantı kurmayı breadboard ve anahtar kablolarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-141">Use the breadboard and jumper wires to make the connection as follows.</span></span> <span data-ttu-id="b6ac6-142">Algılayıcı yoksa, benzetimli algılayıcı verilerini yerine kullandığından bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-142">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Bağlantı Başvurusu](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


<span data-ttu-id="b6ac6-144">Algılayıcı PIN'ler için aşağıdaki kablolama kullanın:</span><span class="sxs-lookup"><span data-stu-id="b6ac6-144">For sensor pins, use the following wiring:</span></span>


| <span data-ttu-id="b6ac6-145">Başlangıç (algılayıcı)</span><span class="sxs-lookup"><span data-stu-id="b6ac6-145">Start (Sensor)</span></span>           | <span data-ttu-id="b6ac6-146">Bitiş (kartı)</span><span class="sxs-lookup"><span data-stu-id="b6ac6-146">End (Board)</span></span>           | <span data-ttu-id="b6ac6-147">Kablo rengi</span><span class="sxs-lookup"><span data-stu-id="b6ac6-147">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="b6ac6-148">VDD (PIN 31F)</span><span class="sxs-lookup"><span data-stu-id="b6ac6-148">VDD (Pin 31F)</span></span>            | <span data-ttu-id="b6ac6-149">3v (PIN 58H)</span><span class="sxs-lookup"><span data-stu-id="b6ac6-149">3V (Pin 58H)</span></span>           | <span data-ttu-id="b6ac6-150">Kırmızı kablosu</span><span class="sxs-lookup"><span data-stu-id="b6ac6-150">Red cable</span></span>     |
| <span data-ttu-id="b6ac6-151">Veri (PIN 32F)</span><span class="sxs-lookup"><span data-stu-id="b6ac6-151">DATA (Pin 32F)</span></span>           | <span data-ttu-id="b6ac6-152">GPIO'yu 2 (PIN 46A)</span><span class="sxs-lookup"><span data-stu-id="b6ac6-152">GPIO 2 (Pin 46A)</span></span>       | <span data-ttu-id="b6ac6-153">Mavi kablosu</span><span class="sxs-lookup"><span data-stu-id="b6ac6-153">Blue cable</span></span>    |
| <span data-ttu-id="b6ac6-154">GND (PIN 34F)</span><span class="sxs-lookup"><span data-stu-id="b6ac6-154">GND (Pin 34F)</span></span>            | <span data-ttu-id="b6ac6-155">GND (PIN 56I)</span><span class="sxs-lookup"><span data-stu-id="b6ac6-155">GND (PIn 56I)</span></span>          | <span data-ttu-id="b6ac6-156">Siyah kablosu</span><span class="sxs-lookup"><span data-stu-id="b6ac6-156">Black cable</span></span>   |

<span data-ttu-id="b6ac6-157">Daha fazla bilgi için bkz: [Adafruit DHT22 algılayıcı Kurulum](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) ve [Adafruit yumuşatma HUZZAH Esp8266 no'lu](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span><span class="sxs-lookup"><span data-stu-id="b6ac6-157">For more information, see [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) and [Adafruit Feather HUZZAH Esp8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span></span>



<span data-ttu-id="b6ac6-158">Şimdi yumuşatma Huzzah ESP8266 ile çalışma algılayıcı bağlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-158">Now your Feather Huzzah ESP8266 should be connected with a working sensor.</span></span>

![Yumuşatma Huzzah ile DHT22 Bağlan](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-to-your-computer"></a><span data-ttu-id="b6ac6-160">Yumuşatma HUZZAH ESP8266 bilgisayarınıza bağlayın</span><span class="sxs-lookup"><span data-stu-id="b6ac6-160">Connect Feather HUZZAH ESP8266 to your computer</span></span>

<span data-ttu-id="b6ac6-161">Sonraki gösterildiği gibi geçiş yumuşatma HUZZAH ESP8266 bilgisayarınıza bağlanmak için mikro USB tipi A USB kablosu kullanın.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-161">As shown next, use the Micro USB to Type A USB cable to connect Feather HUZZAH ESP8266 to your computer.</span></span>

![Yumuşatma Huzzah bilgisayarınıza bağlayın](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="b6ac6-163">Seri bağlantı noktası izinleri (yalnızca Ubuntu) ekleyin</span><span class="sxs-lookup"><span data-stu-id="b6ac6-163">Add serial port permissions (Ubuntu only)</span></span>


<span data-ttu-id="b6ac6-164">Ubuntu kullanırsanız, USB bağlantı noktası, yumuşatma HUZZAH ESP8266 üzerinde çalışması için izinlere sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-164">If you use Ubuntu, make sure you have the permissions to operate on the USB port of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="b6ac6-165">Seri bağlantı noktası izinleri eklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="b6ac6-165">To add serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="b6ac6-166">Terminal aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b6ac6-166">Run the following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="b6ac6-167">Aşağıdaki çıktıları birini alın:</span><span class="sxs-lookup"><span data-stu-id="b6ac6-167">You get one of the following outputs:</span></span>

   * <span data-ttu-id="b6ac6-168">crw-rw---1 kök uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="b6ac6-168">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="b6ac6-169">crw-rw---1 kök araması xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="b6ac6-169">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="b6ac6-170">Çıktıda dikkat `uucp` veya `dialout` USB bağlantı noktasına Grup sahibi adıdır.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-170">In the output, notice that `uucp` or `dialout` is the group owner name of the USB port.</span></span>

1. <span data-ttu-id="b6ac6-171">Kullanıcı, aşağıdaki komutu çalıştırarak gruba ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b6ac6-171">Add the user to the group by running the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="b6ac6-172">`<group-owner-name>`Önceki adımda elde ettiğiniz Grup sahibi adıdır.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-172">`<group-owner-name>` is the group owner name you obtained in the previous step.</span></span> <span data-ttu-id="b6ac6-173">`<username>`Ubuntu kullanıcı adınızdır.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-173">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="b6ac6-174">Ubuntu dışında oturum ve yeniden değişiklik görünmesi oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-174">Sign out of Ubuntu, and then sign in again for the change to appear.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="b6ac6-175">Algılayıcı verilerini toplamak ve IOT hub'ınıza gönderin</span><span class="sxs-lookup"><span data-stu-id="b6ac6-175">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="b6ac6-176">Bu bölümde, dağıtın ve yumuşatma HUZZAH ESP8266 üzerinde bir örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-176">In this section, you deploy and run a sample application on Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="b6ac6-177">Örnek uygulama LED yumuşatma HUZZAH ESP8266 üzerinde yanıp ve IOT hub'ınıza DHT22 algılayıcı toplanan sıcaklık ve nem verileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-177">The sample application blinks the LED on Feather HUZZAH ESP8266, and sends the temperature and humidity data collected from the DHT22 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github"></a><span data-ttu-id="b6ac6-178">Örnek uygulama Github'dan alma</span><span class="sxs-lookup"><span data-stu-id="b6ac6-178">Get the sample application from GitHub</span></span>

<span data-ttu-id="b6ac6-179">Örnek uygulama, GitHub üzerinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-179">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="b6ac6-180">Github'dan örnek uygulamayı içeren örnek depoyu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-180">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="b6ac6-181">Örnek deposuna kopyalamak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="b6ac6-181">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="b6ac6-182">Bir komut istemi veya terminal penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-182">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="b6ac6-183">Depolanması için örnek uygulama istediğiniz bir klasöre gidin.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-183">Go to a folder where you want the sample application to be stored.</span></span>
1. <span data-ttu-id="b6ac6-184">Şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b6ac6-184">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

<span data-ttu-id="b6ac6-185">Yumuşatma HUZZAH ESP8266 Arduino IDE'de paketi yükle:</span><span class="sxs-lookup"><span data-stu-id="b6ac6-185">Install the package for Feather HUZZAH ESP8266 in the Arduino IDE:</span></span>

1. <span data-ttu-id="b6ac6-186">Örnek uygulama depolandığı klasörü açın.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-186">Open the folder where the sample application is stored.</span></span>
1. <span data-ttu-id="b6ac6-187">Arduino IDE uygulama klasöründe app.ino dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-187">Open the app.ino file in the app folder in the Arduino IDE.</span></span>

   ![Örnek uygulamayı Arduino IDE içinde Aç](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="b6ac6-189">Arduino IDE'de tıklatın **dosya** > **Tercihler**.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-189">In the Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="b6ac6-190">İçinde **Tercihler** iletişim kutusunda, simgesine tıklayın **ek panoları yöneticisi URL'leri** kutusu.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-190">In the **Preferences** dialog box, click the icon next to the **Additional Boards Manager URLs** box.</span></span>
1. <span data-ttu-id="b6ac6-191">Açılan pencerede aşağıdaki URL'yi girin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-191">In the pop-up window, enter the following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Paket URL'sini Arduino IDE'de işaret](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="b6ac6-193">İçinde **tercih** iletişim kutusu, tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-193">In the **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="b6ac6-194">Tıklatın **Araçları** > **Panosu** > **panoları Yöneticisi**ve esp8266 için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-194">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>

   <span data-ttu-id="b6ac6-195">Panoları Yöneticisi ESP8266 2.2.0 veya sonraki bir sürümü ile yüklü olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-195">Boards Manager indicates that ESP8266 with a version of 2.2.0 or later is installed.</span></span>

   ![esp8266 paketi yüklü](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="b6ac6-197">Tıklatın **Araçları** > **Panosu** > **Adafruit HUZZAH ESP8266**.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-197">Click **Tools** > **Board** > **Adafruit HUZZAH ESP8266**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="b6ac6-198">Gerekli kitaplıkları yükleme</span><span class="sxs-lookup"><span data-stu-id="b6ac6-198">Install necessary libraries</span></span>

1. <span data-ttu-id="b6ac6-199">Arduino IDE'de tıklatın **taslak** > **dahil Kitaplığı** > **yönetmek kitaplıkları**.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-199">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="b6ac6-200">Aşağıdaki Kitaplığı Ara tek tek adları.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-200">Search for the following library names one by one.</span></span> <span data-ttu-id="b6ac6-201">Bulduğunuz her kitaplığını tıklatın **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-201">For each  library that you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="b6ac6-202">Gerçek DHT22 algılayıcı yok mu?</span><span class="sxs-lookup"><span data-stu-id="b6ac6-202">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="b6ac6-203">Örnek uygulama, gerçek DHT22 algılayıcı olmayan olasılığına sıcaklık ve nem veri benzetimini yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-203">The sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="b6ac6-204">Örnek uygulamayı benzetimli veri kullanacak şekilde ayarlamak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="b6ac6-204">To set up the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="b6ac6-205">Açık `config.h` dosyasını `app` klasör.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-205">Open the `config.h` file in the `app` folder.</span></span>
1. <span data-ttu-id="b6ac6-206">Aşağıdaki kod satırını bulun ve değeri değiştirin `false` için `true`:</span><span class="sxs-lookup"><span data-stu-id="b6ac6-206">Locate the following line of code and change the value from `false` to `true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Örnek uygulamayı benzetimli veri kullanacak şekilde yapılandırma](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. <span data-ttu-id="b6ac6-208">Dosyayı kaydetmek `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-208">Save the file with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-feather-huzzah-esp8266"></a><span data-ttu-id="b6ac6-209">Yumuşatma HUZZAH ESP8266 örnek uygulamayı dağıtmak</span><span class="sxs-lookup"><span data-stu-id="b6ac6-209">Deploy the sample application to Feather HUZZAH ESP8266</span></span>

1. <span data-ttu-id="b6ac6-210">Arduino IDE'de tıklatın **aracı** > **bağlantı noktası**, yumuşatma HUZZAH ESP8266 için seri bağlantı noktası'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-210">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Feather HUZZAH ESP8266.</span></span>
1. <span data-ttu-id="b6ac6-211">' I tıklatın **taslak** > **karşıya** oluşturup yumuşatma HUZZAH ESP8266 örnek uygulamayı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-211">Click **Sketch** > **Upload** to build and deploy the sample application to Feather HUZZAH ESP8266.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="b6ac6-212">Kimlik bilgilerinizi girin</span><span class="sxs-lookup"><span data-stu-id="b6ac6-212">Enter your credentials</span></span>

<span data-ttu-id="b6ac6-213">Karşıya yükleme başarıyla tamamlandıktan sonra kimlik bilgilerinizi girmeniz için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="b6ac6-213">After the upload completes successfully, follow these steps to enter your credentials:</span></span>

1. <span data-ttu-id="b6ac6-214">Arduino IDE'de tıklatın **Araçları** > **seri İzleyici**.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-214">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="b6ac6-215">Seri İzleyicisi penceresinde sağ alt köşedeki iki açılan listelerde dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-215">In the serial monitor window, notice the two drop-down lists in the lower-right corner.</span></span>
1. <span data-ttu-id="b6ac6-216">Seçin **hiçbir satır bitiş** sol aşağı açılan listesi.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-216">Select **No line ending** for the left drop-down list.</span></span>
1. <span data-ttu-id="b6ac6-217">Seçin **115200 baud** sağda açılan listesi.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-217">Select **115200 baud** for the right drop-down list.</span></span>
1. <span data-ttu-id="b6ac6-218">Bunları sağlayın ve ardından sorulursa seri İzleyici penceresinin en üstünde bulunan giriş kutusuna aşağıdaki bilgileri girin **Gönder**.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-218">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span></span>
   * <span data-ttu-id="b6ac6-219">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="b6ac6-219">Wi-Fi SSID</span></span>
   * <span data-ttu-id="b6ac6-220">Wi-Fi parola</span><span class="sxs-lookup"><span data-stu-id="b6ac6-220">Wi-Fi password</span></span>
   * <span data-ttu-id="b6ac6-221">Cihaz bağlantı dizesi</span><span class="sxs-lookup"><span data-stu-id="b6ac6-221">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="b6ac6-222">Kimlik bilgisi EEPROM, yumuşatma HUZZAH ESP8266 içinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-222">The credential information is stored in the EEPROM of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="b6ac6-223">Yumuşatma HUZZAH ESP8266 panosunda Sıfırla düğmesini tıklatın, örnek uygulamayı bilgileri silmek isteyip istemediğinizi sorar.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-223">If you click the reset button on the Feather HUZZAH ESP8266 board, the sample application asks if you want to erase the information.</span></span> <span data-ttu-id="b6ac6-224">Girin `Y` silinmesi bilgilere sahip olması.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-224">Enter `Y` to have the information erased.</span></span> <span data-ttu-id="b6ac6-225">İkinci kez bilgileri vermeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-225">You are asked to provide the information a second time.</span></span>

### <a name="verify-the-sample-application-is-running-successfully"></a><span data-ttu-id="b6ac6-226">Örnek Uygulama başarıyla çalıştığını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="b6ac6-226">Verify the sample application is running successfully</span></span>

<span data-ttu-id="b6ac6-227">Yumuşatma HUZZAH ESP8266 üzerinde seri İzleyici penceresinin ve yanıp sönen LED aşağıdaki çıkışı görürseniz, örnek uygulamayı başarılı bir şekilde çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-227">If you see the following output from the serial monitor window and the blinking LED on Feather HUZZAH ESP8266, the sample application is running successfully.</span></span>

![Arduino IDE içinde son çıktı](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="b6ac6-229">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b6ac6-229">Next steps</span></span>

<span data-ttu-id="b6ac6-230">Başarıyla yumuşatma HUZZAH ESP8266 IOT hub'ına bağlı ve yakalanan algılayıcı verilerini IOT hub'ına gönderilen.</span><span class="sxs-lookup"><span data-stu-id="b6ac6-230">You have successfully connected a Feather HUZZAH ESP8266 to your IoT hub, and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

