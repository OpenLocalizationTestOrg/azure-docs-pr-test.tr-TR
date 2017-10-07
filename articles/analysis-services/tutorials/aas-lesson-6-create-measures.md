---
<span data-ttu-id="b2f40-101">Başlık: aaa "Azure Analysis Services öğretici Ders 6: ölçüleri oluşturun | Microsoft Docs"Açıklama: toocreate hello Azure Analysis Services öğretici projesinde nasıl ölçer açıklar.</span><span class="sxs-lookup"><span data-stu-id="b2f40-101">title: aaa"Azure Analysis Services tutorial lesson 6: Create measures | Microsoft Docs" description: Describes how toocreate measures in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="b2f40-102">Hizmetleri: analysis services documentationcenter: '' Yazar: minewiskan Yöneticisi: erikre Düzenleyicisi: '' etiketler: ''</span><span class="sxs-lookup"><span data-stu-id="b2f40-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="b2f40-103">MS.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get-makalesi ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="b2f40-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---
# <a name="lesson-6-create-measures"></a><span data-ttu-id="b2f40-104">6. Ders: Ölçü oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2f40-104">Lesson 6: Create measures</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="b2f40-105">Bu alıştırmanın ilerisinde modelinizde dahil ölçüleri toobe oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b2f40-105">In this lesson, you create measures toobe included in your model.</span></span> <span data-ttu-id="b2f40-106">Oluşturduğunuz sütunlara benzer toohello hesaplanan, bir ölçü bir DAX formülü kullanılarak oluşturulan bir hesaplama.</span><span class="sxs-lookup"><span data-stu-id="b2f40-106">Similar toohello calculated columns you created, a measure is a calculation created by using a DAX formula.</span></span> <span data-ttu-id="b2f40-107">Bununla birlikte, hesaplanan sütunlardan farklı olarak ölçüler kullanıcı tarafından seçilen bir *filtre* temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="b2f40-107">However, unlike calculated columns, measures are evaluated based on a user selected *filter*.</span></span> <span data-ttu-id="b2f40-108">Örneğin, belirli sütun veya dilimleyici toohello satır etiketleri alan bir PivotTable eklendi.</span><span class="sxs-lookup"><span data-stu-id="b2f40-108">For example, a particular column or slicer added toohello Row Labels field in a PivotTable.</span></span> <span data-ttu-id="b2f40-109">Her hücre hello filtresi için bir değer hello uygulanan ölçünün sonra hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="b2f40-109">A value for each cell in hello filter is then calculated by hello applied measure.</span></span> <span data-ttu-id="b2f40-110">Neredeyse tüm tablolu modeller tooperform dinamik hesaplamaları sayısal veri tooinclude istediğiniz güçlü ve esnek hesaplamalar yöntemleridir.</span><span class="sxs-lookup"><span data-stu-id="b2f40-110">Measures are powerful, flexible calculations that you want tooinclude in almost all tabular models tooperform dynamic calculations on numerical data.</span></span> <span data-ttu-id="b2f40-111">toolearn daha, fazla [ölçüleri](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="b2f40-111">toolearn more, see [Measures](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span></span>
  
<span data-ttu-id="b2f40-112">toocreate ölçüleri kullandığınız hello *ölçü kılavuz*.</span><span class="sxs-lookup"><span data-stu-id="b2f40-112">toocreate measures, you use hello *Measure Grid*.</span></span> <span data-ttu-id="b2f40-113">Varsayılan olarak, her tablonun boş bir ölçüm kılavuzu vardır; bununla birlikte, genellikle her tablo için ölçü oluşturmazsınız.</span><span class="sxs-lookup"><span data-stu-id="b2f40-113">By default, each table has an empty measure grid; however, you typically do not create measures for every table.</span></span> <span data-ttu-id="b2f40-114">Merhaba ölçü kılavuz veri görünümündeki hello modeli Tasarımcısı'nda bir tablo aşağıda yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="b2f40-114">hello measure grid appears below a table in hello model designer when in Data View.</span></span> <span data-ttu-id="b2f40-115">toohide veya Göster hello ölçü bir tablo için kılavuz hello **tablo** menüsüne ve ardından **ölçü Izgarayı Göster**.</span><span class="sxs-lookup"><span data-stu-id="b2f40-115">toohide or show hello measure grid for a table, click hello **Table** menu, and then click **Show Measure Grid**.</span></span>  
  
<span data-ttu-id="b2f40-116">Boş bir hücre hello ölçü kılavuzunda tıklattıktan sonra hello formül çubuğuna bir DAX formülü yazarak bir ölçü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b2f40-116">You can create a measure by clicking an empty cell in hello measure grid, and then typing a DAX formula in hello formula bar.</span></span> <span data-ttu-id="b2f40-117">Ne zaman ENTER toocomplete hello formülü hello ölçü tıklatın ardından hello hücrede görünür.</span><span class="sxs-lookup"><span data-stu-id="b2f40-117">When you click ENTER toocomplete hello formula, hello measure then appears in hello cell.</span></span> <span data-ttu-id="b2f40-118">Ayrıca bir sütuna tıklayarak standart toplama işlevi kullanılarak ölçüleri oluşturabilir ve hello Otomatik Toplam düğmesini tıklatarak (**∑**) hello araç.</span><span class="sxs-lookup"><span data-stu-id="b2f40-118">You can also create measures using a standard aggregation function by clicking a column, and then clicking hello AutoSum button (**∑**) on hello toolbar.</span></span> <span data-ttu-id="b2f40-119">Merhaba otomatik toplam özelliğini kullanarak oluşturulan ölçüleri hello ölçü kılavuz hücresinin doğrudan hello sütunu altında görünür, ancak taşınabilir.</span><span class="sxs-lookup"><span data-stu-id="b2f40-119">Measures created using hello AutoSum feature appear in hello measure grid cell directly beneath hello column, but can be moved.</span></span>  
  
<span data-ttu-id="b2f40-120">Bu alıştırmanın ilerisinde ölçüler, her iki girerek bir DAX formülü hello formül çubuğuna ve hello otomatik toplam özelliğini kullanarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b2f40-120">In this lesson, you create measures by both entering a DAX formula in hello formula bar, and by using hello AutoSum feature.</span></span>  
  
<span data-ttu-id="b2f40-121">Bu ders zaman toocomplete tahmini: **30 dakika**</span><span class="sxs-lookup"><span data-stu-id="b2f40-121">Estimated time toocomplete this lesson: **30 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="b2f40-122">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b2f40-122">Prerequisites</span></span>  
<span data-ttu-id="b2f40-123">Bu konu, sırayla tamamlanması gereken bir tablo modelleme öğreticisinin bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="b2f40-123">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="b2f40-124">Bu ders Hello görevleri gerçekleştirmeden önce hello önceki Ders tamamlandı: [Ders 5: hesaplanan sütunlar oluşturma](../tutorials/aas-lesson-5-create-calculated-columns.md).</span><span class="sxs-lookup"><span data-stu-id="b2f40-124">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 5: Create calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md).</span></span>  
  
## <a name="create-measures"></a><span data-ttu-id="b2f40-125">Ölçü oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2f40-125">Create measures</span></span>  
  
#### <a name="toocreate-a-dayscurrentquartertodate-measure-in-hello-dimdate-table"></a><span data-ttu-id="b2f40-126">toocreate hello DimDate'i tablosunda DaysCurrentQuarterToDate ölçü</span><span class="sxs-lookup"><span data-stu-id="b2f40-126">toocreate a DaysCurrentQuarterToDate measure in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="b2f40-127">Merhaba modeli Tasarımcısı'nda hello tıklayın **DimDate'i** tablo.</span><span class="sxs-lookup"><span data-stu-id="b2f40-127">In hello model designer, click hello **DimDate** table.</span></span>  
  
2.  <span data-ttu-id="b2f40-128">Merhaba ölçü kılavuzunda hello sol üst boş hücreyi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b2f40-128">In hello measure grid, click hello top-left empty cell.</span></span>  
  
3.  <span data-ttu-id="b2f40-129">Merhaba formül çubuğuna formülü aşağıdaki hello yazın:</span><span class="sxs-lookup"><span data-stu-id="b2f40-129">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    <span data-ttu-id="b2f40-130">Bildirim hello sol üst hücre şimdi bir ölçü adı içeriyor **DaysCurrentQuarterToDate**hello sonucu, ardından **92**.</span><span class="sxs-lookup"><span data-stu-id="b2f40-130">Notice hello top-left cell now contains a measure name, **DaysCurrentQuarterToDate**, followed by hello result, **92**.</span></span>
    
      ![aas-lesson6-newmeasure](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    <span data-ttu-id="b2f40-132">Hesaplanan sütunlar, ölçü formüllerle hello formül ifadeyle üste ve ardından hello ölçü adı yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2f40-132">Unlike calculated columns, with measure formulas you can type hello measure name, followed by a colon, followed by hello formula expression.</span></span>

  
#### <a name="toocreate-a-daysincurrentquarter-measure-in-hello-dimdate-table"></a><span data-ttu-id="b2f40-133">toocreate hello DimDate'i tablosunda DaysInCurrentQuarter ölçü</span><span class="sxs-lookup"><span data-stu-id="b2f40-133">toocreate a DaysInCurrentQuarter measure in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="b2f40-134">Merhaba ile **DimDate'i** hello ölçü kılavuzunda hello modeli Tasarımcısı'nda hala etkin tablo, boş bir hücre hello oluşturduğunuz hello ölçü aşağıda'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b2f40-134">With hello **DimDate** table still active in hello model designer, in hello measure grid, click hello empty cell below hello measure you created.</span></span>  
  
2.  <span data-ttu-id="b2f40-135">Merhaba formül çubuğuna formülü aşağıdaki hello yazın:</span><span class="sxs-lookup"><span data-stu-id="b2f40-135">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    <span data-ttu-id="b2f40-136">Bir tamamlanmamış dönemi ve hello arasında bir karşılaştırma oranı önceki dönem oluştururken.</span><span class="sxs-lookup"><span data-stu-id="b2f40-136">When creating a comparison ratio between one incomplete period and hello previous period.</span></span> <span data-ttu-id="b2f40-137">Merhaba formülü, geçti hello dönemi hello oranını hesaplamak ve aynı hello önceki dönemi oranı toohello karşılaştırır.</span><span class="sxs-lookup"><span data-stu-id="b2f40-137">hello formula must calculate hello proportion of hello period that has elapsed and compare it toohello same proportion in hello previous period.</span></span> <span data-ttu-id="b2f40-138">Bu durumda, [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] verir hello oranı hello geçerli süre geçti.</span><span class="sxs-lookup"><span data-stu-id="b2f40-138">In this case, [DaysCurrentQuarterToDate]/[DaysInCurrentQuarter] gives hello proportion elapsed in hello current period.</span></span>  
  
#### <a name="toocreate-an-internetdistinctcountsalesorder-measure-in-hello-factinternetsales-table"></a><span data-ttu-id="b2f40-139">toocreate hello Factınternetsales tablosunda InternetDistinctCountSalesOrder ölçü</span><span class="sxs-lookup"><span data-stu-id="b2f40-139">toocreate an InternetDistinctCountSalesOrder measure in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="b2f40-140">Merhaba tıklatın **Factınternetsales** tablo.</span><span class="sxs-lookup"><span data-stu-id="b2f40-140">Click hello **FactInternetSales** table.</span></span>   
  
2.  <span data-ttu-id="b2f40-141">Merhaba tıklatın **SalesOrderNumber** sütun başlığı.</span><span class="sxs-lookup"><span data-stu-id="b2f40-141">Click hello **SalesOrderNumber** column heading.</span></span>  
  
3.  <span data-ttu-id="b2f40-142">Merhaba araç çubuğunda hello aşağı ok sonraki toohello otomatik toplam'ı tıklatın (**∑**) düğmesine tıklayın ve ardından **DistinctCount**.</span><span class="sxs-lookup"><span data-stu-id="b2f40-142">On hello toolbar, click hello down-arrow next toohello AutoSum (**∑**) button, and then select **DistinctCount**.</span></span>  
  
    <span data-ttu-id="b2f40-143">Merhaba otomatik toplam özelliğini otomatik olarak hello DistinctCount standart toplama formülü kullanarak hello seçili sütun için bir ölçü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b2f40-143">hello AutoSum feature automatically creates a measure for hello selected column using hello DistinctCount standard aggregation formula.</span></span>  
    
       ![aas-lesson6-newmeasure2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  <span data-ttu-id="b2f40-145">Merhaba ölçü kılavuzda hello yeni ölçü tıklatın ve ardından hello **özellikleri** penceresi, **ölçü adı**, hello ölçü çok yeniden adlandırma**InternetDistinctCountSalesOrder**.</span><span class="sxs-lookup"><span data-stu-id="b2f40-145">In hello measure grid, click hello new measure, and then in hello **Properties** window, in **Measure Name**, rename hello measure too**InternetDistinctCountSalesOrder**.</span></span> 
 
  
#### <a name="toocreate-additional-measures-in-hello-factinternetsales-table"></a><span data-ttu-id="b2f40-146">Merhaba Factınternetsales tablosunda toocreate ek ölçümler</span><span class="sxs-lookup"><span data-stu-id="b2f40-146">toocreate additional measures in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="b2f40-147">Merhaba otomatik toplam özelliğini kullanarak oluşturun ve ölçüleri aşağıdaki hello adlandırın:</span><span class="sxs-lookup"><span data-stu-id="b2f40-147">By using hello AutoSum feature, create and name hello following measures:</span></span>  

    |<span data-ttu-id="b2f40-148">Sütun</span><span class="sxs-lookup"><span data-stu-id="b2f40-148">Column</span></span>|<span data-ttu-id="b2f40-149">Ölçü adı</span><span class="sxs-lookup"><span data-stu-id="b2f40-149">Measure name</span></span>|<span data-ttu-id="b2f40-150">Otomatik Toplam (∑)</span><span class="sxs-lookup"><span data-stu-id="b2f40-150">AutoSum (∑)</span></span>|<span data-ttu-id="b2f40-151">Formül</span><span class="sxs-lookup"><span data-stu-id="b2f40-151">Formula</span></span>|  
    |----------------|----------|-----------------|-----------|  
    |<span data-ttu-id="b2f40-152">SalesOrderLineNumber</span><span class="sxs-lookup"><span data-stu-id="b2f40-152">SalesOrderLineNumber</span></span>|<span data-ttu-id="b2f40-153">InternetOrderLinesCount</span><span class="sxs-lookup"><span data-stu-id="b2f40-153">InternetOrderLinesCount</span></span>|<span data-ttu-id="b2f40-154">Sayı</span><span class="sxs-lookup"><span data-stu-id="b2f40-154">Count</span></span>|<span data-ttu-id="b2f40-155">=COUNTA([SalesOrderLineNumber])</span><span class="sxs-lookup"><span data-stu-id="b2f40-155">=COUNTA([SalesOrderLineNumber])</span></span>|  
    |<span data-ttu-id="b2f40-156">OrderQuantity</span><span class="sxs-lookup"><span data-stu-id="b2f40-156">OrderQuantity</span></span>|<span data-ttu-id="b2f40-157">InternetTotalUnits</span><span class="sxs-lookup"><span data-stu-id="b2f40-157">InternetTotalUnits</span></span>|<span data-ttu-id="b2f40-158">Toplam</span><span class="sxs-lookup"><span data-stu-id="b2f40-158">Sum</span></span>|<span data-ttu-id="b2f40-159">=SUM([OrderQuantity])</span><span class="sxs-lookup"><span data-stu-id="b2f40-159">=SUM([OrderQuantity])</span></span>|  
    |<span data-ttu-id="b2f40-160">DiscountAmount</span><span class="sxs-lookup"><span data-stu-id="b2f40-160">DiscountAmount</span></span>|<span data-ttu-id="b2f40-161">InternetTotalDiscountAmount</span><span class="sxs-lookup"><span data-stu-id="b2f40-161">InternetTotalDiscountAmount</span></span>|<span data-ttu-id="b2f40-162">Toplam</span><span class="sxs-lookup"><span data-stu-id="b2f40-162">Sum</span></span>|<span data-ttu-id="b2f40-163">=SUM([DiscountAmount])</span><span class="sxs-lookup"><span data-stu-id="b2f40-163">=SUM([DiscountAmount])</span></span>|  
    |<span data-ttu-id="b2f40-164">TotalProductCost</span><span class="sxs-lookup"><span data-stu-id="b2f40-164">TotalProductCost</span></span>|<span data-ttu-id="b2f40-165">InternetTotalProductCost</span><span class="sxs-lookup"><span data-stu-id="b2f40-165">InternetTotalProductCost</span></span>|<span data-ttu-id="b2f40-166">Toplam</span><span class="sxs-lookup"><span data-stu-id="b2f40-166">Sum</span></span>|<span data-ttu-id="b2f40-167">=SUM([TotalProductCost])</span><span class="sxs-lookup"><span data-stu-id="b2f40-167">=SUM([TotalProductCost])</span></span>|  
    |<span data-ttu-id="b2f40-168">SalesAmount</span><span class="sxs-lookup"><span data-stu-id="b2f40-168">SalesAmount</span></span>|<span data-ttu-id="b2f40-169">InternetTotalSales</span><span class="sxs-lookup"><span data-stu-id="b2f40-169">InternetTotalSales</span></span>|<span data-ttu-id="b2f40-170">Toplam</span><span class="sxs-lookup"><span data-stu-id="b2f40-170">Sum</span></span>|<span data-ttu-id="b2f40-171">=SUM([SalesAmount])</span><span class="sxs-lookup"><span data-stu-id="b2f40-171">=SUM([SalesAmount])</span></span>|  
    |<span data-ttu-id="b2f40-172">Marj</span><span class="sxs-lookup"><span data-stu-id="b2f40-172">Margin</span></span>|<span data-ttu-id="b2f40-173">InternetTotalMargin</span><span class="sxs-lookup"><span data-stu-id="b2f40-173">InternetTotalMargin</span></span>|<span data-ttu-id="b2f40-174">Toplam</span><span class="sxs-lookup"><span data-stu-id="b2f40-174">Sum</span></span>|<span data-ttu-id="b2f40-175">=SUM([Margin])</span><span class="sxs-lookup"><span data-stu-id="b2f40-175">=SUM([Margin])</span></span>|  
    |<span data-ttu-id="b2f40-176">TaxAmt</span><span class="sxs-lookup"><span data-stu-id="b2f40-176">TaxAmt</span></span>|<span data-ttu-id="b2f40-177">InternetTotalTaxAmt</span><span class="sxs-lookup"><span data-stu-id="b2f40-177">InternetTotalTaxAmt</span></span>|<span data-ttu-id="b2f40-178">Toplam</span><span class="sxs-lookup"><span data-stu-id="b2f40-178">Sum</span></span>|<span data-ttu-id="b2f40-179">=SUM([TaxAmt])</span><span class="sxs-lookup"><span data-stu-id="b2f40-179">=SUM([TaxAmt])</span></span>|  
    |<span data-ttu-id="b2f40-180">Nakliye</span><span class="sxs-lookup"><span data-stu-id="b2f40-180">Freight</span></span>|<span data-ttu-id="b2f40-181">InternetTotalFreight</span><span class="sxs-lookup"><span data-stu-id="b2f40-181">InternetTotalFreight</span></span>|<span data-ttu-id="b2f40-182">Toplam</span><span class="sxs-lookup"><span data-stu-id="b2f40-182">Sum</span></span>|<span data-ttu-id="b2f40-183">=SUM([Freight])</span><span class="sxs-lookup"><span data-stu-id="b2f40-183">=SUM([Freight])</span></span>|  
  
2.  <span data-ttu-id="b2f40-184">Boş bir hücreye hello ölçü kılavuzunda ve hello formül çubuğu kullanarak tıklayarak oluşturun ve ad hello aşağıdaki sırayla ölçer:</span><span class="sxs-lookup"><span data-stu-id="b2f40-184">By clicking an empty cell in hello measure grid, and by using hello formula bar, create, and name hello following measures in order:</span></span>  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
<span data-ttu-id="b2f40-185">Merhaba Factınternetsales tablosunda için oluşturulan ölçüleri kullanılan tooanalyze satış, maliyetleri ve hello kullanıcı seçilen filtre tarafından tanımlanan öğeleri için kar marjı gibi kritik finansal verileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="b2f40-185">Measures created for hello FactInternetSales table can be used tooanalyze critical financial data such as sales, costs, and profit margin for items defined by hello user selected filter.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="b2f40-186">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="b2f40-186">What's next?</span></span>
<span data-ttu-id="b2f40-187">[7. Ders: Önemli Performans Göstergeleri oluşturma](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="b2f40-187">[Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  

  
