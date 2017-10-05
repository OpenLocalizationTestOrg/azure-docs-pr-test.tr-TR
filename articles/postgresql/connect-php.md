---
title: "PHP kullanarak PostgreSQL için Azure Veritabanı’na bağlanma | Microsoft Docs"
description: "Bu hızlı başlangıçta, PostgreSQL için Azure Veritabanı’na bağlanmak ve buradan veri sorgulamak için kullanabileceğiniz PHP kod örneği sağlanmıştır."
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
ms.openlocfilehash: ed7c92e0689bca4056401d562271e3b6b7144dcf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-php-to-connect-and-query-data"></a><span data-ttu-id="45d63-103">PostgreSQL için Azure Veritabanı: Bağlanmak ve veri sorgulamak için PHP’yi kullanma</span><span class="sxs-lookup"><span data-stu-id="45d63-103">Azure Database for PostgreSQL: Use PHP to connect and query data</span></span>
<span data-ttu-id="45d63-104">Bu hızlı başlangıçta, [PHP](http://php.net/manual/intro-whatis.php) uygulaması kullanılarak PostgreSQL için Azure Veritabanı’na nasıl bağlanılacağı gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="45d63-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="45d63-105">Hızlı başlangıçta, veritabanında verileri sorgulamak, eklemek, güncelleştirmek ve silmek için SQL deyimlerinin nasıl kullanılacağı da gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="45d63-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="45d63-106">Bu makalede, PHP kullanarak geliştirmeyle ilgili bilgi sahibi olduğunuz ve PostgreSQL için Azure Veritabanı ile çalışmaya yeni başladığınız varsayılır.</span><span class="sxs-lookup"><span data-stu-id="45d63-106">This article assumes you are familiar with development using PHP, but that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45d63-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="45d63-107">Prerequisites</span></span>
<span data-ttu-id="45d63-108">Bu hızlı başlangıçta, başlangıç noktası olarak şu kılavuzlardan birinde oluşturulan kaynaklar kullanılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="45d63-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="45d63-109">DB Oluşturma - Portal</span><span class="sxs-lookup"><span data-stu-id="45d63-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="45d63-110">DB Oluşturma - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="45d63-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="45d63-111">PHP’yi yükleme</span><span class="sxs-lookup"><span data-stu-id="45d63-111">Install PHP</span></span>
<span data-ttu-id="45d63-112">PHP’yi kendi sunucunuza yükleyin veya PHP içeren bir Azure [web uygulaması](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="45d63-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="windows"></a><span data-ttu-id="45d63-113">Windows</span><span class="sxs-lookup"><span data-stu-id="45d63-113">Windows</span></span>
- <span data-ttu-id="45d63-114">[PHP 7.1.4 iş parçacığı güvenli olmayan (x64) sürümünü](http://windows.php.net/download#php-7.1) indirin</span><span class="sxs-lookup"><span data-stu-id="45d63-114">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="45d63-115">PHP’yi yükleyin ve diğer yapılandırmalar için [PHP kılavuzuna](http://php.net/manual/install.windows.php) bakın</span><span class="sxs-lookup"><span data-stu-id="45d63-115">Install PHP and refer to the [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>
- <span data-ttu-id="45d63-116">Kod, PHP yüklemesine dahil olan **pgsql** sınıfını (ext/php_pgsql.dll) kullanır.</span><span class="sxs-lookup"><span data-stu-id="45d63-116">The code uses the **pgsql** class (ext/php_pgsql.dll)  that is included in the PHP installation.</span></span> 
- <span data-ttu-id="45d63-117">Genellikle `C:\Program Files\PHP\v7.1\php.ini` konumunda bulunan php.ini yapılandırma dosyasını düzenleyerek **pgsql** uzantısını etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="45d63-117">Enabled the **pgsql** extension by editing the php.ini configuration file, typically located at `C:\Program Files\PHP\v7.1\php.ini`.</span></span> <span data-ttu-id="45d63-118">Yapılandırma dosyası, `extension=php_pgsql.so` metnine sahip bir satır içermelidir.</span><span class="sxs-lookup"><span data-stu-id="45d63-118">The configuration file should contain a line with the text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="45d63-119">Gösterilmiyorsa metni ekleyip dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="45d63-119">If it is not shown, add the text and save the file.</span></span> <span data-ttu-id="45d63-120">Metin varsa, ancak metne noktalı virgül ön ekiyle açıklama eklenmişse noktalı virgülü kaldırarak metindeki açıklamayı silin.</span><span class="sxs-lookup"><span data-stu-id="45d63-120">If the text is present, but commented with a semicolon prefix, uncomment the text by removing the semicolon.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="45d63-121">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="45d63-121">Linux (Ubuntu)</span></span>
- <span data-ttu-id="45d63-122">[PHP 7.1.4 iş parçacığı güvenli olmayan (x64) sürümünü](http://php.net/downloads.php) indirin</span><span class="sxs-lookup"><span data-stu-id="45d63-122">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span> 
- <span data-ttu-id="45d63-123">PHP’yi yükleyin ve diğer yapılandırmalar için [PHP kılavuzuna](http://php.net/manual/install.unix.php) bakın</span><span class="sxs-lookup"><span data-stu-id="45d63-123">Install PHP and refer to the [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>
- <span data-ttu-id="45d63-124">Kod, **pgsql** sınıfını (php_pgsql.so) kullanır.</span><span class="sxs-lookup"><span data-stu-id="45d63-124">The code uses the **pgsql** class (php_pgsql.so).</span></span> <span data-ttu-id="45d63-125">`sudo apt-get install php-pgsql` öğesini çalıştırarak yükleyin.</span><span class="sxs-lookup"><span data-stu-id="45d63-125">Install it by running `sudo apt-get install php-pgsql`.</span></span>
- <span data-ttu-id="45d63-126">`/etc/php/7.0/mods-available/pgsql.ini` yapılandırma dosyasını düzenleyerek **pgsql** uzantısını etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="45d63-126">Enabled the **pgsql** extension by editing the `/etc/php/7.0/mods-available/pgsql.ini` configuration file.</span></span> <span data-ttu-id="45d63-127">Yapılandırma dosyası, `extension=php_pgsql.so` metnine sahip bir satır içermelidir.</span><span class="sxs-lookup"><span data-stu-id="45d63-127">The configuration file should contain a line with the text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="45d63-128">Gösterilmiyorsa metni ekleyip dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="45d63-128">If it is not shown, add the text and save the file.</span></span> <span data-ttu-id="45d63-129">Metin varsa, ancak metne noktalı virgül ön ekiyle açıklama eklenmişse noktalı virgülü kaldırarak metindeki açıklamayı silin.</span><span class="sxs-lookup"><span data-stu-id="45d63-129">If the text is present, but commented with a semicolon prefix, uncomment the text by removing the semicolon.</span></span>

### <a name="macos"></a><span data-ttu-id="45d63-130">MacOS</span><span class="sxs-lookup"><span data-stu-id="45d63-130">MacOS</span></span>
- <span data-ttu-id="45d63-131">[PHP 7.1.4 sürümünü](http://php.net/downloads.php) indirin</span><span class="sxs-lookup"><span data-stu-id="45d63-131">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="45d63-132">PHP’yi yükleyin ve diğer yapılandırmalar için [PHP kılavuzuna](http://php.net/manual/install.macosx.php) bakın</span><span class="sxs-lookup"><span data-stu-id="45d63-132">Install PHP and refer to the [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="45d63-133">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="45d63-133">Get connection information</span></span>
<span data-ttu-id="45d63-134">PostgreSQL için Azure Veritabanı'na bağlanmak üzere gereken bağlantı bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="45d63-134">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="45d63-135">Tam sunucu adına ve oturum açma kimlik bilgilerine ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="45d63-135">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="45d63-136">[Azure Portal](https://portal.azure.com/)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="45d63-136">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="45d63-137">Azure portalında sol taraftaki menüden **Tüm kaynaklar**'a tıklayın ve oluşturduğunuz sunucuyu (örneğin, **mypgserver-20170401**) arayın.</span><span class="sxs-lookup"><span data-stu-id="45d63-137">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="45d63-138">**mypgserver-20170401** sunucu adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45d63-138">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="45d63-139">Sunucunun **Genel Bakış** sayfasını seçin.</span><span class="sxs-lookup"><span data-stu-id="45d63-139">Select the server's **Overview** page.</span></span> <span data-ttu-id="45d63-140">**Sunucu adını** ve **Sunucu yöneticisi oturum açma adını** not edin.</span><span class="sxs-lookup"><span data-stu-id="45d63-140">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="45d63-141">![PostgreSQL için Azure Veritabanı - Sunucu Yöneticisi Oturum Açma Bilgileri](./media/connect-php/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="45d63-141">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-php/1-connection-string.png)</span></span>
5. <span data-ttu-id="45d63-142">Sunucunuzun oturum açma bilgilerini unuttuysanız **Genel Bakış** sayfasına giderek Sunucu yöneticisi oturum açma adını görüntüleyin ve gerekirse parolayı sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="45d63-142">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="45d63-143">Bir tabloyu bağlama ve oluşturma</span><span class="sxs-lookup"><span data-stu-id="45d63-143">Connect and create a table</span></span>
<span data-ttu-id="45d63-144">**CREATE TABLE** SQL deyimini kullanarak bir tabloyu bağlamak ve oluşturmak ve ardından **INSERT INTO** SQL deyimlerini kullanarak tabloya satırlar eklemek için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="45d63-144">Use the following code to connect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span></span>

<span data-ttu-id="45d63-145">Kod, PostgreSQL için Azure Veritabanı’na bağlanmak amacıyla [pg_connect()](http://php.net/manual/en/function.pg-connect.php) yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="45d63-145">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="45d63-146">Ardından birkaç komutu çalıştırmak için birkaç kez [pg_query()](http://php.net/manual/en/function.pg-query.php) yöntemini ve her seferinde bir hata oluşursa ayrıntıları kontrol etmek için [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="45d63-146">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) several times to run several commands, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred each time.</span></span> <span data-ttu-id="45d63-147">Daha sonra bağlantıyı kapatmak için [pg_close()](http://php.net/manual/en/function.pg-close.php) yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="45d63-147">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="45d63-148">`$host`, `$database`, `$user` ve `$password` parametrelerini kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="45d63-148">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password") 
        or die("Failed to create connection to database: ". pg_last_error(). "<br/>");
    print "Successfully created connection to database.<br/>";

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

## <a name="read-data"></a><span data-ttu-id="45d63-149">Verileri okuma</span><span class="sxs-lookup"><span data-stu-id="45d63-149">Read data</span></span>
<span data-ttu-id="45d63-150">**SELECT** SQL deyimini kullanarak bağlanmak ve verileri okumak için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="45d63-150">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

 <span data-ttu-id="45d63-151">Kod, PostgreSQL için Azure Veritabanı’na bağlanmak amacıyla [pg_connect()](http://php.net/manual/en/function.pg-connect.php) yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="45d63-151">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="45d63-152">Ardından sonuçları bir sonuç kümesinde tutarak SELECT komutunu çalıştırmak için [pg_query()](http://php.net/manual/en/function.pg-query.php) yöntemini ve bir hata oluşursa ayrıntıları kontrol etmek için [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="45d63-152">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) to run the SELECT command, keeping the results in a result set, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred.</span></span>  <span data-ttu-id="45d63-153">Sonuç kümesini okumak için döngüde satır başına bir kez [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) yöntemi çağrılır ve her dizi konumunda sütun başında bir veri değeri olacak şekilde `$row` dizisinde satır verileri alınır.</span><span class="sxs-lookup"><span data-stu-id="45d63-153">To read the result set, method [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) is called in a loop, once per row, and the row data is retrieved in an array `$row`, with one data value per column in each array position.</span></span>  <span data-ttu-id="45d63-154">Sonuç kümesini boşaltmak için [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) yöntemi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="45d63-154">To free the result set, method [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) is called.</span></span> <span data-ttu-id="45d63-155">Daha sonra bağlantıyı kapatmak için [pg_close()](http://php.net/manual/en/function.pg-close.php) yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="45d63-155">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="45d63-156">`$host`, `$database`, `$user` ve `$password` parametrelerini kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="45d63-156">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";
    
    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed to create connection to database: ". pg_last_error(). "<br/>");

    print "Successfully created connection to database. <br/>";

    // Perform some SQL queries over the connection.
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

## <a name="update-data"></a><span data-ttu-id="45d63-157">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="45d63-157">Update data</span></span>
<span data-ttu-id="45d63-158">**UPDATE** SQL deyimini kullanarak bağlanmak ve verileri güncelleştirmek için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="45d63-158">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="45d63-159">Kod, PostgreSQL için Azure Veritabanı’na bağlanmak amacıyla [pg_connect()](http://php.net/manual/en/function.pg-connect.php) yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="45d63-159">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="45d63-160">Ardından bir komut çalıştırmak için [pg_query()](http://php.net/manual/en/function.pg-query.php) yöntemini ve bir hata oluşursa ayrıntıları kontrol etmek için [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="45d63-160">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) to run a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred.</span></span> <span data-ttu-id="45d63-161">Daha sonra bağlantıyı kapatmak için [pg_close()](http://php.net/manual/en/function.pg-close.php) yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="45d63-161">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="45d63-162">`$host`, `$database`, `$user` ve `$password` parametrelerini kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="45d63-162">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed to create connection to database: ". pg_last_error(). ".<br/>");

    print "Successfully created connection to database. <br/>";

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


## <a name="delete-data"></a><span data-ttu-id="45d63-163">Verileri silme</span><span class="sxs-lookup"><span data-stu-id="45d63-163">Delete data</span></span>
<span data-ttu-id="45d63-164">**DELETE** SQL deyimini kullanarak bağlanmak ve verileri okumak için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="45d63-164">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="45d63-165">Kod, PostgreSQL için Azure Veritabanı’na bağlanmak amacıyla [pg_connect()](http://php.net/manual/en/function.pg-connect.php) yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="45d63-165">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to  Azure Database for PostgreSQL.</span></span> <span data-ttu-id="45d63-166">Ardından bir komut çalıştırmak için [pg_query()](http://php.net/manual/en/function.pg-query.php) yöntemini ve bir hata oluşursa ayrıntıları kontrol etmek için [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="45d63-166">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) to run a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred.</span></span> <span data-ttu-id="45d63-167">Daha sonra bağlantıyı kapatmak için [pg_close()](http://php.net/manual/en/function.pg-close.php) yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="45d63-167">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="45d63-168">`$host`, `$database`, `$user` ve `$password` parametrelerini kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="45d63-168">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
            or die("Failed to create connection to database: ". pg_last_error(). ". </br>");

    print "Successfully created connection to database. <br/>";

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

## <a name="next-steps"></a><span data-ttu-id="45d63-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="45d63-169">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="45d63-170">Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme</span><span class="sxs-lookup"><span data-stu-id="45d63-170">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
