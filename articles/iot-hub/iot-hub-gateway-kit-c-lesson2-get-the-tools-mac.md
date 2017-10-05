---
title: "SensorTag cihaz & Azure IOT ağ geçidi - Ders 2: Get Araçlar (macOS) | Microsoft Docs"
description: "Mac bilgisayarda araçlarını yükleme, IOT hub'ı oluşturun ve IOT hub'ı Cihazınızı kaydedin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IOT geliştirme, IOT yazılım, IOT bulut hizmeti, Internet şeyler yazılım, azure CLI yükleme python mac, mac, çalıştırmak, yükleme düğümü js mac gulp Git'i yükleyin"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 94e538ef-9857-4023-9c3c-e92a0be7c395
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 07bc5f2cf6542273c334371b77520c674c5d2f00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos"></a><span data-ttu-id="33139-104">(MacOS) araçları edinin</span><span class="sxs-lookup"><span data-stu-id="33139-104">Get the tools (MacOS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="33139-105">Windows 7 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="33139-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="33139-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="33139-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="33139-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="33139-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="33139-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="33139-108">What you will do</span></span>

- <span data-ttu-id="33139-109">Git, Node.js, Gulp, Python yükleyin.</span><span class="sxs-lookup"><span data-stu-id="33139-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="33139-110">Azure komut satırı arabirimi (Azure CLI) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="33139-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="33139-111">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="33139-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="33139-112">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="33139-112">What you will learn</span></span>

<span data-ttu-id="33139-113">Bu alıştırmanın ilerisinde şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="33139-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="33139-114">Yükleme [Git](https://git-scm.com/) ve [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="33139-114">How to install [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="33139-115">Git bir açık kaynak dağıtılmış sürüm denetim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="33139-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="33139-116">Örnek bir uygulama bu ders için Git üzerinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="33139-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="33139-117">Node.js, JavaScript çalışma zamanı zengin paket ekosistemi ile olur.</span><span class="sxs-lookup"><span data-stu-id="33139-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="33139-118">Nasıl kullanılacağını [NPM](https://www.npmjs.com/) Node.js geliştirme araçlarını yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="33139-118">How to use [NPM](https://www.npmjs.com/) to install Node.js development tools.</span></span>
  - <span data-ttu-id="33139-119">Node.js, gerekli en düşük sürüm 4.5 LTS ' dir.</span><span class="sxs-lookup"><span data-stu-id="33139-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="33139-120">NPM Node.js paket yöneticilerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="33139-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="33139-121">Visual Studio Code yükleme.</span><span class="sxs-lookup"><span data-stu-id="33139-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="33139-122">Visual Studio platformlar arası, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisini kodudur.</span><span class="sxs-lookup"><span data-stu-id="33139-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="33139-123">Hata ayıklama, katıştırılmış Git denetimi, sözdizimi vurgulama, akıllı kod tamamlama, parçacıkları ve kod da yeniden düzenleme için harika desteğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="33139-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="33139-124">Python yükleme.</span><span class="sxs-lookup"><span data-stu-id="33139-124">How to install Python.</span></span>
  - <span data-ttu-id="33139-125">Python yaygın olarak kullanılan üst düzey, genel amaçlı, yorumlanan ve dinamik programlama dilidir.</span><span class="sxs-lookup"><span data-stu-id="33139-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="33139-126">Azure CLI yükleme.</span><span class="sxs-lookup"><span data-stu-id="33139-126">How to install the Azure CLI.</span></span>
  - <span data-ttu-id="33139-127">Azure CLI, Azure için birden çok platformlu bir komut satırı deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="33139-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="33139-128">Doğrudan komut satırından sağlamak için çalışır ve kaynaklarını yönetme.</span><span class="sxs-lookup"><span data-stu-id="33139-128">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="33139-129">IOT hub'ı oluşturmak için Azure CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="33139-129">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="33139-130">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="33139-130">What you need</span></span>

- <span data-ttu-id="33139-131">Araçlar ve yazılım indirmesi için Internet bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="33139-131">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="33139-132">OS X Yosemite (10.10) veya sonraki sürümü çalıştıran bir Mac bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="33139-132">A Mac computer that’s running OS X Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="33139-133">Git ve Node.js yükleyin</span><span class="sxs-lookup"><span data-stu-id="33139-133">Install Git and Node.js</span></span>

<span data-ttu-id="33139-134">Git ve Node.js yüklemek için aşağıdaki adımları izleyerek Homebrew paket yönetimi yardımcı programı'nı kullanın:</span><span class="sxs-lookup"><span data-stu-id="33139-134">To install Git and Node.js, use the Homebrew package management utility by following these steps:</span></span>

1. <span data-ttu-id="33139-135">[Karşıdan](http://brew.sh/) ve Homebrew yükleyin.</span><span class="sxs-lookup"><span data-stu-id="33139-135">[Download](http://brew.sh/) and install Homebrew.</span></span> <span data-ttu-id="33139-136">Homebrew zaten yüklediyseniz, 2. adıma geçin.</span><span class="sxs-lookup"><span data-stu-id="33139-136">If you’ve already installed Homebrew, go to step 2.</span></span>
   1. <span data-ttu-id="33139-137">Tuşuna `Cmd + Space` ve girin `Terminal` bir Terminali açın.</span><span class="sxs-lookup"><span data-stu-id="33139-137">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="33139-138">Şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="33139-138">Run the following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. <span data-ttu-id="33139-139">Git ve Node.js aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="33139-139">Install Git and Node.js by running the following command:</span></span>

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="33139-140">Node.js geliştirme araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="33139-140">Install Node.js development tools</span></span>

<span data-ttu-id="33139-141">Kullandığınız [gulp.js](http://gulpjs.com/) dağıtım ve betiklerinin yürütülmesi otomatik hale getirmek için.</span><span class="sxs-lookup"><span data-stu-id="33139-141">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="33139-142">Gulp yüklemek için terminal aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="33139-142">To install gulp, run the following command in the terminal:</span></span>

```bash
npm install -g gulp
```

<span data-ttu-id="33139-143">Yükleme sorunlarıyla karşılaşırsanız, bkz: [sorun giderme kılavuzu](iot-hub-gateway-kit-c-troubleshooting.md) yaygın sorunların çözümleri için.</span><span class="sxs-lookup"><span data-stu-id="33139-143">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="33139-144">Düğüm, NPM ve Gulp Node.js içinde geliştirilen Otomasyon betikleri çalıştırmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="33139-144">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="33139-145">Python yüklemek</span><span class="sxs-lookup"><span data-stu-id="33139-145">Install Python</span></span>

<span data-ttu-id="33139-146">Mac OS X ile Python 2.7 gelse Homebrew aracılığıyla Python yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="33139-146">Although Mac OS X comes with Python 2.7, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="33139-147">Bkz: [Python Mac OS X yükleme](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="33139-147">See [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="33139-148">Python ve PIP aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="33139-148">Install Python and pip by running the following command:</span></span>

```bash
brew install python
```

## <a name="install-the-azure-cli"></a><span data-ttu-id="33139-149">Azure CLI'yı yükleme</span><span class="sxs-lookup"><span data-stu-id="33139-149">Install the Azure CLI</span></span>

<span data-ttu-id="33139-150">Azure CLI yüklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="33139-150">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="33139-151">Terminale aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="33139-151">Run the following commands in the terminal:</span></span>
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   <span data-ttu-id="33139-152">Yükleme 5 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="33139-152">The installation might take 5 minutes.</span></span>

2. <span data-ttu-id="33139-153">Aşağıdaki komutu çalıştırarak yüklemeyi doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="33139-153">Verify the installation by running the following command:</span></span>
   ```bash
   az iot -h
   ```
   <span data-ttu-id="33139-154">Yükleme başarılı olursa aşağıdaki çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="33139-154">You should see the following output if the installation is successful.</span></span>

   ![Azure CLI yükleme doğrulayın](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="33139-156">Visual Studio Kodu'nu yükle</span><span class="sxs-lookup"><span data-stu-id="33139-156">Install Visual Studio Code</span></span>

<span data-ttu-id="33139-157">Visual Studio Code öğreticide daha sonra yapılandırma dosyalarını düzenlemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="33139-157">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="33139-158">[Karşıdan](https://code.visualstudio.com/docs/setup/osx) ve Visual Studio Code yükleyin.</span><span class="sxs-lookup"><span data-stu-id="33139-158">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="33139-159">Özet</span><span class="sxs-lookup"><span data-stu-id="33139-159">Summary</span></span>

<span data-ttu-id="33139-160">Mac bilgisayarda tüm gerekli araçlar ve yazılımı yüklediğiniz.</span><span class="sxs-lookup"><span data-stu-id="33139-160">You’ve installed all the required tools and software on your Mac computer.</span></span> <span data-ttu-id="33139-161">Sonraki göreviniz IOT hub'ı oluşturun ve IOT hub'ınıza Cihazınızı kaydetmek için Azure CLI kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="33139-161">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33139-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="33139-162">Next steps</span></span>
[<span data-ttu-id="33139-163">IOT hub'ı oluşturma ve cihaz kaydetme</span><span class="sxs-lookup"><span data-stu-id="33139-163">Create an IoT hub and register Device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)
