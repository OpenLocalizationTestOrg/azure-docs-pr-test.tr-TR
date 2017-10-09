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
# <a name="azure-database-for-postgresql-use-ruby-tooconnect-and-query-data"></a><span data-ttu-id="dc41e-103">Azure veritabanı PostgreSQL için: kullanım Ruby tooconnect ve sorgu verileri</span><span class="sxs-lookup"><span data-stu-id="dc41e-103">Azure Database for PostgreSQL: Use Ruby tooconnect and query data</span></span>
<span data-ttu-id="dc41e-104">Bu hızlı başlangıç gösteren Azure tooconnect tooan veritabanı nasıl PostgreSQL kullanmak için bir [Ruby](https://www.ruby-lang.org) uygulama.</span><span class="sxs-lookup"><span data-stu-id="dc41e-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a [Ruby](https://www.ruby-lang.org) application.</span></span> <span data-ttu-id="dc41e-105">Nasıl toouse SQL deyimleri tooquery, Ekle, Güncelleştir ve hello veritabanında bulunan verileri silme gösterir.</span><span class="sxs-lookup"><span data-stu-id="dc41e-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="dc41e-106">Bu makale, yeni tooworking PostgreSQL için Azure veritabanıyla olan ancak bu, Ruby, kullanarak geliştirme ile bildiğinizi varsayar.</span><span class="sxs-lookup"><span data-stu-id="dc41e-106">This article assumes you are familiar with development using Ruby, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc41e-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="dc41e-107">Prerequisites</span></span>
<span data-ttu-id="dc41e-108">Bu hızlı başlangıç Bu kılavuzlara birini başlangıç noktası olarak oluşturulan hello kaynakları kullanır:</span><span class="sxs-lookup"><span data-stu-id="dc41e-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="dc41e-109">DB Oluşturma - Portal</span><span class="sxs-lookup"><span data-stu-id="dc41e-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="dc41e-110">DB Oluşturma - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="dc41e-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="dc41e-111">Ruby’yi yükleme</span><span class="sxs-lookup"><span data-stu-id="dc41e-111">Install Ruby</span></span>
<span data-ttu-id="dc41e-112">Ruby’yi kendi makinenize yükleyin.</span><span class="sxs-lookup"><span data-stu-id="dc41e-112">Install Ruby on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="dc41e-113">Windows</span><span class="sxs-lookup"><span data-stu-id="dc41e-113">Windows</span></span>
- <span data-ttu-id="dc41e-114">İndirme ve yükleme hello en son sürümünü [Ruby](http://rubyinstaller.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="dc41e-114">Download and Install hello latest version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
- <span data-ttu-id="dc41e-115">Merhaba hello MSI Yükleyicisi'nin ekran son, "Çalıştır 'ridk Yükleme' tooinstall MSYS2 ve geliştirme araç zinciri." diyor hello kutuyu işaretleyin</span><span class="sxs-lookup"><span data-stu-id="dc41e-115">On hello finish screen of hello MSI installer, check hello box that says "Run 'ridk install' tooinstall MSYS2 and development toolchain."</span></span> <span data-ttu-id="dc41e-116">Ardından **son** toolaunch hello sonraki yükleyici.</span><span class="sxs-lookup"><span data-stu-id="dc41e-116">Then click **Finish** toolaunch hello next installer.</span></span>
- <span data-ttu-id="dc41e-117">Merhaba RubyInstaller2 için Windows Installer başlatır.</span><span class="sxs-lookup"><span data-stu-id="dc41e-117">hello RubyInstaller2 for Windows installer launches.</span></span> <span data-ttu-id="dc41e-118">2 tooinstall hello MSYS2 depo güncelleştirmesi yazın.</span><span class="sxs-lookup"><span data-stu-id="dc41e-118">Type 2 tooinstall hello MSYS2 repository update.</span></span> <span data-ttu-id="dc41e-119">Tamamlandıktan ve toohello yükleme istemi döndürür sonra hello komut penceresini kapatın.</span><span class="sxs-lookup"><span data-stu-id="dc41e-119">After it finishes and returns toohello installation prompt, close hello command window.</span></span>
- <span data-ttu-id="dc41e-120">Yeni bir komut istemi (cmd) hello Başlat menüsünden başlatın.</span><span class="sxs-lookup"><span data-stu-id="dc41e-120">Launch a new command prompt (cmd) from hello Start menu.</span></span>
- <span data-ttu-id="dc41e-121">Test hello Söyleniş yükleme `ruby -v` toosee hello sürümü yüklü.</span><span class="sxs-lookup"><span data-stu-id="dc41e-121">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="dc41e-122">Test Hello Gem yüklemesi `gem -v` toosee hello sürümü yüklü.</span><span class="sxs-lookup"><span data-stu-id="dc41e-122">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="dc41e-123">Merhaba komutu çalıştırarak Gem kullanarak Ruby için Hello PostgreSQL modülü oluşturmak `gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="dc41e-123">Build hello PostgreSQL module for Ruby using Gem by running hello command `gem install pg`.</span></span>

### <a name="macos"></a><span data-ttu-id="dc41e-124">macOS</span><span class="sxs-lookup"><span data-stu-id="dc41e-124">MacOS</span></span>
- <span data-ttu-id="dc41e-125">Merhaba komutu çalıştırarak Homebrew kullanarak Ruby yüklemek `brew install ruby`.</span><span class="sxs-lookup"><span data-stu-id="dc41e-125">Install Ruby using Homebrew by running hello command `brew install ruby`.</span></span> <span data-ttu-id="dc41e-126">Merhaba Ruby daha fazla yükleme seçenekleri için bkz [yükleme belgeleri](https://www.ruby-lang.org/en/documentation/installation/#homebrew)</span><span class="sxs-lookup"><span data-stu-id="dc41e-126">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew)</span></span>
- <span data-ttu-id="dc41e-127">Test hello Söyleniş yükleme `ruby -v` toosee hello sürümü yüklü.</span><span class="sxs-lookup"><span data-stu-id="dc41e-127">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="dc41e-128">Test Hello Gem yüklemesi `gem -v` toosee hello sürümü yüklü.</span><span class="sxs-lookup"><span data-stu-id="dc41e-128">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="dc41e-129">Merhaba komutu çalıştırarak Gem kullanarak Ruby için Hello PostgreSQL modülü oluşturmak `gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="dc41e-129">Build hello PostgreSQL module for Ruby using Gem by running hello command `gem install pg`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="dc41e-130">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="dc41e-130">Linux (Ubuntu)</span></span>
- <span data-ttu-id="dc41e-131">Ruby hello komutu çalıştırarak yükleyin `sudo apt-get install ruby-full`.</span><span class="sxs-lookup"><span data-stu-id="dc41e-131">Install Ruby by running hello command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="dc41e-132">Merhaba Ruby daha fazla yükleme seçenekleri için bkz [yükleme belgelerini](https://www.ruby-lang.org/en/documentation/installation/).</span><span class="sxs-lookup"><span data-stu-id="dc41e-132">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
- <span data-ttu-id="dc41e-133">Test hello Söyleniş yükleme `ruby -v` toosee hello sürümü yüklü.</span><span class="sxs-lookup"><span data-stu-id="dc41e-133">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="dc41e-134">Merhaba komutu çalıştırarak için Gem Hello en son güncelleştirmeleri yükleyin `sudo gem update --system`.</span><span class="sxs-lookup"><span data-stu-id="dc41e-134">Install hello latest updates for Gem by running hello command `sudo gem update --system`.</span></span>
- <span data-ttu-id="dc41e-135">Test Hello Gem yüklemesi `gem -v` toosee hello sürümü yüklü.</span><span class="sxs-lookup"><span data-stu-id="dc41e-135">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="dc41e-136">Merhaba komutu çalıştırarak Hello gcc, marka ve diğer yapı araçlarını yükleyin `sudo apt-get install build-essential`.</span><span class="sxs-lookup"><span data-stu-id="dc41e-136">Install hello gcc, make, and other build tools by running hello command `sudo apt-get install build-essential`.</span></span>
- <span data-ttu-id="dc41e-137">Merhaba komutu çalıştırarak Hello PostgreSQL kitaplıkları yükleme `sudo apt-get install libpq-dev`.</span><span class="sxs-lookup"><span data-stu-id="dc41e-137">Install hello PostgreSQL libraries by running hello command `sudo apt-get install libpq-dev`.</span></span>
- <span data-ttu-id="dc41e-138">Merhaba komutu çalıştırarak GEM kullanarak hello Söyleniş pg modülü yapı `sudo gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="dc41e-138">Build hello Ruby pg module using Gem by running hello command `sudo gem install pg`.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="dc41e-139">Ruby kodunu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="dc41e-139">Run Ruby code</span></span> 
- <span data-ttu-id="dc41e-140">Merhaba kodu bir metin dosyasına kaydetmek ve gibi hello dosyasını dosya uzantısı .rb ile bir proje klasöre kaydedin `C:\rubypostgres\read.rb` veya`/home/username/rubypostgres/read.rb`</span><span class="sxs-lookup"><span data-stu-id="dc41e-140">Save hello code into a text file, and save hello file into a project folder with file extension .rb, such as `C:\rubypostgres\read.rb` or `/home/username/rubypostgres/read.rb`</span></span>
- <span data-ttu-id="dc41e-141">toorun hello kod hello komut istemi başlatın veya kabuk bash.</span><span class="sxs-lookup"><span data-stu-id="dc41e-141">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="dc41e-142">Proje klasörünüzdeki değişiklik dizine `cd rubypostgres`, hello komutu yazın `ruby read.rb` toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="dc41e-142">Change directory into your project folder `cd rubypostgres`, then type hello command `ruby read.rb` toorun hello application.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="dc41e-143">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="dc41e-143">Get connection information</span></span>
<span data-ttu-id="dc41e-144">Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure veritabanı için PostgreSQL alın.</span><span class="sxs-lookup"><span data-stu-id="dc41e-144">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="dc41e-145">Tam sunucu adını ve oturum açma kimlik bilgileri hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="dc41e-145">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="dc41e-146">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="dc41e-146">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="dc41e-147">Merhaba sol taraftaki menüden Azure portalında, **tüm kaynakları** ve oluşturduğunuz, gibi hello sunucu araması **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="dc41e-147">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="dc41e-148">Merhaba sunucu adına tıklatarak **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="dc41e-148">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="dc41e-149">Select hello sunucunun **genel bakış** sayfası.</span><span class="sxs-lookup"><span data-stu-id="dc41e-149">Select hello server's **Overview** page.</span></span> <span data-ttu-id="dc41e-150">Merhaba Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.</span><span class="sxs-lookup"><span data-stu-id="dc41e-150">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="dc41e-151">![PostgreSQL için Azure Veritabanı - Sunucu Yöneticisi Oturum Açma Bilgileri](./media/connect-ruby/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="dc41e-151">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-ruby/1-connection-string.png)</span></span>
5. <span data-ttu-id="dc41e-152">Sunucu oturum açma bilgilerinizi unutursanız, toohello gidin **genel bakış** sayfa tooview hello sunucu yönetici oturum açma adı.</span><span class="sxs-lookup"><span data-stu-id="dc41e-152">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name.</span></span> <span data-ttu-id="dc41e-153">Gerekirse, hello parola sıfırlama.</span><span class="sxs-lookup"><span data-stu-id="dc41e-153">If necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="dc41e-154">Bağlanma ve tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="dc41e-154">Connect and create a table</span></span>
<span data-ttu-id="dc41e-155">Kullanım hello aşağıdakileri tooconnect kod ve kullanarak bir tablo oluşturmak **CREATE TABLE** SQL deyimi, arkasından **INSERT INTO** SQL deyimleri tooadd satırları hello tabloya.</span><span class="sxs-lookup"><span data-stu-id="dc41e-155">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="dc41e-156">Merhaba kodu kullanan bir [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) Oluşturucusu nesnesiyle [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure PostgreSQL için veritabanı.</span><span class="sxs-lookup"><span data-stu-id="dc41e-156">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="dc41e-157">Yöntem çağrıları sonra [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello bırakma, CREATE TABLE ve INSERT INTO komutları.</span><span class="sxs-lookup"><span data-stu-id="dc41e-157">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="dc41e-158">Merhaba kod hello kullanarak hatalarını denetler [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="dc41e-158">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="dc41e-159">Yöntem çağrıları sonra [çağrısının](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) sonlandırmadan önce tooclose hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="dc41e-159">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="dc41e-160">Hello yerine `host`, `database`, `user`, ve `password` dizeleri kendi değerlerinizle.</span><span class="sxs-lookup"><span data-stu-id="dc41e-160">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 
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

## <a name="read-data"></a><span data-ttu-id="dc41e-161">Verileri okuma</span><span class="sxs-lookup"><span data-stu-id="dc41e-161">Read data</span></span>
<span data-ttu-id="dc41e-162">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **seçin** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="dc41e-162">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="dc41e-163">Merhaba kodu kullanan bir [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) Oluşturucusu nesnesiyle [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure PostgreSQL için veritabanı.</span><span class="sxs-lookup"><span data-stu-id="dc41e-163">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="dc41e-164">Yöntem çağrıları sonra [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) sonuç kümesinde hello sonuçları tutma toorun hello SELECT komutu.</span><span class="sxs-lookup"><span data-stu-id="dc41e-164">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello SELECT command, keeping hello results in a result set.</span></span> <span data-ttu-id="dc41e-165">Merhaba sonuç kümesi koleksiyonu hello kullanarak üzerinden yinelendiğinde `resultSet.each do` hello geçerli satır değerleri hello tutma döngü `row` değişkeni.</span><span class="sxs-lookup"><span data-stu-id="dc41e-165">hello result set collection is iterated over using hello `resultSet.each do` loop, keeping hello current row values in hello `row` variable.</span></span> <span data-ttu-id="dc41e-166">Merhaba kod hello kullanarak hatalarını denetler [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="dc41e-166">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="dc41e-167">Yöntem çağrıları sonra [çağrısının](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) sonlandırmadan önce tooclose hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="dc41e-167">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="dc41e-168">Hello yerine `host`, `database`, `user`, ve `password` dizeleri kendi değerlerinizle.</span><span class="sxs-lookup"><span data-stu-id="dc41e-168">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="dc41e-169">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="dc41e-169">Update data</span></span>
<span data-ttu-id="dc41e-170">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak veri güncelleştirme bir **güncelleştirme** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="dc41e-170">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="dc41e-171">Merhaba kodu kullanan bir [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) Oluşturucusu nesnesiyle [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure PostgreSQL için veritabanı.</span><span class="sxs-lookup"><span data-stu-id="dc41e-171">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="dc41e-172">Yöntem çağrıları sonra [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello güncelleştirme komutu.</span><span class="sxs-lookup"><span data-stu-id="dc41e-172">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello UPDATE command.</span></span> <span data-ttu-id="dc41e-173">Merhaba kod hello kullanarak hatalarını denetler [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="dc41e-173">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="dc41e-174">Yöntem çağrıları sonra [çağrısının](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) sonlandırmadan önce tooclose hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="dc41e-174">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="dc41e-175">Hello yerine `host`, `database`, `user`, ve `password` dizeleri kendi değerlerinizle.</span><span class="sxs-lookup"><span data-stu-id="dc41e-175">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

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


## <a name="delete-data"></a><span data-ttu-id="dc41e-176">Verileri silme</span><span class="sxs-lookup"><span data-stu-id="dc41e-176">Delete data</span></span>
<span data-ttu-id="dc41e-177">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **silmek** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="dc41e-177">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="dc41e-178">Merhaba kodu kullanan bir [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) Oluşturucusu nesnesiyle [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure PostgreSQL için veritabanı.</span><span class="sxs-lookup"><span data-stu-id="dc41e-178">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="dc41e-179">Yöntem çağrıları sonra [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello güncelleştirme komutu.</span><span class="sxs-lookup"><span data-stu-id="dc41e-179">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello UPDATE command.</span></span> <span data-ttu-id="dc41e-180">Merhaba kod hello kullanarak hatalarını denetler [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="dc41e-180">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="dc41e-181">Yöntem çağrıları sonra [çağrısının](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) sonlandırmadan önce tooclose hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="dc41e-181">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="dc41e-182">Hello yerine `host`, `database`, `user`, ve `password` dizeleri kendi değerlerinizle.</span><span class="sxs-lookup"><span data-stu-id="dc41e-182">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="dc41e-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dc41e-183">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="dc41e-184">Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme</span><span class="sxs-lookup"><span data-stu-id="dc41e-184">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
