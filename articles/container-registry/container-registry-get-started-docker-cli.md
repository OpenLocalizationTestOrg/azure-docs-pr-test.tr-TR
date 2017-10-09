---
title: "aaaPush Docker görüntü tooprivate Azure kayıt defteri | Microsoft Docs"
description: "İtme ve görüntüleri tooa özel kapsayıcı kayıt hello Docker CLI kullanarak azure'da Docker çekme"
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
ms.openlocfilehash: a81a6f4bfcb23642a89ac7631348d40e2f4911a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="push-your-first-image-tooa-private-docker-container-registry-using-hello-docker-cli"></a><span data-ttu-id="c1f8a-103">Merhaba Docker CLI kullanarak ilk görüntü tooa özel Docker kapsayıcısı kaydınız bildirme</span><span class="sxs-lookup"><span data-stu-id="c1f8a-103">Push your first image tooa private Docker container registry using hello Docker CLI</span></span>
<span data-ttu-id="c1f8a-104">Azure kapsayıcı kayıt defteri depolar ve özel yönetir [Docker](http://hub.docker.com) kapsayıcı görüntüler, benzer toohello şekilde [Docker hub'a](https://hub.docker.com/) ortak Docker görüntüleri depolar.</span><span class="sxs-lookup"><span data-stu-id="c1f8a-104">An Azure container registry stores and manages private [Docker](http://hub.docker.com) container images, similar toohello way [Docker Hub](https://hub.docker.com/) stores public Docker images.</span></span> <span data-ttu-id="c1f8a-105">Merhaba kullandığınız [Docker komut satırı arabirimi](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) için [oturum açma](https://docs.docker.com/engine/reference/commandline/login/), [itme](https://docs.docker.com/engine/reference/commandline/push/), [çekme](https://docs.docker.com/engine/reference/commandline/pull/)ve, kapsayıcı üzerinde başka işlemler kayıt defteri.</span><span class="sxs-lookup"><span data-stu-id="c1f8a-105">You use hello [Docker Command-Line Interface](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) for [login](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/), and other operations on your container registry.</span></span>

<span data-ttu-id="c1f8a-106">Daha fazla arka plan ve kavramları için bkz: [hello genel bakış](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="c1f8a-106">For more background and concepts, see [hello overview](container-registry-intro.md)</span></span>



## <a name="prerequisites"></a><span data-ttu-id="c1f8a-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c1f8a-107">Prerequisites</span></span>
* <span data-ttu-id="c1f8a-108">**Azure kapsayıcısı kayıt defteri** -Azure aboneliğinizde bir kapsayıcı kayıt defteri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c1f8a-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="c1f8a-109">Örneğin, hello kullan [Azure portal](container-registry-get-started-portal.md) veya hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c1f8a-109">For example, use hello [Azure portal](container-registry-get-started-portal.md) or hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="c1f8a-110">**Docker CLI** -tooset bir Docker ana bilgisayar ve erişim hello Docker CLI komutları olarak, yerel bilgisayarınıza yüklemek [Docker altyapısına](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="c1f8a-110">**Docker CLI** - tooset up your local computer as a Docker host and access hello Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>

## <a name="log-in-tooa-registry"></a><span data-ttu-id="c1f8a-111">Tooa kayıt defterinde oturum</span><span class="sxs-lookup"><span data-stu-id="c1f8a-111">Log in tooa registry</span></span>
<span data-ttu-id="c1f8a-112">Çalıştırma `docker login` ile tooyour kapsayıcı defterinde toolog, [kayıt defteri kimlik](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="c1f8a-112">Run `docker login` toolog in tooyour container registry with your [registry credentials](container-registry-authentication.md).</span></span>

<span data-ttu-id="c1f8a-113">Merhaba aşağıdaki örnek hello kimliği ve parolası bir Azure Active Directory geçirir [hizmet sorumlusu](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="c1f8a-113">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="c1f8a-114">Örneğin, bir hizmet asıl tooyour kayıt defteri bir Otomasyon senaryosu için atanmış.</span><span class="sxs-lookup"><span data-stu-id="c1f8a-114">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> <span data-ttu-id="c1f8a-115">Emin toospecify hello tam kayıt defteri adı (tümü küçük harf) olun.</span><span class="sxs-lookup"><span data-stu-id="c1f8a-115">Make sure toospecify hello fully qualified registry name (all lowercase).</span></span> <span data-ttu-id="c1f8a-116">Bu örnekte bu değer `myregistry.azurecr.io`’dur.</span><span class="sxs-lookup"><span data-stu-id="c1f8a-116">In this example, it is `myregistry.azurecr.io`.</span></span>

## <a name="steps-toopull-and-push-an-image"></a><span data-ttu-id="c1f8a-117">Adımları toopull ve anında iletme görüntü</span><span class="sxs-lookup"><span data-stu-id="c1f8a-117">Steps toopull and push an image</span></span>
<span data-ttu-id="c1f8a-118">Merhaba yüklemeleri hello ortak Docker hub'a kayıt defteri, Nginx görüntüden özel Azure kapsayıcı kaydınız için tooyour kayıt defteri iter, ardından yeniden çeker etiketleri hello örnek izleyin.</span><span class="sxs-lookup"><span data-stu-id="c1f8a-118">hello follow example downloads hello Nginx image from hello public Docker Hub registry, tags it for your private Azure container registry, pushes it tooyour registry, then pulls it again.</span></span>

<span data-ttu-id="c1f8a-119">**1. Merhaba Docker resmi görüntü için Nginx isteme**</span><span class="sxs-lookup"><span data-stu-id="c1f8a-119">**1. Pull hello Docker official image for Nginx**</span></span>

<span data-ttu-id="c1f8a-120">İlk çekme hello ortak Nginx görüntü tooyour yerel bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="c1f8a-120">First pull hello public Nginx image tooyour local computer.</span></span>

```
docker pull nginx
```
<span data-ttu-id="c1f8a-121">**2. Merhaba Nginx kapsayıcısı Başlat**</span><span class="sxs-lookup"><span data-stu-id="c1f8a-121">**2. Start hello Nginx container**</span></span>

<span data-ttu-id="c1f8a-122">Hello aşağıdaki komut hello yerel Nginx kapsayıcısı etkileşimli olarak Nginx toosee çıkışı sağlayan bağlantı noktası 8080 üzerinde başlatır.</span><span class="sxs-lookup"><span data-stu-id="c1f8a-122">hello following command starts hello local Nginx container interactively on port 8080, allowing you toosee output from Nginx.</span></span> <span data-ttu-id="c1f8a-123">Bir kez durduruldu kapsayıcı çalıştıran hello kaldırır.</span><span class="sxs-lookup"><span data-stu-id="c1f8a-123">It removes hello running container once stopped.</span></span>

```
docker run -it --rm -p 8080:80 nginx
```

<span data-ttu-id="c1f8a-124">Çok Gözat[http://localhost: 8080](http://localhost:8080) kapsayıcı çalıştıran tooview hello.</span><span class="sxs-lookup"><span data-stu-id="c1f8a-124">Browse too[http://localhost:8080](http://localhost:8080) tooview hello running container.</span></span> <span data-ttu-id="c1f8a-125">Bir aşağıdaki ekrana benzer toohello bakın.</span><span class="sxs-lookup"><span data-stu-id="c1f8a-125">You see a screen similar toohello following one.</span></span>

![Yerel bilgisayarda Nginx](./media/container-registry-get-started-docker-cli/nginx.png)

<span data-ttu-id="c1f8a-127">toostop çalışan kapsayıcı Merhaba, basın [CTRL] + [C].</span><span class="sxs-lookup"><span data-stu-id="c1f8a-127">toostop hello running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="c1f8a-128">**3. Merhaba görüntünün bir diğer ad, kayıt defterinde oluşturun**</span><span class="sxs-lookup"><span data-stu-id="c1f8a-128">**3. Create an alias of hello image in your registry**</span></span>

<span data-ttu-id="c1f8a-129">Merhaba aşağıdaki komutu bir diğer ad hello görüntünün tam nitelenmiş bir yol tooyour kayıt defteri ile oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c1f8a-129">hello following command creates an alias of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="c1f8a-130">Bu örnek hello belirtir `samples` hello kayıt defteri hello kök ad alanı tooavoid dağınıklığı.</span><span class="sxs-lookup"><span data-stu-id="c1f8a-130">This example specifies hello `samples` namespace tooavoid clutter in hello root of hello registry.</span></span>

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

<span data-ttu-id="c1f8a-131">**4. Anında iletme hello görüntü tooyour kayıt defteri**</span><span class="sxs-lookup"><span data-stu-id="c1f8a-131">**4. Push hello image tooyour registry**</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="c1f8a-132">**5. Çekme hello görüntü, kayıt defteri**</span><span class="sxs-lookup"><span data-stu-id="c1f8a-132">**5. Pull hello image from your registry**</span></span>

```
docker pull myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="c1f8a-133">**6. Kayıt defterinden Hello Nginx kapsayıcısı Başlat**</span><span class="sxs-lookup"><span data-stu-id="c1f8a-133">**6. Start hello Nginx container from your registry**</span></span>

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="c1f8a-134">Çok Gözat[http://localhost: 8080](http://localhost:8080) kapsayıcı çalıştıran tooview hello.</span><span class="sxs-lookup"><span data-stu-id="c1f8a-134">Browse too[http://localhost:8080](http://localhost:8080) tooview hello running container.</span></span>

<span data-ttu-id="c1f8a-135">toostop çalışan kapsayıcı Merhaba, basın [CTRL] + [C].</span><span class="sxs-lookup"><span data-stu-id="c1f8a-135">toostop hello running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="c1f8a-136">**7. (İsteğe bağlı) Merhaba görüntüsünü kaldırın**</span><span class="sxs-lookup"><span data-stu-id="c1f8a-136">**7. (Optional) Remove hello image**</span></span>

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a><span data-ttu-id="c1f8a-137">Eşzamanlı İşlem Limitleri</span><span class="sxs-lookup"><span data-stu-id="c1f8a-137">Concurrent Limits</span></span>
<span data-ttu-id="c1f8a-138">Bazı senaryolarda çağrıların eşzamanlı olarak yürütülmesi hatalara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="c1f8a-138">In some scenarios, executing calls concurrently might result in errors.</span></span> <span data-ttu-id="c1f8a-139">Aşağıdaki tablonun hello Azure kapsayıcı kayıt defteri "Gönderme" ve "Çekme" işlemlerini ile eşzamanlı çağrıları hello sınırları içerir:</span><span class="sxs-lookup"><span data-stu-id="c1f8a-139">hello following table contains hello limits of concurrent calls with "Push" and "Pull" operations on Azure container registry:</span></span>

| <span data-ttu-id="c1f8a-140">İşlem</span><span class="sxs-lookup"><span data-stu-id="c1f8a-140">Operation</span></span>  | <span data-ttu-id="c1f8a-141">Sınır</span><span class="sxs-lookup"><span data-stu-id="c1f8a-141">Limit</span></span>                                  |
| ---------- | -------------------------------------- |
| <span data-ttu-id="c1f8a-142">PULL</span><span class="sxs-lookup"><span data-stu-id="c1f8a-142">PULL</span></span>       | <span data-ttu-id="c1f8a-143">Kayıt defteri too10 eşzamanlı çeker</span><span class="sxs-lookup"><span data-stu-id="c1f8a-143">Up too10 concurrent pulls per registry</span></span> |
| <span data-ttu-id="c1f8a-144">PUSH</span><span class="sxs-lookup"><span data-stu-id="c1f8a-144">PUSH</span></span>       | <span data-ttu-id="c1f8a-145">Kayıt defteri too5 eşzamanlı iter</span><span class="sxs-lookup"><span data-stu-id="c1f8a-145">Up too5 concurrent pushes per registry</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c1f8a-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c1f8a-146">Next steps</span></span>
<span data-ttu-id="c1f8a-147">Merhaba temelleri bildiğinize göre kayıt defterini kullanarak hazır toostart olduğunuz!</span><span class="sxs-lookup"><span data-stu-id="c1f8a-147">Now that you know hello basics, you are ready toostart using your registry!</span></span> <span data-ttu-id="c1f8a-148">Örneğin, kapsayıcı görüntüleri tooan dağıtmaya başlamadan [Azure kapsayıcı hizmeti](https://azure.microsoft.com/documentation/services/container-service/) küme.</span><span class="sxs-lookup"><span data-stu-id="c1f8a-148">For example, start deploying container images tooan [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
