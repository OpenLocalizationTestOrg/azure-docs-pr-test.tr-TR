---
title: "Azure IOT - Ders 1 Connect Raspberry pi (C): Get Araçlar (macOS) | Microsoft Docs"
description: "Karşıdan yükle ve gerekli araçları ve pi ilk örnek uygulama için yazılım üzerinde macOS yükleyin."
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
ms.openlocfilehash: 64db77040ef3482f213bd622320fdb5df243fa93
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="66887-104">Araçları edinme (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="66887-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="66887-105">Windows 7 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="66887-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="66887-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="66887-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="66887-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="66887-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="66887-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="66887-108">What you will do</span></span>
<span data-ttu-id="66887-109">Geliştirme araçları ve ilk uygulama Raspberry Pi 3 için yazılımı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="66887-109">Download the development tools and the software for the first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="66887-110">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="66887-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="66887-111">Asıl mantığı programlama dili C olsa da, Node.js araçları dersleri aygıtları bulmak ve yapı ve örnek uygulamaları dağıtmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="66887-111">Although the programming language of the main logic is C, Node.js tools are used in the lessons to discover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="66887-112">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="66887-112">What you will learn</span></span>
<span data-ttu-id="66887-113">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="66887-113">In this article, you will learn:</span></span>

* <span data-ttu-id="66887-114">Git ve Node.js nasıl yüklenir.</span><span class="sxs-lookup"><span data-stu-id="66887-114">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="66887-115">[Git](https://git-scm.com) bir açık kaynak dağıtılmış sürüm denetim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="66887-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="66887-116">Bu makalede örnek uygulama Git üzerinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="66887-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="66887-117">[Node.js](https://nodejs.org/en/) JavaScript çalışma zamanı zengin paket ekosistemi ile.</span><span class="sxs-lookup"><span data-stu-id="66887-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="66887-118">NPM ek Node.js Geliştirme Araçları'nı yüklemek için nasıl kullanılacağını.</span><span class="sxs-lookup"><span data-stu-id="66887-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="66887-119">Node.js, gerekli en düşük sürüm 4.5 LTS ' dir.</span><span class="sxs-lookup"><span data-stu-id="66887-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="66887-120">[NPM](https://www.npmjs.com) Node.js paket yöneticilerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="66887-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="66887-121">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="66887-121">What you need</span></span>
<span data-ttu-id="66887-122">Bu işlemi tamamlamak için gerekir:</span><span class="sxs-lookup"><span data-stu-id="66887-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="66887-123">Geliştirme araçları ve yazılım indirmesi için Internet bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="66887-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="66887-124">MacOS Yosemite (10.10) çalıştıran bir Mac veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="66887-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="66887-125">Git ve Node.js yükleyin</span><span class="sxs-lookup"><span data-stu-id="66887-125">Install Git and Node.js</span></span>
<span data-ttu-id="66887-126">Git ve Node.js yüklemek için kullandığınız [Homebrew](http://brew.sh) paket yönetimi yardımcı programı aşağıdaki adımları izleyerek:</span><span class="sxs-lookup"><span data-stu-id="66887-126">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="66887-127">Homebrew yükleyin.</span><span class="sxs-lookup"><span data-stu-id="66887-127">Install Homebrew.</span></span> <span data-ttu-id="66887-128">Homebrew zaten yüklediyseniz, 2. adıma geçin.</span><span class="sxs-lookup"><span data-stu-id="66887-128">If you've already installed Homebrew, go to step 2.</span></span>
   
   1. <span data-ttu-id="66887-129">Tuşuna `Cmd + Space` ve girin `Terminal` bir Terminali açın.</span><span class="sxs-lookup"><span data-stu-id="66887-129">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="66887-130">Şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="66887-130">Run the following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="66887-131">Git ve Node.js aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="66887-131">Install Git and Node.js by running the following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="66887-132">Ek Node.js geliştirme araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="66887-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="66887-133">Kullanım [gulp.js](http://gulpjs.com) , Pi örnek uygulamaya dağıtımını otomatik hale getirmek için.</span><span class="sxs-lookup"><span data-stu-id="66887-133">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Pi.</span></span> <span data-ttu-id="66887-134">Kullanım [aygıt bulma CLI](https://github.com/Azure/device-discovery-cli) IOT aygıtlarınızla ilgili ağ bilgileri alınamadı.</span><span class="sxs-lookup"><span data-stu-id="66887-134">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="66887-135">Yükleme `gulp` ve `device-discovery-cli` terminale aşağıdaki komutu çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="66887-135">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="66887-136">Node.js ve bu ek geliştirme araçları üzerinde macOS yüklerken sorunlarla karşılaşırsanız bkz [sorun giderme kılavuzu](iot-hub-raspberry-pi-kit-c-troubleshooting.md) yaygın sorunların çözümleri için.</span><span class="sxs-lookup"><span data-stu-id="66887-136">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="66887-137">Visual Studio Kodu'nu yükle</span><span class="sxs-lookup"><span data-stu-id="66887-137">Install Visual Studio Code</span></span>
<span data-ttu-id="66887-138">[Karşıdan](https://code.visualstudio.com/docs/setup/osx) ve Visual Studio Code yükleyin.</span><span class="sxs-lookup"><span data-stu-id="66887-138">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="66887-139">Visual Studio Code, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisidir.</span><span class="sxs-lookup"><span data-stu-id="66887-139">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="66887-140">Örnek kod düzenlemek için öğreticide daha sonra bu Düzenleyicisi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="66887-140">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="66887-141">Özet</span><span class="sxs-lookup"><span data-stu-id="66887-141">Summary</span></span>
<span data-ttu-id="66887-142">İlk örnek uygulama için yazılım ve gerekli geliştirme araçları yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="66887-142">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="66887-143">Sonraki oluşturmak, dağıtmak ve örnek uygulama Pi üzerinde çalıştırmak için bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="66887-143">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66887-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="66887-144">Next steps</span></span>
[<span data-ttu-id="66887-145">Blink uygulaması oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="66887-145">Create and deploy the blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

