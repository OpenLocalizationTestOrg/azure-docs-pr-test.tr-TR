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
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a><span data-ttu-id="5ee0a-103">İlk Azure veritabanınız için Azure CLI kullanarak PostgreSQL tasarlama</span><span class="sxs-lookup"><span data-stu-id="5ee0a-103">Design your first Azure Database for PostgreSQL using Azure CLI</span></span> 
<span data-ttu-id="5ee0a-104">Bu öğreticide, Azure CLI (komut satırı arabirimi) ve diğer yardımcı programları toolearn nasıl kullanacağınız için:</span><span class="sxs-lookup"><span data-stu-id="5ee0a-104">In this tutorial, you use Azure CLI (command-line interface) and other utilities toolearn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="5ee0a-105">PostgreSQL için Azure Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5ee0a-105">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="5ee0a-106">Merhaba sunucu Güvenlik Duvarı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5ee0a-106">Configure hello server firewall</span></span>
> * <span data-ttu-id="5ee0a-107">Kullanım [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) yardımcı programı toocreate bir veritabanı</span><span class="sxs-lookup"><span data-stu-id="5ee0a-107">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="5ee0a-108">Örnek verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="5ee0a-108">Load sample data</span></span>
> * <span data-ttu-id="5ee0a-109">Verileri sorgulama</span><span class="sxs-lookup"><span data-stu-id="5ee0a-109">Query data</span></span>
> * <span data-ttu-id="5ee0a-110">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="5ee0a-110">Update data</span></span>
> * <span data-ttu-id="5ee0a-111">Verileri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="5ee0a-111">Restore data</span></span>

<span data-ttu-id="5ee0a-112">Hello Azure bulut Kabuk hello tarayıcıda kullanabilir veya [yükleme Azure CLI 2.0]( /cli/azure/install-azure-cli) kendi bilgisayar toorun hello kod blokları bu öğreticideki üzerinde.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-112">You may use hello Azure Cloud Shell in hello browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer toorun hello code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5ee0a-113">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-113">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5ee0a-114">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="5ee0a-115">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5ee0a-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="5ee0a-116">Birden çok aboneliğiniz varsa, hello kaynak yok veya için fatura hello uygun abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-116">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="5ee0a-117">[az account set](/cli/azure/account#set) komutunu kullanarak hesabınız altındaki belirli bir abonelik kimliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-117">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="5ee0a-118">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="5ee0a-118">Create a resource group</span></span>
<span data-ttu-id="5ee0a-119">Oluşturma bir [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md) hello kullanarak [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-119">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="5ee0a-120">Kaynak grubu, Azure kaynaklarının grup olarak dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-120">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="5ee0a-121">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myresourcegroup` hello içinde `westus` konumu.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-121">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="5ee0a-122">PostgreSQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="5ee0a-122">Create an Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="5ee0a-123">Oluşturma bir [PostgreSQL sunucu için Azure veritabanı](overview.md) hello kullanarak [az postgres sunucusu oluşturmak](/cli/azure/postgres/server#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-123">Create an [Azure Database for PostgreSQL server](overview.md) using hello [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="5ee0a-124">Sunucu, grup olarak yönetilen bir veritabanı grubu içerir.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-124">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="5ee0a-125">Merhaba aşağıdaki örnekte oluşturur adlı bir sunucu `mypgserver-20170401` kaynak grubunuzdaki `myresourcegroup` Sunucu Yöneticisi oturum açma ile `mylogin`.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-125">hello following example creates a server called `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="5ee0a-126">Bir sunucunun adını tooDNS adı eşler ve böylece gerekli toobe Azure'da genel benzersiz olur.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-126">Name of a server maps tooDNS name and is thus required toobe globally unique in Azure.</span></span> <span data-ttu-id="5ee0a-127">Yedek hello `<server_admin_password>` kendi değerine sahip.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-127">Substitute hello `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="5ee0a-128">Burada belirttiğiniz Hello Sunucu Yöneticisi oturum açma ve parola toohello Server'daki gerekli toolog ve veritabanlarını Bu hızlı başlangıç devamındaki kümesidir.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-128">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="5ee0a-129">Bu bilgileri daha sonra kullanmak üzere aklınızda tutun veya kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-129">Remember or record this information for later use.</span></span>

<span data-ttu-id="5ee0a-130">Varsayılan olarak, **postgres** veritabanı sunucunuz altında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-130">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="5ee0a-131">Merhaba [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) veritabanıdır varsayılan bir veritabanı kullanıcılar, yardımcı programlar ve üçüncü taraf uygulamalar tarafından kullanılmak üzere anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-131">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="5ee0a-132">Sunucu düzeyinde güvenlik duvarı kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5ee0a-132">Configure a server-level firewall rule</span></span>

<span data-ttu-id="5ee0a-133">Merhaba ile Azure PostgreSQL sunucu düzeyinde güvenlik duvarı kuralını [az postgres sunucu güvenlik duvarı kuralı oluşturmak](/cli/azure/postgres/server/firewall-rule#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-133">Create an Azure PostgreSQL server-level firewall rule with hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="5ee0a-134">Sunucu düzeyinde güvenlik duvarı kuralı gibi bir dış uygulamaya izin verir [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) veya [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour sunucu hello Azure PostgreSQL hizmeti güvenlik duvarı üzerinden.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-134">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server through hello Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="5ee0a-135">Bir IP aralığı toobe mümkün tooconnect ağınızdan kapsayan bir güvenlik duvarı kuralı ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-135">You can set a firewall rule that covers an IP range toobe able tooconnect from your network.</span></span> <span data-ttu-id="5ee0a-136">Merhaba aşağıdaki örnek kullanır [az postgres sunucu güvenlik duvarı kuralı oluşturmak](/cli/azure/postgres/server/firewall-rule#create) toocreate bir güvenlik duvarı kuralı `AllowAllIps` için bir IP adresi aralığı.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-136">hello following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) toocreate a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="5ee0a-137">tooopen tüm IP adresleri hello bitiş adresi başlangıç IP adresi ve 255.255.255.255 hello olarak 0.0.0.0 kullanın.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-137">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="5ee0a-138">Azure PostgreSQL sunucusu, 5432 bağlantı noktası üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-138">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="5ee0a-139">Kurumsal ağ içinden bağlanıyorsanız ağınızın güvenlik duvarı tarafından 5432 numaralı bağlantı noktası üzerinden giden trafiğe izin verilmiyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-139">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="5ee0a-140">Bağlantı noktası 5432 tooconnect tooyour Azure SQL Database sunucusu açın, BT departmanınızın vardır.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-140">Have your IT department open port 5432 tooconnect tooyour Azure SQL Database server.</span></span>
>

## <a name="get-hello-connection-information"></a><span data-ttu-id="5ee0a-141">Merhaba bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="5ee0a-141">Get hello connection information</span></span>

<span data-ttu-id="5ee0a-142">tooconnect tooyour server tooprovide konağı bilgileri ve erişim kimlik bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-142">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="5ee0a-143">Merhaba, JSON biçiminde sonucudur.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-143">hello result is in JSON format.</span></span> <span data-ttu-id="5ee0a-144">Merhaba Not **Admınıstratorlogın** ve **fullyQualifiedDomainName**.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-144">Make a note of hello **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
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

## <a name="connect-tooazure-database-for-postgresql-database-using-psql"></a><span data-ttu-id="5ee0a-145">Psql kullanarak PostgreSQL veritabanı için veritabanı tooAzure Bağlan</span><span class="sxs-lookup"><span data-stu-id="5ee0a-145">Connect tooAzure Database for PostgreSQL database using psql</span></span>
<span data-ttu-id="5ee0a-146">İstemci bilgisayarınızda yüklü PostgreSQL varsa, yerel bir örneğini kullanabilirsiniz [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), veya hello Azure Cloud Console tooconnect tooan Azure PostgreSQL sunucu.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-146">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), or hello Azure Cloud Console tooconnect tooan Azure PostgreSQL server.</span></span> <span data-ttu-id="5ee0a-147">Şimdi hello psql komut satırı yardımcı programını tooconnect toohello Azure veritabanı PostgreSQL sunucusu için kullanalım.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-147">Let's now use hello psql command-line utility tooconnect toohello Azure Database for PostgreSQL server.</span></span>

1. <span data-ttu-id="5ee0a-148">Psql komutu tooconnect tooan Azure veritabanı PostgreSQL sunucusu için aşağıdaki hello çalıştırın</span><span class="sxs-lookup"><span data-stu-id="5ee0a-148">Run hello following psql command tooconnect tooan Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="5ee0a-149">Örneğin, komutu aşağıdaki hello adlı toohello varsayılan veritabanı bağlayan **postgres** PostgreSQL sunucunuzda **mypgserver 20170401.postgres.database.azure.com** erişim kimlik bilgileri kullanılarak.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-149">For example, hello following command connects toohello default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="5ee0a-150">Merhaba girin `<server_admin_password>` parolası istendiğinde seçtiniz.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-150">Enter hello `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  <span data-ttu-id="5ee0a-151">Bağlı toohello sunucu olduktan sonra boş bir veritabanı hello isteminde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-151">Once you are connected toohello server, create a blank database at hello prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="5ee0a-152">Merhaba istemine komut tooswitch bağlantı toohello yeni oluşturulan veritabanı aşağıdaki hello yürütme **mypgsqldb**:</span><span class="sxs-lookup"><span data-stu-id="5ee0a-152">At hello prompt, execute hello following command tooswitch connection toohello newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="5ee0a-153">Merhaba veritabanında tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="5ee0a-153">Create tables in hello database</span></span>
<span data-ttu-id="5ee0a-154">Nasıl tooconnect toohello Azure veritabanı PostgreSQL için biz nasıl gidebilirsiniz bildiğinize göre toocomplete temel bazı görevler.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-154">Now that you know how tooconnect toohello Azure Database for PostgreSQL, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="5ee0a-155">İlk olarak, size bir tablo oluşturun ve bazı verilerle yükleyin.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-155">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="5ee0a-156">Envanter bilgilerini izleyen bir tablo oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-156">Let's create a table that tracks inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

<span data-ttu-id="5ee0a-157">Yeni Tablo tabloların hello listesi şimdi yazarak oluşturulan hello görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5ee0a-157">You can see hello newly created table in hello list of tables now by typing:</span></span>
```sql
\dt
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="5ee0a-158">Merhaba tablolara veri yükleme</span><span class="sxs-lookup"><span data-stu-id="5ee0a-158">Load data into hello tables</span></span>
<span data-ttu-id="5ee0a-159">Bir tablo sahibiz, biz bazı veri içine ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-159">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="5ee0a-160">Hello açık komut istemi penceresinde, sorgu tooinsert aşağıdaki hello bazı satırlar alt kümesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-160">At hello open command prompt window, run hello following query tooinsert some rows of data</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="5ee0a-161">Şimdi örnek verilerin daha önce oluşturduğunuz hello tabloya iki satır var.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-161">You have now two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="5ee0a-162">Sorgulamak ve hello hello tablolarındaki verileri güncelleyin</span><span class="sxs-lookup"><span data-stu-id="5ee0a-162">Query and update hello data in hello tables</span></span>
<span data-ttu-id="5ee0a-163">Sorgu tooretrieve bilgisinden hello veritabanı tablosundan hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-163">Execute hello following query tooretrieve information from hello database table.</span></span> 
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="5ee0a-164">Merhaba tablolardaki hello verileri da güncelleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="5ee0a-164">You can also update hello data in hello tables</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="5ee0a-165">veri aldığınızda hello satır buna göre güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-165">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="5ee0a-166">Zaman içinde veritabanı tooa önceki bir noktaya geri</span><span class="sxs-lookup"><span data-stu-id="5ee0a-166">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="5ee0a-167">Yanlışlıkla bir tabloyu sildiniz düşünün.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-167">Imagine you have accidentally deleted a table.</span></span> <span data-ttu-id="5ee0a-168">Bu, kolayca kurtaramazsınız şeydir.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-168">This is something you cannot easily recover from.</span></span> <span data-ttu-id="5ee0a-169">Azure veritabanı PostgreSQL için toogo geri tooany zaman noktası (hello too7 gün (Temel) en son yukarı ve 35 gün (standart)) verir ve bu zaman içinde nokta tooa yeni sunucu geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-169">Azure Database for PostgreSQL allows you toogo back tooany point-in-time (in hello last up too7 days (Basic) and 35 days (Standard)) and restore this point-in-time tooa new server.</span></span> <span data-ttu-id="5ee0a-170">Bu yeni sunucu toorecover silinmiş verilerinizi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-170">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="5ee0a-171">Merhaba Hello tablo eklenmeden önce aşağıdaki adımları geri yükleme hello örnek sunucu tooa noktası.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-171">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="5ee0a-172">Merhaba `az postgres server restore` komutun şu parametreler hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="5ee0a-172">hello `az postgres server restore` command needs hello following parameters:</span></span>
| <span data-ttu-id="5ee0a-173">Ayar</span><span class="sxs-lookup"><span data-stu-id="5ee0a-173">Setting</span></span> | <span data-ttu-id="5ee0a-174">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="5ee0a-174">Suggested value</span></span> | <span data-ttu-id="5ee0a-175">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5ee0a-175">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="5ee0a-176">--kaynak-grubu</span><span class="sxs-lookup"><span data-stu-id="5ee0a-176">--resource-group</span></span> |  <span data-ttu-id="5ee0a-177">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5ee0a-177">myResourceGroup</span></span> |  <span data-ttu-id="5ee0a-178">Kaynak sunucunun hangi hello mevcut kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-178">The resource group in which hello source server exists.</span></span>  |
| <span data-ttu-id="5ee0a-179">--adı</span><span class="sxs-lookup"><span data-stu-id="5ee0a-179">--name</span></span> | <span data-ttu-id="5ee0a-180">mypgserver geri</span><span class="sxs-lookup"><span data-stu-id="5ee0a-180">mypgserver-restored</span></span> | <span data-ttu-id="5ee0a-181">Merhaba geri yükleme komutu tarafından oluşturulan yeni bir sunucu hello Hello adı.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-181">hello name of hello new server that is created by hello restore command.</span></span> |
| <span data-ttu-id="5ee0a-182">zaman içinde geri yükleme noktası</span><span class="sxs-lookup"><span data-stu-id="5ee0a-182">restore-point-in-time</span></span> | <span data-ttu-id="5ee0a-183">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="5ee0a-183">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="5ee0a-184">Bir zaman içinde nokta toorestore seçin.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-184">Select a point-in-time toorestore to.</span></span> <span data-ttu-id="5ee0a-185">Bu tarih ve saat hello kaynak sunucunun yedekleme saklama dönemi içinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-185">This date and time must be within hello source server's backup retention period.</span></span> <span data-ttu-id="5ee0a-186">ISO8601 tarih ve saat biçimini kullanın.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-186">Use ISO8601 date and time format.</span></span> <span data-ttu-id="5ee0a-187">Örneğin, kendi yerel saat dilimi gibi kullanabilir `2017-04-13T05:59:00-08:00`, veya UTC Zulu dili biçimi kullanın `2017-04-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-187">For example, you may use your own local timezone, such as `2017-04-13T05:59:00-08:00`, or use UTC Zulu format `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="5ee0a-188">--Kaynak sunucusu</span><span class="sxs-lookup"><span data-stu-id="5ee0a-188">--source-server</span></span> | <span data-ttu-id="5ee0a-189">mypgserver 20170401</span><span class="sxs-lookup"><span data-stu-id="5ee0a-189">mypgserver-20170401</span></span> | <span data-ttu-id="5ee0a-190">Merhaba adı veya hello kaynak sunucu toorestore kimliği.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-190">hello name or ID of hello source server toorestore from.</span></span> |

<span data-ttu-id="5ee0a-191">Bir sunucu tooa noktası zaman içinde geri hello özgün sunucusu itibariyle başlangıç noktası olarak belirttiğiniz zamanda kopyalama, yeni bir sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-191">Restoring a server tooa point-in-time creates a new server, copying as hello original server as of hello point in time you specify.</span></span> <span data-ttu-id="5ee0a-192">Merhaba konumu ve fiyatlandırma katmanı değerleri geri hello sunucusu olan hello hello kaynak sunucu ile aynı.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-192">hello location and pricing tier values for hello restored server are hello same as hello source server.</span></span>

<span data-ttu-id="5ee0a-193">Merhaba komut zaman uyumlu ve hello server geri yüklendikten sonra döndürür.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-193">hello command is synchronous, and will return after hello server is restored.</span></span> <span data-ttu-id="5ee0a-194">Merhaba geri yükleme tamamlandıktan sonra oluşturulan yeni bir sunucu hello bulun.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-194">Once hello restore finishes, locate hello new server that was created.</span></span> <span data-ttu-id="5ee0a-195">Veriler beklendiği gibi geri hello doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="5ee0a-195">Verify hello data was restored as expected.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5ee0a-196">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5ee0a-196">Next steps</span></span>
<span data-ttu-id="5ee0a-197">Bu öğreticide, nasıl öğrenilen toouse Azure CLI (komut satırı arabirimi) ve diğer yardımcı programları:</span><span class="sxs-lookup"><span data-stu-id="5ee0a-197">In this tutorial, you learned how toouse Azure CLI (command-line interface) and other utilities to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="5ee0a-198">PostgreSQL için Azure Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5ee0a-198">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="5ee0a-199">Merhaba sunucu Güvenlik Duvarı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5ee0a-199">Configure hello server firewall</span></span>
> * <span data-ttu-id="5ee0a-200">Kullanım [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) yardımcı programı toocreate bir veritabanı</span><span class="sxs-lookup"><span data-stu-id="5ee0a-200">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="5ee0a-201">Örnek verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="5ee0a-201">Load sample data</span></span>
> * <span data-ttu-id="5ee0a-202">Verileri sorgulama</span><span class="sxs-lookup"><span data-stu-id="5ee0a-202">Query data</span></span>
> * <span data-ttu-id="5ee0a-203">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="5ee0a-203">Update data</span></span>
> * <span data-ttu-id="5ee0a-204">Verileri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="5ee0a-204">Restore data</span></span>

<span data-ttu-id="5ee0a-205">Ardından, nasıl toouse hello Azure portal toodo benzer görev öğrenin, Bu öğretici gözden geçirin: [PostgreSQL kullanarak hello için Azure portalını ilk Azure veritabanınızı tasarlama](tutorial-design-database-using-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="5ee0a-205">Next, learn how toouse hello Azure portal toodo similar tasks, review this tutorial: [Design your first Azure Database for PostgreSQL using hello Azure portal](tutorial-design-database-using-azure-portal.md)</span></span>
