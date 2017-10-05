---
title: "Azure Analysis Services öğreticisi - 9. Ders: Hiyerarşi oluşturma | Microsoft Docs"
description: 
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
ms.openlocfilehash: d628dc621335acf231342a6d9186079de16e85f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-9-create-hierarchies"></a><span data-ttu-id="1e7b8-102">9. Ders: Hiyerarşi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1e7b8-102">Lesson 9: Create hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="1e7b8-103">Bu derste hiyerarşi oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="1e7b8-103">In this lesson, you create hierarchies.</span></span> <span data-ttu-id="1e7b8-104">Hiyerarşiler düzeyler halinde düzenlenmiş sütun gruplarıdır. Örneğin, bir Coğrafya hiyerarşisinde Ülke, Eyalet, Şehir ve İlçe alt düzeyleri bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="1e7b8-104">Hierarchies are groups of columns arranged in levels; for example, a Geography hierarchy might have sublevels for Country, State, County, and City.</span></span> <span data-ttu-id="1e7b8-105">Hiyerarşiler raporlama istemcisi uygulama alanı listesinde diğer sütunlardan ayrı görünebilir. Böylece istemci kullanıcıları bu sütunlarda daha kolayca gezinebilir bunları bir rapora daha kolay şekilde ekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="1e7b8-105">Hierarchies can appear separate from other columns in a reporting client application field list, making them easier for client users to navigate and include in a report.</span></span> <span data-ttu-id="1e7b8-106">Daha fazla bilgi için bkz. [Hiyerarşiler](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="1e7b8-106">To learn more, see [Hierarchies](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span></span>
  
<span data-ttu-id="1e7b8-107">Hiyerarşi oluşturmak için *Diyagram Görünümündeki* model tasarımcısını kullanın.</span><span class="sxs-lookup"><span data-stu-id="1e7b8-107">To create hierarchies, use the model designer in *Diagram View*.</span></span> <span data-ttu-id="1e7b8-108">Hiyerarşi oluşturma ve yönetme Veri Görünümünde desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="1e7b8-108">Creating and managing hierarchies is not supported in Data View.</span></span>  
  
<span data-ttu-id="1e7b8-109">Bu dersin tahmini tamamlanma süresi: **20 dakika**</span><span class="sxs-lookup"><span data-stu-id="1e7b8-109">Estimated time to complete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="1e7b8-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="1e7b8-110">Prerequisites</span></span>  
<span data-ttu-id="1e7b8-111">Bu konu başlığı, sırayla tamamlanması gereken bir tablosal modelleme öğreticisinin parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="1e7b8-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="1e7b8-112">Bu dersteki görevleri gerçekleştirebilmek için bir önceki dersi tamamlamış olmanız gerekir: [Ders 8: Perspektif oluşturma](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="1e7b8-112">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>  
  
## <a name="create-hierarchies"></a><span data-ttu-id="1e7b8-113">Hiyerarşi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1e7b8-113">Create hierarchies</span></span>  
  
#### <a name="to-create-a-category-hierarchy-in-the-dimproduct-table"></a><span data-ttu-id="1e7b8-114">DimProduct tablosunda bir Category hiyerarşisi oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="1e7b8-114">To create a Category hierarchy in the DimProduct table</span></span>  
  
1.  <span data-ttu-id="1e7b8-115">Model tasarımcısında (diyagram görünümü), **DimProduct** tablosu > **Hiyerarşi Oluştur**'a sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1e7b8-115">In the model designer (diagram view), right-click the **DimProduct** table > **Create Hierarchy**.</span></span> <span data-ttu-id="1e7b8-116">Tablo penceresinin alt kısmında yeni bir hiyerarşi görünür.</span><span class="sxs-lookup"><span data-stu-id="1e7b8-116">A new hierarchy appears at the bottom of the table window.</span></span> <span data-ttu-id="1e7b8-117">Hiyerarşiyi **Category** olarak yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="1e7b8-117">Rename the hierarchy **Category**.</span></span>  
  
2.  <span data-ttu-id="1e7b8-118">**ProductCategoryName** sütununa tıklayın ve sütunu **Category** hiyerarşisine sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="1e7b8-118">Click and drag the **ProductCategoryName** column to the new **Category** hierarchy.</span></span>  
  
3.  <span data-ttu-id="1e7b8-119">**Kategori** hiyerarşisinde **ProductCategoryName** > **Yeniden Adlandır**'a sağ tıklayın ve **Category** yazın.</span><span class="sxs-lookup"><span data-stu-id="1e7b8-119">In the **Category** hierarchy, right-click the **ProductCategoryName** > **Rename**, and then type **Category**.</span></span>  
  
    > [!NOTE]  
    > <span data-ttu-id="1e7b8-120">Hiyerarşideki bir sütunu yeniden adlandırdığınızda tablodaki sütun yeniden adlandırılmaz.</span><span class="sxs-lookup"><span data-stu-id="1e7b8-120">Renaming a column in a hierarchy does not rename that column in the table.</span></span> <span data-ttu-id="1e7b8-121">Hiyerarşideki sütun tablodaki sütunun yalnızca bir gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="1e7b8-121">A column in a hierarchy is just a representation of the column in the table.</span></span>  
  
4.  <span data-ttu-id="1e7b8-122">**ProductSubcategoryName** sütununa tıklayın ve sütunu **Category** hiyerarşisine sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="1e7b8-122">Click and drag the **ProductSubcategoryName** column to the **Category** hierarchy.</span></span> <span data-ttu-id="1e7b8-123">Sütunu **Subcategory** olarak yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="1e7b8-123">Rename it **Subcategory**.</span></span> 
  
5.  <span data-ttu-id="1e7b8-124">**ModelName** sütunu > **Hiyerarşiye Ekle**'ye sağ tıklayın ve **Category**'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="1e7b8-124">Right-click the **ModelName** column > **Add to hierarchy**, and then select **Category**.</span></span> <span data-ttu-id="1e7b8-125">**Model** olarak yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="1e7b8-125">Rename it **Model**.</span></span>

6.  <span data-ttu-id="1e7b8-126">Son olarak **EnglishProductName**'i Category hiyerarşisine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1e7b8-126">Finally, add **EnglishProductName** to the Category hierarchy.</span></span> <span data-ttu-id="1e7b8-127">**Product** olarak yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="1e7b8-127">Rename it **Product**.</span></span>  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="to-create-hierarchies-in-the-dimdate-table"></a><span data-ttu-id="1e7b8-129">DimDate tablosunda hiyerarşi oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="1e7b8-129">To create hierarchies in the DimDate table</span></span>  
  
1.  <span data-ttu-id="1e7b8-130">**DimDate** tablosunda **Calendar** adlı bir hiyerarşi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1e7b8-130">In the **DimDate** table, create a hierarchy named **Calendar**.</span></span>  
  
3.  <span data-ttu-id="1e7b8-131">Sırayla aşağıdaki sütunları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1e7b8-131">Add the following columns in-order:</span></span>

    *  <span data-ttu-id="1e7b8-132">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="1e7b8-132">CalendarYear</span></span>
    *  <span data-ttu-id="1e7b8-133">CalendarSemester</span><span class="sxs-lookup"><span data-stu-id="1e7b8-133">CalendarSemester</span></span>
    *  <span data-ttu-id="1e7b8-134">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="1e7b8-134">CalendarQuarter</span></span>
    *  <span data-ttu-id="1e7b8-135">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="1e7b8-135">MonthCalendar</span></span>
    *  <span data-ttu-id="1e7b8-136">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="1e7b8-136">DayNumberOfMonth</span></span>
    
4.  <span data-ttu-id="1e7b8-137">**DimDate** tablosunda **Fiscal** adlı bir hiyerarşi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1e7b8-137">In the **DimDate** table, create a **Fiscal** hierarchy.</span></span> <span data-ttu-id="1e7b8-138">Sırayla aşağıdaki sütunları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1e7b8-138">Include the following columns in-order:</span></span>  
  
    *  <span data-ttu-id="1e7b8-139">FiscalYear</span><span class="sxs-lookup"><span data-stu-id="1e7b8-139">FiscalYear</span></span>
    *  <span data-ttu-id="1e7b8-140">FiscalSemester</span><span class="sxs-lookup"><span data-stu-id="1e7b8-140">FiscalSemester</span></span>
    *  <span data-ttu-id="1e7b8-141">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="1e7b8-141">FiscalQuarter</span></span>
    *  <span data-ttu-id="1e7b8-142">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="1e7b8-142">MonthCalendar</span></span>
    *  <span data-ttu-id="1e7b8-143">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="1e7b8-143">DayNumberOfMonth</span></span>
  
5.  <span data-ttu-id="1e7b8-144">Son olarak **DimDate** tablosunda **ProductionCalendar** adlı bir hiyerarşi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1e7b8-144">Finally, in the **DimDate** table, create a **ProductionCalendar** hierarchy.</span></span> <span data-ttu-id="1e7b8-145">Sırayla aşağıdaki sütunları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1e7b8-145">Include the following columns in-order:</span></span>  
    *  <span data-ttu-id="1e7b8-146">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="1e7b8-146">CalendarYear</span></span>
    *  <span data-ttu-id="1e7b8-147">WeekNumberOfYear</span><span class="sxs-lookup"><span data-stu-id="1e7b8-147">WeekNumberOfYear</span></span>
    *  <span data-ttu-id="1e7b8-148">DayNumberOfWeek</span><span class="sxs-lookup"><span data-stu-id="1e7b8-148">DayNumberOfWeek</span></span>
  
 ## <a name="whats-next"></a><span data-ttu-id="1e7b8-149">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="1e7b8-149">What's next?</span></span>
<span data-ttu-id="1e7b8-150">[10. Ders: Bölüm oluşturma](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="1e7b8-150">[Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span> 
  
  
