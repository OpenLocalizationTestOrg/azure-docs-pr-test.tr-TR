---
title: "Raspberry Pi'yi (düğüm) tooAzure IOT - Ders 1 bağlanın: Get Araçlar (Ubuntu) | Microsoft Docs"
description: "İndirin ve Ubuntu üzerinde hello gerekli araçları ve Merhaba ilk örnek uygulaması pi yazılımı yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IOT geliştirme IOT yazılım, şeyler yazılımların internet üzerinde ubuntu Git'i yükleyin, çalışma gulp, düğüm js ubuntu yükleyin"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 4d5e45c0-1db9-4662-a039-99ba26333085
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b4f566fa0d1faf8b2321707145f675e3d87f0bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="a1e7b-104">Merhaba Araçları (Ubuntu 16.04) alın</span><span class="sxs-lookup"><span data-stu-id="a1e7b-104">Get hello tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a1e7b-105">Windows 7 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="a1e7b-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="a1e7b-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="a1e7b-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="a1e7b-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="a1e7b-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a><span data-ttu-id="a1e7b-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="a1e7b-108">What you will do</span></span>
<span data-ttu-id="a1e7b-109">Merhaba geliştirme araçları ve hello ilk örnek bir uygulama için Raspberry Pi 3 hello yazılımı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a1e7b-109">Download hello development tools and hello software for hello first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="a1e7b-110">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="a1e7b-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a1e7b-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="a1e7b-111">What you will learn</span></span>
<span data-ttu-id="a1e7b-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="a1e7b-112">In this article, you will learn:</span></span>

* <span data-ttu-id="a1e7b-113">Nasıl tooinstall Git ve Node.js.</span><span class="sxs-lookup"><span data-stu-id="a1e7b-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="a1e7b-114">[Git](https://git-scm.com) bir açık kaynak dağıtılmış sürüm denetim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="a1e7b-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="a1e7b-115">Bu makale için Merhaba örnek uygulaması Git üzerinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="a1e7b-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="a1e7b-116">[Node.js](https://nodejs.org/en/) JavaScript çalışma zamanı zengin paket ekosistemi ile.</span><span class="sxs-lookup"><span data-stu-id="a1e7b-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="a1e7b-117">Nasıl toouse NPM tooinstall ek Node.js geliştirme araçları.</span><span class="sxs-lookup"><span data-stu-id="a1e7b-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="a1e7b-118">Merhaba gerekli en düşük sürümü Node.js 4.5 LTS ' dir.</span><span class="sxs-lookup"><span data-stu-id="a1e7b-118">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="a1e7b-119">[NPM](https://www.npmjs.com) hello Node.js paket yöneticilerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="a1e7b-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="a1e7b-120">Ne ihtiyacınız var</span><span class="sxs-lookup"><span data-stu-id="a1e7b-120">What do you need</span></span>
<span data-ttu-id="a1e7b-121">toocomplete bu işlem, gerekir:</span><span class="sxs-lookup"><span data-stu-id="a1e7b-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="a1e7b-122">Bir Internet bağlantısı toodownload geliştirme araçları hello ve yazılım hello.</span><span class="sxs-lookup"><span data-stu-id="a1e7b-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="a1e7b-123">Ubuntu 16.04 veya sonraki sürümünü çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="a1e7b-123">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="a1e7b-124">Git, Node.js ve NPM yükleme</span><span class="sxs-lookup"><span data-stu-id="a1e7b-124">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="a1e7b-125">Kullanım hello klavye kısayolu `Ctrl + Alt + T` tooopen aşağıdaki terminal ve çalışma hello komutlar:</span><span class="sxs-lookup"><span data-stu-id="a1e7b-125">Use hello keyboard shortcut `Ctrl + Alt + T` tooopen a terminal and run hello following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="a1e7b-126">Ek Node.js geliştirme araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="a1e7b-126">Install additional Node.js development tools</span></span>
<span data-ttu-id="a1e7b-127">Kullandığınız [gulp.js](http://gulpjs.com) hello örnek uygulama tooPi tooautomate hello dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="a1e7b-127">You use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="a1e7b-128">Merhaba de [aygıt bulma CLI](https://github.com/Azure/device-discovery-cli) IOT aygıtlarınızla ilgili tooretrieve ağ bilgileri.</span><span class="sxs-lookup"><span data-stu-id="a1e7b-128">You also use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="a1e7b-129">Yükleme `gulp` ve `device-discovery-cli` komutu hello terminalde aşağıdaki hello çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="a1e7b-129">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="a1e7b-130">Node.js ve bu ek geliştirme araçları üzerinde Ubuntu yüklerken sorunlarla karşılaşırsanız, hello bkz [sorun giderme kılavuzu](iot-hub-raspberry-pi-kit-node-troubleshooting.md) çözümleri toocommon sorunları.</span><span class="sxs-lookup"><span data-stu-id="a1e7b-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="a1e7b-131">Visual Studio Kodu'nu yükle</span><span class="sxs-lookup"><span data-stu-id="a1e7b-131">Install Visual Studio Code</span></span>
<span data-ttu-id="a1e7b-132">[Karşıdan](https://code.visualstudio.com/docs/setup/linux) ve Visual Studio Code yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a1e7b-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="a1e7b-133">Visual Studio Code, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisidir.</span><span class="sxs-lookup"><span data-stu-id="a1e7b-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="a1e7b-134">Daha sonra hello öğretici tooedit hello örnek kodda bu Düzenleyicisi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="a1e7b-134">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="a1e7b-135">Özet</span><span class="sxs-lookup"><span data-stu-id="a1e7b-135">Summary</span></span>
<span data-ttu-id="a1e7b-136">Gerekli hello geliştirme araçları ve hello ilk örnek uygulama için yazılım yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="a1e7b-136">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="a1e7b-137">Merhaba sonraki toocreate bir görevdir, dağıtmak ve üzerinde Pi hello örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a1e7b-137">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1e7b-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a1e7b-138">Next steps</span></span>
[<span data-ttu-id="a1e7b-139">Merhaba blink örnek uygulama oluşturun ve dağıtın</span><span class="sxs-lookup"><span data-stu-id="a1e7b-139">Create and deploy hello blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

