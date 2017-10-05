---
title: "SensorTag cihaz & Azure IOT ağ geçidi - Ders 2: Get Araçlar (Ubuntu) | Microsoft Docs"
description: "Araçlar ve yazılım Ubuntu çalıştıran ana bilgisayarınıza yüklemek, IOT hub'ı oluşturun ve IOT hub'ı Cihazınızı kaydedin."
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
ms.openlocfilehash: 234b60e1f8eaff52ce07f54d4d12de2421cc1a52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="8a6ba-104">Araçları edinme (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="8a6ba-104">Get the tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8a6ba-105">Windows 7 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="8a6ba-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="8a6ba-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="8a6ba-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="8a6ba-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="8a6ba-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="8a6ba-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="8a6ba-108">What you will do</span></span>

- <span data-ttu-id="8a6ba-109">Git, Node.js, Gulp, Python yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8a6ba-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="8a6ba-110">Azure komut satırı arabirimi (Azure CLI) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8a6ba-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="8a6ba-111">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="8a6ba-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>
## <a name="what-you-will-learn"></a><span data-ttu-id="8a6ba-112">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="8a6ba-112">What you will learn</span></span>

<span data-ttu-id="8a6ba-113">Bu alıştırmanın ilerisinde şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="8a6ba-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="8a6ba-114">Git ve Node.js nasıl yüklenir.</span><span class="sxs-lookup"><span data-stu-id="8a6ba-114">How to install Git and Node.js.</span></span>
  - <span data-ttu-id="8a6ba-115">Git bir açık kaynak dağıtılmış sürüm denetim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="8a6ba-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="8a6ba-116">Örnek bir uygulama bu ders için Git üzerinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="8a6ba-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="8a6ba-117">Node.js, JavaScript çalışma zamanı zengin paket ekosistemi ile olur.</span><span class="sxs-lookup"><span data-stu-id="8a6ba-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="8a6ba-118">NPM Node.js Geliştirme Araçları'nı yüklemek için nasıl kullanılacağını.</span><span class="sxs-lookup"><span data-stu-id="8a6ba-118">How to use NPM to install Node.js development tools.</span></span>
  - <span data-ttu-id="8a6ba-119">Node.js, gerekli en düşük sürüm 4.5 LTS ' dir.</span><span class="sxs-lookup"><span data-stu-id="8a6ba-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="8a6ba-120">NPM Node.js paket yöneticilerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="8a6ba-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="8a6ba-121">Visual Studio Code yükleme.</span><span class="sxs-lookup"><span data-stu-id="8a6ba-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="8a6ba-122">Visual Studio platformlar arası, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisini kodudur.</span><span class="sxs-lookup"><span data-stu-id="8a6ba-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="8a6ba-123">Hata ayıklama, katıştırılmış Git denetimi, sözdizimi vurgulama, akıllı kod tamamlama, parçacıkları ve kod da yeniden düzenleme için harika desteğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="8a6ba-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="8a6ba-124">Azure CLI yükleme</span><span class="sxs-lookup"><span data-stu-id="8a6ba-124">How to install the Azure CLI</span></span>
  - <span data-ttu-id="8a6ba-125">Azure CLI, Azure için birden çok platformlu bir komut satırı deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="8a6ba-125">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="8a6ba-126">Doğrudan komut satırından sağlamak için çalışır ve kaynaklarını yönetme.</span><span class="sxs-lookup"><span data-stu-id="8a6ba-126">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="8a6ba-127">IOT hub'ı oluşturmak için Azure CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="8a6ba-127">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8a6ba-128">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="8a6ba-128">What you need</span></span>

- <span data-ttu-id="8a6ba-129">Araçlar ve yazılım indirmesi için Internet bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="8a6ba-129">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="8a6ba-130">Ubuntu 16.04 veya sonraki sürümünü çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="8a6ba-130">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="8a6ba-131">Git ve Node.js yükleyin</span><span class="sxs-lookup"><span data-stu-id="8a6ba-131">Install Git and Node.js</span></span>

<span data-ttu-id="8a6ba-132">Git ve Node.js yüklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="8a6ba-132">To install Git and Node.js, follow these steps:</span></span>

1. <span data-ttu-id="8a6ba-133">Tuşuna `Ctrl + Alt + T` bir Terminali açın.</span><span class="sxs-lookup"><span data-stu-id="8a6ba-133">Press `Ctrl + Alt + T` to open a terminal.</span></span>
2. <span data-ttu-id="8a6ba-134">Aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8a6ba-134">Run the following commands:</span></span>

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="8a6ba-135">Node.js geliştirme araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="8a6ba-135">Install Node.js development tools</span></span>

<span data-ttu-id="8a6ba-136">Kullandığınız [gulp.js](http://gulpjs.com/) dağıtım ve betiklerinin yürütülmesi otomatik hale getirmek için.</span><span class="sxs-lookup"><span data-stu-id="8a6ba-136">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="8a6ba-137">Gulp yüklemek için terminal aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8a6ba-137">To install gulp, run the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="8a6ba-138">Yükleme sorunlarıyla karşılaşırsanız, bkz: [sorun giderme kılavuzu](iot-hub-gateway-kit-c-troubleshooting.md) yaygın sorunların çözümleri için.</span><span class="sxs-lookup"><span data-stu-id="8a6ba-138">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="8a6ba-139">Düğüm, NPM ve Gulp Node.js içinde geliştirilen Otomasyon betikleri çalıştırmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="8a6ba-139">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="8a6ba-140">Azure CLI'yı yükleme</span><span class="sxs-lookup"><span data-stu-id="8a6ba-140">Install the Azure CLI</span></span>

<span data-ttu-id="8a6ba-141">Azure CLI yüklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="8a6ba-141">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="8a6ba-142">Terminale aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8a6ba-142">Run the following commands in the terminal:</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="8a6ba-143">Yükleme 5 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="8a6ba-143">The installation might take 5 minutes.</span></span>

2. <span data-ttu-id="8a6ba-144">Aşağıdaki komutu çalıştırarak yüklemeyi doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="8a6ba-144">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```
<span data-ttu-id="8a6ba-145">Yükleme başarılı olursa aşağıdaki çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a6ba-145">You should see the following output if the installation is successful.</span></span>
<span data-ttu-id="8a6ba-146">![Azure CLI yükleme doğrulayın](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="8a6ba-146">![Verify Azure CLI installation](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span></span>

### <a name="install-visual-studio-code"></a><span data-ttu-id="8a6ba-147">Visual Studio Kodu'nu yükle</span><span class="sxs-lookup"><span data-stu-id="8a6ba-147">Install Visual Studio Code</span></span>

<span data-ttu-id="8a6ba-148">Visual Studio Code öğreticide daha sonra yapılandırma dosyalarını düzenlemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="8a6ba-148">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="8a6ba-149">[Karşıdan](https://code.visualstudio.com/docs/setup/linux) ve Visual Studio Code yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8a6ba-149">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="8a6ba-150">Özet</span><span class="sxs-lookup"><span data-stu-id="8a6ba-150">Summary</span></span>

<span data-ttu-id="8a6ba-151">Tüm gerekli araçlar ve yazılım ana bilgisayara yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="8a6ba-151">You've installed all the required tools and software on your host computer.</span></span> <span data-ttu-id="8a6ba-152">Sonraki göreviniz IOT hub'ı oluşturun ve IOT hub'ınıza Cihazınızı kaydetmek için Azure CLI kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="8a6ba-152">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a6ba-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8a6ba-153">Next steps</span></span>
[<span data-ttu-id="8a6ba-154">IoT hub'ı oluşturma ve cihazınızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="8a6ba-154">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)
