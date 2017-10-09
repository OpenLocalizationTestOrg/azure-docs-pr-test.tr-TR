---
title: "Benzetimli cihaz & Azure IOT ağ geçidi - Ders 2: Get Araçlar (macOS) | Microsoft Docs"
description: "Araçlar Mac bilgisayarınıza yüklemek, IOT hub'ı oluşturun ve hello IOT hub'da Cihazınızı kaydedin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IOT geliştirme, IOT yazılım, IOT bulut hizmeti, Internet şeyler yazılım, azure CLI yükleme python mac, mac, çalıştırmak, yükleme düğümü js mac gulp Git'i yükleyin"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 42f9d186-e20c-4ef9-98cc-71d39e058b06
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 391d60f3cbb209698cae53098efed360ac0f5fad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos"></a><span data-ttu-id="e1e83-104">Merhaba Araçları (macOS) alın</span><span class="sxs-lookup"><span data-stu-id="e1e83-104">Get hello tools (macOS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e1e83-105">Windows 7 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="e1e83-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="e1e83-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="e1e83-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="e1e83-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="e1e83-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="e1e83-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="e1e83-108">What you will do</span></span>

- <span data-ttu-id="e1e83-109">Git, Node.js, Gulp, Python yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e1e83-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="e1e83-110">Hello Azure komut satırı arabirimi (Azure CLI) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e1e83-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="e1e83-111">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e1e83-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e1e83-112">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="e1e83-112">What you will learn</span></span>

<span data-ttu-id="e1e83-113">Bu alıştırmanın ilerisinde şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="e1e83-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="e1e83-114">Nasıl tooinstall [Git](https://git-scm.com/) ve [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="e1e83-114">How tooinstall [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="e1e83-115">Git bir açık kaynak dağıtılmış sürüm denetim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="e1e83-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="e1e83-116">Merhaba örnek bir uygulama bu ders için Git üzerinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="e1e83-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="e1e83-117">Node.js, JavaScript çalışma zamanı zengin paket ekosistemi ile olur.</span><span class="sxs-lookup"><span data-stu-id="e1e83-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="e1e83-118">Nasıl toouse [NPM](https://www.npmjs.com/) tooinstall Node.js geliştirme araçları.</span><span class="sxs-lookup"><span data-stu-id="e1e83-118">How toouse [NPM](https://www.npmjs.com/) tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="e1e83-119">Merhaba gerekli en düşük sürümü Node.js 4.5 LTS ' dir.</span><span class="sxs-lookup"><span data-stu-id="e1e83-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="e1e83-120">NPM hello paket Node.js yöneticilerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="e1e83-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="e1e83-121">Nasıl tooinstall Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e1e83-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="e1e83-122">Visual Studio platformlar arası, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisini kodudur.</span><span class="sxs-lookup"><span data-stu-id="e1e83-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="e1e83-123">Hata ayıklama, katıştırılmış Git denetimi, sözdizimi vurgulama, akıllı kod tamamlama, parçacıkları ve kod da yeniden düzenleme için harika desteğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e1e83-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="e1e83-124">Nasıl tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="e1e83-124">How tooinstall Python.</span></span>
  - <span data-ttu-id="e1e83-125">Python yaygın olarak kullanılan üst düzey, genel amaçlı, yorumlanan ve dinamik programlama dilidir.</span><span class="sxs-lookup"><span data-stu-id="e1e83-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="e1e83-126">Nasıl tooinstall Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="e1e83-126">How tooinstall hello Azure CLI.</span></span>
  - <span data-ttu-id="e1e83-127">Hello Azure CLI, Azure için birden çok platformlu bir komut satırı deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="e1e83-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="e1e83-128">Doğrudan bir komut satırı tooprovision çalışma ve kaynaklarını yönetme.</span><span class="sxs-lookup"><span data-stu-id="e1e83-128">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="e1e83-129">Nasıl toouse hello Azure CLI toocreate IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="e1e83-129">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e1e83-130">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="e1e83-130">What you need</span></span>

- <span data-ttu-id="e1e83-131">Bir Internet bağlantısı toodownload araçları ve yazılım hello.</span><span class="sxs-lookup"><span data-stu-id="e1e83-131">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="e1e83-132">OS X Yosemite (10.10) veya sonraki sürümü çalıştıran bir Mac bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="e1e83-132">A Mac computer that’s running OS X Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="e1e83-133">Git ve Node.js yükleyin</span><span class="sxs-lookup"><span data-stu-id="e1e83-133">Install Git and Node.js</span></span>

<span data-ttu-id="e1e83-134">tooinstall Git ve Node.js, aşağıdaki adımları izleyerek hello Homebrew paket yönetimi yardımcı programı kullanın:</span><span class="sxs-lookup"><span data-stu-id="e1e83-134">tooinstall Git and Node.js, use hello Homebrew package management utility by following these steps:</span></span>

1. <span data-ttu-id="e1e83-135">[Karşıdan](http://brew.sh/) ve Homebrew yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e1e83-135">[Download](http://brew.sh/) and install Homebrew.</span></span> <span data-ttu-id="e1e83-136">Homebrew zaten yüklediyseniz, toostep 2 gidin.</span><span class="sxs-lookup"><span data-stu-id="e1e83-136">If you’ve already installed Homebrew, go toostep 2.</span></span>
   1. <span data-ttu-id="e1e83-137">Tuşuna `Cmd + Space` ve girin `Terminal` tooopen bir terminal.</span><span class="sxs-lookup"><span data-stu-id="e1e83-137">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="e1e83-138">Merhaba aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e1e83-138">Run hello following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. <span data-ttu-id="e1e83-139">Git ve Node.js hello aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="e1e83-139">Install Git and Node.js by running hello following command:</span></span>

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="e1e83-140">Node.js geliştirme araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="e1e83-140">Install Node.js development tools</span></span>

<span data-ttu-id="e1e83-141">Kullandığınız [gulp.js](http://gulpjs.com/) tooautomate dağıtım ve komut dosyası yürütme.</span><span class="sxs-lookup"><span data-stu-id="e1e83-141">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="e1e83-142">tooinstall gulp, komut hello terminalde aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e1e83-142">tooinstall gulp, run hello following command in hello terminal:</span></span>

```bash
npm install -g gulp
```

<span data-ttu-id="e1e83-143">Merhaba yükleme sorunlarıyla karşılaşırsanız, hello bkz [sorun giderme kılavuzu](iot-hub-gateway-kit-c-sim-troubleshooting.md) çözümleri toocommon sorunları.</span><span class="sxs-lookup"><span data-stu-id="e1e83-143">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="e1e83-144">Düğüm, NPM ve Gulp Node.js içinde geliştirilen gerekli toorun Otomasyon betikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="e1e83-144">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="e1e83-145">Python yüklemek</span><span class="sxs-lookup"><span data-stu-id="e1e83-145">Install Python</span></span>

<span data-ttu-id="e1e83-146">Mac OS X ile Python 2.7 gelse Homebrew aracılığıyla Python yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="e1e83-146">Although Mac OS X comes with Python 2.7, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="e1e83-147">Bkz: [Python Mac OS X yükleme](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="e1e83-147">See [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="e1e83-148">Python ve PIP hello aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="e1e83-148">Install Python and pip by running hello following command:</span></span>

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a><span data-ttu-id="e1e83-149">Hello Azure CLI yükleme</span><span class="sxs-lookup"><span data-stu-id="e1e83-149">Install hello Azure CLI</span></span>

<span data-ttu-id="e1e83-150">tooinstall hello Azure CLI, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="e1e83-150">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="e1e83-151">Komutları hello terminalde aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e1e83-151">Run hello following commands in hello terminal:</span></span>
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   <span data-ttu-id="e1e83-152">Merhaba yükleme 5 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="e1e83-152">hello installation might take 5 minutes.</span></span>

2. <span data-ttu-id="e1e83-153">Merhaba aşağıdaki komutu çalıştırarak Hello yüklemeyi doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="e1e83-153">Verify hello installation by running hello following command:</span></span>
   ```bash
   az iot -h
   ```
   <span data-ttu-id="e1e83-154">Merhaba yükleme başarılı olup olmadığını hello aşağıdaki çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1e83-154">You should see hello following output if hello installation is successful.</span></span>

   ![Azure CLI yükleme doğrulayın](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="e1e83-156">Visual Studio Kodu'nu yükle</span><span class="sxs-lookup"><span data-stu-id="e1e83-156">Install Visual Studio Code</span></span>

<span data-ttu-id="e1e83-157">Visual Studio Code daha sonra hello öğretici tooedit yapılandırma dosyalarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="e1e83-157">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="e1e83-158">[Karşıdan](https://code.visualstudio.com/docs/setup/osx) ve Visual Studio Code yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e1e83-158">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="e1e83-159">Özet</span><span class="sxs-lookup"><span data-stu-id="e1e83-159">Summary</span></span>

<span data-ttu-id="e1e83-160">Mac bilgisayarda tüm gerekli hello araçları ve yazılımı yüklediğiniz.</span><span class="sxs-lookup"><span data-stu-id="e1e83-160">You’ve installed all hello required tools and software on your Mac computer.</span></span> <span data-ttu-id="e1e83-161">Sonraki görev toouse hello Azure CLI toocreate IOT hub'ı ve IOT hub'ınıza Cihazınızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e1e83-161">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1e83-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e1e83-162">Next steps</span></span>
[<span data-ttu-id="e1e83-163">IOT hub'ı oluşturma ve cihaz kaydetme</span><span class="sxs-lookup"><span data-stu-id="e1e83-163">Create an IoT hub and register Device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
