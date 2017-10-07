---
title: "Arduino tooAzure IOT - Ders 1 bağlanın: alma araçlarını (Windows) | Microsoft Docs"
description: "İndirin ve Windows 7 ve sonraki sürümlerde hello gerekli araçları ve hello ilk örnek bir uygulama için Adafruit yumuşatma M0 WiFi yazılımı yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino geliştirme araçları, IOT geliştirme, IOT yazılım, Internet şeyler yazılımın, Windows, düğüm js windows yükleme yükleme git"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9cfb8cd2-eafb-4ba2-b23e-d94e114ff3a6
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4dd946da6c84293987e166fd1d17fac117e94e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="2b631-104">(Windows 7 veya üzeri) Hello araçları edinin</span><span class="sxs-lookup"><span data-stu-id="2b631-104">Get hello tools (Windows 7 or later)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="2b631-105">[Windows 7 veya üzeri][windows]</span><span class="sxs-lookup"><span data-stu-id="2b631-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="2b631-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="2b631-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="2b631-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="2b631-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="2b631-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="2b631-108">What you will do</span></span>

<span data-ttu-id="2b631-109">Merhaba geliştirme araçları ve hello ilk örnek bir uygulama için Adafruit yumuşatma M0 WiFi Arduino panonuzu hello yazılımını indirin.</span><span class="sxs-lookup"><span data-stu-id="2b631-109">Download hello development tools and hello software for hello first sample application for your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="2b631-110">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="2b631-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="2b631-111">Programlama dili hello ana mantığı hello Arduino olsa da, Node.js araçları hello dersleri toobuild kullanılır ve örnek uygulamaları dağıtın.</span><span class="sxs-lookup"><span data-stu-id="2b631-111">Although hello programming language of hello main logic is Arduino, Node.js tools are used in hello lessons toobuild and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2b631-112">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="2b631-112">What you will learn</span></span>
<span data-ttu-id="2b631-113">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="2b631-113">In this article, you will learn:</span></span>

* <span data-ttu-id="2b631-114">Nasıl tooinstall Git ve Node.js.</span><span class="sxs-lookup"><span data-stu-id="2b631-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="2b631-115">[Git](https://git-scm.com) bir açık kaynak dağıtılmış sürüm denetim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="2b631-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="2b631-116">Bu makale için Merhaba örnek uygulaması Git üzerinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="2b631-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="2b631-117">[Node.js](https://nodejs.org/en/) JavaScript çalışma zamanı zengin paket ekosistemi ile.</span><span class="sxs-lookup"><span data-stu-id="2b631-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="2b631-118">Nasıl toouse NPM tooinstall ek Node.js geliştirme araçları.</span><span class="sxs-lookup"><span data-stu-id="2b631-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="2b631-119">Node.js Hello en düşük sürüm gereksinimini 4.5 LTS ' dir.</span><span class="sxs-lookup"><span data-stu-id="2b631-119">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="2b631-120">[NPM](https://www.npmjs.com) hello Node.js paket yöneticilerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="2b631-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2b631-121">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="2b631-121">What you need</span></span>

<span data-ttu-id="2b631-122">toocomplete bu işlem, gerekir:</span><span class="sxs-lookup"><span data-stu-id="2b631-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="2b631-123">Bir Internet bağlantısı toodownload geliştirme araçları hello ve yazılım hello.</span><span class="sxs-lookup"><span data-stu-id="2b631-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="2b631-124">Windows çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="2b631-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="2b631-125">Git ve Node.js yükleyin</span><span class="sxs-lookup"><span data-stu-id="2b631-125">Install Git and Node.js</span></span>

<span data-ttu-id="2b631-126">Toodownload aşağıda Hello Bağlantılar'ı tıklatın ve Git ve Windows için Node.js LTS yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2b631-126">Click hello links below toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="2b631-127">Windows için Git Al</span><span class="sxs-lookup"><span data-stu-id="2b631-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="2b631-128">Windows için node.js LTS Al</span><span class="sxs-lookup"><span data-stu-id="2b631-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="2b631-129">Ek Node.js geliştirme araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="2b631-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="2b631-130">Kullanım [gulp.js](http://gulpjs.com) hello örnek uygulama tooyour Arduino Panosu tooautomate hello dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="2b631-130">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Arduino board.</span></span>

<span data-ttu-id="2b631-131">Bir komut istemini yönetici olarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="2b631-131">Start a command prompt as an administrator.</span></span> <span data-ttu-id="2b631-132">Yükleme `gulp`, `device-discovery-cli` komutu hello terminalde aşağıdaki hello çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="2b631-132">Install `gulp`, `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
npm install -g gulp device-discovery-cli
```

<span data-ttu-id="2b631-133">Node.js ve bu ek Node.js geliştirme araçları bilgisayarınızda yüklerken sorunlarla karşılaşırsanız, hello bkz [sorun giderme kılavuzu] [ troubleshooting] çözümleri toocommon sorunları.</span><span class="sxs-lookup"><span data-stu-id="2b631-133">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="2b631-134">Visual Studio Kodu'nu yükle</span><span class="sxs-lookup"><span data-stu-id="2b631-134">Install Visual Studio Code</span></span>

<span data-ttu-id="2b631-135">[Karşıdan](https://code.visualstudio.com/docs/setup/windows) ve Visual Studio Code yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2b631-135">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="2b631-136">Visual Studio Code, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisidir.</span><span class="sxs-lookup"><span data-stu-id="2b631-136">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="2b631-137">Daha sonra hello öğretici tooedit hello örnek kodda bu Düzenleyicisi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="2b631-137">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="2b631-138">Özet</span><span class="sxs-lookup"><span data-stu-id="2b631-138">Summary</span></span>

<span data-ttu-id="2b631-139">Gerekli hello geliştirme araçları ve hello ilk örnek uygulama için yazılım yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="2b631-139">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="2b631-140">Merhaba sonraki toocreate bir görevdir, dağıtmak ve Arduino Panonuzda hello örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2b631-140">hello next task is toocreate, deploy, and run hello sample application on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b631-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2b631-141">Next steps</span></span>

<span data-ttu-id="2b631-142">[Merhaba blink örnek uygulama oluşturun ve dağıtın][create-and-deploy-the-blink-sample-application]</span><span class="sxs-lookup"><span data-stu-id="2b631-142">[Create and deploy hello blink sample application][create-and-deploy-the-blink-sample-application]</span></span>
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-sample-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md