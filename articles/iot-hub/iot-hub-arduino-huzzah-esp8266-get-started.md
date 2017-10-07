---
title: "aaaESP8266 toocloud - bağlanmak yumuşatma HUZZAH ESP8266 tooAzure IOT hub'ı | Microsoft Docs"
description: "Bilgi nasıl toosetup ve onun için Adafruit yumuşatma HUZZAH ESP8266 tooAzure IOT hub'ı Bu öğreticide toosend veri toohello Azure bulut platformu bağlanın."
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
ms.openlocfilehash: 44fd47232488948d21c7aa71bdd865397e41e63e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="81cc3-103">Adafruit yumuşatma HUZZAH ESP8266 tooAzure IOT Hub'hello bulutta Bağlan</span><span class="sxs-lookup"><span data-stu-id="81cc3-103">Connect Adafruit Feather HUZZAH ESP8266 tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![DHT22, yumuşatma HUZZAH ESP8266 ve IOT hub'ı arasında bir bağlantı](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a><span data-ttu-id="81cc3-105">Neler</span><span class="sxs-lookup"><span data-stu-id="81cc3-105">What you do</span></span>


<span data-ttu-id="81cc3-106">Oluşturduğunuz Adafruit yumuşatma HUZZAH ESP8266 tooan IOT hub bağlayın.</span><span class="sxs-lookup"><span data-stu-id="81cc3-106">Connect Adafruit Feather HUZZAH ESP8266 tooan IoT hub that you create.</span></span> <span data-ttu-id="81cc3-107">Daha sonra örnek bir uygulama DHT22 algılayıcı sıcaklık ve nem ESP8266 toocollect hello verileri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="81cc3-107">Then you run a sample application on ESP8266 toocollect hello temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="81cc3-108">Son olarak, hello algılayıcı verileri tooyour IOT hub'ı gönderin.</span><span class="sxs-lookup"><span data-stu-id="81cc3-108">Finally, you send hello sensor data tooyour IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="81cc3-109">Diğer ESP8266 panoları kullanıyorsanız, bu adımları tooconnect hala izleyebilirsiniz, tooyour IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="81cc3-109">If you're using other ESP8266 boards, you can still follow these steps tooconnect it tooyour IoT hub.</span></span> <span data-ttu-id="81cc3-110">Kullanmakta olduğunuz hello ESP8266 Panosu bağlı olarak, tooreconfigure hello gerekebilecek `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="81cc3-110">Depending on hello ESP8266 board you're using, you might need tooreconfigure hello `LED_PIN`.</span></span> <span data-ttu-id="81cc3-111">AI Thinker gelen ESP8266 kullanıyorsanız, örneğin, ondan değişebilir `0` çok`2`.</span><span class="sxs-lookup"><span data-stu-id="81cc3-111">For example, if you're using ESP8266 from AI-Thinker, you might change it from `0` too`2`.</span></span> <span data-ttu-id="81cc3-112">Bir pakete henüz yok mu?</span><span class="sxs-lookup"><span data-stu-id="81cc3-112">Don't have a kit yet?</span></span> <span data-ttu-id="81cc3-113">Hello alma [Azure Web sitesi](http://azure.com/iotstarterkits).</span><span class="sxs-lookup"><span data-stu-id="81cc3-113">Get it from hello [Azure website](http://azure.com/iotstarterkits).</span></span>




## <a name="what-you-learn"></a><span data-ttu-id="81cc3-114">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="81cc3-114">What you learn</span></span>

* <span data-ttu-id="81cc3-115">Nasıl toocreate IOT hub'ı ve yumuşatma HUZZAH ESP8266 için bir cihaz kaydetme</span><span class="sxs-lookup"><span data-stu-id="81cc3-115">How toocreate an IoT hub and register a device for Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="81cc3-116">Nasıl tooconnect yumuşatma HUZZAH ESP8266 hello algılayıcı ve bilgisayarınız</span><span class="sxs-lookup"><span data-stu-id="81cc3-116">How tooconnect Feather HUZZAH ESP8266 with hello sensor and your computer</span></span>
* <span data-ttu-id="81cc3-117">Nasıl yumuşatma HUZZAH ESP8266 üzerinde bir örnek uygulamayı çalıştırarak toocollect algılayıcı verileri</span><span class="sxs-lookup"><span data-stu-id="81cc3-117">How toocollect sensor data by running a sample application on Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="81cc3-118">Nasıl toosend hello algılayıcı verileri tooyour IOT hub'ı</span><span class="sxs-lookup"><span data-stu-id="81cc3-118">How toosend hello sensor data tooyour IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="81cc3-119">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="81cc3-119">What you need</span></span>

![Merhaba öğretici için gerekli bölümleri](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="81cc3-121">toocomplete bu işlemi yumuşatma HUZZAH ESP8266 Starter Seti'nden bölümleri aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="81cc3-121">toocomplete this operation, you need hello following parts from your Feather HUZZAH ESP8266 Starter Kit:</span></span>

* <span data-ttu-id="81cc3-122">Merhaba yumuşatma HUZZAH ESP8266 Panosu</span><span class="sxs-lookup"><span data-stu-id="81cc3-122">hello Feather HUZZAH ESP8266 board</span></span>
* <span data-ttu-id="81cc3-123">Mikro USB tooType bir USB kablosu</span><span class="sxs-lookup"><span data-stu-id="81cc3-123">A Micro USB tooType A USB cable</span></span>

<span data-ttu-id="81cc3-124">Ayrıca geliştirme ortamınız için öğeleri izleyen hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="81cc3-124">You also need hello following things for your development environment:</span></span>

* <span data-ttu-id="81cc3-125">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="81cc3-125">An active Azure subscription.</span></span> <span data-ttu-id="81cc3-126">Bir Azure hesabınız yoksa [ücretsiz Azure deneme hesabı oluşturma](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="81cc3-126">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="81cc3-127">Mac veya Windows veya Ubuntu çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="81cc3-127">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="81cc3-128">Kablosuz ağ yumuşatma HUZZAH ESP8266 tooconnect için.</span><span class="sxs-lookup"><span data-stu-id="81cc3-128">Wireless network for Feather HUZZAH ESP8266 tooconnect to.</span></span>
* <span data-ttu-id="81cc3-129">Internet bağlantısı toodownload hello yapılandırma aracı.</span><span class="sxs-lookup"><span data-stu-id="81cc3-129">Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="81cc3-130">[Arduino IDE](https://www.arduino.cc/en/main/software) sürüm 1.6.8 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="81cc3-130">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="81cc3-131">Önceki sürümlerde hello AzureIoT kitaplığı ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="81cc3-131">Earlier versions don't work with hello AzureIoT library.</span></span>

<span data-ttu-id="81cc3-132">Algılayıcı olmayan olasılığına hello aşağıdaki öğeler isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="81cc3-132">hello following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="81cc3-133">Benzetimli algılayıcı verilerini kullanmanın hello seçeneğiniz de vardır.</span><span class="sxs-lookup"><span data-stu-id="81cc3-133">You also have hello option of using simulated sensor data.</span></span>

* <span data-ttu-id="81cc3-134">Adafruit DHT22 sıcaklık ve nem algılayıcısı</span><span class="sxs-lookup"><span data-stu-id="81cc3-134">An Adafruit DHT22 temperature and humidity sensor</span></span>
* <span data-ttu-id="81cc3-135">Bir breadboard</span><span class="sxs-lookup"><span data-stu-id="81cc3-135">A breadboard</span></span>
* <span data-ttu-id="81cc3-136">M/M anahtar kabloları</span><span class="sxs-lookup"><span data-stu-id="81cc3-136">M/M jumper wires</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-hello-sensor-and-your-computer"></a><span data-ttu-id="81cc3-137">Merhaba algılayıcı ve bilgisayarınızla yumuşatma HUZZAH ESP8266 Bağlan</span><span class="sxs-lookup"><span data-stu-id="81cc3-137">Connect Feather HUZZAH ESP8266 with hello sensor and your computer</span></span>
<span data-ttu-id="81cc3-138">Bu bölümde, hello algılayıcılar tooyour Panosu bağlayın.</span><span class="sxs-lookup"><span data-stu-id="81cc3-138">In this section, you connect hello sensors tooyour board.</span></span> <span data-ttu-id="81cc3-139">Ardından aygıt tooyour bilgisayarınızdaki başka kullanmak için takın.</span><span class="sxs-lookup"><span data-stu-id="81cc3-139">Then you plug in your device tooyour computer for further use.</span></span>
### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-huzzah-esp8266"></a><span data-ttu-id="81cc3-140">Bir DHT22 sıcaklık ve nem algılayıcı tooFeather HUZZAH ESP8266 Bağlan</span><span class="sxs-lookup"><span data-stu-id="81cc3-140">Connect a DHT22 temperature and humidity sensor tooFeather HUZZAH ESP8266</span></span>

<span data-ttu-id="81cc3-141">Merhaba breadboard ve anahtar kablolarını toomake hello bağlantısı aşağıdaki şekilde kullanın.</span><span class="sxs-lookup"><span data-stu-id="81cc3-141">Use hello breadboard and jumper wires toomake hello connection as follows.</span></span> <span data-ttu-id="81cc3-142">Algılayıcı yoksa, benzetimli algılayıcı verilerini yerine kullandığından bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81cc3-142">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Bağlantı Başvurusu](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


<span data-ttu-id="81cc3-144">Algılayıcı PIN'ler için kablolama aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="81cc3-144">For sensor pins, use hello following wiring:</span></span>


| <span data-ttu-id="81cc3-145">Başlangıç (algılayıcı)</span><span class="sxs-lookup"><span data-stu-id="81cc3-145">Start (Sensor)</span></span>           | <span data-ttu-id="81cc3-146">Bitiş (kartı)</span><span class="sxs-lookup"><span data-stu-id="81cc3-146">End (Board)</span></span>           | <span data-ttu-id="81cc3-147">Kablo rengi</span><span class="sxs-lookup"><span data-stu-id="81cc3-147">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="81cc3-148">VDD (PIN 31F)</span><span class="sxs-lookup"><span data-stu-id="81cc3-148">VDD (Pin 31F)</span></span>            | <span data-ttu-id="81cc3-149">3v (PIN 58H)</span><span class="sxs-lookup"><span data-stu-id="81cc3-149">3V (Pin 58H)</span></span>           | <span data-ttu-id="81cc3-150">Kırmızı kablosu</span><span class="sxs-lookup"><span data-stu-id="81cc3-150">Red cable</span></span>     |
| <span data-ttu-id="81cc3-151">Veri (PIN 32F)</span><span class="sxs-lookup"><span data-stu-id="81cc3-151">DATA (Pin 32F)</span></span>           | <span data-ttu-id="81cc3-152">GPIO'yu 2 (PIN 46A)</span><span class="sxs-lookup"><span data-stu-id="81cc3-152">GPIO 2 (Pin 46A)</span></span>       | <span data-ttu-id="81cc3-153">Mavi kablosu</span><span class="sxs-lookup"><span data-stu-id="81cc3-153">Blue cable</span></span>    |
| <span data-ttu-id="81cc3-154">GND (PIN 34F)</span><span class="sxs-lookup"><span data-stu-id="81cc3-154">GND (Pin 34F)</span></span>            | <span data-ttu-id="81cc3-155">GND (PIN 56I)</span><span class="sxs-lookup"><span data-stu-id="81cc3-155">GND (PIn 56I)</span></span>          | <span data-ttu-id="81cc3-156">Siyah kablosu</span><span class="sxs-lookup"><span data-stu-id="81cc3-156">Black cable</span></span>   |

<span data-ttu-id="81cc3-157">Daha fazla bilgi için bkz: [Adafruit DHT22 algılayıcı Kurulum](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) ve [Adafruit yumuşatma HUZZAH Esp8266 no'lu](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span><span class="sxs-lookup"><span data-stu-id="81cc3-157">For more information, see [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) and [Adafruit Feather HUZZAH Esp8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span></span>



<span data-ttu-id="81cc3-158">Şimdi yumuşatma Huzzah ESP8266 ile çalışma algılayıcı bağlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="81cc3-158">Now your Feather Huzzah ESP8266 should be connected with a working sensor.</span></span>

![Yumuşatma Huzzah ile DHT22 Bağlan](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-tooyour-computer"></a><span data-ttu-id="81cc3-160">Yumuşatma HUZZAH ESP8266 tooyour bilgisayara bağlanma</span><span class="sxs-lookup"><span data-stu-id="81cc3-160">Connect Feather HUZZAH ESP8266 tooyour computer</span></span>

<span data-ttu-id="81cc3-161">Sonraki gösterildiği gibi hello mikro USB tooType bir USB kablosu tooconnect yumuşatma HUZZAH ESP8266 tooyour bilgisayar kullanın.</span><span class="sxs-lookup"><span data-stu-id="81cc3-161">As shown next, use hello Micro USB tooType A USB cable tooconnect Feather HUZZAH ESP8266 tooyour computer.</span></span>

![Yumuşatma Huzzah tooyour bilgisayara bağlanma](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="81cc3-163">Seri bağlantı noktası izinleri (yalnızca Ubuntu) ekleyin</span><span class="sxs-lookup"><span data-stu-id="81cc3-163">Add serial port permissions (Ubuntu only)</span></span>


<span data-ttu-id="81cc3-164">Ubuntu kullanırsanız, hello izinleri toooperate hello USB bağlantı noktası, yumuşatma HUZZAH ESP8266 üzerinde olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="81cc3-164">If you use Ubuntu, make sure you have hello permissions toooperate on hello USB port of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="81cc3-165">tooadd seri bağlantı noktası izinleri, aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="81cc3-165">tooadd serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="81cc3-166">Bir terminal komutları aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="81cc3-166">Run hello following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="81cc3-167">Çıktı aşağıdaki hello birini alın:</span><span class="sxs-lookup"><span data-stu-id="81cc3-167">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="81cc3-168">crw-rw---1 kök uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="81cc3-168">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="81cc3-169">crw-rw---1 kök araması xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="81cc3-169">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="81cc3-170">Merhaba çıktısında dikkat `uucp` veya `dialout` hello Grup sahibi hello USB bağlantı noktasına adıdır.</span><span class="sxs-lookup"><span data-stu-id="81cc3-170">In hello output, notice that `uucp` or `dialout` is hello group owner name of hello USB port.</span></span>

1. <span data-ttu-id="81cc3-171">Merhaba kullanıcı toohello grubu hello aşağıdaki komutu çalıştırarak ekleyin:</span><span class="sxs-lookup"><span data-stu-id="81cc3-171">Add hello user toohello group by running hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="81cc3-172">`<group-owner-name>`elde ettiğiniz hello Grup sahibi hello önceki adımda adıdır.</span><span class="sxs-lookup"><span data-stu-id="81cc3-172">`<group-owner-name>` is hello group owner name you obtained in hello previous step.</span></span> <span data-ttu-id="81cc3-173">`<username>`Ubuntu kullanıcı adınızdır.</span><span class="sxs-lookup"><span data-stu-id="81cc3-173">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="81cc3-174">Ubuntu dışında oturum açın ve yeniden hello değişiklik tooappear için oturum açın.</span><span class="sxs-lookup"><span data-stu-id="81cc3-174">Sign out of Ubuntu, and then sign in again for hello change tooappear.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="81cc3-175">Algılayıcı verilerini toplamak ve tooyour IOT hub'ı gönderin</span><span class="sxs-lookup"><span data-stu-id="81cc3-175">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="81cc3-176">Bu bölümde, dağıtın ve yumuşatma HUZZAH ESP8266 üzerinde bir örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="81cc3-176">In this section, you deploy and run a sample application on Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="81cc3-177">Merhaba örnek uygulaması hello LED yumuşatma HUZZAH ESP8266 üzerinde yanıp ve hello sıcaklık gönderir ve nem veri hello DHT22 algılayıcı tooyour IOT hub'ı toplanır.</span><span class="sxs-lookup"><span data-stu-id="81cc3-177">hello sample application blinks hello LED on Feather HUZZAH ESP8266, and sends hello temperature and humidity data collected from hello DHT22 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github"></a><span data-ttu-id="81cc3-178">Merhaba örnek uygulaması Github'dan alma</span><span class="sxs-lookup"><span data-stu-id="81cc3-178">Get hello sample application from GitHub</span></span>

<span data-ttu-id="81cc3-179">Merhaba örnek uygulaması, GitHub üzerinde barındırılır.</span><span class="sxs-lookup"><span data-stu-id="81cc3-179">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="81cc3-180">Merhaba örnek uygulaması github'dan içeren hello örnek depoyu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="81cc3-180">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="81cc3-181">tooclone hello örnek deposu, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="81cc3-181">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="81cc3-182">Bir komut istemi veya terminal penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="81cc3-182">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="81cc3-183">Depolanan hello örnek uygulama toobe istediğiniz tooa klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="81cc3-183">Go tooa folder where you want hello sample application toobe stored.</span></span>
1. <span data-ttu-id="81cc3-184">Merhaba aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="81cc3-184">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

<span data-ttu-id="81cc3-185">Merhaba paket yumuşatma HUZZAH ESP8266 hello Arduino IDE yükleyin:</span><span class="sxs-lookup"><span data-stu-id="81cc3-185">Install hello package for Feather HUZZAH ESP8266 in hello Arduino IDE:</span></span>

1. <span data-ttu-id="81cc3-186">Merhaba örnek uygulaması depolandığı hello klasörünü açın.</span><span class="sxs-lookup"><span data-stu-id="81cc3-186">Open hello folder where hello sample application is stored.</span></span>
1. <span data-ttu-id="81cc3-187">Merhaba Arduino IDE hello uygulama klasöründe Hello app.ino dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="81cc3-187">Open hello app.ino file in hello app folder in hello Arduino IDE.</span></span>

   ![Merhaba örnek uygulaması Arduino IDE içinde açın](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="81cc3-189">Hello Arduino IDE, tıklatın **dosya** > **Tercihler**.</span><span class="sxs-lookup"><span data-stu-id="81cc3-189">In hello Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="81cc3-190">Merhaba, **Tercihler** iletişim kutusunda, hello simgesi sonraki toohello tıklayın **ek panoları yöneticisi URL'leri** kutusunu.</span><span class="sxs-lookup"><span data-stu-id="81cc3-190">In hello **Preferences** dialog box, click hello icon next toohello **Additional Boards Manager URLs** box.</span></span>
1. <span data-ttu-id="81cc3-191">URL aşağıdaki hello Hello açılır pencerede girin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="81cc3-191">In hello pop-up window, enter hello following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Arduino IDE içinde tooa paket URL'sini noktası](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="81cc3-193">Merhaba, **tercih** iletişim kutusu, tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="81cc3-193">In hello **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="81cc3-194">Tıklatın **Araçları** > **Panosu** > **panoları Yöneticisi**ve esp8266 için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="81cc3-194">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>

   <span data-ttu-id="81cc3-195">Panoları Yöneticisi ESP8266 2.2.0 veya sonraki bir sürümü ile yüklü olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="81cc3-195">Boards Manager indicates that ESP8266 with a version of 2.2.0 or later is installed.</span></span>

   ![Merhaba esp8266 paketinin yüklü olduğu](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="81cc3-197">Tıklatın **Araçları** > **Panosu** > **Adafruit HUZZAH ESP8266**.</span><span class="sxs-lookup"><span data-stu-id="81cc3-197">Click **Tools** > **Board** > **Adafruit HUZZAH ESP8266**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="81cc3-198">Gerekli kitaplıkları yükleme</span><span class="sxs-lookup"><span data-stu-id="81cc3-198">Install necessary libraries</span></span>

1. <span data-ttu-id="81cc3-199">Hello Arduino IDE, tıklatın **taslak** > **dahil Kitaplığı** > **yönetmek kitaplıkları**.</span><span class="sxs-lookup"><span data-stu-id="81cc3-199">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="81cc3-200">Kitaplık adları tek tek aşağıdaki hello arayın.</span><span class="sxs-lookup"><span data-stu-id="81cc3-200">Search for hello following library names one by one.</span></span> <span data-ttu-id="81cc3-201">Bulduğunuz her kitaplığını tıklatın **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="81cc3-201">For each  library that you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="81cc3-202">Gerçek DHT22 algılayıcı yok mu?</span><span class="sxs-lookup"><span data-stu-id="81cc3-202">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="81cc3-203">Gerçek DHT22 algılayıcı olmayan olasılığına Merhaba örnek uygulaması sıcaklık ve nem veri benzetimini yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81cc3-203">hello sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="81cc3-204">tooset hello örnek uygulama benzetimli toouse verileri, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="81cc3-204">tooset up hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="81cc3-205">Açık hello `config.h` hello dosyasında `app` klasör.</span><span class="sxs-lookup"><span data-stu-id="81cc3-205">Open hello `config.h` file in hello `app` folder.</span></span>
1. <span data-ttu-id="81cc3-206">Aşağıdaki kod hello bulun ve hello değerinden değiştirmek `false` çok`true`:</span><span class="sxs-lookup"><span data-stu-id="81cc3-206">Locate hello following line of code and change hello value from `false` too`true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Merhaba örnek uygulama benzetimli toouse verileri yapılandırma](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. <span data-ttu-id="81cc3-208">Merhaba dosyayla Kaydet `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="81cc3-208">Save hello file with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toofeather-huzzah-esp8266"></a><span data-ttu-id="81cc3-209">Merhaba örnek uygulama tooFeather HUZZAH ESP8266 dağıtma</span><span class="sxs-lookup"><span data-stu-id="81cc3-209">Deploy hello sample application tooFeather HUZZAH ESP8266</span></span>

1. <span data-ttu-id="81cc3-210">Hello Arduino IDE, tıklatın **aracı** > **bağlantı noktası**, yumuşatma HUZZAH ESP8266 hello seri bağlantı noktası'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81cc3-210">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Feather HUZZAH ESP8266.</span></span>
1. <span data-ttu-id="81cc3-211">Tıklatın **taslak** > **karşıya** toobuild ve hello örnek uygulama tooFeather HUZZAH ESP8266 dağıtın.</span><span class="sxs-lookup"><span data-stu-id="81cc3-211">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooFeather HUZZAH ESP8266.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="81cc3-212">Kimlik bilgilerinizi girin</span><span class="sxs-lookup"><span data-stu-id="81cc3-212">Enter your credentials</span></span>

<span data-ttu-id="81cc3-213">Merhaba karşıya yükleme başarıyla tamamlandıktan sonra bu adımları tooenter kimlik bilgilerinizi izleyin:</span><span class="sxs-lookup"><span data-stu-id="81cc3-213">After hello upload completes successfully, follow these steps tooenter your credentials:</span></span>

1. <span data-ttu-id="81cc3-214">Hello Arduino IDE, tıklatın **Araçları** > **seri İzleyici**.</span><span class="sxs-lookup"><span data-stu-id="81cc3-214">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="81cc3-215">Merhaba seri İzleyicisi penceresinde hello iki açılan listeleri hello sağ alt köşedeki dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="81cc3-215">In hello serial monitor window, notice hello two drop-down lists in hello lower-right corner.</span></span>
1. <span data-ttu-id="81cc3-216">Seçin **hiçbir satır bitiş** hello sol aşağı açılan listesi.</span><span class="sxs-lookup"><span data-stu-id="81cc3-216">Select **No line ending** for hello left drop-down list.</span></span>
1. <span data-ttu-id="81cc3-217">Seçin **115200 baud** hello sağda açılan listesi.</span><span class="sxs-lookup"><span data-stu-id="81cc3-217">Select **115200 baud** for hello right drop-down list.</span></span>
1. <span data-ttu-id="81cc3-218">Merhaba seri İzleyicisi penceresinde Hello üstünde bulunan hello giriş tooprovide sorulursa bilgisinden hello kutusuna ve ardından **Gönder**.</span><span class="sxs-lookup"><span data-stu-id="81cc3-218">In hello input box located at hello top of hello serial monitor window, enter hello following information if you are asked tooprovide them, and then click **Send**.</span></span>
   * <span data-ttu-id="81cc3-219">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="81cc3-219">Wi-Fi SSID</span></span>
   * <span data-ttu-id="81cc3-220">Wi-Fi parola</span><span class="sxs-lookup"><span data-stu-id="81cc3-220">Wi-Fi password</span></span>
   * <span data-ttu-id="81cc3-221">Cihaz bağlantı dizesi</span><span class="sxs-lookup"><span data-stu-id="81cc3-221">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="81cc3-222">Merhaba kimlik bilgileri hello yumuşatma HUZZAH ESP8266 EEPROM depolanır.</span><span class="sxs-lookup"><span data-stu-id="81cc3-222">hello credential information is stored in hello EEPROM of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="81cc3-223">Merhaba yumuşatma HUZZAH ESP8266 Panosu hello Sıfırla düğmesini tıklatın, Merhaba örnek uygulaması tooerase hello bilgi isteyip istemediğinizi sorar.</span><span class="sxs-lookup"><span data-stu-id="81cc3-223">If you click hello reset button on hello Feather HUZZAH ESP8266 board, hello sample application asks if you want tooerase hello information.</span></span> <span data-ttu-id="81cc3-224">Girin `Y` toohave hello bilgileri silinir.</span><span class="sxs-lookup"><span data-stu-id="81cc3-224">Enter `Y` toohave hello information erased.</span></span> <span data-ttu-id="81cc3-225">Tooprovide hello bilgi ikinci kez istenir.</span><span class="sxs-lookup"><span data-stu-id="81cc3-225">You are asked tooprovide hello information a second time.</span></span>

### <a name="verify-hello-sample-application-is-running-successfully"></a><span data-ttu-id="81cc3-226">Merhaba örnek uygulaması başarılı bir şekilde çalıştığını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="81cc3-226">Verify hello sample application is running successfully</span></span>

<span data-ttu-id="81cc3-227">Görürseniz hello seri İzleyicisi penceresinde hello şu çıktıları ve LED yumuşatma HUZZAH ESP8266, Merhaba örnek uygulaması üzerinde yanıp sönen hello başarılı bir şekilde çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="81cc3-227">If you see hello following output from hello serial monitor window and hello blinking LED on Feather HUZZAH ESP8266, hello sample application is running successfully.</span></span>

![Arduino IDE içinde son çıktı](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="81cc3-229">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="81cc3-229">Next steps</span></span>

<span data-ttu-id="81cc3-230">Başarıyla bir yumuşatma HUZZAH ESP8266 tooyour IOT hub'ı bağlı ve yakalanan hello algılayıcı verileri tooyour IOT hub gönderilen.</span><span class="sxs-lookup"><span data-stu-id="81cc3-230">You have successfully connected a Feather HUZZAH ESP8266 tooyour IoT hub, and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

