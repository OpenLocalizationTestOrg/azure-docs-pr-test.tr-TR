---
title: "Azure CLI komut dosyası örneği - Get ana bilgisayar adı, bağlantı noktaları ve Azure Redis önbelleği için anahtarları | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - Get ana bilgisayar adı, bağlantı noktaları ve Azure Redis önbelleği örneği için anahtarları"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 761eb24e-2ba7-418d-8fc3-431153e69a90
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: cd9adc784bceb0fff5e7c2bbee2be0950c51c8f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-hostname-ports-and-keys-for-azure-redis-cache"></a><span data-ttu-id="da39a-103">Azure Redis önbelleği için ana bilgisayar adı, bağlantı noktalarını ve anahtarları alma</span><span class="sxs-lookup"><span data-stu-id="da39a-103">Get the hostname, ports, and keys for Azure Redis Cache</span></span>

<span data-ttu-id="da39a-104">Bu senaryoda, ana bilgisayar adı, bağlantı noktaları ve Azure Redis önbelleği örneğine bağlanmak için kullanılan anahtarlarını alma hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="da39a-104">In this scenario, you learn how to retrieve the hostname, ports, and keys used to connect to an Azure Redis Cache instance.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="da39a-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="da39a-105">Sample script</span></span>

<span data-ttu-id="da39a-106">[!code-azurecli[Ana](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis önbelleği")]</span><span class="sxs-lookup"><span data-stu-id="da39a-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="da39a-107">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="da39a-107">Script explanation</span></span>

<span data-ttu-id="da39a-108">Bu komut, ana bilgisayar adı, anahtarlar ve bağlantı noktaları bir Azure Redis önbelleği örneğinin almak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="da39a-108">This script uses the following commands to retrieve the hostname, keys, and ports of an Azure Redis Cache instance.</span></span> <span data-ttu-id="da39a-109">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="da39a-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="da39a-110">Komut</span><span class="sxs-lookup"><span data-stu-id="da39a-110">Command</span></span> | <span data-ttu-id="da39a-111">Notlar</span><span class="sxs-lookup"><span data-stu-id="da39a-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="da39a-112">az redis Göster</span><span class="sxs-lookup"><span data-stu-id="da39a-112">az redis show</span></span>](https://docs.microsoft.com/cli/azure/redis#show) | <span data-ttu-id="da39a-113">Bir Azure Redis önbelleği örneği ayrıntılarını alma.</span><span class="sxs-lookup"><span data-stu-id="da39a-113">Retrieve details of an Azure Redis Cache instance.</span></span> |
| [<span data-ttu-id="da39a-114">az redis listesi anahtarlar</span><span class="sxs-lookup"><span data-stu-id="da39a-114">az redis list-keys</span></span>](https://docs.microsoft.com/cli/azure/redis#list-keys) | <span data-ttu-id="da39a-115">Bir Azure Redis önbelleği örneği için erişim anahtarları alır.</span><span class="sxs-lookup"><span data-stu-id="da39a-115">Retrieve access keys for an Azure Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="da39a-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="da39a-116">Next steps</span></span>

<span data-ttu-id="da39a-117">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="da39a-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="da39a-118">Ek Azure Redis önbelleği CLI kod örnekleri bulunabilir [Azure Redis önbelleği belgelerine](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="da39a-118">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>