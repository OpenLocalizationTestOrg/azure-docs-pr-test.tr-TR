---
title: "aaaConnect tooAzure Ruby kullanarak PostgreSQL için veritabanı | Microsoft Docs"
description: "Bu hızlı başlangıç tooconnect kullanın ve Azure veritabanındaki verileri PostgreSQL için sorgu Söyleniş kod bir örnek sağlar."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: ruby
ms.topic: quickstart
ms.date: 06/30/2017
ms.openlocfilehash: 7a0c8c92023452b40ca19d76fa659744f3e9a236
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-ruby-tooconnect-and-query-data"></a>Azure veritabanı PostgreSQL için: kullanım Ruby tooconnect ve sorgu verileri
Bu hızlı başlangıç gösteren Azure tooconnect tooan veritabanı nasıl PostgreSQL kullanmak için bir [Ruby](https://www.ruby-lang.org) uygulama. Nasıl toouse SQL deyimleri tooquery, Ekle, Güncelleştir ve hello veritabanında bulunan verileri silme gösterir. Bu makale, yeni tooworking PostgreSQL için Azure veritabanıyla olan ancak bu, Ruby, kullanarak geliştirme ile bildiğinizi varsayar.

## <a name="prerequisites"></a>Ön koşullar
Bu hızlı başlangıç Bu kılavuzlara birini başlangıç noktası olarak oluşturulan hello kaynakları kullanır:
- [DB Oluşturma - Portal](quickstart-create-server-database-portal.md)
- [DB Oluşturma - Azure CLI](quickstart-create-server-database-azure-cli.md)

## <a name="install-ruby"></a>Ruby’yi yükleme
Ruby’yi kendi makinenize yükleyin. 

### <a name="windows"></a>Windows
- İndirme ve yükleme hello en son sürümünü [Ruby](http://rubyinstaller.org/downloads/).
- Merhaba hello MSI Yükleyicisi'nin ekran son, "Çalıştır 'ridk Yükleme' tooinstall MSYS2 ve geliştirme araç zinciri." diyor hello kutuyu işaretleyin Ardından **son** toolaunch hello sonraki yükleyici.
- Merhaba RubyInstaller2 için Windows Installer başlatır. 2 tooinstall hello MSYS2 depo güncelleştirmesi yazın. Tamamlandıktan ve toohello yükleme istemi döndürür sonra hello komut penceresini kapatın.
- Yeni bir komut istemi (cmd) hello Başlat menüsünden başlatın.
- Test hello Söyleniş yükleme `ruby -v` toosee hello sürümü yüklü.
- Test Hello Gem yüklemesi `gem -v` toosee hello sürümü yüklü.
- Merhaba komutu çalıştırarak Gem kullanarak Ruby için Hello PostgreSQL modülü oluşturmak `gem install pg`.

### <a name="macos"></a>macOS
- Merhaba komutu çalıştırarak Homebrew kullanarak Ruby yüklemek `brew install ruby`. Merhaba Ruby daha fazla yükleme seçenekleri için bkz [yükleme belgeleri](https://www.ruby-lang.org/en/documentation/installation/#homebrew)
- Test hello Söyleniş yükleme `ruby -v` toosee hello sürümü yüklü.
- Test Hello Gem yüklemesi `gem -v` toosee hello sürümü yüklü.
- Merhaba komutu çalıştırarak Gem kullanarak Ruby için Hello PostgreSQL modülü oluşturmak `gem install pg`.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- Ruby hello komutu çalıştırarak yükleyin `sudo apt-get install ruby-full`. Merhaba Ruby daha fazla yükleme seçenekleri için bkz [yükleme belgelerini](https://www.ruby-lang.org/en/documentation/installation/).
- Test hello Söyleniş yükleme `ruby -v` toosee hello sürümü yüklü.
- Merhaba komutu çalıştırarak için Gem Hello en son güncelleştirmeleri yükleyin `sudo gem update --system`.
- Test Hello Gem yüklemesi `gem -v` toosee hello sürümü yüklü.
- Merhaba komutu çalıştırarak Hello gcc, marka ve diğer yapı araçlarını yükleyin `sudo apt-get install build-essential`.
- Merhaba komutu çalıştırarak Hello PostgreSQL kitaplıkları yükleme `sudo apt-get install libpq-dev`.
- Merhaba komutu çalıştırarak GEM kullanarak hello Söyleniş pg modülü yapı `sudo gem install pg`.

## <a name="run-ruby-code"></a>Ruby kodunu çalıştırma 
- Merhaba kodu bir metin dosyasına kaydetmek ve gibi hello dosyasını dosya uzantısı .rb ile bir proje klasöre kaydedin `C:\rubypostgres\read.rb` veya`/home/username/rubypostgres/read.rb`
- toorun hello kod hello komut istemi başlatın veya kabuk bash. Proje klasörünüzdeki değişiklik dizine `cd rubypostgres`, hello komutu yazın `ruby read.rb` toorun Merhaba uygulaması.

## <a name="get-connection-information"></a>Bağlantı bilgilerini alma
Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure veritabanı için PostgreSQL alın. Tam sunucu adını ve oturum açma kimlik bilgileri hello gerekir.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Merhaba sol taraftaki menüden Azure portalında, **tüm kaynakları** ve oluşturduğunuz, gibi hello sunucu araması **mypgserver 20170401**.
3. Merhaba sunucu adına tıklatarak **mypgserver 20170401**.
4. Select hello sunucunun **genel bakış** sayfası. Merhaba Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.
 ![PostgreSQL için Azure Veritabanı - Sunucu Yöneticisi Oturum Açma Bilgileri](./media/connect-ruby/1-connection-string.png)
5. Sunucu oturum açma bilgilerinizi unutursanız, toohello gidin **genel bakış** sayfa tooview hello sunucu yönetici oturum açma adı. Gerekirse, hello parola sıfırlama.

## <a name="connect-and-create-a-table"></a>Bağlanma ve tablo oluşturma
Kullanım hello aşağıdakileri tooconnect kod ve kullanarak bir tablo oluşturmak **CREATE TABLE** SQL deyimi, arkasından **INSERT INTO** SQL deyimleri tooadd satırları hello tabloya.

Merhaba kodu kullanan bir [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) Oluşturucusu nesnesiyle [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure PostgreSQL için veritabanı. Yöntem çağrıları sonra [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello bırakma, CREATE TABLE ve INSERT INTO komutları. Merhaba kod hello kullanarak hatalarını denetler [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) sınıfı. Yöntem çağrıları sonra [çağrısının](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) sonlandırmadan önce tooclose hello bağlantı.

Hello yerine `host`, `database`, `user`, ve `password` dizeleri kendi değerlerinizle. 
```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase'

    # Drop previous table of same name if one exists
    connection.exec('DROP TABLE IF EXISTS inventory;')
    puts 'Finished dropping table (if existed).'

    # Drop previous table of same name if one exists.
    connection.exec('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);')
    puts 'Finished creating table.'

    # Insert some data into table.
    connection.exec("INSERT INTO inventory VALUES(1, 'banana', 150)")
    connection.exec("INSERT INTO inventory VALUES(2, 'orange', 154)")
    connection.exec("INSERT INTO inventory VALUES(3, 'apple', 100)")
    puts 'Inserted 3 rows of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="read-data"></a>Verileri okuma
Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **seçin** SQL deyimi. 

Merhaba kodu kullanan bir [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) Oluşturucusu nesnesiyle [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure PostgreSQL için veritabanı. Yöntem çağrıları sonra [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) sonuç kümesinde hello sonuçları tutma toorun hello SELECT komutu. Merhaba sonuç kümesi koleksiyonu hello kullanarak üzerinden yinelendiğinde `resultSet.each do` hello geçerli satır değerleri hello tutma döngü `row` değişkeni. Merhaba kod hello kullanarak hatalarını denetler [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) sınıfı. Yöntem çağrıları sonra [çağrısının](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) sonlandırmadan önce tooclose hello bağlantı.

Hello yerine `host`, `database`, `user`, ve `password` dizeleri kendi değerlerinizle. 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :database => dbname, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase.'

    resultSet = connection.exec('SELECT * from inventory;')
    resultSet.each do |row|
        puts 'Data row = (%s, %s, %s)' % [row['id'], row['name'], row['quantity']]
    end

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="update-data"></a>Verileri güncelleştirme
Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak veri güncelleştirme bir **güncelleştirme** SQL deyimi.

Merhaba kodu kullanan bir [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) Oluşturucusu nesnesiyle [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure PostgreSQL için veritabanı. Yöntem çağrıları sonra [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello güncelleştirme komutu. Merhaba kod hello kullanarak hatalarını denetler [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) sınıfı. Yöntem çağrıları sonra [çağrısının](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) sonlandırmadan önce tooclose hello bağlantı.

Hello yerine `host`, `database`, `user`, ve `password` dizeleri kendi değerlerinizle. 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase.'

    # Modify some data in table.
    connection.exec('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
    puts 'Updated 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```


## <a name="delete-data"></a>Verileri silme
Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **silmek** SQL deyimi. 

Merhaba kodu kullanan bir [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) Oluşturucusu nesnesiyle [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure PostgreSQL için veritabanı. Yöntem çağrıları sonra [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello güncelleştirme komutu. Merhaba kod hello kullanarak hatalarını denetler [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) sınıfı. Yöntem çağrıları sonra [çağrısının](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) sonlandırmadan önce tooclose hello bağlantı.

Hello yerine `host`, `database`, `user`, ve `password` dizeleri kendi değerlerinizle. 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection toodatabase.'

    # Modify some data in table.
    connection.exec('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="next-steps"></a>Sonraki adımlar
> [!div class="nextstepaction"]
> [Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme](./howto-migrate-using-export-and-import.md)
