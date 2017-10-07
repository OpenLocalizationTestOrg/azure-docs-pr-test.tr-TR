---
title: "aaaAzure kapsayıcı kayıt defteri kancalarını | Microsoft Docs"
description: "Azure kapsayıcı kayıt defteri Web kancaları"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acr, azure-container-registry
keywords: "Docker, kapsayıcıları, ACR"
ms.assetid: 
ms.service: container-registry
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/06/2017
ms.author: nepeters
ms.openlocfilehash: adc2afec486007e2d54cd689e6f7ef8b1098db06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-container-registry-webhooks---azure-portal"></a><span data-ttu-id="01d46-104">Azure kapsayıcı kayıt defteri kancalarını - Azure portalını kullanma</span><span class="sxs-lookup"><span data-stu-id="01d46-104">Using Azure Container Registry webhooks - Azure portal</span></span>

<span data-ttu-id="01d46-105">Azure kapsayıcı kayıt defteri depolar ve özel Docker kapsayıcısı görüntüleri, Docker hub'a genel Docker görüntüleri depolayan benzer toohello şekilde yönetir.</span><span class="sxs-lookup"><span data-stu-id="01d46-105">An Azure container registry stores and manages private Docker container images, similar toohello way Docker Hub stores public Docker images.</span></span> <span data-ttu-id="01d46-106">Bazı Eylemler, kayıt defteri depoları biri gerçekleştiğinde Web kancalarını tootrigger olayları kullanın.</span><span class="sxs-lookup"><span data-stu-id="01d46-106">You use webhooks tootrigger events when certain actions take place in one of your registry repositories.</span></span> <span data-ttu-id="01d46-107">Web kancası tooevents hello kayıt defteri düzeyinde yanıt verebilir veya tooa belirli depo etiketi kapsamlı.</span><span class="sxs-lookup"><span data-stu-id="01d46-107">Webhooks can respond tooevents at hello registry level or they can be scoped down tooa specific repository tag.</span></span> 

<span data-ttu-id="01d46-108">Daha fazla arka plan ve kavramları hello bkz [genel bakış](./container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="01d46-108">For more background and concepts, see hello [overview](./container-registry-intro.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01d46-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="01d46-109">Prerequisites</span></span> 

- <span data-ttu-id="01d46-110">Azure kapsayıcı kayıt defteri - yönetilen Azure aboneliğinizde bir yönetilen kapsayıcı kayıt oluşturun.</span><span class="sxs-lookup"><span data-stu-id="01d46-110">Azure container managed registry - Create a managed container registry in your Azure subscription.</span></span> <span data-ttu-id="01d46-111">Örneğin, hello Azure portal kullanın veya Azure CLI 2.0 hello.</span><span class="sxs-lookup"><span data-stu-id="01d46-111">For example, use hello Azure portal or hello Azure CLI 2.0.</span></span> 
- <span data-ttu-id="01d46-112">Docker CLI - yerel bilgisayarınızı bir Docker ana bilgisayar ve erişim hello Docker CLI komutları olarak tooset Docker altyapısına yükleyin.</span><span class="sxs-lookup"><span data-stu-id="01d46-112">Docker CLI - tooset up your local computer as a Docker host and access hello Docker CLI commands, install Docker Engine.</span></span> 

## <a name="create-webhook-azure-portal"></a><span data-ttu-id="01d46-113">Azure portal Web kancası oluşturma</span><span class="sxs-lookup"><span data-stu-id="01d46-113">Create webhook Azure portal</span></span>

1. <span data-ttu-id="01d46-114">Toohello Azure portalında oturum açın ve toocreate kancalarını istediğiniz toohello kayıt defteri gidin.</span><span class="sxs-lookup"><span data-stu-id="01d46-114">Log in toohello Azure portal and navigate toohello registry in which you want toocreate webhooks.</span></span> 

2. <span data-ttu-id="01d46-115">Merhaba kapsayıcı dikey penceresinde hello "Kancalarını" sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="01d46-115">In hello container blade, select hello "Webhooks" tab.</span></span> 

3. <span data-ttu-id="01d46-116">"Ekle" Merhaba Web kancası dikey araç çubuğundan seçin.</span><span class="sxs-lookup"><span data-stu-id="01d46-116">Select "Add" from hello webhook blade toolbar.</span></span> 

4. <span data-ttu-id="01d46-117">Tam hello *Web kancası oluşturma* bilgisinden hello formla:</span><span class="sxs-lookup"><span data-stu-id="01d46-117">Complete hello *Create Webhook* form with hello following information:</span></span>

| <span data-ttu-id="01d46-118">Değer</span><span class="sxs-lookup"><span data-stu-id="01d46-118">Value</span></span> | <span data-ttu-id="01d46-119">Açıklama</span><span class="sxs-lookup"><span data-stu-id="01d46-119">Description</span></span> |
|---|---|
| <span data-ttu-id="01d46-120">Ad</span><span class="sxs-lookup"><span data-stu-id="01d46-120">Name</span></span> | <span data-ttu-id="01d46-121">toogive toohello Web kancası istediğiniz hello adı.</span><span class="sxs-lookup"><span data-stu-id="01d46-121">hello name you want toogive toohello webhook.</span></span> <span data-ttu-id="01d46-122">Ad yalnızca küçük harfler ve sayılar içerebilir ve 5-50 karakter arasında.</span><span class="sxs-lookup"><span data-stu-id="01d46-122">It can only contain lowercase letters and numbers and between 5-50 characters.</span></span> |
| <span data-ttu-id="01d46-123">Hizmet URI'si</span><span class="sxs-lookup"><span data-stu-id="01d46-123">Service URI</span></span> | <span data-ttu-id="01d46-124">Merhaba URI burada hello Web kancası POST bildirimlerini göndermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="01d46-124">hello URI where hello webhook should send POST notifications.</span></span> |
| <span data-ttu-id="01d46-125">Özel Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="01d46-125">Custom headers</span></span> | <span data-ttu-id="01d46-126">Merhaba POST isteği birlikte toopass istediğiniz üstbilgileri.</span><span class="sxs-lookup"><span data-stu-id="01d46-126">Headers you want toopass along with hello POST request.</span></span> <span data-ttu-id="01d46-127">İçinde olmalıdır "anahtar: değer" biçimi.</span><span class="sxs-lookup"><span data-stu-id="01d46-127">They should be in "key: value" format.</span></span> |
| <span data-ttu-id="01d46-128">Tetikleyici eylemleri</span><span class="sxs-lookup"><span data-stu-id="01d46-128">Trigger actions</span></span> | <span data-ttu-id="01d46-129">Merhaba Web kancası tetiklemek eylemler.</span><span class="sxs-lookup"><span data-stu-id="01d46-129">Actions that trigger hello webhook.</span></span> <span data-ttu-id="01d46-130">Şu anda Web kancalarını itme tarafından tetiklenen ve/veya Eylemler tooan resmini silin.</span><span class="sxs-lookup"><span data-stu-id="01d46-130">Currently webhooks can be triggered by push and/or delete actions tooan image.</span></span> |
| <span data-ttu-id="01d46-131">Durum</span><span class="sxs-lookup"><span data-stu-id="01d46-131">Status</span></span> | <span data-ttu-id="01d46-132">Merhaba Web kancası oluşturulduktan sonra başlangıç durumu.</span><span class="sxs-lookup"><span data-stu-id="01d46-132">hello status for hello webhook after it's created.</span></span> <span data-ttu-id="01d46-133">Varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="01d46-133">It's enabled by default.</span></span> |
| <span data-ttu-id="01d46-134">Kapsam</span><span class="sxs-lookup"><span data-stu-id="01d46-134">Scope</span></span> | <span data-ttu-id="01d46-135">hangi hello Web kancası works kapsamda Hello.</span><span class="sxs-lookup"><span data-stu-id="01d46-135">hello scope at which hello webhook works.</span></span> <span data-ttu-id="01d46-136">Varsayılan olarak tüm olayları hello kayıt defterinde hello kapsam içindir.</span><span class="sxs-lookup"><span data-stu-id="01d46-136">By default hello scope is for all events in hello registry.</span></span> <span data-ttu-id="01d46-137">Bu depo veya bir etiket için hello biçimi kullanılarak belirtilebilir "deposu: Etiket".</span><span class="sxs-lookup"><span data-stu-id="01d46-137">It can be specified for a repository or a tag by using hello format "repository: tag".</span></span> |

<span data-ttu-id="01d46-138">Örnek Web kancası form:</span><span class="sxs-lookup"><span data-stu-id="01d46-138">Example webhook form:</span></span>

![DCOS KULLANICI ARABİRİMİ](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a><span data-ttu-id="01d46-140">Web kancası Azure CLI oluşturma</span><span class="sxs-lookup"><span data-stu-id="01d46-140">Create webhook Azure CLI</span></span>

<span data-ttu-id="01d46-141">kullanarak bir Web kancası toocreate hello Azure CLI, kullanım hello [az acr Web kancası oluşturma](/cli/azure/acr/webhook#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="01d46-141">toocreate a webhook using hello Azure CLI, use hello [az acr webhook create](/cli/azure/acr/webhook#create) command.</span></span>

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a><span data-ttu-id="01d46-142">Test Web kancası</span><span class="sxs-lookup"><span data-stu-id="01d46-142">Test webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="01d46-143">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="01d46-143">Azure portal</span></span>

<span data-ttu-id="01d46-144">Önceki toousing hello Web kancası kapsayıcısı üzerinde görüntü gönderme ve silme eylemlerini, hello kullanılarak sınanabilir **Ping** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="01d46-144">Prior toousing hello webhook on container image push and delete actions, it can be tested using hello **Ping** button.</span></span> <span data-ttu-id="01d46-145">Kullanıldığında, uç nokta ve günlükleri yanıt hello genel post isteği toohello belirtilen hello Ping gönderir.</span><span class="sxs-lookup"><span data-stu-id="01d46-145">When used, hello Ping sends a generic post request toohello specified endpoint and logs hello response.</span></span> <span data-ttu-id="01d46-146">Bu yararlı olur Web kancası hello tooverify doğru şekilde ayarlanmış.</span><span class="sxs-lookup"><span data-stu-id="01d46-146">This is helpful tooverify that hello webhook has been set up correctly.</span></span>

1. <span data-ttu-id="01d46-147">Merhaba Web kancası tootest istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="01d46-147">Select hello webhook you want tootest.</span></span> 
2. <span data-ttu-id="01d46-148">Merhaba üst araç çubuğunda hello "Ping" eylemini seçin.</span><span class="sxs-lookup"><span data-stu-id="01d46-148">In hello top toolbar, select hello "Ping" action.</span></span> 
3. <span data-ttu-id="01d46-149">Merhaba istek ve yanıt denetleyin.</span><span class="sxs-lookup"><span data-stu-id="01d46-149">Check hello request and response.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="01d46-150">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="01d46-150">Azure CLI</span></span>

<span data-ttu-id="01d46-151">tootest bir ACR Web kancası hello Azure CLI ile kullanmak hello [az acr Web kancası ping](/cli/azure/acr/webhook#ping) komutu.</span><span class="sxs-lookup"><span data-stu-id="01d46-151">tootest an ACR webhook with hello Azure CLI, use hello [az acr webhook ping](/cli/azure/acr/webhook#ping) command.</span></span>

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

<span data-ttu-id="01d46-152">toosee hello sonuçları kullanmak hello [az acr Web kancası listesi-olayları](/cli/azure/acr/webhook#list-events) komutu.</span><span class="sxs-lookup"><span data-stu-id="01d46-152">toosee hello results, use hello [az acr webhook list-events](/cli/azure/acr/webhook#list-events) command.</span></span> 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a><span data-ttu-id="01d46-153">Web kancası silme</span><span class="sxs-lookup"><span data-stu-id="01d46-153">Delete webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="01d46-154">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="01d46-154">Azure portal</span></span>

<span data-ttu-id="01d46-155">Her Web kancası hello Web kancası ve hello Azure portal hello Sil düğmesini seçerek silinebilir.</span><span class="sxs-lookup"><span data-stu-id="01d46-155">Each webhook can be deleted by selecting hello webhook and then hello delete button on hello Azure portal.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="01d46-156">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="01d46-156">Azure CLI</span></span>

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```