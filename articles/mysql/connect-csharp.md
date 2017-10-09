---
title: "C# üzerinden MySQL için tooAzure veritabanına bağlanma | Microsoft Docs"
description: "Bu hızlı başlangıç MySQL için Azure veritabanındaki verileri sorgulamak ve tooconnect için kullanabileceğiniz bir C# (.NET) kod örneğini sağlar."
services: MySQL
author: seanli1988
ms.author: seal
manager: janders
editor: jasonwhowell
ms.service: MySQL-database
ms.custom: mvc
ms.devlang: csharp
ms.topic: hero-article
ms.date: 07/10/2017
ms.openlocfilehash: 0dca98186199a40ef9cc592b93c3b2e815260273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-net-c-tooconnect-and-query-data"></a>Azure veritabanı için MySQL: kullanım .NET (C#) tooconnect ve sorgu verileri
Bu hızlı başlangıç gösteren Azure tooconnect tooan veritabanı nasıl bir C# uygulaması kullanarak MySQL için. Nasıl toouse SQL deyimleri tooquery, Ekle, Güncelleştir ve hello veritabanında bulunan verileri silme gösterir. Merhaba bu makaledeki adımları kullanarak C# geliştirme ile tanıdık olduğunuz ve Azure veritabanı için MySQL ile yeni tooworking olduğunu varsayalım.

## <a name="prerequisites"></a>Ön koşullar
Bu hızlı başlangıç Bu kılavuzlara birini başlangıç noktası olarak oluşturulan hello kaynakları kullanır:
- [Azure portalını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Azure CLI kullanarak MySQL için Azure Veritabanı sunucusu oluşturma](./quickstart-create-mysql-server-database-using-azure-cli.md)

Şunları da yapmanız gerekir:
- [.NET](https://www.microsoft.com/net/download) yükleyin. (Windows, Ubuntu Linux veya macOS) platformunuz için özel olarak bağlı hello makale tooinstall .NET Hello adımları izleyin. 
- [Visual Studio](https://www.visualstudio.com/downloads/)’yu yükleyin.
- [MySQL için ODBC Sürücüsü](https://dev.mysql.com/downloads/connector/odbc/)’nü yükleyin.

## <a name="get-connection-information"></a>Bağlantı bilgilerini alma
Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure veritabanı için MySQL alın. Tam sunucu adını ve oturum açma kimlik bilgileri hello gerekir.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Merhaba sol taraftaki menüden Azure portalında, **tüm kaynakları** ve oluşturduğunuz, gibi hello sunucu araması **myserver4demo**.
3. Merhaba sunucu adına tıklayın.
4. Select hello sunucunun **özellikleri** sayfası. Merhaba Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.
 ![MySQL için Azure Veritabanı sunucu adı](./media/connect-csharp/1_server-properties-name-login.png)
5. Sunucu oturum açma bilgilerinizi unutursanız, toohello gidin **genel bakış** tooview hello sunucu yönetici oturum açma adı sayfasında ve gerekirse sıfırlamak hello parola.

## <a name="connect-create-table-and-insert-data"></a>Bağlanma, tablo oluşturma ve veri ekleme
Kullanım hello aşağıdakileri tooconnect kod ve verileri hello kullanarak yük **CREATE TABLE** ve **INSERT INTO** SQL deyimlerini. Merhaba kodu kullanan ODBC sınıfı yöntemiyle [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish bağlantı tooMySQL. Merhaba kod yöntemi kullanıyorsa [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx)hello CommandText özelliği ayarlar ve yöntemini çağırır [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello veritabanı komutları. 

Merhaba konak, DBName, kullanıcı ve parola parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle değiştirin. 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using MySql.Data;
using System.Data.Odbc;

namespace driver
{
    class MySQLCreate
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText = "DROP TABLE IF EXISTS inventory;";
            command.ExecuteNonQuery();
            Console.Out.WriteLine("Finished dropping table (if existed)");

            command.CommandText = "CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);";
            command.ExecuteNonQuery();
            Console.Out.WriteLine("Finished creating table");

            command.CommandText =
                String.Format(
                    @"INSERT INTO inventory (name, quantity) VALUES ({0}, {1});
                    INSERT INTO inventory (name, quantity) VALUES ({2}, {3});
                    INSERT INTO inventory (name, quantity) VALUES ({4}, {5});",
                    "\'banana\'", 150,
                    "\'orange\'", 154,
                    "\'apple\'", 100
                    );

            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows inserted={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }

    }
}

```

## <a name="read-data"></a>Verileri okuma

Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **seçin** SQL deyimi. Merhaba kodu kullanan ODBC sınıfı yöntemiyle [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish bağlantı tooMySQL. Merhaba kod yöntemi kullanıyorsa [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx) ve yöntemi [ExecuteReader()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executereader(v=vs.110).aspx) toorun hello veritabanı komutları. Kod kullanan'sonraki hello [Read()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcdatareader.read(v=vs.110).aspx) hello sonuçlarında tooadvance toohello kaydeder. Daha sonra hello kod hello kaydında Getınt32 ve GetString tooparse hello değerleri kullanır.

Merhaba konak, DBName, kullanıcı ve parola parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle değiştirin. 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using MySql.Data;
using System.Data.Odbc;


namespace driver
{
    class MySQLRead
    {

        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText = "SELECT * FROM inventory;";

            var reader = command.ExecuteReader();
            while (reader.Read())
            {
                Console.WriteLine(
                    string.Format(
                        "Reading from table=({0}, {1}, {2})",
                        reader.GetInt32(0).ToString(),
                        reader.GetString(1),
                        reader.GetInt32(2).ToString()
                        )
                    );
            }

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}


```

## <a name="update-data"></a>Verileri güncelleştirme
Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **güncelleştirme** SQL deyimi. Merhaba kodu kullanan ODBC sınıfı yöntemiyle [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish bağlantı tooMySQL. Merhaba kod yöntemi kullanıyorsa [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx)hello CommandText özelliği ayarlar ve yöntemini çağırır [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello veritabanı komutları.

Merhaba konak, DBName, kullanıcı ve parola parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle değiştirin. 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.Odbc;

namespace driver
{
    class MySQLUpdate
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText =
            String.Format("UPDATE inventory SET quantity = {0} WHERE name = {1};",
                200,
                "\'banana\'"
                );

            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows updated={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}



```


## <a name="delete-data"></a>Verileri silme
Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri silme bir **silmek** SQL deyimi. 

Merhaba kodu kullanan ODBC sınıfı yöntemiyle [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish bağlantı tooMySQL. Merhaba kod yöntemi kullanıyorsa [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx)hello CommandText özelliği ayarlar ve yöntemini çağırır [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello veritabanı komutları.

Merhaba konak, DBName, kullanıcı ve parola parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle değiştirin. 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.Odbc;

namespace driver
{
    class MySQLDelete
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText =
                String.Format("DELETE FROM inventory WHERE name = {0};",
                    "\'orange\'");
            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows deleted={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}

```

## <a name="next-steps"></a>Sonraki adımlar
> [!div class="nextstepaction"]
> [MySQL veritabanı tooAzure veritabanı için MySQL döküm ve geri yükleme kullanarak geçirme](concepts-migrate-dump-restore.md)
