---
title: "Arduino tooAzure IOT - Ders 1 bağlanın: Get Araçlar (macOS) | Microsoft Docs"
description: "Karşıdan yükleyip hello gerekli araçları ve yazılım için Adafruit yumuşatma M0 WiFi hello ilk örnek uygulaması macOS üzerinde."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino geliştirme araçları, IOT geliştirme, IOT yazılım, Internet şeyler yazılımın, mac, yükleme düğümü js mac üzerinde yükleme git"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 0262f3dd-0259-4eb0-962f-9fb534f8359e
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5fd306fecd7259fb8f1e99d76282a1e464c4d4f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="bdde6-104">Merhaba Araçları (macOS 10.10) alın</span><span class="sxs-lookup"><span data-stu-id="bdde6-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="bdde6-105">[Windows 7 veya üzeri][windows]</span><span class="sxs-lookup"><span data-stu-id="bdde6-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="bdde6-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="bdde6-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="bdde6-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="bdde6-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="bdde6-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="bdde6-108">What you will do</span></span>

<span data-ttu-id="bdde6-109">Merhaba geliştirme araçları ve hello ilk örnek bir uygulama için Adafruit yumuşatma M0 WiFi Arduino panonuzu hello yazılımını indirin.</span><span class="sxs-lookup"><span data-stu-id="bdde6-109">Download hello development tools and hello software for hello first sample application for your Adafruit Feather M0 WiFi Arduino board.</span></span> 

<span data-ttu-id="bdde6-110">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="bdde6-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="bdde6-111">Programlama dili hello ana mantığı hello Arduino olsa da, Node.js araçları hello dersleri toobuild kullanılır ve örnek uygulamaları dağıtın.</span><span class="sxs-lookup"><span data-stu-id="bdde6-111">Although hello programming language of hello main logic is Arduino, Node.js tools are used in hello lessons toobuild and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="bdde6-112">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="bdde6-112">What you will learn</span></span>
<span data-ttu-id="bdde6-113">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="bdde6-113">In this article, you will learn:</span></span>

* <span data-ttu-id="bdde6-114">Nasıl tooinstall Git ve Node.js.</span><span class="sxs-lookup"><span data-stu-id="bdde6-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="bdde6-115">[Git](https://git-scm.com) bir açık kaynak dağıtılmış sürüm denetim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="bdde6-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="bdde6-116">Bu makale için Merhaba örnek uygulaması Git üzerinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="bdde6-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="bdde6-117">[Node.js](https://nodejs.org/en/) JavaScript çalışma zamanı zengin paket ekosistemi ile.</span><span class="sxs-lookup"><span data-stu-id="bdde6-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="bdde6-118">Nasıl toouse NPM tooinstall ek Node.js geliştirme araçları.</span><span class="sxs-lookup"><span data-stu-id="bdde6-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="bdde6-119">Merhaba gerekli en düşük sürümü Node.js 4.5 LTS ' dir.</span><span class="sxs-lookup"><span data-stu-id="bdde6-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="bdde6-120">[NPM](https://www.npmjs.com) hello Node.js paket yöneticilerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="bdde6-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bdde6-121">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="bdde6-121">What you need</span></span>
<span data-ttu-id="bdde6-122">toocomplete bu işlem, gerekir:</span><span class="sxs-lookup"><span data-stu-id="bdde6-122">toocomplete this operation, you will need:</span></span>
* <span data-ttu-id="bdde6-123">Bir Internet bağlantısı toodownload geliştirme araçları hello ve yazılım hello.</span><span class="sxs-lookup"><span data-stu-id="bdde6-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="bdde6-124">MacOS Yosemite (10.10) çalıştıran bir Mac veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="bdde6-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="bdde6-125">Git ve Node.js yükleyin</span><span class="sxs-lookup"><span data-stu-id="bdde6-125">Install Git and Node.js</span></span>
<span data-ttu-id="bdde6-126">tooinstall Git ve Node.js kullanın hello [Homebrew](http://brew.sh) paket yönetimi yardımcı programı aşağıdaki adımları izleyerek:</span><span class="sxs-lookup"><span data-stu-id="bdde6-126">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="bdde6-127">Homebrew yükleyin.</span><span class="sxs-lookup"><span data-stu-id="bdde6-127">Install Homebrew.</span></span> <span data-ttu-id="bdde6-128">Homebrew zaten yüklediyseniz, toostep 2 gidin.</span><span class="sxs-lookup"><span data-stu-id="bdde6-128">If you've already installed Homebrew, go toostep 2.</span></span>

   1. <span data-ttu-id="bdde6-129">Tuşuna `Cmd + Space` ve girin `Terminal` tooopen bir terminal.</span><span class="sxs-lookup"><span data-stu-id="bdde6-129">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="bdde6-130">Merhaba aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="bdde6-130">Run hello following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="bdde6-131">Git ve Node.js hello aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="bdde6-131">Install Git and Node.js by running hello following command:</span></span>

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="bdde6-132">Ek Node.js geliştirme araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="bdde6-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="bdde6-133">Kullanım [gulp.js](http://gulpjs.com) hello örnek uygulama tooyour Arduino Panosu tooautomate hello dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="bdde6-133">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Arduino board.</span></span>

<span data-ttu-id="bdde6-134">Yükleme `gulp`, `device-discovery-cli` komutu hello terminalde aşağıdaki hello çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="bdde6-134">Install `gulp`, `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp device-discovery-cli
```

<span data-ttu-id="bdde6-135">Node.js ve bu ek geliştirme araçları üzerinde macOS yüklerken sorunlarla karşılaşırsanız, hello bkz [sorun giderme kılavuzu] [ troubleshooting] çözümleri toocommon sorunları.</span><span class="sxs-lookup"><span data-stu-id="bdde6-135">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="bdde6-136">Visual Studio Kodu'nu yükle</span><span class="sxs-lookup"><span data-stu-id="bdde6-136">Install Visual Studio Code</span></span>
<span data-ttu-id="bdde6-137">[Karşıdan](https://code.visualstudio.com/docs/setup/osx) ve Visual Studio Code yükleyin.</span><span class="sxs-lookup"><span data-stu-id="bdde6-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="bdde6-138">Visual Studio Code, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisidir.</span><span class="sxs-lookup"><span data-stu-id="bdde6-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="bdde6-139">Daha sonra hello öğretici tooedit hello örnek kodda bu Düzenleyicisi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="bdde6-139">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="bdde6-140">Özet</span><span class="sxs-lookup"><span data-stu-id="bdde6-140">Summary</span></span>
<span data-ttu-id="bdde6-141">Gerekli hello geliştirme araçları ve hello ilk örnek uygulama için yazılım yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="bdde6-141">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="bdde6-142">Merhaba sonraki toocreate bir görevdir, dağıtmak ve Arduino Panonuzda hello örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bdde6-142">hello next task is toocreate, deploy, and run hello sample application on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bdde6-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bdde6-143">Next steps</span></span>
<span data-ttu-id="bdde6-144">[Merhaba blink uygulama oluşturun ve dağıtın][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="bdde6-144">[Create and deploy hello blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md