---
title: "aaaImport bir BACPAC toocreate bir Azure SQL veritabanı dosyası | Microsoft Docs"
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
ms.openlocfilehash: 0d5fc93acf27b79502969fcd6199d11161915b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="import-a-bacpac-file-tooa-new-azure-sql-database"></a><span data-ttu-id="690b4-103">Bir BACPAC dosya tooa alma yeni Azure SQL veritabanı</span><span class="sxs-lookup"><span data-stu-id="690b4-103">Import a BACPAC file tooa new Azure SQL Database</span></span>

<span data-ttu-id="690b4-104">Ne zaman tooimport bir arşiv veritabanından gerekir ya da başka bir platformundan geçirilirken hello veritabanı şemasını ve verileri içeri aktarabilirsiniz bir [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) dosya.</span><span class="sxs-lookup"><span data-stu-id="690b4-104">When you need tooimport a database from an archive or when migrating from another platform, you can import hello database schema and data from a [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file.</span></span> <span data-ttu-id="690b4-105">ZIP dosyası BACPAC hello meta verileri ve SQL Server veritabanından veri içeren bir uzantıya sahip bir BACPAC dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="690b4-105">A BACPAC file is a ZIP file with an extension of BACPAC containing hello metadata and data from a SQL Server database.</span></span> <span data-ttu-id="690b4-106">Bir BACPAC dosyası (yalnızca standart depolama) Azure blob depolama alanından içeri aktarılabilir veya bir şirket içi konumda yerel depolama.</span><span class="sxs-lookup"><span data-stu-id="690b4-106">A BACPAC file can be imported from Azure blob storage (standard storage only) or from local storage in an on-premises location.</span></span> <span data-ttu-id="690b4-107">toomaximize hello alma hızı, daha yüksek Hizmet katmanını ve performans düzeyi, bir P6 gibi belirtin ve hello içeri aktarma başarılı olduktan sonra uygun şekilde toodown ölçeklendirme öneririz.</span><span class="sxs-lookup"><span data-stu-id="690b4-107">toomaximize hello import speed, we recommend that you specify a higher service tier and performance level, such as a P6, and then scale toodown as appropriate after hello import is successful.</span></span> <span data-ttu-id="690b4-108">Ayrıca, hello veritabanı uyumluluk düzeyi hello içe aktarmadan sonra hello uyumluluk düzeyi hello kaynak veritabanı üzerinde temel alır.</span><span class="sxs-lookup"><span data-stu-id="690b4-108">Also, hello database compatibility level after hello import is based on hello compatibility level of hello source database.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="690b4-109">SQL veritabanı, veritabanı tooAzure geçirdikten sonra geçerli uyumluluk düzeyinde (düzey 100 hello AdventureWorks2008R2 veritabanı için) veya daha yüksek düzeyde toooperate hello veritabanı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="690b4-109">After you migrate your database tooAzure SQL Database, you can choose toooperate hello database at its current compatibility level (level 100 for hello AdventureWorks2008R2 database) or at a higher level.</span></span> <span data-ttu-id="690b4-110">Merhaba etkileri ve belirli bir uyumluluk düzeyinde bir veritabanı işletim seçenekleri hakkında daha fazla bilgi için bkz: [ALTER veritabanı uyumluluk düzeyi](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span><span class="sxs-lookup"><span data-stu-id="690b4-110">For more information on hello implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span></span> <span data-ttu-id="690b4-111">Ayrıca bkz. [ALTER veritabanı kapsamlı yapılandırma](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) toocompatibility düzeyleri ek veritabanı düzeyi ayarları hakkında bilgi için ilgili.</span><span class="sxs-lookup"><span data-stu-id="690b4-111">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related toocompatibility levels.</span></span>   >

> [!NOTE]
> <span data-ttu-id="690b4-112">tooimport BACPAC tooa yeni bir veritabanı, Azure SQL Database mantıksal sunucusu önce oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="690b4-112">tooimport a BACPAC tooa new database, you must first create an Azure SQL Database logical server.</span></span> <span data-ttu-id="690b4-113">SQLPackage, kullanarak nasıl toomigrate bir SQL Server veritabanı tooAzure SQL veritabanı gösteren bir öğretici için bkz: [SQL Server veritabanına geçirme](sql-database-migrate-your-sql-server-database.md)</span><span class="sxs-lookup"><span data-stu-id="690b4-113">For a tutorial showing you how toomigrate a SQL Server database tooAzure SQL Database using SQLPackage, see [Migrate a SQL Server Database](sql-database-migrate-your-sql-server-database.md)</span></span>
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a><span data-ttu-id="690b4-114">Azure portalını kullanarak bir BACPAC Dosyadan İçeri Aktar</span><span class="sxs-lookup"><span data-stu-id="690b4-114">Import from a BACPAC file using Azure portal</span></span>

<span data-ttu-id="690b4-115">Bu makalede hello kullanarak Azure blob storage'da depolanan bir BACPAC dosyasından bir Azure SQL veritabanı oluşturma için yönergeler sağlanmaktadır [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="690b4-115">This article provides directions for creating an Azure SQL database from a BACPAC file stored in Azure blob storage using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="690b4-116">Azure blob depolama alanından bir BACPAC dosyasını içeri Hello yalnızca Azure portal kullanarak içe destekler.</span><span class="sxs-lookup"><span data-stu-id="690b4-116">Import using hello Azure portal only supports importing a BACPAC file from Azure blob storage.</span></span>

<span data-ttu-id="690b4-117">kullanarak bir veritabanı tooimport hello Azure portalı, açık hello sayfasını tıklatın ve veritabanı için **alma** hello araç.</span><span class="sxs-lookup"><span data-stu-id="690b4-117">tooimport a database using hello Azure portal, open hello page for your database and click **Import** on hello toolbar.</span></span> <span data-ttu-id="690b4-118">Merhaba depolama hesabı ve kapsayıcı belirtin ve tooimport istediğiniz hello BACPAC dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="690b4-118">Specify hello storage account and container, and select hello BACPAC file you want tooimport.</span></span> <span data-ttu-id="690b4-119">Merhaba hello yeni veritabanı boyutunu seçin (genellikle aynı kaynak ' hello) ve hello hedef SQL Server kimlik bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="690b4-119">Select hello size of hello new database (usually hello same as origin) and provide hello destination SQL Server credentials.</span></span>  

   ![Veritabanını içeri aktarma](./media/sql-database-import/import.png)

<span data-ttu-id="690b4-121">Merhaba toomonitor hello ilerlemesini içeri aktarma işlemi, içeri aktarılan hello mantıksal sunucu içeren hello veritabanı için başlangıç sayfasını açın.</span><span class="sxs-lookup"><span data-stu-id="690b4-121">toomonitor hello progress of hello import operation, open hello page for hello logical server containing hello database being imported.</span></span> <span data-ttu-id="690b4-122">Çok ilerleyin**Operations** ve ardından **içeri/dışarı aktarma** geçmişi.</span><span class="sxs-lookup"><span data-stu-id="690b4-122">Scroll down too**Operations** and then click **Import/Export** history.</span></span>

### <a name="monitor-hello-progress-of-an-import-operation"></a><span data-ttu-id="690b4-123">İzleyici hello işlem ilerleme durumunu alma</span><span class="sxs-lookup"><span data-stu-id="690b4-123">Monitor hello progress of an import operation</span></span>

<span data-ttu-id="690b4-124">Merhaba toomonitor hello ilerlemesini içeri aktarma işlemi, içeri hangi hello veritabanı içeri aktarılan hello mantıksal sunucu için başlangıç sayfasını açın.</span><span class="sxs-lookup"><span data-stu-id="690b4-124">toomonitor hello progress of hello import operation, open hello page for hello logical server into which hello database is being imported imported.</span></span> <span data-ttu-id="690b4-125">Çok ilerleyin**Operations** ve ardından **içeri/dışarı aktarma** geçmişi.</span><span class="sxs-lookup"><span data-stu-id="690b4-125">Scroll down too**Operations** and then click **Import/Export** history.</span></span>
   
   <span data-ttu-id="690b4-126">![Alma](./media/sql-database-import/import-history.png) ![alma durumu](./media/sql-database-import/import-status.png)</span><span class="sxs-lookup"><span data-stu-id="690b4-126">![import](./media/sql-database-import/import-history.png) ![import status](./media/sql-database-import/import-status.png)</span></span>

<span data-ttu-id="690b4-127">tooverify hello veritabanı hello sunucuda canlı, tıklatın **SQL veritabanları** ve hello yeni veritabanı doğrulamanız **çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="690b4-127">tooverify hello database is live on hello server, click **SQL databases** and verify hello new database is **Online**.</span></span>

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a><span data-ttu-id="690b4-128">SQLPackage kullanarak bir BACPAC Dosyadan İçeri Aktar</span><span class="sxs-lookup"><span data-stu-id="690b4-128">Import from a BACPAC file using SQLPackage</span></span>

<span data-ttu-id="690b4-129">tooimport bir SQL veritabanı hello kullanarak [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) komut satırı yardımcı programı, bkz: [alma parametreleri ve özellikleri](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span><span class="sxs-lookup"><span data-stu-id="690b4-129">tooimport a SQL database using hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Import parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span></span> <span data-ttu-id="690b4-130">Merhaba SQLPackage yardımcı programı hello en son sürümleri ile birlikte gelen [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) ve [SQL Server veri araçları Visual Studio için](https://msdn.microsoft.com/library/mt204009.aspx), veya hello en son sürümünü indirebilirsiniz [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) hello doğrudan Microsoft İndirme Merkezinden.</span><span class="sxs-lookup"><span data-stu-id="690b4-130">hello SQLPackage utility ships with hello latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download hello latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from hello Microsoft download center.</span></span>

<span data-ttu-id="690b4-131">Ölçek ve performans çoğu üretim ortamlarında için hello SQLPackage yardımcı programı hello kullanılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="690b4-131">We recommend hello use of hello SQLPackage utility for scale and performance in most production environments.</span></span> <span data-ttu-id="690b4-132">BACPAC dosyalarını kullanarak bir SQL Server Müşteri danışma ekibi blogu geçirme hakkında bkz [SQL BACPAC dosyalarını kullanarak veritabanını SQL Server tooAzure geçiş](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span><span class="sxs-lookup"><span data-stu-id="690b4-132">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

<span data-ttu-id="690b4-133">SQLPackage komutu nasıl için bir komut dosyası örneği için aşağıdaki hello bkz tooimport hello **AdventureWorks2008R2** adlı yerel depolama tooan Azure SQL Database mantıksal sunucusu, veritabanından **mynewserver20170403** Bu örnekte.</span><span class="sxs-lookup"><span data-stu-id="690b4-133">See hello following SQLPackage command for a script example for how tooimport hello **AdventureWorks2008R2** database from local storage tooan Azure SQL Database logical server, called **mynewserver20170403** in this example.</span></span> <span data-ttu-id="690b4-134">Bu komut dosyası olarak adlandırılan yeni bir veritabanı hello oluşturulmasını gösterir **myMigratedDatabase**, bir hizmet katmanını ile **Premium**ve bir hizmet amacını **P6**.</span><span class="sxs-lookup"><span data-stu-id="690b4-134">This script shows hello creation of a new database called **myMigratedDatabase**, with a service tier of **Premium**, and a Service Objective of **P6**.</span></span> <span data-ttu-id="690b4-135">Bu değerleri uygun tooyour ortamı olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="690b4-135">Change these values as appropriate tooyour environment.</span></span>

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![sqlpackage alma](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> <span data-ttu-id="690b4-137">Azure SQL Veritabanı mantıksal sunucusu 1433 numaralı bağlantı noktasında dinler.</span><span class="sxs-lookup"><span data-stu-id="690b4-137">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="690b4-138">Tooconnect tooan Azure SQL Database mantıksal sunucudan kurumsal bir güvenlik duvarı içinde çalışıyorsanız, toosuccessfully bağlanmak için bu bağlantı noktası hello Kurumsal Güvenlik Duvarı'nda açık olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="690b4-138">If you are attempting tooconnect tooan Azure SQL Database logical server from within a corporate firewall, this port must be open in hello corporate firewall for you toosuccessfully connect.</span></span>
>

<span data-ttu-id="690b4-139">Bu örnekte gösterilir nasıl SqlPackage.exe Active Directory Evrensel kimlik doğrulaması ile kullanarak veritabanını bir tooimport:</span><span class="sxs-lookup"><span data-stu-id="690b4-139">This example shows how tooimport a database using SqlPackage.exe with Active Directory Universal Authentication:</span></span>

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a><span data-ttu-id="690b4-140">PowerShell kullanarak bir BACPAC Dosyadan İçeri Aktar</span><span class="sxs-lookup"><span data-stu-id="690b4-140">Import from a BACPAC file using PowerShell</span></span>

<span data-ttu-id="690b4-141">Kullanım hello [yeni AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet toosubmit bir içeri aktarma veritabanı isteği toohello Azure SQL veritabanı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="690b4-141">Use hello [New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet toosubmit an import database request toohello Azure SQL Database service.</span></span> <span data-ttu-id="690b4-142">Veritabanınızı Hello boyutuna bağlı olarak, bazı zaman toocomplete hello içeri aktarma işlemi sürebilir.</span><span class="sxs-lookup"><span data-stu-id="690b4-142">Depending on hello size of your database, hello import operation may take some time toocomplete.</span></span>

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

<span data-ttu-id="690b4-143">Merhaba toocheck hello durumu isteği alma, hello kullan [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="690b4-143">toocheck hello status of hello import request, use hello [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span></span> <span data-ttu-id="690b4-144">Bu hemen sonra hello çalıştığını istek genellikle döndürür **durumu: devam ediyor**.</span><span class="sxs-lookup"><span data-stu-id="690b4-144">Running this immediately after hello request usually returns **Status: InProgress**.</span></span> <span data-ttu-id="690b4-145">Gördüğünüzde **durumu: başarılı** hello alma tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="690b4-145">When you see **Status: Succeeded** hello import is complete.</span></span>

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
<span data-ttu-id="690b4-146">Başka bir komut dosyası örneği için bkz: [bir BACPAC dosyadan bir veritabanı](scripts/sql-database-import-from-bacpac-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="690b4-146">For another script example, see [Import a database from a BACPAC file](scripts/sql-database-import-from-bacpac-powershell.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="690b4-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="690b4-147">Next steps</span></span>
* <span data-ttu-id="690b4-148">toolearn tooconnect tooand sorgu nasıl içeri aktarılan bir SQL veritabanı bkz [tooSQL veritabanı SQL Server Management Studio ile bağlanma ve örnek T-SQL sorgusu gerçekleştirmeyi](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="690b4-148">toolearn how tooconnect tooand query an imported SQL Database, see [Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>
* <span data-ttu-id="690b4-149">BACPAC dosyalarını kullanarak bir SQL Server Müşteri danışma ekibi blogu geçirme hakkında bkz [SQL BACPAC dosyalarını kullanarak veritabanını SQL Server tooAzure geçiş](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span><span class="sxs-lookup"><span data-stu-id="690b4-149">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>
* <span data-ttu-id="690b4-150">Performans önerileri dahil olmak üzere hello tüm SQL Server veritabanı geçiş işlemi, bir tartışma için bkz [bir SQL Server veritabanı tooAzure SQL veritabanı geçiş](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="690b4-150">For a discussion of hello entire SQL Server database migration process, including performance recommendations, see [Migrate a SQL Server database tooAzure SQL Database](sql-database-cloud-migrate.md).</span></span>



