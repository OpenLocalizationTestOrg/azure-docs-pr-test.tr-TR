---
Başlık: aaa "Azure Analysis Services öğretici ek Ders: ayrıntı satırları | Microsoft Docs"Açıklama: nasıl toocreate ayrıntı satır ifadesinde bir hello Azure Analysis Services öğretici açıklar.
Hizmetleri: analysis services documentationcenter: '' Yazar: minewiskan Yöneticisi: erikre Düzenleyicisi: '' etiketler: ''

MS.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get-makalesi ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend
---
# <a name="supplemental-lesson---detail-rows"></a>Ek ders - Ayrıntı Satırları

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Bu ek Ders içinde özel bir ayrıntı satırları ifade hello DAX Düzenleyicisi toodefine kullanın. Bir ayrıntı satırları ifadesi bir ölçü üzerinde son kullanıcılar bir ölçünün bir araya getirilir hello sonuçlarıyla ilgili daha fazla bilgi sağlayan bir özelliğidir. 
  
Bu ders zaman toocomplete tahmini: **10 dakika**  
  
## <a name="prerequisites"></a>Ön koşullar  
Bu ek ders konusu bir tablo modelleme öğreticisinin parçasıdır. Bu ek Ders Hello görevleri gerçekleştirmeden önce tüm önceki dersleri tamamladınız veya bir tamamlanmış Adventure Works Internet satış örnek modeli projesi.  
  
## <a name="what-do-we-need-toosolve"></a>Ne toosolve ihtiyacımız var?
Ayrıntı satırları ifade eklemeden önce bizim InternetTotalSales ölçü hello ayrıntıları bakalım.

1.  Merhaba SSDT içinde tıklatın **modeli** menü > **Excel'de çözümleme özelliği** tooopen Excel ve boş bir PivotTable oluşturun.
  
2.  İçinde **PivotTable alanları**, hello eklemek **InternetTotalSales** hello Factınternetsales tablosundan çok ölçü**değerleri**, **CalendarYear**hello DimDate'i ' çok tablo**sütunları**, ve **EnglishCountryRegionName** çok**satırları**. Bizim PivotTable artık bize toplanmış sonuçları bölgeler ve yıl hello InternetTotalSales ölçünün gelen sağlar. 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. Hello PivotTable'da, bir yılın ve bölge adı için bir toplu değeri çift tıklatın. Burada size Avustralya ve hello için hello değer yıl 2014 çift. Verileri (yararlı olmayan verileri) içeren yeni bir sayfa açılır.

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
Burada toosee bizim InternetTotalSales ölçü toplanan toohello sonucunu katkıda veri satırları ve sütunları içeren bir tablo gibi ne biz olacaktır. Ayrıntı satırları ifade hello ölçü bir özellik olarak ekleyebiliriz, toodo.

## <a name="add-a-detail-rows-expression"></a>Ayrıntı Satırları İfadesi ekleme

#### <a name="toocreate-a-detail-rows-expression"></a>toocreate bir ayrıntı satırları ifadesi 
  
1. SSDT içinde hello Factınternetsales tablonun ölçü kılavuzda hello tıklatın **InternetTotalSales** ölçü. 

2. İçinde **özellikleri** > **ayrıntı satırları ifade**, hello Düzenleyicisi düğmesi tooopen hello DAX Düzenleyicisi'ni tıklatın.

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. DAX Düzenleyicisi'nde hello ifade aşağıdaki girin:

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

    Bu ifade adlarının, sütun belirtir ve bir kullanıcı bir PivotTable veya rapor toplanmış bir sonuca tıklattığında hello Factınternetsales tablosunda ve ilgili tablolardaki ölçü sonuçlar döndürülür.

4. Geri Excel'de adım 3'te oluşturulan hello sayfayı silmek, sonra bir toplu değeri çift tıklatın. Bu süre, hello ölçü için tanımlanmış bir ayrıntı satırları ifade özelliği ile çok daha kullanışlı verileri içeren yeni bir sayfa açar.

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. Modelinizi yeniden dağıtın.

  
## <a name="see-also"></a>Ayrıca Bkz.  
[SELECTCOLUMNS İşlevi (DAX)](https://msdn.microsoft.com/library/mt761759.aspx)   
[Ek Ders - Dinamik güvenlik](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[Ek Ders - Düzensiz hiyerarşiler](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
