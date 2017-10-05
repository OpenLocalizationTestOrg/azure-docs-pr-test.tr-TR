---
title: "Azure'da Docker Python ve PostgreSQL bir web uygulaması oluşturma | Microsoft Docs"
description: "Bir PostgreSQL veritabanına bağlantı ile Azure içinde çalışma Docker Python uygulaması alma hakkında bilgi."
services: app-service\web
documentationcenter: python
author: berndverst
manager: erikre
editor: 
ms.assetid: 2bada123-ef18-44e5-be71-e16323b20466
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: tutorial
ms.date: 05/03/2017
ms.author: beverst
ms.custom: mvc
ms.openlocfilehash: e70f85a1eb4a6e1a81e0ca4fae228ca97deca6fe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a><span data-ttu-id="fecd3-103">Azure'da Docker Python ve PostgreSQL bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="fecd3-103">Build a Docker Python and PostgreSQL web app in Azure</span></span>

<span data-ttu-id="fecd3-104">Azure Web Apps düzeyde ölçeklenebilir, otomatik olarak düzeltme eki uygulama web barındırma hizmeti sağlar.</span><span class="sxs-lookup"><span data-stu-id="fecd3-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="fecd3-105">Bu öğretici, temel bir Docker Python web uygulaması oluşturma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="fecd3-105">This tutorial shows how to create a basic Docker Python web app in Azure.</span></span> <span data-ttu-id="fecd3-106">Bu uygulama bir PostgreSQL veritabanına bağlanırsınız.</span><span class="sxs-lookup"><span data-stu-id="fecd3-106">You'll connect this app to a PostgreSQL database.</span></span> <span data-ttu-id="fecd3-107">İşiniz bittiğinde, Docker kapsayıcısı içinde çalışan bir Python Flask uygulaması gerekir [Azure App Service Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fecd3-107">When you're done, you'll have a Python Flask application running within a Docker container on [Azure App Service Web Apps](app-service-web-overview.md).</span></span>

![Docker Python Flask uygulamada Azure uygulama hizmeti](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

<span data-ttu-id="fecd3-109">MacOS üzerinde aşağıdaki adımları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fecd3-109">You can follow the steps below on macOS.</span></span> <span data-ttu-id="fecd3-110">Linux ve Windows yönergeleri çoğu durumda aynıdır, ancak bu öğreticide farklar ayrıntılı değil.</span><span class="sxs-lookup"><span data-stu-id="fecd3-110">Linux and Windows instructions are the same in most cases, but the differences are not detailed in this tutorial.</span></span>
 
## <a name="prerequisites"></a><span data-ttu-id="fecd3-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fecd3-111">Prerequisites</span></span>

<span data-ttu-id="fecd3-112">Bu öğreticiyi tamamlamak için:</span><span class="sxs-lookup"><span data-stu-id="fecd3-112">To complete this tutorial:</span></span>

1. [<span data-ttu-id="fecd3-113">Git'i yükleyin</span><span class="sxs-lookup"><span data-stu-id="fecd3-113">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="fecd3-114">Python'ı yükleyin</span><span class="sxs-lookup"><span data-stu-id="fecd3-114">Install Python</span></span>](https://www.python.org/downloads/)
1. [<span data-ttu-id="fecd3-115">Yükleme ve PostgreSQL çalıştırma</span><span class="sxs-lookup"><span data-stu-id="fecd3-115">Install and run PostgreSQL</span></span>](https://www.postgresql.org/download/)
1. [<span data-ttu-id="fecd3-116">Docker Community Edition'ı yükleme</span><span class="sxs-lookup"><span data-stu-id="fecd3-116">Install Docker Community Edition</span></span>](https://www.docker.com/community-edition)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fecd3-117">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fecd3-117">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="fecd3-118">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fecd3-118">Run `az --version` to find the version.</span></span> <span data-ttu-id="fecd3-119">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fecd3-119">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-postgresql-installation-and-create-a-database"></a><span data-ttu-id="fecd3-120">Yerel PostgreSQL yüklemeyi sınamak ve bir veritabanı oluştur</span><span class="sxs-lookup"><span data-stu-id="fecd3-120">Test local PostgreSQL installation and create a database</span></span>

<span data-ttu-id="fecd3-121">Terminal penceresi açın ve Çalıştır `psql postgres` yerel PostgreSQL sunucunuza bağlanmak için.</span><span class="sxs-lookup"><span data-stu-id="fecd3-121">Open the terminal window and run `psql postgres` to connect to your local PostgreSQL server.</span></span>

```bash
psql postgres
```

<span data-ttu-id="fecd3-122">Bağlantı başarılı olursa, PostgreSQL veritabanınız çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="fecd3-122">If your connection is successful, your PostgreSQL database is running.</span></span> <span data-ttu-id="fecd3-123">Aksi takdirde, yerel PostgresQL veritabanınızı verilen adımları izleyerek başlatıldığından emin olun [yüklemeleri - PostgreSQL çekirdek dağıtım](https://www.postgresql.org/download/).</span><span class="sxs-lookup"><span data-stu-id="fecd3-123">If not, make sure that your local PostgresQL database is started by following the steps at [Downloads - PostgreSQL Core Distribution](https://www.postgresql.org/download/).</span></span>

<span data-ttu-id="fecd3-124">Adlı bir veritabanı oluşturmak *eventregistration* ve adlı bir ayrı veritabanı kullanıcı ayarlama *Yöneticisi* parolayla *supersecretpass*.</span><span class="sxs-lookup"><span data-stu-id="fecd3-124">Create a database called *eventregistration* and set up a separate database user named *manager* with password *supersecretpass*.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration TO manager;
```
<span data-ttu-id="fecd3-125">Tür *\q* PostgreSQL istemci çıkmak için.</span><span class="sxs-lookup"><span data-stu-id="fecd3-125">Type *\q* to exit the PostgreSQL client.</span></span> 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a><span data-ttu-id="fecd3-126">Yerel Python Flask uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="fecd3-126">Create local Python Flask application</span></span>

<span data-ttu-id="fecd3-127">Bu adımda, yerel Python Flask projesi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="fecd3-127">In this step, you set up the local Python Flask project.</span></span>

### <a name="clone-the-sample-application"></a><span data-ttu-id="fecd3-128">Örnek uygulamayı kopyalama</span><span class="sxs-lookup"><span data-stu-id="fecd3-128">Clone the sample application</span></span>

<span data-ttu-id="fecd3-129">Terminal penceresi açın ve `CD` bir çalışma dizini için.</span><span class="sxs-lookup"><span data-stu-id="fecd3-129">Open the terminal window, and `CD` to a working directory.</span></span>  

<span data-ttu-id="fecd3-130">Örnek depoyu kopyalayın ve Git için aşağıdaki komutları çalıştırın *0,1 initialapp* serbest bırakın.</span><span class="sxs-lookup"><span data-stu-id="fecd3-130">Run the following commands to clone the sample repository and go to the *0.1-initialapp* release.</span></span>

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

<span data-ttu-id="fecd3-131">Bu örnek depo içeren bir [Flask](http://flask.pocoo.org/) uygulama.</span><span class="sxs-lookup"><span data-stu-id="fecd3-131">This sample repository contains a [Flask](http://flask.pocoo.org/) application.</span></span> 

### <a name="run-the-application"></a><span data-ttu-id="fecd3-132">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="fecd3-132">Run the application</span></span>

> [!NOTE] 
> <span data-ttu-id="fecd3-133">Bir sonraki adımda üretim veritabanı ile kullanmak için Docker kapsayıcısı oluşturarak bu işlemi basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="fecd3-133">In a later step you simplify this process by building a Docker container to use with the production database.</span></span>

<span data-ttu-id="fecd3-134">Gereken paketleri yükleyip uygulamayı başlatın.</span><span class="sxs-lookup"><span data-stu-id="fecd3-134">Install the required packages and start the application.</span></span>

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="fecd3-135">Uygulamanın tam olarak yüklendiğinde, aşağıdaki iletiye benzer bir şey görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="fecd3-135">When the app is fully loaded, you see something similar to the following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="fecd3-136">Bir tarayıcıda http://127.0.0.1:5000 gidin.</span><span class="sxs-lookup"><span data-stu-id="fecd3-136">Navigate to http://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="fecd3-137">Tıklatın **kaydedin!**</span><span class="sxs-lookup"><span data-stu-id="fecd3-137">Click **Register!**</span></span> <span data-ttu-id="fecd3-138">ve bir test kullanıcısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fecd3-138">and create a test user.</span></span>

![Yerel olarak çalışan Python Flask uygulama](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

<span data-ttu-id="fecd3-140">Flask örnek uygulamanın kullanıcı verilerini veritabanında depolar.</span><span class="sxs-lookup"><span data-stu-id="fecd3-140">The Flask sample application stores user data in the database.</span></span> <span data-ttu-id="fecd3-141">Bir kullanıcı kaydetme sırasında başarılı olursa, veri uygulamanızı yerel PostgreSQL veritabanına yazma.</span><span class="sxs-lookup"><span data-stu-id="fecd3-141">If you are successful at registering a user, your app is writing data to the local PostgreSQL database.</span></span>

<span data-ttu-id="fecd3-142">Flask sunucu zaman durdurmak için Ctrl + C terminale yazın.</span><span class="sxs-lookup"><span data-stu-id="fecd3-142">To stop the Flask server at anytime, type Ctrl+C in the terminal.</span></span> 

## <a name="create-a-production-postgresql-database"></a><span data-ttu-id="fecd3-143">Bir üretim PostgreSQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fecd3-143">Create a production PostgreSQL database</span></span>

<span data-ttu-id="fecd3-144">Bu adımda, Azure PostgreSQL veritabanında oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fecd3-144">In this step, you create a PostgreSQL database in Azure.</span></span> <span data-ttu-id="fecd3-145">Uygulamanızın Azure'a dağıtıldığında, bu bulut veritabanı kullanır.</span><span class="sxs-lookup"><span data-stu-id="fecd3-145">When your app is deployed to Azure, it will use this cloud database.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="fecd3-146">Azure'da oturum açma</span><span class="sxs-lookup"><span data-stu-id="fecd3-146">Log in to Azure</span></span>

<span data-ttu-id="fecd3-147">Şimdi Python uygulamanızı Azure App Service'te barındırmak için gereken kaynakları oluşturmak için Azure CLI 2.0 kullanmayı adımıdır.</span><span class="sxs-lookup"><span data-stu-id="fecd3-147">You are now going to use the Azure CLI 2.0 to create the resources needed to host your Python application in Azure App Service.</span></span>  <span data-ttu-id="fecd3-148">[az login](/cli/azure/#login) komutuyla Azure aboneliğinizde oturum açın ve ekrandaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="fecd3-148">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="fecd3-149">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="fecd3-149">Create a resource group</span></span>

<span data-ttu-id="fecd3-150">[az group create](/cli/azure/group#create) ile bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fecd3-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with the [az group create](/cli/azure/group#create).</span></span> 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="fecd3-151">Aşağıdaki örnek Batı ABD bölgesinde bir kaynak grubu oluşturur:</span><span class="sxs-lookup"><span data-stu-id="fecd3-151">The following example creates a resource group in the West US region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

<span data-ttu-id="fecd3-152">Kullanım [az appservice listesi-konumları](/cli/azure/appservice#list-locations) listesi kullanılabilir konumlar için Azure CLI komutu.</span><span class="sxs-lookup"><span data-stu-id="fecd3-152">Use the [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command to list available locations.</span></span>

### <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="fecd3-153">PostgreSQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="fecd3-153">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="fecd3-154">Bir PostgreSQL sunucusuyla [az postgres sunucusu oluşturmak](/cli/azure/documentdb#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="fecd3-154">Create a PostgreSQL server with the [az postgres server create](/cli/azure/documentdb#create) command.</span></span>

<span data-ttu-id="fecd3-155">Aşağıdaki komutta için bir benzersiz sunucu adı yerine  *\<postgresql_name >* yer tutucu ve bir kullanıcı adı için  *\<admin_username >* yer tutucu.</span><span class="sxs-lookup"><span data-stu-id="fecd3-155">In the following command, substitute a unique server name for the *\<postgresql_name>* placeholder and a user name for the *\<admin_username>* placeholder.</span></span> <span data-ttu-id="fecd3-156">Sunucu adı PostgreSQL uç noktanızı bir parçası olarak kullanılır (`https://<postgresql_name>.postgres.database.azure.com`), adının Azure içindeki tüm sunucular arasında benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fecd3-156">The server name is used as part of your PostgreSQL endpoint (`https://<postgresql_name>.postgres.database.azure.com`), so the name needs to be unique across all servers in Azure.</span></span> <span data-ttu-id="fecd3-157">İlk veritabanı yönetici kullanıcı hesabı için kullanıcı adıdır.</span><span class="sxs-lookup"><span data-stu-id="fecd3-157">The user name is for the initial database admin user account.</span></span> <span data-ttu-id="fecd3-158">Bu kullanıcı için bir parola çekme istenir.</span><span class="sxs-lookup"><span data-stu-id="fecd3-158">You are prompted to pick a password for this user.</span></span>

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

<span data-ttu-id="fecd3-159">Azure CLI PostgreSQL sunucu için Azure veritabanı oluşturulduğunda, bilgileri aşağıdaki örneğe benzer şekilde gösterir:</span><span class="sxs-lookup"><span data-stu-id="fecd3-159">When the Azure Database for PostgreSQL server is created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "administratorLogin": "<my_admin_username>",
  "fullyQualifiedDomainName": "<postgresql_name>.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>",
  "location": "westus",
  "name": "<postgresql_name>",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": 100,
    "family": null,
    "name": "PGSQLS3M100",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

### <a name="create-a-firewall-rule-for-the-azure-database-for-postgresql-server"></a><span data-ttu-id="fecd3-160">PostgreSQL sunucu için Azure veritabanı için bir güvenlik duvarı kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fecd3-160">Create a firewall rule for the Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="fecd3-161">Tüm IP adreslerinden veritabanına erişim için aşağıdaki Azure CLI komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fecd3-161">Run the following Azure CLI command to allow access to the database from all IP addresses.</span></span>

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

<span data-ttu-id="fecd3-162">Azure CLI aşağıdaki örneğe benzer bir çıktı ile güvenlik duvarı kuralı oluşturmayı onaylar:</span><span class="sxs-lookup"><span data-stu-id="fecd3-162">The Azure CLI confirms the firewall rule creation with output similar to the following example:</span></span>

```json
{
  "endIpAddress": "255.255.255.255",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>/firewallRules/AllowAllIPs",
  "name": "AllowAllIPs",
  "resourceGroup": "myResourceGroup",
  "startIpAddress": "0.0.0.0",
  "type": "Microsoft.DBforPostgreSQL/servers/firewallRules"
}
```

## <a name="connect-your-python-flask-application-to-the-database"></a><span data-ttu-id="fecd3-163">Python Flask uygulamanız veritabanına bağlan</span><span class="sxs-lookup"><span data-stu-id="fecd3-163">Connect your Python Flask application to the database</span></span>

<span data-ttu-id="fecd3-164">Bu adımda, Python Flask örnek uygulamanızı oluşturduğunuz PostgreSQL server için Azure veritabanına bağlanın.</span><span class="sxs-lookup"><span data-stu-id="fecd3-164">In this step, you connect your Python Flask sample application to the Azure Database for PostgreSQL server you created.</span></span>

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a><span data-ttu-id="fecd3-165">Boş bir veritabanı oluşturun ve yeni bir veritabanı uygulama kullanıcı ayarlama</span><span class="sxs-lookup"><span data-stu-id="fecd3-165">Create an empty database and set up a new database application user</span></span>

<span data-ttu-id="fecd3-166">Yalnızca tek bir veritabanına erişimi olan bir veritabanı kullanıcısı oluşturmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fecd3-166">Create a database user with access to a single database only.</span></span> <span data-ttu-id="fecd3-167">Sunucuya uygulama tam erişimi vermekten kaçının için bu kimlik bilgileri kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="fecd3-167">You'll use these credentials to avoid giving the application full access to the server.</span></span>

<span data-ttu-id="fecd3-168">(Yönetici parolanızı girmeniz istenir) veritabanına bağlanın.</span><span class="sxs-lookup"><span data-stu-id="fecd3-168">Connect to the database (you're prompted for your admin password).</span></span>

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

<span data-ttu-id="fecd3-169">Veritabanı ve kullanıcı PostgreSQL CLI oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fecd3-169">Create the database and user from the PostgreSQL CLI.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration TO manager;
```

<span data-ttu-id="fecd3-170">Tür *\q* PostgreSQL istemci çıkmak için.</span><span class="sxs-lookup"><span data-stu-id="fecd3-170">Type *\q* to exit the PostgreSQL client.</span></span>

### <a name="test-the-application-locally-against-the-azure-postgresql-database"></a><span data-ttu-id="fecd3-171">Uygulamayı yerel olarak Azure PostgreSQL veritabanına karşı test etme</span><span class="sxs-lookup"><span data-stu-id="fecd3-171">Test the application locally against the Azure PostgreSQL database</span></span> 

<span data-ttu-id="fecd3-172">Geri şimdi gidip *uygulama* klasörü kopyalanan Github depo veritabanı ortam değişkenleri güncelleştirerek Python Flask uygulamayı çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fecd3-172">Going back now to the *app* folder of the cloned Github repository, you can run the Python Flask application by updating the database environment variables.</span></span>

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="fecd3-173">Uygulamanın tam olarak yüklendiğinde, aşağıdaki iletiye benzer bir şey görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="fecd3-173">When the app is fully loaded, you see something similar to the following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="fecd3-174">Bir tarayıcıda http://127.0.0.1:5000 gidin.</span><span class="sxs-lookup"><span data-stu-id="fecd3-174">Navigate to http://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="fecd3-175">Tıklatın **kaydedin!**</span><span class="sxs-lookup"><span data-stu-id="fecd3-175">Click **Register!**</span></span> <span data-ttu-id="fecd3-176">ve bir test kaydı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fecd3-176">and create a test registration.</span></span> <span data-ttu-id="fecd3-177">Şimdi, Azure veritabanına veri yazma.</span><span class="sxs-lookup"><span data-stu-id="fecd3-177">You are now writing data to the database in Azure.</span></span>

![Yerel olarak çalışan Python Flask uygulama](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-the-application-from-a-docker-container"></a><span data-ttu-id="fecd3-179">Docker kapsayıcıdan uygulamayı çalıştırmayı</span><span class="sxs-lookup"><span data-stu-id="fecd3-179">Running the application from a Docker Container</span></span>

<span data-ttu-id="fecd3-180">Docker kapsayıcısı görüntüsünü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fecd3-180">Build the Docker container image.</span></span>

```bash
cd ..
docker build -t flask-postgresql-sample .
```

<span data-ttu-id="fecd3-181">Docker başarıyla kapsayıcı oluşturulduğu bir onay görüntüler.</span><span class="sxs-lookup"><span data-stu-id="fecd3-181">Docker displays a confirmation that it successfully created the container.</span></span>

```bash
Successfully built 7548f983a36b
```

<span data-ttu-id="fecd3-182">Bir ortam değişkeni dosyasına veritabanı ortam değişkenleri eklemek *db.env*.</span><span class="sxs-lookup"><span data-stu-id="fecd3-182">Add database environment variables to an environment variable file *db.env*.</span></span> <span data-ttu-id="fecd3-183">Uygulama Azure PostgreSQL üretim veritabanına bağlanır.</span><span class="sxs-lookup"><span data-stu-id="fecd3-183">The app will connect to the PostgreSQL production database in Azure.</span></span>

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

<span data-ttu-id="fecd3-184">Docker kapsayıcısı içinde uygulamadan çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fecd3-184">Run the app from within the Docker container.</span></span> <span data-ttu-id="fecd3-185">Aşağıdaki komutu ortam değişken dosyası belirtir ve yerel bağlantı noktası 5000 için varsayılan Flask bağlantı noktası 5000 eşler.</span><span class="sxs-lookup"><span data-stu-id="fecd3-185">The following command specifies the environment variable file and maps the default Flask port 5000 to local port 5000.</span></span>

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

<span data-ttu-id="fecd3-186">Çıktı ne daha önce gördüğünüzle için benzer.</span><span class="sxs-lookup"><span data-stu-id="fecd3-186">The output is similar to what you saw earlier.</span></span> <span data-ttu-id="fecd3-187">Ancak, ilk veritabanı geçiş artık gerçekleştirilmesi gerekir ve bu nedenle atlanır.</span><span class="sxs-lookup"><span data-stu-id="fecd3-187">However, the initial database migration no longer needs to be performed and therefore is skipped.</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="fecd3-188">Veritabanı zaten daha önce oluşturduğunuz kayıt içeriyor.</span><span class="sxs-lookup"><span data-stu-id="fecd3-188">The database already contains the registration you created previously.</span></span>

![Docker kapsayıcısı tabanlı Python Flask uygulama yerel olarak çalıştırma](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-the-docker-container-to-a-container-registry"></a><span data-ttu-id="fecd3-190">Docker kapsayıcısı bir kapsayıcı kayıt defterine karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="fecd3-190">Upload the Docker container to a container registry</span></span>

<span data-ttu-id="fecd3-191">Bu adımda, bir kapsayıcı kayıt defterine Docker kapsayıcısı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="fecd3-191">In this step, you upload the Docker container to a container registry.</span></span> <span data-ttu-id="fecd3-192">Azure kapsayıcı kayıt defteri kullanırsınız, ancak Docker Hub gibi diğer popüler olanlar da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fecd3-192">You'll use Azure Container Registry, but you could also use other popular ones such as Docker Hub.</span></span>

### <a name="create-an-azure-container-registry"></a><span data-ttu-id="fecd3-193">Azure Container Registry oluşturma</span><span class="sxs-lookup"><span data-stu-id="fecd3-193">Create an Azure Container Registry</span></span>

<span data-ttu-id="fecd3-194">Bir kapsayıcı kayıt defteri oluşturmak için aşağıdaki komutu yerine  *\<registry_name >* tercih ettiğiniz bir benzersiz Azure kapsayıcı kayıt defteri adı.</span><span class="sxs-lookup"><span data-stu-id="fecd3-194">In the following command to create a container registry replace *\<registry_name>* with a unique Azure container registry name of your choice.</span></span>

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

<span data-ttu-id="fecd3-195">Çıktı</span><span class="sxs-lookup"><span data-stu-id="fecd3-195">Output</span></span>
```json
{
  "adminUserEnabled": false,
  "creationDate": "2017-05-04T08:50:55.635688+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/<registry_name>",
  "location": "westus",
  "loginServer": "<registry_name>.azurecr.io",
  "name": "<registry_name>",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "<registry_name>01234"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

### <a name="retrieve-the-registry-credentials-for-pushing-and-pulling-docker-images"></a><span data-ttu-id="fecd3-196">Docker görüntüleri çekme ve itme için kayıt defteri kimlik bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="fecd3-196">Retrieve the registry credentials for pushing and pulling Docker images</span></span>

<span data-ttu-id="fecd3-197">Kayıt defteri kimlik bilgilerini göstermek için önce yönetici modunu etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="fecd3-197">To show registry credentials, enable admin mode first.</span></span>

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

<span data-ttu-id="fecd3-198">İki parola bakın.</span><span class="sxs-lookup"><span data-stu-id="fecd3-198">You see two passwords.</span></span> <span data-ttu-id="fecd3-199">Kullanıcı adı ve ilk parola not edin.</span><span class="sxs-lookup"><span data-stu-id="fecd3-199">Make note of the user name and the first password.</span></span>

```json
{
  "passwords": [
    {
      "name": "password",
      "value": "<registry_password>"
    },
    {
      "name": "password2",
      "value": "<registry_password2>"
    }
  ],
  "username": "<registry_name>"
}
```

### <a name="upload-your-docker-container-to-azure-container-registry"></a><span data-ttu-id="fecd3-200">Azure kapsayıcı kayıt defterine Docker kapsayıcısı karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="fecd3-200">Upload your Docker container to Azure Container Registry</span></span>

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-the-docker-python-flask-application-to-azure"></a><span data-ttu-id="fecd3-201">Docker Python Flask uygulamayı Azure'a dağıtma</span><span class="sxs-lookup"><span data-stu-id="fecd3-201">Deploy the Docker Python Flask application to Azure</span></span>

<span data-ttu-id="fecd3-202">Bu adımda, Docker kapsayıcısı tabanlı Python Flask uygulamanızı Azure App Service'e dağıtın.</span><span class="sxs-lookup"><span data-stu-id="fecd3-202">In this step, you deploy your Docker container-based Python Flask application to Azure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="fecd3-203">App Service planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fecd3-203">Create an App Service plan</span></span>

<span data-ttu-id="fecd3-204">[az appservice plan create](/cli/azure/appservice/plan#create) komutu ile bir App Service planı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fecd3-204">Create an App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="fecd3-205">Aşağıdaki örnek, adlandırılmış bir Linux tabanlı uygulama hizmeti planı oluşturur *myAppServicePlan* kullanarak S1 fiyatlandırma katmanı:</span><span class="sxs-lookup"><span data-stu-id="fecd3-205">The following example creates a Linux-based App Service plan named *myAppServicePlan* using the S1 pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

<span data-ttu-id="fecd3-206">Uygulama hizmeti planı oluşturulduğunda, Azure CLI bilgileri aşağıdaki örneğe benzer şekilde gösterir:</span><span class="sxs-lookup"><span data-stu-id="fecd3-206">When the App Service plan is created, the Azure CLI shows information similar to the following example:</span></span>

```json 
{
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "West US",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "linux",
  "location": "West US",
  "maximumNumberOfWorkers": 10,
  "name": "myAppServicePlan",
  "numberOfSites": 0,
  "perSiteScaling": false,
  "provisioningState": "Succeeded",
  "reserved": true,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capabilities": null,
    "capacity": 1,
    "family": "S",
    "locations": null,
    "name": "S1",
    "size": "S1",
    "skuCapacity": null,
    "tier": "Standard"
  },
  "status": "Ready",
  "subscription": "00000000-0000-0000-0000-000000000000",
  "tags": null,
  "targetWorkerCount": 0,
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
}
``` 

### <a name="create-a-web-app"></a><span data-ttu-id="fecd3-207">Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="fecd3-207">Create a web app</span></span>

<span data-ttu-id="fecd3-208">Bir web uygulaması oluşturma *myAppServicePlan* uygulama hizmeti planıyla [az webapp oluşturmak](/cli/azure/webapp#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="fecd3-208">Create a web app in the *myAppServicePlan* App Service plan with the [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="fecd3-209">Web uygulaması kodunuzu dağıtmaya barındırma bir alan sağlar ve dağıtılmış uygulamanın görüntülemek bir URL sağlar.</span><span class="sxs-lookup"><span data-stu-id="fecd3-209">The web app gives you a hosting space to deploy your code and provides a URL for you to view the deployed application.</span></span> <span data-ttu-id="fecd3-210">Web uygulaması oluşturmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="fecd3-210">Use  to create the web app.</span></span> 

<span data-ttu-id="fecd3-211">Aşağıdaki komutta,  *\<app_name >* yer tutucu benzersiz bir uygulama adına sahip.</span><span class="sxs-lookup"><span data-stu-id="fecd3-211">In the following command, replace the *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="fecd3-212">Bu ad web uygulaması için varsayılan URL parçası kitabıdır adının tüm Azure uygulama hizmetinde uygulamalar arasında benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fecd3-212">This name is part of the default URL for the web app, so the name needs to be unique across all apps in Azure App Service.</span></span> 

```azurecli
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="fecd3-213">Web uygulaması oluşturulduğunda Azure CLI aşağıda yer alan örnekteki gibi bilgiler gösterir:</span><span class="sxs-lookup"><span data-stu-id="fecd3-213">When the web app has been created, the Azure CLI shows information similar to the following example:</span></span> 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-the-database-environment-variables"></a><span data-ttu-id="fecd3-214">Veritabanı ortam değişkenlerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="fecd3-214">Configure the database environment variables</span></span>

<span data-ttu-id="fecd3-215">Öğreticide daha önce PostgreSQL veritabanına bağlanmak için ortam değişkenleri tanımlı.</span><span class="sxs-lookup"><span data-stu-id="fecd3-215">Earlier in the tutorial, you defined environment variables to connect to your PostgreSQL database.</span></span>

<span data-ttu-id="fecd3-216">Ortam değişkenleri olarak ayarladığınız App Service'te _uygulama ayarları_ kullanarak [az webapp config appsettings kümesi](/cli/azure/webapp/config#set) komutu.</span><span class="sxs-lookup"><span data-stu-id="fecd3-216">In App Service, you set environment variables as _app settings_ by using the [az webapp config appsettings set](/cli/azure/webapp/config#set) command.</span></span> 

<span data-ttu-id="fecd3-217">Aşağıdaki örnek veritabanı bağlantı ayrıntıları uygulama ayarlarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="fecd3-217">The following example specifies the database connection details as app settings.</span></span> <span data-ttu-id="fecd3-218">Ayrıca kullanır *bağlantı noktası* değişkeni eşlemesine bağlantı noktası 5000 bağlantı noktası 80 üzerinde HTTP trafiği almak için Docker kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="fecd3-218">It also uses the *PORT* variable to map PORT 5000 from your Docker Container to receive HTTP traffic on PORT 80.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a><span data-ttu-id="fecd3-219">Docker kapsayıcısı dağıtımını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fecd3-219">Configure Docker container deployment</span></span> 

<span data-ttu-id="fecd3-220">Uygulama hizmeti otomatik olarak karşıdan yükle ve Docker kapsayıcısı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fecd3-220">AppService can automatically download and run a Docker container.</span></span>

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

<span data-ttu-id="fecd3-221">Docker kapsayıcısı güncelleştirmek veya ayarlarını değiştirmek olduğunda, uygulamayı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="fecd3-221">Whenever you update the Docker container or change the settings, restart the app.</span></span> <span data-ttu-id="fecd3-222">Yeniden başlatma, tüm ayarları uygulanır ve en son kapsayıcı kayıt defterinden çekilir sağlar.</span><span class="sxs-lookup"><span data-stu-id="fecd3-222">Restarting ensures that all settings are applied and the latest container is pulled from the registry.</span></span>

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="fecd3-223">Azure web uygulaması'na göz atın</span><span class="sxs-lookup"><span data-stu-id="fecd3-223">Browse to the Azure web app</span></span> 

<span data-ttu-id="fecd3-224">Web tarayıcınız üzerinden dağıtılan web uygulamasının göz atın.</span><span class="sxs-lookup"><span data-stu-id="fecd3-224">Browse to the deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> <span data-ttu-id="fecd3-225">Web uygulaması kapsayıcı indirilir ve kapsayıcı yapılandırma değiştirildikten sonra başlatıldı gerektiğinden yük daha uzun sürer.</span><span class="sxs-lookup"><span data-stu-id="fecd3-225">The web app takes longer to load because the container has to be downloaded and started after the container configuration is changed.</span></span>

<span data-ttu-id="fecd3-226">Önceki adımda Azure üretim veritabanına kaydedildi önceden kaydedilmiş konuklar bakın.</span><span class="sxs-lookup"><span data-stu-id="fecd3-226">You see previously registered guests that were saved to the Azure production database in the previous step.</span></span>

![Docker kapsayıcısı tabanlı Python Flask uygulama yerel olarak çalıştırma](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

<span data-ttu-id="fecd3-228">**Tebrikler!**</span><span class="sxs-lookup"><span data-stu-id="fecd3-228">**Congratulations!**</span></span> <span data-ttu-id="fecd3-229">Azure App Service'te bir Docker kapsayıcısı tabanlı bir Python Flask uygulamanın çalıştırdığınız.</span><span class="sxs-lookup"><span data-stu-id="fecd3-229">You're running a Docker container-based Python Flask app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="fecd3-230">Güncelleştirme veri modeli ve yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="fecd3-230">Update data model and redeploy</span></span>

<span data-ttu-id="fecd3-231">Bu adımda, Konuk modeli güncelleştirerek her olay kaydı katılanların sayısı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fecd3-231">In this step, you add the number of attendees to each event registration by updating the Guest model.</span></span>

<span data-ttu-id="fecd3-232">Kullanıma *0.2 geçiş* yayın aşağıdaki git komutu ile:</span><span class="sxs-lookup"><span data-stu-id="fecd3-232">Check out the *0.2-migration* release with the following git command:</span></span>

```bash
git checkout tags/0.2-migration
```

<span data-ttu-id="fecd3-233">Bu sürüm zaten gerekli görünümleri, denetleyicileri ve modeli için yapılan değişiklikler.</span><span class="sxs-lookup"><span data-stu-id="fecd3-233">This release already made the necessary changes to views, controllers, and model.</span></span> <span data-ttu-id="fecd3-234">Ayrıca aracılığıyla oluşturulan bir veritabanı geçiş içerir *alembic* (`flask db migrate`).</span><span class="sxs-lookup"><span data-stu-id="fecd3-234">It also includes a database migration generated via *alembic* (`flask db migrate`).</span></span> <span data-ttu-id="fecd3-235">Aşağıdaki git komutu yapılan tüm değişiklikleri görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fecd3-235">You can see all changes made via the following git command:</span></span>

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="fecd3-236">Yaptığınız değişiklikler yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="fecd3-236">Test your changes locally</span></span>

<span data-ttu-id="fecd3-237">Değişikliklerinizi flask sunucunun yerel olarak çalıştırarak test etmek için aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fecd3-237">Run the following commands to test your changes locally by running the flask server.</span></span>

<span data-ttu-id="fecd3-238">Mac / Linux:</span><span class="sxs-lookup"><span data-stu-id="fecd3-238">Mac / Linux:</span></span>
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="fecd3-239">Değişiklikleri görmek için tarayıcınızda http://127.0.0.1:5000 gidin.</span><span class="sxs-lookup"><span data-stu-id="fecd3-239">Navigate to http://127.0.0.1:5000 in your browser to view the changes.</span></span> <span data-ttu-id="fecd3-240">Bir test kaydı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fecd3-240">Create a test registration.</span></span>

![Docker kapsayıcısı tabanlı Python Flask uygulama yerel olarak çalıştırma](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-to-azure"></a><span data-ttu-id="fecd3-242">Değişiklikler için Azure yayımlama</span><span class="sxs-lookup"><span data-stu-id="fecd3-242">Publish changes to Azure</span></span>

<span data-ttu-id="fecd3-243">Yeni docker görüntüsünü oluşturabilirsiniz, kapsayıcı kayıt defterine gönderme ve uygulamayı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="fecd3-243">Build the new docker image, push it to the container registry, and restart the app.</span></span>

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

<span data-ttu-id="fecd3-244">Azure web uygulamasına gidin ve yeni işlevselliği yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="fecd3-244">Navigate to your Azure web app and try out the new functionality again.</span></span> <span data-ttu-id="fecd3-245">Başka bir olay kaydı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fecd3-245">Create another event registration.</span></span>

```bash 
http://<app_name>.azurewebsites.net 
```

![Docker Python Flask uygulamada Azure uygulama hizmeti](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="fecd3-247">Azure web uygulamanızı yönetme</span><span class="sxs-lookup"><span data-stu-id="fecd3-247">Manage your Azure web app</span></span>

<span data-ttu-id="fecd3-248">Git [Azure portal](https://portal.azure.com) oluşturduğunuz web uygulaması görmek için.</span><span class="sxs-lookup"><span data-stu-id="fecd3-248">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span>

<span data-ttu-id="fecd3-249">Sol menüden **Uygulama Hizmetleri**’ne ve ardından Azure web uygulamanızın adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fecd3-249">From the left menu, click **App Services**, then click the name of your Azure web app.</span></span>

![Portaldan Azure web uygulamasına gitme](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

<span data-ttu-id="fecd3-251">Varsayılan olarak, portal, web uygulamanızın gösterir **genel bakış** sayfası.</span><span class="sxs-lookup"><span data-stu-id="fecd3-251">By default, the portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="fecd3-252">Bu sayfa, uygulamanızın nasıl çalıştığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="fecd3-252">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="fecd3-253">Buradan ayrıca göz atma, durdurma, başlatma, yeniden başlatma ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fecd3-253">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="fecd3-254">Sayfanın sol tarafında sekmeleri açabilir farklı yapılandırma sayfalarında gösterilir.</span><span class="sxs-lookup"><span data-stu-id="fecd3-254">The tabs on the left side of the page show the different configuration pages you can open.</span></span>

![Azure portalında App Service sayfası](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a><span data-ttu-id="fecd3-256">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fecd3-256">Next steps</span></span>

<span data-ttu-id="fecd3-257">Web uygulamanıza özel bir DNS adı eşleme öğrenmek için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="fecd3-257">Advance to the next tutorial to learn how to map a custom DNS name to your web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="fecd3-258">Mevcut bir özel DNS adını Azure Web Apps ile eşleme</span><span class="sxs-lookup"><span data-stu-id="fecd3-258">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
