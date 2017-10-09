---
title: "Azure SQL veritabanını bir yedekten aaaRestore | Microsoft Docs"
description: "Çalışma zamanı (too35 gün) içinde bir Azure SQL veritabanı tooa önceki noktası tooroll geri sağlayan zaman içinde nokta geri yükleme hakkında hakkında bilgi edinin."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: fd1d334d-a035-4a55-9446-d1cf750d9cf7
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.openlocfilehash: 84ecc306a2072445c10dbf1e9d7cf3d1b43860cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="recover-an-azure-sql-database-using-automated-database-backups"></a>Otomatik veritabanı yedeklerini kullanarak bir Azure SQL veritabanını kurtarma
SQL veritabanı kullanarak veritabanı kurtarma için bu seçenekleri sağlar [veritabanı yedeklemeleri otomatik](sql-database-automated-backups.md) ve [uzun vadeli bekletme yedeklemeleri](sql-database-long-term-retention.md). Bir veritabanı yedeğinden geri yükleyebilirsiniz:

* Aynı mantıksal sunucu kurtarılan hello üzerinde yeni bir veritabanı tooa süre hello saklama dönemi içinde noktası belirtilmiş. 
* Bir veritabanı üzerinde hello aynı mantıksal sunucu kurtarılan toohello silme silinen bir veritabanını süredir.
* Tüm bölgelerdeki herhangi bir mantıksal sunucuda yeni bir veritabanı toohello noktası hello en son günlük yedeklerini coğrafi olarak çoğaltılmış blob depolama (RA-GRS) kurtarıldı.

> [!IMPORTANT]
> Varolan bir veritabanını geri yükleme sırasında üzerine yazılamıyor.
>

Aynı zamanda [veritabanı yedeklemeleri otomatik](sql-database-automated-backups.md) toocreate bir [veritabanı kopyalama](sql-database-copy.md) tüm bölgelerdeki herhangi bir mantıksal sunucuda. 

## <a name="recovery-time"></a>Kurtarma zamanı
Kurtarma zamanı toorestore otomatik veritabanı yedeklerini kullanarak bir veritabanı çeşitli faktörler tarafından etkilenir hello: 

* Merhaba veritabanının Hello boyutu
* Merhaba veritabanının Hello performans düzeyi
* İşlem günlükleri söz konusu Hello sayısı
* toorecover toohello geri yükleme noktası toobe gereken etkinlik Hello miktarı yeniden
* Merhaba ağ bant genişliği Hello geri tooa farklı bir bölgeye ise 
* Merhaba hello hedef bölgede işlenmekte olan eşzamanlı geri yükleme isteği sayısı. 
  
  Çok büyük ve/veya etkin veritabanı için hello geri yükleme birkaç saat sürebilir. Bir bölgede uzun süren kesinti ise, çok sayıda coğrafi geri yükleme isteği ülkeler tarafından işlenmekte olan mümkündür. Birçok istek olduğunda, bu bölgedeki veritabanları için hello kurtarma süresini artırabilir. Çoğu veritabanı 12 saat içinde tam geri yükler.
  
Hiçbir yerleşik işlevsellik toodo toplu geri yükleme yoktur. Merhaba [Azure SQL Database: tam sunucu kurtarma](https://gallery.technet.microsoft.com/Azure-SQL-Database-Full-82941666) komut dosyası bu görevi gerçekleştirmeye bir yolu bir örnektir.

> [!IMPORTANT]
> yedeklemeleri toorecover kullanarak otomatikleştirilmiş, hello SQL Server katkıda bulunan rolü hello Abonelikteki bir üyesi olmanız veya hello abonelik sahibi olmanız gerekir. Hello Azure portal, PowerShell veya hello REST API kullanarak kurtarabilirsiniz. Transact-SQL kullanamazsınız. 
> 

## <a name="point-in-time-restore"></a>Zaman içinde nokta geri yükleme

Varolan bir veritabanını geri tooan önceki tarihli noktaya hello üzerinde yeni bir veritabanı olarak aynı mantıksal sunucu kullanarak hello Azure portal [PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/restore-azurermsqldatabase), veya hello [REST API](https://msdn.microsoft.com/library/azure/mt163685.aspx). 

> [!TIP]
> Tooperform zaman içinde nokta geri yükleme bir veritabanının nasıl görürüm gösteren bir örnek PowerShell komut dosyası için [PowerShell kullanarak bir SQL veritabanını geri](scripts/sql-database-restore-database-powershell.md).
>

Merhaba veritabanının geri yüklenen tooany hizmet katmanı veya performans düzeyi ve tek veritabanı olarak veya bir esnek havuz içine olabilir. Merhaba mantıksal sunucuda yeterli kaynaklara sahip veya hello esnek havuz toowhich hello veritabanı geri yüklediğinizden emin olun. Tamamlandıktan sonra geri hello normal, tamamen erişilebilir, çevrimiçi bir veritabanı veritabanıdır. kendi hizmet katmanını ve performans düzeyi temelinde normal hızlarında geri hello veritabanı ücretlendirilir. Merhaba veritabanı geri yükleme işlemi tamamlanana kadar ücrete tabi değildir.

Genellikle bir veritabanı tooan geri daha önce kurtarma amacıyla gelin. Kabul bunu yaparken hello yerini alacak yeni bir hello özgün veritabanı için veritabanı geri veya tooretrieve verilerden kullanın ve ardından hello özgün veritabanı güncelleştirin. 

* ***Veritabanı değiştirme:*** geri hello veritabanı hello özgün veritabanı için bir yedek olarak amaçlanıyorsa hello performans düzeyi doğrulamanız gerekir ve/veya hizmet katmanı uygundur ve gerekirse hello veritabanı ölçeklendirme. Hello özgün veritabanını yeniden adlandırın ve ardından hello ALTER DATABASE komutu T-SQL kullanarak geri hello veritabanı hello özgün adı verin. 
* ***Veri kurtarma:*** , bir kullanıcı veya uygulama hatadan geri hello veritabanı toorecover tooretrieve verilerden düşünüyorsanız, toowrite gerekir ve hello gerekli veri kurtarma betikleri tooextract veri geri hello veritabanı toohello yürütme özgün veritabanı. Uzun süre toocomplete Hello geri yükleme işlemi devam edebilir ancak veritabanını geri yükleme hello hello geri yükleme işlemi boyunca hello veritabanı listesinde görünür olur. Hello geri yükleme sırasında hello veritabanı silerseniz hello geri yükleme işlemi iptal edilir ve hello geri yükleme tamamlanmadı hello veritabanı için sizden ücret istenmese. 

### <a name="azure-portal"></a>Azure portalına

zaman kullanarak toorecover tooa noktası hello Azure portalı, açık hello sayfasını tıklatın ve veritabanı için **geri** hello araç.

![noktası içinde zaman geri yükleme](./media/sql-database-recovery-using-backups/point-in-time-recovery.png)

## <a name="deleted-database-restore"></a>Silinen bir veritabanını geri yükleme
Silinen bir veritabanını toohello silme süresi geri hello silinmiş bir veritabanı için kullanarak aynı mantıksal sunucu hello Azure portal [PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/restore-azurermsqldatabase), veya hello [REST (createMode = geri yükle)](https://msdn.microsoft.com/library/azure/mt163685.aspx). 

> [!TIP]
> Toorestore silinen bir veritabanını nasıl görürüm gösteren bir örnek PowerShell komut dosyası [PowerShell kullanarak bir SQL veritabanını geri](scripts/sql-database-restore-database-powershell.md).
>

> [!IMPORTANT]
> Bir Azure SQL veritabanı sunucusu örneği silerseniz, tüm veritabanlarını da silinir ve kurtarılamaz. Şu anda silinen bir sunucuya geri yüklemek için destek yok.
> 

### <a name="azure-portal"></a>Azure portalına

toorecover silinmiş sırasında veritabanı kendi [saklama dönemi](sql-database-service-tiers.md) hello Azure portal, sunucunuzun ve hello işlemleri alanında açık hello sayfası kullanarak **veritabanlarını sildi**.

![silinen-veritabanı-geri yükleme-1](./media/sql-database-recovery-using-backups/deleted-database-restore-1.png)


![silinen-veritabanı-geri yükleme-2](./media/sql-database-recovery-using-backups/deleted-database-restore-2.png)

## <a name="geo-restore"></a>Coğrafi Geri Yükleme
Bir SQL veritabanı herhangi bir Azure bölgesine herhangi bir sunucuda hello en son coğrafi olarak çoğaltılmış tam ve fark yedeklerden geri yükleyebilirsiniz. Coğrafi geri yükleme, coğrafi olarak yedekli bir yedekleme, kaynağı olarak kullanır ve hello veritabanı veya veri merkezi tooan kesilmesi erişilemez durumda olsa bile kullanılan toorecover bir veritabanı olabilir. 

Merhaba veritabanı barındırıldığı hello bölgede bir olay nedeniyle veritabanınızı kullanılamaz duruma geldiğinde coğrafi geri yükleme hello varsayılan kurtarma seçeneğidir. Büyük ölçekli olay varsa kullanılamazlık bölge sonuçlarında veritabanı uygulamanızın hello coğrafi olarak çoğaltılmış yedeklemeleri tooa sunucusundan başka bir bölgede bulunan bir veritabanını geri yükleyebilirsiniz. Ne zaman değişiklik yedeklemesi alınır ve coğrafi olarak çoğaltılmış tooan Azure olduğunda arasında bir gecikme olur blob farklı bir bölgede. Bu gecikme olabilir tooan saat, bu nedenle, olağanüstü bir durum oluşursa, olabilir tooone saat veri kaybı. Aşağıdaki çizimde hello hello veritabanı geri yükleme yedekten hello son kullanılabilir başka bir bölgede gösterir.

![coğrafi geri yükleme](./media/sql-database-geo-restore/geo-restore-2.png)

> [!TIP]
> Nasıl tooperform bir coğrafi geri yükleme, bkz: gösteren bir örnek PowerShell komut dosyası [PowerShell kullanarak bir SQL veritabanını geri](scripts/sql-database-restore-database-powershell.md).
> 

Zaman içinde nokta geri yükleme coğrafi ikincil şu anda desteklenmiyor. Zaman içinde nokta geri yükleme, yalnızca birincil veritabanı üzerinde gerçekleştirilebilir. Coğrafi geri yükleme toorecover kesintiden kullanma hakkında ayrıntılı bilgi için bkz: [bir kesintisinden kurtarma](sql-database-disaster-recovery.md).

> [!IMPORTANT]
> Kurtarma yedeklerden hello hello olağanüstü durum en temel olan kurtarma çözümleri SQL veritabanı ile kullanılabilir hello uzun RPO'ya ve tahmin kurtarma süresi (Ekle). Temel veritabanları kullanan çözümler için coğrafi geri yükleme sık bir makul DR 12 saatlik bir Ekle ile çözümüdür. Kısa kurtarma süreleri gerektiren büyük standart veya Premium veritabanlarının kullanan çözümler için kullanmayı düşünmelisiniz [aktif coğrafi çoğaltma](sql-database-geo-replication-overview.md). Aktif coğrafi çoğaltma, bir çok daha kısa RPO ve Ekle yalnızca gerektirir gibi sunar bir yük devretme tooa sürekli olarak çoğaltılmış ikincil başlatın. İş contiuity seçenekleri hakkında daha fazla bilgi için bkz: [iş sürekliliği üzerinden](sql-database-business-continuity.md).
> 

### <a name="azure-portal"></a>Azure portalına

toogeo geri yükleme sırasında veritabanı bir alt [saklama dönemi](sql-database-service-tiers.md) hello Azure portal kullanarak hello SQL veritabanları sayfasını açın ve ardından **Ekle**. Merhaba, **kaynak seçme** metin kutusunda seçin **yedekleme**. Hangi tooperform hello kurtarma Hello yedekten hello bölgede ve tercih ettiğiniz hello sunucuda belirtin. 

## <a name="programmatically-performing-recovery-using-automated-backups"></a>Program aracılığıyla otomatik yedekleme kullanarak kurtarma gerçekleştirme
Daha önce ele alındığı ayrıca toohello Azure portal, veritabanı kurtarma program aracılığıyla Azure PowerShell kullanarak gerçekleştirilebilir veya REST API hello. Merhaba tabloları aşağıdaki komutlar kullanılabilir hello kümesi açıklanmaktadır.

### <a name="powershell"></a>PowerShell
| Cmdlet | Açıklama |
| --- | --- |
| [Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase) |Bir veya daha fazla veritabanı alır. |
| [Get-AzureRMSqlDeletedDatabaseBackup](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | Geri yüklediğiniz silinen bir veritabanını alır. |
| [Get-AzureRmSqlDatabaseGeoBackup](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) |Coğrafi olarak yedekli bir veritabanının yedeğini alır. |
| [Geri yükleme-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) |Bir SQL veritabanını geri yükler. |
|  | |

### <a name="rest-api"></a>REST API
| API | Açıklama |
| --- | --- |
| [REST (createMode kurtarma =)](https://msdn.microsoft.com/library/azure/mt163685.aspx) |Bir veritabanını geri yükler |
| [Get oluştur veya veritabanı durumunu güncelleştir](https://msdn.microsoft.com/library/azure/mt643934.aspx) |Bir geri yükleme işlemi sırasında döndürür hello durumu |
|  | |

## <a name="summary"></a>Özet
Otomatik yedekleme, kullanıcı ve uygulama hataları, yanlışlıkla veritabanı silme ve uzun süren kesintileri veritabanlarınızı koruyun. Bu yerleşik yetenek tüm hizmet katmanları ve performans düzeyleri için kullanılabilir. 

## <a name="next-steps"></a>Sonraki adımlar
* İş sürekliliğine genel bakış ve senaryolar için bkz: [iş sürekliliğine genel bakış](sql-database-business-continuity.md)
* Azure SQL veritabanı otomatik yedeklemeler hakkında toolearn bakın [SQL veritabanı otomatik yedeklemeler](sql-database-automated-backups.md)
* uzun vadeli yedekleme bekletme hakkında toolearn bakın [uzun vadeli yedekleme bekletme](sql-database-long-term-retention.md)
* tooconfigure, yönetmek ve geri yükleme hello kullanarak bir Azure kurtarma Hizmetleri kasası Otomatik yedeklemelerin uzun vadeli bekletme Azure portal, bkz: [yapılandırma ve kullanım uzun vadeli yedekleme bekletme](sql-database-long-term-backup-retention-configure.md). 
* toolearn daha hızlı kurtarma seçenekleri hakkında bkz [aktif coğrafi çoğaltma](sql-database-geo-replication-overview.md)  
