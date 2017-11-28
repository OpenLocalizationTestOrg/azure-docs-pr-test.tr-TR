---
title: "Connect Raspberry pi (C) tooAzure IOT - sorunlarını giderme | Microsoft Docs"
description: "Sayfa hello Raspberry Pi Node.js deneyimi için sorun giderme"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IOT sorunları, Internet şeyler sorunları"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 22cf50dc-8206-42a2-a1fc-f75fa85135fa
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8f0807104550e8e53a132f7741564b33f1db17ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="2d93d-104">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="2d93d-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="2d93d-105">Donanım sorunları</span><span class="sxs-lookup"><span data-stu-id="2d93d-105">Hardware issues</span></span>
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a><span data-ttu-id="2d93d-106">çalıştırır yanı sıra ancak LED hello Merhaba uygulaması yanıp sönen değil</span><span class="sxs-lookup"><span data-stu-id="2d93d-106">hello application runs well but hello LED is not blinking</span></span>
<span data-ttu-id="2d93d-107">Bu her zaman ilgili toohardware hattı bağlantı sorunudur.</span><span class="sxs-lookup"><span data-stu-id="2d93d-107">This issue is always related toohardware circuit connectivity.</span></span> <span data-ttu-id="2d93d-108">Aşağıdaki adımları tooidentify sorunları hello kullan:</span><span class="sxs-lookup"><span data-stu-id="2d93d-108">Use hello following steps tooidentify problems:</span></span>

1. <span data-ttu-id="2d93d-109">Merhaba doğru seçtiğiniz denetleyin **GPIO'yu** panonuzu üzerinde.</span><span class="sxs-lookup"><span data-stu-id="2d93d-109">Check that you chose hello correct **GPIO** on your board.</span></span> <span data-ttu-id="2d93d-110">Merhaba iki bağlantı noktası olmalıdır **GPIO'yu GND (PIN 6)** ve **GPIO'yu 04 (PIN 7)**.</span><span class="sxs-lookup"><span data-stu-id="2d93d-110">hello two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="2d93d-111">Merhaba polarite, LED, doğru olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="2d93d-111">Check that hello polarity of your LED is correct.</span></span> <span data-ttu-id="2d93d-112">Merhaba uzun leg hello belirtmek **pozitif**, Number PIN.</span><span class="sxs-lookup"><span data-stu-id="2d93d-112">hello longer leg should indicate hello **positive**, anode pin.</span></span>
3. <span data-ttu-id="2d93d-113">Kullanım hello **3, 3v PIN** ve **GND PIN** Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="2d93d-113">Use hello **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="2d93d-114">Pi DC Güç hello kabul eder.</span><span class="sxs-lookup"><span data-stu-id="2d93d-114">Treat Pi as hello DC power.</span></span> <span data-ttu-id="2d93d-115">Bu hello LED düzgün çalışır denetleyin.</span><span class="sxs-lookup"><span data-stu-id="2d93d-115">Check that hello LED works fine.</span></span>

![LED belirtimi](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="2d93d-117">Diğer donanım sorunları</span><span class="sxs-lookup"><span data-stu-id="2d93d-117">Other hardware issues</span></span>
<span data-ttu-id="2d93d-118">Merhaba Raspberry Pi 3'te sık karşılaşılan sorunları giderme hakkında daha fazla bilgi için bkz: [resmi sorun giderme sayfa](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="2d93d-118">For information about solving common problems on Raspberry Pi 3, see hello [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="2d93d-119">Node.js paket sorunları</span><span class="sxs-lookup"><span data-stu-id="2d93d-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="2d93d-120">Gulp görevler sırasında yanıt yok</span><span class="sxs-lookup"><span data-stu-id="2d93d-120">No response during gulp tasks</span></span>
<span data-ttu-id="2d93d-121">Çalışan gulp görevleri sorunlarla karşılaşırsanız, hello ekleyebilirsiniz `--verbose` hata ayıklama seçeneği.</span><span class="sxs-lookup"><span data-stu-id="2d93d-121">If you encounter problems in running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="2d93d-122">Ctrl + C'ı kullanarak tooterminate geçerli gulp görevleri deneyin ve ardından konsol penceresinde toosee hata ayıklama iletileri komutunda aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2d93d-122">Try tooterminate current gulp tasks by using Ctrl + C, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="2d93d-123">Ayrıntılı hata iletileri, konsol çıktısı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2d93d-123">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="2d93d-124">Aygıt Bulma sorunları</span><span class="sxs-lookup"><span data-stu-id="2d93d-124">Device discovery issues</span></span>
<span data-ttu-id="2d93d-125">İlgili hello ortak sorunları gidermede yardım için `devdisco` komutu, hello denetleyin [Benioku](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="2d93d-125">For help in troubleshooting common problems with hello `devdisco` command, check hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="2d93d-126">npm sorunları</span><span class="sxs-lookup"><span data-stu-id="2d93d-126">npm issues</span></span>
<span data-ttu-id="2d93d-127">Tooupdate komutu aşağıdaki hello kullanarak npm paket deneyin:</span><span class="sxs-lookup"><span data-stu-id="2d93d-127">Try tooupdate your npm package by using hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="2d93d-128">Merhaba sorun devam ederse, bu makalenin hello sonunda yorumlarınızı bırakın veya bir GitHub sorunu oluşturmak bizim [örnek depo](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span><span class="sxs-lookup"><span data-stu-id="2d93d-128">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="2d93d-129">Uzaktan hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="2d93d-129">Remote debugging</span></span>
### <a name="run-hello-sample-application-in-debug-mode"></a><span data-ttu-id="2d93d-130">Hata ayıklama modunda Hello örnek uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="2d93d-130">Run hello sample application in debug mode</span></span>
```bash
gulp run --debug
```

<span data-ttu-id="2d93d-131">Merhaba hata ayıklama altyapısı hazır olduğunda, görmelisiniz ```Debugger listening on port 5858``` hello konsol çıkışı.</span><span class="sxs-lookup"><span data-stu-id="2d93d-131">When hello debug engine is ready, you should see ```Debugger listening on port 5858``` in hello console output.</span></span>

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a><span data-ttu-id="2d93d-132">Visual Studio Code tooconnect toohello uzak aygıt yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2d93d-132">Configure Visual Studio Code tooconnect toohello remote device</span></span>
1. <span data-ttu-id="2d93d-133">Açık hello **hata ayıklama** hello yan sol panelde.</span><span class="sxs-lookup"><span data-stu-id="2d93d-133">Open hello **Debug** panel on hello left side.</span></span>
2. <span data-ttu-id="2d93d-134">Merhaba yeşil tıklatın **hata ayıklamayı Başlat** (F5) düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2d93d-134">Click hello green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="2d93d-135">Visual Studio Code Launch.json'u dosyasını açar.</span><span class="sxs-lookup"><span data-stu-id="2d93d-135">Visual Studio Code opens a launch.json file.</span></span>
3. <span data-ttu-id="2d93d-136">Merhaba Launch.json'u dosya içeriği aşağıdaki hello ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="2d93d-136">Update hello launch.json file with hello following content.</span></span> <span data-ttu-id="2d93d-137">Değiştir `[device hostname or IP address]` Merhaba, gerçek cihaz IP adresi veya ana bilgisayar adı ile.</span><span class="sxs-lookup"><span data-stu-id="2d93d-137">Replace `[device hostname or IP address]` with hello actual device IP address or host name.</span></span>

> [!NOTE]
> <span data-ttu-id="2d93d-138">Merhaba Visual Studio hata ayıklama, hakkında daha fazla toolearn başvurun çok[Visual Studio kodda hata ayıklama](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span><span class="sxs-lookup"><span data-stu-id="2d93d-138">toolearn more about hello Visual Studio Debugging, please refer too[Debugging in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span></span>


```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Attach",
            "type": "node",
            "request": "attach",
            "port": 5858,
            "address": "[device hostname or IP address]",
            "restart": false,
            "sourceMaps": false,
            "outDir": null,
            "localRoot": "${workspaceRoot}",
            "remoteRoot": null
        }
    ]
}
```

![Uzaktan hata ayıklama yapılandırması](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a><span data-ttu-id="2d93d-140">Toohello uzak uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="2d93d-140">Attach toohello remote application</span></span>
<span data-ttu-id="2d93d-141">Merhaba yeşil tıklatın **hata ayıklamayı Başlat** (F5) düğmesini toostart hata ayıklama.</span><span class="sxs-lookup"><span data-stu-id="2d93d-141">Click hello green **Start Debugging** (F5) button toostart debugging.</span></span>

<span data-ttu-id="2d93d-142">Okuma [JavaScript VS code'da](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn hello hata ayıklayıcı hakkında daha fazla.</span><span class="sxs-lookup"><span data-stu-id="2d93d-142">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn more about hello debugger.</span></span>

![Uzaktan etkileşimli hata ayıklama](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="2d93d-144">Azure CLI sorunları</span><span class="sxs-lookup"><span data-stu-id="2d93d-144">Azure CLI issues</span></span>
<span data-ttu-id="2d93d-145">Hello Azure komut satırı arabirimi (Azure CLI) önizleme yapıdır.</span><span class="sxs-lookup"><span data-stu-id="2d93d-145">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="2d93d-146">tooseek çözümleri hello kullanabilir [Önizleme Yükleme Kılavuzu](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="2d93d-146">tooseek solutions, you can use hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="2d93d-147">Tüm hatalar hello aracı ile karşılaşırsanız, dosya bir [sorunu](https://github.com/Azure/azure-cli/issues) hello içinde **sorunları** hello GitHub deposuna bölümü.</span><span class="sxs-lookup"><span data-stu-id="2d93d-147">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="2d93d-148">Sık karşılaşılan sorunları giderme konusunda yardım için hello denetleyin [Benioku](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="2d93d-148">For help in troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

## <a name="python-installation-issues"></a><span data-ttu-id="2d93d-149">Python yükleme sorunları</span><span class="sxs-lookup"><span data-stu-id="2d93d-149">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="2d93d-150">Eski yükleme sorunları (macOS)</span><span class="sxs-lookup"><span data-stu-id="2d93d-150">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="2d93d-151">PIP yüklüyorsanız, eski paketleri ile yüklendiğinde izin hatası atılır **su** izinleri.</span><span class="sxs-lookup"><span data-stu-id="2d93d-151">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="2d93d-152">Python brew (macOS) kullanarak önceki bir yüklemesini tümüyle kaldırılmamış. Bu durum oluşur.</span><span class="sxs-lookup"><span data-stu-id="2d93d-152">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="2d93d-153">Önceki yüklemeye ait bazı PIP paketler hello izni hatasına neden oluyor kök tarafından oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="2d93d-153">Some pip packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="2d93d-154">Merhaba çözüm tooremove bu paketleri kök tarafından yüklü değil.</span><span class="sxs-lookup"><span data-stu-id="2d93d-154">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="2d93d-155">Aşağıdaki adımları toocomplete hello bu görevi kullanın:</span><span class="sxs-lookup"><span data-stu-id="2d93d-155">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="2d93d-156">Gidin: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="2d93d-156">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="2d93d-157">Kök tarafından oluşturulan listesi paketler:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="2d93d-157">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="2d93d-158">Paketler, adım 2 ' Kaldır:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="2d93d-158">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="2d93d-159">Python yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2d93d-159">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="2d93d-160">Azure IOT hub'ı sorunları</span><span class="sxs-lookup"><span data-stu-id="2d93d-160">Azure IoT Hub issues</span></span>
<span data-ttu-id="2d93d-161">Azure CLI ile Azure IOT hub'ınızı başarıyla kaynak sağlandı ve tooyour IOT hub'a bağlanan bir aracı toomanage hello aygıtları ihtiyacınız varsa araçları aşağıdaki hello deneyin.</span><span class="sxs-lookup"><span data-stu-id="2d93d-161">If you've successfully provisioned your Azure IoT hub with Azure CLI, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="2d93d-162">Cihaz Gezgini</span><span class="sxs-lookup"><span data-stu-id="2d93d-162">Device explorer</span></span>
<span data-ttu-id="2d93d-163">Merhaba [aygıt explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) aracı Windows yerel makinenizde çalıştırır ve azure'da tooyour IOT hub'ı bağlar.</span><span class="sxs-lookup"><span data-stu-id="2d93d-163">hello [Device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) tool runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="2d93d-164">Merhaba aşağıdaki ile iletişim kurar [IOT Hub uç noktaları](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="2d93d-164">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>


* <span data-ttu-id="2d93d-165">*Cihaz Kimlik Yönetimi* tooprovision ve IOT hub'ınıza kayıtlı cihazları yönetme.</span><span class="sxs-lookup"><span data-stu-id="2d93d-165">*Device identity management* tooprovision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="2d93d-166">*Cihaz bulut alma* aygıt tooyour IOT hub'dan gönderilen iletileri izleyebilmek.</span><span class="sxs-lookup"><span data-stu-id="2d93d-166">*Receive device-to-cloud* so you can monitor messages sent from your device tooyour IoT hub.</span></span>
* <span data-ttu-id="2d93d-167">*Bulut cihaz Gönder* IOT hub'ından tooyour aygıtları iletileri gönderebilmesi.</span><span class="sxs-lookup"><span data-stu-id="2d93d-167">*Send cloud-to-device* so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="2d93d-168">IOT hub bağlantı dizenizi bu aracı toouse içindeki tüm özelliklerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2d93d-168">Configure your IoT hub connection string within this tool toouse all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="2d93d-169">ıothub Gezgini</span><span class="sxs-lookup"><span data-stu-id="2d93d-169">iothub-explorer</span></span>
<span data-ttu-id="2d93d-170">[ıothub explorer](https://github.com/Azure/iothub-explorer) bir örnek çok platformlu CLI toomanage aygıtları aracıdır.</span><span class="sxs-lookup"><span data-stu-id="2d93d-170">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage devices.</span></span> <span data-ttu-id="2d93d-171">Merhaba kimlik kayıt defterinde hello aracı toomanage hello aygıtları'nı kullanın, cihaz bulut iletilerini izlemek ve bulut-cihaz iletilerini göndermek.</span><span class="sxs-lookup"><span data-stu-id="2d93d-171">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device messages.</span></span>

<span data-ttu-id="2d93d-172">tooinstall hello ıothub explorer aracı, aşağıdaki komut, komut satırı ortamınızdaki hello çalıştırın (ön) en son sürümünü hello:</span><span class="sxs-lookup"><span data-stu-id="2d93d-172">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="2d93d-173">Tüm hakkında ek Yardım tooget iothub-explorer komutlar ve bunların parametrelerini hello komutu aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2d93d-173">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="2d93d-174">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="2d93d-174">Azure portal</span></span>
<span data-ttu-id="2d93d-175">Tam CLI deneyimi oluşturma ve Azure kaynaklarınızı yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="2d93d-175">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="2d93d-176">Toouse hello isteyebilirsiniz [Azure portal](../azure-portal-overview.md) toohelp sağlamanıza, yönetmek ve Azure kaynaklarınızı hata ayıklama.</span><span class="sxs-lookup"><span data-stu-id="2d93d-176">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="2d93d-177">Azure depolama sorunları</span><span class="sxs-lookup"><span data-stu-id="2d93d-177">Azure Storage issues</span></span>
<span data-ttu-id="2d93d-178">[Microsoft Azure Storage Gezgini (Önizleme)](http://storageexplorer.com) toowork Windows, macOS ve Linux Azure Storage veri ile kullanabileceğiniz Microsoft tek başına uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="2d93d-178">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="2d93d-179">Bu aracı kullanarak tooyour tablo bağlanabilir ve hello verilerde bakın.</span><span class="sxs-lookup"><span data-stu-id="2d93d-179">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="2d93d-180">Bu aracı tootroubleshoot Azure depolama sorunlarınızı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2d93d-180">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

