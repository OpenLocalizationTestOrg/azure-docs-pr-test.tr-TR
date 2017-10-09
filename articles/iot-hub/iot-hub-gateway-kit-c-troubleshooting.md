---
title: "SensorTag cihaz & Azure IOT ağ geçidi - sorunlarını giderme | Microsoft Docs"
description: "Sayfa Intel NUC ağ geçidi için sorun giderme"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IOT sorunları, Internet şeyler sorunları"
ROBOTS: NOINDEX
ms.assetid: 5f742c38-0e33-465a-9a0d-1e41e8d17187
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ed6812c60412afb615012e3d694051d009b149a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="00b6b-104">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="00b6b-104">Troubleshooting</span></span>

## <a name="hardware-issues"></a><span data-ttu-id="00b6b-105">Donanım sorunları</span><span class="sxs-lookup"><span data-stu-id="00b6b-105">Hardware issues</span></span>

### <a name="ti-sensortag-cannot-be-connected"></a><span data-ttu-id="00b6b-106">TI SensorTag bağlı</span><span class="sxs-lookup"><span data-stu-id="00b6b-106">TI SensorTag cannot be connected</span></span>

<span data-ttu-id="00b6b-107">tootroubleshoot SensorTag bağlantı sorunları, hello kullan [SensorTag uygulama](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span><span class="sxs-lookup"><span data-stu-id="00b6b-107">tootroubleshoot SensorTag connectivity issues, use hello [SensorTag app](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span></span>

### <a name="have-an-issue-with-intel-nuc"></a><span data-ttu-id="00b6b-108">Intel NUC ile ilgili bir sorun olması</span><span class="sxs-lookup"><span data-stu-id="00b6b-108">Have an issue with Intel NUC</span></span>

<span data-ttu-id="00b6b-109">tootroubleshoot önyükleme sorunlarını başvurmak çok[Intel NUC üzerinde Hayır önyükleme sorunlarını giderme](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span><span class="sxs-lookup"><span data-stu-id="00b6b-109">tootroubleshoot boot issues, refer too[troubleshooting No Boot Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span></span>

<span data-ttu-id="00b6b-110">tootroubleshoot işletim sistemi sorunları başvurmak çok[Intel NUC üzerinde işletim sistemi sorunlarını giderme](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span><span class="sxs-lookup"><span data-stu-id="00b6b-110">tootroubleshoot operating system issues, refer too[troubleshooting Operating System Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span></span>

<span data-ttu-id="00b6b-111">tootroubleshoot diğer sorunlar başvurmak çok[Blink kodları ve Intel NUC kodları bip sesi](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span><span class="sxs-lookup"><span data-stu-id="00b6b-111">tootroubleshoot other issues, refer too[Blink Codes and Beep Codes for Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="00b6b-112">Node.js paket sorunları</span><span class="sxs-lookup"><span data-stu-id="00b6b-112">Node.js package issues</span></span>

### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="00b6b-113">Gulp görevler sırasında yanıt yok</span><span class="sxs-lookup"><span data-stu-id="00b6b-113">No response during gulp tasks</span></span>

<span data-ttu-id="00b6b-114">Çalışan gulp görevleri sorunlarla karşılaşırsanız, hello ekleyebilirsiniz `--verbose` hata ayıklama seçeneği.</span><span class="sxs-lookup"><span data-stu-id="00b6b-114">If you encounter problems in running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="00b6b-115">Tooterminate geçerli gulp görevleri kullanarak deneyin `Ctrl + C`, ve ardından çalışma hello aşağıdaki konsol penceresi toosee hata ayıklama iletileri komutu.</span><span class="sxs-lookup"><span data-stu-id="00b6b-115">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="00b6b-116">Ayrıntılı hata iletileri, konsol çıktısı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00b6b-116">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="00b6b-117">Aygıt Bulma sorunları</span><span class="sxs-lookup"><span data-stu-id="00b6b-117">Device discovery issues</span></span>

<span data-ttu-id="00b6b-118">İlgili hello ortak sorunları gidermede yardım için `discover-sensortag` komutu, hello denetleyin [wiki sayfa](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span><span class="sxs-lookup"><span data-stu-id="00b6b-118">For help in troubleshooting common problems with hello `discover-sensortag` command, check hello [wiki page](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="00b6b-119">npm sorunları</span><span class="sxs-lookup"><span data-stu-id="00b6b-119">npm issues</span></span>

<span data-ttu-id="00b6b-120">Tooupdate hello aşağıdaki komutu çalıştırarak npm paket deneyin:</span><span class="sxs-lookup"><span data-stu-id="00b6b-120">Try tooupdate your npm package by running hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="00b6b-121">Merhaba sorun devam ederse, bu makalenin hello sonunda yorumlarınızı bırakın veya bir GitHub sorunu oluşturmak bizim [örnek depo](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span><span class="sxs-lookup"><span data-stu-id="00b6b-121">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="00b6b-122">Uzaktan hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="00b6b-122">Remote Debugging</span></span>
> <span data-ttu-id="00b6b-123">Bu öğreticide kullanılan node.js komut hata ayıklama için aşağıdaki yönergeleri yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="00b6b-123">Below instructions are meant for debugging node.js scripts used in this tutorial.</span></span>
### <a name="run-hello-sample-application-in-debug-mode"></a><span data-ttu-id="00b6b-124">Hata ayıklama modunda Hello örnek uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="00b6b-124">Run hello sample application in debug mode</span></span>

<span data-ttu-id="00b6b-125">Merhaba örnek uygulaması hello aşağıdaki komutu çalıştırarak hata ayıklama modunda çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="00b6b-125">Run hello sample application in debug mode by running hello following command:</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="00b6b-126">Merhaba hata ayıklama altyapısı hazır olduğunda, görmelisiniz `Debugger listening on port 5858` hello konsol çıkışı.</span><span class="sxs-lookup"><span data-stu-id="00b6b-126">When hello debug engine is ready, you should see `Debugger listening on port 5858` in hello console output.</span></span>

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a><span data-ttu-id="00b6b-127">Visual Studio Code tooconnect toohello uzak aygıt yapılandırma</span><span class="sxs-lookup"><span data-stu-id="00b6b-127">Configure Visual Studio Code tooconnect toohello remote device</span></span>

1. <span data-ttu-id="00b6b-128">Açık hello **hata ayıklama** hello yan sol panelde.</span><span class="sxs-lookup"><span data-stu-id="00b6b-128">Open hello **Debug** panel on hello left side.</span></span>
2. <span data-ttu-id="00b6b-129">Merhaba yeşil tıklatın **hata ayıklamayı Başlat** (F5) düğmesi.</span><span class="sxs-lookup"><span data-stu-id="00b6b-129">Click hello green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="00b6b-130">Visual Studio Code açılır bir `launch.json` dosyası.</span><span class="sxs-lookup"><span data-stu-id="00b6b-130">Visual Studio Code opens a `launch.json` file.</span></span>
3. <span data-ttu-id="00b6b-131">Güncelleştirme hello `launch.json` içeriği aşağıdaki hello dosyasıyla.</span><span class="sxs-lookup"><span data-stu-id="00b6b-131">Update hello `launch.json` file with hello following content.</span></span> <span data-ttu-id="00b6b-132">Değiştir `[device hostname or IP address]` Merhaba, gerçek cihaz IP adresi veya ana bilgisayar adı ile.</span><span class="sxs-lookup"><span data-stu-id="00b6b-132">Replace `[device hostname or IP address]` with hello actual device IP address or host name.</span></span>

   ``` json
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
            "remoteRoot": "~/ble_sample"
        }
     ]
   }
   ```

![Uzaktan hata ayıklama yapılandırması](./media/iot-hub-gateway-kit-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a><span data-ttu-id="00b6b-134">Toohello uzak uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="00b6b-134">Attach toohello remote application</span></span>

<span data-ttu-id="00b6b-135">Merhaba yeşil tıklatın **hata ayıklamayı Başlat** (F5) düğmesini toostart hata ayıklama.</span><span class="sxs-lookup"><span data-stu-id="00b6b-135">Click hello green **Start Debugging** (F5) button toostart debugging.</span></span>

<span data-ttu-id="00b6b-136">Okuma [JavaScript VS code'da](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn hello hata ayıklayıcı hakkında daha fazla.</span><span class="sxs-lookup"><span data-stu-id="00b6b-136">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn more about hello debugger.</span></span>

![Hata ayıklama bırak örnek](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="00b6b-138">Azure CLI sorunları</span><span class="sxs-lookup"><span data-stu-id="00b6b-138">Azure CLI issues</span></span>

<span data-ttu-id="00b6b-139">Hello Azure komut satırı arabirimi (Azure CLI) önizleme yapıdır.</span><span class="sxs-lookup"><span data-stu-id="00b6b-139">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="00b6b-140">tooseek çözümleri hello kullanabilir [Önizleme Yükleme Kılavuzu](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="00b6b-140">tooseek solutions, you can use hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="00b6b-141">Tüm hatalar hello aracı ile karşılaşırsanız, dosya bir [sorunu](https://github.com/Azure/azure-cli/issues) hello içinde **sorunları** hello GitHub deposuna bölümü.</span><span class="sxs-lookup"><span data-stu-id="00b6b-141">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="00b6b-142">Sık karşılaşılan sorunları giderme konusunda yardım için hello denetleyin [Benioku](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="00b6b-142">For help in troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="00b6b-143">"Merhaba gereksinimini karşılayan bir sürüm bulunamadı", lütfen karşılıyorsa çalışma hello aşağıdaki tooupgrade PIP toolastest sürüm komutu.</span><span class="sxs-lookup"><span data-stu-id="00b6b-143">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="00b6b-144">Python yükleme sorunları</span><span class="sxs-lookup"><span data-stu-id="00b6b-144">Python installation issues</span></span>

### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="00b6b-145">Eski yükleme sorunları (macOS)</span><span class="sxs-lookup"><span data-stu-id="00b6b-145">Legacy installation issues (macOS)</span></span>

<span data-ttu-id="00b6b-146">PIP yüklüyorsanız, eski paketleri ile yüklendiğinde izin hatası atılır **su** izinleri.</span><span class="sxs-lookup"><span data-stu-id="00b6b-146">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="00b6b-147">Python brew (macOS) kullanarak önceki bir yüklemesini tümüyle kaldırılmamış. Bu durum oluşur.</span><span class="sxs-lookup"><span data-stu-id="00b6b-147">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="00b6b-148">Önceki yüklemeye ait bazı PIP paketler hello izni hatasına neden oluyor kök tarafından oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="00b6b-148">Some pip packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="00b6b-149">Merhaba çözüm tooremove bu paketleri kök tarafından yüklü değil.</span><span class="sxs-lookup"><span data-stu-id="00b6b-149">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="00b6b-150">Aşağıdaki adımları toocomplete hello bu görevi kullanın:</span><span class="sxs-lookup"><span data-stu-id="00b6b-150">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="00b6b-151">Çok gidin`/usr/local/lib/python2.7/site-packages`</span><span class="sxs-lookup"><span data-stu-id="00b6b-151">Go too`/usr/local/lib/python2.7/site-packages`</span></span>
2. <span data-ttu-id="00b6b-152">Kök tarafından oluşturulan listesi paketler:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="00b6b-152">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="00b6b-153">Paketler, adım 2 ' Kaldır:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="00b6b-153">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="00b6b-154">Python yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="00b6b-154">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="00b6b-155">Azure IOT hub'ı sorunları</span><span class="sxs-lookup"><span data-stu-id="00b6b-155">Azure IoT Hub issues</span></span>

<span data-ttu-id="00b6b-156">Hello Azure CLI ile Azure IOT hub'ınızı başarıyla kaynak sağlandı ve tooyour IOT hub'a bağlanan bir aracı toomanage hello aygıtları ihtiyacınız varsa araçları aşağıdaki hello deneyin.</span><span class="sxs-lookup"><span data-stu-id="00b6b-156">If you've successfully provisioned your Azure IoT hub with hello Azure CLI, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="00b6b-157">Cihaz Gezgini</span><span class="sxs-lookup"><span data-stu-id="00b6b-157">Device Explorer</span></span>

<span data-ttu-id="00b6b-158">[Cihaz Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) Windows yerel makinenizde çalıştırır ve azure'da tooyour IOT hub'ı bağlar.</span><span class="sxs-lookup"><span data-stu-id="00b6b-158">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="00b6b-159">Merhaba aşağıdaki ile iletişim kurar [IOT Hub uç noktaları](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span><span class="sxs-lookup"><span data-stu-id="00b6b-159">It communicates with hello following [IoT Hub endpoints](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span></span>

- <span data-ttu-id="00b6b-160">Cihaz Kimlik Yönetimi tooprovision ve IOT hub'ınıza kayıtlı cihazları yönetme.</span><span class="sxs-lookup"><span data-stu-id="00b6b-160">Device identity management tooprovision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="00b6b-161">Cihaz bulut alır, böylece cihaz tooyour IOT hub'dan gönderilen iletileri izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00b6b-161">Receive device-to-cloud so you can monitor messages sent from your device tooyour IoT hub.</span></span>
- <span data-ttu-id="00b6b-162">IOT hub'ından tooyour aygıtları iletileri gönderebilmesi bulut cihaz gönderin.</span><span class="sxs-lookup"><span data-stu-id="00b6b-162">Send cloud-to-device so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="00b6b-163">IOT hub bağlantı dizenizi bu aracı toouse içindeki tüm özelliklerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="00b6b-163">Configure your IoT hub connection string within this tool toouse all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="00b6b-164">ıothub Gezgini</span><span class="sxs-lookup"><span data-stu-id="00b6b-164">iothub-explorer</span></span>

<span data-ttu-id="00b6b-165">[ıothub explorer](https://github.com/Azure/iothub-explorer) bir örnek çok platformlu CLI toomanage aygıt istemcileri aracıdır.</span><span class="sxs-lookup"><span data-stu-id="00b6b-165">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="00b6b-166">Merhaba kimlik kayıt defterinde hello aracı toomanage hello aygıtları'nı kullanın, cihaz bulut iletilerini izlemek ve bulut cihaza komut gönderme.</span><span class="sxs-lookup"><span data-stu-id="00b6b-166">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="00b6b-167">(tooinstall hello en son ön) sürümünü hello ıothub explorer aracı, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="00b6b-167">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="00b6b-168">Tüm hakkında ek Yardım tooget iothub-explorer komutlar ve bunların parametrelerini Merhaba, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="00b6b-168">tooget additional help about all hello iothub-explorer commands and their parameters, run hello following command:</span></span>

```bash
iothub-explorer help
```

### <a name="hello-azure-portal"></a><span data-ttu-id="00b6b-169">Hello Azure portalı</span><span class="sxs-lookup"><span data-stu-id="00b6b-169">hello Azure portal</span></span>

<span data-ttu-id="00b6b-170">Tam CLI deneyimi oluşturma ve Azure kaynaklarınızı yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="00b6b-170">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="00b6b-171">Toouse hello isteyebilirsiniz [Azure portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp sağlamanıza, yönetmek ve Azure kaynaklarınızı hata ayıklama.</span><span class="sxs-lookup"><span data-stu-id="00b6b-171">You might also want toouse hello [Azure portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="00b6b-172">Azure depolama sorunları</span><span class="sxs-lookup"><span data-stu-id="00b6b-172">Azure Storage issues</span></span>

<span data-ttu-id="00b6b-173">[Microsoft Azure Storage Gezgini (Önizleme)](http://storageexplorer.com/) toowork Windows, macOS ve Linux Azure Storage veri ile kullanabileceğiniz Microsoft tek başına uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="00b6b-173">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com/) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="00b6b-174">Bu aracı kullanarak tooyour tablo bağlanabilir ve hello verilerde bakın.</span><span class="sxs-lookup"><span data-stu-id="00b6b-174">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="00b6b-175">Bu aracı tootroubleshoot Azure depolama sorunlarınızı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00b6b-175">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>
