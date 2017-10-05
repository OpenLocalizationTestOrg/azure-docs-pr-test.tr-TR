---
title: "CLI örnek bir SQL esnek havuzu Azure SQL veritabanı ölçeklendirir | Microsoft Docs"
description: "Azure SQL veritabanındaki bir SQL esnek havuzu ölçeklendirmek için azure CLI örnek betik"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 888d2b7b7c118fede82d39881570a3b3d7b09961
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="use-cli-to-scale-a-sql-elastic-pool-in-azure-sql-database"></a>Azure SQL veritabanındaki bir SQL esnek havuzu ölçeklemek için CLI kullanın

Bu Azure CLI betik örnek SQL esnek havuzu oluşturur, havuza alınmış veritabanları taşır ve esnek havuz performans düzeyleri değiştirir. 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir. Sürümü bulmak için `az --version` komutunu çalıştırın. Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli-interactive[Ana](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "veritabanı havuzları arasında taşıma")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme

Komut dosyası örneği çalıştırdıktan sonra kaynak grubu ve onunla ilişkili tüm kaynakları kaldırmak için aşağıdaki komutu kullanılabilir.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut, bir kaynak grubu, mantıksal sunucusu, SQL veritabanı ve güvenlik duvarı kuralları oluşturmak için aşağıdaki komutları kullanır. Komut belirli belgeleri tablo bağlanan her komut.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az sql server oluşturun](https://docs.microsoft.com/cli/azure/sql/server#create) | SQL veritabanı barındıran bir mantıksal sunucu oluşturur. |
| [az sql esnek havuzları oluşturma](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | Mantıksal sunucu içindeki esnek veritabanı havuzu oluşturur. |
| [az sql db oluştur](https://docs.microsoft.com/cli/azure/sql/db#create) | SQL Database mantıksal sunucu oluşturur. |
| [az sql esnek havuzu güncelleştirme](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | Esnek veritabanı havuzu güncelleştirmeleri, bu örnekte atanan eDTU değiştirir. |
| [az grubu Sil](https://docs.microsoft.com/cli/azure/vm/extension#set) | Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler. |

## <a name="next-steps"></a>Sonraki adımlar

Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek SQL veritabanı CLI kod örnekleri bulunabilir [Azure SQL veritabanı belgeleri](../sql-database-cli-samples.md).
