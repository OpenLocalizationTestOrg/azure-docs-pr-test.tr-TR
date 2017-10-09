---
title: "aaaAzure kapsayıcı hizmeti Öğreticisi - hazırlama ACR | Microsoft Docs"
description: "Azure kapsayıcı hizmeti Öğreticisi - ACR hazırlama"
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
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 3980e5ce4eb9836f83c761a2f76c944bb3f13060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="d45fb-104">Dağıtma ve Azure kapsayıcı kayıt defteri kullanma</span><span class="sxs-lookup"><span data-stu-id="d45fb-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="d45fb-105">Azure kapsayıcı kayıt defteri (ACR) Docker kapsayıcısı görüntüleri için bir Azure tabanlı, özel kayıt defteri ' dir.</span><span class="sxs-lookup"><span data-stu-id="d45fb-105">Azure Container Registry (ACR) is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="d45fb-106">Bu öğretici, bölümü yedi, iki anlatılmaktadır Azure kapsayıcı kayıt defteri örneğini dağıtma ve kapsayıcı görüntü tooit Ftp'den aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="d45fb-106">This tutorial, part two of seven, walks through deploying an Azure Container Registry instance, and pushing a container image tooit.</span></span> <span data-ttu-id="d45fb-107">Tamamlanan adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="d45fb-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d45fb-108">Azure kapsayıcı kayıt defteri (ACR) örneğini dağıtma</span><span class="sxs-lookup"><span data-stu-id="d45fb-108">Deploying an Azure Container Registry (ACR) instance</span></span>
> * <span data-ttu-id="d45fb-109">ACR için bir kapsayıcı görüntüsü etiketleme</span><span class="sxs-lookup"><span data-stu-id="d45fb-109">Tagging a container image for ACR</span></span>
> * <span data-ttu-id="d45fb-110">Merhaba görüntü tooACR karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="d45fb-110">Uploading hello image tooACR</span></span>

<span data-ttu-id="d45fb-111">Sonraki öğreticilerde bu ACR örnek kapsayıcı görüntüleri güvenli bir şekilde çalıştırmak için bir Azure kapsayıcı hizmeti Kubernetes küme tümleşiktir.</span><span class="sxs-lookup"><span data-stu-id="d45fb-111">In subsequent tutorials, this ACR instance is integrated with an Azure Container Service Kubernetes cluster, for securely running container images.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="d45fb-112">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="d45fb-112">Before you begin</span></span>

<span data-ttu-id="d45fb-113">Merhaba, [önceki öğretici](./container-service-tutorial-kubernetes-prepare-app.md), basit bir Azure oylama uygulaması için bir kapsayıcı görüntüsü oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="d45fb-113">In hello [previous tutorial](./container-service-tutorial-kubernetes-prepare-app.md), a container image was created for a simple Azure Voting application.</span></span> <span data-ttu-id="d45fb-114">Bu öğreticide, bu görüntüyü tooan Azure kapsayıcı kayıt defteri gönderilir.</span><span class="sxs-lookup"><span data-stu-id="d45fb-114">In this tutorial, this image is pushed tooan Azure Container Registry.</span></span> <span data-ttu-id="d45fb-115">Hello Azure oylama uygulama görüntüsü oluşturmadıysanız çok dönüş[Öğreticisi 1 – Oluştur kapsayıcı görüntüleri](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="d45fb-115">If you have not created hello Azure Voting app image, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> <span data-ttu-id="d45fb-116">Alternatif olarak, hello adımlar burada herhangi bir kapsayıcı görüntü ile çalışma ayrıntılı.</span><span class="sxs-lookup"><span data-stu-id="d45fb-116">Alternatively, hello steps detailed here work with any container image.</span></span>

<span data-ttu-id="d45fb-117">Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırdığınız gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="d45fb-117">This tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="d45fb-118">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="d45fb-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d45fb-119">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d45fb-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="d45fb-120">Azure kapsayıcı kayıt defteri dağıtın</span><span class="sxs-lookup"><span data-stu-id="d45fb-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="d45fb-121">Azure kapsayıcı kayıt defteri dağıtırken, önce bir kaynak grubu gerekir.</span><span class="sxs-lookup"><span data-stu-id="d45fb-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="d45fb-122">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="d45fb-122">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="d45fb-123">Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="d45fb-123">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="d45fb-124">Bu örnekte, bir kaynak grubu adında *myResourceGroup* hello oluşturulan *westeurope* bölge.</span><span class="sxs-lookup"><span data-stu-id="d45fb-124">In this example, a resource group named *myResourceGroup* is created in hello *westeurope* region.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="d45fb-125">Azure kapsayıcı kayıt defteri ile Merhaba oluşturma [az acr oluşturmak](/cli/azure/acr#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="d45fb-125">Create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="d45fb-126">bir kapsayıcı kayıt defteri Hello adını **benzersiz olmalıdır**.</span><span class="sxs-lookup"><span data-stu-id="d45fb-126">hello name of a Container Registry **must be unique**.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

<span data-ttu-id="d45fb-127">Hello rest Bu öğreticinin "acrname" yer tutucu olarak seçtiğiniz hello kapsayıcı kayıt defteri adı için kullanırız.</span><span class="sxs-lookup"><span data-stu-id="d45fb-127">Throughout hello rest of this tutorial, we use "acrname" as a placeholder for hello container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="d45fb-128">Kapsayıcı kayıt defteri oturum açma</span><span class="sxs-lookup"><span data-stu-id="d45fb-128">Container registry login</span></span>

<span data-ttu-id="d45fb-129">Görüntüleri tooit göndermeden önce tooyour ACR örneğinde oturum açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d45fb-129">You must log in tooyour ACR instance before pushing images tooit.</span></span> <span data-ttu-id="d45fb-130">Kullanım hello [az acr oturum açma](https://docs.microsoft.com/en-us/cli/azure/acr#login) toocomplete hello işlemi komutu.</span><span class="sxs-lookup"><span data-stu-id="d45fb-130">Use hello [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command toocomplete hello operation.</span></span> <span data-ttu-id="d45fb-131">Oluşturulduğunda toohello kapsayıcı kayıt defteri verilen tooprovide hello benzersiz adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="d45fb-131">You need tooprovide hello unique name given toohello container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="d45fb-132">Merhaba komut tamamlandıktan sonra 'Başarılı oturum açma' iletisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="d45fb-132">hello command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-images"></a><span data-ttu-id="d45fb-133">Etiket kapsayıcı görüntüleri</span><span class="sxs-lookup"><span data-stu-id="d45fb-133">Tag container images</span></span>

<span data-ttu-id="d45fb-134">Her kapsayıcı görüntü hello loginServer adı hello kayıt defteri ile etiketlenmiş toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="d45fb-134">Each container image needs toobe tagged with hello loginServer name of hello registry.</span></span> <span data-ttu-id="d45fb-135">Bu etiket kapsayıcı görüntüleri tooan görüntü kayıt defteri Ftp'den zaman yönlendirme için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d45fb-135">This tag is used for routing when pushing container images tooan image registry.</span></span>

<span data-ttu-id="d45fb-136">toosee geçerli görüntüleri, kullanım hello listesini [docker görüntüleri](https://docs.docker.com/engine/reference/commandline/images/) komutu.</span><span class="sxs-lookup"><span data-stu-id="d45fb-136">toosee a list of current images, use hello [docker images](https://docs.docker.com/engine/reference/commandline/images/) command.</span></span>

```bash
docker images
```

<span data-ttu-id="d45fb-137">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="d45fb-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="d45fb-138">komutu aşağıdaki hello çalıştırmak tooget hello loginServer adı.</span><span class="sxs-lookup"><span data-stu-id="d45fb-138">tooget hello loginServer name, run hello following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="d45fb-139">Şimdi, etiket hello *azure oy ön* hello loginServer hello kapsayıcı kayıt defteri görüntüsüyle.</span><span class="sxs-lookup"><span data-stu-id="d45fb-139">Now, tag hello *azure-vote-front* image with hello loginServer of hello container registry.</span></span> <span data-ttu-id="d45fb-140">Ayrıca, ekleme `:redis-v1` toohello adının sonuna kadar hello görüntü.</span><span class="sxs-lookup"><span data-stu-id="d45fb-140">Also, add `:redis-v1` toohello end of hello image name.</span></span> <span data-ttu-id="d45fb-141">Bu etiket hello resim sürümünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="d45fb-141">This tag indicates hello image version.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="d45fb-142">Etiketli sonra [docker görüntüler] (https://docs.docker.com/engine/reference/commandline/images/) tooverify hello işlemini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d45fb-142">Once tagged, run [docker images] (https://docs.docker.com/engine/reference/commandline/images/) tooverify hello operation.</span></span>

```bash
docker images
```

<span data-ttu-id="d45fb-143">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="d45fb-143">Output:</span></span>

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-tooregistry"></a><span data-ttu-id="d45fb-144">Görüntüleri tooregistry bildirme</span><span class="sxs-lookup"><span data-stu-id="d45fb-144">Push images tooregistry</span></span>

<span data-ttu-id="d45fb-145">Merhaba anında *azure oy ön* görüntü toohello kayıt defteri.</span><span class="sxs-lookup"><span data-stu-id="d45fb-145">Push hello *azure-vote-front* image toohello registry.</span></span> 

<span data-ttu-id="d45fb-146">Aşağıdaki örneğine hello kullanarak, ortamınızdan hello loginServer hello ACR loginServer adı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d45fb-146">Using hello following example, replace hello ACR loginServer name with hello loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="d45fb-147">Bu işlem birkaç dakika toocomplete götürür.</span><span class="sxs-lookup"><span data-stu-id="d45fb-147">This takes a couple of minutes toocomplete.</span></span>

## <a name="list-images-in-registry"></a><span data-ttu-id="d45fb-148">Kayıt defterinde listesi görüntüler</span><span class="sxs-lookup"><span data-stu-id="d45fb-148">List images in registry</span></span>

<span data-ttu-id="d45fb-149">tooreturn tooyour Azure kapsayıcı kayıt defteri, kullanıcı hello gönderilen görüntüleri listesini [az acr deposu listesi](/cli/azure/acr/repository#list) komutu.</span><span class="sxs-lookup"><span data-stu-id="d45fb-149">tooreturn a list of images that have been pushed tooyour Azure Container registry, user hello [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="d45fb-150">Merhaba komutu hello ACR örnek adıyla güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d45fb-150">Update hello command with hello ACR instance name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="d45fb-151">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="d45fb-151">Output:</span></span>

```azurecli
Result
----------------
azure-vote-front
```

<span data-ttu-id="d45fb-152">Ve ardından belirli bir görüntü için toosee hello etiketler hello [az acr deposunu Göster-etiketleri](/cli/azure/acr/repository#show-tags) komutu.</span><span class="sxs-lookup"><span data-stu-id="d45fb-152">And then toosee hello tags for a specific image, use hello [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

<span data-ttu-id="d45fb-153">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="d45fb-153">Output:</span></span>

```azurecli
Result
--------
redis-v1
```

<span data-ttu-id="d45fb-154">Eğitmen tamamlandığında hello kapsayıcı görüntü özel bir Azure kapsayıcı kayıt defteri örneğinde zamandır depolanmış.</span><span class="sxs-lookup"><span data-stu-id="d45fb-154">At tutorial completion, hello container image has been stored in a private Azure Container Registry instance.</span></span> <span data-ttu-id="d45fb-155">Bu görüntü ACR tooa Kubernetes kümeden sonraki öğreticilerde dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="d45fb-155">This image is deployed from ACR tooa Kubernetes cluster in subsequent tutorials.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d45fb-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d45fb-156">Next steps</span></span>

<span data-ttu-id="d45fb-157">Bu öğreticide, bir ACS Kubernetes kümesinde kullanmak için bir Azure kapsayıcı kayıt defteri hazırlanan.</span><span class="sxs-lookup"><span data-stu-id="d45fb-157">In this tutorial, an Azure Container Registry was prepared for use in an ACS Kubernetes cluster.</span></span> <span data-ttu-id="d45fb-158">Aşağıdaki adımları hello tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="d45fb-158">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d45fb-159">Azure kapsayıcı kayıt defteri örneği dağıtılan</span><span class="sxs-lookup"><span data-stu-id="d45fb-159">Deployed an Azure Container Registry instance</span></span>
> * <span data-ttu-id="d45fb-160">ACR için bir kapsayıcı görüntüsü etiketli</span><span class="sxs-lookup"><span data-stu-id="d45fb-160">Tagged a container image for ACR</span></span>
> * <span data-ttu-id="d45fb-161">Karşıya yüklenen hello görüntü tooACR</span><span class="sxs-lookup"><span data-stu-id="d45fb-161">Uploaded hello image tooACR</span></span>

<span data-ttu-id="d45fb-162">Azure Kubernetes kümede dağıtma hakkında toohello sonraki öğretici toolearn ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="d45fb-162">Advance toohello next tutorial toolearn about deploying a Kubernetes cluster in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d45fb-163">Kubernetes kümesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="d45fb-163">Deploy Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-deploy-cluster.md)