---
title: "Azure PowerShell: SQL veritabanı oluşturma | Microsoft Docs"
description: "Azure portalında SQL Veritabanı mantıksal sunucusu, sunucu düzeyi güvenlik duvarı kuralı ve veritabanı oluşturmayı öğrenin."
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
ms.openlocfilehash: 44ed4a603977617c898315c4fc0b2d3dd3a8f16a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-single-azure-sql-database-using-powershell"></a><span data-ttu-id="b6b92-104">PowerShell kullanarak tek Azure SQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b6b92-104">Create a single Azure SQL database using PowerShell</span></span>

<span data-ttu-id="b6b92-105">PowerShell komut satırından veya betik içindeki Azure kaynaklarını oluşturmak ve yönetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b6b92-105">PowerShell is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="b6b92-106">Bu kılavuzda bir [Azure SQL Veritabanı mantıksal sunucusundaki](sql-database-features.md) [Azure kaynak grubuna](../azure-resource-manager/resource-group-overview.md) Azure SQL veritabanı dağıtmak için PowerShell kullanma işlemi ayrıntılı olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b6b92-106">This guide details using PowerShell to deploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="b6b92-107">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz](https://azure.microsoft.com/free/) bir hesap oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b6b92-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

<span data-ttu-id="b6b92-108">Bu öğretici için Azure PowerShell modülünün 4.0 veya daha sonraki bir sürümü gerekir.</span><span class="sxs-lookup"><span data-stu-id="b6b92-108">This tutorial requires the Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="b6b92-109">Sürümü bulmak için ` Get-Module -ListAvailable AzureRM` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b6b92-109">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="b6b92-110">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure PowerShell Modülü yükleme](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="b6b92-110">If you need to install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

## <a name="log-in-to-azure"></a><span data-ttu-id="b6b92-111">Azure'da oturum açma</span><span class="sxs-lookup"><span data-stu-id="b6b92-111">Log in to Azure</span></span>

<span data-ttu-id="b6b92-112">[Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) komutunu kullanarak Azure aboneliğinizde oturum açın ve ekrandaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="b6b92-112">Log in to your Azure subscription using the [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command and follow the on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-variables"></a><span data-ttu-id="b6b92-113">Değişken oluşturma</span><span class="sxs-lookup"><span data-stu-id="b6b92-113">Create variables</span></span>

<span data-ttu-id="b6b92-114">Bu hızlı başlangıçtaki betiklerde kullanılacak değişkenleri tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="b6b92-114">Define variables for use in the scripts in this quick start.</span></span>

```powershell
# The data center and resource name for your resources
$resourcegroupname = "myResourceGroup"
$location = "WestEurope"
# The logical server name: Use a random value or replace with your own value (do not capitalize)
$servername = "server-$(Get-Random)"
# Set an admin login and password for your database
# The login information for the server
$adminlogin = "ServerAdmin"
$password = "ChangeYourAdminPassword1"
# The ip address range that you want to allow to access your server - change as appropriate
$startip = "0.0.0.0"
$endip = "0.0.0.0"
# The database name
$databasename = "mySampleDatabase"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="b6b92-115">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="b6b92-115">Create a resource group</span></span>

<span data-ttu-id="b6b92-116">[New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) komutunu kullanarak yeni bir [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b6b92-116">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="b6b92-117">Kaynak grubu, Azure kaynaklarının grup olarak dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="b6b92-117">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="b6b92-118">Aşağıdaki örnek `westeurope` konumunda `myResourceGroup` adlı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b6b92-118">The following example creates a resource group named `myResourceGroup` in the `westeurope` location.</span></span>

```powershell
New-AzureRmResourceGroup -Name $resourcegroupname -Location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="b6b92-119">Mantıksal sunucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="b6b92-119">Create a logical server</span></span>

<span data-ttu-id="b6b92-120">[New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) komutunu kullanarak bir [Azure SQL Veritabanı mantıksal sunucusu](sql-database-features.md) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b6b92-120">Create an [Azure SQL Database logical server](sql-database-features.md) using the [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) command.</span></span> <span data-ttu-id="b6b92-121">Mantıksal sunucu, grup olarak yönetilen bir veritabanı grubu içerir.</span><span class="sxs-lookup"><span data-stu-id="b6b92-121">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="b6b92-122">Aşağıdaki örnek, kaynak grubunuzda `ServerAdmin` yönetici oturum açma bilgileri ve `ChangeYourAdminPassword1` parolası ile rastgele olarak adlandırılmış bir sunucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b6b92-122">The following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="b6b92-123">Bu önceden tanımlı değerleri istediğiniz gibi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b6b92-123">Replace these pre-defined values as desired.</span></span>

```powershell
New-AzureRmSqlServer -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -Location $location `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="b6b92-124">Sunucu güvenlik duvarı kurallarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b6b92-124">Configure a server firewall rule</span></span>

<span data-ttu-id="b6b92-125">[New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) komutunu kullanarak bir [Azure SQL Veritabanı sunucu düzeyi güvenlik duvarı kuralı](sql-database-firewall-configure.md) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b6b92-125">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using the [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) command.</span></span> <span data-ttu-id="b6b92-126">Bir sunucu düzeyi güvenlik duvarı kuralı SQL Server Management Studio veya SQLCMD yardımcı programı gibi bir dış uygulamanın SQL Veritabanı hizmet güvenlik duvarı üzerinden bir SQL veritabanına bağlanmasına olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="b6b92-126">A server-level firewall rule allows an external application, such as SQL Server Management Studio or the SQLCMD utility to connect to a SQL database through the SQL Database service firewall.</span></span> <span data-ttu-id="b6b92-127">Aşağıdaki örnekte, güvenlik duvarı yalnızca diğer Azure kaynakları için açılır.</span><span class="sxs-lookup"><span data-stu-id="b6b92-127">In the following example, the firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="b6b92-128">Dışarıdan bağlantı kurulabilmesi için IP adresini ortamınız için uygun bir adres olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b6b92-128">To enable external connectivity, change the IP address to an appropriate address for your environment.</span></span> <span data-ttu-id="b6b92-129">Tüm IP adreslerini açmak için başlangıç IP adresi olarak 0.0.0.0’ı, bitiş adresi olaraksa 255.255.255.255’i kullanın.</span><span class="sxs-lookup"><span data-stu-id="b6b92-129">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress $startip -EndIpAddress $endip
```

> [!NOTE]
> <span data-ttu-id="b6b92-130">SQL Veritabanı 1433 numaralı bağlantı noktası üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="b6b92-130">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="b6b92-131">Bir kurumsal ağ içerisinden bağlanmaya çalışıyorsanız, ağınızın güvenlik duvarı tarafından 1433 numaralı bağlantı noktası üzerinden giden trafiğe izin verilmiyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="b6b92-131">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="b6b92-132">Bu durumda, BT departmanınız 1433 numaralı bağlantı noktasını açmadığı sürece Azure SQL veritabanı sunucusuna bağlanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="b6b92-132">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-the-server-with-sample-data"></a><span data-ttu-id="b6b92-133">Sunucuda örnek verilerle veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b6b92-133">Create a database in the server with sample data</span></span>

<span data-ttu-id="b6b92-134">[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) komutunu kullanarak sunucuda [S0 performans düzeyine](sql-database-service-tiers.md) sahip bir veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b6b92-134">Create a database with an [S0 performance level](sql-database-service-tiers.md) in the server using the [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) command.</span></span> <span data-ttu-id="b6b92-135">Aşağıdaki örnek, `mySampleDatabase` adlı bir veritabanı oluşturur ve AdventureWorksLT örnek verilerini bu veritabanına yükler.</span><span class="sxs-lookup"><span data-stu-id="b6b92-135">The following example creates a database called `mySampleDatabase` and loads the AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="b6b92-136">Önceden tanımlanmış bu değerleri istediğiniz gibi değiştirin (bu koleksiyondaki diğer hızlı başlangıçlar, bu hızlı başlangıçtaki değerlere göre belirlenir).</span><span class="sxs-lookup"><span data-stu-id="b6b92-136">Replace these predefined values as desired (other quick starts in this collection build upon the values in this quick start).</span></span>

```powershell
New-AzureRmSqlDatabase  -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -DatabaseName $databasename `
    -SampleName "AdventureWorksLT" `
    -RequestedServiceObjectiveName "S0"
```

## <a name="clean-up-resources"></a><span data-ttu-id="b6b92-137">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="b6b92-137">Clean up resources</span></span>

<span data-ttu-id="b6b92-138">Bu koleksiyondaki diğer hızlı başlangıçlar, bu hızlı başlangıca göre belirlenir.</span><span class="sxs-lookup"><span data-stu-id="b6b92-138">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="b6b92-139">Sonraki hızlı başlangıçlarla çalışmaya devam etmeyi planlıyorsanız, bu hızlı başlangıçta oluşturulan kaynakları temizlemeyin.</span><span class="sxs-lookup"><span data-stu-id="b6b92-139">If you plan to continue on to work with subsequent quick starts, do not clean up the resources created in this quick start.</span></span> <span data-ttu-id="b6b92-140">Devam etmeyi planlamıyorsanız, Azure portalda bu hızlı başlangıç ile oluşturulan tüm kaynakları silmek için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="b6b92-140">If you do not plan to continue, use the following steps to delete all resources created by this quick start in the Azure portal.</span></span>
>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="b6b92-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b6b92-141">Next steps</span></span>

<span data-ttu-id="b6b92-142">Artık bir veritabanınız olduğuna göre, sık kullandığınız araçlarla bağlanabilir ve sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6b92-142">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="b6b92-143">Aşağıdan aracınızı seçerek daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="b6b92-143">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="b6b92-144">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="b6b92-144">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="b6b92-145">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="b6b92-145">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="b6b92-146">.NET</span><span class="sxs-lookup"><span data-stu-id="b6b92-146">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="b6b92-147">PHP</span><span class="sxs-lookup"><span data-stu-id="b6b92-147">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="b6b92-148">Node.js</span><span class="sxs-lookup"><span data-stu-id="b6b92-148">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="b6b92-149">Java</span><span class="sxs-lookup"><span data-stu-id="b6b92-149">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="b6b92-150">Python</span><span class="sxs-lookup"><span data-stu-id="b6b92-150">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="b6b92-151">Ruby</span><span class="sxs-lookup"><span data-stu-id="b6b92-151">Ruby</span></span>](sql-database-connect-query-ruby.md)

