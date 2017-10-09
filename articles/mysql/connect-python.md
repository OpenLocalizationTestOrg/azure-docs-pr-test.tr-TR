---
title: "Python'dan MySQL için tooAzure veritabanına bağlanma | Microsoft Docs"
description: "Bu Hızlı Başlangıç, kod örnekleri tooconnect ve sorgu verileri Azure veritabanından MySQL için kullanabileceğiniz birkaç Python sağlar."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: python
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: 9df5211adcab886a502fd138347aed8fb587cd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-python-tooconnect-and-query-data"></a><span data-ttu-id="b5965-103">Azure veritabanı için MySQL: kullanım Python tooconnect ve sorgu verileri</span><span class="sxs-lookup"><span data-stu-id="b5965-103">Azure Database for MySQL: Use Python tooconnect and query data</span></span>
<span data-ttu-id="b5965-104">Bu hızlı başlangıç gösteren nasıl toouse [Python](https://python.org) tooconnect tooan Azure veritabanı için MySQL.</span><span class="sxs-lookup"><span data-stu-id="b5965-104">This quickstart demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure Database for MySQL.</span></span> <span data-ttu-id="b5965-105">Mac OS, Ubuntu Linux ve Windows platformları hello veritabanında SQL deyimleri tooquery, ekleme, güncelleştirme ve silme verilerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="b5965-105">It uses SQL statements tooquery, insert, update, and delete data in hello database from Mac OS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="b5965-106">Bu makalede Hello adımlarda Python kullanarak geliştirme ile bilgi sahibiyseniz ve yeni tooworking Azure veritabanı MySQL için sahip olduğunuz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="b5965-106">hello steps in this article assume that you are familiar with developing using Python and are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5965-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b5965-107">Prerequisites</span></span>
<span data-ttu-id="b5965-108">Bu hızlı başlangıç Bu kılavuzlara birini başlangıç noktası olarak oluşturulan hello kaynakları kullanır:</span><span class="sxs-lookup"><span data-stu-id="b5965-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="b5965-109">Azure portalını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="b5965-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="b5965-110">Azure CLI kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="b5965-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-python-and-hello-mysql-connector"></a><span data-ttu-id="b5965-111">Python'ı yükleyin ve MySQL bağlayıcı hello</span><span class="sxs-lookup"><span data-stu-id="b5965-111">Install Python and hello MySQL connector</span></span>
<span data-ttu-id="b5965-112">Yükleme [Python](https://www.python.org/downloads/) ve hello [Python MySQL bağlayıcı](https://dev.mysql.com/downloads/connector/python/) kendi makinede.</span><span class="sxs-lookup"><span data-stu-id="b5965-112">Install [Python](https://www.python.org/downloads/) and hello [MySQL connector for Python](https://dev.mysql.com/downloads/connector/python/) on your own machine.</span></span> <span data-ttu-id="b5965-113">Platformunuz bağlı olarak hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="b5965-113">Depending on your platform, follow hello steps:</span></span>

### <a name="windows"></a><span data-ttu-id="b5965-114">Windows</span><span class="sxs-lookup"><span data-stu-id="b5965-114">Windows</span></span>
1. <span data-ttu-id="b5965-115">Python 2.7’yi [python.org](https://www.python.org/downloads/windows/) adresinden indirin ve yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b5965-115">Download and Install Python 2.7 from [python.org](https://www.python.org/downloads/windows/).</span></span> 
2. <span data-ttu-id="b5965-116">Merhaba Python yükleme hello komut istemi başlatarak denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b5965-116">Check hello Python installation by launching hello command prompt.</span></span> <span data-ttu-id="b5965-117">Merhaba komutu çalıştırmak `C:\python27\python.exe -V` hello büyük V anahtar toosee hello sürüm numarasını kullanarak.</span><span class="sxs-lookup"><span data-stu-id="b5965-117">Run hello command `C:\python27\python.exe -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="b5965-118">Merhaba Python bağlayıcı MySQL'den Yükle [mysql.com](https://dev.mysql.com/downloads/connector/python/) Python ilgili tooyour sürümü.</span><span class="sxs-lookup"><span data-stu-id="b5965-118">Install hello Python connector for MySQL from [mysql.com](https://dev.mysql.com/downloads/connector/python/) corresponding tooyour version of Python.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="b5965-119">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="b5965-119">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="b5965-120">Linux (Ubuntu), Python genellikle hello varsayılan yüklemesinin bir parçası yüklenir.</span><span class="sxs-lookup"><span data-stu-id="b5965-120">In Linux (Ubuntu), Python is typically installed as part of hello default installation.</span></span>
2. <span data-ttu-id="b5965-121">Merhaba Python yükleme hello bash kabuğunda başlatarak denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b5965-121">Check hello Python installation by launching hello bash shell.</span></span> <span data-ttu-id="b5965-122">Merhaba komutu çalıştırmak `python -V` hello büyük V anahtar toosee hello sürüm numarasını kullanarak.</span><span class="sxs-lookup"><span data-stu-id="b5965-122">Run hello command `python -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="b5965-123">Merhaba çalıştırarak Hello PIP yükleme denetimi `pip show pip -V` komut toosee hello sürüm numarası.</span><span class="sxs-lookup"><span data-stu-id="b5965-123">Check hello PIP installation by running hello `pip show pip -V` command toosee hello version number.</span></span> 
4. <span data-ttu-id="b5965-124">PIP, Python’un bazı sürümlerine eklenmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="b5965-124">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="b5965-125">PIP yüklü değilse hello [PIP] (https://pip.pypa.io/en/stable/installing/) yükleyebilir komutunu çalıştırarak paket `sudo apt-get install python-pip`.</span><span class="sxs-lookup"><span data-stu-id="b5965-125">If PIP is not installed, you may install hello [PIP] (https://pip.pypa.io/en/stable/installing/) package, by running command `sudo apt-get install python-pip`.</span></span>
5. <span data-ttu-id="b5965-126">Merhaba çalıştırarak güncelleştirme PIP toohello en son sürümü, `pip install -U pip` komutu.</span><span class="sxs-lookup"><span data-stu-id="b5965-126">Update PIP toohello latest version, by running hello `pip install -U pip` command.</span></span>
6. <span data-ttu-id="b5965-127">Merhaba MySQL bağlayıcı Python ve bağımlılıklarını hello PIP komutunu kullanarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="b5965-127">Install hello MySQL connector for Python, and its dependencies by using hello PIP command:</span></span>

   ```bash
   sudo pip install mysql-connector-python-rf
   ```
 
### <a name="macos"></a><span data-ttu-id="b5965-128">macOS</span><span class="sxs-lookup"><span data-stu-id="b5965-128">MacOS</span></span>
1. <span data-ttu-id="b5965-129">MAC'te Python genellikle hello varsayılan işletim sistemi yüklemesinin bir parçası yüklenir.</span><span class="sxs-lookup"><span data-stu-id="b5965-129">In Mac OS, Python is typically installed as part of hello default OS installation.</span></span>
2. <span data-ttu-id="b5965-130">Merhaba Python yükleme hello bash kabuğunda başlatarak denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b5965-130">Check hello Python installation by launching hello bash shell.</span></span> <span data-ttu-id="b5965-131">Merhaba komutu çalıştırmak `python -V` hello büyük V anahtar toosee hello sürüm numarasını kullanarak.</span><span class="sxs-lookup"><span data-stu-id="b5965-131">Run hello command `python -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="b5965-132">Merhaba çalıştırarak Hello PIP yükleme denetimi `pip show pip -V` komut toosee hello sürüm numarası.</span><span class="sxs-lookup"><span data-stu-id="b5965-132">Check hello PIP installation by running hello `pip show pip -V` command toosee hello version number.</span></span>
4. <span data-ttu-id="b5965-133">PIP, Python’un bazı sürümlerine eklenmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="b5965-133">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="b5965-134">PIP yüklü değilse hello yükleyebilir [PIP](https://pip.pypa.io/en/stable/installing/) paket.</span><span class="sxs-lookup"><span data-stu-id="b5965-134">If PIP is not installed, you may install hello [PIP](https://pip.pypa.io/en/stable/installing/) package.</span></span>
5. <span data-ttu-id="b5965-135">Merhaba çalıştırarak güncelleştirme PIP toohello en son sürümü, `pip install -U pip` komutu.</span><span class="sxs-lookup"><span data-stu-id="b5965-135">Update PIP toohello latest version, by running hello `pip install -U pip` command.</span></span>
6. <span data-ttu-id="b5965-136">Merhaba MySQL bağlayıcı Python ve bağımlılıklarını hello PIP komutunu kullanarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="b5965-136">Install hello MySQL connector for Python, and its dependencies by using hello PIP command:</span></span>

   ```bash
   pip install mysql-connector-python-rf
   ```

## <a name="get-connection-information"></a><span data-ttu-id="b5965-137">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="b5965-137">Get connection information</span></span>
<span data-ttu-id="b5965-138">Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure veritabanı için MySQL alın.</span><span class="sxs-lookup"><span data-stu-id="b5965-138">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="b5965-139">Tam sunucu adını ve oturum açma kimlik bilgileri hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="b5965-139">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="b5965-140">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b5965-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b5965-141">Merhaba sol taraftaki menüden Azure portalında, **tüm kaynakları** ve aramak için creased, gibi hello sunucu **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="b5965-141">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="b5965-142">Merhaba sunucu adına tıklatarak **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="b5965-142">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="b5965-143">Select hello sunucunun **özellikleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="b5965-143">Select hello server's **Properties** page.</span></span> <span data-ttu-id="b5965-144">Merhaba Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.</span><span class="sxs-lookup"><span data-stu-id="b5965-144">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="b5965-145">![MySQL için Azure Veritabanı - Sunucu Yöneticisi Oturum Açma](./media/connect-python/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="b5965-145">![Azure Database for MySQL - Server Admin Login](./media/connect-python/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="b5965-146">Sunucu oturum açma bilgilerinizi unutursanız, toohello gidin **genel bakış** tooview hello sunucu yönetici oturum açma adı sayfasında ve gerekirse sıfırlamak hello parola.</span><span class="sxs-lookup"><span data-stu-id="b5965-146">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>
   

## <a name="run-python-code"></a><span data-ttu-id="b5965-147">Python Kodunu Çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b5965-147">Run Python Code</span></span>
- <span data-ttu-id="b5965-148">Merhaba kod bir metin dosyasına yapıştırın ve proje klasörüne C:\pythonmysql\createtable.py veya /home/username/pythonmysql/createtable.py gibi dosya uzantısı .py ile Merhaba dosyasını kaydedin</span><span class="sxs-lookup"><span data-stu-id="b5965-148">Paste hello code into a text file, and save hello file into a project folder with file extension .py, such as C:\pythonmysql\createtable.py or /home/username/pythonmysql/createtable.py</span></span>
- <span data-ttu-id="b5965-149">toorun hello kod hello komut istemi başlatın veya kabuk bash.</span><span class="sxs-lookup"><span data-stu-id="b5965-149">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="b5965-150">Dizini, proje klasörünüzle değiştirin (`cd pythonmysql`).</span><span class="sxs-lookup"><span data-stu-id="b5965-150">Change directory into your project folder `cd pythonmysql`.</span></span> <span data-ttu-id="b5965-151">Merhaba dosya adından hello python komut yazarak `python createtable.py` toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="b5965-151">Then type hello python command followed by hello file name `python createtable.py` toorun hello application.</span></span> <span data-ttu-id="b5965-152">Hello Windows işletim sistemi, Python.exe'yi bulunmazsa, hello tam yolu toohello yürütülebilir sağlayın veya hello Python yolu hello yol ortam değişkenine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b5965-152">On hello Windows OS, if python.exe is not found, you may provide hello full path toohello executable, or add hello Python path into hello path environment variable.</span></span> `C:\python27\python.exe createtable.py`

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="b5965-153">Bağlanma, tablo oluşturma ve veri ekleme</span><span class="sxs-lookup"><span data-stu-id="b5965-153">Connect, create table, and insert data</span></span>
<span data-ttu-id="b5965-154">Kullanım hello aşağıdaki kod tooconnect toohello sunucu, bir tablo oluşturun ve verileri hello kullanarak yük bir **Ekle** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="b5965-154">Use hello following code tooconnect toohello server, create a table, and load hello data using an **INSERT** SQL statement.</span></span> 

<span data-ttu-id="b5965-155">Merhaba kodda hello mysql.connector kitaplığı içeri aktarılır.</span><span class="sxs-lookup"><span data-stu-id="b5965-155">In hello code, hello mysql.connector library is imported.</span></span> <span data-ttu-id="b5965-156">Merhaba [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) işlevidir kullanılan tooconnect tooAzure hello kullanarak MySQL veritabanı [bağlantı bağımsız değişkenleri](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) hello config koleksiyonundaki.</span><span class="sxs-lookup"><span data-stu-id="b5965-156">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="b5965-157">Merhaba kod hello bağlantıda bir imleç kullanır ve [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) yöntemi MySQL veritabanı hello SQL sorgusunu çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="b5965-157">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="b5965-158">Hello yerine `host`, `user`, `password`, ve `database` parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle.</span><span class="sxs-lookup"><span data-stu-id="b5965-158">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Drop previous table of same name if one exists
  cursor.execute("DROP TABLE IF EXISTS inventory;")
  print("Finished dropping table (if existed).")

  # Create table
  cursor.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
  print("Finished creating table.")

  # Insert some data into table
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("banana", 150))
  print("Inserted",cursor.rowcount,"row(s) of data.")
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("orange", 154))
  print("Inserted",cursor.rowcount,"row(s) of data.")
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("apple", 100))
  print("Inserted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="read-data"></a><span data-ttu-id="b5965-159">Verileri okuma</span><span class="sxs-lookup"><span data-stu-id="b5965-159">Read data</span></span>
<span data-ttu-id="b5965-160">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **seçin** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="b5965-160">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="b5965-161">Merhaba kodda hello mysql.connector kitaplığı içeri aktarılır.</span><span class="sxs-lookup"><span data-stu-id="b5965-161">In hello code, hello mysql.connector library is imported.</span></span> <span data-ttu-id="b5965-162">Merhaba [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) işlevidir kullanılan tooconnect tooAzure hello kullanarak MySQL veritabanı [bağlantı bağımsız değişkenleri](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) hello config koleksiyonundaki.</span><span class="sxs-lookup"><span data-stu-id="b5965-162">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="b5965-163">Merhaba kod hello bağlantıda bir imleç kullanır ve [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) yöntemi MySQL veritabanında hello SQL deyimini yürütür.</span><span class="sxs-lookup"><span data-stu-id="b5965-163">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL statement against MySQL database.</span></span> <span data-ttu-id="b5965-164">Merhaba veri satırına hello kullanarak okunur [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="b5965-164">hello data rows are read using hello [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) method.</span></span> <span data-ttu-id="b5965-165">Merhaba sonuç kümesi bir koleksiyon satırda tutulur ve yineleyici hello satır üzerinde kullanılan tooloop için.</span><span class="sxs-lookup"><span data-stu-id="b5965-165">hello result set is kept in a collection row and a for iterator is used tooloop over hello rows.</span></span>

<span data-ttu-id="b5965-166">Hello yerine `host`, `user`, `password`, ve `database` parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle.</span><span class="sxs-lookup"><span data-stu-id="b5965-166">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Read data
  cursor.execute("SELECT * FROM inventory;")
  rows = cursor.fetchall()
  print("Read",cursor.rowcount,"row(s) of data.")

  # Print all rows
  for row in rows:
    print("Data row = (%s, %s, %s)" %(str(row[0]), str(row[1]), str(row[2])))

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="update-data"></a><span data-ttu-id="b5965-167">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="b5965-167">Update data</span></span>
<span data-ttu-id="b5965-168">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak veri güncelleştirme bir **güncelleştirme** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="b5965-168">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="b5965-169">Merhaba kodda hello mysql.connector kitaplığı içeri aktarılır.</span><span class="sxs-lookup"><span data-stu-id="b5965-169">In hello code, hello mysql.connector library is imported.</span></span>  <span data-ttu-id="b5965-170">Merhaba [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) işlevidir kullanılan tooconnect tooAzure hello kullanarak MySQL veritabanı [bağlantı bağımsız değişkenleri](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) hello config koleksiyonundaki.</span><span class="sxs-lookup"><span data-stu-id="b5965-170">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="b5965-171">Merhaba kod hello bağlantıda bir imleç kullanır ve [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) yöntemi MySQL veritabanında hello SQL deyimini yürütür.</span><span class="sxs-lookup"><span data-stu-id="b5965-171">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL statement against MySQL database.</span></span> 

<span data-ttu-id="b5965-172">Hello yerine `host`, `user`, `password`, ve `database` parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle.</span><span class="sxs-lookup"><span data-stu-id="b5965-172">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Update a data row in hello table
  cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
  print("Updated",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="delete-data"></a><span data-ttu-id="b5965-173">Verileri silme</span><span class="sxs-lookup"><span data-stu-id="b5965-173">Delete data</span></span>
<span data-ttu-id="b5965-174">Kullanım hello aşağıdaki tooconnect kod ve verileri kullanarak kaldırma bir **silmek** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="b5965-174">Use hello following code tooconnect and remove data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="b5965-175">Merhaba kodda hello mysql.connector kitaplığı içeri aktarılır.</span><span class="sxs-lookup"><span data-stu-id="b5965-175">In hello code, hello mysql.connector library is imported.</span></span>  <span data-ttu-id="b5965-176">Merhaba [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) işlevidir kullanılan tooconnect tooAzure hello kullanarak MySQL veritabanı [bağlantı bağımsız değişkenleri](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) hello config koleksiyonundaki.</span><span class="sxs-lookup"><span data-stu-id="b5965-176">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="b5965-177">Merhaba kod hello bağlantıda bir imleç kullanır ve [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) yöntemi MySQL veritabanı hello SQL sorgusunu çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="b5965-177">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="b5965-178">Hello yerine `host`, `user`, `password`, ve `database` parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle.</span><span class="sxs-lookup"><span data-stu-id="b5965-178">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established.")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password.")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist.")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Delete a data row in hello table
  cursor.execute("DELETE FROM inventory WHERE name=%(param1)s;", {'param1':"orange"})
  print("Deleted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="next-steps"></a><span data-ttu-id="b5965-179">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b5965-179">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="b5965-180">Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme</span><span class="sxs-lookup"><span data-stu-id="b5965-180">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
