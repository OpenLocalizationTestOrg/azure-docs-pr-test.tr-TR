---
title: "Raspberry Pi'yi (düğüm) tooAzure IOT - Ders 1 bağlanın: cihaz yapılandırma | Microsoft Docs"
description: "Raspberry Pi 3'ü ilk kez kullanmak için yapılandırmak ve hello Raspbian işletim sistemi, Raspberry Pi'yi donanım hello için en iyi duruma getirilmiş boş bir işletim sistemi yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Yükleme raspbian, raspbian indirme tooinstall raspbian raspbian Kurulum Böğürtlenli pi yükleme raspbian, Böğürtlenli pi yükleme işletim sistemi, Böğürtlenli pi sd kart yükleme, Böğürtlenli pi bağlantı kurma tooraspberry pi Böğürtlenli pi bağlantı bağlanma"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 43f7c2cf-f1a5-4dd5-93f0-7e546c6dc91e
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 504a4d2a3f29717f955530812442cce2a78a6448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="686d7-104">Cihazınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="686d7-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="686d7-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="686d7-105">What you will do</span></span>
<span data-ttu-id="686d7-106">Pi ilk kez kullanmak için yapılandırmak ve hello Raspbian işletim sistemini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="686d7-106">Configure Pi for first-time use and install hello Raspbian operating system.</span></span> <span data-ttu-id="686d7-107">Raspbian Raspberry Pi'yi donanım hello için en iyi duruma getirilmiş boş bir işletim sistemi ' dir.</span><span class="sxs-lookup"><span data-stu-id="686d7-107">Raspbian is a free operating system that is optimized for hello Raspberry Pi hardware.</span></span> <span data-ttu-id="686d7-108">Herhangi bir sorun varsa, hello çözümlerini arama [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="686d7-108">If you have any problems, you can seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="686d7-109">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="686d7-109">What you will learn</span></span>
<span data-ttu-id="686d7-110">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="686d7-110">In this article, you will learn:</span></span>

* <span data-ttu-id="686d7-111">Nasıl tooinstall Raspbian Pi üzerinde.</span><span class="sxs-lookup"><span data-stu-id="686d7-111">How tooinstall Raspbian on Pi.</span></span>
* <span data-ttu-id="686d7-112">Nasıl bir USB kablosu kullanarak toopower Pi ayarlama.</span><span class="sxs-lookup"><span data-stu-id="686d7-112">How toopower up Pi by using a USB cable.</span></span>
* <span data-ttu-id="686d7-113">Nasıl tooconnect PI toohello ağ bir Ethernet kablolu veya kablosuz ağ kullanarak.</span><span class="sxs-lookup"><span data-stu-id="686d7-113">How tooconnect Pi toohello network by using an Ethernet cable or wireless network.</span></span>
* <span data-ttu-id="686d7-114">Nasıl tooadd LED toohello breadboard ve tooPi bağlanın.</span><span class="sxs-lookup"><span data-stu-id="686d7-114">How tooadd an LED toohello breadboard and connect it tooPi.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="686d7-115">İhtiyacınız olacak</span><span class="sxs-lookup"><span data-stu-id="686d7-115">What you will need</span></span>
<span data-ttu-id="686d7-116">toocomplete bu işlemi Raspberry Pi 3 Starter Seti'nden bölümleri aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="686d7-116">toocomplete this operation, you need hello following parts from your Raspberry Pi 3 Starter Kit:</span></span>

* <span data-ttu-id="686d7-117">Merhaba Raspberry Pi 3 Panosu</span><span class="sxs-lookup"><span data-stu-id="686d7-117">hello Raspberry Pi 3 board</span></span>
* <span data-ttu-id="686d7-118">Merhaba 16 GB microSD kartı</span><span class="sxs-lookup"><span data-stu-id="686d7-118">hello 16-GB microSD card</span></span>
* <span data-ttu-id="686d7-119">Merhaba 6 kaplama alanı mikro USB kablosu ile Merhaba 5-volt 2 amp güç kaynağı</span><span class="sxs-lookup"><span data-stu-id="686d7-119">hello 5-volt 2-amp power supply with hello 6-foot micro USB cable</span></span>
* <span data-ttu-id="686d7-120">Merhaba breadboard</span><span class="sxs-lookup"><span data-stu-id="686d7-120">hello breadboard</span></span>
* <span data-ttu-id="686d7-121">Bağlayıcı kabloları</span><span class="sxs-lookup"><span data-stu-id="686d7-121">Connector wires</span></span>
* <span data-ttu-id="686d7-122">560 ohm Direnç</span><span class="sxs-lookup"><span data-stu-id="686d7-122">A 560-ohm resistor</span></span>
* <span data-ttu-id="686d7-123">Yayılmış 10 mm LED</span><span class="sxs-lookup"><span data-stu-id="686d7-123">A diffused 10-mm LED</span></span>
* <span data-ttu-id="686d7-124">Merhaba Ethernet kablosu</span><span class="sxs-lookup"><span data-stu-id="686d7-124">hello Ethernet cable</span></span>

![Starter Kit şeyler](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

<span data-ttu-id="686d7-126">Şunları da yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="686d7-126">You also need:</span></span>

* <span data-ttu-id="686d7-127">Pi tooconnect için kablolu veya kablosuz bağlantı.</span><span class="sxs-lookup"><span data-stu-id="686d7-127">A wired or wireless connection for Pi tooconnect to.</span></span>
* <span data-ttu-id="686d7-128">Bir USB SD bağdaştırıcı veya miniSD kartı tooburn hello işletim sistemi görüntüsünü hello microSD kartı.</span><span class="sxs-lookup"><span data-stu-id="686d7-128">A USB-SD adapter or miniSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="686d7-129">Windows, Mac veya Linux çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="686d7-129">A computer running Windows, Mac, or Linux.</span></span> <span data-ttu-id="686d7-130">Merhaba, kullanılan tooinstall Raspbian hello microSD kartı bilgisayardır.</span><span class="sxs-lookup"><span data-stu-id="686d7-130">hello computer is used tooinstall Raspbian on hello microSD card.</span></span>
* <span data-ttu-id="686d7-131">Bir Internet bağlantısı toodownload gerekli araçları ve yazılım hello.</span><span class="sxs-lookup"><span data-stu-id="686d7-131">An Internet connection toodownload hello necessary tools and software.</span></span>

## <a name="install-raspbian-on-hello-microsd-card"></a><span data-ttu-id="686d7-132">Merhaba microSD kartı Raspbian yükleyin</span><span class="sxs-lookup"><span data-stu-id="686d7-132">Install Raspbian on hello microSD card</span></span>
<span data-ttu-id="686d7-133">Merhaba microSD kartı hello Raspbian görüntü yüklemesi için hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="686d7-133">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="686d7-134">Raspbian indirin.</span><span class="sxs-lookup"><span data-stu-id="686d7-134">Download Raspbian.</span></span>
   1. <span data-ttu-id="686d7-135">[Karşıdan](https://www.raspberrypi.org/downloads/raspbian/) Raspbian Jessie piksel ile için hello .zip dosyası.</span><span class="sxs-lookup"><span data-stu-id="686d7-135">[Download](https://www.raspberrypi.org/downloads/raspbian/) hello .zip file for Raspbian Jessie with Pixel.</span></span>
   2. <span data-ttu-id="686d7-136">Bilgisayarınızdaki Hello Raspbian görüntü tooa klasöre ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="686d7-136">Extract hello Raspbian image tooa folder on your computer.</span></span>
2. <span data-ttu-id="686d7-137">Raspbian toohello microSD kartı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="686d7-137">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="686d7-138">[Karşıdan](https://www.etcher.io) ve hello Etcher SD kart yazıcı yardımcı programını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="686d7-138">[Download](https://www.etcher.io) and install hello Etcher SD card burner utility.</span></span>
   2. <span data-ttu-id="686d7-139">Etcher çalıştırın ve 1. adımda ayıkladığınız hello Raspbian görüntüsünü seçin.</span><span class="sxs-lookup"><span data-stu-id="686d7-139">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   3. <span data-ttu-id="686d7-140">Merhaba microSD kartı sürücü seçin.</span><span class="sxs-lookup"><span data-stu-id="686d7-140">Select hello microSD card drive.</span></span>
      <span data-ttu-id="686d7-141">Etcher zaten hello doğru sürücü seçmiş olabilirsiniz olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="686d7-141">Note that Etcher may have already selected hello correct drive.</span></span>
   4. <span data-ttu-id="686d7-142">Tıklatın **Flash** tooinstall Raspbian toohello microSD kartı.</span><span class="sxs-lookup"><span data-stu-id="686d7-142">Click **Flash** tooinstall Raspbian toohello microSD card.</span></span>
   5. <span data-ttu-id="686d7-143">Yükleme tamamlandığında hello microSD kartı bilgisayarınızdan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="686d7-143">Remove hello microSD card from your computer when installation is complete.</span></span>
      <span data-ttu-id="686d7-144">Etcher otomatik olarak çıkarır veya hello microSD kartı tamamlanmasından sonra çıkarır güvenli tooremove hello microSD kartı doğrudan demektir.</span><span class="sxs-lookup"><span data-stu-id="686d7-144">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   6. <span data-ttu-id="686d7-145">Merhaba microSD kartı Pi yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="686d7-145">Insert hello microSD card into Pi.</span></span>

![Merhaba SD kart Ekle](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a><span data-ttu-id="686d7-147">Pi üzerinde Aç</span><span class="sxs-lookup"><span data-stu-id="686d7-147">Turn on Pi</span></span>
<span data-ttu-id="686d7-148">Pi üzerinde hello mikro USB kablosu ve hello güç kaynağı kullanarak açın.</span><span class="sxs-lookup"><span data-stu-id="686d7-148">Turn on Pi by using hello micro USB cable and hello power supply.</span></span>

![Aç](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> <span data-ttu-id="686d7-150">En az hello Seti'nde önemli toouse hello güç kaynağı olan 2A toomake, Raspberry yeterli güç toowork doğru olduğundan emin.</span><span class="sxs-lookup"><span data-stu-id="686d7-150">It is important toouse hello power supply in hello kit that is at least 2A toomake sure that your Raspberry has enough power toowork correctly.</span></span>

## <a name="enable-ssh"></a><span data-ttu-id="686d7-151">SSH etkinleştir</span><span class="sxs-lookup"><span data-stu-id="686d7-151">Enable SSH</span></span>
<span data-ttu-id="686d7-152">Kasım 2016 sürüm Hello itibariyle hello SSH sunucusu varsayılan olarak devre dışı Raspbian sahiptir.</span><span class="sxs-lookup"><span data-stu-id="686d7-152">As of hello November 2016 release, Raspbian has hello SSH server disabled by default.</span></span> <span data-ttu-id="686d7-153">Tooenable gerekir, el ile.</span><span class="sxs-lookup"><span data-stu-id="686d7-153">You need tooenable it manually.</span></span> <span data-ttu-id="686d7-154">Toohello başvurabilir [resmi yönergeleri](https://www.raspberrypi.org/documentation/remote-access/ssh/) veya bir izleyici bağlanmak ve çok Git**Tercihler Raspberry Pi yapılandırma ->** tooenable SSH.</span><span class="sxs-lookup"><span data-stu-id="686d7-154">You can refer toohello [official instructions](https://www.raspberrypi.org/documentation/remote-access/ssh/) or connect a monitor and go too**Preferences -> Raspberry Pi Configuration** tooenable SSH.</span></span>

## <a name="connect-raspberry-pi-3-toohello-network"></a><span data-ttu-id="686d7-155">Raspberry Pi 3 toohello ağa bağlan</span><span class="sxs-lookup"><span data-stu-id="686d7-155">Connect Raspberry Pi 3 toohello network</span></span>
<span data-ttu-id="686d7-156">Pi tooa kablolu ağ veya tooa kablosuz ağa bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="686d7-156">You can connect Pi tooa wired network or tooa wireless network.</span></span> <span data-ttu-id="686d7-157">Pi bağlı toohello aynı bilgisayarınızda olarak ağ olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="686d7-157">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="686d7-158">Örneğin, aynı, bilgisayarın bağlı olduğu anahtar Pi toohello bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="686d7-158">For example, you can connect Pi toohello same switch that your computer is connected to.</span></span>

### <a name="connect-tooa-wired-network"></a><span data-ttu-id="686d7-159">Kablolu ağ tooa Bağlan</span><span class="sxs-lookup"><span data-stu-id="686d7-159">Connect tooa wired network</span></span>
<span data-ttu-id="686d7-160">Merhaba Ethernet kablo tooconnect PI tooyour kablolu ağ kullanın.</span><span class="sxs-lookup"><span data-stu-id="686d7-160">Use hello Ethernet cable tooconnect Pi tooyour wired network.</span></span> <span data-ttu-id="686d7-161">Merhaba bağlantı kurulamazsa hello Pi üzerinde iki LED'leri etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="686d7-161">hello two LEDs on Pi turn on if hello connection is established.</span></span>

![Ethernet kablosu kullanarak bağlanma](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-tooa-wireless-network"></a><span data-ttu-id="686d7-163">Tooa kablosuz ağa bağlan</span><span class="sxs-lookup"><span data-stu-id="686d7-163">Connect tooa wireless network</span></span>
<span data-ttu-id="686d7-164">Merhaba izleyin [yönergeleri](https://www.raspberrypi.org/learning/software-guide/wifi/) hello Raspberry Pi Foundation tooconnect PI tooyour kablosuz ağ üzerinden.</span><span class="sxs-lookup"><span data-stu-id="686d7-164">Follow hello [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) from hello Raspberry Pi Foundation tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="686d7-165">Bu yönergeleri gerektiren bir izleyici ve klavye tooPi toofirst bağlanın.</span><span class="sxs-lookup"><span data-stu-id="686d7-165">These instructions require you toofirst connect a monitor and a keyboard tooPi.</span></span>

## <a name="connect-hello-led-toopi"></a><span data-ttu-id="686d7-166">Merhaba LED tooPi Bağlan</span><span class="sxs-lookup"><span data-stu-id="686d7-166">Connect hello LED tooPi</span></span>
<span data-ttu-id="686d7-167">toocomplete bu görev, kullanım hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard)hello bağlayıcı kablo, LED hello ve hello Direnci.</span><span class="sxs-lookup"><span data-stu-id="686d7-167">toocomplete this task, use hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), hello connector wires, hello LED, and hello resistor.</span></span> <span data-ttu-id="686d7-168">Toohello bağlanmak [genel amaçlı giriş/çıkış](https://www.raspberrypi.org/documentation/usage/gpio/) Pi (GPIO'yu) bağlantı noktaları.</span><span class="sxs-lookup"><span data-stu-id="686d7-168">Connect them toohello [general-purpose input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) ports of Pi.</span></span>

![Breadboard, LED ve Direnç](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. <span data-ttu-id="686d7-170">Merhaba kısa Bacak hello LED için çok bağlanmak**GPIO'yu GND (PIN 6)**.</span><span class="sxs-lookup"><span data-stu-id="686d7-170">Connect hello shorter leg of hello LED too**GPIO GND (Pin 6)**.</span></span>
2. <span data-ttu-id="686d7-171">Merhaba uzun Bacak hello LED tooone Bacak hello Direnci için için bağlayın.</span><span class="sxs-lookup"><span data-stu-id="686d7-171">Connect hello longer leg of hello LED tooone leg of hello resistor.</span></span>
3. <span data-ttu-id="686d7-172">Bağlantı diğer Bacak hello Direnci için çok hello**GPIO'yu 4 (PIN 7)**.</span><span class="sxs-lookup"><span data-stu-id="686d7-172">Connect hello other leg of hello resistor too**GPIO 4 (Pin 7)**.</span></span>

<span data-ttu-id="686d7-173">Merhaba LED polarite önemli olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="686d7-173">Note that hello LED polarity is important.</span></span> <span data-ttu-id="686d7-174">Bu polarite ayarı etkin düşük yaygın olarak bilinir.</span><span class="sxs-lookup"><span data-stu-id="686d7-174">This polarity setting is commonly known as Active Low.</span></span>

![Bağlantı](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

<span data-ttu-id="686d7-176">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="686d7-176">Congratulations!</span></span> <span data-ttu-id="686d7-177">Pi başarıyla yapılandırdıktan.</span><span class="sxs-lookup"><span data-stu-id="686d7-177">You've successfully configured Pi.</span></span>

## <a name="summary"></a><span data-ttu-id="686d7-178">Özet</span><span class="sxs-lookup"><span data-stu-id="686d7-178">Summary</span></span>
<span data-ttu-id="686d7-179">Bu makalede, öğrendiğinize tooconfigure nasıl Pi Raspbian, bağlanan Pi tooa ağ, yükleme ve LED tooPi bağlanma.</span><span class="sxs-lookup"><span data-stu-id="686d7-179">In this article, you’ve learned how tooconfigure Pi by installing Raspbian, connecting Pi tooa network, and connecting an LED tooPi.</span></span> <span data-ttu-id="686d7-180">LED henüz açık değil yukarı bu hello unutmayın.</span><span class="sxs-lookup"><span data-stu-id="686d7-180">Note that hello LED doesn't yet light up.</span></span> <span data-ttu-id="686d7-181">Merhaba sonraki tooinstall hello gerekli araçları ve yazılım üzerinde Pi örnek bir uygulamayı çalıştırmak için hazırlanırken bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="686d7-181">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on Pi.</span></span>

![Donanım hazır.](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a><span data-ttu-id="686d7-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="686d7-183">Next steps</span></span>
[<span data-ttu-id="686d7-184">Merhaba araçları edinin</span><span class="sxs-lookup"><span data-stu-id="686d7-184">Get hello tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

