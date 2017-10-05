---
title: "Azure Container Instances öğreticisi - Uygulamanızı hazırlama | Azure Docs"
description: "Azure Container Instances’a dağıtılacak uygulamayı hazırlama"
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
ms.openlocfilehash: 167297e10eed11833623ff797e676ad43c65f9ad
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-container-for-deployment-to-azure-container-instances"></a><span data-ttu-id="3228c-103">Azure Container Instances’a dağıtılacak kapsayıcıyı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3228c-103">Create container for deployment to Azure Container Instances</span></span>

<span data-ttu-id="3228c-104">Azure Container Instances, Docker kapsayıcılarının herhangi bir sanal makine sağlama veya herhangi bir üst düzey hizmet benimsenmesi gerekmeden Azure altyapısına dağıtılmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="3228c-104">Azure Container Instances enables deployment of Docker containers onto Azure infrastructure without provisioning any virtual machines or adopting any higher-level service.</span></span> <span data-ttu-id="3228c-105">Bu öğreticide, Node.js içinde basit bir web uygulaması oluşturacak ve bu uygulamayı Azure Container Instances kullanılarak çalıştırılabilir bir kapsayıcıda paketleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="3228c-105">In this tutorial, you will build a simple web application in Node.js and package it in a container that can be run using Azure Container Instances.</span></span> <span data-ttu-id="3228c-106">Şu konular yer almaktadır:</span><span class="sxs-lookup"><span data-stu-id="3228c-106">We will cover:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3228c-107">GitHub’dan uygulama kaynağını kopyalama</span><span class="sxs-lookup"><span data-stu-id="3228c-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="3228c-108">Uygulama kaynağından kapsayıcı görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="3228c-108">Creating container images from application source</span></span>
> * <span data-ttu-id="3228c-109">Görüntüleri yerel bir Docker ortamında test etme</span><span class="sxs-lookup"><span data-stu-id="3228c-109">Testing the images in a local Docker environment</span></span>

<span data-ttu-id="3228c-110">Sonraki öğreticilerde, görüntülerinizi Azure Container Registry’ye yükleyecek ve Azure Container Instances’a dağıtacaksınız.</span><span class="sxs-lookup"><span data-stu-id="3228c-110">In subsequent tutorials, you will upload your image to an Azure Container Registry, and then deploy them to Azure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3228c-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="3228c-111">Before you begin</span></span>

<span data-ttu-id="3228c-112">Bu öğreticide kapsayıcılar, kapsayıcı görüntüleri ve temel docker komutları gibi temel Docker kavramları hakkında bilgi sahibi olduğunuz varsayılmıştır.</span><span class="sxs-lookup"><span data-stu-id="3228c-112">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="3228c-113">Gerekirse kapsayıcı temelleri hakkında bilgi için bkz. [Docker ile çalışmaya başlama]( https://docs.docker.com/get-started/).</span><span class="sxs-lookup"><span data-stu-id="3228c-113">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="3228c-114">Bu öğreticiyi tamamlamak için Docker geliştirme ortamı gerekir.</span><span class="sxs-lookup"><span data-stu-id="3228c-114">To complete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="3228c-115">Docker, [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) veya [Linux](https://docs.docker.com/engine/installation/#supported-platforms)’ta Docker’ı kolayca yapılandırmanızı sağlayan paketler sağlar.</span><span class="sxs-lookup"><span data-stu-id="3228c-115">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="3228c-116">Uygulama kodunu alma</span><span class="sxs-lookup"><span data-stu-id="3228c-116">Get application code</span></span>

<span data-ttu-id="3228c-117">Bu öğreticideki örnek, [Node.js](http://nodejs.org) ile yapılmış basit bir web uygulaması içerir.</span><span class="sxs-lookup"><span data-stu-id="3228c-117">The sample in this tutorial includes a simple web application built in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="3228c-118">Uygulama bir statik HTML sayfası sunar ve şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="3228c-118">The app serves a static HTML page and looks like this:</span></span>

![Tarayıcıda gösterilen öğretici uygulama][aci-tutorial-app]

<span data-ttu-id="3228c-120">Örneği indirmek için git kullanma:</span><span class="sxs-lookup"><span data-stu-id="3228c-120">Use git to download the sample:</span></span>

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-the-container-image"></a><span data-ttu-id="3228c-121">Kapsayıcı görüntüsünü oluşturma</span><span class="sxs-lookup"><span data-stu-id="3228c-121">Build the container image</span></span>

<span data-ttu-id="3228c-122">Örnek deposunda sağlanan Dockerfile, kapsayıcının nasıl yapılandırıldığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="3228c-122">The Dockerfile provided in the sample repo shows how the container is built.</span></span> <span data-ttu-id="3228c-123">Kapsayıcılarla kullanmaya uygun küçük bir dağıtım olan [Alpine Linux](https://alpinelinux.org/) tabanlı [resmi bir Node.js görüntüsünden][dockerhub-nodeimage] başlatılır.</span><span class="sxs-lookup"><span data-stu-id="3228c-123">It starts from an [official Node.js image][dockerhub-nodeimage] based on [Alpine Linux](https://alpinelinux.org/), a small distribution that is well suited to use with containers.</span></span> <span data-ttu-id="3228c-124">Ardından uygulama dosyalarını kapsayıcıya kopyalar, Node Package Manager’ı kullanarak bağımlılıkları yükler ve son olarak uygulamayı başlatır.</span><span class="sxs-lookup"><span data-stu-id="3228c-124">It then copies the application files into the container, installs dependencies using the Node Package Manager, and finally starts the application.</span></span>

```
FROM node:8.2.0-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

<span data-ttu-id="3228c-125">Kapsayıcı görüntüsünü oluşturmak için `docker build` komutunu kullanın ve görüntüyü *aci-tutorial-app* olarak etiketleyin:</span><span class="sxs-lookup"><span data-stu-id="3228c-125">Use the `docker build` command to create the container image, tagging it as *aci-tutorial-app*:</span></span>

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

<span data-ttu-id="3228c-126">Yerleşik görüntüyü görmek için `docker images` komutunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="3228c-126">Use the `docker images` to see the built image:</span></span>

```bash
docker images
```

<span data-ttu-id="3228c-127">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="3228c-127">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-the-container-locally"></a><span data-ttu-id="3228c-128">Kapsayıcıyı yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="3228c-128">Run the container locally</span></span>

<span data-ttu-id="3228c-129">Kapsayıcıyı Azure Container Instances’a dağıtmayı denemeden önce yerel olarak çalıştırarak çalışır durumda olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="3228c-129">Before you try deploying the container to Azure Container Instances, run it locally to confirm that it works.</span></span> <span data-ttu-id="3228c-130">`-d` anahtarı kapsayıcının arka planda çalışmasını sağlar. `-p` ise işleminizdeki rastgele bağlantı noktalarından birini kapsayıcının 80 numaralı bağlantı noktasına eşlemenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="3228c-130">The `-d` switch lets the container run in the background, while `-p` allows you to map an arbitrary port on your compute to port 80 in the container.</span></span>

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

<span data-ttu-id="3228c-131">Kapsayıcının çalışır durumda olduğunu doğrulamak için tarayıcıda http://localhost:8080 adresine gidin.</span><span class="sxs-lookup"><span data-stu-id="3228c-131">Open the browser to http://localhost:8080 to confirm that the container is running.</span></span>

![Uygulamayı tarayıcıda yerel olarak çalıştırma][aci-tutorial-app-local]

## <a name="next-steps"></a><span data-ttu-id="3228c-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3228c-133">Next steps</span></span>

<span data-ttu-id="3228c-134">Bu öğreticide, Azure Container Instances’a dağıtılabilir bir kapsayıcı görüntüsü oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="3228c-134">In this tutorial, you created a container image that can be deployed to Azure Container Instances.</span></span> <span data-ttu-id="3228c-135">Aşağıdaki adımlar tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="3228c-135">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3228c-136">GitHub’dan uygulama kaynağını kopyalama</span><span class="sxs-lookup"><span data-stu-id="3228c-136">Cloning the application source from GitHub</span></span>  
> * <span data-ttu-id="3228c-137">Uygulama kaynağından kapsayıcı görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="3228c-137">Creating container images from application source</span></span>
> * <span data-ttu-id="3228c-138">Kapsayıcıyı yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="3228c-138">Testing the container locally</span></span>

<span data-ttu-id="3228c-139">Kapsayıcı görüntülerini bir Azure Container Registry’de depolama hakkında bilgi edinmek için sonraki öğreticiye geçin.</span><span class="sxs-lookup"><span data-stu-id="3228c-139">Advance to the next tutorial to learn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3228c-140">Azure Container Registry’ye görüntüleri gönderme</span><span class="sxs-lookup"><span data-stu-id="3228c-140">Push images to Azure Container Registry</span></span>](./container-instances-tutorial-prepare-acr.md)

<!-- LINKS -->
[dockerhub-nodeimage]: https://hub.docker.com/r/library/node/tags/8.2.0-alpine/

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png