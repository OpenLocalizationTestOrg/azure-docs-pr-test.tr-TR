---
<span data-ttu-id="3b7a2-101">Başlık: aaa "Azure Analysis Services öğretici Ders 9: hiyerarşileri oluşturun | Microsoft Docs"Açıklama: Hizmetleri: analysis services documentationcenter: '' Yazar: minewiskan Yöneticisi: erikre Düzenleyicisi: '' etiketler: ''</span><span class="sxs-lookup"><span data-stu-id="3b7a2-101">title: aaa"Azure Analysis Services tutorial lesson 9: Create hierarchies | Microsoft Docs" description: services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="3b7a2-102">MS.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get-makalesi ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="3b7a2-102">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-9-create-hierarchies"></a><span data-ttu-id="3b7a2-103">9. Ders: Hiyerarşi oluşturma</span><span class="sxs-lookup"><span data-stu-id="3b7a2-103">Lesson 9: Create hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="3b7a2-104">Bu derste hiyerarşi oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="3b7a2-104">In this lesson, you create hierarchies.</span></span> <span data-ttu-id="3b7a2-105">Hiyerarşiler düzeyler halinde düzenlenmiş sütun gruplarıdır. Örneğin, bir Coğrafya hiyerarşisinde Ülke, Eyalet, Şehir ve İlçe alt düzeyleri bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="3b7a2-105">Hierarchies are groups of columns arranged in levels; for example, a Geography hierarchy might have sublevels for Country, State, County, and City.</span></span> <span data-ttu-id="3b7a2-106">Hiyerarşileri, kullanıcıların toonavigate istemci için daha kolay hale getirme diğer sütunlar listesinde bir raporlama istemci uygulaması alan ayrı görünür ve bir rapora dahil.</span><span class="sxs-lookup"><span data-stu-id="3b7a2-106">Hierarchies can appear separate from other columns in a reporting client application field list, making them easier for client users toonavigate and include in a report.</span></span> <span data-ttu-id="3b7a2-107">toolearn daha, fazla [hiyerarşileri](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="3b7a2-107">toolearn more, see [Hierarchies](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span></span>
  
<span data-ttu-id="3b7a2-108">toocreate hiyerarşileri hello modeli Tasarımcısı'nda kullanmak *diyagram görünümü*.</span><span class="sxs-lookup"><span data-stu-id="3b7a2-108">toocreate hierarchies, use hello model designer in *Diagram View*.</span></span> <span data-ttu-id="3b7a2-109">Hiyerarşi oluşturma ve yönetme Veri Görünümünde desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="3b7a2-109">Creating and managing hierarchies is not supported in Data View.</span></span>  
  
<span data-ttu-id="3b7a2-110">Bu ders zaman toocomplete tahmini: **20 dakika**</span><span class="sxs-lookup"><span data-stu-id="3b7a2-110">Estimated time toocomplete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="3b7a2-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3b7a2-111">Prerequisites</span></span>  
<span data-ttu-id="3b7a2-112">Bu konu, sırayla tamamlanması gereken bir tablo modelleme öğreticisinin bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="3b7a2-112">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="3b7a2-113">Bu ders Hello görevleri gerçekleştirmeden önce hello önceki Ders tamamlandı: [Ders 8: Perspektif oluşturmak](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="3b7a2-113">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>  
  
## <a name="create-hierarchies"></a><span data-ttu-id="3b7a2-114">Hiyerarşi oluşturma</span><span class="sxs-lookup"><span data-stu-id="3b7a2-114">Create hierarchies</span></span>  
  
#### <a name="toocreate-a-category-hierarchy-in-hello-dimproduct-table"></a><span data-ttu-id="3b7a2-115">toocreate hello DimProduct tablosundaki kategori hiyerarşisi</span><span class="sxs-lookup"><span data-stu-id="3b7a2-115">toocreate a Category hierarchy in hello DimProduct table</span></span>  
  
1.  <span data-ttu-id="3b7a2-116">Merhaba Hello modeli Tasarımcısı'nda (diyagram görünümünü) sağ **DimProduct** Tablo > **oluşturma hiyerarşi**.</span><span class="sxs-lookup"><span data-stu-id="3b7a2-116">In hello model designer (diagram view), right-click hello **DimProduct** table > **Create Hierarchy**.</span></span> <span data-ttu-id="3b7a2-117">Yeni bir hiyerarşiye hello tablo penceresinin hello altında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="3b7a2-117">A new hierarchy appears at hello bottom of hello table window.</span></span> <span data-ttu-id="3b7a2-118">Merhaba hiyerarşi yeniden adlandırma **kategori**.</span><span class="sxs-lookup"><span data-stu-id="3b7a2-118">Rename hello hierarchy **Category**.</span></span>  
  
2.  <span data-ttu-id="3b7a2-119">Merhaba sürükleyip **ProductCategoryName** yeni sütun toohello **kategori** hiyerarşisi.</span><span class="sxs-lookup"><span data-stu-id="3b7a2-119">Click and drag hello **ProductCategoryName** column toohello new **Category** hierarchy.</span></span>  
  
3.  <span data-ttu-id="3b7a2-120">Merhaba, **kategori** hiyerarşi, sağ hello **ProductCategoryName** > **yeniden adlandırma**ve ardından **kategori**.</span><span class="sxs-lookup"><span data-stu-id="3b7a2-120">In hello **Category** hierarchy, right-click hello **ProductCategoryName** > **Rename**, and then type **Category**.</span></span>  
  
    > [!NOTE]  
    > <span data-ttu-id="3b7a2-121">Bir hiyerarşideki bir sütunu yeniden adlandırma hello tablosundaki bu sütunu yeniden adlandırmak değil.</span><span class="sxs-lookup"><span data-stu-id="3b7a2-121">Renaming a column in a hierarchy does not rename that column in hello table.</span></span> <span data-ttu-id="3b7a2-122">Bir sütun bir hiyerarşideki yalnızca Merhaba tablonun hello sütununda bir gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="3b7a2-122">A column in a hierarchy is just a representation of hello column in hello table.</span></span>  
  
4.  <span data-ttu-id="3b7a2-123">Merhaba sürükleyip **ProductSubcategoryName** sütun toohello **kategori** hiyerarşisi.</span><span class="sxs-lookup"><span data-stu-id="3b7a2-123">Click and drag hello **ProductSubcategoryName** column toohello **Category** hierarchy.</span></span> <span data-ttu-id="3b7a2-124">Sütunu **Subcategory** olarak yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="3b7a2-124">Rename it **Subcategory**.</span></span> 
  
5.  <span data-ttu-id="3b7a2-125">Sağ hello **ModelName** sütun > **toohierarchy ekleme**ve ardından **kategori**.</span><span class="sxs-lookup"><span data-stu-id="3b7a2-125">Right-click hello **ModelName** column > **Add toohierarchy**, and then select **Category**.</span></span> <span data-ttu-id="3b7a2-126">**Model** olarak yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="3b7a2-126">Rename it **Model**.</span></span>

6.  <span data-ttu-id="3b7a2-127">Son olarak, ekleme **EnglishProductName** toohello kategori hiyerarşisi.</span><span class="sxs-lookup"><span data-stu-id="3b7a2-127">Finally, add **EnglishProductName** toohello Category hierarchy.</span></span> <span data-ttu-id="3b7a2-128">**Product** olarak yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="3b7a2-128">Rename it **Product**.</span></span>  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="toocreate-hierarchies-in-hello-dimdate-table"></a><span data-ttu-id="3b7a2-130">Merhaba DimDate'i tablosundaki toocreate hiyerarşileri</span><span class="sxs-lookup"><span data-stu-id="3b7a2-130">toocreate hierarchies in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="3b7a2-131">Merhaba, **DimDate'i** tablo, adlı bir hiyerarşi oluşturmak **Takvim**.</span><span class="sxs-lookup"><span data-stu-id="3b7a2-131">In hello **DimDate** table, create a hierarchy named **Calendar**.</span></span>  
  
3.  <span data-ttu-id="3b7a2-132">Sıralı sütunları aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3b7a2-132">Add hello following columns in-order:</span></span>

    *  <span data-ttu-id="3b7a2-133">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="3b7a2-133">CalendarYear</span></span>
    *  <span data-ttu-id="3b7a2-134">CalendarSemester</span><span class="sxs-lookup"><span data-stu-id="3b7a2-134">CalendarSemester</span></span>
    *  <span data-ttu-id="3b7a2-135">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="3b7a2-135">CalendarQuarter</span></span>
    *  <span data-ttu-id="3b7a2-136">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="3b7a2-136">MonthCalendar</span></span>
    *  <span data-ttu-id="3b7a2-137">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="3b7a2-137">DayNumberOfMonth</span></span>
    
4.  <span data-ttu-id="3b7a2-138">Merhaba, **DimDate'i** tablo, oluşturma bir **mali** hiyerarşisi.</span><span class="sxs-lookup"><span data-stu-id="3b7a2-138">In hello **DimDate** table, create a **Fiscal** hierarchy.</span></span> <span data-ttu-id="3b7a2-139">Sıralı sütunları aşağıdaki hello şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="3b7a2-139">Include hello following columns in-order:</span></span>  
  
    *  <span data-ttu-id="3b7a2-140">FiscalYear</span><span class="sxs-lookup"><span data-stu-id="3b7a2-140">FiscalYear</span></span>
    *  <span data-ttu-id="3b7a2-141">FiscalSemester</span><span class="sxs-lookup"><span data-stu-id="3b7a2-141">FiscalSemester</span></span>
    *  <span data-ttu-id="3b7a2-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="3b7a2-142">FiscalQuarter</span></span>
    *  <span data-ttu-id="3b7a2-143">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="3b7a2-143">MonthCalendar</span></span>
    *  <span data-ttu-id="3b7a2-144">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="3b7a2-144">DayNumberOfMonth</span></span>
  
5.  <span data-ttu-id="3b7a2-145">Son olarak, hello içinde **DimDate'i** tablo, oluşturma bir **ProductionCalendar** hiyerarşisi.</span><span class="sxs-lookup"><span data-stu-id="3b7a2-145">Finally, in hello **DimDate** table, create a **ProductionCalendar** hierarchy.</span></span> <span data-ttu-id="3b7a2-146">Sıralı sütunları aşağıdaki hello şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="3b7a2-146">Include hello following columns in-order:</span></span>  
    *  <span data-ttu-id="3b7a2-147">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="3b7a2-147">CalendarYear</span></span>
    *  <span data-ttu-id="3b7a2-148">WeekNumberOfYear</span><span class="sxs-lookup"><span data-stu-id="3b7a2-148">WeekNumberOfYear</span></span>
    *  <span data-ttu-id="3b7a2-149">DayNumberOfWeek</span><span class="sxs-lookup"><span data-stu-id="3b7a2-149">DayNumberOfWeek</span></span>
  
 ## <a name="whats-next"></a><span data-ttu-id="3b7a2-150">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="3b7a2-150">What's next?</span></span>
<span data-ttu-id="3b7a2-151">[10. Ders: Bölüm oluşturma](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="3b7a2-151">[Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span> 
  
  
