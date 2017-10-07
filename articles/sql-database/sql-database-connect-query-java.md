---
title: "aaaUse Java tooquery Azure SQL veritabanı | Microsoft Docs"
description: "Bu konu, nasıl gösterir toouse Java toocreate tooan Azure SQL veritabanı ve sorgu Transact-SQL deyimi kullanarak bağlanan bir program."
services: sql-database
documentationcenter: 
author: ajlam
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: andrela
ms.openlocfilehash: f014edbe38ca0e7b6e43f4eb4d2e53d3561bf3e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-java-tooquery-an-azure-sql-database"></a><span data-ttu-id="a24d9-103">Java tooquery Azure SQL veritabanını kullan</span><span class="sxs-lookup"><span data-stu-id="a24d9-103">Use Java tooquery an Azure SQL database</span></span>

<span data-ttu-id="a24d9-104">Bu hızlı başlangıç gösteren nasıl toouse [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) tooconnect tooan Azure SQL veritabanı ve Transact-SQL deyimleri tooquery verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="a24d9-104">This quick start demonstrates how toouse [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) tooconnect tooan Azure SQL database and then use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a24d9-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a24d9-105">Prerequisites</span></span>

<span data-ttu-id="a24d9-106">toocomplete Bu hızlı başlangıç Öğreticisi, Önkoşullar aşağıdaki hello sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="a24d9-106">toocomplete this quick start tutorial, make sure you have hello following prerequisites:</span></span>

- <span data-ttu-id="a24d9-107">Bir Azure SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="a24d9-107">An Azure SQL database.</span></span> <span data-ttu-id="a24d9-108">Bu hızlı başlangıç Bu hızlı başlangıçlar birinde oluşturulan hello kaynakları kullanır:</span><span class="sxs-lookup"><span data-stu-id="a24d9-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="a24d9-109">DB Oluşturma - Portal</span><span class="sxs-lookup"><span data-stu-id="a24d9-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="a24d9-110">DB oluşturma - CLI</span><span class="sxs-lookup"><span data-stu-id="a24d9-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="a24d9-111">DB Oluşturma - PowerShell</span><span class="sxs-lookup"><span data-stu-id="a24d9-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="a24d9-112">A [sunucu düzeyinde güvenlik duvarı kuralı](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) hello için genel IP adresi hello bilgisayarın bu hızlı başlangıç öğreticisi için kullanın.</span><span class="sxs-lookup"><span data-stu-id="a24d9-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="a24d9-113">İşletim sisteminiz için Java ve ilgili yazılımları yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="a24d9-113">You have installed Java and related software for your operating system.</span></span>

    - <span data-ttu-id="a24d9-114">**MacOS**: Homebrew ve Java’yı ve ardından Maven’i yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a24d9-114">**MacOS**: Install Homebrew and Java, and then install Maven.</span></span> <span data-ttu-id="a24d9-115">Bkz: [1.2 ve 1.3 adımları](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).</span><span class="sxs-lookup"><span data-stu-id="a24d9-115">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).</span></span>
    - <span data-ttu-id="a24d9-116">**Ubuntu**: hello Java Geliştirme Seti ve Maven yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a24d9-116">**Ubuntu**:  Install hello Java Development Kit, and install Maven.</span></span> <span data-ttu-id="a24d9-117">Bkz: [1.2, 1.3 ve 1.4 adımları](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="a24d9-117">See [Step 1.2, 1.3, and 1.4](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).</span></span>
    - <span data-ttu-id="a24d9-118">**Windows**: hello Java Geliştirme Seti ve Maven yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a24d9-118">**Windows**: Install hello Java Development Kit, and Maven.</span></span> <span data-ttu-id="a24d9-119">Bkz: [1.2 ve 1.3 adımları](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).</span><span class="sxs-lookup"><span data-stu-id="a24d9-119">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="a24d9-120">SQL Server bağlantı bilgileri</span><span class="sxs-lookup"><span data-stu-id="a24d9-120">SQL server connection information</span></span>

<span data-ttu-id="a24d9-121">Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure SQL veritabanı alın.</span><span class="sxs-lookup"><span data-stu-id="a24d9-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="a24d9-122">Merhaba tam sunucu adını, veritabanı adının ve oturum açma bilgilerini hello sonraki yordamlarda gerekir.</span><span class="sxs-lookup"><span data-stu-id="a24d9-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="a24d9-123">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a24d9-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a24d9-124">Seçin **SQL veritabanları** hello sol taraftaki menüden veritabanınızda hello tıklatıp **SQL veritabanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="a24d9-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="a24d9-125">Merhaba üzerinde **genel bakış** sayfasında veritabanınız için görüntü aşağıdaki hello gösterildiği gibi hello tam sunucu adını gözden geçirin: hello sunucu adı toobring hello yukarı üzerine getirin **tıklatın toocopy** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="a24d9-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image: You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="a24d9-127">Sunucu oturum açma bilgilerinizi unutursanız, toohello SQL veritabanı sunucusu sayfa tooview hello sunucu yönetici adı gidin.</span><span class="sxs-lookup"><span data-stu-id="a24d9-127">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name.</span></span>  <span data-ttu-id="a24d9-128">Gerekirse, hello parola sıfırlama.</span><span class="sxs-lookup"><span data-stu-id="a24d9-128">If necessary, reset hello password.</span></span>     

## <a name="create-maven-project-and-dependencies"></a><span data-ttu-id="a24d9-129">**Maven projesi ve bağımlılıklarını oluşturma**</span><span class="sxs-lookup"><span data-stu-id="a24d9-129">**Create Maven project and dependencies**</span></span>
1. <span data-ttu-id="a24d9-130">Terminal Hello adlı yeni bir Maven projesi oluşturun **sqltest**.</span><span class="sxs-lookup"><span data-stu-id="a24d9-130">From hello terminal, create a new Maven project called **sqltest**.</span></span> 

   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=sqltest" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```

2. <span data-ttu-id="a24d9-131">İstendiğinde **Y** girin.</span><span class="sxs-lookup"><span data-stu-id="a24d9-131">Enter **Y** when prompted.</span></span>
3. <span data-ttu-id="a24d9-132">Dizini çok değiştirmek**sqltest** açarak ***pom.xml*** , sık kullandığınız metin düzenleyiciyi ile.</span><span class="sxs-lookup"><span data-stu-id="a24d9-132">Change directory too**sqltest** and open ***pom.xml*** with your favorite text editor.</span></span>  <span data-ttu-id="a24d9-133">Merhaba eklemek **SQL Server için Microsoft JDBC sürücüsü** kullanarak tooyour proje bağımlılıklarınızı hello kodu:</span><span class="sxs-lookup"><span data-stu-id="a24d9-133">Add hello **Microsoft JDBC Driver for SQL Server** tooyour project's dependencies using hello following code:</span></span>

   ```xml
   <dependency>
       <groupId>com.microsoft.sqlserver</groupId>
       <artifactId>mssql-jdbc</artifactId>
       <version>6.2.1.jre8</version>
   </dependency>
   ```

4. <span data-ttu-id="a24d9-134">Ayrıca, ***pom.xml***, Özellikler tooyour proje aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a24d9-134">Also in ***pom.xml***, add hello following properties tooyour project.</span></span>  <span data-ttu-id="a24d9-135">Özellikler bölümü yoksa, başlangıç bağımlılıkları sonra ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a24d9-135">If you don't have a properties section, you can add it after hello dependencies.</span></span>

   ```xml
   <properties>
       <maven.compiler.source>1.8</maven.compiler.source>
       <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```

5. <span data-ttu-id="a24d9-136">***Pom.xml*** dosyasını kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="a24d9-136">Save and close ***pom.xml***.</span></span>

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="a24d9-137">Kod tooquery SQL veritabanı Ekle</span><span class="sxs-lookup"><span data-stu-id="a24d9-137">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="a24d9-138">Maven projenizde, şu konumda zaten ***App.java*** adlı bir dosyanız olmalıdır: ..\sqltest\src\main\java\com\sqlsamples\App.java</span><span class="sxs-lookup"><span data-stu-id="a24d9-138">You should already have a file called ***App.java*** in your Maven project located at:  ..\sqltest\src\main\java\com\sqlsamples\App.java</span></span>

2. <span data-ttu-id="a24d9-139">Merhaba dosya ve içeriğinin hello aşağıdaki ile kod ve sunucu, veritabanı, kullanıcı ve parola için uygun değerleri hello ekleme Değiştir açın.</span><span class="sxs-lookup"><span data-stu-id="a24d9-139">Open hello file and replace its contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.DriverManager;

   public class App {

    public static void main(String[] args) {
    
        // Connect toodatabase
           String hostName = "your_server.database.windows.net";
           String dbName = "your_database";
           String user = "your_username";
           String password = "your_password";
           String url = String.format("jdbc:sqlserver://%s:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", hostName, dbName, user, password);
           Connection connection = null;

           try {
                   connection = DriverManager.getConnection(url);
                   String schema = connection.getSchema();
                   System.out.println("Successful connection - Schema: " + schema);

                   System.out.println("Query data example:");
                   System.out.println("=========================================");

                   // Create and execute a SELECT SQL statement.
                   String selectSql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName " 
                       + "FROM [SalesLT].[ProductCategory] pc "  
                       + "JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid";
                
                   try (Statement statement = connection.createStatement();
                       ResultSet resultSet = statement.executeQuery(selectSql)) {

                           // Print results from select statement
                           System.out.println("Top 20 categories:");
                           while (resultSet.next())
                           {
                               System.out.println(resultSet.getString(1) + " "
                                   + resultSet.getString(2));
                           }
                    connection.close();
                   }                   
           }
           catch (Exception e) {
                   e.printStackTrace();
           }
       }
   }
   ```

## <a name="run-hello-code"></a><span data-ttu-id="a24d9-140">Merhaba kodu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="a24d9-140">Run hello code</span></span>

1. <span data-ttu-id="a24d9-141">Merhaba komut isteminde aşağıdaki komutları hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a24d9-141">At hello command prompt, run hello following commands:</span></span>

   ```bash
   mvn package
   mvn -q exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```

2. <span data-ttu-id="a24d9-142">Merhaba üst 20 satır döndürülür ve hello uygulama penceresini kapatın doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a24d9-142">Verify that hello top 20 rows are returned and then close hello application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a24d9-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a24d9-143">Next steps</span></span>
- [<span data-ttu-id="a24d9-144">İlk Azure SQL veritabanınızı tasarlama</span><span class="sxs-lookup"><span data-stu-id="a24d9-144">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="a24d9-145">SQL Server için Microsoft JDBC sürücüsü</span><span class="sxs-lookup"><span data-stu-id="a24d9-145">Microsoft JDBC Driver for SQL Server</span></span>](https://github.com/microsoft/mssql-jdbc)
- [<span data-ttu-id="a24d9-146">Sorun bildirin/soru sorun</span><span class="sxs-lookup"><span data-stu-id="a24d9-146">Report issues/ask questions</span></span>](https://github.com/microsoft/mssql-jdbc/issues)

