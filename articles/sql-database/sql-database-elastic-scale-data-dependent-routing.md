---
title: "Azure SQL veritabanı ile yönlendirme bağımlı veri | Microsoft Docs"
description: "Veri bağımlı yönlendirme, Azure SQL veritabanında parçalı veritabanlarının bir özellik için .NET uygulamalarında ShardMapManager sınıfını kullanma"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: cad09e15-5561-4448-aa18-b38f54cda004
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: ddove
ms.openlocfilehash: 6b68bbb0133afd1493acdb58f79f3eeaf6a8d7cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="data-dependent-routing"></a><span data-ttu-id="aae2d-103">Verilere bağımlı yönlendirme</span><span class="sxs-lookup"><span data-stu-id="aae2d-103">Data dependent routing</span></span>
<span data-ttu-id="aae2d-104">**Veri bağımlı yönlendirme** uygun bir veritabanına isteği yönlendirmek için bir sorguda veri kullanma yeteneği.</span><span class="sxs-lookup"><span data-stu-id="aae2d-104">**Data dependent routing** is the ability to use the data in a query to route the request to an appropriate database.</span></span> <span data-ttu-id="aae2d-105">Bu temel düzeni parçalı veritabanları ile çalışırken.</span><span class="sxs-lookup"><span data-stu-id="aae2d-105">This is a fundamental pattern when working with sharded databases.</span></span> <span data-ttu-id="aae2d-106">Özellikle parçalama anahtar sorgu parçası değilse, istek bağlamını isteği yönlendirmek için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="aae2d-106">The request context may also be used to route the request, especially if the sharding key is not part of the query.</span></span> <span data-ttu-id="aae2d-107">Her özel bir sorgu veya veri bağımlı yönlendirme kullanarak bir uygulamayı işlemde istek başına tek bir veritabanına erişmek için sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="aae2d-107">Each specific query or transaction in an application using data dependent routing is restricted to accessing a single database per request.</span></span> <span data-ttu-id="aae2d-108">Azure SQL veritabanı esnek araçlar için bu yönlendirme ile gerçekleştirilir  **[ShardMapManager sınıfı](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)**  ADO.NET uygulamalarında.</span><span class="sxs-lookup"><span data-stu-id="aae2d-108">For the Azure SQL Database Elastic tools, this routing is accomplished with the **[ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)** in ADO.NET applications.</span></span>

<span data-ttu-id="aae2d-109">Uygulama çeşitli bağlantı dizeleri ya da parçalı ortamında verileri farklı dilimleri ilişkili DB konumları izlemek zorunda değildir.</span><span class="sxs-lookup"><span data-stu-id="aae2d-109">The application does not need to track various connection strings or DB locations associated with different slices of data in the sharded environment.</span></span> <span data-ttu-id="aae2d-110">Bunun yerine, [parça eşleme Yöneticisi](sql-database-elastic-scale-shard-map-management.md) tabanlı açar bağlantılar gerektiğinde, doğru veritabanlarına parça eşleme ve uygulamanın isteği hedefidir parçalama anahtarının değerini veriler üzerinde.</span><span class="sxs-lookup"><span data-stu-id="aae2d-110">Instead, the [Shard Map Manager](sql-database-elastic-scale-shard-map-management.md) opens connections to the correct databases when needed, based on the data in the shard map and the value of the sharding key that is the target of the application’s request.</span></span> <span data-ttu-id="aae2d-111">Genellikle anahtarıdır *customer_id*, *tenant_id*, *date_key*, veya veritabanı isteğin temel parametresi bazı bir belirli tanıtıcı).</span><span class="sxs-lookup"><span data-stu-id="aae2d-111">The key is typically the *customer_id*, *tenant_id*, *date_key*, or some other specific identifier that is a fundamental parameter of the database request).</span></span> 

<span data-ttu-id="aae2d-112">Daha fazla bilgi için bkz: [ölçeklendirme çıkışı SQL Server ile veri bağımlı yönlendirme](https://technet.microsoft.com/library/cc966448.aspx).</span><span class="sxs-lookup"><span data-stu-id="aae2d-112">For more information, see [Scaling Out SQL Server with Data Dependent Routing](https://technet.microsoft.com/library/cc966448.aspx).</span></span>

## <a name="download-the-client-library"></a><span data-ttu-id="aae2d-113">İstemci kitaplığını yükle</span><span class="sxs-lookup"><span data-stu-id="aae2d-113">Download the client library</span></span>
<span data-ttu-id="aae2d-114">Sınıfını almak için yükleme [esnek veritabanı istemci Kitaplığı](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span><span class="sxs-lookup"><span data-stu-id="aae2d-114">To get the class, install the [Elastic Database Client Library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span> 

## <a name="using-a-shardmapmanager-in-a-data-dependent-routing-application"></a><span data-ttu-id="aae2d-115">Bir ShardMapManager bir veri bağımlı yönlendirme uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="aae2d-115">Using a ShardMapManager in a data dependent routing application</span></span>
<span data-ttu-id="aae2d-116">Uygulamaları örneği **ShardMapManager** başlatılması sırasında fabrikada çağrısı kullanarak  **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="aae2d-116">Applications should instantiate the **ShardMapManager** during initialization, using the factory call **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**.</span></span> <span data-ttu-id="aae2d-117">Bu örnekte, hem bir **ShardMapManager** ve belirli bir **ShardMap** içerdiği başlatılır.</span><span class="sxs-lookup"><span data-stu-id="aae2d-117">In this example, both a **ShardMapManager** and a specific **ShardMap** that it contains are initialized.</span></span> <span data-ttu-id="aae2d-118">Bu örnek GetSqlShardMapManager gösterir ve [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="aae2d-118">This example shows the GetSqlShardMapManager and [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) methods.</span></span>

    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString, 
                      ShardMapManagerLoadPolicy.Lazy);
    RangeShardMap<int> customerShardMap = smm.GetRangeShardMap<int>("customerMap"); 

### <a name="use-lowest-privilege-credentials-possible-for-getting-the-shard-map"></a><span data-ttu-id="aae2d-119">Parça eşleme için olası en düşük ayrıcalıklı kimlik bilgileri kullanın</span><span class="sxs-lookup"><span data-stu-id="aae2d-119">Use lowest privilege credentials possible for getting the shard map</span></span>
<span data-ttu-id="aae2d-120">Bir uygulama parça eşleme düzenleme değil, Fabrika yönteminde kullanılan kimlik bilgileri yalnızca salt okunur izinleri olmalıdır **genel parça eşleme** veritabanı.</span><span class="sxs-lookup"><span data-stu-id="aae2d-120">If an application is not manipulating the shard map itself, the credentials used in the factory method should have just read-only permissions on the **Global Shard Map** database.</span></span> <span data-ttu-id="aae2d-121">Bu kimlik bilgileri bağlantıları parça eşleme Yöneticisi'ni açmak için kullanılan kimlik bilgileri genellikle farklıdır.</span><span class="sxs-lookup"><span data-stu-id="aae2d-121">These credentials are typically different from credentials used to open connections to the shard map manager.</span></span> <span data-ttu-id="aae2d-122">Ayrıca bkz. [esnek veritabanı istemci kitaplığına erişmek için kullanılan kimlik bilgileri](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="aae2d-122">See also [Credentials used to access the Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span> 

## <a name="call-the-openconnectionforkey-method"></a><span data-ttu-id="aae2d-123">OpenConnectionForKey yöntemini çağırın</span><span class="sxs-lookup"><span data-stu-id="aae2d-123">Call the OpenConnectionForKey method</span></span>
<span data-ttu-id="aae2d-124"> **[ShardMap.OpenConnectionForKey yöntemi](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)**  bir ADO.Net bağlantı komutları değerine göre uygun veritabanı verme için hazır döndürür **anahtar** parametre.</span><span class="sxs-lookup"><span data-stu-id="aae2d-124">The **[ShardMap.OpenConnectionForKey method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)** returns an ADO.Net connection ready for issuing commands to the appropriate database based on the value of the **key** parameter.</span></span> <span data-ttu-id="aae2d-125">Parça bilgi uygulama tarafından önbelleğe alınmış **ShardMapManager**, bu istekleri genellikle bir veritabanı araması karşı içermeyen **genel parça eşleme** veritabanı.</span><span class="sxs-lookup"><span data-stu-id="aae2d-125">Shard information is cached in the application by the **ShardMapManager**, so these requests do not typically involve a database lookup against the **Global Shard Map** database.</span></span> 

    // Syntax: 
    public SqlConnection OpenConnectionForKey<TKey>(
        TKey key,
        string connectionString,
        ConnectionOptions options
    )


* <span data-ttu-id="aae2d-126">**Anahtar** parametresi arama anahtarı olarak parça eşlemeye istek için uygun veritabanı belirlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="aae2d-126">The **key** parameter is used as a lookup key into the shard map to determine the appropriate database for the request.</span></span> 
* <span data-ttu-id="aae2d-127">**ConnectionString** yalnızca kullanıcı kimlik bilgilerini istenen bağlantı için geçirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="aae2d-127">The **connectionString** is used to pass only the user credentials for the desired connection.</span></span> <span data-ttu-id="aae2d-128">Hiçbir veritabanı adı veya sunucu adı bu dahil edilen *connectionString* yöntemi ve veritabanı sunucusu kullanarak belirlediğinden **ShardMap**.</span><span class="sxs-lookup"><span data-stu-id="aae2d-128">No database name or server name are included in this *connectionString* since the method will determine the database and server using the **ShardMap**.</span></span> 
* <span data-ttu-id="aae2d-129"> **[ConnectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)**  ayarlanmalı **ConnectionOptions.Validate** burada parça eşleyen bir ortam değişebilir ve satır diğer veritabanlarına sonucu olarak taşırsanız Bölünmüş veya birleştirme işlemleri.</span><span class="sxs-lookup"><span data-stu-id="aae2d-129">The **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)** should be set to **ConnectionOptions.Validate** if an environment where shard maps may change and rows may move to other databases as a result of split or merge operations.</span></span> <span data-ttu-id="aae2d-130">Bu hedefte yerel parça eşleme için kısa bir sorgu içerir bağlantı uygulamaya teslim edilmeden önce veritabanı (değil genel parça eşleme için).</span><span class="sxs-lookup"><span data-stu-id="aae2d-130">This involves a brief query to the local shard map on the target database (not to the global shard map) before the connection is delivered to the application.</span></span> 

<span data-ttu-id="aae2d-131">(Önbellek yanlış olduğunu belirten) yerel parça eşleme karşı doğrulama başarısız olursa, parça eşleme Yöneticisi arama yeni doğru değerini edinme, önbellek, güncelleştirme ve elde ve uygun veritabanı dönmek için genel parça harita sorgulama bağlantı.</span><span class="sxs-lookup"><span data-stu-id="aae2d-131">If the validation against the local shard map fails (indicating that the cache is incorrect), the Shard Map Manager will query the global shard map to obtain the new correct value for the lookup, update the cache, and obtain and return the appropriate database connection.</span></span> 

<span data-ttu-id="aae2d-132">Kullanım **ConnectionOptions.None** uygulamanın çevrimiçi durumdayken yalnızca zaman parça eşleme değişiklikleri beklenmez.</span><span class="sxs-lookup"><span data-stu-id="aae2d-132">Use **ConnectionOptions.None** only when shard mapping changes are not expected while an application is online.</span></span> <span data-ttu-id="aae2d-133">Bu durumda, önbelleğe alınan değer her zaman doğru olması için kabul edilebilir ve hedef veritabanına ek gidiş dönüş doğrulama çağrısı güvenle atlanabilir.</span><span class="sxs-lookup"><span data-stu-id="aae2d-133">In that case, the cached values can be assumed to always be correct, and the extra round-trip validation call to the target database can be safely skipped.</span></span> <span data-ttu-id="aae2d-134">Veritabanı trafiğini azaltır.</span><span class="sxs-lookup"><span data-stu-id="aae2d-134">That reduces database traffic.</span></span> <span data-ttu-id="aae2d-135">**ConnectionOptions** bir değer parçalama değişiklikleri beklenen olup olmadığını belirtmek için bir yapılandırma dosyası veya bir zaman aralığında sırasında değil de ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="aae2d-135">The **connectionOptions** may also be set via a value in a configuration file to indicate whether sharding changes are expected or not during a period of time.</span></span>  

<span data-ttu-id="aae2d-136">Bu örnek bir tamsayı anahtarının değerini kullanır **CustomerID**kullanarak bir **ShardMap** adlı nesne **customerShardMap**.</span><span class="sxs-lookup"><span data-stu-id="aae2d-136">This example uses the value of an integer key **CustomerID**, using a **ShardMap** object named **customerShardMap**.</span></span>  

    int customerId = 12345; 
    int newPersonId = 4321; 

    // Connect to the shard for that customer ID. No need to call a SqlConnection 
    // constructor followed by the Open method.
    using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId, 
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
    { 
        // Execute a simple command. 
        SqlCommand cmd = conn.CreateCommand(); 
        cmd.CommandText = @"UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID"; 

        cmd.Parameters.AddWithValue("@customerID", customerId); 
        cmd.Parameters.AddWithValue("@newPersonID", newPersonId); 
        cmd.ExecuteNonQuery(); 
    }  

<span data-ttu-id="aae2d-137">**OpenConnectionForKey** yöntemi doğru veritabanına yeni bir zaten açık bağlantı döndürür.</span><span class="sxs-lookup"><span data-stu-id="aae2d-137">The **OpenConnectionForKey** method returns a new already-open connection to the correct database.</span></span> <span data-ttu-id="aae2d-138">Bu şekilde kullanılan bağlantılar hala ADO.Net bağlantı havuzu tam avantajından yararlanmak.</span><span class="sxs-lookup"><span data-stu-id="aae2d-138">Connections utilized in this way still take full advantage of ADO.Net connection pooling.</span></span> <span data-ttu-id="aae2d-139">İşlemler ve istekleri tarafından bir parça aynı anda karşılanabilir sürece, bu uygulamada zaten ADO.Net kullanarak gerekli yalnızca değişikliği olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="aae2d-139">As long as transactions and requests can be satisfied by one shard at a time, this should be the only modification necessary in an application already using ADO.Net.</span></span> 

<span data-ttu-id="aae2d-140"> **[OpenConnectionForKeyAsync yöntemi](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)**  da uygulamanızı ADO.Net ile zaman uyumsuz programlama kullanım yaparsa kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="aae2d-140">The **[OpenConnectionForKeyAsync method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)** is also available if your application makes use asynchronous programming with ADO.Net.</span></span> <span data-ttu-id="aae2d-141">Davranışını ADO eşdeğer yönlendirme bağımlı veridir. NET'in  **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)**  yöntemi.</span><span class="sxs-lookup"><span data-stu-id="aae2d-141">Its behavior is the data dependent routing equivalent of ADO.Net's **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)** method.</span></span>

## <a name="integrating-with-transient-fault-handling"></a><span data-ttu-id="aae2d-142">Geçici hata işleme ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="aae2d-142">Integrating with transient fault handling</span></span>
<span data-ttu-id="aae2d-143">Veri erişimi uygulamaları bulutta geliştirilmesi konusunda en iyi uygulama, uygulama tarafından geçici hataları yakalanır ve işlemleri hata atmadan önce birkaç kez denenir emin olmaktır.</span><span class="sxs-lookup"><span data-stu-id="aae2d-143">A best practice in developing data access applications in the cloud is to ensure that transient faults are caught by the app, and that the operations are retried several times before throwing an error.</span></span> <span data-ttu-id="aae2d-144">Geçici hata bulut uygulamaları için işleme sırasında ele alınmıştır [geçici hata işleme](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx).</span><span class="sxs-lookup"><span data-stu-id="aae2d-144">Transient fault handling for cloud applications is discussed at [Transient Fault Handling](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx).</span></span> 

<span data-ttu-id="aae2d-145">Geçici hata işleme, veri bağımlı yönlendirme desenle doğal olarak bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="aae2d-145">Transient fault handling can coexist naturally with the Data Dependent Routing pattern.</span></span> <span data-ttu-id="aae2d-146">Tüm veri erişim isteği dahil olmak üzere yeniden denemek için önemli gereksinimdir **kullanarak** veri bağımlı yönlendirme bağlantısı elde bloğu.</span><span class="sxs-lookup"><span data-stu-id="aae2d-146">The key requirement is to retry the entire data access request including the **using** block that obtained the data-dependent routing connection.</span></span> <span data-ttu-id="aae2d-147">Yukarıdaki örnekte (vurgulanmış Not değiştirin) aşağıdaki gibi yeniden yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="aae2d-147">The example above could be rewritten as follows (note highlighted change).</span></span> 

### <a name="example---data-dependent-routing-with-transient-fault-handling"></a><span data-ttu-id="aae2d-148">Örnek - veri geçici hata işleme ile yönlendirme bağımlı</span><span class="sxs-lookup"><span data-stu-id="aae2d-148">Example - data dependent routing with transient fault handling</span></span>
<pre><code>int customerId = 12345; 
int newPersonId = 4321; 

<span style="background-color:  #FFFF00">Configuration.SqlRetryPolicy.ExecuteAction(() =&gt; </span> 
<span style="background-color:  #FFFF00">    { </span>
        // Connect to the shard for a customer ID. 
        using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId,  
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
        { 
            // Execute a simple command 
            SqlCommand cmd = conn.CreateCommand(); 

            cmd.CommandText = @&quot;UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID&quot;; 

            cmd.Parameters.AddWithValue(&quot;@customerID&quot;, customerId); 
            cmd.Parameters.AddWithValue(&quot;@newPersonID&quot;, newPersonId); 
            cmd.ExecuteNonQuery(); 

            Console.WriteLine(&quot;Update completed&quot;); 
        } 
<span style="background-color:  #FFFF00">    }); </span> 
</code></pre>


<span data-ttu-id="aae2d-149">Esnek veritabanı örnek uygulamasını derlerken geçici hata işleme uygulanması için gerekli paketleri otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="aae2d-149">Packages necessary to implement transient fault handling are downloaded automatically when you build the elastic database sample application.</span></span> <span data-ttu-id="aae2d-150">Paketleri de edinilebilir ayrı olarak [Kurumsal Library - geçici hata işleme uygulama blok](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/).</span><span class="sxs-lookup"><span data-stu-id="aae2d-150">Packages are also available separately at [Enterprise Library - Transient Fault Handling Application Block](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/).</span></span> <span data-ttu-id="aae2d-151">Sürüm 6.0 veya üstü kullanın.</span><span class="sxs-lookup"><span data-stu-id="aae2d-151">Use version 6.0 or later.</span></span> 

## <a name="transactional-consistency"></a><span data-ttu-id="aae2d-152">İşlem tutarlılığı</span><span class="sxs-lookup"><span data-stu-id="aae2d-152">Transactional consistency</span></span>
<span data-ttu-id="aae2d-153">İşlem özellikleri tüm işlemler için bir parça yerel olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="aae2d-153">Transactional properties are guaranteed for all operations local to a shard.</span></span> <span data-ttu-id="aae2d-154">Örneğin, bağlantı için hedef parça kapsamında veri bağımlı yönlendirme üzerinden gönderilen işlemleri yürütün.</span><span class="sxs-lookup"><span data-stu-id="aae2d-154">For example, transactions submitted through data-dependent routing execute within the scope of the target shard for the connection.</span></span> <span data-ttu-id="aae2d-155">Şu anda bir işlem içinde birden çok bağlantı kaydetme için sağlanan özelliği yoktur ve bu nedenle parça üzerinde gerçekleştirilen işlemler için işlem garanti vardır.</span><span class="sxs-lookup"><span data-stu-id="aae2d-155">At this time, there are no capabilities provided for enlisting multiple connections into a transaction, and therefore there are no transactional guarantees for operations performed across shards.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aae2d-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aae2d-156">Next steps</span></span>
<span data-ttu-id="aae2d-157">Bir parça detach veya bir parça yeniden eklemek için bkz: [parça eşleme sorunları düzeltmek için RecoveryManager sınıfını kullanma](sql-database-elastic-database-recovery-manager.md)</span><span class="sxs-lookup"><span data-stu-id="aae2d-157">To detach a shard, or to reattach a shard, see [Using the RecoveryManager class to fix shard map problems](sql-database-elastic-database-recovery-manager.md)</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

