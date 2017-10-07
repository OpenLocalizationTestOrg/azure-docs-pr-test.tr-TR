---
Başlık: aaa "Azure Analysis Services öğretici Ders 9: hiyerarşileri oluşturun | Microsoft Docs"Açıklama: Hizmetleri: analysis services documentationcenter: '' Yazar: minewiskan Yöneticisi: erikre Düzenleyicisi: '' etiketler: ''

MS.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get-makalesi ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend
---
# <a name="lesson-9-create-hierarchies"></a>9. Ders: Hiyerarşi oluşturma

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Bu derste hiyerarşi oluşturacaksınız. Hiyerarşiler düzeyler halinde düzenlenmiş sütun gruplarıdır. Örneğin, bir Coğrafya hiyerarşisinde Ülke, Eyalet, Şehir ve İlçe alt düzeyleri bulunabilir. Hiyerarşileri, kullanıcıların toonavigate istemci için daha kolay hale getirme diğer sütunlar listesinde bir raporlama istemci uygulaması alan ayrı görünür ve bir rapora dahil. toolearn daha, fazla [hiyerarşileri](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)
  
toocreate hiyerarşileri hello modeli Tasarımcısı'nda kullanmak *diyagram görünümü*. Hiyerarşi oluşturma ve yönetme Veri Görünümünde desteklenmemektedir.  
  
Bu ders zaman toocomplete tahmini: **20 dakika**  
  
## <a name="prerequisites"></a>Ön koşullar  
Bu konu, sırayla tamamlanması gereken bir tablo modelleme öğreticisinin bir parçasıdır. Bu ders Hello görevleri gerçekleştirmeden önce hello önceki Ders tamamlandı: [Ders 8: Perspektif oluşturmak](../tutorials/aas-lesson-8-create-perspectives.md).  
  
## <a name="create-hierarchies"></a>Hiyerarşi oluşturma  
  
#### <a name="toocreate-a-category-hierarchy-in-hello-dimproduct-table"></a>toocreate hello DimProduct tablosundaki kategori hiyerarşisi  
  
1.  Merhaba Hello modeli Tasarımcısı'nda (diyagram görünümünü) sağ **DimProduct** Tablo > **oluşturma hiyerarşi**. Yeni bir hiyerarşiye hello tablo penceresinin hello altında görüntülenir. Merhaba hiyerarşi yeniden adlandırma **kategori**.  
  
2.  Merhaba sürükleyip **ProductCategoryName** yeni sütun toohello **kategori** hiyerarşisi.  
  
3.  Merhaba, **kategori** hiyerarşi, sağ hello **ProductCategoryName** > **yeniden adlandırma**ve ardından **kategori**.  
  
    > [!NOTE]  
    > Bir hiyerarşideki bir sütunu yeniden adlandırma hello tablosundaki bu sütunu yeniden adlandırmak değil. Bir sütun bir hiyerarşideki yalnızca Merhaba tablonun hello sütununda bir gösterimidir.  
  
4.  Merhaba sürükleyip **ProductSubcategoryName** sütun toohello **kategori** hiyerarşisi. Sütunu **Subcategory** olarak yeniden adlandırın. 
  
5.  Sağ hello **ModelName** sütun > **toohierarchy ekleme**ve ardından **kategori**. **Model** olarak yeniden adlandırın.

6.  Son olarak, ekleme **EnglishProductName** toohello kategori hiyerarşisi. **Product** olarak yeniden adlandırın.  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="toocreate-hierarchies-in-hello-dimdate-table"></a>Merhaba DimDate'i tablosundaki toocreate hiyerarşileri  
  
1.  Merhaba, **DimDate'i** tablo, adlı bir hiyerarşi oluşturmak **Takvim**.  
  
3.  Sıralı sütunları aşağıdaki hello ekleyin:

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  Merhaba, **DimDate'i** tablo, oluşturma bir **mali** hiyerarşisi. Sıralı sütunları aşağıdaki hello şunları içerir:  
  
    *  FiscalYear
    *  FiscalSemester
    *  FiscalQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
  
5.  Son olarak, hello içinde **DimDate'i** tablo, oluşturma bir **ProductionCalendar** hiyerarşisi. Sıralı sütunları aşağıdaki hello şunları içerir:  
    *  CalendarYear
    *  WeekNumberOfYear
    *  DayNumberOfWeek
  
 ## <a name="whats-next"></a>Sırada ne var?
[10. Ders: Bölüm oluşturma](../tutorials/aas-lesson-10-create-partitions.md). 
  
  
