---
title: "Bulut için - Sparkfun ESP8266 şey geliştirme bağlanmak Azure IOT Hub'ına ESP8266 | Microsoft Docs"
description: "Kurulum ve Bu öğreticide Azure bulut platformuna veri göndermek için Azure IOT Hub için bu Sparkfun ESP8266 şey geliştirme bağlanma hakkında bilgi edinin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 587fe292-9602-45b4-95ee-f39bba10e716
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 557f0cdf375b345e0dbe0526f5a5bd3c050dec38
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="37ae2-103">Bulutta Azure IOT Hub'ına Sparkfun ESP8266 şey geliştirme Bağlan</span><span class="sxs-lookup"><span data-stu-id="37ae2-103">Connect Sparkfun ESP8266 Thing Dev to Azure IoT Hub in the cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![DHT22, şey geliştirme ve IOT hub'ı arasında bir bağlantı](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a><span data-ttu-id="37ae2-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="37ae2-105">What you will do</span></span>

<span data-ttu-id="37ae2-106">Sparkfun ESP8266 şey geliştirme oluşturacağınız bir IOT hub'ınıza bağlanın.</span><span class="sxs-lookup"><span data-stu-id="37ae2-106">Connect Sparkfun ESP8266 Thing Dev to an IoT hub you will create.</span></span> <span data-ttu-id="37ae2-107">Ardından örnek bir uygulama DHT22 algılayıcı sıcaklık ve nem verileri toplamak için ESP8266 çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="37ae2-107">Then run a sample application on ESP8266 to collect temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="37ae2-108">Son olarak, algılayıcı verilerini IOT hub'ınıza gönderir.</span><span class="sxs-lookup"><span data-stu-id="37ae2-108">Finally, send the sensor data to your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="37ae2-109">Diğer ESP8266 panoları kullanıyorsanız, yine IOT hub'ınıza bağlanmak için aşağıdaki adımları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37ae2-109">If you are using other ESP8266 boards, you can still follow these steps to connect it to your IoT hub.</span></span> <span data-ttu-id="37ae2-110">Kullanmakta olduğunuz ESP8266 Panosu bağlı olarak, yeniden yapılandırmanız gerekebilir `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="37ae2-110">Depending on the ESP8266 board you are using, you may need to reconfigure the `LED_PIN`.</span></span> <span data-ttu-id="37ae2-111">AI Thinker gelen ESP8266 kullanıyorsanız, örneğin, ondan değişebilir `0` için `2`.</span><span class="sxs-lookup"><span data-stu-id="37ae2-111">For example, if you are using ESP8266 from AI-Thinker, you may change it from `0` to `2`.</span></span> <span data-ttu-id="37ae2-112">Bir pakete henüz yok mu?: tıklatın [burada](http://azure.com/iotstarterkits)</span><span class="sxs-lookup"><span data-stu-id="37ae2-112">Don't have a kit yet?: Click [here](http://azure.com/iotstarterkits)</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="37ae2-113">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="37ae2-113">What you will learn</span></span>

* <span data-ttu-id="37ae2-114">IOT hub'ı oluşturma ve şey istisnası için bir cihaz kaydetme</span><span class="sxs-lookup"><span data-stu-id="37ae2-114">How to create an IoT hub and register a device for Thing Dev.</span></span>
* <span data-ttu-id="37ae2-115">Şey geliştirme algılayıcı ve bilgisayarınızla bağlanma.</span><span class="sxs-lookup"><span data-stu-id="37ae2-115">How to connect Thing Dev with the sensor and your computer.</span></span>
* <span data-ttu-id="37ae2-116">Örnek bir uygulama üzerinde şey istisnası çalıştırarak algılayıcı verilerini toplamak nasıl</span><span class="sxs-lookup"><span data-stu-id="37ae2-116">How to collect sensor data by running a sample application on Thing Dev.</span></span>
* <span data-ttu-id="37ae2-117">IOT hub'ınıza algılayıcı verileri göndermek nasıl.</span><span class="sxs-lookup"><span data-stu-id="37ae2-117">How to send the sensor data to your IoT hub.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="37ae2-118">İhtiyacınız olacak</span><span class="sxs-lookup"><span data-stu-id="37ae2-118">What you will need</span></span>

![Öğretici için gerekli bölümleri](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="37ae2-120">Bu işlemi tamamlamak için aşağıdaki bölümleri şey geliştirme Starter Seti'nden gerekir:</span><span class="sxs-lookup"><span data-stu-id="37ae2-120">To complete this operation, you need the following parts from your Thing Dev Starter Kit:</span></span>

* <span data-ttu-id="37ae2-121">Sparkfun ESP8266 şey geliştirme Panosu.</span><span class="sxs-lookup"><span data-stu-id="37ae2-121">The Sparkfun ESP8266 Thing Dev board.</span></span>
* <span data-ttu-id="37ae2-122">Mikro USB tipi A USB kablosu.</span><span class="sxs-lookup"><span data-stu-id="37ae2-122">A Micro USB to Type A USB cable.</span></span>

<span data-ttu-id="37ae2-123">Ayrıca geliştirme ortamınız için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="37ae2-123">You also need the following for your development environment:</span></span>

* <span data-ttu-id="37ae2-124">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="37ae2-124">An active Azure subscription.</span></span> <span data-ttu-id="37ae2-125">Bir Azure hesabınız yoksa [ücretsiz Azure deneme hesabı oluşturma](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="37ae2-125">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="37ae2-126">Mac veya Windows veya Ubuntu çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="37ae2-126">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="37ae2-127">Kablosuz ağ bağlanmak Sparkfun ESP8266 şey geliştirme için.</span><span class="sxs-lookup"><span data-stu-id="37ae2-127">Wireless network for Sparkfun ESP8266 Thing Dev to connect to.</span></span>
* <span data-ttu-id="37ae2-128">Yapılandırma Aracı indirmek için Internet bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="37ae2-128">Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="37ae2-129">[Arduino IDE](https://www.arduino.cc/en/main/software) sürüm 1.6.8 (veya daha yeni), önceki sürümleri AzureIoT kitaplığı ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="37ae2-129">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 (or newer), earlier versions will not work with the AzureIoT library.</span></span>

<span data-ttu-id="37ae2-130">Algılayıcı olmayan olasılığına aşağıdaki öğeler isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="37ae2-130">The following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="37ae2-131">Ayrıca sanal algılayıcı verilerini kullanma seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="37ae2-131">You also have the option of using simulated sensor data.</span></span>

* <span data-ttu-id="37ae2-132">Bir Adafruit DHT22 sıcaklık ve nem algılayıcı.</span><span class="sxs-lookup"><span data-stu-id="37ae2-132">An Adafruit DHT22 temperature and humidity sensor.</span></span>
* <span data-ttu-id="37ae2-133">Bir breadboard.</span><span class="sxs-lookup"><span data-stu-id="37ae2-133">A breadboard.</span></span>
* <span data-ttu-id="37ae2-134">M/M anahtar kablolarını.</span><span class="sxs-lookup"><span data-stu-id="37ae2-134">M/M jumper wires.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-the-sensor-and-your-computer"></a><span data-ttu-id="37ae2-135">Algılayıcı ve bilgisayarınızla ESP8266 şey geliştirme Bağlan</span><span class="sxs-lookup"><span data-stu-id="37ae2-135">Connect ESP8266 Thing Dev with the sensor and your computer</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-esp8266-thing-dev"></a><span data-ttu-id="37ae2-136">ESP8266 şey geliştirme DHT22 sıcaklık ve nem algılayıcı Bağlan</span><span class="sxs-lookup"><span data-stu-id="37ae2-136">Connect a DHT22 temperature and humidity sensor to ESP8266 Thing Dev</span></span>

<span data-ttu-id="37ae2-137">Şu şekilde bağlantı kurmayı breadboard ve anahtar kablolarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="37ae2-137">Use the breadboard and jumper wires to make the connection as follows.</span></span> <span data-ttu-id="37ae2-138">Algılayıcı yoksa, benzetimli algılayıcı verilerini yerine kullandığından bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37ae2-138">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Bağlantı Başvurusu](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

<span data-ttu-id="37ae2-140">Aşağıdaki kablolama algılayıcı PIN'ler için kullanırız:</span><span class="sxs-lookup"><span data-stu-id="37ae2-140">For sensor pins, we will use the following wiring:</span></span>

| <span data-ttu-id="37ae2-141">Başlangıç (algılayıcı)</span><span class="sxs-lookup"><span data-stu-id="37ae2-141">Start (Sensor)</span></span>           | <span data-ttu-id="37ae2-142">Bitiş (kartı)</span><span class="sxs-lookup"><span data-stu-id="37ae2-142">End (Board)</span></span>           | <span data-ttu-id="37ae2-143">Kablo rengi</span><span class="sxs-lookup"><span data-stu-id="37ae2-143">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="37ae2-144">VDD (PIN 27F)</span><span class="sxs-lookup"><span data-stu-id="37ae2-144">VDD (Pin 27F)</span></span>            | <span data-ttu-id="37ae2-145">3v (PIN 8A)</span><span class="sxs-lookup"><span data-stu-id="37ae2-145">3V (Pin 8A)</span></span>           | <span data-ttu-id="37ae2-146">Kırmızı kablosu</span><span class="sxs-lookup"><span data-stu-id="37ae2-146">Red cable</span></span>     |
| <span data-ttu-id="37ae2-147">Veri (PIN 28F)</span><span class="sxs-lookup"><span data-stu-id="37ae2-147">DATA (Pin 28F)</span></span>           | <span data-ttu-id="37ae2-148">GPIO'yu 2 (PIN 9A)</span><span class="sxs-lookup"><span data-stu-id="37ae2-148">GPIO 2 (Pin 9A)</span></span>       | <span data-ttu-id="37ae2-149">Beyaz kablosu</span><span class="sxs-lookup"><span data-stu-id="37ae2-149">White cable</span></span>    |
| <span data-ttu-id="37ae2-150">GND (PIN 30F)</span><span class="sxs-lookup"><span data-stu-id="37ae2-150">GND (Pin 30F)</span></span>            | <span data-ttu-id="37ae2-151">GND (PIN 7J)</span><span class="sxs-lookup"><span data-stu-id="37ae2-151">GND (Pin 7J)</span></span>          | <span data-ttu-id="37ae2-152">Siyah kablosu</span><span class="sxs-lookup"><span data-stu-id="37ae2-152">Black cable</span></span>   |


- <span data-ttu-id="37ae2-153">Daha fazla bilgi için bkz: [DHT22 algılayıcı Kurulum](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) ve [Sparkfun ESP8266 şey geliştirme belirtimi](https://www.sparkfun.com/products/13711)</span><span class="sxs-lookup"><span data-stu-id="37ae2-153">For more information, see: [DHT22 sensor setup](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) and [Sparkfun ESP8266 Thing Dev specification](https://www.sparkfun.com/products/13711)</span></span>

<span data-ttu-id="37ae2-154">Şimdi, Sparkfun ESP8266 şey geliştirme ile çalışma algılayıcı bağlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="37ae2-154">Now your Sparkfun ESP8266 Thing Dev should be connected with a working sensor.</span></span>

![dht22 ESP8266 şey geliştirme ile bağlanma](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-to-your-computer"></a><span data-ttu-id="37ae2-156">Sparkfun ESP8266 şey geliştirme bilgisayarınıza bağlayın</span><span class="sxs-lookup"><span data-stu-id="37ae2-156">Connect Sparkfun ESP8266 Thing Dev to your computer</span></span>

<span data-ttu-id="37ae2-157">Sparkfun ESP8266 şey geliştirme bilgisayarınıza şu şekilde bağlanmak için mikro USB tipi A USB kablosu kullanın.</span><span class="sxs-lookup"><span data-stu-id="37ae2-157">Use the Micro USB to Type A USB cable to connect Sparkfun ESP8266 Thing Dev to your computer as follows.</span></span>

![yumuşatma huzzah bilgisayarınıza bağlayın](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a><span data-ttu-id="37ae2-159">Seri bağlantı noktası izinleri – yalnızca Ubuntu ekleyin</span><span class="sxs-lookup"><span data-stu-id="37ae2-159">Add serial port permissions – Ubuntu only</span></span>

<span data-ttu-id="37ae2-160">Ubuntu kullanıyorsanız, normal bir kullanıcı USB bağlantı noktası, Sparkfun ESP8266 şey istisnası üzerinde çalışması için izinlere sahip olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="37ae2-160">If you use Ubuntu, make sure a normal user has the permissions to operate on the USB port of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="37ae2-161">Normal bir kullanıcı için seri bağlantı noktası izinleri eklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="37ae2-161">To add serial port permissions for a normal user, follow these steps:</span></span>

1. <span data-ttu-id="37ae2-162">Terminal aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="37ae2-162">Run the following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="37ae2-163">Aşağıdaki çıktıları birini alın:</span><span class="sxs-lookup"><span data-stu-id="37ae2-163">You get one of the following outputs:</span></span>

   * <span data-ttu-id="37ae2-164">crw-rw---1 kök uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="37ae2-164">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="37ae2-165">crw-rw---1 kök araması xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="37ae2-165">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="37ae2-166">Çıktıda fark `uucp` veya `dialout` diğer bir deyişle USB bağlantı noktasına Grup sahibi adı.</span><span class="sxs-lookup"><span data-stu-id="37ae2-166">In the output, notice `uucp` or `dialout` that is the group owner name of the USB port.</span></span>

1. <span data-ttu-id="37ae2-167">Kullanıcı, aşağıdaki komutu çalıştırarak gruba ekleyin:</span><span class="sxs-lookup"><span data-stu-id="37ae2-167">Add the user to the group by running the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="37ae2-168">`<group-owner-name>`Önceki adımda elde ettiğiniz Grup sahibi adıdır.</span><span class="sxs-lookup"><span data-stu-id="37ae2-168">`<group-owner-name>` is the group owner name you obtained in the previous step.</span></span> <span data-ttu-id="37ae2-169">`<username>`Ubuntu kullanıcı adınızdır.</span><span class="sxs-lookup"><span data-stu-id="37ae2-169">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="37ae2-170">Ubuntu ve değişikliğin etkili olması için yeniden için içindeki oturum.</span><span class="sxs-lookup"><span data-stu-id="37ae2-170">Log out Ubuntu and log in it again for the change to take effect.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="37ae2-171">Algılayıcı verilerini toplamak ve IOT hub'ınıza gönderin</span><span class="sxs-lookup"><span data-stu-id="37ae2-171">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="37ae2-172">Bu bölümde, dağıtma ve Sparkfun ESP8266 şey istisnası üzerinde örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="37ae2-172">In this section, you deploy and run a sample application on Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="37ae2-173">Örnek uygulama LED Sparkfun ESP8266 şey geliştirme üzerinde yanıp ve IOT hub'ınıza DHT22 algılayıcı toplanan sıcaklık ve nem verileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="37ae2-173">The sample application blinks the LED on Sparkfun ESP8266 Thing Dev and sends the temperature and humidity data collected from the DHT22 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github"></a><span data-ttu-id="37ae2-174">Örnek uygulama Github'dan alma</span><span class="sxs-lookup"><span data-stu-id="37ae2-174">Get the sample application from GitHub</span></span>

<span data-ttu-id="37ae2-175">Örnek uygulama, GitHub üzerinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="37ae2-175">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="37ae2-176">Github'dan örnek uygulamayı içeren örnek depoyu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="37ae2-176">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="37ae2-177">Örnek deposuna kopyalamak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="37ae2-177">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="37ae2-178">Bir komut istemi veya terminal penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="37ae2-178">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="37ae2-179">Depolanması için örnek uygulama istediğiniz bir klasöre gidin.</span><span class="sxs-lookup"><span data-stu-id="37ae2-179">Go to a folder where you want the sample application to be stored.</span></span>
1. <span data-ttu-id="37ae2-180">Şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="37ae2-180">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

<span data-ttu-id="37ae2-181">Paket Sparkfun ESP8266 şey geliştirme Arduino IDE'de yükle:</span><span class="sxs-lookup"><span data-stu-id="37ae2-181">Install the package for Sparkfun ESP8266 Thing Dev in Arduino IDE:</span></span>

1. <span data-ttu-id="37ae2-182">Örnek uygulama depolandığı klasörü açın.</span><span class="sxs-lookup"><span data-stu-id="37ae2-182">Open the folder where the sample application is stored.</span></span>
1. <span data-ttu-id="37ae2-183">Arduino IDE uygulama klasöründe app.ino dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="37ae2-183">Open the app.ino file in the app folder in Arduino IDE.</span></span>

   ![Örnek uygulamayı arduino IDE içinde Aç](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="37ae2-185">Arduino IDE'de tıklatın **dosya** > **Tercihler**.</span><span class="sxs-lookup"><span data-stu-id="37ae2-185">In the Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="37ae2-186">İçinde **Tercihler** iletişim kutusunda, simgesine tıklayın **ek panoları yöneticisi URL'leri** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="37ae2-186">In the **Preferences** dialog box, click the icon next to the **Additional Boards Manager URLs** text box.</span></span>
1. <span data-ttu-id="37ae2-187">Açılan pencerede aşağıdaki URL'yi girin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="37ae2-187">In the pop-up window, enter the following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Paket URL'sini arduino IDE'de işaret](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="37ae2-189">İçinde **tercih** iletişim kutusu, tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="37ae2-189">In the **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="37ae2-190">Tıklatın **Araçları** > **Panosu** > **panoları Yöneticisi**ve esp8266 için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="37ae2-190">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>
   <span data-ttu-id="37ae2-191">ESP8266 2.2.0 veya sonraki bir sürümüyle yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="37ae2-191">ESP8266 with a version of 2.2.0 or later should be installed.</span></span>

   ![esp8266 paketi yüklü](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="37ae2-193">Tıklatın **Araçları** > **Panosu** > **Sparkfun ESP8266 şey geliştirme**.</span><span class="sxs-lookup"><span data-stu-id="37ae2-193">Click **Tools** > **Board** > **Sparkfun ESP8266 Thing Dev**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="37ae2-194">Gerekli kitaplıkları yükleme</span><span class="sxs-lookup"><span data-stu-id="37ae2-194">Install necessary libraries</span></span>

1. <span data-ttu-id="37ae2-195">Arduino IDE'de tıklatın **taslak** > **dahil Kitaplığı** > **yönetmek kitaplıkları**.</span><span class="sxs-lookup"><span data-stu-id="37ae2-195">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="37ae2-196">Aşağıdaki Kitaplığı Ara tek tek adları.</span><span class="sxs-lookup"><span data-stu-id="37ae2-196">Search for the following library names one by one.</span></span> <span data-ttu-id="37ae2-197">Her bulduğunuz kitaplığının tıklatın **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="37ae2-197">For each of the library you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="37ae2-198">Gerçek DHT22 algılayıcı yok mu?</span><span class="sxs-lookup"><span data-stu-id="37ae2-198">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="37ae2-199">Örnek uygulama, gerçek DHT22 algılayıcı olmayan olasılığına sıcaklık ve nem veri benzetimini yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37ae2-199">The sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="37ae2-200">Örnek uygulamayı benzetimli veri kullanacak şekilde etkinleştirmek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="37ae2-200">To enable the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="37ae2-201">Açık `config.h` dosyasını `app` klasör.</span><span class="sxs-lookup"><span data-stu-id="37ae2-201">Open the `config.h` file in the `app` folder.</span></span>
1. <span data-ttu-id="37ae2-202">Aşağıdaki kod satırını bulun ve değeri değiştirin `false` için `true`:</span><span class="sxs-lookup"><span data-stu-id="37ae2-202">Locate the following line of code and change the value from `false` to `true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Örnek uygulamayı benzetimli veri kullanacak şekilde yapılandırma](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. <span data-ttu-id="37ae2-204">İle Kaydet `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="37ae2-204">Save with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-sparkfun-esp8266-thing-dev"></a><span data-ttu-id="37ae2-205">Sparkfun ESP8266 şey geliştirme için örnek uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="37ae2-205">Deploy the sample application to Sparkfun ESP8266 Thing Dev</span></span>

1. <span data-ttu-id="37ae2-206">Arduino IDE'de tıklatın **aracı** > **bağlantı noktası**ve ardından seri bağlantı noktası Sparkfun ESP8266 şey istisnası için tıklayın</span><span class="sxs-lookup"><span data-stu-id="37ae2-206">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Sparkfun ESP8266 Thing Dev.</span></span>
1. <span data-ttu-id="37ae2-207">Tıklatın **taslak** > **karşıya** oluşturmak ve Sparkfun ESP8266 şey istisnası örnek uygulamayı dağıtmak için</span><span class="sxs-lookup"><span data-stu-id="37ae2-207">Click **Sketch** > **Upload** to build and deploy the sample application to Sparkfun ESP8266 Thing Dev.</span></span>

> [!Note]
> <span data-ttu-id="37ae2-208">MacOS kullanıyorsanız büyük olasılıkla karşıya yükleme sırasında aşağıdaki iletileri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37ae2-208">If you are using macOS you could probably see the following messages during uploading.</span></span> <span data-ttu-id="37ae2-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span><span class="sxs-lookup"><span data-stu-id="37ae2-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span></span> <span data-ttu-id="37ae2-210">Lütfen ternimal penceresini açın ve bu sorunu çözmek için eylemleri tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="37ae2-210">Please open your ternimal window and finish below actions to solve this issue.</span></span>
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a><span data-ttu-id="37ae2-211">Kimlik bilgilerinizi girin</span><span class="sxs-lookup"><span data-stu-id="37ae2-211">Enter your credentials</span></span>

<span data-ttu-id="37ae2-212">Karşıya yükleme başarıyla tamamlandıktan sonra kimlik bilgilerinizi girmeniz için adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="37ae2-212">After the upload completes successfully, follow the steps to enter your credentials:</span></span>

1. <span data-ttu-id="37ae2-213">Arduino IDE'de tıklatın **Araçları** > **seri İzleyici**.</span><span class="sxs-lookup"><span data-stu-id="37ae2-213">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="37ae2-214">Seri İzleyicisi penceresinde sağ alt köşesindeki iki açılan listelerde dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="37ae2-214">In the serial monitor window, notice the two drop-down lists on the bottom right corner.</span></span>
1. <span data-ttu-id="37ae2-215">Seçin **hiçbir satır bitiş** sol aşağı açılan listesi.</span><span class="sxs-lookup"><span data-stu-id="37ae2-215">Select **No line ending** for the left drop-down list.</span></span>
1. <span data-ttu-id="37ae2-216">Seçin **115200 baud** sağda açılan listesi.</span><span class="sxs-lookup"><span data-stu-id="37ae2-216">Select **115200 baud** for the right drop-down list.</span></span>
1. <span data-ttu-id="37ae2-217">Bunları sağlayın ve ardından sorulursa seri İzleyici penceresinin en üstünde bulunan giriş kutusuna aşağıdaki bilgileri girin **Gönder**.</span><span class="sxs-lookup"><span data-stu-id="37ae2-217">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span></span>
   * <span data-ttu-id="37ae2-218">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="37ae2-218">Wi-Fi SSID</span></span>
   * <span data-ttu-id="37ae2-219">Wi-Fi parola</span><span class="sxs-lookup"><span data-stu-id="37ae2-219">Wi-Fi password</span></span>
   * <span data-ttu-id="37ae2-220">Cihaz bağlantı dizesi</span><span class="sxs-lookup"><span data-stu-id="37ae2-220">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="37ae2-221">Kimlik bilgisi EEPROM, Sparkfun ESP8266 şey istisnası içinde depolanır</span><span class="sxs-lookup"><span data-stu-id="37ae2-221">The credential information is stored in the EEPROM of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="37ae2-222">Sparkfun ESP8266 şey geliştirme panosunda Sıfırla düğmesini tıklatın, örnek uygulamayı bilgileri silmek isteyip istemediğinizi sorar.</span><span class="sxs-lookup"><span data-stu-id="37ae2-222">If you click the reset button on the Sparkfun ESP8266 Thing Dev board, the sample application asks you if you want to erase the information.</span></span> <span data-ttu-id="37ae2-223">Girin `Y` sahip silinmesi bilgi ve bilgileri tekrar sağlamanız istenir.</span><span class="sxs-lookup"><span data-stu-id="37ae2-223">Enter `Y` to have the information erased and you are asked to provide the information again.</span></span>

### <a name="verify-the-sample-application-is-running-successfully"></a><span data-ttu-id="37ae2-224">Örnek Uygulama başarıyla çalıştığını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="37ae2-224">Verify the sample application is running successfully</span></span>

<span data-ttu-id="37ae2-225">Seri İzleyici penceresinin ve yanıp sönen LED aşağıdaki çıkışı Sparkfun ESP8266 şey geliştirme üzerinde görürseniz, örnek uygulamayı başarılı bir şekilde çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="37ae2-225">If you see the following output from the serial monitor window and the blinking LED on Sparkfun ESP8266 Thing Dev, the sample application is running successfully.</span></span>

![arduino IDE içinde son çıktı](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="37ae2-227">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="37ae2-227">Next steps</span></span>

<span data-ttu-id="37ae2-228">Başarıyla Sparkfun ESP8266 şey geliştirme IOT hub'ına bağlı ve IOT hub'ınıza yakalanan algılayıcı verilerini gönderilir.</span><span class="sxs-lookup"><span data-stu-id="37ae2-228">You have successfully connected a Sparkfun ESP8266 Thing Dev to your IoT hub and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
