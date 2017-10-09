---
title: "aaaRaspberry Pi toocloud (Python) - bağlanmak Raspberry Pi'yi tooAzure IOT hub'ı | Microsoft Docs"
description: "Bilgi nasıl toosetup ve Bu öğreticide Raspberry Pi'yi toosend veri toohello Azure bulut platformu için Raspberry Pi'yi tooAzure IOT hub'ı bağlanın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure IOT Böğürtlenli Böğürtlenli pi pi IOT hub'ı Böğürtlenli pi gönderme veri toocloud, Böğürtlenli PI toocloud"
ms.service: iot-hub
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/31/2017
ms.author: xshi
ms.openlocfilehash: 86f5c91ab9dd4e23c563437827fb7d2d06916d2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-python"></a><span data-ttu-id="37e97-104">Raspberry Pi'yi tooAzure IOT hub'ı (Python) bağlanma</span><span class="sxs-lookup"><span data-stu-id="37e97-104">Connect Raspberry Pi tooAzure IoT Hub (Python)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="37e97-105">Bu öğreticide, Raspberry Pi'yi ile Raspbian çalıştıran çalışmanın hello temelleri öğrenerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="37e97-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="37e97-106">Daha sonra nasıl tooseamlessly bağlanacağını aygıtları toohello bulutunuzu kullanarak öğrenin [Azure IOT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="37e97-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="37e97-107">Windows 10 IOT Core örnekleri için toohello Git [Windows Geliştirme Merkezi](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="37e97-107">For Windows 10 IoT Core samples, go toohello [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="37e97-108">Bir pakete henüz yok mu?</span><span class="sxs-lookup"><span data-stu-id="37e97-108">Don't have a kit yet?</span></span> <span data-ttu-id="37e97-109">Deneyin [Raspberry Pi'yi çevrimiçi simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="37e97-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="37e97-110">Veya yeni bir paket satın [burada](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="37e97-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="37e97-111">Neler</span><span class="sxs-lookup"><span data-stu-id="37e97-111">What you do</span></span>

* <span data-ttu-id="37e97-112">IOT hub'ı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="37e97-112">Create an IoT hub.</span></span>
* <span data-ttu-id="37e97-113">Bir cihaz IOT hub'ınıza Pi için kaydetme.</span><span class="sxs-lookup"><span data-stu-id="37e97-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="37e97-114">Böğürtlenli PI kurulumu.</span><span class="sxs-lookup"><span data-stu-id="37e97-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="37e97-115">Pi toosend algılayıcı verileri tooyour IOT hub'ına bir örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="37e97-115">Run a sample application on Pi toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="37e97-116">Oluşturduğunuz Raspberry Pi'yi tooan IOT hub bağlayın.</span><span class="sxs-lookup"><span data-stu-id="37e97-116">Connect Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="37e97-117">Daha sonra örnek bir uygulama BME280 algılayıcının Pi toocollect sıcaklık ve nem veri üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="37e97-117">Then you run a sample application on Pi toocollect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="37e97-118">Son olarak, hello algılayıcı verileri tooyour IOT hub'ı gönderin.</span><span class="sxs-lookup"><span data-stu-id="37e97-118">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="37e97-119">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="37e97-119">What you learn</span></span>

* <span data-ttu-id="37e97-120">Nasıl toocreate Azure IOT hub'ı ve yeni cihaz bağlantı dizenizi alın.</span><span class="sxs-lookup"><span data-stu-id="37e97-120">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="37e97-121">Nasıl tooconnect ile BME280 algılayıcı Pi.</span><span class="sxs-lookup"><span data-stu-id="37e97-121">How tooconnect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="37e97-122">Nasıl Pi üzerinde bir örnek uygulamayı çalıştırarak toocollect algılayıcı verileri.</span><span class="sxs-lookup"><span data-stu-id="37e97-122">How toocollect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="37e97-123">Nasıl toosend algılayıcı verileri tooyour IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="37e97-123">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="37e97-124">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="37e97-124">What you need</span></span>

![Ne gerekiyor](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="37e97-126">Merhaba Raspberry Pi 2 veya Raspberry Pi 3 Panosu.</span><span class="sxs-lookup"><span data-stu-id="37e97-126">hello Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="37e97-127">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="37e97-127">An active Azure subscription.</span></span> <span data-ttu-id="37e97-128">Bir Azure hesabınız yoksa [ücretsiz Azure deneme hesabı oluşturma](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="37e97-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="37e97-129">Bir izleyici, bir USB klavye ve fare tooPi bağlanan.</span><span class="sxs-lookup"><span data-stu-id="37e97-129">A monitor, a USB keyboard, and mouse that connect tooPi.</span></span>
* <span data-ttu-id="37e97-130">Mac veya Windows veya Linux çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="37e97-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="37e97-131">Bir Internet bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="37e97-131">An Internet connection.</span></span>
* <span data-ttu-id="37e97-132">16 GB veya üzeri microSD kartı.</span><span class="sxs-lookup"><span data-stu-id="37e97-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="37e97-133">Bir USB SD bağdaştırıcı veya microSD kartı tooburn hello işletim sistemi görüntüsünü hello microSD kartı.</span><span class="sxs-lookup"><span data-stu-id="37e97-133">A USB-SD adapter or microSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="37e97-134">5-volt 2 amp güç hello 6 kaplama alanı mikro USB kablosu ile sağlayın.</span><span class="sxs-lookup"><span data-stu-id="37e97-134">A 5-volt 2-amp power supply with hello 6-foot micro USB cable.</span></span>

<span data-ttu-id="37e97-135">Aşağıdaki öğelerindeki hello isteğe bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="37e97-135">hello following items are optional:</span></span>

* <span data-ttu-id="37e97-136">Bir birleştirilmiş Adafruit BME280 sıcaklık, baskısı ve nem algılayıcı.</span><span class="sxs-lookup"><span data-stu-id="37e97-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="37e97-137">Bir breadboard.</span><span class="sxs-lookup"><span data-stu-id="37e97-137">A breadboard.</span></span>
* <span data-ttu-id="37e97-138">6 F/M anahtar kablolarını.</span><span class="sxs-lookup"><span data-stu-id="37e97-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="37e97-139">Yayılmış 10 mm LED.</span><span class="sxs-lookup"><span data-stu-id="37e97-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="37e97-140">Merhaba kod örnek desteği algılayıcı verilerini benzetimli çünkü bu öğeler isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="37e97-140">These items are optional because hello code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="set-up-raspberry-pi"></a><span data-ttu-id="37e97-141">Raspberry Pi'yi ayarlayın</span><span class="sxs-lookup"><span data-stu-id="37e97-141">Set up Raspberry Pi</span></span>

### <a name="install-hello-raspbian-operating-system-for-pi"></a><span data-ttu-id="37e97-142">Pi için Hello Raspbian işletim sistemini yükleme</span><span class="sxs-lookup"><span data-stu-id="37e97-142">Install hello Raspbian operating system for Pi</span></span>

<span data-ttu-id="37e97-143">Merhaba microSD kartı hello Raspbian görüntü yüklemesi için hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="37e97-143">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="37e97-144">Raspbian indirin.</span><span class="sxs-lookup"><span data-stu-id="37e97-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="37e97-145">[Masaüstü ile Raspbian Jessie karşıdan](https://www.raspberrypi.org/downloads/raspbian/) (Merhaba .zip dosyası).</span><span class="sxs-lookup"><span data-stu-id="37e97-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (hello .zip file).</span></span>
   1. <span data-ttu-id="37e97-146">Bilgisayarınızdaki Hello Raspbian görüntü tooa klasöre ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="37e97-146">Extract hello Raspbian image tooa folder on your computer.</span></span>
1. <span data-ttu-id="37e97-147">Raspbian toohello microSD kartı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="37e97-147">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="37e97-148">[Merhaba Etcher SD kart yazıcı yardımcı programı yükleyip](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="37e97-148">[Download and install hello Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="37e97-149">Etcher çalıştırın ve 1. adımda ayıkladığınız hello Raspbian görüntüsünü seçin.</span><span class="sxs-lookup"><span data-stu-id="37e97-149">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="37e97-150">Merhaba microSD kartı sürücü seçin.</span><span class="sxs-lookup"><span data-stu-id="37e97-150">Select hello microSD card drive.</span></span> <span data-ttu-id="37e97-151">Etcher zaten hello doğru sürücü seçmiş olabilirsiniz olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="37e97-151">Note that Etcher may have already selected hello correct drive.</span></span>
   1. <span data-ttu-id="37e97-152">Flash tooinstall Raspbian toohello microSD kartı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="37e97-152">Click Flash tooinstall Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="37e97-153">Yükleme tamamlandığında hello microSD kartı bilgisayarınızdan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="37e97-153">Remove hello microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="37e97-154">Etcher otomatik olarak çıkarır veya hello microSD kartı tamamlanmasından sonra çıkarır güvenli tooremove hello microSD kartı doğrudan demektir.</span><span class="sxs-lookup"><span data-stu-id="37e97-154">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   1. <span data-ttu-id="37e97-155">Merhaba microSD kartı Pi yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="37e97-155">Insert hello microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="37e97-156">SSH ve I2C etkinleştir</span><span class="sxs-lookup"><span data-stu-id="37e97-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="37e97-157">Pi toohello monitör, klavye ve fare bağlanmak, Pi başlatın ve ardından içinde Raspbian kullanarak oturum `pi` hello kullanıcı adı ve `raspberry` hello parola olarak.</span><span class="sxs-lookup"><span data-stu-id="37e97-157">Connect Pi toohello monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as hello user name and `raspberry` as hello password.</span></span>
1. <span data-ttu-id="37e97-158">Merhaba Böğürtlenli simgesine tıklayın > **Tercihler** > **Raspberry Pi yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="37e97-158">Click hello Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Merhaba Raspbian Tercihler menüsü](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="37e97-160">Merhaba üzerinde **arabirimleri** sekmesinde, ayarlamak **I2C** ve **SSH** çok**etkinleştirmek**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="37e97-160">On hello **Interfaces** tab, set **I2C** and **SSH** too**Enable**, and then click **OK**.</span></span> <span data-ttu-id="37e97-161">Fiziksel algılayıcılar varsa ve benzetimli toouse algılayıcı verilerini istediğiniz yok, bu adım isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="37e97-161">If you don't have physical sensors and want toouse simulated sensor data, this step is optional.</span></span>

   ![I2C ve Böğürtlenli Pi üzerinde SSH etkinleştir](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="37e97-163">tooenable SSH ve I2C bulabilirsiniz daha fazla başvuru belgeleri üzerinde [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) ve [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span><span class="sxs-lookup"><span data-stu-id="37e97-163">tooenable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-hello-sensor-toopi"></a><span data-ttu-id="37e97-164">Merhaba algılayıcı tooPi Bağlan</span><span class="sxs-lookup"><span data-stu-id="37e97-164">Connect hello sensor tooPi</span></span>

<span data-ttu-id="37e97-165">Merhaba breadboard ve anahtar kablolarını tooconnect bir LED ve BME280 tooPi aşağıdaki şekilde kullanın.</span><span class="sxs-lookup"><span data-stu-id="37e97-165">Use hello breadboard and jumper wires tooconnect an LED and a BME280 tooPi as follows.</span></span> <span data-ttu-id="37e97-166">Merhaba algılayıcı yoksa [Bu bölüm atlayın](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="37e97-166">If you don’t have hello sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![Merhaba Raspberry Pi'yi ve algılayıcı bağlantısı](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="37e97-168">Merhaba BME280 algılayıcı sıcaklık ve nem verileri toplayabilir.</span><span class="sxs-lookup"><span data-stu-id="37e97-168">hello BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="37e97-169">Ve cihaz ve hello bulut arasındaki iletişimi ise hello LED blink.</span><span class="sxs-lookup"><span data-stu-id="37e97-169">And hello LED will blink if there is a communication between device and hello cloud.</span></span> 

<span data-ttu-id="37e97-170">Algılayıcı PIN'ler için kablolama aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="37e97-170">For sensor pins, use hello following wiring:</span></span>

| <span data-ttu-id="37e97-171">Başlangıç (algılayıcı & LED)</span><span class="sxs-lookup"><span data-stu-id="37e97-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="37e97-172">Bitiş (kartı)</span><span class="sxs-lookup"><span data-stu-id="37e97-172">End (Board)</span></span>            | <span data-ttu-id="37e97-173">Kablo rengi</span><span class="sxs-lookup"><span data-stu-id="37e97-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="37e97-174">VDD (PIN 5G)</span><span class="sxs-lookup"><span data-stu-id="37e97-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="37e97-175">3, 3v PWR (PIN 1)</span><span class="sxs-lookup"><span data-stu-id="37e97-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="37e97-176">Beyaz kablosu</span><span class="sxs-lookup"><span data-stu-id="37e97-176">White cable</span></span>   |
| <span data-ttu-id="37e97-177">GND (PIN 7G)</span><span class="sxs-lookup"><span data-stu-id="37e97-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="37e97-178">GND (PIN 6)</span><span class="sxs-lookup"><span data-stu-id="37e97-178">GND (Pin 6)</span></span>            | <span data-ttu-id="37e97-179">Kahverengi kablosu</span><span class="sxs-lookup"><span data-stu-id="37e97-179">Brown cable</span></span>   |
| <span data-ttu-id="37e97-180">SDI (PIN 10G)</span><span class="sxs-lookup"><span data-stu-id="37e97-180">SDI (Pin 10G)</span></span>            | <span data-ttu-id="37e97-181">I2C1 SDA (PIN 3)</span><span class="sxs-lookup"><span data-stu-id="37e97-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="37e97-182">Kırmızı kablosu</span><span class="sxs-lookup"><span data-stu-id="37e97-182">Red cable</span></span>     |
| <span data-ttu-id="37e97-183">SCK (PIN 8G)</span><span class="sxs-lookup"><span data-stu-id="37e97-183">SCK (Pin 8G)</span></span>             | <span data-ttu-id="37e97-184">I2C1 SCL (PIN 5)</span><span class="sxs-lookup"><span data-stu-id="37e97-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="37e97-185">Turuncu kablosu</span><span class="sxs-lookup"><span data-stu-id="37e97-185">Orange cable</span></span>  |
| <span data-ttu-id="37e97-186">LED VDD (PIN 18F)</span><span class="sxs-lookup"><span data-stu-id="37e97-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="37e97-187">GPIO'yu 24 (PIN 18)</span><span class="sxs-lookup"><span data-stu-id="37e97-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="37e97-188">Beyaz kablosu</span><span class="sxs-lookup"><span data-stu-id="37e97-188">White cable</span></span>   |
| <span data-ttu-id="37e97-189">LED GND (PIN 17F)</span><span class="sxs-lookup"><span data-stu-id="37e97-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="37e97-190">GND (PIN 20)</span><span class="sxs-lookup"><span data-stu-id="37e97-190">GND (Pin 20)</span></span>           | <span data-ttu-id="37e97-191">Siyah kablosu</span><span class="sxs-lookup"><span data-stu-id="37e97-191">Black cable</span></span>   |

<span data-ttu-id="37e97-192">Tooview tıklatın [Raspberry Pi 2 ve 3 PIN eşlemeleri](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) daha sonra başvurmak üzere.</span><span class="sxs-lookup"><span data-stu-id="37e97-192">Click tooview [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="37e97-193">BME280 tooyour Raspberry Pi'yi başarıyla bağlandıktan sonra görüntü gibi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="37e97-193">After you've successfully connected BME280 tooyour Raspberry Pi, it should be like below image.</span></span>

![Bağlı Pi ve BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a><span data-ttu-id="37e97-195">Pi toohello ağa bağlan</span><span class="sxs-lookup"><span data-stu-id="37e97-195">Connect Pi toohello network</span></span>

<span data-ttu-id="37e97-196">Pi üzerinde hello mikro USB kablosu ve hello güç kaynağı kullanarak açın.</span><span class="sxs-lookup"><span data-stu-id="37e97-196">Turn on Pi by using hello micro USB cable and hello power supply.</span></span> <span data-ttu-id="37e97-197">Kullanım hello Ethernet kablo tooconnect PI tooyour kablolu ağ veya hello izleyin [hello Raspberry Pi Foundation yönergeleri](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect PI tooyour kablosuz ağ.</span><span class="sxs-lookup"><span data-stu-id="37e97-197">Use hello Ethernet cable tooconnect Pi tooyour wired network or follow hello [instructions from hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="37e97-198">Pi başarıyla bağlı toohello ağ sağlandıktan sonra tootake hello Not gereksinim [IP adresi, pi'nin](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="37e97-198">After your Pi has been successfully connected toohello network, you need tootake a note of hello [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Bağlı toowired ağ](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="37e97-200">Pi bağlı toohello aynı bilgisayarınızda olarak ağ olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="37e97-200">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="37e97-201">Pi kablolu ağ bağlantılı tooa olsa da, bilgisayarınız bağlı tooa kablosuz ağ ise, örneğin, size hello IP göremeyebilirsiniz hello devdisco çıkış adresi.</span><span class="sxs-lookup"><span data-stu-id="37e97-201">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="37e97-202">Pi üzerinde bir örnek uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="37e97-202">Run a sample application on Pi</span></span>

### <a name="install-hello-prerequisite-packages"></a><span data-ttu-id="37e97-203">Merhaba önkoşul yükleyin</span><span class="sxs-lookup"><span data-stu-id="37e97-203">Install hello prerequisite packages</span></span>

<span data-ttu-id="37e97-204">SSH istemcilerini, ana bilgisayar tooconnect tooyour Raspberry Pi'yi aşağıdaki hello birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="37e97-204">Use one of hello following SSH clients from your host computer tooconnect tooyour Raspberry Pi.</span></span>
   
   <span data-ttu-id="37e97-205">**Windows kullanıcıları**</span><span class="sxs-lookup"><span data-stu-id="37e97-205">**Windows Users**</span></span>
   1. <span data-ttu-id="37e97-206">İndirme ve yükleme [PuTTY](http://www.putty.org/) Windows için.</span><span class="sxs-lookup"><span data-stu-id="37e97-206">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="37e97-207">Pi hello ana bilgisayar adı (veya IP adresi) içine bölümünüzü Hello IP adresini kopyalayın ve SSH hello bağlantı türü olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="37e97-207">Copy hello IP address of your Pi into hello Host name (or IP address) section and select SSH as hello connection type.</span></span>
   
   
   <span data-ttu-id="37e97-208">**Mac ve Ubuntu kullanıcılar**</span><span class="sxs-lookup"><span data-stu-id="37e97-208">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="37e97-209">Ubuntu veya macOS Hello yerleşik SSH İstemcisi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="37e97-209">Use hello built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="37e97-210">Toorun gerekebilecek `ssh pi@<ip address of pi>` tooconnect Pi SSH aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="37e97-210">You might need toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="37e97-211">Merhaba varsayılan kullanıcı adı `pi` , ve hello parola `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="37e97-211">hello default username is `pi` , and hello password is `raspberry`.</span></span>


### <a name="configure-hello-sample-application"></a><span data-ttu-id="37e97-212">Merhaba örnek uygulamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="37e97-212">Configure hello sample application</span></span>

1. <span data-ttu-id="37e97-213">Merhaba örnek uygulaması hello aşağıdaki komutu çalıştırarak kopyalama:</span><span class="sxs-lookup"><span data-stu-id="37e97-213">Clone hello sample application by running hello following command:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-python-raspberrypi-client-app.git
   ```
1. <span data-ttu-id="37e97-214">Merhaba yapılandırma dosyası hello aşağıdaki komutları çalıştırarak açın:</span><span class="sxs-lookup"><span data-stu-id="37e97-214">Open hello config file by running hello following commands:</span></span>

   ```bash
   cd iot-hub-python-raspberrypi-client-app
   nano config.py
   ```

   <span data-ttu-id="37e97-215">5 makroları vardır bu dosyada configurate olabilir.</span><span class="sxs-lookup"><span data-stu-id="37e97-215">There are 5 macros in this file you can configurate.</span></span> <span data-ttu-id="37e97-216">Merhaba ilk biridir `MESSAGE_TIMESPAN`, toocloud Gönder arasında iki iletileri hello zaman aralığı (milisaniye cinsinden) tanımlar.</span><span class="sxs-lookup"><span data-stu-id="37e97-216">hello first one is `MESSAGE_TIMESPAN`, which defines hello time interval (in milliseconds) between two messages that send toocloud.</span></span> <span data-ttu-id="37e97-217">İkinci bir hello `SIMULATED_DATA`, veya toouse algılayıcı verilerini olup benzetimi için bir Boole değeri değil.</span><span class="sxs-lookup"><span data-stu-id="37e97-217">hello second one `SIMULATED_DATA`, which is a Boolean value for whether toouse simulated sensor data or not.</span></span> <span data-ttu-id="37e97-218">`I2C_ADDRESS`BME280 algılayıcı bağlı hello I2C adresidir.</span><span class="sxs-lookup"><span data-stu-id="37e97-218">`I2C_ADDRESS` is hello I2C address which your BME280 sensor is connected.</span></span> <span data-ttu-id="37e97-219">`GPIO_PIN_ADDRESS`Merhaba GPIO'yu için LED adresidir.</span><span class="sxs-lookup"><span data-stu-id="37e97-219">`GPIO_PIN_ADDRESS` is hello GPIO address for your LED.</span></span> <span data-ttu-id="37e97-220">Merhaba son biridir `BLINK_TIMESPAN`, milisaniye cinsinden, LED açıldığında hello timespan tanımlı.</span><span class="sxs-lookup"><span data-stu-id="37e97-220">hello last one is `BLINK_TIMESPAN`, which defined hello timespan when your LED is turned on in milliseconds.</span></span>

   <span data-ttu-id="37e97-221">Varsa, **hello algılayıcı yok**ayarlayın hello `SIMULATED_DATA` çok değer`True` toomake Merhaba örnek uygulaması oluşturup benzetimli algılayıcı verilerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37e97-221">If you **don't have hello sensor**, set hello `SIMULATED_DATA` value too`True` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="37e97-222">Kaydedip çıkmak denetimi O tuşlarına basarak > Enter > Denetim X.</span><span class="sxs-lookup"><span data-stu-id="37e97-222">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-hello-sample-application"></a><span data-ttu-id="37e97-223">Derleme ve hello örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="37e97-223">Build and run hello sample application</span></span>

1. <span data-ttu-id="37e97-224">Merhaba aşağıdaki komutu çalıştırarak Merhaba örnek uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="37e97-224">Build hello sample application by running hello following command.</span></span> <span data-ttu-id="37e97-225">Merhaba Python için Azure IOT SDK'ları sarmalayıcıları hello Azure IOT cihaz C SDK'sı üzerinde olduğundan, istediğiniz veya kaynak kodu toogenerate hello Python kitaplıklarından ihtiyacınız varsa toocompile hello C kitaplıkları gerekir.</span><span class="sxs-lookup"><span data-stu-id="37e97-225">Because hello Azure IoT SDKs for Python are wrappers on top of hello Azure IoT Device C SDK, you will need toocompile hello C libraries if you want or need toogenerate hello Python libraries from source code.</span></span>

   ```bash
   sudo chmod u+x setup.sh
   sudo ./setup.sh
   ```
   > [!NOTE] 
   <span data-ttu-id="37e97-226">İstediğiniz çalıştırarak hello sürümü de belirleyebilirsiniz `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span><span class="sxs-lookup"><span data-stu-id="37e97-226">You can also specify hello version you want by running `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span></span> <span data-ttu-id="37e97-227">Betik parametresi olmadan çalıştırırsanız, hello betik yüklü python hello sürümünü otomatik olarak algılar (arama sırasını 2.7 -> 3.4 3.5 ->).</span><span class="sxs-lookup"><span data-stu-id="37e97-227">If you run script without parameter, hello script will automatically detect hello version of python installed (Search sequence 2.7->3.4->3.5).</span></span> <span data-ttu-id="37e97-228">Oluşturma ve çalıştırma sırasında Python sürümünüzü tutarlı tutar emin olun.</span><span class="sxs-lookup"><span data-stu-id="37e97-228">Make sure your Python version keeps consistent during building and running.</span></span> 
   
   > [!NOTE] 
   <span data-ttu-id="37e97-229">Daha az en az 1 GB RAM içeren Linux cihazlarda oluşturma Hello Python istemci kitaplığına (iothub_client.so) görebilirsiniz %98 aşağıda gösterildiği gibi iothub_client_python.cpp oluşturulurken takılmış derleme `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span><span class="sxs-lookup"><span data-stu-id="37e97-229">On building hello Python client library (iothub_client.so) on Linux devices that have less than 1GB RAM, you may see build getting stuck at 98% while building iothub_client_python.cpp as shown below `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span></span> <span data-ttu-id="37e97-230">Bu sorunu yaşayıp çalıştırırsanız, cihaz hello kullanmanın hello bellek tüketimi denetleyin `free -m command` bu süre boyunca başka bir terminal penceresi içinde.</span><span class="sxs-lookup"><span data-stu-id="37e97-230">If you run into this issue, check hello memory consumption of hello device using `free -m command` in another terminal window during that time.</span></span> <span data-ttu-id="37e97-231">Bellek yetersiz iothub_client_python.cpp dosyası derlenirken çalıştırıyorsanız hello takas alanı tooget artırmak tootemporarily olabilir daha fazla kullanılabilir bellek toosuccessfully yapı hello Python istemci-tarafı cihaz SDK'sı kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="37e97-231">If you are running out of memory while compiling iothub_client_python.cpp file, you may have tootemporarily increase hello swap space tooget more available memory toosuccessfully build hello Python client-side device SDK library.</span></span>
   
1. <span data-ttu-id="37e97-232">Merhaba aşağıdaki komutu çalıştırarak Hello örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="37e97-232">Run hello sample application by running hello following command:</span></span>

   ```bash
   python app.py '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="37e97-233">Kopyalama hello cihaz bağlantı dizesi hello tek tırnak yapıştırma emin olun.</span><span class="sxs-lookup"><span data-stu-id="37e97-233">Make sure you copy-paste hello device connection string into hello single quotes.</span></span> <span data-ttu-id="37e97-234">Ve hello python 3 kullandığınız sonra kullanabileceğiniz hello komutu `python3 app.py '<your Azure IoT hub device connection string>'`.</span><span class="sxs-lookup"><span data-stu-id="37e97-234">And if you use hello python 3, then you can use hello command `python3 app.py '<your Azure IoT hub device connection string>'`.</span></span>


   <span data-ttu-id="37e97-235">Gösterir tooyour IOT hub gönderilen algılayıcı verileri ve hello iletileri hello hello aşağıdaki çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="37e97-235">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

   ![Çıktı - Raspberry Pi'yi tooyour IOT hub'ından gönderilen algılayıcı verileri](media/iot-hub-raspberry-pi-kit-c-get-started/success.png
)

## <a name="next-steps"></a><span data-ttu-id="37e97-237">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="37e97-237">Next steps</span></span>

<span data-ttu-id="37e97-238">Bir örnek uygulama toocollect algılayıcı verilerini çalıştırdıktan ve tooyour IOT hub'ı gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37e97-238">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span> <span data-ttu-id="37e97-239">bkz: Merhaba Raspberry Pi'yi tooyour IOT hub'ı veya gönderme iletileri tooyour Raspberry Pi'yi bir komut satırı arabirimi gönderdiğini toosee hello iletileri [iothub-explorer eğitici Mesajlaşma Yönet bulut cihaz](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="37e97-239">toosee hello messages that your Raspberry Pi has sent tooyour IoT hub or send messages tooyour Raspberry Pi in a command line interface, see hello [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
