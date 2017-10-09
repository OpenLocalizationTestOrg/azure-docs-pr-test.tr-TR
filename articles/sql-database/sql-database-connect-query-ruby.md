---
title: "aaaUse Söyleniş tooquery Azure SQL veritabanı | Microsoft Docs"
description: "Bu konu, nasıl gösterir toouse Söyleniş toocreate tooan Azure SQL veritabanı ve sorgu Transact-SQL deyimi kullanarak bağlanan bir program."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 94fec528-58ba-4352-ba0d-25ae4b273e90
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: hero-article
ms.date: 07/14/2017
ms.author: carlrab
ms.openlocfilehash: 0d4b16b8aacb5e376ab80cbe37569130f2fd52b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ruby-tooquery-an-azure-sql-database"></a>Söyleniş tooquery Azure SQL veritabanını kullan

Bu hızlı başlangıç Öğreticisi gösteren nasıl toouse [Ruby](https://www.ruby-lang.org) toocreate program tooconnect tooan Azure SQL veritabanı ve Transact-SQL deyimleri tooquery verileri kullanın.

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu hızlı başlangıç Öğreticisi, Önkoşullar aşağıdaki hello sahip olduğunuzdan emin olun:

- Bir Azure SQL veritabanı. Bu hızlı başlangıç Bu hızlı başlangıçlar birinde oluşturulan hello kaynakları kullanır: 

   - [DB Oluşturma - Portal](sql-database-get-started-portal.md)
   - [DB oluşturma - CLI](sql-database-get-started-cli.md)
   - [DB Oluşturma - PowerShell](sql-database-get-started-powershell.md)

- A [sunucu düzeyinde güvenlik duvarı kuralı](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) hello için genel IP adresi hello bilgisayarın bu hızlı başlangıç öğreticisi için kullanın.
- İşletim sisteminiz için Ruby ve ilgili yazılımları yüklediniz.
    - **MacOS**: Homebrew'i, rbenv ve ruby-build'i, Ruby'yi ve sonra da FreeTDS'yi yükleyin. Bkz: [1.2, 1.3, 1.4 ve 1.5 adımları](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).
    - **Ubuntu**: Ruby'nin önkoşullarını yükleyin, rbenv ve ruby-build'i, Ruby'yi ve sonra da FreeTDS'yi yükleyin. Bkz: [1.2, 1.3, 1.4 ve 1.5 adımları](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).

## <a name="sql-server-connection-information"></a>SQL Server bağlantı bilgileri

Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure SQL veritabanı alın. Merhaba tam sunucu adını, veritabanı adının ve oturum açma bilgilerini hello sonraki yordamlarda gerekir.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Seçin **SQL veritabanları** hello sol taraftaki menüden veritabanınızda hello tıklatıp **SQL veritabanları** sayfası. 
3. Merhaba üzerinde **genel bakış** sayfasında veritabanınız için hello tam sunucu adını gözden geçirin. Hello sunucu adı toobring hello yukarı üzerine getirin **tıklatın toocopy** hello görüntü aşağıdaki gösterildiği gibi seçeneği:

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Merhaba oturum açma bilgilerini Azure SQL veritabanı sunucunuz için unuttuysanız, toohello SQL veritabanı sunucusu sayfa tooview hello sunucu yönetici adı gidin ve gerekiyorsa, sıfırlama, hello parola.

> [!IMPORTANT]
> Bu öğreticiyi gerçekleştirme hello bilgisayarın hello ortak IP adresi için yerinde bir güvenlik duvarı kuralı olması gerekir. Farklı bir bilgisayarda olan veya farklı bir ortak IP adresi varsa, oluşturma bir [sunucu düzeyinde güvenlik duvarı kuralı kullanarak hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule). 

## <a name="insert-code-tooquery-sql-database"></a>Kod tooquery SQL veritabanı Ekle

1. Sık kullandığınız metin düzenleyicisinde **sqltest.rb** adında yeni bir dosya oluşturun

2. Aşağıdaki kod ve sunucu, veritabanı, kullanıcı ve parola için uygun değerleri hello ekleme hello Hello içeriğini değiştirin.

```ruby
require 'tiny_tds'
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
client = TinyTds::Client.new username: username, password: password, 
    host: server, port: 1433, database: database, azure: true

puts "Reading data from table"
tsql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
        FROM [SalesLT].[ProductCategory] pc
        JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid"
result = client.execute(tsql)
result.each do |row|
    puts row
end
```

## <a name="run-hello-code"></a>Merhaba kodu çalıştırma

1. Merhaba komut isteminde aşağıdaki komutları hello çalıştırın:

   ```bash
   ruby sqltest.rb
   ```

2. Merhaba üst 20 satır döndürülür ve hello uygulama penceresini kapatın doğrulayın.


## <a name="next-steps"></a>Sonraki Adımlar
- [İlk Azure SQL veritabanınızı tasarlama](sql-database-design-first-database.md)
- [TinyTDS için GitHub deposu](https://github.com/rails-sqlserver/tiny_tds)
- [TinyTDS hakkında sorun bildirin veya soru sorun](https://github.com/rails-sqlserver/tiny_tds/issues)
- [SQL Server için Ruby Sürücüleri](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/)
