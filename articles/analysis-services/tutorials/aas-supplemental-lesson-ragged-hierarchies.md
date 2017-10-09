---
Başlık: aaa "Azure Analysis Services öğretici ek Ders: düzensiz hiyerarşileri | Microsoft Docs"Açıklama: toofix hiyerarşileri hello Azure Analysis Services öğreticide nasıl düzensiz açıklar.
Hizmetleri: analysis services documentationcenter: '' Yazar: minewiskan Yöneticisi: erikre Düzenleyicisi: '' etiketler: ''

MS.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get-makalesi ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend
---
# <a name="supplemental-lesson---ragged-hierarchies"></a>Ek ders - Düzensiz hiyerarşiler

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Bu ek derste, farklı düzeylerde boş değerler (üyeler) içeren hiyerarşileri özetlerken karşılaşılan ortak bir sorunu çözümlersiniz. Örneğin, bir üst düzey yöneticiye bağlı departman yöneticilerinin ve yönetici olmayan çalışanların olduğu bir kuruluşta. Veya, Ülke-Bölge-Şehirden oluşan ve Washington D.C., Vatikan gibi bazı şehirlerde üst Eyalet veya Bölgenin olmadığı coğrafi hiyerarşilerde. Bir hiyerarşi boş üyeleri olduğunda, genellikle toodifferent terri veya düzensiz düzeyleri.

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

Tablolu modeller hello 1400 uyumluluk düzeyine sahip bir ek **Gizle üyeleri** Hiyerarşiler için özellik. Merhaba **varsayılan** ayarı varsayar herhangi bir düzeyde boş üye yok. Merhaba **Gizle boş üyeleri** ayarı eklendiğinde hello hiyerarşiden boş üyeleri dışlar tooa PivotTable veya rapor.  
  
Bu ders zaman toocomplete tahmini: **20 dakika**  
  
## <a name="prerequisites"></a>Ön koşullar  
Bu ek ders konusu bir tablo modelleme öğreticisinin parçasıdır. Bu ek Ders Hello görevleri gerçekleştirmeden önce tüm önceki dersleri tamamladınız veya bir tamamlanmış Adventure Works Internet satış örnek modeli projesi. 

Merhaba öğreticinin bir parçası olarak hello AW Internet satış proje oluşturduysanız, herhangi bir veri ya da düzensiz hiyerarşileri modelinizi henüz içermiyor. toocomplete bu ek Ders önce Merhaba sorunu bazı ek tablolar ekleyerek, ilişkileri, hesaplanan sütunlarda, bir ölçü ve yeni bir kuruluş hiyerarşisi oluşturmak toocreate olması. Bu kısım yaklaşık 15 dakika sürer. Daha sonra toosolve almak yalnızca birkaç dakika içinde.  

## <a name="add-tables-and-objects"></a>Tablo ve nesne ekleme
  
### <a name="tooadd-new-tables-tooyour-model"></a>tooadd yeni tablolar tooyour modeli
  
1.  Tablo Modeli Gezgini’nde **Veri Kaynakları**’nı genişletin, ardından bağlantınıza sağ tıklayın > **Yeni Tabloları İçeri Aktar**’a tıklayın.
  
2.  Gezgin’de **DimEmployee** ve **FactResellerSales**’i seçip **Tamam**’a tıklayın.

3.  Sorgu Düzenleyicisi'nde **İçeri Aktar**’a tıklayın

4.  Merhaba aşağıdaki oluşturma [ilişkileri](../tutorials/aas-lesson-4-create-relationships.md):

    | Tablo 1           | Sütun       | Filtre Yönü   | Tablo 2     | Sütun      | Etkin |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | FactResellerSales | OrderDateKey | Varsayılan            | DimDate     | Tarih        | Evet    |
    | FactResellerSales | DueDate      | Varsayılan            | DimDate     | Tarih        | Hayır     |
    | FactResellerSales | ShipDateKey  | Varsayılan            | DimDate     | Tarih        | Hayır     |
    | FactResellerSales | ProductKey   | Varsayılan            | DimProduct  | ProductKey  | Evet    |
    | FactResellerSales | EmployeeKey  | tooBoth tabloları | DimEmployee | EmployeeKey | Evet    |

5. Merhaba, **DimEmployee** tablo, hello aşağıdaki oluşturma [hesaplanan sütunlar](../tutorials/aas-lesson-5-create-calculated-columns.md): 

    **Path** 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    **FullName** 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    **Level1** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    **Level2** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,2)) 
    ```

    **Level3** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,3)) 
    ```

    **Level4** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,4)) 
    ```

    **Level5** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,5)) 
    ```

6.  Merhaba, **DimEmployee** tablo, oluşturma bir [hiyerarşi](../tutorials/aas-lesson-9-create-hierarchies.md) adlı **kuruluş**. Sıralı sütunları aşağıdaki hello ekleyin: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.

7.  Merhaba, **FactResellerSales** tablo, hello aşağıdaki oluşturma [ölçü](../tutorials/aas-lesson-6-create-measures.md):

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  Kullanım [Excel'de çözümleme özelliği](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen Excel ve otomatik olarak bir PivotTable oluşturun.

9.  İçinde **PivotTable alanları**, hello eklemek **kuruluş** hello hiyerarşiden **DimEmployee** çok tablo**satırları**ve hello **ResellerTotalSales** hello ölçüyü **FactResellerSales** çok tablo**değerleri**.

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    Merhaba PivotTable görebileceğiniz gibi hello hiyerarşi düzensiz satırları gösterir. Boş üyelerin gösterildiği çok sayıda satır vardır.

## <a name="toofix-hello-ragged-hierarchy-by-setting-hello-hide-members-property"></a>Merhaba Gizle üyeleri özelliği ayarlanarak hiyerarşi toofix hello düzensiz

1.  **Tablo Modeli Gezgini**’nde **Tablolar** > **DimEmployee** > **Hiyerarşiler** > **Kuruluş**’u genişletin.

2.  **Özellikler** > **Üyeleri Gizle** menüsünden **Boş üyeleri gizle**’yi seçin. 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  Geri Excel'de PivotTable hello yenileyin. 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    Şimdi çok daha iyi görünüyor!

## <a name="see-also"></a>Ayrıca Bkz.   
[9. Ders: Hiyerarşi oluşturma](../tutorials/aas-lesson-9-create-hierarchies.md)  
[Ek Ders - Dinamik güvenlik](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[Ek Ders - Ayrıntı satırları](../tutorials/aas-supplemental-lesson-detail-rows.md)  