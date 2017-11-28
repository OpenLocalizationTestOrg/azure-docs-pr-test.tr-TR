---
title: "Azure Analysis Services öğreticisi 7. ders: Ana Performans Göstergeleri Oluşturma | Microsoft Docs"
description: "Azure Analysis Services öğretici projesinde Ana Performans Göstergelerinin nasıl oluşturulacağını açıklar."
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
ms.openlocfilehash: d78808421dd5acd907aa9e9000bb3b770a42c061
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-7-create-key-performance-indicators"></a><span data-ttu-id="bced6-103">7. Ders: Ana Performans Göstergeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="bced6-103">Lesson 7: Create Key Performance Indicators</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="bced6-104">Bu derste Ana Performans Göstergeleri (KPI) oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="bced6-104">In this lesson, you create Key Performance Indicators (KPIs).</span></span> <span data-ttu-id="bced6-105">KPI’lar bir *Temel* ölçü ile tanımlanmış bir değerin performansını, yine bir ölçü ya da mutlak değerle tanımlanmış bir *Hedef* değere göre ölçmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bced6-105">KPIs are used to gauge performance of a value defined by a *Base* measure, against a *Target* value also defined by a measure, or by an absolute value.</span></span> <span data-ttu-id="bced6-106">Raporlama istemci uygulamalarında KPI’lar, iş uzmanlarına iş başarısı özetini anlamanın veya eğilimleri belirlemenin hızlı ve kolay bir yöntemini sunabilir.</span><span class="sxs-lookup"><span data-stu-id="bced6-106">In reporting client applications, KPIs can provide business professionals a quick and easy way to understand a summary of business success or to identify trends.</span></span> <span data-ttu-id="bced6-107">Daha fazla bilgi için bkz. [KPI’lar](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="bced6-107">To learn more, see [KPIs](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span></span>
  
<span data-ttu-id="bced6-108">Bu dersin tahmini tamamlanma süresi: **15 dakika**</span><span class="sxs-lookup"><span data-stu-id="bced6-108">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="bced6-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bced6-109">Prerequisites</span></span>  
<span data-ttu-id="bced6-110">Bu konu, sırayla tamamlanması gereken bir tablo modelleme öğreticisinin bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="bced6-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="bced6-111">Bu dersteki görevleri gerçekleştirmeden önce, bir önceki dersi tamamlamış olmanız gerekir: [6. Ders: Ölçü oluşturma](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="bced6-111">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>   
  
## <a name="create-key-performance-indicators"></a><span data-ttu-id="bced6-112">Ana Performans Göstergeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="bced6-112">Create Key Performance Indicators</span></span>  
  
#### <a name="to-create-an-internetcurrentquartersalesperformance-kpi"></a><span data-ttu-id="bced6-113">InternetCurrentQuarterSalesPerformance KPI’si oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="bced6-113">To create an InternetCurrentQuarterSalesPerformance KPI</span></span>  
  
1.  <span data-ttu-id="bced6-114">Model tasarımcısında **FactInternetSales** tablosuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bced6-114">In the model designer, click the **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="bced6-115">Ölçü kılavuzunda boş bir hücreye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bced6-115">In the measure grid, click an empty cell.</span></span>  
  
3.  <span data-ttu-id="bced6-116">Tablonun üzerindeki formül çubuğuna aşağıdaki formülü yazın:</span><span class="sxs-lookup"><span data-stu-id="bced6-116">In the formula bar, above the table, type the following formula:</span></span> 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    <span data-ttu-id="bced6-117">Bu ölçü, KPI için temel ölçü olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="bced6-117">This measure serves as the Base measure for the KPI.</span></span>  
  
4.  <span data-ttu-id="bced6-118">**InternetCurrentQuarterSalesPerformance** > **KPI Oluştur**’a sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bced6-118">Right-click **InternetCurrentQuarterSalesPerformance** > **Create KPI**.</span></span>   
  
5.  <span data-ttu-id="bced6-119">Ana Performans Göstergesi (KPI) iletişim kutusundaki **Hedef** alanında **Mutlak Değer**’i seçin ve ardından **1.1** yazın.</span><span class="sxs-lookup"><span data-stu-id="bced6-119">In the Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.1**.</span></span>  
  
7.  <span data-ttu-id="bced6-120">Sol (alt) kaydırıcı alanına **1** yazın ve sonra sağ (üst) kaydırıcı alanına **1.07** yazın.</span><span class="sxs-lookup"><span data-stu-id="bced6-120">In the left (low) slider field, type **1**, and then in the right (high) slider field, type **1.07**.</span></span>  
  
8.  <span data-ttu-id="bced6-121">**Simge Stili Seçin** bölümünde baklava (kırmızı), üçgen (sarı), yuvarlak (yeşil) simge türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="bced6-121">In **Select Icon Style**, select the diamond (red), triangle (yellow), circle (green) icon type.</span></span>
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > <span data-ttu-id="bced6-123">Kullanılabilir simge stillerinin altındaki genişletilebilir **Açıklamalar** etiketine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="bced6-123">Notice the expandable **Descriptions** label below the available icon styles.</span></span> <span data-ttu-id="bced6-124">İstemci uygulamalarında daha iyi tanımlanabilmesi için çeşitli KPI öğelerine ilişkin açıklamaları kullanın.</span><span class="sxs-lookup"><span data-stu-id="bced6-124">Use descriptions for the various KPI elements to make them more identifiable in client applications.</span></span>  
  
9. <span data-ttu-id="bced6-125">KPI’yı tamamlamak için **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bced6-125">Click **OK** to complete the KPI.</span></span>  
  
    <span data-ttu-id="bced6-126">Ölçü kılavuzunda **InternetCurrentQuarterSalesPerformance** ölçüsünün yanındaki simgeye dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="bced6-126">In the measure grid, notice the icon next to the **InternetCurrentQuarterSalesPerformance** measure.</span></span> <span data-ttu-id="bced6-127">Bu simge, bu ölçünün bir KPI’ya ait Temel değer olarak görev yaptığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="bced6-127">This icon indicates that this measure serves as a Base value for a KPI.</span></span>  
  
#### <a name="to-create-an-internetcurrentquartermarginperformance-kpi"></a><span data-ttu-id="bced6-128">InternetCurrentQuarterMarginPerformance KPI’si oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="bced6-128">To create an InternetCurrentQuarterMarginPerformance KPI</span></span>  
  
1.  <span data-ttu-id="bced6-129">**FactInternetSales** tablosunun ölçü kılavuzunda boş bir hücreye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bced6-129">In the measure grid for the **FactInternetSales** table, click an empty cell.</span></span>  
  
2.  <span data-ttu-id="bced6-130">Tablonun üzerindeki formül çubuğuna aşağıdaki formülü yazın:</span><span class="sxs-lookup"><span data-stu-id="bced6-130">In the formula bar, above the table, type the following formula:</span></span>  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  <span data-ttu-id="bced6-131">**InternetCurrentQuarterMarginPerformance** > **KPI Oluştur**’a sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bced6-131">Right-click **InternetCurrentQuarterMarginPerformance** > **Create KPI**.</span></span>  
  
4.  <span data-ttu-id="bced6-132">Ana Performans Göstergesi (KPI) iletişim kutusundaki **Hedef** alanında **Mutlak Değer**’i seçin ve ardından **1.25** yazın.</span><span class="sxs-lookup"><span data-stu-id="bced6-132">In the Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.25**.</span></span>   
  
5.  <span data-ttu-id="bced6-133">Sol (alt) kaydırıcı alanında **0.8** görünene kadar ve sağ (üst) kaydırıcı alanında **1.03** görünene kadar kaydırın.</span><span class="sxs-lookup"><span data-stu-id="bced6-133">In the left (low) slider field, slide until the field displays **0.8**, and then slide the right (high) slider field, until the field displays **1.03**.</span></span>  
  
6.  <span data-ttu-id="bced6-134">**Simge Stili Seçin** bölümünde baklava (kırmızı), üçgen (sarı), yuvarlak (yeşil) simge türünü seçip **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bced6-134">In **Select Icon Style**, select the diamond (red), triangle (yellow), circle (green) icon type, and then click **OK**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="bced6-135">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="bced6-135">What's next?</span></span>
<span data-ttu-id="bced6-136">[8. Ders: Perspektif oluşturma](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="bced6-136">[Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>
  
  
