---
title: "Azure kapsayıcı kayıt defteri kancalarını | Microsoft Docs"
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
ms.openlocfilehash: d0190f5725671c320d92b897f0dcef7a526a86e3
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="using-azure-container-registry-webhooks---azure-portal"></a><span data-ttu-id="d5f29-104">Azure kapsayıcı kayıt defteri kancalarını - Azure portalını kullanma</span><span class="sxs-lookup"><span data-stu-id="d5f29-104">Using Azure Container Registry webhooks - Azure portal</span></span>

<span data-ttu-id="d5f29-105">Azure kapsayıcı kayıt defteri depolar ve özel Docker kapsayıcısı görüntüleri, benzer Docker hub'a genel Docker görüntüleri depolayan şekilde yönetir.</span><span class="sxs-lookup"><span data-stu-id="d5f29-105">An Azure container registry stores and manages private Docker container images, similar to the way Docker Hub stores public Docker images.</span></span> <span data-ttu-id="d5f29-106">Web kancalarını belirli eylemleri, kayıt defteri depoları biri gerçekleştiğinde tetikleyici olaylar için kullanın.</span><span class="sxs-lookup"><span data-stu-id="d5f29-106">You use webhooks to trigger events when certain actions take place in one of your registry repositories.</span></span> <span data-ttu-id="d5f29-107">Web kancası kayıt defteri düzeyinde olaylara yanıt verebilir veya belirli depo etiketi kadar kapsamlı.</span><span class="sxs-lookup"><span data-stu-id="d5f29-107">Webhooks can respond to events at the registry level or they can be scoped down to a specific repository tag.</span></span> 

<span data-ttu-id="d5f29-108">Daha fazla arka plan ve kavramları için bkz: [genel bakış](./container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="d5f29-108">For more background and concepts, see the [overview](./container-registry-intro.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5f29-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d5f29-109">Prerequisites</span></span> 

- <span data-ttu-id="d5f29-110">Azure kapsayıcı kayıt defteri - yönetilen Azure aboneliğinizde bir yönetilen kapsayıcı kayıt oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d5f29-110">Azure container managed registry - Create a managed container registry in your Azure subscription.</span></span> <span data-ttu-id="d5f29-111">Örneğin, Azure portalında veya Azure CLI 2.0 kullanın.</span><span class="sxs-lookup"><span data-stu-id="d5f29-111">For example, use the Azure portal or the Azure CLI 2.0.</span></span> 
- <span data-ttu-id="d5f29-112">Docker CLI - yerel bilgisayarınıza Docker ana bilgisayar olarak ayarlayabilir ve Docker CLI komutlara erişmek için Docker altyapısına yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d5f29-112">Docker CLI - To set up your local computer as a Docker host and access the Docker CLI commands, install Docker Engine.</span></span> 

## <a name="create-webhook-azure-portal"></a><span data-ttu-id="d5f29-113">Azure portal Web kancası oluşturma</span><span class="sxs-lookup"><span data-stu-id="d5f29-113">Create webhook Azure portal</span></span>

1. <span data-ttu-id="d5f29-114">Azure portalında oturum açın ve Web kancalarını oluşturmak istediğiniz kayıt defteri gidin.</span><span class="sxs-lookup"><span data-stu-id="d5f29-114">Log in to the Azure portal and navigate to the registry in which you want to create webhooks.</span></span> 

2. <span data-ttu-id="d5f29-115">Kapsayıcı dikey penceresinde "Kancalarını" sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="d5f29-115">In the container blade, select the "Webhooks" tab.</span></span> 

3. <span data-ttu-id="d5f29-116">"Ekle" Web kancası dikey araç çubuğundan seçin.</span><span class="sxs-lookup"><span data-stu-id="d5f29-116">Select "Add" from the webhook blade toolbar.</span></span> 

4. <span data-ttu-id="d5f29-117">Tamamlamak *Web kancası oluşturma* form aşağıdaki bilgilerle:</span><span class="sxs-lookup"><span data-stu-id="d5f29-117">Complete the *Create Webhook* form with the following information:</span></span>

| <span data-ttu-id="d5f29-118">Değer</span><span class="sxs-lookup"><span data-stu-id="d5f29-118">Value</span></span> | <span data-ttu-id="d5f29-119">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d5f29-119">Description</span></span> |
|---|---|
| <span data-ttu-id="d5f29-120">Ad</span><span class="sxs-lookup"><span data-stu-id="d5f29-120">Name</span></span> | <span data-ttu-id="d5f29-121">Web kancası için vermek istediğiniz adı.</span><span class="sxs-lookup"><span data-stu-id="d5f29-121">The name you want to give to the webhook.</span></span> <span data-ttu-id="d5f29-122">Ad yalnızca küçük harfler ve sayılar içerebilir ve 5-50 karakter arasında.</span><span class="sxs-lookup"><span data-stu-id="d5f29-122">It can only contain lowercase letters and numbers and between 5-50 characters.</span></span> |
| <span data-ttu-id="d5f29-123">Hizmet URI'si</span><span class="sxs-lookup"><span data-stu-id="d5f29-123">Service URI</span></span> | <span data-ttu-id="d5f29-124">Web kancası POST bildirimleri burada göndermesi gereken URI.</span><span class="sxs-lookup"><span data-stu-id="d5f29-124">The URI where the webhook should send POST notifications.</span></span> |
| <span data-ttu-id="d5f29-125">Özel Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="d5f29-125">Custom headers</span></span> | <span data-ttu-id="d5f29-126">Üstbilgiler POST istekle birlikte geçirmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5f29-126">Headers you want to pass along with the POST request.</span></span> <span data-ttu-id="d5f29-127">İçinde olmalıdır "anahtar: değer" biçimi.</span><span class="sxs-lookup"><span data-stu-id="d5f29-127">They should be in "key: value" format.</span></span> |
| <span data-ttu-id="d5f29-128">Tetikleyici eylemleri</span><span class="sxs-lookup"><span data-stu-id="d5f29-128">Trigger actions</span></span> | <span data-ttu-id="d5f29-129">Web kancası tetiklemek eylemler.</span><span class="sxs-lookup"><span data-stu-id="d5f29-129">Actions that trigger the webhook.</span></span> <span data-ttu-id="d5f29-130">Şu anda Web kancalarını itme tarafından tetiklenen ve/veya görüntüye eylemlerini silme.</span><span class="sxs-lookup"><span data-stu-id="d5f29-130">Currently webhooks can be triggered by push and/or delete actions to an image.</span></span> |
| <span data-ttu-id="d5f29-131">Durum</span><span class="sxs-lookup"><span data-stu-id="d5f29-131">Status</span></span> | <span data-ttu-id="d5f29-132">Web kancası oluşturulduktan sonra durumu.</span><span class="sxs-lookup"><span data-stu-id="d5f29-132">The status for the webhook after it's created.</span></span> <span data-ttu-id="d5f29-133">Varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="d5f29-133">It's enabled by default.</span></span> |
| <span data-ttu-id="d5f29-134">Kapsam</span><span class="sxs-lookup"><span data-stu-id="d5f29-134">Scope</span></span> | <span data-ttu-id="d5f29-135">Web kancası çalıştığı kapsamı.</span><span class="sxs-lookup"><span data-stu-id="d5f29-135">The scope at which the webhook works.</span></span> <span data-ttu-id="d5f29-136">Varsayılan olarak tüm olayları kayıt defterinde kapsamı içindir.</span><span class="sxs-lookup"><span data-stu-id="d5f29-136">By default the scope is for all events in the registry.</span></span> <span data-ttu-id="d5f29-137">Bu depo veya bir etiket için şu biçimi kullanarak belirtilebilir "deposu: Etiket".</span><span class="sxs-lookup"><span data-stu-id="d5f29-137">It can be specified for a repository or a tag by using the format "repository: tag".</span></span> |

<span data-ttu-id="d5f29-138">Örnek Web kancası form:</span><span class="sxs-lookup"><span data-stu-id="d5f29-138">Example webhook form:</span></span>

![DCOS KULLANICI ARABİRİMİ](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a><span data-ttu-id="d5f29-140">Web kancası Azure CLI oluşturma</span><span class="sxs-lookup"><span data-stu-id="d5f29-140">Create webhook Azure CLI</span></span>

<span data-ttu-id="d5f29-141">Azure CLI kullanarak bir Web kancası oluşturmak üzere kullanmanız [az acr Web kancası oluşturma](/cli/azure/acr/webhook#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="d5f29-141">To create a webhook using the Azure CLI, use the [az acr webhook create](/cli/azure/acr/webhook#create) command.</span></span>

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a><span data-ttu-id="d5f29-142">Test Web kancası</span><span class="sxs-lookup"><span data-stu-id="d5f29-142">Test webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="d5f29-143">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="d5f29-143">Azure portal</span></span>

<span data-ttu-id="d5f29-144">Kullanarak önceki kapsayıcısı üzerinde Web kancası görüntü gönderme ve silme eylemlerini, kullanılarak sınanabilir **Ping** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d5f29-144">Prior to using the webhook on container image push and delete actions, it can be tested using the **Ping** button.</span></span> <span data-ttu-id="d5f29-145">Kullanıldığında, ping işlemi için belirtilen uç nokta bir genel post isteği gönderir ve yanıt günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="d5f29-145">When used, the Ping sends a generic post request to the specified endpoint and logs the response.</span></span> <span data-ttu-id="d5f29-146">Bu, Web kancası doğru şekilde ayarlanmış olması gerektiğini doğrulamak yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="d5f29-146">This is helpful to verify that the webhook has been set up correctly.</span></span>

1. <span data-ttu-id="d5f29-147">Test etmek istediğiniz Web kancası seçin.</span><span class="sxs-lookup"><span data-stu-id="d5f29-147">Select the webhook you want to test.</span></span> 
2. <span data-ttu-id="d5f29-148">Üst araç çubuğunda, "Ping" eylemini seçin.</span><span class="sxs-lookup"><span data-stu-id="d5f29-148">In the top toolbar, select the "Ping" action.</span></span> 
3. <span data-ttu-id="d5f29-149">İstek ve yanıt denetleyin.</span><span class="sxs-lookup"><span data-stu-id="d5f29-149">Check the request and response.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="d5f29-150">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d5f29-150">Azure CLI</span></span>

<span data-ttu-id="d5f29-151">Azure CLI ile bir ACR Web kancası sınamak için kullanın [az acr Web kancası ping](/cli/azure/acr/webhook#ping) komutu.</span><span class="sxs-lookup"><span data-stu-id="d5f29-151">To test an ACR webhook with the Azure CLI, use the [az acr webhook ping](/cli/azure/acr/webhook#ping) command.</span></span>

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

<span data-ttu-id="d5f29-152">Sonuçları görmek için [az acr Web kancası listesi-olayları](/cli/azure/acr/webhook#list-events) komutu.</span><span class="sxs-lookup"><span data-stu-id="d5f29-152">To see the results, use the [az acr webhook list-events](/cli/azure/acr/webhook#list-events) command.</span></span> 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a><span data-ttu-id="d5f29-153">Web kancası silme</span><span class="sxs-lookup"><span data-stu-id="d5f29-153">Delete webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="d5f29-154">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="d5f29-154">Azure portal</span></span>

<span data-ttu-id="d5f29-155">Her Web kancası Web kancası ve Azure Portal'da Sil düğmesini seçerek silinebilir.</span><span class="sxs-lookup"><span data-stu-id="d5f29-155">Each webhook can be deleted by selecting the webhook and then the delete button on the Azure portal.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="d5f29-156">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d5f29-156">Azure CLI</span></span>

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```