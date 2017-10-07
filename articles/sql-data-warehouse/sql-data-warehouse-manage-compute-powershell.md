---
title: "aaaManage işlem güç Azure SQL Data warehouse'da (PowerShell) | Microsoft Docs"
description: "PowerShell görevleri toomanage güç işlem. Dwu ayarlayarak işlem kaynaklarını ölçeklendirme. Veya, duraklatma ve sürdürme kaynakları toosave maliyetlerini işlem."
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
ms.openlocfilehash: 8b379d4cf89570649767f6896d2c630d4f1111d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="aaed5-105">Azure SQL Data warehouse'da (PowerShell) işlem güç yönetimi</span><span class="sxs-lookup"><span data-stu-id="aaed5-105">Manage compute power in Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aaed5-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="aaed5-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="aaed5-107">Portal</span><span class="sxs-lookup"><span data-stu-id="aaed5-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="aaed5-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aaed5-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="aaed5-109">REST</span><span class="sxs-lookup"><span data-stu-id="aaed5-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="aaed5-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="aaed5-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

## <a name="before-you-begin"></a><span data-ttu-id="aaed5-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="aaed5-111">Before you begin</span></span>
### <a name="install-hello-latest-version-of-azure-powershell"></a><span data-ttu-id="aaed5-112">Hello Azure PowerShell'in en son sürümünü yükleyin</span><span class="sxs-lookup"><span data-stu-id="aaed5-112">Install hello latest version of Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="aaed5-113">toouse Azure PowerShell ile SQL Data Warehouse, ihtiyacınız Azure PowerShell 1.0.3 sürümü veya daha büyük.</span><span class="sxs-lookup"><span data-stu-id="aaed5-113">toouse Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="aaed5-114">tooverify geçerli sürümünüzü hello komutu çalıştırın **Get-Module - listavailable birlikte-Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="aaed5-114">tooverify your current version run hello command **Get-Module -ListAvailable -Name Azure**.</span></span> <span data-ttu-id="aaed5-115">Merhaba en son sürümü yükleyebilirsiniz [Microsoft Web Platformu yükleyicisi][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="aaed5-115">You can install hello latest version from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="aaed5-116">Daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="aaed5-116">For more information, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>
>
> 

### <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="aaed5-117">Azure PowerShell cmdlet'leri kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="aaed5-117">Get started with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="aaed5-118">tooget başlatıldı:</span><span class="sxs-lookup"><span data-stu-id="aaed5-118">tooget started:</span></span>

1. <span data-ttu-id="aaed5-119">Azure PowerShell'i açın.</span><span class="sxs-lookup"><span data-stu-id="aaed5-119">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="aaed5-120">PowerShell komut isteminde hello bu komutları toosign toohello Azure Kaynak Yöneticisi'ni çalıştırın ve aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="aaed5-120">At hello PowerShell prompt, run these commands toosign in toohello Azure Resource Manager and select your subscription.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="aaed5-121">Ölçek işlem gücü</span><span class="sxs-lookup"><span data-stu-id="aaed5-121">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="aaed5-122">toochange hello Dwu, hello kullan [Set-AzureRmSqlDatabase] [ Set-AzureRmSqlDatabase] PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="aaed5-122">toochange hello DWUs, use hello [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase] PowerShell cmdlet.</span></span> <span data-ttu-id="aaed5-123">Merhaba aşağıdaki örnek hello hizmet düzeyi hedefi tooDW1000 hello veritabanı barındırılan MySQLDW MyServer sunucusuna ayarlar.</span><span class="sxs-lookup"><span data-stu-id="aaed5-123">hello following example sets hello service level objective tooDW1000 for hello database MySQLDW which is hosted on server MyServer.</span></span>

```Powershell
Set-AzureRmSqlDatabase -DatabaseName "MySQLDW" -ServerName "MyServer" -RequestedServiceObjectiveName "DW1000"
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="aaed5-124">Duraklatma işlem</span><span class="sxs-lookup"><span data-stu-id="aaed5-124">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="aaed5-125">toopause bir veritabanını kullanın hello [Suspend-AzureRmSqlDatabase] [ Suspend-AzureRmSqlDatabase] cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="aaed5-125">toopause a database, use hello [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="aaed5-126">Merhaba aşağıdaki örnek Server01 adlı bir sunucuda barındırılan Database02 adlı bir veritabanı duraklatır.</span><span class="sxs-lookup"><span data-stu-id="aaed5-126">hello following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="aaed5-127">Merhaba sunucu bir Azure kaynak grubu ResourceGroup1 olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="aaed5-127">hello server is in an Azure resource group named ResourceGroup1.</span></span>

> [!NOTE]
> <span data-ttu-id="aaed5-128">Sunucunuz foo.database.windows.net, ise "foo" Merhaba PowerShell cmdlet'leri - ServerName hello olarak kullanmak unutmayın.</span><span class="sxs-lookup"><span data-stu-id="aaed5-128">Note that if your server is foo.database.windows.net, use "foo" as hello -ServerName in hello PowerShell cmdlets.</span></span>
>
> 

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="aaed5-129">Bir değişim bu sonraki örnek hello veritabanı hello $database nesnesine alır.</span><span class="sxs-lookup"><span data-stu-id="aaed5-129">A variation, this next example retrieves hello database into hello $database object.</span></span> <span data-ttu-id="aaed5-130">Bunun ardından hello nesne çok kanallar[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="aaed5-130">It then pipes hello object too[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span> <span data-ttu-id="aaed5-131">Merhaba sonuçları hello nesne resultDatabase içinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="aaed5-131">hello results are stored in hello object resultDatabase.</span></span> <span data-ttu-id="aaed5-132">Merhaba son komut hello sonuçları gösterir.</span><span class="sxs-lookup"><span data-stu-id="aaed5-132">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="aaed5-133">Resume işlem</span><span class="sxs-lookup"><span data-stu-id="aaed5-133">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="aaed5-134">toostart bir veritabanını kullanın hello [Resume-AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="aaed5-134">toostart a database, use hello [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="aaed5-135">Merhaba aşağıdaki örnek Server01 adlı bir sunucuda barındırılan Database02 adlı bir veritabanı başlatır.</span><span class="sxs-lookup"><span data-stu-id="aaed5-135">hello following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="aaed5-136">Merhaba sunucu bir Azure kaynak grubu ResourceGroup1 olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="aaed5-136">hello server is in an Azure resource group named ResourceGroup1.</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="aaed5-137">Bir değişim bu sonraki örnek hello veritabanı hello $database nesnesine alır.</span><span class="sxs-lookup"><span data-stu-id="aaed5-137">A variation, this next example retrieves hello database into hello $database object.</span></span> <span data-ttu-id="aaed5-138">Bunun ardından hello nesne çok kanallar[Resume-AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] ve hello sonuçları $resultDatabase içinde depolar.</span><span class="sxs-lookup"><span data-stu-id="aaed5-138">It then pipes hello object too[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] and stores hello results in $resultDatabase.</span></span> <span data-ttu-id="aaed5-139">Merhaba son komut hello sonuçları gösterir.</span><span class="sxs-lookup"><span data-stu-id="aaed5-139">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
$resultDatabase
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="aaed5-140">Veritabanı durumunu kontrol edin</span><span class="sxs-lookup"><span data-stu-id="aaed5-140">Check database state</span></span>

<span data-ttu-id="aaed5-141">Merhaba örnekleri yukarıda gösterildiği gibi kullanabilirsiniz [Get-AzureRmSqlDatabase] [ Get-AzureRmSqlDatabase] cmdlet tooget bilgi böylece hello durum, aynı zamanda bir bağımsız değişken olarak toouse denetimi, bir veritabanı.</span><span class="sxs-lookup"><span data-stu-id="aaed5-141">As shown in hello above examples, one can use [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase] cmdlet tooget information on a database, thereby checking hello status, but also toouse as an argument.</span></span> 

```powershell
Get-AzureRmSqlDatabase [-ResourceGroupName] <String> [-ServerName] <String> [[-DatabaseName] <String>]
 [-InformationAction <ActionPreference>] [-InformationVariable <String>] [-Confirm] [-WhatIf]
 [<CommonParameters>]
```

<span data-ttu-id="aaed5-142">Hangi bir şey sonucunda ister</span><span class="sxs-lookup"><span data-stu-id="aaed5-142">Which will result in something like</span></span> 

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

<span data-ttu-id="aaed5-143">Burada sonra kontrol edebilirsiniz toosee hello *durum* hello veritabanı.</span><span class="sxs-lookup"><span data-stu-id="aaed5-143">Where you can then check toosee hello *Status* of hello database.</span></span> <span data-ttu-id="aaed5-144">Bu durumda, bu veritabanının çevrimiçi olduğunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aaed5-144">In this case, you can see that this database is online.</span></span> 

<span data-ttu-id="aaed5-145">Bu komutu çalıştırdığınızda, durum değeri ya da çevrimiçi, duraklatma, devam ettirmek, ölçeklendirme ve duraklatıldı almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="aaed5-145">When you run this command, you should receive a Status value of either Online, Pausing, Resuming, Scaling, and Paused.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="aaed5-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aaed5-146">Next steps</span></span>
<span data-ttu-id="aaed5-147">Diğer yönetim görevleri için bkz: [yönetimine genel bakış][Management overview].</span><span class="sxs-lookup"><span data-stu-id="aaed5-147">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Get-AzureRmSqlDatabase]: /powershell/servicemanagement/azure.sqldatabase/v1.6.1/get-azuresqldatabase

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[Azure portal]: http://portal.azure.com/
