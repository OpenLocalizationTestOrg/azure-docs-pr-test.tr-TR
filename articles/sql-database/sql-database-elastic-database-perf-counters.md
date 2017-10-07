---
title: "Parça eşleme Yöneticisi için aaaPerformance sayaçları"
description: "ShardMapManager sınıf ve veri bağımlı Yönlendirme performans sayaçları"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: b090aba0-2e30-454c-96b3-dffa281f539a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: ddove
ms.openlocfilehash: d24198563d9fa88d12e6c464dbe89bc300e72ca0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-counters-for-shard-map-manager"></a>Parça eşleme yöneticisi için performans sayaçları
Merhaba performansını yakalamak için bir [parça eşleme Yöneticisi](sql-database-elastic-scale-shard-map-management.md), özellikle kullanırken [veri bağımlı yönlendirme](sql-database-elastic-scale-data-dependent-routing.md). Sayaçları hello Microsoft.Azure.SqlDatabase.ElasticScale.Client sınıfı yöntemleri ile oluşturulur.  

Sayaçları olan kullanılan tootrack hello performansını [veri bağımlı yönlendirme](sql-database-elastic-scale-data-dependent-routing.md) işlemleri. Bu sayaçlar hello "Esnek veritabanı: Parça Yönetimi" kategorisi altında Performans İzleyicisi Merhaba erişilebilir.

**Merhaba en son sürümü için:** çok Git[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). Ayrıca bkz. [bir uygulama toouse hello son esnek veritabanı istemci kitaplığı yükseltme](sql-database-elastic-scale-upgrade-client-library.md).

## <a name="prerequisites"></a>Ön koşullar
* toocreate hello performans kategorisi ve sayaçları, hello kullanıcı hello yerel bir parçası olmalıdır **Yöneticiler** hello uygulama barındırma hello makinede grup.  
* toocreate bir performans sayacı örneği ve hello sayaçları güncelleştirmek, hello kullanıcı ya da hello üyesi olmalı **Yöneticiler** veya **Performance Monitor Users** grubu. 

## <a name="create-performance-category-and-counters"></a>Performans kategorisi ve sayaçları oluşturma
toocreate hello sayaçları, hello hello CreatePeformanceCategoryAndCounters yöntemi çağrısı [ShardMapManagmentFactory sınıfı](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx). Yalnızca bir yönetici hello yöntemi yürütebilir: 

    ShardMapManagerFactory.CreatePerformanceCategoryAndCounters()  

Aynı zamanda [bu](https://gallery.technet.microsoft.com/scriptcenter/Elastic-DB-Tools-for-Azure-17e3d283) PowerShell komut dosyası tooexecute hello yöntemi. Merhaba yöntemi, performans sayaçlarını izleyerek hello oluşturur:  

* **Eşlemeleri önbelleğe**: hello parça eşleme için önbelleğe alınmış eşlemeleri sayısı.
* **DDR işlemi/sn**: hello parça eşlemesi için verileri bağımlı yönlendirme işlemlerinin hızıdır. Bu sayaç bir çağrı onayladığında çok[OpenConnectionForKey()](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) sonuçları içinde başarılı bağlantı toohello hedef parça. 
* **Arama Önbelleği İsabetli Okuma/sn eşleme**: hello parça eşlemesindeki eşlemeleri başarılı önbellek arama işlemlerinin hızıdır. 
* **Arama önbellek isabetsizliği/sn eşleme**: hello parça eşlemesindeki eşlemeleri başarısız önbellek arama işlemlerinin hızıdır.
* **Eşleme eklendi veya Önbellek/sn güncelleştirildi**: hangi eşlemeleri eklenir veya hello parça eşleme için güncelleştirilmiş içinde önbelleğine hızda. 
* **Eşlemeleri kaldırılan Önbellek/sn**: hangi eşlemeleri kaldırılır hello parça harita önbelleğinden oranı. 

Performans sayaçları, işlem başına her önbelleğe alınmış parça eşleme için oluşturulur.  

## <a name="notes"></a>Notlar
Merhaba aşağıdaki olaylar hello performans sayaçları hello oluşturulmasını tetikleyecek:  

* Merhaba başlatma [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) ile [istekli yükleme](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerloadpolicy.aspx), hello ShardMapManager herhangi parça eşlemeler içeriyorsa. Merhaba bunlar [GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx?f=255&MSPPError=-2147217396#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerFactory.GetSqlShardMapManager%28System.String,Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerLoadPolicy%29) ve hello [TryGetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx) yöntemleri.
* Parça eşleme başarılı arama (kullanarak [GetShardMap()](https://msdn.microsoft.com/library/azure/dn824215.aspx), [GetListShardMap()](https://msdn.microsoft.com/library/azure/dn824212.aspx) veya [GetRangeShardMap()](https://msdn.microsoft.com/library/azure/dn824173.aspx)). 
* Parça eşleme CreateShardMap() kullanarak başarılı oluşturma.

Merhaba performans sayaçları hello parça eşleme ve eşlemeleri gerçekleştirilen tüm önbellek işlemleri tarafından güncelleştirilir. Başarılı kaldırma DeleteShardMap () sonuç hello performans sayaçları örneği silinmesine kullanarak hello parça eşleme.  

## <a name="best-practices"></a>En iyi uygulamalar
* Merhaba performans kategorisi ve sayaçları oluşturulmasını ShardMapManager nesne hello oluşturması işleminden önce yalnızca bir kez gerçekleştirilmesi gerekir. Merhaba komutu her yürütme CreatePerformanceCategoryAndCounters() hello önceki sayaçları (tüm örnekleri tarafından bildirilen veri kaybı) temizler ve yenilerini oluşturur.  
* Performans sayacı örnekleri her işlem için oluşturulur. Herhangi bir uygulama kilitlenme veya parça eşleme hello önbelleğinden kaldırma hello performans sayaçları örnekleri silinmesine neden olacak.  

### <a name="see-also"></a>Ayrıca bkz.
[Esnek veritabanı özelliklere genel bakış](sql-database-elastic-scale-introduction.md)  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->

