---
title: "Böğürtlenli Pi (C) bağlanmak için Azure IOT - sorunlarını giderme | Microsoft Docs"
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
ms.openlocfilehash: 828669db23fa8d608029134fbe364033456d935a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="f8cb8-104">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="f8cb8-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="f8cb8-105">Donanım sorunları</span><span class="sxs-lookup"><span data-stu-id="f8cb8-105">Hardware issues</span></span>
### <a name="the-application-runs-well-but-the-led-is-not-blinking"></a><span data-ttu-id="f8cb8-106">Uygulama iyi çalışır ancak ışığı yanıp sönen değil</span><span class="sxs-lookup"><span data-stu-id="f8cb8-106">The application runs well but the LED is not blinking</span></span>
<span data-ttu-id="f8cb8-107">Bu sorun, her zaman donanım hattı bağlantı ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-107">This issue is always related to the hardware circuit connectivity.</span></span> <span data-ttu-id="f8cb8-108">Sorunları belirlemek için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-108">Use the following steps to identify problems.</span></span>

1. <span data-ttu-id="f8cb8-109">Doğru seçtiğiniz denetleyin **GPIO'yu** panonuzu üzerinde.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-109">Check that you chose the correct **GPIO** on your board.</span></span> <span data-ttu-id="f8cb8-110">İki bağlantı noktası olmalıdır **GPIO'yu GND (PIN 6)** ve **GPIO'yu 04 (PIN 7)**.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-110">The two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="f8cb8-111">LED polarite doğru olduğunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-111">Check that the polarity of your LED is correct.</span></span> <span data-ttu-id="f8cb8-112">Uzun leg belirtmelidir **pozitif**, Number PIN.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-112">The longer leg should indicate the **positive**, anode pin.</span></span>
3. <span data-ttu-id="f8cb8-113">Kullanım **3, 3v PIN** ve **GND PIN** üzerinde Raspberry 3 ila Pi.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-113">Use the **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="f8cb8-114">Pi DC Güç kabul eder.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-114">Treat Pi as the DC power.</span></span> <span data-ttu-id="f8cb8-115">LED düzgün çalışıp çalışmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-115">Check that the LED works fine.</span></span>

![LED belirtimi](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="f8cb8-117">Diğer donanım sorunları</span><span class="sxs-lookup"><span data-stu-id="f8cb8-117">Other hardware issues</span></span>
<span data-ttu-id="f8cb8-118">Raspberry Pi 3'te sık karşılaşılan sorunları giderme hakkında daha fazla bilgi için bkz: [resmi sorun giderme sayfa](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="f8cb8-118">For information about solving common problems on Raspberry Pi 3, see the [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="f8cb8-119">Node.js paket sorunları</span><span class="sxs-lookup"><span data-stu-id="f8cb8-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="f8cb8-120">Gulp görevler sırasında yanıt yok</span><span class="sxs-lookup"><span data-stu-id="f8cb8-120">No response during gulp tasks</span></span>
<span data-ttu-id="f8cb8-121">Ekleyebileceğiniz gulp görevleri çalıştırma sorunlarla varsa, `--verbose` hata ayıklama seçeneği.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-121">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="f8cb8-122">Geçerli gulp görevleri kullanarak sonlandırmak deneyin `Ctrl + C`, hata ayıklama iletileri aşağıdaki görmek için konsol penceresinde komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-122">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="f8cb8-123">Ayrıntılı hata iletileri, konsol çıktısı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-123">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="f8cb8-124">Aygıt Bulma sorunları</span><span class="sxs-lookup"><span data-stu-id="f8cb8-124">Device discovery issues</span></span>
<span data-ttu-id="f8cb8-125">İlgili genel sorunları gidermede yardım için `devdisco` komutu, onay [Benioku](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="f8cb8-125">For help in troubleshooting common problems with the `devdisco` command, check the [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="f8cb8-126">NPM sorunları</span><span class="sxs-lookup"><span data-stu-id="f8cb8-126">NPM issues</span></span>
<span data-ttu-id="f8cb8-127">Aşağıdaki komutla NPM paket güncelleştirmeyi deneyin:</span><span class="sxs-lookup"><span data-stu-id="f8cb8-127">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="f8cb8-128">Sorun devam ederse, bu makalenin sonunda yorumlarınızı bırakın veya bir GitHub sorunu oluşturmak bizim [örnek depo](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span><span class="sxs-lookup"><span data-stu-id="f8cb8-128">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="f8cb8-129">Uzaktan hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="f8cb8-129">Remote debugging</span></span>

<span data-ttu-id="f8cb8-130">Uzaktan hata ayıklama desteği yakında Visual Studio kod C/C++ uzantısı'nda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-130">Remote debugging support will be available soon in Visual Studio Code C/C++ Extension.</span></span>

<span data-ttu-id="f8cb8-131">Bir meanwhile, sık kullanılan SSH terminal GDB kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f8cb8-131">In a meanwhile you can use GDB via your favourite SSH terminal:</span></span>

```bash
cd c-pi-lesson-x
sudo gdb app
```

## <a name="azure-cli-issues"></a><span data-ttu-id="f8cb8-132">Azure CLI sorunları</span><span class="sxs-lookup"><span data-stu-id="f8cb8-132">Azure-CLI issues</span></span>
<span data-ttu-id="f8cb8-133">Azure komut satırı arabirimi (Azure CLI) önizleme yapıdır.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-133">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="f8cb8-134">Çözümde arayın [Önizleme Yükleme Kılavuzu](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) çözümleri arama.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-134">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="f8cb8-135">Azure CLI komutları beklendiği gibi çalışmıyor olduğunda en son sürümüne yükseltmek deneyin.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-135">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="f8cb8-136">Tüm hatalar aracı ile karşılaşırsanız, dosya bir [sorunu](https://github.com/Azure/azure-cli/issues) içinde **sorunları** GitHub depo bölümü.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-136">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="f8cb8-137">Sık karşılaşılan sorunları gidermede yardım için denetleme [Benioku](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="f8cb8-137">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="f8cb8-138">Lütfen "gereksinimini karşılayan bir sürüm bulunamadı" karşılıyorsa, PIP en son sürümüne yükseltmek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-138">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="f8cb8-139">Python yükleme sorunları</span><span class="sxs-lookup"><span data-stu-id="f8cb8-139">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="f8cb8-140">Eski yükleme sorunları (macOS)</span><span class="sxs-lookup"><span data-stu-id="f8cb8-140">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="f8cb8-141">Ne zaman yüklüyorsanız **PIP**, eski paketleri olduğunda izin hatası atılır ile birlikte yüklenen **su** izinleri.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-141">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="f8cb8-142">Python brew (macOS) kullanarak önceki bir yüklemesini tümüyle kaldırılmamış. Bu durum oluşur.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-142">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="f8cb8-143">Bazı **PIP** önceki bir yükleme paketlerinden izni hataya neden olan kök tarafından oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-143">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="f8cb8-144">Kök tarafından yüklenen bu paketleri kaldırmak için çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-144">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="f8cb8-145">Bu görevi tamamlamak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="f8cb8-145">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="f8cb8-146">Gidin: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="f8cb8-146">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="f8cb8-147">Liste paketleri kök tarafından oluşturun:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="f8cb8-147">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="f8cb8-148">Paketler, adım 2 ' Kaldır:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="f8cb8-148">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="f8cb8-149">Python yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-149">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="f8cb8-150">Azure IOT hub'ı sorunları</span><span class="sxs-lookup"><span data-stu-id="f8cb8-150">Azure IoT Hub issues</span></span>
<span data-ttu-id="f8cb8-151">Başarılı bir şekilde Azure IOT hub'ınıza sağladığınız varsa `azure-cli`, ve IOT hub'ınıza bağlanan aygıtları yönetmek için aşağıdaki araçları deneyin bir aracı gerekir:</span><span class="sxs-lookup"><span data-stu-id="f8cb8-151">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="f8cb8-152">Cihaz Gezgini</span><span class="sxs-lookup"><span data-stu-id="f8cb8-152">Device Explorer</span></span>
<span data-ttu-id="f8cb8-153">[Cihaz Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) Windows yerel makinenizde çalıştırır ve Azure IOT hub'ınıza bağlanır.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-153">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="f8cb8-154">Aşağıdaki ile iletişim kurar [IOT Hub uç noktaları](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="f8cb8-154">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="f8cb8-155">*Cihaz Kimlik Yönetimi* sağlamak ve IOT hub'ınıza kayıtlı cihazları yönetmek için.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-155">*Device identity management* to provision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="f8cb8-156">*Cihaz bulut alma* cihazınızın IOT hub'ına gönderilen iletileri izleyebilmek.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-156">*Receive device-to-cloud* so you can monitor messages sent from your device to your IoT hub.</span></span>
* <span data-ttu-id="f8cb8-157">*Bulut cihaz Gönder* IOT hub'ından aygıtlarınıza iletileri gönderebilmesi.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-157">*Send cloud-to-device* so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="f8cb8-158">Yapılandırma, `IoT hub connection string` tüm özellikleri kullanmak için bu aracı içinde.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-158">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="f8cb8-159">IOT hub'ı Gezgini</span><span class="sxs-lookup"><span data-stu-id="f8cb8-159">IoT hub Explorer</span></span>
<span data-ttu-id="f8cb8-160">[IOT hub'ı Explorer](https://github.com/Azure/iothub-explorer) aygıt istemcileri yönetmek için bir örnek çok platformlu CLI aracıdır.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-160">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="f8cb8-161">Cihaz kimlik kayıt defterinde yönetmek, cihaz bulut iletilerini izlemek ve bulut-cihaz komutlarını göndermek için aracını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-161">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="f8cb8-162">Iothub explorer Aracı (ön) en son sürümünü yüklemek için komut satırı ortamınızda aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f8cb8-162">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```
npm install -g iothub-explorer@latest
```

<span data-ttu-id="f8cb8-163">Tüm ıothub explorer komutları ve bunların parametreleri hakkında ek Yardım almak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="f8cb8-163">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="f8cb8-164">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="f8cb8-164">Azure portal</span></span>
<span data-ttu-id="f8cb8-165">Tam CLI deneyimi oluşturma ve Azure kaynaklarınızı yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-165">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="f8cb8-166">Kullanmak isteyebilirsiniz [Azure portal](../azure-portal-overview.md) sağlama Yardım, yönetmek ve Azure kaynaklarınızı hata ayıklamak için.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-166">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="f8cb8-167">Azure depolama sorunları</span><span class="sxs-lookup"><span data-stu-id="f8cb8-167">Azure storage issues</span></span>
<span data-ttu-id="f8cb8-168">[Microsoft Azure Storage Gezgini (Önizleme)](http://storageexplorer.com) Windows, macOS ve Linux Azure Storage verilerle çalışmak için kullanabileceğiniz bir Microsoft tek başına uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-168">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="f8cb8-169">Bu aracı kullanarak tablonuza bağlanabilir ve içindeki verilerin bakın.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-169">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="f8cb8-170">Azure Storage sorunlarını gidermek için bu aracı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8cb8-170">You can use this tool to troubleshoot your Azure Storage issues.</span></span>
