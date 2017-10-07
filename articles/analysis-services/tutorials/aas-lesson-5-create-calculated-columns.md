---
Başlık: aaa "Azure Analysis Services öğretici Ders 5: hesaplanan sütunlar oluşturma | Microsoft Docs"Açıklama: toocreate hello Azure Analysis Services öğretici proje sütunlarında nasıl hesaplandığını açıklar. Hizmetleri: analysis services documentationcenter: '' Yazar: minewiskan Yöneticisi: erikre Düzenleyicisi: '' etiketler: ''

MS.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get-makalesi ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend
---
# <a name="lesson-5-create-calculated-columns"></a>5. Ders: Hesaplanan sütunlar oluşturma

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Bu derste, hesaplanan sütunlar ekleyerek modelinizde veri oluşturursunuz. Hesaplanan sütun (olarak özel sütunları) oluşturabileceğiniz veri al seçeneğini kullanarak, sorgu Düzenleyicisi'ni kullanarak hello ya da daha sonra hello modeli Tasarımcısı benzer, burada yaparsınız. toolearn daha, fazla [hesaplanan sütunlar](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).
  
Üç farklı tabloda beş yeni hesaplanan sütun oluşturabilirsiniz. Merhaba adımları toocreate sütunları çeşitli yolları vardır, onları yeniden adlandırın ve bunları bir tabloda çeşitli konumlara yerleştirmek gösteren her görev için biraz farklıdır.  

Veri Çözümleme İfadeleri’ni (DAX) de ilk olarak bu derste kullanırsınız. DAX, tablosal modeller için yüksek oranda özelleştirilebilen formül ifadeleri oluşturmaya yönelik özel bir dildir. Bu öğreticide DAX toocreate hesaplanan sütunları, ölçüleri ve rol filtreleri kullanın. toolearn daha, fazla [tablolu modeller DAX](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular). 
  
Bu ders zaman toocomplete tahmini: **15 dakika**  
  
## <a name="prerequisites"></a>Ön koşullar  
Bu konu, sırayla tamamlanması gereken bir tablo modelleme öğreticisinin bir parçasıdır. Bu ders Hello görevleri gerçekleştirmeden önce hello önceki Ders tamamlandı: [Ders 4: ilişkiler oluşturmak](../tutorials/aas-lesson-4-create-relationships.md). 
  
## <a name="create-calculated-columns"></a>Hesaplanan sütunlar oluşturma  
  
#### <a name="create-a-monthcalendar-calculated-column-in-hello-dimdate-table"></a>Merhaba DimDate'i tabloda MonthCalendar hesaplanmış bir sütun oluşturun  
  
1.  Merhaba tıklatın **modeli** menü > **Model görünümü** > **veri görünümü**.  
  
    Hesaplanan sütunlar yalnızca veri görünümü'hello modeli Tasarımcısını kullanarak oluşturulabilir.  
  
2.  Merhaba modeli Tasarımcısı'nda hello tıklayın **DimDate'i** tablosu (sekmesi).  
  
3.  Sağ hello **CalendarQuarter** sütun başlığını ve ardından **Sütun Ekle**.  
  
    Adlı yeni bir sütun **hesaplanan sütun 1** eklenen toohello sol tarafındaki hello **Takvim Çeyrek** sütun.  
  
4.  Hello formül çubuğuna Merhaba tablonun yukarısındaki DAX formülü aşağıdaki hello yazın: yazdığınız otomatik tamamlama yardımcı hello sütunları ve tabloları tam olarak nitelenmiş adlar ve listeleri hello kullanılabilen işlevlerin.  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    Değerleri, ardından tüm hello satırların hello hesaplanmış sütunda doldurulur. Merhaba tabloda aşağı kaydırın, satır hello veriler, her satır göre bu sütun için farklı değerlere sahip olabilir bakın.    
  
5.  Bu sütunu çok yeniden adlandırma**MonthCalendar**. 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
Merhaba MonthCalendar hesaplanan sütun ay sıralanabilir bir ad sağlar.  
  
#### <a name="create-a-dayofweek-calculated-column-in-hello-dimdate-table"></a>Merhaba DimDate'i tabloda DayOfWeek hesaplanmış bir sütun oluşturun  
  
1.  Merhaba ile **DimDate'i** hala etkin tablo, hello tıklatın **sütun** menüsüne ve ardından **Sütun Ekle**.  
  
2.  Merhaba formül çubuğuna formülü aşağıdaki hello yazın:  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    Merhaba formülü oluşturmaya tamamladığınızda, ENTER tuşuna basın. Merhaba yeni sütun toohello Merhaba tablonun sağında eklenir.  
  
3.  Merhaba sütunu çok yeniden adlandırma**DayOfWeek**.  
  
4.  Merhaba sütun başlığını tıklatın ve ardından hello sütun hello arasında sürükleyin **EnglishDayNameOfWeek** sütun ve hello **DayNumberOfMonth** sütun.  
  
    > [!TIP]  
    > Sütunları, tabloda taşıma daha kolay toonavigate kolaylaştırır.  
  
Merhaba DayOfWeek hesaplanan sütun haftanın başlangıç günü sıralanabilir bir ad sağlar.  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-hello-dimproduct-table"></a>Merhaba DimProduct tabloda ProductSubcategoryName hesaplanmış bir sütun oluşturun  
  
  
1.  Merhaba, **DimProduct** tablo, sağda Merhaba tablonun toohello kaydırın. Bildirim hello en sağdaki sütun adlandırılan **Sütun Ekle** (italik) hello sütun başlığını tıklatın.  
  
2.  Merhaba formül çubuğuna formülü aşağıdaki hello yazın:  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  Merhaba sütunu çok yeniden adlandırma**ProductSubcategoryName**.  
  
Merhaba ProductSubcategoryName hesaplanmış kullanılan toocreate hello EnglishProductSubcategoryName sütunundaki verileri hello DimProductSubcategory tabloda içerir hello DimProduct tablosunda bir hiyerarşi bir sütundur. Hiyerarşiler birden fazla tabloya yayılamaz. Hiyerarşileri 9. Derste oluşturacaksınız.  
  
#### <a name="create-a-productcategoryname-calculated-column-in-hello-dimproduct-table"></a>Merhaba DimProduct tabloda ProductCategoryName hesaplanmış bir sütun oluşturun  
  
1.  Merhaba ile **DimProduct** hala etkin tablo, hello tıklatın **sütun** menüsüne ve ardından **Sütun Ekle**.  
  
2.  Merhaba formül çubuğuna formülü aşağıdaki hello yazın:  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  Merhaba sütunu çok yeniden adlandırma**ProductCategoryName**.  
  
Merhaba ProductCategoryName hesaplanmış kullanılan toocreate hello EnglishProductCategoryName sütunundaki verileri hello DimProductCategory tabloda içerir hello DimProduct tablosunda bir hiyerarşi bir sütundur. Hiyerarşiler birden fazla tabloya yayılamaz.  
  
#### <a name="create-a-margin-calculated-column-in-hello-factinternetsales-table"></a>Merhaba Factınternetsales tablosunda kenar boşluğu hesaplanan bir sütun oluşturun  
  
1.  Merhaba Hello modeli Tasarımcısı'nda seçin **Factınternetsales** tablo.  
  
2.  Yeni bir hesaplanmış sütun hello arasında oluşturma **SalesAmount** sütun ve hello **TaxAmt** sütun.  
  
3.  Merhaba formül çubuğuna formülü aşağıdaki hello yazın:  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  Merhaba sütunu çok yeniden adlandırma**kenar boşluğu**.  
 
      ![aas lesson5 newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    Başlangıç kenar boşluğu hesaplanmış sütunu her satış için kullanılan tooanalyze kar kenar boşluklarını ' dir.  
  
## <a name="whats-next"></a>Sırada ne var?
[6. Ders: Ölçü oluşturma](../tutorials/aas-lesson-6-create-measures.md).
  
  
  
