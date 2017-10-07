---
title: "aaa \"Azure CLI komut dosyası - Azure veritabanı için MySQL oluşturun. | Microsoft Docs\""
description: "Bu örnek CLI betik MySQL sunucusu için bir Azure veritabanı oluşturur ve bir sunucu düzeyinde güvenlik duvarı kuralı yapılandırır."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: 1d619ee0547efd8275eaf7c1347b6c3427025c3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-mysql-server-and-configure-a-firewall-rule-using-hello-azure-cli"></a>MySQL sunucusu oluşturun ve hello Azure CLI kullanarak bir güvenlik duvarı kuralı yapılandırma
Bu örnek CLI betik MySQL sunucusu için bir Azure veritabanı oluşturur ve bir sunucu düzeyinde güvenlik duvarı kuralı yapılandırır. Hello komut dosyası başarıyla çalıştıktan sonra hello MySQL server tüm Azure Hizmetleri tarafından erişilebilir ve IP adresi hello yapılandırılır.

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Örnek komut dosyası
Bu örnek komut dosyasında vurgulanmış hello satırları toocustomize hello yönetici kullanıcı adı ve parola düzenleyin.
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/create-mysql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for MySQL, and server-level firewall rule.")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme
Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/delete-mysql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a>Komut dosyası açıklaması
Bu komut dosyası komutları aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| **Komutu** | **Notlar** |
|---|---|
| [az grubu oluşturma](/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az mysql sunucusu oluşturun](/cli/azure/mysql/server#create) | Merhaba veritabanlarını barındıran MySQL server oluşturur. |
| [az mysql server güvenlik duvarı oluşturma](/cli/azure/mysql/server/firewall-rule#create) | Bir güvenlik duvarı kuralı tooallow erişim toohello sunucusu ve altındaki veritabanlarını hello girilen IP adresi aralığından oluşturur. |
| [az grubu Sil](/cli/azure/group#delete) | Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler. |

## <a name="next-steps"></a>Sonraki adımlar
- Hello Azure CLI hakkında daha fazla bilgi okuyun: [Azure CLI belgelerine](/cli/azure/overview).
- Ek komut dosyaları deneyin: [Azure veritabanı için MySQL için Azure CLI örnekleri](../sample-scripts-azure-cli.md)
