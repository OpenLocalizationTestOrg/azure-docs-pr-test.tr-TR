---
title: "aaaAzure kapsayıcı kayıt defteri depoları | Microsoft Docs"
description: "Nasıl toouse Azure kapsayıcı kayıt defteri depoları Docker görüntüleri"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: cristyg
ms.openlocfilehash: 108622c565e41777fbb1fc9da9a01168abc7a7fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="35fd0-103">Azure kapsayıcı kayıt defteri depoları</span><span class="sxs-lookup"><span data-stu-id="35fd0-103">Azure container registry repositories</span></span>

<span data-ttu-id="35fd0-104">Azure kapsayıcı kayıt defteri depoları toostore kapsayıcı görüntüleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="35fd0-104">Azure container registry allows you toostore container images in repositories.</span></span> <span data-ttu-id="35fd0-105">Depoları görüntüleri depolayarak Yalıtılmış ortamlarda görüntü (veya görüntüleri sürümü) grupları olabilir.</span><span class="sxs-lookup"><span data-stu-id="35fd0-105">By storing images in repositories, you can have groups of images (or version of images) in isolated environments.</span></span> <span data-ttu-id="35fd0-106">Görüntüleri tooyour kayıt defteri bastığınızda bu depoları belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="35fd0-106">You can specify these repositories when you push images tooyour registry.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="35fd0-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="35fd0-107">Prerequisites</span></span>
* <span data-ttu-id="35fd0-108">**Azure kapsayıcısı kayıt defteri** -Azure aboneliğinizde bir kapsayıcı kayıt defteri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="35fd0-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="35fd0-109">Örneğin, hello kullan [Azure portal](container-registry-get-started-portal.md) veya hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="35fd0-109">For example, use hello [Azure portal](container-registry-get-started-portal.md) or hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="35fd0-110">**Docker CLI** -tooset bir Docker ana bilgisayar ve erişim hello Docker CLI komutları olarak, yerel bilgisayarınıza yüklemek [Docker altyapısına](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="35fd0-110">**Docker CLI** - tooset up your local computer as a Docker host and access hello Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>
* <span data-ttu-id="35fd0-111">**Bir görüntü çekme** - görüntüyü hello ortak Docker hub'a kayıt defterinden çekme etiketlemek ve tooyour kayıt defteri itme.</span><span class="sxs-lookup"><span data-stu-id="35fd0-111">**Pull an image** - Pull an image from hello public Docker Hub registry, tag it, and push it tooyour registry.</span></span> <span data-ttu-id="35fd0-112">Nasıl hakkında yönergeler için anında iletme ve çekme görüntüleri bkz [itme Docker görüntü tooAzure özel kayıt defteri](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="35fd0-112">For guidance on how push and pull images, see [Push Docker image tooAzure private registry](container-registry-get-started-docker-cli.md).</span></span>


## <a name="viewing-repositories-in-hello-portal"></a><span data-ttu-id="35fd0-113">Depoları hello Portal görüntüleme</span><span class="sxs-lookup"><span data-stu-id="35fd0-113">Viewing repositories in hello Portal</span></span>

<span data-ttu-id="35fd0-114">Görüntüleri tooyour kapsayıcı kayıt defteri gönderilen sonra hello Azure portal hello görüntülerinde barındırma hello depoları listesini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="35fd0-114">Once you have pushed images tooyour container registry, you can see a list of hello repositories hosting hello images in hello Azure portal.</span></span>

<span data-ttu-id="35fd0-115">Merhaba hello adımları izlediyseniz [anında Docker görüntü tooAzure özel kayıt defteri](container-registry-get-started-docker-cli.md) makale, kapsayıcı kayıt defterinizde Nginx görüntü şimdi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="35fd0-115">If you followed hello steps in hello [Push Docker image tooAzure private registry](container-registry-get-started-docker-cli.md) article, you should now have a Nginx image in your container registry.</span></span> <span data-ttu-id="35fd0-116">Merhaba yönergeleri bir parçası olarak hello görüntüsü için bir ad belirttiğinizden.</span><span class="sxs-lookup"><span data-stu-id="35fd0-116">As part of hello instructions, you should have specified a namespace for hello image.</span></span> <span data-ttu-id="35fd0-117">Merhaba aşağıdaki örnekte, hello komutu hello NGinx görüntü toohello "örneklerini" deposuna iter:</span><span class="sxs-lookup"><span data-stu-id="35fd0-117">In hello example below, hello command pushes hello NGinx image toohello "samples" repository:</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```
 <span data-ttu-id="35fd0-118">Azure Container Kayıt Defteri, çok düzeyli depo ad alanlarını destekler.</span><span class="sxs-lookup"><span data-stu-id="35fd0-118">Azure Container Registry supports multilevel repository namespaces.</span></span> <span data-ttu-id="35fd0-119">Bu özellik, görüntüleri ilgili tooa belirli uygulama toogroup koleksiyonları veya uygulamaları toospecific geliştirme veya işletimsel takımlar koleksiyonunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="35fd0-119">This feature enables you toogroup collections of images related tooa specific app, or a collection of apps toospecific development or operational teams.</span></span> <span data-ttu-id="35fd0-120">kapsayıcı kayıt defterleri, depoları hakkında daha fazla tooread bkz [özel Docker kapsayıcısı kayıt defterleri azure'da](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="35fd0-120">tooread more about repositories in container registries, see [Private Docker container registries in Azure](container-registry-intro.md).</span></span>

<span data-ttu-id="35fd0-121">tooview hello kapsayıcı kayıt defteri depoları:</span><span class="sxs-lookup"><span data-stu-id="35fd0-121">tooview hello container registry repositories:</span></span>

1. <span data-ttu-id="35fd0-122">Toohello Azure portalında oturum açın</span><span class="sxs-lookup"><span data-stu-id="35fd0-122">Log in toohello Azure portal</span></span>
2. <span data-ttu-id="35fd0-123">Merhaba üzerinde **Azure kapsayıcı kayıt defteri** dikey penceresinde, tooinspect istediğiniz select hello kayıt defteri</span><span class="sxs-lookup"><span data-stu-id="35fd0-123">On hello **Azure Container Registry** blade, select hello registry you wish tooinspect</span></span>
3. <span data-ttu-id="35fd0-124">Merhaba kayıt defteri dikey penceresinde tıklayın **depoları** toosee tüm hello depoları ve resimlerinin listesi</span><span class="sxs-lookup"><span data-stu-id="35fd0-124">In hello registry blade, click **Repositories** toosee a list of all hello repositories and their images</span></span>
4. <span data-ttu-id="35fd0-125">(İsteğe bağlı) Özel görüntü toosee etiketler seçin</span><span class="sxs-lookup"><span data-stu-id="35fd0-125">(Optional) Select a specific image toosee tags</span></span>

![Merhaba portalında depoları](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a><span data-ttu-id="35fd0-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="35fd0-127">Next steps</span></span>
<span data-ttu-id="35fd0-128">Merhaba temelleri bildiğinize göre kayıt defterini kullanarak hazır toostart olduğunuz!</span><span class="sxs-lookup"><span data-stu-id="35fd0-128">Now that you know hello basics, you are ready toostart using your registry!</span></span> <span data-ttu-id="35fd0-129">Örneğin, kapsayıcı görüntüleri tooan dağıtmaya başlamadan [Azure kapsayıcı hizmeti](https://azure.microsoft.com/documentation/services/container-service/) küme.</span><span class="sxs-lookup"><span data-stu-id="35fd0-129">For example, start deploying container images tooan [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
