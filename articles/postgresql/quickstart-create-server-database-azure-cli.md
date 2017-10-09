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
# <a name="create-an-azure-database-for-postgresql-using-hello-azure-cli"></a><span data-ttu-id="7bc04-103">Hello Azure CLI kullanarak PostgreSQL için bir Azure veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7bc04-103">Create an Azure Database for PostgreSQL using hello Azure CLI</span></span>
<span data-ttu-id="7bc04-104">Azure veritabanı PostgreSQL için toorun sağlayan yönetilen bir hizmettir, yönetmek ve yüksek oranda kullanılabilir PostgreSQL veritabanları hello bulutta ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="7bc04-104">Azure Database for PostgreSQL is a managed service that enables you toorun, manage, and scale highly available PostgreSQL databases in hello cloud.</span></span> <span data-ttu-id="7bc04-105">Hello Azure CLI kullanılan toocreate olan ve hello komut satırından veya komut dosyalarında Azure kaynaklarını yönetin.</span><span class="sxs-lookup"><span data-stu-id="7bc04-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="7bc04-106">Bu Hızlı Başlangıç, nasıl Azure toocreate veritabanı PostgreSQL sunucu için gösterir. bir [Azure kaynak grubu](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) hello Azure CLI kullanarak.</span><span class="sxs-lookup"><span data-stu-id="7bc04-106">This quickstart shows you how toocreate an Azure Database for PostgreSQL server in an [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) using hello Azure CLI.</span></span>

<span data-ttu-id="7bc04-107">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz](https://azure.microsoft.com/free/) bir hesap oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7bc04-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7bc04-108">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7bc04-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="7bc04-109">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="7bc04-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="7bc04-110">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7bc04-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="7bc04-111">Birden çok aboneliğiniz varsa, hello kaynak faturalandırılacaksınız hello uygun abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="7bc04-111">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource will be billed.</span></span> <span data-ttu-id="7bc04-112">[az account set](/cli/azure/account#set) komutunu kullanarak hesabınız altındaki belirli bir abonelik kimliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="7bc04-112">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="7bc04-113">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="7bc04-113">Create a resource group</span></span>

<span data-ttu-id="7bc04-114">Oluşturma bir [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md) hello kullanarak [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="7bc04-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="7bc04-115">Kaynak grubu, Azure kaynaklarının grup olarak dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="7bc04-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="7bc04-116">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myresourcegroup` hello içinde `westus` konumu.</span><span class="sxs-lookup"><span data-stu-id="7bc04-116">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="7bc04-117">PostgreSQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="7bc04-117">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="7bc04-118">Oluşturma bir [PostgreSQL sunucu için Azure veritabanı](overview.md) hello kullanarak [az postgres sunucusu oluşturmak](/cli/azure/postgres/server#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="7bc04-118">Create an [Azure Database for PostgreSQL server](overview.md) using hello [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="7bc04-119">Sunucu, grup olarak yönetilen bir veritabanı grubu içerir.</span><span class="sxs-lookup"><span data-stu-id="7bc04-119">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="7bc04-120">Merhaba aşağıdaki örnekte oluşturur adlı bir sunucu `mypgserver-20170401` kaynak grubunuzdaki `myresourcegroup` Sunucu Yöneticisi oturum açma ile `mylogin`.</span><span class="sxs-lookup"><span data-stu-id="7bc04-120">hello following example creates a server named `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="7bc04-121">bir sunucunun adını Hello tooDNS adını eşler ve bunun sonucunda gerekli toobe Azure'da genel benzersiz.</span><span class="sxs-lookup"><span data-stu-id="7bc04-121">hello name of a server maps tooDNS name and is thus required toobe globally unique in Azure.</span></span> <span data-ttu-id="7bc04-122">Yedek hello `<server_admin_password>` kendi değerine sahip.</span><span class="sxs-lookup"><span data-stu-id="7bc04-122">Substitute hello `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401  --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="7bc04-123">Burada belirttiğiniz Hello Sunucu Yöneticisi oturum açma ve parola toohello Server'daki gerekli toolog ve veritabanlarını Bu hızlı başlangıç devamındaki kümesidir.</span><span class="sxs-lookup"><span data-stu-id="7bc04-123">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="7bc04-124">Bu bilgileri daha sonra kullanmak üzere aklınızda tutun veya kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7bc04-124">Remember or record this information for later use.</span></span>

<span data-ttu-id="7bc04-125">Varsayılan olarak, **postgres** veritabanı sunucunuz altında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7bc04-125">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="7bc04-126">Merhaba [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) veritabanıdır varsayılan bir veritabanı kullanıcılar, yardımcı programlar ve üçüncü taraf uygulamalar tarafından kullanılmak üzere anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="7bc04-126">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="7bc04-127">Sunucu düzeyinde güvenlik duvarı kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7bc04-127">Configure a server-level firewall rule</span></span>

<span data-ttu-id="7bc04-128">Merhaba ile Azure PostgreSQL sunucu düzeyinde güvenlik duvarı kuralını [az postgres sunucu güvenlik duvarı kuralı oluşturmak](/cli/azure/postgres/server/firewall-rule#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="7bc04-128">Create an Azure PostgreSQL server-level firewall rule with hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="7bc04-129">Sunucu düzeyinde güvenlik duvarı kuralı gibi bir dış uygulamaya izin verir [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) veya [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour sunucu hello Azure PostgreSQL hizmeti güvenlik duvarı üzerinden.</span><span class="sxs-lookup"><span data-stu-id="7bc04-129">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server through hello Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="7bc04-130">Bir IP aralığı toobe mümkün tooconnect ağınızdan kapsayan bir güvenlik duvarı kuralı ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7bc04-130">You can set a firewall rule that covers an IP range toobe able tooconnect from your network.</span></span> <span data-ttu-id="7bc04-131">Merhaba aşağıdaki örnek kullanır [az postgres sunucu güvenlik duvarı kuralı oluşturmak](/cli/azure/postgres/server/firewall-rule#create) toocreate bir güvenlik duvarı kuralı `AllowAllIps` için bir IP adresi aralığı.</span><span class="sxs-lookup"><span data-stu-id="7bc04-131">hello following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) toocreate a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="7bc04-132">tooopen tüm IP adresleri hello bitiş adresi başlangıç IP adresi ve 255.255.255.255 hello olarak 0.0.0.0 kullanın.</span><span class="sxs-lookup"><span data-stu-id="7bc04-132">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="7bc04-133">Azure PostgreSQL sunucusu, 5432 bağlantı noktası üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="7bc04-133">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="7bc04-134">Kurumsal ağ içinden bağlanıyorsanız ağınızın güvenlik duvarı tarafından 5432 numaralı bağlantı noktası üzerinden giden trafiğe izin verilmiyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="7bc04-134">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="7bc04-135">Bağlantı noktası 5432 tooconnect tooyour Azure SQL Database sunucusu açın, BT departmanınızın vardır.</span><span class="sxs-lookup"><span data-stu-id="7bc04-135">Have your IT department open port 5432 tooconnect tooyour Azure SQL Database server.</span></span>

## <a name="get-hello-connection-information"></a><span data-ttu-id="7bc04-136">Merhaba bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="7bc04-136">Get hello connection information</span></span>

<span data-ttu-id="7bc04-137">tooconnect tooyour server tooprovide konağı bilgileri ve erişim kimlik bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="7bc04-137">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="7bc04-138">Merhaba, JSON biçiminde sonucudur.</span><span class="sxs-lookup"><span data-stu-id="7bc04-138">hello result is in JSON format.</span></span> <span data-ttu-id="7bc04-139">Merhaba Not **Admınıstratorlogın** ve **fullyQualifiedDomainName**.</span><span class="sxs-lookup"><span data-stu-id="7bc04-139">Make a note of hello **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
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

## <a name="connect-toopostgresql-database-using-psql"></a><span data-ttu-id="7bc04-140">Psql kullanarak tooPostgreSQL veritabanına bağlan</span><span class="sxs-lookup"><span data-stu-id="7bc04-140">Connect tooPostgreSQL database using psql</span></span>

<span data-ttu-id="7bc04-141">İstemci bilgisayarınızda yüklü PostgreSQL varsa, yerel bir örneğini kullanabilirsiniz [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooconnect tooan Azure PostgreSQL sunucu.</span><span class="sxs-lookup"><span data-stu-id="7bc04-141">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooconnect tooan Azure PostgreSQL server.</span></span> <span data-ttu-id="7bc04-142">Şimdi hello psql komut satırı yardımcı programını tooconnect toohello Azure PostgreSQL sunucu kullanalım.</span><span class="sxs-lookup"><span data-stu-id="7bc04-142">Let's now use hello psql command-line utility tooconnect toohello Azure PostgreSQL server.</span></span>

1. <span data-ttu-id="7bc04-143">Psql komutu tooconnect tooan Azure veritabanı PostgreSQL sunucusu için aşağıdaki hello çalıştırın</span><span class="sxs-lookup"><span data-stu-id="7bc04-143">Run hello following psql command tooconnect tooan Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="7bc04-144">Örneğin, komutu aşağıdaki hello adlı toohello varsayılan veritabanı bağlayan **postgres** PostgreSQL sunucunuzda **mypgserver 20170401.postgres.database.azure.com** erişim kimlik bilgileri kullanılarak.</span><span class="sxs-lookup"><span data-stu-id="7bc04-144">For example, hello following command connects toohello default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="7bc04-145">Merhaba girin `<server_admin_password>` parolası istendiğinde seçtiniz.</span><span class="sxs-lookup"><span data-stu-id="7bc04-145">Enter hello `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
```

2.  <span data-ttu-id="7bc04-146">Bağlı toohello sunucu olduktan sonra boş bir veritabanı hello isteminde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7bc04-146">Once you are connected toohello server, create a blank database at hello prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="7bc04-147">Merhaba istemine komut tooswitch bağlantı toohello yeni oluşturulan veritabanı aşağıdaki hello yürütme **mypgsqldb**:</span><span class="sxs-lookup"><span data-stu-id="7bc04-147">At hello prompt, execute hello following command tooswitch connection toohello newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="connect-toopostgresql-database-using-pgadmin"></a><span data-ttu-id="7bc04-148">PgAdmin kullanarak tooPostgreSQL veritabanına bağlan</span><span class="sxs-lookup"><span data-stu-id="7bc04-148">Connect tooPostgreSQL database using pgAdmin</span></span>

<span data-ttu-id="7bc04-149">Merhaba GUI aracını kullanarak tooconnect tooAzure PostgreSQL server _pgAdmin_</span><span class="sxs-lookup"><span data-stu-id="7bc04-149">tooconnect tooAzure PostgreSQL server using hello GUI tool _pgAdmin_</span></span>
1.  <span data-ttu-id="7bc04-150">Merhaba başlatma _pgAdmin_ istemci bilgisayarınızda uygulama.</span><span class="sxs-lookup"><span data-stu-id="7bc04-150">Launch hello _pgAdmin_ application on your client computer.</span></span> <span data-ttu-id="7bc04-151">_pgAdmin_’i http://www.pgadmin.org/ adresinden yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7bc04-151">You can install _pgAdmin_ from http://www.pgadmin.org/.</span></span>
2.  <span data-ttu-id="7bc04-152">Seçin **yeni sunucu Ekle** hello gelen **hızlı bağlantılar** menüsü.</span><span class="sxs-lookup"><span data-stu-id="7bc04-152">Choose **Add New Server** from hello **Quick Links** menu.</span></span>
3.  <span data-ttu-id="7bc04-153">Merhaba, **Create - Server** iletişim kutusu **genel** sekmesinde, hello sunucu için benzersiz bir kolay ad girin.</span><span class="sxs-lookup"><span data-stu-id="7bc04-153">In hello **Create - Server** dialog box **General** tab, enter a unique friendly Name for hello server.</span></span> <span data-ttu-id="7bc04-154">Örneğin, **Azure PostgreSQL Sunucusu**.</span><span class="sxs-lookup"><span data-stu-id="7bc04-154">Say **Azure PostgreSQL Server**.</span></span>
 <span data-ttu-id="7bc04-155">![pgAdmin aracı - oluştur - sunucu](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span><span class="sxs-lookup"><span data-stu-id="7bc04-155">![pgAdmin tool - create - server](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span></span>
4.  <span data-ttu-id="7bc04-156">Merhaba, **Create - Server** iletişim kutusu, **bağlantı** sekmesi:</span><span class="sxs-lookup"><span data-stu-id="7bc04-156">In hello **Create - Server** dialog box, **Connection** tab:</span></span>
    - <span data-ttu-id="7bc04-157">Merhaba tam sunucu adını girin (örneğin, **mypgserver 20170401.postgres.database.azure.com**) hello içinde **ana bilgisayar adı / adresi** kutusu.</span><span class="sxs-lookup"><span data-stu-id="7bc04-157">Enter hello fully qualified server name (for example, **mypgserver-20170401.postgres.database.azure.com**) in hello **Host Name/ Address** box.</span></span> 
    - <span data-ttu-id="7bc04-158">Bağlantı noktası 5432 hello girin **bağlantı noktası** kutusu.</span><span class="sxs-lookup"><span data-stu-id="7bc04-158">Enter port 5432 into hello **Port** box.</span></span> 
    - <span data-ttu-id="7bc04-159">Merhaba girin **Sunucu Yöneticisi oturum açma (user@mypgserver)** daha önce bu hızlı başlangıç ve hello hello sunucu oluşturduğunuzda girdiğiniz parola elde **kullanıcıadı** ve **parola** kutular, sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="7bc04-159">Enter hello **Server admin login (user@mypgserver)** obtained earlier in this quickstart and password you entered when you created hello server into hello **Username** and **Password** boxes, respectively.</span></span>
    - <span data-ttu-id="7bc04-160">**SSL Modu**’nu **Gerekli** olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="7bc04-160">Select **SSL Mode** as **Require**.</span></span> <span data-ttu-id="7bc04-161">Tüm Azure PostgreSQL sunucuları, varsayılan olarak SSL’yi zorunla tutma seçeneği AÇIK konumundayken oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7bc04-161">By default, all Azure PostgreSQL servers are created with SSL enforcing turned ON.</span></span> <span data-ttu-id="7bc04-162">SSL zorlama, devre dışı tooturn ayrıntıları görmek [zorlamayı SSL](./concepts-ssl-connection-security.md).</span><span class="sxs-lookup"><span data-stu-id="7bc04-162">tooturn OFF SSL enforcing, see details in [Enforcing SSL](./concepts-ssl-connection-security.md).</span></span>

    ![pgAdmin - Oluştur - Sunucu](./media/quickstart-create-server-database-azure-cli/2-pgadmin-create-server.png)
5.  <span data-ttu-id="7bc04-164">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7bc04-164">Click **Save**.</span></span>
6.  <span data-ttu-id="7bc04-165">Merhaba tarayıcı sol hello bölmesinde **sunucu grupları**.</span><span class="sxs-lookup"><span data-stu-id="7bc04-165">In hello Browser left pane, expand hello **Server Groups**.</span></span> <span data-ttu-id="7bc04-166">**Azure PostgreSQL Sunucusu** adlı sunucunuzu seçin.</span><span class="sxs-lookup"><span data-stu-id="7bc04-166">Choose your server **Azure PostgreSQL Server**.</span></span>
7.  <span data-ttu-id="7bc04-167">Merhaba seçin **Server** bağlı ve ardından **veritabanları** altındaki.</span><span class="sxs-lookup"><span data-stu-id="7bc04-167">Choose hello **Server** you connected to, and then choose **Databases** under it.</span></span> 
8.  <span data-ttu-id="7bc04-168">Sağ **veritabanları** tooCreate bir veritabanı.</span><span class="sxs-lookup"><span data-stu-id="7bc04-168">Right-click on **Databases** tooCreate a Database.</span></span>
9.  <span data-ttu-id="7bc04-169">Veritabanı adı Seç **mypgsqldb** ve onun için hello sahibi olarak Sunucu Yöneticisi oturum açma **mylogin**.</span><span class="sxs-lookup"><span data-stu-id="7bc04-169">Choose a database name **mypgsqldb** and hello owner for it as server admin login **mylogin**.</span></span>
10. <span data-ttu-id="7bc04-170">Tıklatın **kaydetmek** toocreate boş bir veritabanı.</span><span class="sxs-lookup"><span data-stu-id="7bc04-170">Click **Save** toocreate a blank database.</span></span>
11. <span data-ttu-id="7bc04-171">Merhaba, **tarayıcı**, hello genişletin **sunucuları** grubu.</span><span class="sxs-lookup"><span data-stu-id="7bc04-171">In hello **Browser**, expand hello **Servers** group.</span></span> <span data-ttu-id="7bc04-172">Oluşturduğunuz hello sunucusunu genişletin ve hello veritabanı bkz **mypgsqldb** altındaki.</span><span class="sxs-lookup"><span data-stu-id="7bc04-172">Expand hello server you created, and see hello database **mypgsqldb** under it.</span></span>
 <span data-ttu-id="7bc04-173">![pgAdmin - Oluştur - Veritabanı](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span><span class="sxs-lookup"><span data-stu-id="7bc04-173">![pgAdmin - Create - Database](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span></span>


## <a name="clean-up-resources"></a><span data-ttu-id="7bc04-174">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="7bc04-174">Clean up resources</span></span>

<span data-ttu-id="7bc04-175">Temiz hello silerek hello hızlı başlangıcı oluşturulan tüm kaynakları [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7bc04-175">Clean up all resources you created in hello quickstart by deleting hello [Azure resource group](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!TIP]
> <span data-ttu-id="7bc04-176">Bu koleksiyondaki diğer hızlı başlangıçlar, bu hızlı başlangıcı temel alır.</span><span class="sxs-lookup"><span data-stu-id="7bc04-176">Other quickstarts in this collection build upon this quick start.</span></span> <span data-ttu-id="7bc04-177">Sonraki ile toowork toocontinue planlıyorsanız bu quickstart oluşturulan kaynakları quickstarts, değil temizleme hello.</span><span class="sxs-lookup"><span data-stu-id="7bc04-177">If you plan toocontinue on toowork with subsequent quickstarts, do not clean up hello resources created in this quickstart.</span></span> <span data-ttu-id="7bc04-178">Toocontinue düşünmüyorsanız, aşağıdaki adımları toodelete hello hello Azure CLI Bu hızlı başlangıcı tarafından oluşturulan tüm kaynakları kullanın.</span><span class="sxs-lookup"><span data-stu-id="7bc04-178">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quickstart in hello Azure CLI.</span></span>

```azurecli-interactive
az group delete --name myresourcegroup
```

<span data-ttu-id="7bc04-179">Yalnızca toodelete hello bir yeni oluşturulan sunucu isterseniz, çalıştırabilirsiniz [az postgres server silme](/cli/azure/postgres/server#delete) komutu.</span><span class="sxs-lookup"><span data-stu-id="7bc04-179">If you just would like toodelete hello one newly created server, you can run [az postgres server delete](/cli/azure/postgres/server#delete) command.</span></span>
```azurecli-interactive
az postgres server delete --resource-group myresourcegroup --name mypgserver-20170401
```

## <a name="next-steps"></a><span data-ttu-id="7bc04-180">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7bc04-180">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="7bc04-181">Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme</span><span class="sxs-lookup"><span data-stu-id="7bc04-181">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
