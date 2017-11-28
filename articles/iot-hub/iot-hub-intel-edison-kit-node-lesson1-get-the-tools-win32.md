---
title: "Azure IOT - Ders 1 Intel Edison'u (düğüm) bağlanma: alma araçlarını (Windows) | Microsoft Docs"
description: "İndirin ve Windows 7 ve sonraki sürümleri gerekli araçları ve Edison'u için ilk örnek uygulama için yazılım yüklemek."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino geliştirme araçları, IOT geliştirme, IOT yazılım, Internet şeyler yazılımın, Windows, düğüm js windows yükleme yükleme git"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 4164b5a1-5a42-4d8a-9ff6-441e79fcc936
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 35b7ae24f8616848eaa6affccb96630603b823b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-or-later"></a><span data-ttu-id="db8e5-104">(Windows 7 veya üzeri) araçları edinin</span><span class="sxs-lookup"><span data-stu-id="db8e5-104">Get the tools (Windows 7 or later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="db8e5-105">[Windows 7 veya üzeri][windows]</span><span class="sxs-lookup"><span data-stu-id="db8e5-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="db8e5-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="db8e5-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="db8e5-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="db8e5-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="db8e5-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="db8e5-108">What you will do</span></span>
<span data-ttu-id="db8e5-109">Geliştirme araçları ve Intel Edison'u için ilk örnek uygulama için yazılım indirin.</span><span class="sxs-lookup"><span data-stu-id="db8e5-109">Download the development tools and the software for the first sample application for Intel Edison.</span></span> <span data-ttu-id="db8e5-110">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="db8e5-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="db8e5-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="db8e5-111">What you will learn</span></span>
<span data-ttu-id="db8e5-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="db8e5-112">In this article, you will learn:</span></span>

* <span data-ttu-id="db8e5-113">Git ve Node.js nasıl yüklenir.</span><span class="sxs-lookup"><span data-stu-id="db8e5-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="db8e5-114">[Git](https://git-scm.com) bir açık kaynak dağıtılmış sürüm denetim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="db8e5-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="db8e5-115">Bu makalede örnek uygulama Git üzerinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="db8e5-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="db8e5-116">[Node.js](https://nodejs.org/en/) JavaScript çalışma zamanı zengin paket ekosistemi ile.</span><span class="sxs-lookup"><span data-stu-id="db8e5-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="db8e5-117">NPM ek Node.js Geliştirme Araçları'nı yüklemek için nasıl kullanılacağını.</span><span class="sxs-lookup"><span data-stu-id="db8e5-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="db8e5-118">Node.js en düşük sürüm gereksinimini 4.5 LTS ' dir.</span><span class="sxs-lookup"><span data-stu-id="db8e5-118">The minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="db8e5-119">[NPM](https://www.npmjs.com) Node.js paket yöneticilerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="db8e5-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="db8e5-120">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="db8e5-120">What you need</span></span>

<span data-ttu-id="db8e5-121">Bu işlemi tamamlamak için gerekir:</span><span class="sxs-lookup"><span data-stu-id="db8e5-121">To complete this operation, you will need:</span></span>

* <span data-ttu-id="db8e5-122">Geliştirme araçları ve yazılım indirmesi için Internet bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="db8e5-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="db8e5-123">Windows çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="db8e5-123">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="db8e5-124">Git ve Node.js yükleyin</span><span class="sxs-lookup"><span data-stu-id="db8e5-124">Install Git and Node.js</span></span>

<span data-ttu-id="db8e5-125">İndirmek ve Git ve Windows için Node.js LTS yüklemek için aşağıdaki bağlantıları tıklatın.</span><span class="sxs-lookup"><span data-stu-id="db8e5-125">Click the links below to download and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="db8e5-126">Windows için Git Al</span><span class="sxs-lookup"><span data-stu-id="db8e5-126">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="db8e5-127">Windows için node.js LTS Al</span><span class="sxs-lookup"><span data-stu-id="db8e5-127">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="db8e5-128">Ek Node.js geliştirme araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="db8e5-128">Install additional Node.js development tools</span></span>

<span data-ttu-id="db8e5-129">Kullanım [gulp.js](http://gulpjs.com) Edison'u için örnek uygulama dağıtımını otomatik hale getirmek için.</span><span class="sxs-lookup"><span data-stu-id="db8e5-129">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Edison.</span></span>

<span data-ttu-id="db8e5-130">Bir komut istemini yönetici olarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="db8e5-130">Start a command prompt as an administrator.</span></span> <span data-ttu-id="db8e5-131">Yükleme `gulp` aşağıdaki komutu çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="db8e5-131">Install `gulp` by running the following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="db8e5-132">Node.js ve bu ek Node.js geliştirme araçları bilgisayarınızda yüklerken sorunlarla karşılaşırsanız bkz [sorun giderme kılavuzu] [ troubleshooting] yaygın sorunların çözümleri için.</span><span class="sxs-lookup"><span data-stu-id="db8e5-132">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="db8e5-133">Visual Studio Kodu'nu yükle</span><span class="sxs-lookup"><span data-stu-id="db8e5-133">Install Visual Studio Code</span></span>

<span data-ttu-id="db8e5-134">[Karşıdan](https://code.visualstudio.com/docs/setup/windows) ve Visual Studio Code yükleyin.</span><span class="sxs-lookup"><span data-stu-id="db8e5-134">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="db8e5-135">Visual Studio Code, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisidir.</span><span class="sxs-lookup"><span data-stu-id="db8e5-135">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="db8e5-136">Örnek kod düzenlemek için öğreticide daha sonra bu Düzenleyicisi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="db8e5-136">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="db8e5-137">Özet</span><span class="sxs-lookup"><span data-stu-id="db8e5-137">Summary</span></span>

<span data-ttu-id="db8e5-138">İlk örnek uygulama için yazılım ve gerekli geliştirme araçları yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="db8e5-138">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="db8e5-139">Sonraki oluşturmak, dağıtmak ve örnek uygulama Edison'u üzerinde çalıştırmak için bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="db8e5-139">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db8e5-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="db8e5-140">Next steps</span></span>

<span data-ttu-id="db8e5-141">[Blink uygulama oluşturun ve dağıtın][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="db8e5-141">[Create and deploy the blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
