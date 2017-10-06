---
title: "aaaCreate özel Docker kapsayıcısı kayıt defteri - Azure CLI | Microsoft Docs"
description: "Oluşturma ve yönetme özel Docker kapsayıcısı kayıt defterleri hello Azure CLI 2.0 ile çalışmaya başlama"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0d876a70b71a5e1bd564fbc9198f693dfe8a347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-cli-20"></a><span data-ttu-id="9ddb1-103">Hello Azure CLI 2.0 kullanarak özel bir Docker kapsayıcısı kayıt oluşturun</span><span class="sxs-lookup"><span data-stu-id="9ddb1-103">Create a private Docker container registry using hello Azure CLI 2.0</span></span>
<span data-ttu-id="9ddb1-104">Hello komutlarını kullanmak [Azure CLI 2.0](https://github.com/Azure/azure-cli) toocreate bir kapsayıcı kayıt defteri ve Linux, Mac veya Windows bilgisayarınızdan ayarlarını yönetin.</span><span class="sxs-lookup"><span data-stu-id="9ddb1-104">Use commands in hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) toocreate a container registry and manage its settings from your Linux, Mac, or Windows computer.</span></span> <span data-ttu-id="9ddb1-105">Ayrıca oluşturmak ve kapsayıcı kayıt defterleri hello kullanarak yönetmek [Azure portal](container-registry-get-started-portal.md) veya program aracılığıyla hello kapsayıcı kayıt defteri [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="9ddb1-105">You can also create and manage container registries using hello [Azure portal](container-registry-get-started-portal.md) or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="9ddb1-106">Arka plan ve kavramları için bkz: [hello genel bakış](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="9ddb1-106">For background and concepts, see [hello overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="9ddb1-107">Kapsayıcı kayıt defteri CLI komutlar hakkında Yardım almak için (`az acr` komutları), hello geçirmek `-h` parametresi tooany komutu.</span><span class="sxs-lookup"><span data-stu-id="9ddb1-107">For help on Container Registry CLI commands (`az acr` commands), pass hello `-h` parameter tooany command.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="9ddb1-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9ddb1-108">Prerequisites</span></span>
* <span data-ttu-id="9ddb1-109">**Azure CLI 2.0**: tooinstall ve hello CLI 2.0 ile çalışmaya başlama bkz hello [yükleme yönergeleri](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9ddb1-109">**Azure CLI 2.0**: tooinstall and get started with hello CLI 2.0, see hello [installation instructions](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="9ddb1-110">Çalıştırarak tooyour Azure aboneliği oturum `az login`.</span><span class="sxs-lookup"><span data-stu-id="9ddb1-110">Log in tooyour Azure subscription by running `az login`.</span></span> <span data-ttu-id="9ddb1-111">Daha fazla bilgi için bkz: [hello CLI 2.0 ile çalışmaya başlama](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9ddb1-111">For more information, see [Get started with hello CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="9ddb1-112">**Kaynak grubu**: Kapsayıcı kayıt defteri oluşturmadan önce bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md#resource-groups) oluşturun veya mevcut bir kaynak grubunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="9ddb1-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="9ddb1-113">Merhaba kaynak grubu hello kapsayıcı kayıt defteri hizmeti olduğu bir konumda olduğundan emin olun [kullanılabilir](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="9ddb1-113">Make sure hello resource group is in a location where hello Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="9ddb1-114">kullanarak bir kaynak grubu toocreate hello CLI 2.0 bkz [hello CLI 2.0 başvurusu](/cli/azure/group).</span><span class="sxs-lookup"><span data-stu-id="9ddb1-114">toocreate a resource group using hello CLI 2.0, see [hello CLI 2.0 reference](/cli/azure/group).</span></span>
* <span data-ttu-id="9ddb1-115">**Depolama hesabı** (isteğe bağlı): bir standart Azure oluşturma [depolama hesabı](../storage/common/storage-introduction.md) tooback hello kapsayıcı hello kayıt defterinde aynı konumu.</span><span class="sxs-lookup"><span data-stu-id="9ddb1-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) tooback hello container registry in hello same location.</span></span> <span data-ttu-id="9ddb1-116">Kayıt defteri ile oluştururken, bir depolama hesabı belirtmezseniz `az acr create`, hello komut sizin için bir tane oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9ddb1-116">If you don't specify a storage account when creating a registry with `az acr create`, hello command creates one for you.</span></span> <span data-ttu-id="9ddb1-117">bir depolama hesabı kullanarak toocreate CLI 2.0 Merhaba, bkz: [hello CLI 2.0 başvurusu](/cli/azure/storage/account).</span><span class="sxs-lookup"><span data-stu-id="9ddb1-117">toocreate a storage account using hello CLI 2.0, see [hello CLI 2.0 reference](/cli/azure/storage/account).</span></span> <span data-ttu-id="9ddb1-118">Premium Depolama şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="9ddb1-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="9ddb1-119">**Hizmet sorumlusu** (isteğe bağlı): bir kayıt defteri hello CLI ile oluşturduğunuzda, varsayılan olarak, erişim için kurulu değil.</span><span class="sxs-lookup"><span data-stu-id="9ddb1-119">**Service principal** (optional): When you create a registry with hello CLI, by default it is not set up for access.</span></span> <span data-ttu-id="9ddb1-120">Gereksinimlerinize bağlı olarak, varolan bir Azure Active Directory hizmet asıl tooa kayıt atayabilirsiniz (veya oluşturun ve yeni bir ata), veya hello kayıt defterindeki yönetici kullanıcı hesabını etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="9ddb1-120">Depending on your needs, you can assign an existing Azure Active Directory service principal tooa registry (or create and assign a new one), or enable hello registry's admin user account.</span></span> <span data-ttu-id="9ddb1-121">Bu makalenin sonraki bölümlerinde Hello bölümlere bakın.</span><span class="sxs-lookup"><span data-stu-id="9ddb1-121">See hello sections later in this article.</span></span> <span data-ttu-id="9ddb1-122">Kayıt defteri erişim hakkında daha fazla bilgi için bkz: [hello kapsayıcı kayıt defteri ile kimlik doğrulama](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9ddb1-122">For more information about registry access, see [Authenticate with hello container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="9ddb1-123">Kapsayıcı kayıt defteri oluşturma</span><span class="sxs-lookup"><span data-stu-id="9ddb1-123">Create a container registry</span></span>
<span data-ttu-id="9ddb1-124">Merhaba çalıştırmak `az acr create` komutu toocreate bir kapsayıcı kayıt defteri.</span><span class="sxs-lookup"><span data-stu-id="9ddb1-124">Run hello `az acr create` command toocreate a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="9ddb1-125">Bir kayıt defteri oluştururken yalnızca harf ve sayı içeren genel olarak benzersiz bir üst düzey etki alanı adı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="9ddb1-125">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="9ddb1-126">Merhaba kayıt defteri adı hello örneklerde `myRegistry1`, ancak kendi benzersiz adı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9ddb1-126">hello registry name in hello examples is `myRegistry1`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="9ddb1-127">kullandığı hello en az parametreleri toocreate kapsayıcı kayıt defteri komutu aşağıdaki hello `myRegistry1` hello kaynak grubunda `myResourceGroup`ve hello kullanarak *temel* sku:</span><span class="sxs-lookup"><span data-stu-id="9ddb1-127">hello following command uses hello minimal parameters toocreate container registry `myRegistry1` in hello resource group `myResourceGroup`, and using hello *Basic* sku:</span></span>

```azurecli
az acr create --name myRegistry1 --resource-group myResourceGroup --sku Basic
```

* <span data-ttu-id="9ddb1-128">`--storage-account-name` isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="9ddb1-128">`--storage-account-name` is optional.</span></span> <span data-ttu-id="9ddb1-129">Yoksa belirtilen hello kayıt defteri adını oluşan bir ada sahip bir depolama hesabı oluşturulur ve kaynak grubu bir zaman damgasına hello belirtilen.</span><span class="sxs-lookup"><span data-stu-id="9ddb1-129">If not specified, a storage account is created with a name consisting of hello registry name and a timestamp in hello specified resource group.</span></span>

<span data-ttu-id="9ddb1-130">Merhaba kayıt oluşturulduğunda hello çıkış benzer toohello aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="9ddb1-130">When hello registry is created, hello output is similar toohello following:</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T18:36:29.124842+00:00",
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry
/registries/myRegistry1",
  "location": "southcentralus",
  "loginServer": "myregistry1.azurecr.io",
  "name": "myRegistry1",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "myregistry123456789"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}

```


<span data-ttu-id="9ddb1-131">Özellikle şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="9ddb1-131">Take special note:</span></span>

* <span data-ttu-id="9ddb1-132">`id`-Tooassign bir hizmet sorumlusu istiyorsanız, gereksinim duyduğunuz aboneliğinizde hello kayıt defteri tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="9ddb1-132">`id` - Identifier for hello registry in your subscription, which you need if you want tooassign a service principal.</span></span>
* <span data-ttu-id="9ddb1-133">`loginServer`-Belirttiğiniz çok hello tam adı[toohello kayıt defterinde oturum](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9ddb1-133">`loginServer` - hello fully qualified name you specify too[log in toohello registry](container-registry-authentication.md).</span></span> <span data-ttu-id="9ddb1-134">Bu örnekte, hello adıdır `myregistry1.exp.azurecr.io` (tüm küçük harf).</span><span class="sxs-lookup"><span data-stu-id="9ddb1-134">In this example, hello name is `myregistry1.exp.azurecr.io` (all lowercase).</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="9ddb1-135">Hizmet sorumlusu atama</span><span class="sxs-lookup"><span data-stu-id="9ddb1-135">Assign a service principal</span></span>
<span data-ttu-id="9ddb1-136">CLI 2.0 komutları tooassign bir Azure Active Directory hizmet asıl tooa kayıt defteri kullanın.</span><span class="sxs-lookup"><span data-stu-id="9ddb1-136">Use CLI 2.0 commands tooassign an Azure Active Directory service principal tooa registry.</span></span> <span data-ttu-id="9ddb1-137">Merhaba hizmet sorumlusu Bu örneklerde hello sahibi rolü atanmış, ancak atayabilirsiniz [diğer rolleri](../active-directory/role-based-access-control-configure.md) istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="9ddb1-137">hello service principal in these examples is assigned hello Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal-and-assign-access-toohello-registry"></a><span data-ttu-id="9ddb1-138">Bir hizmet sorumlusu oluşturun ve erişim toohello kayıt defteri atayın</span><span class="sxs-lookup"><span data-stu-id="9ddb1-138">Create a service principal and assign access toohello registry</span></span>
<span data-ttu-id="9ddb1-139">Komutu aşağıdaki hello, yeni bir hizmet sorumlusu sahibi rolü erişim toohello kayıt defteri tanımlayıcısı ile Merhaba geçirilen atanır `--scopes` parametresi.</span><span class="sxs-lookup"><span data-stu-id="9ddb1-139">In hello following command, a new service principal is assigned Owner role access toohello registry identifier passed with hello `--scopes` parameter.</span></span> <span data-ttu-id="9ddb1-140">Güçlü bir parola ile Merhaba belirtin `--password` parametresi.</span><span class="sxs-lookup"><span data-stu-id="9ddb1-140">Specify a strong password with hello `--password` parameter.</span></span>

```azurecli
az ad sp create-for-rbac --scopes /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --password myPassword
```



### <a name="assign-an-existing-service-principal"></a><span data-ttu-id="9ddb1-141">Mevcut bir hizmet sorumlusunu atama</span><span class="sxs-lookup"><span data-stu-id="9ddb1-141">Assign an existing service principal</span></span>
<span data-ttu-id="9ddb1-142">Zaten bir hizmet sorumlusu varsa ve tooassign istiyorsanız, aşağıdaki örnek komut benzer toohello çalıştırmak sahibi rolü erişim toohello kayıt defteri,.</span><span class="sxs-lookup"><span data-stu-id="9ddb1-142">If you already have a service principal and want tooassign it Owner role access toohello registry, run a command similar toohello following example.</span></span> <span data-ttu-id="9ddb1-143">Hello kullanarak hello hizmet asıl uygulama kimliği geçirdiğiniz `--assignee` parametre:</span><span class="sxs-lookup"><span data-stu-id="9ddb1-143">You pass hello service principal app ID using hello `--assignee` parameter:</span></span>

```azurecli
az role assignment create --scope /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --assignee myAppId
```



## <a name="manage-admin-credentials"></a><span data-ttu-id="9ddb1-144">Yönetici kimlik bilgilerini yönetme</span><span class="sxs-lookup"><span data-stu-id="9ddb1-144">Manage admin credentials</span></span>
<span data-ttu-id="9ddb1-145">Her kapsayıcı kayıt defteri için otomatik olarak bir yönetici hesabı oluşturulur ve varsayılan olarak devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="9ddb1-145">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="9ddb1-146">Aşağıdaki örneklerde gösterildiği hello `az acr` CLI komutları kapsayıcı kaydınız toomanage hello yönetici kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="9ddb1-146">hello following examples show `az acr` CLI commands toomanage hello admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="9ddb1-147">Yönetici kullanıcı kimlik bilgileri edinme</span><span class="sxs-lookup"><span data-stu-id="9ddb1-147">Obtain admin user credentials</span></span>
```azurecli
az acr credential show -n myRegistry1
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="9ddb1-148">Mevcut bir kayıt defteri için yönetici kullanıcıyı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="9ddb1-148">Enable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled true
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="9ddb1-149">Mevcut bir kayıt defteri için yönetici kullanıcıyı devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="9ddb1-149">Disable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled false
```

## <a name="list-images-and-tags"></a><span data-ttu-id="9ddb1-150">Görüntüleri ve etiketleri listeleme</span><span class="sxs-lookup"><span data-stu-id="9ddb1-150">List images and tags</span></span>
<span data-ttu-id="9ddb1-151">Kullanım hello `az acr` CLI komutları tooquery hello görüntüleri ve bir havuzda etiketler.</span><span class="sxs-lookup"><span data-stu-id="9ddb1-151">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="9ddb1-152">Şu anda, kapsayıcı kayıt defteri hello desteklemiyor `docker search` komutu tooquery görüntüler ve etiketler için.</span><span class="sxs-lookup"><span data-stu-id="9ddb1-152">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>


### <a name="list-repositories"></a><span data-ttu-id="9ddb1-153">Depoları listeleme</span><span class="sxs-lookup"><span data-stu-id="9ddb1-153">List repositories</span></span>
<span data-ttu-id="9ddb1-154">Merhaba aşağıdaki örnek JSON (JavaScript nesne gösterimi) biçiminde bir kayıt defterindeki hello depoları listeler:</span><span class="sxs-lookup"><span data-stu-id="9ddb1-154">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="9ddb1-155">Etiketleri listeleme</span><span class="sxs-lookup"><span data-stu-id="9ddb1-155">List tags</span></span>
<span data-ttu-id="9ddb1-156">Merhaba aşağıdaki örnek listeler hello hello etiketlerini **samples/nginx** JSON biçiminde deposu:</span><span class="sxs-lookup"><span data-stu-id="9ddb1-156">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="9ddb1-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9ddb1-157">Next steps</span></span>
* [<span data-ttu-id="9ddb1-158">Merhaba Docker CLI kullanarak ilk görüntünüzü bildirme</span><span class="sxs-lookup"><span data-stu-id="9ddb1-158">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
