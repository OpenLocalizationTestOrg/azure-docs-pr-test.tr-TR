---
title: "aaaCLI örnek bir SQL esnek havuzu Azure SQL veritabanı ölçeklendirir | Microsoft Docs"
description: "Azure CLI örnek komut dosyası tooscale Azure SQL veritabanındaki bir SQL esnek havuzu"
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
ms.openlocfilehash: 436128b8183213f78b9abc2ec46efe2a3ed3c37c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-tooscale-a-sql-elastic-pool-in-azure-sql-database"></a>CLI tooscale Azure SQL veritabanındaki bir SQL esnek havuzu kullanın

Bu Azure CLI betik örnek SQL esnek havuzu oluşturur, havuza alınmış veritabanları taşır ve esnek havuz performans düzeyleri değiştirir. 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme

Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları toocreate bir kaynak grubu, mantıksal sunucusu, SQL veritabanı ve güvenlik duvarı kuralları aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az sql server oluşturun](https://docs.microsoft.com/cli/azure/sql/server#create) | Konaklar SQL veritabanı hello mantıksal sunucu oluşturur. |
| [az sql esnek havuzları oluşturma](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | Merhaba mantıksal sunucu içindeki esnek veritabanı havuzu oluşturur. |
| [az sql db oluştur](https://docs.microsoft.com/cli/azure/sql/db#create) | SQL veritabanı Hello hello mantıksal Server'da oluşturur. |
| [az sql esnek havuzu güncelleştirme](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | Bu örnek değişiklikleri hello eDTU atanmış bir esnek veritabanı havuzundaki güncelleştirir. |
| [az grubu Sil](https://docs.microsoft.com/cli/azure/vm/extension#set) | Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek SQL veritabanı CLI kod örnekleri hello bulunabilir [Azure SQL veritabanı belgeleri](../sql-database-cli-samples.md).
