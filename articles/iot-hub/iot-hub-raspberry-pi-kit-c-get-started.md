---
title: "aaaRaspberry Pi toocloud (C) - bağlanmak Raspberry Pi'yi tooAzure IOT hub'ı | Microsoft Docs"
description: "Bilgi nasıl toosetup ve Bu öğreticide Raspberry Pi'yi toosend veri toohello Azure bulut platformu için Raspberry Pi'yi tooAzure IOT hub'ı bağlanın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure IOT Böğürtlenli Böğürtlenli pi pi IOT hub'ı Böğürtlenli pi gönderme veri toocloud, Böğürtlenli PI toocloud"
ms.assetid: 68c0e730-1dc8-4e26-ac6b-573b217b302d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/12/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 05086890458e196d7fdc87a53fcabb9386245d6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-c"></a><span data-ttu-id="ba431-104">Raspberry Pi'yi tooAzure IoT Hub (C) Bağlan</span><span class="sxs-lookup"><span data-stu-id="ba431-104">Connect Raspberry Pi tooAzure IoT Hub (C)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="ba431-105">Bu öğreticide, Raspberry Pi'yi ile Raspbian çalıştıran çalışmanın hello temelleri öğrenerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="ba431-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="ba431-106">Daha sonra nasıl tooseamlessly bağlanacağını aygıtları toohello bulutunuzu kullanarak öğrenin [Azure IOT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="ba431-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="ba431-107">Windows 10 IOT Core örnekleri için toohello Git [Windows Geliştirme Merkezi](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="ba431-107">For Windows 10 IoT Core samples, go toohello [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="ba431-108">Bir pakete henüz yok mu?</span><span class="sxs-lookup"><span data-stu-id="ba431-108">Don't have a kit yet?</span></span> <span data-ttu-id="ba431-109">Deneyin [Raspberry Pi'yi çevrimiçi simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ba431-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="ba431-110">Veya yeni bir paket satın [burada](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="ba431-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="ba431-111">Neler</span><span class="sxs-lookup"><span data-stu-id="ba431-111">What you do</span></span>

* <span data-ttu-id="ba431-112">IOT hub'ı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ba431-112">Create an IoT hub.</span></span>
* <span data-ttu-id="ba431-113">Bir cihaz IOT hub'ınıza Pi için kaydetme.</span><span class="sxs-lookup"><span data-stu-id="ba431-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="ba431-114">Böğürtlenli PI kurulumu.</span><span class="sxs-lookup"><span data-stu-id="ba431-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="ba431-115">Pi toosend algılayıcı verileri tooyour IOT hub'ına bir örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ba431-115">Run a sample application on Pi toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="ba431-116">Oluşturduğunuz Raspberry Pi'yi tooan IOT hub bağlayın.</span><span class="sxs-lookup"><span data-stu-id="ba431-116">Connect Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="ba431-117">Daha sonra örnek bir uygulama BME280 algılayıcının Pi toocollect sıcaklık ve nem veri üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ba431-117">Then you run a sample application on Pi toocollect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="ba431-118">Son olarak, hello algılayıcı verileri tooyour IOT hub'ı gönderin.</span><span class="sxs-lookup"><span data-stu-id="ba431-118">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="ba431-119">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="ba431-119">What you learn</span></span>

* <span data-ttu-id="ba431-120">Nasıl toocreate Azure IOT hub'ı ve yeni cihaz bağlantı dizenizi alın.</span><span class="sxs-lookup"><span data-stu-id="ba431-120">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="ba431-121">Nasıl tooconnect ile BME280 algılayıcı Pi.</span><span class="sxs-lookup"><span data-stu-id="ba431-121">How tooconnect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="ba431-122">Nasıl Pi üzerinde bir örnek uygulamayı çalıştırarak toocollect algılayıcı verileri.</span><span class="sxs-lookup"><span data-stu-id="ba431-122">How toocollect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="ba431-123">Nasıl toosend algılayıcı verileri tooyour IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="ba431-123">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ba431-124">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="ba431-124">What you need</span></span>

![Ne gerekiyor](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="ba431-126">Merhaba Raspberry Pi 2 veya Raspberry Pi 3 Panosu.</span><span class="sxs-lookup"><span data-stu-id="ba431-126">hello Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="ba431-127">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="ba431-127">An active Azure subscription.</span></span> <span data-ttu-id="ba431-128">Bir Azure hesabınız yoksa [ücretsiz Azure deneme hesabı oluşturma](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="ba431-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="ba431-129">Bir izleyici, bir USB klavye ve fare tooPi bağlanan.</span><span class="sxs-lookup"><span data-stu-id="ba431-129">A monitor, a USB keyboard, and mouse that connect tooPi.</span></span>
* <span data-ttu-id="ba431-130">Mac veya Windows veya Linux çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="ba431-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="ba431-131">Bir Internet bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="ba431-131">An Internet connection.</span></span>
* <span data-ttu-id="ba431-132">16 GB veya üzeri microSD kartı.</span><span class="sxs-lookup"><span data-stu-id="ba431-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="ba431-133">Bir USB SD bağdaştırıcı veya microSD kartı tooburn hello işletim sistemi görüntüsünü hello microSD kartı.</span><span class="sxs-lookup"><span data-stu-id="ba431-133">A USB-SD adapter or microSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="ba431-134">5-volt 2 amp güç hello 6 kaplama alanı mikro USB kablosu ile sağlayın.</span><span class="sxs-lookup"><span data-stu-id="ba431-134">A 5-volt 2-amp power supply with hello 6-foot micro USB cable.</span></span>

<span data-ttu-id="ba431-135">Aşağıdaki öğelerindeki hello isteğe bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="ba431-135">hello following items are optional:</span></span>

* <span data-ttu-id="ba431-136">Bir birleştirilmiş Adafruit BME280 sıcaklık, baskısı ve nem algılayıcı.</span><span class="sxs-lookup"><span data-stu-id="ba431-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="ba431-137">Bir breadboard.</span><span class="sxs-lookup"><span data-stu-id="ba431-137">A breadboard.</span></span>
* <span data-ttu-id="ba431-138">6 F/M anahtar kablolarını.</span><span class="sxs-lookup"><span data-stu-id="ba431-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="ba431-139">Yayılmış 10 mm LED.</span><span class="sxs-lookup"><span data-stu-id="ba431-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="ba431-140">Merhaba kod örnek desteği algılayıcı verilerini benzetimli çünkü bu öğeler isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="ba431-140">These items are optional because hello code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="ba431-141">Böğürtlenli PI Kurulumu</span><span class="sxs-lookup"><span data-stu-id="ba431-141">Setup Raspberry Pi</span></span>

### <a name="install-hello-raspbian-operating-system-for-pi"></a><span data-ttu-id="ba431-142">Pi için Hello Raspbian işletim sistemini yükleme</span><span class="sxs-lookup"><span data-stu-id="ba431-142">Install hello Raspbian operating system for Pi</span></span>

<span data-ttu-id="ba431-143">Merhaba microSD kartı hello Raspbian görüntü yüklemesi için hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="ba431-143">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="ba431-144">Raspbian indirin.</span><span class="sxs-lookup"><span data-stu-id="ba431-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="ba431-145">[Masaüstü ile Raspbian Jessie karşıdan](https://www.raspberrypi.org/downloads/raspbian/) (Merhaba .zip dosyası).</span><span class="sxs-lookup"><span data-stu-id="ba431-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (hello .zip file).</span></span>
   1. <span data-ttu-id="ba431-146">Bilgisayarınızdaki Hello Raspbian görüntü tooa klasöre ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="ba431-146">Extract hello Raspbian image tooa folder on your computer.</span></span>
1. <span data-ttu-id="ba431-147">Raspbian toohello microSD kartı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ba431-147">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="ba431-148">[Merhaba Etcher SD kart yazıcı yardımcı programı yükleyip](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="ba431-148">[Download and install hello Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="ba431-149">Etcher çalıştırın ve 1. adımda ayıkladığınız hello Raspbian görüntüsünü seçin.</span><span class="sxs-lookup"><span data-stu-id="ba431-149">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="ba431-150">Merhaba microSD kartı sürücü seçin.</span><span class="sxs-lookup"><span data-stu-id="ba431-150">Select hello microSD card drive.</span></span> <span data-ttu-id="ba431-151">Etcher zaten hello doğru sürücü seçmiş olabilirsiniz olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ba431-151">Note that Etcher may have already selected hello correct drive.</span></span>
   1. <span data-ttu-id="ba431-152">Flash tooinstall Raspbian toohello microSD kartı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ba431-152">Click Flash tooinstall Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="ba431-153">Yükleme tamamlandığında hello microSD kartı bilgisayarınızdan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="ba431-153">Remove hello microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="ba431-154">Etcher otomatik olarak çıkarır veya hello microSD kartı tamamlanmasından sonra çıkarır güvenli tooremove hello microSD kartı doğrudan demektir.</span><span class="sxs-lookup"><span data-stu-id="ba431-154">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   1. <span data-ttu-id="ba431-155">Merhaba microSD kartı Pi yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="ba431-155">Insert hello microSD card into Pi.</span></span>

### <a name="enable-ssh-and-spi"></a><span data-ttu-id="ba431-156">SSH ve SPI etkinleştir</span><span class="sxs-lookup"><span data-stu-id="ba431-156">Enable SSH and SPI</span></span>

1. <span data-ttu-id="ba431-157">Pi toohello monitör, klavye ve fare bağlanmak, Pi başlatın ve ardından içinde Raspbian kullanarak oturum `pi` hello kullanıcı adı ve `raspberry` hello parola olarak.</span><span class="sxs-lookup"><span data-stu-id="ba431-157">Connect Pi toohello monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as hello user name and `raspberry` as hello password.</span></span>
1. <span data-ttu-id="ba431-158">Merhaba Böğürtlenli simgesine tıklayın > **Tercihler** > **Raspberry Pi yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="ba431-158">Click hello Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Merhaba Raspbian Tercihler menüsü](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="ba431-160">Merhaba üzerinde **arabirimleri** sekmesinde, ayarlamak **SPI** ve **SSH** çok**etkinleştirmek**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="ba431-160">On hello **Interfaces** tab, set **SPI** and **SSH** too**Enable**, and then click **OK**.</span></span> <span data-ttu-id="ba431-161">Fiziksel algılayıcılar varsa ve benzetimli toouse algılayıcı verilerini istediğiniz yok, bu adım isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="ba431-161">If you don't have physical sensors and want toouse simulated sensor data, this step is optional.</span></span>

   ![SPI ve Böğürtlenli Pi üzerinde SSH etkinleştir](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="ba431-163">tooenable SSH ve SPI bulabilirsiniz daha fazla başvuru belgeleri üzerinde [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) ve [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span><span class="sxs-lookup"><span data-stu-id="ba431-163">tooenable SSH and SPI, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-hello-sensor-toopi"></a><span data-ttu-id="ba431-164">Merhaba algılayıcı tooPi Bağlan</span><span class="sxs-lookup"><span data-stu-id="ba431-164">Connect hello sensor tooPi</span></span>

<span data-ttu-id="ba431-165">Merhaba breadboard ve anahtar kablolarını tooconnect bir LED ve BME280 tooPi aşağıdaki şekilde kullanın.</span><span class="sxs-lookup"><span data-stu-id="ba431-165">Use hello breadboard and jumper wires tooconnect an LED and a BME280 tooPi as follows.</span></span> <span data-ttu-id="ba431-166">Merhaba algılayıcı yoksa [Bu bölüm atlayın](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="ba431-166">If you don’t have hello sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![Merhaba Raspberry Pi'yi ve algılayıcı bağlantısı](media/iot-hub-raspberry-pi-kit-c-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="ba431-168">Merhaba BME280 algılayıcı sıcaklık ve nem verileri toplayabilir.</span><span class="sxs-lookup"><span data-stu-id="ba431-168">hello BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="ba431-169">Ve cihaz ve hello bulut arasındaki iletişimi ise hello LED blink.</span><span class="sxs-lookup"><span data-stu-id="ba431-169">And hello LED will blink if there is a communication between device and hello cloud.</span></span> 

<span data-ttu-id="ba431-170">Algılayıcı PIN'ler için kablolama aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="ba431-170">For sensor pins, use hello following wiring:</span></span>

| <span data-ttu-id="ba431-171">Başlangıç (algılayıcı & LED)</span><span class="sxs-lookup"><span data-stu-id="ba431-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="ba431-172">Bitiş (kartı)</span><span class="sxs-lookup"><span data-stu-id="ba431-172">End (Board)</span></span>            | <span data-ttu-id="ba431-173">Kablo rengi</span><span class="sxs-lookup"><span data-stu-id="ba431-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="ba431-174">LED VDD (PIN 5G)</span><span class="sxs-lookup"><span data-stu-id="ba431-174">LED VDD (Pin 5G)</span></span>         | <span data-ttu-id="ba431-175">GPIO'yu 4 (PIN 7)</span><span class="sxs-lookup"><span data-stu-id="ba431-175">GPIO 4 (Pin 7)</span></span>         | <span data-ttu-id="ba431-176">Beyaz kablosu</span><span class="sxs-lookup"><span data-stu-id="ba431-176">White cable</span></span>   |
| <span data-ttu-id="ba431-177">LED GND (PIN 6G)</span><span class="sxs-lookup"><span data-stu-id="ba431-177">LED GND (Pin 6G)</span></span>         | <span data-ttu-id="ba431-178">GND (PIN 6)</span><span class="sxs-lookup"><span data-stu-id="ba431-178">GND (Pin 6)</span></span>            | <span data-ttu-id="ba431-179">Siyah kablosu</span><span class="sxs-lookup"><span data-stu-id="ba431-179">Black cable</span></span>   |
| <span data-ttu-id="ba431-180">VDD (PIN 18F)</span><span class="sxs-lookup"><span data-stu-id="ba431-180">VDD (Pin 18F)</span></span>            | <span data-ttu-id="ba431-181">3, 3v PWR (PIN 17)</span><span class="sxs-lookup"><span data-stu-id="ba431-181">3.3V PWR (Pin 17)</span></span>      | <span data-ttu-id="ba431-182">Beyaz kablosu</span><span class="sxs-lookup"><span data-stu-id="ba431-182">White cable</span></span>   |
| <span data-ttu-id="ba431-183">GND (PIN 20F)</span><span class="sxs-lookup"><span data-stu-id="ba431-183">GND (Pin 20F)</span></span>            | <span data-ttu-id="ba431-184">GND (PIN 20)</span><span class="sxs-lookup"><span data-stu-id="ba431-184">GND (Pin 20)</span></span>           | <span data-ttu-id="ba431-185">Siyah kablosu</span><span class="sxs-lookup"><span data-stu-id="ba431-185">Black cable</span></span>   |
| <span data-ttu-id="ba431-186">SCK (PIN 21F)</span><span class="sxs-lookup"><span data-stu-id="ba431-186">SCK (Pin 21F)</span></span>            | <span data-ttu-id="ba431-187">SPI0 SCLK (PIN 23)</span><span class="sxs-lookup"><span data-stu-id="ba431-187">SPI0 SCLK (Pin 23)</span></span>     | <span data-ttu-id="ba431-188">Turuncu kablosu</span><span class="sxs-lookup"><span data-stu-id="ba431-188">Orange cable</span></span>  |
| <span data-ttu-id="ba431-189">SDO (PIN 22F)</span><span class="sxs-lookup"><span data-stu-id="ba431-189">SDO (Pin 22F)</span></span>            | <span data-ttu-id="ba431-190">SPI0 MISO (PIN 21)</span><span class="sxs-lookup"><span data-stu-id="ba431-190">SPI0 MISO (Pin 21)</span></span>     | <span data-ttu-id="ba431-191">Sarı kablosu</span><span class="sxs-lookup"><span data-stu-id="ba431-191">Yellow cable</span></span>  |
| <span data-ttu-id="ba431-192">SDI (PIN 23F)</span><span class="sxs-lookup"><span data-stu-id="ba431-192">SDI (Pin 23F)</span></span>            | <span data-ttu-id="ba431-193">SPI0 MOSI (PIN 19)</span><span class="sxs-lookup"><span data-stu-id="ba431-193">SPI0 MOSI (Pin 19)</span></span>     | <span data-ttu-id="ba431-194">Yeşil kablosu</span><span class="sxs-lookup"><span data-stu-id="ba431-194">Green cable</span></span>   |
| <span data-ttu-id="ba431-195">CS (PIN 24F)</span><span class="sxs-lookup"><span data-stu-id="ba431-195">CS (Pin 24F)</span></span>             | <span data-ttu-id="ba431-196">SPI0 CS (PIN 24)</span><span class="sxs-lookup"><span data-stu-id="ba431-196">SPI0 CS (Pin 24)</span></span>       | <span data-ttu-id="ba431-197">Mavi kablosu</span><span class="sxs-lookup"><span data-stu-id="ba431-197">Blue cable</span></span>    |

<span data-ttu-id="ba431-198">Tooview tıklatın [Raspberry Pi 2 ve 3 PIN eşlemeleri](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) daha sonra başvurmak üzere.</span><span class="sxs-lookup"><span data-stu-id="ba431-198">Click tooview [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="ba431-199">BME280 tooyour Raspberry Pi'yi başarıyla bağlandıktan sonra görüntü gibi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ba431-199">After you've successfully connected BME280 tooyour Raspberry Pi, it should be like below image.</span></span>

![Bağlı Pi ve BME280](media/iot-hub-raspberry-pi-kit-c-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a><span data-ttu-id="ba431-201">Pi toohello ağa bağlan</span><span class="sxs-lookup"><span data-stu-id="ba431-201">Connect Pi toohello network</span></span>

<span data-ttu-id="ba431-202">Pi üzerinde hello mikro USB kablosu ve hello güç kaynağı kullanarak açın.</span><span class="sxs-lookup"><span data-stu-id="ba431-202">Turn on Pi by using hello micro USB cable and hello power supply.</span></span> <span data-ttu-id="ba431-203">Kullanım hello Ethernet kablo tooconnect PI tooyour kablolu ağ veya hello izleyin [hello Raspberry Pi Foundation yönergeleri](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect PI tooyour kablosuz ağ.</span><span class="sxs-lookup"><span data-stu-id="ba431-203">Use hello Ethernet cable tooconnect Pi tooyour wired network or follow hello [instructions from hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="ba431-204">Pi başarıyla bağlı toohello ağ sağlandıktan sonra tootake hello Not gereksinim [IP adresi, pi'nin](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="ba431-204">After your Pi has been successfully connected toohello network, you need tootake a note of hello [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Bağlı toowired ağ](media/iot-hub-raspberry-pi-kit-c-get-started/5_power-on-pi.jpg)


## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="ba431-206">Pi üzerinde bir örnek uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="ba431-206">Run a sample application on Pi</span></span>

### <a name="install-hello-prerequisite-packages"></a><span data-ttu-id="ba431-207">Merhaba önkoşul yükleyin</span><span class="sxs-lookup"><span data-stu-id="ba431-207">Install hello prerequisite packages</span></span>

1. <span data-ttu-id="ba431-208">SSH istemcilerini, ana bilgisayar tooconnect tooyour Raspberry Pi'yi aşağıdaki hello birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="ba431-208">Use one of hello following SSH clients from your host computer tooconnect tooyour Raspberry Pi.</span></span>
   
   <span data-ttu-id="ba431-209">**Windows kullanıcıları**</span><span class="sxs-lookup"><span data-stu-id="ba431-209">**Windows Users**</span></span>
   1. <span data-ttu-id="ba431-210">İndirme ve yükleme [PuTTY](http://www.putty.org/) Windows için.</span><span class="sxs-lookup"><span data-stu-id="ba431-210">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="ba431-211">Pi hello ana bilgisayar adı (veya IP adresi) içine bölümünüzü Hello IP adresini kopyalayın ve SSH hello bağlantı türü olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="ba431-211">Copy hello IP address of your Pi into hello Host name (or IP address) section and select SSH as hello connection type.</span></span>
   
   ![PuTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   <span data-ttu-id="ba431-213">**Mac ve Ubuntu kullanıcılar**</span><span class="sxs-lookup"><span data-stu-id="ba431-213">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="ba431-214">Ubuntu veya macOS Hello yerleşik SSH İstemcisi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="ba431-214">Use hello built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="ba431-215">Toorun gerekebilecek `ssh pi@<ip address of pi>` tooconnect Pi SSH aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="ba431-215">You might need toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="ba431-216">Merhaba varsayılan kullanıcı adı `pi` , ve hello parola `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="ba431-216">hello default username is `pi` , and hello password is `raspberry`.</span></span>

1. <span data-ttu-id="ba431-217">Merhaba önkoşul hello Microsoft Azure IOT cihaz SDK'sı için C ve Cmake hello aşağıdaki komutları çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="ba431-217">Install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C and Cmake by running hello following commands:</span></span>

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


### <a name="configure-hello-sample-application"></a><span data-ttu-id="ba431-218">Merhaba örnek uygulamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ba431-218">Configure hello sample application</span></span>

1. <span data-ttu-id="ba431-219">Merhaba örnek uygulaması hello aşağıdaki komutu çalıştırarak kopyalama:</span><span class="sxs-lookup"><span data-stu-id="ba431-219">Clone hello sample application by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-client-app
   ```
1. <span data-ttu-id="ba431-220">Merhaba yapılandırma dosyası hello aşağıdaki komutları çalıştırarak açın:</span><span class="sxs-lookup"><span data-stu-id="ba431-220">Open hello config file by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-raspberrypi-client-app
   nano config.h
   ```

   ![Yapılandırma dosyası](media/iot-hub-raspberry-pi-kit-c-get-started/6_config-file.png)

   <span data-ttu-id="ba431-222">İki makroları vardır bu dosyada configurate olabilir.</span><span class="sxs-lookup"><span data-stu-id="ba431-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="ba431-223">Merhaba ilk biridir `INTERVAL`, toocloud Gönder arasında iki iletileri hello zaman aralığı (milisaniye cinsinden) tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ba431-223">hello first one is `INTERVAL`, which defines hello time interval (in milliseconds) between two messages that send toocloud.</span></span> <span data-ttu-id="ba431-224">İkinci bir hello `SIMULATED_DATA`, veya toouse algılayıcı verilerini olup benzetimi için bir Boole değeri değil.</span><span class="sxs-lookup"><span data-stu-id="ba431-224">hello second one `SIMULATED_DATA`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="ba431-225">Varsa, **hello algılayıcı yok**ayarlayın hello `SIMULATED_DATA` çok değer`1` toomake Merhaba örnek uygulaması oluşturup benzetimli algılayıcı verilerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ba431-225">If you **don't have hello sensor**, set hello `SIMULATED_DATA` value too`1` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="ba431-226">Kaydedip çıkmak denetimi O tuşlarına basarak > Enter > Denetim X.</span><span class="sxs-lookup"><span data-stu-id="ba431-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-hello-sample-application"></a><span data-ttu-id="ba431-227">Derleme ve hello örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="ba431-227">Build and run hello sample application</span></span>

1. <span data-ttu-id="ba431-228">Merhaba örnek uygulaması hello aşağıdaki komutu çalıştırarak oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ba431-228">Build hello sample application by running hello following command:</span></span>

   ```bash
   cmake . && make
   ```
   ![Çıktı derleme](media/iot-hub-raspberry-pi-kit-c-get-started/7_build-output.png)

1. <span data-ttu-id="ba431-230">Merhaba aşağıdaki komutu çalıştırarak Hello örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ba431-230">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo ./app '<DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   <span data-ttu-id="ba431-231">Kopyalama hello cihaz bağlantı dizesi hello tek tırnak yapıştırma emin olun.</span><span class="sxs-lookup"><span data-stu-id="ba431-231">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>


<span data-ttu-id="ba431-232">Gösterir tooyour IOT hub gönderilen algılayıcı verileri ve hello iletileri hello hello aşağıdaki çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ba431-232">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![Çıktı - Raspberry Pi'yi tooyour IOT hub'ından gönderilen algılayıcı verileri](media/iot-hub-raspberry-pi-kit-c-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="ba431-234">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ba431-234">Next steps</span></span>

<span data-ttu-id="ba431-235">Bir örnek uygulama toocollect algılayıcı verilerini çalıştırdıktan ve tooyour IOT hub'ı gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ba431-235">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span> <span data-ttu-id="ba431-236">bkz: Merhaba Raspberry Pi'yi tooyour IOT hub'ı veya gönderme iletileri tooyour Raspberry Pi'yi bir komut satırı arabirimi gönderdiğini toosee hello iletileri [iothub-explorer eğitici Mesajlaşma Yönet bulut cihaz](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="ba431-236">toosee hello messages that your Raspberry Pi has sent tooyour IoT hub or send messages tooyour Raspberry Pi in a command line interface, see hello [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
