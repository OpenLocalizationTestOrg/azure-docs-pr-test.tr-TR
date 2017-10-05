---
title: "Çok kiracılı uygulamalarla esnek veritabanı araçlarını ve satır düzeyi güvenlik"
description: "Azure SQL veritabanı üzerinde çoklu kiracı parça destekleyen bir yüksek düzeyde ölçeklenebilir veri katmanı ile bir uygulama oluşturmak için satır düzeyi güvenlik ile birlikte esnek veritabanı araçlarını kullanmayı öğrenin."
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
ms.openlocfilehash: 73f1210b8d1f5ceca8fac9534d498bdc23d96d48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="multi-tenant-applications-with-elastic-database-tools-and-row-level-security"></a><span data-ttu-id="e1b78-103">Çok kiracılı uygulamalarla esnek veritabanı araçlarını ve satır düzeyi güvenlik</span><span class="sxs-lookup"><span data-stu-id="e1b78-103">Multi-tenant applications with elastic database tools and row-level security</span></span>
<span data-ttu-id="e1b78-104">[Esnek veritabanı araçlarını](sql-database-elastic-scale-get-started.md) ve [satır düzeyi güvenlik (RLS)](https://msdn.microsoft.com/library/dn765131) güçlü bir esnek ve verimli bir şekilde Azure SQL veritabanı olan bir çok kiracılı uygulama veri katmanı ölçeklendirmeye yönelik özellik kümesi sunar.</span><span class="sxs-lookup"><span data-stu-id="e1b78-104">[Elastic database tools](sql-database-elastic-scale-get-started.md) and [row-level security (RLS)](https://msdn.microsoft.com/library/dn765131) offer a powerful set of capabilities for flexibly and efficiently scaling the data tier of a multi-tenant application with Azure SQL Database.</span></span> <span data-ttu-id="e1b78-105">Bkz: [Azure SQL veritabanı ile çok kiracılı SaaS uygulamaları için Tasarım desenleri](sql-database-design-patterns-multi-tenancy-saas-applications.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="e1b78-105">See [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md) for more information.</span></span> 

<span data-ttu-id="e1b78-106">Bu makalede bu teknolojiler birlikte kullanarak çok kiracılı parça destekleyen bir yüksek düzeyde ölçeklenebilir veri katmanı ile bir uygulama oluşturmak için nasıl kullanılacağını anlatan **ADO.NET SqlClient** ve/veya **Entity Framework**.</span><span class="sxs-lookup"><span data-stu-id="e1b78-106">This article illustrates how to use these technologies together to build an application with a highly scalable data tier that supports multi-tenant shards, using **ADO.NET SqlClient** and/or **Entity Framework**.</span></span>  

* <span data-ttu-id="e1b78-107">**Esnek veritabanı araçlarını** bir uygulamanın bir dizi .NET kitaplıkları ve Azure hizmet şablonları kullanarak endüstri standardı parçalama yöntemler aracılığıyla veri katmanı genişletmek için geliştiricilere olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="e1b78-107">**Elastic database tools** enables developers to scale out the data tier of an application via industry-standard sharding practices using a set of .NET libraries and Azure service templates.</span></span> <span data-ttu-id="e1b78-108">Esnek veritabanı istemci kitaplığı kullanılarak ile parça yönetme otomatikleştirmek ve genellikle parçalama ile ilişkili infrastructural görevlerin çoğunu akıcı hale getirmesine yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="e1b78-108">Managing shards with using the Elastic Database Client Library helps automate and streamline many of the infrastructural tasks typically associated with sharding.</span></span> 
* <span data-ttu-id="e1b78-109">**Satır düzeyi güvenlik** aynı veritabanında bir sorgu yürütülürken kiracıya ait değil satırları filtrelemek için güvenlik ilkeleri kullanılarak birden çok Kiracı için verileri depolamak için geliştiricilere olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="e1b78-109">**Row-level security** enables developers to store data for multiple tenants in the same database using security policies to filter out rows that do not belong to the tenant executing a query.</span></span> <span data-ttu-id="e1b78-110">Veritabanı içinde erişim mantığı RLS ile merkezileştirme uygulamada, bakım kolaylaştırır ve uygulama takımın kod temeline etme gibi hata riskini azaltır yerine artar.</span><span class="sxs-lookup"><span data-stu-id="e1b78-110">Centralizing access logic with RLS inside the database, rather than in the application, simplifies maintenance and reduces the risk of error as an application’s codebase grows.</span></span> 

<span data-ttu-id="e1b78-111">Bu özellikleri birlikte kullanarak, bir uygulama için aynı parça veritabanında birden çok kiracıya veri depolayarak maliyet tasarrufu ve verimliliği elde eder yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1b78-111">Using these features together, an application can benefit from cost savings and efficiency gains by storing data for multiple tenants in the same shard database.</span></span> <span data-ttu-id="e1b78-112">Aynı anda bir uygulama hala daha sıkı performans garanti çok kiracılı parça kiracılar arasında eşit kaynak dağıtım garanti etmiyoruz beri duyan "premium" kiracılar için yalıtılmış, tek kiracılı parça teklif esnekliğine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e1b78-112">At the same time, an application still has the flexibility to offer isolated, single-tenant shards for “premium” tenants who require stricter performance guarantees since multi-tenant shards do not guarantee equal resource distribution among tenants.</span></span>  

<span data-ttu-id="e1b78-113">Kısacası, esnek veritabanı istemci kitaplığının [veri bağımlı yönlendirme](sql-database-elastic-scale-data-dependent-routing.md) API'leri otomatik olarak kiracılar kendi parçalama anahtarı (genellikle bir "Tenantıd") içeren doğru parça veritabanına bağlanın.</span><span class="sxs-lookup"><span data-stu-id="e1b78-113">In short, the elastic database client library’s [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) APIs automatically connect tenants to the correct shard database containing their sharding key (generally a “TenantId”).</span></span> <span data-ttu-id="e1b78-114">Bağlantı kurulduktan sonra veritabanını bir RLS güvenlik ilkesinde kiracılar kendi Tenantıd içeren satırları yalnızca erişebilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="e1b78-114">Once connected, an RLS security policy within the database ensures that tenants can only access rows that contain their TenantId.</span></span> <span data-ttu-id="e1b78-115">Tüm tabloları hangi satırların her kiracıya ait belirtmek için bir Tenantıd sütunu içeren varsayılır.</span><span class="sxs-lookup"><span data-stu-id="e1b78-115">It is assumed that all tables contain a TenantId column to indicate which rows belong to each tenant.</span></span> 

![Blog uygulama mimarisi][1]

## <a name="download-the-sample-project"></a><span data-ttu-id="e1b78-117">Örnek Proje yükle</span><span class="sxs-lookup"><span data-stu-id="e1b78-117">Download the sample project</span></span>
### <a name="prerequisites"></a><span data-ttu-id="e1b78-118">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e1b78-118">Prerequisites</span></span>
* <span data-ttu-id="e1b78-119">Visual Studio (2012 veya sonraki sürümlerini) kullanın</span><span class="sxs-lookup"><span data-stu-id="e1b78-119">Use Visual Studio (2012 or higher)</span></span> 
* <span data-ttu-id="e1b78-120">Üç Azure SQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1b78-120">Create three Azure SQL Databases</span></span> 
* <span data-ttu-id="e1b78-121">Örnek projesini indirin: [Azure SQL - çok Kiracılı parça için esnek veritabanı araçları](http://go.microsoft.com/?linkid=9888163)</span><span class="sxs-lookup"><span data-stu-id="e1b78-121">Download sample project: [Elastic DB Tools for Azure SQL - Multi-Tenant Shards](http://go.microsoft.com/?linkid=9888163)</span></span>
  * <span data-ttu-id="e1b78-122">Veritabanlarınızı başındaki bilgileri doldurun **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="e1b78-122">Fill in the information for your databases at the beginning of **Program.cs**</span></span> 

<span data-ttu-id="e1b78-123">Bu proje açıklandığı bir genişletir [Azure SQL - Entity Framework tümleştirme için esnek DB Araçları](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) çok kiracılı parça veritabanları için destek ekleyerek düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="e1b78-123">This project extends the one described in [Elastic DB Tools for Azure SQL - Entity Framework Integration](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) by adding support for multi-tenant shard databases.</span></span> <span data-ttu-id="e1b78-124">Bloglar ve gönderileri, dört kiracılar ve Yukarıdaki diyagramda gösterildiği gibi iki parça çok Kiracı veritabanı oluşturmak için basit bir konsol uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e1b78-124">It builds a simple console application for creating blogs and posts, with four tenants and two multi-tenant shard databases as illustrated in the above diagram.</span></span> 

<span data-ttu-id="e1b78-125">Derleme ve uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e1b78-125">Build and run the application.</span></span> <span data-ttu-id="e1b78-126">Bu esnek veritabanı araçlarını parça eşleme Yöneticisi bootstrap ve aşağıdaki testleri çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e1b78-126">This will bootstrap the elastic database tools’ shard map manager and run the following tests:</span></span> 

1. <span data-ttu-id="e1b78-127">Entity Framework ve LINQ kullanarak yeni bir blog oluşturun ve ardından her bir kiracı için tüm Web Günlüklerini Görüntüle</span><span class="sxs-lookup"><span data-stu-id="e1b78-127">Using Entity Framework and LINQ, create a new blog and then display all blogs for each tenant</span></span>
2. <span data-ttu-id="e1b78-128">ADO.NET SqlClient kullanarak, bir kiracı için tüm Web Günlüklerini Görüntüle</span><span class="sxs-lookup"><span data-stu-id="e1b78-128">Using ADO.NET SqlClient, display all blogs for a tenant</span></span>
3. <span data-ttu-id="e1b78-129">Bir hata atılır doğrulamak yanlış Kiracı için bir blog eklemeyi deneyin</span><span class="sxs-lookup"><span data-stu-id="e1b78-129">Try to insert a blog for the wrong tenant to verify that an error is thrown</span></span>  

<span data-ttu-id="e1b78-130">RLS parça veritabanlarında henüz etkinleştirilmemiş olduğundan, bu testler, her bir sorun ortaya dikkat edin: kiracılar kendilerine ait değil bloglar görmeye ve uygulama yanlış Kiracı için bir blog ekleme engellenemez.</span><span class="sxs-lookup"><span data-stu-id="e1b78-130">Notice that because RLS has not yet been enabled in the shard databases, each of these tests reveals a problem: tenants are able to see blogs that do not belong to them, and the application is not prevented from inserting a blog for the wrong tenant.</span></span> <span data-ttu-id="e1b78-131">Bu makalenin sonraki bölümlerinde, Kiracı yalıtımı RLS ile zorlayarak bu sorunları gidermek açıklar.</span><span class="sxs-lookup"><span data-stu-id="e1b78-131">The remainder of this article describes how to resolve these problems by enforcing tenant isolation with RLS.</span></span> <span data-ttu-id="e1b78-132">İki adımı vardır:</span><span class="sxs-lookup"><span data-stu-id="e1b78-132">There are two steps:</span></span> 

1. <span data-ttu-id="e1b78-133">**Uygulama katmanı**: her zaman bir bağlantı açıldıktan sonra geçerli Tenantıd SESSION_CONTEXT ayarlamak için uygulama kodu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e1b78-133">**Application tier**: Modify the application code to always set the current TenantId in the SESSION_CONTEXT after opening a connection.</span></span> <span data-ttu-id="e1b78-134">Örnek Proje zaten bu yapmıştır.</span><span class="sxs-lookup"><span data-stu-id="e1b78-134">The sample project has already done this.</span></span> 
2. <span data-ttu-id="e1b78-135">**Veri katmanı**: SESSION_CONTEXT içinde depolanan Tenantıd göre filtre satırlara her parça veritabanındaki bir RLS güvenlik ilkesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e1b78-135">**Data tier**: Create an RLS security policy in each shard database to filter rows based on the TenantId stored in SESSION_CONTEXT.</span></span> <span data-ttu-id="e1b78-136">Her parça veritabanlarınız için bunu yapmanız gerekir, aksi takdirde çok kiracılı parça satırlarda değil filtrelenir.</span><span class="sxs-lookup"><span data-stu-id="e1b78-136">You will need to do this for each of your shard databases, otherwise rows in multi-tenant shards will not be filtered.</span></span> 

## <a name="step-1-application-tier-set-tenantid-in-the-sessioncontext"></a><span data-ttu-id="e1b78-137">1. adım) uygulama katmanı: SESSION_CONTEXT içinde Tenantıd ayarlayın</span><span class="sxs-lookup"><span data-stu-id="e1b78-137">Step 1) Application tier: Set TenantId in the SESSION_CONTEXT</span></span>
<span data-ttu-id="e1b78-138">Böylece bir RLS güvenlik ilkesini ait satır filtrelemek bağımlı yönlendirme API, uygulamanın halen veritabanı bildirmek için gereken esnek veritabanı istemci kitaplığının verileri kullanarak bir parça veritabanına bağlandıktan sonra hangi Tenantıd o bağlantı kullanıyor diğer kiracılar.</span><span class="sxs-lookup"><span data-stu-id="e1b78-138">After connecting to a shard database using the elastic database client library’s data dependent routing APIs, the application still needs to tell the database which TenantId is using that connection so that an RLS security policy can filter out rows belonging to other tenants.</span></span> <span data-ttu-id="e1b78-139">Bu bağlantı için geçerli Tenantıd depolamak için bu bilgileri geçirmek için önerilen yöntem olduğu [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span><span class="sxs-lookup"><span data-stu-id="e1b78-139">The recommended way to pass this information is to store the current TenantId for that connection in the [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span></span> <span data-ttu-id="e1b78-140">(Not: alternatif olarak kullanabileceğinizi [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), ancak SESSION_CONTEXT daha iyi bir seçenek kullanmak daha kolay olduğundan varsayılan değer olarak NULL döndürür ve anahtar-değer çiftleri destekler.)</span><span class="sxs-lookup"><span data-stu-id="e1b78-140">(Note: You could alternatively use [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), but SESSION_CONTEXT is a better option because it is easier to use, returns NULL by default, and supports key-value pairs.)</span></span>

### <a name="entity-framework"></a><span data-ttu-id="e1b78-141">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="e1b78-141">Entity Framework</span></span>
<span data-ttu-id="e1b78-142">Entity Framework kullanan uygulamalar için en kolay yaklaşım içinde açıklanan ElasticScaleContext geçersiz kılma SESSION_CONTEXT ayarlamaktır [EF DbContext kullanarak veri bağımlı yönlendirme](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span><span class="sxs-lookup"><span data-stu-id="e1b78-142">For applications using Entity Framework, the easiest approach is to set the SESSION_CONTEXT within the ElasticScaleContext override described in [Data Dependent Routing using EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span></span> <span data-ttu-id="e1b78-143">Veri bağımlı Yönlendirme aracılığıyla aracılı bağlantı dönmeden önce oluşturun ve o bağlantı için belirtilen shardingKey için SESSION_CONTEXT 'Tenantıd' ayarlar SqlCommand yürütün.</span><span class="sxs-lookup"><span data-stu-id="e1b78-143">Before returning the connection brokered through data dependent routing, simply create and execute a SqlCommand that sets 'TenantId' in the SESSION_CONTEXT to the shardingKey specified for that connection.</span></span> <span data-ttu-id="e1b78-144">Bu şekilde, yalnızca bir kez SESSION_CONTEXT ayarlamak için kod yazmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1b78-144">This way, you only need to write code once to set the SESSION_CONTEXT.</span></span> 

```
// ElasticScaleContext.cs 
// ... 
// C'tor for data dependent routing. This call will open a validated connection routed to the proper 
// shard by the shard map manager. Note that the base class c'tor call will fail for an open connection 
// if migrations need to be done and SQL credentials are used. This is the reason for the  
// separation of c'tors into the DDR case (this c'tor) and the internal c'tor for new shards. 
public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
    : base(OpenDDRConnection(shardMap, shardingKey, connectionStr), true /* contextOwnsConnection */)
{
}

public static SqlConnection OpenDDRConnection(ShardMap shardMap, T shardingKey, string connectionStr)
{
    // No initialization
    Database.SetInitializer<ElasticScaleContext<T>>(null);

    // Ask shard map to broker a validated connection for the given key
    SqlConnection conn = null;
    try
    {
        conn = shardMap.OpenConnectionForKey(shardingKey, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT to shardingKey to enable Row-Level Security filtering
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

<span data-ttu-id="e1b78-145">Şimdi ElasticScaleContext çağrılan her SESSION_CONTEXT ile belirtilen Tenantıd otomatik olarak ayarlanır:</span><span class="sxs-lookup"><span data-stu-id="e1b78-145">Now the SESSION_CONTEXT is automatically set with the specified TenantId whenever ElasticScaleContext is invoked:</span></span> 

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

### <a name="adonet-sqlclient"></a><span data-ttu-id="e1b78-146">ADO.NET SqlClient</span><span class="sxs-lookup"><span data-stu-id="e1b78-146">ADO.NET SqlClient</span></span>
<span data-ttu-id="e1b78-147">ADO.NET SqlClient kullanan uygulamalar için otomatik olarak 'Tenantıd' SESSION_CONTEXT doğru Tenantıd için bir bağlantı döndürmeden önce ayarlar ShardMap.OpenConnectionForKey() çevresinde bir sarmalayıcı işlevi oluşturma önerilen yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="e1b78-147">For applications using ADO.NET SqlClient, the recommended approach is to create a wrapper function around ShardMap.OpenConnectionForKey() that automatically sets 'TenantId' in the SESSION_CONTEXT to the correct TenantId before returning a connection.</span></span> <span data-ttu-id="e1b78-148">SESSION_CONTEXT her zaman ayarlandığından emin olmak için yalnızca bu sarmalayıcı işlevi kullanarak bağlantı açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1b78-148">To ensure that SESSION_CONTEXT is always set, you should only open connections using this wrapper function.</span></span>

```
// Program.cs
// ...

// Wrapper function for ShardMap.OpenConnectionForKey() that automatically sets SESSION_CONTEXT with the correct
// tenantId before returning a connection. As a best practice, you should only open connections using this 
// method to ensure that SESSION_CONTEXT is always set before executing a query.
public static SqlConnection OpenConnectionForTenant(ShardMap shardMap, int tenantId, string connectionStr)
{
    SqlConnection conn = null;
    try
    {
        // Ask shard map to broker a validated connection for the given key
        conn = shardMap.OpenConnectionForKey(tenantId, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT to shardingKey to enable Row-Level Security filtering
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

## <a name="step-2-data-tier-create-row-level-security-policy"></a><span data-ttu-id="e1b78-149">2. adım) veri katmanı: satır düzeyi güvenlik ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1b78-149">Step 2) Data tier: Create row-level security policy</span></span>
### <a name="create-a-security-policy-to-filter-the-rows-each-tenant-can-access"></a><span data-ttu-id="e1b78-150">Her Kiracı erişebileceği satırları filtrelemek için bir güvenlik ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1b78-150">Create a security policy to filter the rows each tenant can access</span></span>
<span data-ttu-id="e1b78-151">Uygulama SESSION_CONTEXT geçerli Tenantıd ile sorgulama önce ayarı, bir RLS güvenlik ilkesi sorguları filtrelemek ve farklı bir tenantıd değerine sahip satırları dışlama.</span><span class="sxs-lookup"><span data-stu-id="e1b78-151">Now that the application is setting SESSION_CONTEXT with the current TenantId before querying, an RLS security policy can filter queries and exclude rows that have a different TenantId.</span></span>  

<span data-ttu-id="e1b78-152">RLS, T-SQL uygulanır: kullanıcı tanımlı bir işlev erişim mantığı tanımlar ve bir güvenlik ilkesi bu işlev tabloları herhangi bir sayıda bağlar.</span><span class="sxs-lookup"><span data-stu-id="e1b78-152">RLS is implemented in T-SQL: a user-defined function defines the access logic, and a security policy binds this function to any number of tables.</span></span> <span data-ttu-id="e1b78-153">Bu proje için işlevi yalnızca uygulama (başka bir SQL kullanıcı yerine) veritabanına bağlanır ve belirli bir satırın Tenantıd eşleşen 'Tenantıd' SESSION_CONTEXT depolanan doğrular.</span><span class="sxs-lookup"><span data-stu-id="e1b78-153">For this project, the function will simply verify that the application (rather than some other SQL user) is connected to the database, and that the 'TenantId' stored in the SESSION_CONTEXT matches the TenantId of a given row.</span></span> <span data-ttu-id="e1b78-154">Bir filtre koşulu seçin, güncelleştirme ve silme sorguları için filtre geçmesine bu koşullara uyan satırları izin verir; ve bir engelleme koşuluna eklenen veya güncelleştirilen engeller Bu koşulları ihlal satırları engeller.</span><span class="sxs-lookup"><span data-stu-id="e1b78-154">A filter predicate will allow rows that meet these conditions to pass through the filter for SELECT, UPDATE, and DELETE queries; and a block predicate will prevent rows that violate these conditions from being INSERTed or UPDATEd.</span></span> <span data-ttu-id="e1b78-155">SESSION_CONTEXT ayarlı değil, NULL ve hiçbir satır görünür veya eklenecek mümkün olacaktır döndürür.</span><span class="sxs-lookup"><span data-stu-id="e1b78-155">If SESSION_CONTEXT has not been set, it will return NULL and no rows will be visible or able to be inserted.</span></span> 

<span data-ttu-id="e1b78-156">RLS etkinleştirmek için Visual Studio (SSDT), SSMS veya projeye dahil PowerShell komut dosyası kullanarak tüm parça aşağıdaki T-SQL yürütmek (veya kullanıyorsanız [esnek veritabanı iş](sql-database-elastic-jobs-overview.md), bu yürütülmesi otomatikleştirmek için kullanın Tüm parça üzerinde T-SQL):</span><span class="sxs-lookup"><span data-stu-id="e1b78-156">To enable RLS, execute the following T-SQL on all shards using either Visual Studio (SSDT), SSMS, or the PowerShell script included in the project (or if you are using [Elastic Database Jobs](sql-database-elastic-jobs-overview.md), you can use it to automate execution of this T-SQL on all shards):</span></span> 

```
CREATE SCHEMA rls -- separate schema to organize RLS objects 
GO

CREATE FUNCTION rls.fn_tenantAccessPredicate(@TenantId int)     
    RETURNS TABLE     
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult          
        WHERE DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- the user in your application’s connection string (dbo is only for demo purposes!)         
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
> <span data-ttu-id="e1b78-157">Tabloları yüzlerce üzerinde koşulu eklemek için gereken daha karmaşık projelerde otomatik olarak bir şemadaki tüm tablolarda bir koşul ekleme bir güvenlik ilkesi oluşturur bir yardımcı depolanan yordamı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1b78-157">For more complex projects that need to add the predicate on hundreds of tables, you can use a helper stored procedure that automatically generates a security policy adding a predicate on all tables in a schema.</span></span> <span data-ttu-id="e1b78-158">Bkz: [geçerli satır düzeyi güvenlik tüm tablolara - Yardımcısı komut dosyası (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).</span><span class="sxs-lookup"><span data-stu-id="e1b78-158">See [Apply Row-Level Security to all tables - helper script (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).</span></span>  
> 
> 

<span data-ttu-id="e1b78-159">Şimdi örnek uygulamayı yeniden çalıştırın, kiracılar kendilerine ait satır görmeyebilir olur.</span><span class="sxs-lookup"><span data-stu-id="e1b78-159">Now if you run the sample application again, tenants will able to see only rows that belong to them.</span></span> <span data-ttu-id="e1b78-160">Ayrıca, uygulama bir parça veritabanı şu anda bağlı ve farklı bir Tenantıd olmasını görünen satır güncelleştirilemiyor dışında kiracılara ait satır eklenemiyor.</span><span class="sxs-lookup"><span data-stu-id="e1b78-160">In addition, the application cannot insert rows that belong to tenants other than the one currently connected to the shard database, and it cannot update visible rows to have a different TenantId.</span></span> <span data-ttu-id="e1b78-161">Uygulamanın, aşağıdakilerden birini kullanmaya çalışırsa, bir DbUpdateException gerçekleştirilecektir.</span><span class="sxs-lookup"><span data-stu-id="e1b78-161">If the application attempts to do either, a DbUpdateException will be raised.</span></span>

<span data-ttu-id="e1b78-162">Yeni bir tablo daha sonra eklerseniz, yalnızca güvenlik ilkesi ALTER ve filtre eklemek ve yeni bir tablo üzerinde koşulları engelle:</span><span class="sxs-lookup"><span data-stu-id="e1b78-162">If you add a new table later on, simply ALTER the security policy and add filter and block predicates on the new table:</span></span> 

```
ALTER SECURITY POLICY rls.tenantAccessPolicy     
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable
GO 
```

### <a name="add-default-constraints-to-automatically-populate-tenantid-for-inserts"></a><span data-ttu-id="e1b78-163">Ekler için Tenantıd otomatik olarak doldurulması için varsayılan kısıtlamalar ekleme</span><span class="sxs-lookup"><span data-stu-id="e1b78-163">Add default constraints to automatically populate TenantId for INSERTs</span></span>
<span data-ttu-id="e1b78-164">Varsayılan kısıtlama Tenantıd şu anda satır eklerken SESSION_CONTEXT içinde depolanan değerle otomatik olarak doldurulması için her bir tabloda koyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1b78-164">You can put a default constraint on each table to automatically populate the TenantId with the value currently stored in SESSION_CONTEXT when inserting rows.</span></span> <span data-ttu-id="e1b78-165">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="e1b78-165">For example:</span></span> 

```
-- Create default constraints to auto-populate TenantId with the value of SESSION_CONTEXT for inserts 
ALTER TABLE Blogs     
    ADD CONSTRAINT df_TenantId_Blogs      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO

ALTER TABLE Posts     
    ADD CONSTRAINT df_TenantId_Posts      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO 
```

<span data-ttu-id="e1b78-166">Şimdi uygulamayı satır eklerken bir Tenantıd belirtmek gerekmez:</span><span class="sxs-lookup"><span data-stu-id="e1b78-166">Now the application does not need to specify a TenantId when inserting rows:</span></span> 

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
> <span data-ttu-id="e1b78-167">Bir Entity Framework projesi için varsayılan kısıtlamalar kullanırsanız, Tenantıd sütun EF veri modelinizi içermez önerilir.</span><span class="sxs-lookup"><span data-stu-id="e1b78-167">If you use default constraints for an Entity Framework project, it is recommended that you do NOT include the TenantId column in your EF data model.</span></span> <span data-ttu-id="e1b78-168">Entity Framework sorguları otomatik olarak SESSION_CONTEXT kullanan T-SQL ile oluşturulan varsayılan kısıtlamalar geçersiz kılar varsayılan değerleri sağlayın olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="e1b78-168">This is because Entity Framework queries automatically supply default values which will override the default constraints created in T-SQL that use SESSION_CONTEXT.</span></span> <span data-ttu-id="e1b78-169">Varsayılan kısıtlamalar örnek projesinde kullanmak için örneği için Tenantıd DataClasses.cs (ve çalışma Add-Migration Paket Yöneticisi konsolunda) kaldırın ve T-SQL alanın yalnızca veritabanı tablolarında var olduğundan emin olmak için kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1b78-169">To use default constraints in the sample project, for instance, you should remove TenantId from DataClasses.cs (and run Add-Migration in the Package Manager Console) and use T-SQL to ensure that the field only exists in the database tables.</span></span> <span data-ttu-id="e1b78-170">Bu şekilde EF otomatik olarak yanlış varsayılan değerler veri eklerken sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="e1b78-170">This way, EF will not automatically supply incorrect default values when inserting data.</span></span> 
> 
> 

### <a name="optional-enable-a-superuser-to-access-all-rows"></a><span data-ttu-id="e1b78-171">(İsteğe bağlı) "Tüm satırları erişmek bir süper kullanıcı" etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="e1b78-171">(Optional) Enable a "superuser" to access all rows</span></span>
<span data-ttu-id="e1b78-172">Bazı uygulamalarda tüm parça tüm kiracılar arasında raporlamayı etkinleştirmek için ya da Kiracı satırları veritabanları arasında taşınması parça bölünmüş/birleştirme işlemleri gerçekleştirmek için "tüm satırları örneği için erişebilen bir süper kullanıcı" oluşturmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1b78-172">Some applications may want to create a "superuser" who can access all rows, for instance, in order to enable reporting across all tenants on all shards, or to perform Split/Merge operations on shards that involve moving tenant rows between databases.</span></span> <span data-ttu-id="e1b78-173">Bu ayarı etkinleştirmek için her parça veritabanında yeni bir SQL kullanıcısının ("süper kullanıcı" Bu örnekte) oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1b78-173">To enable this, you should create a new SQL user ("superuser" in this example) in each shard database.</span></span> <span data-ttu-id="e1b78-174">Ardından bu kullanıcının tüm satırları erişmesine imkan tanıyan yeni bir koşul işlevi güvenlik ilkesiyle alter:</span><span class="sxs-lookup"><span data-stu-id="e1b78-174">Then alter the security policy with a new predicate function that allows this user to access all rows:</span></span>

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

-- Atomically swap in the new predicate function on each table
ALTER SECURITY POLICY rls.tenantAccessPolicy
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts
GO
```


### <a name="maintenance"></a><span data-ttu-id="e1b78-175">Bakım</span><span class="sxs-lookup"><span data-stu-id="e1b78-175">Maintenance</span></span>
* <span data-ttu-id="e1b78-176">**Yeni parça ekleme**: tüm yeni parça üzerinde RLS etkinleştirmek için T-SQL betiği yürütmeniz gerekir, aksi takdirde bu parça sorgulamaları değil filtrelenir.</span><span class="sxs-lookup"><span data-stu-id="e1b78-176">**Adding new shards**: You must execute the T-SQL script to enable RLS on any new shards, otherwise queries on these shards will not be filtered.</span></span>
* <span data-ttu-id="e1b78-177">**Yeni tablo ekleme**: yeni bir tablo oluşturulduğunda tüm bölümler için güvenlik ilkesini için bir filtre ve engelleme koşulu eklemeniz gerekir, aksi halde yeni bir tablo sorgularında değil filtrelenir.</span><span class="sxs-lookup"><span data-stu-id="e1b78-177">**Adding new tables**: You must add a filter and block predicate to the security policy on all shards whenever a new table is created, otherwise queries on the new table will not be filtered.</span></span> <span data-ttu-id="e1b78-178">Bu DDL tetikleyicisi kullanarak açıklandığı gibi otomatikleştirilebilir [yeni oluşturulan tabloları (blog) otomatik olarak Uygula satır düzeyi güvenlik](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span><span class="sxs-lookup"><span data-stu-id="e1b78-178">This can be automated using a DDL trigger, as described in [Apply Row-Level Security automatically to newly created tables (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span></span>

## <a name="summary"></a><span data-ttu-id="e1b78-179">Özet</span><span class="sxs-lookup"><span data-stu-id="e1b78-179">Summary</span></span>
<span data-ttu-id="e1b78-180">Esnek veritabanı araçlarını ve satır düzeyi güvenlik genişleme yapmak bir uygulamanın veri katmanı hem çok müşterili desteği ile birlikte kullanılan ve tek Kiracı parça olabilir.</span><span class="sxs-lookup"><span data-stu-id="e1b78-180">Elastic database tools and row-level security can be used together to scale out an application’s data tier with support for both multi-tenant and single-tenant shards.</span></span> <span data-ttu-id="e1b78-181">Çok kiracılı parça (çok sayıda kiracılar yalnızca birkaç satır veri olduğu özellikle durumlarda), verileri daha verimli bir şekilde depolamak için kullanılabilecek tek-Kiracı sırasında parça, premium kiracılar daha sıkı performans ve yalıtım ile desteklemek için kullanılabilir gereksinimleri.</span><span class="sxs-lookup"><span data-stu-id="e1b78-181">Multi-tenant shards can be used to store data more efficiently (particularly in cases where a large number of tenants have only a few rows of data), while single-tenant shards can be used to support premium tenants with stricter performance and isolation requirements.</span></span>  <span data-ttu-id="e1b78-182">Daha fazla bilgi için bkz: [satır düzeyi güvenlik başvurusu](https://msdn.microsoft.com/library/dn765131).</span><span class="sxs-lookup"><span data-stu-id="e1b78-182">For more information, see [Row-Level Security reference](https://msdn.microsoft.com/library/dn765131).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e1b78-183">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e1b78-183">Additional resources</span></span>
* [<span data-ttu-id="e1b78-184">Bir Azure esnek havuz nedir?</span><span class="sxs-lookup"><span data-stu-id="e1b78-184">What is an Azure elastic pool?</span></span>](sql-database-elastic-pool.md)
* [<span data-ttu-id="e1b78-185">Azure SQL Veritabanı ile ölçek genişletme</span><span class="sxs-lookup"><span data-stu-id="e1b78-185">Scaling out with Azure SQL Database</span></span>](sql-database-elastic-scale-introduction.md)
* [<span data-ttu-id="e1b78-186">Azure SQL Veritabanı ile Çok Kiracılı SaaS Uygulamaları için Tasarım Desenleri</span><span class="sxs-lookup"><span data-stu-id="e1b78-186">Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database</span></span>](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [<span data-ttu-id="e1b78-187">Azure AD ve OpenID Connect kullanarak çok müşterili uygulamalarda kimlik doğrulama</span><span class="sxs-lookup"><span data-stu-id="e1b78-187">Authentication in multitenant apps, using Azure AD and OpenID Connect</span></span>](../guidance/guidance-multitenant-identity-authenticate.md)
* [<span data-ttu-id="e1b78-188">Tailspin Surveys uygulaması</span><span class="sxs-lookup"><span data-stu-id="e1b78-188">Tailspin Surveys application</span></span>](../guidance/guidance-multitenant-identity-tailspin.md)

## <a name="questions-and-feature-requests"></a><span data-ttu-id="e1b78-189">Sorular ve özellik istekleri</span><span class="sxs-lookup"><span data-stu-id="e1b78-189">Questions and Feature Requests</span></span>
<span data-ttu-id="e1b78-190">Sorular için lütfen bize üzerinde ulaşmak [SQL veritabanı Forumu](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) ve özellik istekler için lütfen bunları Ekle [SQL veritabanı geri bildirim Forumunda](https://feedback.azure.com/forums/217321-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="e1b78-190">For questions, please reach out to us on the [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them to the [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-tools-multi-tenant-row-level-security/blogging-app.png
<!--anchors-->


