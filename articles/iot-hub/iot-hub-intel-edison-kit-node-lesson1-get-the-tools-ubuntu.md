---
title: "Intel Edison'u (düğüm) tooAzure IOT - Ders 1 bağlanın: Get Araçlar (Ubuntu) | Microsoft Docs"
description: "İndirin ve Ubuntu üzerinde hello gerekli araçları ve hello ilk örnek bir uygulama için Edison'u yazılımı yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino geliştirme araçları, IOT geliştirme, IOT yazılım, Internet şeyler yazılımın, ubuntu, yükleme düğümü js ubuntu üzerinde yükleme git"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 9ab5b161-7ec5-41a6-9c5f-4456e4882752
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ad1a48708bd74bcc07d09f105f597f18c3f9d2b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="6a228-104">Merhaba Araçları (Ubuntu 16.04) alın</span><span class="sxs-lookup"><span data-stu-id="6a228-104">Get hello tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="6a228-105">[Windows 7 veya üzeri][windows]</span><span class="sxs-lookup"><span data-stu-id="6a228-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="6a228-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="6a228-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="6a228-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="6a228-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="6a228-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="6a228-108">What you will do</span></span>
<span data-ttu-id="6a228-109">Merhaba geliştirme araçları ve hello ilk örnek bir uygulama için Intel Edison'u hello yazılımını indirin.</span><span class="sxs-lookup"><span data-stu-id="6a228-109">Download hello development tools and hello software for hello first sample application for your Intel Edison.</span></span> <span data-ttu-id="6a228-110">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="6a228-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="6a228-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="6a228-111">What you will learn</span></span>
<span data-ttu-id="6a228-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="6a228-112">In this article, you will learn:</span></span>

* <span data-ttu-id="6a228-113">Nasıl tooinstall Git ve Node.js</span><span class="sxs-lookup"><span data-stu-id="6a228-113">How tooinstall Git and Node.js</span></span>
  * <span data-ttu-id="6a228-114">[Git](https://git-scm.com) bir açık kaynak dağıtılmış sürüm denetim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="6a228-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="6a228-115">Bu makale için Merhaba örnek uygulaması Git üzerinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="6a228-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="6a228-116">[Node.js](https://nodejs.org/en/) JavaScript çalışma zamanı zengin paket ekosistemi ile.</span><span class="sxs-lookup"><span data-stu-id="6a228-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="6a228-117">Nasıl toouse NPM tooinstall ek Node.js geliştirme araçları.</span><span class="sxs-lookup"><span data-stu-id="6a228-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="6a228-118">Merhaba gerekli en düşük sürümü Node.js 4.5 LTS ' dir.</span><span class="sxs-lookup"><span data-stu-id="6a228-118">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="6a228-119">[NPM](https://www.npmjs.com) hello Node.js paket yöneticilerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="6a228-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6a228-120">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="6a228-120">What you need</span></span>
<span data-ttu-id="6a228-121">toocomplete bu işlem, gerekir:</span><span class="sxs-lookup"><span data-stu-id="6a228-121">toocomplete this operation, you will need:</span></span>
* <span data-ttu-id="6a228-122">Bir Internet bağlantısı toodownload geliştirme araçları hello ve yazılım hello.</span><span class="sxs-lookup"><span data-stu-id="6a228-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="6a228-123">Ubuntu 16.04 veya sonraki sürümünü çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="6a228-123">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="6a228-124">Git, Node.js ve NPM yükleme</span><span class="sxs-lookup"><span data-stu-id="6a228-124">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="6a228-125">Kullanım hello klavye kısayolu `Ctrl + Alt + T` tooopen aşağıdaki terminal ve çalışma hello komutlar:</span><span class="sxs-lookup"><span data-stu-id="6a228-125">Use hello keyboard shortcut `Ctrl + Alt + T` tooopen a terminal and run hello following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="6a228-126">Ek Node.js geliştirme araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="6a228-126">Install additional Node.js development tools</span></span>
<span data-ttu-id="6a228-127">Kullanım [gulp.js](http://gulpjs.com) hello örnek uygulama tooEdison tooautomate hello dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="6a228-127">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooEdison.</span></span>

<span data-ttu-id="6a228-128">Yükleme `gulp` komutu hello terminalde aşağıdaki hello çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="6a228-128">Install `gulp` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="6a228-129">Node.js ve bu ek geliştirme araçları üzerinde Ubuntu yüklerken sorunlarla karşılaşırsanız, hello bkz [sorun giderme kılavuzu] [ troubleshooting] çözümleri toocommon sorunları.</span><span class="sxs-lookup"><span data-stu-id="6a228-129">If you experience issues installing Node.js and these additional development tools on Ubuntu, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="6a228-130">Visual Studio Kodu'nu yükle</span><span class="sxs-lookup"><span data-stu-id="6a228-130">Install Visual Studio Code</span></span>
<span data-ttu-id="6a228-131">[Karşıdan](https://code.visualstudio.com/docs/setup/linux) ve Visual Studio Code yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6a228-131">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="6a228-132">Visual Studio Code, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisidir.</span><span class="sxs-lookup"><span data-stu-id="6a228-132">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="6a228-133">Daha sonra hello öğretici tooedit hello örnek kodda bu Düzenleyicisi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="6a228-133">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="6a228-134">Özet</span><span class="sxs-lookup"><span data-stu-id="6a228-134">Summary</span></span>
<span data-ttu-id="6a228-135">Gerekli hello geliştirme araçları ve hello ilk örnek uygulama için yazılım yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="6a228-135">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="6a228-136">Merhaba sonraki toocreate bir görevdir, dağıtmak ve üzerinde Edison'u hello örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6a228-136">hello next task is toocreate, deploy, and run hello sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a228-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6a228-137">Next steps</span></span>
<span data-ttu-id="6a228-138">[Merhaba blink örnek uygulama oluşturun ve dağıtın][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="6a228-138">[Create and deploy hello blink sample application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
