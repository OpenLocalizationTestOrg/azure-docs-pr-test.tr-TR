---
title: "aaaAzure CLI komut dosyası örneği - bir Azure Redis önbelleği Sil | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - Delete bir Azure Redis önbelleği"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 7beded7a-d2c9-43a6-b3b4-b8079c11de4a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: 788277f6464d40fedc597ce7f3041130312c07a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="delete-an-azure-redis-cache"></a>Bir Azure Redis önbelleği Sil

Bu senaryoda, nasıl toodelete bir Azure Redis önbelleği öğrenin.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli[main](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları toodelete bir Azure Redis önbelleği örneği aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az redis Sil](https://docs.microsoft.com/cli/azure/redis#delete) | Redis önbelleği örneğini silin. |


## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek Azure Redis önbelleği CLI kod örnekleri hello bulunabilir [Azure Redis önbelleği belgelerine](../cli-samples.md).
