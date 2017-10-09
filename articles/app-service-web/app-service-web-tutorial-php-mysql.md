---
title: "aaaBuild azure'da PHP ve MySQL bir web uygulaması | Microsoft Docs"
description: "Bilgi nasıl Azure'da çalışan bir PHP uygulaması ile bağlantı tooa MySQL veritabanı Azure'da tooget."
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
ms.openlocfilehash: 3c050b30e2e2c80d011bed989cd5f8cecac35d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-php-and-mysql-web-app-in-azure"></a><span data-ttu-id="b6324-103">Azure'da PHP ve MySQL bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="b6324-103">Build a PHP and MySQL web app in Azure</span></span>

<span data-ttu-id="b6324-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) yüksek oranda ölçeklenebilen, kendi kendine düzeltme eki uygulayan bir web barındırma hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="b6324-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="b6324-105">Bu öğretici nasıl toocreate bir PHP web uygulaması Azure ve tooa MySQL veritabanına bağlanmak gösterir.</span><span class="sxs-lookup"><span data-stu-id="b6324-105">This tutorial shows how toocreate a PHP web app in Azure and connect it tooa MySQL database.</span></span> <span data-ttu-id="b6324-106">İşiniz bittiğinde, gerekir bir [Laravel](https://laravel.com/) Azure App Service Web Apps üzerinde çalışan uygulama.</span><span class="sxs-lookup"><span data-stu-id="b6324-106">When you're finished, you'll have a [Laravel](https://laravel.com/) app running on Azure App Service Web Apps.</span></span>

![Azure uygulama Hizmeti'nde çalışan PHP uygulaması](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="b6324-108">Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="b6324-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b6324-109">Azure üzerinde MySQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b6324-109">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="b6324-110">PHP uygulama tooMySQL Bağlan</span><span class="sxs-lookup"><span data-stu-id="b6324-110">Connect a PHP app tooMySQL</span></span>
> * <span data-ttu-id="b6324-111">Merhaba uygulama tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="b6324-111">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="b6324-112">Merhaba veri modeli güncelleştirmek ve hello uygulama yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="b6324-112">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="b6324-113">Azure Stream tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="b6324-113">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="b6324-114">Merhaba uygulamada hello Azure portalı Yönet</span><span class="sxs-lookup"><span data-stu-id="b6324-114">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6324-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b6324-115">Prerequisites</span></span>

<span data-ttu-id="b6324-116">toocomplete Bu öğretici:</span><span class="sxs-lookup"><span data-stu-id="b6324-116">toocomplete this tutorial:</span></span>

* [<span data-ttu-id="b6324-117">Git'i yükleyin</span><span class="sxs-lookup"><span data-stu-id="b6324-117">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="b6324-118">PHP 5.6.4 yükleme veya üstü</span><span class="sxs-lookup"><span data-stu-id="b6324-118">Install PHP 5.6.4 or above</span></span>](http://php.net/downloads.php)
* [<span data-ttu-id="b6324-119">Oluşturucu yükleyin</span><span class="sxs-lookup"><span data-stu-id="b6324-119">Install Composer</span></span>](https://getcomposer.org/doc/00-intro.md)
* <span data-ttu-id="b6324-120">PHP uzantıları Laravel gereksinimlerini aşağıdaki hello etkinleştirin: OpenSSL, PDO MySQL, Mbstring, belirteç Oluşturucu, XML</span><span class="sxs-lookup"><span data-stu-id="b6324-120">Enable hello following PHP extensions Laravel needs: OpenSSL, PDO-MySQL, Mbstring, Tokenizer, XML</span></span>
* [<span data-ttu-id="b6324-121">Yükleyin ve MySQL başlatın</span><span class="sxs-lookup"><span data-stu-id="b6324-121">Install and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a><span data-ttu-id="b6324-122">Yerel MySQL hazırlama</span><span class="sxs-lookup"><span data-stu-id="b6324-122">Prepare local MySQL</span></span>

<span data-ttu-id="b6324-123">Bu adımda, bir veritabanı yerel MySQL sunucunuzu Bu öğreticide, kullanımınız için oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b6324-123">In this step, you create a database in your local MySQL server for your use in this tutorial.</span></span>

### <a name="connect-toolocal-mysql-server"></a><span data-ttu-id="b6324-124">Toolocal MySQL server Bağlan</span><span class="sxs-lookup"><span data-stu-id="b6324-124">Connect toolocal MySQL server</span></span>

<span data-ttu-id="b6324-125">Bir terminal penceresi tooyour yerel MySQL sunucusuna bağlanın.</span><span class="sxs-lookup"><span data-stu-id="b6324-125">In a terminal window, connect tooyour local MySQL server.</span></span> <span data-ttu-id="b6324-126">Bu bir terminal penceresi toorun Bu öğreticide tüm hello komutlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6324-126">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="b6324-127">İçin bir parola istenirse Merhaba hello parolayı girin `root` hesabı.</span><span class="sxs-lookup"><span data-stu-id="b6324-127">If you're prompted for a password, enter hello password for hello `root` account.</span></span> <span data-ttu-id="b6324-128">Kök hesap parolanızı hatırlamıyorsanız bkz [MySQL: nasıl tooReset hello kök parola](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span><span class="sxs-lookup"><span data-stu-id="b6324-128">If you don't remember your root account password, see [MySQL: How tooReset hello Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="b6324-129">Komutunuzu başarıyla çalışırsa, MySQL sunucunuzu çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="b6324-129">If your command runs successfully, then your MySQL server is running.</span></span> <span data-ttu-id="b6324-130">Aksi takdirde, yerel MySQL sunucunuz tarafından aşağıdaki hello başlatıldığından emin olun [MySQL yükleme sonrası adımları](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="b6324-130">If not, make sure that your local MySQL server is started by following hello [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database-locally"></a><span data-ttu-id="b6324-131">Yerel bir veritabanı oluşturun</span><span class="sxs-lookup"><span data-stu-id="b6324-131">Create a database locally</span></span>

<span data-ttu-id="b6324-132">Merhaba, `mysql` isteminde, bir veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b6324-132">At hello `mysql` prompt, create a database.</span></span>

```sql 
CREATE DATABASE sampledb;
```

<span data-ttu-id="b6324-133">Sunucu bağlantısı yazarak çıkmak `quit`.</span><span class="sxs-lookup"><span data-stu-id="b6324-133">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a><span data-ttu-id="b6324-134">Yerel olarak bir PHP uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="b6324-134">Create a PHP app locally</span></span>
<span data-ttu-id="b6324-135">Bu adımda, Laravel örnek bir uygulama almak, veritabanı bağlantısını yapılandırın ve yerel olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b6324-135">In this step, you get a Laravel sample application, configure its database connection, and run it locally.</span></span> 

### <a name="clone-hello-sample"></a><span data-ttu-id="b6324-136">Kopya hello örnek</span><span class="sxs-lookup"><span data-stu-id="b6324-136">Clone hello sample</span></span>

<span data-ttu-id="b6324-137">Merhaba terminal penceresinde `cd` tooa çalışma dizini.</span><span class="sxs-lookup"><span data-stu-id="b6324-137">In hello terminal window, `cd` tooa working directory.</span></span>

<span data-ttu-id="b6324-138">Çalışma hello aşağıdaki tooclone hello örnek depo komutu.</span><span class="sxs-lookup"><span data-stu-id="b6324-138">Run hello following command tooclone hello sample repository.</span></span>

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

<span data-ttu-id="b6324-139">`cd`tooyour kopyalanan dizin.</span><span class="sxs-lookup"><span data-stu-id="b6324-139">`cd` tooyour cloned directory.</span></span>
<span data-ttu-id="b6324-140">Gerekli hello paketlerini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b6324-140">Install hello required packages.</span></span>

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a><span data-ttu-id="b6324-141">MySQL bağlantısını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="b6324-141">Configure MySQL connection</span></span>

<span data-ttu-id="b6324-142">Merhaba depo kök dizininde adlı bir dosya oluşturun *.env*.</span><span class="sxs-lookup"><span data-stu-id="b6324-142">In hello repository root, create a file named *.env*.</span></span> <span data-ttu-id="b6324-143">Değişkenleri hello aşağıdaki kopyalama hello *.env* dosya.</span><span class="sxs-lookup"><span data-stu-id="b6324-143">Copy hello following variables into hello *.env* file.</span></span> <span data-ttu-id="b6324-144">Hello yerine  _&lt;root_password >_ yer tutucusunu hello MySQL kök kullanıcının parolası ile.</span><span class="sxs-lookup"><span data-stu-id="b6324-144">Replace hello _&lt;root_password>_ placeholder with hello MySQL root user's password.</span></span>

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

<span data-ttu-id="b6324-145">Laravel hello nasıl kullandığı hakkında bilgi için _.env_ dosya için bkz: [Laravel ortamı Yapılandırması](https://laravel.com/docs/5.4/configuration#environment-configuration).</span><span class="sxs-lookup"><span data-stu-id="b6324-145">For information on how Laravel uses hello _.env_ file, see [Laravel Environment Configuration](https://laravel.com/docs/5.4/configuration#environment-configuration).</span></span>

### <a name="run-hello-sample-locally"></a><span data-ttu-id="b6324-146">Merhaba örnek yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b6324-146">Run hello sample locally</span></span>

<span data-ttu-id="b6324-147">Çalıştırma [Laravel veritabanı geçişler](https://laravel.com/docs/5.4/migrations) toocreate hello tabloları hello uygulama gereksinimleri.</span><span class="sxs-lookup"><span data-stu-id="b6324-147">Run [Laravel database migrations](https://laravel.com/docs/5.4/migrations) toocreate hello tables hello application needs.</span></span> <span data-ttu-id="b6324-148">hangi tablolar oluşturulur hello geçişlerde, arama hello toosee _veritabanı/geçişler_ hello Git deposu dizin.</span><span class="sxs-lookup"><span data-stu-id="b6324-148">toosee which tables are created in hello migrations, look in hello _database/migrations_ directory in hello Git repository.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="b6324-149">Yeni bir Laravel uygulama anahtarı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b6324-149">Generate a new Laravel application key.</span></span>

```bash
php artisan key:generate
```

<span data-ttu-id="b6324-150">Merhaba uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b6324-150">Run hello application.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="b6324-151">Çok gidin`http://localhost:8000` bir tarayıcıda.</span><span class="sxs-lookup"><span data-stu-id="b6324-151">Navigate too`http://localhost:8000` in a browser.</span></span> <span data-ttu-id="b6324-152">Bazı görevleri hello sayfasında ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b6324-152">Add a few tasks in hello page.</span></span>

![PHP tooMySQL başarıyla bağlanır.](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="b6324-154">PHP, toostop yazın `Ctrl + C` hello terminal içinde.</span><span class="sxs-lookup"><span data-stu-id="b6324-154">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a><span data-ttu-id="b6324-155">MySQL oluşturma</span><span class="sxs-lookup"><span data-stu-id="b6324-155">Create MySQL in Azure</span></span>

<span data-ttu-id="b6324-156">Bu adımda oluşturduğunuz MySQL veritabanında [Azure veritabanı için MySQL (Önizleme)](/azure/mysql).</span><span class="sxs-lookup"><span data-stu-id="b6324-156">In this step, you create a MySQL database in [Azure Database for MySQL (Preview)](/azure/mysql).</span></span> <span data-ttu-id="b6324-157">Daha sonra hello PHP uygulama tooconnect toothis veritabanını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b6324-157">Later, you configure hello PHP application tooconnect toothis database.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="b6324-158">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="b6324-158">Create a resource group</span></span>

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a><span data-ttu-id="b6324-159">MySQL sunucusu oluşturun</span><span class="sxs-lookup"><span data-stu-id="b6324-159">Create a MySQL server</span></span>

<span data-ttu-id="b6324-160">Bir sunucu Azure veritabanı'nda MySQL (Önizleme) ile Merhaba oluşturmak [az mysql sunucusu oluşturun](/cli/azure/mysql/server#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="b6324-160">Create a server in Azure Database for MySQL (Preview) with hello [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>

<span data-ttu-id="b6324-161">Hello hello gördüğünüz MySQL server adınızı alternatif komutu, aşağıdaki  _&lt;mysql_server_name >_ yer tutucu (geçerli karakterler `a-z`, `0-9`, ve `-`).</span><span class="sxs-lookup"><span data-stu-id="b6324-161">In hello following command, substitute your MySQL server name where you see hello _&lt;mysql_server_name>_ placeholder (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="b6324-162">Bu ad hello MySQL sunucunun ana bilgisayar adı bir parçasıdır (`<mysql_server_name>.database.windows.net`), toobe genel olarak benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b6324-162">This name is part of hello MySQL server's hostname  (`<mysql_server_name>.database.windows.net`), it needs toobe globally unique.</span></span>

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

<span data-ttu-id="b6324-163">Merhaba MySQL server oluşturulduğunda hello Azure CLI örnek aşağıdaki bilgileri benzer toohello gösterir:</span><span class="sxs-lookup"><span data-stu-id="b6324-163">When hello MySQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="configure-server-firewall"></a><span data-ttu-id="b6324-164">Sunucu Güvenlik Duvarı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b6324-164">Configure server firewall</span></span>

<span data-ttu-id="b6324-165">Bağlantılar için MySQL server tooallow istemcinizi hello kullanarak bir güvenlik duvarı kuralı oluşturun [az mysql server güvenlik duvarı kuralı oluşturmak](/cli/azure/mysql/server/firewall-rule#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="b6324-165">Create a firewall rule for your MySQL server tooallow client connections by using hello [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span>

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="b6324-166">Azure veritabanı için MySQL (Önizleme) şu anda bağlantıları yalnızca tooAzure Hizmetleri sınırlamak değil.</span><span class="sxs-lookup"><span data-stu-id="b6324-166">Azure Database for MySQL (Preview) doesn't currently limit connections only tooAzure services.</span></span> <span data-ttu-id="b6324-167">Dinamik olarak atanmış IP adresleri azure'da gibi daha iyi tooenable olan tüm IP adresleri.</span><span class="sxs-lookup"><span data-stu-id="b6324-167">As IP addresses in Azure are dynamically assigned, it is better tooenable all IP addresses.</span></span> <span data-ttu-id="b6324-168">Merhaba, önizlemede hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="b6324-168">hello service is in preview.</span></span> <span data-ttu-id="b6324-169">Veritabanınızın güvenliğini sağlamak için daha iyi yöntemleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b6324-169">Better methods for securing your database are planned.</span></span>
>
>

### <a name="connect-tooproduction-mysql-server-locally"></a><span data-ttu-id="b6324-170">Yerel olarak tooproduction MySQL server Bağlan</span><span class="sxs-lookup"><span data-stu-id="b6324-170">Connect tooproduction MySQL server locally</span></span>

<span data-ttu-id="b6324-171">Merhaba terminal penceresinde, azure'da toohello MySQL sunucusuna bağlanın.</span><span class="sxs-lookup"><span data-stu-id="b6324-171">In hello terminal window, connect toohello MySQL server in Azure.</span></span> <span data-ttu-id="b6324-172">Daha önce için belirttiğiniz başlangıç değeri kullanın  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="b6324-172">Use hello value you specified previously for _&lt;mysql_server_name>_.</span></span>

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

<span data-ttu-id="b6324-173">Kullanmak için bir parola istendiğinde, _tr0ngPa $$ w0rd!_, hello veritabanı oluşturduğunuzda belirttiğiniz.</span><span class="sxs-lookup"><span data-stu-id="b6324-173">When prompted for a password, use _$tr0ngPa$w0rd!_, which you specified when you created hello database.</span></span>

### <a name="create-a-production-database"></a><span data-ttu-id="b6324-174">Bir üretim veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b6324-174">Create a production database</span></span>

<span data-ttu-id="b6324-175">Merhaba, `mysql` isteminde, bir veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b6324-175">At hello `mysql` prompt, create a database.</span></span>

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="b6324-176">İzinleri olan bir kullanıcı oluşturun</span><span class="sxs-lookup"><span data-stu-id="b6324-176">Create a user with permissions</span></span>

<span data-ttu-id="b6324-177">Adlı bir veritabanı kullanıcısı oluşturmalıdır _phpappuser_ ve hello tüm ayrıcalıkları vermek `sampledb` veritabanı.</span><span class="sxs-lookup"><span data-stu-id="b6324-177">Create a database user called _phpappuser_ and give it all privileges in hello `sampledb` database.</span></span>

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* too'phpappuser';
```

<span data-ttu-id="b6324-178">Exit hello sunucu bağlantısı yazarak `quit`.</span><span class="sxs-lookup"><span data-stu-id="b6324-178">Exit hello server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="connect-app-tooazure-mysql"></a><span data-ttu-id="b6324-179">Uygulama tooAzure MySQL Bağlan</span><span class="sxs-lookup"><span data-stu-id="b6324-179">Connect app tooAzure MySQL</span></span>

<span data-ttu-id="b6324-180">Bu adımda, Azure veritabanı'nda MySQL (Önizleme) için oluşturulan hello PHP uygulama toohello MySQL veritabanını bağlayın.</span><span class="sxs-lookup"><span data-stu-id="b6324-180">In this step, you connect hello PHP application toohello MySQL database you created in Azure Database for MySQL (Preview).</span></span>

<a name="devconfig"></a>

### <a name="configure-hello-database-connection"></a><span data-ttu-id="b6324-181">Merhaba veritabanı bağlantısını yapılandır</span><span class="sxs-lookup"><span data-stu-id="b6324-181">Configure hello database connection</span></span>

<span data-ttu-id="b6324-182">Merhaba depo kök dizininde oluşturma bir _. env.production_ değişkenleri içine aşağıdaki dosya ve kopyalama hello.</span><span class="sxs-lookup"><span data-stu-id="b6324-182">In hello repository root, create an _.env.production_ file and copy hello following variables into it.</span></span> <span data-ttu-id="b6324-183">Merhaba yer tutucu Değiştir  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="b6324-183">Replace hello placeholder _&lt;mysql_server_name>_.</span></span>

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

<span data-ttu-id="b6324-184">Merhaba değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b6324-184">Save hello changes.</span></span>

> [!TIP]
> <span data-ttu-id="b6324-185">MySQL bağlantı bilgilerinizi, bu dosya zaten hello Git deposundan dışarıda toosecure (bkz _.gitignore_ hello depo kök).</span><span class="sxs-lookup"><span data-stu-id="b6324-185">toosecure your MySQL connection information, this file is already excluded from hello Git repository (See _.gitignore_ in hello repository root).</span></span> <span data-ttu-id="b6324-186">Daha sonra uygulama hizmeti tooconnect tooyour tooconfigure ortam değişkenleri Azure veritabanı'nda MySQL (Önizleme) nasıl veritabanı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="b6324-186">Later, you learn how tooconfigure environment variables in App Service tooconnect tooyour database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="b6324-187">Ortam değişkenleri ile Merhaba gerekmeyen *.env* uygulama hizmeti dosyasında.</span><span class="sxs-lookup"><span data-stu-id="b6324-187">With environment variables, you don't need hello *.env* file in App Service.</span></span>
>

### <a name="configure-ssl-certificate"></a><span data-ttu-id="b6324-188">SSL sertifikası yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b6324-188">Configure SSL certificate</span></span>

<span data-ttu-id="b6324-189">Varsayılan olarak, Azure veritabanı için MySQL istemcilerden gelen SSL bağlantıları zorlar.</span><span class="sxs-lookup"><span data-stu-id="b6324-189">By default, Azure Database for MySQL enforces SSL connections from clients.</span></span> <span data-ttu-id="b6324-190">tooconnect tooyour MySQL veritabanında Azure kullanmalıdır bir _.pem_ SSL sertifikası.</span><span class="sxs-lookup"><span data-stu-id="b6324-190">tooconnect tooyour MySQL database in Azure, you must use a _.pem_ SSL certificate.</span></span>

<span data-ttu-id="b6324-191">Açık _config/database.php_ ve hello ekleyin _sslmode_ ve _seçenekleri_ parametreler çok`connections.mysql`hello kod aşağıdaki gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="b6324-191">Open _config/database.php_ and add hello _sslmode_ and _options_ parameters too`connections.mysql`, as shown in hello following code.</span></span>

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

<span data-ttu-id="b6324-192">toolearn nasıl toogenerate bu _certificate.pem_, bkz: [yapılandırma SSL bağlantısı'nda uygulama toosecurely bağlanmak tooAzure veritabanı için MySQL](../mysql/howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="b6324-192">toolearn how toogenerate this _certificate.pem_, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](../mysql/howto-configure-ssl.md).</span></span>

> [!TIP]
> <span data-ttu-id="b6324-193">Merhaba yolu _/ssl/certificate.pem_ işaret tooan varolan _certificate.pem_ hello Git deposu dosyasında.</span><span class="sxs-lookup"><span data-stu-id="b6324-193">hello path _/ssl/certificate.pem_ points tooan existing _certificate.pem_ file in hello Git repository.</span></span> <span data-ttu-id="b6324-194">Bu dosya, bu öğreticide kolaylık sağlaması açısından sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="b6324-194">This file is provided for convenience in this tutorial.</span></span> <span data-ttu-id="b6324-195">En iyi yöntem yürüttükten değil, _.pem_ kaynak denetimine sertifikalar.</span><span class="sxs-lookup"><span data-stu-id="b6324-195">For best practice, you should not commit your _.pem_ certificates into source control.</span></span> 
>

### <a name="test-hello-application-locally"></a><span data-ttu-id="b6324-196">Merhaba uygulamayı yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="b6324-196">Test hello application locally</span></span>

<span data-ttu-id="b6324-197">Laravel veritabanı geçişler ile Çalıştır _. env.production_ (Önizleme) MySQL için ortam dosya toocreate hello MySQL veritabanınızı Azure veritabanında tablolarda hello gibi.</span><span class="sxs-lookup"><span data-stu-id="b6324-197">Run Laravel database migrations with _.env.production_ as hello environment file toocreate hello tables in your MySQL database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="b6324-198">Unutmayın _. env.production_ Azure'da hello bağlantı bilgileri tooyour MySQL veritabanı vardır.</span><span class="sxs-lookup"><span data-stu-id="b6324-198">Remember that _.env.production_ has hello connection information tooyour MySQL database in Azure.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="b6324-199">_. env.production_ geçerli uygulama anahtarı henüz yok.</span><span class="sxs-lookup"><span data-stu-id="b6324-199">_.env.production_ doesn't have a valid application key yet.</span></span> <span data-ttu-id="b6324-200">Merhaba terminal daha yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b6324-200">Generate a new one for it in hello terminal.</span></span>

```bash
php artisan key:generate --env=production --force
```

<span data-ttu-id="b6324-201">Merhaba örnek uygulaması ile Çalıştır _. env.production_ hello ortam dosyası olarak.</span><span class="sxs-lookup"><span data-stu-id="b6324-201">Run hello sample application with _.env.production_ as hello environment file.</span></span>

```bash
php artisan serve --env=production
```

<span data-ttu-id="b6324-202">Çok gidin`http://localhost:8000`.</span><span class="sxs-lookup"><span data-stu-id="b6324-202">Navigate too`http://localhost:8000`.</span></span> <span data-ttu-id="b6324-203">Hello sayfa hatasız yüklerse hello PHP uygulaması Azure toohello MySQL veritabanına bağlanıyor.</span><span class="sxs-lookup"><span data-stu-id="b6324-203">If hello page loads without errors, hello PHP application is connecting toohello MySQL database in Azure.</span></span>

<span data-ttu-id="b6324-204">Bazı görevleri hello sayfasında ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b6324-204">Add a few tasks in hello page.</span></span>

![PHP tooAzure veritabanı için MySQL (Önizleme) başarıyla bağlanır.](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="b6324-206">PHP, toostop yazın `Ctrl + C` hello terminal içinde.</span><span class="sxs-lookup"><span data-stu-id="b6324-206">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

### <a name="commit-your-changes"></a><span data-ttu-id="b6324-207">Değişikliklerinizi uygulamak</span><span class="sxs-lookup"><span data-stu-id="b6324-207">Commit your changes</span></span>

<span data-ttu-id="b6324-208">Git komutları toocommit aşağıdaki hello değişikliklerinizi çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b6324-208">Run hello following Git commands toocommit your changes:</span></span>

```bash
git add .
git commit -m "database.php updates"
```

<span data-ttu-id="b6324-209">Uygulamanızı dağıtılan hazır toobe ' dir.</span><span class="sxs-lookup"><span data-stu-id="b6324-209">Your app is ready toobe deployed.</span></span>

## <a name="deploy-tooazure"></a><span data-ttu-id="b6324-210">TooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="b6324-210">Deploy tooAzure</span></span>

<span data-ttu-id="b6324-211">Bu adımda, hello MySQL bağlı PHP uygulama tooAzure uygulama hizmeti dağıtın.</span><span class="sxs-lookup"><span data-stu-id="b6324-211">In this step, you deploy hello MySQL-connected PHP application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="b6324-212">App Service planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b6324-212">Create an App Service plan</span></span>

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a><span data-ttu-id="b6324-213">Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="b6324-213">Create a web app</span></span>

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-hello-php-version"></a><span data-ttu-id="b6324-214">Set hello PHP sürümü</span><span class="sxs-lookup"><span data-stu-id="b6324-214">Set hello PHP version</span></span>

<span data-ttu-id="b6324-215">Uygulama hello kümesi hello PHP sürümünü gerektirir hello kullanarak [az webapp yapılandırma kümesi](/cli/azure/webapp/config#set) komutu.</span><span class="sxs-lookup"><span data-stu-id="b6324-215">Set hello PHP version that hello application requires by using hello [az webapp config set](/cli/azure/webapp/config#set) command.</span></span>

<span data-ttu-id="b6324-216">Merhaba aşağıdaki komut hello PHP sürümü too_7.0_ ayarlar.</span><span class="sxs-lookup"><span data-stu-id="b6324-216">hello following command sets hello PHP version too_7.0_.</span></span>

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a><span data-ttu-id="b6324-217">Veritabanı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b6324-217">Configure database settings</span></span>

<span data-ttu-id="b6324-218">Daha önce işaret edildiği gibi App Service'te ortam değişkenlerini kullanma tooyour Azure MySQL veritabanı bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="b6324-218">As pointed out previously, you can connect tooyour Azure MySQL database using environment variables in App Service.</span></span>

<span data-ttu-id="b6324-219">Ortam değişkenleri olarak ayarladığınız App Service'te _uygulama ayarları_ hello kullanarak [az webapp config appsettings kümesi](/cli/azure/webapp/config/appsettings#set) komutu.</span><span class="sxs-lookup"><span data-stu-id="b6324-219">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span>

<span data-ttu-id="b6324-220">Merhaba aşağıdaki komutu hello uygulama ayarlarını yapılandırır `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, ve `DB_PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="b6324-220">hello following command configures hello app settings `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD`.</span></span> <span data-ttu-id="b6324-221">Merhaba yer tutucuları değiştirmek  _&lt;uygulamaadı >_ ve  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="b6324-221">Replace hello placeholders _&lt;appname>_ and _&lt;mysql_server_name>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

<span data-ttu-id="b6324-222">Merhaba PHP kullanabilirsiniz [getenv](http://www.php.net/manual/function.getenv.php) yöntemi tooaccess hello ayarları.</span><span class="sxs-lookup"><span data-stu-id="b6324-222">You can use hello PHP [getenv](http://www.php.net/manual/function.getenv.php) method tooaccess hello settings.</span></span> <span data-ttu-id="b6324-223">Merhaba Laravel kodu kullanan bir [env](https://laravel.com/docs/5.4/helpers#method-env) sarmalayıcı hello PHP üzerinden `getenv`.</span><span class="sxs-lookup"><span data-stu-id="b6324-223">hello Laravel code uses an [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper over hello PHP `getenv`.</span></span> <span data-ttu-id="b6324-224">Örneğin, hello MySQL yapılandırmasında _config/database.php_ hello kod aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="b6324-224">For example, hello MySQL configuration in _config/database.php_ looks like hello following code:</span></span>

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

### <a name="configure-laravel-environment-variables"></a><span data-ttu-id="b6324-225">Laravel ortam değişkenlerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="b6324-225">Configure Laravel environment variables</span></span>

<span data-ttu-id="b6324-226">Laravel App Service'te bir uygulama anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="b6324-226">Laravel needs an application key in App Service.</span></span> <span data-ttu-id="b6324-227">Uygulama ayarları ile yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6324-227">You can configure it with app settings.</span></span>

<span data-ttu-id="b6324-228">Kullanım `php artisan` toogenerate too_.env_ kaydetmeden yeni bir uygulama anahtarı.</span><span class="sxs-lookup"><span data-stu-id="b6324-228">Use `php artisan` toogenerate a new application key without saving it too_.env_.</span></span>

```bash
php artisan key:generate --show
```

<span data-ttu-id="b6324-229">Merhaba uygulama anahtarı hello App Service web uygulaması hello kullanarak ayarlamak [az webapp config appsettings kümesi](/cli/azure/webapp/config/appsettings#set) komutu.</span><span class="sxs-lookup"><span data-stu-id="b6324-229">Set hello application key in hello App Service web app by using hello [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span> <span data-ttu-id="b6324-230">Merhaba yer tutucuları değiştirmek  _&lt;uygulamaadı >_ ve  _&lt;outputofphpartisankey: Oluştur >_.</span><span class="sxs-lookup"><span data-stu-id="b6324-230">Replace hello placeholders _&lt;appname>_ and _&lt;outputofphpartisankey:generate>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

<span data-ttu-id="b6324-231">`APP_DEBUG="true"`Merhaba web uygulaması dağıtıldığında Laravel tooreturn hata ayıklama bilgilerini hatayla karşılaştığında söyler.</span><span class="sxs-lookup"><span data-stu-id="b6324-231">`APP_DEBUG="true"` tells Laravel tooreturn debugging information when hello deployed web app encounters errors.</span></span> <span data-ttu-id="b6324-232">Bir üretim uygulaması çalışırken çok ayarlamak`false`, daha güvenli olduğu.</span><span class="sxs-lookup"><span data-stu-id="b6324-232">When running a production application, set it too`false`, which is more secure.</span></span>

### <a name="set-hello-virtual-application-path"></a><span data-ttu-id="b6324-233">Merhaba sanal uygulama yolu ayarla</span><span class="sxs-lookup"><span data-stu-id="b6324-233">Set hello virtual application path</span></span>

<span data-ttu-id="b6324-234">Merhaba sanal uygulama yolu hello web uygulaması için ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b6324-234">Set hello virtual application path for hello web app.</span></span> <span data-ttu-id="b6324-235">Bu adım gereklidir çünkü hello [Laravel uygulama yaşam döngüsü](https://laravel.com/docs/5.4/lifecycle) hello başlar _ortak_ hello uygulamanızın kök dizininde yerine dizin.</span><span class="sxs-lookup"><span data-stu-id="b6324-235">This step is required because hello [Laravel application lifecycle](https://laravel.com/docs/5.4/lifecycle) begins in hello _public_ directory instead of hello application's root directory.</span></span> <span data-ttu-id="b6324-236">Diğer PHP çerçeveleri, yaşam döngüsünü başlatma hello kök dizininde hello sanal uygulama yolu el ile yapılandırma olmadan çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="b6324-236">Other PHP frameworks whose lifecycle start in hello root directory can work without manual configuration of hello virtual application path.</span></span>

<span data-ttu-id="b6324-237">Hello kullanarak hello sanal uygulama yolu ayarla [az kaynak güncelleştirme](/cli/azure/resource#update) komutu.</span><span class="sxs-lookup"><span data-stu-id="b6324-237">Set hello virtual application path by using hello [az resource update](/cli/azure/resource#update) command.</span></span> <span data-ttu-id="b6324-238">Hello yerine  _&lt;uygulamaadı >_ yer tutucu.</span><span class="sxs-lookup"><span data-stu-id="b6324-238">Replace hello _&lt;appname>_ placeholder.</span></span>

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

<span data-ttu-id="b6324-239">Varsayılan olarak, Azure App Service hello kök sanal uygulama yolu işaret (_/_) toohello kök dizini hello dağıtılan uygulama dosyaları (_sites\wwwroot_).</span><span class="sxs-lookup"><span data-stu-id="b6324-239">By default, Azure App Service points hello root virtual application path (_/_) toohello root directory of hello deployed application files (_sites\wwwroot_).</span></span>

### <a name="configure-a-deployment-user"></a><span data-ttu-id="b6324-240">Dağıtım kullanıcısı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b6324-240">Configure a deployment user</span></span>

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a><span data-ttu-id="b6324-241">Yerel Git dağıtımını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b6324-241">Configure local Git deployment</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-tooazure-from-git"></a><span data-ttu-id="b6324-242">Anında iletme tooAzure Git</span><span class="sxs-lookup"><span data-stu-id="b6324-242">Push tooAzure from Git</span></span>

<span data-ttu-id="b6324-243">Bir Azure uzak tooyour yerel Git deposu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b6324-243">Add an Azure remote tooyour local Git repository.</span></span>

```bash
git remote add azure <paste_copied_url_here>
```

<span data-ttu-id="b6324-244">Toohello Azure uzak toodeploy Merhaba PHP uygulaması iletin.</span><span class="sxs-lookup"><span data-stu-id="b6324-244">Push toohello Azure remote toodeploy hello PHP application.</span></span> <span data-ttu-id="b6324-245">Merhaba dağıtım kullanıcının hello oluşturmanın bir parçası daha önce sağlanan hello parola istenir.</span><span class="sxs-lookup"><span data-stu-id="b6324-245">You are prompted for hello password you supplied earlier as part of hello creation of hello deployment user.</span></span>

```bash
git push azure master
```

<span data-ttu-id="b6324-246">Dağıtım sırasında Azure App Service, ilerleme durumunu Git ile iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="b6324-246">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 3, done.
Delta compression using up too8 threads.
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
> <span data-ttu-id="b6324-247">Merhaba dağıtım işlemi yükleyeceğini karşılaşabilirsiniz [Oluşturucu](https://getcomposer.org/) hello sonunda paketler.</span><span class="sxs-lookup"><span data-stu-id="b6324-247">You may notice that hello deployment process installs [Composer](https://getcomposer.org/) packages at hello end.</span></span> <span data-ttu-id="b6324-248">Uygulama hizmeti bu otomasyonlara varsayılan dağıtımı sırasında çalışmaz, bu örnek depo üç nedenle ek kendi kök dizin tooenable, dosyalarını:</span><span class="sxs-lookup"><span data-stu-id="b6324-248">App Service does not run these automations during default deployment, so this sample repository has three additional files in its root directory tooenable it:</span></span>
>
> - <span data-ttu-id="b6324-249">`.deployment`-Uygulama hizmeti toorun bu dosya söyler `bash deploy.sh` hello özel dağıtım komut dosyası olarak.</span><span class="sxs-lookup"><span data-stu-id="b6324-249">`.deployment` - This file tells App Service toorun `bash deploy.sh` as hello custom deployment script.</span></span>
> - <span data-ttu-id="b6324-250">`deploy.sh`-hello özel dağıtım komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="b6324-250">`deploy.sh` - hello custom deployment script.</span></span> <span data-ttu-id="b6324-251">Merhaba dosya gözden geçirirseniz, çalıştığını görürsünüz `php composer.phar install` sonra `npm install`.</span><span class="sxs-lookup"><span data-stu-id="b6324-251">If you review hello file, you will see that it runs `php composer.phar install` after `npm install`.</span></span>
> - <span data-ttu-id="b6324-252">`composer.phar`-hello Oluşturucu Paket Yöneticisi.</span><span class="sxs-lookup"><span data-stu-id="b6324-252">`composer.phar` - hello Composer package manager.</span></span>
>
> <span data-ttu-id="b6324-253">Bu yaklaşım tooadd herhangi adım tooyour Git tabanlı dağıtım tooApp hizmetini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6324-253">You can use this approach tooadd any step tooyour Git-based deployment tooApp Service.</span></span> <span data-ttu-id="b6324-254">Daha fazla bilgi için bkz: [özel dağıtım betiği](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span><span class="sxs-lookup"><span data-stu-id="b6324-254">For more information, see [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span></span>
>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="b6324-255">Toohello Azure web uygulaması Gözat</span><span class="sxs-lookup"><span data-stu-id="b6324-255">Browse toohello Azure web app</span></span>

<span data-ttu-id="b6324-256">Çok Gözat`http://<app_name>.azurewebsites.net` ve birkaç görevleri toohello listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b6324-256">Browse too`http://<app_name>.azurewebsites.net` and add a few tasks toohello list.</span></span>

![Azure uygulama Hizmeti'nde çalışan PHP uygulaması](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

<span data-ttu-id="b6324-258">Tebrikler, Azure App Service'te bir veri güdümlü PHP uygulaması çalıştırıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="b6324-258">Congratulations, you're running a data-driven PHP app in Azure App Service.</span></span>

## <a name="update-model-locally-and-redeploy"></a><span data-ttu-id="b6324-259">Modeli yerel olarak güncelleştirin ve yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="b6324-259">Update model locally and redeploy</span></span>

<span data-ttu-id="b6324-260">Bu adımda, bir basit değişiklik toohello yaptığınız `task` veri modeli ve webapp hello ve hello güncelleştirme tooAzure yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="b6324-260">In this step, you make a simple change toohello `task` data model and hello webapp, and then publish hello update tooAzure.</span></span>

<span data-ttu-id="b6324-261">Merhaba görevler senaryo için bir görev tamamlandı olarak işaretleyebilirsiniz şekilde hello uygulama değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b6324-261">For hello tasks scenario, you modify hello application so that you can mark a task as complete.</span></span>

### <a name="add-a-column"></a><span data-ttu-id="b6324-262">Bir sütun ekleyin</span><span class="sxs-lookup"><span data-stu-id="b6324-262">Add a column</span></span>

<span data-ttu-id="b6324-263">Hello terminal, hello Git deposu toohello köküne gidin.</span><span class="sxs-lookup"><span data-stu-id="b6324-263">In hello terminal, navigate toohello root of hello Git repository.</span></span>

<span data-ttu-id="b6324-264">Hello için yeni bir veritabanı geçiş oluşturmayı `tasks` tablosu:</span><span class="sxs-lookup"><span data-stu-id="b6324-264">Generate a new database migration for hello `tasks` table:</span></span>

```bash
php artisan make:migration add_complete_column --table=tasks
```

<span data-ttu-id="b6324-265">Bu komut oluşturulan hello geçiş dosyasının adı hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="b6324-265">This command shows you hello name of hello migration file that's generated.</span></span> <span data-ttu-id="b6324-266">Bu dosyada Bul _veritabanı/geçişler_ ve açın.</span><span class="sxs-lookup"><span data-stu-id="b6324-266">Find this file in _database/migrations_ and open it.</span></span>

<span data-ttu-id="b6324-267">Hello yerine `up` koddan hello yöntemiyle:</span><span class="sxs-lookup"><span data-stu-id="b6324-267">Replace hello `up` method with hello following code:</span></span>

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

<span data-ttu-id="b6324-268">Merhaba önceki kod bir boolean sütun hello ekler `tasks` adlı bir tablo `complete`.</span><span class="sxs-lookup"><span data-stu-id="b6324-268">hello preceding code adds a boolean column in hello `tasks` table called `complete`.</span></span>

<span data-ttu-id="b6324-269">Hello yerine `down` hello geri alma eylemi için kod aşağıdaki hello yöntemiyle:</span><span class="sxs-lookup"><span data-stu-id="b6324-269">Replace hello `down` method with hello following code for hello rollback action:</span></span>

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

<span data-ttu-id="b6324-270">Hello terminal, Laravel veritabanı geçişler toomake hello değişikliği hello yerel veritabanında çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b6324-270">In hello terminal, run Laravel database migrations toomake hello change in hello local database.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="b6324-271">Merhaba üzerinde temel [Laravel adlandırma kuralı](https://laravel.com/docs/5.4/eloquent#defining-models), hello modeli `Task` (bkz _app/Task.php_) toohello eşlemeleri `tasks` varsayılan olarak tablo.</span><span class="sxs-lookup"><span data-stu-id="b6324-271">Based on hello [Laravel naming convention](https://laravel.com/docs/5.4/eloquent#defining-models), hello model `Task` (see _app/Task.php_) maps toohello `tasks` table by default.</span></span>

### <a name="update-application-logic"></a><span data-ttu-id="b6324-272">Uygulama mantığını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="b6324-272">Update application logic</span></span>

<span data-ttu-id="b6324-273">Açık hello *routes/web.php* dosya.</span><span class="sxs-lookup"><span data-stu-id="b6324-273">Open hello *routes/web.php* file.</span></span> <span data-ttu-id="b6324-274">Merhaba uygulaması kendi yollar ve iş mantığı buraya tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b6324-274">hello application defines its routes and business logic here.</span></span>

<span data-ttu-id="b6324-275">Merhaba dosya Hello sonunda koddan hello ile bir rota ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b6324-275">At hello end of hello file, add a route with hello following code:</span></span>

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

<span data-ttu-id="b6324-276">Merhaba önceki kod basit güncelleştirme toohello veri modeli hello değerini değiştirerek yapar `complete`.</span><span class="sxs-lookup"><span data-stu-id="b6324-276">hello preceding code makes a simple update toohello data model by toggling hello value of `complete`.</span></span>

### <a name="update-hello-view"></a><span data-ttu-id="b6324-277">Merhaba görünümünü güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="b6324-277">Update hello view</span></span>

<span data-ttu-id="b6324-278">Açık hello *resources/views/tasks.blade.php* dosya.</span><span class="sxs-lookup"><span data-stu-id="b6324-278">Open hello *resources/views/tasks.blade.php* file.</span></span> <span data-ttu-id="b6324-279">Hello bulur `<tr>` açma etiketi ve ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b6324-279">Find hello `<tr>` opening tag and replace it with:</span></span>

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

<span data-ttu-id="b6324-280">Merhaba görev tam olup olmamasına bağlı olarak kod değişiklikleri hello satır rengi önceki hello.</span><span class="sxs-lookup"><span data-stu-id="b6324-280">hello preceding code changes hello row color depending on whether hello task is complete.</span></span>

<span data-ttu-id="b6324-281">Merhaba sonraki satırda, kod aşağıdaki hello vardır:</span><span class="sxs-lookup"><span data-stu-id="b6324-281">In hello next line, you have hello following code:</span></span>

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

<span data-ttu-id="b6324-282">Merhaba tüm satırı koddan hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b6324-282">Replace hello entire line with hello following code:</span></span>

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

<span data-ttu-id="b6324-283">Merhaba önceki kod daha önce tanımlanan hello rota başvuran hello Gönder düğmesi ekler.</span><span class="sxs-lookup"><span data-stu-id="b6324-283">hello preceding code adds hello submit button that references hello route that you defined earlier.</span></span>

### <a name="test-hello-changes-locally"></a><span data-ttu-id="b6324-284">Yerel olarak test hello değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="b6324-284">Test hello changes locally</span></span>

<span data-ttu-id="b6324-285">Merhaba Git deposu, Hello kök dizinindeki hello geliştirme sunucusu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b6324-285">From hello root directory of hello Git repository, run hello development server.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="b6324-286">toosee hello görev durumu değişikliği, çok gidin`http://localhost:8000` ve select hello onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="b6324-286">toosee hello task status change, navigate too`http://localhost:8000` and select hello checkbox.</span></span>

![Eklenen onay kutusunu tootask](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

<span data-ttu-id="b6324-288">PHP, toostop yazın `Ctrl + C` hello terminal içinde.</span><span class="sxs-lookup"><span data-stu-id="b6324-288">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

### <a name="publish-changes-tooazure"></a><span data-ttu-id="b6324-289">Değişiklikleri tooAzure yayımlama</span><span class="sxs-lookup"><span data-stu-id="b6324-289">Publish changes tooAzure</span></span>

<span data-ttu-id="b6324-290">Hello terminal, Laravel veritabanı geçişler hello üretim bağlantı dizesi toomake hello değişikliği hello Azure veritabanı ile çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b6324-290">In hello terminal, run Laravel database migrations with hello production connection string toomake hello change in hello Azure database.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="b6324-291">Git tüm hello değişiklikleri kaydetmek ve hello kod değişiklikleri tooAzure anında iletme.</span><span class="sxs-lookup"><span data-stu-id="b6324-291">Commit all hello changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

<span data-ttu-id="b6324-292">Bir kez hello `git push` tamamlamak ise toohello Azure web uygulaması ve test hello yeni işlevsellik gidin.</span><span class="sxs-lookup"><span data-stu-id="b6324-292">Once hello `git push` is complete, navigate toohello Azure web app and test hello new functionality.</span></span>

![Model ve veritabanı değişikliklerini tooAzure yayımlanan](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="b6324-294">Herhangi bir görevi eklediyseniz bunlar hello veritabanında tutulur.</span><span class="sxs-lookup"><span data-stu-id="b6324-294">If you added any tasks, they are retained in hello database.</span></span> <span data-ttu-id="b6324-295">Güncelleştirmeleri toohello veri şeması bırakın mevcut verileri kalır.</span><span class="sxs-lookup"><span data-stu-id="b6324-295">Updates toohello data schema leave existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="b6324-296">Akış tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="b6324-296">Stream diagnostic logs</span></span>

<span data-ttu-id="b6324-297">Merhaba PHP uygulaması Azure App Service'te çalışırken hello konsol günlükleri yöneltilen tooyour terminal elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6324-297">While hello PHP application runs in Azure App Service, you can get hello console logs piped tooyour terminal.</span></span> <span data-ttu-id="b6324-298">Bu şekilde hello aynı tanılama iletileri alabilirsiniz uygulama hatalarını hata ayıklama toohelp.</span><span class="sxs-lookup"><span data-stu-id="b6324-298">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="b6324-299">Akış, kullanım hello toostart günlük [az webapp günlük tail](/cli/azure/webapp/log#tail) komutu.</span><span class="sxs-lookup"><span data-stu-id="b6324-299">toostart log streaming, use hello [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

<span data-ttu-id="b6324-300">Günlük akış başladıktan sonra bazı web trafiği hello tarayıcı tooget hello Azure web uygulamasında yenileyin.</span><span class="sxs-lookup"><span data-stu-id="b6324-300">Once log streaming has started, refresh hello Azure web app in hello browser tooget some web traffic.</span></span> <span data-ttu-id="b6324-301">Konsol günlükleri yöneltilen toohello terminal şimdi görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6324-301">You can now see console logs piped toohello terminal.</span></span> <span data-ttu-id="b6324-302">Konsol günlükleri hemen görmüyorsanız, 30 saniye içinde yeniden kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="b6324-302">If you don't see console logs immediately, check again in 30 seconds.</span></span>

<span data-ttu-id="b6324-303">istediğiniz zaman, akış toostop günlük türü `Ctrl` + `C`.</span><span class="sxs-lookup"><span data-stu-id="b6324-303">toostop log streaming at anytime, type `Ctrl`+`C`.</span></span>

> [!TIP]
> <span data-ttu-id="b6324-304">Bir PHP uygulaması hello standart kullanabilir [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello konsol.</span><span class="sxs-lookup"><span data-stu-id="b6324-304">A PHP application can use hello standard [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello console.</span></span> <span data-ttu-id="b6324-305">Merhaba örnek uygulama bu yaklaşımı kullanır _app/Http/routes.php_.</span><span class="sxs-lookup"><span data-stu-id="b6324-305">hello sample application uses this approach in _app/Http/routes.php_.</span></span>
>
> <span data-ttu-id="b6324-306">Bir web çerçevesidir olarak [Laravel kullanan Monolog](https://laravel.com/docs/5.4/errors) hello oturum açma sağlayıcısı olarak.</span><span class="sxs-lookup"><span data-stu-id="b6324-306">As a web framework, [Laravel uses Monolog](https://laravel.com/docs/5.4/errors) as hello logging provider.</span></span> <span data-ttu-id="b6324-307">toosee tooget Monolog toooutput toohello konsol iletileri nasıl bkz [PHP: nasıl toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span><span class="sxs-lookup"><span data-stu-id="b6324-307">toosee how tooget Monolog toooutput messages toohello console, see [PHP: How toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span></span>
>
>

## <a name="manage-hello-azure-web-app"></a><span data-ttu-id="b6324-308">Hello Azure web uygulaması yönetme</span><span class="sxs-lookup"><span data-stu-id="b6324-308">Manage hello Azure web app</span></span>

<span data-ttu-id="b6324-309">Toohello Git [Azure portal](https://portal.azure.com) oluşturduğunuz toomanage hello web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="b6324-309">Go toohello [Azure portal](https://portal.azure.com) toomanage hello web app you created.</span></span>

<span data-ttu-id="b6324-310">Merhaba sol menüden **uygulama hizmetleri**ve ardından, Azure web uygulamanızın hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b6324-310">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Portal Gezinti tooAzure web uygulaması](./media/app-service-web-tutorial-php-mysql/access-portal.png)

<span data-ttu-id="b6324-312">Web uygulamanızın Genel Bakış sayfasını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b6324-312">You see your web app's Overview page.</span></span> <span data-ttu-id="b6324-313">Burada, Durdur, Başlat, yeniden başlatma, Gözat ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6324-313">Here, you can perform basic management tasks like  stop, start, restart, browse, and delete.</span></span>

<span data-ttu-id="b6324-314">Merhaba soldaki menüden, uygulamanızı yapılandırmak için sayfaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="b6324-314">hello left menu provides pages for configuring your app.</span></span>

![Azure portalında App Service sayfası](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="b6324-316">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b6324-316">Next steps</span></span>

<span data-ttu-id="b6324-317">Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="b6324-317">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b6324-318">Azure üzerinde MySQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b6324-318">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="b6324-319">PHP uygulama tooMySQL Bağlan</span><span class="sxs-lookup"><span data-stu-id="b6324-319">Connect a PHP app tooMySQL</span></span>
> * <span data-ttu-id="b6324-320">Merhaba uygulama tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="b6324-320">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="b6324-321">Merhaba veri modeli güncelleştirmek ve hello uygulama yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="b6324-321">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="b6324-322">Azure Stream tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="b6324-322">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="b6324-323">Merhaba uygulamada hello Azure portalı Yönet</span><span class="sxs-lookup"><span data-stu-id="b6324-323">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="b6324-324">İlerlemek toohello sonraki öğretici toolearn nasıl toomap özel DNS ad tooa web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="b6324-324">Advance toohello next tutorial toolearn how toomap a custom DNS name tooa web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b6324-325">Harita bir var olan özel DNS adı tooAzure Web uygulamaları</span><span class="sxs-lookup"><span data-stu-id="b6324-325">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
