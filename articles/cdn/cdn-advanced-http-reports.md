---
title: "Gelişmiş HTTP raporları aaaAnalyze kullanım istatistikleri Azure CDN ile | Microsoft Docs"
description: "Microsoft Azure CDN HTTP raporlarda nasıl toocreate Gelişmiş öğrenin. Bu raporlar CDN etkinliği hakkında ayrıntılı bilgi sağlar."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: ef90adc1-580e-4955-8ff1-bde3f3cafc5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 3184ec00d089613e25c62762f93043cb4ba68394
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-usage-statistics-with-azure-cdn-advanced-http-reports"></a>Azure CDN Gelişmiş HTTP raporları kullanım istatistiklerini Çözümle
## <a name="overview"></a>Genel Bakış
Bu belgede, Microsoft Azure CDN'de Gelişmiş HTTP raporlama açıklanmaktadır. Bu raporlar CDN etkinliği hakkında ayrıntılı bilgi sağlar.

[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="accessing-advanced-http-reports"></a>Gelişmiş HTTP raporları erişme
1. Merhaba CDN profili dikey penceresinden hello tıklayın **Yönet** düğmesi.
   
    ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-advanced-http-reports/cdn-manage-btn.png)
   
    Merhaba CDN Yönetim Portalı açar.
2. Merhaba üzerine getirin **Analytics** sekmesini ve ardından hello üzerine getirin **Gelişmiş HTTP raporları** çıkma.  Tıklayın **HTTP büyük Platform**.
   
    ![CDN Yönetim Portalı - Gelişmiş Raporlar menüsü](./media/cdn-advanced-http-reports/cdn-advanced-reports.png)
   
    Rapor seçeneklerini görüntülenir.

## <a name="geography-reports-map-based"></a>Coğrafya raporları (harita tabanlı)
İçeriğinizi istenmektedir hello bölgeler harita tooindicate yararlanmak beş rapor vardır. Bu raporlar, dünya harita, Amerika Birleşik Devletleri harita, Kanada harita, Avrupa Harita ve Asya Pasifik harita içindir.

Her eşleme tabanlı rapor coğrafi varlıkları (yani, Ülkeler, durumları ve İl) derecelendirir toohello bu bölgesinden kaynaklanan isabet yüzdesi göre. Bir harita ek olarak, içeriğinizi istenmektedir hello konumları görselleştirmek toohelp sağlanır. Her bölge renk kodlama isteğe bağlı toohello miktarı according bu bölgede yaşadı şekilde mümkün toodo var. İsteğe bağlı içeriğiniz için yüksek düzeyde koyu bölgeler belirtmek sırada daha hafif gölgeli bölgeler, içerik için daha düşük talep gösterir.

Her bölge için ayrıntılı trafiği ve bant genişliği bilgileri doğrudan hello harita verilmiştir. Bu tooview hello sayısı toplam isabet, hello isabet yüzdesi, hello toplam (gigabayt cinsinden) aktarılan veri miktarını sağlar ve veri hello yüzdesi aktarılan her bölge. Bir açıklama her bu ölçümleri görüntüleyin. Bir bölge (yani, ülke, eyalet veya bölge) geldiğinizde, son olarak, hello adı ve hello hello bölgede oluştu isabet yüzdesi araç ipucu olarak görüntülenir.

Kısa bir açıklama harita tabanlı Coğrafya rapor her tür için aşağıda verilmiştir.

| Rapor adı | Açıklama |
| --- | --- |
| Dünya Haritası |Bu rapor, tooview Merhaba Dünya çapında talep CDN içeriğiniz için sağlar. Her ülkenin hello world harita tooindicate hello bu bölgesinden kaynaklanan isabet yüzdesi üzerinde kodludur. |
| Amerika Birleşik Devletleri eşleme |Bu rapor, hello Amerika Birleşik Devletleri tooview hello talep CDN içeriğiniz için sağlar. Bu harita tooindicate hello yüzdesi bu bölgesinden kaynaklanan isabetli okuma sayısının üzerinde her durum renkli kodlu. |
| Kanada eşleme |Bu rapor, CDN içeriğinizi Kanada'da tooview hello talep sağlar. Bu harita tooindicate hello yüzdesi bu bölgesinden kaynaklanan isabetli okuma sayısının üzerinde her bölge renkli kodlu. |
| Avrupa eşleme |Bu rapor, CDN içeriğinizi Avrupa'da tooview hello talep sağlar. Bu harita tooindicate hello yüzdesi bu bölgesinden kaynaklanan isabetli okuma sayısının üzerinde her ülkedeki renkli kodlu. |
| Asya Pasifik eşleme |Bu rapor, CDN içeriğinizi Asya'da tooview hello talep sağlar. Bu harita tooindicate hello yüzdesi bu bölgesinden kaynaklanan isabetli okuma sayısının üzerinde her ülkedeki renkli kodlu. |

## <a name="geography-reports-bar-charts"></a>Coğrafya raporları (çubuk grafikler)
Olan üst şehirler ve üst ülkelerde toogeography, göre istatistiksel bilgiler sağlayan iki ek rapor vardır. Bu raporlar şehirler ve ülkelerde sırasıyla toohello sayısı bu bölgelerden kaynaklanan göre derecelendirmek. Bu tür bir rapor oluşturma sırasında bir çubuk grafik hello üst 10 şehir veya belirli bir platform üzerinde içerik istenen ülkelerde gösterir. Bu çubuk grafik verir tooquickly, içerik istekleri en yüksek sayıda hello oluşturmak hello bölgeler değerlendirin.

Merhaba belirtilen bölgede kaç tane isabet oluştu Hello taraftaki hello grafiğinin (y) gösterir. Doğrudan hello grafik (x ekseni), bir etiket her hello üst 10 bölgeler için bulacaksınız.

### <a name="using-hello-bar-charts"></a>Merhaba çubuk grafikler kullanma
* Çubuğunun üzerine getirirseniz hello adı ve hello toplam sayısı hello bölgede oluşan bir araç ipucu olarak görüntülenir.
* Merhaba araç ipucu hello üst Şehir rapor için bir şehir adı, bölge ve ülke kısaltması tanımlar.
* Merhaba şehir veya bir isteğin kaynaklandığı bölge (yani, eyalet/il) belirlenemedi, bilinmeyen olduğunu gösterir. Merhaba ülke bilinmeyen sonra iki soru işareti (yani??) ise görüntülenir.
* Bir rapor "Avrupa" veya "Asya/Pasifik bölge" Merhaba ölçümleri içerebilir Bu öğeler bu bölgelerdeki tüm IP adresleri hakkında istatistiksel bilgi tooprovide değildir. Bunun yerine, bunlar yalnızca Avrupa veya Asya/Pasifik üzerinden tooa belirli şehir veya ülke yerine genişlediğini IP adreslerini kaynaklanan toorequests geçerlidir.

kullanılan toogenerate hello çubuk grafik edildi hello veri altına görüntülenebilir. İçin aktarılan verilerin hello yüzdesi hello üst 250 bölgeler ve hello toplam sayısı, isabet, hello (gigabayt cinsinden) aktarılan veri miktarını hello yüzdesi var. bulacaksınız. Bir açıklama her bu ölçümleri görüntüleyin.

Aşağıdaki rapor her iki tür için kısa bir açıklaması sağlanır.

| Rapor adı | Açıklama |
| --- | --- |
| Üst Şehir |Bu rapor, şehirler toohello sayısı bu bölgesinden kaynaklanan göre derecelendirir. |
| Üst ülkelerde |Bu rapor ülkelerde toohello sayısı bu bölgesinden kaynaklanan göre derecelendirir. |

## <a name="daily-summary"></a>Günlük özeti
Merhaba günlük Özeti raporu tooview hello toplam sayısı isabetler ve günlük olarak belirli bir platform aktarılan verileri sağlar. Bu bilgiler kullanılabilir tooquickly CDN etkinlik desenlerini keşfedilir. Örneğin, bu raporu hangi günlerinde daha yüksek deneyimli veya beklenen trafik değerinden daha düşük belirlemenize yardımcı olabilir.

Bu tür bir rapor oluşturma sırasında bir çubuk grafik görsel bir gösterge platforma özgü talep deneyimli toohello miktarı olarak günlük olarak hello hello raporun kapsadığı zaman aralığını sağlar. Bunu hello rapordaki her gün için bir çubuk görüntüleyerek görüntülemez. Örneğin, "Geçen hafta" Merhaba süre seçerek olarak adlandırılan bir çubuk grafiği yedi çubukları ile oluşturur. Her çubuk hello toplam sayısı o gün yaşadı belirtir.

Merhaba hello grafik (y) sol tarafında kaç tane isabet belirtilen hello üzerinde oluştuğunu gösteren tarih. Doğrudan hello grafik (x ekseni), başlangıç tarihi belirten bir etiket bulabilirsiniz (biçim: YYYY-AA-GG) hello rapora dahil her gün için.

> [!TIP]
> Çubuğunun üzerine getirirseniz hello toplam sayısı belirli bir tarihte oluşan bir araç ipucu olarak görüntülenir.
> 
> 

kullanılan toogenerate hello çubuk grafik edildi hello veri altına görüntülenebilir. Var. hello raporun kapsadığı her gün için hello toplam isabet sayısı ve (gigabayt cinsinden) aktarılan veri miktarını hello bulacaksınız.

## <a name="by-hour"></a>Saatlik olarak
Merhaba tarafından saat rapor tooview hello toplam sayısı isabetler ve saatlik olarak başka bir belirli bir platform aktarılan verileri sağlar. Bu bilgiler kullanılabilir tooquickly CDN etkinlik desenlerini keşfedilir. Örneğin, bu rapor, beklenen trafiğe daha düşük veya yüksek deneyimi zaman aralıklarında hello gün hello belirlemenize yardımcı olabilir.

Bu tür bir rapor oluşturma sırasında bir çubuk grafik toohello miktarını saatlik olarak başka bir hello hello raporun kapsadığı zaman aralığını yaşadı platforma özgü isteğe bağlı olarak görsel bir gösterge sağlar. Bunu hello raporun kapsadığı her saatte bir çubuk görüntüleyerek görüntülemez. Örneğin, 24 saatlik seçerek süre bir çubuk grafiği yirmi dört çubukları ile oluşturur. Her çubuk hello toplam sayısı bu saatte yaşadı belirtir.

kaç tane isabet hello belirtilen saatte oluştu Hello taraftaki hello grafiğinin (y) gösterir. Doğrudan hello grafik (x ekseni), başlangıç tarihi/saati belirten bir etiket bulabilirsiniz (biçim: YYYY-AA-GG ss: dd) hello rapora dahil her saat. 24 saat biçimini kullanarak bildirilen süresi ve hello UTC/GMT saat dilimi kullanılarak belirtilir.

> [!TIP]
> Çubuğunun üzerine getirirseniz hello toplam sayısı bu saatte oluşan bir araç ipucu olarak görüntülenir.
> 
> 

kullanılan toogenerate hello çubuk grafik edildi hello veri altına görüntülenebilir. Var. hello raporun kapsadığı her saatte hello toplam isabet sayısı ve (gigabayt cinsinden) aktarılan veri miktarını hello bulacaksınız.

## <a name="by-file"></a>Dosya tarafından
Merhaba tarafından dosya en, tooview hello talep ve hello trafik miktarı hello için belirli bir platform üzerinde oluşturulan rapor verir varlıklar istedi. Bu tür bir rapor oluşturma sırasında bir çubuk grafik hello üst 10 en çok istenen varlıklar üzerinde süre belirtilen hello oluşturulur.

> [!NOTE]
> Merhaba bu raporun, kenar CNAME URL'leri dönüştürülmüş tootheir eşdeğer CDN URL'leri amaçlıdır. Bu, hello toplam isabet sayısı için doğru bir tally hello CDN veya edge CNAME kullanılan URL toorequest bağımsız olarak bir varlığı ile ilişkili sağlar.
> 
> 

Merhaba taraftaki hello grafiğinin (y) hello süre belirtilen her varlık için istekleri hello sayısını gösterir. Doğrudan hello grafik (x ekseni), her hello üst 10 istenilen varlıkların hello dosya adını belirten bir etiket bulacaksınız.

kullanılan toogenerate hello çubuk grafik edildi hello veri altına görüntülenebilir. Her hello üst 250 istenen varlıklar için bilgileri aşağıdaki hello var. bulacaksınız: göreli yol, hello toplam sayısı isabet, hello isabet yüzdesi, hello (gigabayt cinsinden) aktarılan veri miktarını ve aktarılan verilerin hello yüzdesi.

## <a name="by-file-detail"></a>Dosya ayrıntısı
Merhaba tarafından dosya ayrıntı raporu tooview hello belirli bir varlık için belirli bir platform üzerinde ücrete talep ve hello trafik miktarı sağlar. Merhaba bu raporun üstündeki hello dosya ayrıntıları için bir seçenektir. Bu seçenek hello seçili platformda en çok istenen varlıklarınızı listesini sağlar. Sipariş toogenerate tarafından dosya ayrıntı raporu, tooselect hello istenen varlığından hello dosya ayrıntıları seçeneği gerekir. Sonrasında, çubuk grafik süre belirtilen hello oluşturulan günlük isteğe bağlı hello miktarını gösterir.

Merhaba grafik (y), sol taraftaki Hello hello isteği sayısı, bir varlığın belirli bir günde yaşadı gösterir. Doğrudan hello grafik (x ekseni), başlangıç tarihi belirten bir etiket bulabilirsiniz (biçim: YYYY-AA-GG) hangi CDN talep hello için varlık bildirildi.

kullanılan toogenerate hello çubuk grafik edildi hello veri altına görüntülenebilir. Var. hello raporun kapsadığı her gün için hello toplam isabet sayısı ve (gigabayt cinsinden) aktarılan veri miktarını hello bulacaksınız.

## <a name="by-file-type"></a>Dosya türü
Merhaba dosya türüne göre raporu, tooview hello dosya türüne göre ücrete talep ve hello trafik miktarı sağlar. Bu tür bir rapor oluşturma sırasında bir halka grafik hello hello üst 10 dosya türleri tarafından oluşturulan isabet yüzdesi belirtir.

> [!TIP]
> Merhaba halka grafikte bir dilim üzerine getirirseniz hello Internet medya dosya türü araç ipucu olarak görüntülenir türü.
> 
> 

kullanılan toogenerate hello halka grafik edildi hello veri altına görüntülenebilir. Vardır, bulacaksınız hello dosya adı uzantısı/Internet medya türü, hello toplam isabet sayısı, hello isabet yüzdesi, hello (gigabayt cinsinden) aktarılan veri miktarını ve hello her hello için aktarılan verilerin yüzdesi top 250 dosya türleri.

## <a name="by-directory"></a>Dizin ile
Merhaba tarafından dizin rapor tooview hello belirli bir dizinden içerik için belirli bir platform üzerinde ücrete talep ve hello trafik miktarı sağlar. Bu tür bir rapor oluşturma sırasında bir çubuk grafik hello toplam sayısı hello üst 10 dizinlerde içerik tarafından oluşturulan belirtir.

### <a name="using-hello-bar-chart"></a>Merhaba çubuk grafik kullanma
* Çubuğunun üzerine getirin tooview hello göreli yol toohello karşılık gelen dizini.
* Bir dizinin bir alt klasöründe depolanan içerik isteğe bağlı dizin hesaplanırken sayılmaz. Bu hesaplama yalnızca hello gerçek dizinde saklanan içerik için oluşturulan istek hello sayısı kullanır.
* Merhaba bu raporun, kenar CNAME URL'leri dönüştürülmüş tootheir eşdeğer CDN URL'leri amaçlıdır. Bu, tüm istatistikler için doğru bir tally hello CDN veya edge CNAME kullanılan URL toorequest bağımsız olarak bir varlığı ile ilişkili sağlar.

Merhaba hello grafik (y) sol tarafındaki üst 10 dizinlerde depolanan hello içerik isteklerini hello toplam sayısını gösterir. Her çubuk hello grafikte bir dizin temsil eder. Bir çubuk yukarı düzeni toomatch renk kodlama kullanım hello tooa dizin hello üst 250 tam dizinleri bölümünde listelenen.

kullanılan toogenerate hello çubuk grafik edildi hello veri altına görüntülenebilir. Her hello üst 250 dizinlerin bilgisinden hello var. bulacaksınız: göreli yol, hello toplam sayısı isabet, hello isabet yüzdesi, hello (gigabayt cinsinden) aktarılan veri miktarını ve aktarılan verilerin hello yüzdesi.

## <a name="by-browser"></a>Tarayıcı tarafından
Merhaba tarayıcı tarafından rapor hangi tarayıcılar kullanılan toorequest içerik olan tooview sağlar. Bu tür bir rapor oluşturma sırasında pasta grafiği hello hello üst 10 tarayıcılar tarafından işlenen isteklerin yüzdesini belirtir.

### <a name="using-hello-pie-chart"></a>Merhaba pasta grafik kullanma
* Bir dilim hello pasta grafik tooview, tarayıcının adı ve sürümü üzerine gelerek.
* Bu rapor Hello amaçları doğrultusunda, her benzersiz tarayıcı/sürüm bileşimi farklı bir tarayıcı olarak kabul edilir.
* "Diğer" olarak adlandırılan hello dilim hello diğer tüm tarayıcılar ve sürümleri tarafından işlenen isteklerin yüzdesini gösterir.

kullanılan toogenerate hello pasta grafik edildi hello veri altına görüntülenebilir. Var. hello tarayıcı türü/sürüm numarası, hello toplam isabet sayısı ve her hello üst 250 tarayıcıların isabet yüzdesi hello bulacaksınız.

## <a name="by-referrer"></a>Göre başvuran
Merhaba tarafından başvuran rapor hello seçili platformda tooview hello üst başvuran toocontent sağlar. Bir başvuran bir istek oluşturulduğu hello hostname gösterir. Bu tür bir rapor oluşturma sırasında isteğe bağlı (yani, isabet) hello miktarını hello üst 10 başvuran tarafından oluşturulan bir çubuk grafik gösterir.

Merhaba grafik (y), sol taraftaki Hello hello isteği sayısı, bir varlık için her başvuran yaşadı gösterir. Her çubuk hello grafikte bir başvuran temsil eder. Bir çubuk yukarı düzeni toomatch renk kodlama kullanım hello tooa başvuran hello üst 250 başvuran bölümünde listelenen.

kullanılan toogenerate hello çubuk grafik edildi hello veri altına görüntülenebilir. Var. hello URL, hello toplam isabet sayısı ve her hello üst 250 başvuran oluşturulan isabet yüzdesi hello bulacaksınız.

## <a name="by-download"></a>Tarafından indirme
Merhaba tarafından karşıdan rapor tooanalyze indirme desenleri en çok istenen içeriğiniz için sağlar. Merhaba rapor Hello üst hello için tamamlanan yükleme denemesi karşılaştırır yüklemeleriyle 10 istenilen varlıkların üst bir çubuk grafik içerir. Her çubuk olmasından toowhether denenen karşıdan yükleme (mavi) veya tamamlanan yükleme (yeşil) göre renkli kodlu.

> [!NOTE]
> Merhaba bu raporun, kenar CNAME URL'leri dönüştürülmüş tootheir eşdeğer CDN URL'leri amaçlıdır. Bu, tüm istatistikler için doğru bir tally hello CDN veya edge CNAME kullanılan URL toorequest bağımsız olarak bir varlığı ile ilişkili sağlar.
> 
> 

Hello taraftaki hello grafiğinin (y) her hello üst 10 istenilen varlıkların hello dosya adını belirtir. Doğrudan hello grafiğin (x ekseni) çalıştı ve tamamlanan yüklemeleri hello toplam sayısını belirtmek etiketleri bulacaksınız.

Doğrudan hello çubuk grafiği bilgileri aşağıdaki hello listelenir hello üst 250 istenen varlıklar için: göreli yolu (dosya adı dahil), hello sayısı indirilen toocompletion, hello sayısı, istenen ve hello edildi tam bir indirme sonuçlandı istekleri yüzdesi.

> [!TIP]
> Bizim CDN HTTP istemci (yani tarayıcısı) bilgisi verilmediği ne zaman bir varlık tamamen indirilir. Sonuç olarak, bir varlık tamamen according toostatus kodları ve bayt aralığı isteklerini indirildi olup olmadığını biz toocalculate sahip. Bu hesaplamayı yapmak olup hello isteği 200 Tamam durum koduna sonuçları olduğunda hello ilk şey biz arayın. Bu durumda, ardından biz bayt aralığı isteklerini tooensure hello tüm varlık kapak arayın. Son olarak, aktarılan verilerin toohello hello istenen varlık boyutunu hello miktarını karşılaştırın. Merhaba veri aktardıysanız eşit tooor hello dosya boyutundan daha büyük ve hello isabet tam bir yükleme olarak sayılır sonra hello bayt aralığı isteklerini bu varlık için uygundur.
> 
> Toohello interpretive yapısı bu raporun, hello tutarlılık ve bu raporun doğruluğunu alter noktaları aşağıdaki göz hello tutmanız gerekir.
> 
> * Kullanıcı aracılarına farklı davranır olduğunda trafiği desenlerini doğru şekilde tahmin edilemez. Bu, % 100'den büyük olan tamamlanan yükleme sonuçlara neden olabilir.
> * HTTP aşamalı indirme yararlanmak varlıklar doğru şekilde bu rapor tarafından temsil edilebilir değil. Bir video toousers arama toodifferent konumları nedeniyle budur.
> 
> 

## <a name="by-404-errors"></a>404 hataları
Merhaba tarafından 404 hataları rapor tooidentify hello hello 404 bulunamadı durum kodlarını pek çok sayı oluşturur içerik türünü sağlar. Merhaba rapor Hello üst 404 bulunamadı durum kodu en iyi duruma döndürüldü hello ilk 10 varlıklar için bir çubuk grafik içerir. Bu çubuk grafik hello isteği sayısı, o varlıklar için 404 bulunamadı durum kodu ile sonuçlandı istekleri ile karşılaştırır. Her çubuk renk kodludur. Sarı çubuğu kullanılan istek hello tooindicate 404 bulunamadı durum koduna sonuçlandı. Kırmızı çubuğu kullanılan tooindicate hello toplam istek sayısı hello varlık için.

> [!NOTE]
> Bu rapor Hello amaçlarla hello aşağıdakileri göz önünde bulundurun:
> 
> * İsabet herhangi bir istek durum kodu bakılmaksızın bir varlık için temsil eder.
> * Edge CNAME URL'leri dönüştürülmüş tootheir eşdeğer CDN URL'leri ' dir. Bu, tüm istatistikler için doğru bir tally hello CDN veya edge CNAME kullanılan URL toorequest bağımsız olarak bir varlığı ile ilişkili sağlar.
> 
> 

Hello taraftaki hello grafiğinin (y) her 404 bulunamadı durum koduna sonuçlanan hello üst 10 istenilen varlıkların hello dosya adını belirtir. Doğrudan hello grafiğin (x ekseni) hello toplam istek sayısı ve 404 bulunamadı durum koduna sonuçlanan istek hello sayısını belirten etiketler bulabilirsiniz.

Doğrudan hello çubuk grafiği bilgileri aşağıdaki hello listelenir hello üst 250 istenen varlıklar için: hello 404 bulunamadı durum koduna, hello toplam sayısı varlık hello sonuçlanan istek sayısı, göreli yol (içeren dosya adı) oluştu İstenen ve 404 bulunamadı durum koduna sonuçlandı isteklerin hello.

## <a name="see-also"></a>Ayrıca bkz.
* [Azure CDN'ye genel bakış](cdn-overview.md)
* [Microsoft Azure cdn'de gerçek zamanlı İstatistikler](cdn-real-time-stats.md)
* [Merhaba kurallar altyapısı kullanarak varsayılan HTTP davranışı geçersiz kılma](cdn-rules-engine.md)
* [Edge performansını çözümleme](cdn-edge-performance.md)

