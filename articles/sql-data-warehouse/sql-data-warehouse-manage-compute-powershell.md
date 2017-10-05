---
title: "Azure SQL Data warehouse'da (PowerShell) işlem güç yönetimi | Microsoft Docs"
description: "İşlem gücüne yönetmek için PowerShell görevleri. Dwu ayarlayarak işlem kaynaklarını ölçeklendirme. Veya, duraklatma ve sürdürme işlem kaynaklarını maliyet tasarrufu sağlamak."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 8354a3c1-4e04-4809-933f-db414a8c74dc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 6a185d96447c2e1b0b463439dd062081e783da5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="94747-105">Azure SQL Data warehouse'da (PowerShell) işlem güç yönetimi</span><span class="sxs-lookup"><span data-stu-id="94747-105">Manage compute power in Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="94747-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="94747-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="94747-107">Portal</span><span class="sxs-lookup"><span data-stu-id="94747-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="94747-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="94747-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="94747-109">REST</span><span class="sxs-lookup"><span data-stu-id="94747-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="94747-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="94747-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

## <a name="before-you-begin"></a><span data-ttu-id="94747-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="94747-111">Before you begin</span></span>
### <a name="install-the-latest-version-of-azure-powershell"></a><span data-ttu-id="94747-112">Azure PowerShell'in en son sürümünü yükleyin</span><span class="sxs-lookup"><span data-stu-id="94747-112">Install the latest version of Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="94747-113">SQL Data Warehouse ile Azure PowerShell kullanmak için Azure PowerShell 1.0.3 sürümü gerekir veya daha büyük.</span><span class="sxs-lookup"><span data-stu-id="94747-113">To use Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="94747-114">Komutu çalıştırın geçerli sürümünüzü doğrulamak için **Get-Module - listavailable birlikte-Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="94747-114">To verify your current version run the command **Get-Module -ListAvailable -Name Azure**.</span></span> <span data-ttu-id="94747-115">En son sürümü yükleyebilirsiniz [Microsoft Web Platformu yükleyicisi][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="94747-115">You can install the latest version from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="94747-116">Daha fazla bilgi için bkz: [Azure PowerShell'i yükleme ve yapılandırma nasıl][How to install and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="94747-116">For more information, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span></span>
>
> 

### <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="94747-117">Azure PowerShell cmdlet'leri kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="94747-117">Get started with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="94747-118">Başlamak için:</span><span class="sxs-lookup"><span data-stu-id="94747-118">To get started:</span></span>

1. <span data-ttu-id="94747-119">Azure PowerShell'i açın.</span><span class="sxs-lookup"><span data-stu-id="94747-119">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="94747-120">PowerShell komut isteminde, Azure Resource Manager için oturum açın ve aboneliğinizi seçmek için şu komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="94747-120">At the PowerShell prompt, run these commands to sign in to the Azure Resource Manager and select your subscription.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="94747-121">Ölçek işlem gücü</span><span class="sxs-lookup"><span data-stu-id="94747-121">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="94747-122">Dwu değiştirmek için kullanın [Set-AzureRmSqlDatabase] [ Set-AzureRmSqlDatabase] PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="94747-122">To change the DWUs, use the [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase] PowerShell cmdlet.</span></span> <span data-ttu-id="94747-123">Aşağıdaki örnek, MyServer sunucusunda barındırılan MySQLDW veritabanı için DW1000 için hizmet düzeyi hedefi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="94747-123">The following example sets the service level objective to DW1000 for the database MySQLDW which is hosted on server MyServer.</span></span>

```Powershell
Set-AzureRmSqlDatabase -DatabaseName "MySQLDW" -ServerName "MyServer" -RequestedServiceObjectiveName "DW1000"
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="94747-124">Duraklatma işlem</span><span class="sxs-lookup"><span data-stu-id="94747-124">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="94747-125">Bir veritabanı duraklatmak için kullanmak [Suspend-AzureRmSqlDatabase] [ Suspend-AzureRmSqlDatabase] cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="94747-125">To pause a database, use the [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="94747-126">Aşağıdaki örnek Server01 adlı bir sunucuda barındırılan Database02 adlı bir veritabanı duraklatır.</span><span class="sxs-lookup"><span data-stu-id="94747-126">The following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="94747-127">Sunucu ResourceGroup1 adlı bir Azure kaynak grubunda yer alıyor.</span><span class="sxs-lookup"><span data-stu-id="94747-127">The server is in an Azure resource group named ResourceGroup1.</span></span>

> [!NOTE]
> <span data-ttu-id="94747-128">Sunucunuz foo.database.windows.net, ise "foo" PowerShell cmdlet'leri - ServerName kullanmak unutmayın.</span><span class="sxs-lookup"><span data-stu-id="94747-128">Note that if your server is foo.database.windows.net, use "foo" as the -ServerName in the PowerShell cmdlets.</span></span>
>
> 

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="94747-129">Bir değişim bu sonraki örnek veritabanı $database nesnesine alır.</span><span class="sxs-lookup"><span data-stu-id="94747-129">A variation, this next example retrieves the database into the $database object.</span></span> <span data-ttu-id="94747-130">Sonra nesneyi kanallar [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="94747-130">It then pipes the object to [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span> <span data-ttu-id="94747-131">Sonuçlar nesne resultDatabase içinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="94747-131">The results are stored in the object resultDatabase.</span></span> <span data-ttu-id="94747-132">Son komutun sonuçlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="94747-132">The final command shows the results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="94747-133">Resume işlem</span><span class="sxs-lookup"><span data-stu-id="94747-133">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="94747-134">Bir veritabanı başlatmak için kullanmak [Resume-AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="94747-134">To start a database, use the [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="94747-135">Aşağıdaki örnek Server01 adlı bir sunucuda barındırılan Database02 adlı bir veritabanı başlatır.</span><span class="sxs-lookup"><span data-stu-id="94747-135">The following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="94747-136">Sunucu ResourceGroup1 adlı bir Azure kaynak grubunda yer alıyor.</span><span class="sxs-lookup"><span data-stu-id="94747-136">The server is in an Azure resource group named ResourceGroup1.</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="94747-137">Bir değişim bu sonraki örnek veritabanı $database nesnesine alır.</span><span class="sxs-lookup"><span data-stu-id="94747-137">A variation, this next example retrieves the database into the $database object.</span></span> <span data-ttu-id="94747-138">Sonra nesneyi kanallar [Resume-AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] ve sonuçları $resultDatabase içinde depolar.</span><span class="sxs-lookup"><span data-stu-id="94747-138">It then pipes the object to [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] and stores the results in $resultDatabase.</span></span> <span data-ttu-id="94747-139">Son komutun sonuçlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="94747-139">The final command shows the results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
$resultDatabase
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="94747-140">Veritabanı durumunu kontrol edin</span><span class="sxs-lookup"><span data-stu-id="94747-140">Check database state</span></span>

<span data-ttu-id="94747-141">Yukarıdaki örneklerde gösterildiği gibi kullanabilirsiniz [Get-AzureRmSqlDatabase] [ Get-AzureRmSqlDatabase] cmdlet böylece durumunu denetleme, bir veritabanı hakkında bilgi almak için aynı zamanda bir bağımsız değişken olarak kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="94747-141">As shown in the above examples, one can use [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase] cmdlet to get information on a database, thereby checking the status, but also to use as an argument.</span></span> 

```powershell
Get-AzureRmSqlDatabase [-ResourceGroupName] <String> [-ServerName] <String> [[-DatabaseName] <String>]
 [-InformationAction <ActionPreference>] [-InformationVariable <String>] [-Confirm] [-WhatIf]
 [<CommonParameters>]
```

<span data-ttu-id="94747-142">Hangi bir şey sonucunda ister</span><span class="sxs-lookup"><span data-stu-id="94747-142">Which will result in something like</span></span> 

```powershell   
ResourceGroupName             : nytrg
ServerName                    : nytsvr
DatabaseName                  : nytdb
Location                      : West US
DatabaseId                    : 86461aae-8e3d-4ded-9389-ac9d4bc69bbb
Edition                       : DataWarehouse
CollationName                 : SQL_Latin1General_CP1CI_AS
CatalogCollation              :
MaxSizeBytes                  : 32212254720
Status                        : Online
CreationDate                  : 10/26/2016 4:33:14 PM
CurrentServiceObjectiveId     : 620323bf-2879-4807-b30d-c2e6d7b3b3aa
CurrentServiceObjectiveName   : System2
RequestedServiceObjectiveId   : 620323bf-2879-4807-b30d-c2e6d7b3b3aa
RequestedServiceObjectiveName :
ElasticPoolName               :
EarliestRestoreDate           : 1/1/0001 12:00:00 AM
```

<span data-ttu-id="94747-143">Burada sonra kontrol edebilirsiniz görmek için *durum* veritabanı.</span><span class="sxs-lookup"><span data-stu-id="94747-143">Where you can then check to see the *Status* of the database.</span></span> <span data-ttu-id="94747-144">Bu durumda, bu veritabanının çevrimiçi olduğunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94747-144">In this case, you can see that this database is online.</span></span> 

<span data-ttu-id="94747-145">Bu komutu çalıştırdığınızda, durum değeri ya da çevrimiçi, duraklatma, devam ettirmek, ölçeklendirme ve duraklatıldı almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="94747-145">When you run this command, you should receive a Status value of either Online, Pausing, Resuming, Scaling, and Paused.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="94747-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="94747-146">Next steps</span></span>
<span data-ttu-id="94747-147">Diğer yönetim görevleri için bkz: [yönetimine genel bakış][Management overview].</span><span class="sxs-lookup"><span data-stu-id="94747-147">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Get-AzureRmSqlDatabase]: /powershell/servicemanagement/azure.sqldatabase/v1.6.1/get-azuresqldatabase

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[Azure portal]: http://portal.azure.com/
