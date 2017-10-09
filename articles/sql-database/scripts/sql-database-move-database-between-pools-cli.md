---
title: "aaaCLI örnek taşıma Azure SQL veritabanı SQL esnek havuzu | Microsoft Docs"
description: "Azure CLI örnek komut dosyası toomove bir SQL veritabanında SQL esnek havuzu"
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
ms.date: 07/05/2017
ms.author: janeng
ms.openlocfilehash: 841eb57d2d49612c3fadd3a6424a2b0309c69719
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomove-an-azure-sql-database-in-a-sql-elastic-pool"></a>SQL esnek havuzda CLI toomove Azure SQL veritabanını kullan

Bu Azure CLI komut dosyası örneği iki esnek havuzlar oluşturur ve bir Azure SQL veritabanı bir SQL esnek havuzdan başka bir SQL esnek havuza ve ardından hello veritabanı esnek havuz tooa tek Azure veritabanı performans düzeyi dışında taşır. 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Move database between pools")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme

Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az sql server oluşturun](https://docs.microsoft.com/cli/azure/sql/server#create) | Bir veritabanı veya esnek havuzu barındıran bir mantıksal sunucu oluşturur. |
| [az sql esnek havuzları oluşturma](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | Merhaba mantıksal sunucu içindeki bir esnek havuz oluşturur. |
| [az sql db oluştur](https://docs.microsoft.com/cli/azure/sql/db#create) | Tek bir ya da bir havuza veritabanı olarak mantıksal sunucu bir veritabanı oluşturur. |
| [az sql db güncelleştirme](https://docs.microsoft.com/cli/azure/sql/db#update) | Veritabanı özellikleri güncelleştirir veya bir veritabanı içine, dışı veya esnek havuzlar arasında taşır. |
| [az grubu Sil](https://docs.microsoft.com/cli/azure/vm/extension#set) | Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek SQL veritabanı CLI kod örnekleri hello bulunabilir [Azure SQL veritabanı belgeleri](../sql-database-cli-samples.md).


