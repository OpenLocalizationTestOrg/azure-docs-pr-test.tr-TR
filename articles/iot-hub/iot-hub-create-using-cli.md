---
title: Azure CLI (az.py) kullanarak bir IOT Hub aaaCreate | Microsoft Docs
description: "Nasıl bir Azure IOT hub'ı kullanarak toocreate hello platformlar arası Azure CLI 2.0 (az.py)."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-hub
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 9c9639235c2ac343e6ceb9578291dafaea26ea24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli-20"></a><span data-ttu-id="ade94-103">Hello Azure CLI 2.0 kullanarak IOT hub oluşturma</span><span class="sxs-lookup"><span data-stu-id="ade94-103">Create an IoT hub using hello Azure CLI 2.0</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="ade94-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="ade94-104">Introduction</span></span>

<span data-ttu-id="ade94-105">Azure CLI 2.0 (az.py) toocreate kullanın ve Azure IOT hub'ları program aracılığıyla yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ade94-105">You can use Azure CLI 2.0 (az.py) toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="ade94-106">Bu makale size nasıl toouse hello Azure CLI 2.0 (az.py) toocreate IOT hub'ı gösterir.</span><span class="sxs-lookup"><span data-stu-id="ade94-106">This article shows you how toouse hello Azure CLI 2.0 (az.py) toocreate an IoT hub.</span></span>

<span data-ttu-id="ade94-107">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="ade94-107">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="ade94-108">[Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) – hello Klasik ve kaynak yönetimi dağıtım modelleri için CLI hello.</span><span class="sxs-lookup"><span data-stu-id="ade94-108">[Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) – hello CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="ade94-109">Azure CLI 2.0 (az.py) - Bu makalede anlatıldığı gibi hello kaynak yönetimi dağıtım modeli için yeni nesil CLI hello.</span><span class="sxs-lookup"><span data-stu-id="ade94-109">Azure CLI 2.0 (az.py) - hello next generation CLI for hello resource management deployment model as described in this article.</span></span>

<span data-ttu-id="ade94-110">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="ade94-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="ade94-111">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="ade94-111">An active Azure account.</span></span> <span data-ttu-id="ade94-112">Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ade94-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="ade94-113">[Azure CLI 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="ade94-113">[Azure CLI 2.0][lnk-CLI-install].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="ade94-114">Oturum açma ve Azure hesabınızı ayarlama</span><span class="sxs-lookup"><span data-stu-id="ade94-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="ade94-115">Tooyour Azure hesabı oturum ve aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="ade94-115">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="ade94-116">Merhaba Hello komut isteminde çalıştırmak [oturum açma komut][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="ade94-116">At hello command prompt, run hello [login command][lnk-login-command]:</span></span>
    
    ```azurecli
    az login
    ```

    <span data-ttu-id="ade94-117">Merhaba yönergeleri tooauthenticate Hello kod kullanarak izleyin ve oturum açma tooyour bir web tarayıcısı aracılığıyla Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="ade94-117">Follow hello instructions tooauthenticate using hello code and sign in tooyour Azure account through a web browser.</span></span>

2. <span data-ttu-id="ade94-118">Birden çok Azure aboneliğiniz varsa tooAzure imzalama tooall erişim verir kimlik bilgilerinizle ilişkili Azure hesapları hello.</span><span class="sxs-lookup"><span data-stu-id="ade94-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure accounts associated with your credentials.</span></span> <span data-ttu-id="ade94-119">Merhaba aşağıdaki kullanın [komutu toolist hello Azure hesapları] [ lnk-az-account-command] , toouse için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="ade94-119">Use hello following [command toolist hello Azure accounts][lnk-az-account-command] available for you toouse:</span></span>
    
    ```azurecli
    az account list 
    ```

    <span data-ttu-id="ade94-120">IOT hub'ınızı toocreate toouse toorun hello komutları istediğiniz komut tooselect abonelik aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="ade94-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="ade94-121">Merhaba hello önceki komutunun çıktısından hello abonelik adı veya kimliği kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ade94-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="create-an-iot-hub"></a><span data-ttu-id="ade94-122">IOT Hub oluşturma</span><span class="sxs-lookup"><span data-stu-id="ade94-122">Create an IoT Hub</span></span>

<span data-ttu-id="ade94-123">Hello Azure CLI toocreate bir kaynak grubu ve IOT hub'ı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ade94-123">Use hello Azure CLI toocreate a resource group and then add an IoT hub.</span></span>

1. <span data-ttu-id="ade94-124">IOT hub'ı oluşturduğunuzda, bir kaynak grubunda oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ade94-124">When you create an IoT hub, you must create it in a resource group.</span></span> <span data-ttu-id="ade94-125">Var olan bir kaynak grubunu kullanabilir veya hello aşağıdaki komutu çalıştırarak [komutu toocreate bir kaynak grubu][lnk-az-resource-command]:</span><span class="sxs-lookup"><span data-stu-id="ade94-125">Either use an existing resource group, or run hello following [command toocreate a resource group][lnk-az-resource-command]:</span></span>
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > <span data-ttu-id="ade94-126">Merhaba önceki örnek hello Batı ABD konumu hello kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ade94-126">hello previous example creates hello resource group in hello West US location.</span></span> <span data-ttu-id="ade94-127">Merhaba komutu çalıştırarak kullanılabilir konumların bir listesini görüntüleyebilirsiniz `az account list-locations -o table`.</span><span class="sxs-lookup"><span data-stu-id="ade94-127">You can view a list of available locations by running hello command `az account list-locations -o table`.</span></span>
    >
    >

2. <span data-ttu-id="ade94-128">Merhaba aşağıdaki komutu çalıştırarak [komutu toocreate IOT hub'ı] [ lnk-az-iot-command] kaynak grubunuzdaki IOT hub'ınız için genel benzersiz bir ad kullanarak:</span><span class="sxs-lookup"><span data-stu-id="ade94-128">Run hello following [command toocreate an IoT hub][lnk-az-iot-command] in your resource group, using a globally unique name for your IoT hub:</span></span>
    
    ```azurecli
    az iot hub create --name {your iot hub name} --resource-group {your resource group name} --sku S1
    ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


> [!NOTE]
> <span data-ttu-id="ade94-129">Merhaba önceki komutu fiyatlandırma katmanı için faturalandırılır hello S1 IOT hub'ı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ade94-129">hello previous command creates an IoT hub in hello S1 pricing tier for which you are billed.</span></span> <span data-ttu-id="ade94-130">Daha fazla bilgi için bkz: [Azure IOT Hub fiyatlandırma][lnk-iot-pricing].</span><span class="sxs-lookup"><span data-stu-id="ade94-130">For more information, see [Azure IoT Hub pricing][lnk-iot-pricing].</span></span>
>
>

## <a name="remove-an-iot-hub"></a><span data-ttu-id="ade94-131">IOT hub'ı kaldırma</span><span class="sxs-lookup"><span data-stu-id="ade94-131">Remove an IoT Hub</span></span>

<span data-ttu-id="ade94-132">Hello Azure CLI kullanabileceğine[tek başına bir kaynak silme][lnk-az-resource-command]bir IOT hub'ı veya silme gibi bir kaynak grubu ve tüm IOT hub'ları da dahil olmak üzere tüm kaynaklarını,.</span><span class="sxs-lookup"><span data-stu-id="ade94-132">You can use hello Azure CLI too[delete an individual resource][lnk-az-resource-command], such as an IoT hub, or delete a resource group and all its resources, including any IoT hubs.</span></span>

<span data-ttu-id="ade94-133">bir IOT hub toodelete hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ade94-133">toodelete an IoT hub, run hello following command:</span></span>

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

<span data-ttu-id="ade94-134">bir kaynak grubu ve tüm kaynaklarını, aşağıdaki çalışma hello komutu toodelete:</span><span class="sxs-lookup"><span data-stu-id="ade94-134">toodelete a resource group and all its resources, run hello following command:</span></span>

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a><span data-ttu-id="ade94-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ade94-135">Next steps</span></span>
<span data-ttu-id="ade94-136">IOT hub'ı geliştirme hakkında daha fazla toolearn makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="ade94-136">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="ade94-137">[IOT Hub Geliştirici Kılavuzu][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="ade94-137">[IoT Hub developer guide][lnk-devguide]</span></span>

<span data-ttu-id="ade94-138">toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:</span><span class="sxs-lookup"><span data-stu-id="ade94-138">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="ade94-139">[Hello Azure portal toomanage IOT hub'ı kullanma][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="ade94-139">[Using hello Azure portal toomanage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-devguide]: iot-hub-devguide.md
[lnk-portal]: iot-hub-create-through-portal.md 
