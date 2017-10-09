---
<span data-ttu-id="19f90-101">Başlık: aaa "Azure Analysis Services öğretici Ders 7: anahtar performans göstergelerini oluşturun | Microsoft Docs"Açıklama: öğretici Azure Analysis Services projesi toocreate anahtar performans göstergelerinin nasıl hello açıklar.</span><span class="sxs-lookup"><span data-stu-id="19f90-101">title: aaa"Azure Analysis Services tutorial lesson 7: Create Key Performance Indicators | Microsoft Docs" description: Describes how toocreate Key Performance Indicators in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="19f90-102">Hizmetleri: analysis services documentationcenter: '' Yazar: minewiskan Yöneticisi: erikre Düzenleyicisi: '' etiketler: ''</span><span class="sxs-lookup"><span data-stu-id="19f90-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="19f90-103">MS.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get-makalesi ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="19f90-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-7-create-key-performance-indicators"></a><span data-ttu-id="19f90-104">7. Ders: Ana Performans Göstergeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="19f90-104">Lesson 7: Create Key Performance Indicators</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="19f90-105">Bu derste Ana Performans Göstergeleri (KPI) oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="19f90-105">In this lesson, you create Key Performance Indicators (KPIs).</span></span> <span data-ttu-id="19f90-106">KPI'ları tarafından tanımlanan bir değer kullanılan toogauge performansını olan bir *temel* ölçüsü karşı bir *hedef* ayrıca bir ölçü veya mutlak bir değer tarafından tanımlanan bir değer.</span><span class="sxs-lookup"><span data-stu-id="19f90-106">KPIs are used toogauge performance of a value defined by a *Base* measure, against a *Target* value also defined by a measure, or by an absolute value.</span></span> <span data-ttu-id="19f90-107">İstemci uygulamaları raporlamada KPI'leri iş uzmanları hızlı ve kolay bir yol toounderstand iş başarı veya tooidentify eğilimlerini özetini sağlar.</span><span class="sxs-lookup"><span data-stu-id="19f90-107">In reporting client applications, KPIs can provide business professionals a quick and easy way toounderstand a summary of business success or tooidentify trends.</span></span> <span data-ttu-id="19f90-108">toolearn daha, fazla [KPI'ları](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="19f90-108">toolearn more, see [KPIs](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span></span>
  
<span data-ttu-id="19f90-109">Bu ders zaman toocomplete tahmini: **15 dakika**</span><span class="sxs-lookup"><span data-stu-id="19f90-109">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="19f90-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="19f90-110">Prerequisites</span></span>  
<span data-ttu-id="19f90-111">Bu konu, sırayla tamamlanması gereken bir tablo modelleme öğreticisinin bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="19f90-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="19f90-112">Bu ders Hello görevleri gerçekleştirmeden önce hello önceki Ders tamamlandı: [Ders 6: ölçüleri oluşturma](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="19f90-112">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>   
  
## <a name="create-key-performance-indicators"></a><span data-ttu-id="19f90-113">Ana Performans Göstergeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="19f90-113">Create Key Performance Indicators</span></span>  
  
#### <a name="toocreate-an-internetcurrentquartersalesperformance-kpi"></a><span data-ttu-id="19f90-114">toocreate InternetCurrentQuarterSalesPerformance KPI</span><span class="sxs-lookup"><span data-stu-id="19f90-114">toocreate an InternetCurrentQuarterSalesPerformance KPI</span></span>  
  
1.  <span data-ttu-id="19f90-115">Merhaba modeli Tasarımcısı'nda hello tıklayın **Factınternetsales** tablo.</span><span class="sxs-lookup"><span data-stu-id="19f90-115">In hello model designer, click hello **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="19f90-116">Merhaba ölçü kılavuzunda, boş bir hücreyi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="19f90-116">In hello measure grid, click an empty cell.</span></span>  
  
3.  <span data-ttu-id="19f90-117">Merhaba tablonun yukarısındaki hello formül çubuğundaki formülü aşağıdaki hello yazın:</span><span class="sxs-lookup"><span data-stu-id="19f90-117">In hello formula bar, above hello table, type hello following formula:</span></span> 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    <span data-ttu-id="19f90-118">Bu ölçü hello KPI için hello temel ölçü olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="19f90-118">This measure serves as hello Base measure for hello KPI.</span></span>  
  
4.  <span data-ttu-id="19f90-119">**InternetCurrentQuarterSalesPerformance** > **KPI Oluştur**’a sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="19f90-119">Right-click **InternetCurrentQuarterSalesPerformance** > **Create KPI**.</span></span>   
  
5.  <span data-ttu-id="19f90-120">Merhaba ana performans göstergesi (KPI) iletişim kutusunda, **hedef** seçin **mutlak değeri**ve ardından **1.1**.</span><span class="sxs-lookup"><span data-stu-id="19f90-120">In hello Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.1**.</span></span>  
  
7.  <span data-ttu-id="19f90-121">Merhaba sol (düşük) kaydırıcı alanına yazın **1**ve ardından hello sağa (yüksek) kaydırıcı alanında, yazın **1.07**.</span><span class="sxs-lookup"><span data-stu-id="19f90-121">In hello left (low) slider field, type **1**, and then in hello right (high) slider field, type **1.07**.</span></span>  
  
8.  <span data-ttu-id="19f90-122">İçinde **simgesi stil seçin**, hello baklava (kırmızı), üçgen (sarı) seçin, yuvarlak (yeşil) simge türü.</span><span class="sxs-lookup"><span data-stu-id="19f90-122">In **Select Icon Style**, select hello diamond (red), triangle (yellow), circle (green) icon type.</span></span>
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > <span data-ttu-id="19f90-124">Bildirim hello Genişletilebilir **açıklamaları** hello kullanılabilir simgesi stilleri altına etiketi.</span><span class="sxs-lookup"><span data-stu-id="19f90-124">Notice hello expandable **Descriptions** label below hello available icon styles.</span></span> <span data-ttu-id="19f90-125">Merhaba açıklamalarını kullan çeşitli KPI öğeleri toomake bunları istemci uygulamalarında daha tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="19f90-125">Use descriptions for hello various KPI elements toomake them more identifiable in client applications.</span></span>  
  
9. <span data-ttu-id="19f90-126">Tıklatın **Tamam** toocomplete hello KPI.</span><span class="sxs-lookup"><span data-stu-id="19f90-126">Click **OK** toocomplete hello KPI.</span></span>  
  
    <span data-ttu-id="19f90-127">Merhaba ölçü kılavuzunda hello simgesi sonraki toohello fark **InternetCurrentQuarterSalesPerformance** ölçü.</span><span class="sxs-lookup"><span data-stu-id="19f90-127">In hello measure grid, notice hello icon next toohello **InternetCurrentQuarterSalesPerformance** measure.</span></span> <span data-ttu-id="19f90-128">Bu simge, bu ölçünün bir KPI’ya ait Temel değer olarak görev yaptığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="19f90-128">This icon indicates that this measure serves as a Base value for a KPI.</span></span>  
  
#### <a name="toocreate-an-internetcurrentquartermarginperformance-kpi"></a><span data-ttu-id="19f90-129">toocreate InternetCurrentQuarterMarginPerformance KPI</span><span class="sxs-lookup"><span data-stu-id="19f90-129">toocreate an InternetCurrentQuarterMarginPerformance KPI</span></span>  
  
1.  <span data-ttu-id="19f90-130">Hello için hello ölçü kılavuzunda **Factınternetsales** tablo, boş bir hücreyi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="19f90-130">In hello measure grid for hello **FactInternetSales** table, click an empty cell.</span></span>  
  
2.  <span data-ttu-id="19f90-131">Merhaba tablonun yukarısındaki hello formül çubuğundaki formülü aşağıdaki hello yazın:</span><span class="sxs-lookup"><span data-stu-id="19f90-131">In hello formula bar, above hello table, type hello following formula:</span></span>  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  <span data-ttu-id="19f90-132">**InternetCurrentQuarterMarginPerformance** > **KPI Oluştur**’a sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="19f90-132">Right-click **InternetCurrentQuarterMarginPerformance** > **Create KPI**.</span></span>  
  
4.  <span data-ttu-id="19f90-133">Merhaba ana performans göstergesi (KPI) iletişim kutusunda, **hedef** seçin **mutlak değeri**ve ardından **1,25**.</span><span class="sxs-lookup"><span data-stu-id="19f90-133">In hello Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.25**.</span></span>   
  
5.  <span data-ttu-id="19f90-134">Merhaba alan görüntüler kadar hello sol (düşük) kaydırıcı alanında, slayt **0,8**, ve ardından slayt hello sağ (yüksek) kaydırıcı alan hello alan görüntüler kadar **1,03 koyun**.</span><span class="sxs-lookup"><span data-stu-id="19f90-134">In hello left (low) slider field, slide until hello field displays **0.8**, and then slide hello right (high) slider field, until hello field displays **1.03**.</span></span>  
  
6.  <span data-ttu-id="19f90-135">İçinde **simgesi stil seçin**hello elmas (kırmızı), üçgen (sarı), daire (yeşil) simge türü seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="19f90-135">In **Select Icon Style**, select hello diamond (red), triangle (yellow), circle (green) icon type, and then click **OK**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="19f90-136">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="19f90-136">What's next?</span></span>
<span data-ttu-id="19f90-137">[8. Ders: Perspektif oluşturma](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="19f90-137">[Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>
  
  
