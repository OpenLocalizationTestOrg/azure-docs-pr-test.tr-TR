---
title: "Raspberry Pi'yi (düğüm) tooAzure IOT - Ders 1 bağlanın: alma araçlarını (Windows) | Microsoft Docs"
description: "İndirin ve Windows 7 ve sonraki sürümlerde hello gerekli araçları ve Merhaba ilk örnek uygulaması pi yazılımı yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IOT geliştirme IOT yazılım, şeyler yazılımların internet windows Git'i yükleyin, çalışma gulp, düğüm js Windows'u yüklemek, windows npm yükleme, Windows'da python yüklemek"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b3d88e17-97cc-4f23-85fd-a688fc228eb8
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ea7f77cc79c70c8c7952b63462b926471fcf71cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="2f1e3-104">(Windows 7 veya üzeri) Hello araçları edinin</span><span class="sxs-lookup"><span data-stu-id="2f1e3-104">Get hello tools (Windows 7 or later)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2f1e3-105">Windows 7 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="2f1e3-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="2f1e3-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="2f1e3-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="2f1e3-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="2f1e3-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a><span data-ttu-id="2f1e3-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="2f1e3-108">What you will do</span></span>
<span data-ttu-id="2f1e3-109">Merhaba geliştirme araçları ve hello ilk örnek bir uygulama için Raspberry Pi 3 hello yazılımı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2f1e3-109">Download hello development tools and hello software for hello first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="2f1e3-110">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="2f1e3-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2f1e3-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="2f1e3-111">What you will learn</span></span>
<span data-ttu-id="2f1e3-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="2f1e3-112">In this article, you will learn:</span></span>

* <span data-ttu-id="2f1e3-113">Nasıl tooinstall Git ve Node.js.</span><span class="sxs-lookup"><span data-stu-id="2f1e3-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="2f1e3-114">[Git](https://git-scm.com) bir açık kaynak dağıtılmış sürüm denetim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="2f1e3-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="2f1e3-115">Bu makale için Merhaba örnek uygulaması Git üzerinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="2f1e3-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="2f1e3-116">[Node.js](https://nodejs.org/en/) JavaScript çalışma zamanı zengin paket ekosistemi ile.</span><span class="sxs-lookup"><span data-stu-id="2f1e3-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="2f1e3-117">Nasıl toouse NPM tooinstall ek Node.js geliştirme araçları.</span><span class="sxs-lookup"><span data-stu-id="2f1e3-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="2f1e3-118">Node.js Hello en düşük sürüm gereksinimini 4.5 LTS ' dir.</span><span class="sxs-lookup"><span data-stu-id="2f1e3-118">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="2f1e3-119">[NPM](https://www.npmjs.com) hello Node.js paket yöneticilerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="2f1e3-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2f1e3-120">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="2f1e3-120">What you need</span></span>
<span data-ttu-id="2f1e3-121">toocomplete bu işlem, gerekir:</span><span class="sxs-lookup"><span data-stu-id="2f1e3-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="2f1e3-122">Bir Internet bağlantısı toodownload geliştirme araçları hello ve yazılım hello.</span><span class="sxs-lookup"><span data-stu-id="2f1e3-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="2f1e3-123">Windows çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="2f1e3-123">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="2f1e3-124">Git ve Node.js yükleyin</span><span class="sxs-lookup"><span data-stu-id="2f1e3-124">Install Git and Node.js</span></span>
<span data-ttu-id="2f1e3-125">Bağlantılar toodownload aşağıdaki hello'ı tıklatın ve Git ve Windows için Node.js LTS yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2f1e3-125">Click hello following links toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="2f1e3-126">Windows için Git Al</span><span class="sxs-lookup"><span data-stu-id="2f1e3-126">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="2f1e3-127">Windows için node.js LTS Al</span><span class="sxs-lookup"><span data-stu-id="2f1e3-127">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="2f1e3-128">Ek Node.js geliştirme araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="2f1e3-128">Install additional Node.js development tools</span></span>
<span data-ttu-id="2f1e3-129">Kullanım [gulp.js](http://gulpjs.com) hello örnek uygulama tooPi tooautomate hello dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="2f1e3-129">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="2f1e3-130">Merhaba de [aygıt bulma CLI](https://github.com/Azure/device-discovery-cli) IOT aygıtlarınızla ilgili tooretrieve ağ bilgileri.</span><span class="sxs-lookup"><span data-stu-id="2f1e3-130">You also use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="2f1e3-131">Bir komut istemini yönetici olarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="2f1e3-131">Start a command prompt as an administrator.</span></span> <span data-ttu-id="2f1e3-132">Yükleme `gulp` ve `device-discovery-cli` hello aşağıdaki komutu çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="2f1e3-132">Install `gulp` and `device-discovery-cli` by running hello following command:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="2f1e3-133">Node.js ve bu ek Node.js geliştirme araçları bilgisayarınızda yüklerken sorunlarla karşılaşırsanız, hello bkz [sorun giderme kılavuzu](iot-hub-raspberry-pi-kit-node-troubleshooting.md) çözümleri toocommon sorunları.</span><span class="sxs-lookup"><span data-stu-id="2f1e3-133">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="2f1e3-134">Visual Studio Kodu'nu yükle</span><span class="sxs-lookup"><span data-stu-id="2f1e3-134">Install Visual Studio Code</span></span>
<span data-ttu-id="2f1e3-135">[Karşıdan](https://code.visualstudio.com/docs/setup/windows) ve Visual Studio Code yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2f1e3-135">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="2f1e3-136">Visual Studio Code, Windows, Linux ve macOS için basit ancak güçlü kaynak kod düzenleyicisidir.</span><span class="sxs-lookup"><span data-stu-id="2f1e3-136">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="2f1e3-137">Daha sonra hello öğretici tooedit hello örnek kodda bu Düzenleyicisi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="2f1e3-137">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="2f1e3-138">Özet</span><span class="sxs-lookup"><span data-stu-id="2f1e3-138">Summary</span></span>
<span data-ttu-id="2f1e3-139">Gerekli hello geliştirme araçları ve hello ilk örnek uygulama için yazılım yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="2f1e3-139">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="2f1e3-140">Merhaba sonraki toocreate bir görevdir, dağıtmak ve üzerinde Pi hello örnek uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2f1e3-140">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f1e3-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2f1e3-141">Next steps</span></span>
[<span data-ttu-id="2f1e3-142">Merhaba blink örnek uygulama oluşturun ve dağıtın</span><span class="sxs-lookup"><span data-stu-id="2f1e3-142">Create and deploy hello blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

