---
title: "aaaUse PHP tooquery Azure SQL veritabanı | Microsoft Docs"
description: "Bu konu, nasıl gösterir toouse PHP toocreate tooan Azure SQL veritabanı ve sorgu Transact-SQL deyimi kullanarak bağlanan bir program."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 4e71db4a-a 22f-4f1c-83e5-4a34a036ecf3
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: hero-article
ms.date: 08/08/2017
ms.author: carlrab
ms.openlocfilehash: 5fc49dcc42ab07cc1bec554be39bdf08dbd6f75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-php-tooquery-an-azure-sql-database"></a>PHP tooquery Azure SQL veritabanını kullan

Bu hızlı başlangıç Öğreticisi gösteren nasıl toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate program tooconnect tooan Azure SQL veritabanı ve Transact-SQL deyimleri tooquery verileri kullanın.

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu hızlı başlangıç Öğreticisi, hello aşağıdaki sahip olduğunuzdan emin olun:

- Bir Azure SQL veritabanı. Bu hızlı başlangıç Bu hızlı başlangıçlar birinde oluşturulan hello kaynakları kullanır: 

   - [DB Oluşturma - Portal](sql-database-get-started-portal.md)
   - [DB oluşturma - CLI](sql-database-get-started-cli.md)
   - [DB Oluşturma - PowerShell](sql-database-get-started-powershell.md)

- A [sunucu düzeyinde güvenlik duvarı kuralı](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) hello için genel IP adresi hello bilgisayarın bu hızlı başlangıç öğreticisi için kullanın.

- İşletim sisteminiz için PHP ve ilgili yazılımları yüklediniz.

    - **MacOS**: Homebrew yükleyin ve PHP, hello ODBC sürücüsü ve SQLCMD yükleyin ve SQL Server için PHP sürücü hello yükleyin. Bkz. [Adım 1.2, 1.3 ve 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).
    - **Ubuntu**: PHP yüklemek ve diğer SQL Server için gerekli paketleri ve yükleme hello PHP sürücü. Bkz. [Adım 1.2 ve 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).
    - **Windows**: hello en yeni sürümünü yüklemek PHP için IIS Express, Microsoft SQL Server için Drivers IIS Express, Chocolatey, hello ODBC sürücüsü ve SQLCMD hello en yeni sürümü. Bkz. [Adım 1.2 ve 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).    

## <a name="sql-server-connection-information"></a>SQL Server bağlantı bilgileri

Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure SQL veritabanı alın. Merhaba tam sunucu adını, veritabanı adının ve oturum açma bilgilerini hello sonraki yordamlarda gerekir.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Seçin **SQL veritabanları** hello sol taraftaki menüden veritabanınızda hello tıklatıp **SQL veritabanları** sayfası. 
3. Merhaba üzerinde **genel bakış** gözden geçirme hello veritabanınız için sayfa hello görüntü aşağıdaki gösterildiği gibi sunucu adı tam olarak nitelenmiş. Merhaba sunucu adı toobring hello yukarı üzerine getirin **tıklatın toocopy** seçeneği.  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Sunucu oturum açma bilgilerinizi unutursanız, toohello SQL veritabanı sunucusu sayfa tooview hello sunucu yönetici adı gidin ve gerekiyorsa, sıfırlama, hello parola.     
    
## <a name="insert-code-tooquery-sql-database"></a>Kod tooquery SQL veritabanı Ekle

1. Sık kullandığınız metin düzenleyicisinde **sqltest.php** adında yeni bir dosya oluşturun.  

2. Aşağıdaki kod ve sunucu, veritabanı, kullanıcı ve parola için uygun değerleri hello ekleme hello Hello içeriğini değiştirin.

   ```PHP
   <?php
   $serverName = "your_server.database.windows.net";
   $connectionOptions = array(
       "Database" => "your_database",
       "Uid" => "your_username",
       "PWD" => "your_password"
   );
   //Establishes hello connection
   $conn = sqlsrv_connect($serverName, $connectionOptions);
   $tsql= "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
           FROM [SalesLT].[ProductCategory] pc
           JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid";
   $getResults= sqlsrv_query($conn, $tsql);
   echo ("Reading data from table" . PHP_EOL);
   if ($getResults == FALSE)
       echo (sqlsrv_errors());
   while ($row = sqlsrv_fetch_array($getResults, SQLSRV_FETCH_ASSOC)) {
    echo ($row['CategoryName'] . " " . $row['ProductName'] . PHP_EOL);
   }
   sqlsrv_free_stmt($getResults);
   ?>
   ```

## <a name="run-hello-code"></a>Merhaba kodu çalıştırma

1. Merhaba komut isteminde aşağıdaki komutları hello çalıştırın:

   ```php
   php sqltest.php
   ```

2. Merhaba üst 20 satır döndürülür ve hello uygulama penceresini kapatın doğrulayın.

## <a name="next-steps"></a>Sonraki adımlar
- [İlk Azure SQL veritabanınızı tasarlama](sql-database-design-first-database.md)
- [SQL Server için Microsoft PHP Sürücüleri](https://github.com/Microsoft/msphpsql/)
- [Sorun bildirin veya soru sorun](https://github.com/Microsoft/msphpsql/issues)
