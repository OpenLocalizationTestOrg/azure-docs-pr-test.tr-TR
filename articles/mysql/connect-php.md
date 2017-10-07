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
# <a name="azure-database-for-mysql-use-php-tooconnect-and-query-data"></a>Azure veritabanı için MySQL: kullanım PHP tooconnect ve sorgu verileri
Bu hızlı başlangıç gösteren Azure tooconnect tooan veritabanı nasıl MySQL kullanmak için bir [PHP](http://php.net/manual/intro-whatis.php) uygulama. Nasıl toouse SQL deyimleri tooquery, Ekle, Güncelleştir ve hello veritabanında bulunan verileri silme gösterir. Bu makale, Azure veritabanı için MySQL ile yeni tooworking olan ancak bu, PHP, kullanarak geliştirme ile bildiğinizi varsayar.

## <a name="prerequisites"></a>Ön koşullar
Bu hızlı başlangıç Bu kılavuzlara birini başlangıç noktası olarak oluşturulan hello kaynakları kullanır:
- [Azure portalını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Azure CLI kullanarak MySQL için Azure Veritabanı sunucusu oluşturma](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-php"></a>PHP'yi yükleme
PHP'yi kendi sunucunuza yükleyin veya PHP içeren bir Azure [web uygulaması](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) oluşturun.

### <a name="macos"></a>macOS
- [PHP 7.1.4 sürümünü](http://php.net/downloads.php) indirin
- PHP yükleme ve toohello başvuran [PHP el ile](http://php.net/manual/install.macosx.php) daha fazla yapılandırma

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- [PHP 7.1.4 iş parçacığı güvenli olmayan (x64) sürümünü](http://php.net/downloads.php) indirin
- PHP yükleme ve toohello başvuran [PHP el ile](http://php.net/manual/install.unix.php) daha fazla yapılandırma

### <a name="windows"></a>Windows
- [PHP 7.1.4 iş parçacığı güvenli olmayan (x64) sürümünü](http://windows.php.net/download#php-7.1) indirin
- PHP yükleme ve toohello başvuran [PHP el ile](http://php.net/manual/install.windows.php) daha fazla yapılandırma

## <a name="get-connection-information"></a>Bağlantı bilgilerini alma
Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure veritabanı için MySQL alın. Tam sunucu adını ve oturum açma kimlik bilgileri hello gerekir.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Merhaba sol bölmede **tüm kaynakları**ve ardından oluşturduğunuz hello sunucusu için arama (örneğin, **myserver4demo**).
3. Merhaba sunucu adına tıklayın.
4. Select hello sunucunun **özellikleri** sayfası. Merhaba Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.
 ![MySQL için Azure Veritabanı sunucu adı](./media/connect-php/1_server-properties-name-login.png)
5. Sunucu oturum açma bilgilerinizi unutursanız, toohello gidin **genel bakış** tooview hello sunucu yönetici oturum açma adı sayfasında ve gerekirse sıfırlamak hello parola.

## <a name="connect-and-create-a-table"></a>Bağlanma ve tablo oluşturma
Kullanım hello aşağıdakileri tooconnect kod ve kullanarak bir tablo oluşturmak **CREATE TABLE** SQL deyimi. 

Merhaba kodu kullanan hello **uzantısı MySQL geliştirilmiş** PHP ile dahil (mysqli) sınıfı. Merhaba yöntemleri kod çağırabilir [mysqli_init](http://php.net/manual/mysqli.init.php) ve [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL. Yöntem çağrıları sonra [mysqli_query](http://php.net/manual/mysqli.query.php) toorun hello sorgu. Yöntem çağrıları sonra [mysqli_close](http://php.net/manual/mysqli.close.php) tooclose hello bağlantı.

Merhaba ana bilgisayar, kullanıcı adı, parola ve db_name parametreleri kendi değerlerinizle değiştirin. 

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

## <a name="insert-data"></a>Veri ekleme
Kullanım hello aşağıdakileri tooconnect kod ve verileri kullanarak Ekle bir **Ekle** SQL deyimi.

Merhaba kodu kullanan hello **uzantısı MySQL geliştirilmiş** PHP ile dahil (mysqli) sınıfı. Merhaba kodu yöntemi kullanan [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate hazırlanmış bir deyim ekleyin, sonra parametreleri yöntemi kullanarak her eklenen sütun değeri için bağlar hello [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php). Merhaba kodu çalıştırır yöntemini kullanarak hello deyimi [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) ve daha sonra kapanır yöntemini kullanarak deyimi hello [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).

Merhaba ana bilgisayar, kullanıcı adı, parola ve db_name parametreleri kendi değerlerinizle değiştirin. 

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

## <a name="read-data"></a>Verileri okuma
Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **seçin** SQL deyimi.  Merhaba kodu kullanan hello **uzantısı MySQL geliştirilmiş** PHP ile dahil (mysqli) sınıfı. Merhaba kodu yöntemi kullanan [mysqli_query](http://php.net/manual/mysqli.query.php) hello sql sorgusu ve kullandığı gerçekleştirmek [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) yöntemi toofetch hello elde edilen satırları.

Merhaba ana bilgisayar, kullanıcı adı, parola ve db_name parametreleri kendi değerlerinizle değiştirin. 

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

## <a name="update-data"></a>Verileri güncelleştirme
Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak veri güncelleştirme bir **güncelleştirme** SQL deyimi.

Merhaba kodu kullanan hello **uzantısı MySQL geliştirilmiş** PHP ile dahil (mysqli) sınıfı. Merhaba kodu yöntemi kullanan [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate hazırlıklı güncelleştirme bildirimi ardından hello parametreleri yöntemi kullanarak her güncelleştirilmiş sütun değeri için bağlar [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php). Merhaba kodu çalıştırır yöntemini kullanarak hello deyimi [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) ve daha sonra kapanır yöntemini kullanarak deyimi hello [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).

Merhaba ana bilgisayar, kullanıcı adı, parola ve db_name parametreleri kendi değerlerinizle değiştirin. 

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


## <a name="delete-data"></a>Verileri silme
Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **silmek** SQL deyimi. 

Merhaba kodu kullanan hello **uzantısı MySQL geliştirilmiş** PHP ile dahil (mysqli) sınıfı. Hello kodu kullanan yöntemi [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate bir hazırlıklı deyimi silin, ardından bağlamalar hello hello parametrelerini burada yöntemini kullanarak hello deyimindeki yan tümcesi [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php). Merhaba kodu çalıştırır yöntemini kullanarak hello deyimi [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) ve daha sonra kapanır yöntemini kullanarak deyimi hello [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).

Merhaba ana bilgisayar, kullanıcı adı, parola ve db_name parametreleri kendi değerlerinizle değiştirin. 

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

## <a name="next-steps"></a>Sonraki adımlar
> [!div class="nextstepaction"]
> [Azure'da PHP ve MySQL web uygulaması oluşturma](../app-service-web/app-service-web-tutorial-php-mysql.md?toc=%2fazure%2fmysql%2ftoc.json)
