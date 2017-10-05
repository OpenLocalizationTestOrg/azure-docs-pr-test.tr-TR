---
title: "Arduino (C) bağlanmak için Azure IOT - sorunlarını giderme | Microsoft Docs"
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
ms.openlocfilehash: 3bb369da9148300a80e7d351522a4d908e926996
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="3f2a1-104">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="3f2a1-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="3f2a1-105">Donanım sorunları</span><span class="sxs-lookup"><span data-stu-id="3f2a1-105">Hardware issues</span></span>
<span data-ttu-id="3f2a1-106">Adafruit yumuşatma M0 WiFi Arduino panonuzu ortak sorunlarını çözme hakkında daha fazla bilgi için bkz: [resmi sorun giderme sayfa](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).</span><span class="sxs-lookup"><span data-stu-id="3f2a1-106">For information about solving common problems on your Adafruit Feather M0 WiFi Arduino board, see the [official troubleshooting page](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="3f2a1-107">Node.js paket sorunları</span><span class="sxs-lookup"><span data-stu-id="3f2a1-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="3f2a1-108">Gulp görevler sırasında yanıt yok</span><span class="sxs-lookup"><span data-stu-id="3f2a1-108">No response during gulp tasks</span></span>
<span data-ttu-id="3f2a1-109">Ekleyebileceğiniz gulp görevleri çalıştırma sorunlarla varsa, `--verbose` hata ayıklama seçeneği.</span><span class="sxs-lookup"><span data-stu-id="3f2a1-109">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="3f2a1-110">Geçerli gulp görevleri kullanarak sonlandırmak deneyin `Ctrl + C`, hata ayıklama iletileri aşağıdaki görmek için konsol penceresinde komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3f2a1-110">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="3f2a1-111">Ayrıntılı hata iletileri, konsol çıktısı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f2a1-111">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

<span data-ttu-id="3f2a1-112">Veya ekleyebileceğiniz `--listen` çıkış aygıt günlük bilgilerini seri bağlantı noktasına açın.</span><span class="sxs-lookup"><span data-stu-id="3f2a1-112">Or you can add `--listen` to open serial port to output device log information.</span></span>

```bash
gulp --listen
``` 

### <a name="npm-issues"></a><span data-ttu-id="3f2a1-113">NPM sorunları</span><span class="sxs-lookup"><span data-stu-id="3f2a1-113">NPM issues</span></span>
<span data-ttu-id="3f2a1-114">Aşağıdaki komutla NPM paket güncelleştirmeyi deneyin:</span><span class="sxs-lookup"><span data-stu-id="3f2a1-114">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="3f2a1-115">Sorun devam ederse, bu makalenin sonunda yorumlarınızı bırakın veya bir GitHub sorunu oluşturmak bizim [örnek depo][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="3f2a1-115">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="azure-cli-issues"></a><span data-ttu-id="3f2a1-116">Azure CLI sorunları</span><span class="sxs-lookup"><span data-stu-id="3f2a1-116">Azure-CLI issues</span></span>
<span data-ttu-id="3f2a1-117">Azure komut satırı arabirimi (Azure CLI) önizleme yapıdır.</span><span class="sxs-lookup"><span data-stu-id="3f2a1-117">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="3f2a1-118">Çözümde arayın [Önizleme Yükleme Kılavuzu](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) çözümleri arama.</span><span class="sxs-lookup"><span data-stu-id="3f2a1-118">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="3f2a1-119">Azure CLI komutları beklendiği gibi çalışmıyor olduğunda en son sürümüne yükseltmek deneyin.</span><span class="sxs-lookup"><span data-stu-id="3f2a1-119">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="3f2a1-120">Tüm hatalar aracı ile karşılaşırsanız, dosya bir [sorunu](https://github.com/Azure/azure-cli/issues) içinde **sorunları** GitHub depo bölümü.</span><span class="sxs-lookup"><span data-stu-id="3f2a1-120">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="3f2a1-121">Sık karşılaşılan sorunları gidermede yardım için denetleme [Benioku](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="3f2a1-121">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="3f2a1-122">Lütfen "gereksinimini karşılayan bir sürüm bulunamadı" karşılıyorsa, PIP en son sürümüne yükseltmek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3f2a1-122">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="3f2a1-123">Python yükleme sorunları</span><span class="sxs-lookup"><span data-stu-id="3f2a1-123">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="3f2a1-124">Eski yükleme sorunları (macOS)</span><span class="sxs-lookup"><span data-stu-id="3f2a1-124">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="3f2a1-125">Ne zaman yüklüyorsanız **PIP**, eski paketleri olduğunda izin hatası atılır ile birlikte yüklenen **su** izinleri.</span><span class="sxs-lookup"><span data-stu-id="3f2a1-125">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="3f2a1-126">Python brew (macOS) kullanarak önceki bir yüklemesini tümüyle kaldırılmamış. Bu durum oluşur.</span><span class="sxs-lookup"><span data-stu-id="3f2a1-126">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="3f2a1-127">Bazı **PIP** önceki bir yükleme paketlerinden izni hataya neden olan kök tarafından oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="3f2a1-127">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="3f2a1-128">Kök tarafından yüklenen bu paketleri kaldırmak için çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="3f2a1-128">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="3f2a1-129">Bu görevi tamamlamak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="3f2a1-129">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="3f2a1-130">Gidin: /usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="3f2a1-130">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="3f2a1-131">Liste paketleri kök tarafından oluşturun:`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="3f2a1-131">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="3f2a1-132">Paketler, adım 2 ' Kaldır:`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="3f2a1-132">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="3f2a1-133">Python yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3f2a1-133">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="3f2a1-134">Azure IOT hub'ı sorunları</span><span class="sxs-lookup"><span data-stu-id="3f2a1-134">Azure IoT Hub issues</span></span>
<span data-ttu-id="3f2a1-135">Başarılı bir şekilde Azure IOT hub'ınıza sağladığınız varsa `azure-cli`, ve IOT hub'ınıza bağlanan aygıtları yönetmek için aşağıdaki araçları deneyin bir aracı gerekir:</span><span class="sxs-lookup"><span data-stu-id="3f2a1-135">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="3f2a1-136">Cihaz Gezgini</span><span class="sxs-lookup"><span data-stu-id="3f2a1-136">Device Explorer</span></span>
<span data-ttu-id="3f2a1-137">[Cihaz Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) Windows yerel makinenizde çalıştırır ve Azure IOT hub'ınıza bağlanır.</span><span class="sxs-lookup"><span data-stu-id="3f2a1-137">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="3f2a1-138">Aşağıdaki ile iletişim kurar [IOT Hub uç noktaları](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="3f2a1-138">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="3f2a1-139">*Cihaz Kimlik Yönetimi* sağlamak ve IOT hub'ınıza kayıtlı cihazları yönetmek için.</span><span class="sxs-lookup"><span data-stu-id="3f2a1-139">*Device identity management* to provision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="3f2a1-140">*Cihaz bulut alma* cihazınızın IOT hub'ına gönderilen iletileri izleyebilmek.</span><span class="sxs-lookup"><span data-stu-id="3f2a1-140">*Receive device-to-cloud* so you can monitor messages sent from your device to your IoT hub.</span></span>
* <span data-ttu-id="3f2a1-141">*Bulut cihaz Gönder* IOT hub'ından aygıtlarınıza iletileri gönderebilmesi.</span><span class="sxs-lookup"><span data-stu-id="3f2a1-141">*Send cloud-to-device* so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="3f2a1-142">Yapılandırma, `IoT hub connection string` tüm özellikleri kullanmak için bu aracı içinde.</span><span class="sxs-lookup"><span data-stu-id="3f2a1-142">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="3f2a1-143">IOT hub'ı Gezgini</span><span class="sxs-lookup"><span data-stu-id="3f2a1-143">IoT hub Explorer</span></span>
<span data-ttu-id="3f2a1-144">[IOT hub'ı Explorer](https://github.com/Azure/iothub-explorer) aygıt istemcileri yönetmek için bir örnek çok platformlu CLI aracıdır.</span><span class="sxs-lookup"><span data-stu-id="3f2a1-144">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="3f2a1-145">Cihaz kimlik kayıt defterinde yönetmek, cihaz bulut iletilerini izlemek ve bulut-cihaz komutlarını göndermek için aracını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f2a1-145">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>


<span data-ttu-id="3f2a1-146">Iothub explorer Aracı (ön) en son sürümünü yüklemek için komut satırı ortamınızda aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="3f2a1-146">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="3f2a1-147">Tüm ıothub explorer komutları ve bunların parametreleri hakkında ek Yardım almak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="3f2a1-147">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="3f2a1-148">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="3f2a1-148">Azure portal</span></span>
<span data-ttu-id="3f2a1-149">Tam CLI deneyimi oluşturma ve Azure kaynaklarınızı yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="3f2a1-149">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="3f2a1-150">Kullanmak isteyebilirsiniz [Azure portal](../azure-portal-overview.md) sağlama Yardım, yönetmek ve Azure kaynaklarınızı hata ayıklamak için.</span><span class="sxs-lookup"><span data-stu-id="3f2a1-150">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="3f2a1-151">Azure depolama sorunları</span><span class="sxs-lookup"><span data-stu-id="3f2a1-151">Azure storage issues</span></span>
<span data-ttu-id="3f2a1-152">[Microsoft Azure Storage Gezgini (Önizleme)](http://storageexplorer.com) Windows, macOS ve Linux Azure Storage verilerle çalışmak için kullanabileceğiniz bir Microsoft tek başına uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="3f2a1-152">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="3f2a1-153">Bu aracı kullanarak tablonuza bağlanabilir ve içindeki verilerin bakın.</span><span class="sxs-lookup"><span data-stu-id="3f2a1-153">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="3f2a1-154">Azure Storage sorunlarını gidermek için bu aracı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f2a1-154">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md