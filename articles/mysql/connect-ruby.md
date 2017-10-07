---
title: "TooAzure veritabanı için MySQL Ruby kullanarak bağlanma | Microsoft Docs"
description: "Bu hızlı başlangıç MySQL için Azure veritabanındaki verileri sorgulamak ve tooconnect için kullanabileceğiniz birkaç Söyleniş kod örnekleri sağlar."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: ruby
ms.topic: hero-article
ms.date: 07/13/2017
ms.openlocfilehash: ff0880dcc24e96f467c9092bc663ce3dc4c2637a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-ruby-tooconnect-and-query-data"></a>Azure veritabanı için MySQL: kullanım Ruby tooconnect ve sorgu verileri
Bu hızlı başlangıç gösteren Azure tooconnect tooan veritabanı nasıl MySQL kullanmak için bir [Ruby](https://www.ruby-lang.org) uygulama ve hello [mysql2](https://rubygems.org/gems/mysql2) Windows, Ubuntu Linux ve Mac platformları gelen gem. Nasıl toouse SQL deyimleri tooquery, Ekle, Güncelleştir ve hello veritabanında bulunan verileri silme gösterir. Bu makale, Azure veritabanı için MySQL ile yeni tooworking olan ancak bu, Ruby, kullanarak geliştirme ile bildiğinizi varsayar.

## <a name="prerequisites"></a>Ön koşullar
Bu hızlı başlangıç Bu kılavuzlara birini başlangıç noktası olarak oluşturulan hello kaynakları kullanır:
- [Azure portalını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Azure CLI kullanarak MySQL için Azure Veritabanı sunucusu oluşturma](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-ruby"></a>Ruby’yi yükleme
Ruby, Gem ve hello MySQL2 kitaplık kendi makineye yükleyin. 

### <a name="windows"></a>Windows
1. İndirme ve yükleme hello 2.3 sürümü [Ruby](http://rubyinstaller.org/downloads/).
2. Yeni bir komut istemi (cmd) hello Başlat menüsünden başlatın.
3. Merhaba sürüm 2.3 Söyleniş dizini içine dizini değiştirin. `cd c:\Ruby23-x64\bin`
4. Test hello hello komutunu çalıştırarak Söyleniş yükleme `ruby -v` toosee hello sürümü yüklü.
5. Merhaba komutu çalıştırarak test Hello Gem yüklemesi `gem -v` toosee hello sürümü yüklü.
6. Merhaba komutu çalıştırarak Gem kullanarak Ruby için Hello Mysql2 modülü oluşturmak `gem install mysql2`.

### <a name="macos"></a>macOS
1. Merhaba komutu çalıştırarak Homebrew kullanarak Ruby yüklemek `brew install ruby`. Merhaba Ruby daha fazla yükleme seçenekleri için bkz [yükleme belgelerini](https://www.ruby-lang.org/en/documentation/installation/#homebrew).
2. Test hello hello komutunu çalıştırarak Söyleniş yükleme `ruby -v` toosee hello sürümü yüklü.
3. Merhaba komutu çalıştırarak test Hello Gem yüklemesi `gem -v` toosee hello sürümü yüklü.
4. Merhaba komutu çalıştırarak Gem kullanarak Ruby için Hello Mysql2 modülü oluşturmak `gem install mysql2`.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. Ruby hello komutu çalıştırarak yükleyin `sudo apt-get install ruby-full`. Merhaba Ruby daha fazla yükleme seçenekleri için bkz [yükleme belgelerini](https://www.ruby-lang.org/en/documentation/installation/).
2. Test hello hello komutunu çalıştırarak Söyleniş yükleme `ruby -v` toosee hello sürümü yüklü.
3. Merhaba komutu çalıştırarak için Gem Hello en son güncelleştirmeleri yükleyin `sudo gem update --system`.
4. Merhaba komutu çalıştırarak test Hello Gem yüklemesi `gem -v` toosee hello sürümü yüklü.
5. Merhaba komutu çalıştırarak Hello gcc, marka ve diğer yapı araçlarını yükleyin `sudo apt-get install build-essential`.
6. Merhaba komutu çalıştırarak Hello MySQL istemci geliştirici kitaplıkları yükleme `sudo apt-get install libmysqlclient-dev`.
7. Merhaba komutu çalıştırarak Gem kullanarak Ruby için Hello mysql2 modülü oluşturmak `sudo gem install mysql2`.

## <a name="get-connection-information"></a>Bağlantı bilgilerini alma
Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure veritabanı için MySQL alın. Tam sunucu adını ve oturum açma kimlik bilgileri hello gerekir.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Merhaba sol taraftaki menüden Azure portalında, **tüm kaynakları** ve aramak için creased, gibi hello sunucu **myserver4demo**.
3. Merhaba sunucu adına tıklatarak **myserver4demo**.
4. Select hello sunucunun **özellikleri** sayfası. Merhaba Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.
 ![MySQL için Azure Veritabanı - Sunucu Yöneticisi Oturum Açma](./media/connect-ruby/1_server-properties-name-login.png)
5. Sunucu oturum açma bilgilerinizi unutursanız, toohello gidin **genel bakış** tooview hello sunucu yönetici oturum açma adı sayfasında ve gerekirse sıfırlamak hello parola.

## <a name="run-ruby-code"></a>Ruby kodunu çalıştırma 
1. Hello hello bölümlere Söyleniş koddan metin dosyasına yapıştırın ve gibi hello dosyaları dosya uzantısı .rb ile bir proje klasöre kaydedin `C:\rubymysql\createtable.rb` veya `/home/username/rubymysql/createtable.rb`.
2. toorun hello kod hello komut istemi başlatın veya kabuk bash. Dizini değiştirerek, proje klasörünüze geçin (`cd rubymysql`)
3. Ardından hello dosya adı, gibi hello Söyleniş komutu yazın `ruby createtable.rb` toorun Merhaba uygulaması.
4. Merhaba ruby uygulaması path ortam değişkeni içinde değilse hello Windows işletim sistemi, toouse hello tam yolu toolaunch hello düğüm uygulama gibi ihtiyacınız`"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`

## <a name="connect-and-create-a-table"></a>Bağlanma ve tablo oluşturma
Kullanım hello aşağıdakileri tooconnect kod ve kullanarak bir tablo oluşturmak **CREATE TABLE** SQL deyimi, arkasından **INSERT INTO** SQL deyimleri tooadd satırları hello tabloya.

Merhaba kodu kullanan bir [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new() yöntemi tooconnect tooAzure veritabanı için MySQL sınıfı. Yöntem çağrıları sonra [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) birkaç kez toorun hello bırakma, CREATE TABLE ve INSERT INTO komutları. Yöntem çağrıları sonra [çağrısının](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) sonlandırmadan önce tooclose hello bağlantı.

Hello yerine `host`, `database`, `username`, ve `password` dizeleri kendi değerlerinizle. 
```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Drop previous table of same name if one exists
    client.query('DROP TABLE IF EXISTS inventory;')
    puts 'Finished dropping table (if existed).'

    # Drop previous table of same name if one exists.
    client.query('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);')
    puts 'Finished creating table.'

    # Insert some data into table.
    client.query("INSERT INTO inventory VALUES(1, 'banana', 150)")
    client.query("INSERT INTO inventory VALUES(2, 'orange', 154)")
    client.query("INSERT INTO inventory VALUES(3, 'apple', 100)")
    puts 'Inserted 3 rows of data.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="read-data"></a>Verileri okuma
Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **seçin** SQL deyimi. 

Merhaba kodu kullanan bir [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new() yöntemi tooconnect tooAzure veritabanı için MySQL sınıfı. Yöntem çağrıları sonra [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello SELECT komutları. Yöntem çağrıları sonra [çağrısının](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) sonlandırmadan önce tooclose hello bağlantı.

Hello yerine `host`, `database`, `username`, ve `password` dizeleri kendi değerlerinizle. 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Read data
    resultSet = client.query('SELECT * from inventory;')
    resultSet.each do |row|
        puts 'Data row = (%s, %s, %s)' % [row['id'], row['name'], row['quantity']]
    end
    puts 'Read ' + resultSet.count.to_s + ' row(s).'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="update-data"></a>Verileri güncelleştirme
Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak veri güncelleştirme bir **güncelleştirme** SQL deyimi.

Merhaba kodu kullanan bir [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new() yöntemi tooconnect tooAzure veritabanı için MySQL sınıfı. Yöntem çağrıları sonra [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello güncelleştirme komutları. Yöntem çağrıları sonra [çağrısının](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) sonlandırmadan önce tooclose hello bağlantı.

Hello yerine `host`, `database`, `username`, ve `password` dizeleri kendi değerlerinizle. 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Update data
   client.query('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
   puts 'Updated 1 row of data.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```


## <a name="delete-data"></a>Verileri silme
Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **silmek** SQL deyimi. 

Merhaba kodu kullanan bir [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new() yöntemi tooconnect tooAzure veritabanı için MySQL sınıfı. Yöntem çağrıları sonra [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello Sil komutları. Yöntem çağrıları sonra [çağrısının](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) sonlandırmadan önce tooclose hello bağlantı.

Hello yerine `host`, `database`, `username`, ve `password` dizeleri kendi değerlerinizle. 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Delete data
    resultSet = client.query('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="next-steps"></a>Sonraki adımlar
> [!div class="nextstepaction"]
> [Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme](./concepts-migrate-import-export.md)
