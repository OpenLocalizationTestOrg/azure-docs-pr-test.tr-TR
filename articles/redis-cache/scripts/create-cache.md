---
title: "Azure CLI örnek komut dosyası - bir Azure Redis önbelleği oluşturma | Microsoft Docs"
description: "Azure CLI örnek komut dosyası - bir Azure Redis önbelleği oluşturma"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: afd7f6e0-9297-4c98-a95e-597be939cef7
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: c6b153d80de4cbf2bec1bc70d67be7befa0c5ec3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-redis-cache"></a><span data-ttu-id="cf543-103">Azure Redis Cache oluşturma</span><span class="sxs-lookup"><span data-stu-id="cf543-103">Create an Azure Redis Cache</span></span>

<span data-ttu-id="cf543-104">Bu senaryoda, bir Azure Redis önbelleği oluşturmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="cf543-104">In this scenario, you learn how to create an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="cf543-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="cf543-105">Sample script</span></span>

<span data-ttu-id="cf543-106">[!code-azurecli[Ana](../../../cli_scripts/redis-cache/create-cache/create-cache.sh "Azure Redis önbelleği")]</span><span class="sxs-lookup"><span data-stu-id="cf543-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/create-cache/create-cache.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="cf543-107">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="cf543-107">Script explanation</span></span>

<span data-ttu-id="cf543-108">Bu komut, bir kaynak grubu ve redis önbelleği oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="cf543-108">This script uses the following commands to create a resource group and a redis cache.</span></span> <span data-ttu-id="cf543-109">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="cf543-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="cf543-110">Komut</span><span class="sxs-lookup"><span data-stu-id="cf543-110">Command</span></span> | <span data-ttu-id="cf543-111">Notlar</span><span class="sxs-lookup"><span data-stu-id="cf543-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cf543-112">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="cf543-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="cf543-113">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cf543-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="cf543-114">az redis oluşturma</span><span class="sxs-lookup"><span data-stu-id="cf543-114">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="cf543-115">Redis önbelleği örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cf543-115">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="cf543-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cf543-116">Next steps</span></span>

<span data-ttu-id="cf543-117">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cf543-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="cf543-118">Ek Azure Redis önbelleği CLI kod örnekleri bulunabilir [Azure Redis önbelleği belgelerine](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="cf543-118">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>