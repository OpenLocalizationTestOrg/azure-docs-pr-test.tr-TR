---
title: "aaaAzure kapsayıcı örnekleri Öğreticisi - uygulamanızı hazırlama | Azure belgeleri"
description: "Bir uygulama dağıtım tooAzure kapsayıcı örnekleri için hazırlama"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 406ba796e5fefb1527f2e894cc3f7bbd8f7a5fd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-for-deployment-tooazure-container-instances"></a><span data-ttu-id="0d362-103">Dağıtım tooAzure kapsayıcı örnekleri için kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0d362-103">Create container for deployment tooAzure Container Instances</span></span>

<span data-ttu-id="0d362-104">Azure Container Instances, Docker kapsayıcılarının herhangi bir sanal makine sağlama veya herhangi bir üst düzey hizmet benimsenmesi gerekmeden Azure altyapısına dağıtılmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="0d362-104">Azure Container Instances enables deployment of Docker containers onto Azure infrastructure without provisioning any virtual machines or adopting any higher-level service.</span></span> <span data-ttu-id="0d362-105">Bu öğreticide, Node.js içinde basit bir web uygulaması oluşturacak ve bu uygulamayı Azure Container Instances kullanılarak çalıştırılabilir bir kapsayıcıda paketleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="0d362-105">In this tutorial, you will build a simple web application in Node.js and package it in a container that can be run using Azure Container Instances.</span></span> <span data-ttu-id="0d362-106">Şu konular yer almaktadır:</span><span class="sxs-lookup"><span data-stu-id="0d362-106">We will cover:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0d362-107">GitHub’dan uygulama kaynağını kopyalama</span><span class="sxs-lookup"><span data-stu-id="0d362-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="0d362-108">Uygulama kaynağından kapsayıcı görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="0d362-108">Creating container images from application source</span></span>
> * <span data-ttu-id="0d362-109">Merhaba görüntüleri yerel bir Docker ortamında test etme</span><span class="sxs-lookup"><span data-stu-id="0d362-109">Testing hello images in a local Docker environment</span></span>

<span data-ttu-id="0d362-110">Sonraki öğreticilerde, görüntü tooan Azure kapsayıcı kayıt defteri karşıya yükleyin ve ardından bunları tooAzure kapsayıcı örneği dağıtın.</span><span class="sxs-lookup"><span data-stu-id="0d362-110">In subsequent tutorials, you will upload your image tooan Azure Container Registry, and then deploy them tooAzure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0d362-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="0d362-111">Before you begin</span></span>

<span data-ttu-id="0d362-112">Bu öğreticide kapsayıcılar, kapsayıcı görüntüleri ve temel docker komutları gibi temel Docker kavramları hakkında bilgi sahibi olduğunuz varsayılmıştır.</span><span class="sxs-lookup"><span data-stu-id="0d362-112">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="0d362-113">Gerekirse kapsayıcı temelleri hakkında bilgi için bkz. [Docker ile çalışmaya başlama]( https://docs.docker.com/get-started/).</span><span class="sxs-lookup"><span data-stu-id="0d362-113">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="0d362-114">toocomplete Bu öğreticide, bir Docker geliştirme ortamı gerekir.</span><span class="sxs-lookup"><span data-stu-id="0d362-114">toocomplete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="0d362-115">Docker, [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) veya [Linux](https://docs.docker.com/engine/installation/#supported-platforms)’ta Docker’ı kolayca yapılandırmanızı sağlayan paketler sağlar.</span><span class="sxs-lookup"><span data-stu-id="0d362-115">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="0d362-116">Uygulama kodunu alma</span><span class="sxs-lookup"><span data-stu-id="0d362-116">Get application code</span></span>

<span data-ttu-id="0d362-117">Bu öğreticide Hello örnek içeren yerleşik basit bir web uygulaması [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="0d362-117">hello sample in this tutorial includes a simple web application built in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="0d362-118">Merhaba uygulama bir statik HTML sayfası sunar ve şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="0d362-118">hello app serves a static HTML page and looks like this:</span></span>

![Tarayıcıda gösterilen öğretici uygulama][aci-tutorial-app]

<span data-ttu-id="0d362-120">Git toodownload hello örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="0d362-120">Use git toodownload hello sample:</span></span>

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-hello-container-image"></a><span data-ttu-id="0d362-121">Merhaba kapsayıcı yansıması oluştur</span><span class="sxs-lookup"><span data-stu-id="0d362-121">Build hello container image</span></span>

<span data-ttu-id="0d362-122">Merhaba hello örnek deposuna sağlanan Dockerfile hello kapsayıcı nasıl yapılandırıldığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="0d362-122">hello Dockerfile provided in hello sample repo shows how hello container is built.</span></span> <span data-ttu-id="0d362-123">Gelen başlatır bir [resmi Node.js görüntü] [ dockerhub-nodeimage] göre [Alpine Linux](https://alpinelinux.org/), kapsayıcılarla uygun toouse olan küçük bir dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="0d362-123">It starts from an [official Node.js image][dockerhub-nodeimage] based on [Alpine Linux](https://alpinelinux.org/), a small distribution that is well suited toouse with containers.</span></span> <span data-ttu-id="0d362-124">Ardından hello kapsayıcıya hello uygulama dosyalarını kopyalar, hello düğüm paketi Yöneticisi kullanarak bağımlılıkları yükler ve son olarak hello uygulamayı başlatır.</span><span class="sxs-lookup"><span data-stu-id="0d362-124">It then copies hello application files into hello container, installs dependencies using hello Node Package Manager, and finally starts hello application.</span></span>

```
FROM node:8.2.0-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

<span data-ttu-id="0d362-125">Kullanım hello `docker build` olarak etiketleme komutu toocreate hello kapsayıcı görüntüsü, *aci öğretici uygulama*:</span><span class="sxs-lookup"><span data-stu-id="0d362-125">Use hello `docker build` command toocreate hello container image, tagging it as *aci-tutorial-app*:</span></span>

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

<span data-ttu-id="0d362-126">Kullanım hello `docker images` toosee yerleşik hello görüntü:</span><span class="sxs-lookup"><span data-stu-id="0d362-126">Use hello `docker images` toosee hello built image:</span></span>

```bash
docker images
```

<span data-ttu-id="0d362-127">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="0d362-127">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-hello-container-locally"></a><span data-ttu-id="0d362-128">Merhaba kapsayıcı yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="0d362-128">Run hello container locally</span></span>

<span data-ttu-id="0d362-129">Merhaba kapsayıcı tooAzure kapsayıcı örnekleri dağıtma denemeden önce yerel olarak çalıştırma çalıştığını tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="0d362-129">Before you try deploying hello container tooAzure Container Instances, run it locally tooconfirm that it works.</span></span> <span data-ttu-id="0d362-130">Merhaba `-d` anahtar hello arka planda çalışan hello kapsayıcı sağlar ancak `-p` toomap, işlem tooport 80 hello kapsayıcısında rastgele bir bağlantı noktası sağlar.</span><span class="sxs-lookup"><span data-stu-id="0d362-130">hello `-d` switch lets hello container run in hello background, while `-p` allows you toomap an arbitrary port on your compute tooport 80 in hello container.</span></span>

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

<span data-ttu-id="0d362-131">Kapsayıcı hello açık hello tarayıcı toohttp://localhost:8080 tooconfirm çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="0d362-131">Open hello browser toohttp://localhost:8080 tooconfirm that hello container is running.</span></span>

![Merhaba tarayıcıda yerel olarak çalışan hello uygulama][aci-tutorial-app-local]

## <a name="next-steps"></a><span data-ttu-id="0d362-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0d362-133">Next steps</span></span>

<span data-ttu-id="0d362-134">Bu öğreticide, dağıtılan tooAzure kapsayıcı örnekleri olabilir bir kapsayıcı görüntüsü oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="0d362-134">In this tutorial, you created a container image that can be deployed tooAzure Container Instances.</span></span> <span data-ttu-id="0d362-135">Aşağıdaki adımları hello tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="0d362-135">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0d362-136">Merhaba Uygulama kaynağı github'dan kopyalama</span><span class="sxs-lookup"><span data-stu-id="0d362-136">Cloning hello application source from GitHub</span></span>  
> * <span data-ttu-id="0d362-137">Uygulama kaynağından kapsayıcı görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="0d362-137">Creating container images from application source</span></span>
> * <span data-ttu-id="0d362-138">Merhaba kapsayıcı yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="0d362-138">Testing hello container locally</span></span>

<span data-ttu-id="0d362-139">Kapsayıcı görüntüleri bir Azure kapsayıcı kayıt defterine depolama hakkında toohello sonraki öğretici toolearn ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="0d362-139">Advance toohello next tutorial toolearn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0d362-140">Anında iletme görüntüleri tooAzure kapsayıcı kayıt defteri</span><span class="sxs-lookup"><span data-stu-id="0d362-140">Push images tooAzure Container Registry</span></span>](./container-instances-tutorial-prepare-acr.md)

<!-- LINKS -->
[dockerhub-nodeimage]: https://hub.docker.com/r/library/node/tags/8.2.0-alpine/

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png