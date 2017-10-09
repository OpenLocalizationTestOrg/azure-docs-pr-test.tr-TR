---
title: "aaaMigrate varolan veritabanları tooscale kullanıma | Microsoft Docs"
description: "Parça eşleme Yöneticisi oluşturarak parçalı veritabanları toouse esnek veritabanı araçlarını Dönüştür"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 8c851d8e-8fd5-4327-89c1-9178b20ddd69
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: fa2c9e3699f30667cf547d1faadf4504609199be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-existing-databases-tooscale-out"></a>Varolan veritabanları tooscale kullanıma geçirme
Azure SQL Database veritabanı araçları kullanarak mevcut ölçeklendirilmiş parçalı veritabanlarınız kolayca yönetmenize (Merhaba gibi [esnek veritabanı istemci Kitaplığı](sql-database-elastic-database-client-library.md)). Var olan bir veritabanları toouse hello dönüştürmeniz gerekir [parça eşleme Yöneticisi](sql-database-elastic-scale-shard-map-management.md). 

## <a name="overview"></a>Genel Bakış
var olan bir parçalı veritabanı toomigrate: 

1. Merhaba hazırlama [parça eşleme Yöneticisi veritabanı](sql-database-elastic-scale-shard-map-management.md).
2. Merhaba parça eşleme oluşturun.
3. Merhaba tek tek parça hazırlayın.  
4. Eşlemeleri toohello parça eşleme ekleyin.

Her iki hello kullanarak bu teknikler uygulanabilir [.NET Framework istemci Kitaplığı](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), veya hello PowerShell betikleri bulunması sırasında [Azure SQL veritabanı - esnek veritabanı araçlarını betikleri](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db). Burada Hello örnekler hello PowerShell betiklerini kullanın.

Merhaba ShardMapManager hakkında daha fazla bilgi için bkz: [parça eşleme Yönetim](sql-database-elastic-scale-shard-map-management.md). Merhaba esnek veritabanı araçlarını genel bakış için bkz: [esnek veritabanı özelliklere genel bakış](sql-database-elastic-scale-introduction.md).

## <a name="prepare-hello-shard-map-manager-database"></a>Merhaba parça eşleme manager veritabanını hazırlama
Merhaba parça eşleme Yöneticisi hello veri toomanage ölçeklendirilmiş veritabanlarını içeren özel bir veritabanıdır. Varolan bir veritabanını kullanın veya yeni bir veritabanı oluşturun. Parça eşleme Yöneticisi hello olmamalıdır bir veritabanı işlevi gören aynı parça veritabanı olduğunu unutmayın. Ayrıca hello PowerShell Betiği hello veritabanı sizin yerinize oluşturmaz olduğunu unutmayın. 

## <a name="step-1-create-a-shard-map-manager"></a>1. adım: bir parça eşleme Yöneticisi oluşturma
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are hello server name and database name 
    # for hello new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="tooretrieve-hello-shard-map-manager"></a>tooretrieve hello parça eşleme Yöneticisi
Oluşturulduktan sonra Bu cmdlet'i hello parça eşleme Yöneticisi alabilir. Toouse hello ShardMapManager nesne gereksinim duyduğunuz her zaman bu adım gereklidir.

    # Try tooget a reference toohello Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-hello-shard-map"></a>2. adım: hello parça eşleme oluşturma
Parça eşleme toocreate hello türü seçmelisiniz. Merhaba seçim hello veritabanı mimarisine bağlıdır: 

1. Veritabanı başına tek bir kiracı (Merhaba koşulları için bkz: [sözlüğü](sql-database-elastic-scale-glossary.md).) 
2. Birden çok Kiracı veritabanı (iki tür) başına:
   1. Liste eşleme
   2. Aralık eşleme

Tek Kiracı model için oluşturduğunuz bir **listesi eşleme** parça eşleme. Merhaba tek kiracılı bir model Kiracı başına tek bir veritabanı atar. Yönetimini basitleştirir gibi SaaS geliştiriciler için etkili bir modeli budur.

![Liste eşleme][1]

Merhaba çok kiracılı bir model çeşitli kiracılar tooa tek veritabanı atar (ve kiracılar grupları birden çok veritabanı arasında dağıtabilirsiniz). Bu model, her Kiracı toohave küçük veri gereken beklediğiniz kullanın. Bu modelde, biz kiracılar tooa veritabanını kullanmanın bir aralığı atamak **aralığı eşleme**. 

![Aralık eşleme][2]

Veya, bir çok Kiracı veritabanı modelini kullanarak uygulayabileceğiniz bir *listesi eşleme* tooassign birden çok kiracılar tooa tek veritabanı. Örneğin, Kiracı kimliği 1 ve 5 kullanılan toostore bilgilerini DB1 olduğu ve DB2 7 Kiracı ve Kiracı 10 için verileri depolar. 

![Birden fazla kiracılar tek DB][3] 

**Seçtiğiniz bağlı olarak, aşağıdaki seçeneklerden birini seçin:**

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a>Seçenek 1: bir liste eşlemesi için bir parça eşleme oluşturma
Merhaba ShardMapManager nesnesi kullanılarak bir parça Haritası oluşturun. 

    # $ShardMapManager is hello shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a>Seçenek 2: bir parça eşlemesi için bir aralığı eşlemesi oluşturma
Bu eşleme deseni bu tooutilize unutmayın, Kiracı kimliği değerleri gereken toobe sürekli aralıkları ve hello veritabanları oluşturulurken hello aralığı yalnızca atlayarak hello aralıklardaki kabul edilebilir toohave boşluk olduğundan.

    # $ShardMapManager is hello shard map manager object 
    # 'RangeShardMap' is hello unique identifier for hello range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a>Seçenek 3: tek bir veritabanı üzerinde eşlemeleri listesi
Bu deseni oluşturan ayarı ayrıca bir liste harita oluşturulmasını adım 2, 1. seçenek gösterildiği gibi gerektirir.

## <a name="step-3-prepare-individual-shards"></a>3. adım: tek tek parça hazırlama
Her parça (veritabanı) toohello parça eşleme Yöneticisi'ni ekleyin. Bu, hello tek veritabanlarını eşleme bilgilerini depolamak için hazırlar. Bu yöntem her parça üzerinde yürütün.

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # hello $ShardMap is hello shard map created in step 2.


## <a name="step-4-add-mappings"></a>4. adım: eşlemeleri ekleme
eşlemeleri Hello eklenmesi hello oluşturduğunuz parça eşleme türüne bağlıdır. Bir liste harita oluşturduysanız, liste eşlemeleri ekleyin. Bir aralık harita oluşturduysanız, aralık eşlemeleri ekleyin.

### <a name="option-1-map-hello-data-for-a-list-mapping"></a>Seçenek 1: eşleme hello verilerini listesi eşleme
Her bir kiracı için bir liste eşlemesi ekleyerek Hello veri eşleme.  

    # Create hello mappings and associate it with hello new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-hello-data-for-a-range-mapping"></a>Seçenek 2: eşleme hello veri için bir aralığı eşleme
Tüm hello Kiracı kimliği aralığı - veritabanı ilişkilendirmeleri Hello aralığı eşlemelerini ekleyin:

    # Create hello mappings and associate it with hello new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-hello-data-for-multiple-tenants-on-a-single-database"></a>Adım 4 seçenek 3: tek bir veritabanı üzerinde birden çok Kiracı için hello veri eşleme
Merhaba Ekle ListMapping her bir kiracı için Çalıştır (yukarıda seçenek 1,). 

## <a name="checking-hello-mappings"></a>Merhaba eşlemeleri denetleniyor
Merhaba varolan parça ve bunlarla ilişkilendirilmiş hello eşlemeleri hakkında bilgi komutları kullanarak sorgulanabilir:  

    # List hello shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a>Özet
Merhaba kurulumu tamamladıktan sonra toouse hello esnek veritabanı istemci kitaplığı başlayabilirsiniz. Aynı zamanda [veri bağımlı yönlendirme](sql-database-elastic-scale-data-dependent-routing.md) ve [çok parça sorgu](sql-database-elastic-scale-multishard-querying.md).

## <a name="next-steps"></a>Sonraki adımlar
Gelen Hello PowerShell komut dosyalarını almak [Azure SQL DB esnek veritabanı araçlarını sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

Merhaba araçlardır de Github'da: [Azure/esnek-db-tools](https://github.com/Azure/elastic-db-tools).

Merhaba bölünmüş Birleştirme aracı toomove veri tooor çok kiracılı bir model tooa tek bir kiracı modelden kullanın. Bkz: [bölünmüş Birleştirme aracı](sql-database-elastic-scale-get-started.md).

## <a name="additional-resources"></a>Ek kaynaklar
Çok kiracılı hizmet olarak yazılım (SaaS) veritabanı uygulamalarının ortak veri mimarisi düzenlerine ilişkin bilgi için bkz. [Azure SQL Database ile Çok Kiracılı SaaS Uygulamaları için Tasarım Düzenleri](sql-database-design-patterns-multi-tenancy-saas-applications.md).

## <a name="questions-and-feature-requests"></a>Sorular ve özellik istekleri
Sorular için lütfen hello üzerinde toous ulaşmak [SQL veritabanı Forumu](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) ve özellik istekleri için lütfen toohello eklemesini [SQL veritabanı geri bildirim Forumunda](https://feedback.azure.com/forums/217321-sql-database/).

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png

