---
title: "aaaManage Azure Swarm Docker API'si ile küme | Microsoft Docs"
description: "Azure kapsayıcı hizmetinde kapsayıcıları tooa Docker Swarm kümesi dağıtma"
services: container-service
documentationcenter: 
author: rgardler
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Docker, Kapsayıcılar, Mikro hizmetler, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: bb9b07c82a7b48caeb2e351455797cbf2a6e7480
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="container-management-with-docker-swarm"></a><span data-ttu-id="07728-104">Docker Swarm ile kapsayıcı yönetimi</span><span class="sxs-lookup"><span data-stu-id="07728-104">Container management with Docker Swarm</span></span>
<span data-ttu-id="07728-105">Docker Swarm, havuza alınmış Docker ana bilgisayarları grubuna kapsayıcılı iş yükleri dağıtmak için bir ortam sağlar.</span><span class="sxs-lookup"><span data-stu-id="07728-105">Docker Swarm provides an environment for deploying containerized workloads across a pooled set of Docker hosts.</span></span> <span data-ttu-id="07728-106">Docker Swarm hello yerel Docker API'sini kullanır.</span><span class="sxs-lookup"><span data-stu-id="07728-106">Docker Swarm uses hello native Docker API.</span></span> <span data-ttu-id="07728-107">Docker Swarm kapsayıcılarında yönetmek için hello bir tek kapsayıcılı ana bilgisayardakiyle neredeyse aynı toowhat iş akışıdır.</span><span class="sxs-lookup"><span data-stu-id="07728-107">hello workflow for managing containers on a Docker Swarm is almost identical toowhat it would be on a single container host.</span></span> <span data-ttu-id="07728-108">Bu belge Docker Swarm’ın Azure Kapsayıcı Hizmeti örneğine kapsayıcılı iş yüklerini dağıtmaya ilişkin basit örnekler sağlar.</span><span class="sxs-lookup"><span data-stu-id="07728-108">This document provides simple examples of deploying containerized workloads in an Azure Container Service instance of Docker Swarm.</span></span> <span data-ttu-id="07728-109">Docker Swarm hakkında daha fazla ayrıntılı belgeler için bkz. [Docker.com’da Docker Swarm ](https://docs.docker.com/swarm/).</span><span class="sxs-lookup"><span data-stu-id="07728-109">For more in-depth documentation on Docker Swarm, see [Docker Swarm on Docker.com](https://docs.docker.com/swarm/).</span></span>

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="07728-110">Bu belge toohello alıştırmalarda Önkoşullar:</span><span class="sxs-lookup"><span data-stu-id="07728-110">Prerequisites toohello exercises in this document:</span></span>

[<span data-ttu-id="07728-111">Azure Container Service'te Swarm kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="07728-111">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)

[<span data-ttu-id="07728-112">Azure kapsayıcı Hizmeti'nde hello Swarm kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="07728-112">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)

## <a name="deploy-a-new-container"></a><span data-ttu-id="07728-113">Yeni bir kapsayıcı dağıtma</span><span class="sxs-lookup"><span data-stu-id="07728-113">Deploy a new container</span></span>
<span data-ttu-id="07728-114">toocreate hello Docker Swarm, yeni bir kapsayıcıda kullanmak hello `docker run` (bir SSH tünel toohello yöneticileri hello Önkoşullar yukarıdaki göredir açtığınız sağlama) komutu.</span><span class="sxs-lookup"><span data-stu-id="07728-114">toocreate a new container in hello Docker Swarm, use hello `docker run` command (ensuring that you have opened an SSH tunnel toohello masters as per hello prerequisites above).</span></span> <span data-ttu-id="07728-115">Bu örnek, hello bir kapsayıcı oluşturur `yeasy/simple-web` görüntü:</span><span class="sxs-lookup"><span data-stu-id="07728-115">This example creates a container from hello `yeasy/simple-web` image:</span></span>

```bash
user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web

4298d397b9ab6f37e2d1978ef3c8c1537c938e98a8bf096ff00def2eab04bf72
```

<span data-ttu-id="07728-116">Merhaba kapsayıcıyı oluşturduktan sonra kullanmak `docker ps` hello kapsayıcı hakkında tooreturn bilgi.</span><span class="sxs-lookup"><span data-stu-id="07728-116">After hello container has been created, use `docker ps` tooreturn information about hello container.</span></span> <span data-ttu-id="07728-117">Burada hello kapsayıcıyı barındıran bu hello Swarm aracının listelendiğine dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="07728-117">Notice here that hello Swarm agent that is hosting hello container is listed:</span></span>

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   31 seconds ago      Up 9 seconds        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

<span data-ttu-id="07728-118">Merhaba hello Swarm aracı yük dengeleyicinin Genel DNS adı aracılığıyla bu kapsayıcıda çalışan Merhaba uygulaması artık erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07728-118">You can now access hello application that is running in this container through hello public DNS name of hello Swarm agent load balancer.</span></span> <span data-ttu-id="07728-119">Bu bilgileri hello Azure portalında bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="07728-119">You can find this information in hello Azure portal:</span></span>  

![Gerçek ziyaret sonuçları](./media/container-service-docker-swarm/real-visit.jpg)  

<span data-ttu-id="07728-121">Varsayılan olarak bağlantı noktası 80, hello yük dengeleyiciye sahip 8080 ve 443 numaralı açın.</span><span class="sxs-lookup"><span data-stu-id="07728-121">By default hello Load Balancer has ports 80, 8080 and 443 open.</span></span> <span data-ttu-id="07728-122">Başka bir bağlantı noktasında tooconnect istiyorsanız aracı havuzu hello için bu bağlantı noktasını hello Azure yük dengeleyici tooopen gerekir.</span><span class="sxs-lookup"><span data-stu-id="07728-122">If you want tooconnect on another port you will need tooopen that port on hello Azure Load Balancer for hello Agent Pool.</span></span>

## <a name="deploy-multiple-containers"></a><span data-ttu-id="07728-123">Birden çok kapsayıcı dağıtma</span><span class="sxs-lookup"><span data-stu-id="07728-123">Deploy multiple containers</span></span>
<span data-ttu-id="07728-124">Birden çok kapsayıcı başlatıldığında, birden çok kez 'docker run' yürüterek hello kullanabilirsiniz `docker ps` üzerinde çalışan Merhaba kapsayıcılara barındıran komutu toosee.</span><span class="sxs-lookup"><span data-stu-id="07728-124">As multiple containers are started, by executing 'docker run' multiple times, you can use hello `docker ps` command toosee which hosts hello containers are running on.</span></span> <span data-ttu-id="07728-125">Merhaba aşağıdaki örnekte, üç kapsayıcı hello üç Swarm aracısında eşit olarak yayılır:</span><span class="sxs-lookup"><span data-stu-id="07728-125">In hello example below, three containers are spread evenly across hello three Swarm agents:</span></span>  

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
11be062ff602        yeasy/simple-web    "/bin/sh -c 'python i"   11 seconds ago      Up 10 seconds       10.0.0.6:83->80/tcp   swarm-agent-34A73819-2/clever_banach
1ff421554c50        yeasy/simple-web    "/bin/sh -c 'python i"   49 seconds ago      Up 48 seconds       10.0.0.4:82->80/tcp   swarm-agent-34A73819-0/stupefied_ride
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   2 minutes ago       Up 2 minutes        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

## <a name="deploy-containers-by-using-docker-compose"></a><span data-ttu-id="07728-126">Docker Compose kullanarak kapsayıcıları dağıtma</span><span class="sxs-lookup"><span data-stu-id="07728-126">Deploy containers by using Docker Compose</span></span>
<span data-ttu-id="07728-127">Docker Compose tooautomate hello dağıtımını ve yapılandırmasını birden çok kapsayıcı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07728-127">You can use Docker Compose tooautomate hello deployment and configuration of multiple containers.</span></span> <span data-ttu-id="07728-128">toodo, bir güvenli Kabuk (SSH) tüneli oluşturulduğundan ve (Merhaba ön koşullar yukarıdaki bakın) bu hello DOCKER_HOST değişkeninin ayarlandığından, olun.</span><span class="sxs-lookup"><span data-stu-id="07728-128">toodo so, ensure that a Secure Shell (SSH) tunnel has been created and that hello DOCKER_HOST variable has been set (see hello pre-requisites above).</span></span>

<span data-ttu-id="07728-129">Yerel sisteminizde docker-compose.yml dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="07728-129">Create a docker-compose.yml file on your local system.</span></span> <span data-ttu-id="07728-130">toodo Bu, bunu kullanın [örnek](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span><span class="sxs-lookup"><span data-stu-id="07728-130">toodo this, use this [sample](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span></span>

```bash
web:
  image: adtd/web:0.1
  ports:
    - "80:80"
  links:
    - rest:rest-demo-azure.marathon.mesos
rest:
  image: adtd/rest:0.1
  ports:
    - "8080:8080"

```

<span data-ttu-id="07728-131">Çalıştırma `docker-compose up -d` toostart hello kapsayıcı dağıtımlarını:</span><span class="sxs-lookup"><span data-stu-id="07728-131">Run `docker-compose up -d` toostart hello container deployments:</span></span>

```bash
user@ubuntu:~/compose$ docker-compose up -d
Pulling rest (adtd/rest:0.1)...
swarm-agent-3B7093B8-0: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-3: Pulling adtd/rest:0.1... : downloaded
Creating compose_rest_1
Pulling web (adtd/web:0.1)...
swarm-agent-3B7093B8-3: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-0: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/web:0.1... : downloaded
Creating compose_web_1
```

<span data-ttu-id="07728-132">Son olarak, çalışan kapsayıcılar hello listesi döndürülür.</span><span class="sxs-lookup"><span data-stu-id="07728-132">Finally, hello list of running containers will be returned.</span></span> <span data-ttu-id="07728-133">Bu liste, Docker Compose kullanarak dağıtılan Merhaba kapsayıcılara yansıtır:</span><span class="sxs-lookup"><span data-stu-id="07728-133">This list reflects hello containers that were deployed by using Docker Compose:</span></span>

```bash
user@ubuntu:~/compose$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                     NAMES
caf185d221b7        adtd/web:0.1        "apache2-foreground"   2 minutes ago       Up About a minute   10.0.0.4:80->80/tcp       swarm-agent-3B7093B8-0/compose_web_1
040efc0ea937        adtd/rest:0.1       "catalina.sh run"      3 minutes ago       Up 2 minutes        10.0.0.4:8080->8080/tcp   swarm-agent-3B7093B8-0/compose_rest_1
```

<span data-ttu-id="07728-134">Doğal olarak, kullanabileceğiniz `docker-compose ps` tooexamine yalnızca tanımlanan kapsayıcıları Merhaba, `compose.yml` dosya.</span><span class="sxs-lookup"><span data-stu-id="07728-134">Naturally, you can use `docker-compose ps` tooexamine only hello containers defined in your `compose.yml` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07728-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="07728-135">Next steps</span></span>
[<span data-ttu-id="07728-136">Docker Swarm hakkında daha fazla bilgi edinme</span><span class="sxs-lookup"><span data-stu-id="07728-136">Learn more about Docker Swarm</span></span>](https://docs.docker.com/swarm/)

