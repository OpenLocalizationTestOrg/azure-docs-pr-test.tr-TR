---
title: "Azure CLI kullanarak PostgreSQL için sunucu günlüklerine aaaConfigure ve erişim | Microsoft Docs"
description: "Bu makalede nasıl tooconfigure ve erişim hello Azure veritabanı'nda Azure CLI komut satırını kullanarak PostgreSQL için olay günlüklerini açıklanmaktadır."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 924d4e7634cc48405bcb0f813cf61d8b72ad8aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a>Yapılandırma ve Azure CLI kullanarak sunucu günlüklerine erişme
Merhaba PostgreSQL server Hata günlüklerini hello komut satırı arabirimi (Azure CLI) kullanarak yükleyebilirsiniz. Ancak, erişim tootransaction günlükleri desteklenmiyor. 

## <a name="prerequisites"></a>Ön koşullar
toostep bu nasıl tooguide aracılığıyla, aşağıdakiler gerekir:
- Bir [PostgreSQL sunucu için Azure veritabanı](quickstart-create-server-database-azure-cli.md)
- Yükleme [Azure CLI 2.0](/cli/azure/install-azure-cli) komut satırı yardımcı programı veya kullanım hello Azure bulut Kabuk hello tarayıcıda.

## <a name="configure-logging-for-azure-database-for-postgresql"></a>Azure veritabanı için günlük kaydını PostgreSQL için yapılandırma
Merhaba sunucu tooaccess sorgu günlüklerini ve Hata günlüklerini yapılandırabilirsiniz. Hata günlüklerini otomatik vakum, bağlantı ve kontrol noktaları bilgiler içerebilir.
1. Günlüğünü etkinleştirme
2. Güncelleştirme günlük\_deyimi ve günlük\_min\_süresi\_deyimi tooenable sorgu günlüğü
3. Saklama dönemi güncelleştir

Daha fazla bilgi için bkz: [sunucu yapılandırma parametreleri özelleştirme](howto-configure-server-parameters-using-cli.md).

## <a name="list-logs-for-azure-database-for-postgresql-server"></a>Azure veritabanı için liste günlüklerini PostgreSQL sunucusu
Merhaba çalıştıran sunucunuz için toolist hello kullanılabilir günlük dosyalarını [az postgres sunucu günlükleri listesi](/cli/azure/postgres/server-logs#list) komutu.

Sunucu için hello günlük dosyalarını listeleyebilirsiniz **mypgserver 20170401.postgres.database.azure.com** kaynak grubu altında **myresourcegroup**ve tooa metni doğrudan adlı dosyaya **günlük\_dosyaları\_list.txt.**
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-hello-server"></a>Günlükleri hello sunucusundan yerel olarak yükle
Merhaba [az postgres server-günlükleri indirmek](/cli/azure/postgres/server-logs#download) komutu toodownload ayrı günlük dosyalarına sunucunuz için sağlar. 

İndirmeler hello hello sunucu için özel günlük dosyası Bu örnek **mypgserver 20170401.postgres.database.azure.com** kaynak grubu altında **myresourcegroup** tooyour yerel ortamı.
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a>Sonraki adımlar
- toolearn sunucu günlükleri hakkında daha fazla bilgi görmek [PostgreSQL için Azure veritabanında sunucu günlükleri](concepts-server-logs.md)
- Sunucu parametreleri hakkında daha fazla bilgi için bkz: [Azure CLI kullanarak sunucu yapılandırma parametreleri özelleştirme](howto-configure-server-parameters-using-cli.md)
