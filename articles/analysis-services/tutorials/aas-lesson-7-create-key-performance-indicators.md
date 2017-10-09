---
Başlık: aaa "Azure Analysis Services öğretici Ders 7: anahtar performans göstergelerini oluşturun | Microsoft Docs"Açıklama: öğretici Azure Analysis Services projesi toocreate anahtar performans göstergelerinin nasıl hello açıklar. Hizmetleri: analysis services documentationcenter: '' Yazar: minewiskan Yöneticisi: erikre Düzenleyicisi: '' etiketler: ''

MS.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get-makalesi ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend
---
# <a name="lesson-7-create-key-performance-indicators"></a>7. Ders: Ana Performans Göstergeleri oluşturma

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Bu derste Ana Performans Göstergeleri (KPI) oluşturursunuz. KPI'ları tarafından tanımlanan bir değer kullanılan toogauge performansını olan bir *temel* ölçüsü karşı bir *hedef* ayrıca bir ölçü veya mutlak bir değer tarafından tanımlanan bir değer. İstemci uygulamaları raporlamada KPI'leri iş uzmanları hızlı ve kolay bir yol toounderstand iş başarı veya tooidentify eğilimlerini özetini sağlar. toolearn daha, fazla [KPI'ları](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)
  
Bu ders zaman toocomplete tahmini: **15 dakika**  
  
## <a name="prerequisites"></a>Ön koşullar  
Bu konu, sırayla tamamlanması gereken bir tablo modelleme öğreticisinin bir parçasıdır. Bu ders Hello görevleri gerçekleştirmeden önce hello önceki Ders tamamlandı: [Ders 6: ölçüleri oluşturma](../tutorials/aas-lesson-6-create-measures.md).   
  
## <a name="create-key-performance-indicators"></a>Ana Performans Göstergeleri oluşturma  
  
#### <a name="toocreate-an-internetcurrentquartersalesperformance-kpi"></a>toocreate InternetCurrentQuarterSalesPerformance KPI  
  
1.  Merhaba modeli Tasarımcısı'nda hello tıklayın **Factınternetsales** tablo.  
  
2.  Merhaba ölçü kılavuzunda, boş bir hücreyi tıklatın.  
  
3.  Merhaba tablonun yukarısındaki hello formül çubuğundaki formülü aşağıdaki hello yazın: 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    Bu ölçü hello KPI için hello temel ölçü olarak görev yapar.  
  
4.  **InternetCurrentQuarterSalesPerformance** > **KPI Oluştur**’a sağ tıklayın.   
  
5.  Merhaba ana performans göstergesi (KPI) iletişim kutusunda, **hedef** seçin **mutlak değeri**ve ardından **1.1**.  
  
7.  Merhaba sol (düşük) kaydırıcı alanına yazın **1**ve ardından hello sağa (yüksek) kaydırıcı alanında, yazın **1.07**.  
  
8.  İçinde **simgesi stil seçin**, hello baklava (kırmızı), üçgen (sarı) seçin, yuvarlak (yeşil) simge türü.
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > Bildirim hello Genişletilebilir **açıklamaları** hello kullanılabilir simgesi stilleri altına etiketi. Merhaba açıklamalarını kullan çeşitli KPI öğeleri toomake bunları istemci uygulamalarında daha tanımlanabilir.  
  
9. Tıklatın **Tamam** toocomplete hello KPI.  
  
    Merhaba ölçü kılavuzunda hello simgesi sonraki toohello fark **InternetCurrentQuarterSalesPerformance** ölçü. Bu simge, bu ölçünün bir KPI’ya ait Temel değer olarak görev yaptığını gösterir.  
  
#### <a name="toocreate-an-internetcurrentquartermarginperformance-kpi"></a>toocreate InternetCurrentQuarterMarginPerformance KPI  
  
1.  Hello için hello ölçü kılavuzunda **Factınternetsales** tablo, boş bir hücreyi tıklatın.  
  
2.  Merhaba tablonun yukarısındaki hello formül çubuğundaki formülü aşağıdaki hello yazın:  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  **InternetCurrentQuarterMarginPerformance** > **KPI Oluştur**’a sağ tıklayın.  
  
4.  Merhaba ana performans göstergesi (KPI) iletişim kutusunda, **hedef** seçin **mutlak değeri**ve ardından **1,25**.   
  
5.  Merhaba alan görüntüler kadar hello sol (düşük) kaydırıcı alanında, slayt **0,8**, ve ardından slayt hello sağ (yüksek) kaydırıcı alan hello alan görüntüler kadar **1,03 koyun**.  
  
6.  İçinde **simgesi stil seçin**hello elmas (kırmızı), üçgen (sarı), daire (yeşil) simge türü seçin ve ardından **Tamam**.  
  
## <a name="whats-next"></a>Sırada ne var?
[8. Ders: Perspektif oluşturma](../tutorials/aas-lesson-8-create-perspectives.md).
  
  
