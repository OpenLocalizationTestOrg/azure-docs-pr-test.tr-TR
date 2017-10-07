---
title: "aaaCreate Docker barındıran Docker makine ile azure'da | Microsoft Docs"
description: "Docker toocreate docker makineler Azure kullanımını açıklar."
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
ms.openlocfilehash: fbf67e8189bbf33f874c4a9b619a931f28ccee12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a><span data-ttu-id="d761c-103">Docker-Machine ile Azure’da Docker Ana Bilgisayarları Oluşturma</span><span class="sxs-lookup"><span data-stu-id="d761c-103">Create Docker Hosts in Azure with Docker-Machine</span></span>
<span data-ttu-id="d761c-104">Çalışan [Docker](https://www.docker.com/) kapsayıcıları konak VM çalışan hello docker daemon gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d761c-104">Running [Docker](https://www.docker.com/) containers requires a host VM running hello docker daemon.</span></span>
<span data-ttu-id="d761c-105">Bu konuda açıklanmaktadır nasıl toouse hello [docker makine](https://docs.docker.com/machine/) toocreate yeni Linux VM'ler, yapılandırılmış ile Merhaba Docker arka plan programı, Azure'da çalışan komutu.</span><span class="sxs-lookup"><span data-stu-id="d761c-105">This topic describes how toouse hello [docker-machine](https://docs.docker.com/machine/) command toocreate new Linux VMs, configured with hello Docker daemon, running in Azure.</span></span> 

<span data-ttu-id="d761c-106">**Not:**</span><span class="sxs-lookup"><span data-stu-id="d761c-106">**Note:**</span></span> 

* <span data-ttu-id="d761c-107">*Bu makalede docker makine sürüm 0.9.0-rc2 ya da büyük bağlıdır*</span><span class="sxs-lookup"><span data-stu-id="d761c-107">*This article depends on docker-machine version 0.9.0-rc2 or greater*</span></span>
* <span data-ttu-id="d761c-108">*Windows kapsayıcıları docker-makine hello yakın zaman içinde aracılığıyla desteklenir*</span><span class="sxs-lookup"><span data-stu-id="d761c-108">*Windows Containers will be supported through docker-machine in hello near future*</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="d761c-109">Docker makineyle VM'ler oluşturma</span><span class="sxs-lookup"><span data-stu-id="d761c-109">Create VMs with Docker Machine</span></span>
<span data-ttu-id="d761c-110">Docker ana bilgisayar sanal makineleri Azure'da hello ile oluşturma `docker-machine create` hello kullanarak komutu `azure` sürücü.</span><span class="sxs-lookup"><span data-stu-id="d761c-110">Create docker host VMs in Azure with hello `docker-machine create` command using hello `azure` driver.</span></span> 

<span data-ttu-id="d761c-111">Hello Azure sürücüsü, abonelik kimliği gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d761c-111">hello Azure driver requires your subscription ID.</span></span> <span data-ttu-id="d761c-112">Merhaba kullanabilirsiniz [Azure CLI](cli-install-nodejs.md) veya hello [Azure Portal](https://portal.azure.com) tooretrieve Azure aboneliğinizi.</span><span class="sxs-lookup"><span data-stu-id="d761c-112">You can use hello [Azure CLI](cli-install-nodejs.md) or hello [Azure Portal](https://portal.azure.com) tooretrieve your Azure Subscription.</span></span> 

<span data-ttu-id="d761c-113">**Hello Azure Portal kullanarak**</span><span class="sxs-lookup"><span data-stu-id="d761c-113">**Using hello Azure Portal**</span></span>

* <span data-ttu-id="d761c-114">Seçin **abonelikleri** hello sol gezinti sayfası ve kopyalama hello abonelik kimliğine.</span><span class="sxs-lookup"><span data-stu-id="d761c-114">Select **Subscriptions** from hello left navigation page and copy hello subscription id.</span></span>

<span data-ttu-id="d761c-115">**Hello Azure CLI kullanma**</span><span class="sxs-lookup"><span data-stu-id="d761c-115">**Using hello Azure CLI**</span></span>

* <span data-ttu-id="d761c-116">Tür ```azure account list``` ve kopyalama hello abonelik kimliği.</span><span class="sxs-lookup"><span data-stu-id="d761c-116">Type ```azure account list``` and copy hello subscription id.</span></span>

<span data-ttu-id="d761c-117">Tür `docker-machine create --driver azure` toosee hello seçenekleri ve varsayılan değerleri.</span><span class="sxs-lookup"><span data-stu-id="d761c-117">Type `docker-machine create --driver azure` toosee hello options and their default values.</span></span>
<span data-ttu-id="d761c-118">Merhaba de görebilirsiniz [Docker Azure sürücü belgelerine](https://docs.docker.com/machine/drivers/azure/) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="d761c-118">You can also see hello [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/) for more info.</span></span> 

<span data-ttu-id="d761c-119">Merhaba aşağıdaki örnek dayanır hello [varsayılan değerlerin](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), ancak isteğe bağlı olarak bu değerleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="d761c-119">hello following example relies upon hello [default values](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), but it does optionally set these values:</span></span> 

* <span data-ttu-id="d761c-120">Azure dns hello genel IP ile ilişkili hello adı ve oluşturulan sertifikaları için.</span><span class="sxs-lookup"><span data-stu-id="d761c-120">azure-dns for hello name associated with hello public IP and certificates generated.</span></span> <span data-ttu-id="d761c-121">Sanal makinenizin hello DNS adı budur.</span><span class="sxs-lookup"><span data-stu-id="d761c-121">This is hello DNS name of your virtual machine.</span></span> <span data-ttu-id="d761c-122">Hello VM sonra güvenli bir şekilde Durdur, hello dinamik IP bırakın ve hello vm ile yeni bir IP yeniden başlatıldıktan sonra hello özelliği tooreconnect sağlayın.</span><span class="sxs-lookup"><span data-stu-id="d761c-122">hello VM can then safely stop, release hello dynamic IP, and provide hello ability tooreconnect after hello vm starts again with a new IP.</span></span> <span data-ttu-id="d761c-123">Merhaba adı ön eki Bu bölge UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d761c-123">hello name prefix must be unique for that region  UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span></span>
* <span data-ttu-id="d761c-124">Merhaba VM giden internet erişimi için bağlantı noktası 80'i açın</span><span class="sxs-lookup"><span data-stu-id="d761c-124">open port 80 on hello VM for outbound internet access</span></span>
* <span data-ttu-id="d761c-125">Merhaba VM tooutilize daha hızlı premium depolama boyutu</span><span class="sxs-lookup"><span data-stu-id="d761c-125">size of hello VM tooutilize faster premium storage</span></span>
* <span data-ttu-id="d761c-126">premium depolama Hello vm disk için kullanılır</span><span class="sxs-lookup"><span data-stu-id="d761c-126">premium storage used for hello vm disk</span></span>

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a><span data-ttu-id="d761c-127">Docker docker makineyle seçin</span><span class="sxs-lookup"><span data-stu-id="d761c-127">Choose a docker host with docker-machine</span></span>
<span data-ttu-id="d761c-128">Docker-makine konağınız için bir giriş olduktan sonra docker komutlarını çalıştırırken hello varsayılan ana bilgisayar ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d761c-128">Once you have an entry in docker-machine for your host, you can set hello default host when running docker commands.</span></span>

## <a name="using-powershell"></a><span data-ttu-id="d761c-129">PowerShell’i kullanma</span><span class="sxs-lookup"><span data-stu-id="d761c-129">Using PowerShell</span></span>
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a><span data-ttu-id="d761c-130">Bash kullanma</span><span class="sxs-lookup"><span data-stu-id="d761c-130">Using Bash</span></span>
```bash
eval $(docker-machine env MyDockerHost)
```

<span data-ttu-id="d761c-131">Şimdi docker komutları hello belirtilen konak karşı çalıştırabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d761c-131">You can now run docker commands against hello specified host</span></span>

```
docker ps
docker info
```

## <a name="run-a-container"></a><span data-ttu-id="d761c-132">Bir kapsayıcı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="d761c-132">Run a container</span></span>
<span data-ttu-id="d761c-133">Yapılandırılmış olan bir konak ana bilgisayarınız doğru yapılandırılmış olup olmadığını basit bir web sunucusu tootest şimdi çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d761c-133">With a host configured, you can now run a simple web server tootest whether your host was configured correctly.</span></span>
<span data-ttu-id="d761c-134">Burada bir standart nginx yansıması kullanın, bağlantı noktası 80 üzerinde dinleme yapması gerektiğini belirtin ve hello konak VM yeniden başlatılırsa, hello kapsayıcı olur de yeniden (`--restart=always`).</span><span class="sxs-lookup"><span data-stu-id="d761c-134">Here we use a standard nginx image, specify that it should listen on port 80, and that if hello host VM restarts, hello container will restart as well (`--restart=always`).</span></span> 

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="d761c-135">Merhaba çıktı hello aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="d761c-135">hello output should look something like hello following:</span></span>

```
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-hello-container"></a><span data-ttu-id="d761c-136">Test hello kapsayıcısı</span><span class="sxs-lookup"><span data-stu-id="d761c-136">Test hello container</span></span>
<span data-ttu-id="d761c-137">Kullanarak çalışan kapsayıcılar inceleyin `docker ps`:</span><span class="sxs-lookup"><span data-stu-id="d761c-137">Examine running containers using `docker ps`:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

<span data-ttu-id="d761c-138">Ve, kapsayıcı türü çalıştıran toosee hello `docker-machine ip <VM name>` toofind başlangıç IP adresi tooenter hello tarayıcıda:</span><span class="sxs-lookup"><span data-stu-id="d761c-138">And, toosee hello running container, type `docker-machine ip <VM name>` toofind hello IP address tooenter in hello browser:</span></span>

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![Çalışan ngnix kapsayıcı](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a><span data-ttu-id="d761c-140">Özet</span><span class="sxs-lookup"><span data-stu-id="d761c-140">Summary</span></span>
<span data-ttu-id="d761c-141">Docker-makineyle Azure docker ana bilgisayarlar için ayrı ayrı docker ana doğrulamaları kolayca sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d761c-141">With docker-machine, you can easily provision docker hosts in Azure for your individual docker host validations.</span></span>
<span data-ttu-id="d761c-142">İçin üretim hello bkz kapsayıcıları için barındırma [Azure kapsayıcı hizmeti](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="d761c-142">For production hosting of containers, see hello [Azure Container Service](http://aka.ms/AzureContainerService)</span></span>

<span data-ttu-id="d761c-143">Visual Studio .NET Core uygulamalarla toodevelop bakın [Visual Studio için Docker araçları](http://aka.ms/DockerToolsForVS)</span><span class="sxs-lookup"><span data-stu-id="d761c-143">toodevelop .NET Core Applications with Visual Studio, see [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)</span></span>

