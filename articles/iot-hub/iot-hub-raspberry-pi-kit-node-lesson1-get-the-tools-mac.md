---
title: "Raspberry Pi'yi (düğüm) tooAzure IOT - Ders 1 bağlanın: Get Araçlar (macOS) | Microsoft Docs"
description: "Karşıdan yükleyip hello gerekli araçları ve yazılım için Pi hello ilk örnek uygulaması macOS üzerinde."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IOT geliştirme IOT yazılım, Internet şeyler yazılımların python mac yükleyin, mac Git'i yükleyin, çalışma gulp, düğüm js mac yükleyin"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 2ea6d211-c0e8-4ade-ac69-d1c2261d78c4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 382b066cb7ece7ffdeb22b162b725727b22e5fac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="32047-104">Merhaba Araçları (macOS 10.10) alın</span><span class="sxs-lookup"><span data-stu-id="32047-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="32047-105">Windows 7 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="32047-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="32047-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="32047-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="32047-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="32047-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="32047-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="32047-108">What you will do</span></span>
<span data-ttu-id="32047-109">Merhaba geliştirme araçları ve hello ilk örnek bir uygulama için Raspberry Pi 3 hello yazılımı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="32047-109">Download hello development tools and hello software for hello first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="32047-110">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="32047-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="32047-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="32047-111">What you will learn</span></span>
<span data-ttu-id="32047-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="32047-112">In this article, you will learn:</span></span>

* <span data-ttu-id="32047-113">Nasıl tooinstall Git ve Node.js.</span><span class="sxs-lookup"><span data-stu-id="32047-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="32047-114">[Git](https://git-scm.com) bir açık kaynak dağıtılmış sürüm denetim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="32047-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="32047-115">Bu makale için Merhaba örnek uygulaması Git üzerinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="32047-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="32047-116">[Node.js](https://nodejs.org/en/) JavaScript çalışma zamanı zengin paket ekosistemi ile.</span><span class="sxs-lookup"><span data-stu-id="32047-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="32047-117">Nasıl toouse NPM tooinstall ek Node.js geliştirme araçları.</span><span class="sxs-lookup"><span data-stu-id="32047-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="32047-118">Merhaba gerekli en düşük sürümü Node.js 4.5 LTS ' dir.</span><span class="sxs-lookup"><span data-stu-id="32047-118">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="32047-119">[NPM](https://www.npmjs.com) hello Node.js paket yöneticilerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="32047-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="32047-120">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="32047-120">What you need</span></span>
<span data-ttu-id="32047-121">toocomplete bu işlem, gerekir:</span><span class="sxs-lookup"><span data-stu-id="32047-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="32047-122">Bir Internet bağlantısı toodownload geliştirme araçları hello ve yazılım hello.</span><span class="sxs-lookup"><span data-stu-id="32047-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="32047-123">MacOS Yosemite (10.10) çalıştıran bir Mac veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="32047-123">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="32047-124">Git ve Node.js yükleyin</span><span class="sxs-lookup"><span data-stu-id="32047-124">Install Git and Node.js</span></span>
<span data-ttu-id="32047-125">tooinstall Git ve Node.js kullanın hello [Homebrew](http://brew.sh) paket yönetimi yardımcı programı aşağıdaki adımları izleyerek:</span><span class="sxs-lookup"><span data-stu-id="32047-125">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="32047-126">Homebrew yükleyin.</span><span class="sxs-lookup"><span data-stu-id="32047-126">Install Homebrew.</span></span> <span data-ttu-id="32047-127">Homebrew zaten yüklediyseniz, toostep 2 gidin.</span><span class="sxs-lookup"><span data-stu-id="32047-127">If you've already installed Homebrew, go toostep 2.</span></span>
   
   1. <span data-ttu-id="32047-128">Tuşuna `Cmd + Space` ve girin `Terminal` tooopen bir terminal.</span><span class="sxs-lookup"><span data-stu-id="32047-128">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="32047-129">Merhaba aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="32047-129">Run hello following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="32047-130">Git ve Node.js hello aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="32047-130">Install Git and Node.js by running hello following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="32047-131">Ek Node.js geliştirme araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="32047-131">Install additional Node.js development tools</span></span>
<span data-ttu-id="32047-132">Kullanım [gulp.js](http://gulpjs.com) hello örnek uygulama tooPi tooautomate hello dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="32047-132">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="32047-133">Kullanım hello [aygıt bulma CLI](https://github.com/Azure/device-discovery-cli) IOT aygıtlarınızla ilgili tooretrieve ağ bilgileri.</span><span class="sxs-lookup"><span data-stu-id="32047-133">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="32047-134">Yükleme `gulp` ve `device-discovery-cli` komutu hello terminalde aşağıdaki hello çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="32047-134">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="32047-135">Node.js ve bu ek geliştirme araçları üzerinde macOS yüklerken sorunlarla karşılaşırsanız, hello bkz [sorun giderme kılavuzu](iot-hub-raspberry-pi-kit-node-troubleshooting.md) çözümleri toocommon sorunları.</span><span class="sxs-lookup"><span data-stu-id="32047-135">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="32047-136">Visual Studio Kodu'nu yükle</span><span class="sxs-lookup"><span data-stu-id="32047-136">Install Visual Studio Code</span></span>
<span data-ttu-id="32047-137">[Karşıdan](https://code.visualstudio.com/docs/setup/osx) ve Visual Studio Code yükleyin.</span><span class="sxs-lookup"><span data-stu-id="32047-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="32047-138">Visual Studio Code, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisidir.</span><span class="sxs-lookup"><span data-stu-id="32047-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="32047-139">Daha sonra hello öğretici tooedit hello örnek kodda bu Düzenleyicisi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="32047-139">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="32047-140">Özet</span><span class="sxs-lookup"><span data-stu-id="32047-140">Summary</span></span>
<span data-ttu-id="32047-141">Gerekli hello geliştirme araçları ve hello ilk örnek uygulama için yazılım yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="32047-141">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="32047-142">Merhaba sonraki toocreate bir görevdir, dağıtmak ve üzerinde Pi hello örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="32047-142">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32047-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="32047-143">Next steps</span></span>
[<span data-ttu-id="32047-144">Merhaba blink örnek uygulama oluşturun ve dağıtın</span><span class="sxs-lookup"><span data-stu-id="32047-144">Create and deploy hello blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

