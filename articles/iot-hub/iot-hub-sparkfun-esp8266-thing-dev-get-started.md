---
title: "aaaESP8266 toocloud - Sparkfun ESP8266 şey geliştirme bağlanmak tooAzure IOT hub'ı | Microsoft Docs"
description: "Bilgi nasıl toosetup ve onun için Sparkfun ESP8266 şey geliştirme tooAzure IOT hub'ı Bu öğreticide toosend veri toohello Azure bulut platformu bağlanın."
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
ms.openlocfilehash: 19b249df23b6df516634853521c6d532f51014da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="57252-103">Sparkfun ESP8266 şey geliştirme tooAzure IOT Hub'hello bulutta Bağlan</span><span class="sxs-lookup"><span data-stu-id="57252-103">Connect Sparkfun ESP8266 Thing Dev tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![DHT22, şey geliştirme ve IOT hub'ı arasında bir bağlantı](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a><span data-ttu-id="57252-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="57252-105">What you will do</span></span>

<span data-ttu-id="57252-106">Oluşturacağınız Sparkfun ESP8266 şey geliştirme tooan IOT hub bağlayın.</span><span class="sxs-lookup"><span data-stu-id="57252-106">Connect Sparkfun ESP8266 Thing Dev tooan IoT hub you will create.</span></span> <span data-ttu-id="57252-107">Daha sonra örnek bir uygulama üzerinde ESP8266 toocollect sıcaklık ve nem veri DHT22 algılayıcının çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="57252-107">Then run a sample application on ESP8266 toocollect temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="57252-108">Son olarak, hello algılayıcı verileri tooyour IOT hub'ı gönderin.</span><span class="sxs-lookup"><span data-stu-id="57252-108">Finally, send hello sensor data tooyour IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="57252-109">Diğer ESP8266 panoları kullanıyorsanız, bu adımları tooconnect hala izleyebilirsiniz, tooyour IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="57252-109">If you are using other ESP8266 boards, you can still follow these steps tooconnect it tooyour IoT hub.</span></span> <span data-ttu-id="57252-110">Kullanmakta olduğunuz hello ESP8266 Panosu bağlı olarak, tooreconfigure hello gerekebilir `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="57252-110">Depending on hello ESP8266 board you are using, you may need tooreconfigure hello `LED_PIN`.</span></span> <span data-ttu-id="57252-111">AI Thinker gelen ESP8266 kullanıyorsanız, örneğin, ondan değişebilir `0` çok`2`.</span><span class="sxs-lookup"><span data-stu-id="57252-111">For example, if you are using ESP8266 from AI-Thinker, you may change it from `0` too`2`.</span></span> <span data-ttu-id="57252-112">Bir pakete henüz yok mu?: tıklatın [burada](http://azure.com/iotstarterkits)</span><span class="sxs-lookup"><span data-stu-id="57252-112">Don't have a kit yet?: Click [here](http://azure.com/iotstarterkits)</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="57252-113">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="57252-113">What you will learn</span></span>

* <span data-ttu-id="57252-114">Nasıl toocreate IOT hub'ı ve şey istisnası için bir cihaz kaydetme</span><span class="sxs-lookup"><span data-stu-id="57252-114">How toocreate an IoT hub and register a device for Thing Dev.</span></span>
* <span data-ttu-id="57252-115">Nasıl tooconnect şey geliştirme hello algılayıcı ve bilgisayarınızı.</span><span class="sxs-lookup"><span data-stu-id="57252-115">How tooconnect Thing Dev with hello sensor and your computer.</span></span>
* <span data-ttu-id="57252-116">Nasıl şey istisnası üzerinde bir örnek uygulamayı çalıştırarak toocollect algılayıcı verileri</span><span class="sxs-lookup"><span data-stu-id="57252-116">How toocollect sensor data by running a sample application on Thing Dev.</span></span>
* <span data-ttu-id="57252-117">Nasıl toosend algılayıcı verileri tooyour IOT hub'ı hello.</span><span class="sxs-lookup"><span data-stu-id="57252-117">How toosend hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="57252-118">İhtiyacınız olacak</span><span class="sxs-lookup"><span data-stu-id="57252-118">What you will need</span></span>

![Merhaba öğretici için gerekli bölümleri](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="57252-120">toocomplete bu işlemi şey geliştirme Starter Seti'nden bölümleri aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="57252-120">toocomplete this operation, you need hello following parts from your Thing Dev Starter Kit:</span></span>

* <span data-ttu-id="57252-121">Merhaba Sparkfun ESP8266 şey geliştirme Panosu.</span><span class="sxs-lookup"><span data-stu-id="57252-121">hello Sparkfun ESP8266 Thing Dev board.</span></span>
* <span data-ttu-id="57252-122">Mikro USB tooType bir USB kablosu.</span><span class="sxs-lookup"><span data-stu-id="57252-122">A Micro USB tooType A USB cable.</span></span>

<span data-ttu-id="57252-123">Ayrıca, geliştirme ortamınız için hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="57252-123">You also need hello following for your development environment:</span></span>

* <span data-ttu-id="57252-124">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="57252-124">An active Azure subscription.</span></span> <span data-ttu-id="57252-125">Bir Azure hesabınız yoksa [ücretsiz Azure deneme hesabı oluşturma](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="57252-125">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="57252-126">Mac veya Windows veya Ubuntu çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="57252-126">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="57252-127">Kablosuz ağ Sparkfun ESP8266 şey geliştirme tooconnect için.</span><span class="sxs-lookup"><span data-stu-id="57252-127">Wireless network for Sparkfun ESP8266 Thing Dev tooconnect to.</span></span>
* <span data-ttu-id="57252-128">Internet bağlantısı toodownload hello yapılandırma aracı.</span><span class="sxs-lookup"><span data-stu-id="57252-128">Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="57252-129">[Arduino IDE](https://www.arduino.cc/en/main/software) sürüm 1.6.8 (veya daha yeni), önceki sürümlerinde hello AzureIoT kitaplığı ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="57252-129">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 (or newer), earlier versions will not work with hello AzureIoT library.</span></span>

<span data-ttu-id="57252-130">Algılayıcı olmayan olasılığına hello aşağıdaki öğeler isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="57252-130">hello following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="57252-131">Benzetimli algılayıcı verilerini kullanmanın hello seçeneğiniz de vardır.</span><span class="sxs-lookup"><span data-stu-id="57252-131">You also have hello option of using simulated sensor data.</span></span>

* <span data-ttu-id="57252-132">Bir Adafruit DHT22 sıcaklık ve nem algılayıcı.</span><span class="sxs-lookup"><span data-stu-id="57252-132">An Adafruit DHT22 temperature and humidity sensor.</span></span>
* <span data-ttu-id="57252-133">Bir breadboard.</span><span class="sxs-lookup"><span data-stu-id="57252-133">A breadboard.</span></span>
* <span data-ttu-id="57252-134">M/M anahtar kablolarını.</span><span class="sxs-lookup"><span data-stu-id="57252-134">M/M jumper wires.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-hello-sensor-and-your-computer"></a><span data-ttu-id="57252-135">Merhaba algılayıcı ve bilgisayarınızla ESP8266 şey geliştirme Bağlan</span><span class="sxs-lookup"><span data-stu-id="57252-135">Connect ESP8266 Thing Dev with hello sensor and your computer</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-tooesp8266-thing-dev"></a><span data-ttu-id="57252-136">DHT22 sıcaklık ve nem algılayıcı bağlanmak tooESP8266 şey geliştirme</span><span class="sxs-lookup"><span data-stu-id="57252-136">Connect a DHT22 temperature and humidity sensor tooESP8266 Thing Dev</span></span>

<span data-ttu-id="57252-137">Merhaba breadboard ve anahtar kablolarını toomake hello bağlantısı aşağıdaki şekilde kullanın.</span><span class="sxs-lookup"><span data-stu-id="57252-137">Use hello breadboard and jumper wires toomake hello connection as follows.</span></span> <span data-ttu-id="57252-138">Algılayıcı yoksa, benzetimli algılayıcı verilerini yerine kullandığından bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57252-138">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Bağlantı Başvurusu](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

<span data-ttu-id="57252-140">Kablolama aşağıdaki hello algılayıcı PIN'ler için kullanırız:</span><span class="sxs-lookup"><span data-stu-id="57252-140">For sensor pins, we will use hello following wiring:</span></span>

| <span data-ttu-id="57252-141">Başlangıç (algılayıcı)</span><span class="sxs-lookup"><span data-stu-id="57252-141">Start (Sensor)</span></span>           | <span data-ttu-id="57252-142">Bitiş (kartı)</span><span class="sxs-lookup"><span data-stu-id="57252-142">End (Board)</span></span>           | <span data-ttu-id="57252-143">Kablo rengi</span><span class="sxs-lookup"><span data-stu-id="57252-143">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="57252-144">VDD (PIN 27F)</span><span class="sxs-lookup"><span data-stu-id="57252-144">VDD (Pin 27F)</span></span>            | <span data-ttu-id="57252-145">3v (PIN 8A)</span><span class="sxs-lookup"><span data-stu-id="57252-145">3V (Pin 8A)</span></span>           | <span data-ttu-id="57252-146">Kırmızı kablosu</span><span class="sxs-lookup"><span data-stu-id="57252-146">Red cable</span></span>     |
| <span data-ttu-id="57252-147">Veri (PIN 28F)</span><span class="sxs-lookup"><span data-stu-id="57252-147">DATA (Pin 28F)</span></span>           | <span data-ttu-id="57252-148">GPIO'yu 2 (PIN 9A)</span><span class="sxs-lookup"><span data-stu-id="57252-148">GPIO 2 (Pin 9A)</span></span>       | <span data-ttu-id="57252-149">Beyaz kablosu</span><span class="sxs-lookup"><span data-stu-id="57252-149">White cable</span></span>    |
| <span data-ttu-id="57252-150">GND (PIN 30F)</span><span class="sxs-lookup"><span data-stu-id="57252-150">GND (Pin 30F)</span></span>            | <span data-ttu-id="57252-151">GND (PIN 7J)</span><span class="sxs-lookup"><span data-stu-id="57252-151">GND (Pin 7J)</span></span>          | <span data-ttu-id="57252-152">Siyah kablosu</span><span class="sxs-lookup"><span data-stu-id="57252-152">Black cable</span></span>   |


- <span data-ttu-id="57252-153">Daha fazla bilgi için bkz: [DHT22 algılayıcı Kurulum](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) ve [Sparkfun ESP8266 şey geliştirme belirtimi](https://www.sparkfun.com/products/13711)</span><span class="sxs-lookup"><span data-stu-id="57252-153">For more information, see: [DHT22 sensor setup](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) and [Sparkfun ESP8266 Thing Dev specification](https://www.sparkfun.com/products/13711)</span></span>

<span data-ttu-id="57252-154">Şimdi, Sparkfun ESP8266 şey geliştirme ile çalışma algılayıcı bağlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="57252-154">Now your Sparkfun ESP8266 Thing Dev should be connected with a working sensor.</span></span>

![dht22 ESP8266 şey geliştirme ile bağlanma](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-tooyour-computer"></a><span data-ttu-id="57252-156">Sparkfun ESP8266 şey geliştirme tooyour bilgisayara bağlanma</span><span class="sxs-lookup"><span data-stu-id="57252-156">Connect Sparkfun ESP8266 Thing Dev tooyour computer</span></span>

<span data-ttu-id="57252-157">Merhaba mikro USB tooType bir USB kablosu tooconnect Sparkfun ESP8266 şey geliştirme tooyour bilgisayar aşağıdaki şekilde kullanın.</span><span class="sxs-lookup"><span data-stu-id="57252-157">Use hello Micro USB tooType A USB cable tooconnect Sparkfun ESP8266 Thing Dev tooyour computer as follows.</span></span>

![yumuşatma huzzah tooyour bilgisayara bağlanma](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a><span data-ttu-id="57252-159">Seri bağlantı noktası izinleri – yalnızca Ubuntu ekleyin</span><span class="sxs-lookup"><span data-stu-id="57252-159">Add serial port permissions – Ubuntu only</span></span>

<span data-ttu-id="57252-160">Ubuntu kullanıyorsanız, normal bir kullanıcı hello izinleri toooperate hello USB bağlantı noktası, Sparkfun ESP8266 şey istisnası üzerinde sahip olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="57252-160">If you use Ubuntu, make sure a normal user has hello permissions toooperate on hello USB port of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="57252-161">tooadd seri bağlantı noktası izinleri normal bir kullanıcı için aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="57252-161">tooadd serial port permissions for a normal user, follow these steps:</span></span>

1. <span data-ttu-id="57252-162">Bir terminal komutları aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="57252-162">Run hello following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="57252-163">Çıktı aşağıdaki hello birini alın:</span><span class="sxs-lookup"><span data-stu-id="57252-163">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="57252-164">crw-rw---1 kök uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="57252-164">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="57252-165">crw-rw---1 kök araması xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="57252-165">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="57252-166">Merhaba çıktısında fark `uucp` veya `dialout` diğer bir deyişle hello Grup sahibi adını hello USB bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="57252-166">In hello output, notice `uucp` or `dialout` that is hello group owner name of hello USB port.</span></span>

1. <span data-ttu-id="57252-167">Merhaba kullanıcı toohello grubu hello aşağıdaki komutu çalıştırarak ekleyin:</span><span class="sxs-lookup"><span data-stu-id="57252-167">Add hello user toohello group by running hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="57252-168">`<group-owner-name>`elde ettiğiniz hello Grup sahibi hello önceki adımda adıdır.</span><span class="sxs-lookup"><span data-stu-id="57252-168">`<group-owner-name>` is hello group owner name you obtained in hello previous step.</span></span> <span data-ttu-id="57252-169">`<username>`Ubuntu kullanıcı adınızdır.</span><span class="sxs-lookup"><span data-stu-id="57252-169">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="57252-170">Ubuntu ve yeniden oturum içinde hello tootake değişikliğin için.</span><span class="sxs-lookup"><span data-stu-id="57252-170">Log out Ubuntu and log in it again for hello change tootake effect.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="57252-171">Algılayıcı verilerini toplamak ve tooyour IOT hub'ı gönderin</span><span class="sxs-lookup"><span data-stu-id="57252-171">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="57252-172">Bu bölümde, dağıtma ve Sparkfun ESP8266 şey istisnası üzerinde örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="57252-172">In this section, you deploy and run a sample application on Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="57252-173">Merhaba örnek uygulaması hello LED Sparkfun ESP8266 şey geliştirme üzerinde yanıp ve hello sıcaklık gönderir ve nem veri hello DHT22 algılayıcı tooyour IOT hub'ı toplanır.</span><span class="sxs-lookup"><span data-stu-id="57252-173">hello sample application blinks hello LED on Sparkfun ESP8266 Thing Dev and sends hello temperature and humidity data collected from hello DHT22 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github"></a><span data-ttu-id="57252-174">Merhaba örnek uygulaması Github'dan alma</span><span class="sxs-lookup"><span data-stu-id="57252-174">Get hello sample application from GitHub</span></span>

<span data-ttu-id="57252-175">Merhaba örnek uygulaması, GitHub üzerinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="57252-175">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="57252-176">Merhaba örnek uygulaması github'dan içeren hello örnek depoyu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="57252-176">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="57252-177">tooclone hello örnek deposu, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="57252-177">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="57252-178">Bir komut istemi veya terminal penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="57252-178">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="57252-179">Depolanan hello örnek uygulama toobe istediğiniz tooa klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="57252-179">Go tooa folder where you want hello sample application toobe stored.</span></span>
1. <span data-ttu-id="57252-180">Merhaba aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="57252-180">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

<span data-ttu-id="57252-181">Sparkfun ESP8266 şey geliştirme Arduino IDE'de Hello paketi yükle:</span><span class="sxs-lookup"><span data-stu-id="57252-181">Install hello package for Sparkfun ESP8266 Thing Dev in Arduino IDE:</span></span>

1. <span data-ttu-id="57252-182">Merhaba örnek uygulaması depolandığı hello klasörünü açın.</span><span class="sxs-lookup"><span data-stu-id="57252-182">Open hello folder where hello sample application is stored.</span></span>
1. <span data-ttu-id="57252-183">Merhaba uygulama klasöründe Arduino IDE Hello app.ino dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="57252-183">Open hello app.ino file in hello app folder in Arduino IDE.</span></span>

   ![Merhaba örnek uygulaması arduino IDE içinde açın](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="57252-185">Hello Arduino IDE, tıklatın **dosya** > **Tercihler**.</span><span class="sxs-lookup"><span data-stu-id="57252-185">In hello Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="57252-186">Merhaba, **Tercihler** iletişim kutusunda, hello simgesi sonraki toohello tıklayın **ek panoları yöneticisi URL'leri** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="57252-186">In hello **Preferences** dialog box, click hello icon next toohello **Additional Boards Manager URLs** text box.</span></span>
1. <span data-ttu-id="57252-187">URL aşağıdaki hello Hello açılır pencerede girin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="57252-187">In hello pop-up window, enter hello following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![arduino IDE içinde tooa paket URL'sini noktası](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="57252-189">Merhaba, **tercih** iletişim kutusu, tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="57252-189">In hello **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="57252-190">Tıklatın **Araçları** > **Panosu** > **panoları Yöneticisi**ve esp8266 için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="57252-190">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>
   <span data-ttu-id="57252-191">ESP8266 2.2.0 veya sonraki bir sürümüyle yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="57252-191">ESP8266 with a version of 2.2.0 or later should be installed.</span></span>

   ![Merhaba esp8266 paketinin yüklü olduğu](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="57252-193">Tıklatın **Araçları** > **Panosu** > **Sparkfun ESP8266 şey geliştirme**.</span><span class="sxs-lookup"><span data-stu-id="57252-193">Click **Tools** > **Board** > **Sparkfun ESP8266 Thing Dev**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="57252-194">Gerekli kitaplıkları yükleme</span><span class="sxs-lookup"><span data-stu-id="57252-194">Install necessary libraries</span></span>

1. <span data-ttu-id="57252-195">Hello Arduino IDE, tıklatın **taslak** > **dahil Kitaplığı** > **yönetmek kitaplıkları**.</span><span class="sxs-lookup"><span data-stu-id="57252-195">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="57252-196">Kitaplık adları tek tek aşağıdaki hello arayın.</span><span class="sxs-lookup"><span data-stu-id="57252-196">Search for hello following library names one by one.</span></span> <span data-ttu-id="57252-197">Her bulduğunuz hello kitaplığının tıklatın **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="57252-197">For each of hello library you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="57252-198">Gerçek DHT22 algılayıcı yok mu?</span><span class="sxs-lookup"><span data-stu-id="57252-198">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="57252-199">Gerçek DHT22 algılayıcı olmayan olasılığına Merhaba örnek uygulaması sıcaklık ve nem veri benzetimini yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57252-199">hello sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="57252-200">tooenable hello örnek uygulama benzetimli toouse verileri, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="57252-200">tooenable hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="57252-201">Açık hello `config.h` hello dosyasında `app` klasör.</span><span class="sxs-lookup"><span data-stu-id="57252-201">Open hello `config.h` file in hello `app` folder.</span></span>
1. <span data-ttu-id="57252-202">Aşağıdaki kod hello bulun ve hello değerinden değiştirmek `false` çok`true`:</span><span class="sxs-lookup"><span data-stu-id="57252-202">Locate hello following line of code and change hello value from `false` too`true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Merhaba örnek uygulama benzetimli toouse verileri yapılandırma](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. <span data-ttu-id="57252-204">İle Kaydet `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="57252-204">Save with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toosparkfun-esp8266-thing-dev"></a><span data-ttu-id="57252-205">Merhaba örnek uygulama tooSparkfun ESP8266 şey geliştirme dağıtma</span><span class="sxs-lookup"><span data-stu-id="57252-205">Deploy hello sample application tooSparkfun ESP8266 Thing Dev</span></span>

1. <span data-ttu-id="57252-206">Hello Arduino IDE, tıklatın **aracı** > **bağlantı noktası**ve Sparkfun ESP8266 şey istisnası hello seri bağlantı noktası'ı tıklatın</span><span class="sxs-lookup"><span data-stu-id="57252-206">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Sparkfun ESP8266 Thing Dev.</span></span>
1. <span data-ttu-id="57252-207">Tıklatın **taslak** > **karşıya** toobuild ve hello örnek uygulama tooSparkfun ESP8266 şey istisnası dağıtma</span><span class="sxs-lookup"><span data-stu-id="57252-207">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooSparkfun ESP8266 Thing Dev.</span></span>

> [!Note]
> <span data-ttu-id="57252-208">MacOS kullanıyorsanız büyük olasılıkla karşıya yükleme sırasında iletileri aşağıdaki hello görebilir.</span><span class="sxs-lookup"><span data-stu-id="57252-208">If you are using macOS you could probably see hello following messages during uploading.</span></span> <span data-ttu-id="57252-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span><span class="sxs-lookup"><span data-stu-id="57252-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span></span> <span data-ttu-id="57252-210">Lütfen ternimal penceresini açın ve bu sorun Eylemler toosolve son.</span><span class="sxs-lookup"><span data-stu-id="57252-210">Please open your ternimal window and finish below actions toosolve this issue.</span></span>
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a><span data-ttu-id="57252-211">Kimlik bilgilerinizi girin</span><span class="sxs-lookup"><span data-stu-id="57252-211">Enter your credentials</span></span>

<span data-ttu-id="57252-212">Merhaba karşıya yükleme başarıyla tamamlandıktan sonra kimlik bilgilerinizi hello adımları tooenter izleyin:</span><span class="sxs-lookup"><span data-stu-id="57252-212">After hello upload completes successfully, follow hello steps tooenter your credentials:</span></span>

1. <span data-ttu-id="57252-213">Hello Arduino IDE, tıklatın **Araçları** > **seri İzleyici**.</span><span class="sxs-lookup"><span data-stu-id="57252-213">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="57252-214">Merhaba seri İzleyicisi penceresinde hello sağ alt köşesindeki hello iki açılan listelerde dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="57252-214">In hello serial monitor window, notice hello two drop-down lists on hello bottom right corner.</span></span>
1. <span data-ttu-id="57252-215">Seçin **hiçbir satır bitiş** hello sol aşağı açılan listesi.</span><span class="sxs-lookup"><span data-stu-id="57252-215">Select **No line ending** for hello left drop-down list.</span></span>
1. <span data-ttu-id="57252-216">Seçin **115200 baud** hello sağda açılan listesi.</span><span class="sxs-lookup"><span data-stu-id="57252-216">Select **115200 baud** for hello right drop-down list.</span></span>
1. <span data-ttu-id="57252-217">Merhaba seri İzleyicisi penceresinde Hello üstünde bulunan hello giriş tooprovide sorulursa bilgisinden hello kutusuna ve ardından **Gönder**.</span><span class="sxs-lookup"><span data-stu-id="57252-217">In hello input box located at hello top of hello serial monitor window, enter hello following information if you are asked tooprovide them, and then click **Send**.</span></span>
   * <span data-ttu-id="57252-218">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="57252-218">Wi-Fi SSID</span></span>
   * <span data-ttu-id="57252-219">Wi-Fi parola</span><span class="sxs-lookup"><span data-stu-id="57252-219">Wi-Fi password</span></span>
   * <span data-ttu-id="57252-220">Cihaz bağlantı dizesi</span><span class="sxs-lookup"><span data-stu-id="57252-220">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="57252-221">Merhaba kimlik bilgileri hello EEPROM Sparkfun ESP8266 şey istisnası depolanır</span><span class="sxs-lookup"><span data-stu-id="57252-221">hello credential information is stored in hello EEPROM of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="57252-222">Merhaba Sparkfun ESP8266 şey geliştirme Panosu hello Sıfırla düğmesini tıklatın, Merhaba örnek uygulaması tooerase hello bilgi isteyip istemediğinizi sorar.</span><span class="sxs-lookup"><span data-stu-id="57252-222">If you click hello reset button on hello Sparkfun ESP8266 Thing Dev board, hello sample application asks you if you want tooerase hello information.</span></span> <span data-ttu-id="57252-223">Girin `Y` toohave hello bilgi silinmesi ve yeniden tooprovide hello bilgi istendi.</span><span class="sxs-lookup"><span data-stu-id="57252-223">Enter `Y` toohave hello information erased and you are asked tooprovide hello information again.</span></span>

### <a name="verify-hello-sample-application-is-running-successfully"></a><span data-ttu-id="57252-224">Merhaba örnek uygulaması başarılı bir şekilde çalıştığını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="57252-224">Verify hello sample application is running successfully</span></span>

<span data-ttu-id="57252-225">Görürseniz hello seri İzleyicisi penceresinde hello şu çıktıları ve LED Sparkfun ESP8266 şey geliştirme, Merhaba örnek uygulaması üzerinde yanıp sönen hello başarılı bir şekilde çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="57252-225">If you see hello following output from hello serial monitor window and hello blinking LED on Sparkfun ESP8266 Thing Dev, hello sample application is running successfully.</span></span>

![arduino IDE içinde son çıktı](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="57252-227">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="57252-227">Next steps</span></span>

<span data-ttu-id="57252-228">Başarıyla bir Sparkfun ESP8266 şey geliştirme tooyour IOT hub'ı bağlı ve yakalanan hello algılayıcı verileri tooyour IOT hub'ı gönderilir.</span><span class="sxs-lookup"><span data-stu-id="57252-228">You have successfully connected a Sparkfun ESP8266 Thing Dev tooyour IoT hub and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
