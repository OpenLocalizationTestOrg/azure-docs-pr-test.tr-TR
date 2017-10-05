---
title: "Azure SQL Data Warehouse için PowerShell cmdlet'leri"
description: "Üst PowerShell cmdlet'leri için Azure SQL veri duraklatma ve sürdürme bir veritabanı da dahil olmak üzere ambarı bulun."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 6f0d5772-f05f-4cc8-9749-4adb153dfd50
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: reference
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: ce3e11587c2e0cb92923868a4f26d7f59c7ef4ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="powershell-cmdlets-and-rest-apis-for-sql-data-warehouse"></a><span data-ttu-id="83640-103">PowerShell cmdlet'leri ve SQL Data Warehouse için REST API'leri</span><span class="sxs-lookup"><span data-stu-id="83640-103">PowerShell cmdlets and REST APIs for SQL Data Warehouse</span></span>
<span data-ttu-id="83640-104">Birçok SQL veri ambarı yönetim görevleri, Azure PowerShell cmdlet'lerini veya REST API'leri kullanılarak yönetilebilir.</span><span class="sxs-lookup"><span data-stu-id="83640-104">Many SQL Data Warehouse administration tasks can be managed using either Azure PowerShell cmdlets or REST APIs.</span></span>  <span data-ttu-id="83640-105">Aşağıda, SQL veri ambarı ortak görevleri otomatikleştirmek için PowerShell komutlarını kullanmak nasıl bazı örnekler verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="83640-105">Below are some examples of how to use PowerShell commands to automate common tasks in your SQL Data Warehouse.</span></span>  <span data-ttu-id="83640-106">Makale iyi bazı diğer örnekler için bkz [ölçeklenebilirlik REST ile yönetme][Manage scalability with REST].</span><span class="sxs-lookup"><span data-stu-id="83640-106">For some good REST examples, see the article [Manage scalability with REST][Manage scalability with REST].</span></span>

> [!NOTE]
> <span data-ttu-id="83640-107">SQL Data Warehouse ile Azure PowerShell kullanmak için Azure PowerShell 1.0.3 sürümü gerekir veya daha büyük.</span><span class="sxs-lookup"><span data-stu-id="83640-107">In order to use Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="83640-108">Çalıştırarak sürümünüzü kontrol edebilirsiniz **Get-Module - listavailable birlikte-Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="83640-108">You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="83640-109">En son sürümünü yüklenebilir [Microsoft Web Platformu yükleyicisi][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="83640-109">The latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="83640-110">En son sürümü yükleme hakkında daha fazla bilgi için bkz. [Azure PowerShell'i yükleme ve yapılandırma][How to install and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="83640-110">For more information on installing the latest version, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span></span>
> 
> 

## <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="83640-111">Azure PowerShell cmdlet'leri kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="83640-111">Get started with Azure PowerShell cmdlets</span></span>
1. <span data-ttu-id="83640-112">Windows PowerShell'i açın.</span><span class="sxs-lookup"><span data-stu-id="83640-112">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="83640-113">PowerShell komut isteminde, Azure Resource Manager için oturum açın ve aboneliğinizi seçmek için şu komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="83640-113">At the PowerShell prompt, run these commands to sign in to the Azure Resource Manager and select your subscription.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

## <a name="pause-sql-data-warehouse-example"></a><span data-ttu-id="83640-114">Duraklatma SQL veri ambarı örneği</span><span class="sxs-lookup"><span data-stu-id="83640-114">Pause SQL Data Warehouse Example</span></span>
<span data-ttu-id="83640-115">"" Server01."adlı bir sunucuda barındırılan Database02" adlı bir veritabanı duraklatma</span><span class="sxs-lookup"><span data-stu-id="83640-115">Pause a database named "Database02" hosted on a server named "Server01."</span></span>  <span data-ttu-id="83640-116">Sunucu "ResourceGroup1." adlı bir Azure kaynak grubunda yer alıyor</span><span class="sxs-lookup"><span data-stu-id="83640-116">The server is in an Azure resource group named "ResourceGroup1."</span></span>

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="83640-117">Bir değişim Bu örnek alınan nesneyi kanallar [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="83640-117">A variation, this example pipes the retrieved object to [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span>  <span data-ttu-id="83640-118">Sonuç olarak, veritabanı duraklatıldı.</span><span class="sxs-lookup"><span data-stu-id="83640-118">As a result, the database is paused.</span></span> <span data-ttu-id="83640-119">Son komutun sonuçlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="83640-119">The final command shows the results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

## <a name="start-sql-data-warehouse-example"></a><span data-ttu-id="83640-120">SQL veri ambarı örneği Başlat</span><span class="sxs-lookup"><span data-stu-id="83640-120">Start SQL Data Warehouse Example</span></span>
<span data-ttu-id="83640-121">"" Server01."adlı bir sunucuda barındırılan Database02" adlı bir veritabanı işlemi sürdürme</span><span class="sxs-lookup"><span data-stu-id="83640-121">Resume operation of a database named "Database02" hosted on a server named "Server01."</span></span> <span data-ttu-id="83640-122">Sunucu "ResourceGroup1." adlı bir kaynak grubunda yer alan</span><span class="sxs-lookup"><span data-stu-id="83640-122">The server is contained in a resource group named "ResourceGroup1."</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="83640-123">Bir değişim Bu örnekte "" ResourceGroup1."adlı bir kaynak grubunda yer alan Server01" adlı bir sunucudan "Database02" adlı bir veritabanı alır.</span><span class="sxs-lookup"><span data-stu-id="83640-123">A variation, this example retrieves a database named "Database02" from a server named "Server01" that is contained in a resource group named "ResourceGroup1."</span></span> <span data-ttu-id="83640-124">Alınan nesnesine kanallar [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="83640-124">It pipes the retrieved object to [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
```

> [!NOTE]
> <span data-ttu-id="83640-125">Sunucunuz foo.database.windows.net, ise "foo" PowerShell cmdlet'leri - ServerName kullanmak unutmayın.</span><span class="sxs-lookup"><span data-stu-id="83640-125">Note that if your server is foo.database.windows.net, use "foo" as the -ServerName in the PowerShell cmdlets.</span></span>
> 
> 

## <a name="other-supported-powershell-cmdlets"></a><span data-ttu-id="83640-126">Diğer desteklenen PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="83640-126">Other supported PowerShell cmdlets</span></span>
<span data-ttu-id="83640-127">Bu PowerShell cmdlet'leri, Azure SQL Data Warehouse ile desteklenir.</span><span class="sxs-lookup"><span data-stu-id="83640-127">These PowerShell cmdlets are supported with Azure SQL Data Warehouse.</span></span>

* <span data-ttu-id="83640-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="83640-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="83640-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span><span class="sxs-lookup"><span data-stu-id="83640-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span></span>
* <span data-ttu-id="83640-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span><span class="sxs-lookup"><span data-stu-id="83640-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span></span>
* <span data-ttu-id="83640-131">[AzureRmSqlDatabase yeni][New-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="83640-131">[New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="83640-132">[Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="83640-132">[Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="83640-133">[Geri yükleme-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="83640-133">[Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="83640-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="83640-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="83640-135">[Select-AzureRmSubscription][Select-AzureRmSubscription]</span><span class="sxs-lookup"><span data-stu-id="83640-135">[Select-AzureRmSubscription][Select-AzureRmSubscription]</span></span>
* <span data-ttu-id="83640-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="83640-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="83640-137">[Askıya alma AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="83640-137">[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span></span>

## <a name="next-steps"></a><span data-ttu-id="83640-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="83640-138">Next steps</span></span>
<span data-ttu-id="83640-139">Daha fazla PowerShell örnekler için bkz:</span><span class="sxs-lookup"><span data-stu-id="83640-139">For more PowerShell examples, see:</span></span>

* <span data-ttu-id="83640-140">[PowerShell kullanarak SQL Data Warehouse oluşturma][Create a SQL Data Warehouse using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="83640-140">[Create a SQL Data Warehouse using PowerShell][Create a SQL Data Warehouse using PowerShell]</span></span>
* <span data-ttu-id="83640-141">[Veritabanı geri yükleme][Database restore]</span><span class="sxs-lookup"><span data-stu-id="83640-141">[Database restore][Database restore]</span></span>

<span data-ttu-id="83640-142">PowerShell ile otomatik olarak diğer görevler için bkz: [Azure SQL veritabanı cmdlet'leri][Azure SQL Database Cmdlets].</span><span class="sxs-lookup"><span data-stu-id="83640-142">For other tasks which can be automated with PowerShell, see [Azure SQL Database Cmdlets][Azure SQL Database Cmdlets].</span></span> <span data-ttu-id="83640-143">Tüm Azure SQL veritabanı cmdlet'leri Azure SQL Data Warehouse için desteklendiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="83640-143">Note that not all Azure SQL Database cmdlets are supported for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="83640-144">Hangi BİLGİSAYARLARLA otomatik görevlerin listesi için bkz: [işlemleri Azure SQL veritabanları için][Operations for Azure SQL Databases].</span><span class="sxs-lookup"><span data-stu-id="83640-144">For a list of tasks which can be automated with REST, see [Operations for Azure SQL Databases][Operations for Azure SQL Databases].</span></span>

<!--Image references-->

<!--Article references-->
[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Create a SQL Data Warehouse using PowerShell]: ./sql-data-warehouse-get-started-provision-powershell.md
[Database restore]: ./sql-data-warehouse-restore-database-powershell.md
[Manage scalability with REST]: ./sql-data-warehouse-manage-compute-rest-api.md

<!--MSDN references-->
[Azure SQL Database Cmdlets]: https://msdn.microsoft.com/library/mt574084.aspx
[Operations for Azure SQL Databases]: https://msdn.microsoft.com/library/azure/dn505719.aspx
[Get-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt603648.aspx
[Get-AzureRmSqlDeletedDatabaseBackup]: https://msdn.microsoft.com/library/mt693387.aspx
[Get-AzureRmSqlDatabaseRestorePoints]: https://msdn.microsoft.com/library/mt603642.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Remove-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619368.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
<!-- It appears that Select-AzureRmSubscription isn't documented, so this points to Select-AzureSubscription -->
[Select-AzureRmSubscription]: https://msdn.microsoft.com/library/dn722499.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
