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
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a>Visual Studio için Azure Data Lake araçları kullanarak veri eğme sorunlarını gidermek

## <a name="what-is-data-skew"></a>Eğme veri nedir?

Kısaca belirtildiği gibi veri eğme bir aşırı gösterilen değeridir. Tooaudit vergi döndürür, her ABD durumu için bir examiner atanan 50 vergi examiners düşünün. Merhaba popülasyon küçük olduğu için hello Wyoming examiner az toodo sahiptir. İzmir'de, ancak hello examiner hello durumun büyük popülasyon nedeniyle çok meşgul tutulur.
    ![Veri eğme sorun örneği](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)

Senaryomuzda hello veri düz olmayan şekilde tüm vergi examiners arasında bazı examiners diğerlerinden daha çalışmalıdır anlamı dağıtılır. Kendi işinde sık hello vergi examiner örnek gibi durumlarla karşılaşırsınız. Daha fazla teknik terimlerinde bir köşesinin çok daha fazla veri eşlerine, diğerleri ve, projenin tamamı yavaşlatır sonunda hello birden fazla iş hello köşe yapan bir durum alır. Kötüsü, hello işi başarısız olabilir, köşe, örneğin, olabileceğinden 5 saatlik çalışma zamanı sınırlaması ve 6 GB bellek kısıtlaması.

## <a name="resolving-data-skew-problems"></a>Veri eğme sorunlarını çözme

Visual Studio için Azure Data Lake araçları, işinizi veri eğme sorunlu olup olmadığını belirlemenize yardımcı olabilir. Bir sorun varsa, bu bölümdeki hello çözümleri deneyerek çözülebilir.

## <a name="solution-1-improve-table-partitioning"></a>Çözüm 1: Tablo bölümleme geliştirmek

### <a name="option-1-filter-hello-skewed-key-value-in-advance"></a>Seçenek 1: Anahtar değeri filtre hello önceden eğri

İş mantığınızın etkilemez varsa hello yüksek sıklığı değerleri önceden filtre uygulayabilirsiniz. Örneğin, çok sayıda 000 000 000 GUID sütununda varsa, tooaggregate bu değeri istemeyebilirsiniz. Önce toplama, yazabileceğiniz "WHERE GUID!"000 000 000"=" toofilter hello yüksek sıklıkta değeri.

### <a name="option-2-pick-a-different-partition-or-distribution-key"></a>Seçenek 2: farklı bir bölüm veya dağıtım anahtarı seçin

Örnek, önceki hello yalnızca toocheck hello vergi denetim iş yükü istiyorsanız tüm üzerinden ülke Merhaba, anahtarınızı olarak hello kimlik numarasını seçerek hello veri dağıtım artırabilir. Farklı bir bölüm veya dağıtım anahtarı çekme bazen hello veri daha eşit olarak dağıtabilirsiniz, ancak bu seçenek, iş mantığınızı etkilemez emin toomake gerekir. Örneğin, toocalculate hello vergi toplam her durum için toodesignate isteyebilirsiniz _durumu_ hello bölüm anahtarı olarak. Bu sorunu tooexperience devam ederseniz, seçenek 3 kullanmayı deneyin.

### <a name="option-3-add-more-partition-or-distribution-keys"></a>Seçenek 3: daha fazla bölüm veya dağıtım anahtarları Ekle

Yalnızca kullanmak yerine _durumu_ bir bölüm anahtarı olarak bölümleme için birden fazla anahtar kullanabilirsiniz. Örneğin, eklemeyi göz önünde bulundurun _posta kodu_ ek bir bölümü olarak anahtar tooreduce veri bölümü boyutları ve hello veri daha eşit olarak dağıtın.

### <a name="option-4-use-round-robin-distribution"></a>Seçenek 4: hepsini dağıtım kullanın

Bölüm ve dağıtım için uygun bir anahtar bulamazsanız, toouse hepsini dağıtım deneyebilirsiniz. Hepsini dağıtım tüm satırları eşit olarak değerlendirir ve rastgele bunları karşılık gelen demet yerleştirir. Merhaba veri dağılımla, ancak yere göre bilgi, aynı zamanda bazı işlemler için iş performansı düşürebilir bir dezavantajı kaybeder. Ayrıca, toplama hello çarpık anahtarı için yine de yapıyorsanız, hello veri eğme sorun korunur. toolearn hepsini dağıtım hakkında daha fazla bilgi görmek hello U-SQL tablo dağıtımları bölümüne [CREATE TABLE (U-SQL): şemasıyla tablo oluşturma](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).

## <a name="solution-2-improve-hello-query-plan"></a>Çözüm 2: hello sorgu planı geliştirmek

### <a name="option-1-use-hello-create-statistics-statement"></a>Seçenek 1: hello CREATE STATISTICS deyimini kullanın

U-SQL hello CREATE STATISTICS deyimi tablolarda sağlar. Bu deyim bir tabloda depolanan hello veri özellikleri, değer dağıtımı gibi hakkında daha fazla bilgi toohello sorgu iyileştiricisi sağlar. Sorguların çoğu için hello sorgu iyileştiricisi zaten bir yüksek kaliteli sorgu planı için gerekli istatistikleri hello oluşturur. Bazen, CREATE STATISTICS ile ek istatistikler oluşturarak veya hello sorgu tasarımı değiştirerek tooimprove sorgu performansı gerekebilir. Daha fazla bilgi için bkz: Merhaba [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) sayfası.

Kod örneği:

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
>İstatistik bilgileri otomatik olarak güncelleştirilmez. Bir tablodaki hello verileri hello istatistikleri tekrar oluşturmak zorunda kalmadan güncelleştirirseniz, hello sorgu performansı reddetme.

### <a name="option-2-use-skewfactor"></a>Seçenek 2: SKEWFACTOR kullanın

Her durum için toosum hello vergi istiyorsanız, GROUP BY durumu, hello veri eğme kaçınmak olmayan bir yaklaşım kullanmanız gerekir. Ancak, böylece hello iyileştirici sizin için yürütme planı hazırlama veri anahtarlarında eğme, sorgu tooidentify veri ipucu sağlayabilir.

Genellikle, hello parametre 0,5 ve konuya eğme ve 1 anlamı ağır eğme anlamı 0,5 ile 1 olarak ayarlayabilirsiniz. Merhaba ipucu hello geçerli deyimi ve tüm aşağı akış deyimleri için yürütme planı iyileştirme etkilediğinden, olası hello key-wise toplama eğri önce emin tooadd hello ipucu olması.

    SKEWFACTOR (columns) = x

    Provides a hint that hello given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

Kod örneği:

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

### <a name="option-3-use-rowcount"></a>Seçenek 3: ROWCOUNT kullanın  
Ayrıca belirli eğri anahtarı için tooSKEWFACTOR katılma durumlarda, bu hello biliyorsanız diğer birleştirilmiş satır kümesini küçük, birleştirme önce hello U-SQL deyiminde ROWCOUNT ipucu ekleyerek hello iyileştirici anlayabilirsiniz. Bu şekilde, bir yayın katılım stratejisi toohelp performansı artırır iyileştirici seçebilirsiniz. ROWCOUNT hello veri eğme sorunu çözmezse, ancak bazı ek Yardım sunabileceğiniz unutmayın.

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

Kod örneği:

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

## <a name="solution-3-improve-hello-user-defined-reducer-and-combiner"></a>Çözüm 3: hello kullanıcı tanımlı reducer ve birleştirici geliştirmek

Karmaşık bir işlem mantığı ile bir kullanıcı tarafından tanımlanan işleci toodeal bazen yazabilir ve iyi yazılmış reducer ve birleştirici bir veri eğme sorun bazı durumlarda azaltmak.

### <a name="option-1-use-a-recursive-reducer-if-possible"></a>Seçenek 1: bir özyinelemeli reducer mümkünse kullanın

Varsayılan olarak, kullanıcı tanımlı bir reducer anahtarı için iş azaltan anlamına tek köşe dağıtılmış özyinelemeli olmayan modda çalışır. Ancak, verilerinizi eğri, hello büyük veri kümeleri içinde tek bir köşe işlenen ve uzun bir süredir çalıştırabilir.

tooimprove performans, kod toodefine reducer toorun özyinelemeli modunda bir öznitelik ekleyebilirsiniz. Ardından, hello büyük veri kümeleri dağıtılmış toomultiple köşeleri olması ve işinizi hızlandırır paralel çalıştırın.

bir özyinelemeli olmayan reducer toorecursive toochange toomake, algoritma ilişkilendirilebilir olmasını gerekir. Örneğin, hello toplam ilişkilendirilebilir ve hello ORTANCA değil. Toomake hello giriş ve çıkış reducer için hello tutmak emin etmeniz aynı şema.

Özyinelemeli reducer öznitelik:

    [SqlUserDefinedReducer(IsRecursive = true)]

Kod örneği:

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

### <a name="option-2-use-row-level-combiner-mode-if-possible"></a>Seçenek 2: satır düzeyi Birleştirici modu, mümkünse kullanın

Böylece Hello iş aynı anda çalıştırılabilecek benzer toohello ROWCOUNT ipucu belirli eğri anahtarı birleşim durumlarda Birleştirici modu toodistribute büyük eğri anahtar değer kümeleri toomultiple köşeleri çalışır. Birleştirici modu veri eğme sorunları çözümlenemiyor ancak büyük eğri anahtar değer kümeleri için bazı ek Yardım sağlayabilir.

Varsayılan olarak, satır kümesi hello sol ve sağ satır kümesi ayrılmış anlamına gelir tam hello Birleştirici modudur. Satır düzeyi birleştirme sol/sağ/iç olarak hello modu ayarı sağlar. Merhaba sistem hello karşılık gelen satır kümeleri ayırır ve bunları paralel olarak çalışan birden çok köşeleri uygulamasına dağıtır. Ancak, hello Birleştirici modu yapılandırmadan önce ilgili satır kümeleri hello tooensure ayrılmış dikkatli olun.

izleyen hello örnek ayrılmış sol satır kümesini gösterir. Tek bir giriş satır hello soldan her çıktı satır bağlıdır ve büyük olasılıkla hello sağ hello ile alınan tüm satırların aynı bağımlı anahtar değeri. Merhaba Birleştirici modu sol ayarlarsanız, hello sistem hello büyük sol-satır kümesi küçük parçalara ayırır ve toomultiple köşeleri atar.

![Birleştirici modu çizim](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
>Merhaba yanlış Birleştirici modu ayarlarsanız hello birlikte daha az verimlidir ve hello sonuçlar hatalı olabilir.

Birleştirici modu öznitelikleri:

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all hello input rows from left and right with hello same key value.

- SqlUserDefinedCombiner(Mode=CombinerMode.Left): Tek bir giriş satır hello soldan her çıktı satır bağlıdır (ve büyük olasılıkla tüm satırları hello hello sağ ile aynı anahtar değeri).

- qlUserDefinedCombiner(Mode=CombinerMode.Right): hello sağ tek giriş satırdan her çıktı satır bağlıdır (ve büyük olasılıkla tüm satırları hello ile Merhaba soldan aynı anahtar değeri).

- SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Her çıktı satır hello sol ve sağ hello ile Merhaba tek bir giriş satır aynı bağlıdır değeri.

Kod örneği:

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }
