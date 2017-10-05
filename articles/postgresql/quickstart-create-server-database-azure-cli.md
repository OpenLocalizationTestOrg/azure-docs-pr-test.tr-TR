---
title: "Azure CLI aracını kullanarak PostgreSQL için Azure Veritabanı oluşturma | Microsoft Docs"
description: "Azure CLI (komut satırı arabirimi) aracını kullanarak PostgreSQL için Azure Veritabanı sunucusu oluşturma ve yönetmeye yönelik hızlı başlangıç kılavuzu."
services: postgresql
author: sanagama
ms.author: sanagama
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: quickstart
ms.date: 06/13/2017
ms.openlocfilehash: d78243abc140c7b3f0b99bdf56821b7920568550
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-azure-database-for-postgresql-using-the-azure-cli"></a><span data-ttu-id="d4cc2-103">Azure CLI aracını kullanarak PostgreSQL için Azure Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d4cc2-103">Create an Azure Database for PostgreSQL using the Azure CLI</span></span>
<span data-ttu-id="d4cc2-104">PostgreSQL için Azure Veritabanı, bulutta yüksek düzeyde kullanılabilir olan PostgreSQL veritabanları çalıştırmanızı, yönetmenizi ve ölçeklendirmenizi sağlayan, yönetilen bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-104">Azure Database for PostgreSQL is a managed service that enables you to run, manage, and scale highly available PostgreSQL databases in the cloud.</span></span> <span data-ttu-id="d4cc2-105">Azure CLI, komut satırından veya betik içindeki Azure kaynaklarını oluşturmak ve yönetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-105">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="d4cc2-106">Bu hızlı başlangıçta, Azure CLI aracını kullanarak bir [Azure kaynak grubunda](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) nasıl PostgreSQL için Azure Veritabanı sunucusu oluşturabileceğiniz gösterilir.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-106">This quickstart shows you how to create an Azure Database for PostgreSQL server in an [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) using the Azure CLI.</span></span>

<span data-ttu-id="d4cc2-107">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz](https://azure.microsoft.com/free/) bir hesap oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d4cc2-108">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d4cc2-109">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="d4cc2-110">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d4cc2-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="d4cc2-111">Birden fazla aboneliğiniz varsa kaynağın faturalanacağı uygun aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-111">If you have multiple subscriptions, choose the appropriate subscription in which the resource will be billed.</span></span> <span data-ttu-id="d4cc2-112">[az account set](/cli/azure/account#set) komutunu kullanarak hesabınız altındaki belirli bir abonelik kimliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-112">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="d4cc2-113">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="d4cc2-113">Create a resource group</span></span>

<span data-ttu-id="d4cc2-114">[az group create](/cli/azure/group#create) komutunu kullanarak bir [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="d4cc2-115">Kaynak grubu, Azure kaynaklarının grup olarak dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="d4cc2-116">Aşağıdaki örnek `westus` konumunda `myresourcegroup` adlı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-116">The following example creates a resource group named `myresourcegroup` in the `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="d4cc2-117">PostgreSQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="d4cc2-117">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="d4cc2-118">[az postgres server create](/cli/azure/postgres/server#create) komutunu kullanarak [PostgreSQL sunucusu için Azure SQL Veritabanı ](overview.md) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-118">Create an [Azure Database for PostgreSQL server](overview.md) using the [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="d4cc2-119">Sunucu, grup olarak yönetilen bir veritabanı grubu içerir.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-119">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="d4cc2-120">Aşağıdaki örnekte, `mylogin` sunucu yöneticisi oturum açma adıyla `myresourcegroup` kaynak grubunuzda `mypgserver-20170401` adlı bir sunucu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-120">The following example creates a server named `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="d4cc2-121">Bir sunucunun adı DNS adıyla eşleşir ve bu nedenle sunucunun Azure’da genel olarak benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-121">The name of a server maps to DNS name and is thus required to be globally unique in Azure.</span></span> <span data-ttu-id="d4cc2-122">`<server_admin_password>` değerini kendi değerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-122">Substitute the `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401  --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="d4cc2-123">Burada belirttiğiniz sunucu yöneticisi kullanıcı adı ve parolası, bu hızlı başlangıcın sonraki bölümlerinde sunucuda ve veritabanlarında oturum açmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-123">The server admin login and password that you specify here are required to log in to the server and its databases later in this quick start.</span></span> <span data-ttu-id="d4cc2-124">Bu bilgileri daha sonra kullanmak üzere aklınızda tutun veya kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-124">Remember or record this information for later use.</span></span>

<span data-ttu-id="d4cc2-125">Varsayılan olarak, **postgres** veritabanı sunucunuz altında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-125">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="d4cc2-126">[Postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) veritabanı; kullanıcılar, yardımcı programlar ve üçüncü taraf uygulamalar tarafından kullanılmak üzere geliştirilmiş varsayılan bir veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-126">The [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="d4cc2-127">Sunucu düzeyinde güvenlik duvarı kuralı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d4cc2-127">Configure a server-level firewall rule</span></span>

<span data-ttu-id="d4cc2-128">[az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) komutunu kullanarak Azure PostgreSQL sunucusu düzeyinde bir güvenlik duvarı kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-128">Create an Azure PostgreSQL server-level firewall rule with the [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="d4cc2-129">Sunucu düzeyindeki bir güvenlik duvarı kuralı, [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) veya [PgAdmin](https://www.pgadmin.org/) gibi bir dış uygulamanın Azure PostgreSQL hizmetinin güvenlik duvarı üzerinden sunucunuza bağlanmasına imkan tanır.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-129">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) to connect to your server through the Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="d4cc2-130">Ağınızdan bağlanabilmek için bir IP aralığını kapsayan bir güvenlik duvarı kuralı ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-130">You can set a firewall rule that covers an IP range to be able to connect from your network.</span></span> <span data-ttu-id="d4cc2-131">Aşağıdaki örnekte, [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) komutu kullanılarak bir IP adresi aralığı için `AllowAllIps` güvenlik duvarı kuralı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-131">The following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) to create a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="d4cc2-132">Tüm IP adreslerini açmak için başlangıç IP adresi olarak 0.0.0.0’ı, bitiş adresi olaraksa 255.255.255.255’i kullanın.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-132">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="d4cc2-133">Azure PostgreSQL sunucusu, 5432 bağlantı noktası üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-133">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="d4cc2-134">Kurumsal ağ içinden bağlanıyorsanız ağınızın güvenlik duvarı tarafından 5432 numaralı bağlantı noktası üzerinden giden trafiğe izin verilmiyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-134">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="d4cc2-135">BT departmanınızdan Azure SQL Veritabanı sunucunuzla bağlantı için 5432 numaralı bağlantı noktasını açmasını isteyin.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-135">Have your IT department open port 5432 to connect to your Azure SQL Database server.</span></span>

## <a name="get-the-connection-information"></a><span data-ttu-id="d4cc2-136">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="d4cc2-136">Get the connection information</span></span>

<span data-ttu-id="d4cc2-137">Sunucunuza bağlanmak için ana bilgisayar bilgilerini ve erişim kimlik bilgilerini sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-137">To connect to your server, you need to provide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="d4cc2-138">Sonuç JSON biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-138">The result is in JSON format.</span></span> <span data-ttu-id="d4cc2-139">**administratorLogin** ve **fullyQualifiedDomainName** bilgilerini not alın.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-139">Make a note of the **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
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

## <a name="connect-to-postgresql-database-using-psql"></a><span data-ttu-id="d4cc2-140">psql’yi kullanarak PostgreSQL veritabanına bağlanma</span><span class="sxs-lookup"><span data-stu-id="d4cc2-140">Connect to PostgreSQL database using psql</span></span>

<span data-ttu-id="d4cc2-141">İstemci bilgisayarınızda PostgreSQL yüklüyse, [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html)’nin yerel bir örneğini kullanarak Azure PostgreSQL sunucusuna bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-141">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) to connect to an Azure PostgreSQL server.</span></span> <span data-ttu-id="d4cc2-142">Şimdi psql komut satırı yardımcı programını kullanarak Azure PostgreSQL sunucusuna bağlanalım.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-142">Let's now use the psql command-line utility to connect to the Azure PostgreSQL server.</span></span>

1. <span data-ttu-id="d4cc2-143">PostgreSQL için Azure Veritabanı sunucusuna bağlanmak üzere aşağıdaki psql komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="d4cc2-143">Run the following psql command to connect to an Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="d4cc2-144">Örneğin aşağıdaki komut, erişim kimlik bilgilerini kullanarak **mypgserver-20170401.postgres.database.azure.com** PostgreSQL sunucunuzda **postgres** adlı varsayılan veritabanına bağlanır.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-144">For example, the following command connects to the default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="d4cc2-145">Parola istendiğinde seçtiğiniz `<server_admin_password>` değerini girin.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-145">Enter the `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
```

2.  <span data-ttu-id="d4cc2-146">Sunucuya bağlandıktan sonra, istemde boş bir veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-146">Once you are connected to the server, create a blank database at the prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="d4cc2-147">İstemde, bağlantıyı yeni oluşturulan **mypgsqldb** veritabanına geçirmek için aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="d4cc2-147">At the prompt, execute the following command to switch connection to the newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="connect-to-postgresql-database-using-pgadmin"></a><span data-ttu-id="d4cc2-148">pgAdmin’i kullanarak PostgreSQL veritabanına bağlanma</span><span class="sxs-lookup"><span data-stu-id="d4cc2-148">Connect to PostgreSQL database using pgAdmin</span></span>

<span data-ttu-id="d4cc2-149">_pgAdmin_ GUI aracını kullanarak Azure PostgreSQL sunucusuna bağlanmak için</span><span class="sxs-lookup"><span data-stu-id="d4cc2-149">To connect to Azure PostgreSQL server using the GUI tool _pgAdmin_</span></span>
1.  <span data-ttu-id="d4cc2-150">İstemci bilgisayarınızda _pgAdmin_ uygulamasını başlatın.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-150">Launch the _pgAdmin_ application on your client computer.</span></span> <span data-ttu-id="d4cc2-151">_pgAdmin_’i http://www.pgadmin.org/ adresinden yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-151">You can install _pgAdmin_ from http://www.pgadmin.org/.</span></span>
2.  <span data-ttu-id="d4cc2-152">**Hızlı Bağlantılar** menüsünden **Yeni Sunucu Ekle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-152">Choose **Add New Server** from the **Quick Links** menu.</span></span>
3.  <span data-ttu-id="d4cc2-153">**Oluştur - Sunucu** iletişim kutusunun **Genel** sekmesinde, sunucu için benzersiz bir kolay ad girin.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-153">In the **Create - Server** dialog box **General** tab, enter a unique friendly Name for the server.</span></span> <span data-ttu-id="d4cc2-154">Örneğin, **Azure PostgreSQL Sunucusu**.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-154">Say **Azure PostgreSQL Server**.</span></span>
 <span data-ttu-id="d4cc2-155">![pgAdmin tool - create - server](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span><span class="sxs-lookup"><span data-stu-id="d4cc2-155">![pgAdmin tool - create - server](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span></span>
4.  <span data-ttu-id="d4cc2-156">**Oluştur - Sunucu** iletişim kutusunda, **Bağlantı** sekmesi:</span><span class="sxs-lookup"><span data-stu-id="d4cc2-156">In the **Create - Server** dialog box, **Connection** tab:</span></span>
    - <span data-ttu-id="d4cc2-157">**Ana Bilgisayar Adı/ Adresi** kutusuna tam sunucu adını (örneğin, **mypgserver-20170401.postgres.database.azure.com**) girin.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-157">Enter the fully qualified server name (for example, **mypgserver-20170401.postgres.database.azure.com**) in the **Host Name/ Address** box.</span></span> 
    - <span data-ttu-id="d4cc2-158">**Bağlantı Noktası** kutusuna 5432 numaralı bağlantı noktasını girin.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-158">Enter port 5432 into the **Port** box.</span></span> 
    - <span data-ttu-id="d4cc2-159">**Kullanıcı Adı** ve **Parola** kutularına, sırasıyla bu hızlı başlangıçta daha önce edinilen **Sunucu yöneticisi oturum açma adını (user@mypgserver)** ve sunucuyu oluştururken girdiğiniz parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-159">Enter the **Server admin login (user@mypgserver)** obtained earlier in this quickstart and password you entered when you created the server into the **Username** and **Password** boxes, respectively.</span></span>
    - <span data-ttu-id="d4cc2-160">**SSL Modu**’nu **Gerekli** olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-160">Select **SSL Mode** as **Require**.</span></span> <span data-ttu-id="d4cc2-161">Tüm Azure PostgreSQL sunucuları, varsayılan olarak SSL’yi zorunlu tutma seçeneği AÇIK olacak şekilde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-161">By default, all Azure PostgreSQL servers are created with SSL enforcing turned ON.</span></span> <span data-ttu-id="d4cc2-162">SSL’yi zorunlu tutma seçeneğini KAPALI konumuna getirmek için [SSL’yi zorunlu tutma](./concepts-ssl-connection-security.md) bölümündeki ayrıntıları inceleyin.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-162">To turn OFF SSL enforcing, see details in [Enforcing SSL](./concepts-ssl-connection-security.md).</span></span>

    ![pgAdmin - Oluştur - Sunucu](./media/quickstart-create-server-database-azure-cli/2-pgadmin-create-server.png)
5.  <span data-ttu-id="d4cc2-164">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-164">Click **Save**.</span></span>
6.  <span data-ttu-id="d4cc2-165">Tarayıcı sol bölmesinde **Sunucu Grupları**’nı genişletin.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-165">In the Browser left pane, expand the **Server Groups**.</span></span> <span data-ttu-id="d4cc2-166">**Azure PostgreSQL Sunucusu** adlı sunucunuzu seçin.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-166">Choose your server **Azure PostgreSQL Server**.</span></span>
7.  <span data-ttu-id="d4cc2-167">Bağlandığınız **Sunucu**’yu ve ardından altındaki **Veritabanları**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-167">Choose the **Server** you connected to, and then choose **Databases** under it.</span></span> 
8.  <span data-ttu-id="d4cc2-168">Veritabanı oluşturmak için **Veritabanları**’na sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-168">Right-click on **Databases** to Create a Database.</span></span>
9.  <span data-ttu-id="d4cc2-169">Veritabanı adı için **mypgsqldb**’yi ve sahibi için sunucu yöneticisi oturum açma bilgileri olarak **mylogin**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-169">Choose a database name **mypgsqldb** and the owner for it as server admin login **mylogin**.</span></span>
10. <span data-ttu-id="d4cc2-170">Boş bir veritabanı oluşturmak için **Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-170">Click **Save** to create a blank database.</span></span>
11. <span data-ttu-id="d4cc2-171">**Tarayıcı**’da **Sunucular** grubunu genişletin.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-171">In the **Browser**, expand the **Servers** group.</span></span> <span data-ttu-id="d4cc2-172">Oluşturduğunuz sunucuyu genişletin ve altındaki **mypgsqldb** veritabanını bulun.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-172">Expand the server you created, and see the database **mypgsqldb** under it.</span></span>
 <span data-ttu-id="d4cc2-173">![pgAdmin - Oluştur - Veritabanı](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span><span class="sxs-lookup"><span data-stu-id="d4cc2-173">![pgAdmin - Create - Database](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span></span>


## <a name="clean-up-resources"></a><span data-ttu-id="d4cc2-174">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="d4cc2-174">Clean up resources</span></span>

<span data-ttu-id="d4cc2-175">[Azure kaynak grubunu](../azure-resource-manager/resource-group-overview.md) silerek hızlı başlangıçta oluşturduğunuz tüm kaynakları temizleyin.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-175">Clean up all resources you created in the quickstart by deleting the [Azure resource group](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!TIP]
> <span data-ttu-id="d4cc2-176">Bu koleksiyondaki diğer hızlı başlangıçlar, bu hızlı başlangıcı temel alır.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-176">Other quickstarts in this collection build upon this quick start.</span></span> <span data-ttu-id="d4cc2-177">Sonraki hızlı başlangıçlarla çalışmaya devam etmeyi planlıyorsanız bu hızlı başlangıçta oluşturulan kaynakları temizlemeyin.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-177">If you plan to continue on to work with subsequent quickstarts, do not clean up the resources created in this quickstart.</span></span> <span data-ttu-id="d4cc2-178">Devam etmeyi planlamıyorsanız, Azure CLI aracında bu hızlı başlangıç ile oluşturulan tüm kaynakları silmek için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-178">If you do not plan to continue, use the following steps to delete all resources created by this quickstart in the Azure CLI.</span></span>

```azurecli-interactive
az group delete --name myresourcegroup
```

<span data-ttu-id="d4cc2-179">Yeni oluşturulan tek bir sunucuyu silmek istiyorsanız [az postgres server delete](/cli/azure/postgres/server#delete) komutunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4cc2-179">If you just would like to delete the one newly created server, you can run [az postgres server delete](/cli/azure/postgres/server#delete) command.</span></span>
```azurecli-interactive
az postgres server delete --resource-group myresourcegroup --name mypgserver-20170401
```

## <a name="next-steps"></a><span data-ttu-id="d4cc2-180">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d4cc2-180">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="d4cc2-181">Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme</span><span class="sxs-lookup"><span data-stu-id="d4cc2-181">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
