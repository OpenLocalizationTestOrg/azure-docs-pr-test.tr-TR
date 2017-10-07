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
# <a name="azure-database-for-mysql-use-ruby-tooconnect-and-query-data"></a><span data-ttu-id="9bbba-103">Azure veritabanı için MySQL: kullanım Ruby tooconnect ve sorgu verileri</span><span class="sxs-lookup"><span data-stu-id="9bbba-103">Azure Database for MySQL: Use Ruby tooconnect and query data</span></span>
<span data-ttu-id="9bbba-104">Bu hızlı başlangıç gösteren Azure tooconnect tooan veritabanı nasıl MySQL kullanmak için bir [Ruby](https://www.ruby-lang.org) uygulama ve hello [mysql2](https://rubygems.org/gems/mysql2) Windows, Ubuntu Linux ve Mac platformları gelen gem.</span><span class="sxs-lookup"><span data-stu-id="9bbba-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a [Ruby](https://www.ruby-lang.org) application and hello [mysql2](https://rubygems.org/gems/mysql2) gem from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="9bbba-105">Nasıl toouse SQL deyimleri tooquery, Ekle, Güncelleştir ve hello veritabanında bulunan verileri silme gösterir.</span><span class="sxs-lookup"><span data-stu-id="9bbba-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="9bbba-106">Bu makale, Azure veritabanı için MySQL ile yeni tooworking olan ancak bu, Ruby, kullanarak geliştirme ile bildiğinizi varsayar.</span><span class="sxs-lookup"><span data-stu-id="9bbba-106">This article assumes you are familiar with development using Ruby, but that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9bbba-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9bbba-107">Prerequisites</span></span>
<span data-ttu-id="9bbba-108">Bu hızlı başlangıç Bu kılavuzlara birini başlangıç noktası olarak oluşturulan hello kaynakları kullanır:</span><span class="sxs-lookup"><span data-stu-id="9bbba-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="9bbba-109">Azure portalını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="9bbba-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="9bbba-110">Azure CLI kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="9bbba-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="9bbba-111">Ruby’yi yükleme</span><span class="sxs-lookup"><span data-stu-id="9bbba-111">Install Ruby</span></span>
<span data-ttu-id="9bbba-112">Ruby, Gem ve hello MySQL2 kitaplık kendi makineye yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9bbba-112">Install Ruby, Gem, and hello MySQL2 library on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="9bbba-113">Windows</span><span class="sxs-lookup"><span data-stu-id="9bbba-113">Windows</span></span>
1. <span data-ttu-id="9bbba-114">İndirme ve yükleme hello 2.3 sürümü [Ruby](http://rubyinstaller.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="9bbba-114">Download and Install hello 2.3 version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
2. <span data-ttu-id="9bbba-115">Yeni bir komut istemi (cmd) hello Başlat menüsünden başlatın.</span><span class="sxs-lookup"><span data-stu-id="9bbba-115">Launch a new command prompt (cmd) from hello Start menu.</span></span>
3. <span data-ttu-id="9bbba-116">Merhaba sürüm 2.3 Söyleniş dizini içine dizini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9bbba-116">Change directory into hello Ruby directory for version 2.3.</span></span> `cd c:\Ruby23-x64\bin`
4. <span data-ttu-id="9bbba-117">Test hello hello komutunu çalıştırarak Söyleniş yükleme `ruby -v` toosee hello sürümü yüklü.</span><span class="sxs-lookup"><span data-stu-id="9bbba-117">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
5. <span data-ttu-id="9bbba-118">Merhaba komutu çalıştırarak test Hello Gem yüklemesi `gem -v` toosee hello sürümü yüklü.</span><span class="sxs-lookup"><span data-stu-id="9bbba-118">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
6. <span data-ttu-id="9bbba-119">Merhaba komutu çalıştırarak Gem kullanarak Ruby için Hello Mysql2 modülü oluşturmak `gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="9bbba-119">Build hello Mysql2 module for Ruby using Gem by running hello command `gem install mysql2`.</span></span>

### <a name="macos"></a><span data-ttu-id="9bbba-120">macOS</span><span class="sxs-lookup"><span data-stu-id="9bbba-120">MacOS</span></span>
1. <span data-ttu-id="9bbba-121">Merhaba komutu çalıştırarak Homebrew kullanarak Ruby yüklemek `brew install ruby`.</span><span class="sxs-lookup"><span data-stu-id="9bbba-121">Install Ruby using Homebrew by running hello command `brew install ruby`.</span></span> <span data-ttu-id="9bbba-122">Merhaba Ruby daha fazla yükleme seçenekleri için bkz [yükleme belgelerini](https://www.ruby-lang.org/en/documentation/installation/#homebrew).</span><span class="sxs-lookup"><span data-stu-id="9bbba-122">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew).</span></span>
2. <span data-ttu-id="9bbba-123">Test hello hello komutunu çalıştırarak Söyleniş yükleme `ruby -v` toosee hello sürümü yüklü.</span><span class="sxs-lookup"><span data-stu-id="9bbba-123">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
3. <span data-ttu-id="9bbba-124">Merhaba komutu çalıştırarak test Hello Gem yüklemesi `gem -v` toosee hello sürümü yüklü.</span><span class="sxs-lookup"><span data-stu-id="9bbba-124">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
4. <span data-ttu-id="9bbba-125">Merhaba komutu çalıştırarak Gem kullanarak Ruby için Hello Mysql2 modülü oluşturmak `gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="9bbba-125">Build hello Mysql2 module for Ruby using Gem by running hello command `gem install mysql2`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="9bbba-126">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="9bbba-126">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="9bbba-127">Ruby hello komutu çalıştırarak yükleyin `sudo apt-get install ruby-full`.</span><span class="sxs-lookup"><span data-stu-id="9bbba-127">Install Ruby by running hello command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="9bbba-128">Merhaba Ruby daha fazla yükleme seçenekleri için bkz [yükleme belgelerini](https://www.ruby-lang.org/en/documentation/installation/).</span><span class="sxs-lookup"><span data-stu-id="9bbba-128">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
2. <span data-ttu-id="9bbba-129">Test hello hello komutunu çalıştırarak Söyleniş yükleme `ruby -v` toosee hello sürümü yüklü.</span><span class="sxs-lookup"><span data-stu-id="9bbba-129">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
3. <span data-ttu-id="9bbba-130">Merhaba komutu çalıştırarak için Gem Hello en son güncelleştirmeleri yükleyin `sudo gem update --system`.</span><span class="sxs-lookup"><span data-stu-id="9bbba-130">Install hello latest updates for Gem by running hello command `sudo gem update --system`.</span></span>
4. <span data-ttu-id="9bbba-131">Merhaba komutu çalıştırarak test Hello Gem yüklemesi `gem -v` toosee hello sürümü yüklü.</span><span class="sxs-lookup"><span data-stu-id="9bbba-131">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
5. <span data-ttu-id="9bbba-132">Merhaba komutu çalıştırarak Hello gcc, marka ve diğer yapı araçlarını yükleyin `sudo apt-get install build-essential`.</span><span class="sxs-lookup"><span data-stu-id="9bbba-132">Install hello gcc, make, and other build tools by running hello command `sudo apt-get install build-essential`.</span></span>
6. <span data-ttu-id="9bbba-133">Merhaba komutu çalıştırarak Hello MySQL istemci geliştirici kitaplıkları yükleme `sudo apt-get install libmysqlclient-dev`.</span><span class="sxs-lookup"><span data-stu-id="9bbba-133">Install hello MySQL client developer libraries by running hello command `sudo apt-get install libmysqlclient-dev`.</span></span>
7. <span data-ttu-id="9bbba-134">Merhaba komutu çalıştırarak Gem kullanarak Ruby için Hello mysql2 modülü oluşturmak `sudo gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="9bbba-134">Build hello mysql2 module for Ruby using Gem by running hello command `sudo gem install mysql2`.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="9bbba-135">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="9bbba-135">Get connection information</span></span>
<span data-ttu-id="9bbba-136">Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure veritabanı için MySQL alın.</span><span class="sxs-lookup"><span data-stu-id="9bbba-136">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="9bbba-137">Tam sunucu adını ve oturum açma kimlik bilgileri hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="9bbba-137">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="9bbba-138">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9bbba-138">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9bbba-139">Merhaba sol taraftaki menüden Azure portalında, **tüm kaynakları** ve aramak için creased, gibi hello sunucu **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="9bbba-139">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="9bbba-140">Merhaba sunucu adına tıklatarak **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="9bbba-140">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="9bbba-141">Select hello sunucunun **özellikleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="9bbba-141">Select hello server's **Properties** page.</span></span> <span data-ttu-id="9bbba-142">Merhaba Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.</span><span class="sxs-lookup"><span data-stu-id="9bbba-142">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="9bbba-143">![MySQL için Azure Veritabanı - Sunucu Yöneticisi Oturum Açma](./media/connect-ruby/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="9bbba-143">![Azure Database for MySQL - Server Admin Login](./media/connect-ruby/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="9bbba-144">Sunucu oturum açma bilgilerinizi unutursanız, toohello gidin **genel bakış** tooview hello sunucu yönetici oturum açma adı sayfasında ve gerekirse sıfırlamak hello parola.</span><span class="sxs-lookup"><span data-stu-id="9bbba-144">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="9bbba-145">Ruby kodunu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9bbba-145">Run Ruby code</span></span> 
1. <span data-ttu-id="9bbba-146">Hello hello bölümlere Söyleniş koddan metin dosyasına yapıştırın ve gibi hello dosyaları dosya uzantısı .rb ile bir proje klasöre kaydedin `C:\rubymysql\createtable.rb` veya `/home/username/rubymysql/createtable.rb`.</span><span class="sxs-lookup"><span data-stu-id="9bbba-146">Paste hello Ruby code from hello sections below into text files, and save hello files into a project folder with file extension .rb, such as `C:\rubymysql\createtable.rb` or `/home/username/rubymysql/createtable.rb`.</span></span>
2. <span data-ttu-id="9bbba-147">toorun hello kod hello komut istemi başlatın veya kabuk bash.</span><span class="sxs-lookup"><span data-stu-id="9bbba-147">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="9bbba-148">Dizini değiştirerek, proje klasörünüze geçin (`cd rubymysql`)</span><span class="sxs-lookup"><span data-stu-id="9bbba-148">Change directory into your project folder `cd rubymysql`</span></span>
3. <span data-ttu-id="9bbba-149">Ardından hello dosya adı, gibi hello Söyleniş komutu yazın `ruby createtable.rb` toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="9bbba-149">Then type hello ruby command followed by hello file name, such as `ruby createtable.rb` toorun hello application.</span></span>
4. <span data-ttu-id="9bbba-150">Merhaba ruby uygulaması path ortam değişkeni içinde değilse hello Windows işletim sistemi, toouse hello tam yolu toolaunch hello düğüm uygulama gibi ihtiyacınız`"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span><span class="sxs-lookup"><span data-stu-id="9bbba-150">On hello Windows OS, if hello ruby application is not in your path environment variable, you may need toouse hello full path toolaunch hello node application, such as `"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="9bbba-151">Bağlanma ve tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="9bbba-151">Connect and create a table</span></span>
<span data-ttu-id="9bbba-152">Kullanım hello aşağıdakileri tooconnect kod ve kullanarak bir tablo oluşturmak **CREATE TABLE** SQL deyimi, arkasından **INSERT INTO** SQL deyimleri tooadd satırları hello tabloya.</span><span class="sxs-lookup"><span data-stu-id="9bbba-152">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="9bbba-153">Merhaba kodu kullanan bir [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new() yöntemi tooconnect tooAzure veritabanı için MySQL sınıfı.</span><span class="sxs-lookup"><span data-stu-id="9bbba-153">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="9bbba-154">Yöntem çağrıları sonra [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) birkaç kez toorun hello bırakma, CREATE TABLE ve INSERT INTO komutları.</span><span class="sxs-lookup"><span data-stu-id="9bbba-154">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) several times toorun hello DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="9bbba-155">Yöntem çağrıları sonra [çağrısının](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) sonlandırmadan önce tooclose hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="9bbba-155">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="9bbba-156">Hello yerine `host`, `database`, `username`, ve `password` dizeleri kendi değerlerinizle.</span><span class="sxs-lookup"><span data-stu-id="9bbba-156">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 
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

## <a name="read-data"></a><span data-ttu-id="9bbba-157">Verileri okuma</span><span class="sxs-lookup"><span data-stu-id="9bbba-157">Read data</span></span>
<span data-ttu-id="9bbba-158">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **seçin** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="9bbba-158">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="9bbba-159">Merhaba kodu kullanan bir [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new() yöntemi tooconnect tooAzure veritabanı için MySQL sınıfı.</span><span class="sxs-lookup"><span data-stu-id="9bbba-159">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="9bbba-160">Yöntem çağrıları sonra [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello SELECT komutları.</span><span class="sxs-lookup"><span data-stu-id="9bbba-160">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello SELECT commands.</span></span> <span data-ttu-id="9bbba-161">Yöntem çağrıları sonra [çağrısının](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) sonlandırmadan önce tooclose hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="9bbba-161">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="9bbba-162">Hello yerine `host`, `database`, `username`, ve `password` dizeleri kendi değerlerinizle.</span><span class="sxs-lookup"><span data-stu-id="9bbba-162">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="9bbba-163">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="9bbba-163">Update data</span></span>
<span data-ttu-id="9bbba-164">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak veri güncelleştirme bir **güncelleştirme** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="9bbba-164">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="9bbba-165">Merhaba kodu kullanan bir [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new() yöntemi tooconnect tooAzure veritabanı için MySQL sınıfı.</span><span class="sxs-lookup"><span data-stu-id="9bbba-165">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="9bbba-166">Yöntem çağrıları sonra [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello güncelleştirme komutları.</span><span class="sxs-lookup"><span data-stu-id="9bbba-166">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello UPDATE commands.</span></span> <span data-ttu-id="9bbba-167">Yöntem çağrıları sonra [çağrısının](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) sonlandırmadan önce tooclose hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="9bbba-167">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="9bbba-168">Hello yerine `host`, `database`, `username`, ve `password` dizeleri kendi değerlerinizle.</span><span class="sxs-lookup"><span data-stu-id="9bbba-168">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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


## <a name="delete-data"></a><span data-ttu-id="9bbba-169">Verileri silme</span><span class="sxs-lookup"><span data-stu-id="9bbba-169">Delete data</span></span>
<span data-ttu-id="9bbba-170">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **silmek** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="9bbba-170">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="9bbba-171">Merhaba kodu kullanan bir [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) .new() yöntemi tooconnect tooAzure veritabanı için MySQL sınıfı.</span><span class="sxs-lookup"><span data-stu-id="9bbba-171">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="9bbba-172">Yöntem çağrıları sonra [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello Sil komutları.</span><span class="sxs-lookup"><span data-stu-id="9bbba-172">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello DELETE commands.</span></span> <span data-ttu-id="9bbba-173">Yöntem çağrıları sonra [çağrısının](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) sonlandırmadan önce tooclose hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="9bbba-173">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="9bbba-174">Hello yerine `host`, `database`, `username`, ve `password` dizeleri kendi değerlerinizle.</span><span class="sxs-lookup"><span data-stu-id="9bbba-174">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="9bbba-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9bbba-175">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="9bbba-176">Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme</span><span class="sxs-lookup"><span data-stu-id="9bbba-176">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
