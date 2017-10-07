---
title: "Connect Arduino (C) tooAzure IOT - sorunlarını giderme | Microsoft Docs"
description: "Sayfa Adafruit yumuşatma M0 WiFi Arduino deneyimi için sorun giderme"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino sorunlarını giderme"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: fdcc56ff-4420-463c-8a0e-5a1d215a874f
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ed793041ffa1887dbe73067f7c48d2417e982866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="51ba7-104">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="51ba7-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="51ba7-105">Donanım sorunları</span><span class="sxs-lookup"><span data-stu-id="51ba7-105">Hardware issues</span></span>
<span data-ttu-id="51ba7-106">Merhaba Adafruit yumuşatma M0 WiFi Arduino panonuzu ortak sorunlarını çözme hakkında daha fazla bilgi için bkz [resmi sorun giderme sayfa](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).</span><span class="sxs-lookup"><span data-stu-id="51ba7-106">For information about solving common problems on your Adafruit Feather M0 WiFi Arduino board, see hello [official troubleshooting page](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="51ba7-107">Node.js paket sorunları</span><span class="sxs-lookup"><span data-stu-id="51ba7-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="51ba7-108">Gulp görevler sırasında yanıt yok</span><span class="sxs-lookup"><span data-stu-id="51ba7-108">No response during gulp tasks</span></span>
<span data-ttu-id="51ba7-109">Çalışan gulp görevleri sorunlarla karşılaşırsanız, hello ekleyebilirsiniz `--verbose` hata ayıklama seçeneği.</span><span class="sxs-lookup"><span data-stu-id="51ba7-109">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="51ba7-110">Tooterminate geçerli gulp görevleri kullanarak deneyin `Ctrl + C`, ve ardından çalışma hello aşağıdaki konsol penceresi toosee hata ayıklama iletileri komutu.</span><span class="sxs-lookup"><span data-stu-id="51ba7-110">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="51ba7-111">Ayrıntılı hata iletileri, konsol çıktısı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51ba7-111">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

<span data-ttu-id="51ba7-112">Veya ekleyebileceğiniz `--listen` tooopen seri bağlantı noktası toooutput aygıt günlük bilgileri.</span><span class="sxs-lookup"><span data-stu-id="51ba7-112">Or you can add `--listen` tooopen serial port toooutput device log information.</span></span>

```bash
gulp --listen
``` 

### <a name="npm-issues"></a><span data-ttu-id="51ba7-113">NPM sorunları</span><span class="sxs-lookup"><span data-stu-id="51ba7-113">NPM issues</span></span>
<span data-ttu-id="51ba7-114">Tooupdate NPM paket komutu aşağıdaki hello ile deneyin:</span><span class="sxs-lookup"><span data-stu-id="51ba7-114">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="51ba7-115">Merhaba sorun devam ederse, bu makalenin hello sonunda yorumlarınızı bırakın veya bir GitHub sorunu oluşturmak bizim [örnek depo][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="51ba7-115">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="azure-cli-issues"></a><span data-ttu-id="51ba7-116">Azure CLI sorunları</span><span class="sxs-lookup"><span data-stu-id="51ba7-116">Azure-CLI issues</span></span>
<span data-ttu-id="51ba7-117">Hello Azure komut satırı arabirimi (Azure CLI) önizleme yapıdır.</span><span class="sxs-lookup"><span data-stu-id="51ba7-117">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="51ba7-118">Merhaba çözümde arayın [Önizleme Yükleme Kılavuzu](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek çözümler.</span><span class="sxs-lookup"><span data-stu-id="51ba7-118">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="51ba7-119">Komutları beklendiği gibi çalışmıyor olduğunda tooupgrade Azure CLI toolatest sürümünü deneyin.</span><span class="sxs-lookup"><span data-stu-id="51ba7-119">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="51ba7-120">Tüm hatalar hello aracı ile karşılaşırsanız, dosya bir [sorunu](https://github.com/Azure/azure-cli/issues) hello içinde **sorunları** hello GitHub deposuna bölümü.</span><span class="sxs-lookup"><span data-stu-id="51ba7-120">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="51ba7-121">Sık karşılaşılan sorunları gidermede yardım için hello denetleyin [Benioku](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="51ba7-121">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="51ba7-122">"Merhaba gereksinimini karşılayan bir sürüm bulunamadı", lütfen karşılıyorsa çalışma hello aşağıdaki tooupgrade PIP toolastest sürüm komutu.</span><span class="sxs-lookup"><span data-stu-id="51ba7-122">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="51ba7-123">Python yükleme sorunları</span><span class="sxs-lookup"><span data-stu-id="51ba7-123">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="51ba7-124">Eski yükleme sorunları (macOS)</span><span class="sxs-lookup"><span data-stu-id="51ba7-124">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="51ba7-125">Ne zaman yüklüyorsanız **PIP**, eski paketleri olduğunda izin hatası atılır ile birlikte yüklenen **su** izinleri.</span><span class="sxs-lookup"><span data-stu-id="51ba7-125">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="51ba7-126">Python brew (macOS) kullanarak önceki bir yüklemesini tümüyle kaldırılmamış. Bu durum oluşur.</span><span class="sxs-lookup"><span data-stu-id="51ba7-126">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="51ba7-127">Bazı **PIP** önceki bir yükleme paketi hello izni hatasına neden oluyor kök tarafından oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="51ba7-127">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="51ba7-128">Merhaba çözüm tooremove bu paketleri kök tarafından yüklü değil.</span><span class="sxs-lookup"><span data-stu-id="51ba7-128">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="51ba7-129">Aşağıdaki adımları toocomplete hello bu görevi kullanın:</span><span class="sxs-lookup"><span data-stu-id="51ba7-129">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="51ba7-130">Gidin: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="51ba7-130">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="51ba7-131">Liste paketleri kök tarafından oluşturun:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="51ba7-131">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="51ba7-132">Paketler, adım 2 ' Kaldır:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="51ba7-132">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="51ba7-133">Python yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="51ba7-133">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="51ba7-134">Azure IOT hub'ı sorunları</span><span class="sxs-lookup"><span data-stu-id="51ba7-134">Azure IoT Hub issues</span></span>
<span data-ttu-id="51ba7-135">Başarılı bir şekilde Azure IOT hub'ınıza sağladığınız varsa `azure-cli`, ve tooyour IOT hub'ı deneyin hello araçları aşağıdaki bağlanan bir aracı toomanage hello aygıtlarının gerekir:</span><span class="sxs-lookup"><span data-stu-id="51ba7-135">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="51ba7-136">Cihaz Gezgini</span><span class="sxs-lookup"><span data-stu-id="51ba7-136">Device Explorer</span></span>
<span data-ttu-id="51ba7-137">[Cihaz Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) Windows yerel makinenizde çalıştırır ve azure'da tooyour IOT hub'ı bağlar.</span><span class="sxs-lookup"><span data-stu-id="51ba7-137">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="51ba7-138">Merhaba aşağıdaki ile iletişim kurar [IOT Hub uç noktaları](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="51ba7-138">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="51ba7-139">*Cihaz Kimlik Yönetimi* tooprovision ve IOT hub'ınıza kayıtlı cihazları yönetme.</span><span class="sxs-lookup"><span data-stu-id="51ba7-139">*Device identity management* tooprovision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="51ba7-140">*Cihaz bulut alma* aygıt tooyour IOT hub'dan gönderilen iletileri izleyebilmek.</span><span class="sxs-lookup"><span data-stu-id="51ba7-140">*Receive device-to-cloud* so you can monitor messages sent from your device tooyour IoT hub.</span></span>
* <span data-ttu-id="51ba7-141">*Bulut cihaz Gönder* IOT hub'ından tooyour aygıtları iletileri gönderebilmesi.</span><span class="sxs-lookup"><span data-stu-id="51ba7-141">*Send cloud-to-device* so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="51ba7-142">Yapılandırma, `IoT hub connection string` bu aracı toouse içindeki tüm özellikleri.</span><span class="sxs-lookup"><span data-stu-id="51ba7-142">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="51ba7-143">IOT hub'ı Gezgini</span><span class="sxs-lookup"><span data-stu-id="51ba7-143">IoT hub Explorer</span></span>
<span data-ttu-id="51ba7-144">[IOT hub'ı Explorer](https://github.com/Azure/iothub-explorer) bir örnek çok platformlu CLI toomanage aygıt istemcileri aracıdır.</span><span class="sxs-lookup"><span data-stu-id="51ba7-144">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="51ba7-145">Merhaba kimlik kayıt defterinde hello aracı toomanage hello aygıtları'nı kullanın, cihaz bulut iletilerini izlemek ve bulut cihaza komut gönderme.</span><span class="sxs-lookup"><span data-stu-id="51ba7-145">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>


<span data-ttu-id="51ba7-146">tooinstall hello ıothub explorer aracı, aşağıdaki komut, komut satırı ortamınızdaki hello çalıştırın (ön) en son sürümünü hello:</span><span class="sxs-lookup"><span data-stu-id="51ba7-146">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="51ba7-147">Tüm hakkında ek Yardım tooget iothub-explorer komutlar ve bunların parametrelerini hello komutu aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="51ba7-147">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="51ba7-148">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="51ba7-148">Azure portal</span></span>
<span data-ttu-id="51ba7-149">Tam CLI deneyimi oluşturma ve Azure kaynaklarınızı yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="51ba7-149">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="51ba7-150">Toouse hello isteyebilirsiniz [Azure portal](../azure-portal-overview.md) toohelp sağlamanıza, yönetmek ve Azure kaynaklarınızı hata ayıklama.</span><span class="sxs-lookup"><span data-stu-id="51ba7-150">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="51ba7-151">Azure depolama sorunları</span><span class="sxs-lookup"><span data-stu-id="51ba7-151">Azure storage issues</span></span>
<span data-ttu-id="51ba7-152">[Microsoft Azure Storage Gezgini (Önizleme)](http://storageexplorer.com) toowork Windows, macOS ve Linux Azure Storage veri ile kullanabileceğiniz Microsoft tek başına uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="51ba7-152">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="51ba7-153">Bu aracı kullanarak tooyour tablo bağlanabilir ve hello verilerde bakın.</span><span class="sxs-lookup"><span data-stu-id="51ba7-153">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="51ba7-154">Bu aracı tootroubleshoot Azure depolama sorunlarınızı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51ba7-154">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md