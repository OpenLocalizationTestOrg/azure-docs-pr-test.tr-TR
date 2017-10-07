---
Başlık: aaa "Azure Analysis Services öğretici Ders 2: veri alma | Microsoft Docs"Açıklama: Azure Analysis Services öğretici proje tooget ve içeri aktarma verileri nasıl hello açıklar. Hizmetleri: analysis services documentationcenter: '' Yazar: minewiskan Yöneticisi: erikre Düzenleyicisi: '' etiketler: ''

MS.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get-makalesi ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend
---

# <a name="lesson-2-get-data"></a>2. Ders: Verileri alma

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Bu ders SSDT tooconnect toohello AdventureWorksDW2014 örnek veritabanı, verileri seçin, Önizleme ve filtre Veri Al kullanın ve sonra model çalışma alanınıza alın.  
  
Verileri Al’ı kullanarak birçok farklı kaynaktaki verileri içeri aktarabilirsiniz: Azure SQL Veritabanı, Oracle, Sybase, OData Feed, Teradata, dosyalar ve daha fazlası. Veriler bir Power Query M formül ifadesi kullanılarak da sorgulanabilir.
  
Bu ders zaman toocomplete tahmini: **10 dakika**  
  
## <a name="prerequisites"></a>Ön koşullar  
Bu konu, sırayla tamamlanması gereken bir tablo modelleme öğreticisinin bir parçasıdır. Bu ders Hello görevleri gerçekleştirmeden önce hello önceki Ders tamamlandı: [Ders 1: yeni bir tablo modeli projesi oluşturmak](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="create-a-connection"></a>Bağlantı oluşturma  
  
#### <a name="toocreate-a-connection-toohello-adventureworksdw2014-database"></a>toocreate bağlantı toohello AdventureWorksDW2014 veritabanı  
  
1.  Tablosal Model Gezgini'nde **Veri Kaynakları** > **Veri Kaynağından İçeri Aktar**’a sağ tıklayın.  
  
    Üzerinden bağlanan tooa veri kaynağına kılavuzları alma veri başlatır. İçinde tablolu Model Gezgini görmüyorsanız, **Çözüm Gezgini**, çift **Model.bim** tooopen hello modeli hello Tasarımcısı'nda. 
    
    ![aas-lesson2-getdata](../tutorials/media/aas-lesson2-getdata.png)
  
2.  Verileri Al’da **Veritabanı** > **SQL Server Veritabanı** > **Bağlan**’a tıklayın.  
  
3.  Merhaba, **SQL Server veritabanı** iletişim, **Server**hello hello AdventureWorksDW2014 veritabanının yüklendiği hello sunucunun adını yazın ve ardından **Bağlan**.  

4.  İstendiğinde tooenter kimlik bilgileri, Analysis Services veri alırken ve verileri işlerken tooconnect toohello veri kaynağını kullanan toospecify hello kimlik bilgileri gerekir. **Kimliğe Bürünme Modu**’nda **Hesap Kimliğine Bürün**’ü seçip kimlik bilgilerini girin ve **Bağlan**’a tıklayın. Burada hello parola kullanım süresi sona ermiyor bir hesabı kullanmanız önerilir.

    ![aas-lesson2-account](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > Bir Windows kullanıcı hesabı ve parola kullanarak bağlanan tooa veri kaynağının hello en güvenli yöntemi sağlar.
  
5.  Merhaba Gezgini içinde seçin **AdventureWorksDW2014** veritabanı ve ardından **Tamam**. Merhaba bağlantı toohello veritabanı oluşturur. 
  
6.  Gezgini içinde tabloları aşağıdaki hello için onay kutusunu seçin hello: **DimCustomer**, **DimDate'i**, **DimGeography**, **DimProduct**,  **DimProductCategory**, **DimProductSubcategory**, ve **Factınternetsales**.  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
Tamam'a tıkladığınızda Sorgu Düzenleyicisi açılır. Merhaba sonraki bölümde, yalnızca tooimport istediğiniz hello verileri seçin.

  
## <a name="filter-hello-table-data"></a>Merhaba tablo verileri filtreleme  
Merhaba AdventureWorksDW2014 örnek veritabanındaki tablolarda modelinizde gerekli tooinclude olmayan veri içeriyor. Mümkün olduğunda, gereksiz verileri toosave bellek içi alanı hello modeli tarafından kullanılan çıkış toofilter istiyor. Bunu dağıtıldıktan sonra hello çalışma alanı veritabanı veya hello model veritabanı alındıktan olmayan bazı tablodan hello sütun filtre. 
  
#### <a name="toofilter-hello-table-data-before-importing"></a>içe aktarmadan önce toofilter hello tablo verileri  
  
1.  Sorgu Düzenleyicisi'nde hello seçin **DimCustomer** tablo. Bir görünümü hello veri kaynağı (AdventureWorksDWQ2014 örnek veritabanınızdaki) hello DimCustomer tablosunda yer alır. 
  
2.  Çoklu seçimi (Ctrl+tıklama) kullanarak **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**’ı seçin, sağ tıklayın ve **Sütunları Kaldır**’a tıklayın. 

    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-columns.png)
  
    Bu sütunlar için Hello değerleri değil ilgili tooInternet Satış Analiz olduğundan, bu sütunları yok gerek tooimport yoktur. Gereksiz sütunların dışarıda bırakılması, modelinizin daha küçük ve daha verimli olmasını sağlar.  
  
4.  Her tablodaki sütunlar aşağıdaki hello kaldırarak tabloları kalan hello filtreleyin:  
    
    **DimDate**
    
      |Sütun|  
      |--------|  
      |DateKey|  
      |**SpanishDayNameOfWeek**|  
      |**FrenchDayNameOfWeek**|  
      |**SpanishMonthName**|  
      |**FrenchMonthName**|  
  
    **DimGeography**
  
      |Sütun|  
      |-------------|  
      |**SpanishCountryRegionName**|  
      |**FrenchCountryRegionName**|  
      |**IpAddressLocator**|  
  
    **DimProduct**
  
      |Sütun|  
      |-----------|  
      |**SpanishProductName**|  
      |**FrenchProductName**|  
      |**FrenchDescription**|  
      |**ChineseDescription**|  
      |**ArabicDescription**|  
      |**HebrewDescription**|  
      |**ThaiDescription**|  
      |**GermanDescription**|  
      |**JapaneseDescription**|  
      |**TurkishDescription**|  
  
    **DimProductCategory**
  
      |Sütun|  
      |--------------------|  
      |**SpanishProductCategoryName**|  
      |**FrenchProductCategoryName**|  
  
    **DimProductSubcategory**
  
      |Sütun|  
      |-----------------------|  
      |**SpanishProductSubcategoryName**|  
      |**FrenchProductSubcategoryName**|  
  
    **FactInternetSales**
  
      |Sütun|  
      |------------------|  
      |**OrderDateKey**|  
      |**DueDateKey**|  
      |**ShipDateKey**|   
  
## <a name="Import"></a>Seçili hello tablo ve sütun veri alın  
Önizlemesi ve gereksiz verileri filtre göre hello kalan istediğiniz hello verileri içeri aktarabilirsiniz. Merhaba sihirbaz tablolar arasındaki ilişkileri birlikte hello tablo verileri alır. Yeni tablolar ve sütunlar hello modelinde oluşturulur ve filtre çıkışı verileri değil olması alınır.  
  
#### <a name="tooimport-hello-selected-tables-and-column-data"></a>Tablo ve sütun veri tooimport hello seçili  
  
1.  Seçimlerinizi gözden geçirin. Her şey yolundaysa **İçeri Aktar**’a tıklayın. Merhaba veri işleme iletişim, veri kaynağını çalışma veritabanınıza içeri aktarılan veriler hello durumunu gösterir.
  
    ![aas-lesson2-success](../tutorials/media/aas-lesson2-success.png) 
  
2.  **Kapat**’a tıklayın.  

  
## <a name="save-your-model-project"></a>Model projenizi kaydetme  
Toofrequently Kaydet modeli projenizi önemlidir.  
  
#### <a name="toosave-hello-model-project"></a>toosave hello modeli projesi  
  
-   **Dosya** > **Tümünü Kaydet**’e tıklayın.  
  
## <a name="whats-next"></a>Sırada ne var?
[3. Ders: Tarih Tablosu Olarak İşaretleme](../tutorials/aas-lesson-3-mark-as-date-table.md).

  
  
