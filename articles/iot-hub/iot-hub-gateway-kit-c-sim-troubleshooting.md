---
title: "Benzetimli cihaz & Azure IOT ağ geçidi - sorunlarını giderme | Microsoft Docs"
description: "Sayfa Intel NUC ağ geçidi için sorun giderme"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IOT sorunları, Internet şeyler sorunları"
ROBOTS: NOINDEX
ms.assetid: 3ee8f4b0-5799-40a3-8cf0-8d5aa44dbc2b
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: eae4c112accaefa8bd1bf85f7b43badc2f491dfd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="eaff9-104">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="eaff9-104">Troubleshooting</span></span>

## <a name="hardware-issues"></a><span data-ttu-id="eaff9-105">Donanım sorunları</span><span class="sxs-lookup"><span data-stu-id="eaff9-105">Hardware issues</span></span>

### <a name="ti-sensortag-cannot-be-connected"></a><span data-ttu-id="eaff9-106">TI SensorTag bağlı</span><span class="sxs-lookup"><span data-stu-id="eaff9-106">TI SensorTag cannot be connected</span></span>

<span data-ttu-id="eaff9-107">SensorTag bağlantı sorunlarını gidermek için kullanmak [SensorTag uygulama](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span><span class="sxs-lookup"><span data-stu-id="eaff9-107">To troubleshoot SensorTag connectivity issues, use the [SensorTag app](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span></span>

### <a name="have-an-issue-with-intel-nuc"></a><span data-ttu-id="eaff9-108">Intel NUC ile ilgili bir sorun olması</span><span class="sxs-lookup"><span data-stu-id="eaff9-108">Have an issue with Intel NUC</span></span>

<span data-ttu-id="eaff9-109">Önyükleme sorunlarını gidermek için bkz [Intel NUC üzerinde Hayır önyükleme sorunlarını giderme](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span><span class="sxs-lookup"><span data-stu-id="eaff9-109">To troubleshoot boot issues, refer to [troubleshooting No Boot Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span></span>

<span data-ttu-id="eaff9-110">İşletim sistemi sorunlarını gidermek için bkz [Intel NUC üzerinde işletim sistemi sorunlarını giderme](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span><span class="sxs-lookup"><span data-stu-id="eaff9-110">To troubleshoot operating system issues, refer to [troubleshooting Operating System Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span></span>

<span data-ttu-id="eaff9-111">Diğer sorunları gidermek için bkz [Blink kodları ve Intel NUC kodları bip sesi](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span><span class="sxs-lookup"><span data-stu-id="eaff9-111">To troubleshoot other issues, refer to [Blink Codes and Beep Codes for Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="eaff9-112">Node.js paket sorunları</span><span class="sxs-lookup"><span data-stu-id="eaff9-112">Node.js package issues</span></span>

### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="eaff9-113">Gulp görevler sırasında yanıt yok</span><span class="sxs-lookup"><span data-stu-id="eaff9-113">No response during gulp tasks</span></span>

<span data-ttu-id="eaff9-114">Ekleyebileceğiniz gulp görevleri çalıştırma sorunlarla karşılaşmanız halinde, `--verbose` hata ayıklama seçeneği.</span><span class="sxs-lookup"><span data-stu-id="eaff9-114">If you encounter problems in running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="eaff9-115">Geçerli gulp görevleri kullanarak sonlandırmak deneyin `Ctrl + C`, hata ayıklama iletileri aşağıdaki görmek için konsol penceresinde komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="eaff9-115">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="eaff9-116">Ayrıntılı hata iletileri, konsol çıktısı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eaff9-116">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="eaff9-117">Aygıt Bulma sorunları</span><span class="sxs-lookup"><span data-stu-id="eaff9-117">Device discovery issues</span></span>

<span data-ttu-id="eaff9-118">İlgili genel sorunları gidermede yardım için `discover-sensortag` komutu, onay [wiki sayfa](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span><span class="sxs-lookup"><span data-stu-id="eaff9-118">For help in troubleshooting common problems with the `discover-sensortag` command, check the [wiki page](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="eaff9-119">npm sorunları</span><span class="sxs-lookup"><span data-stu-id="eaff9-119">npm issues</span></span>

<span data-ttu-id="eaff9-120">Aşağıdaki komutu çalıştırarak npm paket güncelleştirmeyi deneyin:</span><span class="sxs-lookup"><span data-stu-id="eaff9-120">Try to update your npm package by running the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="eaff9-121">Sorun devam ederse, bu makalenin sonunda yorumlarınızı bırakın veya bir GitHub sorunu oluşturmak bizim [örnek depo](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span><span class="sxs-lookup"><span data-stu-id="eaff9-121">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="eaff9-122">Uzaktan hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="eaff9-122">Remote Debugging</span></span>
> <span data-ttu-id="eaff9-123">Bu öğreticide kullanılan node.js komut hata ayıklama için aşağıdaki yönergeleri yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="eaff9-123">Below instructions are meant for debugging node.js scripts used in this tutorial.</span></span>
### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="eaff9-124">Örnek uygulamayı hata ayıklama modunda çalıştırın</span><span class="sxs-lookup"><span data-stu-id="eaff9-124">Run the sample application in debug mode</span></span>

<span data-ttu-id="eaff9-125">Örnek uygulama, aşağıdaki komutu çalıştırarak hata ayıklama modunda çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="eaff9-125">Run the sample application in debug mode by running the following command:</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="eaff9-126">Hata ayıklama altyapısı hazır olduğunda, görmelisiniz `Debugger listening on port 5858` konsol çıkışı.</span><span class="sxs-lookup"><span data-stu-id="eaff9-126">When the debug engine is ready, you should see `Debugger listening on port 5858` in the console output.</span></span>

### <a name="configure-visual-studio-code-to-connect-to-the-remote-device"></a><span data-ttu-id="eaff9-127">Visual Studio Code uzak cihaza bağlanmak için yapılandırın</span><span class="sxs-lookup"><span data-stu-id="eaff9-127">Configure Visual Studio Code to connect to the remote device</span></span>

1. <span data-ttu-id="eaff9-128">Açık **hata ayıklama** sol tarafındaki paneli.</span><span class="sxs-lookup"><span data-stu-id="eaff9-128">Open the **Debug** panel on the left side.</span></span>
2. <span data-ttu-id="eaff9-129">Yeşil tıklatın **hata ayıklamayı Başlat** (F5) düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eaff9-129">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="eaff9-130">Visual Studio Code açılır bir `launch.json` dosyası.</span><span class="sxs-lookup"><span data-stu-id="eaff9-130">Visual Studio Code opens a `launch.json` file.</span></span>
3. <span data-ttu-id="eaff9-131">Güncelleştirme `launch.json` dosya aşağıdaki içeriğe sahip.</span><span class="sxs-lookup"><span data-stu-id="eaff9-131">Update the `launch.json` file with the following content.</span></span> <span data-ttu-id="eaff9-132">Değiştir `[device hostname or IP address]` gerçek aygıt IP adresi veya ana bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="eaff9-132">Replace `[device hostname or IP address]` with the actual device IP address or host name.</span></span>

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

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="eaff9-134">Uzak uygulamasına ekleme</span><span class="sxs-lookup"><span data-stu-id="eaff9-134">Attach to the remote application</span></span>

<span data-ttu-id="eaff9-135">Yeşil tıklatın **hata ayıklamayı Başlat** hata ayıklamayı başlatmak için (F5) düğmesini.</span><span class="sxs-lookup"><span data-stu-id="eaff9-135">Click the green **Start Debugging** (F5) button to start debugging.</span></span>

<span data-ttu-id="eaff9-136">Okuma [JavaScript VS code'da](https://code.visualstudio.com/docs/languages/javascript#_debugging) hata ayıklayıcı hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="eaff9-136">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![Hata ayıklama bırak örnek](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="eaff9-138">Azure CLI sorunları</span><span class="sxs-lookup"><span data-stu-id="eaff9-138">Azure CLI issues</span></span>

<span data-ttu-id="eaff9-139">Azure komut satırı arabirimi (Azure CLI) önizleme yapıdır.</span><span class="sxs-lookup"><span data-stu-id="eaff9-139">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="eaff9-140">Çözümleri aramak için kullanabileceğiniz [Önizleme Yükleme Kılavuzu](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="eaff9-140">To seek solutions, you can use the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="eaff9-141">Tüm hatalar aracı ile karşılaşırsanız, dosya bir [sorunu](https://github.com/Azure/azure-cli/issues) içinde **sorunları** GitHub depo bölümü.</span><span class="sxs-lookup"><span data-stu-id="eaff9-141">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="eaff9-142">Sık karşılaşılan sorunları giderme konusunda yardım için kontrol [Benioku](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="eaff9-142">For help in troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="eaff9-143">Lütfen "gereksinimini karşılayan bir sürüm bulunamadı" karşılıyorsa, PIP en son sürümüne yükseltmek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="eaff9-143">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="eaff9-144">Python yükleme sorunları</span><span class="sxs-lookup"><span data-stu-id="eaff9-144">Python installation issues</span></span>

### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="eaff9-145">Eski yükleme sorunları (macOS)</span><span class="sxs-lookup"><span data-stu-id="eaff9-145">Legacy installation issues (macOS)</span></span>

<span data-ttu-id="eaff9-146">PIP yüklüyorsanız, eski paketleri ile yüklendiğinde izin hatası atılır **su** izinleri.</span><span class="sxs-lookup"><span data-stu-id="eaff9-146">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="eaff9-147">Python brew (macOS) kullanarak önceki bir yüklemesini tümüyle kaldırılmamış. Bu durum oluşur.</span><span class="sxs-lookup"><span data-stu-id="eaff9-147">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="eaff9-148">Önceki yüklemeye ait bazı PIP paketler izni hataya neden olan kök tarafından oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="eaff9-148">Some pip packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="eaff9-149">Kök tarafından yüklenen bu paketleri kaldırmak için çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="eaff9-149">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="eaff9-150">Bu görevi tamamlamak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="eaff9-150">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="eaff9-151">Şuraya gidin: `/usr/local/lib/python2.7/site-packages`</span><span class="sxs-lookup"><span data-stu-id="eaff9-151">Go to `/usr/local/lib/python2.7/site-packages`</span></span>
2. <span data-ttu-id="eaff9-152">Kök tarafından oluşturulan listesi paketler:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="eaff9-152">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="eaff9-153">Paketler, adım 2 ' Kaldır:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="eaff9-153">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="eaff9-154">Python yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="eaff9-154">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="eaff9-155">Azure IOT hub'ı sorunları</span><span class="sxs-lookup"><span data-stu-id="eaff9-155">Azure IoT Hub issues</span></span>

<span data-ttu-id="eaff9-156">Azure CLI ile Azure IOT hub'ınızı başarıyla kaynak sağlandı ve IOT hub'ınıza bağlanan cihazları yönetmek için bir aracı ihtiyacınız varsa aşağıdaki araçları deneyin.</span><span class="sxs-lookup"><span data-stu-id="eaff9-156">If you've successfully provisioned your Azure IoT hub with the Azure CLI, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="eaff9-157">Cihaz Gezgini</span><span class="sxs-lookup"><span data-stu-id="eaff9-157">Device Explorer</span></span>

<span data-ttu-id="eaff9-158">[Cihaz Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) Windows yerel makinenizde çalıştırır ve Azure IOT hub'ınıza bağlanır.</span><span class="sxs-lookup"><span data-stu-id="eaff9-158">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="eaff9-159">Aşağıdaki ile iletişim kurar [IOT Hub uç noktaları](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span><span class="sxs-lookup"><span data-stu-id="eaff9-159">It communicates with the following [IoT Hub endpoints](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span></span>

- <span data-ttu-id="eaff9-160">Cihaz Kimlik Yönetimi sağlamak ve cihazları yönetmek için IOT hub'ınıza kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="eaff9-160">Device identity management to provision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="eaff9-161">Cihazınızın IOT hub'ına gönderilen iletileri izleyebilmek cihaz bulut alırsınız.</span><span class="sxs-lookup"><span data-stu-id="eaff9-161">Receive device-to-cloud so you can monitor messages sent from your device to your IoT hub.</span></span>
- <span data-ttu-id="eaff9-162">IOT hub'ından aygıtlarınıza iletileri gönderebilmesi bulut cihaz gönderin.</span><span class="sxs-lookup"><span data-stu-id="eaff9-162">Send cloud-to-device so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="eaff9-163">IOT hub bağlantı dizenizi tüm özellikleri kullanmak için bu aracı içinde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="eaff9-163">Configure your IoT hub connection string within this tool to use all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="eaff9-164">ıothub Gezgini</span><span class="sxs-lookup"><span data-stu-id="eaff9-164">iothub-explorer</span></span>

<span data-ttu-id="eaff9-165">[ıothub explorer](https://github.com/Azure/iothub-explorer) aygıt istemcileri yönetmek için bir örnek çok platformlu CLI aracıdır.</span><span class="sxs-lookup"><span data-stu-id="eaff9-165">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="eaff9-166">Cihaz kimlik kayıt defterinde yönetmek, cihaz bulut iletilerini izlemek ve bulut-cihaz komutlarını göndermek için aracını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eaff9-166">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="eaff9-167">Iothub explorer Aracı (ön) en son sürümünü yüklemek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="eaff9-167">To install the latest (prerelease) version of the iothub-explorer tool, run the following command:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="eaff9-168">Tüm ıothub explorer komutları ve bunların parametreleri hakkında ek Yardım almak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="eaff9-168">To get additional help about all the iothub-explorer commands and their parameters, run the following command:</span></span>

```bash
iothub-explorer help
```

### <a name="the-azure-portal"></a><span data-ttu-id="eaff9-169">Azure portalı</span><span class="sxs-lookup"><span data-stu-id="eaff9-169">The Azure portal</span></span>

<span data-ttu-id="eaff9-170">Tam CLI deneyimi oluşturma ve Azure kaynaklarınızı yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="eaff9-170">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="eaff9-171">Kullanmak isteyebilirsiniz [Azure portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) sağlama Yardım, yönetmek ve Azure kaynaklarınızı hata ayıklamak için.</span><span class="sxs-lookup"><span data-stu-id="eaff9-171">You might also want to use the [Azure portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="eaff9-172">Azure depolama sorunları</span><span class="sxs-lookup"><span data-stu-id="eaff9-172">Azure Storage issues</span></span>

<span data-ttu-id="eaff9-173">[Microsoft Azure Storage Gezgini (Önizleme)](http://storageexplorer.com/) Windows, macOS ve Linux Azure Storage verilerle çalışmak için kullanabileceğiniz bir Microsoft tek başına uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="eaff9-173">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com/) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="eaff9-174">Bu aracı kullanarak tablonuza bağlanabilir ve içindeki verilerin bakın.</span><span class="sxs-lookup"><span data-stu-id="eaff9-174">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="eaff9-175">Azure Storage sorunlarını gidermek için bu aracı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eaff9-175">You can use this tool to troubleshoot your Azure Storage issues.</span></span>
