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
# <a name="azure-database-for-postgresql-use-php-tooconnect-and-query-data"></a>Azure veritabanı PostgreSQL için: kullanım PHP tooconnect ve sorgu verileri
Bu hızlı başlangıç gösteren Azure tooconnect tooan veritabanı nasıl PostgreSQL kullanmak için bir [PHP](http://php.net/manual/intro-whatis.php) uygulama. Nasıl toouse SQL deyimleri tooquery, Ekle, Güncelleştir ve hello veritabanında bulunan verileri silme gösterir. Bu makale, yeni tooworking PostgreSQL için Azure veritabanıyla olan ancak bu, PHP, kullanarak geliştirme ile bildiğinizi varsayar.

## <a name="prerequisites"></a>Ön koşullar
Bu hızlı başlangıç Bu kılavuzlara birini başlangıç noktası olarak oluşturulan hello kaynakları kullanır:
- [DB Oluşturma - Portal](quickstart-create-server-database-portal.md)
- [DB Oluşturma - Azure CLI](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a>PHP’yi yükleme
PHP’yi kendi sunucunuza yükleyin veya PHP içeren bir Azure [web uygulaması](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) oluşturun.

### <a name="windows"></a>Windows
- [PHP 7.1.4 iş parçacığı güvenli olmayan (x64) sürümünü](http://windows.php.net/download#php-7.1) indirin
- PHP yükleme ve toohello başvuran [PHP el ile](http://php.net/manual/install.windows.php) daha fazla yapılandırma
- Merhaba kodu kullanan hello **pgsql** hello PHP yükleme dahil sınıfı (ext/php_pgsql.dll). 
- Etkin hello **pgsql** hello php.ini yapılandırma dosyası, genellikle konumundaki düzenleyerek uzantısı `C:\Program Files\PHP\v7.1\php.ini`. Merhaba yapılandırma dosyası hello metin içeren bir satır içermelidir `extension=php_pgsql.so`. Görüntülenmiyorsa, hello metin eklemek ve hello dosyasını kaydedin. Merhaba metin varsa, ancak noktalı virgül önekiyle açıklamalı hello metin hello noktalı kaldırarak açıklamadan çıkarın.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- [PHP 7.1.4 iş parçacığı güvenli olmayan (x64) sürümünü](http://php.net/downloads.php) indirin 
- PHP yükleme ve toohello başvuran [PHP el ile](http://php.net/manual/install.unix.php) daha fazla yapılandırma
- Merhaba kodu kullanan hello **pgsql** sınıfı (php_pgsql.so). `sudo apt-get install php-pgsql` öğesini çalıştırarak yükleyin.
- Etkin hello **pgsql** hello düzenleyerek uzantısı `/etc/php/7.0/mods-available/pgsql.ini` yapılandırma dosyası. Merhaba yapılandırma dosyası hello metin içeren bir satır içermelidir `extension=php_pgsql.so`. Görüntülenmiyorsa, hello metin eklemek ve hello dosyasını kaydedin. Merhaba metin varsa, ancak noktalı virgül önekiyle açıklamalı hello metin hello noktalı kaldırarak açıklamadan çıkarın.

### <a name="macos"></a>macOS
- [PHP 7.1.4 sürümünü](http://php.net/downloads.php) indirin
- PHP yükleme ve toohello başvuran [PHP el ile](http://php.net/manual/install.macosx.php) daha fazla yapılandırma

## <a name="get-connection-information"></a>Bağlantı bilgilerini alma
Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure veritabanı için PostgreSQL alın. Tam sunucu adını ve oturum açma kimlik bilgileri hello gerekir.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Merhaba sol taraftaki menüden Azure portalında, **tüm kaynakları** ve oluşturduğunuz, gibi hello sunucu araması **mypgserver 20170401**.
3. Merhaba sunucu adına tıklatarak **mypgserver 20170401**.
4. Select hello sunucunun **genel bakış** sayfası. Merhaba Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.
 ![PostgreSQL için Azure Veritabanı - Sunucu Yöneticisi Oturum Açma Bilgileri](./media/connect-php/1-connection-string.png)
5. Sunucu oturum açma bilgilerinizi unutursanız, toohello gidin **genel bakış** tooview hello sunucu yönetici oturum açma adı sayfasında ve gerekirse sıfırlamak hello parola.

## <a name="connect-and-create-a-table"></a>Bağlanma ve tablo oluşturma
Kullanım hello aşağıdakileri tooconnect kod ve kullanarak bir tablo oluşturmak **CREATE TABLE** SQL deyimi, arkasından **INSERT INTO** SQL deyimleri tooadd satırları hello tabloya.

Merhaba kod arama yönteminde [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure PostgreSQL için veritabanı. Yöntemini çağıran sonra [pg_query()](http://php.net/manual/en/function.pg-query.php) birkaç kez toorun çeşitli komutlar ve [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello ayrıntıları her zaman bir hata ortaya çıktıysa. Yöntem çağrıları sonra [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello bağlantı.

Hello yerine `$host`, `$database`, `$user`, ve `$password` kendi değerlerinizi parametrelerle. 

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

## <a name="read-data"></a>Verileri okuma
Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **seçin** SQL deyimi. 

 Merhaba kod arama yönteminde [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure PostgreSQL için veritabanı. Yöntemini çağıran sonra [pg_query()](http://php.net/manual/en/function.pg-query.php) hello sonuçları bir sonuç kümesinde tutma toorun hello SELECT komutu ve [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello ayrıntıları, bir hata oluştu.  tooread hello sonuç kümesi, yöntem [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) satır ve hello satır bir dizide verileri alındıktan sonra bir döngüde adlı `$row`, her dizi konumu sütunda her bir veri değerine sahip.  toofree hello sonuç kümesi, yöntem [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) olarak adlandırılır. Yöntem çağrıları sonra [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello bağlantı.

Hello yerine `$host`, `$database`, `$user`, ve `$password` kendi değerlerinizi parametrelerle. 

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

## <a name="update-data"></a>Verileri güncelleştirme
Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak veri güncelleştirme bir **güncelleştirme** SQL deyimi.

Merhaba kod arama yönteminde [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure PostgreSQL için veritabanı. Yöntemini çağıran sonra [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun bir komut ve [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello ayrıntıları, bir hata oluştu. Yöntem çağrıları sonra [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello bağlantı.

Hello yerine `$host`, `$database`, `$user`, ve `$password` kendi değerlerinizi parametrelerle. 

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


## <a name="delete-data"></a>Verileri silme
Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **silmek** SQL deyimi. 

 Merhaba kod arama yönteminde [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect PostgreSQL için çok Azure veritabanı. Yöntemini çağıran sonra [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun bir komut ve [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello ayrıntıları, bir hata oluştu. Yöntem çağrıları sonra [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello bağlantı.

Hello yerine `$host`, `$database`, `$user`, ve `$password` kendi değerlerinizi parametrelerle. 

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

## <a name="next-steps"></a>Sonraki adımlar
> [!div class="nextstepaction"]
> [Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme](./howto-migrate-using-export-and-import.md)
