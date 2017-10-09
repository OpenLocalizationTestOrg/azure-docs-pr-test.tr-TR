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
# <a name="get-hello-hostname-ports-and-keys-for-azure-redis-cache"></a>Azure Redis önbelleği için Hello ana bilgisayar adı, bağlantı noktalarını ve anahtarları alma

Bu senaryoda, nasıl tooconnect tooan Azure Redis önbelleği örneği tooretrieve hello ana bilgisayar adı, bağlantı noktalarını ve anahtarları kullanılan öğrenin.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]


## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları tooretrieve hello ana bilgisayar adı, anahtarlar ve bağlantı noktaları bir Azure Redis önbelleği örneğinin aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az redis Göster](https://docs.microsoft.com/cli/azure/redis#show) | Bir Azure Redis önbelleği örneği ayrıntılarını alma. |
| [az redis listesi anahtarlar](https://docs.microsoft.com/cli/azure/redis#list-keys) | Bir Azure Redis önbelleği örneği için erişim anahtarları alır. |


## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek Azure Redis önbelleği CLI kod örnekleri hello bulunabilir [Azure Redis önbelleği belgelerine](../cli-samples.md).
