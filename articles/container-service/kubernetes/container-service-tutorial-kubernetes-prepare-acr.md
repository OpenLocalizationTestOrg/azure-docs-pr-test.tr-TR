---
title: "Azure kapsayıcı hizmeti Öğreticisi - hazırlama ACR | Microsoft Docs"
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
ms.openlocfilehash: 3e1f7617bf2fc52ee4c15598f51a46276f4dc57d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="46668-104">Dağıtma ve Azure kapsayıcı kayıt defteri kullanma</span><span class="sxs-lookup"><span data-stu-id="46668-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="46668-105">Azure kapsayıcı kayıt defteri (ACR) Docker kapsayıcısı görüntüleri için bir Azure tabanlı, özel kayıt defteri ' dir.</span><span class="sxs-lookup"><span data-stu-id="46668-105">Azure Container Registry (ACR) is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="46668-106">Bu öğretici, bölümü yedi, iki kılavuzluk Azure kapsayıcı kayıt defteri örneğini dağıtma ve kapsayıcı görüntü için iletme.</span><span class="sxs-lookup"><span data-stu-id="46668-106">This tutorial, part two of seven, walks through deploying an Azure Container Registry instance, and pushing a container image to it.</span></span> <span data-ttu-id="46668-107">Tamamlanan adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="46668-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="46668-108">Azure kapsayıcı kayıt defteri (ACR) örneğini dağıtma</span><span class="sxs-lookup"><span data-stu-id="46668-108">Deploying an Azure Container Registry (ACR) instance</span></span>
> * <span data-ttu-id="46668-109">ACR için bir kapsayıcı görüntüsü etiketleme</span><span class="sxs-lookup"><span data-stu-id="46668-109">Tagging a container image for ACR</span></span>
> * <span data-ttu-id="46668-110">Görüntü ACR için karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="46668-110">Uploading the image to ACR</span></span>

<span data-ttu-id="46668-111">Sonraki öğreticilerde bu ACR örnek kapsayıcı görüntüleri güvenli bir şekilde çalıştırmak için bir Azure kapsayıcı hizmeti Kubernetes küme tümleşiktir.</span><span class="sxs-lookup"><span data-stu-id="46668-111">In subsequent tutorials, this ACR instance is integrated with an Azure Container Service Kubernetes cluster, for securely running container images.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="46668-112">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="46668-112">Before you begin</span></span>

<span data-ttu-id="46668-113">İçinde [önceki öğretici](./container-service-tutorial-kubernetes-prepare-app.md), basit bir Azure oylama uygulaması için bir kapsayıcı görüntüsü oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="46668-113">In the [previous tutorial](./container-service-tutorial-kubernetes-prepare-app.md), a container image was created for a simple Azure Voting application.</span></span> <span data-ttu-id="46668-114">Bu öğreticide, Azure kapsayıcı kayıt defterine bu görüntüyü gönderilir.</span><span class="sxs-lookup"><span data-stu-id="46668-114">In this tutorial, this image is pushed to an Azure Container Registry.</span></span> <span data-ttu-id="46668-115">Azure oylama uygulama görüntüsü oluşturmadıysanız, geri dönüp [Öğreticisi 1 – Oluştur kapsayıcı görüntüleri](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="46668-115">If you have not created the Azure Voting app image, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> <span data-ttu-id="46668-116">Alternatif olarak, adımlar burada herhangi bir kapsayıcı görüntü ile çalışma ayrıntılı.</span><span class="sxs-lookup"><span data-stu-id="46668-116">Alternatively, the steps detailed here work with any container image.</span></span>

<span data-ttu-id="46668-117">Bu öğretici, Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="46668-117">This tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="46668-118">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="46668-118">Run `az --version` to find the version.</span></span> <span data-ttu-id="46668-119">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="46668-119">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="46668-120">Azure kapsayıcı kayıt defteri dağıtın</span><span class="sxs-lookup"><span data-stu-id="46668-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="46668-121">Azure kapsayıcı kayıt defteri dağıtırken, önce bir kaynak grubu gerekir.</span><span class="sxs-lookup"><span data-stu-id="46668-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="46668-122">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="46668-122">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="46668-123">[az group create](/cli/azure/group#create) komutuyla bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="46668-123">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="46668-124">Bu örnekte, bir kaynak grubu adında *myResourceGroup* oluşturulan *westeurope* bölge.</span><span class="sxs-lookup"><span data-stu-id="46668-124">In this example, a resource group named *myResourceGroup* is created in the *westeurope* region.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="46668-125">Azure kapsayıcı kayıt defteri ile oluşturma [az acr oluşturmak](/cli/azure/acr#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="46668-125">Create an Azure Container registry with the [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="46668-126">Bir kapsayıcı kayıt defteri adını **benzersiz olmalıdır**.</span><span class="sxs-lookup"><span data-stu-id="46668-126">The name of a Container Registry **must be unique**.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

<span data-ttu-id="46668-127">Bu öğreticinin geri kalanını, "acrname" yer tutucu olarak seçtiğiniz kapsayıcı kayıt defteri adını kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="46668-127">Throughout the rest of this tutorial, we use "acrname" as a placeholder for the container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="46668-128">Kapsayıcı kayıt defteri oturum açma</span><span class="sxs-lookup"><span data-stu-id="46668-128">Container registry login</span></span>

<span data-ttu-id="46668-129">ACR örneğinizi görüntüleri göndermeden önce oturum gerekir.</span><span class="sxs-lookup"><span data-stu-id="46668-129">You must log in to your ACR instance before pushing images to it.</span></span> <span data-ttu-id="46668-130">Kullanım [az acr oturum açma](https://docs.microsoft.com/en-us/cli/azure/acr#login) işlemi tamamlamak için komutu.</span><span class="sxs-lookup"><span data-stu-id="46668-130">Use the [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command to complete the operation.</span></span> <span data-ttu-id="46668-131">Kapsayıcı kayıt defterine oluşturulduğunda verilen benzersiz bir ad vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="46668-131">You need to provide the unique name given to the container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="46668-132">Komut tamamlandıktan sonra 'Başarılı oturum açma' iletisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="46668-132">The command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-images"></a><span data-ttu-id="46668-133">Etiket kapsayıcı görüntüleri</span><span class="sxs-lookup"><span data-stu-id="46668-133">Tag container images</span></span>

<span data-ttu-id="46668-134">Her kapsayıcı görüntü kayıt loginServer adıyla etiketlenmesi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="46668-134">Each container image needs to be tagged with the loginServer name of the registry.</span></span> <span data-ttu-id="46668-135">Bu etiket kapsayıcı görüntüleri bir görüntü kayıt defterine Ftp'den zaman yönlendirme için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="46668-135">This tag is used for routing when pushing container images to an image registry.</span></span>

<span data-ttu-id="46668-136">Geçerli görüntüleri listesini görmek için [docker görüntüleri](https://docs.docker.com/engine/reference/commandline/images/) komutu.</span><span class="sxs-lookup"><span data-stu-id="46668-136">To see a list of current images, use the [docker images](https://docs.docker.com/engine/reference/commandline/images/) command.</span></span>

```bash
docker images
```

<span data-ttu-id="46668-137">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="46668-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="46668-138">LoginServer adını almak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="46668-138">To get the loginServer name, run the following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="46668-139">Şimdi, etiket *azure oy ön* kapsayıcı kayıt defteri loginServer görüntüsüyle.</span><span class="sxs-lookup"><span data-stu-id="46668-139">Now, tag the *azure-vote-front* image with the loginServer of the container registry.</span></span> <span data-ttu-id="46668-140">Ayrıca, ekleme `:redis-v1` sonuna kadar görüntü adı.</span><span class="sxs-lookup"><span data-stu-id="46668-140">Also, add `:redis-v1` to the end of the image name.</span></span> <span data-ttu-id="46668-141">Bu etiket resim sürümünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="46668-141">This tag indicates the image version.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="46668-142">Etiketli sonra [docker görüntüler] çalıştırma işlemi doğrulamak için (https://docs.docker.com/engine/reference/commandline/images/).</span><span class="sxs-lookup"><span data-stu-id="46668-142">Once tagged, run [docker images] (https://docs.docker.com/engine/reference/commandline/images/) to verify the operation.</span></span>

```bash
docker images
```

<span data-ttu-id="46668-143">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="46668-143">Output:</span></span>

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-to-registry"></a><span data-ttu-id="46668-144">Kayıt defteri itme görüntüleri</span><span class="sxs-lookup"><span data-stu-id="46668-144">Push images to registry</span></span>

<span data-ttu-id="46668-145">Anında *azure oy ön* kayıt defterine görüntü.</span><span class="sxs-lookup"><span data-stu-id="46668-145">Push the *azure-vote-front* image to the registry.</span></span> 

<span data-ttu-id="46668-146">Aşağıdaki örneği kullanarak, ortamınızdan loginServer ACR loginServer adını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="46668-146">Using the following example, replace the ACR loginServer name with the loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="46668-147">Bu, birkaç tamamlamak için dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="46668-147">This takes a couple of minutes to complete.</span></span>

## <a name="list-images-in-registry"></a><span data-ttu-id="46668-148">Kayıt defterinde listesi görüntüler</span><span class="sxs-lookup"><span data-stu-id="46668-148">List images in registry</span></span>

<span data-ttu-id="46668-149">Azure kapsayıcı kaydınız gönderilen görüntüleri listesini döndürmek için kullanıcı [az acr deposu listesi](/cli/azure/acr/repository#list) komutu.</span><span class="sxs-lookup"><span data-stu-id="46668-149">To return a list of images that have been pushed to your Azure Container registry, user the [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="46668-150">Komut ACR örnek adıyla güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="46668-150">Update the command with the ACR instance name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="46668-151">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="46668-151">Output:</span></span>

```azurecli
Result
----------------
azure-vote-front
```

<span data-ttu-id="46668-152">Ve ardından belirli bir resim için etiketleri görmek için [az acr deposunu Göster-etiketleri](/cli/azure/acr/repository#show-tags) komutu.</span><span class="sxs-lookup"><span data-stu-id="46668-152">And then to see the tags for a specific image, use the [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

<span data-ttu-id="46668-153">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="46668-153">Output:</span></span>

```azurecli
Result
--------
redis-v1
```

<span data-ttu-id="46668-154">Eğitmen tamamlandığında, kapsayıcı görüntünün bir özel Azure kapsayıcı kayıt defteri örneğinde zamandır depolanmış.</span><span class="sxs-lookup"><span data-stu-id="46668-154">At tutorial completion, the container image has been stored in a private Azure Container Registry instance.</span></span> <span data-ttu-id="46668-155">Bu görüntü ACR sonraki öğreticilerde Kubernetes kümeye dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="46668-155">This image is deployed from ACR to a Kubernetes cluster in subsequent tutorials.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46668-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="46668-156">Next steps</span></span>

<span data-ttu-id="46668-157">Bu öğreticide, bir ACS Kubernetes kümesinde kullanmak için bir Azure kapsayıcı kayıt defteri hazırlanan.</span><span class="sxs-lookup"><span data-stu-id="46668-157">In this tutorial, an Azure Container Registry was prepared for use in an ACS Kubernetes cluster.</span></span> <span data-ttu-id="46668-158">Aşağıdaki adımlar tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="46668-158">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="46668-159">Azure kapsayıcı kayıt defteri örneği dağıtılan</span><span class="sxs-lookup"><span data-stu-id="46668-159">Deployed an Azure Container Registry instance</span></span>
> * <span data-ttu-id="46668-160">ACR için bir kapsayıcı görüntüsü etiketli</span><span class="sxs-lookup"><span data-stu-id="46668-160">Tagged a container image for ACR</span></span>
> * <span data-ttu-id="46668-161">ACR için görüntüyü karşıya</span><span class="sxs-lookup"><span data-stu-id="46668-161">Uploaded the image to ACR</span></span>

<span data-ttu-id="46668-162">Azure Kubernetes kümede dağıtma hakkında bilgi edinmek için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="46668-162">Advance to the next tutorial to learn about deploying a Kubernetes cluster in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="46668-163">Kubernetes kümesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="46668-163">Deploy Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-deploy-cluster.md)