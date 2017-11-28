---
title: "SensorTag cihaz & Azure IOT ağ geçidi - Ders 2: alma araçlarını (Windows) | Microsoft Docs"
description: "Merhaba araçları ve hello yazılım Windows çalıştıran ana bilgisayarınıza yüklemek, IOT hub'ı oluşturun ve hello IOT hub'da Cihazınızı kaydedin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IOT geliştirme, IOT yazılım IOT bulut hizmeti, şeyler yazılım, azure CLI, Internet Windows Git'i yükleyin, çalışma gulp, düğüm js Windows'u yüklemek, Windows npm yükleme, Windows'da python yüklemek"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 18ae6ee4-574a-4d5f-9838-ca2a78165628
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 3b30b60a0115413394992061a88dde4cd442ac19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-and-later"></a><span data-ttu-id="53570-104">(Windows 7 ve üzeri) Hello araçları edinin</span><span class="sxs-lookup"><span data-stu-id="53570-104">Get hello tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="53570-105">Windows 7 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="53570-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="53570-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="53570-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="53570-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="53570-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="53570-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="53570-108">What you will do</span></span>

- <span data-ttu-id="53570-109">Git, Node.js, Gulp, Python yükleyin.</span><span class="sxs-lookup"><span data-stu-id="53570-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="53570-110">Hello Azure komut satırı arabirimi (Azure CLI) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="53570-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="53570-111">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="53570-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="53570-112">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="53570-112">What you will learn</span></span>

<span data-ttu-id="53570-113">Bu alıştırmanın ilerisinde şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="53570-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="53570-114">Nasıl tooinstall [Git](https://git-scm.com/) ve [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="53570-114">How tooinstall [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="53570-115">Git bir açık kaynak dağıtılmış sürüm denetim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="53570-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="53570-116">Merhaba örnek bir uygulama bu ders için Git üzerinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="53570-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="53570-117">Node.js, JavaScript çalışma zamanı zengin paket ekosistemi ile olur.</span><span class="sxs-lookup"><span data-stu-id="53570-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="53570-118">Nasıl toouse [NPM](https://www.npmjs.com/) tooinstall Node.js geliştirme araçları.</span><span class="sxs-lookup"><span data-stu-id="53570-118">How toouse [NPM](https://www.npmjs.com/) tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="53570-119">Merhaba gerekli en düşük sürümü Node.js 4.5 LTS ' dir.</span><span class="sxs-lookup"><span data-stu-id="53570-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="53570-120">NPM hello paket Node.js yöneticilerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="53570-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="53570-121">Nasıl tooinstall Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="53570-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="53570-122">Visual Studio platformlar arası, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisini kodudur.</span><span class="sxs-lookup"><span data-stu-id="53570-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="53570-123">Hata ayıklama, katıştırılmış Git denetimi, sözdizimi vurgulama, akıllı kod tamamlama, parçacıkları ve kod da yeniden düzenleme için harika desteğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="53570-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="53570-124">Nasıl tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="53570-124">How tooinstall Python.</span></span>
  - <span data-ttu-id="53570-125">Python yaygın olarak kullanılan üst düzey, genel amaçlı, yorumlanan ve dinamik programlama dilidir.</span><span class="sxs-lookup"><span data-stu-id="53570-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="53570-126">Nasıl tooinstall Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="53570-126">How tooinstall hello Azure CLI.</span></span>
  - <span data-ttu-id="53570-127">Hello Azure CLI, Azure için birden çok platformlu bir komut satırı deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="53570-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="53570-128">Doğrudan bir komut satırı tooprovision çalışma ve kaynaklarını yönetme.</span><span class="sxs-lookup"><span data-stu-id="53570-128">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="53570-129">Nasıl toouse hello Azure CLI toocreate IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="53570-129">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="53570-130">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="53570-130">What you need</span></span>

- <span data-ttu-id="53570-131">Bir Internet bağlantısı toodownload araçları ve yazılım hello.</span><span class="sxs-lookup"><span data-stu-id="53570-131">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="53570-132">Bir Windows bilgisayarı.</span><span class="sxs-lookup"><span data-stu-id="53570-132">A Windows computer.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="53570-133">Git ve Node.js yükleyin</span><span class="sxs-lookup"><span data-stu-id="53570-133">Install Git and Node.js</span></span>

<span data-ttu-id="53570-134">Bağlantılar toodownload aşağıdaki hello'ı tıklatın ve Git ve Windows için Node.js LTS yükleyin.</span><span class="sxs-lookup"><span data-stu-id="53570-134">Click hello following links toodownload and install Git and Node.js LTS for Windows.</span></span>

- [<span data-ttu-id="53570-135">Windows için Git Al</span><span class="sxs-lookup"><span data-stu-id="53570-135">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
- [<span data-ttu-id="53570-136">Windows için node.js LTS Al</span><span class="sxs-lookup"><span data-stu-id="53570-136">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="53570-137">Node.js geliştirme araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="53570-137">Install Node.js development tools</span></span>

<span data-ttu-id="53570-138">Kullandığınız [gulp.js](http://gulpjs.com/) tooautomate dağıtım ve komut dosyası yürütme.</span><span class="sxs-lookup"><span data-stu-id="53570-138">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="53570-139">Basın `Windows + R`, türü `cmd` ve basın `Enter` tooopen bir komut istemi penceresi ve sonra çalışma hello aşağıdaki komutu:</span><span class="sxs-lookup"><span data-stu-id="53570-139">Press `Windows + R`, type `cmd` and press `Enter` tooopen a Command Prompt window, and then run hello following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="53570-140">Merhaba yükleme sorunlarıyla karşılaşırsanız, hello bkz [sorun giderme kılavuzu](iot-hub-gateway-kit-c-troubleshooting.md) çözümleri toocommon sorunları.</span><span class="sxs-lookup"><span data-stu-id="53570-140">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="53570-141">Düğüm, NPM ve Gulp Node.js içinde geliştirilen gerekli toorun Otomasyon betikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="53570-141">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="53570-142">Python yüklemek</span><span class="sxs-lookup"><span data-stu-id="53570-142">Install Python</span></span>

<span data-ttu-id="53570-143">Python 2.7, 3.4 veya 3.5 seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53570-143">You can choose from Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="53570-144">Bu öğreticide, Python 2.7 kullanırız.</span><span class="sxs-lookup"><span data-stu-id="53570-144">In this tutorial, we use Python 2.7.</span></span> <span data-ttu-id="53570-145">Python'ı zaten yüklediyseniz, toohello sonraki bölümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="53570-145">If you've already installed python, go toohello next section.</span></span>

[<span data-ttu-id="53570-146">Python için Windows Al</span><span class="sxs-lookup"><span data-stu-id="53570-146">Get Python for Windows</span></span>](https://www.python.org/downloads/)

<span data-ttu-id="53570-147">Tooadd hello yolu Python.exe'yi ve pip.exe nerede yüklü toohello sistem hello klasörlerinin etmeniz `PATH` ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="53570-147">You also need tooadd hello path of hello folders where Python.exe and pip.exe are installed toohello system `PATH` environment variable.</span></span> <span data-ttu-id="53570-148">Varsayılan olarak, Python.exe'yi yüklü `C:\Python27` ve pip.exe yüklü `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="53570-148">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="53570-149">Hello Azure CLI yükleme</span><span class="sxs-lookup"><span data-stu-id="53570-149">Install hello Azure CLI</span></span>

<span data-ttu-id="53570-150">tooinstall hello Azure CLI, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="53570-150">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="53570-151">Yönetici olarak bir komut istemi penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="53570-151">Open a Command Prompt window as an administrator.</span></span>

2. <span data-ttu-id="53570-152">Hello Azure CLI hello aşağıdaki komutları çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="53570-152">Install hello Azure CLI by running hello following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="53570-153">Merhaba yükleme 5 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="53570-153">hello installation might take 5 minutes.</span></span>

3. <span data-ttu-id="53570-154">Merhaba aşağıdaki komutu çalıştırarak Hello yüklemeyi doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="53570-154">Verify hello installation by running hello following command:</span></span>

   ```cmd
   az iot -h
   ```

   <span data-ttu-id="53570-155">Merhaba yükleme başarılı olup olmadığını hello aşağıdaki çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="53570-155">You should see hello following output if hello installation is successful.</span></span>

   ![Azure CLI yükleme doğrulayın](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="53570-157">Visual Studio Kodu'nu yükle</span><span class="sxs-lookup"><span data-stu-id="53570-157">Install Visual Studio Code</span></span>

<span data-ttu-id="53570-158">Visual Studio Code daha sonra hello öğretici tooedit yapılandırma dosyalarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="53570-158">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="53570-159">[Karşıdan](https://code.visualstudio.com/docs/setup/windows) ve Visual Studio Code yükleyin.</span><span class="sxs-lookup"><span data-stu-id="53570-159">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="53570-160">Özet</span><span class="sxs-lookup"><span data-stu-id="53570-160">Summary</span></span>

<span data-ttu-id="53570-161">Tüm gerekli hello araçları ve yazılım ana bilgisayara yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="53570-161">You've installed all hello required tools and software on your host computer.</span></span> <span data-ttu-id="53570-162">Sonraki görev toouse hello Azure CLI toocreate IOT hub'ı ve IOT hub'ınıza Cihazınızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="53570-162">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53570-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="53570-163">Next steps</span></span>
[<span data-ttu-id="53570-164">IoT hub'ı oluşturma ve cihazınızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="53570-164">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)
