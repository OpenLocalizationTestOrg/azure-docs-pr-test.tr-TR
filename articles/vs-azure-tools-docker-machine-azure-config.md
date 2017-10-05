---
title: "Docker makine ile azure'da Docker konakları oluştur | Microsoft Docs"
description: "Docker Azure'da docker ana bilgisayarları oluşturmak için makine kullanımını açıklar."
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 7a3ff6e1-fa93-4a62-b524-ab182d2fea08
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 766d327a87ed13e04166d71c3d9ae0a1e7a66d19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a><span data-ttu-id="bda8a-103">Docker-Machine ile Azure’da Docker Ana Bilgisayarları Oluşturma</span><span class="sxs-lookup"><span data-stu-id="bda8a-103">Create Docker Hosts in Azure with Docker-Machine</span></span>
<span data-ttu-id="bda8a-104">Çalışan [Docker](https://www.docker.com/) kapsayıcıları VM docker arka plan programı çalıştıran bir konak gerektirir.</span><span class="sxs-lookup"><span data-stu-id="bda8a-104">Running [Docker](https://www.docker.com/) containers requires a host VM running the docker daemon.</span></span>
<span data-ttu-id="bda8a-105">Bu konuda nasıl kullanılacağını açıklar [docker makine](https://docs.docker.com/machine/) yeni Linux VM'ler, Azure'da çalışan Docker daemon ile yapılandırılmış oluşturmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="bda8a-105">This topic describes how to use the [docker-machine](https://docs.docker.com/machine/) command to create new Linux VMs, configured with the Docker daemon, running in Azure.</span></span> 

<span data-ttu-id="bda8a-106">**Not:**</span><span class="sxs-lookup"><span data-stu-id="bda8a-106">**Note:**</span></span> 

* <span data-ttu-id="bda8a-107">*Bu makalede docker makine sürüm 0.9.0-rc2 ya da büyük bağlıdır*</span><span class="sxs-lookup"><span data-stu-id="bda8a-107">*This article depends on docker-machine version 0.9.0-rc2 or greater*</span></span>
* <span data-ttu-id="bda8a-108">*Windows kapsayıcıları docker-makine üzerinden yakın gelecekte desteklenecektir*</span><span class="sxs-lookup"><span data-stu-id="bda8a-108">*Windows Containers will be supported through docker-machine in the near future*</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="bda8a-109">Docker makineyle VM'ler oluşturma</span><span class="sxs-lookup"><span data-stu-id="bda8a-109">Create VMs with Docker Machine</span></span>
<span data-ttu-id="bda8a-110">Docker ana VM'ler ile Azure oluşturmak `docker-machine create` komutu kullanılarak `azure` sürücü.</span><span class="sxs-lookup"><span data-stu-id="bda8a-110">Create docker host VMs in Azure with the `docker-machine create` command using the `azure` driver.</span></span> 

<span data-ttu-id="bda8a-111">Azure sürücüsü, abonelik kimliği gereklidir.</span><span class="sxs-lookup"><span data-stu-id="bda8a-111">The Azure driver requires your subscription ID.</span></span> <span data-ttu-id="bda8a-112">Kullanabileceğiniz [Azure CLI](cli-install-nodejs.md) veya [Azure Portal](https://portal.azure.com) Azure aboneliğinizi alınamadı.</span><span class="sxs-lookup"><span data-stu-id="bda8a-112">You can use the [Azure CLI](cli-install-nodejs.md) or the [Azure Portal](https://portal.azure.com) to retrieve your Azure Subscription.</span></span> 

<span data-ttu-id="bda8a-113">**Azure Portalı'nı kullanarak**</span><span class="sxs-lookup"><span data-stu-id="bda8a-113">**Using the Azure Portal**</span></span>

* <span data-ttu-id="bda8a-114">Seçin **abonelikleri** sol gezinti sayfasında ve kopyalama abonelik kimliği.</span><span class="sxs-lookup"><span data-stu-id="bda8a-114">Select **Subscriptions** from the left navigation page and copy the subscription id.</span></span>

<span data-ttu-id="bda8a-115">**Azure CLI kullanma**</span><span class="sxs-lookup"><span data-stu-id="bda8a-115">**Using the Azure CLI**</span></span>

* <span data-ttu-id="bda8a-116">Tür ```azure account list``` ve abonelik kimliğini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="bda8a-116">Type ```azure account list``` and copy the subscription id.</span></span>

<span data-ttu-id="bda8a-117">Tür `docker-machine create --driver azure` seçenekleri ve varsayılan değerleri görmek için.</span><span class="sxs-lookup"><span data-stu-id="bda8a-117">Type `docker-machine create --driver azure` to see the options and their default values.</span></span>
<span data-ttu-id="bda8a-118">Ayrıca bkz [Docker Azure sürücü belgelerine](https://docs.docker.com/machine/drivers/azure/) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="bda8a-118">You can also see the [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/) for more info.</span></span> 

<span data-ttu-id="bda8a-119">Aşağıdaki örnek bağlı kullanır [varsayılan değerlerin](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), ancak isteğe bağlı olarak bu değerleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="bda8a-119">The following example relies upon the [default values](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), but it does optionally set these values:</span></span> 

* <span data-ttu-id="bda8a-120">Azure dns için oluşturulan sertifikaları ve genel IP ile ilişkili adı.</span><span class="sxs-lookup"><span data-stu-id="bda8a-120">azure-dns for the name associated with the public IP and certificates generated.</span></span> <span data-ttu-id="bda8a-121">Sanal makineniz DNS adıdır.</span><span class="sxs-lookup"><span data-stu-id="bda8a-121">This is the DNS name of your virtual machine.</span></span> <span data-ttu-id="bda8a-122">VM ardından güvenli bir şekilde Durdur, dinamik IP bırakın ve vm ile yeni bir IP yeniden başlatıldıktan sonra yeniden bağlanmayı olanağı sunar.</span><span class="sxs-lookup"><span data-stu-id="bda8a-122">The VM can then safely stop, release the dynamic IP, and provide the ability to reconnect after the vm starts again with a new IP.</span></span> <span data-ttu-id="bda8a-123">Adı ön eki Bu bölge UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bda8a-123">The name prefix must be unique for that region  UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span></span>
* <span data-ttu-id="bda8a-124">VM giden internet erişimi için bağlantı noktası 80'i açın</span><span class="sxs-lookup"><span data-stu-id="bda8a-124">open port 80 on the VM for outbound internet access</span></span>
* <span data-ttu-id="bda8a-125">daha hızlı premium depolama alanını VM boyutu</span><span class="sxs-lookup"><span data-stu-id="bda8a-125">size of the VM to utilize faster premium storage</span></span>
* <span data-ttu-id="bda8a-126">premium depolama vm disk için kullanılır</span><span class="sxs-lookup"><span data-stu-id="bda8a-126">premium storage used for the vm disk</span></span>

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a><span data-ttu-id="bda8a-127">Docker docker makineyle seçin</span><span class="sxs-lookup"><span data-stu-id="bda8a-127">Choose a docker host with docker-machine</span></span>
<span data-ttu-id="bda8a-128">Docker-makine konağınız için bir giriş olduktan sonra docker komutlarını çalıştırırken varsayılan ana bilgisayar ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bda8a-128">Once you have an entry in docker-machine for your host, you can set the default host when running docker commands.</span></span>

## <a name="using-powershell"></a><span data-ttu-id="bda8a-129">PowerShell’i kullanma</span><span class="sxs-lookup"><span data-stu-id="bda8a-129">Using PowerShell</span></span>
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a><span data-ttu-id="bda8a-130">Bash kullanma</span><span class="sxs-lookup"><span data-stu-id="bda8a-130">Using Bash</span></span>
```bash
eval $(docker-machine env MyDockerHost)
```

<span data-ttu-id="bda8a-131">Belirtilen konak karşı şimdi docker komutları çalıştırabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="bda8a-131">You can now run docker commands against the specified host</span></span>

```
docker ps
docker info
```

## <a name="run-a-container"></a><span data-ttu-id="bda8a-132">Bir kapsayıcı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="bda8a-132">Run a container</span></span>
<span data-ttu-id="bda8a-133">Yapılandırılmış olan bir konak ana bilgisayarınız doğru yapılandırılmış olup olmadığını sınamak için basit bir web sunucusu artık çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bda8a-133">With a host configured, you can now run a simple web server to test whether your host was configured correctly.</span></span>
<span data-ttu-id="bda8a-134">Burada bir standart nginx yansıması kullanın, bağlantı noktası 80 üzerinde dinleme yapması gerektiğini belirtin ve VM konak yeniden başlatılırsa, kapsayıcı olur de yeniden (`--restart=always`).</span><span class="sxs-lookup"><span data-stu-id="bda8a-134">Here we use a standard nginx image, specify that it should listen on port 80, and that if the host VM restarts, the container will restart as well (`--restart=always`).</span></span> 

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="bda8a-135">Çıktı aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="bda8a-135">The output should look something like the following:</span></span>

```
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-the-container"></a><span data-ttu-id="bda8a-136">Test kapsayıcısı</span><span class="sxs-lookup"><span data-stu-id="bda8a-136">Test the container</span></span>
<span data-ttu-id="bda8a-137">Kullanarak çalışan kapsayıcılar inceleyin `docker ps`:</span><span class="sxs-lookup"><span data-stu-id="bda8a-137">Examine running containers using `docker ps`:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

<span data-ttu-id="bda8a-138">Ve çalışan kapsayıcı görmek için şunu yazın `docker-machine ip <VM name>` tarayıcıya girmek için IP adresini bulmak için:</span><span class="sxs-lookup"><span data-stu-id="bda8a-138">And, to see the running container, type `docker-machine ip <VM name>` to find the IP address to enter in the browser:</span></span>

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![Çalışan ngnix kapsayıcı](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a><span data-ttu-id="bda8a-140">Özet</span><span class="sxs-lookup"><span data-stu-id="bda8a-140">Summary</span></span>
<span data-ttu-id="bda8a-141">Docker-makineyle Azure docker ana bilgisayarlar için ayrı ayrı docker ana doğrulamaları kolayca sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bda8a-141">With docker-machine, you can easily provision docker hosts in Azure for your individual docker host validations.</span></span>
<span data-ttu-id="bda8a-142">Üretim için kapsayıcı görevi, barındırma bkz [Azure kapsayıcı hizmeti](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="bda8a-142">For production hosting of containers, see the [Azure Container Service](http://aka.ms/AzureContainerService)</span></span>

<span data-ttu-id="bda8a-143">Visual Studio ile .NET Core uygulamaları geliştirmek için bkz: [Visual Studio için Docker araçları](http://aka.ms/DockerToolsForVS)</span><span class="sxs-lookup"><span data-stu-id="bda8a-143">To develop .NET Core Applications with Visual Studio, see [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)</span></span>

