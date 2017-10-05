---
title: "PHP'den MySQL için Azure Veritabanı'na bağlanma | Microsoft Docs"
description: "Bu hızlı başlangıçta, MySQL için Azure Veritabanı'na bağlanmak ve buradan veri sorgulamak için kullanabileceğiniz birkaç PHP kod örneği sağlanmıştır."
services: mysql
author: mswutao
ms.author: wuta
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: 59da1ab9e76685d7ed0c4415ef99578c982e956c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-database-for-mysql-use-php-to-connect-and-query-data"></a><span data-ttu-id="3ec8b-103">MySQL için Azure Veritabanı: PHP'yi kullanarak bağlanma ve veri sorgulama</span><span class="sxs-lookup"><span data-stu-id="3ec8b-103">Azure Database for MySQL: Use PHP to connect and query data</span></span>
<span data-ttu-id="3ec8b-104">Bu hızlı başlangıçta [PHP](http://php.net/manual/intro-whatis.php) uygulaması kullanarak MySQL için Azure Veritabanı'na nasıl bağlanacağınız gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="3ec8b-105">Ayrıca veritabanında veri sorgulamak, eklemek, güncelleştirmek ve silmek için SQL deyimlerini nasıl kullanacağınız da gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="3ec8b-106">Bu makalede, PHP kullanarak geliştirmeyle ilgili bilgi sahibi olduğunuz ve MySQL için Azure Veritabanı ile çalışmaya yeni başladığınız varsayılır.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-106">This article assumes you are familiar with development using PHP, but that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ec8b-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3ec8b-107">Prerequisites</span></span>
<span data-ttu-id="3ec8b-108">Bu hızlı başlangıçta, başlangıç noktası olarak şu kılavuzlardan birinde oluşturulan kaynaklar kullanılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="3ec8b-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="3ec8b-109">Azure portalını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="3ec8b-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="3ec8b-110">Azure CLI kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="3ec8b-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="3ec8b-111">PHP'yi yükleme</span><span class="sxs-lookup"><span data-stu-id="3ec8b-111">Install PHP</span></span>
<span data-ttu-id="3ec8b-112">PHP'yi kendi sunucunuza yükleyin veya PHP içeren bir Azure [web uygulaması](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="macos"></a><span data-ttu-id="3ec8b-113">macOS</span><span class="sxs-lookup"><span data-stu-id="3ec8b-113">MacOS</span></span>
- <span data-ttu-id="3ec8b-114">[PHP 7.1.4 sürümünü](http://php.net/downloads.php) indirin</span><span class="sxs-lookup"><span data-stu-id="3ec8b-114">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="3ec8b-115">PHP'yi yükleyin ve diğer yapılandırmalar için [PHP kılavuzuna](http://php.net/manual/install.macosx.php) bakın</span><span class="sxs-lookup"><span data-stu-id="3ec8b-115">Install PHP and refer to the [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="3ec8b-116">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="3ec8b-116">Linux (Ubuntu)</span></span>
- <span data-ttu-id="3ec8b-117">[PHP 7.1.4 iş parçacığı güvenli olmayan (x64) sürümünü](http://php.net/downloads.php) indirin</span><span class="sxs-lookup"><span data-stu-id="3ec8b-117">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="3ec8b-118">PHP'yi yükleyin ve diğer yapılandırmalar için [PHP kılavuzuna](http://php.net/manual/install.unix.php) bakın</span><span class="sxs-lookup"><span data-stu-id="3ec8b-118">Install PHP and refer to the [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>

### <a name="windows"></a><span data-ttu-id="3ec8b-119">Windows</span><span class="sxs-lookup"><span data-stu-id="3ec8b-119">Windows</span></span>
- <span data-ttu-id="3ec8b-120">[PHP 7.1.4 iş parçacığı güvenli olmayan (x64) sürümünü](http://windows.php.net/download#php-7.1) indirin</span><span class="sxs-lookup"><span data-stu-id="3ec8b-120">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="3ec8b-121">PHP'yi yükleyin ve diğer yapılandırmalar için [PHP kılavuzuna](http://php.net/manual/install.windows.php) bakın</span><span class="sxs-lookup"><span data-stu-id="3ec8b-121">Install PHP and refer to the [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="3ec8b-122">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="3ec8b-122">Get connection information</span></span>
<span data-ttu-id="3ec8b-123">MySQL için Azure Veritabanı'na bağlanmak üzere gereken bağlantı bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-123">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="3ec8b-124">Tam sunucu adına ve oturum açma kimlik bilgilerine ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-124">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="3ec8b-125">[Azure Portal](https://portal.azure.com/)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-125">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3ec8b-126">Sol bölmede **Tüm kaynaklar**’a tıklayın ve ardından oluşturduğunuz sunucuyu arayın (örneğin, **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="3ec8b-126">In the left pane, click **All resources**, and then search for the server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="3ec8b-127">Sunucunun adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-127">Click the server name.</span></span>
4. <span data-ttu-id="3ec8b-128">Sunucunun **Özellikler** sayfasını seçin.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-128">Select the server's **Properties** page.</span></span> <span data-ttu-id="3ec8b-129">**Sunucu adını** ve **Sunucu yöneticisi oturum açma adını** not edin.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-129">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="3ec8b-130">![MySQL için Azure Veritabanı sunucu adı](./media/connect-php/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="3ec8b-130">![Azure Database for MySQL server name](./media/connect-php/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="3ec8b-131">Sunucunuzun oturum açma bilgilerini unuttuysanız **Genel Bakış** sayfasına giderek Sunucu yöneticisi oturum açma adını görüntüleyin ve gerekirse parolayı sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-131">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="3ec8b-132">Bağlanma ve tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="3ec8b-132">Connect and create a table</span></span>
<span data-ttu-id="3ec8b-133">Bağlanmak ve **CREATE TABLE** SQL deyimini kullanarak tablo oluşturmak için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-133">Use the following code to connect and create a table using **CREATE TABLE** SQL statement.</span></span> 

<span data-ttu-id="3ec8b-134">Kod, PHP'de bulunan **MySQL Improved extension** (mysqli) sınıfını kullanır.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-134">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="3ec8b-135">Kod, MySQL'e bağlanmak için [mysqli_init](http://php.net/manual/mysqli.init.php) ve [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) yöntemlerini çağırır.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-135">The code call methods [mysqli_init](http://php.net/manual/mysqli.init.php) and [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) to connect to MySQL.</span></span> <span data-ttu-id="3ec8b-136">Ardından sorgu çalıştırmak için [mysqli_query](http://php.net/manual/mysqli.query.php) yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-136">Then it calls method [mysqli_query](http://php.net/manual/mysqli.query.php) to run the query.</span></span> <span data-ttu-id="3ec8b-137">Daha sonra bağlantıyı kapatmak için [mysqli_close](http://php.net/manual/mysqli.close.php) yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-137">Then it calls method [mysqli_close](http://php.net/manual/mysqli.close.php) to close the connection.</span></span>

<span data-ttu-id="3ec8b-138">host, username, password ve db_name parametre değerlerini kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-138">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

// Run the create table query
if (mysqli_query($conn, '
CREATE TABLE Products (
`Id` INT NOT NULL AUTO_INCREMENT ,
`ProductName` VARCHAR(200) NOT NULL ,
`Color` VARCHAR(50) NOT NULL ,
`Price` DOUBLE NOT NULL ,
PRIMARY KEY (`Id`)
);
')) {
printf("Table created\n");
}

//Close the connection
mysqli_close($conn);
?>
```

## <a name="insert-data"></a><span data-ttu-id="3ec8b-139">Veri ekleme</span><span class="sxs-lookup"><span data-stu-id="3ec8b-139">Insert data</span></span>
<span data-ttu-id="3ec8b-140">Bağlanmak ve **INSERT** SQL deyimi kullanarak veri eklemek için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-140">Use the following code to connect and insert data using an **INSERT** SQL statement.</span></span>

<span data-ttu-id="3ec8b-141">Kod, PHP'de bulunan **MySQL Improved extension** (mysqli) sınıfını kullanır.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-141">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="3ec8b-142">Kod, [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) yöntemini kullanarak hazır bir INSERT deyimi oluşturur, ardından [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php) yöntemini kullanarak, eklenen her bir sütun değerine ilişkin parametreleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-142">The code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) to create a prepared insert statement, then binds the parameters for each inserted column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="3ec8b-143">Kod, [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) yöntemini kullanarak deyimi çalıştırır ve ardından [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php) yöntemini kullanarak deyimi kapatır.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-143">The code runs the statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes the statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="3ec8b-144">host, username, password ve db_name parametre değerlerini kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-144">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Create an Insert prepared statement and run it
$product_name = 'BrandNewProduct';
$product_color = 'Blue';
$product_price = 15.5;
if ($stmt = mysqli_prepare($conn, "INSERT INTO Products (ProductName, Color, Price) VALUES (?, ?, ?)")) {
mysqli_stmt_bind_param($stmt, 'ssd', $product_name, $product_color, $product_price);
mysqli_stmt_execute($stmt);
printf("Insert: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

// Close the connection
mysqli_close($conn);
?>
```

## <a name="read-data"></a><span data-ttu-id="3ec8b-145">Verileri okuma</span><span class="sxs-lookup"><span data-stu-id="3ec8b-145">Read data</span></span>
<span data-ttu-id="3ec8b-146">Bağlanmak ve **SELECT** SQL deyimi kullanarak verileri okumak için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-146">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span>  <span data-ttu-id="3ec8b-147">Kod, PHP'de bulunan **MySQL Improved extension** (mysqli) sınıfını kullanır.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-147">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="3ec8b-148">Kod, [mysqli_query](http://php.net/manual/mysqli.query.php) yöntemini kullanarak SQL sorgusunu gerçekleştirir ve [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) yöntemini kullanarak elde edilen satırları getirir.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-148">The code uses method [mysqli_query](http://php.net/manual/mysqli.query.php) perform the sql query, and uses [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) method to fetch the resulting rows.</span></span>

<span data-ttu-id="3ec8b-149">host, username, password ve db_name parametre değerlerini kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-149">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Run the Select query
printf("Reading data from table: \n");
$res = mysqli_query($conn, 'SELECT * FROM Products');
while ($row = mysqli_fetch_assoc($res)) {
var_dump($row);
}

//Close the connection
mysqli_close($conn);
?>
```

## <a name="update-data"></a><span data-ttu-id="3ec8b-150">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="3ec8b-150">Update data</span></span>
<span data-ttu-id="3ec8b-151">Bağlanmak ve **UPDATE** SQL deyimi kullanarak verileri güncelleştirmek için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-151">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="3ec8b-152">Kod, PHP'de bulunan **MySQL Improved extension** (mysqli) sınıfını kullanır.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-152">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="3ec8b-153">Kod, [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) yöntemini kullanarak hazır bir UPDATE deyimi oluşturur, ardından [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php) yöntemini kullanarak, güncelleştirilen her bir sütun değerine ilişkin parametreleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-153">The code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) to create a prepared update statement, then binds the parameters for each updated column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="3ec8b-154">Kod, [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) yöntemini kullanarak deyimi çalıştırır ve ardından [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php) yöntemini kullanarak deyimi kapatır.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-154">The code runs the statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes the statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="3ec8b-155">host, username, password ve db_name parametre değerlerini kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-155">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Run the Update statement
$product_name = 'BrandNewProduct';
$new_product_price = 15.1;
if ($stmt = mysqli_prepare($conn, "UPDATE Products SET Price = ? WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 'ds', $new_product_price, $product_name);
mysqli_stmt_execute($stmt);
printf("Update: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));

//Close the connection
mysqli_stmt_close($stmt);
}

mysqli_close($conn);
?>
```


## <a name="delete-data"></a><span data-ttu-id="3ec8b-156">Verileri silme</span><span class="sxs-lookup"><span data-stu-id="3ec8b-156">Delete data</span></span>
<span data-ttu-id="3ec8b-157">Bağlanmak ve **DELETE** SQL deyimi kullanarak verileri okumak için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-157">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="3ec8b-158">Kod, PHP'de bulunan **MySQL Improved extension** (mysqli) sınıfını kullanır.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-158">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="3ec8b-159">Kod, [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) yöntemini kullanarak hazır bir DELETE deyimi oluşturur, ardından [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php) yöntemini kullanarak deyimdeki WHERE yan tümcesine ilişkin parametreleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-159">The code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) to create a prepared delete statement, then binds the parameters for the where clause in the statement using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="3ec8b-160">Kod, [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) yöntemini kullanarak deyimi çalıştırır ve ardından [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php) yöntemini kullanarak deyimi kapatır.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-160">The code runs the statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes the statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="3ec8b-161">host, username, password ve db_name parametre değerlerini kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3ec8b-161">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Run the Delete statement
$product_name = 'BrandNewProduct';
if ($stmt = mysqli_prepare($conn, "DELETE FROM Products WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 's', $product_name);
mysqli_stmt_execute($stmt);
printf("Delete: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

//Close the connection
mysqli_close($conn);
?>
```

## <a name="next-steps"></a><span data-ttu-id="3ec8b-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3ec8b-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="3ec8b-163">Azure'da PHP ve MySQL web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="3ec8b-163">Build a PHP and MySQL web app in Azure</span></span>](../app-service-web/app-service-web-tutorial-php-mysql.md?toc=%2fazure%2fmysql%2ftoc.json)
