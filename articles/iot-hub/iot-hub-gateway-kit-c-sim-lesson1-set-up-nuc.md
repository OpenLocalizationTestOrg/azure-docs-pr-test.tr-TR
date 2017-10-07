---
title: "Benzetimli cihaz & Azure IOT ağ geçidi - Ders 1: NUC ayarlama | Microsoft Docs"
description: "Intel NUC toowork algılayıcı ve Azure IOT Hub toocollect Algılayıcı bilgilerine arasında bir IOT ağ geçidi olarak ayarlayın ve tooIoT Hub gönderebilirsiniz."
services: iot-hub
documentationcenter: 
author: shizn
manager: yjianfeng
tags: 
keywords: "IOT ağ geçidi, Intel nuc nuc bilgisayar, DE3815TYKE"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f41d6b2e-9b00-40df-90eb-17d824bea883
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c2146c7cd8ca54adbd0af279364ec8484be1b45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="b5786-104">Intel NUC IOT ağ geçidi olarak ayarlayın</span><span class="sxs-lookup"><span data-stu-id="b5786-104">Set up Intel NUC as an IoT gateway</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="b5786-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="b5786-105">What you will do</span></span>

- <span data-ttu-id="b5786-106">Intel NUC IOT ağ geçidi olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b5786-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="b5786-107">Intel NUC üzerinde Hello Azure IOT kenar paketini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b5786-107">Install hello Azure IoT Edge package on Intel NUC.</span></span>
- <span data-ttu-id="b5786-108">"Hello_world" örnek bir uygulama Intel NUC tooverify hello ağ geçidi işlevini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b5786-108">Run a "hello_world" sample application on Intel NUC tooverify hello gateway functionality.</span></span>
<span data-ttu-id="b5786-109">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="b5786-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="b5786-110">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="b5786-110">What you will learn</span></span>

<span data-ttu-id="b5786-111">Bu alıştırmanın ilerisinde şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="b5786-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="b5786-112">Nasıl tooconnect Intel NUC çevre birimleri ile.</span><span class="sxs-lookup"><span data-stu-id="b5786-112">How tooconnect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="b5786-113">Nasıl Intel NUC kullanma tooinstall ve güncelleştirme gerekli hello paketleri akıllı Paket Yöneticisi hello.</span><span class="sxs-lookup"><span data-stu-id="b5786-113">How tooinstall and update hello required packages on Intel NUC using hello Smart Package Manager.</span></span>
- <span data-ttu-id="b5786-114">Nasıl toorun hello "hello_world" uygulama tooverify hello ağ geçidi işlevselliği örnek.</span><span class="sxs-lookup"><span data-stu-id="b5786-114">How toorun hello "hello_world" sample application tooverify hello gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b5786-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="b5786-115">What you need</span></span>

- <span data-ttu-id="b5786-116">Bir Intel NUC Seti DE3815TYKE hello Intel IOT ağ geçidi yazılım paketi ile (Rüzgar Akarsu Linux * 7.0.0.13) önceden yüklenmiş.</span><span class="sxs-lookup"><span data-stu-id="b5786-116">An Intel NUC Kit DE3815TYKE with hello Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span>
- <span data-ttu-id="b5786-117">Ethernet kablosu.</span><span class="sxs-lookup"><span data-stu-id="b5786-117">An Ethernet cable.</span></span>
- <span data-ttu-id="b5786-118">Klavye.</span><span class="sxs-lookup"><span data-stu-id="b5786-118">A keyboard.</span></span>
- <span data-ttu-id="b5786-119">Bir HDMI veya VGA kablosu.</span><span class="sxs-lookup"><span data-stu-id="b5786-119">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="b5786-120">Bir HDMI veya VGA bağlantı noktasına sahip bir izleme.</span><span class="sxs-lookup"><span data-stu-id="b5786-120">A monitor with an HDMI or VGA port.</span></span>

![Ağ geçidi Seti](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a><span data-ttu-id="b5786-122">Intel NUC hello çevre ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="b5786-122">Connect Intel NUC with hello peripherals</span></span>

<span data-ttu-id="b5786-123">Aşağıdaki Hello görüntü ile çeşitli çevre bağlı Intel NUC örneğidir:</span><span class="sxs-lookup"><span data-stu-id="b5786-123">hello image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="b5786-124">Bağlı tooa klavye.</span><span class="sxs-lookup"><span data-stu-id="b5786-124">Connected tooa keyboard.</span></span>
2. <span data-ttu-id="b5786-125">Toohello İzleyici VGA kablosu veya HDMI kablo tarafından bağlı.</span><span class="sxs-lookup"><span data-stu-id="b5786-125">Connected toohello monitor by a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="b5786-126">Kablolu ağ tarafından Ethernet kablosu bağlı tooa.</span><span class="sxs-lookup"><span data-stu-id="b5786-126">Connected tooa wired network by an Ethernet cable.</span></span>
4. <span data-ttu-id="b5786-127">Güç kablosu bağlı toohello güç kaynakları.</span><span class="sxs-lookup"><span data-stu-id="b5786-127">Connected toohello power supply with a power cable.</span></span>

![Intel NUC tooperipherals bağlı](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="b5786-129">Ana bilgisayar üzerinden güvenli Kabuk (SSH) toohello Intel NUC sistem bağlayın</span><span class="sxs-lookup"><span data-stu-id="b5786-129">Connect toohello Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="b5786-130">Burada NUC Cihazınızı klavye ve monitör tooget başlangıç IP adresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b5786-130">Here you need keyboard and monitor tooget hello IP address of your NUC device.</span></span> <span data-ttu-id="b5786-131">Merhaba IP biliyorsanız adresi toostep 3'te bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b5786-131">If you already know hello IP address, you can skip toostep 3 in this section.</span></span>

1. <span data-ttu-id="b5786-132">Intel NUC üzerinde hello güç düğmesi ve günlük hello sistemde tuşlarına basarak kapatın.</span><span class="sxs-lookup"><span data-stu-id="b5786-132">Turn on Intel NUC by pressing hello Power button and log in hello system.</span></span>

   <span data-ttu-id="b5786-133">Merhaba varsayılan kullanıcı adı ve parola olan her ikisi de `root`.</span><span class="sxs-lookup"><span data-stu-id="b5786-133">hello default user name and password are both `root`.</span></span>

2. <span data-ttu-id="b5786-134">Merhaba çalıştırarak NUC Hello IP adresini alın `ifconfig` komutu.</span><span class="sxs-lookup"><span data-stu-id="b5786-134">Get hello IP address of NUC by running hello `ifconfig` command.</span></span> <span data-ttu-id="b5786-135">Bu adım hello NUC aygıtta yapılır.</span><span class="sxs-lookup"><span data-stu-id="b5786-135">This step is done on hello NUC device.</span></span>

   <span data-ttu-id="b5786-136">Merhaba komutu çıktısı bir örneği burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b5786-136">Here is an example of hello command output.</span></span>

   ![NUC IP gösteren ifconfig çıktı](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="b5786-138">Bu örnekte, aşağıdaki değer hello `inet addr:` tooconnect uzaktan bir ana bilgisayar tooIntel NUC gelen planlarken, gereksinim duyduğunuz hello IP adresidir.</span><span class="sxs-lookup"><span data-stu-id="b5786-138">In this example, hello value that follows `inet addr:` is hello IP address that you need when you plan tooconnect remotely from a host computer tooIntel NUC.</span></span>

3. <span data-ttu-id="b5786-139">SSH istemcilerini, ana makine tooconnect tooIntel NUC aşağıdaki hello birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="b5786-139">Use one of hello following SSH clients from your host machine tooconnect tooIntel NUC.</span></span>

   - <span data-ttu-id="b5786-140">[PuTTY](http://www.putty.org/) Windows için.</span><span class="sxs-lookup"><span data-stu-id="b5786-140">[PuTTY](http://www.putty.org/) for Windows.</span></span>
   - <span data-ttu-id="b5786-141">Merhaba yapı içinde SSH istemcisi Ubuntu veya macOS.</span><span class="sxs-lookup"><span data-stu-id="b5786-141">hello build-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="b5786-142">Bir ana bilgisayardan Intel NUC üzerinde daha etkili ve verimli toooperate olur.</span><span class="sxs-lookup"><span data-stu-id="b5786-142">It is more efficient and productive toooperate on Intel NUC from a host computer.</span></span> <span data-ttu-id="b5786-143">Merhaba hello IP adresi, kullanıcı adı ve parola gerekir SSH istemcisi tooconnect hello NUC.</span><span class="sxs-lookup"><span data-stu-id="b5786-143">You need hello hello IP address, user name and password tooconnect hello NUC via SSH client.</span></span> <span data-ttu-id="b5786-144">MacOS üzerinde hello örnek kullanım SSH istemcisi İşte.</span><span class="sxs-lookup"><span data-stu-id="b5786-144">Here is hello example use SSH client on macOS.</span></span>
   <span data-ttu-id="b5786-145">![MacOS üzerinde çalışan SSH istemcisi](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="b5786-145">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-hello-azure-iot-edge-package"></a><span data-ttu-id="b5786-146">Hello Azure IOT kenar paketini yükle</span><span class="sxs-lookup"><span data-stu-id="b5786-146">Install hello Azure IoT Edge package</span></span>

<span data-ttu-id="b5786-147">Hello Azure IOT kenar paket hello önceden derlenmiş ikili dosyaları hello SDK ve onun bağımlılıklarını içerir.</span><span class="sxs-lookup"><span data-stu-id="b5786-147">hello Azure IoT Edge package contains hello pre-compiled binaries of hello SDK and its dependencies.</span></span> <span data-ttu-id="b5786-148">Bu ikili dosyaları, Azure IOT kenar, hello Azure IOT SDK'sı ve hello karşılık gelen araçlar vardır.</span><span class="sxs-lookup"><span data-stu-id="b5786-148">These binaries are Azure IoT Edge, hello Azure IoT SDK and hello corresponding tools.</span></span> <span data-ttu-id="b5786-149">Merhaba paket kullanılan toovalidate hello ağ geçidi işlevi "hello_world" örnek bir uygulama da içerir.</span><span class="sxs-lookup"><span data-stu-id="b5786-149">hello package also contains a "hello_world" sample application that is used toovalidate hello gateway functionality.</span></span> <span data-ttu-id="b5786-150">IOT kenar hello çekirdek hello ağ geçidi parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="b5786-150">IoT Edge is hello core part of hello gateway.</span></span> <span data-ttu-id="b5786-151">tooinstall hello paketini, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="b5786-151">tooinstall hello package, follow these steps:</span></span>

1. <span data-ttu-id="b5786-152">Bir terminal penceresi komutlarda aşağıdaki hello çalıştırarak Hello IOT bulut deposunu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b5786-152">Add hello IoT cloud repository by running hello following commands in a terminal window:</span></span>

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   <span data-ttu-id="b5786-153">Merhaba `rpm` içeri aktarmalar hello rpm anahtar komutu.</span><span class="sxs-lookup"><span data-stu-id="b5786-153">hello `rpm` command imports hello rpm key.</span></span> <span data-ttu-id="b5786-154">Merhaba `smart channel` komut ekler hello rpm kanal toohello akıllı Paket Yöneticisi.</span><span class="sxs-lookup"><span data-stu-id="b5786-154">hello `smart channel` command adds hello rpm channel toohello Smart Package Manager.</span></span> <span data-ttu-id="b5786-155">Merhaba çalıştırmadan önce `smart update` komutu, gördüğünüz gibi bir çıktı aşağıda.</span><span class="sxs-lookup"><span data-stu-id="b5786-155">Before you run hello `smart update` command, you see an output like below.</span></span>

   ![RPM ve akıllı kanal komutları çıkış](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. <span data-ttu-id="b5786-157">Merhaba aşağıdaki komutu çalıştırarak Hello paketini yükle:</span><span class="sxs-lookup"><span data-stu-id="b5786-157">Install hello package by running hello following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="b5786-158">`packagegroup-cloud-azure`Merhaba paket Hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="b5786-158">`packagegroup-cloud-azure` is hello name of hello package.</span></span> <span data-ttu-id="b5786-159">Merhaba `smart install` kullanılan tooinstall hello paket komuttur.</span><span class="sxs-lookup"><span data-stu-id="b5786-159">hello `smart install` command is used tooinstall hello package.</span></span>

   <span data-ttu-id="b5786-160">Merhaba paket yüklendikten sonra Intel NUC beklenen toowork bir ağ geçidi olarak var.</span><span class="sxs-lookup"><span data-stu-id="b5786-160">After hello package is installed, Intel NUC is expected toowork as a gateway.</span></span>

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="b5786-161">Hello Azure IOT kenar "hello_world" örnek uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="b5786-161">Run hello Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="b5786-162">Çok Git`azureiotgatewaysdk/samples` ve hello örnek "hello_world" örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b5786-162">Go too`azureiotgatewaysdk/samples` and run hello sample "hello_world" sample application.</span></span> <span data-ttu-id="b5786-163">Bu örnek uygulama ağ geçidi hello oluşturur `hello_world.json` dosya ve 5 saniyede hello temel bileşenlerini hello Azure IOT kenar mimarisi toolog hello world ileti tooa dosyası kullanır.</span><span class="sxs-lookup"><span data-stu-id="b5786-163">This sample application creates a gateway from hello `hello_world.json` file and uses hello fundamental components of hello Azure IoT Edge architecture toolog a hello world message tooa file every 5 seconds.</span></span>

<span data-ttu-id="b5786-164">Merhaba aşağıdaki komutu çalıştırarak hello örnek "hello_world" örnek uygulama çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b5786-164">You can run hello sample "hello_world" sample application by running hello following command:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="b5786-165">Merhaba örnek uygulaması hello aşağıdaki hello ağ geçidi işlevini düzgün çalışıp çalışmadığını çıktı üretir:</span><span class="sxs-lookup"><span data-stu-id="b5786-165">hello sample application produces hello following output if hello gateway functionality is working correctly:</span></span>

![Uygulama çıktısı](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

<span data-ttu-id="b5786-167">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="b5786-167">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="b5786-168">Özet</span><span class="sxs-lookup"><span data-stu-id="b5786-168">Summary</span></span>

<span data-ttu-id="b5786-169">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="b5786-169">Congratulations!</span></span> <span data-ttu-id="b5786-170">Intel NUC ayarlama bir ağ geçidi olarak tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="b5786-170">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="b5786-171">Hazır artık toomove toohello sonraki Ders tooset, ana bilgisayar üzerinde Azure IOT hub oluşturma ve Azure IOT hub'ı mantıksal Cihazınızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b5786-171">Now you're ready toomove on toohello next lesson tooset up your host computer, create an Azure IoT hub and register your Azure IoT hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5786-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b5786-172">Next steps</span></span>
[<span data-ttu-id="b5786-173">Ana bilgisayar ve Azure IOT hub'ı hazırlanın</span><span class="sxs-lookup"><span data-stu-id="b5786-173">Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
