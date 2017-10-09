---
title: TSQL ile SQL Data Warehouse aaaCreate | Microsoft Docs
description: "Nasıl toocreate bir Azure SQL Data Warehouse TSQL ile bilgi edinin"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: a4e2e68e-aa9c-4dd3-abb0-f7df997d237a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 81ef59a66c61452ff8a2aca29837f155e87d017d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-sql-data-warehouse-database-by-using-transact-sql-tsql"></a><span data-ttu-id="257d1-103">Transact-SQL (TSQL) kullanarak SQL Data Warehouse oluşturma</span><span class="sxs-lookup"><span data-stu-id="257d1-103">Create a SQL Data Warehouse database by using Transact-SQL (TSQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="257d1-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="257d1-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="257d1-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="257d1-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="257d1-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="257d1-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="257d1-107">Bu makalede nasıl toocreate bir SQL Data Warehouse T-SQL kullanarak gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="257d1-107">This article shows you how toocreate a SQL Data Warehouse using T-SQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="257d1-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="257d1-108">Prerequisites</span></span>
<span data-ttu-id="257d1-109">başlatılan tooget, aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="257d1-109">tooget started, you need:</span></span>

* <span data-ttu-id="257d1-110">**Azure hesabı**: ziyaret [Azure ücretsiz deneme sürümü] [ Azure Free Trial] veya [MSDN Azure KREDİLERİ] [ MSDN Azure Credits] toocreate bir hesap.</span><span class="sxs-lookup"><span data-stu-id="257d1-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="257d1-111">**Azure SQL server**: bkz. [oluşturma hello Azure Portal ile Azure SQL Database mantıksal sunucusu] [hello Azure Portal ile Azure SQL Database mantıksal sunucusu Oluştur] veya [PowerShell ile Azure SQL Database mantıksal sunucusu oluşturma] [bir Azure SQL oluştur PowerShell ile Database mantıksal sunucusu] daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="257d1-111">**Azure SQL server**:  See [Create an Azure SQL Database logical server with hello Azure Portal][Create an Azure SQL Database logical server with hello Azure Portal] or [Create an Azure SQL Database logical server with PowerShell][Create an Azure SQL Database logical server with PowerShell] for more details.</span></span>
* <span data-ttu-id="257d1-112">**Kaynak grubu**: aynı kaynak grubu olarak Azure SQL sunucunuzun ya da bakın hello kullanın ya da [nasıl toocreate bir kaynak grubu][how toocreate a resource group].</span><span class="sxs-lookup"><span data-stu-id="257d1-112">**Resource group**: Either use hello same resource group as your Azure SQL server or see [how toocreate a resource group][how toocreate a resource group].</span></span>
* <span data-ttu-id="257d1-113">**Ortam tooexecute T-SQL**: kullanabileceğiniz [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], veya [SSMS] [ SSMS] tooexecute T-SQL.</span><span class="sxs-lookup"><span data-stu-id="257d1-113">**Environment tooexecute T-SQL**: You can use [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], or [SSMS][SSMS] tooexecute T-SQL.</span></span>

> [!NOTE]
> <span data-ttu-id="257d1-114">Bir SQL Veri Ambarı'nın oluşturulması ek hizmet ücretlerinin alınmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="257d1-114">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="257d1-115">Fiyatlandırmayla ilgili ayrıntılı bilgi için bkz. [SQL Veri Ambarı fiyatlandırması][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="257d1-115">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-database-with-visual-studio"></a><span data-ttu-id="257d1-116">Visual Studio ile veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="257d1-116">Create a database with Visual Studio</span></span>
<span data-ttu-id="257d1-117">Yeni tooVisual Studio varsa, hello makalesine bakın [sorgu Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span><span class="sxs-lookup"><span data-stu-id="257d1-117">If you are new tooVisual Studio, see hello article [Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span></span>  <span data-ttu-id="257d1-118">toostart, Visual Studio ile SQL Server nesne Gezgini'ni açın ve SQL Data Warehouse veritabanınızı barındıracak toohello sunucusuna bağlanın.</span><span class="sxs-lookup"><span data-stu-id="257d1-118">toostart, open SQL Server Object Explorer in Visual Studio and connect toohello server that will host your SQL Data Warehouse database.</span></span>  <span data-ttu-id="257d1-119">Bağlandıktan sonra aşağıdaki SQL komutunu hello hello çalıştırarak SQL Data Warehouse oluşturabilirsiniz **ana** veritabanı.</span><span class="sxs-lookup"><span data-stu-id="257d1-119">Once connected, you can create a SQL Data Warehouse by running hello following SQL command against hello **master** database.</span></span>  <span data-ttu-id="257d1-120">Bu komut, bir hizmet hedefi DW400 olan hello veritabanı olacak oluşturur ve hello veritabanı toogrow tooa maksimum boyutu 10 TB'lık izin.</span><span class="sxs-lookup"><span data-stu-id="257d1-120">This command creates hello database MySqlDwDb with a Service Objective of DW400 and allow hello database toogrow tooa maximum size of 10 TB.</span></span>

```sql
CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB);
```

## <a name="create-a-database-with-sqlcmd"></a><span data-ttu-id="257d1-121">sqlcmd ile veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="257d1-121">Create a database with sqlcmd</span></span>
<span data-ttu-id="257d1-122">Alternatif olarak, aynı komutu çalıştırarak sqlcmd ile Merhaba bir komut isteminde aşağıdaki hello çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="257d1-122">Alternatively, you can run hello same command with sqlcmd by running hello following at a command prompt.</span></span>

```sql
sqlcmd -S <Server Name>.database.windows.net -I -U <User> -P <Password> -Q "CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB)"
```

<span data-ttu-id="257d1-123">belirtilmemişse hello varsayılan harmanlaması HARMANLAMA sql_latin1_general_cp1_cı_as ' dir.</span><span class="sxs-lookup"><span data-stu-id="257d1-123">hello default collation when not specified is COLLATE SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="257d1-124">Merhaba `MAXSIZE` 250 GB ile 240 TB arasında olabilir.</span><span class="sxs-lookup"><span data-stu-id="257d1-124">hello `MAXSIZE` can be between 250 GB and 240 TB.</span></span>  <span data-ttu-id="257d1-125">Merhaba `SERVICE_OBJECTIVE` DW100 ve DW2000 arasında olabilir [DWU][DWU].</span><span class="sxs-lookup"><span data-stu-id="257d1-125">hello `SERVICE_OBJECTIVE` can be between DW100 and DW2000 [DWU][DWU].</span></span>  <span data-ttu-id="257d1-126">Geçerli tüm değerlerin listesi için hello MSDN belgelerine bakın [CREATE DATABASE][CREATE DATABASE].</span><span class="sxs-lookup"><span data-stu-id="257d1-126">For a list of all valid values, see hello MSDN documentation for [CREATE DATABASE][CREATE DATABASE].</span></span>  <span data-ttu-id="257d1-127">Merhaba MAXSIZE ve servıce_objectıve can ile değiştirilmesi bir [ALTER DATABASE] [ ALTER DATABASE] T-SQL komutu.</span><span class="sxs-lookup"><span data-stu-id="257d1-127">Both hello MAXSIZE and SERVICE_OBJECTIVE can be changed with an [ALTER DATABASE][ALTER DATABASE] T-SQL command.</span></span>  <span data-ttu-id="257d1-128">Veritabanı harmanlamasının Hello oluşturulduktan sonra değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="257d1-128">hello collation of a database cannot be changed after creation.</span></span>   <span data-ttu-id="257d1-129">Yürütülen tüm sorguları iptal yeniden başlatma hizmetlerinin DWU değiştirme olarak değişen hello servıce_objectıve neden olduğunda dikkat kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="257d1-129">Caution should be used when changing hello SERVICE_OBJECTIVE as changing DWU causes a restart of services, which cancels all queries in flight.</span></span>  <span data-ttu-id="257d1-130">MAXSIZE parametresinin değiştirilmesi basit bir meta veri işlemi olduğundan hizmetler yeniden başlatılmaz.</span><span class="sxs-lookup"><span data-stu-id="257d1-130">Changing MAXSIZE does not restart services as it is just a simple metadata operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="257d1-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="257d1-131">Next steps</span></span>
<span data-ttu-id="257d1-132">SQL veri ambarı yapabilecekleriniz Sağlama tamamlandıktan sonra [örnek verileri yükleme] [ load sample data] veya nasıl çok denetleyin[geliştirmek][develop], [yük][load], veya [geçirmek][migrate].</span><span class="sxs-lookup"><span data-stu-id="257d1-132">After your SQL Data Warehouse has finished provisioning you can [load sample data][load sample data] or check out how too[develop][develop], [load][load], or [migrate][migrate].</span></span>

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[how toocreate a SQL Data Warehouse from hello Azure portal]: sql-data-warehouse-get-started-provision.md
[Query Azure SQL Data Warehouse (Visual Studio)]: sql-data-warehouse-query-visual-studio.md
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data]: sql-data-warehouse-load-sample-databases.md
[Create an Azure SQL database with hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--MSDN references-->
[CREATE DATABASE]: https://msdn.microsoft.com/library/mt204021.aspx
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
