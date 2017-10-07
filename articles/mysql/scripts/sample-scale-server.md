---
title: "aaaAzure CLI tooscale MySQL sunucusu için bir Azure veritabanı örnekleri | Microsoft Docs"
description: "Bu örnek CLI betik hello ölçümleri sorgulama sonra Azure veritabanı için MySQL server tooa farklı performans düzeyi ölçeklendirir."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: sample
ms.custom: mvc
ms.date: 05/31/2017
ms.openlocfilehash: 721ef9db35a5f3be7a38438c1abb724187b18b75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-an-azure-database-for-mysql-server-using-azure-cli"></a>İzleme ve Azure CLI kullanarak MySQL sunucusu için bir Azure veritabanı ölçekleme
Bu örnek CLI betik hello ölçümleri sorgulama sonra MySQL server tooa farklı performans düzeyi için tek bir Azure veritabanına ölçeklendirir.

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Örnek komut dosyası
Bu örnek komut dosyasında, vurgulanmış hello satırları toocustomize hello yönetici kullanıcı adını ve parolasını değiştirin. Merhaba az İzleyici komutları kendi abonelik kimliği ile kullanılan hello abonelik kimliği değiştirin.[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme
Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Delete hello resource group.")]

## <a name="script-explanation"></a>Komut dosyası açıklaması
Bu komut dosyası komutları aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| **Komutu** | **Notlar** |
|---|---|
| [az grubu oluşturma](/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az mysql sunucusu oluşturun](/cli/azure/mysql/server#create) | Merhaba veritabanlarını barındıran MySQL server oluşturur. |
| [az İzleyici ölçümleri listesi](/cli/azure/monitor/metrics#list) | Merhaba kaynakların listesi hello ölçüm değeri. |
| [az grubu Sil](/cli/azure/group#delete) | Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler. |

## <a name="next-steps"></a>Sonraki adımlar
- Hello Azure CLI hakkında daha fazla bilgi okuyun: [Azure CLI belgelerine](/cli/azure/overview).
- Ek komut dosyaları deneyin: [Azure veritabanı için MySQL için Azure CLI örnekleri](../sample-scripts-azure-cli.md)
- Ölçeklendirme ile ilgili daha fazla bilgi için bkz: [hizmet katmanları](../concepts-service-tiers.md) ve [işlem birimleri ve depolama birimleri](../concepts-compute-unit-and-storage.md).
