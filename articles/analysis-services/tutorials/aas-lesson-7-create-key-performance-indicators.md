---
title: "Azure Analysis Services öğreticisi 7. ders: Ana Performans Göstergeleri Oluşturma | Microsoft Docs"
description: "Azure Analysis Services öğretici projesinde Ana Performans Göstergelerinin nasıl oluşturulacağını açıklar."
services: analysis-services
documentationcenter: 
author: Minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 01/08/2018
ms.author: owend
ms.openlocfilehash: 8f25773541deba2a94d3adc0c9b61c1b90a90aa6
ms.sourcegitcommit: 176c575aea7602682afd6214880aad0be6167c52
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/09/2018
---
# <a name="create-key-performance-indicators"></a>Ana Performans Göstergeleri oluşturma

Bu derste Ana Performans Göstergeleri (KPI) oluşturursunuz. KPI’lar bir *Temel* ölçü ile tanımlanmış bir değerin performansını, yine bir ölçü ya da mutlak değerle tanımlanmış bir *Hedef* değere göre ölçmek için kullanılır. Raporlama istemci uygulamalarında KPI’lar, iş uzmanlarına iş başarısı özetini anlamanın veya eğilimleri belirlemenin hızlı ve kolay bir yöntemini sunabilir. Daha fazla bilgi için bkz. [KPI’lar](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)
  
Bu dersin tahmini tamamlanma süresi: **15 dakika**  
  
## <a name="prerequisites"></a>Önkoşullar  
Bu konu başlığı, sırayla tamamlanması gereken bir tablosal modelleme öğreticisinin parçasıdır. Bu dersteki görevleri gerçekleştirmeden önce, bir önceki dersi tamamlamış olmanız gerekir: [6. Ders: Ölçü oluşturma](../tutorials/aas-lesson-6-create-measures.md).   
  
## <a name="create-key-performance-indicators"></a>Ana Performans Göstergeleri oluşturma  
  
#### <a name="to-create-an-internetcurrentquartersalesperformance-kpi"></a>InternetCurrentQuarterSalesPerformance KPI’si oluşturmak için  
  
1.  Model tasarımcısında **FactInternetSales** tablosuna tıklayın.  
  
2.  Ölçü kılavuzunda boş bir hücreye tıklayın.  
  
3.  Tablonun üzerindeki formül çubuğuna aşağıdaki formülü yazın: 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    Bu ölçü, KPI için temel ölçü olarak görev yapar.  
  
4.  Ölçü kılavuzunda **InternetCurrentQuarterSalesPerformance** > **KPI Oluştur**'a sağ tıklayın.   
  
5.  Ana Performans Göstergesi (KPI) iletişim kutusundaki **Hedef** alanında **Mutlak Değer**’i seçin ve ardından **1.1** yazın.  
  
7.  Sol (alt) kaydırıcı alanına **1** yazın ve sonra sağ (üst) kaydırıcı alanına **1.07** yazın.  
  
8.  **Simge Stili Seçin** bölümünde baklava (kırmızı), üçgen (sarı), yuvarlak (yeşil) simge türünü seçin.
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > Kullanılabilir simge stillerinin altındaki genişletilebilir **Açıklamalar** etiketine dikkat edin. İstemci uygulamalarında daha iyi tanımlanabilmesi için çeşitli KPI öğelerine ilişkin açıklamaları kullanın.  
  
9. KPI’yı tamamlamak için **Tamam**’a tıklayın.  
  
    Ölçü kılavuzunda **InternetCurrentQuarterSalesPerformance** ölçüsünün yanındaki simgeye dikkat edin. Bu simge, bu ölçünün bir KPI’ya ait Temel değer olarak görev yaptığını gösterir.  
  
#### <a name="to-create-an-internetcurrentquartermarginperformance-kpi"></a>InternetCurrentQuarterMarginPerformance KPI’si oluşturmak için  
  
1.  **FactInternetSales** tablosunun ölçü kılavuzunda boş bir hücreye tıklayın.  
  
2.  Tablonun üzerindeki formül çubuğuna aşağıdaki formülü yazın:  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  **InternetCurrentQuarterMarginPerformance** > **KPI Oluştur**’a sağ tıklayın.  
  
4.  Ana Performans Göstergesi (KPI) iletişim kutusundaki **Hedef** alanında **Mutlak Değer**’i seçin ve ardından **1.25** yazın.   
  
5.  Sol (alt) kaydırıcı alanında **0.8** görünene kadar ve sağ (üst) kaydırıcı alanında **1.03** görünene kadar kaydırın.  
  
6.  **Simge Stili Seçin** bölümünde baklava (kırmızı), üçgen (sarı), yuvarlak (yeşil) simge türünü seçip **Tamam**’a tıklayın.  
  
## <a name="whats-next"></a>Sırada ne var?
[8. Ders: Perspektif oluşturma](../tutorials/aas-lesson-8-create-perspectives.md).
  
  
