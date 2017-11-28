---
title: "Python’dan MySQL için Azure Veritabanı'na bağlanma | Microsoft Docs"
description: "Bu hızlı başlangıçta, MySQL için Azure Veritabanı'na bağlanmak ve buradan veri sorgulamak için kullanabileceğiniz birkaç Python kod örneği sağlanmıştır."
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
ms.openlocfilehash: 4c3a2e65b83fab6fe5b8b7778782a747bb5e9cf9
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="azure-database-for-mysql-use-python-to-connect-and-query-data"></a><span data-ttu-id="255c1-103">MySQL için Azure Veritabanı: Python'u kullanarak bağlanma ve veri sorgulama</span><span class="sxs-lookup"><span data-stu-id="255c1-103">Azure Database for MySQL: Use Python to connect and query data</span></span>
<span data-ttu-id="255c1-104">Bu hızlı başlangıçta [Python](https://python.org) kullanarak MySQL için Azure Veritabanı'na nasıl bağlanacağınız gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="255c1-104">This quickstart demonstrates how to use [Python](https://python.org) to connect to an Azure Database for MySQL.</span></span> <span data-ttu-id="255c1-105">Mac OS, Ubuntu Linux ve Windows platformlarındaki veritabanında yer alan verileri sorgulamak, eklemek, güncelleştirmek ve silmek için SQL deyimlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="255c1-105">It uses SQL statements to query, insert, update, and delete data in the database from Mac OS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="255c1-106">Bu makaledeki adımlarda, Python kullanarak geliştirmeyle ilgili bilgi sahibi olduğunuz ve MySQL için Azure Veritabanı ile çalışmaya yeni başladığınız varsayılır.</span><span class="sxs-lookup"><span data-stu-id="255c1-106">The steps in this article assume that you are familiar with developing using Python and are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="255c1-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="255c1-107">Prerequisites</span></span>
<span data-ttu-id="255c1-108">Bu hızlı başlangıçta, başlangıç noktası olarak şu kılavuzlardan birinde oluşturulan kaynaklar kullanılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="255c1-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="255c1-109">Azure portalını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="255c1-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="255c1-110">Azure CLI kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="255c1-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-python-and-the-mysql-connector"></a><span data-ttu-id="255c1-111">Python’u ve MySQL bağlayıcısını yükleme</span><span class="sxs-lookup"><span data-stu-id="255c1-111">Install Python and the MySQL connector</span></span>
<span data-ttu-id="255c1-112">[Python](https://www.python.org/downloads/)’u ve [Python için MySQL bağlayıcısı](https://dev.mysql.com/downloads/connector/python/)’nı kendi makinenize yükleyin.</span><span class="sxs-lookup"><span data-stu-id="255c1-112">Install [Python](https://www.python.org/downloads/) and the [MySQL connector for Python](https://dev.mysql.com/downloads/connector/python/) on your own machine.</span></span> <span data-ttu-id="255c1-113">Platformunuza bağlı olarak, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="255c1-113">Depending on your platform, follow the steps:</span></span>

### <a name="windows"></a><span data-ttu-id="255c1-114">Windows</span><span class="sxs-lookup"><span data-stu-id="255c1-114">Windows</span></span>
1. <span data-ttu-id="255c1-115">Python 2.7’yi [python.org](https://www.python.org/downloads/windows/) adresinden indirin ve yükleyin.</span><span class="sxs-lookup"><span data-stu-id="255c1-115">Download and Install Python 2.7 from [python.org](https://www.python.org/downloads/windows/).</span></span> 
2. <span data-ttu-id="255c1-116">Komut istemini başlatarak Python yüklemesini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="255c1-116">Check the Python installation by launching the command prompt.</span></span> <span data-ttu-id="255c1-117">Sürüm numarasını görmek için büyük harf V anahtarını kullanarak `C:\python27\python.exe -V` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="255c1-117">Run the command `C:\python27\python.exe -V` using the uppercase V switch to see the version number.</span></span>
3. <span data-ttu-id="255c1-118">Python sürümünüze karşılık gelen MySQL için Python bağlayıcısını [mysql.com](https://dev.mysql.com/downloads/connector/python/) adresinden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="255c1-118">Install the Python connector for MySQL from [mysql.com](https://dev.mysql.com/downloads/connector/python/) corresponding to your version of Python.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="255c1-119">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="255c1-119">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="255c1-120">Linux’ta (Ubuntu), Python normalde varsayılan yükleme kapsamında yüklenir.</span><span class="sxs-lookup"><span data-stu-id="255c1-120">In Linux (Ubuntu), Python is typically installed as part of the default installation.</span></span>
2. <span data-ttu-id="255c1-121">Bash kabuğunu başlatarak Python yüklemesini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="255c1-121">Check the Python installation by launching the bash shell.</span></span> <span data-ttu-id="255c1-122">Sürüm numarasını görmek için büyük harf V anahtarını kullanarak `python -V` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="255c1-122">Run the command `python -V` using the uppercase V switch to see the version number.</span></span>
3. <span data-ttu-id="255c1-123">Sürüm numarasını görmek için `pip show pip -V` komutunu çalıştırarak PIP yüklemesini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="255c1-123">Check the PIP installation by running the `pip show pip -V` command to see the version number.</span></span> 
4. <span data-ttu-id="255c1-124">PIP, Python’un bazı sürümlerine eklenmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="255c1-124">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="255c1-125">PIP yüklenmediyse, `sudo apt-get install python-pip` komutunu çalıştırarak [PIP] (https://pip.pypa.io/en/stable/installing/) paketini yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="255c1-125">If PIP is not installed, you may install the [PIP] (https://pip.pypa.io/en/stable/installing/) package, by running command `sudo apt-get install python-pip`.</span></span>
5. <span data-ttu-id="255c1-126">`pip install -U pip` komutunu çalıştırarak PIP’yi en son sürüme güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="255c1-126">Update PIP to the latest version, by running the `pip install -U pip` command.</span></span>
6. <span data-ttu-id="255c1-127">Şu PIP komutunu kullanarak Python için MySQL bağlayıcısını ve onun bağımlılıklarını yükleyin:</span><span class="sxs-lookup"><span data-stu-id="255c1-127">Install the MySQL connector for Python, and its dependencies by using the PIP command:</span></span>

   ```bash
   sudo pip install mysql-connector-python-rf
   ```
 
### <a name="macos"></a><span data-ttu-id="255c1-128">macOS</span><span class="sxs-lookup"><span data-stu-id="255c1-128">MacOS</span></span>
1. <span data-ttu-id="255c1-129">Mac OS’ta, Python normalde varsayılan işletim sistemi yüklemesi kapsamında yüklenir.</span><span class="sxs-lookup"><span data-stu-id="255c1-129">In Mac OS, Python is typically installed as part of the default OS installation.</span></span>
2. <span data-ttu-id="255c1-130">Bash kabuğunu başlatarak Python yüklemesini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="255c1-130">Check the Python installation by launching the bash shell.</span></span> <span data-ttu-id="255c1-131">Sürüm numarasını görmek için büyük harf V anahtarını kullanarak `python -V` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="255c1-131">Run the command `python -V` using the uppercase V switch to see the version number.</span></span>
3. <span data-ttu-id="255c1-132">Sürüm numarasını görmek için `pip show pip -V` komutunu çalıştırarak PIP yüklemesini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="255c1-132">Check the PIP installation by running the `pip show pip -V` command to see the version number.</span></span>
4. <span data-ttu-id="255c1-133">PIP, Python’un bazı sürümlerine eklenmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="255c1-133">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="255c1-134">PIP yüklü değilse, [PIP](https://pip.pypa.io/en/stable/installing/) paketini yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="255c1-134">If PIP is not installed, you may install the [PIP](https://pip.pypa.io/en/stable/installing/) package.</span></span>
5. <span data-ttu-id="255c1-135">`pip install -U pip` komutunu çalıştırarak PIP’yi en son sürüme güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="255c1-135">Update PIP to the latest version, by running the `pip install -U pip` command.</span></span>
6. <span data-ttu-id="255c1-136">Şu PIP komutunu kullanarak Python için MySQL bağlayıcısını ve onun bağımlılıklarını yükleyin:</span><span class="sxs-lookup"><span data-stu-id="255c1-136">Install the MySQL connector for Python, and its dependencies by using the PIP command:</span></span>

   ```bash
   pip install mysql-connector-python-rf
   ```

## <a name="get-connection-information"></a><span data-ttu-id="255c1-137">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="255c1-137">Get connection information</span></span>
<span data-ttu-id="255c1-138">MySQL için Azure Veritabanı'na bağlanmak üzere gereken bağlantı bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="255c1-138">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="255c1-139">Tam sunucu adına ve oturum açma kimlik bilgilerine ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="255c1-139">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="255c1-140">[Azure Portal](https://portal.azure.com/)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="255c1-140">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="255c1-141">Azure portalında sol taraftaki menüden **Tüm kaynaklar**'a tıklayın ve oluşturduğunuz sunucuyu (örneğin, **myserver4demo**) arayın.</span><span class="sxs-lookup"><span data-stu-id="255c1-141">From the left-hand menu in Azure portal, click **All resources** and search for the server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="255c1-142">**myserver4demo** sunucu adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="255c1-142">Click the server name **myserver4demo**.</span></span>
4. <span data-ttu-id="255c1-143">Sunucunun **Özellikler** sayfasını seçin.</span><span class="sxs-lookup"><span data-stu-id="255c1-143">Select the server's **Properties** page.</span></span> <span data-ttu-id="255c1-144">**Sunucu adını** ve **Sunucu yöneticisi oturum açma adını** not edin.</span><span class="sxs-lookup"><span data-stu-id="255c1-144">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="255c1-145">![MySQL için Azure Veritabanı - Sunucu Yöneticisi Oturum Açma](./media/connect-python/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="255c1-145">![Azure Database for MySQL - Server Admin Login](./media/connect-python/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="255c1-146">Sunucunuzun oturum açma bilgilerini unuttuysanız **Genel Bakış** sayfasına giderek Sunucu yöneticisi oturum açma adını görüntüleyin ve gerekirse parolayı sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="255c1-146">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>
   

## <a name="run-python-code"></a><span data-ttu-id="255c1-147">Python Kodunu Çalıştırma</span><span class="sxs-lookup"><span data-stu-id="255c1-147">Run Python Code</span></span>
- <span data-ttu-id="255c1-148">Kodu bir metin dosyasına yapıştırın ve dosyayı .py uzantısıyla bir proje klasörüne kaydedin; örneğin, C:\pythonmysql\createtable.py veya /home/username/pythonmysql/createtable.py</span><span class="sxs-lookup"><span data-stu-id="255c1-148">Paste the code into a text file, and save the file into a project folder with file extension .py, such as C:\pythonmysql\createtable.py or /home/username/pythonmysql/createtable.py</span></span>
- <span data-ttu-id="255c1-149">Kodu çalıştırmak için komut istemi veya bash kabuğu başlatın.</span><span class="sxs-lookup"><span data-stu-id="255c1-149">To run the code, launch the command prompt or bash shell.</span></span> <span data-ttu-id="255c1-150">Dizini, proje klasörünüzle değiştirin (`cd pythonmysql`).</span><span class="sxs-lookup"><span data-stu-id="255c1-150">Change directory into your project folder `cd pythonmysql`.</span></span> <span data-ttu-id="255c1-151">Sonra uygulamayı çalıştırmak için python komutunu ve ardından `python createtable.py` dosya adını yazın.</span><span class="sxs-lookup"><span data-stu-id="255c1-151">Then type the python command followed by the file name `python createtable.py` to run the application.</span></span> <span data-ttu-id="255c1-152">Windows işletim sisteminde, python.exe bulunamazsa yürütülebilir dosyanın tam yolunu sağlayabilir veya yol ortam değişkenine Python yolunu ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="255c1-152">On the Windows OS, if python.exe is not found, you may provide the full path to the executable, or add the Python path into the path environment variable.</span></span> `C:\python27\python.exe createtable.py`

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="255c1-153">Bağlanma, tablo oluşturma ve veri ekleme</span><span class="sxs-lookup"><span data-stu-id="255c1-153">Connect, create table, and insert data</span></span>
<span data-ttu-id="255c1-154">Sunucuya bağlanmak, tablo oluşturmak ve **INSERT** SQL deyimini kullanarak verileri yüklemek için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="255c1-154">Use the following code to connect to the server, create a table, and load the data using an **INSERT** SQL statement.</span></span> 

<span data-ttu-id="255c1-155">Kodda, mysql.connector kitaplığı içeri aktarılır.</span><span class="sxs-lookup"><span data-stu-id="255c1-155">In the code, the mysql.connector library is imported.</span></span> <span data-ttu-id="255c1-156">Yapılandırma koleksiyonundaki [bağlantı bağımsız değişkenleri](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) kullanılarak MySQL için Azure Veritabanı’na bağlanmak üzere, [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) işlevi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="255c1-156">The [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used to connect to Azure Database for MySQL using the [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in the config collection.</span></span> <span data-ttu-id="255c1-157">Kod bağlantıda bir imleç kullanır ve [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) yöntemi MySQL veritabanında SQL sorgusunu yürütür.</span><span class="sxs-lookup"><span data-stu-id="255c1-157">The code uses a cursor on the connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes the SQL query against MySQL database.</span></span> 

<span data-ttu-id="255c1-158">`host`, `user`, `password` ve `database` parametrelerini, sunucu ve veritabanını oluştururken belirttiğiniz değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="255c1-158">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from the portal
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
    print("Something is wrong with the user name or password")
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

## <a name="read-data"></a><span data-ttu-id="255c1-159">Verileri okuma</span><span class="sxs-lookup"><span data-stu-id="255c1-159">Read data</span></span>
<span data-ttu-id="255c1-160">Bağlanmak ve **SELECT** SQL deyimi kullanarak verileri okumak için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="255c1-160">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="255c1-161">Kodda, mysql.connector kitaplığı içeri aktarılır.</span><span class="sxs-lookup"><span data-stu-id="255c1-161">In the code, the mysql.connector library is imported.</span></span> <span data-ttu-id="255c1-162">Yapılandırma koleksiyonundaki [bağlantı bağımsız değişkenleri](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) kullanılarak MySQL için Azure Veritabanı’na bağlanmak üzere, [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) işlevi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="255c1-162">The [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used to connect to Azure Database for MySQL using the [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in the config collection.</span></span> <span data-ttu-id="255c1-163">Kod bağlantıda bir imleç kullanır ve [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) yöntemi MySQL veritabanında SQL deyimini yürütür.</span><span class="sxs-lookup"><span data-stu-id="255c1-163">The code uses a cursor on the connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes the SQL statement against MySQL database.</span></span> <span data-ttu-id="255c1-164">Veri satırları, [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) yöntemi kullanılarak okunur.</span><span class="sxs-lookup"><span data-stu-id="255c1-164">The data rows are read using the [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) method.</span></span> <span data-ttu-id="255c1-165">Sonuç kümesi koleksiyon satırında tutulur ve satırlarda döngü yapmak için bir yineleyici kullanılır.</span><span class="sxs-lookup"><span data-stu-id="255c1-165">The result set is kept in a collection row and a for iterator is used to loop over the rows.</span></span>

<span data-ttu-id="255c1-166">`host`, `user`, `password` ve `database` parametrelerini, sunucu ve veritabanını oluştururken belirttiğiniz değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="255c1-166">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from the portal
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
    print("Something is wrong with the user name or password")
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

## <a name="update-data"></a><span data-ttu-id="255c1-167">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="255c1-167">Update data</span></span>
<span data-ttu-id="255c1-168">Bağlanmak ve **UPDATE** SQL deyimi kullanarak verileri güncelleştirmek için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="255c1-168">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="255c1-169">Kodda, mysql.connector kitaplığı içeri aktarılır.</span><span class="sxs-lookup"><span data-stu-id="255c1-169">In the code, the mysql.connector library is imported.</span></span>  <span data-ttu-id="255c1-170">Yapılandırma koleksiyonundaki [bağlantı bağımsız değişkenleri](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) kullanılarak MySQL için Azure Veritabanı’na bağlanmak üzere, [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) işlevi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="255c1-170">The [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used to connect to Azure Database for MySQL using the [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in the config collection.</span></span> <span data-ttu-id="255c1-171">Kod bağlantıda bir imleç kullanır ve [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) yöntemi MySQL veritabanında SQL deyimini yürütür.</span><span class="sxs-lookup"><span data-stu-id="255c1-171">The code uses a cursor on the connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes the SQL statement against MySQL database.</span></span> 

<span data-ttu-id="255c1-172">`host`, `user`, `password` ve `database` parametrelerini, sunucu ve veritabanını oluştururken belirttiğiniz değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="255c1-172">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from the portal
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
    print("Something is wrong with the user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Update a data row in the table
  cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
  print("Updated",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="delete-data"></a><span data-ttu-id="255c1-173">Verileri silme</span><span class="sxs-lookup"><span data-stu-id="255c1-173">Delete data</span></span>
<span data-ttu-id="255c1-174">Bağlanmak ve **DELETE** SQL deyimini kullanarak verileri kaldırmak için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="255c1-174">Use the following code to connect and remove data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="255c1-175">Kodda, mysql.connector kitaplığı içeri aktarılır.</span><span class="sxs-lookup"><span data-stu-id="255c1-175">In the code, the mysql.connector library is imported.</span></span>  <span data-ttu-id="255c1-176">Yapılandırma koleksiyonundaki [bağlantı bağımsız değişkenleri](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) kullanılarak MySQL için Azure Veritabanı’na bağlanmak üzere, [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) işlevi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="255c1-176">The [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used to connect to Azure Database for MySQL using the [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in the config collection.</span></span> <span data-ttu-id="255c1-177">Kod bağlantıda bir imleç kullanır ve [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) yöntemi MySQL veritabanında SQL sorgusunu yürütür.</span><span class="sxs-lookup"><span data-stu-id="255c1-177">The code uses a cursor on the connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes the SQL query against MySQL database.</span></span> 

<span data-ttu-id="255c1-178">`host`, `user`, `password` ve `database` parametrelerini, sunucu ve veritabanını oluştururken belirttiğiniz değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="255c1-178">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from the portal
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
    print("Something is wrong with the user name or password.")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist.")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Delete a data row in the table
  cursor.execute("DELETE FROM inventory WHERE name=%(param1)s;", {'param1':"orange"})
  print("Deleted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="next-steps"></a><span data-ttu-id="255c1-179">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="255c1-179">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="255c1-180">Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme</span><span class="sxs-lookup"><span data-stu-id="255c1-180">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
