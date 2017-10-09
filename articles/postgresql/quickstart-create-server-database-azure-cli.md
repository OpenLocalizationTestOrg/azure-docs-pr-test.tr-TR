---
title: "Hello Azure CLI kullanarak PostgreSQL için bir Azure veritabanı oluşturma | Microsoft Docs"
description: "Hızlı Başlangıç Kılavuzu toocreate ve Azure CLI (komut satırı arabirimi) kullanılarak PostgreSQL sunucusu için Azure veritabanı yönetin."
services: postgresql
author: sanagama
ms.author: sanagama
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: quickstart
ms.date: 06/13/2017
ms.openlocfilehash: 946aa3cbf5ff9f5ac4e51248412d3da5d718141e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-using-hello-azure-cli"></a>Hello Azure CLI kullanarak PostgreSQL için bir Azure veritabanı oluşturma
Azure veritabanı PostgreSQL için toorun sağlayan yönetilen bir hizmettir, yönetmek ve yüksek oranda kullanılabilir PostgreSQL veritabanları hello bulutta ölçeklendirin. Hello Azure CLI kullanılan toocreate olan ve hello komut satırından veya komut dosyalarında Azure kaynaklarını yönetin. Bu Hızlı Başlangıç, nasıl Azure toocreate veritabanı PostgreSQL sunucu için gösterir. bir [Azure kaynak grubu](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) hello Azure CLI kullanarak.

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz](https://azure.microsoft.com/free/) bir hesap oluşturun.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

Birden çok aboneliğiniz varsa, hello kaynak faturalandırılacaksınız hello uygun abonelik seçin. [az account set](/cli/azure/account#set) komutunu kullanarak hesabınız altındaki belirli bir abonelik kimliğini seçin.
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

Merhaba aşağıdaki örnekte oluşturur adlı bir sunucu `mypgserver-20170401` kaynak grubunuzdaki `myresourcegroup` Sunucu Yöneticisi oturum açma ile `mylogin`. bir sunucunun adını Hello tooDNS adını eşler ve bunun sonucunda gerekli toobe Azure'da genel benzersiz. Yedek hello `<server_admin_password>` kendi değerine sahip.
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401  --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
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

## <a name="connect-toopostgresql-database-using-psql"></a>Psql kullanarak tooPostgreSQL veritabanına bağlan

İstemci bilgisayarınızda yüklü PostgreSQL varsa, yerel bir örneğini kullanabilirsiniz [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooconnect tooan Azure PostgreSQL sunucu. Şimdi hello psql komut satırı yardımcı programını tooconnect toohello Azure PostgreSQL sunucu kullanalım.

1. Psql komutu tooconnect tooan Azure veritabanı PostgreSQL sunucusu için aşağıdaki hello çalıştırın
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  Örneğin, komutu aşağıdaki hello adlı toohello varsayılan veritabanı bağlayan **postgres** PostgreSQL sunucunuzda **mypgserver 20170401.postgres.database.azure.com** erişim kimlik bilgileri kullanılarak. Merhaba girin `<server_admin_password>` parolası istendiğinde seçtiniz.
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
```

2.  Bağlı toohello sunucu olduktan sonra boş bir veritabanı hello isteminde oluşturun.
```sql
CREATE DATABASE mypgsqldb;
```

3.  Merhaba istemine komut tooswitch bağlantı toohello yeni oluşturulan veritabanı aşağıdaki hello yürütme **mypgsqldb**:
```sql
\c mypgsqldb
```

## <a name="connect-toopostgresql-database-using-pgadmin"></a>PgAdmin kullanarak tooPostgreSQL veritabanına bağlan

Merhaba GUI aracını kullanarak tooconnect tooAzure PostgreSQL server _pgAdmin_
1.  Merhaba başlatma _pgAdmin_ istemci bilgisayarınızda uygulama. _pgAdmin_’i http://www.pgadmin.org/ adresinden yükleyebilirsiniz.
2.  Seçin **yeni sunucu Ekle** hello gelen **hızlı bağlantılar** menüsü.
3.  Merhaba, **Create - Server** iletişim kutusu **genel** sekmesinde, hello sunucu için benzersiz bir kolay ad girin. Örneğin, **Azure PostgreSQL Sunucusu**.
 ![pgAdmin aracı - oluştur - sunucu](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)
4.  Merhaba, **Create - Server** iletişim kutusu, **bağlantı** sekmesi:
    - Merhaba tam sunucu adını girin (örneğin, **mypgserver 20170401.postgres.database.azure.com**) hello içinde **ana bilgisayar adı / adresi** kutusu. 
    - Bağlantı noktası 5432 hello girin **bağlantı noktası** kutusu. 
    - Merhaba girin **Sunucu Yöneticisi oturum açma (user@mypgserver)** daha önce bu hızlı başlangıç ve hello hello sunucu oluşturduğunuzda girdiğiniz parola elde **kullanıcıadı** ve **parola** kutular, sırasıyla.
    - **SSL Modu**’nu **Gerekli** olarak seçin. Tüm Azure PostgreSQL sunucuları, varsayılan olarak SSL’yi zorunla tutma seçeneği AÇIK konumundayken oluşturulur. SSL zorlama, devre dışı tooturn ayrıntıları görmek [zorlamayı SSL](./concepts-ssl-connection-security.md).

    ![pgAdmin - Oluştur - Sunucu](./media/quickstart-create-server-database-azure-cli/2-pgadmin-create-server.png)
5.  **Kaydet** düğmesine tıklayın.
6.  Merhaba tarayıcı sol hello bölmesinde **sunucu grupları**. **Azure PostgreSQL Sunucusu** adlı sunucunuzu seçin.
7.  Merhaba seçin **Server** bağlı ve ardından **veritabanları** altındaki. 
8.  Sağ **veritabanları** tooCreate bir veritabanı.
9.  Veritabanı adı Seç **mypgsqldb** ve onun için hello sahibi olarak Sunucu Yöneticisi oturum açma **mylogin**.
10. Tıklatın **kaydetmek** toocreate boş bir veritabanı.
11. Merhaba, **tarayıcı**, hello genişletin **sunucuları** grubu. Oluşturduğunuz hello sunucusunu genişletin ve hello veritabanı bkz **mypgsqldb** altındaki.
 ![pgAdmin - Oluştur - Veritabanı](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)


## <a name="clean-up-resources"></a>Kaynakları temizleme

Temiz hello silerek hello hızlı başlangıcı oluşturulan tüm kaynakları [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md).

> [!TIP]
> Bu koleksiyondaki diğer hızlı başlangıçlar, bu hızlı başlangıcı temel alır. Sonraki ile toowork toocontinue planlıyorsanız bu quickstart oluşturulan kaynakları quickstarts, değil temizleme hello. Toocontinue düşünmüyorsanız, aşağıdaki adımları toodelete hello hello Azure CLI Bu hızlı başlangıcı tarafından oluşturulan tüm kaynakları kullanın.

```azurecli-interactive
az group delete --name myresourcegroup
```

Yalnızca toodelete hello bir yeni oluşturulan sunucu isterseniz, çalıştırabilirsiniz [az postgres server silme](/cli/azure/postgres/server#delete) komutu.
```azurecli-interactive
az postgres server delete --resource-group myresourcegroup --name mypgserver-20170401
```

## <a name="next-steps"></a>Sonraki adımlar
> [!div class="nextstepaction"]
> [Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme](./howto-migrate-using-export-and-import.md)
