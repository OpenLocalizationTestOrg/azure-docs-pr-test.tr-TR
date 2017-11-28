---
title: "Php'den MySQL için tooAzure veritabanına bağlanma | Microsoft Docs"
description: "Bu hızlı başlangıç MySQL için Azure veritabanındaki verileri sorgulamak ve tooconnect için kullanabileceğiniz birkaç PHP kod örnekleri sağlar."
services: mysql
author: mswutao
ms.author: wuta
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: b928748c473c1aef320ae2183f237b5b845e83f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-php-tooconnect-and-query-data"></a><span data-ttu-id="9942f-103">Azure veritabanı için MySQL: kullanım PHP tooconnect ve sorgu verileri</span><span class="sxs-lookup"><span data-stu-id="9942f-103">Azure Database for MySQL: Use PHP tooconnect and query data</span></span>
<span data-ttu-id="9942f-104">Bu hızlı başlangıç gösteren Azure tooconnect tooan veritabanı nasıl MySQL kullanmak için bir [PHP](http://php.net/manual/intro-whatis.php) uygulama.</span><span class="sxs-lookup"><span data-stu-id="9942f-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="9942f-105">Nasıl toouse SQL deyimleri tooquery, Ekle, Güncelleştir ve hello veritabanında bulunan verileri silme gösterir.</span><span class="sxs-lookup"><span data-stu-id="9942f-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="9942f-106">Bu makale, Azure veritabanı için MySQL ile yeni tooworking olan ancak bu, PHP, kullanarak geliştirme ile bildiğinizi varsayar.</span><span class="sxs-lookup"><span data-stu-id="9942f-106">This article assumes you are familiar with development using PHP, but that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9942f-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9942f-107">Prerequisites</span></span>
<span data-ttu-id="9942f-108">Bu hızlı başlangıç Bu kılavuzlara birini başlangıç noktası olarak oluşturulan hello kaynakları kullanır:</span><span class="sxs-lookup"><span data-stu-id="9942f-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="9942f-109">Azure portalını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="9942f-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="9942f-110">Azure CLI kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="9942f-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="9942f-111">PHP'yi yükleme</span><span class="sxs-lookup"><span data-stu-id="9942f-111">Install PHP</span></span>
<span data-ttu-id="9942f-112">PHP'yi kendi sunucunuza yükleyin veya PHP içeren bir Azure [web uygulaması](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9942f-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="macos"></a><span data-ttu-id="9942f-113">macOS</span><span class="sxs-lookup"><span data-stu-id="9942f-113">MacOS</span></span>
- <span data-ttu-id="9942f-114">[PHP 7.1.4 sürümünü](http://php.net/downloads.php) indirin</span><span class="sxs-lookup"><span data-stu-id="9942f-114">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="9942f-115">PHP yükleme ve toohello başvuran [PHP el ile](http://php.net/manual/install.macosx.php) daha fazla yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9942f-115">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="9942f-116">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="9942f-116">Linux (Ubuntu)</span></span>
- <span data-ttu-id="9942f-117">[PHP 7.1.4 iş parçacığı güvenli olmayan (x64) sürümünü](http://php.net/downloads.php) indirin</span><span class="sxs-lookup"><span data-stu-id="9942f-117">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="9942f-118">PHP yükleme ve toohello başvuran [PHP el ile](http://php.net/manual/install.unix.php) daha fazla yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9942f-118">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>

### <a name="windows"></a><span data-ttu-id="9942f-119">Windows</span><span class="sxs-lookup"><span data-stu-id="9942f-119">Windows</span></span>
- <span data-ttu-id="9942f-120">[PHP 7.1.4 iş parçacığı güvenli olmayan (x64) sürümünü](http://windows.php.net/download#php-7.1) indirin</span><span class="sxs-lookup"><span data-stu-id="9942f-120">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="9942f-121">PHP yükleme ve toohello başvuran [PHP el ile](http://php.net/manual/install.windows.php) daha fazla yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9942f-121">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="9942f-122">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="9942f-122">Get connection information</span></span>
<span data-ttu-id="9942f-123">Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure veritabanı için MySQL alın.</span><span class="sxs-lookup"><span data-stu-id="9942f-123">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="9942f-124">Tam sunucu adını ve oturum açma kimlik bilgileri hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="9942f-124">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="9942f-125">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9942f-125">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9942f-126">Merhaba sol bölmede **tüm kaynakları**ve ardından oluşturduğunuz hello sunucusu için arama (örneğin, **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="9942f-126">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="9942f-127">Merhaba sunucu adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9942f-127">Click hello server name.</span></span>
4. <span data-ttu-id="9942f-128">Select hello sunucunun **özellikleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="9942f-128">Select hello server's **Properties** page.</span></span> <span data-ttu-id="9942f-129">Merhaba Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.</span><span class="sxs-lookup"><span data-stu-id="9942f-129">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="9942f-130">![MySQL için Azure Veritabanı sunucu adı](./media/connect-php/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="9942f-130">![Azure Database for MySQL server name](./media/connect-php/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="9942f-131">Sunucu oturum açma bilgilerinizi unutursanız, toohello gidin **genel bakış** tooview hello sunucu yönetici oturum açma adı sayfasında ve gerekirse sıfırlamak hello parola.</span><span class="sxs-lookup"><span data-stu-id="9942f-131">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="9942f-132">Bağlanma ve tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="9942f-132">Connect and create a table</span></span>
<span data-ttu-id="9942f-133">Kullanım hello aşağıdakileri tooconnect kod ve kullanarak bir tablo oluşturmak **CREATE TABLE** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="9942f-133">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement.</span></span> 

<span data-ttu-id="9942f-134">Merhaba kodu kullanan hello **uzantısı MySQL geliştirilmiş** PHP ile dahil (mysqli) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="9942f-134">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="9942f-135">Merhaba yöntemleri kod çağırabilir [mysqli_init](http://php.net/manual/mysqli.init.php) ve [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="9942f-135">hello code call methods [mysqli_init](http://php.net/manual/mysqli.init.php) and [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL.</span></span> <span data-ttu-id="9942f-136">Yöntem çağrıları sonra [mysqli_query](http://php.net/manual/mysqli.query.php) toorun hello sorgu.</span><span class="sxs-lookup"><span data-stu-id="9942f-136">Then it calls method [mysqli_query](http://php.net/manual/mysqli.query.php) toorun hello query.</span></span> <span data-ttu-id="9942f-137">Yöntem çağrıları sonra [mysqli_close](http://php.net/manual/mysqli.close.php) tooclose hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="9942f-137">Then it calls method [mysqli_close](http://php.net/manual/mysqli.close.php) tooclose hello connection.</span></span>

<span data-ttu-id="9942f-138">Merhaba ana bilgisayar, kullanıcı adı, parola ve db_name parametreleri kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9942f-138">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

// Run hello create table query
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

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="insert-data"></a><span data-ttu-id="9942f-139">Veri ekleme</span><span class="sxs-lookup"><span data-stu-id="9942f-139">Insert data</span></span>
<span data-ttu-id="9942f-140">Kullanım hello aşağıdakileri tooconnect kod ve verileri kullanarak Ekle bir **Ekle** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="9942f-140">Use hello following code tooconnect and insert data using an **INSERT** SQL statement.</span></span>

<span data-ttu-id="9942f-141">Merhaba kodu kullanan hello **uzantısı MySQL geliştirilmiş** PHP ile dahil (mysqli) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="9942f-141">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="9942f-142">Merhaba kodu yöntemi kullanan [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate hazırlanmış bir deyim ekleyin, sonra parametreleri yöntemi kullanarak her eklenen sütun değeri için bağlar hello [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="9942f-142">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared insert statement, then binds hello parameters for each inserted column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="9942f-143">Merhaba kodu çalıştırır yöntemini kullanarak hello deyimi [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) ve daha sonra kapanır yöntemini kullanarak deyimi hello [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="9942f-143">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="9942f-144">Merhaba ana bilgisayar, kullanıcı adı, parola ve db_name parametreleri kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9942f-144">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
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

// Close hello connection
mysqli_close($conn);
?>
```

## <a name="read-data"></a><span data-ttu-id="9942f-145">Verileri okuma</span><span class="sxs-lookup"><span data-stu-id="9942f-145">Read data</span></span>
<span data-ttu-id="9942f-146">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **seçin** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="9942f-146">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span>  <span data-ttu-id="9942f-147">Merhaba kodu kullanan hello **uzantısı MySQL geliştirilmiş** PHP ile dahil (mysqli) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="9942f-147">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="9942f-148">Merhaba kodu yöntemi kullanan [mysqli_query](http://php.net/manual/mysqli.query.php) hello sql sorgusu ve kullandığı gerçekleştirmek [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) yöntemi toofetch hello elde edilen satırları.</span><span class="sxs-lookup"><span data-stu-id="9942f-148">hello code uses method [mysqli_query](http://php.net/manual/mysqli.query.php) perform hello sql query, and uses [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) method toofetch hello resulting rows.</span></span>

<span data-ttu-id="9942f-149">Merhaba ana bilgisayar, kullanıcı adı, parola ve db_name parametreleri kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9942f-149">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Select query
printf("Reading data from table: \n");
$res = mysqli_query($conn, 'SELECT * FROM Products');
while ($row = mysqli_fetch_assoc($res)) {
var_dump($row);
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="update-data"></a><span data-ttu-id="9942f-150">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="9942f-150">Update data</span></span>
<span data-ttu-id="9942f-151">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak veri güncelleştirme bir **güncelleştirme** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="9942f-151">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="9942f-152">Merhaba kodu kullanan hello **uzantısı MySQL geliştirilmiş** PHP ile dahil (mysqli) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="9942f-152">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="9942f-153">Merhaba kodu yöntemi kullanan [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate hazırlıklı güncelleştirme bildirimi ardından hello parametreleri yöntemi kullanarak her güncelleştirilmiş sütun değeri için bağlar [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="9942f-153">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared update statement, then binds hello parameters for each updated column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="9942f-154">Merhaba kodu çalıştırır yöntemini kullanarak hello deyimi [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) ve daha sonra kapanır yöntemini kullanarak deyimi hello [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="9942f-154">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="9942f-155">Merhaba ana bilgisayar, kullanıcı adı, parola ve db_name parametreleri kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9942f-155">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Update statement
$product_name = 'BrandNewProduct';
$new_product_price = 15.1;
if ($stmt = mysqli_prepare($conn, "UPDATE Products SET Price = ? WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 'ds', $new_product_price, $product_name);
mysqli_stmt_execute($stmt);
printf("Update: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));

//Close hello connection
mysqli_stmt_close($stmt);
}

mysqli_close($conn);
?>
```


## <a name="delete-data"></a><span data-ttu-id="9942f-156">Verileri silme</span><span class="sxs-lookup"><span data-stu-id="9942f-156">Delete data</span></span>
<span data-ttu-id="9942f-157">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **silmek** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="9942f-157">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="9942f-158">Merhaba kodu kullanan hello **uzantısı MySQL geliştirilmiş** PHP ile dahil (mysqli) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="9942f-158">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="9942f-159">Hello kodu kullanan yöntemi [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate bir hazırlıklı deyimi silin, ardından bağlamalar hello hello parametrelerini burada yöntemini kullanarak hello deyimindeki yan tümcesi [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="9942f-159">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared delete statement, then binds hello parameters for hello where clause in hello statement using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="9942f-160">Merhaba kodu çalıştırır yöntemini kullanarak hello deyimi [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) ve daha sonra kapanır yöntemini kullanarak deyimi hello [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="9942f-160">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="9942f-161">Merhaba ana bilgisayar, kullanıcı adı, parola ve db_name parametreleri kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9942f-161">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Delete statement
$product_name = 'BrandNewProduct';
if ($stmt = mysqli_prepare($conn, "DELETE FROM Products WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 's', $product_name);
mysqli_stmt_execute($stmt);
printf("Delete: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="next-steps"></a><span data-ttu-id="9942f-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9942f-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="9942f-163">Azure'da PHP ve MySQL web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="9942f-163">Build a PHP and MySQL web app in Azure</span></span>](../app-service-web/app-service-web-tutorial-php-mysql.md?toc=%2fazure%2fmysql%2ftoc.json)
