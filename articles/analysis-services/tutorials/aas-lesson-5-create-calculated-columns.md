---
title: "Azure Analysis Services öğreticisi 5. Ders: Hesaplanan sütunlar oluşturma | Microsoft Docs"
description: "Azure Analysis Services öğretici projesinde hesaplanan sütunların nasıl oluşturulacağını açıklar."
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
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: 893371145d77e156843271907aeef0c3756d0403
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-5-create-calculated-columns"></a><span data-ttu-id="160a6-103">5. Ders: Hesaplanan sütunlar oluşturma</span><span class="sxs-lookup"><span data-stu-id="160a6-103">Lesson 5: Create calculated columns</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="160a6-104">Bu derste, hesaplanan sütunlar ekleyerek modelinizde veri oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="160a6-104">In this lesson, you create data in your model by adding calculated columns.</span></span> <span data-ttu-id="160a6-105">Verileri Al’ı kullanırken Sorgu Düzenleyicisi’ni kullanarak veya daha sonra, burada yaptığınız gibi model tasarımcısına giderek hesaplanan sütunlar (özel sütunlar olarak) oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="160a6-105">You can create calculated columns (as custom columns) when using Get Data, by using the Query Editor, or later in the model designer like you do here.</span></span> <span data-ttu-id="160a6-106">Daha fazla bilgi edinmek için bkz. [Hesaplanan sütunlar](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span><span class="sxs-lookup"><span data-stu-id="160a6-106">To learn more, see [Calculated columns](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span></span>
  
<span data-ttu-id="160a6-107">Üç farklı tabloda beş yeni hesaplanan sütun oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="160a6-107">You create five new calculated columns in three different tables.</span></span> <span data-ttu-id="160a6-108">Sütunları oluşturmak, yeniden adlandırmak ve tabloda farklı yerlere eklemek için farklı yollar olduğunu göstermek amacıyla, her görev için gerçekleştirilmesi gereken adımlar biraz farklıdır.</span><span class="sxs-lookup"><span data-stu-id="160a6-108">The steps are slightly different for each task showing there are several ways to create columns, rename them, and place them in various locations in a table.</span></span>  

<span data-ttu-id="160a6-109">Veri Çözümleme İfadeleri’ni (DAX) de ilk olarak bu derste kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="160a6-109">This lesson is also where you first use Data Analysis Expressions (DAX).</span></span> <span data-ttu-id="160a6-110">DAX, tablosal modeller için yüksek oranda özelleştirilebilen formül ifadeleri oluşturmaya yönelik özel bir dildir.</span><span class="sxs-lookup"><span data-stu-id="160a6-110">DAX is a special language for creating highly customizable formula expressions for tabular models.</span></span> <span data-ttu-id="160a6-111">Bu öğreticide, DAX dilini kullanarak hesaplanan sütunlar, ölçüler ve rol filtreleri oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="160a6-111">In this tutorial, you use DAX to create calculated columns, measures, and role filters.</span></span> <span data-ttu-id="160a6-112">Daha fazla bilgi edinmek için bkz. [Tablosal modellerde DAX](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="160a6-112">To learn more, see [DAX in tabular models](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span></span> 
  
<span data-ttu-id="160a6-113">Bu dersin tahmini tamamlanma süresi: **15 dakika**</span><span class="sxs-lookup"><span data-stu-id="160a6-113">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="160a6-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="160a6-114">Prerequisites</span></span>  
<span data-ttu-id="160a6-115">Bu konu, sırayla tamamlanması gereken bir tablosal modelleme öğreticisinin bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="160a6-115">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="160a6-116">Bu dersteki görevleri gerçekleştirmeden önce, bir önceki dersi tamamlamış olmanız gerekir: [4. Ders: İlişki oluşturma](../tutorials/aas-lesson-4-create-relationships.md).</span><span class="sxs-lookup"><span data-stu-id="160a6-116">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span> 
  
## <a name="create-calculated-columns"></a><span data-ttu-id="160a6-117">Hesaplanan sütunlar oluşturma</span><span class="sxs-lookup"><span data-stu-id="160a6-117">Create calculated columns</span></span>  
  
#### <a name="create-a-monthcalendar-calculated-column-in-the-dimdate-table"></a><span data-ttu-id="160a6-118">DimDate tablosunda bir MonthCalendar hesaplanan sütunu oluşturma</span><span class="sxs-lookup"><span data-stu-id="160a6-118">Create a MonthCalendar calculated column in the DimDate table</span></span>  
  
1.  <span data-ttu-id="160a6-119">**Model** menüsü > **Model Görünümü** > **Veri Görünümü**’ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="160a6-119">Click the **Model** menu > **Model View** > **Data View**.</span></span>  
  
    <span data-ttu-id="160a6-120">Hesaplanan sütunlar yalnızca Veri Görünümü'ndeki model tasarımcısı kullanılarak oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="160a6-120">Calculated columns can only be created by using the model designer in Data View.</span></span>  
  
2.  <span data-ttu-id="160a6-121">Model tasarımcısında **DimDate** tablosuna (sekme) tıklayın.</span><span class="sxs-lookup"><span data-stu-id="160a6-121">In the model designer, click the **DimDate** table (tab).</span></span>  
  
3.  <span data-ttu-id="160a6-122">**CalendarQuarter** sütun başlığına sağ tıklayıp **Sütun Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="160a6-122">Right-click the **CalendarQuarter** column header, and then click **Insert Column**.</span></span>  
  
    <span data-ttu-id="160a6-123">**Takvim Çeyreği** sütununun sol tarafına **Hesaplanan Sütun 1** adlı yeni bir sütun eklenir.</span><span class="sxs-lookup"><span data-stu-id="160a6-123">A new column named **Calculated Column 1** is inserted to the left of the **Calendar Quarter** column.</span></span>  
  
4.  <span data-ttu-id="160a6-124">Tablonun üstündeki formül çubuğuna aşağıdaki DAX formülünü yazın: Otomatik Tamamlama, sütun ve tabloların tam adlarını yazmanıza yardımcı olur ve kullanılabilen işlevleri listeler.</span><span class="sxs-lookup"><span data-stu-id="160a6-124">In the formula bar above the table, type the following DAX formula: AutoComplete helps you type the fully qualified names of columns and tables, and lists the functions that are available.</span></span>  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    <span data-ttu-id="160a6-125">Daha sonra, hesaplanan sütundaki tüm satırlar için değerler doldurulur.</span><span class="sxs-lookup"><span data-stu-id="160a6-125">Values are then populated for all the rows in the calculated column.</span></span> <span data-ttu-id="160a6-126">Tabloyu aşağı kaydırırsanız, her bir satırdaki verilere bağlı olarak satırlarda bu sütun için farklı değerler girilebildiğini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="160a6-126">If you scroll down through the table, you see rows can have different values for this column, based on the data in each row.</span></span>    
  
5.  <span data-ttu-id="160a6-127">Bu sütunu **MonthCalendar** olarak yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="160a6-127">Rename this column to **MonthCalendar**.</span></span> 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
<span data-ttu-id="160a6-129">MonthCalendar hesaplanan sütunu, Ay için sıralanabilen bir ad sağlar.</span><span class="sxs-lookup"><span data-stu-id="160a6-129">The MonthCalendar calculated column provides a sortable name for Month.</span></span>  
  
#### <a name="create-a-dayofweek-calculated-column-in-the-dimdate-table"></a><span data-ttu-id="160a6-130">DimDate tablosunda DayOfWeek hesaplanan sütunu oluşturma</span><span class="sxs-lookup"><span data-stu-id="160a6-130">Create a DayOfWeek calculated column in the DimDate table</span></span>  
  
1.  <span data-ttu-id="160a6-131">**DimDate** tablosu hala etkinken **Sütun** menüsüne ve sonra **Sütun Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="160a6-131">With the **DimDate** table still active, click the **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="160a6-132">Formül çubuğuna aşağıdaki formülü yazın:</span><span class="sxs-lookup"><span data-stu-id="160a6-132">In the formula bar, type the following formula:</span></span>  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    <span data-ttu-id="160a6-133">Formülü oluşturmayı tamamladığınızda, ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="160a6-133">When you've finished building the formula, press ENTER.</span></span> <span data-ttu-id="160a6-134">Yeni sütun tablonun en sağına eklenir.</span><span class="sxs-lookup"><span data-stu-id="160a6-134">The new column is added to the far right of the table.</span></span>  
  
3.  <span data-ttu-id="160a6-135">Sütunu **DayOfWeek** olarak yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="160a6-135">Rename the column to **DayOfWeek**.</span></span>  
  
4.  <span data-ttu-id="160a6-136">Sütun başlığına tıklayın, sütunu **EnglishDayNameOfWeek** sütunu ile **DayNumberOfMonth** sütunu arasına sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="160a6-136">Click the column heading, and then drag the column between the **EnglishDayNameOfWeek** column and the **DayNumberOfMonth** column.</span></span>  
  
    > [!TIP]  
    > <span data-ttu-id="160a6-137">Tablonuzdaki sütunların taşınması, gezintiyi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="160a6-137">Moving columns in your table makes it easier to navigate.</span></span>  
  
<span data-ttu-id="160a6-138">DayOfWeek hesaplanan sütunu, haftanın günü için sıralanabilen bir ad sağlar.</span><span class="sxs-lookup"><span data-stu-id="160a6-138">The DayOfWeek calculated column provides a sortable name for the day of week.</span></span>  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-the-dimproduct-table"></a><span data-ttu-id="160a6-139">DimProduct tablosunda ProductSubcategoryName hesaplanan sütunu oluşturma</span><span class="sxs-lookup"><span data-stu-id="160a6-139">Create a ProductSubcategoryName calculated column in the DimProduct table</span></span>  
  
  
1.  <span data-ttu-id="160a6-140">**DimProduct** tablosunda, tablonun en sağına gidin.</span><span class="sxs-lookup"><span data-stu-id="160a6-140">In the **DimProduct** table, scroll to the far right of the table.</span></span> <span data-ttu-id="160a6-141">En sağdaki sütunun **Sütun Ekle** (italik) olarak adlandırıldığına dikkat edin ve sütun başlığına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="160a6-141">Notice the right-most column is named **Add Column** (italicized), click the column heading.</span></span>  
  
2.  <span data-ttu-id="160a6-142">Formül çubuğuna aşağıdaki formülü yazın:</span><span class="sxs-lookup"><span data-stu-id="160a6-142">In the formula bar, type the following formula:</span></span>  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  <span data-ttu-id="160a6-143">Sütunu **ProductSubcategoryName** olarak yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="160a6-143">Rename the column to **ProductSubcategoryName**.</span></span>  
  
<span data-ttu-id="160a6-144">ProductSubcategoryName hesaplanan sütunu, DimProductSubcategory tablosundaki EnglishProductSubcategoryName sütunundan veriler içeren DimProduct tablosunda bir hiyerarşi oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="160a6-144">The ProductSubcategoryName calculated column is used to create a hierarchy in the DimProduct table, which includes data from the EnglishProductSubcategoryName column in the DimProductSubcategory table.</span></span> <span data-ttu-id="160a6-145">Hiyerarşiler birden fazla tabloya yayılamaz.</span><span class="sxs-lookup"><span data-stu-id="160a6-145">Hierarchies cannot span more than one table.</span></span> <span data-ttu-id="160a6-146">Hiyerarşileri 9. Derste oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="160a6-146">You create hierarchies later in Lesson 9.</span></span>  
  
#### <a name="create-a-productcategoryname-calculated-column-in-the-dimproduct-table"></a><span data-ttu-id="160a6-147">DimProduct tablosunda ProductCategoryName hesaplanan sütunu oluşturma</span><span class="sxs-lookup"><span data-stu-id="160a6-147">Create a ProductCategoryName calculated column in the DimProduct table</span></span>  
  
1.  <span data-ttu-id="160a6-148">**DimProduct** tablosu hala etkinken **Sütun** menüsüne ve sonra **Sütun Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="160a6-148">With the **DimProduct** table still active, click the **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="160a6-149">Formül çubuğuna aşağıdaki formülü yazın:</span><span class="sxs-lookup"><span data-stu-id="160a6-149">In the formula bar, type the following formula:</span></span>  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  <span data-ttu-id="160a6-150">Sütunu **ProductCategoryName** olarak yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="160a6-150">Rename the column to **ProductCategoryName**.</span></span>  
  
<span data-ttu-id="160a6-151">ProductCategoryName hesaplanan sütunu, DimProductCategory tablosundaki EnglishProductCategoryName sütunundan veriler içeren DimProduct tablosunda bir hiyerarşi oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="160a6-151">The ProductCategoryName calculated column is used to create a hierarchy in the DimProduct table, which includes data from the EnglishProductCategoryName column in the DimProductCategory table.</span></span> <span data-ttu-id="160a6-152">Hiyerarşiler birden fazla tabloya yayılamaz.</span><span class="sxs-lookup"><span data-stu-id="160a6-152">Hierarchies cannot span more than one table.</span></span>  
  
#### <a name="create-a-margin-calculated-column-in-the-factinternetsales-table"></a><span data-ttu-id="160a6-153">FactInternetSales tablosunda Margin hesaplanan sütunu oluşturma</span><span class="sxs-lookup"><span data-stu-id="160a6-153">Create a Margin calculated column in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="160a6-154">Model tasarımcısında **FactInternetSales** tablosunu seçin.</span><span class="sxs-lookup"><span data-stu-id="160a6-154">In the model designer, select the **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="160a6-155">**SalesAmount** sütunu ile **TaxAmt** sütunu arasında yeni bir hesaplanan sütun oluşturun.</span><span class="sxs-lookup"><span data-stu-id="160a6-155">Create a new calculated column between the **SalesAmount** column and the **TaxAmt** column.</span></span>  
  
3.  <span data-ttu-id="160a6-156">Formül çubuğuna aşağıdaki formülü yazın:</span><span class="sxs-lookup"><span data-stu-id="160a6-156">In the formula bar, type the following formula:</span></span>  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  <span data-ttu-id="160a6-157">Sütunu **Margin** olarak yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="160a6-157">Rename the column to **Margin**.</span></span>  
 
      ![aas lesson5 newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    <span data-ttu-id="160a6-159">Margin hesaplanan sütunu, her satış için kar marjını analiz etmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="160a6-159">The Margin calculated column is used to analyze profit margins for each sale.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="160a6-160">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="160a6-160">What's next?</span></span>
<span data-ttu-id="160a6-161">[6. Ders: Ölçü oluşturma](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="160a6-161">[Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>
  
  
  
