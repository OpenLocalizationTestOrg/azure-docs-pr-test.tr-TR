---
title: "Veritabanı için PHP kullanarak PostgreSQL aaaConnect tooAzure | Microsoft Docs"
description: "Bu hızlı başlangıç PostgreSQL için Azure veritabanındaki verileri sorgulamak ve tooconnect için kullanabileceğiniz bir PHP kod örneğini sağlar."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: php
ms.topic: quickstart
ms.date: 06/29/2017
ms.openlocfilehash: 008505e837e37cb8c7fea3fc164b3446c3580e46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-php-tooconnect-and-query-data"></a><span data-ttu-id="ab35f-103">Azure veritabanı PostgreSQL için: kullanım PHP tooconnect ve sorgu verileri</span><span class="sxs-lookup"><span data-stu-id="ab35f-103">Azure Database for PostgreSQL: Use PHP tooconnect and query data</span></span>
<span data-ttu-id="ab35f-104">Bu hızlı başlangıç gösteren Azure tooconnect tooan veritabanı nasıl PostgreSQL kullanmak için bir [PHP](http://php.net/manual/intro-whatis.php) uygulama.</span><span class="sxs-lookup"><span data-stu-id="ab35f-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="ab35f-105">Nasıl toouse SQL deyimleri tooquery, Ekle, Güncelleştir ve hello veritabanında bulunan verileri silme gösterir.</span><span class="sxs-lookup"><span data-stu-id="ab35f-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="ab35f-106">Bu makale, yeni tooworking PostgreSQL için Azure veritabanıyla olan ancak bu, PHP, kullanarak geliştirme ile bildiğinizi varsayar.</span><span class="sxs-lookup"><span data-stu-id="ab35f-106">This article assumes you are familiar with development using PHP, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab35f-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ab35f-107">Prerequisites</span></span>
<span data-ttu-id="ab35f-108">Bu hızlı başlangıç Bu kılavuzlara birini başlangıç noktası olarak oluşturulan hello kaynakları kullanır:</span><span class="sxs-lookup"><span data-stu-id="ab35f-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="ab35f-109">DB Oluşturma - Portal</span><span class="sxs-lookup"><span data-stu-id="ab35f-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="ab35f-110">DB Oluşturma - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ab35f-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="ab35f-111">PHP’yi yükleme</span><span class="sxs-lookup"><span data-stu-id="ab35f-111">Install PHP</span></span>
<span data-ttu-id="ab35f-112">PHP’yi kendi sunucunuza yükleyin veya PHP içeren bir Azure [web uygulaması](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ab35f-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="windows"></a><span data-ttu-id="ab35f-113">Windows</span><span class="sxs-lookup"><span data-stu-id="ab35f-113">Windows</span></span>
- <span data-ttu-id="ab35f-114">[PHP 7.1.4 iş parçacığı güvenli olmayan (x64) sürümünü](http://windows.php.net/download#php-7.1) indirin</span><span class="sxs-lookup"><span data-stu-id="ab35f-114">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="ab35f-115">PHP yükleme ve toohello başvuran [PHP el ile](http://php.net/manual/install.windows.php) daha fazla yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ab35f-115">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>
- <span data-ttu-id="ab35f-116">Merhaba kodu kullanan hello **pgsql** hello PHP yükleme dahil sınıfı (ext/php_pgsql.dll).</span><span class="sxs-lookup"><span data-stu-id="ab35f-116">hello code uses hello **pgsql** class (ext/php_pgsql.dll)  that is included in hello PHP installation.</span></span> 
- <span data-ttu-id="ab35f-117">Etkin hello **pgsql** hello php.ini yapılandırma dosyası, genellikle konumundaki düzenleyerek uzantısı `C:\Program Files\PHP\v7.1\php.ini`.</span><span class="sxs-lookup"><span data-stu-id="ab35f-117">Enabled hello **pgsql** extension by editing hello php.ini configuration file, typically located at `C:\Program Files\PHP\v7.1\php.ini`.</span></span> <span data-ttu-id="ab35f-118">Merhaba yapılandırma dosyası hello metin içeren bir satır içermelidir `extension=php_pgsql.so`.</span><span class="sxs-lookup"><span data-stu-id="ab35f-118">hello configuration file should contain a line with hello text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="ab35f-119">Görüntülenmiyorsa, hello metin eklemek ve hello dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ab35f-119">If it is not shown, add hello text and save hello file.</span></span> <span data-ttu-id="ab35f-120">Merhaba metin varsa, ancak noktalı virgül önekiyle açıklamalı hello metin hello noktalı kaldırarak açıklamadan çıkarın.</span><span class="sxs-lookup"><span data-stu-id="ab35f-120">If hello text is present, but commented with a semicolon prefix, uncomment hello text by removing hello semicolon.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="ab35f-121">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="ab35f-121">Linux (Ubuntu)</span></span>
- <span data-ttu-id="ab35f-122">[PHP 7.1.4 iş parçacığı güvenli olmayan (x64) sürümünü](http://php.net/downloads.php) indirin</span><span class="sxs-lookup"><span data-stu-id="ab35f-122">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span> 
- <span data-ttu-id="ab35f-123">PHP yükleme ve toohello başvuran [PHP el ile](http://php.net/manual/install.unix.php) daha fazla yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ab35f-123">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>
- <span data-ttu-id="ab35f-124">Merhaba kodu kullanan hello **pgsql** sınıfı (php_pgsql.so).</span><span class="sxs-lookup"><span data-stu-id="ab35f-124">hello code uses hello **pgsql** class (php_pgsql.so).</span></span> <span data-ttu-id="ab35f-125">`sudo apt-get install php-pgsql` öğesini çalıştırarak yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ab35f-125">Install it by running `sudo apt-get install php-pgsql`.</span></span>
- <span data-ttu-id="ab35f-126">Etkin hello **pgsql** hello düzenleyerek uzantısı `/etc/php/7.0/mods-available/pgsql.ini` yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="ab35f-126">Enabled hello **pgsql** extension by editing hello `/etc/php/7.0/mods-available/pgsql.ini` configuration file.</span></span> <span data-ttu-id="ab35f-127">Merhaba yapılandırma dosyası hello metin içeren bir satır içermelidir `extension=php_pgsql.so`.</span><span class="sxs-lookup"><span data-stu-id="ab35f-127">hello configuration file should contain a line with hello text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="ab35f-128">Görüntülenmiyorsa, hello metin eklemek ve hello dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ab35f-128">If it is not shown, add hello text and save hello file.</span></span> <span data-ttu-id="ab35f-129">Merhaba metin varsa, ancak noktalı virgül önekiyle açıklamalı hello metin hello noktalı kaldırarak açıklamadan çıkarın.</span><span class="sxs-lookup"><span data-stu-id="ab35f-129">If hello text is present, but commented with a semicolon prefix, uncomment hello text by removing hello semicolon.</span></span>

### <a name="macos"></a><span data-ttu-id="ab35f-130">macOS</span><span class="sxs-lookup"><span data-stu-id="ab35f-130">MacOS</span></span>
- <span data-ttu-id="ab35f-131">[PHP 7.1.4 sürümünü](http://php.net/downloads.php) indirin</span><span class="sxs-lookup"><span data-stu-id="ab35f-131">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="ab35f-132">PHP yükleme ve toohello başvuran [PHP el ile](http://php.net/manual/install.macosx.php) daha fazla yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ab35f-132">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="ab35f-133">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="ab35f-133">Get connection information</span></span>
<span data-ttu-id="ab35f-134">Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure veritabanı için PostgreSQL alın.</span><span class="sxs-lookup"><span data-stu-id="ab35f-134">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="ab35f-135">Tam sunucu adını ve oturum açma kimlik bilgileri hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="ab35f-135">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="ab35f-136">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ab35f-136">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ab35f-137">Merhaba sol taraftaki menüden Azure portalında, **tüm kaynakları** ve oluşturduğunuz, gibi hello sunucu araması **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="ab35f-137">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="ab35f-138">Merhaba sunucu adına tıklatarak **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="ab35f-138">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="ab35f-139">Select hello sunucunun **genel bakış** sayfası.</span><span class="sxs-lookup"><span data-stu-id="ab35f-139">Select hello server's **Overview** page.</span></span> <span data-ttu-id="ab35f-140">Merhaba Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.</span><span class="sxs-lookup"><span data-stu-id="ab35f-140">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="ab35f-141">![PostgreSQL için Azure Veritabanı - Sunucu Yöneticisi Oturum Açma Bilgileri](./media/connect-php/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="ab35f-141">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-php/1-connection-string.png)</span></span>
5. <span data-ttu-id="ab35f-142">Sunucu oturum açma bilgilerinizi unutursanız, toohello gidin **genel bakış** tooview hello sunucu yönetici oturum açma adı sayfasında ve gerekirse sıfırlamak hello parola.</span><span class="sxs-lookup"><span data-stu-id="ab35f-142">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="ab35f-143">Bağlanma ve tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="ab35f-143">Connect and create a table</span></span>
<span data-ttu-id="ab35f-144">Kullanım hello aşağıdakileri tooconnect kod ve kullanarak bir tablo oluşturmak **CREATE TABLE** SQL deyimi, arkasından **INSERT INTO** SQL deyimleri tooadd satırları hello tabloya.</span><span class="sxs-lookup"><span data-stu-id="ab35f-144">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="ab35f-145">Merhaba kod arama yönteminde [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure PostgreSQL için veritabanı.</span><span class="sxs-lookup"><span data-stu-id="ab35f-145">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="ab35f-146">Yöntemini çağıran sonra [pg_query()](http://php.net/manual/en/function.pg-query.php) birkaç kez toorun çeşitli komutlar ve [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello ayrıntıları her zaman bir hata ortaya çıktıysa.</span><span class="sxs-lookup"><span data-stu-id="ab35f-146">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) several times toorun several commands, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred each time.</span></span> <span data-ttu-id="ab35f-147">Yöntem çağrıları sonra [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="ab35f-147">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="ab35f-148">Hello yerine `$host`, `$database`, `$user`, ve `$password` kendi değerlerinizi parametrelerle.</span><span class="sxs-lookup"><span data-stu-id="ab35f-148">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password") 
        or die("Failed toocreate connection toodatabase: ". pg_last_error(). "<br/>");
    print "Successfully created connection toodatabase.<br/>";

    // Drop previous table of same name if one exists.
    $query = "DROP TABLE IF EXISTS inventory;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    print "Finished dropping table (if existed).<br/>";

    // Create table.
    $query = "CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    print "Finished creating table.<br/>";

    // Insert some data into table.
    $name = '\'banana\'';
    $quantity = 150;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($1, $2);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");

    $name = '\'orange\'';
    $quantity = 154;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($name, $quantity);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");

    $name = '\'apple\'';
    $quantity = 100;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($name, $quantity);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error()). "<br/>";

    print "Inserted 3 rows of data.<br/>";

    // Closing connection
    pg_close($connection);
?>
```

## <a name="read-data"></a><span data-ttu-id="ab35f-149">Verileri okuma</span><span class="sxs-lookup"><span data-stu-id="ab35f-149">Read data</span></span>
<span data-ttu-id="ab35f-150">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **seçin** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="ab35f-150">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

 <span data-ttu-id="ab35f-151">Merhaba kod arama yönteminde [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure PostgreSQL için veritabanı.</span><span class="sxs-lookup"><span data-stu-id="ab35f-151">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="ab35f-152">Yöntemini çağıran sonra [pg_query()](http://php.net/manual/en/function.pg-query.php) hello sonuçları bir sonuç kümesinde tutma toorun hello SELECT komutu ve [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello ayrıntıları, bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="ab35f-152">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun hello SELECT command, keeping hello results in a result set, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span>  <span data-ttu-id="ab35f-153">tooread hello sonuç kümesi, yöntem [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) satır ve hello satır bir dizide verileri alındıktan sonra bir döngüde adlı `$row`, her dizi konumu sütunda her bir veri değerine sahip.</span><span class="sxs-lookup"><span data-stu-id="ab35f-153">tooread hello result set, method [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) is called in a loop, once per row, and hello row data is retrieved in an array `$row`, with one data value per column in each array position.</span></span>  <span data-ttu-id="ab35f-154">toofree hello sonuç kümesi, yöntem [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="ab35f-154">toofree hello result set, method [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) is called.</span></span> <span data-ttu-id="ab35f-155">Yöntem çağrıları sonra [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="ab35f-155">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="ab35f-156">Hello yerine `$host`, `$database`, `$user`, ve `$password` kendi değerlerinizi parametrelerle.</span><span class="sxs-lookup"><span data-stu-id="ab35f-156">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";
    
    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed toocreate connection toodatabase: ". pg_last_error(). "<br/>");

    print "Successfully created connection toodatabase. <br/>";

    // Perform some SQL queries over hello connection.
    $query = "SELECT * from inventory";
    $result_set = pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    while ($row = pg_fetch_row($result_set))
    {
        print "Data row = ($row[0], $row[1], $row[2]). <br/>";
    }

    // Free result_set
    pg_free_result($result_set);

    // Closing connection
    pg_close($connection);
?>
```

## <a name="update-data"></a><span data-ttu-id="ab35f-157">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="ab35f-157">Update data</span></span>
<span data-ttu-id="ab35f-158">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak veri güncelleştirme bir **güncelleştirme** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="ab35f-158">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="ab35f-159">Merhaba kod arama yönteminde [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure PostgreSQL için veritabanı.</span><span class="sxs-lookup"><span data-stu-id="ab35f-159">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="ab35f-160">Yöntemini çağıran sonra [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun bir komut ve [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello ayrıntıları, bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="ab35f-160">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span> <span data-ttu-id="ab35f-161">Yöntem çağrıları sonra [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="ab35f-161">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="ab35f-162">Hello yerine `$host`, `$database`, `$user`, ve `$password` kendi değerlerinizi parametrelerle.</span><span class="sxs-lookup"><span data-stu-id="ab35f-162">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed toocreate connection toodatabase: ". pg_last_error(). ".<br/>");

    print "Successfully created connection toodatabase. <br/>";

    // Modify some data in table.
    $new_quantity = 200;
    $name = '\'banana\'';
    $query = "UPDATE inventory SET quantity = $new_quantity WHERE name = $name;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). ".<br/>");
    print "Updated 1 row of data. </br>";

    // Closing connection
    pg_close($connection);
?>
```


## <a name="delete-data"></a><span data-ttu-id="ab35f-163">Verileri silme</span><span class="sxs-lookup"><span data-stu-id="ab35f-163">Delete data</span></span>
<span data-ttu-id="ab35f-164">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **silmek** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="ab35f-164">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="ab35f-165">Merhaba kod arama yönteminde [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect PostgreSQL için çok Azure veritabanı.</span><span class="sxs-lookup"><span data-stu-id="ab35f-165">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect too Azure Database for PostgreSQL.</span></span> <span data-ttu-id="ab35f-166">Yöntemini çağıran sonra [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun bir komut ve [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello ayrıntıları, bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="ab35f-166">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span> <span data-ttu-id="ab35f-167">Yöntem çağrıları sonra [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="ab35f-167">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="ab35f-168">Hello yerine `$host`, `$database`, `$user`, ve `$password` kendi değerlerinizi parametrelerle.</span><span class="sxs-lookup"><span data-stu-id="ab35f-168">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
            or die("Failed toocreate connection toodatabase: ". pg_last_error(). ". </br>");

    print "Successfully created connection toodatabase. <br/>";

    // Delete some data from table.
    $name = '\'orange\'';
    $query = "DELETE FROM inventory WHERE name = $name;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). ". <br/>");
    print "Deleted 1 row of data. <br/>";

    // Closing connection
    pg_close($connection);
?>
```

## <a name="next-steps"></a><span data-ttu-id="ab35f-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ab35f-169">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="ab35f-170">Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme</span><span class="sxs-lookup"><span data-stu-id="ab35f-170">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
