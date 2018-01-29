---
title: "PHP'den MySQL için Azure Veritabanı'na bağlanma | Microsoft Docs"
description: "Bu hızlı başlangıçta, MySQL için Azure Veritabanı'na bağlanmak ve buradan veri sorgulamak için kullanabileceğiniz birkaç PHP kod örneği sağlanmıştır."
services: mysql
author: mswutao
ms.author: wuta
manager: jhubbard
editor: jasonwhowell
ms.service: mysql
ms.custom: mvc
ms.topic: quickstart
ms.date: 09/22/2017
ms.openlocfilehash: 530b02e7cd2a45ce3d9b8968b090d2b48b34e843
ms.sourcegitcommit: 9ea2edae5dbb4a104322135bef957ba6e9aeecde
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/03/2018
---
# <a name="azure-database-for-mysql-use-php-to-connect-and-query-data"></a>MySQL için Azure Veritabanı: PHP'yi kullanarak bağlanma ve veri sorgulama
Bu hızlı başlangıçta [PHP](http://php.net/manual/intro-whatis.php) uygulaması kullanarak MySQL için Azure Veritabanı'na nasıl bağlanacağınız gösterilmiştir. Hızlı başlangıçta, veritabanında verileri sorgulamak, eklemek, güncelleştirmek ve silmek için SQL deyimlerinin nasıl kullanılacağı da gösterilmiştir. Bu konuda, PHP kullanarak geliştirmeyle ilgili bilgi sahibi olduğunuz ve MySQL için Azure Veritabanı ile çalışmaya yeni başladığınız varsayılır.

## <a name="prerequisites"></a>Ön koşullar
Bu hızlı başlangıçta, başlangıç noktası olarak şu kılavuzlardan birinde oluşturulan kaynaklar kullanılmaktadır:
- [Azure portalını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Azure CLI kullanarak MySQL için Azure Veritabanı sunucusu oluşturma](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-php"></a>PHP'yi yükleme
PHP'yi kendi sunucunuza yükleyin veya PHP içeren bir Azure [web uygulaması](../app-service/app-service-web-overview.md) oluşturun.

### <a name="macos"></a>macOS
- [PHP 7.1.4 sürümünü](http://php.net/downloads.php) indirin.
- PHP'yi yükleyin ve diğer yapılandırmalar için [PHP kılavuzuna](http://php.net/manual/install.macosx.php) bakın.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- [PHP 7.1.4 iş parçacığı güvenli olmayan (x64) sürümünü](http://php.net/downloads.php) indirin.
- PHP'yi yükleyin ve diğer yapılandırmalar için [PHP kılavuzuna](http://php.net/manual/install.unix.php) bakın.

### <a name="windows"></a>Windows
- [PHP 7.1.4 iş parçacığı güvenli olmayan (x64) sürümünü](http://windows.php.net/download#php-7.1) indirin.
- PHP'yi yükleyin ve diğer yapılandırmalar için [PHP kılavuzuna](http://php.net/manual/install.windows.php) bakın.

## <a name="get-connection-information"></a>Bağlantı bilgilerini alma
MySQL için Azure Veritabanı'na bağlanmak üzere gereken bağlantı bilgilerini alın. Tam sunucu adına ve oturum açma kimlik bilgilerine ihtiyacınız vardır.

1. [Azure Portal](https://portal.azure.com/)’da oturum açın.
2. Sol bölmede **Tüm kaynaklar**’a tıklayın ve ardından oluşturduğunuz sunucuyu arayın (örneğin, **myserver4demo**).
3. Sunucunun adına tıklayın.
4. Sunucunun **Özellikler** sayfasını seçin ve **Sunucu adı** ile **Sunucu yöneticisi oturum açma adı**’nı not alın.
 ![MySQL için Azure Veritabanı sunucu adı](./media/connect-php/1_server-properties-name-login.png)
5. Sunucunuzun oturum açma bilgilerini unuttuysanız **Genel Bakış** sayfasına giderek Sunucu yöneticisi oturum açma adını görüntüleyin ve gerekirse parolayı sıfırlayın.

## <a name="connect-and-create-a-table"></a>Bağlanma ve tablo oluşturma
Bağlanmak ve **CREATE TABLE** SQL deyimini kullanarak tablo oluşturmak için aşağıdaki kodu kullanın. 

Kod, PHP'de bulunan **MySQL Improved extension** (mysqli) sınıfını kullanır. Kod, MySQL'e bağlanmak için [mysqli_init](http://php.net/manual/mysqli.init.php) ve [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) yöntemlerini çağırır. Ardından sorgu çalıştırmak için [mysqli_query](http://php.net/manual/mysqli.query.php) yöntemini çağırır. Daha sonra bağlantıyı kapatmak için [mysqli_close](http://php.net/manual/mysqli.close.php) yöntemini çağırır.

host, username, password ve db_name parametre değerlerini kendi değerlerinizle değiştirin. 

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

## <a name="insert-data"></a>Veri ekleme
Bağlanmak ve **INSERT** SQL deyimi kullanarak veri eklemek için aşağıdaki kodu kullanın.

Kod, PHP'de bulunan **MySQL Improved extension** (mysqli) sınıfını kullanır. Kod, [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) yöntemini kullanarak hazır bir INSERT deyimi oluşturur, ardından [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php) yöntemini kullanarak, eklenen her bir sütun değerine ilişkin parametreleri bağlar. Kod, [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) yöntemini kullanarak deyimi çalıştırır ve ardından [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php) yöntemini kullanarak deyimi kapatır.

host, username, password ve db_name parametre değerlerini kendi değerlerinizle değiştirin. 

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

## <a name="read-data"></a>Verileri okuma
Bağlanmak ve **SELECT** SQL deyimi kullanarak verileri okumak için aşağıdaki kodu kullanın.  Kod, PHP'de bulunan **MySQL Improved extension** (mysqli) sınıfını kullanır. Kod, [mysqli_query](http://php.net/manual/mysqli.query.php) yöntemini kullanarak SQL sorgusunu gerçekleştirir ve [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) yöntemini kullanarak elde edilen satırları getirir.

host, username, password ve db_name parametre değerlerini kendi değerlerinizle değiştirin. 

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

## <a name="update-data"></a>Verileri güncelleştirme
Bağlanmak ve bir **UPDATE** SQL deyimi kullanarak verileri güncelleştirmek için aşağıdaki kodu kullanın.

Kod, PHP'de bulunan **MySQL Improved extension** (mysqli) sınıfını kullanır. Kod, [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) yöntemini kullanarak hazır bir UPDATE deyimi oluşturur, ardından [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php) yöntemini kullanarak, güncelleştirilen her bir sütun değerine ilişkin parametreleri bağlar. Kod, [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) yöntemini kullanarak deyimi çalıştırır ve ardından [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php) yöntemini kullanarak deyimi kapatır.

host, username, password ve db_name parametre değerlerini kendi değerlerinizle değiştirin. 

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


## <a name="delete-data"></a>Verileri silme
Bağlanmak ve **DELETE** SQL deyimi kullanarak verileri okumak için aşağıdaki kodu kullanın. 

Kod, PHP'de bulunan **MySQL Improved extension** (mysqli) sınıfını kullanır. Kod, [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) yöntemini kullanarak hazır bir DELETE deyimi oluşturur, ardından [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php) yöntemini kullanarak deyimdeki WHERE yan tümcesine ilişkin parametreleri bağlar. Kod, [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) yöntemini kullanarak deyimi çalıştırır ve ardından [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php) yöntemini kullanarak deyimi kapatır.

host, username, password ve db_name parametre değerlerini kendi değerlerinizle değiştirin. 

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

## <a name="next-steps"></a>Sonraki adımlar
> [!div class="nextstepaction"]
> [SSL aracılığıyla MySQL için Azure Veritabanı'na bağlanma] (howto-configure-ssl.md)
