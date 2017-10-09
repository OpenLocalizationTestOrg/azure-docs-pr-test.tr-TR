---
title: "aaaAzure kapsayıcı hizmeti Öğreticisi - App hazırlama | Microsoft Docs"
description: "Azure kapsayıcı hizmeti Öğreticisi - App hazırlama"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Container’lar, Mikro hizmetler, Kumernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b537ecc9ff50358fb65b128bfe6eb894dd088cc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-images-toobe-used-with-azure-container-service"></a><span data-ttu-id="043a0-104">Azure kapsayıcı hizmeti ile kullanılan kapsayıcı görüntüleri toobe oluşturma</span><span class="sxs-lookup"><span data-stu-id="043a0-104">Create container images toobe used with Azure Container Service</span></span>

<span data-ttu-id="043a0-105">Bu öğreticide, bölümü yedi, biri çok kapsayıcı uygulama Kubernetes kullanım için hazırlanır.</span><span class="sxs-lookup"><span data-stu-id="043a0-105">In this tutorial, part one of seven, a multi-container application is prepared for use in Kubernetes.</span></span> <span data-ttu-id="043a0-106">Tamamlanan adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="043a0-106">Steps completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="043a0-107">GitHub’dan uygulama kaynağını kopyalama</span><span class="sxs-lookup"><span data-stu-id="043a0-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="043a0-108">Merhaba uygulama kaynağından bir kapsayıcı görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="043a0-108">Creating a container image from hello application source</span></span>
> * <span data-ttu-id="043a0-109">Merhaba uygulaması yerel bir Docker ortamında test etme</span><span class="sxs-lookup"><span data-stu-id="043a0-109">Testing hello application in a local Docker environment</span></span>

<span data-ttu-id="043a0-110">Tamamlandığında, uygulama aşağıdaki hello yerel geliştirme ortamınızda erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="043a0-110">Once completed, hello following application is accessible in your local development environment.</span></span>

![Azure’da Kubernetes kümesinin görüntüsü](media/container-service-kubernetes-tutorials/azure-vote.png)

<span data-ttu-id="043a0-112">Sonraki öğreticilerde, hello kapsayıcı görüntüdür karşıya yüklenen tooan Azure kapsayıcı kayıt defteri ve ardından Azure çalıştırmada Kubernetes küme barındırılan.</span><span class="sxs-lookup"><span data-stu-id="043a0-112">In subsequent tutorials, hello container image is uploaded tooan Azure Container Registry, and then run in an Azure hosted Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="043a0-113">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="043a0-113">Before you begin</span></span>

<span data-ttu-id="043a0-114">Bu öğreticide kapsayıcılar, kapsayıcı görüntüleri ve temel docker komutları gibi temel Docker kavramları hakkında bilgi sahibi olduğunuz varsayılmıştır.</span><span class="sxs-lookup"><span data-stu-id="043a0-114">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="043a0-115">Gerekirse kapsayıcı temelleri hakkında bilgi için bkz. [Docker ile çalışmaya başlama]( https://docs.docker.com/get-started/).</span><span class="sxs-lookup"><span data-stu-id="043a0-115">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="043a0-116">toocomplete Bu öğreticide, bir Docker geliştirme ortamı gerekir.</span><span class="sxs-lookup"><span data-stu-id="043a0-116">toocomplete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="043a0-117">Docker, [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) veya [Linux](https://docs.docker.com/engine/installation/#supported-platforms)’ta Docker’ı kolayca yapılandırmanızı sağlayan paketler sağlar.</span><span class="sxs-lookup"><span data-stu-id="043a0-117">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="043a0-118">Uygulama kodunu alma</span><span class="sxs-lookup"><span data-stu-id="043a0-118">Get application code</span></span>

<span data-ttu-id="043a0-119">Bu öğreticide kullanılan hello örnek temel bir oylama uygulama uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="043a0-119">hello sample application used in this tutorial is a basic voting app.</span></span> <span data-ttu-id="043a0-120">Merhaba uygulaması, ön uç web bileşeni ve bir arka uç Redis örneği oluşur.</span><span class="sxs-lookup"><span data-stu-id="043a0-120">hello application consists of a front-end web component and a back-end Redis instance.</span></span> <span data-ttu-id="043a0-121">Merhaba web bileşeni özel kapsayıcı görüntüsüne paketlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="043a0-121">hello web component is packaged into a custom container image.</span></span> <span data-ttu-id="043a0-122">Merhaba Redis örneği Docker hub'a değiştirilmemiş bir görüntüden kullanır.</span><span class="sxs-lookup"><span data-stu-id="043a0-122">hello Redis instance uses an unmodified image from Docker Hub.</span></span>  

<span data-ttu-id="043a0-123">Git toodownload hello uygulama tooyour geliştirme ortamı bir kopyasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="043a0-123">Use git toodownload a copy of hello application tooyour development environment.</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="043a0-124">İç hello kopyalanan dizin hello uygulama kaynak koduna, önceden oluşturulmuş bir Docker compose dosyası ve bir Kubernetes bildirim dosyası.</span><span class="sxs-lookup"><span data-stu-id="043a0-124">Inside hello cloned directory is hello application source code, a pre-created Docker compose file, and a Kubernetes manifest file.</span></span> <span data-ttu-id="043a0-125">Bu dosyalar hello öğretici kümesi boyunca kullanılan toocreate varlıkları içerir.</span><span class="sxs-lookup"><span data-stu-id="043a0-125">These files are used toocreate assets throughout hello tutorial set.</span></span> 

## <a name="create-container-images"></a><span data-ttu-id="043a0-126">Kapsayıcı görüntüleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="043a0-126">Create container images</span></span>

<span data-ttu-id="043a0-127">[Docker Compose](https://docs.docker.com/compose/) olabilir kapsayıcı görüntüleri ve birden çok kapsayıcı uygulamaları hello dağıtımı dışında tooautomate hello yapı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="043a0-127">[Docker Compose](https://docs.docker.com/compose/) can be used tooautomate hello build out of container images and hello deployment of multi-container applications.</span></span>

<span data-ttu-id="043a0-128">Merhaba docker-compose.yml dosyası toocreate hello kapsayıcı resmi çalıştırmak, indirme Merhaba, görüntü Redis ve hello uygulamasını başlatın.</span><span class="sxs-lookup"><span data-stu-id="043a0-128">Run hello docker-compose.yml file toocreate hello container image, download hello Redis image, and start hello application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up -d
```

<span data-ttu-id="043a0-129">Tamamlandığında, hello kullan [docker görüntüleri](https://docs.docker.com/engine/reference/commandline/images/) komut toosee oluşturulan hello görüntüler.</span><span class="sxs-lookup"><span data-stu-id="043a0-129">When completed, use hello [docker images](https://docs.docker.com/engine/reference/commandline/images/) command toosee hello created images.</span></span>

```bash
docker images
```

<span data-ttu-id="043a0-130">Üç görüntüleri indirilebilir veya oluşturulan dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="043a0-130">Notice that three images have been downloaded or created.</span></span> <span data-ttu-id="043a0-131">Merhaba *azure oy ön* görüntü Merhaba uygulaması içerir.</span><span class="sxs-lookup"><span data-stu-id="043a0-131">hello *azure-vote-front* image contains hello application.</span></span> <span data-ttu-id="043a0-132">Merhaba türetilmiş *nginx flask* görüntü.</span><span class="sxs-lookup"><span data-stu-id="043a0-132">It was derived from hello *nginx-flask* image.</span></span> <span data-ttu-id="043a0-133">Merhaba Redis görüntü Docker Hub'ından yüklendi.</span><span class="sxs-lookup"><span data-stu-id="043a0-133">hello Redis image was downloaded from Docker Hub.</span></span>

```bash
REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="043a0-134">Merhaba çalıştırmak [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) komutu toosee Merhaba kapsayıcılara çalıştıran.</span><span class="sxs-lookup"><span data-stu-id="043a0-134">Run hello [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) command toosee hello running containers.</span></span>

```bash
docker ps
```

<span data-ttu-id="043a0-135">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="043a0-135">Output:</span></span>

```bash
CONTAINER ID        IMAGE             COMMAND                  CREATED             STATUS              PORTS                           NAMES
82411933e8f9        azure-vote-front  "/usr/bin/supervisord"   57 seconds ago      Up 30 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
b68fed4b66b6        redis             "docker-entrypoint..."   57 seconds ago      Up 30 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a><span data-ttu-id="043a0-136">Uygulamayı yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="043a0-136">Test application locally</span></span>

<span data-ttu-id="043a0-137">Uygulama çalıştıran toohttp://localhost:8080 toosee hello göz atın.</span><span class="sxs-lookup"><span data-stu-id="043a0-137">Browse toohttp://localhost:8080 toosee hello running application.</span></span>

![Azure’da Kubernetes kümesinin görüntüsü](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="clean-up-resources"></a><span data-ttu-id="043a0-139">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="043a0-139">Clean up resources</span></span>

<span data-ttu-id="043a0-140">Uygulama işlevselliği doğrulandı, çalışan kapsayıcılar hello durdurulur ve kaldırılmış.</span><span class="sxs-lookup"><span data-stu-id="043a0-140">Now that application functionality has been validated, hello running containers can be stopped and removed.</span></span> <span data-ttu-id="043a0-141">Merhaba kapsayıcı görüntüleri silmeyin.</span><span class="sxs-lookup"><span data-stu-id="043a0-141">Do not delete hello container images.</span></span> <span data-ttu-id="043a0-142">Merhaba *azure oy ön* karşıya yüklenen tooan Azure kapsayıcı kayıt defteri örneği hello sonraki öğreticide görüntüdür.</span><span class="sxs-lookup"><span data-stu-id="043a0-142">hello *azure-vote-front* image is uploaded tooan Azure Container Registry instance in hello next tutorial.</span></span>

<span data-ttu-id="043a0-143">Çalışan kapsayıcılar toostop hello aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="043a0-143">Run hello following toostop hello running containers.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml stop
```

<span data-ttu-id="043a0-144">Durdurulmuş Merhaba kapsayıcılara komutu aşağıdaki hello ile silin.</span><span class="sxs-lookup"><span data-stu-id="043a0-144">Delete hello stopped containers with hello following command.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml rm
```

<span data-ttu-id="043a0-145">Tamamlandığında, hello Azure oy uygulamayı içeren bir kapsayıcı görüntüsüne sahip.</span><span class="sxs-lookup"><span data-stu-id="043a0-145">At completion, you have a container image that contains hello Azure Vote application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="043a0-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="043a0-146">Next steps</span></span>

<span data-ttu-id="043a0-147">Bu öğreticide, bir uygulamayı test edilmiştir ve kapsayıcı görüntüleri hello uygulaması için oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="043a0-147">In this tutorial, an application was tested and container images created for hello application.</span></span> <span data-ttu-id="043a0-148">Aşağıdaki adımları hello tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="043a0-148">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="043a0-149">Merhaba Uygulama kaynağı github'dan kopyalama</span><span class="sxs-lookup"><span data-stu-id="043a0-149">Cloning hello application source from GitHub</span></span>  
> * <span data-ttu-id="043a0-150">Uygulama kaynağından bir kapsayıcı görüntüsü oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="043a0-150">Created a container image from application source</span></span>
> * <span data-ttu-id="043a0-151">Bir yerel Docker ortamında test edilmiş hello uygulama</span><span class="sxs-lookup"><span data-stu-id="043a0-151">Tested hello application in a local Docker environment</span></span>

<span data-ttu-id="043a0-152">Kapsayıcı görüntüleri bir Azure kapsayıcı kayıt defterine depolama hakkında toohello sonraki öğretici toolearn ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="043a0-152">Advance toohello next tutorial toolearn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="043a0-153">Anında iletme görüntüleri tooAzure kapsayıcı kayıt defteri</span><span class="sxs-lookup"><span data-stu-id="043a0-153">Push images tooAzure Container Registry</span></span>](./container-service-tutorial-kubernetes-prepare-acr.md)
