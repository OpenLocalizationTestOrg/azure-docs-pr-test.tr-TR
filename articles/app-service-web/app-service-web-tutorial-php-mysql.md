---
title: "Azure'da PHP ve MySQL bir web uygulaması oluşturma | Microsoft Docs"
description: "Azure MySQL veritabanında bağlantısı olan Azure üzerinde çalışan bir PHP uygulaması alma hakkında bilgi."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 14feb4f3-5095-496e-9a40-690e1414bd73
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 07/21/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6e8d8962180f7534b0b9074f03ecc8ea431ae1a4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-php-and-mysql-web-app-in-azure"></a><span data-ttu-id="82ea2-103">Azure'da PHP ve MySQL bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="82ea2-103">Build a PHP and MySQL web app in Azure</span></span>

<span data-ttu-id="82ea2-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) yüksek oranda ölçeklenebilen, kendi kendine düzeltme eki uygulayan bir web barındırma hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="82ea2-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="82ea2-105">Bu öğretici, Azure üzerinde bir PHP web uygulaması oluşturma ve MySQL veritabanına bağlanmak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="82ea2-105">This tutorial shows how to create a PHP web app in Azure and connect it to a MySQL database.</span></span> <span data-ttu-id="82ea2-106">İşiniz bittiğinde, gerekir bir [Laravel](https://laravel.com/) Azure App Service Web Apps üzerinde çalışan uygulama.</span><span class="sxs-lookup"><span data-stu-id="82ea2-106">When you're finished, you'll have a [Laravel](https://laravel.com/) app running on Azure App Service Web Apps.</span></span>

![Azure uygulama Hizmeti'nde çalışan PHP uygulaması](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="82ea2-108">Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="82ea2-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="82ea2-109">Azure üzerinde MySQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="82ea2-109">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="82ea2-110">MySQL için PHP uygulamaya Bağlan</span><span class="sxs-lookup"><span data-stu-id="82ea2-110">Connect a PHP app to MySQL</span></span>
> * <span data-ttu-id="82ea2-111">Uygulamayı Azure'a dağıtma</span><span class="sxs-lookup"><span data-stu-id="82ea2-111">Deploy the app to Azure</span></span>
> * <span data-ttu-id="82ea2-112">Veri modeli güncelleştirme ve uygulamayı yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="82ea2-112">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="82ea2-113">Azure Stream tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="82ea2-113">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="82ea2-114">Azure portalında uygulama yönetme</span><span class="sxs-lookup"><span data-stu-id="82ea2-114">Manage the app in the Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82ea2-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="82ea2-115">Prerequisites</span></span>

<span data-ttu-id="82ea2-116">Bu öğreticiyi tamamlamak için:</span><span class="sxs-lookup"><span data-stu-id="82ea2-116">To complete this tutorial:</span></span>

* [<span data-ttu-id="82ea2-117">Git'i yükleyin</span><span class="sxs-lookup"><span data-stu-id="82ea2-117">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="82ea2-118">PHP 5.6.4 yükleme veya üstü</span><span class="sxs-lookup"><span data-stu-id="82ea2-118">Install PHP 5.6.4 or above</span></span>](http://php.net/downloads.php)
* [<span data-ttu-id="82ea2-119">Oluşturucu yükleyin</span><span class="sxs-lookup"><span data-stu-id="82ea2-119">Install Composer</span></span>](https://getcomposer.org/doc/00-intro.md)
* <span data-ttu-id="82ea2-120">Aşağıdaki PHP uzantılarını Laravel gereksinimlerini etkinleştirme: OpenSSL, PDO MySQL, Mbstring, belirteç Oluşturucu, XML</span><span class="sxs-lookup"><span data-stu-id="82ea2-120">Enable the following PHP extensions Laravel needs: OpenSSL, PDO-MySQL, Mbstring, Tokenizer, XML</span></span>
* [<span data-ttu-id="82ea2-121">Yükleyin ve MySQL başlatın</span><span class="sxs-lookup"><span data-stu-id="82ea2-121">Install and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a><span data-ttu-id="82ea2-122">Yerel MySQL hazırlama</span><span class="sxs-lookup"><span data-stu-id="82ea2-122">Prepare local MySQL</span></span>

<span data-ttu-id="82ea2-123">Bu adımda, bir veritabanı yerel MySQL sunucunuzu Bu öğreticide, kullanımınız için oluşturun.</span><span class="sxs-lookup"><span data-stu-id="82ea2-123">In this step, you create a database in your local MySQL server for your use in this tutorial.</span></span>

### <a name="connect-to-local-mysql-server"></a><span data-ttu-id="82ea2-124">Yerel MySQL sunucuya bağlanın</span><span class="sxs-lookup"><span data-stu-id="82ea2-124">Connect to local MySQL server</span></span>

<span data-ttu-id="82ea2-125">Bir terminal penceresi, yerel MySQL sunucusuna bağlanın.</span><span class="sxs-lookup"><span data-stu-id="82ea2-125">In a terminal window, connect to your local MySQL server.</span></span> <span data-ttu-id="82ea2-126">Bu öğreticide tüm komutları çalıştırmak için bu bir terminal penceresi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82ea2-126">You can use this terminal window to run all the commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="82ea2-127">İçin bir parola istenirse parolayı girin `root` hesabı.</span><span class="sxs-lookup"><span data-stu-id="82ea2-127">If you're prompted for a password, enter the password for the `root` account.</span></span> <span data-ttu-id="82ea2-128">Kök hesap parolanızı hatırlamıyorsanız bkz [MySQL: kök parolasını sıfırlamak nasıl](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span><span class="sxs-lookup"><span data-stu-id="82ea2-128">If you don't remember your root account password, see [MySQL: How to Reset the Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="82ea2-129">Komutunuzu başarıyla çalışırsa, MySQL sunucunuzu çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="82ea2-129">If your command runs successfully, then your MySQL server is running.</span></span> <span data-ttu-id="82ea2-130">Aksi takdirde, yerel MySQL server'ınızdaki izleyerek başlatıldığından emin olun [MySQL yükleme sonrası adımları](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="82ea2-130">If not, make sure that your local MySQL server is started by following the [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database-locally"></a><span data-ttu-id="82ea2-131">Yerel bir veritabanı oluşturun</span><span class="sxs-lookup"><span data-stu-id="82ea2-131">Create a database locally</span></span>

<span data-ttu-id="82ea2-132">Konumundaki `mysql` isteminde, bir veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="82ea2-132">At the `mysql` prompt, create a database.</span></span>

```sql 
CREATE DATABASE sampledb;
```

<span data-ttu-id="82ea2-133">Sunucu bağlantısı yazarak çıkmak `quit`.</span><span class="sxs-lookup"><span data-stu-id="82ea2-133">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a><span data-ttu-id="82ea2-134">Yerel olarak bir PHP uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="82ea2-134">Create a PHP app locally</span></span>
<span data-ttu-id="82ea2-135">Bu adımda, Laravel örnek bir uygulama almak, veritabanı bağlantısını yapılandırın ve yerel olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="82ea2-135">In this step, you get a Laravel sample application, configure its database connection, and run it locally.</span></span> 

### <a name="clone-the-sample"></a><span data-ttu-id="82ea2-136">Örnek kopyalama</span><span class="sxs-lookup"><span data-stu-id="82ea2-136">Clone the sample</span></span>

<span data-ttu-id="82ea2-137">Terminal penceresinde `cd` bir çalışma dizini için.</span><span class="sxs-lookup"><span data-stu-id="82ea2-137">In the terminal window, `cd` to a working directory.</span></span>

<span data-ttu-id="82ea2-138">Örnek depoyu kopyalamak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="82ea2-138">Run the following command to clone the sample repository.</span></span>

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

<span data-ttu-id="82ea2-139">`cd`Kopyalanan dizininize.</span><span class="sxs-lookup"><span data-stu-id="82ea2-139">`cd` to your cloned directory.</span></span>
<span data-ttu-id="82ea2-140">Gerekli paketleri yükleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="82ea2-140">Install the required packages.</span></span>

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a><span data-ttu-id="82ea2-141">MySQL bağlantısını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="82ea2-141">Configure MySQL connection</span></span>

<span data-ttu-id="82ea2-142">Depo kök dizininde adlı bir dosya oluşturun *.env*.</span><span class="sxs-lookup"><span data-stu-id="82ea2-142">In the repository root, create a file named *.env*.</span></span> <span data-ttu-id="82ea2-143">Aşağıdaki değişkenler içine kopyalamak *.env* dosya.</span><span class="sxs-lookup"><span data-stu-id="82ea2-143">Copy the following variables into the *.env* file.</span></span> <span data-ttu-id="82ea2-144">Değiştir  _&lt;root_password >_ yer tutucusunu MySQL kök kullanıcının parolası ile.</span><span class="sxs-lookup"><span data-stu-id="82ea2-144">Replace the _&lt;root_password>_ placeholder with the MySQL root user's password.</span></span>

```
APP_ENV=local
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_DATABASE=sampledb
DB_USERNAME=root
DB_PASSWORD=<root_password>
```

<span data-ttu-id="82ea2-145">Laravel nasıl kullandığı hakkında bilgi için _.env_ dosya için bkz: [Laravel ortamı Yapılandırması](https://laravel.com/docs/5.4/configuration#environment-configuration).</span><span class="sxs-lookup"><span data-stu-id="82ea2-145">For information on how Laravel uses the _.env_ file, see [Laravel Environment Configuration](https://laravel.com/docs/5.4/configuration#environment-configuration).</span></span>

### <a name="run-the-sample-locally"></a><span data-ttu-id="82ea2-146">Örnek yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="82ea2-146">Run the sample locally</span></span>

<span data-ttu-id="82ea2-147">Çalıştırma [Laravel veritabanı geçişler](https://laravel.com/docs/5.4/migrations) tabloları uygulama oluşturması gerekir.</span><span class="sxs-lookup"><span data-stu-id="82ea2-147">Run [Laravel database migrations](https://laravel.com/docs/5.4/migrations) to create the tables the application needs.</span></span> <span data-ttu-id="82ea2-148">Hangi tablolar geçişleri oluşturulur görmek için konum _veritabanı/geçişler_ Git deposunda dizin.</span><span class="sxs-lookup"><span data-stu-id="82ea2-148">To see which tables are created in the migrations, look in the _database/migrations_ directory in the Git repository.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="82ea2-149">Yeni bir Laravel uygulama anahtarı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="82ea2-149">Generate a new Laravel application key.</span></span>

```bash
php artisan key:generate
```

<span data-ttu-id="82ea2-150">Uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="82ea2-150">Run the application.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="82ea2-151">Bir tarayıcıda `http://localhost:8000` sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="82ea2-151">Navigate to `http://localhost:8000` in a browser.</span></span> <span data-ttu-id="82ea2-152">Bazı görevler sayfasında ekleyin.</span><span class="sxs-lookup"><span data-stu-id="82ea2-152">Add a few tasks in the page.</span></span>

![MySQL için PHP başarıyla bağlandığını](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="82ea2-154">PHP durdurmak için aşağıdakileri yazın `Ctrl + C` Terminal.</span><span class="sxs-lookup"><span data-stu-id="82ea2-154">To stop PHP, type `Ctrl + C` in the terminal.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a><span data-ttu-id="82ea2-155">MySQL oluşturma</span><span class="sxs-lookup"><span data-stu-id="82ea2-155">Create MySQL in Azure</span></span>

<span data-ttu-id="82ea2-156">Bu adımda oluşturduğunuz MySQL veritabanında [Azure veritabanı için MySQL (Önizleme)](/azure/mysql).</span><span class="sxs-lookup"><span data-stu-id="82ea2-156">In this step, you create a MySQL database in [Azure Database for MySQL (Preview)](/azure/mysql).</span></span> <span data-ttu-id="82ea2-157">Daha sonra bu veritabanına bağlanmak için PHP uygulaması yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="82ea2-157">Later, you configure the PHP application to connect to this database.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="82ea2-158">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="82ea2-158">Create a resource group</span></span>

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a><span data-ttu-id="82ea2-159">MySQL sunucusu oluşturun</span><span class="sxs-lookup"><span data-stu-id="82ea2-159">Create a MySQL server</span></span>

<span data-ttu-id="82ea2-160">MySQL (Önizleme) Azure veritabanındaki bir sunucu oluşturmak [az mysql sunucusu oluşturun](/cli/azure/mysql/server#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="82ea2-160">Create a server in Azure Database for MySQL (Preview) with the [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>

<span data-ttu-id="82ea2-161">Aşağıdaki komutta, gördüğünüz MySQL server adınızı alternatif  _&lt;mysql_server_name >_ yer tutucu (geçerli karakterler `a-z`, `0-9`, ve `-`).</span><span class="sxs-lookup"><span data-stu-id="82ea2-161">In the following command, substitute your MySQL server name where you see the _&lt;mysql_server_name>_ placeholder (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="82ea2-162">Bu ad MySQL sunucunun ana bilgisayar adı bir parçasıdır (`<mysql_server_name>.database.windows.net`), genel olarak benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="82ea2-162">This name is part of the MySQL server's hostname  (`<mysql_server_name>.database.windows.net`), it needs to be globally unique.</span></span>

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

<span data-ttu-id="82ea2-163">MySQL sunucusu oluşturulduğunda, Azure CLI bilgileri aşağıdaki örneğe benzer şekilde gösterir:</span><span class="sxs-lookup"><span data-stu-id="82ea2-163">When the MySQL server is created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "administratorLogin": "adminuser",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "<mysql_server_name>.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/<mysql_server_name>",
  "location": "northeurope",
  "name": "<mysql_server_name>",
  "resourceGroup": "myResourceGroup",
  ...
}
```

### <a name="configure-server-firewall"></a><span data-ttu-id="82ea2-164">Sunucu Güvenlik Duvarı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="82ea2-164">Configure server firewall</span></span>

<span data-ttu-id="82ea2-165">MySQL sunucunuzu kullanarak istemci bağlantılarına izin verecek şekilde için güvenlik duvarı kuralını [az mysql server güvenlik duvarı kuralı oluşturmak](/cli/azure/mysql/server/firewall-rule#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="82ea2-165">Create a firewall rule for your MySQL server to allow client connections by using the [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span>

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="82ea2-166">Azure veritabanı için MySQL (Önizleme) şu anda yalnızca Azure hizmetlerine bağlantı sayısı sınırı değil.</span><span class="sxs-lookup"><span data-stu-id="82ea2-166">Azure Database for MySQL (Preview) doesn't currently limit connections only to Azure services.</span></span> <span data-ttu-id="82ea2-167">Dinamik olarak atanmış IP adresleri azure'da gibi tüm IP adresleri etkinleştirmek daha iyidir.</span><span class="sxs-lookup"><span data-stu-id="82ea2-167">As IP addresses in Azure are dynamically assigned, it is better to enable all IP addresses.</span></span> <span data-ttu-id="82ea2-168">Hizmet önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="82ea2-168">The service is in preview.</span></span> <span data-ttu-id="82ea2-169">Veritabanınızın güvenliğini sağlamak için daha iyi yöntemleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="82ea2-169">Better methods for securing your database are planned.</span></span>
>
>

### <a name="connect-to-production-mysql-server-locally"></a><span data-ttu-id="82ea2-170">Yerel olarak üretim MySQL sunucusuna bağlan</span><span class="sxs-lookup"><span data-stu-id="82ea2-170">Connect to production MySQL server locally</span></span>

<span data-ttu-id="82ea2-171">Terminal penceresinde Azure MySQL sunucusuna bağlanın.</span><span class="sxs-lookup"><span data-stu-id="82ea2-171">In the terminal window, connect to the MySQL server in Azure.</span></span> <span data-ttu-id="82ea2-172">Daha önce için belirttiğiniz değerini kullanmak  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="82ea2-172">Use the value you specified previously for _&lt;mysql_server_name>_.</span></span>

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

<span data-ttu-id="82ea2-173">Kullanmak için bir parola istendiğinde, _tr0ngPa $$ w0rd!_, veritabanı oluşturduğunuzda belirttiğiniz.</span><span class="sxs-lookup"><span data-stu-id="82ea2-173">When prompted for a password, use _$tr0ngPa$w0rd!_, which you specified when you created the database.</span></span>

### <a name="create-a-production-database"></a><span data-ttu-id="82ea2-174">Bir üretim veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="82ea2-174">Create a production database</span></span>

<span data-ttu-id="82ea2-175">Konumundaki `mysql` isteminde, bir veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="82ea2-175">At the `mysql` prompt, create a database.</span></span>

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="82ea2-176">İzinleri olan bir kullanıcı oluşturun</span><span class="sxs-lookup"><span data-stu-id="82ea2-176">Create a user with permissions</span></span>

<span data-ttu-id="82ea2-177">Adlı bir veritabanı kullanıcısı oluşturmalıdır _phpappuser_ ve tüm ayrıcalıkları verin `sampledb` veritabanı.</span><span class="sxs-lookup"><span data-stu-id="82ea2-177">Create a database user called _phpappuser_ and give it all privileges in the `sampledb` database.</span></span>

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* TO 'phpappuser';
```

<span data-ttu-id="82ea2-178">Sunucu bağlantısı yazarak çıkmak `quit`.</span><span class="sxs-lookup"><span data-stu-id="82ea2-178">Exit the server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="connect-app-to-azure-mysql"></a><span data-ttu-id="82ea2-179">Azure MySQL uygulamaya Bağlan</span><span class="sxs-lookup"><span data-stu-id="82ea2-179">Connect app to Azure MySQL</span></span>

<span data-ttu-id="82ea2-180">Bu adımda, PHP uygulaması, Azure veritabanı'nda (Önizleme) MySQL için oluşturduğunuz MySQL veritabanına bağlanın.</span><span class="sxs-lookup"><span data-stu-id="82ea2-180">In this step, you connect the PHP application to the MySQL database you created in Azure Database for MySQL (Preview).</span></span>

<a name="devconfig"></a>

### <a name="configure-the-database-connection"></a><span data-ttu-id="82ea2-181">Veritabanı bağlantısını yapılandır</span><span class="sxs-lookup"><span data-stu-id="82ea2-181">Configure the database connection</span></span>

<span data-ttu-id="82ea2-182">Depo kök dizininde oluşturma bir _. env.production_ dosya ve aşağıdaki değişkenleri buraya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="82ea2-182">In the repository root, create an _.env.production_ file and copy the following variables into it.</span></span> <span data-ttu-id="82ea2-183">Yer tutucu Değiştir  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="82ea2-183">Replace the placeholder _&lt;mysql_server_name>_.</span></span>

```
APP_ENV=production
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=<mysql_server_name>.database.windows.net
DB_DATABASE=sampledb
DB_USERNAME=phpappuser@<mysql_server_name>
DB_PASSWORD=MySQLAzure2017
MYSQL_SSL=true
```

<span data-ttu-id="82ea2-184">Değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="82ea2-184">Save the changes.</span></span>

> [!TIP]
> <span data-ttu-id="82ea2-185">MySQL bağlantı bilgilerinizin güvenliğini sağlamak için bu dosya zaten Git deposundan dışarıda bırakılmış (bkz _.gitignore_ depo kök içinde).</span><span class="sxs-lookup"><span data-stu-id="82ea2-185">To secure your MySQL connection information, this file is already excluded from the Git repository (See _.gitignore_ in the repository root).</span></span> <span data-ttu-id="82ea2-186">Daha sonra MySQL (Önizleme) Azure veritabanı veritabanınızda bağlanmak için App Service'te ortam değişkenleri yapılandırma konusunda bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="82ea2-186">Later, you learn how to configure environment variables in App Service to connect to your database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="82ea2-187">Ortam değişkenleri ile gerekmeyen *.env* uygulama hizmeti dosyasında.</span><span class="sxs-lookup"><span data-stu-id="82ea2-187">With environment variables, you don't need the *.env* file in App Service.</span></span>
>

### <a name="configure-ssl-certificate"></a><span data-ttu-id="82ea2-188">SSL sertifikası yapılandırma</span><span class="sxs-lookup"><span data-stu-id="82ea2-188">Configure SSL certificate</span></span>

<span data-ttu-id="82ea2-189">Varsayılan olarak, Azure veritabanı için MySQL istemcilerden gelen SSL bağlantıları zorlar.</span><span class="sxs-lookup"><span data-stu-id="82ea2-189">By default, Azure Database for MySQL enforces SSL connections from clients.</span></span> <span data-ttu-id="82ea2-190">Azure, MySQL veritabanınızı bağlanmak için kullanmanız gerekir bir _.pem_ SSL sertifikası.</span><span class="sxs-lookup"><span data-stu-id="82ea2-190">To connect to your MySQL database in Azure, you must use a _.pem_ SSL certificate.</span></span>

<span data-ttu-id="82ea2-191">Açık _config/database.php_ ve ekleme _sslmode_ ve _seçenekleri_ parametreleri `connections.mysql`aşağıdaki kodda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="82ea2-191">Open _config/database.php_ and add the _sslmode_ and _options_ parameters to `connections.mysql`, as shown in the following code.</span></span>

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

<span data-ttu-id="82ea2-192">Bu oluşturma konusunda bilgi almak için _certificate.pem_, bkz: [uygulamanızda güvenli bir şekilde MySQL için Azure veritabanına bağlanmak için SSL yapılandırma bağlantısı](../mysql/howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="82ea2-192">To learn how to generate this _certificate.pem_, see [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL](../mysql/howto-configure-ssl.md).</span></span>

> [!TIP]
> <span data-ttu-id="82ea2-193">Yolun _/ssl/certificate.pem_ noktaları var olan _certificate.pem_ Git deposu dosyasında.</span><span class="sxs-lookup"><span data-stu-id="82ea2-193">The path _/ssl/certificate.pem_ points to an existing _certificate.pem_ file in the Git repository.</span></span> <span data-ttu-id="82ea2-194">Bu dosya, bu öğreticide kolaylık sağlaması açısından sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="82ea2-194">This file is provided for convenience in this tutorial.</span></span> <span data-ttu-id="82ea2-195">En iyi yöntem yürüttükten değil, _.pem_ kaynak denetimine sertifikalar.</span><span class="sxs-lookup"><span data-stu-id="82ea2-195">For best practice, you should not commit your _.pem_ certificates into source control.</span></span> 
>

### <a name="test-the-application-locally"></a><span data-ttu-id="82ea2-196">Uygulamayı yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="82ea2-196">Test the application locally</span></span>

<span data-ttu-id="82ea2-197">Laravel veritabanı geçişler ile Çalıştır _. env.production_ MySQL (Önizleme), MySQL veritabanınızı Azure veritabanı tabloları oluşturmak için ortam dosyası olarak.</span><span class="sxs-lookup"><span data-stu-id="82ea2-197">Run Laravel database migrations with _.env.production_ as the environment file to create the tables in your MySQL database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="82ea2-198">Unutmayın _. env.production_ Azure üzerinde MySQL veritabanı için bağlantı bilgilerini içeren.</span><span class="sxs-lookup"><span data-stu-id="82ea2-198">Remember that _.env.production_ has the connection information to your MySQL database in Azure.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="82ea2-199">_. env.production_ geçerli uygulama anahtarı henüz yok.</span><span class="sxs-lookup"><span data-stu-id="82ea2-199">_.env.production_ doesn't have a valid application key yet.</span></span> <span data-ttu-id="82ea2-200">Terminale daha yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="82ea2-200">Generate a new one for it in the terminal.</span></span>

```bash
php artisan key:generate --env=production --force
```

<span data-ttu-id="82ea2-201">Örnek uygulama ile Çalıştır _. env.production_ ortam dosyası olarak.</span><span class="sxs-lookup"><span data-stu-id="82ea2-201">Run the sample application with _.env.production_ as the environment file.</span></span>

```bash
php artisan serve --env=production
```

<span data-ttu-id="82ea2-202">Gidin `http://localhost:8000`.</span><span class="sxs-lookup"><span data-stu-id="82ea2-202">Navigate to `http://localhost:8000`.</span></span> <span data-ttu-id="82ea2-203">Sayfa hatasız yüklerse, PHP uygulaması Azure MySQL veritabanına bağlanıyor.</span><span class="sxs-lookup"><span data-stu-id="82ea2-203">If the page loads without errors, the PHP application is connecting to the MySQL database in Azure.</span></span>

<span data-ttu-id="82ea2-204">Bazı görevler sayfasında ekleyin.</span><span class="sxs-lookup"><span data-stu-id="82ea2-204">Add a few tasks in the page.</span></span>

![PHP, Azure veritabanına başarıyla MySQL (Önizleme) bağlanır.](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="82ea2-206">PHP durdurmak için aşağıdakileri yazın `Ctrl + C` Terminal.</span><span class="sxs-lookup"><span data-stu-id="82ea2-206">To stop PHP, type `Ctrl + C` in the terminal.</span></span>

### <a name="commit-your-changes"></a><span data-ttu-id="82ea2-207">Değişikliklerinizi uygulamak</span><span class="sxs-lookup"><span data-stu-id="82ea2-207">Commit your changes</span></span>

<span data-ttu-id="82ea2-208">Değişikliklerinizi kaydetmek için aşağıdaki Git komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="82ea2-208">Run the following Git commands to commit your changes:</span></span>

```bash
git add .
git commit -m "database.php updates"
```

<span data-ttu-id="82ea2-209">Uygulamanız dağıtılmaya hazırdır.</span><span class="sxs-lookup"><span data-stu-id="82ea2-209">Your app is ready to be deployed.</span></span>

## <a name="deploy-to-azure"></a><span data-ttu-id="82ea2-210">Azure’a Dağıt</span><span class="sxs-lookup"><span data-stu-id="82ea2-210">Deploy to Azure</span></span>

<span data-ttu-id="82ea2-211">Bu adımda, Azure App Service'e MySQL bağlı PHP uygulaması dağıtın.</span><span class="sxs-lookup"><span data-stu-id="82ea2-211">In this step, you deploy the MySQL-connected PHP application to Azure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="82ea2-212">App Service planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="82ea2-212">Create an App Service plan</span></span>

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a><span data-ttu-id="82ea2-213">Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="82ea2-213">Create a web app</span></span>

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-the-php-version"></a><span data-ttu-id="82ea2-214">PHP sürümünü ayarlayın</span><span class="sxs-lookup"><span data-stu-id="82ea2-214">Set the PHP version</span></span>

<span data-ttu-id="82ea2-215">Kullanarak uygulama gerektiriyor PHP sürümünü ayarlayın [az webapp yapılandırma kümesi](/cli/azure/webapp/config#set) komutu.</span><span class="sxs-lookup"><span data-stu-id="82ea2-215">Set the PHP version that the application requires by using the [az webapp config set](/cli/azure/webapp/config#set) command.</span></span>

<span data-ttu-id="82ea2-216">Aşağıdaki komut PHP sürümünü ayarlar _7.0_.</span><span class="sxs-lookup"><span data-stu-id="82ea2-216">The following command sets the PHP version to _7.0_.</span></span>

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a><span data-ttu-id="82ea2-217">Veritabanı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="82ea2-217">Configure database settings</span></span>

<span data-ttu-id="82ea2-218">Daha önce işaret edildiği gibi Azure MySQL veritabanınızı App Service'te ortam değişkenleri kullanarak bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="82ea2-218">As pointed out previously, you can connect to your Azure MySQL database using environment variables in App Service.</span></span>

<span data-ttu-id="82ea2-219">Ortam değişkenleri olarak ayarladığınız App Service'te _uygulama ayarları_ kullanarak [az webapp config appsettings kümesi](/cli/azure/webapp/config/appsettings#set) komutu.</span><span class="sxs-lookup"><span data-stu-id="82ea2-219">In App Service, you set environment variables as _app settings_ by using the [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span>

<span data-ttu-id="82ea2-220">Aşağıdaki komut uygulama ayarlarını yapılandırır `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, ve `DB_PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="82ea2-220">The following command configures the app settings `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD`.</span></span> <span data-ttu-id="82ea2-221">Yer tutucuları değiştirmek  _&lt;uygulamaadı >_ ve  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="82ea2-221">Replace the placeholders _&lt;appname>_ and _&lt;mysql_server_name>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

<span data-ttu-id="82ea2-222">PHP kullanabilirsiniz [getenv](http://www.php.net/manual/function.getenv.php) ayarlarına erişmek için yöntem.</span><span class="sxs-lookup"><span data-stu-id="82ea2-222">You can use the PHP [getenv](http://www.php.net/manual/function.getenv.php) method to access the settings.</span></span> <span data-ttu-id="82ea2-223">Laravel kodu kullanan bir [env](https://laravel.com/docs/5.4/helpers#method-env) sarmalayıcı PHP üzerinden `getenv`.</span><span class="sxs-lookup"><span data-stu-id="82ea2-223">the Laravel code uses an [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper over the PHP `getenv`.</span></span> <span data-ttu-id="82ea2-224">Örneğin, MySQL yapılandırmasında _config/database.php_ aşağıdaki kod gibi görünüyor:</span><span class="sxs-lookup"><span data-stu-id="82ea2-224">For example, the MySQL configuration in _config/database.php_ looks like the following code:</span></span>

```php
'mysql' => [
    'driver'    => 'mysql',
    'host'      => env('DB_HOST', 'localhost'),
    'database'  => env('DB_DATABASE', 'forge'),
    'username'  => env('DB_USERNAME', 'forge'),
    'password'  => env('DB_PASSWORD', ''),
    ...
],
```

### <a name="configure-laravel-environment-variables"></a><span data-ttu-id="82ea2-225">Laravel ortam değişkenlerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="82ea2-225">Configure Laravel environment variables</span></span>

<span data-ttu-id="82ea2-226">Laravel App Service'te bir uygulama anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="82ea2-226">Laravel needs an application key in App Service.</span></span> <span data-ttu-id="82ea2-227">Uygulama ayarları ile yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82ea2-227">You can configure it with app settings.</span></span>

<span data-ttu-id="82ea2-228">Kullanım `php artisan` için kaydetmeden yeni bir uygulama anahtarı oluşturmak için _.env_.</span><span class="sxs-lookup"><span data-stu-id="82ea2-228">Use `php artisan` to generate a new application key without saving it to _.env_.</span></span>

```bash
php artisan key:generate --show
```

<span data-ttu-id="82ea2-229">Uygulama anahtarı kullanarak App Service'te web uygulaması ayarlamak [az webapp config appsettings kümesi](/cli/azure/webapp/config/appsettings#set) komutu.</span><span class="sxs-lookup"><span data-stu-id="82ea2-229">Set the application key in the App Service web app by using the [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span> <span data-ttu-id="82ea2-230">Yer tutucuları değiştirmek  _&lt;uygulamaadı >_ ve  _&lt;outputofphpartisankey: Oluştur >_.</span><span class="sxs-lookup"><span data-stu-id="82ea2-230">Replace the placeholders _&lt;appname>_ and _&lt;outputofphpartisankey:generate>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

<span data-ttu-id="82ea2-231">`APP_DEBUG="true"`dağıtılan web uygulamasının hatalarla karşılaştığında hata ayıklama bilgileri döndürmek için Laravel söyler.</span><span class="sxs-lookup"><span data-stu-id="82ea2-231">`APP_DEBUG="true"` tells Laravel to return debugging information when the deployed web app encounters errors.</span></span> <span data-ttu-id="82ea2-232">Bir üretim uygulaması çalıştırırken kümesine `false`, daha güvenli olduğu.</span><span class="sxs-lookup"><span data-stu-id="82ea2-232">When running a production application, set it to `false`, which is more secure.</span></span>

### <a name="set-the-virtual-application-path"></a><span data-ttu-id="82ea2-233">Sanal uygulama yolu ayarla</span><span class="sxs-lookup"><span data-stu-id="82ea2-233">Set the virtual application path</span></span>

<span data-ttu-id="82ea2-234">Web uygulaması için sanal uygulama yolu ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="82ea2-234">Set the virtual application path for the web app.</span></span> <span data-ttu-id="82ea2-235">Bu adım gereklidir çünkü [Laravel uygulama yaşam döngüsü](https://laravel.com/docs/5.4/lifecycle) içinde başlar _ortak_ uygulamanızın kök dizininde yerine dizin.</span><span class="sxs-lookup"><span data-stu-id="82ea2-235">This step is required because the [Laravel application lifecycle](https://laravel.com/docs/5.4/lifecycle) begins in the _public_ directory instead of the application's root directory.</span></span> <span data-ttu-id="82ea2-236">İçinde yaşam döngüsü başlatmak diğer PHP çerçeveleri kök dizini sanal uygulama yolu el ile yapılandırma olmadan çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="82ea2-236">Other PHP frameworks whose lifecycle start in the root directory can work without manual configuration of the virtual application path.</span></span>

<span data-ttu-id="82ea2-237">Sanal uygulama yolu kullanarak ayarlamak [az kaynak güncelleştirme](/cli/azure/resource#update) komutu.</span><span class="sxs-lookup"><span data-stu-id="82ea2-237">Set the virtual application path by using the [az resource update](/cli/azure/resource#update) command.</span></span> <span data-ttu-id="82ea2-238">Değiştir  _&lt;uygulamaadı >_ yer tutucu.</span><span class="sxs-lookup"><span data-stu-id="82ea2-238">Replace the _&lt;appname>_ placeholder.</span></span>

```azurecli-interactive
az resource update \
    --name web \
    --resource-group myResourceGroup \
    --namespace Microsoft.Web \
    --resource-type config \
    --parent sites/<app_name> \
    --set properties.virtualApplications[0].physicalPath="site\wwwroot\public" \
    --api-version 2015-06-01
```

<span data-ttu-id="82ea2-239">Varsayılan olarak, Azure App Service kök sanal uygulama yolu işaret (_/_) dağıtılan uygulama dosyalarını kök dizinine (_sites\wwwroot_).</span><span class="sxs-lookup"><span data-stu-id="82ea2-239">By default, Azure App Service points the root virtual application path (_/_) to the root directory of the deployed application files (_sites\wwwroot_).</span></span>

### <a name="configure-a-deployment-user"></a><span data-ttu-id="82ea2-240">Dağıtım kullanıcısı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="82ea2-240">Configure a deployment user</span></span>

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a><span data-ttu-id="82ea2-241">Yerel Git dağıtımını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="82ea2-241">Configure local Git deployment</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-to-azure-from-git"></a><span data-ttu-id="82ea2-242">Git üzerinden Azure'a gönderme</span><span class="sxs-lookup"><span data-stu-id="82ea2-242">Push to Azure from Git</span></span>

<span data-ttu-id="82ea2-243">Yerel Git deponuza bir Azure uzak deposu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="82ea2-243">Add an Azure remote to your local Git repository.</span></span>

```bash
git remote add azure <paste_copied_url_here>
```

<span data-ttu-id="82ea2-244">Azure'a PHP uygulama dağıtmak için uzaktan gönderin.</span><span class="sxs-lookup"><span data-stu-id="82ea2-244">Push to the Azure remote to deploy the PHP application.</span></span> <span data-ttu-id="82ea2-245">Daha önce dağıtım kullanıcı oluşturmanın bir parçası sağlanan parola istenir.</span><span class="sxs-lookup"><span data-stu-id="82ea2-245">You are prompted for the password you supplied earlier as part of the creation of the deployment user.</span></span>

```bash
git push azure master
```

<span data-ttu-id="82ea2-246">Dağıtım sırasında Azure App Service, ilerleme durumunu Git ile iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="82ea2-246">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 291 bytes | 0 bytes/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'a5e076db9c'.
remote: Running custom deployment command...
remote: Running deployment command...
...
< Output has been truncated for readability >
```

> [!NOTE]
> <span data-ttu-id="82ea2-247">Dağıtım işlemi yükleyeceğini karşılaşabilirsiniz [Oluşturucu](https://getcomposer.org/) sonunda paketler.</span><span class="sxs-lookup"><span data-stu-id="82ea2-247">You may notice that the deployment process installs [Composer](https://getcomposer.org/) packages at the end.</span></span> <span data-ttu-id="82ea2-248">Uygulama hizmeti varsayılan dağıtımı sırasında bu otomasyonlara çalışmaz, bu örnek depo etkinleştirmek için kök dizindeki üç ek dosyaların sahiptir:</span><span class="sxs-lookup"><span data-stu-id="82ea2-248">App Service does not run these automations during default deployment, so this sample repository has three additional files in its root directory to enable it:</span></span>
>
> - <span data-ttu-id="82ea2-249">`.deployment`-Bu dosyayı çalıştırmak için uygulama hizmeti söyler `bash deploy.sh` özel dağıtım komut dosyası olarak.</span><span class="sxs-lookup"><span data-stu-id="82ea2-249">`.deployment` - This file tells App Service to run `bash deploy.sh` as the custom deployment script.</span></span>
> - <span data-ttu-id="82ea2-250">`deploy.sh`-Özel dağıtım komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="82ea2-250">`deploy.sh` - The custom deployment script.</span></span> <span data-ttu-id="82ea2-251">Dosyayı gözden geçirirseniz, çalıştığını görürsünüz `php composer.phar install` sonra `npm install`.</span><span class="sxs-lookup"><span data-stu-id="82ea2-251">If you review the file, you will see that it runs `php composer.phar install` after `npm install`.</span></span>
> - <span data-ttu-id="82ea2-252">`composer.phar`-Oluşturucu Paket Yöneticisi.</span><span class="sxs-lookup"><span data-stu-id="82ea2-252">`composer.phar` - The Composer package manager.</span></span>
>
> <span data-ttu-id="82ea2-253">Git tabanlı dağıtımınız App Service için herhangi bir adımı eklemek için bu yaklaşımı kullanın.</span><span class="sxs-lookup"><span data-stu-id="82ea2-253">You can use this approach to add any step to your Git-based deployment to App Service.</span></span> <span data-ttu-id="82ea2-254">Daha fazla bilgi için bkz: [özel dağıtım betiği](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span><span class="sxs-lookup"><span data-stu-id="82ea2-254">For more information, see [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span></span>
>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="82ea2-255">Azure web uygulaması'na göz atın</span><span class="sxs-lookup"><span data-stu-id="82ea2-255">Browse to the Azure web app</span></span>

<span data-ttu-id="82ea2-256">Gözat `http://<app_name>.azurewebsites.net` ve birkaç görevi listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="82ea2-256">Browse to `http://<app_name>.azurewebsites.net` and add a few tasks to the list.</span></span>

![Azure uygulama Hizmeti'nde çalışan PHP uygulaması](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

<span data-ttu-id="82ea2-258">Tebrikler, Azure App Service'te bir veri güdümlü PHP uygulaması çalıştırıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="82ea2-258">Congratulations, you're running a data-driven PHP app in Azure App Service.</span></span>

## <a name="update-model-locally-and-redeploy"></a><span data-ttu-id="82ea2-259">Modeli yerel olarak güncelleştirin ve yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="82ea2-259">Update model locally and redeploy</span></span>

<span data-ttu-id="82ea2-260">Bu adımda, bir basit değişiklik `task` veri modeli ve webapp ve güncelleştirme Azure'a yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82ea2-260">In this step, you make a simple change to the `task` data model and the webapp, and then publish the update to Azure.</span></span>

<span data-ttu-id="82ea2-261">Görevler senaryo için bir görev tamamlandı olarak işaretleyebilirsiniz şekilde uygulama değiştirin.</span><span class="sxs-lookup"><span data-stu-id="82ea2-261">For the tasks scenario, you modify the application so that you can mark a task as complete.</span></span>

### <a name="add-a-column"></a><span data-ttu-id="82ea2-262">Bir sütun ekleyin</span><span class="sxs-lookup"><span data-stu-id="82ea2-262">Add a column</span></span>

<span data-ttu-id="82ea2-263">Terminale Git deposu kök dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="82ea2-263">In the terminal, navigate to the root of the Git repository.</span></span>

<span data-ttu-id="82ea2-264">İçin yeni bir veritabanı geçiş oluşturmayı `tasks` tablosu:</span><span class="sxs-lookup"><span data-stu-id="82ea2-264">Generate a new database migration for the `tasks` table:</span></span>

```bash
php artisan make:migration add_complete_column --table=tasks
```

<span data-ttu-id="82ea2-265">Bu komut oluşturulur geçiş dosyasının adını gösterir.</span><span class="sxs-lookup"><span data-stu-id="82ea2-265">This command shows you the name of the migration file that's generated.</span></span> <span data-ttu-id="82ea2-266">Bu dosyada Bul _veritabanı/geçişler_ ve açın.</span><span class="sxs-lookup"><span data-stu-id="82ea2-266">Find this file in _database/migrations_ and open it.</span></span>

<span data-ttu-id="82ea2-267">Değiştir `up` aşağıdaki kod ile yöntemi:</span><span class="sxs-lookup"><span data-stu-id="82ea2-267">Replace the `up` method with the following code:</span></span>

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

<span data-ttu-id="82ea2-268">Önceki kod bir boolean sütunundaki ekler `tasks` adlı bir tablo `complete`.</span><span class="sxs-lookup"><span data-stu-id="82ea2-268">The preceding code adds a boolean column in the `tasks` table called `complete`.</span></span>

<span data-ttu-id="82ea2-269">Değiştir `down` geri alma eylemi için aşağıdaki kod ile yöntemi:</span><span class="sxs-lookup"><span data-stu-id="82ea2-269">Replace the `down` method with the following code for the rollback action:</span></span>

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

<span data-ttu-id="82ea2-270">Terminale yerel veritabanında değişiklik yapmak için Laravel veritabanı geçiş çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="82ea2-270">In the terminal, run Laravel database migrations to make the change in the local database.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="82ea2-271">Temel [Laravel adlandırma kuralı](https://laravel.com/docs/5.4/eloquent#defining-models), model `Task` (bkz _app/Task.php_) eşlendiği `tasks` varsayılan olarak tablo.</span><span class="sxs-lookup"><span data-stu-id="82ea2-271">Based on the [Laravel naming convention](https://laravel.com/docs/5.4/eloquent#defining-models), the model `Task` (see _app/Task.php_) maps to the `tasks` table by default.</span></span>

### <a name="update-application-logic"></a><span data-ttu-id="82ea2-272">Uygulama mantığını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="82ea2-272">Update application logic</span></span>

<span data-ttu-id="82ea2-273">Açık *routes/web.php* dosya.</span><span class="sxs-lookup"><span data-stu-id="82ea2-273">Open the *routes/web.php* file.</span></span> <span data-ttu-id="82ea2-274">Uygulama kendi yollar ve iş mantığı buraya tanımlar.</span><span class="sxs-lookup"><span data-stu-id="82ea2-274">The application defines its routes and business logic here.</span></span>

<span data-ttu-id="82ea2-275">Dosyanın sonunda bir yol ile aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="82ea2-275">At the end of the file, add a route with the following code:</span></span>

```php
/**
 * Toggle Task completeness
 */
Route::post('/task/{id}', function ($id) {
    error_log('INFO: post /task/'.$id);
    $task = Task::findOrFail($id);

    $task->complete = !$task->complete;
    $task->save();

    return redirect('/');
});
```

<span data-ttu-id="82ea2-276">Önceki kod, değerini değiştirerek veri modelini basit bir güncelleştirme yapar `complete`.</span><span class="sxs-lookup"><span data-stu-id="82ea2-276">The preceding code makes a simple update to the data model by toggling the value of `complete`.</span></span>

### <a name="update-the-view"></a><span data-ttu-id="82ea2-277">Görünümü güncelleştirmek</span><span class="sxs-lookup"><span data-stu-id="82ea2-277">Update the view</span></span>

<span data-ttu-id="82ea2-278">Açık *resources/views/tasks.blade.php* dosya.</span><span class="sxs-lookup"><span data-stu-id="82ea2-278">Open the *resources/views/tasks.blade.php* file.</span></span> <span data-ttu-id="82ea2-279">Bul `<tr>` açma etiketi ve ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="82ea2-279">Find the `<tr>` opening tag and replace it with:</span></span>

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

<span data-ttu-id="82ea2-280">Önceki kod görev tam olup olmamasına bağlı olarak satır rengi değişir.</span><span class="sxs-lookup"><span data-stu-id="82ea2-280">The preceding code changes the row color depending on whether the task is complete.</span></span>

<span data-ttu-id="82ea2-281">Sonraki satırında, aşağıdaki kodu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="82ea2-281">In the next line, you have the following code:</span></span>

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

<span data-ttu-id="82ea2-282">Tüm satırı aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="82ea2-282">Replace the entire line with the following code:</span></span>

```html
<td>
    <form action="{{ url('task/'.$task->id) }}" method="POST">
        {{ csrf_field() }}

        <button type="submit" class="btn btn-xs">
            <i class="fa {{$task->complete ? 'fa-check-square-o' : 'fa-square-o'}}"></i>
        </button>
        {{ $task->name }}
    </form>
</td>
```

<span data-ttu-id="82ea2-283">Önceki kod daha önce tanımlanan rota başvuran Gönder düğmesi ekler.</span><span class="sxs-lookup"><span data-stu-id="82ea2-283">The preceding code adds the submit button that references the route that you defined earlier.</span></span>

### <a name="test-the-changes-locally"></a><span data-ttu-id="82ea2-284">Değişiklikleri yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="82ea2-284">Test the changes locally</span></span>

<span data-ttu-id="82ea2-285">Git deposu kök dizininden geliştirme sunucusu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="82ea2-285">From the root directory of the Git repository, run the development server.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="82ea2-286">Değiştirme, gidin görev durumunu görmek için `http://localhost:8000` ve onay kutusunu seçin.</span><span class="sxs-lookup"><span data-stu-id="82ea2-286">To see the task status change, navigate to `http://localhost:8000` and select the checkbox.</span></span>

![Görev için eklenen onay kutusu](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

<span data-ttu-id="82ea2-288">PHP durdurmak için aşağıdakileri yazın `Ctrl + C` Terminal.</span><span class="sxs-lookup"><span data-stu-id="82ea2-288">To stop PHP, type `Ctrl + C` in the terminal.</span></span>

### <a name="publish-changes-to-azure"></a><span data-ttu-id="82ea2-289">Değişiklikler için Azure yayımlama</span><span class="sxs-lookup"><span data-stu-id="82ea2-289">Publish changes to Azure</span></span>

<span data-ttu-id="82ea2-290">Terminale Laravel veritabanı geçişler üretim bağlantı dizesini içeren Azure veritabanında değişiklik yapmak için çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="82ea2-290">In the terminal, run Laravel database migrations with the production connection string to make the change in the Azure database.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="82ea2-291">Git tüm değişiklikleri uygulayın ve ardından kod değişiklikleri Azure'a gönderin.</span><span class="sxs-lookup"><span data-stu-id="82ea2-291">Commit all the changes in Git, and then push the code changes to Azure.</span></span>

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

<span data-ttu-id="82ea2-292">Bir kez `git push` tamamlamak, Azure web uygulaması'na gidin ve yeni işlevselliğini test etmek içindir.</span><span class="sxs-lookup"><span data-stu-id="82ea2-292">Once the `git push` is complete, navigate to the Azure web app and test the new functionality.</span></span>

![Azure için yayımlanan modeli ve veritabanı değişiklikleri](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="82ea2-294">Herhangi bir görevi eklediyseniz bunlar veritabanında tutulur.</span><span class="sxs-lookup"><span data-stu-id="82ea2-294">If you added any tasks, they are retained in the database.</span></span> <span data-ttu-id="82ea2-295">Veri şema güncelleştirmeleri varolan veriler olduğu gibi bırakın.</span><span class="sxs-lookup"><span data-stu-id="82ea2-295">Updates to the data schema leave existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="82ea2-296">Akış tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="82ea2-296">Stream diagnostic logs</span></span>

<span data-ttu-id="82ea2-297">PHP uygulaması Azure App Service'te çalışırken, terminal yöneltilen konsol günlükleri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82ea2-297">While the PHP application runs in Azure App Service, you can get the console logs piped to your terminal.</span></span> <span data-ttu-id="82ea2-298">Böylece, uygulama hatalarını hata ayıklama yardımcı olmak için aynı tanılama iletileri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82ea2-298">That way, you can get the same diagnostic messages to help you debug application errors.</span></span>

<span data-ttu-id="82ea2-299">Günlük akış başlatmak için kullanmak [az webapp günlük tail](/cli/azure/webapp/log#tail) komutu.</span><span class="sxs-lookup"><span data-stu-id="82ea2-299">To start log streaming, use the [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

<span data-ttu-id="82ea2-300">Günlük akış başladıktan sonra Azure web uygulaması bazı web trafiği almak için tarayıcıda yenileyin.</span><span class="sxs-lookup"><span data-stu-id="82ea2-300">Once log streaming has started, refresh the Azure web app in the browser to get some web traffic.</span></span> <span data-ttu-id="82ea2-301">Konsol günlükleri terminale yöneltilen şimdi görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82ea2-301">You can now see console logs piped to the terminal.</span></span> <span data-ttu-id="82ea2-302">Konsol günlükleri hemen görmüyorsanız, 30 saniye içinde yeniden kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="82ea2-302">If you don't see console logs immediately, check again in 30 seconds.</span></span>

<span data-ttu-id="82ea2-303">Dilediğiniz zaman oturum sırasında akış durdurmak için aşağıdakileri yazın `Ctrl` + `C`.</span><span class="sxs-lookup"><span data-stu-id="82ea2-303">To stop log streaming at anytime, type `Ctrl`+`C`.</span></span>

> [!TIP]
> <span data-ttu-id="82ea2-304">Bir PHP uygulaması standart kullanabilir [error_log()](http://php.net/manual/function.error-log.php) konsola çıktı için.</span><span class="sxs-lookup"><span data-stu-id="82ea2-304">A PHP application can use the standard [error_log()](http://php.net/manual/function.error-log.php) to output to the console.</span></span> <span data-ttu-id="82ea2-305">Örnek uygulama bu yaklaşımı kullanır _app/Http/routes.php_.</span><span class="sxs-lookup"><span data-stu-id="82ea2-305">The sample application uses this approach in _app/Http/routes.php_.</span></span>
>
> <span data-ttu-id="82ea2-306">Bir web çerçevesidir olarak [Laravel kullanan Monolog](https://laravel.com/docs/5.4/errors) olarak oturum açma sağlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="82ea2-306">As a web framework, [Laravel uses Monolog](https://laravel.com/docs/5.4/errors) as the logging provider.</span></span> <span data-ttu-id="82ea2-307">Çıkış iletilerini konsola Monolog alınacağı hakkında bilgi için bkz: [PHP: monolog Konsolu'na (php://out) oturum için nasıl kullanılacağını](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span><span class="sxs-lookup"><span data-stu-id="82ea2-307">To see how to get Monolog to output messages to the console, see [PHP: How to use monolog to log to console (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span></span>
>
>

## <a name="manage-the-azure-web-app"></a><span data-ttu-id="82ea2-308">Azure web uygulamasını yönetme</span><span class="sxs-lookup"><span data-stu-id="82ea2-308">Manage the Azure web app</span></span>

<span data-ttu-id="82ea2-309">Oluşturduğunuz web uygulamasını yönetmek için [Azure portalına](https://portal.azure.com) gidin.</span><span class="sxs-lookup"><span data-stu-id="82ea2-309">Go to the [Azure portal](https://portal.azure.com) to manage the web app you created.</span></span>

<span data-ttu-id="82ea2-310">Sol menüden **Uygulama Hizmetleri**'ne ve ardından Azure web uygulamanızın adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="82ea2-310">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Portaldan Azure web uygulamasına gitme](./media/app-service-web-tutorial-php-mysql/access-portal.png)

<span data-ttu-id="82ea2-312">Web uygulamanızın Genel Bakış sayfasını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="82ea2-312">You see your web app's Overview page.</span></span> <span data-ttu-id="82ea2-313">Burada, Durdur, Başlat, yeniden başlatma, Gözat ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82ea2-313">Here, you can perform basic management tasks like  stop, start, restart, browse, and delete.</span></span>

<span data-ttu-id="82ea2-314">Soldaki menüden, uygulamanızı yapılandırmak için sayfaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="82ea2-314">The left menu provides pages for configuring your app.</span></span>

![Azure portalında App Service sayfası](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="82ea2-316">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="82ea2-316">Next steps</span></span>

<span data-ttu-id="82ea2-317">Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="82ea2-317">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="82ea2-318">Azure üzerinde MySQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="82ea2-318">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="82ea2-319">MySQL için PHP uygulamaya Bağlan</span><span class="sxs-lookup"><span data-stu-id="82ea2-319">Connect a PHP app to MySQL</span></span>
> * <span data-ttu-id="82ea2-320">Uygulamayı Azure'a dağıtma</span><span class="sxs-lookup"><span data-stu-id="82ea2-320">Deploy the app to Azure</span></span>
> * <span data-ttu-id="82ea2-321">Veri modeli güncelleştirme ve uygulamayı yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="82ea2-321">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="82ea2-322">Azure Stream tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="82ea2-322">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="82ea2-323">Azure portalında uygulama yönetme</span><span class="sxs-lookup"><span data-stu-id="82ea2-323">Manage the app in the Azure portal</span></span>

<span data-ttu-id="82ea2-324">Bir web uygulaması için özel bir DNS adı eşleme öğrenmek için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="82ea2-324">Advance to the next tutorial to learn how to map a custom DNS name to a web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="82ea2-325">Mevcut bir özel DNS adını Azure Web Apps ile eşleme</span><span class="sxs-lookup"><span data-stu-id="82ea2-325">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
