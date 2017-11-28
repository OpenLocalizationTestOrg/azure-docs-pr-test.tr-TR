---
title: "Azure SQL veritabanı bellek içi teknolojileri | Microsoft Docs"
description: "Azure SQL veritabanı bellek içi teknolojileri analytics iş yükleri ve işlem performansını önemli ölçüde artırır. Bu teknolojilerden öğrenin."
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
ms.openlocfilehash: 4cb45551c486263f26947e5684d54b4f2ecc7410
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a><span data-ttu-id="c862d-104">SQL veritabanı'nda Bellek içi teknolojileri kullanılarak performansı en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="c862d-104">Optimize performance by using In-Memory technologies in SQL Database</span></span>

<span data-ttu-id="c862d-105">Azure SQL veritabanı'nda Bellek içi teknolojilerini kullanarak, performans iyileştirmeleri çeşitli iş yükleri ile elde edebilirsiniz: işlem (çevrimiçi işlem işleme (OLTP)), analytics (çevrimiçi analitik işlem (OLAP)) ve karma (karma işlem/analitik işleme (HTAP)).</span><span class="sxs-lookup"><span data-stu-id="c862d-105">By using In-Memory technologies in Azure SQL Database, you can achieve performance improvements with various workloads: transactional (online transactional processing (OLTP)), analytics (online analytical processing (OLAP)), and mixed (hybrid transaction/analytical processing (HTAP)).</span></span> <span data-ttu-id="c862d-106">Daha verimli sorgu ve işlem nedeniyle, bellek içi teknolojileri de maliyetini azaltmak için yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="c862d-106">Because of the more efficient query and transaction processing, In-Memory technologies also help you to reduce cost.</span></span> <span data-ttu-id="c862d-107">Genellikle performans artışı elde etmek için veritabanının fiyatlandırma katmanı yükseltme gerekmez.</span><span class="sxs-lookup"><span data-stu-id="c862d-107">You typically don't need to upgrade the pricing tier of the database to achieve performance gains.</span></span> <span data-ttu-id="c862d-108">Bazı durumlarda, hatta yazdıramayabilirsiniz yine de performans iyileştirmeleri bellek içi teknolojileriyle görüyorsanız sırasında fiyatlandırma katmanı azaltın.</span><span class="sxs-lookup"><span data-stu-id="c862d-108">In some cases, you might even be able reduce the pricing tier, while still seeing performance improvements with In-Memory technologies.</span></span>

<span data-ttu-id="c862d-109">Aşağıda, bellek içi OLTP performansı önemli ölçüde artırmak için nasıl Yardım iki örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="c862d-109">Here are two examples of how In-Memory OLTP helped to significantly improve performance:</span></span>

- <span data-ttu-id="c862d-110">Bellek içi OLTP kullanarak [çekirdek işletme çözümleri % 70 Dtu'lar arttırırken, iş yükü çift mümkün](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span><span class="sxs-lookup"><span data-stu-id="c862d-110">By using In-Memory OLTP, [Quorum Business Solutions was able to double their workload while improving DTUs by 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span></span>
    - <span data-ttu-id="c862d-111">DTU anlamına gelir *veritabanı işleme birimi*, ve kaynak tüketimi mesurement içerir.</span><span class="sxs-lookup"><span data-stu-id="c862d-111">DTU means *database throughput unit*, and it includes a mesurement of resource consumption.</span></span>
- <span data-ttu-id="c862d-112">Aşağıdaki videoda bir örnek iş yükü kaynak tüketimi önemli gelişme gösterilmektedir: [Azure SQL veritabanı Video, bellek içi OLTP](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span><span class="sxs-lookup"><span data-stu-id="c862d-112">The following video demonstrates significant improvement in resource consumption with a sample workload: [In-Memory OLTP in Azure SQL Database Video](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span></span>
    - <span data-ttu-id="c862d-113">Daha fazla ayrıntı için blog gönderisine bakın: [bellek içi OLTP Azure SQL veritabanı Blog gönderisine içinde](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span><span class="sxs-lookup"><span data-stu-id="c862d-113">For more details, see the blog post: [In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span></span>

<span data-ttu-id="c862d-114">Bellek içi teknolojileri Premium katmanındaki Premium esnek havuzlarını veritabanları dahil olmak üzere tüm veritabanlarında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c862d-114">In-Memory technologies are available in all databases in the Premium tier, including databases in Premium elastic pools.</span></span>

<span data-ttu-id="c862d-115">Aşağıdaki video Azure SQL veritabanında bellek içi teknolojileriyle olası performans artışı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c862d-115">The following video explains potential performance gains with In-Memory technologies in Azure SQL Database.</span></span> <span data-ttu-id="c862d-116">Her zaman gördüğünüz performans kazancı iş yükü ve verileri, veritabanı, erişim desenini yapısını dahil olmak üzere birçok faktöre bağlıdır unutmayın ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="c862d-116">Remember that the performance gain that you see always depends on many factors, including the nature of the workload and data, access pattern of the database, and so on.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

<span data-ttu-id="c862d-117">Azure SQL veritabanı bellek içi teknolojilerin sahiptir:</span><span class="sxs-lookup"><span data-stu-id="c862d-117">Azure SQL Database has the following In-Memory technologies:</span></span>

- <span data-ttu-id="c862d-118">*Bellek içi OLTP* verimliliğini artırır ve işlem için gecikme süresini azaltır.</span><span class="sxs-lookup"><span data-stu-id="c862d-118">*In-Memory OLTP* increases throughput and reduces latency for transaction processing.</span></span> <span data-ttu-id="c862d-119">Bellek içi OLTP yararlanan senaryolar şunlardır: yüksek verimlilik işlem ticaret ve oyun, veri alımı olayları veya önbelleğe alma, veri yükü ve geçici bir tablo ve tablo değişkeni senaryoları IOT cihazları gibi işleme.</span><span class="sxs-lookup"><span data-stu-id="c862d-119">Scenarios that benefit from In-Memory OLTP are: high-throughput transaction processing such as trading and gaming, data ingestion from events or IoT devices, caching, data load, and temporary table and table variable scenarios.</span></span>
- <span data-ttu-id="c862d-120">*Kümelenmiş columnstore dizinleri* (en fazla 10 kez), depolama ayak izini azaltmak ve raporlama ve analiz sorguları performansını.</span><span class="sxs-lookup"><span data-stu-id="c862d-120">*Clustered columnstore indexes* reduce your storage footprint (up to 10 times) and improve performance for reporting and analytics queries.</span></span> <span data-ttu-id="c862d-121">Bu olgu tabloları ile veri reyonlarını daha fazla veri veritabanınızda sığacak ve performansı artırmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c862d-121">You can use it with fact tables in your data marts to fit more data in your database and improve performance.</span></span> <span data-ttu-id="c862d-122">Ayrıca, bu geçmiş verileriyle işlemsel veritabanında arşivlemek ve en fazla 10 kez daha fazla veri sorgulayabilmesi için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c862d-122">Also, you can use it with historical data in your operational database to archive and be able to query up to 10 times more data.</span></span>
- <span data-ttu-id="c862d-123">*Kümelenmemiş columnstore dizinleri* HTAP yardımcı olmak için işletimsel veritabanının pahalı bir ayıklama çalıştırmaya gerek doğrudan sorgulama aracılığıyla işletmenizin gerçek zamanlı Öngörüler elde size dönüştürme ve yükleme (ETL) işlemi ve doldurulması veri ambarı için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="c862d-123">*Nonclustered columnstore indexes* for HTAP help you to gain real-time insights into your business through querying the operational database directly, without the need to run an expensive extract, transform, and load (ETL) process and wait for the data warehouse to be populated.</span></span> <span data-ttu-id="c862d-124">Kümelenmemiş columnstore dizinleri OLTP veritabanı üzerinde işlem iş yükü üzerindeki etkiyi azaltırken analitik sorguları çok hızlı yürütülmesi izin verin.</span><span class="sxs-lookup"><span data-stu-id="c862d-124">Nonclustered columnstore indexes allow very fast execution of analytics queries on the OLTP database, while reducing the impact on the operational workload.</span></span>
- <span data-ttu-id="c862d-125">Ayrıca, bir columnstore dizini olan bellek için iyileştirilmiş tablo birleşimi olabilir.</span><span class="sxs-lookup"><span data-stu-id="c862d-125">You can also have the combination of a memory-optimized table with a columnstore index.</span></span> <span data-ttu-id="c862d-126">Bu birleşim çok hızlı işlemler gerçekleştirmenizi sağlar ve *eşzamanlı olarak* analitik sorguları aynı verileri çok hızlı bir şekilde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c862d-126">This combination enables you to perform very fast transaction processing, and to *concurrently* run analytics queries very quickly on the same data.</span></span>

<span data-ttu-id="c862d-127">SQL Server ürün parçası 2012 ve 2014, bu yana columnstore dizinleri ve bellek içi OLTP sırasıyla olmuştur.</span><span class="sxs-lookup"><span data-stu-id="c862d-127">Both columnstore indexes and In-Memory OLTP have been part of the SQL Server product since 2012 and 2014, respectively.</span></span> <span data-ttu-id="c862d-128">Azure SQL Database ve SQL Server bellek içi teknolojilerin aynı uygulaması paylaşır.</span><span class="sxs-lookup"><span data-stu-id="c862d-128">Azure SQL Database and SQL Server share the same implementation of In-Memory technologies.</span></span> <span data-ttu-id="c862d-129">SQL Server'da yayımlanmadan önce ileride, bu teknolojiler için yeni özellikler Azure SQL veritabanı'nda ilk olarak yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c862d-129">Going forward, new capabilities for these technologies are released in Azure SQL Database first, before they are released in SQL Server.</span></span>

<span data-ttu-id="c862d-130">Bu konuda, Azure SQL veritabanına özel bellek içi OLTP ve columnstore dizinleri yönlerini açıklar ve ayrıca örnekleri içerir:</span><span class="sxs-lookup"><span data-stu-id="c862d-130">This topic describes aspects of In-Memory OLTP and columnstore indexes that are specific to Azure SQL Database and also includes samples:</span></span>
- <span data-ttu-id="c862d-131">Bu teknolojiler etkisini depolama ve veri boyutu sınırları görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c862d-131">You'll see the impact of these technologies on storage and data size limits.</span></span>
- <span data-ttu-id="c862d-132">Bu teknolojiler farklı fiyatlandırma katmanları arasında kullanan veritabanları hareketini yönetme görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c862d-132">You'll see how to manage the movement of databases that use these technologies between the different pricing tiers.</span></span>
- <span data-ttu-id="c862d-133">Azure SQL veritabanında columnstore dizinleri yanı sıra, bellek içi OLTP kullanımını gösteren iki örnek görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c862d-133">You'll see two samples that illustrate the use of In-Memory OLTP, as well as columnstore indexes in Azure SQL Database.</span></span>

<span data-ttu-id="c862d-134">Daha fazla bilgi için aşağıdaki kaynaklara bakın.</span><span class="sxs-lookup"><span data-stu-id="c862d-134">See the following resources for more information.</span></span>

<span data-ttu-id="c862d-135">Teknolojileri hakkında ayrıntılı bilgi:</span><span class="sxs-lookup"><span data-stu-id="c862d-135">In-depth information about the technologies:</span></span>

- <span data-ttu-id="c862d-136">[Bellek içi OLTP genel bakış ve kullanım senaryoları](https://msdn.microsoft.com/library/mt774593.aspx) (müşteri örnek olay incelemeleri ve başlamak için bilgi başvurular içerir)</span><span class="sxs-lookup"><span data-stu-id="c862d-136">[In-Memory OLTP Overview and Usage Scenarios](https://msdn.microsoft.com/library/mt774593.aspx) (includes references to customer case studies and information to get started)</span></span>
- [<span data-ttu-id="c862d-137">Bellek içi OLTP için belgeler</span><span class="sxs-lookup"><span data-stu-id="c862d-137">Documentation for In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
- [<span data-ttu-id="c862d-138">Columnstore dizinleri Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="c862d-138">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
- <span data-ttu-id="c862d-139">Karma işlem / (HTAP), olarak da bilinen analitik işleme [işletimsel gerçek zamanlı analiz](https://msdn.microsoft.com/library/dn817827.aspx)</span><span class="sxs-lookup"><span data-stu-id="c862d-139">Hybrid transactional/analytical processing (HTAP), also known as [real-time operational analytics](https://msdn.microsoft.com/library/dn817827.aspx)</span></span>

<span data-ttu-id="c862d-140">Bellek içi OLTP hızlı öncü: [hızlı başlangıç 1: bellek içi OLTP teknolojileri daha hızlı T-SQL performansı](http://msdn.microsoft.com/library/mt694156.aspx) (yardımcı olması için başka bir makaleye başlama)</span><span class="sxs-lookup"><span data-stu-id="c862d-140">A quick primer on In-Memory OLTP: [Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance](http://msdn.microsoft.com/library/mt694156.aspx) (another article to help you get started)</span></span>

<span data-ttu-id="c862d-141">Teknolojileri hakkında ayrıntılı videolar:</span><span class="sxs-lookup"><span data-stu-id="c862d-141">In-depth videos about the technologies:</span></span>

- <span data-ttu-id="c862d-142">[Azure SQL veritabanında bellek içi OLTP](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (performans avantajı ve bu sonuçları kendinize yeniden oluşturma adımları gösterimini içeren)</span><span class="sxs-lookup"><span data-stu-id="c862d-142">[In-Memory OLTP in Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (which contains a demo of performance benefits and steps to reproduce these results yourself)</span></span>
- [<span data-ttu-id="c862d-143">Bellek içi OLTP videolar: Nedir ve ne zaman/nasıl kullanmak için</span><span class="sxs-lookup"><span data-stu-id="c862d-143">In-Memory OLTP Videos: What it is and When/How to use it</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- [<span data-ttu-id="c862d-144">Columnstore dizini: Bellek içi Analytics videoların 2016 göz atın.</span><span class="sxs-lookup"><span data-stu-id="c862d-144">Columnstore Index: In-Memory Analytics Videos from Ignite 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)

## <a name="storage-and-data-size"></a><span data-ttu-id="c862d-145">Depolama ve veri boyutu</span><span class="sxs-lookup"><span data-stu-id="c862d-145">Storage and data size</span></span>

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a><span data-ttu-id="c862d-146">Veri boyutu ve depolama cap bellek içi OLTP için</span><span class="sxs-lookup"><span data-stu-id="c862d-146">Data size and storage cap for In-Memory OLTP</span></span>

<span data-ttu-id="c862d-147">Bellek içi OLTP kullanıcı verilerini depolamak için kullanılan bellek için iyileştirilmiş tablolar içerir.</span><span class="sxs-lookup"><span data-stu-id="c862d-147">In-Memory OLTP includes memory-optimized tables, which are used for storing user data.</span></span> <span data-ttu-id="c862d-148">Bu tablolar belleğe sığması için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c862d-148">These tables are required to fit in memory.</span></span> <span data-ttu-id="c862d-149">SQL veritabanı hizmetinin bellekte doğrudan yönetmek için biz kullanıcı verileri için bir kota kavramı vardır.</span><span class="sxs-lookup"><span data-stu-id="c862d-149">Because you manage memory directly in the SQL Database service, we have the  concept of a quota for user data.</span></span> <span data-ttu-id="c862d-150">Bu fikir olarak adlandırılır *bellek içi OLTP depolama*.</span><span class="sxs-lookup"><span data-stu-id="c862d-150">This idea is referred to as *In-Memory OLTP storage*.</span></span>

<span data-ttu-id="c862d-151">Belirli bir miktarda bellek içi OLTP depolama fiyatlandırma katmanı ve fiyatlandırma katmanı her esnek havuz her desteklenen tek başına veritabanı içerir.</span><span class="sxs-lookup"><span data-stu-id="c862d-151">Each supported standalone database pricing tier and each elastic pool pricing tier includes a certain amount of In-Memory OLTP storage.</span></span> <span data-ttu-id="c862d-152">Yazma zaman, her 125 veritabanı işlem birimleri (Dtu'lar) veya esnek veritabanı işlem birimleri (Edtu'lar) için depolama gigabayt alırsınız.</span><span class="sxs-lookup"><span data-stu-id="c862d-152">At the time of writing, you get a gigabyte of storage for every 125 database transaction units (DTUs) or elastic database transaction units (eDTUs).</span></span>

<span data-ttu-id="c862d-153">[SQL Database hizmet katmanlarına](sql-database-service-tiers.md) makale her desteklenen tek başına veritabanı ve fiyatlandırma katmanı esnek havuz için kullanılabilir olan bellek içi OLTP depolama resmi listesi vardır.</span><span class="sxs-lookup"><span data-stu-id="c862d-153">The [SQL Database service tiers](sql-database-service-tiers.md) article has the official list of the In-Memory OLTP storage that is available for each supported standalone database and elastic pool pricing tier.</span></span>

<span data-ttu-id="c862d-154">Aşağıdaki öğeler, bellek içi OLTP depolama cap doğru sayısı:</span><span class="sxs-lookup"><span data-stu-id="c862d-154">The following items count toward your In-Memory OLTP storage cap:</span></span>

- <span data-ttu-id="c862d-155">Bellek için iyileştirilmiş tablolar ve Tablo değişkenlerinin etkin kullanıcı veri satır.</span><span class="sxs-lookup"><span data-stu-id="c862d-155">Active user data rows in memory-optimized tables and table variables.</span></span> <span data-ttu-id="c862d-156">Eski satır sürümlerini doğru ucun sayılmaz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c862d-156">Note that old row versions don't count toward the cap.</span></span>
- <span data-ttu-id="c862d-157">Bellek için iyileştirilmiş tablolardaki dizinler.</span><span class="sxs-lookup"><span data-stu-id="c862d-157">Indexes on memory-optimized tables.</span></span>
- <span data-ttu-id="c862d-158">ALTER TABLE işlemlerin işlemsel yükünü.</span><span class="sxs-lookup"><span data-stu-id="c862d-158">Operational overhead of ALTER TABLE operations.</span></span>

<span data-ttu-id="c862d-159">Ucun isabet, kota hata iletisi ve artık ekleyemez veya verileri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="c862d-159">If you hit the cap, you receive an out-of-quota error, and you are no longer able to insert or update data.</span></span> <span data-ttu-id="c862d-160">Bu hata etkisini azaltmak için verileri silmek veya havuz veya veritabanı fiyatlandırma katmanı artırın.</span><span class="sxs-lookup"><span data-stu-id="c862d-160">To mitigate this error, delete data or increase the pricing tier of the database or pool.</span></span>

<span data-ttu-id="c862d-161">Bellek içi OLTP depolama alanı kullanımı izleme ve neredeyse ucun isabet olduğunda uyarıları yapılandırma hakkında daha fazla bilgi için bkz [monitör bellek içi depolama](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="c862d-161">For details about monitoring In-Memory OLTP storage utilization and configuring alerts when you almost hit the cap, see [Monitor In-Memory storage](sql-database-in-memory-oltp-monitoring.md).</span></span>

#### <a name="about-elastic-pools"></a><span data-ttu-id="c862d-162">Esnek havuzları hakkında</span><span class="sxs-lookup"><span data-stu-id="c862d-162">About elastic pools</span></span>

<span data-ttu-id="c862d-163">Esnek havuzları ile bellek içi OLTP depolama havuzundaki tüm veritabanları arasında paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="c862d-163">With elastic pools, the In-Memory OLTP storage is shared across all databases in the pool.</span></span> <span data-ttu-id="c862d-164">Bu nedenle, bir veritabanında kullanım büyük olasılıkla diğer veritabanlarına etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="c862d-164">Therefore, the usage in one database can potentially affect other databases.</span></span> <span data-ttu-id="c862d-165">Bu iki Azaltıcı Etkenler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c862d-165">Two mitigations for this are:</span></span>

- <span data-ttu-id="c862d-166">Bir en çok-bir bütün olarak havuz eDTU sayısı daha düşük olan eDTU veritabanları için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c862d-166">Configure a Max-eDTU for databases that is lower than the eDTU count for the pool as a whole.</span></span> <span data-ttu-id="c862d-167">Bu maksimum bellek içi OLTP depolama alanı kullanımı herhangi bir veritabanı için eDTU sayısı karşılık gelen bir boyut havuzunda caps.</span><span class="sxs-lookup"><span data-stu-id="c862d-167">This maximum caps the In-Memory OLTP storage utilization, in any database in the pool, to the size that corresponds to the eDTU count.</span></span>
- <span data-ttu-id="c862d-168">0'dan büyük bir Min-eDTU yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c862d-168">Configure a Min-eDTU that is greater than 0.</span></span> <span data-ttu-id="c862d-169">Bu en az havuzdaki her veritabanı için yapılandırılmış en az eDTU karşılık gelen kullanılabilir bellek içi OLTP depolama alanı miktarı olduğunu güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="c862d-169">This minimum guarantees that each database in the pool has the amount of available In-Memory OLTP storage that corresponds to the configured Min-eDTU.</span></span>

### <a name="data-size-and-storage-for-columnstore-indexes"></a><span data-ttu-id="c862d-170">Veri boyutu ve columnstore dizinleri için depolama</span><span class="sxs-lookup"><span data-stu-id="c862d-170">Data size and storage for columnstore indexes</span></span>

<span data-ttu-id="c862d-171">Columnstore dizinleri belleğe sığması için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="c862d-171">Columnstore indexes aren't required to fit in memory.</span></span> <span data-ttu-id="c862d-172">Bu nedenle, yalnızca dizinleri boyutuna belgelenen en fazla genel veritabanı boyutu sınırıdır [SQL Database hizmet katmanlarına](sql-database-service-tiers.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="c862d-172">Therefore, the only cap on the size of the indexes is the maximum overall database size, which is documented in the [SQL Database service tiers](sql-database-service-tiers.md) article.</span></span>

<span data-ttu-id="c862d-173">Kümelenmiş columnstore dizinleri kullandığınızda, sütunlu sıkıştırma temel tablo depolaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c862d-173">When you use clustered columnstore indexes, columnar compression is used for the base table storage.</span></span> <span data-ttu-id="c862d-174">Bu sıkıştırma depolama ayak izini veritabanında daha fazla veri sığabilecek anlamına gelir, verilerinizin kullanıcı önemli ölçüde azaltabilir.</span><span class="sxs-lookup"><span data-stu-id="c862d-174">This compression can significantly reduce the storage footprint of your user data, which means that you can fit more data in the database.</span></span> <span data-ttu-id="c862d-175">Sıkıştırma daha fazla ile artırılabilir [sütunlu arşiv sıkıştırma](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span><span class="sxs-lookup"><span data-stu-id="c862d-175">And the compression can be further increased with [columnar archival compression](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span></span> <span data-ttu-id="c862d-176">Elde edebilirsiniz sıkıştırma veri yapısına bağlıdır, ancak 10 kez sıkıştırma seyrek değil.</span><span class="sxs-lookup"><span data-stu-id="c862d-176">The amount of compression that you can achieve depends on the nature of the data, but 10 times the compression is not uncommon.</span></span>

<span data-ttu-id="c862d-177">Örneğin, 1 terabayt (TB) boyut sınırı olan bir veritabanı varsa ve columnstore dizinleri kullanarak 10 kez sıkıştırma elde size kullanıcı verilerini 10 TB toplam veritabanında uygun olamaz.</span><span class="sxs-lookup"><span data-stu-id="c862d-177">For example, if you have a database with a maximum size of 1 terabyte (TB) and you achieve 10 times the compression by using columnstore indexes, you can fit a total of 10 TB of user data in the database.</span></span>

<span data-ttu-id="c862d-178">Kümelenmemiş columnstore dizinleri kullandığınızda, temel tablo hala geleneksel rowstore biçiminde depolanır.</span><span class="sxs-lookup"><span data-stu-id="c862d-178">When you use nonclustered columnstore indexes, the base table is still stored in the traditional rowstore format.</span></span> <span data-ttu-id="c862d-179">Bu nedenle, depolama tasarrufları kümelenmiş columnstore dizinleriyle kadar büyük değil.</span><span class="sxs-lookup"><span data-stu-id="c862d-179">Therefore, the storage savings aren't as big as with clustered columnstore indexes.</span></span> <span data-ttu-id="c862d-180">Ancak, bir tek columnstore dizini ile geleneksel kümelenmemiş dizin sayısı değiştiriyorsanız, genel bir tablo için depolama ayak izini tasarruf görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c862d-180">However, if you're replacing a number of traditional nonclustered indexes with a single columnstore index, you can still see an overall savings in the storage footprint for the table.</span></span>

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a><span data-ttu-id="c862d-181">Fiyatlandırma katmanı arasındaki bellek içi teknolojileri kullanan veritabanlarını taşıma</span><span class="sxs-lookup"><span data-stu-id="c862d-181">Moving databases that use In-Memory technologies between pricing tiers</span></span>

<span data-ttu-id="c862d-182">Hiçbir zaman uyumsuzlukları ya da diğer sorunlar için daha yüksek bir fiyatlandırma katmanı, gibi standart Premium'a yükseltme, vardır.</span><span class="sxs-lookup"><span data-stu-id="c862d-182">There are never any incompatibilities or other problems when you upgrade to a higher pricing tier, such as from Standard to Premium.</span></span> <span data-ttu-id="c862d-183">Kullanılabilir işlevler ve kaynakları yalnızca artırın.</span><span class="sxs-lookup"><span data-stu-id="c862d-183">The available functionality and resources only increase.</span></span>

<span data-ttu-id="c862d-184">Ancak, fiyatlandırma katmanı eski sürüme düşürmeyi veritabanınızı olumsuz yönde etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="c862d-184">But downgrading the pricing tier can negatively impact your database.</span></span> <span data-ttu-id="c862d-185">Veritabanı bellek içi OLTP nesneler içerdiğinde, Premium'dan standart ya da temel düşürmek olduğunda özellikle belirgin bir etkisidir.</span><span class="sxs-lookup"><span data-stu-id="c862d-185">The impact is especially apparent when you downgrade from Premium to Standard or Basic when your database contains In-Memory OLTP objects.</span></span> <span data-ttu-id="c862d-186">(Bunların görünür kalmasını olsa bile), sonra indirgeme bellek için iyileştirilmiş tablolar ve columnstore dizinleri kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="c862d-186">Memory-optimized tables, and columnstore indexes, are unavailable after the downgrade (even if they remain visible).</span></span> <span data-ttu-id="c862d-187">Bir esnek havuzun fiyatlandırma katmanı düşürmeyi veya bir veritabanı bellek içi teknolojilerle birlikte, standart veya temel esnek havuz taşıma ilgili noktaların aynısı geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="c862d-187">The same considerations apply when you're lowering the pricing tier of an elastic pool, or moving a database with In-Memory technologies, into a Standard or Basic elastic pool.</span></span>

### <a name="in-memory-oltp"></a><span data-ttu-id="c862d-188">Bellek içi OLTP</span><span class="sxs-lookup"><span data-stu-id="c862d-188">In-Memory OLTP</span></span>

<span data-ttu-id="c862d-189">*Basic/standart eski sürüme düşürmeyi*: bellek içi OLTP veritabanlarında standart ya da temel katmanındaki desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="c862d-189">*Downgrading to Basic/Standard*: In-Memory OLTP isn't supported in databases in the Standard or Basic tier.</span></span> <span data-ttu-id="c862d-190">Ayrıca, tüm standart veya temel katmanı bellek içi OLTP nesnelere olan bir veritabanında taşınmasını mümkün değildir.</span><span class="sxs-lookup"><span data-stu-id="c862d-190">In addition, it isn't possible to move a database that has any In-Memory OLTP objects to the Standard or Basic tier.</span></span>

<span data-ttu-id="c862d-191">Standart/temel veritabanına düşürmek önce tüm bellek için iyileştirilmiş tablolar ve tablo türleri yanı sıra, tüm yerel koda derlenmiş T-SQL modülleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="c862d-191">Before you downgrade the database to Standard/Basic, remove all memory-optimized tables and table types, as well as all natively compiled T-SQL modules.</span></span>

<span data-ttu-id="c862d-192">Verilen bir veritabanı bellek içi OLTP destekleyip desteklemediğini anlamak için programlı bir yolu yoktur.</span><span class="sxs-lookup"><span data-stu-id="c862d-192">There is a programmatic way to understand whether a given database supports In-Memory OLTP.</span></span> <span data-ttu-id="c862d-193">Aşağıdaki Transact-SQL sorgusu çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c862d-193">You can execute the following Transact-SQL query:</span></span>

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

<span data-ttu-id="c862d-194">Sorgu döndürürse **1**, bellek içi OLTP bu veritabanında desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c862d-194">If the query returns **1**, In-Memory OLTP is supported in this database.</span></span>


<span data-ttu-id="c862d-195">*Daha düşük bir Premium katmanına eski sürüme düşürmeyi*: bellek için iyileştirilmiş tablolardaki verileri veritabanı fiyatlandırma katmanı ile ilişkili olduğundan veya esnek Havuzda kullanılabilir bellek içi OLTP depolama içinde sığması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c862d-195">*Downgrading to a lower Premium tier*: Data in memory-optimized tables must fit within the In-Memory OLTP storage that is associated with the pricing tier of the database or is available in the elastic pool.</span></span> <span data-ttu-id="c862d-196">Fiyatlandırma katmanı düşürmek deneyin veya yeterli kullanılabilir bellek içi OLTP depolama yok bir havuza veritabanı taşıma işlemi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="c862d-196">If you try to lower the pricing tier or move the database into a pool that doesn't have enough available In-Memory OLTP storage, the operation fails.</span></span>

### <a name="columnstore-indexes"></a><span data-ttu-id="c862d-197">Columnstore dizinleri</span><span class="sxs-lookup"><span data-stu-id="c862d-197">Columnstore indexes</span></span>

<span data-ttu-id="c862d-198">*Temel veya standart eski sürüme düşürmeyi*: Columnstore dizinleri yalnızca Premium fiyatlandırma katmanı ve standart ya da Basic katmanları üzerinde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c862d-198">*Downgrading to Basic or Standard*: Columnstore indexes are supported only on the Premium pricing tier, and not on the Standard or Basic tiers.</span></span> <span data-ttu-id="c862d-199">Veritabanınıza standart ya da temel düşürmek, columnstore dizini kullanılamaz duruma gelir.</span><span class="sxs-lookup"><span data-stu-id="c862d-199">When you downgrade your database to Standard or Basic, your columnstore index becomes unavailable.</span></span> <span data-ttu-id="c862d-200">Columnstore dizini sistem korur ancak hiç dizini yararlanır.</span><span class="sxs-lookup"><span data-stu-id="c862d-200">The system maintains your columnstore index, but it never leverages the index.</span></span> <span data-ttu-id="c862d-201">Daha sonra geri Premium yükseltirseniz, columnstore dizini yeniden işlevden hemen hazırdır.</span><span class="sxs-lookup"><span data-stu-id="c862d-201">If you later upgrade back to Premium, your columnstore index is immediately ready to be leveraged again.</span></span>

<span data-ttu-id="c862d-202">Varsa bir **kümelenmiş** columnstore dizini, tüm tablo olur kullanılamaz katmanı indirgeme sonra.</span><span class="sxs-lookup"><span data-stu-id="c862d-202">If you have a **clustered** columnstore index, the whole table becomes unavailable after tier downgrade.</span></span> <span data-ttu-id="c862d-203">Bu nedenle tüm bırakma öneririz *kümelenmiş* veritabanınızı Premium katmanı aşağıda düşürmek önce columnstore dizinini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c862d-203">Therefore we recommend that you drop all *clustered* columnstore indexes before you downgrade your database below the Premium tier.</span></span>

<span data-ttu-id="c862d-204">*Daha düşük bir Premium katmanına eski sürüme düşürmeyi*: tüm veritabanını esnek Havuzda kullanılabilir depolama alanı veya fiyatlandırma katmanı hedef için en büyük veritabanı boyutu içinde uyuyorsa bu indirgeme başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="c862d-204">*Downgrading to a lower Premium tier*: This downgrade succeeds if the whole database fits within the maximum database size for the target pricing tier, or within the available storage in the elastic pool.</span></span> <span data-ttu-id="c862d-205">Columnstore dizinleri gelen belirli üzerinde etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="c862d-205">There is no specific impact from the columnstore indexes.</span></span>


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-the-in-memory-oltp-sample"></a><span data-ttu-id="c862d-206">1. Bellek içi OLTP örneği yükleme</span><span class="sxs-lookup"><span data-stu-id="c862d-206">1. Install the In-Memory OLTP sample</span></span>

<span data-ttu-id="c862d-207">AdventureWorksLT örnek veritabanı içinde birkaç tıklama ile oluşturabileceğiniz [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c862d-207">You can create the AdventureWorksLT sample database with a few clicks in the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="c862d-208">Ardından, bu bölümdeki adımları nasıl AdventureWorksLT veritabanınızı bellek içi OLTP nesnelerle zenginleştirmek ve performans avantajı göstermek açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c862d-208">Then, the steps in this section explain how you can enrich your AdventureWorksLT database with In-Memory OLTP objects and demonstrate performance benefits.</span></span>

<span data-ttu-id="c862d-209">Daha fazla simplistic, ancak daha görsel olarak çekici performans gösteri için bellek içi OLTP için bkz:</span><span class="sxs-lookup"><span data-stu-id="c862d-209">For a more simplistic, but more visually appealing performance demo for In-Memory OLTP, see:</span></span>

- <span data-ttu-id="c862d-210">Yayın: [içinde-bellek-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span><span class="sxs-lookup"><span data-stu-id="c862d-210">Release: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span></span>
- <span data-ttu-id="c862d-211">Kaynak kodu: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span><span class="sxs-lookup"><span data-stu-id="c862d-211">Source code: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span></span>

#### <a name="installation-steps"></a><span data-ttu-id="c862d-212">Yükleme adımları</span><span class="sxs-lookup"><span data-stu-id="c862d-212">Installation steps</span></span>

1. <span data-ttu-id="c862d-213">İçinde [Azure portal](https://portal.azure.com/), bir sunucu üzerinde bir Premium veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c862d-213">In the [Azure portal](https://portal.azure.com/), create a Premium database on a server.</span></span> <span data-ttu-id="c862d-214">Ayarlama **kaynak** AdventureWorksLT örnek veritabanı.</span><span class="sxs-lookup"><span data-stu-id="c862d-214">Set the **Source** to the AdventureWorksLT sample database.</span></span> <span data-ttu-id="c862d-215">Ayrıntılı yönergeler için bkz: [ilk Azure SQL veritabanınızı oluşturma](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c862d-215">For detailed instructions, see [Create your first Azure SQL database](sql-database-get-started-portal.md).</span></span>

2. <span data-ttu-id="c862d-216">SQL Server Management Studio ile veritabanına bağlanmak [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="c862d-216">Connect to the database with SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

3. <span data-ttu-id="c862d-217">Kopya [bellek içi OLTP Transact-SQL betiği](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) panonuza.</span><span class="sxs-lookup"><span data-stu-id="c862d-217">Copy the [In-Memory OLTP Transact-SQL script](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) to your clipboard.</span></span> <span data-ttu-id="c862d-218">T-SQL komut dosyası, 1. adımda oluşturduğunuz AdventureWorksLT örnek veritabanı gerekli bellek içi nesneleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c862d-218">The T-SQL script creates the necessary In-Memory objects in the AdventureWorksLT sample database that you created in step 1.</span></span>

4. <span data-ttu-id="c862d-219">SSMS T-SQL betiğini yapıştırın ve betiği yürütün.</span><span class="sxs-lookup"><span data-stu-id="c862d-219">Paste the T-SQL script into SSMS, and then execute the script.</span></span> <span data-ttu-id="c862d-220">`MEMORY_OPTIMIZED = ON` Yan tümcesi CREATE TABLE deyimleri önemli.</span><span class="sxs-lookup"><span data-stu-id="c862d-220">The `MEMORY_OPTIMIZED = ON` clause CREATE TABLE statements are crucial.</span></span> <span data-ttu-id="c862d-221">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="c862d-221">For example:</span></span>


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a><span data-ttu-id="c862d-222">Hata 40536</span><span class="sxs-lookup"><span data-stu-id="c862d-222">Error 40536</span></span>


<span data-ttu-id="c862d-223">T-SQL komut dosyasını çalıştırdığınızda 40536 hata alırsanız, veritabanı bellek içi destekleyip desteklemediğini doğrulamak için aşağıdaki T-SQL betiğini çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c862d-223">If you get error 40536 when you run the T-SQL script, run the following T-SQL script to verify whether the database supports In-Memory:</span></span>


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


<span data-ttu-id="c862d-224">Sonucunu **0** , bellek içi desteklenmez, anlamına gelir ve **1** desteklenip desteklenmediğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="c862d-224">A result of **0** means that In-Memory isn't supported, and **1** means that it is supported.</span></span> <span data-ttu-id="c862d-225">Sorunu tanılamak için veritabanının Premium Hizmet katmanını olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c862d-225">To diagnose the problem, ensure that the database is at the Premium service tier.</span></span>


#### <a name="about-the-created-memory-optimized-items"></a><span data-ttu-id="c862d-226">Oluşturulan bellek için iyileştirilmiş öğeleri hakkında</span><span class="sxs-lookup"><span data-stu-id="c862d-226">About the created memory-optimized items</span></span>

<span data-ttu-id="c862d-227">**Tablolar**: örnek aşağıdaki bellek için iyileştirilmiş tablolarda içerir:</span><span class="sxs-lookup"><span data-stu-id="c862d-227">**Tables**: The sample contains the following memory-optimized tables:</span></span>

- <span data-ttu-id="c862d-228">SalesLT.Product_inmem</span><span class="sxs-lookup"><span data-stu-id="c862d-228">SalesLT.Product_inmem</span></span>
- <span data-ttu-id="c862d-229">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="c862d-229">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="c862d-230">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="c862d-230">SalesLT.SalesOrderDetail_inmem</span></span>
- <span data-ttu-id="c862d-231">Demo.DemoSalesOrderHeaderSeed</span><span class="sxs-lookup"><span data-stu-id="c862d-231">Demo.DemoSalesOrderHeaderSeed</span></span>
- <span data-ttu-id="c862d-232">Demo.DemoSalesOrderDetailSeed</span><span class="sxs-lookup"><span data-stu-id="c862d-232">Demo.DemoSalesOrderDetailSeed</span></span>


<span data-ttu-id="c862d-233">Bellek için iyileştirilmiş tablolar aracılığıyla inceleyebilirsiniz **Object Explorer** SSMS içinde.</span><span class="sxs-lookup"><span data-stu-id="c862d-233">You can inspect memory-optimized tables through the **Object Explorer** in SSMS.</span></span> <span data-ttu-id="c862d-234">Sağ **tabloları** > **filtre** > **filtre ayarları** > **bellek için iyileştirilmiş**.</span><span class="sxs-lookup"><span data-stu-id="c862d-234">Right-click **Tables** > **Filter** > **Filter Settings** > **Is Memory Optimized**.</span></span> <span data-ttu-id="c862d-235">Değer 1'e eşittir.</span><span class="sxs-lookup"><span data-stu-id="c862d-235">The value equals 1.</span></span>


<span data-ttu-id="c862d-236">Veya, Katalog görünümleri gibi sorgulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c862d-236">Or you can query the catalog views, such as:</span></span>


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


<span data-ttu-id="c862d-237">**Saklı yordam yerel koda derlenmiş**: SalesLT.usp_InsertSalesOrder_inmem Katalog görünümü sorgu ile inceleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c862d-237">**Natively compiled stored procedure**: You can inspect SalesLT.usp_InsertSalesOrder_inmem through a catalog view query:</span></span>


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-the-sample-oltp-workload"></a><span data-ttu-id="c862d-238">Örnek OLTP iş yükü çalıştırın</span><span class="sxs-lookup"><span data-stu-id="c862d-238">Run the sample OLTP workload</span></span>

<span data-ttu-id="c862d-239">Aşağıdaki iki arasındaki tek fark *saklı yordamlar* olan bellek için iyileştirilmiş tablolar sürümlerini ilk yordamı kullanır, ikinci yordam normal disk üzerinde tabloları kullanır:</span><span class="sxs-lookup"><span data-stu-id="c862d-239">The only difference between the following two *stored procedures* is that the first procedure uses memory-optimized versions of the tables, while the second procedure uses the regular on-disk tables:</span></span>

- <span data-ttu-id="c862d-240">SalesLT**.** usp_InsertSalesOrder**_inmem**</span><span class="sxs-lookup"><span data-stu-id="c862d-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span></span>
- <span data-ttu-id="c862d-241">SalesLT**.** usp_InsertSalesOrder**_ondisk**</span><span class="sxs-lookup"><span data-stu-id="c862d-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span></span>


<span data-ttu-id="c862d-242">Bu bölümde, kullanışlı kullanılması hakkında bilgi **ostress.exe** gerilimli düzeylerinde iki saklı yordamı yürütmek için yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="c862d-242">In this section, you see how to use the handy **ostress.exe** utility to execute the two stored procedures at stressful levels.</span></span> <span data-ttu-id="c862d-243">Tamamlamak iki stres çalıştırmaları için gereken süreyi karşılaştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c862d-243">You can compare how long it takes for the two stress runs to finish.</span></span>


<span data-ttu-id="c862d-244">Ostress.exe çalıştırdığınızda, her iki aşağıdakiler için tasarlanmış parametre değerlerinin geçmesini öneririz:</span><span class="sxs-lookup"><span data-stu-id="c862d-244">When you run ostress.exe, we recommend that you pass parameter values designed for both of the following:</span></span>

- <span data-ttu-id="c862d-245">Çok sayıda eşzamanlı bağlantı çalıştırmak kullanarak - n100.</span><span class="sxs-lookup"><span data-stu-id="c862d-245">Run a large number of concurrent connections, by using -n100.</span></span>
- <span data-ttu-id="c862d-246">Yüzlerce kez, her bağlantı döngü göre sahip kullanma - r500.</span><span class="sxs-lookup"><span data-stu-id="c862d-246">Have each connection loop hundreds of times, by using -r500.</span></span>


<span data-ttu-id="c862d-247">Bununla birlikte, her şeyin çalıştığından emin olmak - n10 ve - r50 gibi çok daha küçük değerlerle Başlat isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c862d-247">However, you might want to start with much smaller values like -n10 and -r50 to ensure that everything is working.</span></span>


### <a name="script-for-ostressexe"></a><span data-ttu-id="c862d-248">Ostress.exe için komut dosyası</span><span class="sxs-lookup"><span data-stu-id="c862d-248">Script for ostress.exe</span></span>


<span data-ttu-id="c862d-249">Bu bölümde bizim ostress.exe komut satırında katıştırılmış T-SQL betiği görüntüler.</span><span class="sxs-lookup"><span data-stu-id="c862d-249">This section displays the T-SQL script that is embedded in our ostress.exe command line.</span></span> <span data-ttu-id="c862d-250">Komut dosyasını daha önce yüklediğiniz T-SQL betiği tarafından oluşturulan öğeleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="c862d-250">The script uses items that were created by the T-SQL script that you installed earlier.</span></span>


<span data-ttu-id="c862d-251">Aşağıdaki komut dosyası bellek için iyileştirilmiş aşağıdaki beş satır öğelerini örnek satış siparişle ekler *tabloları*:</span><span class="sxs-lookup"><span data-stu-id="c862d-251">The following script inserts a sample sales order with five line items into the following memory-optimized *tables*:</span></span>

- <span data-ttu-id="c862d-252">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="c862d-252">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="c862d-253">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="c862d-253">SalesLT.SalesOrderDetail_inmem</span></span>


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


<span data-ttu-id="c862d-254">Yapmak için *_ondisk* ostress.exe için yukarıdaki T-SQL komut dosyası sürümünü, her iki oluşumları değiştirmek *_inmem* ile alt dize *_ondisk*.</span><span class="sxs-lookup"><span data-stu-id="c862d-254">To make the *_ondisk* version of the preceding T-SQL script for ostress.exe, you would replace both occurrences of the *_inmem* substring with *_ondisk*.</span></span> <span data-ttu-id="c862d-255">Bu değişiklik, tabloları ve saklı yordamlar adları etkiler.</span><span class="sxs-lookup"><span data-stu-id="c862d-255">These replacements affect the names of tables and stored procedures.</span></span>


### <a name="install-rml-utilities-and-ostress"></a><span data-ttu-id="c862d-256">RML yardımcı programları ve ostress yükleyin</span><span class="sxs-lookup"><span data-stu-id="c862d-256">Install RML utilities and ostress</span></span>


<span data-ttu-id="c862d-257">İdeal olarak, Azure sanal makine (VM) ostress.exe çalıştırmayı planladığınız.</span><span class="sxs-lookup"><span data-stu-id="c862d-257">Ideally, you would plan to run ostress.exe on an Azure virtual machine (VM).</span></span> <span data-ttu-id="c862d-258">Oluşturacak bir [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) AdventureWorksLT veritabanınızın bulunduğu aynı Azure coğrafi bölgede.</span><span class="sxs-lookup"><span data-stu-id="c862d-258">You would create an [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) in the same Azure geographic region where your AdventureWorksLT database resides.</span></span> <span data-ttu-id="c862d-259">Ancak bunun yerine dizüstü bilgisayarınızda ostress.exe çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c862d-259">But you can run ostress.exe on your laptop instead.</span></span>


<span data-ttu-id="c862d-260">VM veya ne olursa olsun, ana bilgisayar seçin, yeniden yürütme işaretleme dili (RML) yardımcı programlarını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c862d-260">On the VM, or on whatever host you choose, install the Replay Markup Language (RML) utilities.</span></span> <span data-ttu-id="c862d-261">Yardımcı programlar ostress.exe içerir.</span><span class="sxs-lookup"><span data-stu-id="c862d-261">The utilities include ostress.exe.</span></span>

<span data-ttu-id="c862d-262">Daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="c862d-262">For more information, see:</span></span>
- <span data-ttu-id="c862d-263">Ostress.exe tartışmada [örnek veritabanı bellek içi OLTP için](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="c862d-263">The ostress.exe discussion in [Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="c862d-264">[Örnek veritabanı için bellek içi OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="c862d-264">[Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="c862d-265">[Ostress.exe yüklemek için blog](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span><span class="sxs-lookup"><span data-stu-id="c862d-265">The [blog for installing ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span></span>



<!--
dn511655.aspx is for SQL 2014,
[Extensions to AdventureWorks to Demonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-the-inmem-stress-workload-first"></a><span data-ttu-id="c862d-266">Çalıştırma *_inmem* ilk iş yükü stres</span><span class="sxs-lookup"><span data-stu-id="c862d-266">Run the *_inmem* stress workload first</span></span>


<span data-ttu-id="c862d-267">Kullanabileceğiniz bir *RML Cmd komut istemi* bizim ostress.exe komut satırını çalıştırmak için penceresi.</span><span class="sxs-lookup"><span data-stu-id="c862d-267">You can use an *RML Cmd Prompt* window to run our ostress.exe command line.</span></span> <span data-ttu-id="c862d-268">Komut satırı parametreleri için ostress doğrudan:</span><span class="sxs-lookup"><span data-stu-id="c862d-268">The command-line parameters direct ostress to:</span></span>

- <span data-ttu-id="c862d-269">100 bağlantılara eşzamanlı olarak çalıştırın (-n100).</span><span class="sxs-lookup"><span data-stu-id="c862d-269">Run 100 connections concurrently (-n100).</span></span>
- <span data-ttu-id="c862d-270">Her bağlantınız 50 kez T-SQL betiği çalıştırın (-r50).</span><span class="sxs-lookup"><span data-stu-id="c862d-270">Have each connection run the T-SQL script 50 times (-r50).</span></span>


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


<span data-ttu-id="c862d-271">Önceki ostress.exe komut satırını çalıştırmak için:</span><span class="sxs-lookup"><span data-stu-id="c862d-271">To run the preceding ostress.exe command line:</span></span>


1. <span data-ttu-id="c862d-272">Veritabanı veri içeriği SSMS, tüm önceki çalışmalarını tarafından eklenen tüm verileri silmek için aşağıdaki komutu çalıştırarak sıfırlama:</span><span class="sxs-lookup"><span data-stu-id="c862d-272">Reset the database data content by running the following command in SSMS, to delete all the data that was inserted by any previous runs:</span></span>

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. <span data-ttu-id="c862d-273">Önceki ostress.exe komut satırını metnin panonuza kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="c862d-273">Copy the text of the preceding ostress.exe command line to your clipboard.</span></span>

3. <span data-ttu-id="c862d-274">Değiştir `<placeholders>` parametreleri -S - U -P -d doğru gerçek değerlerle için.</span><span class="sxs-lookup"><span data-stu-id="c862d-274">Replace the `<placeholders>` for the parameters -S -U -P -d with the correct real values.</span></span>

4. <span data-ttu-id="c862d-275">Düzenlenen komut satırında bir RML Cmd penceresinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c862d-275">Run your edited command line in an RML Cmd window.</span></span>


#### <a name="result-is-a-duration"></a><span data-ttu-id="c862d-276">Bir süre oluşur</span><span class="sxs-lookup"><span data-stu-id="c862d-276">Result is a duration</span></span>


<span data-ttu-id="c862d-277">Ostress.exe sona erdiğinde, RML Cmd penceresinde çalışma süresi da son satırı çıktı olarak yazar.</span><span class="sxs-lookup"><span data-stu-id="c862d-277">When ostress.exe finishes, it writes the run duration as its final line of output in the RML Cmd window.</span></span> <span data-ttu-id="c862d-278">Örneğin, daha kısa bir test çalıştırması yaklaşık 1,5 dakika devam:</span><span class="sxs-lookup"><span data-stu-id="c862d-278">For example, a shorter test run lasted about 1.5 minutes:</span></span>

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a><span data-ttu-id="c862d-279">Sıfırlama, düzenlemek *_ondisk*, sonra yeniden çalıştırın</span><span class="sxs-lookup"><span data-stu-id="c862d-279">Reset, edit for *_ondisk*, then rerun</span></span>


<span data-ttu-id="c862d-280">Sonuç elde ettikten sonra *_inmem* çalıştırmak, için aşağıdaki adımları gerçekleştirin *_ondisk* çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c862d-280">After you have the result from the *_inmem* run, perform the following steps for the *_ondisk* run:</span></span>


1. <span data-ttu-id="c862d-281">Veritabanı önceki çalışması tarafından eklenen tüm verileri silmek için SSMS aşağıdaki komutu çalıştırarak sıfırlama:</span><span class="sxs-lookup"><span data-stu-id="c862d-281">Reset the database by running the following command in SSMS to delete all the data that was inserted by the previous run:</span></span>
```
EXECUTE Demo.usp_DemoReset;
```

2. <span data-ttu-id="c862d-282">Tüm değiştirmek için ostress.exe komut satırı düzenleyin *_inmem* ile *_ondisk*.</span><span class="sxs-lookup"><span data-stu-id="c862d-282">Edit the ostress.exe command line to replace all *_inmem* with *_ondisk*.</span></span>

3. <span data-ttu-id="c862d-283">Ostress.exe ikinci kez yeniden çalıştırın ve süre sonuç yakalayın.</span><span class="sxs-lookup"><span data-stu-id="c862d-283">Rerun ostress.exe for the second time, and capture the duration result.</span></span>

4. <span data-ttu-id="c862d-284">Yeniden (sorumlu bir şekilde ne test verilerinin büyük bir miktarını olabilir silme) veritabanı sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="c862d-284">Again, reset the database (for responsibly deleting what can be a large amount of test data).</span></span>


#### <a name="expected-comparison-results"></a><span data-ttu-id="c862d-285">Beklenen Karşılaştırma sonuçları</span><span class="sxs-lookup"><span data-stu-id="c862d-285">Expected comparison results</span></span>

<span data-ttu-id="c862d-286">Bellek içi testlerimizde tarafından geliştirilmiş performans göstermiştir **dokuz kez** veritabanı ile aynı Azure bölgesinde bir Azure VM üzerinde çalışan ostress ile simplistic bu iş yükü için.</span><span class="sxs-lookup"><span data-stu-id="c862d-286">Our In-Memory tests have shown that performance improved by **nine times** for this simplistic workload, with ostress running on an Azure VM in the same Azure region as the database.</span></span>

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-the-in-memory-analytics-sample"></a><span data-ttu-id="c862d-287">2. Bellek içi analizi örneği yükleme</span><span class="sxs-lookup"><span data-stu-id="c862d-287">2. Install the In-Memory Analytics sample</span></span>


<span data-ttu-id="c862d-288">Bu bölümde, bir columnstore dizini bir geleneksel b-ağacı dizini karşı kullanırken GÇ ve İstatistikler sonuçlarını karşılaştırın.</span><span class="sxs-lookup"><span data-stu-id="c862d-288">In this section, you compare the IO and statistics results when you're using a columnstore index versus a traditional b-tree index.</span></span>


<span data-ttu-id="c862d-289">Bir OLTP iş yükü için gerçek zamanlı analiz almak için kümelenmemiş bir columnstore dizini kullanmak idealdir.</span><span class="sxs-lookup"><span data-stu-id="c862d-289">For real-time analytics on an OLTP workload, it's often best to use a nonclustered columnstore index.</span></span> <span data-ttu-id="c862d-290">Ayrıntılar için bkz [Columnstore dizinleri açıklanan](http://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="c862d-290">For details, see [Columnstore Indexes Described](http://msdn.microsoft.com/library/gg492088.aspx).</span></span>



### <a name="prepare-the-columnstore-analytics-test"></a><span data-ttu-id="c862d-291">Columnstore analytics test hazırlama</span><span class="sxs-lookup"><span data-stu-id="c862d-291">Prepare the columnstore analytics test</span></span>


1. <span data-ttu-id="c862d-292">Yeni bir AdventureWorksLT veritabanı örnekten oluşturmak için Azure portalını kullanın.</span><span class="sxs-lookup"><span data-stu-id="c862d-292">Use the Azure portal to create a fresh AdventureWorksLT database from the sample.</span></span>
 - <span data-ttu-id="c862d-293">Bu tam ad kullanın.</span><span class="sxs-lookup"><span data-stu-id="c862d-293">Use that exact name.</span></span>
 - <span data-ttu-id="c862d-294">Tüm Premium Hizmet katmanını seçin.</span><span class="sxs-lookup"><span data-stu-id="c862d-294">Choose any Premium service tier.</span></span>

2. <span data-ttu-id="c862d-295">Kopya [sql_in memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) panonuza.</span><span class="sxs-lookup"><span data-stu-id="c862d-295">Copy the [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) to your clipboard.</span></span>
 - <span data-ttu-id="c862d-296">T-SQL komut dosyası, 1. adımda oluşturduğunuz AdventureWorksLT örnek veritabanı gerekli bellek içi nesneleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c862d-296">The T-SQL script creates the necessary In-Memory objects in the AdventureWorksLT sample database that you created in step 1.</span></span>
 - <span data-ttu-id="c862d-297">Komut dosyası Boyut tablosuna ve iki olgu tabloları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c862d-297">The script creates the Dimension table and two fact tables.</span></span> <span data-ttu-id="c862d-298">Olgu tabloları 3.5 milyon satır her doldurulur.</span><span class="sxs-lookup"><span data-stu-id="c862d-298">The fact tables are populated with 3.5 million rows each.</span></span>
 - <span data-ttu-id="c862d-299">Komut dosyasının tamamlanması 15 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="c862d-299">The script might take 15 minutes to complete.</span></span>

3. <span data-ttu-id="c862d-300">SSMS T-SQL betiğini yapıştırın ve betiği yürütün.</span><span class="sxs-lookup"><span data-stu-id="c862d-300">Paste the T-SQL script into SSMS, and then execute the script.</span></span> <span data-ttu-id="c862d-301">**COLUMNSTORE** anahtar sözcük **CREATE INDEX** açıklamadır önemli olarak:</span><span class="sxs-lookup"><span data-stu-id="c862d-301">The **COLUMNSTORE** keyword in the **CREATE INDEX** statement is crucial, as in:</span></span><br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. <span data-ttu-id="c862d-302">AdventureWorksLT 130 uyumluluk düzeyi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="c862d-302">Set AdventureWorksLT to compatibility level 130:</span></span><br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    <span data-ttu-id="c862d-303">Düzeyi 130 doğrudan bellek içi özelliklerle ilgili değildir.</span><span class="sxs-lookup"><span data-stu-id="c862d-303">Level 130 is not directly related to In-Memory features.</span></span> <span data-ttu-id="c862d-304">Ancak düzeyi 130 genellikle 120'den daha hızlı sorgu performansı sağlar.</span><span class="sxs-lookup"><span data-stu-id="c862d-304">But level 130 generally provides faster query performance than 120.</span></span>


#### <a name="key-tables-and-columnstore-indexes"></a><span data-ttu-id="c862d-305">Anahtar tablolar ve columnstore dizinleri</span><span class="sxs-lookup"><span data-stu-id="c862d-305">Key tables and columnstore indexes</span></span>


- <span data-ttu-id="c862d-306">dbo. FactResellerSalesXL_CCI sıkıştırma, Gelişmiş bir kümelenmiş columnstore dizini içeren bir tablo olduğundan *veri* düzeyi.</span><span class="sxs-lookup"><span data-stu-id="c862d-306">dbo.FactResellerSalesXL_CCI is a table that has a clustered columnstore index, which has advanced compression at the *data* level.</span></span>

- <span data-ttu-id="c862d-307">dbo. FactResellerSalesXL_PageCompressed yalnızca sıkıştırılmış bir eşdeğer normal kümelenmiş dizin içeren bir tablo olduğundan *sayfa* düzeyi.</span><span class="sxs-lookup"><span data-stu-id="c862d-307">dbo.FactResellerSalesXL_PageCompressed is a table that has an equivalent regular clustered index, which is compressed only at the *page* level.</span></span>


#### <a name="key-queries-to-compare-the-columnstore-index"></a><span data-ttu-id="c862d-308">Columnstore dizinini karşılaştırmak için anahtar sorguları</span><span class="sxs-lookup"><span data-stu-id="c862d-308">Key queries to compare the columnstore index</span></span>


<span data-ttu-id="c862d-309">Vardır [çalıştırabileceğiniz birkaç T-SQL sorgu türleri](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) performans iyileştirmeleri görmek için.</span><span class="sxs-lookup"><span data-stu-id="c862d-309">There are [several T-SQL query types that you can run](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) to see performance improvements.</span></span> <span data-ttu-id="c862d-310">Adım 2'de T-SQL komut dosyası, bu sorguları çiftinin dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="c862d-310">In step 2 in the T-SQL script, pay attention to this pair of queries.</span></span> <span data-ttu-id="c862d-311">Bunlar yalnızca tek bir satırda farklılık gösterir:</span><span class="sxs-lookup"><span data-stu-id="c862d-311">They differ only on one line:</span></span>


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


<span data-ttu-id="c862d-312">FactResellerSalesXL kümelenmiş columnstore dizini olan\_CCI tablo.</span><span class="sxs-lookup"><span data-stu-id="c862d-312">A clustered columnstore index is in the FactResellerSalesXL\_CCI table.</span></span>

<span data-ttu-id="c862d-313">Aşağıdaki T-SQL komut dosyası Alıntısı istatistikleri GÇ ve her tablo için sorgu SÜREDİR yazdırır.</span><span class="sxs-lookup"><span data-stu-id="c862d-313">The following T-SQL script excerpt prints statistics for IO and TIME for the query of each table.</span></span>


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order to see Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins the Fact Table with dimension tables
-- Note this query will run on the Page Compressed table, Note down the time
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


-- This is the same Prior query on a table with a clustered columnstore index CCI
-- The comparison numbers are even more dramatic the larger the table is (this is an 11 million row table only)
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

<span data-ttu-id="c862d-314">P2 fiyatlandırma katmanı ile bir veritabanında, geleneksel dizin ile karşılaştırıldığında kümelenmiş columnstore dizini kullanarak bu sorgu performansı kazancı yaklaşık dokuz kez bekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c862d-314">In a database with the P2 pricing tier, you can expect about nine times the performance gain for this query by using the clustered columnstore index compared with the traditional index.</span></span> <span data-ttu-id="c862d-315">P15 ile columnstore dizinini kullanarak hakkında 57 kez performans kazancı bekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c862d-315">With P15, you can expect about 57 times the performance gain by using the columnstore index.</span></span>



## <a name="next-steps"></a><span data-ttu-id="c862d-316">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c862d-316">Next steps</span></span>

- [<span data-ttu-id="c862d-317">1 Hızlı Başlangıç: Daha hızlı bir T-SQL performans için bellek içi OLTP teknolojileri</span><span class="sxs-lookup"><span data-stu-id="c862d-317">Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance</span></span>](http://msdn.microsoft.com/library/mt694156.aspx)

- [<span data-ttu-id="c862d-318">Mevcut Azure SQL uygulamada kullanmak bellek içi OLTP</span><span class="sxs-lookup"><span data-stu-id="c862d-318">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

- <span data-ttu-id="c862d-319">[İzleyici bellek içi OLTP depolama](sql-database-in-memory-oltp-monitoring.md) bellek içi OLTP için</span><span class="sxs-lookup"><span data-stu-id="c862d-319">[Monitor In-Memory OLTP storage](sql-database-in-memory-oltp-monitoring.md) for In-Memory OLTP</span></span>


## <a name="additional-resources"></a><span data-ttu-id="c862d-320">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c862d-320">Additional resources</span></span>

#### <a name="deeper-information"></a><span data-ttu-id="c862d-321">Daha ayrıntılı bilgi</span><span class="sxs-lookup"><span data-stu-id="c862d-321">Deeper information</span></span>

- [<span data-ttu-id="c862d-322">Bellek içi OLTP SQL veritabanında ile % 70 tarafından DTU düşürürken çekirdek anahtar veritabanının iş yükü nasıl Katlar öğrenin</span><span class="sxs-lookup"><span data-stu-id="c862d-322">Learn how Quorum doubles key database’s workload while lowering DTU by 70% with In-Memory OLTP in SQL Database</span></span>](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)

- [<span data-ttu-id="c862d-323">Bellek içi OLTP de Azure SQL veritabanı Blog Gönderisi</span><span class="sxs-lookup"><span data-stu-id="c862d-323">In-Memory OLTP in Azure SQL Database Blog Post</span></span>](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

- [<span data-ttu-id="c862d-324">Bellek içi OLTP hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="c862d-324">Learn about In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="c862d-325">Columnstore dizinleri hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="c862d-325">Learn about columnstore indexes</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)

- [<span data-ttu-id="c862d-326">Gerçek zamanlı işletimsel analytics hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="c862d-326">Learn about real-time operational analytics</span></span>](http://msdn.microsoft.com/library/dn817827.aspx)

- <span data-ttu-id="c862d-327">Bkz: [yaygın iş yükü desenleri ve geçiş konuları](http://msdn.microsoft.com/library/dn673538.aspx) (burada bellek içi OLTP sık sağlar önemli performans artışları yükünün desenleri açıklayan)</span><span class="sxs-lookup"><span data-stu-id="c862d-327">See [Common Workload Patterns and Migration Considerations](http://msdn.microsoft.com/library/dn673538.aspx) (which describes workload patterns where In-Memory OLTP commonly provides significant performance gains)</span></span>

#### <a name="application-design"></a><span data-ttu-id="c862d-328">Uygulama tasarımı</span><span class="sxs-lookup"><span data-stu-id="c862d-328">Application design</span></span>

- [<span data-ttu-id="c862d-329">Bellek içi OLTP (bellek içi iyileştirme)</span><span class="sxs-lookup"><span data-stu-id="c862d-329">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="c862d-330">Mevcut Azure SQL uygulamada kullanmak bellek içi OLTP</span><span class="sxs-lookup"><span data-stu-id="c862d-330">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a><span data-ttu-id="c862d-331">Araçlar</span><span class="sxs-lookup"><span data-stu-id="c862d-331">Tools</span></span>

- [<span data-ttu-id="c862d-332">Azure portal</span><span class="sxs-lookup"><span data-stu-id="c862d-332">Azure portal</span></span>](https://portal.azure.com/)

- [<span data-ttu-id="c862d-333">SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="c862d-333">SQL Server Management Studio (SSMS)</span></span>](https://msdn.microsoft.com/library/mt238290.aspx)

- [<span data-ttu-id="c862d-334">SQL Server Veri Araçları (SSDT)</span><span class="sxs-lookup"><span data-stu-id="c862d-334">SQL Server Data Tools (SSDT)</span></span>](http://msdn.microsoft.com/library/mt204009.aspx)
