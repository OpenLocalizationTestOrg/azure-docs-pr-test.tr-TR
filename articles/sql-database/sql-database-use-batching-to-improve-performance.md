---
title: "aaaHow toouse tooimprove Azure SQL veritabanı uygulama performansı toplu işleme"
description: "Merhaba konu toplu işlemleri büyük ölçüde veritabanındaki kanıt sağlar imroves hello hızı ve Azure SQL veritabanı uygulamalarınızın ölçeklenebilirlik. Bu toplu teknikler herhangi bir SQL Server veritabanı için çalışır hello odak hello makalenin Azure üzerinde olsa da."
services: sql-database
documentationcenter: na
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 563862ca-c65a-46f6-975d-10df7ff6aa9c
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 124b203ee69c595f0813852ff09ef9ec6841233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-batching-tooimprove-sql-database-application-performance"></a><span data-ttu-id="eaa13-104">Nasıl toouse tooimprove SQL veritabanı uygulama performansını toplu işleme</span><span class="sxs-lookup"><span data-stu-id="eaa13-104">How toouse batching tooimprove SQL Database application performance</span></span>
<span data-ttu-id="eaa13-105">SQL veritabanı işlemleri tooAzure önemli ölçüde toplu işleme hello performans ve ölçeklenebilirlik uygulamalarınızın artırır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-105">Batching operations tooAzure SQL Database significantly improves hello performance and scalability of your applications.</span></span> <span data-ttu-id="eaa13-106">Sipariş toounderstand hello faydalarını sıralı ve toplu istekleri tooa SQL veritabanı karşılaştırmak bazı örnek test sonuçlarını hello ilk bölümü, bu makalenin ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-106">In order toounderstand hello benefits, hello first part of this article covers some sample test results that compare sequential and batched requests tooa SQL Database.</span></span> <span data-ttu-id="eaa13-107">Merhaba hello makalenin kalanında hello teknikleri, senaryoları ve konuları toohelp gösterir başarıyla Azure uygulamalarınızda toplu işleme toouse.</span><span class="sxs-lookup"><span data-stu-id="eaa13-107">hello remainder of hello article shows hello techniques, scenarios, and considerations toohelp you toouse batching successfully in your Azure applications.</span></span>

## <a name="why-is-batching-important-for-sql-database"></a><span data-ttu-id="eaa13-108">SQL veritabanı için önemli toplu işleme neden?</span><span class="sxs-lookup"><span data-stu-id="eaa13-108">Why is batching important for SQL Database?</span></span>
<span data-ttu-id="eaa13-109">Toplu işlem çağrıları tooa uzak hizmet performansını ve ölçeklenebilirliğini artırmak için iyi bilinen bir stratejidir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-109">Batching calls tooa remote service is a well-known strategy for increasing performance and scalability.</span></span> <span data-ttu-id="eaa13-110">Seri hale getirme, ağ aktarımı ve seri durumdan çıkarma gibi uzak bir hizmet ile maliyetleri tooany etkileşimleri işleme var. düzeltilmiştir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-110">There are fixed processing costs tooany interactions with a remote service, such as serialization, network transfer, and deserialization.</span></span> <span data-ttu-id="eaa13-111">Tek bir toplu birçok ayrı işlemlere paketleme bu maliyetleri en aza indirir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-111">Packaging many separate transactions into a single batch minimizes these costs.</span></span>

<span data-ttu-id="eaa13-112">Bu yazıda, tooexamine çeşitli SQL veritabanı toplu stratejilerini ve senaryoları istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="eaa13-112">In this paper, we want tooexamine various SQL Database batching strategies and scenarios.</span></span> <span data-ttu-id="eaa13-113">Bu stratejileri ayrıca SQL Server kullanan şirket içi uygulamaları için önemli olsa da, SQL veritabanı için toplu işleme hello kullanım vurgulama için birkaç nedeni vardır:</span><span class="sxs-lookup"><span data-stu-id="eaa13-113">Although these strategies are also important for on-premises applications that use SQL Server, there are several reasons for highlighting hello use of batching for SQL Database:</span></span>

* <span data-ttu-id="eaa13-114">Olup olmadığını potansiyel olarak büyük ağ gecikmesi SQL veritabanına erişim özellikle dış hello SQL veritabanına erişme aynı Microsoft Azure veri merkezi.</span><span class="sxs-lookup"><span data-stu-id="eaa13-114">There is potentially greater network latency in accessing SQL Database, especially if you are accessing SQL Database from outside hello same Microsoft Azure datacenter.</span></span>
* <span data-ttu-id="eaa13-115">hello veri verimliliğini hello SQL veritabanı anlamına gelir Hello çok müşterili özelliklere erişim katmanı karşılık gelen toohello hello veritabanının genel ölçeklenebilirlik.</span><span class="sxs-lookup"><span data-stu-id="eaa13-115">hello multitenant characteristics of SQL Database means that hello efficiency of hello data access layer correlates toohello overall scalability of hello database.</span></span> <span data-ttu-id="eaa13-116">SQL veritabanı, veritabanı kaynakları toohello zarar diğer kiracıların tekeline tek bir Kiracı/Kullanıcı engellemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-116">SQL Database must prevent any single tenant/user from monopolizing database resources toohello detriment of other tenants.</span></span> <span data-ttu-id="eaa13-117">Önceden tanımlanmış kotaları aşan yanıt toousage içinde SQL veritabanı işleme azaltın veya özel durumlar azaltma ile yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-117">In response toousage in excess of predefined quotas, SQL Database can reduce throughput or respond with throttling exceptions.</span></span> <span data-ttu-id="eaa13-118">Toplu işleme gibi verimliliği, SQL veritabanı üzerinde daha fazla iş bu sınırları ulaşmadan önce toodo etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="eaa13-118">Efficiencies, such as batching, enable you toodo more work on SQL Database before reaching these limits.</span></span> 
* <span data-ttu-id="eaa13-119">Toplu işleme ayrıca birden çok veritabanı (parçalama) kullanan mimari için geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-119">Batching is also effective for architectures that use multiple databases (sharding).</span></span> <span data-ttu-id="eaa13-120">Her veritabanı birimi ile etkileşim Hello verimliliğini hala bir anahtar genel ölçeklenebilirlik içinde faktördür.</span><span class="sxs-lookup"><span data-stu-id="eaa13-120">hello efficiency of your interaction with each database unit is still a key factor in your overall scalability.</span></span> 

<span data-ttu-id="eaa13-121">SQL veritabanı kullanmanın yararları hello konak hello veritabanının toomanage hello sunucuları yok biridir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-121">One of hello benefits of using SQL Database is that you don’t have toomanage hello servers that host hello database.</span></span> <span data-ttu-id="eaa13-122">Ancak, bu yönetilen altyapı Ayrıca, farklı veritabanı en iyi duruma getirme hakkında toothink anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-122">However, this managed infrastructure also means that you have toothink differently about database optimizations.</span></span> <span data-ttu-id="eaa13-123">Artık, donanım veya ağ tooimprove hello veritabanı altyapısı da bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eaa13-123">You can no longer look tooimprove hello database hardware or network infrastructure.</span></span> <span data-ttu-id="eaa13-124">Microsoft Azure konusu ortamlara denetler.</span><span class="sxs-lookup"><span data-stu-id="eaa13-124">Microsoft Azure controls those environments.</span></span> <span data-ttu-id="eaa13-125">denetleyebileceğiniz hello ana uygulamanızın SQL Database ile nasıl etkileşim kurduğu alanıdır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-125">hello main area that you can control is how your application interacts with SQL Database.</span></span> <span data-ttu-id="eaa13-126">Toplu işleme, bu en iyi duruma getirme biridir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-126">Batching is one of these optimizations.</span></span> 

<span data-ttu-id="eaa13-127">Merhaba ilk bölümü hello kağıt SQL veritabanını kullan .NET uygulamaları için çeşitli toplu teknikleri inceler.</span><span class="sxs-lookup"><span data-stu-id="eaa13-127">hello first part of hello paper examines various batching techniques for .NET applications that use SQL Database.</span></span> <span data-ttu-id="eaa13-128">Merhaba son iki bölüm toplu kılavuzları ve senaryoları kapsar.</span><span class="sxs-lookup"><span data-stu-id="eaa13-128">hello last two sections cover batching guidelines and scenarios.</span></span>

## <a name="batching-strategies"></a><span data-ttu-id="eaa13-129">Toplu işleme stratejileri</span><span class="sxs-lookup"><span data-stu-id="eaa13-129">Batching strategies</span></span>
### <a name="note-about-timing-results-in-this-topic"></a><span data-ttu-id="eaa13-130">Bu konudaki zamanlama sonuçlarıyla ilgili unutmayın</span><span class="sxs-lookup"><span data-stu-id="eaa13-130">Note about timing results in this topic</span></span>
> [!NOTE]
> <span data-ttu-id="eaa13-131">Sonuçları kıyaslamaları değildir ancak tooshow yöneliktir **göreli performans**.</span><span class="sxs-lookup"><span data-stu-id="eaa13-131">Results are not benchmarks but are meant tooshow **relative performance**.</span></span> <span data-ttu-id="eaa13-132">Zamanlamaları, en az 10 test çalışmaları ortalama üzerinde temel alır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-132">Timings are based on an average of at least 10 test runs.</span></span> <span data-ttu-id="eaa13-133">Boş bir tablo ekler işlemleridir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-133">Operations are inserts into an empty table.</span></span> <span data-ttu-id="eaa13-134">Bu testler ölçülen öncesi V12 olan ve mutlaka hello kullanarak yeni bir V12 veritabanında karşılaşabileceğiniz toothroughput benzemez [hizmet katmanları](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="eaa13-134">These tests were measured pre-V12, and they do not necessarily correspond toothroughput that you might experience in a V12 database using hello new [service tiers](sql-database-service-tiers.md).</span></span> <span data-ttu-id="eaa13-135">Merhaba göreli teknik toplu işleme hello yararı benzer olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-135">hello relative benefit of hello batching technique should be similar.</span></span>
> 
> 

### <a name="transactions"></a><span data-ttu-id="eaa13-136">İşlemler</span><span class="sxs-lookup"><span data-stu-id="eaa13-136">Transactions</span></span>
<span data-ttu-id="eaa13-137">Garip toobegin işlemleri ele tarafından toplu işleme, bir gözden geçirme görünüyor.</span><span class="sxs-lookup"><span data-stu-id="eaa13-137">It seems strange toobegin a review of batching by discussing transactions.</span></span> <span data-ttu-id="eaa13-138">Ancak istemci-tarafı işlemleri hello kullanımını performansını artıran zarif bir toplu sunucu tarafı etkisi olmaz.</span><span class="sxs-lookup"><span data-stu-id="eaa13-138">But hello use of client-side transactions has a subtle server-side batching effect that improves performance.</span></span> <span data-ttu-id="eaa13-139">Ve sıralı işlemlerinin bir hızlı yol tooimprove performansını sağlamak için yalnızca birkaç kod satırıyla, işlemleri eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-139">And transactions can be added with only a few lines of code, so they provide a fast way tooimprove performance of sequential operations.</span></span>

<span data-ttu-id="eaa13-140">INSERT dizisini içeren C# kod aşağıdaki hello göz önünde bulundurun ve basit bir tablo üzerinde işlem güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="eaa13-140">Consider hello following C# code that contains a sequence of insert and update operations on a simple table.</span></span>

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

<span data-ttu-id="eaa13-141">ADO.NET kodu sırayla aşağıdaki hello bu işlemleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-141">hello following ADO.NET code sequentially performs these operations.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

<span data-ttu-id="eaa13-142">Bu kodu en iyi şekilde toooptimize hello tooimplement istemci-tarafı bu çağrıları toplu işleme, bazı biçimidir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-142">hello best way toooptimize this code is tooimplement some form of client-side batching of these calls.</span></span> <span data-ttu-id="eaa13-143">Ancak bu kod basit yol tooincrease hello performansını çağrısı hello sırası işlemde yalnızca kaydırma tarafından.</span><span class="sxs-lookup"><span data-stu-id="eaa13-143">But there is a simple way tooincrease hello performance of this code by simply wrapping hello sequence of calls in a transaction.</span></span> <span data-ttu-id="eaa13-144">İşte hello bir işlem kullandığı aynı kodu.</span><span class="sxs-lookup"><span data-stu-id="eaa13-144">Here is hello same code that uses a transaction.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();
        SqlTransaction transaction = conn.BeginTransaction();

        foreach (string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn, transaction);
            cmd.ExecuteNonQuery();
        }

        transaction.Commit();
    }

<span data-ttu-id="eaa13-145">İşlemleri, aslında bu örnekler ikisinde kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="eaa13-145">Transactions are actually being used in both of these examples.</span></span> <span data-ttu-id="eaa13-146">Merhaba ilk örnekte, tek tek her çağrı örtük bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-146">In hello first example, each individual call is an implicit transaction.</span></span> <span data-ttu-id="eaa13-147">Merhaba ikinci örnekte, açık bir işlem tüm hello çağrılarını sarmalar.</span><span class="sxs-lookup"><span data-stu-id="eaa13-147">In hello second example, an explicit transaction wraps all of hello calls.</span></span> <span data-ttu-id="eaa13-148">Merhaba hello belgelerine başına [yazma ileriye işlem günlüğü](https://msdn.microsoft.com/library/ms186259.aspx), günlük kayıtlarını alırken temizlenmiş toohello disk hello hareketi tamamlar.</span><span class="sxs-lookup"><span data-stu-id="eaa13-148">Per hello documentation for hello [write-ahead transaction log](https://msdn.microsoft.com/library/ms186259.aspx), log records are flushed toohello disk when hello transaction commits.</span></span> <span data-ttu-id="eaa13-149">Hello işlem kadar bu nedenle bir işlemde daha fazla çağrıları dahil ederek hello yazma toohello işlem günlüğü gecikmeye yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-149">So by including more calls in a transaction, hello write toohello transaction log can delay until hello transaction is committed.</span></span> <span data-ttu-id="eaa13-150">Uygulamada hello yazma toohello sunucunun işlem günlüğü için toplu işleme olanaklı kılıyor.</span><span class="sxs-lookup"><span data-stu-id="eaa13-150">In effect, you are enabling batching for hello writes toohello server’s transaction log.</span></span>

<span data-ttu-id="eaa13-151">Aşağıdaki tablonun hello bazı geçici test sonuçlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-151">hello following table shows some ad-hoc testing results.</span></span> <span data-ttu-id="eaa13-152">Merhaba testleri sıralı aynı olan ve olmayan işlemler ekler hello gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-152">hello tests performed hello same sequential inserts with and without transactions.</span></span> <span data-ttu-id="eaa13-153">Daha fazla perspektif için bir Microsoft Azure dizüstü toohello veritabanında testlerin ilk Seti hello uzaktan verdi.</span><span class="sxs-lookup"><span data-stu-id="eaa13-153">For more perspective, hello first set of tests ran remotely from a laptop toohello database in Microsoft Azure.</span></span> <span data-ttu-id="eaa13-154">Merhaba testlerin ikinci Seti bir bulut hizmeti ve her ikisi de hello içinde aynı belgeler, veritabanı çalışan Microsoft Azure veri merkezi (Batı ABD).</span><span class="sxs-lookup"><span data-stu-id="eaa13-154">hello second set of tests ran from a cloud service and database that both resided within hello same Microsoft Azure datacenter (West US).</span></span> <span data-ttu-id="eaa13-155">Merhaba aşağıdaki tabloda hello süresi sıralı ekler ve işlemleri kullanılmadan milisaniye olarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-155">hello following table shows hello duration in milliseconds of sequential inserts with and without transactions.</span></span>

<span data-ttu-id="eaa13-156">**Şirket içi tooAzure**:</span><span class="sxs-lookup"><span data-stu-id="eaa13-156">**On-Premises tooAzure**:</span></span>

| <span data-ttu-id="eaa13-157">İşlemler</span><span class="sxs-lookup"><span data-stu-id="eaa13-157">Operations</span></span> | <span data-ttu-id="eaa13-158">Hiçbir işlem (ms)</span><span class="sxs-lookup"><span data-stu-id="eaa13-158">No Transaction (ms)</span></span> | <span data-ttu-id="eaa13-159">İşlem (ms)</span><span class="sxs-lookup"><span data-stu-id="eaa13-159">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eaa13-160">1</span><span class="sxs-lookup"><span data-stu-id="eaa13-160">1</span></span> |<span data-ttu-id="eaa13-161">130</span><span class="sxs-lookup"><span data-stu-id="eaa13-161">130</span></span> |<span data-ttu-id="eaa13-162">402</span><span class="sxs-lookup"><span data-stu-id="eaa13-162">402</span></span> |
| <span data-ttu-id="eaa13-163">10</span><span class="sxs-lookup"><span data-stu-id="eaa13-163">10</span></span> |<span data-ttu-id="eaa13-164">1208</span><span class="sxs-lookup"><span data-stu-id="eaa13-164">1208</span></span> |<span data-ttu-id="eaa13-165">1226</span><span class="sxs-lookup"><span data-stu-id="eaa13-165">1226</span></span> |
| <span data-ttu-id="eaa13-166">100</span><span class="sxs-lookup"><span data-stu-id="eaa13-166">100</span></span> |<span data-ttu-id="eaa13-167">12662</span><span class="sxs-lookup"><span data-stu-id="eaa13-167">12662</span></span> |<span data-ttu-id="eaa13-168">10395</span><span class="sxs-lookup"><span data-stu-id="eaa13-168">10395</span></span> |
| <span data-ttu-id="eaa13-169">1000</span><span class="sxs-lookup"><span data-stu-id="eaa13-169">1000</span></span> |<span data-ttu-id="eaa13-170">128852</span><span class="sxs-lookup"><span data-stu-id="eaa13-170">128852</span></span> |<span data-ttu-id="eaa13-171">102917</span><span class="sxs-lookup"><span data-stu-id="eaa13-171">102917</span></span> |

<span data-ttu-id="eaa13-172">**Azure tooAzure (aynı veri merkezinde)**:</span><span class="sxs-lookup"><span data-stu-id="eaa13-172">**Azure tooAzure (same datacenter)**:</span></span>

| <span data-ttu-id="eaa13-173">İşlemler</span><span class="sxs-lookup"><span data-stu-id="eaa13-173">Operations</span></span> | <span data-ttu-id="eaa13-174">Hiçbir işlem (ms)</span><span class="sxs-lookup"><span data-stu-id="eaa13-174">No Transaction (ms)</span></span> | <span data-ttu-id="eaa13-175">İşlem (ms)</span><span class="sxs-lookup"><span data-stu-id="eaa13-175">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eaa13-176">1</span><span class="sxs-lookup"><span data-stu-id="eaa13-176">1</span></span> |<span data-ttu-id="eaa13-177">21</span><span class="sxs-lookup"><span data-stu-id="eaa13-177">21</span></span> |<span data-ttu-id="eaa13-178">26</span><span class="sxs-lookup"><span data-stu-id="eaa13-178">26</span></span> |
| <span data-ttu-id="eaa13-179">10</span><span class="sxs-lookup"><span data-stu-id="eaa13-179">10</span></span> |<span data-ttu-id="eaa13-180">220</span><span class="sxs-lookup"><span data-stu-id="eaa13-180">220</span></span> |<span data-ttu-id="eaa13-181">56</span><span class="sxs-lookup"><span data-stu-id="eaa13-181">56</span></span> |
| <span data-ttu-id="eaa13-182">100</span><span class="sxs-lookup"><span data-stu-id="eaa13-182">100</span></span> |<span data-ttu-id="eaa13-183">2145</span><span class="sxs-lookup"><span data-stu-id="eaa13-183">2145</span></span> |<span data-ttu-id="eaa13-184">341</span><span class="sxs-lookup"><span data-stu-id="eaa13-184">341</span></span> |
| <span data-ttu-id="eaa13-185">1000</span><span class="sxs-lookup"><span data-stu-id="eaa13-185">1000</span></span> |<span data-ttu-id="eaa13-186">21479</span><span class="sxs-lookup"><span data-stu-id="eaa13-186">21479</span></span> |<span data-ttu-id="eaa13-187">2756</span><span class="sxs-lookup"><span data-stu-id="eaa13-187">2756</span></span> |

> [!NOTE]
> <span data-ttu-id="eaa13-188">Sonuçları kıyaslamaları değildir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-188">Results are not benchmarks.</span></span> <span data-ttu-id="eaa13-189">Merhaba bkz [bu konudaki zamanlama sonuçlarıyla ilgili Not](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="eaa13-189">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="eaa13-190">Merhaba önceki test sonuçlarına bağlı olarak bir işlem içinde tek bir işlem kaydırma aslında performansı düşürür.</span><span class="sxs-lookup"><span data-stu-id="eaa13-190">Based on hello previous test results, wrapping a single operation in a transaction actually decreases performance.</span></span> <span data-ttu-id="eaa13-191">Ancak, tek bir işlem içinde işlemlerinin hello sayısı arttıkça, hello performans geliştirmesi daha olarak işaretlenmiş olur.</span><span class="sxs-lookup"><span data-stu-id="eaa13-191">But as you increase hello number of operations within a single transaction, hello performance improvement becomes more marked.</span></span> <span data-ttu-id="eaa13-192">tüm işlemleri hello Microsoft Azure veri merkezi içinde olduğunda hello performans ayrıca daha belirgin farktır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-192">hello performance difference is also more noticeable when all operations occur within hello Microsoft Azure datacenter.</span></span> <span data-ttu-id="eaa13-193">Merhaba dış hello Microsoft Azure veri merkezinden SQL veritabanı kullanarak, daha yüksek gecikme süresi işlemleri kullanmanın hello performans kazancı gölgelendiren.</span><span class="sxs-lookup"><span data-stu-id="eaa13-193">hello increased latency of using SQL Database from outside hello Microsoft Azure datacenter overshadows hello performance gain of using transactions.</span></span>

<span data-ttu-id="eaa13-194">İşlemler Hello kullanımı performansı artırabilirsiniz ancak çok devam[işlemleri ve bağlantıları için en iyi uygulamaları gözlemlemek](https://msdn.microsoft.com/library/ms187484.aspx).</span><span class="sxs-lookup"><span data-stu-id="eaa13-194">Although hello use of transactions can increase performance, continue too[observe best practices for transactions and connections](https://msdn.microsoft.com/library/ms187484.aspx).</span></span> <span data-ttu-id="eaa13-195">Merhaba iş tamamlandıktan sonra hello işlem olası ve Kapat hello veritabanı bağlantısı olarak kısa tutun.</span><span class="sxs-lookup"><span data-stu-id="eaa13-195">Keep hello transaction as short as possible, and close hello database connection after hello work completes.</span></span> <span data-ttu-id="eaa13-196">Merhaba önceki örnekte deyimiyle hello hello izleyen kod bloğunun tamamlandığında hello bağlantı kapalı olduğundan emin olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="eaa13-196">hello using statement in hello previous example assures that hello connection is closed when hello subsequent code block completes.</span></span>

<span data-ttu-id="eaa13-197">Merhaba önceki örnekte iki satır bir yerel işlem tooany ADO.NET koduyla ekleyebileceğiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-197">hello previous example demonstrates that you can add a local transaction tooany ADO.NET code with two lines.</span></span> <span data-ttu-id="eaa13-198">İşlemler tooimprove hello performans sıralı yapan kod ekleme, güncelleştirme ve silme işlemleri hızlı bir yol sunar.</span><span class="sxs-lookup"><span data-stu-id="eaa13-198">Transactions offer a quick way tooimprove hello performance of code that makes sequential insert, update, and delete operations.</span></span> <span data-ttu-id="eaa13-199">Ancak, hello hızlı performans için tablo değerli parametreleri gibi istemci tarafı, toplu işleme hello kod başka tootake avantajı değiştirmeyi göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="eaa13-199">However, for hello fastest performance, consider changing hello code further tootake advantage of client-side batching, such as table-valued parameters.</span></span>

<span data-ttu-id="eaa13-200">ADO.NET işlemleri hakkında daha fazla bilgi için bkz: [ADO.NET yerel işlemlerde](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span><span class="sxs-lookup"><span data-stu-id="eaa13-200">For more information about transactions in ADO.NET, see [Local Transactions in ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span></span>

### <a name="table-valued-parameters"></a><span data-ttu-id="eaa13-201">Tablo değerli parametreleri</span><span class="sxs-lookup"><span data-stu-id="eaa13-201">Table-valued parameters</span></span>
<span data-ttu-id="eaa13-202">Tablo değerli parametreleri kullanıcı tanımlı tablo türü parametre olarak Transact-SQL deyimi, saklı yordamları ve işlevleri destekler.</span><span class="sxs-lookup"><span data-stu-id="eaa13-202">Table-valued parameters support user-defined table types as parameters in Transact-SQL statements, stored procedures, and functions.</span></span> <span data-ttu-id="eaa13-203">Bu istemci-tarafı toplu teknik toosend sağlayan hello tablo değerli parametre içindeki verilerin birden çok satır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-203">This client-side batching technique allows you toosend multiple rows of data within hello table-valued parameter.</span></span> <span data-ttu-id="eaa13-204">toouse tablo değerli parametreleri, ilk olarak bir tablo türü tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="eaa13-204">toouse table-valued parameters, first define a table type.</span></span> <span data-ttu-id="eaa13-205">Transact-SQL deyimi aşağıdaki hello adlı bir tablo türü oluşturur **MyTableType**.</span><span class="sxs-lookup"><span data-stu-id="eaa13-205">hello following Transact-SQL statement creates a table type named **MyTableType**.</span></span>

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


<span data-ttu-id="eaa13-206">Kod içinde oluşturduğunuz bir **DataTable** hello ile aynı ad ve hello tablo türü türlerini tam.</span><span class="sxs-lookup"><span data-stu-id="eaa13-206">In code, you create a **DataTable** with hello exact same names and types of hello table type.</span></span> <span data-ttu-id="eaa13-207">Bunu geçirmek **DataTable** metin sorgusu veya saklı yordam parametresinde çağırın.</span><span class="sxs-lookup"><span data-stu-id="eaa13-207">Pass this **DataTable** in a parameter in a text query or stored procedure call.</span></span> <span data-ttu-id="eaa13-208">Merhaba aşağıdaki örnekte bu teknik gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="eaa13-208">hello following example shows this technique:</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        DataTable table = new DataTable();
        // Add columns and rows. hello following is a simple example.
        table.Columns.Add("mytext", typeof(string));
        table.Columns.Add("num", typeof(int));    
        for (var i = 0; i < 10; i++)
        {
            table.Rows.Add(DateTime.Now.ToString(), DateTime.Now.Millisecond);
        }

        SqlCommand cmd = new SqlCommand(
            "INSERT INTO MyTable(mytext, num) SELECT mytext, num FROM @TestTvp",
            connection);

        cmd.Parameters.Add(
            new SqlParameter()
            {
                ParameterName = "@TestTvp",
                SqlDbType = SqlDbType.Structured,
                TypeName = "MyTableType",
                Value = table,
            });

        cmd.ExecuteNonQuery();
    }

<span data-ttu-id="eaa13-209">Merhaba önceki örnekte hello **SqlCommand** nesnesi bir tablo değerli parametresinden satırları ekler  **@TestTvp** .</span><span class="sxs-lookup"><span data-stu-id="eaa13-209">In hello previous example, hello **SqlCommand** object inserts rows from a table-valued parameter, **@TestTvp**.</span></span> <span data-ttu-id="eaa13-210">daha önce oluşturduğunuz hello **DataTable** nesne hello toothis parametresiyle atanmış **SqlCommand.Parameters.Add** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="eaa13-210">hello previously created **DataTable** object is assigned toothis parameter with hello **SqlCommand.Parameters.Add** method.</span></span> <span data-ttu-id="eaa13-211">Bir toplu hello ekler, sıralı ekler hello performans artışları önemli ölçüde çağırın.</span><span class="sxs-lookup"><span data-stu-id="eaa13-211">Batching hello inserts in one call significantly increases hello performance over sequential inserts.</span></span>

<span data-ttu-id="eaa13-212">tooimprove hello önceki örnek ayrıca, metin tabanlı komutu yerine bir saklı yordamı kullanın.</span><span class="sxs-lookup"><span data-stu-id="eaa13-212">tooimprove hello previous example further, use a stored procedure instead of a text-based command.</span></span> <span data-ttu-id="eaa13-213">Transact-SQL komutu aşağıdaki hello oluşturur hello isteyen bir saklı yordamı **SimpleTestTableType** tablo değerli parametre.</span><span class="sxs-lookup"><span data-stu-id="eaa13-213">hello following Transact-SQL command creates a stored procedure that takes hello **SimpleTestTableType** table-valued parameter.</span></span>

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

<span data-ttu-id="eaa13-214">Merhaba değiştirme **SqlCommand** hello önceki kod örneğinde toohello aşağıdaki bildiriminde nesne.</span><span class="sxs-lookup"><span data-stu-id="eaa13-214">Then change hello **SqlCommand** object declaration in hello previous code example toohello following.</span></span>

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

<span data-ttu-id="eaa13-215">Çoğu durumda, diğer toplu teknikleri daha eşdeğer veya daha iyi performans tablo değerli parametrelere sahip.</span><span class="sxs-lookup"><span data-stu-id="eaa13-215">In most cases, table-valued parameters have equivalent or better performance than other batching techniques.</span></span> <span data-ttu-id="eaa13-216">Diğer seçenekler daha esnek olduğundan tablo değerli genellikle tercih, parametreleridir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-216">Table-valued parameters are often preferable, because they are more flexible than other options.</span></span> <span data-ttu-id="eaa13-217">Örneğin, SQL toplu kopyalama gibi başka teknikler yalnızca yeni satır hello ekleme izin verir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-217">For example, other techniques, such as SQL bulk copy, only permit hello insertion of new rows.</span></span> <span data-ttu-id="eaa13-218">Ancak tablo değerli parametreleri ile Merhaba saklı yordamı toodetermine hangi satırların güncelleştirmelerin mantığı kullanabilirsiniz ve hangi ekler.</span><span class="sxs-lookup"><span data-stu-id="eaa13-218">But with table-valued parameters, you can use logic in hello stored procedure toodetermine which rows are updates and which are inserts.</span></span> <span data-ttu-id="eaa13-219">Merhaba tablo türü de değiştirilmiş toocontain hello satır eklenmesi, silinmiş veya güncelleştirilmesi belirtilen olup olmadığını gösteren bir "İşlem" sütunu olabilir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-219">hello table type can also be modified toocontain an “Operation” column that indicates whether hello specified row should be inserted, updated, or deleted.</span></span>

<span data-ttu-id="eaa13-220">Aşağıdaki tablonun hello geçici tablo değerli parametreleri hello kullanımı için test sonuçları milisaniye olarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-220">hello following table shows ad-hoc test results for hello use of table-valued parameters in milliseconds.</span></span>

| <span data-ttu-id="eaa13-221">İşlemler</span><span class="sxs-lookup"><span data-stu-id="eaa13-221">Operations</span></span> | <span data-ttu-id="eaa13-222">Şirket içi tooAzure (ms)</span><span class="sxs-lookup"><span data-stu-id="eaa13-222">On-Premises tooAzure (ms)</span></span> | <span data-ttu-id="eaa13-223">Azure aynı veri merkezinde (ms)</span><span class="sxs-lookup"><span data-stu-id="eaa13-223">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eaa13-224">1</span><span class="sxs-lookup"><span data-stu-id="eaa13-224">1</span></span> |<span data-ttu-id="eaa13-225">124</span><span class="sxs-lookup"><span data-stu-id="eaa13-225">124</span></span> |<span data-ttu-id="eaa13-226">32</span><span class="sxs-lookup"><span data-stu-id="eaa13-226">32</span></span> |
| <span data-ttu-id="eaa13-227">10</span><span class="sxs-lookup"><span data-stu-id="eaa13-227">10</span></span> |<span data-ttu-id="eaa13-228">131</span><span class="sxs-lookup"><span data-stu-id="eaa13-228">131</span></span> |<span data-ttu-id="eaa13-229">25</span><span class="sxs-lookup"><span data-stu-id="eaa13-229">25</span></span> |
| <span data-ttu-id="eaa13-230">100</span><span class="sxs-lookup"><span data-stu-id="eaa13-230">100</span></span> |<span data-ttu-id="eaa13-231">338</span><span class="sxs-lookup"><span data-stu-id="eaa13-231">338</span></span> |<span data-ttu-id="eaa13-232">51</span><span class="sxs-lookup"><span data-stu-id="eaa13-232">51</span></span> |
| <span data-ttu-id="eaa13-233">1000</span><span class="sxs-lookup"><span data-stu-id="eaa13-233">1000</span></span> |<span data-ttu-id="eaa13-234">2615</span><span class="sxs-lookup"><span data-stu-id="eaa13-234">2615</span></span> |<span data-ttu-id="eaa13-235">382</span><span class="sxs-lookup"><span data-stu-id="eaa13-235">382</span></span> |
| <span data-ttu-id="eaa13-236">10000</span><span class="sxs-lookup"><span data-stu-id="eaa13-236">10000</span></span> |<span data-ttu-id="eaa13-237">23830</span><span class="sxs-lookup"><span data-stu-id="eaa13-237">23830</span></span> |<span data-ttu-id="eaa13-238">3586</span><span class="sxs-lookup"><span data-stu-id="eaa13-238">3586</span></span> |

> [!NOTE]
> <span data-ttu-id="eaa13-239">Sonuçları kıyaslamaları değildir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-239">Results are not benchmarks.</span></span> <span data-ttu-id="eaa13-240">Merhaba bkz [bu konudaki zamanlama sonuçlarıyla ilgili Not](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="eaa13-240">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="eaa13-241">Toplu işleme gelen hello performans kazancı hemen açıktır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-241">hello performance gain from batching is immediately apparent.</span></span> <span data-ttu-id="eaa13-242">Merhaba önceki sıralı test, 1000 işlemleri dış hello datacenter ve hello veri merkezinde bulunan 21 saniyeden 129 saniye sürdü.</span><span class="sxs-lookup"><span data-stu-id="eaa13-242">In hello previous sequential test, 1000 operations took 129 seconds outside hello datacenter and 21 seconds from within hello datacenter.</span></span> <span data-ttu-id="eaa13-243">Ancak tablo değerli parametreleri ile 1000 işlemleri yalnızca hello veri merkezi dışında 2.6 saniye ile Merhaba veri merkezinde bulunan 0,4 saniye sürer.</span><span class="sxs-lookup"><span data-stu-id="eaa13-243">But with table-valued parameters, 1000 operations take only 2.6 seconds outside hello datacenter and 0.4 seconds within hello datacenter.</span></span>

<span data-ttu-id="eaa13-244">Tablo değerli parametreleri hakkında daha fazla bilgi için bkz: [tablo değerli parametreleri](https://msdn.microsoft.com/library/bb510489.aspx).</span><span class="sxs-lookup"><span data-stu-id="eaa13-244">For more information on table-valued parameters, see [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

### <a name="sql-bulk-copy"></a><span data-ttu-id="eaa13-245">SQL toplu kopyalama</span><span class="sxs-lookup"><span data-stu-id="eaa13-245">SQL bulk copy</span></span>
<span data-ttu-id="eaa13-246">SQL toplu kopyalama başka bir şekilde tooinsert büyük miktarlarda verinin bir hedef veritabanına ' dir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-246">SQL bulk copy is another way tooinsert large amounts of data into a target database.</span></span> <span data-ttu-id="eaa13-247">.NET uygulamaları hello kullanabileceğiniz **SqlBulkCopy** sınıfı tooperform toplu ekleme işlemleri.</span><span class="sxs-lookup"><span data-stu-id="eaa13-247">.NET applications can use hello **SqlBulkCopy** class tooperform bulk insert operations.</span></span> <span data-ttu-id="eaa13-248">**SqlBulkCopy** işlevi toohello komut satırı aracı'nda benzer **Bcp.exe**, veya hello Transact-SQL deyimini **BULK INSERT**.</span><span class="sxs-lookup"><span data-stu-id="eaa13-248">**SqlBulkCopy** is similar in function toohello command-line tool, **Bcp.exe**, or hello Transact-SQL statement, **BULK INSERT**.</span></span> <span data-ttu-id="eaa13-249">Merhaba aşağıdaki kod örneğinde nasıl toobulk kopyalama hello hello kaynağında satırları gösterir **DataTable**, tablo, SQL Server'daki MyTable toohello hedef tablo.</span><span class="sxs-lookup"><span data-stu-id="eaa13-249">hello following code example shows how toobulk copy hello rows in hello source **DataTable**, table, toohello destination table in SQL Server, MyTable.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        using (SqlBulkCopy bulkCopy = new SqlBulkCopy(connection))
        {
            bulkCopy.DestinationTableName = "MyTable";
            bulkCopy.ColumnMappings.Add("mytext", "mytext");
            bulkCopy.ColumnMappings.Add("num", "num");
            bulkCopy.WriteToServer(table);
        }
    }

<span data-ttu-id="eaa13-250">Toplu kopyalama tablo değerli parametre tercih edilen olduğu bazı durumlar vardır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-250">There are some cases where bulk copy is preferred over table-valued parameters.</span></span> <span data-ttu-id="eaa13-251">Tablo değerli parametreleri karşılık toplu ekleme işlemleri hello konudaki Hello karşılaştırma tablosuna bakın [tablo değerli parametreleri](https://msdn.microsoft.com/library/bb510489.aspx).</span><span class="sxs-lookup"><span data-stu-id="eaa13-251">See hello comparison table of Table-Valued parameters versus BULK INSERT operations in hello topic [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

<span data-ttu-id="eaa13-252">Merhaba aşağıdaki geçici test sonuçları gösterir hello performansını ile toplu işleme **SqlBulkCopy** milisaniye cinsinden.</span><span class="sxs-lookup"><span data-stu-id="eaa13-252">hello following ad-hoc test results show hello performance of batching with **SqlBulkCopy** in milliseconds.</span></span>

| <span data-ttu-id="eaa13-253">İşlemler</span><span class="sxs-lookup"><span data-stu-id="eaa13-253">Operations</span></span> | <span data-ttu-id="eaa13-254">Şirket içi tooAzure (ms)</span><span class="sxs-lookup"><span data-stu-id="eaa13-254">On-Premises tooAzure (ms)</span></span> | <span data-ttu-id="eaa13-255">Azure aynı veri merkezinde (ms)</span><span class="sxs-lookup"><span data-stu-id="eaa13-255">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eaa13-256">1</span><span class="sxs-lookup"><span data-stu-id="eaa13-256">1</span></span> |<span data-ttu-id="eaa13-257">433</span><span class="sxs-lookup"><span data-stu-id="eaa13-257">433</span></span> |<span data-ttu-id="eaa13-258">57</span><span class="sxs-lookup"><span data-stu-id="eaa13-258">57</span></span> |
| <span data-ttu-id="eaa13-259">10</span><span class="sxs-lookup"><span data-stu-id="eaa13-259">10</span></span> |<span data-ttu-id="eaa13-260">441</span><span class="sxs-lookup"><span data-stu-id="eaa13-260">441</span></span> |<span data-ttu-id="eaa13-261">32</span><span class="sxs-lookup"><span data-stu-id="eaa13-261">32</span></span> |
| <span data-ttu-id="eaa13-262">100</span><span class="sxs-lookup"><span data-stu-id="eaa13-262">100</span></span> |<span data-ttu-id="eaa13-263">636</span><span class="sxs-lookup"><span data-stu-id="eaa13-263">636</span></span> |<span data-ttu-id="eaa13-264">53</span><span class="sxs-lookup"><span data-stu-id="eaa13-264">53</span></span> |
| <span data-ttu-id="eaa13-265">1000</span><span class="sxs-lookup"><span data-stu-id="eaa13-265">1000</span></span> |<span data-ttu-id="eaa13-266">2535</span><span class="sxs-lookup"><span data-stu-id="eaa13-266">2535</span></span> |<span data-ttu-id="eaa13-267">341</span><span class="sxs-lookup"><span data-stu-id="eaa13-267">341</span></span> |
| <span data-ttu-id="eaa13-268">10000</span><span class="sxs-lookup"><span data-stu-id="eaa13-268">10000</span></span> |<span data-ttu-id="eaa13-269">21605</span><span class="sxs-lookup"><span data-stu-id="eaa13-269">21605</span></span> |<span data-ttu-id="eaa13-270">2737</span><span class="sxs-lookup"><span data-stu-id="eaa13-270">2737</span></span> |

> [!NOTE]
> <span data-ttu-id="eaa13-271">Sonuçları kıyaslamaları değildir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-271">Results are not benchmarks.</span></span> <span data-ttu-id="eaa13-272">Merhaba bkz [bu konudaki zamanlama sonuçlarıyla ilgili Not](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="eaa13-272">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="eaa13-273">Daha küçük toplu boyutlarında hello kullan tablo değerli parametreleri outperformed hello **SqlBulkCopy** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="eaa13-273">In smaller batch sizes, hello use table-valued parameters outperformed hello **SqlBulkCopy** class.</span></span> <span data-ttu-id="eaa13-274">Ancak, **SqlBulkCopy** 12-%31 tablo değerli parametreleri daha hızlı gerçekleştirilen 1.000 ile 10.000 satırları hello testler için.</span><span class="sxs-lookup"><span data-stu-id="eaa13-274">However, **SqlBulkCopy** performed 12-31% faster than table-valued parameters for hello tests of 1,000 and 10,000 rows.</span></span> <span data-ttu-id="eaa13-275">Tablo değerli parametreleri gibi **SqlBulkCopy** özellikle karşılaştırıldığında toplu eklemeleri için iyi bir seçenek olan toplu olmayan işlemlerinin toohello performansını.</span><span class="sxs-lookup"><span data-stu-id="eaa13-275">Like table-valued parameters, **SqlBulkCopy** is a good option for batched inserts, especially when compared toohello performance of non-batched operations.</span></span>

<span data-ttu-id="eaa13-276">ADO.NET toplu kopyalama hakkında daha fazla bilgi için bkz: [SQL Server toplu kopyalama işlemleri](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span><span class="sxs-lookup"><span data-stu-id="eaa13-276">For more information on bulk copy in ADO.NET, see [Bulk Copy Operations in SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span></span>

### <a name="multiple-row-parameterized-insert-statements"></a><span data-ttu-id="eaa13-277">Birden çok satır parametreli INSERT deyimleri</span><span class="sxs-lookup"><span data-stu-id="eaa13-277">Multiple-row Parameterized INSERT statements</span></span>
<span data-ttu-id="eaa13-278">Bir küçük toplu işlemler için birden çok satır ekleyen INSERT deyimi tooconstruct büyük parametreli alternatiftir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-278">One alternative for small batches is tooconstruct a large parameterized INSERT statement that inserts multiple rows.</span></span> <span data-ttu-id="eaa13-279">Aşağıdaki kod örneğine Merhaba, bu tekniği gösterir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-279">hello following code example demonstrates this technique.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        string insertCommand = "INSERT INTO [MyTable] ( mytext, num ) " +
            "VALUES (@p1, @p2), (@p3, @p4), (@p5, @p6), (@p7, @p8), (@p9, @p10)";

        SqlCommand cmd = new SqlCommand(insertCommand, connection);

        for (int i = 1; i <= 10; i += 2)
        {
            cmd.Parameters.Add(new SqlParameter("@p" + i.ToString(), "test"));
            cmd.Parameters.Add(new SqlParameter("@p" + (i+1).ToString(), i));
        }

        cmd.ExecuteNonQuery();
    }


<span data-ttu-id="eaa13-280">Bu örnek tooshow hello temel kavram amaçlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-280">This example is meant tooshow hello basic concept.</span></span> <span data-ttu-id="eaa13-281">Daha gerçekçi bir senaryo hello komut parametreleri gerekli hello varlıklar tooconstruct hello sorgu dizesi ile aynı anda döngüsü.</span><span class="sxs-lookup"><span data-stu-id="eaa13-281">A more realistic scenario would loop through hello required entities tooconstruct hello query string and hello command parameters simultaneously.</span></span> <span data-ttu-id="eaa13-282">Sınırlı tooa toplam 2100 sorgu parametreleri, böylece bu hello bu şekilde işlenebilir satırların toplam sayısını sınırlar.</span><span class="sxs-lookup"><span data-stu-id="eaa13-282">You are limited tooa total of 2100 query parameters, so this limits hello total number of rows that can be processed in this manner.</span></span>

<span data-ttu-id="eaa13-283">Bu tür milisaniye cinsinden INSERT deyiminin geçici test sonuçları göster hello performans aşağıdaki hello.</span><span class="sxs-lookup"><span data-stu-id="eaa13-283">hello following ad-hoc test results show hello performance of this type of insert statement in milliseconds.</span></span>

| <span data-ttu-id="eaa13-284">İşlemler</span><span class="sxs-lookup"><span data-stu-id="eaa13-284">Operations</span></span> | <span data-ttu-id="eaa13-285">Tablo değerli parametreleri (ms)</span><span class="sxs-lookup"><span data-stu-id="eaa13-285">Table-valued parameters (ms)</span></span> | <span data-ttu-id="eaa13-286">Tek deyimli Ekle (ms)</span><span class="sxs-lookup"><span data-stu-id="eaa13-286">Single-statement INSERT (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eaa13-287">1</span><span class="sxs-lookup"><span data-stu-id="eaa13-287">1</span></span> |<span data-ttu-id="eaa13-288">32</span><span class="sxs-lookup"><span data-stu-id="eaa13-288">32</span></span> |<span data-ttu-id="eaa13-289">20</span><span class="sxs-lookup"><span data-stu-id="eaa13-289">20</span></span> |
| <span data-ttu-id="eaa13-290">10</span><span class="sxs-lookup"><span data-stu-id="eaa13-290">10</span></span> |<span data-ttu-id="eaa13-291">30</span><span class="sxs-lookup"><span data-stu-id="eaa13-291">30</span></span> |<span data-ttu-id="eaa13-292">25</span><span class="sxs-lookup"><span data-stu-id="eaa13-292">25</span></span> |
| <span data-ttu-id="eaa13-293">100</span><span class="sxs-lookup"><span data-stu-id="eaa13-293">100</span></span> |<span data-ttu-id="eaa13-294">33</span><span class="sxs-lookup"><span data-stu-id="eaa13-294">33</span></span> |<span data-ttu-id="eaa13-295">51</span><span class="sxs-lookup"><span data-stu-id="eaa13-295">51</span></span> |

> [!NOTE]
> <span data-ttu-id="eaa13-296">Sonuçları kıyaslamaları değildir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-296">Results are not benchmarks.</span></span> <span data-ttu-id="eaa13-297">Merhaba bkz [bu konudaki zamanlama sonuçlarıyla ilgili Not](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="eaa13-297">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="eaa13-298">Bu yaklaşım, 100'den az satırlar toplu işlemler için biraz daha hızlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-298">This approach can be slightly faster for batches that are less than 100 rows.</span></span> <span data-ttu-id="eaa13-299">Merhaba geliştirme küçük olsa da, bu teknik iyi belirli uygulama senaryonuz çalışabilir başka bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-299">Although hello improvement is small, this technique is another option that might work well in your specific application scenario.</span></span>

### <a name="dataadapter"></a><span data-ttu-id="eaa13-300">DataAdapter</span><span class="sxs-lookup"><span data-stu-id="eaa13-300">DataAdapter</span></span>
<span data-ttu-id="eaa13-301">Merhaba **DataAdapter** sınıfı toomodify verir bir **DataSet** nesne ve hello değişiklikleri INSERT, UPDATE ve DELETE işlemleri olarak gönderin.</span><span class="sxs-lookup"><span data-stu-id="eaa13-301">hello **DataAdapter** class allows you toomodify a **DataSet** object and then submit hello changes as INSERT, UPDATE, and DELETE operations.</span></span> <span data-ttu-id="eaa13-302">Merhaba kullanıyorsanız **DataAdapter** bu şekilde, çağrıları ayrı toonote her ayrı bir işlem için yapılan önemlidir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-302">If you are using hello **DataAdapter** in this manner, it is important toonote that separate calls are made for each distinct operation.</span></span> <span data-ttu-id="eaa13-303">tooimprove performansı, kullanım hello **UpdateBatchSize** özelliği toohello aynı anda toplu işlem sayısı.</span><span class="sxs-lookup"><span data-stu-id="eaa13-303">tooimprove performance, use hello **UpdateBatchSize** property toohello number of operations that should be batched at a time.</span></span> <span data-ttu-id="eaa13-304">Daha fazla bilgi için bkz: [toplu işlemleri kullanarak DataAdapters gerçekleştirme](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span><span class="sxs-lookup"><span data-stu-id="eaa13-304">For more information, see [Performing Batch Operations Using DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span></span>

### <a name="entity-framework"></a><span data-ttu-id="eaa13-305">Varlık çerçevesi</span><span class="sxs-lookup"><span data-stu-id="eaa13-305">Entity framework</span></span>
<span data-ttu-id="eaa13-306">Toplu işleme Entity Framework şu anda desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="eaa13-306">Entity Framework does not currently support batching.</span></span> <span data-ttu-id="eaa13-307">Merhaba topluluğundaki farklı geliştiriciler geçersiz kılma hello gibi toodemonstrate geçici çözümler çalıştı **SaveChanges** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="eaa13-307">Different developers in hello community have attempted toodemonstrate workarounds, such as override hello **SaveChanges** method.</span></span> <span data-ttu-id="eaa13-308">Ancak hello çözümler genellikle karmaşık ve özelleştirilmiş toohello uygulama ve veri modeli.</span><span class="sxs-lookup"><span data-stu-id="eaa13-308">But hello solutions are typically complex and customized toohello application and data model.</span></span> <span data-ttu-id="eaa13-309">Hello Entity Framework codeplex proje şu anda bu özellik isteğinde tartışma sayfa yok.</span><span class="sxs-lookup"><span data-stu-id="eaa13-309">hello Entity Framework codeplex project currently has a discussion page on this feature request.</span></span> <span data-ttu-id="eaa13-310">tooview bu tartışma bkz [tasarım Toplantı Notları - 2 Ağustos 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span><span class="sxs-lookup"><span data-stu-id="eaa13-310">tooview this discussion, see [Design Meeting Notes - August 2, 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span></span>

### <a name="xml"></a><span data-ttu-id="eaa13-311">XML</span><span class="sxs-lookup"><span data-stu-id="eaa13-311">XML</span></span>
<span data-ttu-id="eaa13-312">Eksiksiz olması için bir toplu stratejisi olarak XML hakkında önemli tootalk olduğunu düşündüğünüz.</span><span class="sxs-lookup"><span data-stu-id="eaa13-312">For completeness, we feel that it is important tootalk about XML as a batching strategy.</span></span> <span data-ttu-id="eaa13-313">Ancak, XML hello kullanımını diğer yöntemleri hiçbir avantajları ve birkaç dezavantajları vardır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-313">However, hello use of XML has no advantages over other methods and several disadvantages.</span></span> <span data-ttu-id="eaa13-314">Merhaba yaklaşım, benzer tootable değerli parametreleri olmakla birlikte bir XML dosyası veya dize tooa depolanan yordamı kullanıcı tanımlı bir tablo yerine geçirilir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-314">hello approach is similar tootable-valued parameters, but an XML file or string is passed tooa stored procedure instead of a user-defined table.</span></span> <span data-ttu-id="eaa13-315">Merhaba saklı yordamı hello saklı yordamı hello komutlarda ayrıştırır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-315">hello stored procedure parses hello commands in hello stored procedure.</span></span>

<span data-ttu-id="eaa13-316">Toothis yaklaşım birkaç dezavantajları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="eaa13-316">There are several disadvantages toothis approach:</span></span>

* <span data-ttu-id="eaa13-317">XML ile çalışma sıkıcı olabilir ve hataya.</span><span class="sxs-lookup"><span data-stu-id="eaa13-317">Working with XML can be cumbersome and error prone.</span></span>
* <span data-ttu-id="eaa13-318">Merhaba veritabanı hello XML ayrıştırma, yoğun CPU kullanımına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-318">Parsing hello XML on hello database can be CPU-intensive.</span></span>
* <span data-ttu-id="eaa13-319">Çoğu durumda, bu yöntem tablo değerli parametreleri yavaştır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-319">In most cases, this method is slower than table-valued parameters.</span></span>

<span data-ttu-id="eaa13-320">Bu nedenlerle, toplu sorgular için XML hello kullanılması önerilmez.</span><span class="sxs-lookup"><span data-stu-id="eaa13-320">For these reasons, hello use of XML for batch queries is not recommended.</span></span>

## <a name="batching-considerations"></a><span data-ttu-id="eaa13-321">Dikkat edilecek noktalar toplu işleme</span><span class="sxs-lookup"><span data-stu-id="eaa13-321">Batching considerations</span></span>
<span data-ttu-id="eaa13-322">Aşağıdaki bölümlerde hello hello kullanımıyla SQL veritabanı uygulamalarında toplu işleme için daha fazla rehberlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="eaa13-322">hello following sections provide more guidance for hello use of batching in SQL Database applications.</span></span>

### <a name="tradeoffs"></a><span data-ttu-id="eaa13-323">Bileşim</span><span class="sxs-lookup"><span data-stu-id="eaa13-323">Tradeoffs</span></span>
<span data-ttu-id="eaa13-324">Mimarinizi bağlı olarak, toplu işleme kolaylığını performans ve dayanıklılık arasındaki içerebilir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-324">Depending on your architecture, batching can involve a tradeoff between performance and resiliency.</span></span> <span data-ttu-id="eaa13-325">Örneğin, burada rolünüze beklenmedik bir şekilde arıza hello senaryoyu göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="eaa13-325">For example, consider hello scenario where your role unexpectedly goes down.</span></span> <span data-ttu-id="eaa13-326">Bir veri satırı kaybederseniz, hello gönderilmeyen satırları büyük toplu kaybetme hello etkisi küçük etkisidir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-326">If you lose one row of data, hello impact is smaller than hello impact of losing a large batch of unsubmitted rows.</span></span> <span data-ttu-id="eaa13-327">Belirtilen zaman penceresi için toohello veritabanı göndermeden satırları arabellek yapıldığında büyük bir risk alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="eaa13-327">There is a greater risk when you buffer rows before sending them toohello database in a specified time window.</span></span>

<span data-ttu-id="eaa13-328">Bu kolaylığını nedeniyle, toplu işlemler hello türünü değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="eaa13-328">Because of this tradeoff, evaluate hello type of operations that you batch.</span></span> <span data-ttu-id="eaa13-329">Daha agresif toplu (büyük toplu işlemler ve daha uzun zaman pencereleri) verilerle daha az önemlidir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-329">Batch more aggressively (larger batches and longer time windows) with data that is less critical.</span></span>

### <a name="batch-size"></a><span data-ttu-id="eaa13-330">Toplu iş boyutu</span><span class="sxs-lookup"><span data-stu-id="eaa13-330">Batch size</span></span>
<span data-ttu-id="eaa13-331">Bizim testlerinde genellikle hiçbir avantajı toobreaking büyük toplu işlemleri daha küçük parçalara vardı.</span><span class="sxs-lookup"><span data-stu-id="eaa13-331">In our tests, there was typically no advantage toobreaking large batches into smaller chunks.</span></span> <span data-ttu-id="eaa13-332">Aslında, bu alt bölümü genellikle tek bir büyük toplu iş gönderme daha yavaş performans ile sonuçlandı.</span><span class="sxs-lookup"><span data-stu-id="eaa13-332">In fact, this subdivision often resulted in slower performance than submitting a single large batch.</span></span> <span data-ttu-id="eaa13-333">Örneğin, tooinsert 1000 satırı istediğiniz bir senaryo düşünün.</span><span class="sxs-lookup"><span data-stu-id="eaa13-333">For example, consider a scenario where you want tooinsert 1000 rows.</span></span> <span data-ttu-id="eaa13-334">Merhaba aşağıdaki tabloda toouse tablo değerli parametreleri küçük yığınlara bölünmüş zaman tooinsert 1000 satırları süreyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-334">hello following table shows how long it takes toouse table-valued parameters tooinsert 1000 rows when divided into smaller batches.</span></span>

| <span data-ttu-id="eaa13-335">Toplu iş boyutu</span><span class="sxs-lookup"><span data-stu-id="eaa13-335">Batch size</span></span> | <span data-ttu-id="eaa13-336">Yineleme</span><span class="sxs-lookup"><span data-stu-id="eaa13-336">Iterations</span></span> | <span data-ttu-id="eaa13-337">Tablo değerli parametreleri (ms)</span><span class="sxs-lookup"><span data-stu-id="eaa13-337">Table-valued parameters (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eaa13-338">1000</span><span class="sxs-lookup"><span data-stu-id="eaa13-338">1000</span></span> |<span data-ttu-id="eaa13-339">1</span><span class="sxs-lookup"><span data-stu-id="eaa13-339">1</span></span> |<span data-ttu-id="eaa13-340">347</span><span class="sxs-lookup"><span data-stu-id="eaa13-340">347</span></span> |
| <span data-ttu-id="eaa13-341">500</span><span class="sxs-lookup"><span data-stu-id="eaa13-341">500</span></span> |<span data-ttu-id="eaa13-342">2</span><span class="sxs-lookup"><span data-stu-id="eaa13-342">2</span></span> |<span data-ttu-id="eaa13-343">355</span><span class="sxs-lookup"><span data-stu-id="eaa13-343">355</span></span> |
| <span data-ttu-id="eaa13-344">100</span><span class="sxs-lookup"><span data-stu-id="eaa13-344">100</span></span> |<span data-ttu-id="eaa13-345">10</span><span class="sxs-lookup"><span data-stu-id="eaa13-345">10</span></span> |<span data-ttu-id="eaa13-346">465</span><span class="sxs-lookup"><span data-stu-id="eaa13-346">465</span></span> |
| <span data-ttu-id="eaa13-347">50</span><span class="sxs-lookup"><span data-stu-id="eaa13-347">50</span></span> |<span data-ttu-id="eaa13-348">20</span><span class="sxs-lookup"><span data-stu-id="eaa13-348">20</span></span> |<span data-ttu-id="eaa13-349">630</span><span class="sxs-lookup"><span data-stu-id="eaa13-349">630</span></span> |

> [!NOTE]
> <span data-ttu-id="eaa13-350">Sonuçları kıyaslamaları değildir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-350">Results are not benchmarks.</span></span> <span data-ttu-id="eaa13-351">Merhaba bkz [bu konudaki zamanlama sonuçlarıyla ilgili Not](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="eaa13-351">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="eaa13-352">Merhaba en iyi performans için 1000 satırı toosubmit olduğunu görebilirsiniz tümünü.</span><span class="sxs-lookup"><span data-stu-id="eaa13-352">You can see that hello best performance for 1000 rows is toosubmit them all at once.</span></span> <span data-ttu-id="eaa13-353">(Burada gösterilmiyor) diğer testlerinde 5000 iki toplu 10000 satır toplu küçük performans kazancı toobreak vardı.</span><span class="sxs-lookup"><span data-stu-id="eaa13-353">In other tests (not shown here) there was a small performance gain toobreak a 10000 row batch into two batches of 5000.</span></span> <span data-ttu-id="eaa13-354">Ancak hello tablo şemasını bu testler için oldukça basittir, gerçekleştirmesi gereken şekilde, belirli veri ve toplu iş boyutu tooverify bu bulgularını sınar.</span><span class="sxs-lookup"><span data-stu-id="eaa13-354">But hello table schema for these tests is relatively simple, so you should perform tests on your specific data and batch sizes tooverify these findings.</span></span>

<span data-ttu-id="eaa13-355">Başka bir faktör tooconsider hello toplam toplu iş çok büyük olursa, SQL veritabanı azaltma ve toocommit hello toplu Reddet olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-355">Another factor tooconsider is that if hello total batch becomes too large, SQL Database might throttle and refuse toocommit hello batch.</span></span> <span data-ttu-id="eaa13-356">İdeal toplu iş boyutu ise hello en iyi sonuçlar için belirli bir senaryoyu toodetermine sınayın.</span><span class="sxs-lookup"><span data-stu-id="eaa13-356">For hello best results, test your specific scenario toodetermine if there is an ideal batch size.</span></span> <span data-ttu-id="eaa13-357">Merhaba toplu iş boyutu performans veya hatalar göre çalışma zamanı tooenable hızlı ayarlamalar adresindeki yapılandırılabilir olun.</span><span class="sxs-lookup"><span data-stu-id="eaa13-357">Make hello batch size configurable at runtime tooenable quick adjustments based on performance or errors.</span></span>

<span data-ttu-id="eaa13-358">Son olarak, toplu işleme ile ilişkili hello riskleri ile Merhaba toplu iş boyutu hello dengeleyin.</span><span class="sxs-lookup"><span data-stu-id="eaa13-358">Finally, balance hello size of hello batch with hello risks associated with batching.</span></span> <span data-ttu-id="eaa13-359">Geçici bir hata veya hello rol başarısız olursa hello sonuçlarıyla hello işlemi yeniden denemeden veya hello toplu hello veri kaybı göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="eaa13-359">If there are transient errors or hello role fails, consider hello consequences of retrying hello operation or of losing hello data in hello batch.</span></span>

### <a name="parallel-processing"></a><span data-ttu-id="eaa13-360">Paralel işleme</span><span class="sxs-lookup"><span data-stu-id="eaa13-360">Parallel processing</span></span>
<span data-ttu-id="eaa13-361">Ne hello toplu iş boyutunu azaltma hello yaklaşım sürdü ancak çoklu iş parçacığı tooexecute hello iş kullanılan?</span><span class="sxs-lookup"><span data-stu-id="eaa13-361">What if you took hello approach of reducing hello batch size but used multiple threads tooexecute hello work?</span></span> <span data-ttu-id="eaa13-362">Yeniden testlerimizde birkaç küçük birden çok iş parçacıklı toplu işlemi genellikle tek bir büyük toplu daha da kötüsü gerçekleştirdiği gösterdi.</span><span class="sxs-lookup"><span data-stu-id="eaa13-362">Again, our tests showed that several smaller multithreaded batches typically performed worse than a single larger batch.</span></span> <span data-ttu-id="eaa13-363">Merhaba aşağıdaki test bir veya daha fazla paralel yığınlardaki tooinsert 1000 satırı çalışır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-363">hello following test attempts tooinsert 1000 rows in one or more parallel batches.</span></span> <span data-ttu-id="eaa13-364">Bu test nasıl daha fazla eşzamanlı toplu gerçekte performansı düşebilir gösterir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-364">This test shows how more simultaneous batches actually decreased performance.</span></span>

| <span data-ttu-id="eaa13-365">Toplu iş boyutu [yineleme]</span><span class="sxs-lookup"><span data-stu-id="eaa13-365">Batch size [Iterations]</span></span> | <span data-ttu-id="eaa13-366">İki iş parçacığı (ms)</span><span class="sxs-lookup"><span data-stu-id="eaa13-366">Two threads (ms)</span></span> | <span data-ttu-id="eaa13-367">Dört iş parçacığı (ms)</span><span class="sxs-lookup"><span data-stu-id="eaa13-367">Four threads (ms)</span></span> | <span data-ttu-id="eaa13-368">Altı iş parçacıkları (ms)</span><span class="sxs-lookup"><span data-stu-id="eaa13-368">Six threads (ms)</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eaa13-369">1000 [1]</span><span class="sxs-lookup"><span data-stu-id="eaa13-369">1000 [1]</span></span> |<span data-ttu-id="eaa13-370">277</span><span class="sxs-lookup"><span data-stu-id="eaa13-370">277</span></span> |<span data-ttu-id="eaa13-371">315</span><span class="sxs-lookup"><span data-stu-id="eaa13-371">315</span></span> |<span data-ttu-id="eaa13-372">266</span><span class="sxs-lookup"><span data-stu-id="eaa13-372">266</span></span> |
| <span data-ttu-id="eaa13-373">500 [2]</span><span class="sxs-lookup"><span data-stu-id="eaa13-373">500 [2]</span></span> |<span data-ttu-id="eaa13-374">548</span><span class="sxs-lookup"><span data-stu-id="eaa13-374">548</span></span> |<span data-ttu-id="eaa13-375">278</span><span class="sxs-lookup"><span data-stu-id="eaa13-375">278</span></span> |<span data-ttu-id="eaa13-376">256</span><span class="sxs-lookup"><span data-stu-id="eaa13-376">256</span></span> |
| <span data-ttu-id="eaa13-377">250 [4]</span><span class="sxs-lookup"><span data-stu-id="eaa13-377">250 [4]</span></span> |<span data-ttu-id="eaa13-378">405</span><span class="sxs-lookup"><span data-stu-id="eaa13-378">405</span></span> |<span data-ttu-id="eaa13-379">329</span><span class="sxs-lookup"><span data-stu-id="eaa13-379">329</span></span> |<span data-ttu-id="eaa13-380">265</span><span class="sxs-lookup"><span data-stu-id="eaa13-380">265</span></span> |
| <span data-ttu-id="eaa13-381">100 [10]</span><span class="sxs-lookup"><span data-stu-id="eaa13-381">100 [10]</span></span> |<span data-ttu-id="eaa13-382">488</span><span class="sxs-lookup"><span data-stu-id="eaa13-382">488</span></span> |<span data-ttu-id="eaa13-383">439</span><span class="sxs-lookup"><span data-stu-id="eaa13-383">439</span></span> |<span data-ttu-id="eaa13-384">391</span><span class="sxs-lookup"><span data-stu-id="eaa13-384">391</span></span> |

> [!NOTE]
> <span data-ttu-id="eaa13-385">Sonuçları kıyaslamaları değildir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-385">Results are not benchmarks.</span></span> <span data-ttu-id="eaa13-386">Merhaba bkz [bu konudaki zamanlama sonuçlarıyla ilgili Not](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="eaa13-386">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="eaa13-387">Performans düşüşü hello için birkaç olası nedeni vardır son tooparallelism:</span><span class="sxs-lookup"><span data-stu-id="eaa13-387">There are several potential reasons for hello degradation in performance due tooparallelism:</span></span>

* <span data-ttu-id="eaa13-388">Bir yerine birden çok eşzamanlı ağ çağrıları vardır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-388">There are multiple simultaneous network calls instead of one.</span></span>
* <span data-ttu-id="eaa13-389">Birden çok işlem tek bir tabloyu karşı Çekişme ve engelleme neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-389">Multiple operations against a single table can result in contention and blocking.</span></span>
* <span data-ttu-id="eaa13-390">İle ilişkili ek yüklerini vardır çoklu iş parçacığı kullanımı.</span><span class="sxs-lookup"><span data-stu-id="eaa13-390">There are overheads associated with multithreading.</span></span>
* <span data-ttu-id="eaa13-391">birden çok bağlantı açma hello gider paralel işleme hello yararı ağır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-391">hello expense of opening multiple connections outweighs hello benefit of parallel processing.</span></span>

<span data-ttu-id="eaa13-392">Farklı tablolar veya veritabanlarına hedef, bazı performans elde bu strateji ile olası toosee olur.</span><span class="sxs-lookup"><span data-stu-id="eaa13-392">If you target different tables or databases, it is possible toosee some performance gain with this strategy.</span></span> <span data-ttu-id="eaa13-393">Veritabanı parçalama veya Federasyon bir senaryo için bu yaklaşım olacaktır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-393">Database sharding or federations would be a scenario for this approach.</span></span> <span data-ttu-id="eaa13-394">Birden çok veritabanını ve yolları farklı veri tooeach veritabanı parçalama kullanır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-394">Sharding uses multiple databases and routes different data tooeach database.</span></span> <span data-ttu-id="eaa13-395">Her küçük bir toplu iş tooa farklı veritabanı olacaksa, ardından hello paralel işlemleri daha etkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-395">If each small batch is going tooa different database, then performing hello operations in parallel can be more efficient.</span></span> <span data-ttu-id="eaa13-396">Ancak, hello performans kazancı yeterince önemli toouse karar toouse veritabanı parçalama çözümünüzdeki hello temeli olarak değil.</span><span class="sxs-lookup"><span data-stu-id="eaa13-396">However, hello performance gain is not significant enough toouse as hello basis for a decision toouse database sharding in your solution.</span></span>

<span data-ttu-id="eaa13-397">Bazı tasarımları küçük toplu işlemlerin Paralel yürütme yük altında bir sistem isteklerin geliştirilmiş verimini sonuçlanabilir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-397">In some designs, parallel execution of smaller batches can result in improved throughput of requests in a system under load.</span></span> <span data-ttu-id="eaa13-398">Daha hızlı tooprocess tek bir büyük toplu olmasına karşın, bu durumda, birden çok toplu işlem paralel işleme daha etkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-398">In this case, even though it is quicker tooprocess a single larger batch, processing multiple batches in parallel might be more efficient.</span></span>

<span data-ttu-id="eaa13-399">Paralel yürütme kullanırsanız denetleme hello en fazla çalışan iş parçacığı sayısını göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="eaa13-399">If you do use parallel execution, consider controlling hello maximum number of worker threads.</span></span> <span data-ttu-id="eaa13-400">Daha küçük bir sayı çekişmelerinin azalmasını ve daha hızlı bir yürütme süresi neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-400">A smaller number might result in less contention and a faster execution time.</span></span> <span data-ttu-id="eaa13-401">Ayrıca, bu hello hedef veritabanı bağlantılarını ve işlemleri yerleştirir hello ek yük göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="eaa13-401">Also, consider hello additional load that this places on hello target database both in connections and transactions.</span></span>

### <a name="related-performance-factors"></a><span data-ttu-id="eaa13-402">İlgili performans Etkenler</span><span class="sxs-lookup"><span data-stu-id="eaa13-402">Related performance factors</span></span>
<span data-ttu-id="eaa13-403">Toplu işleme veritabanı performansını normal yönergeler de etkiler.</span><span class="sxs-lookup"><span data-stu-id="eaa13-403">Typical guidance on database performance also affects batching.</span></span> <span data-ttu-id="eaa13-404">Örneğin, INSERT performans büyük birincil bir anahtar veya birçok kümelenmemiş dizinlerine sahip tablolar için azaltılır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-404">For example, insert performance is reduced for tables that have a large primary key or many nonclustered indexes.</span></span>

<span data-ttu-id="eaa13-405">Tablo değerli parametreleri bir saklı yordam kullanırsanız, hello komutunu kullanabilirsiniz **SET NOCOUNT ON** hello başında hello yordamı.</span><span class="sxs-lookup"><span data-stu-id="eaa13-405">If table-valued parameters use a stored procedure, you can use hello command **SET NOCOUNT ON** at hello beginning of hello procedure.</span></span> <span data-ttu-id="eaa13-406">Bu bildirimi etkilenen hello satırların hello yordamdaki Merhaba sayımını hello dönüşünü gizler.</span><span class="sxs-lookup"><span data-stu-id="eaa13-406">This statement suppresses hello return of hello count of hello affected rows in hello procedure.</span></span> <span data-ttu-id="eaa13-407">Ancak, bizim testlerinde kullanımını hello **SET NOCOUNT ON** hiçbir etkisi olan ya da performansı düşebilir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-407">However, in our tests, hello use of **SET NOCOUNT ON** either had no effect or decreased performance.</span></span> <span data-ttu-id="eaa13-408">Merhaba test saklı yordamı ile tek bir basit **Ekle** hello tablo değerli parametre komutu.</span><span class="sxs-lookup"><span data-stu-id="eaa13-408">hello test stored procedure was simple with a single **INSERT** command from hello table-valued parameter.</span></span> <span data-ttu-id="eaa13-409">Daha karmaşık saklı yordamlar bu deyimden yararlanabileceğini mümkündür.</span><span class="sxs-lookup"><span data-stu-id="eaa13-409">It is possible that more complex stored procedures would benefit from this statement.</span></span> <span data-ttu-id="eaa13-410">Ancak bu ekleme varsaymayın **SET NOCOUNT ON** tooyour depolanan yordamı, otomatik olarak performansını artırır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-410">But don’t assume that adding **SET NOCOUNT ON** tooyour stored procedure automatically improves performance.</span></span> <span data-ttu-id="eaa13-411">toounderstand Merhaba etkisi, saklı yordam ve hello kullanılmadan test **SET NOCOUNT ON** deyimi.</span><span class="sxs-lookup"><span data-stu-id="eaa13-411">toounderstand hello effect, test your stored procedure with and without hello **SET NOCOUNT ON** statement.</span></span>

## <a name="batching-scenarios"></a><span data-ttu-id="eaa13-412">Toplu işleme senaryoları</span><span class="sxs-lookup"><span data-stu-id="eaa13-412">Batching scenarios</span></span>
<span data-ttu-id="eaa13-413">Merhaba aşağıdaki bölümlerde nasıl üç uygulama senaryolarında toouse tablo değerli parametreleri.</span><span class="sxs-lookup"><span data-stu-id="eaa13-413">hello following sections describe how toouse table-valued parameters in three application scenarios.</span></span> <span data-ttu-id="eaa13-414">Merhaba ilk senaryoda arabelleğe alma ve yığınlama birlikte nasıl çalışabileceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-414">hello first scenario shows how buffering and batching can work together.</span></span> <span data-ttu-id="eaa13-415">Merhaba ikinci senaryo, bir tek bir saklı yordam çağrısında ana-ayrıntı işlemleri gerçekleştirerek performansı artırır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-415">hello second scenario improves performance by performing master-detail operations in a single stored procedure call.</span></span> <span data-ttu-id="eaa13-416">Merhaba son senaryo gösterilmektedir nasıl toouse tablo değerli parametre bir "UPSERT" işlemi.</span><span class="sxs-lookup"><span data-stu-id="eaa13-416">hello final scenario shows how toouse table-valued parameters in an “UPSERT” operation.</span></span>

### <a name="buffering"></a><span data-ttu-id="eaa13-417">Arabelleğe alma</span><span class="sxs-lookup"><span data-stu-id="eaa13-417">Buffering</span></span>
<span data-ttu-id="eaa13-418">Toplu işleme için belirgin aday olan bazı senaryolar olsa da, Gecikmeli işlemesi toplu işleme avantajı ele geçirebilir birçok senaryo vardır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-418">Although there are some scenarios that are obvious candidate for batching, there are many scenarios that could take advantage of batching by delayed processing.</span></span> <span data-ttu-id="eaa13-419">Ancak, aynı zamanda Gecikmeli işleme beklenmeyen bir hata hello olayda hello veri kaybı büyük bir risk taşır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-419">However, delayed processing also carries a greater risk that hello data is lost in hello event of an unexpected failure.</span></span> <span data-ttu-id="eaa13-420">Önemli toounderstand bu riskidir ve hello sonuçlarıyla göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="eaa13-420">It is important toounderstand this risk and consider hello consequences.</span></span>

<span data-ttu-id="eaa13-421">Örneğin, her kullanıcı hello Gezinti geçmişini izler bir web uygulaması göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="eaa13-421">For example, consider a web application that tracks hello navigation history of each user.</span></span> <span data-ttu-id="eaa13-422">Her sayfa isteğinde Merhaba uygulaması bir veritabanı çağrısı toorecord hello kullanıcının sayfa görünümü hale getirebilir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-422">On each page request, hello application could make a database call toorecord hello user’s page view.</span></span> <span data-ttu-id="eaa13-423">Ancak daha yüksek performans ve ölçeklenebilirlik hello kullanıcıların Gezinti etkinlikleri arabelleğe alma ve ardından bu verileri toohello veritabanı toplu olarak gönderilmesi tarafından gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-423">But higher performance and scalability can be achieved by buffering hello users’ navigation activities and then sending this data toohello database in batches.</span></span> <span data-ttu-id="eaa13-424">Geçen süre ve/veya arabellek boyutu tarafından hello veritabanı güncelleştirmeleri tetikleyebilir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-424">You can trigger hello database update by elapsed time and/or buffer size.</span></span> <span data-ttu-id="eaa13-425">Örneğin, bir kural hello toplu sonra 20 saniye veya hello arabellek 1000 öğeleri ulaştığında işlenmesi gerektiğini belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eaa13-425">For example, a rule could specify that hello batch should be processed after 20 seconds or when hello buffer reaches 1000 items.</span></span>

<span data-ttu-id="eaa13-426">Merhaba aşağıdaki kod örneğinde [reaktif uzantılar - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess arabelleğe alınmış izleme sınıfı tarafından başlatılan olayları.</span><span class="sxs-lookup"><span data-stu-id="eaa13-426">hello following code example uses [Reactive Extensions - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess buffered events raised by a monitoring class.</span></span> <span data-ttu-id="eaa13-427">Ne zaman arabellek dolgular Merhaba veya bir zaman aşımı ulaşıldığında, kullanıcı verilerini hello toplu toohello veritabanı tablo değerli bir parametre ile gönderilir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-427">When hello buffer fills or a timeout is reached, hello batch of user data is sent toohello database with a table-valued parameter.</span></span>

<span data-ttu-id="eaa13-428">Aşağıdaki NavHistoryData sınıfı modelleri hello kullanıcı Gezinti ayrıntılara hello.</span><span class="sxs-lookup"><span data-stu-id="eaa13-428">hello following NavHistoryData class models hello user navigation details.</span></span> <span data-ttu-id="eaa13-429">Merhaba kullanıcı tanımlayıcısı gibi temel bilgileri içeren, hello URL erişilen ve erişim zamanı hello.</span><span class="sxs-lookup"><span data-stu-id="eaa13-429">It contains basic information such as hello user identifier, hello URL accessed, and hello access time.</span></span>

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

<span data-ttu-id="eaa13-430">Merhaba NavHistoryDataMonitor sınıfı hello kullanıcı Gezinti veri toohello veritabanına arabelleğe almak için sorumludur.</span><span class="sxs-lookup"><span data-stu-id="eaa13-430">hello NavHistoryDataMonitor class is responsible for buffering hello user navigation data toohello database.</span></span> <span data-ttu-id="eaa13-431">Bir yöntemi, yükselterek yanıt RecordUserNavigationEntry içeren bir **OnAdded** olay.</span><span class="sxs-lookup"><span data-stu-id="eaa13-431">It contains a method, RecordUserNavigationEntry, which responds by raising an **OnAdded** event.</span></span> <span data-ttu-id="eaa13-432">Merhaba aşağıdaki kod Rx toocreate kullanan hello Oluşturucu mantığı hello olaya göre bir observable koleksiyonu gösterir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-432">hello following code shows hello constructor logic that uses Rx toocreate an observable collection based on hello event.</span></span> <span data-ttu-id="eaa13-433">Ardından toothis observable koleksiyonu hello arabellek yöntemiyle abone.</span><span class="sxs-lookup"><span data-stu-id="eaa13-433">It then subscribes toothis observable collection with hello Buffer method.</span></span> <span data-ttu-id="eaa13-434">Merhaba aşırı bu hello arabellek 20 dakikada veya 1000 girişleri gönderilmesi gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-434">hello overload specifies that hello buffer should be sent every 20 seconds or 1000 entries.</span></span>

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

<span data-ttu-id="eaa13-435">Merhaba işleyici arabelleğe hello öğelerin tümünü bir tablo değerli türüne dönüştürür ve ardından bu tür tooa depolanan yordamı işlemleri hello toplu geçirir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-435">hello handler converts all of hello buffered items into a table-valued type and then passes this type tooa stored procedure that processes hello batch.</span></span> <span data-ttu-id="eaa13-436">Merhaba aşağıdaki kod hello tam tanımı hello NavHistoryDataEventArgs ve hello NavHistoryDataMonitor sınıfları gösterir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-436">hello following code shows hello complete definition for both hello NavHistoryDataEventArgs and hello NavHistoryDataMonitor classes.</span></span>

    public class NavHistoryDataEventArgs : System.EventArgs
    {
        public NavHistoryDataEventArgs(NavHistoryData data) { Data = data; }
        public NavHistoryData Data { get; set; }
    }

    public class NavHistoryDataMonitor
    {
        public event EventHandler<NavHistoryDataEventArgs> OnAdded;

        public NavHistoryDataMonitor()
        {
            var observableData =
                Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

            observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
        }

        public void RecordUserNavigationEntry(NavHistoryData data)
        {    
            if (OnAdded != null)
                OnAdded(this, new NavHistoryDataEventArgs(data));
        }

        protected void Handler(IList<EventPattern<NavHistoryDataEventArgs>> items)
        {
            DataTable navHistoryBatch = new DataTable("NavigationHistoryBatch");
            navHistoryBatch.Columns.Add("UserId", typeof(int));
            navHistoryBatch.Columns.Add("URL", typeof(string));
            navHistoryBatch.Columns.Add("AccessTime", typeof(DateTime));
            foreach (EventPattern<NavHistoryDataEventArgs> item in items)
            {
                NavHistoryData data = item.EventArgs.Data;
                navHistoryBatch.Rows.Add(data.UserId, data.URL, data.AccessTime);
            }

            using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
            {
                connection.Open();

                SqlCommand cmd = new SqlCommand("sp_RecordUserNavigation", connection);
                cmd.CommandType = CommandType.StoredProcedure;

                cmd.Parameters.Add(
                    new SqlParameter()
                    {
                        ParameterName = "@NavHistoryBatch",
                        SqlDbType = SqlDbType.Structured,
                        TypeName = "NavigationHistoryTableType",
                        Value = navHistoryBatch,
                    });

                cmd.ExecuteNonQuery();
            }
        }
    }

<span data-ttu-id="eaa13-437">toouse Merhaba uygulaması arabelleğe alma Bu sınıf bir statik NavHistoryDataMonitor nesnesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="eaa13-437">toouse this buffering class, hello application creates a static NavHistoryDataMonitor object.</span></span> <span data-ttu-id="eaa13-438">Sayfasında, bir kullanıcının eriştiği her zaman hello uygulama hello NavHistoryDataMonitor.RecordUserNavigationEntry yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-438">Each time a user accesses a page, hello application calls hello NavHistoryDataMonitor.RecordUserNavigationEntry method.</span></span> <span data-ttu-id="eaa13-439">mantığı arabelleğe alma hello bu girişleri toohello veritabanı toplu olarak gönderilmesi care of tootake devam eder.</span><span class="sxs-lookup"><span data-stu-id="eaa13-439">hello buffering logic proceeds tootake care of sending these entries toohello database in batches.</span></span>

### <a name="master-detail"></a><span data-ttu-id="eaa13-440">Ana ayrıntısı</span><span class="sxs-lookup"><span data-stu-id="eaa13-440">Master detail</span></span>
<span data-ttu-id="eaa13-441">Tablo değerli parametreleri basit Ekle senaryoları için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-441">Table-valued parameters are useful for simple INSERT scenarios.</span></span> <span data-ttu-id="eaa13-442">Ancak, bir tablodaki birden çok içeren daha zorlu toobatch ekler olabilir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-442">However, it can be more challenging toobatch inserts that involve more than one table.</span></span> <span data-ttu-id="eaa13-443">Merhaba "ana/ayrıntı" senaryosu iyi bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-443">hello “master/detail” scenario is a good example.</span></span> <span data-ttu-id="eaa13-444">Merhaba ana tablo hello birincil varlık tanımlar.</span><span class="sxs-lookup"><span data-stu-id="eaa13-444">hello master table identifies hello primary entity.</span></span> <span data-ttu-id="eaa13-445">Bir veya daha fazla ayrıntı tabloları hello varlık hakkında daha fazla veri depolar.</span><span class="sxs-lookup"><span data-stu-id="eaa13-445">One or more detail tables store more data about hello entity.</span></span> <span data-ttu-id="eaa13-446">Bu senaryoda, yabancı anahtar ilişkileri hello ilişki ayrıntıları tooa benzersiz ana varlığın uygulayın.</span><span class="sxs-lookup"><span data-stu-id="eaa13-446">In this scenario, foreign key relationships enforce hello relationship of details tooa unique master entity.</span></span> <span data-ttu-id="eaa13-447">Bir PurchaseOrder tablosu ve onun ilişkili OrderDetail tablosu basitleştirilmiş bir sürümünü göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="eaa13-447">Consider a simplified version of a PurchaseOrder table and its associated OrderDetail table.</span></span> <span data-ttu-id="eaa13-448">Merhaba Transact-SQL aşağıdaki dört sütunlarla hello PurchaseOrder tablo oluşturur: OrderID, OrderDate, CustomerID ve durum.</span><span class="sxs-lookup"><span data-stu-id="eaa13-448">hello following Transact-SQL creates hello PurchaseOrder table with four columns: OrderID, OrderDate, CustomerID, and Status.</span></span>

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

<span data-ttu-id="eaa13-449">Her sipariş bir veya daha fazla ürün satın alma işlemleri içerir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-449">Each order contains one or more product purchases.</span></span> <span data-ttu-id="eaa13-450">Bu bilgiler hello PurchaseOrderDetail tabloda yakalanır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-450">This information is captured in hello PurchaseOrderDetail table.</span></span> <span data-ttu-id="eaa13-451">Transact-SQL aşağıdaki hello beş sütunlarla hello PurchaseOrderDetail tablo oluşturur: OrderID, OrderDetailID, ProductID, UnitPrice ve OrderQty.</span><span class="sxs-lookup"><span data-stu-id="eaa13-451">hello following Transact-SQL creates hello PurchaseOrderDetail table with five columns: OrderID, OrderDetailID, ProductID, UnitPrice, and OrderQty.</span></span>

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

<span data-ttu-id="eaa13-452">Merhaba OrderID hello PurchaseOrderDetail tablo sütununda bir sipariş hello PurchaseOrder tablosundan başvurmalıdır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-452">hello OrderID column in hello PurchaseOrderDetail table must reference an order from hello PurchaseOrder table.</span></span> <span data-ttu-id="eaa13-453">bir yabancı anahtar tanımını izleyen hello bu kısıtlamayı zorlar.</span><span class="sxs-lookup"><span data-stu-id="eaa13-453">hello following definition of a foreign key enforces this constraint.</span></span>

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

<span data-ttu-id="eaa13-454">Sipariş toouse tablo değerli parametreleri, her bir hedef tablo için bir kullanıcı tanımlı tablo türü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-454">In order toouse table-valued parameters, you must have one user-defined table type for each target table.</span></span>

    CREATE TYPE PurchaseOrderTableType AS TABLE 
    ( OrderID INT,
      OrderDate DATETIME,
      CustomerID INT,
      Status NVARCHAR(50) );
    GO

    CREATE TYPE PurchaseOrderDetailTableType AS TABLE 
    ( OrderID INT,
      ProductID INT,
      UnitPrice MONEY,
      OrderQty SMALLINT );
    GO

<span data-ttu-id="eaa13-455">Ardından, bu tür tabloları kabul eden bir saklı yordam tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="eaa13-455">Then define a stored procedure that accepts tables of these types.</span></span> <span data-ttu-id="eaa13-456">Bu yordam bir uygulama toolocally toplu tek bir çağrıda bir dizi siparişleri ve Sipariş ayrıntılarını verir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-456">This procedure allows an application toolocally batch a set of orders and order details in a single call.</span></span> <span data-ttu-id="eaa13-457">Merhaba aşağıdaki Transact-SQL hello tam saklı yordam bildirimi bu satın alma siparişi örneğin sağlar.</span><span class="sxs-lookup"><span data-stu-id="eaa13-457">hello following Transact-SQL provides hello complete stored procedure declaration for this purchase order example.</span></span>

    CREATE PROCEDURE sp_InsertOrdersBatch (
    @orders as PurchaseOrderTableType READONLY,
    @details as PurchaseOrderDetailTableType READONLY )
    AS
    SET NOCOUNT ON;

    -- Table that connects hello order identifiers in hello @orders
    -- table with hello actual order identifiers in hello PurchaseOrder table
    DECLARE @IdentityLink AS TABLE ( 
    SubmittedKey int, 
    ActualKey int, 
    RowNumber int identity(1,1)
    );

          -- Add new orders toohello PurchaseOrder table, storing hello actual
    -- order identifiers in hello @IdentityLink table   
    INSERT INTO PurchaseOrder ([OrderDate], [CustomerID], [Status])
    OUTPUT inserted.OrderID INTO @IdentityLink (ActualKey)
    SELECT [OrderDate], [CustomerID], [Status] FROM @orders ORDER BY OrderID;

    -- Match hello passed-in order identifiers with hello actual identifiers
    -- and complete hello @IdentityLink table for use with inserting hello details
    WITH OrderedRows As (
    SELECT OrderID, ROW_NUMBER () OVER (ORDER BY OrderID) As RowNumber 
    FROM @orders
    )
    UPDATE @IdentityLink SET SubmittedKey = M.OrderID
    FROM @IdentityLink L JOIN OrderedRows M ON L.RowNumber = M.RowNumber;

    -- Insert hello order details into hello PurchaseOrderDetail table, 
          -- using hello actual order identifiers of hello master table, PurchaseOrder
    INSERT INTO PurchaseOrderDetail (
    [OrderID],
    [ProductID],
    [UnitPrice],
    [OrderQty] )
    SELECT L.ActualKey, D.ProductID, D.UnitPrice, D.OrderQty
    FROM @details D
    JOIN @IdentityLink L ON L.SubmittedKey = D.OrderID;
    GO

<span data-ttu-id="eaa13-458">Bu örnekte, yerel olarak tanımlanan hello @IdentityLink tablo hello gerçek OrderID değerleri yeni eklenen hello satırlardan depolar.</span><span class="sxs-lookup"><span data-stu-id="eaa13-458">In this example, hello locally defined @IdentityLink table stores hello actual OrderID values from hello newly inserted rows.</span></span> <span data-ttu-id="eaa13-459">Bu sipariş tanımlayıcılar hello hello geçici OrderID değerlerinden farklı @orders ve @details tablo değerli parametreleri.</span><span class="sxs-lookup"><span data-stu-id="eaa13-459">These order identifiers are different from hello temporary OrderID values in hello @orders and @details table-valued parameters.</span></span> <span data-ttu-id="eaa13-460">Bu nedenle, hello @IdentityLink tablo ardından hello hello OrderID değerleri bağlanır @orders parametresi toohello hello PurchaseOrder tablosundaki hello yeni satırlar için gerçek OrderID değerler.</span><span class="sxs-lookup"><span data-stu-id="eaa13-460">For this reason, hello @IdentityLink table then connects hello OrderID values from hello @orders parameter toohello real OrderID values for hello new rows in hello PurchaseOrder table.</span></span> <span data-ttu-id="eaa13-461">Bu adımdan sonra hello @IdentityLink tablo hello ekleme hello sipariş ayrıntılarla kolaylaştırmak hello yabancı anahtar kısıtlaması karşılayan gerçek OrderID.</span><span class="sxs-lookup"><span data-stu-id="eaa13-461">After this step, hello @IdentityLink table can facilitate inserting hello order details with hello actual OrderID that satisfies hello foreign key constraint.</span></span>

<span data-ttu-id="eaa13-462">Bu saklı yordam, kod veya diğer Transact-SQL çağrıları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-462">This stored procedure can be used from code or from other Transact-SQL calls.</span></span> <span data-ttu-id="eaa13-463">Kod örneği için Bu raporda Hello tablo değerli parametreleri bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="eaa13-463">See hello table-valued parameters section of this paper for a code example.</span></span> <span data-ttu-id="eaa13-464">Transact-SQL aşağıdaki hello nasıl toocall hello sp_InsertOrdersBatch gösterir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-464">hello following Transact-SQL shows how toocall hello sp_InsertOrdersBatch.</span></span>

    declare @orders as PurchaseOrderTableType
    declare @details as PurchaseOrderDetailTableType

    INSERT @orders 
    ([OrderID], [OrderDate], [CustomerID], [Status])
    VALUES(1, '1/1/2013', 1125, 'Complete'),
    (2, '1/13/2013', 348, 'Processing'),
    (3, '1/12/2013', 2504, 'Shipped')

    INSERT @details
    ([OrderID], [ProductID], [UnitPrice], [OrderQty])
    VALUES(1, 10, $11.50, 1),
    (1, 12, $1.58, 1),
    (2, 23, $2.57, 2),
    (3, 4, $10.00, 1)

    exec sp_InsertOrdersBatch @orders, @details

<span data-ttu-id="eaa13-465">Bu çözüm, 1'den başlayan OrderID değerler kümesi her toplu toouse sağlar.</span><span class="sxs-lookup"><span data-stu-id="eaa13-465">This solution allows each batch toouse a set of OrderID values that begin at 1.</span></span> <span data-ttu-id="eaa13-466">Bu geçici OrderID değerleri hello toplu hello ilişkilerde açıklar ancak hello gerçek OrderID değerler hello ekleme işlemi hello aynı anda belirlenir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-466">These temporary OrderID values describe hello relationships in hello batch, but hello actual OrderID values are determined at hello time of hello insert operation.</span></span> <span data-ttu-id="eaa13-467">Merhaba önceki örnekte aynı deyimleri hello art arda çalıştırın ve hello veritabanında benzersiz siparişler oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="eaa13-467">You can run hello same statements in hello previous example repeatedly and generate unique orders in hello database.</span></span> <span data-ttu-id="eaa13-468">Bu nedenle, bu teknik toplu işleme kullanırken yinelenen siparişleri engelleyen daha fazla kod veya veritabanı mantığı eklemeyi düşünün.</span><span class="sxs-lookup"><span data-stu-id="eaa13-468">For this reason, consider adding more code or database logic that prevents duplicate orders when using this batching technique.</span></span>

<span data-ttu-id="eaa13-469">Bu örnek, tablo değerli parametreleri kullanarak ana / ayrıntı işlemleri gibi daha karmaşık veritabanı işlemleri toplu olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-469">This example demonstrates that even more complex database operations, such as master-detail operations, can be batched using table-valued parameters.</span></span>

### <a name="upsert"></a><span data-ttu-id="eaa13-470">UPSERT</span><span class="sxs-lookup"><span data-stu-id="eaa13-470">UPSERT</span></span>
<span data-ttu-id="eaa13-471">Başka bir toplu senaryo, aynı anda var olan satır ve ekleme yeni satırlar güncelleştirilmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-471">Another batching scenario involves simultaneously updating existing rows and inserting new rows.</span></span> <span data-ttu-id="eaa13-472">Bu işlem bazen başvurulan tooas bir "UPSERT" (güncelleştirme + Ekle) işlem olur.</span><span class="sxs-lookup"><span data-stu-id="eaa13-472">This operation is sometimes referred tooas an “UPSERT” (update + insert) operation.</span></span> <span data-ttu-id="eaa13-473">Ayrı çağrıları tooINSERT ve güncelleştirme yapmak yerine, hello MERGE deyiminin en uygun toothis bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-473">Rather than making separate calls tooINSERT and UPDATE, hello MERGE statement is best suited toothis task.</span></span> <span data-ttu-id="eaa13-474">Hello MERGE deyimi, hem INSERT işlemi ve tek bir çağrı işlemlerinde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="eaa13-474">hello MERGE statement can perform both insert and update operations in a single call.</span></span>

<span data-ttu-id="eaa13-475">Tablo değerli parametreleri hello MERGE deyimi tooperform güncelleştirmeleri ve eklemeleri ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-475">Table-valued parameters can be used with hello MERGE statement tooperform updates and inserts.</span></span> <span data-ttu-id="eaa13-476">Örneğin, sütunları aşağıdaki hello içeren basitleştirilmiş bir çalışan tablosunun göz önünde bulundurun: EmployeeID, FirstName, LastName, SocialSecurityNumber:</span><span class="sxs-lookup"><span data-stu-id="eaa13-476">For example, consider a simplified Employee table that contains hello following columns: EmployeeID, FirstName, LastName, SocialSecurityNumber:</span></span>

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

<span data-ttu-id="eaa13-477">Bu örnekte, bu hello SocialSecurityNumber benzersiz tooperform birden fazla çalışanı BİRLEŞTİRMESİ olan hello olgu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eaa13-477">In this example, you can use hello fact that hello SocialSecurityNumber is unique tooperform a MERGE of multiple employees.</span></span> <span data-ttu-id="eaa13-478">İlk olarak, hello kullanıcı tanımlı tablo türü oluşturun:</span><span class="sxs-lookup"><span data-stu-id="eaa13-478">First, create hello user-defined table type:</span></span>

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

<span data-ttu-id="eaa13-479">Ardından, bir saklı yordam oluşturmak veya kullanır MERGE deyimi tooperform hello güncelleştirme hello ve Ekle kod yazma.</span><span class="sxs-lookup"><span data-stu-id="eaa13-479">Next, create a stored procedure or write code that uses hello MERGE statement tooperform hello update and insert.</span></span> <span data-ttu-id="eaa13-480">Merhaba aşağıdaki örnek hello MERGE deyiminin bir tablo değerli parametre kullanır @employees, EmployeeTableType türünde.</span><span class="sxs-lookup"><span data-stu-id="eaa13-480">hello following example uses hello MERGE statement on a table-valued parameter, @employees, of type EmployeeTableType.</span></span> <span data-ttu-id="eaa13-481">Merhaba Merhaba içeriğine @employees tablo aşağıda gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="eaa13-481">hello contents of hello @employees table are not shown here.</span></span>

    MERGE Employee AS target
    USING (SELECT [FirstName], [LastName], [SocialSecurityNumber] FROM @employees) 
    AS source ([FirstName], [LastName], [SocialSecurityNumber])
    ON (target.[SocialSecurityNumber] = source.[SocialSecurityNumber])
    WHEN MATCHED THEN 
    UPDATE SET
    target.FirstName = source.FirstName, 
    target.LastName = source.LastName
    WHEN NOT MATCHED THEN
       INSERT ([FirstName], [LastName], [SocialSecurityNumber])
       VALUES (source.[FirstName], source.[LastName], source.[SocialSecurityNumber]);

<span data-ttu-id="eaa13-482">Daha fazla bilgi için hello belgeler ve örnekler hello MERGE deyimi için bkz.</span><span class="sxs-lookup"><span data-stu-id="eaa13-482">For more information, see hello documentation and examples for hello MERGE statement.</span></span> <span data-ttu-id="eaa13-483">Aynı iş birden çok adım gerçekleştirilebilir hello depolanmış yordam çağrısı ayrı ekleme ve güncelleştirme işlemleri ile rağmen hello MERGE deyimi daha verimli olur.</span><span class="sxs-lookup"><span data-stu-id="eaa13-483">Although hello same work could be performed in a multiple-step stored procedure call with separate INSERT and UPDATE operations, hello MERGE statement is more efficient.</span></span> <span data-ttu-id="eaa13-484">Veritabanı kod iki veritabanı çağrılarını ekleme ve güncelleştirme için gerek kalmadan doğrudan hello MERGE deyiminin kullanan Transact-SQL çağrıları de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eaa13-484">Database code can also construct Transact-SQL calls that use hello MERGE statement directly without requiring two database calls for INSERT and UPDATE.</span></span>

## <a name="recommendation-summary"></a><span data-ttu-id="eaa13-485">Öneri özeti</span><span class="sxs-lookup"><span data-stu-id="eaa13-485">Recommendation summary</span></span>
<span data-ttu-id="eaa13-486">Merhaba aşağıdaki listede bu konuda tartışılan önerileri toplu işleme hello bir özetini sunar:</span><span class="sxs-lookup"><span data-stu-id="eaa13-486">hello following list provides a summary of hello batching recommendations discussed in this topic:</span></span>

* <span data-ttu-id="eaa13-487">Arabelleğe alma ve tooincrease hello performansını ve ölçeklenebilirliğini SQL veritabanı uygulamaları yığınlama kullanın.</span><span class="sxs-lookup"><span data-stu-id="eaa13-487">Use buffering and batching tooincrease hello performance and scalability of SQL Database applications.</span></span>
* <span data-ttu-id="eaa13-488">Toplu işleme/arabelleğe alma ve dayanıklılık arasında Hello bileşim anlayın.</span><span class="sxs-lookup"><span data-stu-id="eaa13-488">Understand hello tradeoffs between batching/buffering and resiliency.</span></span> <span data-ttu-id="eaa13-489">Bir rol hata sırasında işlenmemiş bir toplu iş açısından kritik verilerin kaybı hello risk toplu işleme hello performans avantajı üstün olabilir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-489">During a role failure, hello risk of losing an unprocessed batch of business-critical data might outweigh hello performance benefit of batching.</span></span>
* <span data-ttu-id="eaa13-490">Tookeep tüm çağrıları toohello veritabanı bir tek veri merkezi tooreduce gecikme süresi içinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-490">Attempt tookeep all calls toohello database within a single datacenter tooreduce latency.</span></span>
* <span data-ttu-id="eaa13-491">Tek bir toplu teknik seçerseniz, tablo değerli parametreleri hello en iyi performans ve esneklik sunar.</span><span class="sxs-lookup"><span data-stu-id="eaa13-491">If you choose a single batching technique, table-valued parameters offer hello best performance and flexibility.</span></span>
* <span data-ttu-id="eaa13-492">Merhaba hızlı performans eklemek, aşağıdaki genel yönergeleri izleyin ancak senaryonuza test:</span><span class="sxs-lookup"><span data-stu-id="eaa13-492">For hello fastest insert performance, follow these general guidelines but test your scenario:</span></span>
  * <span data-ttu-id="eaa13-493">< 100 satır için tek bir parametreli Ekle komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="eaa13-493">For < 100 rows, use a single parameterized INSERT command.</span></span>
  * <span data-ttu-id="eaa13-494">< 1000 satırı için tablo değerli parametreleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="eaa13-494">For < 1000 rows, use table-valued parameters.</span></span>
  * <span data-ttu-id="eaa13-495">İçin > = 1000 satır SqlBulkCopy kullanın.</span><span class="sxs-lookup"><span data-stu-id="eaa13-495">For >= 1000 rows, use SqlBulkCopy.</span></span>
* <span data-ttu-id="eaa13-496">İçin güncelleştirme ve silme işlemleri, hello doğru işlemi hello tablo parametresinde her satırda belirler saklı yordam mantığı ile tablo değerli parametreleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="eaa13-496">For update and delete operations, use table-valued parameters with stored procedure logic that determines hello correct operation on each row in hello table parameter.</span></span>
* <span data-ttu-id="eaa13-497">Toplu iş boyutu yönergeleri:</span><span class="sxs-lookup"><span data-stu-id="eaa13-497">Batch size guidelines:</span></span>
  * <span data-ttu-id="eaa13-498">Uygulama ve iş gereksinimleri için anlamlı hello en büyük toplu iş boyutu kullanılır.</span><span class="sxs-lookup"><span data-stu-id="eaa13-498">Use hello largest batch sizes that make sense for your application and business requirements.</span></span>
  * <span data-ttu-id="eaa13-499">Bakiye hello performans büyük toplu geçici veya geri dönülemez hataları hello riskleri ile elde edilir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-499">Balance hello performance gain of large batches with hello risks of temporary or catastrophic failures.</span></span> <span data-ttu-id="eaa13-500">Yeniden deneme hello sonucu veya hello toplu hello veri kaybı nedir?</span><span class="sxs-lookup"><span data-stu-id="eaa13-500">What is hello consequence of retries or loss of hello data in hello batch?</span></span> 
  * <span data-ttu-id="eaa13-501">SQL veritabanı reddetmek değil, hello en büyük toplu iş boyutu tooverify sınayın.</span><span class="sxs-lookup"><span data-stu-id="eaa13-501">Test hello largest batch size tooverify that SQL Database does not reject it.</span></span>
  * <span data-ttu-id="eaa13-502">Bu denetim, hello toplu iş boyutu veya hello arabelleğe alma zaman penceresi gibi toplu işleme yapılandırma ayarları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="eaa13-502">Create configuration settings that control batching, such as hello batch size or hello buffering time window.</span></span> <span data-ttu-id="eaa13-503">Bu ayarları esneklik sağlar.</span><span class="sxs-lookup"><span data-stu-id="eaa13-503">These settings provide flexibility.</span></span> <span data-ttu-id="eaa13-504">Davranış üretim hello bulut hizmeti yeniden dağıtmadan toplu işleme hello değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eaa13-504">You can change hello batching behavior in production without redeploying hello cloud service.</span></span>
* <span data-ttu-id="eaa13-505">Bir veritabanı tek bir tabloda çalışmayabilir toplu işlemlerin Paralel yürütme kaçının.</span><span class="sxs-lookup"><span data-stu-id="eaa13-505">Avoid parallel execution of batches that operate on a single table in one database.</span></span> <span data-ttu-id="eaa13-506">Tek bir toplu toodivide birden fazla çalışan iş parçacıkları arasında seçerseniz, testler toodetermine hello ideal iş parçacığı sayısını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="eaa13-506">If you do choose toodivide a single batch across multiple worker threads, run tests toodetermine hello ideal number of threads.</span></span> <span data-ttu-id="eaa13-507">Belirtilmeyen bir eşik sonra daha fazla iş parçacığı performansını düşürebilir yerine onu artırın.</span><span class="sxs-lookup"><span data-stu-id="eaa13-507">After an unspecified threshold, more threads will decrease performance rather than increase it.</span></span>
* <span data-ttu-id="eaa13-508">Boyut ve daha fazla senaryoları için toplu işleme uygulamanın yolu sürede arabelleğe almayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="eaa13-508">Consider buffering on size and time as a way of implementing batching for more scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eaa13-509">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="eaa13-509">Next steps</span></span>
<span data-ttu-id="eaa13-510">Veritabanı tasarımını ve teknikleri kodlama toobatching ilişkisini üzerine odaklanan bu makalede, uygulama performansı ve ölçeklenebilirliği artırabilir.</span><span class="sxs-lookup"><span data-stu-id="eaa13-510">This article focused on how database design and coding techniques related toobatching can improve your application performance and scalability.</span></span> <span data-ttu-id="eaa13-511">Ancak bu yalnızca bir faktör olarak genel stratejinize.</span><span class="sxs-lookup"><span data-stu-id="eaa13-511">But this is just one factor in your overall strategy.</span></span> <span data-ttu-id="eaa13-512">Daha fazla yol tooimprove performans ve ölçeklenebilirlik için bkz: [tek veritabanları için Azure SQL Database performans rehberi](sql-database-performance-guidance.md) ve [esnek havuzlar için fiyat ve performans konuları](sql-database-elastic-pool-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="eaa13-512">For more ways tooimprove performance and scalability, see [Azure SQL Database performance guidance for single databases](sql-database-performance-guidance.md) and [Price and performance considerations for an elastic pool](sql-database-elastic-pool-guidance.md).</span></span>

