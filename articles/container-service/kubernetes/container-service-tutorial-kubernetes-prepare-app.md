---
title: "Azure kapsayıcı hizmeti Öğreticisi - App hazırlama | Microsoft Docs"
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
ms.openlocfilehash: f02ee61ef1cd3b3dfaa051cfabe52866e3e7e838
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-container-images-to-be-used-with-azure-container-service"></a><span data-ttu-id="5902c-104">Azure kapsayıcı hizmeti ile kullanılmak üzere kapsayıcı görüntüleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="5902c-104">Create container images to be used with Azure Container Service</span></span>

<span data-ttu-id="5902c-105">Bu öğreticide, bölümü yedi, biri çok kapsayıcı uygulama Kubernetes kullanım için hazırlanır.</span><span class="sxs-lookup"><span data-stu-id="5902c-105">In this tutorial, part one of seven, a multi-container application is prepared for use in Kubernetes.</span></span> <span data-ttu-id="5902c-106">Tamamlanan adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="5902c-106">Steps completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="5902c-107">GitHub’dan uygulama kaynağını kopyalama</span><span class="sxs-lookup"><span data-stu-id="5902c-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="5902c-108">Uygulama kaynağından bir kapsayıcı görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="5902c-108">Creating a container image from the application source</span></span>
> * <span data-ttu-id="5902c-109">Uygulamayı bir yerel Docker ortamında test etme</span><span class="sxs-lookup"><span data-stu-id="5902c-109">Testing the application in a local Docker environment</span></span>

<span data-ttu-id="5902c-110">Tamamlandığında, aşağıdaki uygulama yerel geliştirme ortamınızda erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="5902c-110">Once completed, the following application is accessible in your local development environment.</span></span>

![Azure’da Kubernetes kümesinin görüntüsü](media/container-service-kubernetes-tutorials/azure-vote.png)

<span data-ttu-id="5902c-112">Sonraki öğreticilerde, kapsayıcı görüntünün bir Azure kapsayıcı kayıt defterine yüklenir ve ardından Azure çalıştırmada Kubernetes küme barındırılan.</span><span class="sxs-lookup"><span data-stu-id="5902c-112">In subsequent tutorials, the container image is uploaded to an Azure Container Registry, and then run in an Azure hosted Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5902c-113">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="5902c-113">Before you begin</span></span>

<span data-ttu-id="5902c-114">Bu öğreticide kapsayıcılar, kapsayıcı görüntüleri ve temel docker komutları gibi temel Docker kavramları hakkında bilgi sahibi olduğunuz varsayılmıştır.</span><span class="sxs-lookup"><span data-stu-id="5902c-114">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="5902c-115">Gerekirse kapsayıcı temelleri hakkında bilgi için bkz. [Docker ile çalışmaya başlama]( https://docs.docker.com/get-started/).</span><span class="sxs-lookup"><span data-stu-id="5902c-115">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="5902c-116">Bu öğreticiyi tamamlamak için Docker geliştirme ortamı gerekir.</span><span class="sxs-lookup"><span data-stu-id="5902c-116">To complete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="5902c-117">Docker, [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) veya [Linux](https://docs.docker.com/engine/installation/#supported-platforms)’ta Docker’ı kolayca yapılandırmanızı sağlayan paketler sağlar.</span><span class="sxs-lookup"><span data-stu-id="5902c-117">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="5902c-118">Uygulama kodunu alma</span><span class="sxs-lookup"><span data-stu-id="5902c-118">Get application code</span></span>

<span data-ttu-id="5902c-119">Bu öğreticide kullanılan örnek temel bir oylama uygulama uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="5902c-119">The sample application used in this tutorial is a basic voting app.</span></span> <span data-ttu-id="5902c-120">Uygulama bir ön uç web bileşeni ve bir arka uç Redis örneği oluşur.</span><span class="sxs-lookup"><span data-stu-id="5902c-120">The application consists of a front-end web component and a back-end Redis instance.</span></span> <span data-ttu-id="5902c-121">Web bileşeni özel kapsayıcı görüntüsüne paketlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="5902c-121">The web component is packaged into a custom container image.</span></span> <span data-ttu-id="5902c-122">Redis örneği Docker hub'a değiştirilmemiş bir görüntüden kullanır.</span><span class="sxs-lookup"><span data-stu-id="5902c-122">The Redis instance uses an unmodified image from Docker Hub.</span></span>  

<span data-ttu-id="5902c-123">Geliştirme ortamınızı uygulamaya bir kopyasını indirmek için Git kullanın.</span><span class="sxs-lookup"><span data-stu-id="5902c-123">Use git to download a copy of the application to your development environment.</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="5902c-124">Kopyalanan dizini içinde uygulama kaynak koduna, önceden oluşturulmuş bir Docker compose dosyası ve bir Kubernetes bildirim dosyası.</span><span class="sxs-lookup"><span data-stu-id="5902c-124">Inside the cloned directory is the application source code, a pre-created Docker compose file, and a Kubernetes manifest file.</span></span> <span data-ttu-id="5902c-125">Bu dosyalar, öğretici kümesi boyunca varlıklar oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5902c-125">These files are used to create assets throughout the tutorial set.</span></span> 

## <a name="create-container-images"></a><span data-ttu-id="5902c-126">Kapsayıcı görüntüleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="5902c-126">Create container images</span></span>

<span data-ttu-id="5902c-127">[Docker Compose](https://docs.docker.com/compose/) yapı kapsayıcı görüntüler ve birden çok kapsayıcı uygulamalarının dağıtımını otomatik hale getirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5902c-127">[Docker Compose](https://docs.docker.com/compose/) can be used to automate the build out of container images and the deployment of multi-container applications.</span></span>

<span data-ttu-id="5902c-128">Kapsayıcı görüntü oluşturma, Redis görüntüsünü karşıdan yüklemek ve uygulamayı başlatmak için docker-compose.yml dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5902c-128">Run the docker-compose.yml file to create the container image, download the Redis image, and start the application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up -d
```

<span data-ttu-id="5902c-129">Tamamlandığında kullanmak [docker görüntüleri](https://docs.docker.com/engine/reference/commandline/images/) oluşturulan görüntüleri görmek için komutu.</span><span class="sxs-lookup"><span data-stu-id="5902c-129">When completed, use the [docker images](https://docs.docker.com/engine/reference/commandline/images/) command to see the created images.</span></span>

```bash
docker images
```

<span data-ttu-id="5902c-130">Üç görüntüleri indirilebilir veya oluşturulan dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="5902c-130">Notice that three images have been downloaded or created.</span></span> <span data-ttu-id="5902c-131">*Azure oy ön* görüntü, uygulama içerir.</span><span class="sxs-lookup"><span data-stu-id="5902c-131">The *azure-vote-front* image contains the application.</span></span> <span data-ttu-id="5902c-132">Türetilmiş *nginx flask* görüntü.</span><span class="sxs-lookup"><span data-stu-id="5902c-132">It was derived from the *nginx-flask* image.</span></span> <span data-ttu-id="5902c-133">Redis görüntü Docker Hub'ından yüklendi.</span><span class="sxs-lookup"><span data-stu-id="5902c-133">The Redis image was downloaded from Docker Hub.</span></span>

```bash
REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="5902c-134">Çalıştırma [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) çalışan kapsayıcıları görmek için komutu.</span><span class="sxs-lookup"><span data-stu-id="5902c-134">Run the [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) command to see the running containers.</span></span>

```bash
docker ps
```

<span data-ttu-id="5902c-135">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="5902c-135">Output:</span></span>

```bash
CONTAINER ID        IMAGE             COMMAND                  CREATED             STATUS              PORTS                           NAMES
82411933e8f9        azure-vote-front  "/usr/bin/supervisord"   57 seconds ago      Up 30 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
b68fed4b66b6        redis             "docker-entrypoint..."   57 seconds ago      Up 30 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a><span data-ttu-id="5902c-136">Uygulamayı yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="5902c-136">Test application locally</span></span>

<span data-ttu-id="5902c-137">Çalışan uygulama görmek için http://localhost: 8080 için göz atın.</span><span class="sxs-lookup"><span data-stu-id="5902c-137">Browse to http://localhost:8080 to see the running application.</span></span>

![Azure’da Kubernetes kümesinin görüntüsü](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="clean-up-resources"></a><span data-ttu-id="5902c-139">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="5902c-139">Clean up resources</span></span>

<span data-ttu-id="5902c-140">Uygulama işlevselliği doğrulandı, çalışan kapsayıcılar durdurulur ve kaldırılmış.</span><span class="sxs-lookup"><span data-stu-id="5902c-140">Now that application functionality has been validated, the running containers can be stopped and removed.</span></span> <span data-ttu-id="5902c-141">Kapsayıcı görüntüleri silmeyin.</span><span class="sxs-lookup"><span data-stu-id="5902c-141">Do not delete the container images.</span></span> <span data-ttu-id="5902c-142">*Azure oy ön* görüntü sonraki öğreticide Azure kapsayıcı kayıt defteri örneğine yüklenir.</span><span class="sxs-lookup"><span data-stu-id="5902c-142">The *azure-vote-front* image is uploaded to an Azure Container Registry instance in the next tutorial.</span></span>

<span data-ttu-id="5902c-143">Çalışan kapsayıcılar durdurmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5902c-143">Run the following to stop the running containers.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml stop
```

<span data-ttu-id="5902c-144">Aşağıdaki komutla durdurulmuş kapsayıcıları silin.</span><span class="sxs-lookup"><span data-stu-id="5902c-144">Delete the stopped containers with the following command.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml rm
```

<span data-ttu-id="5902c-145">Tamamlandığında, Azure oy uygulamayı içeren bir kapsayıcı görüntüsüne sahip.</span><span class="sxs-lookup"><span data-stu-id="5902c-145">At completion, you have a container image that contains the Azure Vote application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5902c-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5902c-146">Next steps</span></span>

<span data-ttu-id="5902c-147">Bu öğreticide, bir uygulamayı test edilmiştir ve kapsayıcı görüntüleri uygulama için oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="5902c-147">In this tutorial, an application was tested and container images created for the application.</span></span> <span data-ttu-id="5902c-148">Aşağıdaki adımlar tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="5902c-148">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5902c-149">GitHub’dan uygulama kaynağını kopyalama</span><span class="sxs-lookup"><span data-stu-id="5902c-149">Cloning the application source from GitHub</span></span>  
> * <span data-ttu-id="5902c-150">Uygulama kaynağından bir kapsayıcı görüntüsü oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="5902c-150">Created a container image from application source</span></span>
> * <span data-ttu-id="5902c-151">Uygulamayı yerel bir Docker ortamında test</span><span class="sxs-lookup"><span data-stu-id="5902c-151">Tested the application in a local Docker environment</span></span>

<span data-ttu-id="5902c-152">Kapsayıcı görüntülerini bir Azure Container Registry’de depolama hakkında bilgi edinmek için sonraki öğreticiye geçin.</span><span class="sxs-lookup"><span data-stu-id="5902c-152">Advance to the next tutorial to learn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5902c-153">Azure Container Registry’ye görüntüleri gönderme</span><span class="sxs-lookup"><span data-stu-id="5902c-153">Push images to Azure Container Registry</span></span>](./container-service-tutorial-kubernetes-prepare-acr.md)