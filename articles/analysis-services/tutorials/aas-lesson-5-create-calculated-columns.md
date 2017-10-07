---
<span data-ttu-id="71641-101">Başlık: aaa "Azure Analysis Services öğretici Ders 5: hesaplanan sütunlar oluşturma | Microsoft Docs"Açıklama: toocreate hello Azure Analysis Services öğretici proje sütunlarında nasıl hesaplandığını açıklar.</span><span class="sxs-lookup"><span data-stu-id="71641-101">title: aaa"Azure Analysis Services tutorial lesson 5: Create calculated columns | Microsoft Docs" description: Describes how toocreate calculated columns in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="71641-102">Hizmetleri: analysis services documentationcenter: '' Yazar: minewiskan Yöneticisi: erikre Düzenleyicisi: '' etiketler: ''</span><span class="sxs-lookup"><span data-stu-id="71641-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="71641-103">MS.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get-makalesi ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="71641-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---
# <a name="lesson-5-create-calculated-columns"></a><span data-ttu-id="71641-104">5. Ders: Hesaplanan sütunlar oluşturma</span><span class="sxs-lookup"><span data-stu-id="71641-104">Lesson 5: Create calculated columns</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="71641-105">Bu derste, hesaplanan sütunlar ekleyerek modelinizde veri oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="71641-105">In this lesson, you create data in your model by adding calculated columns.</span></span> <span data-ttu-id="71641-106">Hesaplanan sütun (olarak özel sütunları) oluşturabileceğiniz veri al seçeneğini kullanarak, sorgu Düzenleyicisi'ni kullanarak hello ya da daha sonra hello modeli Tasarımcısı benzer, burada yaparsınız.</span><span class="sxs-lookup"><span data-stu-id="71641-106">You can create calculated columns (as custom columns) when using Get Data, by using hello Query Editor, or later in hello model designer like you do here.</span></span> <span data-ttu-id="71641-107">toolearn daha, fazla [hesaplanan sütunlar](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span><span class="sxs-lookup"><span data-stu-id="71641-107">toolearn more, see [Calculated columns](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span></span>
  
<span data-ttu-id="71641-108">Üç farklı tabloda beş yeni hesaplanan sütun oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71641-108">You create five new calculated columns in three different tables.</span></span> <span data-ttu-id="71641-109">Merhaba adımları toocreate sütunları çeşitli yolları vardır, onları yeniden adlandırın ve bunları bir tabloda çeşitli konumlara yerleştirmek gösteren her görev için biraz farklıdır.</span><span class="sxs-lookup"><span data-stu-id="71641-109">hello steps are slightly different for each task showing there are several ways toocreate columns, rename them, and place them in various locations in a table.</span></span>  

<span data-ttu-id="71641-110">Veri Çözümleme İfadeleri’ni (DAX) de ilk olarak bu derste kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="71641-110">This lesson is also where you first use Data Analysis Expressions (DAX).</span></span> <span data-ttu-id="71641-111">DAX, tablosal modeller için yüksek oranda özelleştirilebilen formül ifadeleri oluşturmaya yönelik özel bir dildir.</span><span class="sxs-lookup"><span data-stu-id="71641-111">DAX is a special language for creating highly customizable formula expressions for tabular models.</span></span> <span data-ttu-id="71641-112">Bu öğreticide DAX toocreate hesaplanan sütunları, ölçüleri ve rol filtreleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="71641-112">In this tutorial, you use DAX toocreate calculated columns, measures, and role filters.</span></span> <span data-ttu-id="71641-113">toolearn daha, fazla [tablolu modeller DAX](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="71641-113">toolearn more, see [DAX in tabular models](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span></span> 
  
<span data-ttu-id="71641-114">Bu ders zaman toocomplete tahmini: **15 dakika**</span><span class="sxs-lookup"><span data-stu-id="71641-114">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="71641-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="71641-115">Prerequisites</span></span>  
<span data-ttu-id="71641-116">Bu konu, sırayla tamamlanması gereken bir tablo modelleme öğreticisinin bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="71641-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="71641-117">Bu ders Hello görevleri gerçekleştirmeden önce hello önceki Ders tamamlandı: [Ders 4: ilişkiler oluşturmak](../tutorials/aas-lesson-4-create-relationships.md).</span><span class="sxs-lookup"><span data-stu-id="71641-117">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span> 
  
## <a name="create-calculated-columns"></a><span data-ttu-id="71641-118">Hesaplanan sütunlar oluşturma</span><span class="sxs-lookup"><span data-stu-id="71641-118">Create calculated columns</span></span>  
  
#### <a name="create-a-monthcalendar-calculated-column-in-hello-dimdate-table"></a><span data-ttu-id="71641-119">Merhaba DimDate'i tabloda MonthCalendar hesaplanmış bir sütun oluşturun</span><span class="sxs-lookup"><span data-stu-id="71641-119">Create a MonthCalendar calculated column in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="71641-120">Merhaba tıklatın **modeli** menü > **Model görünümü** > **veri görünümü**.</span><span class="sxs-lookup"><span data-stu-id="71641-120">Click hello **Model** menu > **Model View** > **Data View**.</span></span>  
  
    <span data-ttu-id="71641-121">Hesaplanan sütunlar yalnızca veri görünümü'hello modeli Tasarımcısını kullanarak oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="71641-121">Calculated columns can only be created by using hello model designer in Data View.</span></span>  
  
2.  <span data-ttu-id="71641-122">Merhaba modeli Tasarımcısı'nda hello tıklayın **DimDate'i** tablosu (sekmesi).</span><span class="sxs-lookup"><span data-stu-id="71641-122">In hello model designer, click hello **DimDate** table (tab).</span></span>  
  
3.  <span data-ttu-id="71641-123">Sağ hello **CalendarQuarter** sütun başlığını ve ardından **Sütun Ekle**.</span><span class="sxs-lookup"><span data-stu-id="71641-123">Right-click hello **CalendarQuarter** column header, and then click **Insert Column**.</span></span>  
  
    <span data-ttu-id="71641-124">Adlı yeni bir sütun **hesaplanan sütun 1** eklenen toohello sol tarafındaki hello **Takvim Çeyrek** sütun.</span><span class="sxs-lookup"><span data-stu-id="71641-124">A new column named **Calculated Column 1** is inserted toohello left of hello **Calendar Quarter** column.</span></span>  
  
4.  <span data-ttu-id="71641-125">Hello formül çubuğuna Merhaba tablonun yukarısındaki DAX formülü aşağıdaki hello yazın: yazdığınız otomatik tamamlama yardımcı hello sütunları ve tabloları tam olarak nitelenmiş adlar ve listeleri hello kullanılabilen işlevlerin.</span><span class="sxs-lookup"><span data-stu-id="71641-125">In hello formula bar above hello table, type hello following DAX formula: AutoComplete helps you type hello fully qualified names of columns and tables, and lists hello functions that are available.</span></span>  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    <span data-ttu-id="71641-126">Değerleri, ardından tüm hello satırların hello hesaplanmış sütunda doldurulur.</span><span class="sxs-lookup"><span data-stu-id="71641-126">Values are then populated for all hello rows in hello calculated column.</span></span> <span data-ttu-id="71641-127">Merhaba tabloda aşağı kaydırın, satır hello veriler, her satır göre bu sütun için farklı değerlere sahip olabilir bakın.</span><span class="sxs-lookup"><span data-stu-id="71641-127">If you scroll down through hello table, you see rows can have different values for this column, based on hello data in each row.</span></span>    
  
5.  <span data-ttu-id="71641-128">Bu sütunu çok yeniden adlandırma**MonthCalendar**.</span><span class="sxs-lookup"><span data-stu-id="71641-128">Rename this column too**MonthCalendar**.</span></span> 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
<span data-ttu-id="71641-130">Merhaba MonthCalendar hesaplanan sütun ay sıralanabilir bir ad sağlar.</span><span class="sxs-lookup"><span data-stu-id="71641-130">hello MonthCalendar calculated column provides a sortable name for Month.</span></span>  
  
#### <a name="create-a-dayofweek-calculated-column-in-hello-dimdate-table"></a><span data-ttu-id="71641-131">Merhaba DimDate'i tabloda DayOfWeek hesaplanmış bir sütun oluşturun</span><span class="sxs-lookup"><span data-stu-id="71641-131">Create a DayOfWeek calculated column in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="71641-132">Merhaba ile **DimDate'i** hala etkin tablo, hello tıklatın **sütun** menüsüne ve ardından **Sütun Ekle**.</span><span class="sxs-lookup"><span data-stu-id="71641-132">With hello **DimDate** table still active, click hello **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="71641-133">Merhaba formül çubuğuna formülü aşağıdaki hello yazın:</span><span class="sxs-lookup"><span data-stu-id="71641-133">In hello formula bar, type hello following formula:</span></span>  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    <span data-ttu-id="71641-134">Merhaba formülü oluşturmaya tamamladığınızda, ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="71641-134">When you've finished building hello formula, press ENTER.</span></span> <span data-ttu-id="71641-135">Merhaba yeni sütun toohello Merhaba tablonun sağında eklenir.</span><span class="sxs-lookup"><span data-stu-id="71641-135">hello new column is added toohello far right of hello table.</span></span>  
  
3.  <span data-ttu-id="71641-136">Merhaba sütunu çok yeniden adlandırma**DayOfWeek**.</span><span class="sxs-lookup"><span data-stu-id="71641-136">Rename hello column too**DayOfWeek**.</span></span>  
  
4.  <span data-ttu-id="71641-137">Merhaba sütun başlığını tıklatın ve ardından hello sütun hello arasında sürükleyin **EnglishDayNameOfWeek** sütun ve hello **DayNumberOfMonth** sütun.</span><span class="sxs-lookup"><span data-stu-id="71641-137">Click hello column heading, and then drag hello column between hello **EnglishDayNameOfWeek** column and hello **DayNumberOfMonth** column.</span></span>  
  
    > [!TIP]  
    > <span data-ttu-id="71641-138">Sütunları, tabloda taşıma daha kolay toonavigate kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="71641-138">Moving columns in your table makes it easier toonavigate.</span></span>  
  
<span data-ttu-id="71641-139">Merhaba DayOfWeek hesaplanan sütun haftanın başlangıç günü sıralanabilir bir ad sağlar.</span><span class="sxs-lookup"><span data-stu-id="71641-139">hello DayOfWeek calculated column provides a sortable name for hello day of week.</span></span>  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-hello-dimproduct-table"></a><span data-ttu-id="71641-140">Merhaba DimProduct tabloda ProductSubcategoryName hesaplanmış bir sütun oluşturun</span><span class="sxs-lookup"><span data-stu-id="71641-140">Create a ProductSubcategoryName calculated column in hello DimProduct table</span></span>  
  
  
1.  <span data-ttu-id="71641-141">Merhaba, **DimProduct** tablo, sağda Merhaba tablonun toohello kaydırın.</span><span class="sxs-lookup"><span data-stu-id="71641-141">In hello **DimProduct** table, scroll toohello far right of hello table.</span></span> <span data-ttu-id="71641-142">Bildirim hello en sağdaki sütun adlandırılan **Sütun Ekle** (italik) hello sütun başlığını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="71641-142">Notice hello right-most column is named **Add Column** (italicized), click hello column heading.</span></span>  
  
2.  <span data-ttu-id="71641-143">Merhaba formül çubuğuna formülü aşağıdaki hello yazın:</span><span class="sxs-lookup"><span data-stu-id="71641-143">In hello formula bar, type hello following formula:</span></span>  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  <span data-ttu-id="71641-144">Merhaba sütunu çok yeniden adlandırma**ProductSubcategoryName**.</span><span class="sxs-lookup"><span data-stu-id="71641-144">Rename hello column too**ProductSubcategoryName**.</span></span>  
  
<span data-ttu-id="71641-145">Merhaba ProductSubcategoryName hesaplanmış kullanılan toocreate hello EnglishProductSubcategoryName sütunundaki verileri hello DimProductSubcategory tabloda içerir hello DimProduct tablosunda bir hiyerarşi bir sütundur.</span><span class="sxs-lookup"><span data-stu-id="71641-145">hello ProductSubcategoryName calculated column is used toocreate a hierarchy in hello DimProduct table, which includes data from hello EnglishProductSubcategoryName column in hello DimProductSubcategory table.</span></span> <span data-ttu-id="71641-146">Hiyerarşiler birden fazla tabloya yayılamaz.</span><span class="sxs-lookup"><span data-stu-id="71641-146">Hierarchies cannot span more than one table.</span></span> <span data-ttu-id="71641-147">Hiyerarşileri 9. Derste oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="71641-147">You create hierarchies later in Lesson 9.</span></span>  
  
#### <a name="create-a-productcategoryname-calculated-column-in-hello-dimproduct-table"></a><span data-ttu-id="71641-148">Merhaba DimProduct tabloda ProductCategoryName hesaplanmış bir sütun oluşturun</span><span class="sxs-lookup"><span data-stu-id="71641-148">Create a ProductCategoryName calculated column in hello DimProduct table</span></span>  
  
1.  <span data-ttu-id="71641-149">Merhaba ile **DimProduct** hala etkin tablo, hello tıklatın **sütun** menüsüne ve ardından **Sütun Ekle**.</span><span class="sxs-lookup"><span data-stu-id="71641-149">With hello **DimProduct** table still active, click hello **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="71641-150">Merhaba formül çubuğuna formülü aşağıdaki hello yazın:</span><span class="sxs-lookup"><span data-stu-id="71641-150">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  <span data-ttu-id="71641-151">Merhaba sütunu çok yeniden adlandırma**ProductCategoryName**.</span><span class="sxs-lookup"><span data-stu-id="71641-151">Rename hello column too**ProductCategoryName**.</span></span>  
  
<span data-ttu-id="71641-152">Merhaba ProductCategoryName hesaplanmış kullanılan toocreate hello EnglishProductCategoryName sütunundaki verileri hello DimProductCategory tabloda içerir hello DimProduct tablosunda bir hiyerarşi bir sütundur.</span><span class="sxs-lookup"><span data-stu-id="71641-152">hello ProductCategoryName calculated column is used toocreate a hierarchy in hello DimProduct table, which includes data from hello EnglishProductCategoryName column in hello DimProductCategory table.</span></span> <span data-ttu-id="71641-153">Hiyerarşiler birden fazla tabloya yayılamaz.</span><span class="sxs-lookup"><span data-stu-id="71641-153">Hierarchies cannot span more than one table.</span></span>  
  
#### <a name="create-a-margin-calculated-column-in-hello-factinternetsales-table"></a><span data-ttu-id="71641-154">Merhaba Factınternetsales tablosunda kenar boşluğu hesaplanan bir sütun oluşturun</span><span class="sxs-lookup"><span data-stu-id="71641-154">Create a Margin calculated column in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="71641-155">Merhaba Hello modeli Tasarımcısı'nda seçin **Factınternetsales** tablo.</span><span class="sxs-lookup"><span data-stu-id="71641-155">In hello model designer, select hello **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="71641-156">Yeni bir hesaplanmış sütun hello arasında oluşturma **SalesAmount** sütun ve hello **TaxAmt** sütun.</span><span class="sxs-lookup"><span data-stu-id="71641-156">Create a new calculated column between hello **SalesAmount** column and hello **TaxAmt** column.</span></span>  
  
3.  <span data-ttu-id="71641-157">Merhaba formül çubuğuna formülü aşağıdaki hello yazın:</span><span class="sxs-lookup"><span data-stu-id="71641-157">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  <span data-ttu-id="71641-158">Merhaba sütunu çok yeniden adlandırma**kenar boşluğu**.</span><span class="sxs-lookup"><span data-stu-id="71641-158">Rename hello column too**Margin**.</span></span>  
 
      ![aas lesson5 newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    <span data-ttu-id="71641-160">Başlangıç kenar boşluğu hesaplanmış sütunu her satış için kullanılan tooanalyze kar kenar boşluklarını ' dir.</span><span class="sxs-lookup"><span data-stu-id="71641-160">hello Margin calculated column is used tooanalyze profit margins for each sale.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="71641-161">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="71641-161">What's next?</span></span>
<span data-ttu-id="71641-162">[6. Ders: Ölçü oluşturma](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="71641-162">[Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>
  
  
  
