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
# <a name="implement-a-multi-tenant-saas-application-using-azure-sql-database"></a><span data-ttu-id="7e386-103">Azure SQL veritabanı kullanarak çok kiracılı SaaS uygulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="7e386-103">Implement a multi-tenant SaaS application using Azure SQL Database</span></span>

<span data-ttu-id="7e386-104">Çok kiracılı uygulama bulut ortamında bulunan bir uygulamasıdır ve aynı Hizmetleri toohundreds ya da kimin etmeyin paylaşma veya diğer kişilerin verileri görmek kiracılar binlerce kümesidir hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="7e386-104">A multi-tenant application is an application hosted in a cloud environment and that provides hello same set of services toohundreds or thousands of tenants who do not share or see each other’s data.</span></span> <span data-ttu-id="7e386-105">Bulut tarafından barındırılan bir ortamda Hizmetleri tootenants sağlayan bir SaaS uygulaması örneğidir.</span><span class="sxs-lookup"><span data-stu-id="7e386-105">An example is an SaaS application that provides services tootenants in a cloud-hosted environment.</span></span> <span data-ttu-id="7e386-106">Bu model, her bir kiracı için hello veri yalıtır ve hello dağıtım maliyeti için kaynakların en iyi duruma getirir.</span><span class="sxs-lookup"><span data-stu-id="7e386-106">This model isolates hello data for each tenant and optimizes hello distribution of resources for cost.</span></span> 

<span data-ttu-id="7e386-107">Bu öğretici gösterir nasıl toocreate Azure SQL Database kullanan çok kiracılı SaaS uygulamasına.</span><span class="sxs-lookup"><span data-stu-id="7e386-107">This tutorial demonstrates how toocreate a multi-tenant SaaS application using Azure SQL Database.</span></span>

<span data-ttu-id="7e386-108">Bu öğreticide, öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="7e386-108">In this tutorial, you will learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="7e386-109">Bir veritabanı ortamı toosupport hello Kiracı başına veritabanı modeli kullanarak bir çok kiracılı SaaS uygulaması ayarlayın</span><span class="sxs-lookup"><span data-stu-id="7e386-109">Set up a database environment toosupport a multi-tenant SaaS application, using hello Database-per-tenant pattern</span></span>
> * <span data-ttu-id="7e386-110">Kiracı katalog oluşturma</span><span class="sxs-lookup"><span data-stu-id="7e386-110">Create a tenant catalog</span></span>
> * <span data-ttu-id="7e386-111">Bir kiracı veritabanı sağlamak ve hello Kiracı kataloğunda kaydetme</span><span class="sxs-lookup"><span data-stu-id="7e386-111">Provision a tenant database and register it in hello tenant catalog</span></span>
> * <span data-ttu-id="7e386-112">Bir örnek Java uygulama ayarlama</span><span class="sxs-lookup"><span data-stu-id="7e386-112">Set up a sample Java application</span></span> 
> * <span data-ttu-id="7e386-113">Erişim Kiracı veritabanları basit bir Java konsol uygulaması</span><span class="sxs-lookup"><span data-stu-id="7e386-113">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="7e386-114">Bir kiracı Sil</span><span class="sxs-lookup"><span data-stu-id="7e386-114">Delete a tenant</span></span>

<span data-ttu-id="7e386-115">Bir Azure aboneliğiniz yoksa [ücretsiz bir hesap oluşturma](https://azure.microsoft.com/free/) başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="7e386-115">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e386-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7e386-116">Prerequisites</span></span>

<span data-ttu-id="7e386-117">toocomplete Bu öğretici, yapma emin olduğunuz:</span><span class="sxs-lookup"><span data-stu-id="7e386-117">toocomplete this tutorial, make sure you have:</span></span>

* <span data-ttu-id="7e386-118">PowerShell ve hello en yeni sürümü yüklü hello [en son Azure PowerShell SDK'sı](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="7e386-118">Installed hello newest version of PowerShell and hello [latest Azure PowerShell SDK](http://azure.microsoft.com/downloads/)</span></span>

* <span data-ttu-id="7e386-119">Yüklü hello en son sürümünü [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="7e386-119">Installed hello latest version of [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span> <span data-ttu-id="7e386-120">SQL Server Management Studio'yu yükleme hello SQLPackage, kullanılan tooautomate veritabanı geliştirme görevleri bir dizi olabilir bir komut satırı yardımcı programı en son sürümünü yükler.</span><span class="sxs-lookup"><span data-stu-id="7e386-120">Installing SQL Server Management Studio also installs hello latest version of SQLPackage, a command-line utility that can be used tooautomate a range of database development tasks.</span></span>

* <span data-ttu-id="7e386-121">Yüklü hello [Java Çalışma zamanı ortamı (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) ve hello [en son JAVA Geliştirme Seti (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) makinenize yüklü.</span><span class="sxs-lookup"><span data-stu-id="7e386-121">Installed hello [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) and hello [latest JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed on your machine.</span></span> 

* <span data-ttu-id="7e386-122">Yüklü [Apache Maven](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="7e386-122">Installed [Apache Maven](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="7e386-123">Maven kullanılacak toohelp bağımlılıkları yönetme, derleme, test ve hello örnek Java projesi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7e386-123">Maven will be used toohelp manage dependencies, build, test and run hello sample Java project</span></span>

## <a name="set-up-data-environment"></a><span data-ttu-id="7e386-124">Veri ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="7e386-124">Set up data environment</span></span>

<span data-ttu-id="7e386-125">Kiracı başına bir veritabanı sağlama.</span><span class="sxs-lookup"><span data-stu-id="7e386-125">You will be provisioning a database per tenant.</span></span> <span data-ttu-id="7e386-126">Merhaba Kiracı başına veritabanı modeli hello yüksek derecede az DevOps maliyeti ile kiracılar arasında yalıtım sağlar.</span><span class="sxs-lookup"><span data-stu-id="7e386-126">hello database-per-tenant model provides hello highest degree of isolation between tenants, with little DevOps cost.</span></span> <span data-ttu-id="7e386-127">toooptimize hello maliyet bulut kaynaklarının, aynı zamanda hello Kiracı veritabanları veritabanları grubu için toooptimize hello fiyat performans sağlayan bir esnek havuz içine sağlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="7e386-127">toooptimize hello cost of cloud resources, you will also be provisioning hello tenant databases into an elastic pool which allows you toooptimize hello price performance for a group of databases.</span></span> <span data-ttu-id="7e386-128">modelleri sağlama diğer veritabanıyla ilgili toolearn [Burada gördüğünüz](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span><span class="sxs-lookup"><span data-stu-id="7e386-128">toolearn about other database provisioning models [see here](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span></span>

<span data-ttu-id="7e386-129">Bu adımları toocreate bir SQL server ve tüm Kiracı veritabanlarını barındıracak bir esnek havuz izleyin.</span><span class="sxs-lookup"><span data-stu-id="7e386-129">Follow these steps toocreate a SQL server and an elastic pool that will host all your tenant databases.</span></span> 

1. <span data-ttu-id="7e386-130">Değişkenleri kullanılacak toostore değerleri hello öğreticinin hello kalan oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7e386-130">Create variables toostore values that will be used in hello rest of hello tutorial.</span></span> <span data-ttu-id="7e386-131">IP adresiniz emin toomodify başlangıç IP adresi değişken tooinclude olun</span><span class="sxs-lookup"><span data-stu-id="7e386-131">Make sure toomodify hello IP address variable tooinclude your IP address</span></span> 
   
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
   
2. <span data-ttu-id="7e386-132">Oturum açma tooAzure ve SQL server ve esnek havuz oluşturma</span><span class="sxs-lookup"><span data-stu-id="7e386-132">Login tooAzure and create a SQL server and elastic pool</span></span> 
   
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
   
## <a name="create-tenant-catalog"></a><span data-ttu-id="7e386-133">Kiracı Katalog Oluştur</span><span class="sxs-lookup"><span data-stu-id="7e386-133">Create tenant catalog</span></span> 

<span data-ttu-id="7e386-134">Çok kiracılı bir SaaS uygulaması bir kiracı için bilgi depolandığı önemli tooknow değil.</span><span class="sxs-lookup"><span data-stu-id="7e386-134">In a multi-tenant SaaS application, it’s important tooknow where information for a tenant is stored.</span></span> <span data-ttu-id="7e386-135">Bu, genellikle bir katalog veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="7e386-135">This is commonly stored in a catalog database.</span></span> <span data-ttu-id="7e386-136">başlangıç kataloğu kullanılan toohold bir kiracı ve bu kiracının veri depolandığı bir veritabanı arasında bir eşleme veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="7e386-136">hello catalog database is used toohold a mapping between a tenant and a database in which that tenant’s data is stored.</span></span>  <span data-ttu-id="7e386-137">tek Kiracı veritabanı kullanılan veya bir çok kiracılı olup olmadığını Hello temel deseni uygular.</span><span class="sxs-lookup"><span data-stu-id="7e386-137">hello basic pattern applies whether a multi-tenant or a single-tenant database is used.</span></span>

<span data-ttu-id="7e386-138">Bu adımları toocreate Merhaba örnek SaaS uygulaması için bir katalog veritabanı izleyin.</span><span class="sxs-lookup"><span data-stu-id="7e386-138">Follow these steps toocreate a catalog database for hello sample SaaS application.</span></span>

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

## <a name="provision-database-for-tenant1-and-register-in-tenant-catalog"></a><span data-ttu-id="7e386-139">Veritabanı için 'tenant1' sağlamak ve Kiracı kataloğunda kaydetme</span><span class="sxs-lookup"><span data-stu-id="7e386-139">Provision database for 'tenant1' and register in tenant catalog</span></span> 
<span data-ttu-id="7e386-140">PowerShell tooprovision bir veritabanı için yeni bir kiracı 'tenant1' kullanın ve bu Kiracı hello kataloğunda kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7e386-140">Use Powershell tooprovision a database for a new tenant 'tenant1' and register this tenant in hello catalog.</span></span> 

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

## <a name="provision-database-for-tenant2-and-register-in-tenant-catalog"></a><span data-ttu-id="7e386-141">Veritabanı için 'tenant2' sağlamak ve Kiracı kataloğunda kaydetme</span><span class="sxs-lookup"><span data-stu-id="7e386-141">Provision database for 'tenant2' and register in tenant catalog</span></span>
<span data-ttu-id="7e386-142">PowerShell tooprovision bir veritabanı için yeni bir kiracı 'tenant2' kullanın ve bu Kiracı hello kataloğunda kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7e386-142">Use Powershell tooprovision a database for a new tenant 'tenant2' and register this tenant in hello catalog.</span></span> 

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

## <a name="set-up-sample-java-application"></a><span data-ttu-id="7e386-143">Örnek Java uygulama ayarlama</span><span class="sxs-lookup"><span data-stu-id="7e386-143">Set up sample Java application</span></span> 

1. <span data-ttu-id="7e386-144">Bir maven projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7e386-144">Create a maven project.</span></span> <span data-ttu-id="7e386-145">Bir komut istemi penceresinde Hello aşağıdakileri yazın:</span><span class="sxs-lookup"><span data-stu-id="7e386-145">Type hello following in a command prompt window:</span></span>
   
   ```
   mvn archetype:generate -DgroupId=com.microsoft.sqlserver -DartifactId=mssql-jdbc -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   
2. <span data-ttu-id="7e386-146">Bu bağımlılık, dil düzeyi ekleyin ve seçeneği toosupport bildirim dosyalarında Kavanoz toohello pom.xml dosyasını oluşturun:</span><span class="sxs-lookup"><span data-stu-id="7e386-146">Add this dependency, language level, and build option toosupport manifest files in jars toohello pom.xml file:</span></span>
   
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

3. <span data-ttu-id="7e386-147">Merhaba App.java dosyasına Hello aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7e386-147">Add hello following into hello App.java file:</span></span>

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

4. <span data-ttu-id="7e386-148">Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7e386-148">Save hello file.</span></span>

5. <span data-ttu-id="7e386-149">Toocommand Konsolu gidin ve yürütme</span><span class="sxs-lookup"><span data-stu-id="7e386-149">Go toocommand console and execute</span></span>

   ```bash
   mvn package
   ```

6. <span data-ttu-id="7e386-150">Tamamlandığında, toorun Merhaba uygulaması aşağıdaki hello yürütme</span><span class="sxs-lookup"><span data-stu-id="7e386-150">When finished, execute hello following toorun hello application</span></span> 
   
   ```
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```
   
<span data-ttu-id="7e386-151">başarıyla tamamlanırsa hello çıktı şuna benzeyecektir:</span><span class="sxs-lookup"><span data-stu-id="7e386-151">hello output will look like this if it runs successfully:</span></span>

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

## <a name="delete-first-tenant"></a><span data-ttu-id="7e386-152">İlk Kiracı Sil</span><span class="sxs-lookup"><span data-stu-id="7e386-152">Delete first tenant</span></span> 
<span data-ttu-id="7e386-153">Veritabanı ve Katalog PowerShell toodelete hello Kiracı girişi hello ilk Kiracı için kullanın.</span><span class="sxs-lookup"><span data-stu-id="7e386-153">Use PowerShell toodelete hello tenant database and catalog entry for hello first tenant.</span></span>

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

<span data-ttu-id="7e386-154">Bağlanmayı deneyin çok 'tenant1' kullanarak izin ver hello Java uygulaması.</span><span class="sxs-lookup"><span data-stu-id="7e386-154">Try connecting too'tenant1' using hello Java application.</span></span> <span data-ttu-id="7e386-155">Merhaba Kiracı yok bildiren bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="7e386-155">You will get an error stating that hello tenant does not exist.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e386-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7e386-156">Next steps</span></span> 

<span data-ttu-id="7e386-157">Bu öğreticide için öğrenilen:</span><span class="sxs-lookup"><span data-stu-id="7e386-157">In this tutorial, you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="7e386-158">Bir veritabanı ortamı toosupport hello Kiracı başına veritabanı modeli kullanarak bir çok kiracılı SaaS uygulaması ayarlayın</span><span class="sxs-lookup"><span data-stu-id="7e386-158">Set up a database environment toosupport a multi-tenant SaaS application, using hello Database-per-tenant pattern</span></span>
> * <span data-ttu-id="7e386-159">Kiracı katalog oluşturma</span><span class="sxs-lookup"><span data-stu-id="7e386-159">Create a tenant catalog</span></span>
> * <span data-ttu-id="7e386-160">Bir kiracı veritabanı sağlamak ve hello Kiracı kataloğunda kaydetme</span><span class="sxs-lookup"><span data-stu-id="7e386-160">Provision a tenant database and register it in hello tenant catalog</span></span>
> * <span data-ttu-id="7e386-161">Bir örnek Java uygulama ayarlama</span><span class="sxs-lookup"><span data-stu-id="7e386-161">Set up a sample Java application</span></span> 
> * <span data-ttu-id="7e386-162">Erişim Kiracı veritabanları basit bir Java konsol uygulaması</span><span class="sxs-lookup"><span data-stu-id="7e386-162">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="7e386-163">Bir kiracı Sil</span><span class="sxs-lookup"><span data-stu-id="7e386-163">Delete a tenant</span></span>

* <span data-ttu-id="7e386-164">Ortak görevler için PowerShell örnekleri görmek [SQL veritabanı PowerShell örnekleri](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span><span class="sxs-lookup"><span data-stu-id="7e386-164">PowerShell samples for common tasks, see [SQL Database PowerShell samples](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span></span>

* <span data-ttu-id="7e386-165">Tasarım desenleri çok kiracılı SaaS uygulamaları bakın [tasarım desenleri](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span><span class="sxs-lookup"><span data-stu-id="7e386-165">Design patterns for multi-tenant SaaS applications see [Design patterns](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span></span>

* <span data-ttu-id="7e386-166">Azure ortak görevler için Java örnekleri görmek [Java Geliştirici Merkezi](https://azure.microsoft.com/develop/java/)</span><span class="sxs-lookup"><span data-stu-id="7e386-166">Java samples for common Azure tasks, see [Java Developer Center](https://azure.microsoft.com/develop/java/)</span></span>



