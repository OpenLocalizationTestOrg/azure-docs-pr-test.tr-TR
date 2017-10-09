---
title: "aaaAzure SQL veritabanı bellek içi teknolojileri | Microsoft Docs"
description: "Azure SQL veritabanı bellek içi teknolojileri işlem hello performansını ve analytics iş yükleri büyük ölçüde artırır. Bilgi nasıl bu teknolojiler tootake yararlanabilir."
services: sql-database
documentationCenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: 250ef341-90e5-492f-b075-b4750d237c05
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jodebrui
ms.openlocfilehash: 1bacd7297b2f9b018853088eabf2a2ee66a9cb43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a><span data-ttu-id="cf95c-104">SQL veritabanı'nda Bellek içi teknolojileri kullanılarak performansı en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="cf95c-104">Optimize performance by using In-Memory technologies in SQL Database</span></span>

<span data-ttu-id="cf95c-105">Azure SQL veritabanı'nda Bellek içi teknolojilerini kullanarak, performans iyileştirmeleri çeşitli iş yükleri ile elde edebilirsiniz: işlem (çevrimiçi işlem işleme (OLTP)), analytics (çevrimiçi analitik işlem (OLAP)) ve karma (karma işlem/analitik işleme (HTAP)).</span><span class="sxs-lookup"><span data-stu-id="cf95c-105">By using In-Memory technologies in Azure SQL Database, you can achieve performance improvements with various workloads: transactional (online transactional processing (OLTP)), analytics (online analytical processing (OLAP)), and mixed (hybrid transaction/analytical processing (HTAP)).</span></span> <span data-ttu-id="cf95c-106">Nedeniyle daha verimli sorgu ve işlem Merhaba, bellek içi teknolojileri de yardımcı tooreduce maliyeti.</span><span class="sxs-lookup"><span data-stu-id="cf95c-106">Because of hello more efficient query and transaction processing, In-Memory technologies also help you tooreduce cost.</span></span> <span data-ttu-id="cf95c-107">Fiyatlandırma katmanı hello veritabanı tooachieve performans artışı, tooupgrade hello genellikle gerekmez.</span><span class="sxs-lookup"><span data-stu-id="cf95c-107">You typically don't need tooupgrade hello pricing tier of hello database tooachieve performance gains.</span></span> <span data-ttu-id="cf95c-108">Bazı durumlarda, hatta yazdıramayabilirsiniz fiyatlandırma katmanı, yine de performans iyileştirmeleri bellek içi teknolojileriyle görüyorsanız sırasında hello azaltın.</span><span class="sxs-lookup"><span data-stu-id="cf95c-108">In some cases, you might even be able reduce hello pricing tier, while still seeing performance improvements with In-Memory technologies.</span></span>

<span data-ttu-id="cf95c-109">Aşağıda, bellek içi OLTP performansı toosignificantly nasıl Yardım iki örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="cf95c-109">Here are two examples of how In-Memory OLTP helped toosignificantly improve performance:</span></span>

- <span data-ttu-id="cf95c-110">Bellek içi OLTP kullanarak [çekirdek işletme çözümleri % 70 Dtu'lar arttırırken, iş yükü mümkün toodouble olan](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span><span class="sxs-lookup"><span data-stu-id="cf95c-110">By using In-Memory OLTP, [Quorum Business Solutions was able toodouble their workload while improving DTUs by 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span></span>
    - <span data-ttu-id="cf95c-111">DTU anlamına gelir *veritabanı işleme birimi*, ve kaynak tüketimi mesurement içerir.</span><span class="sxs-lookup"><span data-stu-id="cf95c-111">DTU means *database throughput unit*, and it includes a mesurement of resource consumption.</span></span>
- <span data-ttu-id="cf95c-112">Merhaba aşağıdaki videoda gösteren bir örnek iş yükü kaynak tüketimi önemli geliştirme: [Azure SQL veritabanı Video, bellek içi OLTP](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span><span class="sxs-lookup"><span data-stu-id="cf95c-112">hello following video demonstrates significant improvement in resource consumption with a sample workload: [In-Memory OLTP in Azure SQL Database Video](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span></span>
    - <span data-ttu-id="cf95c-113">Merhaba blog gönderisi daha fazla ayrıntı için bkz: [bellek içi OLTP Azure SQL veritabanı Blog gönderisine içinde](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span><span class="sxs-lookup"><span data-stu-id="cf95c-113">For more details, see hello blog post: [In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span></span>

<span data-ttu-id="cf95c-114">Bellek içi teknolojileri hello Premium katmanı, Premium esnek havuzlarını veritabanları dahil olmak üzere tüm veritabanlarında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="cf95c-114">In-Memory technologies are available in all databases in hello Premium tier, including databases in Premium elastic pools.</span></span>

<span data-ttu-id="cf95c-115">Merhaba aşağıdaki videoda Azure SQL veritabanında bellek içi teknolojileriyle olası performans artışı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cf95c-115">hello following video explains potential performance gains with In-Memory technologies in Azure SQL Database.</span></span> <span data-ttu-id="cf95c-116">Her zaman gördüğünüz hello performans kazancı hello niteliği hello iş yükü ve veri erişimi deseni hello veritabanının dahil olmak üzere birçok faktöre bağlıdır unutmayın ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="cf95c-116">Remember that hello performance gain that you see always depends on many factors, including hello nature of hello workload and data, access pattern of hello database, and so on.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

<span data-ttu-id="cf95c-117">Azure SQL veritabanı bellek içi teknolojileri aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="cf95c-117">Azure SQL Database has hello following In-Memory technologies:</span></span>

- <span data-ttu-id="cf95c-118">*Bellek içi OLTP* verimliliğini artırır ve işlem için gecikme süresini azaltır.</span><span class="sxs-lookup"><span data-stu-id="cf95c-118">*In-Memory OLTP* increases throughput and reduces latency for transaction processing.</span></span> <span data-ttu-id="cf95c-119">Bellek içi OLTP yararlanan senaryolar şunlardır: yüksek verimlilik işlem ticaret ve oyun, veri alımı olayları veya önbelleğe alma, veri yükü ve geçici bir tablo ve tablo değişkeni senaryoları IOT cihazları gibi işleme.</span><span class="sxs-lookup"><span data-stu-id="cf95c-119">Scenarios that benefit from In-Memory OLTP are: high-throughput transaction processing such as trading and gaming, data ingestion from events or IoT devices, caching, data load, and temporary table and table variable scenarios.</span></span>
- <span data-ttu-id="cf95c-120">*Kümelenmiş columnstore dizinleri* (yukarı too10 saatleri), depolama ayak izini azaltmak ve raporlama ve analiz sorguları performansını.</span><span class="sxs-lookup"><span data-stu-id="cf95c-120">*Clustered columnstore indexes* reduce your storage footprint (up too10 times) and improve performance for reporting and analytics queries.</span></span> <span data-ttu-id="cf95c-121">Olgu tabloları ile veri reyonlarını toofit daha fazla veri veritabanınızda kullanmak ve performansı.</span><span class="sxs-lookup"><span data-stu-id="cf95c-121">You can use it with fact tables in your data marts toofit more data in your database and improve performance.</span></span> <span data-ttu-id="cf95c-122">Ayrıca, işletimsel veritabanı tooarchive geçmiş verileriyle kullanması ve too10 kez yukarı mümkün tooquery daha fazla veri olması.</span><span class="sxs-lookup"><span data-stu-id="cf95c-122">Also, you can use it with historical data in your operational database tooarchive and be able tooquery up too10 times more data.</span></span>
- <span data-ttu-id="cf95c-123">*Kümelenmemiş columnstore dizinleri* HTAP Yardım için toogain gerçek zamanlı Öngörüler işletmenize hello işletimsel sorgulama aracılığıyla doğrudan hello gerek toorun pahalı çıkartma, dönüştürme ve yükleme (ETL) işlem veritabanı ve bekleyin doldurulmuş hello veri ambarı toobe için.</span><span class="sxs-lookup"><span data-stu-id="cf95c-123">*Nonclustered columnstore indexes* for HTAP help you toogain real-time insights into your business through querying hello operational database directly, without hello need toorun an expensive extract, transform, and load (ETL) process and wait for hello data warehouse toobe populated.</span></span> <span data-ttu-id="cf95c-124">Kümelenmemiş columnstore dizinleri hello OLTP veritabanlarında hello işlem iş yükü hello etkisini azaltırken analitik sorguları çok hızlı yürütülmesi izin verin.</span><span class="sxs-lookup"><span data-stu-id="cf95c-124">Nonclustered columnstore indexes allow very fast execution of analytics queries on hello OLTP database, while reducing hello impact on hello operational workload.</span></span>
- <span data-ttu-id="cf95c-125">Ayrıca, bir columnstore dizini olan bellek için iyileştirilmiş tablo hello birleşimi olabilir.</span><span class="sxs-lookup"><span data-stu-id="cf95c-125">You can also have hello combination of a memory-optimized table with a columnstore index.</span></span> <span data-ttu-id="cf95c-126">Bu birleşim tooperform çok hızlı hareket işleme, sağlar ve çok*eşzamanlı olarak* çalışma analytics sorgular çok hızlı bir şekilde hello üzerinde aynı veri.</span><span class="sxs-lookup"><span data-stu-id="cf95c-126">This combination enables you tooperform very fast transaction processing, and too*concurrently* run analytics queries very quickly on hello same data.</span></span>

<span data-ttu-id="cf95c-127">Merhaba SQL Server ürün parçası 2012 ve 2014, bu yana columnstore dizinleri ve bellek içi OLTP sırasıyla olmuştur.</span><span class="sxs-lookup"><span data-stu-id="cf95c-127">Both columnstore indexes and In-Memory OLTP have been part of hello SQL Server product since 2012 and 2014, respectively.</span></span> <span data-ttu-id="cf95c-128">Azure SQL Database ve SQL Server paylaşmak hello bellek içi teknolojileri aynı uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="cf95c-128">Azure SQL Database and SQL Server share hello same implementation of In-Memory technologies.</span></span> <span data-ttu-id="cf95c-129">SQL Server'da yayımlanmadan önce ileride, bu teknolojiler için yeni özellikler Azure SQL veritabanı'nda ilk olarak yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="cf95c-129">Going forward, new capabilities for these technologies are released in Azure SQL Database first, before they are released in SQL Server.</span></span>

<span data-ttu-id="cf95c-130">Bu konuda, belirli tooAzure SQL veritabanı olan bellek içi OLTP ve columnstore dizinleri yönlerini açıklar ve ayrıca örnekleri içerir:</span><span class="sxs-lookup"><span data-stu-id="cf95c-130">This topic describes aspects of In-Memory OLTP and columnstore indexes that are specific tooAzure SQL Database and also includes samples:</span></span>
- <span data-ttu-id="cf95c-131">Bu teknolojiler hello etkisini depolama ve veri boyutu sınırları görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="cf95c-131">You'll see hello impact of these technologies on storage and data size limits.</span></span>
- <span data-ttu-id="cf95c-132">Bu teknolojiler hello farklı fiyatlandırma katmanlarına arasında kullanan veritabanları hareketini toomanage hello nasıl görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="cf95c-132">You'll see how toomanage hello movement of databases that use these technologies between hello different pricing tiers.</span></span>
- <span data-ttu-id="cf95c-133">Azure SQL veritabanında columnstore dizinleri yanı sıra, bellek içi OLTP hello kullanımını gösteren iki örnek görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="cf95c-133">You'll see two samples that illustrate hello use of In-Memory OLTP, as well as columnstore indexes in Azure SQL Database.</span></span>

<span data-ttu-id="cf95c-134">Daha fazla bilgi için kaynaklar aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="cf95c-134">See hello following resources for more information.</span></span>

<span data-ttu-id="cf95c-135">Merhaba teknolojileri hakkında ayrıntılı bilgi:</span><span class="sxs-lookup"><span data-stu-id="cf95c-135">In-depth information about hello technologies:</span></span>

- <span data-ttu-id="cf95c-136">[Bellek içi OLTP genel bakış ve kullanım senaryoları](https://msdn.microsoft.com/library/mt774593.aspx) (başvuruları toocustomer örnek olay incelemeleri ve bilgi tooget başlatılan içerir)</span><span class="sxs-lookup"><span data-stu-id="cf95c-136">[In-Memory OLTP Overview and Usage Scenarios](https://msdn.microsoft.com/library/mt774593.aspx) (includes references toocustomer case studies and information tooget started)</span></span>
- [<span data-ttu-id="cf95c-137">Bellek içi OLTP için belgeler</span><span class="sxs-lookup"><span data-stu-id="cf95c-137">Documentation for In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
- [<span data-ttu-id="cf95c-138">Columnstore dizinleri Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="cf95c-138">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
- <span data-ttu-id="cf95c-139">Karma işlem / (HTAP), olarak da bilinen analitik işleme [işletimsel gerçek zamanlı analiz](https://msdn.microsoft.com/library/dn817827.aspx)</span><span class="sxs-lookup"><span data-stu-id="cf95c-139">Hybrid transactional/analytical processing (HTAP), also known as [real-time operational analytics](https://msdn.microsoft.com/library/dn817827.aspx)</span></span>

<span data-ttu-id="cf95c-140">Bellek içi OLTP hızlı öncü: [hızlı başlangıç 1: bellek içi OLTP teknolojileri daha hızlı T-SQL performansı](http://msdn.microsoft.com/library/mt694156.aspx) (başka bir makale toohelp başlamanıza)</span><span class="sxs-lookup"><span data-stu-id="cf95c-140">A quick primer on In-Memory OLTP: [Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance](http://msdn.microsoft.com/library/mt694156.aspx) (another article toohelp you get started)</span></span>

<span data-ttu-id="cf95c-141">Merhaba teknolojileri hakkında ayrıntılı videolar:</span><span class="sxs-lookup"><span data-stu-id="cf95c-141">In-depth videos about hello technologies:</span></span>

- <span data-ttu-id="cf95c-142">[Azure SQL veritabanında bellek içi OLTP](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (performans gösterimini içeren avantaj ve tooreproduce bu sonuçları kendinize adımları)</span><span class="sxs-lookup"><span data-stu-id="cf95c-142">[In-Memory OLTP in Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (which contains a demo of performance benefits and steps tooreproduce these results yourself)</span></span>
- [<span data-ttu-id="cf95c-143">Bellek içi OLTP videolar: Nedir ve ne zaman/nasıl toouse,</span><span class="sxs-lookup"><span data-stu-id="cf95c-143">In-Memory OLTP Videos: What it is and When/How toouse it</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- [<span data-ttu-id="cf95c-144">Columnstore dizini: Bellek içi Analytics videoların 2016 göz atın.</span><span class="sxs-lookup"><span data-stu-id="cf95c-144">Columnstore Index: In-Memory Analytics Videos from Ignite 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)

## <a name="storage-and-data-size"></a><span data-ttu-id="cf95c-145">Depolama ve veri boyutu</span><span class="sxs-lookup"><span data-stu-id="cf95c-145">Storage and data size</span></span>

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a><span data-ttu-id="cf95c-146">Veri boyutu ve depolama cap bellek içi OLTP için</span><span class="sxs-lookup"><span data-stu-id="cf95c-146">Data size and storage cap for In-Memory OLTP</span></span>

<span data-ttu-id="cf95c-147">Bellek içi OLTP kullanıcı verilerini depolamak için kullanılan bellek için iyileştirilmiş tablolar içerir.</span><span class="sxs-lookup"><span data-stu-id="cf95c-147">In-Memory OLTP includes memory-optimized tables, which are used for storing user data.</span></span> <span data-ttu-id="cf95c-148">Bu tablolar bellekte gerekli toofit değildir.</span><span class="sxs-lookup"><span data-stu-id="cf95c-148">These tables are required toofit in memory.</span></span> <span data-ttu-id="cf95c-149">Merhaba SQL veritabanı hizmetinin bellekte doğrudan yönetmek için biz kullanıcı verileri için bir kota hello kavramı vardır.</span><span class="sxs-lookup"><span data-stu-id="cf95c-149">Because you manage memory directly in hello SQL Database service, we have hello  concept of a quota for user data.</span></span> <span data-ttu-id="cf95c-150">Başvurulan tooas bu fikirdir *bellek içi OLTP depolama*.</span><span class="sxs-lookup"><span data-stu-id="cf95c-150">This idea is referred tooas *In-Memory OLTP storage*.</span></span>

<span data-ttu-id="cf95c-151">Belirli bir miktarda bellek içi OLTP depolama fiyatlandırma katmanı ve fiyatlandırma katmanı her esnek havuz her desteklenen tek başına veritabanı içerir.</span><span class="sxs-lookup"><span data-stu-id="cf95c-151">Each supported standalone database pricing tier and each elastic pool pricing tier includes a certain amount of In-Memory OLTP storage.</span></span> <span data-ttu-id="cf95c-152">Yazma Hello anda, depolama gigabayt her 125 veritabanı işlem birimleri (Dtu'lar) veya esnek veritabanı işlem birimleri (Edtu'lar) alın.</span><span class="sxs-lookup"><span data-stu-id="cf95c-152">At hello time of writing, you get a gigabyte of storage for every 125 database transaction units (DTUs) or elastic database transaction units (eDTUs).</span></span>

<span data-ttu-id="cf95c-153">Merhaba [SQL Database hizmet katmanlarına](sql-database-service-tiers.md) makale her desteklenen tek başına veritabanı ve fiyatlandırma katmanı esnek havuz için kullanılabilir olan hello bellek içi OLTP depolama hello resmi listesi içeriyor.</span><span class="sxs-lookup"><span data-stu-id="cf95c-153">hello [SQL Database service tiers](sql-database-service-tiers.md) article has hello official list of hello In-Memory OLTP storage that is available for each supported standalone database and elastic pool pricing tier.</span></span>

<span data-ttu-id="cf95c-154">öğe sayısını, bellek içi OLTP depolama cap doğru aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="cf95c-154">hello following items count toward your In-Memory OLTP storage cap:</span></span>

- <span data-ttu-id="cf95c-155">Bellek için iyileştirilmiş tablolar ve Tablo değişkenlerinin etkin kullanıcı veri satır.</span><span class="sxs-lookup"><span data-stu-id="cf95c-155">Active user data rows in memory-optimized tables and table variables.</span></span> <span data-ttu-id="cf95c-156">Eski satır sürümlerini doğru hello cap sayılmaz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="cf95c-156">Note that old row versions don't count toward hello cap.</span></span>
- <span data-ttu-id="cf95c-157">Bellek için iyileştirilmiş tablolardaki dizinler.</span><span class="sxs-lookup"><span data-stu-id="cf95c-157">Indexes on memory-optimized tables.</span></span>
- <span data-ttu-id="cf95c-158">ALTER TABLE işlemlerin işlemsel yükünü.</span><span class="sxs-lookup"><span data-stu-id="cf95c-158">Operational overhead of ALTER TABLE operations.</span></span>

<span data-ttu-id="cf95c-159">Merhaba cap isabet, kota hata iletisi ve artık mümkün tooinsert veya güncelleştirme veri değil.</span><span class="sxs-lookup"><span data-stu-id="cf95c-159">If you hit hello cap, you receive an out-of-quota error, and you are no longer able tooinsert or update data.</span></span> <span data-ttu-id="cf95c-160">toomitigate bu hata, verileri silmek veya fiyatlandırma katmanı hello veritabanı veya havuzu hello artırın.</span><span class="sxs-lookup"><span data-stu-id="cf95c-160">toomitigate this error, delete data or increase hello pricing tier of hello database or pool.</span></span>

<span data-ttu-id="cf95c-161">Bellek içi OLTP depolama alanı kullanımı izleme ve neredeyse hello cap isabet olduğunda uyarıları yapılandırma hakkında daha fazla bilgi için bkz [monitör bellek içi depolama](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="cf95c-161">For details about monitoring In-Memory OLTP storage utilization and configuring alerts when you almost hit hello cap, see [Monitor In-Memory storage](sql-database-in-memory-oltp-monitoring.md).</span></span>

#### <a name="about-elastic-pools"></a><span data-ttu-id="cf95c-162">Esnek havuzları hakkında</span><span class="sxs-lookup"><span data-stu-id="cf95c-162">About elastic pools</span></span>

<span data-ttu-id="cf95c-163">Esnek havuzları ile bellek içi OLTP depolama hello hello havuzdaki tüm veritabanları arasında paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="cf95c-163">With elastic pools, hello In-Memory OLTP storage is shared across all databases in hello pool.</span></span> <span data-ttu-id="cf95c-164">Bu nedenle, bir veritabanında hello kullanım büyük olasılıkla diğer veritabanlarına etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="cf95c-164">Therefore, hello usage in one database can potentially affect other databases.</span></span> <span data-ttu-id="cf95c-165">Bu iki Azaltıcı Etkenler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="cf95c-165">Two mitigations for this are:</span></span>

- <span data-ttu-id="cf95c-166">Bir Max-hello havuzu bir bütün olarak için hello eDTU sayısı daha düşük olan eDTU veritabanları için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cf95c-166">Configure a Max-eDTU for databases that is lower than hello eDTU count for hello pool as a whole.</span></span> <span data-ttu-id="cf95c-167">Bu maksimum hello havuzundaki toohello eDTU sayısı karşılık gelen toohello boyutu herhangi bir veritabanında hello bellek içi OLTP depolama alanı kullanımı caps.</span><span class="sxs-lookup"><span data-stu-id="cf95c-167">This maximum caps hello In-Memory OLTP storage utilization, in any database in hello pool, toohello size that corresponds toohello eDTU count.</span></span>
- <span data-ttu-id="cf95c-168">0'dan büyük bir Min-eDTU yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cf95c-168">Configure a Min-eDTU that is greater than 0.</span></span> <span data-ttu-id="cf95c-169">Minimum bırakıldığına hello havuzundaki her veritabanı toohello karşılık gelen kullanılabilir bellek içi OLTP depolama hello miktarına sahip en az eDTU yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="cf95c-169">This minimum guarantees that each database in hello pool has hello amount of available In-Memory OLTP storage that corresponds toohello configured Min-eDTU.</span></span>

### <a name="data-size-and-storage-for-columnstore-indexes"></a><span data-ttu-id="cf95c-170">Veri boyutu ve columnstore dizinleri için depolama</span><span class="sxs-lookup"><span data-stu-id="cf95c-170">Data size and storage for columnstore indexes</span></span>

<span data-ttu-id="cf95c-171">Columnstore dizinleri bellekte gerekli toofit değil.</span><span class="sxs-lookup"><span data-stu-id="cf95c-171">Columnstore indexes aren't required toofit in memory.</span></span> <span data-ttu-id="cf95c-172">Merhaba dizinleri hello boyutu CAP hello belgelenen hello maksimum genel veritabanı boyutu, yalnızca bu nedenle, hello [SQL Database hizmet katmanlarına](sql-database-service-tiers.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="cf95c-172">Therefore, hello only cap on hello size of hello indexes is hello maximum overall database size, which is documented in hello [SQL Database service tiers](sql-database-service-tiers.md) article.</span></span>

<span data-ttu-id="cf95c-173">Kümelenmiş columnstore dizinleri kullandığınızda, sütunlu sıkıştırma hello temel tablo depolaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cf95c-173">When you use clustered columnstore indexes, columnar compression is used for hello base table storage.</span></span> <span data-ttu-id="cf95c-174">Bu sıkıştırma hello depolama ayak izini hello veritabanında daha fazla veri sığabilecek anlamına gelir, verilerinizin kullanıcı önemli ölçüde azaltabilir.</span><span class="sxs-lookup"><span data-stu-id="cf95c-174">This compression can significantly reduce hello storage footprint of your user data, which means that you can fit more data in hello database.</span></span> <span data-ttu-id="cf95c-175">Ve hello sıkıştırma daha fazla artırılmasını ile [sütunlu arşiv sıkıştırma](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span><span class="sxs-lookup"><span data-stu-id="cf95c-175">And hello compression can be further increased with [columnar archival compression](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span></span> <span data-ttu-id="cf95c-176">Merhaba veri hello yapısını Hello elde edebilirsiniz sıkıştırma bağlıdır, ancak 10 kez hello sıkıştırma seyrek değil.</span><span class="sxs-lookup"><span data-stu-id="cf95c-176">hello amount of compression that you can achieve depends on hello nature of hello data, but 10 times hello compression is not uncommon.</span></span>

<span data-ttu-id="cf95c-177">Örneğin, 1 terabayt (TB) boyut sınırı olan bir veritabanı varsa ve columnstore dizinleri kullanarak 10 kez hello sıkıştırma elde, kullanıcı verilerini 10 TB toplam hello veritabanında sığabilecek.</span><span class="sxs-lookup"><span data-stu-id="cf95c-177">For example, if you have a database with a maximum size of 1 terabyte (TB) and you achieve 10 times hello compression by using columnstore indexes, you can fit a total of 10 TB of user data in hello database.</span></span>

<span data-ttu-id="cf95c-178">Kümelenmemiş columnstore dizinleri kullandığınızda, hello temel tablo hala hello geleneksel rowstore biçiminde depolanır.</span><span class="sxs-lookup"><span data-stu-id="cf95c-178">When you use nonclustered columnstore indexes, hello base table is still stored in hello traditional rowstore format.</span></span> <span data-ttu-id="cf95c-179">Bu nedenle, hello depolama tasarrufları kümelenmiş columnstore dizinleriyle kadar büyük değil.</span><span class="sxs-lookup"><span data-stu-id="cf95c-179">Therefore, hello storage savings aren't as big as with clustered columnstore indexes.</span></span> <span data-ttu-id="cf95c-180">Ancak, bir tek columnstore dizini ile geleneksel kümelenmemiş dizin sayısı değiştiriyorsanız hello depolama ayak izini hello tablosu için genel bir tasarruf görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf95c-180">However, if you're replacing a number of traditional nonclustered indexes with a single columnstore index, you can still see an overall savings in hello storage footprint for hello table.</span></span>

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a><span data-ttu-id="cf95c-181">Fiyatlandırma katmanı arasındaki bellek içi teknolojileri kullanan veritabanlarını taşıma</span><span class="sxs-lookup"><span data-stu-id="cf95c-181">Moving databases that use In-Memory technologies between pricing tiers</span></span>

<span data-ttu-id="cf95c-182">Vardır hiçbir zaman uyumsuzlukları ya da diğer sorunlar tooa standart tooPremium gibi fiyatlandırma katmanı, daha yüksek yükselttiğinizde.</span><span class="sxs-lookup"><span data-stu-id="cf95c-182">There are never any incompatibilities or other problems when you upgrade tooa higher pricing tier, such as from Standard tooPremium.</span></span> <span data-ttu-id="cf95c-183">Merhaba kullanılabilir işlevler ve kaynakları yalnızca artırın.</span><span class="sxs-lookup"><span data-stu-id="cf95c-183">hello available functionality and resources only increase.</span></span>

<span data-ttu-id="cf95c-184">Ancak, eski sürüme düşürmeyi hello fiyatlandırma katmanı veritabanınızı olumsuz yönde etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="cf95c-184">But downgrading hello pricing tier can negatively impact your database.</span></span> <span data-ttu-id="cf95c-185">Veritabanı bellek içi OLTP nesneler içerdiğinde hello özellikle Premium tooStandard düşürmek olduğunda görünen veya temel etkisidir.</span><span class="sxs-lookup"><span data-stu-id="cf95c-185">hello impact is especially apparent when you downgrade from Premium tooStandard or Basic when your database contains In-Memory OLTP objects.</span></span> <span data-ttu-id="cf95c-186">(Bunların görünür kalmasını olsa bile) bellek için iyileştirilmiş tablolar ve columnstore dizinleri hello indirgeme sonra kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="cf95c-186">Memory-optimized tables, and columnstore indexes, are unavailable after hello downgrade (even if they remain visible).</span></span> <span data-ttu-id="cf95c-187">Merhaba fiyatlandırma katmanı, bir esnek havuzun veya bir veritabanı bellek içi teknolojilerle birlikte, standart veya temel esnek havuz taşıma hello düşürürken ilgili noktaların aynısı geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="cf95c-187">hello same considerations apply when you're lowering hello pricing tier of an elastic pool, or moving a database with In-Memory technologies, into a Standard or Basic elastic pool.</span></span>

### <a name="in-memory-oltp"></a><span data-ttu-id="cf95c-188">Bellek içi OLTP</span><span class="sxs-lookup"><span data-stu-id="cf95c-188">In-Memory OLTP</span></span>

<span data-ttu-id="cf95c-189">*TooBasic/standart eski sürüme düşürmeyi*: bellek içi OLTP hello standart veya temel katmanı veritabanlarında desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="cf95c-189">*Downgrading tooBasic/Standard*: In-Memory OLTP isn't supported in databases in hello Standard or Basic tier.</span></span> <span data-ttu-id="cf95c-190">Ayrıca, olası toomove herhangi bellek içi OLTP nesneleri toohello standart veya temel katmanı olan bir veritabanında değil.</span><span class="sxs-lookup"><span data-stu-id="cf95c-190">In addition, it isn't possible toomove a database that has any In-Memory OLTP objects toohello Standard or Basic tier.</span></span>

<span data-ttu-id="cf95c-191">Merhaba veritabanı tooStandard/temel düşürmek önce tüm bellek için iyileştirilmiş tablolar ve tablo türleri yanı sıra, tüm yerel koda derlenmiş T-SQL modülleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="cf95c-191">Before you downgrade hello database tooStandard/Basic, remove all memory-optimized tables and table types, as well as all natively compiled T-SQL modules.</span></span>

<span data-ttu-id="cf95c-192">Verilen bir veritabanı bellek içi OLTP destekleyip desteklemediğini programlı şekilde toounderstand yoktur.</span><span class="sxs-lookup"><span data-stu-id="cf95c-192">There is a programmatic way toounderstand whether a given database supports In-Memory OLTP.</span></span> <span data-ttu-id="cf95c-193">Transact-SQL sorgusu aşağıdaki hello çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cf95c-193">You can execute hello following Transact-SQL query:</span></span>

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

<span data-ttu-id="cf95c-194">Merhaba sorgu döndürürse **1**, bellek içi OLTP bu veritabanında desteklenir.</span><span class="sxs-lookup"><span data-stu-id="cf95c-194">If hello query returns **1**, In-Memory OLTP is supported in this database.</span></span>


<span data-ttu-id="cf95c-195">*Tooa alt Premium katmanı eski sürüme düşürmeyi*: bellek için iyileştirilmiş tablolardaki verileri fiyatlandırma katmanı hello veritabanının hello ile ilişkili olduğundan veya hello esnek Havuzda kullanılabilir hello bellek içi OLTP depolama içinde sığması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cf95c-195">*Downgrading tooa lower Premium tier*: Data in memory-optimized tables must fit within hello In-Memory OLTP storage that is associated with hello pricing tier of hello database or is available in hello elastic pool.</span></span> <span data-ttu-id="cf95c-196">Fiyatlandırma katmanı toolower hello deneyin veya hello veritabanını taşırsanız bir havuza, yeterli kullanılabilir bellek içi OLTP depolama sahip değil, hello işlemi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="cf95c-196">If you try toolower hello pricing tier or move hello database into a pool that doesn't have enough available In-Memory OLTP storage, hello operation fails.</span></span>

### <a name="columnstore-indexes"></a><span data-ttu-id="cf95c-197">Columnstore dizinleri</span><span class="sxs-lookup"><span data-stu-id="cf95c-197">Columnstore indexes</span></span>

<span data-ttu-id="cf95c-198">*TooBasic veya standart eski sürüme düşürmeyi*: Columnstore dizinleri yalnızca hello Premium fiyatlandırma katmanı ve değil desteklenir hello standart ya da Basic katmanları.</span><span class="sxs-lookup"><span data-stu-id="cf95c-198">*Downgrading tooBasic or Standard*: Columnstore indexes are supported only on hello Premium pricing tier, and not on hello Standard or Basic tiers.</span></span> <span data-ttu-id="cf95c-199">Veritabanı tooStandard veya Basic düşürmek, columnstore dizini kullanılamaz duruma gelir.</span><span class="sxs-lookup"><span data-stu-id="cf95c-199">When you downgrade your database tooStandard or Basic, your columnstore index becomes unavailable.</span></span> <span data-ttu-id="cf95c-200">columnstore dizini Hello sistem korur ancak hiçbir zaman hello dizin yararlanır.</span><span class="sxs-lookup"><span data-stu-id="cf95c-200">hello system maintains your columnstore index, but it never leverages hello index.</span></span> <span data-ttu-id="cf95c-201">Daha sonra geri tooPremium yükseltirseniz, columnstore dizini yeniden işlevden hemen hazır toobe ' dir.</span><span class="sxs-lookup"><span data-stu-id="cf95c-201">If you later upgrade back tooPremium, your columnstore index is immediately ready toobe leveraged again.</span></span>

<span data-ttu-id="cf95c-202">Varsa bir **kümelenmiş** columnstore dizini hello tüm tablo olur kullanılamaz katmanı indirgeme sonra.</span><span class="sxs-lookup"><span data-stu-id="cf95c-202">If you have a **clustered** columnstore index, hello whole table becomes unavailable after tier downgrade.</span></span> <span data-ttu-id="cf95c-203">Bu nedenle tüm bırakma öneririz *kümelenmiş* veritabanınızı hello Premium katmanı aşağıda düşürmek önce columnstore dizinini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cf95c-203">Therefore we recommend that you drop all *clustered* columnstore indexes before you downgrade your database below hello Premium tier.</span></span>

<span data-ttu-id="cf95c-204">*Tooa alt Premium katmanı eski sürüme düşürmeyi*: hello tüm veritabanını hello hello esnek havuzdaki kullanılabilir depolama alanı veya hello en büyük veritabanı boyutu için fiyatlandırma katmanı hello hedef içinde uyuyorsa bu indirgeme başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="cf95c-204">*Downgrading tooa lower Premium tier*: This downgrade succeeds if hello whole database fits within hello maximum database size for hello target pricing tier, or within hello available storage in hello elastic pool.</span></span> <span data-ttu-id="cf95c-205">Merhaba columnstore dizinlerinde öğesinden belirli üzerinde etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="cf95c-205">There is no specific impact from hello columnstore indexes.</span></span>


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-hello-in-memory-oltp-sample"></a><span data-ttu-id="cf95c-206">1. Merhaba bellek içi OLTP örneği yükleme</span><span class="sxs-lookup"><span data-stu-id="cf95c-206">1. Install hello In-Memory OLTP sample</span></span>

<span data-ttu-id="cf95c-207">Merhaba, birkaç tıklama ile Merhaba AdventureWorksLT örnek veritabanı oluşturmak [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cf95c-207">You can create hello AdventureWorksLT sample database with a few clicks in hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="cf95c-208">Ardından, hello bu bölümdeki adımları nasıl AdventureWorksLT veritabanınızı bellek içi OLTP nesnelerle zenginleştirmek ve performans avantajı göstermek açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cf95c-208">Then, hello steps in this section explain how you can enrich your AdventureWorksLT database with In-Memory OLTP objects and demonstrate performance benefits.</span></span>

<span data-ttu-id="cf95c-209">Daha fazla simplistic, ancak daha görsel olarak çekici performans gösteri için bellek içi OLTP için bkz:</span><span class="sxs-lookup"><span data-stu-id="cf95c-209">For a more simplistic, but more visually appealing performance demo for In-Memory OLTP, see:</span></span>

- <span data-ttu-id="cf95c-210">Yayın: [içinde-bellek-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span><span class="sxs-lookup"><span data-stu-id="cf95c-210">Release: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span></span>
- <span data-ttu-id="cf95c-211">Kaynak kodu: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span><span class="sxs-lookup"><span data-stu-id="cf95c-211">Source code: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span></span>

#### <a name="installation-steps"></a><span data-ttu-id="cf95c-212">Yükleme adımları</span><span class="sxs-lookup"><span data-stu-id="cf95c-212">Installation steps</span></span>

1. <span data-ttu-id="cf95c-213">Merhaba, [Azure portal](https://portal.azure.com/), bir sunucu üzerinde bir Premium veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cf95c-213">In hello [Azure portal](https://portal.azure.com/), create a Premium database on a server.</span></span> <span data-ttu-id="cf95c-214">Set hello **kaynak** toohello AdventureWorksLT örnek veritabanı.</span><span class="sxs-lookup"><span data-stu-id="cf95c-214">Set hello **Source** toohello AdventureWorksLT sample database.</span></span> <span data-ttu-id="cf95c-215">Ayrıntılı yönergeler için bkz: [ilk Azure SQL veritabanınızı oluşturma](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cf95c-215">For detailed instructions, see [Create your first Azure SQL database](sql-database-get-started-portal.md).</span></span>

2. <span data-ttu-id="cf95c-216">SQL Server Management Studio ile toohello veritabanı bağlantı [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf95c-216">Connect toohello database with SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

3. <span data-ttu-id="cf95c-217">Kopya hello [bellek içi OLTP Transact-SQL betiği](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour Pano.</span><span class="sxs-lookup"><span data-stu-id="cf95c-217">Copy hello [In-Memory OLTP Transact-SQL script](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour clipboard.</span></span> <span data-ttu-id="cf95c-218">Merhaba T-SQL betiği hello gerekli bellek içi nesneleri 1. adımda oluşturduğunuz hello AdventureWorksLT örnek veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cf95c-218">hello T-SQL script creates hello necessary In-Memory objects in hello AdventureWorksLT sample database that you created in step 1.</span></span>

4. <span data-ttu-id="cf95c-219">SSMS Hello T-SQL betiğini yapıştırın ve hello betiğini yürütün.</span><span class="sxs-lookup"><span data-stu-id="cf95c-219">Paste hello T-SQL script into SSMS, and then execute hello script.</span></span> <span data-ttu-id="cf95c-220">Merhaba `MEMORY_OPTIMIZED = ON` yan tümcesi CREATE TABLE deyimleri önemli.</span><span class="sxs-lookup"><span data-stu-id="cf95c-220">hello `MEMORY_OPTIMIZED = ON` clause CREATE TABLE statements are crucial.</span></span> <span data-ttu-id="cf95c-221">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="cf95c-221">For example:</span></span>


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a><span data-ttu-id="cf95c-222">Hata 40536</span><span class="sxs-lookup"><span data-stu-id="cf95c-222">Error 40536</span></span>


<span data-ttu-id="cf95c-223">Merhaba T-SQL komut dosyasını çalıştırdığınızda 40536 hata alırsanız, bellek içi hello veritabanı destekleyip desteklemediğini T-SQL komut dosyası tooverify aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="cf95c-223">If you get error 40536 when you run hello T-SQL script, run hello following T-SQL script tooverify whether hello database supports In-Memory:</span></span>


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


<span data-ttu-id="cf95c-224">Sonucunu **0** , bellek içi desteklenmez, anlamına gelir ve **1** desteklenip desteklenmediğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="cf95c-224">A result of **0** means that In-Memory isn't supported, and **1** means that it is supported.</span></span> <span data-ttu-id="cf95c-225">toodiagnose hello sorun hello veritabanının hello Premium Hizmet katmanını olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="cf95c-225">toodiagnose hello problem, ensure that hello database is at hello Premium service tier.</span></span>


#### <a name="about-hello-created-memory-optimized-items"></a><span data-ttu-id="cf95c-226">Bellek için iyileştirilmiş öğeleri oluşturulan hello hakkında</span><span class="sxs-lookup"><span data-stu-id="cf95c-226">About hello created memory-optimized items</span></span>

<span data-ttu-id="cf95c-227">**Tablolar**: hello örnek bellek için iyileştirilmiş tablolar aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="cf95c-227">**Tables**: hello sample contains hello following memory-optimized tables:</span></span>

- <span data-ttu-id="cf95c-228">SalesLT.Product_inmem</span><span class="sxs-lookup"><span data-stu-id="cf95c-228">SalesLT.Product_inmem</span></span>
- <span data-ttu-id="cf95c-229">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="cf95c-229">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="cf95c-230">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="cf95c-230">SalesLT.SalesOrderDetail_inmem</span></span>
- <span data-ttu-id="cf95c-231">Demo.DemoSalesOrderHeaderSeed</span><span class="sxs-lookup"><span data-stu-id="cf95c-231">Demo.DemoSalesOrderHeaderSeed</span></span>
- <span data-ttu-id="cf95c-232">Demo.DemoSalesOrderDetailSeed</span><span class="sxs-lookup"><span data-stu-id="cf95c-232">Demo.DemoSalesOrderDetailSeed</span></span>


<span data-ttu-id="cf95c-233">Bellek için iyileştirilmiş tablolar hello aracılığıyla inceleyebilirsiniz **Object Explorer** SSMS içinde.</span><span class="sxs-lookup"><span data-stu-id="cf95c-233">You can inspect memory-optimized tables through hello **Object Explorer** in SSMS.</span></span> <span data-ttu-id="cf95c-234">Sağ **tabloları** > **filtre** > **filtre ayarları** > **bellek için iyileştirilmiş**.</span><span class="sxs-lookup"><span data-stu-id="cf95c-234">Right-click **Tables** > **Filter** > **Filter Settings** > **Is Memory Optimized**.</span></span> <span data-ttu-id="cf95c-235">Başlangıç değeri 1'e eşittir.</span><span class="sxs-lookup"><span data-stu-id="cf95c-235">hello value equals 1.</span></span>


<span data-ttu-id="cf95c-236">Veya gibi hello Katalog görünümleri sorgulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cf95c-236">Or you can query hello catalog views, such as:</span></span>


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


<span data-ttu-id="cf95c-237">**Saklı yordam yerel koda derlenmiş**: SalesLT.usp_InsertSalesOrder_inmem Katalog görünümü sorgu ile inceleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cf95c-237">**Natively compiled stored procedure**: You can inspect SalesLT.usp_InsertSalesOrder_inmem through a catalog view query:</span></span>


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-hello-sample-oltp-workload"></a><span data-ttu-id="cf95c-238">Merhaba örnek OLTP iş yükü çalıştırın</span><span class="sxs-lookup"><span data-stu-id="cf95c-238">Run hello sample OLTP workload</span></span>

<span data-ttu-id="cf95c-239">iki aşağıdaki hello arasındaki tek fark hello *saklı yordamlar* olan hello ilk yordam hello tabloları bellek için iyileştirilmiş sürümlerini kullanır, hello sırasında ikinci yordam hello normal disk üzerinde tabloları kullanır:</span><span class="sxs-lookup"><span data-stu-id="cf95c-239">hello only difference between hello following two *stored procedures* is that hello first procedure uses memory-optimized versions of hello tables, while hello second procedure uses hello regular on-disk tables:</span></span>

- <span data-ttu-id="cf95c-240">SalesLT**.** usp_InsertSalesOrder**_inmem**</span><span class="sxs-lookup"><span data-stu-id="cf95c-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span></span>
- <span data-ttu-id="cf95c-241">SalesLT**.** usp_InsertSalesOrder**_ondisk**</span><span class="sxs-lookup"><span data-stu-id="cf95c-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span></span>


<span data-ttu-id="cf95c-242">Bu bölümde, nasıl toouse hello kullanışlı olan gördüğünüz **ostress.exe** yardımcı programı tooexecute hello gerilimli düzeylerinde iki saklı yordamlar.</span><span class="sxs-lookup"><span data-stu-id="cf95c-242">In this section, you see how toouse hello handy **ostress.exe** utility tooexecute hello two stored procedures at stressful levels.</span></span> <span data-ttu-id="cf95c-243">Merhaba iki stres çalışır toofinish için gereken süreyi karşılaştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf95c-243">You can compare how long it takes for hello two stress runs toofinish.</span></span>


<span data-ttu-id="cf95c-244">Ostress.exe çalıştırdığınızda, her iki hello aşağıdaki için tasarlanmış parametre değerlerinin geçmesini öneririz:</span><span class="sxs-lookup"><span data-stu-id="cf95c-244">When you run ostress.exe, we recommend that you pass parameter values designed for both of hello following:</span></span>

- <span data-ttu-id="cf95c-245">Çok sayıda eşzamanlı bağlantı çalıştırmak kullanarak - n100.</span><span class="sxs-lookup"><span data-stu-id="cf95c-245">Run a large number of concurrent connections, by using -n100.</span></span>
- <span data-ttu-id="cf95c-246">Yüzlerce kez, her bağlantı döngü göre sahip kullanma - r500.</span><span class="sxs-lookup"><span data-stu-id="cf95c-246">Have each connection loop hundreds of times, by using -r500.</span></span>


<span data-ttu-id="cf95c-247">Bununla birlikte, toostart gibi - her şeyin çalıştığını n10 ve - r50 tooensure çok daha küçük değerlerle isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf95c-247">However, you might want toostart with much smaller values like -n10 and -r50 tooensure that everything is working.</span></span>


### <a name="script-for-ostressexe"></a><span data-ttu-id="cf95c-248">Ostress.exe için komut dosyası</span><span class="sxs-lookup"><span data-stu-id="cf95c-248">Script for ostress.exe</span></span>


<span data-ttu-id="cf95c-249">Bu bölümde bizim ostress.exe komut satırında katıştırılmış hello T-SQL komut dosyası görüntüler.</span><span class="sxs-lookup"><span data-stu-id="cf95c-249">This section displays hello T-SQL script that is embedded in our ostress.exe command line.</span></span> <span data-ttu-id="cf95c-250">Merhaba betik hello daha önce yüklediğiniz T-SQL komut dosyası tarafından oluşturulan öğeleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="cf95c-250">hello script uses items that were created by hello T-SQL script that you installed earlier.</span></span>


<span data-ttu-id="cf95c-251">Merhaba aşağıdaki komut dosyası bir örnek sipariş beş satır öğelerle bellek için iyileştirilmiş hello aşağıdaki ekler *tabloları*:</span><span class="sxs-lookup"><span data-stu-id="cf95c-251">hello following script inserts a sample sales order with five line items into hello following memory-optimized *tables*:</span></span>

- <span data-ttu-id="cf95c-252">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="cf95c-252">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="cf95c-253">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="cf95c-253">SalesLT.SalesOrderDetail_inmem</span></span>


```
DECLARE
    @i int = 0,
    @od SalesLT.SalesOrderDetailType_inmem,
    @SalesOrderID int,
    @DueDate datetime2 = sysdatetime(),
    @CustomerID int = rand() * 8000,
    @BillToAddressID int = rand() * 10000,
    @ShipToAddressID int = rand() * 10000;

INSERT INTO @od
    SELECT OrderQty, ProductID
    FROM Demo.DemoSalesOrderDetailSeed
    WHERE OrderID= cast((rand()*60) as int);

WHILE (@i < 20)
begin;
    EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT,
        @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od;
    SET @i = @i + 1;
end
```


<span data-ttu-id="cf95c-254">toomake hello *_ondisk* sürümü Merhaba ostress.exe için yukarıdaki T-SQL komut dosyası, her iki hello oluşumları değiştirirsiniz *_inmem* ile alt dize *_ondisk*.</span><span class="sxs-lookup"><span data-stu-id="cf95c-254">toomake hello *_ondisk* version of hello preceding T-SQL script for ostress.exe, you would replace both occurrences of hello *_inmem* substring with *_ondisk*.</span></span> <span data-ttu-id="cf95c-255">Bu değişiklik, tabloları ve saklı yordamlar hello adları etkiler.</span><span class="sxs-lookup"><span data-stu-id="cf95c-255">These replacements affect hello names of tables and stored procedures.</span></span>


### <a name="install-rml-utilities-and-ostress"></a><span data-ttu-id="cf95c-256">RML yardımcı programları ve ostress yükleyin</span><span class="sxs-lookup"><span data-stu-id="cf95c-256">Install RML utilities and ostress</span></span>


<span data-ttu-id="cf95c-257">İdeal olarak, Azure sanal makine (VM) toorun ostress.exe planlamanız.</span><span class="sxs-lookup"><span data-stu-id="cf95c-257">Ideally, you would plan toorun ostress.exe on an Azure virtual machine (VM).</span></span> <span data-ttu-id="cf95c-258">Oluşturacak bir [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) hello içinde AdventureWorksLT veritabanınızın bulunduğu aynı Azure coğrafi bölge.</span><span class="sxs-lookup"><span data-stu-id="cf95c-258">You would create an [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) in hello same Azure geographic region where your AdventureWorksLT database resides.</span></span> <span data-ttu-id="cf95c-259">Ancak bunun yerine dizüstü bilgisayarınızda ostress.exe çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf95c-259">But you can run ostress.exe on your laptop instead.</span></span>


<span data-ttu-id="cf95c-260">Merhaba VM veya ne olursa olsun, ana bilgisayar seçin, hello yeniden yürütme işaretleme dili (RML) yardımcı programlarını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="cf95c-260">On hello VM, or on whatever host you choose, install hello Replay Markup Language (RML) utilities.</span></span> <span data-ttu-id="cf95c-261">Merhaba yardımcı programları ostress.exe kapsar.</span><span class="sxs-lookup"><span data-stu-id="cf95c-261">hello utilities include ostress.exe.</span></span>

<span data-ttu-id="cf95c-262">Daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="cf95c-262">For more information, see:</span></span>
- <span data-ttu-id="cf95c-263">Merhaba ostress.exe tartışmada [örnek veritabanı bellek içi OLTP için](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf95c-263">hello ostress.exe discussion in [Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="cf95c-264">[Örnek veritabanı için bellek içi OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf95c-264">[Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="cf95c-265">Merhaba [ostress.exe yüklemek için blog](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf95c-265">hello [blog for installing ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span></span>



<!--
dn511655.aspx is for SQL 2014,
[Extensions tooAdventureWorks tooDemonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-hello-inmem-stress-workload-first"></a><span data-ttu-id="cf95c-266">Merhaba çalıştırmak *_inmem* ilk iş yükü stres</span><span class="sxs-lookup"><span data-stu-id="cf95c-266">Run hello *_inmem* stress workload first</span></span>


<span data-ttu-id="cf95c-267">Kullanabileceğiniz bir *RML Cmd komut istemi* penceresi toorun bizim ostress.exe komut satırı.</span><span class="sxs-lookup"><span data-stu-id="cf95c-267">You can use an *RML Cmd Prompt* window toorun our ostress.exe command line.</span></span> <span data-ttu-id="cf95c-268">Merhaba komut satırı parametreleri için ostress doğrudan:</span><span class="sxs-lookup"><span data-stu-id="cf95c-268">hello command-line parameters direct ostress to:</span></span>

- <span data-ttu-id="cf95c-269">100 bağlantılara eşzamanlı olarak çalıştırın (-n100).</span><span class="sxs-lookup"><span data-stu-id="cf95c-269">Run 100 connections concurrently (-n100).</span></span>
- <span data-ttu-id="cf95c-270">Her bağlantınız 50 kez Hello T-SQL betiği çalıştırın (-r50).</span><span class="sxs-lookup"><span data-stu-id="cf95c-270">Have each connection run hello T-SQL script 50 times (-r50).</span></span>


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


<span data-ttu-id="cf95c-271">ostress.exe komut satırı önceki toorun hello:</span><span class="sxs-lookup"><span data-stu-id="cf95c-271">toorun hello preceding ostress.exe command line:</span></span>


1. <span data-ttu-id="cf95c-272">Merhaba veritabanı veri içeriği tüm önceki çalışmalarını tarafından eklenen tüm hello veri SSMS, toodelete komutunda aşağıdaki hello çalıştırarak sıfırlama:</span><span class="sxs-lookup"><span data-stu-id="cf95c-272">Reset hello database data content by running hello following command in SSMS, toodelete all hello data that was inserted by any previous runs:</span></span>

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. <span data-ttu-id="cf95c-273">Ostress.exe komut satırı tooyour Pano önceki hello Hello metnini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="cf95c-273">Copy hello text of hello preceding ostress.exe command line tooyour clipboard.</span></span>

3. <span data-ttu-id="cf95c-274">Hello yerine `<placeholders>` hello parametreleri -S - U -P -d hello için gerçek değerleri düzeltin.</span><span class="sxs-lookup"><span data-stu-id="cf95c-274">Replace hello `<placeholders>` for hello parameters -S -U -P -d with hello correct real values.</span></span>

4. <span data-ttu-id="cf95c-275">Düzenlenen komut satırında bir RML Cmd penceresinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="cf95c-275">Run your edited command line in an RML Cmd window.</span></span>


#### <a name="result-is-a-duration"></a><span data-ttu-id="cf95c-276">Bir süre oluşur</span><span class="sxs-lookup"><span data-stu-id="cf95c-276">Result is a duration</span></span>


<span data-ttu-id="cf95c-277">Ostress.exe bitirdiğinde, kendi çıktı hello RML Cmd penceresinde son satır olarak çalışma süresini hello yazar.</span><span class="sxs-lookup"><span data-stu-id="cf95c-277">When ostress.exe finishes, it writes hello run duration as its final line of output in hello RML Cmd window.</span></span> <span data-ttu-id="cf95c-278">Örneğin, daha kısa bir test çalıştırması yaklaşık 1,5 dakika devam:</span><span class="sxs-lookup"><span data-stu-id="cf95c-278">For example, a shorter test run lasted about 1.5 minutes:</span></span>

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a><span data-ttu-id="cf95c-279">Sıfırlama, düzenlemek *_ondisk*, sonra yeniden çalıştırın</span><span class="sxs-lookup"><span data-stu-id="cf95c-279">Reset, edit for *_ondisk*, then rerun</span></span>


<span data-ttu-id="cf95c-280">Merhaba hello sonucundan sonra *_inmem* çalıştırmak, şu adımları hello için hello gerçekleştirmek *_ondisk* çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="cf95c-280">After you have hello result from hello *_inmem* run, perform hello following steps for hello *_ondisk* run:</span></span>


1. <span data-ttu-id="cf95c-281">Merhaba veritabanı çalıştırmak hello tarafından önceki eklenmiş tüm hello veri SSMS toodelete komutunda aşağıdaki hello çalıştırarak sıfırlama:</span><span class="sxs-lookup"><span data-stu-id="cf95c-281">Reset hello database by running hello following command in SSMS toodelete all hello data that was inserted by hello previous run:</span></span>
```
EXECUTE Demo.usp_DemoReset;
```

2. <span data-ttu-id="cf95c-282">Merhaba ostress.exe komut satırı tooreplace tüm Düzenle *_inmem* ile *_ondisk*.</span><span class="sxs-lookup"><span data-stu-id="cf95c-282">Edit hello ostress.exe command line tooreplace all *_inmem* with *_ondisk*.</span></span>

3. <span data-ttu-id="cf95c-283">Ostress.exe hello için ikinci kez yeniden çalıştırın ve hello süresi sonuç yakalayın.</span><span class="sxs-lookup"><span data-stu-id="cf95c-283">Rerun ostress.exe for hello second time, and capture hello duration result.</span></span>

4. <span data-ttu-id="cf95c-284">Yeniden (sorumlu bir şekilde ne test verilerinin büyük bir miktarını olabilir silme) hello veritabanı sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="cf95c-284">Again, reset hello database (for responsibly deleting what can be a large amount of test data).</span></span>


#### <a name="expected-comparison-results"></a><span data-ttu-id="cf95c-285">Beklenen Karşılaştırma sonuçları</span><span class="sxs-lookup"><span data-stu-id="cf95c-285">Expected comparison results</span></span>

<span data-ttu-id="cf95c-286">Bellek içi testlerimizde tarafından geliştirilmiş performans göstermiştir **dokuz kez** simplistic bu iş yükü için ostress ile bir Azure VM üzerinde çalışan hello aynı hello veritabanı olarak Azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="cf95c-286">Our In-Memory tests have shown that performance improved by **nine times** for this simplistic workload, with ostress running on an Azure VM in hello same Azure region as hello database.</span></span>

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-hello-in-memory-analytics-sample"></a><span data-ttu-id="cf95c-287">2. Merhaba bellek içi analizi örneği yükleme</span><span class="sxs-lookup"><span data-stu-id="cf95c-287">2. Install hello In-Memory Analytics sample</span></span>


<span data-ttu-id="cf95c-288">Bir columnstore dizini bir geleneksel b-ağacı dizini karşı kullanırken bu bölümde, hello GÇ ve istatistikleri sonuçlarını karşılaştırın.</span><span class="sxs-lookup"><span data-stu-id="cf95c-288">In this section, you compare hello IO and statistics results when you're using a columnstore index versus a traditional b-tree index.</span></span>


<span data-ttu-id="cf95c-289">Bir OLTP iş yükü için gerçek zamanlı analiz almak için genellikle en iyi toouse kümelenmemiş bir columnstore dizini olur.</span><span class="sxs-lookup"><span data-stu-id="cf95c-289">For real-time analytics on an OLTP workload, it's often best toouse a nonclustered columnstore index.</span></span> <span data-ttu-id="cf95c-290">Ayrıntılar için bkz [Columnstore dizinleri açıklanan](http://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf95c-290">For details, see [Columnstore Indexes Described](http://msdn.microsoft.com/library/gg492088.aspx).</span></span>



### <a name="prepare-hello-columnstore-analytics-test"></a><span data-ttu-id="cf95c-291">Merhaba columnstore analytics test hazırlama</span><span class="sxs-lookup"><span data-stu-id="cf95c-291">Prepare hello columnstore analytics test</span></span>


1. <span data-ttu-id="cf95c-292">Hello Azure portal toocreate hello örnek yeni bir AdventureWorksLT veritabanından kullanın.</span><span class="sxs-lookup"><span data-stu-id="cf95c-292">Use hello Azure portal toocreate a fresh AdventureWorksLT database from hello sample.</span></span>
 - <span data-ttu-id="cf95c-293">Bu tam ad kullanın.</span><span class="sxs-lookup"><span data-stu-id="cf95c-293">Use that exact name.</span></span>
 - <span data-ttu-id="cf95c-294">Tüm Premium Hizmet katmanını seçin.</span><span class="sxs-lookup"><span data-stu-id="cf95c-294">Choose any Premium service tier.</span></span>

2. <span data-ttu-id="cf95c-295">Kopya hello [sql_in memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour Pano.</span><span class="sxs-lookup"><span data-stu-id="cf95c-295">Copy hello [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour clipboard.</span></span>
 - <span data-ttu-id="cf95c-296">Merhaba T-SQL betiği hello gerekli bellek içi nesneleri 1. adımda oluşturduğunuz hello AdventureWorksLT örnek veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cf95c-296">hello T-SQL script creates hello necessary In-Memory objects in hello AdventureWorksLT sample database that you created in step 1.</span></span>
 - <span data-ttu-id="cf95c-297">Merhaba betiği hello Boyut tablosuna ve iki olgu tabloları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cf95c-297">hello script creates hello Dimension table and two fact tables.</span></span> <span data-ttu-id="cf95c-298">Merhaba olgu tabloları 3.5 milyon satır her doldurulur.</span><span class="sxs-lookup"><span data-stu-id="cf95c-298">hello fact tables are populated with 3.5 million rows each.</span></span>
 - <span data-ttu-id="cf95c-299">Merhaba betik toocomplete 15 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="cf95c-299">hello script might take 15 minutes toocomplete.</span></span>

3. <span data-ttu-id="cf95c-300">SSMS Hello T-SQL betiğini yapıştırın ve hello betiğini yürütün.</span><span class="sxs-lookup"><span data-stu-id="cf95c-300">Paste hello T-SQL script into SSMS, and then execute hello script.</span></span> <span data-ttu-id="cf95c-301">Merhaba **COLUMNSTORE** hello anahtar sözcük **CREATE INDEX** açıklamadır önemli olarak:</span><span class="sxs-lookup"><span data-stu-id="cf95c-301">hello **COLUMNSTORE** keyword in hello **CREATE INDEX** statement is crucial, as in:</span></span><br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. <span data-ttu-id="cf95c-302">AdventureWorksLT toocompatibility düzeyi 130 ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="cf95c-302">Set AdventureWorksLT toocompatibility level 130:</span></span><br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    <span data-ttu-id="cf95c-303">Düzey 130 doğrudan ilgili tooIn bellek özellikleri değil.</span><span class="sxs-lookup"><span data-stu-id="cf95c-303">Level 130 is not directly related tooIn-Memory features.</span></span> <span data-ttu-id="cf95c-304">Ancak düzeyi 130 genellikle 120'den daha hızlı sorgu performansı sağlar.</span><span class="sxs-lookup"><span data-stu-id="cf95c-304">But level 130 generally provides faster query performance than 120.</span></span>


#### <a name="key-tables-and-columnstore-indexes"></a><span data-ttu-id="cf95c-305">Anahtar tablolar ve columnstore dizinleri</span><span class="sxs-lookup"><span data-stu-id="cf95c-305">Key tables and columnstore indexes</span></span>


- <span data-ttu-id="cf95c-306">dbo. FactResellerSalesXL_CCI sıkıştırma hello en gelişmiş bir kümelenmiş columnstore dizini içeren bir tablo olduğundan *veri* düzeyi.</span><span class="sxs-lookup"><span data-stu-id="cf95c-306">dbo.FactResellerSalesXL_CCI is a table that has a clustered columnstore index, which has advanced compression at hello *data* level.</span></span>

- <span data-ttu-id="cf95c-307">dbo. FactResellerSalesXL_PageCompressed yalnızca hello sıkıştırılmış bir eşdeğer normal kümelenmiş dizin içeren bir tablo olduğundan *sayfa* düzeyi.</span><span class="sxs-lookup"><span data-stu-id="cf95c-307">dbo.FactResellerSalesXL_PageCompressed is a table that has an equivalent regular clustered index, which is compressed only at hello *page* level.</span></span>


#### <a name="key-queries-toocompare-hello-columnstore-index"></a><span data-ttu-id="cf95c-308">Anahtar sorguları toocompare hello columnstore dizini</span><span class="sxs-lookup"><span data-stu-id="cf95c-308">Key queries toocompare hello columnstore index</span></span>


<span data-ttu-id="cf95c-309">Vardır [çalıştırabileceğiniz birkaç T-SQL sorgu türleri](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee performans iyileştirmeleri.</span><span class="sxs-lookup"><span data-stu-id="cf95c-309">There are [several T-SQL query types that you can run](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee performance improvements.</span></span> <span data-ttu-id="cf95c-310">Adım 2'de hello T-SQL betiği, sorguları dikkat toothis çifti ücret ödersiniz.</span><span class="sxs-lookup"><span data-stu-id="cf95c-310">In step 2 in hello T-SQL script, pay attention toothis pair of queries.</span></span> <span data-ttu-id="cf95c-311">Bunlar yalnızca tek bir satırda farklılık gösterir:</span><span class="sxs-lookup"><span data-stu-id="cf95c-311">They differ only on one line:</span></span>


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


<span data-ttu-id="cf95c-312">Merhaba FactResellerSalesXL kümelenmiş columnstore dizini olan\_CCI tablo.</span><span class="sxs-lookup"><span data-stu-id="cf95c-312">A clustered columnstore index is in hello FactResellerSalesXL\_CCI table.</span></span>

<span data-ttu-id="cf95c-313">Merhaba aşağıdaki T-SQL komut dosyası Alıntısı istatistikleri GÇ ve her tablonun hello sorgunun süresi yazdırır.</span><span class="sxs-lookup"><span data-stu-id="cf95c-313">hello following T-SQL script excerpt prints statistics for IO and TIME for hello query of each table.</span></span>


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order toosee Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins hello Fact Table with dimension tables
-- Note this query will run on hello Page Compressed table, Note down hello time
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO

SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_PageCompressed a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO
SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO


-- This is hello same Prior query on a table with a clustered columnstore index CCI
-- hello comparison numbers are even more dramatic hello larger hello table is (this is an 11 million row table only)
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO
SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_CCI a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO

SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO
```

<span data-ttu-id="cf95c-314">Merhaba P2 fiyatlandırma katmanı ile bir veritabanında hello geleneksel dizin ile karşılaştırıldığında hello kümelenmiş columnstore dizini kullanarak bu sorgu için yaklaşık dokuz kez hello performans kazancı bekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf95c-314">In a database with hello P2 pricing tier, you can expect about nine times hello performance gain for this query by using hello clustered columnstore index compared with hello traditional index.</span></span> <span data-ttu-id="cf95c-315">P15 ile Merhaba columnstore dizini kullanılarak hakkında 57 kez hello performans kazancı bekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf95c-315">With P15, you can expect about 57 times hello performance gain by using hello columnstore index.</span></span>



## <a name="next-steps"></a><span data-ttu-id="cf95c-316">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cf95c-316">Next steps</span></span>

- [<span data-ttu-id="cf95c-317">1 Hızlı Başlangıç: Daha hızlı bir T-SQL performans için bellek içi OLTP teknolojileri</span><span class="sxs-lookup"><span data-stu-id="cf95c-317">Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance</span></span>](http://msdn.microsoft.com/library/mt694156.aspx)

- [<span data-ttu-id="cf95c-318">Mevcut Azure SQL uygulamada kullanmak bellek içi OLTP</span><span class="sxs-lookup"><span data-stu-id="cf95c-318">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

- <span data-ttu-id="cf95c-319">[İzleyici bellek içi OLTP depolama](sql-database-in-memory-oltp-monitoring.md) bellek içi OLTP için</span><span class="sxs-lookup"><span data-stu-id="cf95c-319">[Monitor In-Memory OLTP storage](sql-database-in-memory-oltp-monitoring.md) for In-Memory OLTP</span></span>


## <a name="additional-resources"></a><span data-ttu-id="cf95c-320">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="cf95c-320">Additional resources</span></span>

#### <a name="deeper-information"></a><span data-ttu-id="cf95c-321">Daha ayrıntılı bilgi</span><span class="sxs-lookup"><span data-stu-id="cf95c-321">Deeper information</span></span>

- [<span data-ttu-id="cf95c-322">Bellek içi OLTP SQL veritabanında ile % 70 tarafından DTU düşürürken çekirdek anahtar veritabanının iş yükü nasıl Katlar öğrenin</span><span class="sxs-lookup"><span data-stu-id="cf95c-322">Learn how Quorum doubles key database’s workload while lowering DTU by 70% with In-Memory OLTP in SQL Database</span></span>](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)

- [<span data-ttu-id="cf95c-323">Bellek içi OLTP de Azure SQL veritabanı Blog Gönderisi</span><span class="sxs-lookup"><span data-stu-id="cf95c-323">In-Memory OLTP in Azure SQL Database Blog Post</span></span>](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

- [<span data-ttu-id="cf95c-324">Bellek içi OLTP hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="cf95c-324">Learn about In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="cf95c-325">Columnstore dizinleri hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="cf95c-325">Learn about columnstore indexes</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)

- [<span data-ttu-id="cf95c-326">Gerçek zamanlı işletimsel analytics hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="cf95c-326">Learn about real-time operational analytics</span></span>](http://msdn.microsoft.com/library/dn817827.aspx)

- <span data-ttu-id="cf95c-327">Bkz: [yaygın iş yükü desenleri ve geçiş konuları](http://msdn.microsoft.com/library/dn673538.aspx) (burada bellek içi OLTP sık sağlar önemli performans artışları yükünün desenleri açıklayan)</span><span class="sxs-lookup"><span data-stu-id="cf95c-327">See [Common Workload Patterns and Migration Considerations](http://msdn.microsoft.com/library/dn673538.aspx) (which describes workload patterns where In-Memory OLTP commonly provides significant performance gains)</span></span>

#### <a name="application-design"></a><span data-ttu-id="cf95c-328">Uygulama tasarımı</span><span class="sxs-lookup"><span data-stu-id="cf95c-328">Application design</span></span>

- [<span data-ttu-id="cf95c-329">Bellek içi OLTP (bellek içi iyileştirme)</span><span class="sxs-lookup"><span data-stu-id="cf95c-329">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="cf95c-330">Mevcut Azure SQL uygulamada kullanmak bellek içi OLTP</span><span class="sxs-lookup"><span data-stu-id="cf95c-330">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a><span data-ttu-id="cf95c-331">Araçlar</span><span class="sxs-lookup"><span data-stu-id="cf95c-331">Tools</span></span>

- [<span data-ttu-id="cf95c-332">Azure portal</span><span class="sxs-lookup"><span data-stu-id="cf95c-332">Azure portal</span></span>](https://portal.azure.com/)

- [<span data-ttu-id="cf95c-333">SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="cf95c-333">SQL Server Management Studio (SSMS)</span></span>](https://msdn.microsoft.com/library/mt238290.aspx)

- [<span data-ttu-id="cf95c-334">SQL Server Veri Araçları (SSDT)</span><span class="sxs-lookup"><span data-stu-id="cf95c-334">SQL Server Data Tools (SSDT)</span></span>](http://msdn.microsoft.com/library/mt204009.aspx)
