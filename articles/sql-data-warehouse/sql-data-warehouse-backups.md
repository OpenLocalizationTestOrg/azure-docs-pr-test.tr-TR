---
title: "aaaAzure SQL Data Warehouse yedeklemeleri - anlık görüntüler, coğrafi olarak yedekli | Microsoft Docs"
description: "Bir Azure SQL Data Warehouse tooa geri yükleme noktası veya farklı coğrafi bölge toorestore etkinleştirmek SQL Data Warehouse yerleşik veritabanı yedeklemeleri hakkında bilgi edinin."
services: sql-data-warehouse
documentationcenter: 
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: b5aff094-05b2-4578-acf3-ec456656febd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: 34659480485246f54a1490e185fc1b903fb2520d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-backups"></a>SQL veri ambarı yedekleri
SQL veri ambarı veri ambarı yedekleme yeteneklerini bir parçası olarak hem yerel hem de coğrafi yedeklemeler sunar. Bunlar, Azure Storage Blobuna anlık görüntüler ve coğrafi olarak yedekli depolama içerir. Veri ambarı tooa geri yüklemenizin hello birincil bölgede noktası veya tooa farklı coğrafi geri yükleme, veri ambarı yedeklemeleri toorestore kullanın. Bu makalede SQL Data Warehouse yedeklemelerin hello özellikleri açıklanmaktadır.

## <a name="what-is-a-data-warehouse-backup"></a>Veri ambarı yedekleme nedir?
Veri ambarı yedekleme, veri ambarı tooa belirli bir süre toorestore kullanabileceğiniz hello verilerdir.  SQL veri ambarı dağıtılmış bir sistemde olduğundan, bir veri ambarı yedekleme Azure blob'larda depolanan çok sayıda dosya oluşur. 

Verilerinizin yanlışlıkla Bozulması veya silme korumak için veritabanı yedeklemeleri tüm iş sürekliliği ve olağanüstü durum kurtarma stratejisi, önemli bir parçasıdır. Daha fazla bilgi için bkz: [iş sürekliliğine genel bakış](../sql-database/sql-database-business-continuity.md).

## <a name="data-redundancy"></a>Veri yedekliği
SQL Data Warehouse, yerel olarak yedekli (LRS) Azure Premium Storage'da veri depolayarak verilerinizi korur. Yerelleştirilmiş hata varsa bu Azure depolama özellik hello verileri birden çok zaman uyumlu kopyası'nde hello yerel veri merkezi tooguarantee saydam veri koruma depolar. Verilerinizi disk hataları gibi altyapı sorunları varlığını sürdürmesi veri artıklık sağlar. Veri artıklığı bir hataya dayanıklı ile iş devamlılığı ve yüksek oranda kullanılabilir bir altyapı sağlar.

toolearn hakkında daha fazla bilgi:

* Azure Premium depolama bkz [giriş tooAzure Premium depolama](../storage/common/storage-premium-storage.md).
* Yerel olarak yedekli depolama bkz [Azure Storage çoğaltma](../storage/common/storage-redundancy.md#locally-redundant-storage).

## <a name="azure-storage-blob-snapshots"></a>Azure depolama blobu anlık görüntüler
Azure Premium Storage kullanmanın avantajı SQL Data Warehouse yerel olarak Azure Storage Blobuna anlık görüntüleri toobackup hello veri ambarı kullanır. Bir veri ambarı tooa anlık görüntü geri yükleme noktası geri yükleyebilirsiniz. Anlık görüntüler her sekiz saatte en az başlatmak ve yedi gün için kullanılabilir.  

toolearn hakkında daha fazla bilgi:

* Azure blob anlık görüntülerini görmek [blob anlık görüntü](../storage/blobs/storage-blob-snapshots.md).

## <a name="geo-redundant-backups"></a>Coğrafi olarak yedekli yedekleri
24 saatte SQL Data Warehouse hello tam veri ambarı standart depolama alanında depolar. Merhaba tam veri ambarı toomatch oluşturulan hello hello son anlık görüntü saati. Merhaba standart depolama tooa coğrafi olarak yedekli depolama okuma erişimi (RA-GRS) hesabıyla aittir. Hello Azure depolama RA-GRS özelliği çoğaltır hello yedekleme dosyalarını tooa [eşleştirilmiş veri merkezi](../best-practices-availability-paired-regions.md). Bu coğrafi çoğaltma, birincil bölgenizde hello anlık görüntüleri erişemiyor durumunda, veri ambarı geri yükleyebilirsiniz sağlar. 

Bu özellik varsayılan olarak açıktır. Toouse coğrafi olarak yedekli yedeklemeler, sizin [çıkma] istemiyorsanız (https://docs.microsoft.com/powershell/resourcemanager/Azurerm.sql/v2.1.0/Set-AzureRmSqlDatabaseGeoBackupPolicy?redirectedfrom=msdn). 

> [!NOTE]
> Azure depolama alanında hello terim *çoğaltma* toocopying dosyaları tek bir konumda tooanother başvuruyor. SQL'in *veritabanı çoğaltması* tookeeping toomultiple ikincil veritabanları birincil veritabanı ile eşitlenen başvuruyor. 
> 
> 

> [!NOTE]
> Coğrafi olarak yedekli yedeklemelerde DWU 9000 ve DWU 18000 dışında kabul edemez. 
>
> 

toolearn hakkında daha fazla bilgi:

* Coğrafi olarak yedekli depolama bkz [Azure Storage çoğaltma](../storage/common/storage-redundancy.md).
* RA-GRS depolama bkz [okuma erişimli coğrafi olarak yedekli depolama](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage).

## <a name="data-warehouse-backup-schedule-and-retention-period"></a>Veri ambarı yedekleme zamanlamasını ve saklama süresi
SQL veri ambarı çevrimiçi veri ambarınız her dört tooeight saatlerini ve her yedi gün için anlık görüntü tutar anlık görüntüleri oluşturur. Son yedi gün, çevrimiçi veritabanı tooone hello geri yükleme noktaları hello içinde geri yükleyebilirsiniz. 

Merhaba son anlık görüntü başlatıldığında toosee çevrimiçi SQL veri ambarı üzerinde bu sorguyu çalıştırın. 

```sql
select top 1 *
from sys.pdw_loader_backup_runs 
order by run_id desc;
```

Yedi günden daha uzun süre tooretain bir anlık görüntü gerekiyorsa, bir geri yükleme noktası tooa yeni veri ambarı geri yükleyebilirsiniz. Merhaba geri yüklemeyi tamamladıktan sonra SQL Data Warehouse anlık hello yeni veri ambarı oluşturmayı başlatır. Değişiklikleri toohello yeni veri ambarı yapmazsanız, hello anlık görüntüleri boş kalır ve bu nedenle hello anlık görüntü maliyeti en az. Merhaba veritabanı tookeep SQL Data Warehouse duraklatın anlık görüntüleri oluşturma.

### <a name="what-happens-toomy-backup-retention-while-my-data-warehouse-is-paused"></a>My veri ambarı duraklatıldığında toomy yedekleme bekletme ne olur?
SQL Data Warehouse anlık görüntülerini oluşturma değil ve bir veri ambarı duraklatıldığında anlık görüntüleri dolmaz. Merhaba veri ambarı duraklatıldığında hello anlık görüntü yaş değiştirmez. Anlık görüntü saklama hello Takvim günleri hello veri ambarı çevrimiçi olduğu gün sayısına bağlıdır.

Örneğin, bir anlık görüntü 4'e 1 Ekim başlatır ve 4'e hello veri ambarı Ekim 3 olarak duraklatıldı hello anlık görüntü iki gün olur. Merhaba veri ambarını yeniden çevrimiçi duruma dönerse her iki gün hello anlık görüntüsüdür. Merhaba veri ambarı Ekim 5 4'e çevrimiçi olursa, hello anlık görüntü iki gün önce yapılmışsa ve daha fazla beş gün boyunca devam eder.

Merhaba veri ambarı tekrar çevrimiçi olduğunda, SQL Data Warehouse Yeni Anlık görüntülerin sürdürür ve yedi günden fazla veri olduğunda anlık görüntüleri süresi dolar.

### <a name="how-long-is-hello-retention-period-for-a-dropped-data-warehouse"></a>Bırakılan veri ambarı Hello saklama süresi uzunluğu nedir?
Veri ambarı bırakıldığında hello veri ambarı ve hello anlık görüntüleri yedi gün için kaydedilir ve sonra kaldırılır. Merhaba veri ambarı tooany kaydedilmiş hello geri yükleme noktaları geri yükleyebilirsiniz.

> [!IMPORTANT]
> Mantıksal bir SQL server örneği silerseniz, toohello örneği ait tüm veritabanlarının da silinir ve kurtarılamaz. Silinen bir sunucuya geri yükleyemezsiniz.
> 
> 

## <a name="data-warehouse-backup-costs"></a>Veri ambarı yedekleme maliyetleri
Maliyet birincil veri ambarı ve Azure Blob anlık görüntü yedi gün için toplam hello TB en yakın yuvarlak toohello ' dir. Örneğin, veri Ambarınızı 1,5 TB ise ve 100 GB hello anlık görüntüleri kullanmak, 2 TB veri Azure Premium Storage hızlarında için faturalandırılır. 

> [!NOTE]
> Her anlık görüntü başlangıçta boş ve değişiklikleri toohello birincil veri ambarı yaptığınız gibi büyür. Tüm anlık görüntüleri hello veri ambarı değiştikçe boyutunu artırın. Bu nedenle, anlık görüntüler için hello depolama maliyetleri değişiklik according toohello oranını artar.
> 
> 

Coğrafi olarak yedekli depolama birimi kullanıyorsanız, ayrı depolama ücret alırsınız. Merhaba coğrafi olarak yedekli depolama hello standart okuma erişimli coğrafi olarak yedekli depolama (RA-GRS) oranı faturalandırılır.

SQL Data Warehouse fiyatlandırması hakkında daha fazla bilgi için bkz: [SQL Data Warehouse fiyatlandırması](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).

## <a name="using-database-backups"></a>Veritabanı Yedeklemeleri kullanma
Merhaba birincil için SQL veri ambarı yedekleri toorestore hello veri ambarı tooone hello geri yükleme noktaları hello saklama dönemi içinde kullanılmasıdır.  

* toorestore SQL data warehouse, bkz: [SQL data warehouse geri](sql-data-warehouse-restore-database-overview.md).

## <a name="related-topics"></a>İlgili konular
### <a name="scenarios"></a>Senaryolar
* İş sürekliliğine genel bakış için bkz: [iş sürekliliğine genel bakış](../sql-database/sql-database-business-continuity.md)

<!-- ### Tasks -->

* toorestore bir veri ambarı bkz [SQL data warehouse geri yükleme](sql-data-warehouse-restore-database-overview.md)

<!-- ### Tutorials -->

