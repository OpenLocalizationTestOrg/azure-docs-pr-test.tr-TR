---
title: "Azure CLI komut dosyası örneği - bir Azure Redis önbelleği Get ayrıntılarını | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - bir Azure Redis önbelleği Ayrıntıları Al"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 155924e6-00d5-4a8c-ba99-5189f300464a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: 9f4eb32227bd8a68837eabd58b9d058bc4995d17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-details-of-an-azure-redis-cache"></a><span data-ttu-id="c055f-103">Bir Azure Redis önbelleği ayrıntılarını alma</span><span class="sxs-lookup"><span data-stu-id="c055f-103">Get details of an Azure Redis Cache</span></span>

<span data-ttu-id="c055f-104">Bu senaryoda, sağlama durumu da dahil olmak üzere bir Azure Redis önbelleği örneği ayrıntılarını alma hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="c055f-104">In this scenario, you learn how to retrieve the details of an Azure Redis Cache instance, including its provisioning status.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="c055f-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="c055f-105">Sample script</span></span>

<span data-ttu-id="c055f-106">[!code-azurecli[Ana](../../../cli_scripts/redis-cache/show-cache/show-cache.sh "Azure Redis önbelleği")]</span><span class="sxs-lookup"><span data-stu-id="c055f-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/show-cache/show-cache.sh "Azure Redis Cache")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="c055f-107">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="c055f-107">Script explanation</span></span>

<span data-ttu-id="c055f-108">Bu komut dosyası, bir Azure Redis önbelleği örneği ayrıntılarını almak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="c055f-108">This script uses the following commands to retrieve the details of an Azure Redis Cache instance.</span></span> <span data-ttu-id="c055f-109">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="c055f-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c055f-110">Komut</span><span class="sxs-lookup"><span data-stu-id="c055f-110">Command</span></span> | <span data-ttu-id="c055f-111">Notlar</span><span class="sxs-lookup"><span data-stu-id="c055f-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c055f-112">az redis Göster</span><span class="sxs-lookup"><span data-stu-id="c055f-112">az redis show</span></span>](https://docs.microsoft.com/cli/azure/redis#show) | <span data-ttu-id="c055f-113">Bir Azure Redis önbelleği örneği ayrıntılarını alma.</span><span class="sxs-lookup"><span data-stu-id="c055f-113">Retrieve details of an Azure Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="c055f-114">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c055f-114">Next steps</span></span>

<span data-ttu-id="c055f-115">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c055f-115">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c055f-116">Ek Azure Redis önbelleği CLI kod örnekleri bulunabilir [Azure Redis önbelleği belgelerine](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c055f-116">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>