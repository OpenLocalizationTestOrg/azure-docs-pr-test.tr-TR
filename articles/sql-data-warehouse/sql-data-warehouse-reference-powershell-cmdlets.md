---
title: "Azure SQL Data Warehouse için aaaPowerShell cmdlet'leri"
description: "Azure SQL Data Warehouse için Hello üst PowerShell cmdlet'leri Bul nasıl dahil toopause ve bir veritabanı sürdürülemedi."
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
ms.openlocfilehash: 84353b56131cf856e0724d338d7ed186fd2ceeaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-cmdlets-and-rest-apis-for-sql-data-warehouse"></a><span data-ttu-id="e3a14-103">PowerShell cmdlet'leri ve SQL Data Warehouse için REST API'leri</span><span class="sxs-lookup"><span data-stu-id="e3a14-103">PowerShell cmdlets and REST APIs for SQL Data Warehouse</span></span>
<span data-ttu-id="e3a14-104">Birçok SQL veri ambarı yönetim görevleri, Azure PowerShell cmdlet'lerini veya REST API'leri kullanılarak yönetilebilir.</span><span class="sxs-lookup"><span data-stu-id="e3a14-104">Many SQL Data Warehouse administration tasks can be managed using either Azure PowerShell cmdlets or REST APIs.</span></span>  <span data-ttu-id="e3a14-105">SQL veri ambarı tooautomate ortak görevlerin nasıl toouse PowerShell komutları bazı örnekleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e3a14-105">Below are some examples of how toouse PowerShell commands tooautomate common tasks in your SQL Data Warehouse.</span></span>  <span data-ttu-id="e3a14-106">Merhaba makale iyi bazı diğer örnekler için bkz [ölçeklenebilirlik REST ile yönetme][Manage scalability with REST].</span><span class="sxs-lookup"><span data-stu-id="e3a14-106">For some good REST examples, see hello article [Manage scalability with REST][Manage scalability with REST].</span></span>

> [!NOTE]
> <span data-ttu-id="e3a14-107">Sipariş toouse Azure PowerShell ile SQL Data Warehouse, ihtiyacınız Azure PowerShell 1.0.3 sürümü veya daha büyük.</span><span class="sxs-lookup"><span data-stu-id="e3a14-107">In order toouse Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="e3a14-108">Çalıştırarak sürümünüzü kontrol edebilirsiniz **Get-Module - listavailable birlikte-Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="e3a14-108">You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="e3a14-109">Merhaba en son sürümünü yüklenebilir [Microsoft Web Platformu yükleyicisi][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="e3a14-109">hello latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="e3a14-110">Merhaba en son sürümü yükleme hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="e3a14-110">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>
> 
> 

## <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="e3a14-111">Azure PowerShell cmdlet'leri kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e3a14-111">Get started with Azure PowerShell cmdlets</span></span>
1. <span data-ttu-id="e3a14-112">Windows PowerShell'i açın.</span><span class="sxs-lookup"><span data-stu-id="e3a14-112">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="e3a14-113">PowerShell komut isteminde hello bu komutları toosign toohello Azure Kaynak Yöneticisi'ni çalıştırın ve aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="e3a14-113">At hello PowerShell prompt, run these commands toosign in toohello Azure Resource Manager and select your subscription.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

## <a name="pause-sql-data-warehouse-example"></a><span data-ttu-id="e3a14-114">Duraklatma SQL veri ambarı örneği</span><span class="sxs-lookup"><span data-stu-id="e3a14-114">Pause SQL Data Warehouse Example</span></span>
<span data-ttu-id="e3a14-115">"" Server01."adlı bir sunucuda barındırılan Database02" adlı bir veritabanı duraklatma</span><span class="sxs-lookup"><span data-stu-id="e3a14-115">Pause a database named "Database02" hosted on a server named "Server01."</span></span>  <span data-ttu-id="e3a14-116">"ResourceGroup1." adlı bir Azure kaynak grubu içinde Hello sunucusudur</span><span class="sxs-lookup"><span data-stu-id="e3a14-116">hello server is in an Azure resource group named "ResourceGroup1."</span></span>

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="e3a14-117">Alınan hello nesne bu örnek bir değişim çok kanallar[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="e3a14-117">A variation, this example pipes hello retrieved object too[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span>  <span data-ttu-id="e3a14-118">Sonuç olarak, hello veritabanı duraklatıldı.</span><span class="sxs-lookup"><span data-stu-id="e3a14-118">As a result, hello database is paused.</span></span> <span data-ttu-id="e3a14-119">Merhaba son komut hello sonuçları gösterir.</span><span class="sxs-lookup"><span data-stu-id="e3a14-119">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

## <a name="start-sql-data-warehouse-example"></a><span data-ttu-id="e3a14-120">SQL veri ambarı örneği Başlat</span><span class="sxs-lookup"><span data-stu-id="e3a14-120">Start SQL Data Warehouse Example</span></span>
<span data-ttu-id="e3a14-121">"" Server01."adlı bir sunucuda barındırılan Database02" adlı bir veritabanı işlemi sürdürme</span><span class="sxs-lookup"><span data-stu-id="e3a14-121">Resume operation of a database named "Database02" hosted on a server named "Server01."</span></span> <span data-ttu-id="e3a14-122">Merhaba sunucu "ResourceGroup1." adlı bir kaynak grubunda yer alan</span><span class="sxs-lookup"><span data-stu-id="e3a14-122">hello server is contained in a resource group named "ResourceGroup1."</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="e3a14-123">Bir değişim Bu örnekte "" ResourceGroup1."adlı bir kaynak grubunda yer alan Server01" adlı bir sunucudan "Database02" adlı bir veritabanı alır.</span><span class="sxs-lookup"><span data-stu-id="e3a14-123">A variation, this example retrieves a database named "Database02" from a server named "Server01" that is contained in a resource group named "ResourceGroup1."</span></span> <span data-ttu-id="e3a14-124">Alınan hello nesne çok kanallar[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="e3a14-124">It pipes hello retrieved object too[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
```

> [!NOTE]
> <span data-ttu-id="e3a14-125">Sunucunuz foo.database.windows.net, ise "foo" Merhaba PowerShell cmdlet'leri - ServerName hello olarak kullanmak unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e3a14-125">Note that if your server is foo.database.windows.net, use "foo" as hello -ServerName in hello PowerShell cmdlets.</span></span>
> 
> 

## <a name="other-supported-powershell-cmdlets"></a><span data-ttu-id="e3a14-126">Diğer desteklenen PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="e3a14-126">Other supported PowerShell cmdlets</span></span>
<span data-ttu-id="e3a14-127">Bu PowerShell cmdlet'leri, Azure SQL Data Warehouse ile desteklenir.</span><span class="sxs-lookup"><span data-stu-id="e3a14-127">These PowerShell cmdlets are supported with Azure SQL Data Warehouse.</span></span>

* <span data-ttu-id="e3a14-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="e3a14-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="e3a14-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span><span class="sxs-lookup"><span data-stu-id="e3a14-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span></span>
* <span data-ttu-id="e3a14-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span><span class="sxs-lookup"><span data-stu-id="e3a14-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span></span>
* <span data-ttu-id="e3a14-131">[AzureRmSqlDatabase yeni][New-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="e3a14-131">[New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="e3a14-132">[Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="e3a14-132">[Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="e3a14-133">[Geri yükleme-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="e3a14-133">[Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="e3a14-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="e3a14-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="e3a14-135">[Select-AzureRmSubscription][Select-AzureRmSubscription]</span><span class="sxs-lookup"><span data-stu-id="e3a14-135">[Select-AzureRmSubscription][Select-AzureRmSubscription]</span></span>
* <span data-ttu-id="e3a14-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="e3a14-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="e3a14-137">[Askıya alma AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="e3a14-137">[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3a14-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e3a14-138">Next steps</span></span>
<span data-ttu-id="e3a14-139">Daha fazla PowerShell örnekler için bkz:</span><span class="sxs-lookup"><span data-stu-id="e3a14-139">For more PowerShell examples, see:</span></span>

* <span data-ttu-id="e3a14-140">[PowerShell kullanarak SQL Data Warehouse oluşturma][Create a SQL Data Warehouse using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="e3a14-140">[Create a SQL Data Warehouse using PowerShell][Create a SQL Data Warehouse using PowerShell]</span></span>
* <span data-ttu-id="e3a14-141">[Veritabanı geri yükleme][Database restore]</span><span class="sxs-lookup"><span data-stu-id="e3a14-141">[Database restore][Database restore]</span></span>

<span data-ttu-id="e3a14-142">PowerShell ile otomatik olarak diğer görevler için bkz: [Azure SQL veritabanı cmdlet'leri][Azure SQL Database Cmdlets].</span><span class="sxs-lookup"><span data-stu-id="e3a14-142">For other tasks which can be automated with PowerShell, see [Azure SQL Database Cmdlets][Azure SQL Database Cmdlets].</span></span> <span data-ttu-id="e3a14-143">Tüm Azure SQL veritabanı cmdlet'leri Azure SQL Data Warehouse için desteklendiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e3a14-143">Note that not all Azure SQL Database cmdlets are supported for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="e3a14-144">Hangi BİLGİSAYARLARLA otomatik görevlerin listesi için bkz: [işlemleri Azure SQL veritabanları için][Operations for Azure SQL Databases].</span><span class="sxs-lookup"><span data-stu-id="e3a14-144">For a list of tasks which can be automated with REST, see [Operations for Azure SQL Databases][Operations for Azure SQL Databases].</span></span>

<!--Image references-->

<!--Article references-->
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
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
<!-- It appears that Select-AzureRmSubscription isn't documented, so this points tooSelect-AzureSubscription -->
[Select-AzureRmSubscription]: https://msdn.microsoft.com/library/dn722499.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
