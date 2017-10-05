---
title: "Benzetimli cihaz & Azure IOT ağ geçidi - Ders 2: alma araçlarını (Windows) | Microsoft Docs"
description: "Araçlar ve yazılımı Windows çalıştıran ana bilgisayarınıza yüklemek, IOT hub'ı oluşturun ve IOT hub'ı Cihazınızı kaydedin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IOT geliştirme, IOT yazılım IOT bulut hizmeti, şeyler yazılım, azure CLI, Internet Windows Git'i yükleyin, çalışma gulp, düğüm js Windows'u yüklemek, Windows npm yükleme, Windows'da python yüklemek"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: c16eee4c-8756-454b-82bf-3eb0dd51aa5f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ecedf5ef89677c73c5d9a3e5250eb9f45f6bad32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-and-later"></a><span data-ttu-id="8e490-104">(Windows 7 ve üzeri) araçları edinin</span><span class="sxs-lookup"><span data-stu-id="8e490-104">Get the tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8e490-105">Windows 7 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="8e490-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="8e490-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="8e490-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="8e490-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="8e490-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="8e490-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="8e490-108">What you will do</span></span>

- <span data-ttu-id="8e490-109">Git, Node.js, Gulp, Python yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8e490-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="8e490-110">Azure komut satırı arabirimi (Azure CLI) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8e490-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="8e490-111">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="8e490-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8e490-112">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="8e490-112">What you will learn</span></span>

<span data-ttu-id="8e490-113">Bu alıştırmanın ilerisinde şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="8e490-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="8e490-114">Yükleme [Git](https://git-scm.com/) ve [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="8e490-114">How to install [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="8e490-115">Git bir açık kaynak dağıtılmış sürüm denetim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="8e490-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="8e490-116">Örnek bir uygulama bu ders için Git üzerinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="8e490-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="8e490-117">Node.js, JavaScript çalışma zamanı zengin paket ekosistemi ile olur.</span><span class="sxs-lookup"><span data-stu-id="8e490-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="8e490-118">Nasıl kullanılacağını [NPM](https://www.npmjs.com/) Node.js geliştirme araçlarını yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="8e490-118">How to use [NPM](https://www.npmjs.com/) to install Node.js development tools.</span></span>
  - <span data-ttu-id="8e490-119">Node.js, gerekli en düşük sürüm 4.5 LTS ' dir.</span><span class="sxs-lookup"><span data-stu-id="8e490-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="8e490-120">NPM Node.js paket yöneticilerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="8e490-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="8e490-121">Visual Studio Code yükleme.</span><span class="sxs-lookup"><span data-stu-id="8e490-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="8e490-122">Visual Studio platformlar arası, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisini kodudur.</span><span class="sxs-lookup"><span data-stu-id="8e490-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="8e490-123">Hata ayıklama, katıştırılmış Git denetimi, sözdizimi vurgulama, akıllı kod tamamlama, parçacıkları ve kod da yeniden düzenleme için harika desteğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="8e490-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="8e490-124">Python yükleme.</span><span class="sxs-lookup"><span data-stu-id="8e490-124">How to install Python.</span></span>
  - <span data-ttu-id="8e490-125">Python yaygın olarak kullanılan üst düzey, genel amaçlı, yorumlanan ve dinamik programlama dilidir.</span><span class="sxs-lookup"><span data-stu-id="8e490-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="8e490-126">Azure CLI yükleme.</span><span class="sxs-lookup"><span data-stu-id="8e490-126">How to install the Azure CLI.</span></span>
  - <span data-ttu-id="8e490-127">Azure CLI, Azure için birden çok platformlu bir komut satırı deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="8e490-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="8e490-128">Doğrudan komut satırından sağlamak için çalışır ve kaynaklarını yönetme.</span><span class="sxs-lookup"><span data-stu-id="8e490-128">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="8e490-129">IOT hub'ı oluşturmak için Azure CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="8e490-129">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8e490-130">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="8e490-130">What you need</span></span>

- <span data-ttu-id="8e490-131">Araçlar ve yazılım indirmesi için Internet bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="8e490-131">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="8e490-132">Bir Windows bilgisayarı.</span><span class="sxs-lookup"><span data-stu-id="8e490-132">A Windows computer.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="8e490-133">Git ve Node.js yükleyin</span><span class="sxs-lookup"><span data-stu-id="8e490-133">Install Git and Node.js</span></span>

<span data-ttu-id="8e490-134">İndirmek ve Git ve Windows için Node.js LTS yüklemek için aşağıdaki bağlantıları tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8e490-134">Click the following links to download and install Git and Node.js LTS for Windows.</span></span>

- [<span data-ttu-id="8e490-135">Windows için Git Al</span><span class="sxs-lookup"><span data-stu-id="8e490-135">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
- [<span data-ttu-id="8e490-136">Windows için node.js LTS Al</span><span class="sxs-lookup"><span data-stu-id="8e490-136">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="8e490-137">Node.js geliştirme araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="8e490-137">Install Node.js development tools</span></span>

<span data-ttu-id="8e490-138">Kullandığınız [gulp.js](http://gulpjs.com/) dağıtım ve betiklerinin yürütülmesi otomatik hale getirmek için.</span><span class="sxs-lookup"><span data-stu-id="8e490-138">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="8e490-139">Basın `Windows + R`, türü `cmd` ve basın `Enter` bir komut istemi penceresi açın ve ardından aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8e490-139">Press `Windows + R`, type `cmd` and press `Enter` to open a Command Prompt window, and then run the following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="8e490-140">Yükleme sorunlarıyla karşılaşırsanız, bkz: [sorun giderme kılavuzu](iot-hub-gateway-kit-c-sim-troubleshooting.md) yaygın sorunların çözümleri için.</span><span class="sxs-lookup"><span data-stu-id="8e490-140">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="8e490-141">Düğüm, NPM ve Gulp Node.js içinde geliştirilen Otomasyon betikleri çalıştırmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="8e490-141">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="8e490-142">Python yüklemek</span><span class="sxs-lookup"><span data-stu-id="8e490-142">Install Python</span></span>

<span data-ttu-id="8e490-143">Python 2.7, 3.4 veya 3.5 seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e490-143">You can choose from Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="8e490-144">Bu öğreticide, Python 2.7 kullanırız.</span><span class="sxs-lookup"><span data-stu-id="8e490-144">In this tutorial, we use Python 2.7.</span></span> <span data-ttu-id="8e490-145">Python'ı zaten yüklediyseniz, sonraki bölüme gidin.</span><span class="sxs-lookup"><span data-stu-id="8e490-145">If you've already installed python, go to the next section.</span></span>

[<span data-ttu-id="8e490-146">Python için Windows Al</span><span class="sxs-lookup"><span data-stu-id="8e490-146">Get Python for Windows</span></span>](https://www.python.org/downloads/)

<span data-ttu-id="8e490-147">Ayrıca Python.exe'yi ve pip.exe yüklendiği için sistem klasörlerinin yolu eklemek gereken `PATH` ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="8e490-147">You also need to add the path of the folders where Python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="8e490-148">Varsayılan olarak, Python.exe'yi yüklü `C:\Python27` ve pip.exe yüklü `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="8e490-148">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="8e490-149">Azure CLI'yı yükleme</span><span class="sxs-lookup"><span data-stu-id="8e490-149">Install the Azure CLI</span></span>

<span data-ttu-id="8e490-150">Azure CLI yüklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="8e490-150">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="8e490-151">Yönetici olarak bir komut istemi penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="8e490-151">Open a Command Prompt window as an administrator.</span></span>

2. <span data-ttu-id="8e490-152">Azure CLI aşağıdaki komutları çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="8e490-152">Install the Azure CLI by running the following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="8e490-153">Yükleme 5 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="8e490-153">The installation might take 5 minutes.</span></span>

3. <span data-ttu-id="8e490-154">Aşağıdaki komutu çalıştırarak yüklemeyi doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="8e490-154">Verify the installation by running the following command:</span></span>

   ```cmd
   az iot -h
   ```

   <span data-ttu-id="8e490-155">Yükleme başarılı olursa aşağıdaki çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8e490-155">You should see the following output if the installation is successful.</span></span>

   ![Azure CLI yükleme doğrulayın](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="8e490-157">Visual Studio Kodu'nu yükle</span><span class="sxs-lookup"><span data-stu-id="8e490-157">Install Visual Studio Code</span></span>

<span data-ttu-id="8e490-158">Visual Studio Code öğreticide daha sonra yapılandırma dosyalarını düzenlemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="8e490-158">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="8e490-159">[Karşıdan](https://code.visualstudio.com/docs/setup/windows) ve Visual Studio Code yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8e490-159">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="8e490-160">Özet</span><span class="sxs-lookup"><span data-stu-id="8e490-160">Summary</span></span>

<span data-ttu-id="8e490-161">Tüm gerekli araçlar ve yazılım ana bilgisayara yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="8e490-161">You've installed all the required tools and software on your host computer.</span></span> <span data-ttu-id="8e490-162">Sonraki göreviniz IOT hub'ı oluşturun ve IOT hub'ınıza Cihazınızı kaydetmek için Azure CLI kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="8e490-162">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e490-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8e490-163">Next steps</span></span>
[<span data-ttu-id="8e490-164">IoT hub'ı oluşturma ve cihazınızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="8e490-164">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
