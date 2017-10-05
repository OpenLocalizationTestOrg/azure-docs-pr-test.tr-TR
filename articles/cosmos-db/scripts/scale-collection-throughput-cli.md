---
title: "Azure CLI betik ölçekli Azure Cosmos DB kapsayıcı işleme | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - ölçek Azure Cosmos DB contianer işleme"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/02/2017
ms.author: mimig
ms.openlocfilehash: f08733cd4074c7144b20a0592522423e729e6f1d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="scale-azure-cosmos-db-container-throughput-using-the-azure-cli"></a>Azure CLI kullanarak ölçek Azure Cosmos DB kapsayıcı işleme

Bu örnek, Azure Cosmos DB kapsayıcı herhangi bir tür için kapsayıcı işleme ölçeklendirir.  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir. Sürümü bulmak için `az --version` komutunu çalıştırın. Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli-interactive[Ana](../../../cli_scripts/cosmosdb/scale-cosmosdb-throughput/scale-cosmosdb-throughput.sh?highlight=40-46 "ölçek Azure Cosmos DB işleme")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme

Komut dosyası örneği çalıştırdıktan sonra kaynak grubu ve onunla ilişkili tüm kaynakları kaldırmak için aşağıdaki komutu kullanılabilir.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyasını aşağıdaki komutları kullanır. Komut belirli belgeleri tablo bağlanan her komut.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az cosmosdb güncelleştirme](https://docs.microsoft.com/cli/azure/cosmosdb#update) | Bir Azure Cosmos DB hesabını güncelleştirir. |
| [az grubu Sil](https://docs.microsoft.com/cli/azure/group#delete) | Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler. |

## <a name="next-steps"></a>Sonraki adımlar

Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek Azure Cosmos DB CLI kod örnekleri bulunabilir [Azure Cosmos DB CLI belgelerine](../cli-samples.md).
