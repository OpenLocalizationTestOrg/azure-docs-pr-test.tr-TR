---
title: "Connect Raspberry pi (C) tooAzure IOT - Ders 1: Get Araçlar (macOS) | Microsoft Docs"
description: "Karşıdan yükleyip hello gerekli araçları ve yazılım için Pi hello ilk örnek uygulaması macOS üzerinde."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IOT geliştirme, IOT yazılım, Internet şeyler yazılımın, Mac, çalıştırmak, yükleme düğümü js mac gulp yükleme git"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fc6bd2c8-a847-4bf5-818f-6f7f9a6835ee
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 68ee44945dd69edcdf61ab3da4c80379c0ef955d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="001bd-104">Merhaba Araçları (macOS 10.10) alın</span><span class="sxs-lookup"><span data-stu-id="001bd-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="001bd-105">Windows 7 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="001bd-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="001bd-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="001bd-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="001bd-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="001bd-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="001bd-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="001bd-108">What you will do</span></span>
<span data-ttu-id="001bd-109">Merhaba geliştirme araçları ve hello ilk örnek bir uygulama için Raspberry Pi 3 hello yazılımı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="001bd-109">Download hello development tools and hello software for hello first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="001bd-110">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="001bd-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="001bd-111">Programlama dili hello ana mantığı hello C olsa da, Node.js araçları hello dersleri toodiscover cihazları kullanılır ve yapı ve örnek uygulamaları dağıtın.</span><span class="sxs-lookup"><span data-stu-id="001bd-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toodiscover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="001bd-112">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="001bd-112">What you will learn</span></span>
<span data-ttu-id="001bd-113">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="001bd-113">In this article, you will learn:</span></span>

* <span data-ttu-id="001bd-114">Nasıl tooinstall Git ve Node.js.</span><span class="sxs-lookup"><span data-stu-id="001bd-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="001bd-115">[Git](https://git-scm.com) bir açık kaynak dağıtılmış sürüm denetim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="001bd-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="001bd-116">Bu makale için Merhaba örnek uygulaması Git üzerinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="001bd-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="001bd-117">[Node.js](https://nodejs.org/en/) JavaScript çalışma zamanı zengin paket ekosistemi ile.</span><span class="sxs-lookup"><span data-stu-id="001bd-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="001bd-118">Nasıl toouse NPM tooinstall ek Node.js geliştirme araçları.</span><span class="sxs-lookup"><span data-stu-id="001bd-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="001bd-119">Merhaba gerekli en düşük sürümü Node.js 4.5 LTS ' dir.</span><span class="sxs-lookup"><span data-stu-id="001bd-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="001bd-120">[NPM](https://www.npmjs.com) hello Node.js paket yöneticilerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="001bd-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="001bd-121">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="001bd-121">What you need</span></span>
<span data-ttu-id="001bd-122">toocomplete bu işlem, gerekir:</span><span class="sxs-lookup"><span data-stu-id="001bd-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="001bd-123">Bir Internet bağlantısı toodownload geliştirme araçları hello ve yazılım hello.</span><span class="sxs-lookup"><span data-stu-id="001bd-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="001bd-124">MacOS Yosemite (10.10) çalıştıran bir Mac veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="001bd-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="001bd-125">Git ve Node.js yükleyin</span><span class="sxs-lookup"><span data-stu-id="001bd-125">Install Git and Node.js</span></span>
<span data-ttu-id="001bd-126">tooinstall Git ve Node.js kullanın hello [Homebrew](http://brew.sh) paket yönetimi yardımcı programı aşağıdaki adımları izleyerek:</span><span class="sxs-lookup"><span data-stu-id="001bd-126">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="001bd-127">Homebrew yükleyin.</span><span class="sxs-lookup"><span data-stu-id="001bd-127">Install Homebrew.</span></span> <span data-ttu-id="001bd-128">Homebrew zaten yüklediyseniz, toostep 2 gidin.</span><span class="sxs-lookup"><span data-stu-id="001bd-128">If you've already installed Homebrew, go toostep 2.</span></span>
   
   1. <span data-ttu-id="001bd-129">Tuşuna `Cmd + Space` ve girin `Terminal` tooopen bir terminal.</span><span class="sxs-lookup"><span data-stu-id="001bd-129">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="001bd-130">Merhaba aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="001bd-130">Run hello following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="001bd-131">Git ve Node.js hello aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="001bd-131">Install Git and Node.js by running hello following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="001bd-132">Ek Node.js geliştirme araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="001bd-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="001bd-133">Kullanım [gulp.js](http://gulpjs.com) hello örnek uygulama tooyour PI tooautomate hello dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="001bd-133">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Pi.</span></span> <span data-ttu-id="001bd-134">Kullanım hello [aygıt bulma CLI](https://github.com/Azure/device-discovery-cli) IOT aygıtlarınızla ilgili tooretrieve ağ bilgileri.</span><span class="sxs-lookup"><span data-stu-id="001bd-134">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="001bd-135">Yükleme `gulp` ve `device-discovery-cli` komutu hello terminalde aşağıdaki hello çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="001bd-135">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="001bd-136">Node.js ve bu ek geliştirme araçları üzerinde macOS yüklerken sorunlarla karşılaşırsanız, hello bkz [sorun giderme kılavuzu](iot-hub-raspberry-pi-kit-c-troubleshooting.md) çözümleri toocommon sorunları.</span><span class="sxs-lookup"><span data-stu-id="001bd-136">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="001bd-137">Visual Studio Kodu'nu yükle</span><span class="sxs-lookup"><span data-stu-id="001bd-137">Install Visual Studio Code</span></span>
<span data-ttu-id="001bd-138">[Karşıdan](https://code.visualstudio.com/docs/setup/osx) ve Visual Studio Code yükleyin.</span><span class="sxs-lookup"><span data-stu-id="001bd-138">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="001bd-139">Visual Studio Code, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisidir.</span><span class="sxs-lookup"><span data-stu-id="001bd-139">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="001bd-140">Daha sonra hello öğretici tooedit hello örnek kodda bu Düzenleyicisi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="001bd-140">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="001bd-141">Özet</span><span class="sxs-lookup"><span data-stu-id="001bd-141">Summary</span></span>
<span data-ttu-id="001bd-142">Gerekli hello geliştirme araçları ve hello ilk örnek uygulama için yazılım yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="001bd-142">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="001bd-143">Merhaba sonraki toocreate bir görevdir, dağıtmak ve üzerinde Pi hello örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="001bd-143">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="001bd-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="001bd-144">Next steps</span></span>
[<span data-ttu-id="001bd-145">Merhaba blink uygulama oluşturun ve dağıtın</span><span class="sxs-lookup"><span data-stu-id="001bd-145">Create and deploy hello blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

