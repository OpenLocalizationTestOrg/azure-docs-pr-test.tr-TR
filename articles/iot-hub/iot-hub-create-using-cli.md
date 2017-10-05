---
title: "Azure CLI (az.py) kullanarak IOT Hub oluşturma | Microsoft Docs"
description: "Platformlar arası Azure CLI 2.0 (az.py) kullanan bir Azure IOT hub oluşturma"
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
ms.openlocfilehash: 161089159999a4a63a39b059e69a08b7a9297445
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-iot-hub-using-the-azure-cli-20"></a><span data-ttu-id="87bc1-103">Azure CLI 2.0 kullanan IOT hub oluşturma</span><span class="sxs-lookup"><span data-stu-id="87bc1-103">Create an IoT hub using the Azure CLI 2.0</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="87bc1-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="87bc1-104">Introduction</span></span>

<span data-ttu-id="87bc1-105">Azure CLI 2.0 (az.py) oluşturmak ve Azure IOT hub'ları programlı olarak yönetmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87bc1-105">You can use Azure CLI 2.0 (az.py) to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="87bc1-106">Bu makalede Azure CLI 2.0 (az.py) IOT hub'ı oluşturmak için nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="87bc1-106">This article shows you how to use the Azure CLI 2.0 (az.py) to create an IoT hub.</span></span>

<span data-ttu-id="87bc1-107">Görevi aşağıdaki CLI sürümlerinden birini kullanarak tamamlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="87bc1-107">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="87bc1-108">[Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) – Klasik ve kaynak yönetimi dağıtım modelleri için CLI.</span><span class="sxs-lookup"><span data-stu-id="87bc1-108">[Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) – the CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="87bc1-109">Azure CLI 2.0 (az.py) - Bu makalede anlatıldığı gibi kaynak yönetimi dağıtım modeli için yeni nesil CLI.</span><span class="sxs-lookup"><span data-stu-id="87bc1-109">Azure CLI 2.0 (az.py) - the next generation CLI for the resource management deployment model as described in this article.</span></span>

<span data-ttu-id="87bc1-110">Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="87bc1-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="87bc1-111">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="87bc1-111">An active Azure account.</span></span> <span data-ttu-id="87bc1-112">Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87bc1-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="87bc1-113">[Azure CLI 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="87bc1-113">[Azure CLI 2.0][lnk-CLI-install].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="87bc1-114">Oturum açma ve Azure hesabınızı ayarlama</span><span class="sxs-lookup"><span data-stu-id="87bc1-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="87bc1-115">Azure hesabınızda oturum açın ve aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="87bc1-115">Sign in to your Azure account and select your subscription.</span></span>

1. <span data-ttu-id="87bc1-116">Komut istemine [oturum açma komut][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="87bc1-116">At the command prompt, run the [login command][lnk-login-command]:</span></span>
    
    ```azurecli
    az login
    ```

    <span data-ttu-id="87bc1-117">Kod kullanarak kimlik doğrulaması yapmak için yönergeleri izleyin ve bir web tarayıcısı aracılığıyla Azure hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="87bc1-117">Follow the instructions to authenticate using the code and sign in to your Azure account through a web browser.</span></span>

2. <span data-ttu-id="87bc1-118">Birden çok Azure aboneliğiniz varsa, Azure'da oturum açma kimlik bilgilerinizle ilişkilendirilen tüm Azure hesaplar için size erişim verir.</span><span class="sxs-lookup"><span data-stu-id="87bc1-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure accounts associated with your credentials.</span></span> <span data-ttu-id="87bc1-119">Aşağıdaki [Azure hesapları listelemek için komut] [ lnk-az-account-command] kullanmanız için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="87bc1-119">Use the following [command to list the Azure accounts][lnk-az-account-command] available for you to use:</span></span>
    
    ```azurecli
    az account list 
    ```

    <span data-ttu-id="87bc1-120">IOT hub'ınızı oluşturması için komutları çalıştırmak için kullanmak istediğiniz aboneliği seçmek için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="87bc1-120">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="87bc1-121">Önceki komut çıktısı abonelik adı veya kimliği kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="87bc1-121">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="create-an-iot-hub"></a><span data-ttu-id="87bc1-122">IOT Hub oluşturma</span><span class="sxs-lookup"><span data-stu-id="87bc1-122">Create an IoT Hub</span></span>

<span data-ttu-id="87bc1-123">Bir kaynak grubu oluşturun ve IOT hub'ı eklemek için Azure CLI kullanın.</span><span class="sxs-lookup"><span data-stu-id="87bc1-123">Use the Azure CLI to create a resource group and then add an IoT hub.</span></span>

1. <span data-ttu-id="87bc1-124">IOT hub'ı oluşturduğunuzda, bir kaynak grubunda oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="87bc1-124">When you create an IoT hub, you must create it in a resource group.</span></span> <span data-ttu-id="87bc1-125">Varolan bir kaynak grubunu kullanın veya aşağıdaki komutu çalıştırarak [bir kaynak grubu oluşturmak için komutu][lnk-az-resource-command]:</span><span class="sxs-lookup"><span data-stu-id="87bc1-125">Either use an existing resource group, or run the following [command to create a resource group][lnk-az-resource-command]:</span></span>
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > <span data-ttu-id="87bc1-126">Önceki örnekte Batı ABD konumunda kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="87bc1-126">The previous example creates the resource group in the West US location.</span></span> <span data-ttu-id="87bc1-127">Komutunu çalıştırarak kullanılabilir konumların bir listesini görüntüleyebilirsiniz `az account list-locations -o table`.</span><span class="sxs-lookup"><span data-stu-id="87bc1-127">You can view a list of available locations by running the command `az account list-locations -o table`.</span></span>
    >
    >

2. <span data-ttu-id="87bc1-128">Aşağıdaki komutu çalıştırarak [IOT hub'ı oluşturmak için komutu] [ lnk-az-iot-command] kaynak grubunuzdaki IOT hub'ınız için genel benzersiz bir ad kullanarak:</span><span class="sxs-lookup"><span data-stu-id="87bc1-128">Run the following [command to create an IoT hub][lnk-az-iot-command] in your resource group, using a globally unique name for your IoT hub:</span></span>
    
    ```azurecli
    az iot hub create --name {your iot hub name} --resource-group {your resource group name} --sku S1
    ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


> [!NOTE]
> <span data-ttu-id="87bc1-129">Önceki komutu fiyatlandırma katmanı için faturalandırılır S1 bir IOT hub oluşturur.</span><span class="sxs-lookup"><span data-stu-id="87bc1-129">The previous command creates an IoT hub in the S1 pricing tier for which you are billed.</span></span> <span data-ttu-id="87bc1-130">Daha fazla bilgi için bkz: [Azure IOT Hub fiyatlandırma][lnk-iot-pricing].</span><span class="sxs-lookup"><span data-stu-id="87bc1-130">For more information, see [Azure IoT Hub pricing][lnk-iot-pricing].</span></span>
>
>

## <a name="remove-an-iot-hub"></a><span data-ttu-id="87bc1-131">IOT hub'ı kaldırma</span><span class="sxs-lookup"><span data-stu-id="87bc1-131">Remove an IoT Hub</span></span>

<span data-ttu-id="87bc1-132">Azure CLI için kullanabileceğiniz [tek başına bir kaynak silme][lnk-az-resource-command]bir IOT hub'ı veya silme gibi bir kaynak grubu ve tüm IOT hub'ları da dahil olmak üzere tüm kaynaklarını,.</span><span class="sxs-lookup"><span data-stu-id="87bc1-132">You can use the Azure CLI to [delete an individual resource][lnk-az-resource-command], such as an IoT hub, or delete a resource group and all its resources, including any IoT hubs.</span></span>

<span data-ttu-id="87bc1-133">Bir IOT hub'ını silmek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="87bc1-133">To delete an IoT hub, run the following command:</span></span>

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

<span data-ttu-id="87bc1-134">Bir kaynak grubu ve tüm kaynaklarını silmek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="87bc1-134">To delete a resource group and all its resources, run the following command:</span></span>

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a><span data-ttu-id="87bc1-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="87bc1-135">Next steps</span></span>
<span data-ttu-id="87bc1-136">IOT Hub için geliştirme hakkında daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="87bc1-136">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="87bc1-137">[IOT Hub Geliştirici Kılavuzu][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="87bc1-137">[IoT Hub developer guide][lnk-devguide]</span></span>

<span data-ttu-id="87bc1-138">Daha fazla IOT hub'ı özelliklerini keşfetmek için bkz:</span><span class="sxs-lookup"><span data-stu-id="87bc1-138">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="87bc1-139">[IOT hub'ı yönetmek için Azure portalını kullanma][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="87bc1-139">[Using the Azure portal to manage IoT Hub][lnk-portal]</span></span>

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
