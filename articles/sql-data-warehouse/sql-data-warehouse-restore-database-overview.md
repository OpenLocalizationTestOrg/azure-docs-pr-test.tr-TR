---
title: "Azure veri ambarı - yerel ve coğrafi olarak yedekli aaaRestore | Microsoft Docs"
description: "Azure SQL Data Warehouse bir veritabanına kurtarmak için hello veritabanı geri yükleme seçeneklerine genel bakış."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: 3e01c65c-6708-4fd7-82f5-4e1b5f61d304
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: a96b898372b29d420e1416ca93a172ff8af47fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-restore"></a>SQL veri ambarı geri yükleme
> [!div class="op_single_selector"]
> * [Genel bakış][Overview]
> * [Portal][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

SQL veri ambarı hem yerel hem de coğrafi geri yükleme, veri ambarı olağanüstü bir parçası olarak kurtarma özellikleri sunar. Veri ambarı tooa geri yüklemenizin hello birincil bölgede noktası veya coğrafi olarak yedekli yedeklemeleri toorestore tooa farklı coğrafi bölge kullanın veri ambarı yedeklemeleri toorestore kullanın. Bu makalede, bir veri ambarı geri yüklenmesi hello özellikleri açıklanmaktadır.

## <a name="what-is-a-data-warehouse-restore"></a>Veri ambarı geri nedir?
Bir veri ambarı geri yükleme, varolan bir yedek kopyadan oluşturulan yeni veri ambarı veya silinen veri ambarı ' dir. Merhaba geri yüklenen veri ambarı hello yedeklenen veri ambarı belirli bir zamanda yeniden oluşturur. SQL veri ambarı dağıtılmış bir sistemde olduğundan, bir veri ambarı geri yükleme dosyalarından Azure BLOB'ları depolanan birçok yedekleme oluşturulur. 

Veritabanı geri yükleme tüm iş sürekliliği ve olağanüstü durum kurtarma stratejisi önemli bir parçası olduğundan, verilerinizin yanlışlıkla Bozulması veya silme işlemi sonrasında yeniden oluşturur.

Daha fazla bilgi için bkz.

* [SQL veri ambarı yedekleri](sql-data-warehouse-backups.md)
* [İş sürekliliğine genel bakış](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a>Veri ambarı geri yükleme noktaları
Azure Premium Storage kullanmanın avantajı Azure Storage Blobuna anlık görüntüleri toobackup hello birincil veri ambarı SQL Data Warehouse kullanır. Başlangıç zamanı temsil eden bir geri yükleme noktası her anlık görüntü var hello anlık görüntü başlatıldı. bir geri yükleme noktası seçin ve geri yükleme komutu toorestore bir veri ambarı.  

SQL Data Warehouse, her zaman hello yedekleme tooa yeni veri ambarı geri yükler. Merhaba geri yüklenen veri ambarı tutmak geçerli bir hello veya bunlardan birini silin. Tooreplace hello geçerli istiyorsanız hello veri ambarına veri ambarını geri, onu yeniden adlandırabilirsiniz.

Toorestore silinmiş ya da duraklatılmış veri ambarı gerekiyorsa, yapabilecekleriniz [destek bileti oluşturma](sql-data-warehouse-get-started-create-support-ticket.md). 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore hello last available restore point.

Yes, for hello next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps hello data warehouse and its snapshots for seven days just in case you need hello data. After seven days, you won't be able toorestore tooany of hello restore points. -->

## <a name="geo-redundant-restore"></a>Coğrafi olarak yedekli geri yükleme
Azure SQL Data Warehouse, seçilen performans düzeyinde destekleyen, veri ambarı tooany bölgesi geri yükleyebilirsiniz. 9000 ve 18000 DWU desteklenmez, tüm bölgelerde hello Önizleme sırasında unutmayın.

> [!NOTE]
> bir coğrafi olarak yedekli tooperform geri yükleme, bu özellik dışında çevirdiniz gerekir değil.
> 
> 

## <a name="restore-timeline"></a>Zaman çizelgesi geri yükleme
Son yedi günde bir veritabanı tooany kullanılabilir geri yükleme noktası hello içinde geri yükleyebilirsiniz. Anlık görüntüler, dört tooeight saatte başlatmak ve yedi gün için kullanılabilir. Bir anlık görüntü yedi günden daha eski olduğunda süresi dolmadan ve geri yükleme noktası artık kullanılamıyor.

## <a name="restore-costs"></a>Maliyetleri geri yükleme
hello Azure Premium Storage hızında hello geri yüklenen veri ambarı için Hello depolama ücret faturalandırılır. 

Geri yüklenen veri ambarı durdurursanız hello Azure Premium Storage hızında depolama için ücretlendirilirsiniz. duraklatma hello avantajı hello DWU bilgi işlem kaynakları için sizden ücret istenmese olmasıdır.

SQL Data Warehouse fiyatlandırması hakkında daha fazla bilgi için bkz: [SQL Data Warehouse fiyatlandırması](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).

## <a name="uses-for-restore"></a>Geri yükleme için de kullanır
Merhaba birincil veri ambarı geri yüklemek için toorecover veri yanlışlıkla veri kaybı veya bozulması sonra kullanılır.

Veri ambarı geri yükleme tooretain bir yedekleme, yedi günden daha uzun için de kullanabilirsiniz. Merhaba yedekleme geri yüklendikten sonra hello veri ambarı çevrimiçi sahip ve duraklatabilir süresiz olarak toosave işlem maliyetleri. Merhaba duraklatılmış veritabanı depolama ücretleri hello Azure Premium Storage hızında doğurur. 

## <a name="related-topics"></a>İlgili konular
### <a name="scenarios"></a>Senaryolar
* İş sürekliliğine genel bakış için bkz: [iş sürekliliğine genel bakış](../sql-database/sql-database-business-continuity.md)

<!-- ### Tasks -->

veri ambarı tooperform geri yükleme, kullanarak geri yükleyin:

* Azure portal, bkz: [hello Azure portal kullanarak bir veri ambarı geri yükle](sql-data-warehouse-restore-database-portal.md)
* PowerShell cmdlet'leri görmek [PowerShell cmdlet'lerini kullanarak bir veri ambarı geri yükle](sql-data-warehouse-restore-database-powershell.md)
* REST API için bkz: [hello REST API'lerini kullanarak bir veri ambarı geri yükle](sql-data-warehouse-restore-database-rest-api.md)

<!-- ### Tutorials -->

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->


<!--Other Web references-->
