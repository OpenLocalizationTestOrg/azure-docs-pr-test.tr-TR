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
# <a name="multi-tenant-applications-with-elastic-database-tools-and-row-level-security"></a><span data-ttu-id="aba42-103">Çok kiracılı uygulamalarla esnek veritabanı araçlarını ve satır düzeyi güvenlik</span><span class="sxs-lookup"><span data-stu-id="aba42-103">Multi-tenant applications with elastic database tools and row-level security</span></span>
<span data-ttu-id="aba42-104">[Esnek veritabanı araçlarını](sql-database-elastic-scale-get-started.md) ve [satır düzeyi güvenlik (RLS)](https://msdn.microsoft.com/library/dn765131) güçlü bir esnek ve verimli bir şekilde hello veri katmanı Azure SQL veritabanı olan bir çok kiracılı uygulama ölçeklendirme için özellik kümesi sunar.</span><span class="sxs-lookup"><span data-stu-id="aba42-104">[Elastic database tools](sql-database-elastic-scale-get-started.md) and [row-level security (RLS)](https://msdn.microsoft.com/library/dn765131) offer a powerful set of capabilities for flexibly and efficiently scaling hello data tier of a multi-tenant application with Azure SQL Database.</span></span> <span data-ttu-id="aba42-105">Bkz: [Azure SQL veritabanı ile çok kiracılı SaaS uygulamaları için Tasarım desenleri](sql-database-design-patterns-multi-tenancy-saas-applications.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="aba42-105">See [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md) for more information.</span></span> 

<span data-ttu-id="aba42-106">Bu makalede gösterilmektedir nasıl toouse bu teknolojiler birlikte toobuild kullanarak çok kiracılı parça destekleyen bir yüksek düzeyde ölçeklenebilir veri katmanı uygulamayla **ADO.NET SqlClient** ve/veya **Entity Framework**.</span><span class="sxs-lookup"><span data-stu-id="aba42-106">This article illustrates how toouse these technologies together toobuild an application with a highly scalable data tier that supports multi-tenant shards, using **ADO.NET SqlClient** and/or **Entity Framework**.</span></span>  

* <span data-ttu-id="aba42-107">**Esnek veritabanı araçlarını** geliştiriciler tooscale hello veri katmanı .NET kitaplıkları ve Azure hizmet şablonları kümesini kullanarak endüstri standardı parçalama yöntemler aracılığıyla bir uygulamanın çıkışı sağlar.</span><span class="sxs-lookup"><span data-stu-id="aba42-107">**Elastic database tools** enables developers tooscale out hello data tier of an application via industry-standard sharding practices using a set of .NET libraries and Azure service templates.</span></span> <span data-ttu-id="aba42-108">Hello esnek veritabanı istemci kitaplığını kullanarak parça yönetme otomatikleştirmek ve birçok hello infrastructural görev genellikle parçalama ile ilişkili akıcı hale getirmesine yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="aba42-108">Managing shards with using hello Elastic Database Client Library helps automate and streamline many of hello infrastructural tasks typically associated with sharding.</span></span> 
* <span data-ttu-id="aba42-109">**Satır düzeyi güvenlik** hello aynı veritabanında bir sorgu yürütülürken toohello Kiracı ait olmayan satırlar çıkışı güvenlik ilkeleri toofilter kullanarak birden çok kiracılar için geliştiricilere toostore veri sağlar.</span><span class="sxs-lookup"><span data-stu-id="aba42-109">**Row-level security** enables developers toostore data for multiple tenants in hello same database using security policies toofilter out rows that do not belong toohello tenant executing a query.</span></span> <span data-ttu-id="aba42-110">RLS ile erişim mantığı hello veritabanı içinde merkezileştirme yerine hello uygulamada bakım basitleştirir ve bir uygulamanın codebase gibi hata hello riskini azaltır daha artar.</span><span class="sxs-lookup"><span data-stu-id="aba42-110">Centralizing access logic with RLS inside hello database, rather than in hello application, simplifies maintenance and reduces hello risk of error as an application’s codebase grows.</span></span> 

<span data-ttu-id="aba42-111">Bunlar kullanarak özellikleri birlikte, bir uygulama birden çok hello aynı Kiracı için veri depolayarak maliyet tasarrufu ve verimliliği elde eder yararlanabilir parça veritabanı.</span><span class="sxs-lookup"><span data-stu-id="aba42-111">Using these features together, an application can benefit from cost savings and efficiency gains by storing data for multiple tenants in hello same shard database.</span></span> <span data-ttu-id="aba42-112">Merhaba aynı zamanda, hala bir uygulama tek Kiracı parça daha sıkı performans garanti çok kiracılı parça kiracılar arasında eşit kaynak dağıtım garanti etmiyoruz beri duyan "premium" kiracılar için ayrık hello esneklik toooffer sahiptir.</span><span class="sxs-lookup"><span data-stu-id="aba42-112">At hello same time, an application still has hello flexibility toooffer isolated, single-tenant shards for “premium” tenants who require stricter performance guarantees since multi-tenant shards do not guarantee equal resource distribution among tenants.</span></span>  

<span data-ttu-id="aba42-113">Kısacası, esnek veritabanı istemci kitaplığının hello [veri bağımlı yönlendirme](sql-database-elastic-scale-data-dependent-routing.md) API'leri kendi parçalama anahtarı (genellikle bir "Tenantıd") içeren kiracılar toohello doğru parça veritabanı otomatik olarak bağlan.</span><span class="sxs-lookup"><span data-stu-id="aba42-113">In short, hello elastic database client library’s [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) APIs automatically connect tenants toohello correct shard database containing their sharding key (generally a “TenantId”).</span></span> <span data-ttu-id="aba42-114">Bağlantı kurulduktan sonra bir RLS güvenlik ilkesinde hello veritabanı kiracılar kendi Tenantıd içeren satırları yalnızca erişebilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="aba42-114">Once connected, an RLS security policy within hello database ensures that tenants can only access rows that contain their TenantId.</span></span> <span data-ttu-id="aba42-115">Tüm tabloları hangi satırların tooeach Kiracı ait Tenantıd sütun tooindicate içeren varsayılır.</span><span class="sxs-lookup"><span data-stu-id="aba42-115">It is assumed that all tables contain a TenantId column tooindicate which rows belong tooeach tenant.</span></span> 

![Blog uygulama mimarisi][1]

## <a name="download-hello-sample-project"></a><span data-ttu-id="aba42-117">Merhaba örnek projesini indirin</span><span class="sxs-lookup"><span data-stu-id="aba42-117">Download hello sample project</span></span>
### <a name="prerequisites"></a><span data-ttu-id="aba42-118">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="aba42-118">Prerequisites</span></span>
* <span data-ttu-id="aba42-119">Visual Studio (2012 veya sonraki sürümlerini) kullanın</span><span class="sxs-lookup"><span data-stu-id="aba42-119">Use Visual Studio (2012 or higher)</span></span> 
* <span data-ttu-id="aba42-120">Üç Azure SQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="aba42-120">Create three Azure SQL Databases</span></span> 
* <span data-ttu-id="aba42-121">Örnek projesini indirin: [Azure SQL - çok Kiracılı parça için esnek veritabanı araçları](http://go.microsoft.com/?linkid=9888163)</span><span class="sxs-lookup"><span data-stu-id="aba42-121">Download sample project: [Elastic DB Tools for Azure SQL - Multi-Tenant Shards](http://go.microsoft.com/?linkid=9888163)</span></span>
  * <span data-ttu-id="aba42-122">Veritabanlarınızı hello başında hello bilgileri doldurun **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="aba42-122">Fill in hello information for your databases at hello beginning of **Program.cs**</span></span> 

<span data-ttu-id="aba42-123">Bu proje bir açıklanan hello genişletir [Azure SQL - Entity Framework tümleştirme için esnek DB Araçları](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) çok kiracılı parça veritabanları için destek ekleyerek düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="aba42-123">This project extends hello one described in [Elastic DB Tools for Azure SQL - Entity Framework Integration](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) by adding support for multi-tenant shard databases.</span></span> <span data-ttu-id="aba42-124">Bloglar ve gönderileri, dört kiracılar ve hello Yukarıdaki diyagramda gösterildiği gibi iki çok kiracılı parça veritabanlarıyla oluşturmak için basit bir konsol uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="aba42-124">It builds a simple console application for creating blogs and posts, with four tenants and two multi-tenant shard databases as illustrated in hello above diagram.</span></span> 

<span data-ttu-id="aba42-125">Derleme ve hello uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="aba42-125">Build and run hello application.</span></span> <span data-ttu-id="aba42-126">Bu işlem hello esnek veritabanı araçlarını parça eşleme Yöneticisi ve testleri aşağıdaki çalışma hello bootstrap:</span><span class="sxs-lookup"><span data-stu-id="aba42-126">This will bootstrap hello elastic database tools’ shard map manager and run hello following tests:</span></span> 

1. <span data-ttu-id="aba42-127">Entity Framework ve LINQ kullanarak yeni bir blog oluşturun ve ardından her bir kiracı için tüm Web Günlüklerini Görüntüle</span><span class="sxs-lookup"><span data-stu-id="aba42-127">Using Entity Framework and LINQ, create a new blog and then display all blogs for each tenant</span></span>
2. <span data-ttu-id="aba42-128">ADO.NET SqlClient kullanarak, bir kiracı için tüm Web Günlüklerini Görüntüle</span><span class="sxs-lookup"><span data-stu-id="aba42-128">Using ADO.NET SqlClient, display all blogs for a tenant</span></span>
3. <span data-ttu-id="aba42-129">Tooinsert bir hata durum hello yanlış Kiracı tooverify için bir blog deneyin</span><span class="sxs-lookup"><span data-stu-id="aba42-129">Try tooinsert a blog for hello wrong tenant tooverify that an error is thrown</span></span>  

<span data-ttu-id="aba42-130">RLS hello parça veritabanlarında henüz etkinleştirilmemiş olduğundan, bu testler, her bir sorun ortaya dikkat edin: kiracılar olan toothem ait değil mümkün toosee bloglar ve Merhaba uygulaması, bir blog hello yanlış Kiracı için ekleme değil engellenir.</span><span class="sxs-lookup"><span data-stu-id="aba42-130">Notice that because RLS has not yet been enabled in hello shard databases, each of these tests reveals a problem: tenants are able toosee blogs that do not belong toothem, and hello application is not prevented from inserting a blog for hello wrong tenant.</span></span> <span data-ttu-id="aba42-131">Merhaba bu makalenin sonraki bölümlerinde tooresolve zorlayarak bu sorunların nasıl Kiracı açıklar yalıtım RLS ile.</span><span class="sxs-lookup"><span data-stu-id="aba42-131">hello remainder of this article describes how tooresolve these problems by enforcing tenant isolation with RLS.</span></span> <span data-ttu-id="aba42-132">İki adımı vardır:</span><span class="sxs-lookup"><span data-stu-id="aba42-132">There are two steps:</span></span> 

1. <span data-ttu-id="aba42-133">**Uygulama katmanı**: hello uygulama kodunu değiştirme tooalways kümesi hello hello SESSION_CONTEXT içinde geçerli Tenantıd bağlantı açıldıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="aba42-133">**Application tier**: Modify hello application code tooalways set hello current TenantId in hello SESSION_CONTEXT after opening a connection.</span></span> <span data-ttu-id="aba42-134">Merhaba örnek proje zaten bu yapmıştır.</span><span class="sxs-lookup"><span data-stu-id="aba42-134">hello sample project has already done this.</span></span> 
2. <span data-ttu-id="aba42-135">**Veri katmanı**: Tenantıd hello üzerinde alarak satırları SESSION_CONTEXT içinde depolanan her parça veritabanı toofilter RLS güvenlik ilkesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="aba42-135">**Data tier**: Create an RLS security policy in each shard database toofilter rows based on hello TenantId stored in SESSION_CONTEXT.</span></span> <span data-ttu-id="aba42-136">Toodo bu her parça veritabanlarınız için gerekir, aksi durumda çok kiracılı parça satırlarda değil filtrelenir.</span><span class="sxs-lookup"><span data-stu-id="aba42-136">You will need toodo this for each of your shard databases, otherwise rows in multi-tenant shards will not be filtered.</span></span> 

## <a name="step-1-application-tier-set-tenantid-in-hello-sessioncontext"></a><span data-ttu-id="aba42-137">1. adım) uygulama katmanı: Merhaba SESSION_CONTEXT içinde Tenantıd ayarlayın</span><span class="sxs-lookup"><span data-stu-id="aba42-137">Step 1) Application tier: Set TenantId in hello SESSION_CONTEXT</span></span>
<span data-ttu-id="aba42-138">Bağımlı yönlendirme API'leri, hello uygulama hala hello esnek veritabanı istemci kitaplığının verileri kullanarak bağlanan tooa parça veritabanının tootell hello veritabanı gereken sonra RLS güvenlik ilkesi satırları filtreleyebilirsiniz böylece hangi Tenantıd o bağlantı kullanıyor tooother kiracılar ait.</span><span class="sxs-lookup"><span data-stu-id="aba42-138">After connecting tooa shard database using hello elastic database client library’s data dependent routing APIs, hello application still needs tootell hello database which TenantId is using that connection so that an RLS security policy can filter out rows belonging tooother tenants.</span></span> <span data-ttu-id="aba42-139">Bu bilgiler önerilen yöntem toopass hello toostore hello hello Bu bağlantı için geçerli bir Tenantıd [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span><span class="sxs-lookup"><span data-stu-id="aba42-139">hello recommended way toopass this information is toostore hello current TenantId for that connection in hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span></span> <span data-ttu-id="aba42-140">(Not: alternatif olarak kullanabileceğinizi [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), ancak SESSION_CONTEXT daha iyi bir seçenek daha kolay toouse olduğundan, varsayılan değer olarak NULL döndürür ve anahtar-değer çiftleri destekler.)</span><span class="sxs-lookup"><span data-stu-id="aba42-140">(Note: You could alternatively use [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), but SESSION_CONTEXT is a better option because it is easier toouse, returns NULL by default, and supports key-value pairs.)</span></span>

### <a name="entity-framework"></a><span data-ttu-id="aba42-141">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="aba42-141">Entity Framework</span></span>
<span data-ttu-id="aba42-142">Entity Framework kullanan uygulamalar için hello kolay SESSION_CONTEXT ElasticScaleContext geçersiz kılma hello içinde açıklanan tooset hello yaklaşımdır [EF DbContext kullanarak veri bağımlı yönlendirme](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span><span class="sxs-lookup"><span data-stu-id="aba42-142">For applications using Entity Framework, hello easiest approach is tooset hello SESSION_CONTEXT within hello ElasticScaleContext override described in [Data Dependent Routing using EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span></span> <span data-ttu-id="aba42-143">Veri bağımlı Yönlendirme aracılığıyla aracılı hello bağlantı dönmeden önce oluşturun ve o bağlantı için belirtilen hello SESSION_CONTEXT toohello shardingKey 'Tenantıd' ayarlar SqlCommand yürütün.</span><span class="sxs-lookup"><span data-stu-id="aba42-143">Before returning hello connection brokered through data dependent routing, simply create and execute a SqlCommand that sets 'TenantId' in hello SESSION_CONTEXT toohello shardingKey specified for that connection.</span></span> <span data-ttu-id="aba42-144">Tooset hello sonra SESSION_CONTEXT bu şekilde, yalnızca toowrite kod gerekir.</span><span class="sxs-lookup"><span data-stu-id="aba42-144">This way, you only need toowrite code once tooset hello SESSION_CONTEXT.</span></span> 

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

<span data-ttu-id="aba42-145">Merhaba SESSION_CONTEXT ile otomatik olarak ayarlanır artık ElasticScaleContext çağrılan her hello Tenantıd belirtilen:</span><span class="sxs-lookup"><span data-stu-id="aba42-145">Now hello SESSION_CONTEXT is automatically set with hello specified TenantId whenever ElasticScaleContext is invoked:</span></span> 

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

### <a name="adonet-sqlclient"></a><span data-ttu-id="aba42-146">ADO.NET SqlClient</span><span class="sxs-lookup"><span data-stu-id="aba42-146">ADO.NET SqlClient</span></span>
<span data-ttu-id="aba42-147">ADO.NET SqlClient hello kullanarak uygulamaları yaklaşım toocreate önerilir 'Tenantıd' hello SESSION_CONTEXT toohello otomatik olarak ayarlar ShardMap.OpenConnectionForKey() çevresinde bir sarmalayıcı işlevi gidermek Tenantıd döndürmeden önce bir bağlantı.</span><span class="sxs-lookup"><span data-stu-id="aba42-147">For applications using ADO.NET SqlClient, hello recommended approach is toocreate a wrapper function around ShardMap.OpenConnectionForKey() that automatically sets 'TenantId' in hello SESSION_CONTEXT toohello correct TenantId before returning a connection.</span></span> <span data-ttu-id="aba42-148">SESSION_CONTEXT her zaman ayarlanır tooensure, yalnızca bu sarmalayıcı işlevi kullanarak bağlantı açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="aba42-148">tooensure that SESSION_CONTEXT is always set, you should only open connections using this wrapper function.</span></span>

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

## <a name="step-2-data-tier-create-row-level-security-policy"></a><span data-ttu-id="aba42-149">2. adım) veri katmanı: satır düzeyi güvenlik ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="aba42-149">Step 2) Data tier: Create row-level security policy</span></span>
### <a name="create-a-security-policy-toofilter-hello-rows-each-tenant-can-access"></a><span data-ttu-id="aba42-150">Bir güvenlik ilkesi toofilter hello her Kiracı erişebileceği satırları oluşturma</span><span class="sxs-lookup"><span data-stu-id="aba42-150">Create a security policy toofilter hello rows each tenant can access</span></span>
<span data-ttu-id="aba42-151">Merhaba uygulaması ile SESSION_CONTEXT ayarı göre geçerli Tenantıd hello sorgulama önce RLS güvenlik ilkesi sorgular ve filtreleyebilirsiniz farklı Tenantıd satırları çıkar.</span><span class="sxs-lookup"><span data-stu-id="aba42-151">Now that hello application is setting SESSION_CONTEXT with hello current TenantId before querying, an RLS security policy can filter queries and exclude rows that have a different TenantId.</span></span>  

<span data-ttu-id="aba42-152">RLS, T-SQL uygulanır: kullanıcı tanımlı bir işlev hello erişim mantığını tanımlayan ve bu tablo işlevi tooany sayısı bir güvenlik ilkesi bağlar.</span><span class="sxs-lookup"><span data-stu-id="aba42-152">RLS is implemented in T-SQL: a user-defined function defines hello access logic, and a security policy binds this function tooany number of tables.</span></span> <span data-ttu-id="aba42-153">Bu proje için hello işlevi yalnızca hello uygulama (yerine başka bir SQL kullanıcı) bağlı toohello veritabanıdır ve 'Tenantıd' hello SESSION_CONTEXT depolanan o hello hello belirli bir satırın Tenantıd eşleşen doğrular.</span><span class="sxs-lookup"><span data-stu-id="aba42-153">For this project, hello function will simply verify that hello application (rather than some other SQL user) is connected toohello database, and that hello 'TenantId' stored in hello SESSION_CONTEXT matches hello TenantId of a given row.</span></span> <span data-ttu-id="aba42-154">Bir filtre koşulu hello filtresini seçin, UPDATE ve DELETE sorgularının üzerinden bu koşullar toopass karşılayan satırları izin verir; ve bir engelleme koşuluna eklenen veya güncelleştirilen engeller Bu koşulları ihlal satırları engeller.</span><span class="sxs-lookup"><span data-stu-id="aba42-154">A filter predicate will allow rows that meet these conditions toopass through hello filter for SELECT, UPDATE, and DELETE queries; and a block predicate will prevent rows that violate these conditions from being INSERTed or UPDATEd.</span></span> <span data-ttu-id="aba42-155">SESSION_CONTEXT ayarlı değil, boş ve hiçbir satır eklenen görünür mü yoksa mümkün toobe olacaktır döndürür.</span><span class="sxs-lookup"><span data-stu-id="aba42-155">If SESSION_CONTEXT has not been set, it will return NULL and no rows will be visible or able toobe inserted.</span></span> 

<span data-ttu-id="aba42-156">tooenable RLS, T-SQL ya da Visual Studio (SSDT), SSMS, kullanarak tüm üzerinde şu hello execute veya PowerShell Betiği hello projeye dahil hello (veya kullanıyorsanız [esnek veritabanı iş](sql-database-elastic-jobs-overview.md), tooautomate yürütme kullanın Bu T-SQL tüm parça):</span><span class="sxs-lookup"><span data-stu-id="aba42-156">tooenable RLS, execute hello following T-SQL on all shards using either Visual Studio (SSDT), SSMS, or hello PowerShell script included in hello project (or if you are using [Elastic Database Jobs](sql-database-elastic-jobs-overview.md), you can use it tooautomate execution of this T-SQL on all shards):</span></span> 

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
> <span data-ttu-id="aba42-157">Tabloları yüzlerce tooadd hello koşul gereken daha karmaşık projelerde otomatik olarak bir şemadaki tüm tablolarda bir koşul ekleme bir güvenlik ilkesi oluşturur bir yardımcı depolanan yordamı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aba42-157">For more complex projects that need tooadd hello predicate on hundreds of tables, you can use a helper stored procedure that automatically generates a security policy adding a predicate on all tables in a schema.</span></span> <span data-ttu-id="aba42-158">Bkz: [geçerli satır düzeyi güvenlik tooall tabloları - Yardımcısı komut dosyası (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).</span><span class="sxs-lookup"><span data-stu-id="aba42-158">See [Apply Row-Level Security tooall tables - helper script (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).</span></span>  
> 
> 

<span data-ttu-id="aba42-159">Şimdi hello örnek uygulamayı yeniden çalıştırın, kiracılar mümkün toosee toothem ait yalnızca satır olur.</span><span class="sxs-lookup"><span data-stu-id="aba42-159">Now if you run hello sample application again, tenants will able toosee only rows that belong toothem.</span></span> <span data-ttu-id="aba42-160">Ayrıca, Merhaba uygulaması hello bir bağlı durumda toohello parça veritabanının dışında tootenants ait satır eklenemiyor ve onu görünen satır toohave farklı Tenantıd güncelleştirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="aba42-160">In addition, hello application cannot insert rows that belong tootenants other than hello one currently connected toohello shard database, and it cannot update visible rows toohave a different TenantId.</span></span> <span data-ttu-id="aba42-161">Merhaba uygulaması toodo ya da çalışırsa, bir DbUpdateException gerçekleştirilecektir.</span><span class="sxs-lookup"><span data-stu-id="aba42-161">If hello application attempts toodo either, a DbUpdateException will be raised.</span></span>

<span data-ttu-id="aba42-162">Daha sonra yeni bir tablo eklerseniz, yalnızca ALTER güvenlik ilkesi hello ve yeni bir tablo hello üzerinde filtre ve engelleme koşulları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="aba42-162">If you add a new table later on, simply ALTER hello security policy and add filter and block predicates on hello new table:</span></span> 

```
ALTER SECURITY POLICY rls.tenantAccessPolicy     
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable
GO 
```

### <a name="add-default-constraints-tooautomatically-populate-tenantid-for-inserts"></a><span data-ttu-id="aba42-163">Varsayılan ekleme kısıtlamaları tooautomatically eklemeleri için Tenantıd doldurma</span><span class="sxs-lookup"><span data-stu-id="aba42-163">Add default constraints tooautomatically populate TenantId for INSERTs</span></span>
<span data-ttu-id="aba42-164">Varsayılan koyabilirsiniz her tablo tooautomatically kısıtlaması doldurmak hello Tenantıd hello ile şu anda satır eklerken SESSION_CONTEXT içinde depolanan değer.</span><span class="sxs-lookup"><span data-stu-id="aba42-164">You can put a default constraint on each table tooautomatically populate hello TenantId with hello value currently stored in SESSION_CONTEXT when inserting rows.</span></span> <span data-ttu-id="aba42-165">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="aba42-165">For example:</span></span> 

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

<span data-ttu-id="aba42-166">Şimdi satır eklerken Merhaba uygulaması toospecify bir Tenantıd gerekmez:</span><span class="sxs-lookup"><span data-stu-id="aba42-166">Now hello application does not need toospecify a TenantId when inserting rows:</span></span> 

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
> <span data-ttu-id="aba42-167">Bir Entity Framework projesi için varsayılan kısıtlamalar kullanırsanız, EF veri modelinizi hello Tenantıd sütun içermez önerilir.</span><span class="sxs-lookup"><span data-stu-id="aba42-167">If you use default constraints for an Entity Framework project, it is recommended that you do NOT include hello TenantId column in your EF data model.</span></span> <span data-ttu-id="aba42-168">Entity Framework sorguları otomatik olarak SESSION_CONTEXT kullanan T-SQL ile oluşturulan hello varsayılan kısıtlamalar geçersiz kılar varsayılan değerleri sağlayın olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="aba42-168">This is because Entity Framework queries automatically supply default values which will override hello default constraints created in T-SQL that use SESSION_CONTEXT.</span></span> <span data-ttu-id="aba42-169">Proje toouse varsayılan kısıtlamalar hello örnek, örneği için DataClasses.cs (ve çalışma Add-Migration hello Paket Yöneticisi konsolu içinde) Tenantıd kaldırmanız gerekir ve alan hello kullan T-SQL tooensure hello veritabanı tablolarında yalnızca mevcut.</span><span class="sxs-lookup"><span data-stu-id="aba42-169">toouse default constraints in hello sample project, for instance, you should remove TenantId from DataClasses.cs (and run Add-Migration in hello Package Manager Console) and use T-SQL tooensure that hello field only exists in hello database tables.</span></span> <span data-ttu-id="aba42-170">Bu şekilde EF otomatik olarak yanlış varsayılan değerler veri eklerken sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="aba42-170">This way, EF will not automatically supply incorrect default values when inserting data.</span></span> 
> 
> 

### <a name="optional-enable-a-superuser-tooaccess-all-rows"></a><span data-ttu-id="aba42-171">(İsteğe bağlı) Tüm satırlarda "süper kullanıcı" tooaccess etkinleştir</span><span class="sxs-lookup"><span data-stu-id="aba42-171">(Optional) Enable a "superuser" tooaccess all rows</span></span>
<span data-ttu-id="aba42-172">Bazı uygulamalar toocreate "tüm satırlar, tüm parça tüm kiracılar veya tooperform bölünmüş/birleştirme işlemleri veritabanları arasında taşıma Kiracı satırları içeren parça genelinde raporlama sipariş tooenable erişebilen örneği için bir süper kullanıcı" isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aba42-172">Some applications may want toocreate a "superuser" who can access all rows, for instance, in order tooenable reporting across all tenants on all shards, or tooperform Split/Merge operations on shards that involve moving tenant rows between databases.</span></span> <span data-ttu-id="aba42-173">tooenable Bu, her parça veritabanında yeni bir SQL kullanıcısının ("süper kullanıcı" Bu örnekte) oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="aba42-173">tooenable this, you should create a new SQL user ("superuser" in this example) in each shard database.</span></span> <span data-ttu-id="aba42-174">Ardından bu kullanıcı tooaccess tüm satırları sağlayan yeni bir koşul işlevi hello güvenlik ilkesiyle alter:</span><span class="sxs-lookup"><span data-stu-id="aba42-174">Then alter hello security policy with a new predicate function that allows this user tooaccess all rows:</span></span>

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


### <a name="maintenance"></a><span data-ttu-id="aba42-175">Bakım</span><span class="sxs-lookup"><span data-stu-id="aba42-175">Maintenance</span></span>
* <span data-ttu-id="aba42-176">**Yeni parça ekleme**: tüm yeni parça üzerinde hello T-SQL komut dosyası tooenable RLS yürütmeniz gerekir, aksi takdirde bu parça sorgulamaları değil filtrelenir.</span><span class="sxs-lookup"><span data-stu-id="aba42-176">**Adding new shards**: You must execute hello T-SQL script tooenable RLS on any new shards, otherwise queries on these shards will not be filtered.</span></span>
* <span data-ttu-id="aba42-177">**Yeni tablo ekleme**: Filtre eklemek ve yeni bir tablo oluşturulduğunda tüm parça koşul toohello güvenlik ilkesini engellemek, aksi takdirde hello yeni tablo sorgularında değil filtrelenir.</span><span class="sxs-lookup"><span data-stu-id="aba42-177">**Adding new tables**: You must add a filter and block predicate toohello security policy on all shards whenever a new table is created, otherwise queries on hello new table will not be filtered.</span></span> <span data-ttu-id="aba42-178">Bu DDL tetikleyicisi kullanarak açıklandığı gibi otomatikleştirilebilir [geçerli satır düzeyi güvenlik otomatik olarak toonewly oluşturulan tabloları (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span><span class="sxs-lookup"><span data-stu-id="aba42-178">This can be automated using a DDL trigger, as described in [Apply Row-Level Security automatically toonewly created tables (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span></span>

## <a name="summary"></a><span data-ttu-id="aba42-179">Özet</span><span class="sxs-lookup"><span data-stu-id="aba42-179">Summary</span></span>
<span data-ttu-id="aba42-180">Esnek veritabanı araçlarını ve satır düzeyi güvenlik çıkışı bir uygulamanın veri katmanı çok Kiracı ve Kiracı tek parça desteği ile birlikte kullanılan tooscale olabilir.</span><span class="sxs-lookup"><span data-stu-id="aba42-180">Elastic database tools and row-level security can be used together tooscale out an application’s data tier with support for both multi-tenant and single-tenant shards.</span></span> <span data-ttu-id="aba42-181">Çok kiracılı parça olabilir kullanılan toostore verileri daha verimli bir şekilde (çok sayıda kiracılar yalnızca birkaç satır veri olduğu özellikle durumlarda), tek-Kiracı sırasında parça kullanılan toosupport premium kiracılar daha sıkı performans ve yalıtım ile olabilir gereksinimleri.</span><span class="sxs-lookup"><span data-stu-id="aba42-181">Multi-tenant shards can be used toostore data more efficiently (particularly in cases where a large number of tenants have only a few rows of data), while single-tenant shards can be used toosupport premium tenants with stricter performance and isolation requirements.</span></span>  <span data-ttu-id="aba42-182">Daha fazla bilgi için bkz: [satır düzeyi güvenlik başvurusu](https://msdn.microsoft.com/library/dn765131).</span><span class="sxs-lookup"><span data-stu-id="aba42-182">For more information, see [Row-Level Security reference](https://msdn.microsoft.com/library/dn765131).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="aba42-183">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="aba42-183">Additional resources</span></span>
* [<span data-ttu-id="aba42-184">Bir Azure esnek havuz nedir?</span><span class="sxs-lookup"><span data-stu-id="aba42-184">What is an Azure elastic pool?</span></span>](sql-database-elastic-pool.md)
* [<span data-ttu-id="aba42-185">Azure SQL Veritabanı ile ölçek genişletme</span><span class="sxs-lookup"><span data-stu-id="aba42-185">Scaling out with Azure SQL Database</span></span>](sql-database-elastic-scale-introduction.md)
* [<span data-ttu-id="aba42-186">Azure SQL Veritabanı ile Çok Kiracılı SaaS Uygulamaları için Tasarım Desenleri</span><span class="sxs-lookup"><span data-stu-id="aba42-186">Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database</span></span>](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [<span data-ttu-id="aba42-187">Azure AD ve OpenID Connect kullanarak çok müşterili uygulamalarda kimlik doğrulama</span><span class="sxs-lookup"><span data-stu-id="aba42-187">Authentication in multitenant apps, using Azure AD and OpenID Connect</span></span>](../guidance/guidance-multitenant-identity-authenticate.md)
* [<span data-ttu-id="aba42-188">Tailspin Surveys uygulaması</span><span class="sxs-lookup"><span data-stu-id="aba42-188">Tailspin Surveys application</span></span>](../guidance/guidance-multitenant-identity-tailspin.md)

## <a name="questions-and-feature-requests"></a><span data-ttu-id="aba42-189">Sorular ve özellik istekleri</span><span class="sxs-lookup"><span data-stu-id="aba42-189">Questions and Feature Requests</span></span>
<span data-ttu-id="aba42-190">Sorular için lütfen hello üzerinde toous ulaşmak [SQL veritabanı Forumu](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) ve özellik istekleri için lütfen toohello eklemesini [SQL veritabanı geri bildirim Forumunda](https://feedback.azure.com/forums/217321-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="aba42-190">For questions, please reach out toous on hello [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them toohello [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-tools-multi-tenant-row-level-security/blogging-app.png
<!--anchors-->


