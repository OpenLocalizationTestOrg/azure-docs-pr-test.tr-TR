---
title: "CLI İzleyici ölçek tek örnek Azure SQL veritabanı | Microsoft Docs"
description: "Tek bir Azure SQL veritabanı ölçekleme ve izlemek için azure CLI örnek betik"
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
ms.openlocfilehash: 01911b85268244a8fddb32aa726f8a870abbaf77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-cli-to-monitor-and-scale-a-single-sql-database"></a>İzlemek ve tek bir SQL veritabanı ölçeklendirmek için CLI kullanın

Bu Azure CLI betik örnek veritabanının boyutu bilgileri sorgulama sonra farklı performans düzeyi tek bir Azure SQL veritabanına ölçeklendirir. 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir. Sürümü bulmak için `az --version` komutunu çalıştırın. Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli-interactive[Ana](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "İzleyici ve ölçek tek SQL veritabanı")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme

Komut dosyası örneği çalıştırdıktan sonra kaynak grubu ve onunla ilişkili tüm kaynakları kaldırmak için aşağıdaki komutu kullanılabilir.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyasını aşağıdaki komutları kullanır. Komut belirli belgeleri tablo bağlanan her komut.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az sql server oluşturun](https://docs.microsoft.com/cli/azure/sql/server#create) | Bir veritabanını barındıran bir mantıksal sunucu oluşturur. |
| [az sql db Göster-kullanım](https://docs.microsoft.com/cli/azure/sql/db#show-usage) | Bir veritabanı boyutu kullanım bilgilerini gösterir. |
| [az sql db güncelleştirme](https://docs.microsoft.com/cli/azure/sql/db#update) | Veritabanı Özellikleri (örneğin, hizmet katmanı veya performans düzeyini) güncelleştirir veya bir veritabanı içine, dışı veya esnek havuzlar arasında taşır. |
| [az grubu Sil](https://docs.microsoft.com/cli/azure/vm/extension#set) | Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler. |
|||

## <a name="next-steps"></a>Sonraki adımlar

Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek SQL veritabanı CLI kod örnekleri bulunabilir [Azure SQL veritabanı belgeleri](../sql-database-cli-samples.md).
