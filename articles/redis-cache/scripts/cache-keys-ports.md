---
title: "aaaAzure CLI komut dosyası örneği - Get hello ana bilgisayar adı, bağlantı noktalarını ve anahtarları Azure Redis önbelleği için | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - Get hello ana bilgisayar adı, bağlantı noktalarını ve anahtarları bir Azure Redis önbelleği örneği için"
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
ms.openlocfilehash: e6e794558087d6568438c439e2bf99fc46eeb8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-hostname-ports-and-keys-for-azure-redis-cache"></a><span data-ttu-id="f6192-103">Azure Redis önbelleği için Hello ana bilgisayar adı, bağlantı noktalarını ve anahtarları alma</span><span class="sxs-lookup"><span data-stu-id="f6192-103">Get hello hostname, ports, and keys for Azure Redis Cache</span></span>

<span data-ttu-id="f6192-104">Bu senaryoda, nasıl tooconnect tooan Azure Redis önbelleği örneği tooretrieve hello ana bilgisayar adı, bağlantı noktalarını ve anahtarları kullanılan öğrenin.</span><span class="sxs-lookup"><span data-stu-id="f6192-104">In this scenario, you learn how tooretrieve hello hostname, ports, and keys used tooconnect tooan Azure Redis Cache instance.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="f6192-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="f6192-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]


## <a name="script-explanation"></a><span data-ttu-id="f6192-106">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="f6192-106">Script explanation</span></span>

<span data-ttu-id="f6192-107">Bu komut dosyası komutları tooretrieve hello ana bilgisayar adı, anahtarlar ve bağlantı noktaları bir Azure Redis önbelleği örneğinin aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="f6192-107">This script uses hello following commands tooretrieve hello hostname, keys, and ports of an Azure Redis Cache instance.</span></span> <span data-ttu-id="f6192-108">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="f6192-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f6192-109">Komut</span><span class="sxs-lookup"><span data-stu-id="f6192-109">Command</span></span> | <span data-ttu-id="f6192-110">Notlar</span><span class="sxs-lookup"><span data-stu-id="f6192-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f6192-111">az redis Göster</span><span class="sxs-lookup"><span data-stu-id="f6192-111">az redis show</span></span>](https://docs.microsoft.com/cli/azure/redis#show) | <span data-ttu-id="f6192-112">Bir Azure Redis önbelleği örneği ayrıntılarını alma.</span><span class="sxs-lookup"><span data-stu-id="f6192-112">Retrieve details of an Azure Redis Cache instance.</span></span> |
| [<span data-ttu-id="f6192-113">az redis listesi anahtarlar</span><span class="sxs-lookup"><span data-stu-id="f6192-113">az redis list-keys</span></span>](https://docs.microsoft.com/cli/azure/redis#list-keys) | <span data-ttu-id="f6192-114">Bir Azure Redis önbelleği örneği için erişim anahtarları alır.</span><span class="sxs-lookup"><span data-stu-id="f6192-114">Retrieve access keys for an Azure Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="f6192-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f6192-115">Next steps</span></span>

<span data-ttu-id="f6192-116">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f6192-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f6192-117">Ek Azure Redis önbelleği CLI kod örnekleri hello bulunabilir [Azure Redis önbelleği belgelerine](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f6192-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
