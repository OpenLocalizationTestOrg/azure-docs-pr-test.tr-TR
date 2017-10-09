---
title: "aaa \"Azure CLI betik ölçekli Azure veritabanı için PostgreSQL | Microsoft Docs\""
description: "Azure CLI komut dosyası örneği - hello ölçümleri sorgulama sonra PostgreSQL sunucu tooa farklı performans düzeyinde için ölçek Azure veritabanı."
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: 678b28941dbb4334cb374d4888991a00b44966b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-a-single-postgresql-server-using-azure-cli"></a>İzleme ve Azure CLI kullanarak tek bir PostgreSQL sunucu ölçekleme
Bu örnek CLI betik hello ölçümleri sorgulama sonra PostgreSQL sunucu tooa farklı performans düzeyi için tek bir Azure veritabanına ölçeklendirir. 

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Örnek komut dosyası
Bu örnek komut dosyasında, vurgulanmış hello satırları toocustomize hello yönetici kullanıcı adını ve parolasını değiştirin. Merhaba az İzleyici komutları kendi abonelik kimliği ile kullanılan hello abonelik kimliği değiştirin.[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme
Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a>Komut dosyası açıklaması
Bu komut dosyası komutları aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| **Komutu** | **Notlar** |
|---|---|
| [az grubu oluşturma](/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az postgres sunucu oluşturma](/cli/azure/postgres/server#create) | Merhaba veritabanlarını barındıran bir PostgreSQL sunucusu oluşturur. |
| [az İzleyici ölçümleri listesi](/cli/azure/monitor/metrics#list) | Merhaba kaynakların listesi hello ölçüm değeri. |
| [az grubu Sil](/cli/azure/group#delete) | Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler. |

## <a name="next-steps"></a>Sonraki adımlar
- Hello Azure CLI hakkında daha fazla bilgi okuyun: [Azure CLI belgeleri](/cli/azure/overview)
- Ek komut dosyaları deneyin: [PostgreSQL Azure veritabanı için Azure CLI örnekleri](../sample-scripts-azure-cli.md)
- Ölçeklendirme hakkında daha fazla bilgi okuyun: [hizmet katmanları](../concepts-service-tiers.md) ve [işlem birimleri ve depolama birimleri](../concepts-compute-unit-and-storage.md)
