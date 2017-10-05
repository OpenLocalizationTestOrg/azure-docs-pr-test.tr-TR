---
title: "İlk Azure veritabanınız için Azure CLI kullanarak PostgreSQL tasarım | Microsoft Docs"
description: "Bu öğretici, Azure CLI kullanarak ilk Azure veritabanınız için PostgreSQL tasarlamak nasıl gösterir."
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
ms.openlocfilehash: cf536fce8925f9173b541b845af25a8d8c38eabd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a><span data-ttu-id="827a2-103">İlk Azure veritabanınız için Azure CLI kullanarak PostgreSQL tasarlama</span><span class="sxs-lookup"><span data-stu-id="827a2-103">Design your first Azure Database for PostgreSQL using Azure CLI</span></span> 
<span data-ttu-id="827a2-104">Bu öğreticide, Azure CLI (komut satırı arabirimi) ve diğer yardımcı programları öğrenmek için kullandığınız nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="827a2-104">In this tutorial, you use Azure CLI (command-line interface) and other utilities to learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="827a2-105">PostgreSQL için Azure Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="827a2-105">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="827a2-106">Sunucu Güvenlik Duvarı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="827a2-106">Configure the server firewall</span></span>
> * <span data-ttu-id="827a2-107">Kullanım [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) bir veritabanı oluşturmak için yardımcı programı</span><span class="sxs-lookup"><span data-stu-id="827a2-107">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility to create a database</span></span>
> * <span data-ttu-id="827a2-108">Örnek verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="827a2-108">Load sample data</span></span>
> * <span data-ttu-id="827a2-109">Verileri sorgulama</span><span class="sxs-lookup"><span data-stu-id="827a2-109">Query data</span></span>
> * <span data-ttu-id="827a2-110">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="827a2-110">Update data</span></span>
> * <span data-ttu-id="827a2-111">Verileri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="827a2-111">Restore data</span></span>

<span data-ttu-id="827a2-112">Tarayıcıda, Azure bulut kabuğunu kullanabilirsiniz veya [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli) bu öğreticideki kod blokları çalıştırmak için kendi bilgisayarınızda.</span><span class="sxs-lookup"><span data-stu-id="827a2-112">You may use the Azure Cloud Shell in the browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer to run the code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="827a2-113">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="827a2-113">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="827a2-114">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="827a2-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="827a2-115">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="827a2-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="827a2-116">Birden fazla aboneliğiniz varsa kaynağın mevcut olduğu ve faturalandırıldığı uygun aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="827a2-116">If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span> <span data-ttu-id="827a2-117">[az account set](/cli/azure/account#set) komutunu kullanarak hesabınız altındaki belirli bir abonelik kimliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="827a2-117">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="827a2-118">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="827a2-118">Create a resource group</span></span>
<span data-ttu-id="827a2-119">[az group create](/cli/azure/group#create) komutunu kullanarak bir [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="827a2-119">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="827a2-120">Kaynak grubu, Azure kaynaklarının grup olarak dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="827a2-120">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="827a2-121">Aşağıdaki örnek `westus` konumunda `myresourcegroup` adlı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="827a2-121">The following example creates a resource group named `myresourcegroup` in the `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="827a2-122">PostgreSQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="827a2-122">Create an Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="827a2-123">[az postgres server create](/cli/azure/postgres/server#create) komutunu kullanarak [PostgreSQL sunucusu için Azure SQL Veritabanı ](overview.md) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="827a2-123">Create an [Azure Database for PostgreSQL server](overview.md) using the [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="827a2-124">Sunucu, grup olarak yönetilen bir veritabanı grubu içerir.</span><span class="sxs-lookup"><span data-stu-id="827a2-124">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="827a2-125">Aşağıdaki örnek adı verilen bir sunucu oluşturur `mypgserver-20170401` kaynak grubunuzdaki `myresourcegroup` Sunucu Yöneticisi oturum açma ile `mylogin`.</span><span class="sxs-lookup"><span data-stu-id="827a2-125">The following example creates a server called `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="827a2-126">Bir sunucunun adını DNS adıyla eşler ve böylece Azure içinde genel olarak benzersiz olması gereklidir.</span><span class="sxs-lookup"><span data-stu-id="827a2-126">Name of a server maps to DNS name and is thus required to be globally unique in Azure.</span></span> <span data-ttu-id="827a2-127">`<server_admin_password>` değerini kendi değerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="827a2-127">Substitute the `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="827a2-128">Burada belirttiğiniz sunucu yöneticisi kullanıcı adı ve parolası, bu hızlı başlangıcın sonraki bölümlerinde sunucuda ve veritabanlarında oturum açmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="827a2-128">The server admin login and password that you specify here are required to log in to the server and its databases later in this quick start.</span></span> <span data-ttu-id="827a2-129">Bu bilgileri daha sonra kullanmak üzere aklınızda tutun veya kaydedin.</span><span class="sxs-lookup"><span data-stu-id="827a2-129">Remember or record this information for later use.</span></span>

<span data-ttu-id="827a2-130">Varsayılan olarak, **postgres** veritabanı sunucunuz altında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="827a2-130">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="827a2-131">[Postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) veritabanı; kullanıcılar, yardımcı programlar ve üçüncü taraf uygulamalar tarafından kullanılmak üzere geliştirilmiş varsayılan bir veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="827a2-131">The [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="827a2-132">Sunucu düzeyinde güvenlik duvarı kuralı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="827a2-132">Configure a server-level firewall rule</span></span>

<span data-ttu-id="827a2-133">[az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) komutunu kullanarak Azure PostgreSQL sunucusu düzeyinde bir güvenlik duvarı kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="827a2-133">Create an Azure PostgreSQL server-level firewall rule with the [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="827a2-134">Sunucu düzeyindeki bir güvenlik duvarı kuralı, [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) veya [PgAdmin](https://www.pgadmin.org/) gibi bir dış uygulamanın Azure PostgreSQL hizmetinin güvenlik duvarı üzerinden sunucunuza bağlanmasına imkan tanır.</span><span class="sxs-lookup"><span data-stu-id="827a2-134">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) to connect to your server through the Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="827a2-135">Ağınızdan bağlanabilmek için bir IP aralığını kapsayan bir güvenlik duvarı kuralı ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="827a2-135">You can set a firewall rule that covers an IP range to be able to connect from your network.</span></span> <span data-ttu-id="827a2-136">Aşağıdaki örnekte, [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) komutu kullanılarak bir IP adresi aralığı için `AllowAllIps` güvenlik duvarı kuralı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="827a2-136">The following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) to create a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="827a2-137">Tüm IP adreslerini açmak için başlangıç IP adresi olarak 0.0.0.0’ı, bitiş adresi olaraksa 255.255.255.255’i kullanın.</span><span class="sxs-lookup"><span data-stu-id="827a2-137">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="827a2-138">Azure PostgreSQL sunucusu, 5432 bağlantı noktası üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="827a2-138">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="827a2-139">Kurumsal ağ içinden bağlanıyorsanız ağınızın güvenlik duvarı tarafından 5432 numaralı bağlantı noktası üzerinden giden trafiğe izin verilmiyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="827a2-139">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="827a2-140">BT departmanınızdan Azure SQL Veritabanı sunucunuzla bağlantı için 5432 numaralı bağlantı noktasını açmasını isteyin.</span><span class="sxs-lookup"><span data-stu-id="827a2-140">Have your IT department open port 5432 to connect to your Azure SQL Database server.</span></span>
>

## <a name="get-the-connection-information"></a><span data-ttu-id="827a2-141">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="827a2-141">Get the connection information</span></span>

<span data-ttu-id="827a2-142">Sunucunuza bağlanmak için ana bilgisayar bilgilerini ve erişim kimlik bilgilerini sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="827a2-142">To connect to your server, you need to provide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="827a2-143">Sonuç JSON biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="827a2-143">The result is in JSON format.</span></span> <span data-ttu-id="827a2-144">**administratorLogin** ve **fullyQualifiedDomainName** bilgilerini not alın.</span><span class="sxs-lookup"><span data-stu-id="827a2-144">Make a note of the **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
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

## <a name="connect-to-azure-database-for-postgresql-database-using-psql"></a><span data-ttu-id="827a2-145">Psql kullanarak PostgreSQL veritabanı için Azure veritabanına bağlan</span><span class="sxs-lookup"><span data-stu-id="827a2-145">Connect to Azure Database for PostgreSQL database using psql</span></span>
<span data-ttu-id="827a2-146">İstemci bilgisayarınızda yüklü PostgreSQL varsa, yerel bir örneğini kullanabilirsiniz [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), veya bir Azure PostgreSQL sunucusuna bağlanmak için Azure bulut Konsolu.</span><span class="sxs-lookup"><span data-stu-id="827a2-146">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), or the Azure Cloud Console to connect to an Azure PostgreSQL server.</span></span> <span data-ttu-id="827a2-147">Şimdi PostgreSQL için Azure Veritabanı sunucusuna bağlanmak üzere psql komut satır yardımcı programını kullanalım.</span><span class="sxs-lookup"><span data-stu-id="827a2-147">Let's now use the psql command-line utility to connect to the Azure Database for PostgreSQL server.</span></span>

1. <span data-ttu-id="827a2-148">PostgreSQL için Azure Veritabanı sunucusuna bağlanmak üzere aşağıdaki psql komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="827a2-148">Run the following psql command to connect to an Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="827a2-149">Örneğin aşağıdaki komut, erişim kimlik bilgilerini kullanarak **mypgserver-20170401.postgres.database.azure.com** PostgreSQL sunucunuzda **postgres** adlı varsayılan veritabanına bağlanır.</span><span class="sxs-lookup"><span data-stu-id="827a2-149">For example, the following command connects to the default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="827a2-150">Parola istendiğinde seçtiğiniz `<server_admin_password>` değerini girin.</span><span class="sxs-lookup"><span data-stu-id="827a2-150">Enter the `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  <span data-ttu-id="827a2-151">Sunucuya bağlandıktan sonra, istemde boş bir veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="827a2-151">Once you are connected to the server, create a blank database at the prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="827a2-152">İstemde, bağlantıyı yeni oluşturulan **mypgsqldb** veritabanına geçirmek için aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="827a2-152">At the prompt, execute the following command to switch connection to the newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="create-tables-in-the-database"></a><span data-ttu-id="827a2-153">Veritabanında tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="827a2-153">Create tables in the database</span></span>
<span data-ttu-id="827a2-154">PostgreSQL için Azure veritabanına bağlanmak nasıl bildiğinize göre biz temel bazı görevlerin nasıl üzerinden gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="827a2-154">Now that you know how to connect to the Azure Database for PostgreSQL, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="827a2-155">İlk olarak, size bir tablo oluşturun ve bazı verilerle yükleyin.</span><span class="sxs-lookup"><span data-stu-id="827a2-155">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="827a2-156">Envanter bilgilerini izleyen bir tablo oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="827a2-156">Let's create a table that tracks inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

<span data-ttu-id="827a2-157">Yazarak Tablo listesinde yeni oluşturulan tabloda şimdi görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="827a2-157">You can see the newly created table in the list of tables now by typing:</span></span>
```sql
\dt
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="827a2-158">Veri tablolarına yükleme</span><span class="sxs-lookup"><span data-stu-id="827a2-158">Load data into the tables</span></span>
<span data-ttu-id="827a2-159">Bir tablo sahibiz, biz bazı veri içine ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="827a2-159">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="827a2-160">Açık komut istemi penceresinde, bazı veri satırı eklemek için aşağıdaki sorguyu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="827a2-160">At the open command prompt window, run the following query to insert some rows of data</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="827a2-161">Şimdi örnek verilerin daha önce oluşturduğunuz tabloya iki satır var.</span><span class="sxs-lookup"><span data-stu-id="827a2-161">You have now two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="827a2-162">Sorgulamak ve tablolarındaki verileri güncelleyin</span><span class="sxs-lookup"><span data-stu-id="827a2-162">Query and update the data in the tables</span></span>
<span data-ttu-id="827a2-163">Veritabanı tablosundan bilgi almak için aşağıdaki sorguyu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="827a2-163">Execute the following query to retrieve information from the database table.</span></span> 
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="827a2-164">Ayrıca tablolardaki verileri güncelleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="827a2-164">You can also update the data in the tables</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="827a2-165">Veri aldığınızda satır buna göre güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="827a2-165">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="827a2-166">Bir veritabanını daha önceki bir noktaya geri yükleme</span><span class="sxs-lookup"><span data-stu-id="827a2-166">Restore a database to a previous point in time</span></span>
<span data-ttu-id="827a2-167">Yanlışlıkla bir tabloyu sildiniz düşünün.</span><span class="sxs-lookup"><span data-stu-id="827a2-167">Imagine you have accidentally deleted a table.</span></span> <span data-ttu-id="827a2-168">Bu, kolayca kurtaramazsınız şeydir.</span><span class="sxs-lookup"><span data-stu-id="827a2-168">This is something you cannot easily recover from.</span></span> <span data-ttu-id="827a2-169">Azure veritabanı PostgreSQL için tüm noktası zamanında (olarak 7 gün (Temel) ve 35 gün (standart) son yukarı) için geri dönün ve bu noktası zaman içinde yeni bir sunucuya geri yüklemek sağlar.</span><span class="sxs-lookup"><span data-stu-id="827a2-169">Azure Database for PostgreSQL allows you to go back to any point-in-time (in the last up to 7 days (Basic) and 35 days (Standard)) and restore this point-in-time to a new server.</span></span> <span data-ttu-id="827a2-170">Bu yeni sunucu silinen verilerinizi kurtarmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="827a2-170">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="827a2-171">Tablo eklenmeden önce aşağıdaki adımları örnek sunucunun bir noktaya geri yükleme.</span><span class="sxs-lookup"><span data-stu-id="827a2-171">The following steps restore the sample server to a point before the table was added.</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="827a2-172">`az postgres server restore` Komutu aşağıdaki parametreleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="827a2-172">The `az postgres server restore` command needs the following parameters:</span></span>
| <span data-ttu-id="827a2-173">Ayar</span><span class="sxs-lookup"><span data-stu-id="827a2-173">Setting</span></span> | <span data-ttu-id="827a2-174">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="827a2-174">Suggested value</span></span> | <span data-ttu-id="827a2-175">Açıklama</span><span class="sxs-lookup"><span data-stu-id="827a2-175">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="827a2-176">--kaynak-grubu</span><span class="sxs-lookup"><span data-stu-id="827a2-176">--resource-group</span></span> |  <span data-ttu-id="827a2-177">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="827a2-177">myResourceGroup</span></span> |  <span data-ttu-id="827a2-178">Kaynak sunucunun bulunduğu kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="827a2-178">The resource group in which the source server exists.</span></span>  |
| <span data-ttu-id="827a2-179">--adı</span><span class="sxs-lookup"><span data-stu-id="827a2-179">--name</span></span> | <span data-ttu-id="827a2-180">mypgserver geri</span><span class="sxs-lookup"><span data-stu-id="827a2-180">mypgserver-restored</span></span> | <span data-ttu-id="827a2-181">Geri yükleme komutu tarafından oluşturulan yeni sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="827a2-181">The name of the new server that is created by the restore command.</span></span> |
| <span data-ttu-id="827a2-182">zaman içinde geri yükleme noktası</span><span class="sxs-lookup"><span data-stu-id="827a2-182">restore-point-in-time</span></span> | <span data-ttu-id="827a2-183">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="827a2-183">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="827a2-184">Bir noktayı geri yüklemek için zaman içinde seçin.</span><span class="sxs-lookup"><span data-stu-id="827a2-184">Select a point-in-time to restore to.</span></span> <span data-ttu-id="827a2-185">Bu tarih ve saat kaynak sunucunun yedekleme saklama dönemi içinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="827a2-185">This date and time must be within the source server's backup retention period.</span></span> <span data-ttu-id="827a2-186">ISO8601 tarih ve saat biçimini kullanın.</span><span class="sxs-lookup"><span data-stu-id="827a2-186">Use ISO8601 date and time format.</span></span> <span data-ttu-id="827a2-187">Örneğin, kendi yerel saat dilimi gibi kullanabilir `2017-04-13T05:59:00-08:00`, veya UTC Zulu dili biçimi kullanın `2017-04-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="827a2-187">For example, you may use your own local timezone, such as `2017-04-13T05:59:00-08:00`, or use UTC Zulu format `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="827a2-188">--Kaynak sunucusu</span><span class="sxs-lookup"><span data-stu-id="827a2-188">--source-server</span></span> | <span data-ttu-id="827a2-189">mypgserver 20170401</span><span class="sxs-lookup"><span data-stu-id="827a2-189">mypgserver-20170401</span></span> | <span data-ttu-id="827a2-190">Adı veya geri yüklemek için kaynak sunucunun kimliği.</span><span class="sxs-lookup"><span data-stu-id="827a2-190">The name or ID of the source server to restore from.</span></span> |

<span data-ttu-id="827a2-191">Sunucuyu bir nokta zaman için geri yükleme noktası itibariyle özgün sunucusu olarak belirttiğiniz zamanda kopyalama, yeni bir sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="827a2-191">Restoring a server to a point-in-time creates a new server, copying as the original server as of the point in time you specify.</span></span> <span data-ttu-id="827a2-192">Geri yüklenen sunucusunun fiyatlandırma katmanı değerleri ve konumunu kaynak sunucu ile aynı olur.</span><span class="sxs-lookup"><span data-stu-id="827a2-192">The location and pricing tier values for the restored server are the same as the source server.</span></span>

<span data-ttu-id="827a2-193">Komut zaman uyumlu ve sunucunun geri yüklendikten sonra döndürür.</span><span class="sxs-lookup"><span data-stu-id="827a2-193">The command is synchronous, and will return after the server is restored.</span></span> <span data-ttu-id="827a2-194">Geri yükleme tamamlandıktan sonra oluşturulan yeni sunucu bulun.</span><span class="sxs-lookup"><span data-stu-id="827a2-194">Once the restore finishes, locate the new server that was created.</span></span> <span data-ttu-id="827a2-195">Verileri beklenen şekilde geri doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="827a2-195">Verify the data was restored as expected.</span></span>


## <a name="next-steps"></a><span data-ttu-id="827a2-196">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="827a2-196">Next steps</span></span>
<span data-ttu-id="827a2-197">Bu öğreticide, Azure CLI (komut satırı arabirimi) ve diğer yardımcı programlarını nasıl kullanılacağı hakkında bilgi edindiniz:</span><span class="sxs-lookup"><span data-stu-id="827a2-197">In this tutorial, you learned how to use Azure CLI (command-line interface) and other utilities to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="827a2-198">PostgreSQL için Azure Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="827a2-198">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="827a2-199">Sunucu Güvenlik Duvarı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="827a2-199">Configure the server firewall</span></span>
> * <span data-ttu-id="827a2-200">Kullanım [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) bir veritabanı oluşturmak için yardımcı programı</span><span class="sxs-lookup"><span data-stu-id="827a2-200">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility to create a database</span></span>
> * <span data-ttu-id="827a2-201">Örnek verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="827a2-201">Load sample data</span></span>
> * <span data-ttu-id="827a2-202">Verileri sorgulama</span><span class="sxs-lookup"><span data-stu-id="827a2-202">Query data</span></span>
> * <span data-ttu-id="827a2-203">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="827a2-203">Update data</span></span>
> * <span data-ttu-id="827a2-204">Verileri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="827a2-204">Restore data</span></span>

<span data-ttu-id="827a2-205">Ardından, Azure portalında benzer görevleri yapmak için Bu öğretici gözden geçirmek için nasıl kullanacağınızı öğrenin: [PostgreSQL için Azure Portalı'nı kullanarak ilk Azure veritabanınızı tasarlama](tutorial-design-database-using-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="827a2-205">Next, learn how to use the Azure portal to do similar tasks, review this tutorial: [Design your first Azure Database for PostgreSQL using the Azure portal](tutorial-design-database-using-azure-portal.md)</span></span>
