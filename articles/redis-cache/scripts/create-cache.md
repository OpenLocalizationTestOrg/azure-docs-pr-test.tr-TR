---
title: "aaaAzure CLI komut dosyası örneği - bir Azure Redis önbelleği oluşturma | Microsoft Docs"
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
ms.openlocfilehash: 85b007a426fbd4752034ec8663835963d140dd75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-redis-cache"></a><span data-ttu-id="05644-103">Azure Redis Cache oluşturma</span><span class="sxs-lookup"><span data-stu-id="05644-103">Create an Azure Redis Cache</span></span>

<span data-ttu-id="05644-104">Bu senaryoda, nasıl toocreate bir Azure Redis önbelleği öğrenin.</span><span class="sxs-lookup"><span data-stu-id="05644-104">In this scenario, you learn how toocreate an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="05644-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="05644-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/create-cache/create-cache.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="05644-106">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="05644-106">Script explanation</span></span>

<span data-ttu-id="05644-107">Bu komut dosyası komutları toocreate aşağıdaki hello bir kaynak grubu ve redis önbelleği kullanır.</span><span class="sxs-lookup"><span data-stu-id="05644-107">This script uses hello following commands toocreate a resource group and a redis cache.</span></span> <span data-ttu-id="05644-108">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="05644-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="05644-109">Komut</span><span class="sxs-lookup"><span data-stu-id="05644-109">Command</span></span> | <span data-ttu-id="05644-110">Notlar</span><span class="sxs-lookup"><span data-stu-id="05644-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="05644-111">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="05644-111">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="05644-112">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="05644-112">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="05644-113">az redis oluşturma</span><span class="sxs-lookup"><span data-stu-id="05644-113">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="05644-114">Redis önbelleği örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="05644-114">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="05644-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="05644-115">Next steps</span></span>

<span data-ttu-id="05644-116">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="05644-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="05644-117">Ek Azure Redis önbelleği CLI kod örnekleri hello bulunabilir [Azure Redis önbelleği belgelerine](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="05644-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
