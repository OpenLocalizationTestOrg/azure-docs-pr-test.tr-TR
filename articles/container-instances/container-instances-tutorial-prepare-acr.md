---
title: "aaaAzure kapsayıcı örnekleri öğretici - Azure kapsayıcı kayıt defteri hazırlama | Microsoft Docs"
description: "Azure kapsayıcı örnekleri Öğreticisi - Azure kapsayıcı kayıt defteri hazırlama"
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Container’lar, Mikro hizmetler, Kumernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2525626125740c3c861fad36aad207d0b587ff54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="48068-104">Dağıtma ve Azure kapsayıcı kayıt defteri kullanma</span><span class="sxs-lookup"><span data-stu-id="48068-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="48068-105">Bu iki üç bölümlü öğretici parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="48068-105">This is part two of a three-part tutorial.</span></span> <span data-ttu-id="48068-106">Merhaba, [önceki adımda](./container-instances-tutorial-prepare-app.md), yazılan basit bir web uygulaması için bir kapsayıcı görüntüsü oluşturuldu [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="48068-106">In hello [previous step](./container-instances-tutorial-prepare-app.md), a container image was created for a simple web application written in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="48068-107">Bu öğreticide, bu görüntüyü tooan Azure kapsayıcı kayıt defteri gönderilir.</span><span class="sxs-lookup"><span data-stu-id="48068-107">In this tutorial, this image is pushed tooan Azure Container Registry.</span></span> <span data-ttu-id="48068-108">Merhaba kapsayıcı görüntü oluşturmadıysanız çok dönüş[Öğreticisi 1 – Oluştur kapsayıcı görüntü](./container-instances-tutorial-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="48068-108">If you have not created hello container image, return too[Tutorial 1 – Create container image](./container-instances-tutorial-prepare-app.md).</span></span> 

<span data-ttu-id="48068-109">Hello Azure kapsayıcı kayıt defteri Docker kapsayıcısı görüntüleri için bir Azure tabanlı, özel kayıt defteri ' dir.</span><span class="sxs-lookup"><span data-stu-id="48068-109">hello Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="48068-110">Bu öğreticide, Azure kapsayıcı kayıt defteri örneğini dağıtma ve kapsayıcı görüntü tooit Ftp'den aracılığıyla açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="48068-110">This tutorial walks through deploying an Azure Container Registry instance, and pushing a container image tooit.</span></span> <span data-ttu-id="48068-111">Tamamlanan adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="48068-111">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="48068-112">Azure kapsayıcı kayıt defteri örneğini dağıtma</span><span class="sxs-lookup"><span data-stu-id="48068-112">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="48068-113">Azure kapsayıcı kayıt defteri için etiketleme kapsayıcı görüntüsü</span><span class="sxs-lookup"><span data-stu-id="48068-113">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="48068-114">Görüntü tooAzure kapsayıcı kayıt defteri karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="48068-114">Uploading image tooAzure Container Registry</span></span>

<span data-ttu-id="48068-115">Sonraki öğreticilerde özel kayıt defteri tooAzure kapsayıcı örnekleri hello kapsayıcı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="48068-115">In subsequent tutorials, you deploy hello container from your private registry tooAzure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="48068-116">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="48068-116">Before you begin</span></span>

<span data-ttu-id="48068-117">Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırdığınız gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="48068-117">This tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="48068-118">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="48068-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="48068-119">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="48068-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="48068-120">Azure kapsayıcı kayıt defteri dağıtın</span><span class="sxs-lookup"><span data-stu-id="48068-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="48068-121">Azure kapsayıcı kayıt defteri dağıtırken, önce bir kaynak grubu gerekir.</span><span class="sxs-lookup"><span data-stu-id="48068-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="48068-122">Bir Azure kaynak grubu hangi Azure kaynakları dağıtılan yönetilen ve mantıksal bir koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="48068-122">An Azure resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="48068-123">Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="48068-123">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="48068-124">Bu örnekte, bir kaynak grubu adında *myResourceGroup* hello oluşturulan *eastus* bölge.</span><span class="sxs-lookup"><span data-stu-id="48068-124">In this example, a resource group named *myResourceGroup* is created in hello *eastus* region.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="48068-125">Azure kapsayıcı kayıt defteri ile Merhaba oluşturma [az acr oluşturmak](/cli/azure/acr#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="48068-125">Create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="48068-126">bir kapsayıcı kayıt defteri Hello adını **benzersiz olmalıdır**.</span><span class="sxs-lookup"><span data-stu-id="48068-126">hello name of a Container Registry **must be unique**.</span></span> <span data-ttu-id="48068-127">Aşağıdaki örneğine hello kullanırız hello adı *mycontainerregistry082*.</span><span class="sxs-lookup"><span data-stu-id="48068-127">In hello following example, we use hello name *mycontainerregistry082*.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name mycontainerregistry082 --sku Basic --admin-enabled true
```

<span data-ttu-id="48068-128">Hello rest Bu öğreticinin kullanırız `<acrname>` seçtiğiniz hello kapsayıcı kayıt defteri adı için bir yer tutucu olarak.</span><span class="sxs-lookup"><span data-stu-id="48068-128">Throughout hello rest of this tutorial, we use `<acrname>` as a placeholder for hello container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="48068-129">Kapsayıcı kayıt defteri oturum açma</span><span class="sxs-lookup"><span data-stu-id="48068-129">Container registry login</span></span>

<span data-ttu-id="48068-130">Görüntüleri tooit göndermeden önce tooyour ACR örneğinde oturum açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="48068-130">You must log in tooyour ACR instance before pushing images tooit.</span></span> <span data-ttu-id="48068-131">Kullanım hello [az acr oturum açma](https://docs.microsoft.com/en-us/cli/azure/acr#login) toocomplete hello işlemi komutu.</span><span class="sxs-lookup"><span data-stu-id="48068-131">Use hello [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command toocomplete hello operation.</span></span> <span data-ttu-id="48068-132">Oluşturulduğunda toohello kapsayıcı kayıt defteri verilen tooprovide hello benzersiz adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="48068-132">You need tooprovide hello unique name given toohello container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="48068-133">Merhaba komut tamamlandıktan sonra 'Başarılı oturum açma' iletisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="48068-133">hello command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-image"></a><span data-ttu-id="48068-134">Etiket kapsayıcı görüntüsü</span><span class="sxs-lookup"><span data-stu-id="48068-134">Tag container image</span></span>

<span data-ttu-id="48068-135">özel bir kayıt defteri kapsayıcı görüntüden toodeploy, hello görüntü gerekiyor hello ile etiketlenmiş toobe `loginServer` hello kayıt adı.</span><span class="sxs-lookup"><span data-stu-id="48068-135">toodeploy a container image from a private registry, hello image needs toobe tagged with hello `loginServer` name of hello registry.</span></span>

<span data-ttu-id="48068-136">toosee geçerli görüntüleri, kullanım hello listesini `docker images` komutu.</span><span class="sxs-lookup"><span data-stu-id="48068-136">toosee a list of current images, use hello `docker images` command.</span></span>

```bash
docker images
```

<span data-ttu-id="48068-137">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="48068-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

<span data-ttu-id="48068-138">komutu aşağıdaki hello çalıştırmak tooget hello loginServer adı.</span><span class="sxs-lookup"><span data-stu-id="48068-138">tooget hello loginServer name, run hello following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="48068-139">Etiket hello *aci öğretici uygulama* hello loginServer hello kapsayıcı kayıt defteri görüntüsüyle.</span><span class="sxs-lookup"><span data-stu-id="48068-139">Tag hello *aci-tutorial-app* image with hello loginServer of hello container registry.</span></span> <span data-ttu-id="48068-140">Ayrıca, ekleme `:v1` toohello adının sonuna kadar hello görüntü.</span><span class="sxs-lookup"><span data-stu-id="48068-140">Also, add `:v1` toohello end of hello image name.</span></span> <span data-ttu-id="48068-141">Bu etiket hello görüntü sürüm numarasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="48068-141">This tag indicates hello image version number.</span></span>

```bash
docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1
```

<span data-ttu-id="48068-142">Etiketlenmiş bir kez çalıştır `docker images` tooverify hello işlemi.</span><span class="sxs-lookup"><span data-stu-id="48068-142">Once tagged, run `docker images` tooverify hello operation.</span></span>

```bash
docker images
```

<span data-ttu-id="48068-143">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="48068-143">Output:</span></span>

```bash
REPOSITORY                                                TAG                 IMAGE ID            CREATED             SIZE
aci-tutorial-app                                          latest              5c745774dfa9        39 seconds ago      68.1 MB
mycontainerregistry082.azurecr.io/aci-tutorial-app        v1                  a9dace4e1a17        7 minutes ago       68.1 MB
```

## <a name="push-image-tooazure-container-registry"></a><span data-ttu-id="48068-144">Anında iletme görüntü tooAzure kapsayıcı kayıt defteri</span><span class="sxs-lookup"><span data-stu-id="48068-144">Push image tooAzure Container Registry</span></span>

<span data-ttu-id="48068-145">Merhaba anında *aci öğretici uygulama* görüntü toohello kayıt defteri.</span><span class="sxs-lookup"><span data-stu-id="48068-145">Push hello *aci-tutorial-app* image toohello registry.</span></span>

<span data-ttu-id="48068-146">Aşağıdaki örneğine hello kullanarak, ortamınızdan hello loginServer hello kapsayıcı kayıt defteri loginServer adı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="48068-146">Using hello following example, replace hello container registry loginServer name with hello loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/aci-tutorial-app:v1
```

## <a name="list-images-in-azure-container-registry"></a><span data-ttu-id="48068-147">Azure kapsayıcı kayıt defterinde listesi görüntüler</span><span class="sxs-lookup"><span data-stu-id="48068-147">List images in Azure Container Registry</span></span>

<span data-ttu-id="48068-148">tooreturn tooyour Azure kapsayıcı kayıt defteri, kullanıcı hello gönderilen görüntüleri listesini [az acr deposu listesi](/cli/azure/acr/repository#list) komutu.</span><span class="sxs-lookup"><span data-stu-id="48068-148">tooreturn a list of images that have been pushed tooyour Azure Container registry, user hello [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="48068-149">Merhaba komutu hello kapsayıcı kayıt defteri adıyla güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="48068-149">Update hello command with hello container registry name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="48068-150">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="48068-150">Output:</span></span>

```azurecli
Result
----------------
aci-tutorial-app
```

<span data-ttu-id="48068-151">Ve ardından belirli bir görüntü için toosee hello etiketler hello [az acr deposunu Göster-etiketleri](/cli/azure/acr/repository#show-tags) komutu.</span><span class="sxs-lookup"><span data-stu-id="48068-151">And then toosee hello tags for a specific image, use hello [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository aci-tutorial-app --output table
```

<span data-ttu-id="48068-152">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="48068-152">Output:</span></span>

```azurecli
Result
--------
v1
```

## <a name="next-steps"></a><span data-ttu-id="48068-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="48068-153">Next steps</span></span>

<span data-ttu-id="48068-154">Bu öğreticide Azure kapsayıcı örnekleri ile kullanmak için bir Azure kapsayıcı kayıt defteri hazırlanan ve hello kapsayıcı görüntü gönderilir.</span><span class="sxs-lookup"><span data-stu-id="48068-154">In this tutorial, an Azure Container Registry was prepared for use with Azure Container Instances, and hello container image was pushed.</span></span> <span data-ttu-id="48068-155">Aşağıdaki adımları hello tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="48068-155">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="48068-156">Azure kapsayıcı kayıt defteri örneğini dağıtma</span><span class="sxs-lookup"><span data-stu-id="48068-156">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="48068-157">Azure kapsayıcı kayıt defteri için etiketleme kapsayıcı görüntüsü</span><span class="sxs-lookup"><span data-stu-id="48068-157">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="48068-158">Görüntü tooAzure kapsayıcı kayıt defteri karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="48068-158">Uploading image tooAzure Container Registry</span></span>

<span data-ttu-id="48068-159">Azure kapsayıcı örnekleri kullanılarak hello kapsayıcı tooAzure dağıtma hakkında toohello sonraki öğretici toolearn ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="48068-159">Advance toohello next tutorial toolearn about deploying hello container tooAzure using Azure Container Instances.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="48068-160">Kapsayıcıları tooAzure kapsayıcı örnekleri dağıtma</span><span class="sxs-lookup"><span data-stu-id="48068-160">Deploy containers tooAzure Container Instances</span></span>](./container-instances-tutorial-deploy-app.md)
