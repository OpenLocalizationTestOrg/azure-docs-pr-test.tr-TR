---
title: "Connect Intel Edison (C) tooAzure IOT - sorunlarını giderme | Microsoft Docs"
description: "Sayfa Intel Edison'u C deneyimi için sorun giderme"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino sorunlarını giderme"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: fe20f2fe-490c-4910-82e1-578ed504ae86
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c4a71983e3906cfc5ce7c832cf858852b9bd744a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="08438-104">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="08438-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="08438-105">Donanım sorunları</span><span class="sxs-lookup"><span data-stu-id="08438-105">Hardware issues</span></span>
<span data-ttu-id="08438-106">Merhaba Intel Edison'u ortak sorunlarını çözme hakkında daha fazla bilgi için bkz [resmi sorun giderme sayfa](https://software.intel.com/en-us/node/637974).</span><span class="sxs-lookup"><span data-stu-id="08438-106">For information about solving common problems on Intel Edison, see hello [official troubleshooting page](https://software.intel.com/en-us/node/637974).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="08438-107">Node.js paket sorunları</span><span class="sxs-lookup"><span data-stu-id="08438-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="08438-108">Gulp görevler sırasında yanıt yok</span><span class="sxs-lookup"><span data-stu-id="08438-108">No response during gulp tasks</span></span>
<span data-ttu-id="08438-109">Çalışan gulp görevleri sorunlarla karşılaşırsanız, hello ekleyebilirsiniz `--verbose` hata ayıklama seçeneği.</span><span class="sxs-lookup"><span data-stu-id="08438-109">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="08438-110">Tooterminate geçerli gulp görevleri kullanarak deneyin `Ctrl + C`, ve ardından çalışma hello aşağıdaki konsol penceresi toosee hata ayıklama iletileri komutu.</span><span class="sxs-lookup"><span data-stu-id="08438-110">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="08438-111">Ayrıntılı hata iletileri, konsol çıktısı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08438-111">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="npm-issues"></a><span data-ttu-id="08438-112">NPM sorunları</span><span class="sxs-lookup"><span data-stu-id="08438-112">NPM issues</span></span>
<span data-ttu-id="08438-113">Tooupdate NPM paket komutu aşağıdaki hello ile deneyin:</span><span class="sxs-lookup"><span data-stu-id="08438-113">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="08438-114">Merhaba sorun devam ederse, bu makalenin hello sonunda yorumlarınızı bırakın veya bir GitHub sorunu oluşturmak bizim [örnek depo][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="08438-114">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="azure-cli-issues"></a><span data-ttu-id="08438-115">Azure CLI sorunları</span><span class="sxs-lookup"><span data-stu-id="08438-115">Azure-CLI issues</span></span>
<span data-ttu-id="08438-116">Hello Azure komut satırı arabirimi (Azure CLI) önizleme yapıdır.</span><span class="sxs-lookup"><span data-stu-id="08438-116">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="08438-117">Merhaba çözümde arayın [Önizleme Yükleme Kılavuzu](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek çözümler.</span><span class="sxs-lookup"><span data-stu-id="08438-117">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="08438-118">Komutları beklendiği gibi çalışmıyor olduğunda tooupgrade Azure CLI toolatest sürümünü deneyin.</span><span class="sxs-lookup"><span data-stu-id="08438-118">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="08438-119">Tüm hatalar hello aracı ile karşılaşırsanız, dosya bir [sorunu](https://github.com/Azure/azure-cli/issues) hello içinde **sorunları** hello GitHub deposuna bölümü.</span><span class="sxs-lookup"><span data-stu-id="08438-119">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="08438-120">Sık karşılaşılan sorunları gidermede yardım için hello denetleyin [Benioku](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="08438-120">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="08438-121">"Merhaba gereksinimini karşılayan bir sürüm bulunamadı", lütfen karşılıyorsa çalışma hello aşağıdaki tooupgrade PIP toolastest sürüm komutu.</span><span class="sxs-lookup"><span data-stu-id="08438-121">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="08438-122">Python yükleme sorunları</span><span class="sxs-lookup"><span data-stu-id="08438-122">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="08438-123">Eski yükleme sorunları (macOS)</span><span class="sxs-lookup"><span data-stu-id="08438-123">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="08438-124">Ne zaman yüklüyorsanız **PIP**, eski paketleri olduğunda izin hatası atılır ile birlikte yüklenen **su** izinleri.</span><span class="sxs-lookup"><span data-stu-id="08438-124">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="08438-125">Python brew (macOS) kullanarak önceki bir yüklemesini tümüyle kaldırılmamış. Bu durum oluşur.</span><span class="sxs-lookup"><span data-stu-id="08438-125">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="08438-126">Bazı **PIP** önceki bir yükleme paketi hello izni hatasına neden oluyor kök tarafından oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="08438-126">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="08438-127">Merhaba çözüm tooremove bu paketleri kök tarafından yüklü değil.</span><span class="sxs-lookup"><span data-stu-id="08438-127">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="08438-128">Aşağıdaki adımları toocomplete hello bu görevi kullanın:</span><span class="sxs-lookup"><span data-stu-id="08438-128">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="08438-129">Gidin: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="08438-129">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="08438-130">Liste paketleri kök tarafından oluşturun:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="08438-130">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="08438-131">Paketler, adım 2 ' Kaldır:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="08438-131">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="08438-132">Python yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="08438-132">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="08438-133">Azure IOT hub'ı sorunları</span><span class="sxs-lookup"><span data-stu-id="08438-133">Azure IoT Hub issues</span></span>
<span data-ttu-id="08438-134">Başarılı bir şekilde Azure IOT hub'ınıza sağladığınız varsa `azure-cli`, ve tooyour IOT hub'ı deneyin hello araçları aşağıdaki bağlanan bir aracı toomanage hello aygıtlarının gerekir:</span><span class="sxs-lookup"><span data-stu-id="08438-134">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="08438-135">Cihaz Gezgini</span><span class="sxs-lookup"><span data-stu-id="08438-135">Device Explorer</span></span>
<span data-ttu-id="08438-136">[Cihaz Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) Windows yerel makinenizde çalıştırır ve azure'da tooyour IOT hub'ı bağlar.</span><span class="sxs-lookup"><span data-stu-id="08438-136">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="08438-137">Merhaba aşağıdaki ile iletişim kurar [IOT Hub uç noktaları](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="08438-137">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

- <span data-ttu-id="08438-138">_Cihaz Kimlik Yönetimi_ tooprovision ve IOT hub'ınıza kayıtlı cihazları yönetme.</span><span class="sxs-lookup"><span data-stu-id="08438-138">_Device identity management_ tooprovision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="08438-139">_Cihaz bulut alma_ aygıt tooyour IOT hub'dan gönderilen iletileri izleyebilmek.</span><span class="sxs-lookup"><span data-stu-id="08438-139">_Receive device-to-cloud_ so you can monitor messages sent from your device tooyour IoT hub.</span></span>
- <span data-ttu-id="08438-140">_Bulut cihaz Gönder_ IOT hub'ından tooyour aygıtları iletileri gönderebilmesi.</span><span class="sxs-lookup"><span data-stu-id="08438-140">_Send cloud-to-device_ so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="08438-141">Yapılandırma, `IoT hub connection string` bu aracı toouse içindeki tüm özellikleri.</span><span class="sxs-lookup"><span data-stu-id="08438-141">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="08438-142">IOT hub'ı Gezgini</span><span class="sxs-lookup"><span data-stu-id="08438-142">IoT hub Explorer</span></span>
<span data-ttu-id="08438-143">[IOT hub'ı Explorer](https://github.com/Azure/iothub-explorer) bir örnek çok platformlu CLI toomanage aygıt istemcileri aracıdır.</span><span class="sxs-lookup"><span data-stu-id="08438-143">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="08438-144">Merhaba kimlik kayıt defterinde hello aracı toomanage hello aygıtları'nı kullanın, cihaz bulut iletilerini izlemek ve bulut cihaza komut gönderme.</span><span class="sxs-lookup"><span data-stu-id="08438-144">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="08438-145">tooinstall hello ıothub explorer aracı, aşağıdaki komut, komut satırı ortamınızdaki hello çalıştırın (ön) en son sürümünü hello:</span><span class="sxs-lookup"><span data-stu-id="08438-145">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="08438-146">Tüm hakkında ek Yardım tooget iothub-explorer komutlar ve bunların parametrelerini hello komutu aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="08438-146">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="08438-147">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="08438-147">Azure portal</span></span>
<span data-ttu-id="08438-148">Tam CLI deneyimi oluşturma ve Azure kaynaklarınızı yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="08438-148">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="08438-149">Toouse hello isteyebilirsiniz [Azure portal](../azure-portal-overview.md) toohelp sağlamanıza, yönetmek ve Azure kaynaklarınızı hata ayıklama.</span><span class="sxs-lookup"><span data-stu-id="08438-149">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="08438-150">Azure depolama sorunları</span><span class="sxs-lookup"><span data-stu-id="08438-150">Azure storage issues</span></span>
<span data-ttu-id="08438-151">[Microsoft Azure Storage Gezgini (Önizleme)](http://storageexplorer.com) toowork ile kullanabileceğiniz Microsoft tek başına uygulamadır [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) Windows, macOS ve Linux veri.</span><span class="sxs-lookup"><span data-stu-id="08438-151">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="08438-152">Bu aracı kullanarak tooyour tablo bağlanabilir ve hello verilerde bakın.</span><span class="sxs-lookup"><span data-stu-id="08438-152">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="08438-153">Bu aracı tootroubleshoot Azure depolama sorunlarınızı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08438-153">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08438-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="08438-154">Next steps</span></span>
<span data-ttu-id="08438-155">Bu sayfa yalnızca Intel Edison'u Seti'nin hello en yaygın sorunları içerir.</span><span class="sxs-lookup"><span data-stu-id="08438-155">This page only includes hello most common problems of Intel Edison kit.</span></span> <span data-ttu-id="08438-156">Bu gibi durumlarda, alt açıklamaları da daha fazla sorun giderme için tooreport sorunları bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08438-156">You can also leave bottom comments tooreport issues for further troubleshooting.</span></span>

<span data-ttu-id="08438-157">Çok dön[Intel Edison (C) ile çalışmaya başlama](iot-hub-intel-edison-kit-c-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="08438-157">Go back too[Get started with Intel Edison (C)](iot-hub-intel-edison-kit-c-get-started.md)</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-c-edison-getting-started