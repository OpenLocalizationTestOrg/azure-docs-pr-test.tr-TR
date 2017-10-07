---
title: "SensorTag cihaz & Azure IOT ağ geçidi - Ders 1: Intel NUC ayarlama | Microsoft Docs"
description: "Intel NUC toowork algılayıcı ve Azure IOT Hub toocollect Algılayıcı bilgilerine arasında bir IOT ağ geçidi olarak ayarlayın ve tooIoT Hub gönderebilirsiniz."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IOT ağ geçidi, Intel nuc nuc bilgisayar, DE3815TYKE"
ms.assetid: 917090d6-35c2-495b-a620-ca6f9c02b317
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7c3ab3b014713c7facb86b8e8622d70e60a960e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="9183e-104">Intel NUC IOT ağ geçidi olarak ayarlayın</span><span class="sxs-lookup"><span data-stu-id="9183e-104">Set up Intel NUC as an IoT gateway</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

## <a name="what-you-will-do"></a><span data-ttu-id="9183e-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="9183e-105">What you will do</span></span>

- <span data-ttu-id="9183e-106">Intel NUC IOT ağ geçidi olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9183e-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="9183e-107">Intel NUC hello üzerinde Hello Azure IOT kenar paketini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9183e-107">Install hello Azure IoT Edge package on hello Intel NUC.</span></span>
- <span data-ttu-id="9183e-108">"Hello_world" örnek bir uygulama Intel NUC tooverify hello ağ geçidi işlevini hello üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9183e-108">Run a "hello_world" sample application on hello Intel NUC tooverify hello gateway functionality.</span></span>

  > <span data-ttu-id="9183e-109">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="9183e-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9183e-110">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="9183e-110">What you will learn</span></span>

<span data-ttu-id="9183e-111">Bu alıştırmanın ilerisinde şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="9183e-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="9183e-112">Nasıl tooconnect Intel NUC çevre birimleri ile.</span><span class="sxs-lookup"><span data-stu-id="9183e-112">How tooconnect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="9183e-113">Nasıl Intel NUC kullanma tooinstall ve güncelleştirme gerekli hello paketleri akıllı Paket Yöneticisi hello.</span><span class="sxs-lookup"><span data-stu-id="9183e-113">How tooinstall and update hello required packages on Intel NUC using hello Smart Package Manager.</span></span>
- <span data-ttu-id="9183e-114">Nasıl toorun hello "hello_world" uygulama tooverify hello ağ geçidi işlevselliği örnek.</span><span class="sxs-lookup"><span data-stu-id="9183e-114">How toorun hello "hello_world" sample application tooverify hello gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9183e-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="9183e-115">What you need</span></span>

- <span data-ttu-id="9183e-116">Bir Intel NUC Seti DE3815TYKE hello Intel IOT ağ geçidi yazılım paketi ile (Rüzgar Akarsu Linux * 7.0.0.13) önceden yüklenmiş.</span><span class="sxs-lookup"><span data-stu-id="9183e-116">An Intel NUC Kit DE3815TYKE with hello Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span> <span data-ttu-id="9183e-117">[Toopurchase Grove IOT ticari ağ geçidi Seti burayı](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span><span class="sxs-lookup"><span data-stu-id="9183e-117">[Click here toopurchase Grove IoT Commercial Gateway Kit](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span></span>
- <span data-ttu-id="9183e-118">Ethernet kablosu.</span><span class="sxs-lookup"><span data-stu-id="9183e-118">An Ethernet cable.</span></span>
- <span data-ttu-id="9183e-119">Klavye.</span><span class="sxs-lookup"><span data-stu-id="9183e-119">A keyboard.</span></span>
- <span data-ttu-id="9183e-120">Bir HDMI veya VGA kablosu.</span><span class="sxs-lookup"><span data-stu-id="9183e-120">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="9183e-121">Bir HDMI veya VGA bağlantı noktasına sahip bir izleme.</span><span class="sxs-lookup"><span data-stu-id="9183e-121">A monitor with an HDMI or VGA port.</span></span>
- <span data-ttu-id="9183e-122">İsteğe bağlı: [Texas Instruments algılayıcı etiketi (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span><span class="sxs-lookup"><span data-stu-id="9183e-122">Optional: [Texas Instruments Sensor Tag (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span></span>

![Ağ geçidi Seti](media/iot-hub-gateway-kit-lessons/lesson1/kit.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a><span data-ttu-id="9183e-124">Intel NUC hello çevre ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="9183e-124">Connect Intel NUC with hello peripherals</span></span>

<span data-ttu-id="9183e-125">Aşağıdaki Hello görüntü ile çeşitli çevre bağlı Intel NUC örneğidir:</span><span class="sxs-lookup"><span data-stu-id="9183e-125">hello image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="9183e-126">Bağlı tooa klavye.</span><span class="sxs-lookup"><span data-stu-id="9183e-126">Connected tooa keyboard.</span></span>
2. <span data-ttu-id="9183e-127">Tooa İzleyici VGA kablo veya HDMI kablo ile bağlı.</span><span class="sxs-lookup"><span data-stu-id="9183e-127">Connected tooa monitor with a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="9183e-128">Kablolu Ethernet kablosu ile ağına bağlı tooa.</span><span class="sxs-lookup"><span data-stu-id="9183e-128">Connected tooa wired network with an Ethernet cable.</span></span>
4. <span data-ttu-id="9183e-129">Güç kablosu bağlı tooa güç kaynakları.</span><span class="sxs-lookup"><span data-stu-id="9183e-129">Connected tooa power supply with a power cable.</span></span>

![Intel NUC tooperipherals bağlı](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="9183e-131">Ana bilgisayar üzerinden güvenli Kabuk (SSH) toohello Intel NUC sistem bağlayın</span><span class="sxs-lookup"><span data-stu-id="9183e-131">Connect toohello Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="9183e-132">Klavye ve Intel NUC aygıtınızın bir izleyici tooget hello IP adresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="9183e-132">You will need a keyboard and a monitor tooget hello IP address of your Intel NUC device.</span></span> <span data-ttu-id="9183e-133">Merhaba IP zaten biliyorsanız, adresi önceden toostep bu bölümdeki 3 atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9183e-133">If you already know hello IP address, you can skip ahead toostep 3 in this section.</span></span>

1. <span data-ttu-id="9183e-134">Intel NUC Hello üzerinde hello güç düğmesine basarak kapatma ve oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9183e-134">Turn on hello Intel NUC by pressing hello power button and then log in.</span></span>

   <span data-ttu-id="9183e-135">Merhaba varsayılan kullanıcı adı ve parola olan her ikisi de `root`.</span><span class="sxs-lookup"><span data-stu-id="9183e-135">hello default user name and password are both `root`.</span></span>

       > Hit hello enter key on your keyboard if you see either of hello following errors when you boot: 'A TPM error (7) occurred attempting tooread a pcr value.' or 'Timeout, No TPM chip found, activating TPM-bypass!'

2. <span data-ttu-id="9183e-136">Merhaba çalıştırarak hello Intel NUC Hello IP adresini alın `ifconfig` hello Intel NUC aygıtta komutu.</span><span class="sxs-lookup"><span data-stu-id="9183e-136">Get hello IP address of hello Intel NUC by running hello `ifconfig` command on hello Intel NUC device.</span></span>

   <span data-ttu-id="9183e-137">Merhaba komutu çıktısı bir örneği burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="9183e-137">Here is an example of hello command output.</span></span>

   ![Intel NUC IP gösteren ifconfig çıktı](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="9183e-139">Bu örnekte, aşağıdaki değer hello `inet addr:` toohello Intel NUC bir ana bilgisayardan bağlandığınızda gereken hello IP adresidir.</span><span class="sxs-lookup"><span data-stu-id="9183e-139">In this example, hello value that follows `inet addr:` is hello IP address that you need when connect toohello Intel NUC from a host computer.</span></span>

3. <span data-ttu-id="9183e-140">SSH istemcilerini, ana bilgisayar tooconnect tooIntel NUC aşağıdaki hello birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="9183e-140">Use one of hello following SSH clients from your host computer tooconnect tooIntel NUC.</span></span>

    - <span data-ttu-id="9183e-141">[PuTTY](http://www.putty.org/) Windows için.</span><span class="sxs-lookup"><span data-stu-id="9183e-141">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="9183e-142">Merhaba yerleşik SSH istemcisi Ubuntu veya macOS.</span><span class="sxs-lookup"><span data-stu-id="9183e-142">hello built-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="9183e-143">Daha etkili ve verimli toooperate bir ana bilgisayardan bir Intel NUC olur.</span><span class="sxs-lookup"><span data-stu-id="9183e-143">It is more efficient and productive toooperate an Intel NUC from a host computer.</span></span> <span data-ttu-id="9183e-144">Intel NUC'ın IP adresi, hello kullanıcı adı ve parola tooconnect tooit bir SSH istemcisi.</span><span class="sxs-lookup"><span data-stu-id="9183e-144">You'll need hello Intel NUC's IP address, user name and password tooconnect tooit via an SSH client.</span></span> <span data-ttu-id="9183e-145">MacOS üzerinde SSH istemcisi kullanan örnek aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="9183e-145">Here is an example that uses an SSH client on macOS.</span></span>
   <span data-ttu-id="9183e-146">![MacOS üzerinde çalışan SSH istemcisi](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="9183e-146">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-hello-azure-iot-edge-package"></a><span data-ttu-id="9183e-147">Hello Azure IOT kenar paketini yükle</span><span class="sxs-lookup"><span data-stu-id="9183e-147">Install hello Azure IoT Edge package</span></span>

<span data-ttu-id="9183e-148">Hello Azure IOT kenar paket hello önceden derlenmiş ikili dosyaları IOT kenarı ve onun bağımlılıklarını içerir.</span><span class="sxs-lookup"><span data-stu-id="9183e-148">hello Azure IoT Edge package contains hello pre-compiled binaries of IoT Edge and its dependencies.</span></span> <span data-ttu-id="9183e-149">Bu ikili dosyaları, Azure IOT kenar, hello Azure IOT SDK'sı ve hello karşılık gelen araçlar vardır.</span><span class="sxs-lookup"><span data-stu-id="9183e-149">These binaries are Azure IoT Edge, hello Azure IoT SDK and hello corresponding tools.</span></span> <span data-ttu-id="9183e-150">Merhaba ayrıca "hello_world" pakette örnek uygulamasıdır kullanılan toovalidate hello ağ geçidi işlevi.</span><span class="sxs-lookup"><span data-stu-id="9183e-150">hello package also contains a "hello_world" sample application is used toovalidate hello gateway functionality.</span></span> <span data-ttu-id="9183e-151">IOT kenar hello çekirdek hello ağ geçidi parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="9183e-151">IoT Edge is hello core part of hello gateway.</span></span> 

<span data-ttu-id="9183e-152">Bu adımları tooinstall hello paket izleyin.</span><span class="sxs-lookup"><span data-stu-id="9183e-152">Follow these steps tooinstall hello package.</span></span>

1. <span data-ttu-id="9183e-153">Merhaba IOT bulut deposu bir terminal penceresi komutlarda aşağıdaki hello çalıştırarak ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9183e-153">Add hello IoT Cloud repository by running hello following commands in a terminal window:</span></span>

   ```bash
   rpm --import https://iotdk.intel.com/misc/iot_pub2.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
   ```

   > <span data-ttu-id="9183e-154">Bu too'Include istediğinde 'y', bu kanal girin?'</span><span class="sxs-lookup"><span data-stu-id="9183e-154">Enter 'y', when it prompts you too'Include this channel?'</span></span>
   
   <span data-ttu-id="9183e-155">Alırsanız, bir `import read failed(-1)` hatası, komutları tooresolve hello sorunu aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="9183e-155">If you receive an `import read failed(-1)` error, use hello following commands tooresolve hello issue:</span></span>
   ```bash
   wget http://iotdk.intel.com/misc/iot_pub2.key 
   rpm --import iot_pub2.key  
   ```

   <span data-ttu-id="9183e-156">Merhaba `rpm` içeri aktarmalar hello rpm anahtar komutu.</span><span class="sxs-lookup"><span data-stu-id="9183e-156">hello `rpm` command imports hello rpm key.</span></span> <span data-ttu-id="9183e-157">Merhaba `smart channel` komut ekler hello rpm kanal toohello akıllı Paket Yöneticisi.</span><span class="sxs-lookup"><span data-stu-id="9183e-157">hello `smart channel` command adds hello rpm channel toohello Smart Package Manager.</span></span> <span data-ttu-id="9183e-158">Merhaba çalıştırmadan önce `smart update` görürsünüz, komut çıktısı ister aşağıda.</span><span class="sxs-lookup"><span data-stu-id="9183e-158">Before you run hello `smart update` command, you will see an output like below.</span></span>

   ![RPM ve akıllı kanal komutları çıkış](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

2. <span data-ttu-id="9183e-160">Merhaba akıllı güncelleştirme komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="9183e-160">Execute hello smart update command:</span></span>

   ```bash
   smart update
   ```

3. <span data-ttu-id="9183e-161">Merhaba aşağıdaki komutu çalıştırarak Hello Azure IOT ağ geçidi paketini yükle:</span><span class="sxs-lookup"><span data-stu-id="9183e-161">Install hello Azure IoT Gateway package by running hello following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="9183e-162">`packagegroup-cloud-azure`Merhaba paket Hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="9183e-162">`packagegroup-cloud-azure` is hello name of hello package.</span></span> <span data-ttu-id="9183e-163">Merhaba `smart install` kullanılan tooinstall hello paket komuttur.</span><span class="sxs-lookup"><span data-stu-id="9183e-163">hello `smart install` command is used tooinstall hello package.</span></span>

    > <span data-ttu-id="9183e-164">Çalışma hello şu komutu bu hatayı görüyorsanız: 'ortak anahtar yok'</span><span class="sxs-lookup"><span data-stu-id="9183e-164">Run hello following command if you see this error: 'public key not available'</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```
    > <span data-ttu-id="9183e-165">Bu hatayı görürseniz hello Intel NUC yeniden: 'hiçbir paket kul linux geliştirme sağlar'</span><span class="sxs-lookup"><span data-stu-id="9183e-165">Reboot hello Intel NUC if you see this error: 'no package provides util-linux-dev'</span></span>

   <span data-ttu-id="9183e-166">Merhaba paket yüklendikten sonra Intel NUC hazır toofunction bir ağ geçidi olarak var.</span><span class="sxs-lookup"><span data-stu-id="9183e-166">After hello package is installed, Intel NUC is ready toofunction as a gateway.</span></span>

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="9183e-167">Hello Azure IOT kenar "hello_world" örnek uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="9183e-167">Run hello Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="9183e-168">örnek uygulama aşağıdaki hello oluşturur bir ağ geçidi'nden bir `hello_world.json` dosya ve Azure IOT kenar mimarisi toolog hello world ileti tooa dosyası (log.txt) temel bileşenlerinin hello 5 saniyede kullanır.</span><span class="sxs-lookup"><span data-stu-id="9183e-168">hello following sample application creates a gateway from a `hello_world.json` file and uses hello fundamental components of Azure IoT Edge architecture toolog a hello world message tooa file (log.txt) every 5 seconds.</span></span>

<span data-ttu-id="9183e-169">Merhaba aşağıdaki komutları yürüterek hello Hello World örnek çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9183e-169">You can run hello Hello World sample by executing hello following commands:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="9183e-170">Birkaç dakika çalıştırın ve hello Enter anahtar toostop isabet Merhaba Merhaba Dünya uygulaması izin onu.</span><span class="sxs-lookup"><span data-stu-id="9183e-170">Let hello Hello World application run for a few minutes and then hit hello Enter key toostop it.</span></span>
<span data-ttu-id="9183e-171">![Uygulama çıktısı](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span><span class="sxs-lookup"><span data-stu-id="9183e-171">![application output](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span></span>

> <span data-ttu-id="9183e-172">Enter tuşuna basın sonra görüntülenen 'geçersiz bağımsız değişken handle(NULL)' hataları yoksayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9183e-172">You can ignore any 'invalid argument handle(NULL)' errors that appear after you hit Enter.</span></span>

<span data-ttu-id="9183e-173">Şimdi hello_world klasörünüzde hello log.txt dosyasını açarak bu hello ağ geçidi başarıyla çalıştırdı doğrulayabilirsiniz ![log.txt dizin görünümü](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span><span class="sxs-lookup"><span data-stu-id="9183e-173">You can verify that hello gateway ran successfully by opening hello log.txt file that is now in your hello_world folder ![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span></span>

<span data-ttu-id="9183e-174">Komutu aşağıdaki hello kullanarak log.txt açın:</span><span class="sxs-lookup"><span data-stu-id="9183e-174">Open log.txt using hello following command:</span></span>

```bash
vim log.txt
```

<span data-ttu-id="9183e-175">Ardından 5 saniyede hello ağ geçidi Hello World modülü tarafından yazılmış günlük iletilerini Merhaba biçimlendirilmiş JSON çıktısını olacaktır log.txt Merhaba içeriğine görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9183e-175">You will then see hello contents of log.txt, which will be a JSON formatted output of hello logging messages that were written every 5 seconds by hello gateway Hello World module.</span></span>
<span data-ttu-id="9183e-176">![log.txt dizin görünümü](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span><span class="sxs-lookup"><span data-stu-id="9183e-176">![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span></span>

<span data-ttu-id="9183e-177">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="9183e-177">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="9183e-178">Özet</span><span class="sxs-lookup"><span data-stu-id="9183e-178">Summary</span></span>

<span data-ttu-id="9183e-179">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="9183e-179">Congratulations!</span></span> <span data-ttu-id="9183e-180">Intel NUC ayarlama bir ağ geçidi olarak tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="9183e-180">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="9183e-181">Hazır artık toomove toohello sonraki Ders tooset, ana bilgisayar üzerinde Azure IOT Hub oluşturma ve Azure IOT hub'ı mantıksal Cihazınızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9183e-181">Now you're ready toomove on toohello next lesson tooset up your host computer, create an Azure IoT Hub and register your Azure IoT Hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9183e-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9183e-182">Next steps</span></span>
[<span data-ttu-id="9183e-183">IOT ağ geçidi tooconnect aygıt tooAzure IOT hub'ı kullanın</span><span class="sxs-lookup"><span data-stu-id="9183e-183">Use an IoT gateway tooconnect a device tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

