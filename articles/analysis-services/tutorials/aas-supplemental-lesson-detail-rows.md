---
title: "Azure Analysis Services öğreticisi ek ders: Ayrıntı Satırları | Microsoft Docs"
description: "Azure Analysis Services öğreticisinde bir Ayrıntı Satırları İfadesinin nasıl oluşturulacağını açıklar."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: fde5cd9a9efc3a13e731a91962ced5c086a72355
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="supplemental-lesson---detail-rows"></a><span data-ttu-id="8b413-103">Ek ders - Ayrıntı Satırları</span><span class="sxs-lookup"><span data-stu-id="8b413-103">Supplemental lesson - Detail Rows</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="8b413-104">Bu ek derste DAX Düzenleyicisi'ni kullanarak özel bir Ayrıntı Satırları İfadesi tanımlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="8b413-104">In this supplemental lesson, you use the DAX Editor to define a custom Detail Rows Expression.</span></span> <span data-ttu-id="8b413-105">Ayrıntı Satırları İfadesi, son kullanıcılar için ölçünün toplu sonuçlarıyla ilgili daha fazla bilgi sağlayan bir ölçü özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="8b413-105">A Detail Rows Expression is a property on a measure, providing end-users more information about the aggregated results of a measure.</span></span> 
  
<span data-ttu-id="8b413-106">Bu dersin tahmini tamamlanma süresi: **10 dakika**</span><span class="sxs-lookup"><span data-stu-id="8b413-106">Estimated time to complete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="8b413-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8b413-107">Prerequisites</span></span>  
<span data-ttu-id="8b413-108">Bu ek ders konusu bir tablo modelleme öğreticisinin parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="8b413-108">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="8b413-109">Bu ek dersteki görevleri gerçekleştirmeden önce tüm önceki dersleri tamamlamış veya bir Adventure Works İnternet Satışları örnek model projesini tamamlamış olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8b413-109">Before performing the tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span>  
  
## <a name="what-do-we-need-to-solve"></a><span data-ttu-id="8b413-110">Neyi çözmemiz gerekiyor?</span><span class="sxs-lookup"><span data-stu-id="8b413-110">What do we need to solve?</span></span>
<span data-ttu-id="8b413-111">Bir Ayrıntı Satırları İfadesi eklemeden önce InternetTotalSales ölçümüzün ayrıntılarına bakalım.</span><span class="sxs-lookup"><span data-stu-id="8b413-111">Let's look at the details of our InternetTotalSales measure, before adding a Detail Rows Expression.</span></span>

1.  <span data-ttu-id="8b413-112">SSDT’de **Model** menüsü > **Excel'de çözümleme**’ye tıklayarak Excel'i açın ve boş bir PivotTable oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8b413-112">In SSDT, click the **Model** menu > **Analyze in Excel** to open Excel and create a blank PivotTable.</span></span>
  
2.  <span data-ttu-id="8b413-113">**PivotTable Alanları**’nda FactInternetSales tablosundaki **InternetTotalSales** ölçüsünü **Değerler**, DimDate tablosundaki **CalendarYear** ölçüsünü **Sütunlar**, **EnglishCountryRegionName** ölçüsünü **Satırlar**’a ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8b413-113">In **PivotTable Fields**, add the **InternetTotalSales** measure from the FactInternetSales table to **Values**, **CalendarYear** from the DimDate table to **Columns**, and **EnglishCountryRegionName** to **Rows**.</span></span> <span data-ttu-id="8b413-114">PivotTable bu durumda bölge ve yıla göre InternetTotalSales ölçüsünden toplu sonuçları verir.</span><span class="sxs-lookup"><span data-stu-id="8b413-114">Our PivotTable now gives us aggregated results from the InternetTotalSales measure by regions and year.</span></span> 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. <span data-ttu-id="8b413-116">PivotTable'da bir yıl ve bölge adı için toplu değere çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8b413-116">In the PivotTable, double-click an aggregated value for a year and a region name.</span></span> <span data-ttu-id="8b413-117">Burada Avustralya ve 2014 yılının değerine çift tıkladık.</span><span class="sxs-lookup"><span data-stu-id="8b413-117">Here we double-clicked the value for Australia and the year 2014.</span></span> <span data-ttu-id="8b413-118">Verileri (yararlı olmayan verileri) içeren yeni bir sayfa açılır.</span><span class="sxs-lookup"><span data-stu-id="8b413-118">A new sheet opens containing data, but not useful data.</span></span>

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
<span data-ttu-id="8b413-120">Burada görmek istediğimiz, InternetTotalSales ölçümüzün toplu sonucuna katkıda bulunan veri sütunlarını ve satırlarını içeren bir tablodur.</span><span class="sxs-lookup"><span data-stu-id="8b413-120">What we would like to see here is a table containing columns and rows of data that contribute to the aggregated result of our InternetTotalSales measure.</span></span> <span data-ttu-id="8b413-121">Bunu yapmak için, ölçünün bir özelliği olarak Ayrıntı Satırları İfadesini ekleyebiliriz.</span><span class="sxs-lookup"><span data-stu-id="8b413-121">To do that, we can add a Detail Rows Expression as a property of the measure.</span></span>

## <a name="add-a-detail-rows-expression"></a><span data-ttu-id="8b413-122">Ayrıntı Satırları İfadesi ekleme</span><span class="sxs-lookup"><span data-stu-id="8b413-122">Add a Detail Rows Expression</span></span>

#### <a name="to-create-a-detail-rows-expression"></a><span data-ttu-id="8b413-123">Ayrıntı Satırları İfadesi oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="8b413-123">To create a Detail Rows Expression</span></span> 
  
1. <span data-ttu-id="8b413-124">SSDT’deki FactInternetSales tablosunun ölçü kılavuzunda **InternetTotalSales** ölçüsüne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8b413-124">In SSDT, in the FactInternetSales table's measure grid, click the **InternetTotalSales** measure.</span></span> 

2. <span data-ttu-id="8b413-125">**Özellikler** > **Ayrıntı Satırları İfadesi** menüsünde düzenleyici düğmesine tıklayarak DAX Düzenleyicisi’ni açın.</span><span class="sxs-lookup"><span data-stu-id="8b413-125">In **Properties** > **Detail Rows Expression**, click the editor button to open the DAX Editor.</span></span>

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. <span data-ttu-id="8b413-127">DAX Düzenleyicisi'nde aşağıdaki ifadeyi girin:</span><span class="sxs-lookup"><span data-stu-id="8b413-127">In DAX Editor, enter the following expression:</span></span>

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

    <span data-ttu-id="8b413-128">Bu ifade FactInternetSales tablosundaki ad, sütun ve ölçü sonuçlarını belirtir ve bir kullanıcı PivotTable veya raporda toplu bir sonuca çift tıkladığında ilgili tablolar döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8b413-128">This expression specifies names, columns, and measure results from the FactInternetSales table and related tables are returned when a user double-clicks an aggregated result in a PivotTable or report.</span></span>

4. <span data-ttu-id="8b413-129">Excel'e geri dönerek 3. Adımda oluşturulan sayfayı silin ve sonra bir toplu değere çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8b413-129">Back in Excel, delete the sheet created in Step 3, then double-click an aggregated value.</span></span> <span data-ttu-id="8b413-130">Bu kez, ölçü için tanımlanan Ayrıntı Satırları İfadesi özelliğiyle birlikte birçok yararlı veri içeren yeni bir sayfa açılır.</span><span class="sxs-lookup"><span data-stu-id="8b413-130">This time, with a Detail Rows Expression property defined for the measure, a new sheet opens containing a lot more useful data.</span></span>

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. <span data-ttu-id="8b413-132">Modelinizi yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="8b413-132">Redeploy your model.</span></span>

  
## <a name="see-also"></a><span data-ttu-id="8b413-133">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b413-133">See Also</span></span>  
<span data-ttu-id="8b413-134">[SELECTCOLUMNS İşlevi (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span><span class="sxs-lookup"><span data-stu-id="8b413-134">[SELECTCOLUMNS Function (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span></span>  
[<span data-ttu-id="8b413-135">Ek Ders - Dinamik güvenlik</span><span class="sxs-lookup"><span data-stu-id="8b413-135">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="8b413-136">Ek Ders - Düzensiz hiyerarşiler</span><span class="sxs-lookup"><span data-stu-id="8b413-136">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
