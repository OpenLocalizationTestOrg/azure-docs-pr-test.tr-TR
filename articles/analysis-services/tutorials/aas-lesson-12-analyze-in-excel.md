---
Başlık: aaa "Azure Analysis Services öğretici Ders 12: Excel'de çözümleme | Microsoft Docs"Açıklama: nasıl toouse Excel'de çözümleme özelliği hello içinde Azure Analysis Services açıklar öğretici projesi. Hizmetleri: analysis services documentationcenter: '' Yazar: minewiskan Yöneticisi: erikre Düzenleyicisi: '' etiketler: ''

MS.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get-makalesi ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend
---
# <a name="lesson-12-analyze-in-excel"></a>12. Ders: Excel’de çözümleme

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Bu ders içinde kullanmak Çözümle hello Excel özelliği tooopen Microsoft Excel, otomatik olarak bir bağlantı toohello modeli çalışma alanı oluşturun ve bir PivotTable toohello çalışma otomatik olarak ekleyin. Excel özelliği Hello Çözümle tooprovide yöneliktir hızlı ve kolay bir yol tootest hello sürecinin modelinizin modelinizi önceki toodeploying tasarlayın. Bu derste herhangi bir veri çözümlemesi yapmayacaksınız. Bu ders Hello amacı toofamiliarize, hello modeli yazar, hello araçlarıyla model tasarımınızı tootest kullanabilirsiniz.   
  
Merhaba üzerinde bu ders Excel yüklü toocomplete SSDT ile aynı bilgisayara.
  
Bu ders zaman toocomplete tahmini: **beş dakika**  
  
## <a name="prerequisites"></a>Ön koşullar  
Bu konu, sırayla tamamlanması gereken bir tablo modelleme öğreticisinin bir parçasıdır. Bu ders Hello görevleri gerçekleştirmeden önce hello önceki Ders tamamlandı: [Ders 11: roller oluşturma](../tutorials/aas-lesson-11-create-roles.md).  
  
## <a name="browse-using-hello-default-and-internet-sales-perspectives"></a>Merhaba varsayılan ve Internet satış Perspektifler kullanarak Gözat  
Bu ilk görevleri modeliniz tüm model nesneleri içeren iki hello varsayılan perspektif kullanarak ve ayrıca hello Internet satış perspektifini kullanarak göz, daha önce. Merhaba Internet satış perspektif hello müşteri tablo nesnesi dışlar.  
  
#### <a name="toobrowse-by-using-hello-default-perspective"></a>Merhaba varsayılan perspektif kullanarak toobrowse  
  
1.  Merhaba tıklatın **modeli** menü > **Excel'de çözümleme özelliği**.  
  
2.  Merhaba, **Excel'de çözümleme özelliği** iletişim kutusu, tıklatın **Tamam**.  
  
    Excel yeni bir çalışma kitabı ile açılır. Merhaba geçerli kullanıcı hesabı kullanarak bir veri kaynağı bağlantısı oluşturulduğunu ve hello varsayılan perspektif kullanılan toodefine görüntülenebilir alanları. Bir PivotTable toohello çalışma otomatik olarak eklenir.  
  
3.  Excel'de, hello **PivotTable alan Listesi'ni**, bildirim hello **DimDate'i** ve **Factınternetsales** ölçü grupları görünür. Merhaba **DimCustomer**, **DimDate'i**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, ve **Factınternetsales** tabloların kendi ilgili sütunları da görünür.  
  
4.  Excel hello çalışma kitabını kaydetmeden kapatın.  
  
#### <a name="toobrowse-by-using-hello-internet-sales-perspective"></a>Merhaba Internet satış perspektifini kullanarak toobrowse  
  
1.  Merhaba tıklatın **modeli** menüsüne ve ardından **Excel'de çözümleme özelliği**.  
  
2.  Merhaba, **Excel'de çözümleme özelliği** iletişim kutusu, bırakın **geçerli Windows kullanıcısı** sonra hello seçili **perspektif** aşağı açılan liste kutusunu seçin **Internet satış** ve ardından **Tamam**. 
    
    ![aas-lesson12-perspective](../tutorials/media/aas-lesson12-perspective.png)
    
3.  Excel'de içinde **PivotTable alanları**, hello DimCustomer tablo hello alan listesinden hariç dikkat edin.  
    
    ![aas-lesson12-fields](../tutorials/media/aas-lesson12-fields.png)
    
4.  Excel hello çalışma kitabını kaydetmeden kapatın.  
  
## <a name="browse-by-using-roles"></a>Rolleri kullanarak göz atma  
Roller herhangi bir tablo modelinin önemli bir parçasıdır. En az bir rol olmadan toowhich kullanıcıların üye olarak ekleneceği, kullanıcılar erişim ve modelinizi kullanarak verileri analiz. Excel özelliği Hello Çözümle bir yol sizin için tanımladığınız tootest hello rolleri sağlar.  
  
#### <a name="toobrowse-by-using-hello-sales-manager-user-role"></a>Merhaba satış yöneticisi kullanıcı rolü kullanarak toobrowse  
  
1.  Merhaba SSDT içinde tıklatın **modeli** menüsüne ve ardından **Excel'de çözümleme özelliği**.  
  
2.  İçinde **belirt hello kullanıcı adını veya rolü toouse tooconnect toohello modeli**seçin **rol**seçip hello aşağı açılan liste kutusunda **Satış Yöneticisi**ve 'ıtıklatın **Tamam**.  
  
    Excel yeni bir çalışma kitabı ile açılır. Bir PivotTable otomatik olarak oluşturulur. Merhaba Özet Tablo alan listesi yeni modelinizde kullanılabilir tüm hello veri alanları içerir.  
      
3.  Excel hello çalışma kitabını kaydetmeden kapatın.  
  
## <a name="whats-next"></a>Sırada ne var?
Git toohello sonraki Ders: [Ders 13: dağıtmak](../tutorials/aas-lesson-13-deploy.md).

  
  
  
