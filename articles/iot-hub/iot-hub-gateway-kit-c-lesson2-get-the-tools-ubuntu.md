---
title: "SensorTag cihaz & Azure IOT ağ geçidi - Ders 2: Get Araçlar (Ubuntu) | Microsoft Docs"
description: "Merhaba araçları ve hello yazılım Ubuntu çalıştıran ana bilgisayarınıza yüklemek, IOT hub'ı oluşturun ve hello IOT hub'da Cihazınızı kaydedin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IOT geliştirme, IOT yazılım IOT bulut hizmeti, şeyler yazılım, azure CLI, Internet üzerinde ubuntu Git'i yükleyin, çalışma gulp, düğüm js ubuntu yükleyin"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0bac1412-385b-4255-a33f-9d44c35feb3e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c9edca91e791ef914b1920178b66eadd12ae0281
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="f3d1b-104">Merhaba Araçları (Ubuntu 16.04) alın</span><span class="sxs-lookup"><span data-stu-id="f3d1b-104">Get hello tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f3d1b-105">Windows 7 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="f3d1b-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="f3d1b-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="f3d1b-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="f3d1b-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="f3d1b-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="f3d1b-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="f3d1b-108">What you will do</span></span>

- <span data-ttu-id="f3d1b-109">Git, Node.js, Gulp, Python yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="f3d1b-110">Hello Azure komut satırı arabirimi (Azure CLI) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="f3d1b-111">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f3d1b-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>
## <a name="what-you-will-learn"></a><span data-ttu-id="f3d1b-112">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="f3d1b-112">What you will learn</span></span>

<span data-ttu-id="f3d1b-113">Bu alıştırmanın ilerisinde şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="f3d1b-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="f3d1b-114">Nasıl tooinstall Git ve Node.js.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-114">How tooinstall Git and Node.js.</span></span>
  - <span data-ttu-id="f3d1b-115">Git bir açık kaynak dağıtılmış sürüm denetim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="f3d1b-116">Merhaba örnek bir uygulama bu ders için Git üzerinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="f3d1b-117">Node.js, JavaScript çalışma zamanı zengin paket ekosistemi ile olur.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="f3d1b-118">Nasıl toouse NPM tooinstall Node.js geliştirme araçları.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-118">How toouse NPM tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="f3d1b-119">Merhaba gerekli en düşük sürümü Node.js 4.5 LTS ' dir.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="f3d1b-120">NPM hello paket Node.js yöneticilerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="f3d1b-121">Nasıl tooinstall Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="f3d1b-122">Visual Studio platformlar arası, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisini kodudur.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="f3d1b-123">Hata ayıklama, katıştırılmış Git denetimi, sözdizimi vurgulama, akıllı kod tamamlama, parçacıkları ve kod da yeniden düzenleme için harika desteğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="f3d1b-124">Nasıl tooinstall hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f3d1b-124">How tooinstall hello Azure CLI</span></span>
  - <span data-ttu-id="f3d1b-125">Hello Azure CLI, Azure için birden çok platformlu bir komut satırı deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-125">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="f3d1b-126">Doğrudan bir komut satırı tooprovision çalışma ve kaynaklarını yönetme.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-126">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="f3d1b-127">Nasıl toouse hello Azure CLI toocreate IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-127">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f3d1b-128">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="f3d1b-128">What you need</span></span>

- <span data-ttu-id="f3d1b-129">Bir Internet bağlantısı toodownload araçları ve yazılım hello.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-129">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="f3d1b-130">Ubuntu 16.04 veya sonraki sürümünü çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-130">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="f3d1b-131">Git ve Node.js yükleyin</span><span class="sxs-lookup"><span data-stu-id="f3d1b-131">Install Git and Node.js</span></span>

<span data-ttu-id="f3d1b-132">tooinstall Git ve Node.js, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="f3d1b-132">tooinstall Git and Node.js, follow these steps:</span></span>

1. <span data-ttu-id="f3d1b-133">Tuşuna `Ctrl + Alt + T` tooopen bir terminal.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-133">Press `Ctrl + Alt + T` tooopen a terminal.</span></span>
2. <span data-ttu-id="f3d1b-134">Merhaba aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f3d1b-134">Run hello following commands:</span></span>

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="f3d1b-135">Node.js geliştirme araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="f3d1b-135">Install Node.js development tools</span></span>

<span data-ttu-id="f3d1b-136">Kullandığınız [gulp.js](http://gulpjs.com/) tooautomate dağıtım ve komut dosyası yürütme.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-136">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="f3d1b-137">tooinstall gulp, komut hello terminalde aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f3d1b-137">tooinstall gulp, run hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="f3d1b-138">Merhaba yükleme sorunlarıyla karşılaşırsanız, hello bkz [sorun giderme kılavuzu](iot-hub-gateway-kit-c-troubleshooting.md) çözümleri toocommon sorunları.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-138">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="f3d1b-139">Düğüm, NPM ve Gulp Node.js içinde geliştirilen gerekli toorun Otomasyon betikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-139">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="f3d1b-140">Hello Azure CLI yükleme</span><span class="sxs-lookup"><span data-stu-id="f3d1b-140">Install hello Azure CLI</span></span>

<span data-ttu-id="f3d1b-141">tooinstall hello Azure CLI, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="f3d1b-141">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="f3d1b-142">Komutları hello terminalde aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f3d1b-142">Run hello following commands in hello terminal:</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="f3d1b-143">Merhaba yükleme 5 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-143">hello installation might take 5 minutes.</span></span>

2. <span data-ttu-id="f3d1b-144">Merhaba aşağıdaki komutu çalıştırarak Hello yüklemeyi doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="f3d1b-144">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```
<span data-ttu-id="f3d1b-145">Merhaba yükleme başarılı olup olmadığını hello aşağıdaki çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-145">You should see hello following output if hello installation is successful.</span></span>
<span data-ttu-id="f3d1b-146">![Azure CLI yükleme doğrulayın](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="f3d1b-146">![Verify Azure CLI installation](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span></span>

### <a name="install-visual-studio-code"></a><span data-ttu-id="f3d1b-147">Visual Studio Kodu'nu yükle</span><span class="sxs-lookup"><span data-stu-id="f3d1b-147">Install Visual Studio Code</span></span>

<span data-ttu-id="f3d1b-148">Visual Studio Code daha sonra hello öğretici tooedit yapılandırma dosyalarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-148">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="f3d1b-149">[Karşıdan](https://code.visualstudio.com/docs/setup/linux) ve Visual Studio Code yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-149">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="f3d1b-150">Özet</span><span class="sxs-lookup"><span data-stu-id="f3d1b-150">Summary</span></span>

<span data-ttu-id="f3d1b-151">Tüm gerekli hello araçları ve yazılım ana bilgisayara yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-151">You've installed all hello required tools and software on your host computer.</span></span> <span data-ttu-id="f3d1b-152">Sonraki görev toouse hello Azure CLI toocreate IOT hub'ı ve IOT hub'ınıza Cihazınızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f3d1b-152">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3d1b-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f3d1b-153">Next steps</span></span>
[<span data-ttu-id="f3d1b-154">IoT hub'ı oluşturma ve cihazınızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="f3d1b-154">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)
