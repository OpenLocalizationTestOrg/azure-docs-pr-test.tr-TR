---
Başlık: aaa "öğretici: hello Portalı'nda ilk Azure Search dizininizi oluşturma | Microsoft Docs"Açıklama: hello Azure portalı, önceden tanımlanmış kullanma örnek veri toogenerate bir dizin. Tam metin arama, filtreler, modeller, belirsiz arama, coğrafi arama ve daha fazlasını keşfedin.
Hizmetleri: documentationcenter arama: '' Yazar: HeidiSteen Yöneticisi: jhubbard Düzenleyicisi: '' etiketler: azure portal

MS.assetid: 21adc351-69bb-4a39-bc59-598c60c8f958 ms.service: ms.devlang arama: na ms.workload: ms.topic arama: hero-article ms.tgt_pltfrm: na ms.date: 06/26/2017 ms.author: heidist

---
# <a name="tutorial-create-your-first-azure-search-index-in-hello-portal"></a>Öğretici: hello Portalı'nda ilk Azure Search dizininizi oluşturma

Hello Azure portalı, önceden tanımlanmış örnek veri kümesi tooquickly Başlarken oluşturmak hello kullanarak dizini **veri içeri aktarma** Sihirbazı. **Search Gezgini** ile tam metin arama, filtreler, modeller, belirsiz arama ve coğrafi aramayı keşfedin.  

Bu kodsuz giriş yazısı, hemen ilginç sorgular yazmaya başlayabilmeniz için önceden tanımlanmış verileri kullanmaya başlamanızı sağlar. Portal araçları kodun yerini alamayacak olsa da aşağıdaki görevler için kullanışlıdır:

+ Olabildiğince az artışla uygulamalı eğitim
+ **Verileri içeri aktarma**’da kod yazmadan önce bir dizin prototipi oluşturma
+ **Search gezgini**’nde test sorguları ve ayrıştırıcı söz dizimi
+ Varolan bir görünüm yayımlanan tooyour hizmeti dizin ve özniteliklerini arayın

**Tahmini Süre:** Yaklaşık 15 dakika sürer, ancak hesap veya hizmete kaydolunması da gerekiyorsa daha uzun sürebilir. 

Alternatif olarak, artırmalarını kullanarak bir [kod tabanlı giriş tooprogramming Azure Search .NET ile](search-howto-dotnet-sdk.md).

## <a name="prerequisites"></a>Ön koşullar

Bu öğretici, bir [Azure aboneliği](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ve [Azure Search hizmeti](search-create-service-portal.md) kullanıldığını varsayar. 

Bir hizmet tooprovision hemen istemiyorsanız, hello 6 dakika Tanıtımı adımları Bu öğreticide, yaklaşık üç dakika olarak bu başlangıç izleyebilir [Azure arama genel bakış videosu](https://channel9.msdn.com/Events/Connect/2016/138).

## <a name="find-your-service"></a>Hizmetinizi bulma
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Hello Azure Search hizmetinizin hizmet panosunu açın. Hello hizmet döşeme tooyour Panosu sabitlerseniz alamadık, böylece hizmetinizi bulabilirsiniz: 
   
   * Hello harf çubuğu, tıklatın **daha fazla hizmet** hello altındaki hello sol gezinti bölmesi.
   * Merhaba arama kutusuna yazın *arama* tooget Hizmetleri, aboneliğiniz için bir arama listesi. Hizmetinizi hello listesinde görünmesi gerekir. 

## <a name="check-for-space"></a>Alan denetleme
Birçok müşteri hello ücretsiz hizmetle başlar. Bu, sınırlı toothree dizinleri, üç veri kaynağı ve üç dizin oluşturucu sürümüdür. Başlamadan önce ek öğeler için yeriniz olduğundan emin olun. Bu öğreticide her nesneden birer tane oluşturulur. 

> [!TIP] 
> Merhaba hizmet panosunu döşeme kaç dizinler, dizin oluşturucular ve veri kaynaklarını zaten gösterir. Merhaba dizin oluşturucu Döşe başarı ve başarısızlık göstergelerini gösterir. Merhaba döşeme tooview hello dizin oluşturucusu sayısı'ı tıklatın. 
>
> ![Dizin oluşturucular ve veri kaynakları için kutucuklar][1]
>

## <a name="create-index"></a> Dizin oluşturma ve verileri yükleme
Arama sorguları, belirli arama davranışlarını iyileştirmek için kullanılan aranabilir verileri, meta verileri ve yapıları içeren bir *dizinde* yinelenir.

tookeep hello aracılığıyla bir dizin oluşturucu kullanarak gezinilebilen yerleşik bir örnek veri kümesi kullandığımız bu görevi portal tabanlı **veri içeri aktarma** Sihirbazı. 

#### <a name="step-1-start-hello-import-data-wizard"></a>1. adım: hello veri içeri aktarma Sihirbazını Başlat
1. Azure Search Hizmeti Panonuzda tıklatın **veri içeri aktarma** hello komut çubuğu toostart oluşturur hem de bir dizini dolduran bir Sihirbazı'nda.
   
    ![Verileri içeri aktar komutu][2]

2. Başlangıç Sihirbazı'nda tıklatın **veri kaynağı** > **örnekleri** > **realestate-us-sample**. Bu veri kaynağı önceden bir ad, tür ve bağlantı bilgileriyle adlandırılır. Oluşturulan kaynak, diğer içeri aktarma işlemlerinde yeniden kullanılabilecek bir “mevcut veri kaynağı” olur.

    ![Örnek veri kümesi seçme][9]

3. Tıklatın **Tamam** toouse onu.

#### <a name="step-2-define-hello-index"></a>2. adım: hello dizin tanımla
Dizin oluşturma genellikle el ile ve kod tabanlı, ancak hello Sihirbazı gezinme herhangi bir veri kaynağı için bir dizin oluşturabilirsiniz. En azından bir ad ve bir alanlar koleksiyonu dizin gerektirir, her bir belgenin belge anahtar toouniquely hello olarak işaretlenmiş bir alanla tanımlayın.

Alanların veri türleri ve öznitelikleri vardır. Merhaba onay kutuları hello üstte *dizin öznitelikleri* hello alanın nasıl kullanıldığını denetleme. 

* **Alınabilir**, arama sonuçları listesinde çıktığı anlamına gelir. Örneğin, alanlar yalnızca filtre ifadelerinde kullanıldığında bu onay kutusunun işaretini kaldırarak alanları arama sonuçları için kapsam dışı olarak işaretleyebilirsiniz. 
* **Filtrelenebilir**, **Sıralanabilir** ve **Modellenebilir** seçeneği bir alanın filtre, sıralama veya model gezinti yapısında kullanılıp kullanılamayacağını belirler. 
* **Aranabilir**, bir alanın tam metin aramasına dahil olduğu anlamına gelir. Dizelerde arama yapılabilir. Sayısal alanlar ve Boolean alanları genellikle aranamaz olarak işaretlenir. 

Varsayılan olarak, Başlangıç Sihirbazı'nı hello veri kaynağı benzersiz tanımlayıcıları için hello anahtar alanı hello temeli olarak tarar. Dizelere alınabilir ve aranabilir öznitelikler atanmıştır. Tam sayılara alınabilir, filtrelenebilir, sıralanabilir ve modellenebilir öznitelikler atanmıştır.

  ![Emlak dizini oluşturuldu][3]

Tıklatın **Tamam** toocreate başlangıç dizini.

#### <a name="step-3-define-hello-indexer"></a>3. adım: hello dizin oluşturucuyu tanımlama
Merhaba yine de **veri içeri aktarma** Sihirbazı'nı tıklatın **dizin oluşturucu** > **adı**ve hello dizin oluşturucu için bir ad yazın. 

Bu nesne, yürütülebilir bir işlemi tanımlar. Tıklattığınızda hemen sonra bunu yinelenen zamanlamaya göre ancak şimdi kullanım hello varsayılan seçeneği toorun hello dizin oluşturucu koyabilirsiniz **Tamam**.  

  ![emlak dizini oluşturucu][8]

## <a name="check-progress"></a>İlerleme durumunu denetleme
toomonitor veri almak, toohello hizmet panosunu geri dönün, aşağı kaydırın ve hello çift **dizin oluşturucular** döşeme tooopen hello dizin oluşturucular listesi. Yeni oluşturulan hello dizin oluşturucu listesinde durumunu gösteren ile Merhaba görmeniz gerekir "Sürüyor" ya da dizinli belge hello sayısı ile birlikte başarılı.

   ![Dizin oluşturucu ilerleme durumu iletisi][4]

## <a name="query-index"></a>Sorgu hello dizini
Artık hazır tooquery olan bir arama dizininiz var. **Arama Gezgini** hello portalda yerleşik bir sorgu aracıdır. Arama sonuçlarının beklediğiniz gibi olduğunu doğrulayabilmeniz için bir arama kutusu sağlar. 

> [!TIP]
> Merhaba, [Azure arama genel bakış videosu](https://channel9.msdn.com/Events/Connect/2016/138), aşağıdaki adımları hello hello video 6m08s gösterilen.
>

1. Tıklatın **arama Gezgini** hello komut çubuğunda.

   ![Search gezgini komutu][5]

2. Tıklatın **dizini Değiştir** hello üzerinde komut tooswitch çok*realestate-us-sample*.

   ![Dizin ve API komutları][6]

3. Tıklatın **API kümesini sürüm** REST API'leri kullanılabilir olan hello komut çubuğu toosee üzerinde. API'leri verin değil henüz genellikle yayımlanan toonew özelliklerine erişimi önizlemede. Aşağıdaki Hello sorgular için yönlendirilmiş sürece hello genel olarak kullanılabilir sürüm (2016-09-01) kullanın. 

    > [!NOTE]
    > [Azure Search REST API'sini](https://docs.microsoft.com/rest/api/searchservice/search-documents) ve hello [.NET kitaplığı](search-howto-dotnet-sdk.md#core-scenarios) tamamen eşdeğer olan ancak **arama Gezgini** yalnızca donanımlı toohandle REST çağrıdır. Sözdizimi için her ikisini de kabul [Basit Sorgu söz dizimi](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) ve [Lucene sorgu ayrıştırıcı tam](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), artı tüm arama parametrelerini bulunan hello [arama belge](https://docs.microsoft.com/rest/api/searchservice/search-documents) işlemleri.
    > 

4. Merhaba arama çubuğunda hello sorgu dizeleri girin ve tıklayın **arama**.

  ![Arama sorgusu örneği][7]

**`search=seattle`**

+ Merhaba `search` parametredir kullanılan tooinput bir anahtar sözcük aramasını tam metin araması, bu durumda, listeleri Kol ilçe, Washington durumda döndürme, içeren *Seattle* hello belge aranabilir herhangi alanında. 

+ **Arama Gezgini** belgeleri yoğun bir yapıya sahip değilse, ayrıntılı ve sabit tooread olduğu sonuçları JSON döndürür. Belgelerinizi bağlı olarak işleyici sonuçları tooextract önemli öğeleri aramak toowrite kod gerekebilir. 

+ Belgeleri hello dizindeki alınabilir olarak işaretlenmiş tüm alanlar oluşur. tooview dizin öznitelikleri hello Portalı'nda tıklatın *realestate-us-sample* hello içinde **dizinleri** döşeme.

**`search=seattle&$count=true&$top=100`**

+ Merhaba `&` simge olan herhangi bir sırada belirtilen kullanılan tooappend arama parametreleri. 

+  Merhaba `$count=true` parametresi, döndürülen tüm belgelerin hello toplam sayısını döndürür. `$count=true` tarafından bildirilen değişiklikleri izleyerek filtre sorgularını doğrulayabilirsiniz. 

+ Merhaba `$top=100` döndürür hello en yüksek derece hello toplam dışında 100 belgeleri. Varsayılan olarak, Azure Search hello ilk 50 en iyi eşleşenleri döndürür. Artırabilir ya da aracılığıyla hello azaltmak `$top`.

**`search=*&facet=city&$top=2`**

+ `search=*` boş bir aramadır. Boş aramalar her şeyi arar. Boş bir sorgu çok filtre gönderme veya model hello eksiksiz belgeler üzerinde bir açıklaması. Örneğin, bir olduğunu gezinti yapısı tooconsist hello dizindeki tüm şehirde istiyorsunuz.

+  `facet`Gezinti döndürür tooa UI denetimi geçirebilirsiniz yapılandırın. Kategorileri ve bir sayımı döndürür. Bu durumda, kategoriler Şehir hello sayısını temel alır. Azure Search'te toplama yoktur ancak her kategorideki belge sayısını veren `facet` ile tahmini bir toplama gerçekleştirebilirsiniz.

+ `$top=2`kullanabileceğinizi gösteren iki belge geri getirir `top` tooboth azaltın veya sonuçları artırın.

**`search=seattle&facet=beds`**

+ Bu sorgu *Seattle* için yapılan metin aramasında yatakların görünümüdür. `"beds"`bir model (sayısal, 1 ile 5) çünkü hello alan olarak alınabilir, filtrelenebilir işaretlenmiş ve başlangıç dizini ve hello modellenebilir değerler içerdiğinden belirtilen, (3 yatak, 4 yatak listelerini) gruplara listeleri kategorilere için ayırmak için uygundur. 

+ Yalnızca filtrelenebilir alanlardan görünüm oluşturulabilir. Yalnızca alınabilir alanları hello sonuçlarında döndürülebilir.

**`search=seattle&$filter=beds gt 3`**

+ Merhaba `filter` parametre, sağlanan hello ölçütleriyle eşleşen sonuçları döndürür. Bu durumda yatak odası sayısı 3’ten büyük olanlar. 

+ Filtre söz dizimi bir OData yapısıdır. Daha fazla bilgi edinmek için bkz. [OData söz dizimini filtreleme](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search).

**`search=granite countertops&highlight=description`**

+ İsabet vurgulama başvuruyor tooformatting metni belirli bir alanda bulunan hello anahtar sözcük eşleşmeleri verilen eşleşen. Arama terimi derine açıklama kaçınma, isabet vurgulama toomake ekleyebilirsiniz, daha kolay toospot. Bu durumda, tümcecik Merhaba biçimlendirilmiş `"granite countertops"` hello açıklaması alanında daha kolay toosee değil.

**`search=mice&highlight=description`**

+ Tam metin arama, benzer semantiğe sahip sözcük biçimlerini bulur. Bu durumda, arama sonuçları "fare", "fare" yanıt tooa anahtar sözcük araması fare infestation sahip ev için vurgulanan metni içerir. Farklı biçimlerde hello aynı sözcük sonuçlarında dil çözümlemesi nedeniyle ortaya çıkabilir. 

+ Azure Search, Lucene ve Microsoft’tan 56 çözümleyiciyi destekler. Azure arama tarafından kullanılan hello hello standart Lucene Çözümleyicisi varsayılandır. 

**`search=samamish`**

+ Merhaba Samammish Plato hello Seattle alanı içinde için 'samamish' gibi yanlış yazılmış sözcüklerin tooreturn eşleşmeleri tipik arama başarısız. toohandle yazım hatası hello sonraki örnekte açıklanan belirsiz aramayı kullanabilirsiniz.

**`search=samamish~&queryType=full`**

+ Benzer arama hello belirttiğinizde etkin `~` sembol ve yorumlar ve doğru ayrıştırmak için hello hello tam sorgu ayrıştırıcı kullanmak `~` sözdizimi. 

+ Benzer arama olduğunda kullanılabilir, ayarladığınızda oluşan hello tam sorgu ayrıştırıcı için tercih `queryType=full`. Merhaba tam sorgu ayrıştırıcı tarafından etkinleştirilen sorgu senaryolar hakkında daha fazla bilgi için bkz: [Lucene sorgu söz dizimi Azure Search'te](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search).

+ Zaman `queryType` olduğu belirtilmemiş, hello varsayılan Basit Sorgu ayrıştırıcı kullanılır. Merhaba Basit Sorgu ayrıştırıcı hızlıdır ancak belirsiz arama, normal ifadeler, yakınlık araması veya diğer gelişmiş sorgu türleri gerektiriyorsa, hello tam sözdizimi gerekir. 

**`search=*&$count=true&$filter=geo.distance(location,geography'POINT(-122.121513 47.673988)') le 5`**

+ Jeo-uzamsal arama hello desteklenen [edm. GeographyPoint veri türü](https://docs.microsoft.com/rest/api/searchservice/supported-data-types) koordinatları içeren bir alan. Coğrafi arama, [OData söz dizimini filtrele](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) seçeneğinde belirtilen bir tür filtredir. 

+ Merhaba örnek sorgu sonuçları değerinden 5 kilometre (enlem ve boylam koordinatları olarak belirtilir) belirli bir noktadan nerede konumsal veriler için tüm sonuçları filtreler. Ekleyerek `$count`, başlangıç uzaklığı veya hello koordinatları değiştirdiğinizde kaç sonuçların döndürülmesini görebilirsiniz. 

+ Arama uygulamanız ‘yakınımda bul’ özelliği içeriyorsa ya da harita navigasyonu kullanıyorsa jeo-uzamsal arama kullanışlıdır. Ancak tam metin arama değildir. Bir şehir veya ülke adına göre aramak için kullanıcı gereksinimleri varsa, şehir veya ülke adları, toplama toocoordinates içeren alanlar ekleyin.

## <a name="next-steps"></a>Sonraki adımlar

+ Yeni oluşturduğunuz hello nesnelerden herhangi birini değiştirin. Merhaba Sihirbazı bir kez çalıştırdıktan sonra geri dönün ve görüntülemek veya bileşenleri tek tek değiştirmek için: dizin, dizin oluşturucu veya veri kaynağı. Merhaba hello alanın veri türünü değiştirme gibi bazı düzenlemelere hello dizini izin verilmez, ancak çoğu özellik ve ayar değiştirilebilir.

  bileşenleri tek tek tooview, tıklatın hello **dizin**, **dizin oluşturucu**, veya **veri kaynakları** var olan bir nesne listesi, Pano toodisplay yerleştirir. toolearn daha bir yeniden oluşturma gerektirmeyen dizin düzenlemeleri hakkında bkz [güncelleştirme dizini (Azure Search REST API'si)](https://docs.microsoft.com/rest/api/searchservice/update-index).

+ Merhaba araçları ve diğer veri kaynakları ile adımları deneyin. Örnek veri kümesini hello `realestate-us-sample`, Azure Search'ün gezinebileceği bir Azure SQL veritabanı. Azure Search, Azure SQL Veritabanı'nın yanı sıra Azure Tablo depolama, Blob depolama, Azure VM'deki SQL Server ve Azure Cosmos DB'de gezinebilir ve düz veri yapılarından dizin oluşturabilir. Tüm bu veri kaynaklarının hello Sihirbazı'nda desteklenmez. Kodda bir *dizin oluşturucu* kullanarak bir dizini kolayca doldurabilirsiniz.

+ Diğer tüm dizin oluşturucu olmayan veri kaynakları, burada kodunuzu yeni iter ve satır kümeleri JSON tooyour dizini içinde değiştirilen bir gönderme modeli aracılığıyla desteklenir. Daha fazla bilgi edinmek için bkz. [Azure Search’te belge ekleme, güncelleştirme veya silme](https://docs.microsoft.com/rest/api/searchservice/addupdate-or-delete-documents).

Aşağıdaki bağlantıları ziyaret ederek burada bahsedilen diğer özellikler hakkında daha fazla bilgi edinin:

* [Dizin oluşturuculara genel bakış](search-indexer-overview.md)
* [(Merhaba dizin öznitelikleri hakkında ayrıntılı bir açıklama içerir) dizin oluşturma](https://docs.microsoft.com/rest/api/searchservice/create-index)
* [Arama Gezgini](search-explorer.md)
* [Search Belgeleri (sorgu söz dizimi örneklerini içerir)](https://docs.microsoft.com/rest/api/searchservice/search-documents)


<!--Image references-->
[1]: ./media/search-get-started-portal/tiles-indexers-datasources2.png
[2]: ./media/search-get-started-portal/import-data-cmd2.png
[3]: ./media/search-get-started-portal/realestateindex2.png
[4]: ./media/search-get-started-portal/indexers-inprogress2.png
[5]: ./media/search-get-started-portal/search-explorer-cmd2.png
[6]: ./media/search-get-started-portal/search-explorer-changeindex-se2.png
[7]: ./media/search-get-started-portal/search-explorer-query2.png
[8]: ./media/search-get-started-portal/realestate-indexer2.png
[9]: ./media/search-get-started-portal/import-datasource-sample2.png