---
title: "Azure SQL Database aaaImplement çok kiracılı SaaS uygulaması | Microsoft Docs"
description: "Çok kiracılı SaaS uygulamasına Azure SQL Database uygulayın."
services: sql-database
documentationcenter: 
author: AyoOlubeko
manager: jhubbard
editor: monicar
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,scale out apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/08/2017
ms.author: AyoOlubek
ms.openlocfilehash: b87b8f296e2c20a8f674b56375f43fdc92df76d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-a-multi-tenant-saas-application-using-azure-sql-database"></a>Azure SQL veritabanı kullanarak çok kiracılı SaaS uygulaması kullanma

Çok kiracılı uygulama bulut ortamında bulunan bir uygulamasıdır ve aynı Hizmetleri toohundreds ya da kimin etmeyin paylaşma veya diğer kişilerin verileri görmek kiracılar binlerce kümesidir hello sağlar. Bulut tarafından barındırılan bir ortamda Hizmetleri tootenants sağlayan bir SaaS uygulaması örneğidir. Bu model, her bir kiracı için hello veri yalıtır ve hello dağıtım maliyeti için kaynakların en iyi duruma getirir. 

Bu öğretici gösterir nasıl toocreate Azure SQL Database kullanan çok kiracılı SaaS uygulamasına.

Bu öğreticide, öğreneceksiniz:
> [!div class="checklist"]
> * Bir veritabanı ortamı toosupport hello Kiracı başına veritabanı modeli kullanarak bir çok kiracılı SaaS uygulaması ayarlayın
> * Kiracı katalog oluşturma
> * Bir kiracı veritabanı sağlamak ve hello Kiracı kataloğunda kaydetme
> * Bir örnek Java uygulama ayarlama 
> * Erişim Kiracı veritabanları basit bir Java konsol uygulaması
> * Bir kiracı Sil

Bir Azure aboneliğiniz yoksa [ücretsiz bir hesap oluşturma](https://azure.microsoft.com/free/) başlamadan önce.

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu öğretici, yapma emin olduğunuz:

* PowerShell ve hello en yeni sürümü yüklü hello [en son Azure PowerShell SDK'sı](http://azure.microsoft.com/downloads/)

* Yüklü hello en son sürümünü [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms). SQL Server Management Studio'yu yükleme hello SQLPackage, kullanılan tooautomate veritabanı geliştirme görevleri bir dizi olabilir bir komut satırı yardımcı programı en son sürümünü yükler.

* Yüklü hello [Java Çalışma zamanı ortamı (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) ve hello [en son JAVA Geliştirme Seti (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) makinenize yüklü. 

* Yüklü [Apache Maven](https://maven.apache.org/download.cgi). Maven kullanılacak toohelp bağımlılıkları yönetme, derleme, test ve hello örnek Java projesi çalıştırma

## <a name="set-up-data-environment"></a>Veri ortamını ayarlama

Kiracı başına bir veritabanı sağlama. Merhaba Kiracı başına veritabanı modeli hello yüksek derecede az DevOps maliyeti ile kiracılar arasında yalıtım sağlar. toooptimize hello maliyet bulut kaynaklarının, aynı zamanda hello Kiracı veritabanları veritabanları grubu için toooptimize hello fiyat performans sağlayan bir esnek havuz içine sağlayacaksınız. modelleri sağlama diğer veritabanıyla ilgili toolearn [Burada gördüğünüz](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).

Bu adımları toocreate bir SQL server ve tüm Kiracı veritabanlarını barındıracak bir esnek havuz izleyin. 

1. Değişkenleri kullanılacak toostore değerleri hello öğreticinin hello kalan oluşturun. IP adresiniz emin toomodify başlangıç IP adresi değişken tooinclude olun 
   
   ```PowerShell 
   # Set an admin login and password for your database
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   
   # Create random unique names for logical server and tenants
   $servername = "server-$(Get-Random)"
   $tenant1 = "geolamice"
   $tenant2 = "ranplex"
   
   # Store current client IP address (modify tooinclude your IP address)
   $startIpAddress = 0.0.0.0 
   $endIpAddress = 0.0.0.0
   ```
   
2. Oturum açma tooAzure ve SQL server ve esnek havuz oluşturma 
   
   ```PowerShell
   # Login tooAzure 
   Login-AzureRmAccount
   
   # Create resource group 
   New-AzureRmResourceGroup -Name "myResourceGroup" -Location "northcentralus"
   
   # Create logical SQL Server with firewall rules 
   New-AzureRmSqlServer -ResourceGroupName "myResourceGroup" `
       -ServerName $servername `
       -Location "northcentralus" `
       -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   
   New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
       -ServerName $servername `
       -FirewallRuleName "singleAddress" -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
   
   # Create elastic pool 
   New-AzureRmSqlElasticPool -ResourceGroupName "myResourceGroup"
       -ServerName $servername `
       -ElasticPoolName "myElasticPool" `
       -Edition "Standard" `
       -Dtu 50 `
       -DatabaseDtuMin 10 `
       -DatabaseDtuMax 20
   ```
   
## <a name="create-tenant-catalog"></a>Kiracı Katalog Oluştur 

Çok kiracılı bir SaaS uygulaması bir kiracı için bilgi depolandığı önemli tooknow değil. Bu, genellikle bir katalog veritabanında depolanır. başlangıç kataloğu kullanılan toohold bir kiracı ve bu kiracının veri depolandığı bir veritabanı arasında bir eşleme veritabanıdır.  tek Kiracı veritabanı kullanılan veya bir çok kiracılı olup olmadığını Hello temel deseni uygular.

Bu adımları toocreate Merhaba örnek SaaS uygulaması için bir katalog veritabanı izleyin.

```PowerShell
# Create empty database in pool
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "tenantCatalog" `
    -ElasticPoolName "myElasticPool"

# Create table tootrack mapping between tenants and their databases
$commandText = "
CREATE TABLE Tenants
(
   TenantId         INT IDENTITY PRIMARY KEY,
   TenantName       NVARCHAR(128) NOT NULL,
   TenantDatabase   NVARCHAR(128) NOT NULL
);

CREATE INDEX IX_TenantName ON Tenants (TenantName);"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="provision-database-for-tenant1-and-register-in-tenant-catalog"></a>Veritabanı için 'tenant1' sağlamak ve Kiracı kataloğunda kaydetme 
PowerShell tooprovision bir veritabanı için yeni bir kiracı 'tenant1' kullanın ve bu Kiracı hello kataloğunda kaydedin. 

```PowerShell
# Create empty database in pool for 'tenant1'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into hello table 
$commandText = "
CREATE TABLE WhoAmI (TenantName NVARCHAR(128) NOT NULL);
INSERT INTO WhoAmI VALUES ('Tenant $tenant1');"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database $tenant1 `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Register 'tenant1' in hello tenant catalog 
$commandText = "
INSERT INTO Tenants VALUES ('$tenant1', '$tenant1');"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="provision-database-for-tenant2-and-register-in-tenant-catalog"></a>Veritabanı için 'tenant2' sağlamak ve Kiracı kataloğunda kaydetme
PowerShell tooprovision bir veritabanı için yeni bir kiracı 'tenant2' kullanın ve bu Kiracı hello kataloğunda kaydedin. 

```PowerShell
# Create empty database in pool for 'tenant2'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant2 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into hello table 
$commandText = "
CREATE TABLE WhoAmI (TenantName NVARCHAR(128) NOT NULL);
INSERT INTO WhoAmI VALUES ('Tenant $tenant2');"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database $tenant2 `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Register tenant 'tenant2' in hello tenant catalog 
$commandText = "
INSERT INTO Tenants VALUES ('$tenant2', '$tenant2');"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="set-up-sample-java-application"></a>Örnek Java uygulama ayarlama 

1. Bir maven projesi oluşturun. Bir komut istemi penceresinde Hello aşağıdakileri yazın:
   
   ```
   mvn archetype:generate -DgroupId=com.microsoft.sqlserver -DartifactId=mssql-jdbc -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   
2. Bu bağımlılık, dil düzeyi ekleyin ve seçeneği toosupport bildirim dosyalarında Kavanoz toohello pom.xml dosyasını oluşturun:
   
   ```XML
   <dependency>
         <groupId>com.microsoft.sqlserver</groupId>
         <artifactId>mssql-jdbc</artifactId>
         <version>6.1.0.jre8</version>
   </dependency>
   
   <properties>
         <maven.compiler.source>1.8</maven.compiler.source>
         <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   
   <build>
        <plugins>
           <plugin>
              <groupId>org.apache.maven.plugins</groupId>
              <artifactId>maven-jar-plugin</artifactId>
              <version>3.0.0</version>
              <configuration>
                 <archive>
                    <manifest>
                       <mainClass>com.sqldbsamples.App</mainClass>
                    </manifest>
                 </archive>
              </configuration>
           </plugin>
        </plugins>
   </build>
   ```

3. Merhaba App.java dosyasına Hello aşağıdakileri ekleyin:

   ```java 
   package com.sqldbsamples;
   
   import java.util.Map;
   
   import java.util.HashMap;
   
   import java.io.BufferedReader;
   
   import java.io.InputStreamReader;
   
   import java.sql.Connection;
   
   import java.sql.Statement;
   
   import java.sql.PreparedStatement;
   
   import java.sql.ResultSet;
   
   import java.sql.DriverManager;
   
   public class App {
   
   private static final String SERVER_NAME = "your-server-name";
   
   private static final String CATALOG_DB_NAME = "tenantCatalog";
   
   private static final String USER = "ServerAdmin";
   
   private static final String PASSWORD = "ChangeYourAdminPassword1";
   
   private static final String CATALOG_DB_URL = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", SERVER_NAME, CATALOG_DB_NAME, USER, PASSWORD);
   
   private static final String CMD_LIST = "LIST";

   private static final String CMD_QUERY = "QUERY";

   private static final String CMD_QUIT = "QUIT";
   
   public static void main(String[] args) {
   
   System.out.println("\n############################");
   
   System.out.println("## SAAS DATABASE TUTORIAL ##");
   
   System.out.println("############################\n");
   
   System.out.println("OPTIONS");
   
   System.out.println(" " + CMD_LIST + " - list tenants");
   
   System.out.println(" " + CMD_QUERY + " <NAME> - connect and tenant query tenant <NAME>");
   
   System.out.println(" " + CMD_QUIT + " - quit hello application\n");
   
   try (BufferedReader br = new BufferedReader(new InputStreamReader(System.in))) {
   
   while(true) {
   
   String[] input = br.readLine().split("\\s");
   
   if (null != input && input.length > 0) {
   
   if (input[0].equalsIgnoreCase(CMD_LIST)) {
   
   listTenants();
   
   } else if (input[0].toLowerCase().startsWith(CMD_QUERY.toLowerCase()) && input.length == 2) {
   
   queryTenant(input[1].trim());
   
   } else if (input[0].equalsIgnoreCase(CMD_QUIT)) {
   
   break;
   
   } else {
   
   System.out.println(" -> Command not supported");
   
   }
   
   }
   
   System.out.println("");
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   }
   
   private static void listTenants() {
   
   // List all tenants that currently exist in hello system
   
   String sql = "SELECT TenantName FROM Tenants";
   
   try (Connection connection = DriverManager.getConnection(CATALOG_DB_URL);
   
   Statement stmt = connection.createStatement();
   
   ResultSet resultSet = stmt.executeQuery(sql)) {
   
   while (resultSet.next()) {
   
   System.out.println(" -> " + resultSet.getString(1));
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   }
   
   private static void queryTenant(String name) {
   
   // Query hello data that was previously inserted into hello primary database from hello geo replicated database
   
   String url = null;
   
   String sql = "SELECT TenantDatabase FROM Tenants WHERE TenantName = ?";
   
   try (Connection connection = DriverManager.getConnection(CATALOG_DB_URL);
   
   PreparedStatement pstmt = connection.prepareStatement(sql)) {
   
   pstmt.setString(1, name);
   
   try (ResultSet resultSet = pstmt.executeQuery()) {
   
   if (resultSet.next()) {
   
   url = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", SERVER_NAME, resultSet.getString(1), USER, PASSWORD);
   
   }
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   if (null != url) {
   
   String tenantSql = "SELECT TenantName FROM WhoAmI";
   
   try (Connection connection = DriverManager.getConnection(url);
   
   Statement stmt = connection.createStatement();

   ResultSet resultSet = stmt.executeQuery(tenantSql)) {
   
   while (resultSet.next()) {
   
   System.out.println(" -> Entry in table WhoAmI in tenant " + name + " is: " + resultSet.getString(1));
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   } else {
   
   System.out.println(" -> Tenant " + name + " not found");
   
   }
   
   }
   
   }
   ```

4. Merhaba dosyasını kaydedin.

5. Toocommand Konsolu gidin ve yürütme

   ```bash
   mvn package
   ```

6. Tamamlandığında, toorun Merhaba uygulaması aşağıdaki hello yürütme 
   
   ```
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```
   
başarıyla tamamlanırsa hello çıktı şuna benzeyecektir:

```
############################

## SAAS DATABASE TUTORIAL ##

############################

OPTIONS

LIST - list tenants

QUERY <NAME> - connect and tenant query tenant <NAME>

QUIT - quit hello application

* List hello tenants

* Query tenants you created
```

## <a name="delete-first-tenant"></a>İlk Kiracı Sil 
Veritabanı ve Katalog PowerShell toodelete hello Kiracı girişi hello ilk Kiracı için kullanın.

```PowerShell
# Remove 'tenant1' from catalog 
$commandText = "DELETE FROM Tenants WHERE TenantName = '$tenant1';"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Delete database 
Remove-AzureRmSqlDatabase -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1
```

Bağlanmayı deneyin çok 'tenant1' kullanarak izin ver hello Java uygulaması. Merhaba Kiracı yok bildiren bir hata alırsınız.

## <a name="next-steps"></a>Sonraki adımlar 

Bu öğreticide için öğrenilen:
> [!div class="checklist"]
> * Bir veritabanı ortamı toosupport hello Kiracı başına veritabanı modeli kullanarak bir çok kiracılı SaaS uygulaması ayarlayın
> * Kiracı katalog oluşturma
> * Bir kiracı veritabanı sağlamak ve hello Kiracı kataloğunda kaydetme
> * Bir örnek Java uygulama ayarlama 
> * Erişim Kiracı veritabanları basit bir Java konsol uygulaması
> * Bir kiracı Sil

* Ortak görevler için PowerShell örnekleri görmek [SQL veritabanı PowerShell örnekleri](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)

* Tasarım desenleri çok kiracılı SaaS uygulamaları bakın [tasarım desenleri](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)

* Azure ortak görevler için Java örnekleri görmek [Java Geliştirici Merkezi](https://azure.microsoft.com/develop/java/)



