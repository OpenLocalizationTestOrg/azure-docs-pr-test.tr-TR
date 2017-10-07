---
title: PowerShell kullanarak SQL Data Warehouse aaaCreate | Microsoft Docs
description: "PowerShell kullanarak SQL Data Warehouse oluşturma"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 97434863-7938-4129-8949-5a119f5949e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d8af29ec285a11285785ab5474e4dfc8c36bc3ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-sql-data-warehouse-using-powershell"></a><span data-ttu-id="568ca-103">PowerShell kullanarak SQL Data Warehouse oluşturma</span><span class="sxs-lookup"><span data-stu-id="568ca-103">Create SQL Data Warehouse using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="568ca-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="568ca-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="568ca-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="568ca-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="568ca-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="568ca-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="568ca-107">Bu makalede nasıl toocreate bir SQL Data Warehouse PowerShell kullanarak gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="568ca-107">This article shows you how toocreate a SQL Data Warehouse using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="568ca-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="568ca-108">Prerequisites</span></span>
<span data-ttu-id="568ca-109">başlatılan tooget, aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="568ca-109">tooget started, you need:</span></span>

* <span data-ttu-id="568ca-110">**Azure hesabı**: ziyaret [Azure ücretsiz deneme sürümü] [ Azure Free Trial] veya [MSDN Azure KREDİLERİ] [ MSDN Azure Credits] toocreate bir hesap.</span><span class="sxs-lookup"><span data-stu-id="568ca-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="568ca-111">**Azure SQL server**: bkz [hello Azure portalı bir Azure SQL veritabanı oluşturma] [ Create an Azure SQL database in hello Azure Portal] veya [PowerShell ile bir Azure SQL veritabanı oluşturma] [ Create an Azure SQL database with PowerShell] daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="568ca-111">**Azure SQL server**:  See [Create an Azure SQL database in hello Azure Portal][Create an Azure SQL database in hello Azure Portal] or [Create an Azure SQL database with PowerShell][Create an Azure SQL database with PowerShell] for more details.</span></span>
* <span data-ttu-id="568ca-112">**Kaynak grubu**: aynı kaynak grubu olarak Azure SQL sunucunuzun ya da bakın hello kullanın ya da [nasıl toocreate bir kaynak grubu](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="568ca-112">**Resource group**: Either use hello same resource group as your Azure SQL server or see [how toocreate a resource group](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="568ca-113">**PowerShell 1.0.3 sürümü veya sonraki bir sürümü**: **Get-Module -ListAvailable -Name Azure** komutunu çalıştırarak sürümünüzü kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="568ca-113">**PowerShell version 1.0.3 or greater**:  You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="568ca-114">Merhaba en son sürümünü yüklenebilir [Microsoft Web Platformu yükleyicisi][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="568ca-114">hello latest version can be installed from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="568ca-115">Merhaba en son sürümü yükleme hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="568ca-115">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>

> [!NOTE]
> <span data-ttu-id="568ca-116">Bir SQL Veri Ambarı'nın oluşturulması ek hizmet ücretlerinin alınmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="568ca-116">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="568ca-117">Fiyatlandırmayla ilgili ayrıntılı bilgi için bkz. [SQL Veri Ambarı fiyatlandırması][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="568ca-117">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="568ca-118">SQL Data Warehouse oluşturma</span><span class="sxs-lookup"><span data-stu-id="568ca-118">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="568ca-119">Windows PowerShell'i açın.</span><span class="sxs-lookup"><span data-stu-id="568ca-119">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="568ca-120">Bu cmdlet toologin tooAzure Kaynak Yöneticisi'ni çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="568ca-120">Run this cmdlet toologin tooAzure Resource Manager.</span></span>

    ```Powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="568ca-121">Geçerli oturumunuz için toouse istediğiniz hello aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="568ca-121">Select hello subscription you want toouse for your current session.</span></span>

    ```Powershell
    Get-AzureRmSubscription    -SubscriptionName "MySubscription" | Select-AzureRmSubscription
    ```
4. <span data-ttu-id="568ca-122">Veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="568ca-122">Create database.</span></span> <span data-ttu-id="568ca-123">Bu örnekte "mywesteuroperesgp1" hizmet hedefi düzeyi "DW400", "mywesteuroperesgp1" adlı hello kaynak grubunda bulunan "sqldwserver1" adlı toohello sunucu adlı bir veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="568ca-123">This example creates a database named "mynewsqldw", with service objective level "DW400", toohello server named "sqldwserver1", which is in hello resource group named "mywesteuroperesgp1".</span></span>

   ```Powershell
   New-AzureRmSqlDatabase -RequestedServiceObjectiveName "DW400" -DatabaseName "mynewsqldw" -ServerName "sqldwserver1" -ResourceGroupName "mywesteuroperesgp1" -Edition "DataWarehouse" -CollationName "SQL_Latin1_General_CP1_CI_AS" -MaxSizeBytes 10995116277760
   ```

<span data-ttu-id="568ca-124">Gerekli Parametreler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="568ca-124">Required Parameters are:</span></span>

* <span data-ttu-id="568ca-125">**RequestedServiceObjectiveName**: hello miktarını [DWU] [ DWU] isteğinde bulunduğunuzu.</span><span class="sxs-lookup"><span data-stu-id="568ca-125">**RequestedServiceObjectiveName**: hello amount of [DWU][DWU] you are requesting.</span></span>  <span data-ttu-id="568ca-126">Desteklenen değerler: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000 ve DW6000.</span><span class="sxs-lookup"><span data-stu-id="568ca-126">Supported values are: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000, and DW6000.</span></span>
* <span data-ttu-id="568ca-127">**DatabaseName**: hello oluşturmakta olduğunuz SQL Data Warehouse hello adı.</span><span class="sxs-lookup"><span data-stu-id="568ca-127">**DatabaseName**: hello name of hello SQL Data Warehouse that you are creating.</span></span>
* <span data-ttu-id="568ca-128">**ServerName**: hello oluşturmak için kullandığınız hello sunucunun adını (V12 olmalıdır).</span><span class="sxs-lookup"><span data-stu-id="568ca-128">**ServerName**: hello name of hello server that you are using for creation (must be V12).</span></span>
* <span data-ttu-id="568ca-129">**ResourceGroupName**: Kullandığınız kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="568ca-129">**ResourceGroupName**: Resource group you are using.</span></span>  <span data-ttu-id="568ca-130">aboneliğinizde toofind kullanılabilir kaynak gruplarını Get-azureresource komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="568ca-130">toofind available resource groups in your subscription use Get-AzureResource.</span></span>
* <span data-ttu-id="568ca-131">**Edition**: "DataWarehouse" toocreate SQL Data Warehouse olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="568ca-131">**Edition**: Must be "DataWarehouse" toocreate a SQL Data Warehouse.</span></span>

<span data-ttu-id="568ca-132">İsteğe Bağlı Parametreler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="568ca-132">Optional Parameters are:</span></span>

* <span data-ttu-id="568ca-133">**CollationName**: belirtilmezse hello varsayılan harmanlama sql_latin1_general_cp1_cı_as olduğu.</span><span class="sxs-lookup"><span data-stu-id="568ca-133">**CollationName**: hello default collation if not specified is SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="568ca-134">Bir veritabanı üzerinde harmanlama değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="568ca-134">Collation cannot be changed on a database.</span></span>
* <span data-ttu-id="568ca-135">**MaxSizeBytes**: veritabanı hello varsayılan en büyük boyut olan 10 GB.</span><span class="sxs-lookup"><span data-stu-id="568ca-135">**MaxSizeBytes**: hello default max size of a database is 10 GB.</span></span>

<span data-ttu-id="568ca-136">Merhaba parametre seçenekleri hakkında daha fazla bilgi için bkz: [New-AzureRmSqlDatabase] [ New-AzureRmSqlDatabase] ve [veritabanı (Azure SQL Data Warehouse) oluşturma][Create Database (Azure SQL Data Warehouse)].</span><span class="sxs-lookup"><span data-stu-id="568ca-136">For more details on hello parameter options, see [New-AzureRmSqlDatabase][New-AzureRmSqlDatabase] and [Create Database (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)].</span></span>

## <a name="next-steps"></a><span data-ttu-id="568ca-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="568ca-137">Next steps</span></span>
<span data-ttu-id="568ca-138">SQL veri ambarı tamamlandıktan sonra sağlama tootry isteyebilirsiniz [örnek veri yükleme] [ loading sample data] veya nasıl çok denetleyin[geliştirmek] [ develop] , [yük][load], veya [geçirmek][migrate].</span><span class="sxs-lookup"><span data-stu-id="568ca-138">After your SQL Data Warehouse has finished provisioning you may want tootry [loading sample data][loading sample data] or check out how too[develop][develop], [load][load], or [migrate][migrate].</span></span>

<span data-ttu-id="568ca-139">Nasıl daha fazla bilgi ilginizi çekiyorsa toomanage SQL Data Warehouse programlı olarak kullanıma nasıl makalesini toouse [PowerShell cmdlet'leri ve REST API'lerinin][PowerShell cmdlets and REST APIs].</span><span class="sxs-lookup"><span data-stu-id="568ca-139">If you're interested in more on how toomanage SQL Data Warehouse programmatically, check out our article on how toouse [PowerShell cmdlets and REST APIs][PowerShell cmdlets and REST APIs].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[migrate]: ./sql-data-warehouse-overview-migrate.md
[develop]: ./sql-data-warehouse-overview-develop.md
[load]: ./sql-data-warehouse-load-with-bcp.md
[loading sample data]: ./sql-data-warehouse-load-sample-databases.md
[PowerShell cmdlets and REST APIs]: ./sql-data-warehouse-reference-powershell-cmdlets.md
[firewall rules]: ../sql-database-configure-firewall-settings.md

[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[how toocreate a SQL Data Warehouse from hello Azure Portal]: ./sql-data-warehouse-get-started-provision.md
[Create an Azure SQL database in hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-get-started-powershell.md
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group

<!--MSDN references-->
[MSDN]: https://msdn.microsoft.com/library/azure/dn546722.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Create Database (Azure SQL Data Warehouse)]: https://msdn.microsoft.com/library/mt204021.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
