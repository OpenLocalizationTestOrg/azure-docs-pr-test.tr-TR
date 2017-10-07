---
Başlık: aaa "Azure Analysis Services öğretici Ders 4: ilişkiler oluşturmak | Microsoft Docs"Açıklama: Azure Analysis Services öğretici proje toocreate ilişkilerde nasıl hello açıklar. Hizmetleri: analysis services documentationcenter: '' Yazar: minewiskan Yöneticisi: erikre Düzenleyicisi: '' etiketler: ''

MS.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get-makalesi ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend
---
# <a name="lesson-4-create-relationships"></a>4. Ders: İlişki oluşturma

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Bu ders veri aktarıldığında, otomatik olarak oluşturulan hello ilişkilerini doğrulayın ve farklı tablolar arasında yeni ilişkiler ekleyin. Bir ilişki bu tablolardaki hello verileri nasıl bağıntılı kurar iki tablo arasında bir bağlantıdır. Örneğin, hello DimProduct tablo ve hello DimProductSubcategory tablo her ürünün tooa alt kategorisi ait hello olgu üzerinde tabanlı bir ilişki var. toolearn daha, fazla [ilişkileri](https://docs.microsoft.com/sql/analysis-services/tabular-models/relationships-ssas-tabular).
  
Bu ders zaman toocomplete tahmini: **10 dakika**  
  
## <a name="prerequisites"></a>Ön koşullar  
Bu konu, sırayla tamamlanması gereken bir tablo modelleme öğreticisinin bir parçasıdır. Bu ders Hello görevleri gerçekleştirmeden önce hello önceki Ders tamamlandı: [Ders 3: tarih tablosu olarak işaretle](../tutorials/aas-lesson-3-mark-as-date-table.md). 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>Mevcut ilişkileri gözden geçirme ve yeni ilişki ekleme  
Veri Al seçeneğini kullanarak tarafından veri içe aktarılırken hello AdventureWorksDW2014 veritabanından yedi tabloları aldı. Genellikle, ilişkisel bir kaynaktan verileri içe aktardığınızda, var olan ilişkileri hello veri ile birlikte otomatik olarak içe aktarılır. Bununla birlikte, kendi modelinizi yazmaya başlamadan önce tablolar arasındaki bu ilişkilerin düzgün oluşturulduğunu doğrulamanız gerekir. Bu öğretici için üç yeni ilişki eklersiniz.  
  
#### <a name="tooreview-existing-relationships"></a>tooreview var olan ilişkileri  
  
1.  Merhaba tıklatın **modeli** menü > **Model görünümü** > **diyagram görünümü**.  

    Merhaba modeli Tasarımcısı şimdi diyagram görünümünde, aralarında çizgili alınan tüm hello tabloları görüntüleme grafiksel bir biçimde görünür. tablolar arasında Hello çizgiler hello veri aktarıldığında, otomatik olarak oluşturulan hello ilişkileri gösterir.
    
    ![aas-lesson4-diagram](../tutorials/media/aas-lesson4-diagram.png)
  
    Merhaba tablolar olabildiğince çoğunu olarak hello modeli Tasarımcısı'nın sağ alt köşedeki hello Mini denetimlerini kullanarak içerir. Tıklayın ve tabloları toodifferent konumları, tablolar yakın araya getiren ya da belirli bir sırada koyma sürükleyin. Tabloları taşıma zaten hello tablolar arasında ilişkiler hello etkilemez. tooview belirli bir tablodaki tüm hello sütun tıklatın ve bir tablo kenar tooexpand üzerinde sürükleyin veya daha küçük olmasını.  
  
2.  Merhaba arasında Hello Kesiksiz çizgi **DimCustomer** tablo ve hello **DimGeography** tablo. Bu iki tablo arasında Hello düz satır, diğer bir deyişle, DAX formüller hesaplanırken, varsayılan olarak kullanılan bu ilişkiyi etkin olduğunu gösterir.  
  
    Bildirim hello **GeographyKey** hello sütununda **DimCustomer** tablo ve hello **GeographyKey** hello sütununda **DimGeography** tablo artık her ikisi de her bir kutu görüntülenir. Bu sütunlar hello ilişkisinde kullanılır. Merhaba ilişkinin özelliklerini şimdi da hello görünür **özellikleri** penceresi.  
  
    > [!TIP]  
    > Ayrıca toousing Merhaba modeli Tasarımcısı'nda diyagram görünümü, hello tablo biçiminde tüm tablolar arasındaki ilişkileri Yönet iletişim kutusu tooshow hello ilişkileri de kullanabilirsiniz. Tablosal Model Gezgini’nde **İlişkiler** > **İlişkileri Yönet**’e sağ tıklayın.
  
3.  İlişkileri aşağıdaki hello ne zaman oluşturulduğu doğrulayın hello tabloların her birinin hello AdventureWorksDW veritabanından aktarılmadı:  
  
    |Etkin|Tablo|İlişkili Arama Tablosu|  
    |----------|---------|------------------------|  
    |Evet|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |Evet|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |Evet|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |Evet|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |Evet|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    Merhaba eksik olan, modelinizi tabloları aşağıdaki hello içerdiğini doğrulayın: DimCustomer, DimDate'i, DimGeography, DimProduct, DimProductCategory, DimProductSubcategory ve Factınternetsales. Aynı veri kaynağı bağlantısı sırasında içeri aktarılan hello tablolardan kez ayırmak, bu tablolar arasındaki ilişkileri olması oluşturulmaz ve el ile oluşturulması gerekir.  

### <a name="take-a-closer-look"></a>Daha yakından bakın
Diyagram Görünümü'nde bir ok, yıldız işareti ve tablolar arasında ilişki hello Göster hello satır sayısına dikkat edin.

![aas-lesson4-line](../tutorials/media/aas-lesson4-line.png)

Merhaba ok hello filtre yönünü gösterir. Merhaba yıldız bu tabloda çok tarafında hello ilişkinin nicelik hello ve hello biri bu tablo hello ilişkisinin bir tarafı hello gösterilir gösterilir. Bir ilişki tooedit gerekirse; Örneğin, hello ilişkinin filtre yönünü veya önem düzeyi değiştirmek, hello ilişkisi satır tooopen hello ilişki Düzenle iletişim kutusu çift tıklayın.

![aas-lesson4-edit](../tutorials/media/aas-lesson4-edit.png)

Bu özellikleri için Gelişmiş Veri modelleme yöneliktir ve bu öğreticinin dış hello kapsamı. toolearn daha, fazla [çift yönlü çapraz Analysis Services tablolu modeller için filtreleri](https://docs.microsoft.com/sql/analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services).

Bazı durumlarda, belirli bir iş mantığı, model toosupport tablolar arasında ek ilişkiler toocreate gerekebilir. Bu öğretici için toocreate üç ek ilişkiler hello Factınternetsales tablosunda hello DimDate'i tablo arasındaki gerekir.  
  
#### <a name="tooadd-new-relationships-between-tables"></a>tablolar arasında tooadd yeni ilişkiler  
  
1.  Merhaba, hello modeli Tasarımcısı'nda **Factınternetsales** tablo,'ı tıklatın ve üzerinde hello tutun **OrderDate** sütun sonra sürükleme hello imleç toohello **tarih** hello sütununda **DimDate'i** tablo ve bırakın.  

    Merhaba arasında etkin bir ilişki oluşturduğunuz gösteren bir kesintisiz çizgiye görünür **OrderDate** hello sütununda **Internet satış** tablo ve hello **tarih** hello sütununda **Tarih** tablo. 
  
      ![aas-lesson4-new](../tutorials/media/aas-lesson4-new.png) 
  
    > [!NOTE]  
    > İlişkiler oluşturma, hello önem düzeyi ve filtre yönünü hello birincil tablosu ile Merhaba ilişkili arama tablosu arasında otomatik olarak seçilir.  
  
2.  Merhaba, **Factınternetsales** tablo,'ı tıklatın ve üzerinde hello tutun **vade tarihi** sütun sonra sürükleme hello imleç toohello **tarih** hello sütununda **DimDate'i** tablo ve bırakın.  
  
    Merhaba arasında etkin bir ilişki oluşturduğunuz gösteren bir noktalı çizgi görünür **vade tarihi** hello sütununda **Factınternetsales** tablo ve hello **tarih** sütununda Merhaba **DimDate'i** tablo. Tablolar arasında birden çok ilişki oluşturabilirsiniz, ancak aynı anda yalnızca bir ilişki etkin olabilir. Etkin olmayan ilişkiler etkin tooperform özel toplamalar özel DAX ifadelerinde yapılabilir.  
  
3.  Son olarak bir tane daha ilişki oluşturun. Merhaba, **Factınternetsales** tablo,'ı tıklatın ve üzerinde hello tutun **SevkTarihi** sütun sonra sürükleme hello imleç toohello **tarih** hello sütununda **DimDate'i** tablo ve bırakın.  
    
     ![aas-lesson4-newinactive](../tutorials/media/aas-lesson4-newinactive.png)
  
## <a name="whats-next"></a>Sırada ne var?
[5. Ders: Hesaplanan sütun oluşturma](../tutorials/aas-lesson-5-create-calculated-columns.md).
  
  
  
