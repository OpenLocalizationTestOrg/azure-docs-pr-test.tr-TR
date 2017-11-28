---
title: "SQL veri ambarı tablolarda aaaManaging istatistikleri | Microsoft Docs"
description: "Azure SQL Data Warehouse tablolarda istatistiklerle ile çalışmaya başlama."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: c9521dc47891f68d124e77a53e2e15d03275caaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-statistics-on-tables-in-sql-data-warehouse"></a><span data-ttu-id="49f56-103">SQL veri ambarı tablolarda istatistiklerle yönetme</span><span class="sxs-lookup"><span data-stu-id="49f56-103">Managing statistics on tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="49f56-104">[Genel bakış][Overview]</span><span class="sxs-lookup"><span data-stu-id="49f56-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="49f56-105">[Veri türleri][Data Types]</span><span class="sxs-lookup"><span data-stu-id="49f56-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="49f56-106">[Dağıt][Distribute]</span><span class="sxs-lookup"><span data-stu-id="49f56-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="49f56-107">[Dizin][Index]</span><span class="sxs-lookup"><span data-stu-id="49f56-107">[Index][Index]</span></span>
> * <span data-ttu-id="49f56-108">[Bölüm][Partition]</span><span class="sxs-lookup"><span data-stu-id="49f56-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="49f56-109">[İstatistikleri][Statistics]</span><span class="sxs-lookup"><span data-stu-id="49f56-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="49f56-110">[Geçici][Temporary]</span><span class="sxs-lookup"><span data-stu-id="49f56-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="49f56-111">Merhaba daha fazla SQL Data Warehouse bilir verilerinizle ilgili hello daha hızlı onu verilerinizi sorguları çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49f56-111">hello more SQL Data Warehouse knows about your data, hello faster it can execute queries against your data.</span></span>  <span data-ttu-id="49f56-112">SQL Data Warehouse verilerinizi hakkında söyleyen hello yoludur verilerinizle ilgili istatistikleri toplama tarafından.</span><span class="sxs-lookup"><span data-stu-id="49f56-112">hello way that you tell SQL Data Warehouse about your data, is by collecting statistics about your data.</span></span>  <span data-ttu-id="49f56-113">Verilerinize ilişkin istatistikler sahip bir olduğundan hello en önemli nokta sorgularınızı toooptimize yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49f56-113">Having statistics on your data is one of hello most important things you can do toooptimize your queries.</span></span>  <span data-ttu-id="49f56-114">İstatistikleri SQL Data Warehouse hello sorgularınızı için en iyi planı oluşturmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="49f56-114">Statistics help SQL Data Warehouse create hello most optimal plan for your queries.</span></span>  <span data-ttu-id="49f56-115">İyileştirici hello SQL Data Warehouse sorgu iyileştiricisi maliyetidir dayalı olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="49f56-115">This is because hello SQL Data Warehouse query optimizer is a cost based optimizer.</span></span>  <span data-ttu-id="49f56-116">Diğer bir deyişle, çeşitli sorgu planlarını hello maliyetini karşılaştırır ve ayrıca hello hızlı yürütecek hello planı olmalıdır hello en düşük maliyeti hello planla seçer.</span><span class="sxs-lookup"><span data-stu-id="49f56-116">That is, it compares hello cost of various query plans and then chooses hello plan with hello lowest cost, which should also be hello plan that will execute hello fastest.</span></span>

<span data-ttu-id="49f56-117">İstatistikleri, birden çok sütun tek bir sütun veya tablo dizini oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="49f56-117">Statistics can be created on a single column, multiple columns or on an index of a table.</span></span>  <span data-ttu-id="49f56-118">İstatistikleri hello aralığı ve değerlerin seçiciliği yakalar çubuk grafik içinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="49f56-118">Statistics are stored in a histogram which captures hello range and selectivity of values.</span></span>  <span data-ttu-id="49f56-119">İlginizi çeken budur Hello iyileştirici ihtiyacı olduğunda tooevaluate birleşimler, GROUP BY, HAVING ve WHERE sorgu yan tümcelerinde.</span><span class="sxs-lookup"><span data-stu-id="49f56-119">This is of particular interest when hello optimizer needs tooevaluate JOINs, GROUP BY, HAVING and WHERE clauses in a query.</span></span>  <span data-ttu-id="49f56-120">Hello iyileştirici tahminleri hello tarih sorgunuzda filtrelemeyi 1 satır döndürür, çok farklı planlama varsa daha da tercih edebilirsiniz örneğin, tarih, tahmin seçmiş 1 milyon satırları döndürür.</span><span class="sxs-lookup"><span data-stu-id="49f56-120">For example, if hello optimizer estimates that hello date you are filtering in your query will return 1 row, it may choose a very different plan than if it estimates that they date you have selected will return 1 million rows.</span></span>  <span data-ttu-id="49f56-121">İstatistik oluşturma oldukça önemli olmakla birlikte, eşit oranda önemli olan bu istatistikleri *doğru şekilde* Merhaba tablonun hello geçerli durumunu yansıtır.</span><span class="sxs-lookup"><span data-stu-id="49f56-121">While creating statistics is extremely important, it is equally important that statistics *accurately* reflect hello current state of hello table.</span></span>  <span data-ttu-id="49f56-122">Güncel istatistikleri olması iyi bir plan hello iyileştiricisi tarafından seçilir sağlar.</span><span class="sxs-lookup"><span data-stu-id="49f56-122">Having up-to-date statistics ensures that a good plan is selected by hello optimizer.</span></span>  <span data-ttu-id="49f56-123">Merhaba iyileştiricisi tarafından oluşturulan hello planlar yalnızca verilerinizi hello istatistik kadar iyi olur.</span><span class="sxs-lookup"><span data-stu-id="49f56-123">hello plans created by hello optimizer are only as good as hello statistics on your data.</span></span>

<span data-ttu-id="49f56-124">oluşturma ve istatistikleri güncelleştirmeyi hello işlemi şu anda el ile ancak çok basit toodo gelir.</span><span class="sxs-lookup"><span data-stu-id="49f56-124">hello process of creating and updating statistics is currently a manual process, but is very simple toodo.</span></span>  <span data-ttu-id="49f56-125">Bu, otomatik olarak oluşturur ve tek sütunları ve dizinleri istatistiklerle güncelleştiren SQL sunucusu benzemez.</span><span class="sxs-lookup"><span data-stu-id="49f56-125">This is unlike SQL Server which automatically creates and updates statistics on single columns and indexes.</span></span>  <span data-ttu-id="49f56-126">Aşağıdaki Hello bilgileri kullanarak, verilerinizi hello istatistikleri hello yönetimini büyük ölçüde otomatikleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49f56-126">By using hello information below, you can greatly automate hello management of hello statistics on your data.</span></span> 

## <a name="getting-started-with-statistics"></a><span data-ttu-id="49f56-127">İstatistikleri ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="49f56-127">Getting started with statistics</span></span>
 <span data-ttu-id="49f56-128">Her sütunda örneklenen istatistikleri oluşturma kolay bir yolu tooget istatistikleri ile başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="49f56-128">Creating sampled statistics on every column is an easy way tooget started with statistics.</span></span>  <span data-ttu-id="49f56-129">Eşit oranda önemli tookeep istatistikleri güncel olduğuna göre koruyucu bir yaklaşım olabilir tooupdate, istatistikleri günlük eşit veya ondan sonra her yük.</span><span class="sxs-lookup"><span data-stu-id="49f56-129">Since it is equally important tookeep statistics up-to-date, a conservative approach may be tooupdate your statistics daily or after each load.</span></span> <span data-ttu-id="49f56-130">Dengelemeler performans ve hello maliyet toocreate ve güncelleştirme istatistiklerini arasındaki her zaman vardır.</span><span class="sxs-lookup"><span data-stu-id="49f56-130">There are always trade-offs between performance and hello cost toocreate and update statistics.</span></span>  <span data-ttu-id="49f56-131">Tüm, istatistik uzun toomaintain sürüyor bulursanız, hangi sütunların istatistiklerine sahip veya hangi sütunların hakkında daha fazla seçmeli tootry toobe sık sık güncelleştirilmesi gerekmeyen isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49f56-131">If you find it is taking too long toomaintain all of your statistics, you may want tootry toobe more selective about which columns have statistics or which columns need frequent updating.</span></span>  <span data-ttu-id="49f56-132">Örneğin, günlük, yeni değerleri eklenebilir gibi yerine her yük sonra tooupdate tarih sütunlarının isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49f56-132">For example, you might want tooupdate date columns daily, as new values may be added rather than after every load.</span></span> <span data-ttu-id="49f56-133">Yeniden, hello çoğu avantajı sütunlarda söz konusu birleşimler, GROUP BY, HAVING istatistikleri sağlayarak elde edersiniz ve WHERE yan tümcelerini.</span><span class="sxs-lookup"><span data-stu-id="49f56-133">Again, you will gain hello most benefit by having statistics on columns involved in JOINs, GROUP BY, HAVING and WHERE clauses.</span></span>  <span data-ttu-id="49f56-134">Çok sayıda içeren bir tablo varsa, yan tümcesi yalnızca hello kullanılan sütunları seçin, bu sütunlar istatistik yardımcı ve biraz daha fazla çaba tooidentify harcama burada istatistikleri yardımcı olur, hello sütunları azaltabilir hello zaman toomaintain, istatistikleri .</span><span class="sxs-lookup"><span data-stu-id="49f56-134">If you have a table with a lot of columns which are only used in hello SELECT clause, statistics on these columns may not help, and spending a little more effort tooidentify only hello columns where statistics will help, can reduce hello time toomaintain your statistics.</span></span>

## <a name="multi-column-statistics"></a><span data-ttu-id="49f56-135">Birden çok sütun istatistikleri</span><span class="sxs-lookup"><span data-stu-id="49f56-135">Multi-column statistics</span></span>
<span data-ttu-id="49f56-136">Ayrıca toocreating istatistikleri tek sütunlarda sorgularınızı çok sütunlu İstatistikler faydalanırsınız bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49f56-136">In addition toocreating statistics on single columns, you may find that your queries will benefit from multi-column statistics.</span></span>  <span data-ttu-id="49f56-137">Çok sütunlu İstatistikler sütun listesini oluşturulan istatistikleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="49f56-137">Multi-column statistics are statistics created on a list of columns.</span></span>  <span data-ttu-id="49f56-138">Merhaba listesinde tek sütun istatistikleri hello ilk sütunda içerirler artı bazı arası sütun bağıntı bilgileri densities çağrılır.</span><span class="sxs-lookup"><span data-stu-id="49f56-138">They include single column statistics on hello first column in hello list, plus some cross-column correlation information called densities.</span></span>  <span data-ttu-id="49f56-139">Örneğin, iki sütun tooanother katıldığı bir tablo varsa, iki sütun arasında ilişki hello bilirse SQL Data Warehouse daha iyi hello planı iyileştirebilirsiniz bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49f56-139">For example, if you have a table that joins tooanother on two columns, you may find that SQL Data Warehouse can better optimize hello plan if it understands hello relationship between two columns.</span></span>   <span data-ttu-id="49f56-140">Çok sütunlu İstatistikler bileşik birleştirmeler ve Grupla gibi bazı işlemleri için sorgu performansını iyileştirebilir.</span><span class="sxs-lookup"><span data-stu-id="49f56-140">Multi-column statistics can improve query performance for some operations such as composite joins and group by.</span></span>

## <a name="updating-statistics"></a><span data-ttu-id="49f56-141">İstatistikleri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="49f56-141">Updating statistics</span></span>
<span data-ttu-id="49f56-142">İstatistikleri güncelleştirmeyi, veritabanı yönetim alışkanlık önemli bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="49f56-142">Updating statistics is an important part of your database management routine.</span></span>  <span data-ttu-id="49f56-143">Merhaba dağıtım hello veritabanında veri değiştiğinde istatistikleri güncelleştirilmiş toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="49f56-143">When hello distribution of data in hello database changes, statistics need toobe updated.</span></span>  <span data-ttu-id="49f56-144">Güncel olmayan İstatistikler toosub en iyi sorgu performansını götürür.</span><span class="sxs-lookup"><span data-stu-id="49f56-144">Out-of-date statistics will lead toosub-optimal query performance.</span></span>

<span data-ttu-id="49f56-145">Yeni tarihleri eklendikçe bir en iyi tarih sütunlarının tooupdate istatistik günde bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="49f56-145">One best practice is tooupdate statistics on date columns each day as new dates are added.</span></span>  <span data-ttu-id="49f56-146">Her zaman yeni satırlar hello veri ambarına yüklenir, yeni yükleme veya işlem tarihleri eklenir.</span><span class="sxs-lookup"><span data-stu-id="49f56-146">Each time new rows are loaded into hello data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="49f56-147">Bunlar hello veri dağıtım değiştirin ve hello istatistikleri güncel olun.</span><span class="sxs-lookup"><span data-stu-id="49f56-147">These change hello data distribution and make hello statistics out-of-date.</span></span> <span data-ttu-id="49f56-148">Buna karşılık, değerlerin Hello dağıtım genellikle değişmez gibi bir müşteri tablosundaki Ülke sütunu istatistiklerle hiçbir zaman güncelleştirilmiş, toobe gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="49f56-148">Conversely, statistics on a country column in a customer table might never need toobe updated, as hello distribution of values doesn’t generally change.</span></span> <span data-ttu-id="49f56-149">Merhaba dağıtım müşterileri arasında sabit olduğunu varsayarak, yeni satır toohello tablosu değişimi ekleme toochange hello veri dağıtım adımıdır değil.</span><span class="sxs-lookup"><span data-stu-id="49f56-149">Assuming hello distribution is constant between customers, adding new rows toohello table variation isn't going toochange hello data distribution.</span></span> <span data-ttu-id="49f56-150">Ancak, veri Ambarınızı yalnızca bir ülkede varsa ve yeni bir ülkeden veri Getir depolanmakta, birden fazla ülkede verilerden sonuçta sonra kesinlikle hello Ülke sütunu tooupdate istatistik gerekir.</span><span class="sxs-lookup"><span data-stu-id="49f56-150">However, if your data warehouse only contains one country and you bring in data from a new country, resulting in data from multiple countries being stored, then you definitely need tooupdate statistics on hello country column.</span></span>

<span data-ttu-id="49f56-151">Bir sorgu sorun giderme olduğunda hello ilk soruları tooask "biri hello istatistikleri güncel?"</span><span class="sxs-lookup"><span data-stu-id="49f56-151">One of hello first questions tooask when troubleshooting a query is, "Are hello statistics up-to-date?"</span></span>

<span data-ttu-id="49f56-152">Bu soru hello veri hello yaşa göre yanıtlanması biri değil.</span><span class="sxs-lookup"><span data-stu-id="49f56-152">This question is not one that can be answered by hello age of hello data.</span></span> <span data-ttu-id="49f56-153">Yukarı toodate istatistikleri nesneyi veri arka plandaki hiçbir malzeme değişiklik toohello yapıldıysa çok eski olabilir.</span><span class="sxs-lookup"><span data-stu-id="49f56-153">An up toodate statistics object could be very old if there's been no material change toohello underlying data.</span></span> <span data-ttu-id="49f56-154">Merhaba satır sayısını önemli ölçüde değişti veya belirtilen sütun için değerlerin hello dağıtımındaki maddi bir değişiklik olduğunda *sonra* süresi tooupdate istatistikleri değil.</span><span class="sxs-lookup"><span data-stu-id="49f56-154">When hello number of rows has changed substantially or there is a material change in hello distribution of values for a given column *then* it's time tooupdate statistics.</span></span>  

<span data-ttu-id="49f56-155">Başvuru için **SQL Server** (SQL Data Warehouse değil) otomatik olarak bu gibi durumlarda istatistiklerini güncelleştirir:</span><span class="sxs-lookup"><span data-stu-id="49f56-155">For reference, **SQL Server** (not SQL Data Warehouse) automatically updates statistics for these situations:</span></span>

* <span data-ttu-id="49f56-156">Satır eklediğinizde hello tablosunda sıfır satır varsa, bir otomatik güncelleştirme istatistik alacaksınız</span><span class="sxs-lookup"><span data-stu-id="49f56-156">If you have zero rows in hello table, when you add rows, you’ll get an automatic update of statistics</span></span>
* <span data-ttu-id="49f56-157">500'den az satırlarla başlangıç 500'den fazla satır tooa tablo eklediğinizde (örn. başlangıçta 499 sahip ve 500 satır tooa toplam 999 satır ekleme), bir otomatik güncelleştirme alırsınız</span><span class="sxs-lookup"><span data-stu-id="49f56-157">When you add more than 500 rows tooa table starting with less than 500 rows (e.g. at start you have 499 and then add 500 rows tooa total of 999 rows), you’ll get an automatic update</span></span> 
* <span data-ttu-id="49f56-158">500'den fazla satır olduğunuzda hello istatistikleri üzerinde bir otomatik güncelleştirme görürsünüz önce tooadd 500 ek satırlar + Merhaba tablonun hello boyutunun % 20 gerekir</span><span class="sxs-lookup"><span data-stu-id="49f56-158">Once you’re over 500 rows you will have tooadd 500 additional rows + 20% of hello size of hello table before you’ll see an automatic update on hello stats</span></span>

<span data-ttu-id="49f56-159">Hiçbir DMV toodetermine olduğundan hello tablo içindeki veri hello son süresi istatistikleri güncelleştirildi oluşturulmasından sonra değiştirilmişse, istatistik hello yaş bilerek, hello resim parçası olan sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49f56-159">Since there is no DMV toodetermine if data within hello table has changed since hello last time statistics were updated, knowing hello age of your statistics can provide you with part of hello picture.</span></span>  <span data-ttu-id="49f56-160">Toodetermine hello son zamanı, istatistikleri sorgu aşağıdaki hello kullanabileceğiniz her bir tabloda güncelleştirilmiş burada.</span><span class="sxs-lookup"><span data-stu-id="49f56-160">You can use hello following query toodetermine hello last time your statistics where updated on each table.</span></span>  

> [!NOTE]
> <span data-ttu-id="49f56-161">Verili bir sütunun değerlerini hello dağıtımını maddi bir değişiklik varsa, bunlar güncelleştirildiği son zaman istatistikleri hello bağımsız olarak güncelleştirmeniz gerekir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="49f56-161">Remember if there is a material change in hello distribution of values for a given column, you should update statistics regardless of hello last time they were updated.</span></span>  
> 
> 

```sql
SELECT
    sm.[name] AS [schema_name],
    tb.[name] AS [table_name],
    co.[name] AS [stats_column_name],
    st.[name] AS [stats_name],
    STATS_DATE(st.[object_id],st.[stats_id]) AS [stats_last_updated_date]
FROM
    sys.objects ob
    JOIN sys.stats st
        ON  ob.[object_id] = st.[object_id]
    JOIN sys.stats_columns sc    
        ON  st.[stats_id] = sc.[stats_id]
        AND st.[object_id] = sc.[object_id]
    JOIN sys.columns co    
        ON  sc.[column_id] = co.[column_id]
        AND sc.[object_id] = co.[object_id]
    JOIN sys.types  ty    
        ON  co.[user_type_id] = ty.[user_type_id]
    JOIN sys.tables tb    
        ON  co.[object_id] = tb.[object_id]
    JOIN sys.schemas sm    
        ON  tb.[schema_id] = sm.[schema_id]
WHERE
    st.[user_created] = 1;
```

<span data-ttu-id="49f56-162">Örneğin, bir veri ambarında tarih sütunlarının genellikle istatistikleri güncelleştirmeleri sık.</span><span class="sxs-lookup"><span data-stu-id="49f56-162">Date columns in a data warehouse, for example, usually need frequent statistics updates.</span></span> <span data-ttu-id="49f56-163">Her zaman yeni satırlar hello veri ambarına yüklenir, yeni yükleme veya işlem tarihleri eklenir.</span><span class="sxs-lookup"><span data-stu-id="49f56-163">Each time new rows are loaded into hello data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="49f56-164">Bunlar hello veri dağıtım değiştirin ve hello istatistikleri güncel olun.</span><span class="sxs-lookup"><span data-stu-id="49f56-164">These change hello data distribution and make hello statistics out-of-date.</span></span>  <span data-ttu-id="49f56-165">Buna karşılık, bir müşteri tabloda cinsiyetiniz sütun istatistiklerle güncelleştirilmiş toobe hiçbir zaman gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="49f56-165">Conversely, statistics on a gender column on a customer table might never need toobe updated.</span></span> <span data-ttu-id="49f56-166">Merhaba dağıtım müşterileri arasında sabit olduğunu varsayarak, yeni satır toohello tablosu değişimi ekleme toochange hello veri dağıtım adımıdır değil.</span><span class="sxs-lookup"><span data-stu-id="49f56-166">Assuming hello distribution is constant between customers, adding new rows toohello table variation isn't going toochange hello data distribution.</span></span> <span data-ttu-id="49f56-167">Veri ambarınız bir cinsiyeti ve birden çok genders yeni gereksinimi sonuçlarında yalnızca içeriyorsa ancak ardından kesinlikle hello cinsiyetiniz sütun tooupdate istatistik gerekir.</span><span class="sxs-lookup"><span data-stu-id="49f56-167">However, if your data warehouse only contains one gender and a new requirement results in multiple genders then you definitely need tooupdate statistics on hello gender column.</span></span>

<span data-ttu-id="49f56-168">Daha fazla açıklama için bkz: [istatistikleri] [ Statistics] konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="49f56-168">For further explanation, see [Statistics][Statistics] on MSDN.</span></span>

## <a name="implementing-statistics-management"></a><span data-ttu-id="49f56-169">İstatistikleri yönetimini uygulama</span><span class="sxs-lookup"><span data-stu-id="49f56-169">Implementing statistics management</span></span>
<span data-ttu-id="49f56-170">İyi bir fikir tooextend görülür adresindeki İstatistikler güncelleştirilir işlem tooensure yüklenirken verilerinizi hello hello yük sonuna.</span><span class="sxs-lookup"><span data-stu-id="49f56-170">It is often a good idea tooextend your data loading process tooensure that statistics are updated at hello end of hello load.</span></span> <span data-ttu-id="49f56-171">tabloları boyutlarına ve/veya bunların değerleri dağıtımını en sık değiştirdiğinizde hello veri yükü var.</span><span class="sxs-lookup"><span data-stu-id="49f56-171">hello data load is when tables most frequently change their size and/or their distribution of values.</span></span> <span data-ttu-id="49f56-172">Bu nedenle, bu mantıksal yer tooimplement olan bazı yönetim işlemleri.</span><span class="sxs-lookup"><span data-stu-id="49f56-172">Therefore, this is a logical place tooimplement some management processes.</span></span>

<span data-ttu-id="49f56-173">Bazı temel ilkeler hello yükleme işlemi sırasında İstatistikleri güncelleştirmek için aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="49f56-173">Some guiding principles are provided below for updating your statistics during hello load process:</span></span>

* <span data-ttu-id="49f56-174">Yüklenen her tablo güncelleştirilmiş en az bir istatistik nesnesi olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="49f56-174">Ensure that each loaded table has at least one statistics object updated.</span></span> <span data-ttu-id="49f56-175">Bu güncelleştirmeleri hello hello istatistikleri güncelleştirme parçası olarak boyutu (satır sayısı ve sayfa sayısı) bilgilerini tablolarını.</span><span class="sxs-lookup"><span data-stu-id="49f56-175">This updates hello tables size (row count and page count) information as part of hello stats update.</span></span>
* <span data-ttu-id="49f56-176">BİRLEŞTİRME, GROUP BY, ORDER BY ve DISTINCT yan tümcelerinde katılan sütunları odaklanmak</span><span class="sxs-lookup"><span data-stu-id="49f56-176">Focus on columns participating in JOIN, GROUP BY, ORDER BY and DISTINCT clauses</span></span>
* <span data-ttu-id="49f56-177">Bu değerleri hello istatistikleri Histogramı dahil edilmeyen daha sık tarihleri "anahtar artan" sütunlarını işlem gibi güncelleştirme göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="49f56-177">Consider updating "ascending key" columns such as transaction dates more frequently as these values will not be included in hello statistics histogram.</span></span>
* <span data-ttu-id="49f56-178">Statik dağıtım sütunları daha az sıklıkla güncelleştirmeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="49f56-178">Consider updating static distribution columns less frequently.</span></span>
* <span data-ttu-id="49f56-179">Her istatistik nesne serisinde güncelleştirilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="49f56-179">Remember each statistic object is updated in series.</span></span> <span data-ttu-id="49f56-180">Yalnızca uygulama `UPDATE STATISTICS <TABLE_NAME>` - özellikle istatistikleri nesnelerin çok geniş tablolar için uygun olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="49f56-180">Simply implementing `UPDATE STATISTICS <TABLE_NAME>` may not be ideal - especially for wide tables with lots of statistics objects.</span></span>

> [!NOTE]
> <span data-ttu-id="49f56-181">[Anahtar artan] hakkında daha fazla ayrıntı için lütfen toohello SQL Server 2014 kardinalite tahmin modeli teknik incelemesine bakın.</span><span class="sxs-lookup"><span data-stu-id="49f56-181">For more details on [ascending key] please refer toohello SQL Server 2014 cardinality estimation model whitepaper.</span></span>
> 
> 

<span data-ttu-id="49f56-182">Daha fazla açıklama için bkz: [kardinalite tahmin] [ Cardinality Estimation] konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="49f56-182">For further explanation, see  [Cardinality Estimation][Cardinality Estimation] on MSDN.</span></span>

## <a name="examples-create-statistics"></a><span data-ttu-id="49f56-183">Örnekler: istatistikler oluşturma</span><span class="sxs-lookup"><span data-stu-id="49f56-183">Examples: Create statistics</span></span>
<span data-ttu-id="49f56-184">Bu örnekler nasıl toouse istatistikleri oluşturmak için çeşitli seçenekler.</span><span class="sxs-lookup"><span data-stu-id="49f56-184">These examples show how toouse various options for creating statistics.</span></span> <span data-ttu-id="49f56-185">her sütun için kullandığınız hello seçenekleri verilerinizi hello özelliklerini ve hello sütunu sorguda nasıl kullanılacağını bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="49f56-185">hello options that you use for each column depend on hello characteristics of your data and how hello column will be used in queries.</span></span>

### <a name="a-create-single-column-statistics-with-default-options"></a><span data-ttu-id="49f56-186">A.</span><span class="sxs-lookup"><span data-stu-id="49f56-186">A.</span></span> <span data-ttu-id="49f56-187">Varsayılan seçeneklerle tek sütunlu istatistikler oluşturma</span><span class="sxs-lookup"><span data-stu-id="49f56-187">Create single-column statistics with default options</span></span>
<span data-ttu-id="49f56-188">bir sütunda toocreate istatistikleri, hello istatistikleri nesnesi için ad ve hello sütunun hello adı yalnızca sağlar.</span><span class="sxs-lookup"><span data-stu-id="49f56-188">toocreate statistics on a column, simply provide a name for hello statistics object and hello name of hello column.</span></span>

<span data-ttu-id="49f56-189">Bu sözdiziminin tüm hello varsayılan seçenekleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="49f56-189">This syntax uses all of hello default options.</span></span> <span data-ttu-id="49f56-190">İstatistikleri oluşturduğunda, varsayılan olarak, SQL Data Warehouse Merhaba tablonun yüzde 20 örnekleri.</span><span class="sxs-lookup"><span data-stu-id="49f56-190">By default, SQL Data Warehouse samples 20 percent of hello table when it creates statistics.</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

<span data-ttu-id="49f56-191">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="49f56-191">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="b-create-single-column-statistics-by-examining-every-row"></a><span data-ttu-id="49f56-192">B.</span><span class="sxs-lookup"><span data-stu-id="49f56-192">B.</span></span> <span data-ttu-id="49f56-193">Her satır inceleyerek tek sütunlu istatistikler oluşturma</span><span class="sxs-lookup"><span data-stu-id="49f56-193">Create single-column statistics by examining every row</span></span>
<span data-ttu-id="49f56-194">Merhaba varsayılan örnekleme oranını yüzde 20 oranında çoğu durumlar için yeterli olur.</span><span class="sxs-lookup"><span data-stu-id="49f56-194">hello default sampling rate of 20 percent is sufficient for most situations.</span></span> <span data-ttu-id="49f56-195">Bununla birlikte, hello örnekleme hızını ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49f56-195">However, you can adjust hello sampling rate.</span></span>

<span data-ttu-id="49f56-196">toosample hello tam tablo, bu söz dizimini kullanın:</span><span class="sxs-lookup"><span data-stu-id="49f56-196">toosample hello full table, use this syntax:</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

<span data-ttu-id="49f56-197">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="49f56-197">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="c-create-single-column-statistics-by-specifying-hello-sample-size"></a><span data-ttu-id="49f56-198">C.</span><span class="sxs-lookup"><span data-stu-id="49f56-198">C.</span></span> <span data-ttu-id="49f56-199">Tek sütunlu İstatistikler hello örnek boyutunu belirterek oluşturun.</span><span class="sxs-lookup"><span data-stu-id="49f56-199">Create single-column statistics by specifying hello sample size</span></span>
<span data-ttu-id="49f56-200">Alternatif olarak, bir yüzde olarak hello örnek boyutu belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="49f56-200">Alternatively, you can specify hello sample size as a percent:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="d-create-single-column-statistics-on-only-some-of-hello-rows"></a><span data-ttu-id="49f56-201">D.</span><span class="sxs-lookup"><span data-stu-id="49f56-201">D.</span></span> <span data-ttu-id="49f56-202">Tek sütunlu İstatistikler yalnızca bazı hello satırları oluşturma</span><span class="sxs-lookup"><span data-stu-id="49f56-202">Create single-column statistics on only some of hello rows</span></span>
<span data-ttu-id="49f56-203">Başka bir seçenek tablonuzda hello satır bir kısmı istatistikleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49f56-203">Another option, you can create statistics on a portion of hello rows in your table.</span></span> <span data-ttu-id="49f56-204">Bu filtrelenmiş istatistiği çağrılır.</span><span class="sxs-lookup"><span data-stu-id="49f56-204">This is called a filtered statistic.</span></span>

<span data-ttu-id="49f56-205">Örneğin, tooquery büyük bölümlenmiş bir tablodaki belirli bir bölüm planlarken filtrelenmiş istatistik kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49f56-205">For example, you could use filtered statistics when you plan tooquery a specific partition of a large partitioned table.</span></span> <span data-ttu-id="49f56-206">İstatistikler yalnızca hello üzerinde bölüm değerleri oluşturmayı tarafından hello istatistikleri hello doğruluğunu artırmak ve bu nedenle sorgu performansını artırmak.</span><span class="sxs-lookup"><span data-stu-id="49f56-206">By creating statistics on only hello partition values, hello accuracy of hello statistics will improve, and therefore improve query performance.</span></span>

<span data-ttu-id="49f56-207">Bu örnek değerleri çeşitli İstatistikler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="49f56-207">This example creates statistics on a range of values.</span></span> <span data-ttu-id="49f56-208">Merhaba değerleri kolayca olabilir değerleri toomatch hello aralığı bir bölümünde tanımlanmış.</span><span class="sxs-lookup"><span data-stu-id="49f56-208">hello values could easily be defined toomatch hello range of values in a partition.</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> <span data-ttu-id="49f56-209">Sorgu iyileştiricisi tooconsider hello dağıtılmış sorgu planı seçtiğinde filtrelenmiş istatistik kullanarak hello için hello sorgu hello istatistikleri nesnesinin hello tanımı içinde sığması gerekir.</span><span class="sxs-lookup"><span data-stu-id="49f56-209">For hello query optimizer tooconsider using filtered statistics when it chooses hello distributed query plan, hello query must fit inside hello definition of hello statistics object.</span></span> <span data-ttu-id="49f56-210">Merhaba önceki örnekte, burada yan tümcesi 2000101 ve 20001231 arasındaki toospecify col1 değerleri gereken hello sorgunun kullanma.</span><span class="sxs-lookup"><span data-stu-id="49f56-210">Using hello previous example, hello query's where clause needs toospecify col1 values between 2000101 and 20001231.</span></span>
> 
> 

### <a name="e-create-single-column-statistics-with-all-hello-options"></a><span data-ttu-id="49f56-211">E.</span><span class="sxs-lookup"><span data-stu-id="49f56-211">E.</span></span> <span data-ttu-id="49f56-212">Tüm hello seçeneklerle tek sütunlu istatistikler oluşturma</span><span class="sxs-lookup"><span data-stu-id="49f56-212">Create single-column statistics with all hello options</span></span>
<span data-ttu-id="49f56-213">Elbette, başlangıç seçenekleri birlikte birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49f56-213">You can, of course, combine hello options together.</span></span> <span data-ttu-id="49f56-214">Aşağıdaki Hello örnek filtrelenmiş istatistik nesnesi bir özel örnek boyutu ile oluşturur:</span><span class="sxs-lookup"><span data-stu-id="49f56-214">hello example below creates a filtered statistics object with a custom sample size:</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="49f56-215">Merhaba tam başvuru için bkz: [CREATE STATISTICS] [ CREATE STATISTICS] konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="49f56-215">For hello full reference, see [CREATE STATISTICS][CREATE STATISTICS] on MSDN.</span></span>

### <a name="f-create-multi-column-statistics"></a><span data-ttu-id="49f56-216">F</span><span class="sxs-lookup"><span data-stu-id="49f56-216">F.</span></span> <span data-ttu-id="49f56-217">Çok sütunlu istatistikler oluşturma</span><span class="sxs-lookup"><span data-stu-id="49f56-217">Create multi-column statistics</span></span>
<span data-ttu-id="49f56-218">toocreate çok sütunlu İstatistikler yalnızca hello önceki örneklerde kullanır, ancak daha fazla sütun belirtin.</span><span class="sxs-lookup"><span data-stu-id="49f56-218">toocreate a multi-column statistics, simply use hello previous examples, but specify more columns.</span></span>

> [!NOTE]
> <span data-ttu-id="49f56-219">kullanılan hello histogram tooestimate hello sorgu sonucu, satır sayısıdır yalnızca hello istatistikleri nesne tanımı'nda listelenen hello ilk sütun için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="49f56-219">hello histogram, which is used tooestimate number of rows in hello query result, is only available for hello first column listed in hello statistics object definition.</span></span>
> 
> 

<span data-ttu-id="49f56-220">Bu örnekte, hello histogram açıktır *ürün\_kategori*.</span><span class="sxs-lookup"><span data-stu-id="49f56-220">In this example, hello histogram is on *product\_category*.</span></span> <span data-ttu-id="49f56-221">Çapraz sütunlu İstatistikler hesaplanır *ürün\_kategori* ve *ürün\_sub_c\ategory*:</span><span class="sxs-lookup"><span data-stu-id="49f56-221">Cross-column statistics are calculated on *product\_category* and *product\_sub_c\ategory*:</span></span>

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="49f56-222">Arasında bir ilişki olduğundan *ürün\_kategori* ve *ürün\_alt\_kategori*, birden çok sütun stat bu sütunları erişilen faydalı olabilir Merhaba, aynı anda.</span><span class="sxs-lookup"><span data-stu-id="49f56-222">Since there is a correlation between *product\_category* and *product\_sub\_category*, a multi-column stat can be useful if these columns are accessed at hello same time.</span></span>

### <a name="g-create-statistics-on-all-hello-columns-in-a-table"></a><span data-ttu-id="49f56-223">G.</span><span class="sxs-lookup"><span data-stu-id="49f56-223">G.</span></span> <span data-ttu-id="49f56-224">Bir tablodaki tüm hello sütunlarda istatistikler oluşturma</span><span class="sxs-lookup"><span data-stu-id="49f56-224">Create statistics on all hello columns in a table</span></span>
<span data-ttu-id="49f56-225">Tek yönlü toocreate istatistikleri hello tablosu oluşturduktan sonra tooissues CREATE STATISTICS komutları olur.</span><span class="sxs-lookup"><span data-stu-id="49f56-225">One way toocreate statistics is tooissues CREATE STATISTICS commands after creating hello table.</span></span>

```sql
CREATE TABLE dbo.table1
(
   col1 int
,  col2 int
,  col3 int
)
WITH
  (
    CLUSTERED COLUMNSTORE INDEX
  )
;

CREATE STATISTICS stats_col1 on dbo.table1 (col1);
CREATE STATISTICS stats_col2 on dbo.table2 (col2);
CREATE STATISTICS stats_col3 on dbo.table3 (col3);
```

### <a name="h-use-a-stored-procedure-toocreate-statistics-on-all-columns-in-a-database"></a><span data-ttu-id="49f56-226">H.</span><span class="sxs-lookup"><span data-stu-id="49f56-226">H.</span></span> <span data-ttu-id="49f56-227">Saklı yordam toocreate istatistikleri veritabanındaki tüm sütunları kullanın</span><span class="sxs-lookup"><span data-stu-id="49f56-227">Use a stored procedure toocreate statistics on all columns in a database</span></span>
<span data-ttu-id="49f56-228">SQL veri ambarı sistem saklı yordam eşdeğer çok yok SQL Server'daki [sp_create_stats] [].</span><span class="sxs-lookup"><span data-stu-id="49f56-228">SQL Data Warehouse does not have a system stored procedure equivalent too[sp_create_stats][] in SQL Server.</span></span> <span data-ttu-id="49f56-229">Bu saklı yordam istatistikleri zaten yok hello veritabanı her sütunun bir tek sütun istatistikleri nesnesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="49f56-229">This stored procedure creates a single column statistics object on every column of hello database that doesn't already have statistics.</span></span>

<span data-ttu-id="49f56-230">Bu, veritabanı tasarımınız ile çalışmaya başlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="49f56-230">This will help you get started with your database design.</span></span> <span data-ttu-id="49f56-231">Ücretsiz tooadapt düşünüyorsanız, tooyour gerekir.</span><span class="sxs-lookup"><span data-stu-id="49f56-231">Feel free tooadapt it tooyour needs.</span></span>

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_create_stats]
(   @create_type    tinyint -- 1 default 2 Fullscan 3 Sample
,   @sample_pct     tinyint
)
AS

IF @create_type NOT IN (1,2,3)
BEGIN
    THROW 151000,'Invalid value for @stats_type parameter. Valid range 1 (default), 2 (fullscan) or 3 (sample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN;
    DROP TABLE #stats_ddl;
END;

CREATE TABLE #stats_ddl
WITH    (   DISTRIBUTION    = HASH([seq_nmbr])
        ,   LOCATION        = USER_DB
        )
AS
WITH T
AS
(
SELECT      t.[name]                        AS [table_name]
,           s.[name]                        AS [table_schema_name]
,           c.[name]                        AS [column_name]
,           c.[column_id]                   AS [column_id]
,           t.[object_id]                   AS [object_id]
,           ROW_NUMBER()
            OVER(ORDER BY (SELECT NULL))    AS [seq_nmbr]
FROM        sys.[tables] t
JOIN        sys.[schemas] s         ON  t.[schema_id]       = s.[schema_id]
JOIN        sys.[columns] c         ON  t.[object_id]       = c.[object_id]
LEFT JOIN   sys.[stats_columns] l   ON  l.[object_id]       = c.[object_id]
                                    AND l.[column_id]       = c.[column_id]
                                    AND l.[stats_column_id] = 1
LEFT JOIN    sys.[external_tables] e    ON    e.[object_id]        = t.[object_id]
WHERE       l.[object_id] IS NULL
AND            e.[object_id] IS NULL -- not an external table
)
SELECT  [table_schema_name]
,       [table_name]
,       [column_name]
,       [column_id]
,       [object_id]
,       [seq_nmbr]
,       CASE @create_type
        WHEN 1
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+')' AS VARCHAR(8000))
        WHEN 2
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH FULLSCAN' AS VARCHAR(8000))
        WHEN 3
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH SAMPLE '+@sample_pct+'PERCENT' AS VARCHAR(8000))
        END AS create_stat_ddl
FROM T
;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''
;

WHILE @i <= @t
BEGIN
    SET @s=(SELECT create_stat_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

<span data-ttu-id="49f56-232">Bu yordam ile Merhaba tablodaki tüm sütunları toocreate istatistik yalnızca hello yordamını çağırın.</span><span class="sxs-lookup"><span data-stu-id="49f56-232">toocreate statistics on all columns in hello table with this procedure, simply call hello procedure.</span></span>

```sql
prc_sqldw_create_stats;
```

## <a name="examples-update-statistics"></a><span data-ttu-id="49f56-233">Örnekler: istatistikleri güncelleştir</span><span class="sxs-lookup"><span data-stu-id="49f56-233">Examples: update statistics</span></span>
<span data-ttu-id="49f56-234">tooupdate istatistikleri, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="49f56-234">tooupdate statistics, you can:</span></span>

1. <span data-ttu-id="49f56-235">Bir istatistik Nesne güncelleştirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="49f56-235">Update one statistics object.</span></span> <span data-ttu-id="49f56-236">İstatistikleri tooupdate istediğiniz nesne hello Hello adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="49f56-236">Specify hello name of hello statistics object you wish tooupdate.</span></span>
2. <span data-ttu-id="49f56-237">Bir tablodaki tüm istatistikleri nesneleri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="49f56-237">Update all statistics objects on a table.</span></span> <span data-ttu-id="49f56-238">Bir özel istatistikleri nesne yerine Merhaba tablonun Hello adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="49f56-238">Specify hello name of hello table instead of one specific statistics object.</span></span>

### <a name="a-update-one-specific-statistics-object"></a><span data-ttu-id="49f56-239">A.</span><span class="sxs-lookup"><span data-stu-id="49f56-239">A.</span></span> <span data-ttu-id="49f56-240">Güncelleştirme belirli bir istatistik nesnesi</span><span class="sxs-lookup"><span data-stu-id="49f56-240">Update one specific statistics object</span></span>
<span data-ttu-id="49f56-241">Sözdizimi tooupdate belirli istatistikleri nesne aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="49f56-241">Use hello following syntax tooupdate a specific statistics object:</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

<span data-ttu-id="49f56-242">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="49f56-242">For example:</span></span>

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

<span data-ttu-id="49f56-243">Belirli istatistikleri nesneleri güncelleştirerek hello zaman ve kaynak gerekli toomanage istatistikleri en aza indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49f56-243">By updating specific statistics objects, you can minimize hello time and resources required toomanage statistics.</span></span> <span data-ttu-id="49f56-244">Bu, bazı, yine de toochoose hello en iyi istatistiklerini nesneleri tooupdate zorlayıcı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="49f56-244">This requires some thought, though, toochoose hello best statistics objects tooupdate.</span></span>

### <a name="b-update-all-statistics-on-a-table"></a><span data-ttu-id="49f56-245">B.</span><span class="sxs-lookup"><span data-stu-id="49f56-245">B.</span></span> <span data-ttu-id="49f56-246">Bir tablodaki tüm istatistikleri güncelleştir</span><span class="sxs-lookup"><span data-stu-id="49f56-246">Update all statistics on a table</span></span>
<span data-ttu-id="49f56-247">Bu tabloda tüm hello istatistikleri nesnelerini güncelleştirme için basit bir yöntemi gösterir.</span><span class="sxs-lookup"><span data-stu-id="49f56-247">This shows a simple method for updating all hello statistics objects on a table.</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

<span data-ttu-id="49f56-248">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="49f56-248">For example:</span></span>

```sql
UPDATE STATISTICS dbo.table1;
```

<span data-ttu-id="49f56-249">Kolay toouse ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="49f56-249">This statement is easy toouse.</span></span> <span data-ttu-id="49f56-250">Yalnızca bu hello tablosundaki tüm istatistiklerini güncelleştirir ve bu nedenle gerekli olandan daha fazla iş gerçekleştirebileceğiniz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="49f56-250">Just remember this updates all statistics on hello table, and therefore might perform more work than is necessary.</span></span> <span data-ttu-id="49f56-251">Merhaba performans sorunu değilse, bu kesinlikle tooguarantee istatistikleri güncel hello en kolay ve eksiksiz yoludur.</span><span class="sxs-lookup"><span data-stu-id="49f56-251">If hello performance is not an issue, this is definitely hello easiest and most complete way tooguarantee statistics are up-to-date.</span></span>

> [!NOTE]
> <span data-ttu-id="49f56-252">Bir tablodaki tüm istatistikleri güncelleştirirken SQL Data Warehouse bir tarama toosample hello tablo her istatistik desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="49f56-252">When updating all statistics on a table, SQL Data Warehouse does a scan toosample hello table for each statistics.</span></span> <span data-ttu-id="49f56-253">Merhaba tablonun büyük ise fazla sayıda sütun ve birçok istatistikleri sahipse, gerekli olduğunda bağlı olarak daha verimli tooupdate tek tek istatistikleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="49f56-253">If hello table is large, has many columns, and many statistics, it might be more efficient tooupdate individual statistics based on need.</span></span>
> 
> 

<span data-ttu-id="49f56-254">Bir uygulama için bir `UPDATE STATISTICS` yordamı Lütfen hello bakın [geçici tablolar] [ Temporary] makalesi.</span><span class="sxs-lookup"><span data-stu-id="49f56-254">For an implementation of an `UPDATE STATISTICS` procedure please see hello [Temporary Tables][Temporary] article.</span></span> <span data-ttu-id="49f56-255">Merhaba uygulama yöntemidir biraz farklı toohello `CREATE STATISTICS` yukarıdaki yordamı hello sonuç ancak aynı hello olduğu.</span><span class="sxs-lookup"><span data-stu-id="49f56-255">hello implementation method is slightly different toohello `CREATE STATISTICS` procedure above but hello end result is hello same.</span></span>

<span data-ttu-id="49f56-256">Merhaba tam sözdizimi için bkz: [Update STATISTICS] [ Update Statistics] konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="49f56-256">For hello full syntax, see [Update Statistics][Update Statistics] on MSDN.</span></span>

## <a name="statistics-metadata"></a><span data-ttu-id="49f56-257">İstatistikleri meta verileri</span><span class="sxs-lookup"><span data-stu-id="49f56-257">Statistics metadata</span></span>
<span data-ttu-id="49f56-258">Çeşitli sistem görünümü ve toofind istatistikleri hakkında bilgi kullanabileceğiniz işlevleri vardır.</span><span class="sxs-lookup"><span data-stu-id="49f56-258">There are several system view and functions that you can use toofind information about statistics.</span></span> <span data-ttu-id="49f56-259">Örneğin, bir istatistik nesnesi istatistikleri en son oluşturulan veya güncelleştirilen hello istatistikleri tarih işlevi toosee kullanarak güncel olmayabilir, görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49f56-259">For example, you can see if a statistics object might be out-of-date by using hello stats-date function toosee when statistics were last created or updated.</span></span>

### <a name="catalog-views-for-statistics"></a><span data-ttu-id="49f56-260">Katalog görünümleri istatistikleri</span><span class="sxs-lookup"><span data-stu-id="49f56-260">Catalog views for statistics</span></span>
<span data-ttu-id="49f56-261">Bu sistem görünümleri İstatistikler hakkında bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="49f56-261">These system views provide information about statistics:</span></span>

| <span data-ttu-id="49f56-262">Katalog görünümü</span><span class="sxs-lookup"><span data-stu-id="49f56-262">Catalog View</span></span> | <span data-ttu-id="49f56-263">Açıklama</span><span class="sxs-lookup"><span data-stu-id="49f56-263">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="49f56-264">[sys.Columns][sys.columns]</span><span class="sxs-lookup"><span data-stu-id="49f56-264">[sys.columns][sys.columns]</span></span> |<span data-ttu-id="49f56-265">Her sütun için bir satır.</span><span class="sxs-lookup"><span data-stu-id="49f56-265">One row for each column.</span></span> |
| <span data-ttu-id="49f56-266">[sys.Objects][sys.objects]</span><span class="sxs-lookup"><span data-stu-id="49f56-266">[sys.objects][sys.objects]</span></span> |<span data-ttu-id="49f56-267">Merhaba veritabanında her nesne için bir satır.</span><span class="sxs-lookup"><span data-stu-id="49f56-267">One row for each object in hello database.</span></span> |
| <span data-ttu-id="49f56-268">[sys.schemas][sys.schemas]</span><span class="sxs-lookup"><span data-stu-id="49f56-268">[sys.schemas][sys.schemas]</span></span> |<span data-ttu-id="49f56-269">Merhaba veritabanındaki her şema için bir satır.</span><span class="sxs-lookup"><span data-stu-id="49f56-269">One row for each schema in hello database.</span></span> |
| <span data-ttu-id="49f56-270">[sys.stats][sys.stats]</span><span class="sxs-lookup"><span data-stu-id="49f56-270">[sys.stats][sys.stats]</span></span> |<span data-ttu-id="49f56-271">Her bir istatistik nesne için bir satır.</span><span class="sxs-lookup"><span data-stu-id="49f56-271">One row for each statistics object.</span></span> |
| <span data-ttu-id="49f56-272">[sys.stats_columns][sys.stats_columns]</span><span class="sxs-lookup"><span data-stu-id="49f56-272">[sys.stats_columns][sys.stats_columns]</span></span> |<span data-ttu-id="49f56-273">Merhaba istatistikleri nesnesindeki her sütun için bir satır.</span><span class="sxs-lookup"><span data-stu-id="49f56-273">One row for each column in hello statistics object.</span></span> <span data-ttu-id="49f56-274">Bağlantılar toosys.columns yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="49f56-274">Links back toosys.columns.</span></span> |
| <span data-ttu-id="49f56-275">[sys.Tables][sys.tables]</span><span class="sxs-lookup"><span data-stu-id="49f56-275">[sys.tables][sys.tables]</span></span> |<span data-ttu-id="49f56-276">(Dış tablolara içerir) her tablo için bir satır.</span><span class="sxs-lookup"><span data-stu-id="49f56-276">One row for each table (includes external tables).</span></span> |
| <span data-ttu-id="49f56-277">[sys.table_types][sys.table_types]</span><span class="sxs-lookup"><span data-stu-id="49f56-277">[sys.table_types][sys.table_types]</span></span> |<span data-ttu-id="49f56-278">Her bir veri türü için bir satır.</span><span class="sxs-lookup"><span data-stu-id="49f56-278">One row for each data type.</span></span> |

### <a name="system-functions-for-statistics"></a><span data-ttu-id="49f56-279">Sistem işlevleri için istatistikleri</span><span class="sxs-lookup"><span data-stu-id="49f56-279">System functions for statistics</span></span>
<span data-ttu-id="49f56-280">Bu sistem işlevler istatistikleri ile çalışmak için yararlıdır:</span><span class="sxs-lookup"><span data-stu-id="49f56-280">These system functions are useful for working with statistics:</span></span>

| <span data-ttu-id="49f56-281">Sistem işlevi</span><span class="sxs-lookup"><span data-stu-id="49f56-281">System Function</span></span> | <span data-ttu-id="49f56-282">Açıklama</span><span class="sxs-lookup"><span data-stu-id="49f56-282">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="49f56-283">[STATS_DATE][STATS_DATE]</span><span class="sxs-lookup"><span data-stu-id="49f56-283">[STATS_DATE][STATS_DATE]</span></span> |<span data-ttu-id="49f56-284">Tarih hello istatistikleri nesnesi son güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="49f56-284">Date hello statistics object was last updated.</span></span> |
| <span data-ttu-id="49f56-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span><span class="sxs-lookup"><span data-stu-id="49f56-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span></span> |<span data-ttu-id="49f56-286">Merhaba istatistikleri nesnesi tarafından anlaşılan değerlerin hello dağıtımı hakkında özet düzeyi ve ayrıntılı bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="49f56-286">Provides summary level and detailed information about hello distribution of values as understood by hello statistics object.</span></span> |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a><span data-ttu-id="49f56-287">Bir görünüme istatistikleri sütunları ve işlevlerini birleştirme</span><span class="sxs-lookup"><span data-stu-id="49f56-287">Combine statistics columns and functions into one view</span></span>
<span data-ttu-id="49f56-288">Bu görünüm toostatistics ve sonuçları hello [STATS_DATE()] [] işlevinden birlikte ilgili sütunları getirir.</span><span class="sxs-lookup"><span data-stu-id="49f56-288">This view brings columns that relate toostatistics, and results from hello [STATS_DATE()][]function together.</span></span>

```sql
CREATE VIEW dbo.vstats_columns
AS
SELECT
        sm.[name]                           AS [schema_name]
,       tb.[name]                           AS [table_name]
,       st.[name]                           AS [stats_name]
,       st.[filter_definition]              AS [stats_filter_defiinition]
,       st.[has_filter]                     AS [stats_is_filtered]
,       STATS_DATE(st.[object_id],st.[stats_id])
                                            AS [stats_last_updated_date]
,       co.[name]                           AS [stats_column_name]
,       ty.[name]                           AS [column_type]
,       co.[max_length]                     AS [column_max_length]
,       co.[precision]                      AS [column_precision]
,       co.[scale]                          AS [column_scale]
,       co.[is_nullable]                    AS [column_is_nullable]
,       co.[collation_name]                 AS [column_collation_name]
,       QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS two_part_name
,       QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS three_part_name
FROM    sys.objects                         AS ob
JOIN    sys.stats           AS st ON    ob.[object_id]      = st.[object_id]
JOIN    sys.stats_columns   AS sc ON    st.[stats_id]       = sc.[stats_id]
                            AND         st.[object_id]      = sc.[object_id]
JOIN    sys.columns         AS co ON    sc.[column_id]      = co.[column_id]
                            AND         sc.[object_id]      = co.[object_id]
JOIN    sys.types           AS ty ON    co.[user_type_id]   = ty.[user_type_id]
JOIN    sys.tables          AS tb ON  co.[object_id]        = tb.[object_id]
JOIN    sys.schemas         AS sm ON  tb.[schema_id]        = sm.[schema_id]
WHERE   1=1
AND     st.[user_created] = 1
;
```

## <a name="dbcc-showstatistics-examples"></a><span data-ttu-id="49f56-289">DBCC SHOW_STATISTICS() örnekleri</span><span class="sxs-lookup"><span data-stu-id="49f56-289">DBCC SHOW_STATISTICS() examples</span></span>
<span data-ttu-id="49f56-290">DBCC SHOW_STATISTICS() istatistikleri nesnesi içinde tutulan hello verileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="49f56-290">DBCC SHOW_STATISTICS() shows hello data held within a statistics object.</span></span> <span data-ttu-id="49f56-291">Bu veriler üç bölümlerinde gelir.</span><span class="sxs-lookup"><span data-stu-id="49f56-291">This data comes in three parts.</span></span>

1. <span data-ttu-id="49f56-292">Üstbilgi</span><span class="sxs-lookup"><span data-stu-id="49f56-292">Header</span></span>
2. <span data-ttu-id="49f56-293">Yoğunluğu vektör</span><span class="sxs-lookup"><span data-stu-id="49f56-293">Density Vector</span></span>
3. <span data-ttu-id="49f56-294">Çubuk grafik</span><span class="sxs-lookup"><span data-stu-id="49f56-294">Histogram</span></span>

<span data-ttu-id="49f56-295">Merhaba istatistiklerde Hello üstbilgi meta veriler.</span><span class="sxs-lookup"><span data-stu-id="49f56-295">hello header metadata about hello statistics.</span></span> <span data-ttu-id="49f56-296">Merhaba histogram hello dağıtım değerlerin hello ilk anahtar sütununa hello istatistikleri nesnesinin görüntüler.</span><span class="sxs-lookup"><span data-stu-id="49f56-296">hello histogram displays hello distribution of values in hello first key column of hello statistics object.</span></span> <span data-ttu-id="49f56-297">Merhaba yoğunluğu vektör arası sütun bağıntı ölçer.</span><span class="sxs-lookup"><span data-stu-id="49f56-297">hello density vector measures cross-column correlation.</span></span> <span data-ttu-id="49f56-298">SQLDW kardinalite tahminlerde hello istatistikleri nesnesindeki hello verilerin hesaplar.</span><span class="sxs-lookup"><span data-stu-id="49f56-298">SQLDW computes cardinality estimates with any of hello data in hello statistics object.</span></span>

### <a name="show-header-density-and-histogram"></a><span data-ttu-id="49f56-299">Üstbilgi, yoğunluğu ve histogram Göster</span><span class="sxs-lookup"><span data-stu-id="49f56-299">Show header, density, and histogram</span></span>
<span data-ttu-id="49f56-300">Bu basit bir örnek istatistikleri nesnesinin tüm üç bölümlerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="49f56-300">This simple example shows all three parts of a statistics object.</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

<span data-ttu-id="49f56-301">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="49f56-301">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-showstatistics"></a><span data-ttu-id="49f56-302">DBCC SHOW_STATISTICS() bir veya daha fazla bölümlerini gösterme;</span><span class="sxs-lookup"><span data-stu-id="49f56-302">Show one or more parts of DBCC SHOW_STATISTICS();</span></span>
<span data-ttu-id="49f56-303">Yalnızca belirli bölümlerini görüntüleme ilgileniyorsanız, hello kullan `WITH` yan tümcesi ve hangi bölümleri belirtin toosee istiyor:</span><span class="sxs-lookup"><span data-stu-id="49f56-303">If you are only interested in viewing specific parts, use hello `WITH` clause and specify which parts you want toosee:</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

<span data-ttu-id="49f56-304">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="49f56-304">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-showstatistics-differences"></a><span data-ttu-id="49f56-305">DBCC SHOW_STATISTICS() farklar</span><span class="sxs-lookup"><span data-stu-id="49f56-305">DBCC SHOW_STATISTICS() differences</span></span>
<span data-ttu-id="49f56-306">DBCC SHOW_STATISTICS() daha kesinlikle SQL Data Warehouse karşılaştırıldığında tooSQL sunucu uygulanır.</span><span class="sxs-lookup"><span data-stu-id="49f56-306">DBCC SHOW_STATISTICS() is more strictly implemented in SQL Data Warehouse compared tooSQL Server.</span></span>

1. <span data-ttu-id="49f56-307">Belgelenmemiş özellikler desteklenmez</span><span class="sxs-lookup"><span data-stu-id="49f56-307">Undocumented features are not supported</span></span>
2. <span data-ttu-id="49f56-308">Stats_stream kullanamazsınız</span><span class="sxs-lookup"><span data-stu-id="49f56-308">Cannot use Stats_stream</span></span>
3. <span data-ttu-id="49f56-309">İstatistik verileri belirli alt kümeleri için sonuçlarını örneğin katılamıyor (STAT_HEADER birleştirme DENSITY_VECTOR)</span><span class="sxs-lookup"><span data-stu-id="49f56-309">Cannot join results for specific subsets of statistics data e.g. (STAT_HEADER JOIN DENSITY_VECTOR)</span></span>
4. <span data-ttu-id="49f56-310">NO_INFOMSGS ileti gizleme için ayarlanamaz</span><span class="sxs-lookup"><span data-stu-id="49f56-310">NO_INFOMSGS cannot be set for message suppression</span></span>
5. <span data-ttu-id="49f56-311">İstatistikleri adları köşeli ayraç kullanılamaz</span><span class="sxs-lookup"><span data-stu-id="49f56-311">Square brackets around statistics names cannot be used</span></span>
6. <span data-ttu-id="49f56-312">Sütun adları tooidentify istatistikleri nesneleri kullanamazsınız</span><span class="sxs-lookup"><span data-stu-id="49f56-312">Cannot use column names tooidentify statistics objects</span></span>
7. <span data-ttu-id="49f56-313">Özel hata 2767 desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="49f56-313">Custom error 2767 is not supported</span></span>

## <a name="next-steps"></a><span data-ttu-id="49f56-314">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="49f56-314">Next steps</span></span>
<span data-ttu-id="49f56-315">Daha fazla ayrıntı için bkz: [DBCC SHOW_STATISTICS] [ DBCC SHOW_STATISTICS] konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="49f56-315">For more details, see [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] on MSDN.</span></span>  <span data-ttu-id="49f56-316">toolearn daha hello makalelere bakın üzerinde [tablo genel bakışı][Overview], [tablo veri türleri][Data Types], [bir tablodağıtma] [ Distribute], [Tablo dizin][Index], [bir tablo bölümleme] [ Partition] ve [ Geçici tablolara][Temporary].</span><span class="sxs-lookup"><span data-stu-id="49f56-316">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="49f56-317">En iyi uygulamalar hakkında daha fazla bilgi için bkz: [SQL veri ambarı en iyi uygulamalar][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="49f56-317">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->  
[Cardinality Estimation]: https://msdn.microsoft.com/library/dn600374.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[DBCC SHOW_STATISTICS]:https://msdn.microsoft.com/library/ms174384.aspx
[Statistics]: https://msdn.microsoft.com/library/ms190397.aspx
[STATS_DATE]: https://msdn.microsoft.com/library/ms190330.aspx
[sys.columns]: https://msdn.microsoft.com/library/ms176106.aspx
[sys.objects]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.schemas]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.stats]: https://msdn.microsoft.com/library/ms177623.aspx
[sys.stats_columns]: https://msdn.microsoft.com/library/ms187340.aspx
[sys.tables]: https://msdn.microsoft.com/library/ms187406.aspx
[sys.table_types]: https://msdn.microsoft.com/library/bb510623.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx

<!--Other Web references-->  
