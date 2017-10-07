---
title: "aaaConfigure hello hizmeti parametreleri PostgreSQL için Azure veritabanında | Microsoft Docs"
description: "Bu makalede, Azure CLI komut satırı PostgreSQL kullanma tooconfigure hello hizmeti parametreleri Azure veritabanında nasıl hello açıklanmaktadır."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 84a11de24ba87fc0eb6744aaa4b53f65a183903d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a>Azure CLI kullanarak sunucu yapılandırma parametreleri özelleştirme
Liste, Göster ve hello komut satırı arabirimi (Azure CLI) kullanarak bir Azure PostgreSQL sunucusu için yapılandırma parametrelerini güncelleştirin. Ancak, yalnızca bir alt kümesini altyapısı yapılandırmaları sunucu düzeyinde sunulur ve değiştirilebilir. 

## <a name="prerequisites"></a>Ön koşullar
toostep bu nasıl tooguide aracılığıyla, aşağıdakiler gerekir:
- Sunucu ve veritabanına [PostgreSQL için bir Azure veritabanı oluşturma](quickstart-create-server-database-azure-cli.md)
- Yükleme [Azure CLI 2.0](/cli/azure/install-azure-cli) komut satırı yardımcı programı veya kullanım hello Azure bulut Kabuk hello tarayıcıda.

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a>Itanium tabanlı sistemler için liste sunucu yapılandırma parametreleri Azure veritabanı için PostgreSQL sunucusu
Tüm değiştirilebilir parametreler bir sunucu ve bunların değerleri toolist çalıştırmak hello [az postgres sunucu yapılandırması listesi](/cli/azure/postgres/server/configuration#list) komutu.

Merhaba hello sunucusu için sunucu yapılandırma parametrelerini listeleyebilirsiniz **mypgserver 20170401.postgres.database.azure.com** kaynak grubu altında **myresourcegroup**.
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a>Sunucu yapılandırması parametre ayrıntıları göster
Merhaba çalıştıran bir sunucu için belirli yapılandırma parametresi tooshow ayrıntılarını [az postgres sunucu yapılandırması Göster](/cli/azure/postgres/server/configuration#show) komutu.

Bu örnek hello ayrıntılarını gösterir **günlük\_min\_iletileri** sunucusu için sunucu yapılandırma parametresi **mypgserver 20170401.postgres.database.azure.com** altında kaynak grubu **myresourcegroup.**
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a>Sunucu Yapılandırma parametresi değerini değiştirin
Belirli bir sunucu yapılandırma parametresi hello değerini de değiştirebilirsiniz ve bu hello PostgreSQL sunucu altyapısı için temel yapılandırma değeri hello güncelleştirir. tooupdate hello yapılandırma kullanım hello [az postgres sunucu yapılandırma kümesi](/cli/azure/postgres/server/configuration#set) komutu. 

tooupdate hello **günlük\_min\_iletileri** sunucu yapılandırma parametresi sunucunun **mypgserver 20170401.postgres.database.azure.com** kaynakgrubundaki**myresourcegroup.**
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
Tooreset hello yapılandırma parametresinin değerini istiyorsanız, isteğe bağlı hello çıkışı tooleave sadece tercih `--value` parametre ve hello hizmeti hello varsayılan değer uygulanacaktır. İçinde Yukarıdaki örnek, onu gibi görünür:
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
Bu hello sıfırlanacak **günlük\_min\_iletileri** yapılandırma toohello varsayılan değeri **uyarı**. Sunucu Yapılandırması ve izin verilen değerlere daha ayrıntılı bilgi için üzerinde PostgreSQL belgelerine bakın. [sunucu yapılandırması](https://www.postgresql.org/docs/9.6/static/runtime-config.html).

## <a name="next-steps"></a>Sonraki adımlar
- tooconfigure ve erişim sunucu günlüklerine bakın [PostgreSQL için Azure veritabanında sunucu günlükleri](concepts-server-logs.md)
