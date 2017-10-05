---
title: "Azure kapsayıcı örnekleri Öğreticisi - Azure kapsayıcı kayıt defteri hazırlama | Microsoft Docs"
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
ms.openlocfilehash: cc96ba9f5abd45a7503ba3327b30e1f809391384
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="7c59d-104">Dağıtma ve Azure kapsayıcı kayıt defteri kullanma</span><span class="sxs-lookup"><span data-stu-id="7c59d-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="7c59d-105">Bu iki üç bölümlü öğretici parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="7c59d-105">This is part two of a three-part tutorial.</span></span> <span data-ttu-id="7c59d-106">İçinde [önceki adımda](./container-instances-tutorial-prepare-app.md), yazılan basit bir web uygulaması için bir kapsayıcı görüntüsü oluşturuldu [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="7c59d-106">In the [previous step](./container-instances-tutorial-prepare-app.md), a container image was created for a simple web application written in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="7c59d-107">Bu öğreticide, Azure kapsayıcı kayıt defterine bu görüntüyü gönderilir.</span><span class="sxs-lookup"><span data-stu-id="7c59d-107">In this tutorial, this image is pushed to an Azure Container Registry.</span></span> <span data-ttu-id="7c59d-108">Kapsayıcı görüntü oluşturmadıysanız, geri dönüp [Öğreticisi 1 – Oluştur kapsayıcı görüntü](./container-instances-tutorial-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="7c59d-108">If you have not created the container image, return to [Tutorial 1 – Create container image](./container-instances-tutorial-prepare-app.md).</span></span> 

<span data-ttu-id="7c59d-109">Azure kapsayıcı kayıt defteri Docker kapsayıcısı görüntüleri için bir Azure tabanlı, özel kayıt defteri ' dir.</span><span class="sxs-lookup"><span data-stu-id="7c59d-109">The Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="7c59d-110">Bu öğreticide Azure kapsayıcı kayıt defteri örneğini dağıtma ve kapsayıcı görüntü için itme açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7c59d-110">This tutorial walks through deploying an Azure Container Registry instance, and pushing a container image to it.</span></span> <span data-ttu-id="7c59d-111">Tamamlanan adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="7c59d-111">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7c59d-112">Azure kapsayıcı kayıt defteri örneğini dağıtma</span><span class="sxs-lookup"><span data-stu-id="7c59d-112">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="7c59d-113">Azure kapsayıcı kayıt defteri için etiketleme kapsayıcı görüntüsü</span><span class="sxs-lookup"><span data-stu-id="7c59d-113">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="7c59d-114">Azure kapsayıcı kayıt defterine görüntüyü karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="7c59d-114">Uploading image to Azure Container Registry</span></span>

<span data-ttu-id="7c59d-115">Sonraki öğreticilerde, kapsayıcı Azure kapsayıcı örnekleri özel kayıt defterinden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="7c59d-115">In subsequent tutorials, you deploy the container from your private registry to Azure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7c59d-116">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="7c59d-116">Before you begin</span></span>

<span data-ttu-id="7c59d-117">Bu öğretici, Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="7c59d-117">This tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="7c59d-118">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7c59d-118">Run `az --version` to find the version.</span></span> <span data-ttu-id="7c59d-119">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7c59d-119">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="7c59d-120">Azure kapsayıcı kayıt defteri dağıtın</span><span class="sxs-lookup"><span data-stu-id="7c59d-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="7c59d-121">Azure kapsayıcı kayıt defteri dağıtırken, önce bir kaynak grubu gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c59d-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="7c59d-122">Bir Azure kaynak grubu hangi Azure kaynakları dağıtılan yönetilen ve mantıksal bir koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="7c59d-122">An Azure resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="7c59d-123">[az group create](/cli/azure/group#create) komutuyla bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7c59d-123">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="7c59d-124">Bu örnekte, bir kaynak grubu adında *myResourceGroup* oluşturulan *eastus* bölge.</span><span class="sxs-lookup"><span data-stu-id="7c59d-124">In this example, a resource group named *myResourceGroup* is created in the *eastus* region.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="7c59d-125">Azure kapsayıcı kayıt defteri ile oluşturma [az acr oluşturmak](/cli/azure/acr#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="7c59d-125">Create an Azure Container registry with the [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="7c59d-126">Bir kapsayıcı kayıt defteri adını **benzersiz olmalıdır**.</span><span class="sxs-lookup"><span data-stu-id="7c59d-126">The name of a Container Registry **must be unique**.</span></span> <span data-ttu-id="7c59d-127">Aşağıdaki örnekte, kullanırız adı *mycontainerregistry082*.</span><span class="sxs-lookup"><span data-stu-id="7c59d-127">In the following example, we use the name *mycontainerregistry082*.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name mycontainerregistry082 --sku Basic --admin-enabled true
```

<span data-ttu-id="7c59d-128">Bu öğreticinin geri kalanını, kullandığımız `<acrname>` seçtiğiniz kapsayıcı kayıt defteri adı için bir yer tutucu olarak.</span><span class="sxs-lookup"><span data-stu-id="7c59d-128">Throughout the rest of this tutorial, we use `<acrname>` as a placeholder for the container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="7c59d-129">Kapsayıcı kayıt defteri oturum açma</span><span class="sxs-lookup"><span data-stu-id="7c59d-129">Container registry login</span></span>

<span data-ttu-id="7c59d-130">ACR örneğinizi görüntüleri göndermeden önce oturum gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c59d-130">You must log in to your ACR instance before pushing images to it.</span></span> <span data-ttu-id="7c59d-131">Kullanım [az acr oturum açma](https://docs.microsoft.com/en-us/cli/azure/acr#login) işlemi tamamlamak için komutu.</span><span class="sxs-lookup"><span data-stu-id="7c59d-131">Use the [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command to complete the operation.</span></span> <span data-ttu-id="7c59d-132">Kapsayıcı kayıt defterine oluşturulduğunda verilen benzersiz bir ad vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c59d-132">You need to provide the unique name given to the container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="7c59d-133">Komut tamamlandıktan sonra 'Başarılı oturum açma' iletisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="7c59d-133">The command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-image"></a><span data-ttu-id="7c59d-134">Etiket kapsayıcı görüntüsü</span><span class="sxs-lookup"><span data-stu-id="7c59d-134">Tag container image</span></span>

<span data-ttu-id="7c59d-135">Özel bir kayıt defteri kapsayıcı görüntü dağıtmak için görüntü ile etiketlenmesi gereken `loginServer` kayıt adı.</span><span class="sxs-lookup"><span data-stu-id="7c59d-135">To deploy a container image from a private registry, the image needs to be tagged with the `loginServer` name of the registry.</span></span>

<span data-ttu-id="7c59d-136">Geçerli görüntüleri listesini görmek için `docker images` komutu.</span><span class="sxs-lookup"><span data-stu-id="7c59d-136">To see a list of current images, use the `docker images` command.</span></span>

```bash
docker images
```

<span data-ttu-id="7c59d-137">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="7c59d-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

<span data-ttu-id="7c59d-138">LoginServer adını almak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7c59d-138">To get the loginServer name, run the following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="7c59d-139">Etiket *aci öğretici uygulama* kapsayıcı kayıt defteri loginServer görüntüsüyle.</span><span class="sxs-lookup"><span data-stu-id="7c59d-139">Tag the *aci-tutorial-app* image with the loginServer of the container registry.</span></span> <span data-ttu-id="7c59d-140">Ayrıca, ekleme `:v1` sonuna kadar görüntü adı.</span><span class="sxs-lookup"><span data-stu-id="7c59d-140">Also, add `:v1` to the end of the image name.</span></span> <span data-ttu-id="7c59d-141">Bu etiket görüntü sürüm numarasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="7c59d-141">This tag indicates the image version number.</span></span>

```bash
docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1
```

<span data-ttu-id="7c59d-142">Etiketlenmiş bir kez çalıştır `docker images` işlemi doğrulamak için.</span><span class="sxs-lookup"><span data-stu-id="7c59d-142">Once tagged, run `docker images` to verify the operation.</span></span>

```bash
docker images
```

<span data-ttu-id="7c59d-143">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="7c59d-143">Output:</span></span>

```bash
REPOSITORY                                                TAG                 IMAGE ID            CREATED             SIZE
aci-tutorial-app                                          latest              5c745774dfa9        39 seconds ago      68.1 MB
mycontainerregistry082.azurecr.io/aci-tutorial-app        v1                  a9dace4e1a17        7 minutes ago       68.1 MB
```

## <a name="push-image-to-azure-container-registry"></a><span data-ttu-id="7c59d-144">Azure kapsayıcı kayıt defterine görüntü gönderme</span><span class="sxs-lookup"><span data-stu-id="7c59d-144">Push image to Azure Container Registry</span></span>

<span data-ttu-id="7c59d-145">Anında *aci öğretici uygulama* kayıt defterine görüntü.</span><span class="sxs-lookup"><span data-stu-id="7c59d-145">Push the *aci-tutorial-app* image to the registry.</span></span>

<span data-ttu-id="7c59d-146">Aşağıdaki örneği kullanarak, ortamınızdan loginServer kapsayıcı kayıt defteri loginServer adını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7c59d-146">Using the following example, replace the container registry loginServer name with the loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/aci-tutorial-app:v1
```

## <a name="list-images-in-azure-container-registry"></a><span data-ttu-id="7c59d-147">Azure kapsayıcı kayıt defterinde listesi görüntüler</span><span class="sxs-lookup"><span data-stu-id="7c59d-147">List images in Azure Container Registry</span></span>

<span data-ttu-id="7c59d-148">Azure kapsayıcı kaydınız gönderilen görüntüleri listesini döndürmek için kullanıcı [az acr deposu listesi](/cli/azure/acr/repository#list) komutu.</span><span class="sxs-lookup"><span data-stu-id="7c59d-148">To return a list of images that have been pushed to your Azure Container registry, user the [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="7c59d-149">Komut kapsayıcı kayıt defteri adıyla güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="7c59d-149">Update the command with the container registry name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="7c59d-150">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="7c59d-150">Output:</span></span>

```azurecli
Result
----------------
aci-tutorial-app
```

<span data-ttu-id="7c59d-151">Ve ardından belirli bir resim için etiketleri görmek için [az acr deposunu Göster-etiketleri](/cli/azure/acr/repository#show-tags) komutu.</span><span class="sxs-lookup"><span data-stu-id="7c59d-151">And then to see the tags for a specific image, use the [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository aci-tutorial-app --output table
```

<span data-ttu-id="7c59d-152">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="7c59d-152">Output:</span></span>

```azurecli
Result
--------
v1
```

## <a name="next-steps"></a><span data-ttu-id="7c59d-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7c59d-153">Next steps</span></span>

<span data-ttu-id="7c59d-154">Bu öğreticide Azure kapsayıcı örnekleri ile kullanmak için bir Azure kapsayıcı kayıt defteri hazırlanan ve kapsayıcı görüntü gönderilir.</span><span class="sxs-lookup"><span data-stu-id="7c59d-154">In this tutorial, an Azure Container Registry was prepared for use with Azure Container Instances, and the container image was pushed.</span></span> <span data-ttu-id="7c59d-155">Aşağıdaki adımlar tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="7c59d-155">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7c59d-156">Azure kapsayıcı kayıt defteri örneğini dağıtma</span><span class="sxs-lookup"><span data-stu-id="7c59d-156">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="7c59d-157">Azure kapsayıcı kayıt defteri için etiketleme kapsayıcı görüntüsü</span><span class="sxs-lookup"><span data-stu-id="7c59d-157">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="7c59d-158">Azure kapsayıcı kayıt defterine görüntüyü karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="7c59d-158">Uploading image to Azure Container Registry</span></span>

<span data-ttu-id="7c59d-159">Azure kapsayıcı örneği kullanarak Azure kapsayıcı dağıtma hakkında bilgi edinmek için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="7c59d-159">Advance to the next tutorial to learn about deploying the container to Azure using Azure Container Instances.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7c59d-160">Azure kapsayıcı örnekleri kapsayıcıları dağıtın</span><span class="sxs-lookup"><span data-stu-id="7c59d-160">Deploy containers to Azure Container Instances</span></span>](./container-instances-tutorial-deploy-app.md)
