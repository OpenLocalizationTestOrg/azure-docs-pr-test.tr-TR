---
title: "Çok kiracılı SaaS uygulaması Azure SQL Database ile kullanma | Microsoft Docs"
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
ms.openlocfilehash: 0aea69d86a51c38c99a72f46737de1eea27bef83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="implement-a-multi-tenant-saas-application-using-azure-sql-database"></a><span data-ttu-id="58dd6-103">Azure SQL veritabanı kullanarak çok kiracılı SaaS uygulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="58dd6-103">Implement a multi-tenant SaaS application using Azure SQL Database</span></span>

<span data-ttu-id="58dd6-104">Çok kiracılı uygulama bulut ortamında bulunan bir uygulamasıdır ve Hizmetleri yüzlerce veya binlerce kimin etmeyin paylaşma veya diğer kişilerin verileri görmek kiracılar için aynı kümesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="58dd6-104">A multi-tenant application is an application hosted in a cloud environment and that provides the same set of services to hundreds or thousands of tenants who do not share or see each other’s data.</span></span> <span data-ttu-id="58dd6-105">Bulut tarafından barındırılan bir ortamda kiracıların hizmetleri sağlayan bir SaaS uygulaması örneğidir.</span><span class="sxs-lookup"><span data-stu-id="58dd6-105">An example is an SaaS application that provides services to tenants in a cloud-hosted environment.</span></span> <span data-ttu-id="58dd6-106">Bu model verileri için her bir kiracı yalıtır ve maliyet kaynakları dağıtımını iyileştirir.</span><span class="sxs-lookup"><span data-stu-id="58dd6-106">This model isolates the data for each tenant and optimizes the distribution of resources for cost.</span></span> 

<span data-ttu-id="58dd6-107">Bu öğretici, Azure SQL veritabanı kullanarak çok kiracılı SaaS uygulamasının nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="58dd6-107">This tutorial demonstrates how to create a multi-tenant SaaS application using Azure SQL Database.</span></span>

<span data-ttu-id="58dd6-108">Bu öğreticide, öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="58dd6-108">In this tutorial, you will learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="58dd6-109">Kiracı başına veritabanı modeli kullanarak bir çok kiracılı SaaS uygulaması desteklemek için bir veritabanı ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="58dd6-109">Set up a database environment to support a multi-tenant SaaS application, using the Database-per-tenant pattern</span></span>
> * <span data-ttu-id="58dd6-110">Kiracı katalog oluşturma</span><span class="sxs-lookup"><span data-stu-id="58dd6-110">Create a tenant catalog</span></span>
> * <span data-ttu-id="58dd6-111">Bir kiracı veritabanı sağlamak ve Kiracı Kataloğu'nda kaydetme</span><span class="sxs-lookup"><span data-stu-id="58dd6-111">Provision a tenant database and register it in the tenant catalog</span></span>
> * <span data-ttu-id="58dd6-112">Bir örnek Java uygulama ayarlama</span><span class="sxs-lookup"><span data-stu-id="58dd6-112">Set up a sample Java application</span></span> 
> * <span data-ttu-id="58dd6-113">Erişim Kiracı veritabanları basit bir Java konsol uygulaması</span><span class="sxs-lookup"><span data-stu-id="58dd6-113">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="58dd6-114">Bir kiracı Sil</span><span class="sxs-lookup"><span data-stu-id="58dd6-114">Delete a tenant</span></span>

<span data-ttu-id="58dd6-115">Bir Azure aboneliğiniz yoksa [ücretsiz bir hesap oluşturma](https://azure.microsoft.com/free/) başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="58dd6-115">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58dd6-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="58dd6-116">Prerequisites</span></span>

<span data-ttu-id="58dd6-117">Bu öğreticiyi tamamlamak için olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="58dd6-117">To complete this tutorial, make sure you have:</span></span>

* <span data-ttu-id="58dd6-118">PowerShell en yeni sürümünün yüklü ve [en son Azure PowerShell SDK'sı](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="58dd6-118">Installed the newest version of PowerShell and the [latest Azure PowerShell SDK](http://azure.microsoft.com/downloads/)</span></span>

* <span data-ttu-id="58dd6-119">En son sürümü yüklü [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="58dd6-119">Installed the latest version of [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span> <span data-ttu-id="58dd6-120">SQL Server Management Studio'yu yükleme SQLPackage, bir dizi veritabanı geliştirme görevlerini otomatikleştirmek için kullanılan bir komut satırı yardımcı programı en son sürümünü yükler.</span><span class="sxs-lookup"><span data-stu-id="58dd6-120">Installing SQL Server Management Studio also installs the latest version of SQLPackage, a command-line utility that can be used to automate a range of database development tasks.</span></span>

* <span data-ttu-id="58dd6-121">Yüklü [Java Çalışma zamanı ortamı (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) ve [en son JAVA Geliştirme Seti (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) makinenize yüklü.</span><span class="sxs-lookup"><span data-stu-id="58dd6-121">Installed the [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) and the [latest JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed on your machine.</span></span> 

* <span data-ttu-id="58dd6-122">Yüklü [Apache Maven](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="58dd6-122">Installed [Apache Maven](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="58dd6-123">Maven bağımlılıkları yönetme, derleme, test ve örnek Java projesi çalıştırma yardımcı olmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="58dd6-123">Maven will be used to help manage dependencies, build, test and run the sample Java project</span></span>

## <a name="set-up-data-environment"></a><span data-ttu-id="58dd6-124">Veri ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="58dd6-124">Set up data environment</span></span>

<span data-ttu-id="58dd6-125">Kiracı başına bir veritabanı sağlama.</span><span class="sxs-lookup"><span data-stu-id="58dd6-125">You will be provisioning a database per tenant.</span></span> <span data-ttu-id="58dd6-126">Kiracı başına veritabanı modeli en yüksek derecede az DevOps maliyeti ile kiracılar arasında yalıtım sağlar.</span><span class="sxs-lookup"><span data-stu-id="58dd6-126">The database-per-tenant model provides the highest degree of isolation between tenants, with little DevOps cost.</span></span> <span data-ttu-id="58dd6-127">Bulut kaynakları maliyetini en iyi duruma getirme, ayrıca Kiracı veritabanı grubu için fiyat performansı iyileştirmek izin veren bir esnek havuz içine sağlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="58dd6-127">To optimize the cost of cloud resources, you will also be provisioning the tenant databases into an elastic pool which allows you to optimize the price performance for a group of databases.</span></span> <span data-ttu-id="58dd6-128">Başka bir veritabanında modelleri sağlama hakkında bilgi edinmek için [Burada gördüğünüz](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span><span class="sxs-lookup"><span data-stu-id="58dd6-128">To learn about other database provisioning models [see here](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span></span>

<span data-ttu-id="58dd6-129">Bir SQL server ve tüm Kiracı veritabanlarını barındıracak bir esnek havuz oluşturmak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="58dd6-129">Follow these steps to create a SQL server and an elastic pool that will host all your tenant databases.</span></span> 

1. <span data-ttu-id="58dd6-130">Öğreticinin geri kalanını kullanılacak değerlerini depolamak için değişkenler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="58dd6-130">Create variables to store values that will be used in the rest of the tutorial.</span></span> <span data-ttu-id="58dd6-131">IP adresi eklemek için IP adresi değişken değiştirdiğinizden emin olun</span><span class="sxs-lookup"><span data-stu-id="58dd6-131">Make sure to modify the IP address variable to include your IP address</span></span> 
   
   ```PowerShell 
   # Set an admin login and password for your database
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   
   # Create random unique names for logical server and tenants
   $servername = "server-$(Get-Random)"
   $tenant1 = "geolamice"
   $tenant2 = "ranplex"
   
   # Store current client IP address (modify to include your IP address)
   $startIpAddress = 0.0.0.0 
   $endIpAddress = 0.0.0.0
   ```
   
2. <span data-ttu-id="58dd6-132">Azure oturum açma ve SQL server ve esnek havuz oluşturma</span><span class="sxs-lookup"><span data-stu-id="58dd6-132">Login to Azure and create a SQL server and elastic pool</span></span> 
   
   ```PowerShell
   # Login to Azure 
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
   
## <a name="create-tenant-catalog"></a><span data-ttu-id="58dd6-133">Kiracı Katalog Oluştur</span><span class="sxs-lookup"><span data-stu-id="58dd6-133">Create tenant catalog</span></span> 

<span data-ttu-id="58dd6-134">Çok kiracılı bir SaaS uygulaması bir kiracı için bilgi depolandığı bilmeniz önemlidir.</span><span class="sxs-lookup"><span data-stu-id="58dd6-134">In a multi-tenant SaaS application, it’s important to know where information for a tenant is stored.</span></span> <span data-ttu-id="58dd6-135">Bu, genellikle bir katalog veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="58dd6-135">This is commonly stored in a catalog database.</span></span> <span data-ttu-id="58dd6-136">Katalog veritabanı, bir kiracı ve bu kiracının veri depolandığı bir veritabanı arasında bir eşleme tutmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="58dd6-136">The catalog database is used to hold a mapping between a tenant and a database in which that tenant’s data is stored.</span></span>  <span data-ttu-id="58dd6-137">Tek Kiracı veritabanı kullanılan veya bir çok kiracılı olup olmadığını temel deseni uygular.</span><span class="sxs-lookup"><span data-stu-id="58dd6-137">The basic pattern applies whether a multi-tenant or a single-tenant database is used.</span></span>

<span data-ttu-id="58dd6-138">Örnek SaaS uygulaması için bir katalog veritabanı oluşturmak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="58dd6-138">Follow these steps to create a catalog database for the sample SaaS application.</span></span>

```PowerShell
# Create empty database in pool
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "tenantCatalog" `
    -ElasticPoolName "myElasticPool"

# Create table to track mapping between tenants and their databases
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

## <a name="provision-database-for-tenant1-and-register-in-tenant-catalog"></a><span data-ttu-id="58dd6-139">Veritabanı için 'tenant1' sağlamak ve Kiracı kataloğunda kaydetme</span><span class="sxs-lookup"><span data-stu-id="58dd6-139">Provision database for 'tenant1' and register in tenant catalog</span></span> 
<span data-ttu-id="58dd6-140">Bir veritabanı için yeni bir kiracı 'tenant1' sağlamak ve bu Kiracı kataloğa kaydetmek için PowerShell kullanın.</span><span class="sxs-lookup"><span data-stu-id="58dd6-140">Use Powershell to provision a database for a new tenant 'tenant1' and register this tenant in the catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant1'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into the table 
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

# Register 'tenant1' in the tenant catalog 
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

## <a name="provision-database-for-tenant2-and-register-in-tenant-catalog"></a><span data-ttu-id="58dd6-141">Veritabanı için 'tenant2' sağlamak ve Kiracı kataloğunda kaydetme</span><span class="sxs-lookup"><span data-stu-id="58dd6-141">Provision database for 'tenant2' and register in tenant catalog</span></span>
<span data-ttu-id="58dd6-142">Bir veritabanı için yeni bir kiracı 'tenant2' sağlamak ve bu Kiracı kataloğa kaydetmek için PowerShell kullanın.</span><span class="sxs-lookup"><span data-stu-id="58dd6-142">Use Powershell to provision a database for a new tenant 'tenant2' and register this tenant in the catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant2'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant2 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into the table 
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

# Register tenant 'tenant2' in the tenant catalog 
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

## <a name="set-up-sample-java-application"></a><span data-ttu-id="58dd6-143">Örnek Java uygulama ayarlama</span><span class="sxs-lookup"><span data-stu-id="58dd6-143">Set up sample Java application</span></span> 

1. <span data-ttu-id="58dd6-144">Bir maven projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="58dd6-144">Create a maven project.</span></span> <span data-ttu-id="58dd6-145">Bir komut istemi penceresinde aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="58dd6-145">Type the following in a command prompt window:</span></span>
   
   ```
   mvn archetype:generate -DgroupId=com.microsoft.sqlserver -DartifactId=mssql-jdbc -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   
2. <span data-ttu-id="58dd6-146">Bu bağımlılık, dil düzeyi ekleyin ve bildirim dosyası pom.xml dosyasını Kavanoz desteklemek için seçeneği yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="58dd6-146">Add this dependency, language level, and build option to support manifest files in jars to the pom.xml file:</span></span>
   
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

3. <span data-ttu-id="58dd6-147">Aşağıdaki App.java dosyasını içine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="58dd6-147">Add the following into the App.java file:</span></span>

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
   
   System.out.println(" " + CMD_QUIT + " - quit the application\n");
   
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
   
   // List all tenants that currently exist in the system
   
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
   
   // Query the data that was previously inserted into the primary database from the geo replicated database
   
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

4. <span data-ttu-id="58dd6-148">Dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="58dd6-148">Save the file.</span></span>

5. <span data-ttu-id="58dd6-149">Komut konsoluna gidin ve yürütme</span><span class="sxs-lookup"><span data-stu-id="58dd6-149">Go to command console and execute</span></span>

   ```bash
   mvn package
   ```

6. <span data-ttu-id="58dd6-150">Bunu yaptıktan sonra uygulamayı çalıştırmak için aşağıdakileri yürütün</span><span class="sxs-lookup"><span data-stu-id="58dd6-150">When finished, execute the following to run the application</span></span> 
   
   ```
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```
   
<span data-ttu-id="58dd6-151">Başarıyla tamamlanırsa çıktı şuna benzeyecektir:</span><span class="sxs-lookup"><span data-stu-id="58dd6-151">The output will look like this if it runs successfully:</span></span>

```
############################

## SAAS DATABASE TUTORIAL ##

############################

OPTIONS

LIST - list tenants

QUERY <NAME> - connect and tenant query tenant <NAME>

QUIT - quit the application

* List the tenants

* Query tenants you created
```

## <a name="delete-first-tenant"></a><span data-ttu-id="58dd6-152">İlk Kiracı Sil</span><span class="sxs-lookup"><span data-stu-id="58dd6-152">Delete first tenant</span></span> 
<span data-ttu-id="58dd6-153">İlk Kiracı için Kiracı veritabanı ve Katalog girişi silmek için PowerShell kullanın.</span><span class="sxs-lookup"><span data-stu-id="58dd6-153">Use PowerShell to delete the tenant database and catalog entry for the first tenant.</span></span>

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

<span data-ttu-id="58dd6-154">'Tenant1' bağlanmayı deneyin Java uygulaması kullanarak.</span><span class="sxs-lookup"><span data-stu-id="58dd6-154">Try connecting to 'tenant1' using the Java application.</span></span> <span data-ttu-id="58dd6-155">Kiracı mevcut olmadığını bildiren bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="58dd6-155">You will get an error stating that the tenant does not exist.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58dd6-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="58dd6-156">Next steps</span></span> 

<span data-ttu-id="58dd6-157">Bu öğreticide için öğrenilen:</span><span class="sxs-lookup"><span data-stu-id="58dd6-157">In this tutorial, you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="58dd6-158">Kiracı başına veritabanı modeli kullanarak bir çok kiracılı SaaS uygulaması desteklemek için bir veritabanı ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="58dd6-158">Set up a database environment to support a multi-tenant SaaS application, using the Database-per-tenant pattern</span></span>
> * <span data-ttu-id="58dd6-159">Kiracı katalog oluşturma</span><span class="sxs-lookup"><span data-stu-id="58dd6-159">Create a tenant catalog</span></span>
> * <span data-ttu-id="58dd6-160">Bir kiracı veritabanı sağlamak ve Kiracı Kataloğu'nda kaydetme</span><span class="sxs-lookup"><span data-stu-id="58dd6-160">Provision a tenant database and register it in the tenant catalog</span></span>
> * <span data-ttu-id="58dd6-161">Bir örnek Java uygulama ayarlama</span><span class="sxs-lookup"><span data-stu-id="58dd6-161">Set up a sample Java application</span></span> 
> * <span data-ttu-id="58dd6-162">Erişim Kiracı veritabanları basit bir Java konsol uygulaması</span><span class="sxs-lookup"><span data-stu-id="58dd6-162">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="58dd6-163">Bir kiracı Sil</span><span class="sxs-lookup"><span data-stu-id="58dd6-163">Delete a tenant</span></span>

* <span data-ttu-id="58dd6-164">Ortak görevler için PowerShell örnekleri görmek [SQL veritabanı PowerShell örnekleri](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span><span class="sxs-lookup"><span data-stu-id="58dd6-164">PowerShell samples for common tasks, see [SQL Database PowerShell samples](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span></span>

* <span data-ttu-id="58dd6-165">Tasarım desenleri çok kiracılı SaaS uygulamaları bakın [tasarım desenleri](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span><span class="sxs-lookup"><span data-stu-id="58dd6-165">Design patterns for multi-tenant SaaS applications see [Design patterns](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span></span>

* <span data-ttu-id="58dd6-166">Azure ortak görevler için Java örnekleri görmek [Java Geliştirici Merkezi](https://azure.microsoft.com/develop/java/)</span><span class="sxs-lookup"><span data-stu-id="58dd6-166">Java samples for common Azure tasks, see [Java Developer Center](https://azure.microsoft.com/develop/java/)</span></span>



