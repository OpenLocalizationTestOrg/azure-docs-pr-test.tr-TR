---
title: "Azure CDN aaaAnalyze kenar düğümü performansını | Microsoft Docs"
description: "Microsoft Azure cdn'de kenar düğümü performansını analiz edin. Edge Performans Analizi CDN hello için ayrıntılı bilgileri trafiği ve bant genişliği kullanımı sağlar."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 8cc596a7-3e01-4f76-af7b-a05a1421517e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 35361d1c5e27fc6b8536c29e33c2ed217ee4d17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-edge-node-performance-in-microsoft-azure-cdn"></a>Microsoft Azure CDN’de kenar düğümü performansını çözümleme
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Genel Bakış
Edge Performans Analizi CDN hello için ayrıntılı bilgileri trafiği ve bant genişliği kullanımı sağlar. Bu bilgiler daha sonra varlıklarınızı önbelleğe alınmış ve teslim tooyour istemcileri nasıl yükleniyor üzerinde toogain Insight izin kullanılan toogenerate oluşturan eğilim istatistikleri olabilir. Buna karşılık, bu toobetter Dengeleme hello CDN nasıl toooptimize hello teslimini içerik ve toodetermine ne sorunları üzerinde bir stratejisi olmalıdır tooform tackled sağlar. Sonuç olarak, yalnızca mümkün tooimprove veri teslimat performansı olacaktır, ancak ayrıca olur CDN maliyetleriniz mümkün tooreduce olabilir.

> [!NOTE]
> Tüm raporlar UTC/GMT gösterimini bir tarih belirtmek için kullanın.
> 
> 

## <a name="reports-and-log-collection"></a>Raporlar ve günlük toplama
Raporlar oluşturmadan önce CDN etkinlik verileri hello kenar Performans Analizi modülü tarafından toplanan gerekir. Bu koleksiyonu işlemi, bir gün ve onu kapsayan sonra hello önceki gün sırasında gerçekleşen hello etkinlik gerçekleşir. Bir raporun istatistikleri işlenmiş ve mutlaka yapın hello zaman hello günün istatistikleri örneği temsil eden anlamına gelir, geçerli gün hello eksiksiz veri hello için içerir. Merhaba birincil Bu raporların tooassess performans işlevdir. Bunlar faturalandırma amaçları veya tam sayısal istatistikler için kullanılmamalıdır.

> [!NOTE]
> Merhaba ham veriler kenar performans analitik raporlar oluşturulmuş en az 90 gün için kullanılabilir.
> 
> 

## <a name="dashboard"></a>Pano
Merhaba kenar Performans Analizi Pano grafiği ve istatistikleri aracılığıyla geçerli ve geçmiş CDN trafiği izler. Bu Pano toodetect son ve uzun vadeli eğilimleri CDN trafiği hello performansını hesabınız için kullanın.

Bu panoyu oluşur:

* Anahtar ölçümleri ve eğilimleri hello görselleştirme sağlayan etkileşimli bir grafik.
* Anahtar ölçümleri ve eğilimleri için uzun vadeli desenleri duygusu sağlayan bir zaman çizelgesi.
* Anahtar ölçümleri ve hakkında istatistiksel bilgi CDN ağımız genel performansı, kullanım ve verimliliği tarafından ölçülen site trafiğini artırır.

### <a name="accessing-hello-edge-performance-dashboard"></a>Merhaba kenar performans Pano erişme
1. Merhaba CDN profili dikey penceresinden hello tıklayın **Yönet** düğmesi.
   
    ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-edge-performance/cdn-manage-btn.png)
   
    Merhaba CDN Yönetim Portalı açar.
2. Merhaba üzerine getirin **Analytics** sekmesini ve ardından hello üzerine getirin **kenar Perfomance Analytics** çıkma.  Tıklayın **Pano**.
   
    Merhaba edge düğüm analytics Panosu görüntülenir.

### <a name="chart"></a>Grafik
Başlangıç Panosu bir ölçüm hello doğrudan göründüğü hello zaman çizelgesi seçilen süre izleyen bir grafik içerir.  CDN Etkinliğin son iki yıl toohello grafik bir zaman çizelgesi doğrudan hello grafik altında görüntülenir.

#### <a name="using-hello-chart"></a>Merhaba grafik kullanma
* Varsayılan olarak, hello son 30 gün için hello önbellek verimliliği hız grafiğinin.
* Bu grafik, günlük olarak Harmanlanmış verilerden oluşturulur.
* Merhaba çizgi grafiği bir günde üzerine gelerek veya onları hello ölçüm tarih ve hello değerini belirli bir tarihte belirtir.
* Hafta sonları vurgulayın tootoggle hafta sonları hello grafik üzerine temsil açık gri dikey çubuk bir katmana tıklayın. Bu tür bir katmana hafta sonları trafik düzenlerini tanımlamak için yararlıdır.
* Görünüm bir yıl önce tootoggle hello önceki kaplamasını tıklatın yılın etkinliğini hello üzerinden aynı zaman dilimi hello grafik üzerine. Bu tür karşılaştırma uzun vadeli CDN kullanım desenlerini bir anlayış sağlar. Merhaba sağ üst köşesindeki hello grafik her çizgi grafiği hello renk kodunu gösteren bir gösterge içerir.

#### <a name="updating-hello-chart"></a>Merhaba grafik güncelleme
* Zaman aralığı: hello aşağıdakilerden birini gerçekleştirin:
  * Merhaba Zaman Çizelgesi'nde Hello istediğiniz bölgeyi seçin. Merhaba grafik seçili süre toohello karşılık gelen verilerle güncelleştirilir.
  * Çift tooa en fazla iki yıllık tüm kullanılabilir geçmiş verileri grafik toodisplay hello.
* Ölçüm: sonraki istenen toohello ölçüm görünür hello grafiği simgesine tıklayın. Merhaba grafik ve hello zaman çizelgesi hello karşılık gelen ölçüm verileri ile yenilenecek.

### <a name="key-metrics-and-statistics"></a>Anahtar ölçümleri ve istatistikleri
#### <a name="efficiency-metrics"></a>Verimlilik ölçümleri
Bu ölçümler hello amacı toosee olup önbellek verimliliği geliştirilebilir. Önbellek verimliliği türetilen hello başlıca yararları şunlardır:

* Azaltılmış yük açabilir hello kaynak sunucusunda:
  * Daha iyi web sunucusunun performans.
  * İşlem maliyetlerini düşürür.
* Daha fazla isteği hello doğrudan CDN sunulacak bu yana veri teslim hızlandırma geliştirilmiş.

| Alan | Açıklama |
| --- | --- |
| Önbellek verimliliği |Merhaba önbellekten sunulduğu aktarılan verilerin yüzdesini gösterir. Bu ölçüm ölçümleri hello önbelleğe alınmış bir sürümü olduğunda içeriği doğrudan hello CDN (Kenar sunucuları) toorequesters (örneğin, web tarayıcısı) ' sunulduğu istenen |
| İsabet oranı |Merhaba önbelleğinden sunulduğunu isteklerinin yüzdesini gösterir. Bu ölçüm ölçümleri hello önbelleğe alınmış bir sürümü, içeriği doğrudan hello CDN (Kenar sunucuları) toorequesters (örneğin, web tarayıcısı) ' sunulduğu istedi. |
| % Uzak bayt - önbellek yapılandırma |Kaynak sunucuları toohello hello atlama önbellek özelliği (HTTP kurallar altyapısı) sonucunda önbelleğe alınmamış CDN (Kenar sunucuları) gelen sunulduğu trafiği Hello yüzdesini gösterir. |
| Uzak bayt - önbellek süresi dolan yüzdesi |Kaynak sunucuları toohello CDN (Kenar sunucuları) sunulduğu trafiği Hello yüzdesini sonucunda eski içerik COLLECTION gösterir. |

#### <a name="usage-metrics"></a>Ölçümleri kullanma
Bu ölçümler Hello amacı maliyet kesme ölçüleri aşağıdaki hello tooprovide fikirler şöyledir:

* Merhaba CDN aracılığıyla işletim maliyetlerini en aza indirir.
* Önbellek verimliliği ve sıkıştırma aracılığıyla CDN harcamalarını azaltır.

> [!NOTE]
> Trafik birim numaralarını oranları yüzdeleri ve hesaplamalarda kullanıldı ve hello toplam trafiğin bir kısmını yüksek hacimli müşteriler için yalnızca gösterebilir trafiğin temsil eder.
> 
> 

| Alan | Açıklama |
| --- | --- |
| Giden Ave bayt |Merhaba hello CDN (Kenar sunucuları) toohello isteyenin (örneğin, web tarayıcısı) sunulan her istek için aktarılan bayt sayısını gösterir. |
| Hiçbir önbellek yapılandırma bayt oranı |Merhaba, toohello atlama önbellek özelliğinin önbelleğe alınmamış hello CDN (Kenar sunucuları) toohello isteyenin (örneğin, web tarayıcısı) gelen sunulan trafik yüzdesini gösterir. |
| Sıkıştırılmış bayt oranı |CDN (Kenar sunucuları) toorequesters (örneğin, web tarayıcısı) hello gönderilen trafiğin Hello yüzdesini sıkıştırılmış biçimde gösterir. |
| Giden bayt |Merhaba hello CDN (Kenar sunucuları) toohello isteyenin (örneğin, web tarayıcısı) teslim edilen bayt cinsinden veri miktarını gösterir. |
| Bayt cinsinden |Merhaba sahiplerini (örneğin, web tarayıcısı) toohello CDN (Kenar sunucuları) gönderilen bayt cinsinden veri miktarını gösterir. |
| Bayt uzaktan |Merhaba CDN ve müşteri kaynak sunucuları toohello CDN (Kenar sunucuları) gönderilen bayt cinsinden veri miktarını gösterir. |

#### <a name="performance-metrics"></a>Performans ölçümleri
Bu ölçümler Hello amacı tootrack, trafik için genel CDN performansı.

| Alan | Açıklama |
| --- | --- |
| Aktarım hızı |İçerik hello CDN tooa isteyenin aktarıldı hello ortalaması gösterir. |
| Süre |Merhaba ortalama zamanını gösterir milisaniye cinsinden toodeliver varlık tooa isteyenin (örneğin, web tarayıcısı) sürdü. |
| Sıkıştırılmış isteği hızı |Merhaba hello CDN (Kenar sunucuları) toohello isteyenin (örneğin, web tarayıcısı) teslim isabet yüzdesi sıkıştırılmış biçimde gösterir. |
| 4xx hata oranı |4xx durum kodu oluşturulan isabet Hello yüzdesini gösterir. |
| 5XX hata oranı |Bir 5xx durum kodu oluşturulan isabet Hello yüzdesini gösterir. |
| İsabet sayısı |CDN içerik isteklerini Hello sayısını gösterir. |

#### <a name="secure-traffic-metrics"></a>Güvenli trafiği ölçümleri
Bu ölçümler Hello amacı tootrack CDN performans HTTPS trafiği için budur.

| Alan | Açıklama |
| --- | --- |
| Güvenli önbellek verimliliği |Önbellekten sunulduğunu HTTPS isteklerinde aktarılan verilerin Hello yüzdesini gösterir. Bu ölçüm, önbelleğe alınan bir hello sürümü hello doğrudan CDN (Kenar sunucuları) toorequesters (örneğin, web tarayıcısı) sunulan içeriği HTTPS üzerinden istendiğinde ölçer. |
| Güvenli aktarım hızı |HTTPS üzerinden içerik hello CDN (Kenar sunucuları) toorequesters (örneğin, web sunucuları) aktarıldı hello ortalaması gösterir. |
| Ortalama güvenli süresi |Merhaba ortalama zamanını gösterir milisaniye cinsinden toodeliver varlık tooa isteyenin (örneğin, web tarayıcısı) HTTPS üzerinden sürdü. |
| Güvenli İsabetli Okuma |Merhaba CDN içeriğini HTTPS isteklerinin sayısını gösterir. |
| Giden güvenli bayt |Merhaba CDN (Kenar sunucuları) toohello isteyenin (örneğin, web tarayıcısı) teslim bayt cinsinden HTTPS trafiği Hello miktarını gösterir. |

## <a name="reports"></a>Reports
Bu modüldeki her bir raporu ölçümleri farklı türleri için bant genişliği ve trafik kullanım istatistikleri ve grafik içerir (örneğin, HTTP durum kodları, önbellek durum kodları, istek URL'si, vb..). Bu bilgiler kullanılan toodelve nasıl içerik tooyour istemcileri ve toofine ayarlama CDN davranışı tooimprove veri teslimat performansı sunulmasını içine daha derin olabilir.

### <a name="accessing-hello-edge-performance-reports"></a>Merhaba kenar performans raporları erişme
1. Merhaba CDN profili dikey penceresinden hello tıklayın **Yönet** düğmesi.
   
    ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-edge-performance/cdn-manage-btn.png)
   
    Merhaba CDN Yönetim Portalı açar.
2. Merhaba üzerine getirin **Analytics** sekmesini ve ardından hello üzerine getirin **kenar Perfomance Analytics** çıkma.  Tıklayın **HTTP büyük nesne**.
   
    Merhaba kenar düğümü analizi raporları ekran görüntülenir.

| Rapor | Açıklama |
| --- | --- |
| Günlük özeti |Belirtilen bir süre boyunca tooview günlük trafiği eğilimleri sağlar. Bu grafik her çubuğunda belirli bir tarih temsil eder. Merhaba çubuğu Hello boyutunu hello toplam sayısı belirli bir tarihte oluşan gösterir. |
| Saatlik özeti |Belirtilen bir süre boyunca tooview saatlik trafiği eğilimleri sağlar. Bu grafik her çubuğunda belirli bir tarihte tek bir saat temsil eder. Merhaba çubuğu Hello boyutunu hello toplam sayısı bu saatte oluşan gösterir. |
| Protokoller |Merhaba HTTP ve HTTPS protokolleri arasındaki trafiği Hello dökümünü gösterir. Bir halka grafik Protokolü her tür için oluştu isabet hello yüzdesini gösterir. |
| HTTP yöntemleri |Hangi HTTP yöntemlerine hızlı bir fikir olan tooget sağlayan verilerinizi kullanılan toorequest bırakılıyor. Genellikle hello en sık kullanılan HTTP istek yöntemleri, GET, HEAD ve POST yayımlanır. Bir halka grafik HTTP istek yöntemi her tür için oluştu isabet hello yüzdesini gösterir. |
| URL'leri |Merhaba üst 10 istenen URL görüntüleyen bir grafik içerir. Her URL için bir çubuk görüntülenir. belirli URL hello zaman aralığı içinde üretti kaç tane isabet hello raporun kapsadığı hello çubuğu Hello yüksekliğini gösterir. Merhaba ilk 100 istatistiklerini URL'leri doğrudan bu grafiğin altında gösterilen istedi. |
| CNAMEs |Merhaba üst 10 kullanılan CNAME'ler toorequest varlıklar üzerinde bir rapor hello zaman aralığını görüntüleyen bir grafik içerir. Merhaba ilk 100 istatistiklerini CNAME'ler doğrudan bu grafiğin altında gösterilen istedi. |
| Çıkış |Varlıklar belirtilen bir süre boyunca istendi hello ilk 10 CDN veya müşteri kaynak sunucuları görüntüleyen bir grafik içerir. Merhaba ilk 100 istatistiklerini CDN veya müşteri kaynak sunucuları doğrudan bu grafiğin altında gösterilen istedi. Müşteri kaynak sunucuları hello dizin adı seçeneği tanımlanan hello ad tarafından tanımlanır. |
| Coğrafi POP |Trafiğinizi ne kadarının bir belirli noktası bulunma (POP) yönlendirilen gösterir. Merhaba üç harfli bir POP bizim CDN ağdaki temsil eder. |
| İstemciler |Belirtilen bir süre boyunca varlıklar istenen hello üst 10 istemcileri görüntüleyen bir grafik içerir. Bu rapor Hello amaçlarla kaynaklanan tüm istekleri hello aynı IP adresi toobe hello gelen kabul aynı istemci. Merhaba üst 100 istemci için istatistikleri doğrudan bu grafiğin altında görüntülenir. Bu rapor, üst istemciler için yükleme etkinlik desenlerini belirlemek için kullanışlıdır. |
| Önbellek durumları |Geliştirme yaklaşımlar gösterebilir önbellek davranışını ayrıntılı bir dökümünü verir hello genel son kullanıcı deneyimi. Hello hızlı performans Önbelleği İsabetli Okuma gelen olduğundan, veri teslim hızlarını en aza İsabetsiz Önbellek okuma sayısı ve süresi dolan Önbelleği İsabetli Okuma göre en iyi duruma getirebilirsiniz. |
| Hiçbiri ayrıntıları |Merhaba üst 10 URL'ler için önbellek içerik yenilik belirtilen bir süre boyunca denetlendi olmayan varlıklar için görüntüleyen bir grafik içerir. Üst 100 URL'lerini Varlık türlerinin hello istatistiklerini doğrudan bu grafiğin altında görüntülenir. |
| CONFIG_NOCACHE ayrıntıları |Merhaba ilk 10 URL'leri toohello Müşteri'nin CDN yapılandırma önbelleğe alınmamış varlıklar için görüntüleyen bir grafik içerir. Bu tür varlıklar doğrudan hello kaynak sunucudan sunulduğunu. Üst 100 URL'lerini Varlık türlerinin hello istatistiklerini doğrudan bu grafiğin altında görüntülenir. |
| UNCACHEABLE ayrıntıları |Üst 10 URL'lerini toorequest üstbilgisi verileri önbelleğe alınmamış varlıklar hello görüntüleyen bir grafik içerir. Üst 100 URL'lerini Varlık türlerinin hello istatistiklerini doğrudan bu grafiğin altında görüntülenir. |
| TCP_HIT ayrıntıları |Üst 10 URL'lerini önbellekten hemen sunulan varlıklar hello görüntüleyen bir grafik içerir. Üst 100 URL'lerini Varlık türlerinin hello istatistiklerini doğrudan bu grafiğin altında görüntülenir. |
| TCP_MISS ayrıntıları |Merhaba üst 10 URL TCP_MISS önbellek durumuna sahip varlıklar için görüntüleyen bir grafik içerir. Üst 100 URL'lerini Varlık türlerinin hello istatistiklerini doğrudan bu grafiğin altında görüntülenir. |
| TCP_EXPIRED_HIT ayrıntıları |Üst 10 URL'lerini doğrudan hello POP ' sunulduğunu eski varlıklar hello görüntüleyen bir grafik içerir. Üst 100 URL'lerini Varlık türlerinin hello istatistiklerini doğrudan bu grafiğin altında görüntülenir. |
| TCP_EXPIRED_MISS ayrıntıları |Üst 10 URL'lerini hello kaynak sunucudan alınan toobe kendisi için yeni bir sürüme sahip eski varlıklar hello görüntüleyen bir grafik içerir. Üst 100 URL'lerini Varlık türlerinin hello istatistiklerini doğrudan bu grafiğin altında görüntülenir. |
| TCP_CLIENT_REFRESH_MISS ayrıntıları |Merhaba üst 10 URL varlıklar tooa Hayır önbellek isteği hello istemciden son bir kaynak sunucudan alındı için görüntüleyen bir çubuk grafik içerir. Hello üst 100 URL'ler bu türde istekler için istatistik doğrudan bu grafiğin altında görüntülenir. |
| İstemci istek türleri |HTTP istemcilerini (örn., tarayıcıları) tarafından yapılan istekleri Hello türünü belirtir. Bu rapor, istekleri işlendiğini toohow bir fikir sağlar bir halka grafik içerir. Bant genişliği ve trafik bilgileri her istek türü için aşağıdaki hello grafik görüntülenir. |
| Kullanıcı Aracısı |İçeriğinizi bizim CDN aracılığıyla hello üst 10 kullanıcı aracıları toorequest görüntüleme bir çubuk grafik içerir. Genellikle, bir kullanıcı web tarayıcısı, media player veya bir cep telefonu tarayıcı aracısıdır. Merhaba üst 100 kullanıcı aracıları için istatistikleri doğrudan bu grafiğin altında görüntülenir. |
| Başvuran |Bizim CDN erişilen hello üst 10 başvuran toocontent görüntüleyen bir çubuk grafik içerir. Genellikle, bir başvuran hello hello web sayfası veya tooyour içerik bağlantılar kaynak URL'sidir. Ayrıntılı bilgi hello grafik hello üst 100 başvuran için sağlanır. |
| Sıkıştırma türleri |İstenilen varlıkların olup bunlar, kenar sunucularımız sıkıştırılan tarafından keser bir halka grafik içeriyor. Sıkıştırılmış varlıklar Hello yüzdesi hello tarafından kullanılan sıkıştırma türünü ayrılmıştır. Ayrıntılı bilgi hello grafiğin altında her sıkıştırma türünü ve durum için sağlanır. |
| Dosya türleri |Hesabınız için bizim CDN aracılığıyla istenen hello üst 10 dosya türlerini görüntüleyen bir çubuk grafik içerir. Bu rapor Hello amaçları doğrultusunda, bir dosya türü hello varlığın dosya adı uzantısı ile tanımlanır ve Internet medya türü (örn., .html \[metin/html\], .htm \[metin/html\], .aspx \[metin/html\], vb..). Ayrıntılı bilgi hello grafik hello üst 100 dosya türleri için sağlanır. |
| Benzersiz dosyaları |Belirli bir günde belirli bir süre istenen benzersiz varlıklar toplam sayısı hello çizer bir grafik içerir. |
| Belirteç kimlik doğrulama özeti |İstenilen varlıkların belirteç tabanlı kimlik doğrulaması ile olup korunan hızlı bir genel bakış sağlayan bir pasta grafik içerir. Korunan varlıklar denenen kendi kimlik doğrulama sonuçlarını toohello göre hello grafikte görüntülenir. |
| Belirteç kimlik doğrulama ayrıntıları Reddet |TooToken tabanlı kimlik doğrulaması reddedildi tooview hello üst 10 istekleri sağlayan bir çubuk grafik içerir. |
| HTTP yanıt kodları |Merhaba HTTP durum kodları dökümünü sağlar (örn., 200 Tamam, 403 Yasak, 404 bulunamadı, vb.), teslim tooyour HTTP istemcileri, sınır sunucularımız. Pasta grafik verir tooquickly değerlendirmek varlıklarınızı nasıl sunulduğunu. Ayrıntılı istatistiksel veriler hello grafik Aşağıda her yanıt kodu sağlanır. |
| 404 hataları |Bir 404 bulunamadı yanıt kodunda sonuçlanan tooview hello üst 10 istekleri sağlayan bir çubuk grafik içerir. |
| 403 hataları |Bir 403 Yasak yanıt kodu sonuçlanan tooview hello üst 10 istekleri sağlayan bir çubuk grafik içerir. Bir müşteri kaynak sunucu veya bizim POP uç sunucusunda tarafından bir istek reddedildiğinde bir 403 Yasak yanıt kodu oluşur. |
| 4xx hataları |Yanıt kodu 400 aralıkta hello sonuçlanan tooview hello üst 10 istekleri sağlayan bir çubuk grafik içerir. Bu raporun dışında 403 olan bulunamadı ve 404 Yasak yanıt kodları. 4xx yanıt kodu genellikle, bir isteğin sonucu olarak bir istemci hatası reddedilmesi durumunda oluşur. |
| 504 hataları |504 ağ geçidi zaman aşımı yanıt kodunda sonuçlanan tooview hello üst 10 istekleri sağlayan bir çubuk grafik içerir. Bir 504 ağ geçidi zaman aşımı yanıt kodu, bir HTTP proxy toocommunicate başka bir sunucu ile çalışırken zaman aşımı ortaya çıktığında oluşur. Bir uç sunucusu müşteri kaynak sunucu ile oluşturulamıyor tooestablish iletişim bizim CDN hello durumda bir 504 ağ geçidi zaman aşımı yanıt kodu genellikle oluşur. |
| 502 hataları |502 hatalı ağ geçidi yanıt kodunda sonuçlanan tooview hello üst 10 istekleri sağlayan bir çubuk grafik içerir. Bir 502 hatalı ağ geçidi yanıt kodu, bir sunucu ve bir HTTP proxy arasında bir HTTP protokolü hatası oluştuğunda oluşur. Bir müşteri kaynak sunucu bir geçersiz yanıt tooan uç sunucusu döndüğünde bizim CDN hello durumda bir 502 hatalı ağ geçidi yanıt kodu genellikle oluşur. Bunu ayrıştırılamıyor veya tamamlanmamış ise, yanıt geçersiz. |
| 5XX hataları |Yanıt kodu hello 500 aralıktaki sonuçlanan tooview hello üst 10 istekleri sağlayan bir çubuk grafik içerir.  Bu raporun dışında 502 hatalı ağ geçidi ve 504 ağ geçidi zaman aşımı yanıt kodları'dır. |

## <a name="see-also"></a>Ayrıca bkz.
* [Azure CDN'ye genel bakış](cdn-overview.md)
* [Microsoft Azure cdn'de gerçek zamanlı İstatistikler](cdn-real-time-stats.md)
* [Merhaba kurallar altyapısı kullanarak varsayılan HTTP davranışı geçersiz kılma](cdn-rules-engine.md)
* [Gelişmiş HTTP raporları](cdn-advanced-http-reports.md)

