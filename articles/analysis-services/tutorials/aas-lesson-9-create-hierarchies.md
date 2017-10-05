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
# <a name="lesson-9-create-hierarchies"></a>9. Ders: Hiyerarşi oluşturma

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Bu derste hiyerarşi oluşturacaksınız. Hiyerarşiler düzeyler halinde düzenlenmiş sütun gruplarıdır. Örneğin, bir Coğrafya hiyerarşisinde Ülke, Eyalet, Şehir ve İlçe alt düzeyleri bulunabilir. Hiyerarşiler raporlama istemcisi uygulama alanı listesinde diğer sütunlardan ayrı görünebilir. Böylece istemci kullanıcıları bu sütunlarda daha kolayca gezinebilir bunları bir rapora daha kolay şekilde ekleyebilir. Daha fazla bilgi için bkz. [Hiyerarşiler](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)
  
Hiyerarşi oluşturmak için *Diyagram Görünümündeki* model tasarımcısını kullanın. Hiyerarşi oluşturma ve yönetme Veri Görünümünde desteklenmemektedir.  
  
Bu dersin tahmini tamamlanma süresi: **20 dakika**  
  
## <a name="prerequisites"></a>Önkoşullar  
Bu konu başlığı, sırayla tamamlanması gereken bir tablosal modelleme öğreticisinin parçasıdır. Bu dersteki görevleri gerçekleştirebilmek için bir önceki dersi tamamlamış olmanız gerekir: [Ders 8: Perspektif oluşturma](../tutorials/aas-lesson-8-create-perspectives.md).  
  
## <a name="create-hierarchies"></a>Hiyerarşi oluşturma  
  
#### <a name="to-create-a-category-hierarchy-in-the-dimproduct-table"></a>DimProduct tablosunda bir Category hiyerarşisi oluşturmak için  
  
1.  Model tasarımcısında (diyagram görünümü), **DimProduct** tablosu > **Hiyerarşi Oluştur**'a sağ tıklayın. Tablo penceresinin alt kısmında yeni bir hiyerarşi görünür. Hiyerarşiyi **Category** olarak yeniden adlandırın.  
  
2.  **ProductCategoryName** sütununa tıklayın ve sütunu **Category** hiyerarşisine sürükleyin.  
  
3.  **Kategori** hiyerarşisinde **ProductCategoryName** > **Yeniden Adlandır**'a sağ tıklayın ve **Category** yazın.  
  
    > [!NOTE]  
    > Hiyerarşideki bir sütunu yeniden adlandırdığınızda tablodaki sütun yeniden adlandırılmaz. Hiyerarşideki sütun tablodaki sütunun yalnızca bir gösterimidir.  
  
4.  **ProductSubcategoryName** sütununa tıklayın ve sütunu **Category** hiyerarşisine sürükleyin. Sütunu **Subcategory** olarak yeniden adlandırın. 
  
5.  **ModelName** sütunu > **Hiyerarşiye Ekle**'ye sağ tıklayın ve **Category**'yi seçin. **Model** olarak yeniden adlandırın.

6.  Son olarak **EnglishProductName**'i Category hiyerarşisine ekleyin. **Product** olarak yeniden adlandırın.  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="to-create-hierarchies-in-the-dimdate-table"></a>DimDate tablosunda hiyerarşi oluşturmak için  
  
1.  **DimDate** tablosunda **Calendar** adlı bir hiyerarşi oluşturun.  
  
3.  Sırayla aşağıdaki sütunları ekleyin:

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  **DimDate** tablosunda **Fiscal** adlı bir hiyerarşi oluşturun. Sırayla aşağıdaki sütunları ekleyin:  
  
    *  FiscalYear
    *  FiscalSemester
    *  FiscalQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
  
5.  Son olarak **DimDate** tablosunda **ProductionCalendar** adlı bir hiyerarşi oluşturun. Sırayla aşağıdaki sütunları ekleyin:  
    *  CalendarYear
    *  WeekNumberOfYear
    *  DayNumberOfWeek
  
 ## <a name="whats-next"></a>Sırada ne var?
[10. Ders: Bölüm oluşturma](../tutorials/aas-lesson-10-create-partitions.md). 
  
  
