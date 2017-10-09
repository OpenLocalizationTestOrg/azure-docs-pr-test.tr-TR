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
# <a name="azure-database-for-mysql-use-python-tooconnect-and-query-data"></a>Azure veritabanı için MySQL: kullanım Python tooconnect ve sorgu verileri
Bu hızlı başlangıç gösteren nasıl toouse [Python](https://python.org) tooconnect tooan Azure veritabanı için MySQL. Mac OS, Ubuntu Linux ve Windows platformları hello veritabanında SQL deyimleri tooquery, ekleme, güncelleştirme ve silme verilerini kullanır. Bu makalede Hello adımlarda Python kullanarak geliştirme ile bilgi sahibiyseniz ve yeni tooworking Azure veritabanı MySQL için sahip olduğunuz varsayılır.

## <a name="prerequisites"></a>Ön koşullar
Bu hızlı başlangıç Bu kılavuzlara birini başlangıç noktası olarak oluşturulan hello kaynakları kullanır:
- [Azure portalını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Azure CLI kullanarak MySQL için Azure Veritabanı sunucusu oluşturma](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-python-and-hello-mysql-connector"></a>Python'ı yükleyin ve MySQL bağlayıcı hello
Yükleme [Python](https://www.python.org/downloads/) ve hello [Python MySQL bağlayıcı](https://dev.mysql.com/downloads/connector/python/) kendi makinede. Platformunuz bağlı olarak hello adımları izleyin:

### <a name="windows"></a>Windows
1. Python 2.7’yi [python.org](https://www.python.org/downloads/windows/) adresinden indirin ve yükleyin. 
2. Merhaba Python yükleme hello komut istemi başlatarak denetleyin. Merhaba komutu çalıştırmak `C:\python27\python.exe -V` hello büyük V anahtar toosee hello sürüm numarasını kullanarak.
3. Merhaba Python bağlayıcı MySQL'den Yükle [mysql.com](https://dev.mysql.com/downloads/connector/python/) Python ilgili tooyour sürümü.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. Linux (Ubuntu), Python genellikle hello varsayılan yüklemesinin bir parçası yüklenir.
2. Merhaba Python yükleme hello bash kabuğunda başlatarak denetleyin. Merhaba komutu çalıştırmak `python -V` hello büyük V anahtar toosee hello sürüm numarasını kullanarak.
3. Merhaba çalıştırarak Hello PIP yükleme denetimi `pip show pip -V` komut toosee hello sürüm numarası. 
4. PIP, Python’un bazı sürümlerine eklenmiş olabilir. PIP yüklü değilse hello [PIP] (https://pip.pypa.io/en/stable/installing/) yükleyebilir komutunu çalıştırarak paket `sudo apt-get install python-pip`.
5. Merhaba çalıştırarak güncelleştirme PIP toohello en son sürümü, `pip install -U pip` komutu.
6. Merhaba MySQL bağlayıcı Python ve bağımlılıklarını hello PIP komutunu kullanarak yükleyin:

   ```bash
   sudo pip install mysql-connector-python-rf
   ```
 
### <a name="macos"></a>macOS
1. MAC'te Python genellikle hello varsayılan işletim sistemi yüklemesinin bir parçası yüklenir.
2. Merhaba Python yükleme hello bash kabuğunda başlatarak denetleyin. Merhaba komutu çalıştırmak `python -V` hello büyük V anahtar toosee hello sürüm numarasını kullanarak.
3. Merhaba çalıştırarak Hello PIP yükleme denetimi `pip show pip -V` komut toosee hello sürüm numarası.
4. PIP, Python’un bazı sürümlerine eklenmiş olabilir. PIP yüklü değilse hello yükleyebilir [PIP](https://pip.pypa.io/en/stable/installing/) paket.
5. Merhaba çalıştırarak güncelleştirme PIP toohello en son sürümü, `pip install -U pip` komutu.
6. Merhaba MySQL bağlayıcı Python ve bağımlılıklarını hello PIP komutunu kullanarak yükleyin:

   ```bash
   pip install mysql-connector-python-rf
   ```

## <a name="get-connection-information"></a>Bağlantı bilgilerini alma
Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure veritabanı için MySQL alın. Tam sunucu adını ve oturum açma kimlik bilgileri hello gerekir.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Merhaba sol taraftaki menüden Azure portalında, **tüm kaynakları** ve aramak için creased, gibi hello sunucu **myserver4demo**.
3. Merhaba sunucu adına tıklatarak **myserver4demo**.
4. Select hello sunucunun **özellikleri** sayfası. Merhaba Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.
 ![MySQL için Azure Veritabanı - Sunucu Yöneticisi Oturum Açma](./media/connect-python/1_server-properties-name-login.png)
5. Sunucu oturum açma bilgilerinizi unutursanız, toohello gidin **genel bakış** tooview hello sunucu yönetici oturum açma adı sayfasında ve gerekirse sıfırlamak hello parola.
   

## <a name="run-python-code"></a>Python Kodunu Çalıştırma
- Merhaba kod bir metin dosyasına yapıştırın ve proje klasörüne C:\pythonmysql\createtable.py veya /home/username/pythonmysql/createtable.py gibi dosya uzantısı .py ile Merhaba dosyasını kaydedin
- toorun hello kod hello komut istemi başlatın veya kabuk bash. Dizini, proje klasörünüzle değiştirin (`cd pythonmysql`). Merhaba dosya adından hello python komut yazarak `python createtable.py` toorun Merhaba uygulaması. Hello Windows işletim sistemi, Python.exe'yi bulunmazsa, hello tam yolu toohello yürütülebilir sağlayın veya hello Python yolu hello yol ortam değişkenine ekleyin. `C:\python27\python.exe createtable.py`

## <a name="connect-create-table-and-insert-data"></a>Bağlanma, tablo oluşturma ve veri ekleme
Kullanım hello aşağıdaki kod tooconnect toohello sunucu, bir tablo oluşturun ve verileri hello kullanarak yük bir **Ekle** SQL deyimi. 

Merhaba kodda hello mysql.connector kitaplığı içeri aktarılır. Merhaba [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) işlevidir kullanılan tooconnect tooAzure hello kullanarak MySQL veritabanı [bağlantı bağımsız değişkenleri](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) hello config koleksiyonundaki. Merhaba kod hello bağlantıda bir imleç kullanır ve [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) yöntemi MySQL veritabanı hello SQL sorgusunu çalıştırır. 

Hello yerine `host`, `user`, `password`, ve `database` parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle.

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

## <a name="read-data"></a>Verileri okuma
Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **seçin** SQL deyimi. 

Merhaba kodda hello mysql.connector kitaplığı içeri aktarılır. Merhaba [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) işlevidir kullanılan tooconnect tooAzure hello kullanarak MySQL veritabanı [bağlantı bağımsız değişkenleri](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) hello config koleksiyonundaki. Merhaba kod hello bağlantıda bir imleç kullanır ve [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) yöntemi MySQL veritabanında hello SQL deyimini yürütür. Merhaba veri satırına hello kullanarak okunur [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) yöntemi. Merhaba sonuç kümesi bir koleksiyon satırda tutulur ve yineleyici hello satır üzerinde kullanılan tooloop için.

Hello yerine `host`, `user`, `password`, ve `database` parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle.

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

## <a name="update-data"></a>Verileri güncelleştirme
Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak veri güncelleştirme bir **güncelleştirme** SQL deyimi. 

Merhaba kodda hello mysql.connector kitaplığı içeri aktarılır.  Merhaba [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) işlevidir kullanılan tooconnect tooAzure hello kullanarak MySQL veritabanı [bağlantı bağımsız değişkenleri](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) hello config koleksiyonundaki. Merhaba kod hello bağlantıda bir imleç kullanır ve [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) yöntemi MySQL veritabanında hello SQL deyimini yürütür. 

Hello yerine `host`, `user`, `password`, ve `database` parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle.

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

## <a name="delete-data"></a>Verileri silme
Kullanım hello aşağıdaki tooconnect kod ve verileri kullanarak kaldırma bir **silmek** SQL deyimi. 

Merhaba kodda hello mysql.connector kitaplığı içeri aktarılır.  Merhaba [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) işlevidir kullanılan tooconnect tooAzure hello kullanarak MySQL veritabanı [bağlantı bağımsız değişkenleri](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) hello config koleksiyonundaki. Merhaba kod hello bağlantıda bir imleç kullanır ve [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) yöntemi MySQL veritabanı hello SQL sorgusunu çalıştırır. 

Hello yerine `host`, `user`, `password`, ve `database` parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle.

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

## <a name="next-steps"></a>Sonraki adımlar
> [!div class="nextstepaction"]
> [Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme](./concepts-migrate-import-export.md)
