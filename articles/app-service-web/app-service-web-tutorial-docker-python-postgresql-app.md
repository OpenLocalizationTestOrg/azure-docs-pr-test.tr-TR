---
title: "aaaBuild azure'da Docker Python ve PostgreSQL bir web uygulaması | Microsoft Docs"
description: "Bilgi nasıl tooget Docker Python uygulaması Azure'da çalışan, bağlantı tooa PostgreSQL veritabanı."
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
ms.openlocfilehash: e594ef9ec8c04ef2bf725e5f998691f3fb8cf815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a><span data-ttu-id="a2e80-103">Azure'da Docker Python ve PostgreSQL bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="a2e80-103">Build a Docker Python and PostgreSQL web app in Azure</span></span>

<span data-ttu-id="a2e80-104">Azure Web Apps düzeyde ölçeklenebilir, otomatik olarak düzeltme eki uygulama web barındırma hizmeti sağlar.</span><span class="sxs-lookup"><span data-stu-id="a2e80-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="a2e80-105">Bu öğretici nasıl toocreate temel Docker Python web uygulaması Azure gösterir.</span><span class="sxs-lookup"><span data-stu-id="a2e80-105">This tutorial shows how toocreate a basic Docker Python web app in Azure.</span></span> <span data-ttu-id="a2e80-106">Bu uygulama tooa PostgreSQL veritabanına bağlanırsınız.</span><span class="sxs-lookup"><span data-stu-id="a2e80-106">You'll connect this app tooa PostgreSQL database.</span></span> <span data-ttu-id="a2e80-107">İşiniz bittiğinde, Docker kapsayıcısı içinde çalışan bir Python Flask uygulaması gerekir [Azure App Service Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a2e80-107">When you're done, you'll have a Python Flask application running within a Docker container on [Azure App Service Web Apps](app-service-web-overview.md).</span></span>

![Docker Python Flask uygulamada Azure uygulama hizmeti](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

<span data-ttu-id="a2e80-109">MacOS üzerinde hello adımları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2e80-109">You can follow hello steps below on macOS.</span></span> <span data-ttu-id="a2e80-110">Linux ve Windows'da aynı hello çoğu durumda, ancak bu öğreticide hello farklar ayrıntılı değil yönergelerdir.</span><span class="sxs-lookup"><span data-stu-id="a2e80-110">Linux and Windows instructions are hello same in most cases, but hello differences are not detailed in this tutorial.</span></span>
 
## <a name="prerequisites"></a><span data-ttu-id="a2e80-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a2e80-111">Prerequisites</span></span>

<span data-ttu-id="a2e80-112">toocomplete Bu öğretici:</span><span class="sxs-lookup"><span data-stu-id="a2e80-112">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="a2e80-113">Git'i yükleyin</span><span class="sxs-lookup"><span data-stu-id="a2e80-113">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="a2e80-114">Python'ı yükleyin</span><span class="sxs-lookup"><span data-stu-id="a2e80-114">Install Python</span></span>](https://www.python.org/downloads/)
1. [<span data-ttu-id="a2e80-115">Yükleme ve PostgreSQL çalıştırma</span><span class="sxs-lookup"><span data-stu-id="a2e80-115">Install and run PostgreSQL</span></span>](https://www.postgresql.org/download/)
1. [<span data-ttu-id="a2e80-116">Docker Community Edition'ı yükleme</span><span class="sxs-lookup"><span data-stu-id="a2e80-116">Install Docker Community Edition</span></span>](https://www.docker.com/community-edition)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a2e80-117">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a2e80-117">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a2e80-118">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="a2e80-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a2e80-119">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a2e80-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-postgresql-installation-and-create-a-database"></a><span data-ttu-id="a2e80-120">Yerel PostgreSQL yüklemeyi sınamak ve bir veritabanı oluştur</span><span class="sxs-lookup"><span data-stu-id="a2e80-120">Test local PostgreSQL installation and create a database</span></span>

<span data-ttu-id="a2e80-121">Merhaba terminal penceresi açın ve çalıştırın `psql postgres` tooconnect tooyour yerel PostgreSQL sunucu.</span><span class="sxs-lookup"><span data-stu-id="a2e80-121">Open hello terminal window and run `psql postgres` tooconnect tooyour local PostgreSQL server.</span></span>

```bash
psql postgres
```

<span data-ttu-id="a2e80-122">Bağlantı başarılı olursa, PostgreSQL veritabanınız çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="a2e80-122">If your connection is successful, your PostgreSQL database is running.</span></span> <span data-ttu-id="a2e80-123">Aksi takdirde, yerel PostgresQL veritabanınızı hello adımları izleyerek başlatıldığından emin olun [yüklemeleri - PostgreSQL çekirdek dağıtım](https://www.postgresql.org/download/).</span><span class="sxs-lookup"><span data-stu-id="a2e80-123">If not, make sure that your local PostgresQL database is started by following hello steps at [Downloads - PostgreSQL Core Distribution](https://www.postgresql.org/download/).</span></span>

<span data-ttu-id="a2e80-124">Adlı bir veritabanı oluşturmak *eventregistration* ve adlı bir ayrı veritabanı kullanıcı ayarlama *Yöneticisi* parolayla *supersecretpass*.</span><span class="sxs-lookup"><span data-stu-id="a2e80-124">Create a database called *eventregistration* and set up a separate database user named *manager* with password *supersecretpass*.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```
<span data-ttu-id="a2e80-125">Tür *\q* tooexit hello PostgreSQL istemci.</span><span class="sxs-lookup"><span data-stu-id="a2e80-125">Type *\q* tooexit hello PostgreSQL client.</span></span> 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a><span data-ttu-id="a2e80-126">Yerel Python Flask uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="a2e80-126">Create local Python Flask application</span></span>

<span data-ttu-id="a2e80-127">Bu adımda, hello yerel Python Flask projesi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a2e80-127">In this step, you set up hello local Python Flask project.</span></span>

### <a name="clone-hello-sample-application"></a><span data-ttu-id="a2e80-128">Merhaba örnek uygulaması kopyalama</span><span class="sxs-lookup"><span data-stu-id="a2e80-128">Clone hello sample application</span></span>

<span data-ttu-id="a2e80-129">Açık hello terminal penceresi ve `CD` tooa çalışma dizini.</span><span class="sxs-lookup"><span data-stu-id="a2e80-129">Open hello terminal window, and `CD` tooa working directory.</span></span>  

<span data-ttu-id="a2e80-130">Çalışma hello aşağıdaki komutları tooclone hello örnek depo ve Git toohello *0,1 initialapp* serbest bırakın.</span><span class="sxs-lookup"><span data-stu-id="a2e80-130">Run hello following commands tooclone hello sample repository and go toohello *0.1-initialapp* release.</span></span>

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

<span data-ttu-id="a2e80-131">Bu örnek depo içeren bir [Flask](http://flask.pocoo.org/) uygulama.</span><span class="sxs-lookup"><span data-stu-id="a2e80-131">This sample repository contains a [Flask](http://flask.pocoo.org/) application.</span></span> 

### <a name="run-hello-application"></a><span data-ttu-id="a2e80-132">Merhaba uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="a2e80-132">Run hello application</span></span>

> [!NOTE] 
> <span data-ttu-id="a2e80-133">Bir sonraki adımda Docker kapsayıcısı toouse hello üretim veritabanıyla oluşturarak bu işlemi basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="a2e80-133">In a later step you simplify this process by building a Docker container toouse with hello production database.</span></span>

<span data-ttu-id="a2e80-134">Merhaba gerekli paketleri yüklemek ve hello uygulamasını başlatın.</span><span class="sxs-lookup"><span data-stu-id="a2e80-134">Install hello required packages and start hello application.</span></span>

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="a2e80-135">Merhaba uygulama tam olarak yüklendiğinde iletiden benzeri toohello bakın:</span><span class="sxs-lookup"><span data-stu-id="a2e80-135">When hello app is fully loaded, you see something similar toohello following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="a2e80-136">Bir tarayıcıda toohttp://127.0.0.1:5000 gidin.</span><span class="sxs-lookup"><span data-stu-id="a2e80-136">Navigate toohttp://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="a2e80-137">Tıklatın **kaydedin!**</span><span class="sxs-lookup"><span data-stu-id="a2e80-137">Click **Register!**</span></span> <span data-ttu-id="a2e80-138">ve bir test kullanıcısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a2e80-138">and create a test user.</span></span>

![Yerel olarak çalışan Python Flask uygulama](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

<span data-ttu-id="a2e80-140">Merhaba Flask örnek uygulamanın kullanıcı verilerini hello veritabanında depolar.</span><span class="sxs-lookup"><span data-stu-id="a2e80-140">hello Flask sample application stores user data in hello database.</span></span> <span data-ttu-id="a2e80-141">Bir kullanıcı kaydetme sırasında başarılı olursa, uygulamanızın veri toohello yerel PostgreSQL veritabanına yazma.</span><span class="sxs-lookup"><span data-stu-id="a2e80-141">If you are successful at registering a user, your app is writing data toohello local PostgreSQL database.</span></span>

<span data-ttu-id="a2e80-142">toostop hello Flask sunucuda dilediğiniz zaman, Ctrl + C hello terminal yazın.</span><span class="sxs-lookup"><span data-stu-id="a2e80-142">toostop hello Flask server at anytime, type Ctrl+C in hello terminal.</span></span> 

## <a name="create-a-production-postgresql-database"></a><span data-ttu-id="a2e80-143">Bir üretim PostgreSQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a2e80-143">Create a production PostgreSQL database</span></span>

<span data-ttu-id="a2e80-144">Bu adımda, Azure PostgreSQL veritabanında oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a2e80-144">In this step, you create a PostgreSQL database in Azure.</span></span> <span data-ttu-id="a2e80-145">Uygulamanızı dağıtılan tooAzure olduğunda, bu bulut veritabanı kullanır.</span><span class="sxs-lookup"><span data-stu-id="a2e80-145">When your app is deployed tooAzure, it will use this cloud database.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="a2e80-146">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="a2e80-146">Log in tooAzure</span></span>

<span data-ttu-id="a2e80-147">Devam eden toouse hello Azure CLI 2.0 toocreate hello kaynakları toohost Python uygulamanızı Azure App Service'te gerekli artık size aittir.</span><span class="sxs-lookup"><span data-stu-id="a2e80-147">You are now going toouse hello Azure CLI 2.0 toocreate hello resources needed toohost your Python application in Azure App Service.</span></span>  <span data-ttu-id="a2e80-148">Tooyour hello Azure aboneliğiyle oturum [az oturum açma](/cli/azure/#login) komut ve hello ekrandaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="a2e80-148">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="a2e80-149">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="a2e80-149">Create a resource group</span></span>

<span data-ttu-id="a2e80-150">Oluşturma bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md) hello ile [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="a2e80-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create).</span></span> 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="a2e80-151">Merhaba aşağıdaki örnekte bir kaynak grubu hello Batı ABD bölgesi oluşturur:</span><span class="sxs-lookup"><span data-stu-id="a2e80-151">hello following example creates a resource group in hello West US region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

<span data-ttu-id="a2e80-152">Kullanım hello [az appservice listesi-konumları](/cli/azure/appservice#list-locations) Azure CLI toolist kullanılabilir konumlarını komutu.</span><span class="sxs-lookup"><span data-stu-id="a2e80-152">Use hello [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command toolist available locations.</span></span>

### <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="a2e80-153">PostgreSQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="a2e80-153">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="a2e80-154">Bir PostgreSQL sunucusu ile Merhaba oluşturmak [az postgres sunucusu oluşturmak](/cli/azure/documentdb#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="a2e80-154">Create a PostgreSQL server with hello [az postgres server create](/cli/azure/documentdb#create) command.</span></span>

<span data-ttu-id="a2e80-155">Hello hello için bir benzersiz sunucu adı yerine komutu, aşağıdaki  *\<postgresql_name >* yer tutucu ve hello için bir kullanıcı adı  *\<admin_username >* yer tutucusu .</span><span class="sxs-lookup"><span data-stu-id="a2e80-155">In hello following command, substitute a unique server name for hello *\<postgresql_name>* placeholder and a user name for hello *\<admin_username>* placeholder.</span></span> <span data-ttu-id="a2e80-156">Merhaba sunucu adı, PostgreSQL uç noktanızı bir parçası olarak kullanılır (`https://<postgresql_name>.postgres.database.azure.com`), hello adı toobe benzersiz Azure içindeki tüm sunucular arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a2e80-156">hello server name is used as part of your PostgreSQL endpoint (`https://<postgresql_name>.postgres.database.azure.com`), so hello name needs toobe unique across all servers in Azure.</span></span> <span data-ttu-id="a2e80-157">Merhaba ilk veritabanı yönetici kullanıcı hesabı Hello kullanıcı adıdır.</span><span class="sxs-lookup"><span data-stu-id="a2e80-157">hello user name is for hello initial database admin user account.</span></span> <span data-ttu-id="a2e80-158">Bu kullanıcı için bir parola istendiğinde toopick var.</span><span class="sxs-lookup"><span data-stu-id="a2e80-158">You are prompted toopick a password for this user.</span></span>

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

<span data-ttu-id="a2e80-159">Hello Azure veritabanı PostgreSQL sunucusu oluşturulduğunda, hello Azure CLI aşağıdaki örneğine benzer toohello bilgileri gösterir:</span><span class="sxs-lookup"><span data-stu-id="a2e80-159">When hello Azure Database for PostgreSQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="create-a-firewall-rule-for-hello-azure-database-for-postgresql-server"></a><span data-ttu-id="a2e80-160">Hello Azure veritabanı PostgreSQL sunucusu için bir güvenlik duvarı kuralı oluşturun</span><span class="sxs-lookup"><span data-stu-id="a2e80-160">Create a firewall rule for hello Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="a2e80-161">Tüm IP adreslerinden Azure CLI komut tooallow erişim toohello veritabanı aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a2e80-161">Run hello following Azure CLI command tooallow access toohello database from all IP addresses.</span></span>

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

<span data-ttu-id="a2e80-162">Hello Azure CLI hello güvenlik duvarı kuralı oluşturma çıkış benzer toohello aşağıdaki örneğine ile onaylar:</span><span class="sxs-lookup"><span data-stu-id="a2e80-162">hello Azure CLI confirms hello firewall rule creation with output similar toohello following example:</span></span>

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

## <a name="connect-your-python-flask-application-toohello-database"></a><span data-ttu-id="a2e80-163">Python Flask uygulama toohello veritabanınız Bağlan</span><span class="sxs-lookup"><span data-stu-id="a2e80-163">Connect your Python Flask application toohello database</span></span>

<span data-ttu-id="a2e80-164">Bu adımda oluşturduğunuz PostgreSQL sunucu, Python Flask örnek uygulama toohello Azure veritabanı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="a2e80-164">In this step, you connect your Python Flask sample application toohello Azure Database for PostgreSQL server you created.</span></span>

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a><span data-ttu-id="a2e80-165">Boş bir veritabanı oluşturun ve yeni bir veritabanı uygulama kullanıcı ayarlama</span><span class="sxs-lookup"><span data-stu-id="a2e80-165">Create an empty database and set up a new database application user</span></span>

<span data-ttu-id="a2e80-166">Bir veritabanı kullanıcısı tooa tek yalnızca access veritabanı ile oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a2e80-166">Create a database user with access tooa single database only.</span></span> <span data-ttu-id="a2e80-167">Merhaba uygulama tam erişim toohello sunucusu vererek bu kimlik bilgileri tooavoid kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="a2e80-167">You'll use these credentials tooavoid giving hello application full access toohello server.</span></span>

<span data-ttu-id="a2e80-168">(Yönetici parolanızı girmeniz istenir) toohello veritabanına bağlanın.</span><span class="sxs-lookup"><span data-stu-id="a2e80-168">Connect toohello database (you're prompted for your admin password).</span></span>

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

<span data-ttu-id="a2e80-169">Merhaba veritabanı ve kullanıcı PostgreSQL CLI hello oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a2e80-169">Create hello database and user from hello PostgreSQL CLI.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```

<span data-ttu-id="a2e80-170">Tür *\q* tooexit hello PostgreSQL istemci.</span><span class="sxs-lookup"><span data-stu-id="a2e80-170">Type *\q* tooexit hello PostgreSQL client.</span></span>

### <a name="test-hello-application-locally-against-hello-azure-postgresql-database"></a><span data-ttu-id="a2e80-171">Merhaba uygulamayı yerel olarak hello Azure PostgreSQL veritabanına karşı test etme</span><span class="sxs-lookup"><span data-stu-id="a2e80-171">Test hello application locally against hello Azure PostgreSQL database</span></span> 

<span data-ttu-id="a2e80-172">Şimdi toohello geri dönerseniz *uygulama* hello klasörünü klonlanmış Github deposunu, hello veritabanı ortam değişkenleri güncelleştirerek hello Python Flask uygulamayı çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2e80-172">Going back now toohello *app* folder of hello cloned Github repository, you can run hello Python Flask application by updating hello database environment variables.</span></span>

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="a2e80-173">Merhaba uygulama tam olarak yüklendiğinde iletiden benzeri toohello bakın:</span><span class="sxs-lookup"><span data-stu-id="a2e80-173">When hello app is fully loaded, you see something similar toohello following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="a2e80-174">Bir tarayıcıda toohttp://127.0.0.1:5000 gidin.</span><span class="sxs-lookup"><span data-stu-id="a2e80-174">Navigate toohttp://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="a2e80-175">Tıklatın **kaydedin!**</span><span class="sxs-lookup"><span data-stu-id="a2e80-175">Click **Register!**</span></span> <span data-ttu-id="a2e80-176">ve bir test kaydı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a2e80-176">and create a test registration.</span></span> <span data-ttu-id="a2e80-177">Şimdi, Azure'da verileri toohello veritabanı yazıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="a2e80-177">You are now writing data toohello database in Azure.</span></span>

![Yerel olarak çalışan Python Flask uygulama](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-hello-application-from-a-docker-container"></a><span data-ttu-id="a2e80-179">Docker kapsayıcısı çalışan hello uygulamadan</span><span class="sxs-lookup"><span data-stu-id="a2e80-179">Running hello application from a Docker Container</span></span>

<span data-ttu-id="a2e80-180">Merhaba Docker kapsayıcısı görüntüsünü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2e80-180">Build hello Docker container image.</span></span>

```bash
cd ..
docker build -t flask-postgresql-sample .
```

<span data-ttu-id="a2e80-181">Docker bu başarıyla oluşturuldu BT hello kapsayıcı bir onay görüntüler.</span><span class="sxs-lookup"><span data-stu-id="a2e80-181">Docker displays a confirmation that it successfully created hello container.</span></span>

```bash
Successfully built 7548f983a36b
```

<span data-ttu-id="a2e80-182">Veritabanı ortam değişkenleri tooan ortam değişken dosyası ekleme *db.env*.</span><span class="sxs-lookup"><span data-stu-id="a2e80-182">Add database environment variables tooan environment variable file *db.env*.</span></span> <span data-ttu-id="a2e80-183">Merhaba uygulama toohello PostgreSQL üretim Azure veritabanında bağlanır.</span><span class="sxs-lookup"><span data-stu-id="a2e80-183">hello app will connect toohello PostgreSQL production database in Azure.</span></span>

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

<span data-ttu-id="a2e80-184">Merhaba uygulama hello Docker kapsayıcısı içinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a2e80-184">Run hello app from within hello Docker container.</span></span> <span data-ttu-id="a2e80-185">Merhaba aşağıdaki komutu hello ortam değişken dosyası belirtir ve hello varsayılan Flask bağlantı noktası 5000 toolocal bağlantı noktası 5000 eşler.</span><span class="sxs-lookup"><span data-stu-id="a2e80-185">hello following command specifies hello environment variable file and maps hello default Flask port 5000 toolocal port 5000.</span></span>

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

<span data-ttu-id="a2e80-186">Merhaba çıktı, daha önce gördüğünüzle benzer toowhat şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="a2e80-186">hello output is similar toowhat you saw earlier.</span></span> <span data-ttu-id="a2e80-187">Ancak, hello ilk veritabanı geçiş artık gerçekleştirilen toobe gerekir ve bu nedenle atlanır.</span><span class="sxs-lookup"><span data-stu-id="a2e80-187">However, hello initial database migration no longer needs toobe performed and therefore is skipped.</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="a2e80-188">daha önce oluşturduğunuz hello kayıt Hello veritabanı zaten var.</span><span class="sxs-lookup"><span data-stu-id="a2e80-188">hello database already contains hello registration you created previously.</span></span>

![Docker kapsayıcısı tabanlı Python Flask uygulama yerel olarak çalıştırma](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-hello-docker-container-tooa-container-registry"></a><span data-ttu-id="a2e80-190">Merhaba Docker kapsayıcısı tooa kapsayıcı kayıt defteri karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="a2e80-190">Upload hello Docker container tooa container registry</span></span>

<span data-ttu-id="a2e80-191">Bu adımda, hello Docker kapsayıcısı tooa kapsayıcı kayıt defteri karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a2e80-191">In this step, you upload hello Docker container tooa container registry.</span></span> <span data-ttu-id="a2e80-192">Azure kapsayıcı kayıt defteri kullanırsınız, ancak Docker Hub gibi diğer popüler olanlar da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2e80-192">You'll use Azure Container Registry, but you could also use other popular ones such as Docker Hub.</span></span>

### <a name="create-an-azure-container-registry"></a><span data-ttu-id="a2e80-193">Azure Container Registry oluşturma</span><span class="sxs-lookup"><span data-stu-id="a2e80-193">Create an Azure Container Registry</span></span>

<span data-ttu-id="a2e80-194">Komut toocreate bir kapsayıcı kayıt defteri aşağıdaki hello yerine  *\<registry_name >* tercih ettiğiniz bir benzersiz Azure kapsayıcı kayıt defteri adı.</span><span class="sxs-lookup"><span data-stu-id="a2e80-194">In hello following command toocreate a container registry replace *\<registry_name>* with a unique Azure container registry name of your choice.</span></span>

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

<span data-ttu-id="a2e80-195">Çıktı</span><span class="sxs-lookup"><span data-stu-id="a2e80-195">Output</span></span>
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

### <a name="retrieve-hello-registry-credentials-for-pushing-and-pulling-docker-images"></a><span data-ttu-id="a2e80-196">Docker görüntüleri çekme ve itme hello kayıt defteri kimlik bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="a2e80-196">Retrieve hello registry credentials for pushing and pulling Docker images</span></span>

<span data-ttu-id="a2e80-197">tooshow kayıt defteri kimlik bilgileri, Yönetici modu ilk etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a2e80-197">tooshow registry credentials, enable admin mode first.</span></span>

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

<span data-ttu-id="a2e80-198">İki parola bakın.</span><span class="sxs-lookup"><span data-stu-id="a2e80-198">You see two passwords.</span></span> <span data-ttu-id="a2e80-199">Merhaba kullanıcı adı ve hello ilk parola not edin.</span><span class="sxs-lookup"><span data-stu-id="a2e80-199">Make note of hello user name and hello first password.</span></span>

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

### <a name="upload-your-docker-container-tooazure-container-registry"></a><span data-ttu-id="a2e80-200">Docker kapsayıcısı tooAzure kapsayıcı kayıt defteri karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="a2e80-200">Upload your Docker container tooAzure Container Registry</span></span>

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-hello-docker-python-flask-application-tooazure"></a><span data-ttu-id="a2e80-201">Merhaba Docker Python Flask uygulama tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="a2e80-201">Deploy hello Docker Python Flask application tooAzure</span></span>

<span data-ttu-id="a2e80-202">Bu adımda, Docker kapsayıcısı tabanlı Python Flask uygulama tooAzure uygulama hizmeti dağıtın.</span><span class="sxs-lookup"><span data-stu-id="a2e80-202">In this step, you deploy your Docker container-based Python Flask application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="a2e80-203">App Service planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a2e80-203">Create an App Service plan</span></span>

<span data-ttu-id="a2e80-204">Merhaba ile bir uygulama hizmeti planı oluştur [az uygulama hizmeti planı oluşturma](/cli/azure/appservice/plan#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="a2e80-204">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="a2e80-205">Merhaba aşağıdaki örnekte oluşturur adlı bir Linux tabanlı uygulama hizmeti planı *myAppServicePlan* fiyatlandırma katmanı hello S1 kullanarak:</span><span class="sxs-lookup"><span data-stu-id="a2e80-205">hello following example creates a Linux-based App Service plan named *myAppServicePlan* using hello S1 pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

<span data-ttu-id="a2e80-206">Uygulama hizmeti planı Hello oluşturulduğunda, hello Azure CLI bilgi benzer toohello aşağıdaki örneğine gösterir:</span><span class="sxs-lookup"><span data-stu-id="a2e80-206">When hello App Service plan is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="create-a-web-app"></a><span data-ttu-id="a2e80-207">Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="a2e80-207">Create a web app</span></span>

<span data-ttu-id="a2e80-208">Hello bir web uygulaması oluşturma *myAppServicePlan* hello ile uygulama hizmeti planı [az webapp oluşturmak](/cli/azure/webapp#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="a2e80-208">Create a web app in hello *myAppServicePlan* App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="a2e80-209">dağıtılan uygulama, bir barındırma kodunuzu toodeploy boşluk ve sizin için bir URL tooview hello sağlar hello web uygulamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="a2e80-209">hello web app gives you a hosting space toodeploy your code and provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="a2e80-210">Toocreate hello web uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="a2e80-210">Use  toocreate hello web app.</span></span> 

<span data-ttu-id="a2e80-211">Hello hello Değiştir komutu, aşağıdaki  *\<app_name >* yer tutucu benzersiz bir uygulama adına sahip.</span><span class="sxs-lookup"><span data-stu-id="a2e80-211">In hello following command, replace hello *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="a2e80-212">Merhaba adının toobe benzersiz Azure App Service'te tüm uygulamalarında gerekir böylece bu adı hello varsayılan URL hello web uygulaması için bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="a2e80-212">This name is part of hello default URL for hello web app, so hello name needs toobe unique across all apps in Azure App Service.</span></span> 

```azurecli
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="a2e80-213">Merhaba web uygulaması oluşturduğunuzda aşağıdaki örneğine bilgi benzer toohello hello Azure CLI gösterir:</span><span class="sxs-lookup"><span data-stu-id="a2e80-213">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-hello-database-environment-variables"></a><span data-ttu-id="a2e80-214">Merhaba veritabanı ortam değişkenlerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="a2e80-214">Configure hello database environment variables</span></span>

<span data-ttu-id="a2e80-215">Öğreticide daha önce Merhaba, ortam değişkenleri tooconnect tooyour PostgreSQL veritabanında tanımlı.</span><span class="sxs-lookup"><span data-stu-id="a2e80-215">Earlier in hello tutorial, you defined environment variables tooconnect tooyour PostgreSQL database.</span></span>

<span data-ttu-id="a2e80-216">Ortam değişkenleri olarak ayarladığınız App Service'te _uygulama ayarları_ hello kullanarak [az webapp config appsettings kümesi](/cli/azure/webapp/config#set) komutu.</span><span class="sxs-lookup"><span data-stu-id="a2e80-216">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings set](/cli/azure/webapp/config#set) command.</span></span> 

<span data-ttu-id="a2e80-217">Merhaba aşağıdaki örnek hello veritabanı bağlantı ayrıntıları uygulama ayarlarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a2e80-217">hello following example specifies hello database connection details as app settings.</span></span> <span data-ttu-id="a2e80-218">Ayrıca hello kullanır *bağlantı noktası* değişken toomap bağlantı noktası 5000 bağlantı noktası 80 üzerinde Docker kapsayıcısı tooreceive HTTP trafiğinden.</span><span class="sxs-lookup"><span data-stu-id="a2e80-218">It also uses hello *PORT* variable toomap PORT 5000 from your Docker Container tooreceive HTTP traffic on PORT 80.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a><span data-ttu-id="a2e80-219">Docker kapsayıcısı dağıtımını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a2e80-219">Configure Docker container deployment</span></span> 

<span data-ttu-id="a2e80-220">Uygulama hizmeti otomatik olarak karşıdan yükle ve Docker kapsayıcısı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a2e80-220">AppService can automatically download and run a Docker container.</span></span>

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

<span data-ttu-id="a2e80-221">Her hello Docker kapsayıcısı güncelleştirmek veya hello ayarlarını değiştirme hello uygulamayı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="a2e80-221">Whenever you update hello Docker container or change hello settings, restart hello app.</span></span> <span data-ttu-id="a2e80-222">Yeniden başlatma, tüm ayarları uygulanır ve hello son kapsayıcı hello kayıt defterinden çekilir sağlar.</span><span class="sxs-lookup"><span data-stu-id="a2e80-222">Restarting ensures that all settings are applied and hello latest container is pulled from hello registry.</span></span>

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="a2e80-223">Toohello Azure web uygulaması Gözat</span><span class="sxs-lookup"><span data-stu-id="a2e80-223">Browse toohello Azure web app</span></span> 

<span data-ttu-id="a2e80-224">Web tarayıcınız üzerinden dağıtılan toohello web uygulaması göz atın.</span><span class="sxs-lookup"><span data-stu-id="a2e80-224">Browse toohello deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> <span data-ttu-id="a2e80-225">Merhaba kapsayıcı indirilir ve hello kapsayıcısı yapılandırmasını değiştirildikten sonra başlatıldı toobe olduğundan hello web uygulaması uzun tooload alır.</span><span class="sxs-lookup"><span data-stu-id="a2e80-225">hello web app takes longer tooload because hello container has toobe downloaded and started after hello container configuration is changed.</span></span>

<span data-ttu-id="a2e80-226">Toohello Azure üretim veritabanını hello önceki adımda kaydedilen önceden kaydedilmiş konuklar bakın.</span><span class="sxs-lookup"><span data-stu-id="a2e80-226">You see previously registered guests that were saved toohello Azure production database in hello previous step.</span></span>

![Docker kapsayıcısı tabanlı Python Flask uygulama yerel olarak çalıştırma](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

<span data-ttu-id="a2e80-228">**Tebrikler!**</span><span class="sxs-lookup"><span data-stu-id="a2e80-228">**Congratulations!**</span></span> <span data-ttu-id="a2e80-229">Azure App Service'te bir Docker kapsayıcısı tabanlı bir Python Flask uygulamanın çalıştırdığınız.</span><span class="sxs-lookup"><span data-stu-id="a2e80-229">You're running a Docker container-based Python Flask app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="a2e80-230">Güncelleştirme veri modeli ve yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="a2e80-230">Update data model and redeploy</span></span>

<span data-ttu-id="a2e80-231">Bu adımda, hello Konuk modeli güncelleştirerek hello sayıda katılımcı tooeach olay kaydı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a2e80-231">In this step, you add hello number of attendees tooeach event registration by updating hello Guest model.</span></span>

<span data-ttu-id="a2e80-232">Merhaba denetleyin *0.2 geçiş* git komut aşağıdaki hello sürümüyle:</span><span class="sxs-lookup"><span data-stu-id="a2e80-232">Check out hello *0.2-migration* release with hello following git command:</span></span>

```bash
git checkout tags/0.2-migration
```

<span data-ttu-id="a2e80-233">Bu sürümü zaten gerekli değişiklikleri tooviews, denetleyicilere ve model hello yaptı.</span><span class="sxs-lookup"><span data-stu-id="a2e80-233">This release already made hello necessary changes tooviews, controllers, and model.</span></span> <span data-ttu-id="a2e80-234">Ayrıca aracılığıyla oluşturulan bir veritabanı geçiş içerir *alembic* (`flask db migrate`).</span><span class="sxs-lookup"><span data-stu-id="a2e80-234">It also includes a database migration generated via *alembic* (`flask db migrate`).</span></span> <span data-ttu-id="a2e80-235">Git komutu aşağıdaki hello yapılan tüm değişiklikleri görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a2e80-235">You can see all changes made via hello following git command:</span></span>

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="a2e80-236">Yaptığınız değişiklikler yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="a2e80-236">Test your changes locally</span></span>

<span data-ttu-id="a2e80-237">Aşağıdaki komutları tootest hello değişikliklerinizi çalışan hello flask sunucu tarafından yerel olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a2e80-237">Run hello following commands tootest your changes locally by running hello flask server.</span></span>

<span data-ttu-id="a2e80-238">Mac / Linux:</span><span class="sxs-lookup"><span data-stu-id="a2e80-238">Mac / Linux:</span></span>
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="a2e80-239">Tarayıcı tooview hello değişikliklerinizi toohttp://127.0.0.1:5000 gidin.</span><span class="sxs-lookup"><span data-stu-id="a2e80-239">Navigate toohttp://127.0.0.1:5000 in your browser tooview hello changes.</span></span> <span data-ttu-id="a2e80-240">Bir test kaydı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a2e80-240">Create a test registration.</span></span>

![Docker kapsayıcısı tabanlı Python Flask uygulama yerel olarak çalıştırma](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-tooazure"></a><span data-ttu-id="a2e80-242">Değişiklikleri tooAzure yayımlama</span><span class="sxs-lookup"><span data-stu-id="a2e80-242">Publish changes tooAzure</span></span>

<span data-ttu-id="a2e80-243">Merhaba yeni docker görüntüsünü oluşturabilirsiniz, toohello kapsayıcı kayıt defteri itme ve hello uygulamayı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="a2e80-243">Build hello new docker image, push it toohello container registry, and restart hello app.</span></span>

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

<span data-ttu-id="a2e80-244">Tooyour Azure web uygulamasına gidin ve hello yeni işlevsellik yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="a2e80-244">Navigate tooyour Azure web app and try out hello new functionality again.</span></span> <span data-ttu-id="a2e80-245">Başka bir olay kaydı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a2e80-245">Create another event registration.</span></span>

```bash 
http://<app_name>.azurewebsites.net 
```

![Docker Python Flask uygulamada Azure uygulama hizmeti](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="a2e80-247">Azure web uygulamanızı yönetme</span><span class="sxs-lookup"><span data-stu-id="a2e80-247">Manage your Azure web app</span></span>

<span data-ttu-id="a2e80-248">Toohello Git [Azure portal](https://portal.azure.com) oluşturduğunuz toosee hello web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a2e80-248">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span>

<span data-ttu-id="a2e80-249">Merhaba sol menüden **uygulama hizmetleri**, Azure web uygulamanızın hello adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a2e80-249">From hello left menu, click **App Services**, then click hello name of your Azure web app.</span></span>

![Portal Gezinti tooAzure web uygulaması](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

<span data-ttu-id="a2e80-251">Varsayılan olarak, web uygulamanızın hello portal gösterir **genel bakış** sayfası.</span><span class="sxs-lookup"><span data-stu-id="a2e80-251">By default, hello portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="a2e80-252">Bu sayfa, uygulamanızın nasıl çalıştığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="a2e80-252">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="a2e80-253">Buradan ayrıca göz atma, durdurma, başlatma, yeniden başlatma ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2e80-253">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="a2e80-254">Merhaba sekmeler hello sayfasının sol tarafında hello açabilirsiniz hello farklı yapılandırma sayfaları gösterir.</span><span class="sxs-lookup"><span data-stu-id="a2e80-254">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span>

![Azure portalında App Service sayfası](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a><span data-ttu-id="a2e80-256">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a2e80-256">Next steps</span></span>

<span data-ttu-id="a2e80-257">İlerlemek toohello sonraki öğretici toolearn nasıl toomap özel DNS ad tooyour web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a2e80-257">Advance toohello next tutorial toolearn how toomap a custom DNS name tooyour web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="a2e80-258">Harita bir var olan özel DNS adı tooAzure Web uygulamaları</span><span class="sxs-lookup"><span data-stu-id="a2e80-258">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
