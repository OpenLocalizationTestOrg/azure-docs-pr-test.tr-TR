---
<span data-ttu-id="6fe89-101">Başlık: aaa "Azure Analysis Services öğretici ek Ders: ayrıntı satırları | Microsoft Docs"Açıklama: nasıl toocreate ayrıntı satır ifadesinde bir hello Azure Analysis Services öğretici açıklar.</span><span class="sxs-lookup"><span data-stu-id="6fe89-101">title: aaa"Azure Analysis Services tutorial supplemental lesson: Detail Rows | Microsoft Docs" description: Describes how toocreate a Detail Rows Expression in hello Azure Analysis Services tutorial.</span></span>
<span data-ttu-id="6fe89-102">Hizmetleri: analysis services documentationcenter: '' Yazar: minewiskan Yöneticisi: erikre Düzenleyicisi: '' etiketler: ''</span><span class="sxs-lookup"><span data-stu-id="6fe89-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="6fe89-103">MS.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get-makalesi ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="6fe89-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="supplemental-lesson---detail-rows"></a><span data-ttu-id="6fe89-104">Ek ders - Ayrıntı Satırları</span><span class="sxs-lookup"><span data-stu-id="6fe89-104">Supplemental lesson - Detail Rows</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="6fe89-105">Bu ek Ders içinde özel bir ayrıntı satırları ifade hello DAX Düzenleyicisi toodefine kullanın.</span><span class="sxs-lookup"><span data-stu-id="6fe89-105">In this supplemental lesson, you use hello DAX Editor toodefine a custom Detail Rows Expression.</span></span> <span data-ttu-id="6fe89-106">Bir ayrıntı satırları ifadesi bir ölçü üzerinde son kullanıcılar bir ölçünün bir araya getirilir hello sonuçlarıyla ilgili daha fazla bilgi sağlayan bir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="6fe89-106">A Detail Rows Expression is a property on a measure, providing end-users more information about hello aggregated results of a measure.</span></span> 
  
<span data-ttu-id="6fe89-107">Bu ders zaman toocomplete tahmini: **10 dakika**</span><span class="sxs-lookup"><span data-stu-id="6fe89-107">Estimated time toocomplete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="6fe89-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6fe89-108">Prerequisites</span></span>  
<span data-ttu-id="6fe89-109">Bu ek ders konusu bir tablo modelleme öğreticisinin parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="6fe89-109">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="6fe89-110">Bu ek Ders Hello görevleri gerçekleştirmeden önce tüm önceki dersleri tamamladınız veya bir tamamlanmış Adventure Works Internet satış örnek modeli projesi.</span><span class="sxs-lookup"><span data-stu-id="6fe89-110">Before performing hello tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span>  
  
## <a name="what-do-we-need-toosolve"></a><span data-ttu-id="6fe89-111">Ne toosolve ihtiyacımız var?</span><span class="sxs-lookup"><span data-stu-id="6fe89-111">What do we need toosolve?</span></span>
<span data-ttu-id="6fe89-112">Ayrıntı satırları ifade eklemeden önce bizim InternetTotalSales ölçü hello ayrıntıları bakalım.</span><span class="sxs-lookup"><span data-stu-id="6fe89-112">Let's look at hello details of our InternetTotalSales measure, before adding a Detail Rows Expression.</span></span>

1.  <span data-ttu-id="6fe89-113">Merhaba SSDT içinde tıklatın **modeli** menü > **Excel'de çözümleme özelliği** tooopen Excel ve boş bir PivotTable oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6fe89-113">In SSDT, click hello **Model** menu > **Analyze in Excel** tooopen Excel and create a blank PivotTable.</span></span>
  
2.  <span data-ttu-id="6fe89-114">İçinde **PivotTable alanları**, hello eklemek **InternetTotalSales** hello Factınternetsales tablosundan çok ölçü**değerleri**, **CalendarYear**hello DimDate'i ' çok tablo**sütunları**, ve **EnglishCountryRegionName** çok**satırları**.</span><span class="sxs-lookup"><span data-stu-id="6fe89-114">In **PivotTable Fields**, add hello **InternetTotalSales** measure from hello FactInternetSales table too**Values**, **CalendarYear** from hello DimDate table too**Columns**, and **EnglishCountryRegionName** too**Rows**.</span></span> <span data-ttu-id="6fe89-115">Bizim PivotTable artık bize toplanmış sonuçları bölgeler ve yıl hello InternetTotalSales ölçünün gelen sağlar.</span><span class="sxs-lookup"><span data-stu-id="6fe89-115">Our PivotTable now gives us aggregated results from hello InternetTotalSales measure by regions and year.</span></span> 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. <span data-ttu-id="6fe89-117">Hello PivotTable'da, bir yılın ve bölge adı için bir toplu değeri çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="6fe89-117">In hello PivotTable, double-click an aggregated value for a year and a region name.</span></span> <span data-ttu-id="6fe89-118">Burada size Avustralya ve hello için hello değer yıl 2014 çift.</span><span class="sxs-lookup"><span data-stu-id="6fe89-118">Here we double-clicked hello value for Australia and hello year 2014.</span></span> <span data-ttu-id="6fe89-119">Verileri (yararlı olmayan verileri) içeren yeni bir sayfa açılır.</span><span class="sxs-lookup"><span data-stu-id="6fe89-119">A new sheet opens containing data, but not useful data.</span></span>

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
<span data-ttu-id="6fe89-121">Burada toosee bizim InternetTotalSales ölçü toplanan toohello sonucunu katkıda veri satırları ve sütunları içeren bir tablo gibi ne biz olacaktır.</span><span class="sxs-lookup"><span data-stu-id="6fe89-121">What we would like toosee here is a table containing columns and rows of data that contribute toohello aggregated result of our InternetTotalSales measure.</span></span> <span data-ttu-id="6fe89-122">Ayrıntı satırları ifade hello ölçü bir özellik olarak ekleyebiliriz, toodo.</span><span class="sxs-lookup"><span data-stu-id="6fe89-122">toodo that, we can add a Detail Rows Expression as a property of hello measure.</span></span>

## <a name="add-a-detail-rows-expression"></a><span data-ttu-id="6fe89-123">Ayrıntı Satırları İfadesi ekleme</span><span class="sxs-lookup"><span data-stu-id="6fe89-123">Add a Detail Rows Expression</span></span>

#### <a name="toocreate-a-detail-rows-expression"></a><span data-ttu-id="6fe89-124">toocreate bir ayrıntı satırları ifadesi</span><span class="sxs-lookup"><span data-stu-id="6fe89-124">toocreate a Detail Rows Expression</span></span> 
  
1. <span data-ttu-id="6fe89-125">SSDT içinde hello Factınternetsales tablonun ölçü kılavuzda hello tıklatın **InternetTotalSales** ölçü.</span><span class="sxs-lookup"><span data-stu-id="6fe89-125">In SSDT, in hello FactInternetSales table's measure grid, click hello **InternetTotalSales** measure.</span></span> 

2. <span data-ttu-id="6fe89-126">İçinde **özellikleri** > **ayrıntı satırları ifade**, hello Düzenleyicisi düğmesi tooopen hello DAX Düzenleyicisi'ni tıklatın.</span><span class="sxs-lookup"><span data-stu-id="6fe89-126">In **Properties** > **Detail Rows Expression**, click hello editor button tooopen hello DAX Editor.</span></span>

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. <span data-ttu-id="6fe89-128">DAX Düzenleyicisi'nde hello ifade aşağıdaki girin:</span><span class="sxs-lookup"><span data-stu-id="6fe89-128">In DAX Editor, enter hello following expression:</span></span>

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    <span data-ttu-id="6fe89-129">Bu ifade adlarının, sütun belirtir ve bir kullanıcı bir PivotTable veya rapor toplanmış bir sonuca tıklattığında hello Factınternetsales tablosunda ve ilgili tablolardaki ölçü sonuçlar döndürülür.</span><span class="sxs-lookup"><span data-stu-id="6fe89-129">This expression specifies names, columns, and measure results from hello FactInternetSales table and related tables are returned when a user double-clicks an aggregated result in a PivotTable or report.</span></span>

4. <span data-ttu-id="6fe89-130">Geri Excel'de adım 3'te oluşturulan hello sayfayı silmek, sonra bir toplu değeri çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="6fe89-130">Back in Excel, delete hello sheet created in Step 3, then double-click an aggregated value.</span></span> <span data-ttu-id="6fe89-131">Bu süre, hello ölçü için tanımlanmış bir ayrıntı satırları ifade özelliği ile çok daha kullanışlı verileri içeren yeni bir sayfa açar.</span><span class="sxs-lookup"><span data-stu-id="6fe89-131">This time, with a Detail Rows Expression property defined for hello measure, a new sheet opens containing a lot more useful data.</span></span>

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. <span data-ttu-id="6fe89-133">Modelinizi yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="6fe89-133">Redeploy your model.</span></span>

  
## <a name="see-also"></a><span data-ttu-id="6fe89-134">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="6fe89-134">See Also</span></span>  
<span data-ttu-id="6fe89-135">[SELECTCOLUMNS İşlevi (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span><span class="sxs-lookup"><span data-stu-id="6fe89-135">[SELECTCOLUMNS Function (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span></span>  
[<span data-ttu-id="6fe89-136">Ek Ders - Dinamik güvenlik</span><span class="sxs-lookup"><span data-stu-id="6fe89-136">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="6fe89-137">Ek Ders - Düzensiz hiyerarşiler</span><span class="sxs-lookup"><span data-stu-id="6fe89-137">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
