---
title: "coğrafi olarak dağıtılan Azure SQL veritabanı çözümü aaaImplement | Microsoft Docs"
description: "Azure SQL Database ve uygulama çoğaltılan yük devretme tooa için veritabanı ve yük devretme sınamasını tooconfigure öğrenin."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/26/2017
ms.author: carlrab
ms.openlocfilehash: 9295d33c669405108a1a64ef1e7cb77f582773a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-a-geo-distributed-database"></a><span data-ttu-id="5cc25-103">Coğrafi olarak dağıtılan bir veritabanı uygulaması</span><span class="sxs-lookup"><span data-stu-id="5cc25-103">Implement a geo-distributed database</span></span>

<span data-ttu-id="5cc25-104">Bu öğreticide bir Azure SQL veritabanı ve yük devretme tooa uzak bölge için uygulamayı yapılandırma ve yük devretme planınız sınayın.</span><span class="sxs-lookup"><span data-stu-id="5cc25-104">In this tutorial, you configure an Azure SQL database and application for failover tooa remote region, and then test your failover plan.</span></span> <span data-ttu-id="5cc25-105">Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5cc25-105">You learn how to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="5cc25-106">Veritabanı kullanıcıları oluşturun ve bunları izinleri</span><span class="sxs-lookup"><span data-stu-id="5cc25-106">Create database users and grant them permissions</span></span>
> * <span data-ttu-id="5cc25-107">Bir veritabanı düzeyinde güvenlik duvarı kuralı ayarlamak</span><span class="sxs-lookup"><span data-stu-id="5cc25-107">Set up a database-level firewall rule</span></span>
> * <span data-ttu-id="5cc25-108">Oluşturma bir [coğrafi çoğaltma yük devretme grubu](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="5cc25-108">Create a [geo-replication failover group](sql-database-geo-replication-overview.md)</span></span>
> * <span data-ttu-id="5cc25-109">Oluşturun ve Java uygulama tooquery bir Azure SQL veritabanı derleme</span><span class="sxs-lookup"><span data-stu-id="5cc25-109">Create and compile a Java application tooquery an Azure SQL database</span></span>
> * <span data-ttu-id="5cc25-110">Bir olağanüstü durum kurtarma ayrıntıya gerçekleştirin</span><span class="sxs-lookup"><span data-stu-id="5cc25-110">Perform a disaster recovery drill</span></span>

<span data-ttu-id="5cc25-111">Bir Azure aboneliğiniz yoksa [ücretsiz bir hesap oluşturma](https://azure.microsoft.com/free/) başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="5cc25-111">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="5cc25-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5cc25-112">Prerequisites</span></span>

<span data-ttu-id="5cc25-113">Bu öğretici, Önkoşullar aşağıdaki yapma emin hello tamamlanır toocomplete:</span><span class="sxs-lookup"><span data-stu-id="5cc25-113">toocomplete this tutorial, make sure hello following prerequisites are completed:</span></span>

- <span data-ttu-id="5cc25-114">Son yüklenen hello [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="5cc25-114">Installed hello latest [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs).</span></span> 
- <span data-ttu-id="5cc25-115">Bir Azure SQL veritabanını yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="5cc25-115">Installed an Azure SQL database.</span></span> <span data-ttu-id="5cc25-116">Bu öğretici bir adı ile Merhaba AdventureWorksLT örnek veritabanı kullanır **mySampleDatabase** Bu hızlı başlangıçlar birinden:</span><span class="sxs-lookup"><span data-stu-id="5cc25-116">This tutorial uses hello AdventureWorksLT sample database with a name of **mySampleDatabase** from one of these quick starts:</span></span>

   - [<span data-ttu-id="5cc25-117">DB Oluşturma - Portal</span><span class="sxs-lookup"><span data-stu-id="5cc25-117">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="5cc25-118">DB oluşturma - CLI</span><span class="sxs-lookup"><span data-stu-id="5cc25-118">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="5cc25-119">DB Oluşturma - PowerShell</span><span class="sxs-lookup"><span data-stu-id="5cc25-119">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="5cc25-120">Yöntem tooexecute SQL tanımladınız betikleri veritabanınızı karşı kullanabileceğiniz sorgu araçları aşağıdaki hello biri:</span><span class="sxs-lookup"><span data-stu-id="5cc25-120">Have identified a method tooexecute SQL scripts against your database, you can use one of hello following query tools:</span></span>
   - <span data-ttu-id="5cc25-121">Merhaba sorgu Düzenleyicisi'nde hello [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5cc25-121">hello query editor in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="5cc25-122">Hello Azure portal hello sorgu Düzenleyicisi'ni kullanarak daha fazla bilgi için bkz: [bağlanma ve sorgu Düzenleyicisi'ni kullanarak sorgu](sql-database-get-started-portal.md#query-the-sql-database).</span><span class="sxs-lookup"><span data-stu-id="5cc25-122">For more information on using hello query editor in hello Azure portal, see [Connect and query using Query Editor](sql-database-get-started-portal.md#query-the-sql-database).</span></span>
   - <span data-ttu-id="5cc25-123">Merhaba en yeni sürümünü [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), SQL Server tooSQL veritabanı Microsoft Windows için herhangi bir SQL altyapı yönetme için tümleşik bir ortam olduğu.</span><span class="sxs-lookup"><span data-stu-id="5cc25-123">hello newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), which is an integrated environment for managing any SQL infrastructure, from SQL Server tooSQL Database for Microsoft Windows.</span></span>
   - <span data-ttu-id="5cc25-124">Merhaba en yeni sürümünü [Visual Studio Code](https://code.visualstudio.com/docs), Linux, macOS, için bir grafik kod düzenleyicisini olduğu ve uzantılar da dahil olmak üzere destekleyen bir Windows hello [mssql uzantısı](https://aka.ms/mssql-marketplace) Microsoft SQL Server sorgulamak için , Azure SQL Database ve SQL veri ambarı.</span><span class="sxs-lookup"><span data-stu-id="5cc25-124">hello newest version of [Visual Studio Code](https://code.visualstudio.com/docs), which is a graphical code editor for Linux, macOS, and Windows that supports extensions, including hello [mssql extension](https://aka.ms/mssql-marketplace) for querying Microsoft SQL Server, Azure SQL Database, and SQL Data Warehouse.</span></span> <span data-ttu-id="5cc25-125">Bu aracı kullanarak Azure SQL veritabanı ile ilgili daha fazla bilgi için bkz: [Connect ve VS Code sorguyla](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="5cc25-125">For more information on using this tool with Azure SQL Database, see [Connect and query with VS Code](sql-database-connect-query-vscode.md).</span></span> 

## <a name="create-database-users-and-grant-permissions"></a><span data-ttu-id="5cc25-126">Veritabanı kullanıcıları oluşturun ve izinleri</span><span class="sxs-lookup"><span data-stu-id="5cc25-126">Create database users and grant permissions</span></span>

<span data-ttu-id="5cc25-127">Tooyour veritabanına bağlanmak ve sorgu araçları aşağıdaki hello birini kullanarak kullanıcı hesapları oluşturun:</span><span class="sxs-lookup"><span data-stu-id="5cc25-127">Connect tooyour database and create user accounts using one of hello following query tools:</span></span>

- <span data-ttu-id="5cc25-128">Merhaba sorgu Düzenleyicisi'nde hello Azure portalı</span><span class="sxs-lookup"><span data-stu-id="5cc25-128">hello Query editor in hello Azure portal</span></span>
- <span data-ttu-id="5cc25-129">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="5cc25-129">SQL Server Management Studio</span></span>
- <span data-ttu-id="5cc25-130">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5cc25-130">Visual Studio Code</span></span>

<span data-ttu-id="5cc25-131">Bu kullanıcı hesaplarını tooyour ikincil sunucu otomatik olarak çoğaltabilir (ve eşitleme tutulması).</span><span class="sxs-lookup"><span data-stu-id="5cc25-131">These user accounts replicate automatically tooyour secondary server (and be kept in sync).</span></span> <span data-ttu-id="5cc25-132">kendisi için henüz bir güvenlik duvarı yapılandırdığınız olmayan bir IP adresinde bir istemciden bağlanıyorsanız toouse SQL Server Management Studio veya Visual Studio Code, tooconfigure bir güvenlik duvarı kuralı gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="5cc25-132">toouse SQL Server Management Studio or Visual Studio Code, you may need tooconfigure a firewall rule if you are connecting from a client at an IP address for which you have not yet configured a firewall.</span></span> <span data-ttu-id="5cc25-133">Ayrıntılı adımlar için bkz: [sunucu düzeyinde güvenlik duvarı kuralı oluşturma](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="5cc25-133">For detailed steps, see [Create a server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>

- <span data-ttu-id="5cc25-134">Sorgu penceresinde, sorgu toocreate iki kullanıcı hesapları, veritabanınızdaki aşağıdaki hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="5cc25-134">In a query window, execute hello following query toocreate two user accounts in your database.</span></span> <span data-ttu-id="5cc25-135">Bu komut dosyası verir **db_owner** izinleri toohello **app_admin** hesabı ve verir **seçin** ve **güncelleştirme** izinleri toohello **app_user** hesabı.</span><span class="sxs-lookup"><span data-stu-id="5cc25-135">This script grants **db_owner** permissions toohello **app_admin** account and grants **SELECT** and **UPDATE** permissions toohello **app_user** account.</span></span> 

   ```sql
   CREATE USER app_admin WITH PASSWORD = 'ChangeYourPassword1';
   --Add SQL user toodb_owner role
   ALTER ROLE db_owner ADD MEMBER app_admin; 
   --Create additional SQL user
   CREATE USER app_user WITH PASSWORD = 'ChangeYourPassword1';
   --grant permission tooSalesLT schema
   GRANT SELECT, INSERT, DELETE, UPDATE ON SalesLT.Product tooapp_user;
   ```

## <a name="create-database-level-firewall"></a><span data-ttu-id="5cc25-136">Veritabanı düzeyinde güvenlik duvarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5cc25-136">Create database-level firewall</span></span>

<span data-ttu-id="5cc25-137">Oluşturma bir [veritabanı düzeyinde güvenlik duvarı kuralı](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) SQL veritabanınız için.</span><span class="sxs-lookup"><span data-stu-id="5cc25-137">Create a [database-level firewall rule](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) for your SQL database.</span></span> <span data-ttu-id="5cc25-138">Bu veritabanı düzeyinde güvenlik duvarı kuralı, bu öğreticide oluşturduğunuz toohello ikincil sunucu otomatik olarak çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="5cc25-138">This database-level firewall rule replicates automatically toohello secondary server that you create in this tutorial.</span></span> <span data-ttu-id="5cc25-139">(Bu öğreticide) kolaylık sağlamak için Bu öğreticide hello adımları gerçekleştiriyorsanız hello bilgisayarın hello ortak IP adresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="5cc25-139">For simplicity (in this tutorial), use hello public IP address of hello computer on which you are performing hello steps in this tutorial.</span></span> <span data-ttu-id="5cc25-140">hello sunucu düzeyinde güvenlik duvarı kuralı geçerli bilgisayarınız için kullanılan toodetermine hello IP adresini bakın [sunucu düzeyinde güvenlik duvarı oluşturma](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="5cc25-140">toodetermine hello IP address used for hello server-level firewall rule for your current computer, see [Create a server-level firewall](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>  

- <span data-ttu-id="5cc25-141">Açık sorgu penceresinde hello önceki sorgu aşağıdaki sorgu, ortamınız için uygun IP adreslerini hello hello IP adreslerini değiştirerek hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5cc25-141">In your open query window, replace hello previous query with hello following query, replacing hello IP addresses with hello appropriate IP addresses for your environment.</span></span>  

   ```sql
   -- Create database-level firewall setting for your public IP address
   EXECUTE sp_set_database_firewall_rule @name = N'myGeoReplicationFirewallRule',@start_ip_address = '0.0.0.0', @end_ip_address = '0.0.0.0';
   ```

## <a name="create-an-active-geo-replication-auto-failover-group"></a><span data-ttu-id="5cc25-142">Aktif coğrafi çoğaltma otomatik yük devretme grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="5cc25-142">Create an active geo-replication auto failover group</span></span> 

<span data-ttu-id="5cc25-143">Azure PowerShell kullanarak oluşturduğunuz bir [aktif coğrafi çoğaltma otomatik yük devretme grubu](sql-database-geo-replication-overview.md) mevcut Azure SQL server ve hello yeni arasında boş bir Azure bölgesi de Azure SQL server ve örnek veritabanı toohello yük devretme grubunuza ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5cc25-143">Using Azure PowerShell, create an [active geo-replication auto failover group](sql-database-geo-replication-overview.md) between your existing Azure SQL server and hello new empty Azure SQL server in an Azure region, and then add your sample database toohello failover group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5cc25-144">Bu cmdlet'ler Azure PowerShell 4.0 gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5cc25-144">These cmdlets require Azure PowerShell 4.0.</span></span> [!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install-no-ssh.md)]
>

1. <span data-ttu-id="5cc25-145">Var olan sunucu ve örnek veritabanı için başlangıç değerlerini kullanarak, bir PowerShell komut dosyası değişkenleri doldurun ve yük devretme grup adı için bir genel benzersiz değer belirtin.</span><span class="sxs-lookup"><span data-stu-id="5cc25-145">Populate variables for your PowerShell scripts using hello values for your existing server and sample database, and provide a globally unique value for failover group name.</span></span>

   ```powershell
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   $myresourcegroupname = "<your resource group name>"
   $mylocation = "<your resource group location>"
   $myservername = "<your existing server name>"
   $mydatabasename = "mySampleDatabase"
   $mydrlocation = "<your disaster recovery location>"
   $mydrservername = "<your disaster recovery server name>"
   $myfailovergroupname = "<your unique failover group name>"
   ```

2. <span data-ttu-id="5cc25-146">Boş bir yedek sunucu yük devretme bölgenizde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5cc25-146">Create an empty backup server in your failover region.</span></span>

   ```powershell
   $mydrserver = New-AzureRmSqlServer -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername `
      -Location $mydrlocation `
      -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   $mydrserver   
   ```

3. <span data-ttu-id="5cc25-147">Merhaba iki sunucu arasında bir yük devretme grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5cc25-147">Create a failover group between hello two servers.</span></span>

   ```powershell
   $myfailovergroup = New-AzureRMSqlDatabaseFailoverGroup `
      –ResourceGroupName $myresourcegroupname `
      -ServerName $myservername `
      -PartnerServerName $mydrservername  `
      –FailoverGroupName $myfailovergroupname `
      –FailoverPolicy Automatic `
      -GracePeriodWithDataLossHours 2
   $myfailovergroup   
   ```

4. <span data-ttu-id="5cc25-148">Veritabanı toohello yük devretme grubunuza ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5cc25-148">Add your database toohello failover group.</span></span>

   ```powershell
   $myfailovergroup = Get-AzureRmSqlDatabase `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $myservername `
      -DatabaseName $mydatabasename | `
    Add-AzureRmSqlDatabaseToFailoverGroup `
      -ResourceGroupName $myresourcegroupname ` `
      -ServerName $myservername `
      -FailoverGroupName $myfailovergroupname
   $myfailovergroup   
   ```

## <a name="install-java-software"></a><span data-ttu-id="5cc25-149">Java yazılımı yükleme</span><span class="sxs-lookup"><span data-stu-id="5cc25-149">Install Java software</span></span>

<span data-ttu-id="5cc25-150">Bu bölümdeki Hello adımları Java kullanarak geliştirme ile bilgi sahibiyseniz ve Azure SQL Database ile yeni tooworking olan varsayalım.</span><span class="sxs-lookup"><span data-stu-id="5cc25-150">hello steps in this section assume that you are familiar with developing using Java and are new tooworking with Azure SQL Database.</span></span> 

### <a name="mac-os"></a><span data-ttu-id="5cc25-151">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="5cc25-151">**Mac OS**</span></span>
<span data-ttu-id="5cc25-152">Terminalinizde açın ve burada Java projenize oluşturmayı planladığınızla tooa dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="5cc25-152">Open your terminal and navigate tooa directory where you plan on creating your Java project.</span></span> <span data-ttu-id="5cc25-153">Yükleme **brew** ve **Maven** hello aşağıdaki komutları girerek:</span><span class="sxs-lookup"><span data-stu-id="5cc25-153">Install **brew** and **Maven** by entering hello following commands:</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install maven
```

<span data-ttu-id="5cc25-154">Yükleme ve Java ve Maven ortam yapılandırma konusunda ayrıntılı yönergeler için hello Git [SQL Server'ı kullanarak bir uygulama oluşturmak](https://www.microsoft.com/sql-server/developer-get-started/)seçin **Java**seçin **MacOS**ve ardından izleyin Merhaba, Java ve Maven 1.2 ve 1.3 adımda yapılandırma yönergeleri ayrıntılı.</span><span class="sxs-lookup"><span data-stu-id="5cc25-154">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **MacOS**, and then follow hello detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="5cc25-155">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="5cc25-155">**Linux (Ubuntu)**</span></span>
<span data-ttu-id="5cc25-156">Terminalinizde açın ve burada Java projenize oluşturmayı planladığınızla tooa dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="5cc25-156">Open your terminal and navigate tooa directory where you plan on creating your Java project.</span></span> <span data-ttu-id="5cc25-157">Yükleme **Maven** hello aşağıdaki komutları girerek:</span><span class="sxs-lookup"><span data-stu-id="5cc25-157">Install **Maven** by entering hello following commands:</span></span>

```bash
sudo apt-get install maven
```

<span data-ttu-id="5cc25-158">Yükleme ve Java ve Maven ortam yapılandırma konusunda ayrıntılı yönergeler için hello Git [SQL Server'ı kullanarak bir uygulama oluşturmak](https://www.microsoft.com/sql-server/developer-get-started/)seçin **Java**seçin **Ubuntu**ve ardından izleyin Merhaba, Java ve Maven 1.2, 1,3 ve 1.4 adımda yapılandırma yönergeleri ayrıntılı.</span><span class="sxs-lookup"><span data-stu-id="5cc25-158">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **Ubuntu**, and then follow hello detailed instructions for configuring Java and Maven in step 1.2, 1.3, and 1.4.</span></span>

### <a name="windows"></a><span data-ttu-id="5cc25-159">**Windows**</span><span class="sxs-lookup"><span data-stu-id="5cc25-159">**Windows**</span></span>
<span data-ttu-id="5cc25-160">Yükleme [Maven](https://maven.apache.org/download.cgi) hello resmi Yükleyicisi'ni kullanarak.</span><span class="sxs-lookup"><span data-stu-id="5cc25-160">Install [Maven](https://maven.apache.org/download.cgi) using hello official installer.</span></span> <span data-ttu-id="5cc25-161">Toohelp bağımlılıklarını yönetme, derleme, test ve Java projenizi çalıştırma Maven kullanın.</span><span class="sxs-lookup"><span data-stu-id="5cc25-161">Use Maven toohelp manage dependencies, build, test, and run your Java project.</span></span> <span data-ttu-id="5cc25-162">Yükleme ve Java ve Maven ortam yapılandırma konusunda ayrıntılı yönergeler için hello Git [SQL Server'ı kullanarak bir uygulama oluşturmak](https://www.microsoft.com/sql-server/developer-get-started/)seçin **Java**Windows seçin ve ardından izleyin hello ayrıntılı yönergeler için Java ve Maven 1.2 ve 1.3 adımda yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="5cc25-162">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select Windows, and then follow hello detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

## <a name="create-sqldbsample-project"></a><span data-ttu-id="5cc25-163">SqlDbSample projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="5cc25-163">Create SqlDbSample project</span></span>

1. <span data-ttu-id="5cc25-164">Merhaba komut konsolunda (örneğin, Bash) bir Maven projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5cc25-164">In hello command console (such as Bash), create a Maven project.</span></span> 
   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=SqlDbSample" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```
2. <span data-ttu-id="5cc25-165">Tür **Y** tıklatıp **Enter**.</span><span class="sxs-lookup"><span data-stu-id="5cc25-165">Type **Y** and click **Enter**.</span></span>
3. <span data-ttu-id="5cc25-166">Yeni oluşturulan projenize dizinleri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5cc25-166">Change directories into your newly created project.</span></span>

   ```bash
   cd SqlDbSamples
   ```

4. <span data-ttu-id="5cc25-167">Tercih ettiğiniz düzenleyicisi kullanarak proje klasörünüzdeki hello pom.xml dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="5cc25-167">Using your favorite editor, open hello pom.xml file in your project folder.</span></span> 

5. <span data-ttu-id="5cc25-168">Sık kullandığınız metin Düzenleyicisi'ni açarak Hello Microsoft JDBC sürücüsü için SQL Server bağımlılık tooyour Maven projesine ekleyin ve kopyalama ve yapıştırma pom.xml dosyanıza satırlardan hello.</span><span class="sxs-lookup"><span data-stu-id="5cc25-168">Add hello Microsoft JDBC Driver for SQL Server dependency tooyour Maven project by opening your favorite text editor and copying and pasting hello following lines into your pom.xml file.</span></span> <span data-ttu-id="5cc25-169">Merhaba dosyasında önceden doldurulmaz hello var olan değerlerin üzerine yazmaz.</span><span class="sxs-lookup"><span data-stu-id="5cc25-169">Do not overwrite hello existing values prepopulated in hello file.</span></span> <span data-ttu-id="5cc25-170">Merhaba JDBC bağımlılık yapıştırılmasına gerekir hello büyük "bağımlılıkları" bölümüne () içinde.</span><span class="sxs-lookup"><span data-stu-id="5cc25-170">hello JDBC dependency must be pasted within hello larger “dependencies” section ( ).</span></span>   

   ```xml
   <dependency>
     <groupId>com.microsoft.sqlserver</groupId>
     <artifactId>mssql-jdbc</artifactId>
    <version>6.1.0.jre8</version>
   </dependency>
   ```

6. <span data-ttu-id="5cc25-171">"Özellikler" bölümüne hello pom.xml dosyasına hello "bağımlılıkları" bölümünden sonra aşağıdaki hello ekleyerek Java toocompile hello proje karşı Hello sürümünü belirtin.</span><span class="sxs-lookup"><span data-stu-id="5cc25-171">Specify hello version of Java toocompile hello project against by adding hello following “properties” section into hello pom.xml file after hello "dependencies" section.</span></span> 

   ```xml
   <properties>
     <maven.compiler.source>1.8</maven.compiler.source>
     <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```
7. <span data-ttu-id="5cc25-172">Merhaba aşağıdaki "bölümü hello pom.xml dosyasına hello"Özellikler"bölümüne toosupport bildirim dosyalarından Kavanoz sonra yapı" ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5cc25-172">Add hello following "build" section into hello pom.xml file after hello "properties" section toosupport manifest files in jars.</span></span>       

   ```xml
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
8. <span data-ttu-id="5cc25-173">Merhaba pom.xml dosyasını kaydedip kapatın.</span><span class="sxs-lookup"><span data-stu-id="5cc25-173">Save and close hello pom.xml file.</span></span>
9. <span data-ttu-id="5cc25-174">Merhaba App.java dosyasını (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) açın ve hello içeriği içeriği aşağıdaki hello ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5cc25-174">Open hello App.java file (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) and replace hello contents with hello following contents.</span></span> <span data-ttu-id="5cc25-175">Merhaba yük devretme grubu adı, yük devretme grubunuz için hello adla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5cc25-175">Replace hello failover group name with hello name for your failover group.</span></span> <span data-ttu-id="5cc25-176">Merhaba veritabanı adı, kullanıcı veya parola hello değerleri değiştirdiyseniz, bu değerleri de değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5cc25-176">If you have changed hello values for hello database name, user, or password, change those values as well.</span></span>

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.Timestamp;
   import java.sql.DriverManager;
   import java.util.Date;
   import java.util.concurrent.TimeUnit;

   public class App {

      private static final String FAILOVER_GROUP_NAME = "myfailovergroupname";
  
      private static final String DB_NAME = "mySampleDatabase";
      private static final String USER = "app_user";
      private static final String PASSWORD = "ChangeYourPassword1";

      private static final String READ_WRITE_URL = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", FAILOVER_GROUP_NAME, DB_NAME, USER, PASSWORD);
      private static final String READ_ONLY_URL = String.format("jdbc:sqlserver://%s.secondary.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", FAILOVER_GROUP_NAME, DB_NAME, USER, PASSWORD);

      public static void main(String[] args) {
         System.out.println("#######################################");
         System.out.println("## GEO DISTRIBUTED DATABASE TUTORIAL ##");
         System.out.println("#######################################");
         System.out.println(""); 

         int highWaterMark = getHighWaterMarkId();

         try {
            for(int i = 1; i < 1000; i++) {
                //  loop will run for about 1 hour
                System.out.print(i + ": insert on primary " + (insertData((highWaterMark + i))?"successful":"failed"));
                TimeUnit.SECONDS.sleep(1);
                System.out.print(", read from secondary " + (selectData((highWaterMark + i))?"successful":"failed") + "\n");
                TimeUnit.SECONDS.sleep(3);
            }
         } catch(Exception e) {
            e.printStackTrace();
      }
   }

   private static boolean insertData(int id) {
      // Insert data into hello product table with a unique product name that we can use toofind hello product again later
      String sql = "INSERT INTO SalesLT.Product (Name, ProductNumber, Color, StandardCost, ListPrice, SellStartDate) VALUES (?,?,?,?,?,?);";

      try (Connection connection = DriverManager.getConnection(READ_WRITE_URL); 
              PreparedStatement pstmt = connection.prepareStatement(sql)) {
         pstmt.setString(1, "BrandNewProduct" + id);
         pstmt.setInt(2, 200989 + id + 10000);
         pstmt.setString(3, "Blue");
         pstmt.setDouble(4, 75.00);
         pstmt.setDouble(5, 89.99);
         pstmt.setTimestamp(6, new Timestamp(new Date().getTime()));
         return (1 == pstmt.executeUpdate());
      } catch (Exception e) {
         return false;
      }
   }

   private static boolean selectData(int id) {
      // Query hello data that was previously inserted into hello primary database from hello geo replicated database
      String sql = "SELECT Name, Color, ListPrice FROM SalesLT.Product WHERE Name = ?";

      try (Connection connection = DriverManager.getConnection(READ_ONLY_URL); 
              PreparedStatement pstmt = connection.prepareStatement(sql)) {
         pstmt.setString(1, "BrandNewProduct" + id);
         try (ResultSet resultSet = pstmt.executeQuery()) {
            return resultSet.next();
         }
      } catch (Exception e) {
         return false;
      }
   }

   private static int getHighWaterMarkId() {
      // Query hello high water mark id that is stored in hello table toobe able toomake unique inserts 
      String sql = "SELECT MAX(ProductId) FROM SalesLT.Product";
      int result = 1;
        
      try (Connection connection = DriverManager.getConnection(READ_WRITE_URL); 
              Statement stmt = connection.createStatement();
              ResultSet resultSet = stmt.executeQuery(sql)) {
         if (resultSet.next()) {
             result =  resultSet.getInt(1);
            }
         } catch (Exception e) {
          e.printStackTrace();
         }
         return result;
      }
   }
   ```
6. <span data-ttu-id="5cc25-177">Merhaba App.java dosyasını kaydedip kapatın.</span><span class="sxs-lookup"><span data-stu-id="5cc25-177">Save and close hello App.java file.</span></span>

## <a name="compile-and-run-hello-sqldbsample-project"></a><span data-ttu-id="5cc25-178">Derleme ve hello SqlDbSample projesi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5cc25-178">Compile and run hello SqlDbSample project</span></span>

1. <span data-ttu-id="5cc25-179">Merhaba komut konsolunda toofollowing komutunu yürütün.</span><span class="sxs-lookup"><span data-stu-id="5cc25-179">In hello command console, execute toofollowing command.</span></span>

   ```bash
   mvn package
   ```
2. <span data-ttu-id="5cc25-180">Tamamlandığında, komut toorun Merhaba uygulaması (el ile durdurun sürece, yaklaşık 1 saat boyunca çalışır) aşağıdaki hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="5cc25-180">When finished, execute hello following command toorun hello application (it runs for about 1 hour unless you stop it manually):</span></span>

   ```bash
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   
   #######################################
   ## GEO DISTRIBUTED DATABASE TUTORIAL ##
   #######################################

   1. insert on primary successful, read from secondary successful
   2. insert on primary successful, read from secondary successful
   3. insert on primary successful, read from secondary successful
   ```

## <a name="perform-disaster-recovery-drill"></a><span data-ttu-id="5cc25-181">Olağanüstü durum kurtarma ayrıntıya gerçekleştirin</span><span class="sxs-lookup"><span data-stu-id="5cc25-181">Perform disaster recovery drill</span></span>

1. <span data-ttu-id="5cc25-182">Yük devretme grubu el ile yük devretme çağırın.</span><span class="sxs-lookup"><span data-stu-id="5cc25-182">Call manual failover of failover group.</span></span> 

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $mydrservername `
   -FailoverGroupName $myfailovergroupname
   ```

2. <span data-ttu-id="5cc25-183">Merhaba, yük devretme sırasında uygulama sonuçları gözlemlemek.</span><span class="sxs-lookup"><span data-stu-id="5cc25-183">Observe hello application results during failover.</span></span> <span data-ttu-id="5cc25-184">Merhaba DNS önbelleği yeniler karşın bazı eklemeleri başarısız.</span><span class="sxs-lookup"><span data-stu-id="5cc25-184">Some inserts fail while hello DNS cache refreshes.</span></span>     

3. <span data-ttu-id="5cc25-185">Olağanüstü durum kurtarma sunucunuzun performansının hangi rolünün ölçeğini bulun.</span><span class="sxs-lookup"><span data-stu-id="5cc25-185">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $mydrserver.ReplicationRole
   ```

4. <span data-ttu-id="5cc25-186">Yeniden çalışma.</span><span class="sxs-lookup"><span data-stu-id="5cc25-186">Failback.</span></span>

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $myservername `
   -FailoverGroupName $myfailovergroupname
   ```

5. <span data-ttu-id="5cc25-187">Merhaba, yeniden çalışma sırasında uygulama sonuçları gözlemlemek.</span><span class="sxs-lookup"><span data-stu-id="5cc25-187">Observe hello application results during failback.</span></span> <span data-ttu-id="5cc25-188">Merhaba DNS önbelleği yeniler karşın bazı eklemeleri başarısız.</span><span class="sxs-lookup"><span data-stu-id="5cc25-188">Some inserts fail while hello DNS cache refreshes.</span></span>     

6. <span data-ttu-id="5cc25-189">Olağanüstü durum kurtarma sunucunuzun performansının hangi rolünün ölçeğini bulun.</span><span class="sxs-lookup"><span data-stu-id="5cc25-189">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $fileovergroup = Get-AzureRMSqlDatabaseFailoverGroup `
      -FailoverGroupName $myfailovergroupname `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername
   $fileovergroup.ReplicationRole
   ```
## <a name="next-steps"></a><span data-ttu-id="5cc25-190">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5cc25-190">Next steps</span></span> 

<span data-ttu-id="5cc25-191">Daha fazla bilgi için bkz: [etkin coğrafi çoğaltma ve yük devretme gruplar](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5cc25-191">For more information, see [Active geo-replication and failover groups](sql-database-geo-replication-overview.md).</span></span>
