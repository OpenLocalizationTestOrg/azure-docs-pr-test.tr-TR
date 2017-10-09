---
<span data-ttu-id="b8c93-101">Başlık: aaa "Azure Analysis Services öğretici ek Ders: düzensiz hiyerarşileri | Microsoft Docs"Açıklama: toofix hiyerarşileri hello Azure Analysis Services öğreticide nasıl düzensiz açıklar.</span><span class="sxs-lookup"><span data-stu-id="b8c93-101">title: aaa"Azure Analysis Services tutorial supplemental lesson: Ragged hierarchies | Microsoft Docs" description: Describes how toofix ragged hierarchies in hello Azure Analysis Services tutorial.</span></span>
<span data-ttu-id="b8c93-102">Hizmetleri: analysis services documentationcenter: '' Yazar: minewiskan Yöneticisi: erikre Düzenleyicisi: '' etiketler: ''</span><span class="sxs-lookup"><span data-stu-id="b8c93-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="b8c93-103">MS.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get-makalesi ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="b8c93-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="supplemental-lesson---ragged-hierarchies"></a><span data-ttu-id="b8c93-104">Ek ders - Düzensiz hiyerarşiler</span><span class="sxs-lookup"><span data-stu-id="b8c93-104">Supplemental lesson - Ragged hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="b8c93-105">Bu ek derste, farklı düzeylerde boş değerler (üyeler) içeren hiyerarşileri özetlerken karşılaşılan ortak bir sorunu çözümlersiniz.</span><span class="sxs-lookup"><span data-stu-id="b8c93-105">In this supplemental lesson, you resolve a common problem when pivoting on hierarchies that contain blank values (members) at different levels.</span></span> <span data-ttu-id="b8c93-106">Örneğin, bir üst düzey yöneticiye bağlı departman yöneticilerinin ve yönetici olmayan çalışanların olduğu bir kuruluşta.</span><span class="sxs-lookup"><span data-stu-id="b8c93-106">For example, an organization where a high-level manager has both departmental managers and non-managers as direct reports.</span></span> <span data-ttu-id="b8c93-107">Veya, Ülke-Bölge-Şehirden oluşan ve Washington D.C., Vatikan gibi bazı şehirlerde üst Eyalet veya Bölgenin olmadığı coğrafi hiyerarşilerde.</span><span class="sxs-lookup"><span data-stu-id="b8c93-107">Or, geographic hierarchies composed of Country-Region-City, where some cities lack a parent State or Province, such as Washington D.C., Vatican City.</span></span> <span data-ttu-id="b8c93-108">Bir hiyerarşi boş üyeleri olduğunda, genellikle toodifferent terri veya düzensiz düzeyleri.</span><span class="sxs-lookup"><span data-stu-id="b8c93-108">When a hierarchy has blank members, it often descends toodifferent, or ragged, levels.</span></span>

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

<span data-ttu-id="b8c93-110">Tablolu modeller hello 1400 uyumluluk düzeyine sahip bir ek **Gizle üyeleri** Hiyerarşiler için özellik.</span><span class="sxs-lookup"><span data-stu-id="b8c93-110">Tabular models at hello 1400 compatibility level have an additional **Hide Members** property for hierarchies.</span></span> <span data-ttu-id="b8c93-111">Merhaba **varsayılan** ayarı varsayar herhangi bir düzeyde boş üye yok.</span><span class="sxs-lookup"><span data-stu-id="b8c93-111">hello **Default** setting assumes there are no blank members at any level.</span></span> <span data-ttu-id="b8c93-112">Merhaba **Gizle boş üyeleri** ayarı eklendiğinde hello hiyerarşiden boş üyeleri dışlar tooa PivotTable veya rapor.</span><span class="sxs-lookup"><span data-stu-id="b8c93-112">hello **Hide blank members** setting excludes blank members from hello hierarchy when added tooa PivotTable or report.</span></span>  
  
<span data-ttu-id="b8c93-113">Bu ders zaman toocomplete tahmini: **20 dakika**</span><span class="sxs-lookup"><span data-stu-id="b8c93-113">Estimated time toocomplete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="b8c93-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b8c93-114">Prerequisites</span></span>  
<span data-ttu-id="b8c93-115">Bu ek ders konusu bir tablo modelleme öğreticisinin parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="b8c93-115">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="b8c93-116">Bu ek Ders Hello görevleri gerçekleştirmeden önce tüm önceki dersleri tamamladınız veya bir tamamlanmış Adventure Works Internet satış örnek modeli projesi.</span><span class="sxs-lookup"><span data-stu-id="b8c93-116">Before performing hello tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span> 

<span data-ttu-id="b8c93-117">Merhaba öğreticinin bir parçası olarak hello AW Internet satış proje oluşturduysanız, herhangi bir veri ya da düzensiz hiyerarşileri modelinizi henüz içermiyor.</span><span class="sxs-lookup"><span data-stu-id="b8c93-117">If you've created hello AW Internet Sales project as part of hello tutorial, your model does not yet contain any data or hierarchies that are ragged.</span></span> <span data-ttu-id="b8c93-118">toocomplete bu ek Ders önce Merhaba sorunu bazı ek tablolar ekleyerek, ilişkileri, hesaplanan sütunlarda, bir ölçü ve yeni bir kuruluş hiyerarşisi oluşturmak toocreate olması.</span><span class="sxs-lookup"><span data-stu-id="b8c93-118">toocomplete this supplemental lesson, you first have toocreate hello problem by adding some additional tables, create relationships, calculated columns, a measure, and a new Organization hierarchy.</span></span> <span data-ttu-id="b8c93-119">Bu kısım yaklaşık 15 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="b8c93-119">That part takes about 15 minutes.</span></span> <span data-ttu-id="b8c93-120">Daha sonra toosolve almak yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="b8c93-120">Then, you get toosolve it in just a few minutes.</span></span>  

## <a name="add-tables-and-objects"></a><span data-ttu-id="b8c93-121">Tablo ve nesne ekleme</span><span class="sxs-lookup"><span data-stu-id="b8c93-121">Add tables and objects</span></span>
  
### <a name="tooadd-new-tables-tooyour-model"></a><span data-ttu-id="b8c93-122">tooadd yeni tablolar tooyour modeli</span><span class="sxs-lookup"><span data-stu-id="b8c93-122">tooadd new tables tooyour model</span></span>
  
1.  <span data-ttu-id="b8c93-123">Tablo Modeli Gezgini’nde **Veri Kaynakları**’nı genişletin, ardından bağlantınıza sağ tıklayın > **Yeni Tabloları İçeri Aktar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b8c93-123">In Tabular Model Explorer, expand **Data Sources**, then right-click your connection > **Import New Tables**.</span></span>
  
2.  <span data-ttu-id="b8c93-124">Gezgin’de **DimEmployee** ve **FactResellerSales**’i seçip **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b8c93-124">In Navigator, select **DimEmployee** and **FactResellerSales**, and then click **OK**.</span></span>

3.  <span data-ttu-id="b8c93-125">Sorgu Düzenleyicisi'nde **İçeri Aktar**’a tıklayın</span><span class="sxs-lookup"><span data-stu-id="b8c93-125">In Query Editor, click **Import**</span></span>

4.  <span data-ttu-id="b8c93-126">Merhaba aşağıdaki oluşturma [ilişkileri](../tutorials/aas-lesson-4-create-relationships.md):</span><span class="sxs-lookup"><span data-stu-id="b8c93-126">Create hello following [relationships](../tutorials/aas-lesson-4-create-relationships.md):</span></span>

    | <span data-ttu-id="b8c93-127">Tablo 1</span><span class="sxs-lookup"><span data-stu-id="b8c93-127">Table 1</span></span>           | <span data-ttu-id="b8c93-128">Sütun</span><span class="sxs-lookup"><span data-stu-id="b8c93-128">Column</span></span>       | <span data-ttu-id="b8c93-129">Filtre Yönü</span><span class="sxs-lookup"><span data-stu-id="b8c93-129">Filter Direction</span></span>   | <span data-ttu-id="b8c93-130">Tablo 2</span><span class="sxs-lookup"><span data-stu-id="b8c93-130">Table 2</span></span>     | <span data-ttu-id="b8c93-131">Sütun</span><span class="sxs-lookup"><span data-stu-id="b8c93-131">Column</span></span>      | <span data-ttu-id="b8c93-132">Etkin</span><span class="sxs-lookup"><span data-stu-id="b8c93-132">Active</span></span> |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | <span data-ttu-id="b8c93-133">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="b8c93-133">FactResellerSales</span></span> | <span data-ttu-id="b8c93-134">OrderDateKey</span><span class="sxs-lookup"><span data-stu-id="b8c93-134">OrderDateKey</span></span> | <span data-ttu-id="b8c93-135">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="b8c93-135">Default</span></span>            | <span data-ttu-id="b8c93-136">DimDate</span><span class="sxs-lookup"><span data-stu-id="b8c93-136">DimDate</span></span>     | <span data-ttu-id="b8c93-137">Tarih</span><span class="sxs-lookup"><span data-stu-id="b8c93-137">Date</span></span>        | <span data-ttu-id="b8c93-138">Evet</span><span class="sxs-lookup"><span data-stu-id="b8c93-138">Yes</span></span>    |
    | <span data-ttu-id="b8c93-139">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="b8c93-139">FactResellerSales</span></span> | <span data-ttu-id="b8c93-140">DueDate</span><span class="sxs-lookup"><span data-stu-id="b8c93-140">DueDate</span></span>      | <span data-ttu-id="b8c93-141">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="b8c93-141">Default</span></span>            | <span data-ttu-id="b8c93-142">DimDate</span><span class="sxs-lookup"><span data-stu-id="b8c93-142">DimDate</span></span>     | <span data-ttu-id="b8c93-143">Tarih</span><span class="sxs-lookup"><span data-stu-id="b8c93-143">Date</span></span>        | <span data-ttu-id="b8c93-144">Hayır</span><span class="sxs-lookup"><span data-stu-id="b8c93-144">No</span></span>     |
    | <span data-ttu-id="b8c93-145">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="b8c93-145">FactResellerSales</span></span> | <span data-ttu-id="b8c93-146">ShipDateKey</span><span class="sxs-lookup"><span data-stu-id="b8c93-146">ShipDateKey</span></span>  | <span data-ttu-id="b8c93-147">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="b8c93-147">Default</span></span>            | <span data-ttu-id="b8c93-148">DimDate</span><span class="sxs-lookup"><span data-stu-id="b8c93-148">DimDate</span></span>     | <span data-ttu-id="b8c93-149">Tarih</span><span class="sxs-lookup"><span data-stu-id="b8c93-149">Date</span></span>        | <span data-ttu-id="b8c93-150">Hayır</span><span class="sxs-lookup"><span data-stu-id="b8c93-150">No</span></span>     |
    | <span data-ttu-id="b8c93-151">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="b8c93-151">FactResellerSales</span></span> | <span data-ttu-id="b8c93-152">ProductKey</span><span class="sxs-lookup"><span data-stu-id="b8c93-152">ProductKey</span></span>   | <span data-ttu-id="b8c93-153">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="b8c93-153">Default</span></span>            | <span data-ttu-id="b8c93-154">DimProduct</span><span class="sxs-lookup"><span data-stu-id="b8c93-154">DimProduct</span></span>  | <span data-ttu-id="b8c93-155">ProductKey</span><span class="sxs-lookup"><span data-stu-id="b8c93-155">ProductKey</span></span>  | <span data-ttu-id="b8c93-156">Evet</span><span class="sxs-lookup"><span data-stu-id="b8c93-156">Yes</span></span>    |
    | <span data-ttu-id="b8c93-157">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="b8c93-157">FactResellerSales</span></span> | <span data-ttu-id="b8c93-158">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="b8c93-158">EmployeeKey</span></span>  | <span data-ttu-id="b8c93-159">tooBoth tabloları</span><span class="sxs-lookup"><span data-stu-id="b8c93-159">tooBoth Tables</span></span> | <span data-ttu-id="b8c93-160">DimEmployee</span><span class="sxs-lookup"><span data-stu-id="b8c93-160">DimEmployee</span></span> | <span data-ttu-id="b8c93-161">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="b8c93-161">EmployeeKey</span></span> | <span data-ttu-id="b8c93-162">Evet</span><span class="sxs-lookup"><span data-stu-id="b8c93-162">Yes</span></span>    |

5. <span data-ttu-id="b8c93-163">Merhaba, **DimEmployee** tablo, hello aşağıdaki oluşturma [hesaplanan sütunlar](../tutorials/aas-lesson-5-create-calculated-columns.md):</span><span class="sxs-lookup"><span data-stu-id="b8c93-163">In hello **DimEmployee** table, create hello following [calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md):</span></span> 

    <span data-ttu-id="b8c93-164">**Path**</span><span class="sxs-lookup"><span data-stu-id="b8c93-164">**Path**</span></span> 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    <span data-ttu-id="b8c93-165">**FullName**</span><span class="sxs-lookup"><span data-stu-id="b8c93-165">**FullName**</span></span> 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    <span data-ttu-id="b8c93-166">**Level1**</span><span class="sxs-lookup"><span data-stu-id="b8c93-166">**Level1**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    <span data-ttu-id="b8c93-167">**Level2**</span><span class="sxs-lookup"><span data-stu-id="b8c93-167">**Level2**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,2)) 
    ```

    <span data-ttu-id="b8c93-168">**Level3**</span><span class="sxs-lookup"><span data-stu-id="b8c93-168">**Level3**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,3)) 
    ```

    <span data-ttu-id="b8c93-169">**Level4**</span><span class="sxs-lookup"><span data-stu-id="b8c93-169">**Level4**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,4)) 
    ```

    <span data-ttu-id="b8c93-170">**Level5**</span><span class="sxs-lookup"><span data-stu-id="b8c93-170">**Level5**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,5)) 
    ```

6.  <span data-ttu-id="b8c93-171">Merhaba, **DimEmployee** tablo, oluşturma bir [hiyerarşi](../tutorials/aas-lesson-9-create-hierarchies.md) adlı **kuruluş**.</span><span class="sxs-lookup"><span data-stu-id="b8c93-171">In hello **DimEmployee** table, create a [hierarchy](../tutorials/aas-lesson-9-create-hierarchies.md) named **Organization**.</span></span> <span data-ttu-id="b8c93-172">Sıralı sütunları aşağıdaki hello ekleyin: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span><span class="sxs-lookup"><span data-stu-id="b8c93-172">Add hello following columns in-order: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span></span>

7.  <span data-ttu-id="b8c93-173">Merhaba, **FactResellerSales** tablo, hello aşağıdaki oluşturma [ölçü](../tutorials/aas-lesson-6-create-measures.md):</span><span class="sxs-lookup"><span data-stu-id="b8c93-173">In hello **FactResellerSales** table, create hello following [measure](../tutorials/aas-lesson-6-create-measures.md):</span></span>

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  <span data-ttu-id="b8c93-174">Kullanım [Excel'de çözümleme özelliği](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen Excel ve otomatik olarak bir PivotTable oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b8c93-174">Use [Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen Excel and automatically create a PivotTable.</span></span>

9.  <span data-ttu-id="b8c93-175">İçinde **PivotTable alanları**, hello eklemek **kuruluş** hello hiyerarşiden **DimEmployee** çok tablo**satırları**ve hello **ResellerTotalSales** hello ölçüyü **FactResellerSales** çok tablo**değerleri**.</span><span class="sxs-lookup"><span data-stu-id="b8c93-175">In **PivotTable Fields**, add hello **Organization** hierarchy from hello **DimEmployee** table too**Rows**, and hello **ResellerTotalSales** measure from hello **FactResellerSales**  table too**Values**.</span></span>

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    <span data-ttu-id="b8c93-177">Merhaba PivotTable görebileceğiniz gibi hello hiyerarşi düzensiz satırları gösterir.</span><span class="sxs-lookup"><span data-stu-id="b8c93-177">As you can see in hello PivotTable, hello hierarchy displays rows that are ragged.</span></span> <span data-ttu-id="b8c93-178">Boş üyelerin gösterildiği çok sayıda satır vardır.</span><span class="sxs-lookup"><span data-stu-id="b8c93-178">There are many rows where blank members are shown.</span></span>

## <a name="toofix-hello-ragged-hierarchy-by-setting-hello-hide-members-property"></a><span data-ttu-id="b8c93-179">Merhaba Gizle üyeleri özelliği ayarlanarak hiyerarşi toofix hello düzensiz</span><span class="sxs-lookup"><span data-stu-id="b8c93-179">toofix hello ragged hierarchy by setting hello Hide members property</span></span>

1.  <span data-ttu-id="b8c93-180">**Tablo Modeli Gezgini**’nde **Tablolar** > **DimEmployee** > **Hiyerarşiler** > **Kuruluş**’u genişletin.</span><span class="sxs-lookup"><span data-stu-id="b8c93-180">In **Tabular Model Explorer**, expand **Tables** > **DimEmployee** > **Hierarchies** > **Organization**.</span></span>

2.  <span data-ttu-id="b8c93-181">**Özellikler** > **Üyeleri Gizle** menüsünden **Boş üyeleri gizle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="b8c93-181">In **Properties** > **Hide Members**, select **Hide blank members**.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  <span data-ttu-id="b8c93-183">Geri Excel'de PivotTable hello yenileyin.</span><span class="sxs-lookup"><span data-stu-id="b8c93-183">Back in Excel, refresh hello PivotTable.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    <span data-ttu-id="b8c93-185">Şimdi çok daha iyi görünüyor!</span><span class="sxs-lookup"><span data-stu-id="b8c93-185">Now that looks a whole lot better!</span></span>

## <a name="see-also"></a><span data-ttu-id="b8c93-186">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="b8c93-186">See Also</span></span>   
[<span data-ttu-id="b8c93-187">9. Ders: Hiyerarşi oluşturma</span><span class="sxs-lookup"><span data-stu-id="b8c93-187">Lesson 9: Create hierarchies</span></span>](../tutorials/aas-lesson-9-create-hierarchies.md)  
[<span data-ttu-id="b8c93-188">Ek Ders - Dinamik güvenlik</span><span class="sxs-lookup"><span data-stu-id="b8c93-188">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="b8c93-189">Ek Ders - Ayrıntı satırları</span><span class="sxs-lookup"><span data-stu-id="b8c93-189">Supplemental Lesson - Detail rows</span></span>](../tutorials/aas-supplemental-lesson-detail-rows.md)  