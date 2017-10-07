---
title: "İlk Azure veritabanınız için Azure CLI kullanarak PostgreSQL tasarım | Microsoft Docs"
description: "Bu öğretici Azure CLI kullanarak nasıl tooDesign ilk Azure veritabanı için PostgreSQL gösterir."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: tutorial
ms.date: 06/13/2017
ms.openlocfilehash: 7914925c090e0b6f3e7c8a999eedb0b2baf83d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a>İlk Azure veritabanınız için Azure CLI kullanarak PostgreSQL tasarlama 
Bu öğreticide, Azure CLI (komut satırı arabirimi) ve diğer yardımcı programları toolearn nasıl kullanacağınız için:
> [!div class="checklist"]
> * PostgreSQL için Azure Veritabanı oluşturma
> * Merhaba sunucu Güvenlik Duvarı'nı yapılandırma
> * Kullanım [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) yardımcı programı toocreate bir veritabanı
> * Örnek verileri yükleme
> * Verileri sorgulama
> * Verileri güncelleştirme
> * Verileri geri yükleme

Hello Azure bulut Kabuk hello tarayıcıda kullanabilir veya [yükleme Azure CLI 2.0]( /cli/azure/install-azure-cli) kendi bilgisayar toorun hello kod blokları bu öğreticideki üzerinde.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

Birden çok aboneliğiniz varsa, hello kaynak yok veya için fatura hello uygun abonelik seçin. [az account set](/cli/azure/account#set) komutunu kullanarak hesabınız altındaki belirli bir abonelik kimliğini seçin.
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma
Oluşturma bir [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md) hello kullanarak [az grubu oluşturma](/cli/azure/group#create) komutu. Kaynak grubu, Azure kaynaklarının grup olarak dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır. Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myresourcegroup` hello içinde `westus` konumu.
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a>PostgreSQL için Azure Veritabanı sunucusu oluşturma
Oluşturma bir [PostgreSQL sunucu için Azure veritabanı](overview.md) hello kullanarak [az postgres sunucusu oluşturmak](/cli/azure/postgres/server#create) komutu. Sunucu, grup olarak yönetilen bir veritabanı grubu içerir. 

Merhaba aşağıdaki örnekte oluşturur adlı bir sunucu `mypgserver-20170401` kaynak grubunuzdaki `myresourcegroup` Sunucu Yöneticisi oturum açma ile `mylogin`. Bir sunucunun adını tooDNS adı eşler ve böylece gerekli toobe Azure'da genel benzersiz olur. Yedek hello `<server_admin_password>` kendi değerine sahip.
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> Burada belirttiğiniz Hello Sunucu Yöneticisi oturum açma ve parola toohello Server'daki gerekli toolog ve veritabanlarını Bu hızlı başlangıç devamındaki kümesidir. Bu bilgileri daha sonra kullanmak üzere aklınızda tutun veya kaydedin.

Varsayılan olarak, **postgres** veritabanı sunucunuz altında oluşturulur. Merhaba [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) veritabanıdır varsayılan bir veritabanı kullanıcılar, yardımcı programlar ve üçüncü taraf uygulamalar tarafından kullanılmak üzere anlamına gelir. 


## <a name="configure-a-server-level-firewall-rule"></a>Sunucu düzeyinde güvenlik duvarı kuralı oluşturma

Merhaba ile Azure PostgreSQL sunucu düzeyinde güvenlik duvarı kuralını [az postgres sunucu güvenlik duvarı kuralı oluşturmak](/cli/azure/postgres/server/firewall-rule#create) komutu. Sunucu düzeyinde güvenlik duvarı kuralı gibi bir dış uygulamaya izin verir [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) veya [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour sunucu hello Azure PostgreSQL hizmeti güvenlik duvarı üzerinden. 

Bir IP aralığı toobe mümkün tooconnect ağınızdan kapsayan bir güvenlik duvarı kuralı ayarlayabilirsiniz. Merhaba aşağıdaki örnek kullanır [az postgres sunucu güvenlik duvarı kuralı oluşturmak](/cli/azure/postgres/server/firewall-rule#create) toocreate bir güvenlik duvarı kuralı `AllowAllIps` için bir IP adresi aralığı. tooopen tüm IP adresleri hello bitiş adresi başlangıç IP adresi ve 255.255.255.255 hello olarak 0.0.0.0 kullanın.
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> Azure PostgreSQL sunucusu, 5432 bağlantı noktası üzerinden iletişim kurar. Kurumsal ağ içinden bağlanıyorsanız ağınızın güvenlik duvarı tarafından 5432 numaralı bağlantı noktası üzerinden giden trafiğe izin verilmiyor olabilir. Bağlantı noktası 5432 tooconnect tooyour Azure SQL Database sunucusu açın, BT departmanınızın vardır.
>

## <a name="get-hello-connection-information"></a>Merhaba bağlantı bilgilerini alma

tooconnect tooyour server tooprovide konağı bilgileri ve erişim kimlik bilgileri gerekir.
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

Merhaba, JSON biçiminde sonucudur. Merhaba Not **Admınıstratorlogın** ve **fullyQualifiedDomainName**.
```json
{
  "administratorLogin": "mylogin",
  "fullyQualifiedDomainName": "mypgserver-20170401.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforPostgreSQL/servers/mypgserver-20170401",
  "location": "westus",
  "name": "mypgserver-20170401",
  "resourceGroup": "myresourcegroup",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "PGSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 51200,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": "9.6"
}
```

## <a name="connect-tooazure-database-for-postgresql-database-using-psql"></a>Psql kullanarak PostgreSQL veritabanı için veritabanı tooAzure Bağlan
İstemci bilgisayarınızda yüklü PostgreSQL varsa, yerel bir örneğini kullanabilirsiniz [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), veya hello Azure Cloud Console tooconnect tooan Azure PostgreSQL sunucu. Şimdi hello psql komut satırı yardımcı programını tooconnect toohello Azure veritabanı PostgreSQL sunucusu için kullanalım.

1. Psql komutu tooconnect tooan Azure veritabanı PostgreSQL sunucusu için aşağıdaki hello çalıştırın
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  Örneğin, komutu aşağıdaki hello adlı toohello varsayılan veritabanı bağlayan **postgres** PostgreSQL sunucunuzda **mypgserver 20170401.postgres.database.azure.com** erişim kimlik bilgileri kullanılarak. Merhaba girin `<server_admin_password>` parolası istendiğinde seçtiniz.
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  Bağlı toohello sunucu olduktan sonra boş bir veritabanı hello isteminde oluşturun.
```sql
CREATE DATABASE mypgsqldb;
```

3.  Merhaba istemine komut tooswitch bağlantı toohello yeni oluşturulan veritabanı aşağıdaki hello yürütme **mypgsqldb**:
```sql
\c mypgsqldb
```

## <a name="create-tables-in-hello-database"></a>Merhaba veritabanında tabloları oluşturma
Nasıl tooconnect toohello Azure veritabanı PostgreSQL için biz nasıl gidebilirsiniz bildiğinize göre toocomplete temel bazı görevler.

İlk olarak, size bir tablo oluşturun ve bazı verilerle yükleyin. Envanter bilgilerini izleyen bir tablo oluşturalım.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

Yeni Tablo tabloların hello listesi şimdi yazarak oluşturulan hello görebilirsiniz:
```sql
\dt
```

## <a name="load-data-into-hello-tables"></a>Merhaba tablolara veri yükleme
Bir tablo sahibiz, biz bazı veri içine ekleyebilirsiniz. Hello açık komut istemi penceresinde, sorgu tooinsert aşağıdaki hello bazı satırlar alt kümesini çalıştırın.
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

Şimdi örnek verilerin daha önce oluşturduğunuz hello tabloya iki satır var.

## <a name="query-and-update-hello-data-in-hello-tables"></a>Sorgulamak ve hello hello tablolarındaki verileri güncelleyin
Sorgu tooretrieve bilgisinden hello veritabanı tablosundan hello yürütün. 
```sql
SELECT * FROM inventory;
```

Merhaba tablolardaki hello verileri da güncelleştirebilirsiniz
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

veri aldığınızda hello satır buna göre güncelleştirilir.
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Zaman içinde veritabanı tooa önceki bir noktaya geri
Yanlışlıkla bir tabloyu sildiniz düşünün. Bu, kolayca kurtaramazsınız şeydir. Azure veritabanı PostgreSQL için toogo geri tooany zaman noktası (hello too7 gün (Temel) en son yukarı ve 35 gün (standart)) verir ve bu zaman içinde nokta tooa yeni sunucu geri yükleyin. Bu yeni sunucu toorecover silinmiş verilerinizi kullanabilirsiniz. Merhaba Hello tablo eklenmeden önce aşağıdaki adımları geri yükleme hello örnek sunucu tooa noktası.

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

Merhaba `az postgres server restore` komutun şu parametreler hello gerekir:
| Ayar | Önerilen değer | Açıklama  |
| --- | --- | --- |
| --kaynak-grubu |  myResourceGroup |  Kaynak sunucunun hangi hello mevcut kaynak grubu.  |
| --adı | mypgserver geri | Merhaba geri yükleme komutu tarafından oluşturulan yeni bir sunucu hello Hello adı. |
| zaman içinde geri yükleme noktası | 2017-04-13T13:59:00Z | Bir zaman içinde nokta toorestore seçin. Bu tarih ve saat hello kaynak sunucunun yedekleme saklama dönemi içinde olmalıdır. ISO8601 tarih ve saat biçimini kullanın. Örneğin, kendi yerel saat dilimi gibi kullanabilir `2017-04-13T05:59:00-08:00`, veya UTC Zulu dili biçimi kullanın `2017-04-13T13:59:00Z`. |
| --Kaynak sunucusu | mypgserver 20170401 | Merhaba adı veya hello kaynak sunucu toorestore kimliği. |

Bir sunucu tooa noktası zaman içinde geri hello özgün sunucusu itibariyle başlangıç noktası olarak belirttiğiniz zamanda kopyalama, yeni bir sunucu oluşturur. Merhaba konumu ve fiyatlandırma katmanı değerleri geri hello sunucusu olan hello hello kaynak sunucu ile aynı.

Merhaba komut zaman uyumlu ve hello server geri yüklendikten sonra döndürür. Merhaba geri yükleme tamamlandıktan sonra oluşturulan yeni bir sunucu hello bulun. Veriler beklendiği gibi geri hello doğrulayın.


## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, nasıl öğrenilen toouse Azure CLI (komut satırı arabirimi) ve diğer yardımcı programları:
> [!div class="checklist"]
> * PostgreSQL için Azure Veritabanı oluşturma
> * Merhaba sunucu Güvenlik Duvarı'nı yapılandırma
> * Kullanım [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) yardımcı programı toocreate bir veritabanı
> * Örnek verileri yükleme
> * Verileri sorgulama
> * Verileri güncelleştirme
> * Verileri geri yükleme

Ardından, nasıl toouse hello Azure portal toodo benzer görev öğrenin, Bu öğretici gözden geçirin: [PostgreSQL kullanarak hello için Azure portalını ilk Azure veritabanınızı tasarlama](tutorial-design-database-using-azure-portal.md)
