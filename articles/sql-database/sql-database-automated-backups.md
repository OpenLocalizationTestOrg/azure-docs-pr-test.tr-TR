---
title: "Otomatik, coğrafi olarak yedekli aaaAzure SQL veritabanı yedeklemeleri | Microsoft Docs"
description: "SQL veritabanı otomatik olarak birkaç dakikada bir yerel veritabanı yedeği oluşturur ve coğrafi yedeklilik için Azure okuma erişimli coğrafi olarak yedekli depolama kullanır."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 3ee3d49d-16fa-47cf-a3ab-7b22aa491a8d
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 8aff5356e8142707dd7cd2533a4aa5ea8fec866d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-automatic-sql-database-backups"></a>Otomatik SQL veritabanını yedekleme hakkında bilgi edinin

SQL veritabanı otomatik olarak veritabanı yedeklerini oluşturur ve Azure okuma erişimli coğrafi olarak yedekli depolama (RA-GRS) tooprovide coğrafi yedeklilik kullanır. Bu yedeklemeler otomatik olarak ve ek ücret ödemeden oluşturulur. Toodo toomake bunları gerçekleşecek herhangi bir şey gerekmez. Verilerinizin yanlışlıkla Bozulması veya silme korumak için veritabanı yedeklemeleri tüm iş sürekliliği ve olağanüstü durum kurtarma stratejisi, önemli bir parçasıdır. Kendi depolama kapsayıcısı tookeep yedeklemeler istiyorsanız, uzun vadeli yedekleme bekletme ilkesi yapılandırabilirsiniz. Daha fazla bilgi için bkz. [Uzun süreli saklama](sql-database-long-term-retention.md).

## <a name="what-is-a-sql-database-backup"></a>Bir SQL veritabanı yedeği nedir?

SQL veritabanı kullanan SQL Server teknolojisini toocreate [tam](https://msdn.microsoft.com/library/ms186289.aspx), [fark](https://msdn.microsoft.com/library/ms175526.aspx), ve [işlem günlüğü](https://msdn.microsoft.com/library/ms191429.aspx) yedekler. Merhaba işlem günlüğü yedeklemeleri 5-10 dakikada hello performans düzeyi ve veritabanı etkinliği miktarı göre hello sıklık genellikle gerçekleşir. İşlem günlüğü yedeklemeleri, tam ve değişim yedeklemeleri toorestore veritabanı tooa belirli zaman içinde nokta toohello izin hello veritabanını barındıran aynı sunucu. Bir veritabanını geri yüklediğinizde, hizmet rakamları hangi tam, fark çıkışı hello ve işlem günlüğü yedeklemeleri geri toobe gerekir.


Bu yedeklemeler için kullanabilirsiniz:

* Bir veritabanı tooa noktası zaman hello saklama dönemi içinde geri yükleyin. Bu işlem hello yeni bir veritabanı oluşturacak hello özgün veritabanı ile aynı sunucu.
* Silinen bir veritabanını toohello birer silindi veya dilediğiniz zaman hello saklama dönemi içinde geri yükleyin. Silinen hello veritabanı yalnızca geri yükleyebilirsiniz hello hello özgün veritabanının oluşturulduğu aynı sunucu.
* Veritabanı tooanother coğrafi bölge geri yükleyin. Sunucu ve veritabanı erişemediğinde Bu, coğrafi bir olağanüstü durum gelen toorecover sağlar. Merhaba Dünya başka bir yerindeki varolan tüm Server'da yeni bir veritabanı oluşturur. 
* Bir veritabanı, Azure kurtarma Hizmetleri kasasında depolanan belirli bir yedekten geri yükleyin. Bu, toorestore hello veritabanı toosatisfy uyumluluk isteği eski bir sürümü ya da toorun hello uygulamanın eski bir sürümü sağlar. Bkz: [uzun vadeli bekletme](sql-database-long-term-retention.md).
* tooperform bir geri yükleme, bkz: [veritabanını yedeklerden geri](sql-database-recovery-using-backups.md).

> [!NOTE]
> Azure depolama alanında hello terim *çoğaltma* toocopying dosyaları tek bir konumda tooanother başvuruyor. SQL'in *veritabanı çoğaltması* tookeeping toomultiple ikincil veritabanları birincil veritabanı ile eşitlenen başvuruyor. 
> 

## <a name="how-much-backup-storage-is-included-at-no-cost"></a>Yedek depolama alanı miktarını hiçbir ücret bulunur?
SQL veritabanı en fazla sağlanan veritabanı deponuzda too200% hiçbir ek ücret ödemeden yedekleme depolama sağlar. Örneğin, bir standart DB örneğini sağlanan bir veritabanı boyutu ile 250 GB varsa ek ücret ödemeden 500 GB yedekleme depolama gerekir. Veritabanı yedekleme depolama sağlanan hello aşarsa, Azure desteği ile iletişim kurarak tooreduce hello saklama dönemi seçebilirsiniz. Toopay hello standart okuma erişimli coğrafi olarak yedekli depolama (RA-GRS) oranı faturalandırılır fazladan Yedekleme depolaması için başka bir seçenektir. 

## <a name="how-often-do-backups-happen"></a>Yedeklemelerin ne sıklıkta meydana?
Tam veritabanı yedeklemeleri, haftalık, artımlı veritabanı yedeklemeleri genellikle her birkaç saat ve işlem günlüğü yedeklemeleri genellikle 5-10 dakikada bir gerçekleşir durum gerçekleşir. hemen bir veritabanı oluşturulduktan sonra hello ilk tam yedeklemede zamanlanır. Genellikle 30 dakika içinde tamamlanır ancak hello veritabanı önemli boyutunu olduğunda uzun sürebilir. Örneğin, hello ilk yedekleme geri yüklenen veritabanı veya veritabanı kopyası üzerinde daha uzun sürebilir. Merhaba ilk tam yedeklemede sonra başka yedeklemelerinin de tümünü otomatik olarak zamanlanır ve hello arka planda sessizce yönetilen. tüm veritabanı yedeklemeleri tam zamanlamasını Hello hello genel dengeleyen gibi hello SQL veritabanı hizmeti tarafından belirlenen sistem iş yükü. 

Merhaba yedekleme depolama coğrafi çoğaltma hello Azure Storage çoğaltma zamanlamaya göre gerçekleşir.

## <a name="how-long-do-you-keep-my-backups"></a>Ne kadar süreyle yedeklerim tutarım?
Her SQL veritabanını yedekleme üzerinde hello dayalı bir bekletme dönemi içeren [hizmet katmanı](sql-database-service-tiers.md) hello veritabanı. bir veritabanında Hello saklama süresi:


* Temel hizmet katmanı 7 gündür.
* Standart hizmet katmanında 35 gün olur.
* Premium Hizmet katmanını 35 gün olur.

Merhaba standart veya Premium hizmet katmanları tooBasic veritabanınızdan düşürmek hello yedeklemeleri yedi gün için kaydedilir. Yedi günden eski tüm var olan yedekleri artık kullanılamaz. 

Merhaba temel hizmet katmanı tooStandard ya da Premium veritabanınızı yükseltirseniz, SQL veritabanı var olan yedekleri 35 gün kadar tutar. 35 gün boyunca oluşurken yeni yedeklemeler tutar.

Bir veritabanı silerseniz, SQL veritabanı hello yedeklemeleri hello tutar. aynı şekilde için çevrimiçi bir veritabanı gerekir. Örneğin, bir yedi günlük tutma süresine sahip bir temel veritabanı silme varsayalım. Dört gün önce yapılmışsa bir yedekleme için üç gün daha kaydedilir.

> [!IMPORTANT]
> SQL veritabanlarını barındıran hello Azure SQL server silerseniz toohello sunucu ait tüm veritabanlarının da silinir ve kurtarılamaz. Silinen bir sunucuya geri yükleyemezsiniz.
> 

## <a name="how-tooextend-hello-backup-retention-period"></a>Nasıl tooextend hello saklama dönemi yedekleme?
Uygulamanız hello yedeklemeleri uzun süre kullanılabilir gerektiriyorsa hello uzun vadeli yedekleme bekletme ilkesi tekil veritabanları (LTR İlkesi) yapılandırarak hello yerleşik saklama dönemi genişletebilirsiniz. Bu, tooextend hello yerleşik BT saklama dönemi 35 gün tooup too10 yılların sağlar. Daha fazla bilgi için bkz. [Uzun süreli saklama](sql-database-long-term-retention.md).

Azure portal veya API kullanarak hello LTR İlkesi tooa veritabanı eklediğinizde hello haftalık tam veritabanı yedeklemeleri otomatik olarak kopyalanan tooyour olur kendi Azure yedekleme hizmeti kasası. Veritabanınız ile şifrelenmişse TDE hello yedeklemeleri bekleyen otomatik olarak şifrelenir.  Merhaba Hizmetleri kasası, zaman damgası ve hello LTR İlkesi göre süresi dolan Yedeklerinizin otomatik olarak silecektir.  Sizin için toomanage hello yedekleme zamanlamasını veya hello temizlenmesi endişe eski dosyaları hello. Merhaba kasa içinde olduğu sürece hello depolanan yedeklerini kasa hello geri yükleme API destekler, SQL veritabanını aynı abonelik hello. Bu yedeklemeler hello Azure portal veya PowerShell tooaccess kullanabilirsiniz.

> [!TIP]
> Bir nasıl tooguide için bkz: [yapılandırma ve Azure SQL veritabanı uzun vadeli yedekleme bekletme geri yükleme](sql-database-long-term-backup-retention-configure.md)
>

## <a name="are-backups-encrypted"></a>Yedeklemeleri şifrelenir?

TDE bir Azure SQL veritabanı için etkinleştirildiğinde, yedeklemeler de şifrelenir. Tüm yeni Azure SQL veritabanları, varsayılan olarak etkin TDE ile yapılandırılır. TDE hakkında daha fazla bilgi için bkz: [saydam veri şifrelemesi ile Azure SQL veritabanı](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database).

## <a name="next-steps"></a>Sonraki adımlar

- Verilerinizin yanlışlıkla Bozulması veya silme korumak için veritabanı yedeklemeleri tüm iş sürekliliği ve olağanüstü durum kurtarma stratejisi, önemli bir parçasıdır. toolearn hakkında diğer Azure SQL Database iş sürekliliği çözümleri Merhaba, bkz: [iş sürekliliğine genel bakış](sql-database-business-continuity.md).
- hello Azure portal kullanarak zaman toorestore tooa noktasına bkz [veritabanı tooa noktası hello Azure portal kullanarak zaman içinde geri](sql-database-recovery-using-backups.md).
- PowerShell kullanarak zaman toorestore tooa noktasına bkz [veritabanı tooa noktası PowerShell kullanarak zaman içinde geri](scripts/sql-database-restore-database-powershell.md).
- tooconfigure, yönetmek ve geri yükleme hello kullanarak bir Azure kurtarma Hizmetleri kasası Otomatik yedeklemelerin uzun vadeli bekletme Azure portal, bkz: [hello Azure portalı Yönet uzun vadeli yedekleme bekletme kullanarak](sql-database-long-term-backup-retention-configure.md).
- tooconfigure, Yönet'i ve PowerShell kullanarak bir Azure kurtarma Hizmetleri kasası Otomatik yedeklemelerin uzun vadeli bekletme geri yükleme, bkz: [uzun vadeli yedekleme bekletme PowerShell kullanarak yönetme](sql-database-long-term-backup-retention-configure.md).
