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
# <a name="get-the-hostname-ports-and-keys-for-azure-redis-cache"></a>Azure Redis önbelleği için ana bilgisayar adı, bağlantı noktalarını ve anahtarları alma

Bu senaryoda, ana bilgisayar adı, bağlantı noktaları ve Azure Redis önbelleği örneğine bağlanmak için kullanılan anahtarlarını alma hakkında bilgi edinin.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli[Ana](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis önbelleği")]


## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut, ana bilgisayar adı, anahtarlar ve bağlantı noktaları bir Azure Redis önbelleği örneğinin almak için aşağıdaki komutları kullanır. Komut belirli belgeleri tablo bağlanan her komut.

| Komut | Notlar |
|---|---|
| [az redis Göster](https://docs.microsoft.com/cli/azure/redis#show) | Bir Azure Redis önbelleği örneği ayrıntılarını alma. |
| [az redis listesi anahtarlar](https://docs.microsoft.com/cli/azure/redis#list-keys) | Bir Azure Redis önbelleği örneği için erişim anahtarları alır. |


## <a name="next-steps"></a>Sonraki adımlar

Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek Azure Redis önbelleği CLI kod örnekleri bulunabilir [Azure Redis önbelleği belgelerine](../cli-samples.md).