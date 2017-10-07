---
Başlık: aaa "Azure Analysis Services öğretici Ders 10: bölümleri oluşturma | Microsoft Docs"Açıklama: toocreate hello Azure Analysis Services öğretici projesinde nasıl bölümler açıklar. Hizmetleri: analysis services documentationcenter: '' Yazar: minewiskan Yöneticisi: erikre Düzenleyicisi: '' etiketler: ''

MS.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get-makalesi ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend
---
# <a name="lesson-10-create-partitions"></a>10. Ders: Bölüm oluşturma

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Bu ders, işlenen (yenilendi) bağımsız olarak diğer bölümler olabilecek daha küçük mantıksal parçalara bölümleri toodivide hello Factınternetsales tablosunda oluşturun. Varsayılan olarak, tüm Merhaba tablonun sütunları ve satırları içeren bir bölüm, modele dahil her tablo sahiptir. Merhaba Factınternetsales tablosunda için yıla göre toodivide hello veri istiyoruz; bir bölüm her Merhaba tablonun beş yıl. Daha sonra her bölüm bağımsız olarak işlenebilir. toolearn daha, fazla [bölümleri](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular). 
  
Bu ders zaman toocomplete tahmini: **15 dakika**  
  
## <a name="prerequisites"></a>Ön koşullar  
Bu konu, sırayla tamamlanması gereken bir tablo modelleme öğreticisinin bir parçasıdır. Bu ders Hello görevleri gerçekleştirmeden önce hello önceki Ders tamamlandı: [Ders 9: hiyerarşileri oluşturma](../tutorials/aas-lesson-9-create-hierarchies.md).  
  
## <a name="create-partitions"></a>Bölüm oluşturma  
  
#### <a name="toocreate-partitions-in-hello-factinternetsales-table"></a>Merhaba Factınternetsales tablosunda toocreate bölümleri  
  
1.  Tablosal Model Gezgini’nde **Tablolar**’ı genişletin ve **FactInternetSales** > **Bölümler**’e sağ tıklayın.  
  
2.  Bölüm Yöneticisi'nde **kopya**ve hello adını çok değiştirin**FactInternetSales2010**.
  
    Merhaba yıl 2010'da, belirli bir dönem içinde yalnızca bu satırları hello bölüm tooinclude istediğiniz çünkü hello sorgu ifadesi değiştirmeniz gerekir.
  
4.  Tıklatın **tasarım** tooopen sorgu Düzenleyicisi'ni ve hello ardından **FactInternetSales2010** sorgu.

5.  Önizlemede hello aşağı hello tıklatın **OrderDate** sütun başlığını ve ardından **tarih filtreleri** > **arasında**.

    ![aas-lesson10-query-editor](../tutorials/media/aas-lesson10-query-editor.png)

6.  Hello filtre satırları iletişim kutusunda, **satırları göster: OrderDate**, bırakın **sonra veya eşittir**ve başlangıç tarihi alanına enter **1/1/2010**. Hello bırakın **ve** seçili işleci seçip **önce**, başlangıç tarihi alanına enter **1/1/2011**ve ardından **Tamam**.

    ![aas-lesson10-filter-rows](../tutorials/media/aas-lesson10-filter-rows.png)
    
    Sorgu Düzenleyicisi’ndeki UYGULANAN ADIMLAR’da Filtrelenen Satırlar adlı başka bir adım göründüğüne dikkat edin. Tooselect yalnızca sipariş tarihleri 2010'dan filtredir.

8.  **İçeri Aktar**’a tıklayın.

    Bölüm Yöneticisi'nde hello sorgu ifade artık ek bir satır filtre yan tümcesi içeriyorsa dikkat edin.

    ![aas-lesson10-query](../tutorials/media/aas-lesson10-query.png)
  
    Bu bölüm yalnızca hello veri hello OrderDate 2010 takvim yılı hello filtrelenmiş Satırları yan tümcesinde belirtilen hello olduğu bu satırı içermelidir bu bildirimi belirtir.  
  
  
#### <a name="toocreate-a-partition-for-hello-2011-year"></a>toocreate hello 2011 yıl için bir bölüm  
  
1.  Merhaba bölümleri listesinde hello tıklayın **FactInternetSales2010** bölüm oluşturduğunuz ve ardından **kopya**.  Merhaba bölüm adı çok değiştirme**FactInternetSales2011**. 

    Sorgu Düzenleyici toocreate yeni bir filtre uygulanmış Satırları yan tümcesi toouse gerekmez. Merhaba sorgu kopyasını 2010 için oluşturulduğundan toodo gereken tek şey hafif hello sorguda 2011 için değişiklik.
  
2.  İçinde **sorgu ifadesi**için bu bölümü tooinclude yalnızca hello için satırları 2011 yıl sıralı, hello satırları filtre yan tümcesi ile Merhaba yıllarda değiştirin, **2011** ve **2012**, sırasıyla gibi:  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="toocreate-partitions-for-2012-2013-and-2014"></a>2012, 2013 ve 2014 için toocreate bölüm.  
  
- 2012, 2013 ve bu yıl hello yıl hello satırları filtre yan tümcesi tooinclude yalnızca satır içinde değiştirme 2014 bölümleri oluşturma hello önceki adımları izleyin. 
  

## <a name="delete-hello-factinternetsales-partition"></a>Merhaba Factınternetsales bölümü silin
Her yıl bölümleri sahip olduğunuza göre hello Factınternetsales bölüm silebilirsiniz; Çakışma işlem tüm bölümleri işlerken seçerken engelliyor.

#### <a name="toodelete-hello-factinternetsales-partition"></a>toodelete hello Factınternetsales bölümü
-  Merhaba Factınternetsales bölüme tıklayın ve ardından **silmek**.



## <a name="process-partitions"></a>İşlem bölümleri  
Bölüm Yöneticisi'nde hello fark **son işlenen** sütun her hello yeni bölümler, oluşturduğunuz bu bölümler hiçbir zaman işlenen gösterir. Bölümler oluştururken, o bölümler bir işlem bölümleri veya işlem tablo işlemi toorefresh hello verileri çalıştırmanız gerekir.  
  
#### <a name="tooprocess-hello-factinternetsales-partitions"></a>tooprocess hello Factınternetsales bölümleri  
  
1.  Tıklatın **Tamam** tooclose Bölüm Yöneticisi.  
  
2.  Hello'ı tıklatın **Factınternetsales** tablo ve ardından hello **modeli** menü > **işlem** > **işlem bölümleri**.  
  
3.  Merhaba işlem bölümleri iletişim kutusunda doğrulayın **modu** çok ayarlanır**işlem varsayılan**.  
  
4.  Hello Hello onay kutusunu seçin **işlem** her hello beş sütun bölümler oluşturduğunuz ve ardından **Tamam**.  

    ![aas-lesson10-process-partitions](../tutorials/media/aas-lesson10-process-partitions.png)
  
    Kimliğe bürünme kimlik bilgilerini istenirse hello Windows kullanıcı adı ve parola Ders 2'de belirtilen girin.  
  
    Merhaba **veri işleme** iletişim kutusu belirir ve her bölüm için işlem ayrıntılarını görüntüler. Her bölüm için farklı sayıda satır aktarıldığına dikkat edin. Her bölüm yalnızca bu satırları hello hello SQL deyimi WHERE yan tümcesinde belirtilen hello yıl içerir. İşlem tamamlandığında, bir tane hello veri işleme iletişim kutusunu kapatın.  
  
    ![aas-lesson10-process-complete](../tutorials/media/aas-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a>Sırada ne var?
Git toohello sonraki Ders: [Ders 11: roller oluşturmak](../tutorials/aas-lesson-11-create-roles.md). 
