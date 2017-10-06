---
title: "Visual Studio için Azure Data Lake araçları kullanarak aaaResolve veri eğme sorunları | Microsoft Docs"
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
ms.openlocfilehash: 3909fbd89eb40f061268cb7128f7fa84a3c33de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="8e394-103">Visual Studio için Azure Data Lake araçları kullanarak veri eğme sorunlarını gidermek</span><span class="sxs-lookup"><span data-stu-id="8e394-103">Resolve data-skew problems by using Azure Data Lake Tools for Visual Studio</span></span>

## <a name="what-is-data-skew"></a><span data-ttu-id="8e394-104">Eğme veri nedir?</span><span class="sxs-lookup"><span data-stu-id="8e394-104">What is data skew?</span></span>

<span data-ttu-id="8e394-105">Kısaca belirtildiği gibi veri eğme bir aşırı gösterilen değeridir.</span><span class="sxs-lookup"><span data-stu-id="8e394-105">Briefly stated, data skew is an over-represented value.</span></span> <span data-ttu-id="8e394-106">Tooaudit vergi döndürür, her ABD durumu için bir examiner atanan 50 vergi examiners düşünün.</span><span class="sxs-lookup"><span data-stu-id="8e394-106">Imagine that you have assigned 50 tax examiners tooaudit tax returns, one examiner for each US state.</span></span> <span data-ttu-id="8e394-107">Merhaba popülasyon küçük olduğu için hello Wyoming examiner az toodo sahiptir.</span><span class="sxs-lookup"><span data-stu-id="8e394-107">hello Wyoming examiner, because hello population there is small, has little toodo.</span></span> <span data-ttu-id="8e394-108">İzmir'de, ancak hello examiner hello durumun büyük popülasyon nedeniyle çok meşgul tutulur.</span><span class="sxs-lookup"><span data-stu-id="8e394-108">In California, however, hello examiner is kept very busy because of hello state's large population.</span></span>
    <span data-ttu-id="8e394-109">![Veri eğme sorun örneği](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span><span class="sxs-lookup"><span data-stu-id="8e394-109">![Data-skew problem example](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span></span>

<span data-ttu-id="8e394-110">Senaryomuzda hello veri düz olmayan şekilde tüm vergi examiners arasında bazı examiners diğerlerinden daha çalışmalıdır anlamı dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="8e394-110">In our scenario, hello data is unevenly distributed across all tax examiners, which means that some examiners must work more than others.</span></span> <span data-ttu-id="8e394-111">Kendi işinde sık hello vergi examiner örnek gibi durumlarla karşılaşırsınız.</span><span class="sxs-lookup"><span data-stu-id="8e394-111">In your own job, you frequently experience situations like hello tax-examiner example here.</span></span> <span data-ttu-id="8e394-112">Daha fazla teknik terimlerinde bir köşesinin çok daha fazla veri eşlerine, diğerleri ve, projenin tamamı yavaşlatır sonunda hello birden fazla iş hello köşe yapan bir durum alır.</span><span class="sxs-lookup"><span data-stu-id="8e394-112">In more technical terms, one vertex gets much more data than its peers, a situation that makes hello vertex work more than hello others and that eventually slows down an entire job.</span></span> <span data-ttu-id="8e394-113">Kötüsü, hello işi başarısız olabilir, köşe, örneğin, olabileceğinden 5 saatlik çalışma zamanı sınırlaması ve 6 GB bellek kısıtlaması.</span><span class="sxs-lookup"><span data-stu-id="8e394-113">What's worse, hello job might fail, because vertices might have, for example, a 5-hour runtime limitation and a 6-GB memory limitation.</span></span>

## <a name="resolving-data-skew-problems"></a><span data-ttu-id="8e394-114">Veri eğme sorunlarını çözme</span><span class="sxs-lookup"><span data-stu-id="8e394-114">Resolving data-skew problems</span></span>

<span data-ttu-id="8e394-115">Visual Studio için Azure Data Lake araçları, işinizi veri eğme sorunlu olup olmadığını belirlemenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="8e394-115">Azure Data Lake Tools for Visual Studio can help detect whether your job has a data-skew problem.</span></span> <span data-ttu-id="8e394-116">Bir sorun varsa, bu bölümdeki hello çözümleri deneyerek çözülebilir.</span><span class="sxs-lookup"><span data-stu-id="8e394-116">If a problem exists, you can resolve it by trying hello solutions in this section.</span></span>

## <a name="solution-1-improve-table-partitioning"></a><span data-ttu-id="8e394-117">Çözüm 1: Tablo bölümleme geliştirmek</span><span class="sxs-lookup"><span data-stu-id="8e394-117">Solution 1: Improve table partitioning</span></span>

### <a name="option-1-filter-hello-skewed-key-value-in-advance"></a><span data-ttu-id="8e394-118">Seçenek 1: Anahtar değeri filtre hello önceden eğri</span><span class="sxs-lookup"><span data-stu-id="8e394-118">Option 1: Filter hello skewed key value in advance</span></span>

<span data-ttu-id="8e394-119">İş mantığınızın etkilemez varsa hello yüksek sıklığı değerleri önceden filtre uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e394-119">If it does not affect your business logic, you can filter hello higher-frequency values in advance.</span></span> <span data-ttu-id="8e394-120">Örneğin, çok sayıda 000 000 000 GUID sütununda varsa, tooaggregate bu değeri istemeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e394-120">For example, if there are a lot of 000-000-000 in column GUID, you might not want tooaggregate that value.</span></span> <span data-ttu-id="8e394-121">Önce toplama, yazabileceğiniz "WHERE GUID!"000 000 000"=" toofilter hello yüksek sıklıkta değeri.</span><span class="sxs-lookup"><span data-stu-id="8e394-121">Before you aggregate, you can write “WHERE GUID != “000-000-000”” toofilter hello high-frequency value.</span></span>

### <a name="option-2-pick-a-different-partition-or-distribution-key"></a><span data-ttu-id="8e394-122">Seçenek 2: farklı bir bölüm veya dağıtım anahtarı seçin</span><span class="sxs-lookup"><span data-stu-id="8e394-122">Option 2: Pick a different partition or distribution key</span></span>

<span data-ttu-id="8e394-123">Örnek, önceki hello yalnızca toocheck hello vergi denetim iş yükü istiyorsanız tüm üzerinden ülke Merhaba, anahtarınızı olarak hello kimlik numarasını seçerek hello veri dağıtım artırabilir.</span><span class="sxs-lookup"><span data-stu-id="8e394-123">In hello preceding example, if you want only toocheck hello tax-audit workload all over hello country, you can improve hello data distribution by selecting hello ID number as your key.</span></span> <span data-ttu-id="8e394-124">Farklı bir bölüm veya dağıtım anahtarı çekme bazen hello veri daha eşit olarak dağıtabilirsiniz, ancak bu seçenek, iş mantığınızı etkilemez emin toomake gerekir.</span><span class="sxs-lookup"><span data-stu-id="8e394-124">Picking a different partition or distribution key can sometimes distribute hello data more evenly, but you need toomake sure that this choice doesn’t affect your business logic.</span></span> <span data-ttu-id="8e394-125">Örneğin, toocalculate hello vergi toplam her durum için toodesignate isteyebilirsiniz _durumu_ hello bölüm anahtarı olarak.</span><span class="sxs-lookup"><span data-stu-id="8e394-125">For instance, toocalculate hello tax sum for each state, you might want toodesignate _State_ as hello partition key.</span></span> <span data-ttu-id="8e394-126">Bu sorunu tooexperience devam ederseniz, seçenek 3 kullanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="8e394-126">If you continue tooexperience this problem, try using Option 3.</span></span>

### <a name="option-3-add-more-partition-or-distribution-keys"></a><span data-ttu-id="8e394-127">Seçenek 3: daha fazla bölüm veya dağıtım anahtarları Ekle</span><span class="sxs-lookup"><span data-stu-id="8e394-127">Option 3: Add more partition or distribution keys</span></span>

<span data-ttu-id="8e394-128">Yalnızca kullanmak yerine _durumu_ bir bölüm anahtarı olarak bölümleme için birden fazla anahtar kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e394-128">Instead of using only _State_ as a partition key, you can use more than one key for partitioning.</span></span> <span data-ttu-id="8e394-129">Örneğin, eklemeyi göz önünde bulundurun _posta kodu_ ek bir bölümü olarak anahtar tooreduce veri bölümü boyutları ve hello veri daha eşit olarak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="8e394-129">For example, consider adding _ZIP Code_ as an additional partition key tooreduce data-partition sizes and distribute hello data more evenly.</span></span>

### <a name="option-4-use-round-robin-distribution"></a><span data-ttu-id="8e394-130">Seçenek 4: hepsini dağıtım kullanın</span><span class="sxs-lookup"><span data-stu-id="8e394-130">Option 4: Use round-robin distribution</span></span>

<span data-ttu-id="8e394-131">Bölüm ve dağıtım için uygun bir anahtar bulamazsanız, toouse hepsini dağıtım deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e394-131">If you cannot find an appropriate key for partition and distribution, you can try toouse round-robin distribution.</span></span> <span data-ttu-id="8e394-132">Hepsini dağıtım tüm satırları eşit olarak değerlendirir ve rastgele bunları karşılık gelen demet yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="8e394-132">Round-robin distribution treats all rows equally and randomly puts them into corresponding buckets.</span></span> <span data-ttu-id="8e394-133">Merhaba veri dağılımla, ancak yere göre bilgi, aynı zamanda bazı işlemler için iş performansı düşürebilir bir dezavantajı kaybeder.</span><span class="sxs-lookup"><span data-stu-id="8e394-133">hello data gets evenly distributed, but it loses locality information, a drawback that can also reduce job performance for some operations.</span></span> <span data-ttu-id="8e394-134">Ayrıca, toplama hello çarpık anahtarı için yine de yapıyorsanız, hello veri eğme sorun korunur.</span><span class="sxs-lookup"><span data-stu-id="8e394-134">Additionally, if you are doing aggregation for hello skewed key anyway, hello data-skew problem will persist.</span></span> <span data-ttu-id="8e394-135">toolearn hepsini dağıtım hakkında daha fazla bilgi görmek hello U-SQL tablo dağıtımları bölümüne [CREATE TABLE (U-SQL): şemasıyla tablo oluşturma](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span><span class="sxs-lookup"><span data-stu-id="8e394-135">toolearn more about round-robin distribution, see hello U-SQL Table Distributions section in [CREATE TABLE (U-SQL): Creating a Table with Schema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span></span>

## <a name="solution-2-improve-hello-query-plan"></a><span data-ttu-id="8e394-136">Çözüm 2: hello sorgu planı geliştirmek</span><span class="sxs-lookup"><span data-stu-id="8e394-136">Solution 2: Improve hello query plan</span></span>

### <a name="option-1-use-hello-create-statistics-statement"></a><span data-ttu-id="8e394-137">Seçenek 1: hello CREATE STATISTICS deyimini kullanın</span><span class="sxs-lookup"><span data-stu-id="8e394-137">Option 1: Use hello CREATE STATISTICS statement</span></span>

<span data-ttu-id="8e394-138">U-SQL hello CREATE STATISTICS deyimi tablolarda sağlar.</span><span class="sxs-lookup"><span data-stu-id="8e394-138">U-SQL provides hello CREATE STATISTICS statement on tables.</span></span> <span data-ttu-id="8e394-139">Bu deyim bir tabloda depolanan hello veri özellikleri, değer dağıtımı gibi hakkında daha fazla bilgi toohello sorgu iyileştiricisi sağlar.</span><span class="sxs-lookup"><span data-stu-id="8e394-139">This statement gives more information toohello query optimizer about hello data characteristics, such as value distribution, that are stored in a table.</span></span> <span data-ttu-id="8e394-140">Sorguların çoğu için hello sorgu iyileştiricisi zaten bir yüksek kaliteli sorgu planı için gerekli istatistikleri hello oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8e394-140">For most queries, hello query optimizer already generates hello necessary statistics for a high-quality query plan.</span></span> <span data-ttu-id="8e394-141">Bazen, CREATE STATISTICS ile ek istatistikler oluşturarak veya hello sorgu tasarımı değiştirerek tooimprove sorgu performansı gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="8e394-141">Occasionally, you might need tooimprove query performance by creating additional statistics with CREATE STATISTICS or by modifying hello query design.</span></span> <span data-ttu-id="8e394-142">Daha fazla bilgi için bkz: Merhaba [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) sayfası.</span><span class="sxs-lookup"><span data-stu-id="8e394-142">For more information, see hello [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) page.</span></span>

<span data-ttu-id="8e394-143">Kod örneği:</span><span class="sxs-lookup"><span data-stu-id="8e394-143">Code example:</span></span>

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
><span data-ttu-id="8e394-144">İstatistik bilgileri otomatik olarak güncelleştirilmez.</span><span class="sxs-lookup"><span data-stu-id="8e394-144">Statistics information is not updated automatically.</span></span> <span data-ttu-id="8e394-145">Bir tablodaki hello verileri hello istatistikleri tekrar oluşturmak zorunda kalmadan güncelleştirirseniz, hello sorgu performansı reddetme.</span><span class="sxs-lookup"><span data-stu-id="8e394-145">If you update hello data in a table without re-creating hello statistics, hello query performance might decline.</span></span>

### <a name="option-2-use-skewfactor"></a><span data-ttu-id="8e394-146">Seçenek 2: SKEWFACTOR kullanın</span><span class="sxs-lookup"><span data-stu-id="8e394-146">Option 2: Use SKEWFACTOR</span></span>

<span data-ttu-id="8e394-147">Her durum için toosum hello vergi istiyorsanız, GROUP BY durumu, hello veri eğme kaçınmak olmayan bir yaklaşım kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8e394-147">If you want toosum hello tax for each state, you must use GROUP BY state, an approach that doesn't avoid hello data-skew problem.</span></span> <span data-ttu-id="8e394-148">Ancak, böylece hello iyileştirici sizin için yürütme planı hazırlama veri anahtarlarında eğme, sorgu tooidentify veri ipucu sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="8e394-148">However, you can provide a data hint in your query tooidentify data skew in keys so that hello optimizer can prepare an execution plan for you.</span></span>

<span data-ttu-id="8e394-149">Genellikle, hello parametre 0,5 ve konuya eğme ve 1 anlamı ağır eğme anlamı 0,5 ile 1 olarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e394-149">Usually, you can set hello parameter as 0.5 and 1, with 0.5 meaning not much skew and 1 meaning heavy skew.</span></span> <span data-ttu-id="8e394-150">Merhaba ipucu hello geçerli deyimi ve tüm aşağı akış deyimleri için yürütme planı iyileştirme etkilediğinden, olası hello key-wise toplama eğri önce emin tooadd hello ipucu olması.</span><span class="sxs-lookup"><span data-stu-id="8e394-150">Because hello hint affects execution-plan optimization for hello current statement and all downstream statements, be sure tooadd hello hint before hello potential skewed key-wise aggregation.</span></span>

    SKEWFACTOR (columns) = x

    Provides a hint that hello given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

<span data-ttu-id="8e394-151">Kod örneği:</span><span class="sxs-lookup"><span data-stu-id="8e394-151">Code example:</span></span>

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

### <a name="option-3-use-rowcount"></a><span data-ttu-id="8e394-152">Seçenek 3: ROWCOUNT kullanın</span><span class="sxs-lookup"><span data-stu-id="8e394-152">Option 3: Use ROWCOUNT</span></span>  
<span data-ttu-id="8e394-153">Ayrıca belirli eğri anahtarı için tooSKEWFACTOR katılma durumlarda, bu hello biliyorsanız diğer birleştirilmiş satır kümesini küçük, birleştirme önce hello U-SQL deyiminde ROWCOUNT ipucu ekleyerek hello iyileştirici anlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e394-153">In addition tooSKEWFACTOR, for specific skewed-key join cases, if you know that hello other joined row set is small, you can tell hello optimizer by adding a ROWCOUNT hint in hello U-SQL statement before JOIN.</span></span> <span data-ttu-id="8e394-154">Bu şekilde, bir yayın katılım stratejisi toohelp performansı artırır iyileştirici seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e394-154">This way, optimizer can choose a broadcast join strategy toohelp improve performance.</span></span> <span data-ttu-id="8e394-155">ROWCOUNT hello veri eğme sorunu çözmezse, ancak bazı ek Yardım sunabileceğiniz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8e394-155">Be aware that ROWCOUNT does not resolve hello data-skew problem, but it can offer some additional help.</span></span>

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

<span data-ttu-id="8e394-156">Kod örneği:</span><span class="sxs-lookup"><span data-stu-id="8e394-156">Code example:</span></span>

    //Unstructured (24-hour daily log impressions)
    @Huge   = EXTRACT ClientId int, ...
                FROM @"wasb://ads@wcentralus/2015/10/30/{*}.nif"
                ;

    //Small subset (that is, ForgetMe opt out)
    @Small  = SELECT * FROM @Huge
                WHERE Bing.ForgetMe(x,y,z)
                OPTION(ROWCOUNT=500)
                ;

    //Result (not enough information toodetermine simple broadcast JOIN)
    @Remove = SELECT * FROM Bing.Sessions
                INNER JOIN @Small ON Sessions.Client == @Small.Client
                ;

## <a name="solution-3-improve-hello-user-defined-reducer-and-combiner"></a><span data-ttu-id="8e394-157">Çözüm 3: hello kullanıcı tanımlı reducer ve birleştirici geliştirmek</span><span class="sxs-lookup"><span data-stu-id="8e394-157">Solution 3: Improve hello user-defined reducer and combiner</span></span>

<span data-ttu-id="8e394-158">Karmaşık bir işlem mantığı ile bir kullanıcı tarafından tanımlanan işleci toodeal bazen yazabilir ve iyi yazılmış reducer ve birleştirici bir veri eğme sorun bazı durumlarda azaltmak.</span><span class="sxs-lookup"><span data-stu-id="8e394-158">You can sometimes write a user-defined operator toodeal with complicated process logic, and a well-written reducer and combiner might mitigate a data-skew problem in some cases.</span></span>

### <a name="option-1-use-a-recursive-reducer-if-possible"></a><span data-ttu-id="8e394-159">Seçenek 1: bir özyinelemeli reducer mümkünse kullanın</span><span class="sxs-lookup"><span data-stu-id="8e394-159">Option 1: Use a recursive reducer, if possible</span></span>

<span data-ttu-id="8e394-160">Varsayılan olarak, kullanıcı tanımlı bir reducer anahtarı için iş azaltan anlamına tek köşe dağıtılmış özyinelemeli olmayan modda çalışır.</span><span class="sxs-lookup"><span data-stu-id="8e394-160">By default, a user-defined reducer runs in non-recursive mode, which means that reduce work for a key is distributed into a single vertex.</span></span> <span data-ttu-id="8e394-161">Ancak, verilerinizi eğri, hello büyük veri kümeleri içinde tek bir köşe işlenen ve uzun bir süredir çalıştırabilir.</span><span class="sxs-lookup"><span data-stu-id="8e394-161">But if your data is skewed, hello huge data sets might be processed in a single vertex and run for a long time.</span></span>

<span data-ttu-id="8e394-162">tooimprove performans, kod toodefine reducer toorun özyinelemeli modunda bir öznitelik ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e394-162">tooimprove performance, you can add an attribute in your code toodefine reducer toorun in recursive mode.</span></span> <span data-ttu-id="8e394-163">Ardından, hello büyük veri kümeleri dağıtılmış toomultiple köşeleri olması ve işinizi hızlandırır paralel çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8e394-163">Then, hello huge data sets can be distributed toomultiple vertices and run in parallel, which speeds up your job.</span></span>

<span data-ttu-id="8e394-164">bir özyinelemeli olmayan reducer toorecursive toochange toomake, algoritma ilişkilendirilebilir olmasını gerekir.</span><span class="sxs-lookup"><span data-stu-id="8e394-164">toochange a non-recursive reducer toorecursive, you need toomake sure that your algorithm is associative.</span></span> <span data-ttu-id="8e394-165">Örneğin, hello toplam ilişkilendirilebilir ve hello ORTANCA değil.</span><span class="sxs-lookup"><span data-stu-id="8e394-165">For example, hello sum is associative, and hello median is not.</span></span> <span data-ttu-id="8e394-166">Toomake hello giriş ve çıkış reducer için hello tutmak emin etmeniz aynı şema.</span><span class="sxs-lookup"><span data-stu-id="8e394-166">You also need toomake sure that hello input and output for reducer keep hello same schema.</span></span>

<span data-ttu-id="8e394-167">Özyinelemeli reducer öznitelik:</span><span class="sxs-lookup"><span data-stu-id="8e394-167">Attribute of recursive reducer:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]

<span data-ttu-id="8e394-168">Kod örneği:</span><span class="sxs-lookup"><span data-stu-id="8e394-168">Code example:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

### <a name="option-2-use-row-level-combiner-mode-if-possible"></a><span data-ttu-id="8e394-169">Seçenek 2: satır düzeyi Birleştirici modu, mümkünse kullanın</span><span class="sxs-lookup"><span data-stu-id="8e394-169">Option 2: Use row-level combiner mode, if possible</span></span>

<span data-ttu-id="8e394-170">Böylece Hello iş aynı anda çalıştırılabilecek benzer toohello ROWCOUNT ipucu belirli eğri anahtarı birleşim durumlarda Birleştirici modu toodistribute büyük eğri anahtar değer kümeleri toomultiple köşeleri çalışır.</span><span class="sxs-lookup"><span data-stu-id="8e394-170">Similar toohello ROWCOUNT hint for specific skewed-key join cases, combiner mode tries toodistribute huge skewed-key value sets toomultiple vertices so that hello work can be executed concurrently.</span></span> <span data-ttu-id="8e394-171">Birleştirici modu veri eğme sorunları çözümlenemiyor ancak büyük eğri anahtar değer kümeleri için bazı ek Yardım sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="8e394-171">Combiner mode can’t resolve data-skew issues, but it can offer some additional help for huge skewed-key value sets.</span></span>

<span data-ttu-id="8e394-172">Varsayılan olarak, satır kümesi hello sol ve sağ satır kümesi ayrılmış anlamına gelir tam hello Birleştirici modudur.</span><span class="sxs-lookup"><span data-stu-id="8e394-172">By default, hello combiner mode is Full, which means that hello left row set and right row set cannot be separated.</span></span> <span data-ttu-id="8e394-173">Satır düzeyi birleştirme sol/sağ/iç olarak hello modu ayarı sağlar.</span><span class="sxs-lookup"><span data-stu-id="8e394-173">Setting hello mode as Left/Right/Inner enables row-level join.</span></span> <span data-ttu-id="8e394-174">Merhaba sistem hello karşılık gelen satır kümeleri ayırır ve bunları paralel olarak çalışan birden çok köşeleri uygulamasına dağıtır.</span><span class="sxs-lookup"><span data-stu-id="8e394-174">hello system separates hello corresponding row sets and distributes them into multiple vertices that run in parallel.</span></span> <span data-ttu-id="8e394-175">Ancak, hello Birleştirici modu yapılandırmadan önce ilgili satır kümeleri hello tooensure ayrılmış dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="8e394-175">However, before you configure hello combiner mode, be careful tooensure that hello corresponding row sets can be separated.</span></span>

<span data-ttu-id="8e394-176">izleyen hello örnek ayrılmış sol satır kümesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="8e394-176">hello example that follows shows a separated left row set.</span></span> <span data-ttu-id="8e394-177">Tek bir giriş satır hello soldan her çıktı satır bağlıdır ve büyük olasılıkla hello sağ hello ile alınan tüm satırların aynı bağımlı anahtar değeri.</span><span class="sxs-lookup"><span data-stu-id="8e394-177">Each output row depends on a single input row from hello left, and it potentially depends on all rows from hello right with hello same key value.</span></span> <span data-ttu-id="8e394-178">Merhaba Birleştirici modu sol ayarlarsanız, hello sistem hello büyük sol-satır kümesi küçük parçalara ayırır ve toomultiple köşeleri atar.</span><span class="sxs-lookup"><span data-stu-id="8e394-178">If you set hello combiner mode as left, hello system separates hello huge left-row set into small ones and assigns them toomultiple vertices.</span></span>

![Birleştirici modu çizim](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
><span data-ttu-id="8e394-180">Merhaba yanlış Birleştirici modu ayarlarsanız hello birlikte daha az verimlidir ve hello sonuçlar hatalı olabilir.</span><span class="sxs-lookup"><span data-stu-id="8e394-180">If you set hello wrong combiner mode, hello combination is less efficient, and hello results might be wrong.</span></span>

<span data-ttu-id="8e394-181">Birleştirici modu öznitelikleri:</span><span class="sxs-lookup"><span data-stu-id="8e394-181">Attributes of combiner mode:</span></span>

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all hello input rows from left and right with hello same key value.

- <span data-ttu-id="8e394-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): Tek bir giriş satır hello soldan her çıktı satır bağlıdır (ve büyük olasılıkla tüm satırları hello hello sağ ile aynı anahtar değeri).</span><span class="sxs-lookup"><span data-stu-id="8e394-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): Every output row depends on a single input row from hello left (and potentially all rows from hello right with hello same key value).</span></span>

- <span data-ttu-id="8e394-183">qlUserDefinedCombiner(Mode=CombinerMode.Right): hello sağ tek giriş satırdan her çıktı satır bağlıdır (ve büyük olasılıkla tüm satırları hello ile Merhaba soldan aynı anahtar değeri).</span><span class="sxs-lookup"><span data-stu-id="8e394-183">qlUserDefinedCombiner(Mode=CombinerMode.Right): Every output row depends on a single input row from hello right (and potentially all rows from hello left with hello same key value).</span></span>

- <span data-ttu-id="8e394-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Her çıktı satır hello sol ve sağ hello ile Merhaba tek bir giriş satır aynı bağlıdır değeri.</span><span class="sxs-lookup"><span data-stu-id="8e394-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Every output row depends on a single input row from hello left and hello right with hello same value.</span></span>

<span data-ttu-id="8e394-185">Kod örneği:</span><span class="sxs-lookup"><span data-stu-id="8e394-185">Code example:</span></span>

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }
