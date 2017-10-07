---
title: "Azure CLI: SQL veritabanı oluşturma | Microsoft Docs"
description: "Azure CLI toocreate SQL Database mantıksal sunucusu, sunucu düzeyinde güvenlik duvarı kuralı ve kullanarak veritabanlarını nasıl hello öğrenin."
keywords: "sql veritabanı öğreticisi, sql veritabanı oluşturma"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: 9b1ffb17eabeb70a000ff0c997128832b07aa4fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-hello-azure-cli"></a>Hello Azure CLI kullanarak tek bir Azure SQL veritabanı oluşturma

Hello Azure CLI kullanılan toocreate olan ve hello komut satırından veya komut dosyalarında Azure kaynaklarını yönetin. Bir Azure SQL veritabanında bu kılavuzu kullanarak hello Azure CLI toodeploy ayrıntılarını bir [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md) içinde bir [Azure SQL Database mantıksal sunucusu](sql-database-features.md).

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="define-variables"></a>Değişkenleri tanımlama

Bu hızlı başlangıç hello komut içinde kullanmak için değişkenleri tanımlayın.

```azurecli-interactive
# hello data center and resource name for your resources
export resourcegroupname = myResourceGroup
export location = westeurope
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
export servername = server-$RANDOM
# Set an admin login and password for your database
export adminlogin = ServerAdmin
export password = ChangeYourAdminPassword1
# hello ip address range that you want tooallow tooaccess your DB
export startip = "0.0.0.0"
export endip = "0.0.0.0"
# hello database name
export databasename = mySampleDatabase
```

## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Oluşturma bir [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md) hello kullanarak [az grubu oluşturma](/cli/azure/group#create) komutu. Kaynak grubu, Azure kaynaklarının grup olarak dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır. Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `westeurope` konumu.

```azurecli-interactive
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a>Mantıksal sunucu oluşturma

Oluşturma bir [Azure SQL Database mantıksal sunucusu](sql-database-features.md) hello kullanarak [az sql server oluşturun](/cli/azure/sql/server#create) komutu. Mantıksal sunucu, grup olarak yönetilen bir veritabanı grubu içerir. Merhaba aşağıdaki örnek rastgele adlandırılmış bir sunucu, kaynak grubunda adlı bir yönetici oturum açma ile oluşturur `ServerAdmin` ve bir parola `ChangeYourAdminPassword1`. Bu önceden tanımlı değerleri istediğiniz gibi değiştirin.

```azurecli-interactive
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a>Sunucu güvenlik duvarı kurallarını yapılandırma

Oluşturma bir [Azure SQL veritabanı sunucu düzeyinde güvenlik duvarı kuralı](sql-database-firewall-configure.md) hello kullanarak [az sql server güvenlik duvarı oluşturma](/cli/azure/sql/server/firewall-rule#create) komutu. Sunucu düzeyinde güvenlik duvarı kuralı SQL Server Management Studio veya hello SQLCMD yardımcı programını tooconnect tooa SQL veritabanı gibi hello SQL Database hizmeti güvenlik duvarı üzerinden bir dış uygulamaya verir. Aşağıdaki örneğine hello hello Güvenlik Duvarı'nı yalnızca diğer Azure kaynakları için açıldı. tooenable harici bağlantı, başlangıç IP adresi tooan uygun adresini Değiştir ortamınız için. tooopen tüm IP adresleri hello bitiş adresi başlangıç IP adresi ve 255.255.255.255 hello olarak 0.0.0.0 kullanın.  

```azurecli-interactive
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> SQL Veritabanı 1433 numaralı bağlantı noktası üzerinden iletişim kurar. Bir şirket ağından gelen tooconnect çalışıyorsanız, bağlantı noktası 1433 üzerinden giden trafik, ağınızın güvenlik duvarı tarafından izin verilmiyor. Öyleyse, BT departmanınızın 1433 numaralı bağlantı noktasını açar sürece mümkün tooconnect tooyour Azure SQL veritabanı sunucusu olmaz.
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a>Merhaba sunucu örnek verilerle bir veritabanı oluşturun

Bir veritabanı oluşturmak bir [S0 performans düzeyi](sql-database-service-tiers.md) hello kullanarak hello Server'daki [az sql db Oluştur](/cli/azure/sql/db#create) komutu. Merhaba aşağıdaki örnek adlı bir veritabanı oluşturur `mySampleDatabase` ve bu veritabanına yükleri hello AdventureWorksLT örnek verileri. Bu önceden tanımlanmış Değiştir istendiği gibi (Bu koleksiyonu yapıda Bu hızlı başlangıç hello değerleri bağlı diğer hızlı başlar) değerleri.

```azurecli-interactive
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a>Kaynakları temizleme

Bu koleksiyondaki diğer hızlı başlangıçlar, bu hızlı başlangıca göre belirlenir. 

> [!TIP]
> Sonraki hızlı başlangıçlar ile toowork üzerinde toocontinue planlıyorsanız, temiz oluşturulan bu hızlı başlangıç kaynakları başlatılmaz. Toocontinue düşünmüyorsanız bu hızlı başlangıç bölümünde hello Azure portal tarafından oluşturulan tüm kaynakları adımları toodelete aşağıdaki hello kullanın.
>

```azurecli-interactive
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a>Sonraki adımlar

Artık bir veritabanınız olduğuna göre, sık kullandığınız araçlarla bağlanabilir ve sorgulayabilirsiniz. Aşağıdan aracınızı seçerek daha fazla bilgi edinin:

- [SQL Server Management Studio](sql-database-connect-query-ssms.md)
- [Visual Studio Code](sql-database-connect-query-vscode.md)
- [.NET](sql-database-connect-query-dotnet.md)
- [PHP](sql-database-connect-query-php.md)
- [Node.js](sql-database-connect-query-nodejs.md)
- [Java](sql-database-connect-query-java.md)
- [Python](sql-database-connect-query-python.md)
- [Ruby](sql-database-connect-query-ruby.md)

