---
title: "Esnek veritabanı araçlarını ve satır düzeyi güvenlik ile aaaMulti Kiracı uygulamaları"
description: "Nasıl toouse esnek veritabanı araçları ile birlikte satır güvenlik toobuild çok kiracılı parça destekleyen bir Azure SQL veritabanı yüksek düzeyde ölçeklenebilir veri katmanı ile bir uygulama düzeyi öğrenin."
metakeywords: azure sql database elastic tools multi tenant row level security rls
services: sql-database
documentationcenter: 
manager: jhubbard
author: tmullaney
ms.assetid: e72d3cfe-e9be-4326-b776-9c6d96c0a18e
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: thmullan;torsteng
ms.openlocfilehash: e00076a8db4a295374993aedd49f2318bd4d701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="multi-tenant-applications-with-elastic-database-tools-and-row-level-security"></a>Çok kiracılı uygulamalarla esnek veritabanı araçlarını ve satır düzeyi güvenlik
[Esnek veritabanı araçlarını](sql-database-elastic-scale-get-started.md) ve [satır düzeyi güvenlik (RLS)](https://msdn.microsoft.com/library/dn765131) güçlü bir esnek ve verimli bir şekilde hello veri katmanı Azure SQL veritabanı olan bir çok kiracılı uygulama ölçeklendirme için özellik kümesi sunar. Bkz: [Azure SQL veritabanı ile çok kiracılı SaaS uygulamaları için Tasarım desenleri](sql-database-design-patterns-multi-tenancy-saas-applications.md) daha fazla bilgi için. 

Bu makalede gösterilmektedir nasıl toouse bu teknolojiler birlikte toobuild kullanarak çok kiracılı parça destekleyen bir yüksek düzeyde ölçeklenebilir veri katmanı uygulamayla **ADO.NET SqlClient** ve/veya **Entity Framework**.  

* **Esnek veritabanı araçlarını** geliştiriciler tooscale hello veri katmanı .NET kitaplıkları ve Azure hizmet şablonları kümesini kullanarak endüstri standardı parçalama yöntemler aracılığıyla bir uygulamanın çıkışı sağlar. Hello esnek veritabanı istemci kitaplığını kullanarak parça yönetme otomatikleştirmek ve birçok hello infrastructural görev genellikle parçalama ile ilişkili akıcı hale getirmesine yardımcı olur. 
* **Satır düzeyi güvenlik** hello aynı veritabanında bir sorgu yürütülürken toohello Kiracı ait olmayan satırlar çıkışı güvenlik ilkeleri toofilter kullanarak birden çok kiracılar için geliştiricilere toostore veri sağlar. RLS ile erişim mantığı hello veritabanı içinde merkezileştirme yerine hello uygulamada bakım basitleştirir ve bir uygulamanın codebase gibi hata hello riskini azaltır daha artar. 

Bunlar kullanarak özellikleri birlikte, bir uygulama birden çok hello aynı Kiracı için veri depolayarak maliyet tasarrufu ve verimliliği elde eder yararlanabilir parça veritabanı. Merhaba aynı zamanda, hala bir uygulama tek Kiracı parça daha sıkı performans garanti çok kiracılı parça kiracılar arasında eşit kaynak dağıtım garanti etmiyoruz beri duyan "premium" kiracılar için ayrık hello esneklik toooffer sahiptir.  

Kısacası, esnek veritabanı istemci kitaplığının hello [veri bağımlı yönlendirme](sql-database-elastic-scale-data-dependent-routing.md) API'leri kendi parçalama anahtarı (genellikle bir "Tenantıd") içeren kiracılar toohello doğru parça veritabanı otomatik olarak bağlan. Bağlantı kurulduktan sonra bir RLS güvenlik ilkesinde hello veritabanı kiracılar kendi Tenantıd içeren satırları yalnızca erişebilmesini sağlar. Tüm tabloları hangi satırların tooeach Kiracı ait Tenantıd sütun tooindicate içeren varsayılır. 

![Blog uygulama mimarisi][1]

## <a name="download-hello-sample-project"></a>Merhaba örnek projesini indirin
### <a name="prerequisites"></a>Ön koşullar
* Visual Studio (2012 veya sonraki sürümlerini) kullanın 
* Üç Azure SQL veritabanı oluşturma 
* Örnek projesini indirin: [Azure SQL - çok Kiracılı parça için esnek veritabanı araçları](http://go.microsoft.com/?linkid=9888163)
  * Veritabanlarınızı hello başında hello bilgileri doldurun **Program.cs** 

Bu proje bir açıklanan hello genişletir [Azure SQL - Entity Framework tümleştirme için esnek DB Araçları](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) çok kiracılı parça veritabanları için destek ekleyerek düzenleyin. Bloglar ve gönderileri, dört kiracılar ve hello Yukarıdaki diyagramda gösterildiği gibi iki çok kiracılı parça veritabanlarıyla oluşturmak için basit bir konsol uygulaması oluşturur. 

Derleme ve hello uygulamayı çalıştırın. Bu işlem hello esnek veritabanı araçlarını parça eşleme Yöneticisi ve testleri aşağıdaki çalışma hello bootstrap: 

1. Entity Framework ve LINQ kullanarak yeni bir blog oluşturun ve ardından her bir kiracı için tüm Web Günlüklerini Görüntüle
2. ADO.NET SqlClient kullanarak, bir kiracı için tüm Web Günlüklerini Görüntüle
3. Tooinsert bir hata durum hello yanlış Kiracı tooverify için bir blog deneyin  

RLS hello parça veritabanlarında henüz etkinleştirilmemiş olduğundan, bu testler, her bir sorun ortaya dikkat edin: kiracılar olan toothem ait değil mümkün toosee bloglar ve Merhaba uygulaması, bir blog hello yanlış Kiracı için ekleme değil engellenir. Merhaba bu makalenin sonraki bölümlerinde tooresolve zorlayarak bu sorunların nasıl Kiracı açıklar yalıtım RLS ile. İki adımı vardır: 

1. **Uygulama katmanı**: hello uygulama kodunu değiştirme tooalways kümesi hello hello SESSION_CONTEXT içinde geçerli Tenantıd bağlantı açıldıktan sonra. Merhaba örnek proje zaten bu yapmıştır. 
2. **Veri katmanı**: Tenantıd hello üzerinde alarak satırları SESSION_CONTEXT içinde depolanan her parça veritabanı toofilter RLS güvenlik ilkesi oluşturun. Toodo bu her parça veritabanlarınız için gerekir, aksi durumda çok kiracılı parça satırlarda değil filtrelenir. 

## <a name="step-1-application-tier-set-tenantid-in-hello-sessioncontext"></a>1. adım) uygulama katmanı: Merhaba SESSION_CONTEXT içinde Tenantıd ayarlayın
Bağımlı yönlendirme API'leri, hello uygulama hala hello esnek veritabanı istemci kitaplığının verileri kullanarak bağlanan tooa parça veritabanının tootell hello veritabanı gereken sonra RLS güvenlik ilkesi satırları filtreleyebilirsiniz böylece hangi Tenantıd o bağlantı kullanıyor tooother kiracılar ait. Bu bilgiler önerilen yöntem toopass hello toostore hello hello Bu bağlantı için geçerli bir Tenantıd [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx). (Not: alternatif olarak kullanabileceğinizi [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), ancak SESSION_CONTEXT daha iyi bir seçenek daha kolay toouse olduğundan, varsayılan değer olarak NULL döndürür ve anahtar-değer çiftleri destekler.)

### <a name="entity-framework"></a>Entity Framework
Entity Framework kullanan uygulamalar için hello kolay SESSION_CONTEXT ElasticScaleContext geçersiz kılma hello içinde açıklanan tooset hello yaklaşımdır [EF DbContext kullanarak veri bağımlı yönlendirme](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext). Veri bağımlı Yönlendirme aracılığıyla aracılı hello bağlantı dönmeden önce oluşturun ve o bağlantı için belirtilen hello SESSION_CONTEXT toohello shardingKey 'Tenantıd' ayarlar SqlCommand yürütün. Tooset hello sonra SESSION_CONTEXT bu şekilde, yalnızca toowrite kod gerekir. 

```
// ElasticScaleContext.cs 
// ... 
// C'tor for data dependent routing. This call will open a validated connection routed toohello proper 
// shard by hello shard map manager. Note that hello base class c'tor call will fail for an open connection 
// if migrations need toobe done and SQL credentials are used. This is hello reason for hello  
// separation of c'tors into hello DDR case (this c'tor) and hello internal c'tor for new shards. 
public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
    : base(OpenDDRConnection(shardMap, shardingKey, connectionStr), true /* contextOwnsConnection */)
{
}

public static SqlConnection OpenDDRConnection(ShardMap shardMap, T shardingKey, string connectionStr)
{
    // No initialization
    Database.SetInitializer<ElasticScaleContext<T>>(null);

    // Ask shard map toobroker a validated connection for hello given key
    SqlConnection conn = null;
    try
    {
        conn = shardMap.OpenConnectionForKey(shardingKey, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT tooshardingKey tooenable Row-Level Security filtering
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"exec sp_set_session_context @key=N'TenantId', @value=@shardingKey";
        cmd.Parameters.AddWithValue("@shardingKey", shardingKey);
        cmd.ExecuteNonQuery();

        return conn;
    }
    catch (Exception)
    {
        if (conn != null)
        {
            conn.Dispose();
        }

        throw;
    }
} 
// ... 
```

Merhaba SESSION_CONTEXT ile otomatik olarak ayarlanır artık ElasticScaleContext çağrılan her hello Tenantıd belirtilen: 

```
// Program.cs 
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
{   
    using (var db = new ElasticScaleContext<int>(sharding.ShardMap, tenantId, connStrBldr.ConnectionString))   
    {     
        var query = from b in db.Blogs
                    orderby b.Name
                    select b;

        Console.WriteLine("All blogs for TenantId {0}:", tenantId);     
        foreach (var item in query)     
        {       
            Console.WriteLine(item.Name);     
        }   
    } 
}); 
```

### <a name="adonet-sqlclient"></a>ADO.NET SqlClient
ADO.NET SqlClient hello kullanarak uygulamaları yaklaşım toocreate önerilir 'Tenantıd' hello SESSION_CONTEXT toohello otomatik olarak ayarlar ShardMap.OpenConnectionForKey() çevresinde bir sarmalayıcı işlevi gidermek Tenantıd döndürmeden önce bir bağlantı. SESSION_CONTEXT her zaman ayarlanır tooensure, yalnızca bu sarmalayıcı işlevi kullanarak bağlantı açmanız gerekir.

```
// Program.cs
// ...

// Wrapper function for ShardMap.OpenConnectionForKey() that automatically sets SESSION_CONTEXT with hello correct
// tenantId before returning a connection. As a best practice, you should only open connections using this 
// method tooensure that SESSION_CONTEXT is always set before executing a query.
public static SqlConnection OpenConnectionForTenant(ShardMap shardMap, int tenantId, string connectionStr)
{
    SqlConnection conn = null;
    try
    {
        // Ask shard map toobroker a validated connection for hello given key
        conn = shardMap.OpenConnectionForKey(tenantId, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT tooshardingKey tooenable Row-Level Security filtering
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"exec sp_set_session_context @key=N'TenantId', @value=@shardingKey";
        cmd.Parameters.AddWithValue("@shardingKey", tenantId);
        cmd.ExecuteNonQuery();

        return conn;
    }
    catch (Exception)
    {
        if (conn != null)
        {
            conn.Dispose();
        }

        throw;
    }
}

// ...

// Example query via ADO.NET SqlClient
// If row-level security is enabled, only Tenant 4's blogs will be listed
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
{
    using (SqlConnection conn = OpenConnectionForTenant(sharding.ShardMap, tenantId4, connStrBldr.ConnectionString))
    {
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"SELECT * FROM Blogs";

        Console.WriteLine("--\nAll blogs for TenantId {0} (using ADO.NET SqlClient):", tenantId4);
        SqlDataReader reader = cmd.ExecuteReader();
        while (reader.Read())
        {
            Console.WriteLine("{0}", reader["Name"]);
        }
    }
});

```

## <a name="step-2-data-tier-create-row-level-security-policy"></a>2. adım) veri katmanı: satır düzeyi güvenlik ilkesi oluşturma
### <a name="create-a-security-policy-toofilter-hello-rows-each-tenant-can-access"></a>Bir güvenlik ilkesi toofilter hello her Kiracı erişebileceği satırları oluşturma
Merhaba uygulaması ile SESSION_CONTEXT ayarı göre geçerli Tenantıd hello sorgulama önce RLS güvenlik ilkesi sorgular ve filtreleyebilirsiniz farklı Tenantıd satırları çıkar.  

RLS, T-SQL uygulanır: kullanıcı tanımlı bir işlev hello erişim mantığını tanımlayan ve bu tablo işlevi tooany sayısı bir güvenlik ilkesi bağlar. Bu proje için hello işlevi yalnızca hello uygulama (yerine başka bir SQL kullanıcı) bağlı toohello veritabanıdır ve 'Tenantıd' hello SESSION_CONTEXT depolanan o hello hello belirli bir satırın Tenantıd eşleşen doğrular. Bir filtre koşulu hello filtresini seçin, UPDATE ve DELETE sorgularının üzerinden bu koşullar toopass karşılayan satırları izin verir; ve bir engelleme koşuluna eklenen veya güncelleştirilen engeller Bu koşulları ihlal satırları engeller. SESSION_CONTEXT ayarlı değil, boş ve hiçbir satır eklenen görünür mü yoksa mümkün toobe olacaktır döndürür. 

tooenable RLS, T-SQL ya da Visual Studio (SSDT), SSMS, kullanarak tüm üzerinde şu hello execute veya PowerShell Betiği hello projeye dahil hello (veya kullanıyorsanız [esnek veritabanı iş](sql-database-elastic-jobs-overview.md), tooautomate yürütme kullanın Bu T-SQL tüm parça): 

```
CREATE SCHEMA rls -- separate schema tooorganize RLS objects 
GO

CREATE FUNCTION rls.fn_tenantAccessPredicate(@TenantId int)     
    RETURNS TABLE     
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult          
        WHERE DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- hello user in your application’s connection string (dbo is only for demo purposes!)         
        AND CAST(SESSION_CONTEXT(N'TenantId') AS int) = @TenantId
GO

CREATE SECURITY POLICY rls.tenantAccessPolicy
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Blogs,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Blogs,
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Posts,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Posts
GO 
```

> [!TIP]
> Tabloları yüzlerce tooadd hello koşul gereken daha karmaşık projelerde otomatik olarak bir şemadaki tüm tablolarda bir koşul ekleme bir güvenlik ilkesi oluşturur bir yardımcı depolanan yordamı kullanabilirsiniz. Bkz: [geçerli satır düzeyi güvenlik tooall tabloları - Yardımcısı komut dosyası (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).  
> 
> 

Şimdi hello örnek uygulamayı yeniden çalıştırın, kiracılar mümkün toosee toothem ait yalnızca satır olur. Ayrıca, Merhaba uygulaması hello bir bağlı durumda toohello parça veritabanının dışında tootenants ait satır eklenemiyor ve onu görünen satır toohave farklı Tenantıd güncelleştirilemiyor. Merhaba uygulaması toodo ya da çalışırsa, bir DbUpdateException gerçekleştirilecektir.

Daha sonra yeni bir tablo eklerseniz, yalnızca ALTER güvenlik ilkesi hello ve yeni bir tablo hello üzerinde filtre ve engelleme koşulları ekleyin: 

```
ALTER SECURITY POLICY rls.tenantAccessPolicy     
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable
GO 
```

### <a name="add-default-constraints-tooautomatically-populate-tenantid-for-inserts"></a>Varsayılan ekleme kısıtlamaları tooautomatically eklemeleri için Tenantıd doldurma
Varsayılan koyabilirsiniz her tablo tooautomatically kısıtlaması doldurmak hello Tenantıd hello ile şu anda satır eklerken SESSION_CONTEXT içinde depolanan değer. Örneğin: 

```
-- Create default constraints tooauto-populate TenantId with hello value of SESSION_CONTEXT for inserts 
ALTER TABLE Blogs     
    ADD CONSTRAINT df_TenantId_Blogs      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO

ALTER TABLE Posts     
    ADD CONSTRAINT df_TenantId_Posts      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO 
```

Şimdi satır eklerken Merhaba uygulaması toospecify bir Tenantıd gerekmez: 

```
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
{   
    using (var db = new ElasticScaleContext<int>(sharding.ShardMap, tenantId, connStrBldr.ConnectionString))
    {
        var blog = new Blog { Name = name }; // default constraint sets TenantId automatically     
        db.Blogs.Add(blog);     
        db.SaveChanges();   
    } 
}); 
```

> [!NOTE]
> Bir Entity Framework projesi için varsayılan kısıtlamalar kullanırsanız, EF veri modelinizi hello Tenantıd sütun içermez önerilir. Entity Framework sorguları otomatik olarak SESSION_CONTEXT kullanan T-SQL ile oluşturulan hello varsayılan kısıtlamalar geçersiz kılar varsayılan değerleri sağlayın olmasıdır. Proje toouse varsayılan kısıtlamalar hello örnek, örneği için DataClasses.cs (ve çalışma Add-Migration hello Paket Yöneticisi konsolu içinde) Tenantıd kaldırmanız gerekir ve alan hello kullan T-SQL tooensure hello veritabanı tablolarında yalnızca mevcut. Bu şekilde EF otomatik olarak yanlış varsayılan değerler veri eklerken sağlamaz. 
> 
> 

### <a name="optional-enable-a-superuser-tooaccess-all-rows"></a>(İsteğe bağlı) Tüm satırlarda "süper kullanıcı" tooaccess etkinleştir
Bazı uygulamalar toocreate "tüm satırlar, tüm parça tüm kiracılar veya tooperform bölünmüş/birleştirme işlemleri veritabanları arasında taşıma Kiracı satırları içeren parça genelinde raporlama sipariş tooenable erişebilen örneği için bir süper kullanıcı" isteyebilirsiniz. tooenable Bu, her parça veritabanında yeni bir SQL kullanıcısının ("süper kullanıcı" Bu örnekte) oluşturmanız gerekir. Ardından bu kullanıcı tooaccess tüm satırları sağlayan yeni bir koşul işlevi hello güvenlik ilkesiyle alter:

```
-- New predicate function that adds superuser logic
CREATE FUNCTION rls.fn_tenantAccessPredicateWithSuperUser(@TenantId int)
    RETURNS TABLE
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult 
        WHERE 
        (
            DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- note, should not be dbo!
            AND CAST(SESSION_CONTEXT(N'TenantId') AS int) = @TenantId
        ) 
        OR
        (
            DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('superuser')
        )
GO

-- Atomically swap in hello new predicate function on each table
ALTER SECURITY POLICY rls.tenantAccessPolicy
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts
GO
```


### <a name="maintenance"></a>Bakım
* **Yeni parça ekleme**: tüm yeni parça üzerinde hello T-SQL komut dosyası tooenable RLS yürütmeniz gerekir, aksi takdirde bu parça sorgulamaları değil filtrelenir.
* **Yeni tablo ekleme**: Filtre eklemek ve yeni bir tablo oluşturulduğunda tüm parça koşul toohello güvenlik ilkesini engellemek, aksi takdirde hello yeni tablo sorgularında değil filtrelenir. Bu DDL tetikleyicisi kullanarak açıklandığı gibi otomatikleştirilebilir [geçerli satır düzeyi güvenlik otomatik olarak toonewly oluşturulan tabloları (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).

## <a name="summary"></a>Özet
Esnek veritabanı araçlarını ve satır düzeyi güvenlik çıkışı bir uygulamanın veri katmanı çok Kiracı ve Kiracı tek parça desteği ile birlikte kullanılan tooscale olabilir. Çok kiracılı parça olabilir kullanılan toostore verileri daha verimli bir şekilde (çok sayıda kiracılar yalnızca birkaç satır veri olduğu özellikle durumlarda), tek-Kiracı sırasında parça kullanılan toosupport premium kiracılar daha sıkı performans ve yalıtım ile olabilir gereksinimleri.  Daha fazla bilgi için bkz: [satır düzeyi güvenlik başvurusu](https://msdn.microsoft.com/library/dn765131). 

## <a name="additional-resources"></a>Ek kaynaklar
* [Bir Azure esnek havuz nedir?](sql-database-elastic-pool.md)
* [Azure SQL Veritabanı ile ölçek genişletme](sql-database-elastic-scale-introduction.md)
* [Azure SQL Veritabanı ile Çok Kiracılı SaaS Uygulamaları için Tasarım Desenleri](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [Azure AD ve OpenID Connect kullanarak çok müşterili uygulamalarda kimlik doğrulama](../guidance/guidance-multitenant-identity-authenticate.md)
* [Tailspin Surveys uygulaması](../guidance/guidance-multitenant-identity-tailspin.md)

## <a name="questions-and-feature-requests"></a>Sorular ve özellik istekleri
Sorular için lütfen hello üzerinde toous ulaşmak [SQL veritabanı Forumu](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) ve özellik istekleri için lütfen toohello eklemesini [SQL veritabanı geri bildirim Forumunda](https://feedback.azure.com/forums/217321-sql-database/).

<!--Image references-->
[1]: ./media/sql-database-elastic-tools-multi-tenant-row-level-security/blogging-app.png
<!--anchors-->


