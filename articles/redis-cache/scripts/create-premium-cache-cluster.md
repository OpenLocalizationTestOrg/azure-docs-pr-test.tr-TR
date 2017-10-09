---
title: "aaaAzure CLI komut dosyası örneği - kümeleme Premium Azure Redis önbelleği oluşturma | Microsoft Docs"
description: "Azure CLI betik örnek - Kümeleme ile Azure Redis önbelleği Premium katmanı oluşturma"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 07bcceae-2521-4fe3-b88f-ed833104ddd2
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: ca34d40059b282cb2abc7e3e2b8771226029744c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-premium-azure-redis-cache-with-clustering"></a><span data-ttu-id="8bbb6-103">Kümeleme Premium Azure Redis önbelleği oluşturma</span><span class="sxs-lookup"><span data-stu-id="8bbb6-103">Create a Premium Azure Redis Cache with clustering</span></span>

<span data-ttu-id="8bbb6-104">Bu senaryoda, nasıl toocreate bir 6 GB Premium Katmanı'Kümeleme ile Azure Redis önbelleği etkin ve iki parça öğrenin.</span><span class="sxs-lookup"><span data-stu-id="8bbb6-104">In this scenario, you learn how toocreate a 6 GB Premium tier Azure Redis Cache with clustering enabled and two shards.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="8bbb6-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="8bbb6-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="8bbb6-106">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="8bbb6-106">Script explanation</span></span>

<span data-ttu-id="8bbb6-107">Bu komut dosyasını etkinleştir Kümeleme ile bir kaynak grubu ve Premium katmanı redis önbelleği komutları toocreate aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="8bbb6-107">This script uses hello following commands toocreate a resource group and a Premium tier redis cache with clustering enable.</span></span> <span data-ttu-id="8bbb6-108">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="8bbb6-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="8bbb6-109">Komut</span><span class="sxs-lookup"><span data-stu-id="8bbb6-109">Command</span></span> | <span data-ttu-id="8bbb6-110">Notlar</span><span class="sxs-lookup"><span data-stu-id="8bbb6-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8bbb6-111">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="8bbb6-111">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="8bbb6-112">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8bbb6-112">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8bbb6-113">az redis oluşturma</span><span class="sxs-lookup"><span data-stu-id="8bbb6-113">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="8bbb6-114">Redis önbelleği örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8bbb6-114">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="8bbb6-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8bbb6-115">Next steps</span></span>

<span data-ttu-id="8bbb6-116">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8bbb6-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8bbb6-117">Ek Azure Redis önbelleği CLI kod örnekleri hello bulunabilir [Azure Redis önbelleği belgelerine](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8bbb6-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
