---
title: "Azure IOT - Ders 1 Connect Intel Edison (C): Get Araçlar (Ubuntu) | Microsoft Docs"
description: "Karşıdan yükle ve gerekli araçları ve Edison'u için ilk örnek uygulama için yazılım üzerinde Ubuntu yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino geliştirme araçları, IOT geliştirme, IOT yazılım, Internet şeyler yazılımın, ubuntu, yükleme düğümü js ubuntu üzerinde yükleme git"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 4c7b8e04-b892-459b-8b03-85bcaff2465c
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: e929a1cb38f1bacca833e86878c13f20e02885ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="019f4-104">Araçları edinme (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="019f4-104">Get the tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="019f4-105">[Windows 7 veya üzeri][windows]</span><span class="sxs-lookup"><span data-stu-id="019f4-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="019f4-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="019f4-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="019f4-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="019f4-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="019f4-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="019f4-108">What you will do</span></span>
<span data-ttu-id="019f4-109">Geliştirme araçları ve Intel Edison'u için ilk örnek uygulama için yazılım indirin.</span><span class="sxs-lookup"><span data-stu-id="019f4-109">Download the development tools and the software for the first sample application for your Intel Edison.</span></span> <span data-ttu-id="019f4-110">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="019f4-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="019f4-111">Asıl mantığı programlama dili C olsa da, Node.js araçları dersleri örnek uygulamaları geliştirmek ve dağıtmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="019f4-111">Although the programming language of the main logic is C, Node.js tools are used in the lessons to build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="019f4-112">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="019f4-112">What you will learn</span></span>
<span data-ttu-id="019f4-113">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="019f4-113">In this article, you will learn:</span></span>

* <span data-ttu-id="019f4-114">Git ve Node.js nasıl yüklenir</span><span class="sxs-lookup"><span data-stu-id="019f4-114">How to install Git and Node.js</span></span>
  * <span data-ttu-id="019f4-115">[Git](https://git-scm.com) bir açık kaynak dağıtılmış sürüm denetim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="019f4-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="019f4-116">Bu makalede örnek uygulama Git üzerinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="019f4-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="019f4-117">[Node.js](https://nodejs.org/en/) JavaScript çalışma zamanı zengin paket ekosistemi ile.</span><span class="sxs-lookup"><span data-stu-id="019f4-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="019f4-118">NPM ek Node.js Geliştirme Araçları'nı yüklemek için nasıl kullanılacağını.</span><span class="sxs-lookup"><span data-stu-id="019f4-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="019f4-119">Node.js, gerekli en düşük sürüm 4.5 LTS ' dir.</span><span class="sxs-lookup"><span data-stu-id="019f4-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="019f4-120">[NPM](https://www.npmjs.com) Node.js paket yöneticilerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="019f4-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="019f4-121">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="019f4-121">What you need</span></span>
<span data-ttu-id="019f4-122">Bu işlemi tamamlamak için gerekir:</span><span class="sxs-lookup"><span data-stu-id="019f4-122">To complete this operation, you will need:</span></span>
* <span data-ttu-id="019f4-123">Geliştirme araçları ve yazılım indirmesi için Internet bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="019f4-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="019f4-124">Ubuntu 16.04 veya sonraki sürümünü çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="019f4-124">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="019f4-125">Git, Node.js ve NPM yükleme</span><span class="sxs-lookup"><span data-stu-id="019f4-125">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="019f4-126">Klavye kısayolunu kullanın `Ctrl + Alt + T` bir Terminali açın ve aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="019f4-126">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="019f4-127">Ek Node.js geliştirme araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="019f4-127">Install additional Node.js development tools</span></span>
<span data-ttu-id="019f4-128">Kullanım [gulp.js](http://gulpjs.com) Edison'u için örnek uygulama dağıtımını otomatik hale getirmek için.</span><span class="sxs-lookup"><span data-stu-id="019f4-128">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Edison.</span></span>

<span data-ttu-id="019f4-129">Yükleme `gulp` terminale aşağıdaki komutu çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="019f4-129">Install `gulp` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="019f4-130">Node.js ve bu ek geliştirme araçları üzerinde Ubuntu yüklerken sorunlarla karşılaşırsanız bkz [sorun giderme kılavuzu] [ troubleshooting] yaygın sorunların çözümleri için.</span><span class="sxs-lookup"><span data-stu-id="019f4-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="019f4-131">Visual Studio Kodu'nu yükle</span><span class="sxs-lookup"><span data-stu-id="019f4-131">Install Visual Studio Code</span></span>
<span data-ttu-id="019f4-132">[Karşıdan](https://code.visualstudio.com/docs/setup/linux) ve Visual Studio Code yükleyin.</span><span class="sxs-lookup"><span data-stu-id="019f4-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="019f4-133">Visual Studio Code, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisidir.</span><span class="sxs-lookup"><span data-stu-id="019f4-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="019f4-134">Örnek kod düzenlemek için öğreticide daha sonra bu Düzenleyicisi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="019f4-134">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="019f4-135">Özet</span><span class="sxs-lookup"><span data-stu-id="019f4-135">Summary</span></span>
<span data-ttu-id="019f4-136">İlk örnek uygulama için yazılım ve gerekli geliştirme araçları yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="019f4-136">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="019f4-137">Sonraki oluşturmak, dağıtmak ve örnek uygulama Edison'u üzerinde çalıştırmak için bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="019f4-137">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="019f4-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="019f4-138">Next steps</span></span>
<span data-ttu-id="019f4-139">[Blink örnek uygulama oluşturun ve dağıtın][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="019f4-139">[Create and deploy the blink sample application][create-and-deploy-the-blink-application]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-c-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-mac.md
