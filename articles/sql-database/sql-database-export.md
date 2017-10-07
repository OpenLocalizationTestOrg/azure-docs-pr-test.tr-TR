---
title: "bir Azure SQL veritabanı tooa BACPAC dosyası aaaExport | Microsoft Docs"
description: "Hello Azure Portal kullanarak Azure SQL veritabanı tooa BACPAC dosyası dışarı aktarma"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 41d63a97-37db-4e40-b652-77c2fd1c09b7
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: cb3b4227318e0fd2114529c86c9792615fe7fd1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-sql-database-tooa-bacpac-file"></a>Bir Azure SQL veritabanı tooa BACPAC dosyası dışarı aktarma

Taşıma tooanother platform veya arşivleme için tooexport bir veritabanı gerektiğinde Merhaba veritabanı şeması ve verisi tooa verebilirsiniz [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) dosya. ZIP dosyası BACPAC hello meta verileri ve SQL Server veritabanından veri içeren bir uzantıya sahip bir BACPAC dosyasıdır. Bir BACPAC dosyayı Azure blob depolama veya bir şirket içi konumda yerel depolama depolanır ve daha sonra geri Azure SQL Database veya SQL Server içi yükleme içe. 

> [!IMPORTANT] 
> Azure SQL veritabanı otomatik dışarı aktarma 1 Mart 2017 üzerinde devre dışı bırakılan. Kullanabileceğiniz [uzun vadeli yedekleme bekletme](sql-database-long-term-retention.md
) veya [Azure Otomasyonu](https://github.com/Microsoft/azure-docs-pr/blob/2461f706f8fc1150e69312098640c0676206a531/articles/automation/automation-intro.md) tercih ettiğiniz tooa zamanlamaya göre PowerShell kullanarak tooperiodically arşiv SQL veritabanları. Bir örnek için hello karşıdan [PowerShell Betiği örnek](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export) github'dan.
>

## <a name="considerations-when-exporting-an-azure-sql-database"></a>Azure SQL veritabanını dışa aktarma ilgili önemli noktalar

* Bir dışarı aktarma için toobe sağlamanız hiçbir yazma etkinliği hello dışa aktarma sırasında oluştuğunu, veya, işlemsel olarak tutarlı vermekte gelen bir [işlemsel olarak tutarlı kopyalama](sql-database-copy.md) Azure SQL veritabanınızın.
* Tooblob depolama veriyorsanız hello bir BACPAC dosyasının en büyük boyutu 200 GB'dir. tooarchive daha büyük bir BACPAC dosyası toolocal depolama verin.
* Bu makalede açıklanan hello yöntemleri kullanarak bir BACPAC dosya tooAzure premium depolama verme desteklenmiyor.
* Azure SQL veritabanından Hello dışa aktarma işlemi 20 saat aşarsa, iptal edilebilir. dışa aktarma sırasında tooincrease performansı, şunları yapabilirsiniz:
  * Geçici olarak hizmet düzeyini artırın.
  * Tüm okuma ve etkinlik hello dışa aktarma sırasında yazma kesildi.
  * Kullanım bir [kümelenmiş dizin](https://msdn.microsoft.com/library/ms190457.aspx) tüm büyük tablolarda null olmayan değerler ile. 6-12 saatten daha uzun sürerse, kümelenmiş dizinler bir dışarı aktarma başarısız olabilir. Merhaba dışarı aktarma hizmeti toocomplete bir tarama tootry tooexport tüm tablo gerektiğinden budur. Dışarı aktarma toorun için tablolarınızı en iyi duruma getirilir, en iyi yolu toodetermine **DBCC SHOW_STATISTICS** ve o hello emin olun *RANGE_HI_KEY* null olmayan ve iyi dağıtım onun değerine sahiptir. Ayrıntılar için bkz [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/ms174384.aspx).

> [!NOTE]
> BACPACs yedekleme ve geri yükleme işlemleri için kullanılan hedeflenen toobe değildir. Azure SQL veritabanı yedeklemeleri her kullanıcı veritabanı için otomatik olarak oluşturur. Ayrıntılar için bkz [iş Sürekliliğine genel bakış](sql-database-business-continuity.md) ve [SQL veritabanı yedeklemeleri](sql-database-automated-backups.md).  
> 

## <a name="export-tooa-bacpac-file-using-hello-azure-portal"></a>Hello Azure portal kullanarak tooa BACPAC dosyasını dışarı aktarma

kullanarak bir veritabanı tooexport hello [Azure portal](https://portal.azure.com), veritabanınız için başlangıç sayfasını açın ve tıklayın **verme** hello araç çubuğunda. Merhaba BACPAC dosya adı belirtin, hello Azure depolama hesabı ve kapsayıcı hello dışa aktarma için sağlayabilir ve hello kimlik bilgileri tooconnect toohello kaynak veritabanı sağlar.  

![Veritabanı dışarı aktarma](./media/sql-database-export/database-export.png)

Merhaba toomonitor hello ilerlemesini dışarı aktarma işlemi, dışarı aktarılan hello mantıksal sunucu içeren hello veritabanı için başlangıç sayfasını açın. Çok ilerleyin**Operations** ve ardından **içeri/dışarı aktarma** geçmişi.

![dışarı aktarma geçmişi](./media/sql-database-export/export-history.png)
![dışa aktarma geçmişi durumu](./media/sql-database-export/export-history2.png)

## <a name="export-tooa-bacpac-file-using-hello-sqlpackage-utility"></a>Merhaba SQLPackage yardımcı programını kullanarak tooa BACPAC dosyasını dışarı aktarma

tooexport bir SQL veritabanı hello kullanarak [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) komut satırı yardımcı programı, bkz: [verme parametreleri ve özellikleri](https://msdn.microsoft.com/library/hh550080.aspx#Export Parameters and Properties). Merhaba SQLPackage yardımcı programı hello en son sürümleri ile birlikte gelen [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) ve [SQL Server veri araçları Visual Studio için](https://msdn.microsoft.com/library/mt204009.aspx), veya hello en son sürümünü indirebilirsiniz [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) hello doğrudan Microsoft İndirme Merkezinden.

Ölçek ve performans çoğu üretim ortamlarında için hello SQLPackage yardımcı programı hello kullanılması önerilir. BACPAC dosyalarını kullanarak bir SQL Server Müşteri danışma ekibi blogu geçirme hakkında bkz [SQL BACPAC dosyalarını kullanarak veritabanını SQL Server tooAzure geçiş](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

Bu örnekte gösterilir nasıl SqlPackage.exe Active Directory Evrensel kimlik doğrulaması ile kullanarak veritabanını bir tooexport:

```cmd
SqlPackage.exe /a:Export /tf:testExport.bacpac /scs:"Data Source=apptestserver.database.windows.net;Initial Catalog=MyDB;" /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="export-tooa-bacpac-file-using-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS) kullanarak tooa BACPAC dosyasını dışarı aktarma

Merhaba en yeni SQL Server Management Studio sürümleri Sihirbazı tooexport bir Azure SQL veritabanı tooa BACPAC dosyası da sağlar. Merhaba bkz [bir veri katmanı uygulaması verme](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application).

## <a name="export-tooa-bacpac-file-using-powershell"></a>PowerShell kullanarak tooa BACPAC dosyasını dışarı aktarma

Kullanım hello [yeni AzureRmSqlDatabaseExport](/powershell/module/azurerm.sql/new-azurermsqldatabaseexport) cmdlet toosubmit bir dışarı aktarma veritabanı isteği toohello Azure SQL veritabanı hizmeti. Veritabanınızı Hello boyutuna bağlı olarak, bazı zaman toocomplete hello dışa aktarma işlemi sürebilir.

 ```powershell
 $exportRequest = New-AzureRmSqlDatabaseExport -ResourceGroupName $ResourceGroupName -ServerName $ServerName `
   -DatabaseName $DatabaseName -StorageKeytype $StorageKeytype -StorageKey $StorageKey -StorageUri $BacpacUri `
   -AdministratorLogin $creds.UserName -AdministratorLoginPassword $creds.Password
 ```

Merhaba toocheck hello durumu dışarı aktarma isteği, hello kullan [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet'i. Bu hemen sonra hello çalıştığını istek genellikle döndürür **durumu: devam ediyor**. Gördüğünüzde **durumu: başarılı** hello verme işlemi tamamlandı.

```powershell
$exportStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $exportRequest.OperationStatusLink
[Console]::Write("Exporting")
while ($exportStatus.Status -eq "InProgress")
{
    $exportStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $exportRequest.OperationStatusLink
    [Console]::Write(".")
    Start-Sleep -s 10
}
[Console]::WriteLine("")
$exportStatus
```

## <a name="next-steps"></a>Sonraki adımlar

* toolearn alternatif bir tooexported arşiv amaçlar için bir veritabanı olarak bir Azure SQL Veritabanı yedeğinin uzun vadeli yedekleme bekletme hakkında bkz [uzun vadeli yedekleme bekletme](sql-database-long-term-retention.md).
- BACPAC dosyalarını kullanarak bir SQL Server Müşteri danışma ekibi blogu geçirme hakkında bkz [SQL BACPAC dosyalarını kullanarak veritabanını SQL Server tooAzure geçiş](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* bir BACPAC tooa SQL Server veritabanını içeri aktarma hakkında toolearn bkz [BACPCAC tooa SQL Server veritabanı alma](https://msdn.microsoft.com/library/hh710052.aspx).
* bir SQL Server veritabanından bir BACPAC verme hakkında toolearn bkz [bir veri katmanı uygulaması verme](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application) ve [ilk veritabanınızı geçirin](sql-database-migrate-your-sql-server-database.md).
* Prelude toomigration tooAzure SQL veritabanı SQL Server'dan dışarı aktarıyorsanız, bkz: [bir SQL Server veritabanı tooAzure SQL veritabanı geçiş](sql-database-cloud-migrate.md).
