---
title: "TooAzure veritabanı için MySQL Java kullanarak bağlanma | Microsoft Docs"
description: "Bu hızlı başlangıç MySQL veritabanı için bir Azure veritabanındaki verileri sorgulamak ve tooconnect için kullanabileceğiniz bir Java kod örneğini sağlar."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.devlang: java
ms.date: 06/20/2017
ms.openlocfilehash: d584b5491d29700b36fae26800c59d93ceb3e265
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-java-tooconnect-and-query-data"></a><span data-ttu-id="d1468-103">Azure veritabanı için MySQL: kullanım Java tooconnect ve sorgu verileri</span><span class="sxs-lookup"><span data-stu-id="d1468-103">Azure Database for MySQL: Use Java tooconnect and query data</span></span>
<span data-ttu-id="d1468-104">Bu hızlı başlangıç gösteren Azure tooconnect tooan veritabanı nasıl bir Java uygulaması kullanarak MySQL için.</span><span class="sxs-lookup"><span data-stu-id="d1468-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a Java application.</span></span> <span data-ttu-id="d1468-105">Nasıl toouse SQL deyimleri tooquery, Ekle, Güncelleştir ve hello veritabanında bulunan verileri silme gösterir.</span><span class="sxs-lookup"><span data-stu-id="d1468-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="d1468-106">Merhaba bu makaledeki adımları Java kullanarak geliştirme ile tanıdık olduğunuz ve Azure veritabanı için MySQL ile yeni tooworking olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="d1468-106">hello steps in this article assume that you are familiar with developing using Java, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1468-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d1468-107">Prerequisites</span></span>
<span data-ttu-id="d1468-108">Bu hızlı başlangıç Bu kılavuzlara birini başlangıç noktası olarak oluşturulan hello kaynakları kullanır:</span><span class="sxs-lookup"><span data-stu-id="d1468-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="d1468-109">Azure portalını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="d1468-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="d1468-110">Azure CLI kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="d1468-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="d1468-111">Şunları da yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d1468-111">You also need to:</span></span>
- <span data-ttu-id="d1468-112">Merhaba JDBC sürücüsü yüklemek [MySQL bağlayıcı/J](https://dev.mysql.com/downloads/connector/j/)</span><span class="sxs-lookup"><span data-stu-id="d1468-112">Download hello JDBC driver [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/)</span></span>
- <span data-ttu-id="d1468-113">Merhaba JDBC jar dosyasını (örneğin mysql-bağlayıcı-java-5.1.42-bin.jar), uygulama sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d1468-113">Include hello JDBC jar file (for example mysql-connector-java-5.1.42-bin.jar) into your application classpath.</span></span> <span data-ttu-id="d1468-114">Bu konuda sorun yaşıyorsanız, lütfen ortamınızın [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) veya [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html) gibi sınıf yolu ayrıntıları hakkındaki belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="d1468-114">If you have trouble with this, please consult your environment's documentation for class path specifics, such as [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) or [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html)</span></span>
- <span data-ttu-id="d1468-115">Azure veritabanınız MySQL bağlantı güvenliği için açılan hello güvenlik duvarı ile yapılandırıldığından emin olun ve SSL ayarları için uygulama tooconnect başarıyla ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="d1468-115">Ensure your Azure Database for MySQL connection security is configured with hello firewall opened and SSL settings adjusted for your application tooconnect successfully.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="d1468-116">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="d1468-116">Get connection information</span></span>
<span data-ttu-id="d1468-117">Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure veritabanı için MySQL alın.</span><span class="sxs-lookup"><span data-stu-id="d1468-117">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="d1468-118">Tam sunucu adını ve oturum açma kimlik bilgileri hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="d1468-118">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="d1468-119">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d1468-119">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d1468-120">Merhaba sol bölmede **tüm kaynakları**ve ardından oluşturduğunuz hello sunucusu için arama (örneğin, **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="d1468-120">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="d1468-121">Merhaba sunucu adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d1468-121">Click hello server name.</span></span>
4. <span data-ttu-id="d1468-122">Select hello sunucunun **özellikleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="d1468-122">Select hello server's **Properties** page.</span></span> <span data-ttu-id="d1468-123">Merhaba Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.</span><span class="sxs-lookup"><span data-stu-id="d1468-123">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="d1468-124">![MySQL için Azure Veritabanı sunucu adı](./media/connect-java/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="d1468-124">![Azure Database for MySQL server name](./media/connect-java/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="d1468-125">Sunucu oturum açma bilgilerinizi unutursanız, toohello gidin **genel bakış** tooview hello sunucu yönetici oturum açma adı sayfasında ve gerekirse sıfırlamak hello parola.</span><span class="sxs-lookup"><span data-stu-id="d1468-125">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="d1468-126">Bağlanma, tablo oluşturma ve veri ekleme</span><span class="sxs-lookup"><span data-stu-id="d1468-126">Connect, create table, and insert data</span></span>
<span data-ttu-id="d1468-127">Merhaba işlevi kullanılarak kod tooconnect ve yük hello verileri aşağıdaki kullanım hello bir **Ekle** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="d1468-127">Use hello following code tooconnect and load hello data using hello function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="d1468-128">Merhaba [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) kullanılan tooconnect tooMySQL bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="d1468-128">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span> <span data-ttu-id="d1468-129">Yöntemleri [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) ve execute() kullanılan toodrop ve hello tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d1468-129">Methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and execute() are used toodrop and create hello table.</span></span> <span data-ttu-id="d1468-130">Merhaba prepareStatement setString() ve setInt() toobind hello parametre değerleri ile kullanılan toobuild hello Ekle komutları nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="d1468-130">hello prepareStatement object is used toobuild hello insert commands, with setString() and setInt() toobind hello parameter values.</span></span> <span data-ttu-id="d1468-131">Yöntem executeUpdate() her parametreleri tooinsert hello değer kümesi için hello komutu çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="d1468-131">Method executeUpdate() runs hello command for each set of parameters tooinsert hello values.</span></span> 

<span data-ttu-id="d1468-132">Merhaba konak, veritabanı, kullanıcı ve parola parametrelerini kendi sunucu ve veritabanı oluşturduğunuzda, belirttiğiniz hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d1468-132">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class CreateTableInsertRows {

    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables. 
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);

            // Set connection properties.
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");

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

## <a name="read-data"></a><span data-ttu-id="d1468-133">Verileri okuma</span><span class="sxs-lookup"><span data-stu-id="d1468-133">Read data</span></span>
<span data-ttu-id="d1468-134">Kullanım hello aşağıdaki kod tooread hello verilerle bir **seçin** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="d1468-134">Use hello following code tooread hello data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="d1468-135">Merhaba [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) kullanılan tooconnect tooMySQL bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="d1468-135">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span> <span data-ttu-id="d1468-136">Merhaba yöntemleri [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) ve executeQuery() kullanılan tooconnect ve hello select deyimi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d1468-136">hello methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and executeQuery() are used tooconnect and run hello select statement.</span></span> <span data-ttu-id="d1468-137">Merhaba sonuçları kullanılarak işlenir bir [sonuç kümesi](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) nesnesi.</span><span class="sxs-lookup"><span data-stu-id="d1468-137">hello results are processed using a [ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) object.</span></span> 

<span data-ttu-id="d1468-138">Merhaba konak, veritabanı, kullanıcı ve parola parametrelerini kendi sunucu ve veritabanı oluşturduğunuzda, belirttiğiniz hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d1468-138">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class ReadTable {

    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables.
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);

            // Set connection properties.
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");
            
            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase", e);
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
                throw new SQLException("Encountered an error when executing given sql statement", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase."); 
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="update-data"></a><span data-ttu-id="d1468-139">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="d1468-139">Update data</span></span>
<span data-ttu-id="d1468-140">Kullanım hello aşağıdaki kod toochange hello verilerle bir **güncelleştirme** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="d1468-140">Use hello following code toochange hello data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="d1468-141">Merhaba [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) kullanılan tooconnect tooMySQL bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="d1468-141">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span> <span data-ttu-id="d1468-142">Merhaba yöntemleri [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) ve executeUpdate() kullanılan tooprepare ve hello güncelleştirme deyimini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d1468-142">hello methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used tooprepare and run hello update statement.</span></span> 

<span data-ttu-id="d1468-143">Merhaba konak, veritabanı, kullanıcı ve parola parametrelerini kendi sunucu ve veritabanı oluşturduğunuzda, belirttiğiniz hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d1468-143">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class UpdateTable {
    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables. 
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }
        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");

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

## <a name="delete-data"></a><span data-ttu-id="d1468-144">Verileri silme</span><span class="sxs-lookup"><span data-stu-id="d1468-144">Delete data</span></span>
<span data-ttu-id="d1468-145">Kullanım hello aşağıdaki kod tooremove verilerle bir **silmek** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="d1468-145">Use hello following code tooremove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="d1468-146">Merhaba [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) kullanılan tooconnect tooMySQL bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="d1468-146">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span>  <span data-ttu-id="d1468-147">Merhaba yöntemleri [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) ve executeUpdate() kullanılan tooprepare ve hello güncelleştirme deyimini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d1468-147">hello methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used tooprepare and run hello update statement.</span></span> 

<span data-ttu-id="d1468-148">Merhaba konak, veritabanı, kullanıcı ve parola parametrelerini kendi sunucu ve veritabanı oluşturduğunuzda, belirttiğiniz hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d1468-148">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class DeleteTable {
    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables.
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";
        
        // check that hello driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");
            
            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase", e);
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

## <a name="next-steps"></a><span data-ttu-id="d1468-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d1468-149">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="d1468-150">MySQL veritabanı tooAzure veritabanı için MySQL döküm ve geri yükleme kullanarak geçirme</span><span class="sxs-lookup"><span data-stu-id="d1468-150">Migrate your MySQL database tooAzure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
