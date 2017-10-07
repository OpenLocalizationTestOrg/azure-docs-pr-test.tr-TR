---
title: "aaaData bekletme ve depolama Azure Application ınsights'ta | Microsoft Docs"
description: Bekletme ve gizlilik ilkesi bildirimi
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: a6268811-c8df-42b5-8b1b-1d5a7e94cbca
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: bwren
ms.openlocfilehash: 7823431d03a57db5268d2724a0604e40666009f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-collection-retention-and-storage-in-application-insights"></a>Application Insights ile veri toplama, tutma ve depolama


Yüklediğinizde [Azure Application Insights] [ start] SDK'sı, uygulamanızda, uygulama toohello bulut hakkında telemetri gönderir. Doğal olarak, sorumlu geliştiriciler tam olarak hangi verilerin gönderilir, toohello veri olanlar ve nasıl denetimini tutabilirsiniz tooknow istiyor. Özellikle de hassas verileri gönderilen, depolanan ve ne kadar güvenli olduğu nedir? 

İlk olarak, hello kısa yanıt:

* "hello kutu dışı" çalıştırılan hello standart telemetri olası toosend hassas verileri toohello hizmet modüllerdir. Merhaba telemetri yük, performans ve kullanım ölçümleri, özel raporlar ve diğer Tanılama verileri ile ilgilidir. Merhaba ana kullanıcı verilerini hello tanılama raporlarında görünür durumda URL'leri; yine de uygun istiyor musunuz? Ancak, uygulamanızın bir URL düz metinde hassas verileri her durumda put döndürmemelidir.
* Ek özel telemetri toohelp gönderir kod yazabilirsiniz, tanılama ve kullanım izleme. (Bu genişletilebilirlik harika Application Insights özelliğidir.) Hata, bu kod kişisel içeren toowrite ve diğer hassas verileri mümkün olmayacaktır. Uygulamanız bu tür veriler ile çalışıyorsa, yazdığınız kapsamlı gözden geçirme işlemleri tooall hello kod uygulamalıdır.
* Geliştirme ve uygulamanızı test ederken, ne hello SDK tarafından gönderilen kolay tooinspect sağlanır. Merhaba veri çıkış windows hello IDE ve tarayıcı hata ayıklama hello görüntülenir. 
* Merhaba veri tutulan içinde [Microsoft Azure](http://azure.com) hello ABD veya Avrupa sunucuları. (Ancak uygulamanızı her yerden çalıştırabilirsiniz.) Azure sahip [güçlü güvenlik işler ve çok çeşitli uyumluluk standartlarını karşılayan](https://azure.microsoft.com/support/trust-center/). Yalnızca sizin ve belirlenen ekibinizin erişim tooyour verilere sahip. Microsoft personeli erişim tooit yalnızca belirli koşullarda sınırlı bilginiz dahilinde kısıtlanmış. Merhaba sunucuları olsa değil, aktarım sırasında şifrelenir.

Merhaba, bu makalenin kalanında daha tam olarak bu yanıtları elaborates. Bunu hemen ekibinizin parçası olmayan toocolleagues Göster toobe kendi içinde bulunan tasarlanmıştır.

## <a name="what-is-application-insights"></a>Application Insights nedir?
[Azure Application Insights] [ start] yardımcı olan Microsoft tarafından sağlanan bir hizmeti geliştirmek hello performans ve kullanılabilirlik, Canlı uygulamanızın değil. Uygulamanız, test sırasında hem yayımlanan veya dağıtılmış sonra çalıştığı tüm hello saat izler. Application Insights grafikler ve gösteren tablolar oluşturur, örneğin, çoğu kullanıcı alma günün ne zaman esnek hello uygulaması nasıl ve iyi bir dış tarafından sunulan hizmetler nasıl bağlıdır. Kilitlenmeler, hatalar veya performans sorunları varsa, ayrıntı toodiagnose hello neden hello telemetri verilerini aracılığıyla arama yapabilirsiniz. Ve hello hizmeti hello kullanılabilirlik ve performans, uygulamanızın herhangi bir değişiklik varsa e-posta gönderir.

Bu işlevselliği sipariş tooget, kendi kod parçası haline gelir, uygulamanızda bir Application Insights SDK'sı yükleyin. Uygulamanızı çalıştırırken hello SDK çalışması izler ve telemetri toohello Application Insights hizmeti gönderir. Bu tarafından barındırılan bir bulut hizmetidir [Microsoft Azure](http://azure.com). (Ancak tüm uygulamaları, Azure üzerinde barındırılan olanlar yalnızca Application Insights çalışır.)

![Merhaba SDK uygulamanızda telemetri toohello Application Insights hizmeti gönderir.](./media/app-insights-data-retention-privacy/01-scheme.png)

Merhaba Application Insights hizmeti depolar ve hello telemetri analiz eder. toosee hello çözümleme veya arama hello aracılığıyla telemetri, tooyour Azure hesabı ve açık hello Application Insights kaynağı, uygulamanız için oturum depolanır. Diğer ekibinizin üyeleri veya belirtilen Azure aboneleri de paylaşımı erişim toohello verileri oluşturabilirsiniz.

Merhaba Application Insights hizmeti, ' dışarı aktarılan verilerin alınabileceği örneğin tooa veritabanı veya tooexternal araçları. Her aracı hello hizmetinden elde özel bir anahtar sağlar. başlangıç anahtarı gerekirse iptal edilebilir. 

Uygulama Insights SDK'ları bir dizi uygulama türleri için kullanılabilir: web kendi J2EE veya ASP.NET sunucusu veya Azure; barındırılan hizmetleri Web istemcileri - diğer bir deyişle, bir web sayfasında çalışan hello kodu; Masaüstü uygulamaları ve Hizmetleri; Windows Phone, iOS ve Android gibi cihaz uygulamaları. Tüm telemetri toohello gönderdikleri aynı hizmet.

## <a name="what-data-does-it-collect"></a>Hangi veri toplamak?
### <a name="how-is-hello-data-is-collected"></a>Merhaba verilerdir nasıl toplanır?
Üç veri kaynağına vardır:

* Merhaba ya da uygulamanızla tümleştirin SDK [geliştirme](app-insights-asp-net.md) veya [çalışma zamanında](app-insights-monitor-performance-live-website-now.md). Farklı uygulama türleri için farklı Sdk'ler vardır. Ayrıca bir [SDK web sayfaları için](app-insights-javascript.md), hello son kullanıcının tarayıcıda hello sayfa birlikte yükler.
  
  * Her SDK çeşitli sahip [modülleri](app-insights-configuration-with-applicationinsights-config.md), farklı teknikleri toocollect farklı telemetri türlerini kullanın.
  * Merhaba SDK geliştirme yüklerseniz, kendi API toosend toplama toohello standart modüllerde kendi telemetrinizi kullanabilirsiniz. Bu özel telemetri toosend istediğiniz herhangi bir veri içerebilir.
* Bazı web sunucuları da hello uygulamayı çalıştırın ve CPU, bellek ve ağ doluluk hakkında telemetri göndermesine aracılar vardır. Docker ana bilgisayarları, örneğin, Azure Vm'leri ve [J2EE sunucuları](app-insights-java-agent.md) bu tür aracılar olabilir.
* [Kullanılabilirlik testleri](app-insights-monitor-web-app-availability.md) işlemleri istekleri tooyour web uygulaması düzenli aralıklarla göndermek Microsoft tarafından çalıştırılır. Merhaba sonuçları toohello Application Insights hizmeti gönderilir.

### <a name="what-kinds-of-data-are-collected"></a>Ne tür veriler toplanır?
Merhaba ana kategoriler şunlardır:

* [Web sunucusu telemetri](app-insights-asp-net.md) -HTTP istekleri.  URI, geçen süre tooprocess hello istek, yanıt kodu, istemci IP adresi. Oturum kimliği.
* [Web sayfaları](app-insights-javascript.md) -sayfası, kullanıcı ve oturum sayısı. Sayfa yükleme sürelerinin. Özel durumlar. AJAX çağrıları.
* Performans sayaçları - bellek, CPU, IO, ağ doluluk.
* İstemci ve sunucu bağlamı - OS, yerel ayar, cihaz türü, tarayıcı, ekran çözünürlüğü.
* [Özel durumlar](app-insights-asp-net-exceptions.md) ve çökme (Crash) - **yığın dökümleri**, yapı kimliği, CPU türü. 
* [Bağımlılıklar](app-insights-asp-net-dependencies.md) -tooexternal Hizmetleri REST, SQL, AJAX gibi çağırır. URI veya bağlantı dizesi, süresi, başarı, komutu.
* [Kullanılabilirlik testleri](app-insights-monitor-web-app-availability.md) -test ve adımları, yanıt süresi.
* [İzleme günlükleri](app-insights-asp-net-trace-logs.md) ve [özel telemetri](app-insights-api-custom-events-metrics.md) - **günlükleri veya telemetri kod herhangi bir şey**.

[Daha fazla ayrıntı](#data-sent-by-application-insights).

## <a name="how-can-i-verify-whats-being-collected"></a>Nasıl ne toplanan doğrulayabilirsiniz?
Visual Studio kullanarak hello uygulama geliştiriyorsanız, hello uygulama (F5) hata ayıklama modunda çalıştırın. Merhaba telemetri hello çıktı penceresinde görüntülenir. Buradan, kopyalamak ve kolay İnceleme için JSON olarak biçimlendirin. 

![](./media/app-insights-data-retention-privacy/06-vs.png)

Merhaba tanılama penceresinde daha okunabilir bir görünüm bulunmaktadır.

Web sayfaları için tarayıcınızın hata ayıklama penceresini açın.

![F12 tuşuna basın ve hello ağ sekmesini açın.](./media/app-insights-data-retention-privacy/08-browser.png)

### <a name="can-i-write-code-toofilter-hello-telemetry-before-it-is-sent"></a>Kod toofilter hello telemetri, gönderilmeden önce yazma?
Bu yazarak sağlayabileceğinizden bir [telemetri işlemci eklentisi](app-insights-api-filtering-sampling.md).

## <a name="how-long-is-hello-data-kept"></a>Ne kadar süre tutulacağını hello veri mi?
Ham veri noktaları (diğer bir deyişle, analizleri sorgulamak ve aramada incelemek öğeleri) için too90 gün saklanır. Daha uzun tookeep verilere gereksiniminiz varsa, kullanabileceğiniz [sürekli verme](app-insights-export-telemetry.md) toocopy, tooa depolama hesabı.

Toplanan veriler (diğer bir deyişle, sayıları, ortalamalar ve ölçüm Gezgininde gördüğünüz diğer istatistik bilgileri), 1 dakika 90 gün boyunca bir çizgisi adresindeki korunur.

## <a name="who-can-access-hello-data"></a>Merhaba veri erişebilecek mi?
Merhaba verilerdir görünür tooyou ve ekip üyelerinin bir kuruluş hesabı varsa. 

Kopyalanan tooother konumları olabilir ve tooother kişiler geçirilen siz ve ekip üyelerinizin tarafından verilebilir.

#### <a name="what-does-microsoft-do-with-hello-information-my-app-sends-tooapplication-insights"></a>Neler var Microsoft hello bilgilerle Uygulamam yapmak tooApplication Öngörüler gönderir?
Microsoft, yalnızca sipariş tooprovide hello hizmet tooyou içinde hello verileri kullanır.

## <a name="where-is-hello-data-held"></a>Merhaba verileri nerede tutulur?
* Merhaba ABD veya Avrupa. Yeni bir Application Insights kaynağı oluşturduğunuzda hello konum seçebilirsiniz. 


#### <a name="does-that-mean-my-app-has-toobe-hosted-in-hello-usa-or-europe"></a>Uygulamam hello ABD veya Avrupa barındırılan toobe sahip anlamı?
* Hayır. Uygulamanız herhangi bir yere, kendi şirket içi konakları veya hello bulut çalıştırabilirsiniz.

## <a name="how-secure-is-my-data"></a>Verilerim nasıl güvenli mi?
Application Insights, bir Azure hizmetidir. Güvenlik ilkeleri hello açıklanan [Azure güvenlik, gizlilik ve uyumluluk incelemeyi](http://go.microsoft.com/fwlink/?linkid=392408).

Merhaba verileri Microsoft Azure sunucularda depolanır. Hello Azure Portal'ın hesapları için hesap kısıtlamaları hello açıklanan [belge Azure güvenlik, gizlilik ve Uyumluluk](http://go.microsoft.com/fwlink/?linkid=392408).

Erişim tooyour veri Microsoft personeli tarafından sınırlandırılır. Biz verilerinizle yalnızca izniniz erişebilir ve onu kullanımınız gerekli toosupport olup olmadığını Application Insights. 

Bizim müşterilerin tüm uygulamalar (örneğin, veri hızlarını ve ortalama boyutu izlemeleri) toplamında veriler kullanılan tooimprove Application Insights bağlıdır.

#### <a name="could-someone-elses-telemetry-interfere-with-my-application-insights-data"></a>Başka birinin telemetri Application Insights verilerimi engelleyebilir mi?
Web sayfalarınıza hello kodda bulunabilir hello izleme anahtarını kullanarak ek telemetri tooyour hesabı gönderebilir. Yeterli ek verilerle ölçümlerinizi doğru uygulamanızın performansını ve kullanımını temsil.

Diğer projelerle kod paylaşıyorsanız, tooremove izleme anahtarını unutmayın.

## <a name="is-hello-data-encrypted"></a>Merhaba veriler şifrelenir mi?
Mevcut hello sunucularda içinde değil.

Veri merkezleri arasında hareket ederken tüm veriler şifrelenir.

#### <a name="is-hello-data-encrypted-in-transit-from-my-application-tooapplication-insights-servers"></a>My uygulama tooApplication Öngörüler sunucularından aktarımda Hello veriler şifrelenir?
Evet, https toosend veri toohello neredeyse tüm SDK'ları, web sunucuları, aygıtları ve HTTPS web sayfaları gibi portaldan kullanırız. Merhaba yalnızca düz HTTP web sayfalarından gönderilen veriler istisnadır. 

## <a name="personally-identifiable-information"></a>Kişisel bilgiler
#### <a name="could-personally-identifiable-information-pii-be-sent-tooapplication-insights"></a>Kişisel bilgilerin (PII) tooApplication Öngörüler gönderilen?
Evet, mümkündür. 

Genel bir yönerge olarak:

* Çoğu standart telemetri (diğer bir deyişle, size herhangi bir kod yazmadan gönderilen telemetri) açık PII dahil değildir. Ancak, bunun olası tooidentify kişiler tarafından olayları koleksiyonundan çıkarım olabilir.
* Özel durum ve izleme iletilerini PII içerebilir
* Özel telemetri - çağrıları hello API ya da günlük izlemelerini kullanarak kod içinde yazma TrackEvent gibi diğer bir deyişle, - seçtiğiniz herhangi bir veri içerebilir.

Bu belge hello sonunda Hello tablo toplanan hello verileri daha ayrıntılı açıklamaları içerir.

#### <a name="am-i-responsible-for-complying-with-laws-and-regulations-in-regard-toopii"></a>Yasalarına ve düzenlemelerine şekilde tooPII içinde ile uymak için sorumlu miyim?
Evet. Merhaba toplama ve kullanım hello veri uyumlu yasalarına ve düzenlemelerine ve hello Microsoft çevrimiçi Hizmet Koşulları'nı, sorumluluk tooensure olur.

Müşterilerinizin uygun şekilde hello veri uygulamanızı toplar ve hello verilerin nasıl kullanıldığını hakkında bilgilendirmek.

#### <a name="can-my-users-turn-off-application-insights"></a>Kullanıcılarım Application Insights kapatabilir miyim?
Doğrudan yönetilemez. Biz bir anahtar sağlamıyorsa, kullanıcılarınızın tooturn Application Insights kapalı çalışabilir.

Ancak, böyle bir özellik uygulamanızda uygulayabilirsiniz. Tüm hello SDK telemetri toplamayı devre dışı bırakır bir API ayarı içerir. 

#### <a name="my-application-is-unintentionally-collecting-sensitive-information-can-application-insights-scrub-this-data-so-it-isnt-retained"></a>Uygulamam istemeden hassas bilgileri toplanıyor. Korunur değil için Application Insights bu verilerini temizle?
Application Insights filtre ya da verilerinizi silin. Merhaba verilerini uygun şekilde yönetmek ve bu tür veri tooApplication Öngörüler göndermekten kaçınmanız gerekir.

## <a name="data-sent-by-application-insights"></a>Application Insights tarafından gönderilen verileri
Merhaba SDK'ları platformları arasında farklılık gösterir ve yüklemek için kullanabileceğiniz çeşitli bileşenler vardır. (Çok başvuran[Application Insights - genel bakış][start].) Her bileşen farklı veri gönderir.

#### <a name="classes-of-data-sent-in-different-scenarios"></a>Farklı senaryolarda gönderilen veri sınıfları
| Eylem | (Sonraki tabloya bakın) toplanan veri sınıfları |
| --- | --- |
| [Application Insights SDK'sı tooa .NET web projesi ekleme][greenbrown] |Sunucu bağlamı<br/>Çıkarımı yapılan<br/>Performans sayaçları<br/>İstekler<br/>**Özel durumlar**<br/>Oturum<br/>kullanıcılar |
| [IIS üzerinde Durum İzleyicisi yükleme][redfield] |Bağımlılıklar<br/>Sunucu bağlamı<br/>Çıkarımı yapılan<br/>Performans sayaçları |
| [Application Insights SDK'sı tooa Java web uygulaması Ekle][java] |Sunucu bağlamı<br/>Çıkarımı yapılan<br/>İstek<br/>Oturum<br/>kullanıcılar |
| [JavaScript SDK'sı tooweb Sayfası Ekle][client] |ClientContext <br/>Çıkarımı yapılan<br/>Sayfa<br/>ClientPerf<br/>AJAX |
| [Varsayılan özellikleri tanımlama][apiproperties] |**Özellikler** tüm standart ve özel olayları hakkında |
| [Çağrı TrackMetric][api] |Sayısal değerler<br/>**Özellikleri** |
| [Çağrı izleme *][api] |Olay adı<br/>**Özellikleri** |
| [Çağrı TrackException][api] |**Özel durumlar**<br/>Yığın Dökümü<br/>**Özellikleri** |
| SDK, veri toplayamazsınız. Örneğin: <br/> -Performans sayacı erişemiyor<br/> -telemetri Başlatıcı özel durumu |SDK tanılama |

İçin [diğer platformlar için SDK'lar][platforms], kendi belgelere bakın.

#### <a name="hello-classes-of-collected-data"></a>Toplanan veriler Hello sınıfları
| Toplanan veriler sınıfı | (Kapsamlı bir liste değil) içerir |
| --- | --- |
| **Özellikleri** |**Kodunuz tarafından belirlenen herhangi bir veriyi-** |
| DeviceContext |Kimliği, IP, yerel ayar, cihaz modeli, ağ, ağ türü, OEM adı, ekran çözünürlüğünü, rol örneği, rol adı, cihaz türü |
| ClientContext |İşletim sistemi, yerel ayar, dil, ağ, pencere çözümleme |
| Oturum |Oturum kimliği |
| Sunucu bağlamı |Makine adı, yerel ayar, işletim sistemi, cihaz, kullanıcı oturumu, kullanıcı bağlamı, işlemi |
| Çıkarımı yapılan |IP adresi, zaman damgası, işletim sistemi, tarayıcı coğrafi konumdan |
| Ölçümler |Ölçüm adı ve değeri |
| Olaylar |Olay ad ve değer |
| PageViews |URL ve sayfa adı veya ekran adı |
| İstemci performans |URL/sayfa adı, tarayıcı yükleme süresi |
| AJAX |Web sayfası tooserver gelen HTTP çağrıları |
| İstekler |URL, süresi, yanıt kodu |
| Bağımlılıklar |Tür (SQL, HTTP,...), bağlantı dizesi veya URI, eşitleme/zaman uyumsuz, süresi, başarı, SQL deyimi (ile durumu İzleyicisi) |
| **Özel durumlar** |Türü, **ileti**, çağrı yığınları, kaynak dosya ve satır numarası, iş parçacığı kimliği |
| Çökme (Crash) |İşlem kimliği, ana işlem kimliği, kilitlenme iş parçacığı kimliği; uygulama düzeltme eki, kimliği, yapı;  özel durum türü, adres, neden; Karıştırılmış simgeleri ve kayıtları, ikili başlangıç ve bitiş adreslerini, ikili dosya adı ve yolu, cpu türü |
| İzleme |**İleti** ve önem düzeyi |
| Performans sayaçları |İşlemci zamanı, kullanılabilir bellek, isteği hızı, özel durum hızı, işlem özel bayt, g/ç hızı, istek süresi, istek sırası uzunluğu |
| Kullanılabilirlik |Web testi yanıt kodu, her test adımı, test adını, zaman damgası, başarı, yanıt süresi, test konumunu süresi |
| SDK tanılama |İzleme iletisi veya özel durumu |

Yapabilecekleriniz [hello verilerin bazıları Applicationınsights.config düzenleyerek geçiş][config]

## <a name="credits"></a>KREDİLERİ
Bu ürün MaxMind, kullanılabilir tarafından oluşturulan GeoLite2 verileri içeren [http://www.maxmind.com](http://www.maxmind.com).



<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiproperties]: app-insights-api-custom-events-metrics.md#properties
[client]: app-insights-javascript.md
[config]: app-insights-configuration-with-applicationinsights-config.md
[greenbrown]: app-insights-asp-net.md
[java]: app-insights-java-get-started.md
[platforms]: app-insights-platforms.md
[pricing]: http://azure.microsoft.com/pricing/details/application-insights/
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md

