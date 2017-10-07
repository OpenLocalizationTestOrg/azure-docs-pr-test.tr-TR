---
Başlık: aaa "Azure Analysis Services öğretici Ders 1: yeni bir tablo modeli projesi oluşturun | Microsoft Docs"Açıklama: nasıl toocreate yeni bir Azure Analysis Services açıklar öğretici projesi. Hizmetleri: analysis services documentationcenter: '' Yazar: minewiskan Yöneticisi: erikre Düzenleyicisi: '' etiketler: ''

MS.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get-makalesi ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend
---
# <a name="lesson-1-create-a-tabular-model-project"></a>1. Ders: Tablosal model projesi oluşturma

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Bu ders, SQL Server veri Araçları (SSDT) toocreate yeni bir tablo modeli projesi hello 1400 uyumluluk düzeyinde kullanın. Yeni projeniz oluşturulduktan sonra, veri eklemeye ve modelinizi yazmaya başlayabilirsiniz. Bu ders de SSDT ortamında yazma kısa giriş toohello tablo modeli sunar.  
  
Bu ders zaman toocomplete tahmini: **10 dakika**  
  
## <a name="prerequisites"></a>Ön koşullar  
Bu konu, öğretici geliştirme sekmeli modelde hello ilk Ders ilgilidir. toocomplete bu ders, yerinde toohave gereken birkaç önkoşul vardır. toolearn daha, fazla [Azure Analysis Services - Adventure Works Öğreticisi](../tutorials/aas-adventure-works-tutorial.md).  
  
## <a name="create-a-new-tabular-model-project"></a>Yeni tablosal model projesi oluşturma  
  
#### <a name="toocreate-a-new-tabular-model-project"></a>toocreate yeni bir tablo modeli projesi  
  
1.  Merhaba üzerinde ssdt'de **dosya** menüsünde tıklatın **yeni** > **proje**.  
  
2.  Merhaba, **yeni proje** iletişim kutusunda, genişletin **yüklü** > **iş zekası** > **Analysis Services**ve ardından **Analysis Services tablolu proje**.  
  
3.  İçinde **adı**, türü **AW Internet satış**ve ardından hello proje dosyaları için konum belirtin.  
  
    Varsayılan olarak, **çözüm adı** olan hello aynı hello proje adı olarak; ancak, farklı çözüm adı yazabilirsiniz.  
  
4.  **Tamam** düğmesine tıklayın.  
  
5.  Merhaba, **Tabular modeli Tasarımcısı** iletişim kutusunda **tümleşik çalışma**.  
  
    Merhaba çalışma hello modeli geliştirme sırasında başlangıç projesi olarak aynı ad ile tablo modelli bir veritabanı barındırır. Tümleşik çalışma hello gerek tooinstall modeli geliştirme için ayrı bir Analysis Services sunucu örneği ortadan SSDT yerleşik bir örnek kullanan anlamına gelir.
      
6.  **Uyumluluk düzeyi**’nde **SQL Server 2017 / Azure Analysis Services (1400)** seçeneğini belirleyin.   
 
    ![aas-lesson1-tmd](../tutorials/media/aas-lesson1-tmd.png)
      
    SQL Server 2017 / Azure Analysis Services (1400) hello uyumluluk düzeyi liste kutusunda görmüyorsanız, SQL Server veri araçları hello en son sürümünü kullandığınızdan değil. tooget hello en son sürümü, bkz: [yükleme SQL Server veri Araçları](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).  
      
  
## <a name="understanding-hello-ssdt-tabular-model-authoring-environment"></a>Merhaba SSDT tablo modeli geliştirme ortamı anlama  
Yeni bir tablo modeli projesi oluşturduğunuza göre geliştirme ortamı ssdt'de şu anda tooexplore hello tablolu model atalım.  
  
Projeniz oluşturulduktan sonra SSDT’de açılır. Merhaba içinde sağ kenar çubuğunda **tablolu Model Gezgini**, modelinizi hello nesnelerin bir ağaç görünümünü bakın. Veri aldığınız henüz yapmadıysanız bu yana hello klasörleri boş. Nesneyi sağ klasör tooperform eylemleri, benzer toohello menü çubuğu. Bu öğreticide adım olarak, modeli projenizde hello tablolu Model Gezgini toonavigate farklı nesneleri kullanın.

![aas-lesson1-tme](../tutorials/media/aas-lesson1-tme.png)

Merhaba tıklatın **Çözüm Gezgini** sekmesi. Burada **Model.bim** dosyanızı görürsünüz. İçinde hello designer penceresi toohello sol (Merhaba boş penceresinde hello Model.bim sekmesi) görmüyorsanız, **Çözüm Gezgini**altında **AW Internet satış proje**, hello çift  **Model.bim** dosya. Merhaba Model.bim dosyası modeli projeniz için hello meta verileri içerir. 

![aas-lesson1-se](../tutorials/media/aas-lesson1-se.png)
  
**Model.bim** öğesine tıklayın. Merhaba, **özellikleri** penceresinde hello model özellikleri, hello olduğu en önemli bkz **DirectQuery modu** özelliği. Bu özellik hello modeli bellek içi modunda (Kapalı) veya DirectQuery modunu (açık) dağıtılırsa belirtir. Bu öğretici için modelinizi Bellek İçi modunda yazar ve dağıtırsınız.

![aas-lesson1-properties](../tutorials/media/aas-lesson1-properties.png)
  
Bir modeli projesi oluşturduğunuzda belirli model özelliklerini toohello hello belirtilen veri modelleme ayarları otomatik olarak göre ayarlanır **Araçları** menü > **seçenekleri** iletişim kutusu. Veri yedekleme, çalışma alanı bekletme ve çalışma alanı sunucusu özellikleri nasıl ve nerede hello çalışma alanı veritabanı (veritabanı yazma, model) yedeklendiğinden, bellek içi korunur ve yerleşik belirtin. Gerekirse bu ayarları daha sonra değiştirebilirsiniz, ancak şimdilik bu özellikleri olduğu gibi bırakın.  

**Çözüm Gezgini**’nde **AW İnternet Satışları**’na (proje) sağ tıklayıp **Özellikler**’e tıklayın. Merhaba **AW Internet satış özellik sayfaları** iletişim kutusu görüntülenir. Bu özelliklerden bazılarını, daha sonra modelinizi dağıtırken ayarlarsınız.  
  
SSDT yüklendiğinde birkaç yeni menü öğeleri toohello Visual Studio ortamı eklendi. Merhaba tıklatın **modeli** menüsü. Buradan, veri almak, çalışma veri yenileme, Excel modelinizde göz atın, perspektifler ve rolleri, select hello model görünümü, oluşturabilir ve hesaplama seçeneklerini ayarlayın. Merhaba tıklatın **tablo** menüsü. Buradan ilişkiler oluşturup bunları yönetebilir, tarih tablosu ayarlarını belirtebilir, bölümler oluşturabilir ve tablo özelliklerini düzenleyebilirsiniz. Merhaba tıklatırsanız **sütun** menüsünde ekleyin ve bir tablodaki sütun silmek, sütunları dondurma ve sıralama düzeni belirtin. SSDT ayrıca bazı düğmeleri toohello çubuğu ekler. Merhaba otomatik toplam özelliğini toocreate standart toplama ölçü seçili sütun için kullanışlıdır. Hızlı erişim toofrequently özellikler ve komutlar kullanılan diğer araç çubuğu düğmeleri sağlar.  
  
Bazı hello iletişim kutuları ve çeşitli özellikleri belirli tooauthoring tablolu modeller için konumları keşfedin. Bazı öğeler henüz etkin değil olsa da, geliştirme ortamı hello tablo modeli için iyi bir fikir alabilirsiniz.  
  

## <a name="whats-next"></a>Sırada ne var?
[2. Ders: Verileri alma](../tutorials/aas-lesson-2-get-data.md).

  
  
  
