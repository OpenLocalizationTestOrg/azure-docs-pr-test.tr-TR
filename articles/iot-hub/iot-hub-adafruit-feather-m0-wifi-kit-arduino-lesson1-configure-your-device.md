---
title: "Connect Arduino (C) tooAzure IOT - Ders 1: cihaz yapılandırma | Microsoft Docs"
description: "Adafruit yumuşatma M0 WiFi ilk kez kullanmak için yapılandırın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "ayarlama, arduino bağlanmak arduino toopc, Kurulum arduino, arduino Panosu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: f5b334f0-a148-41aa-b374-ce7b9f5b305a
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 30b764e8ff6221995456283a226e79f064b2d74e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="3cee4-104">Cihazınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3cee4-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="3cee4-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="3cee4-105">What you will do</span></span>
<span data-ttu-id="3cee4-106">Merhaba Panosu, Yukarı başlatırken birleştirerek Adafruit yumuşatma M0 WiFi Arduino panonuzu ilk kez kullanmak için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3cee4-106">Configure your Adafruit Feather M0 WiFi Arduino board for first-time use by assembling hello board, powering it up.</span></span> <span data-ttu-id="3cee4-107">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="3cee4-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3cee4-108">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="3cee4-108">What you need</span></span>
<span data-ttu-id="3cee4-109">toocomplete bu işlem, Adafruit yumuşatma M0 WiFi Starter Kit için bölümleri aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="3cee4-109">toocomplete this operation, you need hello following parts for your Adafruit Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="3cee4-110">Merhaba Adafruit yumuşatma M0 WiFi Panosu</span><span class="sxs-lookup"><span data-stu-id="3cee4-110">hello Adafruit Feather M0 WiFi board</span></span>
* <span data-ttu-id="3cee4-111">Mikro B tooType bir USB kablosu</span><span class="sxs-lookup"><span data-stu-id="3cee4-111">A Micro B tooType A USB cable</span></span>

![Seti][kit]

<span data-ttu-id="3cee4-113">Şunları da yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="3cee4-113">You also need:</span></span>

* <span data-ttu-id="3cee4-114">Windows, Mac veya Linux çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="3cee4-114">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="3cee4-115">Kablosuz bağlantı, Arduino Panosu tooconnect için.</span><span class="sxs-lookup"><span data-stu-id="3cee4-115">A wireless connection for your Arduino board tooconnect to.</span></span>
* <span data-ttu-id="3cee4-116">Bir Internet bağlantısı toodownload yapılandırma aracı.</span><span class="sxs-lookup"><span data-stu-id="3cee4-116">An Internet connection toodownload configuration tool.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3cee4-117">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="3cee4-117">What you will learn</span></span>
<span data-ttu-id="3cee4-118">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="3cee4-118">In this article, you will learn:</span></span>

* <span data-ttu-id="3cee4-119">Nasıl tooassemble Arduino kurulu ve güç, aşağıdaki hello kaydınızı dersler.</span><span class="sxs-lookup"><span data-stu-id="3cee4-119">How tooassemble your Arduino board and power it up for hello following lessons.</span></span>
* <span data-ttu-id="3cee4-120">Nasıl Ubuntu tooadd seri bağlantı noktası izinleri.</span><span class="sxs-lookup"><span data-stu-id="3cee4-120">How tooadd serial port permissions on Ubuntu.</span></span>

## <a name="connect-your-arduino-board-tooyour-computer"></a><span data-ttu-id="3cee4-121">Arduino tablosu tooyour bilgisayarınızı bağlayın</span><span class="sxs-lookup"><span data-stu-id="3cee4-121">Connect your Arduino board tooyour computer</span></span>

1. <span data-ttu-id="3cee4-122">Merhaba mikro USB kablosu hello üst mikro USB bağlantı noktasına takın.</span><span class="sxs-lookup"><span data-stu-id="3cee4-122">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![Üst mikro USB bağlantı noktası][top-micro-usb-port]

2. <span data-ttu-id="3cee4-124">Tak bilgisayarınıza USB kablosu diğer ucundaki hello.</span><span class="sxs-lookup"><span data-stu-id="3cee4-124">Plug hello other end of USB cable into your computer.</span></span>

   ![Bilgisayar USB][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a><span data-ttu-id="3cee4-126">Seri bağlantı noktası izinleri üzerinde Ubuntu ekleyin</span><span class="sxs-lookup"><span data-stu-id="3cee4-126">Add serial port permissions on Ubuntu</span></span>

<span data-ttu-id="3cee4-127">Windows veya macOS kullanırsanız, bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3cee4-127">You can skip this section if you use Windows or macOS.</span></span> <span data-ttu-id="3cee4-128">Ubuntu için aşağıdaki adımları toomake hello normal linux kullanıcı hello izinleri toooperate Arduino panosunun hello USB bağlantı noktasına sahip olduğundan emin hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="3cee4-128">For Ubuntu, you need hello following steps toomake sure hello normal linux user has hello permissions toooperate on hello USB port of your Arduino board.</span></span>

1. <span data-ttu-id="3cee4-129">Terminal artık normal olarak kullanıcıdan:</span><span class="sxs-lookup"><span data-stu-id="3cee4-129">Now as normal user from terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="3cee4-130">Aşağıdakine benzer alırsınız:</span><span class="sxs-lookup"><span data-stu-id="3cee4-130">You will get something like:</span></span>

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   <span data-ttu-id="3cee4-131">"0" Merhaba farklı bir numara olabilir veya birden çok giriş döndürdü.</span><span class="sxs-lookup"><span data-stu-id="3cee4-131">hello "0" might be a different number, or multiple entries might be returned.</span></span> <span data-ttu-id="3cee4-132">İhtiyacımız hello ilk örneği hello verilerde `uucp`, hello ikinci olan `dialout`, hello dosyanın hello Grup sahibi olduğu.</span><span class="sxs-lookup"><span data-stu-id="3cee4-132">In hello first case hello data we need is `uucp`, in hello second is `dialout`, which is hello group owner of hello file.</span></span>

2. <span data-ttu-id="3cee4-133">Kullanıcı toohello toohello grubu Ekle:</span><span class="sxs-lookup"><span data-stu-id="3cee4-133">Add user toohello toohello group:</span></span>

   ```bash
   sudo usermod -a -G group-name username
   ```

   <span data-ttu-id="3cee4-134">Burada `group-name` hello veri hello ilk adımda bulundu ve `username` linux kullanıcı adınızdır.</span><span class="sxs-lookup"><span data-stu-id="3cee4-134">Where `group-name` is hello data found in hello first step, and `username` is your linux user name.</span></span>

3. <span data-ttu-id="3cee4-135">Bu değişikliğin tootake ve tam hello kurulumu için toolog oturumunuzu kapatıp tekrar gerekir.</span><span class="sxs-lookup"><span data-stu-id="3cee4-135">You will need toolog out and in again for this change tootake effect and complete hello setup.</span></span>

## <a name="summary"></a><span data-ttu-id="3cee4-136">Özet</span><span class="sxs-lookup"><span data-stu-id="3cee4-136">Summary</span></span>
<span data-ttu-id="3cee4-137">Bu makalede, öğrendiğinize nasıl tooconfigure Arduino panonuz.</span><span class="sxs-lookup"><span data-stu-id="3cee4-137">In this article, you’ve learned how tooconfigure your Arduino board.</span></span> <span data-ttu-id="3cee4-138">Merhaba sonraki tooinstall hello gerekli araçları ve yazılım Arduino Panonuzda örnek bir uygulamayı çalıştırmak için hazırlanırken bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="3cee4-138">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on your Arduino board.</span></span>

![Donanım hazır.][hardware-is-ready]

## <a name="next-steps"></a><span data-ttu-id="3cee4-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3cee4-140">Next steps</span></span>
<span data-ttu-id="3cee4-141">[Merhaba araçları edinin][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="3cee4-141">[Get hello tools][get-the-tools]</span></span>
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md