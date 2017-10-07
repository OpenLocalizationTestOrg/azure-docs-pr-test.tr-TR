---
title: "Esnek veritabanı araçlarını kullanarak parça a aaaAdding | Microsoft Docs"
description: "Nasıl toouse esnek ölçeklendirme API'leri tooadd yeni parça tooa parça ayarlayın."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 62a349db-bebe-406f-a120-2f1986f2b286
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f44b59578376d1238b3012a3cb52339978079f0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-shard-using-elastic-database-tools"></a>Esnek veritabanı araçlarını kullanarak bir parça ekleme
## <a name="tooadd-a-shard-for-a-new-range-or-key"></a>Yeni aralık veya anahtarı için bir parça tooadd
Uygulamaları parça eşleme zaten var için toosimply yeni anahtarlar veya anahtar aralıkları, beklenen yeni parça toohandle veriler genellikle eklemeniz. Örneğin, Kiracı kimliği tarafından parçalı bir uygulama için yeni bir kiracı tooprovision yeni bir parça gerekebilir veya veri parçalı aylık yeni her ay hello başlamadan önce sağlanan yeni bir parça gerekebilir. 

Anahtar değerlerinin Hello yeni aralık zaten varolan bir eşleme parçası değilse çok basit tooadd hello yeni parça ve ilişkilendirme hello yeni anahtarı veya aralık toothat parça olur. 

### <a name="example--adding-a-shard-and-its-range-tooan-existing-shard-map"></a>Örnek: bir parça ve kendi aralığı tooan varolan parça eşleme ekleme
Bu örnek hello kullanan [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) hello [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) yöntemleri ve hello örneği oluşturur [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) sınıfı. Aşağıda, adlı bir veritabanı hello örnekteki **sample_shard_2** ve içindeki tüm gerekli şema nesneleri toohold aralığı [300, 400). oluşturuldu  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range being added. 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 
        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Create hello mapping and associate it with hello new shard 
    sm.CreateRangeMapping(new RangeMappingCreationInfo<long> 
                            (new Range<long>(300, 400), shard2, MappingStatus.Online)); 


Alternatif olarak, Powershell toocreate yeni parça eşleme Yöneticisi kullanabilirsiniz. Bir örneği, kullanılabilir [burada](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

## <a name="tooadd-a-shard-for-an-empty-part-of-an-existing-range"></a>var olan bir aralığı boş bir kısmı için bir parça tooadd
Bazı durumlarda, bir aralık tooa parça eşlenmiş ve kısmen verilerle doldurulur olabilirsiniz, ancak şimdi yaklaşan veri toobe yönlendirilmiş tooa farklı parça istiyorsunuz. Örneğin, parça günlük aralığı ve 50 gün tooa parça Tahsis etmiş ancak farklı bir parça, gelecekteki veri tooland istediğiniz 24 günü. Merhaba esnek veritabanı [bölünmüş Birleştirme aracı](sql-database-elastic-scale-overview-split-and-merge.md) bu işlemi gerçekleştirebilir, ancak veri taşıma yani (örneğin, günlük [25, 50 hello aralığı için veri), gerekli değilse gün 25 dahil too50 özel, henüz yok), gerçekleştirebilirsiniz tamamen kullanarak bu hello parça eşleme Yönetimi API'lerini doğrudan.

### <a name="example-splitting-a-range-and-assigning-hello-empty-portion-tooa-newly-added-shard"></a>Örnek: bir aralık bölme ve hello atama bölümü tooa yeni eklenen parça boş
"Sample_shard_2" ve içindeki tüm gerekli şema nesneleri adlı bir veritabanı oluşturuldu.  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range we will move 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 

        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Split hello Range holding Key 25 

    sm.SplitMapping(sm.GetMappingForKey(25), 25); 

    // Map new range holding [25-50) toodifferent shard: 
    // first take existing mapping offline 
    sm.MarkMappingOffline(sm.GetMappingForKey(25)); 
    // now map while offline tooa different shard and take online 
    RangeMappingUpdate upd = new RangeMappingUpdate(); 
    upd.Shard = shard2; 
    sm.MarkMappingOnline(sm.UpdateMapping(sm.GetMappingForKey(25), upd)); 

**Önemli**: aralığının hello belirli varsa güncelleştirilmiş hello eşleme boş, yalnızca bu tekniği kullanın.  Yukarıdaki Hello yöntemleri taşınan hello aralığı için veri denetleme, en iyi şekilde kodunuzda tooinclude denetler.  Satırlar taşınan hello aralığında varsa, hello gerçek veri dağıtım hello güncelleştirilmiş parça eşleme eşleşmez. Kullanım hello [bölünmüş Birleştirme aracı](sql-database-elastic-scale-overview-split-and-merge.md) tooperform hello işlemi bunun yerine bu gibi durumlarda.  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

