---
title: "Connect Raspberry pi (C) tooAzure IOT - sorunlarını giderme | Microsoft Docs"
description: "Sayfa Raspberry Pi Node.js deneyimi için sorun giderme"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IOT sorunları, Internet şeyler sorunları"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 3653c79b-8a0c-41d4-b0bf-f6b4edb4d233
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4f1ea81dd25d10a39c2939f5ee5f19f6d2ba2b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="ef6ba-104">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="ef6ba-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="ef6ba-105">Donanım sorunları</span><span class="sxs-lookup"><span data-stu-id="ef6ba-105">Hardware issues</span></span>
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a><span data-ttu-id="ef6ba-106">çalıştırır yanı sıra ancak LED hello Merhaba uygulaması yanıp sönen değil</span><span class="sxs-lookup"><span data-stu-id="ef6ba-106">hello application runs well but hello LED is not blinking</span></span>
<span data-ttu-id="ef6ba-107">Bu her zaman ilgili toohello donanım hattı bağlantı sorunudur.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-107">This issue is always related toohello hardware circuit connectivity.</span></span> <span data-ttu-id="ef6ba-108">Aşağıdaki adımları tooidentify sorunları hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-108">Use hello following steps tooidentify problems.</span></span>

1. <span data-ttu-id="ef6ba-109">Merhaba doğru seçtiğiniz denetleyin **GPIO'yu** panonuzu üzerinde.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-109">Check that you chose hello correct **GPIO** on your board.</span></span> <span data-ttu-id="ef6ba-110">Merhaba iki bağlantı noktası olmalıdır **GPIO'yu GND (PIN 6)** ve **GPIO'yu 04 (PIN 7)**.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-110">hello two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="ef6ba-111">Merhaba polarite, LED, doğru olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-111">Check that hello polarity of your LED is correct.</span></span> <span data-ttu-id="ef6ba-112">Merhaba uzun leg hello belirtmek **pozitif**, Number PIN.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-112">hello longer leg should indicate hello **positive**, anode pin.</span></span>
3. <span data-ttu-id="ef6ba-113">Kullanım hello **3, 3v PIN** ve **GND PIN** Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-113">Use hello **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="ef6ba-114">Pi DC Güç hello kabul eder.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-114">Treat Pi as hello DC power.</span></span> <span data-ttu-id="ef6ba-115">Bu hello LED düzgün çalışır denetleyin.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-115">Check that hello LED works fine.</span></span>

![LED belirtimi](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="ef6ba-117">Diğer donanım sorunları</span><span class="sxs-lookup"><span data-stu-id="ef6ba-117">Other hardware issues</span></span>
<span data-ttu-id="ef6ba-118">Merhaba Raspberry Pi 3'te sık karşılaşılan sorunları giderme hakkında daha fazla bilgi için bkz: [resmi sorun giderme sayfa](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="ef6ba-118">For information about solving common problems on Raspberry Pi 3, see hello [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="ef6ba-119">Node.js paket sorunları</span><span class="sxs-lookup"><span data-stu-id="ef6ba-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="ef6ba-120">Gulp görevler sırasında yanıt yok</span><span class="sxs-lookup"><span data-stu-id="ef6ba-120">No response during gulp tasks</span></span>
<span data-ttu-id="ef6ba-121">Çalışan gulp görevleri sorunlarla karşılaşırsanız, hello ekleyebilirsiniz `--verbose` hata ayıklama seçeneği.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-121">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="ef6ba-122">Tooterminate geçerli gulp görevleri kullanarak deneyin `Ctrl + C`, ve ardından çalışma hello aşağıdaki konsol penceresi toosee hata ayıklama iletileri komutu.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-122">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="ef6ba-123">Ayrıntılı hata iletileri, konsol çıktısı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-123">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="ef6ba-124">Aygıt Bulma sorunları</span><span class="sxs-lookup"><span data-stu-id="ef6ba-124">Device discovery issues</span></span>
<span data-ttu-id="ef6ba-125">İlgili hello ortak sorunları gidermede yardım için `devdisco` komutu, hello denetleyin [Benioku](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="ef6ba-125">For help in troubleshooting common problems with hello `devdisco` command, check hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="ef6ba-126">NPM sorunları</span><span class="sxs-lookup"><span data-stu-id="ef6ba-126">NPM issues</span></span>
<span data-ttu-id="ef6ba-127">Tooupdate NPM paket komutu aşağıdaki hello ile deneyin:</span><span class="sxs-lookup"><span data-stu-id="ef6ba-127">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="ef6ba-128">Merhaba sorun devam ederse, bu makalenin hello sonunda yorumlarınızı bırakın veya bir GitHub sorunu oluşturmak bizim [örnek depo](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span><span class="sxs-lookup"><span data-stu-id="ef6ba-128">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="ef6ba-129">Uzaktan hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="ef6ba-129">Remote debugging</span></span>

<span data-ttu-id="ef6ba-130">Uzaktan hata ayıklama desteği yakında Visual Studio kod C/C++ uzantısı'nda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-130">Remote debugging support will be available soon in Visual Studio Code C/C++ Extension.</span></span>

<span data-ttu-id="ef6ba-131">Bir meanwhile, sık kullanılan SSH terminal GDB kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ef6ba-131">In a meanwhile you can use GDB via your favourite SSH terminal:</span></span>

```bash
cd c-pi-lesson-x
sudo gdb app
```

## <a name="azure-cli-issues"></a><span data-ttu-id="ef6ba-132">Azure CLI sorunları</span><span class="sxs-lookup"><span data-stu-id="ef6ba-132">Azure-CLI issues</span></span>
<span data-ttu-id="ef6ba-133">Hello Azure komut satırı arabirimi (Azure CLI) önizleme yapıdır.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-133">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="ef6ba-134">Merhaba çözümde arayın [Önizleme Yükleme Kılavuzu](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek çözümler.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-134">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="ef6ba-135">Komutları beklendiği gibi çalışmıyor olduğunda tooupgrade Azure CLI toolatest sürümünü deneyin.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-135">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="ef6ba-136">Tüm hatalar hello aracı ile karşılaşırsanız, dosya bir [sorunu](https://github.com/Azure/azure-cli/issues) hello içinde **sorunları** hello GitHub deposuna bölümü.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-136">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="ef6ba-137">Sık karşılaşılan sorunları gidermede yardım için hello denetleyin [Benioku](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="ef6ba-137">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="ef6ba-138">"Merhaba gereksinimini karşılayan bir sürüm bulunamadı", lütfen karşılıyorsa çalışma hello aşağıdaki tooupgrade PIP toolastest sürüm komutu.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-138">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="ef6ba-139">Python yükleme sorunları</span><span class="sxs-lookup"><span data-stu-id="ef6ba-139">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="ef6ba-140">Eski yükleme sorunları (macOS)</span><span class="sxs-lookup"><span data-stu-id="ef6ba-140">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="ef6ba-141">Ne zaman yüklüyorsanız **PIP**, eski paketleri olduğunda izin hatası atılır ile birlikte yüklenen **su** izinleri.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-141">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="ef6ba-142">Python brew (macOS) kullanarak önceki bir yüklemesini tümüyle kaldırılmamış. Bu durum oluşur.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-142">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="ef6ba-143">Bazı **PIP** önceki bir yükleme paketi hello izni hatasına neden oluyor kök tarafından oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-143">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="ef6ba-144">Merhaba çözüm tooremove bu paketleri kök tarafından yüklü değil.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-144">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="ef6ba-145">Aşağıdaki adımları toocomplete hello bu görevi kullanın:</span><span class="sxs-lookup"><span data-stu-id="ef6ba-145">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="ef6ba-146">Gidin: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="ef6ba-146">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="ef6ba-147">Liste paketleri kök tarafından oluşturun:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="ef6ba-147">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="ef6ba-148">Paketler, adım 2 ' Kaldır:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="ef6ba-148">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="ef6ba-149">Python yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-149">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="ef6ba-150">Azure IOT hub'ı sorunları</span><span class="sxs-lookup"><span data-stu-id="ef6ba-150">Azure IoT Hub issues</span></span>
<span data-ttu-id="ef6ba-151">Başarılı bir şekilde Azure IOT hub'ınıza sağladığınız varsa `azure-cli`, ve tooyour IOT hub'ı deneyin hello araçları aşağıdaki bağlanan bir aracı toomanage hello aygıtlarının gerekir:</span><span class="sxs-lookup"><span data-stu-id="ef6ba-151">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="ef6ba-152">Cihaz Gezgini</span><span class="sxs-lookup"><span data-stu-id="ef6ba-152">Device Explorer</span></span>
<span data-ttu-id="ef6ba-153">[Cihaz Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) Windows yerel makinenizde çalıştırır ve azure'da tooyour IOT hub'ı bağlar.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-153">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="ef6ba-154">Merhaba aşağıdaki ile iletişim kurar [IOT Hub uç noktaları](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="ef6ba-154">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="ef6ba-155">*Cihaz Kimlik Yönetimi* tooprovision ve IOT hub'ınıza kayıtlı cihazları yönetme.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-155">*Device identity management* tooprovision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="ef6ba-156">*Cihaz bulut alma* aygıt tooyour IOT hub'dan gönderilen iletileri izleyebilmek.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-156">*Receive device-to-cloud* so you can monitor messages sent from your device tooyour IoT hub.</span></span>
* <span data-ttu-id="ef6ba-157">*Bulut cihaz Gönder* IOT hub'ından tooyour aygıtları iletileri gönderebilmesi.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-157">*Send cloud-to-device* so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="ef6ba-158">Yapılandırma, `IoT hub connection string` bu aracı toouse içindeki tüm özellikleri.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-158">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="ef6ba-159">IOT hub'ı Gezgini</span><span class="sxs-lookup"><span data-stu-id="ef6ba-159">IoT hub Explorer</span></span>
<span data-ttu-id="ef6ba-160">[IOT hub'ı Explorer](https://github.com/Azure/iothub-explorer) bir örnek çok platformlu CLI toomanage aygıt istemcileri aracıdır.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-160">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="ef6ba-161">Merhaba kimlik kayıt defterinde hello aracı toomanage hello aygıtları'nı kullanın, cihaz bulut iletilerini izlemek ve bulut cihaza komut gönderme.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-161">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="ef6ba-162">tooinstall hello ıothub explorer aracı, aşağıdaki komut, komut satırı ortamınızdaki hello çalıştırın (ön) en son sürümünü hello:</span><span class="sxs-lookup"><span data-stu-id="ef6ba-162">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```
npm install -g iothub-explorer@latest
```

<span data-ttu-id="ef6ba-163">Tüm hakkında ek Yardım tooget iothub-explorer komutlar ve bunların parametrelerini hello komutu aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ef6ba-163">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="ef6ba-164">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="ef6ba-164">Azure portal</span></span>
<span data-ttu-id="ef6ba-165">Tam CLI deneyimi oluşturma ve Azure kaynaklarınızı yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-165">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="ef6ba-166">Toouse hello isteyebilirsiniz [Azure portal](../azure-portal-overview.md) toohelp sağlamanıza, yönetmek ve Azure kaynaklarınızı hata ayıklama.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-166">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="ef6ba-167">Azure depolama sorunları</span><span class="sxs-lookup"><span data-stu-id="ef6ba-167">Azure storage issues</span></span>
<span data-ttu-id="ef6ba-168">[Microsoft Azure Storage Gezgini (Önizleme)](http://storageexplorer.com) toowork Windows, macOS ve Linux Azure Storage veri ile kullanabileceğiniz Microsoft tek başına uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-168">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="ef6ba-169">Bu aracı kullanarak tooyour tablo bağlanabilir ve hello verilerde bakın.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-169">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="ef6ba-170">Bu aracı tootroubleshoot Azure depolama sorunlarınızı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef6ba-170">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>
