---
title: "Azure SQL veritabanı ile yönlendirme bağımlı aaaData | Microsoft Docs"
description: "Nasıl toouse hello veri bağımlı yönlendirme, Azure SQL veritabanında parçalı veritabanlarının bir özellik için .NET uygulamalarında ShardMapManager sınıfı"
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
ms.openlocfilehash: 34014508ae01905686791fe096bb275cb84f53b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-dependent-routing"></a><span data-ttu-id="5c4ef-103">Verilere bağımlı yönlendirme</span><span class="sxs-lookup"><span data-stu-id="5c4ef-103">Data dependent routing</span></span>
<span data-ttu-id="5c4ef-104">**Veri bağımlı yönlendirme** hello özelliği toouse hello veritabanında bir sorgu tooroute hello isteği tooan uygun verilerdir.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-104">**Data dependent routing** is hello ability toouse hello data in a query tooroute hello request tooan appropriate database.</span></span> <span data-ttu-id="5c4ef-105">Bu temel düzeni parçalı veritabanları ile çalışırken.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-105">This is a fundamental pattern when working with sharded databases.</span></span> <span data-ttu-id="5c4ef-106">özellikle hello parçalama anahtar hello sorgu parçası değilse hello istek bağlamı kullanılan tooroute hello isteği de olabilir.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-106">hello request context may also be used tooroute hello request, especially if hello sharding key is not part of hello query.</span></span> <span data-ttu-id="5c4ef-107">Her özel bir sorgu veya işlem veri bağımlı yönlendirme kullanarak bir uygulama içinde kısıtlı tooaccessing istek başına tek bir veritabanı değil.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-107">Each specific query or transaction in an application using data dependent routing is restricted tooaccessing a single database per request.</span></span> <span data-ttu-id="5c4ef-108">Hello Azure SQL veritabanı esnek araçlar bu üretim hello ile gerçekleştirilir  **[ShardMapManager sınıfı](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)**  ADO.NET uygulamalarında.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-108">For hello Azure SQL Database Elastic tools, this routing is accomplished with hello **[ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)** in ADO.NET applications.</span></span>

<span data-ttu-id="5c4ef-109">Merhaba uygulaması, çeşitli bağlantı dizeleri veya hello parçalı ortamında verileri farklı dilimleri ilişkili DB konumları tootrack gerekmez.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-109">hello application does not need tootrack various connection strings or DB locations associated with different slices of data in hello sharded environment.</span></span> <span data-ttu-id="5c4ef-110">Bunun yerine, hello [parça eşleme Yöneticisi](sql-database-elastic-scale-shard-map-management.md) hello parça eşleme ve hello hello uygulamanın isteği hello hedefidir hello parçalama anahtarının değerini hello veriler temelinde gerekli olduğunda, açılır bağlantıları toohello doğru veritabanları.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-110">Instead, hello [Shard Map Manager](sql-database-elastic-scale-shard-map-management.md) opens connections toohello correct databases when needed, based on hello data in hello shard map and hello value of hello sharding key that is hello target of hello application’s request.</span></span> <span data-ttu-id="5c4ef-111">Merhaba anahtarıdır genellikle hello *customer_id*, *tenant_id*, *date_key*, veya temel parametresi hello veritabanı isteğinin bazı bir belirli tanıtıcı).</span><span class="sxs-lookup"><span data-stu-id="5c4ef-111">hello key is typically hello *customer_id*, *tenant_id*, *date_key*, or some other specific identifier that is a fundamental parameter of hello database request).</span></span> 

<span data-ttu-id="5c4ef-112">Daha fazla bilgi için bkz: [ölçeklendirme çıkışı SQL Server ile veri bağımlı yönlendirme](https://technet.microsoft.com/library/cc966448.aspx).</span><span class="sxs-lookup"><span data-stu-id="5c4ef-112">For more information, see [Scaling Out SQL Server with Data Dependent Routing](https://technet.microsoft.com/library/cc966448.aspx).</span></span>

## <a name="download-hello-client-library"></a><span data-ttu-id="5c4ef-113">Merhaba istemci kitaplığı indirin</span><span class="sxs-lookup"><span data-stu-id="5c4ef-113">Download hello client library</span></span>
<span data-ttu-id="5c4ef-114">tooget hello sınıfı, yükleme hello [esnek veritabanı istemci Kitaplığı](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span><span class="sxs-lookup"><span data-stu-id="5c4ef-114">tooget hello class, install hello [Elastic Database Client Library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span> 

## <a name="using-a-shardmapmanager-in-a-data-dependent-routing-application"></a><span data-ttu-id="5c4ef-115">Bir ShardMapManager bir veri bağımlı yönlendirme uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="5c4ef-115">Using a ShardMapManager in a data dependent routing application</span></span>
<span data-ttu-id="5c4ef-116">Uygulamaları hello örneği **ShardMapManager** hello fabrikada çağrısı kullanarak başlatma sırasında  **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-116">Applications should instantiate hello **ShardMapManager** during initialization, using hello factory call **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**.</span></span> <span data-ttu-id="5c4ef-117">Bu örnekte, hem bir **ShardMapManager** ve belirli bir **ShardMap** içerdiği başlatılır.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-117">In this example, both a **ShardMapManager** and a specific **ShardMap** that it contains are initialized.</span></span> <span data-ttu-id="5c4ef-118">Gösterir hello GetSqlShardMapManager Bu örnek ve [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-118">This example shows hello GetSqlShardMapManager and [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) methods.</span></span>

    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString, 
                      ShardMapManagerLoadPolicy.Lazy);
    RangeShardMap<int> customerShardMap = smm.GetRangeShardMap<int>("customerMap"); 

### <a name="use-lowest-privilege-credentials-possible-for-getting-hello-shard-map"></a><span data-ttu-id="5c4ef-119">Merhaba parça eşleme için olası en düşük ayrıcalıklı kimlik bilgileri kullanın</span><span class="sxs-lookup"><span data-stu-id="5c4ef-119">Use lowest privilege credentials possible for getting hello shard map</span></span>
<span data-ttu-id="5c4ef-120">Bir uygulama hello parça eşleme kendisini düzenleme değil, hello Fabrika yönteminde kullanılan hello kimlik hello üzerinde salt okunur yalnızca izinleri olmalıdır **genel parça eşleme** veritabanı.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-120">If an application is not manipulating hello shard map itself, hello credentials used in hello factory method should have just read-only permissions on hello **Global Shard Map** database.</span></span> <span data-ttu-id="5c4ef-121">Bu kimlik bilgileri kullanılan kimlik bilgileri tooopen bağlantıları toohello parça eşleme yöneticisinden genellikle farklıdır.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-121">These credentials are typically different from credentials used tooopen connections toohello shard map manager.</span></span> <span data-ttu-id="5c4ef-122">Ayrıca bkz. [kimlik bilgileri kullanılan tooaccess hello esnek veritabanı istemci Kitaplığı](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="5c4ef-122">See also [Credentials used tooaccess hello Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span> 

## <a name="call-hello-openconnectionforkey-method"></a><span data-ttu-id="5c4ef-123">Merhaba OpenConnectionForKey yöntemini çağırın</span><span class="sxs-lookup"><span data-stu-id="5c4ef-123">Call hello OpenConnectionForKey method</span></span>
<span data-ttu-id="5c4ef-124">Merhaba  **[ShardMap.OpenConnectionForKey yöntemi](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)**  bir ADO.Net bağlantı komutları toohello uygun veritabanı hello değerine göre hello verme için hazır döndürür **anahtar**parametresi.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-124">hello **[ShardMap.OpenConnectionForKey method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)** returns an ADO.Net connection ready for issuing commands toohello appropriate database based on hello value of hello **key** parameter.</span></span> <span data-ttu-id="5c4ef-125">Parça bilgileri tarafından hello hello uygulamada önbelleğe **ShardMapManager**, bu istekleri genellikle bir veritabanı araması hello karşı içermeyen **genel parça eşleme** veritabanı.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-125">Shard information is cached in hello application by hello **ShardMapManager**, so these requests do not typically involve a database lookup against hello **Global Shard Map** database.</span></span> 

    // Syntax: 
    public SqlConnection OpenConnectionForKey<TKey>(
        TKey key,
        string connectionString,
        ConnectionOptions options
    )


* <span data-ttu-id="5c4ef-126">Merhaba **anahtar** parametresi kullanılır arama anahtarı olarak hello parça eşleme toodetermine hello uygun veritabanına hello talebi.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-126">hello **key** parameter is used as a lookup key into hello shard map toodetermine hello appropriate database for hello request.</span></span> 
* <span data-ttu-id="5c4ef-127">Merhaba **connectionString** kullanılan toopass istenen hello bağlantı için yalnızca hello kullanıcı kimlik bilgileri olan.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-127">hello **connectionString** is used toopass only hello user credentials for hello desired connection.</span></span> <span data-ttu-id="5c4ef-128">Hiçbir veritabanı adı veya sunucu adı bu dahil edilen *connectionString* hello yöntemi hello veritabanı ve sunucu hello kullanarak belirlediğinden **ShardMap**.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-128">No database name or server name are included in this *connectionString* since hello method will determine hello database and server using hello **ShardMap**.</span></span> 
* <span data-ttu-id="5c4ef-129">Merhaba  **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)**  çok ayarlanmalıdır**ConnectionOptions.Validate** burada parça eşleyen bir ortam değiştirebilir ve satırlar tooother veritabanları taşındığında bir bölme ve birleştirme işlemleri sonucu.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-129">hello **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)** should be set too**ConnectionOptions.Validate** if an environment where shard maps may change and rows may move tooother databases as a result of split or merge operations.</span></span> <span data-ttu-id="5c4ef-130">Bu kısa sorgu toohello yerel parça eşleme içerir hello bağlantı önce hello hedef veritabanında (toohello genel parça eşleme değil) toohello uygulama teslim edilir.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-130">This involves a brief query toohello local shard map on hello target database (not toohello global shard map) before hello connection is delivered toohello application.</span></span> 

<span data-ttu-id="5c4ef-131">(Merhaba önbellek yanlış olduğunu belirten) hello yerel parça eşleme karşı Hello doğrulama başarısız olursa, hello parça eşleme Yöneticisi hello genel parça eşleme tooobtain hello yeni doğru değeri sorgu hello arama için güncelleştirme hello önbellek ve edinmeli ve dönüş hello uygun veritabanı bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-131">If hello validation against hello local shard map fails (indicating that hello cache is incorrect), hello Shard Map Manager will query hello global shard map tooobtain hello new correct value for hello lookup, update hello cache, and obtain and return hello appropriate database connection.</span></span> 

<span data-ttu-id="5c4ef-132">Kullanım **ConnectionOptions.None** uygulamanın çevrimiçi durumdayken yalnızca zaman parça eşleme değişiklikleri beklenmez.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-132">Use **ConnectionOptions.None** only when shard mapping changes are not expected while an application is online.</span></span> <span data-ttu-id="5c4ef-133">Bu durumda, önbelleğe alınmış hello değerleri tooalways doğru ve hello çok gidiş dönüş doğrulama çağrısı toohello hedef veritabanı güvenle atlanabilir varsayılabilir.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-133">In that case, hello cached values can be assumed tooalways be correct, and hello extra round-trip validation call toohello target database can be safely skipped.</span></span> <span data-ttu-id="5c4ef-134">Veritabanı trafiğini azaltır.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-134">That reduces database traffic.</span></span> <span data-ttu-id="5c4ef-135">Merhaba **connectionOptions** ayrıca bir yapılandırma dosyası tooindicate değerinde aracılığıyla parçalama değişiklikleri beklenen olup olmadığını veya bir zaman aralığında değil sırasında ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-135">hello **connectionOptions** may also be set via a value in a configuration file tooindicate whether sharding changes are expected or not during a period of time.</span></span>  

<span data-ttu-id="5c4ef-136">Bu örnek bir tamsayı anahtarı hello değerini kullanır **CustomerID**kullanarak bir **ShardMap** adlı nesne **customerShardMap**.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-136">This example uses hello value of an integer key **CustomerID**, using a **ShardMap** object named **customerShardMap**.</span></span>  

    int customerId = 12345; 
    int newPersonId = 4321; 

    // Connect toohello shard for that customer ID. No need toocall a SqlConnection 
    // constructor followed by hello Open method.
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

<span data-ttu-id="5c4ef-137">Merhaba **OpenConnectionForKey** yöntemi yeni bir bağlantı zaten açık toohello doğru veritabanı döndürür.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-137">hello **OpenConnectionForKey** method returns a new already-open connection toohello correct database.</span></span> <span data-ttu-id="5c4ef-138">Bu şekilde kullanılan bağlantılar hala ADO.Net bağlantı havuzu tam avantajından yararlanmak.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-138">Connections utilized in this way still take full advantage of ADO.Net connection pooling.</span></span> <span data-ttu-id="5c4ef-139">İşlemler ve istekleri tarafından bir parça aynı anda karşılanabilir sürece bu hello yalnızca değişikliği zaten ADO.Net kullanarak bir uygulama gerekli olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-139">As long as transactions and requests can be satisfied by one shard at a time, this should be hello only modification necessary in an application already using ADO.Net.</span></span> 

<span data-ttu-id="5c4ef-140">Merhaba  **[OpenConnectionForKeyAsync yöntemi](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)**  da uygulamanızı ADO.Net ile zaman uyumsuz programlama kullanım yaparsa kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-140">hello **[OpenConnectionForKeyAsync method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)** is also available if your application makes use asynchronous programming with ADO.Net.</span></span> <span data-ttu-id="5c4ef-141">Davranışını hello ADO eşdeğer yönlendirme bağımlı verilerdir. NET'in  **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)**  yöntemi.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-141">Its behavior is hello data dependent routing equivalent of ADO.Net's **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)** method.</span></span>

## <a name="integrating-with-transient-fault-handling"></a><span data-ttu-id="5c4ef-142">Geçici hata işleme ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="5c4ef-142">Integrating with transient fault handling</span></span>
<span data-ttu-id="5c4ef-143">Geçici hataları hello uygulama tarafından yakalanan ve bir hata atmadan önce birkaç kez yeniden hello işlemleri tooensure veri erişimi uygulamaları hello bulutta geliştirilmesi konusunda en iyi bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-143">A best practice in developing data access applications in hello cloud is tooensure that transient faults are caught by hello app, and that hello operations are retried several times before throwing an error.</span></span> <span data-ttu-id="5c4ef-144">Geçici hata bulut uygulamaları için işleme sırasında ele alınmıştır [geçici hata işleme](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx).</span><span class="sxs-lookup"><span data-stu-id="5c4ef-144">Transient fault handling for cloud applications is discussed at [Transient Fault Handling](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx).</span></span> 

<span data-ttu-id="5c4ef-145">Geçici hata işleme hello veri bağımlı yönlendirme desenle doğal olarak bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-145">Transient fault handling can coexist naturally with hello Data Dependent Routing pattern.</span></span> <span data-ttu-id="5c4ef-146">Merhaba anahtar tooretry hello tüm veri erişim isteği hello dahil olmak üzere gereksinimdir **kullanarak** hello veri bağımlı yönlendirme bağlantısı elde bloğu.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-146">hello key requirement is tooretry hello entire data access request including hello **using** block that obtained hello data-dependent routing connection.</span></span> <span data-ttu-id="5c4ef-147">Yukarıdaki örnekte Hello (vurgulanan değişiklik unutmayın) aşağıdaki gibi yeniden yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-147">hello example above could be rewritten as follows (note highlighted change).</span></span> 

### <a name="example---data-dependent-routing-with-transient-fault-handling"></a><span data-ttu-id="5c4ef-148">Örnek - veri geçici hata işleme ile yönlendirme bağımlı</span><span class="sxs-lookup"><span data-stu-id="5c4ef-148">Example - data dependent routing with transient fault handling</span></span>
<pre><code>int customerId = 12345; 
int newPersonId = 4321; 

<span style="background-color:  #FFFF00">Configuration.SqlRetryPolicy.ExecuteAction(() =&gt; </span> 
<span style="background-color:  #FFFF00">    { </span>
        // Connect toohello shard for a customer ID. 
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


<span data-ttu-id="5c4ef-149">Gerekli tooimplement geçici hata işleme olan paketler Merhaba esnek veritabanı örnek uygulaması oluşturduğunuzda otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-149">Packages necessary tooimplement transient fault handling are downloaded automatically when you build hello elastic database sample application.</span></span> <span data-ttu-id="5c4ef-150">Paketleri de edinilebilir ayrı olarak [Kurumsal Library - geçici hata işleme uygulama blok](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/).</span><span class="sxs-lookup"><span data-stu-id="5c4ef-150">Packages are also available separately at [Enterprise Library - Transient Fault Handling Application Block](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/).</span></span> <span data-ttu-id="5c4ef-151">Sürüm 6.0 veya üstü kullanın.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-151">Use version 6.0 or later.</span></span> 

## <a name="transactional-consistency"></a><span data-ttu-id="5c4ef-152">İşlem tutarlılığı</span><span class="sxs-lookup"><span data-stu-id="5c4ef-152">Transactional consistency</span></span>
<span data-ttu-id="5c4ef-153">İşlem özellikleri için tüm işlemleri yerel tooa parça sağlanır.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-153">Transactional properties are guaranteed for all operations local tooa shard.</span></span> <span data-ttu-id="5c4ef-154">Örneğin, veri bağımlı yönlendirme üzerinden gönderilen işlemleri hello kapsamını hello hedef parça hello bağlantı içinde yürütün.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-154">For example, transactions submitted through data-dependent routing execute within hello scope of hello target shard for hello connection.</span></span> <span data-ttu-id="5c4ef-155">Şu anda bir işlem içinde birden çok bağlantı kaydetme için sağlanan özelliği yoktur ve bu nedenle parça üzerinde gerçekleştirilen işlemler için işlem garanti vardır.</span><span class="sxs-lookup"><span data-stu-id="5c4ef-155">At this time, there are no capabilities provided for enlisting multiple connections into a transaction, and therefore there are no transactional guarantees for operations performed across shards.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c4ef-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5c4ef-156">Next steps</span></span>
<span data-ttu-id="5c4ef-157">toodetach bir parça ya da tooreattach bir parça bakın [hello RecoveryManager sınıfı toofix parça eşlemesi sorunlarının kullanma](sql-database-elastic-database-recovery-manager.md)</span><span class="sxs-lookup"><span data-stu-id="5c4ef-157">toodetach a shard, or tooreattach a shard, see [Using hello RecoveryManager class toofix shard map problems](sql-database-elastic-database-recovery-manager.md)</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

