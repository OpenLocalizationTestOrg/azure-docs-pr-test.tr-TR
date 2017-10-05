---
title: "Azure IOT - Ders 1 Connect Raspberry pi (C): cihaz yapılandırma | Microsoft Docs"
description: "Raspberry Pi 3'ü ilk kez kullanmak için yapılandırmak ve Raspberry Pi'yi donanım için en iyi duruma getirilmiş boş bir işletim sistemi Raspbian işletim sistemi yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Yükleme raspbian, raspbian indirme raspbian, raspbian Kurulum, Böğürtlenli pi yükleme raspbian, Böğürtlenli pi yükleme işletim sistemi, Böğürtlenli pi sd kart yükleme, raspberry yüklemek için pi bağlantı kurma Böğürtlenli pi, Böğürtlenli pi bağlantı bağlanma"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8ee9b23c-93f7-43ff-8ea1-e7761eb87a6f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 2a380f78d67db47a0dcab5b90843404921510528
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="c920e-104">Cihazınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c920e-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="c920e-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="c920e-105">What you will do</span></span>
<span data-ttu-id="c920e-106">Pi ilk kez kullanmak için yapılandırmak ve Raspbian işletim sistemini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c920e-106">Configure Pi for first-time use and install the Raspbian operating system.</span></span> <span data-ttu-id="c920e-107">Raspbian Raspberry Pi'yi donanım için en iyi duruma getirilmiş boş bir işletim sistemi ' dir.</span><span class="sxs-lookup"><span data-stu-id="c920e-107">Raspbian is a free operating system that is optimized for the Raspberry Pi hardware.</span></span> <span data-ttu-id="c920e-108">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="c920e-108">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c920e-109">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="c920e-109">What you will learn</span></span>
<span data-ttu-id="c920e-110">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="c920e-110">In this article, you will learn:</span></span>

* <span data-ttu-id="c920e-111">Raspbian Pi üzerinde yükleme.</span><span class="sxs-lookup"><span data-stu-id="c920e-111">How to install Raspbian on Pi.</span></span>
* <span data-ttu-id="c920e-112">Bir USB kablosu kullanarak pi güç yapma.</span><span class="sxs-lookup"><span data-stu-id="c920e-112">How to power up Pi by using a USB cable.</span></span>
* <span data-ttu-id="c920e-113">Pi ağa bir Ethernet kablolu veya kablosuz ağ kullanarak bağlanma.</span><span class="sxs-lookup"><span data-stu-id="c920e-113">How to connect Pi to the network by using an Ethernet cable or wireless network.</span></span>
* <span data-ttu-id="c920e-114">Nasıl bir LED breadboard ekleyin ve Pi bağlanın.</span><span class="sxs-lookup"><span data-stu-id="c920e-114">How to add an LED to the breadboard and connect it to Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c920e-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="c920e-115">What you need</span></span>
<span data-ttu-id="c920e-116">Bu işlemi tamamlamak için aşağıdaki bölümleri Raspberry Pi 3 Starter Seti'nden gerekir:</span><span class="sxs-lookup"><span data-stu-id="c920e-116">To complete this operation, you need the following parts from your Raspberry Pi 3 Starter Kit:</span></span>

* <span data-ttu-id="c920e-117">Raspberry Pi 3 Panosu</span><span class="sxs-lookup"><span data-stu-id="c920e-117">The Raspberry Pi 3 board</span></span>
* <span data-ttu-id="c920e-118">16 GB microSD kartı</span><span class="sxs-lookup"><span data-stu-id="c920e-118">The 16-GB microSD card</span></span>
* <span data-ttu-id="c920e-119">5-volt 2 amp güç kaynağı ile 6 kaplama alanı mikro USB kablosu</span><span class="sxs-lookup"><span data-stu-id="c920e-119">The 5-volt 2-amp power supply with the 6-foot micro USB cable</span></span>
* <span data-ttu-id="c920e-120">Breadboard</span><span class="sxs-lookup"><span data-stu-id="c920e-120">The breadboard</span></span>
* <span data-ttu-id="c920e-121">Bağlayıcı kabloları</span><span class="sxs-lookup"><span data-stu-id="c920e-121">Connector wires</span></span>
* <span data-ttu-id="c920e-122">560 ohm Direnç</span><span class="sxs-lookup"><span data-stu-id="c920e-122">A 560-ohm resistor</span></span>
* <span data-ttu-id="c920e-123">Yayılmış 10 mm LED</span><span class="sxs-lookup"><span data-stu-id="c920e-123">A diffused 10-mm LED</span></span>
* <span data-ttu-id="c920e-124">Ethernet kablosu</span><span class="sxs-lookup"><span data-stu-id="c920e-124">The Ethernet cable</span></span>

![Starter Kit şeyler](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

<span data-ttu-id="c920e-126">Şunları da yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="c920e-126">You also need:</span></span>

* <span data-ttu-id="c920e-127">Pi bağlanmak için bir kablolu veya kablosuz bağlantı.</span><span class="sxs-lookup"><span data-stu-id="c920e-127">A wired or wireless connection for Pi to connect to.</span></span>
* <span data-ttu-id="c920e-128">İşletim sistemi görüntüsü microSD kartı üzerine yazmak için bir USB SD bağdaştırıcı veya mini SD kart.</span><span class="sxs-lookup"><span data-stu-id="c920e-128">A USB-SD adapter or mini-SD card to burn the OS image onto the microSD card.</span></span>
* <span data-ttu-id="c920e-129">Windows, Mac veya Linux çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="c920e-129">A computer running Windows, Mac, or Linux.</span></span> <span data-ttu-id="c920e-130">Bilgisayar üzerinde microSD kartı Raspbian yüklemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c920e-130">The computer is used to install Raspbian on the microSD card.</span></span>
* <span data-ttu-id="c920e-131">Gerekli araçları ve yazılım indirmesi için Internet bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="c920e-131">An Internet connection to download the necessary tools and software.</span></span>

## <a name="install-raspbian-on-the-microsd-card"></a><span data-ttu-id="c920e-132">Raspbian MicroSD kartı yükleyin</span><span class="sxs-lookup"><span data-stu-id="c920e-132">Install Raspbian on the MicroSD card</span></span>
<span data-ttu-id="c920e-133">MicroSD kartı Raspbian görüntünün yüklenmesi için hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="c920e-133">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="c920e-134">Raspbian indirin.</span><span class="sxs-lookup"><span data-stu-id="c920e-134">Download Raspbian.</span></span>
   1. <span data-ttu-id="c920e-135">[Karşıdan](https://www.raspberrypi.org/downloads/raspbian/) Raspbian Jessie piksel ile .zip dosyası.</span><span class="sxs-lookup"><span data-stu-id="c920e-135">[Download](https://www.raspberrypi.org/downloads/raspbian/) the .zip file for Raspbian Jessie with Pixel.</span></span>
   2. <span data-ttu-id="c920e-136">Raspbian görüntünün bilgisayarınızdaki bir klasöre ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="c920e-136">Extract the Raspbian image to a folder on your computer.</span></span>
2. <span data-ttu-id="c920e-137">Raspbian microSD kartı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c920e-137">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="c920e-138">[Karşıdan](https://www.etcher.io) ve Etcher SD kart yazıcı yardımcı programını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c920e-138">[Download](https://www.etcher.io) and install the Etcher SD card burner utility.</span></span>
   2. <span data-ttu-id="c920e-139">Etcher çalıştırın ve 1. adımda ayıkladığınız Raspbian görüntüyü seçin.</span><span class="sxs-lookup"><span data-stu-id="c920e-139">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   3. <span data-ttu-id="c920e-140">MicroSD kartı sürücü seçin.</span><span class="sxs-lookup"><span data-stu-id="c920e-140">Select the microSD card drive.</span></span>
      <span data-ttu-id="c920e-141">Etcher zaten doğru sürücü seçmiş olabilirsiniz olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c920e-141">Note that Etcher may have already selected the correct drive.</span></span>
   4. <span data-ttu-id="c920e-142">Tıklatın **Flash** Raspbian microSD kartı yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="c920e-142">Click **Flash** to install Raspbian to the microSD card.</span></span>
   5. <span data-ttu-id="c920e-143">Yükleme tamamlandığında microSD kartı bilgisayarınızdan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="c920e-143">Remove the microSD card from your computer when installation is complete.</span></span>
      <span data-ttu-id="c920e-144">Etcher otomatik olarak çıkarır veya tamamlanmasından sonra microSD kartı çıkarır çünkü microSD kartı doğrudan kaldırmak güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="c920e-144">It is safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   6. <span data-ttu-id="c920e-145">MicroSD kartı, Pi yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="c920e-145">Insert the microSD card into your Pi.</span></span>

![SD kart Ekle](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a><span data-ttu-id="c920e-147">Pi üzerinde Aç</span><span class="sxs-lookup"><span data-stu-id="c920e-147">Turn on Pi</span></span>
<span data-ttu-id="c920e-148">Pi üzerinde mikro USB kablosu ve güç kaynağı kullanarak açın.</span><span class="sxs-lookup"><span data-stu-id="c920e-148">Turn on Pi by using the micro USB cable and the power supply.</span></span>

![Aç](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> <span data-ttu-id="c920e-150">En az Seti'nde güç kaynağı kullanmak önemlidir 2A, Raspberry düzgün çalışması için yeterli güç olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c920e-150">It is important to use the power supply in the kit that is at least 2A to make sure that your Raspberry has enough power to work correctly.</span></span>

## <a name="enable-ssh"></a><span data-ttu-id="c920e-151">SSH etkinleştir</span><span class="sxs-lookup"><span data-stu-id="c920e-151">Enable SSH</span></span>
<span data-ttu-id="c920e-152">Kasım 2016 güncelleştirmesinden itibaren Raspbian varsayılan olarak devre dışı SSH sunucusu vardır.</span><span class="sxs-lookup"><span data-stu-id="c920e-152">As of the November 2016 release, Raspbian has the SSH server disabled by default.</span></span> <span data-ttu-id="c920e-153">El ile etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c920e-153">You need to enable it manually.</span></span> <span data-ttu-id="c920e-154">Başvurabilirsiniz [resmi yönergeleri](https://www.raspberrypi.org/documentation/remote-access/ssh/) veya bir izleyici bağlanmak ve Git **Tercihler Raspberry Pi yapılandırma ->** SSH etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="c920e-154">You can refer to the [official instructions](https://www.raspberrypi.org/documentation/remote-access/ssh/) or connect a monitor and go to **Preferences -> Raspberry Pi Configuration** to enable SSH.</span></span>

## <a name="connect-raspberry-pi-3-to-the-network"></a><span data-ttu-id="c920e-155">Raspberry Pi 3 ağa bağlanın</span><span class="sxs-lookup"><span data-stu-id="c920e-155">Connect Raspberry Pi 3 to the network</span></span>
<span data-ttu-id="c920e-156">Pi kablolu veya kablosuz ağa bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="c920e-156">You can connect Pi to a wired network or to a wireless network.</span></span> <span data-ttu-id="c920e-157">Pi bilgisayarınızın aynı ağa bağlı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c920e-157">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="c920e-158">Örneğin, Pi, bilgisayarın bağlı olduğu aynı anahtara bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="c920e-158">For example, you can connect Pi to the same switch that your computer is connected to.</span></span>

### <a name="connect-to-a-wired-network"></a><span data-ttu-id="c920e-159">Kablolu bir ağa bağlan</span><span class="sxs-lookup"><span data-stu-id="c920e-159">Connect to a wired network</span></span>
<span data-ttu-id="c920e-160">Pi kablolu ağa bağlamak için Ethernet kablosu kullanın.</span><span class="sxs-lookup"><span data-stu-id="c920e-160">Use the Ethernet cable to connect Pi to your wired network.</span></span> <span data-ttu-id="c920e-161">Bağlantı kurulamazsa Pi üzerinde iki LED'leri etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c920e-161">The two LEDs on Pi turn on if the connection is established.</span></span>

![Ethernet kablosu kullanarak bağlanma](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-to-a-wireless-network"></a><span data-ttu-id="c920e-163">Kablosuz bir ağa bağlan</span><span class="sxs-lookup"><span data-stu-id="c920e-163">Connect to a wireless network</span></span>
<span data-ttu-id="c920e-164">İzleyin [yönergeleri](https://www.raspberrypi.org/learning/software-guide/wifi/) Pi kablosuz ağınıza bağlanmak için Raspberry Pi Foundation gelen.</span><span class="sxs-lookup"><span data-stu-id="c920e-164">Follow the [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) from the Raspberry Pi Foundation to connect Pi to your wireless network.</span></span> <span data-ttu-id="c920e-165">Bu yönergeleri Pi bir izleyici ve klavye ilk bağlanmanızı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c920e-165">These instructions require you to first connect a monitor and a keyboard to Pi.</span></span>

## <a name="connect-the-led-to-pi"></a><span data-ttu-id="c920e-166">Pi LED Bağlan</span><span class="sxs-lookup"><span data-stu-id="c920e-166">Connect the LED to Pi</span></span>
<span data-ttu-id="c920e-167">Bu görevi tamamlamak için kullanmak [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), bağlayıcı kablo, LED ve Direnci.</span><span class="sxs-lookup"><span data-stu-id="c920e-167">To complete this task, use the [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), the connector wires, the LED, and the resistor.</span></span> <span data-ttu-id="c920e-168">Kendilerine bağlanması [genel amaçlı giriş/çıkış](https://www.raspberrypi.org/documentation/usage/gpio/) Pi (GPIO'yu) bağlantı noktaları.</span><span class="sxs-lookup"><span data-stu-id="c920e-168">Connect them to the [general-purpose input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) ports of Pi.</span></span>

![Breadboard, LED ve Direnç](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. <span data-ttu-id="c920e-170">Daha kısa Bacak LED için bağlanmak **GPIO'yu GND (PIN 6)**.</span><span class="sxs-lookup"><span data-stu-id="c920e-170">Connect the shorter leg of the LED to **GPIO GND (Pin 6)**.</span></span>
2. <span data-ttu-id="c920e-171">LED uzun bacaktaki Direnci bir bacağı için bağlayın.</span><span class="sxs-lookup"><span data-stu-id="c920e-171">Connect the longer leg of the LED to one leg of the resistor.</span></span>
3. <span data-ttu-id="c920e-172">Diğer Bacak Direnci için bağlanmak **GPIO'yu 4 (PIN 7)**.</span><span class="sxs-lookup"><span data-stu-id="c920e-172">Connect the other leg of the resistor to **GPIO 4 (Pin 7)**.</span></span>

<span data-ttu-id="c920e-173">LED polarite önemli olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c920e-173">Note that the LED polarity is important.</span></span> <span data-ttu-id="c920e-174">Bu polarite ayarı etkin düşük yaygın olarak bilinir.</span><span class="sxs-lookup"><span data-stu-id="c920e-174">This polarity setting is commonly known as Active Low.</span></span>

![Bağlantı](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

<span data-ttu-id="c920e-176">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="c920e-176">Congratulations!</span></span> <span data-ttu-id="c920e-177">Pi başarıyla yapılandırdıktan.</span><span class="sxs-lookup"><span data-stu-id="c920e-177">You've successfully configured Pi.</span></span>

## <a name="summary"></a><span data-ttu-id="c920e-178">Özet</span><span class="sxs-lookup"><span data-stu-id="c920e-178">Summary</span></span>
<span data-ttu-id="c920e-179">Bu makalede, Raspbian yükleyerek, Pi ağa bağlanma ve bir LED Pi bağlanma Pi yapılandırma öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="c920e-179">In this article, you’ve learned how to configure Pi by installing Raspbian, connecting Pi to a network, and connecting an LED to Pi.</span></span> <span data-ttu-id="c920e-180">LED henüz açık değil yukarı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c920e-180">Note that the LED doesn't yet light up.</span></span> <span data-ttu-id="c920e-181">Sonraki hazırlık Pi üzerinde örnek bir uygulamayı çalıştırmak için gerekli araçları ve yazılım yüklemek için bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="c920e-181">The next task is to install the necessary tools and software in preparation for running a sample application on Pi.</span></span>

![Donanım hazır.](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a><span data-ttu-id="c920e-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c920e-183">Next steps</span></span>
[<span data-ttu-id="c920e-184">Araçları edinin</span><span class="sxs-lookup"><span data-stu-id="c920e-184">Get the tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

