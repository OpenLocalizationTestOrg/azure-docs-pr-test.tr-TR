---
title: "Java kullanarak PostgreSQL için tooAzure veritabanına bağlanma | Microsoft Docs"
description: "Bu hızlı başlangıç PostgreSQL için Azure veritabanındaki verileri sorgulamak ve tooconnect için kullanabileceğiniz bir Java kod örneğini sağlar."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: java
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: 8f6e0a47a0d6dfebf29eb56c31ccccabd7c2b670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-java-tooconnect-and-query-data"></a><span data-ttu-id="94105-103">Azure veritabanı PostgreSQL için: kullanım Java tooconnect ve sorgu verileri</span><span class="sxs-lookup"><span data-stu-id="94105-103">Azure Database for PostgreSQL: Use Java tooconnect and query data</span></span>
<span data-ttu-id="94105-104">Bu hızlı başlangıç gösteren Azure tooconnect tooan veritabanı nasıl bir Java uygulaması kullanarak PostgreSQL için.</span><span class="sxs-lookup"><span data-stu-id="94105-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a Java application.</span></span> <span data-ttu-id="94105-105">Nasıl toouse SQL deyimleri tooquery, Ekle, Güncelleştir ve hello veritabanında bulunan verileri silme gösterir.</span><span class="sxs-lookup"><span data-stu-id="94105-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="94105-106">Merhaba bu makaledeki adımları Java kullanarak geliştirme ile tanıdık ve yeni tooworking Azure veritabanı PostgreSQL için sahip olduğunuz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="94105-106">hello steps in this article assume that you are familiar with developing using Java, and that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94105-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="94105-107">Prerequisites</span></span>
<span data-ttu-id="94105-108">Bu hızlı başlangıç Bu kılavuzlara birini başlangıç noktası olarak oluşturulan hello kaynakları kullanır:</span><span class="sxs-lookup"><span data-stu-id="94105-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="94105-109">DB Oluşturma - Portal</span><span class="sxs-lookup"><span data-stu-id="94105-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="94105-110">DB Oluşturma - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="94105-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="94105-111">Şunları da yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="94105-111">You also need to:</span></span>
- <span data-ttu-id="94105-112">Merhaba karşıdan [PostgreSQL JDBC sürücüsü](https://jdbc.postgresql.org/download.html) Java ve hello Java Geliştirme Seti sürümünüzle eşleşen.</span><span class="sxs-lookup"><span data-stu-id="94105-112">Download hello [PostgreSQL JDBC Driver](https://jdbc.postgresql.org/download.html) matching your version of Java and hello Java Development Kit.</span></span>
- <span data-ttu-id="94105-113">Merhaba PostgreSQL JDBC jar dosyasını (örneğin postgresql-42.1.1.jar), uygulama sınıf içerir.</span><span class="sxs-lookup"><span data-stu-id="94105-113">Include hello PostgreSQL JDBC jar file (for example postgresql-42.1.1.jar) in your application classpath.</span></span> <span data-ttu-id="94105-114">Daha fazla bilgi için bkz. [sınıf yolu ayrıntıları](https://jdbc.postgresql.org/documentation/head/classpath.html).</span><span class="sxs-lookup"><span data-stu-id="94105-114">For more information, see [classpath details](https://jdbc.postgresql.org/documentation/head/classpath.html).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="94105-115">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="94105-115">Get connection information</span></span>
<span data-ttu-id="94105-116">Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure veritabanı için PostgreSQL alın.</span><span class="sxs-lookup"><span data-stu-id="94105-116">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="94105-117">Tam sunucu adını ve oturum açma kimlik bilgileri hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="94105-117">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="94105-118">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="94105-118">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="94105-119">Merhaba sol taraftaki menüden Azure portalında, **tüm kaynakları** ve oluşturduğunuz, gibi hello sunucu araması **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="94105-119">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="94105-120">Merhaba sunucu adına tıklatarak **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="94105-120">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="94105-121">Select hello sunucunun **genel bakış** sayfası.</span><span class="sxs-lookup"><span data-stu-id="94105-121">Select hello server's **Overview** page.</span></span> <span data-ttu-id="94105-122">Merhaba Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.</span><span class="sxs-lookup"><span data-stu-id="94105-122">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="94105-123">![PostgreSQL için Azure Veritabanı - Sunucu Yöneticisi Oturum Açma Bilgileri](./media/connect-java/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="94105-123">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-java/1-connection-string.png)</span></span>
5. <span data-ttu-id="94105-124">Sunucu oturum açma bilgilerinizi unutursanız, toohello gidin **genel bakış** tooview hello sunucu yönetici oturum açma adı sayfasında ve gerekirse sıfırlamak hello parola.</span><span class="sxs-lookup"><span data-stu-id="94105-124">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="94105-125">Bağlanma, tablo oluşturma ve veri ekleme</span><span class="sxs-lookup"><span data-stu-id="94105-125">Connect, create table, and insert data</span></span>
<span data-ttu-id="94105-126">Merhaba işlevi kullanılarak kod tooconnect ve yük hello verileri aşağıdaki kullanım hello bir **Ekle** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="94105-126">Use hello following code tooconnect and load hello data using hello function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="94105-127">Merhaba yöntemleri [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), ve [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) kullanılan tooconnect olan bırakın ve hello tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="94105-127">hello methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) are used tooconnect, drop, and create hello table.</span></span> <span data-ttu-id="94105-128">Merhaba [prepareStatement](https://jdbc.postgresql.org/documentation/head/query.html) setString() ve setInt() toobind hello parametre değerleri ile kullanılan toobuild hello Ekle komutları bir nesnedir.</span><span class="sxs-lookup"><span data-stu-id="94105-128">hello [prepareStatement](https://jdbc.postgresql.org/documentation/head/query.html) object is used toobuild hello insert commands, with setString() and setInt() toobind hello parameter values.</span></span> <span data-ttu-id="94105-129">Yöntem [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) çalıştırır hello her parametre kümesi için komutu.</span><span class="sxs-lookup"><span data-stu-id="94105-129">Method [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) runs hello command for each set of parameters.</span></span> 

<span data-ttu-id="94105-130">Merhaba konak, veritabanı, kullanıcı ve parola parametrelerini kendi sunucu ve veritabanı oluşturduğunuzda, belirttiğiniz hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="94105-130">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class CreateTableInsertRows {

    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
                // Drop previous table of same name if one exists.
                Statement statement = connection.createStatement();
                statement.execute("DROP TABLE IF EXISTS inventory;");
                System.out.println("Finished dropping table (if existed).");
    
                // Create table.
                statement.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);");
                System.out.println("Created table.");
    
                // Insert some data into table.
                int nRowsInserted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("INSERT INTO inventory (name, quantity) VALUES (?, ?);");
                preparedStatement.setString(1, "banana");
                preparedStatement.setInt(2, 150);
                nRowsInserted += preparedStatement.executeUpdate();

                preparedStatement.setString(1, "orange");
                preparedStatement.setInt(2, 154);
                nRowsInserted += preparedStatement.executeUpdate();

                preparedStatement.setString(1, "apple");
                preparedStatement.setInt(2, 100);
                nRowsInserted += preparedStatement.executeUpdate();
                System.out.println(String.format("Inserted %d row(s) of data.", nRowsInserted));
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
    
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="read-data"></a><span data-ttu-id="94105-131">Verileri okuma</span><span class="sxs-lookup"><span data-stu-id="94105-131">Read data</span></span>
<span data-ttu-id="94105-132">Kullanım hello aşağıdaki kod tooread hello verilerle bir **seçin** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="94105-132">Use hello following code tooread hello data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="94105-133">Merhaba yöntemleri [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), ve [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) kullanılan tooconnect olan oluşturun ve hello select deyimi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="94105-133">hello methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) are used tooconnect, create, and run hello select statement.</span></span> <span data-ttu-id="94105-134">Merhaba sonuçları kullanılarak işlenir bir [sonuç kümesi](https://www.postgresql.org/docs/7.4/static/jdbc-query.html) nesnesi.</span><span class="sxs-lookup"><span data-stu-id="94105-134">hello results are processed using a [ResultSet](https://www.postgresql.org/docs/7.4/static/jdbc-query.html) object.</span></span> 

<span data-ttu-id="94105-135">Merhaba konak, veritabanı, kullanıcı ve parola parametrelerini kendi sunucu ve veritabanı oluşturduğunuzda, belirttiğiniz hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="94105-135">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class ReadTable {

    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
    
                Statement statement = connection.createStatement();
                ResultSet results = statement.executeQuery("SELECT * from inventory;");
                while (results.next())
                {
                    String outputString = 
                        String.format(
                            "Data row = (%s, %s, %s)",
                            results.getString(1),
                            results.getString(2),
                            results.getString(3));
                    System.out.println(outputString);
                }
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}

```

## <a name="update-data"></a><span data-ttu-id="94105-136">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="94105-136">Update data</span></span>
<span data-ttu-id="94105-137">Kullanım hello aşağıdaki kod toochange hello verilerle bir **güncelleştirme** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="94105-137">Use hello following code toochange hello data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="94105-138">Merhaba yöntemleri [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), ve [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) kullanılan tooconnect olan hazırlamak ve hello güncelleştirme deyimini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="94105-138">hello methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) are used tooconnect, prepare, and run hello update statement.</span></span> 

<span data-ttu-id="94105-139">Merhaba konak, veritabanı, kullanıcı ve parola parametrelerini kendi sunucu ve veritabanı oluşturduğunuzda, belirttiğiniz hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="94105-139">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class UpdateTable {
    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
                // Modify some data in table.
                int nRowsUpdated = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?;");
                preparedStatement.setInt(1, 200);
                preparedStatement.setString(2, "banana");
                nRowsUpdated += preparedStatement.executeUpdate();
                System.out.println(String.format("Updated %d row(s) of data.", nRowsUpdated));
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}
```
## <a name="delete-data"></a><span data-ttu-id="94105-140">Verileri silme</span><span class="sxs-lookup"><span data-stu-id="94105-140">Delete data</span></span>
<span data-ttu-id="94105-141">Kullanım hello aşağıdaki kod tooremove verilerle bir **silmek** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="94105-141">Use hello following code tooremove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="94105-142">Merhaba yöntemleri [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), ve [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) kullanılan tooconnect olan hazırlamak ve hello delete deyimini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="94105-142">hello methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) are used tooconnect, prepare, and run hello delete statement.</span></span> 

<span data-ttu-id="94105-143">Merhaba konak, veritabanı, kullanıcı ve parola parametrelerini kendi sunucu ve veritabanı oluşturduğunuzda, belirttiğiniz hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="94105-143">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class DeleteTable {
    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
                // Delete some data from table.
                int nRowsDeleted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("DELETE FROM inventory WHERE name = ?;");
                preparedStatement.setString(1, "orange");
                nRowsDeleted += preparedStatement.executeUpdate();
                System.out.println(String.format("Deleted %d row(s) of data.", nRowsDeleted));
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="94105-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="94105-144">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="94105-145">Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme</span><span class="sxs-lookup"><span data-stu-id="94105-145">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
