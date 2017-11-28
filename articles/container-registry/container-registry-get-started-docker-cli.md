---
title: "Docker görüntüsünü özel Azure kayıt defterine itme | Microsoft Docs"
description: "Docker CLI’yı kullanarak Azure’da özel bir kapsayıcı kayıt defterine Docker görüntüleri itme ve kapsayıcıdan görüntü çekme"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 64fbe43f-fdde-4c17-a39a-d04f2d6d90a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 07d4d72e94eda02e8594dfddb0e911eb0e63012d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="push-your-first-image-to-a-private-docker-container-registry-using-the-docker-cli"></a><span data-ttu-id="56d20-103">Docker CLI’yı kullanarak özel bir Dockler kapsayıcı kayıt defterine ilk görüntünüzü itme</span><span class="sxs-lookup"><span data-stu-id="56d20-103">Push your first image to a private Docker container registry using the Docker CLI</span></span>
<span data-ttu-id="56d20-104">Azure kapsayıcısı kayıt defteri, [Docker Hub](https://hub.docker.com/)’ın genel Docker görüntülerini depolama yöntemine benzer şekilde özel [Docker](http://hub.docker.com) kapsayıcı görüntülerini depolar ve yönetir.</span><span class="sxs-lookup"><span data-stu-id="56d20-104">An Azure container registry stores and manages private [Docker](http://hub.docker.com) container images, similar to the way [Docker Hub](https://hub.docker.com/) stores public Docker images.</span></span> <span data-ttu-id="56d20-105">Kapsayıcı kayıt defterinizde [oturum açma](https://docs.docker.com/engine/reference/commandline/login/), [itme](https://docs.docker.com/engine/reference/commandline/push/), [çekme](https://docs.docker.com/engine/reference/commandline/pull/) ve diğer işlemleri gerçekleştirmek için [Docker Komut Satırı Arabirimi](https://docs.docker.com/engine/reference/commandline/cli/)’ni (Docker CLI) kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="56d20-105">You use the [Docker Command-Line Interface](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) for [login](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/), and other operations on your container registry.</span></span>

<span data-ttu-id="56d20-106">Arka plan ve kavramlar için, bkz: [genel bakış](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="56d20-106">For more background and concepts, see [the overview](container-registry-intro.md)</span></span>



## <a name="prerequisites"></a><span data-ttu-id="56d20-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="56d20-107">Prerequisites</span></span>
* <span data-ttu-id="56d20-108">**Azure kapsayıcısı kayıt defteri** -Azure aboneliğinizde bir kapsayıcı kayıt defteri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="56d20-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="56d20-109">Örneğin, [Azure portalını](container-registry-get-started-portal.md) veya [Azure CLI 2.0](container-registry-get-started-azure-cli.md)’ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="56d20-109">For example, use the [Azure portal](container-registry-get-started-portal.md) or the [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="56d20-110">**Docker CLI** - Yerel bilgisayarınızı bir Docker konağı olarak ayarlamak ve Docker CLI komutlarına erişmek için [Docker Engine](https://docs.docker.com/engine/installation/)’i yükleyin.</span><span class="sxs-lookup"><span data-stu-id="56d20-110">**Docker CLI** - To set up your local computer as a Docker host and access the Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>

## <a name="log-in-to-a-registry"></a><span data-ttu-id="56d20-111">Kayıt defterinde oturum açma</span><span class="sxs-lookup"><span data-stu-id="56d20-111">Log in to a registry</span></span>
<span data-ttu-id="56d20-112">Kapsayıcı kayıt defterinizde [kayıt defteri kimlik bilgileriniz](container-registry-authentication.md) ile oturum açmak için `docker login` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="56d20-112">Run `docker login` to log in to your container registry with your [registry credentials](container-registry-authentication.md).</span></span>

<span data-ttu-id="56d20-113">Aşağıdaki örnekte, bir Azure Active Directory [hizmet sorumlusunun](../active-directory/active-directory-application-objects.md) kimliği ve parolası geçirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="56d20-113">The following example passes the ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="56d20-114">Örneğin, bir otomasyon senaryosu için kayıt defterinize bir hizmet sorumlusu atamış olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56d20-114">For example, you might have assigned a service principal to your registry for an automation scenario.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> <span data-ttu-id="56d20-115">Tam kayıt defteri adını (tamamı küçük harf) belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="56d20-115">Make sure to specify the fully qualified registry name (all lowercase).</span></span> <span data-ttu-id="56d20-116">Bu örnekte bu değer `myregistry.azurecr.io`’dur.</span><span class="sxs-lookup"><span data-stu-id="56d20-116">In this example, it is `myregistry.azurecr.io`.</span></span>

## <a name="steps-to-pull-and-push-an-image"></a><span data-ttu-id="56d20-117">Görüntü çekme ve itme adımları</span><span class="sxs-lookup"><span data-stu-id="56d20-117">Steps to pull and push an image</span></span>
<span data-ttu-id="56d20-118">Aşağıdaki örnekte, genel Docker Hub kayıt defterinden Nginx görüntüsü indirilir, bu Nginx özel Azure kapsayıcısı kayıt defteriniz için etiketlenir, kayıt defterinize itilir ve yeniden çekilir.</span><span class="sxs-lookup"><span data-stu-id="56d20-118">The follow example downloads the Nginx image from the public Docker Hub registry, tags it for your private Azure container registry, pushes it to your registry, then pulls it again.</span></span>

<span data-ttu-id="56d20-119">**1. Nginx için Docker resmi görüntüsünü çekme**</span><span class="sxs-lookup"><span data-stu-id="56d20-119">**1. Pull the Docker official image for Nginx**</span></span>

<span data-ttu-id="56d20-120">Önce genel Nginx görüntüsünü yerel bilgisayarınıza çekin.</span><span class="sxs-lookup"><span data-stu-id="56d20-120">First pull the public Nginx image to your local computer.</span></span>

```
docker pull nginx
```
<span data-ttu-id="56d20-121">**2. Nginx kapsayıcısını başlatma**</span><span class="sxs-lookup"><span data-stu-id="56d20-121">**2. Start the Nginx container**</span></span>

<span data-ttu-id="56d20-122">Aşağıdaki komut yerel Nginx kapsayıcısını 8080 bağlantı noktası üzerinde etkileşimli bir şekilde başlatarak Nginx çıkışını görmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="56d20-122">The following command starts the local Nginx container interactively on port 8080, allowing you to see output from Nginx.</span></span> <span data-ttu-id="56d20-123">Durdurulduğunda çalışmakta olan kapsayıcıyı kaldırır.</span><span class="sxs-lookup"><span data-stu-id="56d20-123">It removes the running container once stopped.</span></span>

```
docker run -it --rm -p 8080:80 nginx
```

<span data-ttu-id="56d20-124">Çalışmakta olan kapsayıcıyı görmek için [http://localhost:8080](http://localhost:8080) konumuna gidin.</span><span class="sxs-lookup"><span data-stu-id="56d20-124">Browse to [http://localhost:8080](http://localhost:8080) to view the running container.</span></span> <span data-ttu-id="56d20-125">Aşağıdakine benzeyen bir ekran görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="56d20-125">You see a screen similar to the following one.</span></span>

![Yerel bilgisayarda Nginx](./media/container-registry-get-started-docker-cli/nginx.png)

<span data-ttu-id="56d20-127">Çalışmakta olan kapsayıcıyı durdurmak için [CTRL]+[C] tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="56d20-127">To stop the running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="56d20-128">**3. Kayıt defterinizde görüntünün bir diğer adını oluşturma**</span><span class="sxs-lookup"><span data-stu-id="56d20-128">**3. Create an alias of the image in your registry**</span></span>

<span data-ttu-id="56d20-129">Aşağıdaki komut, görüntünün kayıt defterinize yönelik tam ada sahip bir diğer adını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="56d20-129">The following command creates an alias of the image, with a fully qualified path to your registry.</span></span> <span data-ttu-id="56d20-130">Bu örnek, kayıt defterinin kökünde dağınıklığı önlemek için `samples` ad alanını belirtir.</span><span class="sxs-lookup"><span data-stu-id="56d20-130">This example specifies the `samples` namespace to avoid clutter in the root of the registry.</span></span>

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

<span data-ttu-id="56d20-131">**4. Görüntüyü kayıt defterinize itme**</span><span class="sxs-lookup"><span data-stu-id="56d20-131">**4. Push the image to your registry**</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="56d20-132">**5. Görüntüyü kayıt defterinizden çekme**</span><span class="sxs-lookup"><span data-stu-id="56d20-132">**5. Pull the image from your registry**</span></span>

```
docker pull myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="56d20-133">**6. Kayıt defterinizden Nginx kapsayıcısını başlatma**</span><span class="sxs-lookup"><span data-stu-id="56d20-133">**6. Start the Nginx container from your registry**</span></span>

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="56d20-134">Çalışmakta olan kapsayıcıyı görmek için [http://localhost:8080](http://localhost:8080) konumuna gidin.</span><span class="sxs-lookup"><span data-stu-id="56d20-134">Browse to [http://localhost:8080](http://localhost:8080) to view the running container.</span></span>

<span data-ttu-id="56d20-135">Çalışmakta olan kapsayıcıyı durdurmak için [CTRL]+[C] tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="56d20-135">To stop the running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="56d20-136">**7. (İsteğe bağlı) Görüntüyü kaldırma**</span><span class="sxs-lookup"><span data-stu-id="56d20-136">**7. (Optional) Remove the image**</span></span>

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a><span data-ttu-id="56d20-137">Eşzamanlı İşlem Limitleri</span><span class="sxs-lookup"><span data-stu-id="56d20-137">Concurrent Limits</span></span>
<span data-ttu-id="56d20-138">Bazı senaryolarda çağrıların eşzamanlı olarak yürütülmesi hatalara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="56d20-138">In some scenarios, executing calls concurrently might result in errors.</span></span> <span data-ttu-id="56d20-139">Aşağıdaki tabloda, Azure kapsayıcı kayıt defterindeki "Push" ve "Pull" işlemleri ile eşzamanlı çağrıların limitleri verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="56d20-139">The following table contains the limits of concurrent calls with "Push" and "Pull" operations on Azure container registry:</span></span>

| <span data-ttu-id="56d20-140">İşlem</span><span class="sxs-lookup"><span data-stu-id="56d20-140">Operation</span></span>  | <span data-ttu-id="56d20-141">Sınır</span><span class="sxs-lookup"><span data-stu-id="56d20-141">Limit</span></span>                                  |
| ---------- | -------------------------------------- |
| <span data-ttu-id="56d20-142">PULL</span><span class="sxs-lookup"><span data-stu-id="56d20-142">PULL</span></span>       | <span data-ttu-id="56d20-143">Kayıt defteri başına en fazla 10 eşzamanlı çekme</span><span class="sxs-lookup"><span data-stu-id="56d20-143">Up to 10 concurrent pulls per registry</span></span> |
| <span data-ttu-id="56d20-144">PUSH</span><span class="sxs-lookup"><span data-stu-id="56d20-144">PUSH</span></span>       | <span data-ttu-id="56d20-145">Kayıt defteri başına en fazla 5 eşzamanlı gönderme</span><span class="sxs-lookup"><span data-stu-id="56d20-145">Up to 5 concurrent pushes per registry</span></span> |

## <a name="next-steps"></a><span data-ttu-id="56d20-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="56d20-146">Next steps</span></span>
<span data-ttu-id="56d20-147">Temel bilgileri de öğrendiğinize göre artık kayıt defterinizi kullanmaya başlamaya hazırsınız demektir!</span><span class="sxs-lookup"><span data-stu-id="56d20-147">Now that you know the basics, you are ready to start using your registry!</span></span> <span data-ttu-id="56d20-148">Örneğin, bir [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) kümesine kapsayıcı görüntüleri dağıtmaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="56d20-148">For example, start deploying container images to an [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
