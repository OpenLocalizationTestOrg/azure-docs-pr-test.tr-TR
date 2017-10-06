---
title: "Arduino tooAzure IOT - Ders 1 bağlanın: Get Araçlar (Ubuntu) | Microsoft Docs"
description: "Karşıdan yükleyip hello gerekli araçları ve yazılım için Adafruit yumuşatma M0 WiFi hello ilk örnek uygulaması Ubuntu üzerinde."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino geliştirme araçları, IOT geliştirme, IOT yazılım, Internet şeyler yazılımın, ubuntu, yükleme düğümü js ubuntu üzerinde yükleme git"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 7572f191-420d-41f0-923b-7ea86c0bfa73
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 586f89025d2fa11a31cb782e3789d306ade018a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="2787d-104">Merhaba Araçları (Ubuntu 16.04) alın</span><span class="sxs-lookup"><span data-stu-id="2787d-104">Get hello tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="2787d-105">[Windows 7 veya üzeri][windows]</span><span class="sxs-lookup"><span data-stu-id="2787d-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="2787d-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="2787d-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="2787d-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="2787d-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="2787d-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="2787d-108">What you will do</span></span>

<span data-ttu-id="2787d-109">Merhaba geliştirme araçları ve hello ilk örnek bir uygulama için Adafruit yumuşatma M0 WiFi Arduino panonuzu hello yazılımını indirin.</span><span class="sxs-lookup"><span data-stu-id="2787d-109">Download hello development tools and hello software for hello first sample application for your Adafruit Feather M0 WiFi Arduino board.</span></span> 

<span data-ttu-id="2787d-110">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="2787d-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="2787d-111">Programlama dili hello ana mantığı hello Arduino olsa da, Node.js araçları hello dersleri toobuild kullanılır ve örnek uygulamaları dağıtın.</span><span class="sxs-lookup"><span data-stu-id="2787d-111">Although hello programming language of hello main logic is Arduino, Node.js tools are used in hello lessons toobuild and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2787d-112">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="2787d-112">What you will learn</span></span>
<span data-ttu-id="2787d-113">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="2787d-113">In this article, you will learn:</span></span>

* <span data-ttu-id="2787d-114">Nasıl tooinstall Git ve Node.js</span><span class="sxs-lookup"><span data-stu-id="2787d-114">How tooinstall Git and Node.js</span></span>
  * <span data-ttu-id="2787d-115">[Git](https://git-scm.com) bir açık kaynak dağıtılmış sürüm denetim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="2787d-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="2787d-116">Bu makale için Merhaba örnek uygulaması Git üzerinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="2787d-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="2787d-117">[Node.js](https://nodejs.org/en/) JavaScript çalışma zamanı zengin paket ekosistemi ile.</span><span class="sxs-lookup"><span data-stu-id="2787d-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="2787d-118">Nasıl toouse NPM tooinstall ek Node.js geliştirme araçları.</span><span class="sxs-lookup"><span data-stu-id="2787d-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="2787d-119">Merhaba gerekli en düşük sürümü Node.js 4.5 LTS ' dir.</span><span class="sxs-lookup"><span data-stu-id="2787d-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="2787d-120">[NPM](https://www.npmjs.com) hello Node.js paket yöneticilerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="2787d-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2787d-121">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="2787d-121">What you need</span></span>
<span data-ttu-id="2787d-122">toocomplete bu işlem, gerekir:</span><span class="sxs-lookup"><span data-stu-id="2787d-122">toocomplete this operation, you will need:</span></span>
* <span data-ttu-id="2787d-123">Bir Internet bağlantısı toodownload geliştirme araçları hello ve yazılım hello.</span><span class="sxs-lookup"><span data-stu-id="2787d-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="2787d-124">Ubuntu 16.04 veya sonraki sürümünü çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="2787d-124">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="2787d-125">Git, Node.js ve NPM yükleme</span><span class="sxs-lookup"><span data-stu-id="2787d-125">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="2787d-126">Kullanım hello klavye kısayolu `Ctrl + Alt + T` tooopen aşağıdaki terminal ve çalışma hello komutlar:</span><span class="sxs-lookup"><span data-stu-id="2787d-126">Use hello keyboard shortcut `Ctrl + Alt + T` tooopen a terminal and run hello following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="2787d-127">Ek Node.js geliştirme araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="2787d-127">Install additional Node.js development tools</span></span>
<span data-ttu-id="2787d-128">Kullanım [gulp.js](http://gulpjs.com) hello örnek uygulama tooyour Arduino Panosu tooautomate hello dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="2787d-128">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Arduino board.</span></span>

<span data-ttu-id="2787d-129">Yükleme `gulp`, `device-discovery-cli` komutu hello terminalde aşağıdaki hello çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="2787d-129">Install `gulp`, `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp device-discovery-cli
```

<span data-ttu-id="2787d-130">Node.js ve bu ek geliştirme araçları üzerinde Ubuntu yüklerken sorunlarla karşılaşırsanız, hello bkz [sorun giderme kılavuzu] [ troubleshooting] çözümleri toocommon sorunları.</span><span class="sxs-lookup"><span data-stu-id="2787d-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="2787d-131">Visual Studio Kodu'nu yükle</span><span class="sxs-lookup"><span data-stu-id="2787d-131">Install Visual Studio Code</span></span>
<span data-ttu-id="2787d-132">[Karşıdan](https://code.visualstudio.com/docs/setup/linux) ve Visual Studio Code yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2787d-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="2787d-133">Visual Studio Code, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisidir.</span><span class="sxs-lookup"><span data-stu-id="2787d-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="2787d-134">Daha sonra hello öğretici tooedit hello örnek kodda bu Düzenleyicisi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="2787d-134">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="2787d-135">Özet</span><span class="sxs-lookup"><span data-stu-id="2787d-135">Summary</span></span>
<span data-ttu-id="2787d-136">Gerekli hello geliştirme araçları ve hello ilk örnek uygulama için yazılım yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="2787d-136">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="2787d-137">Merhaba sonraki toocreate bir görevdir, dağıtmak ve Arduino Panonuzda hello örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2787d-137">hello next task is toocreate, deploy, and run hello sample application on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2787d-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2787d-138">Next steps</span></span>
<span data-ttu-id="2787d-139">[Merhaba blink örnek uygulama oluşturun ve dağıtın][create-and-deploy-the-blink-sample-application]</span><span class="sxs-lookup"><span data-stu-id="2787d-139">[Create and deploy hello blink sample application][create-and-deploy-the-blink-sample-application]</span></span>

<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-sample-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md