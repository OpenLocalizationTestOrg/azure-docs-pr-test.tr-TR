---
title: "Connect Raspberry pi (C) tooAzure IOT - Ders 1: alma araçlarını (Windows) | Microsoft Docs"
description: "İndirin ve Windows 7 ve sonraki sürümlerde hello gerekli araçları ve Merhaba ilk örnek uygulaması pi yazılımı yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IOT geliştirme IOT yazılım, Internet şeyler yazılımların windows Git'i yükleyin, düğüm js Windows'u yüklemek, windows npm yükleme"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: bd765ddd-65b7-4241-a391-dc77cb3af1c0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 70ae6d15f9d6af116ff065a79a30d99afc67bffd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="27c15-104">(Windows 7 veya üzeri) Hello araçları edinin</span><span class="sxs-lookup"><span data-stu-id="27c15-104">Get hello tools (Windows 7 or later)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="27c15-105">Windows 7 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="27c15-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="27c15-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="27c15-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="27c15-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="27c15-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="27c15-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="27c15-108">What you will do</span></span>
<span data-ttu-id="27c15-109">Merhaba geliştirme araçları ve hello ilk örnek bir uygulama için Raspberry Pi 3 hello yazılımı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="27c15-109">Download hello development tools and hello software for hello first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="27c15-110">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="27c15-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="27c15-111">Programlama dili hello ana mantığı hello C olsa da, Node.js araçları hello dersleri toodiscover cihazları kullanılır ve yapı ve örnek uygulamaları dağıtın.</span><span class="sxs-lookup"><span data-stu-id="27c15-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toodiscover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="27c15-112">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="27c15-112">What you will learn</span></span>
<span data-ttu-id="27c15-113">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="27c15-113">In this article, you will learn:</span></span>

* <span data-ttu-id="27c15-114">Nasıl tooinstall Git ve Node.js.</span><span class="sxs-lookup"><span data-stu-id="27c15-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="27c15-115">[Git](https://git-scm.com) bir açık kaynak dağıtılmış sürüm denetim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="27c15-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="27c15-116">Bu makale için Merhaba örnek uygulaması Git üzerinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="27c15-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="27c15-117">[Node.js](https://nodejs.org/en/) JavaScript çalışma zamanı zengin paket ekosistemi ile.</span><span class="sxs-lookup"><span data-stu-id="27c15-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="27c15-118">Nasıl toouse NPM tooinstall ek Node.js geliştirme araçları.</span><span class="sxs-lookup"><span data-stu-id="27c15-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="27c15-119">Node.js Hello en düşük sürüm gereksinimini 4.5 LTS ' dir.</span><span class="sxs-lookup"><span data-stu-id="27c15-119">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="27c15-120">[NPM](https://www.npmjs.com) hello Node.js paket yöneticilerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="27c15-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="27c15-121">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="27c15-121">What you need</span></span>

<span data-ttu-id="27c15-122">toocomplete bu işlem, gerekir:</span><span class="sxs-lookup"><span data-stu-id="27c15-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="27c15-123">Bir Internet bağlantısı toodownload geliştirme araçları hello ve yazılım hello.</span><span class="sxs-lookup"><span data-stu-id="27c15-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="27c15-124">Windows çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="27c15-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="27c15-125">Git ve Node.js yükleyin</span><span class="sxs-lookup"><span data-stu-id="27c15-125">Install Git and Node.js</span></span>

<span data-ttu-id="27c15-126">Toodownload aşağıda Hello Bağlantılar'ı tıklatın ve Git ve Windows için Node.js LTS yükleyin.</span><span class="sxs-lookup"><span data-stu-id="27c15-126">Click hello links below toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="27c15-127">Windows için Git Al</span><span class="sxs-lookup"><span data-stu-id="27c15-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="27c15-128">Windows için node.js LTS Al</span><span class="sxs-lookup"><span data-stu-id="27c15-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="27c15-129">Ek Node.js geliştirme araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="27c15-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="27c15-130">Kullanım [gulp.js](http://gulpjs.com) hello örnek uygulama tooPi tooautomate hello dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="27c15-130">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="27c15-131">Kullanım hello [aygıt bulma CLI](https://github.com/Azure/device-discovery-cli) IOT aygıtlarınızla ilgili tooretrieve ağ bilgileri.</span><span class="sxs-lookup"><span data-stu-id="27c15-131">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="27c15-132">Bir komut istemini yönetici olarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="27c15-132">Start a command prompt as an administrator.</span></span> <span data-ttu-id="27c15-133">Yükleme `gulp` ve `device-discovery-cli` hello aşağıdaki komutu çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="27c15-133">Install `gulp` and `device-discovery-cli` by running hello following command:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="27c15-134">Node.js ve bu ek Node.js geliştirme araçları bilgisayarınızda yüklerken sorunlarla karşılaşırsanız, hello bkz [sorun giderme kılavuzu](iot-hub-raspberry-pi-kit-c-troubleshooting.md) çözümleri toocommon sorunları.</span><span class="sxs-lookup"><span data-stu-id="27c15-134">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="27c15-135">Visual Studio Kodu'nu yükle</span><span class="sxs-lookup"><span data-stu-id="27c15-135">Install Visual Studio Code</span></span>

<span data-ttu-id="27c15-136">[Karşıdan](https://code.visualstudio.com/docs/setup/windows) ve Visual Studio Code yükleyin.</span><span class="sxs-lookup"><span data-stu-id="27c15-136">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="27c15-137">Visual Studio Code, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisidir.</span><span class="sxs-lookup"><span data-stu-id="27c15-137">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="27c15-138">Daha sonra hello öğretici tooedit hello örnek kodda bu Düzenleyicisi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="27c15-138">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="27c15-139">Özet</span><span class="sxs-lookup"><span data-stu-id="27c15-139">Summary</span></span>

<span data-ttu-id="27c15-140">Gerekli hello geliştirme araçları ve hello ilk örnek uygulama için yazılım yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="27c15-140">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="27c15-141">Merhaba sonraki toocreate bir görevdir, dağıtmak ve üzerinde Pi hello örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="27c15-141">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="27c15-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="27c15-142">Next steps</span></span>

[<span data-ttu-id="27c15-143">Merhaba blink uygulama oluşturun ve dağıtın</span><span class="sxs-lookup"><span data-stu-id="27c15-143">Create and deploy hello blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)
