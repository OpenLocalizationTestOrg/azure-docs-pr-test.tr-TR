---
title: "Azure PowerShell: SQL veritabanı oluşturma | Microsoft Docs"
description: "Azure portal toocreate SQL Database mantıksal sunucusu, sunucu düzeyinde güvenlik duvarı kuralı ve veritabanlarında nasıl hello öğrenin."
keywords: "sql veritabanı öğreticisi, sql veritabanı oluşturma"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: PowerShell
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: e89f68b44083a3b64e61f95117dbbedfa6647ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-powershell"></a><span data-ttu-id="0f44d-104">PowerShell kullanarak tek Azure SQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0f44d-104">Create a single Azure SQL database using PowerShell</span></span>

<span data-ttu-id="0f44d-105">PowerShell kullanılan toocreate olan ve hello komut satırından veya komut dosyalarında Azure kaynaklarını yönetin.</span><span class="sxs-lookup"><span data-stu-id="0f44d-105">PowerShell is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="0f44d-106">Bir Azure SQL veritabanında bu kılavuzu kullanarak PowerShell toodeploy ayrıntılarını bir [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md) içinde bir [Azure SQL Database mantıksal sunucusu](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="0f44d-106">This guide details using PowerShell toodeploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="0f44d-107">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz](https://azure.microsoft.com/free/) bir hesap oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0f44d-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

<span data-ttu-id="0f44d-108">Bu öğretici hello Azure PowerShell modülü sürüm 4.0 veya üstünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0f44d-108">This tutorial requires hello Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="0f44d-109">Çalıştırma ` Get-Module -ListAvailable AzureRM` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="0f44d-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="0f44d-110">Tooinstall veya yükseltme gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="0f44d-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

## <a name="log-in-tooazure"></a><span data-ttu-id="0f44d-111">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="0f44d-111">Log in tooAzure</span></span>

<span data-ttu-id="0f44d-112">İçinde tooyour Azure aboneliği hello kullanarak oturum [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) komut ve hello ekrandaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="0f44d-112">Log in tooyour Azure subscription using hello [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command and follow hello on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-variables"></a><span data-ttu-id="0f44d-113">Değişken oluşturma</span><span class="sxs-lookup"><span data-stu-id="0f44d-113">Create variables</span></span>

<span data-ttu-id="0f44d-114">Bu hızlı başlangıç hello komut içinde kullanmak için değişkenleri tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="0f44d-114">Define variables for use in hello scripts in this quick start.</span></span>

```powershell
# hello data center and resource name for your resources
$resourcegroupname = "myResourceGroup"
$location = "WestEurope"
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
$servername = "server-$(Get-Random)"
# Set an admin login and password for your database
# hello login information for hello server
$adminlogin = "ServerAdmin"
$password = "ChangeYourAdminPassword1"
# hello ip address range that you want tooallow tooaccess your server - change as appropriate
$startip = "0.0.0.0"
$endip = "0.0.0.0"
# hello database name
$databasename = "mySampleDatabase"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="0f44d-115">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="0f44d-115">Create a resource group</span></span>

<span data-ttu-id="0f44d-116">Oluşturma bir [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md) hello kullanarak [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) komutu.</span><span class="sxs-lookup"><span data-stu-id="0f44d-116">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="0f44d-117">Kaynak grubu, Azure kaynaklarının grup olarak dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="0f44d-117">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="0f44d-118">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `westeurope` konumu.</span><span class="sxs-lookup"><span data-stu-id="0f44d-118">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location.</span></span>

```powershell
New-AzureRmResourceGroup -Name $resourcegroupname -Location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="0f44d-119">Mantıksal sunucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="0f44d-119">Create a logical server</span></span>

<span data-ttu-id="0f44d-120">Oluşturma bir [Azure SQL Database mantıksal sunucusu](sql-database-features.md) hello kullanarak [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) komutu.</span><span class="sxs-lookup"><span data-stu-id="0f44d-120">Create an [Azure SQL Database logical server](sql-database-features.md) using hello [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) command.</span></span> <span data-ttu-id="0f44d-121">Mantıksal sunucu, grup olarak yönetilen bir veritabanı grubu içerir.</span><span class="sxs-lookup"><span data-stu-id="0f44d-121">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="0f44d-122">Merhaba aşağıdaki örnek rastgele adlandırılmış bir sunucu, kaynak grubunda adlı bir yönetici oturum açma ile oluşturur `ServerAdmin` ve bir parola `ChangeYourAdminPassword1`.</span><span class="sxs-lookup"><span data-stu-id="0f44d-122">hello following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="0f44d-123">Bu önceden tanımlı değerleri istediğiniz gibi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0f44d-123">Replace these pre-defined values as desired.</span></span>

```powershell
New-AzureRmSqlServer -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -Location $location `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="0f44d-124">Sunucu güvenlik duvarı kurallarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0f44d-124">Configure a server firewall rule</span></span>

<span data-ttu-id="0f44d-125">Oluşturma bir [Azure SQL veritabanı sunucu düzeyinde güvenlik duvarı kuralı](sql-database-firewall-configure.md) hello kullanarak [yeni AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) komutu.</span><span class="sxs-lookup"><span data-stu-id="0f44d-125">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using hello [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) command.</span></span> <span data-ttu-id="0f44d-126">Sunucu düzeyinde güvenlik duvarı kuralı SQL Server Management Studio veya hello SQLCMD yardımcı programını tooconnect tooa SQL veritabanı gibi hello SQL Database hizmeti güvenlik duvarı üzerinden bir dış uygulamaya verir.</span><span class="sxs-lookup"><span data-stu-id="0f44d-126">A server-level firewall rule allows an external application, such as SQL Server Management Studio or hello SQLCMD utility tooconnect tooa SQL database through hello SQL Database service firewall.</span></span> <span data-ttu-id="0f44d-127">Aşağıdaki örneğine hello hello Güvenlik Duvarı'nı yalnızca diğer Azure kaynakları için açıldı.</span><span class="sxs-lookup"><span data-stu-id="0f44d-127">In hello following example, hello firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="0f44d-128">tooenable harici bağlantı, başlangıç IP adresi tooan uygun adresini Değiştir ortamınız için.</span><span class="sxs-lookup"><span data-stu-id="0f44d-128">tooenable external connectivity, change hello IP address tooan appropriate address for your environment.</span></span> <span data-ttu-id="0f44d-129">tooopen tüm IP adresleri hello bitiş adresi başlangıç IP adresi ve 255.255.255.255 hello olarak 0.0.0.0 kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f44d-129">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress $startip -EndIpAddress $endip
```

> [!NOTE]
> <span data-ttu-id="0f44d-130">SQL Veritabanı 1433 numaralı bağlantı noktası üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="0f44d-130">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="0f44d-131">Bir şirket ağından gelen tooconnect çalışıyorsanız, bağlantı noktası 1433 üzerinden giden trafik, ağınızın güvenlik duvarı tarafından izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="0f44d-131">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="0f44d-132">Öyleyse, BT departmanınızın 1433 numaralı bağlantı noktasını açar sürece mümkün tooconnect tooyour Azure SQL veritabanı sunucusu olmaz.</span><span class="sxs-lookup"><span data-stu-id="0f44d-132">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a><span data-ttu-id="0f44d-133">Merhaba sunucu örnek verilerle bir veritabanı oluşturun</span><span class="sxs-lookup"><span data-stu-id="0f44d-133">Create a database in hello server with sample data</span></span>

<span data-ttu-id="0f44d-134">Bir veritabanı oluşturmak bir [S0 performans düzeyi](sql-database-service-tiers.md) hello kullanarak hello Server'daki [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) komutu.</span><span class="sxs-lookup"><span data-stu-id="0f44d-134">Create a database with an [S0 performance level](sql-database-service-tiers.md) in hello server using hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) command.</span></span> <span data-ttu-id="0f44d-135">Merhaba aşağıdaki örnek adlı bir veritabanı oluşturur `mySampleDatabase` ve bu veritabanına yükleri hello AdventureWorksLT örnek verileri.</span><span class="sxs-lookup"><span data-stu-id="0f44d-135">hello following example creates a database called `mySampleDatabase` and loads hello AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="0f44d-136">Bu önceden tanımlanmış Değiştir istendiği gibi (Bu koleksiyonu yapıda Bu hızlı başlangıç hello değerleri bağlı diğer hızlı başlar) değerleri.</span><span class="sxs-lookup"><span data-stu-id="0f44d-136">Replace these predefined values as desired (other quick starts in this collection build upon hello values in this quick start).</span></span>

```powershell
New-AzureRmSqlDatabase  -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -DatabaseName $databasename `
    -SampleName "AdventureWorksLT" `
    -RequestedServiceObjectiveName "S0"
```

## <a name="clean-up-resources"></a><span data-ttu-id="0f44d-137">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="0f44d-137">Clean up resources</span></span>

<span data-ttu-id="0f44d-138">Bu koleksiyondaki diğer hızlı başlangıçlar, bu hızlı başlangıca göre belirlenir.</span><span class="sxs-lookup"><span data-stu-id="0f44d-138">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="0f44d-139">Sonraki hızlı başlangıçlar ile toowork üzerinde toocontinue planlıyorsanız, temiz oluşturulan bu hızlı başlangıç kaynakları başlatılmaz.</span><span class="sxs-lookup"><span data-stu-id="0f44d-139">If you plan toocontinue on toowork with subsequent quick starts, do not clean up hello resources created in this quick start.</span></span> <span data-ttu-id="0f44d-140">Toocontinue düşünmüyorsanız bu hızlı başlangıç bölümünde hello Azure portal tarafından oluşturulan tüm kaynakları adımları toodelete aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f44d-140">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quick start in hello Azure portal.</span></span>
>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="0f44d-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0f44d-141">Next steps</span></span>

<span data-ttu-id="0f44d-142">Artık bir veritabanınız olduğuna göre, sık kullandığınız araçlarla bağlanabilir ve sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f44d-142">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="0f44d-143">Aşağıdan aracınızı seçerek daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="0f44d-143">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="0f44d-144">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="0f44d-144">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="0f44d-145">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="0f44d-145">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="0f44d-146">.NET</span><span class="sxs-lookup"><span data-stu-id="0f44d-146">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="0f44d-147">PHP</span><span class="sxs-lookup"><span data-stu-id="0f44d-147">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="0f44d-148">Node.js</span><span class="sxs-lookup"><span data-stu-id="0f44d-148">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="0f44d-149">Java</span><span class="sxs-lookup"><span data-stu-id="0f44d-149">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="0f44d-150">Python</span><span class="sxs-lookup"><span data-stu-id="0f44d-150">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="0f44d-151">Ruby</span><span class="sxs-lookup"><span data-stu-id="0f44d-151">Ruby</span></span>](sql-database-connect-query-ruby.md)

