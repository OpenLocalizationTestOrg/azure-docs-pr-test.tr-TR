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
# <a name="import-a-bacpac-file-tooa-new-azure-sql-database"></a>Bir BACPAC dosya tooa alma yeni Azure SQL veritabanı

Ne zaman tooimport bir arşiv veritabanından gerekir ya da başka bir platformundan geçirilirken hello veritabanı şemasını ve verileri içeri aktarabilirsiniz bir [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) dosya. ZIP dosyası BACPAC hello meta verileri ve SQL Server veritabanından veri içeren bir uzantıya sahip bir BACPAC dosyasıdır. Bir BACPAC dosyası (yalnızca standart depolama) Azure blob depolama alanından içeri aktarılabilir veya bir şirket içi konumda yerel depolama. toomaximize hello alma hızı, daha yüksek Hizmet katmanını ve performans düzeyi, bir P6 gibi belirtin ve hello içeri aktarma başarılı olduktan sonra uygun şekilde toodown ölçeklendirme öneririz. Ayrıca, hello veritabanı uyumluluk düzeyi hello içe aktarmadan sonra hello uyumluluk düzeyi hello kaynak veritabanı üzerinde temel alır. 

> [!IMPORTANT] 
> SQL veritabanı, veritabanı tooAzure geçirdikten sonra geçerli uyumluluk düzeyinde (düzey 100 hello AdventureWorks2008R2 veritabanı için) veya daha yüksek düzeyde toooperate hello veritabanı seçebilirsiniz. Merhaba etkileri ve belirli bir uyumluluk düzeyinde bir veritabanı işletim seçenekleri hakkında daha fazla bilgi için bkz: [ALTER veritabanı uyumluluk düzeyi](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level). Ayrıca bkz. [ALTER veritabanı kapsamlı yapılandırma](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) toocompatibility düzeyleri ek veritabanı düzeyi ayarları hakkında bilgi için ilgili.   >

> [!NOTE]
> tooimport BACPAC tooa yeni bir veritabanı, Azure SQL Database mantıksal sunucusu önce oluşturmanız gerekir. SQLPackage, kullanarak nasıl toomigrate bir SQL Server veritabanı tooAzure SQL veritabanı gösteren bir öğretici için bkz: [SQL Server veritabanına geçirme](sql-database-migrate-your-sql-server-database.md)
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a>Azure portalını kullanarak bir BACPAC Dosyadan İçeri Aktar

Bu makalede hello kullanarak Azure blob storage'da depolanan bir BACPAC dosyasından bir Azure SQL veritabanı oluşturma için yönergeler sağlanmaktadır [Azure portal](https://portal.azure.com). Azure blob depolama alanından bir BACPAC dosyasını içeri Hello yalnızca Azure portal kullanarak içe destekler.

kullanarak bir veritabanı tooimport hello Azure portalı, açık hello sayfasını tıklatın ve veritabanı için **alma** hello araç. Merhaba depolama hesabı ve kapsayıcı belirtin ve tooimport istediğiniz hello BACPAC dosyasını seçin. Merhaba hello yeni veritabanı boyutunu seçin (genellikle aynı kaynak ' hello) ve hello hedef SQL Server kimlik bilgilerini sağlayın.  

   ![Veritabanını içeri aktarma](./media/sql-database-import/import.png)

Merhaba toomonitor hello ilerlemesini içeri aktarma işlemi, içeri aktarılan hello mantıksal sunucu içeren hello veritabanı için başlangıç sayfasını açın. Çok ilerleyin**Operations** ve ardından **içeri/dışarı aktarma** geçmişi.

### <a name="monitor-hello-progress-of-an-import-operation"></a>İzleyici hello işlem ilerleme durumunu alma

Merhaba toomonitor hello ilerlemesini içeri aktarma işlemi, içeri hangi hello veritabanı içeri aktarılan hello mantıksal sunucu için başlangıç sayfasını açın. Çok ilerleyin**Operations** ve ardından **içeri/dışarı aktarma** geçmişi.
   
   ![Alma](./media/sql-database-import/import-history.png) ![alma durumu](./media/sql-database-import/import-status.png)

tooverify hello veritabanı hello sunucuda canlı, tıklatın **SQL veritabanları** ve hello yeni veritabanı doğrulamanız **çevrimiçi**.

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a>SQLPackage kullanarak bir BACPAC Dosyadan İçeri Aktar

tooimport bir SQL veritabanı hello kullanarak [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) komut satırı yardımcı programı, bkz: [alma parametreleri ve özellikleri](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties). Merhaba SQLPackage yardımcı programı hello en son sürümleri ile birlikte gelen [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) ve [SQL Server veri araçları Visual Studio için](https://msdn.microsoft.com/library/mt204009.aspx), veya hello en son sürümünü indirebilirsiniz [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) hello doğrudan Microsoft İndirme Merkezinden.

Ölçek ve performans çoğu üretim ortamlarında için hello SQLPackage yardımcı programı hello kullanılması önerilir. BACPAC dosyalarını kullanarak bir SQL Server Müşteri danışma ekibi blogu geçirme hakkında bkz [SQL BACPAC dosyalarını kullanarak veritabanını SQL Server tooAzure geçiş](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

SQLPackage komutu nasıl için bir komut dosyası örneği için aşağıdaki hello bkz tooimport hello **AdventureWorks2008R2** adlı yerel depolama tooan Azure SQL Database mantıksal sunucusu, veritabanından **mynewserver20170403** Bu örnekte. Bu komut dosyası olarak adlandırılan yeni bir veritabanı hello oluşturulmasını gösterir **myMigratedDatabase**, bir hizmet katmanını ile **Premium**ve bir hizmet amacını **P6**. Bu değerleri uygun tooyour ortamı olarak değiştirin.

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![sqlpackage alma](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> Azure SQL Veritabanı mantıksal sunucusu 1433 numaralı bağlantı noktasında dinler. Tooconnect tooan Azure SQL Database mantıksal sunucudan kurumsal bir güvenlik duvarı içinde çalışıyorsanız, toosuccessfully bağlanmak için bu bağlantı noktası hello Kurumsal Güvenlik Duvarı'nda açık olması gerekir.
>

Bu örnekte gösterilir nasıl SqlPackage.exe Active Directory Evrensel kimlik doğrulaması ile kullanarak veritabanını bir tooimport:

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a>PowerShell kullanarak bir BACPAC Dosyadan İçeri Aktar

Kullanım hello [yeni AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet toosubmit bir içeri aktarma veritabanı isteği toohello Azure SQL veritabanı hizmeti. Veritabanınızı Hello boyutuna bağlı olarak, bazı zaman toocomplete hello içeri aktarma işlemi sürebilir.

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

Merhaba toocheck hello durumu isteği alma, hello kullan [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet'i. Bu hemen sonra hello çalıştığını istek genellikle döndürür **durumu: devam ediyor**. Gördüğünüzde **durumu: başarılı** hello alma tamamlandı.

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
Başka bir komut dosyası örneği için bkz: [bir BACPAC dosyadan bir veritabanı](scripts/sql-database-import-from-bacpac-powershell.md).

## <a name="next-steps"></a>Sonraki adımlar
* toolearn tooconnect tooand sorgu nasıl içeri aktarılan bir SQL veritabanı bkz [tooSQL veritabanı SQL Server Management Studio ile bağlanma ve örnek T-SQL sorgusu gerçekleştirmeyi](sql-database-connect-query-ssms.md).
* BACPAC dosyalarını kullanarak bir SQL Server Müşteri danışma ekibi blogu geçirme hakkında bkz [SQL BACPAC dosyalarını kullanarak veritabanını SQL Server tooAzure geçiş](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* Performans önerileri dahil olmak üzere hello tüm SQL Server veritabanı geçiş işlemi, bir tartışma için bkz [bir SQL Server veritabanı tooAzure SQL veritabanı geçiş](sql-database-cloud-migrate.md).



