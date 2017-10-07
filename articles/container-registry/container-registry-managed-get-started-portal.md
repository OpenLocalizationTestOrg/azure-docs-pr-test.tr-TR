---
title: "aaaCreate özel Docker kayıt defteri - Azure portalı | Microsoft Docs"
description: "Oluşturma ve yönetme özel Docker kapsayıcısı kayıt defterleri hello Azure portal ile çalışmaya başlama"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: cf3ce0dcf3036d0e9cd1eaf01721deccb00248d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-portal"></a><span data-ttu-id="037e5-103">Hello Azure portal kullanarak bir yönetilen kapsayıcı kayıt defteri oluşturma</span><span class="sxs-lookup"><span data-stu-id="037e5-103">Create a managed container registry using hello Azure portal</span></span>

<span data-ttu-id="037e5-104">Azure Container Registry, özel Docker kapsayıcı görüntülerini depolamak için kullanılan bir yönetilen Docker kapsayıcı kayıt defteridir.</span><span class="sxs-lookup"><span data-stu-id="037e5-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="037e5-105">Bu kılavuzu ayrıntıları Hello Azure portal kullanarak yönetilen Azure kapsayıcı kayıt defteri örneği oluşturma.</span><span class="sxs-lookup"><span data-stu-id="037e5-105">This guide details creating a managed Azure Container Registry instance using hello Azure portal.</span></span>

<span data-ttu-id="037e5-106">Yönetilen Azure kapsayıcı kayıt defterleri önizleme aşamasındadır ve tüm bölgelerde kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="037e5-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="037e5-107">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="037e5-107">Log in tooAzure</span></span>

<span data-ttu-id="037e5-108">İçinde toohello http://portal.azure.com Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="037e5-108">Log in toohello Azure portal at http://portal.azure.com.</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="037e5-109">Kapsayıcı kayıt defteri oluşturma</span><span class="sxs-lookup"><span data-stu-id="037e5-109">Create a container registry</span></span>

1. <span data-ttu-id="037e5-110">Merhaba tıklatın **yeni** düğmesi hello sol üst köşesinin hello Azure portalı üzerinde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="037e5-110">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="037e5-111">Arama hello Market **Azure kapsayıcı kayıt defteri** ve seçin.</span><span class="sxs-lookup"><span data-stu-id="037e5-111">Search hello marketplace for **Azure container registry** and select it.</span></span>

3. <span data-ttu-id="037e5-112">Tıklatın **oluşturma** hello ACR oluşturma dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="037e5-112">Click **Create** which will open hello ACR creation blade.</span></span>

    ![Container kayıt defteri ayarları](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. <span data-ttu-id="037e5-114">Merhaba, **Azure kapsayıcı kayıt defteri** dikey penceresinde, aşağıdaki bilgilerle hello girin.</span><span class="sxs-lookup"><span data-stu-id="037e5-114">In hello **Azure Container Registry** blade, enter hello following information.</span></span> <span data-ttu-id="037e5-115">İşiniz bittiğinde **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="037e5-115">Click **Create** when you are done.</span></span>

    <span data-ttu-id="037e5-116">a.</span><span class="sxs-lookup"><span data-stu-id="037e5-116">a.</span></span> <span data-ttu-id="037e5-117">**Kayıt defteri adı**: Oluşturduğunuz kayıt defterinize özel olan, genel olarak benzersiz bir üst düzey etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="037e5-117">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="037e5-118">Bu örnekte hello kayıt defteri adıdır *myAzureContainerRegistry1*, ancak kendi benzersiz adı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="037e5-118">In this example, hello registry name is *myAzureContainerRegistry1*, but substitute a unique name of your own.</span></span> <span data-ttu-id="037e5-119">Merhaba ad yalnızca harfler ve sayılar içerebilir.</span><span class="sxs-lookup"><span data-stu-id="037e5-119">hello name can contain only letters and numbers.</span></span>

    <span data-ttu-id="037e5-120">b.</span><span class="sxs-lookup"><span data-stu-id="037e5-120">b.</span></span> <span data-ttu-id="037e5-121">**Kaynak grubu**: Varolan seçin [kaynak grubu](../azure-resource-manager/resource-group-overview.md#resource-groups) veya yeni bir hello adını yazın.</span><span class="sxs-lookup"><span data-stu-id="037e5-121">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span>

    <span data-ttu-id="037e5-122">c.</span><span class="sxs-lookup"><span data-stu-id="037e5-122">c.</span></span> <span data-ttu-id="037e5-123">**Konum**: hello hizmet olduğu bir Azure veri merkezi konum seçin [kullanılabilir](https://azure.microsoft.com/regions/services/), gibi **Orta Güney ABD**.</span><span class="sxs-lookup"><span data-stu-id="037e5-123">**Location**: Select an Azure datacenter location where hello service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="037e5-124">d.</span><span class="sxs-lookup"><span data-stu-id="037e5-124">d.</span></span> <span data-ttu-id="037e5-125">**Yönetici kullanıcı**: istiyorsanız, bir yönetici kullanıcı tooaccess hello kayıt defteri etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="037e5-125">**Admin user**: If you want, enable an admin user tooaccess hello registry.</span></span> <span data-ttu-id="037e5-126">Merhaba kayıt defteri oluşturduktan sonra bu ayarı değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="037e5-126">You can change this setting after creating hello registry.</span></span>

    <span data-ttu-id="037e5-127">e.</span><span class="sxs-lookup"><span data-stu-id="037e5-127">e.</span></span> <span data-ttu-id="037e5-128">**Kullanım yönetilen kayıt defteri**: Evet'i seçin toohave ACR otomatik olarak hello kayıt defteri depolama yönetin, Web kancası kullanın ve AAD kimlik doğrulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="037e5-128">**Use managed registry**: Select yes toohave ACR automatically manage hello registry storage, use webhooks, and use AAD authentication.</span></span>

    <span data-ttu-id="037e5-129">f.</span><span class="sxs-lookup"><span data-stu-id="037e5-129">f.</span></span> <span data-ttu-id="037e5-130">**Fiyatlandırma Katmanı**: Fiyatlandırma katmanını seçin; daha fazla bilgi için buradaki ACR fiyatlandırma bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="037e5-130">**Pricing Tier**: Select a pricing tier, see here ACR pricing for more information.</span></span>

## <a name="log-in-tooacr-instance"></a><span data-ttu-id="037e5-131">TooACR örneğinde oturum</span><span class="sxs-lookup"><span data-stu-id="037e5-131">Log in tooACR instance</span></span>

<span data-ttu-id="037e5-132">İletme ve kapsayıcı görüntüleri çekme önce toohello ACR örneğinde oturum açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="037e5-132">Before pushing and pulling container images, you must log in toohello ACR instance.</span></span> 

<span data-ttu-id="037e5-133">toodo, bu nedenle, hello Azure CLI 2.0 kullanın.</span><span class="sxs-lookup"><span data-stu-id="037e5-133">toodo so, use hello Azure CLI 2.0.</span></span> <span data-ttu-id="037e5-134">İlk olarak, gerekirse, hello kullanarak Azure'da oturum [az oturum açma](/cli/azure/#login) komutu.</span><span class="sxs-lookup"><span data-stu-id="037e5-134">First, if needed, log into Azure using hello [az login](/cli/azure/#login) command.</span></span> 

```azurecli
az login
```

<span data-ttu-id="037e5-135">Ardından, hello kullanın [az acr oturum açma](/cli/azure/acr#login) toohello Azure kapsayıcı kayıt defteri, komut toolog.</span><span class="sxs-lookup"><span data-stu-id="037e5-135">Next, use hello [az acr login](/cli/azure/acr#login) command toolog in toohello Azure Container Registry.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

## <a name="use-azure-container-registry"></a><span data-ttu-id="037e5-136">Azure Container Registry’yi kullanma</span><span class="sxs-lookup"><span data-stu-id="037e5-136">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="037e5-137">Kapsayıcı görüntülerini listeleme</span><span class="sxs-lookup"><span data-stu-id="037e5-137">List container images</span></span>

<span data-ttu-id="037e5-138">Kullanım hello `az acr` CLI komutları tooquery hello görüntüleri ve bir havuzda etiketler.</span><span class="sxs-lookup"><span data-stu-id="037e5-138">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="037e5-139">Şu anda, kapsayıcı kayıt defteri hello desteklemiyor `docker search` komutu tooquery görüntüler ve etiketler için.</span><span class="sxs-lookup"><span data-stu-id="037e5-139">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="037e5-140">Depoları listeleme</span><span class="sxs-lookup"><span data-stu-id="037e5-140">List repositories</span></span>

<span data-ttu-id="037e5-141">Merhaba aşağıdaki örnek JSON (JavaScript nesne gösterimi) biçiminde bir kayıt defterindeki hello depoları listeler:</span><span class="sxs-lookup"><span data-stu-id="037e5-141">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="037e5-142">Etiketleri listeleme</span><span class="sxs-lookup"><span data-stu-id="037e5-142">List tags</span></span>

<span data-ttu-id="037e5-143">Merhaba aşağıdaki örnek listeler hello hello etiketlerini **samples/nginx** JSON biçiminde deposu:</span><span class="sxs-lookup"><span data-stu-id="037e5-143">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="037e5-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="037e5-144">Next steps</span></span>

<span data-ttu-id="037e5-145">Bu hızlı başlangıç bölümünde hello Azure portal kullanarak yönetilen Azure kapsayıcı kayıt defteri örneği oluşturduğunuzu düşünün.</span><span class="sxs-lookup"><span data-stu-id="037e5-145">In this quick start, you've created a managed Azure Container Registry instance using hello Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="037e5-146">Merhaba Docker CLI kullanarak ilk görüntünüzü bildirme</span><span class="sxs-lookup"><span data-stu-id="037e5-146">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
