---
title: "Python'dan PostgreSQL için tooAzure veritabanına bağlanma | Microsoft Docs"
description: "Bu hızlı başlangıç tooconnect kullanın ve Azure veritabanındaki verileri sorgulamak için PostgreSQL bir Python kodu örneği sağlar."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: python
ms.topic: quickstart
ms.date: 08/15/2017
ms.openlocfilehash: 7d6d9f5424fb39ad8837999d4788b4363c818887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-python-tooconnect-and-query-data"></a><span data-ttu-id="caa64-103">Azure veritabanı PostgreSQL için: kullanım Python tooconnect ve sorgu verileri</span><span class="sxs-lookup"><span data-stu-id="caa64-103">Azure Database for PostgreSQL: Use Python tooconnect and query data</span></span>
<span data-ttu-id="caa64-104">Bu hızlı başlangıç gösteren nasıl toouse [Python](https://python.org) tooconnect tooan Azure veritabanı PostgreSQL için.</span><span class="sxs-lookup"><span data-stu-id="caa64-104">This quickstart demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure Database for PostgreSQL.</span></span> <span data-ttu-id="caa64-105">Ayrıca nasıl toouse SQL deyimleri tooquery, ekleme, güncelleştirme ve hello veritabanındaki verileri silmek macOS, Ubuntu Linux ve Windows platformları gösterir.</span><span class="sxs-lookup"><span data-stu-id="caa64-105">It also demonstrates how toouse SQL statements tooquery, insert, update, and delete data in hello database from macOS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="caa64-106">Bu makalede Hello adımlarda Python kullanarak geliştirme ile bilgi sahibiyseniz ve yeni tooworking Azure veritabanı PostgreSQL için sahip olduğunuz varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="caa64-106">hello steps in this article assume that you are familiar with developing using Python and are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="caa64-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="caa64-107">Prerequisites</span></span>
<span data-ttu-id="caa64-108">Bu hızlı başlangıç Bu kılavuzlara birini başlangıç noktası olarak oluşturulan hello kaynakları kullanır:</span><span class="sxs-lookup"><span data-stu-id="caa64-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="caa64-109">DB Oluşturma - Portal</span><span class="sxs-lookup"><span data-stu-id="caa64-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="caa64-110">DB oluşturma - CLI</span><span class="sxs-lookup"><span data-stu-id="caa64-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="caa64-111">Şunları da yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="caa64-111">You also need:</span></span>
- <span data-ttu-id="caa64-112">[Python](https://www.python.org/downloads/)'ı yükleme</span><span class="sxs-lookup"><span data-stu-id="caa64-112">[python](https://www.python.org/downloads/) installed</span></span>
- <span data-ttu-id="caa64-113">[pip](https://pip.pypa.io/en/stable/installing/) paketi yüklü ([python.org](https://python.org) adresinden indirilen Python 2 >=2.7.9 veya Python 3 >=3.4 ikili dosyalarıyla çalışıyorsanız pip zaten yüklüdür).</span><span class="sxs-lookup"><span data-stu-id="caa64-113">[pip](https://pip.pypa.io/en/stable/installing/) package installed (pip is already installed if you're working with Python 2 >=2.7.9 or Python 3 >=3.4 binaries downloaded from [python.org](https://python.org).</span></span>

## <a name="install-hello-python-connection-libraries-for-postgresql"></a><span data-ttu-id="caa64-114">Merhaba Python bağlantı kitaplıkları için PostgreSQL yükleme</span><span class="sxs-lookup"><span data-stu-id="caa64-114">Install hello Python connection libraries for PostgreSQL</span></span>
<span data-ttu-id="caa64-115">Merhaba yüklemek [psycopg2](http://initd.org/psycopg/docs/install.html) paketi olarak tooconnect ve sorgu hello veritabanını etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="caa64-115">Install hello [psycopg2](http://initd.org/psycopg/docs/install.html) package, which enables you tooconnect and query hello database.</span></span> <span data-ttu-id="caa64-116">psycopg2 olan [Pypı kullanılabilir](https://pypi.python.org/pypi/psycopg2/) hello biçiminde [Tekerlek](http://pythonwheels.com/) hello en yaygın platformları (Linux, OSX, Windows) paketleri.</span><span class="sxs-lookup"><span data-stu-id="caa64-116">psycopg2 is [available on PyPI](https://pypi.python.org/pypi/psycopg2/) in hello form of [wheel](http://pythonwheels.com/) packages for hello most common platforms (Linux, OSX, Windows).</span></span> <span data-ttu-id="caa64-117">Kullanım PIP tooget hello ikili tüm hello bağımlılıklar dahil olmak üzere hello modülünün sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="caa64-117">Use pip install tooget hello binary version of hello module including all hello dependencies.</span></span>

1. <span data-ttu-id="caa64-118">Kendi bilgisayarınızda bir komut satırı arabirimi başlatın:</span><span class="sxs-lookup"><span data-stu-id="caa64-118">On your own computer, launch a command-line interface:</span></span>
    - <span data-ttu-id="caa64-119">Linux üzerinde hello Bash kabuğunda başlatın.</span><span class="sxs-lookup"><span data-stu-id="caa64-119">On Linux, launch hello Bash shell.</span></span>
    - <span data-ttu-id="caa64-120">MacOS üzerinde hello Terminal başlatın.</span><span class="sxs-lookup"><span data-stu-id="caa64-120">On macOS, launch hello Terminal.</span></span>
    - <span data-ttu-id="caa64-121">Windows hello Başlat menüsü gelen hello komut istemi başlatın.</span><span class="sxs-lookup"><span data-stu-id="caa64-121">On Windows, launch hello Command Prompt from hello Start Menu.</span></span>
2. <span data-ttu-id="caa64-122">Bir komutu çalıştırarak PIP hello en son sürümünü kullandığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="caa64-122">Ensure that you are using hello most current version of pip by running a command such as:</span></span>
    ```cmd
    pip install -U pip
    ```

3. <span data-ttu-id="caa64-123">Komut tooinstall hello psycopg2 paketi aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="caa64-123">Run hello following command tooinstall hello psycopg2 package:</span></span>
    ```cmd
    pip install psycopg2
    ```

## <a name="get-connection-information"></a><span data-ttu-id="caa64-124">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="caa64-124">Get connection information</span></span>
<span data-ttu-id="caa64-125">Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure veritabanı için PostgreSQL alın.</span><span class="sxs-lookup"><span data-stu-id="caa64-125">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="caa64-126">Tam sunucu adını ve oturum açma kimlik bilgileri hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="caa64-126">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="caa64-127">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="caa64-127">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="caa64-128">Merhaba sol taraftaki menüden Azure portalında, **tüm kaynakları** arayın ve **mypgserver 20170401** (yeni oluşturduğunuz hello sunucusu).</span><span class="sxs-lookup"><span data-stu-id="caa64-128">From hello left-hand menu in Azure portal, click **All resources** and search for **mypgserver-20170401** (hello server you just created).</span></span>
3. <span data-ttu-id="caa64-129">Merhaba sunucu adına tıklatarak **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="caa64-129">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="caa64-130">Select hello sunucunun **genel bakış** sayfasında ve ardından hello Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.</span><span class="sxs-lookup"><span data-stu-id="caa64-130">Select hello server's **Overview** page, and then make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="caa64-131">![PostgreSQL için Azure Veritabanı - Sunucu Yöneticisi Oturum Açma Bilgileri](./media/connect-python/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="caa64-131">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-python/1-connection-string.png)</span></span>
5. <span data-ttu-id="caa64-132">Sunucu oturum açma bilgilerinizi unutursanız, toohello gidin **genel bakış** tooview hello sunucu yönetici oturum açma adı sayfasında ve gerekirse sıfırlamak hello parola.</span><span class="sxs-lookup"><span data-stu-id="caa64-132">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="how-toorun-python-code"></a><span data-ttu-id="caa64-133">Nasıl toorun Python kodu</span><span class="sxs-lookup"><span data-stu-id="caa64-133">How toorun Python code</span></span>
<span data-ttu-id="caa64-134">Bu konu, her biri belirli bir işlevi gerçekleştiren toplam dört kod örneği içerir.</span><span class="sxs-lookup"><span data-stu-id="caa64-134">This topic contains a total of four code samples, each of which performs a specific function.</span></span> <span data-ttu-id="caa64-135">Merhaba aşağıdaki yönergeleri nasıl toocreate bir metin dosyasına bir kod bloğu Ekle ve böylece daha sonra çalıştırabileceğiniz hello dosyasını kaydedin gösterir.</span><span class="sxs-lookup"><span data-stu-id="caa64-135">hello following instructions indicate how toocreate a text file, insert a code block, and then save hello file so that you can run it later.</span></span> <span data-ttu-id="caa64-136">Emin toocreate dört ayrı dosyalar, her kod bloğu için bir tane olabilir.</span><span class="sxs-lookup"><span data-stu-id="caa64-136">Be sure toocreate four separate files, one for each code block.</span></span>

- <span data-ttu-id="caa64-137">Sık kullandığınız metin düzenleyicisini kullanarak yeni bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="caa64-137">Using your favorite text editor, create a new file.</span></span>
- <span data-ttu-id="caa64-138">Kopyalayın ve bir hello kod örnekleri bölümleri hello metin dosyasına aşağıdaki hello yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="caa64-138">Copy and paste one of hello code samples in hello following sections into hello text file.</span></span> <span data-ttu-id="caa64-139">Hello yerine **konak**, **dbname**, **kullanıcı**, ve **parola** hello değerleri hello oluşturduğunuzda belirtilen parametrelerle Sunucu ve veritabanı.</span><span class="sxs-lookup"><span data-stu-id="caa64-139">Replace hello **host**, **dbname**, **user**, and **password** parameters with hello values that you specified when you created hello server and database.</span></span>
- <span data-ttu-id="caa64-140">Merhaba dosyayı proje klasörünüze (örneğin postgres.py) hello .py uzantısıyla kaydedin.</span><span class="sxs-lookup"><span data-stu-id="caa64-140">Save hello file with hello .py extension (for example postgres.py) into your project folder.</span></span> <span data-ttu-id="caa64-141">Merhaba Windows işletim sistemi çalıştırıyorsanız, emin tooselect UTF-8 hello Dosya kaydedilirken kodlaması olabilir.</span><span class="sxs-lookup"><span data-stu-id="caa64-141">If you are running hello Windows OS, be sure tooselect UTF-8 encoding when saving hello file.</span></span> 
- <span data-ttu-id="caa64-142">Merhaba komut istemi veya Bash Kabuk başlatın ve hello dizin tooyour proje klasörü, örneğin değiştirmek `cd postgres`.</span><span class="sxs-lookup"><span data-stu-id="caa64-142">Launch hello Command Prompt or Bash shell and then change hello directory tooyour project folder, for example `cd postgres`.</span></span>
-  <span data-ttu-id="caa64-143">toorun hello kodu, türü hello ardından hello dosya adını, örneğin Python komut `Python postgres.py`.</span><span class="sxs-lookup"><span data-stu-id="caa64-143">toorun hello code, type hello Python command followed by hello file name, for example `Python postgres.py`.</span></span>

> [!NOTE]
> <span data-ttu-id="caa64-144">Python sürüm 3 başlayarak, hello hatayı görebilirsiniz `SyntaxError: Missing parentheses in call too'print'` kod blokları aşağıdaki hello çalışırken.</span><span class="sxs-lookup"><span data-stu-id="caa64-144">Starting in Python version 3, you may see hello error `SyntaxError: Missing parentheses in call too'print'` when running hello following code blocks.</span></span> <span data-ttu-id="caa64-145">Bu durumda, her çağrı toohello komutu yerine `print "string"` parantez, gibi kullanılarak bir işlev çağrısı ile `print("string")`.</span><span class="sxs-lookup"><span data-stu-id="caa64-145">If that happens, replace each call toohello command `print "string"` with a function call using parenthesis, such as `print("string")`.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="caa64-146">Bağlanma, tablo oluşturma ve veri ekleme</span><span class="sxs-lookup"><span data-stu-id="caa64-146">Connect, create table, and insert data</span></span>
<span data-ttu-id="caa64-147">Kullanım hello aşağıdakileri tooconnect kod ve verileri hello kullanarak yük [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) ile işlev **Ekle** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="caa64-147">Use hello following code tooconnect and load hello data using [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) function with **INSERT** SQL statement.</span></span> <span data-ttu-id="caa64-148">Merhaba [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) PostgreSQL veritabanında kullanılan tooexecute hello SQL sorgu işlevdir.</span><span class="sxs-lookup"><span data-stu-id="caa64-148">hello [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> <span data-ttu-id="caa64-149">Merhaba konak, dbname, kullanıcı ve parola parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="caa64-149">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Drop previous table of same name if one exists
cursor.execute("DROP TABLE IF EXISTS inventory;")
print "Finished dropping table (if existed)"

# Create table
cursor.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
print "Finished creating table"

# Insert some data into table
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("banana", 150))
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("orange", 154))
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("apple", 100))
print "Inserted 3 rows of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

<span data-ttu-id="caa64-150">Merhaba çıktı aşağıdaki gibi görünür Hello kodu başarıyla çalıştıktan sonra:</span><span class="sxs-lookup"><span data-stu-id="caa64-150">After hello code runs successfully, hello output appears as follows:</span></span>

![Komut satırı çıktısı](media/connect-python/2-example-python-output.png)

## <a name="read-data"></a><span data-ttu-id="caa64-152">Verileri okuma</span><span class="sxs-lookup"><span data-stu-id="caa64-152">Read data</span></span>
<span data-ttu-id="caa64-153">Kullanım hello aşağıdaki kod kullanılarak eklenen tooread hello veri [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) ile işlev **seçin** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="caa64-153">Use hello following code tooread hello data inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **SELECT** SQL statement.</span></span> <span data-ttu-id="caa64-154">Bu işlev bir sorgu kabul eder ve bir sonuç kümesi getirir yinelendiğinde üzerinden hello kullanımı ile [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall).</span><span class="sxs-lookup"><span data-stu-id="caa64-154">This function accepts a query and returns a result set that can be iterated over with hello use of [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall).</span></span> <span data-ttu-id="caa64-155">Merhaba konak, dbname, kullanıcı ve parola parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="caa64-155">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Fetch all rows from table
cursor.execute("SELECT * FROM inventory;")
rows = cursor.fetchall()

# Print all rows
for row in rows:
    print "Data row = (%s, %s, %s)" %(str(row[0]), str(row[1]), str(row[2]))

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="update-data"></a><span data-ttu-id="caa64-156">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="caa64-156">Update data</span></span>
<span data-ttu-id="caa64-157">Kullanım hello aşağıdaki kod kullanarak, daha önce eklediğiniz tooupdate hello stok satır [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) ile işlev **güncelleştirme** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="caa64-157">Use hello following code tooupdate hello inventory row that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **UPDATE** SQL statement.</span></span> <span data-ttu-id="caa64-158">Merhaba konak, dbname, kullanıcı ve parola parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="caa64-158">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Update a data row in hello table
cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
print "Updated 1 row of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="delete-data"></a><span data-ttu-id="caa64-159">Verileri silme</span><span class="sxs-lookup"><span data-stu-id="caa64-159">Delete data</span></span>
<span data-ttu-id="caa64-160">Kullanım hello aşağıdaki kod toodelete kullanarak, daha önce eklediğiniz bir envanter öğesini [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) ile işlev **silmek** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="caa64-160">Use hello following code toodelete an inventory item that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **DELETE** SQL statement.</span></span> <span data-ttu-id="caa64-161">Merhaba konak, dbname, kullanıcı ve parola parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="caa64-161">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Delete data row from table
cursor.execute("DELETE FROM inventory WHERE name = %s;", ("orange",))
print "Deleted 1 row of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="caa64-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="caa64-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="caa64-163">Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme</span><span class="sxs-lookup"><span data-stu-id="caa64-163">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
