---
Başlık: aaa "Azure Analysis Services öğretici Ders 6: ölçüleri oluşturun | Microsoft Docs"Açıklama: toocreate hello Azure Analysis Services öğretici projesinde nasıl ölçer açıklar. Hizmetleri: analysis services documentationcenter: '' Yazar: minewiskan Yöneticisi: erikre Düzenleyicisi: '' etiketler: ''

MS.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get-makalesi ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend
---
# <a name="lesson-6-create-measures"></a>6. Ders: Ölçü oluşturma

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Bu alıştırmanın ilerisinde modelinizde dahil ölçüleri toobe oluşturun. Oluşturduğunuz sütunlara benzer toohello hesaplanan, bir ölçü bir DAX formülü kullanılarak oluşturulan bir hesaplama. Bununla birlikte, hesaplanan sütunlardan farklı olarak ölçüler kullanıcı tarafından seçilen bir *filtre* temel alınarak değerlendirilir. Örneğin, belirli sütun veya dilimleyici toohello satır etiketleri alan bir PivotTable eklendi. Her hücre hello filtresi için bir değer hello uygulanan ölçünün sonra hesaplanır. Neredeyse tüm tablolu modeller tooperform dinamik hesaplamaları sayısal veri tooinclude istediğiniz güçlü ve esnek hesaplamalar yöntemleridir. toolearn daha, fazla [ölçüleri](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).
  
toocreate ölçüleri kullandığınız hello *ölçü kılavuz*. Varsayılan olarak, her tablonun boş bir ölçüm kılavuzu vardır; bununla birlikte, genellikle her tablo için ölçü oluşturmazsınız. Merhaba ölçü kılavuz veri görünümündeki hello modeli Tasarımcısı'nda bir tablo aşağıda yer almaktadır. toohide veya Göster hello ölçü bir tablo için kılavuz hello **tablo** menüsüne ve ardından **ölçü Izgarayı Göster**.  
  
Boş bir hücre hello ölçü kılavuzunda tıklattıktan sonra hello formül çubuğuna bir DAX formülü yazarak bir ölçü oluşturun. Ne zaman ENTER toocomplete hello formülü hello ölçü tıklatın ardından hello hücrede görünür. Ayrıca bir sütuna tıklayarak standart toplama işlevi kullanılarak ölçüleri oluşturabilir ve hello Otomatik Toplam düğmesini tıklatarak (**∑**) hello araç. Merhaba otomatik toplam özelliğini kullanarak oluşturulan ölçüleri hello ölçü kılavuz hücresinin doğrudan hello sütunu altında görünür, ancak taşınabilir.  
  
Bu alıştırmanın ilerisinde ölçüler, her iki girerek bir DAX formülü hello formül çubuğuna ve hello otomatik toplam özelliğini kullanarak oluşturun.  
  
Bu ders zaman toocomplete tahmini: **30 dakika**  
  
## <a name="prerequisites"></a>Ön koşullar  
Bu konu, sırayla tamamlanması gereken bir tablo modelleme öğreticisinin bir parçasıdır. Bu ders Hello görevleri gerçekleştirmeden önce hello önceki Ders tamamlandı: [Ders 5: hesaplanan sütunlar oluşturma](../tutorials/aas-lesson-5-create-calculated-columns.md).  
  
## <a name="create-measures"></a>Ölçü oluşturma  
  
#### <a name="toocreate-a-dayscurrentquartertodate-measure-in-hello-dimdate-table"></a>toocreate hello DimDate'i tablosunda DaysCurrentQuarterToDate ölçü  
  
1.  Merhaba modeli Tasarımcısı'nda hello tıklayın **DimDate'i** tablo.  
  
2.  Merhaba ölçü kılavuzunda hello sol üst boş hücreyi tıklatın.  
  
3.  Merhaba formül çubuğuna formülü aşağıdaki hello yazın:  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    Bildirim hello sol üst hücre şimdi bir ölçü adı içeriyor **DaysCurrentQuarterToDate**hello sonucu, ardından **92**.
    
      ![aas-lesson6-newmeasure](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    Hesaplanan sütunlar, ölçü formüllerle hello formül ifadeyle üste ve ardından hello ölçü adı yazabilirsiniz.

  
#### <a name="toocreate-a-daysincurrentquarter-measure-in-hello-dimdate-table"></a>toocreate hello DimDate'i tablosunda DaysInCurrentQuarter ölçü  
  
1.  Merhaba ile **DimDate'i** hello ölçü kılavuzunda hello modeli Tasarımcısı'nda hala etkin tablo, boş bir hücre hello oluşturduğunuz hello ölçü aşağıda'ı tıklatın.  
  
2.  Merhaba formül çubuğuna formülü aşağıdaki hello yazın:  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    Bir tamamlanmamış dönemi ve hello arasında bir karşılaştırma oranı önceki dönem oluştururken. Merhaba formülü, geçti hello dönemi hello oranını hesaplamak ve aynı hello önceki dönemi oranı toohello karşılaştırır. Bu durumda, [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] verir hello oranı hello geçerli süre geçti.  
  
#### <a name="toocreate-an-internetdistinctcountsalesorder-measure-in-hello-factinternetsales-table"></a>toocreate hello Factınternetsales tablosunda InternetDistinctCountSalesOrder ölçü  
  
1.  Merhaba tıklatın **Factınternetsales** tablo.   
  
2.  Merhaba tıklatın **SalesOrderNumber** sütun başlığı.  
  
3.  Merhaba araç çubuğunda hello aşağı ok sonraki toohello otomatik toplam'ı tıklatın (**∑**) düğmesine tıklayın ve ardından **DistinctCount**.  
  
    Merhaba otomatik toplam özelliğini otomatik olarak hello DistinctCount standart toplama formülü kullanarak hello seçili sütun için bir ölçü oluşturur.  
    
       ![aas-lesson6-newmeasure2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  Merhaba ölçü kılavuzda hello yeni ölçü tıklatın ve ardından hello **özellikleri** penceresi, **ölçü adı**, hello ölçü çok yeniden adlandırma**InternetDistinctCountSalesOrder**. 
 
  
#### <a name="toocreate-additional-measures-in-hello-factinternetsales-table"></a>Merhaba Factınternetsales tablosunda toocreate ek ölçümler  
  
1.  Merhaba otomatik toplam özelliğini kullanarak oluşturun ve ölçüleri aşağıdaki hello adlandırın:  

    |Sütun|Ölçü adı|Otomatik Toplam (∑)|Formül|  
    |----------------|----------|-----------------|-----------|  
    |SalesOrderLineNumber|InternetOrderLinesCount|Sayı|=COUNTA([SalesOrderLineNumber])|  
    |OrderQuantity|InternetTotalUnits|Toplam|=SUM([OrderQuantity])|  
    |DiscountAmount|InternetTotalDiscountAmount|Toplam|=SUM([DiscountAmount])|  
    |TotalProductCost|InternetTotalProductCost|Toplam|=SUM([TotalProductCost])|  
    |SalesAmount|InternetTotalSales|Toplam|=SUM([SalesAmount])|  
    |Marj|InternetTotalMargin|Toplam|=SUM([Margin])|  
    |TaxAmt|InternetTotalTaxAmt|Toplam|=SUM([TaxAmt])|  
    |Nakliye|InternetTotalFreight|Toplam|=SUM([Freight])|  
  
2.  Boş bir hücreye hello ölçü kılavuzunda ve hello formül çubuğu kullanarak tıklayarak oluşturun ve ad hello aşağıdaki sırayla ölçer:  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
Merhaba Factınternetsales tablosunda için oluşturulan ölçüleri kullanılan tooanalyze satış, maliyetleri ve hello kullanıcı seçilen filtre tarafından tanımlanan öğeleri için kar marjı gibi kritik finansal verileri olabilir.  
  
## <a name="whats-next"></a>Sırada ne var?
[7. Ders: Önemli Performans Göstergeleri oluşturma](../tutorials/aas-lesson-7-create-key-performance-indicators.md).  

  
