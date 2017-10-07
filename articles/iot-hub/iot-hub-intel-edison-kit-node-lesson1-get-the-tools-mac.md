---
title: "Intel Edison'u (düğüm) tooAzure IOT - Ders 1 bağlanın: Get Araçlar (macOS) | Microsoft Docs"
description: "Karşıdan yükleyip hello gerekli araçları ve yazılım için Edison'u hello ilk örnek uygulaması macOS üzerinde."
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
ms.openlocfilehash: f32c0ea3c69eb2f912171fd694ae883d2586c72e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="08da5-104">Merhaba Araçları (macOS 10.10) alın</span><span class="sxs-lookup"><span data-stu-id="08da5-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="08da5-105">[Windows 7 veya üzeri][windows]</span><span class="sxs-lookup"><span data-stu-id="08da5-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="08da5-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="08da5-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="08da5-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="08da5-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="08da5-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="08da5-108">What you will do</span></span>
<span data-ttu-id="08da5-109">Merhaba geliştirme araçları ve hello ilk örnek bir uygulama için Intel Edison'u hello yazılımını indirin.</span><span class="sxs-lookup"><span data-stu-id="08da5-109">Download hello development tools and hello software for hello first sample application for your Intel Edison.</span></span> <span data-ttu-id="08da5-110">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="08da5-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="08da5-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="08da5-111">What you will learn</span></span>
<span data-ttu-id="08da5-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="08da5-112">In this article, you will learn:</span></span>

* <span data-ttu-id="08da5-113">Nasıl tooinstall Git ve Node.js.</span><span class="sxs-lookup"><span data-stu-id="08da5-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="08da5-114">[Git](https://git-scm.com) bir açık kaynak dağıtılmış sürüm denetim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="08da5-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="08da5-115">Bu makale için Merhaba örnek uygulaması Git üzerinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="08da5-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="08da5-116">[Node.js](https://nodejs.org/en/) JavaScript çalışma zamanı zengin paket ekosistemi ile.</span><span class="sxs-lookup"><span data-stu-id="08da5-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="08da5-117">Nasıl toouse NPM tooinstall ek Node.js geliştirme araçları.</span><span class="sxs-lookup"><span data-stu-id="08da5-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="08da5-118">Merhaba gerekli en düşük sürümü Node.js 4.5 LTS ' dir.</span><span class="sxs-lookup"><span data-stu-id="08da5-118">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="08da5-119">[NPM](https://www.npmjs.com) hello Node.js paket yöneticilerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="08da5-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="08da5-120">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="08da5-120">What you need</span></span>
<span data-ttu-id="08da5-121">toocomplete bu işlem, gerekir:</span><span class="sxs-lookup"><span data-stu-id="08da5-121">toocomplete this operation, you will need:</span></span>
* <span data-ttu-id="08da5-122">Bir Internet bağlantısı toodownload geliştirme araçları hello ve yazılım hello.</span><span class="sxs-lookup"><span data-stu-id="08da5-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="08da5-123">MacOS Yosemite (10.10) çalıştıran bir Mac veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="08da5-123">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="08da5-124">Git ve Node.js yükleyin</span><span class="sxs-lookup"><span data-stu-id="08da5-124">Install Git and Node.js</span></span>
<span data-ttu-id="08da5-125">tooinstall Git ve Node.js kullanın hello [Homebrew](http://brew.sh) paket yönetimi yardımcı programı aşağıdaki adımları izleyerek:</span><span class="sxs-lookup"><span data-stu-id="08da5-125">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="08da5-126">Homebrew yükleyin.</span><span class="sxs-lookup"><span data-stu-id="08da5-126">Install Homebrew.</span></span> <span data-ttu-id="08da5-127">Homebrew zaten yüklediyseniz, toostep 2 gidin.</span><span class="sxs-lookup"><span data-stu-id="08da5-127">If you've already installed Homebrew, go toostep 2.</span></span>

   1. <span data-ttu-id="08da5-128">Tuşuna `Cmd + Space` ve girin `Terminal` tooopen bir terminal.</span><span class="sxs-lookup"><span data-stu-id="08da5-128">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="08da5-129">Merhaba aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="08da5-129">Run hello following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="08da5-130">Git ve Node.js hello aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="08da5-130">Install Git and Node.js by running hello following command:</span></span>

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="08da5-131">Ek Node.js geliştirme araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="08da5-131">Install additional Node.js development tools</span></span>
<span data-ttu-id="08da5-132">Kullanım [gulp.js](http://gulpjs.com) hello örnek uygulama tooyour Edison'u tooautomate hello dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="08da5-132">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Edison.</span></span>

<span data-ttu-id="08da5-133">Yükleme `gulp` komutu hello terminalde aşağıdaki hello çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="08da5-133">Install `gulp` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="08da5-134">Node.js ve bu ek geliştirme araçları üzerinde macOS yüklerken sorunlarla karşılaşırsanız, hello bkz [sorun giderme kılavuzu] [ troubleshooting] çözümleri toocommon sorunları.</span><span class="sxs-lookup"><span data-stu-id="08da5-134">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="08da5-135">Visual Studio Kodu'nu yükle</span><span class="sxs-lookup"><span data-stu-id="08da5-135">Install Visual Studio Code</span></span>
<span data-ttu-id="08da5-136">[Karşıdan](https://code.visualstudio.com/docs/setup/osx) ve Visual Studio Code yükleyin.</span><span class="sxs-lookup"><span data-stu-id="08da5-136">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="08da5-137">Visual Studio Code, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisidir.</span><span class="sxs-lookup"><span data-stu-id="08da5-137">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="08da5-138">Daha sonra hello öğretici tooedit hello örnek kodda bu Düzenleyicisi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="08da5-138">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="08da5-139">Özet</span><span class="sxs-lookup"><span data-stu-id="08da5-139">Summary</span></span>
<span data-ttu-id="08da5-140">Gerekli hello geliştirme araçları ve hello ilk örnek uygulama için yazılım yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="08da5-140">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="08da5-141">Merhaba sonraki toocreate bir görevdir, dağıtmak ve üzerinde Edison'u hello örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="08da5-141">hello next task is toocreate, deploy, and run hello sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08da5-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="08da5-142">Next steps</span></span>
<span data-ttu-id="08da5-143">[Merhaba blink uygulama oluşturun ve dağıtın][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="08da5-143">[Create and deploy hello blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
