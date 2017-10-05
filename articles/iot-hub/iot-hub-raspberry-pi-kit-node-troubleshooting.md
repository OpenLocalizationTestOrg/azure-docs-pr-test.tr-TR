---
title: "Böğürtlenli Pi (C) bağlanmak için Azure IOT - sorunlarını giderme | Microsoft Docs"
description: "Sayfa Raspberry Pi Node.js deneyimi için sorun giderme"
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
ms.openlocfilehash: f9058068972ddbb674d3cd159948835dc88c4451
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="4a7fd-104">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="4a7fd-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="4a7fd-105">Donanım sorunları</span><span class="sxs-lookup"><span data-stu-id="4a7fd-105">Hardware issues</span></span>
### <a name="the-application-runs-well-but-the-led-is-not-blinking"></a><span data-ttu-id="4a7fd-106">Uygulama iyi çalışır ancak ışığı yanıp sönen değil</span><span class="sxs-lookup"><span data-stu-id="4a7fd-106">The application runs well but the LED is not blinking</span></span>
<span data-ttu-id="4a7fd-107">Bu sorun, her zaman donanım hattı bağlantı ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-107">This issue is always related to hardware circuit connectivity.</span></span> <span data-ttu-id="4a7fd-108">Sorunları belirlemek için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="4a7fd-108">Use the following steps to identify problems:</span></span>

1. <span data-ttu-id="4a7fd-109">Doğru seçtiğiniz denetleyin **GPIO'yu** panonuzu üzerinde.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-109">Check that you chose the correct **GPIO** on your board.</span></span> <span data-ttu-id="4a7fd-110">İki bağlantı noktası olmalıdır **GPIO'yu GND (PIN 6)** ve **GPIO'yu 04 (PIN 7)**.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-110">The two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="4a7fd-111">LED polarite doğru olduğunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-111">Check that the polarity of your LED is correct.</span></span> <span data-ttu-id="4a7fd-112">Uzun leg belirtmelidir **pozitif**, Number PIN.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-112">The longer leg should indicate the **positive**, anode pin.</span></span>
3. <span data-ttu-id="4a7fd-113">Kullanım **3, 3v PIN** ve **GND PIN** üzerinde Raspberry 3 ila Pi.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-113">Use the **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="4a7fd-114">Pi DC Güç kabul eder.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-114">Treat Pi as the DC power.</span></span> <span data-ttu-id="4a7fd-115">LED düzgün çalışıp çalışmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-115">Check that the LED works fine.</span></span>

![LED belirtimi](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="4a7fd-117">Diğer donanım sorunları</span><span class="sxs-lookup"><span data-stu-id="4a7fd-117">Other hardware issues</span></span>
<span data-ttu-id="4a7fd-118">Raspberry Pi 3'te sık karşılaşılan sorunları giderme hakkında daha fazla bilgi için bkz: [resmi sorun giderme sayfa](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="4a7fd-118">For information about solving common problems on Raspberry Pi 3, see the [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="4a7fd-119">Node.js paket sorunları</span><span class="sxs-lookup"><span data-stu-id="4a7fd-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="4a7fd-120">Gulp görevler sırasında yanıt yok</span><span class="sxs-lookup"><span data-stu-id="4a7fd-120">No response during gulp tasks</span></span>
<span data-ttu-id="4a7fd-121">Ekleyebileceğiniz gulp görevleri çalıştırma sorunlarla karşılaşmanız halinde, `--verbose` hata ayıklama seçeneği.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-121">If you encounter problems in running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="4a7fd-122">Ctrl + C'ı kullanarak geçerli gulp görevleri sonlandırmak deneyin ve ardından görmek için konsol penceresinde aşağıdaki komutu çalıştırın hata ayıklama iletilerini.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-122">Try to terminate current gulp tasks by using Ctrl + C, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="4a7fd-123">Ayrıntılı hata iletileri, konsol çıktısı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-123">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="4a7fd-124">Aygıt Bulma sorunları</span><span class="sxs-lookup"><span data-stu-id="4a7fd-124">Device discovery issues</span></span>
<span data-ttu-id="4a7fd-125">İlgili genel sorunları gidermede yardım için `devdisco` komutu, onay [Benioku](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="4a7fd-125">For help in troubleshooting common problems with the `devdisco` command, check the [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="4a7fd-126">npm sorunları</span><span class="sxs-lookup"><span data-stu-id="4a7fd-126">npm issues</span></span>
<span data-ttu-id="4a7fd-127">Aşağıdaki komutu kullanarak npm paket güncelleştirmeyi deneyin:</span><span class="sxs-lookup"><span data-stu-id="4a7fd-127">Try to update your npm package by using the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="4a7fd-128">Sorun devam ederse, bu makalenin sonunda yorumlarınızı bırakın veya bir GitHub sorunu oluşturmak bizim [örnek depo](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span><span class="sxs-lookup"><span data-stu-id="4a7fd-128">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="4a7fd-129">Uzaktan hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="4a7fd-129">Remote debugging</span></span>
### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="4a7fd-130">Örnek uygulamayı hata ayıklama modunda çalıştırın</span><span class="sxs-lookup"><span data-stu-id="4a7fd-130">Run the sample application in debug mode</span></span>
```bash
gulp run --debug
```

<span data-ttu-id="4a7fd-131">Hata ayıklama altyapısı hazır olduğunda, görmelisiniz ```Debugger listening on port 5858``` konsol çıkışı.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-131">When the debug engine is ready, you should see ```Debugger listening on port 5858``` in the console output.</span></span>

### <a name="configure-visual-studio-code-to-connect-to-the-remote-device"></a><span data-ttu-id="4a7fd-132">Visual Studio Code uzak cihaza bağlanmak için yapılandırın</span><span class="sxs-lookup"><span data-stu-id="4a7fd-132">Configure Visual Studio Code to connect to the remote device</span></span>
1. <span data-ttu-id="4a7fd-133">Açık **hata ayıklama** sol tarafındaki paneli.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-133">Open the **Debug** panel on the left side.</span></span>
2. <span data-ttu-id="4a7fd-134">Yeşil tıklatın **hata ayıklamayı Başlat** (F5) düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-134">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="4a7fd-135">Visual Studio Code Launch.json'u dosyasını açar.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-135">Visual Studio Code opens a launch.json file.</span></span>
3. <span data-ttu-id="4a7fd-136">Launch.json'u dosyasını aşağıdaki içerik ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-136">Update the launch.json file with the following content.</span></span> <span data-ttu-id="4a7fd-137">Değiştir `[device hostname or IP address]` gerçek aygıt IP adresi veya ana bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-137">Replace `[device hostname or IP address]` with the actual device IP address or host name.</span></span>

> [!NOTE]
> <span data-ttu-id="4a7fd-138">Visual Studio hata ayıklama hakkında daha fazla bilgi için lütfen [Visual Studio kodda hata ayıklama](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span><span class="sxs-lookup"><span data-stu-id="4a7fd-138">To learn more about the Visual Studio Debugging, please refer to [Debugging in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span></span>


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

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="4a7fd-140">Uzak uygulamasına ekleme</span><span class="sxs-lookup"><span data-stu-id="4a7fd-140">Attach to the remote application</span></span>
<span data-ttu-id="4a7fd-141">Yeşil tıklatın **hata ayıklamayı Başlat** hata ayıklamayı başlatmak için (F5) düğmesini.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-141">Click the green **Start Debugging** (F5) button to start debugging.</span></span>

<span data-ttu-id="4a7fd-142">Okuma [JavaScript VS code'da](https://code.visualstudio.com/docs/languages/javascript#_debugging) hata ayıklayıcı hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-142">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![Uzaktan etkileşimli hata ayıklama](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="4a7fd-144">Azure CLI sorunları</span><span class="sxs-lookup"><span data-stu-id="4a7fd-144">Azure CLI issues</span></span>
<span data-ttu-id="4a7fd-145">Azure komut satırı arabirimi (Azure CLI) önizleme yapıdır.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-145">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="4a7fd-146">Çözümleri aramak için kullanabileceğiniz [Önizleme Yükleme Kılavuzu](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="4a7fd-146">To seek solutions, you can use the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="4a7fd-147">Tüm hatalar aracı ile karşılaşırsanız, dosya bir [sorunu](https://github.com/Azure/azure-cli/issues) içinde **sorunları** GitHub depo bölümü.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-147">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="4a7fd-148">Sık karşılaşılan sorunları giderme konusunda yardım için kontrol [Benioku](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="4a7fd-148">For help in troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

## <a name="python-installation-issues"></a><span data-ttu-id="4a7fd-149">Python yükleme sorunları</span><span class="sxs-lookup"><span data-stu-id="4a7fd-149">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="4a7fd-150">Eski yükleme sorunları (macOS)</span><span class="sxs-lookup"><span data-stu-id="4a7fd-150">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="4a7fd-151">PIP yüklüyorsanız, eski paketleri ile yüklendiğinde izin hatası atılır **su** izinleri.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-151">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="4a7fd-152">Python brew (macOS) kullanarak önceki bir yüklemesini tümüyle kaldırılmamış. Bu durum oluşur.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-152">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="4a7fd-153">Önceki yüklemeye ait bazı PIP paketler izni hataya neden olan kök tarafından oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-153">Some pip packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="4a7fd-154">Kök tarafından yüklenen bu paketleri kaldırmak için çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-154">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="4a7fd-155">Bu görevi tamamlamak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="4a7fd-155">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="4a7fd-156">Gidin: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="4a7fd-156">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="4a7fd-157">Kök tarafından oluşturulan listesi paketler:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="4a7fd-157">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="4a7fd-158">Paketler, adım 2 ' Kaldır:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="4a7fd-158">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="4a7fd-159">Python yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-159">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="4a7fd-160">Azure IOT hub'ı sorunları</span><span class="sxs-lookup"><span data-stu-id="4a7fd-160">Azure IoT Hub issues</span></span>
<span data-ttu-id="4a7fd-161">Azure CLI ile Azure IOT hub'ınızı başarıyla kaynak sağlandı ve IOT hub'ınıza bağlanan cihazları yönetmek için bir aracı ihtiyacınız varsa aşağıdaki araçları deneyin.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-161">If you've successfully provisioned your Azure IoT hub with Azure CLI, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="4a7fd-162">Cihaz Gezgini</span><span class="sxs-lookup"><span data-stu-id="4a7fd-162">Device explorer</span></span>
<span data-ttu-id="4a7fd-163">[Aygıt explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) aracı Windows yerel makinenizde çalıştırır ve Azure IOT hub'ınıza bağlanır.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-163">The [Device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) tool runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="4a7fd-164">Aşağıdaki ile iletişim kurar [IOT Hub uç noktaları](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="4a7fd-164">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>


* <span data-ttu-id="4a7fd-165">*Cihaz Kimlik Yönetimi* sağlamak ve IOT hub'ınıza kayıtlı cihazları yönetmek için.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-165">*Device identity management* to provision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="4a7fd-166">*Cihaz bulut alma* cihazınızın IOT hub'ına gönderilen iletileri izleyebilmek.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-166">*Receive device-to-cloud* so you can monitor messages sent from your device to your IoT hub.</span></span>
* <span data-ttu-id="4a7fd-167">*Bulut cihaz Gönder* IOT hub'ından aygıtlarınıza iletileri gönderebilmesi.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-167">*Send cloud-to-device* so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="4a7fd-168">IOT hub bağlantı dizenizi tüm özellikleri kullanmak için bu aracı içinde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-168">Configure your IoT hub connection string within this tool to use all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="4a7fd-169">ıothub Gezgini</span><span class="sxs-lookup"><span data-stu-id="4a7fd-169">iothub-explorer</span></span>
<span data-ttu-id="4a7fd-170">[ıothub explorer](https://github.com/Azure/iothub-explorer) cihazları yönetmek için bir örnek çok platformlu CLI aracıdır.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-170">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage devices.</span></span> <span data-ttu-id="4a7fd-171">Cihaz kimlik kayıt defterinde yönetmek, cihaz bulut iletilerini izlemek ve bulut-cihaz iletilerini göndermek için aracını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-171">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device messages.</span></span>

<span data-ttu-id="4a7fd-172">Iothub explorer Aracı (ön) en son sürümünü yüklemek için komut satırı ortamınızda aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4a7fd-172">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="4a7fd-173">Tüm ıothub explorer komutları ve bunların parametreleri hakkında ek Yardım almak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="4a7fd-173">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="4a7fd-174">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="4a7fd-174">Azure portal</span></span>
<span data-ttu-id="4a7fd-175">Tam CLI deneyimi oluşturma ve Azure kaynaklarınızı yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-175">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="4a7fd-176">Kullanmak isteyebilirsiniz [Azure portal](../azure-portal-overview.md) sağlama Yardım, yönetmek ve Azure kaynaklarınızı hata ayıklamak için.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-176">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="4a7fd-177">Azure depolama sorunları</span><span class="sxs-lookup"><span data-stu-id="4a7fd-177">Azure Storage issues</span></span>
<span data-ttu-id="4a7fd-178">[Microsoft Azure Storage Gezgini (Önizleme)](http://storageexplorer.com) Windows, macOS ve Linux Azure Storage verilerle çalışmak için kullanabileceğiniz bir Microsoft tek başına uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-178">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="4a7fd-179">Bu aracı kullanarak tablonuza bağlanabilir ve içindeki verilerin bakın.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-179">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="4a7fd-180">Azure Storage sorunlarını gidermek için bu aracı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a7fd-180">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

