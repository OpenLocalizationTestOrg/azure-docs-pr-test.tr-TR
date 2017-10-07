---
title: "bir Azure SQL veritabanı çıkışı aaaScale | Microsoft Docs"
description: "Nasıl toouse hello ShardMapManager, esnek veritabanı istemci kitaplığı"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 0e9d647a-9ba9-4875-aa22-662d01283439
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 4cf670d42ad7ded98fb8d6f0830154587dd2c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-out-databases-with-hello-shard-map-manager"></a>Merhaba parça eşleme Yöneticisi veritabanlarıyla ölçeğini genişletme
SQL Azure veritabanı tooeasily ölçeklenebilir bir parça eşleme Yöneticisi'ni kullanın. Merhaba parça eşleme Yöneticisi bir parça kümesindeki tüm parça (veritabanları) hakkında genel eşleme bilgilerini tutan özel bir veritabanıdır. Merhaba meta veri sağlar hello hello değerini alarak bir uygulama tooconnect toohello doğru veritabanı **parçalama anahtar**. Ayrıca, her parça hello kümesindeki hello yerel parça verileri izlemek eşlemeleri içerir (olarak bilinen **shardlets**). 

![Parça eşleme Yönetimi](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

Bu eşlemeleri nasıl oluşturulur anlama temel tooshard harita yönetimidir. Bu yapılır hello kullanarak [ShardMapManager sınıfı](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), hello bulunan [esnek veritabanı istemci Kitaplığı](sql-database-elastic-database-client-library.md) toomanage parça eşler.  

## <a name="shard-maps-and-shard-mappings"></a>Parça eşlemeleri ve parça eşlemeleri
Her parça, parça eşleme toocreate hello türü seçmelisiniz. Merhaba seçim hello veritabanı mimarisine bağlıdır: 

1. Veritabanı başına tek bir kiracı  
2. Birden çok Kiracı veritabanı (iki tür) başına:
   1. Liste eşleme
   2. Aralık eşleme

Tek Kiracı model için oluşturduğunuz bir **listesi eşleme** parça eşleme. Merhaba tek kiracılı bir model Kiracı başına tek bir veritabanı atar. Yönetimini basitleştirir gibi SaaS geliştiriciler için etkili bir modeli budur.

![Liste eşleme][1]

Merhaba çok kiracılı bir model çeşitli kiracılar tooa tek veritabanı atar (ve kiracılar grupları birden çok veritabanı arasında dağıtabilirsiniz). Bu model, her Kiracı toohave küçük veri gereken beklediğiniz kullanın. Bu modelde, biz kiracılar tooa veritabanını kullanmanın bir aralığı atamak **aralığı eşleme**. 

![Aralık eşleme][2]

Veya, bir çok Kiracı veritabanı modelini kullanarak uygulayabileceğiniz bir *listesi eşleme* tooassign birden çok kiracılar tooa tek veritabanı. Örneğin, Kiracı kimliği 1 ve 5 kullanılan toostore bilgilerini DB1 olduğu ve DB2 7 Kiracı ve Kiracı 10 için verileri depolar. 

![Birden fazla kiracılar tek DB][3] 

### <a name="supported-net-types-for-sharding-keys"></a>Parçalama anahtarları için desteklenen .net türleri
.NET aşağıdaki esnek ölçek destek hello Framework parçalama anahtarları olarak türleri:

* tamsayı
* uzun
* GUID
* Byte]  
* Tarih saat
* TimeSpan
* Datetimeoffset

### <a name="list-and-range-shard-maps"></a>Liste ve aralığı parça eşlemeleri
Parça eşlemeleri kullanarak olacak oluşturulan **tek tek parçalama listesi anahtar değerlerini**, veya kullanılarak oluşturulabilir **parçalama aralıklarına anahtar değerlerini**. 

### <a name="list-shard-maps"></a>Liste parça eşlemeleri
**Parça** içeren **shardlets** ve shardlets tooshards hello eşlenmesini parça eşleme tarafından korunur. A **listesi parça eşleme** hello shardlets tanımlayan hello tek tek anahtar değerleri ve parça hizmet hello veritabanları arasındaki ilişkidir.  **Liste eşlemeleri** açık ve farklı anahtar değerleri eşlenen toohello olabilir aynı veritabanı. Örneğin, anahtar 1 tooDatabase A eşler ve anahtar değerlerinin 3 ile 6 veritabanı B. başvurusu

| Anahtar | Parça konumu |
| --- | --- |
| 1 |Database_A |
| 3 |Database_B |
| 4 |Database_C |
| 6 |Database_B |
| ... |... |

### <a name="range-shard-maps"></a>Aralık parça eşlemeleri
İçinde bir **aralığı parça eşleme**, hello anahtar aralığı çifti tarafından açıklanan **[düşük değeri, yüksek değerli)** burada hello *düşük değer* hello minimum anahtarı hello aralığı ve hello *Yüksek değerli* hello ilk değer hello aralığından daha yüksek. 

Örneğin, **[0, 100)** 0 veya daha büyük ve 100'den küçük tüm tamsayılar içerir. Birden çok aralıkları can noktası aynı veritabanı ve ayrık aralıkları toohello desteklenir unutmayın (örneğin, [100,200) ve [400,600) iki nokta tooDatabase C hello örnekte.)

| Anahtar | Parça konumu |
| --- | --- |
| [1,50) |Database_A |
| [50,100) |Database_B |
| [100,200) |Database_C |
| [400,600) |Database_C |
| ... |... |

Yukarıda gösterilen hello tablolardan her biri kavramsal bir örneği olan bir **ShardMap** nesnesi. Her satırda tek bir Basitleştirilmiş örneğidir **PointMapping** (için hello listesi parça eşleme) veya **RangeMapping** (için hello aralığı parça eşleme) nesnesi.

## <a name="shard-map-manager"></a>Parça eşleme Yöneticisi
Merhaba istemci Kitaplığı'nda hello parça eşleme Yöneticisi parça eşlemeleri koleksiyonudur. Merhaba veri tarafından yönetilen bir **ShardMapManager** örneği üç yerde tutulur: 

1. **Genel parça eşleme (GSM)**: tüm parça eşlemeleri ve eşlemeler için hello depo olarak bir veritabanı tooserve belirtin. Özel tabloları ve saklı yordamlar toomanage hello bilgileri otomatik olarak oluşturulur. Bu genellikle küçük bir veritabanı ve hafifçe erişilen ve diğer Merhaba uygulaması gereksinimleriniz için kullanılmamalıdır. Merhaba adlı özel bir şemada tablolardır **__ShardManagement**. 
2. **Yerel parça eşleme (LSM)**: bir parça olduğu toobe değiştiren toocontain birkaç küçük tablolar ve parça eşleme bilgilerini belirli toothat parça yönetmek ve içeren özel saklı yordamlar belirttiğiniz her veritabanı. Bu bilgiler hello GSM hello bilgilerle yedekli ve GSM hello üzerinde hiçbir yük koymadan hello uygulama önbelleğe toovalidate parça eşleme bilgilerini sağlar; önbelleğe alınan bir eşleme hala geçerli ise Merhaba uygulaması hello LSM toodetermine kullanır. Merhaba tabloları her parça üzerinde LSM olan ayrıca hello şemada karşılık gelen toohello **__ShardManagement**.
3. **Uygulama önbelleği**: her uygulama örneği erişen bir **ShardMapManager** nesne eşlemelerini, yerel bir bellek içi önbellek tutar. Son alınan yönlendirme bilgilerini depolar. 

## <a name="constructing-a-shardmapmanager"></a>Bir ShardMapManager oluşturma
A **ShardMapManager** nesnesi kullanılarak yapılandırılmıştır bir [Fabrika](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) düzeni. Merhaba  **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**  yöntemi alır (Merhaba sunucu adını ve veritabanı adını hello GSM bulunduran dahil) kimlik bilgilerini hello biçiminde bir  **ConnectionString** ve bir örneğini döndüren bir **ShardMapManager**.  

**Lütfen dikkat edin:** hello **ShardMapManager** hello başlatma kodundaki bir uygulama için uygulama etki alanı başına yalnızca bir kez örneğinin oluşturulması. Oluşturma ek ShardMapManager durumlarda Merhaba, aynı appdomain sonuçlanacak artan bellek ve CPU kullanımını Merhaba uygulaması. A **ShardMapManager** parça eşlemelerinin herhangi bir sayı içerebilir. Bir tek parça eşleme birçok uygulama için yeterli olabilir, ancak veritabanlarının farklı kümeleri farklı şema veya benzersiz amacıyla kullanıldığında zamanlar vardır; Bu gibi durumlarda birden fazla parça eşlemeleri tercih edilebilir. 

Bu kodda tooopen var olan bir uygulama çalışırsa **ShardMapManager** hello ile [TryGetSqlShardMapManager yöntemi](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).  Varsa bir genel temsil eden nesneler **ShardMapManager** (GSM) sağlamadığı henüz hello veritabanı içinde var, hello istemci kitaplığı oluşturur bunları orada hello kullanarak [CreateSqlShardMapManager yöntemi](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).

    // Try tooget a reference toohello Shard Map Manager 
     // via hello Shard Map Manager database.  
    // If it doesn't already exist, then create it. 
    ShardMapManager shardMapManager; 
    bool shardMapManagerExists = ShardMapManagerFactory.TryGetSqlShardMapManager(
                                        connectionString, 
                                        ShardMapManagerLoadPolicy.Lazy, 
                                        out shardMapManager); 

    if (shardMapManagerExists) 
     { 
        Console.WriteLine("Shard Map Manager already exists");
    } 
    else
    {
        // Create hello Shard Map Manager. 
        ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
        Console.WriteLine("Created SqlShardMapManager"); 

        shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

        // hello connectionString contains server name, database name, and admin credentials 
        // for privileges on both hello GSM and hello shards themselves.
    } 

Alternatif olarak, Powershell toocreate yeni parça eşleme Yöneticisi kullanabilirsiniz. Bir örneği, kullanılabilir [burada](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

## <a name="get-a-rangeshardmap-or-listshardmap"></a>RangeShardMap veya ListShardMap Al
Bir parça eşleme Yöneticisi oluşturduktan sonra hello alabilirsiniz [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) veya [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) hello kullanarak [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [ TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), veya hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) yöntemi.

    /// <summary>
    /// Creates a new Range Shard Map with hello specified name, or gets hello Range Shard Map if it already exists.
    /// </summary>
    public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
    {
        // Try tooget a reference toohello Shard Map.
        RangeShardMap<T> shardMap;
        bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

        if (shardMapExists)
        {
            ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
        }
        else
        {
            // hello Shard Map does not exist, so create it
            shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
            ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
        }

        return shardMap;
    } 

### <a name="shard-map-administration-credentials"></a>Parça eşleme yönetim kimlik bilgileri
Yönetmek ve parça eşlemeleri işlemek hello parça eşlemeleri tooroute bağlantılarını kullanan olanlardan farklı uygulamalarıdır. 

tooadminister parça eşlemeleri (ekleme veya değiştirme parça parça eşlemeleri, parça eşlemeleri, vb.) hello oluşturmalıdır **ShardMapManager** kullanarak **sahip kimlik bilgileri okuma/yazma hem hello GSM veritabanı ve her ayrıcalıklarını Parça hizmet veren veritabanı**. Parça eşleme bilgisi girilen ya da üzerinde yeni parça LSM tablo oluşturma için olduğu gibi değiştirilmiş hello kimlik bilgileri hem hello hello tablolarda karşı yazmalar için GSM ve LSM izin vermeniz gerekir.  

Bkz: [kimlik bilgileri kullanılan tooaccess hello esnek veritabanı istemci Kitaplığı](sql-database-elastic-scale-manage-credentials.md).

### <a name="only-metadata-affected"></a>Yalnızca etkilenen meta veriler
Doldurma veya hello değiştirmek için kullanılan yöntemleri **ShardMapManager** veri hello parça kendilerini depolanan hello kullanıcı verilerini alter değil. Örneğin, yöntemler gibi **CreateShard**, **DeleteShard**, **UpdateMapping**, vb. hello parça eşlemesi meta verileri yalnızca etkiler. Bunlar kaldırmayın, ekleyebilir veya hello parça bulunan kullanıcı verileri alter. Bunun yerine, bu yöntemleri kullanılan tasarlanmış toobe olan ayrı işlemleri ile birlikte toocreate gerçekleştirmek veya gerçek veritabanlarını kaldırmanız ya da bu taşıma parçalı bir ortamda bir parça tooanother toorebalance satırlar.  (Merhaba **bölünmüş birleştirme** esnek veritabanı araçları ile içerdiği aracı yapar parça arasında gerçek veri taşıma yönetme yanı sıra bu API'leri kullanın.) Bkz: [ölçeklendirme hello esnek veritabanı bölünmüş-birleştirme aracını kullanarak](sql-database-elastic-scale-overview-split-and-merge.md).

## <a name="populating-a-shard-map-example"></a>Bir parça eşleme örneği doldurma
Bir örnek dizisi işlemleri toopopulate belirli parça eşleme, aşağıda gösterilmiştir. Merhaba kod aşağıdaki adımları gerçekleştirir: 

1. Yeni bir parça eşleme parça eşleme manager içinde oluşturulur. 
2. iki farklı parça Hello meta verilerini toohello parça eşleme eklenir. 
3. Anahtar aralığı eşlemeleri çeşitli eklenir ve hello genel içeriği hello parça eşleme görüntülenir. 

böylece bir hata oluşursa hello yöntemi yeniden çalıştırılabilir hello kodu yazılır. Her istek bir parça olup olmadığını sınar veya eşleme zaten var, toocreate denemeden önce onu. Merhaba kod veritabanları adlı varsayar **sample_shard_0**, **sample_shard_1** ve **sample_shard_2** dizesitarafındanbaşvurulanhelloServer'dakizatenoluşturulmuş**shardServer**. 

    public void CreatePopulatedRangeMap(ShardMapManager smm, string mapName) 
        {            
            RangeShardMap<long> sm = null; 

            // check if shardmap exists and if not, create it 
            if (!smm.TryGetRangeShardMap(mapName, out sm)) 
            { 
                sm = smm.CreateRangeShardMap<long>(mapName); 
            } 

            Shard shard0 = null, shard1=null; 
            // Check if shard exists and if not, 
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetShard(new ShardLocation(
                                     shardServer, 
                                     "sample_shard_0"), 
                                     out shard0)) 
            { 
                Shard0 = sm.CreateShard(new ShardLocation(
                                            shardServer, 
                                            "sample_shard_0")); 
            } 

            if (!sm.TryGetShard(new ShardLocation(
                                    shardServer, 
                                    "sample_shard_1"), 
                                    out shard1)) 
            { 
                Shard1 = sm.CreateShard(new ShardLocation(
                                             shardServer, 
                                            "sample_shard_1"));  
            } 

            RangeMapping<long> rmpg=null; 

            // Check if mapping exists and if not,
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetMappingForKey(0, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                          new RangeMappingCreationInfo<long>
                          (new Range<long>(0, 50), 
                          shard0, 
                          MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(50, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(50, 100), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(100, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long>
                         (new Range<long>(100, 150), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(150, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(150, 200), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(200, out rmpg)) 
            { 
               sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(200, 300), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            // List hello shards and mappings 
            foreach (Shard s in sm.GetShards()
                         .OrderBy(s => s.Location.DataSource)
                         .ThenBy(s => s.Location.Database))
            { 
               Console.WriteLine("shard: "+ s.Location); 
            } 

            foreach (RangeMapping<long> rm in sm.GetMappings()) 
            { 
                Console.WriteLine("range: [" + rm.Value.Low.ToString() + ":" 
                        + rm.Value.High.ToString()+ ")  ==>" +rm.Shard.Location); 
            } 
        } 

Tooachieve hello PowerShell kullanabileceğiniz alternatif komutlar aynı sonuçlanır. Merhaba örnek PowerShell örnekleri bazıları kullanılabilir [burada](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).     

Parça eşlemeleri doldurulduğunu sonra veri erişimi uygulamaları oluşturulabilir veya toowork hello Haritalar ile uyarlanan. Doldurma veya hello eşlemeleri düzenleme gerçekleşmediği kadar yeniden **harita düzeni** toochange gerekir.  

## <a name="data-dependent-routing"></a>Verilere bağımlı yönlendirme
Merhaba parça eşleme Yöneticisi en veritabanı bağlantılarını tooperform hello uygulamaya özgü verileri işlemleri gerektiren uygulamalarda kullanılır. Bu bağlantılar hello doğru veritabanı ile ilişkilendirilmiş olması gerekir. Bu olarak bilinir **veri bağımlı yönlendirme**. Bu uygulamalar için hello Fabrika hello GSM veritabanında salt okunur erişime sahip kimlik bilgilerini kullanarak bir parça eşleme Yöneticisi nesneden örneği oluşturur. Daha sonraki bağlantılar için istekleri ayrı ayrı toohello uygun parça veritabanına bağlanmak için gereken kimlik bilgilerini sağlayın.

Unutmayın bu uygulamaları (kullanarak **ShardMapManager** salt okunur kimlik bilgileriyle açılan) değişiklik toohello eşlemeleri veya eşlemeleri. Bu ihtiyaçları için özel yönetim uygulamalarını ya da daha önce bahsedildiği gibi daha yüksek ayrıcalıklı kimlik bilgilerini sağlamanız PowerShell komut dosyaları oluşturun. Bkz: [kimlik bilgileri kullanılan tooaccess hello esnek veritabanı istemci Kitaplığı](sql-database-elastic-scale-manage-credentials.md).

Daha fazla ayrıntı için bkz: [veri bağımlı yönlendirme](sql-database-elastic-scale-data-dependent-routing.md). 

## <a name="modifying-a-shard-map"></a>Parça eşlemeyi değiştirme
Parça eşleme farklı şekilde değiştirilebilir. Tüm yöntemleri aşağıdaki hello hello parça ve bu nesnelerin eşlemelerini açıklayan hello meta verilerini değiştirmek ancak fiziksel olarak veri hello parça içinde değiştirmeyin ve bunlar oluşturmak veya hello gerçek veritabanlarını silin.  Aşağıda açıklanan hello parça eşleme hello işlemleri bazıları, fiziksel olarak veri taşıma veya ekleyin ve parça hizmet veren veritabanlarını kaldırmanız yönetim eylemleri ile eşgüdümlü toobe gerekebilir.

Bu yöntemler hello yapı taşları değiştirmek için kullanılabilir olarak birlikte çalışan hello parçalı veritabanı ortamınızdaki verilerin genel dağıtım.  

* tooadd veya kaldırma parça: kullanmak  **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)**  ve  **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)**  Merhaba, [Shardmap sınıfı](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx). 
  
    Merhaba sunucu ve veritabanı hello hedef parça temsil eden bu işlemleri tooexecute için varolmalıdır. Bu yöntemlerin herhangi bir etki hello veritabanlarında kendileri yalnızca meta veri hello parça eşlemesindeki üzerinde sahip değilsiniz.
* toocreate veya kaldırma noktaları veya aralıklarını eşlenen toohello parça: kullanmak  **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**,  **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)**  Merhaba, [RangeShardMapping sınıfı](https://msdn.microsoft.com/library/azure/dn807318.aspx), ve  **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)**  Merhaba, [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)
  
    Birçok farklı noktaları veya aralıklar eşlenen toohello olabilir aynı parça. Bu yöntemler, yalnızca meta veri etkiler - zaten parça içinde bulunabilecek herhangi bir veri etkilemez. Veri sırası toobe ile tutarlı hello veritabanından kaldırılmış toobe gerekip gerekmediğini **DeleteMapping** işlemleri ayrı olarak, ancak bu yöntemleri kullanarak ile birlikte bu işlemler tooperform gerekir.  
* iki veya tek bir birleştirme bitişik aralıkları toosplit varolan aralıkları: kullanmak  **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)**  ve  **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.  
  
    Bölme ve birleştirme işlemlerinin unutmayın **hello parça toowhich anahtar değerleri eşlendi değiştirmeyin**. Bölme iki bölüme var olan bir aralığı keser, ancak hem eşleşen toohello olarak bırakır aynı parça. Bir birleştirme zaten eşlenmiş toohello olan iki bitişik aralıkları çalışır tek bir aralığa birleştirmesi aynı parça.  Merhaba noktaları veya aralıklar kendilerini parça arasında hareketini gereken kullanarak Eşgüdümlü toobe **UpdateMapping** gerçek veri taşıma birlikte.  Merhaba kullanabilirsiniz **bölünmüş/Merge** hizmetinin esnek veritabanı parçası olan araçlar toocoordinate parça eşleme veri taşıma değişikliklerle taşıması gerektiğinde. 
* toore eşleme (veya taşıma) tek tek nokta veya aralıklar toodifferent parça: kullanmak  **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.  
  
    Verileri bir parça tooanother sipariş toobe ile tutarlı olarak taşınmıştır toobe gerekebileceği **UpdateMapping** işlemleri tooperform ayrı olarak, ancak bu yöntemleri kullanarak ile birlikte bu taşıması gerekir.
* tootake eşlemeleri çevrimiçi ve çevrimdışı: kullanmak  **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)**  ve  **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)**  toocontrol hello çevrimiçi durumunu bir eşleme. 
  
    Bir eşleme "Çevrimdışı" bir durumda olduğunda parça eşlemeleri üzerindeki belirli işlemlerin yalnızca verilir dahil olmak üzere **UpdateMapping** ve **DeleteMapping**. Bir eşleme çevrimdışı olduğunda, o eşlemeye dahil bir anahtarı temel alan bir veri bağımlı istek bir hata döndürür. Ayrıca, bir aralık önce çevrimdışı duruma getirildiğinde, tüm bağlantılar etkilenen toohello parça otomatik olarak sonlandırıldı sonuçlarında sipariş tooprevent tutarsız veya tamamlanmamış değiştirilmesini aralıkları karşı yönlendirilmiş sorgular için. 

Eşlemeleri .net içinde değişmez nesneleridir.  Tüm eşlemelerini değiştirmek hello yöntemleri yukarıdaki da kodunuzdaki tüm başvuruları toothem geçersiz. toomake bir eşlemeyi değiştirmek hello yöntemleri tümünün eşleme 's durumunu değiştirme işlemleri daha kolay tooperform dizilerini dönüş yeni bir BT işlemleri yapılabilmesi için başvuru, eşleme. Örneğin, mevcut bir başlangıç anahtarı 25 içeren shardmap sm içinde eşleme toodelete aşağıdaki hello çalıştırabilirsiniz: 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a>Bir parça ekleme
Uygulamaları parça eşleme zaten var için toosimply yeni anahtarlar veya anahtar aralıkları, beklenen yeni parça toohandle veriler genellikle eklemeniz. Örneğin, Kiracı kimliği tarafından parçalı bir uygulama için yeni bir kiracı tooprovision yeni bir parça gerekebilir veya veri parçalı aylık yeni her ay hello başlamadan önce sağlanan yeni bir parça gerekebilir. 

Anahtar değerlerinin Hello yeni aralık zaten yoksa varolan eşlemesini ve hiçbir veri taşıma parçası çok basit tooadd hello yeni parça olduğu gereklidir ve hello yeni bir anahtar ya da aralığı toothat parça ilişkilendirebilirsiniz. Yeni parça ekleme hakkında daha fazla bilgi için bkz: [yeni bir parça eklemek](sql-database-elastic-scale-add-a-shard.md).

Veri taşıma gerektiren senaryolar için ancak hello bölünmüş birleştirme gerekli tooorchestrate hello veri taşıma hello gerekli parça eşleme güncelleştirmeleri ile birlikte parça arasında aracıdır. Bölünmüş birleştirme yool kullanımıyla ilgili ayrıntılar hello için bkz: [bölünmüş birleştirme genel bakış](sql-database-elastic-scale-overview-split-and-merge.md) 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
