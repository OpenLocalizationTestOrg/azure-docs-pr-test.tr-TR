---
title: "Azure IOT - Ders 1 Intel Edison'u (düğüm) bağlanma: Get Araçlar (macOS) | Microsoft Docs"
description: "Karşıdan yükle ve gerekli araçları ve Edison'u için ilk örnek uygulama için yazılım üzerinde macOS yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino geliştirme araçları, IOT geliştirme, IOT yazılım, Internet şeyler yazılımın, mac, yükleme düğümü js mac üzerinde yükleme git"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: fb6742be-2825-4524-89f7-8ccb7e7f1de1
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a5e406f49379e9f2192ee93334ab1dcf9f3e53d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="12018-104">Araçları edinme (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="12018-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="12018-105">[Windows 7 veya üzeri][windows]</span><span class="sxs-lookup"><span data-stu-id="12018-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="12018-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="12018-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="12018-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="12018-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="12018-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="12018-108">What you will do</span></span>
<span data-ttu-id="12018-109">Geliştirme araçları ve Intel Edison'u için ilk örnek uygulama için yazılım indirin.</span><span class="sxs-lookup"><span data-stu-id="12018-109">Download the development tools and the software for the first sample application for your Intel Edison.</span></span> <span data-ttu-id="12018-110">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="12018-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="12018-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="12018-111">What you will learn</span></span>
<span data-ttu-id="12018-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="12018-112">In this article, you will learn:</span></span>

* <span data-ttu-id="12018-113">Git ve Node.js nasıl yüklenir.</span><span class="sxs-lookup"><span data-stu-id="12018-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="12018-114">[Git](https://git-scm.com) bir açık kaynak dağıtılmış sürüm denetim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="12018-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="12018-115">Bu makalede örnek uygulama Git üzerinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="12018-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="12018-116">[Node.js](https://nodejs.org/en/) JavaScript çalışma zamanı zengin paket ekosistemi ile.</span><span class="sxs-lookup"><span data-stu-id="12018-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="12018-117">NPM ek Node.js Geliştirme Araçları'nı yüklemek için nasıl kullanılacağını.</span><span class="sxs-lookup"><span data-stu-id="12018-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="12018-118">Node.js, gerekli en düşük sürüm 4.5 LTS ' dir.</span><span class="sxs-lookup"><span data-stu-id="12018-118">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="12018-119">[NPM](https://www.npmjs.com) Node.js paket yöneticilerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="12018-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="12018-120">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="12018-120">What you need</span></span>
<span data-ttu-id="12018-121">Bu işlemi tamamlamak için gerekir:</span><span class="sxs-lookup"><span data-stu-id="12018-121">To complete this operation, you will need:</span></span>
* <span data-ttu-id="12018-122">Geliştirme araçları ve yazılım indirmesi için Internet bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="12018-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="12018-123">MacOS Yosemite (10.10) çalıştıran bir Mac veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="12018-123">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="12018-124">Git ve Node.js yükleyin</span><span class="sxs-lookup"><span data-stu-id="12018-124">Install Git and Node.js</span></span>
<span data-ttu-id="12018-125">Git ve Node.js yüklemek için kullandığınız [Homebrew](http://brew.sh) paket yönetimi yardımcı programı aşağıdaki adımları izleyerek:</span><span class="sxs-lookup"><span data-stu-id="12018-125">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="12018-126">Homebrew yükleyin.</span><span class="sxs-lookup"><span data-stu-id="12018-126">Install Homebrew.</span></span> <span data-ttu-id="12018-127">Homebrew zaten yüklediyseniz, 2. adıma geçin.</span><span class="sxs-lookup"><span data-stu-id="12018-127">If you've already installed Homebrew, go to step 2.</span></span>

   1. <span data-ttu-id="12018-128">Tuşuna `Cmd + Space` ve girin `Terminal` bir Terminali açın.</span><span class="sxs-lookup"><span data-stu-id="12018-128">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="12018-129">Şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="12018-129">Run the following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="12018-130">Git ve Node.js aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="12018-130">Install Git and Node.js by running the following command:</span></span>

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="12018-131">Ek Node.js geliştirme araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="12018-131">Install additional Node.js development tools</span></span>
<span data-ttu-id="12018-132">Kullanım [gulp.js](http://gulpjs.com) , Edison'u örnek uygulamaya dağıtımını otomatik hale getirmek için.</span><span class="sxs-lookup"><span data-stu-id="12018-132">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Edison.</span></span>

<span data-ttu-id="12018-133">Yükleme `gulp` terminale aşağıdaki komutu çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="12018-133">Install `gulp` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="12018-134">Node.js ve bu ek geliştirme araçları üzerinde macOS yüklerken sorunlarla karşılaşırsanız bkz [sorun giderme kılavuzu] [ troubleshooting] yaygın sorunların çözümleri için.</span><span class="sxs-lookup"><span data-stu-id="12018-134">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="12018-135">Visual Studio Kodu'nu yükle</span><span class="sxs-lookup"><span data-stu-id="12018-135">Install Visual Studio Code</span></span>
<span data-ttu-id="12018-136">[Karşıdan](https://code.visualstudio.com/docs/setup/osx) ve Visual Studio Code yükleyin.</span><span class="sxs-lookup"><span data-stu-id="12018-136">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="12018-137">Visual Studio Code, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisidir.</span><span class="sxs-lookup"><span data-stu-id="12018-137">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="12018-138">Örnek kod düzenlemek için öğreticide daha sonra bu Düzenleyicisi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="12018-138">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="12018-139">Özet</span><span class="sxs-lookup"><span data-stu-id="12018-139">Summary</span></span>
<span data-ttu-id="12018-140">İlk örnek uygulama için yazılım ve gerekli geliştirme araçları yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="12018-140">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="12018-141">Sonraki oluşturmak, dağıtmak ve örnek uygulama Edison'u üzerinde çalıştırmak için bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="12018-141">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12018-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="12018-142">Next steps</span></span>
<span data-ttu-id="12018-143">[Blink uygulama oluşturun ve dağıtın][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="12018-143">[Create and deploy the blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
