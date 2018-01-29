---
title: "Esnek veritabanı araçlarını kullanarak bir parça ekleme | Microsoft Docs"
description: "Esnek ölçeklendirme API'leri yeni parça bir parça eklemek için nasıl kullanılacağını ayarlayın."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 62a349db-bebe-406f-a120-2f1986f2b286
ms.service: sql-database
ms.custom: scale out apps
ms.workload: Inactive
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2017
ms.author: ddove
ms.openlocfilehash: c3abbae20772cfc37fb8c58dc97209ac42dde358
ms.sourcegitcommit: 5a6e943718a8d2bc5babea3cd624c0557ab67bd5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/01/2017
---
# <a name="adding-a-shard-using-elastic-database-tools"></a>Esnek veritabanı araçlarını kullanarak bir parça ekleme
## <a name="to-add-a-shard-for-a-new-range-or-key"></a>Yeni aralık veya anahtarı için bir parça eklemek için
Uygulamalar genellikle yeni anahtarlar veya zaten bir parça eşleme için anahtar aralıklarına beklenen verileri işlemek için yeni parça eklemeniz gerekir. Örneğin, Kiracı kimliği tarafından parçalı bir uygulama için yeni bir kiracı yeni bir parça sağlamak gerekebilir veya veri parçalı aylık yeni her ayın başlangıcını önce sağlanan yeni bir parça gerekebilir. 

Yeni anahtar değerleri aralığı zaten varolan bir eşleme parçası değilse, yeni parça eklemek ve yeni bir anahtar ya da bu parça aralığa ilişkilendirmek basit bir işlemdir. 

### <a name="example--adding-a-shard-and-its-range-to-an-existing-shard-map"></a>Örnek: varolan bir parça eşlemesini bir parça ve kendi aralığı ekleme
Bu örnek TryGetShard kullanır ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._shard_map.trygetshard), [.NET](https://msdn.microsoft.com/library/azure/dn823929.aspx)) CreateShard ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._shard_map.createshard), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)), CreateRangeMapping ([ Java](/java/api/com.microsoft.azure.elasticdb.shard.map._range_shard_map.createrangemapping), [.NET](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\))) yöntemleri ve ShardLocation bir örneğini oluşturur ([Java](/java/api/com.microsoft.azure.elasticdb.shard.base._shard_location), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.)) sınıfı. Aşağıda, adlı bir veritabanı örneğinde **sample_shard_2** ve içindeki tüm gerekli şema nesneleri [300, 400). aralık tutmak için oluşturuldu  

```csharp
// sm is a RangeShardMap object.
// Add a new shard to hold the range being added. 
Shard shard2 = null; 

if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
{ 
    shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
} 

// Create the mapping and associate it with the new shard 
sm.CreateRangeMapping(new RangeMappingCreationInfo<long> 
                            (new Range<long>(300, 400), shard2, MappingStatus.Online)); 
```

.NET sürüm için ayrıca PowerShell alternatif olarak yeni bir parça eşleme yönetici oluşturmak için kullanabilirsiniz. Bir örneği, kullanılabilir [burada](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

## <a name="to-add-a-shard-for-an-empty-part-of-an-existing-range"></a>Var olan bir aralığı boş bir kısmı için bir parça eklemek için
Bazı durumlarda, bir parça için bir aralığı zaten eşlenmiş ve kısmen verilerle doldurulur olabilirsiniz, ancak şimdi için farklı bir parça yönlendirilmesi için yaklaşan veri istiyorsunuz. Örneğin, parça gün aralığı tarafından ve parça için zaten ayrılmış 50 gününüz vardır, ancak gelecekteki verilerin içinde farklı bir parça güden istediğiniz günde 24. Esnek veritabanı [bölünmüş Birleştirme aracı](sql-database-elastic-scale-overview-split-and-merge.md) bu işlemi gerçekleştirebilir, ancak veri taşıma diğer bir deyişle (örneğin, [25, 50 gün aralığı için veri), gerekli değilse gün 25 özel, 50 (dahil) henüz yok), bu gerçekleştirebilirsiniz tamamen parça eşleme Yönetimi API'leri kullanarak doğrudan.

### <a name="example-splitting-a-range-and-assigning-the-empty-portion-to-a-newly-added-shard"></a>Örnek: bir aralık bölme ve boş bölümü için yeni eklenen bir parça atama
"Sample_shard_2" ve içindeki tüm gerekli şema nesneleri adlı bir veritabanı oluşturuldu.  

```csharp
// sm is a RangeShardMap object.
// Add a new shard to hold the range we will move 
Shard shard2 = null; 

if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
{ 
    shard2 = sm.CreateShard(new ShardLocation(shardServer,"sample_shard_2"));  
} 

// Split the Range holding Key 25 
sm.SplitMapping(sm.GetMappingForKey(25), 25); 

// Map new range holding [25-50) to different shard: 
// first take existing mapping offline 
sm.MarkMappingOffline(sm.GetMappingForKey(25)); 

// now map while offline to a different shard and take online 
RangeMappingUpdate upd = new RangeMappingUpdate(); 
upd.Shard = shard2; 
sm.MarkMappingOnline(sm.UpdateMapping(sm.GetMappingForKey(25), upd)); 
```

**Önemli**: aralığının eminseniz güncelleştirilmiş eşleme boş ise yalnızca bu tekniği kullanın.  Denetimleri kodunuzda dahil etmek en iyisidir önceki yöntemler taşınan, aralığı için veri denetlemez.  Satırlar taşınan aralığında varsa, gerçek veri dağıtım güncelleştirilmiş parça eşleme eşleşmez. Kullanım [bölünmüş Birleştirme aracı](sql-database-elastic-scale-overview-split-and-merge.md) bu gibi durumlarda bunun yerine işlemi gerçekleştirmek için.  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

