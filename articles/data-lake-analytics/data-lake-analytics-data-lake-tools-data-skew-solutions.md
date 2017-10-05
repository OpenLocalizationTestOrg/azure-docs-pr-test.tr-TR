---
title: "Visual Studio için Azure Data Lake araçları kullanarak veri eğme sorunlarını çözmek | Microsoft Docs"
description: "Visual Studio için Azure Data Lake araçları kullanarak veri eğme sorunları için sorun giderme olası çözümleri."
services: data-lake-analytics
documentationcenter: 
author: yanancai
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/16/2016
ms.author: yanacai
ms.openlocfilehash: 9b284ef33be4b935569fc368d81ddf040b2c2b7d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="3ac99-103">Visual Studio için Azure Data Lake araçları kullanarak veri eğme sorunlarını gidermek</span><span class="sxs-lookup"><span data-stu-id="3ac99-103">Resolve data-skew problems by using Azure Data Lake Tools for Visual Studio</span></span>

## <a name="what-is-data-skew"></a><span data-ttu-id="3ac99-104">Eğme veri nedir?</span><span class="sxs-lookup"><span data-stu-id="3ac99-104">What is data skew?</span></span>

<span data-ttu-id="3ac99-105">Kısaca belirtildiği gibi veri eğme bir aşırı gösterilen değeridir.</span><span class="sxs-lookup"><span data-stu-id="3ac99-105">Briefly stated, data skew is an over-represented value.</span></span> <span data-ttu-id="3ac99-106">Vergi döndürür, her ABD durumu için bir examiner denetlemek için 50 vergi examiners atadığınız düşünün.</span><span class="sxs-lookup"><span data-stu-id="3ac99-106">Imagine that you have assigned 50 tax examiners to audit tax returns, one examiner for each US state.</span></span> <span data-ttu-id="3ac99-107">Popülasyonun var. küçük olduğu için Wyoming examiner az yapmak için vardır.</span><span class="sxs-lookup"><span data-stu-id="3ac99-107">The Wyoming examiner, because the population there is small, has little to do.</span></span> <span data-ttu-id="3ac99-108">İzmir'de, ancak examiner durumun büyük popülasyon nedeniyle çok meşgul tutulur.</span><span class="sxs-lookup"><span data-stu-id="3ac99-108">In California, however, the examiner is kept very busy because of the state's large population.</span></span>
    <span data-ttu-id="3ac99-109">![Veri eğme sorun örneği](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span><span class="sxs-lookup"><span data-stu-id="3ac99-109">![Data-skew problem example](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span></span>

<span data-ttu-id="3ac99-110">Senaryomuzda verileri düz olmayan şekilde tüm vergi examiners arasında bazı examiners diğerlerinden daha çalışmalıdır anlamı dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="3ac99-110">In our scenario, the data is unevenly distributed across all tax examiners, which means that some examiners must work more than others.</span></span> <span data-ttu-id="3ac99-111">Kendi işinde sık vergi examiner örnek gibi durumlarla karşılaşırsınız.</span><span class="sxs-lookup"><span data-stu-id="3ac99-111">In your own job, you frequently experience situations like the tax-examiner example here.</span></span> <span data-ttu-id="3ac99-112">Daha fazla teknik koşulları bir köşesinin eşlerine çok daha fazla veri alır, projenin tamamı sonunda diğerlerinden daha fazla ve bu iş köşe yapan bir durum yavaşlatır.</span><span class="sxs-lookup"><span data-stu-id="3ac99-112">In more technical terms, one vertex gets much more data than its peers, a situation that makes the vertex work more than the others and that eventually slows down an entire job.</span></span> <span data-ttu-id="3ac99-113">Kötüsü, işi başarısız olabilir, köşe, örneğin, olabileceğinden 5 saatlik çalışma zamanı sınırlaması ve 6 GB bellek kısıtlaması.</span><span class="sxs-lookup"><span data-stu-id="3ac99-113">What's worse, the job might fail, because vertices might have, for example, a 5-hour runtime limitation and a 6-GB memory limitation.</span></span>

## <a name="resolving-data-skew-problems"></a><span data-ttu-id="3ac99-114">Veri eğme sorunlarını çözme</span><span class="sxs-lookup"><span data-stu-id="3ac99-114">Resolving data-skew problems</span></span>

<span data-ttu-id="3ac99-115">Visual Studio için Azure Data Lake araçları, işinizi veri eğme sorunlu olup olmadığını belirlemenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="3ac99-115">Azure Data Lake Tools for Visual Studio can help detect whether your job has a data-skew problem.</span></span> <span data-ttu-id="3ac99-116">Bir sorun varsa, bu bölümdeki çözümleri deneyerek çözülebilir.</span><span class="sxs-lookup"><span data-stu-id="3ac99-116">If a problem exists, you can resolve it by trying the solutions in this section.</span></span>

## <a name="solution-1-improve-table-partitioning"></a><span data-ttu-id="3ac99-117">Çözüm 1: Tablo bölümleme geliştirmek</span><span class="sxs-lookup"><span data-stu-id="3ac99-117">Solution 1: Improve table partitioning</span></span>

### <a name="option-1-filter-the-skewed-key-value-in-advance"></a><span data-ttu-id="3ac99-118">Seçenek 1: asimetrik anahtar değeri önceden filtre</span><span class="sxs-lookup"><span data-stu-id="3ac99-118">Option 1: Filter the skewed key value in advance</span></span>

<span data-ttu-id="3ac99-119">İş mantığınızın etkilemez varsa, yüksek sıklığı değerlerin önceden filtre uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ac99-119">If it does not affect your business logic, you can filter the higher-frequency values in advance.</span></span> <span data-ttu-id="3ac99-120">Örneğin, çok sayıda 000 000 000 GUID sütununda varsa, bu değer bir araya istemeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ac99-120">For example, if there are a lot of 000-000-000 in column GUID, you might not want to aggregate that value.</span></span> <span data-ttu-id="3ac99-121">Önce toplama, yazabileceğiniz "WHERE GUID!"000 000 000"=" yüksek sıklıkta değeri filtre uygulamak için.</span><span class="sxs-lookup"><span data-stu-id="3ac99-121">Before you aggregate, you can write “WHERE GUID != “000-000-000”” to filter the high-frequency value.</span></span>

### <a name="option-2-pick-a-different-partition-or-distribution-key"></a><span data-ttu-id="3ac99-122">Seçenek 2: farklı bir bölüm veya dağıtım anahtarı seçin</span><span class="sxs-lookup"><span data-stu-id="3ac99-122">Option 2: Pick a different partition or distribution key</span></span>

<span data-ttu-id="3ac99-123">Önceki örnekte, yalnızca vergi denetim iş yükü ülke'dünyanın dört bir yanındaki denetlemek istiyorsanız, anahtar olarak kimlik numarasını seçerek veri dağıtım artırabilir.</span><span class="sxs-lookup"><span data-stu-id="3ac99-123">In the preceding example, if you want only to check the tax-audit workload all over the country, you can improve the data distribution by selecting the ID number as your key.</span></span> <span data-ttu-id="3ac99-124">Farklı bir bölüm veya dağıtım anahtarı çekme bazen verileri daha eşit olarak dağıtabilirsiniz, ancak bu seçenek, iş mantığınızı etkilemez emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3ac99-124">Picking a different partition or distribution key can sometimes distribute the data more evenly, but you need to make sure that this choice doesn’t affect your business logic.</span></span> <span data-ttu-id="3ac99-125">Örneğin, her durum için vergi toplam hesaplamak için belirtmek istediğiniz _durumu_ bölüm anahtarı olarak.</span><span class="sxs-lookup"><span data-stu-id="3ac99-125">For instance, to calculate the tax sum for each state, you might want to designate _State_ as the partition key.</span></span> <span data-ttu-id="3ac99-126">Bu sorunu yaşamaya devam ederseniz, seçenek 3 kullanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="3ac99-126">If you continue to experience this problem, try using Option 3.</span></span>

### <a name="option-3-add-more-partition-or-distribution-keys"></a><span data-ttu-id="3ac99-127">Seçenek 3: daha fazla bölüm veya dağıtım anahtarları Ekle</span><span class="sxs-lookup"><span data-stu-id="3ac99-127">Option 3: Add more partition or distribution keys</span></span>

<span data-ttu-id="3ac99-128">Yalnızca kullanmak yerine _durumu_ bir bölüm anahtarı olarak bölümleme için birden fazla anahtar kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ac99-128">Instead of using only _State_ as a partition key, you can use more than one key for partitioning.</span></span> <span data-ttu-id="3ac99-129">Örneğin, eklemeyi göz önünde bulundurun _posta kodu_ veri bölüm boyutlarını küçültmek ve verileri daha eşit olarak dağıtmak için ek bölüm anahtarı olarak.</span><span class="sxs-lookup"><span data-stu-id="3ac99-129">For example, consider adding _ZIP Code_ as an additional partition key to reduce data-partition sizes and distribute the data more evenly.</span></span>

### <a name="option-4-use-round-robin-distribution"></a><span data-ttu-id="3ac99-130">Seçenek 4: hepsini dağıtım kullanın</span><span class="sxs-lookup"><span data-stu-id="3ac99-130">Option 4: Use round-robin distribution</span></span>

<span data-ttu-id="3ac99-131">Bölüm ve dağıtım için uygun bir anahtar bulamazsanız, hepsini dağıtım kullanmayı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ac99-131">If you cannot find an appropriate key for partition and distribution, you can try to use round-robin distribution.</span></span> <span data-ttu-id="3ac99-132">Hepsini dağıtım tüm satırları eşit olarak değerlendirir ve rastgele bunları karşılık gelen demet yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="3ac99-132">Round-robin distribution treats all rows equally and randomly puts them into corresponding buckets.</span></span> <span data-ttu-id="3ac99-133">Veri dağılımla, ancak yere göre bilgi, aynı zamanda bazı işlemler için iş performansı düşürebilir bir dezavantajı kaybeder.</span><span class="sxs-lookup"><span data-stu-id="3ac99-133">The data gets evenly distributed, but it loses locality information, a drawback that can also reduce job performance for some operations.</span></span> <span data-ttu-id="3ac99-134">Ayrıca, asimetrik anahtar için toplama yine de yapıyorsanız, veri eğme sorun korunur.</span><span class="sxs-lookup"><span data-stu-id="3ac99-134">Additionally, if you are doing aggregation for the skewed key anyway, the data-skew problem will persist.</span></span> <span data-ttu-id="3ac99-135">Hepsini bir kez deneme dağıtımı hakkında daha fazla bilgi için U-SQL tablo dağıtımları bölümüne bakın. [CREATE TABLE (U-SQL): şemasıyla tablo oluşturma](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span><span class="sxs-lookup"><span data-stu-id="3ac99-135">To learn more about round-robin distribution, see the U-SQL Table Distributions section in [CREATE TABLE (U-SQL): Creating a Table with Schema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span></span>

## <a name="solution-2-improve-the-query-plan"></a><span data-ttu-id="3ac99-136">Çözüm 2: sorgu planı geliştirmek</span><span class="sxs-lookup"><span data-stu-id="3ac99-136">Solution 2: Improve the query plan</span></span>

### <a name="option-1-use-the-create-statistics-statement"></a><span data-ttu-id="3ac99-137">Seçenek 1: CREATE STATISTICS deyimini kullanın</span><span class="sxs-lookup"><span data-stu-id="3ac99-137">Option 1: Use the CREATE STATISTICS statement</span></span>

<span data-ttu-id="3ac99-138">U-SQL CREATE STATISTICS deyimi tablolarda sağlar.</span><span class="sxs-lookup"><span data-stu-id="3ac99-138">U-SQL provides the CREATE STATISTICS statement on tables.</span></span> <span data-ttu-id="3ac99-139">Bu bildirimi sorgu iyileştiricisi bir tabloda depolanan verileri, gibi özellikleri değer dağıtımı hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="3ac99-139">This statement gives more information to the query optimizer about the data characteristics, such as value distribution, that are stored in a table.</span></span> <span data-ttu-id="3ac99-140">Sorguların çoğu için sorgu iyileştiricisi zaten bir yüksek kaliteli sorgu planı gerekli istatistikleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3ac99-140">For most queries, the query optimizer already generates the necessary statistics for a high-quality query plan.</span></span> <span data-ttu-id="3ac99-141">Bazen, CREATE STATISTICS ile ek istatistikler oluşturarak veya sorgu tasarım değiştirerek sorgu performansını artırmak gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="3ac99-141">Occasionally, you might need to improve query performance by creating additional statistics with CREATE STATISTICS or by modifying the query design.</span></span> <span data-ttu-id="3ac99-142">Daha fazla bilgi için bkz: [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) sayfası.</span><span class="sxs-lookup"><span data-stu-id="3ac99-142">For more information, see the [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) page.</span></span>

<span data-ttu-id="3ac99-143">Kod örneği:</span><span class="sxs-lookup"><span data-stu-id="3ac99-143">Code example:</span></span>

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
><span data-ttu-id="3ac99-144">İstatistik bilgileri otomatik olarak güncelleştirilmez.</span><span class="sxs-lookup"><span data-stu-id="3ac99-144">Statistics information is not updated automatically.</span></span> <span data-ttu-id="3ac99-145">Bir tablodaki verileri istatistikleri tekrar oluşturmak zorunda kalmadan güncelleştirirseniz, sorgu performansı reddet.</span><span class="sxs-lookup"><span data-stu-id="3ac99-145">If you update the data in a table without re-creating the statistics, the query performance might decline.</span></span>

### <a name="option-2-use-skewfactor"></a><span data-ttu-id="3ac99-146">Seçenek 2: SKEWFACTOR kullanın</span><span class="sxs-lookup"><span data-stu-id="3ac99-146">Option 2: Use SKEWFACTOR</span></span>

<span data-ttu-id="3ac99-147">Her durum için vergi toplamak istiyorsanız, GROUP BY durumu, veri eğme kaçınmak olmayan bir yaklaşım kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3ac99-147">If you want to sum the tax for each state, you must use GROUP BY state, an approach that doesn't avoid the data-skew problem.</span></span> <span data-ttu-id="3ac99-148">Ancak, böylece iyileştirici sizin için yürütme planı hazırlama veri eğme anahtarlarında tanımlamak için Sorgunuzdaki veri ipucu sağlar.</span><span class="sxs-lookup"><span data-stu-id="3ac99-148">However, you can provide a data hint in your query to identify data skew in keys so that the optimizer can prepare an execution plan for you.</span></span>

<span data-ttu-id="3ac99-149">Genellikle, parametre 0,5 ve konuya eğme ve 1 anlamı ağır eğme anlamı 0,5 ile 1 olarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ac99-149">Usually, you can set the parameter as 0.5 and 1, with 0.5 meaning not much skew and 1 meaning heavy skew.</span></span> <span data-ttu-id="3ac99-150">İpucu geçerli deyimi ve tüm aşağı akış deyimleri için yürütme planı iyileştirme etkilediğinden, olası key-wise toplama eğri önce ipucu eklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="3ac99-150">Because the hint affects execution-plan optimization for the current statement and all downstream statements, be sure to add the hint before the potential skewed key-wise aggregation.</span></span>

    SKEWFACTOR (columns) = x

    Provides a hint that the given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

<span data-ttu-id="3ac99-151">Kod örneği:</span><span class="sxs-lookup"><span data-stu-id="3ac99-151">Code example:</span></span>

    //Add a SKEWFACTOR hint.
    @Impressions =
        SELECT * FROM
        searchDM.SML.PageView(@start, @end) AS PageView
        OPTION(SKEWFACTOR(Query)=0.5)
        ;

    //Query 1 for key: Query, ClientId
    @Sessions =
        SELECT
            ClientId,
            Query,
            SUM(PageClicks) AS Clicks
        FROM
            @Impressions
        GROUP BY
            Query, ClientId
        ;

    //Query 2 for Key: Query
    @Display =
        SELECT * FROM @Sessions
            INNER JOIN @Campaigns
                ON @Sessions.Query == @Campaigns.Query
        ;   

### <a name="option-3-use-rowcount"></a><span data-ttu-id="3ac99-152">Seçenek 3: ROWCOUNT kullanın</span><span class="sxs-lookup"><span data-stu-id="3ac99-152">Option 3: Use ROWCOUNT</span></span>  
<span data-ttu-id="3ac99-153">Diğer birleştirilmiş satır kümesini küçük olduğunu biliyorsanız, SKEWFACTOR ek olarak, belirli eğri anahtarı birleşim durumlarda, size iyileştirici birleştirme önce U-SQL deyiminde ROWCOUNT ipucu ekleyerek söyleyebilir.</span><span class="sxs-lookup"><span data-stu-id="3ac99-153">In addition to SKEWFACTOR, for specific skewed-key join cases, if you know that the other joined row set is small, you can tell the optimizer by adding a ROWCOUNT hint in the U-SQL statement before JOIN.</span></span> <span data-ttu-id="3ac99-154">Bu şekilde, en iyi hale getirme performansını iyileştirmeye yardımcı olmak için bir yayın katılım stratejisi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ac99-154">This way, optimizer can choose a broadcast join strategy to help improve performance.</span></span> <span data-ttu-id="3ac99-155">ROWCOUNT veri eğme sorunu çözmezse, ancak bazı ek Yardım sunabileceğiniz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="3ac99-155">Be aware that ROWCOUNT does not resolve the data-skew problem, but it can offer some additional help.</span></span>

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

<span data-ttu-id="3ac99-156">Kod örneği:</span><span class="sxs-lookup"><span data-stu-id="3ac99-156">Code example:</span></span>

    //Unstructured (24-hour daily log impressions)
    @Huge   = EXTRACT ClientId int, ...
                FROM @"wasb://ads@wcentralus/2015/10/30/{*}.nif"
                ;

    //Small subset (that is, ForgetMe opt out)
    @Small  = SELECT * FROM @Huge
                WHERE Bing.ForgetMe(x,y,z)
                OPTION(ROWCOUNT=500)
                ;

    //Result (not enough information to determine simple broadcast JOIN)
    @Remove = SELECT * FROM Bing.Sessions
                INNER JOIN @Small ON Sessions.Client == @Small.Client
                ;

## <a name="solution-3-improve-the-user-defined-reducer-and-combiner"></a><span data-ttu-id="3ac99-157">Çözüm 3: kullanıcı tanımlı reducer ve birleştirici geliştirmek</span><span class="sxs-lookup"><span data-stu-id="3ac99-157">Solution 3: Improve the user-defined reducer and combiner</span></span>

<span data-ttu-id="3ac99-158">Karmaşık bir işlem mantığı ile mücadele etmek için bir kullanıcı tarafından tanımlanan işleci bazen yazabilir ve iyi yazılmış reducer ve birleştirici bir veri eğme sorun bazı durumlarda azaltmak.</span><span class="sxs-lookup"><span data-stu-id="3ac99-158">You can sometimes write a user-defined operator to deal with complicated process logic, and a well-written reducer and combiner might mitigate a data-skew problem in some cases.</span></span>

### <a name="option-1-use-a-recursive-reducer-if-possible"></a><span data-ttu-id="3ac99-159">Seçenek 1: bir özyinelemeli reducer mümkünse kullanın</span><span class="sxs-lookup"><span data-stu-id="3ac99-159">Option 1: Use a recursive reducer, if possible</span></span>

<span data-ttu-id="3ac99-160">Varsayılan olarak, kullanıcı tanımlı bir reducer anahtarı için iş azaltan anlamına tek köşe dağıtılmış özyinelemeli olmayan modda çalışır.</span><span class="sxs-lookup"><span data-stu-id="3ac99-160">By default, a user-defined reducer runs in non-recursive mode, which means that reduce work for a key is distributed into a single vertex.</span></span> <span data-ttu-id="3ac99-161">Ancak verilerinizi eğri, büyük veri kümeleri, tek bir köşe işlenmesi ve uzun bir süredir çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3ac99-161">But if your data is skewed, the huge data sets might be processed in a single vertex and run for a long time.</span></span>

<span data-ttu-id="3ac99-162">Performansı artırmak için kodunuzda özyinelemeli modunda çalışacak şekilde reducer tanımlamak için bir öznitelik ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ac99-162">To improve performance, you can add an attribute in your code to define reducer to run in recursive mode.</span></span> <span data-ttu-id="3ac99-163">Ardından, büyük veri kümeleri için birden çok köşeleri dağıtılabilen ve işinizi hızlandırır paralel olarak çalıştır.</span><span class="sxs-lookup"><span data-stu-id="3ac99-163">Then, the huge data sets can be distributed to multiple vertices and run in parallel, which speeds up your job.</span></span>

<span data-ttu-id="3ac99-164">Özyinelemeli olmayan reducer için özyinelemeli değiştirmek için algoritma ilişkilendirilebilir olduğundan emin olmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="3ac99-164">To change a non-recursive reducer to recursive, you need to make sure that your algorithm is associative.</span></span> <span data-ttu-id="3ac99-165">Örneğin, toplam ilişkilendirilebilir ve ORTANCA değil.</span><span class="sxs-lookup"><span data-stu-id="3ac99-165">For example, the sum is associative, and the median is not.</span></span> <span data-ttu-id="3ac99-166">Giriş ve çıkış reducer için aynı şema tutmak emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3ac99-166">You also need to make sure that the input and output for reducer keep the same schema.</span></span>

<span data-ttu-id="3ac99-167">Özyinelemeli reducer öznitelik:</span><span class="sxs-lookup"><span data-stu-id="3ac99-167">Attribute of recursive reducer:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]

<span data-ttu-id="3ac99-168">Kod örneği:</span><span class="sxs-lookup"><span data-stu-id="3ac99-168">Code example:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

### <a name="option-2-use-row-level-combiner-mode-if-possible"></a><span data-ttu-id="3ac99-169">Seçenek 2: satır düzeyi Birleştirici modu, mümkünse kullanın</span><span class="sxs-lookup"><span data-stu-id="3ac99-169">Option 2: Use row-level combiner mode, if possible</span></span>

<span data-ttu-id="3ac99-170">Benzer şekilde belirli eğri anahtarı birleşim durumlarda ROWCOUNT ipucu, böylece iş aynı anda çalıştırılabilecek birden çok köşe için çok büyük eğri anahtar değer kümeleri dağıtmak Birleştirici modu çalışır.</span><span class="sxs-lookup"><span data-stu-id="3ac99-170">Similar to the ROWCOUNT hint for specific skewed-key join cases, combiner mode tries to distribute huge skewed-key value sets to multiple vertices so that the work can be executed concurrently.</span></span> <span data-ttu-id="3ac99-171">Birleştirici modu veri eğme sorunları çözümlenemiyor ancak büyük eğri anahtar değer kümeleri için bazı ek Yardım sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="3ac99-171">Combiner mode can’t resolve data-skew issues, but it can offer some additional help for huge skewed-key value sets.</span></span>

<span data-ttu-id="3ac99-172">Varsayılan olarak, sol satır kümesi ve doğru satır kümesini ayırmanız edemiyor demektir tam Birleştirici modudur.</span><span class="sxs-lookup"><span data-stu-id="3ac99-172">By default, the combiner mode is Full, which means that the left row set and right row set cannot be separated.</span></span> <span data-ttu-id="3ac99-173">Sol/sağ/iç modunu ayarlama satır düzeyi birleştirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="3ac99-173">Setting the mode as Left/Right/Inner enables row-level join.</span></span> <span data-ttu-id="3ac99-174">Sistem, ilgili satır kümeleri ayırır ve bunları paralel olarak çalışan birden çok köşeleri uygulamasına dağıtır.</span><span class="sxs-lookup"><span data-stu-id="3ac99-174">The system separates the corresponding row sets and distributes them into multiple vertices that run in parallel.</span></span> <span data-ttu-id="3ac99-175">Ancak, birleştirici modu yapılandırmadan önce ilgili satır kümeleri birbirinden emin olmak dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="3ac99-175">However, before you configure the combiner mode, be careful to ensure that the corresponding row sets can be separated.</span></span>

<span data-ttu-id="3ac99-176">Aşağıdaki örnek, ayrılmış sol satır kümesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="3ac99-176">The example that follows shows a separated left row set.</span></span> <span data-ttu-id="3ac99-177">Tek bir giriş satır soldan her çıktı satır bağlıdır ve büyük olasılıkla tüm satırlardan aynı anahtar değeriyle sağ bağımlı.</span><span class="sxs-lookup"><span data-stu-id="3ac99-177">Each output row depends on a single input row from the left, and it potentially depends on all rows from the right with the same key value.</span></span> <span data-ttu-id="3ac99-178">Birleştirici modu sol ayarlarsanız, sistem büyük sol-küçük parçalara satır kümesi ayırır ve birden çok köşeleri atar.</span><span class="sxs-lookup"><span data-stu-id="3ac99-178">If you set the combiner mode as left, the system separates the huge left-row set into small ones and assigns them to multiple vertices.</span></span>

![Birleştirici modu çizim](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
><span data-ttu-id="3ac99-180">Yanlış Birleştirici modu ayarlarsanız, daha az verimli bir bileşimidir ve sonuçları bir sorun olabilir.</span><span class="sxs-lookup"><span data-stu-id="3ac99-180">If you set the wrong combiner mode, the combination is less efficient, and the results might be wrong.</span></span>

<span data-ttu-id="3ac99-181">Birleştirici modu öznitelikleri:</span><span class="sxs-lookup"><span data-stu-id="3ac99-181">Attributes of combiner mode:</span></span>

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all the input rows from left and right with the same key value.

- <span data-ttu-id="3ac99-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): Soldan (ve büyük olasılıkla tüm satırların aynı anahtar değeriyle sağdan) tek bir giriş satır her çıktı satır bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="3ac99-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): Every output row depends on a single input row from the left (and potentially all rows from the right with the same key value).</span></span>

- <span data-ttu-id="3ac99-183">qlUserDefinedCombiner(Mode=CombinerMode.Right): her çıktı satır sağa (ve büyük olasılıkla tüm satırların aynı anahtar değeriyle soldan) tek bir giriş satır bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="3ac99-183">qlUserDefinedCombiner(Mode=CombinerMode.Right): Every output row depends on a single input row from the right (and potentially all rows from the left with the same key value).</span></span>

- <span data-ttu-id="3ac99-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Sol ve sağda aynı değere sahip tek bir giriş satırdaki her çıktı satır bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="3ac99-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Every output row depends on a single input row from the left and the right with the same value.</span></span>

<span data-ttu-id="3ac99-185">Kod örneği:</span><span class="sxs-lookup"><span data-stu-id="3ac99-185">Code example:</span></span>

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }
