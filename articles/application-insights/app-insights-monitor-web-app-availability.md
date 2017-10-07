---
title: "aaaMonitor kullanılabilirlik ve yanıt hızını herhangi bir web sitesini | Microsoft Docs"
description: "Application Insights’ta web testleri ayarlayın. Web sitesi kullanılamaz duruma gelirse veya yavaş yanıt verirse uyarı alın."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 46dc13b4-eb2e-4142-a21c-94a156f760ee
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/25/2017
ms.author: bwren
ms.openlocfilehash: 4c5425c948770cc57a648ca50e217c75ac75fbd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-availability-and-responsiveness-of-any-web-site"></a>Web sitelerinin kullanılabilirlik ve yanıt hızını izleme
Web uygulaması veya web sitesi tooany sunucu dağıtıldıktan sonra kullanılabilirlik ve yanıt hızını testleri toomonitor ayarlayabilirsiniz. [Azure Application Insights](app-insights-overview.md) Merhaba Dünya noktalarından düzenli aralıklarla web istekleri tooyour uygulama gönderir. Uygulamanız yanıt vermezse veya yavaş yanıt verirse sizi uyarır.

Erişilebilir HTTPS uç noktası hello genel internet veya tüm HTTP için kullanılabilirlik testleri ayarlayabilirsiniz. Tooadd toohello web test etmekte site herhangi bir şey yok. Hatta, sitenizi toobe yok: üzerinde bağımlı bir REST API hizmeti test edebilirsiniz.

İki tür kullanılabilirlik testi vardır:

* [URL ping testi](#create): hello Azure portalında oluşturabileceğiniz basit bir sınama.
* [Çok adımlı web testi](#multi-step-web-tests): Visual Studio Enterprise ve karşıya yükleme toohello portal oluşturan.

Her uygulama kaynağı too25 kullanılabilirlik testleri oluşturabilirsiniz.

## <a name="create"></a>1. Kullanılabilirlik testi raporlarınız için kaynak açma

**Application Insights zaten yapılandırdıysanız** web uygulamanız için Application Insights kaynağı hello açmak [Azure portal](https://portal.azure.com).

**Veya yeni bir kaynak raporlarınızda toosee istiyorsanız** çok kaydolun[Microsoft Azure](http://azure.com), Git toohello [Azure portal](https://portal.azure.com)ve Application Insights kaynağı oluşturun.

![Yeni > Application Insights](./media/app-insights-monitor-web-app-availability/11-new-app.png)

Tıklatın **tüm kaynakları** tooopen hello genel bakış dikey penceresinde hello yeni kaynak için.

## <a name="setup"></a>2. URL ping testi oluşturma
Merhaba kullanılabilirlik dikey penceresini açın ve bir test ekleyin.

![En az hello Web sitenizin URL'sini doldurma](./media/app-insights-monitor-web-app-availability/13-availability.png)

* **Merhaba URL** herhangi bir web sayfası olabilir tootest istiyor, ancak gelen görünür olmalıdır genel internet hello. Merhaba URL sorgu dizesi içerebilir. Bu nedenle, örneğin, veritabanınızla biraz alıştırma yapabilirsiniz. Merhaba URL tooa yeniden yönlendirme çözümlenirse, biz bunu too10 yeniden yönlendirmeleri izleyin.
* **Bağımlı istekleri Ayrıştır**: Bu seçenek işaretlenirse, görüntüler, betikler, Stil dosyaları ve test altındaki hello web sayfasının parçası olan diğer dosyaları hello test ister. Merhaba kaydedilen yanıt süresi hello geçen süre tooget bu dosyaları içerir. Tüm bu kaynaklar hello tüm test için hello zaman aşımı süresi içinde başarıyla indirilemiyor hello sınama başarısız olur. 

    Merhaba seçeneği işaretli değilse hello test yalnızca belirttiğiniz hello URL'sindeki hello dosya ister.
* **Yeniden denemeyi etkinleştir**: Bu seçenek işaretlenirse hello test başarısız olduğunda, kısa bir süre sonra denenir. Art arda üç deneme başarısız olursa bir hata bildirilir. Sonraki testler ardından hello her zamanki test sıklığında gerçekleştirilir. Merhaba sonraki başarılı olana kadar yeniden deneme geçici olarak askıya alındı. Bu kural her test konuma bağımsız olarak uygulanır. Bu ayar önerilir. Ortalama olarak hataların yaklaşık %80’i yeniden deneme sırasında kaybolur.
* **Test sıklığı**: ne sıklıkta hello test her test konumdan çalıştırılacağını ayarlar. Beş dakikalık sıklığında ve beş test konumuyla, siteniz ortalama olarak dakikada bir test edilir.
* **Test konumları** hello yerleştirir nerede sunucularımızda web istekleri tooyour URL'si den gönderdiğiniz şunlardır. Bir konumdan fazla seçin; böylece, web sitenizdeki ağ sorunlarını ayırt edebilirsiniz. Too16 konumları seçebilirsiniz.
* **Başarı ölçütleri**:

    **Test zaman aşımı**: yavaş yanıtlar hakkında uyarı bu değeri toobe azaltın. Merhaba yanıtlar sitenizden bu süre içinde henüz alınmamıştır varsa hello test hata olarak kabul edilir. Seçtiyseniz **bağımlı istekleri Ayrıştır**, ardından tüm hello görüntüler, Stil dosyaları, betikler ve diğer bağımlı kaynaklar bu süre içinde alınmalıdır.

    **HTTP yanıtı**: hello başarılı sayılan durum kodunu döndürdü. 200, normal web sayfası döndürüldüğünü belirten hello koddur.

    **İçerik eşleşmesi**: "Hoş geldiniz!" gibi bir dize. Her yanıtta büyük küçük harfe duyarlı bir tam eşleşme oluştuğunu test edebiliriz. Joker karakter bulunmayan düz bir dize olmalıdır. Olması durumunda tooupdate olabilir sayfanızın içeriği değişirse unutmayın.
* **Uyarıları** beş dakikayı üç konumda hata varsa varsayılan olarak, tooyou gönderilir. Tek bir konumda büyük olasılıkla toobe bir ağ sorunu ve sitenizi olmayan bir sorun hatasıdır. Ancak hello eşik toobe daha fazla değiştirebilir veya duyarlı ve daha az de e-postaları hello değişiklik gönderilebilir.

    Bir uyarı ortaya çıktığında çağrılan bir [web kancası](../monitoring-and-diagnostics/insights-webhooks-alerts.md) ayarlayabilirsiniz. (Ancak şu anda sorgu parametreleri Özellikler aracılığıyla geçirilmez.)

### <a name="test-more-urls"></a>Daha fazla URL test etme
Daha fazla test ekleyin. Örneğin, ek tootesting giriş sayfanız, arama hello URL'sini test ederek veritabanınızın çalıştığından emin olabilir.


## <a name="monitor"></a>3. Kullanılabilirlik testi sonuçlarınızı görme

Birkaç dakika sonra'ı **yenileme** toosee test sonuçları. 

![Merhaba giriş dikey penceresinde Özet Sonuçları](./media/app-insights-monitor-web-app-availability/14-availSummary-3.png)

Merhaba scatterplot hello örnekleri tanılama testi adım ayrıntı olması test sonuçlarını gösterir. Merhaba test altyapısı hataları olan testleri için tanılama ayrıntı depolar. Başarılı testleri için tanılama ayrıntıları hello yürütmeleri bir kısmı için depolanır. Tüm hello yeşil/kırmızı nokta toosee hello test zaman damgası, test süresi, konum ve test adı gelin. Merhaba dağılım çizim toosee hello ayrıntılarını hello test sonucu herhangi bir nokta üzerinden'ı tıklatın.  

Konum, belirli bir testi seçin veya dönem toosee hello süre ilgi daha fazla sonuç hello süresini azaltabilir. Arama Gezgini toosee tüm yürütmeleri sonuçlarından veya bu veriler üzerinde analiz sorguları toorun özel raporlar kullanın.

Toplama toohello ham sonuçlarında ölçümleri Explorer'da iki kullanılabilirlik ölçümleri vardır: 

1. Kullanılabilirlik: Tüm test yürütmeleri arasında başarılı hello testleri yüzdesi. 
2. Test Süresi: Tüm test yürütmelerinde ortalama test süresi.

Filtreler hello test adı, konumu tooanalyze eğilimleri belirli test ve/veya konum uygulayabilirsiniz.

## <a name="edit"></a> Testleri inceleme ve düzenleme

Merhaba Özet sayfası, belirli bir test seçin. Burada özel sonuçları görebilir ve düzenleyebilir ya da geçici olarak devre dışı bırakabilirsiniz.

![Web testini düzenleme veya devre dışı bırakma](./media/app-insights-monitor-web-app-availability/19-availEdit-3.png)

Toodisable kullanılabilirlik testleri veya hizmetinizde Bakımı gerçekleştirirken kuralları ilişkili hello uyarı isteyebilirsiniz. 

## <a name="failures"></a>Hata görürseniz
Kırmızı noktaya tıklayın.

![Kırmızı noktaya tıklama](./media/app-insights-monitor-web-app-availability/open-instance-3.png)


Bir kullanılabilirlik testi sonucundan şunları yapabilirsiniz:

* Sunucudan alınan hello yanıtı inceleyin.
* Merhaba başarısız istek örneği işlenirken sunucu uygulamanız tarafından gönderilen hello telemetriyi açın.
* Bir sorun oturum veya Git veya VSTS tootrack hello sorun iş öğesi. Merhaba hata bağlantı toothis olayı içerir.
* Merhaba web test sonucu Visual Studio'da açın.


*Sorunsuz görünüyor ancak hata olarak mı bildiriliyor?* Tüm hello görüntüleri, betikler, stil sayfaları ve hello sayfa tarafından yüklenen diğer dosyaları denetleyin. Herhangi biri başarısız olursa, hello ana html sayfası Tamam olarak yüklense bile hello test başarısız olarak raporlanır.

*İlgili öğe yok mu?* Sunucu tarafı uygulamanız için Application Insights ayarlanmışsa, bunun nedeni [örnekleme](app-insights-sampling.md) işleminin devam ediyor olması olabilir. 

## <a name="multi-step-web-tests"></a>Çok adımlı web testleri
Bir dizi URL'nin bulunduğu bir senaryoyu izleyebilirsiniz. Örneğin, bir satış Web sitesi izliyorsanız, öğeleri toohello ekleme alışveriş sepeti düzgün çalıştığını test edebilirsiniz.

> [!NOTE] 
> Çok adımlı web testleri ücrete tabidir. [Fiyatlandırma düzeni](http://azure.microsoft.com/pricing/details/application-insights/).
> 

çok adımlı bir test toocreate, Visual Studio Enterprise kullanarak hello senaryo kaydetmek ve tooApplication Öngörüler kaydı hello yükleyin. Application Insights hello senaryoyu aralıklarla başlayarak yeniden oynatılır ve hello yanıtları doğrular.

> [!NOTE]
> Testlerinizde kodlanmış işlevler veya döngüler kullanamazsınız. Merhaba test tamamen hello .webtest komut dosyasında yer almalıdır. Ancak, standart eklentiler kullanabilirsiniz.
>

#### <a name="1-record-a-scenario"></a>1. Senaryo kaydetme
Visual Studio Enterprise kullanan bir web oturumu toorecord.

1. Web performans testi projesi oluşturun.

    ![Visual Studio Enterprise Edition'da hello Web performansı ve yük testi şablonundan bir proje oluşturun.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-create.png)

 * *Merhaba Web performansı ve yük testi şablon görmüyorum?* - Visual Studio Enterprise’ı kapatın. Açık **Visual Studio yükleyicisi** toomodify, Visual Studio Enterprise yükleme. **Tek Bileşenler** altında **Web Performansı ve yük testi araçları**’nı seçin.

2. Merhaba .webtest dosyasını açın ve kaydı başlatın.

    ![Merhaba .webtest dosyasını açın ve Kaydet'e tıklayın.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-start.png)
3. Testinizde toosimulate istediğiniz kullanıcı eylemleri hello: Web sitenizi açın, bir ürün toohello Sepeti ekleyin ve benzeri. Sonra testinizi durdurun.

    ![Internet Explorer'da Hello web Testi Kaydedicisi çalışır.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-record.png)

    Uzun bir senaryo oluşturmayın. 100 adımlık ve 2 dakikalık bir sınır vardır.
4. Merhaba testine düzenleyin:

   * Doğrulama, toocheck hello alınan metin ve yanıt kodlarını ekleyin.
   * Gereksiz tüm etkileşimleri kaldırma. Ayrıca, resim veya tooad ya da sitelerin izlenmesi için bağımlı istekleri kaldırabilirsiniz.

     Yalnızca hello test betiğini düzenleyebildiğinizi - özel kod ekleme veya başka web testlerinden çağrı unutmayın. Döngüler hello eklemeyin. Standart web testi eklentileri kullanabilirsiniz.
5. Merhaba test çalıştığından emin Visual Studio toomake çalıştırın.

    Merhaba web test Çalıştırıcısı bir web tarayıcısı açar ve kaydettiğiniz eylemleri yineler hello. Beklediğiniz gibi çalıştığından emin olun.

    ![Visual Studio'da hello .webtest dosyasını açın ve Çalıştır'ı tıklatın.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-run.png)

#### <a name="2-upload-hello-web-test-tooapplication-insights"></a>2. Merhaba web testi tooApplication Öngörüler karşıya yükle
1. Merhaba Application Insights portalında bir web testi oluşturun.

    ![Merhaba web testleri dikey penceresinde Ekle'yi seçin.](./media/app-insights-monitor-web-app-availability/16-another-test.png)
2. Çok adımlı testi seçin ve hello .webtest dosyasını yükleyin.

    ![Çok adımlı web testini seçin.](./media/app-insights-monitor-web-app-availability/appinsights-71webtestUpload.png)

    Kümesi hello test konumları, sıklığı ve uyarı parametrelerinde hello aynı şekilde ping gibi sınar.

#### <a name="3-see-hello-results"></a>3. Merhaba sonuçları bakın

Test görüntülemek sonuçlarını ve hatalarını içinde hello aynı şekilde olarak tek url sınamaları.

Ayrıca, hello test sonuçları tooview indirebilirsiniz Visual Studio bunları.

#### <a name="too-many-failures"></a>Çok fazla hata mı var?

* Yaygın bir başarısızlık nedeni hello testin çok uzun çalıştığı yerdir. İki dakikadan uzun çalıştırılmamalıdır.

* Bir sayfanın tüm hello kaynakları betikler, stil sayfaları, görüntüler ve diğerleri de dahil olmak üzere hello test toosucceed için doğru yüklemelisiniz unutmayın.

* Hello web testinin tamamen hello .webtest komut dosyasında yer almalıdır: hello testte kodlanmış işlevleri kullanamazsınız.

### <a name="plugging-time-and-random-numbers-into-your-multi-step-test"></a>Çok adımlı testinizde bağlı kalma süresi ve rasgele rakamlar
Dış bir kaynağa ait stoklar gibi zamana bağımlı veriler alan bir aracı test ettiğinizi varsayalım. Web testinizi kaydettiğinizde, toouse belirli saatler sahip, ancak gibi hello parametrelerinin test, StartTime ve EndTime ayarlayın.

![Parametrelere sahip web testi.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-parameters.png)

Merhaba testi çalıştırdığınızda, EndTime her zaman zaman toobe hello sunmak istediğiniz ve başlangıç saati, 15 dakika olmalıdır önce.

Web testi eklentileri toodo Parametreleştirme kez hello yolunu sağlar.

1. İstediğiniz her değişken parametre değeri için bir web testi eklentisi ekleyin. Merhaba web testi araç çubuğunda seçin **Web Testi Eklentisi Ekle**.

    ![Web Testi Eklentisi Ekle’yi, sonra da bir türü seçin.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugins.png)

    Bu örnekte, hello tarih saat eklentisinin iki örneğini kullanın. Bir örnek "15 dakika önce" için, bir örnek de "şimdi" için.
2. Her eklentinin Hello özelliklerini açın. Bir ad verin ve geçerli saati toouse hello ayarlayın. Bunlardan birini Dakika Ekle = 15 olarak ayarlayın.

    ![Adı, Geçerli Saati Kullan’ı ve Dakika Ekle’yi ayarlayın.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-parameters.png)
3. Merhaba web testi parametrelerinde, eklenti adına {{plug-in name}} tooreference kullanın.

    ![Merhaba test parametresinde {{plug-in name}} kullanın.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-name.png)

Şimdi, test toohello portalınızı karşıya yükleyin. Her hello testi Çalıştır'hello dinamik değerler kullanır.

## <a name="dealing-with-sign-in"></a>Oturum açmayla ilgilenme
Kullanıcılarınızın tooyour uygulamada oturum açarsanız hello oturum açma ötesinde sayfaları test edebilirsiniz bir oturum açma benzetimi için çeşitli seçenekleriniz vardır. kullandığınız hello yaklaşım hello hello uygulamanın sağladığı güvenlik türüne bağlıdır.

Her durumda, uygulamanızı test etme yalnızca hello amacı için bir hesap oluşturmanız gerekir. Gerçek kullanıcıları etkileyen hello web testleri hiçbir olasılığını olmasını sağlamak Mümkünse, bu test hesabın hello izinleri kısıtlayın.

### <a name="simple-username-and-password"></a>Basit kullanıcı adı ve parola
Hello web testini kaydetme her zamanki gibi. Önce tanımlama bilgilerini silin.

### <a name="saml-authentication"></a>SAML kimlik doğrulaması
Web testleri için kullanılabilir hello SAML eklentisini kullanın.

### <a name="client-secret"></a>Gizli anahtar
Uygulamanızda gizli anahtar içeren bir oturum açma yolu varsa bu yolu kullanın. Azure Active Directory (AAD), gizli anahtarla oturum açmayı sağlayan bir hizmet örneğidir. AAD'de, hello gizli hello uygulama anahtarı ' dir.

Aşağıda uygulama anahtarı kullanan bir Azure web uygulaması için web testi örneği verilmiştir:

![Gizli anahtar örneği](./media/app-insights-monitor-web-app-availability/110.png)

1. Gizli anahtar (AppKey) kullanarak AAD’den belirteç alın.
2. Yanıttan taşıyıcı belirteci ayıklayın.
3. Merhaba yetkilendirme üstbilgisinde taşıyıcı belirteci kullanarak API çağrısı.

Merhaba web testi gerçek bir istemcidir - diğer bir deyişle, kendi uygulama - AAD'de var olduğundan emin olun ve kendi ClientID + appkey kullanın. Hizmetinizi test altında kendi uygulama AAD'de de vardır.: hello AppID bu uygulamanın URI hello web testi hello "kaynak" alanında yansıtılır.

### <a name="open-authentication"></a>Açık Kimlik Doğrulaması
Microsoft veya Google hesabınızla oturum açma, bir açık kimlik doğrulaması örneğidir. Birçok uygulama tooinvestigate, ilk Taktik bunun nedenle OAuth sağladıkları kullanım istemci gizli alternatif, o olasılığı hello olduğunu.

Testinizde OAuth kullanılarak oturum gerekir, hello genel yaklaşım şöyledir:

* Web tarayıcınız, hello kimlik doğrulama sitesi ve uygulamanız arasındaki Fiddler tooexamine hello trafiği gibi bir araç kullanın.
* İki veya daha fazla oturum farklı makineler veya tarayıcılar kullanarak bileşenlere gerçekleştirmek veya uzun aralıklarla (tooallow belirteçleri tooexpire).
* Farklı oturumları karşılaştırarak hello tooyour uygulama sunucusuna oturum açma işleminden sonra sonra geçirilen site, kimlik doğrulaması'ndan geçirildi hello belirteci tanımlayın.
* Visual Studio’yu kullanarak web testini kaydetme
* Merhaba belirteci hello doğrulayıcıdan döndürüldüğünde hello parametre ayarlama ve hello sorgu toohello sitede kullanılarak hello belirteçleri parametreleyin.
  (Visual Studio tooparameterize hello test çalışır, ancak doğru hello belirteçleri Parametreleştirme değil.)


## <a name="performance-tests"></a>Performans testleri
Web sitenizde bir yük testi çalıştırabilirsiniz. Merhaba kullanılabilirlik test gibi Merhaba Dünya bizim noktalarından basit istekleri veya çok adımlı istekleri gönderebilirsiniz. Kullanılabilirlik testinden farklı olarak eşzamanlı birden fazla kullanıcıyı benzeten çok sayıda istek gönderilir.

Merhaba genel bakış dikey penceresinden açmak **ayarları**, **performans testleri**. Bir test oluşturduğunuzda, davet tooconnect tooor bir Visual Studio Team Services hesabı oluşturun.

Merhaba test tamamlandığında yanıt sürelerini ve başarı oranları gösterilir.


![Performans testi](./media/app-insights-monitor-web-app-availability/perf-test.png)

> [!TIP]
> bir performans testi tooobserve hello etkilerini kullanmak [canlı akış](app-insights-live-stream.md) ve [profil oluşturucu](app-insights-profiler.md).
>

## <a name="automation"></a>Otomasyon
* [PowerShell komut dosyaları tooset bir kullanılabilirlik test yukarı kullanmak](app-insights-powershell.md#add-an-availability-test) otomatik olarak.
* Bir uyarı ortaya çıktığında çağrılan bir [web kancası](../monitoring-and-diagnostics/insights-webhooks-alerts.md) ayarlayın.

## <a name="qna"></a>Sorularınız mı var? Sorunlarınız mı var?
* *Web testimden kod çağırabilir miyim?*

    Hayır. Merhaba adımları hello test hello .webtest dosyasında olmalıdır. Bu nedenle, başka web testlerini çağıramaz, döngüleri kullanamazsınız. Ancak yararlı bulabileceğiniz bir dizi eklenti vardır.
* *HTTPS destekleniyor mu?*

    TLS 1.1 ve TLS 1.2 desteklenir.
* *"Web testleri" ve "kullanılabilirlik testleri" arasında bir fark var mı?*

    Merhaba iki terimi birbirlerinin yerine başvurulabilir. Kullanılabilirlik testleri olduğu hello tek URL PING daha genel bir terim ayrıca toohello çok adımlı web testleri test eder.
* *Toouse kullanılabilirlik testleri üzerinde bir güvenlik duvarının arkasında çalışan kendi dahili sunucumuzda ister.*

    İki olası çözümü vardır:
    
    * Güvenlik Duvarı, toopermit gelen istekleri hello gelen yapılandırma [web hizmetlerimizi IP adreslerini test aracılarını](app-insights-ip-addresses.md).
    * Kendi kod tooperiodically test iç sunucunuz yazma. Merhaba kodu arka plan işlemi olarak, güvenlik duvarının arkasındaki bir test sunucusunda çalıştırın. Test işleminizi sonuçlarını tooApplication Öngörüler kullanarak gönderebilirsiniz [TrackAvailability()](https://docs.microsoft.com/dotnet/api/microsoft.applicationinsights.telemetryclient.trackavailability) hello çekirdek SDK paketi API. Bu, test sunucu toohave giden erişim toohello Application Insights alım uç nokta gerektiriyor, ancak çok daha küçük güvenlik riski gelen istekleri izin veren, hello alternatif daha. Merhaba sonuçları hello kullanılabilirlik web testleri dikey görünmez, ancak Analytics, arama ve ölçüm Gezgini kullanılabilirlik sonuç olarak görünür.
* *Çok adımlı web testi karşıya yüklenemiyor*

    300 K boyut sınırı vardır.

    Döngüler desteklenmez.

    Başvuruları tooother web testleri desteklenmez.

    Veri kaynakları desteklenmez.
* *Çok adımlı testim tamamlanmıyor*

    Test başına 100 istek sınırı var.

    iki dakikadan uzun çalışırsa hello test durdurulur.
* *İstemci sertifikalarıyla testi nasıl çalıştırırım?*

    Üzgünüz, bunu desteklemiyoruz.


## <a name="next"></a>Sonraki adımlar
[Tanılama günlüklerinde arama yapma][diagnostic]

[Sorun giderme][qna]

[Web testi aracılarının IP adresleri](app-insights-ip-addresses.md)

<!--Link references-->

[azure-availability]: ../insights-create-web-tests.md
[diagnostic]: app-insights-diagnostic-search.md
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
