---
title: "Intel Edison'u (düğüm) tooAzure IOT - Ders 4 bağlanın: sorun giderme | Microsoft Docs"
description: "Sayfa Intel Edison'u Node.js deneyimi için sorun giderme"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino sorunlarını giderme"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: f11c5521-8a36-44c0-baad-f5ec26ab4618
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9502300f7f372255572b49bea45dd3e1fdaeeb37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="bd338-104">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="bd338-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="bd338-105">Donanım sorunları</span><span class="sxs-lookup"><span data-stu-id="bd338-105">Hardware issues</span></span>
<span data-ttu-id="bd338-106">Merhaba Intel Edison'u ortak sorunlarını çözme hakkında daha fazla bilgi için bkz [resmi sorun giderme sayfa](https://software.intel.com/en-us/node/637974).</span><span class="sxs-lookup"><span data-stu-id="bd338-106">For information about solving common problems on Intel Edison, see hello [official troubleshooting page](https://software.intel.com/en-us/node/637974).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="bd338-107">Node.js paket sorunları</span><span class="sxs-lookup"><span data-stu-id="bd338-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="bd338-108">Gulp görevler sırasında yanıt yok</span><span class="sxs-lookup"><span data-stu-id="bd338-108">No response during gulp tasks</span></span>
<span data-ttu-id="bd338-109">Çalışan gulp görevleri sorunlarla karşılaşırsanız, hello ekleyebilirsiniz `--verbose` hata ayıklama seçeneği.</span><span class="sxs-lookup"><span data-stu-id="bd338-109">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="bd338-110">Tooterminate geçerli gulp görevleri kullanarak deneyin `Ctrl + C`, ve ardından çalışma hello aşağıdaki konsol penceresi toosee hata ayıklama iletileri komutu.</span><span class="sxs-lookup"><span data-stu-id="bd338-110">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="bd338-111">Ayrıntılı hata iletileri, konsol çıktısı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd338-111">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="npm-issues"></a><span data-ttu-id="bd338-112">NPM sorunları</span><span class="sxs-lookup"><span data-stu-id="bd338-112">NPM issues</span></span>
<span data-ttu-id="bd338-113">Tooupdate NPM paket komutu aşağıdaki hello ile deneyin:</span><span class="sxs-lookup"><span data-stu-id="bd338-113">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="bd338-114">Merhaba sorun devam ederse, bu makalenin hello sonunda yorumlarınızı bırakın veya bir GitHub sorunu oluşturmak bizim [örnek depo][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="bd338-114">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="bd338-115">Uzaktan hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="bd338-115">Remote debugging</span></span>

### <a name="run-hello-sample-application-in-debug-mode"></a><span data-ttu-id="bd338-116">Hata ayıklama modunda Hello örnek uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="bd338-116">Run hello sample application in debug mode</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="bd338-117">Merhaba hata ayıklama altyapı hazır olduktan sonra mümkün toosee olmalıdır ```Debugger listening on port 5858``` hello konsol çıktısından.</span><span class="sxs-lookup"><span data-stu-id="bd338-117">Once hello debug engine is ready, you should be able toosee ```Debugger listening on port 5858``` from hello console output.</span></span>

### <a name="configure-vs-code-tooconnect-toohello-remote-device"></a><span data-ttu-id="bd338-118">VS Code'da tooconnect toohello uzak aygıt yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bd338-118">Configure VS Code tooconnect toohello remote device</span></span>

<span data-ttu-id="bd338-119">Açık hello **hata ayıklama** hello yan sol panelden.</span><span class="sxs-lookup"><span data-stu-id="bd338-119">Open hello **Debug** panel from hello left side.</span></span>

<span data-ttu-id="bd338-120">Merhaba yeşil tıklatın **hata ayıklamayı Başlat** (F5) düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bd338-120">Click hello green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="bd338-121">VS Code açmak bir **Launch.json'u** dosyası, hangi tooupdate gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd338-121">VS Code would open a **launch.json** file, which you need tooupdate.</span></span>

<span data-ttu-id="bd338-122">Güncelleştirme hello **Launch.json'u** aşağıdaki hello ile içerik dosya getirin, yerine `[device hostname or IP address]` hello gerçek cihazı IP adresi veya ana bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="bd338-122">Update hello **launch.json** file with hello following content, replace `[device hostname or IP address]` with hello actual device IP address or hostname.</span></span>  

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

![Uzaktan hata ayıklama yapılandırması](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a><span data-ttu-id="bd338-124">Toohello uzak uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="bd338-124">Attach toohello remote application</span></span>

<span data-ttu-id="bd338-125">Merhaba yeşil tıklatın **hata ayıklamayı Başlat** (F5) düğmesine tıklayın ve hata ayıklama keyfini çıkarın.</span><span class="sxs-lookup"><span data-stu-id="bd338-125">Click hello green **Start Debugging** (F5) button and enjoy debugging.</span></span>

<span data-ttu-id="bd338-126">Okuyabilirsiniz [JavaScript VS code'da](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn hello hata ayıklayıcı hakkında daha fazla.</span><span class="sxs-lookup"><span data-stu-id="bd338-126">You can read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn more about hello debugger.</span></span>

![Uzaktan etkileşimli hata ayıklama](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="bd338-128">Azure CLI sorunları</span><span class="sxs-lookup"><span data-stu-id="bd338-128">Azure-CLI issues</span></span>
<span data-ttu-id="bd338-129">Hello Azure komut satırı arabirimi (Azure CLI) önizleme yapıdır.</span><span class="sxs-lookup"><span data-stu-id="bd338-129">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="bd338-130">Merhaba çözümde arayın [Önizleme Yükleme Kılavuzu](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek çözümler.</span><span class="sxs-lookup"><span data-stu-id="bd338-130">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="bd338-131">Komutları beklendiği gibi çalışmıyor olduğunda tooupgrade Azure CLI toolatest sürümünü deneyin.</span><span class="sxs-lookup"><span data-stu-id="bd338-131">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="bd338-132">Tüm hatalar hello aracı ile karşılaşırsanız, dosya bir [sorunu](https://github.com/Azure/azure-cli/issues) hello içinde **sorunları** hello GitHub deposuna bölümü.</span><span class="sxs-lookup"><span data-stu-id="bd338-132">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="bd338-133">Sık karşılaşılan sorunları gidermede yardım için hello denetleyin [Benioku](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="bd338-133">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="bd338-134">"Merhaba gereksinimini karşılayan bir sürüm bulunamadı", lütfen karşılıyorsa çalışma hello aşağıdaki tooupgrade PIP toolastest sürüm komutu.</span><span class="sxs-lookup"><span data-stu-id="bd338-134">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="bd338-135">Python yükleme sorunları</span><span class="sxs-lookup"><span data-stu-id="bd338-135">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="bd338-136">Eski yükleme sorunları (macOS)</span><span class="sxs-lookup"><span data-stu-id="bd338-136">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="bd338-137">Ne zaman yüklüyorsanız **PIP**, eski paketleri olduğunda izin hatası atılır ile birlikte yüklenen **su** izinleri.</span><span class="sxs-lookup"><span data-stu-id="bd338-137">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="bd338-138">Python brew (macOS) kullanarak önceki bir yüklemesini tümüyle kaldırılmamış. Bu durum oluşur.</span><span class="sxs-lookup"><span data-stu-id="bd338-138">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="bd338-139">Bazı **PIP** önceki bir yükleme paketi hello izni hatasına neden oluyor kök tarafından oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="bd338-139">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="bd338-140">Merhaba çözüm tooremove bu paketleri kök tarafından yüklü değil.</span><span class="sxs-lookup"><span data-stu-id="bd338-140">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="bd338-141">Aşağıdaki adımları toocomplete hello bu görevi kullanın:</span><span class="sxs-lookup"><span data-stu-id="bd338-141">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="bd338-142">Gidin: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="bd338-142">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="bd338-143">Liste paketleri kök tarafından oluşturun:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="bd338-143">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="bd338-144">Paketler, adım 2 ' Kaldır:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="bd338-144">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="bd338-145">Python yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="bd338-145">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="bd338-146">Azure IOT hub'ı sorunları</span><span class="sxs-lookup"><span data-stu-id="bd338-146">Azure IoT Hub issues</span></span>
<span data-ttu-id="bd338-147">Başarılı bir şekilde Azure IOT hub'ınıza sağladığınız varsa `azure-cli`, ve tooyour IOT hub'ı deneyin hello araçları aşağıdaki bağlanan bir aracı toomanage hello aygıtlarının gerekir:</span><span class="sxs-lookup"><span data-stu-id="bd338-147">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="bd338-148">Cihaz Gezgini</span><span class="sxs-lookup"><span data-stu-id="bd338-148">Device Explorer</span></span>
<span data-ttu-id="bd338-149">[Cihaz Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) Windows yerel makinenizde çalıştırır ve azure'da tooyour IOT hub'ı bağlar.</span><span class="sxs-lookup"><span data-stu-id="bd338-149">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="bd338-150">Merhaba aşağıdaki ile iletişim kurar [IOT Hub uç noktaları](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="bd338-150">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

- <span data-ttu-id="bd338-151">_Cihaz Kimlik Yönetimi_ tooprovision ve IOT hub'ınıza kayıtlı cihazları yönetme.</span><span class="sxs-lookup"><span data-stu-id="bd338-151">_Device identity management_ tooprovision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="bd338-152">_Cihaz bulut alma_ aygıt tooyour IOT hub'dan gönderilen iletileri izleyebilmek.</span><span class="sxs-lookup"><span data-stu-id="bd338-152">_Receive device-to-cloud_ so you can monitor messages sent from your device tooyour IoT hub.</span></span>
- <span data-ttu-id="bd338-153">_Bulut cihaz Gönder_ IOT hub'ından tooyour aygıtları iletileri gönderebilmesi.</span><span class="sxs-lookup"><span data-stu-id="bd338-153">_Send cloud-to-device_ so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="bd338-154">Yapılandırma, `IoT hub connection string` bu aracı toouse içindeki tüm özellikleri.</span><span class="sxs-lookup"><span data-stu-id="bd338-154">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="bd338-155">IOT hub'ı Gezgini</span><span class="sxs-lookup"><span data-stu-id="bd338-155">IoT hub Explorer</span></span>
<span data-ttu-id="bd338-156">[IOT hub'ı Explorer](https://github.com/Azure/iothub-explorer) bir örnek çok platformlu CLI toomanage aygıt istemcileri aracıdır.</span><span class="sxs-lookup"><span data-stu-id="bd338-156">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="bd338-157">Merhaba kimlik kayıt defterinde hello aracı toomanage hello aygıtları'nı kullanın, cihaz bulut iletilerini izlemek ve bulut cihaza komut gönderme.</span><span class="sxs-lookup"><span data-stu-id="bd338-157">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="bd338-158">tooinstall hello ıothub explorer aracı, aşağıdaki komut, komut satırı ortamınızdaki hello çalıştırın (ön) en son sürümünü hello:</span><span class="sxs-lookup"><span data-stu-id="bd338-158">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="bd338-159">Tüm hakkında ek Yardım tooget iothub-explorer komutlar ve bunların parametrelerini hello komutu aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bd338-159">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="bd338-160">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="bd338-160">Azure portal</span></span>
<span data-ttu-id="bd338-161">Tam CLI deneyimi oluşturma ve Azure kaynaklarınızı yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="bd338-161">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="bd338-162">Toouse hello isteyebilirsiniz [Azure portal](../azure-portal-overview.md) toohelp sağlamanıza, yönetmek ve Azure kaynaklarınızı hata ayıklama.</span><span class="sxs-lookup"><span data-stu-id="bd338-162">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="bd338-163">Azure depolama sorunları</span><span class="sxs-lookup"><span data-stu-id="bd338-163">Azure storage issues</span></span>
<span data-ttu-id="bd338-164">[Microsoft Azure Storage Gezgini (Önizleme)](http://storageexplorer.com) toowork ile kullanabileceğiniz Microsoft tek başına uygulamadır [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) Windows, macOS ve Linux veri.</span><span class="sxs-lookup"><span data-stu-id="bd338-164">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="bd338-165">Bu aracı kullanarak tooyour tablo bağlanabilir ve hello verilerde bakın.</span><span class="sxs-lookup"><span data-stu-id="bd338-165">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="bd338-166">Bu aracı tootroubleshoot Azure depolama sorunlarınızı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd338-166">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd338-167">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bd338-167">Next steps</span></span>
<span data-ttu-id="bd338-168">Bu sayfa yalnızca Intel Edison'u Seti'nin hello en yaygın sorunları içerir.</span><span class="sxs-lookup"><span data-stu-id="bd338-168">This page only includes hello most common problems of Intel Edison kit.</span></span> <span data-ttu-id="bd338-169">Bu gibi durumlarda, alt açıklamaları da daha fazla sorun giderme için tooreport sorunları bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd338-169">You can also leave bottom comments tooreport issues for further troubleshooting.</span></span>

<span data-ttu-id="bd338-170">Çok dön[Intel Edison'u (Node.js) ile çalışmaya başlama](iot-hub-intel-edison-kit-node-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="bd338-170">Go back too[Get started with Intel Edison (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-node-edison-getting-started