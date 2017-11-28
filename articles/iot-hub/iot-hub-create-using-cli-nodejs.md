---
title: Azure CLI (azure.js) kullanarak bir IOT hub aaaCreate | Microsoft Docs
description: "Nasıl bir Azure IOT hub'ı kullanarak toocreate hello platformlar arası Azure CLI (azure.js)."
services: iot-hub
documentationcenter: .net
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: 46a17831-650c-41d9-b228-445c5bb423d3
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: boltean
ms.openlocfilehash: c2a7ea98500b0a0e55a39f4cdfea4605c92add94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli"></a><span data-ttu-id="0c075-103">Hello Azure CLI kullanarak IOT hub oluşturma</span><span class="sxs-lookup"><span data-stu-id="0c075-103">Create an IoT hub using hello Azure CLI</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="0c075-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="0c075-104">Introduction</span></span>

<span data-ttu-id="0c075-105">Azure CLI (azure.js) toocreate kullanın ve Azure IOT hub'ları program aracılığıyla yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c075-105">You can use Azure CLI (azure.js) toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="0c075-106">Bu makale size nasıl toouse hello Azure CLI (azure.js) toocreate IOT hub'ı gösterir.</span><span class="sxs-lookup"><span data-stu-id="0c075-106">This article shows you how toouse hello Azure CLI (azure.js) toocreate an IoT hub.</span></span>

<span data-ttu-id="0c075-107">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="0c075-107">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="0c075-108">Azure CLI (azure.js) – hello CLI hello Klasik ve bu makalede anlatıldığı gibi kaynak yönetimi dağıtım modelleri için.</span><span class="sxs-lookup"><span data-stu-id="0c075-108">Azure CLI (azure.js) – hello CLI for hello classic and resource management deployment models as described in this article.</span></span>
* <span data-ttu-id="0c075-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) -hello kaynak yönetimi dağıtım modeli için yeni nesil CLI hello.</span><span class="sxs-lookup"><span data-stu-id="0c075-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) - hello next generation CLI for hello resource management deployment model.</span></span>

<span data-ttu-id="0c075-110">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="0c075-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="0c075-111">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="0c075-111">An active Azure account.</span></span> <span data-ttu-id="0c075-112">Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c075-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="0c075-113">[Azure CLI 0.10.4] [ lnk-CLI-install] veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="0c075-113">[Azure CLI 0.10.4][lnk-CLI-install] or later.</span></span> <span data-ttu-id="0c075-114">Hello Azure CLI yüklenmiş zaten varsa, komutu aşağıdaki hello ile Merhaba geçerli sürümü hello komut isteminde doğrulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0c075-114">If you already have hello Azure CLI installed, you can validate hello current version at hello command prompt with hello following command:</span></span>

```azurecli
azure --version
```

> [!NOTE]
> <span data-ttu-id="0c075-115">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0c075-115">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0c075-116">Hello Azure CLI, Azure Kaynak Yöneticisi modunda olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="0c075-116">hello Azure CLI must be in Azure Resource Manager mode:</span></span>
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="0c075-117">Azure hesabınızı ve aboneliğinizi ayarlama</span><span class="sxs-lookup"><span data-stu-id="0c075-117">Set your Azure account and subscription</span></span>

1. <span data-ttu-id="0c075-118">Merhaba komut isteminde, komutu aşağıdaki hello yazarak oturum açma:</span><span class="sxs-lookup"><span data-stu-id="0c075-118">At hello command prompt, login by typing hello following command:</span></span>

   ```azurecli
    azure login
   ```

   <span data-ttu-id="0c075-119">Merhaba önerilen web tarayıcısı ve kod tooauthenticate kullanın.</span><span class="sxs-lookup"><span data-stu-id="0c075-119">Use hello suggested web browser and code tooauthenticate.</span></span>
1. <span data-ttu-id="0c075-120">Birden çok Azure aboneliğiniz varsa, tooAzure bağlanma verir tooall erişim kimlik bilgilerinizle ilişkili Azure abonelik hello.</span><span class="sxs-lookup"><span data-stu-id="0c075-120">If you have multiple Azure subscriptions, connecting tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="0c075-121">Görüntüleyebileceğiniz Azure abonelikleri hello ve hangisinin hello komutunu kullanarak Merhaba, varsayılandır belirleyin:</span><span class="sxs-lookup"><span data-stu-id="0c075-121">You can view hello Azure subscriptions, and identify which one is hello default, using hello command:</span></span>

   ```azurecli
    azure account list
   ```

   <span data-ttu-id="0c075-122">tooset hello abonelik bağlam altında toorun hello kalan hello komutlarını kullanmak istediğiniz:</span><span class="sxs-lookup"><span data-stu-id="0c075-122">tooset hello subscription context under which you want toorun hello rest of hello commands use:</span></span>

   ```azurecli
    azure account set <subscription name>
   ```

1. <span data-ttu-id="0c075-123">Bir kaynak grubu yoksa, bir adlı oluşturabilirsiniz **exampleResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="0c075-123">If you do not have a resource group, you can create one named **exampleResourceGroup**:</span></span>

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> <span data-ttu-id="0c075-124">Hello makale [hello Azure CLI toomanage Azure kullanmak kaynaklar ve kaynak grupları] [ lnk-CLI-arm] nasıl toouse hello Azure CLI toomanage Azure hakkında daha fazla bilgi sağlayan kaynakları.</span><span class="sxs-lookup"><span data-stu-id="0c075-124">hello article [Use hello Azure CLI toomanage Azure resources and resource groups][lnk-CLI-arm] provides more information about how toouse hello Azure CLI toomanage Azure resources.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="0c075-125">IOT Hub oluşturma</span><span class="sxs-lookup"><span data-stu-id="0c075-125">Create an IoT Hub</span></span>

<span data-ttu-id="0c075-126">Gerekli Parametreler:</span><span class="sxs-lookup"><span data-stu-id="0c075-126">Required parameters:</span></span>

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* <span data-ttu-id="0c075-127">**kaynak grubu**.</span><span class="sxs-lookup"><span data-stu-id="0c075-127">**resource-group**.</span></span> <span data-ttu-id="0c075-128">Merhaba kaynak grubu adı.</span><span class="sxs-lookup"><span data-stu-id="0c075-128">hello resource group name.</span></span> <span data-ttu-id="0c075-129">Merhaba büyük küçük harfe duyarlı alfasayısal, alt çizgi ve tire, 1-64 uzunluğu biçimidir.</span><span class="sxs-lookup"><span data-stu-id="0c075-129">hello format is case insensitive alphanumeric, underscore, and hyphen, 1-64 length.</span></span>
* <span data-ttu-id="0c075-130">**name**.</span><span class="sxs-lookup"><span data-stu-id="0c075-130">**name**.</span></span> <span data-ttu-id="0c075-131">oluşturulan hello IOT hub toobe Hello adı.</span><span class="sxs-lookup"><span data-stu-id="0c075-131">hello name of hello IoT hub toobe created.</span></span> <span data-ttu-id="0c075-132">Merhaba büyük küçük harfe duyarlı alfasayısal, alt çizgi ve tire, 3-50 uzunluğu biçimidir.</span><span class="sxs-lookup"><span data-stu-id="0c075-132">hello format is case insensitive alphanumeric, underscore, and hyphen, 3-50 length.</span></span>
* <span data-ttu-id="0c075-133">**Konum**.</span><span class="sxs-lookup"><span data-stu-id="0c075-133">**location**.</span></span> <span data-ttu-id="0c075-134">Başlangıç konumu (azure bölge/veri merkezi) tooprovision hello IOT hub.</span><span class="sxs-lookup"><span data-stu-id="0c075-134">hello location (azure region/datacenter) tooprovision hello IoT hub.</span></span>
* <span data-ttu-id="0c075-135">**SKU adı**.</span><span class="sxs-lookup"><span data-stu-id="0c075-135">**sku-name**.</span></span> <span data-ttu-id="0c075-136">Merhaba SKU'su, aşağıdakilerden birini Hello adı: [F1, S1, S2, S3].</span><span class="sxs-lookup"><span data-stu-id="0c075-136">hello name of hello sku, one of: [F1, S1, S2, S3].</span></span> <span data-ttu-id="0c075-137">Merhaba en son tam listesi için fiyatlandırma sayfası için IOT Hub toohello bakın.</span><span class="sxs-lookup"><span data-stu-id="0c075-137">For hello latest full list, refer toohello pricing page for IoT Hub.</span></span>
* <span data-ttu-id="0c075-138">**birimleri**.</span><span class="sxs-lookup"><span data-stu-id="0c075-138">**units**.</span></span> <span data-ttu-id="0c075-139">sağlanan birimleri Hello sayısı.</span><span class="sxs-lookup"><span data-stu-id="0c075-139">hello number of provisioned units.</span></span> <span data-ttu-id="0c075-140">Aralık: F1 [1-1]: S1, S2 [1-200]: [1-10] S3.</span><span class="sxs-lookup"><span data-stu-id="0c075-140">Range: F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span></span> <span data-ttu-id="0c075-141">IOT Hub birimleri toplam ileti sayısı ve hello sayısı aygıtlar üzerinde tooconnect istiyor.</span><span class="sxs-lookup"><span data-stu-id="0c075-141">IoT Hub units are based on your total message count and hello number of devices you want tooconnect.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

<span data-ttu-id="0c075-142">toosee tüm oluşturma için kullanılabilen parametreleri Merhaba, komut istemi'nde hello Yardım komutunu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0c075-142">toosee all hello parameters available for creation, you can use hello help command in command prompt:</span></span>

```azurecli
azure iothub create -h
```

<span data-ttu-id="0c075-143">Örnek: bir IOT Hub adı verilen toocreate **exampleIoTHubName** hello kaynak grubunda **exampleResourceGroup**çalıştırın hello komutu aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="0c075-143">Quick example: toocreate an IoT Hub called **exampleIoTHubName** in hello resource group **exampleResourceGroup**, run hello following command:</span></span>

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> <span data-ttu-id="0c075-144">Bu Azure CLI komut S1 standart IOT için faturalandırılır hub'ı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0c075-144">This Azure CLI command creates an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="0c075-145">Merhaba IOT hub'ı silebilmek için **exampleIoTHubName** komutu kullanarak:</span><span class="sxs-lookup"><span data-stu-id="0c075-145">You can delete hello IoT hub **exampleIoTHubName** using following command:</span></span>
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a><span data-ttu-id="0c075-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0c075-146">Next steps</span></span>

<span data-ttu-id="0c075-147">IOT hub'ı geliştirme hakkında daha fazla toolearn aşağıdaki makaleye bakın hello bakın:</span><span class="sxs-lookup"><span data-stu-id="0c075-147">toolearn more about developing for IoT Hub, see hello following article:</span></span>

* <span data-ttu-id="0c075-148">[IOT SDK'ları][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="0c075-148">[IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="0c075-149">toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:</span><span class="sxs-lookup"><span data-stu-id="0c075-149">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="0c075-150">[Hello Azure portal toomanage IOT hub'ı kullanma][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="0c075-150">[Using hello Azure portal toomanage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
