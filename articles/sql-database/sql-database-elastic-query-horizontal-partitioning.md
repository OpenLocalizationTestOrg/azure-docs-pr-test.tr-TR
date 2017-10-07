---
title: "ölçeklendirilen bulut veritabanları arasında aaaReporting | Microsoft Docs"
description: "nasıl tooset yatay bölümleri esnek sorguları ayarlama"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: f86eccb8-6323-4ba7-8559-8a7c039049f3
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: mlandzic
ms.openlocfilehash: 78986c2040bf308195bf7c77e64d4f37273fcf36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a>Raporlama ölçeklendirilmiş bulut veritabanları arasında (Önizleme)
![Parça sorgulama][1]

Parçalı veritabanları dağıtmak satırları genişletilmiş bir veri katmanı. Yatay bölümleme olarak da bilinen tüm katılımcı veritabanlarında Hello şema aynıdır. Esnek bir sorgu kullanarak, tüm veritabanları parçalı bir veritabanında span raporlar oluşturabilirsiniz.

Hızlı Başlangıç için bkz: [ölçeklendirilmiş bulut veritabanları arasında raporlama](sql-database-elastic-query-getting-started.md).

Parçalı dışı veritabanları için bkz: [sorgu farklı şemalarda bulut veritabanları arasında](sql-database-elastic-query-vertical-partitioning.md). 

## <a name="prerequisites"></a>Ön koşullar
* Merhaba esnek veritabanı istemci kitaplığı kullanılarak bir parça Haritası oluşturun. bkz: [parça eşleme Yönetim](sql-database-elastic-scale-shard-map-management.md). Veya hello örnek uygulamasında kullanma [esnek veritabanı araçlarını kullanmaya başlama](sql-database-elastic-scale-get-started.md).
* Alternatif olarak, bkz: [geçirme varolan veritabanları tooscaled kullanıma veritabanları](sql-database-elastic-convert-to-use-elastic-tools.md).
* Merhaba kullanıcı ALTER ANY dış veri KAYNAĞINA iznine sahip olması gerekir. Bu izni hello ALTER DATABASE iznine dahil edilir.
* ALTER ANY dış veri kaynağı, veri kaynağı arka plandaki gerekli toorefer toohello izinlerdir.

## <a name="overview"></a>Genel Bakış
Bu deyimler hello meta veri gösterimi parçalı veriler katman hello esnek sorgu veritabanında oluşturun. 

1. [ANA ANAHTAR OLUŞTURMA](https://msdn.microsoft.com/library/ms174382.aspx)
2. [VERİTABANI KAPSAMLI OLUŞTURMAK KİMLİK BİLGİSİ](https://msdn.microsoft.com/library/mt270260.aspx)
3. [DIŞ VERİ KAYNAĞI OLUŞTURUN](https://msdn.microsoft.com/library/dn935022.aspx)
4. [DIŞ TABLO OLUŞTURMA](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a>1.1 kapsamlı veritabanı ana anahtarı ve kimlik bilgileri oluşturun
Merhaba kimlik bilgisi hello esnek sorgu tooconnect tooyour Uzak veritabanı tarafından kullanılır.  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> Bu hello emin olun *"\<kullanıcıadı\>"* içermez *"@servername"* soneki. 
> 
> 

## <a name="12-create-external-data-sources"></a>1.2 dış veri kaynakları oluşturun
Sözdizimi:

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a>Örnek
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

Hello geçerli dış veri kaynaklarının listesini alın: 

    select * from sys.external_data_sources; 

Parça haritanızı Hello dış veri kaynağına başvuruyor. Esnek bir sorgu daha sonra hello dış veri kaynağı ve hello veri katmanındaki katılmak parça eşleme tooenumerate hello veritabanları temel hello kullanır. Merhaba aynı kimlik bilgileri kullanılan tooread hello parça eşleme ve esnek bir sorgu hello işlenmesi sırasında hello parça verileri tooaccess hello. 

## <a name="13-create-external-tables"></a>1.3 dış tabloları oluşturma
Sözdizimi:  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

**Örnek**

    CREATE EXTERNAL TABLE [dbo].[order_line]( 
         [ol_o_id] int NOT NULL, 
         [ol_d_id] tinyint NOT NULL,
         [ol_w_id] int NOT NULL, 
         [ol_number] tinyint NOT NULL, 
         [ol_i_id] int NOT NULL, 
         [ol_delivery_d] datetime NOT NULL, 
         [ol_amount] smallmoney NOT NULL, 
         [ol_supply_w_id] int NOT NULL, 
         [ol_quantity] smallint NOT NULL, 
         [ol_dist_info] char(24) NOT NULL 
    ) 

    WITH 
    ( 
        DATA_SOURCE = MyExtSrc, 
         SCHEMA_NAME = 'orders', 
         OBJECT_NAME = 'order_details', 
        DISTRIBUTION=SHARDED(ol_w_id)
    ); 

Dış tablolara Hello listesi hello geçerli veritabanından: 

    SELECT * from sys.external_tables; 

toodrop dış tablolar:

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a>Açıklamalar
Merhaba veri\_SOURCE yan tümcesinde hello dış tablo için kullanılan hello dış veri kaynağı (parça eşleme) tanımlar.  

Merhaba şema\_adı ve nesne\_adı yan tümceleri hello dış tablo tanımı tooa farklı bir şema tablosunda eşleyin. Atlanırsa, hello şema hello uzak nesnesinin toobe "dbo" kabul edilir ve adıyla tanımlanan toobe aynı toohello dış tablo adı varsayılır. Bu, uzak tablo hello adını toocreate hello dış tablo istediğiniz hello veritabanında zaten alınmış yararlıdır. Örneğin, bir dış tablo tooget Katalog görünümleri birleşik bir görünümünü toodefine istediğiniz veya genişletilmiş verileriniz üzerinde Dmv'leri katmanı. Katalog görünümleri ve Dmv'leri zaten yerel olarak mevcut olduğundan, adları hello dış tablo tanımı için kullanamazsınız. Bunun yerine, farklı bir ad kullanın ve hello katalog görünümün kullanın veya hello şema DMV'ın adı hello\_adı ve/veya nesne\_adı yan tümceleri. (Merhaba örneğe bakın.) 

Merhaba dağıtım yan tümcesi Bu tablo için kullanılan hello veri dağılımını belirtir. Merhaba Sorgu işlemcisi hello dağıtım yan tümcesi toobuild hello en verimli sorgu planında sağlanan hello bilgileri kullanır.  

1. **PARÇALI** veri hello veritabanları arasında yatay olarak bölümlenmiş anlamına gelir. Merhaba veri dağıtım hello için bölümlendirme anahtarı hello **< sharding_column_name >** parametresi.
2. **ÇOĞALTILAN** özdeş kopyalarını Merhaba tablonun her veritabanını mevcut olduğu anlamına gelir. Bu, sorumluluk tooensure hello çoğaltmaları hello veritabanları arasında aynı olduğundan emin olur.
3. **YUVARLAK\_deneme** hello tablosunun yatay olarak bir uygulama bağımlı dağıtım yöntemini kullanılarak bölümlenmiş anlamına gelir. 

**Veri katmanı başvuru**: hello dış tablo DDL tooan dış veri kaynağına başvuruyor. Merhaba dış veri kaynağına hello bilgi gerekli toolocate ile veri katmanındaki tüm hello veritabanları hello dış tablo sağlayan bir parça eşleme belirtir. 

### <a name="security-considerations"></a>Güvenlikle ilgili dikkat edilmesi gerekenler
Erişim toohello dış tablo kullanıcılarla otomatik olarak toohello temel alınan uzak tablolar hello dış veri kaynağı tanımına verilen hello kimlik bilgileri altında erişin. İstenmeyen ayrıcalıkların hello kimlik bilgisi hello dış veri kaynağının aracılığıyla kaçının. Yalnızca dizinindeymiş gibi olağan bir tablo için bir dış tablo GRANT veya REVOKE kullanın.  

Dış veri kaynağınızda ve dış tablolarınızı tanımladıktan sonra artık dış tablolar üzerindeki tam T-SQL kullanabilirsiniz.

## <a name="example-querying-horizontal-partitioned-databases"></a>Örnek: yatay bölümlenmiş veritabanlarını sorgulama
Merhaba aşağıdaki sorguyu ambarları, sipariş ve sipariş satırları arasında üç yönlü birleştirme gerçekleştirir ve birkaç toplar ve seçmeli bir filtre kullanır. (1) yatay bölümleme (parçalama) ve ambarları, sipariş ve sipariş satırları hello ambar kimliği sütuna göre parçalı ve hello esnek sorgulayan hello birleştirmeler hello parça üzerinde birlikte bulunmasına ve hello pahalı hello hello sorgusunun parçası işleme (2) olduğunu varsayar Paralel parça. 

    select  
         w_id as warehouse,
         o_c_id as customer,
         count(*) as cnt_orderline,
         max(ol_quantity) as max_quantity,
         avg(ol_amount) as avg_amount, 
         min(ol_delivery_d) as min_deliv_date
    from warehouse 
    join orders 
    on w_id = o_w_id
    join order_line 
    on o_id = ol_o_id and o_w_id = ol_w_id 
    where w_id > 100 and w_id < 200 
    group by w_id, o_c_id 

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a>Saklı yordamı uzaktan T-SQL yürütmesi için: sp\_execute_remote
Esnek sorgu aynı zamanda toohello parça doğrudan erişim sağlayan bir saklı yordam sunar. Merhaba saklı yordam adı verilir [sp\_yürütme \_uzak](https://msdn.microsoft.com/library/mt703714) ve kullanılan tooexecute uzak saklı yordamları veya T-SQL kodunu hello Uzak veritabanı üzerinde çalıştırılabilir. Şu parametreler hello alır: 

* Veri kaynağı adı (nvarchar): hello dış veri kaynağı türü RDBMS hello adı. 
* Sorgu (nvarchar): hello T-SQL sorgusu toobe her parça üzerinde yürütülür. 
* Parametre bildirimi (nvarchar) - isteğe bağlı: dize veri türü tanımları (gibi sp_executesql) hello Sorgu parametresinde kullanılan hello parametreler için. 
* Parametre değeri listesi - isteğe bağlı: parametre değerleri (gibi sp_executesql) virgülle ayrılmış listesi.

Merhaba sp\_yürütme\_uzak kullanır hello hello çağırma parametreleri tooexecute hello T-SQL deyimini hello uzak veritabanlarında verilen sağlanan dış veri kaynağı. Merhaba dış veri kaynağı tooconnect toohello shardmap manager veritabanı ve hello uzak veritabanlarına hello kimlik bilgisi kullanır.  

Örnek: 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a>Bağlantı için araçları
Normal SQL Server bağlantı dizelerini tooconnect kullanın, uygulamanızın, BI ve veri tümleştirme araçları toohello veritabanınızla, dış tablo tanımlarını. SQL Server, aracı için bir veri kaynağı olarak desteklendiğinden emin olun. Hello esnek sorgu veritabanını diğer SQL Server veritabanına bağlı toohello araçları gibi başvuru ve yerel tablolar değilmiş gibi aracı veya uygulamadan gelen dış tabloları kullanır. 

## <a name="best-practices"></a>En iyi uygulamalar
* Merhaba esnek sorgu uç veritabanı erişim toohello shardmap veritabanı ve tüm parça hello SQL DB güvenlik duvarları üzerinden verilip verilmediğini emin olun.  
* Merhaba veri dağıtım hello dış tablo tarafından tanımlanan zorunlu veya doğrulayın. Gerçek veri dağıtımınız farklıysa, tablo tanımında belirtilen hello dağıtım sorgularınızı beklenmeyen sonuçlar. 
* Merhaba parçalama anahtarı üzerinden koşulları toosafely dışlama izin verir, esnek sorgu şu anda parça eleme belirli parça işlenmesini gerçekleştirmez.
* Esnek sorgu hello hesaplama çoğunu hello parça üzerinde nerede yapılabilir sorguları için en iyi şekilde çalışır. Genellikle hello en iyi sorgu performansını değerlendirilebilir seçmeli filtre koşulları ile Merhaba parça veya birleştirmeler üzerinde bir bölüme göre hizalı şekilde tüm parça üzerinde gerçekleştirilen anahtarları bölümleme hello üzerinden alırsınız. Diğer sorgu desenlerine tooload büyük miktarlarda veri hello parça toohello baş düğümünden gerekebilir ve kötü gerçekleştirebilir.

## <a name="next-steps"></a>Sonraki adımlar

* Esnek sorgu genel bakış için bkz: [esnek sorgu genel bakış](sql-database-elastic-query-overview.md).
* Dikey bölümleme öğretici için bkz: [(dikey bölümleme) veritabanları arası sorgusu ile çalışmaya başlama](sql-database-elastic-query-getting-started-vertical.md).
* Dikey olarak bölümlenmiş verilere ilişkin söz dizimi ve örnek sorgular için bkz: [dikey sorgulama bölümlenmiş veri)](sql-database-elastic-query-vertical-partitioning.md)
* Yatay bölümleme (parçalama) bir öğretici için bkz: [yatay (parçalama) bölümleme için esnek sorgu ile çalışmaya başlama](sql-database-elastic-query-getting-started.md).
* Bkz: [sp\_yürütme \_uzak](https://msdn.microsoft.com/library/mt703714) tek uzaktan Azure SQL veritabanı ya da yatay bölümleme düzenindeki parça olarak hizmet veren bir veritabanları kümesi üzerinde bir Transact-SQL deyimini yürütür bir saklı yordam için.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
