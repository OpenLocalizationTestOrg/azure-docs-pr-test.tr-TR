---
title: "Bir Azure SQL veritabanı oluşturmak için bir BACPAC dosyasını içeri | Microsoft Docs"
description: "Bir BACPAC dosyasını içeri aktararak newAzure SQL veritabanı oluşturun."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: cf9a9631-56aa-4985-a565-1cacc297871d
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/26/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 285e17ed6d0ce700cb518864df7a3b5f5e55bee5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="import-a-bacpac-file-to-a-new-azure-sql-database"></a><span data-ttu-id="e03a7-103">Yeni bir Azure SQL veritabanı için bir BACPAC dosyasını içeri aktarın</span><span class="sxs-lookup"><span data-stu-id="e03a7-103">Import a BACPAC file to a new Azure SQL Database</span></span>

<span data-ttu-id="e03a7-104">Ne zaman bir veritabanı arşivden içeri aktarmanız gerekir ya da başka bir platformundan geçirirken, verileri ve veritabanı şeması aktarabilirsiniz bir [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) dosya.</span><span class="sxs-lookup"><span data-stu-id="e03a7-104">When you need to import a database from an archive or when migrating from another platform, you can import the database schema and data from a [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file.</span></span> <span data-ttu-id="e03a7-105">ZIP dosyası meta verileri ve SQL Server veritabanından veri içeren BACPAC uzantılı bir BACPAC dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="e03a7-105">A BACPAC file is a ZIP file with an extension of BACPAC containing the metadata and data from a SQL Server database.</span></span> <span data-ttu-id="e03a7-106">Bir BACPAC dosyası (yalnızca standart depolama) Azure blob depolama alanından içeri aktarılabilir veya bir şirket içi konumda yerel depolama.</span><span class="sxs-lookup"><span data-stu-id="e03a7-106">A BACPAC file can be imported from Azure blob storage (standard storage only) or from local storage in an on-premises location.</span></span> <span data-ttu-id="e03a7-107">Alma hızı en üst düzeye çıkarmak için daha yüksek Hizmet katmanını ve performans düzeyi, bir P6 gibi belirtin ve ardından içeri aktarma başarılı olduktan sonra uygun şekilde aşağı Ölçekle öneririz.</span><span class="sxs-lookup"><span data-stu-id="e03a7-107">To maximize the import speed, we recommend that you specify a higher service tier and performance level, such as a P6, and then scale to down as appropriate after the import is successful.</span></span> <span data-ttu-id="e03a7-108">Ayrıca, veritabanı uyumluluk düzeyi içe aktarmadan sonra kaynak veritabanı uyumluluk düzeyini temel alır.</span><span class="sxs-lookup"><span data-stu-id="e03a7-108">Also, the database compatibility level after the import is based on the compatibility level of the source database.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="e03a7-109">Azure SQL veritabanına veritabanınızı geçirdikten sonra veritabanını geçerli uyumluluk düzeyinde (düzey 100 AdventureWorks2008R2 veritabanı için) veya daha yüksek düzeyde çalışmaya seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e03a7-109">After you migrate your database to Azure SQL Database, you can choose to operate the database at its current compatibility level (level 100 for the AdventureWorks2008R2 database) or at a higher level.</span></span> <span data-ttu-id="e03a7-110">Uygulamaları ve belirli bir uyumluluk düzeyinde bir veritabanı işletim seçenekleri hakkında daha fazla bilgi için bkz: [ALTER veritabanı uyumluluk düzeyi](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span><span class="sxs-lookup"><span data-stu-id="e03a7-110">For more information on the implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span></span> <span data-ttu-id="e03a7-111">Ayrıca bkz. [ALTER veritabanı kapsamlı yapılandırma](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) Uyumluluk Düzeyleri ilgili ek veritabanı düzeyi ayarları hakkında bilgi için.</span><span class="sxs-lookup"><span data-stu-id="e03a7-111">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related to compatibility levels.</span></span>   >

> [!NOTE]
> <span data-ttu-id="e03a7-112">Yeni bir veritabanı için bir BACPAC almak için ilk Azure SQL Database mantıksal sunucusu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e03a7-112">To import a BACPAC to a new database, you must first create an Azure SQL Database logical server.</span></span> <span data-ttu-id="e03a7-113">SQL Server veritabanını Azure SQL veritabanına SQLPackage kullanarak geçirmek nasıl gösteren bir öğretici için bkz: [SQL Server veritabanına geçirme](sql-database-migrate-your-sql-server-database.md)</span><span class="sxs-lookup"><span data-stu-id="e03a7-113">For a tutorial showing you how to migrate a SQL Server database to Azure SQL Database using SQLPackage, see [Migrate a SQL Server Database](sql-database-migrate-your-sql-server-database.md)</span></span>
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a><span data-ttu-id="e03a7-114">Azure portalını kullanarak bir BACPAC Dosyadan İçeri Aktar</span><span class="sxs-lookup"><span data-stu-id="e03a7-114">Import from a BACPAC file using Azure portal</span></span>

<span data-ttu-id="e03a7-115">Bu makalede, Azure blob storage kullanarak depolanan bir BACPAC dosyasından bir Azure SQL veritabanı oluşturma için yönergeler sağlanmaktadır [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e03a7-115">This article provides directions for creating an Azure SQL database from a BACPAC file stored in Azure blob storage using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e03a7-116">İçeri aktarma yalnızca Azure portalını kullanarak Azure blob depolama alanından bir BACPAC dosyasını içeri destekler.</span><span class="sxs-lookup"><span data-stu-id="e03a7-116">Import using the Azure portal only supports importing a BACPAC file from Azure blob storage.</span></span>

<span data-ttu-id="e03a7-117">Azure Portalı'nı kullanarak bir veritabanını almak için veritabanınızın sayfasını açın ve **alma** araç çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="e03a7-117">To import a database using the Azure portal, open the page for your database and click **Import** on the toolbar.</span></span> <span data-ttu-id="e03a7-118">Depolama hesabı ve kapsayıcı belirtin ve içeri aktarmak istediğiniz BACPAC dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="e03a7-118">Specify the storage account and container, and select the BACPAC file you want to import.</span></span> <span data-ttu-id="e03a7-119">Yeni veritabanı (genellikle aynı kaynak) boyutunu seçin ve hedef SQL Server kimlik bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="e03a7-119">Select the size of the new database (usually the same as origin) and provide the destination SQL Server credentials.</span></span>  

   ![Veritabanını içeri aktarma](./media/sql-database-import/import.png)

<span data-ttu-id="e03a7-121">İçeri aktarma işlemin ilerlemesini izlemek için içeri aktarılan veritabanını içeren mantıksal sunucu için sayfayı açın.</span><span class="sxs-lookup"><span data-stu-id="e03a7-121">To monitor the progress of the import operation, open the page for the logical server containing the database being imported.</span></span> <span data-ttu-id="e03a7-122">Ekranı aşağı kaydırarak **Operations** ve ardından **içeri/dışarı aktarma** geçmişi.</span><span class="sxs-lookup"><span data-stu-id="e03a7-122">Scroll down to **Operations** and then click **Import/Export** history.</span></span>

### <a name="monitor-the-progress-of-an-import-operation"></a><span data-ttu-id="e03a7-123">İçeri aktarma işleminin ilerleyişini izleyin</span><span class="sxs-lookup"><span data-stu-id="e03a7-123">Monitor the progress of an import operation</span></span>

<span data-ttu-id="e03a7-124">İçe aktarma işleminin ilerlemesini izlemek için alınan veritabanı alınmakta mantıksal sunucu için sayfayı açın.</span><span class="sxs-lookup"><span data-stu-id="e03a7-124">To monitor the progress of the import operation, open the page for the logical server into which the database is being imported imported.</span></span> <span data-ttu-id="e03a7-125">Ekranı aşağı kaydırarak **Operations** ve ardından **içeri/dışarı aktarma** geçmişi.</span><span class="sxs-lookup"><span data-stu-id="e03a7-125">Scroll down to **Operations** and then click **Import/Export** history.</span></span>
   
   <span data-ttu-id="e03a7-126">![Alma](./media/sql-database-import/import-history.png) ![alma durumu](./media/sql-database-import/import-status.png)</span><span class="sxs-lookup"><span data-stu-id="e03a7-126">![import](./media/sql-database-import/import-history.png) ![import status](./media/sql-database-import/import-status.png)</span></span>

<span data-ttu-id="e03a7-127">Veritabanı sunucusunda Canlı doğrulamak için tıklatın **SQL veritabanları** ve yeni veritabanı doğrulamanız **çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="e03a7-127">To verify the database is live on the server, click **SQL databases** and verify the new database is **Online**.</span></span>

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a><span data-ttu-id="e03a7-128">SQLPackage kullanarak bir BACPAC Dosyadan İçeri Aktar</span><span class="sxs-lookup"><span data-stu-id="e03a7-128">Import from a BACPAC file using SQLPackage</span></span>

<span data-ttu-id="e03a7-129">SQL veritabanı kullanarak içe aktarmak için [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) komut satırı yardımcı programı, bkz: [alma parametreleri ve özellikleri](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span><span class="sxs-lookup"><span data-stu-id="e03a7-129">To import a SQL database using the [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Import parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span></span> <span data-ttu-id="e03a7-130">SQLPackage yardımcı programı en son sürümleri ile birlikte gelen [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) ve [SQL Server veri araçları Visual Studio için](https://msdn.microsoft.com/library/mt204009.aspx), veya en son sürümünü indirebilirsiniz [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) doğrudan Microsoft İndirme Merkezi'nden.</span><span class="sxs-lookup"><span data-stu-id="e03a7-130">The SQLPackage utility ships with the latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download the latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from the Microsoft download center.</span></span>

<span data-ttu-id="e03a7-131">Ölçek ve performans çoğu üretim ortamlarında SQLPackage yardımcı programı kullanılmak öneririz.</span><span class="sxs-lookup"><span data-stu-id="e03a7-131">We recommend the use of the SQLPackage utility for scale and performance in most production environments.</span></span> <span data-ttu-id="e03a7-132">BACPAC dosyalarını kullanarak geçiş hakkında bir SQL Server Müşteri Danışmanlık Ekibi blogu için bkz. [BACPAC Dosyalarını kullanarak SQL Server’dan Azure SQL Veritabanına Geçiş](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span><span class="sxs-lookup"><span data-stu-id="e03a7-132">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

<span data-ttu-id="e03a7-133">Aşağıdaki içeri aktarma SQLPackage komutu bir komut dosyası örneği için bkz: **AdventureWorks2008R2** adlı bir Azure SQL Database mantıksal sunucusu yerel depolama biriminden veritabanına **mynewserver20170403** Bu örnekte.</span><span class="sxs-lookup"><span data-stu-id="e03a7-133">See the following SQLPackage command for a script example for how to import the **AdventureWorks2008R2** database from local storage to an Azure SQL Database logical server, called **mynewserver20170403** in this example.</span></span> <span data-ttu-id="e03a7-134">Bu komut dosyası olarak adlandırılan yeni bir veritabanı oluşturulmasını gösterir **myMigratedDatabase**, bir hizmet katmanını ile **Premium**ve bir hizmet amacını **P6**.</span><span class="sxs-lookup"><span data-stu-id="e03a7-134">This script shows the creation of a new database called **myMigratedDatabase**, with a service tier of **Premium**, and a Service Objective of **P6**.</span></span> <span data-ttu-id="e03a7-135">Bu değerleri ortamınıza uygun şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e03a7-135">Change these values as appropriate to your environment.</span></span>

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![sqlpackage alma](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> <span data-ttu-id="e03a7-137">Azure SQL Veritabanı mantıksal sunucusu 1433 numaralı bağlantı noktasında dinler.</span><span class="sxs-lookup"><span data-stu-id="e03a7-137">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="e03a7-138">Azure SQL Veritabanı mantıksal sunucusuna bir şirket ağından bağlanmaya çalışıyorsanız, bu bağlantı noktası başarıyla bağlanmanız için şirket güvenlik ağında açık olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e03a7-138">If you are attempting to connect to an Azure SQL Database logical server from within a corporate firewall, this port must be open in the corporate firewall for you to successfully connect.</span></span>
>

<span data-ttu-id="e03a7-139">Bu örnek, Active Directory Evrensel kimlik doğrulaması ile SqlPackage.exe kullanarak bir veritabanını içeri aktarma gösterir:</span><span class="sxs-lookup"><span data-stu-id="e03a7-139">This example shows how to import a database using SqlPackage.exe with Active Directory Universal Authentication:</span></span>

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a><span data-ttu-id="e03a7-140">PowerShell kullanarak bir BACPAC Dosyadan İçeri Aktar</span><span class="sxs-lookup"><span data-stu-id="e03a7-140">Import from a BACPAC file using PowerShell</span></span>

<span data-ttu-id="e03a7-141">Kullanım [yeni AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet'ini Azure SQL veritabanı hizmetinin bir alma veritabanı isteği gönderin.</span><span class="sxs-lookup"><span data-stu-id="e03a7-141">Use the [New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet to submit an import database request to the Azure SQL Database service.</span></span> <span data-ttu-id="e03a7-142">Veritabanı boyutuna bağlı olarak, içeri aktarma işlemini tamamlamak için biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="e03a7-142">Depending on the size of your database, the import operation may take some time to complete.</span></span>

 ```powershell
 $importRequest = New-AzureRmSqlDatabaseImport -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "MyImportSample" `
    -DatabaseMaxSizeBytes "262144000" `
    -StorageKeyType "StorageAccessKey" `
    -StorageKey $(Get-AzureRmStorageAccountKey -ResourceGroupName "myResourceGroup" -StorageAccountName $storageaccountname).Value[0] `
    -StorageUri "http://$storageaccountname.blob.core.windows.net/importsample/sample.bacpac" `
    -Edition "Standard" `
    -ServiceObjectiveName "P6" `
    -AdministratorLogin "ServerAdmin" `
    -AdministratorLoginPassword $(ConvertTo-SecureString -String "ASecureP@assw0rd" -AsPlainText -Force)

 ```

<span data-ttu-id="e03a7-143">İçeri aktarma isteği durumunu denetlemek için kullanmak [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="e03a7-143">To check the status of the import request, use the [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span></span> <span data-ttu-id="e03a7-144">Bu hemen sonra istek döndürür genellikle çalıştığını **durumu: devam ediyor**.</span><span class="sxs-lookup"><span data-stu-id="e03a7-144">Running this immediately after the request usually returns **Status: InProgress**.</span></span> <span data-ttu-id="e03a7-145">Gördüğünüzde **durumu: başarılı** alma işlemi tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="e03a7-145">When you see **Status: Succeeded** the import is complete.</span></span>

```powershell
$importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
[Console]::Write("Importing")
while ($importStatus.Status -eq "InProgress")
{
    $importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
    [Console]::Write(".")
    Start-Sleep -s 10
}
[Console]::WriteLine("")
$importStatus
```

> [!TIP]
<span data-ttu-id="e03a7-146">Başka bir komut dosyası örneği için bkz: [bir BACPAC dosyadan bir veritabanı](scripts/sql-database-import-from-bacpac-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e03a7-146">For another script example, see [Import a database from a BACPAC file](scripts/sql-database-import-from-bacpac-powershell.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e03a7-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e03a7-147">Next steps</span></span>
* <span data-ttu-id="e03a7-148">Bağlanmak ve içeri aktarılan bir SQL veritabanını sorgulamak öğrenmek için bkz: [SQL Server Management Studio ile SQL veritabanına bağlanma ve örnek T-SQL sorgusu gerçekleştirmeyi](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="e03a7-148">To learn how to connect to and query an imported SQL Database, see [Connect to SQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>
* <span data-ttu-id="e03a7-149">BACPAC dosyalarını kullanarak geçiş hakkında bir SQL Server Müşteri Danışmanlık Ekibi blogu için bkz. [BACPAC Dosyalarını kullanarak SQL Server’dan Azure SQL Veritabanına Geçiş](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span><span class="sxs-lookup"><span data-stu-id="e03a7-149">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>
* <span data-ttu-id="e03a7-150">Performans önerileri dahil olmak üzere tüm SQL Server veritabanı geçiş işlemi, bir tartışma için bkz [bir SQL Server veritabanını Azure SQL veritabanına geçirme](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="e03a7-150">For a discussion of the entire SQL Server database migration process, including performance recommendations, see [Migrate a SQL Server database to Azure SQL Database](sql-database-cloud-migrate.md).</span></span>



