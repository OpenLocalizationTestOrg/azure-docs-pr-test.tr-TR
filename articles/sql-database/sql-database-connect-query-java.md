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
# <a name="use-java-tooquery-an-azure-sql-database"></a>Java tooquery Azure SQL veritabanını kullan

Bu hızlı başlangıç gösteren nasıl toouse [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) tooconnect tooan Azure SQL veritabanı ve Transact-SQL deyimleri tooquery verileri kullanın.

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu hızlı başlangıç Öğreticisi, Önkoşullar aşağıdaki hello sahip olduğunuzdan emin olun:

- Bir Azure SQL veritabanı. Bu hızlı başlangıç Bu hızlı başlangıçlar birinde oluşturulan hello kaynakları kullanır: 

   - [DB Oluşturma - Portal](sql-database-get-started-portal.md)
   - [DB oluşturma - CLI](sql-database-get-started-cli.md)
   - [DB Oluşturma - PowerShell](sql-database-get-started-powershell.md)

- A [sunucu düzeyinde güvenlik duvarı kuralı](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) hello için genel IP adresi hello bilgisayarın bu hızlı başlangıç öğreticisi için kullanın.

- İşletim sisteminiz için Java ve ilgili yazılımları yüklediniz.

    - **MacOS**: Homebrew ve Java’yı ve ardından Maven’i yükleyin. Bkz: [1.2 ve 1.3 adımları](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).
    - **Ubuntu**: hello Java Geliştirme Seti ve Maven yükleyin. Bkz: [1.2, 1.3 ve 1.4 adımları](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).
    - **Windows**: hello Java Geliştirme Seti ve Maven yükleyin. Bkz: [1.2 ve 1.3 adımları](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).    

## <a name="sql-server-connection-information"></a>SQL Server bağlantı bilgileri

Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure SQL veritabanı alın. Merhaba tam sunucu adını, veritabanı adının ve oturum açma bilgilerini hello sonraki yordamlarda gerekir.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Seçin **SQL veritabanları** hello sol taraftaki menüden veritabanınızda hello tıklatıp **SQL veritabanları** sayfası. 
3. Merhaba üzerinde **genel bakış** sayfasında veritabanınız için görüntü aşağıdaki hello gösterildiği gibi hello tam sunucu adını gözden geçirin: hello sunucu adı toobring hello yukarı üzerine getirin **tıklatın toocopy** seçeneği.  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Sunucu oturum açma bilgilerinizi unutursanız, toohello SQL veritabanı sunucusu sayfa tooview hello sunucu yönetici adı gidin.  Gerekirse, hello parola sıfırlama.     

## <a name="create-maven-project-and-dependencies"></a>**Maven projesi ve bağımlılıklarını oluşturma**
1. Terminal Hello adlı yeni bir Maven projesi oluşturun **sqltest**. 

   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=sqltest" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```

2. İstendiğinde **Y** girin.
3. Dizini çok değiştirmek**sqltest** açarak ***pom.xml*** , sık kullandığınız metin düzenleyiciyi ile.  Merhaba eklemek **SQL Server için Microsoft JDBC sürücüsü** kullanarak tooyour proje bağımlılıklarınızı hello kodu:

   ```xml
   <dependency>
       <groupId>com.microsoft.sqlserver</groupId>
       <artifactId>mssql-jdbc</artifactId>
       <version>6.2.1.jre8</version>
   </dependency>
   ```

4. Ayrıca, ***pom.xml***, Özellikler tooyour proje aşağıdaki hello ekleyin.  Özellikler bölümü yoksa, başlangıç bağımlılıkları sonra ekleyebilirsiniz.

   ```xml
   <properties>
       <maven.compiler.source>1.8</maven.compiler.source>
       <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```

5. ***Pom.xml*** dosyasını kaydedin ve kapatın.

## <a name="insert-code-tooquery-sql-database"></a>Kod tooquery SQL veritabanı Ekle

1. Maven projenizde, şu konumda zaten ***App.java*** adlı bir dosyanız olmalıdır: ..\sqltest\src\main\java\com\sqlsamples\App.java

2. Merhaba dosya ve içeriğinin hello aşağıdaki ile kod ve sunucu, veritabanı, kullanıcı ve parola için uygun değerleri hello ekleme Değiştir açın.

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

## <a name="run-hello-code"></a>Merhaba kodu çalıştırma

1. Merhaba komut isteminde aşağıdaki komutları hello çalıştırın:

   ```bash
   mvn package
   mvn -q exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```

2. Merhaba üst 20 satır döndürülür ve hello uygulama penceresini kapatın doğrulayın.


## <a name="next-steps"></a>Sonraki adımlar
- [İlk Azure SQL veritabanınızı tasarlama](sql-database-design-first-database.md)
- [SQL Server için Microsoft JDBC sürücüsü](https://github.com/microsoft/mssql-jdbc)
- [Sorun bildirin/soru sorun](https://github.com/microsoft/mssql-jdbc/issues)

