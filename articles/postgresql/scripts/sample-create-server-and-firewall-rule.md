---
title: "aaa \"Azure CLI SCRIPT - PostgreSQL için bir Azure veritabanı oluşturma | Microsoft Docs\""
description: "Azure CLI komut dosyası örneği - PostgreSQL sunucu için bir Azure veritabanı oluşturur ve bir sunucu düzeyinde güvenlik duvarı kuralı yapılandırır."
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: bbe31f77283aa4a3bb36d1fd9171c280594a8267
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-server-and-configure-a-firewall-rule-using-hello-azure-cli"></a>PostgreSQL sunucu için bir Azure veritabanı oluşturma ve hello Azure CLI kullanarak bir güvenlik duvarı kuralı yapılandırma
Bu örnek CLI betik PostgreSQL sunucu için bir Azure veritabanı oluşturur ve bir sunucu düzeyinde güvenlik duvarı kuralı yapılandırır. Hello betik başarılı şekilde gerçekleştirildikten sonra tüm Azure hizmetlerinden hello PostgreSQL sunucu erişilebilir ve IP adresi hello yapılandırılır.

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Örnek komut dosyası
Bu örnek komut dosyasında vurgulanmış hello satırları toocustomize hello yönetici kullanıcı adı ve parola düzenleyin.
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for PostgreSQL, and server-level firewall rule.")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme
Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a>Komut dosyası açıklaması
Bu komut dosyası komutları aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| **Komutu** | **Notlar** |
|---|---|
| [az grubu oluşturma](/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az postgres sunucu oluşturma](/cli/azure/postgres/server#create) | Merhaba veritabanlarını barındıran bir PostgreSQL sunucusu oluşturur. |
| [az postgres sunucu güvenlik duvarı oluşturma](/cli/azure/postgres/server/firewall-rule#create) | Bir güvenlik duvarı kuralı tooallow erişim toohello sunucusu ve altındaki veritabanlarını hello girilen IP adresi aralığından oluşturur. |
| [az grubu Sil](/cli/azure/group#delete) | Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler. |

## <a name="next-steps"></a>Sonraki adımlar
- Hello Azure CLI hakkında daha fazla bilgi okuyun: [Azure CLI belgeleri](/cli/azure/overview)
- Ek komut dosyaları deneyin: [PostgreSQL Azure veritabanı için Azure CLI örnekleri](../sample-scripts-azure-cli.md)
